---
title: Bölüm 5-USBX OTG
description: USBX, donanım tasarımında bir OTG uyumlu USB denetleyicisi varsa, USB 'nin OTG işlevlerini destekler.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: da562fd843c6ef0fd17f0d979ca57bd37572748d
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104827413"
---
# <a name="chapter-5---usbx-otg"></a><span data-ttu-id="15c53-103">Bölüm 5-USBX OTG</span><span class="sxs-lookup"><span data-stu-id="15c53-103">Chapter 5 - USBX OTG</span></span>

<span data-ttu-id="15c53-104">USBX, donanım tasarımında bir OTG uyumlu USB denetleyicisi varsa, USB 'nin OTG işlevlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="15c53-104">USBX supports the OTG functionalities of USB when an OTG compliant USB controller is available in the hardware design.</span></span>

<span data-ttu-id="15c53-105">USBX, çekirdek USB yığınında OTG 'yi destekler.</span><span class="sxs-lookup"><span data-stu-id="15c53-105">USBX supports OTG in the core USB stack.</span></span> <span data-ttu-id="15c53-106">Ancak OTG 'nin çalışması için, belirli bir USB denetleyicisi gerekir.</span><span class="sxs-lookup"><span data-stu-id="15c53-106">But for OTG to function, it requires a specific USB controller.</span></span> <span data-ttu-id="15c53-107">USBX OTG denetleyici işlevleri usbx_otg dizininde bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="15c53-107">USBX OTG controller functions can be found in the usbx_otg directory.</span></span> <span data-ttu-id="15c53-108">Geçerli USBX sürümü yalnızca tam OTG özelliklerine sahip NXP LPC3131 destekler.</span><span class="sxs-lookup"><span data-stu-id="15c53-108">The current USBX version only supports the NXP LPC3131 with full OTG capabilities.</span></span>

<span data-ttu-id="15c53-109">Normal denetleyici sürücü işlevleri (konak veya cihaz) hala standart USBX usbx_device_controllers ve usbx_host_controllers bulunabilir ancak usbx_otg Dizin, USB denetleyicisiyle ilişkili belirli OTG işlevlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="15c53-109">The regular controller driver functions (host or device) can still be found in the standard USBX usbx_device_controllers and usbx_host_controllers but the usbx_otg directory contains the specific OTG functions associated with the USB controller.</span></span>

<span data-ttu-id="15c53-110">Her zamanki ana bilgisayar/cihaz işlevlerine ek olarak, bir OTG denetleyicisi için dört işlev kategorisi vardır.</span><span class="sxs-lookup"><span data-stu-id="15c53-110">There are four categories of functions for an OTG controller in addition to the usual host/device functions.</span></span>

- <span data-ttu-id="15c53-111">VBUS 'a özgü işlevler</span><span class="sxs-lookup"><span data-stu-id="15c53-111">VBUS specific functions</span></span>
- <span data-ttu-id="15c53-112">Denetleyiciyi başlatma ve durdurma</span><span class="sxs-lookup"><span data-stu-id="15c53-112">Start and Stop of the controller</span></span>
- <span data-ttu-id="15c53-113">USB rol yöneticisi</span><span class="sxs-lookup"><span data-stu-id="15c53-113">USB role manager</span></span>
- <span data-ttu-id="15c53-114">Kesme işleyicileri</span><span class="sxs-lookup"><span data-stu-id="15c53-114">Interrupt handlers</span></span>

## <a name="vbus-functions"></a><span data-ttu-id="15c53-115">VBUS işlevleri</span><span class="sxs-lookup"><span data-stu-id="15c53-115">VBUS functions</span></span>

<span data-ttu-id="15c53-116">Her denetleyicinin, VBUS 'ın durumunu güç yönetimi gereksinimlerine göre değiştirmesi için bir VBUS Yöneticisi olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="15c53-116">Each controller needs to have a VBUS manager to change the state of VBUS based on power management requirements.</span></span> <span data-ttu-id="15c53-117">Genellikle, bu işlev yalnızca VBUS 'ı açmayı veya kapatmayı gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="15c53-117">Usually, this function only performs turning on or off VBUS.</span></span>

## <a name="start-and-stop-the-controller"></a><span data-ttu-id="15c53-118">Denetleyiciyi başlatma ve durdurma</span><span class="sxs-lookup"><span data-stu-id="15c53-118">Start and Stop the controller</span></span>

<span data-ttu-id="15c53-119">Normal bir USB uygulamasından farklı olarak, OTG, rol değiştiğinde konağın ve/veya cihaz yığınının etkinleştirilmesini ve devre dışı olmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="15c53-119">Unlike a regular USB implementation, OTG requires the host and/or the device stack to be activated and deactivated when the role changes.</span></span>

## <a name="usb-role-manager"></a><span data-ttu-id="15c53-120">USB rol yöneticisi</span><span class="sxs-lookup"><span data-stu-id="15c53-120">USB role Manager</span></span>

<span data-ttu-id="15c53-121">USB rol yöneticisi, USB 'nin durumunu değiştirmek için komutları alır.</span><span class="sxs-lookup"><span data-stu-id="15c53-121">The USB role manager receives commands to change the state of the USB.</span></span> <span data-ttu-id="15c53-122">Ve arasında geçiş gerektiren birkaç durum vardır:</span><span class="sxs-lookup"><span data-stu-id="15c53-122">There are several states that need transitions to and from:</span></span>

| <span data-ttu-id="15c53-123">Durum</span><span class="sxs-lookup"><span data-stu-id="15c53-123">State</span></span>                    | <span data-ttu-id="15c53-124">Değer</span><span class="sxs-lookup"><span data-stu-id="15c53-124">Value</span></span> | <span data-ttu-id="15c53-125">Açıklama</span><span class="sxs-lookup"><span data-stu-id="15c53-125">Description</span></span>                                           |
| ------------------------ | ----- | ----------------------------------------------------- |
| <span data-ttu-id="15c53-126">UX_OTG_IDLE</span><span class="sxs-lookup"><span data-stu-id="15c53-126">UX_OTG_IDLE</span></span>            | <span data-ttu-id="15c53-127">0</span><span class="sxs-lookup"><span data-stu-id="15c53-127">0</span></span>     | <span data-ttu-id="15c53-128">Cihaz boşta.</span><span class="sxs-lookup"><span data-stu-id="15c53-128">The device is Idle.</span></span> <span data-ttu-id="15c53-129">Hiçbir şeye bağlanmadı</span><span class="sxs-lookup"><span data-stu-id="15c53-129">Not connected to anything</span></span> |
| <span data-ttu-id="15c53-130">UX_OTG_IDLE_TO_HOST</span><span class="sxs-lookup"><span data-stu-id="15c53-130">UX_OTG_IDLE_TO_HOST</span></span>  | <span data-ttu-id="15c53-131">1</span><span class="sxs-lookup"><span data-stu-id="15c53-131">1</span></span>     | <span data-ttu-id="15c53-132">Cihaz, bağlayıcı türüyle bağlandı</span><span class="sxs-lookup"><span data-stu-id="15c53-132">Device is connected with type A connector</span></span>             |
| <span data-ttu-id="15c53-133">UX_OTG_IDLE_TO_SLAVE</span><span class="sxs-lookup"><span data-stu-id="15c53-133">UX_OTG_IDLE_TO_SLAVE</span></span> | <span data-ttu-id="15c53-134">2</span><span class="sxs-lookup"><span data-stu-id="15c53-134">2</span></span>     | <span data-ttu-id="15c53-135">Cihaz, tür B Bağlayıcısı ile bağlandı</span><span class="sxs-lookup"><span data-stu-id="15c53-135">Device is connected with type B connector</span></span>             |
| <span data-ttu-id="15c53-136">UX_OTG_HOST_TO_IDLE</span><span class="sxs-lookup"><span data-stu-id="15c53-136">UX_OTG_HOST_TO_IDLE</span></span>  | <span data-ttu-id="15c53-137">3</span><span class="sxs-lookup"><span data-stu-id="15c53-137">3</span></span>     | <span data-ttu-id="15c53-138">Ana cihazın bağlantısı kesildi</span><span class="sxs-lookup"><span data-stu-id="15c53-138">Host device got disconnected</span></span>                          |
| <span data-ttu-id="15c53-139">UX_OTG_HOST_TO_SLAVE</span><span class="sxs-lookup"><span data-stu-id="15c53-139">UX_OTG_HOST_TO_SLAVE</span></span> | <span data-ttu-id="15c53-140">4</span><span class="sxs-lookup"><span data-stu-id="15c53-140">4</span></span>     | <span data-ttu-id="15c53-141">Rol, konaktan bağımlı olarak takas</span><span class="sxs-lookup"><span data-stu-id="15c53-141">Role swap from Host to Slave</span></span>                          |
| <span data-ttu-id="15c53-142">UX_OTG_SLAVE_TO_IDLE</span><span class="sxs-lookup"><span data-stu-id="15c53-142">UX_OTG_SLAVE_TO_IDLE</span></span> | <span data-ttu-id="15c53-143">5</span><span class="sxs-lookup"><span data-stu-id="15c53-143">5</span></span>     | <span data-ttu-id="15c53-144">Bağımlı cihazın bağlantısı kesildi</span><span class="sxs-lookup"><span data-stu-id="15c53-144">Slave device is disconnected</span></span>                          |
| <span data-ttu-id="15c53-145">UX_OTG_SLAVE_TO_HOST</span><span class="sxs-lookup"><span data-stu-id="15c53-145">UX_OTG_SLAVE_TO_HOST</span></span> | <span data-ttu-id="15c53-146">6</span><span class="sxs-lookup"><span data-stu-id="15c53-146">6</span></span>     | <span data-ttu-id="15c53-147">Rolü bağımlı sunucudan konağa değiştirme</span><span class="sxs-lookup"><span data-stu-id="15c53-147">Role swap from Slave to Host</span></span>                          |

## <a name="interrupt-handlers"></a><span data-ttu-id="15c53-148">Kesme işleyicileri</span><span class="sxs-lookup"><span data-stu-id="15c53-148">Interrupt handlers</span></span>

<span data-ttu-id="15c53-149">OTG için hem konak hem de cihaz denetleyicisi sürücüleri, SRP ve VBUS nedeniyle belirli sinyallere göre geleneksel USB kesmelerinin ötesinde sinyalleri izlemek için farklı kesme işleyicileri gerektirir.</span><span class="sxs-lookup"><span data-stu-id="15c53-149">Both host and device controller drivers for OTG needs different interrupt handlers to monitor signals beyond traditional USB interrupts, in particular signals due to SRP and VBUS.</span></span>

<span data-ttu-id="15c53-150">USB OTG denetleyicisi başlatma.</span><span class="sxs-lookup"><span data-stu-id="15c53-150">How to initialize a USB OTG controller.</span></span> <span data-ttu-id="15c53-151">Burada örnek olarak NXP LPC3131 kullanıyoruz.</span><span class="sxs-lookup"><span data-stu-id="15c53-151">We use the NXP LPC3131 as an example here.</span></span>

```C
/* Initialize the LPC3131 OTG controller. */
status = ux_otg_lpc3131_initialize(0x19000000, lpc3131_vbus_function,
    tx_demo_change_mode_callback);
```

<span data-ttu-id="15c53-152">Bu örnekte, VBUS işlevini ve mod değişikliği (konaktan bağımlı veya tam tersi) için bir geri çağırma geçirerek OTG modunda LPC3131 'i başlatacağız.</span><span class="sxs-lookup"><span data-stu-id="15c53-152">In this example, we initialize the LPC3131 in OTG mode by passing a VBUS function and a callback for mode change (from host to slave or vice versa).</span></span>

<span data-ttu-id="15c53-153">Geri çağırma işlevi yalnızca yeni modu kaydedip yeni durumu uygulamak için bekleyen bir iş parçacığını uyandırmalıdır.</span><span class="sxs-lookup"><span data-stu-id="15c53-153">The callback function should simply record the new mode and wake up a pending thread to act up the new state.</span></span>

```C
void tx_demo_change_mode_callback(ULONG mode) {
    /* Simply save the otg mode. */
    otg_mode = mode;

    /* Wake up the thread that is waiting. */
    ux_utility_semaphore_put(&mode_change_semaphore);
}
```

<span data-ttu-id="15c53-154">Geçirilen mod değeri aşağıdaki değerlere sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="15c53-154">The mode value that is passed can have the following values.</span></span>

- <span data-ttu-id="15c53-155">**UX_OTG_MODE_IDLE**</span><span class="sxs-lookup"><span data-stu-id="15c53-155">**UX_OTG_MODE_IDLE**</span></span>
- <span data-ttu-id="15c53-156">**UX_OTG_MODE_SLAVE**</span><span class="sxs-lookup"><span data-stu-id="15c53-156">**UX_OTG_MODE_SLAVE**</span></span>
- <span data-ttu-id="15c53-157">**UX_OTG_MODE_HOST**</span><span class="sxs-lookup"><span data-stu-id="15c53-157">**UX_OTG_MODE_HOST**</span></span>

<span data-ttu-id="15c53-158">Uygulama, şu değişkene bakarak cihazın ne olduğunu her zaman denetleyebilir:</span><span class="sxs-lookup"><span data-stu-id="15c53-158">The application can always check what the device is by looking at the variable:</span></span>

```C
_ux_system_otg -> ux_system_otg_device_type
```

<span data-ttu-id="15c53-159">Değerleri aşağıdakilerden herhangi biri olabilir.</span><span class="sxs-lookup"><span data-stu-id="15c53-159">Its values can be any of the following.</span></span>

- <span data-ttu-id="15c53-160">**UX_OTG_DEVICE_A**</span><span class="sxs-lookup"><span data-stu-id="15c53-160">**UX_OTG_DEVICE_A**</span></span>
- <span data-ttu-id="15c53-161">**UX_OTG_DEVICE_B**</span><span class="sxs-lookup"><span data-stu-id="15c53-161">**UX_OTG_DEVICE_B**</span></span>
- <span data-ttu-id="15c53-162">**UX_OTG_DEVICE_IDLE**</span><span class="sxs-lookup"><span data-stu-id="15c53-162">**UX_OTG_DEVICE_IDLE**</span></span>

<span data-ttu-id="15c53-163">Bir USB OTG ana bilgisayar cihazı, aşağıdaki komutu vererek her zaman bir rol takası isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="15c53-163">A USB OTG host device can always ask for a role swap by issuing the following command.</span></span>

```C
/* Ask the stack to perform a HNP swap with the device. We relinquish the host role to A device. */
ux_host_stack_role_swap(storage -> ux_host_class_storage_device);
```

<span data-ttu-id="15c53-164">Bir bağımlı cihaz için, soruna bir komut yoktur, ancak bağımlı cihaz, **GET_STATUS** bir sorun olduğunda ana bilgisayar tarafından çekilecek rolü değiştirmek için bir durum ayarlayabilir ve ardından takas başlatılır.</span><span class="sxs-lookup"><span data-stu-id="15c53-164">For a slave device, there is no command to issue but the slave device can set a state to change the role, which will be picked up by the host when it issues a **GET_STATUS** and the swap will then be initiated.</span></span>

```C
/* We are a B device, ask for role swap.
   The next GET_STATUS from the host will get the status change and do the HNP. */
_ux_system_otg -> ux_system_otg_slave_role_swap_flag =
    UX_OTG_HOST_REQUEST_FLAG;
```
