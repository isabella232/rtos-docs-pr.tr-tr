---
title: Ek A-Azure RTOS NetX Duo DHCPv6 Istemcisi için geri yükleme durumu özelliğinin açıklaması
description: Azure RTOS NetX Duo DHDPv6 Istemci yapılandırma seçeneği NX_DHCPV6_CLIENT_RESTORE_STATE, sistemin önceden oluşturulmuş bir DHCP Istemcisini sistem yeniden başlatmalar arasında bir bağlantılı durumda geri yüklemesine olanak tanır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 3e642af158202bb3b2a4e2a37397b47d707b566e
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826099"
---
# <a name="appendix-a---description-of-the-restore-state-feature-for-azure-rtos-netx-duo-dhcpv6-client"></a><span data-ttu-id="9d6b3-103">Ek A-Azure RTOS NetX Duo DHCPv6 Istemcisi için geri yükleme durumu özelliğinin açıklaması</span><span class="sxs-lookup"><span data-stu-id="9d6b3-103">Appendix A - Description of the Restore State Feature for Azure RTOS NetX Duo DHCPv6 Client</span></span>

<span data-ttu-id="9d6b3-104">Azure RTOS NetX Duo DHDPv6 Istemci yapılandırma seçeneği NX_DHCPV6_CLIENT_RESTORE_STATE, sistemin önceden oluşturulmuş bir DHCP Istemcisini sistem yeniden başlatmalar arasında bir bağlantılı durumda geri yüklemesine olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="9d6b3-104">The Azure RTOS NetX Duo DHDPv6 Client configuration option, NX_DHCPV6_CLIENT_RESTORE_STATE, allows a system to restore a previously created DHCP Client in a Bound state between system reboots.</span></span>

<span data-ttu-id="9d6b3-105">Bu seçenek ayrıca bir uygulamanın DHCPv6 Istemci iş parçacığını askıya almasına ve devam etmesine olanak tanır. Bu işlem, iş parçacığını kapatmadan askıya alma ve sürdürme arasındaki geçen süre ile güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="9d6b3-105">This option also allows an application to suspend the DHCPv6 Client thread and resume it, updated with the elapsed time between suspending and resuming the thread without powering down.</span></span>

## <a name="restoring-the-dhcpv6-client-between-reboots"></a><span data-ttu-id="9d6b3-106">Yeniden başlatmalar arasında DHCPv6 Istemcisini geri yükleme</span><span class="sxs-lookup"><span data-stu-id="9d6b3-106">Restoring the DHCPv6 Client between Reboots</span></span>

<span data-ttu-id="9d6b3-107">Bir DHCPv6 Istemcisini yeniden başlatmalar arasında geri yüklemek için, DHCPv6 uygulaması DHCPv6 Istemcisinin bir örneğini oluşturur ve ardından normal DHCPv6 protokolünü kullanarak bir IP adresi kirası edinir ve *nx_dhcpv6_start* çağırır.</span><span class="sxs-lookup"><span data-stu-id="9d6b3-107">To restore a DHCPv6 Client between reboots, the DHCPv6 application creates an instance of the DHCPv6 Client, and then obtains an IP address lease using the normal DHCPv6 protocol and calling *nx_dhcpv6_start*.</span></span> <span data-ttu-id="9d6b3-108">Ardından, DHCPv6 uygulaması protokolün tamamlanmasını bekler.</span><span class="sxs-lookup"><span data-stu-id="9d6b3-108">Then the DHCPv6 application waits for the protocol to complete.</span></span> <span data-ttu-id="9d6b3-109">Hepsi de varsa, cihaz, DHCPv6 sunucusundan atanan geçerli bir IP adresi ile bağlantılı duruma erişir.</span><span class="sxs-lookup"><span data-stu-id="9d6b3-109">If all goes well, the device achieves the BOUND state with an assigned valid IP address from its DHCPv6 Server.</span></span> <span data-ttu-id="9d6b3-110">DHCPv6 Istemci uygulaması, kapatmadan önce geçerli DHCPv6 Istemci örneğini, daha sonra geçici olmayan bellekte saklanan bir DHCPv6 Istemci kaydına kaydeder.</span><span class="sxs-lookup"><span data-stu-id="9d6b3-110">Before it powers down, the DHCPv6 Client application saves the current DHCPv6 Client instance to a DHCPv6 Client record which is then stored in non-volatile memory.</span></span> <span data-ttu-id="9d6b3-111">Sistemin başka bir yerindeki bağımsız bir ' Time Man ', bu güç durumundayken geçen sürenin izini tutar.</span><span class="sxs-lookup"><span data-stu-id="9d6b3-111">An independent ‘time keeper’ elsewhere in the system keeps track of the time elapsed during this powered down state.</span></span> <span data-ttu-id="9d6b3-112">Uygulama, yeni bir DHCPv6 Istemci örneği oluşturur ve daha önce oluşturulan DHCPv6 Istemci kaydıyla günceller.</span><span class="sxs-lookup"><span data-stu-id="9d6b3-112">On powering up, the application creates a new DHCPv6 Client instance, and then updates it with the previously created DHCPv6 Client record.</span></span> <span data-ttu-id="9d6b3-113">Geçen süre, "zaman Man" kaynağından alınır ve ardından DHCP Clientv6 kirası üzerinde kalan zamana uygulanır.</span><span class="sxs-lookup"><span data-stu-id="9d6b3-113">The elapsed time is obtained from the “time keeper” and then applied to the time remaining on the DHCP Clientv6 lease.</span></span> <span data-ttu-id="9d6b3-114">Bu noktada uygulama, DHCPv6 Istemcisini sürdürür.</span><span class="sxs-lookup"><span data-stu-id="9d6b3-114">At this point, the application can resume the DHCPv6 Client.</span></span>

<span data-ttu-id="9d6b3-115">Güç kapatma sırasında geçen süre DHCPv6 Istemci durumunu yenıleme veya yeniden bağlama durumuna geçirir, DHCPv6 Istemcisi IP adresi kiralamasını yenilemek veya yeniden bağlamak isteyen DHCPv6 iletilerini otomatik olarak başlatır.</span><span class="sxs-lookup"><span data-stu-id="9d6b3-115">If the time elapsed during power down puts the DHCPv6 Client state in either a RENEW or REBIND state, the DHCPv6 Client will automatically initiate DHCPv6 messages requesting to renew or rebind the IP address lease.</span></span> <span data-ttu-id="9d6b3-116">IP adresinin geçerliliği dolmuşsa, DHCPv6 Istemcisi IP örneğindeki IP adresini otomatik olarak temizler ve yeni bir IP adresi isteyen başlangıç durumundan DHCPv6 işlemini başlatır.</span><span class="sxs-lookup"><span data-stu-id="9d6b3-116">If the IP address is expired, the DHCPv6 Client will automatically clear the IP address on the IP instance and begin the DHCPv6 process from the INIT state, requesting a new IP address.</span></span>

<span data-ttu-id="9d6b3-117">Bu şekilde, DHCPv6 Istemcisi kesintisiz olarak yeniden başlatmalar arasında çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="9d6b3-117">In this manner the DHCPv6 Client can operate between reboots as if uninterrupted.</span></span>

<span data-ttu-id="9d6b3-118">Bu özelliğin bir çizimi aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="9d6b3-118">Below is an illustration of this feature.</span></span>

```C
/* On the power up, create an IP instance, DHCPv6 Client, enable ICMPv6 and UDP
   and other resources (not shown) for the DHCPv6 Client/application
   in tx_application_define(). */
 
/* Define the DHCPv6 Client application thread. */     
void    thread_dhcpv6_client_entry(ULONG thread_input)
{

UINT        status;
UINT        time_elapsed = 0;
NX_DHCPV6_CLIENT_RECORD client_my_record;


    /* No previously saved Client record. Start the DHCPv6 Client in the INIT state. */
    status =  nx_dhcpv6_start(&dhcp_0);

    if (status !=NX_SUCCESS)
        return;

    while(1)    
    {
    
        /* Wait for DHCPv6 Client to get the IP address. */
    }

    /* At some point decide we power down the system. */

    /* Save the Client state data which we will subsequently need to restore the DHCPv6    
       Client. */
    status = nx_dhcpv6_client_get_record(&dhcp_0, &client_my_record);               

    /* Copy this memory to non-volatile memory (not shown). */

    /* Delete the IP and DHCPv6 Client instances before powering down. */
    nx_dhcpv6_client_delete(&dhcp_0);

    nx_ip_delete(&ip_0);

    /* Ready to power down, having released other resources as necessary. */

    /* The application has determined there is a previously saved record. We will 
       restore it to the current DHCPv6 Client instance. */

/* Create the IP and DHCPv6 Client instances, enable ICMPv6 and UDP after powering up. */

/* Calculate the time elapsed during power down */

    /* Get the previous Client state data from non-volatile memory. */

    /* Apply the record to the current Client instance. This will also 
       update the IP instance with IP address, mask etc. */
    status = nx_dhcpv6_client_restore_record(&dhcp_0, &client_my_record, time_elapsed);   

     if (status != NX_SUCCESS)
          return;

     /* We are ready to resume the DHCPv6 Client thread and use the assigned IP address. */
     status = nx_dhcpv6_resume(&dhcp_0);

     if (status != NX_SUCCESS)
          return;

}
```

## <a name="nx_dhcpv6_client_get_record"></a><span data-ttu-id="9d6b3-119">nx_dhcpv6_client_get_record</span><span class="sxs-lookup"><span data-stu-id="9d6b3-119">nx_dhcpv6_client_get_record</span></span>

<span data-ttu-id="9d6b3-120">Geçerli DHCPv6 Istemci durumunun bir kaydını oluştur</span><span class="sxs-lookup"><span data-stu-id="9d6b3-120">Create a record of the current DHCPv6 Client state</span></span>

### <a name="prototype"></a><span data-ttu-id="9d6b3-121">Prototype</span><span class="sxs-lookup"><span data-stu-id="9d6b3-121">Prototype</span></span>

```C
ULONG nx_dhcpv6_client_get_record(NX_DHCPV6 *dhcpv6_ptr, 
                                  NX_DHCPV6_CLIENT_RECORD *record_ptr);
```

### <a name="description"></a><span data-ttu-id="9d6b3-122">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9d6b3-122">Description</span></span>

<span data-ttu-id="9d6b3-123">Bu hizmet, DHCPv6 Istemcisini record_ptr tarafından işaret edilen kayda kaydeder.</span><span class="sxs-lookup"><span data-stu-id="9d6b3-123">This service saves the DHCPv6 Client to the record pointed to by record_ptr.</span></span> <span data-ttu-id="9d6b3-124">Bu, DHCPv6 Istemci uygulamasının, bir güç kapatma ve yeniden başlatma gibi DHCPv6 Istemci durumunu geri yüklemesine olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="9d6b3-124">This allows the DHCPv6 Client application restore its DHCPv6 Client state after, for example, a power down and reboot.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9d6b3-125">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="9d6b3-125">Input Parameters</span></span>

- <span data-ttu-id="9d6b3-126">**dhcpv6_ptr** DHCPv6 Istemcisi işaretçisi</span><span class="sxs-lookup"><span data-stu-id="9d6b3-126">**dhcpv6_ptr** Pointer to DHCPv6 Client</span></span>

- <span data-ttu-id="9d6b3-127">**record_ptr** DHCPv6 Istemci kaydına yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="9d6b3-127">**record_ptr** Pointer to DHCPv6 Client record</span></span>

### <a name="return-values"></a><span data-ttu-id="9d6b3-128">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9d6b3-128">Return Values</span></span>

- <span data-ttu-id="9d6b3-129">**NX_SUCCESS (0x0)** Geçerli Istemci kaydı oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="9d6b3-129">**NX_SUCCESS (0x0)** Valid Client record created</span></span>

- <span data-ttu-id="9d6b3-130">**NX_DHCPV6_NOT_BOUND** (0xe94) istemci bağlantılı durumda değil, bu nedenle geçerli IP adresi atanmadı</span><span class="sxs-lookup"><span data-stu-id="9d6b3-130">**NX_DHCPV6_NOT_BOUND** (0xE94) Client not in bound state, therefore not assigned valid IP address</span></span>

- <span data-ttu-id="9d6b3-131">**NX_PTR_ERROR** (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="9d6b3-131">**NX_PTR_ERROR** (0x16) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9d6b3-132">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9d6b3-132">Allowed From</span></span>

<span data-ttu-id="9d6b3-133">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="9d6b3-133">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9d6b3-134">Örnek</span><span class="sxs-lookup"><span data-stu-id="9d6b3-134">Example</span></span>

```C
NX_DHCPV6_CLIENT_RECORD dhcpv6_record;


/* Obtain a record of the current client state. */
status=  nx_dhcpv6_client_get_record(&dhcpv6_ptr, &dhcpv6_record);

/* If status is NX_SUCCESS dhcpv6_record contains the current DHCPv6 client record. */
```

### <a name="see-also"></a><span data-ttu-id="9d6b3-135">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9d6b3-135">See Also</span></span>

- <span data-ttu-id="9d6b3-136">nx_dhcpv6_resume</span><span class="sxs-lookup"><span data-stu-id="9d6b3-136">nx_dhcpv6_resume</span></span>
- <span data-ttu-id="9d6b3-137">nx_dhcpv6_suspend</span><span class="sxs-lookup"><span data-stu-id="9d6b3-137">nx_dhcpv6_suspend</span></span>
- <span data-ttu-id="9d6b3-138">nx_dhcpv6_client_restore_record</span><span class="sxs-lookup"><span data-stu-id="9d6b3-138">nx_dhcpv6_client_restore_record</span></span>

## <a name="nx_dhcpv6_client_restore_record"></a><span data-ttu-id="9d6b3-139">nx_dhcpv6_client_restore_record</span><span class="sxs-lookup"><span data-stu-id="9d6b3-139">nx_dhcpv6_client_restore_record</span></span>

<span data-ttu-id="9d6b3-140">Kaydedilen kayıttaki DHCPv6 Istemci durumunu geri yükle</span><span class="sxs-lookup"><span data-stu-id="9d6b3-140">Restore DHCPv6 Client state from saved record</span></span>

### <a name="prototype"></a><span data-ttu-id="9d6b3-141">Prototype</span><span class="sxs-lookup"><span data-stu-id="9d6b3-141">Prototype</span></span>

```C
ULONG nx_dhcpv6_client_restore_record(NX_DHCPV6 *dhcpv6_ptr, 
                                      NX_DHCPV6_CLIENT_RECORD       
                                      *record_ptr, ULONG time_elapsed);
```

### <a name="description"></a><span data-ttu-id="9d6b3-142">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9d6b3-142">Description</span></span>

<span data-ttu-id="9d6b3-143">Bu hizmet, DHCPv6 istemcisini record_ptr tarafından işaret edilen DHCPv6 istemci kaydıyla güncelleyerek ve DHCPv6 Istemci Kiralama üzerinde kalan süreyi time_elapsed girişi ile güncelleştirerek, bir DHCPv6 uygulamasının DHCPv6 Istemci durumunu önceki bir oturumdan yeniden oluşturmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="9d6b3-143">This service enables a DHCPv6 application to recreate its DHCPv6 Client state from a previous session by updating the DHCPv6 Client with the DHCPv6 Client record pointed to by record_ptr, and updates the time remaining on DHCPv6 Client lease with the time_elapsed input.</span></span> <span data-ttu-id="9d6b3-144">Bu, DHCPv6 Istemci uygulamasının, DHCPv6 Istemcisini yeniden oluşturmasını sağlar, örneğin, kapatıldıktan sonra.</span><span class="sxs-lookup"><span data-stu-id="9d6b3-144">This allows the DHCPv6 Client application to recreate its DHCPv6 Client, for example, after powering down.</span></span> <span data-ttu-id="9d6b3-145">Bu, DHCPv6 Istemci uygulamasının kapatmadan önce DHCPv6 Istemcisinin bir kaydını oluşturulmasını ve bu kaydın geçici olmayan belleğe kaydedilmesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="9d6b3-145">This requires that the DHCPv6 Client application created a record of the DHCPv6 Client before powering down, and saved that record to non-volatile memory.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9d6b3-146">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="9d6b3-146">Input Parameters</span></span>

- <span data-ttu-id="9d6b3-147">**dhcpv6_ptr** DHCPv6 Istemcisi işaretçisi</span><span class="sxs-lookup"><span data-stu-id="9d6b3-147">**dhcpv6_ptr** Pointer to DHCPv6 Client</span></span>

- <span data-ttu-id="9d6b3-148">**record_ptr** DHCPv6 Istemci kaydına yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="9d6b3-148">**record_ptr** Pointer to DHCPv6 Client record</span></span>

- <span data-ttu-id="9d6b3-149">**time_elapsed** Giriş istemci kaydında kalan kira zamanından çıkarma süresi</span><span class="sxs-lookup"><span data-stu-id="9d6b3-149">**time_elapsed** Time to subtract from the lease time remaining in the input client record</span></span>

### <a name="return-values"></a><span data-ttu-id="9d6b3-150">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9d6b3-150">Return Values</span></span>

- <span data-ttu-id="9d6b3-151">**NX_SUCCESS (0x0)** İstemci kaydı geri yüklendi</span><span class="sxs-lookup"><span data-stu-id="9d6b3-151">**NX_SUCCESS (0x0)** Client record restored</span></span>

- <span data-ttu-id="9d6b3-152">NX_PTR_ERROR (0x16) geçersiz Işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="9d6b3-152">NX_PTR_ERROR (0x16) Invalid Pointer Input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9d6b3-153">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9d6b3-153">Allowed From</span></span>

<span data-ttu-id="9d6b3-154">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="9d6b3-154">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9d6b3-155">Örnek</span><span class="sxs-lookup"><span data-stu-id="9d6b3-155">Example</span></span>

```C
NX_DHCPV6_CLIENT_RECORD dhcpv6_record;
ULONG       time_elapsed;

/* Obtain time (timer ticks) elapsed from independent time keeper. */
time_elapsed = /* to be determined by application */ 1000; 

/* Obtain a record of the current client state. */
status=  nx_dhcpv6_client_restore_record(&dhcpv6_ptr, &dhcpv6_record, time_elapsed);

/* If status is NX_SUCCESS the current DHCPv6 Client pointed to by dhcpv6_ptr contains the current client record updated for time elapsed during power down. */
```

### <a name="see-also"></a><span data-ttu-id="9d6b3-156">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9d6b3-156">See Also</span></span>

- <span data-ttu-id="9d6b3-157">nx_dhcpv6_client_get_record</span><span class="sxs-lookup"><span data-stu-id="9d6b3-157">nx_dhcpv6_client_get_record</span></span>