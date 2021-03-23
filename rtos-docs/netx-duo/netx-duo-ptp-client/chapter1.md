---
title: Bölüm 1-Azure RTOS NetX Duo MTP Istemcisine giriş
description: Bu bölümde, Azure RTOS NetX Duo MTP Istemcisine giriş yer almaktadır.
author: v-condav
ms.author: v-condav
ms.date: 01/27/2021
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 5beec64bd6d74e3bed06be15255d6bd4a940ba64
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825805"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-ptp-client"></a><span data-ttu-id="51c4c-103">Bölüm 1-Azure RTOS NetX Duo MTP Istemcisine giriş</span><span class="sxs-lookup"><span data-stu-id="51c4c-103">Chapter 1 - Introduction to Azure RTOS NetX Duo PTP Client</span></span>

<span data-ttu-id="51c4c-104">Azure RTOS NetX Duo PTP, Precision Time Protocol (PTP) sürüm 2 ' nin (IEEE 1588-2008) istemci bölümünü uygular.</span><span class="sxs-lookup"><span data-stu-id="51c4c-104">The Azure RTOS NetX Duo PTP implements the client part of the Precision Time Protocol (PTP) version 2, IEEE 1588-2008.</span></span> <span data-ttu-id="51c4c-105">IPv4 veya IPv6 çok noktaya yayın paketleri aracılığıyla birbirleriyle iletişim kurarak yerel ağdaki mus 'Lar arasındaki saatleri eşleştirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="51c4c-105">It is used to synchronize clocks among MCUs on the local network by communicating each other via IPv4 or IPv6 multicast packets.</span></span>

## <a name="netx-duo-ptp-client-setup"></a><span data-ttu-id="51c4c-106">NetX Duo PTP Istemci kurulumu</span><span class="sxs-lookup"><span data-stu-id="51c4c-106">NetX Duo PTP Client Setup</span></span>

<span data-ttu-id="51c4c-107">Doğru çalışması için, PTP istemci paketi bir NetX Duo IP örneğinin zaten oluşturulmuş olmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="51c4c-107">In order to function properly, the PTP client package requires that a NetX Duo IP instance has already been created.</span></span>

<span data-ttu-id="51c4c-108">Varsayılan olarak, PTP istemcisi IPv4 çok noktaya yayın grubunu birleştirir.</span><span class="sxs-lookup"><span data-stu-id="51c4c-108">By default, the PTP client joins IPv4 multicast group.</span></span> <span data-ttu-id="51c4c-109">PTP Client 'ı bir IPv6 ağında çalıştırmak için, `NX_ENABLE_IPV6_MULTICAST` NetX Duo kitaplığı oluşturulurken tanımlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="51c4c-109">In order to run the PTP client on an IPv6 network, `NX_ENABLE_IPV6_MULTICAST` must be defined when building NetX Duo library.</span></span>

<span data-ttu-id="51c4c-110">PTP istemcisini oluştururken, uygulamanın gelen ve giden paketlerin zaman damgalarını işlemek için bir geri çağırma işlevi sağlaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="51c4c-110">When creating the PTP client, the application must provide a callback function to handle timestamps of incoming and outgoing packets.</span></span> <span data-ttu-id="51c4c-111">Yüksek çözünürlüğe ulaşmak için uygulamaların yüksek çözünürlüklü bir Zamanlayıcı kullanarak zaman damgası oluşturmasını öneririz.</span><span class="sxs-lookup"><span data-stu-id="51c4c-111">To achieve high resolution, we recommend applications to generate timestamps using a high resolution timer.</span></span> <span data-ttu-id="51c4c-112">PTP on simülatörünü çalıştırmak için, yazılım tabanlı bir uygulama `nx_ptp_client_soft_clock_callback` sağlanır.</span><span class="sxs-lookup"><span data-stu-id="51c4c-112">To run the PTP on simulator, a software-based implementation `nx_ptp_client_soft_clock_callback` is provided.</span></span>

<span data-ttu-id="51c4c-113">PTP Client, PTP iletileri iletmek için bir paket havuzu gerektirir.</span><span class="sxs-lookup"><span data-stu-id="51c4c-113">The PTP client requires a packet pool for transmitting PTP messages.</span></span> <span data-ttu-id="51c4c-114">Paket havuzunun yük boyutu `NX_UDP_PACKET + NX_PTP_CLIENT_PACKET_DATA_SIZE` , IPv4 için 108 bayt ve IPv6 etkinse 128 bayt olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51c4c-114">The payload size of packet pool must be no less than `NX_UDP_PACKET + NX_PTP_CLIENT_PACKET_DATA_SIZE`, which is 108 bytes for IPv4, and 128 bytes if IPv6 is enabled.</span></span>

<span data-ttu-id="51c4c-115">PTP Istemcisini oluşturduktan sonra uygulama, PTP istemcisini başlatabilir.</span><span class="sxs-lookup"><span data-stu-id="51c4c-115">After creating the PTP Client, the application can start the PTP client.</span></span> <span data-ttu-id="51c4c-116">Eşitleme, PTP Yardımcısı iş parçacığında yapılır.</span><span class="sxs-lookup"><span data-stu-id="51c4c-116">The synchronization is done in the PTP helper thread.</span></span> <span data-ttu-id="51c4c-117">Olay geri çağırma işlevi belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="51c4c-117">An event callback function can be specified.</span></span> <span data-ttu-id="51c4c-118">Aşağıdaki olaylardan herhangi biri gerçekleştiğinde çağrılacaktır.</span><span class="sxs-lookup"><span data-stu-id="51c4c-118">It will be invoked when any one of the following events happen.</span></span>
* <span data-ttu-id="51c4c-119">Ana öğe seçildi;</span><span class="sxs-lookup"><span data-stu-id="51c4c-119">A master is selected;</span></span> 
* <span data-ttu-id="51c4c-120">Süre ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="51c4c-120">The time is calibrated.</span></span>
* <span data-ttu-id="51c4c-121">Ana zaman aşımı.</span><span class="sxs-lookup"><span data-stu-id="51c4c-121">A master times out.</span></span>

## <a name="netx-duo-ptp-client-messages"></a><span data-ttu-id="51c4c-122">NetX Duo PTP Istemci Iletileri</span><span class="sxs-lookup"><span data-stu-id="51c4c-122">NetX Duo PTP Client Messages</span></span>

<span data-ttu-id="51c4c-123">NetX Duo MTP istemcisi yalnızca gecikmeli istek-yanıt mekanizmasını uygular.</span><span class="sxs-lookup"><span data-stu-id="51c4c-123">The NetX Duo PTP client implements the delay request-response mechanism only.</span></span> <span data-ttu-id="51c4c-124">PTP istemcisi iki UDP bağlantı noktasını açar.</span><span class="sxs-lookup"><span data-stu-id="51c4c-124">The PTP client  opens two UDP ports.</span></span> <span data-ttu-id="51c4c-125">*319* **olay** iletisi için ve **genel** ileti için *320* .</span><span class="sxs-lookup"><span data-stu-id="51c4c-125">*319* for **event** message and *320* for **general** message.</span></span> <span data-ttu-id="51c4c-126">Bu mekanizma için beş tür ileti vardır.</span><span class="sxs-lookup"><span data-stu-id="51c4c-126">There are five types of message for this mechanism.</span></span>

* <span data-ttu-id="51c4c-127">**Duyurur**.</span><span class="sxs-lookup"><span data-stu-id="51c4c-127">**Announce**.</span></span> <span data-ttu-id="51c4c-128">Bu bir olay iletisidir.</span><span class="sxs-lookup"><span data-stu-id="51c4c-128">This is an event message.</span></span> <span data-ttu-id="51c4c-129">Ana saat seçimi için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="51c4c-129">It is used for master clock selection.</span></span>
* <span data-ttu-id="51c4c-130">**Eşitleme**. Bu bir olay iletisidir.</span><span class="sxs-lookup"><span data-stu-id="51c4c-130">**Sync**. This is an event message.</span></span> <span data-ttu-id="51c4c-131">Kaynak zaman damgası göndermek ve ana sunucudan istemciye yol gecikmesini hesaplamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="51c4c-131">It is used to send origin timestamp and calculate the path delay from master to client.</span></span>
* <span data-ttu-id="51c4c-132">**Follow_Up**.</span><span class="sxs-lookup"><span data-stu-id="51c4c-132">**Follow_Up**.</span></span> <span data-ttu-id="51c4c-133">Bu, genel bir iletidir.</span><span class="sxs-lookup"><span data-stu-id="51c4c-133">This is a general message.</span></span> <span data-ttu-id="51c4c-134">Bu, isteğe bağlıdır ve ilgili eşitleme iletisindeki kaynak zaman damgasını düzeltmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="51c4c-134">It is optional and used to correct the origin timestamp in related Sync message.</span></span> <span data-ttu-id="51c4c-135">Yalnızca eşitleme bayrağıyla birlikte iki adımlı bit ayarlandığında gönderilir.</span><span class="sxs-lookup"><span data-stu-id="51c4c-135">It is sent only when the two step bit in Sync flag is set.</span></span>
* <span data-ttu-id="51c4c-136">**Delay_Req**.</span><span class="sxs-lookup"><span data-stu-id="51c4c-136">**Delay_Req**.</span></span> <span data-ttu-id="51c4c-137">Bu bir olay iletisidir.</span><span class="sxs-lookup"><span data-stu-id="51c4c-137">This is an event message.</span></span> <span data-ttu-id="51c4c-138">Delay_Resp alma sırasında istemciden ana kadar yol gecikmesini hesaplamak için PTP istemcisinden gönderilir.</span><span class="sxs-lookup"><span data-stu-id="51c4c-138">It is sent from PTP client to calculate the path delay from client to master, on receiving Delay_Resp.</span></span>
* <span data-ttu-id="51c4c-139">**Delay_Resp**.</span><span class="sxs-lookup"><span data-stu-id="51c4c-139">**Delay_Resp**.</span></span> <span data-ttu-id="51c4c-140">Bu bir olay iletisidir.</span><span class="sxs-lookup"><span data-stu-id="51c4c-140">This is an event message.</span></span> <span data-ttu-id="51c4c-141">İstemciden istemciye yol gecikmesini hesaplamak için ana sunucudan istemciye gönderilir.</span><span class="sxs-lookup"><span data-stu-id="51c4c-141">It is sent from master to client to calculate the path delay from client to master.</span></span>

<span data-ttu-id="51c4c-142">*Not, "en iyi ana saat" algoritması uygulanmadı. PTP istemcisi dinleme durumundayken yalnızca ilk ana saat kabul edilir.*</span><span class="sxs-lookup"><span data-stu-id="51c4c-142">*Note, "best master clock" algorithm is not implemented. Only the first master clock is accepted when the PTP client is in listening state.*</span></span>

## <a name="netx-duo-ptp-client-clock-callback"></a><span data-ttu-id="51c4c-143">NetX Duo PTP Istemci saati geri araması</span><span class="sxs-lookup"><span data-stu-id="51c4c-143">NetX Duo PTP Client Clock Callback</span></span>
<span data-ttu-id="51c4c-144">Saati ana sunucudan eşleştirmek için, PTP istemcisinin yerel bir saat olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="51c4c-144">To synchronize clock from master, PTP client needs a local clock.</span></span> <span data-ttu-id="51c4c-145">Bir saat geri çağırma işlevi, oluşturma sırasında PTP Client 'a geçirilir.</span><span class="sxs-lookup"><span data-stu-id="51c4c-145">A clock callback function is passed into PTP client during creation.</span></span> <span data-ttu-id="51c4c-146">Saat geri çağırma yordamının biçimi aşağıda tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="51c4c-146">The format of the clock callback routine is  defined below.</span></span>
```C
UINT ptp_clock_callback(
    NX_PTP_CLIENT *client_ptr, 
    UINT operation,
    NX_PTP_TIME *time_ptr, 
    NX_PACKET *packet_ptr,
    VOID *callback_data);
```
<span data-ttu-id="51c4c-147">Giriş parametreleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="51c4c-147">The input parameters are defined as follows:</span></span>
* <span data-ttu-id="51c4c-148">*client_ptr* , PTP istemcisine işaret eder.</span><span class="sxs-lookup"><span data-stu-id="51c4c-148">*client_ptr* points to PTP client.</span></span>
* <span data-ttu-id="51c4c-149">*işlem* , geri çağırma işlemini belirtir; geçerli değerler aşağıdaki listede gösterildiği gibi tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="51c4c-149">*operation* specifies the callback operation, valid values are defined as shown in the list below.</span></span>
  * <span data-ttu-id="51c4c-150">**NX_PTP_CLIENT_CLOCK_INIT** Saati başlatın.</span><span class="sxs-lookup"><span data-stu-id="51c4c-150">**NX_PTP_CLIENT_CLOCK_INIT** Initialize clock.</span></span>
  * <span data-ttu-id="51c4c-151">**NX_PTP_CLIENT_CLOCK_SET** Tarafından belirtilen geçerli zaman damgasını ayarla `time_ptr` .</span><span class="sxs-lookup"><span data-stu-id="51c4c-151">**NX_PTP_CLIENT_CLOCK_SET** Set current timestamp specified by `time_ptr`.</span></span>
  * <span data-ttu-id="51c4c-152">**NX_PTP_CLIENT_CLOCK_GET** Geçerli zaman damgasını döndürür `time_ptr` .</span><span class="sxs-lookup"><span data-stu-id="51c4c-152">**NX_PTP_CLIENT_CLOCK_GET** Return current timestamp to `time_ptr`.</span></span>
  * <span data-ttu-id="51c4c-153">**NX_PTP_CLIENT_CLOCK_PACKET_TS_EXTRACT** Zaman damgasını konumundan `packet_ptr` ayıklayın `time_ptr` .</span><span class="sxs-lookup"><span data-stu-id="51c4c-153">**NX_PTP_CLIENT_CLOCK_PACKET_TS_EXTRACT** Extract timestamp from `packet_ptr` to `time_ptr`.</span></span>
  * <span data-ttu-id="51c4c-154">**NX_PTP_CLIENT_CLOCK_ADJUST** Geçerli zaman damgasını *1* saniyeden az ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="51c4c-154">**NX_PTP_CLIENT_CLOCK_ADJUST** Adjust current timestamp less than *1* second.</span></span>
  * <span data-ttu-id="51c4c-155">**NX_PTP_CLIENT_CLOCK_PACKET_TS_PREPARE** `packet_ptr` PTP Client ' ın aktarıldığı zaman damgasına bildirilmesini gerektiren öğesini işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="51c4c-155">**NX_PTP_CLIENT_CLOCK_PACKET_TS_PREPARE** Mark the `packet_ptr` which requires to notify PTP client the timestamp when it is transmitted.</span></span>
  * <span data-ttu-id="51c4c-156">**NX_PTP_CLIENT_CLOCK_SOFT_TIMER_UPDATE** Geçici zamanlayıcıyı güncelleştir.</span><span class="sxs-lookup"><span data-stu-id="51c4c-156">**NX_PTP_CLIENT_CLOCK_SOFT_TIMER_UPDATE** Update soft timer.</span></span> <span data-ttu-id="51c4c-157">Bu, donanım saati tarafından yoksayılabilir.</span><span class="sxs-lookup"><span data-stu-id="51c4c-157">It can be ignored by hardware clock.</span></span>
* <span data-ttu-id="51c4c-158">*time_ptr* zaman damgasına işaret eder.</span><span class="sxs-lookup"><span data-stu-id="51c4c-158">*time_ptr* points to timestamp.</span></span>
* <span data-ttu-id="51c4c-159">*packet_ptr* pakete işaret eder.</span><span class="sxs-lookup"><span data-stu-id="51c4c-159">*packet_ptr* points to packet.</span></span>
* <span data-ttu-id="51c4c-160">*callback_data* , opak geri çağırma verilerine işaret eder.</span><span class="sxs-lookup"><span data-stu-id="51c4c-160">*callback_data* points to opaque callback data.</span></span>

<span data-ttu-id="51c4c-161">NX_PTP_TIME veri türü aşağıdaki gibi tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="51c4c-161">The NX_PTP_TIME data type is defined as follows.</span></span>
```C
typedef struct NX_PTP_TIME_STRUCT
{
    /* The MSB of the number of seconds */
    LONG  second_high;

    /* The LSB of the number of seconds */
    ULONG second_low;

    /* The number of nanoseconds */
    LONG  nanosecond;
} NX_PTP_TIME;
```

## <a name="netx-duo-ptp-client-event-callback"></a><span data-ttu-id="51c4c-162">NetX Duo PTP Istemci olayı geri çağırması</span><span class="sxs-lookup"><span data-stu-id="51c4c-162">NetX Duo PTP Client Event Callback</span></span>
<span data-ttu-id="51c4c-163">Olay geri çağırma işlevi, uygulamayı MTP istemcisinin durumuna bildirmek için ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="51c4c-163">The event callback function can be setup to notify application the state of PTP client.</span></span> <span data-ttu-id="51c4c-164">Olay geri çağırma yordamının biçimi aşağıda gösterildiği gibi tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="51c4c-164">The format of the event callback routine is defined as shown below.</span></span>
```C
UINT event_callback(
    NX_PTP_CLIENT *client_ptr, 
    UINT event, 
    VOID *event_data, 
    VOID *callback_data);
```
<span data-ttu-id="51c4c-165">Giriş parametreleri.</span><span class="sxs-lookup"><span data-stu-id="51c4c-165">The input parameters are.</span></span>
* <span data-ttu-id="51c4c-166">*client_ptr* , PTP istemcisine işaret eder.</span><span class="sxs-lookup"><span data-stu-id="51c4c-166">*client_ptr* points to PTP client.</span></span>
* <span data-ttu-id="51c4c-167">*olay* , geri çağırma olayını belirtir, geçerli değerler şu şekilde tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="51c4c-167">*event* specifies the callback event, valid values are defined as:</span></span>
  * <span data-ttu-id="51c4c-168">**NX_PTP_CLIENT_EVENT_MASTER** Ana saat seçilidir.</span><span class="sxs-lookup"><span data-stu-id="51c4c-168">**NX_PTP_CLIENT_EVENT_MASTER** A master clock is selected.</span></span>
  * <span data-ttu-id="51c4c-169">**NX_PTP_CLIENT_EVENT_SYNC** PTP Client kalibre edilir.</span><span class="sxs-lookup"><span data-stu-id="51c4c-169">**NX_PTP_CLIENT_EVENT_SYNC** PTP client is calibrated.</span></span>
  * <span data-ttu-id="51c4c-170">**NX_PTP_CLIENT_EVENT_TIMEOUT** Ana saat zaman aşımı.</span><span class="sxs-lookup"><span data-stu-id="51c4c-170">**NX_PTP_CLIENT_EVENT_TIMEOUT** Master clock is timeout.</span></span>
* <span data-ttu-id="51c4c-171">*event_data* olayla ilgili verileri belirtir.</span><span class="sxs-lookup"><span data-stu-id="51c4c-171">*event_data* specifies the data related to event.</span></span> <span data-ttu-id="51c4c-172">Olay **NX_PTP_CLIENT_EVENT_MASTER** olduğunda, event_data örneğe işaret eder `NX_PTP_CLIENT_MASTER` .</span><span class="sxs-lookup"><span data-stu-id="51c4c-172">When event is **NX_PTP_CLIENT_EVENT_MASTER**, event_data points to `NX_PTP_CLIENT_MASTER` instance.</span></span> <span data-ttu-id="51c4c-173">Olay **NX_PTP_CLIENT_EVENT_SYNC** olduğunda, olay verileri örneğe işaret eder `NX_PTP_CLIENT_SYNC` .</span><span class="sxs-lookup"><span data-stu-id="51c4c-173">When event is **NX_PTP_CLIENT_EVENT_SYNC**, event data points to `NX_PTP_CLIENT_SYNC` instance.</span></span>

## <a name="netx-duo-ptp-client-communication"></a><span data-ttu-id="51c4c-174">NetX Duo PTP Istemci Iletişimi</span><span class="sxs-lookup"><span data-stu-id="51c4c-174">NetX Duo PTP Client Communication</span></span>
<span data-ttu-id="51c4c-175">Daha önce de belirtildiği gibi, NetX Duo MTP istemcisi yalnızca gecikmeli istek-yanıt mekanizmasını destekler.</span><span class="sxs-lookup"><span data-stu-id="51c4c-175">As mentioned previously, NetX Duo PTP client only supports delay request-response mechanism.</span></span> <span data-ttu-id="51c4c-176">Bu mekanizma, istemci ile ana saat arasındaki ortalama yol gecikmesini aşağıda gösterildiği gibi ölçer:</span><span class="sxs-lookup"><span data-stu-id="51c4c-176">This mechanism measures the mean path delay between the client and the master clock as below:</span></span>
1. <span data-ttu-id="51c4c-177">İstemci ana bilgisayardan *duyuru* iletisi alır ve en iyi ana öğe olarak seçer.</span><span class="sxs-lookup"><span data-stu-id="51c4c-177">Client receives *Announce* message from master and select it as best master.</span></span>
1. <span data-ttu-id="51c4c-178">İstemci, ana bilgisayardan *eşitleme* iletisi alır.</span><span class="sxs-lookup"><span data-stu-id="51c4c-178">Client receives *Sync* message from master.</span></span> <span data-ttu-id="51c4c-179">*T1* zaman damgası, bu iletideki kaynak zaman damgasıdır.</span><span class="sxs-lookup"><span data-stu-id="51c4c-179">The timestamp *t1* is the origin timestamp in this message.</span></span> <span data-ttu-id="51c4c-180">Bu ileti alındığında *T2* zaman damgası olarak yerel saatten okundu.</span><span class="sxs-lookup"><span data-stu-id="51c4c-180">The timestamp *t2* is read from local clock when this message is received.</span></span>
1. <span data-ttu-id="51c4c-181">İstemci ana bilgisayardan *Follow_Up* ileti alır.</span><span class="sxs-lookup"><span data-stu-id="51c4c-181">Client receives *Follow_Up* message from master.</span></span> <span data-ttu-id="51c4c-182">Bu ileti isteğe bağlıdır ve yalnızca iki adım *eşitleme* bayrağıyla ayarlandığında geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="51c4c-182">This message is optional and valid only when two step in *Sync* flag is set.</span></span> <span data-ttu-id="51c4c-183">Sonra zaman damgası *T1* , bu iletideki kaynak zaman damgasına güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="51c4c-183">Then the timestamp *t1* is updated to the origin timestamp in this message.</span></span>
1. <span data-ttu-id="51c4c-184">İstemci ana sunucuya *Delay_Req* ileti gönderir.</span><span class="sxs-lookup"><span data-stu-id="51c4c-184">Client sends *Delay_Req* message to master.</span></span> <span data-ttu-id="51c4c-185">İleti aktarıldığında *T3* zaman damgası yerel saatten okunurdur.</span><span class="sxs-lookup"><span data-stu-id="51c4c-185">The timestamp *t3* is read from local clock when the message is transmitted.</span></span>
1. <span data-ttu-id="51c4c-186">İstemci ana bilgisayardan *Delay_Resp* ileti alır.</span><span class="sxs-lookup"><span data-stu-id="51c4c-186">Client receives *Delay_Resp* message from master.</span></span> <span data-ttu-id="51c4c-187">*T4* zaman damgası bu iletideki alma zaman damgasıdır.</span><span class="sxs-lookup"><span data-stu-id="51c4c-187">The timestamp *t4* is the receive timestamp in this message.</span></span>

<span data-ttu-id="51c4c-188">Ortalama yol gecikmesi aşağıda gösterildiği gibi hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="51c4c-188">The mean path delay is computed as shown below.</span></span>
```C
<meanPathDelay>=[(t2-t1)+(t4-t3)]/2
```
<span data-ttu-id="51c4c-189">Ana sunucudan gelen fark aşağıda gösterildiği gibi hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="51c4c-189">The offset from master is computed as shown below.</span></span>
```C
<offsetFromMaster>=client_clock-master_clock
                  =(t2-t1)-<meanPathDelay>
```

> [!NOTE]
> <span data-ttu-id="51c4c-190">\***CorrectionField** _, Calculation._ sırasında yok sayılır</span><span class="sxs-lookup"><span data-stu-id="51c4c-190">\*The \***correctionField** _ is ignored during the calculation._</span></span>