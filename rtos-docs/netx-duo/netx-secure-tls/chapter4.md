---
title: Bölüm 4-Azure RTOS NetX güvenli hizmetlerinin açıklaması
description: Bu bölüm, tüm NetX güvenli hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 89761ec3438b1b16c1a603764bf7d4e1eac1b4ea
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826950"
---
# <a name="chapter-4---description-of-azure-rtos-netx-secure-services"></a><span data-ttu-id="ee161-103">Bölüm 4-Azure RTOS NetX güvenli hizmetlerinin açıklaması</span><span class="sxs-lookup"><span data-stu-id="ee161-103">Chapter 4 - Description of Azure RTOS NetX Secure services</span></span>

<span data-ttu-id="ee161-104">Bu bölüm, tüm Azure RTOS NetX güvenli hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="ee161-104">This chapter contains a description of all Azure RTOS NetX Secure services (listed below) in alphabetic order.</span></span>

<span data-ttu-id="ee161-105">Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_SECURE_DISABLE_ERROR_CHECKING** makrodan etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="ee161-105">In the "Return Values" section in the following API descriptions, values in **BOLD** are not affected by the **NX_SECURE_DISABLE_ERROR_CHECKING** macro that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

- [<span data-ttu-id="ee161-106">nx_secure_crypto_table_self_test</span><span class="sxs-lookup"><span data-stu-id="ee161-106">nx_secure_crypto_table_self_test</span></span>](#nx_secure_crypto_table_self_test)
  - <span data-ttu-id="ee161-107">Şifreleme yöntemlerinde self_test gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="ee161-107">Perform self_test on the crypto methods</span></span>
- [<span data-ttu-id="ee161-108">nx_secure_module_hash_compute</span><span class="sxs-lookup"><span data-stu-id="ee161-108">nx_secure_module_hash_compute</span></span>](#nx_secure_module_hash_compute)
  - <span data-ttu-id="ee161-109">Karma değeri user_supplied karma işlevi kullanılarak hesaplar</span><span class="sxs-lookup"><span data-stu-id="ee161-109">Computes hash value using user_supplied hash function</span></span>
- [<span data-ttu-id="ee161-110">nx_secure_tls_active_certificate_set</span><span class="sxs-lookup"><span data-stu-id="ee161-110">nx_secure_tls_active_certificate_set</span></span>](#nx_secure_tls_active_certificate_set)
  - <span data-ttu-id="ee161-111">NetX güvenli TLS oturumu için etkin kimlik sertifikası ayarlama</span><span class="sxs-lookup"><span data-stu-id="ee161-111">Set the active identity certificate for a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="ee161-112">nx_secure_tls_client_psk_set</span><span class="sxs-lookup"><span data-stu-id="ee161-112">nx_secure_tls_client_psk_set</span></span>](#nx_secure_tls_client_psk_set)
  - <span data-ttu-id="ee161-113">NetX güvenli TLS Istemci oturumu için bir Pre_Shared anahtarı ayarlama</span><span class="sxs-lookup"><span data-stu-id="ee161-113">Set a Pre_Shared Key for a NetX Secure TLS Client Session</span></span>
- [<span data-ttu-id="ee161-114">nx_secure_tls_initialize</span><span class="sxs-lookup"><span data-stu-id="ee161-114">nx_secure_tls_initialize</span></span>](#nx_secure_tls_initialize)
  - <span data-ttu-id="ee161-115">NetX güvenli TLS modülünü başlatır]</span><span class="sxs-lookup"><span data-stu-id="ee161-115">Initializes the NetX Secure TLS module]</span></span>
- [<span data-ttu-id="ee161-116">nx_secure_tls_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="ee161-116">nx_secure_tls_local_certificate_add</span></span>](#nx_secure_tls_local_certificate_add)
  - <span data-ttu-id="ee161-117">NetX güvenli TLS oturumuna yerel sertifika ekleme</span><span class="sxs-lookup"><span data-stu-id="ee161-117">Add a local certificate to NetX Secure TLS Session</span></span>
- [<span data-ttu-id="ee161-118">nx_secure_tls_local_certificate_find</span><span class="sxs-lookup"><span data-stu-id="ee161-118">nx_secure_tls_local_certificate_find</span></span>](#nx_secure_tls_local_certificate_find)
  - <span data-ttu-id="ee161-119">Ortak ad ile bir NetX güvenli TLS oturumunda yerel bir sertifika bulun</span><span class="sxs-lookup"><span data-stu-id="ee161-119">Find a local certificate in a NetX Secure TLS Session by Common Name</span></span>
- [<span data-ttu-id="ee161-120">nx_secure_tls_local_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="ee161-120">nx_secure_tls_local_certificate_remove</span></span>](#nx_secure_tls_local_certificate_remove)
  - <span data-ttu-id="ee161-121">Yerel sertifikayı NetX güvenli TLS oturumundan kaldır</span><span class="sxs-lookup"><span data-stu-id="ee161-121">Remove local certificate from NetX Secure TLS Session</span></span>
- [<span data-ttu-id="ee161-122">nx_secure_tls_metadata_size_calculate</span><span class="sxs-lookup"><span data-stu-id="ee161-122">nx_secure_tls_metadata_size_calculate</span></span>](#nx_secure_tls_metadata_size_calculate)
  - <span data-ttu-id="ee161-123">NetX güvenli TLS oturumunun şifreleme meta verilerinin boyutunu hesaplama</span><span class="sxs-lookup"><span data-stu-id="ee161-123">Calculate size of cryptographic metadata for a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="ee161-124">nx_secure_tls_packet_allocate</span><span class="sxs-lookup"><span data-stu-id="ee161-124">nx_secure_tls_packet_allocate</span></span>](#nx_secure_tls_packet_allocate)
  - <span data-ttu-id="ee161-125">NetX güvenli TLS oturumu için bir paket ayırın</span><span class="sxs-lookup"><span data-stu-id="ee161-125">Allocate a packet for a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="ee161-126">nx_secure_tls_psk_add</span><span class="sxs-lookup"><span data-stu-id="ee161-126">nx_secure_tls_psk_add</span></span>](#nx_secure_tls_psk_add)
  - <span data-ttu-id="ee161-127">NetX güvenli TLS oturumuna Pre_Shared anahtarı ekleme</span><span class="sxs-lookup"><span data-stu-id="ee161-127">Add a Pre_Shared Key to a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="ee161-128">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="ee161-128">nx_secure_tls_remote_certificate_allocate</span></span>](#nx_secure_tls_remote_certificate_allocate)
  - <span data-ttu-id="ee161-129">Uzak bir TLS ana bilgisayarı tarafından belirtilen sertifika için alan ayır</span><span class="sxs-lookup"><span data-stu-id="ee161-129">Allocate space for the certificate provided by a remote TLS host</span></span>
- [<span data-ttu-id="ee161-130">nx_secure_tls_remote_certificate_buffer_allocate</span><span class="sxs-lookup"><span data-stu-id="ee161-130">nx_secure_tls_remote_certificate_buffer_allocate</span></span>](#nx_secure_tls_remote_certificate_buffer_allocate)
  - <span data-ttu-id="ee161-131">Uzak bir TLS ana bilgisayarı tarafından belirtilen tüm sertifikalar için alan ayır</span><span class="sxs-lookup"><span data-stu-id="ee161-131">Allocate space for all certificates provided by a remote TLS host</span></span>
- [<span data-ttu-id="ee161-132">nx_secure_tls_remote_certificate_free_all</span><span class="sxs-lookup"><span data-stu-id="ee161-132">nx_secure_tls_remote_certificate_free_all</span></span>](#nx_secure_tls_remote_certificate_free_all)
  - <span data-ttu-id="ee161-133">Gelen sertifikalar için ayrılan boş alan</span><span class="sxs-lookup"><span data-stu-id="ee161-133">Free space allocated for incoming certificates</span></span>
- [<span data-ttu-id="ee161-134">nx_secure_tls_server_certificate_add</span><span class="sxs-lookup"><span data-stu-id="ee161-134">nx_secure_tls_server_certificate_add</span></span>](#nx_secure_tls_server_certificate_add)
  - <span data-ttu-id="ee161-135">Sayısal bir tanımlayıcı kullanarak TLS sunucuları için özel olarak bir sertifika ekleyin</span><span class="sxs-lookup"><span data-stu-id="ee161-135">Add a certificate specifically for TLS servers using a numeric identifier</span></span>
- [<span data-ttu-id="ee161-136">nx_secure_tls_server_certificate_find</span><span class="sxs-lookup"><span data-stu-id="ee161-136">nx_secure_tls_server_certificate_find</span></span>](#nx_secure_tls_server_certificate_find)
  - <span data-ttu-id="ee161-137">Sayısal tanımlayıcı kullanarak sertifika bulma</span><span class="sxs-lookup"><span data-stu-id="ee161-137">Find a certificate using a numeric identifier</span></span>
- [<span data-ttu-id="ee161-138">nx_secure_tls_server_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="ee161-138">nx_secure_tls_server_certificate_remove</span></span>](#nx_secure_tls_server_certificate_remove)
  - <span data-ttu-id="ee161-139">Sayısal tanımlayıcıyı kullanarak yerel sunucu sertifikasını kaldırma</span><span class="sxs-lookup"><span data-stu-id="ee161-139">Remove a local server certificate using a numeric identifier</span></span>
- [<span data-ttu-id="ee161-140">nx_secure_tls_session_certificate_callback_set</span><span class="sxs-lookup"><span data-stu-id="ee161-140">nx_secure_tls_session_certificate_callback_set</span></span>](#nx_secure_tls_session_certificate_callback_set)
  - <span data-ttu-id="ee161-141">Ek sertifika doğrulaması için kullanılacak TLS için bir geri çağırma ayarlayın</span><span class="sxs-lookup"><span data-stu-id="ee161-141">Set up a callback for TLS to use for additional certificate validation</span></span>
- [<span data-ttu-id="ee161-142">nx_secure_tls_session_client_callback_set</span><span class="sxs-lookup"><span data-stu-id="ee161-142">nx_secure_tls_session_client_callback_set</span></span>](#nx_secure_tls_session_client_callback_set)
  - <span data-ttu-id="ee161-143">TLS Istemcisi el sıkışmasının başlangıcında çağırmak üzere TLS için bir geri çağırma ayarlayın</span><span class="sxs-lookup"><span data-stu-id="ee161-143">Set up a callback for TLS to invoke at the beginning of a TLS Client handshake</span></span>
- [<span data-ttu-id="ee161-144">nx_secure_tls_session_x509_client_verify_configure</span><span class="sxs-lookup"><span data-stu-id="ee161-144">nx_secure_tls_session_x509_client_verify_configure</span></span>](#nx_secure_tls_session_x509_client_verify_configure)
  - <span data-ttu-id="ee161-145">İstemci X. 509.440 doğrulamasını etkinleştir ve istemci sertifikaları için alan ayır</span><span class="sxs-lookup"><span data-stu-id="ee161-145">Enable client X.509 verification and allocate space for client certificates</span></span>
- [<span data-ttu-id="ee161-146">nx_secure_tls_session_client_verify_disable</span><span class="sxs-lookup"><span data-stu-id="ee161-146">nx_secure_tls_session_client_verify_disable</span></span>](#nx_secure_tls_session_client_verify_disable)
  - <span data-ttu-id="ee161-147">NetX güvenli TLS oturumu için Istemci sertifikası kimlik doğrulamasını devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="ee161-147">Disable Client Certificate Authentication for a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="ee161-148">nx_secure_tls_session_client_verify_enable</span><span class="sxs-lookup"><span data-stu-id="ee161-148">nx_secure_tls_session_client_verify_enable</span></span>](#nx_secure_tls_session_client_verify_enable)
  - <span data-ttu-id="ee161-149">NetX güvenli TLS oturumu için Istemci sertifikası kimlik doğrulamasını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="ee161-149">Enable Client Certificate Authentication for a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="ee161-150">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="ee161-150">nx_secure_tls_session_create</span></span>](#nx_secure_tls_session_create)
  - <span data-ttu-id="ee161-151">Güvenli iletişim için bir NetX güvenli TLS oturumu oluşturun</span><span class="sxs-lookup"><span data-stu-id="ee161-151">Create a NetX Secure TLS Session for secure communications</span></span>
- [<span data-ttu-id="ee161-152">nx_secure_tls_session_delete</span><span class="sxs-lookup"><span data-stu-id="ee161-152">nx_secure_tls_session_delete</span></span>](#nx_secure_tls_session_delete)
  - <span data-ttu-id="ee161-153">NetX güvenli TLS oturumunu silme</span><span class="sxs-lookup"><span data-stu-id="ee161-153">Delete a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="ee161-154">nx_secure_tls_session_end</span><span class="sxs-lookup"><span data-stu-id="ee161-154">nx_secure_tls_session_end</span></span>](#nx_secure_tls_session_end)
  - <span data-ttu-id="ee161-155">Etkin bir NetX güvenli TLS oturumu sonlandır</span><span class="sxs-lookup"><span data-stu-id="ee161-155">End an active NetX Secure TLS Session</span></span>
- [<span data-ttu-id="ee161-156">nx_secure_tls_session_packet_buffer_set</span><span class="sxs-lookup"><span data-stu-id="ee161-156">nx_secure_tls_session_packet_buffer_set</span></span>](#nx_secure_tls_session_packet_buffer_set)
  - <span data-ttu-id="ee161-157">NetX güvenli TLS oturumu için paket yeniden birleştirme arabelleğini ayarlama</span><span class="sxs-lookup"><span data-stu-id="ee161-157">Set the packet reassembly buffer for a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="ee161-158">nx_secure_tls_session_protocol_version_override</span><span class="sxs-lookup"><span data-stu-id="ee161-158">nx_secure_tls_session_protocol_version_override</span></span>](#nx_secure_tls_session_protocol_version_override)
  - <span data-ttu-id="ee161-159">NetX güvenli TLS oturumu için varsayılan TLS protokol sürümünü geçersiz kılın</span><span class="sxs-lookup"><span data-stu-id="ee161-159">Override the default TLS protocol version for a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="ee161-160">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="ee161-160">nx_secure_tls_session_receive</span></span>](#nx_secure_tls_session_receive)
  - <span data-ttu-id="ee161-161">NetX güvenli TLS oturumundan veri alma</span><span class="sxs-lookup"><span data-stu-id="ee161-161">Receive data from a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="ee161-162">nx_secure_tls_session_renegotiate_callback_set</span><span class="sxs-lookup"><span data-stu-id="ee161-162">nx_secure_tls_session_renegotiate_callback_set</span></span>](#nx_secure_tls_session_renegotiate_callback_set)
  - <span data-ttu-id="ee161-163">Oturum yeniden anlaşması başlangıcında çağrılacak bir geri çağırma atayın</span><span class="sxs-lookup"><span data-stu-id="ee161-163">Assign a callback that will be invoked at the beginning of a session renegotiation</span></span>
- [<span data-ttu-id="ee161-164">nx_secure_tls_session_renegotiate</span><span class="sxs-lookup"><span data-stu-id="ee161-164">nx_secure_tls_session_renegotiate</span></span>](#nx_secure_tls_session_renegotiate)
  - <span data-ttu-id="ee161-165">Uzak konakla oturum yeniden anlaşma anlaşmasını başlatma</span><span class="sxs-lookup"><span data-stu-id="ee161-165">Initiate a session renegotiation handshake with the remote host</span></span>
- [<span data-ttu-id="ee161-166">nx_secure_tls_session_reset</span><span class="sxs-lookup"><span data-stu-id="ee161-166">nx_secure_tls_session_reset</span></span>](#nx_secure_tls_session_reset)
  - <span data-ttu-id="ee161-167">NetX güvenli TLS oturumunu Temizleme ve sıfırlama</span><span class="sxs-lookup"><span data-stu-id="ee161-167">Clear out and reset a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="ee161-168">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="ee161-168">nx_secure_tls_session_send</span></span>](#nx_secure_tls_session_send)
  - <span data-ttu-id="ee161-169">NetX güvenli TLS oturumu aracılığıyla veri gönderme</span><span class="sxs-lookup"><span data-stu-id="ee161-169">Send data through a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="ee161-170">nx_secure_tls_session_server_callback_set</span><span class="sxs-lookup"><span data-stu-id="ee161-170">nx_secure_tls_session_server_callback_set</span></span>](#nx_secure_tls_session_server_callback_set)
  - <span data-ttu-id="ee161-171">TLS sunucusu el sıkışmasının başlangıcında çağırmak üzere TLS için bir geri çağırma ayarlayın</span><span class="sxs-lookup"><span data-stu-id="ee161-171">Set up a callback for TLS to invoke at the beginning of a TLS Server handshake</span></span>
- [<span data-ttu-id="ee161-172">nx_secure_tls_session_sni_extension_parse</span><span class="sxs-lookup"><span data-stu-id="ee161-172">nx_secure_tls_session_sni_extension_parse</span></span>](#nx_secure_tls_session_sni_extension_parse)
  - <span data-ttu-id="ee161-173">TLS Istemcisinden alınan Sunucu Adı Belirtme (SNı) uzantısını ayrıştırma</span><span class="sxs-lookup"><span data-stu-id="ee161-173">Parse a Server Name Indication (SNI) extension received from a TLS Client</span></span>
- [<span data-ttu-id="ee161-174">nx_secure_tls_session_sni_extension_set</span><span class="sxs-lookup"><span data-stu-id="ee161-174">nx_secure_tls_session_sni_extension_set</span></span>](#nx_secure_tls_session_sni_extension_set)
  - <span data-ttu-id="ee161-175">Bir Sunucu Adı Belirtme (SNı) uzantısı DNS adını uzak bir sunucuya göndermek üzere ayarla</span><span class="sxs-lookup"><span data-stu-id="ee161-175">Set a Server Name Indication (SNI) extension DNS name to send to a remote Server</span></span>
- [<span data-ttu-id="ee161-176">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="ee161-176">nx_secure_tls_session_start</span></span>](#nx_secure_tls_session_start)
  - <span data-ttu-id="ee161-177">NetX güvenli TLS oturumu başlatma</span><span class="sxs-lookup"><span data-stu-id="ee161-177">Start a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="ee161-178">nx_secure_tls_session_time_function_set</span><span class="sxs-lookup"><span data-stu-id="ee161-178">nx_secure_tls_session_time_function_set</span></span>](#nx_secure_tls_session_time_function_set)
  - <span data-ttu-id="ee161-179">NetX güvenli TLS oturumuna zaman damgası işlevi atama</span><span class="sxs-lookup"><span data-stu-id="ee161-179">Assign a timestamp function to a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="ee161-180">nx_secure_tls_trusted_certificate_add</span><span class="sxs-lookup"><span data-stu-id="ee161-180">nx_secure_tls_trusted_certificate_add</span></span>](#nx_secure_tls_trusted_certificate_add)
  - <span data-ttu-id="ee161-181">NetX güvenli TLS oturumuna güvenilen sertifika ekleme</span><span class="sxs-lookup"><span data-stu-id="ee161-181">Add trusted certificate to NetX Secure TLS Session</span></span>
- [<span data-ttu-id="ee161-182">nx_secure_tls_trusted_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="ee161-182">nx_secure_tls_trusted_certificate_remove</span></span>](#nx_secure_tls_trusted_certificate_remove)
  - <span data-ttu-id="ee161-183">Güvenilen sertifikayı NetX güvenli TLS oturumundan kaldır</span><span class="sxs-lookup"><span data-stu-id="ee161-183">Remove trusted certificate from NetX Secure TLS Session</span></span>
- [<span data-ttu-id="ee161-184">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="ee161-184">nx_secure_x509_certificate_initialize</span></span>](#nx_secure_x509_certificate_initialize)
  - <span data-ttu-id="ee161-185">NetX güvenli TLS için X. 509.440 sertifikasını başlatın</span><span class="sxs-lookup"><span data-stu-id="ee161-185">Initialize X.509 Certificate for NetX Secure TLS</span></span>
- [<span data-ttu-id="ee161-186">nx_secure_x509_common_name_dns_check</span><span class="sxs-lookup"><span data-stu-id="ee161-186">nx_secure_x509_common_name_dns_check</span></span>](#nx_secure_x509_common_name_dns_check)
  - <span data-ttu-id="ee161-187">X. 509.440 sertifikasıyla DNS adını denetle</span><span class="sxs-lookup"><span data-stu-id="ee161-187">Check DNS name against X.509 Certificate</span></span>
- [<span data-ttu-id="ee161-188">nx_secure_x509_crl_revocation_check</span><span class="sxs-lookup"><span data-stu-id="ee161-188">nx_secure_x509_crl_revocation_check</span></span>](#nx_secure_x509_crl_revocation_check)
  - <span data-ttu-id="ee161-189">Sağlanan sertifika Iptal listesine (CRL) göre X. 509.440 sertifikasını denetle]</span><span class="sxs-lookup"><span data-stu-id="ee161-189">Check X.509 Certificate against a supplied Certificate Revocation List (CRL)]</span></span>
- [<span data-ttu-id="ee161-190">nx_secure_x509_dns_name_initialize</span><span class="sxs-lookup"><span data-stu-id="ee161-190">nx_secure_x509_dns_name_initialize</span></span>](#nx_secure_x509_dns_name_initialize)
  - <span data-ttu-id="ee161-191">X. 509.440 DNS adı yapısını başlatma</span><span class="sxs-lookup"><span data-stu-id="ee161-191">Initialize an X.509 DNS name structure</span></span>
- [<span data-ttu-id="ee161-192">nx_secure_x509_extended_key_usage_extension_parse</span><span class="sxs-lookup"><span data-stu-id="ee161-192">nx_secure_x509_extended_key_usage_extension_parse</span></span>](#nx_secure_x509_extended_key_usage_extension_parse)
  - <span data-ttu-id="ee161-193">X. 509.440 sertifikası içindeki X. 509.952 genişletilmiş anahtar kullanımı uzantısını bulma ve ayrıştırma</span><span class="sxs-lookup"><span data-stu-id="ee161-193">Find and parse an X.509 extended key usage extension in an X.509 certificate</span></span>
- [<span data-ttu-id="ee161-194">nx_secure_x509_extension_find</span><span class="sxs-lookup"><span data-stu-id="ee161-194">nx_secure_x509_extension_find</span></span>](#nx_secure_x509_extension_find)
  - <span data-ttu-id="ee161-195">X. 509.440 sertifikasında bir X. 509.440 uzantısı bulun ve döndürün</span><span class="sxs-lookup"><span data-stu-id="ee161-195">Find and return an X.509 extension in an X.509 certificate</span></span>
- [<span data-ttu-id="ee161-196">nx_secure_x509_key_usage_extension_parse</span><span class="sxs-lookup"><span data-stu-id="ee161-196">nx_secure_x509_key_usage_extension_parse</span></span>](#nx_secure_x509_key_usage_extension_parse)
  - <span data-ttu-id="ee161-197">X. 509.440 sertifikasında X. 509.440 anahtar kullanımı uzantısını bulma ve ayrıştırma</span><span class="sxs-lookup"><span data-stu-id="ee161-197">Find and parse an X.509 Key Usage extension in an X.509 certificate</span></span>

## <a name="nx_secure_crypto_table_self_test"></a><span data-ttu-id="ee161-198">nx_secure_crypto_table_self_test</span><span class="sxs-lookup"><span data-stu-id="ee161-198">nx_secure_crypto_table_self_test</span></span>

<span data-ttu-id="ee161-199">Şifre yöntemlerinde kendi kendine test gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="ee161-199">Perform self-test on the crypto methods</span></span>

### <a name="prototype"></a><span data-ttu-id="ee161-200">Prototype</span><span class="sxs-lookup"><span data-stu-id="ee161-200">Prototype</span></span>

```C
UINT nx_secure_crypto_table_self_test(
                                  const NX_SECURE_TLS_CRYPTO *crypto_table,
                                  VOID *metadata, UINT metadata_size);
```

### <a name="description"></a><span data-ttu-id="ee161-201">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-201">Description</span></span>

<span data-ttu-id="ee161-202">Bu hizmet, doğrulamak üzere kendi kendini test eden şifreleme yöntemi aracılığıyla çalışır.</span><span class="sxs-lookup"><span data-stu-id="ee161-202">This service runs through the crypto method self tests to validate.</span></span> <span data-ttu-id="ee161-203">Self test yalnızca NetX güvenli kitaplığı tanımlı NX_SECURE_POWER_ON_SELF_TEST_MODULE_INTEGRITY_CHECK simgesiyle derlenip kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ee161-203">The self test is available only if NetX Secure library is built with the symbol NX_SECURE_POWER_ON_SELF_TEST_MODULE_INTEGRITY_CHECK defined.</span></span>

<span data-ttu-id="ee161-204">Desteklenen her şifreleme yöntemi için, self test önceden tanımlanmış giriş verileri sağlar ve çıktının önceden tanımlanmış beklenen değerle eşleştiğini doğruladı.</span><span class="sxs-lookup"><span data-stu-id="ee161-204">For each supported crypto method, the self test provides pre-defined input data, and verified the output matches the pre-defined expected value.</span></span>

<span data-ttu-id="ee161-205">NetX güvenli şifreleme self test aşağıdaki algoritmaları ve anahtar boyutlarını destekler:</span><span class="sxs-lookup"><span data-stu-id="ee161-205">NetX Secure crypto self test supports the following algorithms and key sizes:</span></span>

- <span data-ttu-id="ee161-206">DES: şifreleme ve şifre çözme</span><span class="sxs-lookup"><span data-stu-id="ee161-206">DES: encryption and decryption</span></span>
- <span data-ttu-id="ee161-207">Üçlü DES (3DES): şifreleme ve şifre çözme</span><span class="sxs-lookup"><span data-stu-id="ee161-207">Triple DES (3DES): encryption and decryption</span></span>
- <span data-ttu-id="ee161-208">AES: 128-, 192-, 256-bit anahtar boyutu, şifreleme ve şifre çözme, CBC modunda ve sayaç modunda.</span><span class="sxs-lookup"><span data-stu-id="ee161-208">AES: 128-, 192-, 256-bit key size, encryption and decryption, in CBC mode and counter mode.</span></span>
- <span data-ttu-id="ee161-209">HMAC-MD5: kimlik doğrulama ve karma hesaplama</span><span class="sxs-lookup"><span data-stu-id="ee161-209">HMAC-MD5: authentication and hash computation</span></span>
- <span data-ttu-id="ee161-210">HMAC-SHA: SHA1-96, SHA1-160, SHA2-256, SHA2-384, SHA2-512, kimlik doğrulama ve karma hesaplama</span><span class="sxs-lookup"><span data-stu-id="ee161-210">HMAC-SHA: SHA1-96, SHA1-160, SHA2-256, SHA2-384, SHA2- 512, authentication and hash computation</span></span>
- <span data-ttu-id="ee161-211">MD5: kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="ee161-211">MD5: authentication</span></span>
- <span data-ttu-id="ee161-212">Sözde rastgele Işlev (PRF): PRF_HMAC_SHA1 ve PRF_HMAC_SHA2-256</span><span class="sxs-lookup"><span data-stu-id="ee161-212">Pseudo-random Function (PRF): PRF_HMAC_SHA1 and PRF_HMAC_SHA2-256</span></span>
- <span data-ttu-id="ee161-213">RSA: 1024-, 2048-, 4096-bit RSA güç-mod işlemi</span><span class="sxs-lookup"><span data-stu-id="ee161-213">RSA: 1024-, 2048-, 4096-bit RSA power-modulus operation</span></span>
- <span data-ttu-id="ee161-214">SHA: SHA1 (96-ve 160-bit), SHA2 (256bit, 384bit, 512bit) kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="ee161-214">SHA: SHA1 (96- and 160-bit), SHA2 (256bit, 384bit, 512bit) authentication</span></span>

<span data-ttu-id="ee161-215">Bu işlev, yukarıda listelenen şifre algoritmalarına yönelik yerleşik vektörlerine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="ee161-215">This function has the built-in vectors for the crypto algorithms listed above.</span></span> <span data-ttu-id="ee161-216">Ancak, yalnızca bu işleve geçirilen *cipher_table* listelenen olanları sınar.</span><span class="sxs-lookup"><span data-stu-id="ee161-216">However it only tests the ones listed in the *cipher_table* passed into this function.</span></span> <span data-ttu-id="ee161-217">Örneğin, bir TLS oturumu yalnızca ciphersuite TLS_RSA_WITH_AES_128_CBC_SHA kullandığında, bu işlev RSA (1024-, 2048-, 4096-bit), AES-CBC (128-bit) ve SHA1 üzerinde kendi kendine test gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="ee161-217">For example, for a TLS session uses only the ciphersuite TLS_RSA_WITH_AES_128_CBC_SHA, this function will perform self test on the RSA (1024-, 2048-, 4096-bit), AES-CBC (128-bit) and SHA1.</span></span>

### <a name="parameters"></a><span data-ttu-id="ee161-218">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ee161-218">Parameters</span></span>

- <span data-ttu-id="ee161-219">**crypto_table** TLS oturumu tarafından kullanılan şifre tablosunun işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-219">**crypto_table** Pointer to the crypto table being used by the TLS session.</span></span> <span data-ttu-id="ee161-220">Bu, **_nx_secure_tls_session_create ()_** çağrısına geçirilen crypto_table aynıdır.</span><span class="sxs-lookup"><span data-stu-id="ee161-220">This is the same crypto_table being passed into the **_nx_secure_tls_session_create()_** call.</span></span>
- <span data-ttu-id="ee161-221">**meta veriler** Şifreleme meta verileri alanı için boşluk işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-221">**metadata** Pointer to space for cryptography metadata area.</span></span> <span data-ttu-id="ee161-222">.</span><span class="sxs-lookup"><span data-stu-id="ee161-222">.</span></span>
- <span data-ttu-id="ee161-223">**metadata_size** Meta veri arabelleğinin boyutu.</span><span class="sxs-lookup"><span data-stu-id="ee161-223">**metadata_size** Size of the metadata buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="ee161-224">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ee161-224">Return Values</span></span>

- <span data-ttu-id="ee161-225">**NX_SECURE_TLS_SUCCESS** (0x00), belirtilen şifreleme yöntemlerini başarıyla test edildi.</span><span class="sxs-lookup"><span data-stu-id="ee161-225">**NX_SECURE_TLS_SUCCESS** (0x00) Successfully tested the crypto methods provided.</span></span>
- <span data-ttu-id="ee161-226">**NX_PTR_ERROR** (0x07) geçersiz şifreleme yöntemi yapısı</span><span class="sxs-lookup"><span data-stu-id="ee161-226">**NX_PTR_ERROR** (0x07) Invalid crypto method structure</span></span>
- <span data-ttu-id="ee161-227">**NX_NOT_SUCCESSFUL** (0x43) şifreleme self test başarısız oluyor.</span><span class="sxs-lookup"><span data-stu-id="ee161-227">**NX_NOT_SUCCESSFUL** (0x43) Crypto self test fails.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ee161-228">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ee161-228">Allowed From</span></span>

<span data-ttu-id="ee161-229">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ee161-229">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="ee161-230">Örnek</span><span class="sxs-lookup"><span data-stu-id="ee161-230">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="ee161-231">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ee161-231">See Also</span></span>

- <span data-ttu-id="ee161-232">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="ee161-232">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_module_hash_compute"></a><span data-ttu-id="ee161-233">nx_secure_module_hash_compute</span><span class="sxs-lookup"><span data-stu-id="ee161-233">nx_secure_module_hash_compute</span></span>

<span data-ttu-id="ee161-234">Kullanıcı tarafından sağlanan karma işlevi kullanarak karma değeri hesaplar</span><span class="sxs-lookup"><span data-stu-id="ee161-234">Computes hash value using user-supplied hash function</span></span>

### <a name="prototype"></a><span data-ttu-id="ee161-235">Prototype</span><span class="sxs-lookup"><span data-stu-id="ee161-235">Prototype</span></span>

```C
UINT nx_secure_module_hash_compute(
                      NX_CRYPTO_METHOD *hamc_ptr,
                      UINT start_address, UINT end_address,
                      UCHAR *key, UINT key_length,
                      VOID *metadata, UINT metadata_size,
                      UCHAR *output_buffer, UINT output_buffer_size,
                      UINT *actual_size);
```

### <a name="description"></a><span data-ttu-id="ee161-236">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-236">Description</span></span>

<span data-ttu-id="ee161-237">Bu işlev, sağlanan HMAC şifre yöntemini ve anahtar dizesini kullanarak belirtilen bellek alanındaki veri akışının karma değerini hesaplar.</span><span class="sxs-lookup"><span data-stu-id="ee161-237">This function computes the hash value of the data stream in the specified memory area, using supplied HMAC crypto method and the key string.</span></span> <span data-ttu-id="ee161-238">Modül karma işlem işlevi yalnızca NetX güvenli kitaplığı tanımlanmakta olan şu sembol ile derleniyorsa kullanılabilir: NX_SECURE_POWER_ON_SELF_TEST_MODULE_INTEGRITY_CHECK</span><span class="sxs-lookup"><span data-stu-id="ee161-238">The module hash compute function is available only if NetX Secure library is built with the following symbol being defined: NX_SECURE_POWER_ON_SELF_TEST_MODULE_INTEGRITY_CHECK</span></span>

### <a name="parameters"></a><span data-ttu-id="ee161-239">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ee161-239">Parameters</span></span>

- <span data-ttu-id="ee161-240">**hmac_ptr** Karma değer hesaplama için kullanılan HMAC şifre yöntemine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ee161-240">**hmac_ptr** Pointer to the HMAC crypto method being used for the hash value computation.</span></span>
- <span data-ttu-id="ee161-241">**start_address** Veri arabelleğinin başlangıç adresi</span><span class="sxs-lookup"><span data-stu-id="ee161-241">**start_address** The starting address of the data buffer</span></span>
- <span data-ttu-id="ee161-242">**end_address** Veri arabelleğinin bitiş adresi.</span><span class="sxs-lookup"><span data-stu-id="ee161-242">**end_address** The ending address of the data buffer.</span></span> <span data-ttu-id="ee161-243">Karma hesaplamasının bu end_address verileri kapsamadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ee161-243">Note that hash computation does not cover the data at this end_address.</span></span>
- <span data-ttu-id="ee161-244">**anahtar** HMAC hesaplamasında kullanılan anahtar dizesi.</span><span class="sxs-lookup"><span data-stu-id="ee161-244">**key** The key string being used in the HMAC computation.</span></span>
- <span data-ttu-id="ee161-245">**key_length** Anahtar dizesinin bayt cinsinden boyutu</span><span class="sxs-lookup"><span data-stu-id="ee161-245">**key_length** The size of the key string, in bytes</span></span>
- <span data-ttu-id="ee161-246">**meta veriler** HMAC algoritması tarafından kullanılan alana yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ee161-246">**metadata** Pointer to space used by the HMAC algorithm.</span></span>
- <span data-ttu-id="ee161-247">**metadata_size** Meta veri arabelleğinin boyutu.</span><span class="sxs-lookup"><span data-stu-id="ee161-247">**metadata_size** Size of the metadata buffer.</span></span>
- <span data-ttu-id="ee161-248">**output_buffer** Karma çıkışın depolandığı bellek konumu.</span><span class="sxs-lookup"><span data-stu-id="ee161-248">**output_buffer** The memory location where the hash output is being stored at.</span></span>
- <span data-ttu-id="ee161-249">**output_buffer_size** Çıkış arabelleğinin bayt cinsinden kullanılabilir alanı</span><span class="sxs-lookup"><span data-stu-id="ee161-249">**output_buffer_size** The available space of the output buffer, in bytes</span></span>
- <span data-ttu-id="ee161-250">**actual_size** İşlev tarafından döndürülen, output_buffer yazılan gerçek bayt sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="ee161-250">**actual_size** Returned by the function indicating the actual number of bytes being written into the output_buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="ee161-251">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ee161-251">Return Values</span></span>

- <span data-ttu-id="ee161-252">**0** , karma değeri başarıyla hesaplandı.</span><span class="sxs-lookup"><span data-stu-id="ee161-252">**0** Successfully computed the hash value.</span></span>
- <span data-ttu-id="ee161-253">**1** karma hesaplama başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="ee161-253">**1** The hash computation failed.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ee161-254">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ee161-254">Allowed From</span></span>

<span data-ttu-id="ee161-255">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ee161-255">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="ee161-256">Örnek</span><span class="sxs-lookup"><span data-stu-id="ee161-256">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="ee161-257">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ee161-257">See Also</span></span>

- <span data-ttu-id="ee161-258">nx_secure_crypto_method_self_test</span><span class="sxs-lookup"><span data-stu-id="ee161-258">nx_secure_crypto_method_self_test</span></span>

## <a name="nx_secure_tls_active_certificate_set"></a><span data-ttu-id="ee161-259">nx_secure_tls_active_certificate_set</span><span class="sxs-lookup"><span data-stu-id="ee161-259">nx_secure_tls_active_certificate_set</span></span>

<span data-ttu-id="ee161-260">NetX güvenli TLS oturumu için etkin kimlik sertifikası ayarlama</span><span class="sxs-lookup"><span data-stu-id="ee161-260">Set the active identity certificate for a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="ee161-261">Prototype</span><span class="sxs-lookup"><span data-stu-id="ee161-261">Prototype</span></span>

```C
UINT  nx_secure_tls_active_certificate_set(
                   NX_SECURE_TLS_SESSION *tls_session,
                   NX_SECURE_X509_CERT *certificate);
```

### <a name="description"></a><span data-ttu-id="ee161-262">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-262">Description</span></span>

<span data-ttu-id="ee161-263">Bu hizmetin bir oturum geri çağırması içinden çağrılması amaçlanmıştır (bkz. nx_secure_tls_session_client_callback_set ve nx_secure_tls_session_server_callback_set).</span><span class="sxs-lookup"><span data-stu-id="ee161-263">This service is intended to be called from within a session callback (see nx_secure_tls_session_client_callback_set and nx_secure_tls_session_server_callback_set).</span></span> <span data-ttu-id="ee161-264">Daha önce başlatılmış bir NX_SECURE_X509_CERT yapısıyla çağrıldığında, bu sertifika varsayılan kimlik sertifikası yerine kullanılacaktır.</span><span class="sxs-lookup"><span data-stu-id="ee161-264">When called with a previously-initialized NX_SECURE_X509_CERT structure, that certificate will be used instead of the default identity certificate.</span></span> <span data-ttu-id="ee161-265">Çoğu durumda, sertifika yerel depoya eklenmiş olmalıdır (bkz. nx_secure_tls_local_certificate_add) veya TLS el sıkışması başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="ee161-265">In most cases, the certificate must have been added to the local store (see nx_secure_tls_local_certificate_add) or the TLS handshake may fail.</span></span>

<span data-ttu-id="ee161-266">Bu hizmet, TLS 'nin birden çok kimlik sertifikasını desteklemesini sağlamak için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="ee161-266">This service is intended to allow TLS to support multiple identity certificates.</span></span> <span data-ttu-id="ee161-267">Bu, birden çok ağ adresine hizmet veren bir TLS sunucusu için yararlıdır, böylece sunucu, istemcinin giriş noktasına bağlı olarak uzak istemciye sağlamak üzere uygun bir sertifika seçebilir.</span><span class="sxs-lookup"><span data-stu-id="ee161-267">This is useful for a TLS server that services multiple network addresses so the server can pick an appropriate certificate to provide to the remote client depending on the client's entrypoint.</span></span> <span data-ttu-id="ee161-268">TLS istemcisi için, bu yordam, bir uzak sunucuya gönderilen sertifikayı, sunucu bir TLS el sıkışmasından tanımladıktan sonra (TLS sunucusu kullanım örneği 'nden daha nadir) değiştirmek üzere kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ee161-268">For a TLS client, this routine may be used to change the certificate sent to a remote server at runtime after the server has identified itself in the TLS handshake (this is more rare than the TLS server use-case).</span></span>

<span data-ttu-id="ee161-269">Birden çok sertifikanın aynı X. 509.952 ayırt edici adını paylaştığı durumlarda, sertifikaların, sertifikadan ayrı bir sayısal tanımlayıcı sunan nx_secure_tls_server_certificate_add kullanılarak eklenmesi gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="ee161-269">In the case where multiple certificates may share the same X.509 distinguished name, certificates will need to be added using nx_secure_tls_server_certificate_add, which introduces a numeric identifier separate from the certificate.</span></span>

### <a name="parameters"></a><span data-ttu-id="ee161-270">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ee161-270">Parameters</span></span>

- <span data-ttu-id="ee161-271">**session_ptr** Oturum geri çağırmaya geçilen bir TLS oturum örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-271">**session_ptr** Pointer to a TLS Session instance passed into the session callback.</span></span>
- <span data-ttu-id="ee161-272">**sertifika** Geçerli oturum için kullanılacak bir başlatılmış X. 509.440 sertifikasına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ee161-272">**certificate** Pointer to an initialized X.509 certificate that is to be used for the current session.</span></span>

### <a name="return-values"></a><span data-ttu-id="ee161-273">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ee161-273">Return Values</span></span>

- <span data-ttu-id="ee161-274">**NX_SUCCESS** (0x00) sertifikanın oturumun başarıyla atanması.</span><span class="sxs-lookup"><span data-stu-id="ee161-274">**NX_SUCCESS** (0x00) Successful assignment of certificate to session.</span></span>
- <span data-ttu-id="ee161-275">**NX_PTR_ERROR** (0x07) geçersiz TLS oturumu veya sertifika işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-275">**NX_PTR_ERROR** (0x07) Invalid TLS session or certificate pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ee161-276">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ee161-276">Allowed From</span></span>

<span data-ttu-id="ee161-277">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ee161-277">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ee161-278">Örnek</span><span class="sxs-lookup"><span data-stu-id="ee161-278">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="ee161-279">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ee161-279">See Also</span></span>

- <span data-ttu-id="ee161-280">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="ee161-280">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="ee161-281">nx_secure_tls_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="ee161-281">nx_secure_tls_local_certificate_add</span></span>
- <span data-ttu-id="ee161-282">nx_secure_tls_session_client_callback_set</span><span class="sxs-lookup"><span data-stu-id="ee161-282">nx_secure_tls_session_client_callback_set</span></span>
- <span data-ttu-id="ee161-283">nx_secure_tls_session_server_callback_set</span><span class="sxs-lookup"><span data-stu-id="ee161-283">nx_secure_tls_session_server_callback_set</span></span>
- <span data-ttu-id="ee161-284">nx_secure_tls_server_certificate_add</span><span class="sxs-lookup"><span data-stu-id="ee161-284">nx_secure_tls_server_certificate_add</span></span>
- <span data-ttu-id="ee161-285">nx_secure_tls_server_certificate_find</span><span class="sxs-lookup"><span data-stu-id="ee161-285">nx_secure_tls_server_certificate_find</span></span>
- <span data-ttu-id="ee161-286">nx_secure_tls_server_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="ee161-286">nx_secure_tls_server_certificate_remove</span></span>

## <a name="nx_secure_tls_client_psk_set"></a><span data-ttu-id="ee161-287">nx_secure_tls_client_psk_set</span><span class="sxs-lookup"><span data-stu-id="ee161-287">nx_secure_tls_client_psk_set</span></span>

<span data-ttu-id="ee161-288">NetX güvenli TLS Istemci oturumu için önceden paylaşılan anahtar ayarlama</span><span class="sxs-lookup"><span data-stu-id="ee161-288">Set a Pre-Shared Key for a NetX Secure TLS Client Session</span></span>

### <a name="prototype"></a><span data-ttu-id="ee161-289">Prototype</span><span class="sxs-lookup"><span data-stu-id="ee161-289">Prototype</span></span>

```C
UINT  nx_secure_tls_client_psk_set(NX_SECURE_TLS_SESSION *session_ptr,
                              UCHAR *pre_shared_key, UINT psk_length,
                              UCHAR *psk_identity, UINT identity_length,
                              UCHAR *hint, UINT hint_length);
```

### <a name="description"></a><span data-ttu-id="ee161-290">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-290">Description</span></span>

<span data-ttu-id="ee161-291">Bu hizmet, bir TLS oturum denetim bloğuna önceden paylaşılan anahtar (PSK), kimlik dizesi ve kimlik ipucu ekler ve bu PSK 'yi sonraki TLS Istemci bağlantılarında kullanılacak şekilde ayarlar.</span><span class="sxs-lookup"><span data-stu-id="ee161-291">This service adds a Pre-Shared Key (PSK), its identity string, and an identity hint to a TLS Session control block, and sets that PSK to be used in subsequent TLS Client connections.</span></span> <span data-ttu-id="ee161-292">PSK ciphersuites etkin ve kullanıldığında, bir dijital sertifika yerine PSK kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ee161-292">The PSK is used in place of a digital certificate when PSK ciphersuites are enabled and used.</span></span>

<span data-ttu-id="ee161-293">Bu durumda, PSK, TLS Istemcisinin iletişim kurmasını istediği belirli bir uzak TLS sunucusuyla ilişkilendirilir.</span><span class="sxs-lookup"><span data-stu-id="ee161-293">In this case, the PSK is associated with a specific remote TLS Server with which the TLS Client wishes to communicate.</span></span> <span data-ttu-id="ee161-294">Bu API aracılığıyla ayarlanan PSK, sonraki TLS el sıkışması sırasında uzak TLS sunucu konağına sunulacaktır.</span><span class="sxs-lookup"><span data-stu-id="ee161-294">The PSK set through this API will be provided to the remote TLS Server host during the next TLS handshake.</span></span>

### <a name="parameters"></a><span data-ttu-id="ee161-295">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ee161-295">Parameters</span></span>

- <span data-ttu-id="ee161-296">**session_ptr** Daha önce oluşturulmuş bir TLS oturum örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ee161-296">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="ee161-297">**pre_shared_key** Gerçek PSK değeri.</span><span class="sxs-lookup"><span data-stu-id="ee161-297">**pre_shared_key** The actual PSK value.</span></span>
- <span data-ttu-id="ee161-298">**psk_length** PSK değeri uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="ee161-298">**psk_length** The length of the PSK value.</span></span>
- <span data-ttu-id="ee161-299">**psk_identity** Bu PSK değerini tanımlamak için kullanılan dize.</span><span class="sxs-lookup"><span data-stu-id="ee161-299">**psk_identity** A string used to identify this PSK value.</span></span>
- <span data-ttu-id="ee161-300">**identity_length** PSK kimliğinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="ee161-300">**identity_length** The length of the PSK identity.</span></span>
- <span data-ttu-id="ee161-301">**İpucu** Bir TLS sunucusunda hangi sayıda PSKs arasından seçim yapmak gerektiğini göstermek için kullanılan dize.</span><span class="sxs-lookup"><span data-stu-id="ee161-301">**hint** A string used to indicate which group of PSKs to choose from on a TLS server.</span></span>
- <span data-ttu-id="ee161-302">**hint_length** İpucu dizesinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="ee161-302">**hint_length** The length of the hint string.</span></span>

### <a name="return-values"></a><span data-ttu-id="ee161-303">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ee161-303">Return Values</span></span>

- <span data-ttu-id="ee161-304">**NX_SUCCESS** (0x00) PSK 'nin başarılı bir şekilde eklenmesi.</span><span class="sxs-lookup"><span data-stu-id="ee161-304">**NX_SUCCESS** (0x00) Successful addition of PSK.</span></span>
- <span data-ttu-id="ee161-305">**NX_PTR_ERROR** (0x07) geçersiz TLS oturum işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-305">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>
- <span data-ttu-id="ee161-306">**NX_SECURE_TLS_NO_MORE_PSK_SPACE** (0x125) başka bir PSK eklenemiyor.</span><span class="sxs-lookup"><span data-stu-id="ee161-306">**NX_SECURE_TLS_NO_MORE_PSK_SPACE** (0x125) Cannot add another PSK.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ee161-307">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ee161-307">Allowed From</span></span>

<span data-ttu-id="ee161-308">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ee161-308">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ee161-309">Örnek</span><span class="sxs-lookup"><span data-stu-id="ee161-309">Example</span></span>

```C
/* PSK value.  */
UCHAR psk[] = { 0x1a, 0x2b, 0x3c, 0x4d };

/* Add PSK to TLS session.  */
status =  nx_secure_tls_client_psk_set(&tls_session, psk, sizeof(psk), “psk_1”, 4,
“Client_identity”, 15);


/* If status is NX_SUCCESS the PSK was successfully added.  */
```

### <a name="see-also"></a><span data-ttu-id="ee161-310">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ee161-310">See Also</span></span>

- <span data-ttu-id="ee161-311">nx_secure_tls_psk_add</span><span class="sxs-lookup"><span data-stu-id="ee161-311">nx_secure_tls_psk_add</span></span>
- <span data-ttu-id="ee161-312">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="ee161-312">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="ee161-313">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="ee161-313">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="ee161-314">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="ee161-314">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="ee161-315">nx_secure_tls_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="ee161-315">nx_secure_tls_local_certificate_add</span></span>

## <a name="nx_secure_tls_initialize"></a><span data-ttu-id="ee161-316">nx_secure_tls_initialize</span><span class="sxs-lookup"><span data-stu-id="ee161-316">nx_secure_tls_initialize</span></span>

<span data-ttu-id="ee161-317">NetX güvenli TLS modülünü başlatır</span><span class="sxs-lookup"><span data-stu-id="ee161-317">Initializes the NetX Secure TLS module</span></span>

### <a name="prototype"></a><span data-ttu-id="ee161-318">Prototype</span><span class="sxs-lookup"><span data-stu-id="ee161-318">Prototype</span></span>

```C
VOID nx_secure_tls_initialize(VOID);
```

### <a name="description"></a><span data-ttu-id="ee161-319">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-319">Description</span></span>

<span data-ttu-id="ee161-320">Bu hizmet NetX güvenli TLS modülünü başlatır.</span><span class="sxs-lookup"><span data-stu-id="ee161-320">This service initializes the NetX Secure TLS module.</span></span> <span data-ttu-id="ee161-321">Diğer NetX güvenli hizmetlere erişilebilmesi için önce bu adı çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ee161-321">It must be called before other NetX Secure services can be accessed.</span></span>

### <a name="parameters"></a><span data-ttu-id="ee161-322">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ee161-322">Parameters</span></span>

<span data-ttu-id="ee161-323">Hiçbiri</span><span class="sxs-lookup"><span data-stu-id="ee161-323">None</span></span>

### <a name="return-values"></a><span data-ttu-id="ee161-324">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ee161-324">Return Values</span></span>

<span data-ttu-id="ee161-325">Yok</span><span class="sxs-lookup"><span data-stu-id="ee161-325">None</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ee161-326">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ee161-326">Allowed From</span></span>

<span data-ttu-id="ee161-327">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ee161-327">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="ee161-328">Örnek</span><span class="sxs-lookup"><span data-stu-id="ee161-328">Example</span></span>

```C
/* Initializes the TLS module. */
Nx_secure_tls_initialize();
```

### <a name="see-also"></a><span data-ttu-id="ee161-329">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ee161-329">See Also</span></span>

- <span data-ttu-id="ee161-330">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="ee161-330">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_local_certificate_add"></a><span data-ttu-id="ee161-331">nx_secure_tls_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="ee161-331">nx_secure_tls_local_certificate_add</span></span>

<span data-ttu-id="ee161-332">NetX güvenli TLS oturumuna yerel sertifika ekleme</span><span class="sxs-lookup"><span data-stu-id="ee161-332">Add a local certificate to NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="ee161-333">Prototype</span><span class="sxs-lookup"><span data-stu-id="ee161-333">Prototype</span></span>

```C
UINT  nx_secure_tls_local_certificate_add(
              NX_SECURE_TLS_SESSION *session_ptr,
              NX_SECURE_X509_CERT *certificate_ptr);
```

### <a name="description"></a><span data-ttu-id="ee161-334">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-334">Description</span></span>

<span data-ttu-id="ee161-335">Bu hizmet, bir TLS oturumunun yerel deposuna başlatılmış bir NX_SECURE_X509_CERT yapısı örneği ekler.</span><span class="sxs-lookup"><span data-stu-id="ee161-335">This service adds an initialized NX_SECURE_X509_CERT structure instance to the local store of a TLS session.</span></span> <span data-ttu-id="ee161-336">Bu sertifika, TLS el sıkışması sırasında (nx_secure_x509_certificate_initialize kullanarak sertifika yapısının başlatılması sırasında kimlik sertifikası olarak işaretlenmişse) veya TLS el sıkışma sırasında uzak ana bilgisayara sağlanmış bir Sertifika zincirinin parçası olarak bir veren olarak, TLS yığını tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ee161-336">This certificate may used by the TLS stack to identify the device during the TLS handshake (if it was marked as an identity certificate during initialization of the certificate structure using nx_secure_x509_certificate_initialize), or as an issuer as part of a certificate chain provided to the remote host during the TLS handshake.</span></span>

<span data-ttu-id="ee161-337">Aynı ortak ada sahip birden çok yerel sertifika gerekiyorsa, Sertifikalar *nx_secure_tls_server_certificate_add* hizmeti kullanılarak eklenebilir (aşağıdaki uyarıya bakın).</span><span class="sxs-lookup"><span data-stu-id="ee161-337">If multiple local certificates with the same Common Name are needed, certificates may be added using the *nx_secure_tls_server_certificate_add* service (see warning below).</span></span>

<span data-ttu-id="ee161-338">TLS sunucu modu için bir sertifika **gereklidir** .</span><span class="sxs-lookup"><span data-stu-id="ee161-338">A certificate is **required** for TLS Server mode.</span></span>

<span data-ttu-id="ee161-339">Bir sertifika, TLS Istemci modu için *isteğe bağlıdır* .</span><span class="sxs-lookup"><span data-stu-id="ee161-339">A certificate is *optional* for TLS Client mode.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ee161-340">*Bu API, nx_secure_tls_server_certificate_add kullanırken aynı TLS oturumuyla kullanılmamalıdır. Sunucu sertifikası API 'SI her sertifika için benzersiz bir sayısal tanımlayıcı kullanır ve X. 509.440 ortak adına göre dizinleri nx_secure_tls_local_certificate_add. Yerel Sertifika Hizmetleri, yalnızca tek bir kimlik sertifikası kullanan uygulamalar için sayısal tanımlayıcıya uygun bir alternatif sağlar: ortak adı kullanarak, uygulamanın sayısal tanımlayıcıları izlememek zorunda olmaması gerekir.*</span><span class="sxs-lookup"><span data-stu-id="ee161-340">*This API should not be used with the same TLS session when using nx_secure_tls_server_certificate_add. The server certificate API uses a unique numeric identifier for each certificate, and nx_secure_tls_local_certificate_add indexes based on the X.509 Common Name. The local certificate services provide a convenient alternative to the numeric identifier for applications that use only a single identity certificate – by using the Common Name, the application need not keep track of numeric identifiers.*</span></span>

### <a name="parameters"></a><span data-ttu-id="ee161-341">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ee161-341">Parameters</span></span>

- <span data-ttu-id="ee161-342">**session_ptr** Daha önce oluşturulmuş bir TLS oturum örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ee161-342">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="ee161-343">**certificate_ptr** Başlatılmış bir TLS sertifikası örneğinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-343">**certificate_ptr** Pointer to an initialized TLS Certificate instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="ee161-344">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ee161-344">Return Values</span></span>

- <span data-ttu-id="ee161-345">Sertifikanın başarılı bir şekilde eklenmesi **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="ee161-345">**NX_SUCCESS** (0x00) Successful addition of certificate.</span></span>
- <span data-ttu-id="ee161-346">**NX_INVALID_PARAMETERS** (0x4D) geçersiz veya yinelenen bir sertifika eklemeye çalıştı.</span><span class="sxs-lookup"><span data-stu-id="ee161-346">**NX_INVALID_PARAMETERS** (0x4D) Tried to add an invalid or duplicate certificate.</span></span>
- <span data-ttu-id="ee161-347">**NX_PTR_ERROR** (0x07) geçersiz TLS oturumu veya sertifika işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-347">**NX_PTR_ERROR** (0x07) Invalid TLS session or certificate pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ee161-348">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ee161-348">Allowed From</span></span>

<span data-ttu-id="ee161-349">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ee161-349">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ee161-350">Örnek</span><span class="sxs-lookup"><span data-stu-id="ee161-350">Example</span></span>

```C
/* Initialize certificate structure. */
status =  nx_secure_x509_certificate_initialize(&certificate, certificate_data,
500, private_key, 64);

/* Add certificate to TLS session.  */
status =  nx_secure_tls_local_certificate_add(&tls_session, &certificate);


/* If status is NX_SUCCESS the certificate was successfully added.  */
```

### <a name="see-also"></a><span data-ttu-id="ee161-351">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ee161-351">See Also</span></span>

- <span data-ttu-id="ee161-352">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="ee161-352">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="ee161-353">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="ee161-353">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="ee161-354">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="ee161-354">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="ee161-355">nx_secure_tls_local_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="ee161-355">nx_secure_tls_local_certificate_remove</span></span>
- <span data-ttu-id="ee161-356">nx_secure_tls_local_certificate_find</span><span class="sxs-lookup"><span data-stu-id="ee161-356">nx_secure_tls_local_certificate_find</span></span>

## <a name="nx_secure_tls_local_certificate_find"></a><span data-ttu-id="ee161-357">nx_secure_tls_local_certificate_find</span><span class="sxs-lookup"><span data-stu-id="ee161-357">nx_secure_tls_local_certificate_find</span></span>

<span data-ttu-id="ee161-358">Ortak ad ile bir NetX güvenli TLS oturumunda yerel bir sertifika bulun</span><span class="sxs-lookup"><span data-stu-id="ee161-358">Find a local certificate in a NetX Secure TLS Session by Common Name</span></span>

### <a name="prototype"></a><span data-ttu-id="ee161-359">Prototype</span><span class="sxs-lookup"><span data-stu-id="ee161-359">Prototype</span></span>

```C
UINT  nx_secure_tls_local_certificate_find(NX_SECURE_TLS_SESSION
                        *session_ptr, NX_SECURE_X509_CERT
                        **certificate, UCHAR *common_name, UINT
                        name_length);
```

### <a name="description"></a><span data-ttu-id="ee161-360">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-360">Description</span></span>

<span data-ttu-id="ee161-361">Bu hizmet, bir TLS oturumunun yerel cihaz sertifika deposundaki bir sertifikayı bulur ve depodaki NX_SECURE_X509_CERT yapısına bir işaretçi döndürür.</span><span class="sxs-lookup"><span data-stu-id="ee161-361">This service finds a certificate in the local device certificate store of a TLS session and returns a pointer to the NX_SECURE_X509_CERT structure in the store.</span></span> <span data-ttu-id="ee161-362">Common_name parametresi ve uzunluğu (name_length), sertifikanın X. 509.440 konusunun ortak ad alanıyla eşleşen sertifikayı tanımlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ee161-362">The common_name parameter and it's length (name_length) are used to identify the certificate in the store by matching the certificate's X.509 Subject Common Name field.</span></span>

<span data-ttu-id="ee161-363">Aynı ortak ada sahip birden fazla sertifika varsa, yalnızca ilki döndürülür – bunun yerine *nx_secure_tls_server_certificate_find* kullanın.</span><span class="sxs-lookup"><span data-stu-id="ee161-363">If more than one certificate with the same Common Name is present, only the first one will be returned – use *nx_secure_tls_server_certificate_find* instead.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ee161-364">*Bu API, nx_secure_tls_server_certificate_add kullanırken aynı TLS oturumuyla kullanılmamalıdır. Sunucu sertifikası API 'SI her sertifika için benzersiz bir sayısal tanımlayıcı kullanır ve X. 509.440 ortak adına göre dizinleri nx_secure_tls_local_certificate_add. Yerel Sertifika Hizmetleri, yalnızca tek bir kimlik sertifikası kullanan uygulamalar için sayısal tanımlayıcıya uygun bir alternatif sağlar: ortak adı kullanarak, uygulamanın sayısal tanımlayıcıları izlememek zorunda olmaması gerekir.*</span><span class="sxs-lookup"><span data-stu-id="ee161-364">*This API should not be used with the same TLS session when using nx_secure_tls_server_certificate_add. The server certificate API uses a unique numeric identifier for each certificate, and nx_secure_tls_local_certificate_add indexes based on the X.509 Common Name. The local certificate services provide a convenient alternative to the numeric identifier for applications that use only a single identity certificate – by using the Common Name, the application need not keep track of numeric identifiers.*</span></span>

### <a name="parameters"></a><span data-ttu-id="ee161-365">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ee161-365">Parameters</span></span>

- <span data-ttu-id="ee161-366">**session_ptr** Daha önce oluşturulmuş bir TLS oturum örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ee161-366">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="ee161-367">**sertifika** Eşleşen sertifikaya yönelik Işaretçiyi döndürün.</span><span class="sxs-lookup"><span data-stu-id="ee161-367">**certificate** Return Pointer to matched certificate.</span></span>
- <span data-ttu-id="ee161-368">**common_name** Eşleştirilecek ortak ad dizesi (DNS adı).</span><span class="sxs-lookup"><span data-stu-id="ee161-368">**common_name** Common Name string to match (DNS name).</span></span>
- <span data-ttu-id="ee161-369">**name_length** Common_name dize verisinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="ee161-369">**name_length** Length of common_name string data.</span></span>

### <a name="return-values"></a><span data-ttu-id="ee161-370">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ee161-370">Return Values</span></span>

- <span data-ttu-id="ee161-371">"Certificate" parametresinde **NX_SUCCESS** (0x00) sertifikası bulundu ve işaretçi döndürüldü.</span><span class="sxs-lookup"><span data-stu-id="ee161-371">**NX_SUCCESS** (0x00) Certificate was found and pointer returned in "certificate" parameter.</span></span>
- <span data-ttu-id="ee161-372">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) sağlanan ortak ada sahip bir sertifika bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="ee161-372">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) No certificate with the supplied Common Name was found.</span></span>
- <span data-ttu-id="ee161-373">**NX_PTR_ERROR** (0x07) geçersiz TLS oturumu, sertifika işaretçisi veya ortak ad dizesi.</span><span class="sxs-lookup"><span data-stu-id="ee161-373">**NX_PTR_ERROR** (0x07) Invalid TLS session, certificate pointer, or common name string.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ee161-374">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ee161-374">Allowed From</span></span>

<span data-ttu-id="ee161-375">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ee161-375">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ee161-376">Örnek</span><span class="sxs-lookup"><span data-stu-id="ee161-376">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="ee161-377">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ee161-377">See Also</span></span>

- <span data-ttu-id="ee161-378">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="ee161-378">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="ee161-379">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="ee161-379">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="ee161-380">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="ee161-380">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="ee161-381">nx_secure_tls_local_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="ee161-381">nx_secure_tls_local_certificate_remove</span></span>
- <span data-ttu-id="ee161-382">nx_secure_tls_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="ee161-382">nx_secure_tls_local_certificate_add</span></span>

## <a name="nx_secure_tls_local_certificate_remove"></a><span data-ttu-id="ee161-383">nx_secure_tls_local_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="ee161-383">nx_secure_tls_local_certificate_remove</span></span>

<span data-ttu-id="ee161-384">Yerel sertifikayı NetX güvenli TLS oturumundan kaldır</span><span class="sxs-lookup"><span data-stu-id="ee161-384">Remove local certificate from NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="ee161-385">Prototype</span><span class="sxs-lookup"><span data-stu-id="ee161-385">Prototype</span></span>

```C
UINT  nx_secure_tls_local_certificate_remove(NX_SECURE_TLS_SESSION
                  *session_ptr, UCHAR *common_name, UINT
                  common_name_length);
```

### <a name="description"></a><span data-ttu-id="ee161-386">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-386">Description</span></span>

<span data-ttu-id="ee161-387">Bu hizmet, sertifikadaki ortak ad alanına girilen bir TLS oturumundan yerel sertifika örneğini kaldırır.</span><span class="sxs-lookup"><span data-stu-id="ee161-387">This service removes a local certificate instance from a TLS session, keyed on the Common Name field in the certificate.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ee161-388">*Bu API, nx_secure_tls_server_certificate_add kullanırken aynı TLS oturumuyla kullanılmamalıdır. Sunucu sertifikası API 'SI her sertifika için benzersiz bir sayısal tanımlayıcı kullanır ve X. 509.440 ortak adına göre dizinleri nx_secure_tls_local_certificate_add. Yerel Sertifika Hizmetleri, yalnızca tek bir kimlik sertifikası kullanan uygulamalar için sayısal tanımlayıcıya uygun bir alternatif sağlar: ortak adı kullanarak, uygulamanın sayısal tanımlayıcıları izlememek zorunda olmaması gerekir.*</span><span class="sxs-lookup"><span data-stu-id="ee161-388">*This API should not be used with the same TLS session when using nx_secure_tls_server_certificate_add. The server certificate API uses a unique numeric identifier for each certificate, and nx_secure_tls_local_certificate_add indexes based on the X.509 Common Name. The local certificate services provide a convenient alternative to the numeric identifier for applications that use only a single identity certificate – by using the Common Name, the application need not keep track of numeric identifiers.*</span></span>

### <a name="parameters"></a><span data-ttu-id="ee161-389">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ee161-389">Parameters</span></span>

- <span data-ttu-id="ee161-390">**session_ptr** Daha önce oluşturulmuş bir TLS oturum örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ee161-390">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="ee161-391">**common_name** Kaldırılacak sertifikanın ortak ad değeri.</span><span class="sxs-lookup"><span data-stu-id="ee161-391">**common_name** The Common Name value of the certificate to be removed.</span></span>
- <span data-ttu-id="ee161-392">**common_name_length** Ortak ad dizesinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="ee161-392">**common_name_length** The length of the Common Name string.</span></span>

### <a name="return-values"></a><span data-ttu-id="ee161-393">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ee161-393">Return Values</span></span>

- <span data-ttu-id="ee161-394">Sertifikanın başarılı bir şekilde eklenmesi **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="ee161-394">**NX_SUCCESS** (0x00) Successful addition of certificate.</span></span>
- <span data-ttu-id="ee161-395">**NX_PTR_ERROR** (0x07) geçersiz TLS oturum işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-395">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>
- <span data-ttu-id="ee161-396">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) sertifikası bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="ee161-396">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) Certificate was not found.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ee161-397">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ee161-397">Allowed From</span></span>

<span data-ttu-id="ee161-398">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ee161-398">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ee161-399">Örnek</span><span class="sxs-lookup"><span data-stu-id="ee161-399">Example</span></span>

```C
/* Add certificate to TLS session.  */
status =  nx_secure_tls_local_certificate_remove(&tls_session,
                                                “www.example.com”, 15);


/* If status is NX_SUCCESS the certificate was successfully removed.  */
```

### <a name="see-also"></a><span data-ttu-id="ee161-400">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ee161-400">See Also</span></span>

- <span data-ttu-id="ee161-401">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="ee161-401">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="ee161-402">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="ee161-402">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="ee161-403">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="ee161-403">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="ee161-404">nx_secure_tls_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="ee161-404">nx_secure_tls_local_certificate_add</span></span>

## <a name="nx_secure_tls_metadata_size_calculate"></a><span data-ttu-id="ee161-405">nx_secure_tls_metadata_size_calculate</span><span class="sxs-lookup"><span data-stu-id="ee161-405">nx_secure_tls_metadata_size_calculate</span></span>

<span data-ttu-id="ee161-406">NetX güvenli TLS oturumunun şifreleme meta verilerinin boyutunu hesaplama</span><span class="sxs-lookup"><span data-stu-id="ee161-406">Calculate size of cryptographic metadata for a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="ee161-407">Prototype</span><span class="sxs-lookup"><span data-stu-id="ee161-407">Prototype</span></span>

```C
UINT  nx_secure_tls_metadata_size_calculate(
                        const NX_SECURE_TLS_CRYPTO *crypto_table,
                        ULONG *metadata_size);
```

### <a name="description"></a><span data-ttu-id="ee161-408">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-408">Description</span></span>

<span data-ttu-id="ee161-409">Bu hizmet, belirli bir TLS oturumu ve TLS şifreleme tablosu için gereken şifreleme meta verilerinin boyutunu hesaplar ve döndürür (şifreleme şifresi tablosu hakkında daha fazla bilgi için "şifreleme yöntemleriyle TLS başlatılıyor" bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="ee161-409">This service calculates and returns the size of the cryptographic metadata needed for a particular TLS session and TLS cryptography table (see the section "Initializing TLS with Cryptographic Methods" for more information on the cryptographic cipher table).</span></span>

<span data-ttu-id="ee161-410">Bu hizmet, nx_secure_tls_session_create iletilen meta veri arabelleğinin boyutunu hesaplamak için istenen şifreleme tablosuyla çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ee161-410">This service should be called with the desired cryptographic table to calculate the size of the metadata buffer passed into nx_secure_tls_session_create.</span></span>

### <a name="parameters"></a><span data-ttu-id="ee161-411">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ee161-411">Parameters</span></span>

- <span data-ttu-id="ee161-412">**crypto_table** Tüm NetX güvenli TLS şifreleme tablosuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ee161-412">**crypto_table** Pointer to a complete NetX Secure TLS cryptography table.</span></span>
- <span data-ttu-id="ee161-413">**metadata_size** Bayt cinsinden boyut hesaplamasının çıktısı.</span><span class="sxs-lookup"><span data-stu-id="ee161-413">**metadata_size** The output of the size calculation in bytes.</span></span>

### <a name="return-values"></a><span data-ttu-id="ee161-414">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ee161-414">Return Values</span></span>

- <span data-ttu-id="ee161-415">**NX_SUCCESS** (0x00) meta veri boyutunun başarıyla hesaplanması.</span><span class="sxs-lookup"><span data-stu-id="ee161-415">**NX_SUCCESS** (0x00) Successful calculation of metadata size.</span></span>
- <span data-ttu-id="ee161-416">**NX_PTR_ERROR** (0x07) geçersiz şifre tablosu veya dönüş boyutu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-416">**NX_PTR_ERROR** (0x07) Invalid crypto table or return size pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ee161-417">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ee161-417">Allowed From</span></span>

<span data-ttu-id="ee161-418">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ee161-418">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ee161-419">Örnek</span><span class="sxs-lookup"><span data-stu-id="ee161-419">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="ee161-420">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ee161-420">See Also</span></span>

- <span data-ttu-id="ee161-421">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="ee161-421">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_module_hash_compute"></a><span data-ttu-id="ee161-422">nx_secure_module_hash_compute</span><span class="sxs-lookup"><span data-stu-id="ee161-422">nx_secure_module_hash_compute</span></span>

<span data-ttu-id="ee161-423">NetX güvenli kitaplık yordamlarının karma değerini hesaplama</span><span class="sxs-lookup"><span data-stu-id="ee161-423">Compute the hash value of the NetX Secure library routines</span></span>

### <a name="prototype"></a><span data-ttu-id="ee161-424">Prototype</span><span class="sxs-lookup"><span data-stu-id="ee161-424">Prototype</span></span>

```C
VOID nx_secure_module_hash_compute(VOID);
```

### <a name="description"></a><span data-ttu-id="ee161-425">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-425">Description</span></span>

<span data-ttu-id="ee161-426">Bu hizmet NetX güvenli TLS modülünü başlatır.</span><span class="sxs-lookup"><span data-stu-id="ee161-426">This service initializes the NetX Secure TLS module.</span></span> <span data-ttu-id="ee161-427">Diğer NetX güvenli hizmetlere erişilebilmesi için önce bu adı çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ee161-427">It must be called before other NetX Secure services can be accessed.</span></span>

### <a name="parameters"></a><span data-ttu-id="ee161-428">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ee161-428">Parameters</span></span>

<span data-ttu-id="ee161-429">Hiçbiri</span><span class="sxs-lookup"><span data-stu-id="ee161-429">None</span></span>

### <a name="return-values"></a><span data-ttu-id="ee161-430">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ee161-430">Return Values</span></span>

<span data-ttu-id="ee161-431">Yok</span><span class="sxs-lookup"><span data-stu-id="ee161-431">None</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ee161-432">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ee161-432">Allowed From</span></span>

<span data-ttu-id="ee161-433">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ee161-433">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="ee161-434">Örnek</span><span class="sxs-lookup"><span data-stu-id="ee161-434">Example</span></span>

```C
/* Initializes the TLS module. */
Nx_secure_tls_initialize();
```

### <a name="see-also"></a><span data-ttu-id="ee161-435">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ee161-435">See Also</span></span>

- <span data-ttu-id="ee161-436">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="ee161-436">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_packet_allocate"></a><span data-ttu-id="ee161-437">nx_secure_tls_packet_allocate</span><span class="sxs-lookup"><span data-stu-id="ee161-437">nx_secure_tls_packet_allocate</span></span>

<span data-ttu-id="ee161-438">NetX güvenli TLS oturumu için bir paket ayırın</span><span class="sxs-lookup"><span data-stu-id="ee161-438">Allocate a packet for a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="ee161-439">Prototype</span><span class="sxs-lookup"><span data-stu-id="ee161-439">Prototype</span></span>

```C
UINT  nx_secure_tls_packet_allocate(NX_SECURE_TLS_SESSION *session_ptr,
                                    NX_PACKET_POOL *pool_ptr,
                                    NX_PACKET **packet_ptr,
                                    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="ee161-440">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-440">Description</span></span>

<span data-ttu-id="ee161-441">Bu hizmet, belirtilen NX_PACKET_POOL belirtilen etkin TLS oturumu için bir NX_PACKET ayırır.</span><span class="sxs-lookup"><span data-stu-id="ee161-441">This service allocates an NX_PACKET for the specified active TLS session from the specified NX_PACKET_POOL.</span></span> <span data-ttu-id="ee161-442">Bu hizmet, bir TLS bağlantısı üzerinden gönderilecek veri paketleri ayırmak için uygulama tarafından çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ee161-442">This service should be called by the application to allocate data packets to be sent over a TLS connection.</span></span> <span data-ttu-id="ee161-443">Bu hizmet çağrılmadan önce TLS oturumunun başlatılmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ee161-443">The TLS session must be initialized before calling this service.</span></span>

<span data-ttu-id="ee161-444">Ayrılan paket, paket verileri doldurulduktan sonra TLS üstbilgi ve altbilgi verilerinin eklenebilmesi için düzgün şekilde başlatılmış olur.</span><span class="sxs-lookup"><span data-stu-id="ee161-444">The allocated packet is properly initialized so that TLS header and footer data may be added after the packet data is populated.</span></span> <span data-ttu-id="ee161-445">Davranış, *nx_packet_allocate* benzer şekilde benzerdir.</span><span class="sxs-lookup"><span data-stu-id="ee161-445">The behavior is otherwise identical to *nx_packet_allocate*.</span></span>

### <a name="parameters"></a><span data-ttu-id="ee161-446">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ee161-446">Parameters</span></span>

- <span data-ttu-id="ee161-447">**session_ptr** Bir TLS oturum örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-447">**session_ptr** Pointer to a TLS Session instance.</span></span>
- <span data-ttu-id="ee161-448">**pool_ptr** Paketin ayırabileceği bir NX_PACKET_POOL işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-448">**pool_ptr** Pointer to an NX_PACKET_POOL from which to allocate the packet.</span></span>
- <span data-ttu-id="ee161-449">**packet_ptr** Yeni ayrılmış pakete çıkış işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-449">**packet_ptr** Output pointer to the newly-allocated packet.</span></span>
- <span data-ttu-id="ee161-450">**wait_option** Paket ayırması için askıya alma seçeneği.</span><span class="sxs-lookup"><span data-stu-id="ee161-450">**wait_option** Suspension option for packet allocation.</span></span>

### <a name="return-values"></a><span data-ttu-id="ee161-451">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ee161-451">Return Values</span></span>

- <span data-ttu-id="ee161-452">**NX_SUCCESS** (0x00) başarılı paket ayırması.</span><span class="sxs-lookup"><span data-stu-id="ee161-452">**NX_SUCCESS** (0x00) Successful packet allocate.</span></span>
- <span data-ttu-id="ee161-453">**NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) temel alınan paket ayırması başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="ee161-453">**NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) Underlying packet allocation failed.</span></span>
- <span data-ttu-id="ee161-454">**NX_SECURE_TLS_SESSION_UNINITIALIZED** (0x101) sağlanan TLS oturumu başlatılmadı.</span><span class="sxs-lookup"><span data-stu-id="ee161-454">**NX_SECURE_TLS_SESSION_UNINITIALIZED** (0x101) The supplied TLS session was not initialized.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ee161-455">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ee161-455">Allowed From</span></span>

<span data-ttu-id="ee161-456">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ee161-456">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ee161-457">Örnek</span><span class="sxs-lookup"><span data-stu-id="ee161-457">Example</span></span>

```C
/* Allocate a new TLS packet from the previously created packet pool and
previously initialized TLS session.   */

status = nx_secure_tls_packet_allocate(&tls_session, &pool_0, &packet_ptr,
                                       NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the newly allocated packet pointer is found in the
variable packet_ptr.  */
```

### <a name="see-also"></a><span data-ttu-id="ee161-458">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ee161-458">See Also</span></span>

- <span data-ttu-id="ee161-459">nx_tcp_socket_receive</span><span class="sxs-lookup"><span data-stu-id="ee161-459">nx_tcp_socket_receive</span></span>
- <span data-ttu-id="ee161-460">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="ee161-460">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="ee161-461">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="ee161-461">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="ee161-462">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="ee161-462">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="ee161-463">nx_secure_tls_session_delete</span><span class="sxs-lookup"><span data-stu-id="ee161-463">nx_secure_tls_session_delete</span></span>
- <span data-ttu-id="ee161-464">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="ee161-464">nx_secure_tls_session_receive</span></span>
- <span data-ttu-id="ee161-465">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="ee161-465">nx_secure_tls_session_send</span></span>
- <span data-ttu-id="ee161-466">nx_secure_tls_session_end</span><span class="sxs-lookup"><span data-stu-id="ee161-466">nx_secure_tls_session_end</span></span>
- <span data-ttu-id="ee161-467">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="ee161-467">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_psk_add"></a><span data-ttu-id="ee161-468">nx_secure_tls_psk_add</span><span class="sxs-lookup"><span data-stu-id="ee161-468">nx_secure_tls_psk_add</span></span>

<span data-ttu-id="ee161-469">NetX güvenli TLS oturumuna önceden paylaşılan anahtar ekleme</span><span class="sxs-lookup"><span data-stu-id="ee161-469">Add a Pre-Shared Key to a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="ee161-470">Prototype</span><span class="sxs-lookup"><span data-stu-id="ee161-470">Prototype</span></span>

```C
UINT  nx_secure_tls_psk_add(NX_SECURE_TLS_SESSION *session_ptr,
                            UCHAR *pre_shared_key, UINT psk_length,
                            UCHAR *psk_identity, UINT
                            identity_length, UCHAR *hint, UINT
                            hint_length);
```

### <a name="description"></a><span data-ttu-id="ee161-471">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-471">Description</span></span>

<span data-ttu-id="ee161-472">Bu hizmet, bir TLS oturum denetim bloğuna önceden paylaşılan anahtar (PSK), kimlik dizesi ve kimlik ipucu ekler.</span><span class="sxs-lookup"><span data-stu-id="ee161-472">This service adds a Pre-Shared Key (PSK), its identity string, and an identity hint to a TLS Session control block.</span></span> <span data-ttu-id="ee161-473">PSK ciphersuites etkin ve kullanıldığında, bir dijital sertifika yerine PSK kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ee161-473">The PSK is used in place of a digital certificate when PSK ciphersuites are enabled and used.</span></span>

### <a name="parameters"></a><span data-ttu-id="ee161-474">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ee161-474">Parameters</span></span>

- <span data-ttu-id="ee161-475">**session_ptr** Daha önce oluşturulmuş bir TLS oturum örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ee161-475">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="ee161-476">**pre_shared_key** Gerçek PSK değeri.</span><span class="sxs-lookup"><span data-stu-id="ee161-476">**pre_shared_key** The actual PSK value.</span></span>
- <span data-ttu-id="ee161-477">**psk_length** PSK değeri uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="ee161-477">**psk_length** The length of the PSK value.</span></span>
- <span data-ttu-id="ee161-478">**psk_identity** Bu PSK değerini tanımlamak için kullanılan dize.</span><span class="sxs-lookup"><span data-stu-id="ee161-478">**psk_identity** A string used to identify this PSK value.</span></span>
- <span data-ttu-id="ee161-479">**identity_length** PSK kimliğinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="ee161-479">**identity_length** The length of the PSK identity.</span></span>
- <span data-ttu-id="ee161-480">**İpucu** Bir TLS sunucusunda hangi sayıda PSKs arasından seçim yapmak gerektiğini göstermek için kullanılan dize.</span><span class="sxs-lookup"><span data-stu-id="ee161-480">**hint** A string used to indicate which group of PSKs to choose from on a TLS server.</span></span>
- <span data-ttu-id="ee161-481">**hint_length** İpucu dizesinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="ee161-481">**hint_length** The length of the hint string.</span></span>

### <a name="return-values"></a><span data-ttu-id="ee161-482">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ee161-482">Return Values</span></span>

- <span data-ttu-id="ee161-483">**NX_SUCCESS** (0x00) PSK 'nin başarılı bir şekilde eklenmesi.</span><span class="sxs-lookup"><span data-stu-id="ee161-483">**NX_SUCCESS** (0x00) Successful addition of PSK.</span></span>
- <span data-ttu-id="ee161-484">**NX_PTR_ERROR** (0x07) geçersiz TLS oturum işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-484">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>
- <span data-ttu-id="ee161-485">**NX_SECURE_TLS_NO_MORE_PSK_SPACE** (0x125) başka bir PSK eklenemiyor.</span><span class="sxs-lookup"><span data-stu-id="ee161-485">**NX_SECURE_TLS_NO_MORE_PSK_SPACE** (0x125)  Cannot add another PSK.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ee161-486">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ee161-486">Allowed From</span></span>

<span data-ttu-id="ee161-487">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ee161-487">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ee161-488">Örnek</span><span class="sxs-lookup"><span data-stu-id="ee161-488">Example</span></span>

```C
/* PSK value.  */
UCHAR psk[] = { 0x1a, 0x2b, 0x3c, 0x4d };

/* Add PSK to TLS session.  */
status =  nx_secure_tls_psk_add(&tls_session, psk, sizeof(psk), “psk_1”, 4,
“Client_identity”, 15);


/* If status is NX_SUCCESS the PSK was successfully added.  */
```

### <a name="see-also"></a><span data-ttu-id="ee161-489">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ee161-489">See Also</span></span>

- <span data-ttu-id="ee161-490">nx_secure_tls_client_psk_set</span><span class="sxs-lookup"><span data-stu-id="ee161-490">nx_secure_tls_client_psk_set</span></span>
- <span data-ttu-id="ee161-491">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="ee161-491">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="ee161-492">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="ee161-492">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="ee161-493">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="ee161-493">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="ee161-494">nx_secure_tls_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="ee161-494">nx_secure_tls_local_certificate_add</span></span>

## <a name="nx_secure_tls_remote_certificate_allocate"></a><span data-ttu-id="ee161-495">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="ee161-495">nx_secure_tls_remote_certificate_allocate</span></span>

<span data-ttu-id="ee161-496">Uzak bir TLS ana bilgisayarı tarafından belirtilen sertifika için alan ayır</span><span class="sxs-lookup"><span data-stu-id="ee161-496">Allocate space for the certificate provided by a remote TLS host</span></span>

### <a name="prototype"></a><span data-ttu-id="ee161-497">Prototype</span><span class="sxs-lookup"><span data-stu-id="ee161-497">Prototype</span></span>

```C
UINT  nx_secure_tls_remote_certificate_allocate(
                 NX_SECURE_TLS_SESSION *session_ptr,
                 NX_SECURE_X509_CERT *certificate_ptr,
                 UCHAR *raw_certificate_buffer,
                 UINT raw_buffer_size);
```

### <a name="description"></a><span data-ttu-id="ee161-498">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-498">Description</span></span>

<span data-ttu-id="ee161-499">Bu hizmet, bir TLS oturumu sırasında uzak bir ana bilgisayar tarafından sunulan sertifikalara alan ayırma amacıyla bir TLS oturumuna başlatılmamış bir NX_SECURE_X509_CERT yapısı örneği ekler.</span><span class="sxs-lookup"><span data-stu-id="ee161-499">This service adds an uninitialized NX_SECURE_X509_CERT structure instance to a TLS session for the purpose of allocating space for certificates provided by a remote host during a TLS session.</span></span> <span data-ttu-id="ee161-500">Uzak sertifika verileri NetX güvenli TLS tarafından ayrıştırılır ve bu işleve sunulan sertifika yapısı örneğini doldurmak için bu bilgiler kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ee161-500">The remote certificate data is parsed by NetX Secure TLS and that information is used to populate the certificate structure instance provided to this function.</span></span> <span data-ttu-id="ee161-501">Bu şekilde eklenen sertifikalar, bağlantılı bir listeye yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="ee161-501">Certificates added in this manner are placed in a linked list.</span></span>

<span data-ttu-id="ee161-502">Uzak konağın birden çok sertifika sağlayabilmesi bekleniyorsa, tüm sertifikalar için alan ayırmak üzere bu işlevin tekrar tekrar çağrılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ee161-502">If it is expected that the remote host will provide multiple certificates, this function should be called repeatedly to allocate space for all certificates.</span></span> <span data-ttu-id="ee161-503">Ek sertifikalar, sertifika bağlantılı listesinin sonuna eklenir.</span><span class="sxs-lookup"><span data-stu-id="ee161-503">The additional certificates are added to the end of the certificate linked list.</span></span>

<span data-ttu-id="ee161-504">Bir uzak sertifika ayrılmaması, önceden paylaşılan anahtar (PSK) ciphersuite kullanımda olmadığı takdirde TLS el sıkışması sırasında TLS Istemci modunun başarısız olmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="ee161-504">Failure to allocate a remote certificate will cause TLS Client mode to fail during the TLS handshake unless a Pre-Shared Key (PSK) ciphersuite is in use.</span></span>

<span data-ttu-id="ee161-505">*Raw_certificate_buffer* parametresi, gelen uzak sertifikayı depolamak için ayrılan alana işaret eder.</span><span class="sxs-lookup"><span data-stu-id="ee161-505">The *raw_certificate_buffer* parameter points to space allocated to store the incoming remote certificate.</span></span> <span data-ttu-id="ee161-506">İmzalar için SHA-256 kullanan 2048 bitin RSA anahtarlarına sahip tipik sertifikalar, 1000-2000 bayt aralığındadır.</span><span class="sxs-lookup"><span data-stu-id="ee161-506">Typical certificates with RSA keys of 2048 bits using SHA-256 for signatures are in the range of 1000-2000 bytes.</span></span> <span data-ttu-id="ee161-507">Arabellek en az bu boyutu tutabilecek kadar büyük olmalıdır, ancak uzak ana bilgisayar sertifikalarına bağlı olarak, önemli ölçüde daha küçük veya daha büyük olabilir.</span><span class="sxs-lookup"><span data-stu-id="ee161-507">The buffer should be large enough to at least hold that size, but depending on the remote host certificates may be significantly smaller or larger.</span></span> <span data-ttu-id="ee161-508">Arabellek gelen sertifikayı tutmak için çok küçük olduğunda, TLS el sıkışması bir hatayla sona erdirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ee161-508">Note that if the buffer is too small to hold the incoming certificate, the TLS handshake will end with an error.</span></span>

<span data-ttu-id="ee161-509">TLS sunucu modu için, yalnızca istemci sertifikası kimlik doğrulaması etkinse bir uzak sertifika ayırması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ee161-509">For TLS Server mode, a remote certificate allocation is needed only if client certificate authentication is enabled.</span></span>

### <a name="parameters"></a><span data-ttu-id="ee161-510">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ee161-510">Parameters</span></span>

- <span data-ttu-id="ee161-511">**session_ptr** Daha önce oluşturulmuş bir TLS oturum örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ee161-511">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="ee161-512">**certificate_ptr** Başlatılmamış X. 509.440 sertifika örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ee161-512">**certificate_ptr** Pointer to an uninitialized X.509 Certificate instance.</span></span>
- <span data-ttu-id="ee161-513">**raw_certificate_buffer** Uzak ana bilgisayardan alınan ayrıştırılmamış sertifikayı tutan bir arabellek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-513">**raw_certificate_buffer** Pointer to a buffer to hold the un-parsed certificate received from the remote host.</span></span>
- <span data-ttu-id="ee161-514">**raw_buffer_size** Ham sertifika arabelleğinin boyutu.</span><span class="sxs-lookup"><span data-stu-id="ee161-514">**raw_buffer_size** Size of the raw certificate buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="ee161-515">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ee161-515">Return Values</span></span>

- <span data-ttu-id="ee161-516">**NX_SUCCESS** (0x00) sertifikanın başarıyla ayrılması.</span><span class="sxs-lookup"><span data-stu-id="ee161-516">**NX_SUCCESS** (0x00) Successful allocation of certificate.</span></span>
- <span data-ttu-id="ee161-517">**NX_PTR_ERROR** (0x07) geçersiz TLS oturum işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-517">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>
- <span data-ttu-id="ee161-518">**NX_SECURE_TLS_INSUFFICIENT_CERT_SPACE** (0x12D) sağlanan arabellek çok küçük.</span><span class="sxs-lookup"><span data-stu-id="ee161-518">**NX_SECURE_TLS_INSUFFICIENT_CERT_SPACE** (0x12D) The supplied buffer was too small.</span></span>
- <span data-ttu-id="ee161-519">**NX_INVALID_PARAMETERS** (0x4D) geçersiz bir sertifika eklemeye çalıştı.</span><span class="sxs-lookup"><span data-stu-id="ee161-519">**NX_INVALID_PARAMETERS** (0x4D) Tried to add an invalid certificate.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ee161-520">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ee161-520">Allowed From</span></span>

<span data-ttu-id="ee161-521">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ee161-521">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ee161-522">Örnek</span><span class="sxs-lookup"><span data-stu-id="ee161-522">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="ee161-523">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ee161-523">See Also</span></span>

- <span data-ttu-id="ee161-524">nx_secure_x509_certificate_initialize,</span><span class="sxs-lookup"><span data-stu-id="ee161-524">nx_secure_x509_certificate_initialize,</span></span>
- <span data-ttu-id="ee161-525">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="ee161-525">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_remote_certificate_buffer_allocate"></a><span data-ttu-id="ee161-526">nx_secure_tls_remote_certificate_buffer_allocate</span><span class="sxs-lookup"><span data-stu-id="ee161-526">nx_secure_tls_remote_certificate_buffer_allocate</span></span>

<span data-ttu-id="ee161-527">Uzak bir TLS ana bilgisayarı tarafından belirtilen tüm sertifikalar için alan ayır</span><span class="sxs-lookup"><span data-stu-id="ee161-527">Allocate space for all certificates provided by a remote TLS host</span></span>

### <a name="prototype"></a><span data-ttu-id="ee161-528">Prototype</span><span class="sxs-lookup"><span data-stu-id="ee161-528">Prototype</span></span>

```C
UINT  nx_secure_tls_remote_certificate_buffer_allocate(
                  NX_SECURE_TLS_SESSION *session_ptr,
                  UINT certs_number, VOID *certificate_buffer,
                  ULONG buffer_size);
```

### <a name="description"></a><span data-ttu-id="ee161-529">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-529">Description</span></span>

<span data-ttu-id="ee161-530">Bu hizmet, bir TLS Istemci örneğinde X. 509.440 kimlik doğrulaması ve doğrulama gerçekleştirmek için uzak sunucu konaklarından gelen sertifika zincirlerini işlemek üzere alan ayırır.</span><span class="sxs-lookup"><span data-stu-id="ee161-530">This service allocates space to process incoming certificate chains from remote server hosts in order to perform X.509 authentication and verification in a TLS Client instance.</span></span> <span data-ttu-id="ee161-531">TLS sunucu modu için, uzak sertifika ayırma yalnızca Client X. 509.440 sertifikası kimlik doğrulaması etkinse gereklidir – TLS sunucu örnekleri için, bunun yerine hizmet *nx_secure_tls_session_x509_client_verify_configure* kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ee161-531">For TLS Server mode, remote certificate allocation is needed only if client X.509 certificate authentication is enabled – for TLS Server instances the service *nx_secure_tls_session_x509_client_verify_configure* should be used instead.</span></span>

<span data-ttu-id="ee161-532">Bir önceden paylaşılan anahtar (PSK) ciphersuite kullanımda değilse, uzak sertifikaları ayıramaması TLS Istemci modunun TLS el sıkışması sırasında başarısız olmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="ee161-532">Failure to allocate remote certificates will cause TLS Client mode to fail during the TLS handshake unless a Pre-Shared Key (PSK) ciphersuite is in use.</span></span>

<span data-ttu-id="ee161-533">*Certificate_buffer* parametresi, gelen uzak sertifikaları ve bu sertifikalar için gereken denetim bloklarını depolamak için ayrılan alana işaret eder.</span><span class="sxs-lookup"><span data-stu-id="ee161-533">The *certificate_buffer* parameter points to space allocated to store the incoming remote certificates and the control blocks needed for those certificates.</span></span> <span data-ttu-id="ee161-534">Arabellek, her sertifikaya verilen eşit bir bölüme sahip sertifika (*certs_number*) sayısına bölünür.</span><span class="sxs-lookup"><span data-stu-id="ee161-534">The buffer will be divided by the number of certificates (*certs_number*) with an equal portion given to each certificate.</span></span> <span data-ttu-id="ee161-535">*Buffer_size* parametresi arabelleğin boyutunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="ee161-535">The *buffer_size*  parameter indicates the size of the buffer.</span></span> <span data-ttu-id="ee161-536">Aşağıdaki formül ile, gereken alan bulunabilir:</span><span class="sxs-lookup"><span data-stu-id="ee161-536">The space needed can be found with the following formula:</span></span>

```C
buffer_size = (<expected max number of certificates in chain>) *
                 (sizeof(NX_SECURE_X509_CERT) + <max cert size>)
```

<span data-ttu-id="ee161-537">İmzalar için SHA-256 kullanan 2048 bitin RSA anahtarlarına sahip tipik sertifikalar, 1000-2000 bayt aralığındadır.</span><span class="sxs-lookup"><span data-stu-id="ee161-537">Typical certificates with RSA keys of 2048 bits using SHA-256 for signatures are in the range of 1000-2000 bytes.</span></span> <span data-ttu-id="ee161-538">Arabellek, her sertifika için en az sayıda tutmaya yetecek kadar büyük olmalıdır, ancak uzak ana bilgisayar sertifikalarına bağlı olarak, önemli ölçüde daha küçük veya daha büyük olabilir.</span><span class="sxs-lookup"><span data-stu-id="ee161-538">The buffer should be large enough to at least hold that size for each certificate, but depending on the remote host certificates may be significantly smaller or larger.</span></span> <span data-ttu-id="ee161-539">Arabellek gelen sertifikayı tutmak için çok küçük olduğunda, TLS el sıkışması bir hatayla sona erdirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ee161-539">Note that if the buffer is too small to hold the incoming certificate, the TLS handshake will end with an error.</span></span>

### <a name="parameters"></a><span data-ttu-id="ee161-540">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ee161-540">Parameters</span></span>

- <span data-ttu-id="ee161-541">**session_ptr** Daha önce oluşturulmuş bir TLS oturum örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ee161-541">**session_ptr** Pointer to a previously created TLS Session  instance.</span></span>
- <span data-ttu-id="ee161-542">**certs_number** Belirtilen arabellekten ayrılacak sertifika sayısı.</span><span class="sxs-lookup"><span data-stu-id="ee161-542">**certs_number** Number of certificates to allocate from the  provided buffer.</span></span>
- <span data-ttu-id="ee161-543">**certificate_buffer** Uzak bir ana bilgisayardan alınan sertifikaları tutan arabellek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-543">**certificate_buffer** Pointer to a buffer to hold certificates received  from a remote host.</span></span>
- <span data-ttu-id="ee161-544">**Buffer_size** Sertifika arabelleğinin boyutu.</span><span class="sxs-lookup"><span data-stu-id="ee161-544">**buffer_size** Size of the certificate buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="ee161-545">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ee161-545">Return Values</span></span>

- <span data-ttu-id="ee161-546">**NX_SUCCESS** (0x00) sertifikanın başarıyla ayrılması.</span><span class="sxs-lookup"><span data-stu-id="ee161-546">**NX_SUCCESS** (0x00) Successful allocation of certificate.</span></span>
- <span data-ttu-id="ee161-547">**NX_PTR_ERROR** (0x07) geçersiz TLS oturumu veya arabellek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-547">**NX_PTR_ERROR** (0x07) Invalid TLS session or buffer pointer.</span></span>
- <span data-ttu-id="ee161-548">**NX_SECURE_TLS_INSUFFICIENT_CERT_SPACE** (0x12D) sağlanan arabellek çok küçük.</span><span class="sxs-lookup"><span data-stu-id="ee161-548">**NX_SECURE_TLS_INSUFFICIENT_CERT_SPACE** (0x12D) The supplied buffer was too small.</span></span>
- <span data-ttu-id="ee161-549">**NX_INVALID_PARAMETERS** (0x4D) Arabellek istenen sayıda sertifikayı tutmak için çok küçük.</span><span class="sxs-lookup"><span data-stu-id="ee161-549">**NX_INVALID_PARAMETERS** (0x4D) The buffer was too small to hold  the desired number of certificates.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ee161-550">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ee161-550">Allowed From</span></span>

<span data-ttu-id="ee161-551">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ee161-551">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ee161-552">Örnek</span><span class="sxs-lookup"><span data-stu-id="ee161-552">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="ee161-553">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ee161-553">See Also</span></span>

- <span data-ttu-id="ee161-554">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="ee161-554">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="ee161-555">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="ee161-555">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_remote_certificate_free_all"></a><span data-ttu-id="ee161-556">nx_secure_tls_remote_certificate_free_all</span><span class="sxs-lookup"><span data-stu-id="ee161-556">nx_secure_tls_remote_certificate_free_all</span></span>

<span data-ttu-id="ee161-557">Gelen sertifikalar için ayrılan boş alan</span><span class="sxs-lookup"><span data-stu-id="ee161-557">Free space allocated for incoming certificates</span></span>

### <a name="prototype"></a><span data-ttu-id="ee161-558">Prototype</span><span class="sxs-lookup"><span data-stu-id="ee161-558">Prototype</span></span>

```C
UINT  nx_secure_tls_remote_certificate_free_all(
                  NX_SECURE_TLS_SESSION *session_ptr);
```

### <a name="description"></a><span data-ttu-id="ee161-559">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-559">Description</span></span>

<span data-ttu-id="ee161-560">Bu hizmet, belirli bir TLS oturumuna ayrılan tüm sertifika arabelleklerinin bu oturumu bu oturum boş sertifika alanına döndürerek nx_secure_tls_remote_certificate_allocated tarafından serbest bırakmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ee161-560">This service is used to free all of the certificate buffers allocated to a particular TLS Session by nx_secure_tls_remote_certificate_allocated by returning them to that session's free certificate space.</span></span> <span data-ttu-id="ee161-561">Bir uygulama, bir TLS oturum nesnesini silmeden yeniden kullanıyorsa ve nx_secure_tls_session_delete ve nx_secure_tls_session_create yeniden oluşturmadan bu gerekli olabilir.</span><span class="sxs-lookup"><span data-stu-id="ee161-561">This may be necessary if an application reuses a TLS session object without deleting it and recreating it with nx_secure_tls_session_delete and nx_secure_tls_session_create.</span></span>

<span data-ttu-id="ee161-562">Nx_secure_tls_session_end, çoğu uygulamanın bu hizmeti çağırması gerekmemesi için, TLS oturumu sıfırlandığında, uzak sertifika alanının otomatik olarak kurtarıldığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ee161-562">Note that the remote certificate space is recovered automatically when the TLS session is reset as happens in nx_secure_tls_session_end so most applications should not need to call this service.</span></span>

### <a name="parameters"></a><span data-ttu-id="ee161-563">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ee161-563">Parameters</span></span>

- <span data-ttu-id="ee161-564">**session_ptr** Daha önce oluşturulmuş bir TLS oturum örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ee161-564">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="ee161-565">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ee161-565">Return Values</span></span>

- <span data-ttu-id="ee161-566">**NX_SUCCESS** (0x00) başarılı işlemi.</span><span class="sxs-lookup"><span data-stu-id="ee161-566">**NX_SUCCESS** (0x00) Successful operation.</span></span>
- <span data-ttu-id="ee161-567">**NX_PTR_ERROR** (0x07) geçersiz TLS oturum işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-567">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>
- <span data-ttu-id="ee161-568">**NX_INVALID_PARAMETERS** (0x4D) iç hata – sertifika deposu muhtemelen bozuk.</span><span class="sxs-lookup"><span data-stu-id="ee161-568">**NX_INVALID_PARAMETERS** (0x4D) Internal error – certificate store likely corrupt.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ee161-569">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ee161-569">Allowed From</span></span>

<span data-ttu-id="ee161-570">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ee161-570">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ee161-571">Örnek</span><span class="sxs-lookup"><span data-stu-id="ee161-571">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="ee161-572">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ee161-572">See Also</span></span>

- <span data-ttu-id="ee161-573">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="ee161-573">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="ee161-574">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="ee161-574">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="ee161-575">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="ee161-575">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="ee161-576">nx_secure_tls_session_end</span><span class="sxs-lookup"><span data-stu-id="ee161-576">nx_secure_tls_session_end</span></span>

## <a name="nx_secure_tls_server_certificate_add"></a><span data-ttu-id="ee161-577">nx_secure_tls_server_certificate_add</span><span class="sxs-lookup"><span data-stu-id="ee161-577">nx_secure_tls_server_certificate_add</span></span>

<span data-ttu-id="ee161-578">Sayısal bir tanımlayıcı kullanarak TLS sunucuları için özel olarak bir sertifika ekleyin</span><span class="sxs-lookup"><span data-stu-id="ee161-578">Add a certificate specifically for TLS servers using a numeric identifier</span></span>

### <a name="prototype"></a><span data-ttu-id="ee161-579">Prototype</span><span class="sxs-lookup"><span data-stu-id="ee161-579">Prototype</span></span>

```C
UINT  nx_secure_tls_server_certificate_add(
                  NX_SECURE_TLS_SESSION *session_ptr,
                  NX_SECURE_X509_CERT *certificate, UINT cert_id);
```

### <a name="description"></a><span data-ttu-id="ee161-580">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-580">Description</span></span>

<span data-ttu-id="ee161-581">Bu hizmet, bir TLS oturumunun yerel deposuna bir sertifika eklemek için kullanılır (bkz. nx_secure_tls_local_certificate_add) sertifikanın içindeki X. 509.952 Subject (ortak ad) kullanarak depoyu dizinlemek yerine bir sayısal tanımlayıcı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="ee161-581">This service is used to add a certificate to a TLS session's local store (see nx_secure_tls_local_certificate_add) using a numeric identifier instead of indexing the store using the X.509 Subject (Common Name) within the certificate.</span></span> <span data-ttu-id="ee161-582">Sayısal tanımlayıcı sertifikadan ayrıdır ve birden çok sertifikanın bir TLS sunucusuna kimlik sertifikası olarak eklenmesine izin verir, ayrıca aynı ortak ada sahip birden çok sertifikanın aynı TLS oturumu yerel deposuna eklenmesine izin verir.</span><span class="sxs-lookup"><span data-stu-id="ee161-582">The numeric identifier is separate from the certificate and allows multiple certificates to be added as identity certificates to a TLS server, as well as allowing multiple certificates with the same Common Name to be added to the same TLS session local store.</span></span> <span data-ttu-id="ee161-583">Aynı hizmet istemci sertifikaları için kullanılabilir, ancak bir TLS istemcisinde birden çok kimlik sertifikası olması nadir bir durumdur.</span><span class="sxs-lookup"><span data-stu-id="ee161-583">This same service can be used for client certificates, but it is rare for a TLS client to have multiple identity certificates.</span></span>

<span data-ttu-id="ee161-584">Cert_id parametresi, uygulama tarafından atanan sıfır olmayan pozitif bir tamsayıdır.</span><span class="sxs-lookup"><span data-stu-id="ee161-584">The cert_id parameter is a non-zero positive integer assigned by the application.</span></span> <span data-ttu-id="ee161-585">Gerçek değer (sıfırdan farklı) değil, ancak belirtilen TLS oturumunun deposunda benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ee161-585">The actual value does not matter (other than zero) but it must be unique in the store for the provided TLS session.</span></span> <span data-ttu-id="ee161-586">Cert_id değeri, sırasıyla nx_secure_tls_server_certificate_find ve nx_secure_tls_server_certificate_remove kullanılarak yerel depodan sertifika bulmak ve kaldırmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ee161-586">The cert_id value can be used to find and remove certificates from the local store using nx_secure_tls_server_certificate_find and nx_secure_tls_server_certificate_remove, respectively.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ee161-587">*Bu API, nx_secure_tls_local_certificate_add kullanırken aynı TLS oturumuyla kullanılmamalıdır. Nx_secure_tls_server_certificate_add API 'SI her sertifika için benzersiz bir sayısal tanımlayıcı ve X. 509.440 ortak adına göre yerel sertifika hizmetleri dizini kullanır. Sunucu sertifikası Hizmetleri, aynı yerel depoda paylaşılan verileri olan birden çok sertifikanın (özellikle ortak ad) bulunmasına izin verir. Bu, birden çok kimliği olan bir sunucu için faydalıdır.*</span><span class="sxs-lookup"><span data-stu-id="ee161-587">*This API should not be used with the same TLS session when using nx_secure_tls_local_certificate_add. The nx_secure_tls_server_certificate_add API uses a unique numeric identifier for each certificate, and local certificate services index based on the X.509 Common Name. The server certificate services allow multiple certificates with shared data (especially Common Name) to exist in the same local store – this is useful for a server with multiple identities.*</span></span>

### <a name="parameters"></a><span data-ttu-id="ee161-588">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ee161-588">Parameters</span></span>

- <span data-ttu-id="ee161-589">**session_ptr** Daha önce oluşturulmuş bir TLS oturum örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ee161-589">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="ee161-590">**sertifika** Daha önce başlatılmış bir X. 509.440 sertifika örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ee161-590">**certificate** Pointer to a previously initialized X.509 certificate instance.</span></span>
- <span data-ttu-id="ee161-591">**cert_id** Pozitif, sıfır olmayan, görece benzersiz sertifika KIMLIĞI numarası.</span><span class="sxs-lookup"><span data-stu-id="ee161-591">**cert_id** Positive, non-zero, relatively unique certificate ID number.</span></span>

### <a name="return-values"></a><span data-ttu-id="ee161-592">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ee161-592">Return Values</span></span>

- <span data-ttu-id="ee161-593">**NX_SUCCESS** (0x00) başarılı işlemi.</span><span class="sxs-lookup"><span data-stu-id="ee161-593">**NX_SUCCESS** (0x00)Successful operation.</span></span>
- <span data-ttu-id="ee161-594">**NX_PTR_ERROR** (0x07) geçersiz TLS oturumu orcertificate işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-594">**NX_PTR_ERROR** (0x07) Invalid TLS session orcertificate pointer.</span></span>
- <span data-ttu-id="ee161-595">**NX_SECURE_TLS_CERT_ID_INVALID** (0x138) BELIRTILEN sertifika kimliğinde geçersiz bir değer (olası 0) vardı.</span><span class="sxs-lookup"><span data-stu-id="ee161-595">**NX_SECURE_TLS_CERT_ID_INVALID** (0x138) The provided certificate ID had An invalid value (likely 0).</span></span>
- <span data-ttu-id="ee161-596">**NX_SECURE_TLS_CERT_ID_DUPLICATE** (0x139) BELIRTILEN sertifika kimliği yerel depoda zaten var.</span><span class="sxs-lookup"><span data-stu-id="ee161-596">**NX_SECURE_TLS_CERT_ID_DUPLICATE** (0x139) The provided certificate ID was already present in the local store.</span></span>
- <span data-ttu-id="ee161-597">**NX_INVALID_PARAMETERS (0x4D)** İç hata – sertifika deposu muhtemelen bozuk.</span><span class="sxs-lookup"><span data-stu-id="ee161-597">**NX_INVALID_PARAMETERS(0x4D)** Internal error – certificate store likely corrupt.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ee161-598">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ee161-598">Allowed From</span></span>

<span data-ttu-id="ee161-599">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ee161-599">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ee161-600">Örnek</span><span class="sxs-lookup"><span data-stu-id="ee161-600">Example</span></span>

```C
/* Certificate control block. */
NX_SECURE_X509_CERT certificate;


/* Add certificate to TLS session.  */
status =  nx_secure_tls_server_certificate_add(&tls_session, &certificate, 0x12);


/* If status is NX_SUCCESS the certificate was successfully added with the ID
0x12.  */
```

### <a name="see-also"></a><span data-ttu-id="ee161-601">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ee161-601">See Also</span></span>

- <span data-ttu-id="ee161-602">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="ee161-602">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="ee161-603">nx_secure_tls_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="ee161-603">nx_secure_tls_local_certificate_add</span></span>
- <span data-ttu-id="ee161-604">nx_secure_tls_active_certificate_set</span><span class="sxs-lookup"><span data-stu-id="ee161-604">nx_secure_tls_active_certificate_set</span></span>
- <span data-ttu-id="ee161-605">nx_secure_tls_server_certificate_find</span><span class="sxs-lookup"><span data-stu-id="ee161-605">nx_secure_tls_server_certificate_find</span></span>
- <span data-ttu-id="ee161-606">nx_secure_tls_server_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="ee161-606">nx_secure_tls_server_certificate_remove</span></span>

## <a name="nx_secure_tls_server_certificate_find"></a><span data-ttu-id="ee161-607">nx_secure_tls_server_certificate_find</span><span class="sxs-lookup"><span data-stu-id="ee161-607">nx_secure_tls_server_certificate_find</span></span>

<span data-ttu-id="ee161-608">Sayısal tanımlayıcı kullanarak sertifika bulma</span><span class="sxs-lookup"><span data-stu-id="ee161-608">Find a certificate using a numeric identifier</span></span>

### <a name="prototype"></a><span data-ttu-id="ee161-609">Prototype</span><span class="sxs-lookup"><span data-stu-id="ee161-609">Prototype</span></span>

```C
UINT  nx_secure_tls_server_certificate_find(
                  NX_SECURE_TLS_SESSION *session_ptr,
                  NX_SECURE_X509_CERT **certificate, UINT cert_id);
```

### <a name="description"></a><span data-ttu-id="ee161-610">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-610">Description</span></span>

<span data-ttu-id="ee161-611">Bu hizmet, bir TLS oturumunun yerel deposundaki bir sertifikayı bulmak için kullanılır (bkz. nx_secure_tls_local_certificate_add) sertifikanın içindeki X. 509.952 Subject (ortak ad) kullanarak depoyu dizinlemek yerine bir sayısal tanımlayıcı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="ee161-611">This service is used to find a certificate in a TLS session's local store (see nx_secure_tls_local_certificate_add) using a numeric identifier instead of indexing the store using the X.509 Subject (Common Name) within the certificate.</span></span>

<span data-ttu-id="ee161-612">Cert_id parametresi, sertifika, nx_secure_tls_server_certificate_add kullanılarak TLS oturumu yerel deposuna eklendiğinde, uygulama tarafından atanan sıfır olmayan pozitif bir tamsayıdır.</span><span class="sxs-lookup"><span data-stu-id="ee161-612">The cert_id parameter is a non-zero positive integer assigned by the application when the certificate is added to the TLS session local store using nx_secure_tls_server_certificate_add.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ee161-613">*Bu API, nx_secure_tls_local_certificate_add kullanırken aynı TLS oturumuyla kullanılmamalıdır. Nx_secure_tls_server_certificate_add API 'SI her sertifika için benzersiz bir sayısal tanımlayıcı ve X. 509.440 ortak adına göre yerel sertifika hizmetleri dizini kullanır. Sunucu sertifikası Hizmetleri, aynı yerel depoda paylaşılan verileri olan birden çok sertifikanın (özellikle ortak ad) bulunmasına izin verir. Bu, birden çok kimliği olan bir sunucu için faydalıdır.*</span><span class="sxs-lookup"><span data-stu-id="ee161-613">*This API should not be used with the same TLS session when using nx_secure_tls_local_certificate_add. The nx_secure_tls_server_certificate_add API uses a unique numeric identifier for each certificate, and local certificate services index based on the X.509 Common Name. The server certificate services allow multiple certificates with shared data (especially Common Name) to exist in the same local store – this is useful for a server with multiple identities.*</span></span>

### <a name="parameters"></a><span data-ttu-id="ee161-614">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ee161-614">Parameters</span></span>

- <span data-ttu-id="ee161-615">**session_ptr** Daha önce oluşturulmuş bir TLS oturum örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ee161-615">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="ee161-616">**sertifika** Bulunan sertifikaya bir başvuru döndürecek bir X. 509.440 sertifika işaretçisine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ee161-616">**certificate** Pointer to an X.509 certificate pointer to return a reference to the found certificate.</span></span>
- <span data-ttu-id="ee161-617">**cert_id** Sıfır olmayan pozitif sertifika KIMLIĞI değeri.</span><span class="sxs-lookup"><span data-stu-id="ee161-617">**cert_id** Non-zero positive certificate ID value.</span></span>

### <a name="return-values"></a><span data-ttu-id="ee161-618">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ee161-618">Return Values</span></span>

- <span data-ttu-id="ee161-619">**NX_SUCCESS** (0x00) başarılı işlemi.</span><span class="sxs-lookup"><span data-stu-id="ee161-619">**NX_SUCCESS** (0x00)Successful operation.</span></span>
- <span data-ttu-id="ee161-620">**NX_PTR_ERROR** (0x07) geçersiz TLS oturumu veya sertifika işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-620">**NX_PTR_ERROR** (0x07) Invalid TLS session or certificate pointer.</span></span>
- <span data-ttu-id="ee161-621">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) BELIRTILEN sertifika kimliği, belirtilen TLS oturumunun yerel deposundaki herhangi bir hiçbiriyle eşleşmedi.</span><span class="sxs-lookup"><span data-stu-id="ee161-621">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) The provided certificate ID did not match any in the local store of the provided TLS session.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ee161-622">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ee161-622">Allowed From</span></span>

<span data-ttu-id="ee161-623">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ee161-623">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ee161-624">Örnek</span><span class="sxs-lookup"><span data-stu-id="ee161-624">Example</span></span>

```C
NX_SECURE_X509_CERT *certificate;


/* Find certificate in TLS session.  */
status =  nx_secure_tls_server_certificate_find(&tls_session, &certificate, 0x12);


/* If status is NX_SUCCESS the certificate was successfully found and a reference
returned in the certificate parameter.  */
```

### <a name="see-also"></a><span data-ttu-id="ee161-625">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ee161-625">See Also</span></span>

- <span data-ttu-id="ee161-626">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="ee161-626">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="ee161-627">nx_secure_tls_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="ee161-627">nx_secure_tls_local_certificate_add</span></span>
- <span data-ttu-id="ee161-628">nx_secure_tls_active_certificate_set</span><span class="sxs-lookup"><span data-stu-id="ee161-628">nx_secure_tls_active_certificate_set</span></span>
- <span data-ttu-id="ee161-629">nx_secure_tls_server_certificate_add</span><span class="sxs-lookup"><span data-stu-id="ee161-629">nx_secure_tls_server_certificate_add</span></span>
- <span data-ttu-id="ee161-630">nx_secure_tls_server_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="ee161-630">nx_secure_tls_server_certificate_remove</span></span>

##  <a name="nx_secure_tls_server_certificate_remove"></a><span data-ttu-id="ee161-631">nx_secure_tls_server_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="ee161-631">nx_secure_tls_server_certificate_remove</span></span>

<span data-ttu-id="ee161-632">Sayısal tanımlayıcıyı kullanarak yerel sunucu sertifikasını kaldırma</span><span class="sxs-lookup"><span data-stu-id="ee161-632">Remove a local server certificate using a numeric identifier</span></span>

### <a name="prototype"></a><span data-ttu-id="ee161-633">Prototype</span><span class="sxs-lookup"><span data-stu-id="ee161-633">Prototype</span></span>

```C
UINT  nx_secure_tls_server_certificate_remove(
                  NX_SECURE_TLS_SESSION *session_ptr, UINT cert_id);
```

### <a name="description"></a><span data-ttu-id="ee161-634">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-634">Description</span></span>

<span data-ttu-id="ee161-635">Bu hizmet, bir sertifikayı bir TLS oturumunun yerel deposundan kaldırmak için kullanılır (bkz. nx_secure_tls_local_certificate_add) sertifikanın içindeki X. 509.952 Subject (ortak ad) kullanarak depoyu dizinlemek yerine sayısal bir tanımlayıcı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="ee161-635">This service is used to remove a certificate from a TLS session's local store (see nx_secure_tls_local_certificate_add) using a numeric identifier instead of indexing the store using the X.509 Subject (Common Name) within the certificate.</span></span>

<span data-ttu-id="ee161-636">Cert_id parametresi, sertifika, nx_secure_tls_server_certificate_add kullanılarak TLS oturumu yerel deposuna eklendiğinde, uygulama tarafından atanan sıfır olmayan pozitif bir tamsayıdır.</span><span class="sxs-lookup"><span data-stu-id="ee161-636">The cert_id parameter is a non-zero positive integer assigned by the application when the certificate is added to the TLS session local store using nx_secure_tls_server_certificate_add.</span></span>

### <a name="parameters"></a><span data-ttu-id="ee161-637">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ee161-637">Parameters</span></span>

- <span data-ttu-id="ee161-638">**session_ptr** Daha önce oluşturulmuş bir TLS oturum örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ee161-638">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="ee161-639">**cert_id** Sıfır olmayan pozitif sertifika KIMLIĞI değeri.</span><span class="sxs-lookup"><span data-stu-id="ee161-639">**cert_id** Non-zero positive certificate ID value.</span></span>

### <a name="return-values"></a><span data-ttu-id="ee161-640">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ee161-640">Return Values</span></span>

- <span data-ttu-id="ee161-641">**NX_SUCCESS** (0x00) başarılı işlemi.</span><span class="sxs-lookup"><span data-stu-id="ee161-641">**NX_SUCCESS** (0x00)Successful operation.</span></span>
- <span data-ttu-id="ee161-642">**NX_PTR_ERROR** (0x07) geçersiz TLS oturumu.</span><span class="sxs-lookup"><span data-stu-id="ee161-642">**NX_PTR_ERROR** (0x07) Invalid TLS session.</span></span>
- <span data-ttu-id="ee161-643">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) BELIRTILEN sertifika kimliği, belirtilen TLS oturumunun yerel deposundaki herhangi bir hiçbiriyle eşleşmedi.</span><span class="sxs-lookup"><span data-stu-id="ee161-643">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) The provided certificate ID did not match any in the local store of the provided TLS session.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ee161-644">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ee161-644">Allowed From</span></span>

<span data-ttu-id="ee161-645">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ee161-645">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ee161-646">Örnek</span><span class="sxs-lookup"><span data-stu-id="ee161-646">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="ee161-647">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ee161-647">See Also</span></span>

- <span data-ttu-id="ee161-648">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="ee161-648">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="ee161-649">nx_secure_tls_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="ee161-649">nx_secure_tls_local_certificate_add</span></span>
- <span data-ttu-id="ee161-650">nx_secure_tls_active_certificate_set</span><span class="sxs-lookup"><span data-stu-id="ee161-650">nx_secure_tls_active_certificate_set</span></span>
- <span data-ttu-id="ee161-651">nx_secure_tls_server_certificate_add</span><span class="sxs-lookup"><span data-stu-id="ee161-651">nx_secure_tls_server_certificate_add</span></span>
- <span data-ttu-id="ee161-652">nx_secure_tls_server_certificate_find</span><span class="sxs-lookup"><span data-stu-id="ee161-652">nx_secure_tls_server_certificate_find</span></span>

## <a name="nx_secure_tls_session_alert_value_get"></a><span data-ttu-id="ee161-653">nx_secure_tls_session_alert_value_get</span><span class="sxs-lookup"><span data-stu-id="ee161-653">nx_secure_tls_session_alert_value_get</span></span>

<span data-ttu-id="ee161-654">Uzak ana bilgisayar tarafından gönderilen TLS uyarı değerini ve düzeyini al</span><span class="sxs-lookup"><span data-stu-id="ee161-654">Get the TLS alert value and level sent by the remote host</span></span>

### <a name="prototype"></a><span data-ttu-id="ee161-655">Prototype</span><span class="sxs-lookup"><span data-stu-id="ee161-655">Prototype</span></span>

```C
UINT  nx_secure_tls_session_alert_value_get(
                   NX_SECURE_TLS_SESSION *session_ptr,
                   UINT *alert_level, UINT *alert_value);
```

### <a name="description"></a><span data-ttu-id="ee161-656">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-656">Description</span></span>

<span data-ttu-id="ee161-657">Bu hizmet, uzak ana bilgisayar bir sorun veya hataya yanıt olarak bir uyarı gönderdiğinde TLS uyarı düzeyini ve değerini almak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ee161-657">This service is used to retrieve the TLS alert level and value when the remote host sends an alert in response to some problem or error.</span></span>

<span data-ttu-id="ee161-658">Alert_level ve alert_value parametrelerinin değerleri yalnızca, bu işlev, uzak konaktan bir uyarının alındığını belirten NX_SECURE_TLS_ALERT_RECEIVED (0x114) durumunu döndüren bir TLS API çağrısından hemen sonra çağrılırsa geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="ee161-658">The values of the alert_level and alert_value parameters are only valid if this function is called immediately following a TLS API call that returned a status of NX_SECURE_TLS_ALERT_RECEIVED (0x114) indicating that an alert was received from the remote host.</span></span>

<span data-ttu-id="ee161-659">Yerel ana bilgisayar TLS bir uyarı gönderirse, döndürülen hata kodları, belirli türde saldırı yapılmasını engellemek için kasıtlı olarak doğru bir şekilde (örneğin, bir "Oracle" saldırısı veya benzer) karşı belirsiz şekilde ayrıldığından TLS uyarısının kendisinden daha fazla tanımlayıcı olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ee161-659">Note that if the local host TLS sends an alert, the returned error codes are far more descriptive of the actual error than the TLS alert itself because TLS alert values are intentionally left ambiguous to prevent certain types of attack (such as a "padding oracle" attack or similar).</span></span>

<span data-ttu-id="ee161-660">Uyarı düzeyi yalnızca iki değerden birini alır: NX_SECURE_TLS_ALERT_LEVEL_WARNING (0x1) veya NX_SECURE_TLS_ALERT_LEVEL_FATAL (0x2).</span><span class="sxs-lookup"><span data-stu-id="ee161-660">The alert level only takes one of two values: NX_SECURE_TLS_ALERT_LEVEL_WARNING (0x1) or NX_SECURE_TLS_ALERT_LEVEL_FATAL (0x2).</span></span> <span data-ttu-id="ee161-661">Genel olarak, yalnızca CloseNotify uyarısına (bir TLS oturumunun başarılı bir şekilde bitmesi için kullanılır), bazı uzantı yapılandırma durumlarında de uyarı olarak kabul edilebilir.</span><span class="sxs-lookup"><span data-stu-id="ee161-661">In general, only the CloseNotify Alert (used to indicate a successful end to a TLS session) will be given a level of "Warning" though some extension configuration situations may also be considered warnings.</span></span> <span data-ttu-id="ee161-662">Uyarıların büyük çoğunluğu olası bir güvenlik hatasını belirten ve TLS bağlantısının (el sıkışma veya oturum) doğrudan kapatılmasını elde eden "önemli" olacaktır.</span><span class="sxs-lookup"><span data-stu-id="ee161-662">The vast majority of alerts will be "Fatal" indicating a potential security failure and resulting in immediate closure of the TLS connection (handshake or session).</span></span>

<span data-ttu-id="ee161-663">TLS uyarı değerleri TLS RFC 'lerde tanımlanmıştır, aşağıdaki başvuru için RFC 5246 (TLSv 1.2) listesidir:</span><span class="sxs-lookup"><span data-stu-id="ee161-663">The TLS alert values are defined in the TLS RFCs, here is the list from RFC 5246 (TLSv1.2) for reference:</span></span>

| <span data-ttu-id="ee161-664">Uyarı Adı</span><span class="sxs-lookup"><span data-stu-id="ee161-664">Alert Name</span></span>                     | <span data-ttu-id="ee161-665">Değer</span><span class="sxs-lookup"><span data-stu-id="ee161-665">Value</span></span> | <span data-ttu-id="ee161-666">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-666">Description</span></span>                                                                                                                                                  |
| ---------------------------------- | --------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <span data-ttu-id="ee161-667">close_notify</span><span class="sxs-lookup"><span data-stu-id="ee161-667">close_notify</span></span>                  | <span data-ttu-id="ee161-668">0</span><span class="sxs-lookup"><span data-stu-id="ee161-668">0</span></span>     | <span data-ttu-id="ee161-669">Hata yok, başarılı oturum sonu olduğunu belirtir</span><span class="sxs-lookup"><span data-stu-id="ee161-669">No error, indicates successful session end</span></span>                                                                                                                   |
| <span data-ttu-id="ee161-670">unexpected_message</span><span class="sxs-lookup"><span data-stu-id="ee161-670">unexpected_message</span></span>            | <span data-ttu-id="ee161-671">10</span><span class="sxs-lookup"><span data-stu-id="ee161-671">10</span></span>    | <span data-ttu-id="ee161-672">TLS beklenmeyen veya bir sıra dışı ileti aldı</span><span class="sxs-lookup"><span data-stu-id="ee161-672">TLS received an unexpected or out-of-order message</span></span>                                                                                                           |
| <span data-ttu-id="ee161-673">bad_record_mac</span><span class="sxs-lookup"><span data-stu-id="ee161-673">bad_record_mac</span></span>               | <span data-ttu-id="ee161-674">20</span><span class="sxs-lookup"><span data-stu-id="ee161-674">20</span></span>    | <span data-ttu-id="ee161-675">Şifre çözme ve/veya MAC doğrulaması başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="ee161-675">Decryption and/or MAC verification failed</span></span>                                                                                                                    |
| <span data-ttu-id="ee161-676">decryption_failed_RESERVED</span><span class="sxs-lookup"><span data-stu-id="ee161-676">decryption_failed_RESERVED</span></span>   | <span data-ttu-id="ee161-677">21</span><span class="sxs-lookup"><span data-stu-id="ee161-677">21</span></span>    | <span data-ttu-id="ee161-678">**Kullanım dışı** Şifre çözme başarısız oldu (Oracle saldırılarını doldurma nedeniyle kullanım dışı)</span><span class="sxs-lookup"><span data-stu-id="ee161-678">**DEPRECATED** Decryption failed (deprecated due to padding oracle attacks)</span></span>                                                                                      |
| <span data-ttu-id="ee161-679">record_overflow</span><span class="sxs-lookup"><span data-stu-id="ee161-679">record_overflow</span></span>               | <span data-ttu-id="ee161-680">22</span><span class="sxs-lookup"><span data-stu-id="ee161-680">22</span></span>    | <span data-ttu-id="ee161-681">En fazla TLS kayıt boyutundan daha büyük olan bir kayıt alındı</span><span class="sxs-lookup"><span data-stu-id="ee161-681">A record was received that is larger than the TLS maximum record size</span></span>                                                                                        |
| <span data-ttu-id="ee161-682">decompression_failure</span><span class="sxs-lookup"><span data-stu-id="ee161-682">decompression_failure</span></span>         | <span data-ttu-id="ee161-683">30</span><span class="sxs-lookup"><span data-stu-id="ee161-683">30</span></span>    | <span data-ttu-id="ee161-684">TLS kaydının sıkıştırılması/sıkıştırması açılmasında bir sorunla karşılaşıldı</span><span class="sxs-lookup"><span data-stu-id="ee161-684">A problem was encountered in compression/decompression of a TLS record</span></span>                                                                                       |
| <span data-ttu-id="ee161-685">handshake_failure</span><span class="sxs-lookup"><span data-stu-id="ee161-685">handshake_failure</span></span>             | <span data-ttu-id="ee161-686">40</span><span class="sxs-lookup"><span data-stu-id="ee161-686">40</span></span>    | <span data-ttu-id="ee161-687">Farklı bir uyarı kapsamında olmayan bazı belirtilmeyen bir el sıkışma hatası oluştu</span><span class="sxs-lookup"><span data-stu-id="ee161-687">Some unspecified handshake error occurred that isn't covered by a different alert</span></span>                                                                            |
| <span data-ttu-id="ee161-688">no_certificate_RESERVED</span><span class="sxs-lookup"><span data-stu-id="ee161-688">no_certificate_RESERVED</span></span>      | <span data-ttu-id="ee161-689">41</span><span class="sxs-lookup"><span data-stu-id="ee161-689">41</span></span>    | <span data-ttu-id="ee161-690">TLS 'de **kullanım dışı** (yalnızca SSL)</span><span class="sxs-lookup"><span data-stu-id="ee161-690">**DEPRECATED** in TLS (SSL only)</span></span>                                                                                                                                 |
| <span data-ttu-id="ee161-691">bad_certificate</span><span class="sxs-lookup"><span data-stu-id="ee161-691">bad_certificate</span></span>               | <span data-ttu-id="ee161-692">42</span><span class="sxs-lookup"><span data-stu-id="ee161-692">42</span></span>    | <span data-ttu-id="ee161-693">Alınan bir sertifika geçersiz biçimlendirme veya imza içeriyordu</span><span class="sxs-lookup"><span data-stu-id="ee161-693">A certificate that was received contained invalid formatting or signatures</span></span>                                                                                   |
| <span data-ttu-id="ee161-694">unsupported_certificate</span><span class="sxs-lookup"><span data-stu-id="ee161-694">unsupported_certificate</span></span>       | <span data-ttu-id="ee161-695">43</span><span class="sxs-lookup"><span data-stu-id="ee161-695">43</span></span>    | <span data-ttu-id="ee161-696">Geçersiz bir tür (örneğin, TLS sunucu kimlik doğrulaması için kullanılan yalnızca oturum açma sertifikası) olan bir sertifika alındı</span><span class="sxs-lookup"><span data-stu-id="ee161-696">A certificate was received that was of an invalid type (e.g. signing-only certificate used for TLS server authentication)</span></span>                                    |
| <span data-ttu-id="ee161-697">certificate_revoked</span><span class="sxs-lookup"><span data-stu-id="ee161-697">certificate_revoked</span></span>           | <span data-ttu-id="ee161-698">44</span><span class="sxs-lookup"><span data-stu-id="ee161-698">44</span></span>    | <span data-ttu-id="ee161-699">Sertifika durumu (bir CRL veya OCSP tarafından sağlandığı gibi) "iptal edildi" olarak belirtilmiştir</span><span class="sxs-lookup"><span data-stu-id="ee161-699">The certificate status (as provided by a CRL or OCSP) was indicated as being "revoked"</span></span>                                                                       |
| <span data-ttu-id="ee161-700">certificate_expired</span><span class="sxs-lookup"><span data-stu-id="ee161-700">certificate_expired</span></span>           | <span data-ttu-id="ee161-701">45</span><span class="sxs-lookup"><span data-stu-id="ee161-701">45</span></span>    | <span data-ttu-id="ee161-702">Alınan sertifika geçerli bir tarih aralığı dışındaydı (henüz geçerli değil veya kullanım tarihi belirtilmemiş)</span><span class="sxs-lookup"><span data-stu-id="ee161-702">The received certificate was outside it's valid date range (either not valid yet or expired)</span></span>                                                                 |
| <span data-ttu-id="ee161-703">certificate_unknown</span><span class="sxs-lookup"><span data-stu-id="ee161-703">certificate_unknown</span></span>           | <span data-ttu-id="ee161-704">46</span><span class="sxs-lookup"><span data-stu-id="ee161-704">46</span></span>    | <span data-ttu-id="ee161-705">Diğer uyarıların kapsamadığı bilinmeyen bir sertifika sorunuyla karşılaşıldı</span><span class="sxs-lookup"><span data-stu-id="ee161-705">Some unknown certificate issue was encountered that was not covered by other alerts</span></span>                                                                          |
| <span data-ttu-id="ee161-706">illegal_parameter</span><span class="sxs-lookup"><span data-stu-id="ee161-706">illegal_parameter</span></span>             | <span data-ttu-id="ee161-707">47</span><span class="sxs-lookup"><span data-stu-id="ee161-707">47</span></span>    | <span data-ttu-id="ee161-708">TLS el sıkışmasındaki bazı yapılandırma veya anlaşmalı değer geçersiz veya Aralık dışında</span><span class="sxs-lookup"><span data-stu-id="ee161-708">Some configuration or negotiated value in the TLS handshake was invalid or out of range</span></span>                                                                      |
| <span data-ttu-id="ee161-709">unknown_ca</span><span class="sxs-lookup"><span data-stu-id="ee161-709">unknown_ca</span></span>                    | <span data-ttu-id="ee161-710">48</span><span class="sxs-lookup"><span data-stu-id="ee161-710">48</span></span>    | <span data-ttu-id="ee161-711">Alınan kimlik sertifikası, bir sertifika zinciri aracılığıyla güvenilen bir kök CA sertifikasına izyüklenemedi.</span><span class="sxs-lookup"><span data-stu-id="ee161-711">The received identity certificate could not be traced via a certificate chain to a trusted root CA certificate.</span></span>                                              |
| <span data-ttu-id="ee161-712">access_denied</span><span class="sxs-lookup"><span data-stu-id="ee161-712">access_denied</span></span>                 | <span data-ttu-id="ee161-713">49</span><span class="sxs-lookup"><span data-stu-id="ee161-713">49</span></span>    | <span data-ttu-id="ee161-714">Geçerli bir sertifika alındığını gösterir, ancak uygulama erişim denetimi, sertifikanın istenen kaynaklar için geçersiz olduğunu belirtti.</span><span class="sxs-lookup"><span data-stu-id="ee161-714">Indicates a valid certificate was received but application access control indicated that the certificate was invalid for the requested resources.</span></span>            |
| <span data-ttu-id="ee161-715">decode_error</span><span class="sxs-lookup"><span data-stu-id="ee161-715">decode_error</span></span>                  | <span data-ttu-id="ee161-716">50</span><span class="sxs-lookup"><span data-stu-id="ee161-716">50</span></span>    | <span data-ttu-id="ee161-717">Bir TLS üstbilgisindeki veya el sıkışma iletisindeki bazı alan veya değerler Aralık dışındaydı veya geçersiz, bir TLS kaydının kodunu çözerken hata verdi.</span><span class="sxs-lookup"><span data-stu-id="ee161-717">Some field or value in a TLS header or handshake message was out of range or invalid, leading to a failure in decoding of a TLS record.</span></span>                      |
| <span data-ttu-id="ee161-718">decrypt_error</span><span class="sxs-lookup"><span data-stu-id="ee161-718">decrypt_error</span></span>                 | <span data-ttu-id="ee161-719">51</span><span class="sxs-lookup"><span data-stu-id="ee161-719">51</span></span>    | <span data-ttu-id="ee161-720">TLS el sıkışması sırasında imza veya tamamlanan ileti karması doğrulanamadı.</span><span class="sxs-lookup"><span data-stu-id="ee161-720">A signature or Finished message hash during the TLS handshake could not be verified.</span></span>                                                                         |
| <span data-ttu-id="ee161-721">export_restriction_RESERVED</span><span class="sxs-lookup"><span data-stu-id="ee161-721">export_restriction_RESERVED</span></span>  | <span data-ttu-id="ee161-722">60</span><span class="sxs-lookup"><span data-stu-id="ee161-722">60</span></span>    | <span data-ttu-id="ee161-723">TLSv 1.2 'de kullanım DıŞı</span><span class="sxs-lookup"><span data-stu-id="ee161-723">DEPRECATED in TLSv1.2</span></span>                                                                                                                                        |
| <span data-ttu-id="ee161-724">protocol_version</span><span class="sxs-lookup"><span data-stu-id="ee161-724">protocol_version</span></span>              | <span data-ttu-id="ee161-725">70</span><span class="sxs-lookup"><span data-stu-id="ee161-725">70</span></span>    | <span data-ttu-id="ee161-726">El sıkışma sırasında anlaşılan TLS protokol sürümü tanınıyor ancak desteklenmez (örneğin, TLSv 1.0 sunuluyor ancak etkinleştirilmemiş).</span><span class="sxs-lookup"><span data-stu-id="ee161-726">The TLS protocol version negotiated during the handshake is recognized but not supported (e.g. TLSv1.0 was presented but not enabled).</span></span>                       |
| <span data-ttu-id="ee161-727">insufficient_security</span><span class="sxs-lookup"><span data-stu-id="ee161-727">insufficient_security</span></span>         | <span data-ttu-id="ee161-728">71</span><span class="sxs-lookup"><span data-stu-id="ee161-728">71</span></span>    | <span data-ttu-id="ee161-729">Güvenli şifrelemelerin olmaması nedeniyle bir el sıkışma olduğunda gönderilir (örn. anahtar boyutu uygulama gereksinimleri için çok küçük)</span><span class="sxs-lookup"><span data-stu-id="ee161-729">Sent whenever a handshake fails due to a lack of secure ciphers (e.g. key size is too small for the application requirements)</span></span>                                |
| <span data-ttu-id="ee161-730">internal_error</span><span class="sxs-lookup"><span data-stu-id="ee161-730">internal_error</span></span>                | <span data-ttu-id="ee161-731">80</span><span class="sxs-lookup"><span data-stu-id="ee161-731">80</span></span>    | <span data-ttu-id="ee161-732">Bazı TLS olmayan hatalar (örneğin, bellek ayırma sorunları, uygulama sorunları), bozuk bir TLS oturumuna neden oldu.</span><span class="sxs-lookup"><span data-stu-id="ee161-732">Some non-TLS error (e.g. memory allocation problems, application issues) occurred resulting in a broken TLS session.</span></span>                                         |
| <span data-ttu-id="ee161-733">user_canceled</span><span class="sxs-lookup"><span data-stu-id="ee161-733">user_canceled</span></span>                 | <span data-ttu-id="ee161-734">90</span><span class="sxs-lookup"><span data-stu-id="ee161-734">90</span></span>    | <span data-ttu-id="ee161-735">El sıkışma tamamlanmadan önce TLS oturumu bir kullanıcı veya uygulama tarafından iptal edildiğinde (CloseNotify 'a benzer) döndürülür.</span><span class="sxs-lookup"><span data-stu-id="ee161-735">Returned if the TLS session is cancelled by a user or application before the handshake is complete (similar to CloseNotify).</span></span>                                 |
| <span data-ttu-id="ee161-736">no_renegotiation</span><span class="sxs-lookup"><span data-stu-id="ee161-736">no_renegotiation</span></span>              | <span data-ttu-id="ee161-737">100</span><span class="sxs-lookup"><span data-stu-id="ee161-737">100</span></span>   | <span data-ttu-id="ee161-738">Uzak konağın, bir yeniden anlaşma isteğine yanıt olarak TLS yeniden anlaşma el sıkışmaları gerçekleştirmesini istemediğinden bağımsız olarak.</span><span class="sxs-lookup"><span data-stu-id="ee161-738">Indiates that the remote host is not willing to perform TLS renegotiation handshakes in response to a renegotiation request.</span></span>                                 |
| <span data-ttu-id="ee161-739">unsupported_extension</span><span class="sxs-lookup"><span data-stu-id="ee161-739">unsupported_extension</span></span>         | <span data-ttu-id="ee161-740">110</span><span class="sxs-lookup"><span data-stu-id="ee161-740">110</span></span>   | <span data-ttu-id="ee161-741">Bir TLS Istemcisi ilk ClientHello (sunucuda bir sorun olduğunu gösterir) için açıkça sorulmayan uzantıları içeren bir ServerHello alırsa gönderilir.</span><span class="sxs-lookup"><span data-stu-id="ee161-741">Sent if a TLS Client receives a ServerHello containing extensions not explicitly asked for in the initial ClientHello (indicating the server has a problem).</span></span> |

### <a name="parameters"></a><span data-ttu-id="ee161-742">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ee161-742">Parameters</span></span>

- <span data-ttu-id="ee161-743">**session_ptr** Bir TLS oturum örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-743">**session_ptr** Pointer to a TLS Session instance.</span></span>
- <span data-ttu-id="ee161-744">**alert_level** Alınan uyarının düzeyini döndürün (uyarı veya önemli).</span><span class="sxs-lookup"><span data-stu-id="ee161-744">**alert_level** Return the level of the received alert (warning or fatal).</span></span>
- <span data-ttu-id="ee161-745">**alert_value** Alınan uyarının değerini döndürür (bkz. tablo).</span><span class="sxs-lookup"><span data-stu-id="ee161-745">**alert_value** Return the value of the received alert (see table).</span></span>

### <a name="return-values"></a><span data-ttu-id="ee161-746">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ee161-746">Return Values</span></span>

- <span data-ttu-id="ee161-747">**NX_SUCCESS** (0x00) başarılı işlemi.</span><span class="sxs-lookup"><span data-stu-id="ee161-747">**NX_SUCCESS** (0x00) Successful operation.</span></span>
- <span data-ttu-id="ee161-748">**NX_PTR_ERROR** (0x07) geçersiz TLS oturumu.</span><span class="sxs-lookup"><span data-stu-id="ee161-748">**NX_PTR_ERROR** (0x07) Invalid TLS session.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ee161-749">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ee161-749">Allowed From</span></span>

<span data-ttu-id="ee161-750">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ee161-750">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ee161-751">Örnek</span><span class="sxs-lookup"><span data-stu-id="ee161-751">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="ee161-752">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ee161-752">See Also</span></span>

- <span data-ttu-id="ee161-753">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="ee161-753">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="ee161-754">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="ee161-754">nx_secure_tls_session_send</span></span>
- <span data-ttu-id="ee161-755">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="ee161-755">nx_secure_tls_session_receive</span></span>

## <a name="nx_secure_tls_session_certificate_callback_set"></a><span data-ttu-id="ee161-756">nx_secure_tls_session_certificate_callback_set</span><span class="sxs-lookup"><span data-stu-id="ee161-756">nx_secure_tls_session_certificate_callback_set</span></span>

<span data-ttu-id="ee161-757">Ek sertifika doğrulaması için kullanılacak TLS için bir geri çağırma ayarlayın</span><span class="sxs-lookup"><span data-stu-id="ee161-757">Set up a callback for TLS to use for additional certificate validation</span></span>

### <a name="prototype"></a><span data-ttu-id="ee161-758">Prototype</span><span class="sxs-lookup"><span data-stu-id="ee161-758">Prototype</span></span>

```C
UINT  nx_secure_tls_ session_certificate_callback_set (
                  NX_SECURE_TLS_SESSION *tls_session,
                  ULONG (*func_ptr)(NX_SECURE_TLS_SESSION *session,
                                    NX_SECURE_X509_CERT *certificate));
```

### <a name="description"></a><span data-ttu-id="ee161-759">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-759">Description</span></span>

<span data-ttu-id="ee161-760">Bu hizmet, uzak bir ana bilgisayardan bir sertifika alındığında, uygulamanın DNS doğrulaması, sertifika iptali ve sertifika ilkesi zorlaması gibi doğrulama denetimleri gerçekleştirmesine izin veren TLS oturumuna bir işlev işaretçisi atar.</span><span class="sxs-lookup"><span data-stu-id="ee161-760">This service assigns a function pointer to a TLS session that TLS will invoke when a certificate is received from a remote host, allowing the application to perform validation checks such as DNS validation, certificate revocation, and certificate policy enforcement.</span></span>

<span data-ttu-id="ee161-761">NetX güvenli TLS, sertifikanın TLS güvenilen sertifika deposundaki bir sertifikaya izlenip izlenmemesini sağlamak için geri çağırma işlemini çağırmadan önce sertifikada temel X. 509.952 yolu doğrulamasını yapar, ancak diğer tüm doğrulamalar bu geri arama tarafından işlenir.</span><span class="sxs-lookup"><span data-stu-id="ee161-761">NetX Secure TLS will perform basic X.509 path validation on the certificate before invoking the callback to assure that the certificate can be traced to a certificate in the TLS trusted certificate store, but all other validation will be handled by this callback.</span></span>

<span data-ttu-id="ee161-762">Geri arama, TLS oturum işaretçisini ve uzak ana bilgisayar kimliği sertifikası (sertifika zincirindeki yaprak) için bir işaretçi sağlar.</span><span class="sxs-lookup"><span data-stu-id="ee161-762">The callback provides the TLS session pointer and a pointer to the remote host identity certificate (the leaf in the certificate chain).</span></span> <span data-ttu-id="ee161-763">Tüm doğrulama başarılı olursa geri çağırma NX_SUCCESS döndürmelidir, aksi takdirde doğrulama hatasını gösteren bir hata kodu döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="ee161-763">The callback should return NX_SUCCESS if all validation is successful, otherwise it should return an error code indicating the validation failure.</span></span> <span data-ttu-id="ee161-764">NX_SUCCESS dışındaki herhangi bir değer, TLS el sıkışmasına hemen iptal edilmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="ee161-764">Any value other than NX_SUCCESS will cause the TLS handshake to immediately abort.</span></span>

### <a name="parameters"></a><span data-ttu-id="ee161-765">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ee161-765">Parameters</span></span>

- <span data-ttu-id="ee161-766">**session_ptr** Daha önce oluşturulmuş bir TLS oturum örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ee161-766">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="ee161-767">**func_ptr** Sertifika doğrulama geri çağırma işlevine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ee161-767">**func_ptr** Pointer to the certificate validation callback function.</span></span>

### <a name="return-values"></a><span data-ttu-id="ee161-768">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ee161-768">Return Values</span></span>

- <span data-ttu-id="ee161-769">Işlev işaretçisinin başarılı bir şekilde ayrılması **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="ee161-769">**NX_SUCCESS** (0x00) Successful allocation of Function pointer.</span></span>
- <span data-ttu-id="ee161-770">**NX_PTR_ERROR** (0x07) geçersiz TLS oturum işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-770">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ee161-771">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ee161-771">Allowed From</span></span>

<span data-ttu-id="ee161-772">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ee161-772">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ee161-773">Örnek</span><span class="sxs-lookup"><span data-stu-id="ee161-773">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="ee161-774">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ee161-774">See Also</span></span>

- <span data-ttu-id="ee161-775">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="ee161-775">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="ee161-776">nx_secure_x509_common_name_dns_check</span><span class="sxs-lookup"><span data-stu-id="ee161-776">nx_secure_x509_common_name_dns_check</span></span>
- <span data-ttu-id="ee161-777">nx_secure_x509_crl_revocation_check</span><span class="sxs-lookup"><span data-stu-id="ee161-777">nx_secure_x509_crl_revocation_check</span></span>

## <a name="nx_secure_tls_session_client_callback_set"></a><span data-ttu-id="ee161-778">nx_secure_tls_session_client_callback_set</span><span class="sxs-lookup"><span data-stu-id="ee161-778">nx_secure_tls_session_client_callback_set</span></span>

<span data-ttu-id="ee161-779">TLS Istemcisi el sıkışmasının başlangıcında çağırmak üzere TLS için bir geri çağırma ayarlayın</span><span class="sxs-lookup"><span data-stu-id="ee161-779">Set up a callback for TLS to invoke at the beginning of a TLS Client handshake</span></span>

### <a name="prototype"></a><span data-ttu-id="ee161-780">Prototype</span><span class="sxs-lookup"><span data-stu-id="ee161-780">Prototype</span></span>

```C
UINT  nx_secure_tls_ session_client_callback_set (
                  NX_SECURE_TLS_SESSION *tls_session,
                  ULONG (*func_ptr)(NX_SECURE_TLS_SESSION *tls_session,
                                    NX_SECURE_TLS_HELLO_EXTENSION
                                    *extensions, UINT num_extensions));
```

### <a name="description"></a><span data-ttu-id="ee161-781">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-781">Description</span></span>

<span data-ttu-id="ee161-782">Bu hizmet, TLS Istemcisi el sıkışması bir ServerHelloDone iletisi aldığında tls oturumuna bir işlev işaretçisi atar.</span><span class="sxs-lookup"><span data-stu-id="ee161-782">This service assigns a function pointer to a TLS session that TLS will invoke when a TLS Client handshake has received a ServerHelloDone message.</span></span> <span data-ttu-id="ee161-783">Geri arama işlevi, bir uygulamanın giriş veya karar verme gerektiren alınan ServerHello iletisinden herhangi bir TLS uzantısını işlemesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="ee161-783">The callback function allows an application to process any TLS extensions from the received ServerHello message that require input or decision making.</span></span>

<span data-ttu-id="ee161-784">Geri çağırma, TLS oturum denetim bloğu ve NX_SECURE_TLS_HELLO_EXTENSION nesnelerinden oluşan bir dizi ile yürütülür.</span><span class="sxs-lookup"><span data-stu-id="ee161-784">The callback is executed with the invoking TLS session control block and an array of NX_SECURE_TLS_HELLO_EXTENSION objects.</span></span> <span data-ttu-id="ee161-785">Uzantı nesnelerinin dizisi, belirli bir uzantıyı bulacak ve ayrıştıracak bir yardımcı işleve geçirilmesi amaçlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="ee161-785">The array of extension objects is intended to be passed into a helper function that will find and parse a specific extension.</span></span> <span data-ttu-id="ee161-786">Şu anda NetX güvenli içinde TLS Istemci girişi gerektiren belirli Uzantılar yoktur, ancak uygulama tasarımcılarının kullanılabilir olabilecek özel veya yeni uzantıları işlemesi için geri çağırma kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ee161-786">Currently, there are no specific extensions supported in NetX Secure that require TLS Client input, but the callback is available for application designers to handle custom or new extensions that may become available.</span></span> <span data-ttu-id="ee161-787">Merhaba iletilerde sunulan TLS uzantılarını ayrıştırır örnek bir yardımcı işlev için bkz. *nx_secure_tls_session_sni_extension_parse*.</span><span class="sxs-lookup"><span data-stu-id="ee161-787">For an example helper function that parses TLS extensions provided in hello messages, see *nx_secure_tls_session_sni_extension_parse*.</span></span>

<span data-ttu-id="ee161-788">İstemci geri çağırması, uzak sunucunun bir sertifika istediği ve TLS Istemcisinin belirli bir sertifikayı seçmesini sağlamak üzere bilgi sağlamış olduğu olaydaki TLS Istemcisi için *nx_secure_tls_active_certificate_set* kullanarak etkin kimlik sertifikasını seçmek için de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ee161-788">The client callback may also be used to select the active identity certificate using *nx_secure_tls_active_certificate_set* for the TLS Client in the event that the remote server has requested a certificate and provided information to allow the TLS Client to select a specific certificate.</span></span> <span data-ttu-id="ee161-789">Daha fazla bilgi için bkz. nx_secure_tls_active_certificate_set başvurusu.</span><span class="sxs-lookup"><span data-stu-id="ee161-789">See the reference for nx_secure_tls_active_certificate_set for more information.</span></span>

### <a name="parameters"></a><span data-ttu-id="ee161-790">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ee161-790">Parameters</span></span>

- <span data-ttu-id="ee161-791">**session_ptr** Daha önce oluşturulmuş bir TLS oturum örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ee161-791">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="ee161-792">**func_ptr** TLS Istemci geri çağırma işlevine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ee161-792">**func_ptr** Pointer to the TLS Client callback function.</span></span>

### <a name="return-values"></a><span data-ttu-id="ee161-793">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ee161-793">Return Values</span></span>

- <span data-ttu-id="ee161-794">İşlev işaretçisinin başarılı bir şekilde ayrılması **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="ee161-794">**NX_SUCCESS** (0x00) Successful allocation of function pointer.</span></span>
- <span data-ttu-id="ee161-795">**NX_PTR_ERROR** (0x07) geçersiz TLS oturum işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-795">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ee161-796">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ee161-796">Allowed From</span></span>

<span data-ttu-id="ee161-797">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ee161-797">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ee161-798">Örnek</span><span class="sxs-lookup"><span data-stu-id="ee161-798">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="ee161-799">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ee161-799">See Also</span></span>

- <span data-ttu-id="ee161-800">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="ee161-800">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="ee161-801">nx_secure_tls_session_server_callback_set</span><span class="sxs-lookup"><span data-stu-id="ee161-801">nx_secure_tls_session_server_callback_set</span></span>
- <span data-ttu-id="ee161-802">nx_secure_tls_active_certificate_set</span><span class="sxs-lookup"><span data-stu-id="ee161-802">nx_secure_tls_active_certificate_set</span></span>

## <a name="nx_secure_tls_session_x509_client_verify_configure"></a><span data-ttu-id="ee161-803">nx_secure_tls_session_x509_client_verify_configure</span><span class="sxs-lookup"><span data-stu-id="ee161-803">nx_secure_tls_session_x509_client_verify_configure</span></span>

<span data-ttu-id="ee161-804">İstemci X. 509.440 doğrulamasını etkinleştir ve istemci sertifikaları için alan ayır</span><span class="sxs-lookup"><span data-stu-id="ee161-804">Enable client X.509 verification and allocate space for client certificates</span></span>

### <a name="prototype"></a><span data-ttu-id="ee161-805">Prototype</span><span class="sxs-lookup"><span data-stu-id="ee161-805">Prototype</span></span>

```C
UINT  nx_secure_tls_session_x509_client_verify_configure(
                  NX_SECURE_TLS_SESSION *session_ptr,
                  UINT certs_number, VOID *certificate_buffer,
                  ULONG buffer_size);
```

### <a name="description"></a><span data-ttu-id="ee161-806">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-806">Description</span></span>

<span data-ttu-id="ee161-807">Bu hizmet, bir TLS sunucu örneği için isteğe bağlı X. 509.440 Istemci kimlik doğrulamasını sunar.</span><span class="sxs-lookup"><span data-stu-id="ee161-807">This service enables the optional X.509 Client Authentication for a TLS Server instance.</span></span> <span data-ttu-id="ee161-808">Ayrıca, uzak istemci konaktan gelen sertifika zincirlerini işlemek için gereken alanı ayırır.</span><span class="sxs-lookup"><span data-stu-id="ee161-808">It also allocates the space needed to process incoming certificate chains from the remote client host.</span></span> <span data-ttu-id="ee161-809">Uzak istemci tarafından sağlanan sertifikalar, hizmet nx_secure_tls_trusted_certificate_add atanmış olan TLS sunucusu örneğinin güvenilen sertifikalarına karşı doğrulanır *.*</span><span class="sxs-lookup"><span data-stu-id="ee161-809">The certificates supplied by the remote client will be verified against the TLS server instance's trusted certificates, assigned with the service *nx_secure_tls_trusted_certificate_add.*</span></span>

<span data-ttu-id="ee161-810">TLS Istemci modu için, uzak sertifika ayırma gereklidir ve bunun yerine hizmet *nx_secure_tls_remote_certificate_buffer_allocate* kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ee161-810">For TLS Client mode, remote certificate allocation is required and the service *nx_secure_tls_remote_certificate_buffer_allocate* should be used instead.</span></span> <span data-ttu-id="ee161-811">Bir TLS Istemci örneğinde X. 509.440 Istemci kimlik doğrulamasının etkinleştirilmesi hiçbir etkiye sahip olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="ee161-811">Enabling X.509 Client Authentication on a TLS Client instance will have no effect.</span></span>

<span data-ttu-id="ee161-812">*Certificate_buffer* parametresi, gelen uzak sertifikaları ve bu sertifikalar için gereken denetim bloklarını depolamak için ayrılan alana işaret eder.</span><span class="sxs-lookup"><span data-stu-id="ee161-812">The *certificate_buffer* parameter points to space allocated to store the incoming remote certificates and the control blocks needed for those certificates.</span></span> <span data-ttu-id="ee161-813">Arabellek, her sertifikaya verilen eşit bir bölüme sahip sertifika (*certs_number*) sayısına bölünür.</span><span class="sxs-lookup"><span data-stu-id="ee161-813">The buffer will be divided by the number of certificates (*certs_number*) with an equal portion given to each certificate.</span></span> <span data-ttu-id="ee161-814">*Buffer_size* parametresi arabelleğin boyutunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="ee161-814">The *buffer_size* parameter indicates the size of the buffer.</span></span> <span data-ttu-id="ee161-815">Aşağıdaki formül ile, gereken alan bulunabilir:</span><span class="sxs-lookup"><span data-stu-id="ee161-815">The space needed can be found with the following formula:</span></span>

```C
buffer_size = (<expected max number of certificates in chain>) *
             (sizeof(NX_SECURE_X509_CERT) + <max cert size>)
```

<span data-ttu-id="ee161-816">İmzalar için SHA-256 kullanan 2048 bitin RSA anahtarlarına sahip tipik sertifikalar, 1000-2000 bayt aralığındadır.</span><span class="sxs-lookup"><span data-stu-id="ee161-816">Typical certificates with RSA keys of 2048 bits using SHA-256 for signatures are in the range of 1000-2000 bytes.</span></span> <span data-ttu-id="ee161-817">Arabellek, her sertifika için en az sayıda tutmaya yetecek kadar büyük olmalıdır, ancak uzak ana bilgisayar sertifikalarına bağlı olarak, önemli ölçüde daha küçük veya daha büyük olabilir.</span><span class="sxs-lookup"><span data-stu-id="ee161-817">The buffer should be large enough to at least hold that size for each certificate, but depending on the remote host certificates may be significantly smaller or larger.</span></span> <span data-ttu-id="ee161-818">Arabellek gelen sertifikayı tutmak için çok küçük olduğunda, TLS el sıkışması bir hatayla sona erdirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ee161-818">Note that if the buffer is too small to hold the incoming certificate, the TLS handshake will end with an error.</span></span>

### <a name="parameters"></a><span data-ttu-id="ee161-819">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ee161-819">Parameters</span></span>

- <span data-ttu-id="ee161-820">**session_ptr** Daha önce oluşturulmuş bir TLS oturum örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ee161-820">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="ee161-821">**certs_number** Belirtilen arabellekten ayrılacak sertifika sayısı.</span><span class="sxs-lookup"><span data-stu-id="ee161-821">**certs_number** Number of certificates to allocate from the provided buffer.</span></span>
- <span data-ttu-id="ee161-822">**certificate_buffer** Uzak bir ana bilgisayardan alınan sertifikaları tutan arabellek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-822">**certificate_buffer** Pointer to a buffer to hold certificates received from a remote host.</span></span>
- <span data-ttu-id="ee161-823">**Buffer_size** Sertifika arabelleğinin boyutu.</span><span class="sxs-lookup"><span data-stu-id="ee161-823">**buffer_size** Size of the certificate buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="ee161-824">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ee161-824">Return Values</span></span>

- <span data-ttu-id="ee161-825">**NX_SUCCESS** (0x00) sertifikanın başarıyla ayrılması.</span><span class="sxs-lookup"><span data-stu-id="ee161-825">**NX_SUCCESS** (0x00)Successful allocation of certificate.</span></span>
- <span data-ttu-id="ee161-826">**NX_PTR_ERROR** (0x07) geçersiz TLS oturumu veya arabellek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-826">**NX_PTR_ERROR** (0x07) Invalid TLS session or buffer pointer.</span></span>
- <span data-ttu-id="ee161-827">**NX_SECURE_TLS_INSUFFICIENT_CERT_SPACE** (0x12D) sağlanan arabellek çok küçük.</span><span class="sxs-lookup"><span data-stu-id="ee161-827">**NX_SECURE_TLS_INSUFFICIENT_CERT_SPACE** (0x12D) The supplied buffer was too small.</span></span>
- <span data-ttu-id="ee161-828">**NX_INVALID_PARAMETERS** (0x4D) Arabellek istenen sayıda sertifikayı tutmak için çok küçük.</span><span class="sxs-lookup"><span data-stu-id="ee161-828">**NX_INVALID_PARAMETERS** (0x4D) The buffer was too small to hold the desired number of certificates.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ee161-829">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ee161-829">Allowed From</span></span>

<span data-ttu-id="ee161-830">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ee161-830">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ee161-831">Örnek</span><span class="sxs-lookup"><span data-stu-id="ee161-831">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="ee161-832">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ee161-832">See Also</span></span>

- <span data-ttu-id="ee161-833">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="ee161-833">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="ee161-834">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="ee161-834">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="ee161-835">nx_secure_tls_remote_certificate_buffer_allocate</span><span class="sxs-lookup"><span data-stu-id="ee161-835">nx_secure_tls_remote_certificate_buffer_allocate</span></span>

## <a name="nx_secure_tls_session_client_verify_disable"></a><span data-ttu-id="ee161-836">nx_secure_tls_session_client_verify_disable</span><span class="sxs-lookup"><span data-stu-id="ee161-836">nx_secure_tls_session_client_verify_disable</span></span>

<span data-ttu-id="ee161-837">NetX güvenli TLS oturumu için Istemci sertifikası kimlik doğrulamasını devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="ee161-837">Disable Client Certificate Authentication for a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="ee161-838">Prototype</span><span class="sxs-lookup"><span data-stu-id="ee161-838">Prototype</span></span>

```C
UINT  nx_secure_tls_session_client_verify_disable(
                              NX_SECURE_TLS_SESSION *session_ptr);
```

### <a name="description"></a><span data-ttu-id="ee161-839">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-839">Description</span></span>

<span data-ttu-id="ee161-840">Bu hizmet, belirli bir TLS oturumu için Istemci sertifikası kimlik doğrulamasını devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="ee161-840">This service disables Client Certificate Authentication for a specific TLS session.</span></span> <span data-ttu-id="ee161-841">Daha fazla bilgi için bkz. nx_secure_tls_session_client_verify_enable.</span><span class="sxs-lookup"><span data-stu-id="ee161-841">See nx_secure_tls_session_client_verify_enable for more information.</span></span>

### <a name="parameters"></a><span data-ttu-id="ee161-842">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ee161-842">Parameters</span></span>

- <span data-ttu-id="ee161-843">**session_ptr** Bir TLS oturum örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-843">**session_ptr** Pointer to a TLS Session instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="ee161-844">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ee161-844">Return Values</span></span>

- <span data-ttu-id="ee161-845">**NX_SUCCESS** (0x00) başarılı durum değişikliği.</span><span class="sxs-lookup"><span data-stu-id="ee161-845">**NX_SUCCESS** (0x00) Successful state change.</span></span>
- <span data-ttu-id="ee161-846">**NX_PTR_ERROR** (0x07) geçersiz TLS oturum işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-846">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ee161-847">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ee161-847">Allowed From</span></span>

<span data-ttu-id="ee161-848">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ee161-848">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ee161-849">Örnek</span><span class="sxs-lookup"><span data-stu-id="ee161-849">Example</span></span>

```C
/* Disable client certificate authentication for this TLS session.   */
status = nx_secure_tls_session_client_verify_disable(&tls_session);

/* Any new TLS Server sessions using the tls_session control block will not
request certificates from the remote TLS client.  */
```

### <a name="see-also"></a><span data-ttu-id="ee161-850">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ee161-850">See Also</span></span>

- <span data-ttu-id="ee161-851">nx_secure_tls_session_client_verify_enable</span><span class="sxs-lookup"><span data-stu-id="ee161-851">nx_secure_tls_session_client_verify_enable</span></span>
- <span data-ttu-id="ee161-852">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="ee161-852">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="ee161-853">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="ee161-853">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_session_client_verify_enable"></a><span data-ttu-id="ee161-854">nx_secure_tls_session_client_verify_enable</span><span class="sxs-lookup"><span data-stu-id="ee161-854">nx_secure_tls_session_client_verify_enable</span></span>

<span data-ttu-id="ee161-855">NetX güvenli TLS oturumu için Istemci sertifikası kimlik doğrulamasını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="ee161-855">Enable Client Certificate Authentication for a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="ee161-856">Prototype</span><span class="sxs-lookup"><span data-stu-id="ee161-856">Prototype</span></span>

```C
UINT  nx_secure_tls_session_client_verify_enable(
                                NX_SECURE_TLS_SESSION *session_ptr);
```

### <a name="description"></a><span data-ttu-id="ee161-857">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-857">Description</span></span>

<span data-ttu-id="ee161-858">Bu hizmet belirli bir TLS oturumu için Istemci sertifikası kimlik doğrulamasını mümkün bir şekilde sunar.</span><span class="sxs-lookup"><span data-stu-id="ee161-858">This service enables Client Certificate Authentication for a specific TLS session.</span></span> <span data-ttu-id="ee161-859">Bir TLS sunucu örneği için Istemci sertifikası kimlik doğrulamasını etkinleştirme, TLS sunucusunun ilk TLS el sıkışması sırasında herhangi bir uzak TLS Istemcisinden sertifika istemesine neden olur.</span><span class="sxs-lookup"><span data-stu-id="ee161-859">Enabling Client Certificate Authentication for a TLS Server instance will cause the TLS Server to request a certificate from any remote TLS Client during the initial TLS handshake.</span></span> <span data-ttu-id="ee161-860">Uzak TLS Istemcisinden alınan sertifikaya, TLS sunucusunun Istemcinin sertifikaya sahip olduğunu doğrulamak için kullandığı bir CertificateVerify iletisi (Bu sertifikayla ilişkili özel anahtara erişimi vardır) ile birlikte gönderilir.</span><span class="sxs-lookup"><span data-stu-id="ee161-860">The certificate received from the remote TLS Client is accompanied by a CertificateVerify message, which the TLS Server uses to verify that the Client owns the certificate (has access to the private key associated with that certificate).</span></span>

<span data-ttu-id="ee161-861">Belirtilen sertifika doğrulanırsa ve bir X. 509.952 sertifika zinciri aracılığıyla TLS sunucusu güvenilen sertifika deposundaki bir sertifikaya geri izleniyorsa, uzak TLS Istemcisinin kimliği doğrulanır ve el sıkışma devam eder.</span><span class="sxs-lookup"><span data-stu-id="ee161-861">If the provided certificate can be verified and traced back to a certificate in the TLS Server trusted certificate store via an X.509 certificate chain, the remote TLS Client is authenticated and the handshake proceeds.</span></span> <span data-ttu-id="ee161-862">Sertifikayı veya CertificateVerify iletisini işlerken herhangi bir hata olması durumunda, TLS anlaşması bir hatayla biter.</span><span class="sxs-lookup"><span data-stu-id="ee161-862">In case of any errors in processing the certificate or CertificateVerify message, the TLS handshake ends with an error.</span></span>

> [!NOTE]
> <span data-ttu-id="ee161-863">*TLS sunucusunda, güvenilir depodaki en az bir sertifika nx_secure_tls_trusted_certificate_add ile eklenmiş olmalıdır veya kimlik doğrulama her zaman başarısız olur.*</span><span class="sxs-lookup"><span data-stu-id="ee161-863">*The TLS Server must have at least one certificate in its trusted store added with nx_secure_tls_trusted_certificate_add or authentication will always fail.*</span></span>

### <a name="parameters"></a><span data-ttu-id="ee161-864">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ee161-864">Parameters</span></span>

- <span data-ttu-id="ee161-865">**session_ptr** Bir TLS oturum örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-865">**session_ptr** Pointer to a TLS Session instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="ee161-866">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ee161-866">Return Values</span></span>

- <span data-ttu-id="ee161-867">**NX_SUCCESS** (0x00) başarılı durum değişikliği.</span><span class="sxs-lookup"><span data-stu-id="ee161-867">**NX_SUCCESS** (0x00) Successful state change.</span></span>
- <span data-ttu-id="ee161-868">**NX_PTR_ERROR** (0x07) geçersiz TLS oturum işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-868">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ee161-869">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ee161-869">Allowed From</span></span>

<span data-ttu-id="ee161-870">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ee161-870">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ee161-871">Örnek</span><span class="sxs-lookup"><span data-stu-id="ee161-871">Example</span></span>

```C
/* Add a trusted certificate so the TLS Server has something to verify against. */
status = nx_secure_tls_trusted_certificate_add(&tls_session,
                                               &trusted_certificate);

/* Disable client certificate authentication for this TLS session.   */
status = nx_secure_tls_session_client_verify_enable(&tls_session);

/* Any new TLS Server sessions using the tls_session control block will now
request and verify certificates from the remote TLS client.  */
```

### <a name="see-also"></a><span data-ttu-id="ee161-872">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ee161-872">See Also</span></span>

- <span data-ttu-id="ee161-873">nx_secure_tls_session_client_verify_enable</span><span class="sxs-lookup"><span data-stu-id="ee161-873">nx_secure_tls_session_client_verify_enable</span></span>
- <span data-ttu-id="ee161-874">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="ee161-874">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="ee161-875">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="ee161-875">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="ee161-876">nx_secure_tls_trusted_certificate_add</span><span class="sxs-lookup"><span data-stu-id="ee161-876">nx_secure_tls_trusted_certificate_add</span></span>

## <a name="nx_secure_tls_session_create"></a><span data-ttu-id="ee161-877">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="ee161-877">nx_secure_tls_session_create</span></span>

<span data-ttu-id="ee161-878">Güvenli iletişim için bir NetX güvenli TLS oturumu oluşturun</span><span class="sxs-lookup"><span data-stu-id="ee161-878">Create a NetX Secure TLS Session for secure communications</span></span>

### <a name="prototype"></a><span data-ttu-id="ee161-879">Prototype</span><span class="sxs-lookup"><span data-stu-id="ee161-879">Prototype</span></span>

```C
UINT  nx_secure_tls_session_create(NX_SECURE_TLS_SESSION *session_ptr
                                   NX_SECURE_TLS_CRYPTO *cipher_table,
                                   VOID *encryption_metadata_area,
                                   ULONG encryption_metadata_size);
```

### <a name="description"></a><span data-ttu-id="ee161-880">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-880">Description</span></span>

<span data-ttu-id="ee161-881">Bu hizmet, bir ağ bağlantısı üzerinden güvenli TLS iletişimleri kurmak için kullanılmak üzere bir NX_SECURE_TLS_SESSION yapısı örneğini başlatır.</span><span class="sxs-lookup"><span data-stu-id="ee161-881">This service initializes an NX_SECURE_TLS_SESSION structure instance for use in establishing secure TLS communications over a network connection.</span></span>

<span data-ttu-id="ee161-882">Yöntemi, TLS için kullanılacak kullanılabilir şifreleme yöntemleriyle doldurulmuş bir NX_SECURE_TLS_CRYPTO nesnesi alır.</span><span class="sxs-lookup"><span data-stu-id="ee161-882">The method takes a NX_SECURE_TLS_CRYPTO object that is populated with the available cryptographic methods to be used for TLS.</span></span> <span data-ttu-id="ee161-883">*Encryption_metadata_area* , hesaplamalar için NX_SECURE_TLS_CRYPTO tablosundaki şifreleme yöntemleri tarafından kullanılan "meta veriler" için TLS tarafından kullanılmak üzere ayrılmış bir arabelleğe işaret eder.</span><span class="sxs-lookup"><span data-stu-id="ee161-883">The *encryption_metadata_area* points to a buffer allocated for use by TLS for the "metadata" used by the cryptographic methods in the NX_SECURE_TLS_CRYPTO table for calculations.</span></span> <span data-ttu-id="ee161-884">Tablonun boyutu nx_secure_tls_metadata_size_calculate hizmeti kullanılarak belirlenebilir.</span><span class="sxs-lookup"><span data-stu-id="ee161-884">The size of the table can be determined by using the nx_secure_tls_metadata_size_calculate service.</span></span> <span data-ttu-id="ee161-885">Daha fazla bilgi için, Bölüm 3 ' teki "NetX güvenli TLS 'de şifreleme" bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="ee161-885">See the section "Cryptography in NetX Secure TLS" in Chapter 3 for more details.</span></span>

### <a name="parameters"></a><span data-ttu-id="ee161-886">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ee161-886">Parameters</span></span>

- <span data-ttu-id="ee161-887">**session_ptr** Bir TLS oturum örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-887">**session_ptr** Pointer to a TLS Session instance.</span></span>
- <span data-ttu-id="ee161-888">**cipher_table** TLS şifreleme yöntemlerine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ee161-888">**cipher_table** Pointer to TLS cryptographic methods.</span></span>
- <span data-ttu-id="ee161-889">**encryption_metadata_area** Şifreleme meta verileri için boşluk işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-889">**encryption_metadata_area** Pointer to space for cryptography metadata.</span></span>
- <span data-ttu-id="ee161-890">**encryption_metadata_size** Meta veri arabelleğinin boyutu.</span><span class="sxs-lookup"><span data-stu-id="ee161-890">**encryption_metadata_size** Size of the metadata buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="ee161-891">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ee161-891">Return Values</span></span>

- <span data-ttu-id="ee161-892">TLS oturumunun başarıyla başlatılmasından **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="ee161-892">**NX_SUCCESS** (0x00)Successful initialization of the TLS session.</span></span>
- <span data-ttu-id="ee161-893">**NX_PTR_ERROR** (0x07) geçersiz bir Işaretçi kullanmaya çalıştı.</span><span class="sxs-lookup"><span data-stu-id="ee161-893">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>
- <span data-ttu-id="ee161-894">**NX_INVALID_PARAMETERS** (0x4D) belirtilen metotlar için meta veri arabelleği çok küçük.</span><span class="sxs-lookup"><span data-stu-id="ee161-894">**NX_INVALID_PARAMETERS** (0x4D) The metadata buffer was too small for the given methods.</span></span>
- <span data-ttu-id="ee161-895">**NX_SECURE_TLS_UNSUPPORTED_CIPHER** (0x106) ŞIFRELEME tablosunda TLS 'nin etkinleştirilmiş sürümü Için gerekli bir şifre yöntemi sağlanmadı.</span><span class="sxs-lookup"><span data-stu-id="ee161-895">**NX_SECURE_TLS_UNSUPPORTED_CIPHER** (0x106) A required cipher method for the enabled version of TLS was not supplied in the cipher table.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ee161-896">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ee161-896">Allowed From</span></span>

<span data-ttu-id="ee161-897">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ee161-897">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ee161-898">Örnek</span><span class="sxs-lookup"><span data-stu-id="ee161-898">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="ee161-899">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ee161-899">See Also</span></span>

- <span data-ttu-id="ee161-900">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="ee161-900">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="ee161-901">nx_secure_tls_metadata_size_calculate</span><span class="sxs-lookup"><span data-stu-id="ee161-901">nx_secure_tls_metadata_size_calculate</span></span>
- <span data-ttu-id="ee161-902">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="ee161-902">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="ee161-903">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="ee161-903">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="ee161-904">nx_secure_tls_session_end</span><span class="sxs-lookup"><span data-stu-id="ee161-904">nx_secure_tls_session_end</span></span>
- <span data-ttu-id="ee161-905">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="ee161-905">nx_secure_tls_session_send</span></span>
- <span data-ttu-id="ee161-906">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="ee161-906">nx_secure_tls_session_receive</span></span>
- <span data-ttu-id="ee161-907">nx_secure_tls_session_delete</span><span class="sxs-lookup"><span data-stu-id="ee161-907">nx_secure_tls_session_delete</span></span>
- <span data-ttu-id="ee161-908">Bölüm 3 ' te NetX güvenli TLS 'de şifreleme</span><span class="sxs-lookup"><span data-stu-id="ee161-908">Cryptography in NetX Secure TLS in Chapter 3</span></span>

## <a name="nx_secure_tls_session_delete"></a><span data-ttu-id="ee161-909">nx_secure_tls_session_delete</span><span class="sxs-lookup"><span data-stu-id="ee161-909">nx_secure_tls_session_delete</span></span>

<span data-ttu-id="ee161-910">NetX güvenli TLS oturumunu silme</span><span class="sxs-lookup"><span data-stu-id="ee161-910">Delete a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="ee161-911">Prototype</span><span class="sxs-lookup"><span data-stu-id="ee161-911">Prototype</span></span>

```C
UINT  nx_secure_tls_session_delete(NX_SECURE_TLS_SESSION *session_ptr);
```

### <a name="description"></a><span data-ttu-id="ee161-912">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-912">Description</span></span>

<span data-ttu-id="ee161-913">Bu hizmet, bir NX_SECURE_TLS_SESSION yapısı örneğiyle temsil edilen bir TLS oturumunu siler ve o oturum örneğine ait tüm sistem kaynaklarını serbest bırakır.</span><span class="sxs-lookup"><span data-stu-id="ee161-913">This service deletes a TLS session represented by an NX_SECURE_TLS_SESSION structure instance and releases all system resources owned by that session instance.</span></span>

### <a name="parameters"></a><span data-ttu-id="ee161-914">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ee161-914">Parameters</span></span>

- <span data-ttu-id="ee161-915">**session_ptr** Bir TLS oturum örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-915">**session_ptr** Pointer to a TLS Session instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="ee161-916">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ee161-916">Return Values</span></span>

- <span data-ttu-id="ee161-917">TLS oturumunun başarıyla başlatılmasından **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="ee161-917">**NX_SUCCESS** (0x00) Successful initialization of the TLS session.</span></span>
- <span data-ttu-id="ee161-918">**NX_PTR_ERROR** (0x07) geçersiz bir Işaretçi kullanmaya çalıştı.</span><span class="sxs-lookup"><span data-stu-id="ee161-918">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ee161-919">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ee161-919">Allowed From</span></span>

<span data-ttu-id="ee161-920">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ee161-920">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ee161-921">Örnek</span><span class="sxs-lookup"><span data-stu-id="ee161-921">Example</span></span>

```C
/* Delete TLS session.  */
status =  nx_secure_tls_session_delete(&tls_session);


/* If status is NX_SUCCESS the TLS Session was successfully deleted.  */
```

### <a name="see-also"></a><span data-ttu-id="ee161-922">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ee161-922">See Also</span></span>

- <span data-ttu-id="ee161-923">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="ee161-923">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="ee161-924">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="ee161-924">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="ee161-925">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="ee161-925">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="ee161-926">nx_secure_tls_session_end</span><span class="sxs-lookup"><span data-stu-id="ee161-926">nx_secure_tls_session_end</span></span>
- <span data-ttu-id="ee161-927">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="ee161-927">nx_secure_tls_session_send</span></span>
- <span data-ttu-id="ee161-928">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="ee161-928">nx_secure_tls_session_receive</span></span>
- <span data-ttu-id="ee161-929">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="ee161-929">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_session_end"></a><span data-ttu-id="ee161-930">nx_secure_tls_session_end</span><span class="sxs-lookup"><span data-stu-id="ee161-930">nx_secure_tls_session_end</span></span>

<span data-ttu-id="ee161-931">Etkin bir NetX güvenli TLS oturumu sonlandır</span><span class="sxs-lookup"><span data-stu-id="ee161-931">End an active NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="ee161-932">Prototype</span><span class="sxs-lookup"><span data-stu-id="ee161-932">Prototype</span></span>

```C
UINT  nx_secure_tls_session_end(NX_SECURE_TLS_SESSION *session_ptr,
                                    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="ee161-933">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-933">Description</span></span>

<span data-ttu-id="ee161-934">Bu hizmet, TLS CloseNotify iletisini uzak ana bilgisayara göndererek bir NX_SECURE_TLS_SESSION yapısı örneği tarafından temsil edilen bir TLS oturumunu sonlandırır.</span><span class="sxs-lookup"><span data-stu-id="ee161-934">This service ends a TLS session represented by an NX_SECURE_TLS_SESSION structure instance by sending the TLS CloseNotify message to the remote host.</span></span> <span data-ttu-id="ee161-935">Daha sonra hizmet, uzak konağın kendi CloseNotify iletisiyle yanıt vermesini bekler.</span><span class="sxs-lookup"><span data-stu-id="ee161-935">The service then waits for the remote host to respond with its own CloseNotify message.</span></span>

<span data-ttu-id="ee161-936">Uzak ana bilgisayar bir CloseNotify iletisi göndermezse, TLS bu hatayı ve olası bir güvenlik ihlalini kabul eder; bu nedenle, güvenli bir bağlantı için dönüş değerinin denetlenmesi önemlidir.</span><span class="sxs-lookup"><span data-stu-id="ee161-936">If the remote host does not send a CloseNotify message, TLS considers this an error and a possible security breach, so checking the return value is important for a secure connection.</span></span> <span data-ttu-id="ee161-937">**Wait_option** parametresi, hizmetin çağıran iş parçacığına denetim döndürmeden önce Yanıt beklemesi gereken süreyi denetlemek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ee161-937">The **wait_option** parameter can be used to control how long the service should wait for the response before returning control to the calling thread.</span></span>

### <a name="parameters"></a><span data-ttu-id="ee161-938">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ee161-938">Parameters</span></span>

- <span data-ttu-id="ee161-939">**session_ptr** Bir TLS oturum örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-939">**session_ptr** Pointer to a TLS Session instance.</span></span>
- <span data-ttu-id="ee161-940">**wait_option** Hizmetin uzak ana bilgisayardan Yanıt beklemesi gereken süreyi belirtir.</span><span class="sxs-lookup"><span data-stu-id="ee161-940">**wait_option** Indicates how long the service should wait for the response from the remote host.</span></span>

### <a name="return-values"></a><span data-ttu-id="ee161-941">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ee161-941">Return Values</span></span>

- <span data-ttu-id="ee161-942">TLS oturumunun başarıyla başlatılmasından **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="ee161-942">**NX_SUCCESS** (0x00) Successful initialization of the TLS session.</span></span>
- <span data-ttu-id="ee161-943">**NX_SECURE_TLS_NO_CLOSE_RESPONSE** (0x113), zaman aşımından önce uzak ana bilgisayardan bir yanıt almadı.</span><span class="sxs-lookup"><span data-stu-id="ee161-943">**NX_SECURE_TLS_NO_CLOSE_RESPONSE** (0x113) Did not receive a response from the remote host before timing out.</span></span>
- <span data-ttu-id="ee161-944">**NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111), CloseNotify iletisini göndermek için bir paket ayıramadı.</span><span class="sxs-lookup"><span data-stu-id="ee161-944">**NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) Could not allocate a packet to send the CloseNotify message.</span></span>
- <span data-ttu-id="ee161-945">**NX_SECURE_TLS_TCP_SEND_FAILED** (0x109), CloseNotify iletisini TCP yuvası üzerinden gönderemiyor.</span><span class="sxs-lookup"><span data-stu-id="ee161-945">**NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) Could not send the CloseNotify message over the TCP socket.</span></span>
- <span data-ttu-id="ee161-946">**NX_PTR_ERROR** (0x07) geçersiz bir Işaretçi kullanmaya çalıştı.</span><span class="sxs-lookup"><span data-stu-id="ee161-946">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ee161-947">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ee161-947">Allowed From</span></span>

<span data-ttu-id="ee161-948">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ee161-948">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ee161-949">Örnek</span><span class="sxs-lookup"><span data-stu-id="ee161-949">Example</span></span>

```C
/* End TLS session.  */
status =  nx_secure_tls_session_end(&tls_session, NX_WAIT_FOREVER);


/* If status is NX_SUCCESS the TLS Session was successfully ended.  */
```

### <a name="see-also"></a><span data-ttu-id="ee161-950">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ee161-950">See Also</span></span>

- <span data-ttu-id="ee161-951">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="ee161-951">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="ee161-952">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="ee161-952">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="ee161-953">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="ee161-953">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="ee161-954">nx_secure_tls_session_delete</span><span class="sxs-lookup"><span data-stu-id="ee161-954">nx_secure_tls_session_delete</span></span>
- <span data-ttu-id="ee161-955">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="ee161-955">nx_secure_tls_session_send</span></span>
- <span data-ttu-id="ee161-956">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="ee161-956">nx_secure_tls_session_receive</span></span>
- <span data-ttu-id="ee161-957">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="ee161-957">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_session_packet_buffer_set"></a><span data-ttu-id="ee161-958">nx_secure_tls_session_packet_buffer_set</span><span class="sxs-lookup"><span data-stu-id="ee161-958">nx_secure_tls_session_packet_buffer_set</span></span>

<span data-ttu-id="ee161-959">NetX güvenli TLS oturumu için paket yeniden birleştirme arabelleğini ayarlama</span><span class="sxs-lookup"><span data-stu-id="ee161-959">Set the packet reassembly buffer for a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="ee161-960">Prototype</span><span class="sxs-lookup"><span data-stu-id="ee161-960">Prototype</span></span>

```C
UINT  nx_secure_tls_session_packet_buffer_set(
                                    NX_SECURE_TLS_SESSION *session_ptr,
                                    UCHAR *buffer_ptr,
                                    ULONG buffer_size);
```

### <a name="description"></a><span data-ttu-id="ee161-961">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-961">Description</span></span>

<span data-ttu-id="ee161-962">Bu hizmet, bir paket yeniden birleştirme arabelleğini bir TLS oturumuyla ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="ee161-962">This service associates a packet reassembly buffer to a TLS session.</span></span> <span data-ttu-id="ee161-963">Gelen TLS kayıtlarının şifresini çözmek ve ayrıştırmak için, her bir kayıttaki verilerin temel alınan TCP paketlerinden bir araya gelmelidir.</span><span class="sxs-lookup"><span data-stu-id="ee161-963">In order to decrypt and parse incoming TLS records, the data in each record must be assembled from the underlying TCP packets.</span></span> <span data-ttu-id="ee161-964">TLS kayıtlarının boyutu 16KB 'a kadar olabilir (genellikle çok daha küçüktür), bu nedenle tek bir TCP paketine uyamayabilir.</span><span class="sxs-lookup"><span data-stu-id="ee161-964">TLS records can be up to 16KB in size (though typically are much smaller) so may not fit into a single TCP packet.</span></span>

<span data-ttu-id="ee161-965">Gelen ileti boyutunun, 16KB olan TLS kayıt sınırından küçük olacağını biliyorsanız, arabellek boyutu daha küçük hale getirilebilir, ancak bilinmeyen gelen verileri işlemek için arabelleğin mümkün olduğunca büyük olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ee161-965">If you know the incoming message size will be smaller than the TLS record limit of 16KB, the buffer size can be made smaller, but in order to handle unknown incoming data the buffer should be made as large as possible.</span></span> <span data-ttu-id="ee161-966">Gelen bir kayıt sağlanan arabellekten fazlaysa, TLS oturumu bir hatayla sona acaktır.</span><span class="sxs-lookup"><span data-stu-id="ee161-966">If an incoming record is larger than the supplied buffer, the TLS session will end with an error.</span></span>

### <a name="parameters"></a><span data-ttu-id="ee161-967">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ee161-967">Parameters</span></span>

- <span data-ttu-id="ee161-968">**session_ptr** Bir TLS oturum örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-968">**session_ptr** Pointer to a TLS Session instance.</span></span>
- <span data-ttu-id="ee161-969">**buffer_ptr** Paket yeniden birleştirme için kullanılacak TLS arabelleği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-969">**buffer_ptr** Pointer to buffer for TLS to use for packet reassembly.</span></span>
- <span data-ttu-id="ee161-970">**Buffer_size** Sağlanan arabelleğin bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="ee161-970">**buffer_size** Size of the supplied buffer in bytes.</span></span>

### <a name="return-values"></a><span data-ttu-id="ee161-971">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ee161-971">Return Values</span></span>

- <span data-ttu-id="ee161-972">TLS oturumunun başarıyla başlatılmasından **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="ee161-972">**NX_SUCCESS** (0x00) Successful initialization of the TLS session.</span></span>
- <span data-ttu-id="ee161-973">**NX_INVALID_PARAMETERS** (0x4D) geçersiz arabellek veya TLS oturum işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-973">**NX_INVALID_PARAMETERS** (0x4D) Invalid buffer or TLS session pointer.</span></span>
- <span data-ttu-id="ee161-974">**NX_PTR_ERROR** (0x07) geçersiz bir Işaretçi kullanmaya çalıştı.</span><span class="sxs-lookup"><span data-stu-id="ee161-974">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ee161-975">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ee161-975">Allowed From</span></span>

<span data-ttu-id="ee161-976">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ee161-976">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ee161-977">Örnek</span><span class="sxs-lookup"><span data-stu-id="ee161-977">Example</span></span>

```C
/* Buffer for TLS packet reassembly. */
UCHAR tls_packet_buffer[16384];
/* Assign buffer to TLS session.  */
status =  nx_secure_tls_session_packet_buffer_set(&tls_session, tls_packet_buffer,
                                                  sizeof(tls_packet_buffer));


/* If status is NX_SUCCESS the buffer was successfully added.  */
```

### <a name="see-also"></a><span data-ttu-id="ee161-978">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ee161-978">See Also</span></span>

- <span data-ttu-id="ee161-979">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="ee161-979">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="ee161-980">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="ee161-980">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="ee161-981">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="ee161-981">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="ee161-982">nx_secure_tls_session_delete</span><span class="sxs-lookup"><span data-stu-id="ee161-982">nx_secure_tls_session_delete</span></span>
- <span data-ttu-id="ee161-983">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="ee161-983">nx_secure_tls_session_send</span></span>
- <span data-ttu-id="ee161-984">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="ee161-984">nx_secure_tls_session_receive</span></span>
- <span data-ttu-id="ee161-985">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="ee161-985">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_session_protocol_version_override"></a><span data-ttu-id="ee161-986">nx_secure_tls_session_protocol_version_override</span><span class="sxs-lookup"><span data-stu-id="ee161-986">nx_secure_tls_session_protocol_version_override</span></span>

<span data-ttu-id="ee161-987">NetX güvenli TLS oturumu için varsayılan TLS protokol sürümünü geçersiz kılın</span><span class="sxs-lookup"><span data-stu-id="ee161-987">Override the default TLS protocol version for a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="ee161-988">Prototype</span><span class="sxs-lookup"><span data-stu-id="ee161-988">Prototype</span></span>

```C
UINT  nx_secure_tls_session_protocol_version_override(
                              NX_SECURE_TLS_SESSION *session_ptr,
                              USHORT protocol_version);
```

### <a name="description"></a><span data-ttu-id="ee161-989">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-989">Description</span></span>

<span data-ttu-id="ee161-990">Bu hizmet, belirli bir oturum tarafından kullanılan varsayılan (en yeni) TLS protokol sürümünü geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="ee161-990">This service overrides the default (newest) TLS protocol version used by a particular session.</span></span> <span data-ttu-id="ee161-991">Bu, NetX güvenli TLS 'in, derleme zamanında daha yeni TLS sürümlerini devre dışı bırakmadan belirli bir TLS oturumu için daha eski bir TLS sürümünü kullanmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="ee161-991">This enables NetX Secure TLS to use an older version of TLS for a specific TLS Session without disabling newer TLS versions at compile time.</span></span> <span data-ttu-id="ee161-992">Bu, en yeni TLS sürümünü desteklemeyen daha eski bir konakla iletişim kurması gerekebilecek uygulamalarda yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="ee161-992">This may be useful in applications that may need to communicate with an older host that does not support the newest version of TLS.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ee161-993">*Sürüm 5.11 SP3 itibariyle NetX Secure TLS, RFC 7507 ' i (aşağıdaki nota bakın) destekler ve bu API ile daha eski bir sürüme yönelik tüm geçersiz kılma, ClientHello içinde bir geri dönüş SCSV gönderilmesine neden olur. Sunucu, TLS 'in daha yeni bir sürümünü destekliyorsa ve geri dönüş SCSV, ClientHello içinde yer alıyorsa, bu sunucu "uygunsuz geri dönüş" uyarısıyla TLS el sıkışması işlemini iptal eder. SCSV yalnızca sürüm geçersiz kılma özelliği, etkin olandan daha eski bir TLS sürümü olduğunda gönderilir (örn. sürümü TLS 1,2 olarak geçersiz kılarsınız, hiçbir SCSV gönderilmez).*</span><span class="sxs-lookup"><span data-stu-id="ee161-993">*As of version 5.11SP3, NetX Secure TLS supports RFC 7507 (see note below) and any override to an older version with this API will result in a fallback SCSV being sent in the ClientHello. If the server supports a newer version of TLS and the fallback SCSV is included in the ClientHello, that server will abort the TLS handshake with an "Inappropriate Fallback" alert. The SCSV is only sent when the version override is an older version of TLS than is enabled (e.g. if you override the version to TLS 1.2, no SCSV will be sent).*</span></span>

<span data-ttu-id="ee161-994">Protocol_version parametresi için geçerli değerler şu makrolardır: NX_SECURE_TLS_VERSION_TLS_1_0, NX_SECURE_TLS_VERSION_TLS_1_1 ve NX_SECURE_TLS_VERSION_TLS_1_2.</span><span class="sxs-lookup"><span data-stu-id="ee161-994">Valid values for the protocol_version parameter are the following macros: NX_SECURE_TLS_VERSION_TLS_1_0, NX_SECURE_TLS_VERSION_TLS_1_1, and NX_SECURE_TLS_VERSION_TLS_1_2.</span></span>

<span data-ttu-id="ee161-995">NX_SECURE_TLS_DISABLE_TLS_1_1 ve NX_SECURE_TLS_ENABLE_TLS_1_0 makrolar, uygulamaya derlenen TLS sürümlerini denetlemek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ee161-995">The macros NX_SECURE_TLS_DISABLE_TLS_1_1 and NX_SECURE_TLS_ENABLE_TLS_1_0 can be used to control the versions of TLS that are compiled into the application.</span></span> <span data-ttu-id="ee161-996">TLS sürüm 1,2 her zaman etkindir.</span><span class="sxs-lookup"><span data-stu-id="ee161-996">TLS version 1.2 is always enabled.</span></span>

<span data-ttu-id="ee161-997">Uzak ana bilgisayar sağlanan sürümü desteklemiyorsa bağlantı başarısız olur – yalnızca belirtilen geçersiz kılma sürümü NetX güvenli TLS tarafından görüşülecektir.</span><span class="sxs-lookup"><span data-stu-id="ee161-997">Note that if the remote host does not support the supplied version, the connection will fail – only the supplied override version will be negotiated by NetX Secure TLS.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ee161-998">RFC 7507: TLS geri dönüş SCSV.</span><span class="sxs-lookup"><span data-stu-id="ee161-998">RFC 7507: TLS Fallback SCSV.</span></span> <span data-ttu-id="ee161-999">Bu RFC, protokol düşürme anlaşmasını yanlış bir şekilde işlenmiş olan ve bunun yerine geçerli ClientHello iletilerini reddettiği sunuculardan kaynaklanan bir güvenlik sorununu hafifletmek üzere sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="ee161-999">This RFC was introduced to mitigate a security problem that was originally caused by servers that improperly handled protocol downgrade negotiation and instead rejected otherwise valid ClientHello messages.</span></span> <span data-ttu-id="ee161-1000">Bu eski sunucularla uyumlu olmaya devam etmek için bazı TLS istemci uygulamaları başarısız el sıkışmaları ve daha eski TLS sürümü ile yeniden denemeye başlamıştır (örneğin, TLS 1,2 başarısız oldu, TLS 1,1 ' yi deneyin).</span><span class="sxs-lookup"><span data-stu-id="ee161-1000">In an attempt to remain compatible with these old servers, some TLS client applications started to retry failed handshakes with and older TLS version (e.g. TLS 1.2 failed so try TLS 1.1).</span></span> <span data-ttu-id="ee161-1001">Bu geçici çözüm, yeni bir sorun ortaya sunmuştur; bir saldırgan, sunucu daha yeni TLS sürümünü desteklense bile, sunucu bağlantısının başarısız olmasına neden olan bir ağ veya paket hatası ile yapay bir istemciyi indirgemeye zorlayabilir.</span><span class="sxs-lookup"><span data-stu-id="ee161-1001">This workaround however introduced a new problem – an attacker could force a client to downgrade by artificially introducing a network or packet error causing the server connection to fail – even when the server supported the newer TLS version.</span></span> <span data-ttu-id="ee161-1002">Daha eski bir sürüme indirgenerek saldırgan, söz konusu sürümdeki zayıf yönleriyle yararlanabilir (SSLv3<sup>21</sup> , özellıkle de çıkış saldırılarına karşı zayıfdır).</span><span class="sxs-lookup"><span data-stu-id="ee161-1002">By downgrading to an older version the attacker could exploit weaknesses in that version (SSLv3<sup>21</sup> in particular is weak to the POODLE attack).</span></span> <span data-ttu-id="ee161-1003">Bu durumu engellemek için, RFC 7507 ' de, bir TLS istemcisi desteklediği en yeni sürüm olmayan bir TLS<sup></sup> sürümünü kullanırken TLS sunucusuna bildiren "GERI dönüş SCSV" bir ClientHello</span><span class="sxs-lookup"><span data-stu-id="ee161-1003">To prevent this situation, RFC 7507 introdued the "fallback SCSV," a pseudo-ciphersuite<sup>22</sup> sent in the ClientHello that notifies a TLS server when a TLS client is using a TLS version that is not the newest version it supports.</span></span> <span data-ttu-id="ee161-1004">Bu şekilde, daha yeni bir sürümü destekleyen bir sunucu, geri dönüş SCSV 'i içeren bir ClientHello reddedebilir ve düşürme saldırılarının başarılı olmasını önler.</span><span class="sxs-lookup"><span data-stu-id="ee161-1004">This way, a server that supports a newer version can reject a ClientHello containing the fallback SCSV and prevent the downgrade attack from succeeding.</span></span>

21. <span data-ttu-id="ee161-1005">NetX Secure, POOıDLE gibi bilinen ciddi zayıf yanlar nedeniyle SSLv3 uygulamaz.</span><span class="sxs-lookup"><span data-stu-id="ee161-1005">NetX Secure does not implement SSLv3 due to the existence of known serious weaknesses such as POODLE.</span></span>

22. <span data-ttu-id="ee161-1006">Sözde ciphersuite veya SCSV (sinyal şifreleme paketi değeri), eski TLS sürümlerinde kullanılamayan özelliklerle ilgili etkin TLS uygulamalarını işaret etmek için kullanılan ayrılmış bir ciphersuite numarasıdır.</span><span class="sxs-lookup"><span data-stu-id="ee161-1006">A pseudo-ciphersuite, or SCSV (Signaling Cipher Suite Value), is a reserved ciphersuite number that is used to signal enabled TLS implementations about features that were not available in older TLS versions.</span></span> <span data-ttu-id="ee161-1007">Geri dönüş SCSV ve TLS_EMPTY_RENEGOTIATION_INFO_SCSV (RFC 5746) örnektir.</span><span class="sxs-lookup"><span data-stu-id="ee161-1007">The fallback SCSV and the TLS_EMPTY_RENEGOTIATION_INFO_SCSV (RFC 5746) are examples.</span></span>

### <a name="parameters"></a><span data-ttu-id="ee161-1008">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ee161-1008">Parameters</span></span>

- <span data-ttu-id="ee161-1009">**session_ptr** Bir TLS oturum örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-1009">**session_ptr** Pointer to a TLS Session instance.</span></span>
- <span data-ttu-id="ee161-1010">**protocol_version** Kullanılacak belirli TLS sürümü için TLS sürümü makrosu.</span><span class="sxs-lookup"><span data-stu-id="ee161-1010">**protocol_version** TLS version macro for the specific TLS version to use.</span></span>

### <a name="return-values"></a><span data-ttu-id="ee161-1011">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ee161-1011">Return Values</span></span>

- <span data-ttu-id="ee161-1012">**NX_SUCCESS** (0x00) başarılı durum değişikliği.</span><span class="sxs-lookup"><span data-stu-id="ee161-1012">**NX_SUCCESS** (0x00) Successful state change.</span></span>
- <span data-ttu-id="ee161-1013">**NX_PTR_ERROR** (0x07) geçersiz TLS oturum işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-1013">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>
- <span data-ttu-id="ee161-1014">**NX_SECURE_TLS_UNSUPPORTED_TLS_VERSION** (0x110) bilinen ancak desteklenmeyen TLS sürümü.</span><span class="sxs-lookup"><span data-stu-id="ee161-1014">**NX_SECURE_TLS_UNSUPPORTED_TLS_VERSION** (0x110) Known but unsupported TLS version.</span></span>
- <span data-ttu-id="ee161-1015">**NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0x10F) geçersiz protokol sürümü.</span><span class="sxs-lookup"><span data-stu-id="ee161-1015">**NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0x10F) Invalid protocol version.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ee161-1016">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ee161-1016">Allowed From</span></span>

<span data-ttu-id="ee161-1017">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ee161-1017">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ee161-1018">Örnek</span><span class="sxs-lookup"><span data-stu-id="ee161-1018">Example</span></span>

```C
/* Set the protocol version to be used to TLSv1.1. */
status = nx_secure_tls_session_protocol_version_override(&tls_session,
                                              NX_SECURE_TLS_VERSION_TLS_1_1);

/* This TLS Session will use TLSv1.1 for the handshake and TLS session. */
status = nx_secure_tls_session_start(&tls_session, &tcp_socket, NX_WAIT_FOREVER);
```

### <a name="see-also"></a><span data-ttu-id="ee161-1019">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ee161-1019">See Also</span></span>

- <span data-ttu-id="ee161-1020">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="ee161-1020">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="ee161-1021">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="ee161-1021">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_session_receive"></a><span data-ttu-id="ee161-1022">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="ee161-1022">nx_secure_tls_session_receive</span></span>

<span data-ttu-id="ee161-1023">NetX güvenli TLS oturumundan veri alma</span><span class="sxs-lookup"><span data-stu-id="ee161-1023">Receive data from a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="ee161-1024">Prototype</span><span class="sxs-lookup"><span data-stu-id="ee161-1024">Prototype</span></span>

```C
UINT  nx_secure_tls_session_receive(NX_SECURE_TLS_SESSION *session_ptr,
                                    NX_PACKET **packet_ptr,
                                    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="ee161-1025">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-1025">Description</span></span>

<span data-ttu-id="ee161-1026">Bu hizmet, belirtilen etkin TLS oturumundan verileri alır ve bu verilerin şifresini, NX_PACKET parametresindeki çağırana sağlamadan önce işleme alır.</span><span class="sxs-lookup"><span data-stu-id="ee161-1026">This service receives data from the specified active TLS session, handling the decryption of that data before providing it to the caller in the NX_PACKET parameter.</span></span> <span data-ttu-id="ee161-1027">Belirtilen oturumda hiçbir veri sıraya alınmaz, çağrı sağlanan bekleme seçeneğine göre askıya alınır.</span><span class="sxs-lookup"><span data-stu-id="ee161-1027">If no data is queued in the specified session, the call suspends based on the supplied wait option.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ee161-1028">*NX_SUCCESS döndürülürse, uygulama artık gerekli olmadığında alınan paketi serbest bırakmaktan sorumludur.*</span><span class="sxs-lookup"><span data-stu-id="ee161-1028">*If NX_SUCCESS is returned, the application is responsible for releasing the received packet when it is no longer needed.*</span></span>

### <a name="parameters"></a><span data-ttu-id="ee161-1029">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ee161-1029">Parameters</span></span>

- <span data-ttu-id="ee161-1030">**session_ptr** Bir TLS oturum örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-1030">**session_ptr** Pointer to a TLS Session instance.</span></span>
- <span data-ttu-id="ee161-1031">**packet_ptr** Ayrılmış bir TLS paket işaretçisine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ee161-1031">**packet_ptr** Pointer to an allocated TLS packet pointer.</span></span>
- <span data-ttu-id="ee161-1032">**wait_option** Hizmetin, döndürmeden önce uzak ana bilgisayardan bir paket için bekleyeceği süreyi belirtir.</span><span class="sxs-lookup"><span data-stu-id="ee161-1032">**wait_option** Indicates how long the service should wait for a packet from the remote host before returning.</span></span>

### <a name="return-values"></a><span data-ttu-id="ee161-1033">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ee161-1033">Return Values</span></span>

- <span data-ttu-id="ee161-1034">TLS oturumunun başarıyla başlatılmasından **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="ee161-1034">**NX_SUCCESS** (0x00) Successful initialization of the TLS session.</span></span>
- <span data-ttu-id="ee161-1035">**NX_NO_PACKET** (0x01) veri alınmadı.</span><span class="sxs-lookup"><span data-stu-id="ee161-1035">**NX_NO_PACKET** (0x01) No data received.</span></span>
- <span data-ttu-id="ee161-1036">**NX_NOT_CONNECTED** (0x38) temel alınan TCP yuvası artık bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="ee161-1036">**NX_NOT_CONNECTED** (0x38) The underlying TCP socket is no longer connected.</span></span>
- <span data-ttu-id="ee161-1037">**NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0x108) alınan bir ileti, kimlik doğrulama karma denetiminde başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="ee161-1037">**NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0x108) A received message failed an authentication hash check.</span></span>
- <span data-ttu-id="ee161-1038">**NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0x10F) alınan bir ileti üstbilgisinde bilinmeyen bir protokol sürümü içeriyordu.</span><span class="sxs-lookup"><span data-stu-id="ee161-1038">**NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0x10F) A received message contained an unknown protocol version in its header.</span></span>
- <span data-ttu-id="ee161-1039">**NX_SECURE_TLS_ALERT_RECEIVED** (0x114) uzak ana BILGISAYARDAN bir TLS uyarısı aldı.</span><span class="sxs-lookup"><span data-stu-id="ee161-1039">**NX_SECURE_TLS_ALERT_RECEIVED** (0x114) Received a TLS alert from the remote host.</span></span>
- <span data-ttu-id="ee161-1040">**NX_PTR_ERROR** (0x07) geçersiz bir Işaretçi kullanmaya çalıştı.</span><span class="sxs-lookup"><span data-stu-id="ee161-1040">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>
- <span data-ttu-id="ee161-1041">**NX_SECURE_TLS_SESSION_UNINITIALIZED** (0x101) sağlanan TLS oturumu başlatılmadı.</span><span class="sxs-lookup"><span data-stu-id="ee161-1041">**NX_SECURE_TLS_SESSION_UNINITIALIZED** (0x101) The supplied TLS session was not initialized.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ee161-1042">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ee161-1042">Allowed From</span></span>

<span data-ttu-id="ee161-1043">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ee161-1043">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ee161-1044">Örnek</span><span class="sxs-lookup"><span data-stu-id="ee161-1044">Example</span></span>

```C
/* Receive a packet from an active TLS session previously created and started with
nx_secure_tls_session_start. Wait until a packet is received, blocking otherwise.
*/
status =  nx_secure_tls_session_receive(&tls_session, &packet_ptr,
NX_WAIT_FOREVER);


/* If status is NX_SUCCESS the received packet is pointed to by  "packet_ptr". */
```

### <a name="see-also"></a><span data-ttu-id="ee161-1045">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ee161-1045">See Also</span></span>

- <span data-ttu-id="ee161-1046">nx_tcp_socket_receive</span><span class="sxs-lookup"><span data-stu-id="ee161-1046">nx_tcp_socket_receive</span></span>
- <span data-ttu-id="ee161-1047">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="ee161-1047">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="ee161-1048">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="ee161-1048">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="ee161-1049">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="ee161-1049">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="ee161-1050">nx_secure_tls_session_delete</span><span class="sxs-lookup"><span data-stu-id="ee161-1050">nx_secure_tls_session_delete</span></span>
- <span data-ttu-id="ee161-1051">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="ee161-1051">nx_secure_tls_session_send</span></span>
- <span data-ttu-id="ee161-1052">nx_secure_tls_session_end</span><span class="sxs-lookup"><span data-stu-id="ee161-1052">nx_secure_tls_session_end</span></span>
- <span data-ttu-id="ee161-1053">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="ee161-1053">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_session_renegotiate_callback_set"></a><span data-ttu-id="ee161-1054">nx_secure_tls_session_renegotiate_callback_set</span><span class="sxs-lookup"><span data-stu-id="ee161-1054">nx_secure_tls_session_renegotiate_callback_set</span></span>

<span data-ttu-id="ee161-1055">Oturum yeniden anlaşması başlangıcında çağrılacak bir geri çağırma atayın</span><span class="sxs-lookup"><span data-stu-id="ee161-1055">Assign a callback that will be invoked at the beginning of a session renegotiation</span></span>

### <a name="prototype"></a><span data-ttu-id="ee161-1056">Prototype</span><span class="sxs-lookup"><span data-stu-id="ee161-1056">Prototype</span></span>

```C
UINT  nx_secure_tls_ session_renegotiate_callback_set (
                  NX_SECURE_TLS_SESSION *tls_session,
                  ULONG (*func_ptr)(struct NX_SECURE_TLS_SESSION_struct
                  *session));
```

### <a name="description"></a><span data-ttu-id="ee161-1057">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-1057">Description</span></span>

<span data-ttu-id="ee161-1058">Bu hizmet, uzak ana bilgisayardan bir oturum yeniden anlaşma el sıkışma iletisi alındığında çağrılacak bir TLS oturumuna geri çağırma işlemi atar.</span><span class="sxs-lookup"><span data-stu-id="ee161-1058">This service assigns a callback to a TLS session that will be invoked whenever the first message of a session renegotiation handshake is received from the remote host.</span></span>

<span data-ttu-id="ee161-1059">Geri çağırma işlevi, bir yeniden anlaşma anlaşmasını oluşturan uygulamaya bildirim olarak tasarlanmıştır. uygulama, geri aramadan sıfır olmayan bir değer döndürerek TLS oturumunu sonlandırarak TLS oturumunun bir hata ile sonlanmasına neden olacak.</span><span class="sxs-lookup"><span data-stu-id="ee161-1059">The callback function is intended as a notification to the application that a renegotiation handshake is beginning – the application may choose to terminate the TLS session by returning any non-zero value from the callback which will cause TLS to end the TLS session with an error.</span></span> <span data-ttu-id="ee161-1060">Uygulama yeniden anlaşmaya devam etmek isterse, geri çağırma NX_SUCCESS döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="ee161-1060">If the application wishes to proceed with the renegotiation, the callback should return NX_SUCCESS.</span></span>

> [!NOTE]
> <span data-ttu-id="ee161-1061">*TLS yeniden anlaşması semantiği nedeniyle, uzak sunucudan bir HelloRequest alındığında, ancak istemci yeniden anlaşmayı başlattığında değil, NetX güvenli TLS Istemcileri için geri arama çağrılacaktır. NetX güvenli TLS sunucularında, bir yeniden anlaşma ClientHello alındığında (etkin bir TLS oturumu bağlamında alınan herhangi bir ClientHello) geri çağırma işlemi çağrılır. Bu, TLS sunucusu uzak istemcinin yanıt verdiği bir merhaba Istek göndereceği için, geri aramanın uzak ana bilgisayar veya yerel uygulamanın yeniden anlaşmayı başlattığını belirtir.*</span><span class="sxs-lookup"><span data-stu-id="ee161-1061">*Due to the semantics of TLS renegotiation, the callback will be invoked for NetX Secure TLS Clients whenever a HelloRequest is received from the remote server, but not when the client initiates the renegotiation. On NetX Secure TLS Servers, the callback will be invoked whenever a renegotiation ClientHello is received (any ClientHello received in the context of an active TLS session). This means that the callback will be invoked whether the remote host or the local application has initiated the renegotiation because the TLS server will send a HelloRequest to which the remote client will respond.*</span></span>

<span data-ttu-id="ee161-1062">NetX güvenli TLS, yeniden anlaşma el sıkışmaları 'nın ortadaki adam saldırılarına maruz olmamasını sağlamak için, RFC 5746 ' den güvenli yeniden anlaşma alma uzantısını uygular.</span><span class="sxs-lookup"><span data-stu-id="ee161-1062">NetX Secure TLS implements the Secure Renegotiation Inidication Extension from RFC 5746 to ensure that renegotiation handshakes are not subject to man-in-the-middle attacks.</span></span>

### <a name="parameters"></a><span data-ttu-id="ee161-1063">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ee161-1063">Parameters</span></span>

- <span data-ttu-id="ee161-1064">**session_ptr** TLS oturum örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-1064">**session_ptr** Pointer to TLS Session instance.</span></span>
- <span data-ttu-id="ee161-1065">**func_ptr** Geri arama işlevine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ee161-1065">**func_ptr** Pointer to callback function.</span></span>

### <a name="return-values"></a><span data-ttu-id="ee161-1066">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ee161-1066">Return Values</span></span>

- <span data-ttu-id="ee161-1067">**NX_SUCCESS** (0x00) geri aramanın başarıyla atanması.</span><span class="sxs-lookup"><span data-stu-id="ee161-1067">**NX_SUCCESS** (0x00) Successful assignment of callback.</span></span>
- <span data-ttu-id="ee161-1068">**NX_PTR_ERROR** (0x07) geri çağırma IşLEVI veya TLS oturumu için geçersiz bir Işaretçi kullanmayı denedi.</span><span class="sxs-lookup"><span data-stu-id="ee161-1068">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer for the callback function or TLS session.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ee161-1069">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ee161-1069">Allowed From</span></span>

<span data-ttu-id="ee161-1070">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ee161-1070">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ee161-1071">Örnek</span><span class="sxs-lookup"><span data-stu-id="ee161-1071">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="ee161-1072">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ee161-1072">See Also</span></span>

- <span data-ttu-id="ee161-1073">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="ee161-1073">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="ee161-1074">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="ee161-1074">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="ee161-1075">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="ee161-1075">nx_secure_tls_session_receive</span></span>
- <span data-ttu-id="ee161-1076">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="ee161-1076">nx_secure_tls_session_send</span></span>
- <span data-ttu-id="ee161-1077">nx_secure_tls_session_renegotiate</span><span class="sxs-lookup"><span data-stu-id="ee161-1077">nx_secure_tls_session_renegotiate</span></span>

## <a name="nx_secure_tls_session_renegotiate"></a><span data-ttu-id="ee161-1078">nx_secure_tls_session_renegotiate</span><span class="sxs-lookup"><span data-stu-id="ee161-1078">nx_secure_tls_session_renegotiate</span></span>

<span data-ttu-id="ee161-1079">Uzak konakla oturum yeniden anlaşma anlaşmasını başlatma</span><span class="sxs-lookup"><span data-stu-id="ee161-1079">Initiate a session renegotiation handshake with the remote host</span></span>

### <a name="prototype"></a><span data-ttu-id="ee161-1080">Prototype</span><span class="sxs-lookup"><span data-stu-id="ee161-1080">Prototype</span></span>

```C
UINT  nx_secure_tls_ session_renegotiate (
                  NX_SECURE_TLS_SESSION *tls_session,
                  UINT wait_option);
```

### <a name="description"></a><span data-ttu-id="ee161-1081">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-1081">Description</span></span>

<span data-ttu-id="ee161-1082">Bu hizmet, bağlı bir uzak TLS ana bilgisayarıyla oturum yeniden *anlaşma* anlaşmasını başlatır.</span><span class="sxs-lookup"><span data-stu-id="ee161-1082">This service initiates a session *renegotiation* handshake with a connected remote TLS host.</span></span> <span data-ttu-id="ee161-1083">Yeniden anlaşma, daha önce oluşturulmuş bir TLS oturumunun bağlamı içindeki ikinci bir TLS el sıkışmasını içerir.</span><span class="sxs-lookup"><span data-stu-id="ee161-1083">A renegotiation consists of a second TLS handshake within the context of a previously-established TLS session.</span></span> <span data-ttu-id="ee161-1084">Yeni oturum anahtarları üretilene ve Changeccrypspec iletileri alınıp, tüm iletileri şifrelemek için yeni anahtarların kullanıldığı zamana kadar her yeni el sıkışma iletisi, TLS oturumu kullanılarak şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="ee161-1084">Each of the new handshake messages is encrypted using the TLS session until new session keys are generated and ChangeCipherSpec messages are exchanged, at which time the new keys are used to encrypt all messages.</span></span>

<span data-ttu-id="ee161-1085">Bir yeniden anlaşma, bir TLS oturumu kurulduktan sonra herhangi bir zamanda başlatılabilir.</span><span class="sxs-lookup"><span data-stu-id="ee161-1085">A renegotiation can be initiated at any time once a TLS session is established.</span></span> <span data-ttu-id="ee161-1086">Bir TLS el sıkışması sırasında veya bir TLS oturumu oluşturulmadan önce yeniden anlaşma denendiğinde hiçbir işlem yapılmaz.</span><span class="sxs-lookup"><span data-stu-id="ee161-1086">If a renegotiation is attempted during a TLS handshake or before a TLS session is established no action will be taken.</span></span>

> [!NOTE]
> <span data-ttu-id="ee161-1087">*Bu hizmet çağrıldığında tüm TLS el sıkışması gerçekleştirilecek ve geri döndürülen durum geçerli TLS ayarlarına ve oturum parametrelerine göre farklılık gösterecektir.*</span><span class="sxs-lookup"><span data-stu-id="ee161-1087">*An entire TLS handshake will be performed when this service is invoked so the time to completion and returned status will vary depending on the current TLS settings and session parameters.*</span></span>

<span data-ttu-id="ee161-1088">NetX güvenli TLS, yeniden anlaşma el sıkışmaları 'nın ortadaki adam saldırılarına maruz olmamasını sağlamak için, RFC 5746 ' den güvenli yeniden anlaşma alma uzantısını uygular.</span><span class="sxs-lookup"><span data-stu-id="ee161-1088">NetX Secure TLS implements the Secure Renegotiation Inidication Extension from RFC 5746 to ensure that renegotiation handshakes are not subject to man-in-the-middle attacks.</span></span>

### <a name="parameters"></a><span data-ttu-id="ee161-1089">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ee161-1089">Parameters</span></span>

- <span data-ttu-id="ee161-1090">**session_ptr** TLS oturum örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-1090">**session_ptr** Pointer to TLS Session instance.</span></span>
- <span data-ttu-id="ee161-1091">**wait_option** Hizmetin, döndürmeden önce uzak ana bilgisayardan bir paket için bekleyeceği süreyi belirtir.</span><span class="sxs-lookup"><span data-stu-id="ee161-1091">**wait_option** Indicates how long the service should wait for a packet from the remote host before returning.</span></span> <span data-ttu-id="ee161-1092">Bu, TLS içindeki tüm NetX hizmetlerine geçirilir.</span><span class="sxs-lookup"><span data-stu-id="ee161-1092">This is passed to all NetX services within TLS.</span></span>

### <a name="return-values"></a><span data-ttu-id="ee161-1093">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ee161-1093">Return Values</span></span>

- <span data-ttu-id="ee161-1094">**NX_SUCCESS** (0x00) başarılı yeniden anlaşma.</span><span class="sxs-lookup"><span data-stu-id="ee161-1094">**NX_SUCCESS** (0x00) Successful renegotiation.</span></span>
- <span data-ttu-id="ee161-1095">**NX_NO_PACKET** (0x01) veri alınmadı.</span><span class="sxs-lookup"><span data-stu-id="ee161-1095">**NX_NO_PACKET** (0x01) No data received.</span></span>
- <span data-ttu-id="ee161-1096">**NX_NOT_CONNECTED** (0x38) temel alınan TCP yuvası artık bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="ee161-1096">**NX_NOT_CONNECTED** (0x38) The underlying TCP socket is no longer connected.</span></span>
- <span data-ttu-id="ee161-1097">**NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0x108) alınan bir ileti, kimlik doğrulama karma denetiminde başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="ee161-1097">**NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0x108) A received message failed an authentication hash check.</span></span>
- <span data-ttu-id="ee161-1098">**NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0x10F) alınan bir ileti üstbilgisinde bilinmeyen bir protokol sürümü içeriyordu.</span><span class="sxs-lookup"><span data-stu-id="ee161-1098">**NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0x10F) A received message contained an unknown protocol version in its header.</span></span>
- <span data-ttu-id="ee161-1099">**NX_SECURE_TLS_ALERT_RECEIVED** (0x114) uzak ana BILGISAYARDAN bir TLS uyarısı aldı.</span><span class="sxs-lookup"><span data-stu-id="ee161-1099">**NX_SECURE_TLS_ALERT_RECEIVED** (0x114) Received a TLS alert from the remote host.</span></span>
- <span data-ttu-id="ee161-1100">**NX_SECURE_TLS_RENEGOTIATION_SESSION_INACTIVE** (0x134) yerel veya uzak TLS oturumu etkin değil, yeniden anlaşma olanaksız hale yapılıyor.</span><span class="sxs-lookup"><span data-stu-id="ee161-1100">**NX_SECURE_TLS_RENEGOTIATION_SESSION_INACTIVE** (0x134) The local or remote TLS session is inactive, making renegotiation impossible.</span></span>
- <span data-ttu-id="ee161-1101">**NX_SECURE_TLS_RENEGOTIATION_FAILURE** (0x13a) uzak ana BILGISAYAR, SCSV veya güvenli yeniden anlaşma uzantısı sağlamadı ve bu nedenle yeniden anlaşma yapılamaz.</span><span class="sxs-lookup"><span data-stu-id="ee161-1101">**NX_SECURE_TLS_RENEGOTIATION_FAILURE** (0x13A) The remote host did not provide either the SCSV or Secure Renegotiation Extension and thus renegotiation cannot be performed.</span></span>
- <span data-ttu-id="ee161-1102">**NX_PTR_ERROR** (0x07) geçersiz bir Işaretçi kullanmaya çalıştı.</span><span class="sxs-lookup"><span data-stu-id="ee161-1102">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>
- <span data-ttu-id="ee161-1103">**NX_SECURE_TLS_SESSION_UNINITIALIZED** (0x101) sağlanan TLS oturumu başlatılmadı.</span><span class="sxs-lookup"><span data-stu-id="ee161-1103">**NX_SECURE_TLS_SESSION_UNINITIALIZED** (0x101) The supplied TLS session was not initialized.</span></span>
- <span data-ttu-id="ee161-1104">**NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) temel alınan paket ayırması başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="ee161-1104">**NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) Underlying packet allocation failed.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ee161-1105">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ee161-1105">Allowed From</span></span>

<span data-ttu-id="ee161-1106">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ee161-1106">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ee161-1107">Örnek</span><span class="sxs-lookup"><span data-stu-id="ee161-1107">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="ee161-1108">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ee161-1108">See Also</span></span>

- <span data-ttu-id="ee161-1109">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="ee161-1109">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="ee161-1110">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="ee161-1110">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="ee161-1111">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="ee161-1111">nx_secure_tls_session_receive</span></span>
- <span data-ttu-id="ee161-1112">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="ee161-1112">nx_secure_tls_session_send</span></span>
- <span data-ttu-id="ee161-1113">nx_secure_tls_session_renegotiation_callback_set</span><span class="sxs-lookup"><span data-stu-id="ee161-1113">nx_secure_tls_session_renegotiation_callback_set</span></span>

## <a name="nx_secure_tls_session_reset"></a><span data-ttu-id="ee161-1114">nx_secure_tls_session_reset</span><span class="sxs-lookup"><span data-stu-id="ee161-1114">nx_secure_tls_session_reset</span></span>

<span data-ttu-id="ee161-1115">NetX güvenli TLS oturumunu Temizleme ve sıfırlama</span><span class="sxs-lookup"><span data-stu-id="ee161-1115">Clear out and reset a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="ee161-1116">Prototype</span><span class="sxs-lookup"><span data-stu-id="ee161-1116">Prototype</span></span>

```C
UINT  nx_secure_tls_session_reset (NX_SECURE_TLS_SESSION *session_ptr);
```

### <a name="description"></a><span data-ttu-id="ee161-1117">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-1117">Description</span></span>

<span data-ttu-id="ee161-1118">Bu hizmet bir TLS oturumunu temizler ve mevcut bir TLS oturum nesnesinin yeni bir oturum için yeniden kullanılabilmesi için oturum oluşturulmuşdaymışsınız gibi durumu sıfırlar.</span><span class="sxs-lookup"><span data-stu-id="ee161-1118">This service clears out a TLS session and resets the state as if the session had just been created so an existing TLS session object can be re-used for a new session.</span></span>

### <a name="parameters"></a><span data-ttu-id="ee161-1119">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ee161-1119">Parameters</span></span>

- <span data-ttu-id="ee161-1120">**session_ptr** Bir TLS oturum örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-1120">**session_ptr** Pointer to a TLS Session instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="ee161-1121">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ee161-1121">Return Values</span></span>

- <span data-ttu-id="ee161-1122">TLS oturumunun başarıyla başlatılmasından **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="ee161-1122">**NX_SUCCESS** (0x00) Successful initialization of the TLS session.</span></span>
- <span data-ttu-id="ee161-1123">**NX_INVALID_PARAMETERS** (0x4D) geçersiz TLS oturum işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-1123">**NX_INVALID_PARAMETERS** (0x4D) Invalid TLS session pointer.</span></span>
- <span data-ttu-id="ee161-1124">**NX_PTR_ERROR** (0x07) geçersiz bir Işaretçi kullanmaya çalıştı.</span><span class="sxs-lookup"><span data-stu-id="ee161-1124">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ee161-1125">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ee161-1125">Allowed From</span></span>

<span data-ttu-id="ee161-1126">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ee161-1126">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ee161-1127">Örnek</span><span class="sxs-lookup"><span data-stu-id="ee161-1127">Example</span></span>

```C
/* Reset a TLS session.  */
status =  nx_secure_tls_session_reset(&tls_session);


/* If status is NX_SUCCESS the session was successfully reset and may be reused.*/
```

### <a name="see-also"></a><span data-ttu-id="ee161-1128">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ee161-1128">See Also</span></span>

- <span data-ttu-id="ee161-1129">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="ee161-1129">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="ee161-1130">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="ee161-1130">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="ee161-1131">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="ee161-1131">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="ee161-1132">nx_secure_tls_session_delete</span><span class="sxs-lookup"><span data-stu-id="ee161-1132">nx_secure_tls_session_delete</span></span>
- <span data-ttu-id="ee161-1133">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="ee161-1133">nx_secure_tls_session_send</span></span>
- <span data-ttu-id="ee161-1134">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="ee161-1134">nx_secure_tls_session_receive</span></span>
- <span data-ttu-id="ee161-1135">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="ee161-1135">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_session_send"></a><span data-ttu-id="ee161-1136">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="ee161-1136">nx_secure_tls_session_send</span></span>

<span data-ttu-id="ee161-1137">NetX güvenli TLS oturumu aracılığıyla veri gönderme</span><span class="sxs-lookup"><span data-stu-id="ee161-1137">Send data through a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="ee161-1138">Prototype</span><span class="sxs-lookup"><span data-stu-id="ee161-1138">Prototype</span></span>

```C
UINT  nx_secure_tls_session_send(NX_SECURE_TLS_SESSION *session_ptr,
                                    NX_PACKET *packet_ptr,
                                    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="ee161-1139">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-1139">Description</span></span>

<span data-ttu-id="ee161-1140">Bu hizmet, belirtilen etkin TLS oturumunu kullanarak ve bu verilerin uzak ana bilgisayara gönderilmeden önce şifrelemesini işleyerek, sağlanan NX_PACKET verileri gönderir.</span><span class="sxs-lookup"><span data-stu-id="ee161-1140">This service sends data in the supplied NX_PACKET, using the specified active TLS session, and handling the encryption of that data before sending it to the remote host.</span></span> <span data-ttu-id="ee161-1141">Alıcının en son tanıtılan pencere boyutu bu istekten azsa, hizmet isteğe bağlı olarak, belirtilen bekleme seçeneklerine göre askıya alınır.</span><span class="sxs-lookup"><span data-stu-id="ee161-1141">If the receiver's last advertised window size is less than this request, the service optionally suspends based on the wait options specified.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ee161-1142">*Bir hata döndürülmediği takdirde, uygulama bu çağrıdan sonra paketi serbest bırakmamalıdır. Bunu yapmak öngörülemeyen sonuçlara neden olur çünkü ağ sürücüsü iletim sonrasında paketi serbest bırakacaktır.*</span><span class="sxs-lookup"><span data-stu-id="ee161-1142">*Unless an error is returned, the application should not release the packet after this call. Doing so will cause unpredictable results because the network driver will release the packet after transmission.*</span></span>

### <a name="parameters"></a><span data-ttu-id="ee161-1143">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ee161-1143">Parameters</span></span>

- <span data-ttu-id="ee161-1144">**session_ptr** Bir TLS oturum örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-1144">**session_ptr** Pointer to a TLS Session instance.</span></span>
- <span data-ttu-id="ee161-1145">**packet_ptr** Gönderilecek verileri içeren TLS paketine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ee161-1145">**packet_ptr** Pointer to a TLS packet containing data to be sent.</span></span>
- <span data-ttu-id="ee161-1146">**wait_option** İstek alıcının pencere boyutundan fazlaysa hizmetin nasıl davranacağını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ee161-1146">**wait_option** Defines how the service behaves if the request is greater than the window size of the receiver.</span></span>

### <a name="return-values"></a><span data-ttu-id="ee161-1147">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ee161-1147">Return Values</span></span>

- <span data-ttu-id="ee161-1148">TLS oturumunun başarıyla başlatılmasından **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="ee161-1148">**NX_SUCCESS** (0x00) Successful initialization of the TLS session.</span></span>
- <span data-ttu-id="ee161-1149">**NX_NO_PACKET** (0x01) veri alınmadı.</span><span class="sxs-lookup"><span data-stu-id="ee161-1149">**NX_NO_PACKET** (0x01) No data received.</span></span>
- <span data-ttu-id="ee161-1150">**NX_NOT_CONNECTED** (0x38) temel alınan TCP yuvası artık bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="ee161-1150">**NX_NOT_CONNECTED** (0x38) The underlying TCP socket is no longer connected.</span></span>
- <span data-ttu-id="ee161-1151">**NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) temel alınan TCP yuvası gönderme başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="ee161-1151">**NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) The underlying TCP socket send failed.</span></span>
- <span data-ttu-id="ee161-1152">**NX_PTR_ERROR** (0x07) geçersiz bir Işaretçi kullanmaya çalıştı.</span><span class="sxs-lookup"><span data-stu-id="ee161-1152">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>
- <span data-ttu-id="ee161-1153">**NX_SECURE_TLS_SESSION_UNINITIALIZED** (0x101) sağlanan TLS oturumu başlatılmadı.</span><span class="sxs-lookup"><span data-stu-id="ee161-1153">**NX_SECURE_TLS_SESSION_UNINITIALIZED** (0x101) The supplied TLS session was not initialized.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ee161-1154">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ee161-1154">Allowed From</span></span>

<span data-ttu-id="ee161-1155">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ee161-1155">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ee161-1156">Örnek</span><span class="sxs-lookup"><span data-stu-id="ee161-1156">Example</span></span>

```C
/* Send a packet using an active TLS session previously created and started with
nx_secure_tls_session_start. Wait until a packet is sent, blocking otherwise.   */
status =  nx_secure_tls_session_send(&tls_session, &packet_ptr, NX_WAIT_FOREVER);


/* If status is NX_SUCCESS the packet has been sent. */
```

### <a name="see-also"></a><span data-ttu-id="ee161-1157">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ee161-1157">See Also</span></span>

- <span data-ttu-id="ee161-1158">nx_tcp_socket_receive</span><span class="sxs-lookup"><span data-stu-id="ee161-1158">nx_tcp_socket_receive</span></span>
- <span data-ttu-id="ee161-1159">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="ee161-1159">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="ee161-1160">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="ee161-1160">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="ee161-1161">nx_secure_tls_packet_allocate</span><span class="sxs-lookup"><span data-stu-id="ee161-1161">nx_secure_tls_packet_allocate</span></span>
- <span data-ttu-id="ee161-1162">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="ee161-1162">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="ee161-1163">nx_secure_tls_session_delete</span><span class="sxs-lookup"><span data-stu-id="ee161-1163">nx_secure_tls_session_delete</span></span>
- <span data-ttu-id="ee161-1164">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="ee161-1164">nx_secure_tls_session_receive</span></span>
- <span data-ttu-id="ee161-1165">nx_secure_tls_session_end</span><span class="sxs-lookup"><span data-stu-id="ee161-1165">nx_secure_tls_session_end</span></span>
- <span data-ttu-id="ee161-1166">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="ee161-1166">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_session_server_callback_set"></a><span data-ttu-id="ee161-1167">nx_secure_tls_session_server_callback_set</span><span class="sxs-lookup"><span data-stu-id="ee161-1167">nx_secure_tls_session_server_callback_set</span></span>

<span data-ttu-id="ee161-1168">TLS sunucusu el sıkışmasının başlangıcında çağırmak üzere TLS için bir geri çağırma ayarlayın</span><span class="sxs-lookup"><span data-stu-id="ee161-1168">Set up a callback for TLS to invoke at the beginning of a TLS Server handshake</span></span>

### <a name="prototype"></a><span data-ttu-id="ee161-1169">Prototype</span><span class="sxs-lookup"><span data-stu-id="ee161-1169">Prototype</span></span>

```C
UINT  nx_secure_tls_ session_server_callback_set (
                 NX_SECURE_TLS_SESSION *tls_session,
                 ULONG (*func_ptr)(NX_SECURE_TLS_SESSION *tls_session,
                                   NX_SECURE_TLS_HELLO_EXTENSION
                                   *extensions, UINT num_extensions));
```

### <a name="description"></a><span data-ttu-id="ee161-1170">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-1170">Description</span></span>

<span data-ttu-id="ee161-1171">Bu hizmet, TLS sunucusu el sıkışması bir ClientHello iletisi aldığında TLS 'nin çağıracağı bir TLS oturumuna bir işlev işaretçisi atar.</span><span class="sxs-lookup"><span data-stu-id="ee161-1171">This service assigns a function pointer to a TLS session that TLS will invoke when a TLS Server handshake has received a ClientHello message.</span></span> <span data-ttu-id="ee161-1172">Geri arama işlevi, bir uygulamanın giriş veya karar verme gerektiren alınan ClientHello iletisindeki TLS uzantılarını işlemesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="ee161-1172">The callback function allows an application to process any TLS extensions from the received ClientHello message that require input or decision making.</span></span>

<span data-ttu-id="ee161-1173">Geri çağırma, TLS oturum denetim bloğu ve NX_SECURE_TLS_HELLO_EXTENSION nesnelerinden oluşan bir dizi ile yürütülür.</span><span class="sxs-lookup"><span data-stu-id="ee161-1173">The callback is executed with the invoking TLS session control block and an array of NX_SECURE_TLS_HELLO_EXTENSION objects.</span></span> <span data-ttu-id="ee161-1174">Uzantı nesnelerinin dizisi, belirli bir uzantıyı bulacak ve ayrıştıracak bir yardımcı işleve geçirilmesi amaçlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="ee161-1174">The array of extension objects is intended to be passed into a helper function that will find and parse a specific extension.</span></span> <span data-ttu-id="ee161-1175">Merhaba iletilerde sunulan TLS uzantılarını ayrıştırır örnek bir yardımcı işlev için bkz. *nx_secure_tls_session_sni_extension_parse*.</span><span class="sxs-lookup"><span data-stu-id="ee161-1175">For an example helper function that parses TLS extensions provided in hello messages, see *nx_secure_tls_session_sni_extension_parse*.</span></span>

<span data-ttu-id="ee161-1176">Sunucu geri çağırması, TLS sunucusu için *nx_secure_tls_active_certificate_set* kullanarak etkin kimlik sertifikasını seçmek için de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ee161-1176">The server callback may also be used to select the active identity certificate using *nx_secure_tls_active_certificate_set* for the TLS Server.</span></span> <span data-ttu-id="ee161-1177">Bu, çoğu zaman bir Sunucu Adı Belirtme (SNı) uzantısına yanıt olarak oluşur ve bu da bir TLS Istemcisinin hangi sunucuyu iletişim kurmaya çalıştığını belirlemesine izin verir.</span><span class="sxs-lookup"><span data-stu-id="ee161-1177">This will most often occur in response to a Server Name Indication (SNI) extension which allows a TLS Client to indicate which server it is attempting to contact.</span></span> <span data-ttu-id="ee161-1178">Daha fazla bilgi için *nx_secure_tls_session_sni_extension_parse* ve *nx_secure_tls_active_certificate_set* başvurularına bakın.</span><span class="sxs-lookup"><span data-stu-id="ee161-1178">See the references for *nx_secure_tls_session_sni_extension_parse* and *nx_secure_tls_active_certificate_set* for more information.</span></span>

### <a name="parameters"></a><span data-ttu-id="ee161-1179">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ee161-1179">Parameters</span></span>

- <span data-ttu-id="ee161-1180">**session_ptr** Daha önce oluşturulmuş bir TLS oturum örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ee161-1180">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="ee161-1181">**func_ptr** TLS sunucusu geri çağırma işlevine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ee161-1181">**func_ptr** Pointer to the TLS Server callback function.</span></span>

### <a name="return-values"></a><span data-ttu-id="ee161-1182">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ee161-1182">Return Values</span></span>

- <span data-ttu-id="ee161-1183">Işlev işaretçisinin başarılı bir şekilde ayrılması **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="ee161-1183">**NX_SUCCESS** (0x00) Successful allocation of Function pointer.</span></span>
- <span data-ttu-id="ee161-1184">**NX_PTR_ERROR** (0x07) geçersiz TLS oturum işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-1184">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ee161-1185">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ee161-1185">Allowed From</span></span>

<span data-ttu-id="ee161-1186">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ee161-1186">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ee161-1187">Örnek</span><span class="sxs-lookup"><span data-stu-id="ee161-1187">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="ee161-1188">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ee161-1188">See Also</span></span>

- <span data-ttu-id="ee161-1189">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="ee161-1189">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="ee161-1190">nx_secure_tls_session_client_callback_set</span><span class="sxs-lookup"><span data-stu-id="ee161-1190">nx_secure_tls_session_client_callback_set</span></span>
- <span data-ttu-id="ee161-1191">nx_secure_tls_active_certificate_set</span><span class="sxs-lookup"><span data-stu-id="ee161-1191">nx_secure_tls_active_certificate_set</span></span>
- <span data-ttu-id="ee161-1192">nx_secure_tls_session_sni_extension_parse</span><span class="sxs-lookup"><span data-stu-id="ee161-1192">nx_secure_tls_session_sni_extension_parse</span></span>
- <span data-ttu-id="ee161-1193">nx_secure_tls_server_certificate_add</span><span class="sxs-lookup"><span data-stu-id="ee161-1193">nx_secure_tls_server_certificate_add</span></span>
- <span data-ttu-id="ee161-1194">nx_secure_tls_server_certificate_find</span><span class="sxs-lookup"><span data-stu-id="ee161-1194">nx_secure_tls_server_certificate_find</span></span>

## <a name="nx_secure_tls_session_sni_extension_parse"></a><span data-ttu-id="ee161-1195">nx_secure_tls_session_sni_extension_parse</span><span class="sxs-lookup"><span data-stu-id="ee161-1195">nx_secure_tls_session_sni_extension_parse</span></span>

<span data-ttu-id="ee161-1196">TLS Istemcisinden alınan Sunucu Adı Belirtme (SNı) uzantısını ayrıştırma</span><span class="sxs-lookup"><span data-stu-id="ee161-1196">Parse a Server Name Indication (SNI) extension received from a TLS Client</span></span>

### <a name="prototype"></a><span data-ttu-id="ee161-1197">Prototype</span><span class="sxs-lookup"><span data-stu-id="ee161-1197">Prototype</span></span>

```C
UINT  nx_secure_tls_session_sni_extension_parse(
                                    NX_SECURE_TLS_SESSION *session_ptr,
                                    NX_SECURE_TLS_HELLO_EXTENSION
                                    *extensions,
                                    UINT num_extensions,
                                    NX_SECURE_X509_DNS_NAME *dns_name);
```

### <a name="description"></a><span data-ttu-id="ee161-1198">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-1198">Description</span></span>

<span data-ttu-id="ee161-1199">Bu hizmetin, nx_secure_tls_session_server_callback_set kullanarak bir TLS oturumuna eklenen bir TLS sunucusu oturumu geri çağırması içinden çağrılması amaçlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="ee161-1199">This service is intended to be called from within a TLS Server session callback, added to a TLS session using nx_secure_tls_session_server_callback_set.</span></span> <span data-ttu-id="ee161-1200">Geri çağırma, uzak bir TLS istemcisinden bir ClientHello iletisinin alınması sonrasında çağrılır ve kullanılabilir uzantıların bir dizisi (ve dizideki uzantı sayısı) sağlanır.</span><span class="sxs-lookup"><span data-stu-id="ee161-1200">The callback is invoked following the reception of a ClientHello message from a remote TLS client and is supplied an array of available extensions (and the number of extensions in the array).</span></span> <span data-ttu-id="ee161-1201">Bu dizi ve uzunluğu, mevcut bir SNı uzantısı olup olmadığını belirtmek için doğrudan bu yordama geçirilebilir. yoksa, istemcinin SNı uzantısını hiçbir şekilde kabul etmedi (Bu bir hata değil) olarak NX_SECURE_TLS_EXTENSION_NOT_FOUND döndürülür.</span><span class="sxs-lookup"><span data-stu-id="ee161-1201">That array and its length can be passed directly to this routine to determine if there is an SNI extension present – if not, NX_SECURE_TLS_EXTENSION_NOT_FOUND is returned indicating simply that the client opted not to provice the SNI extension (this is not an error).</span></span>

<span data-ttu-id="ee161-1202">SNı uzantısı bulunursa, TLS istemcisi tarafından sağlanan X. 509.440 DNS adı dns_name yapısında döndürülür.</span><span class="sxs-lookup"><span data-stu-id="ee161-1202">If the SNI extension is found, the X.509 DNS name supplied by the TLS client is returned in the dns_name structure.</span></span> <span data-ttu-id="ee161-1203">Şu anda SNı uzantısı yalnızca, uzak istemciye hangi kimlik sertifikasının gönderileceğini belirleyebilmek için TLS sunucusu tarafından kullanılabilen tek bir DNS ad girişi sağlar. \* \*</span><span class="sxs-lookup"><span data-stu-id="ee161-1203">Currently, the SNI extension only supplies a single DNS name entry, which may be used by the TLS server to determine which identity certificate to send to the remote client.\*\*</span></span>

<span data-ttu-id="ee161-1204">NX_SECURE_X509_DNS_NAME yapısı, DNS adını alan *nx_secure_x509_dns_name* BIR uşar dizesi olarak ve *nx_secure_x509_dns_name_length* ad dizesinin uzunluğu olarak içerir.</span><span class="sxs-lookup"><span data-stu-id="ee161-1204">The NX_SECURE_X509_DNS_NAME structure simply contains the DNS name as a UCHAR string in the field *nx_secure_x509_dns_name* and the length of the name string in *nx_secure_x509_dns_name_length*.</span></span> <span data-ttu-id="ee161-1205">Makro NX_SECURE_X509_DNS_NAME_MAX nx_secure_x509_dns_name arabelleğinin boyutunu denetler.</span><span class="sxs-lookup"><span data-stu-id="ee161-1205">The macro NX_SECURE_X509_DNS_NAME_MAX controls the size of the nx_secure_x509_dns_name buffer.</span></span>

### <a name="parameters"></a><span data-ttu-id="ee161-1206">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ee161-1206">Parameters</span></span>

- <span data-ttu-id="ee161-1207">**session_ptr** Bir TLS oturum örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-1207">**session_ptr** Pointer to a TLS Session instance.</span></span>
- <span data-ttu-id="ee161-1208">**Uzantılar** Bir TLS Merhaba uzantısı dizisine yönelik işaretçi (oturum geri çağırmada).</span><span class="sxs-lookup"><span data-stu-id="ee161-1208">**extensions** Pointer to an array of TLS Hello extensions (from session callback).</span></span>
- <span data-ttu-id="ee161-1209">**num_extensions** Dizideki uzantı sayısı (oturum geri çağrısından).</span><span class="sxs-lookup"><span data-stu-id="ee161-1209">**num_extensions** Number of extensions in array (from session callback).</span></span>
- <span data-ttu-id="ee161-1210">**dns_name** SNı uzantısında sağlanan DNS adını döndürür.</span><span class="sxs-lookup"><span data-stu-id="ee161-1210">**dns_name** Return DNS name supplied in the SNI extension.</span></span>

### <a name="return-values"></a><span data-ttu-id="ee161-1211">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ee161-1211">Return Values</span></span>

- <span data-ttu-id="ee161-1212">Uzantının başarılı ayrıştırması **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="ee161-1212">**NX_SUCCESS** (0x00) Successful parsing of the extension.</span></span>
- <span data-ttu-id="ee161-1213">**NX_PTR_ERROR** (0x07) geçersiz uzantılar DIZISI veya TLS oturum işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-1213">**NX_PTR_ERROR** (0x07) Invalid extensions array or TLS session pointer.</span></span>
- <span data-ttu-id="ee161-1214">**NX_SECURE_TLS_EXTENSION_NOT_FOUND** (0x136) SNI uzantısı bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="ee161-1214">**NX_SECURE_TLS_EXTENSION_NOT_FOUND** (0x136) SNI extension not found.</span></span>
- <span data-ttu-id="ee161-1215">**NX_SECURE_TLS_SNI_EXTENSION_INVALID** (0x137) SNI uzantı biçimi geçersizdi.</span><span class="sxs-lookup"><span data-stu-id="ee161-1215">**NX_SECURE_TLS_SNI_EXTENSION_INVALID** (0x137) SNI extension format was invalid.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ee161-1216">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ee161-1216">Allowed From</span></span>

<span data-ttu-id="ee161-1217">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ee161-1217">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ee161-1218">Örnek</span><span class="sxs-lookup"><span data-stu-id="ee161-1218">Example</span></span>

### <a name="see-also"></a><span data-ttu-id="ee161-1219">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ee161-1219">See Also</span></span>

- <span data-ttu-id="ee161-1220">nx_secure_tls_session_server_callback_set</span><span class="sxs-lookup"><span data-stu-id="ee161-1220">nx_secure_tls_session_server_callback_set</span></span>
- <span data-ttu-id="ee161-1221">nx_secure_tls_session_client_callback_set</span><span class="sxs-lookup"><span data-stu-id="ee161-1221">nx_secure_tls_session_client_callback_set</span></span>
- <span data-ttu-id="ee161-1222">nx_secure_tls_server_callback_set</span><span class="sxs-lookup"><span data-stu-id="ee161-1222">nx_secure_tls_server_callback_set</span></span>
- <span data-ttu-id="ee161-1223">nx_secure_tls_active_certificate_set</span><span class="sxs-lookup"><span data-stu-id="ee161-1223">nx_secure_tls_active_certificate_set</span></span>

## <a name="nx_secure_tls_session_sni_extension_set"></a><span data-ttu-id="ee161-1224">nx_secure_tls_session_sni_extension_set</span><span class="sxs-lookup"><span data-stu-id="ee161-1224">nx_secure_tls_session_sni_extension_set</span></span>

<span data-ttu-id="ee161-1225">Bir Sunucu Adı Belirtme (SNı) uzantısı DNS adını uzak bir sunucuya göndermek üzere ayarla</span><span class="sxs-lookup"><span data-stu-id="ee161-1225">Set a Server Name Indication (SNI) extension DNS name to send to a remote Server</span></span>

### <a name="prototype"></a><span data-ttu-id="ee161-1226">Prototype</span><span class="sxs-lookup"><span data-stu-id="ee161-1226">Prototype</span></span>

```C
UINT  nx_secure_tls_session_sni_extension_set(
                                    NX_SECURE_TLS_SESSION *session_ptr,
                                    NX_SECURE_X509_DNS_NAME *dns_name);
```

### <a name="description"></a><span data-ttu-id="ee161-1227">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-1227">Description</span></span>

<span data-ttu-id="ee161-1228">Bu hizmet, bir TLS Istemci uygulamasının, Sunucu Adı Belirtme (SNı) TLS uzantısını kullanarak uzak bir TLS sunucusuna tercih edilen sunucu DNS adı sağlamasına izin verir.</span><span class="sxs-lookup"><span data-stu-id="ee161-1228">This service allows a TLS Client application to provide a preferred server DNS name to a remote TLS server using the Server Name Indication (SNI) TLS extension.</span></span> <span data-ttu-id="ee161-1229">SNı uzantısı, sunucunun belirtilen sunucu tercihini temel alarak uygun kimlik sertifikası ve parametrelerini seçmesine olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="ee161-1229">The SNI extension allows the server to select the proper identity certificate and parameters based on the client's indicated server preference.</span></span> <span data-ttu-id="ee161-1230">SNı uzantısı Şu anda yalnızca gönderilecek tek bir DNS adını, dolayısıyla tekil ad parametresini destekliyor.</span><span class="sxs-lookup"><span data-stu-id="ee161-1230">The SNI extension currently only supports a single DNS name to be sent, hence the singular name parameter.</span></span> <span data-ttu-id="ee161-1231">Dns_name parametresi *nx_secure_x509_dns_name_initialize* birlikte başlatılmalıdır ve istemcinin tercih edilen sunucusunu içerecek şekilde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ee161-1231">The dns_name parameter must be initialized with *nx_secure_x509_dns_name_initialize* and will contain the client's preferred server.</span></span> <span data-ttu-id="ee161-1232">Uzantı adını kaldırmak için bu hizmeti NX_NULL bir "dns_name" parametre değeri ile çağırmanız yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="ee161-1232">To unset the extension name, simply call this service with a "dns_name" parameter value of NX_NULL.</span></span>

<span data-ttu-id="ee161-1233">NX_SECURE_X509_DNS_NAME yapısı, DNS adını alan  *nx_secure_x509_dns_name* BIR uşar dizesi olarak ve *nx_secure_x509_dns_name_length* ad dizesinin uzunluğu olarak içerir.</span><span class="sxs-lookup"><span data-stu-id="ee161-1233">The NX_SECURE_X509_DNS_NAME structure simply contains the DNS name as a UCHAR string in the field  *nx_secure_x509_dns_name* and the length of the name string in *nx_secure_x509_dns_name_length*.</span></span> <span data-ttu-id="ee161-1234">Makro NX_SECURE_X509_DNS_NAME_MAX nx_secure_x509_dns_name arabelleğinin boyutunu denetler.</span><span class="sxs-lookup"><span data-stu-id="ee161-1234">The macro  NX_SECURE_X509_DNS_NAME_MAX controls the size of the nx_secure_x509_dns_name buffer.</span></span>

> [!NOTE]
> <span data-ttu-id="ee161-1235">*Nx_secure_tls_session_start çağrılmadan önce bu yordamın çağrılması gerekir veya ClientHello SNı uzantısını içermemelidir.*</span><span class="sxs-lookup"><span data-stu-id="ee161-1235">*This routine must be called before nx_secure_tls_session_start is invoked or the ClientHello will not contain the SNI extension.*</span></span>

### <a name="parameters"></a><span data-ttu-id="ee161-1236">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ee161-1236">Parameters</span></span>

- <span data-ttu-id="ee161-1237">**session_ptr** Bir TLS oturum örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-1237">**session_ptr** Pointer to a TLS Session instance.</span></span>
- <span data-ttu-id="ee161-1238">**dns_name** Uygulama tarafından sağlanan DNS adı.</span><span class="sxs-lookup"><span data-stu-id="ee161-1238">**dns_name** DNS name supplied by the application.</span></span>

### <a name="return-values"></a><span data-ttu-id="ee161-1239">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ee161-1239">Return Values</span></span>

- <span data-ttu-id="ee161-1240">DNS sunucusu adının başarıyla eklenmesi **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="ee161-1240">**NX_SUCCESS** (0x00) Successful addition of DNS server name.</span></span>
- <span data-ttu-id="ee161-1241">**NX_PTR_ERROR** (0x07) geçersiz DNS adı veya TLS oturum işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-1241">**NX_PTR_ERROR** (0x07) Invalid DNS name or TLS session pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ee161-1242">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ee161-1242">Allowed From</span></span>

<span data-ttu-id="ee161-1243">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ee161-1243">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ee161-1244">Örnek</span><span class="sxs-lookup"><span data-stu-id="ee161-1244">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="ee161-1245">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ee161-1245">See Also</span></span>

- <span data-ttu-id="ee161-1246">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="ee161-1246">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="ee161-1247">nx_secure_x509_dns_name_initialize</span><span class="sxs-lookup"><span data-stu-id="ee161-1247">nx_secure_x509_dns_name_initialize</span></span>

## <a name="nx_secure_tls_session_start"></a><span data-ttu-id="ee161-1248">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="ee161-1248">nx_secure_tls_session_start</span></span>

<span data-ttu-id="ee161-1249">NetX güvenli TLS oturumu başlatma</span><span class="sxs-lookup"><span data-stu-id="ee161-1249">Start a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="ee161-1250">Prototype</span><span class="sxs-lookup"><span data-stu-id="ee161-1250">Prototype</span></span>

```C
UINT  nx_secure_tls_session_start(NX_SECURE_TLS_SESSION *session_ptr,
                                  NX_TCP_SOCKET *tcp_socket_ptr,
                                  ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="ee161-1251">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-1251">Description</span></span>

<span data-ttu-id="ee161-1252">Bu hizmet, sağlanan TLS oturum denetim bloğunu ve bağlı bir TCP yuvasını kullanarak bir TLS oturumu başlatır.</span><span class="sxs-lookup"><span data-stu-id="ee161-1252">This service starts a TLS session using the supplied TLS session control block and a connected TCP socket.</span></span> <span data-ttu-id="ee161-1253">Nx_tcp_client_socket_connect veya nx_tcp_server_socket_accept başarılı bir çağrıdan sonra TCP bağlantısının zaten tamamlanmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ee161-1253">The TCP connection must already be complete following a successful call to either nx_tcp_client_socket_connect or nx_tcp_server_socket_accept.</span></span>

<span data-ttu-id="ee161-1254">Bu hizmet, TCP yuvasından TLS oturumunun (Istemci veya sunucu) türünü belirleyecek.</span><span class="sxs-lookup"><span data-stu-id="ee161-1254">This service will determine the type of TLS session (Client or Server) from the TCP socket.</span></span>

<span data-ttu-id="ee161-1255">Bekle seçeneği, TLS el sıkışması sürerken hizmetin nasıl davranacağını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ee161-1255">The wait option defines how the service behaves while the TLS handshake is in progress.</span></span>

### <a name="parameters"></a><span data-ttu-id="ee161-1256">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ee161-1256">Parameters</span></span>

- <span data-ttu-id="ee161-1257">**session_ptr** Bir TLS oturum örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-1257">**session_ptr** Pointer to a TLS Session instance.</span></span>
- <span data-ttu-id="ee161-1258">**tcp_socket_ptr** Bağlı TCP yuvasına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ee161-1258">**tcp_socket_ptr** Pointer to a connected TCP socket.</span></span>
- <span data-ttu-id="ee161-1259">**wait_option** TLS el sıkışması sürerken hizmetin nasıl davranacağını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ee161-1259">**wait_option** Defines how the service behaves while the TLS handshake is in progress.</span></span>

### <a name="return-values"></a><span data-ttu-id="ee161-1260">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ee161-1260">Return Values</span></span>

- <span data-ttu-id="ee161-1261">TLS oturumunun başarıyla başlatılmasından **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="ee161-1261">**NX_SUCCESS** (0x00) Successful initialization of the TLS session.</span></span>
- <span data-ttu-id="ee161-1262">**NX_NOT_CONNECTED** (0x38) temel alınan TCP yuvası artık bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="ee161-1262">**NX_NOT_CONNECTED** (0x38) The underlying TCP socket is no longer connected.</span></span>
- <span data-ttu-id="ee161-1263">**NX_SECURE_TLS_UNRECOGNIZED_MESSAGE_TYPE** (0x102) ALıNAN bir TLS ileti türü yanlış.</span><span class="sxs-lookup"><span data-stu-id="ee161-1263">**NX_SECURE_TLS_UNRECOGNIZED_MESSAGE_TYPE** (0x102) A received TLS message type is incorrect.</span></span>
- <span data-ttu-id="ee161-1264">**NX_SECURE_TLS_UNSUPPORTED_CIPHER** (0x106) uzak ana bilgisayar tarafından sağlanmış bir şifre desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="ee161-1264">**NX_SECURE_TLS_UNSUPPORTED_CIPHER** (0x106) A cipher provided by the remote host is not supported.</span></span>
- <span data-ttu-id="ee161-1265">TLS el sıkışması sırasında **NX_SECURE_TLS_HANDSHAKE_FAILURE** (0x107) ileti işleme başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="ee161-1265">**NX_SECURE_TLS_HANDSHAKE_FAILURE** (0x107) Message processing during the TLS handshake has failed.</span></span>
- <span data-ttu-id="ee161-1266">**NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0x108) gelen bir ILETI karma Mac denetiminde başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="ee161-1266">**NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0x108) An incoming message failed a hash MAC check.</span></span>
- <span data-ttu-id="ee161-1267">**NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) temel alınan TCP yuvası gönderme başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="ee161-1267">**NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) An underlying TCP socket send failed.</span></span>
- <span data-ttu-id="ee161-1268">**NX_SECURE_TLS_INCORRECT_MESSAGE_LENGTH** (0x10a) gelen iletide geçersiz uzunluk alanı vardı.</span><span class="sxs-lookup"><span data-stu-id="ee161-1268">**NX_SECURE_TLS_INCORRECT_MESSAGE_LENGTH** (0x10A) An incoming message had an invalid length field.</span></span>
- <span data-ttu-id="ee161-1269">**NX_SECURE_TLS_BAD_CIPHERSPEC** (0x10b) gelen bir Changecyaspec iletisi hatalı.</span><span class="sxs-lookup"><span data-stu-id="ee161-1269">**NX_SECURE_TLS_BAD_CIPHERSPEC** (0x10B) An incoming ChangeCipherSpec message was incorrect.</span></span>
- <span data-ttu-id="ee161-1270">**NX_SECURE_TLS_INVALID_SERVER_CERT** (0x10c) uzak TLS sunucusunu tanımlamak Için gelen bir TLS sertifikası kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="ee161-1270">**NX_SECURE_TLS_INVALID_SERVER_CERT** (0x10C) An incoming TLS certificate is unusable for identifying the remote TLS server.</span></span>
- <span data-ttu-id="ee161-1271">**NX_SECURE_TLS_UNSUPPORTED_PUBLIC_CIPHER** (0x10d) uzak ana bilgisayar tarafından sunulan ortak anahtar şifresi desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="ee161-1271">**NX_SECURE_TLS_UNSUPPORTED_PUBLIC_CIPHER** (0x10D) The public-key cipher provided by the remote host is unsupported.</span></span>
- <span data-ttu-id="ee161-1272">**NX_SECURE_TLS_NO_SUPPORTED_CIPHERS** (0x10e) uzak ana bilgisayar, NETX güvenli TLS yığını tarafından desteklenen ciphersuites belirtti.</span><span class="sxs-lookup"><span data-stu-id="ee161-1272">**NX_SECURE_TLS_NO_SUPPORTED_CIPHERS** (0x10E) The remote host has indicated no ciphersuites that are supported by the NetX Secure TLS stack.</span></span>
- <span data-ttu-id="ee161-1273">**NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0x10F) ALıNAN bir TLS iletisinde üst bilgisinde BILINMEYEN bir TLS sürümü vardı.</span><span class="sxs-lookup"><span data-stu-id="ee161-1273">**NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0x10F) A received TLS message had an unknown TLS version in its header.</span></span>
- <span data-ttu-id="ee161-1274">**NX_SECURE_TLS_UNSUPPORTED_TLS_VERSION** (0x110) ALıNAN bir TLS iletisinde, üstbilgisinde bilinen ancak desteklenmeyen bir TLS sürümü vardı.</span><span class="sxs-lookup"><span data-stu-id="ee161-1274">**NX_SECURE_TLS_UNSUPPORTED_TLS_VERSION** (0x110) A received TLS message had a known but unsupported TLS version in its header.</span></span>
- <span data-ttu-id="ee161-1275">**NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) BIR iç TLS paket ayırması başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="ee161-1275">**NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) An internal TLS packet allocation failed.</span></span>
- <span data-ttu-id="ee161-1276">**NX_SECURE_TLS_INVALID_CERTIFICATE** (0x112) uzak ana bilgisayar geçersiz bir sertifika sağladı.</span><span class="sxs-lookup"><span data-stu-id="ee161-1276">**NX_SECURE_TLS_INVALID_CERTIFICATE** (0x112) The remote host provided an invalid certificate.</span></span>
- <span data-ttu-id="ee161-1277">**NX_SECURE_TLS_ALERT_RECEIVED** (0x114) uzak ana bilgisayar bir hatayı BELIRTEN ve TLS oturumunu sonlandıran bir uyarı gönderdi.</span><span class="sxs-lookup"><span data-stu-id="ee161-1277">**NX_SECURE_TLS_ALERT_RECEIVED** (0x114) The remote host sent an alert indicating an error and ending the TLS session.</span></span>
- <span data-ttu-id="ee161-1278">**NX_SECURE_TLS_MISSING_CRYPTO_ROUTINE** (0x13b) ciphersuite tablosundaki BIR girdinin null işlev işaretçisi vardı.</span><span class="sxs-lookup"><span data-stu-id="ee161-1278">**NX_SECURE_TLS_MISSING_CRYPTO_ROUTINE** (0x13B) An entry in the ciphersuite table had a NULL function pointer.</span></span>
- <span data-ttu-id="ee161-1279">**NX_SECURE_TLS_INAPPROPRIATE_FALLBACK** (0x146) BIR uzak TLS ClientHello, GERI dönüş SCSV bir sürüm geri dönüşü içeriyordu.</span><span class="sxs-lookup"><span data-stu-id="ee161-1279">**NX_SECURE_TLS_INAPPROPRIATE_FALLBACK** (0x146) A remote TLS ClientHello included the fallback SCSV andattempted a version fallback.</span></span>
- <span data-ttu-id="ee161-1280">**NX_PTR_ERROR** (0x07) geçersiz bir Işaretçi kullanmaya çalıştı.</span><span class="sxs-lookup"><span data-stu-id="ee161-1280">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ee161-1281">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ee161-1281">Allowed From</span></span>

<span data-ttu-id="ee161-1282">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ee161-1282">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ee161-1283">Örnek</span><span class="sxs-lookup"><span data-stu-id="ee161-1283">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="ee161-1284">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ee161-1284">See Also</span></span>

- <span data-ttu-id="ee161-1285">nx_tcp_socket_receive</span><span class="sxs-lookup"><span data-stu-id="ee161-1285">nx_tcp_socket_receive</span></span>
- <span data-ttu-id="ee161-1286">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="ee161-1286">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="ee161-1287">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="ee161-1287">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="ee161-1288">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="ee161-1288">nx_secure_tls_session_send</span></span>
- <span data-ttu-id="ee161-1289">nx_secure_tls_session_delete</span><span class="sxs-lookup"><span data-stu-id="ee161-1289">nx_secure_tls_session_delete</span></span>
- <span data-ttu-id="ee161-1290">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="ee161-1290">nx_secure_tls_session_receive</span></span>
- <span data-ttu-id="ee161-1291">nx_secure_tls_packet_allocate</span><span class="sxs-lookup"><span data-stu-id="ee161-1291">nx_secure_tls_packet_allocate</span></span>
- <span data-ttu-id="ee161-1292">nx_secure_tls_session_end</span><span class="sxs-lookup"><span data-stu-id="ee161-1292">nx_secure_tls_session_end</span></span>
- <span data-ttu-id="ee161-1293">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="ee161-1293">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="ee161-1294">nx_tcp_socket_accept</span><span class="sxs-lookup"><span data-stu-id="ee161-1294">nx_tcp_socket_accept</span></span>
- <span data-ttu-id="ee161-1295">nx_tcp_socket_listen</span><span class="sxs-lookup"><span data-stu-id="ee161-1295">nx_tcp_socket_listen</span></span>
- <span data-ttu-id="ee161-1296">nx_tcp_socket_disconnect</span><span class="sxs-lookup"><span data-stu-id="ee161-1296">nx_tcp_socket_disconnect</span></span>
- <span data-ttu-id="ee161-1297">nx_tcp_socket_unaccept</span><span class="sxs-lookup"><span data-stu-id="ee161-1297">nx_tcp_socket_unaccept</span></span>
- <span data-ttu-id="ee161-1298">nx_tcp_socket_relisten</span><span class="sxs-lookup"><span data-stu-id="ee161-1298">nx_tcp_socket_relisten</span></span>
- <span data-ttu-id="ee161-1299">nx_tcp_socket_delete</span><span class="sxs-lookup"><span data-stu-id="ee161-1299">nx_tcp_socket_delete</span></span>
- <span data-ttu-id="ee161-1300">nx_packet_allocate</span><span class="sxs-lookup"><span data-stu-id="ee161-1300">nx_packet_allocate</span></span>
- <span data-ttu-id="ee161-1301">nx_packet_data_append</span><span class="sxs-lookup"><span data-stu-id="ee161-1301">nx_packet_data_append</span></span>
- <span data-ttu-id="ee161-1302">nx_packet_data_extract_offset</span><span class="sxs-lookup"><span data-stu-id="ee161-1302">nx_packet_data_extract_offset</span></span>

## <a name="nx_secure_tls_session_time_function_set"></a><span data-ttu-id="ee161-1303">nx_secure_tls_session_time_function_set</span><span class="sxs-lookup"><span data-stu-id="ee161-1303">nx_secure_tls_session_time_function_set</span></span>

<span data-ttu-id="ee161-1304">NetX güvenli TLS oturumuna zaman damgası işlevi atama</span><span class="sxs-lookup"><span data-stu-id="ee161-1304">Assign a timestamp function to a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="ee161-1305">Prototype</span><span class="sxs-lookup"><span data-stu-id="ee161-1305">Prototype</span></span>

```C
UINT  nx_secure_tls_time_function_set(
                              NX_SECURE_TLS_SESSION *session_ptr,
                              ULONG (*time_func_ptr)(void));
```

### <a name="description"></a><span data-ttu-id="ee161-1306">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-1306">Description</span></span>

<span data-ttu-id="ee161-1307">Bu işlev, farklı TLS el iletilerinde kullanılan ve sertifikaların doğrulanması için geçerli zamanı alması gerektiğinde TLS 'nin çağıracağı bir işlev işaretçisi ayarlar.</span><span class="sxs-lookup"><span data-stu-id="ee161-1307">This function sets up a function pointer that TLS will invoke when it needs to get the current time, which is used in various TLS handshake messages and for verification of certificates.</span></span>

<span data-ttu-id="ee161-1308">Bu işlevin, TLS RFC 5246 ' de ClientHello gereksinimlere göre geçerli GMT 'yi UNIX 32 bit biçiminde (gece yarısından itibaren 1, 1970, UTC, daha fazla saniyeler yok saydıktan sonra saniye) döndürmesi beklenir.</span><span class="sxs-lookup"><span data-stu-id="ee161-1308">The function is expected to return the current GMT in UNIX 32-bit format (seconds since the midnight starting Jan 1, 1970, UTC, ignoring leap seconds), as per the ClientHello requirements in the TLS RFC 5246.</span></span>

<span data-ttu-id="ee161-1309">Zaman damgası işlevi atanmamışsa, TLS el sıkışmasındaki zaman damgası için 0 değeri kullanılır ve sertifika süre sonu denetimi çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="ee161-1309">If no timestamp function is assigned, a value of 0 for the timestamp in the TLS handshake will be used and certificate expiration checking will not work.</span></span>

### <a name="parameters"></a><span data-ttu-id="ee161-1310">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ee161-1310">Parameters</span></span>

- <span data-ttu-id="ee161-1311">**session_ptr** Bir TLS oturum örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-1311">**session_ptr** Pointer to a TLS Session instance.</span></span>
- <span data-ttu-id="ee161-1312">**time_func_ptr** UNIX 32 bit biçiminde geçerli saati (GMT) döndüren bir işlev işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-1312">**time_func_ptr** Pointer to a function that returns the current time (GMT) in UNIX 32-bit format.</span></span>

### <a name="return-values"></a><span data-ttu-id="ee161-1313">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ee161-1313">Return Values</span></span>

- <span data-ttu-id="ee161-1314">TLS oturumunun başarıyla başlatılmasından **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="ee161-1314">**NX_SUCCESS** (0x00) Successful initialization of the TLS session.</span></span>
- <span data-ttu-id="ee161-1315">**NX_INVALID_PARAMETERS** (0x4D) geçersiz TLS oturum işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-1315">**NX_INVALID_PARAMETERS** (0x4D) Invalid TLS session pointer.</span></span>
- <span data-ttu-id="ee161-1316">**NX_PTR_ERROR** (0x07) geçersiz bir Işaretçi kullanmaya çalıştı.</span><span class="sxs-lookup"><span data-stu-id="ee161-1316">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ee161-1317">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ee161-1317">Allowed From</span></span>

<span data-ttu-id="ee161-1318">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ee161-1318">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ee161-1319">Örnek</span><span class="sxs-lookup"><span data-stu-id="ee161-1319">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="ee161-1320">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ee161-1320">See Also</span></span>

- <span data-ttu-id="ee161-1321">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="ee161-1321">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="ee161-1322">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="ee161-1322">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="ee161-1323">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="ee161-1323">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="ee161-1324">nx_secure_tls_session_delete</span><span class="sxs-lookup"><span data-stu-id="ee161-1324">nx_secure_tls_session_delete</span></span>
- <span data-ttu-id="ee161-1325">nx_secure_tls_session_sendnx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="ee161-1325">nx_secure_tls_session_sendnx_secure_tls_session_receive</span></span>
- <span data-ttu-id="ee161-1326">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="ee161-1326">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_trusted_certificate_add"></a><span data-ttu-id="ee161-1327">nx_secure_tls_trusted_certificate_add</span><span class="sxs-lookup"><span data-stu-id="ee161-1327">nx_secure_tls_trusted_certificate_add</span></span>

<span data-ttu-id="ee161-1328">NetX güvenli TLS oturumuna güvenilen sertifika ekleme</span><span class="sxs-lookup"><span data-stu-id="ee161-1328">Add trusted certificate to NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="ee161-1329">Prototype</span><span class="sxs-lookup"><span data-stu-id="ee161-1329">Prototype</span></span>

```C
UINT  nx_secure_tls_trusted_certificate_add(NX_SECURE_TLS_SESSION
                            *session_ptr, NX_SECURE_X509_CERT *certificate_ptr);
```

### <a name="description"></a><span data-ttu-id="ee161-1330">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-1330">Description</span></span>

<span data-ttu-id="ee161-1331">Bu hizmet, bir TLS oturumuna başlatılmış bir NX_SECURE_X509_CERT yapısı örneği ekler.</span><span class="sxs-lookup"><span data-stu-id="ee161-1331">This service adds an initialized NX_SECURE_X509_CERT structure instance to a TLS session.</span></span> <span data-ttu-id="ee161-1332">Bu sertifika, TLS el sıkışması sırasında uzak ana bilgisayar tarafından sağlanan sertifikaları doğrulamak için TLS yığını tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ee161-1332">This certificate is used by the TLS stack to verify certificates supplied by the remote host during the TLS handshake.</span></span>

<span data-ttu-id="ee161-1333">TLS Istemci modu için güvenilen sertifikalar gereklidir.</span><span class="sxs-lookup"><span data-stu-id="ee161-1333">Trusted certificates are required for TLS Client mode.</span></span>

<span data-ttu-id="ee161-1334">Güvenilen sertifikalar yalnızca istemci sertifikası kimlik doğrulaması etkinse TLS sunucu modu için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="ee161-1334">Trusted certificates are only required for TLS Server mode if client certificate authentication is enabled.</span></span>

### <a name="parameters"></a><span data-ttu-id="ee161-1335">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ee161-1335">Parameters</span></span>

- <span data-ttu-id="ee161-1336">**session_ptr** Daha önce oluşturulmuş bir TLS oturum örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ee161-1336">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="ee161-1337">**certificate_ptr** Başlatılmış bir TLS sertifikası örneğinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-1337">**certificate_ptr** Pointer to an initialized TLS Certificate instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="ee161-1338">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ee161-1338">Return Values</span></span>

- <span data-ttu-id="ee161-1339">Sertifikanın başarılı bir şekilde eklenmesi **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="ee161-1339">**NX_SUCCESS** (0x00) Successful addition of certificate.</span></span>
- <span data-ttu-id="ee161-1340">**NX_INVALID_PARAMETERS** (0x4D) geçersiz bir sertifika eklemeye çalıştı.</span><span class="sxs-lookup"><span data-stu-id="ee161-1340">**NX_INVALID_PARAMETERS** (0x4D) Tried to add an invalid certificate.</span></span>
- <span data-ttu-id="ee161-1341">**NX_PTR_ERROR** (0x07) geçersiz TLS oturum işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-1341">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ee161-1342">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ee161-1342">Allowed From</span></span>

<span data-ttu-id="ee161-1343">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ee161-1343">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ee161-1344">Örnek</span><span class="sxs-lookup"><span data-stu-id="ee161-1344">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="ee161-1345">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ee161-1345">See Also</span></span>

- <span data-ttu-id="ee161-1346">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="ee161-1346">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="ee161-1347">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="ee161-1347">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="ee161-1348">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="ee161-1348">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="ee161-1349">nx_secure_tls_trusted_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="ee161-1349">nx_secure_tls_trusted_certificate_remove</span></span>

## <a name="nx_secure_tls_trusted_certificate_remove"></a><span data-ttu-id="ee161-1350">nx_secure_tls_trusted_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="ee161-1350">nx_secure_tls_trusted_certificate_remove</span></span>

<span data-ttu-id="ee161-1351">Güvenilen sertifikayı NetX güvenli TLS oturumundan kaldır</span><span class="sxs-lookup"><span data-stu-id="ee161-1351">Remove trusted certificate from NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="ee161-1352">Prototype</span><span class="sxs-lookup"><span data-stu-id="ee161-1352">Prototype</span></span>

```C
UINT  nx_secure_tls_trusted_certificate_remove(
                                    NX_SECURE_TLS_SESSION *session_ptr,
                                    UCHAR *common_name,
                                    UINT common_name_length);
```

### <a name="description"></a><span data-ttu-id="ee161-1353">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-1353">Description</span></span>

<span data-ttu-id="ee161-1354">Bu hizmet, güvenilen bir sertifikayı, sertifikadaki ortak ad alanına girilen bir TLS oturumundan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="ee161-1354">This service removes a trusted certificate from a TLS session, keyed on the Common Name field in the certificate.</span></span>

### <a name="parameters"></a><span data-ttu-id="ee161-1355">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ee161-1355">Parameters</span></span>

- <span data-ttu-id="ee161-1356">**session_ptr** Daha önce oluşturulmuş bir TLS oturum örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ee161-1356">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="ee161-1357">**common_name** Kaldırılacak sertifikanın ortak ad değeri.</span><span class="sxs-lookup"><span data-stu-id="ee161-1357">**common_name** The Common Name value of the certificate to be removed.</span></span>
- <span data-ttu-id="ee161-1358">**common_name_length** Ortak ad dizesinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="ee161-1358">**common_name_length** The length of the Common Name string.</span></span>

### <a name="return-values"></a><span data-ttu-id="ee161-1359">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ee161-1359">Return Values</span></span>

- <span data-ttu-id="ee161-1360">Sertifikanın başarılı bir şekilde eklenmesi **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="ee161-1360">**NX_SUCCESS** (0x00) Successful addition of certificate.</span></span>
- <span data-ttu-id="ee161-1361">**NX_PTR_ERROR** (0x07) geçersiz TLS oturum işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-1361">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>
- <span data-ttu-id="ee161-1362">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) sertifikası bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="ee161-1362">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) Certificate was not found.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ee161-1363">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ee161-1363">Allowed From</span></span>

<span data-ttu-id="ee161-1364">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ee161-1364">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ee161-1365">Örnek</span><span class="sxs-lookup"><span data-stu-id="ee161-1365">Example</span></span>

```C
/* Remove certificate from TLS session.  */
status =  nx_secure_tls_trusted_certificate_remove(&tls_session,
                                                “www.example.com”, 15);


/* If status is NX_SUCCESS the certificate was successfully removed.  */
```

### <a name="see-also"></a><span data-ttu-id="ee161-1366">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ee161-1366">See Also</span></span>

- <span data-ttu-id="ee161-1367">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="ee161-1367">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="ee161-1368">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="ee161-1368">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="ee161-1369">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="ee161-1369">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="ee161-1370">nx_secure_tls_trusted_certificate_add</span><span class="sxs-lookup"><span data-stu-id="ee161-1370">nx_secure_tls_trusted_certificate_add</span></span>

## <a name="nx_secure_x509_certificate_initialize"></a><span data-ttu-id="ee161-1371">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="ee161-1371">nx_secure_x509_certificate_initialize</span></span>

<span data-ttu-id="ee161-1372">NetX güvenli TLS için X. 509.440 sertifikasını başlatın</span><span class="sxs-lookup"><span data-stu-id="ee161-1372">Initialize X.509 Certificate for NetX Secure TLS</span></span>

### <a name="prototype"></a><span data-ttu-id="ee161-1373">Prototype</span><span class="sxs-lookup"><span data-stu-id="ee161-1373">Prototype</span></span>

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

### <a name="description"></a><span data-ttu-id="ee161-1374">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-1374">Description</span></span>

<span data-ttu-id="ee161-1375">Bu hizmet, bir TLS oturumunda kullanılmak üzere ikili kodlanmış X. 509.952 dijital sertifikasından bir NX_SECURE_X509_CERT yapısını başlatır.</span><span class="sxs-lookup"><span data-stu-id="ee161-1375">This service initializes an NX_SECURE_X509_CERT structure from a binary-encoded X.509 digital certificate for use in a TLS session.</span></span>

<span data-ttu-id="ee161-1376">Sertifika verileri, DER kodlu ikili biçimde geçerli bir X. 509.952 dijital sertifikası **olmalıdır** .</span><span class="sxs-lookup"><span data-stu-id="ee161-1376">The certificate data **must** be a valid X.509 digital certificate in DER-encoded binary format.</span></span> <span data-ttu-id="ee161-1377">Veriler, bu verilere yönelik bir uşar işaretçisi sağlandığı sürece herhangi bir kaynaktan (ör. dosya sistemi, derlenmiş sabit arabellek, vb.) oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="ee161-1377">The data can some from any source (e.g. file system, compiled constant buffer, etc.) as long as a UCHAR pointer to that data is provided.</span></span>

<span data-ttu-id="ee161-1378">*Raw_data_buffer* parametresi ve boyutu, sertifika verilerinin ayrıştırılmadan önce kopyalandığı ayrılmış bir arabelleği belirten isteğe bağlı parametrelerdir.</span><span class="sxs-lookup"><span data-stu-id="ee161-1378">The *raw_data_buffer* parameter and its size are optional parameters that specify a dedicated buffer into which the certificate data is copied before parsing.</span></span> <span data-ttu-id="ee161-1379">Raw_data_buffer NX_NULL olarak geçirilirse NX_SECURE_X509_CERT yapısı doğrudan certificate_data dizisine işaret eder (Bu durumda buffer_size yok sayılır).</span><span class="sxs-lookup"><span data-stu-id="ee161-1379">If raw_data_buffer is passed as NX_NULL then the NX_SECURE_X509_CERT structure will point directly into the certificate_data array (buffer_size is ignored in this case).</span></span> <span data-ttu-id="ee161-1380">Raw_data_buffer NX_NULL olarak geçirilirse certificate_data işaretçisi tarafından işaret edilen ***verileri değiştirmeyin veya*** sertifika işleme muhtemelen başarısız olur!</span><span class="sxs-lookup"><span data-stu-id="ee161-1380">If raw_data_buffer is passed as NX_NULL, ***do not*** modify the data pointed to by the certificate_data pointer or certificate processing will likely fail!</span></span>

<span data-ttu-id="ee161-1381">Özel anahtar parametresi yerel kimlik sertifikalarına yöneliktir. özel anahtar, sunucular tarafından bir istemciden gelen anahtar verilerinin şifresini çözmek (sunucunun ortak anahtarı kullanılarak şifrelenir) ve istemciler tarafından sunucu istemci sertifikası istediğinde bir sunucuya kimliklerini doğrulamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ee161-1381">The private key parameter is for local identity certificates – the private key is used by servers to decrypt the incoming key data from a client (encrypted using the server's public key) and by clients to verify their identity to a server when the server requests a client certificate.</span></span> <span data-ttu-id="ee161-1382">Bu API 'ye özel anahtar eklemek, ilişkili sertifikayı bir TLS uygulaması için kimlik sertifikası olarak otomatik olarak işaretler.</span><span class="sxs-lookup"><span data-stu-id="ee161-1382">Adding a private key with this API will automatically mark the associated certificate as being an identity certificate for a TLS application.</span></span> <span data-ttu-id="ee161-1383">Sertifikaları diğer amaçlar için başlatırken (örn. güvenilen mağaza), *private_key_data* parametresi null, 0 olarak *private_key_data_length* ve *private_key_type* NX_SECURE_X509_KEY_TYPE_NONE olarak geçirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="ee161-1383">When initializing certificates for other purposes (e.g. the trusted store), the *private_key_data* parameter should be passed as NULL, the *private_key_data_length* as 0, and the *private_key_type* should be passed as NX_SECURE_X509_KEY_TYPE_NONE.</span></span>

<span data-ttu-id="ee161-1384">*Private_key_type* parametresi, özel anahtarın biçimlendirmesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="ee161-1384">The *private_key_type* parameter indicates the formatting of the private key.</span></span> <span data-ttu-id="ee161-1385">Örneğin, özel anahtar DER ile kodlanmış bir PKCS # 1-Format RSA özel anahtarılüdür, private_key_type NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER olarak geçirilmelidir ve daha sonra kullanılmak üzere hemen ayrıştırılacak ve daha sonra kullanılmak üzere kaydedilecek NetX güvenli olarak bilinen bir tür.</span><span class="sxs-lookup"><span data-stu-id="ee161-1385">For example, if the private key is a DER-encoded PKCS#1-format RSA private key, the private_key_type should be passed as NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER, a type known to NetX Secure which will be parsed immediately and saved for later use.</span></span>

<span data-ttu-id="ee161-1386">Private_key_type, belirli anahtar biçimlerine veya diğer gereksinimlere sahip platformlar ve uygulamalar için<sup>23</sup> Kullanıcı tanımlı anahtar türlerini de destekler.</span><span class="sxs-lookup"><span data-stu-id="ee161-1386">The private_key_type also supports user-defined key types<sup>23</sup> for platforms and applications that have specific key formats or other needs.</span></span> <span data-ttu-id="ee161-1387">Örneğin, donanım tabanlı bir şifreleme altyapısı NetX güvenli yazılım tarafından anlaşılmayan belirli bir biçimi kullanabilir veya bir özel anahtar, bir Güvenilir Platform Modülü (TPM) veya PKCS # 11 şifreleme donanımında olduğu gibi bir şifreleme belirteci tarafından şifrelenmiş veya temsil edilebilir.</span><span class="sxs-lookup"><span data-stu-id="ee161-1387">For example, a hardware-based encryption engine may use a specific format not understood by the NetX Secure software, or a private key may be encrypted or represented by a cryptographic token as might be the case with a Trusted Platform Module (TPM) or PKCS#11 cryptographic hardware.</span></span> <span data-ttu-id="ee161-1388">Kullanıcı tanımlı anahtar türü kullanıldığında, anahtar veriler uygun şifreleme yordamına doğru iletilir. Örneğin, bir RSA özel anahtarı, herhangi bir ayrıştırma veya işleme olmadan, doğrudan ciphersuite tablosunda TLS için sunulan RSA şifreleme yordamına geçirilir.</span><span class="sxs-lookup"><span data-stu-id="ee161-1388">When a user-defined key type is used, the key data is passed verbatim to the appropriate cryptographic routine - for example, an RSA private key would be passed, without any parsing or processing, directly to the RSA cryptographic routine provided to TLS in the ciphersuite table.</span></span> <span data-ttu-id="ee161-1389">Kullanıcı tanımlı anahtar türü de şifreleme yordamına geçirilir (RSA durumunda, bu "op" parametresidir).</span><span class="sxs-lookup"><span data-stu-id="ee161-1389">The user-defined key type is also passed to the cryptographic routine (in the case of RSA, this is the "op" parameter).</span></span>

<span data-ttu-id="ee161-1390">Kullanıcı tanımlı anahtarların aralığı, 32 bitlik işaretsiz tamsayının en üst yarısını (0x0001 0000-0xFFFF FFFF) içerir.</span><span class="sxs-lookup"><span data-stu-id="ee161-1390">The range of user-defined keys covers the top half of a 32-bit unsigned integer, from 0x0001 0000-0xFFFF FFFF.</span></span> <span data-ttu-id="ee161-1391">0x0001 0000 'tan küçük değerler NetX güvenli kullanımı için ayrılmıştır.</span><span class="sxs-lookup"><span data-stu-id="ee161-1391">Values less than 0x0001 0000 are reserved for NetX Secure use.</span></span>

<span data-ttu-id="ee161-1392">Kullanıcı tanımlı anahtar türleri, ham özel anahtar verilerini işlemek için özel şifreleme yordamları gerektiren gelişmiş bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="ee161-1392">User-defined key types are an advanced feature that requires custom cryptographic routines to handle the raw private key data.</span></span> <span data-ttu-id="ee161-1393">Bu özelliğe ihtiyacınız varsa lütfen Express Logic temsilcisiyle iletişime geçin.</span><span class="sxs-lookup"><span data-stu-id="ee161-1393">Please contact your Express Logic representative if you have need of this feature.</span></span>

### <a name="parameters"></a><span data-ttu-id="ee161-1394">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ee161-1394">Parameters</span></span>

- <span data-ttu-id="ee161-1395">**certificate_ptr** Başlatılmamış X. 509.440 sertifika örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ee161-1395">**certificate_ptr** Pointer to an uninitialized X.509 Certificate instance.</span></span>
- <span data-ttu-id="ee161-1396">**certificate_data** DER ile kodlanmış X. 509.440 ikili verileri işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-1396">**certificate_data** Pointer to DER-encoded X.509 binary data.</span></span>
- <span data-ttu-id="ee161-1397">**raw_data_buffer** İsteğe bağlı adanmış sertifika veri arabelleği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-1397">**raw_data_buffer** Pointer to optional dedicated certificate data buffer.</span></span>
- <span data-ttu-id="ee161-1398">**Buffer_size** İsteğe bağlı ayrılmış sertifika veri arabelleğinin boyutu.</span><span class="sxs-lookup"><span data-stu-id="ee161-1398">**buffer_size** Size of optional dedicated certificate data buffer.</span></span>
- <span data-ttu-id="ee161-1399">**certificate_data_length** Bayt cinsinden sertifika ikili verilerinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="ee161-1399">**certificate_data_length** Length of certificate binary data in bytes.</span></span>
- <span data-ttu-id="ee161-1400">**private_key_data** İsteğe bağlı özel anahtar verilerine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ee161-1400">**private_key_data** Pointer to optional private key data.</span></span>
- <span data-ttu-id="ee161-1401">**private_key_data_length** Özel anahtar verileri uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="ee161-1401">**private_key_data_length** Length of private key data.</span></span>
- <span data-ttu-id="ee161-1402">**private_key_type** Anahtar türü tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="ee161-1402">**private_key_type** Key type identifier.</span></span>

### <a name="return-values"></a><span data-ttu-id="ee161-1403">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ee161-1403">Return Values</span></span>

- <span data-ttu-id="ee161-1404">Sertifikanın başarılı bir şekilde eklenmesi **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="ee161-1404">**NX_SUCCESS** (0x00) Successful addition of certificate.</span></span>
- <span data-ttu-id="ee161-1405">**NX_PTR_ERROR** (0x07) geçersiz bir Işaretçi kullanmaya çalıştı.</span><span class="sxs-lookup"><span data-stu-id="ee161-1405">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>
- <span data-ttu-id="ee161-1406">**NX_SECURE_TLS_INVALID_CERTIFICATE** (0x112) SERTIFIKA verileri der-Encoded X. 509.952 sertifikası içermiyordu.</span><span class="sxs-lookup"><span data-stu-id="ee161-1406">**NX_SECURE_TLS_INVALID_CERTIFICATE** (0x112) Certificate data did not contain a DER-encoded X.509 certificate.</span></span>
- <span data-ttu-id="ee161-1407">**NX_SECURE_TLS_UNSUPPORTED_PUBLIC_CIPHER** (0x10d) sertifikada NETX güvenli tarafından desteklenen bir ortak anahtar şifresi yoktu.</span><span class="sxs-lookup"><span data-stu-id="ee161-1407">**NX_SECURE_TLS_UNSUPPORTED_PUBLIC_CIPHER** (0x10D) Certificate did not have a public-key cipher that is supported by NetX Secure.</span></span>
- <span data-ttu-id="ee161-1408">**NX_SECURE_X509_INVALID_CERTIFICATE_SEQUENCE** (0x186) özel anahtar veya sertifika GEÇERLI bir ASN. 1 sırası içermiyordu.</span><span class="sxs-lookup"><span data-stu-id="ee161-1408">**NX_SECURE_X509_INVALID_CERTIFICATE_SEQUENCE** (0x186) Private key or certificate did not contain a valid ASN.1 sequence.</span></span>
- <span data-ttu-id="ee161-1409">**NX_SECURE_PKCS1_INVALID_PRIVATE_KEY** (0x18a) belirtilen özel anahtar GEÇERLI bir PKCS # 1 RSA anahtarı değildi.</span><span class="sxs-lookup"><span data-stu-id="ee161-1409">**NX_SECURE_PKCS1_INVALID_PRIVATE_KEY** (0x18A) The provided private key was not a valid PKCS#1 RSA key.</span></span>
- <span data-ttu-id="ee161-1410">**NX_SECURE_X509_INVALID_PRIVATE_KEY_TYPE** (0x19d) belirtilen özel anahtar türü kullanıcı tanımlı değildi ve bilinen hiçbir türle eşleşmedi.</span><span class="sxs-lookup"><span data-stu-id="ee161-1410">**NX_SECURE_X509_INVALID_PRIVATE_KEY_TYPE** (0x19D) The private key type provided was not user-defined and did not match any known type.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ee161-1411">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ee161-1411">Allowed From</span></span>

<span data-ttu-id="ee161-1412">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ee161-1412">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ee161-1413">Örnek</span><span class="sxs-lookup"><span data-stu-id="ee161-1413">Example</span></span>

```C
/* Initialize certificate structure. The certificate structure will point directly
   into the certificate_data array since we are passing the raw_data_buffer as
   NX_NULL. This certificate has a private key so it will be used to identify this
   device. */
status =  nx_secure_x509_certificate_initialize(&certificate, certificate_data,
500, NX_NULL, 0, private_key, 64, NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);


/* If status is NX_SUCCESS the certificate was successfully initialized.  */
```

### <a name="see-also"></a><span data-ttu-id="ee161-1414">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ee161-1414">See Also</span></span>

- <span data-ttu-id="ee161-1415">nx_secure_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="ee161-1415">nx_secure_local_certificate_add</span></span>
- <span data-ttu-id="ee161-1416">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="ee161-1416">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="ee161-1417">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="ee161-1417">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="ee161-1418">Bölüm 3 ' te X. 509.440 sertifikalarını NetX güvenli olarak içeri aktarma.</span><span class="sxs-lookup"><span data-stu-id="ee161-1418">Importing X.509 Certificates into NetX Secure in Chapter 3.</span></span>

## <a name="nx_secure_x509_common_name_dns_check"></a><span data-ttu-id="ee161-1419">nx_secure_x509_common_name_dns_check</span><span class="sxs-lookup"><span data-stu-id="ee161-1419">nx_secure_x509_common_name_dns_check</span></span>

<span data-ttu-id="ee161-1420">X. 509.440 sertifikasıyla DNS adını denetle</span><span class="sxs-lookup"><span data-stu-id="ee161-1420">Check DNS name against X.509 Certificate</span></span>

### <a name="prototype"></a><span data-ttu-id="ee161-1421">Prototype</span><span class="sxs-lookup"><span data-stu-id="ee161-1421">Prototype</span></span>

```C
UINT  nx_secure_x509_common_name_dns_check(
                        NX_SECURE_X509_CERT *certificate,
                        const UCHAR *dns_tld, UINT dns_tld_length);
```

### <a name="description"></a><span data-ttu-id="ee161-1422">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-1422">Description</span></span>

<span data-ttu-id="ee161-1423">Bu hizmet, uzak bir ana bilgisayarın DNS doğrulaması amacıyla arayan tarafından belirtilen bir üst etki alanı adına (TLD) karşı bir sertifikanın ortak adını denetler.</span><span class="sxs-lookup"><span data-stu-id="ee161-1423">This service checks a certificate's Common Name against a Top- Domain name (TLD) provided by the caller for the purposes of DNS validation of a remote host.</span></span> <span data-ttu-id="ee161-1424">Bu yardımcı program işlevi, uygulama tarafından verilen bir sertifika doğrulama geri çağırma yordamının içinden çağrılması amaçlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="ee161-1424">This utility function is intended to be called from within a certificate validation callback routine provided by the application.</span></span> <span data-ttu-id="ee161-1425">TLD adı, uzak ana bilgisayara erişmek için kullanılan URL 'nin en üst bölümü olmalıdır ("." ilk eğik çizgiden önce ayrılmış dize).</span><span class="sxs-lookup"><span data-stu-id="ee161-1425">The TLD name should be the top part of the URL used to access the remote host (the "."-separated string before the first slash).</span></span> <span data-ttu-id="ee161-1426">Ortak ad bir joker karakter (örn *. example.com) içeriyorsa, joker karakter aynı soneke sahip herhangi biriyle eşleşir. Joker karakter eşleştirmesi için yalnızca ilk joker ("*") ile karşılaşılan (sağdan sola okuma) değerlendirildiğini unutmayın; Örneğin, ABC. \*. example. com, ". example.com" ile biten *Tüm* ad ile eşleşir.</span><span class="sxs-lookup"><span data-stu-id="ee161-1426">If the Common Name contains a wildcard (such as *.example.com), the wildcard will match any with the same suffix. Note that only the first wildcard ("*") encountered (reading right-to-left) will be considered for wildcard matching – for example, abc.\*.example.com will match *any* name ending in ".example.com".</span></span>

<span data-ttu-id="ee161-1427">Ortak ad, belirtilen dizeyle eşleşmezse, "subjectAltName" uzantısı ayrıştırılır (sertifikada varsa) ve herhangi bir DNSName girdisi de karşılaştırılır.</span><span class="sxs-lookup"><span data-stu-id="ee161-1427">If the Common Name does not match the provided string, the "subjectAltName" extension is parsed (if it exists in the certificate) and any DNSName entries are also compared.</span></span> <span data-ttu-id="ee161-1428">Bu girdilerden hiçbiri eşleşmezse bir hata döndürülür.</span><span class="sxs-lookup"><span data-stu-id="ee161-1428">If none of those entries match, an error is returned.</span></span>

<span data-ttu-id="ee161-1429">Beklenen sertifikalarda ortak ad (ve subjectAltName girişlerinin) biçiminin anlaşılması önemlidir.</span><span class="sxs-lookup"><span data-stu-id="ee161-1429">It is important to understand the format of the common name (and subjectAltName entries) in expected certificates.</span></span> <span data-ttu-id="ee161-1430">Örneğin, bazı sertifikalar bir ham IP adresi veya bir joker karakter kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="ee161-1430">For example, some certificates may use a raw IP address or a wild card.</span></span> <span data-ttu-id="ee161-1431">DNS TLD dizesinin, alınan sertifikalarda beklenen değerlerle eşleşecek şekilde biçimlendirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="ee161-1431">The DNS TLD string must be formatted such that it will match the expected values in received certificates.</span></span>

### <a name="parameters"></a><span data-ttu-id="ee161-1432">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ee161-1432">Parameters</span></span>

- <span data-ttu-id="ee161-1433">**certificate_ptr** X. 509.440 sertifika örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-1433">**certificate_ptr** Pointer to an X.509 Certificate instance.</span></span>
- <span data-ttu-id="ee161-1434">Karşılaştırılacak etki alanı adı Top-Level **dns_tld** .</span><span class="sxs-lookup"><span data-stu-id="ee161-1434">**dns_tld** Top-Level Domain name to compare against.</span></span>
- <span data-ttu-id="ee161-1435">**dns_tld_length** TLD dizesinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="ee161-1435">**dns_tld_length** Length of TLD string.</span></span>

### <a name="return-values"></a><span data-ttu-id="ee161-1436">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ee161-1436">Return Values</span></span>

- <span data-ttu-id="ee161-1437">Ortak ad veya subjectAltName ile başarılı bir karşılaştırma **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="ee161-1437">**NX_SUCCESS** (0x00) Successful comparison with Common Name or subjectAltName.</span></span>
- <span data-ttu-id="ee161-1438">**NX_SECURE_X509_CERTIFICATE_DNS_MISMATCH** (0x195) eşleşen ad bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="ee161-1438">**NX_SECURE_X509_CERTIFICATE_DNS_MISMATCH** (0x195) No matching name found.</span></span>
- <span data-ttu-id="ee161-1439">**NX_PTR_ERROR** (0x07) geçersiz bir Işaretçi kullanmaya çalıştı.</span><span class="sxs-lookup"><span data-stu-id="ee161-1439">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ee161-1440">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ee161-1440">Allowed From</span></span>

<span data-ttu-id="ee161-1441">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ee161-1441">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ee161-1442">Örnek</span><span class="sxs-lookup"><span data-stu-id="ee161-1442">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="ee161-1443">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ee161-1443">See Also</span></span>

- <span data-ttu-id="ee161-1444">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="ee161-1444">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="ee161-1445">nx_secure_tls_session_certificate_callback_set</span><span class="sxs-lookup"><span data-stu-id="ee161-1445">nx_secure_tls_session_certificate_callback_set</span></span>
- <span data-ttu-id="ee161-1446">nx_secure_x509_crl_revocation_check</span><span class="sxs-lookup"><span data-stu-id="ee161-1446">nx_secure_x509_crl_revocation_check</span></span>

## <a name="nx_secure_x509_crl_revocation_check"></a><span data-ttu-id="ee161-1447">nx_secure_x509_crl_revocation_check</span><span class="sxs-lookup"><span data-stu-id="ee161-1447">nx_secure_x509_crl_revocation_check</span></span>

<span data-ttu-id="ee161-1448">Sağlanan sertifika Iptal listesine (CRL) göre X. 509.440 sertifikasını denetle</span><span class="sxs-lookup"><span data-stu-id="ee161-1448">Check X.509 Certificate against a supplied Certificate Revocation List (CRL)</span></span>

### <a name="prototype"></a><span data-ttu-id="ee161-1449">Prototype</span><span class="sxs-lookup"><span data-stu-id="ee161-1449">Prototype</span></span>

```C
UINT  nx_secure_x509_crl_revocation_check(const UCHAR *crl_data,
                              UINT crl_length,
                              NX_SECURE_X509_CERTIFICATE_STORE *store,
                              NX_SECURE_X509_CERT *certificate);
```

### <a name="description"></a><span data-ttu-id="ee161-1450">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-1450">Description</span></span>

<span data-ttu-id="ee161-1451">Bu hizmet, DER kodlu bir sertifika Iptal listesi alır ve bu listedeki belirli bir sertifikayı arar.</span><span class="sxs-lookup"><span data-stu-id="ee161-1451">This service takes a DER-encoded Certificate Revocation List and searches for a specific certificate in that list.</span></span> <span data-ttu-id="ee161-1452">CRL veren, sağlanan sertifika deposuna göre doğrulandıktan sonra, CRL veren, denetlenen sertifikayla aynı olacak şekilde onaylanır ve iptal edilen sertifikalar listesinde aramak için söz konusu sertifikanın seri numarası kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ee161-1452">The issuer of the CRL is validated against a supplied certificate store, the CRL issuer is validated to be the same as the one for the certificate being checked, and the serial number of the certificate in question is used to search the revoked certificates list.</span></span> <span data-ttu-id="ee161-1453">Verenler eşleşiyorsa imza kontrol eder ve sertifika **listede yoksa,** çağrı başarılı olur.</span><span class="sxs-lookup"><span data-stu-id="ee161-1453">If the issuers match, the signature checks out, and the certificate is **not** present in the list, the call is successful.</span></span> <span data-ttu-id="ee161-1454">Tüm diğer durumlar hata döndürülmesine neden olur.</span><span class="sxs-lookup"><span data-stu-id="ee161-1454">All other cases cause an error to be returned.</span></span>

### <a name="parameters"></a><span data-ttu-id="ee161-1455">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ee161-1455">Parameters</span></span>

- <span data-ttu-id="ee161-1456">**crl_data** DER kodlu CRL işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-1456">**crl_data** Pointer to a DER-encoded CRL.</span></span>
- <span data-ttu-id="ee161-1457">**crl_length** CRL verilerinin bayt cinsinden uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="ee161-1457">**crl_length** Length in bytes of CRL data.</span></span>
- <span data-ttu-id="ee161-1458">**Mağaza** X. 509.440 sertifika deposuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ee161-1458">**store** Pointer to an X.509 Certificate store.</span></span>
- <span data-ttu-id="ee161-1459">**certificate_ptr** X. 509.440 sertifika örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-1459">**certificate_ptr** Pointer to an X.509 Certificate instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="ee161-1460">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ee161-1460">Return Values</span></span>

- <span data-ttu-id="ee161-1461">**NX_SUCCESS** (0x00) sertifikanın iptal edilmediğini doğrulama başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="ee161-1461">**NX_SUCCESS** (0x00) Successful validation that the certificate was not revoked.</span></span>
- <span data-ttu-id="ee161-1462">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) CRL veren sertifikası bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="ee161-1462">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) CRL issuer certificate not found.</span></span>
- <span data-ttu-id="ee161-1463">**NX_SECURE_TLS_ISSUER_CERTIFICATE_NOT_FOUND** 0x11b) sertifika veren sertifikası bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="ee161-1463">**NX_SECURE_TLS_ISSUER_CERTIFICATE_NOT_FOUND** 0x11B) Certificate issuer certificate not found.</span></span>
- <span data-ttu-id="ee161-1464">**NX_SECURE_X509_ASN1_LENGTH_TOO_LONG** (0x182) CRL ASN. 1, geçersiz bir uzunluk alanı içeriyordu.</span><span class="sxs-lookup"><span data-stu-id="ee161-1464">**NX_SECURE_X509_ASN1_LENGTH_TOO_LONG** (0x182) The CRL ASN.1 contained an invalid length field.</span></span>
- <span data-ttu-id="ee161-1465">**NX_SECURE_X509_UNEXPECTED_ASN1_TAG (0x189)** CRL geçersiz ASN. 1 içeriyordu.</span><span class="sxs-lookup"><span data-stu-id="ee161-1465">**NX_SECURE_X509_UNEXPECTED_ASN1_TAG(0x189)** The CRL contained invalid ASN.1.</span></span>
- <span data-ttu-id="ee161-1466">**NX_SECURE_X509_CHAIN_VERIFY_FAILURE** (0x18C) bir sertifika zinciri doğrulaması başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="ee161-1466">**NX_SECURE_X509_CHAIN_VERIFY_FAILURE** (0x18C) A certificate chain verification failed.</span></span>
- <span data-ttu-id="ee161-1467">**NX_SECURE_X509_CRL_ISSUER_MISMATCH** (0x197) CRL ve sertifika verenler eşleşmedi.</span><span class="sxs-lookup"><span data-stu-id="ee161-1467">**NX_SECURE_X509_CRL_ISSUER_MISMATCH** (0x197) CRL and certificate issuers did not match.</span></span>
- <span data-ttu-id="ee161-1468">**NX_SECURE_X509_CRL_SIGNATURE_CHECK_FAILED** 0x198) CRL imzası geçersizdi.</span><span class="sxs-lookup"><span data-stu-id="ee161-1468">**NX_SECURE_X509_CRL_SIGNATURE_CHECK_FAILED** 0x198) The CRL signature was invalid.</span></span>
- <span data-ttu-id="ee161-1469">**NX_SECURE_X509_CRL_CERTIFICATE_REVOKED** (0x199) denetlenen sertifika CRL 'de bulundu ve bu nedenle iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="ee161-1469">**NX_SECURE_X509_CRL_CERTIFICATE_REVOKED** (0x199) The certificate being checked was found in the CRL and is therefore revoked.</span></span>
- <span data-ttu-id="ee161-1470">**NX_PTR_ERROR** (0x07) geçersiz bir Işaretçi kullanmaya çalıştı.</span><span class="sxs-lookup"><span data-stu-id="ee161-1470">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ee161-1471">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ee161-1471">Allowed From</span></span>

<span data-ttu-id="ee161-1472">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ee161-1472">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ee161-1473">Örnek</span><span class="sxs-lookup"><span data-stu-id="ee161-1473">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="ee161-1474">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ee161-1474">See Also</span></span>

- <span data-ttu-id="ee161-1475">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="ee161-1475">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="ee161-1476">nx_secure_tls_session_certificate_callback_set</span><span class="sxs-lookup"><span data-stu-id="ee161-1476">nx_secure_tls_session_certificate_callback_set</span></span>
- <span data-ttu-id="ee161-1477">nx_secure_x509_common_name_dns_check</span><span class="sxs-lookup"><span data-stu-id="ee161-1477">nx_secure_x509_common_name_dns_check</span></span>

## <a name="nx_secure_x509_dns_name_initialize"></a><span data-ttu-id="ee161-1478">nx_secure_x509_dns_name_initialize</span><span class="sxs-lookup"><span data-stu-id="ee161-1478">nx_secure_x509_dns_name_initialize</span></span>

<span data-ttu-id="ee161-1479">X. 509.440 DNS adı yapısını başlatma</span><span class="sxs-lookup"><span data-stu-id="ee161-1479">Initialize an X.509 DNS name structure</span></span>

### <a name="prototype"></a><span data-ttu-id="ee161-1480">Prototype</span><span class="sxs-lookup"><span data-stu-id="ee161-1480">Prototype</span></span>

```C
UINT  nx_secure_x509_dns_name_initialize(
                        NX_SECURE_X509_DNS_NAME *dns_name,
                        const UCHAR *name_string, UINT length);
```

### <a name="description"></a><span data-ttu-id="ee161-1481">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-1481">Description</span></span>

<span data-ttu-id="ee161-1482">Bu hizmet belirli bir ad biçimi gerektiren belirli API hizmetleriyle kullanılmak üzere bir X. 509.440 DNS adı başlatır.</span><span class="sxs-lookup"><span data-stu-id="ee161-1482">This service initializes an X.509 DNS name for use with certain API services requiring a specific name format.</span></span> <span data-ttu-id="ee161-1483">Örneğin, *nx_secure_tls_sni_extension_parse* HIZMETI, TLS anlaşması sırasında sunucu adı belirtme uzantısında uzak bir ana bilgisayar tarafından girilen adı eşleştirmek için bir NX_SECURE_X509_DNS_NAME nesnesi bekler.</span><span class="sxs-lookup"><span data-stu-id="ee161-1483">For example, the *nx_secure_tls_sni_extension_parse* service expects an NX_SECURE_X509_DNS_NAME object in order to match the name provided by a remote host in the Server Name Indication extension during the TLS handshake.</span></span> <span data-ttu-id="ee161-1484">DNS adı yalnızca uzunluğu olan bir charater dizesidir; bir DNS adı için izin verilen uzunluk üst sınırı (ve NX_SECURE_X509_DNS_NAME içindeki iç arabelleğin boyutu), makro NX_SECURE_X509_DNS_NAME_MAX (varsayılan 100 bayt) tarafından denetlenir.</span><span class="sxs-lookup"><span data-stu-id="ee161-1484">A DNS name is simply a charater string with a length – the maximum allowed length of a DNS name (and the size of the internal buffer in NX_SECURE_X509_DNS_NAME) is controlled by the macro NX_SECURE_X509_DNS_NAME_MAX (default 100 bytes).</span></span>

### <a name="parameters"></a><span data-ttu-id="ee161-1485">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ee161-1485">Parameters</span></span>

- <span data-ttu-id="ee161-1486">**dns_name** Başlatılacak DNS ad yapısı.</span><span class="sxs-lookup"><span data-stu-id="ee161-1486">**dns_name** DNS name structure to initialize.</span></span>
- <span data-ttu-id="ee161-1487">**name_string** DNS adı dize verileri.</span><span class="sxs-lookup"><span data-stu-id="ee161-1487">**name_string** DNS name string data.</span></span>
- <span data-ttu-id="ee161-1488">**uzunluk** Ad dizesinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="ee161-1488">**length** Length of name string.</span></span>

### <a name="return-values"></a><span data-ttu-id="ee161-1489">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ee161-1489">Return Values</span></span>

- <span data-ttu-id="ee161-1490">**NX_SUCCESS** (0x00) başarıyla başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="ee161-1490">**NX_SUCCESS** (0x00) Successful initialization.</span></span>
- <span data-ttu-id="ee161-1491">**NX_SECURE_X509_NAME_STRING_TOO_LONG** (0x19e) verilen ad dizesi NX_SECURE_X509_DNS_NAME_MAX aştı.</span><span class="sxs-lookup"><span data-stu-id="ee161-1491">**NX_SECURE_X509_NAME_STRING_TOO_LONG** (0x19E) The given name string exceeded NX_SECURE_X509_DNS_NAME_MAX.</span></span>
- <span data-ttu-id="ee161-1492">**NX_PTR_ERROR** (0x07) geçersiz bir Işaretçi kullanmaya çalıştı.</span><span class="sxs-lookup"><span data-stu-id="ee161-1492">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ee161-1493">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ee161-1493">Allowed From</span></span>

<span data-ttu-id="ee161-1494">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ee161-1494">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ee161-1495">Örnek</span><span class="sxs-lookup"><span data-stu-id="ee161-1495">Example</span></span>

```C
NX_SECURE_X509_DNS_NAME dns_name;

/* Initialize DNS name. */
status = nx_secure_x509_dns_name_initialize(&dns_name, “www.example.com”,
                                            strlen(“www.example.com”);

/* Use initialized DNS name to send the Server Name Indication extension to the
   remote TLS server. */
status = nx_secure_tls_session_sni_extension_set(&tls_session, &dns_name);
```

### <a name="see-also"></a><span data-ttu-id="ee161-1496">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ee161-1496">See Also</span></span>

- <span data-ttu-id="ee161-1497">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="ee161-1497">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="ee161-1498">nx_secure_tls_session_sni_extension_parse</span><span class="sxs-lookup"><span data-stu-id="ee161-1498">nx_secure_tls_session_sni_extension_parse</span></span>
- <span data-ttu-id="ee161-1499">nx_secure_tls_session_sni_extension_set</span><span class="sxs-lookup"><span data-stu-id="ee161-1499">nx_secure_tls_session_sni_extension_set</span></span>

## <a name="nx_secure_x509_extended_key_usage_extension_parse"></a><span data-ttu-id="ee161-1500">nx_secure_x509_extended_key_usage_extension_parse</span><span class="sxs-lookup"><span data-stu-id="ee161-1500">nx_secure_x509_extended_key_usage_extension_parse</span></span>

<span data-ttu-id="ee161-1501">X. 509.440 sertifikası içindeki X. 509.952 genişletilmiş anahtar kullanımı uzantısını bulma ve ayrıştırma</span><span class="sxs-lookup"><span data-stu-id="ee161-1501">Find and parse an X.509 extended key usage extension in an X.509 certificate</span></span>

### <a name="prototype"></a><span data-ttu-id="ee161-1502">Prototype</span><span class="sxs-lookup"><span data-stu-id="ee161-1502">Prototype</span></span>

```C
UINT  nx_secure_x509_extended_key_usage_extension_parse(
                        NX_SECURE_X509_CERT *certificate,
                        UINT key_usage);
```

### <a name="description"></a><span data-ttu-id="ee161-1503">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-1503">Description</span></span>

<span data-ttu-id="ee161-1504">Bu hizmetin bir sertifika doğrulama geri çağırması içinden çağrılması amaçlanmıştır (bkz. *nx_secure_tls_session_certificate_callback_set)*.</span><span class="sxs-lookup"><span data-stu-id="ee161-1504">This service is intended to be called from within a certificate verification callback (see *nx_secure_tls_session_certificate_callback_set)*.</span></span> <span data-ttu-id="ee161-1505">Bu, bir X. 509.440 sertifikası içinde belirli bir genişletilmiş anahtar kullanımı OID 'sini arar ve OID 'nin mevcut olup olmadığını döndürür.</span><span class="sxs-lookup"><span data-stu-id="ee161-1505">It will search for a specific extended key usage OID within an X.509 certificate and return whether the OID is present.</span></span> <span data-ttu-id="ee161-1506">Key_usage parametresi, değişken uzunluklu OID dizelerinin parametre olarak geçirilmesini önlemek için NetX güvenli X. 509.440 ve TLS tarafından dahili olarak kullanılan OID 'lerin bir tamsayı eşlemesidir.</span><span class="sxs-lookup"><span data-stu-id="ee161-1506">The key_usage parameter is an integer mapping of the OIDs which is used internally by NetX Secure X.509 and TLS to avoid passing the variable-length OID strings as parameters.</span></span>

<span data-ttu-id="ee161-1507">Genişletilmiş anahtar kullanımı uzantısı için ilgili OID 'ler aşağıdaki tabloda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ee161-1507">The relevant OIDs for the extended key usage extension are given in the table below.</span></span> <span data-ttu-id="ee161-1508">Alınan bir TLS Sunucu sertifikasında genişletilmiş anahtar kullanımını denetlemek isteyen tipik bir TLS Istemci uygulamasının, OID 'nin varlığını denetlemesi NX_SECURE_TLS_X509_TYPE_PKIX_KP_SERVER_AUTH – uzantı varsa ancak bu OID yoksa, sertifika identifiying için geçersiz kabul edilir ve sertifika doğrulama geri araması bir hata döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="ee161-1508">A typical TLS Client implementation wishing to check extended key usage in a received TLS server certificate would check for the existence of the OID NX_SECURE_TLS_X509_TYPE_PKIX_KP_SERVER_AUTH – if the extension is present but that OID is not, then the certificate would be considered invalid for identifiying the host as a TLS server and the certificate verification callback should return an error.</span></span> <span data-ttu-id="ee161-1509">Uzantının kendisi eksikse, TLS el sıkışması ile devam edilip edilmeyeceğini uygulamaya göre yapılır.</span><span class="sxs-lookup"><span data-stu-id="ee161-1509">If the extension itself is missing, then it is up to the application whether or not to proceed with the TLS handshake.</span></span>

<span data-ttu-id="ee161-1510">Sertifika doğrulama geri çağrısında hata dönüş kodu NX_SECURE_X509_KEY_USAGE_ERROR, uygulama kullanımı için ayrılmıştır.</span><span class="sxs-lookup"><span data-stu-id="ee161-1510">In the certificate verification callback, the error return code NX_SECURE_X509_KEY_USAGE_ERROR is reserved for application use.</span></span> <span data-ttu-id="ee161-1511">Anahtar kullanımını denetlerken bir hata oluşursa, hatanın nedenini göstermek için bu değer geri aramadan döndürülür.</span><span class="sxs-lookup"><span data-stu-id="ee161-1511">If there is an error in checking key usage, this value may be returned from the callback to indicate the reason for failure.</span></span>

| <span data-ttu-id="ee161-1512">NetX güvenli tanımlayıcısı</span><span class="sxs-lookup"><span data-stu-id="ee161-1512">NetX Secure Identifier</span></span>                                | <span data-ttu-id="ee161-1513">OID değeri</span><span class="sxs-lookup"><span data-stu-id="ee161-1513">OID Value</span></span>         | <span data-ttu-id="ee161-1514">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-1514">Description</span></span>                                      |
| --------------------------------------------------------- | --------------------- | ---------------------------------------------------- |
| <span data-ttu-id="ee161-1515">NX_SECURE_TLS_X509_TYPE_PKIX_KP_SERVER_AUTH</span><span class="sxs-lookup"><span data-stu-id="ee161-1515">NX_SECURE_TLS_X509_TYPE_PKIX_KP_SERVER_AUTH</span></span>   | <span data-ttu-id="ee161-1516">1.3.6.1.5.5.7.3.1</span><span class="sxs-lookup"><span data-stu-id="ee161-1516">1.3.6.1.5.5.7.3.1</span></span> | <span data-ttu-id="ee161-1517">Sertifika, bir TLS sunucusunu tanımlamak için kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="ee161-1517">Certificate can be used to identify a TLS server</span></span> |
| <span data-ttu-id="ee161-1518">NX_SECURE_TLS_X509_TYPE_PKIX_KP_CLIENT_AUTH</span><span class="sxs-lookup"><span data-stu-id="ee161-1518">NX_SECURE_TLS_X509_TYPE_PKIX_KP_CLIENT_AUTH</span></span>   | <span data-ttu-id="ee161-1519">1.3.6.1.5.5.7.3.2</span><span class="sxs-lookup"><span data-stu-id="ee161-1519">1.3.6.1.5.5.7.3.2</span></span> | <span data-ttu-id="ee161-1520">Sertifika, bir TLS istemcisini tanımlamak için kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="ee161-1520">Certificate can be used to identify a TLS client</span></span> |
| <span data-ttu-id="ee161-1521">NX_SECURE_TLS_X509_TYPE_PKIX_KP_CODE_SIGNING</span><span class="sxs-lookup"><span data-stu-id="ee161-1521">NX_SECURE_TLS_X509_TYPE_PKIX_KP_CODE_SIGNING</span></span>  | <span data-ttu-id="ee161-1522">1.3.6.1.5.5.7.3.3</span><span class="sxs-lookup"><span data-stu-id="ee161-1522">1.3.6.1.5.5.7.3.3</span></span> | <span data-ttu-id="ee161-1523">Sertifika, kodu imzalamak için kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="ee161-1523">Certificate can be used to sign code</span></span>             |
| <span data-ttu-id="ee161-1524">NX_SECURE_TLS_X509_TYPE_PKIX_KP_EMAIL_PROTECT</span><span class="sxs-lookup"><span data-stu-id="ee161-1524">NX_SECURE_TLS_X509_TYPE_PKIX_KP_EMAIL_PROTECT</span></span> | <span data-ttu-id="ee161-1525">1.3.6.1.5.5.7.3.4</span><span class="sxs-lookup"><span data-stu-id="ee161-1525">1.3.6.1.5.5.7.3.4</span></span> | <span data-ttu-id="ee161-1526">Sertifika, e-postaları imzalamak için kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="ee161-1526">Certificate can be used to sign emails</span></span>           |
| <span data-ttu-id="ee161-1527">NX_SECURE_TLS_X509_TYPE_PKIX_KP_TIME_STAMPING</span><span class="sxs-lookup"><span data-stu-id="ee161-1527">NX_SECURE_TLS_X509_TYPE_PKIX_KP_TIME_STAMPING</span></span> | <span data-ttu-id="ee161-1528">1.3.6.1.5.5.7.3.8</span><span class="sxs-lookup"><span data-stu-id="ee161-1528">1.3.6.1.5.5.7.3.8</span></span> | <span data-ttu-id="ee161-1529">Sertifika, zaman damgalarını imzalamak için kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="ee161-1529">Certificate can be used to sign timestamps</span></span>       |
| <span data-ttu-id="ee161-1530">NX_SECURE_TLS_X509_TYPE_PKIX_KP_OCSP_SIGNING</span><span class="sxs-lookup"><span data-stu-id="ee161-1530">NX_SECURE_TLS_X509_TYPE_PKIX_KP_OCSP_SIGNING</span></span>  | <span data-ttu-id="ee161-1531">1.3.6.1.5.5.7.3.9</span><span class="sxs-lookup"><span data-stu-id="ee161-1531">1.3.6.1.5.5.7.3.9</span></span> | <span data-ttu-id="ee161-1532">Sertifika, OCSP yanıtlarını imzalamak için kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="ee161-1532">Certificate can be used to sign OCSP responses</span></span>   |

<span data-ttu-id="ee161-1533">X. 509.440 genişletilmiş anahtar kullanımı uzantısı için OID ve eşlemeler</span><span class="sxs-lookup"><span data-stu-id="ee161-1533">OIDs and mappings for X.509 Extended Key Usage Extension</span></span>

### <a name="parameters"></a><span data-ttu-id="ee161-1534">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ee161-1534">Parameters</span></span>

- <span data-ttu-id="ee161-1535">**sertifika** Doğrulanan sertifikaya yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ee161-1535">**certificate** Pointer to certificate being verified.</span></span>
- <span data-ttu-id="ee161-1536">**key_usage** Yukarıdaki tablodan OID tamsayı eşleme.</span><span class="sxs-lookup"><span data-stu-id="ee161-1536">**key_usage** OID integer mapping from table above.</span></span>

### <a name="return-values"></a><span data-ttu-id="ee161-1537">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ee161-1537">Return Values</span></span>

- <span data-ttu-id="ee161-1538">**NX_SUCCESS** (0x00) belirtilen anahtar kullanımı OID 'i bulundu.</span><span class="sxs-lookup"><span data-stu-id="ee161-1538">**NX_SUCCESS** (0x00) Specified key usage OID found.</span></span>
- <span data-ttu-id="ee161-1539">**NX_SECURE_X509_MULTIBYTE_TAG_UNSUPPORTED** (0x181) ASN. 1 Multi-Byte etiketiyle karşılaşıldı (desteklenmeyen sertifika).</span><span class="sxs-lookup"><span data-stu-id="ee161-1539">**NX_SECURE_X509_MULTIBYTE_TAG_UNSUPPORTED** (0x181) ASN.1 multi-byte tag encountered (unsupported certificate).</span></span>
- <span data-ttu-id="ee161-1540">**NX_SECURE_X509_ASN1_LENGTH_TOO_LONG** (0x182) Invaild ASN. 1 alanla karşılaşıldı (geçersiz sertifika).</span><span class="sxs-lookup"><span data-stu-id="ee161-1540">**NX_SECURE_X509_ASN1_LENGTH_TOO_LONG** (0x182) Invaild ASN.1 field encountered (invalid certificate).</span></span>
- <span data-ttu-id="ee161-1541">**NX_SECURE_X509_INVALID_TAG_CLASS** (0x190) geçersiz ASN. 1 etiket sınıfıyla karşılaşıldı (geçersiz sertifika).</span><span class="sxs-lookup"><span data-stu-id="ee161-1541">**NX_SECURE_X509_INVALID_TAG_CLASS** (0x190) Invalid ASN.1 tag class encountered (invalid certificate).</span></span>
- <span data-ttu-id="ee161-1542">**NX_SECURE_X509_INVALID_EXTENSION_SEQUENCE** (0x192) geçersiz uzantıyla karşılaşıldı (geçersiz sertifika).</span><span class="sxs-lookup"><span data-stu-id="ee161-1542">**NX_SECURE_X509_INVALID_EXTENSION_SEQUENCE** (0x192) Invalid extension encountered (invalid certificate).</span></span>
- <span data-ttu-id="ee161-1543">**NX_SECURE_X509_EXTENSION_NOT_FOUND** (0x19b) uzatılmış anahtar kullanımı uzantısı, belirtilen sertifikada bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="ee161-1543">**NX_SECURE_X509_EXTENSION_NOT_FOUND** (0x19B) The Extended Key Usage extension was not found in the provided certificate.</span></span>
- <span data-ttu-id="ee161-1544">**NX_PTR_ERROR** (0x07) geçersiz sertifika işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-1544">**NX_PTR_ERROR** (0x07) Invalid certificate pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ee161-1545">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ee161-1545">Allowed From</span></span>

<span data-ttu-id="ee161-1546">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ee161-1546">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ee161-1547">Örnek</span><span class="sxs-lookup"><span data-stu-id="ee161-1547">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="ee161-1548">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ee161-1548">See Also</span></span>

- <span data-ttu-id="ee161-1549">nx_secure_tls_session_certificate_callback_set</span><span class="sxs-lookup"><span data-stu-id="ee161-1549">nx_secure_tls_session_certificate_callback_set</span></span>
- <span data-ttu-id="ee161-1550">nx_secure_x509_key_usage_extension_parse</span><span class="sxs-lookup"><span data-stu-id="ee161-1550">nx_secure_x509_key_usage_extension_parse</span></span>
- <span data-ttu-id="ee161-1551">nx_secure_x509_crl_revocation_check</span><span class="sxs-lookup"><span data-stu-id="ee161-1551">nx_secure_x509_crl_revocation_check</span></span>
- <span data-ttu-id="ee161-1552">nx_secure_x509_common_name_dns_check</span><span class="sxs-lookup"><span data-stu-id="ee161-1552">nx_secure_x509_common_name_dns_check</span></span>
- <span data-ttu-id="ee161-1553">nx_secure_x509_extension_find</span><span class="sxs-lookup"><span data-stu-id="ee161-1553">nx_secure_x509_extension_find</span></span>

## <a name="nx_secure_x509_extension_find"></a><span data-ttu-id="ee161-1554">nx_secure_x509_extension_find</span><span class="sxs-lookup"><span data-stu-id="ee161-1554">nx_secure_x509_extension_find</span></span>

<span data-ttu-id="ee161-1555">X. 509.440 sertifikasında bir X. 509.440 uzantısı bulun ve döndürün</span><span class="sxs-lookup"><span data-stu-id="ee161-1555">Find and return an X.509 extension in an X.509 certificate</span></span>

### <a name="prototype"></a><span data-ttu-id="ee161-1556">Prototype</span><span class="sxs-lookup"><span data-stu-id="ee161-1556">Prototype</span></span>

```C
UINT  nx_secure_x509_extension_find(
                        NX_SECURE_X509_CERT *certificate,
                        NX_SECURE_X509_EXTENSION *extension,
                        USHORT extension_id);
```

### <a name="description"></a><span data-ttu-id="ee161-1557">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-1557">Description</span></span>

<span data-ttu-id="ee161-1558">Bu hizmetin bir sertifika doğrulama geri çağırması içinden çağrılması amaçlanmıştır (bkz. *nx_secure_tls_session_certificate_callback_set)* ve gelişmiş bir X. 509.440 hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="ee161-1558">This service is intended to be called from within a certificate verification callback (see *nx_secure_tls_session_certificate_callback_set)* and is an advanced X.509 service.</span></span>

<span data-ttu-id="ee161-1559">İşlevi, bir OID 'ye dayalı bir X. 509.440 sertifikası içindeki belirli bir uzantıyı arar ve OID 'nin mevcut ham uzantı verilerine yönelik başvuruları içeren bir yapıyla birlikte, OID 'nin var olup olmadığını döndürür.</span><span class="sxs-lookup"><span data-stu-id="ee161-1559">The function will search for a specific extension within an X.509 certificate based on an OID and return whether the OID is present, along with a structure containing references to the relevant raw extension data.</span></span> <span data-ttu-id="ee161-1560">Extension_id parametresi, değişken uzunluklu OID dizelerinin parametre olarak geçirilmesini önlemek için NetX güvenli X. 509.440 ve TLS tarafından dahili olarak kullanılan OID 'lerin bir tamsayı eşlemesidir.</span><span class="sxs-lookup"><span data-stu-id="ee161-1560">The extension_id parameter is an integer mapping of the OIDs which is used internally by NetX Secure X.509 and TLS to avoid passing the variable-length OID strings as parameters.</span></span>

<span data-ttu-id="ee161-1561">Belirli Uzantılar için belirtilen yardımcı işlevler ( *nx_secure_x509_key_usage_extension_parse*) çağrısı, dahili olarak uzantı verilerini almak için nx_secure_x509_extension_find.</span><span class="sxs-lookup"><span data-stu-id="ee161-1561">The helper functions provided for specific extensions (such as *nx_secure_x509_key_usage_extension_parse*) call nx_secure_x509_extension_find internally to obtain the extension data.</span></span>

<span data-ttu-id="ee161-1562">Bilinen X. 509.440 uzantıları için ilgili OID 'ler aşağıdaki tabloda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ee161-1562">The relevant OIDs for known X.509 extensions are given in the table below.</span></span>

<span data-ttu-id="ee161-1563">NX_SECURE_X509_EXTENSION yapısı, X. 509.952 sertifikasına, *nx_secure_x509_key_usage_extension_parse* gibi yardımcı işlevlere, ham uzantının der kodlu ASN. 1 verilerini hızlıca çözmesini sağlayan işaretçiler içerir.</span><span class="sxs-lookup"><span data-stu-id="ee161-1563">The NX_SECURE_X509_EXTENSION structure contains pointers into the X.509 certificate that allow helper functions such as *nx_secure_x509_key_usage_extension_parse* to quickly decode the raw extension DER-encoded ASN.1 data.</span></span>

<span data-ttu-id="ee161-1564">Belirli uzantılar hakkında daha fazla bilgi için bkz. RFC 5280 (X. 509.440 belirtimi) veya varsa uygun yardımcı işlevleri başvurusu.</span><span class="sxs-lookup"><span data-stu-id="ee161-1564">For information on specific extensions, see RFC 5280 (X.509 specification) or the reference for the appropriate helper functions if available.</span></span>

<span data-ttu-id="ee161-1565">NetX Secure X. 509.440 sürümünün geçerli sürümü, X. 509.440 uzantıları için sınırlı desteğe sahip.</span><span class="sxs-lookup"><span data-stu-id="ee161-1565">The current version of NetX Secure X.509 has limited support for X.509 extensions.</span></span> <span data-ttu-id="ee161-1566">Daha sonra daha fazla yardımcı işlev eklenecektir.</span><span class="sxs-lookup"><span data-stu-id="ee161-1566">More helper functions will be added in the future.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ee161-1567">*Bu hizmet, X. 509.440 uzantılarına ve DER kodlu ASN. 1 ' i bilen kullanıcılara yönelik gelişmiş bir özelliktir. Bu kullanıcıların, NetX Secure X. 509.952 'in Şu anda yardımcı işlevler sağlamayan uzantılara erişmesini sağlamak için sağlanmıştır. Yardımcı işlevleri olmayan bu uzantılar için ham DER kodlu ASN. 1 ' i kendiniz ayrıştırmanıza gerek olacaktır.*</span><span class="sxs-lookup"><span data-stu-id="ee161-1567">*This service is an advanced feature for users familiar with X.509 extensions and DER-encoded ASN.1. It is provided to enable those users to access extensions for which NetX Secure X.509 does not currently provide helper functions. For those extensions without helper functions, you will have to parse the raw DER-encoded ASN.1 yourself.*</span></span>

| <span data-ttu-id="ee161-1568">NetX güvenli tanımlayıcısı</span><span class="sxs-lookup"><span data-stu-id="ee161-1568">NetX Secure Identifier</span></span>                              | <span data-ttu-id="ee161-1569">OID değeri</span><span class="sxs-lookup"><span data-stu-id="ee161-1569">OID Value</span></span> | <span data-ttu-id="ee161-1570">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-1570">Description</span></span>                                                                    | <span data-ttu-id="ee161-1571">Yardımcı işlevi?</span><span class="sxs-lookup"><span data-stu-id="ee161-1571">Helper function?</span></span> |
| ------------------------------------------------------- | ------------- | ---------------------------------------------------------------------------------- | -------------------- |
| <span data-ttu-id="ee161-1572">NX_SECURE_TLS_X509_TYPE_DIRECTORY_ATTRIBUTES</span><span class="sxs-lookup"><span data-stu-id="ee161-1572">NX_SECURE_TLS_X509_TYPE_DIRECTORY_ATTRIBUTES</span></span>  | <span data-ttu-id="ee161-1573">2.5.29.9</span><span class="sxs-lookup"><span data-stu-id="ee161-1573">2.5.29.9</span></span>  | <span data-ttu-id="ee161-1574">Dizin öznitelikleri – sertifika konusu hakkında temel bilgi öznitelikleri</span><span class="sxs-lookup"><span data-stu-id="ee161-1574">Directory Attributes – basic information attributes about certificate subject</span></span>  | <span data-ttu-id="ee161-1575">Hayır</span><span class="sxs-lookup"><span data-stu-id="ee161-1575">No</span></span>               |
| <span data-ttu-id="ee161-1576">NX_SECURE_TLS_X509_TYPE_SUBJECT_KEY_ID</span><span class="sxs-lookup"><span data-stu-id="ee161-1576">NX_SECURE_TLS_X509_TYPE_SUBJECT_KEY_ID</span></span>       | <span data-ttu-id="ee161-1577">2.5.29.14</span><span class="sxs-lookup"><span data-stu-id="ee161-1577">2.5.29.14</span></span> | <span data-ttu-id="ee161-1578">Belirli bir ortak anahtarı tanımlamak için kullanılır</span><span class="sxs-lookup"><span data-stu-id="ee161-1578">Used to identify a specific public key</span></span>                                         | <span data-ttu-id="ee161-1579">Hayır</span><span class="sxs-lookup"><span data-stu-id="ee161-1579">No</span></span>               |
| <span data-ttu-id="ee161-1580">NX_SECURE_TLS_X509_TYPE_KEY_USAGE</span><span class="sxs-lookup"><span data-stu-id="ee161-1580">NX_SECURE_TLS_X509_TYPE_KEY_USAGE</span></span>             | <span data-ttu-id="ee161-1581">2.5.29.15</span><span class="sxs-lookup"><span data-stu-id="ee161-1581">2.5.29.15</span></span> | <span data-ttu-id="ee161-1582">Sertifika ortak anahtarı için geçerli kullanımlar hakkında bilgi sağlar</span><span class="sxs-lookup"><span data-stu-id="ee161-1582">Provides information on valid uses for the certificate public key</span></span>              | <span data-ttu-id="ee161-1583">Yes</span><span class="sxs-lookup"><span data-stu-id="ee161-1583">Yes</span></span>              |
| <span data-ttu-id="ee161-1584">NX_SECURE_TLS_X509_TYPE_SUBJECT_ALT_NAME</span><span class="sxs-lookup"><span data-stu-id="ee161-1584">NX_SECURE_TLS_X509_TYPE_SUBJECT_ALT_NAME</span></span>     | <span data-ttu-id="ee161-1585">2.5.29.17</span><span class="sxs-lookup"><span data-stu-id="ee161-1585">2.5.29.17</span></span> | <span data-ttu-id="ee161-1586">Sertifikayı tanımlamak için alternatif DNS adları sağlar</span><span class="sxs-lookup"><span data-stu-id="ee161-1586">Provides alternative DNS names to identify the certificate</span></span>                     | <span data-ttu-id="ee161-1587">Evet<sup>24</sup></span><span class="sxs-lookup"><span data-stu-id="ee161-1587">Yes<sup>24</sup></span></span>        |
| <span data-ttu-id="ee161-1588">NX_SECURE_TLS_X509_TYPE_ISSUER_ALT_NAME</span><span class="sxs-lookup"><span data-stu-id="ee161-1588">NX_SECURE_TLS_X509_TYPE_ISSUER_ALT_NAME</span></span>      | <span data-ttu-id="ee161-1589">2.5.29.18</span><span class="sxs-lookup"><span data-stu-id="ee161-1589">2.5.29.18</span></span> | <span data-ttu-id="ee161-1590">Sertifikanın vereni tanımlamak için alternatif DNS adları sağlar</span><span class="sxs-lookup"><span data-stu-id="ee161-1590">Provides alternative DNS names to identify the certificate's issuer</span></span>            | <span data-ttu-id="ee161-1591">Hayır</span><span class="sxs-lookup"><span data-stu-id="ee161-1591">No</span></span>               |
| <span data-ttu-id="ee161-1592">NX_SECURE_TLS_X509_TYPE_BASIC_CONSTRAINTS</span><span class="sxs-lookup"><span data-stu-id="ee161-1592">NX_SECURE_TLS_X509_TYPE_BASIC_CONSTRAINTS</span></span>     | <span data-ttu-id="ee161-1593">2.5.29.19</span><span class="sxs-lookup"><span data-stu-id="ee161-1593">2.5.29.19</span></span> | <span data-ttu-id="ee161-1594">Temel sertifika kullanım kısıtlaması bilgilerini sağlar</span><span class="sxs-lookup"><span data-stu-id="ee161-1594">Provides basic certificate usage constraint information</span></span>                        | <span data-ttu-id="ee161-1595">Hayır</span><span class="sxs-lookup"><span data-stu-id="ee161-1595">No</span></span>               |
| <span data-ttu-id="ee161-1596">NX_SECURE_TLS_X509_TYPE_NAME_CONSTRAINTS</span><span class="sxs-lookup"><span data-stu-id="ee161-1596">NX_SECURE_TLS_X509_TYPE_NAME_CONSTRAINTS</span></span>      | <span data-ttu-id="ee161-1597">2.5.29.30</span><span class="sxs-lookup"><span data-stu-id="ee161-1597">2.5.29.30</span></span> | <span data-ttu-id="ee161-1598">Sertifika adlarını belirli etki alanlarına kısıtlamak için kullanılır</span><span class="sxs-lookup"><span data-stu-id="ee161-1598">Used to constrain certificate names to specific domains</span></span>                        | <span data-ttu-id="ee161-1599">Hayır</span><span class="sxs-lookup"><span data-stu-id="ee161-1599">No</span></span>               |
| <span data-ttu-id="ee161-1600">NX_SECURE_TLS_X509_TYPE_CRL_DISTRIBUTION</span><span class="sxs-lookup"><span data-stu-id="ee161-1600">NX_SECURE_TLS_X509_TYPE_CRL_DISTRIBUTION</span></span>      | <span data-ttu-id="ee161-1601">2.5.29.31</span><span class="sxs-lookup"><span data-stu-id="ee161-1601">2.5.29.31</span></span> | <span data-ttu-id="ee161-1602">CRL dağıtımı için URI 'Ler sağlar</span><span class="sxs-lookup"><span data-stu-id="ee161-1602">Provides URIs for CRL distribution</span></span>                                             | <span data-ttu-id="ee161-1603">Hayır</span><span class="sxs-lookup"><span data-stu-id="ee161-1603">No</span></span>               |
| <span data-ttu-id="ee161-1604">NX_SECURE_TLS_X509_TYPE_CERTIFICATE_POLICIES</span><span class="sxs-lookup"><span data-stu-id="ee161-1604">NX_SECURE_TLS_X509_TYPE_CERTIFICATE_POLICIES</span></span>  | <span data-ttu-id="ee161-1605">2.5.29.32</span><span class="sxs-lookup"><span data-stu-id="ee161-1605">2.5.29.32</span></span> | <span data-ttu-id="ee161-1606">Büyük PKI sistemleri için sertifika ilkeleri listesi</span><span class="sxs-lookup"><span data-stu-id="ee161-1606">List of certificate policies for large PKI systems</span></span>                             | <span data-ttu-id="ee161-1607">Hayır</span><span class="sxs-lookup"><span data-stu-id="ee161-1607">No</span></span>               |
| <span data-ttu-id="ee161-1608">NX_SECURE_TLS_X509_TYPE_CERT_POLICY_MAPPINGS</span><span class="sxs-lookup"><span data-stu-id="ee161-1608">NX_SECURE_TLS_X509_TYPE_CERT_POLICY_MAPPINGS</span></span> | <span data-ttu-id="ee161-1609">2.5.29.33</span><span class="sxs-lookup"><span data-stu-id="ee161-1609">2.5.29.33</span></span> | <span data-ttu-id="ee161-1610">CA sertifika ilkelerinin listesi</span><span class="sxs-lookup"><span data-stu-id="ee161-1610">List of CA certificate policies</span></span>                                                | <span data-ttu-id="ee161-1611">Hayır</span><span class="sxs-lookup"><span data-stu-id="ee161-1611">No</span></span>               |
| <span data-ttu-id="ee161-1612">NX_SECURE_TLS_X509_TYPE_AUTHORITY_KEY_ID</span><span class="sxs-lookup"><span data-stu-id="ee161-1612">NX_SECURE_TLS_X509_TYPE_AUTHORITY_KEY_ID</span></span>     | <span data-ttu-id="ee161-1613">2.5.29.35</span><span class="sxs-lookup"><span data-stu-id="ee161-1613">2.5.29.35</span></span> | <span data-ttu-id="ee161-1614">Bir sertifika imzasıyla ilişkili belirli bir ortak anahtarı tanımlamak için kullanılır</span><span class="sxs-lookup"><span data-stu-id="ee161-1614">Used to identify a specific public key associated with a certificate signature</span></span> | <span data-ttu-id="ee161-1615">Hayır</span><span class="sxs-lookup"><span data-stu-id="ee161-1615">No</span></span>               |
| <span data-ttu-id="ee161-1616">NX_SECURE_TLS_X509_TYPE_POLICY_CONSTRAINTS</span><span class="sxs-lookup"><span data-stu-id="ee161-1616">NX_SECURE_TLS_X509_TYPE_POLICY_CONSTRAINTS</span></span>    | <span data-ttu-id="ee161-1617">2.5.29.36</span><span class="sxs-lookup"><span data-stu-id="ee161-1617">2.5.29.36</span></span> | <span data-ttu-id="ee161-1618">CA ilkesi kısıtlamaları</span><span class="sxs-lookup"><span data-stu-id="ee161-1618">CA policy constraints</span></span>                                                          | <span data-ttu-id="ee161-1619">Hayır</span><span class="sxs-lookup"><span data-stu-id="ee161-1619">No</span></span>               |
| <span data-ttu-id="ee161-1620">NX_SECURE_TLS_X509_TYPE_EXTENDED_KEY_USAGE</span><span class="sxs-lookup"><span data-stu-id="ee161-1620">NX_SECURE_TLS_X509_TYPE_EXTENDED_KEY_USAGE</span></span>   | <span data-ttu-id="ee161-1621">2.5.29.37</span><span class="sxs-lookup"><span data-stu-id="ee161-1621">2.5.29.37</span></span> | <span data-ttu-id="ee161-1622">Ek OID tabanlı anahtar kullanımı bilgileri</span><span class="sxs-lookup"><span data-stu-id="ee161-1622">Additional OID-based key usage information</span></span>                                     | <span data-ttu-id="ee161-1623">Yes</span><span class="sxs-lookup"><span data-stu-id="ee161-1623">Yes</span></span>              |
| <span data-ttu-id="ee161-1624">NX_SECURE_TLS_X509_TYPE_FRESHEST_CRL</span><span class="sxs-lookup"><span data-stu-id="ee161-1624">NX_SECURE_TLS_X509_TYPE_FRESHEST_CRL</span></span>          | <span data-ttu-id="ee161-1625">2.5.29.46</span><span class="sxs-lookup"><span data-stu-id="ee161-1625">2.5.29.46</span></span> | <span data-ttu-id="ee161-1626">Delta CRL 'Leri alma hakkında bilgi sağlar</span><span class="sxs-lookup"><span data-stu-id="ee161-1626">Provides information for obtaining delta CRLs</span></span>                                  | <span data-ttu-id="ee161-1627">Hayır</span><span class="sxs-lookup"><span data-stu-id="ee161-1627">No</span></span>               |
| <span data-ttu-id="ee161-1628">NX_SECURE_TLS_X509_TYPE_INHIBIT_ANYPOLICY</span><span class="sxs-lookup"><span data-stu-id="ee161-1628">NX_SECURE_TLS_X509_TYPE_INHIBIT_ANYPOLICY</span></span>     | <span data-ttu-id="ee161-1629">2.5.29.54</span><span class="sxs-lookup"><span data-stu-id="ee161-1629">2.5.29.54</span></span> | <span data-ttu-id="ee161-1630">AnyPolicy 'in kullanılamayacağını gösteren CA sertifikası alanı</span><span class="sxs-lookup"><span data-stu-id="ee161-1630">CA certificate field indicating that AnyPolicy cannot be used</span></span>                  | <span data-ttu-id="ee161-1631">Hayır</span><span class="sxs-lookup"><span data-stu-id="ee161-1631">No</span></span>               |

<span data-ttu-id="ee161-1632">X. 509.440 uzantıları için OID ve eşlemeler</span><span class="sxs-lookup"><span data-stu-id="ee161-1632">OIDs and mappings for X.509 Extensions</span></span>

24. <span data-ttu-id="ee161-1633">SubjectAltName uzantısı, hizmet nx_secure_x509_common_name_dns_check DNS adı denetiminin bir parçası olarak ayrıştırılır.</span><span class="sxs-lookup"><span data-stu-id="ee161-1633">The SubjectAltName extension is parsed as part of the DNS name check in the service nx_secure_x509_common_name_dns_check.</span></span>

### <a name="parameters"></a><span data-ttu-id="ee161-1634">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ee161-1634">Parameters</span></span>

- <span data-ttu-id="ee161-1635">**sertifika** Doğrulanan sertifikaya yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ee161-1635">**certificate** Pointer to certificate being verified.</span></span>
- <span data-ttu-id="ee161-1636">**uzantı** Uzantı verisi işaretçisi ve uzunluğu içeren dönüş yapısı.</span><span class="sxs-lookup"><span data-stu-id="ee161-1636">**extension** Return structure containing extension data pointer and length.</span></span>
- <span data-ttu-id="ee161-1637">**extension_id** Yukarıdaki tablodan OID tamsayı eşleme.</span><span class="sxs-lookup"><span data-stu-id="ee161-1637">**extension_id** OID integer mapping from table above.</span></span>

### <a name="return-values"></a><span data-ttu-id="ee161-1638">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ee161-1638">Return Values</span></span>

- <span data-ttu-id="ee161-1639">**NX_SUCCESS** (0x00) BELIRTILEN uzantı OID 'si bulundu ve döndürülen veriler.</span><span class="sxs-lookup"><span data-stu-id="ee161-1639">**NX_SUCCESS** (0x00) Specified extension OID found and data returned.</span></span>
- <span data-ttu-id="ee161-1640">**NX_SECURE_X509_MULTIBYTE_TAG_UNSUPPORTED** (0x181) ASN. 1 Multi-Byte etiketiyle karşılaşıldı (desteklenmeyen sertifika).</span><span class="sxs-lookup"><span data-stu-id="ee161-1640">**NX_SECURE_X509_MULTIBYTE_TAG_UNSUPPORTED** (0x181) ASN.1 multi-byte tag encountered (unsupported certificate).</span></span>
- <span data-ttu-id="ee161-1641">**NX_SECURE_X509_ASN1_LENGTH_TOO_LONG** (0x182) Invaild ASN. 1 alanla karşılaşıldı (geçersiz sertifika).</span><span class="sxs-lookup"><span data-stu-id="ee161-1641">**NX_SECURE_X509_ASN1_LENGTH_TOO_LONG** (0x182) Invaild ASN.1 field encountered (invalid certificate).</span></span>
- <span data-ttu-id="ee161-1642">**NX_SECURE_X509_INVALID_TAG_CLASS** (0x190) geçersiz ASN. 1 etiket sınıfıyla karşılaşıldı (geçersiz sertifika).</span><span class="sxs-lookup"><span data-stu-id="ee161-1642">**NX_SECURE_X509_INVALID_TAG_CLASS** (0x190) Invalid ASN.1 tag class encountered (invalid certificate).</span></span>
- <span data-ttu-id="ee161-1643">**NX_SECURE_X509_INVALID_EXTENSION_SEQUENCE** (0x192) geçersiz uzantıyla karşılaşıldı</span><span class="sxs-lookup"><span data-stu-id="ee161-1643">**NX_SECURE_X509_INVALID_EXTENSION_SEQUENCE** (0x192) Invalid extension encountered</span></span>
- <span data-ttu-id="ee161-1644">**NX_SECURE_X509_EXTENSION_NOT_FOUND** (0x19b) VERILEN uzantı OID 'si sağlanan sertifikada bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="ee161-1644">**NX_SECURE_X509_EXTENSION_NOT_FOUND** (0x19B) The given extension OID was not found in the provided certificate.</span></span>
- <span data-ttu-id="ee161-1645">**NX_PTR_ERROR** (0x07) geçersiz sertifika veya uzantı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-1645">**NX_PTR_ERROR** (0x07) Invalid certificate or extension pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ee161-1646">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ee161-1646">Allowed From</span></span>

<span data-ttu-id="ee161-1647">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ee161-1647">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ee161-1648">Örnek</span><span class="sxs-lookup"><span data-stu-id="ee161-1648">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="ee161-1649">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ee161-1649">See Also</span></span>

- <span data-ttu-id="ee161-1650">nx_secure_tls_session_certificate_callback_set</span><span class="sxs-lookup"><span data-stu-id="ee161-1650">nx_secure_tls_session_certificate_callback_set</span></span>
- <span data-ttu-id="ee161-1651">nx_secure_x509_key_usage_extension_parse</span><span class="sxs-lookup"><span data-stu-id="ee161-1651">nx_secure_x509_key_usage_extension_parse</span></span>
- <span data-ttu-id="ee161-1652">nx_secure_x509_crl_revocation_check</span><span class="sxs-lookup"><span data-stu-id="ee161-1652">nx_secure_x509_crl_revocation_check</span></span>
- <span data-ttu-id="ee161-1653">nx_secure_x509_common_name_dns_check</span><span class="sxs-lookup"><span data-stu-id="ee161-1653">nx_secure_x509_common_name_dns_check</span></span>
- <span data-ttu-id="ee161-1654">nx_secure_x509_extended_key_usage_extension_parse</span><span class="sxs-lookup"><span data-stu-id="ee161-1654">nx_secure_x509_extended_key_usage_extension_parse</span></span>

## <a name="nx_secure_x509_key_usage_extension_parse"></a><span data-ttu-id="ee161-1655">nx_secure_x509_key_usage_extension_parse</span><span class="sxs-lookup"><span data-stu-id="ee161-1655">nx_secure_x509_key_usage_extension_parse</span></span>

<span data-ttu-id="ee161-1656">X. 509.440 sertifikasında X. 509.440 anahtar kullanımı uzantısını bulma ve ayrıştırma</span><span class="sxs-lookup"><span data-stu-id="ee161-1656">Find and parse an X.509 Key Usage extension in an X.509 certificate</span></span>

### <a name="prototype"></a><span data-ttu-id="ee161-1657">Prototype</span><span class="sxs-lookup"><span data-stu-id="ee161-1657">Prototype</span></span>

```C
UINT  nx_secure_x509_key_usage_extension_parse(
                        NX_SECURE_X509_CERT *certificate,
                        USHORT *bitfield);
```

### <a name="description"></a><span data-ttu-id="ee161-1658">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-1658">Description</span></span>

<span data-ttu-id="ee161-1659">Bu hizmetin bir sertifika doğrulama geri çağırması içinden çağrılması amaçlanmıştır (bkz. *nx_secure_tls_session_certificate_callback_set)*.</span><span class="sxs-lookup"><span data-stu-id="ee161-1659">This service is intended to be called from within a certificate verification callback (see *nx_secure_tls_session_certificate_callback_set)*.</span></span> <span data-ttu-id="ee161-1660">Anahtar kullanımı uzantısını arar ve bulunursa "bit alanından" parametresindeki anahtar kullanımı bitalanını döndürür.</span><span class="sxs-lookup"><span data-stu-id="ee161-1660">It will search for the Key Usage extension and if found, will return the Key Usage bitfield in the "bitfield" parameter.</span></span>

<span data-ttu-id="ee161-1661">X. 509.440 belirtimi (RFC 5280) tarafından tanımlanan bitler aşağıdaki tabloda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ee161-1661">The bits, as defined by the X.509 specification (RFC 5280) are given in the table below.</span></span> <span data-ttu-id="ee161-1662">Bit düzeyinde AND ve uygun bit maskesi (sıfır olmayan), her bitin değerini verir.</span><span class="sxs-lookup"><span data-stu-id="ee161-1662">A bitwise AND with the appropriate bitmask (and checking for non-zero) will give the value of each bit.</span></span>

<span data-ttu-id="ee161-1663">Bit alanından 'ın der-Encoding değeri, diğer sıfırları ortadan kaldırdığına göre, ham sertifika verilerinde bitlerin gerçek konumunun kodu çözülmüş bit alanından ' daki konumlarından farklı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="ee161-1663">Note that the DER-encoding of the bitfield eliminates extra zeroes so the actual position of the bits in the raw certificate data will likely be different from their positions in the decoded bitfield.</span></span> <span data-ttu-id="ee161-1664">Sağlanan bit maskeleri, ham der kodlu sertifika verileriyle değil, yalnızca *nx_secure_x509_key_usage_extension_parse* tarafından döndürülen kodu çözülmüş bit alanından üzerinde kullanılmak üzere tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="ee161-1664">The supplied bitmasks are only intended to be used on the decoded bitfield returned by *nx_secure_x509_key_usage_extension_parse* and not with the raw DER-encoded certificate data.</span></span>

<span data-ttu-id="ee161-1665">Sertifika doğrulama geri çağrısında hata dönüş kodu NX_SECURE_X509_KEY_USAGE_ERROR, uygulama kullanımı için ayrılmıştır.</span><span class="sxs-lookup"><span data-stu-id="ee161-1665">In the certificate verification callback, the error return code NX_SECURE_X509_KEY_USAGE_ERROR is reserved for application use.</span></span> <span data-ttu-id="ee161-1666">Anahtar kullanımını denetlerken bir hata oluşursa, hatanın nedenini göstermek için bu değer geri aramadan döndürülür.</span><span class="sxs-lookup"><span data-stu-id="ee161-1666">If there is an error in checking key usage, this value may be returned from the callback to indicate the reason for failure.</span></span>

| <span data-ttu-id="ee161-1667">NetX güvenli tanımlayıcısı</span><span class="sxs-lookup"><span data-stu-id="ee161-1667">NetX Secure Identifier</span></span>                            | <span data-ttu-id="ee161-1668">Bit konumu</span><span class="sxs-lookup"><span data-stu-id="ee161-1668">Bit position</span></span> | <span data-ttu-id="ee161-1669">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee161-1669">Description</span></span>                                                                                                                                                  |
| ----------------------------------------------------- | ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <span data-ttu-id="ee161-1670">NX_SECURE_X509_KEY_USAGE_DIGITAL_SIGNATURE</span><span class="sxs-lookup"><span data-stu-id="ee161-1670">NX_SECURE_X509_KEY_USAGE_DIGITAL_SIGNATURE</span></span>  | <span data-ttu-id="ee161-1671">0</span><span class="sxs-lookup"><span data-stu-id="ee161-1671">0</span></span>            | <span data-ttu-id="ee161-1672">Sertifika, dijital imzalar için kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="ee161-1672">Certificate can be used for digital signatures</span></span>                                                                                                               |
| <span data-ttu-id="ee161-1673">NX_SECURE_X509_KEY_USAGE_NON_REPUDIATION</span><span class="sxs-lookup"><span data-stu-id="ee161-1673">NX_SECURE_X509_KEY_USAGE_NON_REPUDIATION</span></span>    | <span data-ttu-id="ee161-1674">1</span><span class="sxs-lookup"><span data-stu-id="ee161-1674">1</span></span>            | <span data-ttu-id="ee161-1675">Sertifika, sertifikalar ve CRL 'Ler dışında dijital imzaları doğrulamak için kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="ee161-1675">Certificate can be used to verify digital signatures other than those for certificates and CRLs</span></span>                                                              |
| <span data-ttu-id="ee161-1676">NX_SECURE_X509_KEY_USAGE_KEY_ENCIPHERMENT</span><span class="sxs-lookup"><span data-stu-id="ee161-1676">NX_SECURE_X509_KEY_USAGE_KEY_ENCIPHERMENT</span></span>   | <span data-ttu-id="ee161-1677">2</span><span class="sxs-lookup"><span data-stu-id="ee161-1677">2</span></span>            | <span data-ttu-id="ee161-1678">Sertifika, simetrik anahtarları şifrelemek için kullanılabilir (anahtar aktarımı)</span><span class="sxs-lookup"><span data-stu-id="ee161-1678">Certificate can be used to encrypt symmetric keys (key transport)</span></span>                                                                                            |
| <span data-ttu-id="ee161-1679">NX_SECURE_X509_KEY_USAGE_DATA_ENCIPHERMENT</span><span class="sxs-lookup"><span data-stu-id="ee161-1679">NX_SECURE_X509_KEY_USAGE_DATA_ENCIPHERMENT</span></span>  | <span data-ttu-id="ee161-1680">3</span><span class="sxs-lookup"><span data-stu-id="ee161-1680">3</span></span>            | <span data-ttu-id="ee161-1681">Sertifika, ham Kullanıcı verilerini doğrudan şifrelemek için kullanılabilir (seyrek)</span><span class="sxs-lookup"><span data-stu-id="ee161-1681">Certificate can be used to directly encrypt raw user data (uncommon)</span></span>                                                                                         |
| <span data-ttu-id="ee161-1682">NX_SECURE_X509_KEY_USAGE_KEY_AGREEMENT</span><span class="sxs-lookup"><span data-stu-id="ee161-1682">NX_SECURE_X509_KEY_USAGE_KEY_AGREEMENT</span></span>      | <span data-ttu-id="ee161-1683">4</span><span class="sxs-lookup"><span data-stu-id="ee161-1683">4</span></span>            | <span data-ttu-id="ee161-1684">Sertifika, anahtar anlaşması için kullanılabilir (Diffie-Hellman ' de olduğu gibi)</span><span class="sxs-lookup"><span data-stu-id="ee161-1684">Certificate can be used for key agreement (as with Diffie-Hellman)</span></span>                                                                                           |
| <span data-ttu-id="ee161-1685">NX_SECURE_X509_KEY_USAGE_KEY_CERT_SIGN</span><span class="sxs-lookup"><span data-stu-id="ee161-1685">NX_SECURE_X509_KEY_USAGE_KEY_CERT_SIGN</span></span>     | <span data-ttu-id="ee161-1686">5</span><span class="sxs-lookup"><span data-stu-id="ee161-1686">5</span></span>            | <span data-ttu-id="ee161-1687">Sertifika, diğer sertifikaları imzalamak ve doğrulamak için kullanılabilir (sertifika bir CA veya ICA sertifikası).</span><span class="sxs-lookup"><span data-stu-id="ee161-1687">Certificate can be used to sign and verify other certificates (the certificate is a CA or ICA certificate).</span></span>                                                  |
| <span data-ttu-id="ee161-1688">NX_SECURE_X509_KEY_USAGE_CRL_SIGN</span><span class="sxs-lookup"><span data-stu-id="ee161-1688">NX_SECURE_X509_KEY_USAGE_CRL_SIGN</span></span>           | <span data-ttu-id="ee161-1689">6</span><span class="sxs-lookup"><span data-stu-id="ee161-1689">6</span></span>            | <span data-ttu-id="ee161-1690">CRL 'lerde imzaları doğrulamak için sertifika ortak anahtarı kullanılır</span><span class="sxs-lookup"><span data-stu-id="ee161-1690">Certificate public key is used to verify signatures on CRLs</span></span>                                                                                                  |
| <span data-ttu-id="ee161-1691">NX_SECURE_X509_KEY_USAGE_ENCIPHER_ONLY</span><span class="sxs-lookup"><span data-stu-id="ee161-1691">NX_SECURE_X509_KEY_USAGE_ENCIPHER_ONLY</span></span>      | <span data-ttu-id="ee161-1692">7</span><span class="sxs-lookup"><span data-stu-id="ee161-1692">7</span></span>            | <span data-ttu-id="ee161-1693">Anahtar anlaşması biti (bit 4) ile birlikte kullanıldığında – ayarlandığında, sertifika anahtarı yalnızca anahtar anlaşması sırasında şifrelemek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ee161-1693">Used with Key Agreement bit (bit 4) – when set, certificate key can only be used to encrypt during key agreement.</span></span> <span data-ttu-id="ee161-1694">Anahtar anlaşması biti ayarlanmamışsa tanımsız.</span><span class="sxs-lookup"><span data-stu-id="ee161-1694">Undefined if Key Agreement bit is not set.</span></span> |
| <span data-ttu-id="ee161-1695">NX_SECURE_X509_KEY_USAGE_DECIPHER_ONLY</span><span class="sxs-lookup"><span data-stu-id="ee161-1695">NX_SECURE_X509_KEY_USAGE_DECIPHER_ONLY</span></span>      | <span data-ttu-id="ee161-1696">8</span><span class="sxs-lookup"><span data-stu-id="ee161-1696">8</span></span>            | <span data-ttu-id="ee161-1697">Anahtar anlaşması biti (bit 4) ile birlikte kullanıldığında – ayarlandığında, sertifika anahtarı yalnızca anahtar anlaşması sırasında şifre çözme için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ee161-1697">Used with Key Agreement bit (bit 4) – when set, certificate key can only be used to decrypt during key agreement.</span></span> <span data-ttu-id="ee161-1698">Anahtar anlaşması biti ayarlanmamışsa tanımsız.</span><span class="sxs-lookup"><span data-stu-id="ee161-1698">Undefined if Key Agreement bit is not set.</span></span> |

<span data-ttu-id="ee161-1699">X. 509.440 anahtar kullanımı uzantısı için bit maskeleri ve değerler</span><span class="sxs-lookup"><span data-stu-id="ee161-1699">Bitmasks and values for X.509 Key Usage Extension</span></span>

### <a name="parameters"></a><span data-ttu-id="ee161-1700">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ee161-1700">Parameters</span></span>

- <span data-ttu-id="ee161-1701">**sertifika** Doğrulanan sertifikaya yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="ee161-1701">**certificate** Pointer to certificate being verified.</span></span>
- <span data-ttu-id="ee161-1702">**bit alanından** Uzantıdan tüm bit alanından 'ı döndürün.</span><span class="sxs-lookup"><span data-stu-id="ee161-1702">**bitfield** Return the entire bitfield from the extension.</span></span>

### <a name="return-values"></a><span data-ttu-id="ee161-1703">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ee161-1703">Return Values</span></span>

- <span data-ttu-id="ee161-1704">**NX_SUCCESS** (0x00) anahtar kullanımı uzantısı bulundu ve bit alanından döndürüldü.</span><span class="sxs-lookup"><span data-stu-id="ee161-1704">**NX_SUCCESS** (0x00) Key usage extension found and bitfield returned.</span></span>
- <span data-ttu-id="ee161-1705">**NX_SECURE_X509_MULTIBYTE_TAG_UNSUPPORTED** (0x181) ASN. 1 Multi-Byte etiketiyle karşılaşıldı (desteklenmeyen sertifika).</span><span class="sxs-lookup"><span data-stu-id="ee161-1705">**NX_SECURE_X509_MULTIBYTE_TAG_UNSUPPORTED** (0x181) ASN.1 multi-byte tag encountered (unsupported certificate).</span></span>
- <span data-ttu-id="ee161-1706">**NX_SECURE_X509_ASN1_LENGTH_TOO_LONG** (0x182) Invaild ASN. 1 alanla karşılaşıldı (geçersiz sertifika).</span><span class="sxs-lookup"><span data-stu-id="ee161-1706">**NX_SECURE_X509_ASN1_LENGTH_TOO_LONG** (0x182) Invaild ASN.1 field encountered (invalid certificate).</span></span>
- <span data-ttu-id="ee161-1707">**NX_SECURE_X509_INVALID_TAG_CLASS** (0x190) geçersiz ASN. 1 etiket sınıfıyla karşılaşıldı (geçersiz sertifika).</span><span class="sxs-lookup"><span data-stu-id="ee161-1707">**NX_SECURE_X509_INVALID_TAG_CLASS** (0x190) Invalid ASN.1 tag class encountered (invalid certificate).</span></span>
- <span data-ttu-id="ee161-1708">**NX_SECURE_X509_INVALID_EXTENSION_SEQUENCE** (0x192) geçersiz uzantıyla karşılaşıldı (geçersiz sertifika).</span><span class="sxs-lookup"><span data-stu-id="ee161-1708">**NX_SECURE_X509_INVALID_EXTENSION_SEQUENCE** (0x192) Invalid extension encountered (invalid certificate).</span></span>
- <span data-ttu-id="ee161-1709">**NX_SECURE_X509_EXTENSION_NOT_FOUND** (0x19b) anahtar kullanımı uzantısı, belirtilen sertifikada bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="ee161-1709">**NX_SECURE_X509_EXTENSION_NOT_FOUND** (0x19B)The Key Usage extension was not found in the provided certificate.</span></span>
- <span data-ttu-id="ee161-1710">**NX_PTR_ERROR** (0x07) geçersiz sertifika veya bit alanından işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ee161-1710">**NX_PTR_ERROR** (0x07) Invalid certificate or bitfield pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ee161-1711">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ee161-1711">Allowed From</span></span>

<span data-ttu-id="ee161-1712">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ee161-1712">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ee161-1713">Örnek</span><span class="sxs-lookup"><span data-stu-id="ee161-1713">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="ee161-1714">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ee161-1714">See Also</span></span>

- <span data-ttu-id="ee161-1715">nx_secure_tls_session_certificate_callback_set</span><span class="sxs-lookup"><span data-stu-id="ee161-1715">nx_secure_tls_session_certificate_callback_set</span></span>
- <span data-ttu-id="ee161-1716">nx_secure_x509_extended_key_usage_extension_parse</span><span class="sxs-lookup"><span data-stu-id="ee161-1716">nx_secure_x509_extended_key_usage_extension_parse</span></span>
- <span data-ttu-id="ee161-1717">nx_secure_x509_crl_revocation_check</span><span class="sxs-lookup"><span data-stu-id="ee161-1717">nx_secure_x509_crl_revocation_check</span></span>
- <span data-ttu-id="ee161-1718">nx_secure_x509_common_name_dns_check</span><span class="sxs-lookup"><span data-stu-id="ee161-1718">nx_secure_x509_common_name_dns_check</span></span>
- <span data-ttu-id="ee161-1719">nx_secure_x509_extension_find</span><span class="sxs-lookup"><span data-stu-id="ee161-1719">nx_secure_x509_extension_find</span></span>
