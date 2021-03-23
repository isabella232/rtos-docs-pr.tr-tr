---
title: Bölüm 4-USBX cihaz hizmetlerinin açıklaması
description: USBX cihaz hizmetleri hakkında bilgi edinin.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: d4aea7470ba2d9075296164b9d1fb61db4f88523
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104828138"
---
# <a name="description-of-usbx-device-services"></a><span data-ttu-id="6b186-103">USBX cihaz hizmetlerinin açıklaması</span><span class="sxs-lookup"><span data-stu-id="6b186-103">Description of USBX Device Services</span></span>

### <a name="ux_device_stack_alternate_setting_get"></a><span data-ttu-id="6b186-104">ux_device_stack_alternate_setting_get</span><span class="sxs-lookup"><span data-stu-id="6b186-104">ux_device_stack_alternate_setting_get</span></span>

<span data-ttu-id="6b186-105">Bir arabirim değeri için geçerli alternatif ayarı al</span><span class="sxs-lookup"><span data-stu-id="6b186-105">Get current alternate setting for an interface value</span></span>

### <a name="prototype"></a><span data-ttu-id="6b186-106">Prototype</span><span class="sxs-lookup"><span data-stu-id="6b186-106">Prototype</span></span>

```c
UINT ux_device_stack_alternate_setting_get(ULONG interface_value);
```

### <a name="description"></a><span data-ttu-id="6b186-107">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6b186-107">Description</span></span>

<span data-ttu-id="6b186-108">Bu işlev, USB ana bilgisayarı tarafından belirli bir arabirim değeri için geçerli alternatif ayarı elde etmek üzere kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6b186-108">This function is used by the USB host to obtain the current alternate setting for a specific interface value.</span></span> <span data-ttu-id="6b186-109">Bir **GET_INTERFACE** isteği alındığında denetleyici sürücü tarafından çağrılır.</span><span class="sxs-lookup"><span data-stu-id="6b186-109">It is called by the controller driver when a **GET_INTERFACE** request is received.</span></span>

### <a name="input-parameter"></a><span data-ttu-id="6b186-110">Giriş parametresi</span><span class="sxs-lookup"><span data-stu-id="6b186-110">Input Parameter</span></span>

- <span data-ttu-id="6b186-111">**Interface_value** Geçerli alternatif ayarın sorgulandığı arabirim değeri</span><span class="sxs-lookup"><span data-stu-id="6b186-111">**Interface_value** Interface value for which the current alternate setting is queried</span></span>

### <a name="return-values"></a><span data-ttu-id="6b186-112">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="6b186-112">Return Values</span></span>

- <span data-ttu-id="6b186-113">**UX_SUCCESS** (0x00) veri aktarımı tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="6b186-113">**UX_SUCCESS** (0x00) The data transfer was completed.</span></span>
- <span data-ttu-id="6b186-114">**UX_ERROR** (0xFF) yanlış arabirim değeri.</span><span class="sxs-lookup"><span data-stu-id="6b186-114">**UX_ERROR** (0xFF) Wrong interface value.</span></span>

### <a name="example"></a><span data-ttu-id="6b186-115">Örnek</span><span class="sxs-lookup"><span data-stu-id="6b186-115">Example</span></span>

```c
ULONG interface_value;
UINT status;

/* The following example illustrates this service. */
status = ux_device_stack_alternate_setting_get(interface_value);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_alternate_setting_set"></a><span data-ttu-id="6b186-116">ux_device_stack_alternate_setting_set</span><span class="sxs-lookup"><span data-stu-id="6b186-116">ux_device_stack_alternate_setting_set</span></span>

<span data-ttu-id="6b186-117">Bir arabirim değeri için geçerli alternatif ayarı ayarla</span><span class="sxs-lookup"><span data-stu-id="6b186-117">Set current alternate setting for an interface value</span></span>

### <a name="prototype"></a><span data-ttu-id="6b186-118">Prototype</span><span class="sxs-lookup"><span data-stu-id="6b186-118">Prototype</span></span>

```c
UINT ux_device_stack_alternate_setting_set(
    ULONG interface_value, 
    ULONG alternate_setting_value);
```

### <a name="description"></a><span data-ttu-id="6b186-119">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6b186-119">Description</span></span>

<span data-ttu-id="6b186-120">Bu işlev, USB ana bilgisayarı tarafından belirli bir arabirim değeri için geçerli alternatif ayarı ayarlamak üzere kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6b186-120">This function is used by the USB host to set the current alternate setting for a specific interface value.</span></span> <span data-ttu-id="6b186-121">Bir **SET_INTERFACE** isteği alındığında denetleyici sürücü tarafından çağrılır.</span><span class="sxs-lookup"><span data-stu-id="6b186-121">It is called by the controller driver when a **SET_INTERFACE** request is received.</span></span> <span data-ttu-id="6b186-122">**SET_INTERFACE** tamamlandığında, alternatif ayarların değerleri sınıfa uygulanır.</span><span class="sxs-lookup"><span data-stu-id="6b186-122">When the **SET_INTERFACE** is completed, the values of the alternate settings are applied to the class.</span></span>

<span data-ttu-id="6b186-123">Cihaz yığını, alternatif ayarın değiştirilmesini yansıtmak için bu arabirime sahip olan sınıfa bir **UX_SLAVE_CLASS_COMMAND_CHANGE** yayımlayacak.</span><span class="sxs-lookup"><span data-stu-id="6b186-123">The device stack will issue a **UX_SLAVE_CLASS_COMMAND_CHANGE** to the class that owns this interface to reflect the change of alternate setting.</span></span>

### <a name="parameters"></a><span data-ttu-id="6b186-124">Parametreler</span><span class="sxs-lookup"><span data-stu-id="6b186-124">Parameters</span></span>

- <span data-ttu-id="6b186-125">**interface_value**: geçerli alternatif ayarın ayarlandığı arabirim değeri.</span><span class="sxs-lookup"><span data-stu-id="6b186-125">**interface_value**: Interface value for which the current alternate setting is set.</span></span>
- <span data-ttu-id="6b186-126">**alternate_setting_value**: yeni alternatif ayar değeri.</span><span class="sxs-lookup"><span data-stu-id="6b186-126">**alternate_setting_value**: The new alternate setting value.</span></span>

### <a name="return-values"></a><span data-ttu-id="6b186-127">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="6b186-127">Return Values</span></span>

- <span data-ttu-id="6b186-128">**UX_SUCCESS** (0x00) veri aktarımı tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="6b186-128">**UX_SUCCESS** (0x00) The data transfer was completed.</span></span>
- <span data-ttu-id="6b186-129">**UX_INTERFACE_HANDLE_UNKNOWN** (0x52) hiç arabirim eklenmedi.</span><span class="sxs-lookup"><span data-stu-id="6b186-129">**UX_INTERFACE_HANDLE_UNKNOWN** (0x52) No interface attached.</span></span>
- <span data-ttu-id="6b186-130">**UX_FUNCTION_NOT_SUPPORTED** (0x54) cihaz yapılandırılmadı.</span><span class="sxs-lookup"><span data-stu-id="6b186-130">**UX_FUNCTION_NOT_SUPPORTED** (0x54) Device is not configured.</span></span>
- <span data-ttu-id="6b186-131">**UX_ERROR** (0xFF) yanlış arabirim değeri.</span><span class="sxs-lookup"><span data-stu-id="6b186-131">**UX_ERROR** (0xFF) Wrong interface value.</span></span>

### <a name="example"></a><span data-ttu-id="6b186-132">Örnek</span><span class="sxs-lookup"><span data-stu-id="6b186-132">Example</span></span>

```c
ULONG interface_value;

ULONG alternate_setting_value;

/* The following example illustrates this service. */
status = ux_device_stack_alternate_setting_set(interface_value, alternate_setting_value);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_class_register"></a><span data-ttu-id="6b186-133">ux_device_stack_class_register</span><span class="sxs-lookup"><span data-stu-id="6b186-133">ux_device_stack_class_register</span></span>

<span data-ttu-id="6b186-134">Yeni bir USB cihaz sınıfı Kaydet</span><span class="sxs-lookup"><span data-stu-id="6b186-134">Register a new USB device class</span></span>

### <a name="prototype"></a><span data-ttu-id="6b186-135">Prototype</span><span class="sxs-lookup"><span data-stu-id="6b186-135">Prototype</span></span>

```c
UINT ux_device_stack_class_register(
    UCHAR *class_name,
    UINT (*class_entry_function)(struct UX_SLAVE_CLASS_COMMAND_STRUCT *),
    ULONG configuration_number, 
    ULONG interface_number,  
    VOID *parameter);
```

### <a name="description"></a><span data-ttu-id="6b186-136">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6b186-136">Description</span></span>

<span data-ttu-id="6b186-137">Bu işlev, uygulama tarafından yeni bir USB cihaz sınıfı kaydetmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6b186-137">This function is used by the application to register a new USB device class.</span></span> <span data-ttu-id="6b186-138">Bu kayıt, sınıfının bir örneğini değil, bir sınıf kapsayıcısını başlatır.</span><span class="sxs-lookup"><span data-stu-id="6b186-138">This registration starts a class container and not an instance of the class.</span></span> <span data-ttu-id="6b186-139">Bir sınıf etkin bir iş parçacığına sahip olmalı ve belirli bir arabirime eklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="6b186-139">A class should have an active thread and be attached to a specific interface.</span></span>

<span data-ttu-id="6b186-140">Bazı sınıflar bir parametre veya parametre listesi bekler.</span><span class="sxs-lookup"><span data-stu-id="6b186-140">Some classes expect a parameter or parameter list.</span></span> <span data-ttu-id="6b186-141">Örneğin, cihaz depolama sınıfı, öykünmeye çalıştığı depolama cihazının geometrisini bekler.</span><span class="sxs-lookup"><span data-stu-id="6b186-141">For instance, the device storage class would expect the geometry of the storage device it is trying to emulate.</span></span> <span data-ttu-id="6b186-142">Bu nedenle parametre alanı, sınıf gereksinimine bağımlıdır ve sınıf değerleriyle doldurulmuş bir yapı için bir değer veya işaretçi olabilir.</span><span class="sxs-lookup"><span data-stu-id="6b186-142">The parameter field is therefore dependent on the class requirement and can be a value or a pointer to a structure filled with the class values.</span></span>

> [!NOTE]
> <span data-ttu-id="6b186-143">Class_name C dizesi NULL ile sonlandırılmış olmalı ve bunun uzunluğu (NULL-Sonlandırıcı kendisi olmadan) **UX_MAX_CLASS_NAME_LENGTH** daha büyük olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="6b186-143">The C string of class_name must be NULL-terminated and the length of it (without the NULL-terminator itself) must be no larger than **UX_MAX_CLASS_NAME_LENGTH**.</span></span>

### <a name="parameters"></a><span data-ttu-id="6b186-144">Parametreler</span><span class="sxs-lookup"><span data-stu-id="6b186-144">Parameters</span></span>

- <span data-ttu-id="6b186-145">**class_name** Sınıf adı</span><span class="sxs-lookup"><span data-stu-id="6b186-145">**class_name** Class Name</span></span>
- <span data-ttu-id="6b186-146">**class_entry_function** Sınıfın giriş işlevi.</span><span class="sxs-lookup"><span data-stu-id="6b186-146">**class_entry_function** The entry function of the class.</span></span>
- <span data-ttu-id="6b186-147">**configuration_number** Bu sınıfın iliştirildiği yapılandırma numarası.</span><span class="sxs-lookup"><span data-stu-id="6b186-147">**configuration_number** The configuration number this class is attached to.</span></span>
- <span data-ttu-id="6b186-148">**interface_number** Bu sınıfın iliştirildiği arabirim numarası.</span><span class="sxs-lookup"><span data-stu-id="6b186-148">**interface_number** The interface number this class is attached to.</span></span>
- <span data-ttu-id="6b186-149">**parametre** Sınıfa özgü bir parametre listesi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="6b186-149">**parameter** A pointer to a class specific parameter list.</span></span>

### <a name="return-values"></a><span data-ttu-id="6b186-150">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="6b186-150">Return Values</span></span>

- <span data-ttu-id="6b186-151">**UX_SUCCESS** (0x00) sınıf kaydettirildi</span><span class="sxs-lookup"><span data-stu-id="6b186-151">**UX_SUCCESS** (0x00) The class was registered</span></span>
- <span data-ttu-id="6b186-152">**UX_MEMORY_INSUFFICIENT** (0x12) sınıf tablosunda hiçbir giriş kalmadı.</span><span class="sxs-lookup"><span data-stu-id="6b186-152">**UX_MEMORY_INSUFFICIENT** (0x12) No entries left in class table.</span></span>
- <span data-ttu-id="6b186-153">**UX_THREAD_ERROR** (0x16) bir sınıf iş parçacığı oluşturamaz.</span><span class="sxs-lookup"><span data-stu-id="6b186-153">**UX_THREAD_ERROR** (0x16) Cannot create a class thread.</span></span>

### <a name="example"></a><span data-ttu-id="6b186-154">Örnek</span><span class="sxs-lookup"><span data-stu-id="6b186-154">Example</span></span>

```c
UINT status;

/* The following example illustrates this service. */

/* Initialize the device storage class. The class is connected with interface 1 */
status = ux_device_stack_class_register(_ux_system_slave_class_storage_name ux_device_class_storage_entry,
    1, 1, (VOID *)&parameter);
```

### <a name="ux_device_stack_class_unregister"></a><span data-ttu-id="6b186-155">ux_device_stack_class_unregister</span><span class="sxs-lookup"><span data-stu-id="6b186-155">ux_device_stack_class_unregister</span></span>

<span data-ttu-id="6b186-156">USB cihaz sınıfının kaydını silme</span><span class="sxs-lookup"><span data-stu-id="6b186-156">Unregister a USB device class</span></span>

### <a name="prototype"></a><span data-ttu-id="6b186-157">Prototype</span><span class="sxs-lookup"><span data-stu-id="6b186-157">Prototype</span></span>

```c
UINT ux_device_stack_class_unregister(
    UCHAR *class_name,
    UINT (*class_entry_function)(struct UX_SLAVE_CLASS_COMMAND_STRUCT*));
```

### <a name="description"></a><span data-ttu-id="6b186-158">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6b186-158">Description</span></span>

<span data-ttu-id="6b186-159">Bu işlev, uygulama tarafından USB cihaz sınıfının kaydını silmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6b186-159">This function is used by the application to unregister a USB device class.</span></span>

> [!NOTE]
> <span data-ttu-id="6b186-160">Class_name C dizesi NULL ile sonlandırılmış olmalı ve bunun uzunluğu (NULL-Sonlandırıcı kendisi olmadan) **UX_MAX_CLASS_NAME_LENGTH** daha büyük olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="6b186-160">The C string of class_name must be NULL-terminated and the length of it (without the NULL-terminator itself) must be no larger than **UX_MAX_CLASS_NAME_LENGTH**.</span></span>

### <a name="parameters"></a><span data-ttu-id="6b186-161">Parametreler</span><span class="sxs-lookup"><span data-stu-id="6b186-161">Parameters</span></span>

- <span data-ttu-id="6b186-162">**class_name**: sınıf adı</span><span class="sxs-lookup"><span data-stu-id="6b186-162">**class_name**: Class Name</span></span>
- <span data-ttu-id="6b186-163">**class_entry_function**: sınıfının giriş işlevi.</span><span class="sxs-lookup"><span data-stu-id="6b186-163">**class_entry_function**: The entry function of the class.</span></span>

### <a name="return-values"></a><span data-ttu-id="6b186-164">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="6b186-164">Return Values</span></span>

- <span data-ttu-id="6b186-165">**UX_SUCCESS** (0x00) sınıfın kaydı silindi.</span><span class="sxs-lookup"><span data-stu-id="6b186-165">**UX_SUCCESS** (0x00) The class was unregistered.</span></span>
- <span data-ttu-id="6b186-166">**UX_NO_CLASS_MATCH** (0x57) Sınıf kayıtlı değil.</span><span class="sxs-lookup"><span data-stu-id="6b186-166">**UX_NO_CLASS_MATCH** (0x57) The class isn't registered.</span></span>

### <a name="example"></a><span data-ttu-id="6b186-167">Örnek</span><span class="sxs-lookup"><span data-stu-id="6b186-167">Example</span></span>

```c
/* The following example illustrates this service. */

/* Unitialize the device storage class. */
status = ux_device_stack_class_unregister(_ux_system_slave_class_storage_name, ux_device_class_storage_entry);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_configuration_get"></a><span data-ttu-id="6b186-168">ux_device_stack_configuration_get</span><span class="sxs-lookup"><span data-stu-id="6b186-168">ux_device_stack_configuration_get</span></span>

<span data-ttu-id="6b186-169">Geçerli yapılandırmayı al</span><span class="sxs-lookup"><span data-stu-id="6b186-169">Get the current configuration</span></span>

### <a name="prototype"></a><span data-ttu-id="6b186-170">Prototype</span><span class="sxs-lookup"><span data-stu-id="6b186-170">Prototype</span></span>

```c
UINT ux_device_stack_configuration_get(VOID);
```

### <a name="description"></a><span data-ttu-id="6b186-171">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6b186-171">Description</span></span>

<span data-ttu-id="6b186-172">Bu işlev, ana bilgisayar tarafından cihazda çalışan geçerli yapılandırmayı almak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6b186-172">This function is used by the host to obtain the current configuration running in the device.</span></span>

### <a name="input-parameter"></a><span data-ttu-id="6b186-173">Giriş parametresi</span><span class="sxs-lookup"><span data-stu-id="6b186-173">Input Parameter</span></span>

<span data-ttu-id="6b186-174">Yok</span><span class="sxs-lookup"><span data-stu-id="6b186-174">None</span></span>

### <a name="return-value"></a><span data-ttu-id="6b186-175">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="6b186-175">Return Value</span></span>

- <span data-ttu-id="6b186-176">**UX_SUCCESS** (0x00) veri aktarımı tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="6b186-176">**UX_SUCCESS** (0x00) The data transfer was completed.</span></span>

### <a name="example"></a><span data-ttu-id="6b186-177">Örnek</span><span class="sxs-lookup"><span data-stu-id="6b186-177">Example</span></span>

```c
UINT status;

/* The following example illustrates this service. */
status = ux_device_stack_configuration_get();

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_configuration_set"></a><span data-ttu-id="6b186-178">ux_device_stack_configuration_set</span><span class="sxs-lookup"><span data-stu-id="6b186-178">ux_device_stack_configuration_set</span></span>

<span data-ttu-id="6b186-179">Geçerli yapılandırmayı ayarla</span><span class="sxs-lookup"><span data-stu-id="6b186-179">Set the current configuration</span></span>

### <a name="prototype"></a><span data-ttu-id="6b186-180">Prototype</span><span class="sxs-lookup"><span data-stu-id="6b186-180">Prototype</span></span>

```c
UINT ux_device_stack_configuration_set(ULONG configuration_value);
```

### <a name="description"></a><span data-ttu-id="6b186-181">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6b186-181">Description</span></span>

<span data-ttu-id="6b186-182">Bu işlev, ana bilgisayar tarafından cihazda çalışan geçerli yapılandırmayı ayarlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6b186-182">This function is used by the host to set the current configuration running in the device.</span></span> <span data-ttu-id="6b186-183">Bu komutun alınması sırasında, USB cihaz yığını bu yapılandırmaya bağlı her arabirimin 0 alternatif ayarını etkinleştireceğiz.</span><span class="sxs-lookup"><span data-stu-id="6b186-183">Upon reception of this command, the USB device stack will activate the alternate setting 0 of each interface connected to this configuration.</span></span>

### <a name="input-parameter"></a><span data-ttu-id="6b186-184">Giriş parametresi</span><span class="sxs-lookup"><span data-stu-id="6b186-184">Input Parameter</span></span>

- <span data-ttu-id="6b186-185">**configuration_value** Konak tarafından seçilen yapılandırma değeri.</span><span class="sxs-lookup"><span data-stu-id="6b186-185">**configuration_value** The configuration value selected by the host.</span></span>

### <a name="return-value"></a><span data-ttu-id="6b186-186">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="6b186-186">Return Value</span></span>

- <span data-ttu-id="6b186-187">**UX_SUCCESS** (0x00) yapılandırma başarıyla ayarlandı.</span><span class="sxs-lookup"><span data-stu-id="6b186-187">**UX_SUCCESS** (0x00) The configuration was successfully set.</span></span>

### <a name="example"></a><span data-ttu-id="6b186-188">Örnek</span><span class="sxs-lookup"><span data-stu-id="6b186-188">Example</span></span>

```c
ULONG configuration_value;
UINT status;

/* The following example illustrates this service. */
status = ux_device_stack_configuration_set(configuration_value);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_descriptor_send"></a><span data-ttu-id="6b186-189">ux_device_stack_descriptor_send</span><span class="sxs-lookup"><span data-stu-id="6b186-189">ux_device_stack_descriptor_send</span></span>

<span data-ttu-id="6b186-190">Konağa tanımlayıcı gönder</span><span class="sxs-lookup"><span data-stu-id="6b186-190">Send a descriptor to the host</span></span>

### <a name="prototype"></a><span data-ttu-id="6b186-191">Prototype</span><span class="sxs-lookup"><span data-stu-id="6b186-191">Prototype</span></span>

```c
UINT ux_device_stack_descriptor_send(
    ULONG descriptor_type, 
    ULONG request_index, 
    ULONG host_length);
```

### <a name="description"></a><span data-ttu-id="6b186-192">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6b186-192">Description</span></span>

<span data-ttu-id="6b186-193">Bu işlev, konak için bir tanımlayıcı döndürmek üzere cihaz tarafında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6b186-193">This function is used by the device side to return a descriptor to the host.</span></span> <span data-ttu-id="6b186-194">Bu tanımlayıcı bir cihaz tanımlayıcısı, bir yapılandırma tanımlayıcısı veya dize tanımlayıcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="6b186-194">This descriptor can be a device descriptor, a configuration descriptor or a string descriptor.</span></span>

### <a name="parameters"></a><span data-ttu-id="6b186-195">Parametreler</span><span class="sxs-lookup"><span data-stu-id="6b186-195">Parameters</span></span>

- <span data-ttu-id="6b186-196">**descriptor_type**: tanımlayıcının türü.</span><span class="sxs-lookup"><span data-stu-id="6b186-196">**descriptor_type**: The type of the descriptor.</span></span> <span data-ttu-id="6b186-197">Aşağıdaki değerlerden biri olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6b186-197">Must be one of the following values.</span></span>
  - <span data-ttu-id="6b186-198">**UX_DEVICE_DESCRIPTOR_ITEM**</span><span class="sxs-lookup"><span data-stu-id="6b186-198">**UX_DEVICE_DESCRIPTOR_ITEM**</span></span>
  - <span data-ttu-id="6b186-199">**UX_CONFIGURATION_DESCRIPTOR_ITEM**</span><span class="sxs-lookup"><span data-stu-id="6b186-199">**UX_CONFIGURATION_DESCRIPTOR_ITEM**</span></span>
  - <span data-ttu-id="6b186-200">**UX_STRING_DESCRIPTOR_ITEM**</span><span class="sxs-lookup"><span data-stu-id="6b186-200">**UX_STRING_DESCRIPTOR_ITEM**</span></span>
  - <span data-ttu-id="6b186-201">**UX_DEVICE_QUALIFIER_DESCRIPTOR_ITEM**</span><span class="sxs-lookup"><span data-stu-id="6b186-201">**UX_DEVICE_QUALIFIER_DESCRIPTOR_ITEM**</span></span>
  - <span data-ttu-id="6b186-202">**UX_OTHER_SPEED_DESCRIPTOR_ITEM**</span><span class="sxs-lookup"><span data-stu-id="6b186-202">**UX_OTHER_SPEED_DESCRIPTOR_ITEM**</span></span>
- <span data-ttu-id="6b186-203">**request_index**: tanımlayıcının dizini.</span><span class="sxs-lookup"><span data-stu-id="6b186-203">**request_index**: The index of the descriptor.</span></span>
- <span data-ttu-id="6b186-204">**host_length**: konağın gerektirdiği uzunluk.</span><span class="sxs-lookup"><span data-stu-id="6b186-204">**host_length**: The length required by the host.</span></span>

### <a name="return-values"></a><span data-ttu-id="6b186-205">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="6b186-205">Return Values</span></span>

- <span data-ttu-id="6b186-206">**UX_SUCCESS** (0x00) veri aktarımı tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="6b186-206">**UX_SUCCESS** (0x00) The data transfer was completed.</span></span>
- <span data-ttu-id="6b186-207">**UX_ERROR** (0xFF) aktarma tamamlanmadı.</span><span class="sxs-lookup"><span data-stu-id="6b186-207">**UX_ERROR** (0xFF) The transfer was not completed.</span></span>

### <a name="example"></a><span data-ttu-id="6b186-208">Örnek</span><span class="sxs-lookup"><span data-stu-id="6b186-208">Example</span></span>

```c
ULONG descriptor_type;
ULONG request_index;
ULONG host_length;
UINT status;

/* The following example illustrates this service. */
status = ux_device_stack_descriptor_send(descriptor_type, request_index, host_length);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_disconnect"></a><span data-ttu-id="6b186-209">ux_device_stack_disconnect</span><span class="sxs-lookup"><span data-stu-id="6b186-209">ux_device_stack_disconnect</span></span>

<span data-ttu-id="6b186-210">Cihaz yığınının bağlantısını kes</span><span class="sxs-lookup"><span data-stu-id="6b186-210">Disconnect device stack</span></span>

### <a name="prototype"></a><span data-ttu-id="6b186-211">Prototype</span><span class="sxs-lookup"><span data-stu-id="6b186-211">Prototype</span></span>

```c
UINT ux_device_stack_disconnect(VOID);
```

### <a name="description"></a><span data-ttu-id="6b186-212">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6b186-212">Description</span></span>

<span data-ttu-id="6b186-213">Bir cihaz bağlantısının kesilmesi durumunda VBUS Yöneticisi bu işlevi çağırır.</span><span class="sxs-lookup"><span data-stu-id="6b186-213">The VBUS manager calls this function when there is a device disconnection.</span></span> <span data-ttu-id="6b186-214">Cihaz yığını, bu cihaza kayıtlı tüm sınıfları bilgilendirir ve sonra tüm cihaz kaynaklarını serbest bırakacaktır.</span><span class="sxs-lookup"><span data-stu-id="6b186-214">The device stack will inform all classes registered to this device and will thereafter release all the device resources.</span></span>

### <a name="input-parameter"></a><span data-ttu-id="6b186-215">Giriş parametresi</span><span class="sxs-lookup"><span data-stu-id="6b186-215">Input Parameter</span></span>

<span data-ttu-id="6b186-216">Yok</span><span class="sxs-lookup"><span data-stu-id="6b186-216">None</span></span>

### <a name="return-value"></a><span data-ttu-id="6b186-217">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="6b186-217">Return Value</span></span>

- <span data-ttu-id="6b186-218">**UX_SUCCESS** (0x00) cihazın bağlantısı kesildi.</span><span class="sxs-lookup"><span data-stu-id="6b186-218">**UX_SUCCESS** (0x00) The device was disconnected.</span></span>

### <a name="example"></a><span data-ttu-id="6b186-219">Örnek</span><span class="sxs-lookup"><span data-stu-id="6b186-219">Example</span></span>

```c
UINT status;

/* The following example illustrates this service. */
status = ux_device_stack_disconnect();

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_endpoint_stall"></a><span data-ttu-id="6b186-220">ux_device_stack_endpoint_stall</span><span class="sxs-lookup"><span data-stu-id="6b186-220">ux_device_stack_endpoint_stall</span></span>

<span data-ttu-id="6b186-221">İstek uç noktası kabini koşulu</span><span class="sxs-lookup"><span data-stu-id="6b186-221">Request endpoint Stall condition</span></span>

### <a name="prototype"></a><span data-ttu-id="6b186-222">Prototype</span><span class="sxs-lookup"><span data-stu-id="6b186-222">Prototype</span></span>

```c
UINT ux_device_stack_endpoint_stall(UX_SLAVE_ENDPOINT*endpoint);
```

### <a name="description"></a><span data-ttu-id="6b186-223">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6b186-223">Description</span></span>

<span data-ttu-id="6b186-224">Bu işlev, bir uç noktanın konağa bir kabin koşulu döndürmesi gerektiğinde USB cihaz sınıfı tarafından çağrılır.</span><span class="sxs-lookup"><span data-stu-id="6b186-224">This function is called by the USB device class when an endpoint should return a Stall condition to the host.</span></span>

### <a name="input-parameter"></a><span data-ttu-id="6b186-225">Giriş parametresi</span><span class="sxs-lookup"><span data-stu-id="6b186-225">Input Parameter</span></span>

- <span data-ttu-id="6b186-226">**uç nokta** Kabin koşulunun istendiği uç nokta.</span><span class="sxs-lookup"><span data-stu-id="6b186-226">**endpoint** The endpoint on which the Stall condition is requested.</span></span>

### <a name="return-value"></a><span data-ttu-id="6b186-227">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="6b186-227">Return Value</span></span>

- <span data-ttu-id="6b186-228">**UX_SUCCESS** (0x00) Bu işlem başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="6b186-228">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="6b186-229">**UX_ERROR** (0xFF) cihaz geçersiz bir durumda.</span><span class="sxs-lookup"><span data-stu-id="6b186-229">**UX_ERROR** (0xFF) The device is in an invalid state.</span></span>

### <a name="example"></a><span data-ttu-id="6b186-230">Örnek</span><span class="sxs-lookup"><span data-stu-id="6b186-230">Example</span></span>

```c
UINT status;

/* The following example illustrates this service. */
status = ux_device_stack_endpoint_stall(endpoint);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_host_wakeup"></a><span data-ttu-id="6b186-231">ux_device_stack_host_wakeup</span><span class="sxs-lookup"><span data-stu-id="6b186-231">ux_device_stack_host_wakeup</span></span>

<span data-ttu-id="6b186-232">Konağı uyandırma</span><span class="sxs-lookup"><span data-stu-id="6b186-232">Wake up the host</span></span>

### <a name="prototype"></a><span data-ttu-id="6b186-233">Prototype</span><span class="sxs-lookup"><span data-stu-id="6b186-233">Prototype</span></span>

```c
UINT ux_device_stack_host_wakeup(VOID);
```

### <a name="description"></a><span data-ttu-id="6b186-234">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6b186-234">Description</span></span>

<span data-ttu-id="6b186-235">Bu işlev, cihaz ana bilgisayarı uyandırmayı istediğinde çağrılır.</span><span class="sxs-lookup"><span data-stu-id="6b186-235">This function is called when the device wants to wake up the host.</span></span> <span data-ttu-id="6b186-236">Bu komut yalnızca cihaz askıda kalma modundayken geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="6b186-236">This command is only valid when the device is in suspend mode.</span></span> <span data-ttu-id="6b186-237">Bu cihaz, USB konağını uyku modundan çıkarmak isteyip istemediğinize karar vermek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6b186-237">It is up to the device application to decide when it wants to wake up the USB host.</span></span> <span data-ttu-id="6b186-238">Örneğin, bir USB Modem, telefon hattında halka sinyali algıladığında bir ana bilgisayarı uyandırabilirler.</span><span class="sxs-lookup"><span data-stu-id="6b186-238">For instance, a USB modem can wake up a host when it detects a RING signal on the telephone line.</span></span>

### <a name="input-parameter"></a><span data-ttu-id="6b186-239">Giriş parametresi</span><span class="sxs-lookup"><span data-stu-id="6b186-239">Input Parameter</span></span>

<span data-ttu-id="6b186-240">Yok</span><span class="sxs-lookup"><span data-stu-id="6b186-240">None</span></span>

### <a name="return-values"></a><span data-ttu-id="6b186-241">Dönüş değerleri</span><span class="sxs-lookup"><span data-stu-id="6b186-241">Return values</span></span>

- <span data-ttu-id="6b186-242">**UX_SUCCESS** (0x00) çağrı başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="6b186-242">**UX_SUCCESS** (0x00) The call was successful.</span></span>
- <span data-ttu-id="6b186-243">**UX_FUNCTION_NOT_SUPPORTED** (0x54) çağrı başarısız oldu (cihaz muhtemelen askıya alınmış modda değildi).</span><span class="sxs-lookup"><span data-stu-id="6b186-243">**UX_FUNCTION_NOT_SUPPORTED** (0x54) The call failed (the device was probably not in the suspended mode).</span></span>

### <a name="example"></a><span data-ttu-id="6b186-244">Örnek</span><span class="sxs-lookup"><span data-stu-id="6b186-244">Example</span></span>

```c
UINT status;

/* The following example illustrates this service. */
status = ux_device_stack_host_wakeup();

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_initialize"></a><span data-ttu-id="6b186-245">ux_device_stack_initialize</span><span class="sxs-lookup"><span data-stu-id="6b186-245">ux_device_stack_initialize</span></span>

<span data-ttu-id="6b186-246">USB cihaz yığınını Başlat</span><span class="sxs-lookup"><span data-stu-id="6b186-246">Initialize USB device stack</span></span>

### <a name="prototype"></a><span data-ttu-id="6b186-247">Prototype</span><span class="sxs-lookup"><span data-stu-id="6b186-247">Prototype</span></span>

```c
UINT ux_device_stack_initialize(
    UCHAR *device_framework_high_speed,
    ULONG device_framework_length_high_speed,
    UCHAR *device_framework_full_speed,
    ULONG device_framework_length_full_speed,
    UCHAR *string_framework,
    ULONG string_framework_length,
    UCHAR *language_id_framework,
    ULONG language_id_framework_length),
    UINT (*ux_system_slave_change_function)(ULONG)));
```

### <a name="description"></a><span data-ttu-id="6b186-248">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6b186-248">Description</span></span>

<span data-ttu-id="6b186-249">Bu işlev, USB cihaz yığınını başlatmak için uygulama tarafından çağırılır.</span><span class="sxs-lookup"><span data-stu-id="6b186-249">This function is called by the application to initialize the USB device stack.</span></span> <span data-ttu-id="6b186-250">Herhangi bir sınıfı veya denetleyicisi başlatmaz.</span><span class="sxs-lookup"><span data-stu-id="6b186-250">It does not initialize any classes or any controllers.</span></span> <span data-ttu-id="6b186-251">Bu, ayrı işlev çağrılarında yapılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6b186-251">This should be done with separate function calls.</span></span> <span data-ttu-id="6b186-252">Bu çağrı, genellikle, USB işlevinin cihaz çerçevesi ile yığın sağlar.</span><span class="sxs-lookup"><span data-stu-id="6b186-252">This call mainly provides the stack with the device framework for the USB function.</span></span> <span data-ttu-id="6b186-253">Her hız için tamamen ayrı ayrı cihaz çerçevesine sahip olma olasılığa sahip hem yüksek hem de tam hızları destekler.</span><span class="sxs-lookup"><span data-stu-id="6b186-253">It supports both high and full speeds with the possibility to have completely separate device framework for each speed.</span></span> <span data-ttu-id="6b186-254">Dize çerçevesi ve birden çok dil desteklenir.</span><span class="sxs-lookup"><span data-stu-id="6b186-254">String framework and multiple languages are supported.</span></span>

### <a name="parameters"></a><span data-ttu-id="6b186-255">Parametreler</span><span class="sxs-lookup"><span data-stu-id="6b186-255">Parameters</span></span>

- <span data-ttu-id="6b186-256">**device_framework_high_speed**: yüksek hız çerçevesine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="6b186-256">**device_framework_high_speed**: Pointer to the high speed framework.</span></span>
- <span data-ttu-id="6b186-257">**device_framework_length_high_speed**: yüksek hız çerçevesinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="6b186-257">**device_framework_length_high_speed**: Length of the high speed framework.</span></span>
- <span data-ttu-id="6b186-258">**device_framework_full_speed**: tam hız çerçevesine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="6b186-258">**device_framework_full_speed**: Pointer to the full speed framework.</span></span>
- <span data-ttu-id="6b186-259">**device_framework_length_full_speed**: tam hız çerçevesinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="6b186-259">**device_framework_length_full_speed**: Length of the full speed framework.</span></span>
- <span data-ttu-id="6b186-260">**string_framework**: dize çerçevesi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="6b186-260">**string_framework**: Pointer to string framework.</span></span>
- <span data-ttu-id="6b186-261">**string_framework_length**: dize çerçevesinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="6b186-261">**string_framework_length**: Length of string framework.</span></span>
- <span data-ttu-id="6b186-262">**language_id_framework**: dize Language Framework işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="6b186-262">**language_id_framework**: Pointer to string language framework.</span></span>
- <span data-ttu-id="6b186-263">**language_id_framework_length**: dize dili çerçevesinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="6b186-263">**language_id_framework_length**: Length of the string language framework.</span></span>
- <span data-ttu-id="6b186-264">**ux_system_slave_change_function**: cihaz durumu değiştiğinde çağrılacak işlev.</span><span class="sxs-lookup"><span data-stu-id="6b186-264">**ux_system_slave_change_function**: Function to be called when the device state changes.</span></span>

### <a name="return-values"></a><span data-ttu-id="6b186-265">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="6b186-265">Return Values</span></span>

- <span data-ttu-id="6b186-266">**UX_SUCCESS** (0x00) Bu işlem başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="6b186-266">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="6b186-267">**UX_MEMORY_INSUFFICIENT** (0x12) yığının başlatılması için yeterli bellek yok.</span><span class="sxs-lookup"><span data-stu-id="6b186-267">**UX_MEMORY_INSUFFICIENT** (0x12) Not enough memory to initialize the stack.</span></span>
- <span data-ttu-id="6b186-268">**UX_DESCRIPTOR_CORRUPTED** (0x42) tanımlayıcı geçersiz.</span><span class="sxs-lookup"><span data-stu-id="6b186-268">**UX_DESCRIPTOR_CORRUPTED** (0x42) The descriptor is invalid.</span></span>

### <a name="example"></a><span data-ttu-id="6b186-269">Örnek</span><span class="sxs-lookup"><span data-stu-id="6b186-269">Example</span></span>

```c
/* Example of a device framework */

#define DEVICE_FRAMEWORK_LENGTH_FULL_SPEED 50

UCHAR device_framework_full_speed[] = {
    /* Device descriptor */
    0x12, 0x01, 0x10, 0x01, 0x00, 0x00, 0x00, 0x08,
    0xec, 0x08, 0x10, 0x00, 0x00, 0x00, 0x00, 0x00,
    0x00, 0x01,

    /* Configuration descriptor */
    0x09, 0x02, 0x20, 0x00, 0x01, 0x01, 0x00, 0xc0,
    0x32,

    /* Interface descriptor */
    0x09, 0x04, 0x00, 0x00, 0x02, 0x08, 0x06, 0x50,
    0x00,

    /* Endpoint descriptor (Bulk Out) */
    0x07, 0x05, 0x01, 0x02, 0x40, 0x00, 0x00,

    /* Endpoint descriptor (Bulk In) */
    0x07, 0x05, 0x82, 0x02, 0x40, 0x00, 0x00
};

#define DEVICE_FRAMEWORK_LENGTH_HIGH_SPEED 60

UCHAR device_framework_high_speed[] = {
    /* Device descriptor */
    0x12, 0x01, 0x00, 0x02, 0x00, 0x00, 0x00, 0x40,
    0x0a, 0x07, 0x25, 0x40, 0x01, 0x00, 0x01, 0x02,
    0x03, 0x01,

    /* Device qualifier descriptor */
    0x0a, 0x06, 0x00, 0x02, 0x00, 0x00, 0x00, 0x40,
    0x01, 0x00,

    /* Configuration descriptor */
    0x09, 0x02, 0x20, 0x00, 0x01, 0x01, 0x00, 0xc0,
    0x32,

    /* Interface descriptor */
    0x09, 0x04, 0x00, 0x00, 0x02, 0x08, 0x06, 0x50,
    0x00,

    /* Endpoint descriptor (Bulk Out) */
    0x07, 0x05, 0x01, 0x02, 0x00, 0x02, 0x00,

    /* Endpoint descriptor (Bulk In) */
    0x07, 0x05, 0x82, 0x02, 0x00, 0x02, 0x00
};

/* String Device Framework:
    Byte 0 and 1: Word containing the language ID: 0x0904 for US
    Byte 2 : Byte containing the index of the descriptor
    Byte 3 : Byte containing the length of the descriptor string */

#define STRING_FRAMEWORK_LENGTH 38 UCHAR string_framework[] = {
    /* Manufacturer string descriptor: Index 1 */
    0x09, 0x04, 0x01, 0x0c,
    0x45, 0x78, 0x70, 0x72,0x65, 0x73, 0x20, 0x4c,
    0x6f, 0x67, 0x69, 0x63,

    /* Product string descriptor: Index 2 */
    0x09, 0x04, 0x02, 0x0c,
    0x4D, 0x4C, 0x36, 0x39, 0x36, 0x35, 0x30, 0x30,
    0x20, 0x53, 0x44, 0x4B,

    /* Serial Number string descriptor: Index 3 */
    0x09, 0x04, 0x03, 0x04,
    0x30, 0x30, 0x30, 0x31
};

/* Multiple languages are supported on the device, to add a language besides English, 
  the Unicode language code must be appended to the language_id_framework array 
  and the length adjusted accordingly. */

#define LANGUAGE_ID_FRAMEWORK_LENGTH 2

UCHAR language_id_framework[] = {
    /* English. */
    0x09, 0x04
};
```

<span data-ttu-id="6b186-270">Bu uygulama, denetleyici durumunu değiştirdiğinde bir geri arama isteğinde bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="6b186-270">The application can request a call back when the controller changes its state.</span></span> <span data-ttu-id="6b186-271">Denetleyicinin iki ana durumu şunlardır:</span><span class="sxs-lookup"><span data-stu-id="6b186-271">The two main states for the controller are:</span></span>

- <span data-ttu-id="6b186-272">**UX_DEVICE_SUSPENDED**</span><span class="sxs-lookup"><span data-stu-id="6b186-272">**UX_DEVICE_SUSPENDED**</span></span>
- <span data-ttu-id="6b186-273">**UX_DEVICE_RESUMED**</span><span class="sxs-lookup"><span data-stu-id="6b186-273">**UX_DEVICE_RESUMED**</span></span>

<span data-ttu-id="6b186-274">Uygulamanın askıya alma/sürdürülme sinyalleri gerekmiyorsa, bir UX_NULL işlevi sağlar.</span><span class="sxs-lookup"><span data-stu-id="6b186-274">If the application does not need Suspend/Resume signals, it would supply a UX_NULL function.</span></span>

```c
UINT status;

/* The code below is required for installing the device portion of USBX. 
    There is no call back for device status change in this example. */
status = ux_device_stack_initialize(&device_framework_high_speed,
    DEVICE_FRAMEWORK_LENGTH_HIGH_SPEED, &device_framework_full_speed,
    DEVICE_FRAMEWORK_LENGTH_FULL_SPEED, &string_framework,
    STRING_FRAMEWORK_LENGTH, &language_id_framework,
    LANGUAGE_ID_FRAMEWORK_LENGTH, UX_NULL);

/* If status equals UX_SUCCESS, initialization was successful. */
```

### <a name="ux_device_stack_interface_delete"></a><span data-ttu-id="6b186-275">ux_device_stack_interface_delete</span><span class="sxs-lookup"><span data-stu-id="6b186-275">ux_device_stack_interface_delete</span></span>

<span data-ttu-id="6b186-276">Yığın arabirimini silme</span><span class="sxs-lookup"><span data-stu-id="6b186-276">Delete a stack interface</span></span>

### <a name="prototype"></a><span data-ttu-id="6b186-277">Prototype</span><span class="sxs-lookup"><span data-stu-id="6b186-277">Prototype</span></span>

```c
UINT ux_device_stack_interface_delete(UX_SLAVE_INTERFACE*interface);
```

### <a name="description"></a><span data-ttu-id="6b186-278">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6b186-278">Description</span></span>

<span data-ttu-id="6b186-279">Bu işlev, bir arabirim kaldırılması gerektiğinde çağrılır.</span><span class="sxs-lookup"><span data-stu-id="6b186-279">This function is called when an interface should be removed.</span></span> <span data-ttu-id="6b186-280">Bir cihaz ayıklanırken veya bir veri yolu sıfırlaması sonrasında ya da yeni bir alternatif ayar olduğunda arabirim kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="6b186-280">An interface is either removed when a device is extracted, or following a bus reset, or when there is a new alternate setting.</span></span>

### <a name="input-parameter"></a><span data-ttu-id="6b186-281">Giriş parametresi</span><span class="sxs-lookup"><span data-stu-id="6b186-281">Input Parameter</span></span>

- <span data-ttu-id="6b186-282">**arabirim**: kaldırılacak arabirime yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="6b186-282">**interface**: Pointer to the interface to remove.</span></span>

### <a name="return-value"></a><span data-ttu-id="6b186-283">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="6b186-283">Return Value</span></span>

- <span data-ttu-id="6b186-284">**UX_SUCCESS** (0x00) Bu işlem başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="6b186-284">**UX_SUCCESS** (0x00) This operation was successful.</span></span>

### <a name="example"></a><span data-ttu-id="6b186-285">Örnek</span><span class="sxs-lookup"><span data-stu-id="6b186-285">Example</span></span>

```c
UINT status;

/* The following example illustrates this service. */
status = ux_device_stack_interface_delete(interface);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_interface_get"></a><span data-ttu-id="6b186-286">ux_device_stack_interface_get</span><span class="sxs-lookup"><span data-stu-id="6b186-286">ux_device_stack_interface_get</span></span>

<span data-ttu-id="6b186-287">Geçerli arabirim değerini Al</span><span class="sxs-lookup"><span data-stu-id="6b186-287">Get the current interface value</span></span>

### <a name="prototype"></a><span data-ttu-id="6b186-288">Prototype</span><span class="sxs-lookup"><span data-stu-id="6b186-288">Prototype</span></span>

```c
UINT ux_device_stack_interface_get(UINT interface_value);
```

### <a name="description"></a><span data-ttu-id="6b186-289">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6b186-289">Description</span></span>

<span data-ttu-id="6b186-290">Bu işlev, ana bilgisayar geçerli arabirimi sorguladığında çağrılır.</span><span class="sxs-lookup"><span data-stu-id="6b186-290">This function is called when the host queries the current interface.</span></span> <span data-ttu-id="6b186-291">Cihaz geçerli arabirim değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="6b186-291">The device returns the current interface value.</span></span>

> [!NOTE]
> <span data-ttu-id="6b186-292">Bu işlev kullanım dışıdır.</span><span class="sxs-lookup"><span data-stu-id="6b186-292">This function is deprecated.</span></span> <span data-ttu-id="6b186-293">Bu, eski yazılımlar için kullanılabilir, ancak yeni yazılımların bunun yerine ***ux_device_stack_alternate_setting_get*** işlevini kullanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="6b186-293">It is available for legacy software, but new software should use the ***ux_device_stack_alternate_setting_get*** function instead.</span></span>

### <a name="input-parameter"></a><span data-ttu-id="6b186-294">Giriş parametresi</span><span class="sxs-lookup"><span data-stu-id="6b186-294">Input Parameter</span></span>

- <span data-ttu-id="6b186-295">**interface_value** Döndürülecek arabirim değeri.</span><span class="sxs-lookup"><span data-stu-id="6b186-295">**interface_value** Interface value to return.</span></span>

### <a name="return-values"></a><span data-ttu-id="6b186-296">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="6b186-296">Return Values</span></span>

- <span data-ttu-id="6b186-297">**UX_SUCCESS** (0x00) Bu işlem başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="6b186-297">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="6b186-298">**UX_ERROR** (0xFF) arabirim yok.</span><span class="sxs-lookup"><span data-stu-id="6b186-298">**UX_ERROR** (0xFF) No interface exists.</span></span>

### <a name="example"></a><span data-ttu-id="6b186-299">Örnek</span><span class="sxs-lookup"><span data-stu-id="6b186-299">Example</span></span>

```c
ULONG interface_value;

UINT status;

/* The following example illustrates this service. */
status = ux_device_stack_interface_get(interface_value);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_interface_set"></a><span data-ttu-id="6b186-300">ux_device_stack_interface_set</span><span class="sxs-lookup"><span data-stu-id="6b186-300">ux_device_stack_interface_set</span></span>

<span data-ttu-id="6b186-301">Arabirimin alternatif ayarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="6b186-301">Change the alternate setting of the interface</span></span>

### <a name="prototype"></a><span data-ttu-id="6b186-302">Prototype</span><span class="sxs-lookup"><span data-stu-id="6b186-302">Prototype</span></span>

```c
UINT ux_device_stack_interface_set(
    UCHAR *device_framework,
    ULONG device_framework_length, 
    ULONG alternate_setting_value);
```

### <a name="description"></a><span data-ttu-id="6b186-303">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6b186-303">Description</span></span>

<span data-ttu-id="6b186-304">Bu işlev, ana bilgisayar arabirim için alternatif ayarda bir değişiklik istediğinde çağrılır.</span><span class="sxs-lookup"><span data-stu-id="6b186-304">This function is called when the host requests a change of the alternate setting for the interface.</span></span>

### <a name="parameters"></a><span data-ttu-id="6b186-305">Parametreler</span><span class="sxs-lookup"><span data-stu-id="6b186-305">Parameters</span></span>

- <span data-ttu-id="6b186-306">**device_framework**: Bu arabirim için cihaz çerçevesinin adresi.</span><span class="sxs-lookup"><span data-stu-id="6b186-306">**device_framework**: Address of the device framework for this interface.</span></span>
- <span data-ttu-id="6b186-307">**device_framework_length**: cihaz çerçevesinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="6b186-307">**device_framework_length**: Length of the device framework.</span></span>
- <span data-ttu-id="6b186-308">**alternate_setting_value**: Bu arabirim tarafından kullanılacak alternatif ayar değeri.</span><span class="sxs-lookup"><span data-stu-id="6b186-308">**alternate_setting_value**: Alternate setting value to be used by this interface.</span></span>

### <a name="return-values"></a><span data-ttu-id="6b186-309">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="6b186-309">Return Values</span></span>

- <span data-ttu-id="6b186-310">**UX_SUCCESS** (0x00) Bu işlem başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="6b186-310">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="6b186-311">**UX_ERROR** (0xFF) arabirim yok.</span><span class="sxs-lookup"><span data-stu-id="6b186-311">**UX_ERROR** (0xFF) No interface exists.</span></span>

### <a name="example"></a><span data-ttu-id="6b186-312">Örnek</span><span class="sxs-lookup"><span data-stu-id="6b186-312">Example</span></span>

```c
UCHAR * device_framework
ULONG device_framework_length;
ULONG alternate_setting_value;
UINT status;

/* The following example illustrates this service. */
status = ux_device_stack_interface_set(device_framework,
    device_framework_length, alternate_setting_value);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_interface_start"></a><span data-ttu-id="6b186-313">ux_device_stack_interface_start</span><span class="sxs-lookup"><span data-stu-id="6b186-313">ux_device_stack_interface_start</span></span>

<span data-ttu-id="6b186-314">Arabirim örneğine sahip bir sınıf için Aramayı başlatma</span><span class="sxs-lookup"><span data-stu-id="6b186-314">Start search for a class to own an interface instance</span></span>

### <a name="prototype"></a><span data-ttu-id="6b186-315">Prototype</span><span class="sxs-lookup"><span data-stu-id="6b186-315">Prototype</span></span>

```c
UINT ux_device_stack_interface_start(UX_SLAVE_INTERFACE*interface);
```

### <a name="description"></a><span data-ttu-id="6b186-316">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6b186-316">Description</span></span>

<span data-ttu-id="6b186-317">Bu işlev, ana bilgisayar tarafından bir arabirim seçildiğinde ve cihaz yığınının bu arabirim örneğine sahip olmak için bir cihaz sınıfı araması gerektiğinde çağrılır.</span><span class="sxs-lookup"><span data-stu-id="6b186-317">This function is called when an interface has been selected by the host and the device stack needs to search for a device class to own this interface instance.</span></span>

### <a name="input-parameter"></a><span data-ttu-id="6b186-318">Giriş parametresi</span><span class="sxs-lookup"><span data-stu-id="6b186-318">Input Parameter</span></span>

- <span data-ttu-id="6b186-319">**arabirim**: oluşturulan arabirime yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="6b186-319">**interface**: Pointer to the interface created.</span></span>

### <a name="return-values"></a><span data-ttu-id="6b186-320">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="6b186-320">Return Values</span></span>

- <span data-ttu-id="6b186-321">**UX_SUCCESS** (0x00) Bu işlem başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="6b186-321">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="6b186-322">**UX_NO_CLASS_MATCH** (0x57) Bu arabirim için hiçbir sınıf yok.</span><span class="sxs-lookup"><span data-stu-id="6b186-322">**UX_NO_CLASS_MATCH** (0x57) No class exists for this interface.</span></span>

### <a name="example"></a><span data-ttu-id="6b186-323">Örnek</span><span class="sxs-lookup"><span data-stu-id="6b186-323">Example</span></span>

```c
UINT status;

/* The following example illustrates this service. */
status = ux_device_stack_interface_start(interface);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_transfer_request"></a><span data-ttu-id="6b186-324">ux_device_stack_transfer_request</span><span class="sxs-lookup"><span data-stu-id="6b186-324">ux_device_stack_transfer_request</span></span>

<span data-ttu-id="6b186-325">Konağa veri aktarma isteği</span><span class="sxs-lookup"><span data-stu-id="6b186-325">Request to transfer data to the host</span></span>

### <a name="prototype"></a><span data-ttu-id="6b186-326">Prototype</span><span class="sxs-lookup"><span data-stu-id="6b186-326">Prototype</span></span>

```c
UINT ux_device_stack_transfer_request(
    UX_SLAVE_TRANSFER *transfer_request,
    ULONG slave_length, 
    ULONG host_length);
```

### <a name="description"></a><span data-ttu-id="6b186-327">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6b186-327">Description</span></span>

<span data-ttu-id="6b186-328">Bu işlev, bir sınıf veya yığın konağa veri aktarmak istediğinde çağrılır.</span><span class="sxs-lookup"><span data-stu-id="6b186-328">This function is called when a class or the stack wants to transfer data to the host.</span></span> <span data-ttu-id="6b186-329">Konak, cihazı her zaman yoklar, ancak cihaz verileri önceden hazırlayabilir.</span><span class="sxs-lookup"><span data-stu-id="6b186-329">The host always polls the device but the device can prepare data in advance.</span></span>

### <a name="parameters"></a><span data-ttu-id="6b186-330">Parametreler</span><span class="sxs-lookup"><span data-stu-id="6b186-330">Parameters</span></span>

- <span data-ttu-id="6b186-331">**transfer_request**: aktarım isteğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="6b186-331">**transfer_request**: Pointer to the transfer request.</span></span>
- <span data-ttu-id="6b186-332">**slave_length**: cihazın geri dönmek istediği uzunluk.</span><span class="sxs-lookup"><span data-stu-id="6b186-332">**slave_length**: Length the device wants to return.</span></span>
- <span data-ttu-id="6b186-333">**host_length**: konağın istediği uzunluk.</span><span class="sxs-lookup"><span data-stu-id="6b186-333">**host_length**: Length the host has requested.</span></span>

### <a name="return-values"></a><span data-ttu-id="6b186-334">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="6b186-334">Return Values</span></span>

- <span data-ttu-id="6b186-335">**UX_SUCCESS** (0x00) Bu işlem başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="6b186-335">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="6b186-336">**UX_TRANSFER_NOT_READY** (0x25) cihaz geçersiz bir durumda; **eklenmiş**, **yapılandırılmış** veya **Çözümlenmiş** olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6b186-336">**UX_TRANSFER_NOT_READY** (0x25) The device is in an invalid state; it must be **ATTACHED**, **CONFIGURED**, or **ADDRESSED**.</span></span>
- <span data-ttu-id="6b186-337">**UX_ERROR** (0xFF) aktarım hatası.</span><span class="sxs-lookup"><span data-stu-id="6b186-337">**UX_ERROR** (0xFF) Transport error.</span></span>

### <a name="example"></a><span data-ttu-id="6b186-338">Örnek</span><span class="sxs-lookup"><span data-stu-id="6b186-338">Example</span></span>

```c
UINT status;

/* The following example illustrates how to transfer more data than an application requests. */
while(total_length) {
    /* How much can we send in this transfer? */
    if (total_length > UX_SLAVE_CLASS_STORAGE_BUFFER_SIZE)
        transfer_length = UX_SLAVE_CLASS_STORAGE_BUFFER_SIZE;
    else
        transfer_length = total_length;

   /* Copy the Storage Buffer into the transfer request memory. */
   ux_utility_memory_copy(transfer_request ->  ux_slave_transfer_request_data_pointer,
       media_memory, transfer_length);

   /* Send the data payload back to the caller. */
   status = ux_device_transfer_request(transfer_request,
       transfer_length, transfer_length);

   /* If status equals UX_SUCCESS, the operation was successful. */

   /* Update the buffer address.  */
    media_memory += transfer_length;

   /* Update the length to remain. */
    total_length -= transfer_length;
}
```

### <a name="ux_device_stack_transfer_abort"></a><span data-ttu-id="6b186-339">ux_device_stack_transfer_abort</span><span class="sxs-lookup"><span data-stu-id="6b186-339">ux_device_stack_transfer_abort</span></span>

<span data-ttu-id="6b186-340">Aktarım isteğini iptal etme</span><span class="sxs-lookup"><span data-stu-id="6b186-340">Cancel a transfer request</span></span>

### <a name="prototype"></a><span data-ttu-id="6b186-341">Prototype</span><span class="sxs-lookup"><span data-stu-id="6b186-341">Prototype</span></span>

```c
UINT ux_device_stack_transfer_abort(
    UX_SLAVE_TRANSFER *transfer_request, 
    ULONG completion_code);
```

### <a name="description"></a><span data-ttu-id="6b186-342">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6b186-342">Description</span></span>

<span data-ttu-id="6b186-343">Bu işlev, bir uygulamanın bir aktarım isteğini iptal etmek gerektiğinde veya yığının bir uç noktayla ilişkili bir aktarım isteğini iptal etmek gerektiğinde çağrılır.</span><span class="sxs-lookup"><span data-stu-id="6b186-343">This function is called when an application needs to cancel a transfer request or when the stack needs to abort a transfer request associated with an endpoint.</span></span>

### <a name="parameters"></a><span data-ttu-id="6b186-344">Parametreler</span><span class="sxs-lookup"><span data-stu-id="6b186-344">Parameters</span></span>

- <span data-ttu-id="6b186-345">**transfer_request**: aktarım isteğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="6b186-345">**transfer_request**: Pointer to the transfer request.</span></span>
- <span data-ttu-id="6b186-346">**completion_code**: Bu aktarım isteğinin tamamlanmasını bekleyen sınıfa döndürülecek hata kodu.</span><span class="sxs-lookup"><span data-stu-id="6b186-346">**completion_code**: Error code to be returned to the class waiting for this transfer request to complete.</span></span>

### <a name="return-value"></a><span data-ttu-id="6b186-347">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="6b186-347">Return Value</span></span>

- <span data-ttu-id="6b186-348">**UX_SUCCESS** (0x00) Bu işlem başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="6b186-348">**UX_SUCCESS** (0x00) This operation was successful.</span></span>

### <a name="example"></a><span data-ttu-id="6b186-349">Örnek</span><span class="sxs-lookup"><span data-stu-id="6b186-349">Example</span></span>

```c
UINT status;

/* The following example illustrates how to abort a transfer when a
    bus reset has been detected on the bus. */
status = ux_device_stack_transfer_abort(transfer_request, UX_TRANSFER_BUS_RESET);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_uninitialize"></a><span data-ttu-id="6b186-350">ux_device_stack_uninitialize</span><span class="sxs-lookup"><span data-stu-id="6b186-350">ux_device_stack_uninitialize</span></span>

<span data-ttu-id="6b186-351">Yığın kaldırma</span><span class="sxs-lookup"><span data-stu-id="6b186-351">Unitialize stack</span></span>

### <a name="prototype"></a><span data-ttu-id="6b186-352">Prototype</span><span class="sxs-lookup"><span data-stu-id="6b186-352">Prototype</span></span>

```c
UINT ux_device_stack_uninitialize();
```

### <a name="description"></a><span data-ttu-id="6b186-353">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6b186-353">Description</span></span>

<span data-ttu-id="6b186-354">Bu işlev, bir uygulamanın USBX cihaz yığınını geri almaması gerektiğinde çağrılır – tüm cihaz yığını kaynakları serbest bırakılır.</span><span class="sxs-lookup"><span data-stu-id="6b186-354">This function is called when an application needs to unitialize the USBX device stack – all device stack resources are freed.</span></span> <span data-ttu-id="6b186-355">Bu, tüm sınıfların ux_device_stack_class_unregister aracılığıyla kaydolduktan sonra çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6b186-355">This should be called after all classes have been unregistered via ux_device_stack_class_unregister.</span></span>

### <a name="parameters"></a><span data-ttu-id="6b186-356">Parametreler</span><span class="sxs-lookup"><span data-stu-id="6b186-356">Parameters</span></span>

<span data-ttu-id="6b186-357">Hiçbiri</span><span class="sxs-lookup"><span data-stu-id="6b186-357">None</span></span>

### <a name="return-value"></a><span data-ttu-id="6b186-358">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="6b186-358">Return Value</span></span>

<span data-ttu-id="6b186-359">**UX_SUCCESS** (0x00) Bu işlem başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="6b186-359">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
