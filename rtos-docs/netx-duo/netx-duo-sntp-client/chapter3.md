---
title: Bölüm 3-Azure RTOS NetX Duo SNTP Istemci hizmetlerinin açıklaması
description: Bu bölüm, tüm NetX Duo SNTP Istemci hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 75b2b878cd084ca1c1cdd1eed4333d303fe32ad6
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825745"
---
# <a name="chapter-3---description-of-azure-rtos-netx-duo-sntp-client-services"></a><span data-ttu-id="bce7a-103">Bölüm 3-Azure RTOS NetX Duo SNTP Istemci hizmetlerinin açıklaması</span><span class="sxs-lookup"><span data-stu-id="bce7a-103">Chapter 3 - Description of Azure RTOS NetX Duo SNTP Client Services</span></span>

<span data-ttu-id="bce7a-104">Bu bölüm, tüm Azure RTOS NetX Duo SNTP Istemci hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="bce7a-104">This chapter contains a description of all Azure RTOS NetX Duo SNTP Client services (listed below) in alphabetic order.</span></span>

<span data-ttu-id="bce7a-105">Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_DISABLE_ERROR_CHECKING** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="bce7a-105">In the “Return Values” section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

- <span data-ttu-id="bce7a-106">**nx_sntp_client_create**: *SNTP istemcisini oluşturma*</span><span class="sxs-lookup"><span data-stu-id="bce7a-106">**nx_sntp_client_create**: *Create the SNTP Client*</span></span>
- <span data-ttu-id="bce7a-107">**nx_sntp_client_delete**: *SNTP istemcisini silme*</span><span class="sxs-lookup"><span data-stu-id="bce7a-107">**nx_sntp_client_delete**: *Delete the SNTP Client*</span></span>
- <span data-ttu-id="bce7a-108">**nx_sntp_client_get_local_time**: *SNTP istemci yerel saati al*</span><span class="sxs-lookup"><span data-stu-id="bce7a-108">**nx_sntp_client_get_local_time**: *Get SNTP Client local time*</span></span>
- <span data-ttu-id="bce7a-109">**nx_sntp_client_get_local_time_extended**: *SNTP istemci yerel saati al*</span><span class="sxs-lookup"><span data-stu-id="bce7a-109">**nx_sntp_client_get_local_time_extended**: *Get SNTP Client local time*</span></span>
- <span data-ttu-id="bce7a-110">**nx_sntp_client_initialize_broadcast**: *istemciyi IPv4 yayını işlemi için başlatın*</span><span class="sxs-lookup"><span data-stu-id="bce7a-110">**nx_sntp_client_initialize_broadcast**: *Initialize Client for IPv4 broadcast operation*</span></span>
- <span data-ttu-id="bce7a-111">**nxd_sntp_client_initialize_broadcast**: *IPv6 veya IPv4 yayın işlemi için istemciyi başlatın*</span><span class="sxs-lookup"><span data-stu-id="bce7a-111">**nxd_sntp_client_initialize_broadcast**: *Initialize Client for IPv6 or IPv4 broadcast operation*</span></span>
- <span data-ttu-id="bce7a-112">**nx_sntp_client_initialize_unicast**: *istemciyi IPv4 tek noktaya yayın işlemi için başlatın*</span><span class="sxs-lookup"><span data-stu-id="bce7a-112">**nx_sntp_client_initialize_unicast**: *Initialize Client for IPv4 unicast operation*</span></span>
- <span data-ttu-id="bce7a-113">**nxd_sntp_client_initialize_unicast**: *Istemciyi IPv4 veya IPv6 tek noktaya yayın işlemi için başlatın*</span><span class="sxs-lookup"><span data-stu-id="bce7a-113">**nxd_sntp_client_initialize_unicast**: *Initialize Client for IPv4 or IPv6 unicast operation*</span></span>
- <span data-ttu-id="bce7a-114">**nx_sntp_client_receiving_udpates**: *istemci şu anda geçerli SNTP güncelleştirmelerini alıyor*</span><span class="sxs-lookup"><span data-stu-id="bce7a-114">**nx_sntp_client_receiving_udpates**: *Client is currently receiving valid SNTP updates*</span></span>
- <span data-ttu-id="bce7a-115">**nx_sntp_client_request_unicast_time**: *doğrudan NTP sunucusuna bir tek noktaya yayın isteği gönderin*</span><span class="sxs-lookup"><span data-stu-id="bce7a-115">**nx_sntp_client_request_unicast_time**: *Send a unicast request directly to the NTP Server*</span></span>
- <span data-ttu-id="bce7a-116">**nx_sntp_client_run_broadcast**: *istemciyi yayın modunda çalıştırın*</span><span class="sxs-lookup"><span data-stu-id="bce7a-116">**nx_sntp_client_run_broadcast**: *Run the Client in broadcast mode*</span></span>
- <span data-ttu-id="bce7a-117">**nx_sntp_client_run_unicast**: *istemciyi tek noktaya yayın modunda çalıştırma*</span><span class="sxs-lookup"><span data-stu-id="bce7a-117">**nx_sntp_client_run_unicast**: *Run the Client in unicast mode*</span></span>
- <span data-ttu-id="bce7a-118">**nx_sntp_client_set_local_time**: *SNTP istemcisinin ilk yerel saatini ayarla*</span><span class="sxs-lookup"><span data-stu-id="bce7a-118">**nx_sntp_client_set_local_time**: *Set SNTP Client initial local time*</span></span>
- <span data-ttu-id="bce7a-119">**nx_sntp_client_set_time_update_notify**: *SNTP güncelleştirme geri aramasını ayarlama*</span><span class="sxs-lookup"><span data-stu-id="bce7a-119">**nx_sntp_client_set_time_update_notify**: *Set the SNTP update callback*</span></span>
- <span data-ttu-id="bce7a-120">**nx_sntp_client_stop**: *SNTP istemci iş parçacığını durdur*</span><span class="sxs-lookup"><span data-stu-id="bce7a-120">**nx_sntp_client_stop**: *Stop the SNTP Client thread*</span></span>
- <span data-ttu-id="bce7a-121">**nx_sntp_client_utility_display_date_and_time**: *NTP süresini saniye cinsinden görüntüle*</span><span class="sxs-lookup"><span data-stu-id="bce7a-121">**nx_sntp_client_utility_display_date_and_time**: *Display NTP time in seconds*</span></span>
- <span data-ttu-id="bce7a-122">**nx_sntp_client_utility_msecs_to_fraction**: *milisaniyeyi NTP kesir bileşenine dönüştürme*</span><span class="sxs-lookup"><span data-stu-id="bce7a-122">**nx_sntp_client_utility_msecs_to_fraction**: *Convert milliseconds to an NTP fraction component*</span></span>
- <span data-ttu-id="bce7a-123">**nx_sntp_client_utility_usecs_to_fraction**: *mikrosaniye 'yi NTP kesir Bileşenine Dönüştür*</span><span class="sxs-lookup"><span data-stu-id="bce7a-123">**nx_sntp_client_utility_usecs_to_fraction**: *Convert microseconds to an NTP fraction component*</span></span>
- <span data-ttu-id="bce7a-124">**nx_sntp_client_utility_fraction_to_usecs**: *NTP kesir bileşenini mikrosaniye olarak dönüştürme*</span><span class="sxs-lookup"><span data-stu-id="bce7a-124">**nx_sntp_client_utility_fraction_to_usecs**: *Convert an NTP fraction component to microseconds*</span></span>


## <a name="nx_sntp_client_create"></a><span data-ttu-id="bce7a-125">nx_sntp_client_create</span><span class="sxs-lookup"><span data-stu-id="bce7a-125">nx_sntp_client_create</span></span>

<span data-ttu-id="bce7a-126">SNTP Istemcisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="bce7a-126">Create an SNTP Client</span></span>

### <a name="prototype"></a><span data-ttu-id="bce7a-127">Prototype</span><span class="sxs-lookup"><span data-stu-id="bce7a-127">Prototype</span></span>

```C
UINT nx_sntp_client_create(NX_SNTP_CLIENT *client_ptr, NX_IP *ip_ptr,  
                                     UINT iface_index, 
                                     NX_PACKET_POOL *packet_pool_ptr, 
UINT (*leap_second_handler)(NX_SNTP_CLIENT *client_ptr, 
                                        UINT indicator), 
UINT (*kiss_of_death_handler)(NX_SNTP_CLIENT *client_ptr, 
                               NX_SNTP_TIME_MESSAGE *server_time_msg),
VOID (random_number_generator)(struct NX_SNTP_CLIENT_STRUCT 
                                *client_ptr, ULONG *rand));

```

### <a name="description"></a><span data-ttu-id="bce7a-128">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bce7a-128">Description</span></span>

<span data-ttu-id="bce7a-129">Bu hizmet bir SNTP Istemci örneği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="bce7a-129">This service creates an SNTP Client instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="bce7a-130">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="bce7a-130">Input Parameters</span></span>

- <span data-ttu-id="bce7a-131">**client_ptr** SNTP Istemci denetim bloğu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="bce7a-131">**client_ptr** Pointer to SNTP Client control block</span></span>

- <span data-ttu-id="bce7a-132">**ip_ptr** Istemci IP örneği işaretçisi</span><span class="sxs-lookup"><span data-stu-id="bce7a-132">**ip_ptr** Pointer to Client IP instance</span></span>

- <span data-ttu-id="bce7a-133">**iface_index** SNTP ağ arabirimine Dizin</span><span class="sxs-lookup"><span data-stu-id="bce7a-133">**iface_index** Index to SNTP network interface</span></span>

- <span data-ttu-id="bce7a-134">**packet_pool_ptr** Istemci paket havuzu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="bce7a-134">**packet_pool_ptr** Pointer to Client packet pool</span></span>

- <span data-ttu-id="bce7a-135">**leap_second_handler** Uygulama yanıtı için geri çağırma, artık saniye</span><span class="sxs-lookup"><span data-stu-id="bce7a-135">**leap_second_handler** Callback for application response to impending leap second</span></span>

- <span data-ttu-id="bce7a-136">**kiss_of_death_handler** Uygulama yanıtı için geri çağırma paketin Kiss 'i alma</span><span class="sxs-lookup"><span data-stu-id="bce7a-136">**kiss_of_death_handler** Callback for application response to receiving Kiss of Death packet</span></span>

- <span data-ttu-id="bce7a-137">**random_number_generator** Rastgele sayı Oluşturucu hizmetine geri çağırma</span><span class="sxs-lookup"><span data-stu-id="bce7a-137">**random_number_generator** Callback to random number generator service</span></span>

### <a name="return-values"></a><span data-ttu-id="bce7a-138">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="bce7a-138">Return Values</span></span>

- <span data-ttu-id="bce7a-139">**NX_SUCCESS** (0x00) Istemci oluşturma başarılı</span><span class="sxs-lookup"><span data-stu-id="bce7a-139">**NX_SUCCESS** (0x00) Successful Client creation</span></span>

- <span data-ttu-id="bce7a-140">**NX_SNTP_INSUFFICIENT_PACKET_PAYLOAD** (0xd2a) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="bce7a-140">**NX_SNTP_INSUFFICIENT_PACKET_PAYLOAD** (0xD2A) Invalid non pointer input</span></span>

- <span data-ttu-id="bce7a-141">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="bce7a-141">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

- <span data-ttu-id="bce7a-142">NX_INVALID_INTERFACE (0x4C) geçersiz ağ arabirimi</span><span class="sxs-lookup"><span data-stu-id="bce7a-142">NX_INVALID_INTERFACE (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="bce7a-143">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="bce7a-143">Allowed From</span></span>

<span data-ttu-id="bce7a-144">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="bce7a-144">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="bce7a-145">Örnek</span><span class="sxs-lookup"><span data-stu-id="bce7a-145">Example</span></span>

```C
/* Create the SNTP Client on the primary interface. */
UINT iface_index = 0;
status =  nx_sntp_client_create(&demo_client, 
                     iface_index, &client_ip, 
&client_packet_pool, leap_second_handler, 
                    kiss_of_death_handler, 
NULL /* no random_number_generator callback */);

/* If status is NX_SUCCESS an SNTP Client instance was successfully
   created.  */

```

## <a name="nx_sntp_client_delete"></a><span data-ttu-id="bce7a-146">nx_sntp_client_delete</span><span class="sxs-lookup"><span data-stu-id="bce7a-146">nx_sntp_client_delete</span></span>

<span data-ttu-id="bce7a-147">Bir SNTP Istemcisini silme</span><span class="sxs-lookup"><span data-stu-id="bce7a-147">Delete an SNTP Client</span></span>

### <a name="prototype"></a><span data-ttu-id="bce7a-148">Prototype</span><span class="sxs-lookup"><span data-stu-id="bce7a-148">Prototype</span></span>

```C
UINT nx_sntp_client_delete(NX_SNTP_CLIENT *client_ptr);
```

### <a name="description"></a><span data-ttu-id="bce7a-149">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bce7a-149">Description</span></span>

<span data-ttu-id="bce7a-150">Bu hizmet, bir SNTP Istemci örneğini siler.</span><span class="sxs-lookup"><span data-stu-id="bce7a-150">This service deletes an SNTP Client instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="bce7a-151">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="bce7a-151">Input Parameters</span></span>

- <span data-ttu-id="bce7a-152">**client_ptr** SNTP Istemci denetim bloğu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="bce7a-152">**client_ptr** Pointer to SNTP Client control block</span></span>

### <a name="return-values"></a><span data-ttu-id="bce7a-153">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="bce7a-153">Return Values</span></span>

- <span data-ttu-id="bce7a-154">**NX_SUCCESS** (0x00) Istemci oluşturma başarılı</span><span class="sxs-lookup"><span data-stu-id="bce7a-154">**NX_SUCCESS** (0x00) Successful Client creation</span></span>

- <span data-ttu-id="bce7a-155">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="bce7a-155">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

- <span data-ttu-id="bce7a-156">NX_CALLER_ERROR (0x11) geçersiz hizmet çağıranı</span><span class="sxs-lookup"><span data-stu-id="bce7a-156">NX_CALLER_ERROR (0x11) Invalid caller of service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="bce7a-157">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="bce7a-157">Allowed From</span></span>

<span data-ttu-id="bce7a-158">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="bce7a-158">Threads</span></span>

### <a name="example"></a><span data-ttu-id="bce7a-159">Örnek</span><span class="sxs-lookup"><span data-stu-id="bce7a-159">Example</span></span>

```C
/* Delete the SNTP Client. */
status =  nx_sntp_client_delete(&demo_client);

/* If status is NX_SUCCESS an SNTP Client 
   instance was successfully deleted.  */

```

## <a name="nx_sntp_client_get_local_time"></a><span data-ttu-id="bce7a-160">nx_sntp_client_get_local_time</span><span class="sxs-lookup"><span data-stu-id="bce7a-160">nx_sntp_client_get_local_time</span></span>

<span data-ttu-id="bce7a-161">SNTP Istemci yerel saatini al</span><span class="sxs-lookup"><span data-stu-id="bce7a-161">Get the SNTP Client local time</span></span>

### <a name="prototype"></a><span data-ttu-id="bce7a-162">Prototype</span><span class="sxs-lookup"><span data-stu-id="bce7a-162">Prototype</span></span>

```C
UINT nx_sntp_client_get_local_time(NX_SNTP_CLIENT *client_ptr , 
                                                ULONG *seconds, 
                                                ULONG *fraction, 
                                                CHAR *buffer);

```

### <a name="description"></a><span data-ttu-id="bce7a-163">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bce7a-163">Description</span></span>

<span data-ttu-id="bce7a-164">Bu hizmet, verileri dize ileti biçiminde almak için bir seçenek arabellek işaretçisi girişi ile SNTP Istemci yerel saatini alır.</span><span class="sxs-lookup"><span data-stu-id="bce7a-164">This service gets the SNTP Client local time with an option buffer pointer input to receive the data in string message format.</span></span>

<span data-ttu-id="bce7a-165">Bu hizmet kullanımdan kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="bce7a-165">This service is deprecated.</span></span> <span data-ttu-id="bce7a-166">Geliştiricilerin *nx_sntp_client_get_local_time_extended*() uygulamasına geçirilmesi önerilir.</span><span class="sxs-lookup"><span data-stu-id="bce7a-166">Developers are encouraged to migrate to *nx_sntp_client_get_local_time_extended*().</span></span>

### <a name="input-parameters"></a><span data-ttu-id="bce7a-167">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="bce7a-167">Input Parameters</span></span>

- <span data-ttu-id="bce7a-168">**client_ptr** SNTP Istemci denetim bloğu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="bce7a-168">**client_ptr** Pointer to SNTP Client control block</span></span>

- <span data-ttu-id="bce7a-169">**saniyeler** Yerel saat/saniye işaretçisi</span><span class="sxs-lookup"><span data-stu-id="bce7a-169">**seconds** Pointer to local time seconds</span></span>

- <span data-ttu-id="bce7a-170">**kesir** Yerel zaman kesir bileşeni</span><span class="sxs-lookup"><span data-stu-id="bce7a-170">**fraction** Local time fraction component</span></span>

- <span data-ttu-id="bce7a-171">**arabellek** Zaman verilerini yazmak için arabellek işaretçisi</span><span class="sxs-lookup"><span data-stu-id="bce7a-171">**buffer** Pointer to buffer to write time data</span></span>

### <a name="return-values"></a><span data-ttu-id="bce7a-172">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="bce7a-172">Return Values</span></span>

- <span data-ttu-id="bce7a-173">**NX_SUCCESS** (0x00) Istemci oluşturma başarılı</span><span class="sxs-lookup"><span data-stu-id="bce7a-173">**NX_SUCCESS** (0x00) Successful Client creation</span></span>

- <span data-ttu-id="bce7a-174">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="bce7a-174">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

- <span data-ttu-id="bce7a-175">NX_CALLER_ERROR (0x11) geçersiz hizmet çağıranı</span><span class="sxs-lookup"><span data-stu-id="bce7a-175">NX_CALLER_ERROR (0x11) Invalid caller of service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="bce7a-176">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="bce7a-176">Allowed From</span></span>

<span data-ttu-id="bce7a-177">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="bce7a-177">Threads</span></span>

### <a name="example"></a><span data-ttu-id="bce7a-178">Örnek</span><span class="sxs-lookup"><span data-stu-id="bce7a-178">Example</span></span>

```C
/* Get the SNTP Client local time without the 
   string message option. */

ULONG base_seconds;
ULONG base_fraction;

status =  nx_sntp_client_get_local_time(&demo_client, 
                                       &base_seconds, 
                                       &base_fraction, 
                                       NX_NULL);
/* If status is NX_SUCCESS an SNTP Client time was successfully
   retrieved.  */

```

## <a name="nx_sntp_client_get_local_time_extended"></a><span data-ttu-id="bce7a-179">nx_sntp_client_get_local_time_extended</span><span class="sxs-lookup"><span data-stu-id="bce7a-179">nx_sntp_client_get_local_time_extended</span></span>

<span data-ttu-id="bce7a-180">Genişletilmiş SNTP Istemcisi yerel saatini al</span><span class="sxs-lookup"><span data-stu-id="bce7a-180">Get the extended SNTP Client local time</span></span>

### <a name="prototype"></a><span data-ttu-id="bce7a-181">Prototype</span><span class="sxs-lookup"><span data-stu-id="bce7a-181">Prototype</span></span>

```C
UINT nx_sntp_client_get_local_time_extended(
                 NX_SNTP_CLIENT *client_ptr,
                 ULONG *seconds, 
                 ULONG *fraction, 
                 CHAR *buffer
                 UINT buffer_size);

```

### <a name="description"></a><span data-ttu-id="bce7a-182">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bce7a-182">Description</span></span>

<span data-ttu-id="bce7a-183">Bu hizmet, verileri dize ileti biçiminde almak için bir seçenek arabellek işaretçisi girişi ile genişletilmiş SNTP Istemci yerel saatini alır.</span><span class="sxs-lookup"><span data-stu-id="bce7a-183">This service gets the extended SNTP Client local time with an option buffer pointer input to receive the data in string message format.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="bce7a-184">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="bce7a-184">Input Parameters</span></span>

- <span data-ttu-id="bce7a-185">**client_ptr** SNTP Istemci denetim bloğu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="bce7a-185">**client_ptr** Pointer to SNTP Client control block</span></span>

- <span data-ttu-id="bce7a-186">**saniyeler** Yerel saat/saniye işaretçisi</span><span class="sxs-lookup"><span data-stu-id="bce7a-186">**seconds** Pointer to local time seconds</span></span>

- <span data-ttu-id="bce7a-187">**kesir** Kesir bileşeni işaretçisi</span><span class="sxs-lookup"><span data-stu-id="bce7a-187">**fraction** Pointer to fraction component</span></span>

- <span data-ttu-id="bce7a-188">**arabellek** Zaman verilerini yazmak için arabellek işaretçisi</span><span class="sxs-lookup"><span data-stu-id="bce7a-188">**buffer** Pointer to buffer to write time data</span></span>

- <span data-ttu-id="bce7a-189">**Buffer_size** Arabellek uzunluğu</span><span class="sxs-lookup"><span data-stu-id="bce7a-189">**buffer_size** Length of buffer</span></span>

### <a name="return-values"></a><span data-ttu-id="bce7a-190">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="bce7a-190">Return Values</span></span>

- <span data-ttu-id="bce7a-191">**NX_SUCCESS** (0x00) Istemci oluşturma başarılı</span><span class="sxs-lookup"><span data-stu-id="bce7a-191">**NX_SUCCESS** (0x00) Successful Client creation</span></span>

- <span data-ttu-id="bce7a-192">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="bce7a-192">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

- <span data-ttu-id="bce7a-193">NX_CALLER_ERROR (0x11) geçersiz hizmet çağıranı</span><span class="sxs-lookup"><span data-stu-id="bce7a-193">NX_CALLER_ERROR (0x11) Invalid caller of service</span></span>

- <span data-ttu-id="bce7a-194">NX_SIZE_ERROR (0x09) denetim buffer_size başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="bce7a-194">NX_SIZE_ERROR (0x09) Check buffer_size fail</span></span>

### <a name="allowed-from"></a><span data-ttu-id="bce7a-195">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="bce7a-195">Allowed From</span></span>

<span data-ttu-id="bce7a-196">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="bce7a-196">Threads</span></span>

### <a name="example"></a><span data-ttu-id="bce7a-197">Örnek</span><span class="sxs-lookup"><span data-stu-id="bce7a-197">Example</span></span>

```C
/* Get the SNTP Client local time without the 
   string message option. */

#define BUFSIZE 50

ULONG seconds;
ULONG fraction;
CHAR  buffer[BUFSIZE];

status =  nx_sntp_client_get_local_time_extended(&demo_client, 
                                                &seconds, 
                                                &fraction, 
                                                buffer, 
                                                BUFSIZE);

/* If status is NX_SUCCESS an SNTP Client 
   time was successfully retrieved.  */

```

## <a name="nx_sntp_client_initialize_broadcast"></a><span data-ttu-id="bce7a-198">nx_sntp_client_initialize_broadcast</span><span class="sxs-lookup"><span data-stu-id="bce7a-198">nx_sntp_client_initialize_broadcast</span></span>

<span data-ttu-id="bce7a-199">Yayın için Istemciyi başlatma işlemi</span><span class="sxs-lookup"><span data-stu-id="bce7a-199">Initialize the Client for broadcast operation</span></span>

### <a name="prototype"></a><span data-ttu-id="bce7a-200">Prototype</span><span class="sxs-lookup"><span data-stu-id="bce7a-200">Prototype</span></span>

```C
UINT nx_sntp_client_initialize_broadcast(NX_SNTP_CLIENT *client_ptr,
                                    ULONG multicast_server_address, 
                                    ULONG broadcast_time_servers);


```

### <a name="description"></a><span data-ttu-id="bce7a-201">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bce7a-201">Description</span></span>

<span data-ttu-id="bce7a-202">Bu hizmet, SNTP sunucu IP adresini ayarlayarak ve SNTP başlangıç parametrelerini ve zaman aşımlarını başlatarak, yayın için Istemciyi başlatır.</span><span class="sxs-lookup"><span data-stu-id="bce7a-202">This service initializes the Client for broadcast operation by setting the the SNTP Server IP address and initializing SNTP startup parameters and timeouts.</span></span> <span data-ttu-id="bce7a-203">Hem çok noktaya yayın hem de yayın adresleri null değilse, çok noktaya yayın adresi seçilir.</span><span class="sxs-lookup"><span data-stu-id="bce7a-203">If both multicast and broadcast addresses are non-null, the multicast address is selected.</span></span> <span data-ttu-id="bce7a-204">Her iki adres null ise bir hata döndürülür.</span><span class="sxs-lookup"><span data-stu-id="bce7a-204">If both addresses are null an error is returned.</span></span> <span data-ttu-id="bce7a-205">Bu, yalnızca IPv4 sunucu adreslerini destekler.</span><span class="sxs-lookup"><span data-stu-id="bce7a-205">Note this supports IPv4 server addresses only.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="bce7a-206">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="bce7a-206">Input Parameters</span></span>

- <span data-ttu-id="bce7a-207">**client_ptr** SNTP Istemci denetim bloğu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="bce7a-207">**client_ptr** Pointer to SNTP Client control block</span></span>

- <span data-ttu-id="bce7a-208">**multicast_server_address** SNTP çok noktaya yayın adresi</span><span class="sxs-lookup"><span data-stu-id="bce7a-208">**multicast_server_address** SNTP multicast address</span></span>

- <span data-ttu-id="bce7a-209">**broadcast_time_server** SNTP sunucusu yayın adresi</span><span class="sxs-lookup"><span data-stu-id="bce7a-209">**broadcast_time_server** SNTP server broadcast address</span></span>

### <a name="return-values"></a><span data-ttu-id="bce7a-210">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="bce7a-210">Return Values</span></span>

- <span data-ttu-id="bce7a-211">**NX_SUCCESS** (0x00) Istemci oluşturma başarılı</span><span class="sxs-lookup"><span data-stu-id="bce7a-211">**NX_SUCCESS** (0x00) Successful Client Creation</span></span>

- <span data-ttu-id="bce7a-212">**NX_INVALID_PARAMETERS** (0x4D) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="bce7a-212">**NX_INVALID_PARAMETERS** (0x4D) Invalid non pointer input</span></span>

- <span data-ttu-id="bce7a-213">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="bce7a-213">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

- <span data-ttu-id="bce7a-214">NX_CALLER_ERROR (0x11) geçersiz hizmet çağıranı</span><span class="sxs-lookup"><span data-stu-id="bce7a-214">NX_CALLER_ERROR (0x11) Invalid caller of service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="bce7a-215">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="bce7a-215">Allowed From</span></span>

<span data-ttu-id="bce7a-216">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="bce7a-216">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="bce7a-217">Örnek</span><span class="sxs-lookup"><span data-stu-id="bce7a-217">Example</span></span>

```C
/* Initialize the client for broadcast operation.  */
status =  nx_sntp_client_initialize_broadcast(client_ptr,0x0,
                            NX_NULL, IP_ADDRESS(192,2,2,255);

/* If status is NX_SUCCESS the Client 
   was successfully initialized.  */

```

## <a name="nxd_sntp_client_initialize_broadcast"></a><span data-ttu-id="bce7a-218">nxd_sntp_client_initialize_broadcast</span><span class="sxs-lookup"><span data-stu-id="bce7a-218">nxd_sntp_client_initialize_broadcast</span></span>

<span data-ttu-id="bce7a-219">IPv4 veya IPv6 yayın işlemi için Istemciyi başlatma</span><span class="sxs-lookup"><span data-stu-id="bce7a-219">Initialize the Client for IPv4 or IPv6 broadcast operation</span></span>

### <a name="prototype"></a><span data-ttu-id="bce7a-220">Prototype</span><span class="sxs-lookup"><span data-stu-id="bce7a-220">Prototype</span></span>

```C
UINT nxd_sntp_client_initialize_broadcast(NX_SNTP_CLIENT *client_ptr,
                            NXD_ADDRESS *multicast_server_address, 
                            NXD_ADDRESS *broadcast_server_address);

```

### <a name="description"></a><span data-ttu-id="bce7a-221">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bce7a-221">Description</span></span>

<span data-ttu-id="bce7a-222">Bu hizmet, SNTP sunucu IP adresini ayarlayıp SNTP başlangıç parametrelerini ve zaman aşımlarını başlatarak yayın için Istemciyi başlatır.</span><span class="sxs-lookup"><span data-stu-id="bce7a-222">This service initializes the Client for broadcast operation by setting up the SNTP Server IP address and initializing SNTP startup parameters and timeouts.</span></span> <span data-ttu-id="bce7a-223">Hem yayın hem çok noktaya yayın adres işaretçileri null değilse, çok noktaya yayın adresi seçilir.</span><span class="sxs-lookup"><span data-stu-id="bce7a-223">If both broadcast and multicast address pointers are non null, the multicast address is selected.</span></span> <span data-ttu-id="bce7a-224">Her iki adres işaretçisi de null ise bir hata döndürülür.</span><span class="sxs-lookup"><span data-stu-id="bce7a-224">If both address pointers are null, an error is returned.</span></span> <span data-ttu-id="bce7a-225">Bu, hem IPv4 hem de IPv6 adres türlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="bce7a-225">This supports both IPv4 and IPv6 address types.</span></span> <span data-ttu-id="bce7a-226">IPv6 yayını desteklemez, bu nedenle yayın adresi işaretçisi IPv6 olarak ayarlanır, bir hata döndürülür.</span><span class="sxs-lookup"><span data-stu-id="bce7a-226">Note that IPv6 does not support broadcast, so the broadcast address pointer is set to IPv6, an error is returned.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="bce7a-227">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="bce7a-227">Input Parameters</span></span>

- <span data-ttu-id="bce7a-228">**client_ptr** SNTP Istemci denetim bloğu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="bce7a-228">**client_ptr** Pointer to SNTP Client control block</span></span>

- <span data-ttu-id="bce7a-229">**multicast_server_address** SNTP sunucu çok noktaya yayın adresi</span><span class="sxs-lookup"><span data-stu-id="bce7a-229">**multicast_server_address** SNTP server multicast address</span></span>

- <span data-ttu-id="bce7a-230">**broadcast_server_address** SNTP sunucusu yayın adresi</span><span class="sxs-lookup"><span data-stu-id="bce7a-230">**broadcast_server_address** SNTP server broadcast address</span></span>

### <a name="return-values"></a><span data-ttu-id="bce7a-231">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="bce7a-231">Return Values</span></span>

- <span data-ttu-id="bce7a-232">**NX_SUCCESS** (0x00) istemci başarıyla başlatıldı</span><span class="sxs-lookup"><span data-stu-id="bce7a-232">**NX_SUCCESS** (0x00) Client successfully initialized</span></span>

- <span data-ttu-id="bce7a-233">NX_SNTP_PARAM_ERROR (0xD0D) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="bce7a-233">NX_SNTP_PARAM_ERROR (0xD0D) Invalid non pointer input</span></span>

- <span data-ttu-id="bce7a-234">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="bce7a-234">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

- <span data-ttu-id="bce7a-235">NX_CALLER_ERROR (0x11) geçersiz hizmet çağıranı</span><span class="sxs-lookup"><span data-stu-id="bce7a-235">NX_CALLER_ERROR (0x11) Invalid caller of service</span></span>


### <a name="allowed-from"></a><span data-ttu-id="bce7a-236">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="bce7a-236">Allowed From</span></span>

<span data-ttu-id="bce7a-237">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="bce7a-237">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="bce7a-238">Örnek</span><span class="sxs-lookup"><span data-stu-id="bce7a-238">Example</span></span>

```C
/* Initialize the client for broadcast operation.  */
NXD_ADDRESS broadcast_server;

Broadcast_server.nxd_ip_address = NX_IP_VERSION_V6;
Broadcast_server.nxd_ip_address.v6[0] = 0x20010db1;
Broadcast_server.nxd_ip_address.v6[1] = 0x0f101;
Broadcast_server.nxd_ip_address.v6[2] = 0x0;
Broadcast_server.nxd_ip_address.v6[3] = 0x101;

status =  nxd_sntp_client_initialize_broadcast(client_ptr,0x0,
                                  NX_NULL, &broadcast_server)


/* If status is NX_SUCCESS the Client 
   was successfully initialized.  */

```

## <a name="nx_sntp_client_initialize_unicast"></a><span data-ttu-id="bce7a-239">nx_sntp_client_initialize_unicast</span><span class="sxs-lookup"><span data-stu-id="bce7a-239">nx_sntp_client_initialize_unicast</span></span>

<span data-ttu-id="bce7a-240">Tek noktaya yayın içinde çalışacak SNTP Istemcisini ayarlama</span><span class="sxs-lookup"><span data-stu-id="bce7a-240">Set up the SNTP Client to run in unicast</span></span>

### <a name="prototype"></a><span data-ttu-id="bce7a-241">Prototype</span><span class="sxs-lookup"><span data-stu-id="bce7a-241">Prototype</span></span>

```C
UINT nx_sntp_client_initialize_unicast(NX_SNTP_CLIENT * client_ptr, 
                                        ULONG unicast_time_server);

```
### <a name="description"></a><span data-ttu-id="bce7a-242">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bce7a-242">Description</span></span>

<span data-ttu-id="bce7a-243">Bu hizmet, SNTP sunucu IP adresini ayarlayarak ve SNTP başlangıç parametrelerini ve zaman aşımlarını başlatarak tek noktaya yayın işlemi için Istemciyi başlatır.</span><span class="sxs-lookup"><span data-stu-id="bce7a-243">This service initializes the Client for unicast operation by setting the SNTP Server IP address and initializing SNTP startup parameters and timeouts.</span></span> <span data-ttu-id="bce7a-244">Bu, yalnızca IPv4 sunucu adreslerini destekler.</span><span class="sxs-lookup"><span data-stu-id="bce7a-244">Note this supports IPv4 server addresses only.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="bce7a-245">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="bce7a-245">Input Parameters</span></span>

- <span data-ttu-id="bce7a-246">**client_ptr** SNTP Istemci denetim bloğu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="bce7a-246">**client_ptr** Pointer to SNTP Client control block</span></span>

- <span data-ttu-id="bce7a-247">**unicast_time_server** SNTP sunucu IP adresi</span><span class="sxs-lookup"><span data-stu-id="bce7a-247">**unicast_time_server** SNTP server IP address</span></span>

### <a name="return-values"></a><span data-ttu-id="bce7a-248">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="bce7a-248">Return Values</span></span>

- <span data-ttu-id="bce7a-249">**NX_SUCCESS** (0x00) istemci başarıyla başlatıldı</span><span class="sxs-lookup"><span data-stu-id="bce7a-249">**NX_SUCCESS** (0x00) Client successfully initialized</span></span>

- <span data-ttu-id="bce7a-250">NX_INVALID_PARAMETERS (0x4D) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="bce7a-250">NX_INVALID_PARAMETERS (0x4D) Invalid non pointer input</span></span>

- <span data-ttu-id="bce7a-251">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="bce7a-251">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

- <span data-ttu-id="bce7a-252">NX_CALLER_ERROR (0x11) geçersiz hizmet çağıranı</span><span class="sxs-lookup"><span data-stu-id="bce7a-252">NX_CALLER_ERROR (0x11) Invalid caller of service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="bce7a-253">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="bce7a-253">Allowed From</span></span>

<span data-ttu-id="bce7a-254">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="bce7a-254">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="bce7a-255">Örnek</span><span class="sxs-lookup"><span data-stu-id="bce7a-255">Example</span></span>

```C
/* Initialize the Client for unicast operation.  */
status =  nx_sntp_client_initialize_unicast(&client_ptr, 
                                 IP_ADDRESS(192,2,2,1));


/* If status is NX_SUCCESS the Client 
   is initialized for unicast operation.  */

```


## <a name="nxd_sntp_client_initialize_unicast"></a><span data-ttu-id="bce7a-256">nxd_sntp_client_initialize_unicast</span><span class="sxs-lookup"><span data-stu-id="bce7a-256">nxd_sntp_client_initialize_unicast</span></span>

<span data-ttu-id="bce7a-257">SNTP Istemcisini IPv4 veya IPv6 tek noktaya yayın içinde çalışacak şekilde ayarlama</span><span class="sxs-lookup"><span data-stu-id="bce7a-257">Set up the SNTP Client to run in IPv4 or IPv6 unicast</span></span>

### <a name="prototype"></a><span data-ttu-id="bce7a-258">Prototype</span><span class="sxs-lookup"><span data-stu-id="bce7a-258">Prototype</span></span>

```C
UINT nxd_sntp_client_initialize_unicast(NX_SNTP_CLIENT * client_ptr, 
                                  NXD_ADDRESS *unicast_time_server);

```

### <a name="description"></a><span data-ttu-id="bce7a-259">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bce7a-259">Description</span></span>

<span data-ttu-id="bce7a-260">Bu hizmet, SNTP sunucu IP adresini ayarlayıp SNTP başlangıç parametrelerini ve zaman aşımlarını başlatarak tek noktaya yayın işlemi için Istemciyi başlatır.</span><span class="sxs-lookup"><span data-stu-id="bce7a-260">This service initializes the Client for unicast operation by setting up the SNTP Server IP address and initializing SNTP startup parameters and timeouts.</span></span> <span data-ttu-id="bce7a-261">Bu, hem IPv4 hem de IPv6 adres türlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="bce7a-261">This supports both IPv4 and IPv6 address types.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="bce7a-262">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="bce7a-262">Input Parameters</span></span>

- <span data-ttu-id="bce7a-263">**client_ptr** SNTP Istemci denetim bloğu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="bce7a-263">**client_ptr** Pointer to SNTP Client control block</span></span>

- <span data-ttu-id="bce7a-264">**unicast_time_server** SNTP sunucu IP adresi</span><span class="sxs-lookup"><span data-stu-id="bce7a-264">**unicast_time_server** SNTP server IP address</span></span>

### <a name="return-values"></a><span data-ttu-id="bce7a-265">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="bce7a-265">Return Values</span></span>

- <span data-ttu-id="bce7a-266">**NX_SUCCESS** (0x00) istemci başarıyla başlatıldı</span><span class="sxs-lookup"><span data-stu-id="bce7a-266">**NX_SUCCESS** (0x00) Client successfully initialized</span></span>

- <span data-ttu-id="bce7a-267">NX_INVALID_PARAMETERS (0x4D) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="bce7a-267">NX_INVALID_PARAMETERS (0x4D) Invalid non pointer input</span></span>

- <span data-ttu-id="bce7a-268">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="bce7a-268">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

- <span data-ttu-id="bce7a-269">NX_CALLER_ERROR (0x11) geçersiz hizmet çağıranı</span><span class="sxs-lookup"><span data-stu-id="bce7a-269">NX_CALLER_ERROR (0x11) Invalid caller of service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="bce7a-270">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="bce7a-270">Allowed From</span></span>

<span data-ttu-id="bce7a-271">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="bce7a-271">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="bce7a-272">Örnek</span><span class="sxs-lookup"><span data-stu-id="bce7a-272">Example</span></span>

```C
/* Initialize the Client for unicast operation.  */
NXD_ADDRESS unicast_server;

unicast _server.nxd_ip_address = NX_IP_VERSION_V6;
unicast _server.nxd_ip_address.v6[0] = 0x20010db1;
unicast _server.nxd_ip_address.v6[1] = 0x0f101;
unicast _server.nxd_ip_address.v6[2] = 0x0;
unicast _server.nxd_ip_address.v6[3] = 0x101;

status =  nxd_sntp_client_initialize_unicast(&client_ptr, 
                                        *unicast_server); 


/* If status is NX_SUCCESS the Client 
   is initialized for unicast operation.  */

```

## <a name="nx_sntp_client_receiving_updates"></a><span data-ttu-id="bce7a-273">nx_sntp_client_receiving_updates</span><span class="sxs-lookup"><span data-stu-id="bce7a-273">nx_sntp_client_receiving_updates</span></span>

<span data-ttu-id="bce7a-274">Istemcinin geçerli güncelleştirmeleri aldığını belirtin</span><span class="sxs-lookup"><span data-stu-id="bce7a-274">Indicate if Client is receiving valid updates</span></span>

### <a name="prototype"></a><span data-ttu-id="bce7a-275">Prototype</span><span class="sxs-lookup"><span data-stu-id="bce7a-275">Prototype</span></span>

```C
UINT nx_sntp_client_receiving_updates(NX_SNTP_CLIENT *client_ptr, 
                                           UINT *receive_status);

```

### <a name="description"></a><span data-ttu-id="bce7a-276">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bce7a-276">Description</span></span>

<span data-ttu-id="bce7a-277">Bu hizmet, Istemcinin geçerli SNTP güncelleştirmelerini alıp almadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="bce7a-277">This service indicates if the Client is receiving valid SNTP updates.</span></span> <span data-ttu-id="bce7a-278">En uzun süre geçerli bir güncelleştirme olmadan veya birbirini izleyen geçersiz güncelleştirmeler için sınır aşıldıysa, alma durumu false olarak döndürülür.</span><span class="sxs-lookup"><span data-stu-id="bce7a-278">If the maximum time lapse without a valid update or limit on consecutive invalid updates is exceeded, the receive status is returned as false.</span></span> <span data-ttu-id="bce7a-279">SNTP Istemcisinin hala çalıştığını ve uygulamanın başka bir tek noktaya yayın veya yayın/çok noktaya yayın sunucusu ile SNTP Istemcisini yeniden başlatmasını isterse *nx_sntp_client_stop* HIZMETINI kullanarak SNTP istemcisini durdurması gerekir, başka bir sunucu ile başlatma hizmetlerinden birini kullanarak istemciyi yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="bce7a-279">Note that the SNTP Client is still running and if the application wishes to restart the SNTP Client with another unicast or broadcast/multicast server it must stop the SNTP Client using the *nx_sntp_client_stop* service, reinitialize the Client using one of the initialize services with another server.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="bce7a-280">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="bce7a-280">Input Parameters</span></span>

- <span data-ttu-id="bce7a-281">**client_ptr** SNTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="bce7a-281">**client_ptr** Pointer to SNTP Client control block.</span></span>

- <span data-ttu-id="bce7a-282">**receive_status** Istemci geçerli güncelleştirmeleri alıyorsa, gösterge işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="bce7a-282">**receive_status** Pointer to indicator if Client is receiving valid updates.</span></span>

### <a name="return-values"></a><span data-ttu-id="bce7a-283">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="bce7a-283">Return Values</span></span>

- <span data-ttu-id="bce7a-284">**NX_SUCCESS** (0x00) istemci güncelleştirme durumunu başarıyla aldı</span><span class="sxs-lookup"><span data-stu-id="bce7a-284">**NX_SUCCESS** (0x00) Client successfully received update status</span></span>

- <span data-ttu-id="bce7a-285">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="bce7a-285">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="bce7a-286">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="bce7a-286">Allowed From</span></span>

<span data-ttu-id="bce7a-287">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="bce7a-287">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="bce7a-288">Örnek</span><span class="sxs-lookup"><span data-stu-id="bce7a-288">Example</span></span>

```C
/* Determine if the SNTP Client is receiving valid udpates.  */
UINT receive_status;

status =  nx_sntp_client_receiving_updates(client_ptr, 
                                     &receive_status);

/* If status is NX_SUCCESS and receive_status is NX_TRUE, 
   the client is currently receiving valid updates.  */

```

## <a name="nx_sntp_client_request_unicast_time"></a><span data-ttu-id="bce7a-289">nx_sntp_client_request_unicast_time</span><span class="sxs-lookup"><span data-stu-id="bce7a-289">nx_sntp_client_request_unicast_time</span></span>

<span data-ttu-id="bce7a-290">Doğrudan NTP sunucusuna bir tek noktaya yayın isteği gönderin</span><span class="sxs-lookup"><span data-stu-id="bce7a-290">Send a unicast request directly to the NTP Server</span></span>


### <a name="prototype"></a><span data-ttu-id="bce7a-291">Prototype</span><span class="sxs-lookup"><span data-stu-id="bce7a-291">Prototype</span></span>

```C
UINT nx_sntp_client_request_unicast_time(NX_SNTP_CLIENT *client_ptr, 
                                                  UINT wait_option);
```

### <a name="description"></a><span data-ttu-id="bce7a-292">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bce7a-292">Description</span></span>

<span data-ttu-id="bce7a-293">Bu hizmet, uygulamanın bir tek noktaya yayın isteğini, SNTP Istemci iş parçacığı görevinin zaman uyumsuz olarak NTP sunucusuna doğrudan göndermesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="bce7a-293">This service allows the application to directly send a unicast request to the NTP server asynchronously from the SNTP Client thread task.</span></span> <span data-ttu-id="bce7a-294">Bekle seçeneği, yanıt için ne kadar bekleneceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="bce7a-294">The wait option specifies how long to wait for a response.</span></span> <span data-ttu-id="bce7a-295">Başarılı olursa, uygulama, en son saati elde etmek için diğer SNTP Istemci hizmetlerini kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="bce7a-295">If successful, the application can use other SNTP Client services to obtain the latest time.</span></span> <span data-ttu-id="bce7a-296">Daha fazla ayrıntı için bkz. **SNTP zaman uyumsuz tek noktaya yayın istekleri** .</span><span class="sxs-lookup"><span data-stu-id="bce7a-296">See section **SNTP Asynchronous Unicast Requests** for more details.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="bce7a-297">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="bce7a-297">Input Parameters</span></span>

- <span data-ttu-id="bce7a-298">**client_ptr** SNTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="bce7a-298">**client_ptr** Pointer to SNTP Client control block.</span></span>

- <span data-ttu-id="bce7a-299">**Wait_option** Zamanlayıcı Tick 'ındaki NTP yanıtı için bekleme seçeneği.</span><span class="sxs-lookup"><span data-stu-id="bce7a-299">**Wait_option** Wait option for NTP response in timer ticks.</span></span>

### <a name="return-values"></a><span data-ttu-id="bce7a-300">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="bce7a-300">Return Values</span></span>

- <span data-ttu-id="bce7a-301">**NX_SUCCESS** (0x00) istemci tek noktaya yayın güncelleştirmesini başarıyla gönderiyor ve alıyor</span><span class="sxs-lookup"><span data-stu-id="bce7a-301">**NX_SUCCESS** (0x00) Client successfully sends and receives unicast update</span></span>

- <span data-ttu-id="bce7a-302">**NX_SNTP_CLIENT_NOT_STARTED** (0xd0b) istemci iş parçacığı başlatılmadı</span><span class="sxs-lookup"><span data-stu-id="bce7a-302">**NX_SNTP_CLIENT_NOT_STARTED** (0xD0B) Client thread not started</span></span>

- <span data-ttu-id="bce7a-303">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="bce7a-303">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

- <span data-ttu-id="bce7a-304">NX_CALLER_ERROR (0x11) geçersiz hizmet çağıranı</span><span class="sxs-lookup"><span data-stu-id="bce7a-304">NX_CALLER_ERROR (0x11) Invalid caller of service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="bce7a-305">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="bce7a-305">Allowed From</span></span>

<span data-ttu-id="bce7a-306">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="bce7a-306">Threads</span></span>

### <a name="example"></a><span data-ttu-id="bce7a-307">Örnek</span><span class="sxs-lookup"><span data-stu-id="bce7a-307">Example</span></span>

```C
/* Determine if the SNTP Client is receiving valid udpates.  */
UINT receive_status;

status =  nx_sntp_client_request_unicast_time(client_ptr, 400);

/* If status is NX_SUCCESS and receive_status is NX_TRUE, 
   the client is received a valid response to the unicast request.  */

```

## <a name="nx_sntp_client_run_broadcast"></a><span data-ttu-id="bce7a-308">nx_sntp_client_run_broadcast</span><span class="sxs-lookup"><span data-stu-id="bce7a-308">nx_sntp_client_run_broadcast</span></span>

<span data-ttu-id="bce7a-309">Istemciyi yayın modunda çalıştır</span><span class="sxs-lookup"><span data-stu-id="bce7a-309">Run the Client in broadcast mode</span></span>

### <a name="prototype"></a><span data-ttu-id="bce7a-310">Prototype</span><span class="sxs-lookup"><span data-stu-id="bce7a-310">Prototype</span></span>

```C
UINT nx_sntp_client_run_broadcast(NX_SNTP_CLIENT *client_ptr);
```

### <a name="description"></a><span data-ttu-id="bce7a-311">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bce7a-311">Description</span></span>

<span data-ttu-id="bce7a-312">Bu hizmet, Istemci, SNTP sunucusundan yayınlar almak için bekleyeceği, yayın modunda başlatılır.</span><span class="sxs-lookup"><span data-stu-id="bce7a-312">This service starts the Client in broadcast mode where it will wait to receive broadcasts from the SNTP server.</span></span> <span data-ttu-id="bce7a-313">Geçerli bir, SNTP iletisi alınmışsa, bir güncelleştirme olmadan maksimum lapken için SNTP istemci zaman aşımı ve alınan birbirini izleyen geçersiz iletilerin sayısı sıfırlanır.</span><span class="sxs-lookup"><span data-stu-id="bce7a-313">If a valid broadcast SNTP message is received, the SNTP client timeout for maximum lapse without an update and count of consecutive invalid messages received are reset.</span></span> <span data-ttu-id="bce7a-314">Bu limitlerden herhangi biri aşılırsa, SNTP Istemcisi sunucu durumunu geçersiz olarak ayarlar, ancak yine de güncelleştirmeleri almaya bekleyecek.</span><span class="sxs-lookup"><span data-stu-id="bce7a-314">If the either of these limits are exceeded, the SNTP Client sets the server status to invalid although it will still wait to receive updates.</span></span> <span data-ttu-id="bce7a-315">Uygulama, sunucu durumu için SNTP Istemci görevini yoklayabiliyor ve geçersiz SNTP Istemcisini durdurup başka bir SNTP yayın adresiyle yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="bce7a-315">The application can poll the SNTP Client task for server status, and if invalid stop the SNTP Client and reinitialize it with another SNTP broadcast address.</span></span> <span data-ttu-id="bce7a-316">Ayrıca tek noktaya yayın SNTP sunucusuna geçiş yapabilir.</span><span class="sxs-lookup"><span data-stu-id="bce7a-316">It can also switch to a unicast SNTP server.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="bce7a-317">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="bce7a-317">Input Parameters</span></span>

- <span data-ttu-id="bce7a-318">**client_ptr** SNTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="bce7a-318">**client_ptr** Pointer to SNTP Client control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="bce7a-319">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="bce7a-319">Return Values</span></span>

- <span data-ttu-id="bce7a-320">**durum** --------fiili tamamlanma durumu</span><span class="sxs-lookup"><span data-stu-id="bce7a-320">**status** -------- Actual completion status</span></span>

- <span data-ttu-id="bce7a-321">**NX_SNTP_CLIENT_ALREADY_STARTED** (0xd0c) istemcisi zaten başlatılmış</span><span class="sxs-lookup"><span data-stu-id="bce7a-321">**NX_SNTP_CLIENT_ALREADY_STARTED** (0xD0C) Client already started</span></span>

- <span data-ttu-id="bce7a-322">**NX_SNTP_CLIENT_NOT_INITIALIZED** (0xd01) istemci başlatılmadı</span><span class="sxs-lookup"><span data-stu-id="bce7a-322">**NX_SNTP_CLIENT_NOT_INITIALIZED** (0xD01) Client not initialized</span></span>

- <span data-ttu-id="bce7a-323">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="bce7a-323">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

- <span data-ttu-id="bce7a-324">NX_CALLER_ERROR (0x11) geçersiz hizmet çağıranı</span><span class="sxs-lookup"><span data-stu-id="bce7a-324">NX_CALLER_ERROR (0x11) Invalid caller of service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="bce7a-325">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="bce7a-325">Allowed From</span></span>

<span data-ttu-id="bce7a-326">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="bce7a-326">Threads</span></span>

### <a name="example"></a><span data-ttu-id="bce7a-327">Örnek</span><span class="sxs-lookup"><span data-stu-id="bce7a-327">Example</span></span>

```C
/* Start Client running in broadcast mode.  */
status =  nx_sntp_client_run_broadcast(client_ptr);

/* If status is NX_SUCCESS, the client is successfully started.  */

```

## <a name="nx_sntp_client_run_unicast"></a><span data-ttu-id="bce7a-328">nx_sntp_client_run_unicast</span><span class="sxs-lookup"><span data-stu-id="bce7a-328">nx_sntp_client_run_unicast</span></span>

<span data-ttu-id="bce7a-329">Istemciyi tek noktaya yayın modunda çalıştırma</span><span class="sxs-lookup"><span data-stu-id="bce7a-329">Run the Client in unicast mode</span></span>

### <a name="prototype"></a><span data-ttu-id="bce7a-330">Prototype</span><span class="sxs-lookup"><span data-stu-id="bce7a-330">Prototype</span></span>

```C
UINT nx_sntp_client_run_unicast(NX_SNTP_CLIENT *client_ptr);
```

### <a name="description"></a><span data-ttu-id="bce7a-331">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bce7a-331">Description</span></span>

<span data-ttu-id="bce7a-332">Bu hizmet, Istemciyi bir zaman güncelleştirmesi için düzenli olarak SNTP sunucusuna bir tek noktaya yayın isteği gönderdiği tek noktaya yayın modunda başlatır.</span><span class="sxs-lookup"><span data-stu-id="bce7a-332">This service starts the Client in unicast mode where it periodically sends a unicast request to its SNTP Server for a time update.</span></span> <span data-ttu-id="bce7a-333">Geçerli bir SNTP iletisi alınmışsa, güncelleştirme olmadan maksimum lapken için SNTP istemci zaman aşımı, ilk yoklama aralığı ve alınan ardışık geçersiz ileti sayısı sıfırlanır.</span><span class="sxs-lookup"><span data-stu-id="bce7a-333">If a valid SNTP message is received, the SNTP client timeout for maximum lapse without an update, initial polling interval and count of consecutive invalid messages received are reset.</span></span> <span data-ttu-id="bce7a-334">Bu limitlerden herhangi biri aşılırsa, SNTP Istemcisi sunucu durumunu geçersiz olarak ayarlar, ancak yine de yoklama yapar ve güncelleştirmeleri almaya bekler.</span><span class="sxs-lookup"><span data-stu-id="bce7a-334">If the either of these limits are exceeded, the SNTP Client sets the Server status to invalid although it will still poll and wait to receive updates.</span></span> <span data-ttu-id="bce7a-335">Uygulama, sunucu durumu için SNTP Istemci görevini yoklayabiliyor ve geçersiz SNTP Istemcisini durdurup başka bir SNTP tek noktaya yayın adresiyle yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="bce7a-335">The application can poll the SNTP Client task for server status, and if invalid stop the SNTP Client and reinitialize it with another SNTP unicast address.</span></span> <span data-ttu-id="bce7a-336">Ayrıca, bir yayın SNTP sunucusuna geçiş yapabilir.</span><span class="sxs-lookup"><span data-stu-id="bce7a-336">It can also switch to a broadcast SNTP server.</span></span>

<span data-ttu-id="bce7a-337">.</span><span class="sxs-lookup"><span data-stu-id="bce7a-337">.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="bce7a-338">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="bce7a-338">Input Parameters</span></span>

- <span data-ttu-id="bce7a-339">**client_ptr** SNTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="bce7a-339">**client_ptr** Pointer to SNTP Client control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="bce7a-340">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="bce7a-340">Return Values</span></span>

- <span data-ttu-id="bce7a-341">**NX_SUCCESS** (0x00) istemci tek noktaya yayın modunda başarıyla başlatıldı</span><span class="sxs-lookup"><span data-stu-id="bce7a-341">**NX_SUCCESS** (0x00) Successfully started Client in unicast mode</span></span>

- <span data-ttu-id="bce7a-342">**NX_SNTP_CLIENT_ALREADY_STARTED** (0xd0c) istemcisi zaten başlatılmış</span><span class="sxs-lookup"><span data-stu-id="bce7a-342">**NX_SNTP_CLIENT_ALREADY_STARTED** (0xD0C) Client already started</span></span>

- <span data-ttu-id="bce7a-343">**NX_SNTP_CLIENT_NOT_INITIALIZED** (0xd01) istemci başlatılmadı</span><span class="sxs-lookup"><span data-stu-id="bce7a-343">**NX_SNTP_CLIENT_NOT_INITIALIZED** (0xD01) Client not initialized</span></span>

- <span data-ttu-id="bce7a-344">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="bce7a-344">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

- <span data-ttu-id="bce7a-345">NX_CALLER_ERROR (0x11) geçersiz hizmet çağıranı</span><span class="sxs-lookup"><span data-stu-id="bce7a-345">NX_CALLER_ERROR (0x11) Invalid caller of service</span></span>


### <a name="allowed-from"></a><span data-ttu-id="bce7a-346">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="bce7a-346">Allowed From</span></span>

<span data-ttu-id="bce7a-347">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="bce7a-347">Threads</span></span>

### <a name="example"></a><span data-ttu-id="bce7a-348">Örnek</span><span class="sxs-lookup"><span data-stu-id="bce7a-348">Example</span></span>

```C
/* Start the Client in unicast mode. */
status =  nx_sntp_client_run_unicast(client_ptr);

/* If status = NX_SUCCESS, the Client was successfully started.  */

```

## <a name="nx_sntp_client_set_local_time"></a><span data-ttu-id="bce7a-349">nx_sntp_client_set_local_time</span><span class="sxs-lookup"><span data-stu-id="bce7a-349">nx_sntp_client_set_local_time</span></span>

<span data-ttu-id="bce7a-350">SNTP Istemci yerel saatini ayarlama</span><span class="sxs-lookup"><span data-stu-id="bce7a-350">Set the SNTP Client local time</span></span>

### <a name="prototype"></a><span data-ttu-id="bce7a-351">Prototype</span><span class="sxs-lookup"><span data-stu-id="bce7a-351">Prototype</span></span>

```C
UINT nx_sntp_client_set_local_time(NX_SNTP_CLIENT *client_ptr , 
                                ULONG seconds, ULONG fraction);

```

### <a name="description"></a><span data-ttu-id="bce7a-352">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bce7a-352">Description</span></span>

<span data-ttu-id="bce7a-353">Bu hizmet, SNTP Istemci yerel saati ' ni, değer olarak ondalık biçimde (örneğin, saniye ve ' kesir '), onaltılı biçimde bir saniyede yerleştirmek için biçim olan SNTP biçiminde ayarlar.</span><span class="sxs-lookup"><span data-stu-id="bce7a-353">This service sets the SNTP Client local time with the input time, in SNTP format e.g. seconds and ‘fraction’ which is the format for putting fractions of a second in hexadecimal format.</span></span> <span data-ttu-id="bce7a-354">Gerçek zamanlı bir zaman ile (örn. gerçek zamanlı olarak) SNTP Istemci yerel saati 'nin güncelleştirilmesi amaçlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="bce7a-354">It is intended for updating the SNTP Client local time from an independent time keeper, e.g. a real time clock.</span></span> <span data-ttu-id="bce7a-355">SNTP protokolü, yerel saat zamanını ' dritaslağı ' üzerinden tutmak için SNTP zaman güncelleştirmelerine yöneliktir.</span><span class="sxs-lookup"><span data-stu-id="bce7a-355">The SNTP protocol is intended for SNTP time updates to keep local clock time from ‘drifting’.</span></span> <span data-ttu-id="bce7a-356">SNTP sunucu saati güncelleştirmeleri olabilir, ancak uygulama cihazında bağımsız bir zaman Man yoksa, SNTP Istemci yerel saatine tek giriş olarak atanmamıştır.</span><span class="sxs-lookup"><span data-stu-id="bce7a-356">SNTP server time updates can be, but are not intended to be the sole input to the SNTP Client local time if there is no independent time keeper on the application device.</span></span>

<span data-ttu-id="bce7a-357">Bu API, SNTP istemci iş parçacığını başlatmadan önce SNTP Istemcisine temel bir zaman vermek için de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="bce7a-357">This API can also be used to give the SNTP Client a base time before starting the SNTP Client thread.</span></span> <span data-ttu-id="bce7a-358">SNTP Istemci yerel saati, geçerli saat verileri için alınan güncelleştirmelerle karşılaştırılır.</span><span class="sxs-lookup"><span data-stu-id="bce7a-358">The SNTP Client local time is compared to received updates for valid time data.</span></span> <span data-ttu-id="bce7a-359">İlk kez güncelleştirme alındığında çok büyük bir tutarsızlık olabilir.</span><span class="sxs-lookup"><span data-stu-id="bce7a-359">For the first time update received, there might be a very large discrepancy.</span></span> <span data-ttu-id="bce7a-360">Bu nedenle, SNTP Istemcisinin ilk güncelleştirmedeki tutarsızlığı yoksaymasına yönelik bir seçenek vardır.</span><span class="sxs-lookup"><span data-stu-id="bce7a-360">Therefore there is an option for the SNTP Client to ignore the discrepancy on the first update.</span></span> <span data-ttu-id="bce7a-361">Bu şekilde, SNTP Istemcisi temel saat olmadan başlayabilir.</span><span class="sxs-lookup"><span data-stu-id="bce7a-361">In this manner, the SNTP Client can start without a base time.</span></span> <span data-ttu-id="bce7a-362">Giriş saati, bilinen dönem sürelerinden elde edilebilir (genellikle Internet 'te kullanılabilir) ve 1 Ocak 1900 ' den itibaren geçen saniye sayısı (yeni bir ' dönem ' başlatıldığında 2036 ' i) olarak hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="bce7a-362">Input time can be obtained from known epoch times (usually available on the Internet) and are computed as the number of seconds since January 1, 1900 (until 2036 when a new ‘epoch’ will be started.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="bce7a-363">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="bce7a-363">Input Parameters</span></span>

- <span data-ttu-id="bce7a-364">**client_ptr** SNTP Istemci denetim bloğu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="bce7a-364">**client_ptr** Pointer to SNTP Client control block</span></span>

- <span data-ttu-id="bce7a-365">**saniyeler** Süre girişinin saniye bileşeni</span><span class="sxs-lookup"><span data-stu-id="bce7a-365">**seconds** Seconds component of the time input</span></span>

- <span data-ttu-id="bce7a-366">**kesir** SNTP kesir biçimindeki alt saniyeler bileşeni</span><span class="sxs-lookup"><span data-stu-id="bce7a-366">**fraction** Subseconds component in the SNTP fraction format</span></span>

### <a name="return-values"></a><span data-ttu-id="bce7a-367">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="bce7a-367">Return Values</span></span>

- <span data-ttu-id="bce7a-368">**NX_SUCCESS** (0x00) yerel saati başarıyla ayarla</span><span class="sxs-lookup"><span data-stu-id="bce7a-368">**NX_SUCCESS** (0x00) Successfully set local time</span></span>

- <span data-ttu-id="bce7a-369">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="bce7a-369">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="bce7a-370">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="bce7a-370">Allowed From</span></span>

<span data-ttu-id="bce7a-371">Başlatma</span><span class="sxs-lookup"><span data-stu-id="bce7a-371">Initialization</span></span>

### <a name="example"></a><span data-ttu-id="bce7a-372">Örnek</span><span class="sxs-lookup"><span data-stu-id="bce7a-372">Example</span></span>

```C
/* Set the SNTP Client local time. */
base_seconds =  0xd2c50b71;
base_fraction = 0xa132db1e;

status =  nx_sntp_client_set_local_time(&demo_client, 
                                        base_seconds, 
                                        base_fraction);

/* If status is NX_SUCCESS an SNTP Client time 
   was successfully set.  */

```

## <a name="nx_sntp_client_set_time_update_notify"></a><span data-ttu-id="bce7a-373">nx_sntp_client_set_time_update_notify</span><span class="sxs-lookup"><span data-stu-id="bce7a-373">nx_sntp_client_set_time_update_notify</span></span>

<span data-ttu-id="bce7a-374">SNTP güncelleştirme geri aramasını ayarla</span><span class="sxs-lookup"><span data-stu-id="bce7a-374">Set the SNTP update callback</span></span>

### <a name="prototype"></a><span data-ttu-id="bce7a-375">Prototype</span><span class="sxs-lookup"><span data-stu-id="bce7a-375">Prototype</span></span>

```C
UINT nx_sntp_client_set_time_update_notify(NX_SNTP_CLIENT *client_ptr, 
                           VOID (time_update_cb)(NX_SNTP_TIME_MESSAGE 
                        *time_update_ptr, NX_SNTP_TIME *local_time)));

```

### <a name="description"></a><span data-ttu-id="bce7a-376">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bce7a-376">Description</span></span>

<span data-ttu-id="bce7a-377">Bu hizmet, SNTP Istemcisi geçerli bir saat güncelleştirmesi aldığında uygulamayı bilgilendirmek için geri çağırma işlemini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="bce7a-377">This service sets callback to notify the application when the SNTP Client receives a valid time update.</span></span> <span data-ttu-id="bce7a-378">Gerçek SNTP iletisini ve SNTP Istemcisinin yerel saatini (genellikle aynı) NTP biçiminde sağlar.</span><span class="sxs-lookup"><span data-stu-id="bce7a-378">It supplies the actual SNTP message and the SNTP Client’s local time (usually the same) in NTP format.</span></span> <span data-ttu-id="bce7a-379">Uygulama, NTP verilerini doğrudan kullanabilir veya *nx_sntp_client_utility_display_date_time hizmetini* arayarak zaman okunabilir biçime dönüştürebilir.</span><span class="sxs-lookup"><span data-stu-id="bce7a-379">The application can use the NTP data directly or call the *nx_sntp_client_utility_display_date_time service* to convert the time to human readable format.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="bce7a-380">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="bce7a-380">Input Parameters</span></span>

- <span data-ttu-id="bce7a-381">**client_ptr** SNTP Istemci denetim bloğu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="bce7a-381">**client_ptr** Pointer to SNTP Client control block</span></span>

- <span data-ttu-id="bce7a-382">**time_update_cb** Geri çağırma işlevine işaretçisi</span><span class="sxs-lookup"><span data-stu-id="bce7a-382">**time_update_cb** Pointer to callback function</span></span>

### <a name="return-values"></a><span data-ttu-id="bce7a-383">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="bce7a-383">Return Values</span></span>

- <span data-ttu-id="bce7a-384">**NX_SUCCESS** (0x00) geri çağırma başarıyla ayarlandı</span><span class="sxs-lookup"><span data-stu-id="bce7a-384">**NX_SUCCESS** (0x00) Successfully set callback</span></span>

- <span data-ttu-id="bce7a-385">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="bce7a-385">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="bce7a-386">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="bce7a-386">Allowed From</span></span>

<span data-ttu-id="bce7a-387">Başlatma</span><span class="sxs-lookup"><span data-stu-id="bce7a-387">Initialization</span></span>

### <a name="example"></a><span data-ttu-id="bce7a-388">Örnek</span><span class="sxs-lookup"><span data-stu-id="bce7a-388">Example</span></span>

```C
/* Set the SNTP Client time update callback. */
VOID client_time_update_notify(NX_SNTP_TIME_MESSAGE *time_update_ptr, 
                                           NX_SNTP_TIME *local time);

NX_SNTP_CLIENT demo_client;


status = nx_sntp_client_set_time_update_notify(&demo_client, 
                                            time_update_cb);

/* If status is NX_SUCCESS an SNTP Client 
   time update callback was successfully set.  */

```

## <a name="nx_sntp_client_stop"></a><span data-ttu-id="bce7a-389">nx_sntp_client_stop</span><span class="sxs-lookup"><span data-stu-id="bce7a-389">nx_sntp_client_stop</span></span>

<span data-ttu-id="bce7a-390">SNTP Istemci iş parçacığını durdur</span><span class="sxs-lookup"><span data-stu-id="bce7a-390">Stop the SNTP Client thread</span></span>

### <a name="prototype"></a><span data-ttu-id="bce7a-391">Prototype</span><span class="sxs-lookup"><span data-stu-id="bce7a-391">Prototype</span></span>

```C
UINT nx_sntp_client_stop(NX_SNTP_CLIENT *client_ptr);
```

### <a name="description"></a><span data-ttu-id="bce7a-392">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bce7a-392">Description</span></span>

<span data-ttu-id="bce7a-393">Bu hizmet, SNTP Istemci iş parçacığını durduruyor.</span><span class="sxs-lookup"><span data-stu-id="bce7a-393">This service stops the SNTP Client thread.</span></span> <span data-ttu-id="bce7a-394">Sonsuz bir döngüde çalışan SNTP Istemci iş parçacığı görevleri, SNTP istemci durumunun denetimini serbest bırakma ve uygulamaların SNTP Istemcisinde API çağrıları yapmasına izin veren her yinelemede duraklatılır.</span><span class="sxs-lookup"><span data-stu-id="bce7a-394">The SNTP Client thread tasks, which runs in an infinite loop, pauses on every iteration to release control of the SNTP Client state and allow applications to make API calls on the SNTP Client.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="bce7a-395">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="bce7a-395">Input Parameters</span></span>

- <span data-ttu-id="bce7a-396">**client_ptr** SNTP Istemci denetim bloğu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="bce7a-396">**client_ptr** Pointer to SNTP Client control block</span></span>

### <a name="return-values"></a><span data-ttu-id="bce7a-397">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="bce7a-397">Return Values</span></span>

- <span data-ttu-id="bce7a-398">**NX_SUCCESS** (0x00) başarılı durdurulan istemci iş parçacığı</span><span class="sxs-lookup"><span data-stu-id="bce7a-398">**NX_SUCCESS** (0x00) Successful stopped Client thread</span></span>

- <span data-ttu-id="bce7a-399">**NX_SNTP_CLIENT_NOT_STARTED** (0xDB) SNTP istemci iş parçacığı başlatılmadı</span><span class="sxs-lookup"><span data-stu-id="bce7a-399">**NX_SNTP_CLIENT_NOT_STARTED** (0xDB) SNTP Client thread not started</span></span>

- <span data-ttu-id="bce7a-400">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="bce7a-400">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="bce7a-401">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="bce7a-401">Allowed From</span></span>

<span data-ttu-id="bce7a-402">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="bce7a-402">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="bce7a-403">Örnek</span><span class="sxs-lookup"><span data-stu-id="bce7a-403">Example</span></span>

```C
/* Stop the SNTP Client. */
status =  nx_sntp_client_stop(&demo_client);

/* If status is NX_SUCCESS an SNTP 
   Client instance was successfully stopped.  */

```

## <a name="nx_sntp_client_utility_display_date_time"></a><span data-ttu-id="bce7a-404">nx_sntp_client_utility_display_date_time</span><span class="sxs-lookup"><span data-stu-id="bce7a-404">nx_sntp_client_utility_display_date_time</span></span>

<span data-ttu-id="bce7a-405">NTP saatini tarih ve saat dizesine Dönüştür</span><span class="sxs-lookup"><span data-stu-id="bce7a-405">Convert an NTP Time to Date and Time string</span></span>

### <a name="prototype"></a><span data-ttu-id="bce7a-406">Prototype</span><span class="sxs-lookup"><span data-stu-id="bce7a-406">Prototype</span></span>

```C
UINT nx_sntp_client_utility_display_date_time (NX_SNTP_CLIENT 
                      *client_ptr, CHAR *buffer, UINT length);

```

### <a name="description"></a><span data-ttu-id="bce7a-407">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bce7a-407">Description</span></span>

<span data-ttu-id="bce7a-408">Bu hizmet, SNTP Istemci yerel saatini yıl ay tarih biçimine dönüştürür ve sağlanan arabellekteki tarihi döndürür.</span><span class="sxs-lookup"><span data-stu-id="bce7a-408">This service converts the SNTP Client local time to a year month date format and returns the date in the supplied buffer.</span></span> <span data-ttu-id="bce7a-409">NX_SNTP_CURRENT_YEAR geçerli Istemci saatine göre aynı yıl olması gerekir, ancak tanımlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="bce7a-409">The NX_SNTP_CURRENT_YEAR need not be the same year as the current Client time but it must be defined.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="bce7a-410">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="bce7a-410">Input Parameters</span></span>

- <span data-ttu-id="bce7a-411">**SNTP Istemcisine client_ptr Işaretçisi**</span><span class="sxs-lookup"><span data-stu-id="bce7a-411">**client_ptr Pointer to SNTP Client**</span></span>

- <span data-ttu-id="bce7a-412">**arabellek** Tarihi depolamak için arabelleğin işaretçisi</span><span class="sxs-lookup"><span data-stu-id="bce7a-412">**buffer** Pointer to buffer to store date</span></span>

- <span data-ttu-id="bce7a-413">**uzunluk** Giriş arabelleğinin boyutu</span><span class="sxs-lookup"><span data-stu-id="bce7a-413">**length** Size of input buffer</span></span>

### <a name="return-values"></a><span data-ttu-id="bce7a-414">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="bce7a-414">Return Values</span></span>

- <span data-ttu-id="bce7a-415">**NX_SUCCESS** (0x00) başarılı dönüştürme</span><span class="sxs-lookup"><span data-stu-id="bce7a-415">**NX_SUCCESS** (0x00) Successful conversion</span></span>

- <span data-ttu-id="bce7a-416">**NX_SNTP_ERROR_CONVERTING_DATETIME** (0xd08) NX_SNTP_CURRENT_YEAR tanımlı değil veya hiçbir yerel istemci zamanı kurulmadı</span><span class="sxs-lookup"><span data-stu-id="bce7a-416">**NX_SNTP_ERROR_CONVERTING_DATETIME** (0xD08) NX_SNTP_CURRENT_YEAR not defined or no local client time established</span></span>

- <span data-ttu-id="bce7a-417">**NX_SNTP_INVALID_DATETIME_BUFFER** (0xd07) yetersiz arabellek uzunluğu</span><span class="sxs-lookup"><span data-stu-id="bce7a-417">**NX_SNTP_INVALID_DATETIME_BUFFER** (0xD07) Insufficient buffer length</span></span>


### <a name="allowed-from"></a><span data-ttu-id="bce7a-418">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="bce7a-418">Allowed From</span></span>

<span data-ttu-id="bce7a-419">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="bce7a-419">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="bce7a-420">Örnek</span><span class="sxs-lookup"><span data-stu-id="bce7a-420">Example</span></span>

```C
/* Convert and display the Client’s local time. */

status =  nx_sntp_client_utility_display_date_time(client_ptr , 
                                        buffer, sizeof(buffer));

/* If status is NX_SUCCESS, 
   date was successfully written to buffer.  */

```

## <a name="nx_sntp_client_utility_msecs_to_fraction"></a><span data-ttu-id="bce7a-421">nx_sntp_client_utility_msecs_to_fraction</span><span class="sxs-lookup"><span data-stu-id="bce7a-421">nx_sntp_client_utility_msecs_to_fraction</span></span>

<span data-ttu-id="bce7a-422">Milisaniyeyi NTP kesir Bileşenine Dönüştür</span><span class="sxs-lookup"><span data-stu-id="bce7a-422">Convert milliseconds to an NTP fraction component</span></span>

### <a name="prototype"></a><span data-ttu-id="bce7a-423">Prototype</span><span class="sxs-lookup"><span data-stu-id="bce7a-423">Prototype</span></span>

```C
UINT nx_sntp_client_utility_msecs_to_fraction (ULONG milliseconds,   
                                                 ULONG *fraction);

```

### <a name="description"></a><span data-ttu-id="bce7a-424">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bce7a-424">Description</span></span>

<span data-ttu-id="bce7a-425">Bu hizmet giriş milisaniyesini NTP kesir bileşenine dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="bce7a-425">This service converts the input milliseconds to the NTP fraction component.</span></span> <span data-ttu-id="bce7a-426">Bu, SNTP Istemcisinin başlangıç temel saati olan uygulamalarla ve NTP saniyesi/kesir biçiminde değil, kullanılmak üzere tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="bce7a-426">It is intended for use with applications that have a starting base time for the SNTP Client but not in NTP seconds/fraction format.</span></span> <span data-ttu-id="bce7a-427">Geçerli bir kesir yapmak için milisaniye sayısı 1000 ' den az olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="bce7a-427">The number of milliseconds must be less than 1000 to make a valid fraction.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="bce7a-428">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="bce7a-428">Input Parameters</span></span>

- <span data-ttu-id="bce7a-429">**Dönüştürülecek milisaniye milisaniyesi**</span><span class="sxs-lookup"><span data-stu-id="bce7a-429">**milliseconds Milliseconds to convert**</span></span>

- <span data-ttu-id="bce7a-430">**kesir** Milisaniyeye, kesire dönüştürülmüş işaretçi</span><span class="sxs-lookup"><span data-stu-id="bce7a-430">**fraction** Pointer to milliseconds converted to fraction</span></span>

### <a name="return-values"></a><span data-ttu-id="bce7a-431">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="bce7a-431">Return Values</span></span>

- <span data-ttu-id="bce7a-432">**NX_SUCCESS** (0x00) başarılı dönüştürme</span><span class="sxs-lookup"><span data-stu-id="bce7a-432">**NX_SUCCESS** (0x00) Successful conversion</span></span>

- <span data-ttu-id="bce7a-433">**NX_SNTP_OVERFLOW_ERROR** (0xd32) saati tarihe dönüştürme hatası</span><span class="sxs-lookup"><span data-stu-id="bce7a-433">**NX_SNTP_OVERFLOW_ERROR** (0xD32) Error converting time to a date</span></span>

- <span data-ttu-id="bce7a-434">NX_SNTP_INVALID_TIME (0xD30) geçersiz SNTP veri girişi</span><span class="sxs-lookup"><span data-stu-id="bce7a-434">NX_SNTP_INVALID_TIME (0xD30) Invalid SNTP data input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="bce7a-435">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="bce7a-435">Allowed From</span></span>

<span data-ttu-id="bce7a-436">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="bce7a-436">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="bce7a-437">Örnek</span><span class="sxs-lookup"><span data-stu-id="bce7a-437">Example</span></span>

```C
/* Convert the milliseconds to a fraction. */


status =  nx_sntp_client_utility_msecs_to_fraction(milliseconds, 
                                                     &fraction);

/* If status is NX_SUCCESS, 
   data was successfully converted.  */

```

## <a name="nx_sntp_client_utility_usecs_to_fraction"></a><span data-ttu-id="bce7a-438">nx_sntp_client_utility_usecs_to_fraction</span><span class="sxs-lookup"><span data-stu-id="bce7a-438">nx_sntp_client_utility_usecs_to_fraction</span></span>

<span data-ttu-id="bce7a-439">Mikromikrosaniye bir NTP kesir Bileşenine Dönüştür</span><span class="sxs-lookup"><span data-stu-id="bce7a-439">Convert microseconds to an NTP fraction component</span></span>

### <a name="prototype"></a><span data-ttu-id="bce7a-440">Prototype</span><span class="sxs-lookup"><span data-stu-id="bce7a-440">Prototype</span></span>

```C
UINT nx_sntp_client_utility_usecs_to_fraction (ULONG microseconds,   
                                                 ULONG *fraction);

```
### <a name="description"></a><span data-ttu-id="bce7a-441">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bce7a-441">Description</span></span>

<span data-ttu-id="bce7a-442">Bu hizmet, giriş mikrosaniye 'ni NTP kesir bileşenine dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="bce7a-442">This service converts the input microseconds to the NTP fraction component.</span></span> <span data-ttu-id="bce7a-443">Bu, SNTP Istemcisinin başlangıç temel saati olan uygulamalarla ve NTP saniyesi/kesir biçiminde değil, kullanılmak üzere tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="bce7a-443">It is intended for use with applications that have a starting base time for the SNTP Client but not in NTP seconds/fraction format.</span></span> <span data-ttu-id="bce7a-444">Mikrosaniye sayısı, geçerli bir kesir yapmak için 1000000 'den az olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="bce7a-444">The number of microseconds must be less than 1000000 to make a valid fraction.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="bce7a-445">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="bce7a-445">Input Parameters</span></span>

- <span data-ttu-id="bce7a-446">**mikrosaniye** Dönüştürülecek mikrosaniye</span><span class="sxs-lookup"><span data-stu-id="bce7a-446">**microseconds** Microseconds to convert</span></span>

- <span data-ttu-id="bce7a-447">**kesir** Mikrosaniye için bir mikrosaniye işaretçisine işaretçiye dönüştürme</span><span class="sxs-lookup"><span data-stu-id="bce7a-447">**fraction** Pointer to microseconds converted to fraction</span></span>

### <a name="return-values"></a><span data-ttu-id="bce7a-448">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="bce7a-448">Return Values</span></span>

- <span data-ttu-id="bce7a-449">**NX_SUCCESS** (0x00) başarılı dönüştürme</span><span class="sxs-lookup"><span data-stu-id="bce7a-449">**NX_SUCCESS** (0x00) Successful conversion</span></span>

- <span data-ttu-id="bce7a-450">**NX_SNTP_OVERFLOW_ERROR** (0xd32) saati tarihe dönüştürme hatası</span><span class="sxs-lookup"><span data-stu-id="bce7a-450">**NX_SNTP_OVERFLOW_ERROR** (0xD32) Error converting time to a date</span></span>

- <span data-ttu-id="bce7a-451">NX_SNTP_INVALID_TIME (0xD30) geçersiz SNTP veri girişi</span><span class="sxs-lookup"><span data-stu-id="bce7a-451">NX_SNTP_INVALID_TIME (0xD30) Invalid SNTP data input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="bce7a-452">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="bce7a-452">Allowed From</span></span>

<span data-ttu-id="bce7a-453">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="bce7a-453">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="bce7a-454">Örnek</span><span class="sxs-lookup"><span data-stu-id="bce7a-454">Example</span></span>

```C
/* Convert the microseconds to a fraction. */


status =  nx_sntp_client_utility_msecs_to_fraction(microseconds, 
                                                     &fraction);

/* If status is NX_SUCCESS, data was successfully converted.  */

```

## <a name="nx_sntp_client_utility_fraction_to_usecs"></a><span data-ttu-id="bce7a-455">nx_sntp_client_utility_fraction_to_usecs</span><span class="sxs-lookup"><span data-stu-id="bce7a-455">nx_sntp_client_utility_fraction_to_usecs</span></span>

<span data-ttu-id="bce7a-456">NTP kesir bileşenini mikrosaniye olarak dönüştürme</span><span class="sxs-lookup"><span data-stu-id="bce7a-456">Convert an NTP fraction component to microseconds</span></span>

### <a name="prototype"></a><span data-ttu-id="bce7a-457">Prototype</span><span class="sxs-lookup"><span data-stu-id="bce7a-457">Prototype</span></span>

```C
UINT nx_sntp_client_utility_fraction_to_usecs (ULONG fraction,   
                                         ULONG *microseconds);

```

### <a name="description"></a><span data-ttu-id="bce7a-458">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bce7a-458">Description</span></span>

<span data-ttu-id="bce7a-459">Bu hizmet, giriş NTP kesir bileşenini mikrosaniye olarak dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="bce7a-459">This service converts the input NTP fraction component to microseconds.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="bce7a-460">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="bce7a-460">Input Parameters</span></span>

- <span data-ttu-id="bce7a-461">**Dönüştürülecek kesir kesri**</span><span class="sxs-lookup"><span data-stu-id="bce7a-461">**fraction Fraction to convert**</span></span>

- <span data-ttu-id="bce7a-462">**mikrosaniye** Mikrosaniye 'a dönüştürülen kesir işaretçisi</span><span class="sxs-lookup"><span data-stu-id="bce7a-462">**microseconds** Pointer to fraction converted to microseconds</span></span>

### <a name="return-values"></a><span data-ttu-id="bce7a-463">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="bce7a-463">Return Values</span></span>

- <span data-ttu-id="bce7a-464">**NX_SUCCESS** (0x00) başarılı dönüştürme</span><span class="sxs-lookup"><span data-stu-id="bce7a-464">**NX_SUCCESS** (0x00) Successful conversion</span></span>

- <span data-ttu-id="bce7a-465">NX_SNTP_INVALID_TIME (0xD30) geçersiz SNTP veri girişi</span><span class="sxs-lookup"><span data-stu-id="bce7a-465">NX_SNTP_INVALID_TIME (0xD30) Invalid SNTP data input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="bce7a-466">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="bce7a-466">Allowed From</span></span>

<span data-ttu-id="bce7a-467">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="bce7a-467">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="bce7a-468">Örnek</span><span class="sxs-lookup"><span data-stu-id="bce7a-468">Example</span></span>

```C
/* Convert the fraction to microseconds. */


status =  nx_sntp_client_utility_fraction_to_msecs(fraction, 
                                             &microseconds);

/* If status is NX_SUCCESS, data was successfully converted.  */
```