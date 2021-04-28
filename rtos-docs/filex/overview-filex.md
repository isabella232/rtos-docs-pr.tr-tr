---
title: Azure RTOS FileX 'i anlama
description: Azure RTOS FileX, Azure RTOS ThreadX ile tam olarak tümleştirilmiş ve desteklenen tüm işlemciler için kullanılabilen yüksek performanslı, dosya ayırma tablosu (FAT) ile uyumlu bir dosya sistemidir. Azure RTOS ThreadX gibi Azure RTOS FileX, küçük bir ayak izi ve yüksek performansa sahip olacak şekilde tasarlanmıştır ve bu da dosya yönetimi işlemleri gerektiren, günümüzün derin eklenmiş uygulamalar için idealdir. FileX, RAM, Azure RTOS USBX, SD kartı ve nve/veya Flash anıları dahil olmak üzere çoğu fiziksel medyayı Azure RTOS LevelX aracılığıyla destekler.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: 0a54f160c96fb3e90c2295ae72020c121d367a12
ms.sourcegitcommit: 19d50693d8f5287ba6938ae1d23eef88435ed7b1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/28/2021
ms.locfileid: "108171377"
---
# <a name="overview-of-azure-rtos-filex"></a><span data-ttu-id="9e56a-105">Azure RTOS FileX 'e genel bakış</span><span class="sxs-lookup"><span data-stu-id="9e56a-105">Overview of Azure RTOS FileX</span></span>

<span data-ttu-id="9e56a-106">Azure RTOS FileX Embedded dosya sistemi, özel olarak gömülü, gerçek zamanlı ve IoT uygulamaları için tasarlanan, Microsoft FAT dosya biçimleri için Azure RTOS 'ın gelişmiş, endüstriyel sınıf çözümüdür.</span><span class="sxs-lookup"><span data-stu-id="9e56a-106">Azure RTOS FileX embedded file system is Azure RTOS's advanced, industrial grade solution for Microsoft FAT file formats, designed specifically for deeply embedded, real-time, and IoT applications.</span></span> <span data-ttu-id="9e56a-107">Azure RTOS FileX, FAT12, FAT16, FAT32 ve exFAT gibi Microsoft 'un dosya biçimlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="9e56a-107">Azure RTOS FileX supports all of Microsoft’s file formats, including FAT12, FAT16, FAT32, and exFAT.</span></span> <span data-ttu-id="9e56a-108">FileX, [Azure RTOS LevelX](https://docs.microsoft.com/azure/rtos/levelx/)adlı bir eklenti ürünü aracılığıyla isteğe bağlı hata TOLERANSı ve Flash giyme seviyelendirme de sunar.</span><span class="sxs-lookup"><span data-stu-id="9e56a-108">FileX also offers optional fault tolerance and FLASH wear leveling via an add-on product called [Azure RTOS LevelX](https://docs.microsoft.com/azure/rtos/levelx/).</span></span> <span data-ttu-id="9e56a-109">Tüm bu, küçük bir ayak izi, Hızlı yürütme ve üstün kullanım kolaylığıyla birlikte Azure RTOS dosya x ' i en zorlu ekli IoT uygulamalarına yönelik ideal bir seçenek haline getirir.</span><span class="sxs-lookup"><span data-stu-id="9e56a-109">All of this combined with a small footprint, fast execution, and superior ease-of-use, make Azure RTOS FileX the ideal choice for the most demanding embedded IoT applications.</span></span>

## <a name="api-protocols"></a><span data-ttu-id="9e56a-110">API protokolleri</span><span class="sxs-lookup"><span data-stu-id="9e56a-110">API protocols</span></span>

### <a name="media-services"></a><span data-ttu-id="9e56a-111">Media Services</span><span class="sxs-lookup"><span data-stu-id="9e56a-111">Media Services</span></span>

- <span data-ttu-id="9e56a-112">FAT 12/16/32 ve exFAT desteği</span><span class="sxs-lookup"><span data-stu-id="9e56a-112">FAT 12/16/32 and exFAT support</span></span>
- <span data-ttu-id="9e56a-113">Minimum 6KB FLASH, 2,5 KB RAM</span><span class="sxs-lookup"><span data-stu-id="9e56a-113">Minimal 6KB FLASH, 2.5KB RAM</span></span>
- <span data-ttu-id="9e56a-114">Medya erişim Hizmetleri 'ni doldurun</span><span class="sxs-lookup"><span data-stu-id="9e56a-114">Complete media access services</span></span>
- <span data-ttu-id="9e56a-115">Sınırsız sayıda medya örneği</span><span class="sxs-lookup"><span data-stu-id="9e56a-115">Unlimited number of media instance</span></span>
- <span data-ttu-id="9e56a-116">Basit okuma/yazma mantıksal sektör sürücü arabirimi</span><span class="sxs-lookup"><span data-stu-id="9e56a-116">Simple read/write logical sector driver interface</span></span>
- <span data-ttu-id="9e56a-117">Birden çok bölüm desteği</span><span class="sxs-lookup"><span data-stu-id="9e56a-117">Multiple partition support</span></span>
- <span data-ttu-id="9e56a-118">Mantıksal kesim önbelleği</span><span class="sxs-lookup"><span data-stu-id="9e56a-118">Logical sector cache</span></span>
- <span data-ttu-id="9e56a-119">FAT giriş önbelleği</span><span class="sxs-lookup"><span data-stu-id="9e56a-119">FAT entry cache</span></span>
- <span data-ttu-id="9e56a-120">İsteğe bağlı hata toleransı desteği</span><span class="sxs-lookup"><span data-stu-id="9e56a-120">Optional fault tolerance support</span></span>
- <span data-ttu-id="9e56a-121">Ertelenmiş Ikincil FAT güncelleştirmesi</span><span class="sxs-lookup"><span data-stu-id="9e56a-121">Deferred Secondary FAT update</span></span>
- <span data-ttu-id="9e56a-122">Azure RTOS TraceX aracılığıyla sistem düzeyinde Izleme</span><span class="sxs-lookup"><span data-stu-id="9e56a-122">System-level Trace via Azure RTOS TraceX</span></span>
- <span data-ttu-id="9e56a-123">Aşağıdakiler dahil, sezgisel medya erişim API 'Leri:</span><span class="sxs-lookup"><span data-stu-id="9e56a-123">Intuitive media access APIs, including:</span></span>
  - <span data-ttu-id="9e56a-124">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="9e56a-124">fx_media_open</span></span>
  - <span data-ttu-id="9e56a-125">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="9e56a-125">fx_media_close</span></span>
  - <span data-ttu-id="9e56a-126">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="9e56a-126">fx_media_format</span></span>
  - <span data-ttu-id="9e56a-127">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="9e56a-127">fx_media_space_available</span></span>

### <a name="directory-services"></a><span data-ttu-id="9e56a-128">Dizin Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="9e56a-128">Directory Services</span></span>

- <span data-ttu-id="9e56a-129">En fazla 256 bayt yolu</span><span class="sxs-lookup"><span data-stu-id="9e56a-129">Up to 256 byte paths</span></span>
- <span data-ttu-id="9e56a-130">Uzun ve 8,3 dizin adları destekleniyor</span><span class="sxs-lookup"><span data-stu-id="9e56a-130">Long and 8.3 directory names supported</span></span>
- <span data-ttu-id="9e56a-131">Dizin oluşturma & silme</span><span class="sxs-lookup"><span data-stu-id="9e56a-131">Directory create & delete</span></span>
- <span data-ttu-id="9e56a-132">Dizin gezintisi ve geçişi</span><span class="sxs-lookup"><span data-stu-id="9e56a-132">Directory navigation and traversal</span></span>
- <span data-ttu-id="9e56a-133">Dizin öznitelikleri yönetimi</span><span class="sxs-lookup"><span data-stu-id="9e56a-133">Directory attributes management</span></span>
- <span data-ttu-id="9e56a-134">Azure RTOS TraceX aracılığıyla sistem düzeyinde Izleme</span><span class="sxs-lookup"><span data-stu-id="9e56a-134">System-level Trace via Azure RTOS TraceX</span></span>
- <span data-ttu-id="9e56a-135">Aşağıdakiler dahil, sezgisel dizin erişimi API 'Leri:</span><span class="sxs-lookup"><span data-stu-id="9e56a-135">Intuitive directory access APIs, including:</span></span>
  - <span data-ttu-id="9e56a-136">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="9e56a-136">fx_directory_create</span></span>
  - <span data-ttu-id="9e56a-137">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="9e56a-137">fx_directory_delete</span></span>
  - <span data-ttu-id="9e56a-138">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9e56a-138">fx_directory_attributes_set</span></span>
  - <span data-ttu-id="9e56a-139">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9e56a-139">fx_directory_attributes_read</span></span>
  - <span data-ttu-id="9e56a-140">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="9e56a-140">fx_directory_first_entry_find</span></span>
  - <span data-ttu-id="9e56a-141">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="9e56a-141">fx_directory_next_entry_find</span></span>

### <a name="file-services"></a><span data-ttu-id="9e56a-142">Dosya Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="9e56a-142">File Services</span></span>

- <span data-ttu-id="9e56a-143">Minimum 3.3 KB FLASH</span><span class="sxs-lookup"><span data-stu-id="9e56a-143">Minimal 3.3KB FLASH</span></span>
- <span data-ttu-id="9e56a-144">Sınırsız açık dosya</span><span class="sxs-lookup"><span data-stu-id="9e56a-144">Unlimited open files</span></span>
- <span data-ttu-id="9e56a-145">Salt okuma dosyaları birden çok kez açılabilir</span><span class="sxs-lookup"><span data-stu-id="9e56a-145">Read-only files can be opened multiple times</span></span>
- <span data-ttu-id="9e56a-146">Uzun ve 8,3 dizin adları destekleniyor</span><span class="sxs-lookup"><span data-stu-id="9e56a-146">Long and 8.3 directory names supported</span></span>
- <span data-ttu-id="9e56a-147">Ardışık dosya desteği</span><span class="sxs-lookup"><span data-stu-id="9e56a-147">Contiguous file support</span></span>
- <span data-ttu-id="9e56a-148">Hızlı arama mantığı</span><span class="sxs-lookup"><span data-stu-id="9e56a-148">Fast seek logic</span></span>
- <span data-ttu-id="9e56a-149">Kümelerin ön ayırması</span><span class="sxs-lookup"><span data-stu-id="9e56a-149">Pre-allocation of clusters</span></span>
- <span data-ttu-id="9e56a-150">Dosya oluşturma, silme ve yeniden adlandırma</span><span class="sxs-lookup"><span data-stu-id="9e56a-150">File create, delete, and rename</span></span>
- <span data-ttu-id="9e56a-151">Dosya okuma, yazma ve görme</span><span class="sxs-lookup"><span data-stu-id="9e56a-151">File read, write, and see</span></span>
- <span data-ttu-id="9e56a-152">Dosya öznitelikleri yönetimi</span><span class="sxs-lookup"><span data-stu-id="9e56a-152">File attributes management</span></span>
- <span data-ttu-id="9e56a-153">Azure RTOS TraceX aracılığıyla sistem düzeyinde Izleme</span><span class="sxs-lookup"><span data-stu-id="9e56a-153">System-level Trace via Azure RTOS TraceX</span></span>
- <span data-ttu-id="9e56a-154">Aşağıdakiler dahil, sezgisel dosya erişim API 'Leri:</span><span class="sxs-lookup"><span data-stu-id="9e56a-154">Intuitive file access APIs, including:</span></span>
  - <span data-ttu-id="9e56a-155">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="9e56a-155">fx_file_create</span></span>
  - <span data-ttu-id="9e56a-156">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="9e56a-156">fx_file_delete</span></span>
  - <span data-ttu-id="9e56a-157">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9e56a-157">fx_file_attributes_set</span></span>
  - <span data-ttu-id="9e56a-158">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9e56a-158">fx_file_attributes_read</span></span>
  - <span data-ttu-id="9e56a-159">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="9e56a-159">fx_file_read</span></span>
  - <span data-ttu-id="9e56a-160">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="9e56a-160">fx_file_seek</span></span>
  - <span data-ttu-id="9e56a-161">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="9e56a-161">fx_file_write</span></span>

## <a name="advanced-technology"></a><span data-ttu-id="9e56a-162">Gelişmiş teknoloji</span><span class="sxs-lookup"><span data-stu-id="9e56a-162">Advanced technology</span></span>

<span data-ttu-id="9e56a-163">Azure RTOS FileX, aşağıdakiler de dahil olmak üzere gelişmiş bir teknolojidir.</span><span class="sxs-lookup"><span data-stu-id="9e56a-163">Azure RTOS FileX is advanced technology, including the following.</span></span>

- <span data-ttu-id="9e56a-164">FAT 12/16/32 ve exFAT desteği</span><span class="sxs-lookup"><span data-stu-id="9e56a-164">FAT 12/16/32 and exFAT support</span></span>
- <span data-ttu-id="9e56a-165">Birden çok bölüm desteği</span><span class="sxs-lookup"><span data-stu-id="9e56a-165">Multiple partition support</span></span>
- <span data-ttu-id="9e56a-166">Otomatik ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="9e56a-166">Automatic scaling</span></span>
- <span data-ttu-id="9e56a-167">Endian nötr</span><span class="sxs-lookup"><span data-stu-id="9e56a-167">Endian neutral</span></span>
- <span data-ttu-id="9e56a-168">Uzun dosya adı ve 8,3 desteği</span><span class="sxs-lookup"><span data-stu-id="9e56a-168">Long file name and 8.3 support</span></span>
- <span data-ttu-id="9e56a-169">İsteğe bağlı hata toleransı desteği</span><span class="sxs-lookup"><span data-stu-id="9e56a-169">Optional fault tolerance support</span></span>
- <span data-ttu-id="9e56a-170">Mantıksal kesim önbelleği</span><span class="sxs-lookup"><span data-stu-id="9e56a-170">Logical sector cache</span></span>
- <span data-ttu-id="9e56a-171">FAT giriş önbelleği</span><span class="sxs-lookup"><span data-stu-id="9e56a-171">FAT entry cache</span></span>
- <span data-ttu-id="9e56a-172">Kümelerin ön ayırması</span><span class="sxs-lookup"><span data-stu-id="9e56a-172">Pre-allocation of clusters</span></span>
- <span data-ttu-id="9e56a-173">Ardışık dosya desteği</span><span class="sxs-lookup"><span data-stu-id="9e56a-173">Contiguous file support</span></span>
- <span data-ttu-id="9e56a-174">İsteğe bağlı performans ölçümleri</span><span class="sxs-lookup"><span data-stu-id="9e56a-174">Optional performance metrics</span></span>
- <span data-ttu-id="9e56a-175">Azure RTOS TraceX sistem analizi desteği</span><span class="sxs-lookup"><span data-stu-id="9e56a-175">Azure RTOS TraceX system analysis support</span></span>

## <a name="nornand-wear-leveling-azure-rtos-levelx"></a><span data-ttu-id="9e56a-176">VEYA/nve aşınma dengeleme (Azure RTOS LevelX)</span><span class="sxs-lookup"><span data-stu-id="9e56a-176">NOR/NAND Wear Leveling (Azure RTOS LevelX)</span></span>

<span data-ttu-id="9e56a-177">Azure RTOS LevelX, Microsoft 'un veya/nve FLASH giyme Dengeleme ürünüdür.</span><span class="sxs-lookup"><span data-stu-id="9e56a-177">Azure RTOS LevelX is Microsoft’s NOR/NAND FLASH wear leveling product.</span></span> <span data-ttu-id="9e56a-178">Azure RTOS LevelX, FileX ile birlikte veya uygulama için tek başına, doğrudan okuma/yazma FLASH sektör kitaplığı olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="9e56a-178">Azure RTOS LevelX can be used in conjunction with FileX or as a stand-alone, direct read/write FLASH sector library for the application.</span></span>
