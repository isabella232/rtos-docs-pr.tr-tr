---
title: Bölüm 3-Modül Yöneticisi gereksinimleri
description: Bu makale, ThreadX modül yöneticisini oluşturmak için gereken adımların bir açıklamasıdır.
author: philmea
ms.author: philmea
ms.date: 07/15/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: e8ea1a05096b5975de203648fddfb19c1a6105e0
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826596"
---
# <a name="chapter-3---module-manager-requirements"></a><span data-ttu-id="af1a6-103">Bölüm 3-Modül Yöneticisi gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="af1a6-103">Chapter 3 - Module Manager requirements</span></span>

<span data-ttu-id="af1a6-104">ThreadX Modül Yöneticisi, ThreadX RTOS ile birlikte uygulamanın yerleşik bölümünde bulunur.</span><span class="sxs-lookup"><span data-stu-id="af1a6-104">The ThreadX Module Manager resides in the resident portion of the application along with the ThreadX RTOS.</span></span> <span data-ttu-id="af1a6-105">Modülün başlatılmasının yanı sıra ThreadX API hizmetleri için tüm modül isteklerini alan ve gönderen bir sorumludur.</span><span class="sxs-lookup"><span data-stu-id="af1a6-105">It is responsible for starting the module as well as fielding and dispatching all module requests for ThreadX API services.</span></span>

> [!NOTE]
> <span data-ttu-id="af1a6-106">ThreadX modül **Yöneticisi** kaynak dosyaları (C ve derleme), threadx kitaplığı projesine "**TX**" eklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="af1a6-106">The ThreadX Module **Manager** source files (C and assembly) should be added to the ThreadX library project "**tx**".</span></span>

<span data-ttu-id="af1a6-107">ThreadX modül yöneticisini oluşturmak için aşağıdaki adımlar gereklidir (her adım aşağıda daha ayrıntılı olarak açıklanmıştır).</span><span class="sxs-lookup"><span data-stu-id="af1a6-107">The following steps are required for building the ThreadX Module Manager (each step is described in greater detail below).</span></span>

1. <span data-ttu-id="af1a6-108">**TX_THREAD** denetim bloğu modül bilgilerini içerecek şekilde genişletilmelidir.</span><span class="sxs-lookup"><span data-stu-id="af1a6-108">The **TX_THREAD** control block must be extended to include module information.</span></span> <span data-ttu-id="af1a6-109">Bunu yapmanın en kolay yolu, **_tx_port. h_\*_ dosyasındaki**\* **TX_THREAD_EXTENSION_2** tanımını **_txm_module_port. h_** içinde bulunan _ TX_THREAD_EXTENSION_2 değiştirecek şekilde kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="af1a6-109">The easiest way to accomplish this is to replace the definition of **TX_THREAD_EXTENSION_2** in the **_tx_port.h_*_ file with the _\* TX_THREAD_EXTENSION_2*\* found in **_txm_module_port.h_**.</span></span> <span data-ttu-id="af1a6-110">Bkz. bağlantı noktasına özgü uzantılar için [ek](appendix.md) .</span><span class="sxs-lookup"><span data-stu-id="af1a6-110">See [appendix](appendix.md) for port-specific extensions.</span></span>

<span data-ttu-id="af1a6-111">Örnek uzantı:</span><span class="sxs-lookup"><span data-stu-id="af1a6-111">Example extension:</span></span>

   ```c
   #define TX_THREAD_EXTENSION_2                     \
       VOID      tx_thread_module_instance_ptr;      \
       VOID      tx_thread_module_entry_info_ptr;    \
       ULONG     tx_thread_module_current_user_mode; \
       ULONG     tx_thread_module_user_mode;         \
       VOID     *tx_thread_module_kernel_stack_start;\
       VOID     *tx_thread_module_kernel_stack_end;  \
       ULONG     tx_thread_module_kernel_stack_size; \
       VOID     *tx_thread_module_stack_ptr;         \
       VOID     *tx_thread_module_stack_start;       \
       VOID     *tx_thread_module_stack_end;         \
       ULONG     tx_thread_module_stack_size;        \
       VOID     *tx_thread_module_reserved;
   ```

   <span data-ttu-id="af1a6-112">Aşağıdaki uzantıların ***tx_port. h*** içinde tanımlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="af1a6-112">The following extensions must be defined in ***tx_port.h***.</span></span>

   ```c
   #define TX_EVENT_FLAGS_GROUP_EXTENSION  VOID    *tx_event_flags_group_module_instance; \
        VOID   (*tx_event_flags_group_set_module_notify)(struct TX_EVENT_FLAGS_GROUP_STRUCT *group_ptr);

   #define TX_QUEUE_EXTENSION              VOID    *tx_queue_module_instance; \
        VOID   (*tx_queue_send_module_notify)(struct TX_QUEUE_STRUCT *queue_ptr);

   #define TX_SEMAPHORE_EXTENSION          VOID    *tx_semaphore_module_instance; \
        VOID   (*tx_semaphore_put_module_notify)(struct TX_SEMAPHORE_STRUCT *semaphore_ptr);

   #define TX_TIMER_EXTENSION              VOID    *tx_timer_module_instance; \
        VOID   (*tx_timer_module_expiration_function)(ULONG id);
   ```

2. <span data-ttu-id="af1a6-113">Tüm ***txm_module_manager_ \**** C ve derleme dosyalarını threadx kitaplığı proje **_TX_** öğesine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="af1a6-113">Add all the ***txm_module_manager_\**** C and assembly files to the ThreadX library project **_tx_**.</span></span>
3. <span data-ttu-id="af1a6-114">Tüm kitaplıkları ve yürütülebilir projeleri yeniden derleyin.</span><span class="sxs-lookup"><span data-stu-id="af1a6-114">Rebuild all libraries and executable projects.</span></span> <span data-ttu-id="af1a6-115">NetX Duo gerekliyse, tüm modül ve Modül Yöneticisi C kodu, **TXM_MODULE_ENABLE_NETX_DUO** tanımlanmış olarak oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="af1a6-115">If NetX Duo is required, all Module and Module Manager C code should be built with **TXM_MODULE_ENABLE_NETX_DUO** defined.</span></span>

## <a name="module-manager-sources"></a><span data-ttu-id="af1a6-116">Modül Yöneticisi Kaynakları</span><span class="sxs-lookup"><span data-stu-id="af1a6-116">Module Manager sources</span></span>

<span data-ttu-id="af1a6-117">ThreadX Modül Yöneticisi, bağlantılı ve doğrudan yerleşik ThreadX kodu ile konumlandırılabilir şekilde tasarlanan bir kaynak dosyalar kümesine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="af1a6-117">The ThreadX Module Manager has a set of source files that are designed to be linked and located directly with the resident ThreadX code.</span></span> <span data-ttu-id="af1a6-118">Bu dosyalar modülden bir modül ve alan izleyen ThreadX API istekleri başlatma yeteneği sağlar.</span><span class="sxs-lookup"><span data-stu-id="af1a6-118">These files provide the ability to launch a module and field subsequent ThreadX API requests from the module.</span></span> <span data-ttu-id="af1a6-119">Modül Yöneticisi dosyaları aşağıdaki gibidir.</span><span class="sxs-lookup"><span data-stu-id="af1a6-119">The module manager files are as follows.</span></span>

| <span data-ttu-id="af1a6-120">**Dosya adı**</span><span class="sxs-lookup"><span data-stu-id="af1a6-120">**File Name**</span></span> |  <span data-ttu-id="af1a6-121">**İçerik**</span><span class="sxs-lookup"><span data-stu-id="af1a6-121">**Contents**</span></span> |
|-------------- | ------------- |
| <span data-ttu-id="af1a6-122">***txm_module. h***</span><span class="sxs-lookup"><span data-stu-id="af1a6-122">***txm_module.h***</span></span> | <span data-ttu-id="af1a6-123">Modül bilgilerini tanımlayan dosyayı (modül kaynak koduna da dahil) içerir.</span><span class="sxs-lookup"><span data-stu-id="af1a6-123">Include file that defines module information (also included in the module source code).</span></span> |
| <span data-ttu-id="af1a6-124">***txm_module_manager_dispatch. h***</span><span class="sxs-lookup"><span data-stu-id="af1a6-124">***txm_module_manager_dispatch.h***</span></span> | <span data-ttu-id="af1a6-125">Dağıtım Yardımcısı işlevlerini tanımlayan içerme dosyası.</span><span class="sxs-lookup"><span data-stu-id="af1a6-125">Include file that defines dispatch helper functions.</span></span>|
| <span data-ttu-id="af1a6-126">***txm_module_manager_util. h***</span><span class="sxs-lookup"><span data-stu-id="af1a6-126">***txm_module_manager_util.h***</span></span> | <span data-ttu-id="af1a6-127">İç yardımcı program Yardımcısı makrolarını & işlevleri tanımlayan dosya ekleme.</span><span class="sxs-lookup"><span data-stu-id="af1a6-127">Include file that defines internal utility helper macros & functions.</span></span> |
| <span data-ttu-id="af1a6-128">***txm_module_port. h***</span><span class="sxs-lookup"><span data-stu-id="af1a6-128">***txm_module_port.h***</span></span> | <span data-ttu-id="af1a6-129">Bağlantı noktasına özgü modül bilgilerini tanımlayan dosyayı (modül kaynak koduna da dahil olmak üzere) içerir.</span><span class="sxs-lookup"><span data-stu-id="af1a6-129">Include file that defines port-specific module information (also included in the module source code).</span></span> |
| <span data-ttu-id="af1a6-130">\***tx_initialize_low_level. \[ s, S, 68 \]** _</span><span class="sxs-lookup"><span data-stu-id="af1a6-130">\***tx_initialize_low_level.\[s,S,68\]** _</span></span> | <span data-ttu-id="af1a6-131">Var olan ThreadX kitaplık dosyasının yerini alır.</span><span class="sxs-lookup"><span data-stu-id="af1a6-131">Replaces existing ThreadX library file.</span></span> <span data-ttu-id="af1a6-132">Modül Yöneticisi ve bellek özel durumları için güncelleştirilmiş vektör tablosu ve ek vektör işleyicileri.</span><span class="sxs-lookup"><span data-stu-id="af1a6-132">Updated vector table and additional vector handlers for module manager and memory exceptions.</span></span> <span data-ttu-id="af1a6-133">_This dosya yalnızca Cortex-A7/ARM, Cortex-M7/ARM, Cortex-R4/ARM, Cortex-R4/IAR, MCF544xx/GHS, RX63/IAR, RX65N/IAR. \*</span><span class="sxs-lookup"><span data-stu-id="af1a6-133">_This file is only in Cortex-A7/ARM, Cortex-M7/ARM, Cortex-R4/ARM, Cortex-R4/IAR, MCF544xx/GHS, RX63/IAR, RX65N/IAR.\*</span></span>|
| <span data-ttu-id="af1a6-134">\***tx_thread_context_restore. s** _</span><span class="sxs-lookup"><span data-stu-id="af1a6-134">\***tx_thread_context_restore.s** _</span></span> | <span data-ttu-id="af1a6-135">Var olan ThreadX kitaplık dosyasının yerini alır.</span><span class="sxs-lookup"><span data-stu-id="af1a6-135">Replaces existing ThreadX library file.</span></span> <span data-ttu-id="af1a6-136">Kesme işleminden sonra iş parçacığı bağlamını geri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="af1a6-136">Restore thread context after interrupt processing.</span></span> <span data-ttu-id="af1a6-137">_This dosya yalnızca Cortex-A7/ARM, Cortex-R4/ARM, Cortex-R4/IAR içinde. \*</span><span class="sxs-lookup"><span data-stu-id="af1a6-137">_This file is only in Cortex-A7/ARM, Cortex-R4/ARM, Cortex-R4/IAR.\*</span></span>|
| <span data-ttu-id="af1a6-138">***tx_thread_schedule. \[ s, S, 68\]***</span><span class="sxs-lookup"><span data-stu-id="af1a6-138">***tx_thread_schedule.\[s,S,68\]***</span></span> | <span data-ttu-id="af1a6-139">Var olan ThreadX kitaplık dosyasının yerini alır.</span><span class="sxs-lookup"><span data-stu-id="af1a6-139">Replaces existing ThreadX library file.</span></span> <span data-ttu-id="af1a6-140">Bu durumda bellek yönetimi kayıtlarını güncelleştirmek için kullanılan genişletilmiş Zamanlayıcı kodu.</span><span class="sxs-lookup"><span data-stu-id="af1a6-140">Extended scheduler code, which in this case is used to update memory management registers.</span></span> |
| <span data-ttu-id="af1a6-141">\***tx_thread_stack_build. s** _</span><span class="sxs-lookup"><span data-stu-id="af1a6-141">\***tx_thread_stack_build.s** _</span></span> | <span data-ttu-id="af1a6-142">Var olan ThreadX kitaplık dosyasının yerini alır.</span><span class="sxs-lookup"><span data-stu-id="af1a6-142">Replaces existing ThreadX library file.</span></span> <span data-ttu-id="af1a6-143">Bir iş parçacığının yığın çerçevesini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="af1a6-143">Builds the stack frame of a thread.</span></span> <span data-ttu-id="af1a6-144">_This dosya yalnızca Cortex-A7/ARM, Cortex-R4/ARM, Cortex-R4/IAR içinde. \*</span><span class="sxs-lookup"><span data-stu-id="af1a6-144">_This file is only in Cortex-A7/ARM, Cortex-R4/ARM, Cortex-R4/IAR.\*</span></span>|
| <span data-ttu-id="af1a6-145">***txm_module_manager_thread_stack_build. \[ s, S, 68\]***</span><span class="sxs-lookup"><span data-stu-id="af1a6-145">***txm_module_manager_thread_stack_build.\[s,S,68\]***</span></span> | <span data-ttu-id="af1a6-146">Tüm modül ilk yığınlarını oluşturur, konuma bağımsız veri erişimi için kurulum 'u içerir.</span><span class="sxs-lookup"><span data-stu-id="af1a6-146">Builds all module initial stacks, includes setup for position-independent data access.</span></span> |
| <span data-ttu-id="af1a6-147">\***txm_module_manager_user_mode_entry. \[ s, S \]** _</span><span class="sxs-lookup"><span data-stu-id="af1a6-147">\***txm_module_manager_user_mode_entry.\[s,S\]** _</span></span> | <span data-ttu-id="af1a6-148">Modülün çekirdek moduna girmesine izin verir.</span><span class="sxs-lookup"><span data-stu-id="af1a6-148">Allows the module to enter kernel mode.</span></span> <span data-ttu-id="af1a6-149">_This dosya yalnızca Cortex-A7/ARM, Cortex-R4/ARM, Cortex-R4/IAR içinde. \*</span><span class="sxs-lookup"><span data-stu-id="af1a6-149">_This file is only in Cortex-A7/ARM, Cortex-R4/ARM, Cortex-R4/IAR.\*</span></span>|
| <span data-ttu-id="af1a6-150">***txm_module_manager_alignment_adjust. c***</span><span class="sxs-lookup"><span data-stu-id="af1a6-150">***txm_module_manager_alignment_adjust.c***</span></span> | <span data-ttu-id="af1a6-151">Bağlantı noktasına özgü hizalama gereksinimlerini işler.</span><span class="sxs-lookup"><span data-stu-id="af1a6-151">Handles port-specific alignment requirements.</span></span>|
| <span data-ttu-id="af1a6-152">***txm_module_manager_application_request. c***</span><span class="sxs-lookup"><span data-stu-id="af1a6-152">***txm_module_manager_application_request.c***</span></span> | <span data-ttu-id="af1a6-153">Yerleşik koda uygulamaya özgü istekleri işler.</span><span class="sxs-lookup"><span data-stu-id="af1a6-153">Handles the application-specific requests to the resident code.</span></span> |
| <span data-ttu-id="af1a6-154">***txm_module_manager_callback_request. c***</span><span class="sxs-lookup"><span data-stu-id="af1a6-154">***txm_module_manager_callback_request.c***</span></span> | <span data-ttu-id="af1a6-155">Bir modüle geri çağırma isteği gönderir.</span><span class="sxs-lookup"><span data-stu-id="af1a6-155">Sends a callback request to a module.</span></span> |
| <span data-ttu-id="af1a6-156">***txm_module_manager_event_flags_notify_trampoline. c***</span><span class="sxs-lookup"><span data-stu-id="af1a6-156">***txm_module_manager_event_flags_notify_trampoline.c***</span></span> | <span data-ttu-id="af1a6-157">Etkinlik bayraklarını, ThreadX 'den bildirim çağrısını ayarla olarak işler.</span><span class="sxs-lookup"><span data-stu-id="af1a6-157">Processes the event flags set notification call from ThreadX.</span></span> |
| <span data-ttu-id="af1a6-158">***txm_module_manager_external_memory_enable. c***</span><span class="sxs-lookup"><span data-stu-id="af1a6-158">***txm_module_manager_external_memory_enable.c***</span></span> | <span data-ttu-id="af1a6-159">Modülün erişebileceği paylaşılan bellek alanı için bellek yönetimi tablosunda bir giriş oluşturur.</span><span class="sxs-lookup"><span data-stu-id="af1a6-159">Creates an entry in the memory management table for a shared memory space the module can access.</span></span> |
| <span data-ttu-id="af1a6-160">***txm_module_manager_file_load. c***</span><span class="sxs-lookup"><span data-stu-id="af1a6-160">***txm_module_manager_file_load.c***</span></span> | <span data-ttu-id="af1a6-161">Modül bellek alanına bir ikili modül dosyası ayırır ve yükler ve yürütülmek üzere hazırlar.</span><span class="sxs-lookup"><span data-stu-id="af1a6-161">Allocates and loads a binary module file into the module memory area and prepares it for execution.</span></span> |
| <span data-ttu-id="af1a6-162">***txm_module_manager_in_place_load. c***</span><span class="sxs-lookup"><span data-stu-id="af1a6-162">***txm_module_manager_in_place_load.c***</span></span> | <span data-ttu-id="af1a6-163">Modül veri alanını ayırır ve sağlanan kod adresinden modül yürütmesi için hazırlar.</span><span class="sxs-lookup"><span data-stu-id="af1a6-163">Allocates the module data area and prepares for module execution from the supplied code address.</span></span> |
| <span data-ttu-id="af1a6-164">***txm_module_manager_initialize. c***</span><span class="sxs-lookup"><span data-stu-id="af1a6-164">***txm_module_manager_initialize.c***</span></span> | <span data-ttu-id="af1a6-165">Modülleri yüklemek ve çalıştırmak için kullanılabilir modül belleği alanının belirtimi dahil olmak üzere modül yöneticisini başlatır.</span><span class="sxs-lookup"><span data-stu-id="af1a6-165">Initializes the Module Manager, including specification of the module memory area available for loading and running modules.</span></span> |
| <span data-ttu-id="af1a6-166">\***txm_module_manager_initialize_mmu. c** _</span><span class="sxs-lookup"><span data-stu-id="af1a6-166">\***txm_module_manager_initialize_mmu.c** _</span></span> | <span data-ttu-id="af1a6-167">MMU 'i başlatın.</span><span class="sxs-lookup"><span data-stu-id="af1a6-167">Initialize MMU.</span></span> <span data-ttu-id="af1a6-168">Kullanıcılar, bu dosyayı bellek haritalarına göre düzenleyebilir.</span><span class="sxs-lookup"><span data-stu-id="af1a6-168">Users can edit this file according to their memory map.</span></span> <span data-ttu-id="af1a6-169">_This dosya yalnızca Cortex-A7/ARM \*</span><span class="sxs-lookup"><span data-stu-id="af1a6-169">_This file is only in Cortex-A7/ARM\*</span></span> |
| <span data-ttu-id="af1a6-170">\***txm_module_manager_mm_initialize. c** _</span><span class="sxs-lookup"><span data-stu-id="af1a6-170">\***txm_module_manager_mm_initialize.c** _</span></span> | <span data-ttu-id="af1a6-171">MPU/MMU 'i başlatın.</span><span class="sxs-lookup"><span data-stu-id="af1a6-171">Initialize MPU/MMU.</span></span> <span data-ttu-id="af1a6-172">Kullanıcılar, bu dosyayı bellek haritalarına göre düzenleyebilir.</span><span class="sxs-lookup"><span data-stu-id="af1a6-172">Users can edit this file according to their memory map.</span></span> <span data-ttu-id="af1a6-173">_This dosya yalnızca Cortex-A7/ARM \*</span><span class="sxs-lookup"><span data-stu-id="af1a6-173">_This file is only in Cortex-A7/ARM\*</span></span> |
| <span data-ttu-id="af1a6-174">***txm_module_manager_kernel_dispatch. c***</span><span class="sxs-lookup"><span data-stu-id="af1a6-174">***txm_module_manager_kernel_dispatch.c***</span></span> | <span data-ttu-id="af1a6-175">İstek KIMLIĞINE göre modül API 'SI isteklerini işler.</span><span class="sxs-lookup"><span data-stu-id="af1a6-175">Handles the module API requests, based on the request ID.</span></span> |
| <span data-ttu-id="af1a6-176">***txm_module_manager_maximum_module_priority_set. c***</span><span class="sxs-lookup"><span data-stu-id="af1a6-176">***txm_module_manager_maximum_module_priority_set.c***</span></span> | <span data-ttu-id="af1a6-177">Bir modülde izin verilen en fazla iş parçacığı önceliğini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="af1a6-177">Sets the maximum thread priority allowed in a module.</span></span> |
| <span data-ttu-id="af1a6-178">***txm_module_manager_memory_fault_handler. c***</span><span class="sxs-lookup"><span data-stu-id="af1a6-178">***txm_module_manager_memory_fault_handler.c***</span></span> | <span data-ttu-id="af1a6-179">Yürütülen modülde algılanan bellek hatalarını işler.</span><span class="sxs-lookup"><span data-stu-id="af1a6-179">Handles memory faults detected in an executing module.</span></span> |
| <span data-ttu-id="af1a6-180">***txm_module_manager_memory_fault_notify. c***</span><span class="sxs-lookup"><span data-stu-id="af1a6-180">***txm_module_manager_memory_fault_notify.c***</span></span> | <span data-ttu-id="af1a6-181">Bir bellek hatası oluştuğunda uygulama bildirimi geri aramasını kaydeder.</span><span class="sxs-lookup"><span data-stu-id="af1a6-181">Registers an application notification callback whenever a memory fault occurs.</span></span> |
| <span data-ttu-id="af1a6-182">***txm_module_manager_memory_load. c***</span><span class="sxs-lookup"><span data-stu-id="af1a6-182">***txm_module_manager_memory_load.c***</span></span> | <span data-ttu-id="af1a6-183">Modülün kodunu ve verilerini ayırır ve yükler ve modülü yürütülmek üzere hazırlar.</span><span class="sxs-lookup"><span data-stu-id="af1a6-183">Allocates and loads a module's code and data and prepares the module for execution.</span></span> |
| <span data-ttu-id="af1a6-184">***txm_module_manager_mm_register_setup. c***</span><span class="sxs-lookup"><span data-stu-id="af1a6-184">***txm_module_manager_mm_register_setup.c***</span></span> | <span data-ttu-id="af1a6-185">Modül için kod ve verilerin yüklendiği yere bağlı olarak, modül için MPU/MMU yazmaçlarını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="af1a6-185">Sets up MPU/MMU registers for the module based on where the code and data are loaded.</span></span> |
| <span data-ttu-id="af1a6-186">***txm_module_manager_object_allocate. c***</span><span class="sxs-lookup"><span data-stu-id="af1a6-186">***txm_module_manager_object_allocate.c***</span></span> | <span data-ttu-id="af1a6-187">Bir modül nesnesi için belleği ayırır.</span><span class="sxs-lookup"><span data-stu-id="af1a6-187">Allocates memory for a module object.</span></span> |
| <span data-ttu-id="af1a6-188">***txm_module_manager_object_deallocate. c***</span><span class="sxs-lookup"><span data-stu-id="af1a6-188">***txm_module_manager_object_deallocate.c***</span></span> | <span data-ttu-id="af1a6-189">Modül nesnesi için belleği ayırır.</span><span class="sxs-lookup"><span data-stu-id="af1a6-189">Deallocates memory for a module object.</span></span> |
| <span data-ttu-id="af1a6-190">***txm_module_manager_object_pointer_get. c***</span><span class="sxs-lookup"><span data-stu-id="af1a6-190">***txm_module_manager_object_pointer_get.c***</span></span> | <span data-ttu-id="af1a6-191">Sağlanan nesne türünü ve adını arar ve bulunursa, nesne işaretçisini döndürür.</span><span class="sxs-lookup"><span data-stu-id="af1a6-191">Searches for the supplied object type and name, and if found, returns the object pointer.</span></span> |
| <span data-ttu-id="af1a6-192">***txm_module_manager_object_pointer_get_extended. c***</span><span class="sxs-lookup"><span data-stu-id="af1a6-192">***txm_module_manager_object_pointer_get_extended.c***</span></span> | <span data-ttu-id="af1a6-193">Sağlanan nesne türünü ve adını arar ve bulunursa, nesne işaretçisini döndürür.</span><span class="sxs-lookup"><span data-stu-id="af1a6-193">Searches for the supplied object type and name, and if found, returns the object pointer.</span></span> <span data-ttu-id="af1a6-194">Güvenlik için ad uzunluğu belirtildi.</span><span class="sxs-lookup"><span data-stu-id="af1a6-194">Name length specified for safety.</span></span> |
| <span data-ttu-id="af1a6-195">***txm_module_manager_object_pool_create. c***</span><span class="sxs-lookup"><span data-stu-id="af1a6-195">***txm_module_manager_object_pool_create.c***</span></span>  | <span data-ttu-id="af1a6-196">Modül uygulamalarının ayırabilecek modül veri alanı dışında bir nesne havuzu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="af1a6-196">Creates a pool of objects outside the module's data area that module applications can allocate from.</span></span> |
| <span data-ttu-id="af1a6-197">***txm_module_manager_properties_get. c***</span><span class="sxs-lookup"><span data-stu-id="af1a6-197">***txm_module_manager_properties_get.c***</span></span> | <span data-ttu-id="af1a6-198">Belirtilen modülün özelliklerini alır.</span><span class="sxs-lookup"><span data-stu-id="af1a6-198">Gets the properties of the specified module.</span></span> |
| <span data-ttu-id="af1a6-199">***txm_module_manager_queue_notify_trampoline. c***</span><span class="sxs-lookup"><span data-stu-id="af1a6-199">***txm_module_manager_queue_notify_trampoline.c***</span></span> | <span data-ttu-id="af1a6-200">ThreadX 'den kuyruk bildirim çağrısını işler.</span><span class="sxs-lookup"><span data-stu-id="af1a6-200">Processes the queue notification call from ThreadX.</span></span> |
| <span data-ttu-id="af1a6-201">***txm_module_manager_semaphore_notify_trampoline. c***</span><span class="sxs-lookup"><span data-stu-id="af1a6-201">***txm_module_manager_semaphore_notify_trampoline.c***</span></span> | <span data-ttu-id="af1a6-202">ThreadX 'ten semafor put bildirim çağrısını işler.</span><span class="sxs-lookup"><span data-stu-id="af1a6-202">Processes the semaphore put notification call from ThreadX.</span></span>|
| <span data-ttu-id="af1a6-203">***txm_module_manager_start. c***</span><span class="sxs-lookup"><span data-stu-id="af1a6-203">***txm_module_manager_start.c***</span></span> | <span data-ttu-id="af1a6-204">Bir modülün yürütülmesini başlatır.</span><span class="sxs-lookup"><span data-stu-id="af1a6-204">Starts execution of a module.</span></span> |
| <span data-ttu-id="af1a6-205">***txm_module_manager_stop. c***</span><span class="sxs-lookup"><span data-stu-id="af1a6-205">***txm_module_manager_stop.c***</span></span> | <span data-ttu-id="af1a6-206">Modülün yürütülmesini durduruyor.</span><span class="sxs-lookup"><span data-stu-id="af1a6-206">Stops execution of a module.</span></span> |
| <span data-ttu-id="af1a6-207">***txm_module_manager_thread_create. c***</span><span class="sxs-lookup"><span data-stu-id="af1a6-207">***txm_module_manager_thread_create.c***</span></span> | <span data-ttu-id="af1a6-208">Tüm modül iş parçacıklarını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="af1a6-208">Creates all module threads.</span></span> |
| <span data-ttu-id="af1a6-209">***txm_module_manager_thread_notify_trampoline. c***</span><span class="sxs-lookup"><span data-stu-id="af1a6-209">***txm_module_manager_thread_notify_trampoline.c***</span></span> | <span data-ttu-id="af1a6-210">ThreadX iş parçacığı giriş/çıkış bildirimi çağrısını işler.</span><span class="sxs-lookup"><span data-stu-id="af1a6-210">Processes the thread entry/exit notification call from ThreadX.</span></span> |
| <span data-ttu-id="af1a6-211">***txm_module_manager_thread_reset. c***</span><span class="sxs-lookup"><span data-stu-id="af1a6-211">***txm_module_manager_thread_reset.c***</span></span> | <span data-ttu-id="af1a6-212">Modül iş parçacığını sıfırlayın.</span><span class="sxs-lookup"><span data-stu-id="af1a6-212">Reset a module thread.</span></span> |
| <span data-ttu-id="af1a6-213">***txm_module_manager_timer_notify_trampoline. c***</span><span class="sxs-lookup"><span data-stu-id="af1a6-213">***txm_module_manager_timer_notify_trampoline.c***</span></span> | <span data-ttu-id="af1a6-214">ThreadX 'den süreölçer süre sonlarını işler.</span><span class="sxs-lookup"><span data-stu-id="af1a6-214">Processes timer expirations from ThreadX.</span></span> |
| <span data-ttu-id="af1a6-215">***txm_module_manager_unload. c***</span><span class="sxs-lookup"><span data-stu-id="af1a6-215">***txm_module_manager_unload.c***</span></span> | <span data-ttu-id="af1a6-216">Modülü modül bellek alanından kaldırır.</span><span class="sxs-lookup"><span data-stu-id="af1a6-216">Unloads the module from the module memory area.</span></span> |
| <span data-ttu-id="af1a6-217">***txm_module_manager_util. c***</span><span class="sxs-lookup"><span data-stu-id="af1a6-217">***txm_module_manager_util.c***</span></span> | <span data-ttu-id="af1a6-218">Yöneticinin iç yardımcı işlevleri.</span><span class="sxs-lookup"><span data-stu-id="af1a6-218">Internal helper functions for manager.</span></span> |

## <a name="module-manager-initialization"></a><span data-ttu-id="af1a6-219">Modül Yöneticisi başlatma</span><span class="sxs-lookup"><span data-stu-id="af1a6-219">Module Manager initialization</span></span>

<span data-ttu-id="af1a6-220">Uygulamanın yerleşik bölümü, ***Txm_module_manager_initialize*** Modül Yöneticisi başlatma işlevinin çağrılmasından sorumludur.</span><span class="sxs-lookup"><span data-stu-id="af1a6-220">The resident portion of the application is responsible for calling the Module Manager initialization function ***txm_module_manager_initialize***.</span></span> <span data-ttu-id="af1a6-221">Bu işlev, modül belleği ayırmak için kullanılan bellek alanını ayarlama da dahil olmak üzere modülleri yükleme ve kaldırma için iç yapıları ayarlar.</span><span class="sxs-lookup"><span data-stu-id="af1a6-221">This function sets up the internal structures for loading and unloading modules, including setting up the memory area used for allocating module memory.</span></span>

## <a name="module-manager-loading"></a><span data-ttu-id="af1a6-222">Modül Yöneticisi yükleniyor</span><span class="sxs-lookup"><span data-stu-id="af1a6-222">Module Manager loading</span></span>

<span data-ttu-id="af1a6-223">Modül Yöneticisi, ikili modül dosyalarından veya yerleşik kod alanında zaten mevcut olan bir modül kodu bölümünden modül belleğine dinamik olarak modül yükleyebilir.</span><span class="sxs-lookup"><span data-stu-id="af1a6-223">The Module Manager can load modules dynamically into the module memory from binary module files or from a module code section that is already present in the resident code area.</span></span> <span data-ttu-id="af1a6-224">Ayrıca, Modül Yöneticisi kodu yerinde yürütebilir, diğer bir deyişle modül belleğinde yalnızca modül verileri ayrılır ve kod yürütme yerinde yapılır.</span><span class="sxs-lookup"><span data-stu-id="af1a6-224">In addition, the module manager can execute code in place, that is, only the module data is allocated in the module memory and the code execution is done in place.</span></span> <span data-ttu-id="af1a6-225">Aşağıdaki Modül Yöneticisi yük API işlevleri kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="af1a6-225">The following Module Manager load API functions are available.</span></span>

* <span data-ttu-id="af1a6-226">***txm_module_manager_file_load***</span><span class="sxs-lookup"><span data-stu-id="af1a6-226">***txm_module_manager_file_load***</span></span>

* <span data-ttu-id="af1a6-227">***txm_module_manager_in_place_load***</span><span class="sxs-lookup"><span data-stu-id="af1a6-227">***txm_module_manager_in_place_load***</span></span>

* <span data-ttu-id="af1a6-228">***txm_module_manager_memory_load***</span><span class="sxs-lookup"><span data-stu-id="af1a6-228">***txm_module_manager_memory_load***</span></span>

<span data-ttu-id="af1a6-229">Modül yöneticisinin bellek korumalı sürümü aynı zamanda modülün uygun hizalamayla yüklendiğinden ve bellek yönetimi saklayıcıları her modül için doğru şekilde kurulduğundan emin olur.</span><span class="sxs-lookup"><span data-stu-id="af1a6-229">The memory protected version of the Module Manager also makes sure that the module is loaded with the proper alignment and the memory management registers are set up properly for each module.</span></span> <span data-ttu-id="af1a6-230">Bellek koruması modül girişi seçenekleri aracılığıyla etkinleştirildiğinde modül belleği erişimi modül kodu ve veri alanlarıyla kısıtlıdır.</span><span class="sxs-lookup"><span data-stu-id="af1a6-230">When memory protection is enabled via the module preamble options, module memory access is restricted to the module code and data areas.</span></span>

## <a name="module-manager-starting"></a><span data-ttu-id="af1a6-231">Modül Yöneticisi başlatılıyor</span><span class="sxs-lookup"><span data-stu-id="af1a6-231">Module Manager starting</span></span>

<span data-ttu-id="af1a6-232">Modül Yöneticisi, ***txm_module_manager_start*** API işlevi aracılığıyla önceden yüklenmiş bir modülün yürütülmesini başlatır.</span><span class="sxs-lookup"><span data-stu-id="af1a6-232">The Module Manager initiates execution of a previously-loaded module via the ***txm_module_manager_start*** API function.</span></span> <span data-ttu-id="af1a6-233">Modül yürütmeyi başlatmak için, bu işlev modül girişi içinde belirtilen başlangıç konumunda modülü giren bir iş parçacığı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="af1a6-233">To initiate module execution, this function creates a thread that enters the module at the starting location specified in the module preamble.</span></span> <span data-ttu-id="af1a6-234">Bu iş parçacığının öncelik ve yığın boyutu Ayrıca modül girişi içinde de belirtilir.</span><span class="sxs-lookup"><span data-stu-id="af1a6-234">The priority and stack size of this thread is also specified in the module preamble.</span></span>

## <a name="module-manager-stopping"></a><span data-ttu-id="af1a6-235">Modül Yöneticisi durduruluyor</span><span class="sxs-lookup"><span data-stu-id="af1a6-235">Module Manager stopping</span></span>

<span data-ttu-id="af1a6-236">Modül Yöneticisi, ***txm_module_manager_stop*** işlevi aracılığıyla daha önce yüklenmiş ve yürütülen bir modülün yürütülmesini sonlandırır.</span><span class="sxs-lookup"><span data-stu-id="af1a6-236">The Module Manager terminates execution of a previously-loaded and executing module via the ***txm_module_manager_stop*** function.</span></span> <span data-ttu-id="af1a6-237">Bu API işlevi ilk olarak sonlanır ve başlangıç iş parçacığını siler.</span><span class="sxs-lookup"><span data-stu-id="af1a6-237">This API function first terminates and deletes the initial starting thread.</span></span> <span data-ttu-id="af1a6-238">Modül girişi bir durdurma iş parçacığını belirtiyorsa, bu iş parçacığı oluşturulup yürütülür.</span><span class="sxs-lookup"><span data-stu-id="af1a6-238">If the module preamble specifies a stop thread, this thread is created and executed.</span></span> <span data-ttu-id="af1a6-239">Modül Yöneticisi durdurma iş parçacığının tamamlaması için sabit bir süre bekler.</span><span class="sxs-lookup"><span data-stu-id="af1a6-239">The Module Manager waits for a fixed period of time for the stop thread to complete.</span></span> <span data-ttu-id="af1a6-240">Tamamlandıktan sonra, modül tarafından oluşturulan tüm sistem kaynakları silinir ve modül, yeniden başlatılabilir veya bellekten kaldırılabileceği bir etkin durumdan konur.</span><span class="sxs-lookup"><span data-stu-id="af1a6-240">Once complete, all system resources created by the module are deleted and the module is placed in a dormant state, from which it can be either restarted or unloaded.</span></span>

## <a name="module-manager-unloading"></a><span data-ttu-id="af1a6-241">Modül yöneticisini kaldırma</span><span class="sxs-lookup"><span data-stu-id="af1a6-241">Module Manager unloading</span></span>

<span data-ttu-id="af1a6-242">Modül Yöneticisi, daha önce yüklenmiş ancak ***txm_module_manager_unload*** işlevi aracılığıyla bir modül yürütmez modülünü kaldırır.</span><span class="sxs-lookup"><span data-stu-id="af1a6-242">The Module Manager unloads a previously-loaded but not executing module via the ***txm_module_manager_unload*** function.</span></span> <span data-ttu-id="af1a6-243">Bu API, modülle ilişkili tüm belleği yayınlar ve gelecekte başka bir modülle kullanılmak üzere serbest bırakır.</span><span class="sxs-lookup"><span data-stu-id="af1a6-243">This API releases all memory associated with the module, freeing it for use with another module in the future.</span></span>

## <a name="module-manager-requests"></a><span data-ttu-id="af1a6-244">Modül Yöneticisi istekleri</span><span class="sxs-lookup"><span data-stu-id="af1a6-244">Module Manager requests</span></span>

<span data-ttu-id="af1a6-245">Modül Yöneticisi 'ne modüller tarafından yapılan istekler, Modül Yöneticisi tarafından modüle sağlanan bir işlev işaretçisi aracılığıyla Modül Yöneticisi gönderme işlevini çağıran ***txm_module. h*** içindeki makrolar aracılığıyla yapılır.</span><span class="sxs-lookup"><span data-stu-id="af1a6-245">Requests made by modules to the Module Manager are done via macros in ***txm_module.h*** that map all ThreadX calls to call the Module Manager dispatch function via a function pointer supplied to the module by the Module Manager.</span></span>

<span data-ttu-id="af1a6-246">***Txm_module_application_request*** çağıran modül aracılığıyla yapılan uygulamaya özgü ek hizmetler, THREADX API 'si için kullanılan aynı makro mekanizması tarafından işlenir.</span><span class="sxs-lookup"><span data-stu-id="af1a6-246">Additional application-specific services made via the module calling ***txm_module_application_request*** are handled by the same macro mechanism used for the ThreadX API.</span></span> <span data-ttu-id="af1a6-247">Varsayılan olarak, modül yöneticisindeki bu işleme işlevi boştur ve uygulamanın uygulamaya özgü istekleri işlemek için gerekli kodu eklemesi için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="af1a6-247">By default, this handling function in the Module Manager is empty and designed such that the application adds the necessary code to process the application-specific requests.</span></span>

<span data-ttu-id="af1a6-248">İstek Modül Yöneticisi tarafından uygulanmadığından, Modül Yöneticisi tarafından **TX_NOT_AVAILABLE** hata durumu değeri döndürülür.</span><span class="sxs-lookup"><span data-stu-id="af1a6-248">If the request is not implemented by the Module Manager, a value of **TX_NOT_AVAILABLE** error status is returned by the Module Manager.</span></span> <span data-ttu-id="af1a6-249">Modül erişimi kapsamı dışında bir işlem isterse, bu hata kodu da döndürülür.</span><span class="sxs-lookup"><span data-stu-id="af1a6-249">This error code is also returned if the module requests an operation that is outside the scope of the module's access.</span></span> <span data-ttu-id="af1a6-250">Örneğin, bir modülün, Zamanlayıcı denetim bloğu veya geri çağırma adresiyle modülün kod alanı dışında bir Zamanlayıcı oluşturmasına izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="af1a6-250">For example, a module is not allowed to create a timer with the timer control block or callback address outside of the module's code area.</span></span>

## <a name="module-manager-example"></a><span data-ttu-id="af1a6-251">Modül Yöneticisi örneği</span><span class="sxs-lookup"><span data-stu-id="af1a6-251">Module Manager example</span></span>

<span data-ttu-id="af1a6-252">Aşağıda, Bölüm 2 ' de daha önce tanımlanan örnek modülünü Başlatan modül yöneticisi kodunun bir örneği verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="af1a6-252">The following is an example of Module Manager code that launches the example module previously defined in Chapter 2.</span></span> <span data-ttu-id="af1a6-253">Modülün zaten yüklü olduğu varsayılır, bu da hata ayıklayıcının, 0x00800000 ROM adresidir.</span><span class="sxs-lookup"><span data-stu-id="af1a6-253">It is assumed that the module is already loaded, presumably by the debugger, at ROM address 0x00800000.</span></span>

```c
#include "tx_api.h"
#include "txm_module.h"

#define DEMO_STACK_SIZE 1024

/* Define the ThreadX object control blocks. */
TX_THREAD   module_manager;

/* Define thread prototype. */
void        module_manager_entry(ULONG thread_input);

/* Define the module object pool area. */
UCHAR       object_memory[8192];

/* Define the module data pool area. */
#define MODULE_DATA_SIZE 65536
UCHAR       module_data_area[MODULE_DATA_SIZE];

/* Define module instances. */
TXM_MODULE_INSTANCE     my_module1;
TXM_MODULE_INSTANCE     my_module2;

/* Define the count of memory faults. */
ULONG memory_faults;

/* Define fault handler. */
VOID module_fault_handler(TX_THREAD *thread, TXM_MODULE_INSTANCE *module)
{
    /* Just increment the fault counter. */
    memory_faults++;
}

/* Define main entry point. */
int main()
{
    /* Enter the ThreadX kernel. */
    tx_kernel_enter();
}

/* Define what the initial system looks like. */
void tx_application_define(void *first_unused_memory)
{
    /* Create the module manager thread. */
    tx_thread_create(&module_manager, "Module Manager Thread", module_manager_entry, 0,
                    first_unused_memory, DEMO_STACK_SIZE,
                    1, 1, TX_NO_TIME_SLICE, TX_AUTO_START);
}

/* Define the test threads. */
void module_manager_entry(ULONG thread_input)
{
    /* Initialize the module manager. */
    txm_module_manager_initialize((VOID *) module_data_area, MODULE_DATA_SIZE);

    /* Create a pool for module objects. */
    txm_module_manager_object_pool_create(object_memory, sizeof(object_memory));

    /* Register a fault handler. */
    txm_module_manager_memory_fault_notify(module_fault_handler);

    /* Load the module that is already there,
        in this example it is placed at 0x00800000. */
    txm_module_manager_in_place_load(&my_module1, "my module1", (VOID *) 0x00800000);

    /* Load a second instance of the module. */
    txm_module_manager_in_place_load(&my_module2, "my module2", (VOID *) 0x00800000);

    /* Enable shared memory region for module2. */
    txm_module_manager_external_memory_enable(&my_module2, (void*)0x20600000, 0x010000, 0x3F);

    /* Start the modules. */
    txm_module_manager_start(&my_module1);
    txm_module_manager_start(&my_module2);

    /* Sleep for a while and let the modules run... */
    tx_thread_sleep(300);

    /* Stop the modules. */
    txm_module_manager_stop(&my_module1);
    txm_module_manager_stop(&my_module2);

    /* Unload the modules. */
    txm_module_manager_unload(&my_module1);
    txm_module_manager_unload(&my_module2);

    /* Reload the modules. */
    txm_module_manager_in_place_load(&my_module2, "my module2", (VOID *) 0x00800000);
    txm_module_manager_in_place_load(&my_module1, "my module1", (VOID *) 0x00800000);

    /* Give both modules shared memory. */
    txm_module_manager_external_memory_enable(&my_module2, (void*)0x20600000, 0x010000, 0x3F);
    txm_module_manager_external_memory_enable(&my_module1, (void*)0x20600000, 0x010000, 0x3F);

    /* Set maximum module1 priority to 5. */
    txm_module_manager_maximum_module_priority_set(&my_module1, 5);

    /* Start the modules again. */
    txm_module_manager_start(&my_module2);
    txm_module_manager_start(&my_module1);

    /* Now just spin... */
    while(1)
    {
        tx_thread_sleep(100);

        /* Threads 0 and 5 in module1 are not created because they violate the maximum priority. */
    }
}
```

## <a name="module-manager-building"></a><span data-ttu-id="af1a6-254">Modül Yöneticisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="af1a6-254">Module Manager building</span></span>

<span data-ttu-id="af1a6-255">***Txm_module_manager_ \**** kaynak dosyaları threadx kitaplığına eklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="af1a6-255">The ***txm_module_manager_\**** source files must be added to the ThreadX library.</span></span>

<span data-ttu-id="af1a6-256">Bir ThreadX Modül Yöneticisi uygulaması, bir veya daha fazla uygulama dosyası olan ThreadX Kitaplığı ***TX. a*** ile birlikte bağlantılı bir standart threadx uygulamasıyla aynı şekilde aynıdır.</span><span class="sxs-lookup"><span data-stu-id="af1a6-256">A ThreadX Module Manager application is effectively the same as a standard ThreadX application, which is one or more application files linked together with the ThreadX library ***tx.a***.</span></span> <span data-ttu-id="af1a6-257">Modül Yöneticisi uygulaması derleme, kullanılan araç zincirine bağımlıdır.</span><span class="sxs-lookup"><span data-stu-id="af1a6-257">Building a module manager application is dependent on the tool chain being used.</span></span> <span data-ttu-id="af1a6-258">Bkz. bağlantı noktasına özgü örnekler için [ek](appendix.md) .</span><span class="sxs-lookup"><span data-stu-id="af1a6-258">See [appendix](appendix.md) for port-specific examples.</span></span>
