---
title: Bölüm 2-ARMv8-d için ThreadX desteği yükleme
description: Bu bölümde, ARMv8-e mimarisi için ThreadX kaynak kodunun nasıl yükleneceği ve kullanılacağı açıklanmaktadır.
author: v-condav
ms.author: v-condav
ms.date: 03/04/2021
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 303b83bcc92797314b764353b770965c0170fb99
ms.sourcegitcommit: d8edbb3207fe99f8afb431597dac063e73383e68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/05/2021
ms.locfileid: "106377625"
---
#  <a name="chapter-2--installing-threadx-support-for-armv8-m"></a><span data-ttu-id="c3ae7-103">Bölüm 2 ARMv8-d için ThreadX desteğini yükleme</span><span class="sxs-lookup"><span data-stu-id="c3ae7-103">Chapter 2  Installing ThreadX support for ARMv8-M</span></span>

<span data-ttu-id="c3ae7-104">ARMv8-e mimarisini desteklemek için ek ThreadX kaynak kodu dosyaları vardır.</span><span class="sxs-lookup"><span data-stu-id="c3ae7-104">There are additional ThreadX source code files to support the ARMv8-M architecture.</span></span>

<span data-ttu-id="c3ae7-105">ThreadX güvenli modda çalıştırılabilmesi için bu ek dosyalar ve API 'Ler gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="c3ae7-105">If ThreadX is to be run in secure mode, these additional files and APIs are not needed.</span></span> <span data-ttu-id="c3ae7-106">ThreadX 'i güvenli modda çalıştırmak için,  **_tx_port. h_ _ ' nin üstündeki *veya komut satırında veya proje ayarlarında sembol TX_SECURE_EXECUTION belirleyin. _* TX_SECURE_EXECUTION** tüm c ve derleme dosyaları için tanımlandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="c3ae7-106">To run ThreadX in secure mode, define the symbol **TX_SECURE_EXECUTION** at the top of **_tx_port.h_*_ or on the command line or project settings. Ensure _\* TX_SECURE_EXECUTION*\* is defined for all c and assembly files.</span></span> <span data-ttu-id="c3ae7-107">ThreadX ve Kullanıcı uygulaması güvenli modda yürütülür.</span><span class="sxs-lookup"><span data-stu-id="c3ae7-107">ThreadX and the user application will execute in secure mode.</span></span>

<span data-ttu-id="c3ae7-108">ThreadX ve Kullanıcı uygulamasını güvenli olmayan modda çalıştırmak ve güvenli olmayan çağrılabilir güvenli işlevleri desteklemek için lütfen aşağıdakileri yapın.</span><span class="sxs-lookup"><span data-stu-id="c3ae7-108">To run ThreadX and the user application in non-secure mode and support non-secure callable secure functions, please do the following.</span></span>

<span data-ttu-id="c3ae7-109">***Tx_thread_secure_stack. c*** dosyası güvenli uygulamaya eklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="c3ae7-109">The file ***tx_thread_secure_stack.c*** must be added to the secure application.</span></span>

<span data-ttu-id="c3ae7-110">Aşağıdaki dosyalar ThreadX kitaplığına eklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="c3ae7-110">The following files must be added to the ThreadX library.</span></span>

- <span data-ttu-id="c3ae7-111">***tx_secure_interface. h***</span><span class="sxs-lookup"><span data-stu-id="c3ae7-111">***tx_secure_interface.h***</span></span>
- <span data-ttu-id="c3ae7-112">***txe_thread_secure_stack_allocate. c***</span><span class="sxs-lookup"><span data-stu-id="c3ae7-112">***txe_thread_secure_stack_allocate.c***</span></span>
- <span data-ttu-id="c3ae7-113">***txe_thread_secure_stack_free. c***</span><span class="sxs-lookup"><span data-stu-id="c3ae7-113">***txe_thread_secure_stack_free.c***</span></span>
- <span data-ttu-id="c3ae7-114">***tx_thread_secure_stack_allocate. s***</span><span class="sxs-lookup"><span data-stu-id="c3ae7-114">***tx_thread_secure_stack_allocate.s***</span></span>
- <span data-ttu-id="c3ae7-115">***tx_thread_secure_stack_free. s***</span><span class="sxs-lookup"><span data-stu-id="c3ae7-115">***tx_thread_secure_stack_free.s***</span></span>

<span data-ttu-id="c3ae7-116">Aşağıdaki iki dosya, ThreadX kitaplığındaki genel dosyaları değiştirir.</span><span class="sxs-lookup"><span data-stu-id="c3ae7-116">The following two files replace the generic files in the ThreadX library.</span></span>

- <span data-ttu-id="c3ae7-117">***tx_thread_stack_error_handler. c***</span><span class="sxs-lookup"><span data-stu-id="c3ae7-117">***tx_thread_stack_error_handler.c***</span></span>
- <span data-ttu-id="c3ae7-118">***tx_thread_stack_error_notify. c***</span><span class="sxs-lookup"><span data-stu-id="c3ae7-118">***tx_thread_stack_error_notify.c***</span></span>

## <a name="additional-threadx-sources-for-armv8-m"></a><span data-ttu-id="c3ae7-119">ARMv8-d için ek ThreadX kaynakları</span><span class="sxs-lookup"><span data-stu-id="c3ae7-119">Additional ThreadX Sources for ARMv8-M</span></span>

<span data-ttu-id="c3ae7-120">ARMv8-p TrustZone mimarisine yönelik ek ThreadX dosyaları aşağıda açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="c3ae7-120">The additional ThreadX files for the ARMv8-M TrustZone architecture are described below.</span></span>

  | <span data-ttu-id="c3ae7-121">**Dosya adı**</span><span class="sxs-lookup"><span data-stu-id="c3ae7-121">**File Name**</span></span>                            | <span data-ttu-id="c3ae7-122">**İçerik**</span><span class="sxs-lookup"><span data-stu-id="c3ae7-122">**Contents**</span></span>                                                        |
  |------------------------------------------|---------------------------------------------------------------------|
  | <span data-ttu-id="c3ae7-123">***tx_secure_interface. h***</span><span class="sxs-lookup"><span data-stu-id="c3ae7-123">***tx_secure_interface.h***</span></span>              | <span data-ttu-id="c3ae7-124">ThreadX güvenli olmayan çağrılabilir işlevleri tanımlayan dosya ekleme.</span><span class="sxs-lookup"><span data-stu-id="c3ae7-124">Include file that defines the ThreadX non-secure callable functions.</span></span> |
  | <span data-ttu-id="c3ae7-125">***txe_thread_secure_stack_allocate. c***</span><span class="sxs-lookup"><span data-stu-id="c3ae7-125">***txe_thread_secure_stack_allocate.c***</span></span> |  <span data-ttu-id="c3ae7-126">Güvenli yığın ayırma API 'SI için dosya denetleniyor.</span><span class="sxs-lookup"><span data-stu-id="c3ae7-126">Error-checking file for the secure stack allocate API.</span></span> |
  | <span data-ttu-id="c3ae7-127">***txe_thread_secure_stack_free. c***</span><span class="sxs-lookup"><span data-stu-id="c3ae7-127">***txe_thread_secure_stack_free.c***</span></span>     |  <span data-ttu-id="c3ae7-128">Hata-güvenli yığın ücretsiz API 'SI için dosya denetleniyor.</span><span class="sxs-lookup"><span data-stu-id="c3ae7-128">Error-checking file for the secure stack free API.</span></span> |
  | <span data-ttu-id="c3ae7-129">***tx_thread_secure_stack_allocate. s***</span><span class="sxs-lookup"><span data-stu-id="c3ae7-129">***tx_thread_secure_stack_allocate.s***</span></span>  |  <span data-ttu-id="c3ae7-130">Güvenli yığın ayırma hizmeti için güvenli olmayan veneer.</span><span class="sxs-lookup"><span data-stu-id="c3ae7-130">Non-secure veneer for the secure stack allocate service.</span></span> |
  | <span data-ttu-id="c3ae7-131">***tx_thread_secure_stack_free. s***</span><span class="sxs-lookup"><span data-stu-id="c3ae7-131">***tx_thread_secure_stack_free.s***</span></span>      |  <span data-ttu-id="c3ae7-132">Güvenli yığın ücretsiz hizmeti için güvenli olmayan veneer.</span><span class="sxs-lookup"><span data-stu-id="c3ae7-132">Non-secure veneer for the secure stack free service.</span></span> |
  | <span data-ttu-id="c3ae7-133">***tx_thread_stack_error_handler. c***</span><span class="sxs-lookup"><span data-stu-id="c3ae7-133">***tx_thread_stack_error_handler.c***</span></span>    |  <span data-ttu-id="c3ae7-134">İş parçacığı yığın hataları için işleyici.</span><span class="sxs-lookup"><span data-stu-id="c3ae7-134">Handler for thread stack errors.</span></span> |
  | <span data-ttu-id="c3ae7-135">***tx_thread_stack_error_notify. c***</span><span class="sxs-lookup"><span data-stu-id="c3ae7-135">***tx_thread_stack_error_notify.c***</span></span>     |  <span data-ttu-id="c3ae7-136">İş parçacığı yığın hatalarını işlemek için bildirim geri aramasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="c3ae7-136">Register notification callback for handling thread stack errors.</span></span> |
