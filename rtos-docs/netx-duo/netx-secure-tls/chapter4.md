---
title: Bölüm 4-Azure RTOS NetX güvenli hizmetlerinin açıklaması
description: Bu bölüm, tüm NetX güvenli hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 80ec22058ab64ed0c6258bb3d9364ec44f9a741b
ms.sourcegitcommit: 4ebe7c51ba850951c6a9d0f15e22d07bb752bc28
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/20/2021
ms.locfileid: "110223401"
---
# <a name="chapter-4---description-of-azure-rtos-netx-secure-services"></a><span data-ttu-id="1c3ae-103">Bölüm 4-Azure RTOS NetX güvenli hizmetlerinin açıklaması</span><span class="sxs-lookup"><span data-stu-id="1c3ae-103">Chapter 4 - Description of Azure RTOS NetX Secure services</span></span>

<span data-ttu-id="1c3ae-104">Bu bölüm, tüm Azure RTOS NetX güvenli hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-104">This chapter contains a description of all Azure RTOS NetX Secure services (listed below) in alphabetic order.</span></span>

<span data-ttu-id="1c3ae-105">Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_SECURE_DISABLE_ERROR_CHECKING** makrodan etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-105">In the "Return Values" section in the following API descriptions, values in **BOLD** are not affected by the **NX_SECURE_DISABLE_ERROR_CHECKING** macro that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

- [<span data-ttu-id="1c3ae-106">nx_secure_crypto_table_self_test</span><span class="sxs-lookup"><span data-stu-id="1c3ae-106">nx_secure_crypto_table_self_test</span></span>](#nx_secure_crypto_table_self_test)
  - <span data-ttu-id="1c3ae-107">Şifreleme yöntemlerinde self_test gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="1c3ae-107">Perform self_test on the crypto methods</span></span>
- [<span data-ttu-id="1c3ae-108">nx_secure_module_hash_compute</span><span class="sxs-lookup"><span data-stu-id="1c3ae-108">nx_secure_module_hash_compute</span></span>](#nx_secure_module_hash_compute)
  - <span data-ttu-id="1c3ae-109">Karma değeri user_supplied karma işlevi kullanılarak hesaplar</span><span class="sxs-lookup"><span data-stu-id="1c3ae-109">Computes hash value using user_supplied hash function</span></span>
- [<span data-ttu-id="1c3ae-110">nx_secure_tls_active_certificate_set</span><span class="sxs-lookup"><span data-stu-id="1c3ae-110">nx_secure_tls_active_certificate_set</span></span>](#nx_secure_tls_active_certificate_set)
  - <span data-ttu-id="1c3ae-111">NetX güvenli TLS oturumu için etkin kimlik sertifikası ayarlama</span><span class="sxs-lookup"><span data-stu-id="1c3ae-111">Set the active identity certificate for a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="1c3ae-112">nx_secure_tls_client_psk_set</span><span class="sxs-lookup"><span data-stu-id="1c3ae-112">nx_secure_tls_client_psk_set</span></span>](#nx_secure_tls_client_psk_set)
  - <span data-ttu-id="1c3ae-113">NetX güvenli TLS Istemci oturumu için bir Pre_Shared anahtarı ayarlama</span><span class="sxs-lookup"><span data-stu-id="1c3ae-113">Set a Pre_Shared Key for a NetX Secure TLS Client Session</span></span>
- [<span data-ttu-id="1c3ae-114">nx_secure_tls_initialize</span><span class="sxs-lookup"><span data-stu-id="1c3ae-114">nx_secure_tls_initialize</span></span>](#nx_secure_tls_initialize)
  - <span data-ttu-id="1c3ae-115">NetX güvenli TLS modülünü başlatır]</span><span class="sxs-lookup"><span data-stu-id="1c3ae-115">Initializes the NetX Secure TLS module]</span></span>
- [<span data-ttu-id="1c3ae-116">nx_secure_tls_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="1c3ae-116">nx_secure_tls_local_certificate_add</span></span>](#nx_secure_tls_local_certificate_add)
  - <span data-ttu-id="1c3ae-117">NetX güvenli TLS oturumuna yerel sertifika ekleme</span><span class="sxs-lookup"><span data-stu-id="1c3ae-117">Add a local certificate to NetX Secure TLS Session</span></span>
- [<span data-ttu-id="1c3ae-118">nx_secure_tls_local_certificate_find</span><span class="sxs-lookup"><span data-stu-id="1c3ae-118">nx_secure_tls_local_certificate_find</span></span>](#nx_secure_tls_local_certificate_find)
  - <span data-ttu-id="1c3ae-119">Ortak ad ile bir NetX güvenli TLS oturumunda yerel bir sertifika bulun</span><span class="sxs-lookup"><span data-stu-id="1c3ae-119">Find a local certificate in a NetX Secure TLS Session by Common Name</span></span>
- [<span data-ttu-id="1c3ae-120">nx_secure_tls_local_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="1c3ae-120">nx_secure_tls_local_certificate_remove</span></span>](#nx_secure_tls_local_certificate_remove)
  - <span data-ttu-id="1c3ae-121">NetX Secure TLS Oturumundan yerel sertifikayı kaldırma</span><span class="sxs-lookup"><span data-stu-id="1c3ae-121">Remove local certificate from NetX Secure TLS Session</span></span>
- [<span data-ttu-id="1c3ae-122">nx_secure_tls_metadata_size_calculate</span><span class="sxs-lookup"><span data-stu-id="1c3ae-122">nx_secure_tls_metadata_size_calculate</span></span>](#nx_secure_tls_metadata_size_calculate)
  - <span data-ttu-id="1c3ae-123">NetX Güvenli TLS Oturumu için şifreleme meta verisi boyutunu hesaplama</span><span class="sxs-lookup"><span data-stu-id="1c3ae-123">Calculate size of cryptographic metadata for a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="1c3ae-124">nx_secure_tls_packet_allocate</span><span class="sxs-lookup"><span data-stu-id="1c3ae-124">nx_secure_tls_packet_allocate</span></span>](#nx_secure_tls_packet_allocate)
  - <span data-ttu-id="1c3ae-125">NetX Güvenli TLS Oturumu için paket ayırma</span><span class="sxs-lookup"><span data-stu-id="1c3ae-125">Allocate a packet for a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="1c3ae-126">nx_secure_tls_psk_add</span><span class="sxs-lookup"><span data-stu-id="1c3ae-126">nx_secure_tls_psk_add</span></span>](#nx_secure_tls_psk_add)
  - <span data-ttu-id="1c3ae-127">NetX Pre_Shared TLS Oturumuna Bir Anahtar Ekleme</span><span class="sxs-lookup"><span data-stu-id="1c3ae-127">Add a Pre_Shared Key to a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="1c3ae-128">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="1c3ae-128">nx_secure_tls_remote_certificate_allocate</span></span>](#nx_secure_tls_remote_certificate_allocate)
  - <span data-ttu-id="1c3ae-129">Uzak bir TLS ana bilgisayarı tarafından sağlanan sertifika için alan ayırma</span><span class="sxs-lookup"><span data-stu-id="1c3ae-129">Allocate space for the certificate provided by a remote TLS host</span></span>
- [<span data-ttu-id="1c3ae-130">nx_secure_tls_remote_certificate_buffer_allocate</span><span class="sxs-lookup"><span data-stu-id="1c3ae-130">nx_secure_tls_remote_certificate_buffer_allocate</span></span>](#nx_secure_tls_remote_certificate_buffer_allocate)
  - <span data-ttu-id="1c3ae-131">Uzak bir TLS ana bilgisayarı tarafından sağlanan tüm sertifikalar için alan ayırma</span><span class="sxs-lookup"><span data-stu-id="1c3ae-131">Allocate space for all certificates provided by a remote TLS host</span></span>
- [<span data-ttu-id="1c3ae-132">nx_secure_tls_remote_certificate_free_all</span><span class="sxs-lookup"><span data-stu-id="1c3ae-132">nx_secure_tls_remote_certificate_free_all</span></span>](#nx_secure_tls_remote_certificate_free_all)
  - <span data-ttu-id="1c3ae-133">Gelen sertifikalar için ayrılan boş alan</span><span class="sxs-lookup"><span data-stu-id="1c3ae-133">Free space allocated for incoming certificates</span></span>
- [<span data-ttu-id="1c3ae-134">nx_secure_tls_server_certificate_add</span><span class="sxs-lookup"><span data-stu-id="1c3ae-134">nx_secure_tls_server_certificate_add</span></span>](#nx_secure_tls_server_certificate_add)
  - <span data-ttu-id="1c3ae-135">Sayısal tanımlayıcı kullanan TLS sunucuları için özel olarak sertifika ekleme</span><span class="sxs-lookup"><span data-stu-id="1c3ae-135">Add a certificate specifically for TLS servers using a numeric identifier</span></span>
- [<span data-ttu-id="1c3ae-136">nx_secure_tls_server_certificate_find</span><span class="sxs-lookup"><span data-stu-id="1c3ae-136">nx_secure_tls_server_certificate_find</span></span>](#nx_secure_tls_server_certificate_find)
  - <span data-ttu-id="1c3ae-137">Sayısal tanımlayıcı kullanarak sertifika bulma</span><span class="sxs-lookup"><span data-stu-id="1c3ae-137">Find a certificate using a numeric identifier</span></span>
- [<span data-ttu-id="1c3ae-138">nx_secure_tls_server_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="1c3ae-138">nx_secure_tls_server_certificate_remove</span></span>](#nx_secure_tls_server_certificate_remove)
  - <span data-ttu-id="1c3ae-139">Sayısal tanımlayıcı kullanarak yerel sunucu sertifikasını kaldırma</span><span class="sxs-lookup"><span data-stu-id="1c3ae-139">Remove a local server certificate using a numeric identifier</span></span>
- [<span data-ttu-id="1c3ae-140">nx_secure_tls_session_certificate_callback_set</span><span class="sxs-lookup"><span data-stu-id="1c3ae-140">nx_secure_tls_session_certificate_callback_set</span></span>](#nx_secure_tls_session_certificate_callback_set)
  - <span data-ttu-id="1c3ae-141">Ek sertifika doğrulaması için kullanılacak TLS için bir geri çağırma ayarlayın</span><span class="sxs-lookup"><span data-stu-id="1c3ae-141">Set up a callback for TLS to use for additional certificate validation</span></span>
- [<span data-ttu-id="1c3ae-142">nx_secure_tls_session_client_callback_set</span><span class="sxs-lookup"><span data-stu-id="1c3ae-142">nx_secure_tls_session_client_callback_set</span></span>](#nx_secure_tls_session_client_callback_set)
  - <span data-ttu-id="1c3ae-143">TLS Istemcisi el sıkışmasının başlangıcında çağırmak üzere TLS için bir geri çağırma ayarlayın</span><span class="sxs-lookup"><span data-stu-id="1c3ae-143">Set up a callback for TLS to invoke at the beginning of a TLS Client handshake</span></span>
- [<span data-ttu-id="1c3ae-144">nx_secure_tls_session_x509_client_verify_configure</span><span class="sxs-lookup"><span data-stu-id="1c3ae-144">nx_secure_tls_session_x509_client_verify_configure</span></span>](#nx_secure_tls_session_x509_client_verify_configure)
  - <span data-ttu-id="1c3ae-145">İstemci X. 509.440 doğrulamasını etkinleştir ve istemci sertifikaları için alan ayır</span><span class="sxs-lookup"><span data-stu-id="1c3ae-145">Enable client X.509 verification and allocate space for client certificates</span></span>
- [<span data-ttu-id="1c3ae-146">nx_secure_tls_session_client_verify_disable</span><span class="sxs-lookup"><span data-stu-id="1c3ae-146">nx_secure_tls_session_client_verify_disable</span></span>](#nx_secure_tls_session_client_verify_disable)
  - <span data-ttu-id="1c3ae-147">NetX güvenli TLS oturumu için Istemci sertifikası kimlik doğrulamasını devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="1c3ae-147">Disable Client Certificate Authentication for a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="1c3ae-148">nx_secure_tls_session_client_verify_enable</span><span class="sxs-lookup"><span data-stu-id="1c3ae-148">nx_secure_tls_session_client_verify_enable</span></span>](#nx_secure_tls_session_client_verify_enable)
  - <span data-ttu-id="1c3ae-149">NetX güvenli TLS oturumu için Istemci sertifikası kimlik doğrulamasını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="1c3ae-149">Enable Client Certificate Authentication for a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="1c3ae-150">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="1c3ae-150">nx_secure_tls_session_create</span></span>](#nx_secure_tls_session_create)
  - <span data-ttu-id="1c3ae-151">Güvenli iletişim için bir NetX güvenli TLS oturumu oluşturun</span><span class="sxs-lookup"><span data-stu-id="1c3ae-151">Create a NetX Secure TLS Session for secure communications</span></span>
- [<span data-ttu-id="1c3ae-152">nx_secure_tls_session_delete</span><span class="sxs-lookup"><span data-stu-id="1c3ae-152">nx_secure_tls_session_delete</span></span>](#nx_secure_tls_session_delete)
  - <span data-ttu-id="1c3ae-153">NetX güvenli TLS oturumunu silme</span><span class="sxs-lookup"><span data-stu-id="1c3ae-153">Delete a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="1c3ae-154">nx_secure_tls_session_end</span><span class="sxs-lookup"><span data-stu-id="1c3ae-154">nx_secure_tls_session_end</span></span>](#nx_secure_tls_session_end)
  - <span data-ttu-id="1c3ae-155">Etkin bir NetX güvenli TLS oturumu sonlandır</span><span class="sxs-lookup"><span data-stu-id="1c3ae-155">End an active NetX Secure TLS Session</span></span>
- [<span data-ttu-id="1c3ae-156">nx_secure_tls_session_packet_buffer_set</span><span class="sxs-lookup"><span data-stu-id="1c3ae-156">nx_secure_tls_session_packet_buffer_set</span></span>](#nx_secure_tls_session_packet_buffer_set)
  - <span data-ttu-id="1c3ae-157">NetX güvenli TLS oturumu için paket yeniden birleştirme arabelleğini ayarlama</span><span class="sxs-lookup"><span data-stu-id="1c3ae-157">Set the packet reassembly buffer for a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="1c3ae-158">nx_secure_tls_session_protocol_version_override</span><span class="sxs-lookup"><span data-stu-id="1c3ae-158">nx_secure_tls_session_protocol_version_override</span></span>](#nx_secure_tls_session_protocol_version_override)
  - <span data-ttu-id="1c3ae-159">NetX güvenli TLS oturumu için varsayılan TLS protokol sürümünü geçersiz kılın</span><span class="sxs-lookup"><span data-stu-id="1c3ae-159">Override the default TLS protocol version for a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="1c3ae-160">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="1c3ae-160">nx_secure_tls_session_receive</span></span>](#nx_secure_tls_session_receive)
  - <span data-ttu-id="1c3ae-161">NetX Güvenli TLS Oturumundan veri alma</span><span class="sxs-lookup"><span data-stu-id="1c3ae-161">Receive data from a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="1c3ae-162">nx_secure_tls_session_renegotiate_callback_set</span><span class="sxs-lookup"><span data-stu-id="1c3ae-162">nx_secure_tls_session_renegotiate_callback_set</span></span>](#nx_secure_tls_session_renegotiate_callback_set)
  - <span data-ttu-id="1c3ae-163">Oturum yeniden görüşmenin başında çağrılan bir geri çağırma at atama</span><span class="sxs-lookup"><span data-stu-id="1c3ae-163">Assign a callback that will be invoked at the beginning of a session renegotiation</span></span>
- [<span data-ttu-id="1c3ae-164">nx_secure_tls_session_renegotiate</span><span class="sxs-lookup"><span data-stu-id="1c3ae-164">nx_secure_tls_session_renegotiate</span></span>](#nx_secure_tls_session_renegotiate)
  - <span data-ttu-id="1c3ae-165">Uzak konakla oturum yeniden anlaşma başlatma</span><span class="sxs-lookup"><span data-stu-id="1c3ae-165">Initiate a session renegotiation handshake with the remote host</span></span>
- [<span data-ttu-id="1c3ae-166">nx_secure_tls_session_reset</span><span class="sxs-lookup"><span data-stu-id="1c3ae-166">nx_secure_tls_session_reset</span></span>](#nx_secure_tls_session_reset)
  - <span data-ttu-id="1c3ae-167">NetX Secure TLS Oturumunu temizleme ve sıfırlama</span><span class="sxs-lookup"><span data-stu-id="1c3ae-167">Clear out and reset a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="1c3ae-168">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="1c3ae-168">nx_secure_tls_session_send</span></span>](#nx_secure_tls_session_send)
  - <span data-ttu-id="1c3ae-169">NetX Güvenli TLS Oturumu aracılığıyla veri gönderme</span><span class="sxs-lookup"><span data-stu-id="1c3ae-169">Send data through a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="1c3ae-170">nx_secure_tls_session_server_callback_set</span><span class="sxs-lookup"><span data-stu-id="1c3ae-170">nx_secure_tls_session_server_callback_set</span></span>](#nx_secure_tls_session_server_callback_set)
  - <span data-ttu-id="1c3ae-171">TLS Sunucusu el sıkışması başlangıcında çağırmak için TLS için bir geri çağırma ayarlayın</span><span class="sxs-lookup"><span data-stu-id="1c3ae-171">Set up a callback for TLS to invoke at the beginning of a TLS Server handshake</span></span>
- [<span data-ttu-id="1c3ae-172">nx_secure_tls_session_sni_extension_parse</span><span class="sxs-lookup"><span data-stu-id="1c3ae-172">nx_secure_tls_session_sni_extension_parse</span></span>](#nx_secure_tls_session_sni_extension_parse)
  - <span data-ttu-id="1c3ae-173">TLS İstemcisi Sunucu Adı Belirtme alınan bir Sunucu Adı Belirtme (SNI) uzantısını ayrıştırma</span><span class="sxs-lookup"><span data-stu-id="1c3ae-173">Parse a Server Name Indication (SNI) extension received from a TLS Client</span></span>
- [<span data-ttu-id="1c3ae-174">nx_secure_tls_session_sni_extension_set</span><span class="sxs-lookup"><span data-stu-id="1c3ae-174">nx_secure_tls_session_sni_extension_set</span></span>](#nx_secure_tls_session_sni_extension_set)
  - <span data-ttu-id="1c3ae-175">Uzak Sunucu Adı Belirtme (SNI) uzantısı DNS adı ayarlama</span><span class="sxs-lookup"><span data-stu-id="1c3ae-175">Set a Server Name Indication (SNI) extension DNS name to send to a remote Server</span></span>
- [<span data-ttu-id="1c3ae-176">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="1c3ae-176">nx_secure_tls_session_start</span></span>](#nx_secure_tls_session_start)
  - <span data-ttu-id="1c3ae-177">NetX Güvenli TLS Oturumu Başlatma</span><span class="sxs-lookup"><span data-stu-id="1c3ae-177">Start a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="1c3ae-178">nx_secure_tls_session_time_function_set</span><span class="sxs-lookup"><span data-stu-id="1c3ae-178">nx_secure_tls_session_time_function_set</span></span>](#nx_secure_tls_session_time_function_set)
  - <span data-ttu-id="1c3ae-179">NetX Güvenli TLS Oturumuna zaman damgası işlevi atama</span><span class="sxs-lookup"><span data-stu-id="1c3ae-179">Assign a timestamp function to a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="1c3ae-180">nx_secure_tls_trusted_certificate_add</span><span class="sxs-lookup"><span data-stu-id="1c3ae-180">nx_secure_tls_trusted_certificate_add</span></span>](#nx_secure_tls_trusted_certificate_add)
  - <span data-ttu-id="1c3ae-181">NetX güvenli TLS oturumuna güvenilen sertifika ekleme</span><span class="sxs-lookup"><span data-stu-id="1c3ae-181">Add trusted certificate to NetX Secure TLS Session</span></span>
- [<span data-ttu-id="1c3ae-182">nx_secure_tls_trusted_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="1c3ae-182">nx_secure_tls_trusted_certificate_remove</span></span>](#nx_secure_tls_trusted_certificate_remove)
  - <span data-ttu-id="1c3ae-183">Güvenilen sertifikayı NetX güvenli TLS oturumundan kaldır</span><span class="sxs-lookup"><span data-stu-id="1c3ae-183">Remove trusted certificate from NetX Secure TLS Session</span></span>
- [<span data-ttu-id="1c3ae-184">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="1c3ae-184">nx_secure_x509_certificate_initialize</span></span>](#nx_secure_x509_certificate_initialize)
  - <span data-ttu-id="1c3ae-185">NetX güvenli TLS için X. 509.440 sertifikasını başlatın</span><span class="sxs-lookup"><span data-stu-id="1c3ae-185">Initialize X.509 Certificate for NetX Secure TLS</span></span>
- [<span data-ttu-id="1c3ae-186">nx_secure_x509_common_name_dns_check</span><span class="sxs-lookup"><span data-stu-id="1c3ae-186">nx_secure_x509_common_name_dns_check</span></span>](#nx_secure_x509_common_name_dns_check)
  - <span data-ttu-id="1c3ae-187">X. 509.440 sertifikasıyla DNS adını denetle</span><span class="sxs-lookup"><span data-stu-id="1c3ae-187">Check DNS name against X.509 Certificate</span></span>
- [<span data-ttu-id="1c3ae-188">nx_secure_x509_crl_revocation_check</span><span class="sxs-lookup"><span data-stu-id="1c3ae-188">nx_secure_x509_crl_revocation_check</span></span>](#nx_secure_x509_crl_revocation_check)
  - <span data-ttu-id="1c3ae-189">Sağlanan sertifika Iptal listesine (CRL) göre X. 509.440 sertifikasını denetle]</span><span class="sxs-lookup"><span data-stu-id="1c3ae-189">Check X.509 Certificate against a supplied Certificate Revocation List (CRL)]</span></span>
- [<span data-ttu-id="1c3ae-190">nx_secure_x509_dns_name_initialize</span><span class="sxs-lookup"><span data-stu-id="1c3ae-190">nx_secure_x509_dns_name_initialize</span></span>](#nx_secure_x509_dns_name_initialize)
  - <span data-ttu-id="1c3ae-191">X. 509.440 DNS adı yapısını başlatma</span><span class="sxs-lookup"><span data-stu-id="1c3ae-191">Initialize an X.509 DNS name structure</span></span>
- [<span data-ttu-id="1c3ae-192">nx_secure_x509_extended_key_usage_extension_parse</span><span class="sxs-lookup"><span data-stu-id="1c3ae-192">nx_secure_x509_extended_key_usage_extension_parse</span></span>](#nx_secure_x509_extended_key_usage_extension_parse)
  - <span data-ttu-id="1c3ae-193">X. 509.440 sertifikası içindeki X. 509.952 genişletilmiş anahtar kullanımı uzantısını bulma ve ayrıştırma</span><span class="sxs-lookup"><span data-stu-id="1c3ae-193">Find and parse an X.509 extended key usage extension in an X.509 certificate</span></span>
- [<span data-ttu-id="1c3ae-194">nx_secure_x509_extension_find</span><span class="sxs-lookup"><span data-stu-id="1c3ae-194">nx_secure_x509_extension_find</span></span>](#nx_secure_x509_extension_find)
  - <span data-ttu-id="1c3ae-195">X. 509.440 sertifikasında bir X. 509.440 uzantısı bulun ve döndürün</span><span class="sxs-lookup"><span data-stu-id="1c3ae-195">Find and return an X.509 extension in an X.509 certificate</span></span>
- [<span data-ttu-id="1c3ae-196">nx_secure_x509_key_usage_extension_parse</span><span class="sxs-lookup"><span data-stu-id="1c3ae-196">nx_secure_x509_key_usage_extension_parse</span></span>](#nx_secure_x509_key_usage_extension_parse)
  - <span data-ttu-id="1c3ae-197">X. 509.440 sertifikasında X. 509.440 anahtar kullanımı uzantısını bulma ve ayrıştırma</span><span class="sxs-lookup"><span data-stu-id="1c3ae-197">Find and parse an X.509 Key Usage extension in an X.509 certificate</span></span>

## <a name="nx_secure_crypto_table_self_test"></a><span data-ttu-id="1c3ae-198">nx_secure_crypto_table_self_test</span><span class="sxs-lookup"><span data-stu-id="1c3ae-198">nx_secure_crypto_table_self_test</span></span>

<span data-ttu-id="1c3ae-199">Şifre yöntemlerinde kendi kendine test gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="1c3ae-199">Perform self-test on the crypto methods</span></span>

### <a name="prototype"></a><span data-ttu-id="1c3ae-200">Prototype</span><span class="sxs-lookup"><span data-stu-id="1c3ae-200">Prototype</span></span>

```C
UINT nx_secure_crypto_table_self_test(
                                  const NX_SECURE_TLS_CRYPTO *crypto_table,
                                  VOID *metadata, UINT metadata_size);
```

### <a name="description"></a><span data-ttu-id="1c3ae-201">Description</span><span class="sxs-lookup"><span data-stu-id="1c3ae-201">Description</span></span>

<span data-ttu-id="1c3ae-202">Bu hizmet, doğrulamak üzere kendi kendini test eden şifreleme yöntemi aracılığıyla çalışır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-202">This service runs through the crypto method self tests to validate.</span></span> <span data-ttu-id="1c3ae-203">Kendi kendine test yalnızca NetX Secure kitaplığı tanımlandığı gibi sembolüyle NX_SECURE_POWER_ON_SELF_TEST_MODULE_INTEGRITY_CHECK kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-203">The self test is available only if NetX Secure library is built with the symbol NX_SECURE_POWER_ON_SELF_TEST_MODULE_INTEGRITY_CHECK defined.</span></span>

<span data-ttu-id="1c3ae-204">Desteklenen her şifreleme yöntemi için, kendi kendine test önceden tanımlanmış giriş verileri sağlar ve çıkışın önceden tanımlanmış beklenen değerle eşleştirildi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-204">For each supported crypto method, the self test provides pre-defined input data, and verified the output matches the pre-defined expected value.</span></span>

<span data-ttu-id="1c3ae-205">NetX Secure şifreleme kendi kendine testi aşağıdaki algoritmaları ve anahtar boyutlarını destekler:</span><span class="sxs-lookup"><span data-stu-id="1c3ae-205">NetX Secure crypto self test supports the following algorithms and key sizes:</span></span>

- <span data-ttu-id="1c3ae-206">DES: şifreleme ve şifre çözme</span><span class="sxs-lookup"><span data-stu-id="1c3ae-206">DES: encryption and decryption</span></span>
- <span data-ttu-id="1c3ae-207">Üçlü DES (3DES): şifreleme ve şifre çözme</span><span class="sxs-lookup"><span data-stu-id="1c3ae-207">Triple DES (3DES): encryption and decryption</span></span>
- <span data-ttu-id="1c3ae-208">AES: CBC modunda ve sayaç modunda 128, 192,256 bit anahtar boyutu, şifreleme ve şifre çözme.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-208">AES: 128-, 192-, 256-bit key size, encryption and decryption, in CBC mode and counter mode.</span></span>
- <span data-ttu-id="1c3ae-209">HMAC-MD5: kimlik doğrulaması ve karma hesaplama</span><span class="sxs-lookup"><span data-stu-id="1c3ae-209">HMAC-MD5: authentication and hash computation</span></span>
- <span data-ttu-id="1c3ae-210">HMAC-SHA: SHA1-96, SHA1-160, SHA2-256, SHA2-384, SHA2- 512, kimlik doğrulaması ve karma hesaplama</span><span class="sxs-lookup"><span data-stu-id="1c3ae-210">HMAC-SHA: SHA1-96, SHA1-160, SHA2-256, SHA2-384, SHA2- 512, authentication and hash computation</span></span>
- <span data-ttu-id="1c3ae-211">MD5: kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="1c3ae-211">MD5: authentication</span></span>
- <span data-ttu-id="1c3ae-212">Sözde rastgele İşlev (PRF): PRF_HMAC_SHA1 ve PRF_HMAC_SHA2-256</span><span class="sxs-lookup"><span data-stu-id="1c3ae-212">Pseudo-random Function (PRF): PRF_HMAC_SHA1 and PRF_HMAC_SHA2-256</span></span>
- <span data-ttu-id="1c3ae-213">RSA: 1024-, 2048-, 4096 bit RSA güç modulus işlemi</span><span class="sxs-lookup"><span data-stu-id="1c3ae-213">RSA: 1024-, 2048-, 4096-bit RSA power-modulus operation</span></span>
- <span data-ttu-id="1c3ae-214">SHA: SHA1 (96 ve 160 bit), SHA2 (256 bit, 384 bit, 512 bit) kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="1c3ae-214">SHA: SHA1 (96- and 160-bit), SHA2 (256bit, 384bit, 512bit) authentication</span></span>

<span data-ttu-id="1c3ae-215">Bu işlev, yukarıda listelenen şifreleme algoritmaları için yerleşik vektörlere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-215">This function has the built-in vectors for the crypto algorithms listed above.</span></span> <span data-ttu-id="1c3ae-216">Ancak yalnızca bu işleve geçirilen cipher_table *testlerini* içerir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-216">However it only tests the ones listed in the *cipher_table* passed into this function.</span></span> <span data-ttu-id="1c3ae-217">Örneğin TLS oturumunda yalnızca şifreleme TLS_RSA_WITH_AES_128_CBC_SHA için bu işlev RSA (1024-, 2048-, 4096 bit), AES-CBC (128 bit) ve SHA1 üzerinde kendi kendine test gerçekleştirecek.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-217">For example, for a TLS session uses only the ciphersuite TLS_RSA_WITH_AES_128_CBC_SHA, this function will perform self test on the RSA (1024-, 2048-, 4096-bit), AES-CBC (128-bit) and SHA1.</span></span>

### <a name="parameters"></a><span data-ttu-id="1c3ae-218">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1c3ae-218">Parameters</span></span>

- <span data-ttu-id="1c3ae-219">**crypto_table** TLS oturumu tarafından kullanılan şifreleme tablosu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-219">**crypto_table** Pointer to the crypto table being used by the TLS session.</span></span> <span data-ttu-id="1c3ae-220">Bu, crypto_table() çağrısına geçirilen **_nx_secure_tls_session_create aynıdır._**</span><span class="sxs-lookup"><span data-stu-id="1c3ae-220">This is the same crypto_table being passed into the **_nx_secure_tls_session_create()_** call.</span></span>
- <span data-ttu-id="1c3ae-221">**meta veriler** Şifreleme meta veri alanı için alan işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-221">**metadata** Pointer to space for cryptography metadata area.</span></span> <span data-ttu-id="1c3ae-222">.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-222">.</span></span>
- <span data-ttu-id="1c3ae-223">**metadata_size** Meta veri arabelleğinin boyutu.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-223">**metadata_size** Size of the metadata buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="1c3ae-224">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-224">Return Values</span></span>

- <span data-ttu-id="1c3ae-225">**NX_SECURE_TLS_SUCCESS** (0x00) Sağlanan şifreleme yöntemleri başarıyla test edildi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-225">**NX_SECURE_TLS_SUCCESS** (0x00) Successfully tested the crypto methods provided.</span></span>
- <span data-ttu-id="1c3ae-226">**NX_PTR_ERROR** (0x07) geçersiz şifreleme yöntemi yapısı</span><span class="sxs-lookup"><span data-stu-id="1c3ae-226">**NX_PTR_ERROR** (0x07) Invalid crypto method structure</span></span>
- <span data-ttu-id="1c3ae-227">**NX_NOT_SUCCESSFUL** (0x43) şifreleme self test başarısız oluyor.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-227">**NX_NOT_SUCCESSFUL** (0x43) Crypto self test fails.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1c3ae-228">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="1c3ae-228">Allowed From</span></span>

<span data-ttu-id="1c3ae-229">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="1c3ae-229">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="1c3ae-230">Örnek</span><span class="sxs-lookup"><span data-stu-id="1c3ae-230">Example</span></span>

```C
/* crypto_tls_ciphers is the cipher table for the TLS session. */
/* metadata_buffer is the memory area used by the cipher functions. */

/* The following function verifies the supplied ciphersuties using the built-in
   self test. */

if (nx_secure_crypto_table_self_test(&crypto_tls_ciphers, metadata_buffer,
    sizeof(metadata_buffer)))
{
    printf("Crypto self test failed!\r\n");
    exit(0);
}
else
{
    printf("Crypto self test succeed!\r\n");
}

/* Now the ciphersuites are successfully test, it can be used in
   nx_secure_tls_session_create() */
```

### <a name="see-also"></a><span data-ttu-id="1c3ae-231">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-231">See Also</span></span>

- <span data-ttu-id="1c3ae-232">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="1c3ae-232">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_module_hash_compute"></a><span data-ttu-id="1c3ae-233">nx_secure_module_hash_compute</span><span class="sxs-lookup"><span data-stu-id="1c3ae-233">nx_secure_module_hash_compute</span></span>

<span data-ttu-id="1c3ae-234">Kullanıcı tarafından sağlanan karma işlevi kullanarak karma değeri hesaplar</span><span class="sxs-lookup"><span data-stu-id="1c3ae-234">Computes hash value using user-supplied hash function</span></span>

### <a name="prototype"></a><span data-ttu-id="1c3ae-235">Prototype</span><span class="sxs-lookup"><span data-stu-id="1c3ae-235">Prototype</span></span>

```C
UINT nx_secure_module_hash_compute(
                      NX_CRYPTO_METHOD *hamc_ptr,
                      UINT start_address, UINT end_address,
                      UCHAR *key, UINT key_length,
                      VOID *metadata, UINT metadata_size,
                      UCHAR *output_buffer, UINT output_buffer_size,
                      UINT *actual_size);
```

### <a name="description"></a><span data-ttu-id="1c3ae-236">Description</span><span class="sxs-lookup"><span data-stu-id="1c3ae-236">Description</span></span>

<span data-ttu-id="1c3ae-237">Bu işlev, sağlanan HMAC şifre yöntemini ve anahtar dizesini kullanarak belirtilen bellek alanındaki veri akışının karma değerini hesaplar.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-237">This function computes the hash value of the data stream in the specified memory area, using supplied HMAC crypto method and the key string.</span></span> <span data-ttu-id="1c3ae-238">Modül karma işlem işlevi yalnızca NetX güvenli kitaplığı tanımlanmakta olan şu sembol ile derleniyorsa kullanılabilir: NX_SECURE_POWER_ON_SELF_TEST_MODULE_INTEGRITY_CHECK</span><span class="sxs-lookup"><span data-stu-id="1c3ae-238">The module hash compute function is available only if NetX Secure library is built with the following symbol being defined: NX_SECURE_POWER_ON_SELF_TEST_MODULE_INTEGRITY_CHECK</span></span>

### <a name="parameters"></a><span data-ttu-id="1c3ae-239">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1c3ae-239">Parameters</span></span>

- <span data-ttu-id="1c3ae-240">**hmac_ptr** Karma değer hesaplama için kullanılan HMAC şifre yöntemine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-240">**hmac_ptr** Pointer to the HMAC crypto method being used for the hash value computation.</span></span>
- <span data-ttu-id="1c3ae-241">**start_address** Veri arabelleğinin başlangıç adresi</span><span class="sxs-lookup"><span data-stu-id="1c3ae-241">**start_address** The starting address of the data buffer</span></span>
- <span data-ttu-id="1c3ae-242">**end_address** Veri arabelleğinin bitiş adresi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-242">**end_address** The ending address of the data buffer.</span></span> <span data-ttu-id="1c3ae-243">Karma hesaplamasının bu end_address verileri kapsamadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-243">Note that hash computation does not cover the data at this end_address.</span></span>
- <span data-ttu-id="1c3ae-244">**anahtar** HMAC hesaplamasında kullanılan anahtar dizesi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-244">**key** The key string being used in the HMAC computation.</span></span>
- <span data-ttu-id="1c3ae-245">**key_length** Anahtar dizesinin bayt cinsinden boyutu</span><span class="sxs-lookup"><span data-stu-id="1c3ae-245">**key_length** The size of the key string, in bytes</span></span>
- <span data-ttu-id="1c3ae-246">**meta veriler** HMAC algoritması tarafından kullanılan alana yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-246">**metadata** Pointer to space used by the HMAC algorithm.</span></span>
- <span data-ttu-id="1c3ae-247">**metadata_size** Meta veri arabelleğinin boyutu.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-247">**metadata_size** Size of the metadata buffer.</span></span>
- <span data-ttu-id="1c3ae-248">**output_buffer** Karma çıkışın depolandığı bellek konumu.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-248">**output_buffer** The memory location where the hash output is being stored at.</span></span>
- <span data-ttu-id="1c3ae-249">**output_buffer_size** Çıkış arabelleğinin bayt cinsinden kullanılabilir alanı</span><span class="sxs-lookup"><span data-stu-id="1c3ae-249">**output_buffer_size** The available space of the output buffer, in bytes</span></span>
- <span data-ttu-id="1c3ae-250">**actual_size** İşlev tarafından döndürülen, output_buffer yazılan gerçek bayt sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-250">**actual_size** Returned by the function indicating the actual number of bytes being written into the output_buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="1c3ae-251">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-251">Return Values</span></span>

- <span data-ttu-id="1c3ae-252">**0** Karma değeri başarıyla hesaplandı.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-252">**0** Successfully computed the hash value.</span></span>
- <span data-ttu-id="1c3ae-253">**1** Karma hesaplama başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-253">**1** The hash computation failed.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1c3ae-254">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="1c3ae-254">Allowed From</span></span>

<span data-ttu-id="1c3ae-255">Başlatma, İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="1c3ae-255">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="1c3ae-256">Örnek</span><span class="sxs-lookup"><span data-stu-id="1c3ae-256">Example</span></span>

```C
/* Define the HMAC SHA256 method */
NX_CRYPTO_METHOD hmac_sha256 =
{
    NX_CRYPTO_AUTHENTICATION_HMAC_SHA2_256,    /* HMAC SHA256 algorithm  */
    0,                                         /* Key size, not used     */
    0,                                         /* IV size, not used      */
    NX_CRYPTO_HMAC_SHA256_ICV_FULL_LEN_IN_BITS,/* Transmitted ICV size   */
    NX_CRYPTO_SHA2_BLOCK_SIZE_IN_BYTES,        /* Block size in bytes    */
    sizeof(NX_CRYPTO_SHA256_HMAC),             /* Metadata size in bytes */
    _nx_crypto_method_hmac_sha256_init,        /* HMAC SHA256 init       */
    _nx_crypto_method_hmac_sha256_cleanup,     /* HMAC SHA256 cleanup    */
    _nx_crypto_method_hmac_sha256_operation    /* HMAC SHA256 operation  */
};

/* Define the hash key being used. */
const CHAR hash_key = “my hash key”;

/* Define starting address. */
UINT starting_address = 0x10000;

/* Define the ending address.
   Note that the hash computation covers the memory location
   before the ending address. */
UINT ending_address = 0x11000;

/* Declare the output buffer. */
#define OUTPUT_BUFFER_SIZE
UCHAR output_buffer[OUTPUT_BUFFER_SIZE];

UINT actual_size;

/* Declare 1K bytes of metadata buffer area. */
UCHAR metadata_buffer[1024];

/* Compute the hash value of the data between 0x10000 – 0x10FFF */
nx_secure_module_hash_compute(&hmac_sha256,
                              starting_address, ending_address,
                              hash_key, strlen(hash_key),
                              metadata_buffer, sizeof(metadata_buffer),
                              output_buffer, OUTPUT_BUFFER_SIZE, &actual_size);

/* If this function returns “0”, the hash value has been computed and is stored
   in output_buffer. */
```

### <a name="see-also"></a><span data-ttu-id="1c3ae-257">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-257">See Also</span></span>

- <span data-ttu-id="1c3ae-258">nx_secure_crypto_method_self_test</span><span class="sxs-lookup"><span data-stu-id="1c3ae-258">nx_secure_crypto_method_self_test</span></span>

## <a name="nx_secure_tls_active_certificate_set"></a><span data-ttu-id="1c3ae-259">nx_secure_tls_active_certificate_set</span><span class="sxs-lookup"><span data-stu-id="1c3ae-259">nx_secure_tls_active_certificate_set</span></span>

<span data-ttu-id="1c3ae-260">NetX Secure TLS Oturumu için etkin kimlik sertifikasını ayarlama</span><span class="sxs-lookup"><span data-stu-id="1c3ae-260">Set the active identity certificate for a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="1c3ae-261">Prototype</span><span class="sxs-lookup"><span data-stu-id="1c3ae-261">Prototype</span></span>

```C
UINT  nx_secure_tls_active_certificate_set(
                   NX_SECURE_TLS_SESSION *tls_session,
                   NX_SECURE_X509_CERT *certificate);
```

### <a name="description"></a><span data-ttu-id="1c3ae-262">Description</span><span class="sxs-lookup"><span data-stu-id="1c3ae-262">Description</span></span>

<span data-ttu-id="1c3ae-263">Bu hizmetin bir oturum geri çağırma içinde çağrılma amacı vardır (bkz. nx_secure_tls_session_client_callback_set ve nx_secure_tls_session_server_callback_set).</span><span class="sxs-lookup"><span data-stu-id="1c3ae-263">This service is intended to be called from within a session callback (see nx_secure_tls_session_client_callback_set and nx_secure_tls_session_server_callback_set).</span></span> <span data-ttu-id="1c3ae-264">Daha önce başlatılmış bir NX_SECURE_X509_CERT ile çağrıldık, bu sertifika varsayılan kimlik sertifikası yerine kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-264">When called with a previously-initialized NX_SECURE_X509_CERT structure, that certificate will be used instead of the default identity certificate.</span></span> <span data-ttu-id="1c3ae-265">Çoğu durumda sertifikanın yerel depoya eklenmiş olması gerekir (bkz. nx_secure_tls_local_certificate_add) veya TLS el sıkışması başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-265">In most cases, the certificate must have been added to the local store (see nx_secure_tls_local_certificate_add) or the TLS handshake may fail.</span></span>

<span data-ttu-id="1c3ae-266">Bu hizmet, TLS'nin birden çok kimlik sertifikasını desteklemesine izin vermek için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-266">This service is intended to allow TLS to support multiple identity certificates.</span></span> <span data-ttu-id="1c3ae-267">Bu, sunucunun istemcinin giriş noktası bağlı olarak uzak istemciye sağılacak uygun bir sertifika seçerek birden çok ağ adresine hizmet sağlayan bir TLS sunucusu için yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-267">This is useful for a TLS server that services multiple network addresses so the server can pick an appropriate certificate to provide to the remote client depending on the client's entrypoint.</span></span> <span data-ttu-id="1c3ae-268">Bir TLS istemcisi için bu yordam, sunucu TLS el sıkışması içinde kendisini belirledikten sonra çalışma zamanında uzak bir sunucuya gönderilen sertifikayı değiştirmek için kullanılabilir (bu, TLS sunucusunun kullanım örneğinden daha nadirdir).</span><span class="sxs-lookup"><span data-stu-id="1c3ae-268">For a TLS client, this routine may be used to change the certificate sent to a remote server at runtime after the server has identified itself in the TLS handshake (this is more rare than the TLS server use-case).</span></span>

<span data-ttu-id="1c3ae-269">Birden çok sertifikanın aynı X.509 ayırt edici adını paylaşması durumunda, sertifikaların sertifikadan ayrı bir sayısal tanımlayıcıyı tanıtan nx_secure_tls_server_certificate_add kullanılarak ekleniyor olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-269">In the case where multiple certificates may share the same X.509 distinguished name, certificates will need to be added using nx_secure_tls_server_certificate_add, which introduces a numeric identifier separate from the certificate.</span></span>

### <a name="parameters"></a><span data-ttu-id="1c3ae-270">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1c3ae-270">Parameters</span></span>

- <span data-ttu-id="1c3ae-271">**session_ptr** Oturum geri çağırmaya geçirilen BIR TLS Oturumu örneğinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-271">**session_ptr** Pointer to a TLS Session instance passed into the session callback.</span></span>
- <span data-ttu-id="1c3ae-272">**sertifika** Geçerli oturum için kullanılacak, başlatılan bir X.509 sertifikasının işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-272">**certificate** Pointer to an initialized X.509 certificate that is to be used for the current session.</span></span>

### <a name="return-values"></a><span data-ttu-id="1c3ae-273">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-273">Return Values</span></span>

- <span data-ttu-id="1c3ae-274">**NX_SUCCESS** (0x00) Sertifikanın oturuma başarıyla ataması.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-274">**NX_SUCCESS** (0x00) Successful assignment of certificate to session.</span></span>
- <span data-ttu-id="1c3ae-275">**NX_PTR_ERROR** (0x07) Geçersiz TLS oturumu veya sertifika işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-275">**NX_PTR_ERROR** (0x07) Invalid TLS session or certificate pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1c3ae-276">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="1c3ae-276">Allowed From</span></span>

<span data-ttu-id="1c3ae-277">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="1c3ae-277">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1c3ae-278">Örnek</span><span class="sxs-lookup"><span data-stu-id="1c3ae-278">Example</span></span>

```C
#define TLS_SNI_SERVER_NAME “www.example.com”
#define TLS_DEFAULT_SERVER_CERT_ID 2
#define TLS_EXAMPLE_CERT_ID 3


/* Callback for ClientHello extensions processing. */
static ULONG tls_server_callback(NX_SECURE_TLS_SESSION *tls_session,
                                 NX_SECURE_TLS_HELLO_EXTENSION *extensions,
                                 UINT num_extensions)
{
NX_SECURE_X509_DNS_NAME dns_name;
INT compare_value;
UINT status;
NX_SECURE_X509_CERT *cert_ptr;

    /* Grab a pointer to our default certificate in case the SNI extension is not
       available or the specified server name is unknown. */
    nx_secure_tls_server_certificate_find(tls_session, &cert_ptr,
                                     TLS_DEFAULT_SERVER_CERT_ID);


    /* Process Server Name Indication extension. */
    status = _nx_secure_tls_session_sni_extension_parse(tls_session, extensions,
                                                    num_extensions, &dns_name);

    /* If no extension found, that is OK. Use default certificate. */
    if(status == NX_SUCCESS)
    {
          /* SNI extension found, select an active certificate based on the server
             name. */

          /* Make sure our SNI name matches. */
          compare_value = memcmp(dns_name.nx_secure_x509_dns_name,
                                TLS_SNI_SERVER_NAME, strlen(TLS_SNI_SERVER_NAME));

          if(compare_value == 0 && dns_name.nx_secure_x509_dns_name_length !=
             strlen(TLS_SNI_SERVER_NAME))
          {
             /* Found a match, find the certificate we want to use. */
             _nx_secure_tls_server_certificate_find(tls_session, &cert_ptr,
                                                      TLS_EXAMPLE_CERT_ID);
          }
          else
          {
             /* No matching server name found. The application may choose to simply
                provide the default certificate (and probably resulting in an error
                in the remote client) or returning an error here to end the
                handshake. A user-defined non-zero error code will be sufficient –
                the error code will abort the TLS handshake and be returned to the
                caller that started the server. */
                return(0x500);
          }
      }
      else
      {
      }
      /* Set the certificate we want to use. */
      nx_secure_tls_active_certificate_set(tls_session, cert_ptr);

      /* Return success to continue TLS handshake. */
      return(NX_SUCCESS);
}

/* Sockets, sessions, certificates defined in global static space to preserve
   application stack. */
NX_SECURE_TLS_SESSION server_tls_session;

/* Application where TLS session is started. */
void main()
{
    /* Create a TLS session for our socket. Ciphers and metadata defined
       elsewhere. See nx_secure_tls_session_create reference for more
       information. */
    status =  nx_secure_tls_session_create(&server_tls_session,
                                           &nx_crypto_tls_ciphers,
                                           server_crypto_metadata,
                                           sizeof(server_crypto_metadata));

    /* Check for error.  */
    if(status)
    {
        printf("Error in function nx_secure_tls_session_create: 0x%x\n", status);
    }

    /* Setup our packet reassembly buffer. See
       nx_secure_tls_session_packet_buffer_set for more information. */
    nx_secure_tls_session_packet_buffer_set(&server_tls_session,
                                      server_packet_buffer,
                                      sizeof(server_packet_buffer));


    /* Set callback for server TLS extension handling. */
    _nx_secure_tls_session_server_callback_set(&server_tls_session,
                                              tls_server_callback);

    /* Initialize our certificates – certificate data defined elsewhere. See
       section “Importing X.509 Certificates into NetX Secure” for more
       information. */
    nx_secure_x509_certificate_initialize(&default_certificate,
                                      default_cert_der,
                                      default _cert_der_len, NX_NULL, 0,
                                      default_cert_key_der,
                                      default_cert_key_der_len,
                                      NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add the certificate to the local store using a numeric ID. */
    nx_secure_tls_server_certificate_add(&server_tls_session,
                                         &default_certificate,
                                         TLS_DEFAULT_SERVER_CERT_ID);

    /* Alternative identity certificate, needs to have a private key! */
    nx_secure_x509_certificate_initialize(&example_certificate,
                                      example_cert_der,
                                      example cert_der_len, NX_NULL, 0,
                                      example_cert_key_der,
                                      example_cert_key_der_len,
                                      NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add the certificate to the local store using a numeric ID. */
    nx_secure_tls_server_certificate_add(&server_tls_session,
                                         &example_certificate,
                                         TLS_EXAMPLE_CERT_ID);

    /* Now we can start the TLS session as normal. */
       …
}
```

### <a name="see-also"></a><span data-ttu-id="1c3ae-279">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-279">See Also</span></span>

- <span data-ttu-id="1c3ae-280">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="1c3ae-280">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="1c3ae-281">nx_secure_tls_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="1c3ae-281">nx_secure_tls_local_certificate_add</span></span>
- <span data-ttu-id="1c3ae-282">nx_secure_tls_session_client_callback_set</span><span class="sxs-lookup"><span data-stu-id="1c3ae-282">nx_secure_tls_session_client_callback_set</span></span>
- <span data-ttu-id="1c3ae-283">nx_secure_tls_session_server_callback_set</span><span class="sxs-lookup"><span data-stu-id="1c3ae-283">nx_secure_tls_session_server_callback_set</span></span>
- <span data-ttu-id="1c3ae-284">nx_secure_tls_server_certificate_add</span><span class="sxs-lookup"><span data-stu-id="1c3ae-284">nx_secure_tls_server_certificate_add</span></span>
- <span data-ttu-id="1c3ae-285">nx_secure_tls_server_certificate_find</span><span class="sxs-lookup"><span data-stu-id="1c3ae-285">nx_secure_tls_server_certificate_find</span></span>
- <span data-ttu-id="1c3ae-286">nx_secure_tls_server_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="1c3ae-286">nx_secure_tls_server_certificate_remove</span></span>

## <a name="nx_secure_tls_client_psk_set"></a><span data-ttu-id="1c3ae-287">nx_secure_tls_client_psk_set</span><span class="sxs-lookup"><span data-stu-id="1c3ae-287">nx_secure_tls_client_psk_set</span></span>

<span data-ttu-id="1c3ae-288">NetX güvenli TLS Istemci oturumu için önceden paylaşılan anahtar ayarlama</span><span class="sxs-lookup"><span data-stu-id="1c3ae-288">Set a Pre-Shared Key for a NetX Secure TLS Client Session</span></span>

### <a name="prototype"></a><span data-ttu-id="1c3ae-289">Prototype</span><span class="sxs-lookup"><span data-stu-id="1c3ae-289">Prototype</span></span>

```C
UINT  nx_secure_tls_client_psk_set(NX_SECURE_TLS_SESSION *session_ptr,
                              UCHAR *pre_shared_key, UINT psk_length,
                              UCHAR *psk_identity, UINT identity_length,
                              UCHAR *hint, UINT hint_length);
```

### <a name="description"></a><span data-ttu-id="1c3ae-290">Description</span><span class="sxs-lookup"><span data-stu-id="1c3ae-290">Description</span></span>

<span data-ttu-id="1c3ae-291">Bu hizmet, bir TLS oturum denetim bloğuna önceden paylaşılan anahtar (PSK), kimlik dizesi ve kimlik ipucu ekler ve bu PSK 'yi sonraki TLS Istemci bağlantılarında kullanılacak şekilde ayarlar.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-291">This service adds a Pre-Shared Key (PSK), its identity string, and an identity hint to a TLS Session control block, and sets that PSK to be used in subsequent TLS Client connections.</span></span> <span data-ttu-id="1c3ae-292">PSK ciphersuites etkin ve kullanıldığında, bir dijital sertifika yerine PSK kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-292">The PSK is used in place of a digital certificate when PSK ciphersuites are enabled and used.</span></span>

<span data-ttu-id="1c3ae-293">Bu durumda, PSK, TLS Istemcisinin iletişim kurmasını istediği belirli bir uzak TLS sunucusuyla ilişkilendirilir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-293">In this case, the PSK is associated with a specific remote TLS Server with which the TLS Client wishes to communicate.</span></span> <span data-ttu-id="1c3ae-294">Bu API aracılığıyla ayarlanan PSK, sonraki TLS el sıkışması sırasında uzak TLS sunucu konağına sunulacaktır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-294">The PSK set through this API will be provided to the remote TLS Server host during the next TLS handshake.</span></span>

### <a name="parameters"></a><span data-ttu-id="1c3ae-295">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1c3ae-295">Parameters</span></span>

- <span data-ttu-id="1c3ae-296">**session_ptr** Daha önce oluşturulmuş bir TLS oturum örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-296">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="1c3ae-297">**pre_shared_key** Gerçek PSK değeri.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-297">**pre_shared_key** The actual PSK value.</span></span>
- <span data-ttu-id="1c3ae-298">**psk_length** PSK değeri uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-298">**psk_length** The length of the PSK value.</span></span>
- <span data-ttu-id="1c3ae-299">**psk_identity** Bu PSK değerini tanımlamak için kullanılan dize.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-299">**psk_identity** A string used to identify this PSK value.</span></span>
- <span data-ttu-id="1c3ae-300">**identity_length** PSK kimliğinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-300">**identity_length** The length of the PSK identity.</span></span>
- <span data-ttu-id="1c3ae-301">**İpucu** Bir TLS sunucusunda hangi sayıda PSKs arasından seçim yapmak gerektiğini göstermek için kullanılan dize.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-301">**hint** A string used to indicate which group of PSKs to choose from on a TLS server.</span></span>
- <span data-ttu-id="1c3ae-302">**hint_length** İpucu dizesinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-302">**hint_length** The length of the hint string.</span></span>

### <a name="return-values"></a><span data-ttu-id="1c3ae-303">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-303">Return Values</span></span>

- <span data-ttu-id="1c3ae-304">**NX_SUCCESS** (0x00) PSK 'nin başarılı bir şekilde eklenmesi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-304">**NX_SUCCESS** (0x00) Successful addition of PSK.</span></span>
- <span data-ttu-id="1c3ae-305">**NX_PTR_ERROR** (0x07) Geçersiz TLS oturum işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-305">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>
- <span data-ttu-id="1c3ae-306">**NX_SECURE_TLS_NO_MORE_PSK_SPACE** (0x125) Başka bir PSK ek olamaz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-306">**NX_SECURE_TLS_NO_MORE_PSK_SPACE** (0x125) Cannot add another PSK.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1c3ae-307">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="1c3ae-307">Allowed From</span></span>

<span data-ttu-id="1c3ae-308">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="1c3ae-308">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1c3ae-309">Örnek</span><span class="sxs-lookup"><span data-stu-id="1c3ae-309">Example</span></span>

```C
/* PSK value.  */
UCHAR psk[] = { 0x1a, 0x2b, 0x3c, 0x4d };

/* Add PSK to TLS session.  */
status =  nx_secure_tls_client_psk_set(&tls_session, psk, sizeof(psk), “psk_1”, 4,
“Client_identity”, 15);


/* If status is NX_SUCCESS the PSK was successfully added.  */
```

### <a name="see-also"></a><span data-ttu-id="1c3ae-310">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-310">See Also</span></span>

- <span data-ttu-id="1c3ae-311">nx_secure_tls_psk_add</span><span class="sxs-lookup"><span data-stu-id="1c3ae-311">nx_secure_tls_psk_add</span></span>
- <span data-ttu-id="1c3ae-312">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="1c3ae-312">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="1c3ae-313">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="1c3ae-313">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="1c3ae-314">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="1c3ae-314">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="1c3ae-315">nx_secure_tls_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="1c3ae-315">nx_secure_tls_local_certificate_add</span></span>

## <a name="nx_secure_tls_initialize"></a><span data-ttu-id="1c3ae-316">nx_secure_tls_initialize</span><span class="sxs-lookup"><span data-stu-id="1c3ae-316">nx_secure_tls_initialize</span></span>

<span data-ttu-id="1c3ae-317">NetX Secure TLS modülünü başlatıyor</span><span class="sxs-lookup"><span data-stu-id="1c3ae-317">Initializes the NetX Secure TLS module</span></span>

### <a name="prototype"></a><span data-ttu-id="1c3ae-318">Prototype</span><span class="sxs-lookup"><span data-stu-id="1c3ae-318">Prototype</span></span>

```C
VOID nx_secure_tls_initialize(VOID);
```

### <a name="description"></a><span data-ttu-id="1c3ae-319">Description</span><span class="sxs-lookup"><span data-stu-id="1c3ae-319">Description</span></span>

<span data-ttu-id="1c3ae-320">Bu hizmet NetX Secure TLS modülünü başlatıyor.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-320">This service initializes the NetX Secure TLS module.</span></span> <span data-ttu-id="1c3ae-321">Diğer NetX Güvenli hizmetlere erişilmeden önce çağrılmaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-321">It must be called before other NetX Secure services can be accessed.</span></span>

### <a name="parameters"></a><span data-ttu-id="1c3ae-322">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1c3ae-322">Parameters</span></span>

<span data-ttu-id="1c3ae-323">Hiçbiri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-323">None</span></span>

### <a name="return-values"></a><span data-ttu-id="1c3ae-324">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-324">Return Values</span></span>

<span data-ttu-id="1c3ae-325">Hiçbiri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-325">None</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1c3ae-326">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="1c3ae-326">Allowed From</span></span>

<span data-ttu-id="1c3ae-327">Başlatma, İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="1c3ae-327">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="1c3ae-328">Örnek</span><span class="sxs-lookup"><span data-stu-id="1c3ae-328">Example</span></span>

```C
/* Initializes the TLS module. */
Nx_secure_tls_initialize();
```

### <a name="see-also"></a><span data-ttu-id="1c3ae-329">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-329">See Also</span></span>

- <span data-ttu-id="1c3ae-330">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="1c3ae-330">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_local_certificate_add"></a><span data-ttu-id="1c3ae-331">nx_secure_tls_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="1c3ae-331">nx_secure_tls_local_certificate_add</span></span>

<span data-ttu-id="1c3ae-332">NetX Secure TLS Oturumuna yerel sertifika ekleme</span><span class="sxs-lookup"><span data-stu-id="1c3ae-332">Add a local certificate to NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="1c3ae-333">Prototype</span><span class="sxs-lookup"><span data-stu-id="1c3ae-333">Prototype</span></span>

```C
UINT  nx_secure_tls_local_certificate_add(
              NX_SECURE_TLS_SESSION *session_ptr,
              NX_SECURE_X509_CERT *certificate_ptr);
```

### <a name="description"></a><span data-ttu-id="1c3ae-334">Description</span><span class="sxs-lookup"><span data-stu-id="1c3ae-334">Description</span></span>

<span data-ttu-id="1c3ae-335">Bu hizmet, bir TLS NX_SECURE_X509_CERT yerel deposuna başlatılmış bir uygulama yapısı örneği ekler.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-335">This service adds an initialized NX_SECURE_X509_CERT structure instance to the local store of a TLS session.</span></span> <span data-ttu-id="1c3ae-336">Bu sertifika, TLS yığını tarafından TLS el sıkışması sırasında cihazı tanımlamak için (nx_secure_x509_certificate_initialize kullanılarak sertifika yapısının başlatılmış olması sırasında kimlik sertifikası olarak işaretlenmişse) veya TLS el sıkışması sırasında uzak ana bilgisayara sağlanan bir sertifika zincirinin parçası olarak bir sertifikayı verir olarak kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-336">This certificate may used by the TLS stack to identify the device during the TLS handshake (if it was marked as an identity certificate during initialization of the certificate structure using nx_secure_x509_certificate_initialize), or as an issuer as part of a certificate chain provided to the remote host during the TLS handshake.</span></span>

<span data-ttu-id="1c3ae-337">Aynı Ortak Ad ile birden çok yerel sertifika gerekirse, sertifikalar nx_secure_tls_server_certificate_add hizmeti kullanılarak eklenebilir (aşağıdaki uyarıya bakın). </span><span class="sxs-lookup"><span data-stu-id="1c3ae-337">If multiple local certificates with the same Common Name are needed, certificates may be added using the *nx_secure_tls_server_certificate_add* service (see warning below).</span></span>

<span data-ttu-id="1c3ae-338">TLS sunucu modu için bir sertifika **gereklidir** .</span><span class="sxs-lookup"><span data-stu-id="1c3ae-338">A certificate is **required** for TLS Server mode.</span></span>

<span data-ttu-id="1c3ae-339">Bir sertifika, TLS Istemci modu için *isteğe bağlıdır* .</span><span class="sxs-lookup"><span data-stu-id="1c3ae-339">A certificate is *optional* for TLS Client mode.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1c3ae-340">*Bu API, nx_secure_tls_server_certificate_add kullanırken aynı TLS oturumuyla kullanılmamalıdır. Sunucu sertifikası API 'SI her sertifika için benzersiz bir sayısal tanımlayıcı kullanır ve X. 509.440 ortak adına göre dizinleri nx_secure_tls_local_certificate_add. Yerel Sertifika Hizmetleri, yalnızca tek bir kimlik sertifikası kullanan uygulamalar için sayısal tanımlayıcıya uygun bir alternatif sağlar: ortak adı kullanarak, uygulamanın sayısal tanımlayıcıları izlememek zorunda olmaması gerekir.*</span><span class="sxs-lookup"><span data-stu-id="1c3ae-340">*This API should not be used with the same TLS session when using nx_secure_tls_server_certificate_add. The server certificate API uses a unique numeric identifier for each certificate, and nx_secure_tls_local_certificate_add indexes based on the X.509 Common Name. The local certificate services provide a convenient alternative to the numeric identifier for applications that use only a single identity certificate – by using the Common Name, the application need not keep track of numeric identifiers.*</span></span>

### <a name="parameters"></a><span data-ttu-id="1c3ae-341">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1c3ae-341">Parameters</span></span>

- <span data-ttu-id="1c3ae-342">**session_ptr** Daha önce oluşturulmuş bir TLS oturum örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-342">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="1c3ae-343">**certificate_ptr** Başlatılmış bir TLS sertifikası örneğinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-343">**certificate_ptr** Pointer to an initialized TLS Certificate instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="1c3ae-344">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-344">Return Values</span></span>

- <span data-ttu-id="1c3ae-345">Sertifikanın başarılı bir şekilde eklenmesi **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="1c3ae-345">**NX_SUCCESS** (0x00) Successful addition of certificate.</span></span>
- <span data-ttu-id="1c3ae-346">**NX_INVALID_PARAMETERS** (0x4D) geçersiz veya yinelenen bir sertifika eklemeye çalıştı.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-346">**NX_INVALID_PARAMETERS** (0x4D) Tried to add an invalid or duplicate certificate.</span></span>
- <span data-ttu-id="1c3ae-347">**NX_PTR_ERROR** (0x07) geçersiz TLS oturumu veya sertifika işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-347">**NX_PTR_ERROR** (0x07) Invalid TLS session or certificate pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1c3ae-348">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="1c3ae-348">Allowed From</span></span>

<span data-ttu-id="1c3ae-349">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="1c3ae-349">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1c3ae-350">Örnek</span><span class="sxs-lookup"><span data-stu-id="1c3ae-350">Example</span></span>

```C
/* Initialize certificate structure. */
status =  nx_secure_x509_certificate_initialize(&certificate, certificate_data,
500, private_key, 64);

/* Add certificate to TLS session.  */
status =  nx_secure_tls_local_certificate_add(&tls_session, &certificate);


/* If status is NX_SUCCESS the certificate was successfully added.  */
```

### <a name="see-also"></a><span data-ttu-id="1c3ae-351">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-351">See Also</span></span>

- <span data-ttu-id="1c3ae-352">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="1c3ae-352">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="1c3ae-353">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="1c3ae-353">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="1c3ae-354">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="1c3ae-354">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="1c3ae-355">nx_secure_tls_local_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="1c3ae-355">nx_secure_tls_local_certificate_remove</span></span>
- <span data-ttu-id="1c3ae-356">nx_secure_tls_local_certificate_find</span><span class="sxs-lookup"><span data-stu-id="1c3ae-356">nx_secure_tls_local_certificate_find</span></span>

## <a name="nx_secure_tls_local_certificate_find"></a><span data-ttu-id="1c3ae-357">nx_secure_tls_local_certificate_find</span><span class="sxs-lookup"><span data-stu-id="1c3ae-357">nx_secure_tls_local_certificate_find</span></span>

<span data-ttu-id="1c3ae-358">Ortak ad ile bir NetX güvenli TLS oturumunda yerel bir sertifika bulun</span><span class="sxs-lookup"><span data-stu-id="1c3ae-358">Find a local certificate in a NetX Secure TLS Session by Common Name</span></span>

### <a name="prototype"></a><span data-ttu-id="1c3ae-359">Prototype</span><span class="sxs-lookup"><span data-stu-id="1c3ae-359">Prototype</span></span>

```C
UINT  nx_secure_tls_local_certificate_find(NX_SECURE_TLS_SESSION
                        *session_ptr, NX_SECURE_X509_CERT
                        **certificate, UCHAR *common_name, UINT
                        name_length);
```

### <a name="description"></a><span data-ttu-id="1c3ae-360">Description</span><span class="sxs-lookup"><span data-stu-id="1c3ae-360">Description</span></span>

<span data-ttu-id="1c3ae-361">Bu hizmet, bir TLS oturumunun yerel cihaz sertifika deposundaki bir sertifikayı bulur ve depodaki NX_SECURE_X509_CERT yapısına bir işaretçi döndürür.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-361">This service finds a certificate in the local device certificate store of a TLS session and returns a pointer to the NX_SECURE_X509_CERT structure in the store.</span></span> <span data-ttu-id="1c3ae-362">Common_name parametresi ve uzunluğu (name_length), sertifikanın X. 509.440 konusunun ortak ad alanıyla eşleşen sertifikayı tanımlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-362">The common_name parameter and it's length (name_length) are used to identify the certificate in the store by matching the certificate's X.509 Subject Common Name field.</span></span>

<span data-ttu-id="1c3ae-363">Aynı ortak ada sahip birden fazla sertifika varsa, yalnızca ilki döndürülür – bunun yerine *nx_secure_tls_server_certificate_find* kullanın.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-363">If more than one certificate with the same Common Name is present, only the first one will be returned – use *nx_secure_tls_server_certificate_find* instead.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1c3ae-364">*Bu API, uygulama kullanılırken aynı TLS oturumuyla nx_secure_tls_server_certificate_add. Sunucu sertifikası API'si her sertifika için benzersiz bir sayısal tanımlayıcı kullanır nx_secure_tls_local_certificate_add X.509 Ortak Adını temel alan dizinleri kullanır. Yerel sertifika hizmetleri, yalnızca tek bir kimlik sertifikası kullanan uygulamalar için sayısal tanımlayıcıya uygun bir alternatif sağlar. Ortak Ad'ı kullanarak uygulamanın sayısal tanımlayıcıları izlemesi gerekli değildir.*</span><span class="sxs-lookup"><span data-stu-id="1c3ae-364">*This API should not be used with the same TLS session when using nx_secure_tls_server_certificate_add. The server certificate API uses a unique numeric identifier for each certificate, and nx_secure_tls_local_certificate_add indexes based on the X.509 Common Name. The local certificate services provide a convenient alternative to the numeric identifier for applications that use only a single identity certificate – by using the Common Name, the application need not keep track of numeric identifiers.*</span></span>

### <a name="parameters"></a><span data-ttu-id="1c3ae-365">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1c3ae-365">Parameters</span></span>

- <span data-ttu-id="1c3ae-366">**session_ptr** Daha önce oluşturulmuş bir TLS Oturumu örneğinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-366">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="1c3ae-367">**sertifika** İşaretçiyi, eşlene sertifikaya geri dön.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-367">**certificate** Return Pointer to matched certificate.</span></span>
- <span data-ttu-id="1c3ae-368">**common_name** Eşecek Ortak Ad dizesi (DNS adı).</span><span class="sxs-lookup"><span data-stu-id="1c3ae-368">**common_name** Common Name string to match (DNS name).</span></span>
- <span data-ttu-id="1c3ae-369">**name_length** Dize common_name uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-369">**name_length** Length of common_name string data.</span></span>

### <a name="return-values"></a><span data-ttu-id="1c3ae-370">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-370">Return Values</span></span>

- <span data-ttu-id="1c3ae-371">**NX_SUCCESS** (0x00) Sertifika bulundu ve işaretçi "certificate" parametresinde döndürüldü.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-371">**NX_SUCCESS** (0x00) Certificate was found and pointer returned in "certificate" parameter.</span></span>
- <span data-ttu-id="1c3ae-372">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) Sağlanan Ortak Ad ile sertifika bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-372">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) No certificate with the supplied Common Name was found.</span></span>
- <span data-ttu-id="1c3ae-373">**NX_PTR_ERROR** (0x07) Geçersiz TLS oturumu, sertifika işaretçisi veya ortak ad dizesi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-373">**NX_PTR_ERROR** (0x07) Invalid TLS session, certificate pointer, or common name string.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1c3ae-374">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="1c3ae-374">Allowed From</span></span>

<span data-ttu-id="1c3ae-375">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="1c3ae-375">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1c3ae-376">Örnek</span><span class="sxs-lookup"><span data-stu-id="1c3ae-376">Example</span></span>

```C
NX_SECURE_X509_CERT *certificate_ptr;

/* Initialize certificate structure. */
status =  nx_secure_x509_certificate_initialize(&certificate, certificate_data,
500, private_key, 64);

/* Add certificate to TLS session.  */
status =  nx_secure_tls_local_certificate_add(&tls_session, &certificate);


/* If status is NX_SUCCESS the certificate was successfully added.  */

status = nx_secure_tls_local_certificate_find(&tls_session, &certificate_ptr,
                                      “common name”, strlen(“common name”));

/* If status is NX_SUCCESS the variable “certificate_ptr” points to a certificate
   structure containing a certificate with the Common Name “common name”. */
```

### <a name="see-also"></a><span data-ttu-id="1c3ae-377">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-377">See Also</span></span>

- <span data-ttu-id="1c3ae-378">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="1c3ae-378">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="1c3ae-379">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="1c3ae-379">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="1c3ae-380">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="1c3ae-380">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="1c3ae-381">nx_secure_tls_local_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="1c3ae-381">nx_secure_tls_local_certificate_remove</span></span>
- <span data-ttu-id="1c3ae-382">nx_secure_tls_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="1c3ae-382">nx_secure_tls_local_certificate_add</span></span>

## <a name="nx_secure_tls_local_certificate_remove"></a><span data-ttu-id="1c3ae-383">nx_secure_tls_local_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="1c3ae-383">nx_secure_tls_local_certificate_remove</span></span>

<span data-ttu-id="1c3ae-384">NetX Secure TLS Oturumundan yerel sertifikayı kaldırma</span><span class="sxs-lookup"><span data-stu-id="1c3ae-384">Remove local certificate from NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="1c3ae-385">Prototype</span><span class="sxs-lookup"><span data-stu-id="1c3ae-385">Prototype</span></span>

```C
UINT  nx_secure_tls_local_certificate_remove(NX_SECURE_TLS_SESSION
                  *session_ptr, UCHAR *common_name, UINT
                  common_name_length);
```

### <a name="description"></a><span data-ttu-id="1c3ae-386">Description</span><span class="sxs-lookup"><span data-stu-id="1c3ae-386">Description</span></span>

<span data-ttu-id="1c3ae-387">Bu hizmet, sertifikadaki Ortak Ad alanına anahtarlanan bir TLS oturumundan yerel sertifika örneğini kaldırır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-387">This service removes a local certificate instance from a TLS session, keyed on the Common Name field in the certificate.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1c3ae-388">*Bu API, uygulama kullanılırken aynı TLS oturumuyla nx_secure_tls_server_certificate_add. Sunucu sertifikası API'si her sertifika için benzersiz bir sayısal tanımlayıcı kullanır nx_secure_tls_local_certificate_add X.509 Ortak Adını temel alan dizinleri kullanır. Yerel sertifika hizmetleri, yalnızca tek bir kimlik sertifikası kullanan uygulamalar için sayısal tanımlayıcıya uygun bir alternatif sağlar. Ortak Ad'ı kullanarak uygulamanın sayısal tanımlayıcıları izlemesi gerekli değildir.*</span><span class="sxs-lookup"><span data-stu-id="1c3ae-388">*This API should not be used with the same TLS session when using nx_secure_tls_server_certificate_add. The server certificate API uses a unique numeric identifier for each certificate, and nx_secure_tls_local_certificate_add indexes based on the X.509 Common Name. The local certificate services provide a convenient alternative to the numeric identifier for applications that use only a single identity certificate – by using the Common Name, the application need not keep track of numeric identifiers.*</span></span>

### <a name="parameters"></a><span data-ttu-id="1c3ae-389">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1c3ae-389">Parameters</span></span>

- <span data-ttu-id="1c3ae-390">**session_ptr** Daha önce oluşturulmuş bir TLS oturum örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-390">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="1c3ae-391">**common_name** Kaldırılacak sertifikanın ortak ad değeri.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-391">**common_name** The Common Name value of the certificate to be removed.</span></span>
- <span data-ttu-id="1c3ae-392">**common_name_length** Ortak ad dizesinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-392">**common_name_length** The length of the Common Name string.</span></span>

### <a name="return-values"></a><span data-ttu-id="1c3ae-393">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-393">Return Values</span></span>

- <span data-ttu-id="1c3ae-394">Sertifikanın başarılı bir şekilde eklenmesi **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="1c3ae-394">**NX_SUCCESS** (0x00) Successful addition of certificate.</span></span>
- <span data-ttu-id="1c3ae-395">**NX_PTR_ERROR** (0x07) geçersiz TLS oturum işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-395">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>
- <span data-ttu-id="1c3ae-396">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) sertifikası bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-396">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) Certificate was not found.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1c3ae-397">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="1c3ae-397">Allowed From</span></span>

<span data-ttu-id="1c3ae-398">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="1c3ae-398">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1c3ae-399">Örnek</span><span class="sxs-lookup"><span data-stu-id="1c3ae-399">Example</span></span>

```C
/* Add certificate to TLS session.  */
status =  nx_secure_tls_local_certificate_remove(&tls_session,
                                                “www.example.com”, 15);


/* If status is NX_SUCCESS the certificate was successfully removed.  */
```

### <a name="see-also"></a><span data-ttu-id="1c3ae-400">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-400">See Also</span></span>

- <span data-ttu-id="1c3ae-401">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="1c3ae-401">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="1c3ae-402">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="1c3ae-402">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="1c3ae-403">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="1c3ae-403">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="1c3ae-404">nx_secure_tls_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="1c3ae-404">nx_secure_tls_local_certificate_add</span></span>

## <a name="nx_secure_tls_metadata_size_calculate"></a><span data-ttu-id="1c3ae-405">nx_secure_tls_metadata_size_calculate</span><span class="sxs-lookup"><span data-stu-id="1c3ae-405">nx_secure_tls_metadata_size_calculate</span></span>

<span data-ttu-id="1c3ae-406">NetX güvenli TLS oturumunun şifreleme meta verilerinin boyutunu hesaplama</span><span class="sxs-lookup"><span data-stu-id="1c3ae-406">Calculate size of cryptographic metadata for a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="1c3ae-407">Prototype</span><span class="sxs-lookup"><span data-stu-id="1c3ae-407">Prototype</span></span>

```C
UINT  nx_secure_tls_metadata_size_calculate(
                        const NX_SECURE_TLS_CRYPTO *crypto_table,
                        ULONG *metadata_size);
```

### <a name="description"></a><span data-ttu-id="1c3ae-408">Description</span><span class="sxs-lookup"><span data-stu-id="1c3ae-408">Description</span></span>

<span data-ttu-id="1c3ae-409">Bu hizmet, belirli bir TLS oturumu ve TLS şifreleme tablosu için gereken şifreleme meta verilerinin boyutunu hesaplar ve döndürür (şifreleme şifresi tablosu hakkında daha fazla bilgi için "şifreleme yöntemleriyle TLS başlatılıyor" bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-409">This service calculates and returns the size of the cryptographic metadata needed for a particular TLS session and TLS cryptography table (see the section "Initializing TLS with Cryptographic Methods" for more information on the cryptographic cipher table).</span></span>

<span data-ttu-id="1c3ae-410">Bu hizmet, nx_secure_tls_session_create iletilen meta veri arabelleğinin boyutunu hesaplamak için istenen şifreleme tablosuyla çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-410">This service should be called with the desired cryptographic table to calculate the size of the metadata buffer passed into nx_secure_tls_session_create.</span></span>

### <a name="parameters"></a><span data-ttu-id="1c3ae-411">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1c3ae-411">Parameters</span></span>

- <span data-ttu-id="1c3ae-412">**crypto_table** Tüm NetX güvenli TLS şifreleme tablosuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-412">**crypto_table** Pointer to a complete NetX Secure TLS cryptography table.</span></span>
- <span data-ttu-id="1c3ae-413">**metadata_size** Bayt cinsinden boyut hesaplamasının çıktısı.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-413">**metadata_size** The output of the size calculation in bytes.</span></span>

### <a name="return-values"></a><span data-ttu-id="1c3ae-414">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-414">Return Values</span></span>

- <span data-ttu-id="1c3ae-415">**NX_SUCCESS** (0x00) meta veri boyutunun başarıyla hesaplanması.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-415">**NX_SUCCESS** (0x00) Successful calculation of metadata size.</span></span>
- <span data-ttu-id="1c3ae-416">**NX_PTR_ERROR** (0x07) geçersiz şifre tablosu veya dönüş boyutu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-416">**NX_PTR_ERROR** (0x07) Invalid crypto table or return size pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1c3ae-417">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="1c3ae-417">Allowed From</span></span>

<span data-ttu-id="1c3ae-418">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="1c3ae-418">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1c3ae-419">Örnek</span><span class="sxs-lookup"><span data-stu-id="1c3ae-419">Example</span></span>

```C
/* Pointer to the platform-specific cipher table. */
extern nx_crypto_tls_ciphers;

/* Return variable for metadata size. */
ULONG crypto_metadata_size;

/* Calculate metadata size.  */
status =  nx_secure_tls_metadata_size_calculate(&nx_crypto_tls_ciphers,
                                                &crypto_metadata_size);


/* If status is NX_SUCCESS then crypto_metadata_size contains the size of the
   metadata buffer for the table nx_crypto_tls_ciphers.  */
```

### <a name="see-also"></a><span data-ttu-id="1c3ae-420">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-420">See Also</span></span>

- <span data-ttu-id="1c3ae-421">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="1c3ae-421">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_packet_allocate"></a><span data-ttu-id="1c3ae-422">nx_secure_tls_packet_allocate</span><span class="sxs-lookup"><span data-stu-id="1c3ae-422">nx_secure_tls_packet_allocate</span></span>

<span data-ttu-id="1c3ae-423">NetX Güvenli TLS Oturumu için paket ayırma</span><span class="sxs-lookup"><span data-stu-id="1c3ae-423">Allocate a packet for a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="1c3ae-424">Prototype</span><span class="sxs-lookup"><span data-stu-id="1c3ae-424">Prototype</span></span>

```C
UINT  nx_secure_tls_packet_allocate(NX_SECURE_TLS_SESSION *session_ptr,
                                    NX_PACKET_POOL *pool_ptr,
                                    NX_PACKET **packet_ptr,
                                    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="1c3ae-425">Description</span><span class="sxs-lookup"><span data-stu-id="1c3ae-425">Description</span></span>

<span data-ttu-id="1c3ae-426">Bu hizmet, belirtilen NX_PACKET TLS oturumu için belirtilen oturumdan bir NX_PACKET_POOL.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-426">This service allocates an NX_PACKET for the specified active TLS session from the specified NX_PACKET_POOL.</span></span> <span data-ttu-id="1c3ae-427">Bu hizmet, bir TLS bağlantısı üzerinden gönderilecek veri paketlerini ayırmak için uygulama tarafından çağrılmalı.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-427">This service should be called by the application to allocate data packets to be sent over a TLS connection.</span></span> <span data-ttu-id="1c3ae-428">Bu hizmet çağrılmadan önce TLS oturumunun başlatılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-428">The TLS session must be initialized before calling this service.</span></span>

<span data-ttu-id="1c3ae-429">Ayrılan paket düzgün şekilde başlatılır, böylece paket verileri doldurulduğunda TLS üst bilgisi ve alt bilgi verileri eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-429">The allocated packet is properly initialized so that TLS header and footer data may be added after the packet data is populated.</span></span> <span data-ttu-id="1c3ae-430">Aksi takdirde davranış, ile *nx_packet_allocate.*</span><span class="sxs-lookup"><span data-stu-id="1c3ae-430">The behavior is otherwise identical to *nx_packet_allocate*.</span></span>

### <a name="parameters"></a><span data-ttu-id="1c3ae-431">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1c3ae-431">Parameters</span></span>

- <span data-ttu-id="1c3ae-432">**session_ptr** TLS Oturumu örneğinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-432">**session_ptr** Pointer to a TLS Session instance.</span></span>
- <span data-ttu-id="1c3ae-433">**pool_ptr** Paketin ayrıl NX_PACKET_POOL bir uygulamanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-433">**pool_ptr** Pointer to an NX_PACKET_POOL from which to allocate the packet.</span></span>
- <span data-ttu-id="1c3ae-434">**packet_ptr** Yeni ayrılan paketin çıkış işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-434">**packet_ptr** Output pointer to the newly-allocated packet.</span></span>
- <span data-ttu-id="1c3ae-435">**wait_option** Paket ayırma için askıya alma seçeneği.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-435">**wait_option** Suspension option for packet allocation.</span></span>

### <a name="return-values"></a><span data-ttu-id="1c3ae-436">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-436">Return Values</span></span>

- <span data-ttu-id="1c3ae-437">**NX_SUCCESS** (0x00) Başarılı paket ayırma.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-437">**NX_SUCCESS** (0x00) Successful packet allocate.</span></span>
- <span data-ttu-id="1c3ae-438">**NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) Temel paket ayırma başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-438">**NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) Underlying packet allocation failed.</span></span>
- <span data-ttu-id="1c3ae-439">**NX_SECURE_TLS_SESSION_UNINITIALIZED** (0x101) Sağlanan TLS oturumu başlatılmadı.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-439">**NX_SECURE_TLS_SESSION_UNINITIALIZED** (0x101) The supplied TLS session was not initialized.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1c3ae-440">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="1c3ae-440">Allowed From</span></span>

<span data-ttu-id="1c3ae-441">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="1c3ae-441">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1c3ae-442">Örnek</span><span class="sxs-lookup"><span data-stu-id="1c3ae-442">Example</span></span>

```C
/* Allocate a new TLS packet from the previously created packet pool and
previously initialized TLS session.   */

status = nx_secure_tls_packet_allocate(&tls_session, &pool_0, &packet_ptr,
                                       NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the newly allocated packet pointer is found in the
variable packet_ptr.  */
```

### <a name="see-also"></a><span data-ttu-id="1c3ae-443">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-443">See Also</span></span>

- <span data-ttu-id="1c3ae-444">nx_tcp_socket_receive</span><span class="sxs-lookup"><span data-stu-id="1c3ae-444">nx_tcp_socket_receive</span></span>
- <span data-ttu-id="1c3ae-445">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="1c3ae-445">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="1c3ae-446">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="1c3ae-446">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="1c3ae-447">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="1c3ae-447">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="1c3ae-448">nx_secure_tls_session_delete</span><span class="sxs-lookup"><span data-stu-id="1c3ae-448">nx_secure_tls_session_delete</span></span>
- <span data-ttu-id="1c3ae-449">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="1c3ae-449">nx_secure_tls_session_receive</span></span>
- <span data-ttu-id="1c3ae-450">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="1c3ae-450">nx_secure_tls_session_send</span></span>
- <span data-ttu-id="1c3ae-451">nx_secure_tls_session_end</span><span class="sxs-lookup"><span data-stu-id="1c3ae-451">nx_secure_tls_session_end</span></span>
- <span data-ttu-id="1c3ae-452">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="1c3ae-452">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_psk_add"></a><span data-ttu-id="1c3ae-453">nx_secure_tls_psk_add</span><span class="sxs-lookup"><span data-stu-id="1c3ae-453">nx_secure_tls_psk_add</span></span>

<span data-ttu-id="1c3ae-454">NetX güvenli TLS oturumuna önceden paylaşılan anahtar ekleme</span><span class="sxs-lookup"><span data-stu-id="1c3ae-454">Add a Pre-Shared Key to a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="1c3ae-455">Prototype</span><span class="sxs-lookup"><span data-stu-id="1c3ae-455">Prototype</span></span>

```C
UINT  nx_secure_tls_psk_add(NX_SECURE_TLS_SESSION *session_ptr,
                            UCHAR *pre_shared_key, UINT psk_length,
                            UCHAR *psk_identity, UINT
                            identity_length, UCHAR *hint, UINT
                            hint_length);
```

### <a name="description"></a><span data-ttu-id="1c3ae-456">Description</span><span class="sxs-lookup"><span data-stu-id="1c3ae-456">Description</span></span>

<span data-ttu-id="1c3ae-457">Bu hizmet, bir TLS oturum denetim bloğuna önceden paylaşılan anahtar (PSK), kimlik dizesi ve kimlik ipucu ekler.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-457">This service adds a Pre-Shared Key (PSK), its identity string, and an identity hint to a TLS Session control block.</span></span> <span data-ttu-id="1c3ae-458">PSK ciphersuites etkin ve kullanıldığında, bir dijital sertifika yerine PSK kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-458">The PSK is used in place of a digital certificate when PSK ciphersuites are enabled and used.</span></span>

### <a name="parameters"></a><span data-ttu-id="1c3ae-459">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1c3ae-459">Parameters</span></span>

- <span data-ttu-id="1c3ae-460">**session_ptr** Daha önce oluşturulmuş bir TLS oturum örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-460">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="1c3ae-461">**pre_shared_key** Gerçek PSK değeri.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-461">**pre_shared_key** The actual PSK value.</span></span>
- <span data-ttu-id="1c3ae-462">**psk_length** PSK değeri uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-462">**psk_length** The length of the PSK value.</span></span>
- <span data-ttu-id="1c3ae-463">**psk_identity** Bu PSK değerini tanımlamak için kullanılan dize.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-463">**psk_identity** A string used to identify this PSK value.</span></span>
- <span data-ttu-id="1c3ae-464">**identity_length** PSK kimliğinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-464">**identity_length** The length of the PSK identity.</span></span>
- <span data-ttu-id="1c3ae-465">**İpucu** Bir TLS sunucusunda hangi sayıda PSKs arasından seçim yapmak gerektiğini göstermek için kullanılan dize.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-465">**hint** A string used to indicate which group of PSKs to choose from on a TLS server.</span></span>
- <span data-ttu-id="1c3ae-466">**hint_length** İpucu dizesinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-466">**hint_length** The length of the hint string.</span></span>

### <a name="return-values"></a><span data-ttu-id="1c3ae-467">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-467">Return Values</span></span>

- <span data-ttu-id="1c3ae-468">**NX_SUCCESS** (0x00) PSK 'nin başarılı bir şekilde eklenmesi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-468">**NX_SUCCESS** (0x00) Successful addition of PSK.</span></span>
- <span data-ttu-id="1c3ae-469">**NX_PTR_ERROR** (0x07) geçersiz TLS oturum işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-469">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>
- <span data-ttu-id="1c3ae-470">**NX_SECURE_TLS_NO_MORE_PSK_SPACE** (0x125) başka bir PSK eklenemiyor.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-470">**NX_SECURE_TLS_NO_MORE_PSK_SPACE** (0x125)  Cannot add another PSK.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1c3ae-471">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="1c3ae-471">Allowed From</span></span>

<span data-ttu-id="1c3ae-472">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="1c3ae-472">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1c3ae-473">Örnek</span><span class="sxs-lookup"><span data-stu-id="1c3ae-473">Example</span></span>

```C
/* PSK value.  */
UCHAR psk[] = { 0x1a, 0x2b, 0x3c, 0x4d };

/* Add PSK to TLS session.  */
status =  nx_secure_tls_psk_add(&tls_session, psk, sizeof(psk), “psk_1”, 4,
“Client_identity”, 15);


/* If status is NX_SUCCESS the PSK was successfully added.  */
```

### <a name="see-also"></a><span data-ttu-id="1c3ae-474">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-474">See Also</span></span>

- <span data-ttu-id="1c3ae-475">nx_secure_tls_client_psk_set</span><span class="sxs-lookup"><span data-stu-id="1c3ae-475">nx_secure_tls_client_psk_set</span></span>
- <span data-ttu-id="1c3ae-476">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="1c3ae-476">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="1c3ae-477">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="1c3ae-477">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="1c3ae-478">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="1c3ae-478">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="1c3ae-479">nx_secure_tls_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="1c3ae-479">nx_secure_tls_local_certificate_add</span></span>

## <a name="nx_secure_tls_remote_certificate_allocate"></a><span data-ttu-id="1c3ae-480">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="1c3ae-480">nx_secure_tls_remote_certificate_allocate</span></span>

<span data-ttu-id="1c3ae-481">Uzak bir TLS ana bilgisayarı tarafından sağlanan sertifika için alan ayırma</span><span class="sxs-lookup"><span data-stu-id="1c3ae-481">Allocate space for the certificate provided by a remote TLS host</span></span>

### <a name="prototype"></a><span data-ttu-id="1c3ae-482">Prototype</span><span class="sxs-lookup"><span data-stu-id="1c3ae-482">Prototype</span></span>

```C
UINT  nx_secure_tls_remote_certificate_allocate(
                 NX_SECURE_TLS_SESSION *session_ptr,
                 NX_SECURE_X509_CERT *certificate_ptr,
                 UCHAR *raw_certificate_buffer,
                 UINT raw_buffer_size);
```

### <a name="description"></a><span data-ttu-id="1c3ae-483">Description</span><span class="sxs-lookup"><span data-stu-id="1c3ae-483">Description</span></span>

<span data-ttu-id="1c3ae-484">Bu hizmet, TLS oturumu NX_SECURE_X509_CERT uzak konak tarafından sağlanan sertifikalar için alan ayrım yapmak amacıyla bir TLS oturumuna başlatlanmamış bir NX_SECURE_X509_CERT yapısı örneği ekler.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-484">This service adds an uninitialized NX_SECURE_X509_CERT structure instance to a TLS session for the purpose of allocating space for certificates provided by a remote host during a TLS session.</span></span> <span data-ttu-id="1c3ae-485">Uzak sertifika verileri NetX Secure TLS tarafından ayrıştırıldı ve bu bilgiler bu işleve sağlanan sertifika yapısı örneğini doldurmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-485">The remote certificate data is parsed by NetX Secure TLS and that information is used to populate the certificate structure instance provided to this function.</span></span> <span data-ttu-id="1c3ae-486">Bu şekilde eklenen sertifikalar bağlantılı bir listeye yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-486">Certificates added in this manner are placed in a linked list.</span></span>

<span data-ttu-id="1c3ae-487">Uzak ana bilgisayarın birden çok sertifika sağlaması bekleniyorsa, tüm sertifikalar için alan ayırmak için bu işlev tekrar tekrar çağrılır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-487">If it is expected that the remote host will provide multiple certificates, this function should be called repeatedly to allocate space for all certificates.</span></span> <span data-ttu-id="1c3ae-488">Ek sertifikalar, sertifika bağlantılı listesinin sonuna eklenir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-488">The additional certificates are added to the end of the certificate linked list.</span></span>

<span data-ttu-id="1c3ae-489">Uzak sertifikanın ayrılamaz olması, ÖNCEDEN Paylaşılan Anahtar (PSK) şifrelemesi kullandıkça TLS İstemci modunun TLS el sıkışması sırasında başarısız olmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-489">Failure to allocate a remote certificate will cause TLS Client mode to fail during the TLS handshake unless a Pre-Shared Key (PSK) ciphersuite is in use.</span></span>

<span data-ttu-id="1c3ae-490">Bu *raw_certificate_buffer* parametresi, gelen uzak sertifikayı depolamak için ayrılan alanı belirtir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-490">The *raw_certificate_buffer* parameter points to space allocated to store the incoming remote certificate.</span></span> <span data-ttu-id="1c3ae-491">İmzalar için SHA-256 kullanan 2048 bit RSA anahtarları olan tipik sertifikalar 1000-2000 bayt aralığındadır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-491">Typical certificates with RSA keys of 2048 bits using SHA-256 for signatures are in the range of 1000-2000 bytes.</span></span> <span data-ttu-id="1c3ae-492">Arabellek en azından bu boyutu tutacak kadar büyük olmalı, ancak uzak konak sertifikalara bağlı olarak önemli ölçüde daha küçük veya daha büyük olabilir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-492">The buffer should be large enough to at least hold that size, but depending on the remote host certificates may be significantly smaller or larger.</span></span> <span data-ttu-id="1c3ae-493">Arabellek gelen sertifikayı tutmayacak kadar küçükse TLS el sıkışması bir hatayla sona erer.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-493">Note that if the buffer is too small to hold the incoming certificate, the TLS handshake will end with an error.</span></span>

<span data-ttu-id="1c3ae-494">TLS Sunucusu modu için, uzak sertifika ayırma yalnızca istemci sertifikası kimlik doğrulaması etkinse gereklidir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-494">For TLS Server mode, a remote certificate allocation is needed only if client certificate authentication is enabled.</span></span>

### <a name="parameters"></a><span data-ttu-id="1c3ae-495">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1c3ae-495">Parameters</span></span>

- <span data-ttu-id="1c3ae-496">**session_ptr** Daha önce oluşturulmuş bir TLS Oturumu örneğinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-496">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="1c3ae-497">**certificate_ptr** Uninitialized X.509 Sertifika örneğinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-497">**certificate_ptr** Pointer to an uninitialized X.509 Certificate instance.</span></span>
- <span data-ttu-id="1c3ae-498">**raw_certificate_buffer** Uzak ana bilgisayardan alınan ayrıştırılmamış sertifikayı tutan bir arabellek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-498">**raw_certificate_buffer** Pointer to a buffer to hold the un-parsed certificate received from the remote host.</span></span>
- <span data-ttu-id="1c3ae-499">**raw_buffer_size** Ham sertifika arabelleğinin boyutu.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-499">**raw_buffer_size** Size of the raw certificate buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="1c3ae-500">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-500">Return Values</span></span>

- <span data-ttu-id="1c3ae-501">**NX_SUCCESS** (0x00) sertifikanın başarıyla ayrılması.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-501">**NX_SUCCESS** (0x00) Successful allocation of certificate.</span></span>
- <span data-ttu-id="1c3ae-502">**NX_PTR_ERROR** (0x07) geçersiz TLS oturum işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-502">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>
- <span data-ttu-id="1c3ae-503">**NX_SECURE_TLS_INSUFFICIENT_CERT_SPACE** (0x12D) sağlanan arabellek çok küçük.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-503">**NX_SECURE_TLS_INSUFFICIENT_CERT_SPACE** (0x12D) The supplied buffer was too small.</span></span>
- <span data-ttu-id="1c3ae-504">**NX_INVALID_PARAMETERS** (0x4D) geçersiz bir sertifika eklemeye çalıştı.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-504">**NX_INVALID_PARAMETERS** (0x4D) Tried to add an invalid certificate.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1c3ae-505">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="1c3ae-505">Allowed From</span></span>

<span data-ttu-id="1c3ae-506">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="1c3ae-506">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1c3ae-507">Örnek</span><span class="sxs-lookup"><span data-stu-id="1c3ae-507">Example</span></span>

```C
/* Certificate control block. */
NX_SECURE_X509_CERT certificate;

/* Buffer space to hold the incoming certificate. */
UCHAR certificate_buffer[2000];

/* Add certificate to TLS session.  */
status =  nx_secure_tls_remote_certificate_allocate(&tls_session, &certificate,
                                                    certificate_buffer,
                                                    sizeof(certificate_buffer));


/* If status is NX_SUCCESS the certificate was successfully allocated.  */
```

### <a name="see-also"></a><span data-ttu-id="1c3ae-508">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-508">See Also</span></span>

- <span data-ttu-id="1c3ae-509">nx_secure_x509_certificate_initialize,</span><span class="sxs-lookup"><span data-stu-id="1c3ae-509">nx_secure_x509_certificate_initialize,</span></span>
- <span data-ttu-id="1c3ae-510">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="1c3ae-510">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_remote_certificate_buffer_allocate"></a><span data-ttu-id="1c3ae-511">nx_secure_tls_remote_certificate_buffer_allocate</span><span class="sxs-lookup"><span data-stu-id="1c3ae-511">nx_secure_tls_remote_certificate_buffer_allocate</span></span>

<span data-ttu-id="1c3ae-512">Uzak bir TLS ana bilgisayarı tarafından belirtilen tüm sertifikalar için alan ayır</span><span class="sxs-lookup"><span data-stu-id="1c3ae-512">Allocate space for all certificates provided by a remote TLS host</span></span>

### <a name="prototype"></a><span data-ttu-id="1c3ae-513">Prototype</span><span class="sxs-lookup"><span data-stu-id="1c3ae-513">Prototype</span></span>

```C
UINT  nx_secure_tls_remote_certificate_buffer_allocate(
                  NX_SECURE_TLS_SESSION *session_ptr,
                  UINT certs_number, VOID *certificate_buffer,
                  ULONG buffer_size);
```

### <a name="description"></a><span data-ttu-id="1c3ae-514">Description</span><span class="sxs-lookup"><span data-stu-id="1c3ae-514">Description</span></span>

<span data-ttu-id="1c3ae-515">Bu hizmet, bir TLS Istemci örneğinde X. 509.440 kimlik doğrulaması ve doğrulama gerçekleştirmek için uzak sunucu konaklarından gelen sertifika zincirlerini işlemek üzere alan ayırır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-515">This service allocates space to process incoming certificate chains from remote server hosts in order to perform X.509 authentication and verification in a TLS Client instance.</span></span> <span data-ttu-id="1c3ae-516">TLS sunucu modu için, uzak sertifika ayırma yalnızca Client X. 509.440 sertifikası kimlik doğrulaması etkinse gereklidir – TLS sunucu örnekleri için, bunun yerine hizmet *nx_secure_tls_session_x509_client_verify_configure* kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-516">For TLS Server mode, remote certificate allocation is needed only if client X.509 certificate authentication is enabled – for TLS Server instances the service *nx_secure_tls_session_x509_client_verify_configure* should be used instead.</span></span>

<span data-ttu-id="1c3ae-517">Bir önceden paylaşılan anahtar (PSK) ciphersuite kullanımda değilse, uzak sertifikaları ayıramaması TLS Istemci modunun TLS el sıkışması sırasında başarısız olmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-517">Failure to allocate remote certificates will cause TLS Client mode to fail during the TLS handshake unless a Pre-Shared Key (PSK) ciphersuite is in use.</span></span>

<span data-ttu-id="1c3ae-518">*Certificate_buffer* parametresi, gelen uzak sertifikaları ve bu sertifikalar için gereken denetim bloklarını depolamak için ayrılan alana işaret eder.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-518">The *certificate_buffer* parameter points to space allocated to store the incoming remote certificates and the control blocks needed for those certificates.</span></span> <span data-ttu-id="1c3ae-519">Arabellek, her sertifikaya verilen eşit bir bölüme sahip sertifika (*certs_number*) sayısına bölünür.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-519">The buffer will be divided by the number of certificates (*certs_number*) with an equal portion given to each certificate.</span></span> <span data-ttu-id="1c3ae-520">*Buffer_size* parametresi arabelleğin boyutunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-520">The *buffer_size*  parameter indicates the size of the buffer.</span></span> <span data-ttu-id="1c3ae-521">Aşağıdaki formül ile, gereken alan bulunabilir:</span><span class="sxs-lookup"><span data-stu-id="1c3ae-521">The space needed can be found with the following formula:</span></span>

```C
buffer_size = (<expected max number of certificates in chain>) *
                 (sizeof(NX_SECURE_X509_CERT) + <max cert size>)
```

<span data-ttu-id="1c3ae-522">İmzalar için SHA-256 kullanan 2048 bitin RSA anahtarlarına sahip tipik sertifikalar, 1000-2000 bayt aralığındadır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-522">Typical certificates with RSA keys of 2048 bits using SHA-256 for signatures are in the range of 1000-2000 bytes.</span></span> <span data-ttu-id="1c3ae-523">Arabellek, her sertifika için en az sayıda tutmaya yetecek kadar büyük olmalıdır, ancak uzak ana bilgisayar sertifikalarına bağlı olarak, önemli ölçüde daha küçük veya daha büyük olabilir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-523">The buffer should be large enough to at least hold that size for each certificate, but depending on the remote host certificates may be significantly smaller or larger.</span></span> <span data-ttu-id="1c3ae-524">Arabellek gelen sertifikayı tutmayacak kadar küçükse TLS el sıkışması bir hatayla sona erer.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-524">Note that if the buffer is too small to hold the incoming certificate, the TLS handshake will end with an error.</span></span>

### <a name="parameters"></a><span data-ttu-id="1c3ae-525">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1c3ae-525">Parameters</span></span>

- <span data-ttu-id="1c3ae-526">**session_ptr** Daha önce oluşturulmuş bir TLS Oturumu örneğinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-526">**session_ptr** Pointer to a previously created TLS Session  instance.</span></span>
- <span data-ttu-id="1c3ae-527">**certs_number** Sağlanan arabellekten ayrılacak sertifika sayısı.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-527">**certs_number** Number of certificates to allocate from the  provided buffer.</span></span>
- <span data-ttu-id="1c3ae-528">**certificate_buffer** Uzak bir konaktan alınan sertifikaları tutmak için bir arabelleğe işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-528">**certificate_buffer** Pointer to a buffer to hold certificates received  from a remote host.</span></span>
- <span data-ttu-id="1c3ae-529">**buffer_size** Sertifika arabelleğinin boyutu.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-529">**buffer_size** Size of the certificate buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="1c3ae-530">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-530">Return Values</span></span>

- <span data-ttu-id="1c3ae-531">**NX_SUCCESS** (0x00) Sertifikanın başarıyla tahsisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-531">**NX_SUCCESS** (0x00) Successful allocation of certificate.</span></span>
- <span data-ttu-id="1c3ae-532">**NX_PTR_ERROR** (0x07) Geçersiz TLS oturumu veya arabellek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-532">**NX_PTR_ERROR** (0x07) Invalid TLS session or buffer pointer.</span></span>
- <span data-ttu-id="1c3ae-533">**NX_SECURE_TLS_INSUFFICIENT_CERT_SPACE** (0x12D) Sağlanan arabellek çok küçüktü.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-533">**NX_SECURE_TLS_INSUFFICIENT_CERT_SPACE** (0x12D) The supplied buffer was too small.</span></span>
- <span data-ttu-id="1c3ae-534">**NX_INVALID_PARAMETERS** (0x4D) Arabellek istenen sayıda sertifikayı tutmak için çok küçüktü.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-534">**NX_INVALID_PARAMETERS** (0x4D) The buffer was too small to hold  the desired number of certificates.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1c3ae-535">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="1c3ae-535">Allowed From</span></span>

<span data-ttu-id="1c3ae-536">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="1c3ae-536">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1c3ae-537">Örnek</span><span class="sxs-lookup"><span data-stu-id="1c3ae-537">Example</span></span>

```C
/* Buffer space to hold the incoming certificates. */
#define CERTIFICATE_NUMBER    (2)
#define CERTIFICATE_SIZE      (2000)
#define BUFFER_SIZE           (CERTIFICATE_NUMBER * \
                              (sizeof(NX_SECURE_X509_CERT) + CERTIFICATE_SIZE))
UCHAR certificate_buffer[BUFFER_SIZE];

/* Add certificate to TLS session.  */
status =  nx_secure_tls_remote_certificate_buffer_allocate(&tls_session,
                                                      CERTIFICATE_NUMBER,
                                                      certificate_buffer,
                                                      BUFFER_SIZE);


/* If status is NX_SUCCESS the buffer was successfully allocated.  */
```

### <a name="see-also"></a><span data-ttu-id="1c3ae-538">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-538">See Also</span></span>

- <span data-ttu-id="1c3ae-539">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="1c3ae-539">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="1c3ae-540">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="1c3ae-540">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_remote_certificate_free_all"></a><span data-ttu-id="1c3ae-541">nx_secure_tls_remote_certificate_free_all</span><span class="sxs-lookup"><span data-stu-id="1c3ae-541">nx_secure_tls_remote_certificate_free_all</span></span>

<span data-ttu-id="1c3ae-542">Gelen sertifikalar için ayrılan boş alan</span><span class="sxs-lookup"><span data-stu-id="1c3ae-542">Free space allocated for incoming certificates</span></span>

### <a name="prototype"></a><span data-ttu-id="1c3ae-543">Prototype</span><span class="sxs-lookup"><span data-stu-id="1c3ae-543">Prototype</span></span>

```C
UINT  nx_secure_tls_remote_certificate_free_all(
                  NX_SECURE_TLS_SESSION *session_ptr);
```

### <a name="description"></a><span data-ttu-id="1c3ae-544">Description</span><span class="sxs-lookup"><span data-stu-id="1c3ae-544">Description</span></span>

<span data-ttu-id="1c3ae-545">Bu hizmet, belirli bir TLS Oturumuna ayrılmış olan tüm sertifika arabelleklerini nx_secure_tls_remote_certificate_allocated oturumun boş sertifika alanlarına döndürerek bu arabellekleri serbest bırakarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-545">This service is used to free all of the certificate buffers allocated to a particular TLS Session by nx_secure_tls_remote_certificate_allocated by returning them to that session's free certificate space.</span></span> <span data-ttu-id="1c3ae-546">Bu, bir uygulamanın tlS oturum nesnesini silmeden yeniden kullanması ve bir tls ile yeniden oluşturması nx_secure_tls_session_delete nx_secure_tls_session_create.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-546">This may be necessary if an application reuses a TLS session object without deleting it and recreating it with nx_secure_tls_session_delete and nx_secure_tls_session_create.</span></span>

<span data-ttu-id="1c3ae-547">TLS oturumu oturumda olduğu gibi sıfırlanır ve bu nedenle çoğu uygulamanın bu hizmeti nx_secure_tls_session_end uzak sertifika alanı otomatik olarak kurtarılır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-547">Note that the remote certificate space is recovered automatically when the TLS session is reset as happens in nx_secure_tls_session_end so most applications should not need to call this service.</span></span>

### <a name="parameters"></a><span data-ttu-id="1c3ae-548">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1c3ae-548">Parameters</span></span>

- <span data-ttu-id="1c3ae-549">**session_ptr** Daha önce oluşturulmuş bir TLS Oturumu örneğinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-549">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="1c3ae-550">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-550">Return Values</span></span>

- <span data-ttu-id="1c3ae-551">**NX_SUCCESS** (0x00) Başarılı işlem.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-551">**NX_SUCCESS** (0x00) Successful operation.</span></span>
- <span data-ttu-id="1c3ae-552">**NX_PTR_ERROR** (0x07) Geçersiz TLS oturum işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-552">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>
- <span data-ttu-id="1c3ae-553">**NX_INVALID_PARAMETERS** (0x4D) iç hata – sertifika deposu muhtemelen bozuk.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-553">**NX_INVALID_PARAMETERS** (0x4D) Internal error – certificate store likely corrupt.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1c3ae-554">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="1c3ae-554">Allowed From</span></span>

<span data-ttu-id="1c3ae-555">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="1c3ae-555">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1c3ae-556">Örnek</span><span class="sxs-lookup"><span data-stu-id="1c3ae-556">Example</span></span>

```C
/* Certificate control block. */
NX_SECURE_X509_CERT certificate;

/* Buffer space to hold the incoming certificate. */
UCHAR certificate_buffer[2000];

/* Add certificate to TLS session.  */
status =  nx_secure_tls_remote_certificate_allocate(&tls_session, &certificate,
                                                    certificate_buffer,
                                                    sizeof(certificate_buffer));


/* If status is NX_SUCCESS the certificate was successfully allocated.  */

/* … TLS session setup, TCP connection, etc… */

/* End TLS session. */
nx_secure_tls_session_end(&tls_session, NX_WAIT_FOREVER);

/* Free up certificate buffers for next connection. */
nx_secure_tls_remote_certificate_free_all(&tls_session);
```

### <a name="see-also"></a><span data-ttu-id="1c3ae-557">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-557">See Also</span></span>

- <span data-ttu-id="1c3ae-558">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="1c3ae-558">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="1c3ae-559">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="1c3ae-559">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="1c3ae-560">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="1c3ae-560">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="1c3ae-561">nx_secure_tls_session_end</span><span class="sxs-lookup"><span data-stu-id="1c3ae-561">nx_secure_tls_session_end</span></span>

## <a name="nx_secure_tls_server_certificate_add"></a><span data-ttu-id="1c3ae-562">nx_secure_tls_server_certificate_add</span><span class="sxs-lookup"><span data-stu-id="1c3ae-562">nx_secure_tls_server_certificate_add</span></span>

<span data-ttu-id="1c3ae-563">Sayısal bir tanımlayıcı kullanarak TLS sunucuları için özel olarak bir sertifika ekleyin</span><span class="sxs-lookup"><span data-stu-id="1c3ae-563">Add a certificate specifically for TLS servers using a numeric identifier</span></span>

### <a name="prototype"></a><span data-ttu-id="1c3ae-564">Prototype</span><span class="sxs-lookup"><span data-stu-id="1c3ae-564">Prototype</span></span>

```C
UINT  nx_secure_tls_server_certificate_add(
                  NX_SECURE_TLS_SESSION *session_ptr,
                  NX_SECURE_X509_CERT *certificate, UINT cert_id);
```

### <a name="description"></a><span data-ttu-id="1c3ae-565">Description</span><span class="sxs-lookup"><span data-stu-id="1c3ae-565">Description</span></span>

<span data-ttu-id="1c3ae-566">Bu hizmet, bir TLS oturumunun yerel deposuna bir sertifika eklemek için kullanılır (bkz. nx_secure_tls_local_certificate_add) sertifikanın içindeki X. 509.952 Subject (ortak ad) kullanarak depoyu dizinlemek yerine bir sayısal tanımlayıcı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-566">This service is used to add a certificate to a TLS session's local store (see nx_secure_tls_local_certificate_add) using a numeric identifier instead of indexing the store using the X.509 Subject (Common Name) within the certificate.</span></span> <span data-ttu-id="1c3ae-567">Sayısal tanımlayıcı sertifikadan ayrıdır ve birden çok sertifikanın bir TLS sunucusuna kimlik sertifikası olarak eklenmesine izin verir, ayrıca aynı ortak ada sahip birden çok sertifikanın aynı TLS oturumu yerel deposuna eklenmesine izin verir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-567">The numeric identifier is separate from the certificate and allows multiple certificates to be added as identity certificates to a TLS server, as well as allowing multiple certificates with the same Common Name to be added to the same TLS session local store.</span></span> <span data-ttu-id="1c3ae-568">Aynı hizmet istemci sertifikaları için kullanılabilir, ancak bir TLS istemcisinde birden çok kimlik sertifikası olması nadir bir durumdur.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-568">This same service can be used for client certificates, but it is rare for a TLS client to have multiple identity certificates.</span></span>

<span data-ttu-id="1c3ae-569">Cert_id parametresi, uygulama tarafından atanan sıfır olmayan pozitif bir tamsayıdır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-569">The cert_id parameter is a non-zero positive integer assigned by the application.</span></span> <span data-ttu-id="1c3ae-570">Gerçek değer (sıfırdan farklı) değil, ancak belirtilen TLS oturumunun deposunda benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-570">The actual value does not matter (other than zero) but it must be unique in the store for the provided TLS session.</span></span> <span data-ttu-id="1c3ae-571">Cert_id değeri, sırasıyla nx_secure_tls_server_certificate_find ve nx_secure_tls_server_certificate_remove kullanılarak yerel depodan sertifika bulmak ve kaldırmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-571">The cert_id value can be used to find and remove certificates from the local store using nx_secure_tls_server_certificate_find and nx_secure_tls_server_certificate_remove, respectively.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1c3ae-572">*Bu API, nx_secure_tls_local_certificate_add kullanırken aynı TLS oturumuyla kullanılmamalıdır. Nx_secure_tls_server_certificate_add API 'SI her sertifika için benzersiz bir sayısal tanımlayıcı ve X. 509.440 ortak adına göre yerel sertifika hizmetleri dizini kullanır. Sunucu sertifikası Hizmetleri, aynı yerel depoda paylaşılan verileri olan birden çok sertifikanın (özellikle ortak ad) bulunmasına izin verir. Bu, birden çok kimliği olan bir sunucu için faydalıdır.*</span><span class="sxs-lookup"><span data-stu-id="1c3ae-572">*This API should not be used with the same TLS session when using nx_secure_tls_local_certificate_add. The nx_secure_tls_server_certificate_add API uses a unique numeric identifier for each certificate, and local certificate services index based on the X.509 Common Name. The server certificate services allow multiple certificates with shared data (especially Common Name) to exist in the same local store – this is useful for a server with multiple identities.*</span></span>

### <a name="parameters"></a><span data-ttu-id="1c3ae-573">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1c3ae-573">Parameters</span></span>

- <span data-ttu-id="1c3ae-574">**session_ptr** Daha önce oluşturulmuş bir TLS oturum örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-574">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="1c3ae-575">**sertifika** Daha önce başlatılmış bir X. 509.440 sertifika örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-575">**certificate** Pointer to a previously initialized X.509 certificate instance.</span></span>
- <span data-ttu-id="1c3ae-576">**cert_id** Pozitif, sıfır olmayan, görece benzersiz sertifika kimliği numarası.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-576">**cert_id** Positive, non-zero, relatively unique certificate ID number.</span></span>

### <a name="return-values"></a><span data-ttu-id="1c3ae-577">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-577">Return Values</span></span>

- <span data-ttu-id="1c3ae-578">**NX_SUCCESS** (0x00)Başarılı işlem.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-578">**NX_SUCCESS** (0x00)Successful operation.</span></span>
- <span data-ttu-id="1c3ae-579">**NX_PTR_ERROR** (0x07) Geçersiz TLS oturumu veya sertifika işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-579">**NX_PTR_ERROR** (0x07) Invalid TLS session orcertificate pointer.</span></span>
- <span data-ttu-id="1c3ae-580">**NX_SECURE_TLS_CERT_ID_INVALID** (0x138) Sağlanan sertifika kimliğinin Geçersiz bir değeri vardı (büyük olasılıkla 0).</span><span class="sxs-lookup"><span data-stu-id="1c3ae-580">**NX_SECURE_TLS_CERT_ID_INVALID** (0x138) The provided certificate ID had An invalid value (likely 0).</span></span>
- <span data-ttu-id="1c3ae-581">**NX_SECURE_TLS_CERT_ID_DUPLICATE** (0x139) Sağlanan sertifika kimliği yerel depoda zaten mevcut.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-581">**NX_SECURE_TLS_CERT_ID_DUPLICATE** (0x139) The provided certificate ID was already present in the local store.</span></span>
- <span data-ttu-id="1c3ae-582">**NX_INVALID_PARAMETERS(0x4D)** İç hata – sertifika deposu büyük olasılıkla bozuk.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-582">**NX_INVALID_PARAMETERS(0x4D)** Internal error – certificate store likely corrupt.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1c3ae-583">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="1c3ae-583">Allowed From</span></span>

<span data-ttu-id="1c3ae-584">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="1c3ae-584">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1c3ae-585">Örnek</span><span class="sxs-lookup"><span data-stu-id="1c3ae-585">Example</span></span>

```C
/* Certificate control block. */
NX_SECURE_X509_CERT certificate;


/* Add certificate to TLS session.  */
status =  nx_secure_tls_server_certificate_add(&tls_session, &certificate, 0x12);


/* If status is NX_SUCCESS the certificate was successfully added with the ID
0x12.  */
```

### <a name="see-also"></a><span data-ttu-id="1c3ae-586">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-586">See Also</span></span>

- <span data-ttu-id="1c3ae-587">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="1c3ae-587">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="1c3ae-588">nx_secure_tls_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="1c3ae-588">nx_secure_tls_local_certificate_add</span></span>
- <span data-ttu-id="1c3ae-589">nx_secure_tls_active_certificate_set</span><span class="sxs-lookup"><span data-stu-id="1c3ae-589">nx_secure_tls_active_certificate_set</span></span>
- <span data-ttu-id="1c3ae-590">nx_secure_tls_server_certificate_find</span><span class="sxs-lookup"><span data-stu-id="1c3ae-590">nx_secure_tls_server_certificate_find</span></span>
- <span data-ttu-id="1c3ae-591">nx_secure_tls_server_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="1c3ae-591">nx_secure_tls_server_certificate_remove</span></span>

## <a name="nx_secure_tls_server_certificate_find"></a><span data-ttu-id="1c3ae-592">nx_secure_tls_server_certificate_find</span><span class="sxs-lookup"><span data-stu-id="1c3ae-592">nx_secure_tls_server_certificate_find</span></span>

<span data-ttu-id="1c3ae-593">Sayısal tanımlayıcı kullanarak sertifika bulma</span><span class="sxs-lookup"><span data-stu-id="1c3ae-593">Find a certificate using a numeric identifier</span></span>

### <a name="prototype"></a><span data-ttu-id="1c3ae-594">Prototype</span><span class="sxs-lookup"><span data-stu-id="1c3ae-594">Prototype</span></span>

```C
UINT  nx_secure_tls_server_certificate_find(
                  NX_SECURE_TLS_SESSION *session_ptr,
                  NX_SECURE_X509_CERT **certificate, UINT cert_id);
```

### <a name="description"></a><span data-ttu-id="1c3ae-595">Description</span><span class="sxs-lookup"><span data-stu-id="1c3ae-595">Description</span></span>

<span data-ttu-id="1c3ae-596">Bu hizmet, sertifika içindeki X.509 Konu (Ortak Ad) kullanarak depo dizini oluşturma yerine sayısal tanımlayıcı kullanarak TLS oturumunun yerel depolama (bkz. nx_secure_tls_local_certificate_add) içinde bir sertifika bulmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-596">This service is used to find a certificate in a TLS session's local store (see nx_secure_tls_local_certificate_add) using a numeric identifier instead of indexing the store using the X.509 Subject (Common Name) within the certificate.</span></span>

<span data-ttu-id="1c3ae-597">Cert_id parametresi, sertifika tlS oturumu yerel deposuna kullanılarak ekleniyorsa uygulama tarafından atanan sıfır olmayan bir pozitif tamsayıdır nx_secure_tls_server_certificate_add.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-597">The cert_id parameter is a non-zero positive integer assigned by the application when the certificate is added to the TLS session local store using nx_secure_tls_server_certificate_add.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1c3ae-598">*Bu API, uygulama kullanılırken aynı TLS oturumuyla nx_secure_tls_local_certificate_add. Uygulama nx_secure_tls_server_certificate_add API'si, her sertifika için benzersiz bir sayısal tanımlayıcı ve X.509 Ortak Adı'nın temel alınan yerel sertifika hizmetleri dizinini kullanır. Sunucu sertifika hizmetleri, paylaşılan verilere sahip birden çok sertifikanın (özellikle Ortak Ad) aynı yerel depoda var olmasına olanak sağlar. Bu, birden çok kimli sunucu için yararlıdır.*</span><span class="sxs-lookup"><span data-stu-id="1c3ae-598">*This API should not be used with the same TLS session when using nx_secure_tls_local_certificate_add. The nx_secure_tls_server_certificate_add API uses a unique numeric identifier for each certificate, and local certificate services index based on the X.509 Common Name. The server certificate services allow multiple certificates with shared data (especially Common Name) to exist in the same local store – this is useful for a server with multiple identities.*</span></span>

### <a name="parameters"></a><span data-ttu-id="1c3ae-599">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1c3ae-599">Parameters</span></span>

- <span data-ttu-id="1c3ae-600">**session_ptr** Daha önce oluşturulmuş bir TLS Oturumu örneğinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-600">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="1c3ae-601">**sertifika** Bulunan sertifikaya başvuru dönmek için X.509 sertifika işaretçisinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-601">**certificate** Pointer to an X.509 certificate pointer to return a reference to the found certificate.</span></span>
- <span data-ttu-id="1c3ae-602">**cert_id** Sıfır olmayan pozitif sertifika kimliği değeri.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-602">**cert_id** Non-zero positive certificate ID value.</span></span>

### <a name="return-values"></a><span data-ttu-id="1c3ae-603">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-603">Return Values</span></span>

- <span data-ttu-id="1c3ae-604">**NX_SUCCESS** (0x00) başarılı işlemi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-604">**NX_SUCCESS** (0x00)Successful operation.</span></span>
- <span data-ttu-id="1c3ae-605">**NX_PTR_ERROR** (0x07) geçersiz TLS oturumu veya sertifika işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-605">**NX_PTR_ERROR** (0x07) Invalid TLS session or certificate pointer.</span></span>
- <span data-ttu-id="1c3ae-606">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) BELIRTILEN sertifika kimliği, belirtilen TLS oturumunun yerel deposundaki herhangi bir hiçbiriyle eşleşmedi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-606">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) The provided certificate ID did not match any in the local store of the provided TLS session.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1c3ae-607">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="1c3ae-607">Allowed From</span></span>

<span data-ttu-id="1c3ae-608">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="1c3ae-608">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1c3ae-609">Örnek</span><span class="sxs-lookup"><span data-stu-id="1c3ae-609">Example</span></span>

```C
NX_SECURE_X509_CERT *certificate;


/* Find certificate in TLS session.  */
status =  nx_secure_tls_server_certificate_find(&tls_session, &certificate, 0x12);


/* If status is NX_SUCCESS the certificate was successfully found and a reference
returned in the certificate parameter.  */
```

### <a name="see-also"></a><span data-ttu-id="1c3ae-610">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-610">See Also</span></span>

- <span data-ttu-id="1c3ae-611">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="1c3ae-611">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="1c3ae-612">nx_secure_tls_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="1c3ae-612">nx_secure_tls_local_certificate_add</span></span>
- <span data-ttu-id="1c3ae-613">nx_secure_tls_active_certificate_set</span><span class="sxs-lookup"><span data-stu-id="1c3ae-613">nx_secure_tls_active_certificate_set</span></span>
- <span data-ttu-id="1c3ae-614">nx_secure_tls_server_certificate_add</span><span class="sxs-lookup"><span data-stu-id="1c3ae-614">nx_secure_tls_server_certificate_add</span></span>
- <span data-ttu-id="1c3ae-615">nx_secure_tls_server_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="1c3ae-615">nx_secure_tls_server_certificate_remove</span></span>

##  <a name="nx_secure_tls_server_certificate_remove"></a><span data-ttu-id="1c3ae-616">nx_secure_tls_server_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="1c3ae-616">nx_secure_tls_server_certificate_remove</span></span>

<span data-ttu-id="1c3ae-617">Sayısal tanımlayıcıyı kullanarak yerel sunucu sertifikasını kaldırma</span><span class="sxs-lookup"><span data-stu-id="1c3ae-617">Remove a local server certificate using a numeric identifier</span></span>

### <a name="prototype"></a><span data-ttu-id="1c3ae-618">Prototype</span><span class="sxs-lookup"><span data-stu-id="1c3ae-618">Prototype</span></span>

```C
UINT  nx_secure_tls_server_certificate_remove(
                  NX_SECURE_TLS_SESSION *session_ptr, UINT cert_id);
```

### <a name="description"></a><span data-ttu-id="1c3ae-619">Description</span><span class="sxs-lookup"><span data-stu-id="1c3ae-619">Description</span></span>

<span data-ttu-id="1c3ae-620">Bu hizmet, bir sertifikayı bir TLS oturumunun yerel deposundan kaldırmak için kullanılır (bkz. nx_secure_tls_local_certificate_add) sertifikanın içindeki X. 509.952 Subject (ortak ad) kullanarak depoyu dizinlemek yerine sayısal bir tanımlayıcı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-620">This service is used to remove a certificate from a TLS session's local store (see nx_secure_tls_local_certificate_add) using a numeric identifier instead of indexing the store using the X.509 Subject (Common Name) within the certificate.</span></span>

<span data-ttu-id="1c3ae-621">Cert_id parametresi, sertifika, nx_secure_tls_server_certificate_add kullanılarak TLS oturumu yerel deposuna eklendiğinde, uygulama tarafından atanan sıfır olmayan pozitif bir tamsayıdır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-621">The cert_id parameter is a non-zero positive integer assigned by the application when the certificate is added to the TLS session local store using nx_secure_tls_server_certificate_add.</span></span>

### <a name="parameters"></a><span data-ttu-id="1c3ae-622">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1c3ae-622">Parameters</span></span>

- <span data-ttu-id="1c3ae-623">**session_ptr** Daha önce oluşturulmuş bir TLS oturum örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-623">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="1c3ae-624">**cert_id** Sıfır olmayan pozitif sertifika KIMLIĞI değeri.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-624">**cert_id** Non-zero positive certificate ID value.</span></span>

### <a name="return-values"></a><span data-ttu-id="1c3ae-625">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-625">Return Values</span></span>

- <span data-ttu-id="1c3ae-626">**NX_SUCCESS** (0x00) başarılı işlemi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-626">**NX_SUCCESS** (0x00)Successful operation.</span></span>
- <span data-ttu-id="1c3ae-627">**NX_PTR_ERROR** (0x07) geçersiz TLS oturumu.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-627">**NX_PTR_ERROR** (0x07) Invalid TLS session.</span></span>
- <span data-ttu-id="1c3ae-628">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) BELIRTILEN sertifika kimliği, belirtilen TLS oturumunun yerel deposundaki herhangi bir hiçbiriyle eşleşmedi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-628">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) The provided certificate ID did not match any in the local store of the provided TLS session.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1c3ae-629">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="1c3ae-629">Allowed From</span></span>

<span data-ttu-id="1c3ae-630">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="1c3ae-630">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1c3ae-631">Örnek</span><span class="sxs-lookup"><span data-stu-id="1c3ae-631">Example</span></span>

```C
/* Certificate control block. */
NX_SECURE_X509_CERT certificate;


/* Add certificate to TLS session with id 0x12.  */
status =  nx_secure_tls_server_certificate_add(&tls_session, &certificate, 0x12);
/* Use certificate in TLS session, etc… */

/* Remove certificate from TLS session with id 0x12.  */
status =  nx_secure_tls_server_certificate_remove(&tls_session, 0x12);


/* If status is NX_SUCCESS the certificate was successfully removed.  */
```

### <a name="see-also"></a><span data-ttu-id="1c3ae-632">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-632">See Also</span></span>

- <span data-ttu-id="1c3ae-633">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="1c3ae-633">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="1c3ae-634">nx_secure_tls_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="1c3ae-634">nx_secure_tls_local_certificate_add</span></span>
- <span data-ttu-id="1c3ae-635">nx_secure_tls_active_certificate_set</span><span class="sxs-lookup"><span data-stu-id="1c3ae-635">nx_secure_tls_active_certificate_set</span></span>
- <span data-ttu-id="1c3ae-636">nx_secure_tls_server_certificate_add</span><span class="sxs-lookup"><span data-stu-id="1c3ae-636">nx_secure_tls_server_certificate_add</span></span>
- <span data-ttu-id="1c3ae-637">nx_secure_tls_server_certificate_find</span><span class="sxs-lookup"><span data-stu-id="1c3ae-637">nx_secure_tls_server_certificate_find</span></span>

## <a name="nx_secure_tls_session_alert_value_get"></a><span data-ttu-id="1c3ae-638">nx_secure_tls_session_alert_value_get</span><span class="sxs-lookup"><span data-stu-id="1c3ae-638">nx_secure_tls_session_alert_value_get</span></span>

<span data-ttu-id="1c3ae-639">Uzak konak tarafından gönderilen TLS uyarı değerini ve düzeyini al</span><span class="sxs-lookup"><span data-stu-id="1c3ae-639">Get the TLS alert value and level sent by the remote host</span></span>

### <a name="prototype"></a><span data-ttu-id="1c3ae-640">Prototype</span><span class="sxs-lookup"><span data-stu-id="1c3ae-640">Prototype</span></span>

```C
UINT  nx_secure_tls_session_alert_value_get(
                   NX_SECURE_TLS_SESSION *session_ptr,
                   UINT *alert_level, UINT *alert_value);
```

### <a name="description"></a><span data-ttu-id="1c3ae-641">Description</span><span class="sxs-lookup"><span data-stu-id="1c3ae-641">Description</span></span>

<span data-ttu-id="1c3ae-642">Bu hizmet, uzak konak bir soruna veya hataya yanıt olarak uyarı gönderdiğinde TLS uyarı düzeyini ve değerini almak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-642">This service is used to retrieve the TLS alert level and value when the remote host sends an alert in response to some problem or error.</span></span>

<span data-ttu-id="1c3ae-643">alert_level ve alert_value parametrelerinin değerleri yalnızca bu işlev, uzak konaktan bir uyarı alınarak uyarı alınarak NX_SECURE_TLS_ALERT_RECEIVED (0x114) durumu döndürülen bir TLS API çağrısından hemen sonra çağrılsa geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-643">The values of the alert_level and alert_value parameters are only valid if this function is called immediately following a TLS API call that returned a status of NX_SECURE_TLS_ALERT_RECEIVED (0x114) indicating that an alert was received from the remote host.</span></span>

<span data-ttu-id="1c3ae-644">Yerel ana bilgisayar TLS bir uyarı gönderirse, TLS uyarı değerleri belirli saldırı türlerini (örneğin, "doldurma kahini" saldırısı veya benzeri) önlemek için kasıtlı olarak belirsiz bırakılana kadar, döndürülen hata kodları gerçek hatayı TLS uyarısının kendisine göre çok daha açıklayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-644">Note that if the local host TLS sends an alert, the returned error codes are far more descriptive of the actual error than the TLS alert itself because TLS alert values are intentionally left ambiguous to prevent certain types of attack (such as a "padding oracle" attack or similar).</span></span>

<span data-ttu-id="1c3ae-645">Uyarı düzeyi yalnızca iki değerden birini alır: NX_SECURE_TLS_ALERT_LEVEL_WARNING (0x1) veya NX_SECURE_TLS_ALERT_LEVEL_FATAL (0x2).</span><span class="sxs-lookup"><span data-stu-id="1c3ae-645">The alert level only takes one of two values: NX_SECURE_TLS_ALERT_LEVEL_WARNING (0x1) or NX_SECURE_TLS_ALERT_LEVEL_FATAL (0x2).</span></span> <span data-ttu-id="1c3ae-646">Bazı uzantı yapılandırma durumlarında uyarı olarak da düşünülebilir ancak genel olarak yalnızca CloseNotify Uyarısına (TLS oturumunun başarılı bir şekilde son verildiğini belirtmek için kullanılır) "Uyarı" düzeyi verilir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-646">In general, only the CloseNotify Alert (used to indicate a successful end to a TLS session) will be given a level of "Warning" though some extension configuration situations may also be considered warnings.</span></span> <span data-ttu-id="1c3ae-647">Uyarıların büyük çoğunluğu olası bir güvenlik hatasına işaret eden "Önemli" olur ve TLS bağlantısının (el sıkışma veya oturum) hemen kapatılmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-647">The vast majority of alerts will be "Fatal" indicating a potential security failure and resulting in immediate closure of the TLS connection (handshake or session).</span></span>

<span data-ttu-id="1c3ae-648">TLS uyarı değerleri TLS RFC'lerde tanımlanmıştır; rfc 5246 (TLSv1.2) listesinden başvuru için:</span><span class="sxs-lookup"><span data-stu-id="1c3ae-648">The TLS alert values are defined in the TLS RFCs, here is the list from RFC 5246 (TLSv1.2) for reference:</span></span>

| <span data-ttu-id="1c3ae-649">Uyarı Adı</span><span class="sxs-lookup"><span data-stu-id="1c3ae-649">Alert Name</span></span>                     | <span data-ttu-id="1c3ae-650">Değer</span><span class="sxs-lookup"><span data-stu-id="1c3ae-650">Value</span></span> | <span data-ttu-id="1c3ae-651">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1c3ae-651">Description</span></span>                                                                                                                                                  |
| ---------------------------------- | --------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <span data-ttu-id="1c3ae-652">close_notify</span><span class="sxs-lookup"><span data-stu-id="1c3ae-652">close_notify</span></span>                  | <span data-ttu-id="1c3ae-653">0</span><span class="sxs-lookup"><span data-stu-id="1c3ae-653">0</span></span>     | <span data-ttu-id="1c3ae-654">Hata yok, oturum sonunun başarılı olduğunu gösteriyor</span><span class="sxs-lookup"><span data-stu-id="1c3ae-654">No error, indicates successful session end</span></span>                                                                                                                   |
| <span data-ttu-id="1c3ae-655">unexpected_message</span><span class="sxs-lookup"><span data-stu-id="1c3ae-655">unexpected_message</span></span>            | <span data-ttu-id="1c3ae-656">10</span><span class="sxs-lookup"><span data-stu-id="1c3ae-656">10</span></span>    | <span data-ttu-id="1c3ae-657">TLS beklenmeyen veya sıranın dışında iletisi aldı</span><span class="sxs-lookup"><span data-stu-id="1c3ae-657">TLS received an unexpected or out-of-order message</span></span>                                                                                                           |
| <span data-ttu-id="1c3ae-658">bad_record_mac</span><span class="sxs-lookup"><span data-stu-id="1c3ae-658">bad_record_mac</span></span>               | <span data-ttu-id="1c3ae-659">20</span><span class="sxs-lookup"><span data-stu-id="1c3ae-659">20</span></span>    | <span data-ttu-id="1c3ae-660">Şifre çözme ve/veya MAC doğrulaması başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="1c3ae-660">Decryption and/or MAC verification failed</span></span>                                                                                                                    |
| <span data-ttu-id="1c3ae-661">decryption_failed_RESERVED</span><span class="sxs-lookup"><span data-stu-id="1c3ae-661">decryption_failed_RESERVED</span></span>   | <span data-ttu-id="1c3ae-662">21</span><span class="sxs-lookup"><span data-stu-id="1c3ae-662">21</span></span>    | <span data-ttu-id="1c3ae-663">**Kullanım dışı** Şifre çözme başarısız oldu (Oracle saldırılarını doldurma nedeniyle kullanım dışı)</span><span class="sxs-lookup"><span data-stu-id="1c3ae-663">**DEPRECATED** Decryption failed (deprecated due to padding oracle attacks)</span></span>                                                                                      |
| <span data-ttu-id="1c3ae-664">record_overflow</span><span class="sxs-lookup"><span data-stu-id="1c3ae-664">record_overflow</span></span>               | <span data-ttu-id="1c3ae-665">22</span><span class="sxs-lookup"><span data-stu-id="1c3ae-665">22</span></span>    | <span data-ttu-id="1c3ae-666">En fazla TLS kayıt boyutundan daha büyük olan bir kayıt alındı</span><span class="sxs-lookup"><span data-stu-id="1c3ae-666">A record was received that is larger than the TLS maximum record size</span></span>                                                                                        |
| <span data-ttu-id="1c3ae-667">decompression_failure</span><span class="sxs-lookup"><span data-stu-id="1c3ae-667">decompression_failure</span></span>         | <span data-ttu-id="1c3ae-668">30</span><span class="sxs-lookup"><span data-stu-id="1c3ae-668">30</span></span>    | <span data-ttu-id="1c3ae-669">TLS kaydının sıkıştırılması/sıkıştırması açılmasında bir sorunla karşılaşıldı</span><span class="sxs-lookup"><span data-stu-id="1c3ae-669">A problem was encountered in compression/decompression of a TLS record</span></span>                                                                                       |
| <span data-ttu-id="1c3ae-670">handshake_failure</span><span class="sxs-lookup"><span data-stu-id="1c3ae-670">handshake_failure</span></span>             | <span data-ttu-id="1c3ae-671">40</span><span class="sxs-lookup"><span data-stu-id="1c3ae-671">40</span></span>    | <span data-ttu-id="1c3ae-672">Farklı bir uyarı kapsamında olmayan bazı belirtilmeyen bir el sıkışma hatası oluştu</span><span class="sxs-lookup"><span data-stu-id="1c3ae-672">Some unspecified handshake error occurred that isn't covered by a different alert</span></span>                                                                            |
| <span data-ttu-id="1c3ae-673">no_certificate_RESERVED</span><span class="sxs-lookup"><span data-stu-id="1c3ae-673">no_certificate_RESERVED</span></span>      | <span data-ttu-id="1c3ae-674">41</span><span class="sxs-lookup"><span data-stu-id="1c3ae-674">41</span></span>    | <span data-ttu-id="1c3ae-675">TLS 'de **kullanım dışı** (yalnızca SSL)</span><span class="sxs-lookup"><span data-stu-id="1c3ae-675">**DEPRECATED** in TLS (SSL only)</span></span>                                                                                                                                 |
| <span data-ttu-id="1c3ae-676">bad_certificate</span><span class="sxs-lookup"><span data-stu-id="1c3ae-676">bad_certificate</span></span>               | <span data-ttu-id="1c3ae-677">42</span><span class="sxs-lookup"><span data-stu-id="1c3ae-677">42</span></span>    | <span data-ttu-id="1c3ae-678">Alınan bir sertifika geçersiz biçimlendirme veya imza içeriyordu</span><span class="sxs-lookup"><span data-stu-id="1c3ae-678">A certificate that was received contained invalid formatting or signatures</span></span>                                                                                   |
| <span data-ttu-id="1c3ae-679">unsupported_certificate</span><span class="sxs-lookup"><span data-stu-id="1c3ae-679">unsupported_certificate</span></span>       | <span data-ttu-id="1c3ae-680">43</span><span class="sxs-lookup"><span data-stu-id="1c3ae-680">43</span></span>    | <span data-ttu-id="1c3ae-681">Geçersiz bir tür (örneğin, TLS sunucu kimlik doğrulaması için kullanılan yalnızca oturum açma sertifikası) olan bir sertifika alındı</span><span class="sxs-lookup"><span data-stu-id="1c3ae-681">A certificate was received that was of an invalid type (e.g. signing-only certificate used for TLS server authentication)</span></span>                                    |
| <span data-ttu-id="1c3ae-682">certificate_revoked</span><span class="sxs-lookup"><span data-stu-id="1c3ae-682">certificate_revoked</span></span>           | <span data-ttu-id="1c3ae-683">44</span><span class="sxs-lookup"><span data-stu-id="1c3ae-683">44</span></span>    | <span data-ttu-id="1c3ae-684">Sertifika durumu (bir CRL veya OCSP tarafından sağlandığı gibi) "iptal edildi" olarak belirtilmiştir</span><span class="sxs-lookup"><span data-stu-id="1c3ae-684">The certificate status (as provided by a CRL or OCSP) was indicated as being "revoked"</span></span>                                                                       |
| <span data-ttu-id="1c3ae-685">certificate_expired</span><span class="sxs-lookup"><span data-stu-id="1c3ae-685">certificate_expired</span></span>           | <span data-ttu-id="1c3ae-686">45</span><span class="sxs-lookup"><span data-stu-id="1c3ae-686">45</span></span>    | <span data-ttu-id="1c3ae-687">Alınan sertifika geçerli bir tarih aralığı dışındaydı (henüz geçerli değil veya kullanım tarihi belirtilmemiş)</span><span class="sxs-lookup"><span data-stu-id="1c3ae-687">The received certificate was outside it's valid date range (either not valid yet or expired)</span></span>                                                                 |
| <span data-ttu-id="1c3ae-688">certificate_unknown</span><span class="sxs-lookup"><span data-stu-id="1c3ae-688">certificate_unknown</span></span>           | <span data-ttu-id="1c3ae-689">46</span><span class="sxs-lookup"><span data-stu-id="1c3ae-689">46</span></span>    | <span data-ttu-id="1c3ae-690">Diğer uyarıların kapsamadığı bilinmeyen bir sertifika sorunuyla karşılaşıldı</span><span class="sxs-lookup"><span data-stu-id="1c3ae-690">Some unknown certificate issue was encountered that was not covered by other alerts</span></span>                                                                          |
| <span data-ttu-id="1c3ae-691">illegal_parameter</span><span class="sxs-lookup"><span data-stu-id="1c3ae-691">illegal_parameter</span></span>             | <span data-ttu-id="1c3ae-692">47</span><span class="sxs-lookup"><span data-stu-id="1c3ae-692">47</span></span>    | <span data-ttu-id="1c3ae-693">TLS el sıkışması içinde bazı yapılandırma veya anlaşmalı değer geçersiz veya aralık dışında</span><span class="sxs-lookup"><span data-stu-id="1c3ae-693">Some configuration or negotiated value in the TLS handshake was invalid or out of range</span></span>                                                                      |
| <span data-ttu-id="1c3ae-694">unknown_ca</span><span class="sxs-lookup"><span data-stu-id="1c3ae-694">unknown_ca</span></span>                    | <span data-ttu-id="1c3ae-695">48</span><span class="sxs-lookup"><span data-stu-id="1c3ae-695">48</span></span>    | <span data-ttu-id="1c3ae-696">Alınan kimlik sertifikası, güvenilen bir kök CA sertifikasına bir sertifika zinciri aracılığıyla izlenmedi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-696">The received identity certificate could not be traced via a certificate chain to a trusted root CA certificate.</span></span>                                              |
| <span data-ttu-id="1c3ae-697">access_denied</span><span class="sxs-lookup"><span data-stu-id="1c3ae-697">access_denied</span></span>                 | <span data-ttu-id="1c3ae-698">49</span><span class="sxs-lookup"><span data-stu-id="1c3ae-698">49</span></span>    | <span data-ttu-id="1c3ae-699">Geçerli bir sertifikanın alınmıştır ancak uygulama erişim denetimi, istenen kaynaklar için sertifikanın geçersiz olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-699">Indicates a valid certificate was received but application access control indicated that the certificate was invalid for the requested resources.</span></span>            |
| <span data-ttu-id="1c3ae-700">decode_error</span><span class="sxs-lookup"><span data-stu-id="1c3ae-700">decode_error</span></span>                  | <span data-ttu-id="1c3ae-701">50</span><span class="sxs-lookup"><span data-stu-id="1c3ae-701">50</span></span>    | <span data-ttu-id="1c3ae-702">TLS üst bilgisinde veya el sıkışma iletisinde yer alan bir alan veya değer aralık dışında veya geçersizdi ve bu da TLS kaydının kodunun çözülerek hataya neden oldu.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-702">Some field or value in a TLS header or handshake message was out of range or invalid, leading to a failure in decoding of a TLS record.</span></span>                      |
| <span data-ttu-id="1c3ae-703">decrypt_error</span><span class="sxs-lookup"><span data-stu-id="1c3ae-703">decrypt_error</span></span>                 | <span data-ttu-id="1c3ae-704">51</span><span class="sxs-lookup"><span data-stu-id="1c3ae-704">51</span></span>    | <span data-ttu-id="1c3ae-705">TLS el sıkışması sırasında bir imza veya Tamamlandı ileti karması doğrulanamadı.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-705">A signature or Finished message hash during the TLS handshake could not be verified.</span></span>                                                                         |
| <span data-ttu-id="1c3ae-706">export_restriction_RESERVED</span><span class="sxs-lookup"><span data-stu-id="1c3ae-706">export_restriction_RESERVED</span></span>  | <span data-ttu-id="1c3ae-707">60</span><span class="sxs-lookup"><span data-stu-id="1c3ae-707">60</span></span>    | <span data-ttu-id="1c3ae-708">TLSv1.2'de KULLANıM DıŞı</span><span class="sxs-lookup"><span data-stu-id="1c3ae-708">DEPRECATED in TLSv1.2</span></span>                                                                                                                                        |
| <span data-ttu-id="1c3ae-709">protocol_version</span><span class="sxs-lookup"><span data-stu-id="1c3ae-709">protocol_version</span></span>              | <span data-ttu-id="1c3ae-710">70</span><span class="sxs-lookup"><span data-stu-id="1c3ae-710">70</span></span>    | <span data-ttu-id="1c3ae-711">El sıkışma sırasında anlaştırılacak TLS protokol sürümü tanınıyor ancak desteklenmiyor (örneğin TLSv1.0 sunulsa da etkinleştirilmedi).</span><span class="sxs-lookup"><span data-stu-id="1c3ae-711">The TLS protocol version negotiated during the handshake is recognized but not supported (e.g. TLSv1.0 was presented but not enabled).</span></span>                       |
| <span data-ttu-id="1c3ae-712">insufficient_security</span><span class="sxs-lookup"><span data-stu-id="1c3ae-712">insufficient_security</span></span>         | <span data-ttu-id="1c3ae-713">71</span><span class="sxs-lookup"><span data-stu-id="1c3ae-713">71</span></span>    | <span data-ttu-id="1c3ae-714">Güvenli şifrelemelerin olmaması nedeniyle el sıkışması başarısız olduğunda gönderilir (örneğin, anahtar boyutu uygulama gereksinimleri için çok küçüktür)</span><span class="sxs-lookup"><span data-stu-id="1c3ae-714">Sent whenever a handshake fails due to a lack of secure ciphers (e.g. key size is too small for the application requirements)</span></span>                                |
| <span data-ttu-id="1c3ae-715">internal_error</span><span class="sxs-lookup"><span data-stu-id="1c3ae-715">internal_error</span></span>                | <span data-ttu-id="1c3ae-716">80</span><span class="sxs-lookup"><span data-stu-id="1c3ae-716">80</span></span>    | <span data-ttu-id="1c3ae-717">TLS olmayan bazı hata (örneğin bellek ayırma sorunları, uygulama sorunları) bir TLS oturumunun bozuk olarak ortaya çıktı.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-717">Some non-TLS error (e.g. memory allocation problems, application issues) occurred resulting in a broken TLS session.</span></span>                                         |
| <span data-ttu-id="1c3ae-718">user_canceled</span><span class="sxs-lookup"><span data-stu-id="1c3ae-718">user_canceled</span></span>                 | <span data-ttu-id="1c3ae-719">90</span><span class="sxs-lookup"><span data-stu-id="1c3ae-719">90</span></span>    | <span data-ttu-id="1c3ae-720">El sıkışma işlemi tamamlanmadan önce TLS oturumu bir kullanıcı veya uygulama tarafından iptal edilirse döndürülür (CloseNotify'a benzer).</span><span class="sxs-lookup"><span data-stu-id="1c3ae-720">Returned if the TLS session is cancelled by a user or application before the handshake is complete (similar to CloseNotify).</span></span>                                 |
| <span data-ttu-id="1c3ae-721">no_renegotiation</span><span class="sxs-lookup"><span data-stu-id="1c3ae-721">no_renegotiation</span></span>              | <span data-ttu-id="1c3ae-722">100</span><span class="sxs-lookup"><span data-stu-id="1c3ae-722">100</span></span>   | <span data-ttu-id="1c3ae-723">Uzak konağın, bir yeniden anlaşma isteğine yanıt olarak TLS yeniden anlaşma el sıkışmaları gerçekleştirmesini istemediğinden bağımsız olarak.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-723">Indiates that the remote host is not willing to perform TLS renegotiation handshakes in response to a renegotiation request.</span></span>                                 |
| <span data-ttu-id="1c3ae-724">unsupported_extension</span><span class="sxs-lookup"><span data-stu-id="1c3ae-724">unsupported_extension</span></span>         | <span data-ttu-id="1c3ae-725">110</span><span class="sxs-lookup"><span data-stu-id="1c3ae-725">110</span></span>   | <span data-ttu-id="1c3ae-726">Bir TLS Istemcisi ilk ClientHello (sunucuda bir sorun olduğunu gösterir) için açıkça sorulmayan uzantıları içeren bir ServerHello alırsa gönderilir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-726">Sent if a TLS Client receives a ServerHello containing extensions not explicitly asked for in the initial ClientHello (indicating the server has a problem).</span></span> |

### <a name="parameters"></a><span data-ttu-id="1c3ae-727">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1c3ae-727">Parameters</span></span>

- <span data-ttu-id="1c3ae-728">**session_ptr** Bir TLS oturum örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-728">**session_ptr** Pointer to a TLS Session instance.</span></span>
- <span data-ttu-id="1c3ae-729">**alert_level** Alınan uyarının düzeyini döndürün (uyarı veya önemli).</span><span class="sxs-lookup"><span data-stu-id="1c3ae-729">**alert_level** Return the level of the received alert (warning or fatal).</span></span>
- <span data-ttu-id="1c3ae-730">**alert_value** Alınan uyarının değerini döndürür (bkz. tablo).</span><span class="sxs-lookup"><span data-stu-id="1c3ae-730">**alert_value** Return the value of the received alert (see table).</span></span>

### <a name="return-values"></a><span data-ttu-id="1c3ae-731">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-731">Return Values</span></span>

- <span data-ttu-id="1c3ae-732">**NX_SUCCESS** (0x00) başarılı işlemi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-732">**NX_SUCCESS** (0x00) Successful operation.</span></span>
- <span data-ttu-id="1c3ae-733">**NX_PTR_ERROR** (0x07) geçersiz TLS oturumu.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-733">**NX_PTR_ERROR** (0x07) Invalid TLS session.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1c3ae-734">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="1c3ae-734">Allowed From</span></span>

<span data-ttu-id="1c3ae-735">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="1c3ae-735">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1c3ae-736">Örnek</span><span class="sxs-lookup"><span data-stu-id="1c3ae-736">Example</span></span>

```C
/* Return values. */
UINT status, alert_level, alert_value;


/* Start a TLS session.  */
status =  nx_secure_tls_session_start(&tls_session, &tcp_socket, NX_WAIT_FOREVER);

/* Check for “alert received” error. */
if(status == NX_SECURE_TLS_ALERT_RECEIVED)
{

        /* Get the alert level and value. */
        status =  nx_secure_tls_session_alert_value_get(&tls_session,
                                             &alert_level, &alert_value);

        /* Print out the received alert level and value. */
        printf("Alert recieved. Value: %d, Level: %d\n", alert_value,
                alert_level);
}
else if(status != NX_SUCCESS)
{
    /* Additional error handling. */
}
```

### <a name="see-also"></a><span data-ttu-id="1c3ae-737">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-737">See Also</span></span>

- <span data-ttu-id="1c3ae-738">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="1c3ae-738">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="1c3ae-739">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="1c3ae-739">nx_secure_tls_session_send</span></span>
- <span data-ttu-id="1c3ae-740">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="1c3ae-740">nx_secure_tls_session_receive</span></span>

## <a name="nx_secure_tls_session_certificate_callback_set"></a><span data-ttu-id="1c3ae-741">nx_secure_tls_session_certificate_callback_set</span><span class="sxs-lookup"><span data-stu-id="1c3ae-741">nx_secure_tls_session_certificate_callback_set</span></span>

<span data-ttu-id="1c3ae-742">Ek sertifika doğrulaması için kullanılacak TLS için bir geri çağırma ayarlayın</span><span class="sxs-lookup"><span data-stu-id="1c3ae-742">Set up a callback for TLS to use for additional certificate validation</span></span>

### <a name="prototype"></a><span data-ttu-id="1c3ae-743">Prototype</span><span class="sxs-lookup"><span data-stu-id="1c3ae-743">Prototype</span></span>

```C
UINT  nx_secure_tls_ session_certificate_callback_set (
                  NX_SECURE_TLS_SESSION *tls_session,
                  ULONG (*func_ptr)(NX_SECURE_TLS_SESSION *session,
                                    NX_SECURE_X509_CERT *certificate));
```

### <a name="description"></a><span data-ttu-id="1c3ae-744">Description</span><span class="sxs-lookup"><span data-stu-id="1c3ae-744">Description</span></span>

<span data-ttu-id="1c3ae-745">Bu hizmet, uzak bir ana bilgisayardan bir sertifika alındığında, uygulamanın DNS doğrulaması, sertifika iptali ve sertifika ilkesi zorlaması gibi doğrulama denetimleri gerçekleştirmesine izin veren TLS oturumuna bir işlev işaretçisi atar.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-745">This service assigns a function pointer to a TLS session that TLS will invoke when a certificate is received from a remote host, allowing the application to perform validation checks such as DNS validation, certificate revocation, and certificate policy enforcement.</span></span>

<span data-ttu-id="1c3ae-746">NetX güvenli TLS, sertifikanın TLS güvenilen sertifika deposundaki bir sertifikaya izlenip izlenmemesini sağlamak için geri çağırma işlemini çağırmadan önce sertifikada temel X. 509.952 yolu doğrulamasını yapar, ancak diğer tüm doğrulamalar bu geri arama tarafından işlenir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-746">NetX Secure TLS will perform basic X.509 path validation on the certificate before invoking the callback to assure that the certificate can be traced to a certificate in the TLS trusted certificate store, but all other validation will be handled by this callback.</span></span>

<span data-ttu-id="1c3ae-747">Geri arama, TLS oturum işaretçisini ve uzak ana bilgisayar kimliği sertifikası (sertifika zincirindeki yaprak) için bir işaretçi sağlar.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-747">The callback provides the TLS session pointer and a pointer to the remote host identity certificate (the leaf in the certificate chain).</span></span> <span data-ttu-id="1c3ae-748">Tüm doğrulama başarılı olursa geri çağırma NX_SUCCESS döndürmelidir, aksi takdirde doğrulama hatasını gösteren bir hata kodu döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-748">The callback should return NX_SUCCESS if all validation is successful, otherwise it should return an error code indicating the validation failure.</span></span> <span data-ttu-id="1c3ae-749">NX_SUCCESS dışındaki herhangi bir değer, TLS el sıkışmasına hemen iptal edilmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-749">Any value other than NX_SUCCESS will cause the TLS handshake to immediately abort.</span></span>

### <a name="parameters"></a><span data-ttu-id="1c3ae-750">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1c3ae-750">Parameters</span></span>

- <span data-ttu-id="1c3ae-751">**session_ptr** Daha önce oluşturulmuş bir TLS oturum örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-751">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="1c3ae-752">**func_ptr** Sertifika doğrulama geri çağırma işlevinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-752">**func_ptr** Pointer to the certificate validation callback function.</span></span>

### <a name="return-values"></a><span data-ttu-id="1c3ae-753">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-753">Return Values</span></span>

- <span data-ttu-id="1c3ae-754">**NX_SUCCESS** (0x00) İşlev işaretçisinin başarıyla ayırması.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-754">**NX_SUCCESS** (0x00) Successful allocation of Function pointer.</span></span>
- <span data-ttu-id="1c3ae-755">**NX_PTR_ERROR** (0x07) Geçersiz TLS oturum işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-755">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1c3ae-756">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="1c3ae-756">Allowed From</span></span>

<span data-ttu-id="1c3ae-757">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="1c3ae-757">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1c3ae-758">Örnek</span><span class="sxs-lookup"><span data-stu-id="1c3ae-758">Example</span></span>

```C
/* Callback routine used to perform additional checks on a certificate. */
ULONG certificate_callback(NX_SECURE_TLS_SESSION *session, NX_SECURE_X509_CERT
*certificate)
{
    /* Certificate validation checking goes here. */
    return(NX_SUCCESS);
}

/* In TLS setup routine. */
{
        /* Add callback to TLS session.  */
        status =  nx_secure_tls_session_certificate_callback_set(&tls_session,
                                                            certificate_callback);

        /* If status is NX_SUCCESS the certificate callback was added.  */
}
```

### <a name="see-also"></a><span data-ttu-id="1c3ae-759">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-759">See Also</span></span>

- <span data-ttu-id="1c3ae-760">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="1c3ae-760">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="1c3ae-761">nx_secure_x509_common_name_dns_check</span><span class="sxs-lookup"><span data-stu-id="1c3ae-761">nx_secure_x509_common_name_dns_check</span></span>
- <span data-ttu-id="1c3ae-762">nx_secure_x509_crl_revocation_check</span><span class="sxs-lookup"><span data-stu-id="1c3ae-762">nx_secure_x509_crl_revocation_check</span></span>

## <a name="nx_secure_tls_session_client_callback_set"></a><span data-ttu-id="1c3ae-763">nx_secure_tls_session_client_callback_set</span><span class="sxs-lookup"><span data-stu-id="1c3ae-763">nx_secure_tls_session_client_callback_set</span></span>

<span data-ttu-id="1c3ae-764">TLS İstemci el sıkışması başlangıcında çağırmak için TLS için bir geri çağırma ayarlayın</span><span class="sxs-lookup"><span data-stu-id="1c3ae-764">Set up a callback for TLS to invoke at the beginning of a TLS Client handshake</span></span>

### <a name="prototype"></a><span data-ttu-id="1c3ae-765">Prototype</span><span class="sxs-lookup"><span data-stu-id="1c3ae-765">Prototype</span></span>

```C
UINT  nx_secure_tls_ session_client_callback_set (
                  NX_SECURE_TLS_SESSION *tls_session,
                  ULONG (*func_ptr)(NX_SECURE_TLS_SESSION *tls_session,
                                    NX_SECURE_TLS_HELLO_EXTENSION
                                    *extensions, UINT num_extensions));
```

### <a name="description"></a><span data-ttu-id="1c3ae-766">Description</span><span class="sxs-lookup"><span data-stu-id="1c3ae-766">Description</span></span>

<span data-ttu-id="1c3ae-767">Bu hizmet, BIR TLS İstemci el sıkışması ServerHelloDone iletisi aldığı zaman TLS'nin çağıracak olduğu bir TLS oturumuna işlev işaretçisi atar.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-767">This service assigns a function pointer to a TLS session that TLS will invoke when a TLS Client handshake has received a ServerHelloDone message.</span></span> <span data-ttu-id="1c3ae-768">Geri çağırma işlevi, bir uygulamanın alınan ServerHello iletilerinden giriş veya karar alma gerektiren tüm TLS uzantılarını işlemesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-768">The callback function allows an application to process any TLS extensions from the received ServerHello message that require input or decision making.</span></span>

<span data-ttu-id="1c3ae-769">Geri çağırma TLS oturum denetim bloğu ve bir dizi farklı nesne NX_SECURE_TLS_HELLO_EXTENSION yürütülür.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-769">The callback is executed with the invoking TLS session control block and an array of NX_SECURE_TLS_HELLO_EXTENSION objects.</span></span> <span data-ttu-id="1c3ae-770">Uzantı nesneleri dizisinin, belirli bir uzantıyı bulup ayrıştıracak bir yardımcı işleve geçirileme amacı vardır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-770">The array of extension objects is intended to be passed into a helper function that will find and parse a specific extension.</span></span> <span data-ttu-id="1c3ae-771">Şu anda NetX Secure'de TLS İstemcisi girişi gerektiren belirli uzantılar yoktur, ancak uygulama tasarımcılarının kullanılabilir hale gelen özel veya yeni uzantıları işlemesi için geri çağırma kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-771">Currently, there are no specific extensions supported in NetX Secure that require TLS Client input, but the callback is available for application designers to handle custom or new extensions that may become available.</span></span> <span data-ttu-id="1c3ae-772">Merhaba iletilerde sağlanan TLS uzantılarını ayrıştıran örnek bir yardımcı işlev için bkz. *nx_secure_tls_session_sni_extension_parse.*.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-772">For an example helper function that parses TLS extensions provided in hello messages, see *nx_secure_tls_session_sni_extension_parse*.</span></span>

<span data-ttu-id="1c3ae-773">İstemci geri çağırma, uzak sunucunun bir sertifika  isteğinde bulunuyor olması ve TLS İstemcisi'nin belirli bir sertifikayı seçmesine izin vermek için bilgi sağladığında TLS İstemcisi için nx_secure_tls_active_certificate_set kullanarak etkin kimlik sertifikasını seçmek için de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-773">The client callback may also be used to select the active identity certificate using *nx_secure_tls_active_certificate_set* for the TLS Client in the event that the remote server has requested a certificate and provided information to allow the TLS Client to select a specific certificate.</span></span> <span data-ttu-id="1c3ae-774">Daha fazla bilgi için nx_secure_tls_active_certificate_set için başvuruya bakın.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-774">See the reference for nx_secure_tls_active_certificate_set for more information.</span></span>

### <a name="parameters"></a><span data-ttu-id="1c3ae-775">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1c3ae-775">Parameters</span></span>

- <span data-ttu-id="1c3ae-776">**session_ptr** Daha önce oluşturulmuş bir TLS Oturumu örneğinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-776">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="1c3ae-777">**func_ptr** TLS İstemci geri çağırma işlevinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-777">**func_ptr** Pointer to the TLS Client callback function.</span></span>

### <a name="return-values"></a><span data-ttu-id="1c3ae-778">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-778">Return Values</span></span>

- <span data-ttu-id="1c3ae-779">**NX_SUCCESS** (0x00) İşlev işaretçisinin başarıyla ayırması.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-779">**NX_SUCCESS** (0x00) Successful allocation of function pointer.</span></span>
- <span data-ttu-id="1c3ae-780">**NX_PTR_ERROR** (0x07) geçersiz TLS oturum işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-780">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1c3ae-781">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="1c3ae-781">Allowed From</span></span>

<span data-ttu-id="1c3ae-782">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="1c3ae-782">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1c3ae-783">Örnek</span><span class="sxs-lookup"><span data-stu-id="1c3ae-783">Example</span></span>

```C
/* Callback routine used to process ServerHello extensions and perform other
   runtime actions at the beginning of a TLS handshake (such as selecting an
   identify certificate to provide to the server). */

ULONG tls_client_callback(NX_SECURE_TLS_SESSION *session,
                          NX_SECURE_TLS_HELLO_EXTENSION *extensions, UINT
                          num_extensions)
{

    /* Extension parsing would go here. */

    /* Set an active identity certificate – the certificate should have been added
       to the local store at application start with
       nx_secure_tls_local_certificate_add. */
    nx_secure_tls_active_certificate_set(session, &global_identity_certificate);

    return(NX_SUCCESS);
}

/* TLS setup routine. */
UINT tls_setup(NX_SECURE_TLS_SESSION *tls_session)
{
    /* Add callback to TLS session.  */
    status =  nx_secure_tls_session_client_callback_set(tls_session,
                                                        client_callback);

    /* If status is NX_SUCCESS the callback was added and will be invoked once
       a ServerHelloDone message is received. */

    return(status);
}
```

### <a name="see-also"></a><span data-ttu-id="1c3ae-784">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-784">See Also</span></span>

- <span data-ttu-id="1c3ae-785">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="1c3ae-785">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="1c3ae-786">nx_secure_tls_session_server_callback_set</span><span class="sxs-lookup"><span data-stu-id="1c3ae-786">nx_secure_tls_session_server_callback_set</span></span>
- <span data-ttu-id="1c3ae-787">nx_secure_tls_active_certificate_set</span><span class="sxs-lookup"><span data-stu-id="1c3ae-787">nx_secure_tls_active_certificate_set</span></span>

## <a name="nx_secure_tls_session_x509_client_verify_configure"></a><span data-ttu-id="1c3ae-788">nx_secure_tls_session_x509_client_verify_configure</span><span class="sxs-lookup"><span data-stu-id="1c3ae-788">nx_secure_tls_session_x509_client_verify_configure</span></span>

<span data-ttu-id="1c3ae-789">İstemci X. 509.440 doğrulamasını etkinleştir ve istemci sertifikaları için alan ayır</span><span class="sxs-lookup"><span data-stu-id="1c3ae-789">Enable client X.509 verification and allocate space for client certificates</span></span>

### <a name="prototype"></a><span data-ttu-id="1c3ae-790">Prototype</span><span class="sxs-lookup"><span data-stu-id="1c3ae-790">Prototype</span></span>

```C
UINT  nx_secure_tls_session_x509_client_verify_configure(
                  NX_SECURE_TLS_SESSION *session_ptr,
                  UINT certs_number, VOID *certificate_buffer,
                  ULONG buffer_size);
```

### <a name="description"></a><span data-ttu-id="1c3ae-791">Description</span><span class="sxs-lookup"><span data-stu-id="1c3ae-791">Description</span></span>

<span data-ttu-id="1c3ae-792">Bu hizmet, bir TLS sunucu örneği için isteğe bağlı X. 509.440 Istemci kimlik doğrulamasını sunar.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-792">This service enables the optional X.509 Client Authentication for a TLS Server instance.</span></span> <span data-ttu-id="1c3ae-793">Ayrıca, uzak istemci konaktan gelen sertifika zincirlerini işlemek için gereken alanı ayırır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-793">It also allocates the space needed to process incoming certificate chains from the remote client host.</span></span> <span data-ttu-id="1c3ae-794">Uzak istemci tarafından sağlanan sertifikalar, hizmet nx_secure_tls_trusted_certificate_add atanmış olan TLS sunucusu örneğinin güvenilen sertifikalarına karşı doğrulanır *.*</span><span class="sxs-lookup"><span data-stu-id="1c3ae-794">The certificates supplied by the remote client will be verified against the TLS server instance's trusted certificates, assigned with the service *nx_secure_tls_trusted_certificate_add.*</span></span>

<span data-ttu-id="1c3ae-795">TLS Istemci modu için, uzak sertifika ayırma gereklidir ve bunun yerine hizmet *nx_secure_tls_remote_certificate_buffer_allocate* kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-795">For TLS Client mode, remote certificate allocation is required and the service *nx_secure_tls_remote_certificate_buffer_allocate* should be used instead.</span></span> <span data-ttu-id="1c3ae-796">Bir TLS Istemci örneğinde X. 509.440 Istemci kimlik doğrulamasının etkinleştirilmesi hiçbir etkiye sahip olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-796">Enabling X.509 Client Authentication on a TLS Client instance will have no effect.</span></span>

<span data-ttu-id="1c3ae-797">*Certificate_buffer* parametresi, gelen uzak sertifikaları ve bu sertifikalar için gereken denetim bloklarını depolamak için ayrılan alana işaret eder.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-797">The *certificate_buffer* parameter points to space allocated to store the incoming remote certificates and the control blocks needed for those certificates.</span></span> <span data-ttu-id="1c3ae-798">Arabellek, her sertifikaya verilen eşit bir bölüme sahip sertifika (*certs_number*) sayısına bölünür.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-798">The buffer will be divided by the number of certificates (*certs_number*) with an equal portion given to each certificate.</span></span> <span data-ttu-id="1c3ae-799">*Buffer_size* parametresi arabelleğin boyutunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-799">The *buffer_size* parameter indicates the size of the buffer.</span></span> <span data-ttu-id="1c3ae-800">Aşağıdaki formül ile, gereken alan bulunabilir:</span><span class="sxs-lookup"><span data-stu-id="1c3ae-800">The space needed can be found with the following formula:</span></span>

```C
buffer_size = (<expected max number of certificates in chain>) *
             (sizeof(NX_SECURE_X509_CERT) + <max cert size>)
```

<span data-ttu-id="1c3ae-801">İmzalar için SHA-256 kullanan 2048 bitin RSA anahtarlarına sahip tipik sertifikalar, 1000-2000 bayt aralığındadır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-801">Typical certificates with RSA keys of 2048 bits using SHA-256 for signatures are in the range of 1000-2000 bytes.</span></span> <span data-ttu-id="1c3ae-802">Arabellek, her sertifika için en az sayıda tutmaya yetecek kadar büyük olmalıdır, ancak uzak ana bilgisayar sertifikalarına bağlı olarak, önemli ölçüde daha küçük veya daha büyük olabilir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-802">The buffer should be large enough to at least hold that size for each certificate, but depending on the remote host certificates may be significantly smaller or larger.</span></span> <span data-ttu-id="1c3ae-803">Arabellek gelen sertifikayı tutmak için çok küçük olduğunda, TLS el sıkışması bir hatayla sona erdirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-803">Note that if the buffer is too small to hold the incoming certificate, the TLS handshake will end with an error.</span></span>

### <a name="parameters"></a><span data-ttu-id="1c3ae-804">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1c3ae-804">Parameters</span></span>

- <span data-ttu-id="1c3ae-805">**session_ptr** Daha önce oluşturulmuş bir TLS oturum örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-805">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="1c3ae-806">**certs_number** Sağlanan arabellekten ayrılacak sertifika sayısı.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-806">**certs_number** Number of certificates to allocate from the provided buffer.</span></span>
- <span data-ttu-id="1c3ae-807">**certificate_buffer** Uzak bir konaktan alınan sertifikaları tutmak için bir arabelleğe işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-807">**certificate_buffer** Pointer to a buffer to hold certificates received from a remote host.</span></span>
- <span data-ttu-id="1c3ae-808">**buffer_size** Sertifika arabelleğinin boyutu.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-808">**buffer_size** Size of the certificate buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="1c3ae-809">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-809">Return Values</span></span>

- <span data-ttu-id="1c3ae-810">**NX_SUCCESS** (0x00)Başarılı sertifika ayırma.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-810">**NX_SUCCESS** (0x00)Successful allocation of certificate.</span></span>
- <span data-ttu-id="1c3ae-811">**NX_PTR_ERROR** (0x07) Geçersiz TLS oturumu veya arabellek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-811">**NX_PTR_ERROR** (0x07) Invalid TLS session or buffer pointer.</span></span>
- <span data-ttu-id="1c3ae-812">**NX_SECURE_TLS_INSUFFICIENT_CERT_SPACE** (0x12D) Sağlanan arabellek çok küçüktü.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-812">**NX_SECURE_TLS_INSUFFICIENT_CERT_SPACE** (0x12D) The supplied buffer was too small.</span></span>
- <span data-ttu-id="1c3ae-813">**NX_INVALID_PARAMETERS** (0x4D) Arabellek istenen sayıda sertifikayı tutmak için çok küçüktü.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-813">**NX_INVALID_PARAMETERS** (0x4D) The buffer was too small to hold the desired number of certificates.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1c3ae-814">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="1c3ae-814">Allowed From</span></span>

<span data-ttu-id="1c3ae-815">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="1c3ae-815">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1c3ae-816">Örnek</span><span class="sxs-lookup"><span data-stu-id="1c3ae-816">Example</span></span>

```C
/* Buffer space to hold the incoming certificates. */
#define CERTIFICATE_NUMBER    (2)
#define CERTIFICATE_SIZE      (2000)
#define BUFFER_SIZE          (CERTIFICATE_NUMBER * \
                                (sizeof(NX_SECURE_X509_CERT) + CERTIFICATE_SIZE))
UCHAR certificate_buffer[BUFFER_SIZE];

/* Enable X.509 Client verification and allocate certificate space in our TLS
   Server session.  */
status =  nx_secure_tls_session_x509_client_verify_configure(&tls_session,
                                                    CERTIFICATE_NUMBER,
                                                    certificate_buffer,
                                                    BUFFER_SIZE);


/* If status is NX_SUCCESS the buffer was successfully allocated.  */
```

### <a name="see-also"></a><span data-ttu-id="1c3ae-817">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-817">See Also</span></span>

- <span data-ttu-id="1c3ae-818">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="1c3ae-818">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="1c3ae-819">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="1c3ae-819">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="1c3ae-820">nx_secure_tls_remote_certificate_buffer_allocate</span><span class="sxs-lookup"><span data-stu-id="1c3ae-820">nx_secure_tls_remote_certificate_buffer_allocate</span></span>

## <a name="nx_secure_tls_session_client_verify_disable"></a><span data-ttu-id="1c3ae-821">nx_secure_tls_session_client_verify_disable</span><span class="sxs-lookup"><span data-stu-id="1c3ae-821">nx_secure_tls_session_client_verify_disable</span></span>

<span data-ttu-id="1c3ae-822">NetX Güvenli TLS Oturumu için İstemci Sertifikası Kimlik Doğrulamasını Devre Dışı Bırakma</span><span class="sxs-lookup"><span data-stu-id="1c3ae-822">Disable Client Certificate Authentication for a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="1c3ae-823">Prototype</span><span class="sxs-lookup"><span data-stu-id="1c3ae-823">Prototype</span></span>

```C
UINT  nx_secure_tls_session_client_verify_disable(
                              NX_SECURE_TLS_SESSION *session_ptr);
```

### <a name="description"></a><span data-ttu-id="1c3ae-824">Description</span><span class="sxs-lookup"><span data-stu-id="1c3ae-824">Description</span></span>

<span data-ttu-id="1c3ae-825">Bu hizmet, belirli bir TLS oturumu için İstemci Sertifikası Kimlik Doğrulamasını devre dışı bırakıyor.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-825">This service disables Client Certificate Authentication for a specific TLS session.</span></span> <span data-ttu-id="1c3ae-826">Daha fazla nx_secure_tls_session_client_verify_enable için bkz. Nx_secure_tls_session_client_verify_enable.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-826">See nx_secure_tls_session_client_verify_enable for more information.</span></span>

### <a name="parameters"></a><span data-ttu-id="1c3ae-827">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1c3ae-827">Parameters</span></span>

- <span data-ttu-id="1c3ae-828">**session_ptr** TLS Oturumu örneğinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-828">**session_ptr** Pointer to a TLS Session instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="1c3ae-829">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-829">Return Values</span></span>

- <span data-ttu-id="1c3ae-830">**NX_SUCCESS** (0x00) Başarılı durum değişikliği.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-830">**NX_SUCCESS** (0x00) Successful state change.</span></span>
- <span data-ttu-id="1c3ae-831">**NX_PTR_ERROR** (0x07) Geçersiz TLS oturum işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-831">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1c3ae-832">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="1c3ae-832">Allowed From</span></span>

<span data-ttu-id="1c3ae-833">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="1c3ae-833">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1c3ae-834">Örnek</span><span class="sxs-lookup"><span data-stu-id="1c3ae-834">Example</span></span>

```C
/* Disable client certificate authentication for this TLS session.   */
status = nx_secure_tls_session_client_verify_disable(&tls_session);

/* Any new TLS Server sessions using the tls_session control block will not
request certificates from the remote TLS client.  */
```

### <a name="see-also"></a><span data-ttu-id="1c3ae-835">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-835">See Also</span></span>

- <span data-ttu-id="1c3ae-836">nx_secure_tls_session_client_verify_enable</span><span class="sxs-lookup"><span data-stu-id="1c3ae-836">nx_secure_tls_session_client_verify_enable</span></span>
- <span data-ttu-id="1c3ae-837">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="1c3ae-837">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="1c3ae-838">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="1c3ae-838">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_session_client_verify_enable"></a><span data-ttu-id="1c3ae-839">nx_secure_tls_session_client_verify_enable</span><span class="sxs-lookup"><span data-stu-id="1c3ae-839">nx_secure_tls_session_client_verify_enable</span></span>

<span data-ttu-id="1c3ae-840">NetX güvenli TLS oturumu için Istemci sertifikası kimlik doğrulamasını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="1c3ae-840">Enable Client Certificate Authentication for a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="1c3ae-841">Prototype</span><span class="sxs-lookup"><span data-stu-id="1c3ae-841">Prototype</span></span>

```C
UINT  nx_secure_tls_session_client_verify_enable(
                                NX_SECURE_TLS_SESSION *session_ptr);
```

### <a name="description"></a><span data-ttu-id="1c3ae-842">Description</span><span class="sxs-lookup"><span data-stu-id="1c3ae-842">Description</span></span>

<span data-ttu-id="1c3ae-843">Bu hizmet belirli bir TLS oturumu için Istemci sertifikası kimlik doğrulamasını mümkün bir şekilde sunar.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-843">This service enables Client Certificate Authentication for a specific TLS session.</span></span> <span data-ttu-id="1c3ae-844">Bir TLS sunucu örneği için Istemci sertifikası kimlik doğrulamasını etkinleştirme, TLS sunucusunun ilk TLS el sıkışması sırasında herhangi bir uzak TLS Istemcisinden sertifika istemesine neden olur.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-844">Enabling Client Certificate Authentication for a TLS Server instance will cause the TLS Server to request a certificate from any remote TLS Client during the initial TLS handshake.</span></span> <span data-ttu-id="1c3ae-845">Uzak TLS Istemcisinden alınan sertifikaya, TLS sunucusunun Istemcinin sertifikaya sahip olduğunu doğrulamak için kullandığı bir CertificateVerify iletisi (Bu sertifikayla ilişkili özel anahtara erişimi vardır) ile birlikte gönderilir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-845">The certificate received from the remote TLS Client is accompanied by a CertificateVerify message, which the TLS Server uses to verify that the Client owns the certificate (has access to the private key associated with that certificate).</span></span>

<span data-ttu-id="1c3ae-846">Belirtilen sertifika doğrulanırsa ve bir X. 509.952 sertifika zinciri aracılığıyla TLS sunucusu güvenilen sertifika deposundaki bir sertifikaya geri izleniyorsa, uzak TLS Istemcisinin kimliği doğrulanır ve el sıkışma devam eder.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-846">If the provided certificate can be verified and traced back to a certificate in the TLS Server trusted certificate store via an X.509 certificate chain, the remote TLS Client is authenticated and the handshake proceeds.</span></span> <span data-ttu-id="1c3ae-847">Sertifikayı veya CertificateVerify iletisini işlerken herhangi bir hata olması durumunda, TLS anlaşması bir hatayla biter.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-847">In case of any errors in processing the certificate or CertificateVerify message, the TLS handshake ends with an error.</span></span>

> [!NOTE]
> <span data-ttu-id="1c3ae-848">*TLS sunucusunda, güvenilir depodaki en az bir sertifika nx_secure_tls_trusted_certificate_add ile eklenmiş olmalıdır veya kimlik doğrulama her zaman başarısız olur.*</span><span class="sxs-lookup"><span data-stu-id="1c3ae-848">*The TLS Server must have at least one certificate in its trusted store added with nx_secure_tls_trusted_certificate_add or authentication will always fail.*</span></span>

### <a name="parameters"></a><span data-ttu-id="1c3ae-849">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1c3ae-849">Parameters</span></span>

- <span data-ttu-id="1c3ae-850">**session_ptr** Bir TLS oturum örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-850">**session_ptr** Pointer to a TLS Session instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="1c3ae-851">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-851">Return Values</span></span>

- <span data-ttu-id="1c3ae-852">**NX_SUCCESS** (0x00) başarılı durum değişikliği.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-852">**NX_SUCCESS** (0x00) Successful state change.</span></span>
- <span data-ttu-id="1c3ae-853">**NX_PTR_ERROR** (0x07) geçersiz TLS oturum işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-853">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1c3ae-854">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="1c3ae-854">Allowed From</span></span>

<span data-ttu-id="1c3ae-855">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="1c3ae-855">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1c3ae-856">Örnek</span><span class="sxs-lookup"><span data-stu-id="1c3ae-856">Example</span></span>

```C
/* Add a trusted certificate so the TLS Server has something to verify against. */
status = nx_secure_tls_trusted_certificate_add(&tls_session,
                                               &trusted_certificate);

/* Disable client certificate authentication for this TLS session.   */
status = nx_secure_tls_session_client_verify_enable(&tls_session);

/* Any new TLS Server sessions using the tls_session control block will now
request and verify certificates from the remote TLS client.  */
```

### <a name="see-also"></a><span data-ttu-id="1c3ae-857">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-857">See Also</span></span>

- <span data-ttu-id="1c3ae-858">nx_secure_tls_session_client_verify_enable</span><span class="sxs-lookup"><span data-stu-id="1c3ae-858">nx_secure_tls_session_client_verify_enable</span></span>
- <span data-ttu-id="1c3ae-859">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="1c3ae-859">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="1c3ae-860">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="1c3ae-860">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="1c3ae-861">nx_secure_tls_trusted_certificate_add</span><span class="sxs-lookup"><span data-stu-id="1c3ae-861">nx_secure_tls_trusted_certificate_add</span></span>

## <a name="nx_secure_tls_session_create"></a><span data-ttu-id="1c3ae-862">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="1c3ae-862">nx_secure_tls_session_create</span></span>

<span data-ttu-id="1c3ae-863">Güvenli iletişim için bir NetX güvenli TLS oturumu oluşturun</span><span class="sxs-lookup"><span data-stu-id="1c3ae-863">Create a NetX Secure TLS Session for secure communications</span></span>

### <a name="prototype"></a><span data-ttu-id="1c3ae-864">Prototype</span><span class="sxs-lookup"><span data-stu-id="1c3ae-864">Prototype</span></span>

```C
UINT  nx_secure_tls_session_create(NX_SECURE_TLS_SESSION *session_ptr
                                   NX_SECURE_TLS_CRYPTO *cipher_table,
                                   VOID *encryption_metadata_area,
                                   ULONG encryption_metadata_size);
```

### <a name="description"></a><span data-ttu-id="1c3ae-865">Description</span><span class="sxs-lookup"><span data-stu-id="1c3ae-865">Description</span></span>

<span data-ttu-id="1c3ae-866">Bu hizmet, bir NX_SECURE_TLS_SESSION üzerinden güvenli TLS iletişimleri kurmada kullanmak üzere bir ağ yapısı örneği başlatıyor.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-866">This service initializes an NX_SECURE_TLS_SESSION structure instance for use in establishing secure TLS communications over a network connection.</span></span>

<span data-ttu-id="1c3ae-867">yöntemi, TLS NX_SECURE_TLS_CRYPTO kullanılabilen şifreleme yöntemleriyle doldurulan bir nesne alır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-867">The method takes a NX_SECURE_TLS_CRYPTO object that is populated with the available cryptographic methods to be used for TLS.</span></span> <span data-ttu-id="1c3ae-868">Bu *encryption_metadata_area,* hesaplamalar için tablodaki şifreleme yöntemleri tarafından kullanılan "meta veriler" için TLS tarafından NX_SECURE_TLS_CRYPTO bir arabelleğe gösterir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-868">The *encryption_metadata_area* points to a buffer allocated for use by TLS for the "metadata" used by the cryptographic methods in the NX_SECURE_TLS_CRYPTO table for calculations.</span></span> <span data-ttu-id="1c3ae-869">Tablonun boyutu, nx_secure_tls_metadata_size_calculate kullanılarak belirlenecektir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-869">The size of the table can be determined by using the nx_secure_tls_metadata_size_calculate service.</span></span> <span data-ttu-id="1c3ae-870">Daha fazla ayrıntı için Bölüm 3'te "NetX Secure TLS'de Şifreleme" bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-870">See the section "Cryptography in NetX Secure TLS" in Chapter 3 for more details.</span></span>

### <a name="parameters"></a><span data-ttu-id="1c3ae-871">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1c3ae-871">Parameters</span></span>

- <span data-ttu-id="1c3ae-872">**session_ptr** TLS Oturumu örneğinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-872">**session_ptr** Pointer to a TLS Session instance.</span></span>
- <span data-ttu-id="1c3ae-873">**cipher_table** TLS şifreleme yöntemlerinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-873">**cipher_table** Pointer to TLS cryptographic methods.</span></span>
- <span data-ttu-id="1c3ae-874">**encryption_metadata_area** Şifreleme meta verileri için alan işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-874">**encryption_metadata_area** Pointer to space for cryptography metadata.</span></span>
- <span data-ttu-id="1c3ae-875">**encryption_metadata_size** Meta veri arabelleğinin boyutu.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-875">**encryption_metadata_size** Size of the metadata buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="1c3ae-876">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-876">Return Values</span></span>

- <span data-ttu-id="1c3ae-877">**NX_SUCCESS** (0x00)TLS oturumunun başarıyla başlatılıyor.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-877">**NX_SUCCESS** (0x00)Successful initialization of the TLS session.</span></span>
- <span data-ttu-id="1c3ae-878">**NX_PTR_ERROR** (0x07) Geçersiz bir işaretçi kullanmayı denedi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-878">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>
- <span data-ttu-id="1c3ae-879">**NX_INVALID_PARAMETERS** (0x4D) Meta veri arabelleği verilen yöntemler için çok küçüktü.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-879">**NX_INVALID_PARAMETERS** (0x4D) The metadata buffer was too small for the given methods.</span></span>
- <span data-ttu-id="1c3ae-880">**NX_SECURE_TLS_UNSUPPORTED_CIPHER** (0x106) TLS'nin etkin sürümü için gerekli bir şifreleme yöntemi, şifreleme tablosunda sağlanmadı.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-880">**NX_SECURE_TLS_UNSUPPORTED_CIPHER** (0x106) A required cipher method for the enabled version of TLS was not supplied in the cipher table.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1c3ae-881">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="1c3ae-881">Allowed From</span></span>

<span data-ttu-id="1c3ae-882">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="1c3ae-882">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1c3ae-883">Örnek</span><span class="sxs-lookup"><span data-stu-id="1c3ae-883">Example</span></span>

```C
/* Reference the platform-specific TLS cryptographic method table. */
extern const NX_SECURE_TLS_CRYPTO nx_crypto_tls_ciphers;

/* Declare a buffer for the cryptographic metadata. The size should be calculated
   using nx_secure_tls_metadata_size_calculate. */
UCHAR crypto_metadata[4500];

/* Initialize TLS session.  */
status =  nx_secure_tls_session_create(&tls_session,
                                       &nx_crypto_tls_ciphers,
                                       crypto_metadata,
                                       sizeof(crypto_metadata));


/* If status is NX_SUCCESS the TLS Session was successfully initialized.  */
```

### <a name="see-also"></a><span data-ttu-id="1c3ae-884">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-884">See Also</span></span>

- <span data-ttu-id="1c3ae-885">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="1c3ae-885">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="1c3ae-886">nx_secure_tls_metadata_size_calculate</span><span class="sxs-lookup"><span data-stu-id="1c3ae-886">nx_secure_tls_metadata_size_calculate</span></span>
- <span data-ttu-id="1c3ae-887">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="1c3ae-887">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="1c3ae-888">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="1c3ae-888">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="1c3ae-889">nx_secure_tls_session_end</span><span class="sxs-lookup"><span data-stu-id="1c3ae-889">nx_secure_tls_session_end</span></span>
- <span data-ttu-id="1c3ae-890">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="1c3ae-890">nx_secure_tls_session_send</span></span>
- <span data-ttu-id="1c3ae-891">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="1c3ae-891">nx_secure_tls_session_receive</span></span>
- <span data-ttu-id="1c3ae-892">nx_secure_tls_session_delete</span><span class="sxs-lookup"><span data-stu-id="1c3ae-892">nx_secure_tls_session_delete</span></span>
- <span data-ttu-id="1c3ae-893">Bölüm 3 ' te NetX güvenli TLS 'de şifreleme</span><span class="sxs-lookup"><span data-stu-id="1c3ae-893">Cryptography in NetX Secure TLS in Chapter 3</span></span>

## <a name="nx_secure_tls_session_delete"></a><span data-ttu-id="1c3ae-894">nx_secure_tls_session_delete</span><span class="sxs-lookup"><span data-stu-id="1c3ae-894">nx_secure_tls_session_delete</span></span>

<span data-ttu-id="1c3ae-895">NetX güvenli TLS oturumunu silme</span><span class="sxs-lookup"><span data-stu-id="1c3ae-895">Delete a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="1c3ae-896">Prototype</span><span class="sxs-lookup"><span data-stu-id="1c3ae-896">Prototype</span></span>

```C
UINT  nx_secure_tls_session_delete(NX_SECURE_TLS_SESSION *session_ptr);
```

### <a name="description"></a><span data-ttu-id="1c3ae-897">Description</span><span class="sxs-lookup"><span data-stu-id="1c3ae-897">Description</span></span>

<span data-ttu-id="1c3ae-898">Bu hizmet, bir NX_SECURE_TLS_SESSION yapısı örneğiyle temsil edilen bir TLS oturumunu siler ve o oturum örneğine ait tüm sistem kaynaklarını serbest bırakır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-898">This service deletes a TLS session represented by an NX_SECURE_TLS_SESSION structure instance and releases all system resources owned by that session instance.</span></span>

### <a name="parameters"></a><span data-ttu-id="1c3ae-899">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1c3ae-899">Parameters</span></span>

- <span data-ttu-id="1c3ae-900">**session_ptr** Bir TLS oturum örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-900">**session_ptr** Pointer to a TLS Session instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="1c3ae-901">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-901">Return Values</span></span>

- <span data-ttu-id="1c3ae-902">TLS oturumunun başarıyla başlatılmasından **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="1c3ae-902">**NX_SUCCESS** (0x00) Successful initialization of the TLS session.</span></span>
- <span data-ttu-id="1c3ae-903">**NX_PTR_ERROR** (0x07) geçersiz bir Işaretçi kullanmaya çalıştı.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-903">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1c3ae-904">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="1c3ae-904">Allowed From</span></span>

<span data-ttu-id="1c3ae-905">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="1c3ae-905">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1c3ae-906">Örnek</span><span class="sxs-lookup"><span data-stu-id="1c3ae-906">Example</span></span>

```C
/* Delete TLS session.  */
status =  nx_secure_tls_session_delete(&tls_session);


/* If status is NX_SUCCESS the TLS Session was successfully deleted.  */
```

### <a name="see-also"></a><span data-ttu-id="1c3ae-907">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-907">See Also</span></span>

- <span data-ttu-id="1c3ae-908">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="1c3ae-908">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="1c3ae-909">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="1c3ae-909">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="1c3ae-910">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="1c3ae-910">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="1c3ae-911">nx_secure_tls_session_end</span><span class="sxs-lookup"><span data-stu-id="1c3ae-911">nx_secure_tls_session_end</span></span>
- <span data-ttu-id="1c3ae-912">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="1c3ae-912">nx_secure_tls_session_send</span></span>
- <span data-ttu-id="1c3ae-913">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="1c3ae-913">nx_secure_tls_session_receive</span></span>
- <span data-ttu-id="1c3ae-914">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="1c3ae-914">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_session_end"></a><span data-ttu-id="1c3ae-915">nx_secure_tls_session_end</span><span class="sxs-lookup"><span data-stu-id="1c3ae-915">nx_secure_tls_session_end</span></span>

<span data-ttu-id="1c3ae-916">Etkin bir NetX güvenli TLS oturumu sonlandır</span><span class="sxs-lookup"><span data-stu-id="1c3ae-916">End an active NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="1c3ae-917">Prototype</span><span class="sxs-lookup"><span data-stu-id="1c3ae-917">Prototype</span></span>

```C
UINT  nx_secure_tls_session_end(NX_SECURE_TLS_SESSION *session_ptr,
                                    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="1c3ae-918">Description</span><span class="sxs-lookup"><span data-stu-id="1c3ae-918">Description</span></span>

<span data-ttu-id="1c3ae-919">Bu hizmet, TLS CloseNotify iletisini uzak ana bilgisayara göndererek bir NX_SECURE_TLS_SESSION yapısı örneği tarafından temsil edilen bir TLS oturumunu sonlandırır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-919">This service ends a TLS session represented by an NX_SECURE_TLS_SESSION structure instance by sending the TLS CloseNotify message to the remote host.</span></span> <span data-ttu-id="1c3ae-920">Ardından hizmet, uzak ana bilgisayarın kendi CloseNotify iletisiyle yanıt vermesini bekler.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-920">The service then waits for the remote host to respond with its own CloseNotify message.</span></span>

<span data-ttu-id="1c3ae-921">Uzak konak bir CloseNotify iletisi göndermse TLS bunu bir hata ve olası bir güvenlik ihlali olarak kabul ederek güvenli bağlantı için dönüş değerinin denetlen önemlidir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-921">If the remote host does not send a CloseNotify message, TLS considers this an error and a possible security breach, so checking the return value is important for a secure connection.</span></span> <span data-ttu-id="1c3ae-922">wait_option  parametresi, çağrıyı çağıran iş parçacığına denetim döndürmeden önce hizmetin yanıt için ne kadar beklemesi gerektiğini kontrol etmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-922">The **wait_option** parameter can be used to control how long the service should wait for the response before returning control to the calling thread.</span></span>

### <a name="parameters"></a><span data-ttu-id="1c3ae-923">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1c3ae-923">Parameters</span></span>

- <span data-ttu-id="1c3ae-924">**session_ptr** TLS Oturumu örneğinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-924">**session_ptr** Pointer to a TLS Session instance.</span></span>
- <span data-ttu-id="1c3ae-925">**wait_option** Hizmetin uzak konaktan ne kadar süreyle yanıt beklemesi gerektiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-925">**wait_option** Indicates how long the service should wait for the response from the remote host.</span></span>

### <a name="return-values"></a><span data-ttu-id="1c3ae-926">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-926">Return Values</span></span>

- <span data-ttu-id="1c3ae-927">**NX_SUCCESS** (0x00) TLS oturumunun başarıyla başlatılıyor.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-927">**NX_SUCCESS** (0x00) Successful initialization of the TLS session.</span></span>
- <span data-ttu-id="1c3ae-928">**NX_SECURE_TLS_NO_CLOSE_RESPONSE** (0x113) Zaman dışından uzak konaktan yanıt almadı.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-928">**NX_SECURE_TLS_NO_CLOSE_RESPONSE** (0x113) Did not receive a response from the remote host before timing out.</span></span>
- <span data-ttu-id="1c3ae-929">**NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) CloseNotify iletisi göndermek için bir paket ayrılamadı.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-929">**NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) Could not allocate a packet to send the CloseNotify message.</span></span>
- <span data-ttu-id="1c3ae-930">**NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) TCP yuvası üzerinden CloseNotify iletisi gönderildi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-930">**NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) Could not send the CloseNotify message over the TCP socket.</span></span>
- <span data-ttu-id="1c3ae-931">**NX_PTR_ERROR** (0x07) Geçersiz bir işaretçi kullanmayı denedi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-931">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1c3ae-932">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="1c3ae-932">Allowed From</span></span>

<span data-ttu-id="1c3ae-933">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="1c3ae-933">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1c3ae-934">Örnek</span><span class="sxs-lookup"><span data-stu-id="1c3ae-934">Example</span></span>

```C
/* End TLS session.  */
status =  nx_secure_tls_session_end(&tls_session, NX_WAIT_FOREVER);


/* If status is NX_SUCCESS the TLS Session was successfully ended.  */
```

### <a name="see-also"></a><span data-ttu-id="1c3ae-935">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-935">See Also</span></span>

- <span data-ttu-id="1c3ae-936">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="1c3ae-936">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="1c3ae-937">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="1c3ae-937">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="1c3ae-938">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="1c3ae-938">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="1c3ae-939">nx_secure_tls_session_delete</span><span class="sxs-lookup"><span data-stu-id="1c3ae-939">nx_secure_tls_session_delete</span></span>
- <span data-ttu-id="1c3ae-940">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="1c3ae-940">nx_secure_tls_session_send</span></span>
- <span data-ttu-id="1c3ae-941">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="1c3ae-941">nx_secure_tls_session_receive</span></span>
- <span data-ttu-id="1c3ae-942">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="1c3ae-942">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_session_packet_buffer_set"></a><span data-ttu-id="1c3ae-943">nx_secure_tls_session_packet_buffer_set</span><span class="sxs-lookup"><span data-stu-id="1c3ae-943">nx_secure_tls_session_packet_buffer_set</span></span>

<span data-ttu-id="1c3ae-944">NetX Güvenli TLS Oturumu için paket yeniden değerlendirme arabelleği ayarlama</span><span class="sxs-lookup"><span data-stu-id="1c3ae-944">Set the packet reassembly buffer for a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="1c3ae-945">Prototype</span><span class="sxs-lookup"><span data-stu-id="1c3ae-945">Prototype</span></span>

```C
UINT  nx_secure_tls_session_packet_buffer_set(
                                    NX_SECURE_TLS_SESSION *session_ptr,
                                    UCHAR *buffer_ptr,
                                    ULONG buffer_size);
```

### <a name="description"></a><span data-ttu-id="1c3ae-946">Description</span><span class="sxs-lookup"><span data-stu-id="1c3ae-946">Description</span></span>

<span data-ttu-id="1c3ae-947">Bu hizmet, bir paket yeniden birleştirme arabelleğini bir TLS oturumuyla ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-947">This service associates a packet reassembly buffer to a TLS session.</span></span> <span data-ttu-id="1c3ae-948">Gelen TLS kayıtlarının şifresini çözmek ve ayrıştırmak için, her bir kayıttaki verilerin temel alınan TCP paketlerinden bir araya gelmelidir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-948">In order to decrypt and parse incoming TLS records, the data in each record must be assembled from the underlying TCP packets.</span></span> <span data-ttu-id="1c3ae-949">TLS kayıtlarının boyutu 16KB 'a kadar olabilir (genellikle çok daha küçüktür), bu nedenle tek bir TCP paketine uyamayabilir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-949">TLS records can be up to 16KB in size (though typically are much smaller) so may not fit into a single TCP packet.</span></span>

<span data-ttu-id="1c3ae-950">Gelen ileti boyutunun, 16KB olan TLS kayıt sınırından küçük olacağını biliyorsanız, arabellek boyutu daha küçük hale getirilebilir, ancak bilinmeyen gelen verileri işlemek için arabelleğin mümkün olduğunca büyük olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-950">If you know the incoming message size will be smaller than the TLS record limit of 16KB, the buffer size can be made smaller, but in order to handle unknown incoming data the buffer should be made as large as possible.</span></span> <span data-ttu-id="1c3ae-951">Gelen bir kayıt sağlanan arabellekten fazlaysa, TLS oturumu bir hatayla sona acaktır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-951">If an incoming record is larger than the supplied buffer, the TLS session will end with an error.</span></span>

### <a name="parameters"></a><span data-ttu-id="1c3ae-952">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1c3ae-952">Parameters</span></span>

- <span data-ttu-id="1c3ae-953">**session_ptr** Bir TLS oturum örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-953">**session_ptr** Pointer to a TLS Session instance.</span></span>
- <span data-ttu-id="1c3ae-954">**buffer_ptr** Paket yeniden birleştirme için kullanılacak TLS arabelleği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-954">**buffer_ptr** Pointer to buffer for TLS to use for packet reassembly.</span></span>
- <span data-ttu-id="1c3ae-955">**Buffer_size** Sağlanan arabelleğin bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-955">**buffer_size** Size of the supplied buffer in bytes.</span></span>

### <a name="return-values"></a><span data-ttu-id="1c3ae-956">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-956">Return Values</span></span>

- <span data-ttu-id="1c3ae-957">TLS oturumunun başarıyla başlatılmasından **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="1c3ae-957">**NX_SUCCESS** (0x00) Successful initialization of the TLS session.</span></span>
- <span data-ttu-id="1c3ae-958">**NX_INVALID_PARAMETERS** (0x4D) geçersiz arabellek veya TLS oturum işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-958">**NX_INVALID_PARAMETERS** (0x4D) Invalid buffer or TLS session pointer.</span></span>
- <span data-ttu-id="1c3ae-959">**NX_PTR_ERROR** (0x07) geçersiz bir Işaretçi kullanmaya çalıştı.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-959">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1c3ae-960">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="1c3ae-960">Allowed From</span></span>

<span data-ttu-id="1c3ae-961">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="1c3ae-961">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1c3ae-962">Örnek</span><span class="sxs-lookup"><span data-stu-id="1c3ae-962">Example</span></span>

```C
/* Buffer for TLS packet reassembly. */
UCHAR tls_packet_buffer[16384];
/* Assign buffer to TLS session.  */
status =  nx_secure_tls_session_packet_buffer_set(&tls_session, tls_packet_buffer,
                                                  sizeof(tls_packet_buffer));


/* If status is NX_SUCCESS the buffer was successfully added.  */
```

### <a name="see-also"></a><span data-ttu-id="1c3ae-963">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-963">See Also</span></span>

- <span data-ttu-id="1c3ae-964">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="1c3ae-964">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="1c3ae-965">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="1c3ae-965">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="1c3ae-966">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="1c3ae-966">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="1c3ae-967">nx_secure_tls_session_delete</span><span class="sxs-lookup"><span data-stu-id="1c3ae-967">nx_secure_tls_session_delete</span></span>
- <span data-ttu-id="1c3ae-968">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="1c3ae-968">nx_secure_tls_session_send</span></span>
- <span data-ttu-id="1c3ae-969">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="1c3ae-969">nx_secure_tls_session_receive</span></span>
- <span data-ttu-id="1c3ae-970">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="1c3ae-970">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_session_protocol_version_override"></a><span data-ttu-id="1c3ae-971">nx_secure_tls_session_protocol_version_override</span><span class="sxs-lookup"><span data-stu-id="1c3ae-971">nx_secure_tls_session_protocol_version_override</span></span>

<span data-ttu-id="1c3ae-972">NetX Güvenli TLS Oturumu için varsayılan TLS protokol sürümünü geçersiz kılma</span><span class="sxs-lookup"><span data-stu-id="1c3ae-972">Override the default TLS protocol version for a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="1c3ae-973">Prototype</span><span class="sxs-lookup"><span data-stu-id="1c3ae-973">Prototype</span></span>

```C
UINT  nx_secure_tls_session_protocol_version_override(
                              NX_SECURE_TLS_SESSION *session_ptr,
                              USHORT protocol_version);
```

### <a name="description"></a><span data-ttu-id="1c3ae-974">Description</span><span class="sxs-lookup"><span data-stu-id="1c3ae-974">Description</span></span>

<span data-ttu-id="1c3ae-975">Bu hizmet, belirli bir oturum tarafından kullanılan varsayılan (en yeni) TLS protokol sürümünü geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-975">This service overrides the default (newest) TLS protocol version used by a particular session.</span></span> <span data-ttu-id="1c3ae-976">Bu, NetX Secure TLS'nin derleme zamanında daha yeni TLS sürümlerini devre dışı bırakmadan belirli bir TLS Oturumu için daha eski bir TLS sürümünü kullanmasına olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-976">This enables NetX Secure TLS to use an older version of TLS for a specific TLS Session without disabling newer TLS versions at compile time.</span></span> <span data-ttu-id="1c3ae-977">Bu, TLS'nin en yeni sürümünü desteklemeen eski bir ana bilgisayarla iletişim kurması gerektirilen uygulamalarda yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-977">This may be useful in applications that may need to communicate with an older host that does not support the newest version of TLS.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1c3ae-978">*Sürüm 5.11SP3'te NetX Secure TLS RFC 7507'yi destekler (aşağıdaki nota bakın) ve bu API ile eski bir sürümde yapılan geçersiz kılmalar ClientHello'da geri dönüş SCSV'si gönderilir. Sunucu daha yeni bir TLS sürümünü destekliyorsa ve ClientHello'ya geri dönüş SCSV'si dahil edilirse, bu sunucu TLS el sıkışmayı "Uygunsuz Geri Dönüş" uyarısıyla iptal eder. SCSV yalnızca sürüm geçersiz kılma özelliği tlS'nin etkin olandan eski bir sürümü olduğunda gönderilir (örneğin, sürümü TLS 1.2 olarak geçersiz kılarsanız, SCSV gönderilmez).*</span><span class="sxs-lookup"><span data-stu-id="1c3ae-978">*As of version 5.11SP3, NetX Secure TLS supports RFC 7507 (see note below) and any override to an older version with this API will result in a fallback SCSV being sent in the ClientHello. If the server supports a newer version of TLS and the fallback SCSV is included in the ClientHello, that server will abort the TLS handshake with an "Inappropriate Fallback" alert. The SCSV is only sent when the version override is an older version of TLS than is enabled (e.g. if you override the version to TLS 1.2, no SCSV will be sent).*</span></span>

<span data-ttu-id="1c3ae-979">protocol_version parametresi için geçerli değerler şu makrolardır: NX_SECURE_TLS_VERSION_TLS_1_0, NX_SECURE_TLS_VERSION_TLS_1_1 ve NX_SECURE_TLS_VERSION_TLS_1_2.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-979">Valid values for the protocol_version parameter are the following macros: NX_SECURE_TLS_VERSION_TLS_1_0, NX_SECURE_TLS_VERSION_TLS_1_1, and NX_SECURE_TLS_VERSION_TLS_1_2.</span></span>

<span data-ttu-id="1c3ae-980">Bu NX_SECURE_TLS_DISABLE_TLS_1_1 NX_SECURE_TLS_ENABLE_TLS_1_0, uygulamaya derlenmiş TLS sürümlerini kontrol etmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-980">The macros NX_SECURE_TLS_DISABLE_TLS_1_1 and NX_SECURE_TLS_ENABLE_TLS_1_0 can be used to control the versions of TLS that are compiled into the application.</span></span> <span data-ttu-id="1c3ae-981">TLS sürüm 1.2 her zaman etkindir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-981">TLS version 1.2 is always enabled.</span></span>

<span data-ttu-id="1c3ae-982">Uzak ana bilgisayar sağlanan sürümü desteklemezse bağlantının başarısız olacağını unutmayın. Yalnızca verilen geçersiz kılma sürümü NetX Secure TLS tarafından anılacaktır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-982">Note that if the remote host does not support the supplied version, the connection will fail – only the supplied override version will be negotiated by NetX Secure TLS.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1c3ae-983">RFC 7507: TLS Geri Dönüş SCSV.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-983">RFC 7507: TLS Fallback SCSV.</span></span> <span data-ttu-id="1c3ae-984">Bu RFC, başlangıçta protokol eski sürüm düşürme anlaşmalarını hatalı bir şekilde ele alan ve bunun yerine geçerli olmayan ClientHello iletilerini reddeden sunuculardan kaynaklanan bir güvenlik sorununu azaltmak için tanıtıldı.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-984">This RFC was introduced to mitigate a security problem that was originally caused by servers that improperly handled protocol downgrade negotiation and instead rejected otherwise valid ClientHello messages.</span></span> <span data-ttu-id="1c3ae-985">Bu eski sunucularla uyumlu olmaya devam etmek için bazı TLS istemci uygulamaları ile başarısız el sıkışmalarını ve eski TLS sürümünü yeniden denemeye başladı (örneğin TLS 1.2 başarısız oldu, bu nedenle TLS 1.1'i deneyin).</span><span class="sxs-lookup"><span data-stu-id="1c3ae-985">In an attempt to remain compatible with these old servers, some TLS client applications started to retry failed handshakes with and older TLS version (e.g. TLS 1.2 failed so try TLS 1.1).</span></span> <span data-ttu-id="1c3ae-986">Bu geçici çözüm, yeni bir sorun ortaya sunmuştur; bir saldırgan, sunucu daha yeni TLS sürümünü desteklense bile, sunucu bağlantısının başarısız olmasına neden olan bir ağ veya paket hatası ile yapay bir istemciyi indirgemeye zorlayabilir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-986">This workaround however introduced a new problem – an attacker could force a client to downgrade by artificially introducing a network or packet error causing the server connection to fail – even when the server supported the newer TLS version.</span></span> <span data-ttu-id="1c3ae-987">Daha eski bir sürüme indirgenerek saldırgan, söz konusu sürümdeki zayıf yönleriyle yararlanabilir (SSLv3<sup>21</sup> , özellıkle de çıkış saldırılarına karşı zayıfdır).</span><span class="sxs-lookup"><span data-stu-id="1c3ae-987">By downgrading to an older version the attacker could exploit weaknesses in that version (SSLv3<sup>21</sup> in particular is weak to the POODLE attack).</span></span> <span data-ttu-id="1c3ae-988">Bu durumu engellemek için, RFC 7507 ' de, bir TLS istemcisi desteklediği en yeni sürüm olmayan bir TLS<sup></sup> sürümünü kullanırken TLS sunucusuna bildiren "GERI dönüş SCSV" bir ClientHello</span><span class="sxs-lookup"><span data-stu-id="1c3ae-988">To prevent this situation, RFC 7507 introdued the "fallback SCSV," a pseudo-ciphersuite<sup>22</sup> sent in the ClientHello that notifies a TLS server when a TLS client is using a TLS version that is not the newest version it supports.</span></span> <span data-ttu-id="1c3ae-989">Bu şekilde, daha yeni bir sürümü destekleyen bir sunucu, geri dönüş SCSV 'i içeren bir ClientHello reddedebilir ve düşürme saldırılarının başarılı olmasını önler.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-989">This way, a server that supports a newer version can reject a ClientHello containing the fallback SCSV and prevent the downgrade attack from succeeding.</span></span>

21. <span data-ttu-id="1c3ae-990">NetX Secure, POOıDLE gibi bilinen ciddi zayıf yanlar nedeniyle SSLv3 uygulamaz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-990">NetX Secure does not implement SSLv3 due to the existence of known serious weaknesses such as POODLE.</span></span>

22. <span data-ttu-id="1c3ae-991">Sözde ciphersuite veya SCSV (sinyal şifreleme paketi değeri), eski TLS sürümlerinde kullanılamayan özelliklerle ilgili etkin TLS uygulamalarını işaret etmek için kullanılan ayrılmış bir ciphersuite numarasıdır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-991">A pseudo-ciphersuite, or SCSV (Signaling Cipher Suite Value), is a reserved ciphersuite number that is used to signal enabled TLS implementations about features that were not available in older TLS versions.</span></span> <span data-ttu-id="1c3ae-992">Geri dönüş SCSV ve TLS_EMPTY_RENEGOTIATION_INFO_SCSV (RFC 5746) örnektir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-992">The fallback SCSV and the TLS_EMPTY_RENEGOTIATION_INFO_SCSV (RFC 5746) are examples.</span></span>

### <a name="parameters"></a><span data-ttu-id="1c3ae-993">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1c3ae-993">Parameters</span></span>

- <span data-ttu-id="1c3ae-994">**session_ptr** Bir TLS oturum örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-994">**session_ptr** Pointer to a TLS Session instance.</span></span>
- <span data-ttu-id="1c3ae-995">**protocol_version** Kullanılacak belirli TLS sürümü için TLS sürümü makrosu.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-995">**protocol_version** TLS version macro for the specific TLS version to use.</span></span>

### <a name="return-values"></a><span data-ttu-id="1c3ae-996">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-996">Return Values</span></span>

- <span data-ttu-id="1c3ae-997">**NX_SUCCESS** (0x00) başarılı durum değişikliği.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-997">**NX_SUCCESS** (0x00) Successful state change.</span></span>
- <span data-ttu-id="1c3ae-998">**NX_PTR_ERROR** (0x07) geçersiz TLS oturum işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-998">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>
- <span data-ttu-id="1c3ae-999">**NX_SECURE_TLS_UNSUPPORTED_TLS_VERSION** (0x110) bilinen ancak desteklenmeyen TLS sürümü.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-999">**NX_SECURE_TLS_UNSUPPORTED_TLS_VERSION** (0x110) Known but unsupported TLS version.</span></span>
- <span data-ttu-id="1c3ae-1000">**NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0x10F) geçersiz protokol sürümü.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1000">**NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0x10F) Invalid protocol version.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1c3ae-1001">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1001">Allowed From</span></span>

<span data-ttu-id="1c3ae-1002">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1002">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1c3ae-1003">Örnek</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1003">Example</span></span>

```C
/* Set the protocol version to be used to TLSv1.1. */
status = nx_secure_tls_session_protocol_version_override(&tls_session,
                                              NX_SECURE_TLS_VERSION_TLS_1_1);

/* This TLS Session will use TLSv1.1 for the handshake and TLS session. */
status = nx_secure_tls_session_start(&tls_session, &tcp_socket, NX_WAIT_FOREVER);
```

### <a name="see-also"></a><span data-ttu-id="1c3ae-1004">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1004">See Also</span></span>

- <span data-ttu-id="1c3ae-1005">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1005">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="1c3ae-1006">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1006">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_session_receive"></a><span data-ttu-id="1c3ae-1007">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1007">nx_secure_tls_session_receive</span></span>

<span data-ttu-id="1c3ae-1008">NetX güvenli TLS oturumundan veri alma</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1008">Receive data from a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="1c3ae-1009">Prototype</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1009">Prototype</span></span>

```C
UINT  nx_secure_tls_session_receive(NX_SECURE_TLS_SESSION *session_ptr,
                                    NX_PACKET **packet_ptr,
                                    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="1c3ae-1010">Description</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1010">Description</span></span>

<span data-ttu-id="1c3ae-1011">Bu hizmet, belirtilen etkin TLS oturumundan verileri alır ve bu verilerin şifresini, NX_PACKET parametresindeki çağırana sağlamadan önce işleme alır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1011">This service receives data from the specified active TLS session, handling the decryption of that data before providing it to the caller in the NX_PACKET parameter.</span></span> <span data-ttu-id="1c3ae-1012">Belirtilen oturumda hiçbir veri sıraya alınmaz, çağrı sağlanan bekleme seçeneğine göre askıya alınır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1012">If no data is queued in the specified session, the call suspends based on the supplied wait option.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1c3ae-1013">*Bir NX_SUCCESS döndürülürse, uygulama artık gerekli olmadığı zaman alınan paketi serbest bırakmakla sorumludur.*</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1013">*If NX_SUCCESS is returned, the application is responsible for releasing the received packet when it is no longer needed.*</span></span>

### <a name="parameters"></a><span data-ttu-id="1c3ae-1014">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1014">Parameters</span></span>

- <span data-ttu-id="1c3ae-1015">**session_ptr** TLS Oturumu örneğinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1015">**session_ptr** Pointer to a TLS Session instance.</span></span>
- <span data-ttu-id="1c3ae-1016">**packet_ptr** Ayrılmış bir TLS paket işaretçisinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1016">**packet_ptr** Pointer to an allocated TLS packet pointer.</span></span>
- <span data-ttu-id="1c3ae-1017">**wait_option** Hizmetin, geri dönmeden önce uzak konaktan bir paket için ne kadar beklemesi gerektiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1017">**wait_option** Indicates how long the service should wait for a packet from the remote host before returning.</span></span>

### <a name="return-values"></a><span data-ttu-id="1c3ae-1018">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1018">Return Values</span></span>

- <span data-ttu-id="1c3ae-1019">**NX_SUCCESS** (0x00) TLS oturumunun başarıyla başlatılıyor.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1019">**NX_SUCCESS** (0x00) Successful initialization of the TLS session.</span></span>
- <span data-ttu-id="1c3ae-1020">**NX_NO_PACKET** (0x01) Veri alınmamıştır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1020">**NX_NO_PACKET** (0x01) No data received.</span></span>
- <span data-ttu-id="1c3ae-1021">**NX_NOT_CONNECTED** (0x38) Temel ALıNAN TCP yuvası artık bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1021">**NX_NOT_CONNECTED** (0x38) The underlying TCP socket is no longer connected.</span></span>
- <span data-ttu-id="1c3ae-1022">**NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0x108) Alınan ileti kimlik doğrulaması karma denetimi başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1022">**NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0x108) A received message failed an authentication hash check.</span></span>
- <span data-ttu-id="1c3ae-1023">**NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0x10F) Alınan ileti üst bilgisinde bilinmeyen bir protokol sürümü içeriyordu.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1023">**NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0x10F) A received message contained an unknown protocol version in its header.</span></span>
- <span data-ttu-id="1c3ae-1024">**NX_SECURE_TLS_ALERT_RECEIVED** (0x114) Uzak konaktan bir TLS uyarısı alındı.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1024">**NX_SECURE_TLS_ALERT_RECEIVED** (0x114) Received a TLS alert from the remote host.</span></span>
- <span data-ttu-id="1c3ae-1025">**NX_PTR_ERROR** (0x07) Geçersiz bir işaretçi kullanmayı denedi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1025">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>
- <span data-ttu-id="1c3ae-1026">**NX_SECURE_TLS_SESSION_UNINITIALIZED** (0x101) Sağlanan TLS oturumu başlatılmadı.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1026">**NX_SECURE_TLS_SESSION_UNINITIALIZED** (0x101) The supplied TLS session was not initialized.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1c3ae-1027">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1027">Allowed From</span></span>

<span data-ttu-id="1c3ae-1028">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1028">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1c3ae-1029">Örnek</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1029">Example</span></span>

```C
/* Receive a packet from an active TLS session previously created and started with
nx_secure_tls_session_start. Wait until a packet is received, blocking otherwise.
*/
status =  nx_secure_tls_session_receive(&tls_session, &packet_ptr,
NX_WAIT_FOREVER);


/* If status is NX_SUCCESS the received packet is pointed to by  "packet_ptr". */
```

### <a name="see-also"></a><span data-ttu-id="1c3ae-1030">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1030">See Also</span></span>

- <span data-ttu-id="1c3ae-1031">nx_tcp_socket_receive</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1031">nx_tcp_socket_receive</span></span>
- <span data-ttu-id="1c3ae-1032">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1032">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="1c3ae-1033">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1033">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="1c3ae-1034">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1034">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="1c3ae-1035">nx_secure_tls_session_delete</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1035">nx_secure_tls_session_delete</span></span>
- <span data-ttu-id="1c3ae-1036">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1036">nx_secure_tls_session_send</span></span>
- <span data-ttu-id="1c3ae-1037">nx_secure_tls_session_end</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1037">nx_secure_tls_session_end</span></span>
- <span data-ttu-id="1c3ae-1038">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1038">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_session_renegotiate_callback_set"></a><span data-ttu-id="1c3ae-1039">nx_secure_tls_session_renegotiate_callback_set</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1039">nx_secure_tls_session_renegotiate_callback_set</span></span>

<span data-ttu-id="1c3ae-1040">Oturum yeniden anlaşması başlangıcında çağrılacak bir geri çağırma atayın</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1040">Assign a callback that will be invoked at the beginning of a session renegotiation</span></span>

### <a name="prototype"></a><span data-ttu-id="1c3ae-1041">Prototype</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1041">Prototype</span></span>

```C
UINT  nx_secure_tls_ session_renegotiate_callback_set (
                  NX_SECURE_TLS_SESSION *tls_session,
                  ULONG (*func_ptr)(struct NX_SECURE_TLS_SESSION_struct
                  *session));
```

### <a name="description"></a><span data-ttu-id="1c3ae-1042">Description</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1042">Description</span></span>

<span data-ttu-id="1c3ae-1043">Bu hizmet, uzak ana bilgisayardan bir oturum yeniden anlaşma el sıkışma iletisi alındığında çağrılacak bir TLS oturumuna geri çağırma işlemi atar.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1043">This service assigns a callback to a TLS session that will be invoked whenever the first message of a session renegotiation handshake is received from the remote host.</span></span>

<span data-ttu-id="1c3ae-1044">Geri çağırma işlevi, bir yeniden anlaşma anlaşmasını oluşturan uygulamaya bildirim olarak tasarlanmıştır. uygulama, geri aramadan sıfır olmayan bir değer döndürerek TLS oturumunu sonlandırarak TLS oturumunun bir hata ile sonlanmasına neden olacak.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1044">The callback function is intended as a notification to the application that a renegotiation handshake is beginning – the application may choose to terminate the TLS session by returning any non-zero value from the callback which will cause TLS to end the TLS session with an error.</span></span> <span data-ttu-id="1c3ae-1045">Uygulama yeniden anlaşmaya devam etmek isterse, geri çağırma NX_SUCCESS döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1045">If the application wishes to proceed with the renegotiation, the callback should return NX_SUCCESS.</span></span>

> [!NOTE]
> <span data-ttu-id="1c3ae-1046">*TLS yeniden anlaşması semantiği nedeniyle, uzak sunucudan bir HelloRequest alındığında, ancak istemci yeniden anlaşmayı başlattığında değil, NetX güvenli TLS Istemcileri için geri arama çağrılacaktır. NetX güvenli TLS sunucularında, bir yeniden anlaşma ClientHello alındığında (etkin bir TLS oturumu bağlamında alınan herhangi bir ClientHello) geri çağırma işlemi çağrılır. Bu, TLS sunucusu uzak istemcinin yanıt verdiği bir merhaba Istek göndereceği için, geri aramanın uzak ana bilgisayar veya yerel uygulamanın yeniden anlaşmayı başlattığını belirtir.*</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1046">*Due to the semantics of TLS renegotiation, the callback will be invoked for NetX Secure TLS Clients whenever a HelloRequest is received from the remote server, but not when the client initiates the renegotiation. On NetX Secure TLS Servers, the callback will be invoked whenever a renegotiation ClientHello is received (any ClientHello received in the context of an active TLS session). This means that the callback will be invoked whether the remote host or the local application has initiated the renegotiation because the TLS server will send a HelloRequest to which the remote client will respond.*</span></span>

<span data-ttu-id="1c3ae-1047">NetX güvenli TLS, yeniden anlaşma el sıkışmaları 'nın ortadaki adam saldırılarına maruz olmamasını sağlamak için, RFC 5746 ' den güvenli yeniden anlaşma alma uzantısını uygular.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1047">NetX Secure TLS implements the Secure Renegotiation Inidication Extension from RFC 5746 to ensure that renegotiation handshakes are not subject to man-in-the-middle attacks.</span></span>

### <a name="parameters"></a><span data-ttu-id="1c3ae-1048">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1048">Parameters</span></span>

- <span data-ttu-id="1c3ae-1049">**session_ptr** TLS oturum örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1049">**session_ptr** Pointer to TLS Session instance.</span></span>
- <span data-ttu-id="1c3ae-1050">**func_ptr** Geri arama işlevine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1050">**func_ptr** Pointer to callback function.</span></span>

### <a name="return-values"></a><span data-ttu-id="1c3ae-1051">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1051">Return Values</span></span>

- <span data-ttu-id="1c3ae-1052">**NX_SUCCESS** (0x00) geri aramanın başarıyla atanması.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1052">**NX_SUCCESS** (0x00) Successful assignment of callback.</span></span>
- <span data-ttu-id="1c3ae-1053">**NX_PTR_ERROR** (0x07) geri çağırma IşLEVI veya TLS oturumu için geçersiz bir Işaretçi kullanmayı denedi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1053">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer for the callback function or TLS session.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1c3ae-1054">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1054">Allowed From</span></span>

<span data-ttu-id="1c3ae-1055">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1055">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1c3ae-1056">Örnek</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1056">Example</span></span>

```C
/* Simple callback notifying the user that a renegotiation is starting. */
ULONG tls_renegotiation_callback(NX_SECURE_TLS_SESSION *session)
{
    printf("Renegotiation initiated by remote host\n");

    return(NX_SUCCESS);
}

/* Establish a TLS session with a remote host (TLS Client) */
status =  nx_secure_tls_session_create(&tls_session,
                                       &nx_crypto_tls_ciphers,
                                       crypto_metadata,
                                       sizeof(crypto_metadata));


/* Set callback for renegotiation notification. */
status = nx_secure_tls_session_renegotiate_callback_set(&tls_session,
                                                tls_renegotiation_callback);
```

### <a name="see-also"></a><span data-ttu-id="1c3ae-1057">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1057">See Also</span></span>

- <span data-ttu-id="1c3ae-1058">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1058">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="1c3ae-1059">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1059">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="1c3ae-1060">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1060">nx_secure_tls_session_receive</span></span>
- <span data-ttu-id="1c3ae-1061">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1061">nx_secure_tls_session_send</span></span>
- <span data-ttu-id="1c3ae-1062">nx_secure_tls_session_renegotiate</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1062">nx_secure_tls_session_renegotiate</span></span>

## <a name="nx_secure_tls_session_renegotiate"></a><span data-ttu-id="1c3ae-1063">nx_secure_tls_session_renegotiate</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1063">nx_secure_tls_session_renegotiate</span></span>

<span data-ttu-id="1c3ae-1064">Uzak konakla oturum yeniden anlaşma başlatma</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1064">Initiate a session renegotiation handshake with the remote host</span></span>

### <a name="prototype"></a><span data-ttu-id="1c3ae-1065">Prototype</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1065">Prototype</span></span>

```C
UINT  nx_secure_tls_ session_renegotiate (
                  NX_SECURE_TLS_SESSION *tls_session,
                  UINT wait_option);
```

### <a name="description"></a><span data-ttu-id="1c3ae-1066">Description</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1066">Description</span></span>

<span data-ttu-id="1c3ae-1067">Bu hizmet, bağlı uzak TLS *ana bilgisayarıyla* oturum yeniden anlaşmaları başlatıyor.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1067">This service initiates a session *renegotiation* handshake with a connected remote TLS host.</span></span> <span data-ttu-id="1c3ae-1068">Yeniden anlaşma, önceden kurulmuş bir TLS oturumu bağlamında ikinci bir TLS el sıkışması oluşur.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1068">A renegotiation consists of a second TLS handshake within the context of a previously-established TLS session.</span></span> <span data-ttu-id="1c3ae-1069">Yeni oturum anahtarları oluşturulana ve ChangeCipherSpec iletileri değiştirilene kadar yeni el sıkışma iletilerinin her biri TLS oturumu kullanılarak şifrelenir ve bu sırada tüm iletileri şifrelemek için yeni anahtarlar kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1069">Each of the new handshake messages is encrypted using the TLS session until new session keys are generated and ChangeCipherSpec messages are exchanged, at which time the new keys are used to encrypt all messages.</span></span>

<span data-ttu-id="1c3ae-1070">TLS oturumu kurulduktan sonra herhangi bir zamanda yeniden görüşme başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1070">A renegotiation can be initiated at any time once a TLS session is established.</span></span> <span data-ttu-id="1c3ae-1071">TLS el sıkışması sırasında veya TLS oturumu kurulmadan önce yeniden anlaşma denenirse hiçbir işlem olmaz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1071">If a renegotiation is attempted during a TLS handshake or before a TLS session is established no action will be taken.</span></span>

> [!NOTE]
> <span data-ttu-id="1c3ae-1072">*Bu hizmet çağrıldığında tüm TLS el sıkışması gerçekleştirilir, bu nedenle tamamlanma süresi ve döndürülen durum geçerli TLS ayarlarına ve oturum parametrelerine bağlı olarak değişir.*</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1072">*An entire TLS handshake will be performed when this service is invoked so the time to completion and returned status will vary depending on the current TLS settings and session parameters.*</span></span>

<span data-ttu-id="1c3ae-1073">NetX Secure TLS, yeniden anlaşma el sıkışmalarının ortadaki adam saldırılarına maruz olmadığını güvence altına almak için RFC 5746'dan Güvenli Yeniden Anlaşma Kimlik Doğrulama Uzantısı'nın uygulanmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1073">NetX Secure TLS implements the Secure Renegotiation Inidication Extension from RFC 5746 to ensure that renegotiation handshakes are not subject to man-in-the-middle attacks.</span></span>

### <a name="parameters"></a><span data-ttu-id="1c3ae-1074">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1074">Parameters</span></span>

- <span data-ttu-id="1c3ae-1075">**session_ptr** TLS Oturumu örneğinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1075">**session_ptr** Pointer to TLS Session instance.</span></span>
- <span data-ttu-id="1c3ae-1076">**wait_option** Hizmetin, geri dönmeden önce uzak konaktan bir paket için ne kadar beklemesi gerektiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1076">**wait_option** Indicates how long the service should wait for a packet from the remote host before returning.</span></span> <span data-ttu-id="1c3ae-1077">Bu, TLS içindeki tüm NetX hizmetlerine geçirildi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1077">This is passed to all NetX services within TLS.</span></span>

### <a name="return-values"></a><span data-ttu-id="1c3ae-1078">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1078">Return Values</span></span>

- <span data-ttu-id="1c3ae-1079">**NX_SUCCESS** (0x00) Başarılı yeniden yapılanma.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1079">**NX_SUCCESS** (0x00) Successful renegotiation.</span></span>
- <span data-ttu-id="1c3ae-1080">**NX_NO_PACKET** (0x01) Veri alınmamıştır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1080">**NX_NO_PACKET** (0x01) No data received.</span></span>
- <span data-ttu-id="1c3ae-1081">**NX_NOT_CONNECTED** (0x38) Temel ALıNAN TCP yuvası artık bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1081">**NX_NOT_CONNECTED** (0x38) The underlying TCP socket is no longer connected.</span></span>
- <span data-ttu-id="1c3ae-1082">**NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0x108) Alınan ileti kimlik doğrulaması karma denetimi başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1082">**NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0x108) A received message failed an authentication hash check.</span></span>
- <span data-ttu-id="1c3ae-1083">**NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0x10F) Alınan ileti üst bilgisinde bilinmeyen bir protokol sürümü içeriyordu.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1083">**NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0x10F) A received message contained an unknown protocol version in its header.</span></span>
- <span data-ttu-id="1c3ae-1084">**NX_SECURE_TLS_ALERT_RECEIVED** (0x114) Uzak konaktan bir TLS uyarısı alındı.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1084">**NX_SECURE_TLS_ALERT_RECEIVED** (0x114) Received a TLS alert from the remote host.</span></span>
- <span data-ttu-id="1c3ae-1085">**NX_SECURE_TLS_RENEGOTIATION_SESSION_INACTIVE** (0x134) Yerel veya uzak TLS oturumu devre dışıdır ve bu da yeniden görüşmeyi imkansız hale gelir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1085">**NX_SECURE_TLS_RENEGOTIATION_SESSION_INACTIVE** (0x134) The local or remote TLS session is inactive, making renegotiation impossible.</span></span>
- <span data-ttu-id="1c3ae-1086">**NX_SECURE_TLS_RENEGOTIATION_FAILURE** (0x13a) uzak ana BILGISAYAR, SCSV veya güvenli yeniden anlaşma uzantısı sağlamadı ve bu nedenle yeniden anlaşma yapılamaz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1086">**NX_SECURE_TLS_RENEGOTIATION_FAILURE** (0x13A) The remote host did not provide either the SCSV or Secure Renegotiation Extension and thus renegotiation cannot be performed.</span></span>
- <span data-ttu-id="1c3ae-1087">**NX_PTR_ERROR** (0x07) geçersiz bir Işaretçi kullanmaya çalıştı.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1087">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>
- <span data-ttu-id="1c3ae-1088">**NX_SECURE_TLS_SESSION_UNINITIALIZED** (0x101) sağlanan TLS oturumu başlatılmadı.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1088">**NX_SECURE_TLS_SESSION_UNINITIALIZED** (0x101) The supplied TLS session was not initialized.</span></span>
- <span data-ttu-id="1c3ae-1089">**NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) temel alınan paket ayırması başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1089">**NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) Underlying packet allocation failed.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1c3ae-1090">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1090">Allowed From</span></span>

<span data-ttu-id="1c3ae-1091">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1091">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1c3ae-1092">Örnek</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1092">Example</span></span>

```C
/* Establish a TLS session with a remote host (TLS Client) */
status =  nx_secure_tls_session_create(&tls_session,
                                       &nx_crypto_tls_ciphers,
                                       crypto_metadata,
                                       sizeof(crypto_metadata));


/* Setup a client socket connection.  */
status = nx_tcp_client_socket_connect(&tcp_socket, server_ipv4_address,
REMOTE_SERVER_PORT, NX_WAIT_FOREVER);

/* Start the TLS session. */
status = nx_secure_tls_session_start(&tls_session, &tcp_socket, NX_WAIT_FOREVER);

/* Send some data in the first TLS session. (Check “status” for errors…)*/
status = nx_secure_tls_packet_allocate(&tls_session, &pool_0, &send_packet,
                                       NX_WAIT_FOREVER);
status = nx_packet_data_append(send_packet, "Hello there!\r\n", 14, &pool_0,
                               NX_WAIT_FOREVER);
status = nx_secure_tls_session_send(&tls_session, send_packet,
                                    NX_IP_PERIODIC_RATE);

/* Now renegotiate the session. */
status  = nx_secure_tls_session_renegotiate(&tls_session, NX_WAIT_FOREVER);

/* If status == NX_SUCCESS, new TLS session keys have been generated. */

/* Send some data in the new TLS session. This will be encrypted using the new
   keys. */
status = nx_secure_tls_packet_allocate(&tls_session, &pool_0, &send_packet,
                                       NX_WAIT_FOREVER);
status = nx_packet_data_append(send_packet, "Another message…\r\n", 18, &pool_0,
                               NX_WAIT_FOREVER);
status = nx_secure_tls_session_send(&tls_session, send_packet,
                                    NX_IP_PERIODIC_RATE);
```

### <a name="see-also"></a><span data-ttu-id="1c3ae-1093">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1093">See Also</span></span>

- <span data-ttu-id="1c3ae-1094">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1094">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="1c3ae-1095">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1095">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="1c3ae-1096">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1096">nx_secure_tls_session_receive</span></span>
- <span data-ttu-id="1c3ae-1097">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1097">nx_secure_tls_session_send</span></span>
- <span data-ttu-id="1c3ae-1098">nx_secure_tls_session_renegotiation_callback_set</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1098">nx_secure_tls_session_renegotiation_callback_set</span></span>

## <a name="nx_secure_tls_session_reset"></a><span data-ttu-id="1c3ae-1099">nx_secure_tls_session_reset</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1099">nx_secure_tls_session_reset</span></span>

<span data-ttu-id="1c3ae-1100">NetX güvenli TLS oturumunu Temizleme ve sıfırlama</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1100">Clear out and reset a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="1c3ae-1101">Prototype</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1101">Prototype</span></span>

```C
UINT  nx_secure_tls_session_reset (NX_SECURE_TLS_SESSION *session_ptr);
```

### <a name="description"></a><span data-ttu-id="1c3ae-1102">Description</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1102">Description</span></span>

<span data-ttu-id="1c3ae-1103">Bu hizmet bir TLS oturumunu temizler ve mevcut bir TLS oturum nesnesinin yeni bir oturum için yeniden kullanılabilmesi için oturum oluşturulmuşdaymışsınız gibi durumu sıfırlar.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1103">This service clears out a TLS session and resets the state as if the session had just been created so an existing TLS session object can be re-used for a new session.</span></span>

### <a name="parameters"></a><span data-ttu-id="1c3ae-1104">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1104">Parameters</span></span>

- <span data-ttu-id="1c3ae-1105">**session_ptr** Bir TLS oturum örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1105">**session_ptr** Pointer to a TLS Session instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="1c3ae-1106">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1106">Return Values</span></span>

- <span data-ttu-id="1c3ae-1107">TLS oturumunun başarıyla başlatılmasından **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1107">**NX_SUCCESS** (0x00) Successful initialization of the TLS session.</span></span>
- <span data-ttu-id="1c3ae-1108">**NX_INVALID_PARAMETERS** (0x4D) geçersiz TLS oturum işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1108">**NX_INVALID_PARAMETERS** (0x4D) Invalid TLS session pointer.</span></span>
- <span data-ttu-id="1c3ae-1109">**NX_PTR_ERROR** (0x07) geçersiz bir Işaretçi kullanmaya çalıştı.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1109">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1c3ae-1110">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1110">Allowed From</span></span>

<span data-ttu-id="1c3ae-1111">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1111">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1c3ae-1112">Örnek</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1112">Example</span></span>

```C
/* Reset a TLS session.  */
status =  nx_secure_tls_session_reset(&tls_session);


/* If status is NX_SUCCESS the session was successfully reset and may be reused.*/
```

### <a name="see-also"></a><span data-ttu-id="1c3ae-1113">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1113">See Also</span></span>

- <span data-ttu-id="1c3ae-1114">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1114">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="1c3ae-1115">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1115">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="1c3ae-1116">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1116">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="1c3ae-1117">nx_secure_tls_session_delete</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1117">nx_secure_tls_session_delete</span></span>
- <span data-ttu-id="1c3ae-1118">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1118">nx_secure_tls_session_send</span></span>
- <span data-ttu-id="1c3ae-1119">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1119">nx_secure_tls_session_receive</span></span>
- <span data-ttu-id="1c3ae-1120">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1120">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_session_send"></a><span data-ttu-id="1c3ae-1121">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1121">nx_secure_tls_session_send</span></span>

<span data-ttu-id="1c3ae-1122">NetX Güvenli TLS Oturumu aracılığıyla veri gönderme</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1122">Send data through a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="1c3ae-1123">Prototype</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1123">Prototype</span></span>

```C
UINT  nx_secure_tls_session_send(NX_SECURE_TLS_SESSION *session_ptr,
                                    NX_PACKET *packet_ptr,
                                    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="1c3ae-1124">Description</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1124">Description</span></span>

<span data-ttu-id="1c3ae-1125">Bu hizmet, belirtilen etkin TLS NX_PACKET kullanarak ve uzak ana bilgisayara göndermeden önce bu verilerin şifrelemesi işlemesi için sağlanan hizmette verileri gönderir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1125">This service sends data in the supplied NX_PACKET, using the specified active TLS session, and handling the encryption of that data before sending it to the remote host.</span></span> <span data-ttu-id="1c3ae-1126">Alıcının son tanıtan pencere boyutu bu istekten küçükse, hizmet belirtilen bekleme seçeneklerine göre isteğe bağlı olarak askıya alır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1126">If the receiver's last advertised window size is less than this request, the service optionally suspends based on the wait options specified.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1c3ae-1127">*Bir hata döndürül olmadığı sürece, uygulama bu çağrıdan sonra paketi serbest bırakmamalı. Ağ sürücüsü iletimden sonra paketi serbest bıraktıracak olduğundan, bunu yapmak öngörülemeyen sonuçlara neden olur.*</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1127">*Unless an error is returned, the application should not release the packet after this call. Doing so will cause unpredictable results because the network driver will release the packet after transmission.*</span></span>

### <a name="parameters"></a><span data-ttu-id="1c3ae-1128">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1128">Parameters</span></span>

- <span data-ttu-id="1c3ae-1129">**session_ptr** TLS Oturumu örneğinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1129">**session_ptr** Pointer to a TLS Session instance.</span></span>
- <span data-ttu-id="1c3ae-1130">**packet_ptr** Gönderilecek verileri içeren bir TLS paketinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1130">**packet_ptr** Pointer to a TLS packet containing data to be sent.</span></span>
- <span data-ttu-id="1c3ae-1131">**wait_option** İstek, alıcının pencere boyutundan büyükse hizmetin nasıl davranacağını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1131">**wait_option** Defines how the service behaves if the request is greater than the window size of the receiver.</span></span>

### <a name="return-values"></a><span data-ttu-id="1c3ae-1132">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1132">Return Values</span></span>

- <span data-ttu-id="1c3ae-1133">**NX_SUCCESS** (0x00) TLS oturumunun başarıyla başlatılıyor.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1133">**NX_SUCCESS** (0x00) Successful initialization of the TLS session.</span></span>
- <span data-ttu-id="1c3ae-1134">**NX_NO_PACKET** (0x01) Veri alınmamıştır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1134">**NX_NO_PACKET** (0x01) No data received.</span></span>
- <span data-ttu-id="1c3ae-1135">**NX_NOT_CONNECTED** (0x38) Temel ALıNAN TCP yuvası artık bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1135">**NX_NOT_CONNECTED** (0x38) The underlying TCP socket is no longer connected.</span></span>
- <span data-ttu-id="1c3ae-1136">**NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) Temel ALıNAN TCP yuvası gönderme işlemi başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1136">**NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) The underlying TCP socket send failed.</span></span>
- <span data-ttu-id="1c3ae-1137">**NX_PTR_ERROR** (0x07) Geçersiz bir işaretçi kullanmayı denedi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1137">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>
- <span data-ttu-id="1c3ae-1138">**NX_SECURE_TLS_SESSION_UNINITIALIZED** (0x101) Sağlanan TLS oturumu başlatılmadı.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1138">**NX_SECURE_TLS_SESSION_UNINITIALIZED** (0x101) The supplied TLS session was not initialized.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1c3ae-1139">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1139">Allowed From</span></span>

<span data-ttu-id="1c3ae-1140">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1140">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1c3ae-1141">Örnek</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1141">Example</span></span>

```C
/* Send a packet using an active TLS session previously created and started with
nx_secure_tls_session_start. Wait until a packet is sent, blocking otherwise.   */
status =  nx_secure_tls_session_send(&tls_session, &packet_ptr, NX_WAIT_FOREVER);


/* If status is NX_SUCCESS the packet has been sent. */
```

### <a name="see-also"></a><span data-ttu-id="1c3ae-1142">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1142">See Also</span></span>

- <span data-ttu-id="1c3ae-1143">nx_tcp_socket_receive</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1143">nx_tcp_socket_receive</span></span>
- <span data-ttu-id="1c3ae-1144">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1144">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="1c3ae-1145">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1145">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="1c3ae-1146">nx_secure_tls_packet_allocate</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1146">nx_secure_tls_packet_allocate</span></span>
- <span data-ttu-id="1c3ae-1147">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1147">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="1c3ae-1148">nx_secure_tls_session_delete</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1148">nx_secure_tls_session_delete</span></span>
- <span data-ttu-id="1c3ae-1149">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1149">nx_secure_tls_session_receive</span></span>
- <span data-ttu-id="1c3ae-1150">nx_secure_tls_session_end</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1150">nx_secure_tls_session_end</span></span>
- <span data-ttu-id="1c3ae-1151">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1151">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_session_server_callback_set"></a><span data-ttu-id="1c3ae-1152">nx_secure_tls_session_server_callback_set</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1152">nx_secure_tls_session_server_callback_set</span></span>

<span data-ttu-id="1c3ae-1153">TLS sunucusu el sıkışmasının başlangıcında çağırmak üzere TLS için bir geri çağırma ayarlayın</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1153">Set up a callback for TLS to invoke at the beginning of a TLS Server handshake</span></span>

### <a name="prototype"></a><span data-ttu-id="1c3ae-1154">Prototype</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1154">Prototype</span></span>

```C
UINT  nx_secure_tls_ session_server_callback_set (
                 NX_SECURE_TLS_SESSION *tls_session,
                 ULONG (*func_ptr)(NX_SECURE_TLS_SESSION *tls_session,
                                   NX_SECURE_TLS_HELLO_EXTENSION
                                   *extensions, UINT num_extensions));
```

### <a name="description"></a><span data-ttu-id="1c3ae-1155">Description</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1155">Description</span></span>

<span data-ttu-id="1c3ae-1156">Bu hizmet, TLS sunucusu el sıkışması bir ClientHello iletisi aldığında TLS 'nin çağıracağı bir TLS oturumuna bir işlev işaretçisi atar.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1156">This service assigns a function pointer to a TLS session that TLS will invoke when a TLS Server handshake has received a ClientHello message.</span></span> <span data-ttu-id="1c3ae-1157">Geri arama işlevi, bir uygulamanın giriş veya karar verme gerektiren alınan ClientHello iletisindeki TLS uzantılarını işlemesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1157">The callback function allows an application to process any TLS extensions from the received ClientHello message that require input or decision making.</span></span>

<span data-ttu-id="1c3ae-1158">Geri çağırma, TLS oturum denetim bloğu ve NX_SECURE_TLS_HELLO_EXTENSION nesnelerinden oluşan bir dizi ile yürütülür.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1158">The callback is executed with the invoking TLS session control block and an array of NX_SECURE_TLS_HELLO_EXTENSION objects.</span></span> <span data-ttu-id="1c3ae-1159">Uzantı nesnelerinin dizisi, belirli bir uzantıyı bulacak ve ayrıştıracak bir yardımcı işleve geçirilmesi amaçlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1159">The array of extension objects is intended to be passed into a helper function that will find and parse a specific extension.</span></span> <span data-ttu-id="1c3ae-1160">Merhaba iletilerde sunulan TLS uzantılarını ayrıştırır örnek bir yardımcı işlev için bkz. *nx_secure_tls_session_sni_extension_parse*.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1160">For an example helper function that parses TLS extensions provided in hello messages, see *nx_secure_tls_session_sni_extension_parse*.</span></span>

<span data-ttu-id="1c3ae-1161">Sunucu geri çağırması, TLS sunucusu için *nx_secure_tls_active_certificate_set* kullanarak etkin kimlik sertifikasını seçmek için de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1161">The server callback may also be used to select the active identity certificate using *nx_secure_tls_active_certificate_set* for the TLS Server.</span></span> <span data-ttu-id="1c3ae-1162">Bu, çoğu zaman bir Sunucu Adı Belirtme (SNı) uzantısına yanıt olarak oluşur ve bu da bir TLS Istemcisinin hangi sunucuyu iletişim kurmaya çalıştığını belirlemesine izin verir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1162">This will most often occur in response to a Server Name Indication (SNI) extension which allows a TLS Client to indicate which server it is attempting to contact.</span></span> <span data-ttu-id="1c3ae-1163">Daha fazla bilgi için *nx_secure_tls_session_sni_extension_parse* ve *nx_secure_tls_active_certificate_set* başvurularına bakın.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1163">See the references for *nx_secure_tls_session_sni_extension_parse* and *nx_secure_tls_active_certificate_set* for more information.</span></span>

### <a name="parameters"></a><span data-ttu-id="1c3ae-1164">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1164">Parameters</span></span>

- <span data-ttu-id="1c3ae-1165">**session_ptr** Daha önce oluşturulmuş bir TLS oturum örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1165">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="1c3ae-1166">**func_ptr** TLS Sunucusu geri çağırma işlevinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1166">**func_ptr** Pointer to the TLS Server callback function.</span></span>

### <a name="return-values"></a><span data-ttu-id="1c3ae-1167">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1167">Return Values</span></span>

- <span data-ttu-id="1c3ae-1168">**NX_SUCCESS** (0x00) İşlev işaretçisinin başarıyla ayırması.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1168">**NX_SUCCESS** (0x00) Successful allocation of Function pointer.</span></span>
- <span data-ttu-id="1c3ae-1169">**NX_PTR_ERROR** (0x07) Geçersiz TLS oturum işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1169">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1c3ae-1170">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1170">Allowed From</span></span>

<span data-ttu-id="1c3ae-1171">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1171">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1c3ae-1172">Örnek</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1172">Example</span></span>

```C
/* Application-supplied function to map server DNS name to a specific certificate
   ID. The certificate ID is supplied by the application when the certificate is
   added with nx_secure_tls_server_certificate_add. */
UINT application_find_id_by_dns_name(NX_SECURE_X509_DNS_NAME *dns_name)
{
    if(strncmp(dns_name->nx_secure_x509_dns_name, “server_name”,
               dns_name->nx_secure_x509_dns_name_length) == 0)
    {
        /* DNS name matches one we know, return it’s ID. */
        return(0x12);
    }

    /* Unknown DNS name, return 0 to indicate no matching ID found. */
    return(0);
}

/* Callback routine used to process ClientHello extensions and perform other
   runtime actions at the beginning of a TLS handshake (such as selecting an
   identify certificate to provide to the client). */
ULONG tls_server_callback(NX_SECURE_TLS_SESSION *session,
                          NX_SECURE_TLS_HELLO_EXTENSION *extensions, UINT
                          num_extensions)
{
UINT status;
NX_SECURE_X509_DNS_NAME dns_name;
UINT cert_id;
NX_SECURE_X509_CERT *certificate;


    /* Find and parse a Server Name Indication (SNI) extension. */
    status = nx_secure_tls_session_sni_extension_parse(session, extensions,
                                                       num_extensions, &dns_name);

    if(status != NX_SUCCESS && status != NX_SECURE_TLS_EXTENSION_NOT_FOUND)
    {
        /* Parsed an invalid extension, return the error. */
        return(status);
    }

    if(status == NX_SECURE_TLS_EXTENSION_NOT_FOUND)
    {
            /* SNI extension not found, just return success to use the default
               certificate. */
            return(NX_SUCCESS);
    }

    /* Find the application-supplied numeric identifier for the specified DNS
       name provided by the remote client. */
    cert_id = application_find_id_by_dns_name(&dns_name);

    /* If cert_id is 0, just use the default identity certificate added with
       nx_secure_tls_local_certificate_add. */
    if(cert_id != 0)
    {
        /* Application found a matching name, find the certificate in our
           store. */
        status = nx_secure_tls_server_certificate_find(tls_session, &certificate,
                                                       cert_id);

        if(status != NX_SUCCESS)
        {
            /* Didn’t find a valid certificate with the supplied ID. Return an
               error so TLS can shut down the handshake. */
            return(NX_SECURE_TLS_CERTIFICATE_NOT_FOUND);
        }

        /* Set the active identity certificate – the certificate should have been
           added to the local store at application start with
           nx_secure_tls_local_certificate_add. */
        nx_secure_tls_active_certificate_set(session, certificate);
    }

    return(NX_SUCCESS);
}

/* TLS setup routine. */
UINT tls_setup(NX_SECURE_TLS_SESSION *tls_session)
{
        /* Add callback to TLS session.  */
        status =  nx_secure_tls_session_server_callback_set(tls_session,
                                                            server_callback);

        /* If status is NX_SUCCESS the callback was added and will be invoked
           immediately after a ClientHello message is received. */

        return(status);
}
```

### <a name="see-also"></a><span data-ttu-id="1c3ae-1173">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1173">See Also</span></span>

- <span data-ttu-id="1c3ae-1174">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1174">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="1c3ae-1175">nx_secure_tls_session_client_callback_set</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1175">nx_secure_tls_session_client_callback_set</span></span>
- <span data-ttu-id="1c3ae-1176">nx_secure_tls_active_certificate_set</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1176">nx_secure_tls_active_certificate_set</span></span>
- <span data-ttu-id="1c3ae-1177">nx_secure_tls_session_sni_extension_parse</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1177">nx_secure_tls_session_sni_extension_parse</span></span>
- <span data-ttu-id="1c3ae-1178">nx_secure_tls_server_certificate_add</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1178">nx_secure_tls_server_certificate_add</span></span>
- <span data-ttu-id="1c3ae-1179">nx_secure_tls_server_certificate_find</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1179">nx_secure_tls_server_certificate_find</span></span>

## <a name="nx_secure_tls_session_sni_extension_parse"></a><span data-ttu-id="1c3ae-1180">nx_secure_tls_session_sni_extension_parse</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1180">nx_secure_tls_session_sni_extension_parse</span></span>

<span data-ttu-id="1c3ae-1181">TLS İstemcisi Sunucu Adı Belirtme alınan bir Sunucu Adı Belirtme (SNI) uzantısını ayrıştırma</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1181">Parse a Server Name Indication (SNI) extension received from a TLS Client</span></span>

### <a name="prototype"></a><span data-ttu-id="1c3ae-1182">Prototype</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1182">Prototype</span></span>

```C
UINT  nx_secure_tls_session_sni_extension_parse(
                                    NX_SECURE_TLS_SESSION *session_ptr,
                                    NX_SECURE_TLS_HELLO_EXTENSION
                                    *extensions,
                                    UINT num_extensions,
                                    NX_SECURE_X509_DNS_NAME *dns_name);
```

### <a name="description"></a><span data-ttu-id="1c3ae-1183">Description</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1183">Description</span></span>

<span data-ttu-id="1c3ae-1184">Bu hizmetin, bir TLS Sunucusu oturum geri çağırması içinde çağrılarak bir TLS oturumuna çağrıl nx_secure_tls_session_server_callback_set.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1184">This service is intended to be called from within a TLS Server session callback, added to a TLS session using nx_secure_tls_session_server_callback_set.</span></span> <span data-ttu-id="1c3ae-1185">Geri çağırma, uzak bir TLS istemcisinde ClientHello iletisinin alımından sonra çağrılır ve bir dizi kullanılabilir uzantı (ve dizide uzantı sayısı) sağlanır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1185">The callback is invoked following the reception of a ClientHello message from a remote TLS client and is supplied an array of available extensions (and the number of extensions in the array).</span></span> <span data-ttu-id="1c3ae-1186">Bu dizi ve uzunluğu, mevcut bir SNI uzantısı olup olmadığını belirlemek için doğrudan bu yordama geçirebilirsiniz; yoksa NX_SECURE_TLS_EXTENSION_NOT_FOUND yalnızca istemcinin SNI uzantısını provice almayı tercih etmiş olduğunu gösterir (bu bir hata değildir).</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1186">That array and its length can be passed directly to this routine to determine if there is an SNI extension present – if not, NX_SECURE_TLS_EXTENSION_NOT_FOUND is returned indicating simply that the client opted not to provice the SNI extension (this is not an error).</span></span>

<span data-ttu-id="1c3ae-1187">SNI uzantısı bulunursa TLS istemcisi tarafından sağlanan X.509 DNS adı, dns_name döndürülür.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1187">If the SNI extension is found, the X.509 DNS name supplied by the TLS client is returned in the dns_name structure.</span></span> <span data-ttu-id="1c3ae-1188">Şu anda SNI uzantısı yalnızca tek bir DNS adı girişi sağlar ve bu giriş TLS sunucusu tarafından uzak istemciye hangi kimlik sertifikasının gönderileceğini belirlemek için kullanılabilir.\*\*</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1188">Currently, the SNI extension only supplies a single DNS name entry, which may be used by the TLS server to determine which identity certificate to send to the remote client.\*\*</span></span>

<span data-ttu-id="1c3ae-1189">Bu NX_SECURE_X509_DNS_NAME, dns adını yalnızca nx_secure_x509_dns_name alanında UCHAR dizesi  olarak ve *nx_secure_x509_dns_name_length.*</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1189">The NX_SECURE_X509_DNS_NAME structure simply contains the DNS name as a UCHAR string in the field *nx_secure_x509_dns_name* and the length of the name string in *nx_secure_x509_dns_name_length*.</span></span> <span data-ttu-id="1c3ae-1190">Makro NX_SECURE_X509_DNS_NAME_MAX arabelleğinin boyutunu nx_secure_x509_dns_name sağlar.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1190">The macro NX_SECURE_X509_DNS_NAME_MAX controls the size of the nx_secure_x509_dns_name buffer.</span></span>

### <a name="parameters"></a><span data-ttu-id="1c3ae-1191">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1191">Parameters</span></span>

- <span data-ttu-id="1c3ae-1192">**session_ptr** TLS Oturumu örneğinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1192">**session_ptr** Pointer to a TLS Session instance.</span></span>
- <span data-ttu-id="1c3ae-1193">**Uzantılar** Bir TLS Merhaba uzantısı dizisine yönelik işaretçi (oturum geri çağırmada).</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1193">**extensions** Pointer to an array of TLS Hello extensions (from session callback).</span></span>
- <span data-ttu-id="1c3ae-1194">**num_extensions** Dizideki uzantı sayısı (oturum geri çağrısından).</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1194">**num_extensions** Number of extensions in array (from session callback).</span></span>
- <span data-ttu-id="1c3ae-1195">**dns_name** SNı uzantısında sağlanan DNS adını döndürür.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1195">**dns_name** Return DNS name supplied in the SNI extension.</span></span>

### <a name="return-values"></a><span data-ttu-id="1c3ae-1196">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1196">Return Values</span></span>

- <span data-ttu-id="1c3ae-1197">Uzantının başarılı ayrıştırması **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1197">**NX_SUCCESS** (0x00) Successful parsing of the extension.</span></span>
- <span data-ttu-id="1c3ae-1198">**NX_PTR_ERROR** (0x07) geçersiz uzantılar DIZISI veya TLS oturum işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1198">**NX_PTR_ERROR** (0x07) Invalid extensions array or TLS session pointer.</span></span>
- <span data-ttu-id="1c3ae-1199">**NX_SECURE_TLS_EXTENSION_NOT_FOUND** (0x136) SNI uzantısı bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1199">**NX_SECURE_TLS_EXTENSION_NOT_FOUND** (0x136) SNI extension not found.</span></span>
- <span data-ttu-id="1c3ae-1200">**NX_SECURE_TLS_SNI_EXTENSION_INVALID** (0x137) SNI uzantı biçimi geçersizdi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1200">**NX_SECURE_TLS_SNI_EXTENSION_INVALID** (0x137) SNI extension format was invalid.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1c3ae-1201">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1201">Allowed From</span></span>

<span data-ttu-id="1c3ae-1202">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1202">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1c3ae-1203">Örnek</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1203">Example</span></span>

### <a name="see-also"></a><span data-ttu-id="1c3ae-1204">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1204">See Also</span></span>

- <span data-ttu-id="1c3ae-1205">nx_secure_tls_session_server_callback_set</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1205">nx_secure_tls_session_server_callback_set</span></span>
- <span data-ttu-id="1c3ae-1206">nx_secure_tls_session_client_callback_set</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1206">nx_secure_tls_session_client_callback_set</span></span>
- <span data-ttu-id="1c3ae-1207">nx_secure_tls_server_callback_set</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1207">nx_secure_tls_server_callback_set</span></span>
- <span data-ttu-id="1c3ae-1208">nx_secure_tls_active_certificate_set</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1208">nx_secure_tls_active_certificate_set</span></span>

## <a name="nx_secure_tls_session_sni_extension_set"></a><span data-ttu-id="1c3ae-1209">nx_secure_tls_session_sni_extension_set</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1209">nx_secure_tls_session_sni_extension_set</span></span>

<span data-ttu-id="1c3ae-1210">Bir Sunucu Adı Belirtme (SNı) uzantısı DNS adını uzak bir sunucuya göndermek üzere ayarla</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1210">Set a Server Name Indication (SNI) extension DNS name to send to a remote Server</span></span>

### <a name="prototype"></a><span data-ttu-id="1c3ae-1211">Prototype</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1211">Prototype</span></span>

```C
UINT  nx_secure_tls_session_sni_extension_set(
                                    NX_SECURE_TLS_SESSION *session_ptr,
                                    NX_SECURE_X509_DNS_NAME *dns_name);
```

### <a name="description"></a><span data-ttu-id="1c3ae-1212">Description</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1212">Description</span></span>

<span data-ttu-id="1c3ae-1213">Bu hizmet, bir TLS Istemci uygulamasının, Sunucu Adı Belirtme (SNı) TLS uzantısını kullanarak uzak bir TLS sunucusuna tercih edilen sunucu DNS adı sağlamasına izin verir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1213">This service allows a TLS Client application to provide a preferred server DNS name to a remote TLS server using the Server Name Indication (SNI) TLS extension.</span></span> <span data-ttu-id="1c3ae-1214">SNı uzantısı, sunucunun belirtilen sunucu tercihini temel alarak uygun kimlik sertifikası ve parametrelerini seçmesine olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1214">The SNI extension allows the server to select the proper identity certificate and parameters based on the client's indicated server preference.</span></span> <span data-ttu-id="1c3ae-1215">SNı uzantısı Şu anda yalnızca gönderilecek tek bir DNS adını, dolayısıyla tekil ad parametresini destekliyor.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1215">The SNI extension currently only supports a single DNS name to be sent, hence the singular name parameter.</span></span> <span data-ttu-id="1c3ae-1216">Dns_name parametresi *nx_secure_x509_dns_name_initialize* birlikte başlatılmalıdır ve istemcinin tercih edilen sunucusunu içerecek şekilde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1216">The dns_name parameter must be initialized with *nx_secure_x509_dns_name_initialize* and will contain the client's preferred server.</span></span> <span data-ttu-id="1c3ae-1217">Uzantı adını kaldırmak için bu hizmeti NX_NULL bir "dns_name" parametre değeri ile çağırmanız yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1217">To unset the extension name, simply call this service with a "dns_name" parameter value of NX_NULL.</span></span>

<span data-ttu-id="1c3ae-1218">NX_SECURE_X509_DNS_NAME yapısı, DNS adını alan  *nx_secure_x509_dns_name* BIR uşar dizesi olarak ve *nx_secure_x509_dns_name_length* ad dizesinin uzunluğu olarak içerir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1218">The NX_SECURE_X509_DNS_NAME structure simply contains the DNS name as a UCHAR string in the field  *nx_secure_x509_dns_name* and the length of the name string in *nx_secure_x509_dns_name_length*.</span></span> <span data-ttu-id="1c3ae-1219">Makro NX_SECURE_X509_DNS_NAME_MAX arabelleğinin boyutunu nx_secure_x509_dns_name sağlar.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1219">The macro  NX_SECURE_X509_DNS_NAME_MAX controls the size of the nx_secure_x509_dns_name buffer.</span></span>

> [!NOTE]
> <span data-ttu-id="1c3ae-1220">*Bu yordam, çağrılmadan nx_secure_tls_session_start veya ClientHello SNI uzantısını içermez.*</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1220">*This routine must be called before nx_secure_tls_session_start is invoked or the ClientHello will not contain the SNI extension.*</span></span>

### <a name="parameters"></a><span data-ttu-id="1c3ae-1221">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1221">Parameters</span></span>

- <span data-ttu-id="1c3ae-1222">**session_ptr** TLS Oturumu örneğinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1222">**session_ptr** Pointer to a TLS Session instance.</span></span>
- <span data-ttu-id="1c3ae-1223">**dns_name** Uygulama tarafından sağlanan DNS adı.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1223">**dns_name** DNS name supplied by the application.</span></span>

### <a name="return-values"></a><span data-ttu-id="1c3ae-1224">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1224">Return Values</span></span>

- <span data-ttu-id="1c3ae-1225">**NX_SUCCESS** (0x00) DNS sunucusu adı başarıyla ekleme.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1225">**NX_SUCCESS** (0x00) Successful addition of DNS server name.</span></span>
- <span data-ttu-id="1c3ae-1226">**NX_PTR_ERROR** (0x07) Geçersiz DNS adı veya TLS oturum işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1226">**NX_PTR_ERROR** (0x07) Invalid DNS name or TLS session pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1c3ae-1227">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1227">Allowed From</span></span>

<span data-ttu-id="1c3ae-1228">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1228">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1c3ae-1229">Örnek</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1229">Example</span></span>

```C
#define TLS_SNI_SERVER_NAME “www.example.com”

NX_SECURE_X509_DNS_NAME dns_name;
NX_SECURE_TLS_SESSION client_tls_session;

/* Application where TLS session is started. */
void main()
{
    /* Create a TLS session for our socket. Ciphers and metadata defined
       elsewhere. See nx_secure_tls_session_create reference for more
       information. */
    status =  nx_secure_tls_session_create(&client_tls_session,
                                           &nx_crypto_tls_ciphers,
                                           server_crypto_metadata,
                                           sizeof(server_crypto_metadata));


    /* Initialize the DNS server name we want to send in the SNI extension. */
    nx_secure_x509_dns_name_initialize(&dns_name, TLS_SNI_SERVER_NAME,
                                    strlen(TLS_SNI_SERVER_NAME));

    /* The SNI server name needs to be set prior to starting the TLS session. */
    nx_secure_tls_session_sni_extension_set(&tls_session, &dns_name);

   /* Start TLS session as normal. */
}
```

### <a name="see-also"></a><span data-ttu-id="1c3ae-1230">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1230">See Also</span></span>

- <span data-ttu-id="1c3ae-1231">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1231">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="1c3ae-1232">nx_secure_x509_dns_name_initialize</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1232">nx_secure_x509_dns_name_initialize</span></span>

## <a name="nx_secure_tls_session_start"></a><span data-ttu-id="1c3ae-1233">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1233">nx_secure_tls_session_start</span></span>

<span data-ttu-id="1c3ae-1234">NetX Güvenli TLS Oturumu Başlatma</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1234">Start a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="1c3ae-1235">Prototype</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1235">Prototype</span></span>

```C
UINT  nx_secure_tls_session_start(NX_SECURE_TLS_SESSION *session_ptr,
                                  NX_TCP_SOCKET *tcp_socket_ptr,
                                  ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="1c3ae-1236">Description</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1236">Description</span></span>

<span data-ttu-id="1c3ae-1237">Bu hizmet, sağlanan TLS oturum denetim bloğu ve bağlı bir TCP yuvası kullanarak bir TLS oturumu başlatır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1237">This service starts a TLS session using the supplied TLS session control block and a connected TCP socket.</span></span> <span data-ttu-id="1c3ae-1238">Tcp bağlantısının başarılı bir çağrıdan sonra ya nx_tcp_client_socket_connect veya nx_tcp_server_socket_accept.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1238">The TCP connection must already be complete following a successful call to either nx_tcp_client_socket_connect or nx_tcp_server_socket_accept.</span></span>

<span data-ttu-id="1c3ae-1239">Bu hizmet, TCP yuvasından TLS oturumunun türünü (İstemci veya Sunucu) belirler.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1239">This service will determine the type of TLS session (Client or Server) from the TCP socket.</span></span>

<span data-ttu-id="1c3ae-1240">Bekleme seçeneği, TLS el sıkışması devam ederken hizmetin nasıl davranacağını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1240">The wait option defines how the service behaves while the TLS handshake is in progress.</span></span>

### <a name="parameters"></a><span data-ttu-id="1c3ae-1241">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1241">Parameters</span></span>

- <span data-ttu-id="1c3ae-1242">**session_ptr** TLS Oturumu örneğinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1242">**session_ptr** Pointer to a TLS Session instance.</span></span>
- <span data-ttu-id="1c3ae-1243">**tcp_socket_ptr** Bağlı bir TCP yuvasının işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1243">**tcp_socket_ptr** Pointer to a connected TCP socket.</span></span>
- <span data-ttu-id="1c3ae-1244">**wait_option** TLS el sıkışması devam ederken hizmetin nasıl davranacağını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1244">**wait_option** Defines how the service behaves while the TLS handshake is in progress.</span></span>

### <a name="return-values"></a><span data-ttu-id="1c3ae-1245">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1245">Return Values</span></span>

- <span data-ttu-id="1c3ae-1246">**NX_SUCCESS** (0x00) TLS oturumunun başarıyla başlatılıyor.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1246">**NX_SUCCESS** (0x00) Successful initialization of the TLS session.</span></span>
- <span data-ttu-id="1c3ae-1247">**NX_NOT_CONNECTED** (0x38) Temel ALıNAN TCP yuvası artık bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1247">**NX_NOT_CONNECTED** (0x38) The underlying TCP socket is no longer connected.</span></span>
- <span data-ttu-id="1c3ae-1248">**NX_SECURE_TLS_UNRECOGNIZED_MESSAGE_TYPE** (0x102) ALıNAN bir TLS ileti türü yanlış.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1248">**NX_SECURE_TLS_UNRECOGNIZED_MESSAGE_TYPE** (0x102) A received TLS message type is incorrect.</span></span>
- <span data-ttu-id="1c3ae-1249">**NX_SECURE_TLS_UNSUPPORTED_CIPHER** (0x106) uzak ana bilgisayar tarafından sağlanmış bir şifre desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1249">**NX_SECURE_TLS_UNSUPPORTED_CIPHER** (0x106) A cipher provided by the remote host is not supported.</span></span>
- <span data-ttu-id="1c3ae-1250">TLS el sıkışması sırasında **NX_SECURE_TLS_HANDSHAKE_FAILURE** (0x107) ileti işleme başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1250">**NX_SECURE_TLS_HANDSHAKE_FAILURE** (0x107) Message processing during the TLS handshake has failed.</span></span>
- <span data-ttu-id="1c3ae-1251">**NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0x108) gelen bir ILETI karma Mac denetiminde başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1251">**NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0x108) An incoming message failed a hash MAC check.</span></span>
- <span data-ttu-id="1c3ae-1252">**NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) temel alınan TCP yuvası gönderme başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1252">**NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) An underlying TCP socket send failed.</span></span>
- <span data-ttu-id="1c3ae-1253">**NX_SECURE_TLS_INCORRECT_MESSAGE_LENGTH** (0x10a) gelen iletide geçersiz uzunluk alanı vardı.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1253">**NX_SECURE_TLS_INCORRECT_MESSAGE_LENGTH** (0x10A) An incoming message had an invalid length field.</span></span>
- <span data-ttu-id="1c3ae-1254">**NX_SECURE_TLS_BAD_CIPHERSPEC** (0x10b) gelen bir Changecyaspec iletisi hatalı.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1254">**NX_SECURE_TLS_BAD_CIPHERSPEC** (0x10B) An incoming ChangeCipherSpec message was incorrect.</span></span>
- <span data-ttu-id="1c3ae-1255">**NX_SECURE_TLS_INVALID_SERVER_CERT** (0x10c) uzak TLS sunucusunu tanımlamak Için gelen bir TLS sertifikası kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1255">**NX_SECURE_TLS_INVALID_SERVER_CERT** (0x10C) An incoming TLS certificate is unusable for identifying the remote TLS server.</span></span>
- <span data-ttu-id="1c3ae-1256">**NX_SECURE_TLS_UNSUPPORTED_PUBLIC_CIPHER** (0x10d) uzak ana bilgisayar tarafından sunulan ortak anahtar şifresi desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1256">**NX_SECURE_TLS_UNSUPPORTED_PUBLIC_CIPHER** (0x10D) The public-key cipher provided by the remote host is unsupported.</span></span>
- <span data-ttu-id="1c3ae-1257">**NX_SECURE_TLS_NO_SUPPORTED_CIPHERS** (0x10e) uzak ana bilgisayar, NETX güvenli TLS yığını tarafından desteklenen ciphersuites belirtti.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1257">**NX_SECURE_TLS_NO_SUPPORTED_CIPHERS** (0x10E) The remote host has indicated no ciphersuites that are supported by the NetX Secure TLS stack.</span></span>
- <span data-ttu-id="1c3ae-1258">**NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0x10F) ALıNAN bir TLS iletisinde üst bilgisinde BILINMEYEN bir TLS sürümü vardı.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1258">**NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0x10F) A received TLS message had an unknown TLS version in its header.</span></span>
- <span data-ttu-id="1c3ae-1259">**NX_SECURE_TLS_UNSUPPORTED_TLS_VERSION** (0x110) ALıNAN bir TLS iletisinde, üstbilgisinde bilinen ancak desteklenmeyen bir TLS sürümü vardı.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1259">**NX_SECURE_TLS_UNSUPPORTED_TLS_VERSION** (0x110) A received TLS message had a known but unsupported TLS version in its header.</span></span>
- <span data-ttu-id="1c3ae-1260">**NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) BIR iç TLS paket ayırması başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1260">**NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) An internal TLS packet allocation failed.</span></span>
- <span data-ttu-id="1c3ae-1261">**NX_SECURE_TLS_INVALID_CERTIFICATE** (0x112) uzak ana bilgisayar geçersiz bir sertifika sağladı.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1261">**NX_SECURE_TLS_INVALID_CERTIFICATE** (0x112) The remote host provided an invalid certificate.</span></span>
- <span data-ttu-id="1c3ae-1262">**NX_SECURE_TLS_ALERT_RECEIVED** (0x114) uzak ana bilgisayar bir hatayı BELIRTEN ve TLS oturumunu sonlandıran bir uyarı gönderdi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1262">**NX_SECURE_TLS_ALERT_RECEIVED** (0x114) The remote host sent an alert indicating an error and ending the TLS session.</span></span>
- <span data-ttu-id="1c3ae-1263">**NX_SECURE_TLS_MISSING_CRYPTO_ROUTINE** (0x13b) ciphersuite tablosundaki BIR girdinin null işlev işaretçisi vardı.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1263">**NX_SECURE_TLS_MISSING_CRYPTO_ROUTINE** (0x13B) An entry in the ciphersuite table had a NULL function pointer.</span></span>
- <span data-ttu-id="1c3ae-1264">**NX_SECURE_TLS_INAPPROPRIATE_FALLBACK** (0x146) BIR uzak TLS ClientHello, GERI dönüş SCSV bir sürüm geri dönüşü içeriyordu.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1264">**NX_SECURE_TLS_INAPPROPRIATE_FALLBACK** (0x146) A remote TLS ClientHello included the fallback SCSV andattempted a version fallback.</span></span>
- <span data-ttu-id="1c3ae-1265">**NX_PTR_ERROR** (0x07) geçersiz bir Işaretçi kullanmaya çalıştı.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1265">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1c3ae-1266">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1266">Allowed From</span></span>

<span data-ttu-id="1c3ae-1267">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1267">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1c3ae-1268">Örnek</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1268">Example</span></span>

```C
NX_TCP_SOCKET tcp_socket;
NX_SECURE_TLS_SESSION tls_session;
NX_SECURE_X509_CERT certificate;

/* Initialize the TLS session structure. */
nx_secure_tls_session_create(&tls_session,
                              &nx_crypto_tls_ciphers,
                              crypto_metadata,
                              sizeof(crypto_metadata));

/* Setup the TLS packet reassembly buffer. */
status = nx_secure_tls_session_packet_buffer_set(&tls_session, tls_packet_buffer,
                                                 sizeof(tls_packet_buffer));

/* Initialize a certificate for the TLS server. */
status =  nx_secure_x509_certificate_initialize(&certificate, certificate_data, 500,
NX_NULL, 0, private_key, 64);

/* If status is NX_SUCCESS, certificate is initialized. */

/* Add the certificate a local certificate to identify this TLS server. */
status = nx_secure_tls_add_local_certificate(&tls_session, &certificate);

/* If status is NX_SUCCESS, certificate was added successfully. */

/* Create and start a TCP socket as a server. */
/* NOTE: This assumes an IP instance called “ip_0” has already been created. */

/* Create a TCP server socket on the previously created IP instance, with normal
   delivery, IP fragmentation enabled, default time to live, a 8192-byte receive
   window, no urgent callback routine, and the "client_disconnect" routine to
   handle disconnection initiated from the other end of the connection.  */
status =  nx_tcp_socket_create(&ip_0, &tcp_socket, "TLS Server Socket", NX_IP_NORMAL,
                               NX_FRAGMENT_OKAY, NX_IP_TIME_TO_LIVE, 8192, NX_NULL,
                               NX_NULL);

/* If status is NX_SUCCESS, the TCP socket was created successfully. */

/* Start up a TCP server socket by listening on port 443 with a listen queue of
   size 5. */
status =  nx_tcp_server_socket_listen(&ip_0, 443, &tcp_socket, 5, NX_NULL);

/* Application main loop. */
while(1)
{
        /* Accept incoming requests on the TCP socket. */
        status =  nx_tcp_server_socket_accept(&tcp_socket, NX_WAIT_FOREVER);

        /* At this point, the TCP socket should be established (but not the TLS
        session yet). */

        /* Start the TLS session on our active TCP socket. */
        status = nx_secure_tls_session_start(&tls_session, &tcp_socket,
                                             NX_WAIT_FOREVER);

        /* At this point, if status is NX_SUCCESS, the TLS session has been
           established.  Application may now send/receive data through this
           channel. */

        /* Send and receive data using the TLS session. */
        /* Allocate TLS packets using nx_secure_tls_packet_allocate, write data with
           nx_packet_data_append, read data with nx_packet_data_extract_offset. */

        /* Send TLS data. */
        nx_secure_tls_session_send(&tls_session, &send_packet, NX_WAIT_FOREVER);

        nx_secure_tls_session_receive(&tls_session, &receive_packet_ptr,
        NX_WAIT_FOREVER);


        /* Once all application data is sent/received, end the TLS session. */
        status = nx_secure_tls_session_end(&tls_session);

        /* If status is NX_SUCCESS, the TLS session has been closed properly. */

        /* Now disconnect the TCP server socket from the client.  */
        nx_tcp_socket_disconnect(&tcp_socket, 200);

        /* Unaccept the TCP server socket.  Note that unaccept is called even if
           disconnect or accept fails.  */
        nx_tcp_server_socket_unaccept(&tcp_socket);

        /* Setup server socket for listening with this socket again.  */
        nx_tcp_server_socket_relisten(&ip_0, 443, &tcp_socket);
}

/* When the server application is shut down, clean up the TLS session. */
nx_secure_tls_session_delete(&tls_session);

/* Finally, clean up the TCP socket as well. */
nx_tcp_socket_delete(&tcp_socket);
```

### <a name="see-also"></a><span data-ttu-id="1c3ae-1269">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1269">See Also</span></span>

- <span data-ttu-id="1c3ae-1270">nx_tcp_socket_receive</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1270">nx_tcp_socket_receive</span></span>
- <span data-ttu-id="1c3ae-1271">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1271">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="1c3ae-1272">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1272">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="1c3ae-1273">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1273">nx_secure_tls_session_send</span></span>
- <span data-ttu-id="1c3ae-1274">nx_secure_tls_session_delete</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1274">nx_secure_tls_session_delete</span></span>
- <span data-ttu-id="1c3ae-1275">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1275">nx_secure_tls_session_receive</span></span>
- <span data-ttu-id="1c3ae-1276">nx_secure_tls_packet_allocate</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1276">nx_secure_tls_packet_allocate</span></span>
- <span data-ttu-id="1c3ae-1277">nx_secure_tls_session_end</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1277">nx_secure_tls_session_end</span></span>
- <span data-ttu-id="1c3ae-1278">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1278">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="1c3ae-1279">nx_tcp_socket_accept</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1279">nx_tcp_socket_accept</span></span>
- <span data-ttu-id="1c3ae-1280">nx_tcp_socket_listen</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1280">nx_tcp_socket_listen</span></span>
- <span data-ttu-id="1c3ae-1281">nx_tcp_socket_disconnect</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1281">nx_tcp_socket_disconnect</span></span>
- <span data-ttu-id="1c3ae-1282">nx_tcp_socket_unaccept</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1282">nx_tcp_socket_unaccept</span></span>
- <span data-ttu-id="1c3ae-1283">nx_tcp_socket_relisten</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1283">nx_tcp_socket_relisten</span></span>
- <span data-ttu-id="1c3ae-1284">nx_tcp_socket_delete</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1284">nx_tcp_socket_delete</span></span>
- <span data-ttu-id="1c3ae-1285">nx_packet_allocate</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1285">nx_packet_allocate</span></span>
- <span data-ttu-id="1c3ae-1286">nx_packet_data_append</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1286">nx_packet_data_append</span></span>
- <span data-ttu-id="1c3ae-1287">nx_packet_data_extract_offset</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1287">nx_packet_data_extract_offset</span></span>

## <a name="nx_secure_tls_session_time_function_set"></a><span data-ttu-id="1c3ae-1288">nx_secure_tls_session_time_function_set</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1288">nx_secure_tls_session_time_function_set</span></span>

<span data-ttu-id="1c3ae-1289">NetX Secure TLS Oturumuna zaman damgası işlevi atama</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1289">Assign a timestamp function to a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="1c3ae-1290">Prototype</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1290">Prototype</span></span>

```C
UINT  nx_secure_tls_time_function_set(
                              NX_SECURE_TLS_SESSION *session_ptr,
                              ULONG (*time_func_ptr)(void));
```

### <a name="description"></a><span data-ttu-id="1c3ae-1291">Description</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1291">Description</span></span>

<span data-ttu-id="1c3ae-1292">Bu işlev, ÇEŞITLI TLS el sıkışma iletilerinde ve sertifikaların doğrulanmasında kullanılan geçerli saati almak için TLS'nin çağıracak bir işlev işaretçisi ayarlar.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1292">This function sets up a function pointer that TLS will invoke when it needs to get the current time, which is used in various TLS handshake messages and for verification of certificates.</span></span>

<span data-ttu-id="1c3ae-1293">Bu işlevin, TLS RFC 5246 ' de ClientHello gereksinimlere göre geçerli GMT 'yi UNIX 32 bit biçiminde (gece yarısından itibaren 1, 1970, UTC, daha fazla saniyeler yok saydıktan sonra saniye) döndürmesi beklenir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1293">The function is expected to return the current GMT in UNIX 32-bit format (seconds since the midnight starting Jan 1, 1970, UTC, ignoring leap seconds), as per the ClientHello requirements in the TLS RFC 5246.</span></span>

<span data-ttu-id="1c3ae-1294">Zaman damgası işlevi atanmamışsa, TLS el sıkışmasındaki zaman damgası için 0 değeri kullanılır ve sertifika süre sonu denetimi çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1294">If no timestamp function is assigned, a value of 0 for the timestamp in the TLS handshake will be used and certificate expiration checking will not work.</span></span>

### <a name="parameters"></a><span data-ttu-id="1c3ae-1295">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1295">Parameters</span></span>

- <span data-ttu-id="1c3ae-1296">**session_ptr** Bir TLS oturum örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1296">**session_ptr** Pointer to a TLS Session instance.</span></span>
- <span data-ttu-id="1c3ae-1297">**time_func_ptr** UNIX 32 bit biçiminde geçerli saati (GMT) döndüren bir işlev işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1297">**time_func_ptr** Pointer to a function that returns the current time (GMT) in UNIX 32-bit format.</span></span>

### <a name="return-values"></a><span data-ttu-id="1c3ae-1298">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1298">Return Values</span></span>

- <span data-ttu-id="1c3ae-1299">TLS oturumunun başarıyla başlatılmasından **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1299">**NX_SUCCESS** (0x00) Successful initialization of the TLS session.</span></span>
- <span data-ttu-id="1c3ae-1300">**NX_INVALID_PARAMETERS** (0x4D) geçersiz TLS oturum işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1300">**NX_INVALID_PARAMETERS** (0x4D) Invalid TLS session pointer.</span></span>
- <span data-ttu-id="1c3ae-1301">**NX_PTR_ERROR** (0x07) geçersiz bir Işaretçi kullanmaya çalıştı.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1301">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1c3ae-1302">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1302">Allowed From</span></span>

<span data-ttu-id="1c3ae-1303">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1303">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1c3ae-1304">Örnek</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1304">Example</span></span>

```C
/* This function returns a 32-bit UNIX-style representation of the current GMT
   time. */
ULONG get_gmt_time(void)
{
ULONG time_value;

   /* Platform-specific time calculation goes here… */

   return(time_value);
}

/* Reset a TLS session.  */
status =  nx_secure_tls_timestamp_function_set(&tls_session, get_gmt_time);


/* If status is NX_SUCCESS the function was successfully added.*/
```

### <a name="see-also"></a><span data-ttu-id="1c3ae-1305">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1305">See Also</span></span>

- <span data-ttu-id="1c3ae-1306">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1306">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="1c3ae-1307">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1307">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="1c3ae-1308">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1308">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="1c3ae-1309">nx_secure_tls_session_delete</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1309">nx_secure_tls_session_delete</span></span>
- <span data-ttu-id="1c3ae-1310">nx_secure_tls_session_sendnx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1310">nx_secure_tls_session_sendnx_secure_tls_session_receive</span></span>
- <span data-ttu-id="1c3ae-1311">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1311">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_trusted_certificate_add"></a><span data-ttu-id="1c3ae-1312">nx_secure_tls_trusted_certificate_add</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1312">nx_secure_tls_trusted_certificate_add</span></span>

<span data-ttu-id="1c3ae-1313">NetX güvenli TLS oturumuna güvenilen sertifika ekleme</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1313">Add trusted certificate to NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="1c3ae-1314">Prototype</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1314">Prototype</span></span>

```C
UINT  nx_secure_tls_trusted_certificate_add(NX_SECURE_TLS_SESSION
                            *session_ptr, NX_SECURE_X509_CERT *certificate_ptr);
```

### <a name="description"></a><span data-ttu-id="1c3ae-1315">Description</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1315">Description</span></span>

<span data-ttu-id="1c3ae-1316">Bu hizmet, bir TLS oturumuna başlatılmış bir NX_SECURE_X509_CERT yapısı örneği ekler.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1316">This service adds an initialized NX_SECURE_X509_CERT structure instance to a TLS session.</span></span> <span data-ttu-id="1c3ae-1317">Bu sertifika, TLS el sıkışması sırasında uzak ana bilgisayar tarafından sağlanan sertifikaları doğrulamak için TLS yığını tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1317">This certificate is used by the TLS stack to verify certificates supplied by the remote host during the TLS handshake.</span></span>

<span data-ttu-id="1c3ae-1318">TLS Istemci modu için güvenilen sertifikalar gereklidir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1318">Trusted certificates are required for TLS Client mode.</span></span>

<span data-ttu-id="1c3ae-1319">Güvenilen sertifikalar yalnızca istemci sertifikası kimlik doğrulaması etkinse TLS sunucu modu için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1319">Trusted certificates are only required for TLS Server mode if client certificate authentication is enabled.</span></span>

### <a name="parameters"></a><span data-ttu-id="1c3ae-1320">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1320">Parameters</span></span>

- <span data-ttu-id="1c3ae-1321">**session_ptr** Daha önce oluşturulmuş bir TLS Oturumu örneğinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1321">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="1c3ae-1322">**certificate_ptr** Başlatılan bir TLS Sertifika örneğinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1322">**certificate_ptr** Pointer to an initialized TLS Certificate instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="1c3ae-1323">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1323">Return Values</span></span>

- <span data-ttu-id="1c3ae-1324">**NX_SUCCESS** (0x00) Sertifika başarıyla eksildi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1324">**NX_SUCCESS** (0x00) Successful addition of certificate.</span></span>
- <span data-ttu-id="1c3ae-1325">**NX_INVALID_PARAMETERS** (0x4D) Geçersiz sertifika eklemeye çalıştı.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1325">**NX_INVALID_PARAMETERS** (0x4D) Tried to add an invalid certificate.</span></span>
- <span data-ttu-id="1c3ae-1326">**NX_PTR_ERROR** (0x07) Geçersiz TLS oturum işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1326">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1c3ae-1327">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1327">Allowed From</span></span>

<span data-ttu-id="1c3ae-1328">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1328">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1c3ae-1329">Örnek</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1329">Example</span></span>

```C
/* Initialize certificate structure. */
status = nx_secure_x509_certificate_initialize(&certificate, certificate_data,
                                               certificate_buffer,
                                               sizeof(certificate_buffer), 500,
                                               private_key, 64);

/* Add certificate to TLS session.  */
status =  nx_secure_tls_trusted_certificate_add(&tls_session, &certificate);


/* If status is NX_SUCCESS the certificate was successfully added.  */
```

### <a name="see-also"></a><span data-ttu-id="1c3ae-1330">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1330">See Also</span></span>

- <span data-ttu-id="1c3ae-1331">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1331">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="1c3ae-1332">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1332">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="1c3ae-1333">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1333">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="1c3ae-1334">nx_secure_tls_trusted_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1334">nx_secure_tls_trusted_certificate_remove</span></span>

## <a name="nx_secure_tls_trusted_certificate_remove"></a><span data-ttu-id="1c3ae-1335">nx_secure_tls_trusted_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1335">nx_secure_tls_trusted_certificate_remove</span></span>

<span data-ttu-id="1c3ae-1336">NetX Secure TLS Oturumundan güvenilen sertifikayı kaldırma</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1336">Remove trusted certificate from NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="1c3ae-1337">Prototype</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1337">Prototype</span></span>

```C
UINT  nx_secure_tls_trusted_certificate_remove(
                                    NX_SECURE_TLS_SESSION *session_ptr,
                                    UCHAR *common_name,
                                    UINT common_name_length);
```

### <a name="description"></a><span data-ttu-id="1c3ae-1338">Description</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1338">Description</span></span>

<span data-ttu-id="1c3ae-1339">Bu hizmet, sertifikadaki Ortak Ad alanına anahtarlanan bir TLS oturumundan güvenilen bir sertifikayı kaldırır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1339">This service removes a trusted certificate from a TLS session, keyed on the Common Name field in the certificate.</span></span>

### <a name="parameters"></a><span data-ttu-id="1c3ae-1340">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1340">Parameters</span></span>

- <span data-ttu-id="1c3ae-1341">**session_ptr** Daha önce oluşturulmuş bir TLS Oturumu örneğinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1341">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="1c3ae-1342">**common_name** Kaldırılacak sertifikanın Ortak Ad değeri.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1342">**common_name** The Common Name value of the certificate to be removed.</span></span>
- <span data-ttu-id="1c3ae-1343">**common_name_length** Ortak Ad dizesinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1343">**common_name_length** The length of the Common Name string.</span></span>

### <a name="return-values"></a><span data-ttu-id="1c3ae-1344">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1344">Return Values</span></span>

- <span data-ttu-id="1c3ae-1345">**NX_SUCCESS** (0x00) Sertifika başarıyla eksildi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1345">**NX_SUCCESS** (0x00) Successful addition of certificate.</span></span>
- <span data-ttu-id="1c3ae-1346">**NX_PTR_ERROR** (0x07) Geçersiz TLS oturum işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1346">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>
- <span data-ttu-id="1c3ae-1347">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) Sertifikası bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1347">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) Certificate was not found.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1c3ae-1348">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1348">Allowed From</span></span>

<span data-ttu-id="1c3ae-1349">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1349">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1c3ae-1350">Örnek</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1350">Example</span></span>

```C
/* Remove certificate from TLS session.  */
status =  nx_secure_tls_trusted_certificate_remove(&tls_session,
                                                “www.example.com”, 15);


/* If status is NX_SUCCESS the certificate was successfully removed.  */
```

### <a name="see-also"></a><span data-ttu-id="1c3ae-1351">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1351">See Also</span></span>

- <span data-ttu-id="1c3ae-1352">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1352">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="1c3ae-1353">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1353">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="1c3ae-1354">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1354">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="1c3ae-1355">nx_secure_tls_trusted_certificate_add</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1355">nx_secure_tls_trusted_certificate_add</span></span>

## <a name="nx_secure_x509_certificate_initialize"></a><span data-ttu-id="1c3ae-1356">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1356">nx_secure_x509_certificate_initialize</span></span>

<span data-ttu-id="1c3ae-1357">NetX güvenli TLS için X. 509.440 sertifikasını başlatın</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1357">Initialize X.509 Certificate for NetX Secure TLS</span></span>

### <a name="prototype"></a><span data-ttu-id="1c3ae-1358">Prototype</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1358">Prototype</span></span>

```C
UINT  nx_secure_x509_certificate_initialize(
                  NX_SECURE_X509_CERT *certificate_ptr,
                  const UCHAR *certificate_data,
                  USHORT certificate_data_length,
                  UCHAR *raw_data_buffer,
                  USHORT buffer_size,
                  const UCHAR *private_key_data,
                  USHORT private_key_data_length,
                  UINT private_key_type);
```

### <a name="description"></a><span data-ttu-id="1c3ae-1359">Description</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1359">Description</span></span>

<span data-ttu-id="1c3ae-1360">Bu hizmet, bir TLS oturumunda kullanılmak üzere ikili kodlanmış X. 509.952 dijital sertifikasından bir NX_SECURE_X509_CERT yapısını başlatır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1360">This service initializes an NX_SECURE_X509_CERT structure from a binary-encoded X.509 digital certificate for use in a TLS session.</span></span>

<span data-ttu-id="1c3ae-1361">Sertifika verileri, DER kodlu ikili biçimde geçerli bir X. 509.952 dijital sertifikası **olmalıdır** .</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1361">The certificate data **must** be a valid X.509 digital certificate in DER-encoded binary format.</span></span> <span data-ttu-id="1c3ae-1362">Veriler, bu verilere yönelik bir uşar işaretçisi sağlandığı sürece herhangi bir kaynaktan (ör. dosya sistemi, derlenmiş sabit arabellek, vb.) oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1362">The data can some from any source (e.g. file system, compiled constant buffer, etc.) as long as a UCHAR pointer to that data is provided.</span></span>

<span data-ttu-id="1c3ae-1363">*Raw_data_buffer* parametresi ve boyutu, sertifika verilerinin ayrıştırılmadan önce kopyalandığı ayrılmış bir arabelleği belirten isteğe bağlı parametrelerdir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1363">The *raw_data_buffer* parameter and its size are optional parameters that specify a dedicated buffer into which the certificate data is copied before parsing.</span></span> <span data-ttu-id="1c3ae-1364">Raw_data_buffer NX_NULL olarak geçirilirse NX_SECURE_X509_CERT yapısı doğrudan certificate_data dizisine işaret eder (Bu durumda buffer_size yok sayılır).</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1364">If raw_data_buffer is passed as NX_NULL then the NX_SECURE_X509_CERT structure will point directly into the certificate_data array (buffer_size is ignored in this case).</span></span> <span data-ttu-id="1c3ae-1365">Raw_data_buffer NX_NULL olarak geçirilirse certificate_data işaretçisi tarafından işaret edilen ***verileri değiştirmeyin veya*** sertifika işleme muhtemelen başarısız olur!</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1365">If raw_data_buffer is passed as NX_NULL, ***do not*** modify the data pointed to by the certificate_data pointer or certificate processing will likely fail!</span></span>

<span data-ttu-id="1c3ae-1366">Özel anahtar parametresi yerel kimlik sertifikalarına yöneliktir. özel anahtar, sunucular tarafından bir istemciden gelen anahtar verilerinin şifresini çözmek (sunucunun ortak anahtarı kullanılarak şifrelenir) ve istemciler tarafından sunucu istemci sertifikası istediğinde bir sunucuya kimliklerini doğrulamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1366">The private key parameter is for local identity certificates – the private key is used by servers to decrypt the incoming key data from a client (encrypted using the server's public key) and by clients to verify their identity to a server when the server requests a client certificate.</span></span> <span data-ttu-id="1c3ae-1367">Bu API 'ye özel anahtar eklemek, ilişkili sertifikayı bir TLS uygulaması için kimlik sertifikası olarak otomatik olarak işaretler.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1367">Adding a private key with this API will automatically mark the associated certificate as being an identity certificate for a TLS application.</span></span> <span data-ttu-id="1c3ae-1368">Sertifikaları diğer amaçlar için başlatırken (örn. güvenilen mağaza), *private_key_data* parametresi null, 0 olarak *private_key_data_length* ve *private_key_type* NX_SECURE_X509_KEY_TYPE_NONE olarak geçirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1368">When initializing certificates for other purposes (e.g. the trusted store), the *private_key_data* parameter should be passed as NULL, the *private_key_data_length* as 0, and the *private_key_type* should be passed as NX_SECURE_X509_KEY_TYPE_NONE.</span></span>

<span data-ttu-id="1c3ae-1369">*Private_key_type* parametresi, özel anahtarın biçimlendirmesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1369">The *private_key_type* parameter indicates the formatting of the private key.</span></span> <span data-ttu-id="1c3ae-1370">Örneğin, özel anahtar DER ile kodlanmış PKCS#1 biçimli bir RSA özel anahtarı ise, netx secure olarak bilinen bir tür olan private_key_type, hemen ayrıştıracak ve daha sonra kullanmak üzere kaydedecek olan NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER olarak geçirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1370">For example, if the private key is a DER-encoded PKCS#1-format RSA private key, the private_key_type should be passed as NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER, a type known to NetX Secure which will be parsed immediately and saved for later use.</span></span>

<span data-ttu-id="1c3ae-1371">Bu private_key_type, belirli anahtar biçimlerine veya diğer ihtiyaçlarına sahip platformlar ve uygulamalar için kullanıcı tanımlı anahtar türleri<sup>23'ü</sup> de destekler.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1371">The private_key_type also supports user-defined key types<sup>23</sup> for platforms and applications that have specific key formats or other needs.</span></span> <span data-ttu-id="1c3ae-1372">Örneğin, donanım tabanlı bir şifreleme altyapısı NetX Secure yazılımı tarafından anlaşılmayan belirli bir biçim kullanabilir veya bir özel anahtar şifrelenir veya bir şifreleme belirteci ile temsil edilir. Bu durum Güvenilir Platform Modülü (TPM) veya PKCS#11 şifreleme donanımıyla da olabilir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1372">For example, a hardware-based encryption engine may use a specific format not understood by the NetX Secure software, or a private key may be encrypted or represented by a cryptographic token as might be the case with a Trusted Platform Module (TPM) or PKCS#11 cryptographic hardware.</span></span> <span data-ttu-id="1c3ae-1373">Kullanıcı tanımlı bir anahtar türü kullanılırken, anahtar verileri uygun şifreleme yordamına tam olarak geçirılır. Örneğin, herhangi bir ayrıştırma veya işleme olmadan doğrudan şifreleme tablosunda TLS'ye sağlanan RSA şifreleme yordamına bir RSA özel anahtarı geçirilebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1373">When a user-defined key type is used, the key data is passed verbatim to the appropriate cryptographic routine - for example, an RSA private key would be passed, without any parsing or processing, directly to the RSA cryptographic routine provided to TLS in the ciphersuite table.</span></span> <span data-ttu-id="1c3ae-1374">Kullanıcı tanımlı anahtar türü de şifreleme yordamına geçirildi (RSA söz konusu ise bu "op" parametresidir).</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1374">The user-defined key type is also passed to the cryptographic routine (in the case of RSA, this is the "op" parameter).</span></span>

<span data-ttu-id="1c3ae-1375">Kullanıcı tanımlı anahtar aralığı, 0000-0xFFFF FFFF aralığından 32 bitlik bir imzasız tamsayının üst 0x0001 kapsar.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1375">The range of user-defined keys covers the top half of a 32-bit unsigned integer, from 0x0001 0000-0xFFFF FFFF.</span></span> <span data-ttu-id="1c3ae-1376">0000'0x0001 küçük değerler NetX Secure kullanımı için ayrılmıştır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1376">Values less than 0x0001 0000 are reserved for NetX Secure use.</span></span>

<span data-ttu-id="1c3ae-1377">Kullanıcı tanımlı anahtar türleri, ham özel anahtar verilerini işlemek için özel şifreleme yordamları gerektiren gelişmiş bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1377">User-defined key types are an advanced feature that requires custom cryptographic routines to handle the raw private key data.</span></span> <span data-ttu-id="1c3ae-1378">Bu özel şeye ihtiyacınız varsa lütfen Express Logic temsilcinize başvurun.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1378">Please contact your Express Logic representative if you have need of this feature.</span></span>

### <a name="parameters"></a><span data-ttu-id="1c3ae-1379">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1379">Parameters</span></span>

- <span data-ttu-id="1c3ae-1380">**certificate_ptr** Uninitialized X.509 Sertifika örneğinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1380">**certificate_ptr** Pointer to an uninitialized X.509 Certificate instance.</span></span>
- <span data-ttu-id="1c3ae-1381">**certificate_data** DER ile kodlanmış X.509 ikili verileri işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1381">**certificate_data** Pointer to DER-encoded X.509 binary data.</span></span>
- <span data-ttu-id="1c3ae-1382">**raw_data_buffer** İsteğe bağlı ayrılmış sertifika veri arabelleği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1382">**raw_data_buffer** Pointer to optional dedicated certificate data buffer.</span></span>
- <span data-ttu-id="1c3ae-1383">**buffer_size** İsteğe bağlı ayrılmış sertifika veri arabelleğinin boyutu.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1383">**buffer_size** Size of optional dedicated certificate data buffer.</span></span>
- <span data-ttu-id="1c3ae-1384">**certificate_data_length** Sertifika ikili verilerinin bayt cinsinden uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1384">**certificate_data_length** Length of certificate binary data in bytes.</span></span>
- <span data-ttu-id="1c3ae-1385">**private_key_data** İsteğe bağlı özel anahtar verilerine işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1385">**private_key_data** Pointer to optional private key data.</span></span>
- <span data-ttu-id="1c3ae-1386">**private_key_data_length** Özel anahtar verisi uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1386">**private_key_data_length** Length of private key data.</span></span>
- <span data-ttu-id="1c3ae-1387">**private_key_type** Anahtar türü tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1387">**private_key_type** Key type identifier.</span></span>

### <a name="return-values"></a><span data-ttu-id="1c3ae-1388">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1388">Return Values</span></span>

- <span data-ttu-id="1c3ae-1389">Sertifikanın başarılı bir şekilde eklenmesi **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1389">**NX_SUCCESS** (0x00) Successful addition of certificate.</span></span>
- <span data-ttu-id="1c3ae-1390">**NX_PTR_ERROR** (0x07) geçersiz bir Işaretçi kullanmaya çalıştı.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1390">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>
- <span data-ttu-id="1c3ae-1391">**NX_SECURE_TLS_INVALID_CERTIFICATE** (0x112) SERTIFIKA verileri der-Encoded X. 509.952 sertifikası içermiyordu.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1391">**NX_SECURE_TLS_INVALID_CERTIFICATE** (0x112) Certificate data did not contain a DER-encoded X.509 certificate.</span></span>
- <span data-ttu-id="1c3ae-1392">**NX_SECURE_TLS_UNSUPPORTED_PUBLIC_CIPHER** (0x10d) sertifikada NETX güvenli tarafından desteklenen bir ortak anahtar şifresi yoktu.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1392">**NX_SECURE_TLS_UNSUPPORTED_PUBLIC_CIPHER** (0x10D) Certificate did not have a public-key cipher that is supported by NetX Secure.</span></span>
- <span data-ttu-id="1c3ae-1393">**NX_SECURE_X509_INVALID_CERTIFICATE_SEQUENCE** (0x186) özel anahtar veya sertifika GEÇERLI bir ASN. 1 sırası içermiyordu.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1393">**NX_SECURE_X509_INVALID_CERTIFICATE_SEQUENCE** (0x186) Private key or certificate did not contain a valid ASN.1 sequence.</span></span>
- <span data-ttu-id="1c3ae-1394">**NX_SECURE_PKCS1_INVALID_PRIVATE_KEY** (0x18a) belirtilen özel anahtar GEÇERLI bir PKCS # 1 RSA anahtarı değildi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1394">**NX_SECURE_PKCS1_INVALID_PRIVATE_KEY** (0x18A) The provided private key was not a valid PKCS#1 RSA key.</span></span>
- <span data-ttu-id="1c3ae-1395">**NX_SECURE_X509_INVALID_PRIVATE_KEY_TYPE** (0x19d) belirtilen özel anahtar türü kullanıcı tanımlı değildi ve bilinen hiçbir türle eşleşmedi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1395">**NX_SECURE_X509_INVALID_PRIVATE_KEY_TYPE** (0x19D) The private key type provided was not user-defined and did not match any known type.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1c3ae-1396">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1396">Allowed From</span></span>

<span data-ttu-id="1c3ae-1397">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1397">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1c3ae-1398">Örnek</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1398">Example</span></span>

```C
/* Initialize certificate structure. The certificate structure will point directly
   into the certificate_data array since we are passing the raw_data_buffer as
   NX_NULL. This certificate has a private key so it will be used to identify this
   device. */
status =  nx_secure_x509_certificate_initialize(&certificate, certificate_data,
500, NX_NULL, 0, private_key, 64, NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);


/* If status is NX_SUCCESS the certificate was successfully initialized.  */
```

### <a name="see-also"></a><span data-ttu-id="1c3ae-1399">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1399">See Also</span></span>

- <span data-ttu-id="1c3ae-1400">nx_secure_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1400">nx_secure_local_certificate_add</span></span>
- <span data-ttu-id="1c3ae-1401">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1401">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="1c3ae-1402">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1402">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="1c3ae-1403">Bölüm 3 ' te X. 509.440 sertifikalarını NetX güvenli olarak içeri aktarma.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1403">Importing X.509 Certificates into NetX Secure in Chapter 3.</span></span>

## <a name="nx_secure_x509_common_name_dns_check"></a><span data-ttu-id="1c3ae-1404">nx_secure_x509_common_name_dns_check</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1404">nx_secure_x509_common_name_dns_check</span></span>

<span data-ttu-id="1c3ae-1405">X. 509.440 sertifikasıyla DNS adını denetle</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1405">Check DNS name against X.509 Certificate</span></span>

### <a name="prototype"></a><span data-ttu-id="1c3ae-1406">Prototype</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1406">Prototype</span></span>

```C
UINT  nx_secure_x509_common_name_dns_check(
                        NX_SECURE_X509_CERT *certificate,
                        const UCHAR *dns_tld, UINT dns_tld_length);
```

### <a name="description"></a><span data-ttu-id="1c3ae-1407">Description</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1407">Description</span></span>

<span data-ttu-id="1c3ae-1408">Bu hizmet, uzak bir ana bilgisayarın DNS doğrulaması amacıyla arayan tarafından belirtilen bir üst etki alanı adına (TLD) karşı bir sertifikanın ortak adını denetler.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1408">This service checks a certificate's Common Name against a Top- Domain name (TLD) provided by the caller for the purposes of DNS validation of a remote host.</span></span> <span data-ttu-id="1c3ae-1409">Bu yardımcı program işlevi, uygulama tarafından verilen bir sertifika doğrulama geri çağırma yordamının içinden çağrılması amaçlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1409">This utility function is intended to be called from within a certificate validation callback routine provided by the application.</span></span> <span data-ttu-id="1c3ae-1410">TLD adı, uzak ana bilgisayara erişmek için kullanılan URL 'nin en üst bölümü olmalıdır ("." ilk eğik çizgiden önce ayrılmış dize).</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1410">The TLD name should be the top part of the URL used to access the remote host (the "."-separated string before the first slash).</span></span> <span data-ttu-id="1c3ae-1411">Ortak ad bir joker karakter (örn *. example.com) içeriyorsa, joker karakter aynı soneke sahip herhangi biriyle eşleşir. Joker karakter eşleştirmesi için yalnızca ilk joker ("*") ile karşılaşılan (sağdan sola okuma) değerlendirildiğini unutmayın; Örneğin, ABC. \*. example. com, ". example.com" ile biten *Tüm* ad ile eşleşir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1411">If the Common Name contains a wildcard (such as *.example.com), the wildcard will match any with the same suffix. Note that only the first wildcard ("*") encountered (reading right-to-left) will be considered for wildcard matching – for example, abc.\*.example.com will match *any* name ending in ".example.com".</span></span>

<span data-ttu-id="1c3ae-1412">Ortak ad, belirtilen dizeyle eşleşmezse, "subjectAltName" uzantısı ayrıştırılır (sertifikada varsa) ve herhangi bir DNSName girdisi de karşılaştırılır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1412">If the Common Name does not match the provided string, the "subjectAltName" extension is parsed (if it exists in the certificate) and any DNSName entries are also compared.</span></span> <span data-ttu-id="1c3ae-1413">Bu girdilerden hiçbiri eşleşmezse bir hata döndürülür.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1413">If none of those entries match, an error is returned.</span></span>

<span data-ttu-id="1c3ae-1414">Beklenen sertifikalarda ortak adın (ve subjectAltName girdilerinin) biçimini anlamak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1414">It is important to understand the format of the common name (and subjectAltName entries) in expected certificates.</span></span> <span data-ttu-id="1c3ae-1415">Örneğin, bazı sertifikalar ham IP adresi veya joker karakter kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1415">For example, some certificates may use a raw IP address or a wild card.</span></span> <span data-ttu-id="1c3ae-1416">DNS TLD dizesi, alınan sertifikalarda beklenen değerlerle eş olacak şekilde biçimlendirildi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1416">The DNS TLD string must be formatted such that it will match the expected values in received certificates.</span></span>

### <a name="parameters"></a><span data-ttu-id="1c3ae-1417">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1417">Parameters</span></span>

- <span data-ttu-id="1c3ae-1418">**certificate_ptr** X.509 Sertifika örneğinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1418">**certificate_ptr** Pointer to an X.509 Certificate instance.</span></span>
- <span data-ttu-id="1c3ae-1419">**dns_tld** Top-Level etki alanı adını seçin.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1419">**dns_tld** Top-Level Domain name to compare against.</span></span>
- <span data-ttu-id="1c3ae-1420">**dns_tld_length** TLD dizesinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1420">**dns_tld_length** Length of TLD string.</span></span>

### <a name="return-values"></a><span data-ttu-id="1c3ae-1421">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1421">Return Values</span></span>

- <span data-ttu-id="1c3ae-1422">**NX_SUCCESS** (0x00) Ortak Ad veya subjectAltName ile başarılı karşılaştırma.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1422">**NX_SUCCESS** (0x00) Successful comparison with Common Name or subjectAltName.</span></span>
- <span data-ttu-id="1c3ae-1423">**NX_SECURE_X509_CERTIFICATE_DNS_MISMATCH** (0x195) Eşleşen ad bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1423">**NX_SECURE_X509_CERTIFICATE_DNS_MISMATCH** (0x195) No matching name found.</span></span>
- <span data-ttu-id="1c3ae-1424">**NX_PTR_ERROR** (0x07) Geçersiz bir işaretçi kullanmayı denedi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1424">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1c3ae-1425">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1425">Allowed From</span></span>

<span data-ttu-id="1c3ae-1426">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1426">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1c3ae-1427">Örnek</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1427">Example</span></span>

```C
/* Callback routine used to perform additional checks on a certificate. */
ULONG certificate_callback(NX_SECURE_TLS_SESSION *session, NX_SECURE_X509_CERT
*certificate)
{
ULONG status;
UCHAR *tld = “www.example.com”;

    /* Check our DNS TLD against the certificate provided by the
       remote TLS host. */
    status = nx_secure_x509_common_name_dns_check(certificate, tld, strlen(tld));

        if(status != NX_SUCCESS)
        {
            /* TLD did not match any names in the certificate. */
            return(status);
        }

        /* DNS validation and any other checks were successful. */
        return(NX_SUCCESS);
}

…

/* Add callback to TLS session in TLS setup routine.  */
status =  nx_secure_tls_session_certificate_callback_set(&tls_session,
                                                         certificate_callback);
```

### <a name="see-also"></a><span data-ttu-id="1c3ae-1428">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1428">See Also</span></span>

- <span data-ttu-id="1c3ae-1429">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1429">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="1c3ae-1430">nx_secure_tls_session_certificate_callback_set</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1430">nx_secure_tls_session_certificate_callback_set</span></span>
- <span data-ttu-id="1c3ae-1431">nx_secure_x509_crl_revocation_check</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1431">nx_secure_x509_crl_revocation_check</span></span>

## <a name="nx_secure_x509_crl_revocation_check"></a><span data-ttu-id="1c3ae-1432">nx_secure_x509_crl_revocation_check</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1432">nx_secure_x509_crl_revocation_check</span></span>

<span data-ttu-id="1c3ae-1433">Sağlanan bir Sertifika İptal Listesi (CRL) için X.509 Sertifikasını denetleme</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1433">Check X.509 Certificate against a supplied Certificate Revocation List (CRL)</span></span>

### <a name="prototype"></a><span data-ttu-id="1c3ae-1434">Prototype</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1434">Prototype</span></span>

```C
UINT  nx_secure_x509_crl_revocation_check(const UCHAR *crl_data,
                              UINT crl_length,
                              NX_SECURE_X509_CERTIFICATE_STORE *store,
                              NX_SECURE_X509_CERT *certificate);
```

### <a name="description"></a><span data-ttu-id="1c3ae-1435">Description</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1435">Description</span></span>

<span data-ttu-id="1c3ae-1436">Bu hizmet DER kodlanmış Sertifika İptal Listesi alır ve bu listede belirli bir sertifikayı arar.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1436">This service takes a DER-encoded Certificate Revocation List and searches for a specific certificate in that list.</span></span> <span data-ttu-id="1c3ae-1437">CRL'nin sertifikayı teslim alan kişi, sağlanan bir sertifika deposuna göre doğrulanır, CRL'nin sertifikayı teslim alanla aynı olduğu doğrulanır ve iptal edilen sertifika listesinde arama yapmak için söz konusu sertifikanın seri numarası kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1437">The issuer of the CRL is validated against a supplied certificate store, the CRL issuer is validated to be the same as the one for the certificate being checked, and the serial number of the certificate in question is used to search the revoked certificates list.</span></span> <span data-ttu-id="1c3ae-1438">Sertifikayı alanlar eşlenirse, imza  onaylar ve sertifika listede yoksa, çağrı başarılı olur.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1438">If the issuers match, the signature checks out, and the certificate is **not** present in the list, the call is successful.</span></span> <span data-ttu-id="1c3ae-1439">Diğer tüm durumlar bir hatanın döndürül yollarına neden olur.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1439">All other cases cause an error to be returned.</span></span>

### <a name="parameters"></a><span data-ttu-id="1c3ae-1440">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1440">Parameters</span></span>

- <span data-ttu-id="1c3ae-1441">**crl_data** DER ile kodlanmış CRL'nin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1441">**crl_data** Pointer to a DER-encoded CRL.</span></span>
- <span data-ttu-id="1c3ae-1442">**crl_length** CRL verilerinin bayt cinsinden uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1442">**crl_length** Length in bytes of CRL data.</span></span>
- <span data-ttu-id="1c3ae-1443">**Mağaza** X. 509.440 sertifika deposuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1443">**store** Pointer to an X.509 Certificate store.</span></span>
- <span data-ttu-id="1c3ae-1444">**certificate_ptr** X. 509.440 sertifika örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1444">**certificate_ptr** Pointer to an X.509 Certificate instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="1c3ae-1445">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1445">Return Values</span></span>

- <span data-ttu-id="1c3ae-1446">**NX_SUCCESS** (0x00) sertifikanın iptal edilmediğini doğrulama başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1446">**NX_SUCCESS** (0x00) Successful validation that the certificate was not revoked.</span></span>
- <span data-ttu-id="1c3ae-1447">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) CRL veren sertifikası bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1447">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) CRL issuer certificate not found.</span></span>
- <span data-ttu-id="1c3ae-1448">**NX_SECURE_TLS_ISSUER_CERTIFICATE_NOT_FOUND** 0x11b) sertifika veren sertifikası bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1448">**NX_SECURE_TLS_ISSUER_CERTIFICATE_NOT_FOUND** 0x11B) Certificate issuer certificate not found.</span></span>
- <span data-ttu-id="1c3ae-1449">**NX_SECURE_X509_ASN1_LENGTH_TOO_LONG** (0x182) CRL ASN. 1, geçersiz bir uzunluk alanı içeriyordu.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1449">**NX_SECURE_X509_ASN1_LENGTH_TOO_LONG** (0x182) The CRL ASN.1 contained an invalid length field.</span></span>
- <span data-ttu-id="1c3ae-1450">**NX_SECURE_X509_UNEXPECTED_ASN1_TAG (0x189)** CRL geçersiz ASN. 1 içeriyordu.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1450">**NX_SECURE_X509_UNEXPECTED_ASN1_TAG(0x189)** The CRL contained invalid ASN.1.</span></span>
- <span data-ttu-id="1c3ae-1451">**NX_SECURE_X509_CHAIN_VERIFY_FAILURE** (0x18C) bir sertifika zinciri doğrulaması başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1451">**NX_SECURE_X509_CHAIN_VERIFY_FAILURE** (0x18C) A certificate chain verification failed.</span></span>
- <span data-ttu-id="1c3ae-1452">**NX_SECURE_X509_CRL_ISSUER_MISMATCH** (0x197) CRL ve sertifika verenler eşleşmedi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1452">**NX_SECURE_X509_CRL_ISSUER_MISMATCH** (0x197) CRL and certificate issuers did not match.</span></span>
- <span data-ttu-id="1c3ae-1453">**NX_SECURE_X509_CRL_SIGNATURE_CHECK_FAILED** 0x198) CRL imzası geçersizdi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1453">**NX_SECURE_X509_CRL_SIGNATURE_CHECK_FAILED** 0x198) The CRL signature was invalid.</span></span>
- <span data-ttu-id="1c3ae-1454">**NX_SECURE_X509_CRL_CERTIFICATE_REVOKED** (0x199) denetlenen sertifika CRL 'de bulundu ve bu nedenle iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1454">**NX_SECURE_X509_CRL_CERTIFICATE_REVOKED** (0x199) The certificate being checked was found in the CRL and is therefore revoked.</span></span>
- <span data-ttu-id="1c3ae-1455">**NX_PTR_ERROR** (0x07) geçersiz bir Işaretçi kullanmaya çalıştı.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1455">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1c3ae-1456">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1456">Allowed From</span></span>

<span data-ttu-id="1c3ae-1457">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1457">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1c3ae-1458">Örnek</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1458">Example</span></span>

```C
/* CRL obtained for the expected certificate issuer through some means (downloaded
   from server manually, obtained from CRL endpoint, etc…) */
const UCHAR *crl_data;
UINT crl_length = 300;

/* Callback routine used to perform additional checks on a certificate. */
ULONG certificate_callback(NX_SECURE_TLS_SESSION *session, NX_SECURE_X509_CERT
*certificate)
{
ULONG status;
NX_SECURE_X509_CERTIFICATE_STORE *store;

    /* Obtain a certificate store to check against. In the certificate callback,
       it usually makes the most sense to use the store associated with the TLS
       session. */
    store = &session -> nx_secure_tls_credentials.nx_secure_tls_certificate_store;

    /* Check our certificate against the CRL and TLS certificate store. */
    status = nx_secure_x509_crl_revocation_check(crl, crl_length, store,
                                                 certificate);

        if(status != NX_SUCCESS)
        {
            if(status == NX_SECURE_X509_CRL_CERTIFICATE_REVOKED)
            {
                /* Certificate was revoked. */
               return(status);
            }
            else
            {
               /* CRL was invalid or some other issue. In this case the certificate
                  may still be valid since the CRL itself was a problem. At this
                  point it is up to the application to decide whether to continue
                  with the TLS handshake. For this example, assume certificate is
                  valid (faulty CRL is a possible Denial-of-Service attack).*/
               status = NX_SUCCESS;
        }

    /* Other certificate checking can go here. */

    /* Return status of certificate checks. */
    return(status);
}

…

/* Add callback to TLS session in TLS setup routine.  */
status =  nx_secure_tls_session_certificate_callback_set(&tls_session,
                                                         certificate_callback);
```

### <a name="see-also"></a><span data-ttu-id="1c3ae-1459">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1459">See Also</span></span>

- <span data-ttu-id="1c3ae-1460">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1460">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="1c3ae-1461">nx_secure_tls_session_certificate_callback_set</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1461">nx_secure_tls_session_certificate_callback_set</span></span>
- <span data-ttu-id="1c3ae-1462">nx_secure_x509_common_name_dns_check</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1462">nx_secure_x509_common_name_dns_check</span></span>

## <a name="nx_secure_x509_dns_name_initialize"></a><span data-ttu-id="1c3ae-1463">nx_secure_x509_dns_name_initialize</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1463">nx_secure_x509_dns_name_initialize</span></span>

<span data-ttu-id="1c3ae-1464">X. 509.440 DNS adı yapısını başlatma</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1464">Initialize an X.509 DNS name structure</span></span>

### <a name="prototype"></a><span data-ttu-id="1c3ae-1465">Prototype</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1465">Prototype</span></span>

```C
UINT  nx_secure_x509_dns_name_initialize(
                        NX_SECURE_X509_DNS_NAME *dns_name,
                        const UCHAR *name_string, UINT length);
```

### <a name="description"></a><span data-ttu-id="1c3ae-1466">Description</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1466">Description</span></span>

<span data-ttu-id="1c3ae-1467">Bu hizmet belirli bir ad biçimi gerektiren belirli API hizmetleriyle kullanılmak üzere bir X. 509.440 DNS adı başlatır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1467">This service initializes an X.509 DNS name for use with certain API services requiring a specific name format.</span></span> <span data-ttu-id="1c3ae-1468">Örneğin, *nx_secure_tls_sni_extension_parse* hizmeti, TLS el sıkışması sırasında NX_SECURE_X509_DNS_NAME uzantısında uzak bir ana bilgisayar tarafından sağlanan adla eşleşmesi için Sunucu Adı Belirtme nesnesi bekler.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1468">For example, the *nx_secure_tls_sni_extension_parse* service expects an NX_SECURE_X509_DNS_NAME object in order to match the name provided by a remote host in the Server Name Indication extension during the TLS handshake.</span></span> <span data-ttu-id="1c3ae-1469">DNS adı yalnızca uzunluğu olan bir karakter dizesidir. Bir DNS adının izin verilen en uzun uzunluğu (ve NX_SECURE_X509_DNS_NAME'daki iç arabelleğin boyutu) makro NX_SECURE_X509_DNS_NAME_MAX (varsayılan 100 bayt) tarafından denetlenmektedir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1469">A DNS name is simply a charater string with a length – the maximum allowed length of a DNS name (and the size of the internal buffer in NX_SECURE_X509_DNS_NAME) is controlled by the macro NX_SECURE_X509_DNS_NAME_MAX (default 100 bytes).</span></span>

### <a name="parameters"></a><span data-ttu-id="1c3ae-1470">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1470">Parameters</span></span>

- <span data-ttu-id="1c3ae-1471">**dns_name** Başlat için DNS ad yapısı.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1471">**dns_name** DNS name structure to initialize.</span></span>
- <span data-ttu-id="1c3ae-1472">**name_string** DNS ad dizesi verileri.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1472">**name_string** DNS name string data.</span></span>
- <span data-ttu-id="1c3ae-1473">**uzunluk** Ad dizesinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1473">**length** Length of name string.</span></span>

### <a name="return-values"></a><span data-ttu-id="1c3ae-1474">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1474">Return Values</span></span>

- <span data-ttu-id="1c3ae-1475">**NX_SUCCESS** (0x00) Başarılı başlatma.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1475">**NX_SUCCESS** (0x00) Successful initialization.</span></span>
- <span data-ttu-id="1c3ae-1476">**NX_SECURE_X509_NAME_STRING_TOO_LONG** (0x19E) Verilen ad dizesi NX_SECURE_X509_DNS_NAME_MAX.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1476">**NX_SECURE_X509_NAME_STRING_TOO_LONG** (0x19E) The given name string exceeded NX_SECURE_X509_DNS_NAME_MAX.</span></span>
- <span data-ttu-id="1c3ae-1477">**NX_PTR_ERROR** (0x07) Geçersiz bir işaretçi kullanmayı denedi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1477">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1c3ae-1478">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1478">Allowed From</span></span>

<span data-ttu-id="1c3ae-1479">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1479">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1c3ae-1480">Örnek</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1480">Example</span></span>

```C
NX_SECURE_X509_DNS_NAME dns_name;

/* Initialize DNS name. */
status = nx_secure_x509_dns_name_initialize(&dns_name, “www.example.com”,
                                            strlen(“www.example.com”);

/* Use initialized DNS name to send the Server Name Indication extension to the
   remote TLS server. */
status = nx_secure_tls_session_sni_extension_set(&tls_session, &dns_name);
```

### <a name="see-also"></a><span data-ttu-id="1c3ae-1481">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1481">See Also</span></span>

- <span data-ttu-id="1c3ae-1482">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1482">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="1c3ae-1483">nx_secure_tls_session_sni_extension_parse</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1483">nx_secure_tls_session_sni_extension_parse</span></span>
- <span data-ttu-id="1c3ae-1484">nx_secure_tls_session_sni_extension_set</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1484">nx_secure_tls_session_sni_extension_set</span></span>

## <a name="nx_secure_x509_extended_key_usage_extension_parse"></a><span data-ttu-id="1c3ae-1485">nx_secure_x509_extended_key_usage_extension_parse</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1485">nx_secure_x509_extended_key_usage_extension_parse</span></span>

<span data-ttu-id="1c3ae-1486">X.509 sertifikasında X.509 genişletilmiş anahtar kullanımı uzantısını bulma ve ayrıştırma</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1486">Find and parse an X.509 extended key usage extension in an X.509 certificate</span></span>

### <a name="prototype"></a><span data-ttu-id="1c3ae-1487">Prototype</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1487">Prototype</span></span>

```C
UINT  nx_secure_x509_extended_key_usage_extension_parse(
                        NX_SECURE_X509_CERT *certificate,
                        UINT key_usage);
```

### <a name="description"></a><span data-ttu-id="1c3ae-1488">Description</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1488">Description</span></span>

<span data-ttu-id="1c3ae-1489">Bu hizmetin bir sertifika doğrulama geri çağırma içinde çağrılma amacı vardır (bkz. *nx_secure_tls_session_certificate_callback_set).*</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1489">This service is intended to be called from within a certificate verification callback (see *nx_secure_tls_session_certificate_callback_set)*.</span></span> <span data-ttu-id="1c3ae-1490">Bir X.509 sertifikası içinde belirli bir genişletilmiş anahtar kullanımı OID'sını aratır ve OID'nin mevcut olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1490">It will search for a specific extended key usage OID within an X.509 certificate and return whether the OID is present.</span></span> <span data-ttu-id="1c3ae-1491">key_usage parametresi, değişken uzunluklu OID dizelerini parametre olarak geçirmemek için NetX Secure X.509 ve TLS tarafından dahili olarak kullanılan OID'lere bir tamsayı eşlemesidir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1491">The key_usage parameter is an integer mapping of the OIDs which is used internally by NetX Secure X.509 and TLS to avoid passing the variable-length OID strings as parameters.</span></span>

<span data-ttu-id="1c3ae-1492">Genişletilmiş anahtar kullanım uzantısı için ilgili OID'ler aşağıdaki tabloda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1492">The relevant OIDs for the extended key usage extension are given in the table below.</span></span> <span data-ttu-id="1c3ae-1493">Alınan bir TLS sunucu sertifikasında genişletilmiş anahtar kullanımını kontrol etmek isteyen tipik bir TLS İstemcisi uygulaması, uzantı mevcutsa ancak OID mevcutsa NX_SECURE_TLS_X509_TYPE_PKIX_KP_SERVER_AUTH, sertifikanın ana bilgisayarı TLS sunucusu olarak tanımlay için geçersiz olarak kabul edilir ve sertifika doğrulama geri çağırma bir hata döndürür.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1493">A typical TLS Client implementation wishing to check extended key usage in a received TLS server certificate would check for the existence of the OID NX_SECURE_TLS_X509_TYPE_PKIX_KP_SERVER_AUTH – if the extension is present but that OID is not, then the certificate would be considered invalid for identifiying the host as a TLS server and the certificate verification callback should return an error.</span></span> <span data-ttu-id="1c3ae-1494">Uzantının kendisi eksikse, TLS el sıkışması ile devam edilip edilmeyeceğini uygulamaya göre yapılır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1494">If the extension itself is missing, then it is up to the application whether or not to proceed with the TLS handshake.</span></span>

<span data-ttu-id="1c3ae-1495">Sertifika doğrulama geri çağrısında hata dönüş kodu NX_SECURE_X509_KEY_USAGE_ERROR, uygulama kullanımı için ayrılmıştır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1495">In the certificate verification callback, the error return code NX_SECURE_X509_KEY_USAGE_ERROR is reserved for application use.</span></span> <span data-ttu-id="1c3ae-1496">Anahtar kullanımını denetlerken bir hata oluşursa, hatanın nedenini göstermek için bu değer geri aramadan döndürülür.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1496">If there is an error in checking key usage, this value may be returned from the callback to indicate the reason for failure.</span></span>

| <span data-ttu-id="1c3ae-1497">NetX güvenli tanımlayıcısı</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1497">NetX Secure Identifier</span></span>                                | <span data-ttu-id="1c3ae-1498">OID değeri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1498">OID Value</span></span>         | <span data-ttu-id="1c3ae-1499">Description</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1499">Description</span></span>                                      |
| --------------------------------------------------------- | --------------------- | ---------------------------------------------------- |
| <span data-ttu-id="1c3ae-1500">NX_SECURE_TLS_X509_TYPE_PKIX_KP_SERVER_AUTH</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1500">NX_SECURE_TLS_X509_TYPE_PKIX_KP_SERVER_AUTH</span></span>   | <span data-ttu-id="1c3ae-1501">1.3.6.1.5.5.7.3.1</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1501">1.3.6.1.5.5.7.3.1</span></span> | <span data-ttu-id="1c3ae-1502">Sertifika, bir TLS sunucusunu tanımlamak için kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1502">Certificate can be used to identify a TLS server</span></span> |
| <span data-ttu-id="1c3ae-1503">NX_SECURE_TLS_X509_TYPE_PKIX_KP_CLIENT_AUTH</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1503">NX_SECURE_TLS_X509_TYPE_PKIX_KP_CLIENT_AUTH</span></span>   | <span data-ttu-id="1c3ae-1504">1.3.6.1.5.5.7.3.2</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1504">1.3.6.1.5.5.7.3.2</span></span> | <span data-ttu-id="1c3ae-1505">Sertifika, bir TLS istemcisini tanımlamak için kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1505">Certificate can be used to identify a TLS client</span></span> |
| <span data-ttu-id="1c3ae-1506">NX_SECURE_TLS_X509_TYPE_PKIX_KP_CODE_SIGNING</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1506">NX_SECURE_TLS_X509_TYPE_PKIX_KP_CODE_SIGNING</span></span>  | <span data-ttu-id="1c3ae-1507">1.3.6.1.5.5.7.3.3</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1507">1.3.6.1.5.5.7.3.3</span></span> | <span data-ttu-id="1c3ae-1508">Sertifika, kodu imzalamak için kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1508">Certificate can be used to sign code</span></span>             |
| <span data-ttu-id="1c3ae-1509">NX_SECURE_TLS_X509_TYPE_PKIX_KP_EMAIL_PROTECT</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1509">NX_SECURE_TLS_X509_TYPE_PKIX_KP_EMAIL_PROTECT</span></span> | <span data-ttu-id="1c3ae-1510">1.3.6.1.5.5.7.3.4</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1510">1.3.6.1.5.5.7.3.4</span></span> | <span data-ttu-id="1c3ae-1511">Sertifika, e-postaları imzalamak için kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1511">Certificate can be used to sign emails</span></span>           |
| <span data-ttu-id="1c3ae-1512">NX_SECURE_TLS_X509_TYPE_PKIX_KP_TIME_STAMPING</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1512">NX_SECURE_TLS_X509_TYPE_PKIX_KP_TIME_STAMPING</span></span> | <span data-ttu-id="1c3ae-1513">1.3.6.1.5.5.7.3.8</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1513">1.3.6.1.5.5.7.3.8</span></span> | <span data-ttu-id="1c3ae-1514">Sertifika, zaman damgalarını imzalamak için kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1514">Certificate can be used to sign timestamps</span></span>       |
| <span data-ttu-id="1c3ae-1515">NX_SECURE_TLS_X509_TYPE_PKIX_KP_OCSP_SIGNING</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1515">NX_SECURE_TLS_X509_TYPE_PKIX_KP_OCSP_SIGNING</span></span>  | <span data-ttu-id="1c3ae-1516">1.3.6.1.5.5.7.3.9</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1516">1.3.6.1.5.5.7.3.9</span></span> | <span data-ttu-id="1c3ae-1517">OCSP yanıtlarını imzalamak için sertifika kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1517">Certificate can be used to sign OCSP responses</span></span>   |

<span data-ttu-id="1c3ae-1518">X.509 Genişletilmiş Anahtar Kullanımı Uzantısı için OID'ler ve eşlemeler</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1518">OIDs and mappings for X.509 Extended Key Usage Extension</span></span>

### <a name="parameters"></a><span data-ttu-id="1c3ae-1519">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1519">Parameters</span></span>

- <span data-ttu-id="1c3ae-1520">**sertifika** Doğrulanan sertifikanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1520">**certificate** Pointer to certificate being verified.</span></span>
- <span data-ttu-id="1c3ae-1521">**key_usage** Yukarıdaki tablodan OID tamsayı eşlemesi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1521">**key_usage** OID integer mapping from table above.</span></span>

### <a name="return-values"></a><span data-ttu-id="1c3ae-1522">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1522">Return Values</span></span>

- <span data-ttu-id="1c3ae-1523">**NX_SUCCESS** (0x00) Belirtilen anahtar kullanımı OID bulundu.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1523">**NX_SUCCESS** (0x00) Specified key usage OID found.</span></span>
- <span data-ttu-id="1c3ae-1524">**NX_SECURE_X509_MULTIBYTE_TAG_UNSUPPORTED** (0x181) ASN.1 çoklu bayt etiketiyle karşılaşıldı (desteklenmeyen sertifika).</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1524">**NX_SECURE_X509_MULTIBYTE_TAG_UNSUPPORTED** (0x181) ASN.1 multi-byte tag encountered (unsupported certificate).</span></span>
- <span data-ttu-id="1c3ae-1525">**NX_SECURE_X509_ASN1_LENGTH_TOO_LONG** (0x182) Invaild ASN.1 alanıyla karşılaşıldı (geçersiz sertifika).</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1525">**NX_SECURE_X509_ASN1_LENGTH_TOO_LONG** (0x182) Invaild ASN.1 field encountered (invalid certificate).</span></span>
- <span data-ttu-id="1c3ae-1526">**NX_SECURE_X509_INVALID_TAG_CLASS** (0x190) Geçersiz ASN.1 etiket sınıfıyla karşılaşıldı (geçersiz sertifika).</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1526">**NX_SECURE_X509_INVALID_TAG_CLASS** (0x190) Invalid ASN.1 tag class encountered (invalid certificate).</span></span>
- <span data-ttu-id="1c3ae-1527">**NX_SECURE_X509_INVALID_EXTENSION_SEQUENCE** (0x192) Geçersiz uzantıyla karşılaşıldı (geçersiz sertifika).</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1527">**NX_SECURE_X509_INVALID_EXTENSION_SEQUENCE** (0x192) Invalid extension encountered (invalid certificate).</span></span>
- <span data-ttu-id="1c3ae-1528">**NX_SECURE_X509_EXTENSION_NOT_FOUND** (0x19B) Genişletilmiş Anahtar Kullanımı uzantısı sağlanan sertifikada bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1528">**NX_SECURE_X509_EXTENSION_NOT_FOUND** (0x19B) The Extended Key Usage extension was not found in the provided certificate.</span></span>
- <span data-ttu-id="1c3ae-1529">**NX_PTR_ERROR** (0x07) Geçersiz sertifika işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1529">**NX_PTR_ERROR** (0x07) Invalid certificate pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1c3ae-1530">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1530">Allowed From</span></span>

<span data-ttu-id="1c3ae-1531">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1531">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1c3ae-1532">Örnek</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1532">Example</span></span>

```C
ULONG certificate_verification_callback(NX_SECURE_TLS_SESSION *session, NX_SECURE_X509_CERT* certificate)
{
UINT status;

    /* Extended key usage - look for specific OIDs. */
    status = nx_secure_x509_extended_key_usage_extension_parse(certificate,
                        NX_SECURE_TLS_X509_TYPE_PKIX_KP_SERVER_AUTH);

    if(status != NX_SUCCESS)
    {
        if(NX_SECURE_X509_EXT_KEY_USAGE_NOT_FOUND)
        {
            printf("Extended key usage extension not found or specified key usage OID not
                    provided in extension.\n");
            /* The certificate was valid but the specified OID was not found. The
               application can decide whether to continue or abort the TLS handshake. */
            return(NX_SECURE_X509_KEY_USAGE_ERROR);
        }
        else
        {
            /* The extension or certificate was invalid. */
            return(status);
        }
    }

    /* The specified OID was found, return success! */
    return(NX_SUCCESS);
}
```

### <a name="see-also"></a><span data-ttu-id="1c3ae-1533">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1533">See Also</span></span>

- <span data-ttu-id="1c3ae-1534">nx_secure_tls_session_certificate_callback_set</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1534">nx_secure_tls_session_certificate_callback_set</span></span>
- <span data-ttu-id="1c3ae-1535">nx_secure_x509_key_usage_extension_parse</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1535">nx_secure_x509_key_usage_extension_parse</span></span>
- <span data-ttu-id="1c3ae-1536">nx_secure_x509_crl_revocation_check</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1536">nx_secure_x509_crl_revocation_check</span></span>
- <span data-ttu-id="1c3ae-1537">nx_secure_x509_common_name_dns_check</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1537">nx_secure_x509_common_name_dns_check</span></span>
- <span data-ttu-id="1c3ae-1538">nx_secure_x509_extension_find</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1538">nx_secure_x509_extension_find</span></span>

## <a name="nx_secure_x509_extension_find"></a><span data-ttu-id="1c3ae-1539">nx_secure_x509_extension_find</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1539">nx_secure_x509_extension_find</span></span>

<span data-ttu-id="1c3ae-1540">X. 509.440 sertifikasında bir X. 509.440 uzantısı bulun ve döndürün</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1540">Find and return an X.509 extension in an X.509 certificate</span></span>

### <a name="prototype"></a><span data-ttu-id="1c3ae-1541">Prototype</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1541">Prototype</span></span>

```C
UINT  nx_secure_x509_extension_find(
                        NX_SECURE_X509_CERT *certificate,
                        NX_SECURE_X509_EXTENSION *extension,
                        USHORT extension_id);
```

### <a name="description"></a><span data-ttu-id="1c3ae-1542">Description</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1542">Description</span></span>

<span data-ttu-id="1c3ae-1543">Bu hizmetin bir sertifika doğrulama geri çağırması içinden çağrılması amaçlanmıştır (bkz. *nx_secure_tls_session_certificate_callback_set)* ve gelişmiş bir X. 509.440 hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1543">This service is intended to be called from within a certificate verification callback (see *nx_secure_tls_session_certificate_callback_set)* and is an advanced X.509 service.</span></span>

<span data-ttu-id="1c3ae-1544">İşlevi, bir OID 'ye dayalı bir X. 509.440 sertifikası içindeki belirli bir uzantıyı arar ve OID 'nin mevcut ham uzantı verilerine yönelik başvuruları içeren bir yapıyla birlikte, OID 'nin var olup olmadığını döndürür.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1544">The function will search for a specific extension within an X.509 certificate based on an OID and return whether the OID is present, along with a structure containing references to the relevant raw extension data.</span></span> <span data-ttu-id="1c3ae-1545">Extension_id parametresi, değişken uzunluklu OID dizelerinin parametre olarak geçirilmesini önlemek için NetX güvenli X. 509.440 ve TLS tarafından dahili olarak kullanılan OID 'lerin bir tamsayı eşlemesidir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1545">The extension_id parameter is an integer mapping of the OIDs which is used internally by NetX Secure X.509 and TLS to avoid passing the variable-length OID strings as parameters.</span></span>

<span data-ttu-id="1c3ae-1546">Belirli Uzantılar için belirtilen yardımcı işlevler ( *nx_secure_x509_key_usage_extension_parse*) çağrısı, dahili olarak uzantı verilerini almak için nx_secure_x509_extension_find.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1546">The helper functions provided for specific extensions (such as *nx_secure_x509_key_usage_extension_parse*) call nx_secure_x509_extension_find internally to obtain the extension data.</span></span>

<span data-ttu-id="1c3ae-1547">Bilinen X. 509.440 uzantıları için ilgili OID 'ler aşağıdaki tabloda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1547">The relevant OIDs for known X.509 extensions are given in the table below.</span></span>

<span data-ttu-id="1c3ae-1548">NX_SECURE_X509_EXTENSION yapısı, X. 509.952 sertifikasına, *nx_secure_x509_key_usage_extension_parse* gibi yardımcı işlevlere, ham uzantının der kodlu ASN. 1 verilerini hızlıca çözmesini sağlayan işaretçiler içerir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1548">The NX_SECURE_X509_EXTENSION structure contains pointers into the X.509 certificate that allow helper functions such as *nx_secure_x509_key_usage_extension_parse* to quickly decode the raw extension DER-encoded ASN.1 data.</span></span>

<span data-ttu-id="1c3ae-1549">Belirli uzantılar hakkında daha fazla bilgi için bkz. RFC 5280 (X. 509.440 belirtimi) veya varsa uygun yardımcı işlevleri başvurusu.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1549">For information on specific extensions, see RFC 5280 (X.509 specification) or the reference for the appropriate helper functions if available.</span></span>

<span data-ttu-id="1c3ae-1550">NetX Secure X. 509.440 sürümünün geçerli sürümü, X. 509.440 uzantıları için sınırlı desteğe sahip.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1550">The current version of NetX Secure X.509 has limited support for X.509 extensions.</span></span> <span data-ttu-id="1c3ae-1551">Daha sonra daha fazla yardımcı işlev eklenecektir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1551">More helper functions will be added in the future.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1c3ae-1552">*Bu hizmet, X. 509.440 uzantılarına ve DER kodlu ASN. 1 ' i bilen kullanıcılara yönelik gelişmiş bir özelliktir. Bu kullanıcıların, NetX Secure X. 509.952 'in Şu anda yardımcı işlevler sağlamayan uzantılara erişmesini sağlamak için sağlanmıştır. Yardımcı işlevleri olmayan bu uzantılar için ham DER kodlu ASN. 1 ' i kendiniz ayrıştırmanıza gerek olacaktır.*</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1552">*This service is an advanced feature for users familiar with X.509 extensions and DER-encoded ASN.1. It is provided to enable those users to access extensions for which NetX Secure X.509 does not currently provide helper functions. For those extensions without helper functions, you will have to parse the raw DER-encoded ASN.1 yourself.*</span></span>

| <span data-ttu-id="1c3ae-1553">NetX güvenli tanımlayıcısı</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1553">NetX Secure Identifier</span></span>                              | <span data-ttu-id="1c3ae-1554">OID değeri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1554">OID Value</span></span> | <span data-ttu-id="1c3ae-1555">Description</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1555">Description</span></span>                                                                    | <span data-ttu-id="1c3ae-1556">Yardımcı işlevi?</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1556">Helper function?</span></span> |
| ------------------------------------------------------- | ------------- | ---------------------------------------------------------------------------------- | -------------------- |
| <span data-ttu-id="1c3ae-1557">NX_SECURE_TLS_X509_TYPE_DIRECTORY_ATTRIBUTES</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1557">NX_SECURE_TLS_X509_TYPE_DIRECTORY_ATTRIBUTES</span></span>  | <span data-ttu-id="1c3ae-1558">2.5.29.9</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1558">2.5.29.9</span></span>  | <span data-ttu-id="1c3ae-1559">Dizin öznitelikleri – sertifika konusu hakkında temel bilgi öznitelikleri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1559">Directory Attributes – basic information attributes about certificate subject</span></span>  | <span data-ttu-id="1c3ae-1560">No</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1560">No</span></span>               |
| <span data-ttu-id="1c3ae-1561">NX_SECURE_TLS_X509_TYPE_SUBJECT_KEY_ID</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1561">NX_SECURE_TLS_X509_TYPE_SUBJECT_KEY_ID</span></span>       | <span data-ttu-id="1c3ae-1562">2.5.29.14</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1562">2.5.29.14</span></span> | <span data-ttu-id="1c3ae-1563">Belirli bir ortak anahtarı tanımlamak için kullanılır</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1563">Used to identify a specific public key</span></span>                                         | <span data-ttu-id="1c3ae-1564">No</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1564">No</span></span>               |
| <span data-ttu-id="1c3ae-1565">NX_SECURE_TLS_X509_TYPE_KEY_USAGE</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1565">NX_SECURE_TLS_X509_TYPE_KEY_USAGE</span></span>             | <span data-ttu-id="1c3ae-1566">2.5.29.15</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1566">2.5.29.15</span></span> | <span data-ttu-id="1c3ae-1567">Sertifika ortak anahtarı için geçerli kullanımlar hakkında bilgi sağlar</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1567">Provides information on valid uses for the certificate public key</span></span>              | <span data-ttu-id="1c3ae-1568">Yes</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1568">Yes</span></span>              |
| <span data-ttu-id="1c3ae-1569">NX_SECURE_TLS_X509_TYPE_SUBJECT_ALT_NAME</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1569">NX_SECURE_TLS_X509_TYPE_SUBJECT_ALT_NAME</span></span>     | <span data-ttu-id="1c3ae-1570">2.5.29.17</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1570">2.5.29.17</span></span> | <span data-ttu-id="1c3ae-1571">Sertifikayı tanımlamak için alternatif DNS adları sağlar</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1571">Provides alternative DNS names to identify the certificate</span></span>                     | <span data-ttu-id="1c3ae-1572">Evet<sup>24</sup></span><span class="sxs-lookup"><span data-stu-id="1c3ae-1572">Yes<sup>24</sup></span></span>        |
| <span data-ttu-id="1c3ae-1573">NX_SECURE_TLS_X509_TYPE_ISSUER_ALT_NAME</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1573">NX_SECURE_TLS_X509_TYPE_ISSUER_ALT_NAME</span></span>      | <span data-ttu-id="1c3ae-1574">2.5.29.18</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1574">2.5.29.18</span></span> | <span data-ttu-id="1c3ae-1575">Sertifikayı vereni tanımlamak için alternatif DNS adları sağlar</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1575">Provides alternative DNS names to identify the certificate's issuer</span></span>            | <span data-ttu-id="1c3ae-1576">No</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1576">No</span></span>               |
| <span data-ttu-id="1c3ae-1577">NX_SECURE_TLS_X509_TYPE_BASIC_CONSTRAINTS</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1577">NX_SECURE_TLS_X509_TYPE_BASIC_CONSTRAINTS</span></span>     | <span data-ttu-id="1c3ae-1578">2.5.29.19</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1578">2.5.29.19</span></span> | <span data-ttu-id="1c3ae-1579">Temel sertifika kullanım kısıtlaması bilgilerini sağlar</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1579">Provides basic certificate usage constraint information</span></span>                        | <span data-ttu-id="1c3ae-1580">No</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1580">No</span></span>               |
| <span data-ttu-id="1c3ae-1581">NX_SECURE_TLS_X509_TYPE_NAME_CONSTRAINTS</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1581">NX_SECURE_TLS_X509_TYPE_NAME_CONSTRAINTS</span></span>      | <span data-ttu-id="1c3ae-1582">2.5.29.30</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1582">2.5.29.30</span></span> | <span data-ttu-id="1c3ae-1583">Sertifika adlarını belirli etki alanlarıyla sınırlamak için kullanılır</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1583">Used to constrain certificate names to specific domains</span></span>                        | <span data-ttu-id="1c3ae-1584">No</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1584">No</span></span>               |
| <span data-ttu-id="1c3ae-1585">NX_SECURE_TLS_X509_TYPE_CRL_DISTRIBUTION</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1585">NX_SECURE_TLS_X509_TYPE_CRL_DISTRIBUTION</span></span>      | <span data-ttu-id="1c3ae-1586">2.5.29.31</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1586">2.5.29.31</span></span> | <span data-ttu-id="1c3ae-1587">CRL dağıtımı için URL'ler sağlar</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1587">Provides URIs for CRL distribution</span></span>                                             | <span data-ttu-id="1c3ae-1588">No</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1588">No</span></span>               |
| <span data-ttu-id="1c3ae-1589">NX_SECURE_TLS_X509_TYPE_CERTIFICATE_POLICIES</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1589">NX_SECURE_TLS_X509_TYPE_CERTIFICATE_POLICIES</span></span>  | <span data-ttu-id="1c3ae-1590">2.5.29.32</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1590">2.5.29.32</span></span> | <span data-ttu-id="1c3ae-1591">Büyük PKI sistemleri için sertifika ilkeleri listesi</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1591">List of certificate policies for large PKI systems</span></span>                             | <span data-ttu-id="1c3ae-1592">No</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1592">No</span></span>               |
| <span data-ttu-id="1c3ae-1593">NX_SECURE_TLS_X509_TYPE_CERT_POLICY_MAPPINGS</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1593">NX_SECURE_TLS_X509_TYPE_CERT_POLICY_MAPPINGS</span></span> | <span data-ttu-id="1c3ae-1594">2.5.29.33</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1594">2.5.29.33</span></span> | <span data-ttu-id="1c3ae-1595">CA sertifika ilkelerinin listesi</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1595">List of CA certificate policies</span></span>                                                | <span data-ttu-id="1c3ae-1596">No</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1596">No</span></span>               |
| <span data-ttu-id="1c3ae-1597">NX_SECURE_TLS_X509_TYPE_AUTHORITY_KEY_ID</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1597">NX_SECURE_TLS_X509_TYPE_AUTHORITY_KEY_ID</span></span>     | <span data-ttu-id="1c3ae-1598">2.5.29.35</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1598">2.5.29.35</span></span> | <span data-ttu-id="1c3ae-1599">Bir sertifika imzasıyla ilişkili belirli bir ortak anahtarı tanımlamak için kullanılır</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1599">Used to identify a specific public key associated with a certificate signature</span></span> | <span data-ttu-id="1c3ae-1600">No</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1600">No</span></span>               |
| <span data-ttu-id="1c3ae-1601">NX_SECURE_TLS_X509_TYPE_POLICY_CONSTRAINTS</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1601">NX_SECURE_TLS_X509_TYPE_POLICY_CONSTRAINTS</span></span>    | <span data-ttu-id="1c3ae-1602">2.5.29.36</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1602">2.5.29.36</span></span> | <span data-ttu-id="1c3ae-1603">CA ilkesi kısıtlamaları</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1603">CA policy constraints</span></span>                                                          | <span data-ttu-id="1c3ae-1604">No</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1604">No</span></span>               |
| <span data-ttu-id="1c3ae-1605">NX_SECURE_TLS_X509_TYPE_EXTENDED_KEY_USAGE</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1605">NX_SECURE_TLS_X509_TYPE_EXTENDED_KEY_USAGE</span></span>   | <span data-ttu-id="1c3ae-1606">2.5.29.37</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1606">2.5.29.37</span></span> | <span data-ttu-id="1c3ae-1607">Ek OID tabanlı anahtar kullanımı bilgileri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1607">Additional OID-based key usage information</span></span>                                     | <span data-ttu-id="1c3ae-1608">Yes</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1608">Yes</span></span>              |
| <span data-ttu-id="1c3ae-1609">NX_SECURE_TLS_X509_TYPE_FRESHEST_CRL</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1609">NX_SECURE_TLS_X509_TYPE_FRESHEST_CRL</span></span>          | <span data-ttu-id="1c3ae-1610">2.5.29.46</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1610">2.5.29.46</span></span> | <span data-ttu-id="1c3ae-1611">Delta CRL 'Leri alma hakkında bilgi sağlar</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1611">Provides information for obtaining delta CRLs</span></span>                                  | <span data-ttu-id="1c3ae-1612">No</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1612">No</span></span>               |
| <span data-ttu-id="1c3ae-1613">NX_SECURE_TLS_X509_TYPE_INHIBIT_ANYPOLICY</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1613">NX_SECURE_TLS_X509_TYPE_INHIBIT_ANYPOLICY</span></span>     | <span data-ttu-id="1c3ae-1614">2.5.29.54</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1614">2.5.29.54</span></span> | <span data-ttu-id="1c3ae-1615">AnyPolicy 'in kullanılamayacağını gösteren CA sertifikası alanı</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1615">CA certificate field indicating that AnyPolicy cannot be used</span></span>                  | <span data-ttu-id="1c3ae-1616">No</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1616">No</span></span>               |

<span data-ttu-id="1c3ae-1617">X.509 Uzantıları için OID'ler ve eşlemeler</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1617">OIDs and mappings for X.509 Extensions</span></span>

24. <span data-ttu-id="1c3ae-1618">SubjectAltName uzantısı, hizmet hizmet denetiminde DNS adı denetimi kapsamında ayrıştır nx_secure_x509_common_name_dns_check.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1618">The SubjectAltName extension is parsed as part of the DNS name check in the service nx_secure_x509_common_name_dns_check.</span></span>

### <a name="parameters"></a><span data-ttu-id="1c3ae-1619">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1619">Parameters</span></span>

- <span data-ttu-id="1c3ae-1620">**sertifika** Doğrulanan sertifikanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1620">**certificate** Pointer to certificate being verified.</span></span>
- <span data-ttu-id="1c3ae-1621">**uzantı** Uzantı veri işaretçisi ve uzunluğu içeren dönüş yapısı.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1621">**extension** Return structure containing extension data pointer and length.</span></span>
- <span data-ttu-id="1c3ae-1622">**extension_id** Yukarıdaki tablodan OID tamsayı eşlemesi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1622">**extension_id** OID integer mapping from table above.</span></span>

### <a name="return-values"></a><span data-ttu-id="1c3ae-1623">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1623">Return Values</span></span>

- <span data-ttu-id="1c3ae-1624">**NX_SUCCESS** (0x00) Belirtilen uzantı OID bulundu ve veriler döndürüldü.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1624">**NX_SUCCESS** (0x00) Specified extension OID found and data returned.</span></span>
- <span data-ttu-id="1c3ae-1625">**NX_SECURE_X509_MULTIBYTE_TAG_UNSUPPORTED** (0x181) ASN.1 çoklu bayt etiketiyle karşılaşıldı (desteklenmeyen sertifika).</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1625">**NX_SECURE_X509_MULTIBYTE_TAG_UNSUPPORTED** (0x181) ASN.1 multi-byte tag encountered (unsupported certificate).</span></span>
- <span data-ttu-id="1c3ae-1626">**NX_SECURE_X509_ASN1_LENGTH_TOO_LONG** (0x182) Invaild ASN.1 alanıyla karşılaşıldı (geçersiz sertifika).</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1626">**NX_SECURE_X509_ASN1_LENGTH_TOO_LONG** (0x182) Invaild ASN.1 field encountered (invalid certificate).</span></span>
- <span data-ttu-id="1c3ae-1627">**NX_SECURE_X509_INVALID_TAG_CLASS** (0x190) Geçersiz ASN.1 etiket sınıfıyla karşılaşıldı (geçersiz sertifika).</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1627">**NX_SECURE_X509_INVALID_TAG_CLASS** (0x190) Invalid ASN.1 tag class encountered (invalid certificate).</span></span>
- <span data-ttu-id="1c3ae-1628">**NX_SECURE_X509_INVALID_EXTENSION_SEQUENCE** (0x192) Geçersiz uzantıyla karşılaşıldı</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1628">**NX_SECURE_X509_INVALID_EXTENSION_SEQUENCE** (0x192) Invalid extension encountered</span></span>
- <span data-ttu-id="1c3ae-1629">**NX_SECURE_X509_EXTENSION_NOT_FOUND** (0x19B) Verilen uzantı OID'i sağlanan sertifikada bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1629">**NX_SECURE_X509_EXTENSION_NOT_FOUND** (0x19B) The given extension OID was not found in the provided certificate.</span></span>
- <span data-ttu-id="1c3ae-1630">**NX_PTR_ERROR** (0x07) Geçersiz sertifika veya uzantı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1630">**NX_PTR_ERROR** (0x07) Invalid certificate or extension pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1c3ae-1631">İzin Verilen</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1631">Allowed From</span></span>

<span data-ttu-id="1c3ae-1632">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1632">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1c3ae-1633">Örnek</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1633">Example</span></span>

```C
/* Function to parse a Basic Constraints X.509 extension. */
UINT _basic_constraints_extension_parse(NX_SECURE_X509_CERT *certificate)
{
const UCHAR             *current_buffer;
ULONG                    length;
UINT                     status;
NX_SECURE_X509_EXTENSION extension_data;

    /* Find the Basic Constraints extension in the certificate. */
    status = _nx_secure_x509_extension_find(certificate, &extension_data,
                              NX_SECURE_TLS_X509_TYPE_BASIC_CONSTRAINTS);

    /* See if extension present - it might be OK if not present! */
    if (status != NX_SUCCESS)
    {
        return(status);
    }

    /* The extension_data structure now points to the raw extension ASN.1
      (DER-encoded). */
    current_buffer = extension_data.nx_secure_x509_extension_data;
    length = extension_data.nx_secure_x509_extension_data_length;

   /* Extension ASN.1 parsing… */

   return(NX_SUCCESS);
}
```

### <a name="see-also"></a><span data-ttu-id="1c3ae-1634">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1634">See Also</span></span>

- <span data-ttu-id="1c3ae-1635">nx_secure_tls_session_certificate_callback_set</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1635">nx_secure_tls_session_certificate_callback_set</span></span>
- <span data-ttu-id="1c3ae-1636">nx_secure_x509_key_usage_extension_parse</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1636">nx_secure_x509_key_usage_extension_parse</span></span>
- <span data-ttu-id="1c3ae-1637">nx_secure_x509_crl_revocation_check</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1637">nx_secure_x509_crl_revocation_check</span></span>
- <span data-ttu-id="1c3ae-1638">nx_secure_x509_common_name_dns_check</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1638">nx_secure_x509_common_name_dns_check</span></span>
- <span data-ttu-id="1c3ae-1639">nx_secure_x509_extended_key_usage_extension_parse</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1639">nx_secure_x509_extended_key_usage_extension_parse</span></span>

## <a name="nx_secure_x509_key_usage_extension_parse"></a><span data-ttu-id="1c3ae-1640">nx_secure_x509_key_usage_extension_parse</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1640">nx_secure_x509_key_usage_extension_parse</span></span>

<span data-ttu-id="1c3ae-1641">X.509 sertifikasında X.509 Anahtar Kullanımı uzantısını bulma ve ayrıştırma</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1641">Find and parse an X.509 Key Usage extension in an X.509 certificate</span></span>

### <a name="prototype"></a><span data-ttu-id="1c3ae-1642">Prototype</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1642">Prototype</span></span>

```C
UINT  nx_secure_x509_key_usage_extension_parse(
                        NX_SECURE_X509_CERT *certificate,
                        USHORT *bitfield);
```

### <a name="description"></a><span data-ttu-id="1c3ae-1643">Description</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1643">Description</span></span>

<span data-ttu-id="1c3ae-1644">Bu hizmetin bir sertifika doğrulama geri çağırması içinden çağrılması amaçlanmıştır (bkz. *nx_secure_tls_session_certificate_callback_set)*.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1644">This service is intended to be called from within a certificate verification callback (see *nx_secure_tls_session_certificate_callback_set)*.</span></span> <span data-ttu-id="1c3ae-1645">Anahtar kullanımı uzantısını arar ve bulunursa "bit alanından" parametresindeki anahtar kullanımı bitalanını döndürür.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1645">It will search for the Key Usage extension and if found, will return the Key Usage bitfield in the "bitfield" parameter.</span></span>

<span data-ttu-id="1c3ae-1646">X. 509.440 belirtimi (RFC 5280) tarafından tanımlanan bitler aşağıdaki tabloda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1646">The bits, as defined by the X.509 specification (RFC 5280) are given in the table below.</span></span> <span data-ttu-id="1c3ae-1647">Bit düzeyinde AND ve uygun bit maskesi (sıfır olmayan), her bitin değerini verir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1647">A bitwise AND with the appropriate bitmask (and checking for non-zero) will give the value of each bit.</span></span>

<span data-ttu-id="1c3ae-1648">Bit alanından 'ın der-Encoding değeri, diğer sıfırları ortadan kaldırdığına göre, ham sertifika verilerinde bitlerin gerçek konumunun kodu çözülmüş bit alanından ' daki konumlarından farklı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1648">Note that the DER-encoding of the bitfield eliminates extra zeroes so the actual position of the bits in the raw certificate data will likely be different from their positions in the decoded bitfield.</span></span> <span data-ttu-id="1c3ae-1649">Sağlanan bit maskeleri, ham der kodlu sertifika verileriyle değil, yalnızca *nx_secure_x509_key_usage_extension_parse* tarafından döndürülen kodu çözülmüş bit alanından üzerinde kullanılmak üzere tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1649">The supplied bitmasks are only intended to be used on the decoded bitfield returned by *nx_secure_x509_key_usage_extension_parse* and not with the raw DER-encoded certificate data.</span></span>

<span data-ttu-id="1c3ae-1650">Sertifika doğrulama geri çağrısında hata dönüş kodu NX_SECURE_X509_KEY_USAGE_ERROR, uygulama kullanımı için ayrılmıştır.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1650">In the certificate verification callback, the error return code NX_SECURE_X509_KEY_USAGE_ERROR is reserved for application use.</span></span> <span data-ttu-id="1c3ae-1651">Anahtar kullanımını denetlerken bir hata oluşursa, hatanın nedenini göstermek için bu değer geri aramadan döndürülür.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1651">If there is an error in checking key usage, this value may be returned from the callback to indicate the reason for failure.</span></span>

| <span data-ttu-id="1c3ae-1652">NetX güvenli tanımlayıcısı</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1652">NetX Secure Identifier</span></span>                            | <span data-ttu-id="1c3ae-1653">Bit konumu</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1653">Bit position</span></span> | <span data-ttu-id="1c3ae-1654">Description</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1654">Description</span></span>                                                                                                                                                  |
| ----------------------------------------------------- | ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <span data-ttu-id="1c3ae-1655">NX_SECURE_X509_KEY_USAGE_DIGITAL_SIGNATURE</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1655">NX_SECURE_X509_KEY_USAGE_DIGITAL_SIGNATURE</span></span>  | <span data-ttu-id="1c3ae-1656">0</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1656">0</span></span>            | <span data-ttu-id="1c3ae-1657">Sertifika, dijital imzalar için kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1657">Certificate can be used for digital signatures</span></span>                                                                                                               |
| <span data-ttu-id="1c3ae-1658">NX_SECURE_X509_KEY_USAGE_NON_REPUDIATION</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1658">NX_SECURE_X509_KEY_USAGE_NON_REPUDIATION</span></span>    | <span data-ttu-id="1c3ae-1659">1</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1659">1</span></span>            | <span data-ttu-id="1c3ae-1660">Sertifika, sertifikalar ve CRL 'Ler dışında dijital imzaları doğrulamak için kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1660">Certificate can be used to verify digital signatures other than those for certificates and CRLs</span></span>                                                              |
| <span data-ttu-id="1c3ae-1661">NX_SECURE_X509_KEY_USAGE_KEY_ENCIPHERMENT</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1661">NX_SECURE_X509_KEY_USAGE_KEY_ENCIPHERMENT</span></span>   | <span data-ttu-id="1c3ae-1662">2</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1662">2</span></span>            | <span data-ttu-id="1c3ae-1663">Sertifika, simetrik anahtarları şifrelemek için kullanılabilir (anahtar aktarımı)</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1663">Certificate can be used to encrypt symmetric keys (key transport)</span></span>                                                                                            |
| <span data-ttu-id="1c3ae-1664">NX_SECURE_X509_KEY_USAGE_DATA_ENCIPHERMENT</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1664">NX_SECURE_X509_KEY_USAGE_DATA_ENCIPHERMENT</span></span>  | <span data-ttu-id="1c3ae-1665">3</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1665">3</span></span>            | <span data-ttu-id="1c3ae-1666">Sertifika, ham Kullanıcı verilerini doğrudan şifrelemek için kullanılabilir (seyrek)</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1666">Certificate can be used to directly encrypt raw user data (uncommon)</span></span>                                                                                         |
| <span data-ttu-id="1c3ae-1667">NX_SECURE_X509_KEY_USAGE_KEY_AGREEMENT</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1667">NX_SECURE_X509_KEY_USAGE_KEY_AGREEMENT</span></span>      | <span data-ttu-id="1c3ae-1668">4</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1668">4</span></span>            | <span data-ttu-id="1c3ae-1669">Sertifika, anahtar anlaşması için kullanılabilir (Diffie-Hellman ' de olduğu gibi)</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1669">Certificate can be used for key agreement (as with Diffie-Hellman)</span></span>                                                                                           |
| <span data-ttu-id="1c3ae-1670">NX_SECURE_X509_KEY_USAGE_KEY_CERT_SIGN</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1670">NX_SECURE_X509_KEY_USAGE_KEY_CERT_SIGN</span></span>     | <span data-ttu-id="1c3ae-1671">5</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1671">5</span></span>            | <span data-ttu-id="1c3ae-1672">Sertifika, diğer sertifikaları imzalamak ve doğrulamak için kullanılabilir (sertifika bir CA veya ICA sertifikasıdır).</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1672">Certificate can be used to sign and verify other certificates (the certificate is a CA or ICA certificate).</span></span>                                                  |
| <span data-ttu-id="1c3ae-1673">NX_SECURE_X509_KEY_USAGE_CRL_SIGN</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1673">NX_SECURE_X509_KEY_USAGE_CRL_SIGN</span></span>           | <span data-ttu-id="1c3ae-1674">6</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1674">6</span></span>            | <span data-ttu-id="1c3ae-1675">CRL'lerde imzaları doğrulamak için sertifika ortak anahtarı kullanılır</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1675">Certificate public key is used to verify signatures on CRLs</span></span>                                                                                                  |
| <span data-ttu-id="1c3ae-1676">NX_SECURE_X509_KEY_USAGE_ENCIPHER_ONLY</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1676">NX_SECURE_X509_KEY_USAGE_ENCIPHER_ONLY</span></span>      | <span data-ttu-id="1c3ae-1677">7</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1677">7</span></span>            | <span data-ttu-id="1c3ae-1678">Anahtar Sözleşmesi biti (bit 4) ile kullanılır– ayar olduğunda, sertifika anahtarı yalnızca anahtar sözleşmesi sırasında şifrelemek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1678">Used with Key Agreement bit (bit 4) – when set, certificate key can only be used to encrypt during key agreement.</span></span> <span data-ttu-id="1c3ae-1679">Anahtar Sözleşmesi biti ayarlanmamışsa tanımsız.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1679">Undefined if Key Agreement bit is not set.</span></span> |
| <span data-ttu-id="1c3ae-1680">NX_SECURE_X509_KEY_USAGE_DECIPHER_ONLY</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1680">NX_SECURE_X509_KEY_USAGE_DECIPHER_ONLY</span></span>      | <span data-ttu-id="1c3ae-1681">8</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1681">8</span></span>            | <span data-ttu-id="1c3ae-1682">Anahtar Sözleşmesi biti (bit 4) ile kullanılır– ayar olduğunda, sertifika anahtarı yalnızca anahtar sözleşmesi sırasında şifresini çözmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1682">Used with Key Agreement bit (bit 4) – when set, certificate key can only be used to decrypt during key agreement.</span></span> <span data-ttu-id="1c3ae-1683">Anahtar Sözleşmesi biti ayarlanmamışsa tanımsız.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1683">Undefined if Key Agreement bit is not set.</span></span> |

<span data-ttu-id="1c3ae-1684">X.509 Anahtar Kullanımı Uzantısı için Bit maskeleri ve değerleri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1684">Bitmasks and values for X.509 Key Usage Extension</span></span>

### <a name="parameters"></a><span data-ttu-id="1c3ae-1685">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1685">Parameters</span></span>

- <span data-ttu-id="1c3ae-1686">**sertifika** Doğrulanan sertifikanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1686">**certificate** Pointer to certificate being verified.</span></span>
- <span data-ttu-id="1c3ae-1687">**bitfield** Uzantıdan bitfield'in tamamını iade.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1687">**bitfield** Return the entire bitfield from the extension.</span></span>

### <a name="return-values"></a><span data-ttu-id="1c3ae-1688">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1688">Return Values</span></span>

- <span data-ttu-id="1c3ae-1689">**NX_SUCCESS** (0x00) Anahtar kullanım uzantısı bulundu ve bitfield döndürüldü.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1689">**NX_SUCCESS** (0x00) Key usage extension found and bitfield returned.</span></span>
- <span data-ttu-id="1c3ae-1690">**NX_SECURE_X509_MULTIBYTE_TAG_UNSUPPORTED** (0x181) ASN.1 çoklu bayt etiketiyle karşılaşıldı (desteklenmeyen sertifika).</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1690">**NX_SECURE_X509_MULTIBYTE_TAG_UNSUPPORTED** (0x181) ASN.1 multi-byte tag encountered (unsupported certificate).</span></span>
- <span data-ttu-id="1c3ae-1691">**NX_SECURE_X509_ASN1_LENGTH_TOO_LONG** (0x182) Invaild ASN.1 alanıyla karşılaşıldı (geçersiz sertifika).</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1691">**NX_SECURE_X509_ASN1_LENGTH_TOO_LONG** (0x182) Invaild ASN.1 field encountered (invalid certificate).</span></span>
- <span data-ttu-id="1c3ae-1692">**NX_SECURE_X509_INVALID_TAG_CLASS** (0x190) Geçersiz ASN.1 etiket sınıfıyla karşılaşıldı (geçersiz sertifika).</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1692">**NX_SECURE_X509_INVALID_TAG_CLASS** (0x190) Invalid ASN.1 tag class encountered (invalid certificate).</span></span>
- <span data-ttu-id="1c3ae-1693">**NX_SECURE_X509_INVALID_EXTENSION_SEQUENCE** (0x192) Geçersiz uzantıyla karşılaşıldı (geçersiz sertifika).</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1693">**NX_SECURE_X509_INVALID_EXTENSION_SEQUENCE** (0x192) Invalid extension encountered (invalid certificate).</span></span>
- <span data-ttu-id="1c3ae-1694">**NX_SECURE_X509_EXTENSION_NOT_FOUND** (0x19B)Anahtar Kullanımı uzantısı sağlanan sertifikada bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1694">**NX_SECURE_X509_EXTENSION_NOT_FOUND** (0x19B)The Key Usage extension was not found in the provided certificate.</span></span>
- <span data-ttu-id="1c3ae-1695">**NX_PTR_ERROR** (0x07) Geçersiz sertifika veya bitfield işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1695">**NX_PTR_ERROR** (0x07) Invalid certificate or bitfield pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1c3ae-1696">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1696">Allowed From</span></span>

<span data-ttu-id="1c3ae-1697">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1697">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1c3ae-1698">Örnek</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1698">Example</span></span>

```C
ULONG certificate_verification_callback(NX_SECURE_TLS_SESSION *session,
  NX_SECURE_X509_CERT* certificate)
{
UINT status;
USHORT key_usage_bitfield;

    /* Key usage – extract key usage bitfield. */
    status = nx_secure_x509_key_usage_extension_parse(certificate, &key_usage_bitfield);

   /* Check certificate for a few specific key usage bits. */
   if((key_usage_bitfield & NX_SECURE_X509_KEY_USAGE_DIGITAL_SIGNATURE) == 0 ||
      (key_usage_bitfield & NX_SECURE_X509_KEY_USAGE_NON_REPUDIATION)   == 0 ||
      (key_usage_bitfield & NX_SECURE_X509_KEY_USAGE_KEY_ENCIPHERMENT)  == 0)
    {
        printf("Expected key usage bitfield bits not set!\n");
        return(NX_SECURE_X509_KEY_USAGE_ERROR);
    }

    /* The specified bits were set, return success! */
    return(NX_SUCCESS);
}
```

### <a name="see-also"></a><span data-ttu-id="1c3ae-1699">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1699">See Also</span></span>

- <span data-ttu-id="1c3ae-1700">nx_secure_tls_session_certificate_callback_set</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1700">nx_secure_tls_session_certificate_callback_set</span></span>
- <span data-ttu-id="1c3ae-1701">nx_secure_x509_extended_key_usage_extension_parse</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1701">nx_secure_x509_extended_key_usage_extension_parse</span></span>
- <span data-ttu-id="1c3ae-1702">nx_secure_x509_crl_revocation_check</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1702">nx_secure_x509_crl_revocation_check</span></span>
- <span data-ttu-id="1c3ae-1703">nx_secure_x509_common_name_dns_check</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1703">nx_secure_x509_common_name_dns_check</span></span>
- <span data-ttu-id="1c3ae-1704">nx_secure_x509_extension_find</span><span class="sxs-lookup"><span data-stu-id="1c3ae-1704">nx_secure_x509_extension_find</span></span>
