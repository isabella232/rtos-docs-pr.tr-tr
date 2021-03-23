---
title: Ek A-geri yükleme durumu özelliğinin açıklaması
description: Azure RTOS NetX DHDP Istemci yapılandırma seçeneği, NX_DHCP_CLIENT_RESTORE_STATE, sistemin önceden oluşturulmuş bir DHCP Istemci kaydını sistem yeniden başlatmalar arasında bir bağlantılı durumda geri yüklemesine olanak tanır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: be8b5dc4885951bee3dba38af6fe5e21b81aa767
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826807"
---
# <a name="appendix-a---description-of-the-restore-state-feature"></a><span data-ttu-id="b6462-103">Ek A-geri yükleme durumu özelliğinin açıklaması</span><span class="sxs-lookup"><span data-stu-id="b6462-103">Appendix A - Description of the Restore State Feature</span></span>

<span data-ttu-id="b6462-104">Azure RTOS NetX DHDP Istemci yapılandırma seçeneği, NX_DHCP_CLIENT_RESTORE_STATE, sistemin önceden oluşturulmuş bir DHCP Istemci kaydını sistem yeniden başlatmalar arasında bir bağlantılı durumda geri yüklemesine olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="b6462-104">The Azure RTOS NetX DHDP Client configuration option, NX_DHCP_CLIENT_RESTORE_STATE, allows a system to restore a previously created DHCP Client Record in a Bound state between system reboots.</span></span>

<span data-ttu-id="b6462-105">Bu seçenek etkinleştirildiğinde, uygulama DHCP Istemci iş parçacığını askıya alabilir ve sürdürebilir.</span><span class="sxs-lookup"><span data-stu-id="b6462-105">When this option is enabled, the application can suspend and resume the DHCP Client thread.</span></span> <span data-ttu-id="b6462-106">DHCP Istemcisini, iş parçacığını askıya alma ve sürdürme arasındaki geçen süre ile güncelleştirmek için de bir hizmet vardır.</span><span class="sxs-lookup"><span data-stu-id="b6462-106">There is also a service to update the DHCP Client with the elapsed time between suspending and resuming the thread.</span></span>

## <a name="restoring-the-dhcp-client-between-reboots"></a><span data-ttu-id="b6462-107">Yeniden başlatmalar arasında DHCP Istemcisini geri yükleme</span><span class="sxs-lookup"><span data-stu-id="b6462-107">Restoring the DHCP Client between Reboots</span></span>

<span data-ttu-id="b6462-108">Yeniden başlatmadan sonra bir DHCP Istemcisini geri yüklemeden önce, daha önce oluşturulmuş bir DHCP Istemcisi, bağlantılı duruma ulaşmalıdır ve DHCP sunucusundan bir IP adresi atanır.</span><span class="sxs-lookup"><span data-stu-id="b6462-108">Before restoring a DHCP Client after rebooting, a previously created DHCP Client that must reach the Bound state and be is assigned an IP address from the DHCP server.</span></span> <span data-ttu-id="b6462-109">Kapatmadan önce, DHCP uygulamasının geçerli DHCP Istemci kaydını geçici olmayan belleğe kaydetmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="b6462-109">Before it powers down, the DHCP application must then save the current DHCP Client record to non-volatile memory.</span></span> <span data-ttu-id="b6462-110">Bu güç durumu sırasında geçen süreyi izlemek için, sistemde başka bir yerde bağımsız bir ' Time Man ' olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b6462-110">There must also be an independent ‘time keeper’ elsewhere in the system to keep track of the time elapsed during this powered down state.</span></span> <span data-ttu-id="b6462-111">Uygulama, yeni bir DHCP Istemci örneği oluşturur ve daha önce oluşturulan DHCP Istemci kaydıyla günceller.</span><span class="sxs-lookup"><span data-stu-id="b6462-111">On powering up, the application creates a new DHCP Client instance, and then updates it with the previously created DHCP Client record.</span></span> <span data-ttu-id="b6462-112">Geçen süre, "zaman Man" kaynağından alınır ve DHCP Istemcisi kiralamasında kalan zamana uygulanır.</span><span class="sxs-lookup"><span data-stu-id="b6462-112">The elapsed time is obtained from the “time keeper” and then applied to the time remaining on the DHCP Client lease.</span></span> <span data-ttu-id="b6462-113">Bu, DHCP Istemcisinin, örneğin, yenıleme göre, durumları değiştirmesine neden olabileceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b6462-113">Note that this may cause the DHCP Client to change states e.g. from BOUND to RENEWING.</span></span> <span data-ttu-id="b6462-114">Bu noktada, uygulama DHCP Istemcisini sürdürür.</span><span class="sxs-lookup"><span data-stu-id="b6462-114">At this point, the application can resume the DHCP Client.</span></span>

<span data-ttu-id="b6462-115">Güç kapatma sırasında geçen süre DHCP Istemci durumunu yenıleme ya da yeniden bağlama durumuna geçirir, DHCP Istemcisi IP adresi kiralamasını yenilemek veya yeniden bağlamak isteyen DHCP iletilerini otomatik olarak başlatır.</span><span class="sxs-lookup"><span data-stu-id="b6462-115">If the time elapsed during power down puts the DHCP Client state in either a RENEW or REBIND state, the DHCP Client will automatically initiate DHCP messages requesting to renew or rebind the IP address lease.</span></span> <span data-ttu-id="b6462-116">IP adresinin geçerliliği dolmuşsa, DHCP Istemcisi IP örneğindeki IP adresini otomatik olarak temizler ve yeni bir IP adresi isteyen başlangıç durumundan DHCP işlemine başlar.</span><span class="sxs-lookup"><span data-stu-id="b6462-116">If the IP address is expired, the DHCP Client will automatically clear the IP address on the IP instance and begin the DHCP process from the INIT state, requesting a new IP address.</span></span>

<span data-ttu-id="b6462-117">Bu şekilde, DHCP Istemcisi kesintisiz olarak yeniden başlatmalar arasında çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="b6462-117">In this manner the DHCP Client can operate between reboots as if uninterrupted.</span></span>

<span data-ttu-id="b6462-118">Bu özelliğin bir çizimi aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b6462-118">Below is an illustration of this feature.</span></span> <span data-ttu-id="b6462-119">Bu, DHCP Istemcisinin yalnızca birincil arabirimde çalıştığını varsayar.</span><span class="sxs-lookup"><span data-stu-id="b6462-119">This assumes DHCP Client is running only on the primary interface.</span></span>

```C
/* On the power up, create an IP instance, DHCP Client, enable ICMP and UDP
   and other resources (not shown) for the DHCP Client/application
   in tx_application_define(). */
 
/* Define the DHCP application thread. */     
void    thread_dhcp_client_entry(ULONG thread_input)
{

UINT        status;
UINT        time_elapsed = 0;
NX_DHCP_CLIENT_RECORD client_nv_record;


if (/* The application checks if there is a previously saved DHCP Client record. */)
{


  /* No previously saved Client record. Start the DHCP Client in the INIT state. */
  status =  nx_dhcp_start(&dhcp_0);

  if (status !=NX_SUCCESS)
    return;

  do
  {
  
    /* Wait for DHCP to assign the IP address. */
  } while (status != NX_SUCCESS);

  /* We have a valid IP address. */

  /* At some point decide we power down the system. */

  /* Save the Client state data which we will subsequently need to restore the DHCP  
     Client. */
  status = nx_dhcp_client_get_record(&dhcp_0, &client_nv_record);         

  /* Copy this memory to non-volatile memory (not shown). */

  /* Delete the IP and DHCP Client instances before powering down. */
  nx_dhcp_delete(&dhcp_0);

  nx_ip_delete(&ip_0);

  /* Ready to power down, having released other resources as necessary. */

}
else
{

  /* The application has determined there is a previously saved record. We will 
     restore it to the current DHCP Client instance. */

  /* Get the previous Client state data from non-volatile memory. */

  /* Apply the record to the current Client instance. This will also 
     update the IP instance with IP address, mask etc. */
  status = nx_dhcp_client_restore_record(&dhcp_0, &client_nv_record, time_elapsed);   

     if (status != NX_SUCCESS)
      return;

     /* We are ready to resume the DHCP Client thread and use the assigned IP address. */
     status = nx_dhcp_resume(&dhcp_0);

     if (status != NX_SUCCESS)
      return;

}
```

## <a name="resuming-the-dhcp-client-thread-after-suspension"></a><span data-ttu-id="b6462-120">Askıya alındıktan sonra DHCP Istemci Iş parçacığı sürdürülüyor</span><span class="sxs-lookup"><span data-stu-id="b6462-120">Resuming the DHCP Client Thread after Suspension</span></span> 

<span data-ttu-id="b6462-121">Uygulamayı kapatmadan bir DHCP Istemci iş parçacığını askıya almak için, uygulama, bağlı durumu elde eden ve geçerli bir IP adresine sahip olan bir DHCP Istemcisinde *nx_dhcp_suspend* çağırır.</span><span class="sxs-lookup"><span data-stu-id="b6462-121">To suspend a DHCP Client thread without powering down, the application calls *nx_dhcp_suspend* on a DHCP Client which has achieved the BOUND state and which has a valid IP address.</span></span> <span data-ttu-id="b6462-122">DHCP Istemcisini sürdürmeye hazırlanıyorsa, ilk olarak DHCP adresi kiralamasında kalan süreyi (bağımsız bir saatten geçen süreyi elde) güncelleştirmek için *nx_dhcp_client_update_time_remaining* çağırır.</span><span class="sxs-lookup"><span data-stu-id="b6462-122">When it is ready to resume the DHCP Client it first calls *nx_dhcp_client_update_time_remaining* to update the time remaining on the DHCP address lease (obtaining the time elapsed from an independent time keeper).</span></span> <span data-ttu-id="b6462-123">Ardından, DHCP Istemci iş parçacığını sürdürmesini sağlamak için *nx_dhcp_resume* çağırır.</span><span class="sxs-lookup"><span data-stu-id="b6462-123">Then it calls the *nx_dhcp_resume* to resume the DHCP Client thread.</span></span>

<span data-ttu-id="b6462-124">Geçen süre DHCP Istemci durumunu yenıleme veya yeniden bağlama durumuna geçirir, DHCP Istemcisi IP adresi kiralamasını yenilemek veya yeniden bağlamak isteyen DHCP iletilerini otomatik olarak başlatır.</span><span class="sxs-lookup"><span data-stu-id="b6462-124">If the time elapsed puts the DHCP Client state in either a RENEW or REBIND state, the DHCP Client will automatically initiate DHCP messages requesting to renew or rebind the IP address lease.</span></span> <span data-ttu-id="b6462-125">IP adresinin geçerliliği dolmuşsa, DHCP Istemcisi IP adresini otomatik olarak temizler ve yeni bir IP adresi isteyen başlangıç durumundan DHCP işlemine başlar.</span><span class="sxs-lookup"><span data-stu-id="b6462-125">If the IP address is expired, the DHCP Client will automatically clear the IP address and begin the DHCP process from the INIT state, requesting a new IP address.</span></span>

<span data-ttu-id="b6462-126">Bu özelliğin kullanımına ilişkin bir çizim aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b6462-126">Below is an illustration of using this feature.</span></span>

```C
/* Create an IP instance, DHCP Client, enable ICMP and UDP
   and other resources (not shown) typically in tx_application_define(). */
 
/* Define the DHCP application thread. */     
void    thread_dhcp_client_entry(ULONG thread_input)
{

  /* Start the DHCP Client. */
  status =  nx_dhcp_start(&dhcp_0);

  if (status !=NX_SUCCESS)
    return;

  while(1)
  {
   
    /* Wait for DHCP to obtain an IP address. */
  }

  /* Do tasks with the IP address e.g. send pings to another host on the 
     network... */
  status =  nx_icmp_ping(…);

  if (status !=NX_SUCCESS)
          printf("Failed %d byte Ping!\n", length);

  /* At some later time, suspend the DHCP Client e.g. the device is going to low 
   power mode (sleep) so we do not want any threads to wake it up. */

  nx_dhcp_suspend(&dhcp_0);  

  /* During this suspended state, an independent timer is keeping track of the
     elapsed time. */


  /* At some point, we are ready to resume the DHCP Client thread. */

  /* Update the DHCP Client lease time remaining with the time elapsed. */
  status = nx_dhcp_client_update_time_remaining(&dhcp_0, time_elapsed);   

  if (status != NX_SUCCESS)
       return;

  /* We now can resume the DHCP Client thread. */
  status = nx_dhcp_resume(&dhcp_0);

  if (status != NX_SUCCESS)
       return;

  /* Resume tasks e.g. ping another host. */
  status =  nx_icmp_ping(…);

}
```

<span data-ttu-id="b6462-127">Aşağıda, bir DHCP Istemci durumunun bellekten geri yüklenmesi ve DHCP Istemcisini askıya almak ve sürdürmek için hizmetlerin bir listesi verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b6462-127">Below is a list of services for restoring a DHCP Client state from memory and for suspending and resuming the DHCP Client.</span></span>

## <a name="nx_dhcp_client_get_record"></a><span data-ttu-id="b6462-128">nx_dhcp_client_get_record</span><span class="sxs-lookup"><span data-stu-id="b6462-128">nx_dhcp_client_get_record</span></span>

<span data-ttu-id="b6462-129">Geçerli DHCP Istemci durumunun bir kaydını oluştur</span><span class="sxs-lookup"><span data-stu-id="b6462-129">Create a record of the current DHCP Client state</span></span>

### <a name="prototype"></a><span data-ttu-id="b6462-130">Prototype</span><span class="sxs-lookup"><span data-stu-id="b6462-130">Prototype</span></span>

```C
ULONG nx_dhcp_ client_get_record(NX_DHCP *dhcp_ptr, 
                                 NX_DHCP_CLIENT_RECORD *record_ptr);
```

### <a name="description"></a><span data-ttu-id="b6462-131">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b6462-131">Description</span></span>

<span data-ttu-id="b6462-132">Bu hizmet, DHCP Istemci örneğinde bulunan DHCP için etkinleştirilen ilk arabirimde çalışan DHCP Istemcisini, record_ptr tarafından işaret edilen kayda kaydeder.</span><span class="sxs-lookup"><span data-stu-id="b6462-132">This service saves the DHCP Client running on the first interface enabled for DHCP found on the DHCP Client instance to the record pointed to by record_ptr.</span></span> <span data-ttu-id="b6462-133">Bu, DHCP Istemci uygulamasının DHCP Istemci durumunu, örneğin bir güç kapatma ve yeniden başlatma gibi geri yüklemesine olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="b6462-133">This allows the DHCP Client application restore its DHCP Client state after, for example, a power down and reboot.</span></span>

<span data-ttu-id="b6462-134">DHCP için birden fazla arabirim etkinleştirilmişse, belirli bir arabirimdeki DHCP Istemci kaydını kaydetmek için *nx_dhcp_interface_client_get_record* hizmetini kullanın.</span><span class="sxs-lookup"><span data-stu-id="b6462-134">To save a DHCP Client record on a specific interface if more than one interface is enabled for DHCP, use the *nx_dhcp_interface_client_get_record* service.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="b6462-135">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="b6462-135">Input Parameters</span></span>

- <span data-ttu-id="b6462-136">**dhcp_ptr** DHCP Istemcisi işaretçisi</span><span class="sxs-lookup"><span data-stu-id="b6462-136">**dhcp_ptr** Pointer to DHCP Client</span></span>

- <span data-ttu-id="b6462-137">**record_ptr** DHCP Istemci kaydı işaretçisi</span><span class="sxs-lookup"><span data-stu-id="b6462-137">**record_ptr** Pointer to DHCP Client record</span></span>

### <a name="return-values"></a><span data-ttu-id="b6462-138">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="b6462-138">Return Values</span></span>

- <span data-ttu-id="b6462-139">**NX_SUCCESS** (0x0) istemci kaydı oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="b6462-139">**NX_SUCCESS** (0x0) Client record created</span></span>

- <span data-ttu-id="b6462-140">**NX_DHCP_NOT_BOUND** (0x94) Istemci, bağlantılı durumda değil</span><span class="sxs-lookup"><span data-stu-id="b6462-140">**NX_DHCP_NOT_BOUND** (0x94) Client not in Bound state</span></span>

- <span data-ttu-id="b6462-141">**NX_DHCP_NO_INTERFACES_ENABLED** (0xa5) DHCP için etkinleştirilen arabirim yok</span><span class="sxs-lookup"><span data-stu-id="b6462-141">**NX_DHCP_NO_INTERFACES_ENABLED** (0xA5) No interfaces enabled for DHCP</span></span>

- <span data-ttu-id="b6462-142">**NX_PTR_ERROR** (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="b6462-142">**NX_PTR_ERROR** (0x16) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="b6462-143">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="b6462-143">Allowed From</span></span>

<span data-ttu-id="b6462-144">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b6462-144">Threads</span></span>

### <a name="example"></a><span data-ttu-id="b6462-145">Örnek</span><span class="sxs-lookup"><span data-stu-id="b6462-145">Example</span></span>

```C
NX_DHCP_CLIENT_RECORD dhcp_record;


/* Obtain a record of the current client state. */
status=  nx_dhcp_client_get_record(dhcp_ptr, &dhcp_record);

/* If status is NX_SUCCESS dhcp_record contains the current DHCP client record. */
```

## <a name="nx_dhcp_interface_client_get_record"></a><span data-ttu-id="b6462-146">nx_dhcp_interface_client_get_record</span><span class="sxs-lookup"><span data-stu-id="b6462-146">nx_dhcp_interface_client_get_record</span></span>

<span data-ttu-id="b6462-147">Belirtilen arabirimdeki geçerli DHCP Istemci durumunun bir kaydını oluştur</span><span class="sxs-lookup"><span data-stu-id="b6462-147">Create a record of the current DHCP Client state on the specified interface</span></span>

### <a name="prototype"></a><span data-ttu-id="b6462-148">Prototype</span><span class="sxs-lookup"><span data-stu-id="b6462-148">Prototype</span></span>

```C
ULONG nx_dhcp_interface_client_get_record(NX_DHCP *dhcp_ptr, 
                                 UINT interface_index,
                                 NX_DHCP_CLIENT_RECORD *record_ptr);
```
### <a name="description"></a><span data-ttu-id="b6462-149">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b6462-149">Description</span></span>

<span data-ttu-id="b6462-150">Bu hizmet, belirtilen arabirimde çalışan DHCP Istemcisini record_ptr tarafından işaret edilen kayda kaydeder.</span><span class="sxs-lookup"><span data-stu-id="b6462-150">This service saves the DHCP Client running on the specified interface to the record pointed to by record_ptr.</span></span> <span data-ttu-id="b6462-151">Bu, DHCP Istemci uygulamasının DHCP Istemci durumunu, örneğin bir güç kapatma ve yeniden başlatma gibi geri yüklemesine olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="b6462-151">This allows the DHCP Client application restore its DHCP Client state after, for example, a power down and reboot.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="b6462-152">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="b6462-152">Input Parameters</span></span>

- <span data-ttu-id="b6462-153">**dhcp_ptr** DHCP Istemcisi işaretçisi</span><span class="sxs-lookup"><span data-stu-id="b6462-153">**dhcp_ptr** Pointer to DHCP Client</span></span>

- <span data-ttu-id="b6462-154">**interface_index** Kaydın alınacağı dizin</span><span class="sxs-lookup"><span data-stu-id="b6462-154">**interface_index** Index on which to get record</span></span>

- <span data-ttu-id="b6462-155">**record_ptr** DHCP Istemci kaydı işaretçisi</span><span class="sxs-lookup"><span data-stu-id="b6462-155">**record_ptr** Pointer to DHCP Client record</span></span>

### <a name="return-values"></a><span data-ttu-id="b6462-156">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="b6462-156">Return Values</span></span>

- <span data-ttu-id="b6462-157">**NX_SUCCESS** (0x0) istemci kaydı oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="b6462-157">**NX_SUCCESS** (0x0) Client record created</span></span>

- <span data-ttu-id="b6462-158">**NX_DHCP_NOT_BOUND** (0x94) Istemci, bağlantılı durumda değil</span><span class="sxs-lookup"><span data-stu-id="b6462-158">**NX_DHCP_NOT_BOUND** (0x94) Client not in Bound state</span></span>

- <span data-ttu-id="b6462-159">**NX_DHCP_BAD_INTERFACE_INDEX_ERROR** (0x9A) geçersiz arabirim dizini</span><span class="sxs-lookup"><span data-stu-id="b6462-159">**NX_DHCP_BAD_INTERFACE_INDEX_ERROR** (0x9A) Invalid interface index</span></span>

- <span data-ttu-id="b6462-160">NX_PTR_ERROR (0x16) geçersiz DHCP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b6462-160">NX_PTR_ERROR (0x16) Invalid DHCP pointer.</span></span>

- <span data-ttu-id="b6462-161">NX_INVALID_INTERFACE (0x4C) geçersiz ağ arabirimi</span><span class="sxs-lookup"><span data-stu-id="b6462-161">NX_INVALID_INTERFACE (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="b6462-162">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="b6462-162">Allowed From</span></span>

<span data-ttu-id="b6462-163">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b6462-163">Threads</span></span>

### <a name="example"></a><span data-ttu-id="b6462-164">Örnek</span><span class="sxs-lookup"><span data-stu-id="b6462-164">Example</span></span>

```C
NX_DHCP_CLIENT_RECORD dhcp_record;


/* Obtain a record of the current client state on interface 1. */
status=  nx_dhcp_interface_client_get_record(dhcp_ptr, 1, &dhcp_record);

/* If status is NX_SUCCESS dhcp_record contains the current DHCP client record. */
```

## <a name="nx_dhcp_-client_restore_record"></a><span data-ttu-id="b6462-165">nx_dhcp_ client_restore_record</span><span class="sxs-lookup"><span data-stu-id="b6462-165">nx_dhcp_ client_restore_record</span></span>

<span data-ttu-id="b6462-166">DHCP Istemcisini daha önce kaydedilen bir kayıttan geri yükleme</span><span class="sxs-lookup"><span data-stu-id="b6462-166">Restore DHCP Client from a previously saved record</span></span>

### <a name="prototype"></a><span data-ttu-id="b6462-167">Prototype</span><span class="sxs-lookup"><span data-stu-id="b6462-167">Prototype</span></span>

```C
ULONG nx_dhcp_client_restore_record(NX_DHCP *dhcp_ptr, 
                                    NX_DHCP_CLIENT_RECORD       
                                    *record_ptr, ULONG time_elapsed);
```
### <a name="description"></a><span data-ttu-id="b6462-168">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b6462-168">Description</span></span>

<span data-ttu-id="b6462-169">Bu hizmet, bir uygulamanın DHCP istemcisini record_ptr tarafından işaret edilen DHCP Istemci kaydını kullanarak önceki bir oturumdan geri yüklemesine olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="b6462-169">This service enables an application to restore its DHCP Client from a previous session using the DHCP Client record pointed to by record_ptr.</span></span> <span data-ttu-id="b6462-170">Time_elapsed girişi, DHCP Istemci kirası üzerinde kalan zamana uygulanır.</span><span class="sxs-lookup"><span data-stu-id="b6462-170">The time_elapsed input is applied to the time remaining on DHCP Client lease.</span></span>

<span data-ttu-id="b6462-171">Bu, DHCP Istemci uygulamasının kapatmadan önce DHCP Istemcisinin bir kaydını oluşturulmasını ve bu kaydı kalıcı belleğe kaydetmesidir.</span><span class="sxs-lookup"><span data-stu-id="b6462-171">This requires that the DHCP Client application created a record of the DHCP Client before powering down, and saved that record to nonvolatile memory.</span></span>

<span data-ttu-id="b6462-172">DHCP Istemcisi için birden fazla arabirim etkinse, bu hizmet DHCP Istemci örneğinde bulunan ilk geçerli arabirime uygulanır.</span><span class="sxs-lookup"><span data-stu-id="b6462-172">If more than one interface is enabled for DHCP Client, this service is applied to the first valid interface found in the DHCP Client instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="b6462-173">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="b6462-173">Input Parameters</span></span>

- <span data-ttu-id="b6462-174">**dhcp_ptr** DHCP Istemcisi işaretçisi</span><span class="sxs-lookup"><span data-stu-id="b6462-174">**dhcp_ptr** Pointer to DHCP Client</span></span>

- <span data-ttu-id="b6462-175">**record_ptr** DHCP Istemci kaydı işaretçisi</span><span class="sxs-lookup"><span data-stu-id="b6462-175">**record_ptr** Pointer to DHCP Client record</span></span>

- <span data-ttu-id="b6462-176">**time_elapsed** Giriş istemci kaydında kalan kira zamanından çıkarma süresi</span><span class="sxs-lookup"><span data-stu-id="b6462-176">**time_elapsed** Time to subtract from the lease time remaining in the input client record</span></span>

### <a name="return-values"></a><span data-ttu-id="b6462-177">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="b6462-177">Return Values</span></span>

- <span data-ttu-id="b6462-178">**NX_SUCCESS** (0x0) istemci kaydı geri yüklendi</span><span class="sxs-lookup"><span data-stu-id="b6462-178">**NX_SUCCESS** (0x0) Client record restored</span></span>

- <span data-ttu-id="b6462-179">**NX_DHCP_NO_INTERFACES_ENABLED** (0xa5) DHCP çalıştıran arabirim yok</span><span class="sxs-lookup"><span data-stu-id="b6462-179">**NX_DHCP_NO_INTERFACES_ENABLED** (0xA5) No interfaces running DHCP</span></span>

- <span data-ttu-id="b6462-180">**NX_PTR_ERROR** (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="b6462-180">**NX_PTR_ERROR** (0x16) Invalid pointer Input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="b6462-181">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="b6462-181">Allowed From</span></span>

<span data-ttu-id="b6462-182">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b6462-182">Threads</span></span>

### <a name="example"></a><span data-ttu-id="b6462-183">Örnek</span><span class="sxs-lookup"><span data-stu-id="b6462-183">Example</span></span>
```C
NX_DHCP_CLIENT_RECORD dhcp_record;
ULONG       time_elapsed;

/* Obtain time (timer ticks) elapsed from independent time keeper. */
Time_elapsed = /* to be determined by application */ 1000; 


/* Obtain a record of the current client state. */
status=  nx_dhcp_client_restore_record(client_ptr, &dhcp_record, time_elapsed);

/* If status is NX_SUCCESS the current DHCP Client pointed to by dhcp_ptr
   contains the current client record updated for time elapsed during power down. */
```

## <a name="nx_dhcp_interace_client_restore_record"></a><span data-ttu-id="b6462-184">nx_dhcp_interace_client_restore_record</span><span class="sxs-lookup"><span data-stu-id="b6462-184">nx_dhcp_interace_client_restore_record</span></span>

<span data-ttu-id="b6462-185">DHCP Istemcisini belirtilen arabirimdeki daha önce kaydedilmiş bir kayıttan geri yükle</span><span class="sxs-lookup"><span data-stu-id="b6462-185">Restore DHCP Client from a previously saved record on specified interface</span></span>

### <a name="prototype"></a><span data-ttu-id="b6462-186">Prototype</span><span class="sxs-lookup"><span data-stu-id="b6462-186">Prototype</span></span>

```C
ULONG nx_dhcp_interface_client_restore_record(NX_DHCP *dhcp_ptr, 
                                              NX_DHCP_CLIENT_RECORD       
                                              *record_ptr, ULONG time_elapsed);
```
### <a name="description"></a><span data-ttu-id="b6462-187">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b6462-187">Description</span></span>

<span data-ttu-id="b6462-188">Bu hizmet, bir uygulamanın DHCP istemcisini, record_ptr tarafından işaret edilen DHCP Istemci kaydını kullanarak belirtilen arabirime geri yüklemesine olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="b6462-188">This service enables an application to restore its DHCP Client on the specified interface using the DHCP Client record pointed to by record_ptr.</span></span> <span data-ttu-id="b6462-189">Time_elapsed girişi, DHCP Istemci kirası üzerinde kalan zamana uygulanır.</span><span class="sxs-lookup"><span data-stu-id="b6462-189">The time_elapsed input is applied to the time remaining on DHCP Client lease.</span></span>

<span data-ttu-id="b6462-190">Bu, DHCP Istemci uygulamasının kapatmadan önce DHCP Istemcisinin bir kaydını oluşturulmasını ve bu kaydı kalıcı belleğe kaydetmesidir.</span><span class="sxs-lookup"><span data-stu-id="b6462-190">This requires that the DHCP Client application created a record of the DHCP Client before powering down, and saved that record to nonvolatile memory.</span></span>

<span data-ttu-id="b6462-191">DHCP Istemcisi için birden fazla arabirim etkinse, bu hizmet DHCP Istemci örneğinde bulunan ilk geçerli arabirime uygulanır.</span><span class="sxs-lookup"><span data-stu-id="b6462-191">If more than one interface is enabled for DHCP Client, this service is applied to the first valid interface found in the DHCP Client instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="b6462-192">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="b6462-192">Input Parameters</span></span>

- <span data-ttu-id="b6462-193">**dhcp_ptr** DHCP Istemcisi işaretçisi</span><span class="sxs-lookup"><span data-stu-id="b6462-193">**dhcp_ptr** Pointer to DHCP Client</span></span>

- <span data-ttu-id="b6462-194">**record_ptr** DHCP Istemci kaydı işaretçisi</span><span class="sxs-lookup"><span data-stu-id="b6462-194">**record_ptr** Pointer to DHCP Client record</span></span>

- <span data-ttu-id="b6462-195">**time_elapsed** Giriş istemci kaydında kalan kira zamanından çıkarma süresi</span><span class="sxs-lookup"><span data-stu-id="b6462-195">**time_elapsed** Time to subtract from the lease time remaining in the input client record</span></span>

### <a name="return-values"></a><span data-ttu-id="b6462-196">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="b6462-196">Return Values</span></span>

- <span data-ttu-id="b6462-197">**NX_SUCCESS** (0x0) istemci kaydı geri yüklendi</span><span class="sxs-lookup"><span data-stu-id="b6462-197">**NX_SUCCESS** (0x0) Client record restored</span></span>

- <span data-ttu-id="b6462-198">**NX_DHCP_NOT_BOUND** (0x94) istemci IP adresine bağlanmadı</span><span class="sxs-lookup"><span data-stu-id="b6462-198">**NX_DHCP_NOT_BOUND** (0x94) Client not bound to IP address</span></span>

- <span data-ttu-id="b6462-199">**NX_DHCP_BAD_INTERFACE_INDEX_ERROR** (0x9A) geçersiz arabirim dizini</span><span class="sxs-lookup"><span data-stu-id="b6462-199">**NX_DHCP_BAD_INTERFACE_INDEX_ERROR** (0x9A) Invalid interface index</span></span>

- <span data-ttu-id="b6462-200">NX_PTR_ERROR (0x16) geçersiz DHCP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b6462-200">NX_PTR_ERROR (0x16) Invalid DHCP pointer.</span></span>

- <span data-ttu-id="b6462-201">NX_INVALID_INTERFACE (0x4C) geçersiz ağ arabirimi</span><span class="sxs-lookup"><span data-stu-id="b6462-201">NX_INVALID_INTERFACE (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="b6462-202">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="b6462-202">Allowed From</span></span>

<span data-ttu-id="b6462-203">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b6462-203">Threads</span></span>

### <a name="example"></a><span data-ttu-id="b6462-204">Örnek</span><span class="sxs-lookup"><span data-stu-id="b6462-204">Example</span></span>

```C
NX_DHCP_CLIENT_RECORD dhcp_record;
ULONG       time_elapsed;

/* Obtain time (timer ticks) elapsed from independent time keeper. */
Time_elapsed = /* to be determined by application */ 1000; 


/* Obtain a record of the current client state on the primary interface. */
status=  nx_dhcp_interface_client_restore_record(client_ptr, 0, &dhcp_record, time_elapsed);

/* If status is NX_SUCCESS the current DHCP Client pointed to by dhcp_ptr  
   contains the current client record updated for time elapsed during power down. */
```

## <a name="nx_dhcp_-client_update_time_remaining"></a><span data-ttu-id="b6462-205">nx_dhcp_ client_update_time_remaining</span><span class="sxs-lookup"><span data-stu-id="b6462-205">nx_dhcp_ client_update_time_remaining</span></span>

<span data-ttu-id="b6462-206">DHCP Istemcisi kiralamasında kalan süreyi Güncelleştir</span><span class="sxs-lookup"><span data-stu-id="b6462-206">Update the time remaining on DHCP Client lease</span></span>

### <a name="prototype"></a><span data-ttu-id="b6462-207">Prototype</span><span class="sxs-lookup"><span data-stu-id="b6462-207">Prototype</span></span>

```C
ULONG nx_dhcp_client_update_time_remaining(NX_DHCP *dhcp_ptr
                                           ULONG time_elapsed);
```
### <a name="description"></a><span data-ttu-id="b6462-208">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b6462-208">Description</span></span>

<span data-ttu-id="b6462-209">Bu hizmet DHCP istemci IP adresi kirası üzerinde kalan süreyi, DHCP Istemci örneğinde bulunan DHCP için etkinleştirilen ilk arabirimdeki time_elapsed girişi ile güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="b6462-209">This service updates the time remaining on the DHCP Client IP address lease with the time_elapsed input on the first interface enabled for DHCP found on the DHCP Client instance.</span></span> <span data-ttu-id="b6462-210">Uygulama, *nx_dhcp_suspend* kullanarak bu hizmeti kullanmadan önce DHCP istemci iş parçacığını askıya almalıdır.</span><span class="sxs-lookup"><span data-stu-id="b6462-210">The application must suspend the DHCP Client thread before using this service using *nx_dhcp_suspend*.</span></span> <span data-ttu-id="b6462-211">Bu hizmet çağrıldıktan sonra uygulama, *nx_dhcp_resume* çağırarak DHCP istemci iş parçacığını sürdürür.</span><span class="sxs-lookup"><span data-stu-id="b6462-211">After calling this service, the application can resume the DHCP Client thread by calling *nx_dhcp_resume*.</span></span>

<span data-ttu-id="b6462-212">Bu, DHCP Istemci iş parçacığını bir süre için askıya almanız gereken DHCP Istemci uygulamalarına yöneliktir ve kalan IP adresi kiralama süresini güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="b6462-212">This is intended for DHCP Client applications that need to suspend the DHCP Client thread for a period of time, and then update the IP address lease time remaining.</span></span>

> [!NOTE]
> <span data-ttu-id="b6462-213">Bu hizmet, daha önce açıklanan *nx_dhcp_client_get_record* ve *nx_dhcp_client_restore_record* birlikte kullanılmak üzere tasarlanmamıştır.</span><span class="sxs-lookup"><span data-stu-id="b6462-213">This service is not intended to be used with *nx_dhcp_client_get_record* and *nx_dhcp_client_restore_record* described previously).</span></span> <span data-ttu-id="b6462-214">Bu hizmetler daha önce bu bölümde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="b6462-214">These services are previously described in this section.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="b6462-215">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="b6462-215">Input Parameters</span></span>

- <span data-ttu-id="b6462-216">**dhcp_ptr** DHCP Istemcisi işaretçisi</span><span class="sxs-lookup"><span data-stu-id="b6462-216">**dhcp_ptr** Pointer to DHCP Client</span></span>

- <span data-ttu-id="b6462-217">**time_elapsed** IP adresi kirası üzerinde kalan süreden çıkarma süresi</span><span class="sxs-lookup"><span data-stu-id="b6462-217">**time_elapsed** Time to subtract from the time remaining on the IP address lease</span></span>

### <a name="return-values"></a><span data-ttu-id="b6462-218">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="b6462-218">Return Values</span></span>

- <span data-ttu-id="b6462-219">**NX_SUCCESS** (0x0) istemci IP kirası güncelleştirildi</span><span class="sxs-lookup"><span data-stu-id="b6462-219">**NX_SUCCESS** (0x0) Client IP lease updated</span></span>

- <span data-ttu-id="b6462-220">**NX_DHCP_NO_INTERFACES_ENABLED** (0xa5) DHCP için etkinleştirilen arabirim yok</span><span class="sxs-lookup"><span data-stu-id="b6462-220">**NX_DHCP_NO_INTERFACES_ENABLED** (0xA5) No interfaces enabled for DHCP</span></span>

- <span data-ttu-id="b6462-221">**NX_PTR_ERROR** (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="b6462-221">**NX_PTR_ERROR** (0x16) Invalid Pointer Input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="b6462-222">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="b6462-222">Allowed From</span></span>

<span data-ttu-id="b6462-223">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b6462-223">Threads</span></span>

### <a name="example"></a><span data-ttu-id="b6462-224">Örnek</span><span class="sxs-lookup"><span data-stu-id="b6462-224">Example</span></span>

```C
ULONG       time_elapsed;

/* Obtain time (timer ticks) elapsed from independent time keeper. */
time_elapsed = /* to be determined by application */ 1000; 


/* Apply the elapsed time to the DHCP Client address lease. */
status=  nx_dhcp_client_update_time_remaining(client_ptr, time_elapsed);

/* If status is NX_SUCCESS the DHCP Client is updated for time elapsed. */
```


## <a name="nx_dhcp_interface_client_update_time_remaining"></a><span data-ttu-id="b6462-225">nx_dhcp_interface_client_update_time_remaining</span><span class="sxs-lookup"><span data-stu-id="b6462-225">nx_dhcp_interface_client_update_time_remaining</span></span>

<span data-ttu-id="b6462-226">Belirtilen arabirimdeki DHCP Istemcisi kiralamasında kalan süreyi Güncelleştir</span><span class="sxs-lookup"><span data-stu-id="b6462-226">Update the time remaining on DHCP Client lease on the specified interface</span></span>

### <a name="prototype"></a><span data-ttu-id="b6462-227">Prototype</span><span class="sxs-lookup"><span data-stu-id="b6462-227">Prototype</span></span>

```C
ULONG nx_dhcp_interface_client_update_time_remaining(NX_DHCP *dhcp_ptr,
                                                     UINT interface_index,
                                                     ULONG time_elapsed);
```
### <a name="description"></a><span data-ttu-id="b6462-228">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b6462-228">Description</span></span>

<span data-ttu-id="b6462-229">Bu hizmet DHCP Istemci IP adresi kiralamasında kalan süreyi, bu arabirim DHCP için etkinleştirildiğinde belirtilen arabirimdeki time_elapsed girişi ile güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="b6462-229">This service updates the time remaining on the DHCP Client IP address lease with the time_elapsed input on the specified interface if that interface is enabled for DHCP.</span></span> <span data-ttu-id="b6462-230">Uygulama, *nx_dhcp_suspend* kullanarak bu hizmeti kullanmadan önce DHCP istemci iş parçacığını askıya almalıdır.</span><span class="sxs-lookup"><span data-stu-id="b6462-230">The application must suspend the DHCP Client thread before using this service using *nx_dhcp_suspend*.</span></span> <span data-ttu-id="b6462-231">Bu hizmet çağrıldıktan sonra uygulama, *nx_dhcp_resume* çağırarak DHCP istemci iş parçacığını sürdürür.</span><span class="sxs-lookup"><span data-stu-id="b6462-231">After calling this service, the application can resume the DHCP Client thread by calling *nx_dhcp_resume*.</span></span> <span data-ttu-id="b6462-232">Bkz. DHCP Istemci iş parçacığını askıya alma ve sürdürme, DHCP için etkinleştirilen tüm arabirimler için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="b6462-232">Note suspending and resuming the DHCP Client thread applies to all interfaces enabled for DHCP.</span></span>

<span data-ttu-id="b6462-233">Bu, DHCP Istemci iş parçacığını bir süre için askıya almanız gereken DHCP Istemci uygulamalarına yöneliktir ve kalan IP adresi kiralama süresini güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="b6462-233">This is intended for DHCP Client applications that need to suspend the DHCP Client thread for a period of time, and then update the IP address lease time remaining.</span></span>

> [!NOTE] 
> <span data-ttu-id="b6462-234">Bu hizmet, daha önce açıklanan *nx_dhcp_client_get_record* ve *nx_dhcp_client_restore_record* birlikte kullanılmak üzere tasarlanmamıştır.</span><span class="sxs-lookup"><span data-stu-id="b6462-234">This service is not intended to be used with *nx_dhcp_client_get_record* and *nx_dhcp_client_restore_record* described previously).</span></span> <span data-ttu-id="b6462-235">Bu hizmetler daha önce bu bölümde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="b6462-235">These services are previously described in this section.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="b6462-236">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="b6462-236">Input Parameters</span></span>

- <span data-ttu-id="b6462-237">**dhcp_ptr** DHCP Istemcisi işaretçisi</span><span class="sxs-lookup"><span data-stu-id="b6462-237">**dhcp_ptr** Pointer to DHCP Client</span></span>

- <span data-ttu-id="b6462-238">**interface_index** Geçen süreyi uygulamak için arabirim dizini</span><span class="sxs-lookup"><span data-stu-id="b6462-238">**interface_index** Index to interface to apply elapsed time to</span></span>

- <span data-ttu-id="b6462-239">**time_elapsed** IP adresi kirası üzerinde kalan süreden çıkarma süresi</span><span class="sxs-lookup"><span data-stu-id="b6462-239">**time_elapsed** Time to subtract from the time remaining on the IP address lease</span></span>

### <a name="return-values"></a><span data-ttu-id="b6462-240">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="b6462-240">Return Values</span></span>

- <span data-ttu-id="b6462-241">**NX_SUCCESS** (0x0) istemci IP kirası güncelleştirildi</span><span class="sxs-lookup"><span data-stu-id="b6462-241">**NX_SUCCESS** (0x0) Client IP lease updated</span></span>

- <span data-ttu-id="b6462-242">**NX_DHCP_BAD_INTERFACE_INDEX_ERROR** (0x9A) geçersiz arabirim dizini</span><span class="sxs-lookup"><span data-stu-id="b6462-242">**NX_DHCP_BAD_INTERFACE_INDEX_ERROR** (0x9A) Invalid interface index</span></span>

- <span data-ttu-id="b6462-243">NX_PTR_ERROR (0x16) geçersiz DHCP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b6462-243">NX_PTR_ERROR (0x16) Invalid DHCP pointer.</span></span>

- <span data-ttu-id="b6462-244">NX_INVALID_INTERFACE (0x4C) geçersiz ağ arabirimi</span><span class="sxs-lookup"><span data-stu-id="b6462-244">NX_INVALID_INTERFACE (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="b6462-245">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="b6462-245">Allowed From</span></span>

<span data-ttu-id="b6462-246">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b6462-246">Threads</span></span>

### <a name="example"></a><span data-ttu-id="b6462-247">Örnek</span><span class="sxs-lookup"><span data-stu-id="b6462-247">Example</span></span>

```C
ULONG       time_elapsed;

/* Obtain time (timer ticks) elapsed from independent time keeper. */
time_elapsed = /* to be determined by application */ 1000; 


/* Apply the elapsed time to the DHCP Client address lease on interface 1. */
status=  nx_dhcp_interface_client_update_time_remaining(client_ptr, 1, time_elapsed);

/* If status is NX_SUCCESS the DHCP Client is updated for time elapsed. */
```


## <a name="nx_dhcp_suspend"></a><span data-ttu-id="b6462-248">nx_dhcp_suspend</span><span class="sxs-lookup"><span data-stu-id="b6462-248">nx_dhcp_suspend</span></span>

<span data-ttu-id="b6462-249">DHCP Istemci iş parçacığını askıya alma</span><span class="sxs-lookup"><span data-stu-id="b6462-249">Suspend the DHCP Client thread</span></span>

### <a name="prototype"></a><span data-ttu-id="b6462-250">Prototype</span><span class="sxs-lookup"><span data-stu-id="b6462-250">Prototype</span></span>

```C
ULONG nx_dhcp_suspend(NX_DHCP *dhcp_ptr);
```
### <a name="description"></a><span data-ttu-id="b6462-251">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b6462-251">Description</span></span>

<span data-ttu-id="b6462-252">Bu hizmet, geçerli DHCP Istemci iş parçacığını askıya alır.</span><span class="sxs-lookup"><span data-stu-id="b6462-252">This service suspends the current DHCP Client thread.</span></span> <span data-ttu-id="b6462-253">*Nx_dhcp_stop* farklı olarak, bu HIZMET çağrıldığında DHCP istemci durumunda hiçbir değişiklik olmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b6462-253">Note that unlike *nx_dhcp_stop*, there is no change to the DHCP Client state when this service is called.</span></span>

<span data-ttu-id="b6462-254">Bu hizmet, DHCP için etkinleştirilen tüm arabirimlerde çalışan DHCP 'yi askıya alır.</span><span class="sxs-lookup"><span data-stu-id="b6462-254">This service suspends DHCP running on all interfaces enabled for DHCP.</span></span>

<span data-ttu-id="b6462-255">DHCP Istemcisi askıya alındığında DHCP Istemci durumunu geçen süre ile güncelleştirmek için, daha önce açıklanan *nx_dhcp_client_update_time_remaining* bakın.</span><span class="sxs-lookup"><span data-stu-id="b6462-255">To update the DHCP Client state with elapsed time while the DHCP Client is suspended, see the *nx_dhcp_client_update_time_remaining* described previously.</span></span> <span data-ttu-id="b6462-256">Askıya alınmış bir DHCP Istemci iş parçacığını sürdürmesini sağlamak için uygulama *nx_dhcp_resume* çağırmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b6462-256">To resume a suspended DHCP Client thread, the application should call *nx_dhcp_resume*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="b6462-257">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="b6462-257">Input Parameters</span></span>

- <span data-ttu-id="b6462-258">**dhcp_ptr** DHCP Istemcisi işaretçisi</span><span class="sxs-lookup"><span data-stu-id="b6462-258">**dhcp_ptr** Pointer to DHCP Client</span></span>

### <a name="return-values"></a><span data-ttu-id="b6462-259">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="b6462-259">Return Values</span></span>

- <span data-ttu-id="b6462-260">**NX_SUCCESS** (0x0) istemci iş parçacığı askıya alındı</span><span class="sxs-lookup"><span data-stu-id="b6462-260">**NX_SUCCESS** (0x0) Client thread is suspended</span></span>

- <span data-ttu-id="b6462-261">**NX_PTR_ERROR** (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="b6462-261">**NX_PTR_ERROR** (0x16) Invalid pointer Input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="b6462-262">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="b6462-262">Allowed From</span></span>

<span data-ttu-id="b6462-263">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b6462-263">Threads</span></span>

### <a name="example"></a><span data-ttu-id="b6462-264">Örnek</span><span class="sxs-lookup"><span data-stu-id="b6462-264">Example</span></span>

```C
/* Pause the DHCP client thread. */
status=  nx_dhcp_suspend(client_ptr);

/* If status is NX_SUCCESS the current DHCP Client thread is paused. */
```


## <a name="nx_dhcp_resume"></a><span data-ttu-id="b6462-265">nx_dhcp_resume</span><span class="sxs-lookup"><span data-stu-id="b6462-265">nx_dhcp_resume</span></span>

<span data-ttu-id="b6462-266">Askıya alınmış bir DHCP Istemci iş parçacığını sürdürür</span><span class="sxs-lookup"><span data-stu-id="b6462-266">Resume a suspended DHCP Client thread</span></span>

### <a name="prototype"></a><span data-ttu-id="b6462-267">Prototype</span><span class="sxs-lookup"><span data-stu-id="b6462-267">Prototype</span></span>

```C
ULONG nx_dhcp_resume(NX_DHCP *dhcp_ptr);
```
### <a name="description"></a><span data-ttu-id="b6462-268">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b6462-268">Description</span></span>

<span data-ttu-id="b6462-269">Bu hizmet, askıya alınmış bir DHCP Istemci iş parçacığını sürdürür.</span><span class="sxs-lookup"><span data-stu-id="b6462-269">This service resumes a suspended DHCP Client thread.</span></span> <span data-ttu-id="b6462-270">Istemci iş parçacığına devam ettikten sonra gerçek DHCP Istemci durumunda değişiklik olmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b6462-270">Note that there is no change to the actual DHCP Client state after resuming the Client thread.</span></span> <span data-ttu-id="b6462-271">DHCP Istemci IP adresi kiralamasında kalan süreyi, *nx_dhcp_resume* çağrılmadan önce geçen süre ile güncelleştirmek için, daha önce açıklanan *nx_dhcp_client_update_time_remaining* bakın.</span><span class="sxs-lookup"><span data-stu-id="b6462-271">To update the time remaining on the DHCP Client IP address lease with elapsed time before calling *nx_dhcp_resume*, see the *nx_dhcp_client_update_time_remaining* described previously.</span></span>

<span data-ttu-id="b6462-272">Bu hizmet, DHCP için etkinleştirilen tüm arabirimlerde çalışan DHCP 'yi sürdürür.</span><span class="sxs-lookup"><span data-stu-id="b6462-272">This service resumes DHCP running on all interfaces enabled for DHCP.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="b6462-273">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="b6462-273">Input Parameters</span></span>

- <span data-ttu-id="b6462-274">**dhcp_ptr** DHCP Istemcisi işaretçisi</span><span class="sxs-lookup"><span data-stu-id="b6462-274">**dhcp_ptr** Pointer to DHCP Client</span></span>

### <a name="return-values"></a><span data-ttu-id="b6462-275">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="b6462-275">Return Values</span></span>

- <span data-ttu-id="b6462-276">**NX_SUCCESS** (0x0) istemci iş parçacığı sürdürülüyor</span><span class="sxs-lookup"><span data-stu-id="b6462-276">**NX_SUCCESS** (0x0) Client thread is resumed</span></span>

- <span data-ttu-id="b6462-277">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="b6462-277">NX_PTR_ERROR (0x16) Invalid pointer Input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="b6462-278">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="b6462-278">Allowed From</span></span>

<span data-ttu-id="b6462-279">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b6462-279">Threads</span></span>

### <a name="example"></a><span data-ttu-id="b6462-280">Örnek</span><span class="sxs-lookup"><span data-stu-id="b6462-280">Example</span></span>

```C
/* Resume the DHCP client thread. */
status=  nx_dhcp_resume(client_ptr);

/* If status is NX_SUCCESS the current DHCP Client thread is resumed. */
```