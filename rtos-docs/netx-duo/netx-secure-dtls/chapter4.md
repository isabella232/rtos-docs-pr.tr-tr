---
title: Bölüm 4-Azure RTOS NetX güvenli DTLS hizmetlerinin açıklaması
description: Bu bölümde, alfabetik sırada listelenen tüm Azure RTOS NetX güvenli DTLS hizmetlerinin açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: e795a5fa35a4590e508c7fe2eec53f5494809657
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825690"
---
# <a name="chapter-4-description-of-azure-rtos-netx-secure-dtls-services"></a><span data-ttu-id="7d363-103">Bölüm 4: Azure RTOS NetX güvenli DTLS hizmetlerinin açıklaması</span><span class="sxs-lookup"><span data-stu-id="7d363-103">Chapter 4: Description of Azure RTOS NetX Secure DTLS services</span></span>

<span data-ttu-id="7d363-104">Bu bölüm, tüm Azure RTOS NetX güvenli DTLS hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="7d363-104">This chapter contains a description of all Azure RTOS NetX Secure DTLS services (listed below) in alphabetic order.</span></span>

<span data-ttu-id="7d363-105">Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_SECURE_DISABLE_ERROR_CHECKING** makrodan etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="7d363-105">In the “Return Values” section in the following API descriptions, values in **BOLD** are not affected by the **NX_SECURE_DISABLE_ERROR_CHECKING** macro that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

- [<span data-ttu-id="7d363-106">nx_secure_dtls_client_session_start</span><span class="sxs-lookup"><span data-stu-id="7d363-106">nx_secure_dtls_client_session_start</span></span>](#nx_secure_dtls_client_session_start)
- [<span data-ttu-id="7d363-107">nx_secure_dtls_packet_allocate</span><span class="sxs-lookup"><span data-stu-id="7d363-107">nx_secure_dtls_packet_allocate</span></span>](#nx_secure_dtls_packet_allocate)
- [<span data-ttu-id="7d363-108">nx_secure_dtls_psk_add</span><span class="sxs-lookup"><span data-stu-id="7d363-108">nx_secure_dtls_psk_add</span></span>](#nx_secure_dtls_psk_add)
- [<span data-ttu-id="7d363-109">nx_secure_dtls_server_create</span><span class="sxs-lookup"><span data-stu-id="7d363-109">nx_secure_dtls_server_create</span></span>](#nx_secure_dtls_server_create)
- [<span data-ttu-id="7d363-110">nx_secure_dtls_server_delete</span><span class="sxs-lookup"><span data-stu-id="7d363-110">nx_secure_dtls_server_delete</span></span>](#nx_secure_dtls_server_delete)
- [<span data-ttu-id="7d363-111">nx_secure_dtls_server_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="7d363-111">nx_secure_dtls_server_local_certificate_add</span></span>](#nx_secure_dtls_server_local_certificate_add)
- [<span data-ttu-id="7d363-112">nx_secure_dtls_server_local_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="7d363-112">nx_secure_dtls_server_local_certificate_remove</span></span>](#nx_secure_dtls_server_local_certificate_remove)
- [<span data-ttu-id="7d363-113">nx_secure_dtls_server_notify_set</span><span class="sxs-lookup"><span data-stu-id="7d363-113">nx_secure_dtls_server_notify_set</span></span>](#nx_secure_dtls_server_notify_set)
- [<span data-ttu-id="7d363-114">nx_secure_dtls_server_psk_add</span><span class="sxs-lookup"><span data-stu-id="7d363-114">nx_secure_dtls_server_psk_add</span></span>](#nx_secure_dtls_server_psk_add)
- [<span data-ttu-id="7d363-115">nx_secure_dtls_server_session_send</span><span class="sxs-lookup"><span data-stu-id="7d363-115">nx_secure_dtls_server_session_send</span></span>](#nx_secure_dtls_server_session_send)
- [<span data-ttu-id="7d363-116">nx_secure_dtls_server_session_start</span><span class="sxs-lookup"><span data-stu-id="7d363-116">nx_secure_dtls_server_session_start</span></span>](#nx_secure_dtls_server_session_start)
- [<span data-ttu-id="7d363-117">nx_secure_dtls_server_start</span><span class="sxs-lookup"><span data-stu-id="7d363-117">nx_secure_dtls_server_start</span></span>](#nx_secure_dtls_server_start)
- [<span data-ttu-id="7d363-118">nx_secure_dtls_server_stop</span><span class="sxs-lookup"><span data-stu-id="7d363-118">nx_secure_dtls_server_stop</span></span>](#nx_secure_dtls_server_stop)
- [<span data-ttu-id="7d363-119">nx_secure_dtls_server_trusted_certificate_add</span><span class="sxs-lookup"><span data-stu-id="7d363-119">nx_secure_dtls_server_trusted_certificate_add</span></span>](#nx_secure_dtls_server_trusted_certificate_add)
- [<span data-ttu-id="7d363-120">nx_secure_dtls_server_trusted_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="7d363-120">nx_secure_dtls_server_trusted_certificate_remove</span></span>](#nx_secure_dtls_server_trusted_certificate_remove)
- [<span data-ttu-id="7d363-121">nx_secure_dtls_server_x509_client_verify_configure</span><span class="sxs-lookup"><span data-stu-id="7d363-121">nx_secure_dtls_server_x509_client_verify_configure</span></span>](#nx_secure_dtls_server_x509_client_verify_configure)
- [<span data-ttu-id="7d363-122">nx_secure_dtls_server_x509_client_verify_disable</span><span class="sxs-lookup"><span data-stu-id="7d363-122">nx_secure_dtls_server_x509_client_verify_disable</span></span>](#nx_secure_dtls_server_x509_client_verify_disable)
- [<span data-ttu-id="7d363-123">nx_secure_dtls_session_client_info_get</span><span class="sxs-lookup"><span data-stu-id="7d363-123">nx_secure_dtls_session_client_info_get</span></span>](#nx_secure_dtls_session_client_info_get)
- [<span data-ttu-id="7d363-124">nx_secure_dtls_session_create</span><span class="sxs-lookup"><span data-stu-id="7d363-124">nx_secure_dtls_session_create</span></span>](#nx_secure_dtls_session_create)
- [<span data-ttu-id="7d363-125">nx_secure_dtls_session_delete</span><span class="sxs-lookup"><span data-stu-id="7d363-125">nx_secure_dtls_session_delete</span></span>](#nx_secure_dtls_session_delete)
- [<span data-ttu-id="7d363-126">nx_secure_dtls_session_end</span><span class="sxs-lookup"><span data-stu-id="7d363-126">nx_secure_dtls_session_end</span></span>](#nx_secure_dtls_session_end)
- [<span data-ttu-id="7d363-127">nx_secure_dtls_session_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="7d363-127">nx_secure_dtls_session_local_certificate_add</span></span>](#nx_secure_dtls_session_local_certificate_add)
- [<span data-ttu-id="7d363-128">nx_secure_dtls_session_local_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="7d363-128">nx_secure_dtls_session_local_certificate_remove</span></span>](#nx_secure_dtls_session_local_certificate_remove)
- [<span data-ttu-id="7d363-129">nx_secure_dtls_session_receive</span><span class="sxs-lookup"><span data-stu-id="7d363-129">nx_secure_dtls_session_receive</span></span>](#nx_secure_dtls_session_receive)
- [<span data-ttu-id="7d363-130">nx_secure_dtls_session_reset</span><span class="sxs-lookup"><span data-stu-id="7d363-130">nx_secure_dtls_session_reset</span></span>](#nx_secure_dtls_session_reset)
- [<span data-ttu-id="7d363-131">nx_secure_dtls_ session_send</span><span class="sxs-lookup"><span data-stu-id="7d363-131">nx_secure_dtls_ session_send</span></span>](#nx_secure_dtls_-session_send)
- [<span data-ttu-id="7d363-132">nx_secure_dtls_session_trusted_certificate_add</span><span class="sxs-lookup"><span data-stu-id="7d363-132">nx_secure_dtls_session_trusted_certificate_add</span></span>](#nx_secure_dtls_session_trusted_certificate_add)
- [<span data-ttu-id="7d363-133">nx_secure_dtls_session_trusted_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="7d363-133">nx_secure_dtls_session_trusted_certificate_remove</span></span>](#nx_secure_dtls_session_trusted_certificate_remove)


## <a name="nx_secure_dtls_client_session_start"></a><span data-ttu-id="7d363-134">nx_secure_dtls_client_session_start</span><span class="sxs-lookup"><span data-stu-id="7d363-134">nx_secure_dtls_client_session_start</span></span>

<span data-ttu-id="7d363-135">NetX güvenli DTLS Istemci oturumu başlatma</span><span class="sxs-lookup"><span data-stu-id="7d363-135">Start a NetX Secure DTLS Client Session</span></span>

### <a name="prototype"></a><span data-ttu-id="7d363-136">Prototype</span><span class="sxs-lookup"><span data-stu-id="7d363-136">Prototype</span></span>

```C
UINT nx_secure_dtls_client_session_start(
                        NX_SECURE_DTLS_SESSION *dtls_session,
                        NX_UDP_SOCKET *udp_socket,
                        NXD_ADDRESS *ip_address, UINT port,
                        UINT wait_option);

```

### <a name="description"></a><span data-ttu-id="7d363-137">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7d363-137">Description</span></span>

<span data-ttu-id="7d363-138">Bu hizmet, ağ iletişimleri için belirtilen UDP yuvasını kullanarak, belirtilen IP adresi ve UDP bağlantı noktasındaki sunucuya bağlanan bir DTLS Istemci oturumu başlatır.</span><span class="sxs-lookup"><span data-stu-id="7d363-138">This service starts a DTLS Client session, connecting to the server at the provided IP address and UDP port, using the provided UDP socket for network communications.</span></span>

<span data-ttu-id="7d363-139">Bu hizmet nx_secure_dtls_session_create kullanılarak çağrılmadan önce DTLS oturum denetim bloğunun başlatılmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d363-139">The DTLS session control block must be initialized prior to calling this service using nx_secure_dtls_session_create.</span></span> <span data-ttu-id="7d363-140">Ayrıca, DTLS Istemcisi nx_secure_dtls_session_trusted_certificate_add veya önceden paylaşılan anahtarlar etkin ve yapılandırılmış olarak oturum için en az bir güvenilir CA sertifikası eklenmiş olmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="7d363-140">Additionally, the DTLS Client requires that at least one trusted CA certificate has been added to the session using nx_secure_dtls_session_trusted_certificate_add or Pre-Shared Keys are enabled and configured.</span></span>

### <a name="parameters"></a><span data-ttu-id="7d363-141">Parametreler</span><span class="sxs-lookup"><span data-stu-id="7d363-141">Parameters</span></span>

- <span data-ttu-id="7d363-142">**dtls_session** Daha önce başlatılmış olan DTLS oturum yapısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="7d363-142">**dtls_session** Pointer to a DTLS Session structure that was initialized previously.</span></span>
- <span data-ttu-id="7d363-143">**udp_socket** Uzak DTLS sunucusuyla ağ iletişimi kurmak için kullanılacak UDP yuvası başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="7d363-143">**udp_socket** Initialized UDP socket that will be used to establish network communications with the remote DTLS server.</span></span>
- <span data-ttu-id="7d363-144">**ip_address** Uzak DTLS sunucusunun adresini içeren IP adresi yapısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="7d363-144">**ip_address** Pointer to IP address structure containing the address of the remote DTLS server.</span></span>
- <span data-ttu-id="7d363-145">**bağlantı noktası** Uzak DTLS sunucusuyla ağ iletişimi kurmak için kullanılacak UDP yuvası başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="7d363-145">**port** Initialized UDP socket that will be used to establish network communications with the remote DTLS server.</span></span>
- <span data-ttu-id="7d363-146">**wait_option** Bağlantı girişimi için askıya alma seçeneği.</span><span class="sxs-lookup"><span data-stu-id="7d363-146">**wait_option** Suspension option for connection attempt.</span></span>

### <a name="return-values"></a><span data-ttu-id="7d363-147">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="7d363-147">Return Values</span></span>

- <span data-ttu-id="7d363-148">**NX_SUCCESS** (0x00) sertifikanın oturumun başarıyla atanması.</span><span class="sxs-lookup"><span data-stu-id="7d363-148">**NX_SUCCESS** (0x00) Successful assignment of certificate to session.</span></span>
- <span data-ttu-id="7d363-149">**NX_NOT_CONNECTED** (0x38) sunucuya, belirtilen adreste ve bağlantı noktasında ulaşılamıyor.</span><span class="sxs-lookup"><span data-stu-id="7d363-149">**NX_NOT_CONNECTED** (0x38) The server cannot be reached at the given address and port.</span></span>
- <span data-ttu-id="7d363-150">**NX_SECURE_TLS_UNRECOGNIZED_MESSAGE_TYPE** (0x102) ALıNAN bir TLS/DTLS ileti türü yanlış.</span><span class="sxs-lookup"><span data-stu-id="7d363-150">**NX_SECURE_TLS_UNRECOGNIZED_MESSAGE_TYPE** (0x102) A received TLS/DTLS message type is incorrect.</span></span>
- <span data-ttu-id="7d363-151">**NX_SECURE_TLS_UNSUPPORTED_CIPHER** (0x106) uzak ana bilgisayar tarafından sağlanmış bir şifre desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="7d363-151">**NX_SECURE_TLS_UNSUPPORTED_CIPHER** (0x106) A cipher provided by the remote host is not supported.</span></span>
- <span data-ttu-id="7d363-152">TLS el sıkışması sırasında **NX_SECURE_TLS_HANDSHAKE_FAILURE** (0x107) ileti işleme başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="7d363-152">**NX_SECURE_TLS_HANDSHAKE_FAILURE** (0x107) Message processing during the TLS handshake has failed.</span></span>
- <span data-ttu-id="7d363-153">**NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0x108) gelen bir ILETI karma Mac denetiminde başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="7d363-153">**NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0x108) An incoming message failed a hash MAC check.</span></span>
- <span data-ttu-id="7d363-154">**NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) temel alınan TCP yuvası gönderme başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="7d363-154">**NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) An underlying TCP socket send failed.</span></span>
- <span data-ttu-id="7d363-155">**NX_SECURE_TLS_INCORRECT_MESSAGE_LENGTH** (0x10a) gelen iletide geçersiz uzunluk alanı vardı.</span><span class="sxs-lookup"><span data-stu-id="7d363-155">**NX_SECURE_TLS_INCORRECT_MESSAGE_LENGTH** (0x10A) An incoming message had an invalid length field.</span></span>
- <span data-ttu-id="7d363-156">**NX_SECURE_TLS_BAD_CIPHERSPEC** (0x10b) gelen bir Changecyaspec iletisi hatalı.</span><span class="sxs-lookup"><span data-stu-id="7d363-156">**NX_SECURE_TLS_BAD_CIPHERSPEC** (0x10B) An incoming ChangeCipherSpec message was incorrect.</span></span>
- <span data-ttu-id="7d363-157">**NX_SECURE_TLS_INVALID_SERVER_CERT** (0x10c) uzak DTLS sunucusunu tanımlamak Için gelen bir TLS sertifikası kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="7d363-157">**NX_SECURE_TLS_INVALID_SERVER_CERT** (0x10C) An incoming TLS certificate is unusable for identifying the remote DTLS server.</span></span>
- <span data-ttu-id="7d363-158">**NX_SECURE_TLS_UNSUPPORTED_PUBLIC_CIPHER** (0x10d) uzak ana bilgisayar tarafından sunulan ortak anahtar şifresi desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="7d363-158">**NX_SECURE_TLS_UNSUPPORTED_PUBLIC_CIPHER** (0x10D) The public-key cipher provided by the remote host is unsupported.</span></span>
- <span data-ttu-id="7d363-159">**NX_SECURE_TLS_NO_SUPPORTED_CIPHERS** (0x10e) uzak ana bilgisayar, NETX GÜVENLI DTLS yığını tarafından desteklenen bir ciphersuites belirtti.</span><span class="sxs-lookup"><span data-stu-id="7d363-159">**NX_SECURE_TLS_NO_SUPPORTED_CIPHERS** (0x10E) The remote host has indicated no ciphersuites that are supported by the NetX Secure DTLS stack.</span></span>
- <span data-ttu-id="7d363-160">**NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0x10F) ALıNAN DTLS iletisinin üstbilgisinde bilinmeyen DTLS sürümü vardı.</span><span class="sxs-lookup"><span data-stu-id="7d363-160">**NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0x10F) A received DTLS message had an unknown DTLS version in its header.</span></span>
- <span data-ttu-id="7d363-161">**NX_SECURE_TLS_UNSUPPORTED_TLS_VERSION** (0x110) ALıNAN DTLS iletisi üstbilgisinde bilinen ancak desteklenmeyen bir DTLS sürümü vardı.</span><span class="sxs-lookup"><span data-stu-id="7d363-161">**NX_SECURE_TLS_UNSUPPORTED_TLS_VERSION** (0x110) A received DTLS message had a known but unsupported DTLS version in its header.</span></span>
- <span data-ttu-id="7d363-162">**NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) BIR iç TLS paket ayırması başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="7d363-162">**NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) An internal TLS packet allocation failed.</span></span>
- <span data-ttu-id="7d363-163">**NX_SECURE_TLS_INVALID_CERTIFICATE** (0x112) uzak ana bilgisayar geçersiz bir sertifika sağladı.</span><span class="sxs-lookup"><span data-stu-id="7d363-163">**NX_SECURE_TLS_INVALID_CERTIFICATE** (0x112) The remote host provided an invalid certificate.</span></span>
- <span data-ttu-id="7d363-164">**NX_SECURE_TLS_ALERT_RECEIVED** (0x114) uzak ana bilgisayar bir hatayı BELIRTEN ve TLS oturumunu sonlandıran bir uyarı gönderdi.</span><span class="sxs-lookup"><span data-stu-id="7d363-164">**NX_SECURE_TLS_ALERT_RECEIVED** (0x114) The remote host sent an alert indicating an error and ending the TLS session.</span></span>
- <span data-ttu-id="7d363-165">**NX_SECURE_TLS_MISSING_CRYPTO_ROUTINE** (0x13b) ciphersuite tablosundaki BIR girdinin null işlev işaretçisi vardı.</span><span class="sxs-lookup"><span data-stu-id="7d363-165">**NX_SECURE_TLS_MISSING_CRYPTO_ROUTINE** (0x13B) An entry in the ciphersuite table had a NULL function pointer.</span></span>
- <span data-ttu-id="7d363-166">**NX_PTR_ERROR** (0x07) geçersiz oturum, yuva veya adres işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="7d363-166">**NX_PTR_ERROR** (0x07) Invalid session, socket, or address pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="7d363-167">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="7d363-167">Allowed From</span></span>

<span data-ttu-id="7d363-168">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="7d363-168">Threads</span></span>

### <a name="example"></a><span data-ttu-id="7d363-169">Örnek</span><span class="sxs-lookup"><span data-stu-id="7d363-169">Example</span></span>

```C
/* Sockets, sessions, certificates defined in global static space to preserve
   application stack. */
NX_SECURE_DTLS_SESSION client_dtls_session;

/* Trusted certificate structure and raw data. */
NX_SECURE_X509_CERT trusted_cert;
const UCHAR trusted_cert_der = { … };

/* Cryptography routines and crypto work buffers. */
extern const NX_SECURE_TLS_CRYPTO nx_crypto_tls_ciphers;
UCHAR crypto_metadata[9000];

/* Packet reassembly buffer for decryption. */
UCHAR packet_buffer[4000];

/* Remote certificate buffer for incoming certificates. */
#define REMOTE_CERT_SIZE (sizeof(NX_SECURE_X509_CERT) + 2000)
#define REMOTE_CERT_NUMBER  (3)
UCHAR remote_certs_buffer[REMOTE_CERT_SIZE * REMOTE_CERT_NUMBER];

/* Application thread where TLS session is started. */
void application_thread()
{
NXD_ADDRESS server_ip;

    /* Create a TLS session for our socket. Ciphers and metadata defined
       elsewhere. See nx_secure_tls_session_create reference for more
       information. */
    status =  nx_secure_dtls_session_create(&client_dtls_session,
                                           &nx_crypto_tls_ciphers,
                                           crypto_metadata,
                                           sizeof(crypto_metadata),
                                           packet_buffer,
                                           sizeof(packet_buffer),
                                           REMOTE_CERT_NUMBER,
                                           remote_certs_buffer,
                                           sizeof(remote_certs_buffer));

    /* Check for error.  */
    if(status)
    {
        printf("Error in function nx_secure_dtls_session_create: 0x%x\n", status);
    }

    /* Initialize our trusted certificate. See section “Importing X.509
       Certificates into NetX Secure” for more information. */
    nx_secure_x509_certificate_initialize(&trusted_certificate,
                                      trusted_cert_der,
                                      trusted_cert_der_len,
                                      NX_NULL, 0, NX_NULL, 0,
                                      NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add the certificate to the local store using a numeric ID. */
    nx_secure_dtls_session_trusted_certificate_add(&client_dtls_session,
                                                   &certificate, 1);

    /* Set up IP address of remote host. */
    server_ip.nxd_ip_version = NX_IP_VERSION_V4;
    server_ip.nxd_ip_address.v4 = IP_ADDRESS(192, 168, 1, 150);


    /* Now we can start the DTLS session as normal. */
    status =  nx_secure_dtls_client_session_start(&client_dtls_session,
                                                  &udp_socket, &server_ip,
                                                  4443,
                                                  NX_IP_PERIODIC_RATE);

    if(status != NX_SUCCESS)
    {
      /* Error! */
      return(status);
    }

    /* Add data to send packet as usual for NX_PACKET and send to server.  */
    status = nx_secure_dtls_session_send(&client_dtls_session, &send_packet,
                                                        &server_ip, 4443);

    /* Receive response from server. */
    status = nx_secure_dtls_session_receive(&client_dtls_session, &receive_packet,
                                                            NX_IP_PERIODIC_RATE);

    /* Process response. */

    /* Shut down DTLS session. */
    status = nx_secure_dtls_session_end(&client_dtls_session, NX_IP_PERIODIC_RATE);

    /* Clean up. */
    status = nx_secure_dtls_session_delete(&client_dtls_session);

}

```

### <a name="see-also"></a><span data-ttu-id="7d363-170">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="7d363-170">See Also</span></span>

- <span data-ttu-id="7d363-171">nx_secure_dtls_session_receive, nx_secure_dtls_session_send,</span><span class="sxs-lookup"><span data-stu-id="7d363-171">nx_secure_dtls_session_receive, nx_secure_dtls_session_send,</span></span>
- <span data-ttu-id="7d363-172">nx_secure_dtls_session_create</span><span class="sxs-lookup"><span data-stu-id="7d363-172">nx_secure_dtls_session_create</span></span>

## <a name="nx_secure_dtls_packet_allocate"></a><span data-ttu-id="7d363-173">nx_secure_dtls_packet_allocate</span><span class="sxs-lookup"><span data-stu-id="7d363-173">nx_secure_dtls_packet_allocate</span></span>

<span data-ttu-id="7d363-174">NetX güvenli DTLS oturumu için bir paket ayırın</span><span class="sxs-lookup"><span data-stu-id="7d363-174">Allocate a packet for a NetX Secure DTLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="7d363-175">Prototype</span><span class="sxs-lookup"><span data-stu-id="7d363-175">Prototype</span></span>

```C
UINT  nx_secure_dtls_packet_allocate(
                              NX_SECURE_DTLS_SESSION *session_ptr,
                         NX_PACKET_POOL *pool_ptr,
                         NX_PACKET **packet_ptr,
                              ULONG wait_option);

```

### <a name="description"></a><span data-ttu-id="7d363-176">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7d363-176">Description</span></span>

<span data-ttu-id="7d363-177">Bu hizmet, belirtilen NX_PACKET_POOL belirtilen etkin DTLS oturumu için bir NX_PACKET ayırır.</span><span class="sxs-lookup"><span data-stu-id="7d363-177">This service allocates an NX_PACKET for the specified active DTLS session from the specified NX_PACKET_POOL.</span></span> <span data-ttu-id="7d363-178">Bu hizmet, bir DTLS bağlantısı üzerinden gönderilecek veri paketleri ayırmak için uygulama tarafından çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7d363-178">This service should be called by the application to allocate data packets to be sent over a DTLS connection.</span></span> <span data-ttu-id="7d363-179">Bu hizmet çağrılmadan önce DTLS oturumunun başlatılmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d363-179">The DTLS session must be initialized before calling this service.</span></span>

<span data-ttu-id="7d363-180">Ayrılan paket düzgün bir şekilde başlatılır, böylece DTLS üstbilgi ve altbilgi verileri, paket verileri doldurulduktan sonra eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="7d363-180">The allocated packet is properly initialized so that DTLS header and footer data may be added after the packet data is populated.</span></span> <span data-ttu-id="7d363-181">Davranış, *nx_packet_allocate* benzer şekilde benzerdir.</span><span class="sxs-lookup"><span data-stu-id="7d363-181">The behavior is otherwise identical to *nx_packet_allocate*.</span></span>

### <a name="parameters"></a><span data-ttu-id="7d363-182">Parametreler</span><span class="sxs-lookup"><span data-stu-id="7d363-182">Parameters</span></span>

- <span data-ttu-id="7d363-183">**session_ptr** DTLS oturum örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="7d363-183">**session_ptr** Pointer to a DTLS Session instance.</span></span>
- <span data-ttu-id="7d363-184">**pool_ptr** Paketin ayırabileceği bir NX_PACKET_POOL işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="7d363-184">**pool_ptr** Pointer to an NX_PACKET_POOL from which to allocate the packet.</span></span>
- <span data-ttu-id="7d363-185">**packet_ptr** Yeni ayrılmış pakete çıkış işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="7d363-185">**packet_ptr** Output pointer to the newly-allocated packet.</span></span>
- <span data-ttu-id="7d363-186">**wait_option** Paket ayırması için askıya alma seçeneği.</span><span class="sxs-lookup"><span data-stu-id="7d363-186">**wait_option** Suspension option for packet allocation.</span></span>


### <a name="return-values"></a><span data-ttu-id="7d363-187">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="7d363-187">Return Values</span></span>

- <span data-ttu-id="7d363-188">**NX_SUCCESS** (0x00) başarılı paket ayırması.</span><span class="sxs-lookup"><span data-stu-id="7d363-188">**NX_SUCCESS** (0x00) Successful packet allocate.</span></span>
- <span data-ttu-id="7d363-189">**NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) temel alınan paket ayırması başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="7d363-189">**NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) Underlying packet allocation failed.</span></span>
- <span data-ttu-id="7d363-190">**NX_SECURE_TLS_SESSION_UNINITIALIZED** (0x101) sağlanan DTLS oturumu başlatılmadı.</span><span class="sxs-lookup"><span data-stu-id="7d363-190">**NX_SECURE_TLS_SESSION_UNINITIALIZED** (0x101) The supplied DTLS session was not initialized.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="7d363-191">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="7d363-191">Allowed From</span></span>

<span data-ttu-id="7d363-192">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="7d363-192">Threads</span></span>

### <a name="example"></a><span data-ttu-id="7d363-193">Örnek</span><span class="sxs-lookup"><span data-stu-id="7d363-193">Example</span></span>

```C
/* Allocate a new DTLS packet from the previously created packet pool and
previously initialized DTLS session.   */

status = nx_secure_dtls_packet_allocate(&dtls_session, &pool_0, &packet_ptr,
                                                              NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the newly allocated packet pointer is found in
the variable packet_ptr.  */

```

### <a name="see-also"></a><span data-ttu-id="7d363-194">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="7d363-194">See Also</span></span>

- <span data-ttu-id="7d363-195">nx_secure_x509_certificate_initialize, nx_secure_dtls_session_create,</span><span class="sxs-lookup"><span data-stu-id="7d363-195">nx_secure_x509_certificate_initialize, nx_secure_dtls_session_create,</span></span>
- <span data-ttu-id="7d363-196">nx_secure_dtls_session_trusted_certificate_add,</span><span class="sxs-lookup"><span data-stu-id="7d363-196">nx_secure_dtls_session_trusted_certificate_add,</span></span>
- <span data-ttu-id="7d363-197">nx_secure_dtls_session_send, nx_secure_dtls_session_receive,</span><span class="sxs-lookup"><span data-stu-id="7d363-197">nx_secure_dtls_session_send, nx_secure_dtls_session_receive,</span></span>
- <span data-ttu-id="7d363-198">nx_secure_dtls_session_end, nx_secure_dtls_session_delete</span><span class="sxs-lookup"><span data-stu-id="7d363-198">nx_secure_dtls_session_end, nx_secure_dtls_session_delete</span></span>

## <a name="nx_secure_dtls_psk_add"></a><span data-ttu-id="7d363-199">nx_secure_dtls_psk_add</span><span class="sxs-lookup"><span data-stu-id="7d363-199">nx_secure_dtls_psk_add</span></span>

<span data-ttu-id="7d363-200">NetX güvenli DTLS oturumuna önceden paylaşılan anahtar ekleme</span><span class="sxs-lookup"><span data-stu-id="7d363-200">Add a Pre-Shared Key to a NetX Secure DTLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="7d363-201">Prototype</span><span class="sxs-lookup"><span data-stu-id="7d363-201">Prototype</span></span>

```C
UINT  nx_secure_dtls_psk_add(NX_SECURE_DTLS_SESSION *session_ptr,
                            UCHAR *pre_shared_key, UINT psk_length,
                            UCHAR *psk_identity, UINT
                            identity_length, UCHAR *hint, UINT
                            hint_length);
```

### <a name="description"></a><span data-ttu-id="7d363-202">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7d363-202">Description</span></span>

<span data-ttu-id="7d363-203">Bu hizmet, bir DTLS oturum denetim bloğuna bir önceden paylaşılan anahtar (PSK), kimlik dizesi ve kimlik ipucu ekler.</span><span class="sxs-lookup"><span data-stu-id="7d363-203">This service adds a Pre-Shared Key (PSK), its identity string, and an identity hint to a DTLS Session control block.</span></span> <span data-ttu-id="7d363-204">PSK ciphersuites etkin ve kullanıldığında, bir dijital sertifika yerine PSK kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7d363-204">The PSK is used in place of a digital certificate when PSK ciphersuites are enabled and used.</span></span>

### <a name="parameters"></a><span data-ttu-id="7d363-205">Parametreler</span><span class="sxs-lookup"><span data-stu-id="7d363-205">Parameters</span></span>

- <span data-ttu-id="7d363-206">**session_ptr** Daha önce oluşturulmuş bir DTLS oturum örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="7d363-206">**session_ptr** Pointer to a previously created DTLS Session instance.</span></span>
- <span data-ttu-id="7d363-207">**pre_shared_key** Gerçek PSK değeri.</span><span class="sxs-lookup"><span data-stu-id="7d363-207">**pre_shared_key** The actual PSK value.</span></span>
- <span data-ttu-id="7d363-208">**psk_length** PSK değeri uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="7d363-208">**psk_length** The length of the PSK value.</span></span>
- <span data-ttu-id="7d363-209">**psk_identity** Bu PSK değerini tanımlamak için kullanılan dize.</span><span class="sxs-lookup"><span data-stu-id="7d363-209">**psk_identity** A string used to identify this PSK value.</span></span>
- <span data-ttu-id="7d363-210">**identity_length** PSK kimliğinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="7d363-210">**identity_length** The length of the PSK identity.</span></span>
- <span data-ttu-id="7d363-211">**İpucu** Bir TLS sunucusunda hangi sayıda PSKs arasından seçim yapmak gerektiğini göstermek için kullanılan dize.</span><span class="sxs-lookup"><span data-stu-id="7d363-211">**hint** A string used to indicate which group of PSKs to choose from on a TLS server.</span></span>
- <span data-ttu-id="7d363-212">**hint_length** İpucu dizesinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="7d363-212">**hint_length** The length of the hint string.</span></span>

### <a name="return-values"></a><span data-ttu-id="7d363-213">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="7d363-213">Return Values</span></span>

- <span data-ttu-id="7d363-214">**NX_SUCCESS** (0x00) PSK 'nin başarılı bir şekilde eklenmesi.</span><span class="sxs-lookup"><span data-stu-id="7d363-214">**NX_SUCCESS** (0x00) Successful addition of PSK.</span></span>
- <span data-ttu-id="7d363-215">**NX_PTR_ERROR** (0x07) geçersiz DTLS oturum işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="7d363-215">**NX_PTR_ERROR** (0x07) Invalid DTLS session pointer.</span></span>
- <span data-ttu-id="7d363-216">**NX_SECURE_TLS_NO_MORE_PSK_SPACE** (0x125) başka bir PSK eklenemiyor.</span><span class="sxs-lookup"><span data-stu-id="7d363-216">**NX_SECURE_TLS_NO_MORE_PSK_SPACE** (0x125) Cannot add another PSK.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="7d363-217">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="7d363-217">Allowed From</span></span>

<span data-ttu-id="7d363-218">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="7d363-218">Threads</span></span>

### <a name="example"></a><span data-ttu-id="7d363-219">Örnek</span><span class="sxs-lookup"><span data-stu-id="7d363-219">Example</span></span>

```C
/* PSK value.  */
UCHAR psk[] = { 0x1a, 0x2b, 0x3c, 0x4d };

/* Add PSK to DTLS session.  */
status =  nx_secure_dtls_psk_add(&dtls_session, psk,
                            sizeof(psk), “psk_1”, 4,
                            “Client_identity”, 15);


/* If status is NX_SUCCESS the PSK was successfully added.  */


```

### <a name="see-also"></a><span data-ttu-id="7d363-220">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="7d363-220">See Also</span></span>

- <span data-ttu-id="7d363-221">nx_secure_dtls_server_psk_add, nx_secure_dtls_client_session_create</span><span class="sxs-lookup"><span data-stu-id="7d363-221">nx_secure_dtls_server_psk_add, nx_secure_dtls_client_session_create</span></span>

## <a name="nx_secure_dtls_server_create"></a><span data-ttu-id="7d363-222">nx_secure_dtls_server_create</span><span class="sxs-lookup"><span data-stu-id="7d363-222">nx_secure_dtls_server_create</span></span>

<span data-ttu-id="7d363-223">NetX güvenli DTLS sunucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="7d363-223">Create a NetX Secure DTLS Server</span></span>

### <a name="prototype"></a><span data-ttu-id="7d363-224">Prototype</span><span class="sxs-lookup"><span data-stu-id="7d363-224">Prototype</span></span>

```C
UINT  nx_secure_dtls_server_create(
                NX_SECURE_DTLS_SERVER *server_ptr, NX_IP *ip_ptr,
                UINT port, ULONG timeout, VOID *session_buffer,
                UINT session_buffer_size,
                const NX_SECURE_TLS_CRYPTO *crypto_table,
                VOID *crypto_metadata_buffer, ULONG crypto_metadata_size,
                UCHAR *packet_reassembly_buffer,
                UINT packet_reassembly_buffer_size,
                UINT (*connect_notify)(
                              NX_SECURE_DTLS_SESSION *dtls_session,
                              NXD_ADDRESS *ip_address, UINT port),
                UINT (*receive_notify)(
                              NX_SECURE_DTLS_SESSION *dtls_session)));

```

### <a name="description"></a><span data-ttu-id="7d363-225">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7d363-225">Description</span></span>

<span data-ttu-id="7d363-226">Bu hizmet, belirli bir UDP bağlantı noktasındaki gelen DTLS isteklerini işlemek için bir DTLS sunucusu örneği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7d363-226">This service creates an instance of a DTLS server to handle incoming DTLS requests on a particular UDP port.</span></span> <span data-ttu-id="7d363-227">UDP 'nin durum bilgisiz olması nedeniyle, birden fazla istemciden alınan DTLS istekleri, diğer DTLS oturumları etkinken tek bir bağlantı noktasında gelebilir.</span><span class="sxs-lookup"><span data-stu-id="7d363-227">Due to the fact that UDP is stateless, DTLS requests from multiple clients can come in on a single port while other DTLS sessions are active.</span></span> <span data-ttu-id="7d363-228">Bu nedenle, sunucu etkin oturumları sürdürmek ve gelen iletileri doğru işleyiciye yönlendirmek için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="7d363-228">Thus, the server is needed to maintain active sessions and properly route incoming messages to the proper handler.</span></span>

<span data-ttu-id="7d363-229">İp_ptr parametresi, DTLS sunucusuyla ilişkili iç UDP yuvası için kullanılacak bir NX_IP örneğini işaret eder (ve NX_SECURE_DTLS_SERVER denetim bloğunda depolanır).</span><span class="sxs-lookup"><span data-stu-id="7d363-229">The ip_ptr parameter points to an NX_IP instance to be used for the internal UDP socket associated with the DTLS Server (and stored in the NX_SECURE_DTLS_SERVER control block).</span></span> <span data-ttu-id="7d363-230">IP örneği ve bağlantı noktası, sunucunun nx_secure_dtls_server_start hizmeti ile örneği oluşturulan UDP arabirimini tanımlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7d363-230">The IP instance and port are used to define the UDP interface upon which the server is instantiated with the nx_secure_dtls_server_start service.</span></span>

<span data-ttu-id="7d363-231">Oturum arabelleği parametresi, DTLS sunucusu için tüm olası aynı DTLS oturumlarının denetim bloklarını tutmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7d363-231">The session buffer parameter is used to hold the control blocks for all the possible simultaneous DTLS sessions for the DTLS server.</span></span> <span data-ttu-id="7d363-232">NX_SECURE_DTLS_SESSION denetim bloğu yapısının boyutunun bir daha katı olan bir boyutla ayrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7d363-232">It should be allocated with a size that is an even multiple of the size of the NX_SECURE_DTLS_SESSION control block structure.</span></span>

<span data-ttu-id="7d363-233">Gerekli meta veri boyutunu hesaplamak için, API nx_secure_tls_metadata_size_calculate kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7d363-233">To calculate the necessary metadata size, the API nx_secure_tls_metadata_size_calculate may be used.</span></span>

<span data-ttu-id="7d363-234">Packet_reassembly_buffer parametresi, şifreleme amacıyla UDP datagramlarını tam DTLS kaydına yeniden birleştirmek için DTLS tarafından kullanılır ve en büyük beklenen DTLS kaydına uyum sağlayacak kadar büyük olmalıdır (16KB, en büyük kayıt boyutudur, ancak birçok uygulama bu çok fazla veriyi tek bir kayıtta göndermez).</span><span class="sxs-lookup"><span data-stu-id="7d363-234">The packet_reassembly_buffer parameter is used by DTLS to reassemble UDP datagrams into a complete DTLS record for the purposes of decryption and should be large enough to accommodate the largest expected DTLS record (16KB is the DTLS maximum record size but many applications don’t send that much data in a single record).</span></span>

<span data-ttu-id="7d363-235">Connect_notify geri çağırma yordamı, her yeni DTLS istemcisi sunucuya bağlandığında çağrılır.</span><span class="sxs-lookup"><span data-stu-id="7d363-235">The connect_notify callback routine is invoked whenever a new DTLS client connects to the server.</span></span> <span data-ttu-id="7d363-236">Bu, uygulama, Service *nx_secure_dtls_server_session_start* kullanarak DTLS oturumunu başlatacak.</span><span class="sxs-lookup"><span data-stu-id="7d363-236">It is up to the application to then start the DTLS session using the service *nx_secure_dtls_server_session_start*.</span></span> <span data-ttu-id="7d363-237">Oturum geri çağırmada başlatılmayabilir, ancak geri çağırma, tüm alt düzey ağ işlemlerini (örn. UDP) işlemek için kullanılan IP iş parçacığını (veya uygulama tarafından oluşturulan adanmış DTLS iş parçacığını) bildirmek için kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7d363-237">While the session may be started in the callback itself, it is recommended that the callback only be used to notify the application thread (or dedicated DTLS thread created by the application) of the connection as the callback is invoked by the IP thread which is used to process all lower-level network processing (e.g. UDP).</span></span> <span data-ttu-id="7d363-238">Bu, DTLS oturum parametresini kaydetme (geri çağırmaya bir parametre olarak sunulur) ve diğer iş parçacığında nx_secure_dtls_server_session_start çağırma kadar kolay olabilir.</span><span class="sxs-lookup"><span data-stu-id="7d363-238">This can be as simple as saving the DTLS session parameter (provided as a parameter to the callback) and invoking nx_secure_dtls_server_session_start in the other thread.</span></span> <span data-ttu-id="7d363-239">Connect_notify geri çağırma genellikle NX_SUCCESS döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="7d363-239">The connect_notify callback should generally return NX_SUCCESS.</span></span>

<span data-ttu-id="7d363-240">Receive_notify geri çağırma yordamı, mevcut bir DTLS oturumuyla eşleşen bir DTLS kaydı alındığında çağrılır (var olan bir oturumu tanımlamak için uzak ana bilgisayar IP adresi ve bağlantı noktası kullanılır).</span><span class="sxs-lookup"><span data-stu-id="7d363-240">The receive_notify callback routine is invoked whenever a DTLS record is received that matches an existing established DTLS session (the remote host IP address and port are used to identify an existing session).</span></span> <span data-ttu-id="7d363-241">Bu, DTLS üzerinden şifrelenen ve gönderilen "uygulama verilerini" temsil eder.</span><span class="sxs-lookup"><span data-stu-id="7d363-241">This represents the “application data” that is encrypted and sent over DTLS.</span></span> <span data-ttu-id="7d363-242">Uygulamanın alınan verileri almak için, belirtilen DTLS oturumunda hizmet *nx_secure_dtls_session_receive* çağrısı gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d363-242">The application must call the service *nx_secure_dtls_session_receive* on the provided DTLS session to retrieve the received data.</span></span> <span data-ttu-id="7d363-243">Connect_receive geri çağırmada olduğu gibi, geri çağırma IP iş parçacığından çağrıldığında ileti işlemeyi işlemek için oturumun başka bir iş parçacığına geçirilmesi önerilir.</span><span class="sxs-lookup"><span data-stu-id="7d363-243">As with the connect_receive callback, it is recommended that the session be passed to another thread to handle the message processing as the callback is invoked from the IP thread.</span></span> <span data-ttu-id="7d363-244">Receive_notify geri çağırma genellikle NX_SUCCESS döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="7d363-244">The receive_notify callback should generally return NX_SUCCESS.</span></span>

### <a name="parameters"></a><span data-ttu-id="7d363-245">Parametreler</span><span class="sxs-lookup"><span data-stu-id="7d363-245">Parameters</span></span>

- <span data-ttu-id="7d363-246">**server_ptr** Daha önce oluşturulmuş bir DTLS sunucu örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="7d363-246">**server_ptr** Pointer to a previously created DTLS Server instance.</span></span>
- <span data-ttu-id="7d363-247">**ip_ptr** DTLS sunucusu için ağ arabirimi olarak kullanılacak başlatılmış bir NX_IP denetim bloğunun işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="7d363-247">**ip_ptr** Pointer to an initialized NX_IP control block to use as the network interface for the DTLS server.</span></span>
- <span data-ttu-id="7d363-248">**bağlantı noktası** DTLS sunucusu UDP yuvasının bağlandığı yerel UDP bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="7d363-248">**port** The local UDP port to which the DTLS server UDP socket is bound.</span></span>
- <span data-ttu-id="7d363-249">**zaman aşımı** Ağ işlemleri için kullanılacak zaman aşımı değeri.</span><span class="sxs-lookup"><span data-stu-id="7d363-249">**timeout** Timeout value to use for network operations.</span></span>
- <span data-ttu-id="7d363-250">**session_buffer** Bu DTLS sunucu örneğine atanan tüm NX_SECURE_DTLS_SESSION örnekleri için denetim blokları içeren arabellek alanı.</span><span class="sxs-lookup"><span data-stu-id="7d363-250">**session_buffer** Buffer space to contain control blocks for all instances of NX_SECURE_DTLS_SESSION assigned to this DTLS Server instance.</span></span>
- <span data-ttu-id="7d363-251">**session_buffer_size** Oturum arabelleğinin boyutu.</span><span class="sxs-lookup"><span data-stu-id="7d363-251">**session_buffer_size** Size of the session buffer.</span></span> <span data-ttu-id="7d363-252">Bu, DTLS sunucusuna atanan DTLS oturumlarının sayısını belirler.</span><span class="sxs-lookup"><span data-stu-id="7d363-252">This determines the number of DTLS sessions assigned to the DTLS Server.</span></span>
- <span data-ttu-id="7d363-253">**crypto_table** Tüm şifreleme işlemleri için kullanılan TLS/DTLS Şifreleme tablosu yapısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="7d363-253">**crypto_table** Pointer to a TLS/DTLS encryption table structure used for all cryptographic operations.</span></span>
- <span data-ttu-id="7d363-254">**crypto_metadata_buffer** Şifreleme işlemi hesaplamaları ve durum bilgileri için arabellek alanı.</span><span class="sxs-lookup"><span data-stu-id="7d363-254">**crypto_metadata_buffer** Buffer space for cryptographic operation calculations and state information.</span></span>
- <span data-ttu-id="7d363-255">**crypto_metadata_size** Meta veri arabelleğinin boyutu.</span><span class="sxs-lookup"><span data-stu-id="7d363-255">**crypto_metadata_size** Size of metadata buffer.</span></span>
- <span data-ttu-id="7d363-256">**packet_reassembly_buffer** DTLS tarafından, IP verilerini şifre çözme için DTLS kayıtlarına yeniden birleştirmek üzere kullanılan arabellek.</span><span class="sxs-lookup"><span data-stu-id="7d363-256">**packet_reassembly_buffer** Buffer used by DTLS to reassemble UDP data into DTLS records for decryption.</span></span>
- <span data-ttu-id="7d363-257">**packet_reassembly_buffer_size** Yeniden birleştirme arabelleğinin boyutu.</span><span class="sxs-lookup"><span data-stu-id="7d363-257">**packet_reassembly_buffer_size** Size of reassembly buffer.</span></span> <span data-ttu-id="7d363-258">Genellikle 16KB 'den büyük olmalıdır, ancak uygulamaya bağlı olarak daha küçük olabilir.</span><span class="sxs-lookup"><span data-stu-id="7d363-258">Generally should be greater than 16KB but may be smaller depending on application.</span></span>
- <span data-ttu-id="7d363-259">**connect_notify** Uzak DTLS Istemcisi bu DTLS sunucusuna bağlanmaya çalıştığında, geri arama yordamı çağrılır.</span><span class="sxs-lookup"><span data-stu-id="7d363-259">**connect_notify** Callback routine invoked whenever a remote DTLS Client attempts to connect to this DTLS server.</span></span>
- <span data-ttu-id="7d363-260">**receive_notify** Mevcut bir DTLS oturumu üzerinden uygulama verileri alındığında çağrı çağrılır.</span><span class="sxs-lookup"><span data-stu-id="7d363-260">**receive_notify** Callback invoked whenever application data is received over an existing DTLS session.</span></span>

### <a name="return-values"></a><span data-ttu-id="7d363-261">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="7d363-261">Return Values</span></span>

- <span data-ttu-id="7d363-262">**NX_SUCCESS** (0x00) DTLS sunucusu başarıyla oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="7d363-262">**NX_SUCCESS** (0x00) Successful creation of DTLS server.</span></span>
- <span data-ttu-id="7d363-263">**NX_PTR_ERROR** (0x07) geçersiz işaretçi geçirildi.</span><span class="sxs-lookup"><span data-stu-id="7d363-263">**NX_PTR_ERROR** (0x07) Invalid pointer passed.</span></span>
- <span data-ttu-id="7d363-264">**NX_INVALID_PARAMETERS** (0x4D) oturumlar, paket yeniden birleştirme veya şifreleme için yeterli arabellek alanı yok.</span><span class="sxs-lookup"><span data-stu-id="7d363-264">**NX_INVALID_PARAMETERS** (0x4D) Not enough buffer space for sessions, packet reassembly, or cryptography.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="7d363-265">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="7d363-265">Allowed From</span></span>

<span data-ttu-id="7d363-266">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="7d363-266">Threads</span></span>

### <a name="example"></a><span data-ttu-id="7d363-267">Örnek</span><span class="sxs-lookup"><span data-stu-id="7d363-267">Example</span></span>

```C
#define DTLS_SERVER_SESSION (3)

/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Allocate space for DTLS sessions in the DTLS server. */
UCHAR dtls_server_session_buffer[sizeof(NX_SECURE_DTLS_SESSION)
                                        * DTLS_SERVER_SESSIONS];

/* Flag used to indicate that a DTLS Client has connected. */
UINT connect_flag = 0;

/* Flag used to indicate application data reception. */
UINT receive_flag = 0;

/* Pointer to newly-connected DTLS session.
   NOTE: In practice this should be an array or list in case a new connection is
         attempted while a previous session is being started. */
NX_SECURE_DTLS_SESSION *new_dtls_session;

/* Pointer to session for application data receive.
   NOTE: Should be an array or list as
   with new_dtls_session */
NX_SECURE_DTLS_SESSION *receive_dtls_session;

/* Connect notify callback routine. */
UINT dtls_server_connect_notify(NX_SECURE_DTLS_SESSION *dtls_session, NXD_ADDRESS
    *ip_address, UINT port)
{
    /* NOTE: proper inter-thread communication procedures (e.g. mutex handling)
             Omitted for clarity. */

    /* Notify application thread that a connection request has been received. */
    connect_flag = 1;
    new_dtls_session = dtls_session;

    return(NX_SUCCESS);
}

/* Receive notify callback routine invoked when DTLS application data is received
   on an existing DTLS server session. */
UINT dtls_server_receive_notify(NX_SECURE_DTLS_SESSION *dtls_session)
{
    /* Receive and process DTLS record.
       NOTE: Mutex handling omitted for clarity. */
    receive_flag = 1;
    receive_dtls_session = dtls_session;

    return(NX_SUCCESS);
}

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
    NX_PACKET *send_packet;
    NX_PACKET *receive_packet;
    UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                LOCAL_SERVER_PORT,
                                NX_IP_PERIODIC_RATE, dtls_server_session_buffer,
                                sizeof(dtls_server_session_buffer),
                                &tls_crypto_table, crypto_metadata_buffer,
                                sizeof(crypto_metadata_buffer), packet_buffer,
                                sizeof(packet_buffer),
                                dtls_server_connect_notify,
                                dtls_server_receive_notify);

    /* Initialize local server identity certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&certificate, device_cert_der,
                        device_cert_der_len, NX_NULL, 0,
                        device_cert_key_der, device_cert_key_der_len,
                        NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_local_certificate_add(&dtls_server,
                                                    &certificate, 1);

    /* Start server. */
    status = nx_secure_dtls_server_start(&dtls_server);

    /* Loop continuously to handle incoming data. */
    while(1)
    {
        /* Check for new connections. Muxtex handling omitted for clarity. */
        if(connect_flag)
        {
            /* We have a new connection attempt, start the DTLS session. */
            status = nx_secure_dtls_server_session_start(new_dtls_session,
                                                    NX_IP_PERIODIC_RATE);

        }

        /* Check for received application data. */
        if(receive_flag)
        {
            /* We have received data over a previously-established DTLS session.
               Mutex handling omitted for clarity. */
            Status = nx_secure_dtls_session_receive(receive_dtls_session,
                                                        &receive_packet,
                                                           NX_IP_PERIODIC_RATE);

            /* Process received data… */

            /* Prepare and send response to client. */
        status = nx_secure_dtls_packet_allocate(receive_dtls_session, &packet_pool,
                                                   &send_packet, NX_IP_PERIODIC_RATE);

        /* Check for errors and prepare response data
        (e.g. nx_packet_data_append). */

        /* Send response to client. */
        status = nx_secure_dtls_server_session_send(receive_dtls_session,
                                                            send_packet);

        }

        /* If not processing connections or received data,
        let the thread sleep. */
        if(!connect_flag && !receive_flag)
        {
            tx_thread_sleep(100);
        }
    }

    /* Server processing is done, stop the server
    instance from accepting requests. */
    status = nx_secure_dtls_server_stop(&dtls_server);

    /* If we exit the processing loop, clean up the server. */
    status = nx_secure_dtls_server_delete(&dtls_server);
}

```

### <a name="see-also"></a><span data-ttu-id="7d363-268">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="7d363-268">See Also</span></span>

- <span data-ttu-id="7d363-269">nx_secure_dtls_server_start, nx_secure_dtls_server_delete,</span><span class="sxs-lookup"><span data-stu-id="7d363-269">nx_secure_dtls_server_start, nx_secure_dtls_server_delete,</span></span>
- <span data-ttu-id="7d363-270">nx_secure_dtls_session_receive, nx_secure_dtls_server_session_send,</span><span class="sxs-lookup"><span data-stu-id="7d363-270">nx_secure_dtls_session_receive, nx_secure_dtls_server_session_send,</span></span>
- <span data-ttu-id="7d363-271">nx_secure_dtls_server_session_start,</span><span class="sxs-lookup"><span data-stu-id="7d363-271">nx_secure_dtls_server_session_start,</span></span>
- <span data-ttu-id="7d363-272">nx_secure_dtls_server_session_stop,</span><span class="sxs-lookup"><span data-stu-id="7d363-272">nx_secure_dtls_server_session_stop,</span></span>
- <span data-ttu-id="7d363-273">nx_secure_dtls_server_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="7d363-273">nx_secure_dtls_server_local_certificate_add</span></span>

## <a name="nx_secure_dtls_server_delete"></a><span data-ttu-id="7d363-274">nx_secure_dtls_server_delete</span><span class="sxs-lookup"><span data-stu-id="7d363-274">nx_secure_dtls_server_delete</span></span>

<span data-ttu-id="7d363-275">NetX güvenli DTLS sunucusu tarafından kullanılan kaynakları boşaltma</span><span class="sxs-lookup"><span data-stu-id="7d363-275">Free up resources used by a NetX Secure DTLS Server</span></span>

### <a name="prototype"></a><span data-ttu-id="7d363-276">Prototype</span><span class="sxs-lookup"><span data-stu-id="7d363-276">Prototype</span></span>

```C
UINT  nx_secure_dtls_server_delete(NX_SECURE_DTLS_SERVER *server_ptr);
```

### <a name="description"></a><span data-ttu-id="7d363-277">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7d363-277">Description</span></span>

<span data-ttu-id="7d363-278">Bu hizmet, sunucu tarafından kullanılan iç UDP yuvası dahil olmak üzere bir DTLS sunucu örneğine ayrılan kaynakları boşaltır.</span><span class="sxs-lookup"><span data-stu-id="7d363-278">This service frees up the resources allocated to a DTLS Server instance, including the internal UDP socket used by the server.</span></span>

### <a name="parameters"></a><span data-ttu-id="7d363-279">Parametreler</span><span class="sxs-lookup"><span data-stu-id="7d363-279">Parameters</span></span>

- <span data-ttu-id="7d363-280">**server_ptr** Daha önce oluşturulmuş bir DTLS sunucu örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="7d363-280">**server_ptr** Pointer to a previously created DTLS Server instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="7d363-281">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="7d363-281">Return Values</span></span>

- <span data-ttu-id="7d363-282">**NX_SUCCESS** (0x00) sunucu başarıyla silindi.</span><span class="sxs-lookup"><span data-stu-id="7d363-282">**NX_SUCCESS** (0x00) Successful deletion of server.</span></span>
- <span data-ttu-id="7d363-283">**NX_PTR_ERROR** (0x07) geçersiz işaretçi geçirildi.</span><span class="sxs-lookup"><span data-stu-id="7d363-283">**NX_PTR_ERROR** (0x07) Invalid pointer passed.</span></span>
- <span data-ttu-id="7d363-284">**NX_STILL_BOUND** (0x42) UDP yuvası hala bağımlı.</span><span class="sxs-lookup"><span data-stu-id="7d363-284">**NX_STILL_BOUND** (0x42) UDP socket is still bound.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="7d363-285">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="7d363-285">Allowed From</span></span>

<span data-ttu-id="7d363-286">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="7d363-286">Threads</span></span>

### <a name="example"></a><span data-ttu-id="7d363-287">Örnek</span><span class="sxs-lookup"><span data-stu-id="7d363-287">Example</span></span>

```C
#define DTLS_SERVER_SESSION (3)

/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Allocate space for DTLS sessions in the DTLS server. */
UCHAR dtls_server_session_buffer[sizeof(NX_SECURE_DTLS_SESSION)
                                        * DTLS_SERVER_SESSIONS];

/* Flag used to indicate that a DTLS Client has connected. */
UINT connect_flag = 0;

/* Flag used to indicate application data reception. */
UINT receive_flag = 0;

/* Pointer to newly-connected DTLS session.
   NOTE: In practice this should be an array or list in case a new connection is
         attempted while a previous session is being started. */
NX_SECURE_DTLS_SESSION *new_dtls_session;

/* Pointer to session for application data receive.
NOTE: Should be an array or list as
   with new_dtls_session */
NX_SECURE_DTLS_SESSION *receive_dtls_session;

/* Connect notify callback routine. */
UINT dtls_server_connect_notify(NX_SECURE_DTLS_SESSION *dtls_session, NXD_ADDRESS
*ip_address, UINT port)
{
    /* NOTE: proper inter-thread communication procedures (e.g. mutex handling)
             Omitted for clarity. */

    /* Notify application thread that a connection request has been received. */
    connect_flag = 1;
    new_dtls_session = dtls_session;

    return(NX_SUCCESS);
}

/* Receive notify callback routine invoked when DTLS application data is received
   on an existing DTLS server session. */
UINT dtls_server_receive_notify(NX_SECURE_DTLS_SESSION *dtls_session)
{
    /* Receive and process DTLS record.
       NOTE: Mutex handling omitted for clarity. */
    receive_flag = 1;
    receive_dtls_session = dtls_session;

    return(NX_SUCCESS);
}

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
    NX_PACKET *send_packet;
    NX_PACKET *receive_packet;
    UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                            LOCAL_SERVER_PORT,
                                            NX_IP_PERIODIC_RATE,
                                            dtls_server_session_buffer,
                                            sizeof(dtls_server_session_buffer),
                                            &tls_crypto_table,
                                            crypto_metadata_buffer,
                                            sizeof(crypto_metadata_buffer),
                                            packet_buffer, sizeof(packet_buffer),
                                            dtls_server_connect_notify,
                                            dtls_server_receive_notify);


    /* Check for errors. */

    /* Initialize local server identity certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&certificate, device_cert_der,
                                            device_cert_der_len,
                                            NX_NULL, 0,
                                            device_cert_key_der,
                                            device_cert_key_der_len,
                                            NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_local_certificate_add(&dtls_server,
                                                    &certificate, 1);


    /* Start server. */
    status = nx_secure_dtls_server_start(&dtls_server);

    /* Loop continuously to handle incoming data. */
    while(1)
    {
        /* Check for new connections. Muxtex handling omitted for clarity. */
        if(connect_flag)
        {
            /* We have a new connection attempt, start the DTLS session. */
            status = nx_secure_dtls_server_session_start(new_dtls_session,
                                                    NX_IP_PERIODIC_RATE);
        }

        /* Check for received application data. */
        if(receive_flag)
        {
            /* We have received data over a previously-established DTLS session.
               Mutex handling omitted for clarity. */
            Status = nx_secure_dtls_session_receive(receive_dtls_session,
                                                        &receive_packet,
                                                         NX_IP_PERIODIC_RATE);

            /* Process received data… */

            /* Prepare and send response to client. */
        status = nx_secure_dtls_packet_allocate(receive_dtls_session,
                                                        &packet_pool,
                                                        &send_packet,
                                                        NX_IP_PERIODIC_RATE);

        /* Send response to client. */
        status = nx_secure_dtls_server_session_send(receive_dtls_session,
                                                            send_packet);

        }

        /* If not processing connections or received data, let the thread sleep. */
        if(!connect_flag && !receive_flag)
        {
            tx_thread_sleep(100);
        }
    }

    /* If we exit the processing loop, clean up the server. */
    status = nx_secure_dtls_server_delete(&dtls_server);
}

```

### <a name="see-also"></a><span data-ttu-id="7d363-288">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="7d363-288">See Also</span></span>

- <span data-ttu-id="7d363-289">nx_secure_dtls_server_start, nx_secure_dtls_server_create,</span><span class="sxs-lookup"><span data-stu-id="7d363-289">nx_secure_dtls_server_start, nx_secure_dtls_server_create,</span></span>
- <span data-ttu-id="7d363-290">nx_secure_dtls_session_receive, nx_secure_dtls_server_session_send,</span><span class="sxs-lookup"><span data-stu-id="7d363-290">nx_secure_dtls_session_receive, nx_secure_dtls_server_session_send,</span></span>
- <span data-ttu-id="7d363-291">nx_secure_dtls_server_session_start</span><span class="sxs-lookup"><span data-stu-id="7d363-291">nx_secure_dtls_server_session_start</span></span>

## <a name="nx_secure_dtls_server_local_certificate_add"></a><span data-ttu-id="7d363-292">nx_secure_dtls_server_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="7d363-292">nx_secure_dtls_server_local_certificate_add</span></span>

<span data-ttu-id="7d363-293">NetX güvenli DTLS sunucusuna yerel sunucu kimlik sertifikası ekleme</span><span class="sxs-lookup"><span data-stu-id="7d363-293">Add a local server identity certificate to a NetX Secure DTLS Server</span></span>

### <a name="prototype"></a><span data-ttu-id="7d363-294">Prototype</span><span class="sxs-lookup"><span data-stu-id="7d363-294">Prototype</span></span>

```C
UINT  nx_secure_dtls_server_local_certificate_add(
                                   NX_SECURE_DTLS_SERVER *server_ptr,
                                 NX_SECURE_X509_CERT *certificate,
                                 UINT cert_id);

```

### <a name="description"></a><span data-ttu-id="7d363-295">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7d363-295">Description</span></span>

<span data-ttu-id="7d363-296">Bu hizmet bir DTLS sunucu örneğine yerel sunucu kimlik sertifikası ekler.</span><span class="sxs-lookup"><span data-stu-id="7d363-296">This service adds a local server identity certificate to a DTLS Server instance.</span></span> <span data-ttu-id="7d363-297">Diğer bir kimlik doğrulama mekanizması (ör. önceden paylaşılan anahtarlar) kullanılmadığı takdirde, istemcilerin bir DTLS sunucusuna bağlanması için en az bir kimlik sertifikası gereklidir.</span><span class="sxs-lookup"><span data-stu-id="7d363-297">At least one identity certificate is required for clients to connect to a DTLS server unless an alternate authentication mechanism (e.g. Pre-Shared Keys) is used.</span></span>

<span data-ttu-id="7d363-298">Cert_id parametresi, sertifika için sayısal, sıfır olmayan bir tanıtıcıdır.</span><span class="sxs-lookup"><span data-stu-id="7d363-298">The cert_id parameter is a numeric, non-zero identifier for the certificate.</span></span> <span data-ttu-id="7d363-299">Bu, DTLS sunucu deposunda aynı X. 509.440 ortak adına sahip birden çok kimlik sertifikası bulunan olayda kolayca kaldırılmasını veya bu durumda bulunabilmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="7d363-299">This enables the certificate to be easily removed or found in the event there are multiple identity certificates with the same X.509 Common Name present in the DTLS server store.</span></span> <span data-ttu-id="7d363-300">X. 509.440 sunucu sertifikaları hakkında daha fazla bilgi için NetX güvenli TLS Kullanıcı Kılavuzu 'na bakın.</span><span class="sxs-lookup"><span data-stu-id="7d363-300">See the NetX Secure TLS User Guide for more information about X.509 server certificates.</span></span>

### <a name="parameters"></a><span data-ttu-id="7d363-301">Parametreler</span><span class="sxs-lookup"><span data-stu-id="7d363-301">Parameters</span></span>

- <span data-ttu-id="7d363-302">**server_ptr** Daha önce oluşturulmuş bir DTLS sunucu örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="7d363-302">**server_ptr** Pointer to a previously created DTLS Server instance.</span></span>
- <span data-ttu-id="7d363-303">**sertifika** Daha önce başlatılmış bir X. 509.440 sertifika yapısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="7d363-303">**certificate** Pointer to a previously initialized X.509 certificate structure.</span></span>
- <span data-ttu-id="7d363-304">**cert_id** Bu DTLS sunucusunda bu sertifika için sıfır olmayan sayısal benzersiz tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="7d363-304">**cert_id** Numeric non-zero unique identifier for this certificate in this DTLS server.</span></span>

### <a name="return-values"></a><span data-ttu-id="7d363-305">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="7d363-305">Return Values</span></span>

- <span data-ttu-id="7d363-306">**NX_SUCCESS** (0x00) DTLS sunucusuna sertifikanın başarıyla eklenmesi.</span><span class="sxs-lookup"><span data-stu-id="7d363-306">**NX_SUCCESS** (0x00) Successful addition of certificate to DTLS server.</span></span>
- <span data-ttu-id="7d363-307">**NX_PTR_ERROR** (0x07) geçersiz işaretçi geçirildi.</span><span class="sxs-lookup"><span data-stu-id="7d363-307">**NX_PTR_ERROR** (0x07) Invalid pointer passed.</span></span>
- <span data-ttu-id="7d363-308">**NX_INVALID_PARAMETERS** (0x4D) BIR sertifika kimliği (0) geçirildi.</span><span class="sxs-lookup"><span data-stu-id="7d363-308">**NX_INVALID_PARAMETERS** (0x4D) A certificate ID of 0 was passed in.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="7d363-309">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="7d363-309">Allowed From</span></span>

<span data-ttu-id="7d363-310">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="7d363-310">Threads</span></span>

### <a name="example"></a><span data-ttu-id="7d363-311">Örnek</span><span class="sxs-lookup"><span data-stu-id="7d363-311">Example</span></span>

<span data-ttu-id="7d363-312">\* Daha kapsamlı bir örnek için bkz. *nx_secure_dtls_server_create* başvurusu.</span><span class="sxs-lookup"><span data-stu-id="7d363-312">\*See reference for *nx_secure_dtls_server_create* for a more complete example.</span></span>

```C
/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Certificate control block and data. */
NX_SECURE_X509_CERT certificate;
UCHAR certificate_der_data[] = { … };
UCHAR certificate_key_der_data[] = { … };

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                    LOCAL_SERVER_PORT,
                                    NX_IP_PERIODIC_RATE,
                                    dtls_server_session_buffer,
                                    sizeof(dtls_server_session_buffer),
                                    &tls_crypto_table,
                                    crypto_metadata_buffer,
                                    sizeof(crypto_metadata_buffer),
                                    packet_buffer,
                                    sizeof(packet_buffer),
                                    dtls_server_connect_notify,
                                    dtls_server_receive_notify);

    /* Check for errors. */

    /* Initialize local server identity certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&certificate,
                            certificate_der_data,
                            sizeof(certificate_der_data),
                            NX_NULL, 0,
                            certificate_key_der_data,
                            sizeof(certificate_key_der_data),
                            NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_local_certificate_add(&dtls_server,
                                                    &certificate, 1);

    /* Start server. */
    status = nx_secure_dtls_server_start(&dtls_server);

    /* Loop continuously to handle incoming data. */
    while(1)
    {
        /* Process incoming requests and data. */
    }

}

```

### <a name="see-also"></a><span data-ttu-id="7d363-313">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="7d363-313">See Also</span></span>

- <span data-ttu-id="7d363-314">nx_secure_dtls_server_start, nx_secure_dtls_server_create,</span><span class="sxs-lookup"><span data-stu-id="7d363-314">nx_secure_dtls_server_start, nx_secure_dtls_server_create,</span></span>
- <span data-ttu-id="7d363-315">nx_secure_dtls_session_receive, nx_secure_dtls_server_session_send,</span><span class="sxs-lookup"><span data-stu-id="7d363-315">nx_secure_dtls_session_receive, nx_secure_dtls_server_session_send,</span></span>
- <span data-ttu-id="7d363-316">nx_secure_dtls_server_session_start,</span><span class="sxs-lookup"><span data-stu-id="7d363-316">nx_secure_dtls_server_session_start,</span></span>
- <span data-ttu-id="7d363-317">nx_secure_dtls_server_local_certificate_remove,</span><span class="sxs-lookup"><span data-stu-id="7d363-317">nx_secure_dtls_server_local_certificate_remove,</span></span>
- <span data-ttu-id="7d363-318">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="7d363-318">nx_secure_x509_certificate_initialize</span></span>

## <a name="nx_secure_dtls_server_local_certificate_remove"></a><span data-ttu-id="7d363-319">nx_secure_dtls_server_local_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="7d363-319">nx_secure_dtls_server_local_certificate_remove</span></span>

<span data-ttu-id="7d363-320">NetX güvenli DTLS sunucusundan yerel sunucu kimlik sertifikasını kaldırma</span><span class="sxs-lookup"><span data-stu-id="7d363-320">Remove a local server identity certificate from a NetX Secure DTLS Server</span></span>

### <a name="prototype"></a><span data-ttu-id="7d363-321">Prototype</span><span class="sxs-lookup"><span data-stu-id="7d363-321">Prototype</span></span>

```C
UINT  nx_secure_dtls_server_local_certificate_remove(
                                   NX_SECURE_DTLS_SERVER *server_ptr,
                                   UCHAR *common_name,
                                   UINT common_name_length,
                                   UINT cert_id);

```

### <a name="description"></a><span data-ttu-id="7d363-322">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7d363-322">Description</span></span>

<span data-ttu-id="7d363-323">Bu hizmet, bir DTLS sunucu örneğinden yerel sunucu kimlik sertifikasını kaldırır.</span><span class="sxs-lookup"><span data-stu-id="7d363-323">This service removes a local server identity certificate from a DTLS Server instance.</span></span> <span data-ttu-id="7d363-324">Diğer bir kimlik doğrulama mekanizması (ör. önceden paylaşılan anahtarlar) kullanılmadığı takdirde, istemcilerin bir DTLS sunucusuna bağlanması için en az bir kimlik sertifikası gereklidir.</span><span class="sxs-lookup"><span data-stu-id="7d363-324">At least one identity certificate is required for clients to connect to a DTLS server unless an alternate authentication mechanism (e.g. Pre-Shared Keys) is used.</span></span>

<span data-ttu-id="7d363-325">Kaldırılacak sertifika, X. 509.440 ortak adı ya da *nx_secure_dtls_server_local_certificate_add* çağrısında atanan sayısal cert_id tarafından belirlenebilir.</span><span class="sxs-lookup"><span data-stu-id="7d363-325">The certificate to be removed can be identified either by its X.509 Common Name or by the numeric cert_id that was assigned in the call to *nx_secure_dtls_server_local_certificate_add*.</span></span> <span data-ttu-id="7d363-326">Cert_id yalnızca sertifikayı tanımlamak için kullanılır ve uygulama tarafından korunur.</span><span class="sxs-lookup"><span data-stu-id="7d363-326">The cert_id is only used to identify the certificate and is maintained by the application.</span></span> <span data-ttu-id="7d363-327">Sayısal sertifika tanımlayıcısı yerine ortak ad kullanılırsa, cert_id parametresi 0 olarak ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7d363-327">If the Common Name is used instead of the numeric certificate identifier, the cert_id parameter should be set to 0.</span></span>

> [!NOTE]
> <span data-ttu-id="7d363-328">Bir DTLS el sıkışması işlenirken bir sertifikayı kaldırmak beklenmeyen davranışlara neden olur.</span><span class="sxs-lookup"><span data-stu-id="7d363-328">Removing a certificate while a DTLS handshake is being processed will result in unexpected behavior.</span></span> <span data-ttu-id="7d363-329">Sertifikalar kaldırılmadan önce hizmet *nx_secure_dtls_server_stop* çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7d363-329">The service *nx_secure_dtls_server_stop* should be called before removing certificates.</span></span>

### <a name="parameters"></a><span data-ttu-id="7d363-330">Parametreler</span><span class="sxs-lookup"><span data-stu-id="7d363-330">Parameters</span></span>

- <span data-ttu-id="7d363-331">**server_ptr** Daha önce oluşturulmuş bir DTLS sunucu örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="7d363-331">**server_ptr** Pointer to a previously created DTLS Server instance.</span></span>
- <span data-ttu-id="7d363-332">**common_name** Kaldırılacak sertifikanın X. 509.440 CommonName.</span><span class="sxs-lookup"><span data-stu-id="7d363-332">**common_name** X.509 CommonName of the certificate to remove.</span></span> <span data-ttu-id="7d363-333">Bu kullanılırsa, cert_id sıfır olarak geçirin.</span><span class="sxs-lookup"><span data-stu-id="7d363-333">If this is used, pass cert_id as zero.</span></span>
- <span data-ttu-id="7d363-334">**common_name_length** Bayt cinsinden common_name dize uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="7d363-334">**common_name_length** Length of common_name string in bytes.</span></span>
- <span data-ttu-id="7d363-335">**cert_id** Bu DTLS sunucusunda bu sertifika için sıfır olmayan sayısal benzersiz tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="7d363-335">**cert_id** Numeric non-zero unique identifier for this certificate in this DTLS server.</span></span> <span data-ttu-id="7d363-336">Bu kullanılırsa, common_name parametresi için NX_NULL geçirin.</span><span class="sxs-lookup"><span data-stu-id="7d363-336">If this is used, pass NX_NULL for the common_name parameter.</span></span>

### <a name="return-values"></a><span data-ttu-id="7d363-337">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="7d363-337">Return Values</span></span>

- <span data-ttu-id="7d363-338">**NX_SUCCESS** (0x00) DTLS sunucusundan sertifikanın başarıyla kaldırılması.</span><span class="sxs-lookup"><span data-stu-id="7d363-338">**NX_SUCCESS** (0x00) Successful removal of certificate from DTLS server.</span></span>
- <span data-ttu-id="7d363-339">**NX_PTR_ERROR** (0x07) geçersiz işaretçi geçirildi.</span><span class="sxs-lookup"><span data-stu-id="7d363-339">**NX_PTR_ERROR** (0x07) Invalid pointer passed.</span></span>
- <span data-ttu-id="7d363-340">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) VERILEN DTLS sunucusunda cert_id veya common_name eşleşen bir sertifika bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="7d363-340">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) No certificate matching the cert_id or common_name was found in the given DTLS server.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="7d363-341">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="7d363-341">Allowed From</span></span>

<span data-ttu-id="7d363-342">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="7d363-342">Threads</span></span>

### <a name="example"></a><span data-ttu-id="7d363-343">Örnek</span><span class="sxs-lookup"><span data-stu-id="7d363-343">Example</span></span>

```C
/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Certificate control block and data. */
NX_SECURE_X509_CERT certificate;
UCHAR certificate_der_data[] = { … };
UCHAR certificate_key_der_data[] = { … };

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
    UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                LOCAL_SERVER_PORT, NX_IP_PERIODIC_RATE,
                                dtls_server_session_buffer,
                                sizeof(dtls_server_session_buffer),
                                &tls_crypto_table, crypto_metadata_buffer,
                                sizeof(crypto_metadata_buffer), packet_buffer,
                                sizeof(packet_buffer),
                                dtls_server_connect_notify,
                                dtls_server_receive_notify);

    /* Check for errors. */

    /* Initialize local server identity certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&certificate,
                                        certificate_der_data,
                                        sizeof(certificate_der_data),
                                        NX_NULL, 0, certificate_key_der_data,
                                        sizeof(certificate_key_der_data),
                                        NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_local_certificate_add(&dtls_server,
                                                     &certificate, 1);

    /* Start server. */
    status = nx_secure_dtls_server_start(&dtls_server);

    /* Process client requests, etc… */

    /* Stop the server before removing a certificate. */
    Status = nx_secure_dtls_server_stop(&dtls_server);

    /* At some point in the future we decide to remove the certificate we added.
    We can use the certificate identifier we passed into the call to
    nx_secure_dtls_local_certificate_add (value = 1); */
    status = nx_secure_dtls_server_local_certificate_remove(&dtls_server,
                                                          NX_NULL, 0, 1);

}

```

### <a name="see-also"></a><span data-ttu-id="7d363-344">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="7d363-344">See Also</span></span>

- <span data-ttu-id="7d363-345">nx_secure_dtls_server_start, nx_secure_dtls_server_create,</span><span class="sxs-lookup"><span data-stu-id="7d363-345">nx_secure_dtls_server_start, nx_secure_dtls_server_create,</span></span>
- <span data-ttu-id="7d363-346">nx_secure_dtls_server_session_start,</span><span class="sxs-lookup"><span data-stu-id="7d363-346">nx_secure_dtls_server_session_start,</span></span>
- <span data-ttu-id="7d363-347">nx_secure_dtls_server_session_stop,</span><span class="sxs-lookup"><span data-stu-id="7d363-347">nx_secure_dtls_server_session_stop,</span></span>
- <span data-ttu-id="7d363-348">nx_secure_dtls_server_local_certificate_add,</span><span class="sxs-lookup"><span data-stu-id="7d363-348">nx_secure_dtls_server_local_certificate_add,</span></span>
- <span data-ttu-id="7d363-349">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="7d363-349">nx_secure_x509_certificate_initialize</span></span>

## <a name="nx_secure_dtls_server_notify_set"></a><span data-ttu-id="7d363-350">nx_secure_dtls_server_notify_set</span><span class="sxs-lookup"><span data-stu-id="7d363-350">nx_secure_dtls_server_notify_set</span></span>

<span data-ttu-id="7d363-351">NetX güvenli DTLS sunucusuna isteğe bağlı bildirim geri çağırma yordamlarını atama</span><span class="sxs-lookup"><span data-stu-id="7d363-351">Assign optional notification callback routines to a NetX Secure DTLS Server</span></span>

### <a name="prototype"></a><span data-ttu-id="7d363-352">Prototype</span><span class="sxs-lookup"><span data-stu-id="7d363-352">Prototype</span></span>

```C
UINT  nx_secure_dtls_server_notify_set(
                         NX_SECURE_DTLS_SERVER *server_ptr,
                         UINT (*disconnect_notify)(
                                      NX_SECURE_DTLS_SESSION *dtls_session),
                         UINT (*error_notify)(
                                      NX_SECURE_DTLS_SESSION *dtls_session,
                                      UINT error_code));

```

### <a name="description"></a><span data-ttu-id="7d363-353">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7d363-353">Description</span></span>

<span data-ttu-id="7d363-354">Bu hizmet, bir DTLS sunucusuna isteğe bağlı bildirim geri çağırma yordamlarını eklemek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7d363-354">This service can be used to add optional notification callback routines to a DTLS server.</span></span> <span data-ttu-id="7d363-355">Yalnızca bir geri çağırma isteniyorsa, geri çağırma parametresi NX_NULL olarak geçirilebilir.</span><span class="sxs-lookup"><span data-stu-id="7d363-355">Either callback parameter may be passed as NX_NULL if only one callback is desired.</span></span>

<span data-ttu-id="7d363-356">Disconnect_notify geri çağırması, uzak bir istemci bir DTLS oturumunu sona erdirdiğinde çağrılır.</span><span class="sxs-lookup"><span data-stu-id="7d363-356">The disconnect_notify callback is invoked when a remote client ends a DTLS session.</span></span> <span data-ttu-id="7d363-357">Dtls_session parametresi, kapatılan oturum örneğidir.</span><span class="sxs-lookup"><span data-stu-id="7d363-357">The dtls_session parameter is the session instance that was closed.</span></span> <span data-ttu-id="7d363-358">Geri çağırma genellikle NX_SUCCESS döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="7d363-358">The callback should generally return NX_SUCCESS.</span></span>

<span data-ttu-id="7d363-359">Error_notify geri çağırma, bir DTLS hatası veya zaman aşımı oluştuğunda çağrılır.</span><span class="sxs-lookup"><span data-stu-id="7d363-359">The error_notify callback is invoked whenever a DTLS error or timeout occurs.</span></span> <span data-ttu-id="7d363-360">Dtls_session parametresi, hatanın gerçekleştiği oturum örneğidir ve error_code soruna neden olan hatanın sayısal durum kodudur (bkz. Ek A)</span><span class="sxs-lookup"><span data-stu-id="7d363-360">The dtls_session parameter is the session instance for which the error occurred, and error_code is the numeric status code for the error that caused the issue (see Appendix A)</span></span>

<span data-ttu-id="7d363-361">NetX güvenli döndürülen hata kodları listesi için hata kodları).</span><span class="sxs-lookup"><span data-stu-id="7d363-361">NetX Secure Return/Error Codes for a list of error codes that may be returned).</span></span> <span data-ttu-id="7d363-362">Geri çağırma genellikle NX_SUCCESS döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="7d363-362">The callback should generally return NX_SUCCESS.</span></span>

### <a name="parameters"></a><span data-ttu-id="7d363-363">Parametreler</span><span class="sxs-lookup"><span data-stu-id="7d363-363">Parameters</span></span>

- <span data-ttu-id="7d363-364">**server_ptr** Daha önce oluşturulmuş bir DTLS sunucu örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="7d363-364">**server_ptr** Pointer to a previously created DTLS Server instance.</span></span>
- <span data-ttu-id="7d363-365">**disconnect_notify** Bir uzak istemci ana bilgisayarı bir DTLS oturumunu her kapattığında, geri çağırma yordamı çağrılır.</span><span class="sxs-lookup"><span data-stu-id="7d363-365">**disconnect_notify** Callback routine invoked whenever a remote client host closes a DTLS session.</span></span>
- <span data-ttu-id="7d363-366">**error_notify** DTLS bir hata veya zaman aşımıyla karşılaştığında çağrılan geri çağırma yordamı.</span><span class="sxs-lookup"><span data-stu-id="7d363-366">**error_notify** Callback routine invoked whenever DTLS encounters an error or timeout.</span></span>

### <a name="return-values"></a><span data-ttu-id="7d363-367">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="7d363-367">Return Values</span></span>

- <span data-ttu-id="7d363-368">**NX_SUCCESS** (0x00) geri çağırma yordamlarının başarıyla atanması.</span><span class="sxs-lookup"><span data-stu-id="7d363-368">**NX_SUCCESS** (0x00) Successful assignment of callback routines.</span></span>
- <span data-ttu-id="7d363-369">**NX_PTR_ERROR** (0x07) geçersiz işaretçi geçirildi.</span><span class="sxs-lookup"><span data-stu-id="7d363-369">**NX_PTR_ERROR** (0x07) Invalid pointer passed.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="7d363-370">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="7d363-370">Allowed From</span></span>

<span data-ttu-id="7d363-371">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="7d363-371">Threads</span></span>

### <a name="example"></a><span data-ttu-id="7d363-372">Örnek</span><span class="sxs-lookup"><span data-stu-id="7d363-372">Example</span></span>

```C
/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

UINT disconnect_notify(NX_SECURE_DTLS_SESSION *dtls_session)
{
NXD_ADDRESS client_ip_addr;
UINT client_port;
UINT local_port;

    /* We have received a disconnection notice (CloseNotify message) from a
       remote client. Application can use the dtls_session parameter for any
       desired processing. */

    /* See what client disconnected by extracting its IP address and port.
       NOTE: depending on how the session ended, the client information may
             no longer be available. */
    status  = nx_secure_dtls_session_client_info_get(dtls_session,
                                                    &ip_addr,
                                                    &client_port,
                                                    &local_port);

    return(NX_SUCCESS);
}

UINT error_notify(NX_SECURE_DTLS_SESSION *dtls_session, UINT error_code)
{
    /* The DTLS server has encountered an error or timeout condition. We
    can use the error_code parameter to determine the error and we
    can insect the dtls_session for more information. */

    return(NX_SUCCESS);
}

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
    UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                LOCAL_SERVER_PORT,
                                NX_IP_PERIODIC_RATE,
                                dtls_server_session_buffer,
                                sizeof(dtls_server_session_buffer),
                                &tls_crypto_table,
                                crypto_metadata_buffer,
                                sizeof(crypto_metadata_buffer),
                                packet_buffer,
                                sizeof(packet_buffer),
                                dtls_server_connect_notify,
                                dtls_server_receive_notify);

    /* Check for errors. */

    /* Other setup (e.g. certificates) goes here … */

    status = nx_secure_dtls_server_notify_set(&dtls_server, disconnect_notify,
                                                                 error_notify);

    /* Start server. */
    status = nx_secure_dtls_server_start(&dtls_server);

    /* Process client requests, etc… */

}

```

### <a name="see-also"></a><span data-ttu-id="7d363-373">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="7d363-373">See Also</span></span>

- <span data-ttu-id="7d363-374">nx_secure_dtls_server_start, nx_secure_dtls_server_create,</span><span class="sxs-lookup"><span data-stu-id="7d363-374">nx_secure_dtls_server_start, nx_secure_dtls_server_create,</span></span>
- <span data-ttu-id="7d363-375">nx_secure_dtls_server_session_start,</span><span class="sxs-lookup"><span data-stu-id="7d363-375">nx_secure_dtls_server_session_start,</span></span>
- <span data-ttu-id="7d363-376">nx_secure_dtls_server_session_stop</span><span class="sxs-lookup"><span data-stu-id="7d363-376">nx_secure_dtls_server_session_stop</span></span>

## <a name="nx_secure_dtls_server_psk_add"></a><span data-ttu-id="7d363-377">nx_secure_dtls_server_psk_add</span><span class="sxs-lookup"><span data-stu-id="7d363-377">nx_secure_dtls_server_psk_add</span></span>

<span data-ttu-id="7d363-378">NetX güvenli DTLS sunucusuna önceden paylaşılan anahtar ekleme</span><span class="sxs-lookup"><span data-stu-id="7d363-378">Add a Pre-Shared Key to a NetX Secure DTLS Server</span></span>

### <a name="prototype"></a><span data-ttu-id="7d363-379">Prototype</span><span class="sxs-lookup"><span data-stu-id="7d363-379">Prototype</span></span>

```C
UINT  nx_secure_dtls_server_psk_add(
                                NX_SECURE_DTLS_SERVER *server_ptr,
                                UCHAR *pre_shared_key, UINT psk_length,
                                UCHAR *psk_identity,
                                UINT identity_length, UCHAR *hint,
                                UINT hint_length);

```

### <a name="description"></a><span data-ttu-id="7d363-380">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7d363-380">Description</span></span>

<span data-ttu-id="7d363-381">Bu hizmet, bir DTLS sunucu denetim bloğuna bir önceden paylaşılan anahtar (PSK), kimlik dizesi ve kimlik ipucu ekler.</span><span class="sxs-lookup"><span data-stu-id="7d363-381">This service adds a Pre-Shared Key (PSK), its identity string, and an identity hint to a DTLS Server control block.</span></span> <span data-ttu-id="7d363-382">PSK ciphersuites etkin ve kullanıldığında, bir dijital sertifika yerine PSK kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7d363-382">The PSK is used in place of a digital certificate when PSK ciphersuites are enabled and used.</span></span>

<span data-ttu-id="7d363-383">Eklenen PSK, DTLS sunucusuna atanan tüm DTLS oturumlarında çoğaltılır (nx_secure_dtls_server_create çağrısında verilen oturum arabelleği aracılığıyla).</span><span class="sxs-lookup"><span data-stu-id="7d363-383">The PSK that is added is replicated across all the DTLS sessions assigned to the DTLS Server (via the session buffer given in the call to nx_secure_dtls_server_create).</span></span>

### <a name="parameters"></a><span data-ttu-id="7d363-384">Parametreler</span><span class="sxs-lookup"><span data-stu-id="7d363-384">Parameters</span></span>

- <span data-ttu-id="7d363-385">**server_ptr** Daha önce oluşturulmuş bir DTLS sunucu örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="7d363-385">**server_ptr** Pointer to a previously created DTLS Server instance.</span></span>
- <span data-ttu-id="7d363-386">**pre_shared_key** Gerçek PSK değeri.</span><span class="sxs-lookup"><span data-stu-id="7d363-386">**pre_shared_key** The actual PSK value.</span></span>
- <span data-ttu-id="7d363-387">**psk_length** PSK değeri uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="7d363-387">**psk_length** The length of the PSK value.</span></span>
- <span data-ttu-id="7d363-388">**psk_identity** Bu PSK değerini tanımlamak için kullanılan dize.</span><span class="sxs-lookup"><span data-stu-id="7d363-388">**psk_identity** A string used to identify this PSK value.</span></span>
- <span data-ttu-id="7d363-389">**identity_length** PSK kimliğinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="7d363-389">**identity_length** The length of the PSK identity.</span></span>
- <span data-ttu-id="7d363-390">**İpucu** Bir TLS sunucusunda hangi sayıda PSKs arasından seçim yapmak gerektiğini göstermek için kullanılan dize.</span><span class="sxs-lookup"><span data-stu-id="7d363-390">**hint** A string used to indicate which group of PSKs to choose from on a TLS server.</span></span>
- <span data-ttu-id="7d363-391">**hint_length** İpucu dizesinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="7d363-391">**hint_length** The length of the hint string.</span></span>

### <a name="return-values"></a><span data-ttu-id="7d363-392">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="7d363-392">Return Values</span></span>

- <span data-ttu-id="7d363-393">**NX_SUCCESS** (0x00) PSK 'nin başarılı bir şekilde eklenmesi.</span><span class="sxs-lookup"><span data-stu-id="7d363-393">**NX_SUCCESS** (0x00) Successful addition of PSK.</span></span>
- <span data-ttu-id="7d363-394">**NX_PTR_ERROR** (0x07) geçersiz DTLS sunucu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="7d363-394">**NX_PTR_ERROR** (0x07) Invalid DTLS server pointer.</span></span>
- <span data-ttu-id="7d363-395">**NX_SECURE_TLS_NO_MORE_PSK_SPACE** (0x125) başka bir PSK eklenemiyor.</span><span class="sxs-lookup"><span data-stu-id="7d363-395">**NX_SECURE_TLS_NO_MORE_PSK_SPACE** (0x125) Cannot add another PSK.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="7d363-396">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="7d363-396">Allowed From</span></span>

<span data-ttu-id="7d363-397">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="7d363-397">Threads</span></span>

### <a name="example"></a><span data-ttu-id="7d363-398">Örnek</span><span class="sxs-lookup"><span data-stu-id="7d363-398">Example</span></span>

```C
/* PSK value.  */
UCHAR psk[] = { 0x1a, 0x2b, 0x3c, 0x4d };

/* Add PSK to DTLS session.  */
status =  nx_secure_dtls_server_psk_add(&dtls_server, psk, sizeof(psk), “psk_1”,
   4, “Client_identity”, 15);


/* If status is NX_SUCCESS the PSK was successfully added.  */

```

### <a name="see-also"></a><span data-ttu-id="7d363-399">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="7d363-399">See Also</span></span>

- <span data-ttu-id="7d363-400">nx_secure_dtls_psk_add, nx_secure_dtls_server_create</span><span class="sxs-lookup"><span data-stu-id="7d363-400">nx_secure_dtls_psk_add, nx_secure_dtls_server_create</span></span>

## <a name="nx_secure_dtls_server_session_send"></a><span data-ttu-id="7d363-401">nx_secure_dtls_server_session_send</span><span class="sxs-lookup"><span data-stu-id="7d363-401">nx_secure_dtls_server_session_send</span></span>

<span data-ttu-id="7d363-402">NetX güvenli DTLS sunucusuyla kurulu bir DTLS oturumu üzerinden veri gönderme</span><span class="sxs-lookup"><span data-stu-id="7d363-402">Send data over a DTLS session established with a NetX Secure DTLS Server</span></span>

### <a name="prototype"></a><span data-ttu-id="7d363-403">Prototype</span><span class="sxs-lookup"><span data-stu-id="7d363-403">Prototype</span></span>

```C
UINT  nx_secure_dtls_server_session_send(
                                NX_SECURE_DTLS_SESSION *session_ptr,
                               NX_PACKET *packet_ptr);

```

### <a name="description"></a><span data-ttu-id="7d363-404">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7d363-404">Description</span></span>

<span data-ttu-id="7d363-405">Bu hizmet, uzak DTLS Istemci konağına, belirlenen DTLS sunucusu oturumu üzerinden bir veri paketi gönderir.</span><span class="sxs-lookup"><span data-stu-id="7d363-405">This service sends a packet of data over an established DTLS Server session to a remote DTLS Client host.</span></span> <span data-ttu-id="7d363-406">Kullanılan oturum, nx_secure_dtls_session_create için sunulan receive_notify geri çağırma yordamında elde edilir.</span><span class="sxs-lookup"><span data-stu-id="7d363-406">The session used is obtained in the receive_notify callback routine provided to nx_secure_dtls_session_create.</span></span>

<span data-ttu-id="7d363-407">Pakette belirtilen veriler, *nx_secure_dtls_packet_allocate* kullanılarak ayrılması gereken DTLS oturum şifreleme parametreleri ve yordamları kullanılarak şifrelenir ve ardından DTLS sunucusu iç UDP bağlantı noktası üzerinden uzak ana bilgisayara, eklenen istemcinin IP adresine ve bağlantı noktasına (DTLS oturumunda depolanır) gönderilir.</span><span class="sxs-lookup"><span data-stu-id="7d363-407">The data provided in the packet, which must be allocated using *nx_secure_dtls_packet_allocate*, is encrypted using the DTLS session cryptographic parameters and routines and then sent to the remote host over the DTLS Server internal UDP port to the attached client’s IP address and port (stored in the DTLS Session).</span></span>

### <a name="parameters"></a><span data-ttu-id="7d363-408">Parametreler</span><span class="sxs-lookup"><span data-stu-id="7d363-408">Parameters</span></span>

- <span data-ttu-id="7d363-409">**session_ptr** Uygulama tarafından sunulan receive_notify geri çağırma yordamından alınan DTLS oturum örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="7d363-409">**session_ptr** Pointer to a DTLS session instance obtained from the receive_notify callback routine provided by the application.</span></span>
- <span data-ttu-id="7d363-410">**packet_ptr** Daha önce ayrılan ve uygulama verileriyle doldurulmuş bir NX_PACKET örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="7d363-410">**packet_ptr** Pointer to an NX_PACKET instance allocated previously and populated with application data.</span></span>

### <a name="return-values"></a><span data-ttu-id="7d363-411">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="7d363-411">Return Values</span></span>

- <span data-ttu-id="7d363-412">**NX_SUCCESS** (0x00) DTLS sunucusu başarıyla oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="7d363-412">**NX_SUCCESS** (0x00) Successful creation of DTLS server.</span></span>
- <span data-ttu-id="7d363-413">**NX_PTR_ERROR** (0x07) geçersiz işaretçi geçirildi.</span><span class="sxs-lookup"><span data-stu-id="7d363-413">**NX_PTR_ERROR** (0x07) Invalid pointer passed.</span></span>
- <span data-ttu-id="7d363-414">**NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) temel alınan UDP gönderme işleminde bir hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="7d363-414">**NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) An error occurred in the underlying UDP send operation.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="7d363-415">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="7d363-415">Allowed From</span></span>

<span data-ttu-id="7d363-416">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="7d363-416">Threads</span></span>

### <a name="example"></a><span data-ttu-id="7d363-417">Örnek</span><span class="sxs-lookup"><span data-stu-id="7d363-417">Example</span></span>

```C
#define DTLS_SERVER_SESSION (3)

/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Flag used to indicate application data reception. */
UINT receive_flag = 0;

/* Pointer to session for application data receive.
   NOTE: Should be an array or list as
   with new_dtls_session */
NX_SECURE_DTLS_SESSION *receive_dtls_session;


/* Receive notify callback routine invoked when DTLS application data is received
   on an existing DTLS server session. */
UINT dtls_server_receive_notify(NX_SECURE_DTLS_SESSION *dtls_session)
{
    /* Receive and process DTLS record.
       NOTE: Mutex handling omitted for clarity. */
    receive_flag = 1;
    receive_dtls_session = dtls_session;

    return(NX_SUCCESS);
}

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
    NX_PACKET *send_packet;
    NX_PACKET *receive_packet;
    UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                LOCAL_SERVER_PORT,
                                NX_IP_PERIODIC_RATE,
                                dtls_server_session_buffer,
                                sizeof(dtls_server_session_buffer),
                                &tls_crypto_table,
                                crypto_metadata_buffer,
                                sizeof(crypto_metadata_buffer),
                                packet_buffer,
                                sizeof(packet_buffer),
                                dtls_server_connect_notify,
                                dtls_server_receive_notify);

    /* Check for errors. */

    /* Initialize local server identity certificate with key
    and add to server. */
    status = nx_secure_x509_certificate_initialize(&certificate,
                                        device_cert_der,
                                        device_cert_der_len,
                                        NX_NULL,
                                        0, device_cert_key_der,
                                        device_cert_key_der_len,
                                        NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_local_certificate_add(&dtls_server,
                                                    &certificate, 1);


    /* Start server. */
    status = nx_secure_dtls_server_start(&dtls_server);

    /* Loop continuously to handle incoming data. */
    while(1)
    {
        /* Check for new connections. Muxtex handling omitted for clarity. */
        if(connect_flag)
        {
            /* We have a new connection attempt, start the DTLS session. */
            status = nx_secure_dtls_server_session_start(new_dtls_session,
                                                    NX_IP_PERIODIC_RATE);

            /* Check for errors. */
        }

        /* Check for received application data. */
        if(receive_flag)
        {
            /* We have received data over a previously-established DTLS session.
               Mutex handling omitted for clarity. */
            Status = nx_secure_dtls_session_receive(receive_dtls_session,
                                                    &receive_packet,
                                                    NX_IP_PERIODIC_RATE);

            /* Process received data… */

            /* Prepare and send response to client. */
        status = nx_secure_dtls_packet_allocate(receive_dtls_session,
                                                &packet_pool,
                                                &send_packet,
                                                NX_IP_PERIODIC_RATE);

        /* Check for errors and prepare response data
        (e.g. nx_packet_data_append). */

        /* Send response to client. */
        status = nx_secure_dtls_server_session_send(receive_dtls_session,
                                                            send_packet);

}

/* If not processing connections or received data, let the thread sleep. */
if(!connect_flag && !receive_flag)
{
    tx_thread_sleep(100);
}
    }

    /* Server processing is done, stop the server instance
    from accepting requests. */
    status = nx_secure_dtls_server_stop(&dtls_server);

    /* If we exit the processing loop, clean up the server. */
    status = nx_secure_dtls_server_delete(&dtls_server);
}

```

### <a name="see-also"></a><span data-ttu-id="7d363-418">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="7d363-418">See Also</span></span>

- <span data-ttu-id="7d363-419">nx_secure_dtls_server_start, nx_secure_dtls_server_delete,</span><span class="sxs-lookup"><span data-stu-id="7d363-419">nx_secure_dtls_server_start, nx_secure_dtls_server_delete,</span></span>
- <span data-ttu-id="7d363-420">nx_secure_dtls_session_receive, nx_secure_dtls_server_session_create,</span><span class="sxs-lookup"><span data-stu-id="7d363-420">nx_secure_dtls_session_receive, nx_secure_dtls_server_session_create,</span></span>
- <span data-ttu-id="7d363-421">nx_secure_dtls_server_session_start, nx_secure_dtls_server_session_stop,</span><span class="sxs-lookup"><span data-stu-id="7d363-421">nx_secure_dtls_server_session_start, nx_secure_dtls_server_session_stop,</span></span>
- <span data-ttu-id="7d363-422">nx_secure_dtls_server_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="7d363-422">nx_secure_dtls_server_local_certificate_add</span></span>

## <a name="nx_secure_dtls_server_session_start"></a><span data-ttu-id="7d363-423">nx_secure_dtls_server_session_start</span><span class="sxs-lookup"><span data-stu-id="7d363-423">nx_secure_dtls_server_session_start</span></span>

<span data-ttu-id="7d363-424">NetX güvenli DTLS sunucusundan DTLS oturumu başlatma</span><span class="sxs-lookup"><span data-stu-id="7d363-424">Start a DTLS Session from a NetX Secure DTLS Server</span></span>

### <a name="prototype"></a><span data-ttu-id="7d363-425">Prototype</span><span class="sxs-lookup"><span data-stu-id="7d363-425">Prototype</span></span>

```C
UINT  nx_secure_dtls_server_session_start(
                 NX_SECURE_DTLS_SESSION *session_ptr, UINT wait_option);

```

### <a name="description"></a><span data-ttu-id="7d363-426">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7d363-426">Description</span></span>

<span data-ttu-id="7d363-427">Bu hizmet, uzak bir DTLS Istemcisi sunucuya bağlanıp bir DTLS bağlantısı talep edildiğinde sunucu tarafı DTLS anlaşmasını gerçekleştirerek bir DTLS sunucu oturumu başlatır.</span><span class="sxs-lookup"><span data-stu-id="7d363-427">This service starts a DTLS Server session by performing the server-side DTLS handshake when a remote DTLS Client has connected to the server and requested a DTLS connection.</span></span>

<span data-ttu-id="7d363-428">DTLS oturumu nx_secure_dtls_server_create için sunulan connect_notify geri çağırma yordamında alınır.</span><span class="sxs-lookup"><span data-stu-id="7d363-428">The DTLS Session is obtained in the connect_notify callback routine provided to nx_secure_dtls_server_create.</span></span>

### <a name="parameters"></a><span data-ttu-id="7d363-429">Parametreler</span><span class="sxs-lookup"><span data-stu-id="7d363-429">Parameters</span></span>

- <span data-ttu-id="7d363-430">**session_ptr** DTLS sunucusundan alınan DTLS oturum örneğinin işaretçisi connect_notify geri çağırma.</span><span class="sxs-lookup"><span data-stu-id="7d363-430">**session_ptr** Pointer to a DTLS Session instance obtained from a DTLS Server connect_notify callback.</span></span>
- <span data-ttu-id="7d363-431">**wait_option** Ağ işlemleri için kullanılacak ThreadX bekleme değeri.</span><span class="sxs-lookup"><span data-stu-id="7d363-431">**wait_option** ThreadX wait value to use for network operations.</span></span>

### <a name="return-values"></a><span data-ttu-id="7d363-432">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="7d363-432">Return Values</span></span>

- <span data-ttu-id="7d363-433">**NX_SUCCESS** (0x00) DTLS sunucusu başarıyla oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="7d363-433">**NX_SUCCESS** (0x00) Successful creation of DTLS server.</span></span>
- <span data-ttu-id="7d363-434">**NX_PTR_ERROR** (0x07) geçersiz işaretçi geçirildi.</span><span class="sxs-lookup"><span data-stu-id="7d363-434">**NX_PTR_ERROR** (0x07) Invalid pointer passed.</span></span>
- <span data-ttu-id="7d363-435">**NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) BIR DTLS el sıkışma paketi ayıramadı (paket havuzu boş).</span><span class="sxs-lookup"><span data-stu-id="7d363-435">**NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) Could not allocate a DTLS handshake packet (packet pool empty).</span></span>
- <span data-ttu-id="7d363-436">**NX_SECURE_TLS_INVALID_PACKET** (0x104) geçerli bir DTLS kaydı olmayan veri alındı.</span><span class="sxs-lookup"><span data-stu-id="7d363-436">**NX_SECURE_TLS_INVALID_PACKET** (0x104) Recevied data that was not a valid DTLS record.</span></span>
- <span data-ttu-id="7d363-437">**NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0x108) DTLS kaydı düzgün bir şekilde karıştırılıp (şifreleme hatası) başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="7d363-437">**NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0x108) A DTLS record failed to be properly hashed (encryption error).</span></span>
- <span data-ttu-id="7d363-438">**NX_SECURE_TLS_PADDING_CHECK_FAILED** (0x12a) şifreleme doldurma denetimi hatası.</span><span class="sxs-lookup"><span data-stu-id="7d363-438">**NX_SECURE_TLS_PADDING_CHECK_FAILED** (0x12A) Encryption padding check failure.</span></span>
- <span data-ttu-id="7d363-439">**NX_SECURE_TLS_ALERT_RECEIVED** (0x114), DTLS el sıkışması sırasında uzak ana bilgisayardan bir uyarı alındı.</span><span class="sxs-lookup"><span data-stu-id="7d363-439">**NX_SECURE_TLS_ALERT_RECEIVED** (0x114) Recevied an alert from the remote host during the DTLS handshake.</span></span>
- <span data-ttu-id="7d363-440">**NX_SECURE_TLS_UNRECOGNIZED_MESSAGE_TYPE** (0x102), DTLS el sıkışması sırasında tanınmayan bir ileti aldı.</span><span class="sxs-lookup"><span data-stu-id="7d363-440">**NX_SECURE_TLS_UNRECOGNIZED_MESSAGE_TYPE** (0x102) Received an unrecognized message during the DTLS handshake.</span></span>
- <span data-ttu-id="7d363-441">**NX_SECURE_TLS_INCORRECT_MESSAGE_LENGTH** (0x10a), geçersiz uzunluğa sahıp bır DTLS kaydı alındı.</span><span class="sxs-lookup"><span data-stu-id="7d363-441">**NX_SECURE_TLS_INCORRECT_MESSAGE_LENGTH** (0x10A) Recevied a DTLS record with an invalid length.</span></span>
- <span data-ttu-id="7d363-442">**NX_SECURE_TLS_NO_SUPPORTED_CIPHERS** (0x10e), desteklenen DTLS cipherpaketlerine sahip olmayan bir ClientHello aldı.</span><span class="sxs-lookup"><span data-stu-id="7d363-442">**NX_SECURE_TLS_NO_SUPPORTED_CIPHERS** (0x10E) Received a ClientHello with no supported DTLS ciphersuites.</span></span>
- <span data-ttu-id="7d363-443">**NX_SECURE_TLS_BAD_COMPRESSION_METHOD** (0x118) bilinmeyen bir sıkıştırma yöntemiyle bir ClientHello alındı.</span><span class="sxs-lookup"><span data-stu-id="7d363-443">**NX_SECURE_TLS_BAD_COMPRESSION_METHOD** (0x118) Recevied a ClientHello with a unknown compression method.</span></span>
- <span data-ttu-id="7d363-444">**NX_SECURE_TLS_HANDSHAKE_FAILURE** (0X107) genel (belirtilmemiş) el sıkışma hatası, genellikle uzantı işleme sorunları nedeniyle.</span><span class="sxs-lookup"><span data-stu-id="7d363-444">**NX_SECURE_TLS_HANDSHAKE_FAILURE** (0x107) Generic (unspecified) handshake failure, usually due to problems with extension processing.</span></span>
- <span data-ttu-id="7d363-445">**NX_SECURE_TLS_UNSUPPORTED_FEATURE** (0x130) DTLS el sıkışması sırasında henüz desteklenmeyen bir özellik çağrılmıştı.</span><span class="sxs-lookup"><span data-stu-id="7d363-445">**NX_SECURE_TLS_UNSUPPORTED_FEATURE** (0x130) A feature that is not yet supported was invoked during the DTLS handshake.</span></span>
- <span data-ttu-id="7d363-446">**NX_SECURE_TLS_UNKNOWN_CIPHERSUITE** (0x105) bilinmeyen bir ciphersuite ile karşılaşıldı (iç şifreleme hatası belirtildi).</span><span class="sxs-lookup"><span data-stu-id="7d363-446">**NX_SECURE_TLS_UNKNOWN_CIPHERSUITE** (0x105) An unknown ciphersuite was encountered (indicated internal cryptography error).</span></span>
- <span data-ttu-id="7d363-447">**NX_SECURE_TLS_PROTOCOL_VERSION_CHANGED** (0x12e) eşleşmeyen DTLS sürümüne sahıp bır DTLS kaydı alındı.</span><span class="sxs-lookup"><span data-stu-id="7d363-447">**NX_SECURE_TLS_PROTOCOL_VERSION_CHANGED** (0x12E) Recevied a DTLS record with a mismatched DTLS version.</span></span>
- <span data-ttu-id="7d363-448">**NX_SECURE_TLS_FINISHED_HASH_FAILURE** (0x115) DTLS el sıkışma karmasını doğrulayamadı, oturum geçersiz.</span><span class="sxs-lookup"><span data-stu-id="7d363-448">**NX_SECURE_TLS_FINISHED_HASH_FAILURE** (0x115) Failed to validate the DTLS handshake hash, session is invalid.</span></span>
- <span data-ttu-id="7d363-449">**NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) iç UDP gönderme başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="7d363-449">**NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) Internal UDP send failed.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="7d363-450">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="7d363-450">Allowed From</span></span>

<span data-ttu-id="7d363-451">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="7d363-451">Threads</span></span>

### <a name="example"></a><span data-ttu-id="7d363-452">Örnek</span><span class="sxs-lookup"><span data-stu-id="7d363-452">Example</span></span>

```C
#define DTLS_SERVER_SESSION (3)

/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Allocate space for DTLS sessions in the DTLS server. */
UCHAR dtls_server_session_buffer[sizeof(NX_SECURE_DTLS_SESSION)
* DTLS_SERVER_SESSIONS];

/* Flag used to indicate that a DTLS Client has connected. */
UINT connect_flag = 0;

/* Flag used to indicate application data reception. */
UINT receive_flag = 0;

/* Pointer to newly-connected DTLS session.
   NOTE: In practice this should be an array or list in case a new connection is
         attempted while a previous session is being started. */
NX_SECURE_DTLS_SESSION *new_dtls_session;

/* Pointer to session for application data receive.
   NOTE: Should be an array or list as
   with new_dtls_session */
NX_SECURE_DTLS_SESSION *receive_dtls_session;

/* Connect notify callback routine. */
UINT dtls_server_connect_notify(NX_SECURE_DTLS_SESSION *dtls_session,
                                    NXD_ADDRESS *ip_address, UINT port)
{
    /* NOTE: proper inter-thread communication procedures (e.g. mutex handling)
             Omitted for clarity. */

    /* Notify application thread that a connection request has been received. */
    connect_flag = 1;
    new_dtls_session = dtls_session;

    return(NX_SUCCESS);
}

/* Receive notify callback routine invoked when DTLS application data is received
   on an existing DTLS server session. */
UINT dtls_server_receive_notify(NX_SECURE_DTLS_SESSION *dtls_session)
{
    /* Receive and process DTLS record.
       NOTE: Mutex handling omitted for clarity. */
    receive_flag = 1;
    receive_dtls_session = dtls_session;

    return(NX_SUCCESS);
}

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
    NX_PACKET *send_packet;
    NX_PACKET *receive_packet;
    UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                LOCAL_SERVER_PORT, NX_IP_PERIODIC_RATE,
                                dtls_server_session_buffer,
                                sizeof(dtls_server_session_buffer),
                                &tls_crypto_table, crypto_metadata_buffer,
                                sizeof(crypto_metadata_buffer), packet_buffer,
                                sizeof(packet_buffer),
                                dtls_server_connect_notify,
                                dtls_server_receive_notify);

    /* Initialize local server identity certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&certificate, device_cert_der,
                                            device_cert_der_len, NX_NULL, 0,
                                            device_cert_key_der,
                                            device_cert_key_der_len,
                                            NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_local_certificate_add(&dtls_server,
                                                    &certificate, 1);

    /* Start server. */
    status = nx_secure_dtls_server_start(&dtls_server);

    /* Loop continuously to handle incoming data. */
    while(1)
    {
        /* Check for new connections. Muxtex handling omitted for clarity. */
        if(connect_flag)
        {
            /* We have a new connection attempt, start the DTLS session. */
            status = nx_secure_dtls_server_session_start(new_dtls_session,
                                                    NX_IP_PERIODIC_RATE);
        }

        /* Check for received application data. */
        if(receive_flag)
        {
            /* We have received data over a previously-established DTLS session.
               Mutex handling omitted for clarity. */
            Status = nx_secure_dtls_session_receive(receive_dtls_session,
                                                        &receive_packet,
                                                        NX_IP_PERIODIC_RATE);

            /* Process received data… */

            /* Prepare and send response to client. */
            status = nx_secure_dtls_packet_allocate(receive_dtls_session,
                                                    &packet_pool, &send_packet,
                                                    NX_IP_PERIODIC_RATE);

            /* Check for errors and prepare response data
            (e.g. nx_packet_data_append). */

            /* Send response to client. */
            status = nx_secure_dtls_server_session_send(receive_dtls_session,
                                                                send_packet);

        }

        /* If not processing connections or received data, let the thread sleep. */
        if(!connect_flag && !receive_flag)
        {
            tx_thread_sleep(100);
        }
    }

    /* Server processing is done,
    stop the server instance from accepting requests. */
    status = nx_secure_dtls_server_stop(&dtls_server);

    /* If we exit the processing loop, clean up the server. */
    status = nx_secure_dtls_server_delete(&dtls_server);
}

```

### <a name="see-also"></a><span data-ttu-id="7d363-453">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="7d363-453">See Also</span></span>

- <span data-ttu-id="7d363-454">nx_secure_dtls_server_start, nx_secure_dtls_server_delete,</span><span class="sxs-lookup"><span data-stu-id="7d363-454">nx_secure_dtls_server_start, nx_secure_dtls_server_delete,</span></span>
- <span data-ttu-id="7d363-455">nx_secure_dtls_session_receive, nx_secure_dtls_server_session_send,</span><span class="sxs-lookup"><span data-stu-id="7d363-455">nx_secure_dtls_session_receive, nx_secure_dtls_server_session_send,</span></span>
- <span data-ttu-id="7d363-456">nx_secure_dtls_server_session_create, nx_secure_dtls_server_session_stop,</span><span class="sxs-lookup"><span data-stu-id="7d363-456">nx_secure_dtls_server_session_create, nx_secure_dtls_server_session_stop,</span></span>
- <span data-ttu-id="7d363-457">nx_secure_dtls_server_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="7d363-457">nx_secure_dtls_server_local_certificate_add</span></span>

## <a name="nx_secure_dtls_server_start"></a><span data-ttu-id="7d363-458">nx_secure_dtls_server_start</span><span class="sxs-lookup"><span data-stu-id="7d363-458">nx_secure_dtls_server_start</span></span>

<span data-ttu-id="7d363-459">Yapılandırılmış UDP bağlantı noktasında dinleme yapan bir NetX güvenli DTLS sunucu örneği başlatın</span><span class="sxs-lookup"><span data-stu-id="7d363-459">Start a NetX Secure DTLS Server instance listening on the configured UDP port</span></span>

### <a name="prototype"></a><span data-ttu-id="7d363-460">Prototype</span><span class="sxs-lookup"><span data-stu-id="7d363-460">Prototype</span></span>

```C
UINT  nx_secure_dtls_server_start(
                  NX_SECURE_DTLS_SERVER *server_ptr);

```

### <a name="description"></a><span data-ttu-id="7d363-461">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7d363-461">Description</span></span>

<span data-ttu-id="7d363-462">Bu hizmet bir DTLS sunucusu başlatır.</span><span class="sxs-lookup"><span data-stu-id="7d363-462">This service starts a DTLS Server.</span></span> <span data-ttu-id="7d363-463">Çağrı geri döndüğünde, sunucu etkindir ve DTLS istemcilerinden gelen istekleri işlemeye başlayacaktır.</span><span class="sxs-lookup"><span data-stu-id="7d363-463">After the call returns, the server is active and will begin processing incoming requests from DTLS clients.</span></span> <span data-ttu-id="7d363-464">Sunucu örneği, hizmet *nx_secure_dtls_server_create* yapılandırılmış olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7d363-464">The server instance must have been configured with the service *nx_secure_dtls_server_create*.</span></span>

> [!NOTE]
> <span data-ttu-id="7d363-465">Bu hizmet, iç DTLS sunucusu UDP bağlantı noktasını yapılandırılmış yerel bağlantı noktasına bağlar, bu nedenle karşılaşılan çoğu sorun UDP iletişimleri ve ağ yapılandırması ile yapılır.</span><span class="sxs-lookup"><span data-stu-id="7d363-465">This service binds the internal DTLS Server UDP port to the configured local port so most issues encountered will have to do with UDP communications and network configuration.</span></span>

### <a name="parameters"></a><span data-ttu-id="7d363-466">Parametreler</span><span class="sxs-lookup"><span data-stu-id="7d363-466">Parameters</span></span>

- <span data-ttu-id="7d363-467">**server_ptr** Daha önce oluşturulmuş bir DTLS sunucu örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="7d363-467">**server_ptr** Pointer to a previously created DTLS Server instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="7d363-468">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="7d363-468">Return Values</span></span>

- <span data-ttu-id="7d363-469">**NX_SUCCESS** (0x00) sunucu başarıyla başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="7d363-469">**NX_SUCCESS** (0x00) Successful start of server.</span></span>
- <span data-ttu-id="7d363-470">**NX_PTR_ERROR** (0x07) geçersiz işaretçi geçirildi.</span><span class="sxs-lookup"><span data-stu-id="7d363-470">**NX_PTR_ERROR** (0x07) Invalid pointer passed.</span></span>
- <span data-ttu-id="7d363-471">**NX_NOT_ENABLED** (0x14) UDP etkin değil.</span><span class="sxs-lookup"><span data-stu-id="7d363-471">**NX_NOT_ENABLED** (0x14) UDP not enabled.</span></span>
- <span data-ttu-id="7d363-472">**NX_NO_FREE_PORTS** (0x45) kullanılabilir UDP bağlantı noktası yok.</span><span class="sxs-lookup"><span data-stu-id="7d363-472">**NX_NO_FREE_PORTS** (0x45) No available UDP ports.</span></span>
- <span data-ttu-id="7d363-473">**NX_INVALID_PORT** (0x46) geçersiz UDP bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="7d363-473">**NX_INVALID_PORT** (0x46) Invalid UDP port.</span></span>
- <span data-ttu-id="7d363-474">**NX_ALREADY_BOUND** (0x22) UDP bağlantı noktası zaten bağlıydı.</span><span class="sxs-lookup"><span data-stu-id="7d363-474">**NX_ALREADY_BOUND** (0x22) UDP port already bound.</span></span>
- <span data-ttu-id="7d363-475">**NX_PORT_UNAVAILABLE** (0x23) UDP bağlantı noktası kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="7d363-475">**NX_PORT_UNAVAILABLE** (0x23) UDP port not available for use.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="7d363-476">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="7d363-476">Allowed From</span></span>

<span data-ttu-id="7d363-477">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="7d363-477">Threads</span></span>

### <a name="example"></a><span data-ttu-id="7d363-478">Örnek</span><span class="sxs-lookup"><span data-stu-id="7d363-478">Example</span></span>

```C
#define DTLS_SERVER_SESSION (3)

/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Allocate space for DTLS sessions in the DTLS server. */
UCHAR dtls_server_session_buffer[sizeof(NX_SECURE_DTLS_SESSION)
                                        * DTLS_SERVER_SESSIONS];

/* Flag used to indicate that a DTLS Client has connected. */
UINT connect_flag = 0;

/* Flag used to indicate application data reception. */
UINT receive_flag = 0;

/* Pointer to newly-connected DTLS session.
   NOTE: In practice this should be an array or list in case a new connection is
         attempted while a previous session is being started. */
NX_SECURE_DTLS_SESSION *new_dtls_session;

/* Pointer to session for application data receive.
   NOTE: Should be an array or list as
   with new_dtls_session */
NX_SECURE_DTLS_SESSION *receive_dtls_session;

/* Connect notify callback routine. */
UINT dtls_server_connect_notify(NX_SECURE_DTLS_SESSION *dtls_session,
                                    NXD_ADDRESS *ip_address, UINT port)
{
    /* NOTE: proper inter-thread communication procedures (e.g. mutex handling)
             Omitted for clarity. */

    /* Notify application thread that a connection request has been received. */
    connect_flag = 1;
    new_dtls_session = dtls_session;

    return(NX_SUCCESS);
}

/* Receive notify callback routine invoked when DTLS application data is received
   on an existing DTLS server session. */
UINT dtls_server_receive_notify(NX_SECURE_DTLS_SESSION *dtls_session)
{
    /* Receive and process DTLS record.
       NOTE: Mutex handling omitted for clarity. */
    receive_flag = 1;
    receive_dtls_session = dtls_session;

    return(NX_SUCCESS);
}

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
    NX_PACKET *send_packet;
    NX_PACKET *receive_packet;
    UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                    LOCAL_SERVER_PORT,
                                    NX_IP_PERIODIC_RATE,
                                    dtls_server_session_buffer,
                                    sizeof(dtls_server_session_buffer),
                                    &tls_crypto_table,
                                    crypto_metadata_buffer,
                                    sizeof(crypto_metadata_buffer),
                                    packet_buffer,
                                    sizeof(packet_buffer),
                                    dtls_server_connect_notify,
                                    dtls_server_receive_notify);

    /* Initialize local server identity certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&certificate, device_cert_der,
                                            device_cert_der_len,
                                            NX_NULL, 0,
                                            device_cert_key_der,
                                            device_cert_key_der_len,
                                            NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_local_certificate_add(&dtls_server,
                                                        &certificate, 1);

    /* Start server. */
    status = nx_secure_dtls_server_start(&dtls_server);

    /* Loop continuously to handle incoming data. */
    while(1)
    {
        /* Check for new connections. Muxtex handling omitted for clarity. */
        if(connect_flag)
        {
            /* We have a new connection attempt, start the DTLS session. */
            status = nx_secure_dtls_server_session_start(new_dtls_session,
                                            NX_IP_PERIODIC_RATE);

            /* Check for errors. */
        }

        /* Check for received application data. */
        if(receive_flag)
        {
            /* We have received data over a previously-established DTLS session.
               Mutex handling omitted for clarity. */
            Status = nx_secure_dtls_session_receive(receive_dtls_session,
                                                        &receive_packet,
                                                        NX_IP_PERIODIC_RATE);

            /* Process received data… */

            /* Prepare and send response to client. */
            status = nx_secure_dtls_packet_allocate(receive_dtls_session, &packet_pool,
                &send_packet, NX_IP_PERIODIC_RATE);

            /* Check for errors and prepare response data
                (e.g. nx_packet_data_append). */

            /* Send response to client. */
            status = nx_secure_dtls_server_session_send(receive_dtls_session,
                send_packet);
        }

        /* If not processing connections or received data, let the thread sleep. */
        if(!connect_flag && !receive_flag)
        {
            tx_thread_sleep(100);
        }
    }

    /* If we exit the processing loop, clean up the server. */
    status = nx_secure_dtls_server_delete(&dtls_server);
}

```

### <a name="see-also"></a><span data-ttu-id="7d363-479">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="7d363-479">See Also</span></span>

- <span data-ttu-id="7d363-480">nx_secure_dtls_server_stop, nx_secure_dtls_server_create,</span><span class="sxs-lookup"><span data-stu-id="7d363-480">nx_secure_dtls_server_stop, nx_secure_dtls_server_create,</span></span>
- <span data-ttu-id="7d363-481">nx_secure_dtls_server_delete, nx_secure_dtls_session_receive,</span><span class="sxs-lookup"><span data-stu-id="7d363-481">nx_secure_dtls_server_delete, nx_secure_dtls_session_receive,</span></span>
- <span data-ttu-id="7d363-482">nx_secure_dtls_server_session_send,</span><span class="sxs-lookup"><span data-stu-id="7d363-482">nx_secure_dtls_server_session_send,</span></span>
- <span data-ttu-id="7d363-483">nx_secure_dtls_server_session_start</span><span class="sxs-lookup"><span data-stu-id="7d363-483">nx_secure_dtls_server_session_start</span></span>

## <a name="nx_secure_dtls_server_stop"></a><span data-ttu-id="7d363-484">nx_secure_dtls_server_stop</span><span class="sxs-lookup"><span data-stu-id="7d363-484">nx_secure_dtls_server_stop</span></span>

<span data-ttu-id="7d363-485">Etkin bir NetX güvenli DTLS sunucu örneğini durdur</span><span class="sxs-lookup"><span data-stu-id="7d363-485">Stop an active NetX Secure DTLS Server instance</span></span>

### <a name="prototype"></a><span data-ttu-id="7d363-486">Prototype</span><span class="sxs-lookup"><span data-stu-id="7d363-486">Prototype</span></span>

```C
UINT  nx_secure_dtls_server_stop(NX_SECURE_DTLS_SERVER *server_ptr);
```

### <a name="description"></a><span data-ttu-id="7d363-487">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7d363-487">Description</span></span>

<span data-ttu-id="7d363-488">Bu hizmet, bir DTLS sunucusunun UDP bağlantı noktasını yapılandırma bölümünde dinleme yaptığı ve tüm devam eden DTLS iletişimlerini sıfırlayıp tüm devam eden DTLS oturumlarını sıfırlamasından yanıt vermez.</span><span class="sxs-lookup"><span data-stu-id="7d363-488">This service stops a DTLS Server from listening on the configure UDP port and resets all the associated DTLS sessions, halting any in-progress DTLS communications.</span></span>

### <a name="parameters"></a><span data-ttu-id="7d363-489">Parametreler</span><span class="sxs-lookup"><span data-stu-id="7d363-489">Parameters</span></span>

- <span data-ttu-id="7d363-490">**server_ptr** Etkin bir DTLS sunucu örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="7d363-490">**server_ptr** Pointer to an active DTLS Server instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="7d363-491">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="7d363-491">Return Values</span></span>

- <span data-ttu-id="7d363-492">**NX_SUCCESS** (0x00) sunucu başarıyla durdu.</span><span class="sxs-lookup"><span data-stu-id="7d363-492">**NX_SUCCESS** (0x00) Successful stop of server.</span></span>
- <span data-ttu-id="7d363-493">**NX_PTR_ERROR** (0x07) geçersiz işaretçi geçirildi.</span><span class="sxs-lookup"><span data-stu-id="7d363-493">**NX_PTR_ERROR** (0x07) Invalid pointer passed.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="7d363-494">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="7d363-494">Allowed From</span></span>

<span data-ttu-id="7d363-495">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="7d363-495">Threads</span></span>

### <a name="example"></a><span data-ttu-id="7d363-496">Örnek</span><span class="sxs-lookup"><span data-stu-id="7d363-496">Example</span></span>

```C
#define DTLS_SERVER_SESSION (3)

/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Allocate space for DTLS sessions in the DTLS server. */
UCHAR dtls_server_session_buffer[sizeof(NX_SECURE_DTLS_SESSION)
                                        * DTLS_SERVER_SESSIONS];

/* Flag used to indicate that a DTLS Client has connected. */
UINT connect_flag = 0;

/* Flag used to indicate application data reception. */
UINT receive_flag = 0;

/* Pointer to newly-connected DTLS session.
   NOTE: In practice this should be an array or list in case a new connection is
         attempted while a previous session is being started. */
NX_SECURE_DTLS_SESSION *new_dtls_session;

/* Pointer to session for application data receive.
   NOTE: Should be an array or list as
   with new_dtls_session */
NX_SECURE_DTLS_SESSION *receive_dtls_session;

/* Connect notify callback routine. */
UINT dtls_server_connect_notify(NX_SECURE_DTLS_SESSION *dtls_session,
                                    NXD_ADDRESS *ip_address, UINT port)
{
    /* NOTE: proper inter-thread communication procedures (e.g. mutex handling)
             Omitted for clarity. */

    /* Notify application thread that a connection request has been received. */
    connect_flag = 1;
    new_dtls_session = dtls_session;

    return(NX_SUCCESS);
}

/* Receive notify callback routine invoked when DTLS application data is received
   on an existing DTLS server session. */
UINT dtls_server_receive_notify(NX_SECURE_DTLS_SESSION *dtls_session)
{
    /* Receive and process DTLS record.
       NOTE: Mutex handling omitted for clarity. */
    receive_flag = 1;
    receive_dtls_session = dtls_session;

    return(NX_SUCCESS);
}

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
    NX_PACKET *send_packet;
    NX_PACKET *receive_packet;
    UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                    LOCAL_SERVER_PORT,
                                    NX_IP_PERIODIC_RATE,
                                    dtls_server_session_buffer,
                                    sizeof(dtls_server_session_buffer),
                                    &tls_crypto_table,
                                    crypto_metadata_buffer,
                                    sizeof(crypto_metadata_buffer),
                                    packet_buffer,
                                    sizeof(packet_buffer),
                                    dtls_server_connect_notify,
                                    dtls_server_receive_notify);

    /* Check for errors. */

    /* Initialize local server identity certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&certificate, device_cert_der,
                                            device_cert_der_len,
                                            NX_NULL, 0,
                                            device_cert_key_der,
                                            device_cert_key_der_len,
                                            NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_local_certificate_add(&dtls_server,
                                                        &certificate, 1);


    /* Start server. */
    status = nx_secure_dtls_server_start(&dtls_server);

    /* Loop continuously to handle incoming data. */
    while(1)
    {
        /* Check for new connections. Muxtex handling omitted for clarity. */
        if(connect_flag)
        {
            /* We have a new connection attempt, start the DTLS session. */
            status = nx_secure_dtls_server_session_start(new_dtls_session,
                                            NX_IP_PERIODIC_RATE);

            /* Check for errors. */
        }

        /* Check for received application data. */
        if(receive_flag)
        {
            /* We have received data over a previously-established DTLS session.
               Mutex handling omitted for clarity. */
            Status = nx_secure_dtls_session_receive(receive_dtls_session,
                                                    &receive_packet,
                                                    NX_IP_PERIODIC_RATE);

            /* Process received data… */

            /* Prepare and send response to client. */
            status = nx_secure_dtls_packet_allocate(receive_dtls_session,
                                                &packet_pool,
                                                &send_packet,
                                                NX_IP_PERIODIC_RATE);

            /* Check for errors and prepare response data
            (e.g. nx_packet_data_append). */

            /* Send response to client. */
            status = nx_secure_dtls_server_session_send(receive_dtls_session,
                send_packet);

        }

        /* If not processing connections or received data, let the thread sleep. */
        if(!connect_flag && !receive_flag)
        {
            tx_thread_sleep(100);
        }
    }

    /* We have exited the processing loop, stop the server. */
    status = nx_secure_dtls_server_stop(&dtls_server);

    /* If we exit the processing loop, clean up the server. */
    status = nx_secure_dtls_server_delete(&dtls_server);
}

```

### <a name="see-also"></a><span data-ttu-id="7d363-497">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="7d363-497">See Also</span></span>

- <span data-ttu-id="7d363-498">nx_secure_dtls_server_start, nx_secure_dtls_server_create,</span><span class="sxs-lookup"><span data-stu-id="7d363-498">nx_secure_dtls_server_start, nx_secure_dtls_server_create,</span></span>
- <span data-ttu-id="7d363-499">nx_secure_dtls_server_delete, nx_secure_dtls_session_receive,</span><span class="sxs-lookup"><span data-stu-id="7d363-499">nx_secure_dtls_server_delete, nx_secure_dtls_session_receive,</span></span>
- <span data-ttu-id="7d363-500">nx_secure_dtls_server_session_send,</span><span class="sxs-lookup"><span data-stu-id="7d363-500">nx_secure_dtls_server_session_send,</span></span>
- <span data-ttu-id="7d363-501">nx_secure_dtls_server_session_start</span><span class="sxs-lookup"><span data-stu-id="7d363-501">nx_secure_dtls_server_session_start</span></span>

## <a name="nx_secure_dtls_server_trusted_certificate_add"></a><span data-ttu-id="7d363-502">nx_secure_dtls_server_trusted_certificate_add</span><span class="sxs-lookup"><span data-stu-id="7d363-502">nx_secure_dtls_server_trusted_certificate_add</span></span>

<span data-ttu-id="7d363-503">NetX güvenli DTLS sunucusuna güvenilir bir CA sertifikası ekleme</span><span class="sxs-lookup"><span data-stu-id="7d363-503">Add a trusted CA certificate to a NetX Secure DTLS Server</span></span>

### <a name="prototype"></a><span data-ttu-id="7d363-504">Prototype</span><span class="sxs-lookup"><span data-stu-id="7d363-504">Prototype</span></span>

```C
UINT  nx_secure_dtls_server_trusted_certificate_add(
                                         NX_SECURE_DTLS_SERVER *server_ptr,
                                         NX_SECURE_X509_CERT *certificate,
                                         UINT cert_id);

```

### <a name="description"></a><span data-ttu-id="7d363-505">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7d363-505">Description</span></span>

<span data-ttu-id="7d363-506">Bu hizmet, bir DTLS sunucu örneğine güvenilir bir CA veya ara CA sertifikası ekler ve tüm iç DTLS sunucusu oturumlarına atanır.</span><span class="sxs-lookup"><span data-stu-id="7d363-506">This service adds a trusted CA or intermediate CA certificate to a DTLS Server instance and assigned to all the internal DTLS server sessions.</span></span> <span data-ttu-id="7d363-507">Bu yalnızca, *nx_secure_dtls_server_x509_client_verify_configure* kullanılarak X. 509.440 istemci sertifikası kimlik doğrulamasının etkinleştirilmesi durumunda gereklidir.</span><span class="sxs-lookup"><span data-stu-id="7d363-507">This is only necessary if X.509 Client certificate authentication is enabled using *nx_secure_dtls_server_x509_client_verify_configure*.</span></span> <span data-ttu-id="7d363-508">Eklenen sertifika, gelen Client X. 509.440 sertifikalarını doğrulamak için kullanılacaktır.</span><span class="sxs-lookup"><span data-stu-id="7d363-508">The added certificate will be used to verify incoming Client X.509 certificates.</span></span>

<span data-ttu-id="7d363-509">Cert_id parametresi, sertifika için sayısal, sıfır olmayan bir tanıtıcıdır.</span><span class="sxs-lookup"><span data-stu-id="7d363-509">The cert_id parameter is a numeric, non-zero identifier for the certificate.</span></span> <span data-ttu-id="7d363-510">Bu, DTLS sunucu deposunda aynı X. 509.440 ortak adına sahip birden çok kimlik sertifikası bulunan olayda kolayca kaldırılmasını veya bu durumda bulunabilmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="7d363-510">This enables the certificate to be easily removed or found in the event there are multiple identity certificates with the same X.509 Common Name present in the DTLS server store.</span></span> <span data-ttu-id="7d363-511">X. 509.440 sunucu sertifikaları hakkında daha fazla bilgi için NetX güvenli TLS Kullanıcı Kılavuzu 'na bakın.</span><span class="sxs-lookup"><span data-stu-id="7d363-511">See the NetX Secure TLS User Guide for more information about X.509 server certificates.</span></span>

### <a name="parameters"></a><span data-ttu-id="7d363-512">Parametreler</span><span class="sxs-lookup"><span data-stu-id="7d363-512">Parameters</span></span>

- <span data-ttu-id="7d363-513">**server_ptr** Daha önce oluşturulmuş bir DTLS sunucu örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="7d363-513">**server_ptr** Pointer to a previously created DTLS Server instance.</span></span>
- <span data-ttu-id="7d363-514">**sertifika** Daha önce başlatılmış bir X. 509.440 sertifika yapısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="7d363-514">**certificate** Pointer to a previously initialized X.509 certificate structure.</span></span>
- <span data-ttu-id="7d363-515">**cert_id** Bu DTLS sunucusunda bu sertifika için sıfır olmayan sayısal benzersiz tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="7d363-515">**cert_id** Numeric non-zero unique identifier for this certificate in this DTLS server.</span></span>

### <a name="return-values"></a><span data-ttu-id="7d363-516">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="7d363-516">Return Values</span></span>

- <span data-ttu-id="7d363-517">**NX_SUCCESS** (0x00) DTLS sunucusuna sertifikanın başarıyla eklenmesi.</span><span class="sxs-lookup"><span data-stu-id="7d363-517">**NX_SUCCESS** (0x00) Successful addition of certificate to DTLS server.</span></span>
- <span data-ttu-id="7d363-518">**NX_PTR_ERROR** (0x07) geçersiz işaretçi geçirildi.</span><span class="sxs-lookup"><span data-stu-id="7d363-518">**NX_PTR_ERROR** (0x07) Invalid pointer passed.</span></span>
- <span data-ttu-id="7d363-519">**NX_INVALID_PARAMETERS** (0x4D) BIR sertifika kimliği (0) geçirildi.</span><span class="sxs-lookup"><span data-stu-id="7d363-519">**NX_INVALID_PARAMETERS** (0x4D) A certificate ID of 0 was passed in.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="7d363-520">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="7d363-520">Allowed From</span></span>

<span data-ttu-id="7d363-521">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="7d363-521">Threads</span></span>

### <a name="example"></a><span data-ttu-id="7d363-522">Örnek</span><span class="sxs-lookup"><span data-stu-id="7d363-522">Example</span></span>

<span data-ttu-id="7d363-523">\* Daha kapsamlı bir örnek için bkz. *nx_secure_dtls_server_create* başvurusu.</span><span class="sxs-lookup"><span data-stu-id="7d363-523">\*See reference for *nx_secure_dtls_server_create* for a more complete example.</span></span>

```C
/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Certificate control block and data. */
NX_SECURE_X509_CERT trusted_ca_certificate;
UCHAR certificate_der_data[] = { … };

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                LOCAL_SERVER_PORT,
                                NX_IP_PERIODIC_RATE,
                                dtls_server_session_buffer,
                                sizeof(dtls_server_session_buffer),
                                &tls_crypto_table,
                                crypto_metadata_buffer,
                                sizeof(crypto_metadata_buffer),
                                packet_buffer,
                                sizeof(packet_buffer),
                                dtls_server_connect_notify,
                                dtls_server_receive_notify);

    /* Check for errors. */

    /* Initialize trusted certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&trusted_ca_certificate,
                                            certificate_der_data,
                                            sizeof(certificate_der_data),
                                            NX_NULL, 0, NX_NULL,
                                            0, NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add trusted CA certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_trusted_certificate_add(&dtls_server,
                                            &trusted_ca_certificate, 1);

    /* Start server. */
    status = nx_secure_dtls_server_start(&dtls_server);

    /* Loop continuously to handle incoming data. */
    while(1)
    {
        /* Process incoming requests and data. */
    }

}

```

### <a name="see-also"></a><span data-ttu-id="7d363-524">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="7d363-524">See Also</span></span>

- <span data-ttu-id="7d363-525">nx_secure_dtls_server_start, nx_secure_dtls_server_create,</span><span class="sxs-lookup"><span data-stu-id="7d363-525">nx_secure_dtls_server_start, nx_secure_dtls_server_create,</span></span>
- <span data-ttu-id="7d363-526">nx_secure_dtls_session_receive, nx_secure_dtls_server_session_send,</span><span class="sxs-lookup"><span data-stu-id="7d363-526">nx_secure_dtls_session_receive, nx_secure_dtls_server_session_send,</span></span>
- <span data-ttu-id="7d363-527">nx_secure_dtls_server_session_start,</span><span class="sxs-lookup"><span data-stu-id="7d363-527">nx_secure_dtls_server_session_start,</span></span>
- <span data-ttu-id="7d363-528">nx_secure_dtls_server_local_certificate_add,</span><span class="sxs-lookup"><span data-stu-id="7d363-528">nx_secure_dtls_server_local_certificate_add,</span></span>
- <span data-ttu-id="7d363-529">nx_secure_dtls_server_trusted_certificate_remove,</span><span class="sxs-lookup"><span data-stu-id="7d363-529">nx_secure_dtls_server_trusted_certificate_remove,</span></span>
- <span data-ttu-id="7d363-530">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="7d363-530">nx_secure_x509_certificate_initialize</span></span>

## <a name="nx_secure_dtls_server_trusted_certificate_remove"></a><span data-ttu-id="7d363-531">nx_secure_dtls_server_trusted_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="7d363-531">nx_secure_dtls_server_trusted_certificate_remove</span></span>

<span data-ttu-id="7d363-532">NetX güvenli DTLS sunucusundan güvenilir bir CA sertifikasını kaldırma</span><span class="sxs-lookup"><span data-stu-id="7d363-532">Remove a trusted CA certificate from a NetX Secure DTLS Server</span></span>

### <a name="prototype"></a><span data-ttu-id="7d363-533">Prototype</span><span class="sxs-lookup"><span data-stu-id="7d363-533">Prototype</span></span>

```C
UINT  nx_secure_dtls_server_trusted_certificate_remove(
                                NX_SECURE_DTLS_SERVER *server_ptr,
                                UCHAR *common_name,
                                UINT common_name_length,
                                UINT cert_id);

```

### <a name="description"></a><span data-ttu-id="7d363-534">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7d363-534">Description</span></span>

<span data-ttu-id="7d363-535">Bu hizmet, bir DTLS sunucu örneğinden güvenilir bir CA sertifikasını kaldırır.</span><span class="sxs-lookup"><span data-stu-id="7d363-535">This service removes a trusted CA certificate from a DTLS Server instance.</span></span> <span data-ttu-id="7d363-536">Güvenilen CA sertifikaları yalnızca, *nx_secure_dtls_server_x509_client_verify_configure* çağırarak X. 509.440 istemci sertifikası doğrulamasının etkinleştirildiği DTLS sunucusu için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="7d363-536">Trusted CA certificates are only necessary for a DTLS Server for which X.509 Client certificate verification has been enabled by calling *nx_secure_dtls_server_x509_client_verify_configure*.</span></span>

<span data-ttu-id="7d363-537">Kaldırılacak sertifika, X. 509.440 ortak adı ya da *nx_secure_dtls_server_trusted_certificate_add* çağrısında atanan sayısal cert_id tarafından belirlenebilir.</span><span class="sxs-lookup"><span data-stu-id="7d363-537">The certificate to be removed can be identified either by its X.509 Common Name or by the numeric cert_id that was assigned in the call to *nx_secure_dtls_server_trusted_certificate_add*.</span></span> <span data-ttu-id="7d363-538">Cert_id yalnızca sertifikayı tanımlamak için kullanılır ve uygulama tarafından korunur.</span><span class="sxs-lookup"><span data-stu-id="7d363-538">The cert_id is only used to identify the certificate and is maintained by the application.</span></span> <span data-ttu-id="7d363-539">Sayısal sertifika tanımlayıcısı yerine ortak ad kullanılırsa, cert_id parametresi 0 olarak ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7d363-539">If the Common Name is used instead of the numeric certificate identifier, the cert_id parameter should be set to 0.</span></span>

> [!NOTE]
> <span data-ttu-id="7d363-540">Bir DTLS el sıkışması işlenirken bir sertifikayı kaldırmak beklenmedik davranışa neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="7d363-540">Removing a certificate while a DTLS handshake is being processed may result in unexpected behavior.</span></span> <span data-ttu-id="7d363-541">Sertifikalar kaldırılmadan önce hizmet *nx_secure_dtls_server_stop* çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7d363-541">The service *nx_secure_dtls_server_stop* should be called before removing certificates.</span></span>

### <a name="parameters"></a><span data-ttu-id="7d363-542">Parametreler</span><span class="sxs-lookup"><span data-stu-id="7d363-542">Parameters</span></span>

- <span data-ttu-id="7d363-543">**server_ptr** Daha önce oluşturulmuş bir DTLS sunucu örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="7d363-543">**server_ptr** Pointer to a previously created DTLS Server instance.</span></span>
- <span data-ttu-id="7d363-544">**common_name** Kaldırılacak sertifikanın X. 509.440 CommonName.</span><span class="sxs-lookup"><span data-stu-id="7d363-544">**common_name** X.509 CommonName of the certificate to remove.</span></span> <span data-ttu-id="7d363-545">Bu kullanılırsa, cert_id sıfır olarak geçirin.</span><span class="sxs-lookup"><span data-stu-id="7d363-545">If this is used, pass cert_id as zero.</span></span>
- <span data-ttu-id="7d363-546">**common_name_length** Bayt cinsinden common_name dize uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="7d363-546">**common_name_length** Length of common_name string in bytes.</span></span>
- <span data-ttu-id="7d363-547">**cert_id** Bu DTLS sunucusunda bu sertifika için sıfır olmayan sayısal benzersiz tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="7d363-547">**cert_id** Numeric non-zero unique identifier for this certificate in this DTLS server.</span></span> <span data-ttu-id="7d363-548">Bu kullanılırsa, common_name parametresi için NX_NULL geçirin.</span><span class="sxs-lookup"><span data-stu-id="7d363-548">If this is used, pass NX_NULL for the common_name parameter.</span></span>


### <a name="return-values"></a><span data-ttu-id="7d363-549">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="7d363-549">Return Values</span></span>

- <span data-ttu-id="7d363-550">**NX_SUCCESS** (0x00) DTLS sunucusundan sertifikanın başarıyla kaldırılması.</span><span class="sxs-lookup"><span data-stu-id="7d363-550">**NX_SUCCESS** (0x00) Successful removal of certificate from DTLS server.</span></span>
- <span data-ttu-id="7d363-551">**NX_PTR_ERROR** (0x07) geçersiz işaretçi geçirildi.</span><span class="sxs-lookup"><span data-stu-id="7d363-551">**NX_PTR_ERROR** (0x07) Invalid pointer passed.</span></span>
- <span data-ttu-id="7d363-552">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) VERILEN DTLS sunucusunda cert_id veya common_name eşleşen bir sertifika bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="7d363-552">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) No certificate matching the cert_id or common_name was found in the given DTLS server.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="7d363-553">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="7d363-553">Allowed From</span></span>

<span data-ttu-id="7d363-554">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="7d363-554">Threads</span></span>

### <a name="example"></a><span data-ttu-id="7d363-555">Örnek</span><span class="sxs-lookup"><span data-stu-id="7d363-555">Example</span></span>

```C
/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Certificate control block and data. */
NX_SECURE_X509_CERT trusted_ca_certificate;
UCHAR certificate_der_data[] = { … };

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                    LOCAL_SERVER_PORT,
                                    NX_IP_PERIODIC_RATE,
                                    dtls_server_session_buffer,
                                    sizeof(dtls_server_session_buffer),
                                    &tls_crypto_table,
                                    crypto_metadata_buffer,
                                    sizeof(crypto_metadata_buffer),
                                    packet_buffer,
                                    sizeof(packet_buffer),
                                    dtls_server_connect_notify,
                                    dtls_server_receive_notify);

    /* Check for errors. */

    /* Initialize trusted certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&trusted_ca_certificate,
                                                    certificate_der_data,
                                                    sizeof(certificate_der_data),
                                                    NX_NULL, 0, NX_NULL, 0,
                                                    NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_trusted_certificate_add(&dtls_server,
                                                       &trusted_ca_certificate, 1);

    /* Start server. */
    status = nx_secure_dtls_server_start(&dtls_server);

    /* Process client requests, etc… */

    /* Stop the server before removing a certificate. */
    Status = nx_secure_dtls_server_stop(&dtls_server);


/* At some point in the future we decide to remove the certificate we added. We can
       use the certificate identifier we passed into the call to
       nx_secure_dtls_trusted_certificate_add (value = 1); */
    status = nx_secure_dtls_server_trusted_certificate_remove(&dtls_server,
                                                          NX_NULL, 0, 1);

}

```

### <a name="see-also"></a><span data-ttu-id="7d363-556">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="7d363-556">See Also</span></span>

- <span data-ttu-id="7d363-557">nx_secure_dtls_server_start, nx_secure_dtls_server_create,</span><span class="sxs-lookup"><span data-stu-id="7d363-557">nx_secure_dtls_server_start, nx_secure_dtls_server_create,</span></span>
- <span data-ttu-id="7d363-558">nx_secure_dtls_server_session_start,</span><span class="sxs-lookup"><span data-stu-id="7d363-558">nx_secure_dtls_server_session_start,</span></span>
- <span data-ttu-id="7d363-559">nx_secure_dtls_server_session_stop,</span><span class="sxs-lookup"><span data-stu-id="7d363-559">nx_secure_dtls_server_session_stop,</span></span>
- <span data-ttu-id="7d363-560">nx_secure_dtls_server_trusted_certificate_add,</span><span class="sxs-lookup"><span data-stu-id="7d363-560">nx_secure_dtls_server_trusted_certificate_add,</span></span>
- <span data-ttu-id="7d363-561">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="7d363-561">nx_secure_x509_certificate_initialize</span></span>

## <a name="nx_secure_dtls_server_x509_client_verify_configure"></a><span data-ttu-id="7d363-562">nx_secure_dtls_server_x509_client_verify_configure</span><span class="sxs-lookup"><span data-stu-id="7d363-562">nx_secure_dtls_server_x509_client_verify_configure</span></span>

<span data-ttu-id="7d363-563">İstemci sertifikaları istemek ve doğrulamak için bir NetX güvenli DTLS sunucusu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="7d363-563">Configure a NetX Secure DTLS Server to request and verify client certificates</span></span>

### <a name="prototype"></a><span data-ttu-id="7d363-564">Prototype</span><span class="sxs-lookup"><span data-stu-id="7d363-564">Prototype</span></span>

```C
UINT nx_secure_dtls_server_x509_client_verify_configure(
                           NX_SECURE_DTLS_SERVER *server_ptr,
                               UINT certs_per_session,
                               UCHAR *certs_buffer, ULONG buffer_size);

```

### <a name="description"></a><span data-ttu-id="7d363-565">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7d363-565">Description</span></span>

<span data-ttu-id="7d363-566">Bu hizmet DTLS Istemci sertifikalarını istemek ve doğrulamak üzere bir DTLS sunucusunu yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="7d363-566">This service configures a DTLS Server to request and verify DTLS Client certificates.</span></span> <span data-ttu-id="7d363-567">Bu isteğe bağlı özellik, istemci kimlik doğrulaması için diğer mekanizmaların yerine X. 509.440 sertifikaları istendiğinde kullanılır (örneğin, önceden paylaşılan bir anahtar).</span><span class="sxs-lookup"><span data-stu-id="7d363-567">This optional feature is used when X.509 certificates are desired for client authentication in place of other mechanisms (e.g. a Pre-Shared Key).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7d363-568">*Bu hizmeti kullanarak istemci sertifikalarını doğrulamak üzere bir DTLS sunucusu yapılandırıldığında, nx_secure_dtls_server_trusted_certificate_add kullanarak sunucuya en az bir güvenilir CA sertifikası eklenmelidir veya istemci sertifikalarını güvenilir depoya doğrulayamayacak olduğundan sunucu tüm gelen istemci bağlantılarını reddeder.*</span><span class="sxs-lookup"><span data-stu-id="7d363-568">*When a DTLS Server is configured to verify client certificates using this service, at least one trusted CA certificate must be added to the server using nx_secure_dtls_server_trusted_certificate_add or the server will reject all incoming client connections because it will be unable to verify client certificates against the trusted store.*</span></span>

<span data-ttu-id="7d363-569">Bu hizmet çağrıldıktan sonra DTLS sunucu örneği (başlatıldıktan sonra) DTLS el sıkışmasının bir parçası olarak istemci sertifikaları ister.</span><span class="sxs-lookup"><span data-stu-id="7d363-569">Upon calling this service, the DTLS Server instance will (once started) request client certificates as part of the DTLS handshake.</span></span> <span data-ttu-id="7d363-570">İstemcinin bir kimlik sertifikası (ve uygulanabilirse ilişkili sertifika zinciri) ile düzgün şekilde yapılandırıldığı varsayılarak, DTLS sunucusu, istemci sertifikası verilerini işlemek için belleğin ayrılmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="7d363-570">Assuming the client is properly configured with an identity certificate (and associated certificate chain when applicable), the DTLS Server requires memory to be allocated to process the client certificate data.</span></span> <span data-ttu-id="7d363-571">Bu bellek *certs_buffer* parametresi olarak geçirilir.</span><span class="sxs-lookup"><span data-stu-id="7d363-571">This memory is passed in as the *certs_buffer* parameter.</span></span>

<span data-ttu-id="7d363-572">Certs_buffer bir DTLS istemcisinden beklenen en büyük sertifika zincirini, her *zaman DTLS sunucusu oturumlarının sayısını* kapsayacak şekilde boyutlandırılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7d363-572">The certs_buffer must be sized to accommodate the largest expected certificate chain from a DTLS client, *times the number of DTLS server sessions*.</span></span> <span data-ttu-id="7d363-573">Arabellek, bir Istemci sertifika zincirindeki beklenen en fazla sertifika sayısını temsil eden *certs_per_session* parametresi kullanılarak kullanılabilir Oturumlar arasında bölünür.</span><span class="sxs-lookup"><span data-stu-id="7d363-573">The buffer is divided amongst the available sessions using the *certs_per_session* parameter which represents the maximum expected number of certificates in a Client certificate chain.</span></span> <span data-ttu-id="7d363-574">Arabellek Ayrıca, sertifika verilerini ayrıştırmak için kullanılan NX_SECURE_X509_CERT veri yapısına boşluk sağlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="7d363-574">The buffer also needs to provide space for the NX_SECURE_X509_CERT data structure which is used to parse the certificate data.</span></span>

<span data-ttu-id="7d363-575">Uygun arabellek boyutunu hesaplamak aşağıdaki formül ile yapılabilir:</span><span class="sxs-lookup"><span data-stu-id="7d363-575">Calculating the proper buffer size can be done with the following formula:</span></span>

```C
buffer_size = (# of DTLS sessions in server) *
                (certs_per_session) *
                (    maximum expected certificate size +
                      sizeof(NX_SECURE_X509_CERT)    )

```

- <span data-ttu-id="7d363-576">DTLS oturumlarının sayısı, nx_secure_dtls_server_create iletilen oturum arabelleğinin boyutuna göre belirlenir.</span><span class="sxs-lookup"><span data-stu-id="7d363-576">The number of DTLS sessions is determined by the size of the session buffer passed into nx_secure_dtls_server_create.</span></span>
- <span data-ttu-id="7d363-577">certs_per_session, herhangi bir istemci sertifika zincirindeki beklenen en fazla sertifika sayısına ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7d363-577">certs_per_session should be set to the maximum expected number of certificates in any client certificate chain.</span></span>
- <span data-ttu-id="7d363-578">En büyük beklenen sertifika boyutu uygulamaya, anahtar boyutlarına ve diğer faktörlere bağlıdır, ancak 2KB genellikle yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="7d363-578">The maximum expected certificate size is dependent on the application, key sizes, and other factors but 2KB is generally sufficient.</span></span>

### <a name="parameters"></a><span data-ttu-id="7d363-579">Parametreler</span><span class="sxs-lookup"><span data-stu-id="7d363-579">Parameters</span></span>

- <span data-ttu-id="7d363-580">**server_ptr** Daha önce oluşturulmuş bir DTLS sunucu örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="7d363-580">**server_ptr** Pointer to a previously created DTLS Server instance.</span></span>
- <span data-ttu-id="7d363-581">**certs_per_session** Her DTLS sunucu oturumuna ayrılacak sertifika sayısı.</span><span class="sxs-lookup"><span data-stu-id="7d363-581">**certs_per_session** Number of certificates to allocate to each DTLS server session.</span></span>
- <span data-ttu-id="7d363-582">**certs_buffer** Gelen sertifika verileri için arabellek alanı.</span><span class="sxs-lookup"><span data-stu-id="7d363-582">**certs_buffer** Buffer space for incoming certificate data.</span></span>
- <span data-ttu-id="7d363-583">**Buffer_size** Sertifika arabelleğinin boyutu.</span><span class="sxs-lookup"><span data-stu-id="7d363-583">**buffer_size** Size of the certificate buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="7d363-584">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="7d363-584">Return Values</span></span>

- <span data-ttu-id="7d363-585">**NX_SUCCESS** (0x00) X. 509.440 Istemci doğrulamasının başarılı yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="7d363-585">**NX_SUCCESS** (0x00) Successful configuration of X.509 Client verification.</span></span>
- <span data-ttu-id="7d363-586">**NX_PTR_ERROR** (0x07) geçersiz işaretçi geçirildi.</span><span class="sxs-lookup"><span data-stu-id="7d363-586">**NX_PTR_ERROR** (0x07) Invalid pointer passed.</span></span>
- <span data-ttu-id="7d363-587">**NX_INVALID_PARAMETERS** (0x4D) geçersiz sertifika deposu (DTLSserver örneği başlatılmadı mi?).</span><span class="sxs-lookup"><span data-stu-id="7d363-587">**NX_INVALID_PARAMETERS** (0x4D) Invalid certificate store (DTLSserver instance not initalized?).</span></span>

### <a name="allowed-from"></a><span data-ttu-id="7d363-588">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="7d363-588">Allowed From</span></span>

<span data-ttu-id="7d363-589">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="7d363-589">Threads</span></span>

### <a name="example"></a><span data-ttu-id="7d363-590">Örnek</span><span class="sxs-lookup"><span data-stu-id="7d363-590">Example</span></span>

```C
/* Configure number of sessions per server. */
#define DTLS_SERVER_SESSIONS 3

/* Define parameters for X.509 client verification. */
#define MAX_CERT_SIZE         (2000)       /* 2KB expected maximum certificate size. */
#define CERTS_PER_SESSION (3)            /* Assume maximum chain length of 3 certificates. */
#define CERT_BUFFER_SIZE     (DTLS_SERVER_SESSIONS * CERTS_PER_SESSION * \
 (MAX_CERT_SIZE + sizeof(NX_SECURE_X509_CERT))

/* Define our incoming certificate buffer. */
UCHAR client_certs_buffer[CERT_BUFFER_SIZE];

/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Certificate control block and data. */
NX_SECURE_X509_CERT trusted_ca_certificate;
UCHAR certificate_der_data[] = { … };

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                    LOCAL_SERVER_PORT,
                                    NX_IP_PERIODIC_RATE,
                                    dtls_server_session_buffer,
                                    sizeof(dtls_server_session_buffer),
                                    &tls_crypto_table,
                                    crypto_metadata_buffer,
                                    sizeof(crypto_metadata_buffer),
                                    packet_buffer,
                                    sizeof(packet_buffer),
                                    dtls_server_connect_notify,
                                    dtls_server_receive_notify);

    /* Check for errors. */

    /* Initialize trusted certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&trusted_ca_certificate,
                                    certificate_der_data,
                                    sizeof(certificate_der_data),
                                    NX_NULL, 0,
                                    NX_NULL, 0, NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_trusted_certificate_add(&dtls_server,
                                                &trusted_ca_certificate, 1);

    /* Configure client X.509 authentication and verification. */
    status = nx_secure_dtls_server_x509_client_verify_configure(&dtls_server,
        CERTS_PER_SESSION,
        client_certs_buffer,
        sizeof(client_certs_buffer));

    /* Start server. */
    status = nx_secure_dtls_server_start(&dtls_server);

    /* Process client requests, etc… */
}

```

### <a name="see-also"></a><span data-ttu-id="7d363-591">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="7d363-591">See Also</span></span>

- <span data-ttu-id="7d363-592">nx_secure_dtls_server_x509_client_verify_disable,</span><span class="sxs-lookup"><span data-stu-id="7d363-592">nx_secure_dtls_server_x509_client_verify_disable,</span></span>
- <span data-ttu-id="7d363-593">nx_secure_dtls_server_start, nx_secure_dtls_server_create,</span><span class="sxs-lookup"><span data-stu-id="7d363-593">nx_secure_dtls_server_start, nx_secure_dtls_server_create,</span></span>
- <span data-ttu-id="7d363-594">nx_secure_dtls_server_session_start,</span><span class="sxs-lookup"><span data-stu-id="7d363-594">nx_secure_dtls_server_session_start,</span></span>
- <span data-ttu-id="7d363-595">nx_secure_dtls_server_session_stop,</span><span class="sxs-lookup"><span data-stu-id="7d363-595">nx_secure_dtls_server_session_stop,</span></span>
- <span data-ttu-id="7d363-596">nx_secure_dtls_server_trusted_certificate_add,</span><span class="sxs-lookup"><span data-stu-id="7d363-596">nx_secure_dtls_server_trusted_certificate_add,</span></span>
- <span data-ttu-id="7d363-597">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="7d363-597">nx_secure_x509_certificate_initialize</span></span>

## <a name="nx_secure_dtls_server_x509_client_verify_disable"></a><span data-ttu-id="7d363-598">nx_secure_dtls_server_x509_client_verify_disable</span><span class="sxs-lookup"><span data-stu-id="7d363-598">nx_secure_dtls_server_x509_client_verify_disable</span></span>

<span data-ttu-id="7d363-599">NetX güvenli DTLS sunucusu için Client X. 509.952 sertifikası doğrulamasını devre dışı bırakır</span><span class="sxs-lookup"><span data-stu-id="7d363-599">Disables client X.509 certificate verification for a NetX Secure DTLS Server</span></span>

### <a name="prototype"></a><span data-ttu-id="7d363-600">Prototype</span><span class="sxs-lookup"><span data-stu-id="7d363-600">Prototype</span></span>

```C
UINT nx_secure_dtls_server_x509_client_verify_disable(
                           NX_SECURE_DTLS_SERVER *server_ptr);
```

### <a name="description"></a><span data-ttu-id="7d363-601">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7d363-601">Description</span></span>

<span data-ttu-id="7d363-602">Bu hizmet, bir DTLS sunucusunda X. 509.440 Istemci sertifikası doğrulamasını devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="7d363-602">This service disables X.509 Client certificate verification on a DTLS Server.</span></span> <span data-ttu-id="7d363-603">X. 509.440 Istemci sertifikası doğrulaması etkinleştirilmemişse hizmetin hiçbir etkisi yoktur.</span><span class="sxs-lookup"><span data-stu-id="7d363-603">The service has no effect if X.509 Client certificate verification is not enabled.</span></span>

> [!NOTE]
> <span data-ttu-id="7d363-604">Etkin bir DTLS sunucu örneğinde istemci kimlik doğrulamasının devre dışı bırakılması öngörülemeyen davranışlara neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="7d363-604">Disabling client authentication on an active DTLS Server instance may result in unpredictable behavior.</span></span> <span data-ttu-id="7d363-605">Sunucu durumunu değiştirmeden önce nx_secure_dtls_server_stop hizmeti çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7d363-605">The nx_secure_dtls_server_stop service should be called before changing server state.</span></span>

### <a name="parameters"></a><span data-ttu-id="7d363-606">Parametreler</span><span class="sxs-lookup"><span data-stu-id="7d363-606">Parameters</span></span>

- <span data-ttu-id="7d363-607">**server_ptr** Daha önce oluşturulmuş bir DTLS sunucu örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="7d363-607">**server_ptr** Pointer to a previously created DTLS Server instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="7d363-608">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="7d363-608">Return Values</span></span>

- <span data-ttu-id="7d363-609">X. 509.440 istemci kimlik doğrulamasının başarıyla devre dışı bırakılması **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="7d363-609">**NX_SUCCESS** (0x00) Successful disabling of X.509 client authentication.</span></span>
- <span data-ttu-id="7d363-610">**NX_PTR_ERROR** (0x07) geçersiz işaretçi geçirildi.</span><span class="sxs-lookup"><span data-stu-id="7d363-610">**NX_PTR_ERROR** (0x07) Invalid pointer passed.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="7d363-611">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="7d363-611">Allowed From</span></span>

<span data-ttu-id="7d363-612">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="7d363-612">Threads</span></span>

### <a name="example"></a><span data-ttu-id="7d363-613">Örnek</span><span class="sxs-lookup"><span data-stu-id="7d363-613">Example</span></span>

```C
/* Configure number of sessions per server. */
#define DTLS_SERVER_SESSIONS 3

/* Define parameters for X.509 client verification. */
#define MAX_CERT_SIZE         (2000)       /* 2KB expected maximum certificate size. */
#define CERTS_PER_SESSION (3)            /* Assume maximum chain length of 3 certificates. */
#define CERT_BUFFER_SIZE     (DTLS_SERVER_SESSIONS * CERTS_PER_SESSION * \
 (MAX_CERT_SIZE + sizeof(NX_SECURE_X509_CERT))

/* Define our incoming certificate buffer. */
UCHAR client_certs_buffer[CERT_BUFFER_SIZE];

/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Certificate control block and data. */
NX_SECURE_X509_CERT trusted_ca_certificate;
UCHAR certificate_der_data[] = { … };

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                    LOCAL_SERVER_PORT,
                                    NX_IP_PERIODIC_RATE,
                                    dtls_server_session_buffer,
                                    sizeof(dtls_server_session_buffer),
                                    &tls_crypto_table,
                                    crypto_metadata_buffer,
                                    sizeof(crypto_metadata_buffer),
                                    packet_buffer,
                                    sizeof(packet_buffer),
                                    dtls_server_connect_notify,
                                    dtls_server_receive_notify);

    /* Check for errors. */

    /* Initialize trusted certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&trusted_ca_certificate,
                                    certificate_der_data,
                        sizeof(certificate_der_data), NX_NULL, 0,
                        NX_NULL, 0, NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_trusted_certificate_add(&dtls_server,
                                            &trusted_ca_certificate, 1);

    /* Configure client X.509 authentication and verification. */
    status = nx_secure_dtls_server_x509_client_verify_configure(&dtls_server,
        CERTS_PER_SESSION,
        client_certs_buffer,
        sizeof(client_certs_buffer));

    /* Start server. */
    status = nx_secure_dtls_server_start(&dtls_server);

    /* Process client requests, etc… */

    /* Stop the server before changing state. */
    status = nx_secure_dtls_server_stop(&dtls_server);

    /* Disable X.509 authentication and verification. */
    status = nx_secure_dtls_server_x509_client_verify_disable(&dtls_server);

}

```

### <a name="see-also"></a><span data-ttu-id="7d363-614">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="7d363-614">See Also</span></span>

- <span data-ttu-id="7d363-615">nx_secure_dtls_server_x509_client_verify_configure,</span><span class="sxs-lookup"><span data-stu-id="7d363-615">nx_secure_dtls_server_x509_client_verify_configure,</span></span>
- <span data-ttu-id="7d363-616">nx_secure_dtls_server_start, nx_secure_dtls_server_create,</span><span class="sxs-lookup"><span data-stu-id="7d363-616">nx_secure_dtls_server_start, nx_secure_dtls_server_create,</span></span>
- <span data-ttu-id="7d363-617">nx_secure_dtls_server_session_start,</span><span class="sxs-lookup"><span data-stu-id="7d363-617">nx_secure_dtls_server_session_start,</span></span>
- <span data-ttu-id="7d363-618">nx_secure_dtls_server_session_stop,</span><span class="sxs-lookup"><span data-stu-id="7d363-618">nx_secure_dtls_server_session_stop,</span></span>
- <span data-ttu-id="7d363-619">nx_secure_dtls_server_trusted_certificate_add,</span><span class="sxs-lookup"><span data-stu-id="7d363-619">nx_secure_dtls_server_trusted_certificate_add,</span></span>
- <span data-ttu-id="7d363-620">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="7d363-620">nx_secure_x509_certificate_initialize</span></span>

## <a name="nx_secure_dtls_session_client_info_get"></a><span data-ttu-id="7d363-621">nx_secure_dtls_session_client_info_get</span><span class="sxs-lookup"><span data-stu-id="7d363-621">nx_secure_dtls_session_client_info_get</span></span>

<span data-ttu-id="7d363-622">Bir DTLS sunucu oturumundan uzak istemci bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="7d363-622">Get remote client information from a DTLS Server session</span></span>

### <a name="prototype"></a><span data-ttu-id="7d363-623">Prototype</span><span class="sxs-lookup"><span data-stu-id="7d363-623">Prototype</span></span>

```C
UINT  nx_secure_dtls_session_client_info_get(
                                    NX_SECURE_DTLS_SESSION *session_ptr,
                                    NXD_ADDRESS *client_ip_address,
                                    UINT *client_port, UINT *local_port);

```

### <a name="description"></a><span data-ttu-id="7d363-624">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7d363-624">Description</span></span>

<span data-ttu-id="7d363-625">Bu hizmet, belirli bir DTLS sunucusu oturumuna bağlı olan bir DTLS Istemcisiyle ilgili ağ bilgilerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="7d363-625">This service returns the network information about a DTLS Client that is connected to a particular DTLS Server session.</span></span> <span data-ttu-id="7d363-626">Döndürülen bilgiler, uzak istemcinin IP adresinden ve UDP bağlantı noktasından ve istemcinin bağlı olduğu yerel sunucu bağlantı noktasından oluşur.</span><span class="sxs-lookup"><span data-stu-id="7d363-626">The information returned consists of the remote client’s IP address and UDP port, as well as the local server port to which the client is connected.</span></span>

<span data-ttu-id="7d363-627">Genel olarak, DTLS oturum örneği, DTLS bildirim geri çağırma yordamlarından birini çağırmada elde edilen bir işlem olacaktır (örn. connect_notify veya receive_notify geri çağrılar nx_secure_dtls_server_create).</span><span class="sxs-lookup"><span data-stu-id="7d363-627">In general, the DTLS session instance will be the one obtained in the invocation of one of the DTLS notification callback routines (e.g. the connect_notify or receive_notify callbacks passed into nx_secure_dtls_server_create).</span></span>

### <a name="parameters"></a><span data-ttu-id="7d363-628">Parametreler</span><span class="sxs-lookup"><span data-stu-id="7d363-628">Parameters</span></span>

- <span data-ttu-id="7d363-629">**session_ptr** Etkin bir DTLS sunucu oturumu örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="7d363-629">**session_ptr** Pointer to an active DTLS server session instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="7d363-630">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="7d363-630">Return Values</span></span>

- <span data-ttu-id="7d363-631">**NX_SUCCESS** (0x00) sunucu başarıyla silindi.</span><span class="sxs-lookup"><span data-stu-id="7d363-631">**NX_SUCCESS** (0x00) Successful deletion of server.</span></span>
- <span data-ttu-id="7d363-632">**NX_PTR_ERROR** (0x07) geçersiz işaretçi geçirildi.</span><span class="sxs-lookup"><span data-stu-id="7d363-632">**NX_PTR_ERROR** (0x07) Invalid pointer passed.</span></span>
- <span data-ttu-id="7d363-633">**NX_INVALID_SOCKET** (0x13) ilişkili UDP yuvası geçerli değil (oturum başlatılmamış mi?).</span><span class="sxs-lookup"><span data-stu-id="7d363-633">**NX_INVALID_SOCKET** (0x13) The associated UDP socket is not valid (session not initialized?).</span></span>
- <span data-ttu-id="7d363-634">**NX_NOT_CONNECTED** (0x38) UDP yuvası bağlı değil – istemci bağlantısı bırakılmıştı veya henüz kurulmadı.</span><span class="sxs-lookup"><span data-stu-id="7d363-634">**NX_NOT_CONNECTED** (0x38) UDP socket is not connected – client connection dropped or not yet established.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="7d363-635">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="7d363-635">Allowed From</span></span>

<span data-ttu-id="7d363-636">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="7d363-636">Threads</span></span>

### <a name="example"></a><span data-ttu-id="7d363-637">Örnek</span><span class="sxs-lookup"><span data-stu-id="7d363-637">Example</span></span>

```C
#define DTLS_SERVER_SESSION (3)

/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Allocate space for DTLS sessions in the DTLS server. */
UCHAR dtls_server_session_buffer[sizeof(NX_SECURE_DTLS_SESSION)
                                        * DTLS_SERVER_SESSIONS];

/* Flag used to indicate that a DTLS Client has connected. */
UINT connect_flag = 0;

/* Flag used to indicate application data reception. */
UINT receive_flag = 0;

/* Pointer to newly-connected DTLS session.
   NOTE: In practice this should be an array
   or list in case a new connection is
   attempted while a previous session is being started. */
NX_SECURE_DTLS_SESSION *new_dtls_session;

/* Pointer to session for application data receive.
NOTE: Should be an array or list as
   with new_dtls_session */
NX_SECURE_DTLS_SESSION *receive_dtls_session;

/* Connect notify callback routine. */
UINT dtls_server_connect_notify(NX_SECURE_DTLS_SESSION *dtls_session, NXD_ADDRESS
                                                            *ip_address, UINT port)
{
    /* NOTE: proper inter-thread communication procedures (e.g. mutex handling)
             Omitted for clarity. */

    /* Notify application thread that a connection request has been received. */
    connect_flag = 1;
    new_dtls_session = dtls_session;

    return(NX_SUCCESS);
}

/* Receive notify callback routine invoked when DTLS application data is received
   on an existing DTLS server session. */
UINT dtls_server_receive_notify(NX_SECURE_DTLS_SESSION *dtls_session)
{
    NXD_ADDRESS client_ip;
    UINT client_port, server_port;

    /* Get DTLS client information which can be used in filtering or associating
       the DTLS session with application data (e.g. a session pointer table). */
    status = nx_secure_dtls_session_client_info_get(dtls_session, &client_ip,
   &client_port, &server_port);

    /* Receive and process DTLS record.
       NOTE: Mutex handling omitted for clarity. */
    receive_flag = 1;
    receive_dtls_session = dtls_session;

    return(NX_SUCCESS);
}

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
    NX_PACKET *send_packet;
    NX_PACKET *receive_packet;
    UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                            LOCAL_SERVER_PORT,
                                            NX_IP_PERIODIC_RATE,
                                            dtls_server_session_buffer,
                                            sizeof(dtls_server_session_buffer),
                                            &tls_crypto_table,
                                            crypto_metadata_buffer,
                                            sizeof(crypto_metadata_buffer),
                                            packet_buffer,
                                            sizeof(packet_buffer),
                                            dtls_server_connect_notify,
                                            dtls_server_receive_notify);

    /* Check for errors. */

    /* Initialize local server identity certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&certificate,
                                            device_cert_der,
                                            device_cert_der_len,
                                            NX_NULL, 0,
                                            device_cert_key_der,
                                            device_cert_key_der_len,
                                            NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_local_certificate_add(&dtls_server,
                                                        &certificate, 1);


    /* Start server. */
    status = nx_secure_dtls_server_start(&dtls_server);

    /* Loop continuously to handle incoming data. */
    while(1)
    {
        /* Check for new connections. Muxtex handling omitted for clarity. */
        if(connect_flag)
        {
            /* We have a new connection attempt, start the DTLS session. */
            status = nx_secure_dtls_server_session_start(new_dtls_session,
                                            NX_IP_PERIODIC_RATE);

            /* Check for errors. */
        }

        /* Check for received application data. */
        if(receive_flag)
        {
            /* We have received data over a previously-established DTLS session.
               Mutex handling omitted for clarity. */
            Status = nx_secure_dtls_session_receive(receive_dtls_session,
                                                    &receive_packet,
                                                    NX_IP_PERIODIC_RATE);

            /* Process received data… */

            /* Prepare and send response to client. */
            status = nx_secure_dtls_packet_allocate(receive_dtls_session,
                                                &packet_pool,
                                                &send_packet,
                                                NX_IP_PERIODIC_RATE);

            /* Check for errors and prepare response data
            (e.g. nx_packet_data_append). */

            /* Send response to client. */
            status = nx_secure_dtls_server_session_send(receive_dtls_session,
                send_packet);
        }

        /* If not processing connections or received data, let the thread sleep. */
        if(!connect_flag && !receive_flag)
        {
            tx_thread_sleep(100);
        }
    }

    /* If we exit the processing loop, clean up the server. */
    status = nx_secure_dtls_server_delete(&dtls_server);
}

```

### <a name="see-also"></a><span data-ttu-id="7d363-638">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="7d363-638">See Also</span></span>

- <span data-ttu-id="7d363-639">nx_secure_dtls_server_start, nx_secure_dtls_server_stop,</span><span class="sxs-lookup"><span data-stu-id="7d363-639">nx_secure_dtls_server_start, nx_secure_dtls_server_stop,</span></span>
- <span data-ttu-id="7d363-640">nx_secure_dtls_server_create, nx_secure_dtls_server_delete,</span><span class="sxs-lookup"><span data-stu-id="7d363-640">nx_secure_dtls_server_create, nx_secure_dtls_server_delete,</span></span>
- <span data-ttu-id="7d363-641">nx_secure_dtls_session_receive, nx_secure_dtls_server_session_send,</span><span class="sxs-lookup"><span data-stu-id="7d363-641">nx_secure_dtls_session_receive, nx_secure_dtls_server_session_send,</span></span>
- <span data-ttu-id="7d363-642">nx_secure_dtls_server_session_start</span><span class="sxs-lookup"><span data-stu-id="7d363-642">nx_secure_dtls_server_session_start</span></span>

## <a name="nx_secure_dtls_session_create"></a><span data-ttu-id="7d363-643">nx_secure_dtls_session_create</span><span class="sxs-lookup"><span data-stu-id="7d363-643">nx_secure_dtls_session_create</span></span>

<span data-ttu-id="7d363-644">NetX güvenli DTLS oturumu oluşturma ve yapılandırma</span><span class="sxs-lookup"><span data-stu-id="7d363-644">Create and configure a NetX Secure DTLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="7d363-645">Prototype</span><span class="sxs-lookup"><span data-stu-id="7d363-645">Prototype</span></span>

```C
UINT nx_secure_dtls_session_create(
                        NX_SECURE_DTLS_SESSION *dtls_session,
                        const NX_SECURE_TLS_CRYPTO *crypto_table,
                        VOID *metadata_buffer, ULONG metadata_size,
                        UCHAR *packet_reassembly_buffer,
                        UINT packet_reassembly_buffer_size,
                        UINT certs_number,
                        UCHAR *remote_certificate_buffer,
                        ULONG remote_certificate_buffer_size));

```

### <a name="description"></a><span data-ttu-id="7d363-646">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7d363-646">Description</span></span>

<span data-ttu-id="7d363-647">Bu hizmet bir DTLS oturumu oluşturur ve yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="7d363-647">This service creates and configures a DTLS session.</span></span> <span data-ttu-id="7d363-648">Genel olarak, DTLS sunucu oturumları DTLS sunucu mekanizması (bkz. *nx_secure_dtls_server_create*) ile yönetildiği için bu durum genellikle DTLS istemci oturumları oluşturmak için kullanılır, ancak bir uygulamanın tek bir tek başına DTLS sunucu oturumu örneği oluşturması gereken durumlarda bu hizmet, bu <sup>hizmetin kullanılabileceği durumlar</sup>olabilir.</span><span class="sxs-lookup"><span data-stu-id="7d363-648">Generally, this will be used to create DTLS Client sessions as DTLS Server sessions are managed with the DTLS Server mechanism (see *nx_secure_dtls_server_create*), but there may be instances where an application needs to create a single stand-alone DTLS Server session instance in which case this service may be used<sup>7</sup>.</span></span>

<span data-ttu-id="7d363-649">Parametreler, bir DTLS oturumunun örneğini oluşturmak için gereken bilgileri ve bellek ayırmayı yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="7d363-649">The parameters configure the information and memory allocation needed to instantiate a DTLS session.</span></span> <span data-ttu-id="7d363-650">Crypto_table parametresi, TLS/DTLS şifrelemesi ve kimlik doğrulaması için gerekli tüm şifreleme yordamlarını içeren bir TLS tablosudur.</span><span class="sxs-lookup"><span data-stu-id="7d363-650">The crypto_table parameter is a TLS table containing all of the cryptographic routines needed for TLS/DTLS encryption and authentication.</span></span> <span data-ttu-id="7d363-651">Metadata_buffer şifreleme kullanıcıları için kullanılır (NetX güvenli TLS kullanıcı kılavuzunda nx_secure_tls_metadata_size_calculate bakın) ve packet_reassembly_buffer, UDP datagramlarını şifre çözme için tamamen bir DTLS kaydına yeniden birleştirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7d363-651">The metadata_buffer is used for encryption caclulations (see nx_secure_tls_metadata_size_calculate in the NetX Secure TLS User Guide), and the packet_reassembly_buffer is used to reassemble UDP datagrams into a complete DTLS record for decryption.</span></span>

<span data-ttu-id="7d363-652">Certs_number ve remote_certificate_buffer, gelen DTLS sunucusu sertifika zincirini depolamak ve işlemek için alan gerektiren DTLS Istemcileri için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="7d363-652">The certs_number and remote_certificate_buffer are required for DTLS Clients which need space to store and process the incoming DTLS Server certificate chain.</span></span> <span data-ttu-id="7d363-653">Arabelleğin bağlanacağı her sunucu için, Sertifika zincirinin beklenen en büyük boyutuna uyum sağlaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d363-653">The buffer must be able to accommodate the maximum expected size of the certificate chain for any server to which it will connect.</span></span> <span data-ttu-id="7d363-654">Arabellek, beklenen sertifika sayısına (certs_number parametresi) bölünür ve ayrıca sertifika başına bir NX_SECURE_X509_CERT yapısını tutabilecek kadar büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7d363-654">The buffer is divided up by the number of expected certificates (certs_number parameter) and must also be large enough to hold one NX_SECURE_X509_CERT structure per certificate.</span></span> <span data-ttu-id="7d363-655">Arabellek boyutu aşağıdaki formül kullanılarak belirlenebilir:</span><span class="sxs-lookup"><span data-stu-id="7d363-655">The buffer size can be determined using the following formula:</span></span>

```C
remote_certificate_buffer_size = (certs_number) *
                 (maximum cert size + sizeof(NX_SECURE_X509_CERT))
```

- <span data-ttu-id="7d363-656">certs_number, sunucunun sertifika zincirindeki beklenen en fazla sertifika sayısıdır</span><span class="sxs-lookup"><span data-stu-id="7d363-656">certs_number is the expected maximum number of certificates in the server’s certificate chain</span></span>
- <span data-ttu-id="7d363-657">En büyük sertifika boyutu, kullanılan anahtarların boyutuna ve sertifikadaki bilgilere bağlıdır, ancak 2KB genellikle yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="7d363-657">Maximum certificate size is dependent on the size of keys being used and the information in the certificate, but 2KB is generally sufficient.</span></span>

<span data-ttu-id="7d363-658">**7** Bu yordam ile DTLS sunucu oturumları oluşturma önerilmez ve bazı sınırlamalar gelir.</span><span class="sxs-lookup"><span data-stu-id="7d363-658">**7** Creating DTLS Server sessions with this routine is not recommended and comes with some limitations.</span></span> <span data-ttu-id="7d363-659">Birincil sorun, oturumun ek istemci bağlantılarını düzgün bir şekilde işleyememesi gerekir. UDP bağlantısı olmadığından, önceki bir DTLS oturumu hala etkin olduğunda, sunucu oturumunun bir hata ile sonlanmasına neden olacak şekilde sunucunun UDP bağlantı noktasına yasal olarak veri gönderebileceği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="7d363-659">The primary issue is that the session will not handle additional client connections gracefully – since UDP is connectionless a second client can legally send data to the server’s UDP port when a previous DTLS session is still active which would cause the server session to end with an error.</span></span>

### <a name="parameters"></a><span data-ttu-id="7d363-660">Parametreler</span><span class="sxs-lookup"><span data-stu-id="7d363-660">Parameters</span></span>

- <span data-ttu-id="7d363-661">**dtls_session** Başlatılmamış DTLS oturum yapısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="7d363-661">**dtls_session** Pointer to an uninitialized DTLS Session structure.</span></span>
- <span data-ttu-id="7d363-662">**crypto_table** Tüm şifreleme işlemleri için kullanılan TLS/DTLS Şifreleme tablosu yapısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="7d363-662">**crypto_table** Pointer to a TLS/DTLS encryption table structure used for all cryptographic operations.</span></span>
- <span data-ttu-id="7d363-663">**crypto_metadata_buffer** Şifreleme işlemi hesaplamaları ve durum bilgileri için arabellek alanı.</span><span class="sxs-lookup"><span data-stu-id="7d363-663">**crypto_metadata_buffer** Buffer space for cryptographic operation calculations and state information.</span></span>
- <span data-ttu-id="7d363-664">**crypto_metadata_size** Meta veri arabelleğinin boyutu.</span><span class="sxs-lookup"><span data-stu-id="7d363-664">**crypto_metadata_size** Size of metadata buffer.</span></span>
- <span data-ttu-id="7d363-665">**packet_reassembly_buffer** DTLS tarafından, IP verilerini şifre çözme için DTLS kayıtlarına yeniden birleştirmek üzere kullanılan arabellek.</span><span class="sxs-lookup"><span data-stu-id="7d363-665">**packet_reassembly_buffer** Buffer used by DTLS to reassemble UDP data into DTLS records for decryption.</span></span>
- <span data-ttu-id="7d363-666">**packet_reassembly_buffer_size** Yeniden birleştirme arabelleğinin boyutu.</span><span class="sxs-lookup"><span data-stu-id="7d363-666">**packet_reassembly_buffer_size** Size of reassembly buffer.</span></span> <span data-ttu-id="7d363-667">Genellikle 16KB 'den büyük olmalıdır, ancak uygulamaya bağlı olarak daha küçük olabilir.</span><span class="sxs-lookup"><span data-stu-id="7d363-667">Generally should be greater than 16KB but may be smaller depending on application.</span></span>
- <span data-ttu-id="7d363-668">**certs_number** Uzak sunucunun sertifika zincirindeki en fazla beklenen sertifika sayısı.</span><span class="sxs-lookup"><span data-stu-id="7d363-668">**certs_number** Maximum expected number of certificates in the remote server’s certificate chain.</span></span>
- <span data-ttu-id="7d363-669">**remote_certificate_buffer** Gelen sertifika verileri için arabellek alanı.</span><span class="sxs-lookup"><span data-stu-id="7d363-669">**remote_certificate_buffer** Buffer space for incoming certificate data.</span></span>
- <span data-ttu-id="7d363-670">**remote_certificate_buffer_size** Sertifika arabelleğinin boyutu.</span><span class="sxs-lookup"><span data-stu-id="7d363-670">**remote_certificate_buffer_size** Size of the certificate buffer.</span></span>


### <a name="return-values"></a><span data-ttu-id="7d363-671">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="7d363-671">Return Values</span></span>

- <span data-ttu-id="7d363-672">**NX_SUCCESS** (0x00) başarılı oturum oluşturma.</span><span class="sxs-lookup"><span data-stu-id="7d363-672">**NX_SUCCESS** (0x00) Successful creation of session.</span></span>
- <span data-ttu-id="7d363-673">**NX_PTR_ERROR** (0x07) geçersiz oturum veya arabellek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="7d363-673">**NX_PTR_ERROR** (0x07) Invalid session or buffer pointer.</span></span>
- <span data-ttu-id="7d363-674">**NX_INVALID_PARAMETERS** (0x4D) paket yeniden birleştirme, sertifikalar veya şifreleme için yeterli arabellek alanı yok.</span><span class="sxs-lookup"><span data-stu-id="7d363-674">**NX_INVALID_PARAMETERS** (0x4D) Not enough buffer space for packet reassembly, certificates, or cryptography.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="7d363-675">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="7d363-675">Allowed From</span></span>

<span data-ttu-id="7d363-676">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="7d363-676">Threads</span></span>

### <a name="example"></a><span data-ttu-id="7d363-677">Örnek</span><span class="sxs-lookup"><span data-stu-id="7d363-677">Example</span></span>

```C
/* Sockets, sessions, certificates defined in global static space to preserve
   application stack. */
NX_SECURE_DTLS_SESSION client_dtls_session;

/* Trusted certificate structure and raw data. */
NX_SECURE_X509_CERT trusted_cert;
const UCHAR trusted_cert_der = { … };

/* Cryptography routines and crypto work buffers. */
extern const NX_SECURE_TLS_CRYPTO nx_crypto_tls_ciphers;
UCHAR crypto_metadata[9000];

/* Packet reassembly buffer for decryption. */
UCHAR packet_buffer[4000];

/* Remote certificate buffer for incoming certificates. */
#define REMOTE_CERT_SIZE (sizeof(NX_SECURE_X509_CERT) + 2000)
#define REMOTE_CERT_NUMBER  (3)
UCHAR remote_certs_buffer[REMOTE_CERT_SIZE * REMOTE_CERT_NUMBER];

/* Application thread where TLS session is started. */
void application_thread()
{
NXD_ADDRESS server_ip;

    /* Create a TLS session for our socket. Ciphers and metadata defined
    elsewhere. See nx_secure_tls_session_create reference for more
    information. */
        status =  nx_secure_dtls_session_create(&client_dtls_session,
                                            &nx_crypto_tls_ciphers,
                                            crypto_metadata,
                                            sizeof(crypto_metadata),
                                            packet_buffer,
                                            sizeof(packet_buffer),
                                            REMOTE_CERT_NUMBER,
                                            remote_certs_buffer,
                                            sizeof(remote_certs_buffer));

    /* Check for error.  */
    if(status)
    {
        printf("Error in function nx_secure_dtls_session_create: 0x%x\n", status);
    }

    /* Initialize our trusted certificate. See section “Importing X.509
    Certificates into NetX Secure” for more information. */
    nx_secure_x509_certificate_initialize(&trusted_certificate,
                                    trusted_cert_der,
                                    trusted_cert_der_len,
                                    NX_NULL, 0, NX_NULL, 0,
                                    NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add the certificate to the local store using a numeric ID. */
    nx_secure_dtls_session_trusted_certificate_add(&client_dtls_session,
    &certificate, 1);

    /* Set up IP address of remote host. */
    server_ip.nxd_ip_version = NX_IP_VERSION_V4;
    server_ip.nxd_ip_address.v4 = IP_ADDRESS(192, 168, 1, 150);


    /* Now we can start the DTLS session as normal. */
    status =  nx_secure_dtls_client_session_start(&client_dtls_session,
                                            &udp_socket, &server_ip,
                                            4443,
                                            NX_IP_PERIODIC_RATE);

    if(status != NX_SUCCESS)
    {
        /* Error! */
        return(status);
    }

    /* Add data to send packet as usual for NX_PACKET and send to server.  */
    status = nx_secure_dtls_session_send(&client_dtls_session,
                                                &send_packet,
                                                &server_ip, 4443);

    /* Receive response from server. */
    status = nx_secure_dtls_session_receive(&client_dtls_session,
                                            &receive_packet,
                                            NX_IP_PERIODIC_RATE);

    /* Process response. */

    /* Shut down DTLS session. */
        status = nx_secure_dtls_session_end(&client_dtls_session,
                                            NX_IP_PERIODIC_RATE);

    /* Clean up. */
        status = nx_secure_dtls_session_delete(&client_dtls_session);

}

```

### <a name="see-also"></a><span data-ttu-id="7d363-678">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="7d363-678">See Also</span></span>

- <span data-ttu-id="7d363-679">nx_secure_dtls_client_session_start, nx_secure_dtls_session_receive,</span><span class="sxs-lookup"><span data-stu-id="7d363-679">nx_secure_dtls_client_session_start,nx_secure_dtls_session_receive,</span></span>
- <span data-ttu-id="7d363-680">nx_secure_dtls_session_send</span><span class="sxs-lookup"><span data-stu-id="7d363-680">nx_secure_dtls_session_send</span></span>

## <a name="nx_secure_dtls_session_delete"></a><span data-ttu-id="7d363-681">nx_secure_dtls_session_delete</span><span class="sxs-lookup"><span data-stu-id="7d363-681">nx_secure_dtls_session_delete</span></span>

<span data-ttu-id="7d363-682">NetX güvenli DTLS oturumu tarafından kullanılan kaynakları boşaltma</span><span class="sxs-lookup"><span data-stu-id="7d363-682">Free up resources used by a NetX Secure DTLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="7d363-683">Prototype</span><span class="sxs-lookup"><span data-stu-id="7d363-683">Prototype</span></span>

```C
UINT nx_secure_dtls_session_delete(
                        NX_SECURE_DTLS_SESSION *dtls_session);

```

### <a name="description"></a><span data-ttu-id="7d363-684">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7d363-684">Description</span></span>

<span data-ttu-id="7d363-685">Bu hizmet, bir DTLS oturumunu siler ve oluşturulduğu zaman ayrılan kaynakları serbest bırakır.</span><span class="sxs-lookup"><span data-stu-id="7d363-685">This service deletes a DTLS session, freeing up any resources that were allocated when it was created.</span></span>

### <a name="parameters"></a><span data-ttu-id="7d363-686">Parametreler</span><span class="sxs-lookup"><span data-stu-id="7d363-686">Parameters</span></span>

- <span data-ttu-id="7d363-687">**dtls_session** Daha önce başlatılmış olan DTLS oturum yapısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="7d363-687">**dtls_session** Pointer to a DTLS Session structure that was initialized previously.</span></span>

### <a name="return-values"></a><span data-ttu-id="7d363-688">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="7d363-688">Return Values</span></span>

- <span data-ttu-id="7d363-689">**NX_SUCCESS** (0x00) oturumu başarıyla silindi.</span><span class="sxs-lookup"><span data-stu-id="7d363-689">**NX_SUCCESS** (0x00) Successful deletion of session.</span></span>
- <span data-ttu-id="7d363-690">**NX_PTR_ERROR** (0x07) geçersiz oturum veya arabellek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="7d363-690">**NX_PTR_ERROR** (0x07) Invalid session or buffer pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="7d363-691">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="7d363-691">Allowed From</span></span>

<span data-ttu-id="7d363-692">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="7d363-692">Threads</span></span>

### <a name="example"></a><span data-ttu-id="7d363-693">Örnek</span><span class="sxs-lookup"><span data-stu-id="7d363-693">Example</span></span>

```C
/* Sockets, sessions, certificates defined in global static space to preserve
   application stack. */
NX_SECURE_DTLS_SESSION client_dtls_session;

/* Trusted certificate structure and raw data. */
NX_SECURE_X509_CERT trusted_cert;
const UCHAR trusted_cert_der = { … };

/* Cryptography routines and crypto work buffers. */
extern const NX_SECURE_TLS_CRYPTO nx_crypto_tls_ciphers;
UCHAR crypto_metadata[9000];

/* Packet reassembly buffer for decryption. */
UCHAR packet_buffer[4000];

/* Remote certificate buffer for incoming certificates. */
#define REMOTE_CERT_SIZE (sizeof(NX_SECURE_X509_CERT) + 2000)
#define REMOTE_CERT_NUMBER  (3)
UCHAR remote_certs_buffer[REMOTE_CERT_SIZE * REMOTE_CERT_NUMBER];

/* Application thread where TLS session is started. */
void application_thread()
{
    NXD_ADDRESS server_ip;

    /* Create a TLS session for our socket. Ciphers and metadata defined
    elsewhere. See nx_secure_tls_session_create reference for more
    information. */
        status =  nx_secure_dtls_session_create(&client_dtls_session,
                                            &nx_crypto_tls_ciphers,
                                            crypto_metadata,
                                            sizeof(crypto_metadata),
                                            packet_buffer,
                                            sizeof(packet_buffer),
                                            REMOTE_CERT_NUMBER,
                                            remote_certs_buffer,
                                            sizeof(remote_certs_buffer));

    /* Check for error.  */
    if(status)
    {
        printf("Error in function nx_secure_dtls_session_create: 0x%x\n", status);
    }

    /* Initialize our trusted certificate. See section “Importing X.509
    Certificates into NetX Secure” for more information. */
        nx_secure_x509_certificate_initialize(&trusted_certificate,
                                        trusted_cert_der,
                                        trusted_cert_der_len,
                                        NX_NULL, 0, NX_NULL, 0,
                                        NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add the certificate to the local store using a numeric ID. */
    nx_secure_dtls_session_trusted_certificate_add(&client_dtls_session,
                                                        &certificate, 1);

    /* Set up IP address of remote host. */
    server_ip.nxd_ip_version = NX_IP_VERSION_V4;
    server_ip.nxd_ip_address.v4 = IP_ADDRESS(192, 168, 1, 150);


    /* Now we can start the DTLS session as normal. */
    status =  nx_secure_dtls_client_session_start(&client_dtls_session,
                                                    &udp_socket,
                                                    &server_ip, 4443,
                                                    NX_IP_PERIODIC_RATE);

    if(status != NX_SUCCESS)
    {
        /* Error! */
        return(status);
    }

    /* Add data to send packet as usual for NX_PACKET and send to server.  */
    status = nx_secure_dtls_session_send(&client_dtls_session, &send_packet,
                                                        &server_ip, 4443);

        /* Receive response from server. */
        status = nx_secure_dtls_session_receive(&client_dtls_session,
                                                &receive_packet,
                                                NX_IP_PERIODIC_RATE);

    /* Process response. */

    /* Shut down DTLS session. */
        status = nx_secure_dtls_session_end(&client_dtls_session,
                                            NX_IP_PERIODIC_RATE);

    /* Clean up. */
        status = nx_secure_dtls_session_delete(&client_dtls_session);

}

```

### <a name="see-also"></a><span data-ttu-id="7d363-694">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="7d363-694">See Also</span></span>

- <span data-ttu-id="7d363-695">nx_secure_dtls_client_session_start, nx_secure_dtls_session_receive,</span><span class="sxs-lookup"><span data-stu-id="7d363-695">nx_secure_dtls_client_session_start, nx_secure_dtls_session_receive,</span></span>
- <span data-ttu-id="7d363-696">nx_secure_dtls_session_send, nx_secure_dtls_session_delete</span><span class="sxs-lookup"><span data-stu-id="7d363-696">nx_secure_dtls_session_send, nx_secure_dtls_session_delete</span></span>

## <a name="nx_secure_dtls_session_end"></a><span data-ttu-id="7d363-697">nx_secure_dtls_session_end</span><span class="sxs-lookup"><span data-stu-id="7d363-697">nx_secure_dtls_session_end</span></span>

<span data-ttu-id="7d363-698">Etkin bir NetX güvenli DTLS oturumunu kapatma</span><span class="sxs-lookup"><span data-stu-id="7d363-698">Shut down an active NetX Secure DTLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="7d363-699">Prototype</span><span class="sxs-lookup"><span data-stu-id="7d363-699">Prototype</span></span>

```C
UINT nx_secure_dtls_session_end(NX_SECURE_DTLS_SESSION *dtls_session,
                                UINT wait_option);

```

### <a name="description"></a><span data-ttu-id="7d363-700">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7d363-700">Description</span></span>

<span data-ttu-id="7d363-701">Bu hizmet, uzak konağa bir TLS/DTLS CloseNotify uyarısı göndererek etkin bir DTLS oturumunu sonlandırır.</span><span class="sxs-lookup"><span data-stu-id="7d363-701">This service ends an active DTLS session by sending a TLS/DTLS CloseNotify alert to the remote host.</span></span> <span data-ttu-id="7d363-702">Kullanılan IP adresi ve bağlantı noktası, önceki nx_secure_dtls_session_send çağrısında kullanılan olanlardır.</span><span class="sxs-lookup"><span data-stu-id="7d363-702">The IP address and port used are those used in the previous call to nx_secure_dtls_session_send.</span></span>

### <a name="parameters"></a><span data-ttu-id="7d363-703">Parametreler</span><span class="sxs-lookup"><span data-stu-id="7d363-703">Parameters</span></span>

- <span data-ttu-id="7d363-704">**dtls_session** Daha önce başlatılmış olan DTLS oturum yapısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="7d363-704">**dtls_session** Pointer to a DTLS Session structure that was initialized previously.</span></span>
- <span data-ttu-id="7d363-705">**wait_option** Ağ işlemleri için kullanılacak ThreadX bekleme değeri.</span><span class="sxs-lookup"><span data-stu-id="7d363-705">**wait_option** ThreadX wait value to use for network operations.</span></span>

### <a name="return-values"></a><span data-ttu-id="7d363-706">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="7d363-706">Return Values</span></span>

- <span data-ttu-id="7d363-707">**NX_SUCCESS** (0x00) oturumu başarıyla silindi.</span><span class="sxs-lookup"><span data-stu-id="7d363-707">**NX_SUCCESS** (0x00) Successful deletion of session.</span></span>
- <span data-ttu-id="7d363-708">**NX_PTR_ERROR** (0x07) geçersiz oturum veya arabellek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="7d363-708">**NX_PTR_ERROR** (0x07) Invalid session or buffer pointer.</span></span>
- <span data-ttu-id="7d363-709">**NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0X111), CloseNotify uyarısı için paket (ler) ayıramadı.</span><span class="sxs-lookup"><span data-stu-id="7d363-709">**NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) Could not allocate packet(s) for CloseNotify alert.</span></span>
- <span data-ttu-id="7d363-710">**NX_SECURE_TLS_UNKNOWN_CIPHERSUITE** (0x105) büyük olasılıkla iç hata – şifreleme yordamı tanınmıyor.</span><span class="sxs-lookup"><span data-stu-id="7d363-710">**NX_SECURE_TLS_UNKNOWN_CIPHERSUITE** (0x105) Likely internal error – cryptographic routine not recognized.</span></span>
- <span data-ttu-id="7d363-711">Temel alınan UDP gönderimi **NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="7d363-711">**NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) Underlying UDP send failed.</span></span>
- <span data-ttu-id="7d363-712">**NX_IP_ADDRESS_ERROR** (0x21) uzak ana bilgisayar IP adresi hatası.</span><span class="sxs-lookup"><span data-stu-id="7d363-712">**NX_IP_ADDRESS_ERROR** (0x21) Error with remote host IP address.</span></span>
- <span data-ttu-id="7d363-713">**NX_NOT_BOUND** (0x24) temel alınan UDP yuvası, bağlantı noktasına bağlanmadı.</span><span class="sxs-lookup"><span data-stu-id="7d363-713">**NX_NOT_BOUND** (0x24) Underlying UDP socket not bound to port.</span></span>
- <span data-ttu-id="7d363-714">**NX_INVALID_PORT** (0x46) geçersiz UDP bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="7d363-714">**NX_INVALID_PORT** (0x46) Invalid UDP port.</span></span>
- <span data-ttu-id="7d363-715">**NX_PORT_UNAVAILABLE** (0x23) UDP bağlantı noktası kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="7d363-715">**NX_PORT_UNAVAILABLE** (0x23) UDP port not available for use.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="7d363-716">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="7d363-716">Allowed From</span></span>

<span data-ttu-id="7d363-717">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="7d363-717">Threads</span></span>

### <a name="example"></a><span data-ttu-id="7d363-718">Örnek</span><span class="sxs-lookup"><span data-stu-id="7d363-718">Example</span></span>

```C
/* Sockets, sessions, certificates defined in global static space to preserve
   application stack. */
NX_SECURE_DTLS_SESSION client_dtls_session;

/* Trusted certificate structure and raw data. */
NX_SECURE_X509_CERT trusted_cert;
const UCHAR trusted_cert_der = { … };

/* Cryptography routines and crypto work buffers. */
extern const NX_SECURE_TLS_CRYPTO nx_crypto_tls_ciphers;
UCHAR crypto_metadata[9000];

/* Packet reassembly buffer for decryption. */
UCHAR packet_buffer[4000];

/* Remote certificate buffer for incoming certificates. */
#define REMOTE_CERT_SIZE (sizeof(NX_SECURE_X509_CERT) + 2000)
#define REMOTE_CERT_NUMBER  (3)
UCHAR remote_certs_buffer[REMOTE_CERT_SIZE * REMOTE_CERT_NUMBER];

/* Application thread where TLS session is started. */
void application_thread()
{
    NXD_ADDRESS server_ip;

    /* Create a TLS session for our socket. Ciphers and metadata defined
    elsewhere. See nx_secure_tls_session_create reference for more
    information. */
    status =  nx_secure_dtls_session_create(&client_dtls_session,
                                        &nx_crypto_tls_ciphers,
                                        crypto_metadata,
                                        sizeof(crypto_metadata),
                                        packet_buffer,
                                        sizeof(packet_buffer),
                                        REMOTE_CERT_NUMBER,
                                        remote_certs_buffer,
                                        sizeof(remote_certs_buffer));

    /* Check for error.  */
    if(status)
    {
        printf("Error in function nx_secure_dtls_session_create: 0x%x\n", status);
    }

    /* Initialize our trusted certificate. See section “Importing X.509
            Certificates into NetX Secure” for more information. */
        nx_secure_x509_certificate_initialize(&trusted_certificate,
                                    trusted_cert_der,
                                    trusted_cert_der_len, NX_NULL,
                                    0, NX_NULL, 0,
                                    NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add the certificate to the local store using a numeric ID. */
    nx_secure_dtls_session_trusted_certificate_add(&client_dtls_session,
                                                        &certificate, 1);

    /* Set up IP address of remote host. */
    server_ip.nxd_ip_version = NX_IP_VERSION_V4;
    server_ip.nxd_ip_address.v4 = IP_ADDRESS(192, 168, 1, 150);


    /* Now we can start the DTLS session as normal. */
    status =  nx_secure_dtls_client_session_start(&client_dtls_session,
                                        &udp_socket, &server_ip, 4443,
                                        NX_IP_PERIODIC_RATE);

    if(status != NX_SUCCESS)
    {
        /* Error! */
        return(status);
    }

    /* Add data to send packet as usual for NX_PACKET and send to server.  */
    status = nx_secure_dtls_session_send(&client_dtls_session,
                                                &send_packet,
                                                &server_ip, 4443);

    /* Receive response from server. */
        status = nx_secure_dtls_session_receive(&client_dtls_session,
                                                    &receive_packet,
                                                    NX_IP_PERIODIC_RATE);

    /* Process response. */

    /* Shut down DTLS session. */
    status = nx_secure_dtls_session_end(&client_dtls_session,
                                        NX_IP_PERIODIC_RATE);

    /* Clean up. */
    status = nx_secure_dtls_session_delete(&client_dtls_session);

    }

```

### <a name="see-also"></a><span data-ttu-id="7d363-719">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="7d363-719">See Also</span></span>

- <span data-ttu-id="7d363-720">nx_secure_dtls_client_session_start, nx_secure_dtls_session_receive,</span><span class="sxs-lookup"><span data-stu-id="7d363-720">nx_secure_dtls_client_session_start, nx_secure_dtls_session_receive,</span></span>
- <span data-ttu-id="7d363-721">nx_secure_dtls_session_send, nx_secure_dtls_session_delete</span><span class="sxs-lookup"><span data-stu-id="7d363-721">nx_secure_dtls_session_send, nx_secure_dtls_session_delete</span></span>

## <a name="nx_secure_dtls_session_local_certificate_add"></a><span data-ttu-id="7d363-722">nx_secure_dtls_session_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="7d363-722">nx_secure_dtls_session_local_certificate_add</span></span>

<span data-ttu-id="7d363-723">NetX güvenli DTLS oturumuna yerel kimlik sertifikası ekleme</span><span class="sxs-lookup"><span data-stu-id="7d363-723">Add a local identity certificate to a NetX Secure DTLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="7d363-724">Prototype</span><span class="sxs-lookup"><span data-stu-id="7d363-724">Prototype</span></span>

```C
UINT  nx_secure_dtls_session_local_certificate_add(
                            NX_SECURE_DTLS_SESSION *session_ptr,
                            NX_SECURE_X509_CERT *certificate,
                            UINT cert_id);

```

### <a name="description"></a><span data-ttu-id="7d363-725">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7d363-725">Description</span></span>

<span data-ttu-id="7d363-726">Bu hizmet bir DTLS oturum örneğine yerel kimlik sertifikası ekler.</span><span class="sxs-lookup"><span data-stu-id="7d363-726">This service adds a local identity certificate to a DTLS Session instance.</span></span> <span data-ttu-id="7d363-727">Genel olarak, bu hizmet bir DTLS Istemci oturumunun bir uzak sunucu konağına kimlik sertifikası sağlaması gerektiğinde kullanılacaktır.</span><span class="sxs-lookup"><span data-stu-id="7d363-727">In general, this service will be used when a DTLS Client session needs to provide an identity certificate to a remote server host.</span></span> <span data-ttu-id="7d363-728">Bu, DTLS için isteğe bağlı bir yapılandırmadır. bu nedenle, DTLS Istemcileri için genellikle bir sertifika gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="7d363-728">This is an optional configuration for DTLS so a certificate is not generally required for DTLS Clients.</span></span> <span data-ttu-id="7d363-729">Kimlik sertifikası, ilişkili bir özel anahtar gerektirir.</span><span class="sxs-lookup"><span data-stu-id="7d363-729">An identity certificate requires an associated private key.</span></span>

<span data-ttu-id="7d363-730">Cert_id parametresi, sertifika için sayısal, sıfır olmayan bir tanıtıcıdır.</span><span class="sxs-lookup"><span data-stu-id="7d363-730">The cert_id parameter is a numeric, non-zero identifier for the certificate.</span></span> <span data-ttu-id="7d363-731">Bu, DTLS sertifika deposunda aynı X. 509.440 ortak adına sahip birden çok kimlik sertifikası bulunan olayda kolayca kaldırılmasını veya bu durumda bulunabilmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="7d363-731">This enables the certificate to be easily removed or found in the event there are multiple identity certificates with the same X.509 Common Name present in the DTLS certificate store.</span></span> <span data-ttu-id="7d363-732">X. 509.440 sertifikaları hakkında daha fazla bilgi için NetX güvenli TLS Kullanıcı Kılavuzu 'na bakın.</span><span class="sxs-lookup"><span data-stu-id="7d363-732">See the NetX Secure TLS User Guide for more information about X.509 certificates.</span></span>

### <a name="parameters"></a><span data-ttu-id="7d363-733">Parametreler</span><span class="sxs-lookup"><span data-stu-id="7d363-733">Parameters</span></span>

- <span data-ttu-id="7d363-734">**session_ptr** Daha önce oluşturulmuş bir DTLS oturum örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="7d363-734">**session_ptr** Pointer to a previously created DTLS Session instance.</span></span>
- <span data-ttu-id="7d363-735">**sertifika** Daha önce başlatılmış bir X. 509.440 sertifika yapısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="7d363-735">**certificate** Pointer to a previously initialized X.509 certificate structure.</span></span>
- <span data-ttu-id="7d363-736">**cert_id** Bu DTLS sunucusunda bu sertifika için sıfır olmayan sayısal benzersiz tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="7d363-736">**cert_id** Numeric non-zero unique identifier for this certificate in this DTLS server.</span></span>

### <a name="return-values"></a><span data-ttu-id="7d363-737">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="7d363-737">Return Values</span></span>

- <span data-ttu-id="7d363-738">**NX_SUCCESS** (0x00) DTLS oturumunun sertifikasının başarılı bir şekilde eklenmesi.</span><span class="sxs-lookup"><span data-stu-id="7d363-738">**NX_SUCCESS** (0x00) Successful addition of certificate to DTLS session.</span></span>
- <span data-ttu-id="7d363-739">**NX_PTR_ERROR** (0x07) geçersiz işaretçi geçirildi.</span><span class="sxs-lookup"><span data-stu-id="7d363-739">**NX_PTR_ERROR** (0x07) Invalid pointer passed.</span></span>
- <span data-ttu-id="7d363-740">**NX_INVALID_PARAMETERS** (0x4D) BIR sertifika kimliği (0) geçirildi.</span><span class="sxs-lookup"><span data-stu-id="7d363-740">**NX_INVALID_PARAMETERS** (0x4D) A certificate ID of 0 was passed in.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="7d363-741">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="7d363-741">Allowed From</span></span>

<span data-ttu-id="7d363-742">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="7d363-742">Threads</span></span>

### <a name="example"></a><span data-ttu-id="7d363-743">Örnek</span><span class="sxs-lookup"><span data-stu-id="7d363-743">Example</span></span>

<span data-ttu-id="7d363-744">\* Daha kapsamlı bir örnek için bkz. *nx_secure_dtls_session_create* başvurusu.</span><span class="sxs-lookup"><span data-stu-id="7d363-744">\*See reference for *nx_secure_dtls_session_create* for a more complete example.</span></span>

```C
/* Our DTLS Server instance. */
NX_SECURE_DTLS_SESSION dtls_client;

/* Certificate control block and data. Identity
certificates require a private key. */
NX_SECURE_X509_CERT certificate;
UCHAR certificate_der_data[] = { … };
UCHAR certificate_key_der_data[] = { … };


/* Application thread where TLS session is started. */
void application_thread()
{
NXD_ADDRESS server_ip;

/* Create a TLS session for our socket. Ciphers and metadata defined
   elsewhere. See nx_secure_tls_session_create reference for more
   information. */
    status =  nx_secure_dtls_session_create(&client_dtls_session,
                                        &nx_crypto_tls_ciphers,
                                        crypto_metadata,
                                        sizeof(crypto_metadata),
                                        packet_buffer,
                                        sizeof(packet_buffer),
                                        REMOTE_CERT_NUMBER,
                                        remote_certs_buffer,
                                        sizeof(remote_certs_buffer));

    /* Check for error.  */
    if(status)
{
    printf("Error in function nx_secure_dtls_session_create: 0x%x\n", status);
}

/* Initialize our trusted certificate. See section “Importing X.509
   Certificates into NetX Secure” for more information. */
    nx_secure_x509_certificate_initialize(&trusted_certificate,
                                    trusted_cert_der,
                                    trusted_cert_der_len,
                                    NX_NULL, 0, NX_NULL, 0,
                                    NX_SECURE_X509_KEY_TYPE_NONE);

/* Add the certificate to the local store using a numeric ID. */
    nx_secure_dtls_session_trusted_certificate_add(&client_dtls_session,
                                                              &certificate, 1);

    /* Initialize local server identity certificate with key and
    add to server. */
    status = nx_secure_x509_certificate_initialize(&certificate,
                        certificate_der_data,
                        sizeof(certificate_der_data),
                        NX_NULL, 0,
                        certificate_key_der_data,
                        sizeof(certificate_key_der_data),
                        NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_session_local_certificate_add(&dtls_client,
                                                    &certificate, 1);

/* Set up IP address of remote host. */
server_ip.nxd_ip_version = NX_IP_VERSION_V4;
server_ip.nxd_ip_address.v4 = IP_ADDRESS(192, 168, 1, 150);


/* Now we can start the DTLS session as normal. */
status =  nx_secure_dtls_client_session_start(&client_dtls_session,
                                    &udp_socket, &server_ip, 4443,
                                    NX_IP_PERIODIC_RATE);


    /* Process responses, etc…*/
}

```

### <a name="see-also"></a><span data-ttu-id="7d363-745">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="7d363-745">See Also</span></span>

- <span data-ttu-id="7d363-746">nx_secure_dtls_session_create, nx_secure_dtls_session_receive,</span><span class="sxs-lookup"><span data-stu-id="7d363-746">nx_secure_dtls_session_create, nx_secure_dtls_session_receive,</span></span>
- <span data-ttu-id="7d363-747">nx_secure_dtls_session_send, nx_secure_dtls_session_start,</span><span class="sxs-lookup"><span data-stu-id="7d363-747">nx_secure_dtls_session_send, nx_secure_dtls_session_start,</span></span>
- <span data-ttu-id="7d363-748">nx_secure_dtls_session_local_certificate_remove,</span><span class="sxs-lookup"><span data-stu-id="7d363-748">nx_secure_dtls_session_local_certificate_remove,</span></span>
- <span data-ttu-id="7d363-749">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="7d363-749">nx_secure_x509_certificate_initialize</span></span>

## <a name="nx_secure_dtls_session_local_certificate_remove"></a><span data-ttu-id="7d363-750">nx_secure_dtls_session_local_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="7d363-750">nx_secure_dtls_session_local_certificate_remove</span></span>

<span data-ttu-id="7d363-751">NetX güvenli DTLS oturumundan yerel kimlik sertifikasını kaldırma</span><span class="sxs-lookup"><span data-stu-id="7d363-751">Remove a local identity certificate from a NetX Secure DTLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="7d363-752">Prototype</span><span class="sxs-lookup"><span data-stu-id="7d363-752">Prototype</span></span>

```C
UINT  nx_secure_dtls_session_local_certificate_remove(
                                         NX_SECURE_DTLS_SESSION *session_ptr,
                                         UCHAR *common_name,
                                         UINT common_name_length, UINT cert_id);

```

### <a name="description"></a><span data-ttu-id="7d363-753">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7d363-753">Description</span></span>

<span data-ttu-id="7d363-754">Bu hizmet, bir sertifika KIMLIĞI numarası (sertifika nx_secure_dtls_session_local_certificate_add ile eklendiğinde atanır) veya X. 509.440 CommonName alanı kullanarak bir DTLS oturum örneğinden yerel kimlik sertifikasını kaldırır.</span><span class="sxs-lookup"><span data-stu-id="7d363-754">This service removes a local identity certificate from a DTLS Session instance using either a certificate ID number (assigned when the certificate was added with nx_secure_dtls_session_local_certificate_add) or the X.509 CommonName field.</span></span>

<span data-ttu-id="7d363-755">Common_name sertifikayla eşleştirmek için kullanılırsa, cert_id parametresi 0 olarak ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7d363-755">If the common_name is used to match the certificate, the cert_id parameter should be set to 0.</span></span> <span data-ttu-id="7d363-756">Cert_id kullanılırsa, common_name NX_NULL bir değer geçirmelidir.</span><span class="sxs-lookup"><span data-stu-id="7d363-756">If cert_id is used, common_name should be passed a value of NX_NULL.</span></span>

<span data-ttu-id="7d363-757">Cert_id parametresi, sertifika için sayısal, sıfır olmayan bir tanıtıcıdır.</span><span class="sxs-lookup"><span data-stu-id="7d363-757">The cert_id parameter is a numeric, non-zero identifier for the certificate.</span></span> <span data-ttu-id="7d363-758">Bu, DTLS sertifika deposunda aynı X. 509.440 ortak adına sahip birden çok kimlik sertifikası bulunan olayda kolayca kaldırılmasını veya bu durumda bulunabilmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="7d363-758">This enables the certificate to be easily removed or found in the event there are multiple identity certificates with the same X.509 Common Name present in the DTLS certificate store.</span></span> <span data-ttu-id="7d363-759">X. 509.440 sertifikaları hakkında daha fazla bilgi için NetX güvenli TLS Kullanıcı Kılavuzu 'na bakın.</span><span class="sxs-lookup"><span data-stu-id="7d363-759">See the NetX Secure TLS User Guide for more information about X.509 certificates.</span></span>

### <a name="parameters"></a><span data-ttu-id="7d363-760">Parametreler</span><span class="sxs-lookup"><span data-stu-id="7d363-760">Parameters</span></span>

- <span data-ttu-id="7d363-761">**session_ptr** Daha önce oluşturulmuş bir DTLS oturum örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="7d363-761">**session_ptr** Pointer to a previously created DTLS Session instance.</span></span>
- <span data-ttu-id="7d363-762">**common_name** Eşleştirilecek CommonName dizesinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="7d363-762">**common_name** Pointer to the CommonName string to match.</span></span>
- <span data-ttu-id="7d363-763">**common_name_length** Common_name dizesinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="7d363-763">**common_name_length** Length of the common_name string.</span></span>
- <span data-ttu-id="7d363-764">**cert_id** Bu DTLS sunucusunda bu sertifika için sıfır olmayan sayısal benzersiz tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="7d363-764">**cert_id** Numeric non-zero unique identifier for this certificate in this DTLS server.</span></span>

### <a name="return-values"></a><span data-ttu-id="7d363-765">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="7d363-765">Return Values</span></span>

- <span data-ttu-id="7d363-766">**NX_SUCCESS** (0x00) DTLS oturumundan sertifika başarıyla silindi.</span><span class="sxs-lookup"><span data-stu-id="7d363-766">**NX_SUCCESS** (0x00) Successful removal of certificate from DTLS session.</span></span>
- <span data-ttu-id="7d363-767">**NX_PTR_ERROR** (0x07) geçersiz işaretçi geçirildi.</span><span class="sxs-lookup"><span data-stu-id="7d363-767">**NX_PTR_ERROR** (0x07) Invalid pointer passed.</span></span>
- <span data-ttu-id="7d363-768">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) VERILEN DTLS oturumunda cert_id veya common_name eşleşen bir sertifika bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="7d363-768">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) No certificate matching the cert_id or common_name was found in the given DTLS session.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="7d363-769">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="7d363-769">Allowed From</span></span>

<span data-ttu-id="7d363-770">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="7d363-770">Threads</span></span>

### <a name="example"></a><span data-ttu-id="7d363-771">Örnek</span><span class="sxs-lookup"><span data-stu-id="7d363-771">Example</span></span>

<span data-ttu-id="7d363-772">\* Daha kapsamlı bir örnek için bkz. *nx_secure_dtls_session_create* başvurusu.</span><span class="sxs-lookup"><span data-stu-id="7d363-772">\*See reference for *nx_secure_dtls_session_create* for a more complete example.</span></span>

```C

/* Our DTLS Server instance. */
NX_SECURE_DTLS_SESSION dtls_client;

/* Certificate control block and data.
Identity certificates require a private key. */
NX_SECURE_X509_CERT certificate;
UCHAR certificate_der_data[] = { … };
UCHAR certificate_key_der_data[] = { … };


/* Application thread where TLS session is started. */
void application_thread()
{
    NXD_ADDRESS server_ip;

    /* Create a TLS session for our socket. Ciphers and metadata defined
    elsewhere. See nx_secure_tls_session_create reference for more
    information. */
        status =  nx_secure_dtls_session_create(&client_dtls_session,
                                            &nx_crypto_tls_ciphers,
                                            crypto_metadata,
                                            sizeof(crypto_metadata),
                                            packet_buffer,
                                            sizeof(packet_buffer),
                                            REMOTE_CERT_NUMBER,
                                            remote_certs_buffer,
                                            sizeof(remote_certs_buffer));

    /* Check for error.  */
    if(status)
    {
        printf("Error in function nx_secure_dtls_session_create: 0x%x\n", status);
    }

    /* Initialize our trusted certificate. See section “Importing X.509
    Certificates into NetX Secure” for more information. */
        nx_secure_x509_certificate_initialize(&trusted_certificate,
                                    trusted_cert_der,
                                    trusted_cert_der_len, NX_NULL,
                                    0, NX_NULL, 0,
                                    NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add the certificate to the local store using a numeric ID. */
        nx_secure_dtls_session_trusted_certificate_add(&client_dtls_session,
                                                            &certificate, 1);

        /* Initialize local server identity certificate with key
        and add to server. */
        status = nx_secure_x509_certificate_initialize(&certificate,
                                certificate_der_data,
                                sizeof(certificate_der_data),
                                NX_NULL, 0,
                                certificate_key_der_data,
                                sizeof(certificate_key_der_data),
                                NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

        /* Add local server identity certificate to DTLS server with ID of 1. */
        status = nx_secure_dtls_session_local_certificate_add(&dtls_client,
                                                            &certificate, 1);

    /* Set up IP address of remote host. */
    server_ip.nxd_ip_version = NX_IP_VERSION_V4;
    server_ip.nxd_ip_address.v4 = IP_ADDRESS(192, 168, 1, 150);


    /* Now we can start the DTLS session as normal. */
    status =  nx_secure_dtls_client_session_start(&client_dtls_session,
        &udp_socket, &server_ip, 4443,
        NX_IP_PERIODIC_RATE);

        /* Process responses, etc…*/

    /* At some point in the future,
    we decide to remove the certificate using the ID of 1
    when it was added to the session. */
        status = nx_secure_dtls_session_local_certificate_remove(&client_dtls_session,
                                                                NX_NULL, 0, 1);
}

```

### <a name="see-also"></a><span data-ttu-id="7d363-773">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="7d363-773">See Also</span></span>

- <span data-ttu-id="7d363-774">nx_secure_dtls_session_create, nx_secure_dtls_session_receive,</span><span class="sxs-lookup"><span data-stu-id="7d363-774">nx_secure_dtls_session_create, nx_secure_dtls_session_receive,</span></span>
- <span data-ttu-id="7d363-775">nx_secure_dtls_session_send, nx_secure_dtls_session_start,</span><span class="sxs-lookup"><span data-stu-id="7d363-775">nx_secure_dtls_session_send, nx_secure_dtls_session_start,</span></span>
- <span data-ttu-id="7d363-776">nx_secure_dtls_session_local_certificate_add,</span><span class="sxs-lookup"><span data-stu-id="7d363-776">nx_secure_dtls_session_local_certificate_add,</span></span>
- <span data-ttu-id="7d363-777">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="7d363-777">nx_secure_x509_certificate_initialize</span></span>

## <a name="nx_secure_dtls_session_receive"></a><span data-ttu-id="7d363-778">nx_secure_dtls_session_receive</span><span class="sxs-lookup"><span data-stu-id="7d363-778">nx_secure_dtls_session_receive</span></span>

<span data-ttu-id="7d363-779">Belirlenen bir NetX güvenli DTLS oturumu üzerinden uygulama verileri alma</span><span class="sxs-lookup"><span data-stu-id="7d363-779">Receive application data over an established NetX Secure DTLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="7d363-780">Prototype</span><span class="sxs-lookup"><span data-stu-id="7d363-780">Prototype</span></span>

```C
UINT nx_secure_dtls_session_receive(
                                NX_SECURE_DTLS_SESSION *dtls_session,
                                NX_PACKET **packet_ptr_ptr,
                                UINT wait_option);

```

### <a name="description"></a><span data-ttu-id="7d363-781">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7d363-781">Description</span></span>

<span data-ttu-id="7d363-782">Bu hizmet, etkin bir DTLS oturumu tarafından alınan uygulama verilerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="7d363-782">This service returns application data received by an active DTLS Session.</span></span> <span data-ttu-id="7d363-783">DTLS oturumu bir DTLS sunucu oturumu (bir DTLS sunucu örneğiyle yönetilen) ya da DTLS Istemci oturumu olabilir.</span><span class="sxs-lookup"><span data-stu-id="7d363-783">The DTLS Session may be either a DTLS Server session (managed by a DTLS Server instance) or a DTLS Client session.</span></span> <span data-ttu-id="7d363-784">Döndürülen paket, NX_PACKET API hizmetlerinden herhangi biri kullanılarak işlenebilir (daha fazla bilgi için bkz. NetX belgeleri).</span><span class="sxs-lookup"><span data-stu-id="7d363-784">The returned packet may be processed using any of the NX_PACKET API services (see the NetX documentation for more information).</span></span>

### <a name="parameters"></a><span data-ttu-id="7d363-785">Parametreler</span><span class="sxs-lookup"><span data-stu-id="7d363-785">Parameters</span></span>

- <span data-ttu-id="7d363-786">**dtls_session** Daha önce başlatılmış olan DTLS oturum yapısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="7d363-786">**dtls_session** Pointer to a DTLS Session structure that was initialized previously.</span></span>
- <span data-ttu-id="7d363-787">**packet_ptr_ptr** Dönüş paketi için NX_PACKET işaretçisine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="7d363-787">**packet_ptr_ptr** Pointer to an NX_PACKET pointer for the return packet.</span></span>
- <span data-ttu-id="7d363-788">**wait_option** Ağ işlemleri için kullanılacak ThreadX bekleme değeri.</span><span class="sxs-lookup"><span data-stu-id="7d363-788">**wait_option** ThreadX wait value to use for network operations.</span></span>

### <a name="return-values"></a><span data-ttu-id="7d363-789">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="7d363-789">Return Values</span></span>

- <span data-ttu-id="7d363-790">**NX_SUCCESS** (0x00) uygulama veri paketinin başarılı bir şekilde alındı.</span><span class="sxs-lookup"><span data-stu-id="7d363-790">**NX_SUCCESS** (0x00) Successful receipt of application data packet.</span></span>
- <span data-ttu-id="7d363-791">**NX_PTR_ERROR** (0x07) geçersiz oturum veya paket işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="7d363-791">**NX_PTR_ERROR** (0x07) Invalid session or packet pointer.</span></span>
- <span data-ttu-id="7d363-792">**NX_NOT_ENABLED** (0x14) UDP etkin değil.</span><span class="sxs-lookup"><span data-stu-id="7d363-792">**NX_NOT_ENABLED** (0x14) UDP is not enabled.</span></span>
- <span data-ttu-id="7d363-793">**NX_NOT_BOUND** (0x24) UDP yuvası bağlantı noktasına bağlanmadı.</span><span class="sxs-lookup"><span data-stu-id="7d363-793">**NX_NOT_BOUND** (0x24) UDP socket not bound to port.</span></span>
- <span data-ttu-id="7d363-794">**NX_SECURE_TLS_INVALID_PACKET** (0x104) geçerli bir DTLS kaydı olmayan veri alındı.</span><span class="sxs-lookup"><span data-stu-id="7d363-794">**NX_SECURE_TLS_INVALID_PACKET** (0x104) Recevied data that was not a valid DTLS record.</span></span>
- <span data-ttu-id="7d363-795">**NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0x108) DTLS kaydı düzgün bir şekilde karıştırılıp (şifreleme hatası) başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="7d363-795">**NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0x108) A DTLS record failed to be properly hashed (encryption error).</span></span>
- <span data-ttu-id="7d363-796">**NX_SECURE_TLS_PADDING_CHECK_FAILED** (0x12a) şifreleme doldurma denetimi hatası.</span><span class="sxs-lookup"><span data-stu-id="7d363-796">**NX_SECURE_TLS_PADDING_CHECK_FAILED** (0x12A) Encryption padding check failure.</span></span>
- <span data-ttu-id="7d363-797">**NX_SECURE_TLS_ALERT_RECEIVED** (0x114) uzak ana bilgisayardan bir uyarı alındı.</span><span class="sxs-lookup"><span data-stu-id="7d363-797">**NX_SECURE_TLS_ALERT_RECEIVED** (0x114) Recevied an alert from the remote host.</span></span>
- <span data-ttu-id="7d363-798">**NX_SECURE_TLS_UNRECOGNIZED_MESSAGE_TYPE**    (0x102) tanınmayan bir ileti aldı.</span><span class="sxs-lookup"><span data-stu-id="7d363-798">**NX_SECURE_TLS_UNRECOGNIZED_MESSAGE_TYPE**    (0x102) Received an unrecognized message.</span></span>
- <span data-ttu-id="7d363-799">**NX_SECURE_TLS_INCORRECT_MESSAGE_LENGTH** (0x10a), geçersiz uzunluğa sahıp bır DTLS kaydı alındı.</span><span class="sxs-lookup"><span data-stu-id="7d363-799">**NX_SECURE_TLS_INCORRECT_MESSAGE_LENGTH** (0x10A) Recevied a DTLS record with an invalid length.</span></span>
- <span data-ttu-id="7d363-800">**NX_SECURE_TLS_UNKNOWN_CIPHERSUITE** (0x105) bilinmeyen bir ciphersuite ile karşılaşıldı (iç şifreleme hatasını gösterir).</span><span class="sxs-lookup"><span data-stu-id="7d363-800">**NX_SECURE_TLS_UNKNOWN_CIPHERSUITE** (0x105) An unknown ciphersuite was encountered (indicates internal cryptography error).</span></span>
- <span data-ttu-id="7d363-801">**NX_SECURE_TLS_PROTOCOL_VERSION_CHANGED** (0x12e) eşleşmeyen DTLS sürümüne sahıp bır DTLS kaydı alındı.</span><span class="sxs-lookup"><span data-stu-id="7d363-801">**NX_SECURE_TLS_PROTOCOL_VERSION_CHANGED** (0x12E) Recevied a DTLS record with a mismatched DTLS version.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="7d363-802">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="7d363-802">Allowed From</span></span>

<span data-ttu-id="7d363-803">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="7d363-803">Threads</span></span>

### <a name="example"></a><span data-ttu-id="7d363-804">Örnek</span><span class="sxs-lookup"><span data-stu-id="7d363-804">Example</span></span>

```C
/* Sockets, sessions, certificates defined in global static space to preserve
   application stack. */
NX_SECURE_DTLS_SESSION client_dtls_session;

/* Trusted certificate structure and raw data. */
NX_SECURE_X509_CERT trusted_cert;
const UCHAR trusted_cert_der = { … };

/* Cryptography routines and crypto work buffers. */
extern const NX_SECURE_TLS_CRYPTO nx_crypto_tls_ciphers;
UCHAR crypto_metadata[9000];

/* Packet reassembly buffer for decryption. */
UCHAR packet_buffer[4000];

/* Remote certificate buffer for incoming certificates. */
#define REMOTE_CERT_SIZE (sizeof(NX_SECURE_X509_CERT) + 2000)
#define REMOTE_CERT_NUMBER  (3)
UCHAR remote_certs_buffer[REMOTE_CERT_SIZE * REMOTE_CERT_NUMBER];

/* Application thread where TLS session is started. */
void application_thread()
{
    NXD_ADDRESS server_ip;

    /* Create a TLS session for our socket. Ciphers and metadata defined
    elsewhere. See nx_secure_tls_session_create reference for more
    information. */
    status =  nx_secure_dtls_session_create(&client_dtls_session,
                                        &nx_crypto_tls_ciphers,
                                        crypto_metadata,
                                        sizeof(crypto_metadata),
                                        packet_buffer,
                                        sizeof(packet_buffer),
                                        REMOTE_CERT_NUMBER,
                                        remote_certs_buffer,
                                        sizeof(remote_certs_buffer));

    /* Check for error.  */
    if(status)
    {
    printf("Error in function nx_secure_dtls_session_create: 0x%x\n", status);
    }

    /* Initialize our trusted certificate. See section “Importing X.509
            Certificates into NetX Secure” for more information. */
        nx_secure_x509_certificate_initialize(&trusted_certificate,
                                    trusted_cert_der,
                                    trusted_cert_der_len, NX_NULL,
                                    0, NX_NULL, 0,
                                    NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add the certificate to the local store using a numeric ID. */
    nx_secure_dtls_session_trusted_certificate_add(&client_dtls_session,
                                                        &certificate, 1);

    /* Set up IP address of remote host. */
    server_ip.nxd_ip_version = NX_IP_VERSION_V4;
    server_ip.nxd_ip_address.v4 = IP_ADDRESS(192, 168, 1, 150);


    /* Now we can start the DTLS session as normal. */
    status =  nx_secure_dtls_client_session_start(&client_dtls_session,
                                        &udp_socket, &server_ip, 4443,
                                        NX_IP_PERIODIC_RATE);

    if(status != NX_SUCCESS)
    {
        /* Error! */
        return(status);
    }

    /* Add data to send packet as usual for NX_PACKET and send to server.  */
    status = nx_secure_dtls_session_send(&client_dtls_session, &send_packet,
                                                        &server_ip, 4443);

    /* Receive response from server. */
    status = nx_secure_dtls_session_receive(&client_dtls_session, &receive_packet,
                                                            NX_IP_PERIODIC_RATE);

    /* Process response. */

    /* Shut down DTLS session. */
    status = nx_secure_dtls_session_end(&client_dtls_session, NX_IP_PERIODIC_RATE);

    /* Clean up. */
    status = nx_secure_dtls_session_delete(&client_dtls_session);

}

```

### <a name="see-also"></a><span data-ttu-id="7d363-805">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="7d363-805">See Also</span></span>

- <span data-ttu-id="7d363-806">nx_secure_dtls_client_session_start, nx_secure_dtls_session_end,</span><span class="sxs-lookup"><span data-stu-id="7d363-806">nx_secure_dtls_client_session_start, nx_secure_dtls_session_end,</span></span>
- <span data-ttu-id="7d363-807">nx_secure_dtls_session_send, nx_secure_dtls_session_delete</span><span class="sxs-lookup"><span data-stu-id="7d363-807">nx_secure_dtls_session_send, nx_secure_dtls_session_delete</span></span>

## <a name="nx_secure_dtls_session_reset"></a><span data-ttu-id="7d363-808">nx_secure_dtls_session_reset</span><span class="sxs-lookup"><span data-stu-id="7d363-808">nx_secure_dtls_session_reset</span></span>

<span data-ttu-id="7d363-809">NetX güvenli DTLS oturum örneğindeki verileri temizleme</span><span class="sxs-lookup"><span data-stu-id="7d363-809">Clear data in an NetX Secure DTLS Session instance</span></span>

### <a name="prototype"></a><span data-ttu-id="7d363-810">Prototype</span><span class="sxs-lookup"><span data-stu-id="7d363-810">Prototype</span></span>

```C
UINT nx_secure_dtls_session_reset(NX_SECURE_DTLS_SESSION *dtls_session);
```

### <a name="description"></a><span data-ttu-id="7d363-811">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7d363-811">Description</span></span>

<span data-ttu-id="7d363-812">Bu hizmet, bir DTLS oturumunu sıfırlar, tüm kısa ömürlü şifreleme verilerini temizleyerek yapının yeni bir oturum için yeniden kullanılmasına izin verir.</span><span class="sxs-lookup"><span data-stu-id="7d363-812">This service resets a DTLS session, clearing all ephemeral cryptographic data and allowing the structure to be re-used for a new session.</span></span> <span data-ttu-id="7d363-813">Kalıcı veriler (örn. sertifika depoları) korunur, böylece nx_secure_dtls_session_create tekrar tekrar çağrılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="7d363-813">Persistent data (e.g. certificate stores) are maintained so that nx_secure_dtls_session_create need not be called repeatedly.</span></span>

### <a name="parameters"></a><span data-ttu-id="7d363-814">Parametreler</span><span class="sxs-lookup"><span data-stu-id="7d363-814">Parameters</span></span>

- <span data-ttu-id="7d363-815">**dtls_session** Daha önce başlatılmış olan DTLS oturum yapısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="7d363-815">**dtls_session** Pointer to a DTLS Session structure that was initialized previously.</span></span>

### <a name="return-values"></a><span data-ttu-id="7d363-816">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="7d363-816">Return Values</span></span>

- <span data-ttu-id="7d363-817">**NX_SUCCESS** (0x00) başarılı oturum sıfırlama.</span><span class="sxs-lookup"><span data-stu-id="7d363-817">**NX_SUCCESS** (0x00) Successful reset of session.</span></span>
- <span data-ttu-id="7d363-818">**NX_PTR_ERROR** (0x07) geçersiz oturum veya arabellek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="7d363-818">**NX_PTR_ERROR** (0x07) Invalid session or buffer pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="7d363-819">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="7d363-819">Allowed From</span></span>

<span data-ttu-id="7d363-820">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="7d363-820">Threads</span></span>

### <a name="example"></a><span data-ttu-id="7d363-821">Örnek</span><span class="sxs-lookup"><span data-stu-id="7d363-821">Example</span></span>

```C
/* Sockets, sessions, certificates defined in global static space to preserve
   application stack. */
NX_SECURE_DTLS_SESSION client_dtls_session;

/* Trusted certificate structure and raw data. */
NX_SECURE_X509_CERT trusted_cert;
const UCHAR trusted_cert_der = { … };

/* Cryptography routines and crypto work buffers. */
extern const NX_SECURE_TLS_CRYPTO nx_crypto_tls_ciphers;
UCHAR crypto_metadata[9000];

/* Packet reassembly buffer for decryption. */
UCHAR packet_buffer[4000];

/* Remote certificate buffer for incoming certificates. */
#define REMOTE_CERT_SIZE (sizeof(NX_SECURE_X509_CERT) + 2000)
#define REMOTE_CERT_NUMBER  (3)
UCHAR remote_certs_buffer[REMOTE_CERT_SIZE * REMOTE_CERT_NUMBER];

/* Application thread where TLS session is started. */
void application_thread()
{
    NXD_ADDRESS server_ip;

    /* Create a TLS session for our socket. Ciphers and metadata defined
    elsewhere. See nx_secure_tls_session_create reference for more
    information. */
    status =  nx_secure_dtls_session_create(&client_dtls_session,
                                        &nx_crypto_tls_ciphers,
                                        crypto_metadata,
                                        sizeof(crypto_metadata),
                                        packet_buffer,
                                        sizeof(packet_buffer),
                                        REMOTE_CERT_NUMBER,
                                        remote_certs_buffer,
                                        sizeof(remote_certs_buffer));

    /* Check for error.  */
    if(status)
    {
    printf("Error in function nx_secure_dtls_session_create: 0x%x\n", status);
    }

    /* Initialize our trusted certificate. See section “Importing X.509
            Certificates into NetX Secure” for more information. */
        nx_secure_x509_certificate_initialize(&trusted_certificate,
                                    trusted_cert_der,
                                    trusted_cert_der_len, NX_NULL,
                                    0, NX_NULL, 0,
                                    NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add the certificate to the local store using a numeric ID. */
    nx_secure_dtls_session_trusted_certificate_add(&client_dtls_session,
                                                        &certificate, 1);

    /* Set up IP address of remote host. */
    server_ip.nxd_ip_version = NX_IP_VERSION_V4;
    server_ip.nxd_ip_address.v4 = IP_ADDRESS(192, 168, 1, 150);


    /* Now we can start the DTLS session as normal. */
    status =  nx_secure_dtls_client_session_start(&client_dtls_session,
                                        &udp_socket, &server_ip, 4443,
                                        NX_IP_PERIODIC_RATE);

    if(status != NX_SUCCESS)
    {
        /* Error! */
        return(status);
    }

    /* Add data to send packet as usual for NX_PACKET and send to server.  */
    status = nx_secure_dtls_session_send(&client_dtls_session, &send_packet,
                                                        &server_ip, 4443);

    /* Receive response from server. */
        status = nx_secure_dtls_session_receive(&client_dtls_session,
                                                    &receive_packet,
                                                    NX_IP_PERIODIC_RATE);

    /* Process response. */

    /* Shut down DTLS session. */
    status = nx_secure_dtls_session_reset(&client_dtls_session);

    /* A new session can now be started using the same structure. */
    status =  nx_secure_dtls_client_session_start(&client_dtls_session,



    /* Clean up. */
    status = nx_secure_dtls_session_delete(&client_dtls_session);

}

```

### <a name="see-also"></a><span data-ttu-id="7d363-822">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="7d363-822">See Also</span></span>

- <span data-ttu-id="7d363-823">nx_secure_dtls_client_session_start, nx_secure_dtls_session_receive,</span><span class="sxs-lookup"><span data-stu-id="7d363-823">nx_secure_dtls_client_session_start, nx_secure_dtls_session_receive,</span></span>
- <span data-ttu-id="7d363-824">nx_secure_dtls_session_send, nx_secure_dtls_session_delete</span><span class="sxs-lookup"><span data-stu-id="7d363-824">nx_secure_dtls_session_send, nx_secure_dtls_session_delete</span></span>

## <a name="nx_secure_dtls_-session_send"></a><span data-ttu-id="7d363-825">nx_secure_dtls_ session_send</span><span class="sxs-lookup"><span data-stu-id="7d363-825">nx_secure_dtls_ session_send</span></span>

<span data-ttu-id="7d363-826">Bir DTLS oturumu üzerinden veri gönderme</span><span class="sxs-lookup"><span data-stu-id="7d363-826">Send data over a DTLS session</span></span>

### <a name="prototype"></a><span data-ttu-id="7d363-827">Prototype</span><span class="sxs-lookup"><span data-stu-id="7d363-827">Prototype</span></span>

```C
UINT  nx_secure_dtls_session_send(NX_SECURE_DTLS_SESSION *session_ptr,
                                          NX_PACKET *packet_ptr,
                                          NXD_ADDRESS *ip_address, UINT port);

```

### <a name="description"></a><span data-ttu-id="7d363-828">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7d363-828">Description</span></span>

<span data-ttu-id="7d363-829">Bu hizmet, belirlenen bir DTLS oturumu üzerinden, belirtilen IP adresi ve bağlantı noktasındaki uzak DTLS ana bilgisayarına bir veri paketi gönderir.</span><span class="sxs-lookup"><span data-stu-id="7d363-829">This service sends a packet of data over an established DTLS Session to a remote DTLS host at the given IP address and port.</span></span> <span data-ttu-id="7d363-830">Kullanılan oturum, etkin bir DTLS Istemci oturumundur.</span><span class="sxs-lookup"><span data-stu-id="7d363-830">The session used is an active DTLS Client session.</span></span> <span data-ttu-id="7d363-831">IP adresi ve bağlantı noktasının durum bilgisiz doğası nedeniyle sağlandığını, ancak genellikle nx_secure_dtls_session_start oturumu başlatmak için kullanılan adresle ve bağlantı noktasıyla eşleşmesi gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="7d363-831">Note that the IP address and port are provided due to the stateless nature of UDP but should generally match the address and port used to start the session in nx_secure_dtls_session_start.</span></span>

<span data-ttu-id="7d363-832">Pakette belirtilen veriler, *nx_secure_dtls_packet_allocate* kullanılarak ayrılması gereken DTLS oturum şifreleme parametreleri ve yordamları kullanılarak şifrelenir ve ardından DTLS oturumunun UDP yuvası üzerinden uzak konağa gönderilir.</span><span class="sxs-lookup"><span data-stu-id="7d363-832">The data provided in the packet, which must be allocated using *nx_secure_dtls_packet_allocate*, is encrypted using the DTLS session cryptographic parameters and routines and then sent to the remote host over the DTLS Session’s UDP socket.</span></span>

### <a name="parameters"></a><span data-ttu-id="7d363-833">Parametreler</span><span class="sxs-lookup"><span data-stu-id="7d363-833">Parameters</span></span>

- <span data-ttu-id="7d363-834">**session_ptr** Etkin bir DTLS istemci oturumu örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="7d363-834">**session_ptr** Pointer to an active DTLS client session instance.</span></span>
- <span data-ttu-id="7d363-835">**packet_ptr** Daha önce ayrılan ve uygulama verileriyle doldurulmuş bir NX_PACKET örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="7d363-835">**packet_ptr** Pointer to an NX_PACKET instance allocated previously and populated with application data.</span></span>
- <span data-ttu-id="7d363-836">**ip_address** Uzak konağın IP adresini içeren NXD_ADDRESS yapısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="7d363-836">**ip_address** Pointer to an NXD_ADDRESS structure containing the IP address of the remote host.</span></span>
- <span data-ttu-id="7d363-837">**bağlantı noktası** Uzak konaktaki UDP bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="7d363-837">**port** UDP port on the remote host.</span></span>

### <a name="return-values"></a><span data-ttu-id="7d363-838">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="7d363-838">Return Values</span></span>

- <span data-ttu-id="7d363-839">**NX_SUCCESS** (0x00) paketin başarıyla gönderilmesi.</span><span class="sxs-lookup"><span data-stu-id="7d363-839">**NX_SUCCESS** (0x00) Successful send of packet.</span></span>
- <span data-ttu-id="7d363-840">**NX_PTR_ERROR** (0x07) geçersiz işaretçi geçirildi.</span><span class="sxs-lookup"><span data-stu-id="7d363-840">**NX_PTR_ERROR** (0x07) Invalid pointer passed.</span></span>
- <span data-ttu-id="7d363-841">**NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) temel alınan UDP gönderme işleminde bir hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="7d363-841">**NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) An error occurred in the underlying UDP send operation.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="7d363-842">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="7d363-842">Allowed From</span></span>

<span data-ttu-id="7d363-843">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="7d363-843">Threads</span></span>

### <a name="example"></a><span data-ttu-id="7d363-844">Örnek</span><span class="sxs-lookup"><span data-stu-id="7d363-844">Example</span></span>

```C
/* Sockets, sessions, certificates defined in global static space to preserve
   application stack. */
NX_SECURE_DTLS_SESSION client_dtls_session;

/* Trusted certificate structure and raw data. */
NX_SECURE_X509_CERT trusted_cert;
const UCHAR trusted_cert_der = { … };

/* Cryptography routines and crypto work buffers. */
extern const NX_SECURE_TLS_CRYPTO nx_crypto_tls_ciphers;
UCHAR crypto_metadata[9000];

/* Packet reassembly buffer for decryption. */
UCHAR packet_buffer[4000];

/* Remote certificate buffer for incoming certificates. */
#define REMOTE_CERT_SIZE (sizeof(NX_SECURE_X509_CERT) + 2000)
#define REMOTE_CERT_NUMBER  (3)
UCHAR remote_certs_buffer[REMOTE_CERT_SIZE * REMOTE_CERT_NUMBER];

/* Application thread where TLS session is started. */
void application_thread()
{
    NXD_ADDRESS server_ip;

    /* Create a TLS session for our socket. Ciphers and metadata defined
    elsewhere. See nx_secure_tls_session_create reference for more
    information. */
        status =  nx_secure_dtls_session_create(&client_dtls_session,
                                            &nx_crypto_tls_ciphers,
                                            crypto_metadata,
                                            sizeof(crypto_metadata),
                                            packet_buffer,
                                            sizeof(packet_buffer),
                                            REMOTE_CERT_NUMBER,
                                            remote_certs_buffer,
                                            sizeof(remote_certs_buffer));

    /* Check for error.  */
    if(status)
    {
        printf("Error in function nx_secure_dtls_session_create: 0x%x\n", status);
    }

    /* Initialize our trusted certificate. See section “Importing X.509
    Certificates into NetX Secure” for more information. */
        nx_secure_x509_certificate_initialize(&trusted_certificate,
                                    trusted_cert_der,
                                    trusted_cert_der_len, NX_NULL,
                                    0, NX_NULL, 0,
                                    NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add the certificate to the local store using a numeric ID. */
    nx_secure_dtls_session_trusted_certificate_add(&client_dtls_session,
                                                        &certificate, 1);

    /* Set up IP address of remote host. */
    server_ip.nxd_ip_version = NX_IP_VERSION_V4;
    server_ip.nxd_ip_address.v4 = IP_ADDRESS(192, 168, 1, 150);


    /* Now we can start the DTLS session as normal. */
    status =  nx_secure_dtls_client_session_start(&client_dtls_session,
                                        &udp_socket, &server_ip, 4443,
                                        NX_IP_PERIODIC_RATE);

    if(status != NX_SUCCESS)
    {
    /* Error! */
    return(status);
    }

    /* Add data to send packet as usual for NX_PACKET and send to server.  */
    status = nx_secure_dtls_session_send(&client_dtls_session, &send_packet,
                                                        &server_ip, 4443);

        /* Receive response from server. */
        status = nx_secure_dtls_session_receive(&client_dtls_session,
                                                    &receive_packet,
                                                    NX_IP_PERIODIC_RATE);

    /* Process response. */

    /* Shut down DTLS session. */
        status = nx_secure_dtls_session_end(&client_dtls_session,
                                            NX_IP_PERIODIC_RATE);

    /* Clean up. */
        status = nx_secure_dtls_session_delete(&client_dtls_session);

}

```

### <a name="see-also"></a><span data-ttu-id="7d363-845">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="7d363-845">See Also</span></span>

- <span data-ttu-id="7d363-846">nx_secure_dtls_client_session_start, nx_secure_dtls_session_receive,</span><span class="sxs-lookup"><span data-stu-id="7d363-846">nx_secure_dtls_client_session_start, nx_secure_dtls_session_receive,</span></span>
- <span data-ttu-id="7d363-847">nx_secure_dtls_session_create</span><span class="sxs-lookup"><span data-stu-id="7d363-847">nx_secure_dtls_session_create</span></span>

## <a name="nx_secure_dtls_session_trusted_certificate_add"></a><span data-ttu-id="7d363-848">nx_secure_dtls_session_trusted_certificate_add</span><span class="sxs-lookup"><span data-stu-id="7d363-848">nx_secure_dtls_session_trusted_certificate_add</span></span>

<span data-ttu-id="7d363-849">NetX güvenli DTLS oturumuna güvenilir bir CA sertifikası ekleme</span><span class="sxs-lookup"><span data-stu-id="7d363-849">Add a trusted CA certificate to a NetX Secure DTLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="7d363-850">Prototype</span><span class="sxs-lookup"><span data-stu-id="7d363-850">Prototype</span></span>

```C
UINT  nx_secure_dtls_session_trusted_certificate_add(
                                         NX_SECURE_DTLS_SESSION *session_ptr,
                                         NX_SECURE_X509_CERT *certificate,
                                         UINT cert_id);

```

### <a name="description"></a><span data-ttu-id="7d363-851">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7d363-851">Description</span></span>

<span data-ttu-id="7d363-852">Bu hizmet, bir DTLS oturum örneğine güvenilir bir CA veya ara CA X. 509.440 sertifikası ekler.</span><span class="sxs-lookup"><span data-stu-id="7d363-852">This service adds a trusted CA or intermediate CA X.509 certificate to a DTLS Session instance.</span></span> <span data-ttu-id="7d363-853">Alternatif bir kimlik doğrulama mekanizması kullanılmamışsa (ör. önceden paylaşılan anahtarlar), uzak sunucu sertifikalarını doğrulamak için bir DTLS Istemcisi en az bir güvenilen sertifika gerektirir.</span><span class="sxs-lookup"><span data-stu-id="7d363-853">A DTLS Client requires at least one trusted certificate in order to validate remote server certificates unless an alternative authentication mechanism is used (e.g. Pre-Shared Keys).</span></span> <span data-ttu-id="7d363-854">Güvenilen bir sertifika genellikle özel bir anahtara sahip değildir.</span><span class="sxs-lookup"><span data-stu-id="7d363-854">A trusted certificate does not usually have a private key.</span></span>

<span data-ttu-id="7d363-855">Cert_id parametresi, sertifika için sayısal, sıfır olmayan bir tanıtıcıdır.</span><span class="sxs-lookup"><span data-stu-id="7d363-855">The cert_id parameter is a numeric, non-zero identifier for the certificate.</span></span> <span data-ttu-id="7d363-856">Bu, DTLS sertifika deposunda aynı X. 509.440 ortak adına sahip birden çok kimlik sertifikası bulunan olayda kolayca kaldırılmasını veya bu durumda bulunabilmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="7d363-856">This enables the certificate to be easily removed or found in the event there are multiple identity certificates with the same X.509 Common Name present in the DTLS certificate store.</span></span> <span data-ttu-id="7d363-857">X. 509.440 sertifikaları hakkında daha fazla bilgi için NetX güvenli TLS Kullanıcı Kılavuzu 'na bakın.</span><span class="sxs-lookup"><span data-stu-id="7d363-857">See the NetX Secure TLS User Guide for more information about X.509 certificates.</span></span>

### <a name="parameters"></a><span data-ttu-id="7d363-858">Parametreler</span><span class="sxs-lookup"><span data-stu-id="7d363-858">Parameters</span></span>

- <span data-ttu-id="7d363-859">**session_ptr** Daha önce oluşturulmuş bir DTLS oturum örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="7d363-859">**session_ptr** Pointer to a previously created DTLS Session instance.</span></span>
- <span data-ttu-id="7d363-860">**sertifika** Daha önce başlatılmış bir X. 509.440 sertifika yapısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="7d363-860">**certificate** Pointer to a previously initialized X.509 certificate structure.</span></span>
- <span data-ttu-id="7d363-861">**cert_id** Bu DTLS sunucusunda bu sertifika için sıfır olmayan sayısal benzersiz tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="7d363-861">**cert_id** Numeric non-zero unique identifier for this certificate in this DTLS server.</span></span>

### <a name="return-values"></a><span data-ttu-id="7d363-862">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="7d363-862">Return Values</span></span>

- <span data-ttu-id="7d363-863">**NX_SUCCESS** (0x00) DTLS oturumunun sertifikasının başarılı bir şekilde eklenmesi.</span><span class="sxs-lookup"><span data-stu-id="7d363-863">**NX_SUCCESS** (0x00) Successful addition of certificate to DTLS session.</span></span>
- <span data-ttu-id="7d363-864">**NX_PTR_ERROR** (0x07) geçersiz işaretçi geçirildi.</span><span class="sxs-lookup"><span data-stu-id="7d363-864">**NX_PTR_ERROR** (0x07) Invalid pointer passed.</span></span>
- <span data-ttu-id="7d363-865">**NX_INVALID_PARAMETERS** (0x4D) BIR sertifika kimliği (0) geçirildi.</span><span class="sxs-lookup"><span data-stu-id="7d363-865">**NX_INVALID_PARAMETERS** (0x4D) A certificate ID of 0 was passed in.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="7d363-866">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="7d363-866">Allowed From</span></span>

<span data-ttu-id="7d363-867">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="7d363-867">Threads</span></span>

### <a name="example"></a><span data-ttu-id="7d363-868">Örnek</span><span class="sxs-lookup"><span data-stu-id="7d363-868">Example</span></span>

<span data-ttu-id="7d363-869">\* Daha kapsamlı bir örnek için bkz. *nx_secure_dtls_session_create* başvurusu.</span><span class="sxs-lookup"><span data-stu-id="7d363-869">\*See reference for *nx_secure_dtls_session_create* for a more complete example.</span></span>

```C
/* Our DTLS Server instance. */
NX_SECURE_DTLS_SESSION dtls_client;

/* Certificate control block and data.
Identity certificates require a private key. */
NX_SECURE_X509_CERT certificate;
UCHAR certificate_der_data[] = { … };
UCHAR certificate_key_der_data[] = { … };


/* Application thread where TLS session is started. */
void application_thread()
{
NXD_ADDRESS server_ip;

    /* Create a TLS session for our socket. Ciphers and metadata defined
       elsewhere. See nx_secure_tls_session_create reference for more
       information. */
    status =  nx_secure_dtls_session_create(&client_dtls_session,
                                            &nx_crypto_tls_ciphers,
                                            crypto_metadata,
                                            sizeof(crypto_metadata),
                                            packet_buffer,
                                            sizeof(packet_buffer),
                                            REMOTE_CERT_NUMBER,
                                            remote_certs_buffer,
                                            sizeof(remote_certs_buffer));

    /* Check for error.  */
    if(status)
    {
        printf("Error in function nx_secure_dtls_session_create: 0x%x\n", status);
    }

    /* Initialize our trusted certificate. See section “Importing X.509
   Certificates into NetX Secure” for more information. */
    nx_secure_x509_certificate_initialize(&trusted_certificate,
                                            trusted_cert_der,
                                            trusted_cert_der_len,
                                            NX_NULL, 0, NX_NULL, 0,
                                            NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add the certificate to the trusted store using a numeric ID. */
    nx_secure_dtls_session_trusted_certificate_add(&client_dtls_session,
                                                      &certificate, 1);

    /* Initialize local server identity certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&certificate,
                                            certificate_der_data,
                                            sizeof(certificate_der_data),
                                            NX_NULL, 0,
                                            certificate_key_der_data,
                                            sizeof(certificate_key_der_data),
                                            NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_session_local_certificate_add(&dtls_client,
                                                        &certificate, 1);

    /* Set up IP address of remote host. */
    server_ip.nxd_ip_version = NX_IP_VERSION_V4;
    server_ip.nxd_ip_address.v4 = IP_ADDRESS(192, 168, 1, 150);

    /* Now we can start the DTLS session as normal. */
    status =  nx_secure_dtls_client_session_start(&client_dtls_session,
         &udp_socket, &server_ip, 4443,
         NX_IP_PERIODIC_RATE);


    /* Process responses, etc…*/
}

```

### <a name="see-also"></a><span data-ttu-id="7d363-870">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="7d363-870">See Also</span></span>

- <span data-ttu-id="7d363-871">nx_secure_dtls_session_create, nx_secure_dtls_session_receive,</span><span class="sxs-lookup"><span data-stu-id="7d363-871">nx_secure_dtls_session_create, nx_secure_dtls_session_receive,</span></span>
- <span data-ttu-id="7d363-872">nx_secure_dtls_session_send, nx_secure_dtls_session_start,</span><span class="sxs-lookup"><span data-stu-id="7d363-872">nx_secure_dtls_session_send, nx_secure_dtls_session_start,</span></span>
- <span data-ttu-id="7d363-873">nx_secure_dtls_session_trusted_certificate_remove,</span><span class="sxs-lookup"><span data-stu-id="7d363-873">nx_secure_dtls_session_trusted_certificate_remove,</span></span>
- <span data-ttu-id="7d363-874">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="7d363-874">nx_secure_x509_certificate_initialize</span></span>

## <a name="nx_secure_dtls_session_trusted_certificate_remove"></a><span data-ttu-id="7d363-875">nx_secure_dtls_session_trusted_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="7d363-875">nx_secure_dtls_session_trusted_certificate_remove</span></span>

<span data-ttu-id="7d363-876">NetX güvenli DTLS oturumundan güvenilir bir CA sertifikasını kaldırma</span><span class="sxs-lookup"><span data-stu-id="7d363-876">Remove a trusted CA certificate from a NetX Secure DTLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="7d363-877">Prototype</span><span class="sxs-lookup"><span data-stu-id="7d363-877">Prototype</span></span>

```C
UINT  nx_secure_dtls_session_trusted_certificate_remove(
                            NX_SECURE_DTLS_SESSION *session_ptr,
                            UCHAR *common_name,
                            UINT common_name_length, UINT cert_id);

```

### <a name="description"></a><span data-ttu-id="7d363-878">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7d363-878">Description</span></span>

<span data-ttu-id="7d363-879">Bu hizmet, bir sertifika KIMLIĞI numarası (sertifika nx_secure_dtls_session_trusted_certificate_add ile eklendiğinde atanır) veya X. 509.440 CommonName alanı kullanarak bir DTLS oturum örneğinden güvenilir bir CA sertifikasını kaldırır.</span><span class="sxs-lookup"><span data-stu-id="7d363-879">This service removes a trusted CA certificate from a DTLS Session instance using either a certificate ID number (assigned when the certificate was added with nx_secure_dtls_session_trusted_certificate_add) or the X.509 CommonName field.</span></span>

<span data-ttu-id="7d363-880">Common_name sertifikayla eşleştirmek için kullanılırsa, cert_id parametresi 0 olarak ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7d363-880">If the common_name is used to match the certificate, the cert_id parameter should be set to 0.</span></span> <span data-ttu-id="7d363-881">Cert_id kullanılırsa, common_name NX_NULL bir değer geçirmelidir.</span><span class="sxs-lookup"><span data-stu-id="7d363-881">If cert_id is used, common_name should be passed a value of NX_NULL.</span></span>

<span data-ttu-id="7d363-882">Cert_id parametresi, sertifika için sayısal, sıfır olmayan bir tanıtıcıdır.</span><span class="sxs-lookup"><span data-stu-id="7d363-882">The cert_id parameter is a numeric, non-zero identifier for the certificate.</span></span> <span data-ttu-id="7d363-883">Bu, DTLS sertifika deposunda aynı X. 509.440 ortak adına sahip birden çok kimlik sertifikası bulunan olayda kolayca kaldırılmasını veya bu durumda bulunabilmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="7d363-883">This enables the certificate to be easily removed or found in the event there are multiple identity certificates with the same X.509 Common Name present in the DTLS certificate store.</span></span> <span data-ttu-id="7d363-884">X. 509.440 sertifikaları hakkında daha fazla bilgi için NetX güvenli TLS Kullanıcı Kılavuzu 'na bakın.</span><span class="sxs-lookup"><span data-stu-id="7d363-884">See the NetX Secure TLS User Guide for more information about X.509 certificates.</span></span>

### <a name="parameters"></a><span data-ttu-id="7d363-885">Parametreler</span><span class="sxs-lookup"><span data-stu-id="7d363-885">Parameters</span></span>

- <span data-ttu-id="7d363-886">**session_ptr** Daha önce oluşturulmuş bir DTLS oturum örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="7d363-886">**session_ptr** Pointer to a previously created DTLS Session instance.</span></span>
- <span data-ttu-id="7d363-887">**common_name** Eşleştirilecek CommonName dizesinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="7d363-887">**common_name** Pointer to the CommonName string to match.</span></span>
- <span data-ttu-id="7d363-888">**common_name_length** Common_name dizesinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="7d363-888">**common_name_length** Length of the common_name string.</span></span>
- <span data-ttu-id="7d363-889">**cert_id** Bu DTLS sunucusunda bu sertifika için sıfır olmayan sayısal benzersiz tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="7d363-889">**cert_id** Numeric non-zero unique identifier for this certificate in this DTLS server.</span></span>


### <a name="return-values"></a><span data-ttu-id="7d363-890">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="7d363-890">Return Values</span></span>

- <span data-ttu-id="7d363-891">**NX_SUCCESS** (0x00) DTLS oturumundan sertifika başarıyla silindi.</span><span class="sxs-lookup"><span data-stu-id="7d363-891">**NX_SUCCESS** (0x00) Successful removal of certificate from DTLS session.</span></span>
- <span data-ttu-id="7d363-892">**NX_PTR_ERROR** (0x07) geçersiz işaretçi geçirildi.</span><span class="sxs-lookup"><span data-stu-id="7d363-892">**NX_PTR_ERROR** (0x07) Invalid pointer passed.</span></span>
- <span data-ttu-id="7d363-893">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) VERILEN DTLS oturumunda cert_id veya common_name eşleşen bir sertifika bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="7d363-893">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) No certificate matching the cert_id or common_name was found in the given DTLS session.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="7d363-894">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="7d363-894">Allowed From</span></span>

<span data-ttu-id="7d363-895">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="7d363-895">Threads</span></span>

### <a name="example"></a><span data-ttu-id="7d363-896">Örnek</span><span class="sxs-lookup"><span data-stu-id="7d363-896">Example</span></span>

<span data-ttu-id="7d363-897">\* Daha kapsamlı bir örnek için bkz. *nx_secure_dtls_session_create* başvurusu.</span><span class="sxs-lookup"><span data-stu-id="7d363-897">\*See reference for *nx_secure_dtls_session_create* for a more complete example.</span></span>

```C
/* Our DTLS Server instance. */
NX_SECURE_DTLS_SESSION dtls_client;

/* Certificate control block and data. Identity certificates require a private key. */
NX_SECURE_X509_CERT certificate;
UCHAR certificate_der_data[] = { … };
UCHAR certificate_key_der_data[] = { … };


/* Application thread where TLS session is started. */
void application_thread()
{
    NXD_ADDRESS server_ip;

    /* Create a TLS session for our socket. Ciphers and metadata defined
    elsewhere. See nx_secure_tls_session_create reference for more
    information. */
        status =  nx_secure_dtls_session_create(&client_dtls_session,
                                            &nx_crypto_tls_ciphers,
                                            crypto_metadata,
                                            sizeof(crypto_metadata),
                                            packet_buffer,
                                            sizeof(packet_buffer),
                                            REMOTE_CERT_NUMBER,
                                            remote_certs_buffer,
                                            sizeof(remote_certs_buffer));

    /* Check for error.  */
    if(status)
    {
        printf("Error in function nx_secure_dtls_session_create: 0x%x\n", status);
    }

    /* Initialize our trusted certificate. See section “Importing X.509
    Certificates into NetX Secure” for more information. */
        nx_secure_x509_certificate_initialize(&trusted_certificate,
                                    trusted_cert_der,
                                    trusted_cert_der_len, NX_NULL, 0,
                                    NX_NULL, 0,
                                    NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add the certificate to the local store using a numeric ID. */
        nx_secure_dtls_session_trusted_certificate_add(&client_dtls_session,
                                                            &certificate, 1);

    /* Initialize local server identity certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&certificate,
                                            certificate_der_data,
                                            sizeof(certificate_der_data),
                                            NX_NULL, 0,
                                            certificate_key_der_data,
                                            sizeof(certificate_key_der_data),
                                            NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_session_local_certificate_add(&dtls_client,
                                                        &certificate, 1);

    /* Set up IP address of remote host. */
    server_ip.nxd_ip_version = NX_IP_VERSION_V4;
    server_ip.nxd_ip_address.v4 = IP_ADDRESS(192, 168, 1, 150);


    /* Now we can start the DTLS session as normal. */
    status =  nx_secure_dtls_client_session_start(&client_dtls_session,
                                        &udp_socket, &server_ip, 4443,
                                        NX_IP_PERIODIC_RATE);

    /* Process responses, etc…*/

    /* At some point in the future,
    we decide to remove the certificate using the ID of 1
    when it was added to the session. */
    status = nx_secure_dtls_session_trusted_certificate_remove(&client_dtls_session,
                                                                    NX_NULL, 0, 1);
}

```

### <a name="see-also"></a><span data-ttu-id="7d363-898">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="7d363-898">See Also</span></span>

- <span data-ttu-id="7d363-899">nx_secure_dtls_session_create, nx_secure_dtls_session_receive,</span><span class="sxs-lookup"><span data-stu-id="7d363-899">nx_secure_dtls_session_create, nx_secure_dtls_session_receive,</span></span>
- <span data-ttu-id="7d363-900">nx_secure_dtls_session_send, nx_secure_dtls_session_start,</span><span class="sxs-lookup"><span data-stu-id="7d363-900">nx_secure_dtls_session_send, nx_secure_dtls_session_start,</span></span>
- <span data-ttu-id="7d363-901">nx_secure_dtls_session_trusted_certificate_add,</span><span class="sxs-lookup"><span data-stu-id="7d363-901">nx_secure_dtls_session_trusted_certificate_add,</span></span>
- <span data-ttu-id="7d363-902">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="7d363-902">nx_secure_x509_certificate_initialize</span></span>
