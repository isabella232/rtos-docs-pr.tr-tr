---
title: Bölüm 6-Azure RTOS FileX hataya dayanıklı modül
description: Bu bölümde, medya güç kaybettiğinde veya dosya yazma işleminin ortasında çıkarıldığında dosya sistemi bütünlüğünü sürdürmek üzere tasarlanan Azure RTOS FileX hata toleranslı modülünün bir açıklaması bulunur.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 68a24f0345a2c4d3e824270699b00a2daab32f8e
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826506"
---
# <a name="chapter-6---azure-rtos-filex-fault-tolerant-module"></a><span data-ttu-id="54a15-103">Bölüm 6-Azure RTOS FileX hataya dayanıklı modül</span><span class="sxs-lookup"><span data-stu-id="54a15-103">Chapter 6 - Azure RTOS FileX fault tolerant module</span></span>

<span data-ttu-id="54a15-104">Bu bölümde, medya güç kaybettiğinde veya dosya yazma işleminin ortasında çıkarıldığında dosya sistemi bütünlüğünü sürdürmek üzere tasarlanan Azure RTOS FileX hata toleranslı modülünün bir açıklaması bulunur.</span><span class="sxs-lookup"><span data-stu-id="54a15-104">This chapter contains a description of the Azure RTOS FileX Fault Tolerant Module that is designed to maintain file system integrity if the media loses power or is ejected in the middle of a file write operation.</span></span>

## <a name="filex-fault-tolerant-module-overview"></a><span data-ttu-id="54a15-105">FileX hataya dayanıklı modüle genel bakış</span><span class="sxs-lookup"><span data-stu-id="54a15-105">FileX Fault Tolerant Module Overview</span></span>

<span data-ttu-id="54a15-106">Bir uygulama bir dosyaya veri yazdığında, FileX veri kümelerini ve sistem bilgilerini güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="54a15-106">When an application writes data into a file, FileX updates both data clusters and system information.</span></span> <span data-ttu-id="54a15-107">Bu güncelleştirmelerin, dosya sistemindeki bilgilerin tutarlı tutulması için atomik bir işlem olarak tamamlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="54a15-107">These updates must be completed as an atomic operation to keep information in the file system coherent.</span></span> <span data-ttu-id="54a15-108">Örneğin, bir dosyaya veri eklerken, FileX 'in medyada kullanılabilir bir kümeyi bulması, FAT zincirini güncelleştirmesi, Dizin girişinde dosyalanan uzunluğu güncelleştirmesi ve Dizin girişinde başlangıç kümesi numarasını güncelleştirmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="54a15-108">For example, when appending data to a file, FileX needs to find an available cluster in the media, update the FAT chain, update the length filed in the directory entry, and possibly update the starting cluster number in the directory entry.</span></span> <span data-ttu-id="54a15-109">Güç kesintisi veya medya çıkarma, güncelleştirme dizisini kesintiye uğratabilir, bu da dosya sistemini tutarsız bir durumda bırakır.</span><span class="sxs-lookup"><span data-stu-id="54a15-109">Either a power failure or media ejection can interrupt the sequence of updates, which will leave the file system in an inconsistent state.</span></span> <span data-ttu-id="54a15-110">Tutarsız durum düzeltilmemişse, güncelleştirilmekte olan veriler kaybolabilir ve sistem bilgilerine zarar verebileceğinden, sonraki dosya sistemi işlemi ortamdaki diğer dosyalara veya dizinlere zarar verebilir.</span><span class="sxs-lookup"><span data-stu-id="54a15-110">If the inconsistent state is not corrected, the data being updated can be lost, and because of damage to the system information, subsequent file system operation may damage other files or directories on the media.</span></span>

<span data-ttu-id="54a15-111">FileX hata toleransı modülü, bu adımlar dosya sistemine uygulanmadan *önce* bir dosyayı güncelleştirmek için gereken günlüğe kaydetme adımları ile işe yarar.</span><span class="sxs-lookup"><span data-stu-id="54a15-111">The FileX Fault Tolerant Module works by journaling steps required to update a file *before* these steps are applied to the file system.</span></span> <span data-ttu-id="54a15-112">Dosya güncelleştirmesi başarılı olursa bu günlük girdileri kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="54a15-112">If the file update is successful, these log entries are removed.</span></span> <span data-ttu-id="54a15-113">Ancak, dosya güncelleştirmesi kesintiye uğrarsa günlük girdileri medyada depolanır.</span><span class="sxs-lookup"><span data-stu-id="54a15-113">However, if the file update is interrupted, the log entries are stored on the media.</span></span> <span data-ttu-id="54a15-114">Medyanın bir sonraki takılışında, FileX bu günlük girdilerini önceki (tamamlanmamış) yazma işleminden algılar.</span><span class="sxs-lookup"><span data-stu-id="54a15-114">Next time the media is mounted, FileX detects these log entries from the previous (unfinished) write operation.</span></span> <span data-ttu-id="54a15-115">Bu gibi durumlarda, FileX, dosya sistemine zaten yapılmış olan değişiklikleri geri alarak veya önceki işlemi tamamlamaya yönelik gerekli değişiklikleri yeniden uygulayarak bir hatadan kurtuya olabilir.</span><span class="sxs-lookup"><span data-stu-id="54a15-115">In such cases, FileX can recover from a failure by either rolling back the changes already made to the file system, or by reapplying the required changes to complete the previous operation.</span></span> <span data-ttu-id="54a15-116">Bu şekilde, bir güncelleştirme işlemi sırasında medya güç kesilirse, FileX hata toleransı modülü dosya sistemi bütünlüğünü korur.</span><span class="sxs-lookup"><span data-stu-id="54a15-116">In this way, the FileX Fault Tolerant Module maintains file system integrity if the media loses power during an update operation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="54a15-117">*FileX hata toleranslı modülü, fiziksel medya bozulmasından kaynaklanan geçerli verilerle oluşan dosya sistemi bozulmasını önleyecek şekilde tasarlanmamıştır.*</span><span class="sxs-lookup"><span data-stu-id="54a15-117">*The FileX Fault Tolerant Module is not designed to prevent file system corruption caused by physical media corruption with valid data in it.*</span></span>

> [!IMPORTANT]
> <span data-ttu-id="54a15-118">*FileX hataya dayanıklı modül bir medyayı koruduktan sonra, hata toleransı etkinleştirilmiş olarak dosya x dışında bir şeye bağlı olmamalıdır. Bunun yapılması, dosya sistemindeki günlük girişlerinin medyada sistem bilgileriyle tutarsız olmasına neden olabilir. Medya başka bir dosya sistemi tarafından güncelleştirildikten sonra FileX hata toleranslı modülü günlük girdilerini işlemeye çalışırsa, kurtarma yordamı başarısız olabilir ve tüm dosya sistemi öngörülemeyen bir durumda bırakılır.*</span><span class="sxs-lookup"><span data-stu-id="54a15-118">*After the FileX Fault Tolerant module protects a media, the media must not be mounted by anything other than FileX with Fault Tolerant enabled. Doing so can cause the log entries in the file system to be inconsistent with system information on the media. If the FileX Fault Tolerant module attempts to process log entries after the media is updated by another file system, the recovery procedure may fail, leaving the entire file system in an unpredictable state.*</span></span>

## <a name="use-of-the-fault-tolerant-module"></a><span data-ttu-id="54a15-119">Hataya dayanıklı modülün kullanımı</span><span class="sxs-lookup"><span data-stu-id="54a15-119">Use of the Fault Tolerant Module</span></span>

<span data-ttu-id="54a15-120">FileX hataya dayanıklı özelliği, FileX tarafından desteklenen FAT12, FAT16, FAT32 ve exFAT gibi tüm FAT dosya sistemleri tarafından kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="54a15-120">The FileX Fault Tolerant feature is available to all FAT file systems supported by FileX, including FAT12, FAT16, FAT32, and exFAT.</span></span> <span data-ttu-id="54a15-121">Hataya dayanıklı özelliği etkinleştirmek için, FileX, tanımlı **FX_ENABLE_FAULT_TOLERANT** sembol ile oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="54a15-121">To enable the fault tolerant feature, FileX must be built with the symbol **FX_ENABLE_FAULT_TOLERANT** defined.</span></span> <span data-ttu-id="54a15-122">Çalışma zamanında uygulama, ***_ fx_media_open çağrısından hemen sonra fx_fault_tolerant_enable _*** çağırarak hataya dayanıklı hizmet başlatır.</span><span class="sxs-lookup"><span data-stu-id="54a15-122">At run time, application starts fault tolerant service by calling **_fx_fault_tolerant_enable_*_ immediately after the call to _*_fx_media_open_**.</span></span> <span data-ttu-id="54a15-123">Hata toleransı etkinleştirildikten sonra, belirlenen medyaya tüm dosya yazma işlemleri korunur.</span><span class="sxs-lookup"><span data-stu-id="54a15-123">After fault tolerant is enabled, all file write operations to the designated media are protected.</span></span> <span data-ttu-id="54a15-124">Varsayılan olarak, hataya dayanıklı modül etkin değildir.</span><span class="sxs-lookup"><span data-stu-id="54a15-124">By default the fault tolerant module is not enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="54a15-125">\* Uygulamanın dosya sistemine \***fx_fault_tolerant_enable** _ çağrılmadan önce erişilmediğinden emin olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="54a15-125">\*Application needs to make sure the file system is not being accessed prior to \***fx_fault_tolerant_enable** _ being called.</span></span> <span data-ttu-id="54a15-126">Uygulama, hataya dayanıklı etkinleştirilmesinden önce dosya sistemine veri yazardıysa, önceki yazma işlemleri tamamlanmıyorsa ve dosya sistemi hataya dayanıklı günlük entries._ ile geri yüklenmediğinde yazma işlemi medyayı bozabilir.</span><span class="sxs-lookup"><span data-stu-id="54a15-126">If application writes data to the file system prior to fault tolerant enable, the write operation could corrupt the media if prior write operations were not completed, and the file system was not restored using fault tolerant log entries._</span></span>

## <a name="filex-fault-tolerant-module-log"></a><span data-ttu-id="54a15-127">FileX hataya dayanıklı modül günlüğü</span><span class="sxs-lookup"><span data-stu-id="54a15-127">FileX Fault Tolerant Module Log</span></span>

<span data-ttu-id="54a15-128">FileX hata toleransı günlüğü, Flash 'ta bir mantıksal küme kullanır.</span><span class="sxs-lookup"><span data-stu-id="54a15-128">The FileX fault tolerant log takes up one logical cluster in flash.</span></span> <span data-ttu-id="54a15-129">Bu kümenin başlangıç kümesi numarasına olan dizin, **FX_FAULT_TOLERANT_BOOT_INDEX** sembol tarafından belirtilen bir uzaklığa sahip medyanın önyükleme kesimine kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="54a15-129">The index to the starting cluster number of that cluster is recorded in the boot sector of the media, with an offset specified by the symbol **FX_FAULT_TOLERANT_BOOT_INDEX**.</span></span> <span data-ttu-id="54a15-130">Varsayılan olarak, bu sembol 116 olarak tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="54a15-130">By default this symbol is defined to be 116.</span></span> <span data-ttu-id="54a15-131">Bu konum, FAT12/16/32 ve exFAT belirtiminde ayrılmış olarak işaretlendiğinden seçilir.</span><span class="sxs-lookup"><span data-stu-id="54a15-131">This location is chosen because it is marked as reserved in FAT12/ 16/32 and exFAT specification.</span></span>

<span data-ttu-id="54a15-132">Şekil 5, "günlük yapısı düzeni", günlük yapısının genel yerleşimini gösterir.</span><span class="sxs-lookup"><span data-stu-id="54a15-132">Figure 5, "Log Structure Layout," shows the general layout of the log structure.</span></span> <span data-ttu-id="54a15-133">Günlük yapısı üç bölüm içerir: günlük üstbilgisi, FAT zinciri ve günlük girişleri.</span><span class="sxs-lookup"><span data-stu-id="54a15-133">The log structure contains three sections: Log Header, FAT Chain, and Log Entries.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="54a15-134">*Günlük girişlerinde depolanan tüm çok baytlı değerler little endian biçimindedir.*</span><span class="sxs-lookup"><span data-stu-id="54a15-134">*All multi-byte values stored in the log entries are in Little Endian format.*</span></span>

![Günlük yapısı düzeni](./media/user-guide/log-structure-layout.png)

<span data-ttu-id="54a15-136">**Şekil 5. Günlük yapısı düzeni**</span><span class="sxs-lookup"><span data-stu-id="54a15-136">**Figure 5. Log Structure Layout**</span></span>

<span data-ttu-id="54a15-137">Günlük üstbilgisi alanı, tüm günlük yapısını açıklayan bilgileri içerir ve her bir alanı ayrıntılı olarak açıklar.</span><span class="sxs-lookup"><span data-stu-id="54a15-137">The Log Header area contains information that describes the entire log structure and explains each field in detail.</span></span>

<span data-ttu-id="54a15-138">**TABLO 8. Günlük üst bilgi alanı**</span><span class="sxs-lookup"><span data-stu-id="54a15-138">**TABLE 8. Log Header Area**</span></span>

|<span data-ttu-id="54a15-139">Alan</span><span class="sxs-lookup"><span data-stu-id="54a15-139">Field</span></span>|<span data-ttu-id="54a15-140">Boyut (bayt)</span><span class="sxs-lookup"><span data-stu-id="54a15-140">Size(in bytes)</span></span>|<span data-ttu-id="54a15-141">Description</span><span class="sxs-lookup"><span data-stu-id="54a15-141">Description</span></span>|
|-----|--------------|-----------|
|<span data-ttu-id="54a15-142">ID</span><span class="sxs-lookup"><span data-stu-id="54a15-142">ID</span></span>|<span data-ttu-id="54a15-143">4</span><span class="sxs-lookup"><span data-stu-id="54a15-143">4</span></span>|<span data-ttu-id="54a15-144">Bir FileX hata toleransı günlük yapısını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="54a15-144">Identifies a FileX Fault Tolerant Log structure.</span></span> <span data-ttu-id="54a15-145">KIMLIK değeri 0x46544C52 değilse, günlük yapısı geçersiz olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="54a15-145">The log structure is considered invalid if the ID value is not 0x46544C52.</span></span>|
|<span data-ttu-id="54a15-146">Toplam Boyut</span><span class="sxs-lookup"><span data-stu-id="54a15-146">Total Size</span></span>|<span data-ttu-id="54a15-147">2</span><span class="sxs-lookup"><span data-stu-id="54a15-147">2</span></span>|<span data-ttu-id="54a15-148">Tüm günlük yapısının toplam boyutunu (bayt olarak) belirtir.</span><span class="sxs-lookup"><span data-stu-id="54a15-148">Indicates the total size (in bytes) of the entire log structure.</span></span>|
|<span data-ttu-id="54a15-149">Üst bilgi sağlama toplamı</span><span class="sxs-lookup"><span data-stu-id="54a15-149">Header Checksum</span></span>|<span data-ttu-id="54a15-150">2</span><span class="sxs-lookup"><span data-stu-id="54a15-150">2</span></span>|<span data-ttu-id="54a15-151">Günlük üst bilgi alanını dönüştüren sağlama toplamı.</span><span class="sxs-lookup"><span data-stu-id="54a15-151">Checksum that converts the log header area.</span></span> <span data-ttu-id="54a15-152">Üstbilgi alanları sağlama toplamı doğrulamasında başarısız olursa günlük yapısı geçersiz olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="54a15-152">The log structure is considered invalid if the header fields fail the checksum verification.</span></span>|
|<span data-ttu-id="54a15-153">Sürüm Numarası</span><span class="sxs-lookup"><span data-stu-id="54a15-153">Version Number</span></span>|<span data-ttu-id="54a15-154">2</span><span class="sxs-lookup"><span data-stu-id="54a15-154">2</span></span>|<span data-ttu-id="54a15-155">FileX hataya dayanıklı büyük ve küçük sürüm numaraları.</span><span class="sxs-lookup"><span data-stu-id="54a15-155">FileX Fault Tolerant major and minor version numbers.</span></span>|
|<span data-ttu-id="54a15-156">Ayrılmıştır</span><span class="sxs-lookup"><span data-stu-id="54a15-156">Reserved</span></span>|<span data-ttu-id="54a15-157">2</span><span class="sxs-lookup"><span data-stu-id="54a15-157">2</span></span>|<span data-ttu-id="54a15-158">Daha sonra genişletme için.</span><span class="sxs-lookup"><span data-stu-id="54a15-158">For future expansion.</span></span>|

<span data-ttu-id="54a15-159">Günlük üst bilgi alanının ardından FAT zinciri günlük alanı bulunur.</span><span class="sxs-lookup"><span data-stu-id="54a15-159">The Log Header area is followed by the FAT Chain Log area.</span></span> <span data-ttu-id="54a15-160">Şekil 9 ' da, FAT zincirinin nasıl değiştirilmesi gerektiğini açıklayan bilgiler yer alır.</span><span class="sxs-lookup"><span data-stu-id="54a15-160">Figure 9 contains information that describes how the FAT chain should be modified.</span></span> <span data-ttu-id="54a15-161">Bu günlük alanı, bir dosyaya ayrılan kümelerle ilgili bilgiler, bir dosyadan çıkarılan kümeler ve ekleme/silmenin nerede olması gerektiğini ve FAT zinciri günlük alanındaki her alanı açıklar.</span><span class="sxs-lookup"><span data-stu-id="54a15-161">This log area contains information on the clusters being allocated to a file, the clusters being removed from a file, and where the insertion/deletion should be and describes each field in the FAT Chain Log area.</span></span>

<span data-ttu-id="54a15-162">**TABLO 9. FAT zinciri günlük alanı**</span><span class="sxs-lookup"><span data-stu-id="54a15-162">**TABLE 9. FAT Chain Log Area**</span></span>

|<span data-ttu-id="54a15-163">Alan</span><span class="sxs-lookup"><span data-stu-id="54a15-163">Field</span></span>|<span data-ttu-id="54a15-164">Boyut (bayt)</span><span class="sxs-lookup"><span data-stu-id="54a15-164">Size(in bytes)</span></span>|<span data-ttu-id="54a15-165">Açıklama</span><span class="sxs-lookup"><span data-stu-id="54a15-165">Description</span></span>|
|-----|--------------|-----------|
|<span data-ttu-id="54a15-166">FAT zinciri günlüğü sağlama toplamı</span><span class="sxs-lookup"><span data-stu-id="54a15-166">FAT Chain Log Checksum</span></span>|<span data-ttu-id="54a15-167">2</span><span class="sxs-lookup"><span data-stu-id="54a15-167">2</span></span>|<span data-ttu-id="54a15-168">Tüm FAT zinciri günlük alanının sağlama toplamı.</span><span class="sxs-lookup"><span data-stu-id="54a15-168">Checksum of the entire FAT Chain Log area.</span></span> <span data-ttu-id="54a15-169">Sağlama toplamı doğrulamasında başarısız olursa FAT zinciri günlük alanı geçersiz olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="54a15-169">The FAT Chain Log area is considered invalid if the it fails the checksum verification.</span></span>|
|<span data-ttu-id="54a15-170">Bayrak</span><span class="sxs-lookup"><span data-stu-id="54a15-170">Flag</span></span>|<span data-ttu-id="54a15-171">1</span><span class="sxs-lookup"><span data-stu-id="54a15-171">1</span></span>|<span data-ttu-id="54a15-172">Geçerli bayrak değerleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="54a15-172">Valid flag values are:</span></span><br/><span data-ttu-id="54a15-173">0x01 FAT zinciri geçerli</span><span class="sxs-lookup"><span data-stu-id="54a15-173">0x01 FAT Chain Valid</span></span><br /><span data-ttu-id="54a15-174">0x02 BIT EŞLEMI kullanılıyor</span><span class="sxs-lookup"><span data-stu-id="54a15-174">0x02 BITMAP is being used</span></span>|
|<span data-ttu-id="54a15-175">Ayrılmıştır</span><span class="sxs-lookup"><span data-stu-id="54a15-175">Reserved</span></span>|<span data-ttu-id="54a15-176">1</span><span class="sxs-lookup"><span data-stu-id="54a15-176">1</span></span>|<span data-ttu-id="54a15-177">Gelecekte kullanılmak üzere ayrılmış</span><span class="sxs-lookup"><span data-stu-id="54a15-177">Reserved for future use</span></span>|
|<span data-ttu-id="54a15-178">Ekleme noktası – ön</span><span class="sxs-lookup"><span data-stu-id="54a15-178">Insertion Point – Front</span></span>|<span data-ttu-id="54a15-179">4</span><span class="sxs-lookup"><span data-stu-id="54a15-179">4</span></span>|<span data-ttu-id="54a15-180">Yeni oluşturulan zincirin eklendiği küme (orijinal FAT zincirine ait).</span><span class="sxs-lookup"><span data-stu-id="54a15-180">The cluster (that belongs to the original FAT chain) where the newly created chain is going to be attached to.</span></span>|
|<span data-ttu-id="54a15-181">Yeni FAT zincirinin baş kümesi</span><span class="sxs-lookup"><span data-stu-id="54a15-181">Head Cluster of New FAT Chain</span></span>|<span data-ttu-id="54a15-182">4</span><span class="sxs-lookup"><span data-stu-id="54a15-182">4</span></span>|<span data-ttu-id="54a15-183">Yeni oluşturulan FAT zincirinin ilk kümesi</span><span class="sxs-lookup"><span data-stu-id="54a15-183">The first cluster of the newly created FAT Chain</span></span>|
|<span data-ttu-id="54a15-184">Özgün FAT zincirinin baş kümesi</span><span class="sxs-lookup"><span data-stu-id="54a15-184">Head Cluster of Original FAT Chain</span></span>|<span data-ttu-id="54a15-185">4</span><span class="sxs-lookup"><span data-stu-id="54a15-185">4</span></span>|<span data-ttu-id="54a15-186">Kaldırılacak özgün FAT zincirinin bölümünün ilk kümesi.</span><span class="sxs-lookup"><span data-stu-id="54a15-186">The first cluster of the portion of the original FAT Chain that is to be removed.</span></span>|
|<span data-ttu-id="54a15-187">Ekleme noktası – geri</span><span class="sxs-lookup"><span data-stu-id="54a15-187">Insertion Point – Back</span></span>|<span data-ttu-id="54a15-188">4</span><span class="sxs-lookup"><span data-stu-id="54a15-188">4</span></span>|<span data-ttu-id="54a15-189">Yeni oluşturulan FAT zincirinin üzerinde birleşen özgün küme.</span><span class="sxs-lookup"><span data-stu-id="54a15-189">The original cluster where the newly created FAT chain joins at.</span></span>|
|<span data-ttu-id="54a15-190">Sonraki silme noktası</span><span class="sxs-lookup"><span data-stu-id="54a15-190">Next Deletion Point</span></span>|<span data-ttu-id="54a15-191">4</span><span class="sxs-lookup"><span data-stu-id="54a15-191">4</span></span>|<span data-ttu-id="54a15-192">Bu alan, FAT zinciri Temizleme yordamına yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="54a15-192">This field assists the FAT chain cleanup procedure.</span></span>|

<span data-ttu-id="54a15-193">Günlük girişleri alanı, bir hatadan kurtarmak için gereken değişiklikleri tanımlayan günlük girdilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="54a15-193">The Log Entries Area contains log entries that describe the changes needed to recover from a failure.</span></span> <span data-ttu-id="54a15-194">FileX hata toleranslı modülünde desteklenen üç günlük girişi türü vardır: FAT günlük girdisi; Dizin günlüğü girişi; ve bit eşlem günlüğü girişi.</span><span class="sxs-lookup"><span data-stu-id="54a15-194">There are three types of log entry supported in the FileX fault tolerant module: FAT Log Entry; Directory Log Entry; and Bitmap Log Entry.</span></span>

<span data-ttu-id="54a15-195">Aşağıdaki üç şekil ve üç tablo bu günlük girdilerini ayrıntılı olarak anlatmaktadır.</span><span class="sxs-lookup"><span data-stu-id="54a15-195">The following three figures and three tables describe these log entries in detail.</span></span>

![FAT günlük girdisi](./media/user-guide/fat-log-entry.png)

<span data-ttu-id="54a15-197">**Şekil 6. FAT günlük girdisi**</span><span class="sxs-lookup"><span data-stu-id="54a15-197">**Figure 6. FAT Log Entry**</span></span>

<span data-ttu-id="54a15-198">**TABLO 10. FAT günlük girdisi**</span><span class="sxs-lookup"><span data-stu-id="54a15-198">**TABLE 10. FAT Log Entry**</span></span>

|<span data-ttu-id="54a15-199">Alan</span><span class="sxs-lookup"><span data-stu-id="54a15-199">Field</span></span>|<span data-ttu-id="54a15-200">Boyut (bayt)</span><span class="sxs-lookup"><span data-stu-id="54a15-200">Size(in bytes)</span></span>|<span data-ttu-id="54a15-201">Açıklama</span><span class="sxs-lookup"><span data-stu-id="54a15-201">Description</span></span>|
|-----|--------------|-----------|
<span data-ttu-id="54a15-202">Tür</span><span class="sxs-lookup"><span data-stu-id="54a15-202">Type</span></span>|<span data-ttu-id="54a15-203">2</span><span class="sxs-lookup"><span data-stu-id="54a15-203">2</span></span>|<span data-ttu-id="54a15-204">Giriş türü, FX_FAULT_TOLERANT_FAT_LOG_TYPE olmalıdır</span><span class="sxs-lookup"><span data-stu-id="54a15-204">Type of Entry, must be FX_FAULT_TOLERANT_FAT_LOG_TYPE</span></span>|
|<span data-ttu-id="54a15-205">Boyut</span><span class="sxs-lookup"><span data-stu-id="54a15-205">Size</span></span>|<span data-ttu-id="54a15-206">2</span><span class="sxs-lookup"><span data-stu-id="54a15-206">2</span></span>|<span data-ttu-id="54a15-207">Bu girdinin boyutu</span><span class="sxs-lookup"><span data-stu-id="54a15-207">Size of this entry</span></span>|
|<span data-ttu-id="54a15-208">Küme numarası</span><span class="sxs-lookup"><span data-stu-id="54a15-208">Cluster Number</span></span>|<span data-ttu-id="54a15-209">4</span><span class="sxs-lookup"><span data-stu-id="54a15-209">4</span></span>|<span data-ttu-id="54a15-210">Küme numarası</span><span class="sxs-lookup"><span data-stu-id="54a15-210">Cluster number</span></span>|
|<span data-ttu-id="54a15-211">Değer</span><span class="sxs-lookup"><span data-stu-id="54a15-211">Value</span></span>|<span data-ttu-id="54a15-212">4</span><span class="sxs-lookup"><span data-stu-id="54a15-212">4</span></span>|<span data-ttu-id="54a15-213">FAT girişine yazılacak değer</span><span class="sxs-lookup"><span data-stu-id="54a15-213">Value to be written into the FAT entry</span></span>|

![Dizin günlüğü girdisi](./media/user-guide/directory-log-entry.png)

<span data-ttu-id="54a15-215">**Şekil 7. Dizin günlüğü girdisi**</span><span class="sxs-lookup"><span data-stu-id="54a15-215">**Figure 7. Directory Log Entry**</span></span>

<span data-ttu-id="54a15-216">**TABLO 11. Dizin günlüğü girdisi**</span><span class="sxs-lookup"><span data-stu-id="54a15-216">**TABLE 11. Directory Log Entry**</span></span>

|<span data-ttu-id="54a15-217">Alan</span><span class="sxs-lookup"><span data-stu-id="54a15-217">Field</span></span>|<span data-ttu-id="54a15-218">Boyut (bayt)</span><span class="sxs-lookup"><span data-stu-id="54a15-218">Size(in bytes)</span></span>|<span data-ttu-id="54a15-219">Açıklama</span><span class="sxs-lookup"><span data-stu-id="54a15-219">Description</span></span>|
|-----|--------------|-----------|
|<span data-ttu-id="54a15-220">Tür</span><span class="sxs-lookup"><span data-stu-id="54a15-220">Type</span></span>|<span data-ttu-id="54a15-221">2</span><span class="sxs-lookup"><span data-stu-id="54a15-221">2</span></span>|<span data-ttu-id="54a15-222">Giriş türü, FX_FAULT_TOLERANT_DIRECTORY_LOG_TYPE olmalıdır</span><span class="sxs-lookup"><span data-stu-id="54a15-222">Type of Entry, must be FX_FAULT_TOLERANT_DIRECTORY_LOG_TYPE</span></span>|
|<span data-ttu-id="54a15-223">Boyut</span><span class="sxs-lookup"><span data-stu-id="54a15-223">Size</span></span>|<span data-ttu-id="54a15-224">2</span><span class="sxs-lookup"><span data-stu-id="54a15-224">2</span></span>|<span data-ttu-id="54a15-225">Bu girdinin boyutu</span><span class="sxs-lookup"><span data-stu-id="54a15-225">Size of this entry</span></span>|
|<span data-ttu-id="54a15-226">Kesim boşluğu</span><span class="sxs-lookup"><span data-stu-id="54a15-226">Sector Offset</span></span>|<span data-ttu-id="54a15-227">4</span><span class="sxs-lookup"><span data-stu-id="54a15-227">4</span></span>|<span data-ttu-id="54a15-228">Bu dizinin bulunduğu kesime (bayt cinsinden).</span><span class="sxs-lookup"><span data-stu-id="54a15-228">Offset (in bytes) into the sector where this directory is located.</span></span>|
|<span data-ttu-id="54a15-229">Günlük kesimi</span><span class="sxs-lookup"><span data-stu-id="54a15-229">Log Sector</span></span>|<span data-ttu-id="54a15-230">4</span><span class="sxs-lookup"><span data-stu-id="54a15-230">4</span></span>|<span data-ttu-id="54a15-231">Dizin girişinin bulunduğu sektör</span><span class="sxs-lookup"><span data-stu-id="54a15-231">The sector where the directory entry is located</span></span>|
|<span data-ttu-id="54a15-232">Günlük Verileri</span><span class="sxs-lookup"><span data-stu-id="54a15-232">Log Data</span></span>|<span data-ttu-id="54a15-233">Değişken</span><span class="sxs-lookup"><span data-stu-id="54a15-233">Variable</span></span>|<span data-ttu-id="54a15-234">Dizin girişinin içeriği</span><span class="sxs-lookup"><span data-stu-id="54a15-234">Content of the directory entry</span></span>|

![Bit eşlem günlüğü girdisi](./media/user-guide/bitmap-log-entry.png)

<span data-ttu-id="54a15-236">**Şekil 8. Bit eşlem günlüğü girdisi**</span><span class="sxs-lookup"><span data-stu-id="54a15-236">**Figure 8. Bitmap Log Entry**</span></span>

<span data-ttu-id="54a15-237">**TABLO 12. Bit eşlem günlüğü girdisi**</span><span class="sxs-lookup"><span data-stu-id="54a15-237">**TABLE 12. Bitmap Log Entry**</span></span>

|<span data-ttu-id="54a15-238">Alan</span><span class="sxs-lookup"><span data-stu-id="54a15-238">Field</span></span>|<span data-ttu-id="54a15-239">Boyut (bayt)</span><span class="sxs-lookup"><span data-stu-id="54a15-239">Size(in bytes)</span></span>|<span data-ttu-id="54a15-240">Açıklama</span><span class="sxs-lookup"><span data-stu-id="54a15-240">Description</span></span>|
|-----|--------------|-----------|
|<span data-ttu-id="54a15-241">Tür</span><span class="sxs-lookup"><span data-stu-id="54a15-241">Type</span></span>|<span data-ttu-id="54a15-242">2</span><span class="sxs-lookup"><span data-stu-id="54a15-242">2</span></span>|<span data-ttu-id="54a15-243">Giriş türü, FX_FAULT_TOLERANT_BITMAP_LOG_TYPE olmalıdır</span><span class="sxs-lookup"><span data-stu-id="54a15-243">Type of Entry, must be FX_FAULT_TOLERANT_BITMAP_LOG_TYPE</span></span>|
|<span data-ttu-id="54a15-244">Boyut</span><span class="sxs-lookup"><span data-stu-id="54a15-244">Size</span></span>|<span data-ttu-id="54a15-245">2</span><span class="sxs-lookup"><span data-stu-id="54a15-245">2</span></span>|<span data-ttu-id="54a15-246">Bu girdinin boyutu</span><span class="sxs-lookup"><span data-stu-id="54a15-246">Size of this entry</span></span>|
|<span data-ttu-id="54a15-247">Küme numarası</span><span class="sxs-lookup"><span data-stu-id="54a15-247">Cluster Number</span></span>|<span data-ttu-id="54a15-248">4</span><span class="sxs-lookup"><span data-stu-id="54a15-248">4</span></span>|<span data-ttu-id="54a15-249">Küme numarası</span><span class="sxs-lookup"><span data-stu-id="54a15-249">Cluster number</span></span>|
|<span data-ttu-id="54a15-250">Değer</span><span class="sxs-lookup"><span data-stu-id="54a15-250">Value</span></span>|<span data-ttu-id="54a15-251">4</span><span class="sxs-lookup"><span data-stu-id="54a15-251">4</span></span>|<span data-ttu-id="54a15-252">FAT girişine yazılacak değer</span><span class="sxs-lookup"><span data-stu-id="54a15-252">Value to be written into the FAT entry</span></span>|

## <a name="fault-tolerant-protection"></a><span data-ttu-id="54a15-253">Hataya dayanıklı koruma</span><span class="sxs-lookup"><span data-stu-id="54a15-253">Fault Tolerant Protection</span></span>

<span data-ttu-id="54a15-254">FileX hata toleranslı modülü başladıktan sonra, öncelikle medyada mevcut bir hataya dayanıklı günlük dosyası arar.</span><span class="sxs-lookup"><span data-stu-id="54a15-254">After the FileX Fault Tolerant Module starts, it first searches for an existing fault tolerant log file in the media.</span></span> <span data-ttu-id="54a15-255">Geçerli bir günlük dosyası bulunamazsa, FileX medyayı korumasız olarak değerlendirir.</span><span class="sxs-lookup"><span data-stu-id="54a15-255">If a valid log file cannot be found, FileX considers the media unprotected.</span></span> <span data-ttu-id="54a15-256">Bu durumda, FileX medyada bir hata toleranslı günlük dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="54a15-256">In this case FileX will create a fault tolerant log file on the media.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="54a15-257">\* FileX, dosya sistemini, FileX hata toleranslı modülü başlamadan önce bozuksa koruyamaz.</span><span class="sxs-lookup"><span data-stu-id="54a15-257">\*FileX is not able to protect a file system if it was corrupted before the FileX Fault Tolerant Module starts.</span></span> *

<span data-ttu-id="54a15-258">Bir hata toleranslı günlük dosyası bulunuyorsa, FileX mevcut günlük girişlerini denetler.</span><span class="sxs-lookup"><span data-stu-id="54a15-258">If a fault tolerant log file is located, FileX checks for existing log entries.</span></span> <span data-ttu-id="54a15-259">Günlük girişi olmayan bir günlük dosyası, önceki dosya işleminin başarılı olduğunu ve tüm günlük girişlerinin kaldırıldığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="54a15-259">A log file with no log entry indicates prior file operation was successful, and all log entries were removed.</span></span> <span data-ttu-id="54a15-260">Bu durumda, uygulama hataya dayanıklı koruma ile dosya sistemini kullanmaya başlayabilir.</span><span class="sxs-lookup"><span data-stu-id="54a15-260">In this case the application can start using the file system with fault tolerant protection.</span></span>

<span data-ttu-id="54a15-261">Ancak günlük girişleri konumlandırıldığında, FileX 'in önceki dosya işlemini tamamlaması veya dosya sistemine zaten uygulanmış olan değişiklikleri geri döndürmesinden önce, değişiklikleri etkin bir şekilde geri alın.</span><span class="sxs-lookup"><span data-stu-id="54a15-261">However if log entries are located, FileX needs to either complete the prior file operation, or revert the changes already applied to the file system, effectively undo the changes.</span></span> <span data-ttu-id="54a15-262">Her iki durumda da, günlük girdileri dosya sistemine uygulandıktan sonra, dosya sistemi tutarlı bir duruma geri yüklenir ve uygulama dosya sistemini yeniden kullanmaya başlayabilir.</span><span class="sxs-lookup"><span data-stu-id="54a15-262">In either case, after the log entries are applied to the file system, the file system is restored into a coherent state, and application can start using the file system again.</span></span>

<span data-ttu-id="54a15-263">Dosya güncelleştirme işlemi sırasında FileX tarafından korunan medya için veri bölümü doğrudan medyaya yazılır.</span><span class="sxs-lookup"><span data-stu-id="54a15-263">For media protected by FileX, during file update operation, the data portion is written directly to the media.</span></span> <span data-ttu-id="54a15-264">FileX, verileri yazdığında, Dizin girişlerine, FAT tablosuna uygulanması gereken tüm değişiklikleri de kaydeder.</span><span class="sxs-lookup"><span data-stu-id="54a15-264">As FileX writes data, it also records any changes needed to be applied to directory entries, FAT table.</span></span> <span data-ttu-id="54a15-265">Bu bilgiler, dosya dayanıklı günlük girişlerine kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="54a15-265">This information is recorded in the file tolerant log entries.</span></span> <span data-ttu-id="54a15-266">Bu yaklaşım, veriler medyaya yazıldıktan sonra dosya sistemi güncelleştirmelerinin gerçekleşmesini güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="54a15-266">This approach guarantees that updates to the file system occur after the data is written to the media.</span></span> <span data-ttu-id="54a15-267">Veri yazma aşamasında medya çıkartılamamışsa, önemli dosya sistemi bilgileri henüz değiştirilmez.</span><span class="sxs-lookup"><span data-stu-id="54a15-267">If the media is ejected during the data-write phase, crucial file system information has not been changed yet.</span></span> <span data-ttu-id="54a15-268">Bu nedenle, dosya sistemi kesintiye karşı etkilenmez.</span><span class="sxs-lookup"><span data-stu-id="54a15-268">Therefore the file system is not affected by the interruption.</span></span>

<span data-ttu-id="54a15-269">Tüm veriler medyaya başarıyla yazıldıktan sonra, FileX, değişiklikleri sistem bilgilerinde, tek seferde bir giriş olacak şekilde uygulamak için günlük girdilerindeki bilgileri izler.</span><span class="sxs-lookup"><span data-stu-id="54a15-269">After all the data is successfully written to the media, FileX then follows information in the log entries to applies the changes to system information, one entry at a time.</span></span> <span data-ttu-id="54a15-270">Tüm sistem bilgileri medyaya kaydedildikten sonra, günlük girişleri hataya dayanıklı günlüğünden kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="54a15-270">After all the system information is committed to the media, the log entries are removed from the fault tolerant log.</span></span> <span data-ttu-id="54a15-271">Bu noktada, FileX dosya güncelleştirme işlemini tamamlar.</span><span class="sxs-lookup"><span data-stu-id="54a15-271">At this point, FileX completes the file update operation.</span></span>

<span data-ttu-id="54a15-272">Dosya güncelleştirme işlemi sırasında dosyalar yerinde güncellenmez.</span><span class="sxs-lookup"><span data-stu-id="54a15-272">During file update operation, files are not updated in place.</span></span> <span data-ttu-id="54a15-273">Hataya dayanıklı modül, verilerin yeni verileri içine yazması için bir sektör ayırır ve sonra üzerine yazılacak verilerin bulunduğu kesimi kaldırır ve yeni kesimi chça bağlamak üzere ilgili FAT girişlerini günceller.</span><span class="sxs-lookup"><span data-stu-id="54a15-273">The fault tolerant module allocates a sector for the data to write the new data into, and then remove the sector that contains the data to be overwritten, updating related FAT entries to link the new sector into the chian.</span></span> <span data-ttu-id="54a15-274">Bir kümedeki kısmi verilerin değiştirilmesi gereken durumlarda, FileX her zaman yeni kümeler ayırır, güncelleştirilmiş verilerle eski kümelerden tüm verileri yeni kümelere yazar ve ardından eski kümeleri boşaltır.</span><span class="sxs-lookup"><span data-stu-id="54a15-274">For situations in which partial data in a cluster needs to be modified, FileX always allocates new clusters, writes the entire data from the old clusters with updated data into the new clusters, then frees up the old clusters.</span></span> <span data-ttu-id="54a15-275">Bu, dosya güncelleştirmesi kesintiye uğrarsa özgün dosyanın bozulmadan emin olur.</span><span class="sxs-lookup"><span data-stu-id="54a15-275">This guarantees that if the file update is interrupted, the original file is intact.</span></span> <span data-ttu-id="54a15-276">Uygulamanın, FileX hataya dayanıklı koruma altında, bir dosyadaki verilerin güncelleştirilmesi için medyanın, eski verileri olan kesimlerin yayımlanmasından önce yeni verileri tutacak yeterli boş alana sahip olması gerektiğini bilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="54a15-276">The application needs to be aware that under FileX fault tolerant protection, updating data in a file requires the media to have enough free space to hold new data before sectors with old data can be released.</span></span> <span data-ttu-id="54a15-277">Medyada yeni verileri tutmak için yeterli alan yoksa güncelleştirme işlemi başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="54a15-277">If the media doesn't have enough space to hold new data, the update operation fails.</span></span>