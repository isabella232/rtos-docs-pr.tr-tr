---
title: Bölüm 3-Azure RTOS NetX Duo SNMP aracı hizmetlerinin açıklaması
description: Bu bölüm, tüm NetX Duo SNMP aracı hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: cf4c4cb0edb7deb7bd0f257f48949b5c7355426b
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825768"
---
# <a name="chapter-3---description-of-azure-rtos-netx-duo-snmp-agent-services"></a><span data-ttu-id="d1e56-103">Bölüm 3-Azure RTOS NetX Duo SNMP aracı hizmetlerinin açıklaması</span><span class="sxs-lookup"><span data-stu-id="d1e56-103">Chapter 3 - Description of Azure RTOS NetX Duo SNMP agent services</span></span>

<span data-ttu-id="d1e56-104">Bu bölüm, tüm Azure RTOS NetX Duo SNMP Aracısı Hizmetleri (aşağıda listelenmiştir) alfabetik sırayla bir açıklama içerir.</span><span class="sxs-lookup"><span data-stu-id="d1e56-104">This chapter contains a description of all Azure RTOS NetX Duo SNMP agent services (listed below) in alphabetical order.</span></span>

<span data-ttu-id="d1e56-105">Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_DISABLE_ERROR_CHECKING** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-105">In the “Return Values” section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

- [<span data-ttu-id="d1e56-106">nx_snmp_agent_auth_trap_key_use</span><span class="sxs-lookup"><span data-stu-id="d1e56-106">nx_snmp_agent_auth_trap_key_use</span></span>](#nx_snmp_agent_auth_trap_key_use)
   - <span data-ttu-id="d1e56-107">*Tuzak iletileri için kimlik doğrulama anahtarını belirtin (yalnızca SNMP v3)*</span><span class="sxs-lookup"><span data-stu-id="d1e56-107">*Specify authentication key (SNMP v3 only) for trap messages*</span></span>
- [<span data-ttu-id="d1e56-108">nx_snmp_agent_authenticate_key_use</span><span class="sxs-lookup"><span data-stu-id="d1e56-108">nx_snmp_agent_authenticate_key_use</span></span>](#nx_snmp_agent_authenticate_key_use)
   - <span data-ttu-id="d1e56-109">*Yanıt iletileri için kimlik doğrulama anahtarını belirtin (yalnızca SNMP v3)*</span><span class="sxs-lookup"><span data-stu-id="d1e56-109">*Specify authentication key (SNMP v3 only) for response messages*</span></span>
- [<span data-ttu-id="d1e56-110">nx_snmp_agent_community_get</span><span class="sxs-lookup"><span data-stu-id="d1e56-110">nx_snmp_agent_community_get</span></span>](#nx_snmp_agent_community_get)
   - <span data-ttu-id="d1e56-111">*Topluluk adını al*</span><span class="sxs-lookup"><span data-stu-id="d1e56-111">*Retrieve community name*</span></span>
- [<span data-ttu-id="d1e56-112">nx_snmp_agent_context_engine_set</span><span class="sxs-lookup"><span data-stu-id="d1e56-112">nx_snmp_agent_context_engine_set</span></span>](#nx_snmp_agent_context_engine_set)
   - <span data-ttu-id="d1e56-113">*Bağlam altyapısını ayarla (yalnızca SNMP v3)*</span><span class="sxs-lookup"><span data-stu-id="d1e56-113">*Set context engine (SNMP v3 only)*</span></span>
- [<span data-ttu-id="d1e56-114">nx_snmp_agent_context_name_set</span><span class="sxs-lookup"><span data-stu-id="d1e56-114">nx_snmp_agent_context_name_set</span></span>](#nx_snmp_agent_context_name_set)
   - <span data-ttu-id="d1e56-115">*Bağlam adını ayarla (yalnızca SNMP v3)*</span><span class="sxs-lookup"><span data-stu-id="d1e56-115">*Set context name (SNMP v3 only)*</span></span>
- [<span data-ttu-id="d1e56-116">nx_snmp_agent_create</span><span class="sxs-lookup"><span data-stu-id="d1e56-116">nx_snmp_agent_create</span></span>](#nx_snmp_agent_create)
   - <span data-ttu-id="d1e56-117">*SNMP Aracısı oluşturma*</span><span class="sxs-lookup"><span data-stu-id="d1e56-117">*Create SNMP agent*</span></span>
- [<span data-ttu-id="d1e56-118">nx_snmp_agent_current_version_get</span><span class="sxs-lookup"><span data-stu-id="d1e56-118">nx_snmp_agent_current_version_get</span></span>](#nx_snmp_agent_current_version_get)
   - <span data-ttu-id="d1e56-119">*Alınan paketin SNMP sürümünü al*</span><span class="sxs-lookup"><span data-stu-id="d1e56-119">*Get the SNMP version of received packet*</span></span>
- [<span data-ttu-id="d1e56-120">nx_snmp_agent_request_get_type_test</span><span class="sxs-lookup"><span data-stu-id="d1e56-120">nx_snmp_agent_request_get_type_test</span></span>](#nx_snmp_agent_request_get_type_test)
   - <span data-ttu-id="d1e56-121">*Son SNMP isteğinin Al veya ayarla türü olduğunu belirtir*</span><span class="sxs-lookup"><span data-stu-id="d1e56-121">*Indicate if last SNMP request is GET or SET type*</span></span>
- [<span data-ttu-id="d1e56-122">nx_snmp_agent_private_string_test</span><span class="sxs-lookup"><span data-stu-id="d1e56-122">nx_snmp_agent_private_string_test</span></span>](#nx_snmp_agent_private_string_test)
   - <span data-ttu-id="d1e56-123">*Dizenin aracı özel dizesiyle eşleşip eşleşmediğini belirleme*</span><span class="sxs-lookup"><span data-stu-id="d1e56-123">*Determine if string matches agent private string*</span></span>
- [<span data-ttu-id="d1e56-124">nx_snmp_agent_public_string_test</span><span class="sxs-lookup"><span data-stu-id="d1e56-124">nx_snmp_agent_public_string_test</span></span>](#nx_snmp_agent_public_string_test)
   - <span data-ttu-id="d1e56-125">*Dizenin aracı ortak dizesiyle eşleşip eşleşmediğini belirleme*</span><span class="sxs-lookup"><span data-stu-id="d1e56-125">*Determine if string matches agent public string*</span></span>
- [<span data-ttu-id="d1e56-126">nx_snmp_agent_set_interface</span><span class="sxs-lookup"><span data-stu-id="d1e56-126">nx_snmp_agent_set_interface</span></span>](#nx_snmp_agent_set_interface)
   - <span data-ttu-id="d1e56-127">*SNMP mesajlaşma için ağ arabirimini ayarlama*</span><span class="sxs-lookup"><span data-stu-id="d1e56-127">*Set network interface for SNMP messaging*</span></span>
- [<span data-ttu-id="d1e56-128">nx_snmp_agent_private_string_set</span><span class="sxs-lookup"><span data-stu-id="d1e56-128">nx_snmp_agent_private_string_set</span></span>](#nx_snmp_agent_private_string_set)
   - <span data-ttu-id="d1e56-129">*SNMP Aracısı özel topluluk dizesini ayarla*</span><span class="sxs-lookup"><span data-stu-id="d1e56-129">*Set the SNMP agent private community string*</span></span>
- [<span data-ttu-id="d1e56-130">nx_snmp_agent_public_string_set</span><span class="sxs-lookup"><span data-stu-id="d1e56-130">nx_snmp_agent_public_string_set</span></span>](#nx_snmp_agent_public_string_set)
   - <span data-ttu-id="d1e56-131">*SNMP Aracısı ortak topluluk dizesini ayarlama*</span><span class="sxs-lookup"><span data-stu-id="d1e56-131">*Set the SNMP agent public community string*</span></span>
- [<span data-ttu-id="d1e56-132">nx_snmp_agent_version_set</span><span class="sxs-lookup"><span data-stu-id="d1e56-132">nx_snmp_agent_version_set</span></span>](#nx_snmp_agent_version_set)
   - <span data-ttu-id="d1e56-133">*Tüm SNMP sürümleri için SNMP Aracısı durumunu ayarla*</span><span class="sxs-lookup"><span data-stu-id="d1e56-133">*Set the SNMP agent status for all SNMP versions*</span></span>
- [<span data-ttu-id="d1e56-134">nx_snmp_agent_delete</span><span class="sxs-lookup"><span data-stu-id="d1e56-134">nx_snmp_agent_delete</span></span>](#nx_snmp_agent_delete)
   - <span data-ttu-id="d1e56-135">*SNMP aracısını Sil*</span><span class="sxs-lookup"><span data-stu-id="d1e56-135">*Delete SNMP agent*</span></span>
- [<span data-ttu-id="d1e56-136">nx_snmp_agent_md5_key_create</span><span class="sxs-lookup"><span data-stu-id="d1e56-136">nx_snmp_agent_md5_key_create</span></span>](#nx_snmp_agent_md5_key_create)
   - <span data-ttu-id="d1e56-137">*MD5 anahtarı oluştur (yalnızca SNMP v3)*</span><span class="sxs-lookup"><span data-stu-id="d1e56-137">*Create md5 key (SNMP v3 only)*</span></span>
- [<span data-ttu-id="d1e56-138">nx_snmp_agent_md5_key_create_extended</span><span class="sxs-lookup"><span data-stu-id="d1e56-138">nx_snmp_agent_md5_key_create_extended</span></span>](#nx_snmp_agent_md5_key_create_extended)
   - <span data-ttu-id="d1e56-139">*MD5 anahtarı oluştur (yalnızca SNMP v3)*</span><span class="sxs-lookup"><span data-stu-id="d1e56-139">*Create md5 key (SNMP v3 only)*</span></span>
- [<span data-ttu-id="d1e56-140">nx_snmp_agent_priv_trap_key_use</span><span class="sxs-lookup"><span data-stu-id="d1e56-140">nx_snmp_agent_priv_trap_key_use</span></span>](#nx_snmp_agent_priv_trap_key_use)
   - <span data-ttu-id="d1e56-141">*Tuzak iletileri için şifreleme anahtarı (yalnızca SNMP v3) belirtin*</span><span class="sxs-lookup"><span data-stu-id="d1e56-141">*Specify encryption key (SNMP v3 only) for trap messages*</span></span>
- [<span data-ttu-id="d1e56-142">nx_snmp_agent_privacy_key_use</span><span class="sxs-lookup"><span data-stu-id="d1e56-142">nx_snmp_agent_privacy_key_use</span></span>](#nx_snmp_agent_privacy_key_use)
   - <span data-ttu-id="d1e56-143">*Yanıt iletileri için şifreleme anahtarı belirtin (yalnızca SNMP v3)*</span><span class="sxs-lookup"><span data-stu-id="d1e56-143">*Specify encryption key (SNMP v3 only) for response messages*</span></span>
- [<span data-ttu-id="d1e56-144">nx_snmp_agent_sha_key_create</span><span class="sxs-lookup"><span data-stu-id="d1e56-144">nx_snmp_agent_sha_key_create</span></span>](#nx_snmp_agent_sha_key_create)
   - <span data-ttu-id="d1e56-145">*Sha anahtarı oluştur (yalnızca SNMP v3)*</span><span class="sxs-lookup"><span data-stu-id="d1e56-145">*Create sha key (SNMP v3 only)*</span></span>
- [<span data-ttu-id="d1e56-146">nx_snmp_agent_sha_key_create_extended</span><span class="sxs-lookup"><span data-stu-id="d1e56-146">nx_snmp_agent_sha_key_create_extended</span></span>](#nx_snmp_agent_sha_key_create_extended)
   - <span data-ttu-id="d1e56-147">*Sha anahtarı oluştur (yalnızca SNMP v3)*</span><span class="sxs-lookup"><span data-stu-id="d1e56-147">*Create sha key (SNMP v3 only)*</span></span>
- [<span data-ttu-id="d1e56-148">nx_snmp_agent_start</span><span class="sxs-lookup"><span data-stu-id="d1e56-148">nx_snmp_agent_start</span></span>](#nx_snmp_agent_start)
   - <span data-ttu-id="d1e56-149">*SNMP aracısını Başlat*</span><span class="sxs-lookup"><span data-stu-id="d1e56-149">*Start SNMP agent*</span></span>
- [<span data-ttu-id="d1e56-150">nx_snmp_agent_stop</span><span class="sxs-lookup"><span data-stu-id="d1e56-150">nx_snmp_agent_stop</span></span>](#nx_snmp_agent_stop)
   - <span data-ttu-id="d1e56-151">*SNMP aracısını durdur*</span><span class="sxs-lookup"><span data-stu-id="d1e56-151">*Stop SNMP agent*</span></span>
- [<span data-ttu-id="d1e56-152">nx_snmp_agent_trap_send</span><span class="sxs-lookup"><span data-stu-id="d1e56-152">nx_snmp_agent_trap_send</span></span>](#nx_snmp_agent_trap_send)
   - <span data-ttu-id="d1e56-153">*SNMP v1 tuzağı gönderme (yalnızca IPv4)*</span><span class="sxs-lookup"><span data-stu-id="d1e56-153">*Send SNMP v1 trap (IPv4 only)*</span></span>
- [<span data-ttu-id="d1e56-154">nx_snmp_agent_trapv2_send</span><span class="sxs-lookup"><span data-stu-id="d1e56-154">nx_snmp_agent_trapv2_send</span></span>](#nx_snmp_agent_trapv2_send)
   - <span data-ttu-id="d1e56-155">*SNMP v2 tuzağı gönderme (yalnızca IPv4)*</span><span class="sxs-lookup"><span data-stu-id="d1e56-155">*Send SNMP v2 trap (IPv4 only)*</span></span>
- [<span data-ttu-id="d1e56-156">nx_snmp_agent_trapv2_oid_send</span><span class="sxs-lookup"><span data-stu-id="d1e56-156">nx_snmp_agent_trapv2_oid_send</span></span>](#nx_snmp_agent_trapv2_oid_send)
   - <span data-ttu-id="d1e56-157">*OID 'yi belirterek SNMP v2 tuzağı (yalnızca IPv4) gönderin*</span><span class="sxs-lookup"><span data-stu-id="d1e56-157">*Send SNMP v2 trap (IPv4 only) specifying the OID*</span></span>
- [<span data-ttu-id="d1e56-158">nx_snmp_agent_trapv3_send</span><span class="sxs-lookup"><span data-stu-id="d1e56-158">nx_snmp_agent_trapv3_send</span></span>](#nx_snmp_agent_trapv3_send)
   - <span data-ttu-id="d1e56-159">*SNMP v3 yakalamasını gönder (yalnızca IPv4)*</span><span class="sxs-lookup"><span data-stu-id="d1e56-159">*Send SNMP v3 trap (IPv4 only)*</span></span>
- [<span data-ttu-id="d1e56-160">nx_snmp_agent_trapv3_oid_send</span><span class="sxs-lookup"><span data-stu-id="d1e56-160">nx_snmp_agent_trapv3_oid_send</span></span>](#nx_snmp_agent_trapv3_oid_send)
   - <span data-ttu-id="d1e56-161">*OID 'yi belirterek SNMP v2 tuzağı (yalnızca IPv4) gönderin*</span><span class="sxs-lookup"><span data-stu-id="d1e56-161">*Send SNMP v2 trap (IPv4 only) specifying the OID*</span></span>
- [<span data-ttu-id="d1e56-162">nxd_snmp_agent_trap_send</span><span class="sxs-lookup"><span data-stu-id="d1e56-162">nxd_snmp_agent_trap_send</span></span>](#nxd_snmp_agent_trap_send)
   - <span data-ttu-id="d1e56-163">*SNMP v1 tuzağı (IPv4 ve IPv6) gönder*</span><span class="sxs-lookup"><span data-stu-id="d1e56-163">*Send SNMP v1 trap (IPv4 and IPv6)*</span></span>
- [<span data-ttu-id="d1e56-164">nxd_snmp_agent_trapv2_send</span><span class="sxs-lookup"><span data-stu-id="d1e56-164">nxd_snmp_agent_trapv2_send</span></span>](#nxd_snmp_agent_trapv2_send)
   - <span data-ttu-id="d1e56-165">*SNMP v2 tuzağı (IPv4 ve IPv6) gönder*</span><span class="sxs-lookup"><span data-stu-id="d1e56-165">*Send SNMP v2 trap (IPv4 and IPv6)*</span></span>
- [<span data-ttu-id="d1e56-166">nxd_snmp_agent_trapv2_oid_send</span><span class="sxs-lookup"><span data-stu-id="d1e56-166">nxd_snmp_agent_trapv2_oid_send</span></span>](#nxd_snmp_agent_trapv2_oid_send)
   - <span data-ttu-id="d1e56-167">*OID 'yi belirten SNMP v2 tuzağı (IPv4/IPv6) gönderin*</span><span class="sxs-lookup"><span data-stu-id="d1e56-167">*Send SNMP v2 trap (IPv4/IPv6) specifying the OID*</span></span>
- [<span data-ttu-id="d1e56-168">nxd_snmp_agent_trapv3_send</span><span class="sxs-lookup"><span data-stu-id="d1e56-168">nxd_snmp_agent_trapv3_send</span></span>](#nxd_snmp_agent_trapv3_send)
   - <span data-ttu-id="d1e56-169">*SNMP v3 yakalamasını (IPv4 ve IPv6) gönder*</span><span class="sxs-lookup"><span data-stu-id="d1e56-169">*Send SNMP v3 trap (IPv4 and IPv6)*</span></span>
- [<span data-ttu-id="d1e56-170">nxd_snmp_agent_trapv3_oid_send</span><span class="sxs-lookup"><span data-stu-id="d1e56-170">nxd_snmp_agent_trapv3_oid_send</span></span>](#nxd_snmp_agent_trapv3_oid_send)
   - <span data-ttu-id="d1e56-171">*OID 'yi belirten SNMP v2 tuzağı (IPv4/IPv6) gönderin*</span><span class="sxs-lookup"><span data-stu-id="d1e56-171">*Send SNMP v2 trap (IPv4/IPv6) specifying the OID*</span></span>
- [<span data-ttu-id="d1e56-172">nx_snmp_agent_v3_context_boots_set</span><span class="sxs-lookup"><span data-stu-id="d1e56-172">nx_snmp_agent_v3_context_boots_set</span></span>](#nx_snmp_agent_v3_context_boots_set)
   - <span data-ttu-id="d1e56-173">*Yeniden başlatmalar sayısını ayarla*</span><span class="sxs-lookup"><span data-stu-id="d1e56-173">*Set the number of reboots*</span></span>
- [<span data-ttu-id="d1e56-174">nx_snmp_object_compare</span><span class="sxs-lookup"><span data-stu-id="d1e56-174">nx_snmp_object_compare</span></span>](#nx_snmp_object_compare)
   - <span data-ttu-id="d1e56-175">*İki nesneyi karşılaştırın*</span><span class="sxs-lookup"><span data-stu-id="d1e56-175">*Compare two objects*</span></span>
- [<span data-ttu-id="d1e56-176">nx_snmp_object_compare_extended</span><span class="sxs-lookup"><span data-stu-id="d1e56-176">nx_snmp_object_compare_extended</span></span>](#nx_snmp_object_compare_extended)
   - <span data-ttu-id="d1e56-177">*İki nesneyi karşılaştırın*</span><span class="sxs-lookup"><span data-stu-id="d1e56-177">*Compare two objects*</span></span>
- [<span data-ttu-id="d1e56-178">nx_snmp_object_copy</span><span class="sxs-lookup"><span data-stu-id="d1e56-178">nx_snmp_object_copy</span></span>](#nx_snmp_object_copy)
   - <span data-ttu-id="d1e56-179">*Nesne kopyalama*</span><span class="sxs-lookup"><span data-stu-id="d1e56-179">*Copy an object*</span></span>
- [<span data-ttu-id="d1e56-180">nx_snmp_object_copy_extended</span><span class="sxs-lookup"><span data-stu-id="d1e56-180">nx_snmp_object_copy_extended</span></span>](#nx_snmp_object_copy_extended)
   - <span data-ttu-id="d1e56-181">*Nesne kopyalama*</span><span class="sxs-lookup"><span data-stu-id="d1e56-181">*Copy an object*</span></span>
- [<span data-ttu-id="d1e56-182">nx_snmp_object_counter_get</span><span class="sxs-lookup"><span data-stu-id="d1e56-182">nx_snmp_object_counter_get</span></span>](#nx_snmp_object_counter_get)
   - <span data-ttu-id="d1e56-183">*Sayaç nesnesi Al*</span><span class="sxs-lookup"><span data-stu-id="d1e56-183">*Get counter object*</span></span>
- [<span data-ttu-id="d1e56-184">nx_snmp_object_counter_set</span><span class="sxs-lookup"><span data-stu-id="d1e56-184">nx_snmp_object_counter_set</span></span>](#nx_snmp_object_counter_set)
   - <span data-ttu-id="d1e56-185">*Sayaç nesnesi ayarla*</span><span class="sxs-lookup"><span data-stu-id="d1e56-185">*Set counter object*</span></span>
- [<span data-ttu-id="d1e56-186">nx_snmp_object_counter64_get</span><span class="sxs-lookup"><span data-stu-id="d1e56-186">nx_snmp_object_counter64_get</span></span>](#nx_snmp_object_counter64_get)
   - <span data-ttu-id="d1e56-187">*64 bitlik sayaç nesnesi Al*</span><span class="sxs-lookup"><span data-stu-id="d1e56-187">*Get 64-bit counter object*</span></span>
- [<span data-ttu-id="d1e56-188">nx_snmp_object_counter64_set</span><span class="sxs-lookup"><span data-stu-id="d1e56-188">nx_snmp_object_counter64_set</span></span>](#nx_snmp_object_counter64_set)
   - <span data-ttu-id="d1e56-189">*64 bitlik sayaç nesnesini ayarla*</span><span class="sxs-lookup"><span data-stu-id="d1e56-189">*Set 64-bit counter object*</span></span>
- [<span data-ttu-id="d1e56-190">nx_snmp_object_end_of_mib</span><span class="sxs-lookup"><span data-stu-id="d1e56-190">nx_snmp_object_end_of_mib</span></span>](#nx_snmp_object_end_of_mib)
   - <span data-ttu-id="d1e56-191">*MIB sonu değerini ayarla*</span><span class="sxs-lookup"><span data-stu-id="d1e56-191">*Set end-of-mib value*</span></span>
- [<span data-ttu-id="d1e56-192">nx_snmp_object_gauge_get</span><span class="sxs-lookup"><span data-stu-id="d1e56-192">nx_snmp_object_gauge_get</span></span>](#nx_snmp_object_gauge_get)
   - <span data-ttu-id="d1e56-193">*Ölçer nesnesini Al*</span><span class="sxs-lookup"><span data-stu-id="d1e56-193">*Get gauge object*</span></span>
- [<span data-ttu-id="d1e56-194">nx_snmp_object_gauge_set</span><span class="sxs-lookup"><span data-stu-id="d1e56-194">nx_snmp_object_gauge_set</span></span>](#nx_snmp_object_gauge_set)
   - <span data-ttu-id="d1e56-195">*Ölçer nesnesi ayarla*</span><span class="sxs-lookup"><span data-stu-id="d1e56-195">*Set gauge object*</span></span>
- [<span data-ttu-id="d1e56-196">nx_snmp_object_id_get</span><span class="sxs-lookup"><span data-stu-id="d1e56-196">nx_snmp_object_id_get</span></span>](#nx_snmp_object_id_get)
   - <span data-ttu-id="d1e56-197">*Nesne kimliğini al*</span><span class="sxs-lookup"><span data-stu-id="d1e56-197">*Get object id*</span></span>
- [<span data-ttu-id="d1e56-198">nx_snmp_object_id_set</span><span class="sxs-lookup"><span data-stu-id="d1e56-198">nx_snmp_object_id_set</span></span>](#nx_snmp_object_id_set)
   - <span data-ttu-id="d1e56-199">*Nesne kimliğini ayarla*</span><span class="sxs-lookup"><span data-stu-id="d1e56-199">*Set object id*</span></span>
- [<span data-ttu-id="d1e56-200">nx_snmp_object_integer_get</span><span class="sxs-lookup"><span data-stu-id="d1e56-200">nx_snmp_object_integer_get</span></span>](#nx_snmp_object_integer_get)
   - <span data-ttu-id="d1e56-201">*Tamsayı nesnesi Al*</span><span class="sxs-lookup"><span data-stu-id="d1e56-201">*Get integer object*</span></span>
- [<span data-ttu-id="d1e56-202">nx_snmp_object_integer_set</span><span class="sxs-lookup"><span data-stu-id="d1e56-202">nx_snmp_object_integer_set</span></span>](#nx_snmp_object_integer_set)
   - <span data-ttu-id="d1e56-203">*Tamsayı nesnesini ayarla*</span><span class="sxs-lookup"><span data-stu-id="d1e56-203">*Set integer object*</span></span>
- [<span data-ttu-id="d1e56-204">nx_snmp_object_ip_address_get</span><span class="sxs-lookup"><span data-stu-id="d1e56-204">nx_snmp_object_ip_address_get</span></span>](#nx_snmp_object_ip_address_get)
   - <span data-ttu-id="d1e56-205">*IP adresi nesnesi Al (yalnızca IPv4)*</span><span class="sxs-lookup"><span data-stu-id="d1e56-205">*Get IP address object (IPv4 only)*</span></span>
- [<span data-ttu-id="d1e56-206">nx_snmp_object_ip_address_set</span><span class="sxs-lookup"><span data-stu-id="d1e56-206">nx_snmp_object_ip_address_set</span></span>](#nx_snmp_object_ip_address_set)
   - <span data-ttu-id="d1e56-207">*IP adresi nesnesini ayarla (yalnızca IPv4)*</span><span class="sxs-lookup"><span data-stu-id="d1e56-207">*Set IP address object (IPv4 only)*</span></span>
- [<span data-ttu-id="d1e56-208">nx_snmp_object_ipv6_address_get</span><span class="sxs-lookup"><span data-stu-id="d1e56-208">nx_snmp_object_ipv6_address_get</span></span>](#nx_snmp_object_ipv6_address_get)
   - <span data-ttu-id="d1e56-209">*IP adresi nesnesi Al (yalnızca IPv6)*</span><span class="sxs-lookup"><span data-stu-id="d1e56-209">*Get IP address object (IPv6 only)*</span></span>
- [<span data-ttu-id="d1e56-210">nx_snmp_object_ipv6_address_set</span><span class="sxs-lookup"><span data-stu-id="d1e56-210">nx_snmp_object_ipv6_address_set</span></span>](#nx_snmp_object_ipv6_address_set)
   - <span data-ttu-id="d1e56-211">*IP adresi nesnesini ayarla (yalnızca IPv6)*</span><span class="sxs-lookup"><span data-stu-id="d1e56-211">*Set IP address object (IPv6 only)*</span></span>
- [<span data-ttu-id="d1e56-212">nx_snmp_object_no_instance</span><span class="sxs-lookup"><span data-stu-id="d1e56-212">nx_snmp_object_no_instance</span></span>](#nx_snmp_object_no_instance)
   - <span data-ttu-id="d1e56-213">*Örnek olmayan değer ayarla*</span><span class="sxs-lookup"><span data-stu-id="d1e56-213">*Set no-instance value*</span></span>
- [<span data-ttu-id="d1e56-214">nx_snmp_object_not_found</span><span class="sxs-lookup"><span data-stu-id="d1e56-214">nx_snmp_object_not_found</span></span>](#nx_snmp_object_not_found)
   - <span data-ttu-id="d1e56-215">*Not Found değeri ayarla*</span><span class="sxs-lookup"><span data-stu-id="d1e56-215">*Set not-found value*</span></span>
- [<span data-ttu-id="d1e56-216">nx_snmp_object_octet_string_get</span><span class="sxs-lookup"><span data-stu-id="d1e56-216">nx_snmp_object_octet_string_get</span></span>](#nx_snmp_object_octet_string_get)
   - <span data-ttu-id="d1e56-217">*Sekizli dize nesnesi Al*</span><span class="sxs-lookup"><span data-stu-id="d1e56-217">*Get octet string object*</span></span>
- [<span data-ttu-id="d1e56-218">nx_snmp_object_octet_string_set</span><span class="sxs-lookup"><span data-stu-id="d1e56-218">nx_snmp_object_octet_string_set</span></span>](#nx_snmp_object_octet_string_set)
   - <span data-ttu-id="d1e56-219">*Sekizli dize nesnesi ayarla*</span><span class="sxs-lookup"><span data-stu-id="d1e56-219">*Set octet string object*</span></span>
- [<span data-ttu-id="d1e56-220">nx_snmp_object_string_get</span><span class="sxs-lookup"><span data-stu-id="d1e56-220">nx_snmp_object_string_get</span></span>](#nx_snmp_object_string_get)
   - <span data-ttu-id="d1e56-221">*ASCII dize nesnesi Al*</span><span class="sxs-lookup"><span data-stu-id="d1e56-221">*Get ASCII string object*</span></span>
- [<span data-ttu-id="d1e56-222">nx_snmp_object_string_set</span><span class="sxs-lookup"><span data-stu-id="d1e56-222">nx_snmp_object_string_set</span></span>](#nx_snmp_object_string_set)
   - <span data-ttu-id="d1e56-223">*ASCII dize nesnesi ayarla*</span><span class="sxs-lookup"><span data-stu-id="d1e56-223">*Set ASCII string object*</span></span>
- [<span data-ttu-id="d1e56-224">nx_snmp_object_timetics_get</span><span class="sxs-lookup"><span data-stu-id="d1e56-224">nx_snmp_object_timetics_get</span></span>](#nx_snmp_object_timetics_get)
   - <span data-ttu-id="d1e56-225">*Timetika nesnesini Al*</span><span class="sxs-lookup"><span data-stu-id="d1e56-225">*Get timetics object*</span></span>
- [<span data-ttu-id="d1e56-226">nx_snmp_object_timetics_set</span><span class="sxs-lookup"><span data-stu-id="d1e56-226">nx_snmp_object_timetics_set</span></span>](#nx_snmp_object_timetics_set)
   - <span data-ttu-id="d1e56-227">*Timetika nesnesini ayarla*</span><span class="sxs-lookup"><span data-stu-id="d1e56-227">*Set timetics object*</span></span>

## <a name="nx_snmp_agent_auth_trap_key_use"></a><span data-ttu-id="d1e56-228">nx_snmp_agent_auth_trap_key_use</span><span class="sxs-lookup"><span data-stu-id="d1e56-228">nx_snmp_agent_auth_trap_key_use</span></span>
<span data-ttu-id="d1e56-229">Tuzak iletileri için kimlik doğrulama anahtarını belirt</span><span class="sxs-lookup"><span data-stu-id="d1e56-229">Specify authentication key for trap messages</span></span>

### <a name="prototype"></a><span data-ttu-id="d1e56-230">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-230">Prototype</span></span>

```c
UINT nx_snmp_agent_auth_trap_key_use(NX_SNMP_AGENT *agent_ptr, 
                                     NX_SNMP_SECURITY_KEY *key);
```
### <a name="description"></a><span data-ttu-id="d1e56-231">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-231">Description</span></span>

<span data-ttu-id="d1e56-232">Bu hizmet, tuzak iletilerindeki SNMPv3 güvenlik üstbilgisinde kimlik doğrulama parametrelerini ayarlamak için kullanılacak anahtarı belirtir.</span><span class="sxs-lookup"><span data-stu-id="d1e56-232">This service specifies the key to be used for setting authentication parameters in the SNMPv3 security header in trap messages.</span></span> <span data-ttu-id="d1e56-233">Anahtar için bir NX_NULL değeri sağlamak, kimlik doğrulamasını devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-233">Supplying a NX_NULL value for the key disables authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="d1e56-234">Anahtarın önceden oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d1e56-234">The key must be previously created.</span></span> <span data-ttu-id="d1e56-235">Bkz. nx_snmp_agent_md5_key_create veya nx_snmp_agent_sha_key_create.</span><span class="sxs-lookup"><span data-stu-id="d1e56-235">See nx_snmp_agent_md5_key_create or nx_snmp_agent_sha_key_create.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-236">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-236">Input Parameters</span></span>

- <span data-ttu-id="d1e56-237">**agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-237">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="d1e56-238">**anahtar** Daha önce oluşturulmuş bir MD5 veya SHA anahtarı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-238">**key** Pointer to a previously created MD5 or SHA key.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-239">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-239">Return Values</span></span>

- <span data-ttu-id="d1e56-240">**NX_SUCCESS** (0x00) başarılı kimlik doğrulama anahtarı kümesi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-240">**NX_SUCCESS** (0x00) Successful authentication key set.</span></span>
- <span data-ttu-id="d1e56-241">**NX_NOT_ENABLED** (0x14) SNMP güvenliği devre dışı</span><span class="sxs-lookup"><span data-stu-id="d1e56-241">**NX_NOT_ENABLED** (0x14) SNMP Security disabled</span></span> 
- <span data-ttu-id="d1e56-242">**NX_PTR_ERROR** (0x07) geçersiz SNMP aracı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-242">**NX_PTR_ERROR** (0x07) Invalid SNMP Agent pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-243">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-243">Allowed From</span></span>

<span data-ttu-id="d1e56-244">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-244">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-245">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-245">Example</span></span>

```c
/* Use previously created “my_key” for SNMPv3 trap message authentication.  */
status =  nx_snmp_agent_auth_trap_key_use(&my_agent, &my_key);


/* If status is NX_SUCCESS the SNMP Agent will use “my_key” for
   for authentication parameters in trap messages.  */
```

## <a name="nx_snmp_agent_authenticate_key_use"></a><span data-ttu-id="d1e56-246">nx_snmp_agent_authenticate_key_use</span><span class="sxs-lookup"><span data-stu-id="d1e56-246">nx_snmp_agent_authenticate_key_use</span></span>
<span data-ttu-id="d1e56-247">Yanıt iletileri için kimlik doğrulama anahtarını belirtin</span><span class="sxs-lookup"><span data-stu-id="d1e56-247">Specify authentication key for response messages</span></span>

### <a name="prototype"></a><span data-ttu-id="d1e56-248">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-248">Prototype</span></span>

```c
UINT nx_snmp_agent_authenticate_key_use(NX_SNMP_AGENT *agent_ptr, 
                                        NX_SNMP_SECURITY_KEY *key);
```
### <a name="description"></a><span data-ttu-id="d1e56-249">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-249">Description</span></span>

<span data-ttu-id="d1e56-250">Bu hizmet, ayarlandıktan sonra yapılan tüm istekler için SNMPv3 güvenlik parametresindeki kimlik doğrulama parametreleri için kullanılacak anahtarı belirtir.</span><span class="sxs-lookup"><span data-stu-id="d1e56-250">This service specifies the key to be used for authentication parameters in the SNMPv3 security parameter for all requests made after it is set.</span></span> <span data-ttu-id="d1e56-251">Anahtar için bir NX_NULL değeri sağlamak, kimlik doğrulamasını devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-251">Supplying a NX_NULL value for the key disables authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="d1e56-252">Anahtarın önceden oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d1e56-252">The key must be previously created.</span></span> <span data-ttu-id="d1e56-253">Bkz. nx_snmp_agent_md5_key_create veya nx_snmp_agent_sha_key_create.</span><span class="sxs-lookup"><span data-stu-id="d1e56-253">See nx_snmp_agent_md5_key_create or nx_snmp_agent_sha_key_create.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-254">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-254">Input Parameters</span></span>

- <span data-ttu-id="d1e56-255">**agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-255">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="d1e56-256">**anahtar** Daha önce oluşturulmuş bir MD5 veya SHA anahtarı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-256">**key** Pointer to a previously created MD5 or SHA key.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-257">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-257">Return Values</span></span>

- <span data-ttu-id="d1e56-258">**NX_SUCCESS** (0x00) başarılı SNMP anahtar kümesi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-258">**NX_SUCCESS** (0x00) Successful SNMP key set.</span></span>
- <span data-ttu-id="d1e56-259">**NX_NOT_ENABLED** (0x14) SNMP güvenliği devre dışı</span><span class="sxs-lookup"><span data-stu-id="d1e56-259">**NX_NOT_ENABLED** (0x14) SNMP Security disabled</span></span>
- <span data-ttu-id="d1e56-260">**NX_PTR_ERROR** (0x07) geçersiz SNMP aracı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-260">**NX_PTR_ERROR** (0x07) Invalid SNMP Agent pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-261">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-261">Allowed From</span></span>

<span data-ttu-id="d1e56-262">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-262">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-263">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-263">Example</span></span>

```c
/* Use previously created “my_key” for SNMPv3 authentication.  */
status =  nx_snmp_agent_authenticate_key_use(&my_agent, &my_key);


/* If status is NX_SUCCESS the SNMP Agent will use “my_key” for
   for setting the authentication parameters of SNMPv3 requests.  */
```

## <a name="nx_snmp_agent_community_get"></a><span data-ttu-id="d1e56-264">nx_snmp_agent_community_get</span><span class="sxs-lookup"><span data-stu-id="d1e56-264">nx_snmp_agent_community_get</span></span>
<span data-ttu-id="d1e56-265">Topluluk adını al</span><span class="sxs-lookup"><span data-stu-id="d1e56-265">Retrieve community name</span></span>

### <a name="prototype"></a><span data-ttu-id="d1e56-266">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-266">Prototype</span></span>

```c
UINT nx_snmp_agent_community_get(NX_SNMP_AGENT *agent_ptr, 
                                 UCHAR **community_string_ptr);
```

### <a name="description"></a><span data-ttu-id="d1e56-267">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-267">Description</span></span>

<span data-ttu-id="d1e56-268">Bu hizmet, topluluk adını SNMP Aracısı tarafından alınan en son SNMP isteğinden alır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-268">This service retrieves the community name from the most recent SNMP request received by the SNMP Agent.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-269">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-269">Input Parameters</span></span>

- <span data-ttu-id="d1e56-270">**agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-270">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="d1e56-271">**community_string_ptr** SNMP Aracısı topluluk dizesini döndürmek için bir dize işaretçisine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-271">**community_string_ptr** Pointer to a string pointer to return the SNMP Agent community string.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-272">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-272">Return Values</span></span>

- <span data-ttu-id="d1e56-273">**NX_SUCCESS** (0x00) başarılı SNMP topluluğu Get.</span><span class="sxs-lookup"><span data-stu-id="d1e56-273">**NX_SUCCESS** (0x00) Successful SNMP community get.</span></span>
- <span data-ttu-id="d1e56-274">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-274">**NX_PTR_ERROR** (0x07) Invalid input pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-275">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-275">Allowed From</span></span>

<span data-ttu-id="d1e56-276">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-276">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-277">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-277">Example</span></span>

```c
UCHAR *string_ptr;

/* Pickup the community string pointer for my_agent.  */
status =  nx_snmp_agent_community_get(&my_agent, &string_ptr);


/* If status is NX_SUCCESS the pointer “string_ptr” points to the
   last community name supplied to the SNMP agent.  */
```

## <a name="nx_snmp_agent_request_get_type_test"></a><span data-ttu-id="d1e56-278">nx_snmp_agent_request_get_type_test</span><span class="sxs-lookup"><span data-stu-id="d1e56-278">nx_snmp_agent_request_get_type_test</span></span>
<span data-ttu-id="d1e56-279">Son SNMP isteğinin Al veya ayarla türü olduğunu belirtir</span><span class="sxs-lookup"><span data-stu-id="d1e56-279">Indicate if last SNMP request is GET or SET type</span></span>

### <a name="prototype"></a><span data-ttu-id="d1e56-280">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-280">Prototype</span></span>

```c
UINT nx_snmp_agent_request_get_type_test(NX_SNMP_AGENT *agent_ptr,
                                         UINT *is_get_type);
```

### <a name="description"></a><span data-ttu-id="d1e56-281">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-281">Description</span></span>

<span data-ttu-id="d1e56-282">Bu hizmet, SNMP Yöneticisi 'ndeki en son isteğin bir GET (GET, GETNEXT veya GETBULK) veya SET türünde olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="d1e56-282">This service indicates if the most recent request from the SNMP Manager is a GET (GET, GETNEXT, or GETBULK) or SET type.</span></span> <span data-ttu-id="d1e56-283">İstek bir GET türüdür veya istek bir küme türü ise SNMP Aracısı özel dizesinde, SNMPv1 veya SNMPv2 uygulamasının alınan topluluk dizesini SNMP Aracısı ortak dizesiyle karşılaştırmak isteyeceğini, Kullanıcı adı geri çağırması ile kullanılması amaçlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-283">It is intended for use with the username callback where the SNMPv1 or SNMPv2 application will want to compare the received community string to the SNMP Agent public string if the request is a GET type, or to the SNMP Agent private string if the request is a SET type.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-284">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-284">Input Parameters</span></span>

- <span data-ttu-id="d1e56-285">**agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-285">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="d1e56-286">**is_get_type** İstek türü durumu işaretçisi:</span><span class="sxs-lookup"><span data-stu-id="d1e56-286">**is_get_type** Pointer to request type status:</span></span>  
<span data-ttu-id="d1e56-287">Tür al NX_TRUE</span><span class="sxs-lookup"><span data-stu-id="d1e56-287">NX_TRUE if GET type</span></span>  
<span data-ttu-id="d1e56-288">Tür AYARLANDıYSA NX_FALSE</span><span class="sxs-lookup"><span data-stu-id="d1e56-288">NX_FALSE if SET type</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-289">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-289">Return Values</span></span>

- <span data-ttu-id="d1e56-290">**NX_SUCCESS** (0x00) başarıyla döndürülen tür</span><span class="sxs-lookup"><span data-stu-id="d1e56-290">**NX_SUCCESS** (0x00) Successfully returned type</span></span>
- <span data-ttu-id="d1e56-291">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-291">**NX_PTR_ERROR** (0x07) Invalid input pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-292">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-292">Allowed From</span></span>

<span data-ttu-id="d1e56-293">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-293">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-294">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-294">Example</span></span>

```c
UINT is_get_type;

/* Determine if the current SNMP request is a GET or SET type.  */
status =  nx_snmp_agent_request_get_type_test(&my_agent, &is_get_type);


/* If status is NX_SUCCESS, is_get_type will indicate the request type.  */
```

## <a name="nx_snmp_agent_context_engine_set"></a><span data-ttu-id="d1e56-295">nx_snmp_agent_context_engine_set</span><span class="sxs-lookup"><span data-stu-id="d1e56-295">nx_snmp_agent_context_engine_set</span></span>
<span data-ttu-id="d1e56-296">Bağlam altyapısını ayarla (yalnızca SNMP v3)</span><span class="sxs-lookup"><span data-stu-id="d1e56-296">Set context engine (SNMP v3 only)</span></span>

### <a name="prototype"></a><span data-ttu-id="d1e56-297">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-297">Prototype</span></span>

```c
UINT nx_snmp_agent_context_engine_set(NX_SNMP_AGENT *agent_ptr, 
                                      UCHAR *context_engine, 
                                      UINT context_engine_size);
```
### <a name="description"></a><span data-ttu-id="d1e56-298">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-298">Description</span></span>

<span data-ttu-id="d1e56-299">Bu hizmet SNMP aracısının bağlam altyapısını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d1e56-299">This service sets the context engine of the SNMP Agent.</span></span> <span data-ttu-id="d1e56-300">Yalnızca SNMPv3 işleme için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="d1e56-300">It is only applicable for SNMPv3 processing.</span></span> <span data-ttu-id="d1e56-301">Uygulama kimlik doğrulama ve şifreleme kullanıyorsa, bu, anahtar oluşturma işleminde kullanıldığı için güvenlik anahtarları oluşturulmadan önce bu çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-301">This should be called before creating security keys if the application is using authentication and encryption, since the context engine ID is used in the key creation process.</span></span> <span data-ttu-id="d1e56-302">Aksi takdirde NetX Duo SNMP, *nxd_snmp. c* ' nin en üstünde varsayılan bir bağlam altyapısı kimliği sağlar:</span><span class="sxs-lookup"><span data-stu-id="d1e56-302">If not, NetX Duo SNMP provides a default context engine id at the top of *nxd_snmp.c:*</span></span>

```c
UCHAR _nx_snmp_default_context_engine[NX_SNMP_MAX_CONTEXT_STRING] =  
                {0x80, 0x00, 0x03, 0x10, 0x01, 0xc0, 0xa8, 0x64, 0xaf};

```

### <a name="input-parameters"></a><span data-ttu-id="d1e56-303">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-303">Input Parameters</span></span>

- <span data-ttu-id="d1e56-304">**agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-304">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="d1e56-305">**context_engine** Bağlam motoru dizesinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-305">**context_engine** Pointer to the context engine string.</span></span>
- <span data-ttu-id="d1e56-306">**context_engine_size** Bağlam altyapısı dizesinin boyutu.</span><span class="sxs-lookup"><span data-stu-id="d1e56-306">**context_engine_size** Size of context engine string.</span></span> <span data-ttu-id="d1e56-307">Bağlam altyapısından en fazla bayt sayısının NX_SNMP_MAX_CONTEXT_STRING göre tanımlandığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d1e56-307">Note that the maximum number of bytes in a context engine is defined by NX_SNMP_MAX_CONTEXT_STRING.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-308">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-308">Return Values</span></span>

- <span data-ttu-id="d1e56-309">**NX_SUCCESS** (0x00) başarılı SNMP bağlam altyapısı kümesi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-309">**NX_SUCCESS** (0x00) Successful SNMP context engine set.</span></span>
- <span data-ttu-id="d1e56-310">**NX_NOT_ENABLED** (0x14) SNMPv3 etkin değil</span><span class="sxs-lookup"><span data-stu-id="d1e56-310">**NX_NOT_ENABLED** (0x14) SNMPv3 is not enabled</span></span>
- <span data-ttu-id="d1e56-311">**NX_SNMP_ERROR** (0x100) bağlam altyapısı boyut hatası.</span><span class="sxs-lookup"><span data-stu-id="d1e56-311">**NX_SNMP_ERROR** (0x100) Context engine size error.</span></span>
- <span data-ttu-id="d1e56-312">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-312">**NX_PTR_ERROR** (0x07) Invalid input pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-313">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-313">Allowed From</span></span>

<span data-ttu-id="d1e56-314">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-314">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-315">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-315">Example</span></span>

```c
UCHAR my_engine[] = {0x80, 0x00, 0x01, 0x02, 0x03, 0x04, 0x05, 0x06, 0x07};

/* Set the context engine for my_agent.  */
status =  nx_snmp_agent_context_engine_set(&my_agent, my_engine, 9);


/* If status is NX_SUCCESS the context engine has been set.  */
```
## <a name="nx_snmp_agent_context_name_set"></a><span data-ttu-id="d1e56-316">nx_snmp_agent_context_name_set</span><span class="sxs-lookup"><span data-stu-id="d1e56-316">nx_snmp_agent_context_name_set</span></span>
<span data-ttu-id="d1e56-317">Bağlam adını ayarla (yalnızca SNMP v3)</span><span class="sxs-lookup"><span data-stu-id="d1e56-317">Set context name (SNMP v3 only)</span></span>

### <a name="prototype"></a><span data-ttu-id="d1e56-318">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-318">Prototype</span></span>

```c
UINT nx_snmp_agent_context_name_set(NX_SNMP_AGENT *agent_ptr, 
                                    UCHAR *context_name, 
                                    UINT context_name_size);
```

### <a name="description"></a><span data-ttu-id="d1e56-319">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-319">Description</span></span>

<span data-ttu-id="d1e56-320">Bu hizmet SNMP aracısının bağlam adını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d1e56-320">This service sets the context name of the SNMP Agent.</span></span> <span data-ttu-id="d1e56-321">Yalnızca SNMPv3 işleme için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="d1e56-321">It is only applicable for SNMPv3 processing.</span></span> <span data-ttu-id="d1e56-322">Çağrılmıyorsa NetX Duo SNMP Aracısı bağlam adını boş bırakır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-322">If not called, NetX Duo SNMP Agent will leave the context name blank.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-323">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-323">Input Parameters</span></span>

- <span data-ttu-id="d1e56-324">**agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-324">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="d1e56-325">**context_name** Bağlam adı dizesinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-325">**context_name** Pointer to the context name string.</span></span>
- <span data-ttu-id="d1e56-326">**context_name_size** Bağlam adı dizesinin boyutu.</span><span class="sxs-lookup"><span data-stu-id="d1e56-326">**context_name_size** Size of context name string.</span></span> <span data-ttu-id="d1e56-327">Bağlam adındaki en fazla bayt sayısının NX_SNMP_MAX_CONTEXT_STRING göre tanımlandığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d1e56-327">Note that the maximum number of bytes in a context name is defined by NX_SNMP_MAX_CONTEXT_STRING.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-328">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-328">Return Values</span></span>

- <span data-ttu-id="d1e56-329">**NX_SUCCESS** (0x00) başarılı SNMP bağlamı adı kümesi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-329">**NX_SUCCESS** (0x00) Successful SNMP context name set.</span></span>
- <span data-ttu-id="d1e56-330">**NX_SNMP_ERROR** (0x100) bağlam adı boyutu hatası.</span><span class="sxs-lookup"><span data-stu-id="d1e56-330">**NX_SNMP_ERROR** (0x100) Context name size error.</span></span>
- <span data-ttu-id="d1e56-331">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-331">**NX_PTR_ERROR** (0x07) Invalid input pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-332">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-332">Allowed From</span></span>

<span data-ttu-id="d1e56-333">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-333">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-334">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-334">Example</span></span>

```c
/* Set the context name for my_agent.  */
status =  nx_snmp_agent_context_name_set(&my_agent, “my_context_name”, 15);


/* If status is NX_SUCCESS the context name has been set.  */
```

## <a name="nx_snmp_agent_create"></a><span data-ttu-id="d1e56-335">nx_snmp_agent_create</span><span class="sxs-lookup"><span data-stu-id="d1e56-335">nx_snmp_agent_create</span></span>
<span data-ttu-id="d1e56-336">SNMP Aracısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d1e56-336">Create SNMP agent</span></span>

### <a name="prototype"></a><span data-ttu-id="d1e56-337">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-337">Prototype</span></span>

```c
UINT nx_snmp_agent_create(NX_SNMP_AGENT *agent_ptr, 
      CHAR *snmp_agent_name, NX_IP *ip_ptr, VOID *stack_ptr, 
      ULONG stack_size, NX_PACKET_POOL *pool_ptr,
      UINT (*snmp_agent_username_process)(struct NX_SNMP_AGENT_STRUCT 
                                    *agent_ptr, UCHAR *username),
      UINT (*snmp_agent_get_process)(struct NX_SNMP_AGENT_STRUCT 
                  *agent_ptr, UCHAR *object_requested, 
                  NX_SNMP_OBJECT_DATA *object_data),
      UINT (*snmp_agent_getnext_process)(struct NX_SNMP_AGENT_STRUCT 
                  *agent_ptr, UCHAR *object_requested, 
                  NX_SNMP_OBJECT_DATA *object_data),
      UINT (*snmp_agent_set_process)(struct NX_SNMP_AGENT_STRUCT 
                  *agent_ptr, UCHAR *object_requested, 
                  NX_SNMP_OBJECT_DATA *object_data));
```
### <a name="description"></a><span data-ttu-id="d1e56-338">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-338">Description</span></span>

<span data-ttu-id="d1e56-339">Bu hizmet, belirtilen IP örneğinde bir SNMP Aracısı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d1e56-339">This service creates a SNMP Agent on the specified IP instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-340">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-340">Input Parameters</span></span>

- <span data-ttu-id="d1e56-341">**agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-341">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="d1e56-342">**snmp_agent_name** SNMP aracı adı dizesinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-342">**snmp_agent_name** Pointer to the SNMP Agent name string.</span></span>
- <span data-ttu-id="d1e56-343">**ip_ptr** IP örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-343">**ip_ptr** Pointer to IP instance.</span></span>
- <span data-ttu-id="d1e56-344">**stack_ptr** SNMP Aracısı iş parçacığı yığın işaretçisine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-344">**stack_ptr** Pointer to SNMP Agent thread stack pointer.</span></span>
- <span data-ttu-id="d1e56-345">**stack_size** Bayt cinsinden yığın boyutu.</span><span class="sxs-lookup"><span data-stu-id="d1e56-345">**stack_size** Stack size in bytes.</span></span>
- <span data-ttu-id="d1e56-346">**pool_ptr** Bu SNMP Aracısı için varsayılan paket havuzunu işaretçisine getirin.</span><span class="sxs-lookup"><span data-stu-id="d1e56-346">**pool_ptr** Pointer the default packet pool for this SNMP Agent.</span></span>
- <span data-ttu-id="d1e56-347">**snmp_agent_username_process** Uygulamanın Kullanıcı adı işleme yordamına yönelik işlev işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-347">**snmp_agent_username_process** Function pointer to application’s username handling routine.</span></span>
- <span data-ttu-id="d1e56-348">**snmp_agent_get_process** Uygulamanın alma isteği işleme yordamına yönelik işlev işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-348">**snmp_agent_get_process** Function pointer to application’s GET request handling routine.</span></span>
- <span data-ttu-id="d1e56-349">**snmp_agent_getnext_process** Uygulamanın GETNEXT istek işleme yordamına yönelik işlev işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-349">**snmp_agent_getnext_process** Function pointer to application’s GETNEXT request handling routine.</span></span>
- <span data-ttu-id="d1e56-350">**snmp_agent_set_process** Uygulamanın ayarlanan istek işleme yordamına yönelik işlev işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-350">**snmp_agent_set_process** Function pointer to application’s SET request handling routine.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-351">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-351">Return Values</span></span>

- <span data-ttu-id="d1e56-352">**NX_SUCCESS** (0x00) başarılı SNMP Aracısı oluşturma.</span><span class="sxs-lookup"><span data-stu-id="d1e56-352">**NX_SUCCESS** (0x00) Successful SNMP Agent create.</span></span>
- <span data-ttu-id="d1e56-353">**NX_SNMP_ERROR** (0x100) SNMP Aracısı oluşturma hatası.</span><span class="sxs-lookup"><span data-stu-id="d1e56-353">**NX_SNMP_ERROR** (0x100) SNMP Agent create error.</span></span>
- <span data-ttu-id="d1e56-354">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-354">**NX_PTR_ERROR** (0x07) Invalid input pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-355">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-355">Allowed From</span></span>

<span data-ttu-id="d1e56-356">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-356">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-357">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-357">Example</span></span>

```c
NX_SNMP_AGENT my_agent;

/* Create the SNMP Agent “my_agent.”  */
status =  nx_snmp_agent_create(&my_agent, "My SNMP Agent", &ip_0, stack_start_ptr,
                4096, &pool_0, my_username_processing, my_get_processing, 
                my_getnext_processing, my_set_processing);


/* If status is NX_SUCCESS the SNMP Agent “my_agent” has been created.  */
```

## <a name="nx_snmp_agent_current_version_get"></a><span data-ttu-id="d1e56-358">nx_snmp_agent_current_version_get</span><span class="sxs-lookup"><span data-stu-id="d1e56-358">nx_snmp_agent_current_version_get</span></span>
<span data-ttu-id="d1e56-359">SNMP paket sürümünü al</span><span class="sxs-lookup"><span data-stu-id="d1e56-359">Get the SNMP packet version</span></span>

### <a name="prototype"></a><span data-ttu-id="d1e56-360">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-360">Prototype</span></span>

```c
UINT nx_snmp_agent_current_version_get(NX_SNMP_AGENT *agent_ptr, 
                                       UINT *version);
```

### <a name="description"></a><span data-ttu-id="d1e56-361">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-361">Description</span></span>

<span data-ttu-id="d1e56-362">Bu hizmet, alınan en son SNMP paketinden ayrıştırılmış SNMP sürümünü alır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-362">This service retrieves the SNMP version parsed from the most recent SNMP packet received.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-363">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-363">Input Parameters</span></span>

- <span data-ttu-id="d1e56-364">**agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-364">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="d1e56-365">**sürümü** Alınan SNMP paketindeki SNMP sürümü işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d1e56-365">**version** Pointer to the SNMP version parsed from received SNMP packet</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-366">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-366">Return Values</span></span>

- <span data-ttu-id="d1e56-367">**NX_SUCCESS** (0x00) başarılı SNMP sürümü Al</span><span class="sxs-lookup"><span data-stu-id="d1e56-367">**NX_SUCCESS** (0x00) Successful SNMP version get</span></span>
- <span data-ttu-id="d1e56-368">**NX_PTR_ERROR** (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="d1e56-368">**NX_PTR_ERROR** (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-369">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-369">Allowed From</span></span>

<span data-ttu-id="d1e56-370">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-370">Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-371">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-371">Example</span></span>

```c
UINT          snmp_version;
NX_SNMP_AGENT my_agent;

/* Get the version of the last received SNMP packet. */
status =  nx_snmp_agent_current_version_get (&my_agent, &snmp_version);


/* If status is NX_SUCCESS, snmp_version contains 
   the received packet SNMP version.  */
```

## <a name="nx_snmp_agent_private_string_test"></a><span data-ttu-id="d1e56-372">nx_snmp_agent_private_string_test</span><span class="sxs-lookup"><span data-stu-id="d1e56-372">nx_snmp_agent_private_string_test</span></span>
<span data-ttu-id="d1e56-373">Özel dize ile eşleşen aracı özel dizesini doğrula</span><span class="sxs-lookup"><span data-stu-id="d1e56-373">Verify private string matches Agent private string</span></span>

### <a name="prototype"></a><span data-ttu-id="d1e56-374">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-374">Prototype</span></span>

```c
UINT nx_snmp_agent_private_string_test(NX_SNMP_AGENT *agent_ptr, 
                                       UCHAR *community_string,          
                                       UINT *is_private);
```

### <a name="description"></a><span data-ttu-id="d1e56-375">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-375">Description</span></span>

<span data-ttu-id="d1e56-376">Bu hizmet, null sonlandırılmış giriş topluluğu dizesini SNMP Aracısı özel dizesiyle karşılaştırır ve eşleşip eşleşmediğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="d1e56-376">This service compares the null terminated input community string with the SNMP agent private string and indicates if they match.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-377">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-377">Input Parameters</span></span>

- <span data-ttu-id="d1e56-378">**agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-378">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="d1e56-379">**community_string** Karşılaştırılacak dize işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d1e56-379">**community_string** Pointer to string to compare</span></span>
- <span data-ttu-id="d1e56-380">**is_private** Karşılaştırma sonucu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d1e56-380">**is_private** Pointer to result of comparison</span></span>  
<span data-ttu-id="d1e56-381">NX_TRUE dize eşleşmeleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-381">NX_TRUE - string matches</span></span>  
<span data-ttu-id="d1e56-382">NX_FALSE dize eşleşmiyor</span><span class="sxs-lookup"><span data-stu-id="d1e56-382">NX_FALSE - string does not match</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-383">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-383">Return Values</span></span>

- <span data-ttu-id="d1e56-384">**NX_SUCCESS** (0x00) başarılı karşılaştırma</span><span class="sxs-lookup"><span data-stu-id="d1e56-384">**NX_SUCCESS** (0x00) Successful comparison</span></span>
- <span data-ttu-id="d1e56-385">**NX_PTR_ERROR** (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="d1e56-385">**NX_PTR_ERROR** (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-386">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-386">Allowed From</span></span>

<span data-ttu-id="d1e56-387">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-387">Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-388">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-388">Example</span></span>

```c
UINT        is_private;
UCHAR       *community_string_ptr;
NX_SNMP_AGENT   my_agent;

/* Determine if the community string matches the agent private string */
status =  nx_snmp_agent_private_string_test(&my_agent, community_string_ptr,  
                                            &is_private);


/* If status is NX_SUCCESS, is_private will indicate if there is a match. 
   If is_private is NX_TRUE, they match.  */
```

## <a name="nx_snmp_agent_public_string_test"></a><span data-ttu-id="d1e56-389">nx_snmp_agent_public_string_test</span><span class="sxs-lookup"><span data-stu-id="d1e56-389">nx_snmp_agent_public_string_test</span></span>
<span data-ttu-id="d1e56-390">Alınan ortak dizenin, aracının ortak dizesiyle eşleştiğinden emin olun</span><span class="sxs-lookup"><span data-stu-id="d1e56-390">Verify received public string matches Agent’s public string</span></span>

### <a name="prototype"></a><span data-ttu-id="d1e56-391">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-391">Prototype</span></span>

```c
UINT nx_snmp_agent_public_string_test(NX_SNMP_AGENT *agent_ptr, 
                                      UCHAR *community_string,          
                                      UINT *is_public);
```
### <a name="description"></a><span data-ttu-id="d1e56-392">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-392">Description</span></span>

<span data-ttu-id="d1e56-393">Bu hizmet, null sonlandırılmış bir giriş topluluğu dizesini SNMP Aracısı genel dizesiyle karşılaştırır ve eşleşip eşleşmediğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="d1e56-393">This service compares a null terminated input community string with the SNMP agent public string and indicates if they match.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-394">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-394">Input Parameters</span></span>

- <span data-ttu-id="d1e56-395">**agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-395">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="d1e56-396">**community_string** Karşılaştırılacak dize işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d1e56-396">**community_string** Pointer to string to compare</span></span>
- <span data-ttu-id="d1e56-397">**is_public** Karşılaştırma sonucu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d1e56-397">**is_public** Pointer to result of comparison</span></span>  
<span data-ttu-id="d1e56-398">NX_TRUE dize eşleşmeleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-398">NX_TRUE - string matches</span></span>  
<span data-ttu-id="d1e56-399">NX_FALSE dize eşleşmiyor</span><span class="sxs-lookup"><span data-stu-id="d1e56-399">NX_FALSE - string does not match</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-400">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-400">Return Values</span></span>

- <span data-ttu-id="d1e56-401">**NX_SUCCESS** (0x00) başarılı karşılaştırma</span><span class="sxs-lookup"><span data-stu-id="d1e56-401">**NX_SUCCESS** (0x00) Successful comparison</span></span>
- <span data-ttu-id="d1e56-402">**NX_PTR_ERROR** (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="d1e56-402">**NX_PTR_ERROR** (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-403">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-403">Allowed From</span></span>

<span data-ttu-id="d1e56-404">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-404">Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-405">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-405">Example</span></span>

```c
UINT        is_public;
UCHAR       *community_string_ptr;
NX_SNMP_AGENT   my_agent;


/* Determine if the community string matches the agent public string */
status =  nx_snmp_agent_public_string_test(&my_agent, community_string_ptr,  
                                           &is_public);


/* If status is NX_SUCCESS, is_public will indicate if there is a match. 
   If is_public is true they match.  */
```

## <a name="nx_snmp_agent_version_set"></a><span data-ttu-id="d1e56-406">nx_snmp_agent_version_set</span><span class="sxs-lookup"><span data-stu-id="d1e56-406">nx_snmp_agent_version_set</span></span>
<span data-ttu-id="d1e56-407">Her SNMP sürümü için SNMP aracı durumunu ayarla</span><span class="sxs-lookup"><span data-stu-id="d1e56-407">Set the SNMP agent status for each SNMP version</span></span>

### <a name="prototype"></a><span data-ttu-id="d1e56-408">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-408">Prototype</span></span>

```c
UINT nx_snmp_agent_version_set(NX_SNMP_AGENT *agent_ptr, 
                               UINT enabled_v1, UINT enable_v2, 
                               UINT enable_v3);
```

### <a name="description"></a><span data-ttu-id="d1e56-409">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-409">Description</span></span>

<span data-ttu-id="d1e56-410">Bu hizmet SNMP aracısındaki her bir SNMP sürümü, v1, v2 ve v3 için durumu (etkin/devre dışı) ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d1e56-410">This service sets the status (enabled/disabled) for each of the SNMP versions, V1, V2 and V3 on the SNMP agent.</span></span> <span data-ttu-id="d1e56-411">Kullanıcı tarafından yapılandırılabilir seçenekler, NX_SNMP_DISABLE_V1, NX_SNMP_DISABLE_V2 ve NX_SNMP_DISABLE_V3, bu çalışma zamanı ayarlarını geçersiz kıldığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d1e56-411">Note that the user configurable options, NX_SNMP_DISABLE_V1, NX_SNMP_DISABLE_V2, and NX_SNMP_DISABLE_V3, will override these run time settings.</span></span> <span data-ttu-id="d1e56-412">Varsayılan olarak, SNMP Aracısı üç sürüm için etkinleştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="d1e56-412">By default, the SNMP agent is enabled for all three versions.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-413">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-413">Input Parameters</span></span>

- <span data-ttu-id="d1e56-414">**agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-414">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="d1e56-415">**enabled_v1** SNMP v1 için etkin durumu açık/kapalı olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d1e56-415">**enabled_v1** Sets enabled status for SNMP V1 to on/off.</span></span>
- <span data-ttu-id="d1e56-416">**enabled_v2** SNMP v2 için etkin durumu açık/kapalı olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d1e56-416">**enabled_v2** Sets enabled status for SNMP V2 to on/off.</span></span>
- <span data-ttu-id="d1e56-417">**enabled_v3** SNMP v3 için etkin durumu açık/kapalı olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d1e56-417">**enabled_v3** Sets enabled status for SNMP V3 to on/off.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-418">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-418">Return Values</span></span>

- <span data-ttu-id="d1e56-419">**NX_SUCCESS** (0x00) başarılı SNMP sürümü kümesi</span><span class="sxs-lookup"><span data-stu-id="d1e56-419">**NX_SUCCESS** (0x00) Successful SNMP version set</span></span>
- <span data-ttu-id="d1e56-420">**NX_PTR_ERROR** (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="d1e56-420">**NX_PTR_ERROR** (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-421">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-421">Allowed From</span></span>

<span data-ttu-id="d1e56-422">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-422">Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-423">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-423">Example</span></span>

```c
UINT          v1_on = NX_TRUE;
UINT          v2_on = NX_TRUE;
UINT          v3_on = NX_FALSE;

NX_SNMP_AGENT my_agent;

/* Enable/Disable each SNMP protocol (version) for the SNMP Agent) */
status =  nx_snmp_agent_version_set(&my_agent, v1_on, v2_on, v3_on);


/* If status is NX_SUCCESS, my_agent is enabled only for V1 and V2 assuming 
   NX_SNMP_DISABLE_V1 and NX_SNMP_DISABLE_V2 are not defined. */
```

## <a name="nx_snmp_agent_private_string_set"></a><span data-ttu-id="d1e56-424">nx_snmp_agent_private_string_set</span><span class="sxs-lookup"><span data-stu-id="d1e56-424">nx_snmp_agent_private_string_set</span></span>
<span data-ttu-id="d1e56-425">SNMP Aracısı özel dizesini ayarla</span><span class="sxs-lookup"><span data-stu-id="d1e56-425">Set the SNMP agent private string</span></span>

### <a name="prototype"></a><span data-ttu-id="d1e56-426">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-426">Prototype</span></span>

```c
UINT nx_snmp_agent_private_string_set(NX_SNMP_AGENT *agent_ptr, 
                                      UCHAR *community_string);
```

### <a name="description"></a><span data-ttu-id="d1e56-427">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-427">Description</span></span>

<span data-ttu-id="d1e56-428">Bu hizmet SNMP Aracısı özel topluluk dizesini girdi null sonlandırılmış dizesiyle ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d1e56-428">This service sets the SNMP agent private community string with the input null terminated string.</span></span> <span data-ttu-id="d1e56-429">Varsayılan değer NULL (özel dize kümesi yoktur), "özel" topluluk dizesiyle alınan tüm SNMP paketleri, okuma/yazma erişimi için SNMP Aracısı tarafından kabul edilmez.</span><span class="sxs-lookup"><span data-stu-id="d1e56-429">The default value is NULL (no private string set), such that any SNMP packet received with a “private” community string will not be accepted by the SNMP agent for read/write access.</span></span> <span data-ttu-id="d1e56-430">Giriş dizesi Kullanıcı tarafından yapılandırılabilir NX_SNMP_MAX_USER_NAME-1 ' e eşit veya ondan küçük olmalıdır (null sonlandırma için odaya izin vermek için) boyutu.</span><span class="sxs-lookup"><span data-stu-id="d1e56-430">The input string must be less than or equal to the user configurable NX_SNMP_MAX_USER_NAME-1 (to allow room for null termination) size.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-431">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-431">Input Parameters</span></span>

- <span data-ttu-id="d1e56-432">**agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-432">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="d1e56-433">**community_string** Atanacak özel dizeye yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="d1e56-433">**community_string** Pointer to the private string to assign</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-434">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-434">Return Values</span></span>

- <span data-ttu-id="d1e56-435">**NX_SUCCESS** (0x00) özel dize başarıyla ayarlandı</span><span class="sxs-lookup"><span data-stu-id="d1e56-435">**NX_SUCCESS** (0x00) Successfully set private string</span></span>
- <span data-ttu-id="d1e56-436">**NX_SNMP_ERROR_TOOBIG** (0x01) dize boyutu çok büyük</span><span class="sxs-lookup"><span data-stu-id="d1e56-436">**NX_SNMP_ERROR_TOOBIG** (0x01) String size too large</span></span> 
- <span data-ttu-id="d1e56-437">**NX_PTR_ERROR** (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="d1e56-437">**NX_PTR_ERROR** (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-438">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-438">Allowed From</span></span>

<span data-ttu-id="d1e56-439">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-439">Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-440">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-440">Example</span></span>

```c
NX_SNMP_AGENT my_agent;

/* Set the SNMP agent’s private community string */
status =  nx_snmp_agent_private_string_set(&my_agent, “private”));


/* If status is NX_SUCCESS, the SNMP agent private string is set.  */
```

## <a name="nx_snmp_agent_public_string_set"></a><span data-ttu-id="d1e56-441">nx_snmp_agent_public_string_set</span><span class="sxs-lookup"><span data-stu-id="d1e56-441">nx_snmp_agent_public_string_set</span></span>
<span data-ttu-id="d1e56-442">SNMP Aracısı genel dizesini ayarla</span><span class="sxs-lookup"><span data-stu-id="d1e56-442">Set the SNMP agent public string</span></span>

### <a name="prototype"></a><span data-ttu-id="d1e56-443">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-443">Prototype</span></span>

```c
UINT nx_snmp_agent_public_string_set(NX_SNMP_AGENT *agent_ptr, 
                                     UCHAR *community_string);
```

### <a name="description"></a><span data-ttu-id="d1e56-444">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-444">Description</span></span>

<span data-ttu-id="d1e56-445">Bu hizmet SNMP Aracısı ortak topluluk dizesini girdi null sonlandırılmış dizesiyle ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d1e56-445">This service sets the SNMP agent public community string with the input null terminated string.</span></span> <span data-ttu-id="d1e56-446">Topluluk dizesi, Kullanıcı tarafından yapılandırılabilir NX_SNMP_MAX_USER_NAME-1 ' e eşit veya ondan küçük olmalıdır (null sonlandırma için odaya izin vermek için) boyutu.</span><span class="sxs-lookup"><span data-stu-id="d1e56-446">The community string must be less than or equal to the user configurable NX_SNMP_MAX_USER_NAME-1 (to allow room for null termination) size.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-447">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-447">Input Parameters</span></span>

- <span data-ttu-id="d1e56-448">**agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-448">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="d1e56-449">**community_string** Atanacak ortak dizenin işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d1e56-449">**community_string** Pointer to the public string to assign</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-450">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-450">Return Values</span></span>

- <span data-ttu-id="d1e56-451">**NX_SUCCESS** (0x00) genel dize başarıyla ayarlandı</span><span class="sxs-lookup"><span data-stu-id="d1e56-451">**NX_SUCCESS** (0x00) Successfully set public string</span></span>
- <span data-ttu-id="d1e56-452">**NX_SNMP_ERROR_TOOBIG** (0x01) dize boyutu çok büyük</span><span class="sxs-lookup"><span data-stu-id="d1e56-452">**NX_SNMP_ERROR_TOOBIG** (0x01) String size too large</span></span>
- <span data-ttu-id="d1e56-453">**NX_PTR_ERROR** (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="d1e56-453">**NX_PTR_ERROR** (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-454">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-454">Allowed From</span></span>

<span data-ttu-id="d1e56-455">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-455">Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-456">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-456">Example</span></span>

```c
NX_SNMP_AGENT my_agent;

/* Set the SNMP agent’s public string. */
nx_snmp_agent_public_string_set(&my_agent, “my_public”));


/* If status is NX_SUCCESS, the SNMP agent public string is set.  */
```

## <a name="nx_snmp_agent_delete"></a><span data-ttu-id="d1e56-457">nx_snmp_agent_delete</span><span class="sxs-lookup"><span data-stu-id="d1e56-457">nx_snmp_agent_delete</span></span>
<span data-ttu-id="d1e56-458">SNMP aracısını Sil</span><span class="sxs-lookup"><span data-stu-id="d1e56-458">Delete SNMP agent</span></span>

### <a name="prototype"></a><span data-ttu-id="d1e56-459">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-459">Prototype</span></span>

```C
UINT nx_snmp_agent_delete(NX_SNMP_AGENT *agent_ptr);
```
### <a name="description"></a><span data-ttu-id="d1e56-460">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-460">Description</span></span>

<span data-ttu-id="d1e56-461">Bu hizmet önceden oluşturulmuş bir SNMP aracısını siler.</span><span class="sxs-lookup"><span data-stu-id="d1e56-461">This service deletes a previously created SNMP Agent.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-462">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-462">Input Parameters</span></span>

- <span data-ttu-id="d1e56-463">**agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-463">**agent_ptr** Pointer to SNMP Agent control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-464">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-464">Return Values</span></span>

- <span data-ttu-id="d1e56-465">**NX_SUCCESS** (0x00) başarılı SNMP Aracısı silme.</span><span class="sxs-lookup"><span data-stu-id="d1e56-465">**NX_SUCCESS** (0x00) Successful SNMP Agent delete.</span></span>
- <span data-ttu-id="d1e56-466">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-466">**NX_PTR_ERROR** (0x07) Invalid input pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-467">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-467">Allowed From</span></span>

<span data-ttu-id="d1e56-468">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-468">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-469">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-469">Example</span></span>

```c
/* Delete the SNMP Agent “my_agent.”  */
status =  nx_snmp_agent_delete(&my_agent);


/* If status is NX_SUCCESS the SNMP Agent “my_agent” has been deleted.  */
```

## <a name="nx_snmp_agent_set_interface"></a><span data-ttu-id="d1e56-470">nx_snmp_agent_set_interface</span><span class="sxs-lookup"><span data-stu-id="d1e56-470">nx_snmp_agent_set_interface</span></span>
<span data-ttu-id="d1e56-471">SNMP Aracısı ağ arabirimini ayarlama</span><span class="sxs-lookup"><span data-stu-id="d1e56-471">Set the SNMP agent network interface</span></span>

### <a name="prototype"></a><span data-ttu-id="d1e56-472">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-472">Prototype</span></span>

```c
UINT nx_snmp_agent_set_interface(NX_SNMP_AGENT *agent_ptr,  
                                 UINT if_index);
```

### <a name="description"></a><span data-ttu-id="d1e56-473">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-473">Description</span></span>

<span data-ttu-id="d1e56-474">Bu hizmet, SNMP aracısının SNMP ağ arabirimini giriş arabirimi dizini tarafından belirtilen şekilde ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d1e56-474">This service sets the SNMP network interface for the SNMP Agent as specified by the input interface index.</span></span> <span data-ttu-id="d1e56-475">Bu, yalnızca NetX Duo 5,6 veya üzeri olan SNMP ana bilgisayar uygulamaları için çok sayıda ağ arabirimini destekledikleri için yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-475">This is only useful for SNMP host applications with NetX Duo 5.6 or higher which support multiple network interfaces.</span></span> <span data-ttu-id="d1e56-476">Ana bilgisayar tarafından belirtilmemişse, birincil arabirim için varsayılan değer sıfırdır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-476">The default value if not specified by the host is zero, for the primary interface.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-477">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-477">Input Parameters</span></span>

- <span data-ttu-id="d1e56-478">**agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-478">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="d1e56-479">**If_index** SNMP arabirimini belirten Dizin.</span><span class="sxs-lookup"><span data-stu-id="d1e56-479">**If_index** Index specifying the SNMP interface.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-480">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-480">Return Values</span></span>

- <span data-ttu-id="d1e56-481">**NX_SUCCESS** (0x00) başarılı SNMP arabirimi kümesi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-481">**NX_SUCCESS** (0x00) Successful SNMP interface set.</span></span>
- <span data-ttu-id="d1e56-482">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-482">**NX_PTR_ERROR** (0x07) Invalid input pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-483">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-483">Allowed From</span></span>

<span data-ttu-id="d1e56-484">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-484">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-485">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-485">Example</span></span>

```c
/* Set the SNMP Agent “my_agent” to the secondary interface.  */
if_index = 1;
status =  nx_snmp_agent_set_interface(&my_agent, if_index);


/* If status is NX_SUCCESS the SNMP agent interface is set.  */
```

## <a name="nx_snmp_agent_md5_key_create"></a><span data-ttu-id="d1e56-486">nx_snmp_agent_md5_key_create</span><span class="sxs-lookup"><span data-stu-id="d1e56-486">nx_snmp_agent_md5_key_create</span></span>
<span data-ttu-id="d1e56-487">MD5 anahtarı oluştur (yalnızca SNMP v3)</span><span class="sxs-lookup"><span data-stu-id="d1e56-487">Create md5 key (SNMP v3 only)</span></span>

### <a name="prototype"></a><span data-ttu-id="d1e56-488">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-488">Prototype</span></span>

```c
UINT nx_snmp_agent_md5_key_create(NX_SNMP_AGENT *agent_ptr, 
                                  UCHAR *password, 
                                  NX_SNMP_SECURITY_KEY 
                                       *destination_key);
```
### <a name="description"></a><span data-ttu-id="d1e56-489">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-489">Description</span></span>

<span data-ttu-id="d1e56-490">Bu hizmet, kimlik doğrulama ve şifreleme için kullanılabilen bir MD5 anahtarı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d1e56-490">This service creates a MD5 key that can be used for authentication and encryption.</span></span>

<span data-ttu-id="d1e56-491">Bu hizmet kullanımdan kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-491">This service is deprecated.</span></span> <span data-ttu-id="d1e56-492">Geliştiricilerin *nx_snmp_agent_md5_key_create_extended ()* uygulamasına geçirilmesi önerilir.</span><span class="sxs-lookup"><span data-stu-id="d1e56-492">Developers are encouraged to migrate to *nx_snmp_agent_md5_key_create_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-493">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-493">Input Parameters</span></span>

- <span data-ttu-id="d1e56-494">**agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-494">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="d1e56-495">**parola** Parola dizesi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-495">**password** Pointer to password string.</span></span>
- <span data-ttu-id="d1e56-496">**destination_key** SNMP anahtar veri yapısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-496">**destination_key** Pointer to SNMP key data structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-497">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-497">Return Values</span></span>

- <span data-ttu-id="d1e56-498">**NX_SUCCESS** (0x00) başarılı anahtar oluştur.</span><span class="sxs-lookup"><span data-stu-id="d1e56-498">**NX_SUCCESS** (0x00) Successful key create.</span></span>
- <span data-ttu-id="d1e56-499">**NX_NOT_ENABLED** (0x14) güvenlik etkin değil.</span><span class="sxs-lookup"><span data-stu-id="d1e56-499">**NX_NOT_ENABLED** (0x14) Security not enabled.</span></span>
- <span data-ttu-id="d1e56-500">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-500">**NX_PTR_ERROR** (0x07) Invalid input pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-501">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-501">Allowed From</span></span>

<span data-ttu-id="d1e56-502">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-502">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-503">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-503">Example</span></span>

```c
NX_SNMP_SECURITY_KEY my_key;

/* Create the MD5 key for “my_agent.”   */
status =  nx_snmp_agent_md5_key_create(&my_agent, “authpw”, &my_key);


/* If status is NX_SUCCESS an MD5 key has been created.  */
```

## <a name="nx_snmp_agent_md5_key_create_extended"></a><span data-ttu-id="d1e56-504">nx_snmp_agent_md5_key_create_extended</span><span class="sxs-lookup"><span data-stu-id="d1e56-504">nx_snmp_agent_md5_key_create_extended</span></span>
<span data-ttu-id="d1e56-505">MD5 anahtarı oluştur (yalnızca SNMP v3)</span><span class="sxs-lookup"><span data-stu-id="d1e56-505">Create md5 key (SNMP v3 only)</span></span>

### <a name="prototype"></a><span data-ttu-id="d1e56-506">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-506">Prototype</span></span>

```c
UINT nx_snmp_agent_md5_key_create_extended(NX_SNMP_AGENT *agent_ptr, 
                                           UCHAR *password, 
                                           UINT password_length,
                                           NX_SNMP_SECURITY_KEY 
                                           *destination_key);
```
### <a name="description"></a><span data-ttu-id="d1e56-507">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-507">Description</span></span>

<span data-ttu-id="d1e56-508">Bu hizmet, kimlik doğrulama ve şifreleme için kullanılabilen bir MD5 anahtarı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d1e56-508">This service creates a MD5 key that can be used for authentication and encryption.</span></span>

<span data-ttu-id="d1e56-509">Bu hizmet *nx_snmp_agent_md5_key_create ()* yerini alır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-509">This service replaces *nx_snmp_agent_md5_key_create().*</span></span> <span data-ttu-id="d1e56-510">Bu sürüm için çağıranın parola uzunluğu sağlaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d1e56-510">This version requires caller to supply password length.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-511">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-511">Input Parameters</span></span>

- <span data-ttu-id="d1e56-512">**agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-512">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="d1e56-513">**parola** Parola dizesi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-513">**password** Pointer to password string.</span></span>
- <span data-ttu-id="d1e56-514">**password_length** Parola dizesinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="d1e56-514">**password_length** Length of password string.</span></span>
- <span data-ttu-id="d1e56-515">**destination_key** SNMP anahtar veri yapısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-515">**destination_key** Pointer to SNMP key data structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-516">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-516">Return Values</span></span>

- <span data-ttu-id="d1e56-517">**NX_SUCCESS** (0x00) başarılı anahtar oluştur.</span><span class="sxs-lookup"><span data-stu-id="d1e56-517">**NX_SUCCESS** (0x00) Successful key create.</span></span>
- <span data-ttu-id="d1e56-518">**NX_NOT_ENABLED** (0x14) güvenlik etkin değil.</span><span class="sxs-lookup"><span data-stu-id="d1e56-518">**NX_NOT_ENABLED** (0x14) Security not enabled.</span></span>
- <span data-ttu-id="d1e56-519">**NX_SNMP_FAILED** (0x102) SNMP başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="d1e56-519">**NX_SNMP_FAILED** (0x102) SNMP failed.</span></span>
- <span data-ttu-id="d1e56-520">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-520">**NX_PTR_ERROR** (0x07) Invalid input pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-521">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-521">Allowed From</span></span>

<span data-ttu-id="d1e56-522">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-522">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-523">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-523">Example</span></span>

```c
NX_SNMP_SECURITY_KEY my_key;

/* Create the MD5 key for “my_agent.”   */
status =  nx_snmp_agent_md5_key_create_extended(&my_agent, “authpw”, 6, &my_key);


/* If status is NX_SUCCESS the key for the password “authpw” has been created.  */
```

## <a name="nx_snmp_agent_priv_trap_key_use"></a><span data-ttu-id="d1e56-524">nx_snmp_agent_priv_trap_key_use</span><span class="sxs-lookup"><span data-stu-id="d1e56-524">nx_snmp_agent_priv_trap_key_use</span></span>
<span data-ttu-id="d1e56-525">Tuzak iletileri için şifreleme anahtarı belirtin</span><span class="sxs-lookup"><span data-stu-id="d1e56-525">Specify encryption key for trap messages</span></span>

### <a name="prototype"></a><span data-ttu-id="d1e56-526">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-526">Prototype</span></span>

```c
UINT nx_snmp_agent_priv_trap_key_use(NX_SNMP_AGENT *agent_ptr, 
                                     NX_SNMP_SECURITY_KEY *key);
```

### <a name="description"></a><span data-ttu-id="d1e56-527">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-527">Description</span></span>

<span data-ttu-id="d1e56-528">Bu hizmet, önceden oluşturulmuş bir gizlilik anahtarının, SNMPv3 tuzak iletilerinin şifrelenmesi ve şifresinin çözülmesi için kullanıldığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="d1e56-528">This service specifies that a previously created privacy key is to be used for encryption and decryption of SNMPv3 trap messages.</span></span>

> [!NOTE]
> <span data-ttu-id="d1e56-529">*Authentictation anahtarının önceden oluşturulması gerekir. SNMP v3 gizliliği (şifreleme) kimlik doğrulaması gerektirir. Ayrıntılar için nx_snmp_agent_auth_trap_key_use bakın.*</span><span class="sxs-lookup"><span data-stu-id="d1e56-529">*An authentictation key must be previously created. SNMP v3 privacy (encryption) requires authentication. See nx_snmp_agent_auth_trap_key_use for details.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-530">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-530">Input Parameters</span></span>

- <span data-ttu-id="d1e56-531">**agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-531">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="d1e56-532">**anahtar** Daha önce anahtar oluşturma işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-532">**key** Pointer to previously create key.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-533">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-533">Return Values</span></span>

- <span data-ttu-id="d1e56-534">**NX_SUCCESS** (0x00) başarılı gizlilik anahtarı kümesi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-534">**NX_SUCCESS** (0x00) Successful privacy key set.</span></span>
- <span data-ttu-id="d1e56-535">**NX_NOT_ENABLED** (0x14) güvenlik etkin değil.</span><span class="sxs-lookup"><span data-stu-id="d1e56-535">**NX_NOT_ENABLED** (0x14) Security not enabled.</span></span>
- <span data-ttu-id="d1e56-536">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-536">**NX_PTR_ERROR** (0x07) Invalid input pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-537">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-537">Allowed From</span></span>

<span data-ttu-id="d1e56-538">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-538">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-539">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-539">Example</span></span>

```c
/* Use the “my_privacy_key” for the SNMP Agent “my_agent” trap messages.   */
status =  nx_snmp_agent_priv_trap_key_use(&my_agent, &my_privacy_key);


/* If status is NX_SUCCESS the privacy key is registered with the SNMP agent.  */
```

## <a name="nx_snmp_agent_privacy_key_use"></a><span data-ttu-id="d1e56-540">nx_snmp_agent_privacy_key_use</span><span class="sxs-lookup"><span data-stu-id="d1e56-540">nx_snmp_agent_privacy_key_use</span></span>
<span data-ttu-id="d1e56-541">Yanıt iletileri için şifreleme anahtarı belirtin</span><span class="sxs-lookup"><span data-stu-id="d1e56-541">Specify encryption key for response messages</span></span>

### <a name="prototype"></a><span data-ttu-id="d1e56-542">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-542">Prototype</span></span>

```c
UINT nx_snmp_agent_privacy_key_use(NX_SNMP_AGENT *agent_ptr, 
                                   NX_SNMP_SECURITY_KEY *key);
```
### <a name="description"></a><span data-ttu-id="d1e56-543">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-543">Description</span></span>

<span data-ttu-id="d1e56-544">Bu hizmet, önceden oluşturulmuş anahtarın, SNMPv3 yanıt iletilerinin şifrelenmesi ve şifresinin çözülmesi için kullanıldığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="d1e56-544">This service specifies that the previously created key is to be used for encryption and decryption of SNMPv3 response messages.</span></span>

> [!NOTE]
> <span data-ttu-id="d1e56-545">*Bir kimlik doğrulama anahtarı daha önce belirtilmiş olmalıdır. SNMP v3 şifrelemesi de bir kimlik doğrulama anahtarı oluşturulmasını gerektirir. Ayrıntılar için nx_snmp_agent_authentiation_key_use bakın.*</span><span class="sxs-lookup"><span data-stu-id="d1e56-545">*An authentication key must have previously been specified. SNMP v3 encryption requires creation of an authentication key as well. See nx_snmp_agent_authentiation_key_use for details.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-546">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-546">Input Parameters</span></span>

- <span data-ttu-id="d1e56-547">**agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-547">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="d1e56-548">**anahtar** Daha önce anahtar oluşturma işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-548">**key** Pointer to previously create key.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-549">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-549">Return Values</span></span>

- <span data-ttu-id="d1e56-550">**NX_SUCCESS** (0x00) başarılı gizlilik anahtarı kümesi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-550">**NX_SUCCESS** (0x00) Successful privacy key set.</span></span>
- <span data-ttu-id="d1e56-551">**NX_NOT_ENABLED** (0x14) güvenlik etkin değil.</span><span class="sxs-lookup"><span data-stu-id="d1e56-551">**NX_NOT_ENABLED** (0x14) Security not enabled.</span></span>
- <span data-ttu-id="d1e56-552">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-552">**NX_PTR_ERROR** (0x07) Invalid input pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-553">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-553">Allowed From</span></span>

<span data-ttu-id="d1e56-554">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-554">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-555">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-555">Example</span></span>

```c
/* Use the “my_privacy_key” for the SNMP Agent “my_agent.”   */
status =  nx_snmp_agent_privacy_key_use(&my_agent, &my_privacy_key);


/* If status is NX_SUCCESS the privacy key is registered with the SNMP agent.  */
```

## <a name="nx_snmp_agent_sha_key_create"></a><span data-ttu-id="d1e56-556">nx_snmp_agent_sha_key_create</span><span class="sxs-lookup"><span data-stu-id="d1e56-556">nx_snmp_agent_sha_key_create</span></span>
<span data-ttu-id="d1e56-557">SHA anahtarı oluştur (yalnızca SNMP v3)</span><span class="sxs-lookup"><span data-stu-id="d1e56-557">Create SHA key (SNMP v3 only)</span></span>

### <a name="prototype"></a><span data-ttu-id="d1e56-558">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-558">Prototype</span></span>

```c
UINT nx_snmp_agent_sha_key_create(NX_SNMP_AGENT *agent_ptr, 
                                  UCHAR *password, 
                                  NX_SNMP_SECURITY_KEY  
                                  *destination_key);
```
### <a name="description"></a><span data-ttu-id="d1e56-559">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-559">Description</span></span>

<span data-ttu-id="d1e56-560">Bu hizmet, kimlik doğrulama ve şifreleme için kullanılabilen bir SHA anahtarı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d1e56-560">This service creates a SHA key that can be used for authentication and encryption.</span></span>

<span data-ttu-id="d1e56-561">Bu hizmet kullanımdan kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-561">This service is deprecated.</span></span> <span data-ttu-id="d1e56-562">Geliştiricilerin *nx_snmp_agent_sha_key_create_extended ()* uygulamasına geçirilmesi önerilir.</span><span class="sxs-lookup"><span data-stu-id="d1e56-562">Developers are encouraged to migrate to *nx_snmp_agent_sha_key_create_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-563">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-563">Input Parameters</span></span>

- <span data-ttu-id="d1e56-564">**agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-564">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="d1e56-565">**parola** Parola dizesi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-565">**password** Pointer to password string.</span></span>
- <span data-ttu-id="d1e56-566">**destination_key** SNMP anahtar veri yapısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-566">**destination_key** Pointer to SNMP key data structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-567">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-567">Return Values</span></span>

- <span data-ttu-id="d1e56-568">**NX_SUCCESS** (0x00) başarılı anahtar oluştur.</span><span class="sxs-lookup"><span data-stu-id="d1e56-568">**NX_SUCCESS** (0x00) Successful key create.</span></span>
- <span data-ttu-id="d1e56-569">**NX_SNMP_ERROR** (0x100) anahtar oluşturma hatası.</span><span class="sxs-lookup"><span data-stu-id="d1e56-569">**NX_SNMP_ERROR** (0x100) Key create error.</span></span>
- <span data-ttu-id="d1e56-570">**NX_PTR_ERROR** (0x07) geçersiz SNMP Aracısı veya anahtar işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-570">**NX_PTR_ERROR** (0x07) Invalid SNMP Agent or key pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-571">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-571">Allowed From</span></span>

<span data-ttu-id="d1e56-572">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-572">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-573">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-573">Example</span></span>

```c
NX_SNMP_SECURITY_KEY my_key;

/* Create the SHA key for “my_agent.”   */
status =  nx_snmp_agent_sha_key_create(&my_agent, “authpw”, &my_key);


/* If status is NX_SUCCESS the key for the password “authpw” has been created.  */
```

## <a name="nx_snmp_agent_sha_key_create_extended"></a><span data-ttu-id="d1e56-574">nx_snmp_agent_sha_key_create_extended</span><span class="sxs-lookup"><span data-stu-id="d1e56-574">nx_snmp_agent_sha_key_create_extended</span></span>
<span data-ttu-id="d1e56-575">SHA anahtarı oluştur (yalnızca SNMP v3)</span><span class="sxs-lookup"><span data-stu-id="d1e56-575">Create SHA key (SNMP v3 only)</span></span>

### <a name="prototype"></a><span data-ttu-id="d1e56-576">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-576">Prototype</span></span>

```c
UINT nx_snmp_agent_sha_key_create_extended(NX_SNMP_AGENT *agent_ptr, 
                                           UCHAR *password, 
                                           UINT password_length,
                                           NX_SNMP_SECURITY_KEY  
                                           *destination_key);
```
### <a name="description"></a><span data-ttu-id="d1e56-577">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-577">Description</span></span>

<span data-ttu-id="d1e56-578">Bu hizmet, kimlik doğrulama ve şifreleme için kullanılabilen bir SHA anahtarı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d1e56-578">This service creates a SHA key that can be used for authentication and encryption.</span></span>

<span data-ttu-id="d1e56-579">Bu hizmet *nx_snmp_agent_sha_key_create ()* yerini alır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-579">This service replaces *nx_snmp_agent_sha_key_create().*</span></span> <span data-ttu-id="d1e56-580">Bu sürüm için çağıranın parola uzunluğu sağlaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d1e56-580">This version requires caller to supply password length.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-581">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-581">Input Parameters</span></span>

- <span data-ttu-id="d1e56-582">**agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-582">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="d1e56-583">**parola** Parola dizesi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-583">**password** Pointer to password string.</span></span>
- <span data-ttu-id="d1e56-584">**password_length** Parola dizesinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="d1e56-584">**password_length** Length of password string.</span></span>
- <span data-ttu-id="d1e56-585">**destination_key** SNMP anahtar veri yapısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-585">**destination_key** Pointer to SNMP key data structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-586">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-586">Return Values</span></span>

- <span data-ttu-id="d1e56-587">**NX_SUCCESS** (0x00) başarılı anahtar oluştur.</span><span class="sxs-lookup"><span data-stu-id="d1e56-587">**NX_SUCCESS** (0x00) Successful key create.</span></span>
- <span data-ttu-id="d1e56-588">**NX_SNMP_ERROR** (0x100) anahtar oluşturma hatası.</span><span class="sxs-lookup"><span data-stu-id="d1e56-588">**NX_SNMP_ERROR** (0x100) Key create error.</span></span>
- <span data-ttu-id="d1e56-589">**NX_SNMP_FAILED** (0x102) anahtar oluşturulamadı.</span><span class="sxs-lookup"><span data-stu-id="d1e56-589">**NX_SNMP_FAILED** (0x102) Key create failed.</span></span>
- <span data-ttu-id="d1e56-590">**NX_PTR_ERROR** (0x07) geçersiz SNMP Aracısı veya anahtar işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-590">**NX_PTR_ERROR** (0x07) Invalid SNMP Agent or key pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-591">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-591">Allowed From</span></span>

<span data-ttu-id="d1e56-592">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-592">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-593">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-593">Example</span></span>

```c
NX_SNMP_SECURITY_KEY my_key;

/* Create the SHA key for “my_agent.”   */
status =  nx_snmp_agent_sha_key_create_extended(&my_agent, “authpw”, 6, &my_key);


/* If status is NX_SUCCESS the key for the password “authpw” has been created.  */
```

## <a name="nx_snmp_agent_start"></a><span data-ttu-id="d1e56-594">nx_snmp_agent_start</span><span class="sxs-lookup"><span data-stu-id="d1e56-594">nx_snmp_agent_start</span></span>
<span data-ttu-id="d1e56-595">SNMP aracısını Başlat</span><span class="sxs-lookup"><span data-stu-id="d1e56-595">Start SNMP agent</span></span> 

### <a name="prototype"></a><span data-ttu-id="d1e56-596">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-596">Prototype</span></span>

```c
UINT nx_snmp_agent_start(NX_SNMP_AGENT *agent_ptr);
```
### <a name="description"></a><span data-ttu-id="d1e56-597">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-597">Description</span></span>

<span data-ttu-id="d1e56-598">Bu hizmet UDP yuvasını SNMP bağlantı noktası 161 ' e bağlar ve SNMP Aracısı iş parçacığı görevini başlatır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-598">This service binds the UDP socket to the SNMP port 161 and starts the SNMP Agent thread task.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-599">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-599">Input Parameters</span></span>

- <span data-ttu-id="d1e56-600">**agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-600">**agent_ptr** Pointer to SNMP Agent control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-601">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-601">Return Values</span></span>

- <span data-ttu-id="d1e56-602">**NX_SUCCESS** (0x00) SNMP aracısının başarıyla başlangıcı.</span><span class="sxs-lookup"><span data-stu-id="d1e56-602">**NX_SUCCESS** (0x00) Successful start of SNMP Agent.</span></span>
- <span data-ttu-id="d1e56-603">**NX_SNMP_ERROR** (0x100) SNMP Aracısı başlatma hatası.</span><span class="sxs-lookup"><span data-stu-id="d1e56-603">**NX_SNMP_ERROR** (0x100) SNMP Agent start error.</span></span>
- <span data-ttu-id="d1e56-604">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-604">**NX_PTR_ERROR** (0x07) Invalid input pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-605">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-605">Allowed From</span></span>

<span data-ttu-id="d1e56-606">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-606">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-607">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-607">Example</span></span>

```c
/* Start the previously created SNMP Agent “my_agent.”   */
status =  nx_snmp_agent_start(&my_agent);


/* If status is NX_SUCCESS the SNMP Agent “my_agent” has been started.  */
```
## <a name="nx_snmp_agent_stop"></a><span data-ttu-id="d1e56-608">nx_snmp_agent_stop</span><span class="sxs-lookup"><span data-stu-id="d1e56-608">nx_snmp_agent_stop</span></span>
<span data-ttu-id="d1e56-609">SNMP aracısını durdur</span><span class="sxs-lookup"><span data-stu-id="d1e56-609">Stop SNMP agent</span></span> 

### <a name="prototype"></a><span data-ttu-id="d1e56-610">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-610">Prototype</span></span>

```c
UINT nx_snmp_agent_stop(NX_SNMP_AGENT *agent_ptr);
```
### <a name="description"></a><span data-ttu-id="d1e56-611">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-611">Description</span></span>

<span data-ttu-id="d1e56-612">Bu hizmet SNMP Aracısı iş parçacığı görevini durduruyor ve UDP yuvasının SNMP bağlantı noktasına bağlantısını kaldırır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-612">This service stops the SNMP Agent thread task and unbinds the UDP socket to the SNMP port.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-613">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-613">Input Parameters</span></span>

- <span data-ttu-id="d1e56-614">**agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-614">**agent_ptr** Pointer to SNMP Agent control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-615">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-615">Return Values</span></span>

- <span data-ttu-id="d1e56-616">**NX_SUCCESS** (0x00) SNMP aracısının başarıyla durdurulması.</span><span class="sxs-lookup"><span data-stu-id="d1e56-616">**NX_SUCCESS** (0x00) Successful stop of SNMP Agent.</span></span>
- <span data-ttu-id="d1e56-617">**NX_PTR_ERROR** (0x07) geçersiz SNMP aracı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-617">**NX_PTR_ERROR** (0x07) Invalid SNMP Agent pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-618">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-618">Allowed From</span></span>

<span data-ttu-id="d1e56-619">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-619">Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-620">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-620">Example</span></span>

```c
/* Stop the previously created and started SNMP Agent “my_agent.”   */
status =  nx_snmp_agent_stop(&my_agent);


/* If status is NX_SUCCESS the SNMP Agent “my_agent” has been stopped.  */
```
## <a name="nx_snmp_agent_trap_send"></a><span data-ttu-id="d1e56-621">nx_snmp_agent_trap_send</span><span class="sxs-lookup"><span data-stu-id="d1e56-621">nx_snmp_agent_trap_send</span></span>
<span data-ttu-id="d1e56-622">SNMPv1 tuzağı gönder *(yalnızca IPv4)*</span><span class="sxs-lookup"><span data-stu-id="d1e56-622">Send SNMPv1 trap *(IPv4 only)*</span></span>

### <a name="prototype"></a><span data-ttu-id="d1e56-623">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-623">Prototype</span></span>

```c
UINT nx_snmp_agent_trap_send(NX_SNMP_AGENT *agent_ptr, 
                             ULONG ip_address, UCHAR *enterprise, 
                             UINT trap_type, UINT trap_code, 
                             ULONG elapsed_time, 
                             NX_SNMP_TRAP_OBJECT *object_list_ptr);
```

### <a name="description"></a><span data-ttu-id="d1e56-624">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-624">Description</span></span>

<span data-ttu-id="d1e56-625">Bu hizmet, belirtilen IPv4 adresinde SNMP Yöneticisi 'ne SNMP tuzağı gönderir.</span><span class="sxs-lookup"><span data-stu-id="d1e56-625">This service sends an SNMP trap to the SNMP Manager at the specified IPv4 address.</span></span> <span data-ttu-id="d1e56-626">NetX Duo 'da SNMP tuzağı göndermek için tercih edilen yöntem *nxd_snmp_agent_trap_send* hizmetini kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-626">The preferred method for sending an SNMP trap in NetX Duo is to use the *nxd_snmp_agent_trap_send* service.</span></span> <span data-ttu-id="d1e56-627">*nx_snmp_agent_trap_send* , mevcut NETX SNMP Aracısı uygulamalarını desteklemek üzere NETX Duo 'e dahildir.</span><span class="sxs-lookup"><span data-stu-id="d1e56-627">*nx_snmp_agent_trap_send* is included in NetX Duo to support existing NetX SNMP Agent applications.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-628">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-628">Input Parameters</span></span>

- <span data-ttu-id="d1e56-629">**agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-629">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="d1e56-630">**ip_address** SNMP yöneticisinin IPv4 adresi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-630">**ip_address** IPv4 address of the SNMP Manager.</span></span>
- <span data-ttu-id="d1e56-631">**Kurumsal** Kurumsal nesne KIMLIĞI dizesi (sysObectID).</span><span class="sxs-lookup"><span data-stu-id="d1e56-631">**enterprise** Enterprise object ID string (sysObectID).</span></span>
- <span data-ttu-id="d1e56-632">**trap_type** İstenen tuzak türü, aşağıdaki gibi:</span><span class="sxs-lookup"><span data-stu-id="d1e56-632">**trap_type** Type of trap requested, as follows:</span></span>  
   - <span data-ttu-id="d1e56-633">NX_SNMP_TRAP_COLDSTART (0)</span><span class="sxs-lookup"><span data-stu-id="d1e56-633">NX_SNMP_TRAP_COLDSTART (0)</span></span>  
   - <span data-ttu-id="d1e56-634">NX_SNMP_TRAP_WARMSTART (1)</span><span class="sxs-lookup"><span data-stu-id="d1e56-634">NX_SNMP_TRAP_WARMSTART (1)</span></span>  
   - <span data-ttu-id="d1e56-635">NX_SNMP_TRAP_LINKDOWN (2)</span><span class="sxs-lookup"><span data-stu-id="d1e56-635">NX_SNMP_TRAP_LINKDOWN (2)</span></span>  
   - <span data-ttu-id="d1e56-636">NX_SNMP_TRAP_LINKUP (3)</span><span class="sxs-lookup"><span data-stu-id="d1e56-636">NX_SNMP_TRAP_LINKUP (3)</span></span>  
   - <span data-ttu-id="d1e56-637">NX_SNMP_TRAP_AUTHENTICATE_FAILURE (4)</span><span class="sxs-lookup"><span data-stu-id="d1e56-637">NX_SNMP_TRAP_AUTHENTICATE_FAILURE (4)</span></span>  
   - <span data-ttu-id="d1e56-638">NX_SNMP_TRAP_EGPNEIGHBORLOSS (5)</span><span class="sxs-lookup"><span data-stu-id="d1e56-638">NX_SNMP_TRAP_EGPNEIGHBORLOSS (5)</span></span>  

- <span data-ttu-id="d1e56-639">**trap_code** Belirli tuzak kodu.</span><span class="sxs-lookup"><span data-stu-id="d1e56-639">**trap_code** Specific trap code.</span></span>
- <span data-ttu-id="d1e56-640">**Elapsed_Time** Zaman sistemi (sysUpTime).</span><span class="sxs-lookup"><span data-stu-id="d1e56-640">**elapsed_time** Time system has been up (sysUpTime).</span></span>
- <span data-ttu-id="d1e56-641">**object_list_ptr** SNMP tuzağı dahil edilecek nesne dizisi ve bunlarla ilişkili değerler.</span><span class="sxs-lookup"><span data-stu-id="d1e56-641">**object_list_ptr** Array of objects and their associated values to be included in the SNMP trap.</span></span> <span data-ttu-id="d1e56-642">Listenin sonlandırılması NX_NULL.</span><span class="sxs-lookup"><span data-stu-id="d1e56-642">The list is NX_NULL terminated.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-643">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-643">Return Values</span></span>

- <span data-ttu-id="d1e56-644">**NX_SUCCESS** (0x00) başarılı SNMP tuzak gönderme.</span><span class="sxs-lookup"><span data-stu-id="d1e56-644">**NX_SUCCESS** (0x00) Successful SNMP trap send.</span></span>
- <span data-ttu-id="d1e56-645">**NX_SNMP_ERROR** (0x100) SNMP tuzağı gönderme hatası.</span><span class="sxs-lookup"><span data-stu-id="d1e56-645">**NX_SNMP_ERROR** (0x100) Error sending SNMP trap.</span></span>
- <span data-ttu-id="d1e56-646">**NX_NOT_ENABLED** (0x14) SNMPv1 etkin değil.</span><span class="sxs-lookup"><span data-stu-id="d1e56-646">**NX_NOT_ENABLED** (0x14) SNMPv1 not enabled.</span></span>
- <span data-ttu-id="d1e56-647">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-647">**NX_PTR_ERROR** (0x07) Invalid input pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-648">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-648">Allowed From</span></span>

<span data-ttu-id="d1e56-649">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-649">Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-650">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-650">Example</span></span>

```c
NX_SNMP_TRAP_OBJECT trap_list[5];

ULONG dest_ip_address = IP_ADDRESS(1,2,3,4);

/* Build list of objects to supply in the trap.  */
trap_list[0].nx_snmp_object_string_ptr =  "1.3.6.1.2.1.2.2.1.1.0";
trap_list[0].nx_snmp_object_data.nx_snmp_object_data_type =  NX_SNMP_INTEGER;
trap_list[0].nx_snmp_object_data.nx_snmp_object_data_msw =   counter;
trap_list[1].nx_snmp_object_string_ptr =  "1.3.6.1.2.1.1.3.0";
trap_list[1].nx_snmp_object_data.nx_snmp_object_data_type =  NX_SNMP_TIME_TICS;
trap_list[1].nx_snmp_object_data.nx_snmp_object_data_msw =   tx_time_get();
trap_list[2].nx_snmp_object_string_ptr =  NX_NULL; /* Terminate list!  */

/* Send trap to SNMP manager at 193.2.2.61.  */
status =  nx_snmp_agent_trap_send(&my_agent,dest_ip_address,
                                   "1.3.6.7.7.7", NX_SNMP_TRAP_LINKUP, counter++, 
                                  tx_time_get(), trap_list);

/* If status is NX_SUCCESS the SNMP trap has been sent.  */
```
## <a name="nxd_snmp_agent_trap_send"></a><span data-ttu-id="d1e56-651">nxd_snmp_agent_trap_send</span><span class="sxs-lookup"><span data-stu-id="d1e56-651">nxd_snmp_agent_trap_send</span></span>
<span data-ttu-id="d1e56-652">SNMPv1 tuzağı gönderme *(IPv4 ve IPv6)*</span><span class="sxs-lookup"><span data-stu-id="d1e56-652">Send SNMPv1 trap *(IPv4 and IPv6)*</span></span>

### <a name="prototype"></a><span data-ttu-id="d1e56-653">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-653">Prototype</span></span>

```c
UINT nxd_snmp_agent_trap_send(NX_SNMP_AGENT *agent_ptr, 
            ULONG ip_address, UCHAR *enterprise, UINT trap_type, 
            UINT trap_code, ULONG elapsed_time, 
            NX_SNMP_TRAP_OBJECT *object_list_ptr);
```
### <a name="description"></a><span data-ttu-id="d1e56-654">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-654">Description</span></span>

<span data-ttu-id="d1e56-655">Bu hizmet, belirtilen IP adresindeki SNMP Yöneticisi 'ne SNMP tuzağı gönderir.</span><span class="sxs-lookup"><span data-stu-id="d1e56-655">This service sends an SNMP trap to the SNMP Manager at the specified IP address.</span></span> <span data-ttu-id="d1e56-656">NetX 'te SNMP tuzağı göndermek için eşdeğer Yöntem *nxd_snmp_agent_trap_send* hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="d1e56-656">The equivalent method for sending an SNMP trap in NetX is the *nxd_snmp_agent_trap_send* service.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-657">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-657">Input Parameters</span></span>

- <span data-ttu-id="d1e56-658">**agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-658">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="d1e56-659">**ip_address** SNMP yöneticisinin IPv4 veya IPv6 adresi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-659">**ip_address** IPv4 or IPv6 address of the SNMP Manager.</span></span>
- <span data-ttu-id="d1e56-660">**Kurumsal** Kurumsal nesne KIMLIĞI dizesi (sysObectID).</span><span class="sxs-lookup"><span data-stu-id="d1e56-660">**enterprise** Enterprise object ID string (sysObectID).</span></span>
- <span data-ttu-id="d1e56-661">**trap_type** İstenen tuzak türü, aşağıdaki gibi:</span><span class="sxs-lookup"><span data-stu-id="d1e56-661">**trap_type** Type of trap requested, as follows:</span></span>  
   - <span data-ttu-id="d1e56-662">NX_SNMP_TRAP_COLDSTART (0)</span><span class="sxs-lookup"><span data-stu-id="d1e56-662">NX_SNMP_TRAP_COLDSTART (0)</span></span>
   - <span data-ttu-id="d1e56-663">NX_SNMP_TRAP_WARMSTART (1)</span><span class="sxs-lookup"><span data-stu-id="d1e56-663">NX_SNMP_TRAP_WARMSTART (1)</span></span>
   - <span data-ttu-id="d1e56-664">NX_SNMP_TRAP_LINKDOWN (2)</span><span class="sxs-lookup"><span data-stu-id="d1e56-664">NX_SNMP_TRAP_LINKDOWN (2)</span></span>
   - <span data-ttu-id="d1e56-665">NX_SNMP_TRAP_LINKUP (3)</span><span class="sxs-lookup"><span data-stu-id="d1e56-665">NX_SNMP_TRAP_LINKUP (3)</span></span>
   - <span data-ttu-id="d1e56-666">NX_SNMP_TRAP_AUTHENTICATE_FAILURE (4)</span><span class="sxs-lookup"><span data-stu-id="d1e56-666">NX_SNMP_TRAP_AUTHENTICATE_FAILURE (4)</span></span>
   - <span data-ttu-id="d1e56-667">NX_SNMP_TRAP_EGPNEIGHBORLOSS (5)</span><span class="sxs-lookup"><span data-stu-id="d1e56-667">NX_SNMP_TRAP_EGPNEIGHBORLOSS (5)</span></span>

- <span data-ttu-id="d1e56-668">**trap_code** Belirli tuzak kodu.</span><span class="sxs-lookup"><span data-stu-id="d1e56-668">**trap_code** Specific trap code.</span></span>
- <span data-ttu-id="d1e56-669">**Elapsed_Time** Zaman sistemi (sysUpTime).</span><span class="sxs-lookup"><span data-stu-id="d1e56-669">**elapsed_time** Time system has been up (sysUpTime).</span></span>
- <span data-ttu-id="d1e56-670">**object_list_ptr** SNMP tuzağı dahil edilecek nesne dizisi ve bunlarla ilişkili değerler.</span><span class="sxs-lookup"><span data-stu-id="d1e56-670">**object_list_ptr** Array of objects and their associated values to be included in the SNMP trap.</span></span> <span data-ttu-id="d1e56-671">Listenin sonlandırılması NX_NULL.</span><span class="sxs-lookup"><span data-stu-id="d1e56-671">The list is NX_NULL terminated.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-672">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-672">Return Values</span></span>

- <span data-ttu-id="d1e56-673">**NX_SUCCESS** (0x00) başarılı SNMP tuzak gönderme.</span><span class="sxs-lookup"><span data-stu-id="d1e56-673">**NX_SUCCESS** (0x00) Successful SNMP trap send.</span></span>
- <span data-ttu-id="d1e56-674">**NX_SNMP_ERROR** (0x100) SNMP tuzağı gönderme hatası.</span><span class="sxs-lookup"><span data-stu-id="d1e56-674">**NX_SNMP_ERROR** (0x100) Error sending SNMP trap.</span></span>
- <span data-ttu-id="d1e56-675">**NX_NOT_ENABLED** (0x14) SNMPv1 etkin değil.</span><span class="sxs-lookup"><span data-stu-id="d1e56-675">**NX_NOT_ENABLED** (0x14) SNMPv1 not enabled.</span></span>
- <span data-ttu-id="d1e56-676">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-676">**NX_PTR_ERROR** (0x07) Invalid input pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-677">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-677">Allowed From</span></span>

<span data-ttu-id="d1e56-678">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-678">Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-679">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-679">Example</span></span>

```c
NX_SNMP_TRAP_OBJECT trap_list[5];

NXD_ADDRESS dest_ip_address;

    dest_ip_address.nxd_ip_version = NX_IP_VERSION_V6 ;
    dest_ip_address.nxd_ip_address.v6[0] = 0x20010db8;
    dest_ip_address.nxd_ip_address.v6[1] = 0xf101;
    dest_ip_address.nxd_ip_address.v6[2] = 0x00000000;
    dest_ip_address.nxd_ip_address.v6[3] = 0x00000101;

/* Build list of objects to supply in the trap.  */
trap_list[0].nx_snmp_object_string_ptr =  "1.3.6.1.2.1.2.2.1.1.0";
trap_list[0].nx_snmp_object_data.nx_snmp_object_data_type =  NX_SNMP_INTEGER;
trap_list[0].nx_snmp_object_data.nx_snmp_object_data_msw =   counter;
trap_list[1].nx_snmp_object_string_ptr =  "1.3.6.1.2.1.1.3.0";
trap_list[1].nx_snmp_object_data.nx_snmp_object_data_type =  NX_SNMP_TIME_TICS;
trap_list[1].nx_snmp_object_data.nx_snmp_object_data_msw =   tx_time_get();
trap_list[2].nx_snmp_object_string_ptr =  NX_NULL; /* Terminate list!  */

/* Send trap to SNMP manager at 193.2.2.61.  */
status =  nxd_snmp_agent_trap_send(&my_agent,&dest_ip_address,
                 "1.3.6.7.7.7", NX_SNMP_TRAP_LINKUP, counter++, tx_time_get(), 
               trap_list);

/* If status is NX_SUCCESS the SNMP trap has been sent.  */
```

## <a name="nx_snmp_agent_trapv2_send"></a><span data-ttu-id="d1e56-680">nx_snmp_agent_trapv2_send</span><span class="sxs-lookup"><span data-stu-id="d1e56-680">nx_snmp_agent_trapv2_send</span></span>
<span data-ttu-id="d1e56-681">SNMPv2 tuzak gönderme (yalnızca IPv4)</span><span class="sxs-lookup"><span data-stu-id="d1e56-681">Send SNMPv2 trap (IPv4 only)</span></span>

### <a name="prototype"></a><span data-ttu-id="d1e56-682">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-682">Prototype</span></span>

```c
UINT nx_snmp_agent_trapv2_send(NX_SNMP_AGENT *agent_ptr, 
            NXD_ADDRESS *ip_address, UCHAR *community, UINT trap_type, 
            ULONG elapsed_time, NX_SNMP_TRAP_OBJECT *object_list_ptr);
```
### <a name="description"></a><span data-ttu-id="d1e56-683">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-683">Description</span></span>

<span data-ttu-id="d1e56-684">Bu hizmet, belirtilen IPv4 adresindeki SNMP Yöneticisi 'ne bir SNMPv2 tuzak gönderir.</span><span class="sxs-lookup"><span data-stu-id="d1e56-684">This service sends an SNMPv2 trap to the SNMP Manager at the specified IPv4 address.</span></span> <span data-ttu-id="d1e56-685">NetX Duo 'da SNMP tuzağı göndermek için tercih edilen yöntem *nxd_snmp_agent_trapv2_send* hizmetini kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-685">The preferred method for sending an SNMP trap in NetX Duo is to use the *nxd_snmp_agent_trapv2_send* service.</span></span> <span data-ttu-id="d1e56-686">*nx_snmp_agent_trapv2_send* , mevcut NETX SNMP Aracısı uygulamalarını desteklemek üzere NETX Duo 'e dahildir.</span><span class="sxs-lookup"><span data-stu-id="d1e56-686">*nx_snmp_agent_trapv2_send* is included in NetX Duo to support existing NetX SNMP Agent applications.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-687">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-687">Input Parameters</span></span>

- <span data-ttu-id="d1e56-688">**agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-688">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="d1e56-689">**ip_address** SNMP yöneticisinin IPv4 adresi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-689">**ip_address** IPv4 address of the SNMP Manager.</span></span>
- <span data-ttu-id="d1e56-690">**topluluk** Topluluk adı (Kullanıcı adı).</span><span class="sxs-lookup"><span data-stu-id="d1e56-690">**community** Community name (username).</span></span>
- <span data-ttu-id="d1e56-691">**trap_type**</span><span class="sxs-lookup"><span data-stu-id="d1e56-691">**trap_type**</span></span>  
   <span data-ttu-id="d1e56-692">İstenen tuzak türü.</span><span class="sxs-lookup"><span data-stu-id="d1e56-692">Type of trap requested.</span></span> <span data-ttu-id="d1e56-693">Standart olaylar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="d1e56-693">The standard events are:</span></span>  
   - <span data-ttu-id="d1e56-694">NX_SNMP_TRAP_COLDSTART (0)</span><span class="sxs-lookup"><span data-stu-id="d1e56-694">NX_SNMP_TRAP_COLDSTART (0)</span></span>
   - <span data-ttu-id="d1e56-695">NX_SNMP_TRAP_WARMSTART (1)</span><span class="sxs-lookup"><span data-stu-id="d1e56-695">NX_SNMP_TRAP_WARMSTART (1)</span></span>
   - <span data-ttu-id="d1e56-696">NX_SNMP_TRAP_LINKDOWN (2)</span><span class="sxs-lookup"><span data-stu-id="d1e56-696">NX_SNMP_TRAP_LINKDOWN (2)</span></span>
   - <span data-ttu-id="d1e56-697">NX_SNMP_TRAP_LINKUP (3)</span><span class="sxs-lookup"><span data-stu-id="d1e56-697">NX_SNMP_TRAP_LINKUP (3)</span></span>
   - <span data-ttu-id="d1e56-698">NX_SNMP_TRAP_AUTHENTICATE_FAILURE (4)</span><span class="sxs-lookup"><span data-stu-id="d1e56-698">NX_SNMP_TRAP_AUTHENTICATE_FAILURE (4)</span></span>
   - <span data-ttu-id="d1e56-699">NX_SNMP_TRAP_EGPNEIGHBORLOSS (5)</span><span class="sxs-lookup"><span data-stu-id="d1e56-699">NX_SNMP_TRAP_EGPNEIGHBORLOSS (5)</span></span>

   <span data-ttu-id="d1e56-700">Özel veriler için:</span><span class="sxs-lookup"><span data-stu-id="d1e56-700">For proprietary data:</span></span>  
   - <span data-ttu-id="d1e56-701">NX_SNMP_TRAP_CUSTOM (0xFFFFFFFF) ( *nxd_snmp. h* içinde tanımlanmıştır)</span><span class="sxs-lookup"><span data-stu-id="d1e56-701">NX_SNMP_TRAP_CUSTOM (0xFFFFFFFF) (defined in *nxd_snmp.h*)</span></span>
   
- <span data-ttu-id="d1e56-702">**Elapsed_Time** Zaman sistemi (sysUpTime).</span><span class="sxs-lookup"><span data-stu-id="d1e56-702">**elapsed_time** Time system has been up (sysUpTime).</span></span>
- <span data-ttu-id="d1e56-703">**object_list_ptr** SNMP tuzağı dahil edilecek nesne dizisi ve bunlarla ilişkili değerler.</span><span class="sxs-lookup"><span data-stu-id="d1e56-703">**object_list_ptr** Array of objects and their associated values to be included in the SNMP trap.</span></span> <span data-ttu-id="d1e56-704">Listenin sonlandırılması NX_NULL.</span><span class="sxs-lookup"><span data-stu-id="d1e56-704">The list is NX_NULL terminated.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-705">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-705">Return Values</span></span>

- <span data-ttu-id="d1e56-706">**NX_SUCCESS** (0x00) başarılı SNMP tuzak gönderme.</span><span class="sxs-lookup"><span data-stu-id="d1e56-706">**NX_SUCCESS** (0x00) Successful SNMP trap send.</span></span>
- <span data-ttu-id="d1e56-707">**NX_SNMP_ERROR** (0x100) SNMP tuzağı gönderme hatası.</span><span class="sxs-lookup"><span data-stu-id="d1e56-707">**NX_SNMP_ERROR** (0x100) Error sending SNMP trap.</span></span>
- <span data-ttu-id="d1e56-708">**NX_NOT_ENABLED** (0x14) SNMPv2 etkin değil.</span><span class="sxs-lookup"><span data-stu-id="d1e56-708">**NX_NOT_ENABLED** (0x14) SNMPv2 not enabled.</span></span>
- <span data-ttu-id="d1e56-709">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-709">**NX_PTR_ERROR** (0x07) Invalid input pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-710">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-710">Allowed From</span></span>

<span data-ttu-id="d1e56-711">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-711">Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-712">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-712">Example</span></span>

```c
NX_SNMP_TRAP_OBJECT trap_list[5];
ULONG  dest_ip_address = IP_ADDRESS(1,2,3,4);

/* Build an empty object list, since it is not needed for the 
   NX_SNMP_TRAP_COLDSTART trap.  */
trap_list[0].nx_snmp_object_string_ptr =  NX_NULL;

/* Send trap to SNMP manager at 193.2.2.61.  */
Status =  nx_snmp_agent_trapv2_send(&my_agent,dest_ip_address, "public",
               NX_SNMP_TRAP_COLDSTART, tx_time_get(), trap_list);

/* If status is NX_SUCCESS the SNMP trap has been sent.  */
```

## <a name="nx_snmp_agent_trapv2_oid_send"></a><span data-ttu-id="d1e56-713">nx_snmp_agent_trapv2_oid_send</span><span class="sxs-lookup"><span data-stu-id="d1e56-713">nx_snmp_agent_trapv2_oid_send</span></span>
<span data-ttu-id="d1e56-714">Doğrudan OID 'yi belirten SNMPv2 tuzağı gönder</span><span class="sxs-lookup"><span data-stu-id="d1e56-714">Send SNMPv2 trap specifying OID directly</span></span> 

### <a name="prototype"></a><span data-ttu-id="d1e56-715">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-715">Prototype</span></span>

```c
UINT nx_snmp_agent_trapv2_oid_send(NX_SNMP_AGENT *agent_ptr, 
                                   ULONG ip_address, UCHAR *community,        
                                   UCHAR *oid, ULONG elapsed_time,   
                                   NX_SNMP_TRAP_OBJECT 
                                            *object_list_ptr);
```
### <a name="description"></a><span data-ttu-id="d1e56-716">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-716">Description</span></span>

<span data-ttu-id="d1e56-717">Bu hizmet, belirtilen IP adresindeki (yalnızca IPv4) SNMP Yöneticisi 'ne bir SNMPv2 tuzak gönderir ve çağıranın OID 'yi doğrudan belirlemesine izin verir.</span><span class="sxs-lookup"><span data-stu-id="d1e56-717">This service sends an SNMPv2 trap to the SNMP Manager at the specified IP address (IPv4 only) and allows the caller to specify the OID directly.</span></span> <span data-ttu-id="d1e56-718">NetX Duo 'da belirtilen OID ile SNMP tuzağı göndermek için tercih edilen yöntem *nxd_snmp_agent_trapv2_oid_send* hizmetini kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-718">The preferred method for sending an SNMP trap with specified OID in NetX Duo is to use the *nxd_snmp_agent_trapv2_oid_send* service.</span></span> <span data-ttu-id="d1e56-719">Mevcut NetX SNMP Aracısı uygulamalarını desteklemek için, NetX Duo 'e *nx_snmp_agent_trapv2_oid_ Send* işlemi dahildir.</span><span class="sxs-lookup"><span data-stu-id="d1e56-719">*nx_snmp_agent_trapv2_oid_ send* is included in NetX Duo to support existing NetX SNMP Agent applications.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-720">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-720">Input Parameters</span></span>

- <span data-ttu-id="d1e56-721">**agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-721">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="d1e56-722">**ip_address** SNMP yöneticisinin IP adresi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-722">**ip_address** IP address of SNMP Manager.</span></span>
- <span data-ttu-id="d1e56-723">**topluluk** Topluluk adı (Kullanıcı adı).</span><span class="sxs-lookup"><span data-stu-id="d1e56-723">**community** Community name (username).</span></span>
- <span data-ttu-id="d1e56-724">**OID** OID içeren arabelleğin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-724">**oid** Pointer to buffer containing OID.</span></span>
- <span data-ttu-id="d1e56-725">**Elapsed_Time** Zaman sistemi (sysUpTime).</span><span class="sxs-lookup"><span data-stu-id="d1e56-725">**elapsed_time** Time system has been up (sysUpTime).</span></span>
- <span data-ttu-id="d1e56-726">**object_list_ptr** SNMP tuzağı dahil edilecek nesne dizisi ve bunlarla ilişkili değerler.</span><span class="sxs-lookup"><span data-stu-id="d1e56-726">**object_list_ptr** Array of objects and their associated values to be included in the SNMP trap.</span></span> <span data-ttu-id="d1e56-727">Listenin sonlandırılması NX_NULL.</span><span class="sxs-lookup"><span data-stu-id="d1e56-727">The list is NX_NULL terminated.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-728">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-728">Return Values</span></span>

- <span data-ttu-id="d1e56-729">**NX_SUCCESS** (0x00) başarılı SNMP tuzak gönderme.</span><span class="sxs-lookup"><span data-stu-id="d1e56-729">**NX_SUCCESS** (0x00) Successful SNMP trap send.</span></span>
- <span data-ttu-id="d1e56-730">**NX_SNMP_ERROR** (0x100) SNMP tuzağı gönderme hatası.</span><span class="sxs-lookup"><span data-stu-id="d1e56-730">**NX_SNMP_ERROR** (0x100) Error sending SNMP trap.</span></span>
- <span data-ttu-id="d1e56-731">**NX_PTR_ERROR** (0x16) geçersiz SNMP Aracısı veya parametre işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-731">**NX_PTR_ERROR** (0x16) Invalid SNMP Agent or parameter pointer.</span></span>
- <span data-ttu-id="d1e56-732">**NX_IP_ADDRESS_ERROR** (0x21) GEÇERSIZ hedef IP adresi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-732">**NX_IP_ADDRESS_ERROR** (0x21) Invalid destination IP address.</span></span>
- <span data-ttu-id="d1e56-733">**NX_OPTION_ERROR** (0X0a) geçersiz parametre.</span><span class="sxs-lookup"><span data-stu-id="d1e56-733">**NX_OPTION_ERROR** (0x0a) Invalid parameter.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-734">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-734">Allowed From</span></span>

<span data-ttu-id="d1e56-735">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-735">Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-736">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-736">Example</span></span>

```c
NX_SNMP_TRAP_OBJECT trap_list[5];

/* Build an empty object list */
trap_list[0].nx_snmp_object_string_ptr =  NX_NULL;

/* Send trap to SNMP manager at 193.2.2.61.  */
Status =  nx_snmp_agent_trapv2_oid_send(&my_agent, IP_ADDRESS(193,2,2,61), 
                                       "public", (UCHAR *)"0.9.9.9.9.9.9.9.9.9",  
                                       tx_time_get(), trap_list);

/* If status is NX_SUCCESS the SNMP trap has been sent.  */
```

## <a name="nxd_snmp_agent_trapv2_send"></a><span data-ttu-id="d1e56-737">nxd_snmp_agent_trapv2_send</span><span class="sxs-lookup"><span data-stu-id="d1e56-737">nxd_snmp_agent_trapv2_send</span></span>
<span data-ttu-id="d1e56-738">SNMPv2 tuzağı gönderme (IPv4 ve IPv6)</span><span class="sxs-lookup"><span data-stu-id="d1e56-738">Send SNMPv2 trap (IPv4 and IPv6)</span></span>

### <a name="prototype"></a><span data-ttu-id="d1e56-739">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-739">Prototype</span></span>

```c
UINT nxd_snmp_agent_trapv2_send(NX_SNMP_AGENT *agent_ptr, 
                                NXD_ADDRESS *ip_address, 
                                UCHAR *community, UINT trap_type, 
                                ULONG elapsed_time, 
                                NX_SNMP_TRAP_OBJECT *object_list_ptr);
```
### <a name="description"></a><span data-ttu-id="d1e56-740">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-740">Description</span></span>

<span data-ttu-id="d1e56-741">Bu hizmet, belirtilen IP adresindeki SNMP Yöneticisi 'ne bir SNMP v2 tuzağı gönderir.</span><span class="sxs-lookup"><span data-stu-id="d1e56-741">This service sends an SNMP V2 trap to the SNMP Manager at the specified IP address.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-742">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-742">Input Parameters</span></span>

- <span data-ttu-id="d1e56-743">**agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-743">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="d1e56-744">**ip_address** SNMP yöneticisinin IP (IPv4 veya IPv6) adresi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-744">**ip_address** IP (IPv4 or IPv6) address of the SNMP Manager.</span></span>
- <span data-ttu-id="d1e56-745">**topluluk** Topluluk adı (Kullanıcı adı).</span><span class="sxs-lookup"><span data-stu-id="d1e56-745">**community** Community name (username).</span></span>
- <span data-ttu-id="d1e56-746">**trap_type**</span><span class="sxs-lookup"><span data-stu-id="d1e56-746">**trap_type**</span></span>  
   <span data-ttu-id="d1e56-747">İstenen tuzak türü.</span><span class="sxs-lookup"><span data-stu-id="d1e56-747">Type of trap requested.</span></span> <span data-ttu-id="d1e56-748">Standart olaylar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="d1e56-748">The standard events are:</span></span>  
   - <span data-ttu-id="d1e56-749">NX_SNMP_TRAP_COLDSTART (0)</span><span class="sxs-lookup"><span data-stu-id="d1e56-749">NX_SNMP_TRAP_COLDSTART (0)</span></span>
   - <span data-ttu-id="d1e56-750">NX_SNMP_TRAP_WARMSTART (1)</span><span class="sxs-lookup"><span data-stu-id="d1e56-750">NX_SNMP_TRAP_WARMSTART (1)</span></span>
   - <span data-ttu-id="d1e56-751">NX_SNMP_TRAP_LINKDOWN (2)</span><span class="sxs-lookup"><span data-stu-id="d1e56-751">NX_SNMP_TRAP_LINKDOWN (2)</span></span>
   - <span data-ttu-id="d1e56-752">NX_SNMP_TRAP_LINKUP (3)</span><span class="sxs-lookup"><span data-stu-id="d1e56-752">NX_SNMP_TRAP_LINKUP (3)</span></span>
   - <span data-ttu-id="d1e56-753">NX_SNMP_TRAP_AUTHENTICATE_FAILURE (4)</span><span class="sxs-lookup"><span data-stu-id="d1e56-753">NX_SNMP_TRAP_AUTHENTICATE_FAILURE (4)</span></span>
   - <span data-ttu-id="d1e56-754">NX_SNMP_TRAP_EGPNEIGHBORLOSS (5)</span><span class="sxs-lookup"><span data-stu-id="d1e56-754">NX_SNMP_TRAP_EGPNEIGHBORLOSS (5)</span></span>

   <span data-ttu-id="d1e56-755">Özel veriler için:</span><span class="sxs-lookup"><span data-stu-id="d1e56-755">For proprietary data:</span></span>

   - <span data-ttu-id="d1e56-756">NX_SNMP_TRAP_CUSTOM (0xFFFFFFFF) ( *nxd_snmp. h* içinde tanımlanmıştır)</span><span class="sxs-lookup"><span data-stu-id="d1e56-756">NX_SNMP_TRAP_CUSTOM (0xFFFFFFFF) (defined in *nxd_snmp.h*)</span></span>

- <span data-ttu-id="d1e56-757">**Elapsed_Time** Zaman sistemi (sysUpTime).</span><span class="sxs-lookup"><span data-stu-id="d1e56-757">**elapsed_time** Time system has been up (sysUpTime).</span></span>
- <span data-ttu-id="d1e56-758">**object_list_ptr** SNMP tuzağı dahil edilecek nesne dizisi ve bunlarla ilişkili değerler.</span><span class="sxs-lookup"><span data-stu-id="d1e56-758">**object_list_ptr** Array of objects and their associated values to be included in the SNMP trap.</span></span> <span data-ttu-id="d1e56-759">Listenin sonlandırılması NX_NULL.</span><span class="sxs-lookup"><span data-stu-id="d1e56-759">The list is NX_NULL terminated.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-760">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-760">Return Values</span></span>

- <span data-ttu-id="d1e56-761">**NX_SUCCESS** (0x00) başarılı SNMP tuzak gönderme.</span><span class="sxs-lookup"><span data-stu-id="d1e56-761">**NX_SUCCESS** (0x00) Successful SNMP trap send.</span></span>
- <span data-ttu-id="d1e56-762">**NX_SNMP_ERROR** (0x100) SNMP tuzağı gönderme hatası.</span><span class="sxs-lookup"><span data-stu-id="d1e56-762">**NX_SNMP_ERROR** (0x100) Error sending SNMP trap.</span></span>
- <span data-ttu-id="d1e56-763">**NX_NOT_ENABLED** (0x14) SNMPv2 etkin değil.</span><span class="sxs-lookup"><span data-stu-id="d1e56-763">**NX_NOT_ENABLED** (0x14) SNMPv2 not enabled.</span></span>
- <span data-ttu-id="d1e56-764">**NX_SNMP_INVALID_IP_PROTOCOL_ERROR** (0x104) desteklenmeyen IP sürümü</span><span class="sxs-lookup"><span data-stu-id="d1e56-764">**NX_SNMP_INVALID_IP_PROTOCOL_ERROR** (0x104) Unsupported IP version</span></span>
- <span data-ttu-id="d1e56-765">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-765">**NX_PTR_ERROR** (0x07) Invalid input pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-766">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-766">Allowed From</span></span>

<span data-ttu-id="d1e56-767">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-767">Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-768">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-768">Example</span></span>

```c
NX_SNMP_TRAP_OBJECT trap_list[5];
NXD_ADDRESS dest_ip_address;

    dest_ip_address.nxd_ip_version = NX_IP_VERSION_V6 ;
    dest_ip_address.nxd_ip_address.v6[0] = 0x20010db8;
    dest_ip_address.nxd_ip_address.v6[1] = 0xf101;
    dest_ip_address.nxd_ip_address.v6[2] = 0x00000000;
    dest_ip_address.nxd_ip_address.v6[3] = 0x00000101;

/* Build an empty object list, since it is not needed for the 
   NX_SNMP_TRAP_COLDSTART trap.  */
trap_list[0].nx_snmp_object_string_ptr =  NX_NULL;

/* Send a standard event trap to SNMP manager at 193.2.2.61.  */
Status =  nxd_snmp_agent_trapv2_send(&my_agent,&dest_ip_address, "public",
                                    NX_SNMP_TRAP_COLDSTART, tx_time_get(),  
                                    trap_list);

/* If status is NX_SUCCESS the SNMP trap has been sent.  */
```

## <a name="nxd_snmp_agent_trapv2_oid_send"></a><span data-ttu-id="d1e56-769">nxd_snmp_agent_trapv2_oid_send</span><span class="sxs-lookup"><span data-stu-id="d1e56-769">nxd_snmp_agent_trapv2_oid_send</span></span>
<span data-ttu-id="d1e56-770">Doğrudan OID 'yi belirten SNMPv2 tuzağı gönder</span><span class="sxs-lookup"><span data-stu-id="d1e56-770">Send SNMPv2 trap specifying OID directly</span></span> 

### <a name="prototype"></a><span data-ttu-id="d1e56-771">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-771">Prototype</span></span>

```c
UINT nxd_snmp_agent_trapv2_oid_send(NX_SNMP_AGENT *agent_ptr, 
                                    NXD_ADDRESS *ip_address, 
                                    UCHAR *community,        
                                    UCHAR *oid, ULONG elapsed_time,   
                                    NX_SNMP_TRAP_OBJECT 
                                    *object_list_ptr);
```
### <a name="description"></a><span data-ttu-id="d1e56-772">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-772">Description</span></span>

<span data-ttu-id="d1e56-773">Bu hizmet, belirtilen IP adresindeki (IPv4/IPv6) SNMP Yöneticisi 'ne SNMP v2 tuzağı gönderir ve çağıranın OID 'yi doğrudan belirlemesine izin verir.</span><span class="sxs-lookup"><span data-stu-id="d1e56-773">This service sends an SNMP v2 trap to the SNMP Manager at the specified IP address (IPv4/IPv6) and allows the caller to specify the OID directly.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-774">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-774">Input Parameters</span></span>

- <span data-ttu-id="d1e56-775">**agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-775">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="d1e56-776">**ip_address** SNMP yöneticisinin IP adresi (IPv4/IPv6).</span><span class="sxs-lookup"><span data-stu-id="d1e56-776">**ip_address** IP address of SNMP Manager (IPv4/IPv6).</span></span>
- <span data-ttu-id="d1e56-777">**topluluk** Topluluk adı (Kullanıcı adı).</span><span class="sxs-lookup"><span data-stu-id="d1e56-777">**community** Community name (username).</span></span>
- <span data-ttu-id="d1e56-778">**OID** OID içeren arabelleğin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-778">**oid** Pointer to buffer containing OID.</span></span>
- <span data-ttu-id="d1e56-779">**Elapsed_Time** Zaman sistemi (sysUpTime).</span><span class="sxs-lookup"><span data-stu-id="d1e56-779">**elapsed_time** Time system has been up (sysUpTime).</span></span>
- <span data-ttu-id="d1e56-780">**object_list_ptr** SNMP tuzağı dahil edilecek nesne dizisi ve bunlarla ilişkili değerler.</span><span class="sxs-lookup"><span data-stu-id="d1e56-780">**object_list_ptr** Array of objects and their associated values to be included in the SNMP trap.</span></span> <span data-ttu-id="d1e56-781">Listenin sonlandırılması NX_NULL.</span><span class="sxs-lookup"><span data-stu-id="d1e56-781">The list is NX_NULL terminated.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-782">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-782">Return Values</span></span>

- <span data-ttu-id="d1e56-783">**NX_SUCCESS** (0x00) başarılı SNMP tuzak gönderme.</span><span class="sxs-lookup"><span data-stu-id="d1e56-783">**NX_SUCCESS** (0x00) Successful SNMP trap send.</span></span>
- <span data-ttu-id="d1e56-784">**NX_SNMP_ERROR** (0x100) SNMP tuzağı gönderme hatası.</span><span class="sxs-lookup"><span data-stu-id="d1e56-784">**NX_SNMP_ERROR** (0x100) Error sending SNMP trap.</span></span>
- <span data-ttu-id="d1e56-785">**NX_PTR_ERROR** (0x16) geçersiz SNMP Aracısı veya parametre işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-785">**NX_PTR_ERROR** (0x16) Invalid SNMP Agent or parameter pointer.</span></span>
- <span data-ttu-id="d1e56-786">**NX_IP_ADDRESS_ERROR** (0x21) GEÇERSIZ hedef IP adresi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-786">**NX_IP_ADDRESS_ERROR** (0x21) Invalid destination IP address.</span></span>
- <span data-ttu-id="d1e56-787">**NX_OPTION_ERROR** (0X0a) geçersiz parametre.</span><span class="sxs-lookup"><span data-stu-id="d1e56-787">**NX_OPTION_ERROR** (0x0a) Invalid parameter.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-788">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-788">Allowed From</span></span>

<span data-ttu-id="d1e56-789">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-789">Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-790">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-790">Example</span></span>

```c
NX_SNMP_TRAP_OBJECT trap_list[5];
NXD_ADDRESS         address;


/* Build an empty object list */
trap_list[0].nx_snmp_object_string_ptr =  NX_NULL;

address.nxd_ip_version = NX_IP_VERSION_V4;
address.nxd_ip_address.v4 = IP_ADDRESS(193,2,2,61)

/* Send trap to SNMP manager at 193.2.2.61.  */
Status =  nxd_snmp_agent_trapv2_oid_send(&my_agent, &address, 
                                       "public", (UCHAR *)"0.9.9.9.9.9.9.9.9.9",  
                                       tx_time_get(), trap_list);

/* If status is NX_SUCCESS the SNMP trap has been sent.  */
```
## <a name="nx_snmp_agent_trapv3_send"></a><span data-ttu-id="d1e56-791">nx_snmp_agent_trapv3_send</span><span class="sxs-lookup"><span data-stu-id="d1e56-791">nx_snmp_agent_trapv3_send</span></span>
<span data-ttu-id="d1e56-792">SNMPv3 tuzağı gönder (yalnızca IPv4)</span><span class="sxs-lookup"><span data-stu-id="d1e56-792">Send SNMPv3 trap (IPv4 only)</span></span>

### <a name="prototype"></a><span data-ttu-id="d1e56-793">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-793">Prototype</span></span>

```c
UINT nx_snmp_agent_trapv3_send(NX_SNMP_AGENT *agent_ptr, 
            ULONG ip_address, UCHAR *username, UINT trap_type, 
            ULONG elapsed_time, NX_SNMP_TRAP_OBJECT *object_list_ptr);
```

### <a name="description"></a><span data-ttu-id="d1e56-794">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-794">Description</span></span>

<span data-ttu-id="d1e56-795">Bu hizmet, belirtilen IPv4 adresinde SNMP Yöneticisi 'ne bir SNMPv3 tuzağı gönderir.</span><span class="sxs-lookup"><span data-stu-id="d1e56-795">This service sends an SNMPv3 trap to the SNMP Manager at the specified IPv4 address.</span></span> <span data-ttu-id="d1e56-796">NetX Duo 'da SNMP tuzağı göndermek için tercih edilen yöntem *nxd_snmp_agent_trapv3_send* hizmetini kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-796">The preferred method for sending an SNMP trap in NetX Duo is to use the *nxd_snmp_agent_trapv3_send* service.</span></span> <span data-ttu-id="d1e56-797">*nx_snmp_agent_trapv3_send* , mevcut NETX SNMP Aracısı uygulamalarını desteklemek üzere NETX Duo 'e dahildir.</span><span class="sxs-lookup"><span data-stu-id="d1e56-797">*nx_snmp_agent_trapv3_send* is included in NetX Duo to support existing NetX SNMP Agent applications.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-798">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-798">Input Parameters</span></span>

- <span data-ttu-id="d1e56-799">**agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-799">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="d1e56-800">**ip_address** SNMP yöneticisinin IPv4 adresi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-800">**ip_address** IPv4 address of the SNMP Manager.</span></span>
- <span data-ttu-id="d1e56-801">**Kullanıcı adı** Topluluk adı (Kullanıcı adı).</span><span class="sxs-lookup"><span data-stu-id="d1e56-801">**username** Community name (username).</span></span>
- <span data-ttu-id="d1e56-802">**trap_type**</span><span class="sxs-lookup"><span data-stu-id="d1e56-802">**trap_type**</span></span>  
   <span data-ttu-id="d1e56-803">İstenen tuzak türü.</span><span class="sxs-lookup"><span data-stu-id="d1e56-803">Type of trap requested.</span></span> <span data-ttu-id="d1e56-804">Standart olaylar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="d1e56-804">The standard events are:</span></span>  
   - <span data-ttu-id="d1e56-805">NX_SNMP_TRAP_COLDSTART (0)</span><span class="sxs-lookup"><span data-stu-id="d1e56-805">NX_SNMP_TRAP_COLDSTART (0)</span></span>
   - <span data-ttu-id="d1e56-806">NX_SNMP_TRAP_WARMSTART (1)</span><span class="sxs-lookup"><span data-stu-id="d1e56-806">NX_SNMP_TRAP_WARMSTART (1)</span></span>
   - <span data-ttu-id="d1e56-807">NX_SNMP_TRAP_LINKDOWN (2)</span><span class="sxs-lookup"><span data-stu-id="d1e56-807">NX_SNMP_TRAP_LINKDOWN (2)</span></span>
   - <span data-ttu-id="d1e56-808">NX_SNMP_TRAP_LINKUP (3)</span><span class="sxs-lookup"><span data-stu-id="d1e56-808">NX_SNMP_TRAP_LINKUP (3)</span></span>
   - <span data-ttu-id="d1e56-809">NX_SNMP_TRAP_AUTHENTICATE_FAILURE (4)</span><span class="sxs-lookup"><span data-stu-id="d1e56-809">NX_SNMP_TRAP_AUTHENTICATE_FAILURE (4)</span></span>
   - <span data-ttu-id="d1e56-810">NX_SNMP_TRAP_EGPNEIGHBORLOSS (5)</span><span class="sxs-lookup"><span data-stu-id="d1e56-810">NX_SNMP_TRAP_EGPNEIGHBORLOSS (5)</span></span>

   <span data-ttu-id="d1e56-811">Özel veriler için:</span><span class="sxs-lookup"><span data-stu-id="d1e56-811">For proprietary data:</span></span>
   - <span data-ttu-id="d1e56-812">NX_SNMP_TRAP_CUSTOM (0xFFFFFFFF) ( *nxd_snmp. h* içinde tanımlanmıştır)</span><span class="sxs-lookup"><span data-stu-id="d1e56-812">NX_SNMP_TRAP_CUSTOM (0xFFFFFFFF) (defined in *nxd_snmp.h*)</span></span>

- <span data-ttu-id="d1e56-813">**Elapsed_Time** Zaman sistemi (sysUpTime).</span><span class="sxs-lookup"><span data-stu-id="d1e56-813">**elapsed_time** Time system has been up (sysUpTime).</span></span>
- <span data-ttu-id="d1e56-814">**object_list_ptr** SNMP tuzağı dahil edilecek nesne dizisi ve bunlarla ilişkili değerler.</span><span class="sxs-lookup"><span data-stu-id="d1e56-814">**object_list_ptr** Array of objects and their associated values to be included in the SNMP trap.</span></span> <span data-ttu-id="d1e56-815">Listenin sonlandırılması NX_NULL.</span><span class="sxs-lookup"><span data-stu-id="d1e56-815">The list is NX_NULL terminated.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-816">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-816">Return Values</span></span>

- <span data-ttu-id="d1e56-817">**NX_SUCCESS** (0x00) başarılı SNMP tuzak gönderme.</span><span class="sxs-lookup"><span data-stu-id="d1e56-817">**NX_SUCCESS** (0x00) Successful SNMP trap send.</span></span>
- <span data-ttu-id="d1e56-818">**NX_SNMP_ERROR** (0x100) SNMP tuzağı gönderme hatası.</span><span class="sxs-lookup"><span data-stu-id="d1e56-818">**NX_SNMP_ERROR** (0x100) Error sending SNMP trap.</span></span>
- <span data-ttu-id="d1e56-819">**NX_NOT_ENABLED** (0x14) SNMPv3 etkin değil.</span><span class="sxs-lookup"><span data-stu-id="d1e56-819">**NX_NOT_ENABLED** (0x14) SNMPv3 not enabled.</span></span>
- <span data-ttu-id="d1e56-820">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-820">**NX_PTR_ERROR** (0x07) Invalid input pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-821">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-821">Allowed From</span></span>

<span data-ttu-id="d1e56-822">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-822">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-823">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-823">Example</span></span>

```c
NX_SNMP_TRAP_OBJECT trap_list[5];
ULONG dest_ip_address = IP_ADDRESS(1,2,3,4);

/* Build an empty object list, since it is not needed for the 
   NX_SNMP_TRAP_COLDSTART trap.  */
trap_list[0].nx_snmp_object_string_ptr =  NX_NULL;

/* Send trap to SNMP manager at 193.2.2.61.  */
Status =  nx_snmp_agent_trapv3_send(&my_agent, dest_ip_address, "public",
               NX_SNMP_TRAP_COLDSTART, tx_time_get(), trap_list);

/* If status is NX_SUCCESS the SNMP trap has been sent.  */
```

## <a name="nx_snmp_agent_trapv3_oid_send"></a><span data-ttu-id="d1e56-824">nx_snmp_agent_trapv3_oid_send</span><span class="sxs-lookup"><span data-stu-id="d1e56-824">nx_snmp_agent_trapv3_oid_send</span></span>
<span data-ttu-id="d1e56-825">Doğrudan OID 'yi belirten SNMPv3 tuzağı gönder</span><span class="sxs-lookup"><span data-stu-id="d1e56-825">Send SNMPv3 trap specifying OID directly</span></span> 

### <a name="prototype"></a><span data-ttu-id="d1e56-826">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-826">Prototype</span></span>

```c
UINT nx_snmp_agent_trapv3_oid_send(NX_SNMP_AGENT *agent_ptr, 
                                   ULONG ip_address, UCHAR *username,        
                                   UCHAR *oid, ULONG elapsed_time,   
                                   NX_SNMP_TRAP_OBJECT 
                                   *object_list_ptr);
```
### <a name="description"></a><span data-ttu-id="d1e56-827">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-827">Description</span></span>

<span data-ttu-id="d1e56-828">Bu hizmet, belirtilen IP adresindeki (yalnızca IPv4) SNMP yöneticisine bir SNMPv3 tuzağı gönderir ve çağıranın OID 'yi doğrudan belirlemesine izin verir.</span><span class="sxs-lookup"><span data-stu-id="d1e56-828">This service sends an SNMPv3 trap to the SNMP Manager at the specified IP address (IPv4 only) and allows the caller to specify the OID directly.</span></span> <span data-ttu-id="d1e56-829">NetX Duo 'da belirtilen OID ile SNMP tuzağı göndermek için tercih edilen yöntem *nxd_snmp_agent_trapv3_oid_send* hizmetini kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-829">The preferred method for sending an SNMP trap with specified OID in NetX Duo is to use the *nxd_snmp_agent_trapv3_oid_send* service.</span></span> <span data-ttu-id="d1e56-830">Mevcut NetX SNMP Aracısı uygulamalarını desteklemek için, NetX Duo 'e *nx_snmp_agent_trapv3_oid_ Send* işlemi dahildir.</span><span class="sxs-lookup"><span data-stu-id="d1e56-830">*nx_snmp_agent_trapv3_oid_ send* is included in NetX Duo to support existing NetX SNMP Agent applications.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-831">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-831">Input Parameters</span></span>

- <span data-ttu-id="d1e56-832">**agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-832">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="d1e56-833">**ip_address** SNMP yöneticisinin IP adresi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-833">**ip_address** IP address of SNMP Manager.</span></span>
- <span data-ttu-id="d1e56-834">**Kullanıcı adı** Topluluk adı (Kullanıcı adı).</span><span class="sxs-lookup"><span data-stu-id="d1e56-834">**username** Community name (username).</span></span>
- <span data-ttu-id="d1e56-835">**OID** OID içeren arabelleğin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-835">**oid** Pointer to buffer containing OID.</span></span>
- <span data-ttu-id="d1e56-836">**Elapsed_Time** Zaman sistemi (sysUpTime).</span><span class="sxs-lookup"><span data-stu-id="d1e56-836">**elapsed_time** Time system has been up (sysUpTime).</span></span>
- <span data-ttu-id="d1e56-837">**object_list_ptr** SNMP tuzağı dahil edilecek nesne dizisi ve bunlarla ilişkili değerler.</span><span class="sxs-lookup"><span data-stu-id="d1e56-837">**object_list_ptr** Array of objects and their associated values to be included in the SNMP trap.</span></span> <span data-ttu-id="d1e56-838">Listenin sonlandırılması NX_NULL.</span><span class="sxs-lookup"><span data-stu-id="d1e56-838">The list is NX_NULL terminated.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-839">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-839">Return Values</span></span>

- <span data-ttu-id="d1e56-840">**NX_SUCCESS** (0x00) başarılı SNMP tuzak gönderme.</span><span class="sxs-lookup"><span data-stu-id="d1e56-840">**NX_SUCCESS** (0x00) Successful SNMP trap send.</span></span>
- <span data-ttu-id="d1e56-841">**NX_SNMP_ERROR** (0x100) SNMP tuzağı gönderme hatası.</span><span class="sxs-lookup"><span data-stu-id="d1e56-841">**NX_SNMP_ERROR** (0x100) Error sending SNMP trap.</span></span>
- <span data-ttu-id="d1e56-842">**NX_PTR_ERROR** (0x16) geçersiz SNMP Aracısı veya parametre işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-842">**NX_PTR_ERROR** (0x16) Invalid SNMP Agent or parameter pointer.</span></span>
- <span data-ttu-id="d1e56-843">**NX_IP_ADDRESS_ERROR** (0x21) GEÇERSIZ hedef IP adresi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-843">**NX_IP_ADDRESS_ERROR** (0x21) Invalid destination IP address.</span></span>
- <span data-ttu-id="d1e56-844">**NX_OPTION_ERROR** (0X0a) geçersiz parametre.</span><span class="sxs-lookup"><span data-stu-id="d1e56-844">**NX_OPTION_ERROR** (0x0a) Invalid parameter.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-845">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-845">Allowed From</span></span>

<span data-ttu-id="d1e56-846">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-846">Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-847">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-847">Example</span></span>

```c
NX_SNMP_TRAP_OBJECT trap_list[5];

/* Build an empty object list */
trap_list[0].nx_snmp_object_string_ptr =  NX_NULL;

/* Send trap to SNMP manager at 193.2.2.61.  */
Status =  nx_snmp_agent_trapv3_oid_send(&my_agent, IP_ADDRESS(193,2,2,61), 
                                       "public", (UCHAR *)"0.9.9.9.9.9.9.9.9.9",  
                                       tx_time_get(), trap_list);

/* If status is NX_SUCCESS the SNMP trap has been sent.  */
```
## <a name="nxd_snmp_agent_trapv3_send"></a><span data-ttu-id="d1e56-848">nxd_snmp_agent_trapv3_send</span><span class="sxs-lookup"><span data-stu-id="d1e56-848">nxd_snmp_agent_trapv3_send</span></span>
<span data-ttu-id="d1e56-849">SNMPv3 tuzağı gönderme (IPv4 ve IPv6)</span><span class="sxs-lookup"><span data-stu-id="d1e56-849">Send SNMPv3 trap (IPv4 and IPv6)</span></span>

### <a name="prototype"></a><span data-ttu-id="d1e56-850">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-850">Prototype</span></span>

```c
UINT nxd_snmp_agent_trapv3_send(NX_SNMP_AGENT *agent_ptr, 
                                NXD_ADDRESS *ip_address, 
                                UCHAR *username, UINT trap_type, 
                                ULONG elapsed_time, 
                                NX_SNMP_TRAP_OBJECT *object_list_ptr);
```
### <a name="description"></a><span data-ttu-id="d1e56-851">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-851">Description</span></span>

<span data-ttu-id="d1e56-852">Bu hizmet, belirtilen IP adresindeki SNMP Yöneticisi 'ne SNMP tuzağı gönderir.</span><span class="sxs-lookup"><span data-stu-id="d1e56-852">This service sends an SNMP trap to the SNMP Manager at the specified IP address.</span></span> <span data-ttu-id="d1e56-853">Tuzak iletisi biçimi SNMP v3 PDU 'SU içinde içerilmediği sürece bu tuzak, SNMP v2 tuzağı temelde aynıdır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-853">This trap is basically the same as the SNMP v2 trap, except the trap message format is contained in the SNMP v3 PDU.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-854">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-854">Input Parameters</span></span>

- <span data-ttu-id="d1e56-855">**agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-855">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="d1e56-856">**ip_address** SNMP yöneticisinin IP (IPv4 veya IPv6) adresi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-856">**ip_address** IP (IPv4 or IPv6) address of the SNMP Manager.</span></span>
- <span data-ttu-id="d1e56-857">**Kullanıcı adı** Topluluk adı (Kullanıcı adı).</span><span class="sxs-lookup"><span data-stu-id="d1e56-857">**username** Community name (username).</span></span>
- <span data-ttu-id="d1e56-858">**trap_type**</span><span class="sxs-lookup"><span data-stu-id="d1e56-858">**trap_type**</span></span>  
   <span data-ttu-id="d1e56-859">İstenen tuzak türü.</span><span class="sxs-lookup"><span data-stu-id="d1e56-859">Type of trap requested.</span></span> <span data-ttu-id="d1e56-860">Standart olaylar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="d1e56-860">The standard events are:</span></span>
   - <span data-ttu-id="d1e56-861">NX_SNMP_TRAP_COLDSTART (0)</span><span class="sxs-lookup"><span data-stu-id="d1e56-861">NX_SNMP_TRAP_COLDSTART (0)</span></span>
   - <span data-ttu-id="d1e56-862">NX_SNMP_TRAP_WARMSTART (1)</span><span class="sxs-lookup"><span data-stu-id="d1e56-862">NX_SNMP_TRAP_WARMSTART (1)</span></span>
   - <span data-ttu-id="d1e56-863">NX_SNMP_TRAP_LINKDOWN (2)</span><span class="sxs-lookup"><span data-stu-id="d1e56-863">NX_SNMP_TRAP_LINKDOWN (2)</span></span>
   - <span data-ttu-id="d1e56-864">NX_SNMP_TRAP_LINKUP (3)</span><span class="sxs-lookup"><span data-stu-id="d1e56-864">NX_SNMP_TRAP_LINKUP (3)</span></span>
   - <span data-ttu-id="d1e56-865">NX_SNMP_TRAP_AUTHENTICATE_FAILURE (4)</span><span class="sxs-lookup"><span data-stu-id="d1e56-865">NX_SNMP_TRAP_AUTHENTICATE_FAILURE (4)</span></span>
   - <span data-ttu-id="d1e56-866">NX_SNMP_TRAP_EGPNEIGHBORLOSS (5)</span><span class="sxs-lookup"><span data-stu-id="d1e56-866">NX_SNMP_TRAP_EGPNEIGHBORLOSS (5)</span></span>  
   <span data-ttu-id="d1e56-867">Özel veriler için:</span><span class="sxs-lookup"><span data-stu-id="d1e56-867">For proprietary data:</span></span>
   - <span data-ttu-id="d1e56-868">NX_SNMP_TRAP_CUSTOM (0xFFFFFFFF) ( *nxd_snmp. h* içinde tanımlanmıştır)</span><span class="sxs-lookup"><span data-stu-id="d1e56-868">NX_SNMP_TRAP_CUSTOM (0xFFFFFFFF) (defined in *nxd_snmp.h*)</span></span>

- <span data-ttu-id="d1e56-869">**Elapsed_Time** Zaman sistemi (sysUpTime).</span><span class="sxs-lookup"><span data-stu-id="d1e56-869">**elapsed_time** Time system has been up (sysUpTime).</span></span>
- <span data-ttu-id="d1e56-870">**object_list_ptr** SNMP tuzağı dahil edilecek nesne dizisi ve bunlarla ilişkili değerler.</span><span class="sxs-lookup"><span data-stu-id="d1e56-870">**object_list_ptr** Array of objects and their associated values to be included in the SNMP trap.</span></span> <span data-ttu-id="d1e56-871">Listenin sonlandırılması NX_NULL.</span><span class="sxs-lookup"><span data-stu-id="d1e56-871">The list is NX_NULL terminated.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-872">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-872">Return Values</span></span>

- <span data-ttu-id="d1e56-873">**NX_SUCCESS** (0x00) başarılı SNMP tuzak gönderme.</span><span class="sxs-lookup"><span data-stu-id="d1e56-873">**NX_SUCCESS** (0x00) Successful SNMP trap send.</span></span>
- <span data-ttu-id="d1e56-874">**NX_SNMP_ERROR** (0x100) SNMP tuzağı gönderme hatası.</span><span class="sxs-lookup"><span data-stu-id="d1e56-874">**NX_SNMP_ERROR** (0x100) Error sending SNMP trap.</span></span>
- <span data-ttu-id="d1e56-875">**NX_NOT_ENABLED** (0x14) SNMPv3 etkin değil.</span><span class="sxs-lookup"><span data-stu-id="d1e56-875">**NX_NOT_ENABLED** (0x14) SNMPv3 not enabled.</span></span>
- <span data-ttu-id="d1e56-876">**NX_SNMP_INVALID_IP_PROTOCOL_ERROR** (0x104) desteklenmeyen IP sürümü</span><span class="sxs-lookup"><span data-stu-id="d1e56-876">**NX_SNMP_INVALID_IP_PROTOCOL_ERROR** (0x104) Unsupported IP version</span></span>
- <span data-ttu-id="d1e56-877">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-877">**NX_PTR_ERROR** (0x07) Invalid input pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-878">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-878">Allowed From</span></span>

<span data-ttu-id="d1e56-879">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-879">Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-880">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-880">Example</span></span>

```c
NX_SNMP_TRAP_OBJECT trap_list[5];
NXD_ADDRESS dest_ip_address;

    dest_ip_address.nxd_ip_version = NX_IP_VERSION_V6 ;
    dest_ip_address.nxd_ip_address.v6[0] = 0x20010db8;
    dest_ip_address.nxd_ip_address.v6[1] = 0xf101;
    dest_ip_address.nxd_ip_address.v6[2] = 0x00000000;
    dest_ip_address.nxd_ip_address.v6[3] = 0x00000101;

/* Build an empty object list, since it is not needed for the 
   NX_SNMP_TRAP_COLDSTART trap.  */
trap_list[0].nx_snmp_object_string_ptr =  NX_NULL;

/* Send trap to SNMP manager at 193.2.2.61.  */
Status =  nxd_snmp_agent_trapv3_send(&my_agent, &dest_ip_address, "public",
                                    NX_SNMP_TRAP_COLDSTART, tx_time_get(),  
                                    trap_list);

/* If status is NX_SUCCESS the SNMP trap has been sent.  */
```

## <a name="nxd_snmp_agent_trapv3_oid_send"></a><span data-ttu-id="d1e56-881">nxd_snmp_agent_trapv3_oid_send</span><span class="sxs-lookup"><span data-stu-id="d1e56-881">nxd_snmp_agent_trapv3_oid_send</span></span>
<span data-ttu-id="d1e56-882">Doğrudan OID 'yi belirten SNMPv3 tuzağı gönder</span><span class="sxs-lookup"><span data-stu-id="d1e56-882">Send SNMPv3 trap specifying OID directly</span></span> 

### <a name="prototype"></a><span data-ttu-id="d1e56-883">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-883">Prototype</span></span>

```c
UINT nxd_snmp_agent_trapv3_oid_send(NX_SNMP_AGENT *agent_ptr, 
                                    NXD_ADDRESS *ip_address, 
                                    UCHAR *username,        
                                    UCHAR *oid, ULONG elapsed_time,   
                                    NX_SNMP_TRAP_OBJECT 
                                            *object_list_ptr);
```
### <a name="description"></a><span data-ttu-id="d1e56-884">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-884">Description</span></span>

<span data-ttu-id="d1e56-885">Bu hizmet, belirtilen IP adresindeki (IPv4/IPv6) SNMP Yöneticisi 'ne bir SNMPv3 tuzağı gönderir ve çağıranın OID 'yi doğrudan belirlemesine izin verir.</span><span class="sxs-lookup"><span data-stu-id="d1e56-885">This service sends an SNMPv3 trap to the SNMP Manager at the specified IP address (IPv4/IPv6) and allows the caller to specify the OID directly.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-886">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-886">Input Parameters</span></span>

- <span data-ttu-id="d1e56-887">**agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-887">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="d1e56-888">**ip_address** SNMP yöneticisinin IP adresi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-888">**ip_address** Pointer to IP address of SNMP Manager.</span></span>
- <span data-ttu-id="d1e56-889">**Kullanıcı adı** Kullanıcı adı (topluluk adı).</span><span class="sxs-lookup"><span data-stu-id="d1e56-889">**username** Username (community name).</span></span>
- <span data-ttu-id="d1e56-890">**OID** OID içeren arabelleğin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-890">**oid** Pointer to buffer containing OID.</span></span>
- <span data-ttu-id="d1e56-891">**Elapsed_Time** Zaman sistemi (sysUpTime).</span><span class="sxs-lookup"><span data-stu-id="d1e56-891">**elapsed_time** Time system has been up (sysUpTime).</span></span>
- <span data-ttu-id="d1e56-892">**object_list_ptr** SNMP tuzağı dahil edilecek nesne dizisi ve bunlarla ilişkili değerler.</span><span class="sxs-lookup"><span data-stu-id="d1e56-892">**object_list_ptr** Array of objects and their associated values to be included in the SNMP trap.</span></span> <span data-ttu-id="d1e56-893">Listenin sonlandırılması NX_NULL.</span><span class="sxs-lookup"><span data-stu-id="d1e56-893">The list is NX_NULL terminated.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-894">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-894">Return Values</span></span>

- <span data-ttu-id="d1e56-895">**NX_SUCCESS** (0x00) başarılı SNMP tuzak gönderme.</span><span class="sxs-lookup"><span data-stu-id="d1e56-895">**NX_SUCCESS** (0x00) Successful SNMP trap send.</span></span>
- <span data-ttu-id="d1e56-896">**NX_SNMP_ERROR** (0x100) SNMP tuzağı gönderme hatası.</span><span class="sxs-lookup"><span data-stu-id="d1e56-896">**NX_SNMP_ERROR** (0x100) Error sending SNMP trap.</span></span>
- <span data-ttu-id="d1e56-897">**NX_PTR_ERROR** (0x16) geçersiz SNMP Aracısı veya parametre işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-897">**NX_PTR_ERROR** (0x16) Invalid SNMP Agent or parameter pointer.</span></span>
- <span data-ttu-id="d1e56-898">**NX_IP_ADDRESS_ERROR** (0x21) GEÇERSIZ hedef IP adresi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-898">**NX_IP_ADDRESS_ERROR** (0x21) Invalid destination IP address.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-899">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-899">Allowed From</span></span>

<span data-ttu-id="d1e56-900">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-900">Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-901">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-901">Example</span></span>

```c
NXD_ADDRESS         ip_address;
NX_SNMP_TRAP_OBJECT trap_list[5];

/* Build an empty object list */
trap_list[0].nx_snmp_object_string_ptr =  NX_NULL;

ip_address.nxd_ip_version = NX_IP_VERSION_V4;
ip_address.nxd_ip_address.v4 = IP_ADDRESS(193,2,2,61);

/* Send trap to SNMP manager at 193.2.2.61.  */
Status =  nxd_snmp_agent_trapv3_oid_send(&my_agent, &ip_address, 
                                       "public", (UCHAR *)"0.9.9.9.9.9.9.9.9.9",  
                                       tx_time_get(), trap_list);

/* If status is NX_SUCCESS the SNMP trap has been sent.  */
```
## <a name="nx_snmp_agent_v3_context_boots_set"></a><span data-ttu-id="d1e56-902">nx_snmp_agent_v3_context_boots_set</span><span class="sxs-lookup"><span data-stu-id="d1e56-902">nx_snmp_agent_v3_context_boots_set</span></span>
<span data-ttu-id="d1e56-903">Yeniden başlatmalar sayısını ayarla (SNMPv3 etkin ise)</span><span class="sxs-lookup"><span data-stu-id="d1e56-903">Set the number of reboots (if SNMPv3 enabled)</span></span>

### <a name="prototype"></a><span data-ttu-id="d1e56-904">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-904">Prototype</span></span>

```c
UINT nx_snmp_agent_v3_context_boots_set(NX_SNMP_AGENT *agent_ptr, 
                                        UINT boots);
```

### <a name="description"></a><span data-ttu-id="d1e56-905">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-905">Description</span></span>

<span data-ttu-id="d1e56-906">Bu hizmet SNMP Aracısı tarafından kaydedilen yeniden başlatmalar sayısını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d1e56-906">This service sets the number of reboots recorded by the SNMP agent.</span></span> <span data-ttu-id="d1e56-907">Bu hizmet yalnızca, önyükleme sayısı SNMPv3 protokolünde kullanıldığı için SNMP Aracısı için SNMPv3 etkin olduğunda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d1e56-907">This service is only available if SNMPv3 is enabled for the SNMP agent because boot count is only used in the SNMPv3 protocol.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-908">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-908">Input Parameters</span></span>

- <span data-ttu-id="d1e56-909">**agent_ptr** SNMP Aracısı denetim bloğu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d1e56-909">**agent_ptr** Pointer to SNMP Agent control block</span></span>
- <span data-ttu-id="d1e56-910">**önyüklemeler** SNMP Aracısı önyükleme sayısı ayarlanacak değer</span><span class="sxs-lookup"><span data-stu-id="d1e56-910">**boots** The value to set SNMP Agent boot count to</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-911">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-911">Return Values</span></span>

- <span data-ttu-id="d1e56-912">**NX_SUCCESS** (0x00) önyükleme sayısı başarıyla ayarlandı</span><span class="sxs-lookup"><span data-stu-id="d1e56-912">**NX_SUCCESS** (0x00) Successfully set boot count</span></span>
- <span data-ttu-id="d1e56-913">**NX_SNMP_ERROR** (0x100) önyükleme sayısı ayarlanırken hata oluştu</span><span class="sxs-lookup"><span data-stu-id="d1e56-913">**NX_SNMP_ERROR** (0x100) Error setting boot count</span></span>
- <span data-ttu-id="d1e56-914">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d1e56-914">**NX_PTR_ERROR** (0x07) Invalid input pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-915">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-915">Allowed From</span></span>

<span data-ttu-id="d1e56-916">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-916">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-917">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-917">Example</span></span>

```c
UINT my_boots = 4;

if (my_agent.nx_snmp_agent_v3_enabled == NX_TRUE)
{
   status = nx_snmp_agent_v3_context_boots_set(&my_agent, my_boots);
}


/* If status is NX_SUCCESS the SNMP boot count is set.  */
```

## <a name="nx_snmp_object_compare"></a><span data-ttu-id="d1e56-918">nx_snmp_object_compare</span><span class="sxs-lookup"><span data-stu-id="d1e56-918">nx_snmp_object_compare</span></span>
<span data-ttu-id="d1e56-919">İki nesneyi karşılaştırın</span><span class="sxs-lookup"><span data-stu-id="d1e56-919">Compare two objects</span></span> 

### <a name="prototype"></a><span data-ttu-id="d1e56-920">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-920">Prototype</span></span>

```c
UINT nx_snmp_object_compare(UCHAR *object, UCHAR *reference_object);
```

### <a name="description"></a><span data-ttu-id="d1e56-921">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-921">Description</span></span>

<span data-ttu-id="d1e56-922">Bu hizmet, sağlanan nesne KIMLIĞINI başvuru nesne KIMLIĞIYLE karşılaştırır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-922">This service compares the supplied object ID with the reference object ID.</span></span> <span data-ttu-id="d1e56-923">Her iki nesne kimliği de ASCII SMı gösteriminde, ör. her iki nesne da "1.3.6" ASCII dizesiyle başlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-923">Both object IDs are in the ASCII SMI notation, e.g., both object must start with the ASCII string “1.3.6”.</span></span>

<span data-ttu-id="d1e56-924">Bu hizmet kullanımdan kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-924">This service is deprecated.</span></span> <span data-ttu-id="d1e56-925">Geliştiricilerin *nx_snmp_object_compare_extended ()* uygulamasına geçirilmesi önerilir.</span><span class="sxs-lookup"><span data-stu-id="d1e56-925">Developers are encouraged to migrate to *nx_snmp_object_compare_extended().*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-926">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-926">Input Parameters</span></span>

- <span data-ttu-id="d1e56-927">**nesne** Nesne KIMLIĞI işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-927">**object** Pointer to object ID.</span></span>
- <span data-ttu-id="d1e56-928">**reference_object** Başvuru nesnesi KIMLIĞINE yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-928">**reference_object** Pointer to the reference object ID.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-929">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-929">Return Values</span></span>

- <span data-ttu-id="d1e56-930">**NX_SUCCESS** (0x00) nesne başvuru nesnesiyle eşleşir.</span><span class="sxs-lookup"><span data-stu-id="d1e56-930">**NX_SUCCESS** (0x00) The object matches the reference object.</span></span>
- <span data-ttu-id="d1e56-931">**NX_SNMP_NEXT_ENTRY** (0x101) nesne başvuru nesnesinden küçüktür.</span><span class="sxs-lookup"><span data-stu-id="d1e56-931">**NX_SNMP_NEXT_ENTRY** (0x101) The object is less than the reference object.</span></span>
- <span data-ttu-id="d1e56-932">**NX_SNMP_ERROR** (0x100) nesne başvuru nesnesinden daha büyük.</span><span class="sxs-lookup"><span data-stu-id="d1e56-932">**NX_SNMP_ERROR** (0x100) The object is greater than the reference object.</span></span>
- <span data-ttu-id="d1e56-933">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-933">**NX_PTR_ERROR** (0x07) Invalid input pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-934">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-934">Allowed From</span></span>

<span data-ttu-id="d1e56-935">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-935">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-936">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-936">Example</span></span>

```c
/* Compare “requested_object” with the sysDescr object ID of 
   "1.3.6.1.2.1.1.1.0".  */
Status =  nx_snmp_object_compare(requested_object, "1.3.6.1.2.1.1.1.0");

/* If status is NX_SUCCESS, requested_object is the sysDescr object. 
   Otherwise, if status is NX_SNMP_NEXT_ENTRY, the requested object is
   less than the sysDescr. If status is NX_SNMP_ERROR, the object is 
   greater than sysDescr. */
```

## <a name="nx_snmp_object_compare_extended"></a><span data-ttu-id="d1e56-937">nx_snmp_object_compare_extended</span><span class="sxs-lookup"><span data-stu-id="d1e56-937">nx_snmp_object_compare_extended</span></span>
<span data-ttu-id="d1e56-938">İki nesneyi karşılaştırın</span><span class="sxs-lookup"><span data-stu-id="d1e56-938">Compare two objects</span></span> 

### <a name="prototype"></a><span data-ttu-id="d1e56-939">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-939">Prototype</span></span>

```c
UINT nx_snmp_object_compare_extended(UCHAR *request_object, 
                                     UINT requested_object_length,
                                     UCHAR *reference_object
                                     UINT reference_object_length);
```
### <a name="description"></a><span data-ttu-id="d1e56-940">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-940">Description</span></span>

<span data-ttu-id="d1e56-941">Bu hizmet, sağlanan nesne KIMLIĞINI başvuru nesne KIMLIĞIYLE karşılaştırır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-941">This service compares the supplied object ID with the reference object ID.</span></span> <span data-ttu-id="d1e56-942">Her iki nesne kimliği de ASCII SMı gösteriminde, ör. her iki nesne da "1.3.6" ASCII dizesiyle başlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-942">Both object IDs are in the ASCII SMI notation, e.g., both object must start with the ASCII string “1.3.6”.</span></span>

<span data-ttu-id="d1e56-943">Bu hizmet *nx_snmp_object_compare ()* yerini alır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-943">This service replaces *nx_snmp_object_compare().*</span></span> <span data-ttu-id="d1e56-944">Bu sürüm, arayanlara uzunluk bilgilerini sağlaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d1e56-944">This version requires callers to supply length information.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-945">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-945">Input Parameters</span></span>

- <span data-ttu-id="d1e56-946">**request_object** İstek nesnesi KIMLIĞI işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-946">**request_object** Pointer to request object ID.</span></span>
- <span data-ttu-id="d1e56-947">**request_object_length** İstek nesnesi KIMLIĞININ uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="d1e56-947">**request_object_length** Length of the request object ID.</span></span>
- <span data-ttu-id="d1e56-948">**reference_object** Başvuru nesnesi KIMLIĞINE yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-948">**reference_object** Pointer to the reference object ID.</span></span>
- <span data-ttu-id="d1e56-949">**reference_object_length** Başvuru nesnesi KIMLIĞININ uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="d1e56-949">**reference_object_length** Length of the reference object ID.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-950">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-950">Return Values</span></span>

- <span data-ttu-id="d1e56-951">**NX_SUCCESS** (0x00) nesne başvuru nesnesiyle eşleşir.</span><span class="sxs-lookup"><span data-stu-id="d1e56-951">**NX_SUCCESS** (0x00) The object matches the reference object.</span></span>
- <span data-ttu-id="d1e56-952">**NX_SNMP_NEXT_ENTRY** (0x101) nesne başvuru nesnesinden küçüktür.</span><span class="sxs-lookup"><span data-stu-id="d1e56-952">**NX_SNMP_NEXT_ENTRY** (0x101) The object is less than the reference object.</span></span>
- <span data-ttu-id="d1e56-953">**NX_SNMP_ERROR** (0x100) nesne başvuru nesnesinden daha büyük.</span><span class="sxs-lookup"><span data-stu-id="d1e56-953">**NX_SNMP_ERROR** (0x100) The object is greater than the reference object.</span></span>
- <span data-ttu-id="d1e56-954">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-954">**NX_PTR_ERROR** (0x07) Invalid input pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-955">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-955">Allowed From</span></span>

<span data-ttu-id="d1e56-956">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-956">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-957">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-957">Example</span></span>

```c
/* Compare “requested_object” with the sysDescr object ID of 
   "1.3.6.1.2.1.1.1.0".  */
Status =  nx_snmp_object_compare_extended(requested_object, 17,
                                          "1.3.6.1.2.1.1.1.0", 17);

/* If status is NX_SUCCESS, requested_object is the sysDescr object. 
   Otherwise, if status is NX_SNMP_NEXT_ENTRY, the requested object is
   less than the sysDescr. If status is NX_SNMP_ERROR, the object is 
   greater than sysDescr. */
```

## <a name="nx_snmp_object_copy"></a><span data-ttu-id="d1e56-958">nx_snmp_object_copy</span><span class="sxs-lookup"><span data-stu-id="d1e56-958">nx_snmp_object_copy</span></span>
<span data-ttu-id="d1e56-959">Nesne kopyalama</span><span class="sxs-lookup"><span data-stu-id="d1e56-959">Copy an object</span></span> 

### <a name="prototype"></a><span data-ttu-id="d1e56-960">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-960">Prototype</span></span>

```c
UINT  nx_snmp_object_copy(UCHAR *source_object_name, 
                          UCHAR *destination_object_name);
```
### <a name="description"></a><span data-ttu-id="d1e56-961">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-961">Description</span></span>

<span data-ttu-id="d1e56-962">Bu hizmet, ASCII SIM gösterimi içindeki kaynak nesneyi hedef nesneye kopyalar.</span><span class="sxs-lookup"><span data-stu-id="d1e56-962">This service copies the source object in ASCII SIM notation to the destination object.</span></span>

<span data-ttu-id="d1e56-963">Bu hizmet kullanımdan kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-963">This service is deprecated.</span></span> <span data-ttu-id="d1e56-964">Geliştiricilerin *nx_snmp_object_copy_extended ()* uygulamasına geçirilmesi önerilir.</span><span class="sxs-lookup"><span data-stu-id="d1e56-964">Developers are encouraged to migrate to *nx_snmp_object_copy_extended().*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-965">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-965">Input Parameters</span></span>

- <span data-ttu-id="d1e56-966">**source_object_name** Kaynak nesne KIMLIĞI işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-966">**source_object_name** Pointer to source object ID.</span></span>
- <span data-ttu-id="d1e56-967">**destination_object_name** Hedef nesne KIMLIĞI işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-967">**destination_object_name** Pointer to destination object ID.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-968">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-968">Return Values</span></span>

- <span data-ttu-id="d1e56-969">**Boyut** Hedef ada kopyalanmış bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="d1e56-969">**size** Number of bytes copied to destination name.</span></span> <span data-ttu-id="d1e56-970">Hata ise, sıfır döndürülür.</span><span class="sxs-lookup"><span data-stu-id="d1e56-970">If error, zero is returned.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-971">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-971">Allowed From</span></span>

<span data-ttu-id="d1e56-972">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-972">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-973">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-973">Example</span></span>

```c
/* Copy “my_object” to “my_new_object”.  */
size =  nx_snmp_object_copy(my_object, my_new_object);

/* Size contains the number of bytes copied. */
```

## <a name="nx_snmp_object_copy_extended"></a><span data-ttu-id="d1e56-974">nx_snmp_object_copy_extended</span><span class="sxs-lookup"><span data-stu-id="d1e56-974">nx_snmp_object_copy_extended</span></span>
<span data-ttu-id="d1e56-975">Nesne kopyalama</span><span class="sxs-lookup"><span data-stu-id="d1e56-975">Copy an object</span></span> 

### <a name="prototype"></a><span data-ttu-id="d1e56-976">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-976">Prototype</span></span>

```c
UINT  nx_snmp_object_copy_extended(UCHAR *source_object_name, 
                             UINT source_object_name_length,
                             UCHAR *destination_object_name_buffer,
                             UINT destination_object_name_buffer_size);
```

### <a name="description"></a><span data-ttu-id="d1e56-977">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-977">Description</span></span>

<span data-ttu-id="d1e56-978">Bu hizmet, ASCII SIM gösterimi içindeki kaynak nesneyi hedef nesneye kopyalar.</span><span class="sxs-lookup"><span data-stu-id="d1e56-978">This service copies the source object in ASCII SIM notation to the destination object.</span></span>

<span data-ttu-id="d1e56-979">Bu hizmet *nx_snmp_object_copy ()* yerini alır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-979">This service replaces *nx_snmp_object_copy().*</span></span> <span data-ttu-id="d1e56-980">Bu sürüm, arayanlara uzunluk bilgilerini sağlaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d1e56-980">This version requires callers to supply length information.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-981">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-981">Input Parameters</span></span>

- <span data-ttu-id="d1e56-982">**source_object_name** Kaynak nesne KIMLIĞI işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-982">**source_object_name** Pointer to source object ID.</span></span>
- <span data-ttu-id="d1e56-983">**source_object_name_length** Kaynak nesne KIMLIĞININ uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="d1e56-983">**source_object_name_length** Length of source object ID.</span></span>
- <span data-ttu-id="d1e56-984">**destination_object_name_buffer** Hedef nesne arabelleği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-984">**destination_object_name_buffer** Pointer to destination object buffer.</span></span>
- <span data-ttu-id="d1e56-985">**destination_object_name_buffer_size** Hedef nesne arabelleğinin boyutu.</span><span class="sxs-lookup"><span data-stu-id="d1e56-985">**destination_object_name_buffer_size** Size of destination object buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-986">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-986">Return Values</span></span>

- <span data-ttu-id="d1e56-987">**Boyut** Hedef ada kopyalanmış bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="d1e56-987">**size** Number of bytes copied to destination name.</span></span> <span data-ttu-id="d1e56-988">Hata ise, sıfır döndürülür.</span><span class="sxs-lookup"><span data-stu-id="d1e56-988">If error, zero is returned.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-989">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-989">Allowed From</span></span>

<span data-ttu-id="d1e56-990">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-990">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-991">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-991">Example</span></span>

```c
UCHAR   my_object = "1.3.6.1.2.1.1.1.0";
UCHAR   my_new_object[32];


/* Copy “my_object” to “my_new_object”.  */
size =  nx_snmp_object_copy(my_object, 17, my_new_object, sizeof(my_new_object));

/* Size contains the number of bytes copied. */
```

## <a name="nx_snmp_object_counter_get"></a><span data-ttu-id="d1e56-992">nx_snmp_object_counter_get</span><span class="sxs-lookup"><span data-stu-id="d1e56-992">nx_snmp_object_counter_get</span></span>
<span data-ttu-id="d1e56-993">Sayaç nesnesi Al</span><span class="sxs-lookup"><span data-stu-id="d1e56-993">Get counter object</span></span> 

### <a name="prototype"></a><span data-ttu-id="d1e56-994">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-994">Prototype</span></span>

```c
UINT  nx_snmp_object_counter_get(VOID *source_ptr, 
                                 NX_SNMP_OBJECT_DATA *object_data);
```
### <a name="description"></a><span data-ttu-id="d1e56-995">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-995">Description</span></span>

<span data-ttu-id="d1e56-996">Bu hizmet, kaynak işaretçi tarafından belirtilen adresteki sayaç nesnesini alır ve NetX nesne verileri yapısına koyar.</span><span class="sxs-lookup"><span data-stu-id="d1e56-996">This service retrieves the counter object at the address specified by the source pointer and places it in the NetX object data structure.</span></span> <span data-ttu-id="d1e56-997">Bu yordam genellikle GET veya GETNEXT uygulama geri çağırma yordamından çağırılır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-997">This routine is typically called from the GET or GETNEXT application callback routine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-998">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-998">Input Parameters</span></span>

- <span data-ttu-id="d1e56-999">**source_ptr** Sayaç kaynağı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-999">**source_ptr** Pointer to counter source.</span></span>
- <span data-ttu-id="d1e56-1000">**object_data** Hedef nesne yapısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1000">**object_data** Pointer to destination object structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-1001">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-1001">Return Values</span></span>

- <span data-ttu-id="d1e56-1002">**NX_SUCCESS** (0x00) sayaç nesnesi başarıyla alındı.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1002">**NX_SUCCESS** (0x00) The counter object has be successfully retrieved.</span></span>
- <span data-ttu-id="d1e56-1003">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1003">**NX_PTR_ERROR** (0x07) Invalid input pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-1004">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-1004">Allowed From</span></span>

<span data-ttu-id="d1e56-1005">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-1005">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-1006">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-1006">Example</span></span>

```c
/* Get the ifInOctets (1.3.6.1.2.1.2.2.1.10.0) MIB-2 object.  */
status =  nx_snmp_object_counter_get(&ifInOctets, my_object);

/* If status is NX_SUCCESS, the ifInOctets object has been 
   retrieved and is ready to be returned. */
```

## <a name="nx_snmp_object_counter_set"></a><span data-ttu-id="d1e56-1007">nx_snmp_object_counter_set</span><span class="sxs-lookup"><span data-stu-id="d1e56-1007">nx_snmp_object_counter_set</span></span>
<span data-ttu-id="d1e56-1008">Sayaç nesnesi ayarla</span><span class="sxs-lookup"><span data-stu-id="d1e56-1008">Set counter object</span></span> 

### <a name="prototype"></a><span data-ttu-id="d1e56-1009">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-1009">Prototype</span></span>

```c
UINT  nx_snmp_object_counter_set(VOID *destination_ptr, 
                                 NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a><span data-ttu-id="d1e56-1010">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-1010">Description</span></span>

<span data-ttu-id="d1e56-1011">Bu hizmet, hedef işaretçi tarafından belirtilen adresteki sayacı NetX nesne verileri yapısındaki sayaç değeriyle ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1011">This service sets the counter at the address specified by the destination pointer with the counter value in the NetX object data structure.</span></span> <span data-ttu-id="d1e56-1012">Bu yordam genellikle uygulama geri aramasını ayarla yordamından çağırılır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1012">This routine is typically called from the SET application callback routine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-1013">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-1013">Input Parameters</span></span>

- <span data-ttu-id="d1e56-1014">**destination_ptr** Sayaç hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1014">**destination_ptr** Pointer to counter destination.</span></span>
- <span data-ttu-id="d1e56-1015">**object_data** Sayaç kaynak nesne yapısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1015">**object_data** Pointer to counter source object structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-1016">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-1016">Return Values</span></span>

- <span data-ttu-id="d1e56-1017">**NX_SUCCESS** (0x00) sayaç nesnesi başarıyla ayarlandı.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1017">**NX_SUCCESS** (0x00) The counter object has be successfully set.</span></span>
- <span data-ttu-id="d1e56-1018">**NX_SNMP_ERROR_WRONGTYPE** (0x07) geçersiz nesne türü.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1018">**NX_SNMP_ERROR_WRONGTYPE** (0x07) Invalid object type.</span></span>
- <span data-ttu-id="d1e56-1019">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1019">**NX_PTR_ERROR** (0x07) Invalid input pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-1020">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-1020">Allowed From</span></span>

<span data-ttu-id="d1e56-1021">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-1021">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-1022">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-1022">Example</span></span>

```c
/* Set the ifInOctets (1.3.6.1.2.1.2.2.1.10.0) MIB-2 object with
   the counter object value contained in my_object.  */
status =  nx_snmp_object_counter_set(&ifInOctets, my_object);

/* If status is NX_SUCCESS, the ifInOctets object has been 
   set. */
```

## <a name="nx_snmp_object_counter64_get"></a><span data-ttu-id="d1e56-1023">nx_snmp_object_counter64_get</span><span class="sxs-lookup"><span data-stu-id="d1e56-1023">nx_snmp_object_counter64_get</span></span>
<span data-ttu-id="d1e56-1024">64 bitlik sayaç nesnesi Al</span><span class="sxs-lookup"><span data-stu-id="d1e56-1024">Get 64-bit counter object</span></span> 

### <a name="prototype"></a><span data-ttu-id="d1e56-1025">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-1025">Prototype</span></span>

```c
UINT  nx_snmp_object_counter64_get(VOID *source_ptr, 
                                   NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a><span data-ttu-id="d1e56-1026">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-1026">Description</span></span>

<span data-ttu-id="d1e56-1027">Bu hizmet, kaynak işaretçi tarafından belirtilen adresteki 64 bitlik sayaç nesnesini alır ve NetX nesne verileri yapısına koyar.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1027">This service retrieves the 64-bit counter object at the address specified by the source pointer and places it in the NetX object data structure.</span></span> <span data-ttu-id="d1e56-1028">Bu yordam genellikle GET veya GETNEXT uygulama geri çağırma yordamından çağırılır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1028">This routine is typically called from the GET or GETNEXT application callback routine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-1029">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-1029">Input Parameters</span></span>

- <span data-ttu-id="d1e56-1030">**source_ptr** Sayaç kaynağı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1030">**source_ptr** Pointer to counter source.</span></span>
- <span data-ttu-id="d1e56-1031">**object_data** Hedef nesne yapısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1031">**object_data** Pointer to destination object structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-1032">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-1032">Return Values</span></span>

- <span data-ttu-id="d1e56-1033">**NX_SUCCESS** (0x00) sayaç nesnesi başarıyla alındı.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1033">**NX_SUCCESS** (0x00) The counter object has be successfully retrieved.</span></span>
- <span data-ttu-id="d1e56-1034">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d1e56-1034">**NX_PTR_ERROR** (0x07) Invalid input pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-1035">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-1035">Allowed From</span></span>

<span data-ttu-id="d1e56-1036">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-1036">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-1037">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-1037">Example</span></span>

```c
/* Get the value of my_64_bit_counter and place it into my_object
   for return.  */
status =  nx_snmp_object_counter64_get(&my_64_bit_counter, my_object);

/* If status is NX_SUCCESS, the my_64_bit_counter object has been 
   retrieved and is ready to be returned. */
```

## <a name="nx_snmp_object_counter64_set"></a><span data-ttu-id="d1e56-1038">nx_snmp_object_counter64_set</span><span class="sxs-lookup"><span data-stu-id="d1e56-1038">nx_snmp_object_counter64_set</span></span>
<span data-ttu-id="d1e56-1039">64 bitlik sayaç nesnesini ayarla</span><span class="sxs-lookup"><span data-stu-id="d1e56-1039">Set 64-bit counter object</span></span> 

### <a name="prototype"></a><span data-ttu-id="d1e56-1040">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-1040">Prototype</span></span>

```c
UINT  nx_snmp_object_counter64_set(VOID *destination_ptr, 
                                   NX_SNMP_OBJECT_DATA *object_data);
```
### <a name="description"></a><span data-ttu-id="d1e56-1041">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-1041">Description</span></span>

<span data-ttu-id="d1e56-1042">Bu hizmet, hedef işaretçi tarafından belirtilen adresteki 64 bitlik sayacı NetX nesne verileri yapısında sayaç değeriyle ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1042">This service sets the 64-bit counter at the address specified by the destination pointer with the counter value in the NetX object data structure.</span></span> <span data-ttu-id="d1e56-1043">Bu yordam genellikle uygulama geri aramasını ayarla yordamından çağırılır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1043">This routine is typically called from the SET application callback routine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-1044">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-1044">Input Parameters</span></span>

- <span data-ttu-id="d1e56-1045">**destination_ptr** Sayaç hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1045">**destination_ptr** Pointer to counter destination.</span></span>
- <span data-ttu-id="d1e56-1046">**object_data** Sayaç kaynak nesne yapısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1046">**object_data** Pointer to counter source object structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-1047">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-1047">Return Values</span></span>

- <span data-ttu-id="d1e56-1048">**NX_SUCCESS** (0x00) sayaç nesnesi başarıyla ayarlandı.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1048">**NX_SUCCESS** (0x00) The counter object has be successfully set.</span></span>
- <span data-ttu-id="d1e56-1049">**NX_SNMP_ERROR_WRONGTYPE** (0x07) geçersiz nesne türü.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1049">**NX_SNMP_ERROR_WRONGTYPE** (0x07) Invalid object type.</span></span>
- <span data-ttu-id="d1e56-1050">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1050">**NX_PTR_ERROR** (0x07) Invalid input pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-1051">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-1051">Allowed From</span></span>

<span data-ttu-id="d1e56-1052">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-1052">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-1053">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-1053">Example</span></span>

```c
/* Set the value of my_64_bit_counter with the value in my_object.  */
status =  nx_snmp_object_counter64_set(&my_64_bit_counter, my_object);

/* If status is NX_SUCCESS, the my_64_bit_counter object has been 
   set. */
```

## <a name="nx_snmp_object_end_of_mib"></a><span data-ttu-id="d1e56-1054">nx_snmp_object_end_of_mib</span><span class="sxs-lookup"><span data-stu-id="d1e56-1054">nx_snmp_object_end_of_mib</span></span>
<span data-ttu-id="d1e56-1055">MIB sonu değerini ayarla</span><span class="sxs-lookup"><span data-stu-id="d1e56-1055">Set end-of-mib value</span></span> 

### <a name="prototype"></a><span data-ttu-id="d1e56-1056">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-1056">Prototype</span></span>

```c
UINT  nx_snmp_object_end_of_mib(VOID *not_used_ptr, 
                              NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a><span data-ttu-id="d1e56-1057">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-1057">Description</span></span>

<span data-ttu-id="d1e56-1058">Bu hizmet, MıB 'nin sonuna işaret eden bir nesne oluşturur ve genellikle GET veya GETNEXT uygulama geri çağırma yordamından çağırılır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1058">This service creates an object signaling the end of the MIB and is typically called from the GET or GETNEXT application callback routine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-1059">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-1059">Input Parameters</span></span>

- <span data-ttu-id="d1e56-1060">**not_used_ptr** İşaretçi kullanılmadı – NX_NULL olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1060">**not_used_ptr** Pointer not used – should be NX_NULL.</span></span>
- <span data-ttu-id="d1e56-1061">**object_data** Hedef nesne yapısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1061">**object_data** Pointer to destination object structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-1062">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-1062">Return Values</span></span>

- <span data-ttu-id="d1e56-1063">**NX_SUCCESS** (0x00) son MIB nesnesi başarıyla oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1063">**NX_SUCCESS** (0x00) The end-of-mib object has be successfully built.</span></span>
- <span data-ttu-id="d1e56-1064">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d1e56-1064">**NX_PTR_ERROR** (0x07) Invalid input pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-1065">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-1065">Allowed From</span></span>

<span data-ttu-id="d1e56-1066">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-1066">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-1067">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-1067">Example</span></span>

```c
/* Place an end-of-mib value in my_object.  */
status =  nx_snmp_object_end_of_mib(NX_NULL, my_object);

/* If status is NX_SUCCESS, the my_object is now an end-of-mib object. */
```

## <a name="nx_snmp_object_gauge_get"></a><span data-ttu-id="d1e56-1068">nx_snmp_object_gauge_get</span><span class="sxs-lookup"><span data-stu-id="d1e56-1068">nx_snmp_object_gauge_get</span></span>
<span data-ttu-id="d1e56-1069">Ölçer nesnesini Al</span><span class="sxs-lookup"><span data-stu-id="d1e56-1069">Get gauge object</span></span> 

### <a name="prototype"></a><span data-ttu-id="d1e56-1070">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-1070">Prototype</span></span>

```c
UINT  nx_snmp_object_gauge_get(VOID *source_ptr, 
                               NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a><span data-ttu-id="d1e56-1071">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-1071">Description</span></span>

<span data-ttu-id="d1e56-1072">Bu hizmet, kaynak işaretçi tarafından belirtilen adresteki ölçer nesnesini alır ve NetX nesne verileri yapısına koyar.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1072">This service retrieves the gauge object at the address specified by the source pointer and places it in the NetX object data structure.</span></span> <span data-ttu-id="d1e56-1073">Bu yordam genellikle GET veya GETNEXT uygulama geri çağırma yordamından çağırılır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1073">This routine is typically called from the GET or GETNEXT application callback routine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-1074">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-1074">Input Parameters</span></span>

- <span data-ttu-id="d1e56-1075">**source_ptr** Ölçer kaynağı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1075">**source_ptr** Pointer to gauge source.</span></span>
- <span data-ttu-id="d1e56-1076">**object_data** Hedef nesne yapısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1076">**object_data** Pointer to destination object structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-1077">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-1077">Return Values</span></span>

- <span data-ttu-id="d1e56-1078">**NX_SUCCESS** (0x00) ölçer nesnesi başarıyla alındı.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1078">**NX_SUCCESS** (0x00) The gauge object has be successfully retrieved.</span></span>
- <span data-ttu-id="d1e56-1079">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d1e56-1079">**NX_PTR_ERROR** (0x07) Invalid input pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-1080">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-1080">Allowed From</span></span>

<span data-ttu-id="d1e56-1081">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-1081">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-1082">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-1082">Example</span></span>

```c
/* Get the value of ifSpeed (1.3.6.1.2.1.2.2.1.5.0) and place it in my_object
   for return.  */
status =  nx_snmp_object_gauge_get(&ifSpeed, my_object);

/* If status is NX_SUCCESS, the my_object now contains the ifSpeed gauge value. */
```

## <a name="nx_snmp_object_gauge_set"></a><span data-ttu-id="d1e56-1083">nx_snmp_object_gauge_set</span><span class="sxs-lookup"><span data-stu-id="d1e56-1083">nx_snmp_object_gauge_set</span></span>
<span data-ttu-id="d1e56-1084">Ölçer nesnesi ayarla</span><span class="sxs-lookup"><span data-stu-id="d1e56-1084">Set gauge object</span></span> 

### <a name="prototype"></a><span data-ttu-id="d1e56-1085">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-1085">Prototype</span></span>

```c
UINT  nx_snmp_object_gauge_set(VOID *destination_ptr,
                                     NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a><span data-ttu-id="d1e56-1086">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-1086">Description</span></span>

<span data-ttu-id="d1e56-1087">Bu hizmet, hedef işaretçi tarafından belirtilen adresteki ölçerin değerini NetX nesne verileri yapısındaki ölçer değeriyle ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1087">This service sets the gauge at the address specified by the destination pointer with the gauge value in the NetX object data structure.</span></span> <span data-ttu-id="d1e56-1088">Bu yordam genellikle uygulama geri aramasını ayarla yordamından çağırılır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1088">This routine is typically called from the SET application callback routine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-1089">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-1089">Input Parameters</span></span>

- <span data-ttu-id="d1e56-1090">**destination_ptr** Ölçer hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1090">**destination_ptr** Pointer to gauge destination.</span></span>
- <span data-ttu-id="d1e56-1091">**object_data** Ölçer kaynak nesne yapısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1091">**object_data** Pointer to gauge source object structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-1092">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-1092">Return Values</span></span>

- <span data-ttu-id="d1e56-1093">**NX_SUCCESS** (0x00) ölçer nesnesi başarıyla ayarlandı.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1093">**NX_SUCCESS** (0x00) The gauge object has be successfully set.</span></span>
- <span data-ttu-id="d1e56-1094">**NX_SNMP_ERROR_WRONGTYPE** (0x07) geçersiz nesne türü.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1094">**NX_SNMP_ERROR_WRONGTYPE** (0x07) Invalid object type.</span></span>
- <span data-ttu-id="d1e56-1095">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d1e56-1095">**NX_PTR_ERROR** (0x07) Invalid input pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-1096">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-1096">Allowed From</span></span>

<span data-ttu-id="d1e56-1097">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-1097">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-1098">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-1098">Example</span></span>

```c
/* Set the value of “my_gauge” from the gauge value in my_object.  */
status =  nx_snmp_object_gauge_set(&my_gauge, my_object);

/* If status is NX_SUCCESS, the my_gauge now contains the new gauge value. */
```

## <a name="nx_snmp_object_id_get"></a><span data-ttu-id="d1e56-1099">nx_snmp_object_id_get</span><span class="sxs-lookup"><span data-stu-id="d1e56-1099">nx_snmp_object_id_get</span></span>
<span data-ttu-id="d1e56-1100">Nesne kimliğini al</span><span class="sxs-lookup"><span data-stu-id="d1e56-1100">Get object id</span></span> 

### <a name="prototype"></a><span data-ttu-id="d1e56-1101">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-1101">Prototype</span></span>

```c
UINT  nx_snmp_object_id_get(VOID *source_ptr, 
                            NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a><span data-ttu-id="d1e56-1102">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-1102">Description</span></span>

<span data-ttu-id="d1e56-1103">Bu hizmet, kaynak işaretçi tarafından belirtilen adresteki nesne KIMLIĞINI (ASCII SIM gösteriminde) alır ve NetX nesne verileri yapısına koyar.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1103">This service retrieves the object ID (in ASCII SIM notation) at the address specified by the source pointer and places it in the NetX object data structure.</span></span> <span data-ttu-id="d1e56-1104">Bu yordam genellikle GET veya GETNEXT uygulama geri çağırma yordamından çağırılır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1104">This routine is typically called from the GET or GETNEXT application callback routine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-1105">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-1105">Input Parameters</span></span>

- <span data-ttu-id="d1e56-1106">**source_ptr** Nesne KIMLIĞI kaynağı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1106">**source_ptr** Pointer to object ID source.</span></span>
- <span data-ttu-id="d1e56-1107">**object_data** Hedef nesne yapısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1107">**object_data** Pointer to destination object structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-1108">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-1108">Return Values</span></span>

- <span data-ttu-id="d1e56-1109">**NX_SUCCESS** (0x00) nesne kimliği başarıyla alındı.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1109">**NX_SUCCESS** (0x00) The object ID has be successfully retrieved.</span></span>
- <span data-ttu-id="d1e56-1110">**NX_SNMP_ERROR** (0x100) geçersiz nesne uzunluğu</span><span class="sxs-lookup"><span data-stu-id="d1e56-1110">**NX_SNMP_ERROR** (0x100) Invalid length of object</span></span>
- <span data-ttu-id="d1e56-1111">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d1e56-1111">**NX_PTR_ERROR** (0x07) Invalid input pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-1112">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-1112">Allowed From</span></span>

<span data-ttu-id="d1e56-1113">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-1113">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-1114">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-1114">Example</span></span>

```c
/* Get the value of sysObjectID(1.3.6.1.2.1.1.2.0) and place it in my_object
   for return.  */
status =  nx_snmp_object_id_get(&sysObjectID, my_object);

/* If status is NX_SUCCESS, the my_object now contains the sysObjectID value. */
```

## <a name="nx_snmp_object_id_set"></a><span data-ttu-id="d1e56-1115">nx_snmp_object_id_set</span><span class="sxs-lookup"><span data-stu-id="d1e56-1115">nx_snmp_object_id_set</span></span>
<span data-ttu-id="d1e56-1116">Nesne kimliğini ayarla</span><span class="sxs-lookup"><span data-stu-id="d1e56-1116">Set object id</span></span> 

### <a name="prototype"></a><span data-ttu-id="d1e56-1117">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-1117">Prototype</span></span>

```c
UINT  nx_snmp_object_id_set(VOID *destination_ptr, 
                             NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a><span data-ttu-id="d1e56-1118">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-1118">Description</span></span>

<span data-ttu-id="d1e56-1119">Bu hizmet, hedef işaretçi tarafından belirtilen adresteki nesne KIMLIĞINI (ASCII SIM gösteriminde), NetX nesne verileri yapısındaki nesne KIMLIĞIYLE ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1119">This service sets the object ID (in ASCII SIM notation) at the address specified by the destination pointer with the object ID in the NetX object data structure.</span></span> <span data-ttu-id="d1e56-1120">Bu yordam genellikle uygulama geri aramasını ayarla yordamından çağırılır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1120">This routine is typically called from the SET application callback routine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-1121">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-1121">Input Parameters</span></span>

- <span data-ttu-id="d1e56-1122">**destination_ptr** Nesne KIMLIĞI hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1122">**destination_ptr** Pointer to object ID destination.</span></span>
- <span data-ttu-id="d1e56-1123">**object_data** Nesne yapısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1123">**object_data** Pointer to object structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-1124">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-1124">Return Values</span></span>

- <span data-ttu-id="d1e56-1125">**NX_SUCCESS** (0x00) nesne kimliği başarıyla ayarlandı.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1125">**NX_SUCCESS** (0x00) The object ID has been successfully set.</span></span>
- <span data-ttu-id="d1e56-1126">**NX_SNMP_ERROR_WRONGTYPE** (0x07) geçersiz nesne türü.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1126">**NX_SNMP_ERROR_WRONGTYPE** (0x07) Invalid object type.</span></span>
- <span data-ttu-id="d1e56-1127">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d1e56-1127">**NX_PTR_ERROR** (0x07) Invalid input pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-1128">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-1128">Allowed From</span></span>

<span data-ttu-id="d1e56-1129">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-1129">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-1130">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-1130">Example</span></span>

```c
/* Set the string “my_object_id” with the object ID value contained 
   in my_object.  */
status =  nx_snmp_object_id_set(my_object_id, my_object);

/* If status is NX_SUCCESS, the my_object_id now contains the object ID value. */
```

## <a name="nx_snmp_object_integer_get"></a><span data-ttu-id="d1e56-1131">nx_snmp_object_integer_get</span><span class="sxs-lookup"><span data-stu-id="d1e56-1131">nx_snmp_object_integer_get</span></span>
<span data-ttu-id="d1e56-1132">Tamsayı nesnesi Al</span><span class="sxs-lookup"><span data-stu-id="d1e56-1132">Get integer object</span></span> 

### <a name="prototype"></a><span data-ttu-id="d1e56-1133">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-1133">Prototype</span></span>

```c
UINT  nx_snmp_object_integer_get(VOID *source_ptr, 
                                  NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a><span data-ttu-id="d1e56-1134">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-1134">Description</span></span>

<span data-ttu-id="d1e56-1135">Bu hizmet, kaynak işaretçi tarafından belirtilen adresteki tamsayı nesnesini alır ve NetX nesne verileri yapısına koyar.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1135">This service retrieves the integer object at the address specified by the source pointer and places it in the NetX object data structure.</span></span> <span data-ttu-id="d1e56-1136">Bu yordam genellikle GET veya GETNEXT uygulama geri çağırma yordamından çağırılır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1136">This routine is typically called from the GET or GETNEXT application callback routine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-1137">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-1137">Input Parameters</span></span>

- <span data-ttu-id="d1e56-1138">**source_ptr** Tamsayı kaynağı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1138">**source_ptr** Pointer to integer source.</span></span>
- <span data-ttu-id="d1e56-1139">**object_data** Hedef nesne yapısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1139">**object_data** Pointer to destination object structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-1140">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-1140">Return Values</span></span>

- <span data-ttu-id="d1e56-1141">**NX_SUCCESS** (0x00) tamsayı nesnesi başarıyla alındı.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1141">**NX_SUCCESS** (0x00) The integer object has been successfully retrieved.</span></span>
- <span data-ttu-id="d1e56-1142">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d1e56-1142">**NX_PTR_ERROR** (0x07) Invalid input pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-1143">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-1143">Allowed From</span></span>

<span data-ttu-id="d1e56-1144">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-1144">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-1145">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-1145">Example</span></span>

```c
/* Get the value of sysServices (1.3.6.1.2.1.1.7.0) and place it in my_object
   for return.  */
status =  nx_snmp_object_integer_get(&sysServices, my_object);

/* If status is NX_SUCCESS, the my_object now contains the sysServices value. */
```

## <a name="nx_snmp_object_integer_set"></a><span data-ttu-id="d1e56-1146">nx_snmp_object_integer_set</span><span class="sxs-lookup"><span data-stu-id="d1e56-1146">nx_snmp_object_integer_set</span></span>
<span data-ttu-id="d1e56-1147">Tamsayı nesnesini ayarla</span><span class="sxs-lookup"><span data-stu-id="d1e56-1147">Set integer object</span></span> 

### <a name="prototype"></a><span data-ttu-id="d1e56-1148">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-1148">Prototype</span></span>

```c
UINT  nx_snmp_object_integer_set(VOID *destination_ptr,
                                      NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a><span data-ttu-id="d1e56-1149">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-1149">Description</span></span>

<span data-ttu-id="d1e56-1150">Bu hizmet, hedef işaretçi tarafından belirtilen adresteki tamsayıyı NetX nesne verileri yapısındaki tamsayı değeriyle ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1150">This service sets the integer at the address specified by the destination pointer with the integer value in the NetX object data structure.</span></span> <span data-ttu-id="d1e56-1151">Bu yordam genellikle uygulama geri aramasını ayarla yordamından çağırılır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1151">This routine is typically called from the SET application callback routine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-1152">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-1152">Input Parameters</span></span>

- <span data-ttu-id="d1e56-1153">**destination_ptr** Tamsayı hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1153">**destination_ptr** Pointer to integer destination.</span></span>
- <span data-ttu-id="d1e56-1154">**object_data** Tamsayı kaynak nesne yapısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1154">**object_data** Pointer to integer source object structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-1155">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-1155">Return Values</span></span>

- <span data-ttu-id="d1e56-1156">**NX_SUCCESS** (0x00) tamsayı nesnesi başarıyla ayarlandı.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1156">**NX_SUCCESS** (0x00) The integer object has been successfully set.</span></span>
- <span data-ttu-id="d1e56-1157">**NX_SNMP_ERROR_WRONGTYPE** (0x07) geçersiz nesne türü.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1157">**NX_SNMP_ERROR_WRONGTYPE** (0x07) Invalid object type.</span></span>
- <span data-ttu-id="d1e56-1158">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d1e56-1158">**NX_PTR_ERROR** (0x07) Invalid input pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-1159">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-1159">Allowed From</span></span>

<span data-ttu-id="d1e56-1160">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-1160">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-1161">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-1161">Example</span></span>

```c
/* Set the value of ifAdminStatus from the integer value in my_object.  */
status =  nx_snmp_object_integer_set(&ifAdminStatus, my_object);

/* If status is NX_SUCCESS, ifAdnminStatus now contains the new integer value. */
```

## <a name="nx_snmp_object_ip_address_get"></a><span data-ttu-id="d1e56-1162">nx_snmp_object_ip_address_get</span><span class="sxs-lookup"><span data-stu-id="d1e56-1162">nx_snmp_object_ip_address_get</span></span>
<span data-ttu-id="d1e56-1163">IP adresi nesnesi Al (yalnızca IPv4)</span><span class="sxs-lookup"><span data-stu-id="d1e56-1163">Get IP address object (IPv4 only)</span></span>

### <a name="prototype"></a><span data-ttu-id="d1e56-1164">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-1164">Prototype</span></span>

```c
UINT  nx_snmp_object_ip_address_get(VOID *source_ptr,
                                          NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a><span data-ttu-id="d1e56-1165">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-1165">Description</span></span>

<span data-ttu-id="d1e56-1166">Bu hizmet, kaynak işaretçi tarafından belirtilen adresteki IP adresi nesnesini alır ve NetX nesne verileri yapısına koyar.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1166">This service retrieves the IP address object at the address specified by the source pointer and places it in the NetX object data structure.</span></span> <span data-ttu-id="d1e56-1167">Bu yordam genellikle GET veya GETNEXT uygulama geri çağırma yordamından çağırılır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1167">This routine is typically called from the GET or GETNEXT application callback routine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-1168">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-1168">Input Parameters</span></span>

- <span data-ttu-id="d1e56-1169">**source_ptr** IPv4 adres kaynağı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1169">**source_ptr** Pointer to IPv4 address source.</span></span>
- <span data-ttu-id="d1e56-1170">**object_data** Hedef nesne yapısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1170">**object_data** Pointer to destination object structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-1171">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-1171">Return Values</span></span>

- <span data-ttu-id="d1e56-1172">**NX_SUCCESS** (0x00) IP adresi nesnesi başarıyla alındı.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1172">**NX_SUCCESS** (0x00) The IP address object has been successfully retrieved.</span></span>
- <span data-ttu-id="d1e56-1173">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d1e56-1173">**NX_PTR_ERROR** (0x07) Invalid input pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-1174">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-1174">Allowed From</span></span>

<span data-ttu-id="d1e56-1175">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-1175">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-1176">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-1176">Example</span></span>

```c
/* Get the value of ipAdEntAddr (1.3.6.1.2.1.4.20.1.1.0) and place it in my_object
   for return.  */
status =  nx_snmp_object_ip_address_get(&ipAdEntAddr, my_object);

/* If status is NX_SUCCESS, the my_object now contains the ipAdEntAddr value. */
```

## <a name="nx_snmp_object_ipv6_address_get"></a><span data-ttu-id="d1e56-1177">nx_snmp_object_ipv6_address_get</span><span class="sxs-lookup"><span data-stu-id="d1e56-1177">nx_snmp_object_ipv6_address_get</span></span>
<span data-ttu-id="d1e56-1178">IP adresi nesnesi Al (yalnızca IPv6)</span><span class="sxs-lookup"><span data-stu-id="d1e56-1178">Get IP address object (IPv6 only)</span></span>

### <a name="prototype"></a><span data-ttu-id="d1e56-1179">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-1179">Prototype</span></span>

```c
UINT  nx_snmp_object_ipv6_address_get(VOID *source_ptr,
                                          NX_SNMP_OBJECT_DATA 
                                      *object_data);
```

### <a name="description"></a><span data-ttu-id="d1e56-1180">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-1180">Description</span></span>

<span data-ttu-id="d1e56-1181">Bu hizmet, kaynak işaretçi tarafından belirtilen adresteki IPv6 adres nesnesini alır ve NetX nesne verileri yapısına koyar.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1181">This service retrieves the IPv6 address object at the address specified by the source pointer and places it in the NetX object data structure.</span></span>
<span data-ttu-id="d1e56-1182">Bu yordam genellikle GET veya GETNEXT uygulama geri çağırma yordamından çağırılır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1182">This routine is typically called from the GET or GETNEXT application callback routine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-1183">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-1183">Input Parameters</span></span>

- <span data-ttu-id="d1e56-1184">**source_ptr** IPv6 adres kaynağı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1184">**source_ptr** Pointer to IPv6 address source.</span></span>
- <span data-ttu-id="d1e56-1185">**object_data** Hedef nesne yapısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1185">**object_data** Pointer to destination object structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-1186">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-1186">Return Values</span></span>

- <span data-ttu-id="d1e56-1187">**NX_SUCCESS** (0x00) IP adresi nesnesi başarıyla alındı.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1187">**NX_SUCCESS** (0x00) The IP address object has been successfully retrieved.</span></span>
- <span data-ttu-id="d1e56-1188">**NX_SNMP_ERROR_WRONGTYPE** (0x07) yanlış giriş SNMP nesne kodu</span><span class="sxs-lookup"><span data-stu-id="d1e56-1188">**NX_SNMP_ERROR_WRONGTYPE** (0x07) Incorrect input SNMP object code</span></span>
- <span data-ttu-id="d1e56-1189">**NX_NOT_ENABLED** (0x14) IPv6 etkin değil</span><span class="sxs-lookup"><span data-stu-id="d1e56-1189">**NX_NOT_ENABLED** (0x14) IPv6 not enabled</span></span>
- <span data-ttu-id="d1e56-1190">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d1e56-1190">**NX_PTR_ERROR** (0x07) Invalid input pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-1191">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-1191">Allowed From</span></span>

<span data-ttu-id="d1e56-1192">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-1192">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-1193">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-1193">Example</span></span>

```c
/* Get the value of ipAdEntAddr (1.3.6.1.2.1.4.20.1.1.0) and place it in my_object
   for return.  */
status =  nx_snmp_object_ipv6_address_get(&ipAdEntAddr, my_object);

/* If status is NX_SUCCESS, the my_object now contains the ipAdEntAddr value. */
```

## <a name="nx_snmp_object_ip_address_set"></a><span data-ttu-id="d1e56-1194">nx_snmp_object_ip_address_set</span><span class="sxs-lookup"><span data-stu-id="d1e56-1194">nx_snmp_object_ip_address_set</span></span>
<span data-ttu-id="d1e56-1195">IPv4 adresi nesnesi ayarla</span><span class="sxs-lookup"><span data-stu-id="d1e56-1195">Set IPv4 address object</span></span> 

### <a name="prototype"></a><span data-ttu-id="d1e56-1196">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-1196">Prototype</span></span>

```c
UINT  nx_snmp_object_ip_address_set(VOID *destination_ptr, 
                                    NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a><span data-ttu-id="d1e56-1197">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-1197">Description</span></span>

<span data-ttu-id="d1e56-1198">Bu hizmet, hedef işaretçi tarafından belirtilen adresteki IPv4 adresini NetX nesne verileri yapısındaki IP adresiyle ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1198">This service sets the IPv4 address at the address specified by the destination pointer with the IP address in the NetX object data structure.</span></span> <span data-ttu-id="d1e56-1199">Bu yordam genellikle uygulama geri aramasını ayarla yordamından çağırılır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1199">This routine is typically called from the SET application callback routine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-1200">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-1200">Input Parameters</span></span>

- <span data-ttu-id="d1e56-1201">**destination_ptr** Ayarlanacak IP adresi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1201">**destination_ptr** Pointer to IP address to set.</span></span>
- <span data-ttu-id="d1e56-1202">**object_data** IP adresi nesne yapısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1202">**object_data** Pointer to IP address object structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-1203">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-1203">Return Values</span></span>

- <span data-ttu-id="d1e56-1204">**NX_SUCCESS** (0x00) IP adresi nesnesi başarıyla ayarlandı.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1204">**NX_SUCCESS** (0x00) The IP address object has been successfully set.</span></span>
- <span data-ttu-id="d1e56-1205">**NX_SNMP_ERROR_WRONGTYPE** (0x07) geçersiz nesne türü.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1205">**NX_SNMP_ERROR_WRONGTYPE** (0x07) Invalid object type.</span></span>
- <span data-ttu-id="d1e56-1206">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d1e56-1206">**NX_PTR_ERROR** (0x07) Invalid input pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-1207">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-1207">Allowed From</span></span>

<span data-ttu-id="d1e56-1208">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-1208">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-1209">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-1209">Example</span></span>

```c
/* Set the value of atNetworkAddress to the IP address in my_object.  */
status =  nx_snmp_object_ip_address_set(&atNetworkAddress, my_object);

/* If status is NX_SUCCESS, atNetWorkAddress now contains the new IP address. */
```

## <a name="nx_snmp_object_ipv6_address_set"></a><span data-ttu-id="d1e56-1210">nx_snmp_object_ipv6_address_set</span><span class="sxs-lookup"><span data-stu-id="d1e56-1210">nx_snmp_object_ipv6_address_set</span></span>
<span data-ttu-id="d1e56-1211">IPv6 adres nesnesini ayarla</span><span class="sxs-lookup"><span data-stu-id="d1e56-1211">Set IPv6 address object</span></span> 

### <a name="prototype"></a><span data-ttu-id="d1e56-1212">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-1212">Prototype</span></span>

```c
UINT  nx_snmp_object_ipv6_address_set(VOID *destination_ptr, 
                                      NX_SNMP_OBJECT_DATA  
                                      *object_data);
```

### <a name="description"></a><span data-ttu-id="d1e56-1213">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-1213">Description</span></span>

<span data-ttu-id="d1e56-1214">Bu hizmet, hedef işaretçi tarafından belirtilen adresteki IPv6 adresini NetX nesne verileri yapısındaki IP adresiyle ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1214">This service sets the IPv6 address at the address specified by the destination pointer with the IP address in the NetX object data structure.</span></span> <span data-ttu-id="d1e56-1215">Bu yordam genellikle uygulama geri aramasını ayarla yordamından çağırılır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1215">This routine is typically called from the SET application callback routine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-1216">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-1216">Input Parameters</span></span>

- <span data-ttu-id="d1e56-1217">**destination_ptr** Ayarlanacak IP adresi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1217">**destination_ptr** Pointer to IP address to set.</span></span>
- <span data-ttu-id="d1e56-1218">**object_data** IP adresi nesne yapısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1218">**object_data** Pointer to IP address object structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-1219">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-1219">Return Values</span></span>

- <span data-ttu-id="d1e56-1220">**NX_SUCCESS** (0x00) IPv6 adresi başarıyla ayarlandı.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1220">**NX_SUCCESS** (0x00) The IPv6 address has been successfully set.</span></span>
- <span data-ttu-id="d1e56-1221">**NX_SNMP_ERROR_WRONGTYPE** (0x07) geçersiz nesne türü.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1221">**NX_SNMP_ERROR_WRONGTYPE** (0x07) Invalid object type.</span></span>
- <span data-ttu-id="d1e56-1222">**NX_NOT_ENABLED** (0x14) IPv6 etkin değil</span><span class="sxs-lookup"><span data-stu-id="d1e56-1222">**NX_NOT_ENABLED** (0x14) IPv6 not enabled</span></span>
- <span data-ttu-id="d1e56-1223">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d1e56-1223">**NX_PTR_ERROR** (0x07) Invalid input pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-1224">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-1224">Allowed From</span></span>

<span data-ttu-id="d1e56-1225">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-1225">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-1226">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-1226">Example</span></span>

```c
/* Set the value of atNetworkAddress to the IP address in my_object.  */
status =  nx_snmp_object_ipv6_address_set(&atNetworkAddress, my_object);

/* If status is NX_SUCCESS, atNetWorkAddress now contains the new IP address. */
```

## <a name="nx_snmp_object_no_instance"></a><span data-ttu-id="d1e56-1227">nx_snmp_object_no_instance</span><span class="sxs-lookup"><span data-stu-id="d1e56-1227">nx_snmp_object_no_instance</span></span>
<span data-ttu-id="d1e56-1228">Örnek olmayan nesne ayarla</span><span class="sxs-lookup"><span data-stu-id="d1e56-1228">Set no-instance object</span></span> 

### <a name="prototype"></a><span data-ttu-id="d1e56-1229">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-1229">Prototype</span></span>

```c
UINT  nx_snmp_object_no_instance(VOID *not_used_ptr, 
                                 NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a><span data-ttu-id="d1e56-1230">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-1230">Description</span></span>

<span data-ttu-id="d1e56-1231">Bu hizmet, belirtilen nesnenin örneği olmadığını belirten bir nesne sinyali oluşturur ve genellikle GET veya GETNEXT uygulama geri çağırma yordamından çağırılır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1231">This service creates an object signaling that there was no instance of the specified object and is typically called from the GET or GETNEXT application callback routine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-1232">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-1232">Input Parameters</span></span>

- <span data-ttu-id="d1e56-1233">**not_used_ptr** İşaretçi kullanılmadı – NX_NULL olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1233">**not_used_ptr** Pointer not used – should be NX_NULL.</span></span>
- <span data-ttu-id="d1e56-1234">**object_data** Hedef nesne yapısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1234">**object_data** Pointer to destination object structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-1235">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-1235">Return Values</span></span>

- <span data-ttu-id="d1e56-1236">**NX_SUCCESS** (0x00) örnek olmayan nesne başarıyla oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1236">**NX_SUCCESS** (0x00) The no-instance object has been successfully built.</span></span>
- <span data-ttu-id="d1e56-1237">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d1e56-1237">**NX_PTR_ERROR** (0x07) Invalid input pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-1238">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-1238">Allowed From</span></span>

<span data-ttu-id="d1e56-1239">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-1239">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-1240">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-1240">Example</span></span>

```c
/* Place no-instance value in my_object.  */
status =  nx_snmp_object_no_instance(NX_NULL, my_object);

/* If status is NX_SUCCESS, the my_object is now a no-instance object. */
```

## <a name="nx_snmp_object_not_found"></a><span data-ttu-id="d1e56-1241">nx_snmp_object_not_found</span><span class="sxs-lookup"><span data-stu-id="d1e56-1241">nx_snmp_object_not_found</span></span>
<span data-ttu-id="d1e56-1242">Bulunamadı nesnesi ayarla</span><span class="sxs-lookup"><span data-stu-id="d1e56-1242">Set not-found object</span></span> 

### <a name="prototype"></a><span data-ttu-id="d1e56-1243">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-1243">Prototype</span></span>

```c
UINT  nx_snmp_object_not_found(VOID *not_used_ptr, 
                               NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a><span data-ttu-id="d1e56-1244">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-1244">Description</span></span>

<span data-ttu-id="d1e56-1245">Bu hizmet, nesne bulunamadığı ve genellikle GET veya GETNEXT uygulama geri çağırma yordamından çağrılan bir nesne sinyali oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1245">This service creates an object signaling the object was not found and is typically called from the GET or GETNEXT application callback routine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-1246">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-1246">Input Parameters</span></span>

- <span data-ttu-id="d1e56-1247">**not_used_ptr** İşaretçi kullanılmadı – NX_NULL olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1247">**not_used_ptr** Pointer not used – should be NX_NULL.</span></span>
- <span data-ttu-id="d1e56-1248">**object_data** Hedef nesne yapısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1248">**object_data** Pointer to destination object structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-1249">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-1249">Return Values</span></span>

- <span data-ttu-id="d1e56-1250">**NX_SUCCESS** (0x00) olmayan nesne başarıyla oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1250">**NX_SUCCESS** (0x00) The not-found object has been successfully built.</span></span>
- <span data-ttu-id="d1e56-1251">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d1e56-1251">**NX_PTR_ERROR** (0x07) Invalid input pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-1252">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-1252">Allowed From</span></span>

<span data-ttu-id="d1e56-1253">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-1253">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-1254">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-1254">Example</span></span>

```c
/* Place not-found value in my_object.  */
status =  nx_snmp_object_not_found(NX_NULL, my_object);

/* If status is NX_SUCCESS, the my_object is now a not-found object. */
```

## <a name="nx_snmp_object_octet_string_get"></a><span data-ttu-id="d1e56-1255">nx_snmp_object_octet_string_get</span><span class="sxs-lookup"><span data-stu-id="d1e56-1255">nx_snmp_object_octet_string_get</span></span>
<span data-ttu-id="d1e56-1256">Sekizli dize nesnesi Al</span><span class="sxs-lookup"><span data-stu-id="d1e56-1256">Get octet string object</span></span> 

### <a name="prototype"></a><span data-ttu-id="d1e56-1257">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-1257">Prototype</span></span>

```c
UINT  nx_snmp_object_octet_string_get(VOID *source_ptr,
                                            NX_SNMP_OBJECT_DATA *object_data, 
                                      UINT length);
```
### <a name="description"></a><span data-ttu-id="d1e56-1258">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-1258">Description</span></span>

<span data-ttu-id="d1e56-1259">Bu hizmet, kaynak işaretçi tarafından belirtilen adresteki sekizli dizeyi alır ve NetX nesne verileri yapısına koyar.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1259">This service retrieves the octet string at the address specified by the source pointer and places it in the NetX object data structure.</span></span> <span data-ttu-id="d1e56-1260">Bu yordam genellikle GET veya GETNEXT uygulama geri çağırma yordamından çağırılır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1260">This routine is typically called from the GET or GETNEXT application callback routine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-1261">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-1261">Input Parameters</span></span>

- <span data-ttu-id="d1e56-1262">**source_ptr** Sekizli dize kaynağı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1262">**source_ptr** Pointer to octet string source.</span></span>
- <span data-ttu-id="d1e56-1263">**object_data** Hedef nesne yapısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1263">**object_data** Pointer to destination object structure.</span></span>
- <span data-ttu-id="d1e56-1264">**uzunluk** Sekizli dizedeki bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1264">**length** Number of bytes in octet string.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-1265">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-1265">Return Values</span></span>

- <span data-ttu-id="d1e56-1266">**NX_SUCCESS** (0x00) sekizli dize nesnesi başarıyla alındı.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1266">**NX_SUCCESS** (0x00) The octet string object has been successfully retrieved.</span></span>
- <span data-ttu-id="d1e56-1267">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d1e56-1267">**NX_PTR_ERROR** (0x07) Invalid input pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-1268">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-1268">Allowed From</span></span>

<span data-ttu-id="d1e56-1269">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-1269">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-1270">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-1270">Example</span></span>

```c
/* Get the value of the 6-byte ifPhysAddress (1.3.6.1.2.1.2.2.1.6.0) and place 
   it in my_object for return.  */
status =  nx_snmp_object_octet_string_get(ifPhysAddress, my_object, 6);

/* If status is NX_SUCCESS, the my_object now contains the ifPhysAddress value. */
```

## <a name="nx_snmp_object_octet_string_set"></a><span data-ttu-id="d1e56-1271">nx_snmp_object_octet_string_set</span><span class="sxs-lookup"><span data-stu-id="d1e56-1271">nx_snmp_object_octet_string_set</span></span>
<span data-ttu-id="d1e56-1272">Sekizli dize nesnesi ayarla</span><span class="sxs-lookup"><span data-stu-id="d1e56-1272">Set octet string object</span></span> 

### <a name="prototype"></a><span data-ttu-id="d1e56-1273">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-1273">Prototype</span></span>

```c
UINT  nx_snmp_object_octet_string_set(VOID *destination_ptr, 
                                      NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a><span data-ttu-id="d1e56-1274">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-1274">Description</span></span>

<span data-ttu-id="d1e56-1275">Bu hizmet, hedef işaretçi tarafından belirtilen adresteki sekizli dizeyi NetX nesne verileri yapısında sekizli dize olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1275">This service sets the octet string at the address specified by the destination pointer with the octet string in the NetX object data structure.</span></span> <span data-ttu-id="d1e56-1276">Bu yordam genellikle uygulama geri aramasını ayarla yordamından çağırılır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1276">This routine is typically called from the SET application callback routine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-1277">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-1277">Input Parameters</span></span>

- <span data-ttu-id="d1e56-1278">**destination_ptr** Sekizli dize hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1278">**destination_ptr** Pointer to octet string destination.</span></span>
- <span data-ttu-id="d1e56-1279">**object_data** Sekizli dize kaynak nesne yapısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1279">**object_data** Pointer to octet string source object structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-1280">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-1280">Return Values</span></span>

- <span data-ttu-id="d1e56-1281">**NX_SUCCESS** (0x00) sekizli dize nesnesi başarıyla ayarlandı.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1281">**NX_SUCCESS** (0x00) The octet string object has been successfully set.</span></span>
- <span data-ttu-id="d1e56-1282">**NX_SNMP_ERROR_WRONGTYPE** (0x07) geçersiz nesne türü.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1282">**NX_SNMP_ERROR_WRONGTYPE** (0x07) Invalid object type.</span></span>
- <span data-ttu-id="d1e56-1283">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d1e56-1283">**NX_PTR_ERROR** (0x07) Invalid input pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-1284">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-1284">Allowed From</span></span>

<span data-ttu-id="d1e56-1285">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-1285">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-1286">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-1286">Example</span></span>

```c
/* Set the value of sysContact (1.3.6.1.2.1.1.4.0) from the 
   octet string in my_object.  */
status =  nx_snmp_object_octet_string_set(sysContact, my_object);

/* If status is NX_SUCCESS, sysContact now contains the new octet string. */
```

## <a name="nx_snmp_object_string_get"></a><span data-ttu-id="d1e56-1287">nx_snmp_object_string_get</span><span class="sxs-lookup"><span data-stu-id="d1e56-1287">nx_snmp_object_string_get</span></span>
<span data-ttu-id="d1e56-1288">ASCII dize nesnesi Al</span><span class="sxs-lookup"><span data-stu-id="d1e56-1288">Get ASCII string object</span></span> 

### <a name="prototype"></a><span data-ttu-id="d1e56-1289">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-1289">Prototype</span></span>

```c
UINT  nx_snmp_object_string_get(VOID *source_ptr, 
                                NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a><span data-ttu-id="d1e56-1290">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-1290">Description</span></span>

<span data-ttu-id="d1e56-1291">Bu hizmet, kaynak işaretçi tarafından belirtilen adresteki ASCII dizesini alır ve NetX nesne verileri yapısına koyar.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1291">This service retrieves the ASCII string at the address specified by the source pointer and places it in the NetX object data structure.</span></span> <span data-ttu-id="d1e56-1292">Bu yordam genellikle GET veya GETNEXT uygulama geri çağırma yordamından çağırılır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1292">This routine is typically called from the GET or GETNEXT application callback routine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-1293">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-1293">Input Parameters</span></span>

- <span data-ttu-id="d1e56-1294">**source_ptr** ASCII dize kaynağı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1294">**source_ptr** Pointer to ASCII string source.</span></span>
- <span data-ttu-id="d1e56-1295">**object_data** Hedef nesne yapısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1295">**object_data** Pointer to destination object structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-1296">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-1296">Return Values</span></span>

- <span data-ttu-id="d1e56-1297">**NX_SUCCESS** (0x00) ASCII dize nesnesi başarıyla alındı.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1297">**NX_SUCCESS** (0x00) The ASCII string object has been successfully retrieved.</span></span>
- <span data-ttu-id="d1e56-1298">**NX_SNMP_ERROR** (0x100) dize çok büyük</span><span class="sxs-lookup"><span data-stu-id="d1e56-1298">**NX_SNMP_ERROR** (0x100) String is too big</span></span>  
- <span data-ttu-id="d1e56-1299">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d1e56-1299">**NX_PTR_ERROR** (0x07) Invalid input pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-1300">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-1300">Allowed From</span></span>

<span data-ttu-id="d1e56-1301">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-1301">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-1302">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-1302">Example</span></span>

```c
/* Get the value of the sysDescr (1.3.6.1.2.1.1.1.0) and place 
   it in my_object for return.  */
status =  nx_snmp_object_string_get(sysDescr, my_object);

/* If status is NX_SUCCESS, the my_object now contains the sysDescr string. */
```

## <a name="nx_snmp_object_string_set"></a><span data-ttu-id="d1e56-1303">nx_snmp_object_string_set</span><span class="sxs-lookup"><span data-stu-id="d1e56-1303">nx_snmp_object_string_set</span></span>
<span data-ttu-id="d1e56-1304">ASCII dize nesnesi ayarla</span><span class="sxs-lookup"><span data-stu-id="d1e56-1304">Set ASCII string object</span></span> 

### <a name="prototype"></a><span data-ttu-id="d1e56-1305">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-1305">Prototype</span></span>

```c
UINT  nx_snmp_object_string_set(VOID *destination_ptr, 
                                NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a><span data-ttu-id="d1e56-1306">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-1306">Description</span></span>

<span data-ttu-id="d1e56-1307">Bu hizmet, hedef işaretçi tarafından belirtilen adresteki ASCII dizesini NetX nesne verileri yapısında ASCII dizesiyle ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1307">This service sets the ASCII string at the address specified by the destination pointer with the ASCII string in the NetX object data structure.</span></span> <span data-ttu-id="d1e56-1308">Bu yordam genellikle uygulama geri aramasını ayarla yordamından çağırılır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1308">This routine is typically called from the SET application callback routine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-1309">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-1309">Input Parameters</span></span>

- <span data-ttu-id="d1e56-1310">**destination_ptr** ASCII dize hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1310">**destination_ptr** Pointer to ASCII string destination.</span></span>
- <span data-ttu-id="d1e56-1311">**object_data** ASCII dize kaynak nesne yapısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1311">**object_data** Pointer to ASCII string source object structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-1312">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-1312">Return Values</span></span>

- <span data-ttu-id="d1e56-1313">**NX_SUCCESS** (0x00) ASCII dize nesnesi başarıyla ayarlandı.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1313">**NX_SUCCESS** (0x00) The ASCII string object has been successfully set.</span></span>
- <span data-ttu-id="d1e56-1314">**NX_SNMP_ERROR** (0x100) dize çok büyük.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1314">**NX_SNMP_ERROR** (0x100) String too large.</span></span>
- <span data-ttu-id="d1e56-1315">**NX_SNMP_ERROR_BADVALUE** (0x03) dizede geçersiz karakter</span><span class="sxs-lookup"><span data-stu-id="d1e56-1315">**NX_SNMP_ERROR_BADVALUE** (0x03) Invalid character in string</span></span>
- <span data-ttu-id="d1e56-1316">**NX_SNMP_ERROR_WRONGTYPE** (0x07) geçersiz nesne türü.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1316">**NX_SNMP_ERROR_WRONGTYPE** (0x07) Invalid object type.</span></span>
- <span data-ttu-id="d1e56-1317">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d1e56-1317">**NX_PTR_ERROR** (0x07) Invalid input pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-1318">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-1318">Allowed From</span></span>

<span data-ttu-id="d1e56-1319">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-1319">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-1320">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-1320">Example</span></span>

```c
/* Set the value of sysContact (1.3.6.1.2.1.1.4.0) from the 
   ASCII string in my_object.  */
status =  nx_snmp_object_string_set(sysContact, my_object);

/* If status is NX_SUCCESS, sysContact now contains the new ASCII string. */
```

## <a name="nx_snmp_object_timetics_get"></a><span data-ttu-id="d1e56-1321">nx_snmp_object_timetics_get</span><span class="sxs-lookup"><span data-stu-id="d1e56-1321">nx_snmp_object_timetics_get</span></span>
<span data-ttu-id="d1e56-1322">Timetika nesnesini Al</span><span class="sxs-lookup"><span data-stu-id="d1e56-1322">Get timetics object</span></span> 

### <a name="prototype"></a><span data-ttu-id="d1e56-1323">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-1323">Prototype</span></span>

```c
UINT  nx_snmp_object_timetics_get(VOID *source_ptr, 
                                  NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a><span data-ttu-id="d1e56-1324">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-1324">Description</span></span>

<span data-ttu-id="d1e56-1325">Bu hizmet, kaynak işaretçi tarafından belirtilen adresteki zaman kaynaklarını alır ve NetX nesne verileri yapısına koyar.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1325">This service retrieves the timetics at the address specified by the source pointer and places it in the NetX object data structure.</span></span> <span data-ttu-id="d1e56-1326">Bu yordam genellikle GET veya GETNEXT uygulama geri çağırma yordamından çağırılır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1326">This routine is typically called from the GET or GETNEXT application callback routine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-1327">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-1327">Input Parameters</span></span>

- <span data-ttu-id="d1e56-1328">**source_ptr** Timetika kaynağı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1328">**source_ptr** Pointer to timetics source.</span></span>
- <span data-ttu-id="d1e56-1329">**object_data** Hedef nesne yapısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1329">**object_data** Pointer to destination object structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-1330">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-1330">Return Values</span></span>

- <span data-ttu-id="d1e56-1331">**NX_SUCCESS** (0x00) timetika nesnesi başarıyla alındı.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1331">**NX_SUCCESS** (0x00) The timetics object has been successfully retrieved.</span></span>
- <span data-ttu-id="d1e56-1332">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d1e56-1332">**NX_PTR_ERROR** (0x07) Invalid input pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-1333">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-1333">Allowed From</span></span>

<span data-ttu-id="d1e56-1334">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-1334">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-1335">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-1335">Example</span></span>

```c
/* Get the value of the sysUpTime (1.3.6.1.2.1.1.3.0) and place 
   it in my_object for return.  */
status =  nx_snmp_object_timetics_get(sysUpTime, my_object);

/* If status is NX_SUCCESS, the my_object now contains the sysUpTime value. */
```

## <a name="nx_snmp_object_timetics_set"></a><span data-ttu-id="d1e56-1336">nx_snmp_object_timetics_set</span><span class="sxs-lookup"><span data-stu-id="d1e56-1336">nx_snmp_object_timetics_set</span></span>
<span data-ttu-id="d1e56-1337">Timetika nesnesini ayarla</span><span class="sxs-lookup"><span data-stu-id="d1e56-1337">Set timetics object</span></span> 

### <a name="prototype"></a><span data-ttu-id="d1e56-1338">Prototype</span><span class="sxs-lookup"><span data-stu-id="d1e56-1338">Prototype</span></span>

```c
UINT  nx_snmp_object_timetics_set(VOID *destination_ptr, 
                                  NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a><span data-ttu-id="d1e56-1339">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1e56-1339">Description</span></span>

<span data-ttu-id="d1e56-1340">Bu hizmet, hedef işaretçi tarafından belirtilen adresteki timetika değişkenini NetX nesne verileri yapısında zaman dilimlerle ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1340">This service sets the timetics variable at the address specified by the destination pointer with the timetics in the NetX object data structure.</span></span>
<span data-ttu-id="d1e56-1341">Bu yordam genellikle uygulama geri aramasını ayarla yordamından çağırılır.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1341">This routine is typically called from the SET application callback routine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d1e56-1342">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-1342">Input Parameters</span></span>

- <span data-ttu-id="d1e56-1343">**destination_ptr** Timetika hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1343">**destination_ptr** Pointer to timetics destination.</span></span>
- <span data-ttu-id="d1e56-1344">**object_data** Timetika kaynak nesne yapısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1344">**object_data** Pointer to timetics source object structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="d1e56-1345">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d1e56-1345">Return Values</span></span>

- <span data-ttu-id="d1e56-1346">**NX_SUCCESS** (0x00) timetika nesnesi başarıyla ayarlandı.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1346">**NX_SUCCESS** (0x00) The timetics object has been successfully set.</span></span>
- <span data-ttu-id="d1e56-1347">**NX_SNMP_ERROR_WRONGTYPE** (0x07) geçersiz nesne türü.</span><span class="sxs-lookup"><span data-stu-id="d1e56-1347">**NX_SNMP_ERROR_WRONGTYPE** (0x07) Invalid object type.</span></span>
- <span data-ttu-id="d1e56-1348">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d1e56-1348">**NX_PTR_ERROR** (0x07) Invalid input pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d1e56-1349">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d1e56-1349">Allowed From</span></span>

<span data-ttu-id="d1e56-1350">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d1e56-1350">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="d1e56-1351">Örnek</span><span class="sxs-lookup"><span data-stu-id="d1e56-1351">Example</span></span>

```c
/* Set the value of “my_time” from the timetics value in my_object.  */
status =  nx_snmp_object_timetics_set(&my_time, my_object);

/* If status is NX_SUCCESS, my_time now contains the new timetics. */
```