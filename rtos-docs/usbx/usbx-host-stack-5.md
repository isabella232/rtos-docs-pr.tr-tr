---
title: Bölüm 5-USBX konak sınıfları API 'SI
description: USBX konak sınıfları API 'SI hakkında bilgi edinin.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: bf5876042e08a59979adcd429917bfc3fbfdbc20
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104828619"
---
# <a name="chapter-5---usbx-host-classes-api"></a><span data-ttu-id="e13a5-103">Bölüm 5-USBX konak sınıfları API 'SI</span><span class="sxs-lookup"><span data-stu-id="e13a5-103">Chapter 5 - USBX Host Classes API</span></span>

<span data-ttu-id="e13a5-104">Bu bölümde, USBX konak sınıflarının tüm sunulan API 'Leri ele alınmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e13a5-104">This chapter covers all the exposed APIs of the USBX host classes.</span></span> <span data-ttu-id="e13a5-105">Her sınıf için aşağıdaki API 'Ler ayrıntılı olarak açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="e13a5-105">The following APIs for each class are described in detail.</span></span>

- <span data-ttu-id="e13a5-106">HID sınıfı</span><span class="sxs-lookup"><span data-stu-id="e13a5-106">HID class</span></span>
- <span data-ttu-id="e13a5-107">CDC-ACM sınıfı</span><span class="sxs-lookup"><span data-stu-id="e13a5-107">CDC-ACM class</span></span>
- <span data-ttu-id="e13a5-108">CDC-ECD sınıfı</span><span class="sxs-lookup"><span data-stu-id="e13a5-108">CDC-ECM class</span></span>
- <span data-ttu-id="e13a5-109">Depolama sınıfı</span><span class="sxs-lookup"><span data-stu-id="e13a5-109">Storage class</span></span>

## <a name="ux_host_class_hid_client_register"></a><span data-ttu-id="e13a5-110">ux_host_class_hid_client_register</span><span class="sxs-lookup"><span data-stu-id="e13a5-110">ux_host_class_hid_client_register</span></span>

<span data-ttu-id="e13a5-111">HID sınıfına bir HID istemcisini kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e13a5-111">Register a HID client to the HID class.</span></span>

### <a name="prototype"></a><span data-ttu-id="e13a5-112">Prototype</span><span class="sxs-lookup"><span data-stu-id="e13a5-112">Prototype</span></span>

```c
UINT ux_host_class_hid_client_register(
    UCHAR *hid_client_name,
    UINT (*hid_client_handler)
    (struct UX_HOST_CLASS_HID_CLIENT_COMMAND_STRUCT *));
```

### <a name="description"></a><span data-ttu-id="e13a5-113">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e13a5-113">Description</span></span>

<span data-ttu-id="e13a5-114">Bu işlev, bir HID istemcisini HID sınıfına kaydetmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e13a5-114">This function is used to register a HID client to the HID class.</span></span> <span data-ttu-id="e13a5-115">HID sınıfının, bu cihazdan veri istenmeden önce bir HID aygıtı ile HID istemcisi arasında bir eşleşme bulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e13a5-115">The HID class needs to find a match between a HID device and HID client before requesting data from this device.</span></span>

> [!NOTE]
> <span data-ttu-id="e13a5-116">Hid_client_name C dizesi NULL ile sonlandırılmış olmalı ve bunun uzunluğu (NULL-Sonlandırıcı kendisi olmadan) **UX_HOST_CLASS_HID_MAX_CLIENT_NAME_LENGTH** daha büyük olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="e13a5-116">The C string of hid_client_name must be NULL-terminated and the length of it (without the NULL-terminator itself) must be no larger than **UX_HOST_CLASS_HID_MAX_CLIENT_NAME_LENGTH**.</span></span>

### <a name="parameters"></a><span data-ttu-id="e13a5-117">Parametreler</span><span class="sxs-lookup"><span data-stu-id="e13a5-117">Parameters</span></span>

- <span data-ttu-id="e13a5-118">**hid_client_name** HID istemci adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="e13a5-118">**hid_client_name** Pointer to the HID client name.</span></span>
- <span data-ttu-id="e13a5-119">**hid_client_handler** HID istemci işleyicisine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="e13a5-119">**hid_client_handler** Pointer to the HID client handler.</span></span>

### <a name="return-values"></a><span data-ttu-id="e13a5-120">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="e13a5-120">Return Values</span></span>

- <span data-ttu-id="e13a5-121">**UX_SUCCESS** (0x00) veri aktarımı tamamlandı</span><span class="sxs-lookup"><span data-stu-id="e13a5-121">**UX_SUCCESS** (0x00) The data transfer was completed</span></span>
- <span data-ttu-id="e13a5-122">İstemci için **UX_MEMORY_INSUFFICIENT** (0x12) bellek ayırması başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="e13a5-122">**UX_MEMORY_INSUFFICIENT** (0x12) Memory allocation for client failed.</span></span>
- <span data-ttu-id="e13a5-123">**UX_MEMORY_ARRAY_FULL** (0x1A) en fazla istemci zaten kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="e13a5-123">**UX_MEMORY_ARRAY_FULL** (0x1a) Max clients already registered.</span></span>
- <span data-ttu-id="e13a5-124">**UX_HOST_CLASS_ALREADY_INSTALLED** (0x58) Bu sınıf zaten var</span><span class="sxs-lookup"><span data-stu-id="e13a5-124">**UX_HOST_CLASS_ALREADY_INSTALLED** (0x58) This class already exists</span></span>

### <a name="example"></a><span data-ttu-id="e13a5-125">Örnek</span><span class="sxs-lookup"><span data-stu-id="e13a5-125">Example</span></span>

```c
UINT status;

/* The following example illustrates how to register a HID client, in
this case a USB mouse, to the HID class. */

status = ux_host_class_hid_client_register("ux_host_class_hid_client_mouse",
    ux_host_class_hid_mouse_entry);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_hid_report_callback_register"></a><span data-ttu-id="e13a5-126">ux_host_class_hid_report_callback_register</span><span class="sxs-lookup"><span data-stu-id="e13a5-126">ux_host_class_hid_report_callback_register</span></span>

<span data-ttu-id="e13a5-127">HID sınıfından bir geri çağırma kaydeder.</span><span class="sxs-lookup"><span data-stu-id="e13a5-127">Register a callback from the HID class.</span></span>

### <a name="prototype"></a><span data-ttu-id="e13a5-128">Prototype</span><span class="sxs-lookup"><span data-stu-id="e13a5-128">Prototype</span></span>

```c
UINT ux_host_class_hid_report_callback_register(
    UX_HOST_CLASS_HID *hid,
    UX_HOST_CLASS_HID_REPORT_CALLBACK *call_back);
```

### <a name="description"></a><span data-ttu-id="e13a5-129">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e13a5-129">Description</span></span>

<span data-ttu-id="e13a5-130">Bu işlev, bir rapor alındığında, HID sınıfından bir geri çağırma işlemini HID istemcisine kaydetmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e13a5-130">This function is used to register a callback from the HID class to the HID client when a report is received.</span></span>

### <a name="parameters"></a><span data-ttu-id="e13a5-131">Parametreler</span><span class="sxs-lookup"><span data-stu-id="e13a5-131">Parameters</span></span>

- <span data-ttu-id="e13a5-132">**HID** HID sınıfı örneğine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="e13a5-132">**hid** Pointer to the HID class instance</span></span>
- <span data-ttu-id="e13a5-133">**call_back** Call_back yapısına yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="e13a5-133">**call_back** Pointer to the call_back structure</span></span>

### <a name="return-values"></a><span data-ttu-id="e13a5-134">Dönüş değerleri</span><span class="sxs-lookup"><span data-stu-id="e13a5-134">Return values</span></span>

- <span data-ttu-id="e13a5-135">**UX_SUCCESS** (0x00) veri aktarımı tamamlandı</span><span class="sxs-lookup"><span data-stu-id="e13a5-135">**UX_SUCCESS** (0x00) The data transfer was completed</span></span>
- <span data-ttu-id="e13a5-136">**UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) geçersiz HID örneği.</span><span class="sxs-lookup"><span data-stu-id="e13a5-136">**UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) Invalid HID instance.</span></span>
- <span data-ttu-id="e13a5-137">Rapor geri çağırma kaydında **UX_HOST_CLASS_HID_REPORT_ERROR** (0x79) hatası.</span><span class="sxs-lookup"><span data-stu-id="e13a5-137">**UX_HOST_CLASS_HID_REPORT_ERROR** (0x79) Error in the report callback registration.</span></span>

### <a name="example"></a><span data-ttu-id="e13a5-138">Örnek</span><span class="sxs-lookup"><span data-stu-id="e13a5-138">Example</span></span>

```c
UINT status;

/* This example illustrates how to register a HID client, in this case a USB mouse, to the HID class. In this case, the HID client is asking the HID class to call the client for each usage received in the HID report. */

call_back.ux_host_class_hid_report_callback_id = 0;
call_back.ux_host_class_hid_report_callback_function = ux_host_class_hid_mouse_callback;

call_back.ux_host_class_hid_report_callback_buffer = UX_NULL;
call_back.ux_host_class_hid_report_callback_flags = UX_HOST_CLASS_HID_REPORT_INDIVIDUAL_USAGE;

call_back.ux_host_class_hid_report_callback_length = 0;

status = ux_host_class_hid_report_callback_register(hid, &call_back);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_hid_periodic_report_start"></a><span data-ttu-id="e13a5-139">ux_host_class_hid_periodic_report_start</span><span class="sxs-lookup"><span data-stu-id="e13a5-139">ux_host_class_hid_periodic_report_start</span></span>

<span data-ttu-id="e13a5-140">Bir HID sınıf örneği için dönemsel uç noktayı başlatın.</span><span class="sxs-lookup"><span data-stu-id="e13a5-140">Start the periodic endpoint for a HID class instance.</span></span>

### <a name="prototype"></a><span data-ttu-id="e13a5-141">Prototype</span><span class="sxs-lookup"><span data-stu-id="e13a5-141">Prototype</span></span>

```c
UINT ux_host_class_hid_periodic_report_start(UX_HOST_CLASS_HID *hid);
```

### <a name="description"></a><span data-ttu-id="e13a5-142">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e13a5-142">Description</span></span>

<span data-ttu-id="e13a5-143">Bu işlev, bu HID istemcisine bağlanan HID sınıfının örneği için dönemsel (kesme) uç noktasını başlatmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e13a5-143">This function is used to start the periodic (interrupt) endpoint for the instance of the HID class that is bound to this HID client.</span></span> <span data-ttu-id="e13a5-144">HID sınıfı, HID istemcisi etkinleştirilinceye kadar düzenli bitiş noktasını başlatamıyor ve bu nedenle bu uç noktayı rapor almak için başlatmak üzere HID istemcisine bırakılır.</span><span class="sxs-lookup"><span data-stu-id="e13a5-144">The HID class cannot start the periodic endpoint until the HID client is activated and therefore it is left to the HID client to start this endpoint to receive reports.</span></span>

### <a name="input-parameter"></a><span data-ttu-id="e13a5-145">Giriş parametresi</span><span class="sxs-lookup"><span data-stu-id="e13a5-145">Input Parameter</span></span>

- <span data-ttu-id="e13a5-146">**HID** HID sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="e13a5-146">**hid** Pointer to the HID class instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="e13a5-147">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="e13a5-147">Return Values</span></span>

- <span data-ttu-id="e13a5-148">**UX_SUCCESS** (0x00) düzenli raporlama başarıyla başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="e13a5-148">**UX_SUCCESS** (0x00) Periodic reporting successfully started.</span></span>
- <span data-ttu-id="e13a5-149">düzenli raporda **ux_host_class_hid_PERIODIC_REPORT_ERROR** (0x7A) hatası.</span><span class="sxs-lookup"><span data-stu-id="e13a5-149">**ux_host_class_hid_PERIODIC_REPORT_ERROR** (0x7A) Error in the periodic report.</span></span>
- <span data-ttu-id="e13a5-150">**UX_HOST_CLASS_INSTANCE_UNKNOWN** (0X5B) HID sınıfı örneği yok.</span><span class="sxs-lookup"><span data-stu-id="e13a5-150">**UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) HID class instance does not exist.</span></span>

### <a name="example"></a><span data-ttu-id="e13a5-151">Örnek</span><span class="sxs-lookup"><span data-stu-id="e13a5-151">Example</span></span>

```c
UINT status;

/* The following example illustrates how to start the periodic
endpoint. */

status = ux_host_class_hid_periodic_report_start(hid);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_hid_periodic_report_stop"></a><span data-ttu-id="e13a5-152">ux_host_class_hid_periodic_report_stop</span><span class="sxs-lookup"><span data-stu-id="e13a5-152">ux_host_class_hid_periodic_report_stop</span></span>

<span data-ttu-id="e13a5-153">Bir HID sınıf örneği için dönemsel uç noktayı durdurun.</span><span class="sxs-lookup"><span data-stu-id="e13a5-153">Stop the periodic endpoint for a HID class instance.</span></span>

### <a name="prototype"></a><span data-ttu-id="e13a5-154">Prototype</span><span class="sxs-lookup"><span data-stu-id="e13a5-154">Prototype</span></span>

```c
UINT ux_host_class_hid_periodic_report_stop(UX_HOST_CLASS_HID *hid);
```

### <a name="description"></a><span data-ttu-id="e13a5-155">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e13a5-155">Description</span></span>

<span data-ttu-id="e13a5-156">Bu işlev, bu HID istemcisine bağlanan HID sınıfının örneği için periyodik (kesme) uç noktasını durdurmak üzere kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e13a5-156">This function is used to stop the periodic (interrupt) endpoint for the instance of the HID class that is bound to this HID client.</span></span> <span data-ttu-id="e13a5-157">HID istemcisi devre dışı bırakılana kadar HID sınıfı, tüm kaynakları serbest bırakılıncaya ve bu nedenle bu uç noktayı durdurmak için HID istemcisine bırakılıncaya kadar, düzenli bitiş noktasını durduramıyor.</span><span class="sxs-lookup"><span data-stu-id="e13a5-157">The HID class cannot stop the periodic endpoint until the HID client is deactivated, all its resources freed and therefore it is left to the HID client to stop this endpoint.</span></span>

### <a name="input-parameter"></a><span data-ttu-id="e13a5-158">Giriş parametresi</span><span class="sxs-lookup"><span data-stu-id="e13a5-158">Input Parameter</span></span>

- <span data-ttu-id="e13a5-159">**HID** HID sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="e13a5-159">**hid** Pointer to the HID class instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="e13a5-160">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="e13a5-160">Return Values</span></span>

- <span data-ttu-id="e13a5-161">**UX_SUCCESS** (0x00) düzenli raporlama başarıyla durduruldu.</span><span class="sxs-lookup"><span data-stu-id="e13a5-161">**UX_SUCCESS** (0x00) Periodic reporting successfully stopped.</span></span>
- <span data-ttu-id="e13a5-162">düzenli raporda **ux_host_class_hid_PERIODIC_REPORT_ERROR** (0x7A) hatası.</span><span class="sxs-lookup"><span data-stu-id="e13a5-162">**ux_host_class_hid_PERIODIC_REPORT_ERROR** (0x7A) Error in the periodic report.</span></span>
- <span data-ttu-id="e13a5-163">**UX_HOST_CLASS_INSTANCE_UNKNOWN** (0X5B) HID sınıfı örneği yok</span><span class="sxs-lookup"><span data-stu-id="e13a5-163">**UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) HID class instance does not exist</span></span>

### <a name="example"></a><span data-ttu-id="e13a5-164">Örnek</span><span class="sxs-lookup"><span data-stu-id="e13a5-164">Example</span></span>

```c
UINT status;

/* The following example illustrates how to stop the periodic endpoint. */

status = ux_host_class_hid_periodic_report_stop(hid);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_hid_report_get"></a><span data-ttu-id="e13a5-165">ux_host_class_hid_report_get</span><span class="sxs-lookup"><span data-stu-id="e13a5-165">ux_host_class_hid_report_get</span></span>

<span data-ttu-id="e13a5-166">Bir HID sınıf örneğinden rapor alın.</span><span class="sxs-lookup"><span data-stu-id="e13a5-166">Get a report from a HID class instance.</span></span>

### <a name="prototype"></a><span data-ttu-id="e13a5-167">Prototype</span><span class="sxs-lookup"><span data-stu-id="e13a5-167">Prototype</span></span>

```c
UINT ux_host_class_hid_report_get(
    UX_HOST_CLASS_HID *hid,
    UX_HOST_CLASS_HID_CLIENT_REPORT *client_report);
```

### <a name="description"></a><span data-ttu-id="e13a5-168">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e13a5-168">Description</span></span>

<span data-ttu-id="e13a5-169">Bu işlev, düzenli bitiş noktasına bağlı olmadan doğrudan cihazdan rapor almak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e13a5-169">This function is used to receive a report directly from the device without relying on the periodic endpoint.</span></span> <span data-ttu-id="e13a5-170">Bu rapor, denetim uç noktasından geliyor, ancak işlemi, düzenli uç noktada gelmekle aynı.</span><span class="sxs-lookup"><span data-stu-id="e13a5-170">This report is coming from the control endpoint but its treatment is the same as though it were coming on the periodic endpoint.</span></span>

### <a name="parameters"></a><span data-ttu-id="e13a5-171">Parametreler</span><span class="sxs-lookup"><span data-stu-id="e13a5-171">Parameters</span></span>

- <span data-ttu-id="e13a5-172">**HID** HID sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="e13a5-172">**hid** Pointer to the HID class instance.</span></span>
- <span data-ttu-id="e13a5-173">**client_report** HID istemci raporuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="e13a5-173">**client_report** Pointer to the HID client report.</span></span>

### <a name="return-values"></a><span data-ttu-id="e13a5-174">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="e13a5-174">Return Values</span></span>

- <span data-ttu-id="e13a5-175">**UX_SUCCESS** (0x00) rapor başarıyla alındı.</span><span class="sxs-lookup"><span data-stu-id="e13a5-175">**UX_SUCCESS** (0x00) The report was successfully received.</span></span>
- <span data-ttu-id="e13a5-176">**UX_HOST_CLASS_HID_REPORT_ERROR** (0x70) istemci raporu geçersiz ya da aktarım sırasında hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="e13a5-176">**UX_HOST_CLASS_HID_REPORT_ERROR** (0x70) Either client report was invalid or error during transfer.</span></span>
- <span data-ttu-id="e13a5-177">**UX_HOST_CLASS_INSTANCE_UNKNOWN** (0X5B) HID sınıfı örneği yok.</span><span class="sxs-lookup"><span data-stu-id="e13a5-177">**UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) HID class instance does not exist.</span></span>
- <span data-ttu-id="e13a5-178">**UX_BUFFER_OVERFLOW** (0x5D) sağlanan arabellek sıkıştırılmamış rapora uyum sağlayacak kadar büyük değil.</span><span class="sxs-lookup"><span data-stu-id="e13a5-178">**UX_BUFFER_OVERFLOW** (0x5d) The buffer supplied is not big enough to accommodate the uncompressed report.</span></span>

### <a name="example"></a><span data-ttu-id="e13a5-179">Örnek</span><span class="sxs-lookup"><span data-stu-id="e13a5-179">Example</span></span>

```c
UX_HOST_CLASS_HID_CLIENT_REPORT input_report;

UINT status;

/* The following example illustrates how to get a report. */

input_report.ux_host_class_hid_client_report = hid_report;
input_report.ux_host_class_hid_client_report_buffer = buffer;
input_report.ux_host_class_hid_client_report_length = length;
input_report.ux_host_class_hid_client_flags = UX_HOST_CLASS_HID_REPORT_INDIVIDUAL_USAGE;

status = ux_host_class_hid_report_get(hid, &input_report);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_hid_report_set"></a><span data-ttu-id="e13a5-180">ux_host_class_hid_report_set</span><span class="sxs-lookup"><span data-stu-id="e13a5-180">ux_host_class_hid_report_set</span></span>

<span data-ttu-id="e13a5-181">Rapor gönderme</span><span class="sxs-lookup"><span data-stu-id="e13a5-181">Send a report</span></span>

### <a name="prototype"></a><span data-ttu-id="e13a5-182">Prototype</span><span class="sxs-lookup"><span data-stu-id="e13a5-182">Prototype</span></span>

```c
UINT ux_host_class_hid_report_set(
    UX_HOST_CLASS_HID *hid,
    UX_HOST_CLASS_HID_CLIENT_REPORT *client_report);
```

### <a name="description"></a><span data-ttu-id="e13a5-183">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e13a5-183">Description</span></span>

<span data-ttu-id="e13a5-184">Bu işlev, bir raporu doğrudan cihaza göndermek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e13a5-184">This function is used to send a report directly to the device.</span></span>

### <a name="parameters"></a><span data-ttu-id="e13a5-185">Parametreler</span><span class="sxs-lookup"><span data-stu-id="e13a5-185">Parameters</span></span>

- <span data-ttu-id="e13a5-186">**HID** HID sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="e13a5-186">**hid** Pointer to the HID class instance.</span></span>
- <span data-ttu-id="e13a5-187">**client_report** HID istemci raporuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="e13a5-187">**client_report** Pointer to the HID client report.</span></span>

### <a name="return-values"></a><span data-ttu-id="e13a5-188">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="e13a5-188">Return Values</span></span>

- <span data-ttu-id="e13a5-189">**UX_SUCCESS** (0x00) rapor başarıyla gönderildi.</span><span class="sxs-lookup"><span data-stu-id="e13a5-189">**UX_SUCCESS** (0x00) The report was successfully sent.</span></span>
- <span data-ttu-id="e13a5-190">**UX_HOST_CLASS_HID_REPORT_ERROR** (0x70) istemci raporu geçersiz ya da aktarım sırasında hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="e13a5-190">**UX_HOST_CLASS_HID_REPORT_ERROR** (0x70) Either client report was invalid or error during transfer.</span></span>
- <span data-ttu-id="e13a5-191">**UX_HOST_CLASS_INSTANCE_UNKNOWN** (0X5B) HID sınıfı örneği yok.</span><span class="sxs-lookup"><span data-stu-id="e13a5-191">**UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) HID class instance does not exist.</span></span>
- <span data-ttu-id="e13a5-192">**UX_HOST_CLASS_HID_REPORT_OVERFLOW** (0x5D) sağlanan arabellek sıkıştırılmamış rapora uyum sağlayacak kadar büyük değil.</span><span class="sxs-lookup"><span data-stu-id="e13a5-192">**UX_HOST_CLASS_HID_REPORT_OVERFLOW** (0x5d) The buffer supplied is not big enough to accommodate the uncompressed report.</span></span>

### <a name="example"></a><span data-ttu-id="e13a5-193">Örnek</span><span class="sxs-lookup"><span data-stu-id="e13a5-193">Example</span></span>

```c
/* The following example illustrates how to send a report. */

UX_HOST_CLASS_HID_CLIENT_REPORT input_report;

input_report.ux_host_class_hid_client_report = hid_report;
input_report.ux_host_class_hid_client_report_buffer = buffer;
input_report.ux_host_class_hid_client_report_length = length;
input_report.ux_host_class_hid_client_report_flags = UX_HOST_CLASS_HID_REPORT_INDIVIDUAL_USAGE;

status = ux_host_class_hid_report_set(hid, &input_report);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_hid_mouse_buttons_get"></a><span data-ttu-id="e13a5-194">ux_host_class_hid_mouse_buttons_get</span><span class="sxs-lookup"><span data-stu-id="e13a5-194">ux_host_class_hid_mouse_buttons_get</span></span>

<span data-ttu-id="e13a5-195">Fare düğmelerini al.</span><span class="sxs-lookup"><span data-stu-id="e13a5-195">Get mouse buttons.</span></span>

### <a name="prototype"></a><span data-ttu-id="e13a5-196">Prototype</span><span class="sxs-lookup"><span data-stu-id="e13a5-196">Prototype</span></span>

```c
UINT ux_host_class_hid_mouse_buttons_get(
    UX_HOST_CLASS_HID_MOUSE *mouse_instance,
    ULONG *mouse_buttons);
```

### <a name="description"></a><span data-ttu-id="e13a5-197">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e13a5-197">Description</span></span>

<span data-ttu-id="e13a5-198">Bu işlev, fare düğmelerini almak için kullanılır</span><span class="sxs-lookup"><span data-stu-id="e13a5-198">This function is used to get the mouse buttons</span></span>

### <a name="parameters"></a><span data-ttu-id="e13a5-199">Parametreler</span><span class="sxs-lookup"><span data-stu-id="e13a5-199">Parameters</span></span>

- <span data-ttu-id="e13a5-200">**mouse_instance** HID fare örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="e13a5-200">**mouse_instance** Pointer to the HID mouse instance.</span></span>
- <span data-ttu-id="e13a5-201">**mouse_buttons** Dönüş düğmelerinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="e13a5-201">**mouse_buttons** Pointer to the return buttons.</span></span>

### <a name="return-values"></a><span data-ttu-id="e13a5-202">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="e13a5-202">Return Values</span></span>

- <span data-ttu-id="e13a5-203">**UX_SUCCESS** (0x00) fare düğmesi başarıyla alındı.</span><span class="sxs-lookup"><span data-stu-id="e13a5-203">**UX_SUCCESS** (0x00) Mouse button successfully retrieved.</span></span>
- <span data-ttu-id="e13a5-204">**UX_HOST_CLASS_INSTANCE_UNKNOWN** (0X5B) HID sınıfı örneği yok.</span><span class="sxs-lookup"><span data-stu-id="e13a5-204">**UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) HID class instance does not exist.</span></span>

### <a name="example"></a><span data-ttu-id="e13a5-205">Örnek</span><span class="sxs-lookup"><span data-stu-id="e13a5-205">Example</span></span>

```c
/* The following example illustrates how to obtain mouse buttons. */

UX_HOST_CLASS_HID_MOUSE *mouse_instance;

ULONG mouse_buttons;

status = ux_host_class_hid_mouse_button_get(mouse_instance, &mouse_buttons);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_hid_mouse_position_get"></a><span data-ttu-id="e13a5-206">ux_host_class_hid_mouse_position_get</span><span class="sxs-lookup"><span data-stu-id="e13a5-206">ux_host_class_hid_mouse_position_get</span></span>

<span data-ttu-id="e13a5-207">Fare konumunu al.</span><span class="sxs-lookup"><span data-stu-id="e13a5-207">Get mouse position.</span></span>

### <a name="prototype"></a><span data-ttu-id="e13a5-208">Prototype</span><span class="sxs-lookup"><span data-stu-id="e13a5-208">Prototype</span></span>

```c
UINT ux_host_class_hid_mouse_position_get(
    UX_HOST_CLASS_HID_MOUSE *mouse_instance,
    SLONG *mouse_x_position, 
    SLONG *mouse_y_position);
```

### <a name="description"></a><span data-ttu-id="e13a5-209">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e13a5-209">Description</span></span>

<span data-ttu-id="e13a5-210">Bu işlev, x & y koordinatlarındaki fare konumunu almak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e13a5-210">This function is used to get the mouse position in x & y coordinates.</span></span>

### <a name="parameters"></a><span data-ttu-id="e13a5-211">Parametreler</span><span class="sxs-lookup"><span data-stu-id="e13a5-211">Parameters</span></span>

- <span data-ttu-id="e13a5-212">**mouse_instance** HID fare örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="e13a5-212">**mouse_instance** Pointer to the HID mouse instance.</span></span>
- <span data-ttu-id="e13a5-213">**mouse_x_position** X koordinatı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="e13a5-213">**mouse_x_position** Pointer to the x coordinate.</span></span>
- <span data-ttu-id="e13a5-214">**mouse_y_position** Y koordinatı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="e13a5-214">**mouse_y_position** Pointer to the y coordinate.</span></span>

### <a name="return-values"></a><span data-ttu-id="e13a5-215">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="e13a5-215">Return Values</span></span>

- <span data-ttu-id="e13a5-216">**UX_SUCCESS** (0x00) X &amp; Y koordinatları başarıyla alındı.</span><span class="sxs-lookup"><span data-stu-id="e13a5-216">**UX_SUCCESS** (0x00) X &amp; Y coordinates successfully retrieved.</span></span>
- <span data-ttu-id="e13a5-217">**UX_HOST_CLASS_INSTANCE_UNKNOWN** (0X5B) HID sınıfı örneği yok.</span><span class="sxs-lookup"><span data-stu-id="e13a5-217">**UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) HID class instance does not exist.</span></span>

### <a name="example"></a><span data-ttu-id="e13a5-218">Örnek</span><span class="sxs-lookup"><span data-stu-id="e13a5-218">Example</span></span>

```c
/* The following example illustrates how to obtain mouse coordinates. */

UX_HOST_CLASS_HID_MOUSE *mouse_instance;

SLONG mouse_x_position;
SLONG mouse_y_position;

status = ux_host_class_hid_mouse_position_get(mouse_instance,
    &mouse_x_position, &mouse_y_position);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_hid_keyboard_key_get"></a><span data-ttu-id="e13a5-219">ux_host_class_hid_keyboard_key_get</span><span class="sxs-lookup"><span data-stu-id="e13a5-219">ux_host_class_hid_keyboard_key_get</span></span>

<span data-ttu-id="e13a5-220">Klavye anahtarını ve durumunu alın.</span><span class="sxs-lookup"><span data-stu-id="e13a5-220">Get keyboard key and state.</span></span>

### <a name="prototype"></a><span data-ttu-id="e13a5-221">Prototype</span><span class="sxs-lookup"><span data-stu-id="e13a5-221">Prototype</span></span>

```c
UINT ux_host_class_hid_keyboard_key_get(
    UX_HOST_CLASS_HID_KEYBOARD *keyboard_instance,
    ULONG *keyboard_key, 
    ULONG *keyboard_state);
```

### <a name="description"></a><span data-ttu-id="e13a5-222">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e13a5-222">Description</span></span>

<span data-ttu-id="e13a5-223">Bu işlev, klavye anahtarını ve durumunu almak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e13a5-223">This function is used to get the keyboard key and state.</span></span>

### <a name="parameters"></a><span data-ttu-id="e13a5-224">Parametreler</span><span class="sxs-lookup"><span data-stu-id="e13a5-224">Parameters</span></span>

- <span data-ttu-id="e13a5-225">**keyboard_instance** HID Klavye örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="e13a5-225">**keyboard_instance** Pointer to the HID keyboard instance.</span></span>
- <span data-ttu-id="e13a5-226">**keyboard_key** Klavye anahtar kapsayıcısı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="e13a5-226">**keyboard_key** Pointer to keyboard key container.</span></span>
- <span data-ttu-id="e13a5-227">**keyboard_state** Klavye durumu kapsayıcısının işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="e13a5-227">**keyboard_state** Pointer to the keyboard state container.</span></span>

### <a name="return-values"></a><span data-ttu-id="e13a5-228">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="e13a5-228">Return Values</span></span>

- <span data-ttu-id="e13a5-229">**UX_SUCCESS** (0x00) anahtar ve durum başarıyla alındı.</span><span class="sxs-lookup"><span data-stu-id="e13a5-229">**UX_SUCCESS** (0x00) Key and state successfully retrieved.</span></span>
- <span data-ttu-id="e13a5-230">Raporlanacak hiçbir şey **UX_ERROR** (0xFF).</span><span class="sxs-lookup"><span data-stu-id="e13a5-230">**UX_ERROR** (0xff) Nothing to report.</span></span>
- <span data-ttu-id="e13a5-231">**UX_HOST_CLASS_INSTANCE_UNKNOWN** (0X5B) HID sınıfı örneği yok.</span><span class="sxs-lookup"><span data-stu-id="e13a5-231">**UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) HID class instance does not exist.</span></span>

<span data-ttu-id="e13a5-232">Klavye durumu aşağıdaki değerlere sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="e13a5-232">The keyboard state can have the following values.</span></span>

- <span data-ttu-id="e13a5-233">**UX_HID_KEYBOARD_STATE_KEY_UP** 0x10000</span><span class="sxs-lookup"><span data-stu-id="e13a5-233">**UX_HID_KEYBOARD_STATE_KEY_UP** 0x10000</span></span>
- <span data-ttu-id="e13a5-234">**UX_HID_KEYBOARD_STATE_NUM_LOCK** 0x0001</span><span class="sxs-lookup"><span data-stu-id="e13a5-234">**UX_HID_KEYBOARD_STATE_NUM_LOCK** 0x0001</span></span>
- <span data-ttu-id="e13a5-235">**UX_HID_KEYBOARD_STATE_CAPS_LOCK** 0x0002</span><span class="sxs-lookup"><span data-stu-id="e13a5-235">**UX_HID_KEYBOARD_STATE_CAPS_LOCK** 0x0002</span></span>
- <span data-ttu-id="e13a5-236">**UX_HID_KEYBOARD_STATE_SCROLL_LOCK** 0x0004</span><span class="sxs-lookup"><span data-stu-id="e13a5-236">**UX_HID_KEYBOARD_STATE_SCROLL_LOCK** 0x0004</span></span>
- <span data-ttu-id="e13a5-237">**UX_HID_KEYBOARD_STATE_MASK_LOCK** 0x0007</span><span class="sxs-lookup"><span data-stu-id="e13a5-237">**UX_HID_KEYBOARD_STATE_MASK_LOCK** 0x0007</span></span>
- <span data-ttu-id="e13a5-238">**UX_HID_KEYBOARD_STATE_LEFT_SHIFT** 0x0100</span><span class="sxs-lookup"><span data-stu-id="e13a5-238">**UX_HID_KEYBOARD_STATE_LEFT_SHIFT** 0x0100</span></span>
- <span data-ttu-id="e13a5-239">**UX_HID_KEYBOARD_STATE_RIGHT_SHIFT** 0x0200</span><span class="sxs-lookup"><span data-stu-id="e13a5-239">**UX_HID_KEYBOARD_STATE_RIGHT_SHIFT** 0x0200</span></span>
- <span data-ttu-id="e13a5-240">**UX_HID_KEYBOARD_STATE_SHIFT** 0x0300</span><span class="sxs-lookup"><span data-stu-id="e13a5-240">**UX_HID_KEYBOARD_STATE_SHIFT** 0x0300</span></span>
- <span data-ttu-id="e13a5-241">**UX_HID_KEYBOARD_STATE_LEFT_ALT** 0x0400</span><span class="sxs-lookup"><span data-stu-id="e13a5-241">**UX_HID_KEYBOARD_STATE_LEFT_ALT** 0x0400</span></span>
- <span data-ttu-id="e13a5-242">**UX_HID_KEYBOARD_STATE_RIGHT_ALT** 0x0800</span><span class="sxs-lookup"><span data-stu-id="e13a5-242">**UX_HID_KEYBOARD_STATE_RIGHT_ALT** 0x0800</span></span>
- <span data-ttu-id="e13a5-243">**UX_HID_KEYBOARD_STATE_ALT** 0x0A00</span><span class="sxs-lookup"><span data-stu-id="e13a5-243">**UX_HID_KEYBOARD_STATE_ALT** 0x0a00</span></span>
- <span data-ttu-id="e13a5-244">**UX_HID_KEYBOARD_STATE_LEFT_CTRL** 0x1000</span><span class="sxs-lookup"><span data-stu-id="e13a5-244">**UX_HID_KEYBOARD_STATE_LEFT_CTRL** 0x1000</span></span>
- <span data-ttu-id="e13a5-245">**UX_HID_KEYBOARD_STATE_RIGHT_CTRL** 0x2000</span><span class="sxs-lookup"><span data-stu-id="e13a5-245">**UX_HID_KEYBOARD_STATE_RIGHT_CTRL** 0x2000</span></span>
- <span data-ttu-id="e13a5-246">**UX_HID_KEYBOARD_STATE_CTRL** 0x3000</span><span class="sxs-lookup"><span data-stu-id="e13a5-246">**UX_HID_KEYBOARD_STATE_CTRL** 0x3000</span></span>
- <span data-ttu-id="e13a5-247">**UX_HID_KEYBOARD_STATE_LEFT_GUI** 0x4000</span><span class="sxs-lookup"><span data-stu-id="e13a5-247">**UX_HID_KEYBOARD_STATE_LEFT_GUI** 0x4000</span></span>
- <span data-ttu-id="e13a5-248">**UX_HID_KEYBOARD_STATE_RIGHT_GUI** 0x8000</span><span class="sxs-lookup"><span data-stu-id="e13a5-248">**UX_HID_KEYBOARD_STATE_RIGHT_GUI** 0x8000</span></span>
- <span data-ttu-id="e13a5-249">**UX_HID_KEYBOARD_STATE_GUI** 0xa000</span><span class="sxs-lookup"><span data-stu-id="e13a5-249">**UX_HID_KEYBOARD_STATE_GUI** 0xa000</span></span>

### <a name="example"></a><span data-ttu-id="e13a5-250">Örnek</span><span class="sxs-lookup"><span data-stu-id="e13a5-250">Example</span></span>

```c
while (1)
{

    /* Get a key/state from the keyboard. */
    status = ux_host_class_hid_keyboard_key_get(keyboard,
        &keyboard_char, &keyboard_state);

    /* Check if there is something. */
    if (status == UX_SUCCESS)
    {

        #ifdef UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE
            if (keyboard_state & UX_HID_KEYBOARD_STATE_KEY_UP)
            {
                /* The key was released. */
            } else
            {
                /* The key was pressed. */
            }
        #endif

        /* We have a character in the queue. */
        keyboard_queue[keyboard_queue_index] = (UCHAR) keyboard_char;

        /* Can we accept more ? */
        if(keyboard_queue_index < 1024)
            keyboard_queue_index++;
    }

    tx_thread_sleep(10);

}
```

## <a name="ux_host_class_hid_keyboard_ioctl"></a><span data-ttu-id="e13a5-251">ux_host_class_hid_keyboard_ioctl</span><span class="sxs-lookup"><span data-stu-id="e13a5-251">ux_host_class_hid_keyboard_ioctl</span></span>

<span data-ttu-id="e13a5-252">HID klavyesi için bir ıOCTL işlevi gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="e13a5-252">Perform an IOCTL function to the HID keyboard.</span></span>

### <a name="prototype"></a><span data-ttu-id="e13a5-253">Prototype</span><span class="sxs-lookup"><span data-stu-id="e13a5-253">Prototype</span></span>

```c
UINT ux_host_class_hid_keyboard_ioctl(
    UX_HOST_CLASS_HID_KEYBOARD *keyboard_instance,
    ULONG ioctl_function, VOID *parameter);
```

### <a name="description"></a><span data-ttu-id="e13a5-254">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e13a5-254">Description</span></span>

<span data-ttu-id="e13a5-255">Bu işlev, HID klavyesi için belirli bir IOCTL işlevi gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="e13a5-255">This function performs a specific ioctl function to the HID keyboard.</span></span> <span data-ttu-id="e13a5-256">Çağrı engelleniyor ve yalnızca bir hata olduğunda ya da komut tamamlandığında döndürülür.</span><span class="sxs-lookup"><span data-stu-id="e13a5-256">The call is blocking and only returns when there is either an error or when the command is completed.</span></span>

### <a name="parameters"></a><span data-ttu-id="e13a5-257">Parametreler</span><span class="sxs-lookup"><span data-stu-id="e13a5-257">Parameters</span></span>

- <span data-ttu-id="e13a5-258">**keyboard_instance** HID Klavye örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="e13a5-258">**keyboard_instance** Pointer to the HID keyboard instance.</span></span>
- <span data-ttu-id="e13a5-259">gerçekleştirilecek **ioctl_function** IOCTL işlevi.</span><span class="sxs-lookup"><span data-stu-id="e13a5-259">**ioctl_function** ioctl function to be performed.</span></span> <span data-ttu-id="e13a5-260">İzin verilen IOCTL işlevlerinden biri için aşağıdaki tabloya bakın.</span><span class="sxs-lookup"><span data-stu-id="e13a5-260">See table below for one of the allowed ioctl functions.</span></span>
- <span data-ttu-id="e13a5-261">**parametre** IOCTL 'ye özgü bir parametreye yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="e13a5-261">**parameter** Pointer to a parameter specific to the ioctl.</span></span>

### <a name="return-values"></a><span data-ttu-id="e13a5-262">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="e13a5-262">Return Values</span></span>

- <span data-ttu-id="e13a5-263">**UX_SUCCESS** (0x00) IOCTL işlevi başarıyla tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="e13a5-263">**UX_SUCCESS** (0x00) The ioctl function completed successfully.</span></span>
- <span data-ttu-id="e13a5-264">**UX_FUNCTION_NOT_SUPPORTED** (0x54) bilinmeyen IOCTL işlevi</span><span class="sxs-lookup"><span data-stu-id="e13a5-264">**UX_FUNCTION_NOT_SUPPORTED** (0x54) Unknown IOCTL function</span></span>

### <a name="ioctl-functions"></a><span data-ttu-id="e13a5-265">IOCTL işlevleri</span><span class="sxs-lookup"><span data-stu-id="e13a5-265">IOCTL functions</span></span>

- <span data-ttu-id="e13a5-266">UX_HID_KEYBOARD_IOCTL_SET_LAYOUT</span><span class="sxs-lookup"><span data-stu-id="e13a5-266">UX_HID_KEYBOARD_IOCTL_SET_LAYOUT</span></span>
- <span data-ttu-id="e13a5-267">UX_HID_KEYBOARD_IOCTL_KEY_DECODING_ENABLE</span><span class="sxs-lookup"><span data-stu-id="e13a5-267">UX_HID_KEYBOARD_IOCTL_KEY_DECODING_ENABLE</span></span>
- <span data-ttu-id="e13a5-268">UX_HID_KEYBOARD_IOCTL_KEY_DECODING_DISABLE</span><span class="sxs-lookup"><span data-stu-id="e13a5-268">UX_HID_KEYBOARD_IOCTL_KEY_DECODING_DISABLE</span></span>

### <a name="example--change-keyboard-layout"></a><span data-ttu-id="e13a5-269">Örnek – Klavye yerleşimini değiştirme</span><span class="sxs-lookup"><span data-stu-id="e13a5-269">Example – change keyboard layout</span></span>

```c
UINT status;

/* This example shows usage of the SET_LAYOUT IOCTL function.
    USBX receives raw key values from the device (these raw values
    are defined in the HID usage table specification) and optionally
    decodes them for application usage. The decoding is performed
    based on a set of arrays that act as maps – which array is used
    depends on the raw key value (i.e. keypad and non-keypad) and
    the current state of the keyboard (i.e. shift, caps lock, etc.). */

/* When the shift condition is not present and the raw key value
    is not within the keypad value range, this array will be used to decode the raw key value. */

static UCHAR keyboard_layout_raw_to_unshifted_map[] =
{
    0,0,0,0,
    'a','b','c','d','e','f','g',
    'h','i','j','k','l','m','n',
    'o','p','q','r','s','t',
    'u','v','w','x','y','z',
    '1','2','3','4','5','6','7','8','9','0',
    0x0d,0x1b,0x08,0x07,0x20,'-','=','[',']',
    '\\','#',';',0x27,'`',',','.','/',0xf0,
    0xbb,0xbc,0xbd,0xbe,0xbf,0xc0,0xc1,0xc2,0xc3,0xc4,0xc5,0xc6,
    0x00,0xf1,0x00,0xd2,0xc7,0xc9,0xd3,0xcf,0xd1,0xcd,0xcd,0xd0,0xc8,0xf2,
    '/','*','-','+',
    0x0d,'1','2','3','4','5','6','7','8','9','0','.','\\',0x00,0x00,'=',
    0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,
};

/* When the shift condition is present and the raw key value
    is not within the keypad value range, this array will be used to decode the raw key value. */

static UCHAR keyboard_layout_raw_to_shifted_map[] =
{
    0,0,0,0,
    'A','B','C','D','E','F','G',
    'H','I','J','K','L','M','N',
    'O','P','Q','R','S','T',
    'U','V','W','X','Y','Z',
    '!','@','#','$','%','^','&','*','(',')',
    0x0d,0x1b,0x08,0x07,0x20,'_','+','{','}',
    '|','~',':','"','~','<','>','?',0xf0,
    0xbb,0xbc,0xbd,0xbe,0xbf,0xc0,0xc1,0xc2,0xc3,0xc4,0xc5,0xc6,
    0x00,0xf1,0x00,0xd2,0xc7,0xc9,0xd3,0xcf,0xd1,0xcd,0xcd,0xd0,0xc8,0xf2,
    '/','*','-','+',
    0x0d,'1','2','3','4','5','6','7','8','9','0','.','\\',0x00,0x00,'=',
    0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,
};

/* When numlock is on and the raw key value is within the keypad
    value range, this array will be used to decode the raw key value. */

static UCHAR keyboard_layout_raw_to_numlock_on_map[] =
{
    '/','*','-','+',
    0x0d,'1','2','3','4','5','6','7','8','9','0','.','\\',0x00,0x00,'=',
};

/* When numlock is off and the raw key value is within the keypad value
    range, this array will be used to decode the raw key value. */
static UCHAR keyboard_layout_raw_to_numlock_off_map[] =
{
    '/','*','-','+',
    0x0d,0xcf,0xd0,0xd1,0xcb,'5',0xcd,0xc7,0xc8,0xc9,0xd2,0xd3,'\\',0x00,0x
    00,'=',
};

/* Specify the keyboard layout for USBX usage. */
static UX_HOST_CLASS_HID_KEYBOARD_LAYOUT keyboard_layout =
{
    keyboard_layout_raw_to_shifted_map,
    keyboard_layout_raw_to_unshifted_map,
    keyboard_layout_raw_to_numlock_on_map,
    keyboard_layout_raw_to_numlock_off_map,
    /* The maximum raw key value. Values larger than this are discarded. */
    UX_HID_KEYBOARD_KEYS_UPPER_RANGE,
    /* The raw key value for the letter 'a'. */
    UX_HID_KEYBOARD_KEY_LETTER_A,
    /* The raw key value for the letter 'z'. */
    UX_HID_KEYBOARD_KEY_LETTER_Z,
    /* The lower range raw key value for keypad keys - inclusive. */
    UX_HID_KEYBOARD_KEYS_KEYPAD_LOWER_RANGE,
    /* The upper range raw key value for keypad keys. */
    UX_HID_KEYBOARD_KEYS_KEYPAD_UPPER_RANGE
};

/* Call the IOCTL function to change the keyboard layout. */
status = ux_host_class_hid_keyboard_ioctl(keyboard,
    UX_HID_KEYBOARD_IOCTL_SET_LAYOUT, (VOID *)&keyboard_layout);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="example--disable-keyboard-key-decode"></a><span data-ttu-id="e13a5-270">Örnek – klavye anahtar kodunu çöz devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="e13a5-270">Example – disable keyboard key decode</span></span>

```c
UINT status;

/* The following example illustrates IOCTL function of Disable key decode from keyboard layout. */
status = ux_host_class_hid_keyboard_ioctl(keyboard,
    UX_HID_KEYBOARD_IOCTL_DISABLE_KEYS_DECODE, UX_NULL);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_hid_remote_control_usage_get"></a><span data-ttu-id="e13a5-271">ux_host_class_hid_remote_control_usage_get</span><span class="sxs-lookup"><span data-stu-id="e13a5-271">ux_host_class_hid_remote_control_usage_get</span></span>

<span data-ttu-id="e13a5-272">Uzaktan denetim kullanımı al</span><span class="sxs-lookup"><span data-stu-id="e13a5-272">Get remote control usage</span></span>

### <a name="prototype"></a><span data-ttu-id="e13a5-273">Prototype</span><span class="sxs-lookup"><span data-stu-id="e13a5-273">Prototype</span></span>

```c
UINT ux_host_class_hid_remote_control_usage_get(
    UX_HOST_CLASS_HID_REMOTE_CONTROL *remote_control_instance,
    LONG *usage, 
    ULONG *value);
```

### <a name="description"></a><span data-ttu-id="e13a5-274">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e13a5-274">Description</span></span>

<span data-ttu-id="e13a5-275">Bu işlev, uzaktan denetim kullanımlarını almak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e13a5-275">This function is used to get the remote control usages.</span></span>

### <a name="parameters"></a><span data-ttu-id="e13a5-276">Parametreler</span><span class="sxs-lookup"><span data-stu-id="e13a5-276">Parameters</span></span>

- <span data-ttu-id="e13a5-277">**remote_control_instance** HID uzaktan denetim örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="e13a5-277">**remote_control_instance** Pointer to the HID remote control instance.</span></span>
- <span data-ttu-id="e13a5-278">**kullanım** Kullanım işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="e13a5-278">**usage** Pointer to the usage.</span></span>
- <span data-ttu-id="e13a5-279">**değer** Kullanım için değer işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="e13a5-279">**value** Pointer to the value for the usage.</span></span>

### <a name="return-values"></a><span data-ttu-id="e13a5-280">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="e13a5-280">Return Values</span></span>

- <span data-ttu-id="e13a5-281">**UX_SUCCESS** (0x00) veri aktarımı tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="e13a5-281">**UX_SUCCESS** (0x00) The data transfer was completed.</span></span>
- <span data-ttu-id="e13a5-282">Raporlanacak hiçbir şey **UX_ERROR** (0xFF).</span><span class="sxs-lookup"><span data-stu-id="e13a5-282">**UX_ERROR** (0xff) Nothing to report.</span></span>
- <span data-ttu-id="e13a5-283">**UX_HOST_CLASS_INSTANCE_UNKNOWN** (0X5B) HID sınıfı örneği yok.</span><span class="sxs-lookup"><span data-stu-id="e13a5-283">**UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) HID class instance does not exist.</span></span>

<span data-ttu-id="e13a5-284">Olası tüm kullanımların listesi bu kullanıcı kılavuzuna sığamayacak kadar uzun.</span><span class="sxs-lookup"><span data-stu-id="e13a5-284">The list of all possible usages is too long to fit in this user guide.</span></span> <span data-ttu-id="e13a5-285">Tam bir açıklama için ux_host_class_hid. h tüm olası değerler kümesine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="e13a5-285">For a full description, the ux_host_class_hid.h has the entire set of possible values.</span></span>

### <a name="example"></a><span data-ttu-id="e13a5-286">Örnek</span><span class="sxs-lookup"><span data-stu-id="e13a5-286">Example</span></span>

```c
/* Read usages and values as the user changes the vol/bass/treble buttons on the speaker */

while (remote_control != UX_NULL)
{
    status = ux_host_class_hid_remote_control_usage_get(remote_control, &usage, &value);
    if (status == UX_SUCCESS)
    {
        /* We have something coming from the HID remote control,
        we filter the usage here and only allow the
        volume usage which can be VOLUME, VOLUME_INCREMENT or VOLUME_DECREMENT */
        switch(usage)
        {
            case UX_HOST_CLASS_HID_CONSUMER_VOLUME :
            case UX_HOST_CLASS_HID_CONSUMER_VOLUME_INCREMENT :
            case UX_HOST_CLASS_HID_CONSUMER_VOLUME_DECREMENT :

            if (value<0x80)
            {
                if (current_volume + audio_control.ux_host_class_audio_control_res < 0xffff)
                    current_volume = current_volume + audio_control.ux_host_class_audio_control_res;
                } else {
                if (current_volume > audio_control.ux_host_class_audio_control_res)
                    current_volume = current_volumeaudio_control.ux_host_class_audio_control_res;
            }

            audio_control.ux_host_class_audio_control_channel = 1;
            audio_control.ux_host_class_audio_control = UX_HOST_CLASS_AUDIO_VOLUME_CONTROL;
            audio_control.ux_host_class_audio_control_cur = current_volume;
            status = ux_host_class_audio_control_value_set(audio, &audio_control);
            audio_control.ux_host_class_audio_control_channel = 2;
            audio_control.ux_host_class_audio_control = UX_HOST_CLASS_AUDIO_VOLUME_CONTROL;
            audio_control.ux_host_class_audio_control_cur = current_volume;
            status = ux_host_class_audio_control_value_set(audio, &audio_control);
            break;

        }
    }
    tx_thread_sleep(10);

}
```

### <a name="ux_host_class_cdc_acm_read"></a><span data-ttu-id="e13a5-287">ux_host_class_cdc_acm_read</span><span class="sxs-lookup"><span data-stu-id="e13a5-287">ux_host_class_cdc_acm_read</span></span>

<span data-ttu-id="e13a5-288">Cdc_acm arabiriminden okuyun.</span><span class="sxs-lookup"><span data-stu-id="e13a5-288">Read from the cdc_acm interface.</span></span>

### <a name="prototype"></a><span data-ttu-id="e13a5-289">Prototype</span><span class="sxs-lookup"><span data-stu-id="e13a5-289">Prototype</span></span>

```c
UINT ux_host_class_cdc_acm_read(
    UX_HOST_CLASS_CDC_ACM *cdc_acm,
    UCHAR *data_pointer,
    ULONG requested_length,
    ULONG *actual_length);
```

### <a name="description"></a><span data-ttu-id="e13a5-290">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e13a5-290">Description</span></span>

<span data-ttu-id="e13a5-291">Bu işlev cdc_acm arabiriminden okur.</span><span class="sxs-lookup"><span data-stu-id="e13a5-291">This function reads from the cdc_acm interface.</span></span> <span data-ttu-id="e13a5-292">Çağrı engelleniyor ve yalnızca bir hata olduğunda ya da aktarım tamamlandığında döndürülür.</span><span class="sxs-lookup"><span data-stu-id="e13a5-292">The call is blocking and only returns when there is either an error or when the transfer is complete.</span></span>

### <a name="parameters"></a><span data-ttu-id="e13a5-293">Parametreler</span><span class="sxs-lookup"><span data-stu-id="e13a5-293">Parameters</span></span>

- <span data-ttu-id="e13a5-294">**cdc_acm** Cdc_acm sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="e13a5-294">**cdc_acm** Pointer to the cdc_acm class instance.</span></span>
- <span data-ttu-id="e13a5-295">**data_pointer** Veri yükünün arabellek adresine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="e13a5-295">**data_pointer** Pointer to the buffer address of the data payload.</span></span>
- <span data-ttu-id="e13a5-296">**requested_length** Alınacak uzunluk.</span><span class="sxs-lookup"><span data-stu-id="e13a5-296">**requested_length** Length to be received.</span></span>
- <span data-ttu-id="e13a5-297">**actual_length** Gerçekte alınan uzunluk.</span><span class="sxs-lookup"><span data-stu-id="e13a5-297">**actual_length** Length actually received.</span></span>

### <a name="return-values"></a><span data-ttu-id="e13a5-298">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="e13a5-298">Return Values</span></span>

- <span data-ttu-id="e13a5-299">**UX_SUCCESS** (0x00) veri aktarımı tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="e13a5-299">**UX_SUCCESS** (0x00) The data transfer was completed.</span></span>
- <span data-ttu-id="e13a5-300">**UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) cdc_acm örneği geçersiz.</span><span class="sxs-lookup"><span data-stu-id="e13a5-300">**UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) The cdc_acm instance is invalid.</span></span>
- <span data-ttu-id="e13a5-301">**UX_TRANSFER_TIMEOUT** (0x5c) aktarım zaman aşımı, okuma tamamlanmadı.</span><span class="sxs-lookup"><span data-stu-id="e13a5-301">**UX_TRANSFER_TIMEOUT** (0x5c) Transfer timeout, reading incomplete.</span></span>

### <a name="example"></a><span data-ttu-id="e13a5-302">Örnek</span><span class="sxs-lookup"><span data-stu-id="e13a5-302">Example</span></span>

```c
UINT status;

/* The following example illustrates this service. */

status = ux_host_class_cdc_acm_read(cdc_acm, data_pointer,
    requested_length, &actual_length);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_cdc_acm_write"></a><span data-ttu-id="e13a5-303">ux_host_class_cdc_acm_write</span><span class="sxs-lookup"><span data-stu-id="e13a5-303">ux_host_class_cdc_acm_write</span></span>

<span data-ttu-id="e13a5-304">Cdc_acm arabirimine yaz</span><span class="sxs-lookup"><span data-stu-id="e13a5-304">Write to the cdc_acm interface</span></span>

### <a name="prototype"></a><span data-ttu-id="e13a5-305">Prototype</span><span class="sxs-lookup"><span data-stu-id="e13a5-305">Prototype</span></span>

```c
UINT ux_host_class_cdc_acm_write(
    UX_HOST_CLASS_CDC_ACM *cdc_acm,
    UCHAR *data_pointer, 
    ULONG requested_length, 
    ULONG *actual_length);
```

### <a name="description"></a><span data-ttu-id="e13a5-306">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e13a5-306">Description</span></span>

<span data-ttu-id="e13a5-307">Bu işlev cdc_acm arabirimine yazar.</span><span class="sxs-lookup"><span data-stu-id="e13a5-307">This function writes to the cdc_acm interface.</span></span> <span data-ttu-id="e13a5-308">Çağrı engelleniyor ve yalnızca bir hata olduğunda ya da aktarım tamamlandığında döndürülür.</span><span class="sxs-lookup"><span data-stu-id="e13a5-308">The call is blocking and only returns when there is either an error or when the transfer is complete.</span></span>

### <a name="parameters"></a><span data-ttu-id="e13a5-309">Parametreler</span><span class="sxs-lookup"><span data-stu-id="e13a5-309">Parameters</span></span>

- <span data-ttu-id="e13a5-310">**cdc_acm** Cdc_acm sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="e13a5-310">**cdc_acm** Pointer to the cdc_acm class instance.</span></span>
- <span data-ttu-id="e13a5-311">**data_pointer** Veri yükünün arabellek adresine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="e13a5-311">**data_pointer** Pointer to the buffer address of the data payload.</span></span>
- <span data-ttu-id="e13a5-312">**requested_length** Gönderilecek uzunluk.</span><span class="sxs-lookup"><span data-stu-id="e13a5-312">**requested_length** Length to be sent.</span></span>
- <span data-ttu-id="e13a5-313">**actual_length** Gerçekte gönderilen uzunluk.</span><span class="sxs-lookup"><span data-stu-id="e13a5-313">**actual_length** Length actually sent.</span></span>

### <a name="return-values"></a><span data-ttu-id="e13a5-314">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="e13a5-314">Return Values</span></span>

- <span data-ttu-id="e13a5-315">**UX_SUCCESS** (0x00) veri aktarımı tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="e13a5-315">**UX_SUCCESS** (0x00) The data transfer was completed.</span></span>
- <span data-ttu-id="e13a5-316">**UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) cdc_acm örneği geçersiz.</span><span class="sxs-lookup"><span data-stu-id="e13a5-316">**UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) The cdc_acm instance is invalid.</span></span>
- <span data-ttu-id="e13a5-317">**UX_TRANSFER_TIMEOUT** (0x5c) aktarım zaman aşımı, yazma tamamlanmamış.</span><span class="sxs-lookup"><span data-stu-id="e13a5-317">**UX_TRANSFER_TIMEOUT** (0x5c) Transfer timeout, writing incomplete.</span></span>

### <a name="example"></a><span data-ttu-id="e13a5-318">Örnek</span><span class="sxs-lookup"><span data-stu-id="e13a5-318">Example</span></span>

```c
UINT status;

/* The following example illustrates this service. */

status = ux_host_class_cdc_acm_write(cdc_acm, data_pointer,
    requested_length, &actual_length);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_cdc_acm_ioctl"></a><span data-ttu-id="e13a5-319">ux_host_class_cdc_acm_ioctl</span><span class="sxs-lookup"><span data-stu-id="e13a5-319">ux_host_class_cdc_acm_ioctl</span></span>

<span data-ttu-id="e13a5-320">Cdc_acm arabirimine bir ıOCTL işlevi gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="e13a5-320">Perform an IOCTL function to the cdc_acm interface.</span></span>

### <a name="prototype"></a><span data-ttu-id="e13a5-321">Prototype</span><span class="sxs-lookup"><span data-stu-id="e13a5-321">Prototype</span></span>

```c
UINT ux_host_class_cdc_acm_ioctl(
    UX_HOST_CLASS_CDC_ACM *cdc_acm,
    ULONG ioctl_function, 
    VOID *parameter);
```

### <a name="description"></a><span data-ttu-id="e13a5-322">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e13a5-322">Description</span></span>

<span data-ttu-id="e13a5-323">Bu işlev cdc_acm arabirimine belirli bir IOCTL işlevi gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="e13a5-323">This function performs a specific ioctl function to the cdc_acm interface.</span></span> <span data-ttu-id="e13a5-324">Çağrı engelleniyor ve yalnızca bir hata olduğunda ya da komut tamamlandığında döndürülür.</span><span class="sxs-lookup"><span data-stu-id="e13a5-324">The call is blocking and only returns when there is either an error or when the command is completed.</span></span>

### <a name="parameters"></a><span data-ttu-id="e13a5-325">Parametreler</span><span class="sxs-lookup"><span data-stu-id="e13a5-325">Parameters</span></span>

- <span data-ttu-id="e13a5-326">**cdc_acm** Cdc_acm sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="e13a5-326">**cdc_acm** Pointer to the cdc_acm class instance.</span></span>
- <span data-ttu-id="e13a5-327">gerçekleştirilecek **ioctl_function** IOCTL işlevi.</span><span class="sxs-lookup"><span data-stu-id="e13a5-327">**ioctl_function** ioctl function to be performed.</span></span> <span data-ttu-id="e13a5-328">İzin verilen IOCTL işlevlerinden biri için aşağıdaki tabloya bakın.</span><span class="sxs-lookup"><span data-stu-id="e13a5-328">See table below for one of the allowed ioctl functions.</span></span>
- <span data-ttu-id="e13a5-329">**parametre** IOCTL 'ye özgü parametreye yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="e13a5-329">**parameter** Pointer to a parameter specific to the ioctl</span></span>

### <a name="return-value"></a><span data-ttu-id="e13a5-330">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="e13a5-330">Return Value</span></span>

- <span data-ttu-id="e13a5-331">**UX_SUCCESS** (0x00) veri aktarımı tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="e13a5-331">**UX_SUCCESS** (0x00) The data transfer was completed.</span></span>
- <span data-ttu-id="e13a5-332">**UX_MEMORY_INSUFFICIENT** (0x12) yeterli bellek yok.</span><span class="sxs-lookup"><span data-stu-id="e13a5-332">**UX_MEMORY_INSUFFICIENT** (0x12) Not enough memory.</span></span>
- <span data-ttu-id="e13a5-333">**UX_HOST_CLASS_INSTANCE_UNKNOWN** (0X5B) CDC-ACM örneği geçersiz bir durumda.</span><span class="sxs-lookup"><span data-stu-id="e13a5-333">**UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) CDC-ACM instance is in an invalid state.</span></span>
- <span data-ttu-id="e13a5-334">**UX_FUNCTION_NOT_SUPPORTED** (0x54) bilinmeyen IOCTL işlevi.</span><span class="sxs-lookup"><span data-stu-id="e13a5-334">**UX_FUNCTION_NOT_SUPPORTED** (0x54) Unknown IOCTL function.</span></span>

### <a name="ioctl-functions"></a><span data-ttu-id="e13a5-335">IOCTL işlevleri:</span><span class="sxs-lookup"><span data-stu-id="e13a5-335">IOCTL functions:</span></span>

- <span data-ttu-id="e13a5-336">UX_HOST_CLASS_CDC_ACM_IOCTL_SET_LINE_CODING</span><span class="sxs-lookup"><span data-stu-id="e13a5-336">UX_HOST_CLASS_CDC_ACM_IOCTL_SET_LINE_CODING</span></span>
- <span data-ttu-id="e13a5-337">UX_HOST_CLASS_CDC_ACM_IOCTL_GET_LINE_CODING</span><span class="sxs-lookup"><span data-stu-id="e13a5-337">UX_HOST_CLASS_CDC_ACM_IOCTL_GET_LINE_CODING</span></span>
- <span data-ttu-id="e13a5-338">UX_HOST_CLASS_CDC_ACM_IOCTL_SET_LINE_STATE</span><span class="sxs-lookup"><span data-stu-id="e13a5-338">UX_HOST_CLASS_CDC_ACM_IOCTL_SET_LINE_STATE</span></span>
- <span data-ttu-id="e13a5-339">UX_HOST_CLASS_CDC_ACM_IOCTL_SEND_BREAK</span><span class="sxs-lookup"><span data-stu-id="e13a5-339">UX_HOST_CLASS_CDC_ACM_IOCTL_SEND_BREAK</span></span>
- <span data-ttu-id="e13a5-340">UX_HOST_CLASS_CDC_ACM_IOCTL_ABORT_IN_PIPE</span><span class="sxs-lookup"><span data-stu-id="e13a5-340">UX_HOST_CLASS_CDC_ACM_IOCTL_ABORT_IN_PIPE</span></span>
- <span data-ttu-id="e13a5-341">UX_HOST_CLASS_CDC_ACM_IOCTL_ABORT_OUT_PIPE</span><span class="sxs-lookup"><span data-stu-id="e13a5-341">UX_HOST_CLASS_CDC_ACM_IOCTL_ABORT_OUT_PIPE</span></span>
- <span data-ttu-id="e13a5-342">UX_HOST_CLASS_CDC_ACM_IOCTL_NOTIFICATION_CALLBACK</span><span class="sxs-lookup"><span data-stu-id="e13a5-342">UX_HOST_CLASS_CDC_ACM_IOCTL_NOTIFICATION_CALLBACK</span></span>
- <span data-ttu-id="e13a5-343">UX_HOST_CLASS_CDC_ACM_IOCTL_GET_DEVICE_STATUS</span><span class="sxs-lookup"><span data-stu-id="e13a5-343">UX_HOST_CLASS_CDC_ACM_IOCTL_GET_DEVICE_STATUS</span></span>

```c
UINT status;

/* The following example illustrates this service. */

status = ux_host_class_cdc_acm_ioctl(cdc_acm,
    UX_HOST_CLASS_CDC_ACM_IOCTL_GET_LINE_CODING, (VOID *)&line_coding);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_cdc_acm_reception_start"></a><span data-ttu-id="e13a5-344">ux_host_class_cdc_acm_reception_start</span><span class="sxs-lookup"><span data-stu-id="e13a5-344">ux_host_class_cdc_acm_reception_start</span></span>

<span data-ttu-id="e13a5-345">Cihazdan verilerin arka planda alınması başladı.</span><span class="sxs-lookup"><span data-stu-id="e13a5-345">Begins background reception of data from the device.</span></span>

### <a name="prototype"></a><span data-ttu-id="e13a5-346">Prototype</span><span class="sxs-lookup"><span data-stu-id="e13a5-346">Prototype</span></span>

```c
UINT ux_host_class_cdc_acm_reception_start(
    UX_HOST_CLASS_CDC_ACM *cdc_acm,
    UX_HOST_CLASS_CDC_ACM_RECEPTION *cdc_acm_reception);
```

### <a name="description"></a><span data-ttu-id="e13a5-347">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e13a5-347">Description</span></span>

<span data-ttu-id="e13a5-348">Bu işlev, USBX 'in arka planda Cihazdaki verileri sürekli okuyamasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="e13a5-348">This function causes USBX to continuously read data from the device in the background.</span></span> <span data-ttu-id="e13a5-349">Her bir işlemin tamamlanmasından sonra, **cdc_acm_reception** ' de belirtilen geri çağırma çağrılır, böylece uygulama işlemin verilerinin daha fazla işlenmesini gerçekleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="e13a5-349">Upon completion of each transaction, the callback specified in **cdc_acm_reception** is invoked so the application may perform further processing of the transaction's data.</span></span>

> [!NOTE]
> <span data-ttu-id="e13a5-350">**ux_host_class_cdc_acm_read** , arka plan alımı kullanımda iken kullanılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="e13a5-350">**ux_host_class_cdc_acm_read** must not be used while background reception is in use.</span></span>

### <a name="parameters"></a><span data-ttu-id="e13a5-351">Parametreler</span><span class="sxs-lookup"><span data-stu-id="e13a5-351">Parameters</span></span>

- <span data-ttu-id="e13a5-352">**cdc_acm** Cdc_acm sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="e13a5-352">**cdc_acm** Pointer to the cdc_acm class instance.</span></span>
- <span data-ttu-id="e13a5-353">**cdc_acm_reception** Arka plan Alım davranışını tanımlayan değerleri içeren parametreye yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="e13a5-353">**cdc_acm_reception** Pointer to parameter that contains values defining behavior of background reception.</span></span> <span data-ttu-id="e13a5-354">Bu parametrenin düzeni aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="e13a5-354">The layout of this parameter follows:</span></span>

```c
typedef struct UX_HOST_CLASS_CDC_ACM_RECEPTION_STRUCT
{
    ULONG ux_host_class_cdc_acm_reception_state;
    ULONG ux_host_class_cdc_acm_reception_block_size;
    UCHAR *ux_host_class_cdc_acm_reception_data_buffer;
    ULONG ux_host_class_cdc_acm_reception_data_buffer_size;
    UCHAR *ux_host_class_cdc_acm_reception_data_head;
    UCHAR *ux_host_class_cdc_acm_reception_data_tail;
    VOID (*ux_host_class_cdc_acm_reception_callback)(struct UX_HOST_CLASS_CDC_ACM_STRUCT *cdc_acm,
        UINT status, UCHAR *reception_buffer, ULONG reception_size);
} UX_HOST_CLASS_CDC_ACM_RECEPTION;
```

### <a name="return-value"></a><span data-ttu-id="e13a5-355">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="e13a5-355">Return Value</span></span>

- <span data-ttu-id="e13a5-356">**UX_SUCCESS** (0x00) arka plan alımı başarıyla başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="e13a5-356">**UX_SUCCESS** (0x00) Background reception successfully started.</span></span>
- <span data-ttu-id="e13a5-357">**UX_HOST_CLASS_INSTANCE _UNKNOWN** (0x5b) yanlış sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="e13a5-357">**UX_HOST_CLASS_INSTANCE _UNKNOWN** (0x5b) Wrong class instance.</span></span>

```c
UINT status;
UX_HOST_CLASS_CDC_ACM_RECEPTION cdc_acm_reception;

/* Setup the background reception parameter. */

/* Set the desired max read size for each transaction.
    For example, if this value is 64, then the maximum amount of
    data received from the device in a single transaction is 64.
    If the amount of data received from the device is less than this value,
    the callback will still be invoked with the actual amount of data received. */
cdc_acm_reception.ux_host_class_cdc_acm_reception_block_size = block_size;

/* Set the buffer where the data from the device is read to. */
cdc_acm_reception.ux_host_class_cdc_acm_reception_data_buffer = cdc_acm_reception_buffer;

/* Set the size of the data reception buffer.
    Note that this should be at least as large as ux_host_class_cdc_acm_reception_block_size. */
cdc_acm_reception.ux_host_class_cdc_acm_reception_data_buffer_size = cdc_acm_reception_buffer_size;

/* Set the callback that is to be invoked upon each reception transfer completion. */
cdc_acm_reception.ux_host_class_cdc_acm_reception_callback = reception_callback;

/* Start background reception using the values we defined in the reception parameter. */
status = ux_host_class_cdc_acm_reception_start(cdc_acm_host_data, &cdc_acm_reception);

/* If status equals UX_SUCCESS, background reception has successfully started. */
```

## <a name="ux_host_class_cdc_acm_reception_stop"></a><span data-ttu-id="e13a5-358">ux_host_class_cdc_acm_reception_stop</span><span class="sxs-lookup"><span data-stu-id="e13a5-358">ux_host_class_cdc_acm_reception_stop</span></span>

<span data-ttu-id="e13a5-359">Paketlerin arka planda alımına yanıt vermez.</span><span class="sxs-lookup"><span data-stu-id="e13a5-359">Stops background reception of packets.</span></span>

### <a name="prototype"></a><span data-ttu-id="e13a5-360">Prototype</span><span class="sxs-lookup"><span data-stu-id="e13a5-360">Prototype</span></span>

```c
UINT ux_host_class_cdc_acm_reception_stop(
    UX_HOST_CLASS_CDC_ACM *cdc_acm,
    UX_HOST_CLASS_CDC_ACM_RECEPTION *cdc_acm_reception);
```

### <a name="description"></a><span data-ttu-id="e13a5-361">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e13a5-361">Description</span></span>

<span data-ttu-id="e13a5-362">Bu işlev, USBX 'in daha önce **ux_host_class_cdc_acm_reception_start** tarafından başlatılan arka plan alımını durdurmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="e13a5-362">This function causes USBX to stop background reception previously started by **ux_host_class_cdc_acm_reception_start**.</span></span>

### <a name="parameters"></a><span data-ttu-id="e13a5-363">Parametreler</span><span class="sxs-lookup"><span data-stu-id="e13a5-363">Parameters</span></span>

- <span data-ttu-id="e13a5-364">**cdc_acm** Cdc_acm sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="e13a5-364">**cdc_acm** Pointer to the cdc_acm class instance.</span></span>
- <span data-ttu-id="e13a5-365">**cdc_acm_reception** Arka plan alımı başlatmak için kullanılan aynı parametreye yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="e13a5-365">**cdc_acm_reception** Pointer to the same parameter that was used to start background reception.</span></span> <span data-ttu-id="e13a5-366">Bu parametrenin düzeni aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="e13a5-366">The layout of this parameter follows:</span></span>

```c
typedef struct UX_HOST_CLASS_CDC_ACM_RECEPTION_STRUCT
{
    ULONG ux_host_class_cdc_acm_reception_state;
    ULONG ux_host_class_cdc_acm_reception_block_size;
    UCHAR *ux_host_class_cdc_acm_reception_data_buffer;
    ULONG ux_host_class_cdc_acm_reception_data_buffer_size;
    UCHAR *ux_host_class_cdc_acm_reception_data_head;
    UCHAR *ux_host_class_cdc_acm_reception_data_tail;
    VOID (*ux_host_class_cdc_acm_reception_callback)(
            struct UX_HOST_CLASS_CDC_ACM_STRUCT *cdc_acm, UINT status,
            UCHAR *reception_buffer, ULONG reception_size);
} UX_HOST_CLASS_CDC_ACM_RECEPTION;
```

### <a name="return-value"></a><span data-ttu-id="e13a5-367">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="e13a5-367">Return Value</span></span>

- <span data-ttu-id="e13a5-368">**UX_SUCCESS** (0x00) arka plan alımı başarıyla durduruldu.</span><span class="sxs-lookup"><span data-stu-id="e13a5-368">**UX_SUCCESS** (0x00) Background reception successfully stopped.</span></span>
- <span data-ttu-id="e13a5-369">**UX_HOST_CLASS_INSTANCE _UNKNOWN** (0x5b) yanlış sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="e13a5-369">**UX_HOST_CLASS_INSTANCE _UNKNOWN** (0x5b) Wrong class instance.</span></span>

```c
UINT status;
UX_HOST_CLASS_CDC_ACM_RECEPTION cdc_acm_reception;

/* Stop background reception. The reception parameter should be the same
    that was passed to ux_host_class_cdc_acm_reception_start. */
status = ux_host_class_cdc_acm_reception_stop(cdc_acm, &cdc_acm_reception);

/* If status equals UX_SUCCESS, background reception has successfully stopped. */
```
