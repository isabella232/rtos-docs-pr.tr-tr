---
title: Azure RTOS FileX 'i anlama
description: Azure RTOS FileX, Azure RTOS ThreadX ile tam olarak tümleştirilmiş ve desteklenen tüm işlemciler için kullanılabilen yüksek performanslı, dosya ayırma tablosu (FAT) ile uyumlu bir dosya sistemidir. Azure RTOS ThreadX gibi Azure RTOS FileX, küçük bir ayak izi ve yüksek performansa sahip olacak şekilde tasarlanmıştır ve bu da dosya yönetimi işlemleri gerektiren, günümüzün derin eklenmiş uygulamalar için idealdir. FileX, RAM, Azure RTOS USBX, SD kartı ve nve/veya Flash anıları dahil olmak üzere çoğu fiziksel medyayı Azure RTOS LevelX aracılığıyla destekler.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: a3a20c8ced3426399ceedf6994c872ce7aec93c3
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104827322"
---
# <a name="overview-of-azure-rtos-filex"></a><span data-ttu-id="58a4f-105">Azure RTOS FileX 'e genel bakış</span><span class="sxs-lookup"><span data-stu-id="58a4f-105">Overview of Azure RTOS FileX</span></span>

<span data-ttu-id="58a4f-106">Azure RTOS FileX Embedded dosya sistemi, özel olarak gömülü, gerçek zamanlı ve IoT uygulamaları için tasarlanan, Microsoft FAT dosya biçimleri için Azure RTOS 'ın gelişmiş, endüstriyel sınıf çözümüdür.</span><span class="sxs-lookup"><span data-stu-id="58a4f-106">Azure RTOS FileX embedded file system is Azure RTOS's advanced, industrial grade solution for Microsoft FAT file formats, designed specifically for deeply embedded, real-time, and IoT applications.</span></span> <span data-ttu-id="58a4f-107">Azure RTOS FileX, FAT12, FAT16, FAT32 ve exFAT gibi Microsoft 'un dosya biçimlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="58a4f-107">Azure RTOS FileX supports all of Microsoft’s file formats, including FAT12, FAT16, FAT32, and exFAT.</span></span> <span data-ttu-id="58a4f-108">FileX, [Azure RTOS LevelX](https://docs.microsoft.com/azure/rtos/levelx/)adlı bir eklenti ürünü aracılığıyla isteğe bağlı hata TOLERANSı ve Flash giyme seviyelendirme de sunar.</span><span class="sxs-lookup"><span data-stu-id="58a4f-108">FileX also offers optional fault tolerance and FLASH wear leveling via an add-on product called [Azure RTOS LevelX](https://docs.microsoft.com/azure/rtos/levelx/).</span></span> <span data-ttu-id="58a4f-109">Tüm bu, küçük bir ayak izi, Hızlı yürütme ve üstün kullanım kolaylığıyla birlikte Azure RTOS dosya x ' i en zorlu ekli IoT uygulamalarına yönelik ideal bir seçenek haline getirir.</span><span class="sxs-lookup"><span data-stu-id="58a4f-109">All of this combined with a small footprint, fast execution, and superior ease-of-use, make Azure RTOS FileX the ideal choice for the most demanding embedded IoT applications.</span></span>

## <a name="api-protocols"></a><span data-ttu-id="58a4f-110">API protokolleri</span><span class="sxs-lookup"><span data-stu-id="58a4f-110">API protocols</span></span>

### <a name="azure-rtos-filex-api"></a><span data-ttu-id="58a4f-111">Azure RTOS FileX API 'SI</span><span class="sxs-lookup"><span data-stu-id="58a4f-111">Azure RTOS FileX API</span></span>

- <span data-ttu-id="58a4f-112">Sezgisel ve tutarlı API</span><span class="sxs-lookup"><span data-stu-id="58a4f-112">Intuitive and consistent API</span></span>
- <span data-ttu-id="58a4f-113">İsim-fiil adlandırma kuralı</span><span class="sxs-lookup"><span data-stu-id="58a4f-113">Noun-verb naming convention</span></span>
- <span data-ttu-id="58a4f-114">Tüm API 'Ler, FileX olarak kolayca tanımlanabilmesi için önde gelen *fx_* sahiptir</span><span class="sxs-lookup"><span data-stu-id="58a4f-114">All APIs have leading *fx_* to easily identify as FileX</span></span>
- <span data-ttu-id="58a4f-115">API 'Lerin engellenmesi isteğe bağlı iş parçacığı zaman aşımına uğradı</span><span class="sxs-lookup"><span data-stu-id="58a4f-115">Blocking APIs have optional thread timeout</span></span>
- <span data-ttu-id="58a4f-116">Medya ve dosya işlemleri için isteğe bağlı Kullanıcı bildirimi geri çağırmaları</span><span class="sxs-lookup"><span data-stu-id="58a4f-116">Optional user-notification callbacks for media and file operations</span></span>
- <span data-ttu-id="58a4f-117">Daha fazla ayrıntı için lütfen bkz. [Azure RTOS Fılex Kullanıcı Kılavuzu](about-this-guide.md)</span><span class="sxs-lookup"><span data-stu-id="58a4f-117">Please see [Azure RTOS FileX User Guide](about-this-guide.md) for more details</span></span>

### <a name="media-services"></a><span data-ttu-id="58a4f-118">Media Services</span><span class="sxs-lookup"><span data-stu-id="58a4f-118">Media Services</span></span>

- <span data-ttu-id="58a4f-119">FAT 12/16/32 ve exFAT desteği</span><span class="sxs-lookup"><span data-stu-id="58a4f-119">FAT 12/16/32 and exFAT support</span></span>
- <span data-ttu-id="58a4f-120">Minimum 6KB FLASH, 2,5 KB RAM</span><span class="sxs-lookup"><span data-stu-id="58a4f-120">Minimal 6KB FLASH, 2.5KB RAM</span></span>
- <span data-ttu-id="58a4f-121">Medya erişim Hizmetleri 'ni doldurun</span><span class="sxs-lookup"><span data-stu-id="58a4f-121">Complete media access services</span></span>
- <span data-ttu-id="58a4f-122">Sınırsız sayıda medya örneği</span><span class="sxs-lookup"><span data-stu-id="58a4f-122">Unlimited number of media instance</span></span>
- <span data-ttu-id="58a4f-123">Basit okuma/yazma mantıksal sektör sürücü arabirimi</span><span class="sxs-lookup"><span data-stu-id="58a4f-123">Simple read/write logical sector driver interface</span></span>
- <span data-ttu-id="58a4f-124">Birden çok bölüm desteği</span><span class="sxs-lookup"><span data-stu-id="58a4f-124">Multiple partition support</span></span>
- <span data-ttu-id="58a4f-125">Mantıksal kesim önbelleği</span><span class="sxs-lookup"><span data-stu-id="58a4f-125">Logical sector cache</span></span>
- <span data-ttu-id="58a4f-126">FAT giriş önbelleği</span><span class="sxs-lookup"><span data-stu-id="58a4f-126">FAT entry cache</span></span>
- <span data-ttu-id="58a4f-127">İsteğe bağlı hata toleransı desteği</span><span class="sxs-lookup"><span data-stu-id="58a4f-127">Optional fault tolerance support</span></span>
- <span data-ttu-id="58a4f-128">Ertelenmiş Ikincil FAT güncelleştirmesi</span><span class="sxs-lookup"><span data-stu-id="58a4f-128">Deferred Secondary FAT update</span></span>
- <span data-ttu-id="58a4f-129">Azure RTOS TraceX aracılığıyla sistem düzeyinde Izleme</span><span class="sxs-lookup"><span data-stu-id="58a4f-129">System-level Trace via Azure RTOS TraceX</span></span>
- <span data-ttu-id="58a4f-130">Aşağıdakiler dahil, sezgisel medya erişim API 'Leri:</span><span class="sxs-lookup"><span data-stu-id="58a4f-130">Intuitive media access APIs, including:</span></span>
  - <span data-ttu-id="58a4f-131">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="58a4f-131">fx_media_open</span></span>
  - <span data-ttu-id="58a4f-132">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="58a4f-132">fx_media_close</span></span>
  - <span data-ttu-id="58a4f-133">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="58a4f-133">fx_media_format</span></span>
  - <span data-ttu-id="58a4f-134">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="58a4f-134">fx_media_space_available</span></span>

### <a name="directory-services"></a><span data-ttu-id="58a4f-135">Dizin Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="58a4f-135">Directory Services</span></span>

- <span data-ttu-id="58a4f-136">En fazla 256 bayt yolu</span><span class="sxs-lookup"><span data-stu-id="58a4f-136">Up to 256 byte paths</span></span>
- <span data-ttu-id="58a4f-137">Uzun ve 8,3 dizin adları destekleniyor</span><span class="sxs-lookup"><span data-stu-id="58a4f-137">Long and 8.3 directory names supported</span></span>
- <span data-ttu-id="58a4f-138">Dizin oluşturma & silme</span><span class="sxs-lookup"><span data-stu-id="58a4f-138">Directory create & delete</span></span>
- <span data-ttu-id="58a4f-139">Dizin gezintisi ve geçişi</span><span class="sxs-lookup"><span data-stu-id="58a4f-139">Directory navigation and traversal</span></span>
- <span data-ttu-id="58a4f-140">Dizin öznitelikleri yönetimi</span><span class="sxs-lookup"><span data-stu-id="58a4f-140">Directory attributes management</span></span>
- <span data-ttu-id="58a4f-141">Azure RTOS TraceX aracılığıyla sistem düzeyinde Izleme</span><span class="sxs-lookup"><span data-stu-id="58a4f-141">System-level Trace via Azure RTOS TraceX</span></span>
- <span data-ttu-id="58a4f-142">Aşağıdakiler dahil, sezgisel dizin erişimi API 'Leri:</span><span class="sxs-lookup"><span data-stu-id="58a4f-142">Intuitive directory access APIs, including:</span></span>
  - <span data-ttu-id="58a4f-143">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="58a4f-143">fx_directory_create</span></span>
  - <span data-ttu-id="58a4f-144">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="58a4f-144">fx_directory_delete</span></span>
  - <span data-ttu-id="58a4f-145">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="58a4f-145">fx_directory_attributes_set</span></span>
  - <span data-ttu-id="58a4f-146">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="58a4f-146">fx_directory_attributes_read</span></span>
  - <span data-ttu-id="58a4f-147">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="58a4f-147">fx_directory_first_entry_find</span></span>
  - <span data-ttu-id="58a4f-148">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="58a4f-148">fx_directory_next_entry_find</span></span>

### <a name="file-services"></a><span data-ttu-id="58a4f-149">Dosya Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="58a4f-149">File Services</span></span>

- <span data-ttu-id="58a4f-150">Minimum 3.3 KB FLASH</span><span class="sxs-lookup"><span data-stu-id="58a4f-150">Minimal 3.3KB FLASH</span></span>
- <span data-ttu-id="58a4f-151">Sınırsız açık dosya</span><span class="sxs-lookup"><span data-stu-id="58a4f-151">Unlimited open files</span></span>
- <span data-ttu-id="58a4f-152">Salt okuma dosyaları birden çok kez açılabilir</span><span class="sxs-lookup"><span data-stu-id="58a4f-152">Read-only files can be opened multiple times</span></span>
- <span data-ttu-id="58a4f-153">Uzun ve 8,3 dizin adları destekleniyor</span><span class="sxs-lookup"><span data-stu-id="58a4f-153">Long and 8.3 directory names supported</span></span>
- <span data-ttu-id="58a4f-154">Ardışık dosya desteği</span><span class="sxs-lookup"><span data-stu-id="58a4f-154">Contiguous file support</span></span>
- <span data-ttu-id="58a4f-155">Hızlı arama mantığı</span><span class="sxs-lookup"><span data-stu-id="58a4f-155">Fast seek logic</span></span>
- <span data-ttu-id="58a4f-156">Kümelerin ön ayırması</span><span class="sxs-lookup"><span data-stu-id="58a4f-156">Pre-allocation of clusters</span></span>
- <span data-ttu-id="58a4f-157">Dosya oluşturma, silme ve yeniden adlandırma</span><span class="sxs-lookup"><span data-stu-id="58a4f-157">File create, delete, and rename</span></span>
- <span data-ttu-id="58a4f-158">Dosya okuma, yazma ve görme</span><span class="sxs-lookup"><span data-stu-id="58a4f-158">File read, write, and see</span></span>
- <span data-ttu-id="58a4f-159">Dosya öznitelikleri yönetimi</span><span class="sxs-lookup"><span data-stu-id="58a4f-159">File attributes management</span></span>
- <span data-ttu-id="58a4f-160">Azure RTOS TraceX aracılığıyla sistem düzeyinde Izleme</span><span class="sxs-lookup"><span data-stu-id="58a4f-160">System-level Trace via Azure RTOS TraceX</span></span>
- <span data-ttu-id="58a4f-161">Aşağıdakiler dahil, sezgisel dosya erişim API 'Leri:</span><span class="sxs-lookup"><span data-stu-id="58a4f-161">Intuitive file access APIs, including:</span></span>
  - <span data-ttu-id="58a4f-162">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="58a4f-162">fx_file_create</span></span>
  - <span data-ttu-id="58a4f-163">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="58a4f-163">fx_file_delete</span></span>
  - <span data-ttu-id="58a4f-164">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="58a4f-164">fx_file_attributes_set</span></span>
  - <span data-ttu-id="58a4f-165">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="58a4f-165">fx_file_attributes_read</span></span>
  - <span data-ttu-id="58a4f-166">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="58a4f-166">fx_file_read</span></span>
  - <span data-ttu-id="58a4f-167">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="58a4f-167">fx_file_seek</span></span>
  - <span data-ttu-id="58a4f-168">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="58a4f-168">fx_file_write</span></span>

## <a name="small-footprint"></a><span data-ttu-id="58a4f-169">Küçük ayak izi</span><span class="sxs-lookup"><span data-stu-id="58a4f-169">Small-footprint</span></span>

<span data-ttu-id="58a4f-170">Azure RTOS FileX Embedded dosya sistemi, temel dosya okuma/yazma desteği için 8,6 KB ile 12 KB arasında bir remarkalı küçük boyut içerir.</span><span class="sxs-lookup"><span data-stu-id="58a4f-170">Azure RTOS FileX embedded file system has a remarkably small minimal footprint of 8.6 KB to 12 KB for basic file read/write support.</span></span> <span data-ttu-id="58a4f-171">En az Azure RTOS FileX RAM kullanımı, tek bir medya örneği için 1,8 KB ve yalnızca 512 baytlık bir mantıksal kesim önbelleğidir.</span><span class="sxs-lookup"><span data-stu-id="58a4f-171">Minimal Azure RTOS FileX RAM usage is on the order of 1.8 KB for one media instance and with only a 512-byte logical sector cache.</span></span> <span data-ttu-id="58a4f-172">Azure RTOS ThreadX gibi Azure RTOS dosya x boyutu, uygulama tarafından kullanılan hizmetlere göre otomatik olarak ölçeklendirilir.</span><span class="sxs-lookup"><span data-stu-id="58a4f-172">Like Azure RTOS ThreadX, the size of Azure RTOS FileX automatically scales based on the services used by the application.</span></span> <span data-ttu-id="58a4f-173">Bu, karmaşık yapılandırma ve derleme parametrelerine gerek duymayı neredeyse ortadan kaldırır, böylece geliştirici daha kolay hale getirir.</span><span class="sxs-lookup"><span data-stu-id="58a4f-173">This virtually eliminates the need for complicated configuration and builds parameters, making things easier for the developer.</span></span>

## <a name="fast-execution"></a><span data-ttu-id="58a4f-174">Hızlı yürütme</span><span class="sxs-lookup"><span data-stu-id="58a4f-174">Fast execution</span></span>

<span data-ttu-id="58a4f-175">Azure RTOS FileX, bir mantıksal kesim önbelleğinin yanı sıra bir FAT giriş önbelleği de sağlar.</span><span class="sxs-lookup"><span data-stu-id="58a4f-175">Azure RTOS FileX provides a logical sector cache as well as a FAT entry cache.</span></span> <span data-ttu-id="58a4f-176">Her ikisinin de boyutları uygulamanın doğrudan denetimi altındadır.</span><span class="sxs-lookup"><span data-stu-id="58a4f-176">The sizes of both are under direct control of the application.</span></span> <span data-ttu-id="58a4f-177">Ayrıca, Azure RTOS FileX, ardışık küme ayırma ve doğrudan ardışık küme okuma ve yazma sağlar.</span><span class="sxs-lookup"><span data-stu-id="58a4f-177">In addition, Azure RTOS FileX provides contiguous cluster allocation and direct consecutive cluster reading and writing.</span></span> <span data-ttu-id="58a4f-178">Bütün kesimlerin okuma/yazma istekleri doğrudan uygulama arabelleği ve medya arasında yapılır; diğer bir deyişle, ara belleğe alma yapılmaz.</span><span class="sxs-lookup"><span data-stu-id="58a4f-178">Read/write requests of whole sectors are done directly between the application buffer and the media – that is, no intermediate buffering is done.</span></span> <span data-ttu-id="58a4f-179">Tüm bu ve genel performans odaklı bir tasarım felseno, Azure RTOS dosya x 'in olası en hızlı performansı elde etmesine yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="58a4f-179">All of this and a general performance-oriented design philosophy helps Azure RTOS FileX achieve the fastest possible performance.</span></span>

## <a name="advanced-technology"></a><span data-ttu-id="58a4f-180">Gelişmiş teknoloji</span><span class="sxs-lookup"><span data-stu-id="58a4f-180">Advanced technology</span></span>

<span data-ttu-id="58a4f-181">Azure RTOS FileX, aşağıdakiler de dahil olmak üzere gelişmiş bir teknolojidir.</span><span class="sxs-lookup"><span data-stu-id="58a4f-181">Azure RTOS FileX is advanced technology, including the following.</span></span>

- <span data-ttu-id="58a4f-182">FAT 12/16/32 ve exFAT desteği</span><span class="sxs-lookup"><span data-stu-id="58a4f-182">FAT 12/16/32 and exFAT support</span></span>
- <span data-ttu-id="58a4f-183">Birden çok bölüm desteği</span><span class="sxs-lookup"><span data-stu-id="58a4f-183">Multiple partition support</span></span>
- <span data-ttu-id="58a4f-184">Otomatik ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="58a4f-184">Automatic scaling</span></span>
- <span data-ttu-id="58a4f-185">Endian nötr</span><span class="sxs-lookup"><span data-stu-id="58a4f-185">Endian neutral</span></span>
- <span data-ttu-id="58a4f-186">Uzun dosya adı ve 8,3 desteği</span><span class="sxs-lookup"><span data-stu-id="58a4f-186">Long file name and 8.3 support</span></span>
- <span data-ttu-id="58a4f-187">İsteğe bağlı hata toleransı desteği</span><span class="sxs-lookup"><span data-stu-id="58a4f-187">Optional fault tolerance support</span></span>
- <span data-ttu-id="58a4f-188">Mantıksal kesim önbelleği</span><span class="sxs-lookup"><span data-stu-id="58a4f-188">Logical sector cache</span></span>
- <span data-ttu-id="58a4f-189">FAT giriş önbelleği</span><span class="sxs-lookup"><span data-stu-id="58a4f-189">FAT entry cache</span></span>
- <span data-ttu-id="58a4f-190">Kümelerin ön ayırması</span><span class="sxs-lookup"><span data-stu-id="58a4f-190">Pre-allocation of clusters</span></span>
- <span data-ttu-id="58a4f-191">Ardışık dosya desteği</span><span class="sxs-lookup"><span data-stu-id="58a4f-191">Contiguous file support</span></span>
- <span data-ttu-id="58a4f-192">İsteğe bağlı performans ölçümleri</span><span class="sxs-lookup"><span data-stu-id="58a4f-192">Optional performance metrics</span></span>
- <span data-ttu-id="58a4f-193">Azure RTOS TraceX sistem analizi desteği</span><span class="sxs-lookup"><span data-stu-id="58a4f-193">Azure RTOS TraceX system analysis support</span></span>

## <a name="nornand-wear-leveling-azure-rtos-levelx"></a><span data-ttu-id="58a4f-194">VEYA/nve aşınma dengeleme (Azure RTOS LevelX)</span><span class="sxs-lookup"><span data-stu-id="58a4f-194">NOR/NAND Wear Leveling (Azure RTOS LevelX)</span></span>

<span data-ttu-id="58a4f-195">Azure RTOS LevelX, Microsoft 'un veya/nve FLASH giyme Dengeleme ürünüdür.</span><span class="sxs-lookup"><span data-stu-id="58a4f-195">Azure RTOS LevelX is Microsoft’s NOR/NAND FLASH wear leveling product.</span></span> <span data-ttu-id="58a4f-196">Azure RTOS LevelX, FileX ile birlikte veya uygulama için tek başına, doğrudan okuma/yazma FLASH sektör kitaplığı olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="58a4f-196">Azure RTOS LevelX can be used in conjunction with FileX or as a stand-alone, direct read/write FLASH sector library for the application.</span></span>

## <a name="fastest-time-to-market"></a><span data-ttu-id="58a4f-197">En hızlı pazar süresi</span><span class="sxs-lookup"><span data-stu-id="58a4f-197">Fastest time-to-market</span></span>

<span data-ttu-id="58a4f-198">Azure RTOS FileX 'i yüklemek, öğrenmek, kullanmak, hata ayıklamak, doğrulamak, onaylamak ve sürdürmek kolaydır.</span><span class="sxs-lookup"><span data-stu-id="58a4f-198">Azure RTOS FileX is easy to install, learn, use, debug, verify, certify, and maintain.</span></span> <span data-ttu-id="58a4f-199">Sonuç olarak, Azure RTOS FileX, katıştırılmış IoT cihazları için en popüler FAT dosya sistemlerinden biridir.</span><span class="sxs-lookup"><span data-stu-id="58a4f-199">As a result, Azure RTOS FileX is one of the most popular FAT file systems for embedded IoT devices.</span></span> <span data-ttu-id="58a4f-200">Aşağıda, tutarlı bir pazar süresi avantajımız için bazı nedenler verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="58a4f-200">The following are some reasons for our consistent time-to-market advantage:</span></span>

- <span data-ttu-id="58a4f-201">Kalite belgeleri: lütfen [Azure RTOS FileX Kullanıcı Kılavuzumuzu](about-this-guide.md) gözden geçirin ve kendiniz görün!</span><span class="sxs-lookup"><span data-stu-id="58a4f-201">Quality Documentation – please review our [Azure RTOS FileX User Guide](about-this-guide.md) and see for yourself!</span></span>
- <span data-ttu-id="58a4f-202">Tüm kaynak kodu kullanılabilirliği</span><span class="sxs-lookup"><span data-stu-id="58a4f-202">Complete Source Code Availability</span></span>
- <span data-ttu-id="58a4f-203">Kullanımı kolay API</span><span class="sxs-lookup"><span data-stu-id="58a4f-203">Easy-to-use API</span></span>
- <span data-ttu-id="58a4f-204">Kapsamlı ve gelişmiş özellik kümesi</span><span class="sxs-lookup"><span data-stu-id="58a4f-204">Comprehensive and Advanced Feature Set</span></span>

## <a name="pre-certified--by-tuv-and-ul-to-many-safety-standards"></a><span data-ttu-id="58a4f-205">TUV ve UL ile birçok güvenlik standartlarına ön sertifikalı</span><span class="sxs-lookup"><span data-stu-id="58a4f-205">Pre-certified  by TUV and UL to many safety standards</span></span>

![SGS-TUV Saar](./media/overview-filex/partener-logo-sgs-tuv-saar-2.png)

<span data-ttu-id="58a4f-207">Azure RTOS FileX, SGS-TUV Saar tarafından, ıEC-61508 SIL 4, ıEC-62304 SW Safety Class C, ISO 26262 asıl D ve EN 50128 'e göre güvenlik açısından kritik sistemlerde kullanılmak üzere sertifikalandırilmiştir.</span><span class="sxs-lookup"><span data-stu-id="58a4f-207">Azure RTOS FileX has been certified by SGS-TUV Saar for use in safety-critical systems, according to IEC-61508 SIL 4, IEC-62304  SW Safety Class C, ISO 26262 ASIL D and EN 50128.</span></span> <span data-ttu-id="58a4f-208">Sertifika, "elektrik, elektronik ve programlanabilir elektronik güvenliği ile ilgili sistemlerin Işlevsel güvenliği" için ıEC-61508, ıEC-62304, ISO 26262 ve 50128 EN yüksek güvenlik bütünlüğü düzeyleri için, FileX 'in güvenlik açısından ilgili yazılımlar geliştirmesinde kullanılabileceğini onaylar.</span><span class="sxs-lookup"><span data-stu-id="58a4f-208">The certification confirms that FileX can be used in the development of safety-related software for the highest safety integrity levels of IEC-61508, IEC-62304, ISO 26262 and EN 50128 for the “Functional Safety of electrical, electronic, and programmable electronic safety-related systems.”</span></span> <span data-ttu-id="58a4f-209">Almanya 'nın SGS-Group ve TUV Saarland 'ın Birleşik bir tezi aracılığıyla oluşturulan SGS-TUV Saar, dünya çapındaki güvenlikle ilgili sistemler için eklenmiş yazılımları test etmek, denetlemek, doğrulamak ve sertifika almak için önde gelen acalacaklandırılan şirkete gelmiştir.</span><span class="sxs-lookup"><span data-stu-id="58a4f-209">SGS-TUV Saar, formed through a joint venture of Germany’s SGS-Group and TUV Saarland, has become the leading accredited, independent company for testing, auditing, verifying, and certifying embedded software for safety-related systems worldwide.</span></span> <span data-ttu-id="58a4f-210">Endüstriyel güvenlik standardı IEC 61508 ve bundan türetilmiş tüm standartlar, IEC-62304, ISO 26262 ve en 50128 dahil, elektrik, elektronik ve programlanabilir elektronik güvenliği ile ilgili tıbbi cihazların, işlem denetim sistemlerinin, endüstriyel makinelerin, otomobil ve demiryolu denetim sistemlerinin işlevsel güvenlik düzeyini güvence altına almak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="58a4f-210">The industrial safety standard IEC 61508, and all standards that are derived from it, including IEC-62304, ISO 26262 and EN 50128, are used to assure the functional safety of electrical, electronic, and programmable electronic safety-related medical devices, process control systems, industrial machinery, automobiles, and railway control systems.</span></span>

:::image type="content" source="media/overview-filex/cru-logo-certification.png" alt-text="CRU UL sertifikası":::

<span data-ttu-id="58a4f-212">Azure RTOS Fılex, ınımg 60730-1 Ek H, CSA E60730-1 Ek H, ıEC 60730-1 Ek H, UL 60335-1 ek R, ıEC 60335-1 ek R 1998 ve programlanabilir.</span><span class="sxs-lookup"><span data-stu-id="58a4f-212">Azure RTOS FileX has been recognized by UL for compliance with UL 60730-1 Annex H, CSA E60730-1 Annex H, IEC 60730-1 Annex H, UL 60335-1 Annex R, IEC 60335-1 Annex R, and UL 1998 safety standards for software in programmable components.</span></span> <span data-ttu-id="58a4f-213">UL, en fazla uzman sürmek güvenlik çözümleri sunan küresel, bağımsız bir güvenlik bilimi şirketidir. Bu, elektrik, yenilenebilir enerji ve Nanotechnology için genel olarak elektrik 'yi benimseme özelliğine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="58a4f-213">UL is a global, independent, safety-science company with more than a century of expertise innovating safety solutions, ranging from the public adoption of electricity to breakthroughs in sustainability, renewable energy, and nanotechnology.</span></span>

<span data-ttu-id="58a4f-214">TUV ve UL sertifikalarıyla ilişkili yapıtlar (sertifika, güvenlik el kitabı, test raporu vb.) satış için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="58a4f-214">Artifacts (Certificate, Safety Manual, Test Report, etc.) associated with the TUV and UL certifications are available for sale.</span></span>

<span data-ttu-id="58a4f-215">Uygulamanın ek sertifikaya ihtiyacı olduğu durumlarda, gerçek donanım platformunu kullanarak ve hatta uygulama kodunu kapsayan çeşitli standartlara anahtar sertifikası sağlamak için Microsoft aracılığıyla bir sertifika hizmeti kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="58a4f-215">In cases where the application needs additional certification, a certification service is available through Microsoft for providing turn-key certification to various standards using the actual hardware platform and even covering the application code.</span></span>

## <a name="one-simple-license"></a><span data-ttu-id="58a4f-216">Tek bir basit lisans</span><span class="sxs-lookup"><span data-stu-id="58a4f-216">One Simple License</span></span>

<span data-ttu-id="58a4f-217">Önceden lisanslanmış cihazlara dağıtıldığında, diğer tüm cihazların basit bir yıllık lisansa sahip olması için, kaynak kodu ve test lisansları için ücret ve maliyet kullanımı maliyeti yoktur.</span><span class="sxs-lookup"><span data-stu-id="58a4f-217">There is no cost to use and test the source code and no cost for production licenses when deployed to pre-licensed devices, all other devices need a simple annual license.</span></span>

## <a name="full-highest-quality-source-code"></a><span data-ttu-id="58a4f-218">Tam, en yüksek kaliteli kaynak kodu</span><span class="sxs-lookup"><span data-stu-id="58a4f-218">Full, highest-quality source code</span></span>

<span data-ttu-id="58a4f-219">Yıl boyunca, FileX kaynak kodu çubuğun kalitesini ve anlamayı kolay bir şekilde ayarladı.</span><span class="sxs-lookup"><span data-stu-id="58a4f-219">Throughout the years, FileX source code has set the bar in quality and ease of understanding.</span></span> <span data-ttu-id="58a4f-220">Ayrıca, dosya başına bir işleve sahip olma kuralı, kolay kaynak gezintisi için sağlar.</span><span class="sxs-lookup"><span data-stu-id="58a4f-220">In addition, the convention of having one function per file provides for easy source navigation.</span></span>

## <a name="supports-most-popular-architectures"></a><span data-ttu-id="58a4f-221">Popüler mimarilerin çoğunu destekler</span><span class="sxs-lookup"><span data-stu-id="58a4f-221">Supports most popular architectures</span></span>

<span data-ttu-id="58a4f-222">Azure RTOS FileX, en popüler 32/64 bit mikro işlemciler, kullanıma hazır, tam olarak sınanmış ve aşağıdakiler dahil olmak üzere tam olarak desteklenmiş şekilde çalışır:</span><span class="sxs-lookup"><span data-stu-id="58a4f-222">Azure RTOS FileX runs on most popular 32/64-bit microprocessors, out-of-the-box, fully tested and fully supported, including the following:</span></span>

<span data-ttu-id="58a4f-223">**Analog cihazlar**: parça, BlackICE, CM4xx</span><span class="sxs-lookup"><span data-stu-id="58a4f-223">**Analog Devices**: SHARC, Blackfin, CM4xx</span></span>

<span data-ttu-id="58a4f-224">**Andes Core**: RISC-V</span><span class="sxs-lookup"><span data-stu-id="58a4f-224">**Andes Core**: RISC-V</span></span>

<span data-ttu-id="58a4f-225">**Ambiqmicro**: Apollo MCUs</span><span class="sxs-lookup"><span data-stu-id="58a4f-225">**Ambiqmicro**: Apollo MCUs</span></span>

<span data-ttu-id="58a4f-226">**ARM**: ARM7, ARM9, ARM11, Cortex-M0/m3/M4/M7/A15/a5/A7/A8/A9/A5X 64-bı/A7x 64-bit/R4/R5, TrustZone ARMv8-ı</span><span class="sxs-lookup"><span data-stu-id="58a4f-226">**ARM**: ARM7, ARM9, ARM11, Cortex-M0/M3/M4/M7/A15/A5/A7/A8/A9/A5x 64-bi/A7x 64-bit/R4/R5, TrustZone ARMv8-M</span></span>

<span data-ttu-id="58a4f-227">**Temposunda**: xtensa, elmas</span><span class="sxs-lookup"><span data-stu-id="58a4f-227">**Cadence**: Xtensa, Diamond</span></span>

<span data-ttu-id="58a4f-228">**Ceva**: PSoC, PSoC 4, PSoC 5, PSoC 6, FM0 +, FM3, MF4, Werwifi</span><span class="sxs-lookup"><span data-stu-id="58a4f-228">**CEVA**: PSoC, PSoC 4, PSoC 5, PSoC 6, FM0+, FM3, MF4, WICED WiFi</span></span>

<span data-ttu-id="58a4f-229">**Cypress**: RISC-V</span><span class="sxs-lookup"><span data-stu-id="58a4f-229">**Cypress**: RISC-V</span></span>

<span data-ttu-id="58a4f-230">**Ensilica**: ESI-RISC</span><span class="sxs-lookup"><span data-stu-id="58a4f-230">**EnSilica**: eSi-RISC</span></span>

<span data-ttu-id="58a4f-231">**Infineon**: XMC1000, XMC4000, kanore</span><span class="sxs-lookup"><span data-stu-id="58a4f-231">**Infineon**: XMC1000, XMC4000, TriCore</span></span>

<span data-ttu-id="58a4f-232">**Intel**; **Intel FPGA**: X36/Pentium, XSCALE, NIOS II, Cyclone, varış a 10</span><span class="sxs-lookup"><span data-stu-id="58a4f-232">**Intel**; **Intel FPGA**: x36/Pentium, XScale, NIOS II, Cyclone, Arria 10</span></span>

<span data-ttu-id="58a4f-233">**Mikro yonga**: AVR32, ARM7, ARM9, Cortex-M3/M4/M7, SAM3/4/7/9/A/C/D/E/G/L/ZF, PIC24/PIC32</span><span class="sxs-lookup"><span data-stu-id="58a4f-233">**Microchip**: AVR32, ARM7, ARM9, Cortex-M3/M4/M7, SAM3/4/7/9/A/C/D/E/G/L/SV, PIC24/PIC32</span></span>

<span data-ttu-id="58a4f-234">**Mikro yarı**: RISC-V</span><span class="sxs-lookup"><span data-stu-id="58a4f-234">**Microsemi**: RISC-V</span></span>

<span data-ttu-id="58a4f-235">**NXP**: LPC, ARM7, ARM9, PowerPC, 68 K, I.MX, ColdFire, Kinetis Cortex-M3/M4</span><span class="sxs-lookup"><span data-stu-id="58a4f-235">**NXP**: LPC, ARM7, ARM9, PowerPC, 68 K, i.MX, ColdFire, Kinetis Cortex-M3/M4</span></span>

<span data-ttu-id="58a4f-236">**Renesas**: SH, HS, v850, RX, Rz, Synergy</span><span class="sxs-lookup"><span data-stu-id="58a4f-236">**Renesas**: SH, HS, V850, RX, RZ, Synergy</span></span>

<span data-ttu-id="58a4f-237">**Silicon** Labs: EFM32</span><span class="sxs-lookup"><span data-stu-id="58a4f-237">**Silicon** Labs: EFM32</span></span>

<span data-ttu-id="58a4f-238">**Synopsys**: Arc 600, 700, Arc Em, Arc HS</span><span class="sxs-lookup"><span data-stu-id="58a4f-238">**Synopsys**: ARC 600, 700, ARC EM, ARC HS</span></span>

<span data-ttu-id="58a4f-239">**St**: STM32, ARM7, ARM9, Cortex-M3/M4/M7</span><span class="sxs-lookup"><span data-stu-id="58a4f-239">**ST**: STM32, ARM7, ARM9, Cortex-M3/M4/M7</span></span>

<span data-ttu-id="58a4f-240">**TL**: C5xxx, C6xxx, Stellardo, Sitara, Tiva-C</span><span class="sxs-lookup"><span data-stu-id="58a4f-240">**Tl**: C5xxx, C6xxx, Stellaris, Sitara, Tiva-C</span></span>

<span data-ttu-id="58a4f-241">**Dalga bilgi işlem**: MIPS32 4k, 24 K, 34 k, 1004 k, ver 5k, mikro Aptiv, ınteraptiv, Proaptiv, M-class</span><span class="sxs-lookup"><span data-stu-id="58a4f-241">**Wave Computing**: MIPS32 4K, 24 K, 34 K, 1004 K, MIPS64 5K, microAptiv, interAptiv, proAptiv, M-Class</span></span>

<span data-ttu-id="58a4f-242">**Xilinx**: mikro Blaze, PowerPC 405, zynq, Zynq UltraSCALE</span><span class="sxs-lookup"><span data-stu-id="58a4f-242">**Xilinx**: MicroBlaze, PowerPC 405, ZYNQ, ZYNQ UltraSCALE</span></span>

<span data-ttu-id="58a4f-243">*Listelenen tüm zamanlama ve boyut rakamları tahminlerdir ve geliştirme platformunuzun farklı olabilir.*</span><span class="sxs-lookup"><span data-stu-id="58a4f-243">*All timing and size figures listed are estimates and may be different on your development platform.*</span></span>
