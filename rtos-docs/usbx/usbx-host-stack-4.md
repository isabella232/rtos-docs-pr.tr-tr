---
title: Bölüm 4-USBX konak hizmetlerinin açıklaması
description: USBX konak hizmetleri hakkında bilgi edinin.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: d730658c07f3cd7cec8c75a47818314bdc63f35a
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104828456"
---
# <a name="chapter-4---description-of-usbx-host-services"></a><span data-ttu-id="61e9f-103">Bölüm 4-USBX konak hizmetlerinin açıklaması</span><span class="sxs-lookup"><span data-stu-id="61e9f-103">Chapter 4 - Description of USBX Host Services</span></span>

## <a name="ux_host_stack_initialize"></a><span data-ttu-id="61e9f-104">ux_host_stack_initialize</span><span class="sxs-lookup"><span data-stu-id="61e9f-104">ux_host_stack_initialize</span></span>

<span data-ttu-id="61e9f-105">Konak işlemi için USBX 'i başlatın.</span><span class="sxs-lookup"><span data-stu-id="61e9f-105">Initialize USBX for host operation.</span></span>

### <a name="prototype"></a><span data-ttu-id="61e9f-106">Prototype</span><span class="sxs-lookup"><span data-stu-id="61e9f-106">Prototype</span></span>

```c
UINT ux_host_stack_initialize(
    UINT (*system_change_function)
    (ULONG, UX_HOST_CLASS *));
```

### <a name="description"></a><span data-ttu-id="61e9f-107">Açıklama</span><span class="sxs-lookup"><span data-stu-id="61e9f-107">Description</span></span>

<span data-ttu-id="61e9f-108">Bu işlev, USB ana bilgisayar yığınını başlatacak.</span><span class="sxs-lookup"><span data-stu-id="61e9f-108">This function will initialize the USB host stack.</span></span> <span data-ttu-id="61e9f-109">Sağlanan bellek alanı, USBX iç kullanımı için kurulum olacaktır.</span><span class="sxs-lookup"><span data-stu-id="61e9f-109">The supplied memory area will be setup for USBX internal use.</span></span> <span data-ttu-id="61e9f-110">UX_SUCCESS döndürülürse, USBX konak denetleyicisi ve sınıf kaydı için hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="61e9f-110">If UX_SUCCESS is returned, USBX is ready for host controller and class registration.</span></span>

### <a name="input-parameter"></a><span data-ttu-id="61e9f-111">Giriş parametresi</span><span class="sxs-lookup"><span data-stu-id="61e9f-111">Input Parameter</span></span>

- <span data-ttu-id="61e9f-112">**system_change_function** Cihaz değişikliklerinin uygulamasına bildirimde bulunmak için isteğe bağlı geri arama yordamının işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="61e9f-112">**system_change_function** Pointer to optional callback routine for notifying application of device changes.</span></span>

### <a name="return-value"></a><span data-ttu-id="61e9f-113">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="61e9f-113">Return Value</span></span>

- <span data-ttu-id="61e9f-114">**UX_SUCCESS** (0x00) başarıyla başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="61e9f-114">**UX_SUCCESS** (0x00) Successful initialization.</span></span>
- <span data-ttu-id="61e9f-115">**UX_MEMORY_INSUFFICIENT** (0x12) bir bellek ayırma başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="61e9f-115">**UX_MEMORY_INSUFFICIENT** (0x12) A memory allocation failed.</span></span>

### <a name="example"></a><span data-ttu-id="61e9f-116">Örnek</span><span class="sxs-lookup"><span data-stu-id="61e9f-116">Example</span></span>

```c
UINT status;

/* Initialize USBX for host operation, without notification. */
status = ux_host_stack_initialize(UX_NULL);

/* If status equals UX_SUCCESS, USBX has been successfully initialized for host operation. */
```

## <a name="ux_host_stack_endpoint_transfer_abort"></a><span data-ttu-id="61e9f-117">ux_host_stack_endpoint_transfer_abort</span><span class="sxs-lookup"><span data-stu-id="61e9f-117">ux_host_stack_endpoint_transfer_abort</span></span>

<span data-ttu-id="61e9f-118">Bir uç nokta için aktarım isteğine bağlı tüm işlemleri iptal edin.</span><span class="sxs-lookup"><span data-stu-id="61e9f-118">Abort all transactions attached to a transfer request for an endpoint.</span></span>

### <a name="prototype"></a><span data-ttu-id="61e9f-119">Prototype</span><span class="sxs-lookup"><span data-stu-id="61e9f-119">Prototype</span></span>

```c
UINT ux_host_stack_endpoint_transfer_abort(UX_ENDPOINT *endpoint);
```

### <a name="description"></a><span data-ttu-id="61e9f-120">Açıklama</span><span class="sxs-lookup"><span data-stu-id="61e9f-120">Description</span></span>

<span data-ttu-id="61e9f-121">Bu işlev, bir uç noktaya bağlı belirli bir aktarım isteği için etkin veya bekleyen tüm işlemleri iptal eder.</span><span class="sxs-lookup"><span data-stu-id="61e9f-121">This function will cancel all transactions active or pending for a specific transfer request attached to an endpoint.</span></span> <span data-ttu-id="61e9f-122">Aktarım isteğinde bir geri çağırma işlevi eklenmiş, geri çağırma işlevi UX_TRANSACTION_ABORTED durumuyla çağrılır.</span><span class="sxs-lookup"><span data-stu-id="61e9f-122">It the transfer request has a callback function attached, the callback function will be called with the UX_TRANSACTION_ABORTED status.</span></span>

### <a name="input-parameter"></a><span data-ttu-id="61e9f-123">Giriş parametresi</span><span class="sxs-lookup"><span data-stu-id="61e9f-123">Input Parameter</span></span>

- <span data-ttu-id="61e9f-124">**uç nokta** Uç nokta işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="61e9f-124">**endpoint** Pointer to an endpoint.</span></span>

### <a name="return-values"></a><span data-ttu-id="61e9f-125">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="61e9f-125">Return Values</span></span>

- <span data-ttu-id="61e9f-126">Hata **UX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="61e9f-126">**UX_SUCCESS** (0x00) No errors.</span></span>
- <span data-ttu-id="61e9f-127">**UX_ENDPOINT_HANDLE_UNKNOWN** (0x53) uç noktası tanıtıcısı geçerli değil.</span><span class="sxs-lookup"><span data-stu-id="61e9f-127">**UX_ENDPOINT_HANDLE_UNKNOWN** (0x53) Endpoint handle is not valid.</span></span>

### <a name="example"></a><span data-ttu-id="61e9f-128">Örnek</span><span class="sxs-lookup"><span data-stu-id="61e9f-128">Example</span></span>

```c
UX_HOST_CLASS_PRINTER *printer;
UINT status;

/* Get the instance for this class. */
printer = (UX_HOST_CLASS_PRINTER *) command ->
    ux_host_class_command_instance;

/* The printer is being shut down. */

printer -> printer_state = UX_HOST_CLASS_INSTANCE_SHUTDOWN;

/* We need to abort transactions on the bulk out pipe. */
status = ux_host_stack_endpoint_transfer_abort
    (printer -> printer_bulk_out_endpoint);

/* If status equals UX_SUCCESS, the operation was successful */
```

## <a name="ux_host_stack_class_get"></a><span data-ttu-id="61e9f-129">ux_host_stack_class_get</span><span class="sxs-lookup"><span data-stu-id="61e9f-129">ux_host_stack_class_get</span></span>

<span data-ttu-id="61e9f-130">Bir sınıf kapsayıcısının işaretçisini alır.</span><span class="sxs-lookup"><span data-stu-id="61e9f-130">Get the pointer to a class container.</span></span>

### <a name="prototype"></a><span data-ttu-id="61e9f-131">Prototype</span><span class="sxs-lookup"><span data-stu-id="61e9f-131">Prototype</span></span>

```c
UINT ux_host_stack_class_get(
    UCHAR *class_name,
    UX_HOST_CLASS **class);
```

### <a name="description"></a><span data-ttu-id="61e9f-132">Açıklama</span><span class="sxs-lookup"><span data-stu-id="61e9f-132">Description</span></span>

<span data-ttu-id="61e9f-133">Bu işlev, sınıf kapsayıcısına bir işaretçi döndürür.</span><span class="sxs-lookup"><span data-stu-id="61e9f-133">This function returns a pointer to the class container.</span></span> <span data-ttu-id="61e9f-134">Bir sınıf veya uygulama bir cihazı açmak istediğinde örnekleri aramak için bir sınıfın kapsayıcısını USB yığınından alması gerekir.</span><span class="sxs-lookup"><span data-stu-id="61e9f-134">A class needs to obtain its container from the USB stack to search for instances when a class or an application wants to open a device.</span></span>

> [!NOTE]
> <span data-ttu-id="61e9f-135">Class_name C dizesi NULL ile sonlandırılmış olmalı ve bunun uzunluğu (NULL-Sonlandırıcı kendisi olmadan) UX_MAX_CLASS_NAME_LENGTH daha büyük olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="61e9f-135">The C string of class_name must be NULL-terminated and the length of it (without the NULL-terminator itself) must be no larger than UX_MAX_CLASS_NAME_LENGTH.</span></span>

### <a name="parameters"></a><span data-ttu-id="61e9f-136">Parametreler</span><span class="sxs-lookup"><span data-stu-id="61e9f-136">Parameters</span></span>

- <span data-ttu-id="61e9f-137">**class_name** Sınıf adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="61e9f-137">**class_name** Pointer to the class name.</span></span>
- <span data-ttu-id="61e9f-138">**sınıf** Sınıf adı için sınıf kapsayıcısını içeren işlev çağrısı tarafından güncelleştirilmiş bir işaretçi.</span><span class="sxs-lookup"><span data-stu-id="61e9f-138">**class** A pointer updated by the function call that contains the class container for the name of the class.</span></span>

### <a name="return-values"></a><span data-ttu-id="61e9f-139">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="61e9f-139">Return Values</span></span>

- <span data-ttu-id="61e9f-140">**UX_SUCCESS** (0x00) hata yok, return üzerinde sınıf alanı sınıf kapsayıcısının işaretçisi ile dosyalandı.</span><span class="sxs-lookup"><span data-stu-id="61e9f-140">**UX_SUCCESS** (0x00) No errors, on return the class field is filed with the pointer to the class container.</span></span>
- <span data-ttu-id="61e9f-141">**UX_HOST_CLASS_UNKNOWN** (0x59) sınıfı yığın tarafından bilinmiyor.</span><span class="sxs-lookup"><span data-stu-id="61e9f-141">**UX_HOST_CLASS_UNKNOWN** (0x59) Class is unknown by the stack.</span></span>

### <a name="example"></a><span data-ttu-id="61e9f-142">Örnek</span><span class="sxs-lookup"><span data-stu-id="61e9f-142">Example</span></span>

```c
UX_HOST_CLASS *printer_container;
UINT status;

/* Get the container for this class. */
status = ux_host_stack_class_get("ux_host_class_printer", &printer_container);

/* If status equals UX_SUCCESS, the operation was successful */
```

## <a name="ux_host_stack_class_register"></a><span data-ttu-id="61e9f-143">ux_host_stack_class_register</span><span class="sxs-lookup"><span data-stu-id="61e9f-143">ux_host_stack_class_register</span></span>

<span data-ttu-id="61e9f-144">USB yığınına USB sınıfı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="61e9f-144">Register a USB class to the USB stack.</span></span>

### <a name="prototype"></a><span data-ttu-id="61e9f-145">Prototype</span><span class="sxs-lookup"><span data-stu-id="61e9f-145">Prototype</span></span>

```c
UINT ux_host_stack_class_register(
    UCHAR *class_name,
    UINT (*class_entry_address) (struct UX_HOST_CLASS_COMMAND_STRUCT *));
```

### <a name="description"></a><span data-ttu-id="61e9f-146">Açıklama</span><span class="sxs-lookup"><span data-stu-id="61e9f-146">Description</span></span>

<span data-ttu-id="61e9f-147">Bu işlev USB yığınına USB sınıfı kaydeder.</span><span class="sxs-lookup"><span data-stu-id="61e9f-147">This function registers a USB class to the USB stack.</span></span> <span data-ttu-id="61e9f-148">Sınıfı, USB yığınının aşağıdaki gibi komutları gönderebilmesi için bir giriş noktası belirtmelidir.</span><span class="sxs-lookup"><span data-stu-id="61e9f-148">The class must specify an entry point for the USB stack to send commands such as the following.</span></span>

- <span data-ttu-id="61e9f-149">**UX_HOST_CLASS_COMMAND_QUERY**</span><span class="sxs-lookup"><span data-stu-id="61e9f-149">**UX_HOST_CLASS_COMMAND_QUERY**</span></span>
- <span data-ttu-id="61e9f-150">**UX_HOST_CLASS_COMMAND_ACTIVATE**</span><span class="sxs-lookup"><span data-stu-id="61e9f-150">**UX_HOST_CLASS_COMMAND_ACTIVATE**</span></span>
- <span data-ttu-id="61e9f-151">**UX_HOST_CLASS_COMMAND_DESTROY**</span><span class="sxs-lookup"><span data-stu-id="61e9f-151">**UX_HOST_CLASS_COMMAND_DESTROY**</span></span>

> [!NOTE]
> <span data-ttu-id="61e9f-152">*Class_name* C dizesi null ile sonlandırılmış olmalı ve bunun uzunluğu (null-Sonlandırıcı kendisi olmadan) **UX_MAX_CLASS_NAME_LENGTH** daha büyük olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="61e9f-152">The C string of *class_name* must be NULL-terminated and the length of it (without the NULL-terminator itself) must be no larger than **UX_MAX_CLASS_NAME_LENGTH**.</span></span>

### <a name="parameters"></a><span data-ttu-id="61e9f-153">Parametreler</span><span class="sxs-lookup"><span data-stu-id="61e9f-153">Parameters</span></span>

- <span data-ttu-id="61e9f-154">**class_name** Sınıfın adı işaretçisi, geçerli girdiler, USBX USB sınıfları altındaki ux_system_initialize. c dosyasında bulunur.</span><span class="sxs-lookup"><span data-stu-id="61e9f-154">**class_name** Pointer to the name of the class, valid entries are found in the file ux_system_initialize.c under the USB Classes of USBX.</span></span>
- <span data-ttu-id="61e9f-155">**class_entry_address** Sınıfın giriş işlevinin adresi.</span><span class="sxs-lookup"><span data-stu-id="61e9f-155">**class_entry_address** Address of the entry function of the class.</span></span>

### <a name="return-values"></a><span data-ttu-id="61e9f-156">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="61e9f-156">Return Values</span></span>

- <span data-ttu-id="61e9f-157">**UX_SUCCESS** (0x00) sınıfı başarıyla yüklendi.</span><span class="sxs-lookup"><span data-stu-id="61e9f-157">**UX_SUCCESS** (0x00) Class installed successfully.</span></span>
- <span data-ttu-id="61e9f-158">**UX_MEMORY_ARRAY_FULL** (0x1A) bu sınıfı depolamak için daha fazla bellek yok.</span><span class="sxs-lookup"><span data-stu-id="61e9f-158">**UX_MEMORY_ARRAY_FULL** (0x1a) No more memory to store this class.</span></span>
- <span data-ttu-id="61e9f-159">**UX_HOST_CLASS_ALREADY_INSTALLED** (0x58) konak sınıfı zaten yüklü.</span><span class="sxs-lookup"><span data-stu-id="61e9f-159">**UX_HOST_CLASS_ALREADY_INSTALLED** (0x58) Host class already installed.</span></span>

### <a name="example"></a><span data-ttu-id="61e9f-160">Örnek:</span><span class="sxs-lookup"><span data-stu-id="61e9f-160">Example:</span></span>

```c
UINT status;

/* Register all the classes for this implementation. */
status = ux_host_stack_class_register("ux_host_class_hub", ux_host_class_hub_entry);

/* If status equals UX_SUCCESS, class was successfully installed. */
```

## <a name="ux_host_stack_class_instance_create"></a><span data-ttu-id="61e9f-161">ux_host_stack_class_instance_create</span><span class="sxs-lookup"><span data-stu-id="61e9f-161">ux_host_stack_class_instance_create</span></span>

<span data-ttu-id="61e9f-162">Sınıf kapsayıcısı için yeni bir sınıf örneği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="61e9f-162">Create a new class instance for a class container.</span></span>

### <a name="prototype"></a><span data-ttu-id="61e9f-163">Prototype</span><span class="sxs-lookup"><span data-stu-id="61e9f-163">Prototype</span></span>

```c
UINT ux_host_stack_class_instance_create(
    UX_HOST_CLASS *class, 
    VOID *class_instance);
```

### <a name="description"></a><span data-ttu-id="61e9f-164">Açıklama</span><span class="sxs-lookup"><span data-stu-id="61e9f-164">Description</span></span>

<span data-ttu-id="61e9f-165">Bu işlev, sınıf kapsayıcısı için yeni bir sınıf örneği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="61e9f-165">This function creates a new class instance for a class container.</span></span> <span data-ttu-id="61e9f-166">Sınıf karmaşıklığını azaltmak için sınıfın örneği sınıf kodunda yer alır.</span><span class="sxs-lookup"><span data-stu-id="61e9f-166">The instance of a class is not contained in the class code to reduce the class complexity.</span></span> <span data-ttu-id="61e9f-167">Bunun yerine, her bir sınıf örneği, ana yığında bulunan sınıf kapsayıcısına iliştirilir.</span><span class="sxs-lookup"><span data-stu-id="61e9f-167">Rather, each class instance is attached to the class container located in the main stack.</span></span>

### <a name="parameters"></a><span data-ttu-id="61e9f-168">Parametreler</span><span class="sxs-lookup"><span data-stu-id="61e9f-168">Parameters</span></span>

- <span data-ttu-id="61e9f-169">**sınıf** Sınıf kapsayıcısının işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="61e9f-169">**class** Pointer to the class container.</span></span>
- <span data-ttu-id="61e9f-170">**class_instance** Oluşturulacak sınıf örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="61e9f-170">**class_instance** Pointer to the class instance to be created.</span></span>

### <a name="return-value"></a><span data-ttu-id="61e9f-171">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="61e9f-171">Return Value</span></span>

- <span data-ttu-id="61e9f-172">**UX_SUCCESS** (0x00) sınıf örneği sınıf kapsayıcısına iliştirildi.</span><span class="sxs-lookup"><span data-stu-id="61e9f-172">**UX_SUCCESS** (0x00) The class instance was attached to the class container.</span></span>

### <a name="example"></a><span data-ttu-id="61e9f-173">Örnek</span><span class="sxs-lookup"><span data-stu-id="61e9f-173">Example</span></span>

```c
UINT status;

UX_HOST_CLASS_PRINTER *printer;

/* Obtain memory for this class instance. */

printer = ux_memory_allocate(UX_NO_ALIGN, sizeof(UX_HOST_CLASS_PRINTER));

if (printer == UX_NULL)
    return(UX_MEMORY_INSUFFICIENT);

/* Store the class container into this instance. */
printer -> printer_class = command -> ux_host_class;

/* Create this class instance. */
status = ux_host_stack_class_instance_create(printer -> printer_class, (VOID *)printer);

/* If status equals UX_SUCCESS, the class instance was successfully created and attached to the class container. */
```

## <a name="ux_host_stack_class_instance_destroy"></a><span data-ttu-id="61e9f-174">ux_host_stack_class_instance_destroy</span><span class="sxs-lookup"><span data-stu-id="61e9f-174">ux_host_stack_class_instance_destroy</span></span>

<span data-ttu-id="61e9f-175">Sınıf kapsayıcısı için bir sınıf örneğini yok edin.</span><span class="sxs-lookup"><span data-stu-id="61e9f-175">Destroy a class instance for a class container.</span></span>

### <a name="prototype"></a><span data-ttu-id="61e9f-176">Prototype</span><span class="sxs-lookup"><span data-stu-id="61e9f-176">Prototype</span></span>

```c
UINT ux_host_stack_class_instance_destroy(
    UX_HOST_CLASS *class, 
    VOID *class_instance);
```

### <a name="description"></a><span data-ttu-id="61e9f-177">Açıklama</span><span class="sxs-lookup"><span data-stu-id="61e9f-177">Description</span></span>

<span data-ttu-id="61e9f-178">Bu işlev, sınıf kapsayıcısı için bir sınıf örneğini yok eder.</span><span class="sxs-lookup"><span data-stu-id="61e9f-178">This function destroys a class instance for a class container.</span></span>

### <a name="parameters"></a><span data-ttu-id="61e9f-179">Parametreler</span><span class="sxs-lookup"><span data-stu-id="61e9f-179">Parameters</span></span>

- <span data-ttu-id="61e9f-180">**sınıf** Sınıf kapsayıcısının işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="61e9f-180">**class** Pointer to the class container.</span></span>
- <span data-ttu-id="61e9f-181">**class_instance** Yok edilecek örneğe yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="61e9f-181">**class_instance** Pointer to the instance to destroy.</span></span>

### <a name="return-values"></a><span data-ttu-id="61e9f-182">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="61e9f-182">Return Values</span></span>

- <span data-ttu-id="61e9f-183">**UX_SUCCESS** (0x00) sınıf örneği yok edildi.</span><span class="sxs-lookup"><span data-stu-id="61e9f-183">**UX_SUCCESS** (0x00) The class instance was destroyed.</span></span>
- <span data-ttu-id="61e9f-184">**UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) sınıf örneği sınıf kapsayıcısına eklenmez.</span><span class="sxs-lookup"><span data-stu-id="61e9f-184">**UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) The class instance is not attached to the class container.</span></span>

### <a name="example"></a><span data-ttu-id="61e9f-185">Örnek</span><span class="sxs-lookup"><span data-stu-id="61e9f-185">Example</span></span>

```c
UINT status;
UX_HOST_CLASS_PRINTER *printer;

/* Get the instance for this class. */
printer = (UX_HOST_CLASS_PRINTER *) command -> ux_host_class_command_instance;

/* The printer is being shut down. */
printer -> printer_state = UX_HOST_CLASS_INSTANCE_SHUTDOWN;

/* Destroy the instance. */
status = ux_host_stack_class_instance_destroy(printer -> printer_class, (VOID *) printer);

/* If status equals UX_SUCCESS, the class instance was successfully destroyed. */
```

## <a name="ux_host_stack_class_instance_get"></a><span data-ttu-id="61e9f-186">ux_host_stack_class_instance_get</span><span class="sxs-lookup"><span data-stu-id="61e9f-186">ux_host_stack_class_instance_get</span></span>

<span data-ttu-id="61e9f-187">Belirli bir sınıf için bir sınıf örneği işaretçisi alır.</span><span class="sxs-lookup"><span data-stu-id="61e9f-187">Get a class instance pointer for a specific class.</span></span>

### <a name="prototype"></a><span data-ttu-id="61e9f-188">Prototype</span><span class="sxs-lookup"><span data-stu-id="61e9f-188">Prototype</span></span>

```c
UINT ux_host_stack_class_instance_get(
    UX_HOST_CLASS *class,
    UINT class_index, 
    VOID **class_instance);
```

### <a name="description"></a><span data-ttu-id="61e9f-189">Açıklama</span><span class="sxs-lookup"><span data-stu-id="61e9f-189">Description</span></span>

<span data-ttu-id="61e9f-190">Bu işlev, belirli bir sınıf için bir sınıf örneği işaretçisi döndürür.</span><span class="sxs-lookup"><span data-stu-id="61e9f-190">This function returns a class instance pointer for a specific class.</span></span> <span data-ttu-id="61e9f-191">Sınıf karmaşıklığını azaltmak için sınıfın örneği sınıf kodunda yer alır.</span><span class="sxs-lookup"><span data-stu-id="61e9f-191">The instance of a class is not contained in the class code to reduce the class complexity.</span></span> <span data-ttu-id="61e9f-192">Bunun yerine, her bir sınıf örneği sınıf kapsayıcısına iliştirilir.</span><span class="sxs-lookup"><span data-stu-id="61e9f-192">Rather, each class instance is attached to the class container.</span></span> <span data-ttu-id="61e9f-193">Bu işlev, sınıf kapsayıcısı içinde sınıf örnekleri aramak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="61e9f-193">This function is used to search for class instances within a class container.</span></span>

### <a name="parameters"></a><span data-ttu-id="61e9f-194">Parametreler</span><span class="sxs-lookup"><span data-stu-id="61e9f-194">Parameters</span></span>

- <span data-ttu-id="61e9f-195">**sınıf** Sınıf kapsayıcısının işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="61e9f-195">**class** Pointer to the class container.</span></span>
- <span data-ttu-id="61e9f-196">**class_index** Kapsayıcıya iliştirilmiş sınıfların listesi içindeki işlev çağrısı tarafından kullanılacak dizin.</span><span class="sxs-lookup"><span data-stu-id="61e9f-196">**class_index** An index to be used by the function call within the list of attached classes to the container.</span></span>
- <span data-ttu-id="61e9f-197">**class_instance** İşlev çağrısının döndürdüğü örneğe yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="61e9f-197">**class_instance** Pointer to the instance to be returned by the function call.</span></span>

### <a name="return-values"></a><span data-ttu-id="61e9f-198">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="61e9f-198">Return Values</span></span>

- <span data-ttu-id="61e9f-199">**UX_SUCCESS** (0x00) sınıf örneği bulundu.</span><span class="sxs-lookup"><span data-stu-id="61e9f-199">**UX_SUCCESS** (0x00) The class instance was found.</span></span>

- <span data-ttu-id="61e9f-200">**UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) sınıf kapsayıcısına iliştirilmiş daha fazla sınıf örneği yok.</span><span class="sxs-lookup"><span data-stu-id="61e9f-200">**UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) There are no more class instances attached to the class container.</span></span>

### <a name="example"></a><span data-ttu-id="61e9f-201">Örnek</span><span class="sxs-lookup"><span data-stu-id="61e9f-201">Example</span></span>

```c
UINT status;

UX_HOST_CLASS_PRINTER *printer;

/* Obtain memory for this class instance. */
printer = ux_memory_allocate(UX_NO_ALIGN, sizeof(UX_HOST_CLASS_PRINTER));

if (printer == UX_NULL) return(UX_MEMORY_INSUFFICIENT);

/* Search for instance index 2. */
status = ux_host_stack_class_instance_get(class, 2, (VOID *) printer);

/* If status equals UX_SUCCESS, the class instance was found. */
```

## <a name="ux_host_stack_device_configuration_get"></a><span data-ttu-id="61e9f-202">ux_host_stack_device_configuration_get</span><span class="sxs-lookup"><span data-stu-id="61e9f-202">ux_host_stack_device_configuration_get</span></span>

<span data-ttu-id="61e9f-203">Yapılandırma kapsayıcısına yönelik bir işaretçi alır.</span><span class="sxs-lookup"><span data-stu-id="61e9f-203">Get a pointer to a configuration container.</span></span>

### <a name="prototype"></a><span data-ttu-id="61e9f-204">Prototype</span><span class="sxs-lookup"><span data-stu-id="61e9f-204">Prototype</span></span>

```c
UINT ux_host_stack_device_configuration_get(
    UX_DEVICE *device,
    UINT configuration_index, 
    UX_CONFIGURATION *configuration);
```

### <a name="description"></a><span data-ttu-id="61e9f-205">Açıklama</span><span class="sxs-lookup"><span data-stu-id="61e9f-205">Description</span></span>

<span data-ttu-id="61e9f-206">Bu işlev bir cihaz tanıtıcısına ve bir yapılandırma dizinine bağlı olarak bir yapılandırma kapsayıcısı döndürür.</span><span class="sxs-lookup"><span data-stu-id="61e9f-206">This function returns a configuration container based on a device handle and a configuration index.</span></span>

### <a name="parameters"></a><span data-ttu-id="61e9f-207">Parametreler</span><span class="sxs-lookup"><span data-stu-id="61e9f-207">Parameters</span></span>

- <span data-ttu-id="61e9f-208">**cihaz** İstenen yapılandırmanın sahibi olan cihaz kapsayıcısının işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="61e9f-208">**device** Pointer to the device container that owns the configuration requested.</span></span>
- <span data-ttu-id="61e9f-209">**configuration_index** Aranacak yapılandırmanın dizini.</span><span class="sxs-lookup"><span data-stu-id="61e9f-209">**configuration_index** Index of the configuration to be searched.</span></span>
- <span data-ttu-id="61e9f-210">**yapılandırma** Döndürülecek Yapılandırma kapsayıcısının işaretçisinin adresi.</span><span class="sxs-lookup"><span data-stu-id="61e9f-210">**configuration** Address of the pointer to the configuration container to be returned.</span></span>

### <a name="return-values"></a><span data-ttu-id="61e9f-211">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="61e9f-211">Return Values</span></span>

- <span data-ttu-id="61e9f-212">**UX_SUCCESS** (0x00) yapılandırma bulundu.</span><span class="sxs-lookup"><span data-stu-id="61e9f-212">**UX_SUCCESS** (0x00) The configuration was found.</span></span>
- <span data-ttu-id="61e9f-213">**UX_DEVICE_HANDLE_UNKNOWN** (0x50) cihaz kapsayıcısı yok.</span><span class="sxs-lookup"><span data-stu-id="61e9f-213">**UX_DEVICE_HANDLE_UNKNOWN** (0x50) The device container does not exist.</span></span>
- <span data-ttu-id="61e9f-214">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) dizin için yapılandırma tanıtıcısı yok.</span><span class="sxs-lookup"><span data-stu-id="61e9f-214">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) The configuration handle for the index does not exist.</span></span>

### <a name="example"></a><span data-ttu-id="61e9f-215">Örnek</span><span class="sxs-lookup"><span data-stu-id="61e9f-215">Example</span></span>

```c
UINT status;

UX_HOST_CLASS_PRINTER *printer;

/* If the device has been configured already, we don't need to do it
again. */

if (printer -> printer_device -> ux_device_state == UX_DEVICE_CONFIGURED)
    return(UX_SUCCESS);

/* A printer normally has one configuration, retrieve 1st configuration only. */

status = ux_host_stack_device_configuration_get(printer -> printer_device,
    0, configuration);

/* If status equals UX_SUCCESS, the configuration was found. */
```

## <a name="ux_host_stack_device_configuration_select"></a><span data-ttu-id="61e9f-216">ux_host_stack_device_configuration_select</span><span class="sxs-lookup"><span data-stu-id="61e9f-216">ux_host_stack_device_configuration_select</span></span>

<span data-ttu-id="61e9f-217">Bir cihaz için belirli bir yapılandırma seçin.</span><span class="sxs-lookup"><span data-stu-id="61e9f-217">Select a specific configuration for a device.</span></span>

### <a name="prototype"></a><span data-ttu-id="61e9f-218">Prototype</span><span class="sxs-lookup"><span data-stu-id="61e9f-218">Prototype</span></span>

```c
UINT ux_host_stack_device_configuration_select (UX_CONFIGURATION *configuration);
```

### <a name="description"></a><span data-ttu-id="61e9f-219">Açıklama</span><span class="sxs-lookup"><span data-stu-id="61e9f-219">Description</span></span>

<span data-ttu-id="61e9f-220">Bu işlev, bir cihaz için belirli bir yapılandırma seçer.</span><span class="sxs-lookup"><span data-stu-id="61e9f-220">This function selects a specific configuration for a device.</span></span> <span data-ttu-id="61e9f-221">Bu yapılandırma cihaza ayarlandığında, varsayılan olarak, her cihaz arabirimi ve ilişkili alternatif ayarı 0 ' da cihazda etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="61e9f-221">When this configuration is set to the device, by default, each device interface and its associated alternate setting 0 is activated on the device.</span></span> <span data-ttu-id="61e9f-222">Cihaz/arabirim sınıfı belirli bir arabirimin ayarını değiştirmeyi istiyorsa, bir **ux_host_stack_interface_setting_select** hizmet çağrısı vermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="61e9f-222">If the device/interface class wishes to change the setting of a particular interface, it needs to issue a **ux_host_stack_interface_setting_select** service call.</span></span>

### <a name="parameters"></a><span data-ttu-id="61e9f-223">Parametreler</span><span class="sxs-lookup"><span data-stu-id="61e9f-223">Parameters</span></span>

- <span data-ttu-id="61e9f-224">**yapılandırma** Bu cihaz için etkinleştirilecek Yapılandırma kapsayıcısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="61e9f-224">**configuration** Pointer to the configuration container that is to be enabled for this device.</span></span>

### <a name="return-values"></a><span data-ttu-id="61e9f-225">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="61e9f-225">Return Values</span></span>

- <span data-ttu-id="61e9f-226">**UX_SUCCESS** (0x00) yapılandırma seçimi başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="61e9f-226">**UX_SUCCESS** (0x00) The configuration selection was successful.</span></span>
- <span data-ttu-id="61e9f-227">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) yapılandırma tanıtıcısı yok.</span><span class="sxs-lookup"><span data-stu-id="61e9f-227">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) The configuration handle does not exist.</span></span>
- <span data-ttu-id="61e9f-228">**UX_OVER_CURRENT_CONDITION** (0x43) Bu yapılandırma için veri yolunda geçerli bir durum var.</span><span class="sxs-lookup"><span data-stu-id="61e9f-228">**UX_OVER_CURRENT_CONDITION** (0x43) An over current condition exists on the bus for this configuration.</span></span>

### <a name="example"></a><span data-ttu-id="61e9f-229">Örnek</span><span class="sxs-lookup"><span data-stu-id="61e9f-229">Example</span></span>

```c
UINT status;

UX_HOST_CLASS_PRINTER *printer;

/* If the device has been configured already, we don't need to do it again. */
if (printer -> printer_device -> ux_device_state == UX_DEVICE_CONFIGURED)
    return(UX_SUCCESS);

/* A printer normally has one configuration - retrieve 1st configuration only. */
status = ux_host_stack_device_configuration_get(printer -> printer_device, 0,configuration);

/* If status equals UX_SUCCESS, the configuration selection was successful. */

/* If valid configuration, ask USBX to set this configuration. */
status = ux_host_stack_device_configuration_select(configuration);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_stack_device_get"></a><span data-ttu-id="61e9f-230">ux_host_stack_device_get</span><span class="sxs-lookup"><span data-stu-id="61e9f-230">ux_host_stack_device_get</span></span>

<span data-ttu-id="61e9f-231">Cihaz kapsayıcısı için bir işaretçi alır.</span><span class="sxs-lookup"><span data-stu-id="61e9f-231">Get a pointer to a device container.</span></span>

### <a name="prototype"></a><span data-ttu-id="61e9f-232">Prototype</span><span class="sxs-lookup"><span data-stu-id="61e9f-232">Prototype</span></span>

```c
UINT ux_host_stack_device_get(
    ULONG device_index, 
    UX_DEVICE *device);
```

### <a name="description"></a><span data-ttu-id="61e9f-233">Açıklama</span><span class="sxs-lookup"><span data-stu-id="61e9f-233">Description</span></span>

<span data-ttu-id="61e9f-234">Bu işlev, dizinine göre bir cihaz kapsayıcısı döndürür.</span><span class="sxs-lookup"><span data-stu-id="61e9f-234">This function returns a device container based on its index.</span></span> <span data-ttu-id="61e9f-235">Cihaz dizini 0 ile başlar.</span><span class="sxs-lookup"><span data-stu-id="61e9f-235">The device index starts with 0.</span></span> <span data-ttu-id="61e9f-236">Birkaç denetleyicimiz olduğundan ve bir bayt dizini yeterince bulunmayabilir, dizinin bir ULONG olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="61e9f-236">Note that the index is a ULONG because we could have several controllers and a byte index might not be enough.</span></span> <span data-ttu-id="61e9f-237">Cihaz dizini, veri yoluna özgü olan cihaz adresiyle karıştırılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="61e9f-237">The device index should not be confused with the device address that is bus specific.</span></span>

### <a name="parameters"></a><span data-ttu-id="61e9f-238">Parametreler</span><span class="sxs-lookup"><span data-stu-id="61e9f-238">Parameters</span></span>

- <span data-ttu-id="61e9f-239">**device_index** Cihazın dizini.</span><span class="sxs-lookup"><span data-stu-id="61e9f-239">**device_index** Index of the device.</span></span>
- <span data-ttu-id="61e9f-240">**cihaz** Döndürülecek cihaz kapsayıcısının işaretçisinin adresi.</span><span class="sxs-lookup"><span data-stu-id="61e9f-240">**device** Address of the pointer for the device container to return.</span></span>

### <a name="return-values"></a><span data-ttu-id="61e9f-241">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="61e9f-241">Return Values</span></span>

- <span data-ttu-id="61e9f-242">**UX_SUCCESS** (0x00) cihaz kapsayıcısı var ve döndürülür</span><span class="sxs-lookup"><span data-stu-id="61e9f-242">**UX_SUCCESS** (0x00) The device container exists and is returned</span></span>
- <span data-ttu-id="61e9f-243">**UX_DEVICE_HANDLE_UNKNOWN** (0x50) cihaz bilinmiyor</span><span class="sxs-lookup"><span data-stu-id="61e9f-243">**UX_DEVICE_HANDLE_UNKNOWN** (0x50) Device unknown</span></span>

### <a name="example"></a><span data-ttu-id="61e9f-244">Örnek</span><span class="sxs-lookup"><span data-stu-id="61e9f-244">Example</span></span>

```c
UINT status;

/* Locate the first device in USBX. */
status = ux_host_stack_device_get(0, device);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_stack_interface_endpoint_get"></a><span data-ttu-id="61e9f-245">ux_host_stack_interface_endpoint_get</span><span class="sxs-lookup"><span data-stu-id="61e9f-245">ux_host_stack_interface_endpoint_get</span></span>

<span data-ttu-id="61e9f-246">Bir uç nokta kapsayıcısı alın.</span><span class="sxs-lookup"><span data-stu-id="61e9f-246">Get an endpoint container.</span></span>

### <a name="prototype"></a><span data-ttu-id="61e9f-247">Prototype</span><span class="sxs-lookup"><span data-stu-id="61e9f-247">Prototype</span></span>

```c
UINT ux_host_stack_interface_endpoint_get(
    UX_INTERFACE *interface,
    UINT endpoint_index,
    UX_ENDPOINT *endpoint);
```

### <a name="description"></a><span data-ttu-id="61e9f-248">Açıklama</span><span class="sxs-lookup"><span data-stu-id="61e9f-248">Description</span></span>

<span data-ttu-id="61e9f-249">Bu işlev, arabirim tanıtıcısına ve bir uç nokta dizinine göre bir uç nokta kapsayıcısı döndürür.</span><span class="sxs-lookup"><span data-stu-id="61e9f-249">This function returns an endpoint container based on the interface handle and an endpoint index.</span></span> <span data-ttu-id="61e9f-250">Bu, arabirim için alternatif ayarların seçildiği veya aranmakta olan bitiş noktaları öncesinde varsayılan ayar kullanıldığı varsayılır.</span><span class="sxs-lookup"><span data-stu-id="61e9f-250">It is assumed that the alternate setting for the interface has been selected or the default setting is being used prior to the endpoint(s) being searched.</span></span>

### <a name="parameters"></a><span data-ttu-id="61e9f-251">Parametreler</span><span class="sxs-lookup"><span data-stu-id="61e9f-251">Parameters</span></span>

- <span data-ttu-id="61e9f-252">**arabirim** İstenen uç noktayı içeren arabirim kapsayıcısının işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="61e9f-252">**interface** Pointer to the interface container that contains the endpoint requested.</span></span>
- <span data-ttu-id="61e9f-253">**endpoint_index** Bu arabirimdeki uç noktanın dizini.</span><span class="sxs-lookup"><span data-stu-id="61e9f-253">**endpoint_index** Index of the endpoint in this interface.</span></span>
- <span data-ttu-id="61e9f-254">**uç nokta** Döndürülecek uç nokta kapsayıcısının adresi.</span><span class="sxs-lookup"><span data-stu-id="61e9f-254">**endpoint** Address of the endpoint container to be returned.</span></span>

### <a name="return-values"></a><span data-ttu-id="61e9f-255">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="61e9f-255">Return Values</span></span>

- <span data-ttu-id="61e9f-256">**UX_SUCCESS** (0x00) uç nokta kapsayıcısı var ve döndürülür.</span><span class="sxs-lookup"><span data-stu-id="61e9f-256">**UX_SUCCESS** (0x00) The endpoint container exists and is returned.</span></span>
- <span data-ttu-id="61e9f-257">**UX_INTERFACE_HANDLE_UNKNOWN** (0x52) belirtilen arabirim yok.</span><span class="sxs-lookup"><span data-stu-id="61e9f-257">**UX_INTERFACE_HANDLE_UNKNOWN** (0x52) Interface specified does not exist.</span></span>
- <span data-ttu-id="61e9f-258">**UX_ENDPOINT_HANDLE_UNKNOWN** (0x53) uç noktası dizini yok.</span><span class="sxs-lookup"><span data-stu-id="61e9f-258">**UX_ENDPOINT_HANDLE_UNKNOWN** (0x53) Endpoint index does not exist.</span></span>

### <a name="example"></a><span data-ttu-id="61e9f-259">Örnek</span><span class="sxs-lookup"><span data-stu-id="61e9f-259">Example</span></span>

```c
UINT status;
UX_HOST_CLASS_PRINTER *printer;

for(endpoint_index = 0;
    endpoint_index < printer -> printer_interface ->
        ux_interface_descriptor.bNumEndpoints;
    endpoint_index++)
{
    status = ux_host_stack_interface_endpoint_get (printer -> printer_interface,
        endpoint_index, &endpoint);

    if (status == UX_SUCCESS)
    {
        /* Check if endpoint is bulk and OUT. */
        if (((endpoint -> ux_endpoint_descriptor.bEndpointAddress &
            UX_ENDPOINT_DIRECTION) == UX_ENDPOINT_OUT) &&
            ((endpoint -> ux_endpoint_descriptor.bmAttributes &
            UX_MASK_ENDPOINT_TYPE) == UX_BULK_ENDPOINT))
        return(UX_SUCCESS);
    }
}
```

## <a name="ux_host_stack_hcd_register"></a><span data-ttu-id="61e9f-260">ux_host_stack_hcd_register</span><span class="sxs-lookup"><span data-stu-id="61e9f-260">ux_host_stack_hcd_register</span></span>

<span data-ttu-id="61e9f-261">USB yığınına USB denetleyicisi kaydedin.</span><span class="sxs-lookup"><span data-stu-id="61e9f-261">Register a USB controller to the USB stack.</span></span>

### <a name="prototype"></a><span data-ttu-id="61e9f-262">Prototype</span><span class="sxs-lookup"><span data-stu-id="61e9f-262">Prototype</span></span>

```c
UINT ux_host_stack_hcd_register(
    UCHAR *hcd_name,
    UINT (*hcd_function)(struct UX_HCD_STRUCT *),
    ULONG hcd_param1, ULONG hcd_param2);
```

### <a name="description"></a><span data-ttu-id="61e9f-263">Açıklama</span><span class="sxs-lookup"><span data-stu-id="61e9f-263">Description</span></span>

<span data-ttu-id="61e9f-264">Bu işlev USB yığınına USB denetleyicisi kaydeder.</span><span class="sxs-lookup"><span data-stu-id="61e9f-264">This function registers a USB controller to the USB stack.</span></span> <span data-ttu-id="61e9f-265">Bu, genellikle bu denetleyici tarafından kullanılan belleği ayırır ve başlatma komutunu denetleyiciye geçirir.</span><span class="sxs-lookup"><span data-stu-id="61e9f-265">It mainly allocates the memory used by this controller and passes the initialization command to the controller.</span></span>

### <a name="parameters"></a><span data-ttu-id="61e9f-266">Parametreler</span><span class="sxs-lookup"><span data-stu-id="61e9f-266">Parameters</span></span>

- <span data-ttu-id="61e9f-267">**hcd_name** Konak denetleyicisinin adı</span><span class="sxs-lookup"><span data-stu-id="61e9f-267">**hcd_name** Name of the host controller</span></span>
- <span data-ttu-id="61e9f-268">**hcd_function** Başlangıçtan sorumlu ana bilgisayar denetleyicisindeki işlev.</span><span class="sxs-lookup"><span data-stu-id="61e9f-268">**hcd_function** The function in the host controller responsible for the initialization.</span></span>
- <span data-ttu-id="61e9f-269">**hcd_param1** HCD tarafından kullanılan GÇ veya bellek kaynağı.</span><span class="sxs-lookup"><span data-stu-id="61e9f-269">**hcd_param1** The IO or memory resource used by the hcd.</span></span>
- <span data-ttu-id="61e9f-270">**hcd_param2** Konak denetleyicisi tarafından kullanılan IRQ.</span><span class="sxs-lookup"><span data-stu-id="61e9f-270">**hcd_param2** The IRQ used by the host controller.</span></span>

### <a name="return-values"></a><span data-ttu-id="61e9f-271">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="61e9f-271">Return Values</span></span>

- <span data-ttu-id="61e9f-272">**UX_SUCCESS** (0x00) denetleyici düzgün şekilde başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="61e9f-272">**UX_SUCCESS** (0x00) The controller was initialized properly.</span></span>
- <span data-ttu-id="61e9f-273">**UX_MEMORY_INSUFFICIENT** (0x12) Bu denetleyici için yeterli bellek yok.</span><span class="sxs-lookup"><span data-stu-id="61e9f-273">**UX_MEMORY_INSUFFICIENT** (0x12) Not enough memory for this controller.</span></span>
- <span data-ttu-id="61e9f-274">**UX_PORT_RESET_FAILED** (0x31) denetleyicinin sıfırlanması başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="61e9f-274">**UX_PORT_RESET_FAILED** (0x31) The reset of the controller failed.</span></span>
- <span data-ttu-id="61e9f-275">**UX_CONTROLLER_INIT_FAILED** (0x32) denetleyici düzgün şekilde başlatılamadı.</span><span class="sxs-lookup"><span data-stu-id="61e9f-275">**UX_CONTROLLER_INIT_FAILED** (0x32) The controller failed to initialize properly.</span></span>

### <a name="example"></a><span data-ttu-id="61e9f-276">Örnek</span><span class="sxs-lookup"><span data-stu-id="61e9f-276">Example</span></span>

```c
UINT status;

/* Initialize a host controller mapped at address 0xd0000 and using IRQ 10. */

status = ux_host_stack_hcd_register("ux_hcd_controller",
    ux_hcd_controller_initialize, 0xd0000, 0x0a);

/* If status equals UX_SUCCESS, the controller was initialized properly. */

/* Note that the application must also setup a call to the
    interrupt handler for the controller.
    The function for the controller is called _ux_hch_controller_interrupt_handler. */
```

## <a name="ux_host_stack_configuration_interface_get"></a><span data-ttu-id="61e9f-277">ux_host_stack_configuration_interface_get</span><span class="sxs-lookup"><span data-stu-id="61e9f-277">ux_host_stack_configuration_interface_get</span></span>

<span data-ttu-id="61e9f-278">Arabirim kapsayıcısı işaretçisi alın.</span><span class="sxs-lookup"><span data-stu-id="61e9f-278">Get an interface container pointer.</span></span>

### <a name="prototype"></a><span data-ttu-id="61e9f-279">Prototype</span><span class="sxs-lookup"><span data-stu-id="61e9f-279">Prototype</span></span>

```c
UINT ux_host_stack_configuration_interface_get (
    UX_CONFIGURATION *configuration,
    UINT interface_index, 
    UINT alternate_setting_index, 
    UX_INTERFACE **interface);
```

### <a name="description"></a><span data-ttu-id="61e9f-280">Açıklama</span><span class="sxs-lookup"><span data-stu-id="61e9f-280">Description</span></span>

<span data-ttu-id="61e9f-281">Bu işlev, bir yapılandırma tanıtıcısına, bir arabirim dizinine ve alternatif ayar dizinine göre bir arabirim kapsayıcısı döndürür.</span><span class="sxs-lookup"><span data-stu-id="61e9f-281">This function returns an interface container based on a configuration handle, an interface index, and an alternate setting index.</span></span>

### <a name="parameters"></a><span data-ttu-id="61e9f-282">Parametreler</span><span class="sxs-lookup"><span data-stu-id="61e9f-282">Parameters</span></span>

- <span data-ttu-id="61e9f-283">**yapılandırma** Arabirime sahip olan Yapılandırma kapsayıcısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="61e9f-283">**configuration** Pointer to the configuration container that owns the interface.</span></span>
- <span data-ttu-id="61e9f-284">**interface_index** Aranacak arabirim dizini.</span><span class="sxs-lookup"><span data-stu-id="61e9f-284">**interface_index** Interface index to be searched.</span></span>
- <span data-ttu-id="61e9f-285">**alternate_setting_index** Arama için arabirim içindeki alternatif ayar.</span><span class="sxs-lookup"><span data-stu-id="61e9f-285">**alternate_setting_index** Alternate setting within the interface to search.</span></span>
- <span data-ttu-id="61e9f-286">**arabirim** Döndürülecek arabirim kapsayıcısı işaretçisinin adresi.</span><span class="sxs-lookup"><span data-stu-id="61e9f-286">**interface** Address of the interface container pointer to be returned.</span></span>

### <a name="return-values"></a><span data-ttu-id="61e9f-287">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="61e9f-287">Return Values</span></span>

- <span data-ttu-id="61e9f-288">**UX_SUCCESS** (0x00) arabirim dizini için arabirim kapsayıcısı ve alternatif ayar bulundu ve döndürüldü.</span><span class="sxs-lookup"><span data-stu-id="61e9f-288">**UX_SUCCESS** (0x00) The interface container for the interface index and the alternate setting was found and returned.</span></span>
- <span data-ttu-id="61e9f-289">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) yapılandırma yok.</span><span class="sxs-lookup"><span data-stu-id="61e9f-289">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) The configuration does not exist.</span></span>
- <span data-ttu-id="61e9f-290">**UX_INTERFACE_HANDLE_UNKNOWN** (0x52) arabirim yok.</span><span class="sxs-lookup"><span data-stu-id="61e9f-290">**UX_INTERFACE_HANDLE_UNKNOWN** (0x52) The interface does not exist.</span></span>

### <a name="example"></a><span data-ttu-id="61e9f-291">Örnek</span><span class="sxs-lookup"><span data-stu-id="61e9f-291">Example</span></span>

```c
UINT status;

/* Search for the default alternate setting on the first interface for the printer. */
status = ux_host_stack_configuration_interface_get(configuration, 0, 0,
    &printer -> printer_interface);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_stack_interface_setting_select"></a><span data-ttu-id="61e9f-292">ux_host_stack_interface_setting_select</span><span class="sxs-lookup"><span data-stu-id="61e9f-292">ux_host_stack_interface_setting_select</span></span>

<span data-ttu-id="61e9f-293">Arabirim için alternatif bir ayar seçin.</span><span class="sxs-lookup"><span data-stu-id="61e9f-293">Select an alternate setting for an interface.</span></span>

### <a name="prototype"></a><span data-ttu-id="61e9f-294">Prototype</span><span class="sxs-lookup"><span data-stu-id="61e9f-294">Prototype</span></span>

```c
UINT ux_host_stack_interface_setting_select(UX_INTERFACE *interface);
```

### <a name="description"></a><span data-ttu-id="61e9f-295">Açıklama</span><span class="sxs-lookup"><span data-stu-id="61e9f-295">Description</span></span>

<span data-ttu-id="61e9f-296">Bu işlev, seçilen yapılandırmaya ait belirli bir arabirim için belirli bir alternatif ayarı seçer.</span><span class="sxs-lookup"><span data-stu-id="61e9f-296">This function selects a specific alternate setting for a given interface belonging to the selected configuration.</span></span> <span data-ttu-id="61e9f-297">Bu işlev, varsayılan alternatif ayarından yeni bir ayara geçmek veya varsayılan alternatif ayara geri dönmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="61e9f-297">This function is used to change from the default alternate setting to a new setting or to go back to the default alternate setting.</span></span> <span data-ttu-id="61e9f-298">Yeni bir alternatif ayar seçildiğinde, önceki uç nokta özellikleri geçersizdir ve yeniden yüklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="61e9f-298">When a new alternate setting is selected, the previous endpoint characteristics are invalid and should be reloaded.</span></span>

### <a name="input-parameter"></a><span data-ttu-id="61e9f-299">Giriş parametresi</span><span class="sxs-lookup"><span data-stu-id="61e9f-299">Input Parameter</span></span>

- <span data-ttu-id="61e9f-300">**arabirim** Alternatif ayarı seçilecek olan arabirim kapsayıcısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="61e9f-300">**interface** Pointer to the interface container whose alternate setting is to be selected.</span></span>

### <a name="return-values"></a><span data-ttu-id="61e9f-301">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="61e9f-301">Return Values</span></span>

- <span data-ttu-id="61e9f-302">**UX_SUCCESS** (0x00) Bu arabirim için alternatif ayar başarıyla seçildi.</span><span class="sxs-lookup"><span data-stu-id="61e9f-302">**UX_SUCCESS** (0x00) The alternate setting for this interface has been successfully selected.</span></span>
- <span data-ttu-id="61e9f-303">**UX_INTERFACE_HANDLE_UNKNOWN** (0x52) arabirim yok.</span><span class="sxs-lookup"><span data-stu-id="61e9f-303">**UX_INTERFACE_HANDLE_UNKNOWN** (0x52) The interface does not exist.</span></span>

### <a name="example"></a><span data-ttu-id="61e9f-304">Örnek</span><span class="sxs-lookup"><span data-stu-id="61e9f-304">Example</span></span>

```c
UINT status;

/* Select a new alternate setting for this interface. */
status = ux_host_stack_interface_setting_select(interface);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_stack_transfer_request_abort"></a><span data-ttu-id="61e9f-305">ux_host_stack_transfer_request_abort</span><span class="sxs-lookup"><span data-stu-id="61e9f-305">ux_host_stack_transfer_request_abort</span></span>

<span data-ttu-id="61e9f-306">Bekleyen bir aktarım isteğini iptal edin.</span><span class="sxs-lookup"><span data-stu-id="61e9f-306">Abort a pending transfer request.</span></span>

### <a name="prototype"></a><span data-ttu-id="61e9f-307">Prototype</span><span class="sxs-lookup"><span data-stu-id="61e9f-307">Prototype</span></span>

```c
UINT ux_host_stack_transfer_request_abort(UX_TRANSFER REQUEST *transfer request);
```

### <a name="description"></a><span data-ttu-id="61e9f-308">Açıklama</span><span class="sxs-lookup"><span data-stu-id="61e9f-308">Description</span></span>

<span data-ttu-id="61e9f-309">Bu işlev, daha önce gönderilen bir bekleyen aktarım isteğini iptal eder.</span><span class="sxs-lookup"><span data-stu-id="61e9f-309">This function aborts a pending transfer request that has been previously submitted.</span></span> <span data-ttu-id="61e9f-310">Bu işlev yalnızca belirli bir aktarım isteğini iptal eder.</span><span class="sxs-lookup"><span data-stu-id="61e9f-310">This function only cancels a specific transfer request.</span></span> <span data-ttu-id="61e9f-311">İşleve geri çağrı UX_TRANSFER REQUEST_STATUS_ABORT durumuna sahip olur.</span><span class="sxs-lookup"><span data-stu-id="61e9f-311">The call back to the function will have the UX_TRANSFER REQUEST_STATUS_ABORT status.</span></span>

### <a name="parameters"></a><span data-ttu-id="61e9f-312">Parametreler</span><span class="sxs-lookup"><span data-stu-id="61e9f-312">Parameters</span></span>

- <span data-ttu-id="61e9f-313">**aktarım isteği** İptal edilecek aktarım isteğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="61e9f-313">**transfer request** Pointer to the transfer request to be aborted.</span></span>

### <a name="return-values"></a><span data-ttu-id="61e9f-314">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="61e9f-314">Return Values</span></span>

- <span data-ttu-id="61e9f-315">**UX_SUCCESS** (0x00) bu aktarım isteğinin USB aktarımı iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="61e9f-315">**UX_SUCCESS** (0x00) The USB transfer for this transfer request was canceled.</span></span>

### <a name="example"></a><span data-ttu-id="61e9f-316">Örnek</span><span class="sxs-lookup"><span data-stu-id="61e9f-316">Example</span></span>

```c
UINT status;

/* The following example illustrates this service. */
status = ux_host_stack_transfer_request_abort(transfer request);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_stack_transfer_request"></a><span data-ttu-id="61e9f-317">ux_host_stack_transfer_request</span><span class="sxs-lookup"><span data-stu-id="61e9f-317">ux_host_stack_transfer_request</span></span>

<span data-ttu-id="61e9f-318">Bir USB aktarımı isteyin.</span><span class="sxs-lookup"><span data-stu-id="61e9f-318">Request a USB transfer.</span></span>

### <a name="prototype"></a><span data-ttu-id="61e9f-319">Prototype</span><span class="sxs-lookup"><span data-stu-id="61e9f-319">Prototype</span></span>

```c
UINT ux_host_stack_transfer_request(UX_TRANSFER REQUEST *transfer request);
```

### <a name="description"></a><span data-ttu-id="61e9f-320">Açıklama</span><span class="sxs-lookup"><span data-stu-id="61e9f-320">Description</span></span>

<span data-ttu-id="61e9f-321">Bu işlev bir USB işlemi gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="61e9f-321">This function performs a USB transaction.</span></span> <span data-ttu-id="61e9f-322">Girişte, aktarım isteği bu işlem için seçili uç nokta kanalını ve aktarımıyla ilişkili parametreleri (veri yükü, işlem uzunluğu) sağlar.</span><span class="sxs-lookup"><span data-stu-id="61e9f-322">On entry the transfer request gives the endpoint pipe selected for this transaction and the parameters associated with the transfer (data payload, length of transaction).</span></span> <span data-ttu-id="61e9f-323">Denetim kanalı için, işlem engelleniyor ve yalnızca denetim aktarımının üç aşaması tamamlandığında veya önceki bir hata varsa döndürülür.</span><span class="sxs-lookup"><span data-stu-id="61e9f-323">For Control pipe, the transaction is blocking and will only return when the three phases of the control transfer have been completed or if there is a previous error.</span></span> <span data-ttu-id="61e9f-324">Diğer kanallar için, USB yığını işlemi USB üzerinde zamanlar, ancak tamamlanmasını beklemez.</span><span class="sxs-lookup"><span data-stu-id="61e9f-324">For other pipes, the USB stack will schedule the transaction on the USB but will not wait for its completion.</span></span> <span data-ttu-id="61e9f-325">Engelleyici olmayan kanallara yönelik her aktarım isteğinin bir tamamlama yordamı işleyicisi belirtmesi vardır.</span><span class="sxs-lookup"><span data-stu-id="61e9f-325">Each transfer request for non-blocking pipes has to specify a completion routine handler.</span></span>

<span data-ttu-id="61e9f-326">İşlev çağrısı döndüğünde, aktarım isteğinin durumu işlemin sonucunu içerdiğinden incelenmelidir.</span><span class="sxs-lookup"><span data-stu-id="61e9f-326">When the function call returns, the status of the transfer request should be examined as it contains the result of the transaction.</span></span>

### <a name="input-parameter"></a><span data-ttu-id="61e9f-327">Giriş parametresi</span><span class="sxs-lookup"><span data-stu-id="61e9f-327">Input Parameter</span></span>

- <span data-ttu-id="61e9f-328">**transfer_request** Aktarım isteğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="61e9f-328">**transfer_request** Pointer to the transfer request.</span></span> <span data-ttu-id="61e9f-329">Aktarım isteği, aktarım için gereken tüm gerekli bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="61e9f-329">The transfer request contains all the necessary information required for the transfer.</span></span>

### <a name="return-values"></a><span data-ttu-id="61e9f-330">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="61e9f-330">Return Values</span></span>

- <span data-ttu-id="61e9f-331">**UX_SUCCESS** (0x00) bu aktarım isteğinin USB aktarımı düzgün zamanlandı.</span><span class="sxs-lookup"><span data-stu-id="61e9f-331">**UX_SUCCESS** (0x00) The USB transfer for this transfer request was scheduled properly.</span></span> <span data-ttu-id="61e9f-332">Aktarım isteği tamamlandığında aktarım isteğinin durum kodu incelenmelidir.</span><span class="sxs-lookup"><span data-stu-id="61e9f-332">The status code of the transfer request should be examined when the transfer request completes.</span></span>
- <span data-ttu-id="61e9f-333">**UX_MEMORY_INSUFFICIENT** (0x12) gerekli denetleyici kaynaklarını ayırmak için yeterli bellek yok.</span><span class="sxs-lookup"><span data-stu-id="61e9f-333">**UX_MEMORY_INSUFFICIENT** (0x12) Not enough memory to allocate the necessary controller resources.</span></span>
- <span data-ttu-id="61e9f-334">**UX_TRANSFER_NOT_READY** (0x25) cihaz geçersiz bir durumda; bağlı, ÇÖZÜMLENMIŞ veya yapılandırılmış olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="61e9f-334">**UX_TRANSFER_NOT_READY** (0x25) The device was in an invalid state – must be ATTACHED,ADDRESSED, or CONFIGURED.</span></span>

### <a name="example"></a><span data-ttu-id="61e9f-335">Örnek:</span><span class="sxs-lookup"><span data-stu-id="61e9f-335">Example:</span></span>

```c
UINT status;

/* Create a transfer request for the SET_CONFIGURATION request. No data for this request. */
transfer_request -> ux_transfer_request_requested_length = 0;
transfer_request -> ux_transfer_request_function = UX_SET_CONFIGURATION;
transfer_request -> ux_transfer_request_type =
    UX_REQUEST_OUT |
    UX_REQUEST_TYPE_STANDARD |
    UX_REQUEST_TARGET_DEVICE;

transfer_request -> ux_transfer_request_value = (USHORT)
    configuration -> ux_configuration_descriptor.bConfigurationValue;
transfer_request -> ux_transfer_request_index = 0;

/* Send request to HCD layer. */
status = ux_host_stack_transfer_request(transfer_request);

/* If status equals UX_SUCCESS, the operation was successful. */
```
