---
title: Bölüm 5-Modül Yöneticisi API 'Leri
author: philmea
description: Bu makale, uygulamanın yerleşik bölümünün kullanabildiği Modül Yöneticisi API 'lerinin bir özetidir.
ms.author: philmea
ms.date: 07/15/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: ca0fee443c23fd1bdd34651f4a7b31cf71f886f0
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825486"
---
# <a name="chapter-5---module-manager-apis"></a><span data-ttu-id="8cbc8-103">Bölüm 5-Modül Yöneticisi API 'Leri</span><span class="sxs-lookup"><span data-stu-id="8cbc8-103">Chapter 5 - Module Manager APIs</span></span>

## <a name="summary-of-module-manager-apis"></a><span data-ttu-id="8cbc8-104">Modül Yöneticisi API 'Lerinin Özeti</span><span class="sxs-lookup"><span data-stu-id="8cbc8-104">Summary of Module Manager APIs</span></span>

<span data-ttu-id="8cbc8-105">Uygulamanın yerleşik bölümü için aşağıdaki gibi çeşitli ek API 'Ler mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-105">There are several additional APIs available to the resident portion of the application, as follows.</span></span>

- <span data-ttu-id="8cbc8-106">\***txm_module_manager_external_memory_enable** _-_Enable modül erişimi paylaşılan bir bellek alanına erişebilir \*</span><span class="sxs-lookup"><span data-stu-id="8cbc8-106">***txm_module_manager_external_memory_enable** _ - _Enable module access to a shared memory space*</span></span>
- <span data-ttu-id="8cbc8-107">\*Fılex \* ile dosya **txm_module_manager_file_load** _-_Load modülü</span><span class="sxs-lookup"><span data-stu-id="8cbc8-107">***txm_module_manager_file_load** _ - _Load module from file via FileX*</span></span>
- <span data-ttu-id="8cbc8-108">\***txm_module_manager_in_place_load** _-_Load modül verileri, yerinde yürütme \*</span><span class="sxs-lookup"><span data-stu-id="8cbc8-108">***txm_module_manager_in_place_load** _ - _Load module data, execute in place*</span></span>
- <span data-ttu-id="8cbc8-109">\***txm_module_manager_initialize** _-_Initialize Modül Yöneticisi \*</span><span class="sxs-lookup"><span data-stu-id="8cbc8-109">***txm_module_manager_initialize** _ - _Initialize the module manager*</span></span>
- <span data-ttu-id="8cbc8-110">\***txm_module_manager_mm_initialize** _-bellek yönetimi donanımı _Initialize \*</span><span class="sxs-lookup"><span data-stu-id="8cbc8-110">***txm_module_manager_mm_initialize** _ - _Initialize the memory management hardware*</span></span>
- <span data-ttu-id="8cbc8-111">\***txm_module_manager_maximum_module_priority_set** _-bir modülde izin verilen en fazla iş parçacığı önceliği _Set.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-111">***txm_module_manager_maximum_module_priority_set** _ - _Set the maximum thread priority allowed in a module*</span></span>
- <span data-ttu-id="8cbc8-112">\***txm_module_manager_memory_fault_notify** _-bellek hatasında bir uygulama geri çağırması _Register</span><span class="sxs-lookup"><span data-stu-id="8cbc8-112">***txm_module_manager_memory_fault_notify** _ - _Register an application callback on memory fault*</span></span>
- <span data-ttu-id="8cbc8-113">\***txm_module_manager_memory_load** _-modülü bellekten _Load \*</span><span class="sxs-lookup"><span data-stu-id="8cbc8-113">***txm_module_manager_memory_load** _ - _Load the module from memory*</span></span>
- <span data-ttu-id="8cbc8-114">\***txm_module_manager_object_pool_create** _-modüller için bir nesne havuzu _Create</span><span class="sxs-lookup"><span data-stu-id="8cbc8-114">***txm_module_manager_object_pool_create** _ - _Create an object pool for modules*</span></span>
- <span data-ttu-id="8cbc8-115">\***txm_module_manager_properties_get** _-_Get modül özellikleri \*</span><span class="sxs-lookup"><span data-stu-id="8cbc8-115">***txm_module_manager_properties_get** _ - _Get module properties*</span></span>
- <span data-ttu-id="8cbc8-116">\***txm_module_manager_start** _-belirtilen modülün _Start yürütmesi \*</span><span class="sxs-lookup"><span data-stu-id="8cbc8-116">***txm_module_manager_start** _ - _Start execution of the specified module*</span></span>
- <span data-ttu-id="8cbc8-117">\***txm_module_manager_stop** _-belirtilen modülün _Stop yürütmesi \*</span><span class="sxs-lookup"><span data-stu-id="8cbc8-117">***txm_module_manager_stop** _ - _Stop execution of the specified module*</span></span>
- <span data-ttu-id="8cbc8-118">\***txm_module_manager_unload** _-modülü _Unload \*</span><span class="sxs-lookup"><span data-stu-id="8cbc8-118">***txm_module_manager_unload** _ - _Unload the module*</span></span>

---

## <a name="txm_module_manager_external_memory_enable"></a><span data-ttu-id="8cbc8-119">txm_module_manager_external_memory_enable</span><span class="sxs-lookup"><span data-stu-id="8cbc8-119">txm_module_manager_external_memory_enable</span></span>

<span data-ttu-id="8cbc8-120">Modülü paylaşılan bir bellek alanına erişmek için etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-120">Enable module to access a shared memory space.</span></span>

### <a name="prototype"></a><span data-ttu-id="8cbc8-121">Prototype</span><span class="sxs-lookup"><span data-stu-id="8cbc8-121">Prototype</span></span>

```c
UINT txm_module_manager_external_memory_enable(
     TXM_MODULE_INSTANCE *module_instance,
     VOID *start_address,
     ULONG length,
     UINT attributes);
```

### <a name="description"></a><span data-ttu-id="8cbc8-122">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8cbc8-122">Description</span></span>

<span data-ttu-id="8cbc8-123">Bu hizmet, modülün erişebileceği paylaşılan bellek bölgesi için bellek yönetimi donanım tablosunda bir giriş oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-123">This service creates an entry in the memory management hardware table for a shared memory region that the module can access.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8cbc8-124">Giriş parametreleri</span><span class="sxs-lookup"><span data-stu-id="8cbc8-124">Input parameters</span></span>

- <span data-ttu-id="8cbc8-125">**module_instance** Modülün örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-125">**module_instance** Pointer to the instance of the module.</span></span>
- <span data-ttu-id="8cbc8-126">**start_address** Paylaşılan bellek bölgesinin başlangıç adresi.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-126">**start_address** Starting address of shared memory region.</span></span>
- <span data-ttu-id="8cbc8-127">**uzunluk** Paylaşılan bellek bölgesinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-127">**length** Length of shared memory region.</span></span>
- <span data-ttu-id="8cbc8-128">**öznitelikler** Bellek bölgesinin öznitelikleri (önbellek, okuma, yazma, vb.).</span><span class="sxs-lookup"><span data-stu-id="8cbc8-128">**attributes** Attributes of memory region (cache, read, write, etc.).</span></span> <span data-ttu-id="8cbc8-129">Öznitelikler, bağlantı noktasına özeldir; bkz. öznitelik biçimi için [ek](appendix.md) .</span><span class="sxs-lookup"><span data-stu-id="8cbc8-129">Attributes are port-specific; see [appendix](appendix.md) for attributes format.</span></span>

### <a name="return-values"></a><span data-ttu-id="8cbc8-130">Dönüş değerleri</span><span class="sxs-lookup"><span data-stu-id="8cbc8-130">Return values</span></span>

- <span data-ttu-id="8cbc8-131">**TX_SUCCESS** (0x00) bellek girdisi başarıyla oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-131">**TX_SUCCESS** (0x00) Memory entry created successfully.</span></span>
- <span data-ttu-id="8cbc8-132">**TX_NOT_AVAILABLE** (0x1d) Manager başlatılmadı veya özellik kullanılamıyor.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-132">**TX_NOT_AVAILABLE** (0x1D) Manager not initialized or feature not available.</span></span>
- <span data-ttu-id="8cbc8-133">**TX_PTR_ERROR** (0x03) geçersiz modül örneği.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-133">**TX_PTR_ERROR** (0x03) Invalid module instance.</span></span>
- <span data-ttu-id="8cbc8-134">**TX_START_ERROR** (0x10) modül yüklü durumda değil.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-134">**TX_START_ERROR** (0x10) Module not in loaded state.</span></span>
- <span data-ttu-id="8cbc8-135">**TXM_MODULE_ALIGNMENT_ERROR** (0xf0) geçersiz başlangıç adresi hizalaması.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-135">**TXM_MODULE_ALIGNMENT_ERROR** (0xF0) Invalid start address alignment.</span></span>
- <span data-ttu-id="8cbc8-136">**TXM_MODULE_INVALID_PROPERTIES** (0xF3) uyumsuz Özellikler.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-136">**TXM_MODULE_INVALID_PROPERTIES** (0xF3) Incompatible properties.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8cbc8-137">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8cbc8-137">Allowed from</span></span>

<span data-ttu-id="8cbc8-138">Başlatma ve iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8cbc8-138">Initialization and threads</span></span>

### <a name="example"></a><span data-ttu-id="8cbc8-139">Örnek</span><span class="sxs-lookup"><span data-stu-id="8cbc8-139">Example</span></span>

```c
TXM_MODULE_INSTANCE my_module;

/* Initialize the module manager with 64KB of RAM starting at address 0x64010000. */
txm_module_manager_initialize((VOID *) 0x64010000, 0x10000);

/* Load the module that has its code area at address 0x080F0000. */
txm_module_manager_in_place_load(&my_module, "my module", (VOID *) 0x080F0000);

/* Create a shared memory space 256 bytes long at address 0x64005000
   with read & write, no execute, outer & inner write back cache
   attributes. Note that these attributes are port-specific. */
txm_module_manager_external_memory_enable(&my_module, (VOID*)0x64005000, 256, 0x3F);
```

---

## <a name="txm_module_manager_file_load"></a><span data-ttu-id="8cbc8-140">txm_module_manager_file_load</span><span class="sxs-lookup"><span data-stu-id="8cbc8-140">txm_module_manager_file_load</span></span>

<span data-ttu-id="8cbc8-141">Modülü FileX aracılığıyla dosyadan yükleyin.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-141">Load module from file via FileX.</span></span>

### <a name="prototype"></a><span data-ttu-id="8cbc8-142">Prototype</span><span class="sxs-lookup"><span data-stu-id="8cbc8-142">Prototype</span></span>

```c
UINT txm_module_manager_file_load(
    TXM_MODULE_INSTANCE *module_instance,
    CHAR *module_name,
    FX_MEDIA *media_ptr,
    CHAR *file_name);
```

### <a name="description"></a><span data-ttu-id="8cbc8-143">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8cbc8-143">Description</span></span>

<span data-ttu-id="8cbc8-144">Bu hizmet, belirtilen dosyada bulunan modülün ikili görüntüsünü modül bellek alanına yükler ve yürütülmek üzere hazırlar.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-144">This service loads the binary image of the module contained in the specified file into the module memory area and prepares it for execution.</span></span> <span data-ttu-id="8cbc8-145">Belirtilen medyanın zaten açık olduğu varsayılır.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-145">It is assumed that the supplied media is already opened.</span></span>

> [!NOTE]
> <span data-ttu-id="8cbc8-146">Dosyayı yüklemek için FileX sistemi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-146">The FileX system is utilized to load the file.</span></span> <span data-ttu-id="8cbc8-147">FileX erişimini etkinleştirmek için modül, modül kitaplığı, Modül Yöneticisi ve ThreadX kitaplığı (Modül Yöneticisi kaynaklarıyla birlikte), projelerde tanımlanmış **FX_FILEX_PRESENT** oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-147">In order to enable FileX access, the module, module library, Module Manager and the ThreadX library (with the Module Manager sources) must be built with **FX_FILEX_PRESENT** defined in the projects.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8cbc8-148">Giriş parametreleri</span><span class="sxs-lookup"><span data-stu-id="8cbc8-148">Input parameters</span></span>

- <span data-ttu-id="8cbc8-149">**module_instance** Modülün örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-149">**module_instance** Pointer to the instance of the module.</span></span>
- <span data-ttu-id="8cbc8-150">**module_name** Modülün adı.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-150">**module_name** Name of the module.</span></span>
- <span data-ttu-id="8cbc8-151">**media_ptr** Zaten açılmış FileX medyası işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-151">**media_ptr** Pointer to already opened FileX media.</span></span>
- <span data-ttu-id="8cbc8-152">**file_name** Modülün ikili dosyasının adı.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-152">**file_name** Name of module's binary file.</span></span>

### <a name="return-values"></a><span data-ttu-id="8cbc8-153">Dönüş değerleri</span><span class="sxs-lookup"><span data-stu-id="8cbc8-153">Return values</span></span>

- <span data-ttu-id="8cbc8-154">**TX_SUCCESS** (0x00) başarılı modül yüklemesi.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-154">**TX_SUCCESS** (0x00) Successful module load.</span></span>
- <span data-ttu-id="8cbc8-155">**TX_CALLER_ERROR** (0x13) geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-155">**TX_CALLER_ERROR** (0x13) Invalid caller.</span></span>
- <span data-ttu-id="8cbc8-156">**TX_NOT_AVAILABLE** (0x1d) Yöneticisi başlatılmadı.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-156">**TX_NOT_AVAILABLE** (0x1D) Manager not initialized.</span></span>
- <span data-ttu-id="8cbc8-157">**TX_NO_MEMORY** (0x10) modülü yüklemek için yeterli bellek yok.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-157">**TX_NO_MEMORY** (0x10) Not enough memory to load module.</span></span>
- <span data-ttu-id="8cbc8-158">**TX_NOT_DONE** (0x20) medya açık değil, dosya bulunamadı veya dosya geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-158">**TX_NOT_DONE** (0x20) Media not open, file not found or file is invalid.</span></span>
- <span data-ttu-id="8cbc8-159">**TX_PTR_ERROR** (0x03) geçersiz modül işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-159">**TX_PTR_ERROR** (0x03) Invalid module pointer.</span></span>
- <span data-ttu-id="8cbc8-160">**TXM_MODULE_ALIGNMENT_ERROR** (0xf0) geçersiz hizalama.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-160">**TXM_MODULE_ALIGNMENT_ERROR** (0xF0) Invalid alignment.</span></span>
- <span data-ttu-id="8cbc8-161">**TXM_MODULE_ALREADY_LOADED** (0xf1) modülü zaten yüklü.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-161">**TXM_MODULE_ALREADY_LOADED** (0xF1) Module already loaded.</span></span>
- <span data-ttu-id="8cbc8-162">**TXM_MODULE_INVALID** (0xF2) | Geçersiz modül girişi.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-162">**TXM_MODULE_INVALID** (0xF2) | Invalid module preamble.</span></span>
- <span data-ttu-id="8cbc8-163">**TXM_MODULE_INVALID_PROPERTIES** (0xF3) uyumsuz Özellikler.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-163">**TXM_MODULE_INVALID_PROPERTIES** (0xF3) Incompatible properties.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8cbc8-164">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8cbc8-164">Allowed from</span></span>

<span data-ttu-id="8cbc8-165">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8cbc8-165">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8cbc8-166">Örnek</span><span class="sxs-lookup"><span data-stu-id="8cbc8-166">Example</span></span>

```c
TXM_MODULE_INSTANCE my_module;

/* Initialize the module manager. */
status = txm_module_manager_initialize((VOID*)0x64010000,0x10000);

/* Load the module from a binary file. */
status = txm_module_manager_file_load(&my_module, "my module",
                                      &sdio_disk, "demo_thread_module.bin");

/* Start the module. */
status = txm_module_manager_start(&my_module);
```

### <a name="see-also"></a><span data-ttu-id="8cbc8-167">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-167">See also</span></span>

- <span data-ttu-id="8cbc8-168">txm_module_manager_in_place_load</span><span class="sxs-lookup"><span data-stu-id="8cbc8-168">txm_module_manager_in_place_load</span></span>
- <span data-ttu-id="8cbc8-169">txm_module_manager_memory_load</span><span class="sxs-lookup"><span data-stu-id="8cbc8-169">txm_module_manager_memory_load</span></span>
- <span data-ttu-id="8cbc8-170">txm_module_manager_unload</span><span class="sxs-lookup"><span data-stu-id="8cbc8-170">txm_module_manager_unload</span></span>

---

## <a name="txm_module_manager_in_place_load"></a><span data-ttu-id="8cbc8-171">txm_module_manager_in_place_load</span><span class="sxs-lookup"><span data-stu-id="8cbc8-171">txm_module_manager_in_place_load</span></span>

<span data-ttu-id="8cbc8-172">Yalnızca modül verilerini yükle, modülü mevcut konumda Yürüt.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-172">Load module data only, execute module in existing location.</span></span>

### <a name="prototype"></a><span data-ttu-id="8cbc8-173">Prototype</span><span class="sxs-lookup"><span data-stu-id="8cbc8-173">Prototype</span></span>

```c
UINT txm_module_manager_in_place_load(
    TXM_MODULE_INSTANCE *module_instance,
    CHAR *module_name,
    VOID *location);
```

### <a name="description"></a><span data-ttu-id="8cbc8-174">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8cbc8-174">Description</span></span>

<span data-ttu-id="8cbc8-175">Bu hizmet, modülün veri alanını yalnızca modül bellek alanına yükler ve yürütülmek üzere hazırlar.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-175">This service loads the module's data area only into the module memory area and prepares it for execution.</span></span> <span data-ttu-id="8cbc8-176">Modül kodu yürütme, belirtilen konumdaki modül girişi tarafından belirtilen adres uzaklığında yerinde olacaktır.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-176">Module code execution will be in-place, that is, from the address offset specified by the module preamble at the supplied location.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8cbc8-177">Giriş parametreleri</span><span class="sxs-lookup"><span data-stu-id="8cbc8-177">Input parameters</span></span>

- <span data-ttu-id="8cbc8-178">**module_instance** Modülün örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-178">**module_instance** Pointer to the instance of the module.</span></span>
- <span data-ttu-id="8cbc8-179">**module_name** Modülün adı.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-179">**module_name** Name of the module.</span></span>
- <span data-ttu-id="8cbc8-180">**konum** Modülün kod alanına yönelik işaretçi, giriş ilk.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-180">**location** Pointer to module's code area, preamble first.</span></span>

### <a name="return-values"></a><span data-ttu-id="8cbc8-181">Dönüş değerleri</span><span class="sxs-lookup"><span data-stu-id="8cbc8-181">Return values</span></span>

- <span data-ttu-id="8cbc8-182">**TX_SUCCESS** (0x00) başarılı modül yüklemesi.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-182">**TX_SUCCESS** (0x00) Successful module load.</span></span>
- <span data-ttu-id="8cbc8-183">**TX_CALLER_ERROR** (0x13) geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-183">**TX_CALLER_ERROR** (0x13) Invalid caller.</span></span>
- <span data-ttu-id="8cbc8-184">**TX_NOT_AVAILABLE** (0x1d) Yöneticisi başlatılmadı.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-184">**TX_NOT_AVAILABLE** (0x1D) Manager not initialized.</span></span>
- <span data-ttu-id="8cbc8-185">**TX_NO_MEMORY** (0x10) modülü yüklemek için yeterli bellek yok.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-185">**TX_NO_MEMORY** (0x10) Not enough memory to load module.</span></span>
- <span data-ttu-id="8cbc8-186">**TX_PTR_ERROR** (0x03) geçersiz işaretçi, modül örneği veya modül girişi.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-186">**TX_PTR_ERROR** (0x03) Invalid pointer, module instance, or module preamble.</span></span>
- <span data-ttu-id="8cbc8-187">**TXM_MODULE_ALIGNMENT_ERROR** (0xf0) geçersiz hizalama.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-187">**TXM_MODULE_ALIGNMENT_ERROR** (0xF0) Invalid alignment.</span></span>
- <span data-ttu-id="8cbc8-188">**TXM_MODULE_ALREADY_LOADED** (0xf1) modülü zaten yüklü.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-188">**TXM_MODULE_ALREADY_LOADED** (0xF1) Module already loaded.</span></span>
- <span data-ttu-id="8cbc8-189">**TXM_MODULE_INVALID** (0xF2) geçersiz modül girişi.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-189">**TXM_MODULE_INVALID** (0xF2) Invalid module preamble.</span></span>
- <span data-ttu-id="8cbc8-190">**TXM_MODULE_INVALID_PROPERTIES** (0xF3) uyumsuz Özellikler.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-190">**TXM_MODULE_INVALID_PROPERTIES** (0xF3) Incompatible properties.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8cbc8-191">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8cbc8-191">Allowed from</span></span>

<span data-ttu-id="8cbc8-192">Başlatma ve iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8cbc8-192">Initialization and threads</span></span>

### <a name="example"></a><span data-ttu-id="8cbc8-193">Örnek</span><span class="sxs-lookup"><span data-stu-id="8cbc8-193">Example</span></span>

```c
TXM_MODULE_INSTANCE my_module;

/* Initialize the module manager with 64KB of RAM starting at address 0x64010000. */
txm_module_manager_initialize((VOID *) 0x64010000, 0x10000);

/* Load the module that has its code area at address 0x080F0000. */
txm_module_manager_in_place_load(&my_module, "my module", (VOID *) 0x080F0000);

/* Start the module. */
txm_module_manager_start(&my_module);
```

### <a name="see-also"></a><span data-ttu-id="8cbc8-194">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-194">See also</span></span>

- <span data-ttu-id="8cbc8-195">txm_module_manager_file_load</span><span class="sxs-lookup"><span data-stu-id="8cbc8-195">txm_module_manager_file_load</span></span>
- <span data-ttu-id="8cbc8-196">txm_module_manager_memory_load</span><span class="sxs-lookup"><span data-stu-id="8cbc8-196">txm_module_manager_memory_load</span></span>
- <span data-ttu-id="8cbc8-197">txm_module_manager_unload</span><span class="sxs-lookup"><span data-stu-id="8cbc8-197">txm_module_manager_unload</span></span>

---

## <a name="txm_module_manager_initialize"></a><span data-ttu-id="8cbc8-198">txm_module_manager_initialize</span><span class="sxs-lookup"><span data-stu-id="8cbc8-198">txm_module_manager_initialize</span></span>

<span data-ttu-id="8cbc8-199">Modül Yöneticisini başlatın.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-199">Initialize the module manager.</span></span>

### <a name="prototype"></a><span data-ttu-id="8cbc8-200">Prototype</span><span class="sxs-lookup"><span data-stu-id="8cbc8-200">Prototype</span></span>

```c
UINT txm_module_manager_initialize(
    VOID *module_memory_start,
    ULONG module_memory_size);
```

### <a name="description"></a><span data-ttu-id="8cbc8-201">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8cbc8-201">Description</span></span>

<span data-ttu-id="8cbc8-202">Bu hizmet modül yöneticisinin iç kaynaklarını, modülleri yüklemek için kullanılan bellek alanı dahil olmak üzere başlatır.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-202">This service initializes the Module Manager's internal resources, including the memory area used for loading modules.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8cbc8-203">Giriş parametreleri</span><span class="sxs-lookup"><span data-stu-id="8cbc8-203">Input parameters</span></span>

- <span data-ttu-id="8cbc8-204">**module_memory_start** Modül belleğinin başlangıcına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-204">**module_memory_start** Pointer to the start of module memory.</span></span>
- <span data-ttu-id="8cbc8-205">**module_memory_size** Modül belleğinin bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-205">**module_memory_size** Size in bytes of the module memory.</span></span>

### <a name="return-values"></a><span data-ttu-id="8cbc8-206">Dönüş değerleri</span><span class="sxs-lookup"><span data-stu-id="8cbc8-206">Return values</span></span>

- <span data-ttu-id="8cbc8-207">**TX_SUCCESS** (0x00) başarıyla başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-207">**TX_SUCCESS** (0x00) Successful initialization.</span></span>
- <span data-ttu-id="8cbc8-208">**TX_CALLER_ERROR** (0x13) geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-208">**TX_CALLER_ERROR** (0x13) Invalid caller.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8cbc8-209">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8cbc8-209">Allowed from</span></span>

<span data-ttu-id="8cbc8-210">Başlatma ve iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8cbc8-210">Initialization and threads</span></span>

### <a name="example"></a><span data-ttu-id="8cbc8-211">Örnek</span><span class="sxs-lookup"><span data-stu-id="8cbc8-211">Example</span></span>

```c
/* Initialize the module manager with 64KB of RAM starting at
   address 0x64010000. */
txm_module_manager_initialize((VOID *) 0x64010000, 0x10000);
```

### <a name="see-also"></a><span data-ttu-id="8cbc8-212">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-212">See also</span></span>

- <span data-ttu-id="8cbc8-213">txm_module_manager_object_pool_create</span><span class="sxs-lookup"><span data-stu-id="8cbc8-213">txm_module_manager_object_pool_create</span></span>

---

## <a name="txm_module_manager_initialize_mmu"></a><span data-ttu-id="8cbc8-214">txm_module_manager_initialize_mmu</span><span class="sxs-lookup"><span data-stu-id="8cbc8-214">txm_module_manager_initialize_mmu</span></span>

<span data-ttu-id="8cbc8-215">Bellek yönetimi donanımını başlatın.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-215">Initialize the memory management hardware.</span></span>

### <a name="prototype"></a><span data-ttu-id="8cbc8-216">Prototype</span><span class="sxs-lookup"><span data-stu-id="8cbc8-216">Prototype</span></span>

```c
UINT txm_module_manager_initialize_mmu(VOID);
```

### <a name="description"></a><span data-ttu-id="8cbc8-217">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8cbc8-217">Description</span></span>

<span data-ttu-id="8cbc8-218">Bu hizmet, MMU başlatır.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-218">This service initializes the MMU.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8cbc8-219">Giriş parametreleri</span><span class="sxs-lookup"><span data-stu-id="8cbc8-219">Input parameters</span></span>

<span data-ttu-id="8cbc8-220">yok</span><span class="sxs-lookup"><span data-stu-id="8cbc8-220">none</span></span>

### <a name="return-values"></a><span data-ttu-id="8cbc8-221">Dönüş değerleri</span><span class="sxs-lookup"><span data-stu-id="8cbc8-221">Return values</span></span>

- <span data-ttu-id="8cbc8-222">**TX_SUCCESS** (0x00) başarıyla başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-222">**TX_SUCCESS** (0x00) Successful initialization.</span></span>
- <span data-ttu-id="8cbc8-223">**TX_CALLER_ERROR** (0x13) geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-223">**TX_CALLER_ERROR** (0x13) Invalid caller.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8cbc8-224">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8cbc8-224">Allowed from</span></span>

<span data-ttu-id="8cbc8-225">Başlatma ve Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8cbc8-225">Initialization and Threads</span></span>

### <a name="example"></a><span data-ttu-id="8cbc8-226">Örnek</span><span class="sxs-lookup"><span data-stu-id="8cbc8-226">Example</span></span>

```c
/* Initialize the module manager with 64KB of RAM starting at address 0x64010000. */
txm_module_manager_initialize((VOID *) 0x64010000, 0x10000);

/* Initialize the MMU. */
txm_module_manager_initialize_mmu();
```

---

## <a name="txm_module_manager_maximum_module_priority_set"></a><span data-ttu-id="8cbc8-227">txm_module_manager_maximum_module_priority_set</span><span class="sxs-lookup"><span data-stu-id="8cbc8-227">txm_module_manager_maximum_module_priority_set</span></span>

<span data-ttu-id="8cbc8-228">Bir modülde izin verilen en fazla iş parçacığı önceliğini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-228">Set the maximum thread priority allowed in a module.</span></span>

### <a name="prototype"></a><span data-ttu-id="8cbc8-229">Prototype</span><span class="sxs-lookup"><span data-stu-id="8cbc8-229">Prototype</span></span>

```c
UINT txm_module_manager_maximum_module_priority_set(
         TXM_MODULE_INSTANCE *module_instance,
         UINT priority);
```

### <a name="description"></a><span data-ttu-id="8cbc8-230">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8cbc8-230">Description</span></span>

<span data-ttu-id="8cbc8-231">Bu hizmet, bir modülde izin verilen en fazla iş parçacığı önceliğini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-231">This service sets the maximum thread priority allowed in a module.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8cbc8-232">Giriş parametreleri</span><span class="sxs-lookup"><span data-stu-id="8cbc8-232">Input parameters</span></span>

- <span data-ttu-id="8cbc8-233">**module_instance** Modülün örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-233">**module_instance** Pointer to the instance of the module.</span></span>
- <span data-ttu-id="8cbc8-234">**Öncelik** En fazla iş parçacığı önceliği.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-234">**priority** Maximum thread priority.</span></span>

### <a name="return-values"></a><span data-ttu-id="8cbc8-235">Dönüş değerleri</span><span class="sxs-lookup"><span data-stu-id="8cbc8-235">Return values</span></span>

- <span data-ttu-id="8cbc8-236">**TX_SUCCESS** (0x00) başarıyla başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-236">**TX_SUCCESS** (0x00) Successful initialization.</span></span>
- <span data-ttu-id="8cbc8-237">**TX_NOT_AVAILABLE** (0x1d) Yöneticisi başlatılmadı.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-237">**TX_NOT_AVAILABLE** (0x1D) Manager not initialized.</span></span>
- <span data-ttu-id="8cbc8-238">**TX_PTR_ERROR** (0x03) geçersiz modül örneği.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-238">**TX_PTR_ERROR** (0x03) Invalid module instance.</span></span>
- <span data-ttu-id="8cbc8-239">**TX_START_ERROR** (0x10) modül yüklü durumda değil.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-239">**TX_START_ERROR** (0x10) Module not in loaded state.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8cbc8-240">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8cbc8-240">Allowed from</span></span>

<span data-ttu-id="8cbc8-241">Başlatma ve iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8cbc8-241">Initialization and threads</span></span>

### <a name="example"></a><span data-ttu-id="8cbc8-242">Örnek</span><span class="sxs-lookup"><span data-stu-id="8cbc8-242">Example</span></span>

```c
/* Load the module that has its code area at address 0x080F0000. */
txm_module_manager_in_place_load(&my_module, "my module", (VOID *) 0x080F0000);

/* Set the maximum thread priority in my_module to 5. */
txm_module_manager_maximum_module_priority_set(&my_module, 5);
```

---

## <a name="txm_module_manager_memory_fault_notify"></a><span data-ttu-id="8cbc8-243">txm_module_manager_memory_fault_notify</span><span class="sxs-lookup"><span data-stu-id="8cbc8-243">txm_module_manager_memory_fault_notify</span></span>

<span data-ttu-id="8cbc8-244">Bellek hatasında bir uygulama geri araması kaydedin.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-244">Register an application callback on memory fault.</span></span>

### <a name="prototype"></a><span data-ttu-id="8cbc8-245">Prototype</span><span class="sxs-lookup"><span data-stu-id="8cbc8-245">Prototype</span></span>

```c
UINT txm_module_manager_memory_fault_notify(
     VOID (*notify_function)(TX_THREAD *, MODULE_INSTANCE *));
```

### <a name="description"></a><span data-ttu-id="8cbc8-246">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8cbc8-246">Description</span></span>

<span data-ttu-id="8cbc8-247">Bu hizmet, belirtilen uygulama belleği hata bildirimi geri arama işlevini Modül Yöneticisi ile kaydeder.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-247">This service registers the specified application memory fault notification callback function with the Module Manager.</span></span> <span data-ttu-id="8cbc8-248">Bir bellek hatası oluşursa, bu işlev sorunlu iş parçacığına ve soruna neden olan iş parçacığına karşılık gelen modül örneğine yönelik bir işaretçi ile çağırılır.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-248">If a memory fault occurs, this function is called with a pointer to the offending thread and the module instance corresponding to the offending thread.</span></span> <span data-ttu-id="8cbc8-249">Modül Yöneticisi işlemi, sorunlu iş parçacığını otomatik olarak sonlandırır, ancak modüldeki diğer iş parçacıklarını bırakır.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-249">The Module Manager processing automatically terminates the offending thread, but leaves any other threads in the module untouched.</span></span> <span data-ttu-id="8cbc8-250">Bellek hatası ile ilişkili modülle ne yapacağına karar vermek uygulamaya kadar yapılır.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-250">It is up to the application to decide what to do with the module associated with the memory fault.</span></span>

<span data-ttu-id="8cbc8-251">Bellek hatası hakkında belirli bilgiler için lütfen iç **_txm_module_manager_memory_fault_info** yapısına bakın.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-251">Please see the internal **_txm_module_manager_memory_fault_info** struct for specific information on the memory fault itself.</span></span>

> [!NOTE]
> <span data-ttu-id="8cbc8-252">Bellek hatası bildirimi geri çağırma işlevi doğrudan bellek hatası özel durumuyla yürütülür, bu nedenle yalnızca kesme hizmeti yordamlarından Izin verilen ThreadX API 'Leri çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-252">The memory fault notification callback function is executed directly from the memory fault exception, so only ThreadX APIs Allowed from interrupt service routines can be called.</span></span> <span data-ttu-id="8cbc8-253">Bu nedenle, soruna neden olan modülün durdurulması ve kaldırılması için, uygulama bildirimi geri çağrısının bir uygulama görevine bir sinyal gönderilmesi gerekir, böylece modülün durdurulup bellekten kaldırılabilir.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-253">Thus, in order to stop and unload the offending module, the application notification callback must send a signal to an application task so that the module can be stopped and unloaded.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8cbc8-254">Giriş parametreleri</span><span class="sxs-lookup"><span data-stu-id="8cbc8-254">Input parameters</span></span>

- <span data-ttu-id="8cbc8-255">**notify_function** Uygulamanın bellek hatası bildirimi geri çağırması için işlev işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-255">**notify_function** Function pointer to the application's memory fault notification callback.</span></span> <span data-ttu-id="8cbc8-256">NULL değer sağlama, bellek hata bildirimini devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-256">Supplying a NULL value disables the memory fault notification.</span></span>

### <a name="return-values"></a><span data-ttu-id="8cbc8-257">Dönüş değerleri</span><span class="sxs-lookup"><span data-stu-id="8cbc8-257">Return values</span></span>

- <span data-ttu-id="8cbc8-258">**TX_SUCCESS** (0x00) başarılı bildirim işlevi kaydı.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-258">**TX_SUCCESS** (0x00) Successful notification function registration.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8cbc8-259">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8cbc8-259">Allowed from</span></span>

<span data-ttu-id="8cbc8-260">Başlatma ve iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8cbc8-260">Initialization and threads</span></span>

### <a name="example"></a><span data-ttu-id="8cbc8-261">Örnek</span><span class="sxs-lookup"><span data-stu-id="8cbc8-261">Example</span></span>

```c
/* Register a memory fault callback. */
txm_module_manager_memory_fault_notify(my_memory_fault_handler);
```

---

## <a name="txm_module_manager_memory_load"></a><span data-ttu-id="8cbc8-262">txm_module_manager_memory_load</span><span class="sxs-lookup"><span data-stu-id="8cbc8-262">txm_module_manager_memory_load</span></span>

<span data-ttu-id="8cbc8-263">Modülü bellekten yükleyin.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-263">Load module from memory.</span></span>

### <a name="prototype"></a><span data-ttu-id="8cbc8-264">Prototype</span><span class="sxs-lookup"><span data-stu-id="8cbc8-264">Prototype</span></span>

```c
UINT txm_module_manager_memory_load (
    TXM_MODULE_INSTANCE *module_instance,
    CHAR *module_name,
    VOID *location);
```

### <a name="description"></a><span data-ttu-id="8cbc8-265">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8cbc8-265">Description</span></span>

<span data-ttu-id="8cbc8-266">Bu hizmet, modülün kodunu ve veri alanını ***txm_module_manager_initialize*** tarafından ayarlanan modül bellek alanına yükler ve yürütülmek üzere hazırlar.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-266">This service loads the module's code and data area into the module memory area set up by ***txm_module_manager_initialize*** and prepares it for execution.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8cbc8-267">Giriş parametreleri</span><span class="sxs-lookup"><span data-stu-id="8cbc8-267">Input parameters</span></span>

- <span data-ttu-id="8cbc8-268">**module_instance** Modülün örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-268">**module_instance** Pointer to the instance of the module.</span></span>
- <span data-ttu-id="8cbc8-269">**module_name** Modülün adı.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-269">**module_name** Name of the module.</span></span>
- <span data-ttu-id="8cbc8-270">**konum** Modülün kod alanına yönelik işaretçi, giriş ilk.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-270">**location** Pointer to module's code area, preamble first.</span></span>

### <a name="return-values"></a><span data-ttu-id="8cbc8-271">Dönüş değerleri</span><span class="sxs-lookup"><span data-stu-id="8cbc8-271">Return values</span></span>

- <span data-ttu-id="8cbc8-272">**TX_SUCCESS** (0x00) başarılı modül yüklemesi.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-272">**TX_SUCCESS** (0x00) Successful module load.</span></span>
- <span data-ttu-id="8cbc8-273">**TX_CALLER_ERROR** (0x13) geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-273">**TX_CALLER_ERROR** (0x13) Invalid caller.</span></span>
- <span data-ttu-id="8cbc8-274">**TX_NOT_AVAILABLE** (0x1d) Yöneticisi başlatılmadı.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-274">**TX_NOT_AVAILABLE** (0x1D) Manager not initialized.</span></span>
- <span data-ttu-id="8cbc8-275">**TX_NO_MEMORY** (0x10) modülü yüklemek için yeterli bellek yok.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-275">**TX_NO_MEMORY** (0x10) Not enough memory to load module.</span></span>
- <span data-ttu-id="8cbc8-276">**TX_PTR_ERROR** (0x03) geçersiz işaretçi, modül örneği veya modül girişi.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-276">**TX_PTR_ERROR** (0x03) Invalid pointer, module instance, or module preamble.</span></span>
- <span data-ttu-id="8cbc8-277">**TXM_MODULE_ALIGNMENT_ERROR** (0xf0) geçersiz hizalama.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-277">**TXM_MODULE_ALIGNMENT_ERROR** (0xF0) Invalid alignment.</span></span>
- <span data-ttu-id="8cbc8-278">**TXM_MODULE_ALREADY_LOADED** (0xf1) modülü zaten yüklü.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-278">**TXM_MODULE_ALREADY_LOADED** (0xF1) Module already loaded.</span></span>
- <span data-ttu-id="8cbc8-279">**TXM_MODULE_INVALID** (0xF2) geçersiz modül girişi.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-279">**TXM_MODULE_INVALID** (0xF2) Invalid module preamble.</span></span>
- <span data-ttu-id="8cbc8-280">**TXM_MODULE_INVALID_PROPERTIES** (0xF3) uyumsuz Özellikler.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-280">**TXM_MODULE_INVALID_PROPERTIES** (0xF3) Incompatible properties.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8cbc8-281">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8cbc8-281">Allowed from</span></span>

<span data-ttu-id="8cbc8-282">Başlatma ve iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8cbc8-282">Initialization and threads</span></span>

### <a name="example"></a><span data-ttu-id="8cbc8-283">Örnek</span><span class="sxs-lookup"><span data-stu-id="8cbc8-283">Example</span></span>

```c
TXM_MODULE_INSTANCE     my_module;

/* Initialize the module manager with 64KB of RAM starting at address 0x64010000. */
txm_module_manager_initialize((VOID *) 0x64010000, 0x10000);

/* Load the module that has its code area at address 0x080F0000. */
 txm_module_manager_memory_load(&my_module, "my module", (VOID *) 0x080F0000);
```

### <a name="see-also"></a><span data-ttu-id="8cbc8-284">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-284">See also</span></span>

- <span data-ttu-id="8cbc8-285">txm_module_manager_file_load</span><span class="sxs-lookup"><span data-stu-id="8cbc8-285">txm_module_manager_file_load</span></span>
- <span data-ttu-id="8cbc8-286">txm_module_manager_in_place_load</span><span class="sxs-lookup"><span data-stu-id="8cbc8-286">txm_module_manager_in_place_load</span></span>
- <span data-ttu-id="8cbc8-287">txm_module_manager_unload</span><span class="sxs-lookup"><span data-stu-id="8cbc8-287">txm_module_manager_unload</span></span>

---

## <a name="txm_module_manager_object_pool_create"></a><span data-ttu-id="8cbc8-288">txm_module_manager_object_pool_create</span><span class="sxs-lookup"><span data-stu-id="8cbc8-288">txm_module_manager_object_pool_create</span></span>

<span data-ttu-id="8cbc8-289">Modüller için bir nesne havuzu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-289">Create an object pool for modules.</span></span>

### <a name="prototype"></a><span data-ttu-id="8cbc8-290">Prototype</span><span class="sxs-lookup"><span data-stu-id="8cbc8-290">Prototype</span></span>

```c
UINT txm_module_manager_object_pool_create(
    VOID *pool_memory_start,
    ULONG pool_memory_size);
```

### <a name="description"></a><span data-ttu-id="8cbc8-291">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8cbc8-291">Description</span></span>

<span data-ttu-id="8cbc8-292">Bu hizmet, modüllerin ThreadX/NetX nesneleri ayırabilecek bir modül Yöneticisi nesne bellek havuzu oluşturur ve bu sayede sistem nesnesini modülün bellek alanından ayırır.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-292">This service creates a Module Manager object memory pool that the modules can allocate ThreadX/NetX objects from, thereby keeping the system object out of the module's memory area.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8cbc8-293">Giriş parametreleri</span><span class="sxs-lookup"><span data-stu-id="8cbc8-293">Input parameters</span></span>

- <span data-ttu-id="8cbc8-294">**pool_memory_start** Nesne belleğinin başlangıcına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-294">**pool_memory_start** Pointer to the start of object memory.</span></span>
- <span data-ttu-id="8cbc8-295">**pool_memory_size** Nesne bellek havuzunun bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-295">**pool_memory_size** Size in bytes of the object memory pool.</span></span>

### <a name="return-values"></a><span data-ttu-id="8cbc8-296">Dönüş değerleri</span><span class="sxs-lookup"><span data-stu-id="8cbc8-296">Return values</span></span>

- <span data-ttu-id="8cbc8-297">**TX_SUCCESS** (0x00) başarıyla başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-297">**TX_SUCCESS** (0x00) Successful initialization.</span></span>
- <span data-ttu-id="8cbc8-298">**TX_CALLER_ERROR** (0x13) geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-298">**TX_CALLER_ERROR** (0x13) Invalid caller.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8cbc8-299">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8cbc8-299">Allowed from</span></span>

<span data-ttu-id="8cbc8-300">Başlatma ve iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8cbc8-300">Initialization and threads</span></span>

### <a name="example"></a><span data-ttu-id="8cbc8-301">Örnek</span><span class="sxs-lookup"><span data-stu-id="8cbc8-301">Example</span></span>

```c
TXM_MODULE_INSTANCE my_module;

/* Initialize the module manager with 64KB of RAM starting at address 0x64010000. */
txm_module_manager_initialize((VOID *) 0x64010000, 0x10000);

/* Create an object memory pool in the next 64KB of memory. */
txm_module_manager_object_pool_create((VOID *) 0x64020000, 0x10000);
```

### <a name="see-also"></a><span data-ttu-id="8cbc8-302">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-302">See also</span></span>

- <span data-ttu-id="8cbc8-303">txm_module_manager_initialize</span><span class="sxs-lookup"><span data-stu-id="8cbc8-303">txm_module_manager_initialize</span></span>

---

## <a name="txm_module_manager_properties_get"></a><span data-ttu-id="8cbc8-304">txm_module_manager_properties_get</span><span class="sxs-lookup"><span data-stu-id="8cbc8-304">txm_module_manager_properties_get</span></span>

<span data-ttu-id="8cbc8-305">Modül özelliklerini al.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-305">Get module properties.</span></span>

### <a name="prototype"></a><span data-ttu-id="8cbc8-306">Prototype</span><span class="sxs-lookup"><span data-stu-id="8cbc8-306">Prototype</span></span>

```c
UINT txm_module_manager_properties_get(
    TXM_MODULE_INSTANCE *module_instance,
    ULONG *module_properties_ptr);
```

### <a name="description"></a><span data-ttu-id="8cbc8-307">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8cbc8-307">Description</span></span>

<span data-ttu-id="8cbc8-308">Bu hizmet, bir modülün (giriş bölümünde belirtilen) özellikleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-308">This service returns the properties (specified in the preamble) of a module.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8cbc8-309">Giriş parametreleri</span><span class="sxs-lookup"><span data-stu-id="8cbc8-309">Input parameters</span></span>

- <span data-ttu-id="8cbc8-310">**module_instance** Modül örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-310">**module_instance** Pointer to the module instance.</span></span>
- <span data-ttu-id="8cbc8-311">**module_properties_ptr** Modülün özellikleri için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-311">**module_properties_ptr** Pointer to destination for module's properties.</span></span>

### <a name="return-values"></a><span data-ttu-id="8cbc8-312">Dönüş değerleri</span><span class="sxs-lookup"><span data-stu-id="8cbc8-312">Return values</span></span>

- <span data-ttu-id="8cbc8-313">**TX_SUCCESS** (0x00) başarıyla başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-313">**TX_SUCCESS** (0x00) Successful initialization.</span></span>
- <span data-ttu-id="8cbc8-314">**TX_PTR_ERROR** (0x03) geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-314">**TX_PTR_ERROR** (0x03) Invalid pointer.</span></span>
- <span data-ttu-id="8cbc8-315">**TX_CALLER_ERROR** (0x13) geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-315">**TX_CALLER_ERROR** (0x13) Invalid caller.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8cbc8-316">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8cbc8-316">Allowed from</span></span>

<span data-ttu-id="8cbc8-317">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8cbc8-317">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8cbc8-318">Örnek</span><span class="sxs-lookup"><span data-stu-id="8cbc8-318">Example</span></span>

```c
TXM_MODULE_INSTANCE     my_module;
ULONG                   module_properties;

/* Initialize the module manager with 64KB of RAM starting at address 0x64010000. */
txm_module_manager_initialize((VOID *) 0x64010000, 0x10000);

/* Create an object memory pool in the next 64KB of memory. */
txm_module_manager_object_pool_create((VOID *) 0x64020000, 0x10000);

/* Load the module that has its code area at address 0x080F0000. */
txm_module_manager_in_place_load(&my_module, "my module", (VOID *) 0x080F0000);

/* Get module properties. */
txm_module_manager_properties_get(&my_module, &module_properties);
```

---

## <a name="txm_module_manager_start"></a><span data-ttu-id="8cbc8-319">txm_module_manager_start</span><span class="sxs-lookup"><span data-stu-id="8cbc8-319">txm_module_manager_start</span></span>

<span data-ttu-id="8cbc8-320">Modülün yürütülmesini başlatın.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-320">Start execution of the module.</span></span>

### <a name="prototype"></a><span data-ttu-id="8cbc8-321">Prototype</span><span class="sxs-lookup"><span data-stu-id="8cbc8-321">Prototype</span></span>

```c
UINT txm_module_manager_start(TXM_MODULE_INSTANCE *module_instance);
```

### <a name="description"></a><span data-ttu-id="8cbc8-322">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8cbc8-322">Description</span></span>

<span data-ttu-id="8cbc8-323">Bu hizmet belirtilen, zaten yüklü olan modülün yürütülmesini başlatır.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-323">This service starts execution of the specified, already loaded module.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8cbc8-324">Giriş parametreleri</span><span class="sxs-lookup"><span data-stu-id="8cbc8-324">Input parameters</span></span>

- <span data-ttu-id="8cbc8-325">**module_instance** Daha önce yüklenmiş modül örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-325">**module_instance** Pointer to previously loaded module instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="8cbc8-326">Dönüş değerleri</span><span class="sxs-lookup"><span data-stu-id="8cbc8-326">Return values</span></span>

- <span data-ttu-id="8cbc8-327">**TX_SUCCESS** (0x00) başarılı modül başladı.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-327">**TX_SUCCESS** (0x00) Successful module start.</span></span>
- <span data-ttu-id="8cbc8-328">**TX_CALLER_ERROR** (0x13) geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-328">**TX_CALLER_ERROR** (0x13) Invalid caller.</span></span>
- <span data-ttu-id="8cbc8-329">**TX_NOT_AVAILABLE** (0x1d) Yöneticisi başlatılmadı.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-329">**TX_NOT_AVAILABLE** (0x1D) Manager not initialized.</span></span>
- <span data-ttu-id="8cbc8-330">**TX_PTR_ERROR** (0x03) geçersiz işaretçi veya modül örneği.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-330">**TX_PTR_ERROR** (0x03) Invalid pointer or module instance.</span></span>
- <span data-ttu-id="8cbc8-331">**TX_START_ERROR** (0x10) modülü zaten başlatılmış.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-331">**TX_START_ERROR** (0x10) Module already started.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8cbc8-332">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8cbc8-332">Allowed from</span></span>

<span data-ttu-id="8cbc8-333">Başlatma ve iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8cbc8-333">Initialization and threads</span></span>

### <a name="example"></a><span data-ttu-id="8cbc8-334">Örnek</span><span class="sxs-lookup"><span data-stu-id="8cbc8-334">Example</span></span>

```c
/* Start the module. */
txm_module_manager_start(&my_module);

/* Let the module run for a while. */
tx_thread_sleep(2000);

/* Stop the module. */
txm_module_manager_stop(&my_module);

/* Unload the module. */
txm_module_manager_unload(&my_module);
```

### <a name="see-also"></a><span data-ttu-id="8cbc8-335">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-335">See also</span></span>

- <span data-ttu-id="8cbc8-336">txm_module_manager_stop</span><span class="sxs-lookup"><span data-stu-id="8cbc8-336">txm_module_manager_stop</span></span>

---

## <a name="txm_module_manager_stop"></a><span data-ttu-id="8cbc8-337">txm_module_manager_stop</span><span class="sxs-lookup"><span data-stu-id="8cbc8-337">txm_module_manager_stop</span></span>

<span data-ttu-id="8cbc8-338">Modülün yürütülmesini durdurun.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-338">Stop execution of the module.</span></span>

### <a name="prototype"></a><span data-ttu-id="8cbc8-339">Prototype</span><span class="sxs-lookup"><span data-stu-id="8cbc8-339">Prototype</span></span>

```c
UINT txm_module_manager_stop(TXM_MODULE_INSTANCE *module_instance);
```

### <a name="description"></a><span data-ttu-id="8cbc8-340">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8cbc8-340">Description</span></span>

<span data-ttu-id="8cbc8-341">Bu hizmet daha önce yüklenmiş ve başlatılmış bir modülü durduruyor.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-341">This service stops a module that was previously loaded and started.</span></span> <span data-ttu-id="8cbc8-342">Modül durdurulduğunda modülün isteğe bağlı durdurma iş parçacığını yürütme, tüm iş parçacıklarını sonlandırma ve modülle ilişkili tüm kaynakları silme dahildir.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-342">Stopping a module includes executing the module's optional stop thread, terminating all threads, and deleting all resources associated with the module.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8cbc8-343">Giriş parametreleri</span><span class="sxs-lookup"><span data-stu-id="8cbc8-343">Input parameters</span></span>

- <span data-ttu-id="8cbc8-344">**module_instance** Modül örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-344">**module_instance** Pointer to module instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="8cbc8-345">Dönüş değerleri</span><span class="sxs-lookup"><span data-stu-id="8cbc8-345">Return values</span></span>

- <span data-ttu-id="8cbc8-346">**TX_SUCCESS** (0x00) başarılı modül durdu.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-346">**TX_SUCCESS** (0x00) Successful module stop.</span></span>
- <span data-ttu-id="8cbc8-347">**TX_CALLER_ERROR** (0x13) geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-347">**TX_CALLER_ERROR** (0x13) Invalid caller.</span></span>
- <span data-ttu-id="8cbc8-348">**TX_NOT_AVAILABLE** (0x1d) Yöneticisi başlatılmadı.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-348">**TX_NOT_AVAILABLE** (0x1D) Manager not initialized.</span></span>
- <span data-ttu-id="8cbc8-349">**TX_PTR_ERROR** (0x03) geçersiz işaretçi veya modül örneği.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-349">**TX_PTR_ERROR** (0x03) Invalid pointer or module instance.</span></span>
- <span data-ttu-id="8cbc8-350">**TX_START_ERROR** (0x10) modül başlatılmadı.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-350">**TX_START_ERROR** (0x10) Module not started.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8cbc8-351">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8cbc8-351">Allowed from</span></span>

<span data-ttu-id="8cbc8-352">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8cbc8-352">Threads</span></span>

### <a name="example"></a><span data-ttu-id="8cbc8-353">Örnek</span><span class="sxs-lookup"><span data-stu-id="8cbc8-353">Example</span></span>

```c
/* Start the module. */
txm_module_manager_start(&my_module);

/* Let the module run for a while. */
tx_thread_sleep(20000);

/* Stop the module. */
txm_module_manager_stop(&my_module);

/* Unload the module. */
txm_module_manager_unload(&my_module);
```

### <a name="see-also"></a><span data-ttu-id="8cbc8-354">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-354">See also</span></span>

- <span data-ttu-id="8cbc8-355">txm_module_manager_start</span><span class="sxs-lookup"><span data-stu-id="8cbc8-355">txm_module_manager_start</span></span>

---

## <a name="txm_module_manager_unload"></a><span data-ttu-id="8cbc8-356">txm_module_manager_unload</span><span class="sxs-lookup"><span data-stu-id="8cbc8-356">txm_module_manager_unload</span></span>

<span data-ttu-id="8cbc8-357">Modülü kaldırın.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-357">Unload the module.</span></span>

### <a name="prototype"></a><span data-ttu-id="8cbc8-358">Prototype</span><span class="sxs-lookup"><span data-stu-id="8cbc8-358">Prototype</span></span>

```c
UINT txm_module_manager_unload(TXM_MODULE_INSTANCE *module_instance);
```

### <a name="description"></a><span data-ttu-id="8cbc8-359">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8cbc8-359">Description</span></span>

<span data-ttu-id="8cbc8-360">Bu hizmet, daha önce yüklenmiş ve durdurulmuş modülünü kaldırır ve tüm ilişkili modül bellek kaynaklarını serbest bırakır.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-360">This service unloads the previously loaded and stopped module, freeing all the associated module memory resources.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8cbc8-361">Giriş parametreleri</span><span class="sxs-lookup"><span data-stu-id="8cbc8-361">Input parameters</span></span>

- <span data-ttu-id="8cbc8-362">**module_instance** Modülün örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-362">**module_instance** Pointer to the instance of the module.</span></span>

### <a name="return-values"></a><span data-ttu-id="8cbc8-363">Dönüş değerleri</span><span class="sxs-lookup"><span data-stu-id="8cbc8-363">Return values</span></span>

- <span data-ttu-id="8cbc8-364">**TX_SUCCESS** 0x00) başarılı modül yüklemesi.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-364">**TX_SUCCESS** 0x00) Successful module unload.</span></span>
- <span data-ttu-id="8cbc8-365">**TX_CALLER_ERROR** (0x13) geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-365">**TX_CALLER_ERROR** (0x13) Invalid caller.</span></span>
- <span data-ttu-id="8cbc8-366">**TX_NOT_AVAILABLE** (0x1d) Yöneticisi başlatılmadı.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-366">**TX_NOT_AVAILABLE** (0x1D) Manager not initialized.</span></span>
- <span data-ttu-id="8cbc8-367">**TX_NOT_DONE** (0x20) geçersiz modül veya modül durdurulmadı.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-367">**TX_NOT_DONE** (0x20) Invalid module or module not stopped.</span></span>
- <span data-ttu-id="8cbc8-368">**TX_PTR_ERROR** (0x03) geçersiz işaretçi veya modül örneği.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-368">**TX_PTR_ERROR** (0x03) Invalid pointer or module instance.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="8cbc8-369">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="8cbc8-369">Allowed from</span></span>

<span data-ttu-id="8cbc8-370">Başlatma ve iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="8cbc8-370">Initialization and threads</span></span>

### <a name="example"></a><span data-ttu-id="8cbc8-371">Örnek</span><span class="sxs-lookup"><span data-stu-id="8cbc8-371">Example</span></span>

```c
/* Stop the module. */
txm_module_manager_stop(&my_module);

/* Unload the module. */
status = txm_module_manager_unload(&my_module);
```

### <a name="see-also"></a><span data-ttu-id="8cbc8-372">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="8cbc8-372">See also</span></span>

- <span data-ttu-id="8cbc8-373">txm_module_manager_file_load</span><span class="sxs-lookup"><span data-stu-id="8cbc8-373">txm_module_manager_file_load</span></span>
- <span data-ttu-id="8cbc8-374">txm_module_manager_in_place_load</span><span class="sxs-lookup"><span data-stu-id="8cbc8-374">txm_module_manager_in_place_load</span></span>
- <span data-ttu-id="8cbc8-375">txm_module_manager_memory_load</span><span class="sxs-lookup"><span data-stu-id="8cbc8-375">txm_module_manager_memory_load</span></span>
- <span data-ttu-id="8cbc8-376">txm_module_manager_stop</span><span class="sxs-lookup"><span data-stu-id="8cbc8-376">txm_module_manager_stop</span></span>
