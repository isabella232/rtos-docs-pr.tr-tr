---
title: Bölüm 3-Azure RTOS NetX Duo MTP Istemci hizmetlerinin açıklaması
description: Bu bölüm, tüm NetX Duo MTP istemci hizmetlerinin alfabetik sırada bir açıklamasını içerir.
author: v-condav
ms.author: v-condav
ms.date: 01/27/2021
ms.topic: article
ms.service: rtos
ms.openlocfilehash: b4cdeca81c157934e35a219cd5535ec38f2c0746
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825804"
---
# <a name="chapter-3---description-of-azure-rtos-netx-duo-ptp-client-services"></a><span data-ttu-id="0b12e-103">Bölüm 3-Azure RTOS NetX Duo MTP Istemci hizmetlerinin açıklaması</span><span class="sxs-lookup"><span data-stu-id="0b12e-103">Chapter 3 - Description of Azure RTOS NetX Duo PTP Client Services</span></span>

<span data-ttu-id="0b12e-104">Bu bölüm, tüm NetX Duo MTP istemci hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="0b12e-104">This chapter contains a description of all NetX Duo PTP client services (listed below) in alphabetical order.</span></span>

[!NOTE]
> <span data-ttu-id="0b12e-105">*Aşağıdaki API işlevi açıklamalarındaki **dönüş değerleri** bölümünde **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_DISABLE_ERROR_CHECKING** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.*</span><span class="sxs-lookup"><span data-stu-id="0b12e-105">*In the **Return Values** section in the following API function descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.*</span></span>

## <a name="nx_ptp_client_create"></a><span data-ttu-id="0b12e-106">nx_ptp_client_create</span><span class="sxs-lookup"><span data-stu-id="0b12e-106">nx_ptp_client_create</span></span>

<span data-ttu-id="0b12e-107">Bir PTP istemci örneği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0b12e-107">Create a PTP client instance.</span></span>

### <a name="prototype"></a><span data-ttu-id="0b12e-108">Prototype</span><span class="sxs-lookup"><span data-stu-id="0b12e-108">Prototype</span></span>

```C
UINT nx_ptp_client_create(
    NX_PTP_CLIENT *client_ptr, NX_IP *ip_ptr, 
    UINT interface_index,
    NX_PACKET_POOL *packet_pool_ptr, 
    UINT thread_priority, 
    UCHAR *thread_stack, 
    UINT stack_size,
    NX_PTP_CLIENT_CLOCK_CALLBACK clock_callback, 
    VOID *clock_callback_data);
```

### <a name="description"></a><span data-ttu-id="0b12e-109">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0b12e-109">Description</span></span>

<span data-ttu-id="0b12e-110">Bu hizmet, PTP Client 'ın bir örneğini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0b12e-110">This service creates an instance of the PTP client.</span></span>

<span data-ttu-id="0b12e-111">Uygulamanın, bir IP örneği ve MTP istemcisinin paketleri aktarabilmesi için bir paket havuzu oluşturması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="0b12e-111">Note that the  application must first create an IP instance and a packet pool for the PTP client to transmit packets.</span></span> <span data-ttu-id="0b12e-112">Uygulama, paket havuzu için IP örneğinde aynı paket havuzunu kullanabilir. veya, PTP istemcisi için adanmış bir paket havuzu oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="0b12e-112">For the packet pool, application may use the same packet pool in the IP instance; or it can create a dedicated packet pool for PTP client.</span></span>  <span data-ttu-id="0b12e-113">Adanmış paket havuzu yaklaşımı, küçük paketleri (IPv6 kullanılıyorsa 128 bayt paketi veya yalnızca IPv4 için 108 bayt) kullanmanın avantajlarından yararlanır.</span><span class="sxs-lookup"><span data-stu-id="0b12e-113">The dedicated packet pool approach has the advantage of using small packets (128 bytes packets if IPv6 is used, or 108 bytes for IPv4-only).</span></span>

### <a name="input-parameters"></a><span data-ttu-id="0b12e-114">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="0b12e-114">Input Parameters</span></span>
* <span data-ttu-id="0b12e-115">**client_ptr** Oluşturulacak PTP Client işaretçisi</span><span class="sxs-lookup"><span data-stu-id="0b12e-115">**client_ptr** Pointer to PTP client to create</span></span>
* <span data-ttu-id="0b12e-116">**ip_ptr** IP örneği işaretçisi</span><span class="sxs-lookup"><span data-stu-id="0b12e-116">**ip_ptr** Pointer to IP instance</span></span>
* <span data-ttu-id="0b12e-117">**interface_index** PTP Network arabiriminin dizini</span><span class="sxs-lookup"><span data-stu-id="0b12e-117">**interface_index** Index of PTP network interface</span></span>
* <span data-ttu-id="0b12e-118">**packet_pool_ptr** İstemci paket havuzu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="0b12e-118">**packet_pool_ptr** Pointer to client packet pool</span></span>
* <span data-ttu-id="0b12e-119">**thread_priority**  PTP iş parçacığının önceliği</span><span class="sxs-lookup"><span data-stu-id="0b12e-119">**thread_priority**  Priority of PTP thread</span></span>
* <span data-ttu-id="0b12e-120">**thread_stack** İş parçacığı yığını işaretçisi</span><span class="sxs-lookup"><span data-stu-id="0b12e-120">**thread_stack** Pointer to thread stack</span></span>
* <span data-ttu-id="0b12e-121">**stack_size** İş parçacığı yığınının boyutu</span><span class="sxs-lookup"><span data-stu-id="0b12e-121">**stack_size** Size of thread stack</span></span>
* <span data-ttu-id="0b12e-122">**clock_callback** PTP Clock geri çağırma</span><span class="sxs-lookup"><span data-stu-id="0b12e-122">**clock_callback** PTP clock callback</span></span>
* <span data-ttu-id="0b12e-123">**clock_callback_data** Saat geri çağırması için veriler</span><span class="sxs-lookup"><span data-stu-id="0b12e-123">**clock_callback_data** Data for the clock callback</span></span>

### <a name="return-values"></a><span data-ttu-id="0b12e-124">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="0b12e-124">Return Values</span></span>
* <span data-ttu-id="0b12e-125">**NX_SUCCESS** (0x00) istemci başarıyla oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="0b12e-125">**NX_SUCCESS** (0x00) Client successfully created</span></span>
* <span data-ttu-id="0b12e-126">**NX_PTP_CLIENT_INSUFFICIENT_PACKET_PAYLOAD** (0xd04) paket yükü çok küçük</span><span class="sxs-lookup"><span data-stu-id="0b12e-126">**NX_PTP_CLIENT_INSUFFICIENT_PACKET_PAYLOAD** (0xD04) Packet payload too small</span></span>
* <span data-ttu-id="0b12e-127">**NX_PTP_CLIENT_CLOCK_CALLBACK_FAILURE** (0xd05) saat geri aramasında hata</span><span class="sxs-lookup"><span data-stu-id="0b12e-127">**NX_PTP_CLIENT_CLOCK_CALLBACK_FAILURE** (0xD05) Failure on clock callback</span></span>
* <span data-ttu-id="0b12e-128">**durum** NetX Duo ve ThreadX hizmeti çağrılarının durum bitimi</span><span class="sxs-lookup"><span data-stu-id="0b12e-128">**status** Status completion of NetX Duo and ThreadX service calls</span></span>
* <span data-ttu-id="0b12e-129">NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi</span><span class="sxs-lookup"><span data-stu-id="0b12e-129">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>
* <span data-ttu-id="0b12e-130">NX_INVALID_INTERFACE (0x4C) geçersiz arabirim</span><span class="sxs-lookup"><span data-stu-id="0b12e-130">NX_INVALID_INTERFACE (0x4C) Invalid interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="0b12e-131">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="0b12e-131">Allowed From</span></span>
<span data-ttu-id="0b12e-132">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="0b12e-132">Threads</span></span>

### <a name="example"></a><span data-ttu-id="0b12e-133">Örnek</span><span class="sxs-lookup"><span data-stu-id="0b12e-133">Example</span></span>
```C
/* Create the PTP client instance */
status = nx_ptp_client_create(&ptp_client, &ip_0, 0, &pool_0, 
                              PTP_THREAD_PRIORITY, (UCHAR *)ptp_stack, sizeof(ptp_stack),
                              clock_callback, NX_NULL);

/* If the client was successfully created, status = NX_SUCCESS. */
```

## <a name="nx_ptp_client_delete"></a><span data-ttu-id="0b12e-134">nx_ptp_client_delete</span><span class="sxs-lookup"><span data-stu-id="0b12e-134">nx_ptp_client_delete</span></span>

<span data-ttu-id="0b12e-135">Bir PTP istemci örneğini siler.</span><span class="sxs-lookup"><span data-stu-id="0b12e-135">Deletes a PTP client instance.</span></span>

### <a name="prototype"></a><span data-ttu-id="0b12e-136">Prototype</span><span class="sxs-lookup"><span data-stu-id="0b12e-136">Prototype</span></span>

```C
UINT nx_ptp_client_delete(NX_PTP_CLIENT *client_ptr);
```

### <a name="description"></a><span data-ttu-id="0b12e-137">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0b12e-137">Description</span></span>

<span data-ttu-id="0b12e-138">Bu hizmet, PTP istemcisinin bir örneğini siler.</span><span class="sxs-lookup"><span data-stu-id="0b12e-138">This service deletes an instance of the PTP client.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="0b12e-139">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="0b12e-139">Input Parameters</span></span>
* <span data-ttu-id="0b12e-140">**client_ptr** Silinecek PTP Client işaretçisi</span><span class="sxs-lookup"><span data-stu-id="0b12e-140">**client_ptr** Pointer to PTP client to delete</span></span>

### <a name="return-values"></a><span data-ttu-id="0b12e-141">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="0b12e-141">Return Values</span></span>
* <span data-ttu-id="0b12e-142">**NX_SUCCESS** (0x00) istemci başarıyla silindi</span><span class="sxs-lookup"><span data-stu-id="0b12e-142">**NX_SUCCESS** (0x00) Client successfully deleted</span></span>
* <span data-ttu-id="0b12e-143">NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi</span><span class="sxs-lookup"><span data-stu-id="0b12e-143">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="0b12e-144">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="0b12e-144">Allowed From</span></span>
<span data-ttu-id="0b12e-145">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="0b12e-145">Threads</span></span>

### <a name="example"></a><span data-ttu-id="0b12e-146">Örnek</span><span class="sxs-lookup"><span data-stu-id="0b12e-146">Example</span></span>
```C
/* Delete the PTP client instance */
status = nx_ptp_client_delete(&ptp_client);

/* If the client was successfully deleted, status = NX_SUCCESS. */
```

## <a name="nx_ptp_client_master_info_get"></a><span data-ttu-id="0b12e-147">nx_ptp_client_master_info_get</span><span class="sxs-lookup"><span data-stu-id="0b12e-147">nx_ptp_client_master_info_get</span></span>

<span data-ttu-id="0b12e-148">Ana saat bilgilerini alın.</span><span class="sxs-lookup"><span data-stu-id="0b12e-148">Get master clock information.</span></span>

### <a name="prototype"></a><span data-ttu-id="0b12e-149">Prototype</span><span class="sxs-lookup"><span data-stu-id="0b12e-149">Prototype</span></span>

```C
UINT nx_ptp_client_master_info_get(
    NX_PTP_CLIENT_MASTER *master_ptr, 
    NXD_ADDRESS *address, 
    UCHAR **port_identity, 
    UINT *port_identity_length, 
    UCHAR *priority1, 
    UCHAR *priority2, 
    UCHAR *clock_class, UCHAR *clock_accuracy, 
    USHORT *clock_variance, 
    UCHAR **grandmaster_identity,
    UINT *grandmaster_identity_length, 
    USHORT *steps_removed, 
    UCHAR *time_source);
```

### <a name="description"></a><span data-ttu-id="0b12e-150">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0b12e-150">Description</span></span>
<span data-ttu-id="0b12e-151">Bu hizmet, ana saat bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="0b12e-151">This service gets information of master clock.</span></span> <span data-ttu-id="0b12e-152">Ana denetim bloğu, olay geri çağırma işlevi aracılığıyla kullanıcı uygulamasına geçirilir.</span><span class="sxs-lookup"><span data-stu-id="0b12e-152">The master control block is passed to user application through event callback function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="0b12e-153">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="0b12e-153">Input Parameters</span></span>
* <span data-ttu-id="0b12e-154">**master_ptr** PTP ana saati işaretçisi</span><span class="sxs-lookup"><span data-stu-id="0b12e-154">**master_ptr** Pointer to PTP master clock</span></span>
* <span data-ttu-id="0b12e-155">**Adres** Ana saatin adresi</span><span class="sxs-lookup"><span data-stu-id="0b12e-155">**address** Address of master clock</span></span>
* <span data-ttu-id="0b12e-156">**port_identity** PTP ana bağlantı noktası ve kimliği</span><span class="sxs-lookup"><span data-stu-id="0b12e-156">**port_identity** PTP master port and identity</span></span>
* <span data-ttu-id="0b12e-157">**port_identity_length** PTP ana bağlantı noktasının ve kimliğin uzunluğu</span><span class="sxs-lookup"><span data-stu-id="0b12e-157">**port_identity_length** Length of PTP master port and identity</span></span>
* <span data-ttu-id="0b12e-158">**Priority1** Priority1 of PTP Master saati</span><span class="sxs-lookup"><span data-stu-id="0b12e-158">**priority1** Priority1 of PTP master clock</span></span>
* <span data-ttu-id="0b12e-159">**priority2** Priority2 of PTP Master saati</span><span class="sxs-lookup"><span data-stu-id="0b12e-159">**priority2** Priority2 of PTP master clock</span></span>
* <span data-ttu-id="0b12e-160">**clock_class** PTP Master saatinin sınıfı</span><span class="sxs-lookup"><span data-stu-id="0b12e-160">**clock_class** Class of PTP master clock</span></span>
* <span data-ttu-id="0b12e-161">**clock_accuracy** PTP Master saatinin doğruluğu</span><span class="sxs-lookup"><span data-stu-id="0b12e-161">**clock_accuracy** Accuracy of PTP master clock</span></span>
* <span data-ttu-id="0b12e-162">**clock_variance** PTP Master saatinin varyansı</span><span class="sxs-lookup"><span data-stu-id="0b12e-162">**clock_variance** Variance of PTP master clock</span></span>
* <span data-ttu-id="0b12e-163">**grandmaster_identity** Ana saatin kimliği</span><span class="sxs-lookup"><span data-stu-id="0b12e-163">**grandmaster_identity** Identity of grandmaster clock</span></span>
* <span data-ttu-id="0b12e-164">**grandmaster_identity_length** Ana kimliğin uzunluğu</span><span class="sxs-lookup"><span data-stu-id="0b12e-164">**grandmaster_identity_length** Length of grandmaster Identity</span></span>
* <span data-ttu-id="0b12e-165">**steps_removed** Adımlar, PTP başlığından kaldırıldı</span><span class="sxs-lookup"><span data-stu-id="0b12e-165">**steps_removed** Steps removed from PTP header</span></span>
* <span data-ttu-id="0b12e-166">**time_source** Ana saat tarafından kullanılan zamanlayıcı kaynağı</span><span class="sxs-lookup"><span data-stu-id="0b12e-166">**time_source** The source of timer used by grandmaster clock</span></span>

### <a name="return-values"></a><span data-ttu-id="0b12e-167">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="0b12e-167">Return Values</span></span>
* <span data-ttu-id="0b12e-168">**NX_SUCCESS** (0x00) ana saat bilgilerini başarıyla alın</span><span class="sxs-lookup"><span data-stu-id="0b12e-168">**NX_SUCCESS** (0x00) Get master clock information successfully</span></span>
* <span data-ttu-id="0b12e-169">NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi</span><span class="sxs-lookup"><span data-stu-id="0b12e-169">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="0b12e-170">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="0b12e-170">Allowed From</span></span>
<span data-ttu-id="0b12e-171">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="0b12e-171">Threads</span></span>

### <a name="example"></a><span data-ttu-id="0b12e-172">Örnek</span><span class="sxs-lookup"><span data-stu-id="0b12e-172">Example</span></span>
```C
static UINT ptp_event_callback(NX_PTP_CLIENT *ptp_client_ptr, UINT event, VOID *event_data, VOID *callback_data)
{
NXD_ADDRESS address;
UCHAR *port_identity;
UINT port_identity_length;
UCHAR priority1, priority2;
UCHAR clock_class, clock_accuracy;
USHORT clock_variance;
UCHAR *grandmaster_identity;
UINT grandmaster_identity_length;
USHORT steps_removed;
UCHAR time_source;

    switch (event)
    {
        case NX_PTP_CLIENT_EVENT_MASTER:
        {
            status = nx_ptp_client_master_info_get((NX_PTP_CLIENT_MASTER *)event_data, 
                                                   &address, &port_identity,
                                                   &port_identity_length, &priority1, 
                                                   &priority2, &clock_class,
                                                   &clock_accuracy, &clock_variance, 
                                                   &grandmaster_identity,
                                                   &grandmaster_identity_length, 
                                                   &steps_removed, &time_source);

            /* If the master clock information was successfully get, status = NX_SUCCESS. */
            break;
        }

        /* Other event process. */
    }
}
```

## <a name="nx_ptp_client_packet_timestamp_notify"></a><span data-ttu-id="0b12e-173">nx_ptp_client_packet_timestamp_notify</span><span class="sxs-lookup"><span data-stu-id="0b12e-173">nx_ptp_client_packet_timestamp_notify</span></span>

<span data-ttu-id="0b12e-174">PTP Client 'ı paketin zaman damgasına bildirme.</span><span class="sxs-lookup"><span data-stu-id="0b12e-174">Notify PTP client the timestamp of the packet.</span></span>

### <a name="prototype"></a><span data-ttu-id="0b12e-175">Prototype</span><span class="sxs-lookup"><span data-stu-id="0b12e-175">Prototype</span></span>

```C
VOID nx_ptp_client_packet_timestamp_notify(
    NX_PTP_CLIENT *client_ptr, 
    NX_PACKET *packet_ptr, 
    NX_PTP_TIME *timestamp_ptr);
```

### <a name="description"></a><span data-ttu-id="0b12e-176">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0b12e-176">Description</span></span>
<span data-ttu-id="0b12e-177">Bu hizmet, PTP istemcisine paketin zaman damgasıyla iletildiğini bildirir.</span><span class="sxs-lookup"><span data-stu-id="0b12e-177">This service notifies the PTP client that packet is transmitted with timestamp.</span></span> <span data-ttu-id="0b12e-178">Bu hizmet ağ sürücüsü için tasarlanmıştır ve paket iletildiğinde çağrılır.</span><span class="sxs-lookup"><span data-stu-id="0b12e-178">This service is designed for network driver and invoked when the packet is transmitted.</span></span> <span data-ttu-id="0b12e-179">Zaman damgası genellikle donanım tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="0b12e-179">The timestamp is usually generated by hardware.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="0b12e-180">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="0b12e-180">Input Parameters</span></span>
* <span data-ttu-id="0b12e-181">**client_ptr** Oluşturulacak PTP Client işaretçisi</span><span class="sxs-lookup"><span data-stu-id="0b12e-181">**client_ptr** Pointer to PTP client to create</span></span>
* <span data-ttu-id="0b12e-182">**packet_ptr** Aktarılan PTP paketi işaretçisi</span><span class="sxs-lookup"><span data-stu-id="0b12e-182">**packet_ptr** Pointer to PTP packet that is transmitted</span></span>
* <span data-ttu-id="0b12e-183">**timestamp_ptr** MTP paketinin zaman damgası işaretçisi</span><span class="sxs-lookup"><span data-stu-id="0b12e-183">**timestamp_ptr** Pointer to timestamp of PTP packet</span></span>

### <a name="return-values"></a><span data-ttu-id="0b12e-184">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="0b12e-184">Return Values</span></span>
<span data-ttu-id="0b12e-185">Yok</span><span class="sxs-lookup"><span data-stu-id="0b12e-185">None</span></span>

### <a name="allowed-from"></a><span data-ttu-id="0b12e-186">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="0b12e-186">Allowed From</span></span>
<span data-ttu-id="0b12e-187">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="0b12e-187">Threads</span></span>

### <a name="example"></a><span data-ttu-id="0b12e-188">Örnek</span><span class="sxs-lookup"><span data-stu-id="0b12e-188">Example</span></span>
```C
/* Call notification callback */
nx_ptp_client_packet_timestamp_notify(client_ptr, packet_ptr, &ts);
```

## <a name="nx_ptp_client_soft_clock_callback"></a><span data-ttu-id="0b12e-189">nx_ptp_client_soft_clock_callback</span><span class="sxs-lookup"><span data-stu-id="0b12e-189">nx_ptp_client_soft_clock_callback</span></span>

<span data-ttu-id="0b12e-190">Bir PTP saatinin yazılım uygulama.</span><span class="sxs-lookup"><span data-stu-id="0b12e-190">Software implementation of a PTP clock.</span></span>

### <a name="prototype"></a><span data-ttu-id="0b12e-191">Prototype</span><span class="sxs-lookup"><span data-stu-id="0b12e-191">Prototype</span></span>

```C
UINT nx_ptp_client_soft_clock_callback(
    NX_PTP_CLIENT *client_ptr, 
    UINT operation,
    NX_PTP_TIME *time_ptr, 
    NX_PACKET *packet_ptr,
    VOID *callback_data);
```

### <a name="description"></a><span data-ttu-id="0b12e-192">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0b12e-192">Description</span></span>
<span data-ttu-id="0b12e-193">Bu geri çağırma işlevi, PTP için benzetimli düşük çözünürlüklü saat kaynağı olarak görev yapar.</span><span class="sxs-lookup"><span data-stu-id="0b12e-193">This callback function serves as a simulated low resolution clock source for PTP.</span></span> <span data-ttu-id="0b12e-194">Bu yordam bir başvuru olarak sağlanır ve üretim için kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="0b12e-194">This routine is provided as a reference and cannot be used for production.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="0b12e-195">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="0b12e-195">Input Parameters</span></span>
* <span data-ttu-id="0b12e-196">**client_ptr** Oluşturulacak PTP Client işaretçisi</span><span class="sxs-lookup"><span data-stu-id="0b12e-196">**client_ptr** Pointer to PTP client to create</span></span>
* <span data-ttu-id="0b12e-197">**işlem** Geri çağırma işlemi, geçerli değerler şu şekilde tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="0b12e-197">**operation** Callback operation, valid values are defined as:</span></span>
  * <span data-ttu-id="0b12e-198">**NX_PTP_CLIENT_CLOCK_INIT** Saati başlatın.</span><span class="sxs-lookup"><span data-stu-id="0b12e-198">**NX_PTP_CLIENT_CLOCK_INIT** Initialize clock.</span></span>
  * <span data-ttu-id="0b12e-199">**NX_PTP_CLIENT_CLOCK_SET** Tarafından belirtilen geçerli zaman damgasını ayarla `time_ptr` .</span><span class="sxs-lookup"><span data-stu-id="0b12e-199">**NX_PTP_CLIENT_CLOCK_SET** Set current timestamp specified by `time_ptr`.</span></span>
  * <span data-ttu-id="0b12e-200">**NX_PTP_CLIENT_CLOCK_GET** Geçerli zaman damgasını döndürür `time_ptr` .</span><span class="sxs-lookup"><span data-stu-id="0b12e-200">**NX_PTP_CLIENT_CLOCK_GET** Return current timestamp to `time_ptr`.</span></span>
  * <span data-ttu-id="0b12e-201">**NX_PTP_CLIENT_CLOCK_PACKET_TS_EXTRACT** Zaman damgasını konumundan `packet_ptr` ayıklayın `time_ptr` .</span><span class="sxs-lookup"><span data-stu-id="0b12e-201">**NX_PTP_CLIENT_CLOCK_PACKET_TS_EXTRACT** Extract timestamp from `packet_ptr` to `time_ptr`.</span></span>
  * <span data-ttu-id="0b12e-202">**NX_PTP_CLIENT_CLOCK_ADJUST** Geçerli zaman damgasını *1* saniyeden az ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="0b12e-202">**NX_PTP_CLIENT_CLOCK_ADJUST** Adjust current timestamp less than *1* second.</span></span>
  * <span data-ttu-id="0b12e-203">**NX_PTP_CLIENT_CLOCK_PACKET_TS_PREPARE** `packet_ptr` PTP Client ' ın aktarıldığı zaman damgasına bildirilmesini gerektiren öğesini işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="0b12e-203">**NX_PTP_CLIENT_CLOCK_PACKET_TS_PREPARE** Mark the `packet_ptr` which requires to notify PTP client the timestamp when it is transmitted.</span></span>
  * <span data-ttu-id="0b12e-204">**NX_PTP_CLIENT_CLOCK_SOFT_TIMER_UPDATE** Geçici zamanlayıcıyı güncelleştir.</span><span class="sxs-lookup"><span data-stu-id="0b12e-204">**NX_PTP_CLIENT_CLOCK_SOFT_TIMER_UPDATE** Update soft timer.</span></span> <span data-ttu-id="0b12e-205">Bu, donanım saati tarafından yoksayılabilir.</span><span class="sxs-lookup"><span data-stu-id="0b12e-205">It can be ignored by hardware clock.</span></span>
* <span data-ttu-id="0b12e-206">**time_ptr** Zaman damgası işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0b12e-206">**time_ptr** Pointer to timestamp.</span></span>
* <span data-ttu-id="0b12e-207">**packet_ptr** Paket işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0b12e-207">**packet_ptr** Pointer to packet.</span></span>
* <span data-ttu-id="0b12e-208">**callback_data** Donuk geri çağırma verileri işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0b12e-208">**callback_data** Pointer to opaque callback data.</span></span>

### <a name="return-values"></a><span data-ttu-id="0b12e-209">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="0b12e-209">Return Values</span></span>
* <span data-ttu-id="0b12e-210">Işlem başarıyla **NX_SUCCESS** (0x00)</span><span class="sxs-lookup"><span data-stu-id="0b12e-210">**NX_SUCCESS** (0x00) Operation successfully</span></span>
* <span data-ttu-id="0b12e-211">**NX_PTP_PARAM_ERROR** (0xd03) geçersiz parametre</span><span class="sxs-lookup"><span data-stu-id="0b12e-211">**NX_PTP_PARAM_ERROR** (0xD03) Invalid parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="0b12e-212">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="0b12e-212">Allowed From</span></span>
<span data-ttu-id="0b12e-213">PTP iç</span><span class="sxs-lookup"><span data-stu-id="0b12e-213">PTP internal</span></span>

### <a name="example"></a><span data-ttu-id="0b12e-214">Örnek</span><span class="sxs-lookup"><span data-stu-id="0b12e-214">Example</span></span>
```C/* Create the PTP client instance */
status = nx_ptp_client_create(&ptp_client, &ip_0, 0, &pool_0, 
                              PTP_THREAD_PRIORITY, (UCHAR *)ptp_stack, sizeof(ptp_stack),
                              nx_ptp_client_soft_clock_callback, NX_NULL);

/* If the client was successfully created, status = NX_SUCCESS. */
```

## <a name="nx_ptp_client_start"></a><span data-ttu-id="0b12e-215">nx_ptp_client_start</span><span class="sxs-lookup"><span data-stu-id="0b12e-215">nx_ptp_client_start</span></span>

<span data-ttu-id="0b12e-216">PTP Client 'ı başlatın.</span><span class="sxs-lookup"><span data-stu-id="0b12e-216">Start PTP client.</span></span>

### <a name="prototype"></a><span data-ttu-id="0b12e-217">Prototype</span><span class="sxs-lookup"><span data-stu-id="0b12e-217">Prototype</span></span>

```C
UINT nx_ptp_client_start(
    NX_PTP_CLIENT *client_ptr, 
    UCHAR *client_port_identity_ptr, 
    UINT client_port_identity_length,
    UINT domain, 
    UINT transport_specific, 
    NX_PTP_CLIENT_EVENT_CALLBACK event_callback,
    VOID *event_callback_data)
```

### <a name="description"></a><span data-ttu-id="0b12e-218">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0b12e-218">Description</span></span>
<span data-ttu-id="0b12e-219">Bu hizmet daha önce oluşturulmuş bir PTP istemci örneğini başlatır.</span><span class="sxs-lookup"><span data-stu-id="0b12e-219">This service starts a previously created PTP client instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="0b12e-220">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="0b12e-220">Input Parameters</span></span>
* <span data-ttu-id="0b12e-221">**client_ptr** Oluşturulacak PTP Client işaretçisi</span><span class="sxs-lookup"><span data-stu-id="0b12e-221">**client_ptr** Pointer to PTP client to create</span></span>
* <span data-ttu-id="0b12e-222">**client_port_identity_ptr** İstemci bağlantı noktası ve kimlik işaretçisi, NULL olabilir</span><span class="sxs-lookup"><span data-stu-id="0b12e-222">**client_port_identity_ptr** Pointer to client port and identity, it can be NULL</span></span>
* <span data-ttu-id="0b12e-223">**client_port_identity_length** İstemci bağlantı noktası ve kimlik uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="0b12e-223">**client_port_identity_length** Length of client port and identity.</span></span> <span data-ttu-id="0b12e-224">Client_port_identity_ptr NULL veya NX_PTP_CLOCK_PORT_IDENTITY_SIZE (10) ise 0 olmalıdır</span><span class="sxs-lookup"><span data-stu-id="0b12e-224">It must be 0 if client_port_identity_ptr is NULL or NX_PTP_CLOCK_PORT_IDENTITY_SIZE (10)</span></span>
* <span data-ttu-id="0b12e-225">**etki alanı** PTP saat etki alanı</span><span class="sxs-lookup"><span data-stu-id="0b12e-225">**domain** PTP clock domain</span></span>
* <span data-ttu-id="0b12e-226">**transport_specific** 4 bit aktarıma özgü</span><span class="sxs-lookup"><span data-stu-id="0b12e-226">**transport_specific** 4 bits of transport specific</span></span>
* <span data-ttu-id="0b12e-227">**event_callback** Geri çağırma işlevi olayda çağrıldı</span><span class="sxs-lookup"><span data-stu-id="0b12e-227">**event_callback** Callback function invoked on event</span></span>
* <span data-ttu-id="0b12e-228">**event_callback_data** Olay geri çağırması için veriler</span><span class="sxs-lookup"><span data-stu-id="0b12e-228">**event_callback_data** Data for the event callback</span></span>

### <a name="return-values"></a><span data-ttu-id="0b12e-229">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="0b12e-229">Return Values</span></span>
* <span data-ttu-id="0b12e-230">**NX_SUCCESS** (0x00) istemci başarıyla başlatıldı</span><span class="sxs-lookup"><span data-stu-id="0b12e-230">**NX_SUCCESS** (0x00) Client successfully started</span></span>
* <span data-ttu-id="0b12e-231">**NX_PTP_CLIENT_ALREADY_STARTED** (0xd02) MTP istemcisi zaten başlatılmış</span><span class="sxs-lookup"><span data-stu-id="0b12e-231">**NX_PTP_CLIENT_ALREADY_STARTED** (0xD02) PTP client already started</span></span>
* <span data-ttu-id="0b12e-232">**durum** NetX Duo ve ThreadX hizmeti çağrılarının durum bitimi</span><span class="sxs-lookup"><span data-stu-id="0b12e-232">**status** Status completion of NetX Duo and ThreadX service calls</span></span>
* <span data-ttu-id="0b12e-233">NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi</span><span class="sxs-lookup"><span data-stu-id="0b12e-233">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="0b12e-234">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="0b12e-234">Allowed From</span></span>
<span data-ttu-id="0b12e-235">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="0b12e-235">Threads</span></span>

### <a name="example"></a><span data-ttu-id="0b12e-236">Örnek</span><span class="sxs-lookup"><span data-stu-id="0b12e-236">Example</span></span>
```C
status = nx_ptp_client_start(&ptp_client, NX_NULL, 0, 0, 0, ptp_event_callback, NX_NULL);

/* If the client was successfully started, status = NX_SUCCESS. */
```

## <a name="nx_ptp_client_stop"></a><span data-ttu-id="0b12e-237">nx_ptp_client_stop</span><span class="sxs-lookup"><span data-stu-id="0b12e-237">nx_ptp_client_stop</span></span>

<span data-ttu-id="0b12e-238">PTP Client 'ı durdurun.</span><span class="sxs-lookup"><span data-stu-id="0b12e-238">Stop PTP client.</span></span>  <span data-ttu-id="0b12e-239">PTP Client durdurulduktan sonra, PTP paketlerini işlemez veya PTP paketlerini iletmez.</span><span class="sxs-lookup"><span data-stu-id="0b12e-239">After the PTP client is stopped, it does not process PTP packets, nor does it transmit PTP packets.</span></span>

### <a name="prototype"></a><span data-ttu-id="0b12e-240">Prototype</span><span class="sxs-lookup"><span data-stu-id="0b12e-240">Prototype</span></span>

```C
UINT nx_ptp_client_stop(NX_PTP_CLIENT *client_ptr);
```

### <a name="description"></a><span data-ttu-id="0b12e-241">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0b12e-241">Description</span></span>
<span data-ttu-id="0b12e-242">Bu hizmet daha önce oluşturulmuş ve başlatılmış bir PTP istemci örneğini durduruyor.</span><span class="sxs-lookup"><span data-stu-id="0b12e-242">This service stops a previously created and started PTP client instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="0b12e-243">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="0b12e-243">Input Parameters</span></span>
* <span data-ttu-id="0b12e-244">**client_ptr** Durdurulacak PTP Client işaretçisi</span><span class="sxs-lookup"><span data-stu-id="0b12e-244">**client_ptr** Pointer to PTP client to stop</span></span>

### <a name="return-values"></a><span data-ttu-id="0b12e-245">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="0b12e-245">Return Values</span></span>
* <span data-ttu-id="0b12e-246">**NX_SUCCESS** (0x00) istemci başarıyla durduruldu</span><span class="sxs-lookup"><span data-stu-id="0b12e-246">**NX_SUCCESS** (0x00) Client successfully stopped</span></span>
* <span data-ttu-id="0b12e-247">**NX_PTP_CLIENT_NOT_STARTED** (0xd01) istemci başlatılmadı</span><span class="sxs-lookup"><span data-stu-id="0b12e-247">**NX_PTP_CLIENT_NOT_STARTED** (0xD01) Client not started</span></span>
* <span data-ttu-id="0b12e-248">NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi</span><span class="sxs-lookup"><span data-stu-id="0b12e-248">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="0b12e-249">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="0b12e-249">Allowed From</span></span>
<span data-ttu-id="0b12e-250">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="0b12e-250">Threads</span></span>

### <a name="example"></a><span data-ttu-id="0b12e-251">Örnek</span><span class="sxs-lookup"><span data-stu-id="0b12e-251">Example</span></span>
```C
status = nx_ptp_client_stop(&ptp_client);

/* If the client was successfully stopped, status = NX_SUCCESS. */
```

## <a name="nx_ptp_client_sync_info_get"></a><span data-ttu-id="0b12e-252">nx_ptp_client_sync_info_get</span><span class="sxs-lookup"><span data-stu-id="0b12e-252">nx_ptp_client_sync_info_get</span></span>

<span data-ttu-id="0b12e-253">Eşitleme bilgilerini alın.</span><span class="sxs-lookup"><span data-stu-id="0b12e-253">Get Sync information.</span></span>

### <a name="prototype"></a><span data-ttu-id="0b12e-254">Prototype</span><span class="sxs-lookup"><span data-stu-id="0b12e-254">Prototype</span></span>

```C
UINT nx_ptp_client_sync_info_get(
    NX_PTP_CLIENT_SYNC *sync_ptr, 
    USHORT *flags, 
    SHORT *utc_offset);
```

### <a name="description"></a><span data-ttu-id="0b12e-255">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0b12e-255">Description</span></span>
<span data-ttu-id="0b12e-256">Bu hizmet, eşitleme iletisi bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="0b12e-256">This service gets information of Sync message.</span></span> <span data-ttu-id="0b12e-257">Eşitleme denetim bloğu, olay geri çağırma işlevi aracılığıyla kullanıcı uygulamasına geçirilir.</span><span class="sxs-lookup"><span data-stu-id="0b12e-257">The Sync control block is passed to user application through event callback function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="0b12e-258">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="0b12e-258">Input Parameters</span></span>
* <span data-ttu-id="0b12e-259">**client_ptr** Oluşturulacak PTP Client işaretçisi</span><span class="sxs-lookup"><span data-stu-id="0b12e-259">**client_ptr** Pointer to PTP client to create</span></span>
* <span data-ttu-id="0b12e-260">**bayraklar** Eşitleme iletisindeki bayraklar</span><span class="sxs-lookup"><span data-stu-id="0b12e-260">**flags** Flags in Sync message</span></span>
* <span data-ttu-id="0b12e-261">**utc_offset** Day ile UTC arasındaki fark</span><span class="sxs-lookup"><span data-stu-id="0b12e-261">**utc_offset** Offset between TAI and UTC</span></span>

### <a name="return-values"></a><span data-ttu-id="0b12e-262">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="0b12e-262">Return Values</span></span>
* <span data-ttu-id="0b12e-263">**NX_SUCCESS** (0x00) eşitleme bilgilerini başarıyla alın</span><span class="sxs-lookup"><span data-stu-id="0b12e-263">**NX_SUCCESS** (0x00) Get Sync information successfully</span></span>
* <span data-ttu-id="0b12e-264">NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi</span><span class="sxs-lookup"><span data-stu-id="0b12e-264">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="0b12e-265">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="0b12e-265">Allowed From</span></span>
<span data-ttu-id="0b12e-266">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="0b12e-266">Threads</span></span>

### <a name="example"></a><span data-ttu-id="0b12e-267">Örnek</span><span class="sxs-lookup"><span data-stu-id="0b12e-267">Example</span></span>
```C
static UINT ptp_event_callback(NX_PTP_CLIENT *ptp_client_ptr, UINT event, VOID *event_data, VOID *callback_data)
{
USHORT utc_offset;

    switch (event)
    {
        case NX_PTP_CLIENT_EVENT_SYNC:
        {
            nx_ptp_client_sync_info_get((NX_PTP_CLIENT_SYNC *)event_data, NX_NULL, &utc_offset);

            /* If the Sync information was successfully get, status = NX_SUCCESS. */
            break;
        }

        /* Other event process. */
    }
}
```

## <a name="nx_ptp_client_time_get"></a><span data-ttu-id="0b12e-268">nx_ptp_client_time_get</span><span class="sxs-lookup"><span data-stu-id="0b12e-268">nx_ptp_client_time_get</span></span>

<span data-ttu-id="0b12e-269">Geçerli saati al.</span><span class="sxs-lookup"><span data-stu-id="0b12e-269">Get current time.</span></span>

### <a name="prototype"></a><span data-ttu-id="0b12e-270">Prototype</span><span class="sxs-lookup"><span data-stu-id="0b12e-270">Prototype</span></span>

```C
UINT nx_ptp_client_time_get(
    NX_PTP_CLIENT *client_ptr, 
    NX_PTP_TIME *time_ptr);
```

### <a name="description"></a><span data-ttu-id="0b12e-271">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0b12e-271">Description</span></span>
<span data-ttu-id="0b12e-272">Bu hizmet, PTP saatinin geçerli değerini alır.</span><span class="sxs-lookup"><span data-stu-id="0b12e-272">This service gets the current value of the PTP clock.</span></span> <span data-ttu-id="0b12e-273">Her ne zaman bir PTP istemcisi ana saatle eşitlenmez.</span><span class="sxs-lookup"><span data-stu-id="0b12e-273">It is available no matter PTP client is synchronized with master clock or not.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="0b12e-274">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="0b12e-274">Input Parameters</span></span>
* <span data-ttu-id="0b12e-275">**client_ptr** Oluşturulacak PTP Client işaretçisi</span><span class="sxs-lookup"><span data-stu-id="0b12e-275">**client_ptr** Pointer to PTP client to create</span></span>
* <span data-ttu-id="0b12e-276">**time_ptr** PTP saati işaretçisi</span><span class="sxs-lookup"><span data-stu-id="0b12e-276">**time_ptr** Pointer to PTP time</span></span>

### <a name="return-values"></a><span data-ttu-id="0b12e-277">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="0b12e-277">Return Values</span></span>
* <span data-ttu-id="0b12e-278">**NX_SUCCESS** (0x00) istemci başarıyla oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="0b12e-278">**NX_SUCCESS** (0x00) Client successfully created</span></span>
* <span data-ttu-id="0b12e-279">NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi</span><span class="sxs-lookup"><span data-stu-id="0b12e-279">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="0b12e-280">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="0b12e-280">Allowed From</span></span>
<span data-ttu-id="0b12e-281">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="0b12e-281">Threads</span></span>

### <a name="example"></a><span data-ttu-id="0b12e-282">Örnek</span><span class="sxs-lookup"><span data-stu-id="0b12e-282">Example</span></span>
```C
/* Get the PTP clock */
nx_ptp_client_time_get(&ptp_client, &tm);
```

## <a name="nx_ptp_client_time_set"></a><span data-ttu-id="0b12e-283">nx_ptp_client_time_set</span><span class="sxs-lookup"><span data-stu-id="0b12e-283">nx_ptp_client_time_set</span></span>

<span data-ttu-id="0b12e-284">Geçerli saati ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="0b12e-284">Set current time.</span></span>

### <a name="prototype"></a><span data-ttu-id="0b12e-285">Prototype</span><span class="sxs-lookup"><span data-stu-id="0b12e-285">Prototype</span></span>

```C
UINT nx_ptp_client_time_set(
    NX_PTP_CLIENT *client_ptr, 
    NX_PTP_TIME *time_ptr);
```

### <a name="description"></a><span data-ttu-id="0b12e-286">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0b12e-286">Description</span></span>
<span data-ttu-id="0b12e-287">Bu hizmet, PTP saatinin geçerli değerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="0b12e-287">This service sets the current value of the PTP clock.</span></span> <span data-ttu-id="0b12e-288">PTP Client başlamadan önce çağrılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0b12e-288">It must be invoked before PTP client starts.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="0b12e-289">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="0b12e-289">Input Parameters</span></span>
* <span data-ttu-id="0b12e-290">**client_ptr** Oluşturulacak PTP Client işaretçisi</span><span class="sxs-lookup"><span data-stu-id="0b12e-290">**client_ptr** Pointer to PTP client to create</span></span>
* <span data-ttu-id="0b12e-291">**time_ptr** PTP saati işaretçisi</span><span class="sxs-lookup"><span data-stu-id="0b12e-291">**time_ptr** Pointer to PTP time</span></span>

### <a name="return-values"></a><span data-ttu-id="0b12e-292">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="0b12e-292">Return Values</span></span>
* <span data-ttu-id="0b12e-293">**NX_SUCCESS** (0x00) istemci başarıyla oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="0b12e-293">**NX_SUCCESS** (0x00) Client successfully created</span></span>
* <span data-ttu-id="0b12e-294">**NX_PTP_CLIENT_ALREADY_STARTED** (0xd02) MTP istemcisi zaten başlatılmış</span><span class="sxs-lookup"><span data-stu-id="0b12e-294">**NX_PTP_CLIENT_ALREADY_STARTED** (0xD02) PTP client already started</span></span>
* <span data-ttu-id="0b12e-295">NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi</span><span class="sxs-lookup"><span data-stu-id="0b12e-295">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="0b12e-296">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="0b12e-296">Allowed From</span></span>
<span data-ttu-id="0b12e-297">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="0b12e-297">Threads</span></span>

### <a name="example"></a><span data-ttu-id="0b12e-298">Örnek</span><span class="sxs-lookup"><span data-stu-id="0b12e-298">Example</span></span>
```C
/* Set current time before PTP client started.  */
status = nx_ptp_client_time_set(&ptp_client, &tm);
```

## <a name="nx_ptp_client_utility_convert_time_to_date"></a><span data-ttu-id="0b12e-299">nx_ptp_client_utility_convert_time_to_date</span><span class="sxs-lookup"><span data-stu-id="0b12e-299">nx_ptp_client_utility_convert_time_to_date</span></span>

<span data-ttu-id="0b12e-300">PTP Time saatini UTC Tarih ve saatine dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="0b12e-300">Convert PTP time to a UTC date and time.</span></span>

### <a name="prototype"></a><span data-ttu-id="0b12e-301">Prototype</span><span class="sxs-lookup"><span data-stu-id="0b12e-301">Prototype</span></span>

```C
UINT nx_ptp_client_utility_convert_time_to_date(
    NX_PTP_TIME *time_ptr, 
    LONG offset, 
    NX_PTP_DATE_TIME *date_time_ptr);
```

### <a name="description"></a><span data-ttu-id="0b12e-302">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0b12e-302">Description</span></span>
<span data-ttu-id="0b12e-303">Bu hizmet, PTP Time süresini UTC Tarih ve saatine dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="0b12e-303">This service converts PTP time to a UTC date and time.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="0b12e-304">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="0b12e-304">Input Parameters</span></span>
* <span data-ttu-id="0b12e-305">**time_ptr** PTP saati işaretçisi</span><span class="sxs-lookup"><span data-stu-id="0b12e-305">**time_ptr** Pointer to PTP time</span></span>
* <span data-ttu-id="0b12e-306">**konum** PTP saati eklemek için imzalanan ikinci konum</span><span class="sxs-lookup"><span data-stu-id="0b12e-306">**offset** Signed second offset to add the PTP time</span></span>
* <span data-ttu-id="0b12e-307">**date_time_ptr** Sonuç tarihi işaretçisi</span><span class="sxs-lookup"><span data-stu-id="0b12e-307">**date_time_ptr** Pointer to resulting date</span></span>

### <a name="return-values"></a><span data-ttu-id="0b12e-308">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="0b12e-308">Return Values</span></span>
* <span data-ttu-id="0b12e-309">**NX_SUCCESS** (0x00) istemci başarıyla oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="0b12e-309">**NX_SUCCESS** (0x00) Client successfully created</span></span>
* <span data-ttu-id="0b12e-310">**Sonuç tarihi işaretçisi** (0xd03) geçersiz giriş parametresi</span><span class="sxs-lookup"><span data-stu-id="0b12e-310">**Pointer to resulting date** (0xD03) Invalid input parameter</span></span>
* <span data-ttu-id="0b12e-311">NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi</span><span class="sxs-lookup"><span data-stu-id="0b12e-311">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="0b12e-312">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="0b12e-312">Allowed From</span></span>
<span data-ttu-id="0b12e-313">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="0b12e-313">Threads</span></span>

### <a name="example"></a><span data-ttu-id="0b12e-314">Örnek</span><span class="sxs-lookup"><span data-stu-id="0b12e-314">Example</span></span>
```C
/* convert PTP time to UTC date and time */
status = nx_ptp_client_utility_convert_time_to_date(&tm, -ptp_utc_offset, &date);

/* If the time was successfully converted, status = NX_SUCCESS. */
```

## <a name="nx_ptp_client_utility_time_diff"></a><span data-ttu-id="0b12e-315">nx_ptp_client_utility_time_diff</span><span class="sxs-lookup"><span data-stu-id="0b12e-315">nx_ptp_client_utility_time_diff</span></span>

<span data-ttu-id="0b12e-316">İki PTP kez fark.</span><span class="sxs-lookup"><span data-stu-id="0b12e-316">Diff two PTP times.</span></span>

### <a name="prototype"></a><span data-ttu-id="0b12e-317">Prototype</span><span class="sxs-lookup"><span data-stu-id="0b12e-317">Prototype</span></span>

```C
UINT nx_ptp_client_utility_time_diff(
    NX_PTP_TIME *time1_ptr, 
    NX_PTP_TIME *time2_ptr, 
    NX_PTP_TIME *result_ptr);
```

### <a name="description"></a><span data-ttu-id="0b12e-318">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0b12e-318">Description</span></span>
<span data-ttu-id="0b12e-319">Bu hizmet iki MTP saati arasındaki farkı hesaplar.</span><span class="sxs-lookup"><span data-stu-id="0b12e-319">This service computes the difference between two PTP times.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="0b12e-320">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="0b12e-320">Input Parameters</span></span>
* <span data-ttu-id="0b12e-321">**time1_ptr** İlk PTP saati işaretçisi</span><span class="sxs-lookup"><span data-stu-id="0b12e-321">**time1_ptr** Pointer to first PTP time</span></span>
* <span data-ttu-id="0b12e-322">**time2_ptr** İkinci PTP saati işaretçisi</span><span class="sxs-lookup"><span data-stu-id="0b12e-322">**time2_ptr** Pointer to second PTP time</span></span>
* <span data-ttu-id="0b12e-323">**result_ptr** Result Time1-time2 işaretçisi</span><span class="sxs-lookup"><span data-stu-id="0b12e-323">**result_ptr** Pointer to result time1-time2</span></span>

### <a name="return-values"></a><span data-ttu-id="0b12e-324">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="0b12e-324">Return Values</span></span>
* <span data-ttu-id="0b12e-325">**NX_SUCCESS** (0x00) istemci başarıyla oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="0b12e-325">**NX_SUCCESS** (0x00) Client successfully created</span></span>
* <span data-ttu-id="0b12e-326">NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi</span><span class="sxs-lookup"><span data-stu-id="0b12e-326">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="0b12e-327">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="0b12e-327">Allowed From</span></span>
<span data-ttu-id="0b12e-328">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="0b12e-328">Threads</span></span>

### <a name="example"></a><span data-ttu-id="0b12e-329">Örnek</span><span class="sxs-lookup"><span data-stu-id="0b12e-329">Example</span></span>
```C
/* Diff time.  */
status = nx_ptp_client_utility_time_diff(&time1, &time2, &result);

/* If the calculation was successfully, status = NX_SUCCESS. */
```