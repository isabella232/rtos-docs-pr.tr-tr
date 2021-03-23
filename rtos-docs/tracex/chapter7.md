---
title: Bölüm 7-Azure RTOS FileX izleme olayları
description: Bu bölümde, Azure RTOS FileX olaylarının açıklaması yer almaktadır.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: c3cbc945e33b87b6759c56ec1429d6bf57259bd9
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104827491"
---
# <a name="chapter-7---azure-rtos-filex-trace-events"></a><span data-ttu-id="0d3a2-103">Bölüm 7-Azure RTOS FileX izleme olayları</span><span class="sxs-lookup"><span data-stu-id="0d3a2-103">Chapter 7 - Azure RTOS FileX trace events</span></span>

<span data-ttu-id="0d3a2-104">Bu bölümde, Azure RTOS FileX olaylarının açıklaması yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-104">This chapter contains a description of the Azure RTOS FileX events.</span></span> 

## <a name="list-of-events-and-icons"></a><span data-ttu-id="0d3a2-105">Olay ve simgelerin listesi</span><span class="sxs-lookup"><span data-stu-id="0d3a2-105">List of Events and Icons</span></span>

<span data-ttu-id="0d3a2-106">**Aşağıda, TraceX tarafından görünen FileX olaylarının bir listesi verilmiştir.**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-106">**The following is a list of FileX events displayed by TraceX.**</span></span>

<span data-ttu-id="0d3a2-107">Aşağıda her bir olay açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="0d3a2-107">The following describes each event:</span></span>

| <span data-ttu-id="0d3a2-108">**Simge**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-108">**Icon**</span></span>                         | <span data-ttu-id="0d3a2-109">**Anlamı**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-109">**Meaning**</span></span>                               |
| -------------------------------- | ----------------------------------------- |
| ![İç mantıksal kesim önbelleğinde Isabetsizlik simgesi](./media/user-guide/fx-events/image1.png)    | <span data-ttu-id="0d3a2-111">İç mantıksal kesim önbelleği Isabetsizlik</span><span class="sxs-lookup"><span data-stu-id="0d3a2-111">Internal Logical Sector Cache Miss</span></span> |
| ![İç dizin önbelleği Isabetsizlik simgesi](./media/user-guide/fx-events/image2.png)    | <span data-ttu-id="0d3a2-113">İç dizin önbelleğinde Isabetsizlik</span><span class="sxs-lookup"><span data-stu-id="0d3a2-113">Internal Directory Cache Miss</span></span> |
| ![İç medya Temizleme simgesi](./media/user-guide/fx-events/image3.png)    | <span data-ttu-id="0d3a2-115">İç medya Temizleme</span><span class="sxs-lookup"><span data-stu-id="0d3a2-115">Internal Media Flush</span></span> |
| ![İç dizin girişi okuma simgesi](./media/user-guide/fx-events/image4.png)    | <span data-ttu-id="0d3a2-117">İç dizin girişi okundu</span><span class="sxs-lookup"><span data-stu-id="0d3a2-117">Internal Directory Entry Read</span></span> |
| ![İç dizin girişi yazma simgesi](./media/user-guide/fx-events/image5.png)    | <span data-ttu-id="0d3a2-119">İç dizin girişi yazma</span><span class="sxs-lookup"><span data-stu-id="0d3a2-119">Internal Directory Entry Write</span></span> |
| ![İç g/ç sürücüsü okuma simgesi](./media/user-guide/fx-events/image6.png)    | <span data-ttu-id="0d3a2-121">İç g/ç sürücüsü okuma</span><span class="sxs-lookup"><span data-stu-id="0d3a2-121">Internal I/O Driver Read</span></span> |
| ![İç g/ç sürücüsü yazma simgesi](./media/user-guide/fx-events/image7.png)    | <span data-ttu-id="0d3a2-123">İç g/ç sürücüsü yazma</span><span class="sxs-lookup"><span data-stu-id="0d3a2-123">Internal I/O Driver Write</span></span> |
| ![İç g/ç sürücüsü Temizleme simgesi](./media/user-guide/fx-events/image8.png)    | <span data-ttu-id="0d3a2-125">İç g/ç sürücüsü Temizleme</span><span class="sxs-lookup"><span data-stu-id="0d3a2-125">Internal I/O Driver Flush</span></span> |
| ![İç g/ç sürücüsü Iptali simgesi](./media/user-guide/fx-events/image9.png)    | <span data-ttu-id="0d3a2-127">İç g/ç sürücüsü Iptali</span><span class="sxs-lookup"><span data-stu-id="0d3a2-127">Internal I/O Driver Abort</span></span> |
| ![İç g/ç sürücüsü başlatma simgesi](./media/user-guide/fx-events/image10.png)    | <span data-ttu-id="0d3a2-129">İç g/ç sürücüsü başlatma</span><span class="sxs-lookup"><span data-stu-id="0d3a2-129">Internal I/O Driver Initialize</span></span> |
| ![İç g/ç sürücüsü önyüklemesi okuma simgesi](./media/user-guide/fx-events/image11.png)    | <span data-ttu-id="0d3a2-131">İç g/ç sürücüsü önyüklemesi okuma</span><span class="sxs-lookup"><span data-stu-id="0d3a2-131">Internal I/O Driver Boot Read</span></span> |
| ![İç g/ç sürücüsü sürüm kesimleri simgesi](./media/user-guide/fx-events/image12.png)    | <span data-ttu-id="0d3a2-133">İç g/ç sürücüsü sürüm kesimleri</span><span class="sxs-lookup"><span data-stu-id="0d3a2-133">Internal I/O Driver Release Sectors</span></span> |
| ![İç g/ç sürücüsü önyükleme yazma simgesi](./media/user-guide/fx-events/image13.png)    | <span data-ttu-id="0d3a2-135">İç g/ç sürücüsü önyükleme yazma</span><span class="sxs-lookup"><span data-stu-id="0d3a2-135">Internal I/O Driver Boot Write</span></span> |
| ![İç g/ç sürücü sürücüsü başlatması kaldır simgesi](./media/user-guide/fx-events/image14.png)    | <span data-ttu-id="0d3a2-137">İç g/ç sürücü sürücüsü başlatması kaldır</span><span class="sxs-lookup"><span data-stu-id="0d3a2-137">Internal I / O Driver Driver Un-initialize</span></span> |
| ![Dizin özniteliklerini oku simgesi](./media/user-guide/fx-events/image15.png)    | <span data-ttu-id="0d3a2-139">**Dizin öznitelikleri okuma** (*fx_directory_attributes_read*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-139">**Directory Attributes Read** (*fx_directory_attributes_read*)</span></span> |
| ![Dizin öznitelikleri kümesi simgesi](./media/user-guide/fx-events/image16.png)    | <span data-ttu-id="0d3a2-141">**Dizin öznitelikleri kümesi** (*fx_directory_attributes_set*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-141">**Directory Attributes Set** (*fx_directory_attributes_set*)</span></span> |
| ![Dizin oluşturma simgesi](./media/user-guide/fx-events/image17.png)    | <span data-ttu-id="0d3a2-143">**Dizin oluşturma** (*fx_directory_create*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-143">**Directory Create** (*fx_directory_create*)</span></span> |
| ![Dizin varsayılanı al simgesi](./media/user-guide/fx-events/image18.png)    | <span data-ttu-id="0d3a2-145">**Dizin varsayılanı al** (*fx_directory_default_get*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-145">**Directory Default Get** (*fx_directory_default_get*)</span></span> |
| ![Dizin varsayılan kümesi simgesi](./media/user-guide/fx-events/image19.png)    | <span data-ttu-id="0d3a2-147">**Dizin varsayılan kümesi** (*fx_directory_default_set*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-147">**Directory Default Set** (*fx_directory_default_set*)</span></span> |
| ![Dizin silme simgesi](./media/user-guide/fx-events/image20.png)    | <span data-ttu-id="0d3a2-149">**Dizin silme** (*fx_directory_delete*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-149">**Directory Delete** (*fx_directory_delete*)</span></span> |
| ![Dizin Ilk girişi bul simgesi](./media/user-guide/fx-events/image21.png)    | <span data-ttu-id="0d3a2-151">**Dizin Ilk giriş bulma** (*fx_directory_first_entry_find*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-151">**Directory First Entry Find** (*fx_directory_first_entry_find*)</span></span> |
| ![Dizinin Ilk tam giriş bul simgesi](./media/user-guide/fx-events/image22.png)    | <span data-ttu-id="0d3a2-153">**Dizinin Ilk tam girişi bul** (*fx_directory_first_full_entry_find*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-153">**Directory First Full Entry Find** (*fx_directory_first_full_entry_find*)</span></span> |
| ![Dizin bilgileri al simgesi](./media/user-guide/fx-events/image23.png)    | <span data-ttu-id="0d3a2-155">**Dizin bilgileri al** (*fx_directory_information_get*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-155">**Directory Information Get** (*fx_directory_information_get*)</span></span> |
| ![Dizin yerel yolu temizle simgesi](./media/user-guide/fx-events/image24.png)    | <span data-ttu-id="0d3a2-157">**Dizin yerel yolu temizle** (*fx_directory_local_path_clear*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-157">**Directory Local Path Clear** (*fx_directory_local_path_clear*)</span></span> |
| ![Dizin yerel yolu al simgesi](./media/user-guide/fx-events/image25.png)    | <span data-ttu-id="0d3a2-159">**Dizin yerel yolu al** (*fx_directory_local_path_get*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-159">**Directory Local Path Get** (*fx_directory_local_path_get*)</span></span> |
| ![Dizin yerel yolu geri yükleme simgesi](./media/user-guide/fx-events/image26.png)    | <span data-ttu-id="0d3a2-161">**Dizin yerel yolunu geri yükleme** (*fx_directory_local_path_restore*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-161">**Directory Local Path Restore** (*fx_directory_local_path_restore*)</span></span> |
| ![Dizin yerel yolu kümesi simgesi](./media/user-guide/fx-events/image27.png)    | <span data-ttu-id="0d3a2-163">**Dizin yerel yol kümesi** (*fx_directory_local_path_set*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-163">**Directory Local Path Set** (*fx_directory_local_path_set*)</span></span> |
| ![Dizin uzun adı Al simgesi](./media/user-guide/fx-events/image28.png)    | <span data-ttu-id="0d3a2-165">**Dizin uzun adı Al** (*fx_directory_long_name_get*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-165">**Directory Long Name Get** (*fx_directory_long_name_get*)</span></span> |
| ![Dizin adı test simgesi](./media/user-guide/fx-events/image29.png)    | <span data-ttu-id="0d3a2-167">**Dizin adı testi** (*fx_directory_name_test*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-167">**Directory Name Test** (*fx_directory_name_test*)</span></span> |
| ![Dizin sonraki giriş bul simgesi](./media/user-guide/fx-events/image30.png)    | <span data-ttu-id="0d3a2-169">**Dizin sonraki giriş bul** (*fx_directory_next_entry_find*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-169">**Directory Next Entry Find** (*fx_directory_next_entry_find*)</span></span> |
| ![Dizin bir sonraki tam giriş bul simgesi](./media/user-guide/fx-events/image31.png)    | <span data-ttu-id="0d3a2-171">**Dizin bir sonraki tam girdi bul** (*fx_directory_next_full_entry_find*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-171">**Directory Next Full Entry Find** (*fx_directory_next_full_entry_find*)</span></span> |
| ![Dizin yeniden adlandırma simgesi](./media/user-guide/fx-events/image32.png)    | <span data-ttu-id="0d3a2-173">**Dizin yeniden adlandırma** (*fx_directory_rename*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-173">**Directory Rename** (*fx_directory_rename*)</span></span> |
| ![Dizin kısa adı Al simgesi](./media/user-guide/fx-events/image33.png)    | <span data-ttu-id="0d3a2-175">**Dizin kısa adı Get** (*fx_directory_short_name_get*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-175">**Directory Short Name Get** (*fx_directory_short_name_get*)</span></span> |
| ![Dosya ayırma simgesi](./media/user-guide/fx-events/image34.png)    | <span data-ttu-id="0d3a2-177">**Dosya ayırma** (*fx_file_allocate*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-177">**File Allocate** (*fx_file_allocate*)</span></span> |
| ![Dosya öznitelikleri okuma simgesi](./media/user-guide/fx-events/image35.png)    | <span data-ttu-id="0d3a2-179">**Dosya öznitelikleri okuma** (*fx_file_attributes_read*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-179">**File Attributes Read** (*fx_file_attributes_read*)</span></span> |
| ![Dosya öznitelikleri kümesi simgesi](./media/user-guide/fx-events/image36.png)    | <span data-ttu-id="0d3a2-181">**Dosya öznitelikleri kümesi** (*fx_file_attributes_set*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-181">**File Attributes Set** (*fx_file_attributes_set*)</span></span> |
| ![Dosya En Iyi çaba ayırma simgesi](./media/user-guide/fx-events/image37.png)    | <span data-ttu-id="0d3a2-183">**Dosya En Iyi efor tahsisi** (*fx_file_best_effort_allocate*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-183">**File Best Effort Allocate** (*fx_file_best_effort_allocate*)</span></span> |
| ![Dosya Kapat simgesi](./media/user-guide/fx-events/image38.png)    | <span data-ttu-id="0d3a2-185">**Dosya Kapat** (*fx_file_close*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-185">**File Close** (*fx_file_close*)</span></span> |
| ![Dosya oluşturma simgesi](./media/user-guide/fx-events/image39.png)    | <span data-ttu-id="0d3a2-187">**Dosya oluşturma** (*fx_file_create*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-187">**File Create** (*fx_file_create*)</span></span> |
| ![Dosya tarih saat kümesi simgesi](./media/user-guide/fx-events/image40.png)    | <span data-ttu-id="0d3a2-189">**Dosya tarih saat kümesi** (*fx_file_date_time_set*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-189">**File Date Time Set** (*fx_file_date_time_set*)</span></span> |
| ![Dosya silme simgesi](./media/user-guide/fx-events/image41.png)    | <span data-ttu-id="0d3a2-191">**Dosya silme** (*fx_file_delete*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-191">**File Delete** (*fx_file_delete*)</span></span> |
| ![Dosya aç simgesi](./media/user-guide/fx-events/image42.png)    | <span data-ttu-id="0d3a2-193">**Dosya açık** (*fx_file_open*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-193">**File Open** (*fx_file_open*)</span></span> |
| ![Dosya okuma simgesi](./media/user-guide/fx-events/image43.png)    | <span data-ttu-id="0d3a2-195">**Dosya okuma** (*fx_file_read*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-195">**File Read** (*fx_file_read*)</span></span> |
| ![Dosya göreli arama simgesi](./media/user-guide/fx-events/image44.png)    | <span data-ttu-id="0d3a2-197">**Dosya göreli arama** (*fx_file_relative_seek*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-197">**File Relative Seek** (*fx_file_relative_seek*)</span></span> |
| ![Dosya yeniden adlandırma simgesi](./media/user-guide/fx-events/image45.png)    | <span data-ttu-id="0d3a2-199">**Dosya yeniden adlandırma** (*fx_file_rename*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-199">**File Rename** (*fx_file_rename*)</span></span> |
| ![Dosya arama simgesi](./media/user-guide/fx-events/image46.png)    | <span data-ttu-id="0d3a2-201">**Dosya ara** (*fx_file_seek*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-201">**File Seek** (*fx_file_seek*)</span></span> |
| ![Dosya kesme simgesi](./media/user-guide/fx-events/image47.png)    | <span data-ttu-id="0d3a2-203">**Dosya Kes** (*fx_file_truncate*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-203">**File Truncate** (*fx_file_truncate*)</span></span> |
| ![Dosya kesme sürümü simgesi](./media/user-guide/fx-events/image48.png)    | <span data-ttu-id="0d3a2-205">**Dosya kesme sürümü** (*fx_file_truncate_release*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-205">**File Truncate Release** (*fx_file_truncate_release*)</span></span> |
| ![Dosya yazma simgesi](./media/user-guide/fx-events/image49.png)    | <span data-ttu-id="0d3a2-207">**Dosya yazma** (*fx_file_write*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-207">**File Write** (*fx_file_write*)</span></span> |
| ![Medya Iptali simgesi](./media/user-guide/fx-events/image50.png)    | <span data-ttu-id="0d3a2-209">**Medya iptali** (*fx_media_abort*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-209">**Media Abort** (*fx_media_abort*)</span></span> |
| ![Medya önbelleği geçersiz kıl simgesi](./media/user-guide/fx-events/image51.png)    | <span data-ttu-id="0d3a2-211">**Medya önbelleği geçersiz kıl** (*fx_media_cache_invalidate*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-211">**Media Cache Invalidate** (*fx_media_cache_invalidate*)</span></span> |
| ![Medya onay simgesi](./media/user-guide/fx-events/image52.png)    | <span data-ttu-id="0d3a2-213">**Medya denetimi** (*fx_media_check*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-213">**Media Check** (*fx_media_check*)</span></span> |
| ![\* Medya kapatma simgesi](./media/user-guide/fx-events/image53.png)    | <span data-ttu-id="0d3a2-215">**Medya kapatma** (*fx_media_close*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-215">**Media Close** (*fx_media_close*)</span></span> |
| ![Medya Temizleme simgesi](./media/user-guide/fx-events/image54.png)    | <span data-ttu-id="0d3a2-217">**Medya Temizleme** (*fx_media_flush*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-217">**Media Flush** (*fx_media_flush*)</span></span> |
| ![Medya biçimi simgesi](./media/user-guide/fx-events/image55.png)    | <span data-ttu-id="0d3a2-219">**Medya biçimi** (*fx_media_format*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-219">**Media Format** (*fx_media_format*)</span></span> |
| ![Medya açma simgesi](./media/user-guide/fx-events/image56.png)    | <span data-ttu-id="0d3a2-221">**Medya açık** (*fx_media_open*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-221">**Media Open** (*fx_media_open*)</span></span> |
| ![Medya okuma simgesi](./media/user-guide/fx-events/image57.png)    | <span data-ttu-id="0d3a2-223">**Medya okuma** (*fx_media_read*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-223">**Media Read** (*fx_media_read*)</span></span> |
| ![Medya alanı kullanılabilir simgesi](./media/user-guide/fx-events/image58.png)    | <span data-ttu-id="0d3a2-225">**Kullanılabilir medya alanı** (*fx_media_space_available*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-225">**Media Space Available** (*fx_media_space_available*)</span></span> |
| ![Medya birimi al simgesi](./media/user-guide/fx-events/image59.png)    | <span data-ttu-id="0d3a2-227">**Medya hacmi al** (*fx_media_volume_get*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-227">**Media Volume Get** (*fx_media_volume_get*)</span></span> |
| ![Medya birimi kümesi simgesi](./media/user-guide/fx-events/image60.png)    | <span data-ttu-id="0d3a2-229">**Medya birimi kümesi** (*fx_media_volume_set*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-229">**Media Volume Set** (*fx_media_volume_set*)</span></span> |
| ![Medya yazma simgesi](./media/user-guide/fx-events/image61.png)    | <span data-ttu-id="0d3a2-231">**Medya yazma** (*fx_media_write*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-231">**Media Write** (*fx_media_write*)</span></span> |
| ![Sistem tarihi al simgesi](./media/user-guide/fx-events/image62.png)    | <span data-ttu-id="0d3a2-233">**Sistem tarihi al** (*fx_system_date_get*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-233">**System Date Get** (*fx_system_date_get*)</span></span> |
| ![Sistem tarihi kümesi simgesi](./media/user-guide/fx-events/image63.png)    | <span data-ttu-id="0d3a2-235">**Sistem tarihi kümesi** (*fx_system_date_set*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-235">**System Date Set** (*fx_system_date_set*)</span></span> |
| ![Sistem başlatma simgesi](./media/user-guide/fx-events/image64.png)    | <span data-ttu-id="0d3a2-237">**Sistem başlatma** (*fx_system_initialize*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-237">**System Initialize** (*fx_system_initialize*)</span></span> |
| ![Sistem saati al simgesi](./media/user-guide/fx-events/image65.png)    | <span data-ttu-id="0d3a2-239">**Sistem saati al** (*fx_system_time_get*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-239">**System Time Get** (*fx_system_time_get*)</span></span> |
| ![Sistem zaman kümesi simgesi](./media/user-guide/fx-events/image66.png)    | <span data-ttu-id="0d3a2-241">**Sistem zaman kümesi** (*fx_system_time_set*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-241">**System Time Set** (*fx_system_time_set*)</span></span> |
| ![Unicode dizin oluşturma simgesi](./media/user-guide/fx-events/image67.png)    | <span data-ttu-id="0d3a2-243">**Unicode dizin oluşturma** (*fx_unicode_directory_create*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-243">**Unicode Directory Create** (*fx_unicode_directory_create*)</span></span> |
| ![Unicode dizin yeniden adlandırma simgesi](./media/user-guide/fx-events/image68.png)    | <span data-ttu-id="0d3a2-245">**Unicode dizin yeniden adlandırma** (*fx_unicode_directory_rename*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-245">**Unicode Directory Rename** (*fx_unicode_directory_rename*)</span></span> |
| ![Unicode dosya oluştur simgesi](./media/user-guide/fx-events/image69.png)    | <span data-ttu-id="0d3a2-247">**Unicode dosya oluşturma** (*fx_unicode_file_create*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-247">**Unicode File Create** (*fx_unicode_file_create*)</span></span> |
| ![Unicode dosya yeniden adlandırma simgesi](./media/user-guide/fx-events/image70.png)    | <span data-ttu-id="0d3a2-249">**Unicode dosya yeniden adlandırma** (*fx_unicode_file_rename*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-249">**Unicode File Rename** (*fx_unicode_file_rename*)</span></span> |
| ![Unicode Lensağ al simgesi](./media/user-guide/fx-events/image71.png)    | <span data-ttu-id="0d3a2-251">**Unicode Lenlen al** (*fx_unicode_length_get*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-251">**Unicode Lenght Get** (*fx_unicode_length_get*)</span></span> |
| ![Unicode ad Al simgesi](./media/user-guide/fx-events/image72.png)    | <span data-ttu-id="0d3a2-253">**Unicode adı Al** (*fx_unicode_name_get*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-253">**Unicode Name Get** (*fx_unicode_name_get*)</span></span> |
| ![Unicode kısa ad Al simgesi](./media/user-guide/fx-events/image73.png)    | <span data-ttu-id="0d3a2-255">**Unicode kısa adı Get** (*fx_unicode_short_name_get*)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-255">**Unicode Short Name Get** (*fx_unicode_short_name_get*)</span></span> |

## <a name="event-descriptions"></a><span data-ttu-id="0d3a2-256">Olay Açıklamaları</span><span class="sxs-lookup"><span data-stu-id="0d3a2-256">Event Descriptions</span></span>

<span data-ttu-id="0d3a2-257">Aşağıda her bir olay açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-257">The following describes each individual event.</span></span>

### <a name="internal-logical-sector-cache-miss"></a><span data-ttu-id="0d3a2-258">İç mantıksal kesim önbelleği Isabetsizlik</span><span class="sxs-lookup"><span data-stu-id="0d3a2-258">Internal Logical Sector Cache Miss</span></span> 

#### <a name="internal-logical-sector-cache-miss"></a><span data-ttu-id="0d3a2-259">İç mantıksal kesim önbelleği isabetsizlik</span><span class="sxs-lookup"><span data-stu-id="0d3a2-259">Internal logical sector cache miss</span></span>

<span data-ttu-id="0d3a2-260">**Simge** ![ İç mantıksal kesim önbelleğinde isabetsizlik simgesi](./media/user-guide/fx-events/image1.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-260">**Icon** ![Internal logical sector cache miss icon](./media/user-guide/fx-events/image1.png)</span></span>

<span data-ttu-id="0d3a2-261">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-261">**Description**</span></span>

<span data-ttu-id="0d3a2-262">Bu olay bir iç FileX mantıksal sektör önbelleğinin isabetsiz olduğunu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-262">This event represents an internal FileX logical sector cache miss.</span></span>

<span data-ttu-id="0d3a2-263">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-263">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-264">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-264">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-265">Bilgi alanı 2: sektör.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-265">Info Field 2: Sector.</span></span>
- <span data-ttu-id="0d3a2-266">Bilgi alanı 3: Toplam isabetsizlik sayısı.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-266">Info Field 3: Total misses.</span></span>
- <span data-ttu-id="0d3a2-267">Bilgi alanı 4: önbellek boyutu.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-267">Info Field 4: Cache size.</span></span>

### <a name="internal-directory-cache-miss"></a><span data-ttu-id="0d3a2-268">İç dizin önbelleğinde Isabetsizlik</span><span class="sxs-lookup"><span data-stu-id="0d3a2-268">Internal Directory Cache Miss</span></span>

#### <a name="internal-directory-cache-miss"></a><span data-ttu-id="0d3a2-269">İç dizin önbelleğinde isabetsizlik</span><span class="sxs-lookup"><span data-stu-id="0d3a2-269">Internal directory cache miss</span></span>

<span data-ttu-id="0d3a2-270">**Simge** ![ İç dizin önbelleği isabetsizlik simgesi](./media/user-guide/fx-events/image2.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-270">**Icon** ![Internal directory cache miss icon](./media/user-guide/fx-events/image2.png)</span></span>

<span data-ttu-id="0d3a2-271">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-271">**Description**</span></span> 

<span data-ttu-id="0d3a2-272">Bu olay bir iç FileX dizin önbelleğinin isabetsiz olduğunu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-272">This event represents an internal FileX directory cache miss.</span></span>

<span data-ttu-id="0d3a2-273">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-273">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-274">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-274">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-275">Bilgi alanı 2: Toplam isabetsizlik sayısı.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-275">Info Field 2: Total misses.</span></span>
- <span data-ttu-id="0d3a2-276">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-276">Info Field 3: Not used.</span></span>
- <span data-ttu-id="0d3a2-277">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-277">Info Field 4: Not used.</span></span>

### <a name="internal-media-flush"></a><span data-ttu-id="0d3a2-278">İç medya Temizleme</span><span class="sxs-lookup"><span data-stu-id="0d3a2-278">Internal Media Flush</span></span> 

#### <a name="internal-media-flush"></a><span data-ttu-id="0d3a2-279">İç medya Temizleme</span><span class="sxs-lookup"><span data-stu-id="0d3a2-279">Internal media flush</span></span>

<span data-ttu-id="0d3a2-280">**Simge** ![ İç medya Temizleme simgesi](./media/user-guide/fx-events/image3.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-280">**Icon** ![Internal media flush icon](./media/user-guide/fx-events/image3.png)</span></span>

<span data-ttu-id="0d3a2-281">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-281">**Description**</span></span>

<span data-ttu-id="0d3a2-282">Bu olay bir iç FileX medyası temizleme işlemini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-282">This event represents an internal FileX media flush.</span></span>

<span data-ttu-id="0d3a2-283">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-283">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-284">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-284">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-285">Bilgi alanı 2: kirli kesimlerin sayısı.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-285">Info Field 2: Number of dirty sectors.</span></span>
- <span data-ttu-id="0d3a2-286">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-286">Info Field 3: Not used.</span></span>
- <span data-ttu-id="0d3a2-287">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-287">Info Field 4: Not used.</span></span>


### <a name="internal-directory-entry-read"></a><span data-ttu-id="0d3a2-288">İç dizin girişi okundu</span><span class="sxs-lookup"><span data-stu-id="0d3a2-288">Internal Directory Entry Read</span></span> 

#### <a name="internal-directory-entry-read"></a><span data-ttu-id="0d3a2-289">İç dizin girişi okundu</span><span class="sxs-lookup"><span data-stu-id="0d3a2-289">Internal directory entry read</span></span>

<span data-ttu-id="0d3a2-290">**Simge** ![ İç dizin girişi okuma simgesi](./media/user-guide/fx-events/image4.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-290">**Icon** ![Internal directory entry read icon](./media/user-guide/fx-events/image4.png)</span></span>

<span data-ttu-id="0d3a2-291">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-291">**Description**</span></span>

<span data-ttu-id="0d3a2-292">Bu olay bir iç FileX Dizin girişi okuma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-292">This event represents an internal FileX directory entry read event.</span></span>

<span data-ttu-id="0d3a2-293">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-293">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-294">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-294">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-295">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-295">Info Field 2: Not used.</span></span>
- <span data-ttu-id="0d3a2-296">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-296">Info Field 3: Not used.</span></span>
- <span data-ttu-id="0d3a2-297">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-297">Info Field 4: Not used.</span></span>

### <a name="internal-directory-entry-write"></a><span data-ttu-id="0d3a2-298">İç dizin girişi yazma</span><span class="sxs-lookup"><span data-stu-id="0d3a2-298">Internal Directory Entry Write</span></span>

#### <a name="internal-directory-entry-write"></a><span data-ttu-id="0d3a2-299">İç dizin girişi yazma</span><span class="sxs-lookup"><span data-stu-id="0d3a2-299">Internal directory entry write</span></span>

<span data-ttu-id="0d3a2-300">**Simge** ![ İç dizin girişi yazma simgesi](./media/user-guide/fx-events/image5.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-300">**Icon** ![Internal directory entry write icon](./media/user-guide/fx-events/image5.png)</span></span>

<span data-ttu-id="0d3a2-301">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-301">**Description**</span></span>

<span data-ttu-id="0d3a2-302">Bu olay bir iç FileX Dizin girişi yazma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-302">This event represents an internal FileX directory entry write event.</span></span>

<span data-ttu-id="0d3a2-303">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-303">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-304">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-304">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-305">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-305">Info Field 2: Not used.</span></span>
- <span data-ttu-id="0d3a2-306">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-306">Info Field 3: Not used.</span></span>
- <span data-ttu-id="0d3a2-307">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-307">Info Field 4: Not used.</span></span>

### <a name="internal-io-driver-read"></a><span data-ttu-id="0d3a2-308">İç g/ç sürücüsü okuma</span><span class="sxs-lookup"><span data-stu-id="0d3a2-308">Internal I/O Driver Read</span></span> 

#### <a name="internal-io-driver-read"></a><span data-ttu-id="0d3a2-309">İç g/ç sürücüsü okuma</span><span class="sxs-lookup"><span data-stu-id="0d3a2-309">Internal I/O driver read</span></span> 

<span data-ttu-id="0d3a2-310">**Simge** ![ İç g/ç sürücüsü okuma simgesi](./media/user-guide/fx-events/image6.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-310">**Icon** ![Internal I / O driver read icon](./media/user-guide/fx-events/image6.png)</span></span>

<span data-ttu-id="0d3a2-311">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-311">**Description**</span></span> 

<span data-ttu-id="0d3a2-312">Bu olay iç bir FileX g/ç sürücüsü okuma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-312">This event represents an internal FileX I/O driver read event.</span></span>

<span data-ttu-id="0d3a2-313">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-313">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-314">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-314">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-315">Bilgi alanı 2: sektör.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-315">Info Field 2: Sector.</span></span>
- <span data-ttu-id="0d3a2-316">Bilgi alanı 3: sektör sayısı.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-316">Info Field 3: Number of sectors.</span></span>
- <span data-ttu-id="0d3a2-317">Bilgi alanı 4: arabellek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-317">Info Field 4: Buffer pointer.</span></span>

### <a name="internal-io-driver-write"></a><span data-ttu-id="0d3a2-318">İç g/ç sürücüsü yazma</span><span class="sxs-lookup"><span data-stu-id="0d3a2-318">Internal I/O Driver Write</span></span> 

#### <a name="internal-io-driver-write"></a><span data-ttu-id="0d3a2-319">İç g/ç sürücüsü yazma</span><span class="sxs-lookup"><span data-stu-id="0d3a2-319">Internal I/O driver write</span></span> 

<span data-ttu-id="0d3a2-320">**Simge** ![ İç g/ç sürücüsü yazma simgesi](./media/user-guide/fx-events/image7.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-320">**Icon** ![Internal I / O driver write icon](./media/user-guide/fx-events/image7.png)</span></span>

<span data-ttu-id="0d3a2-321">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-321">**Description**</span></span> 

<span data-ttu-id="0d3a2-322">Bu olay bir iç FileX g/ç sürücüsü yazma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-322">This event represents an internal FileX I/O driver write event.</span></span>

<span data-ttu-id="0d3a2-323">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-323">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-324">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-324">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-325">Bilgi alanı 2: sektör.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-325">Info Field 2: Sector.</span></span>
- <span data-ttu-id="0d3a2-326">Bilgi alanı 3: sektör sayısı.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-326">Info Field 3: Number of sectors.</span></span>
- <span data-ttu-id="0d3a2-327">Bilgi alanı 4: arabellek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-327">Info Field 4: Buffer pointer.</span></span>

### <a name="internal-io-driver-flush"></a><span data-ttu-id="0d3a2-328">İç g/ç sürücüsü Temizleme</span><span class="sxs-lookup"><span data-stu-id="0d3a2-328">Internal I/O Driver Flush</span></span> 

#### <a name="internal-io-driver-flush"></a><span data-ttu-id="0d3a2-329">İç g/ç sürücüsü Temizleme</span><span class="sxs-lookup"><span data-stu-id="0d3a2-329">Internal I/O driver flush</span></span> 

<span data-ttu-id="0d3a2-330">**Simge** ![ İç g/ç sürücüsü Temizleme simgesi](./media/user-guide/fx-events/image8.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-330">**Icon** ![Internal I / O driver flush icon](./media/user-guide/fx-events/image8.png)</span></span>

<span data-ttu-id="0d3a2-331">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-331">**Description**</span></span> 

<span data-ttu-id="0d3a2-332">Bu olay bir iç FileX g/ç Sürücü temizleme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-332">This event represents an internal FileX I/O driver flush event.</span></span>

<span data-ttu-id="0d3a2-333">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-333">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-334">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-334">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-335">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-335">Info Field 2: Not used.</span></span>
- <span data-ttu-id="0d3a2-336">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-336">Info Field 3: Not used.</span></span>
- <span data-ttu-id="0d3a2-337">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-337">Info Field 4: Not used.</span></span>

### <a name="internal-io-driver-abort"></a><span data-ttu-id="0d3a2-338">İç g/ç sürücüsü Iptali</span><span class="sxs-lookup"><span data-stu-id="0d3a2-338">Internal I/O Driver Abort</span></span> 

#### <a name="internal-io-dirver-abort"></a><span data-ttu-id="0d3a2-339">İç g/ç dirver iptali</span><span class="sxs-lookup"><span data-stu-id="0d3a2-339">Internal I/O dirver abort</span></span>

<span data-ttu-id="0d3a2-340">**Simge** ![ İç g/ç sürücüsü iptali simgesi](./media/user-guide/fx-events/image9.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-340">**Icon** ![Internal I / O driver abort icon](./media/user-guide/fx-events/image9.png)</span></span>

<span data-ttu-id="0d3a2-341">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-341">**Description**</span></span>

<span data-ttu-id="0d3a2-342">Bu olay bir iç FileX g/ç sürücüsü iptali olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-342">This event represents an internal FileX I/O driver abort event.</span></span>

<span data-ttu-id="0d3a2-343">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-343">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-344">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-344">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-345">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-345">Info Field 2: Not used.</span></span>
- <span data-ttu-id="0d3a2-346">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-346">Info Field 3: Not used.</span></span>
- <span data-ttu-id="0d3a2-347">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-347">Info Field 4: Not used.</span></span>

### <a name="internal-io-driver-initialize"></a><span data-ttu-id="0d3a2-348">İç g/ç sürücüsü başlatma</span><span class="sxs-lookup"><span data-stu-id="0d3a2-348">Internal I/O Driver Initialize</span></span> 

#### <a name="internal-io-driver-initialize"></a><span data-ttu-id="0d3a2-349">İç g/ç sürücüsü başlatma</span><span class="sxs-lookup"><span data-stu-id="0d3a2-349">Internal I/O driver initialize</span></span> 

<span data-ttu-id="0d3a2-350">**Simge** ![ İç g/ç sürücüsü başlatma simgesi](./media/user-guide/fx-events/image10.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-350">**Icon** ![Internal I / O driver initialize icon](./media/user-guide/fx-events/image10.png)</span></span>

<span data-ttu-id="0d3a2-351">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-351">**Description**</span></span> 

<span data-ttu-id="0d3a2-352">Bu olay bir iç FileX g/ç sürücüsü başlatma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-352">This event represents an internal FileX I/O driver initialize event.</span></span>

<span data-ttu-id="0d3a2-353">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-353">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-354">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-354">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-355">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-355">Info Field 2: Not used.</span></span>
- <span data-ttu-id="0d3a2-356">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-356">Info Field 3: Not used.</span></span>
- <span data-ttu-id="0d3a2-357">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-357">Info Field 4: Not used.</span></span>

### <a name="internal-io-driver-boot-sector-read"></a><span data-ttu-id="0d3a2-358">İç g/ç sürücüsü önyükleme kesimi okuma</span><span class="sxs-lookup"><span data-stu-id="0d3a2-358">Internal I/O Driver Boot Sector Read</span></span> 

#### <a name="internal-io-driver-boot-sector-read"></a><span data-ttu-id="0d3a2-359">İç g/ç sürücüsü önyükleme kesimi okuma</span><span class="sxs-lookup"><span data-stu-id="0d3a2-359">Internal I/O driver boot sector read</span></span> 

<span data-ttu-id="0d3a2-360">**Simge** ![ İç g/ç sürücüsü önyükleme kesimini okuma simgesi](./media/user-guide/fx-events/image11.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-360">**Icon** ![Internal I / O driver boot sector read icon](./media/user-guide/fx-events/image11.png)</span></span>

<span data-ttu-id="0d3a2-361">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-361">**Description**</span></span> 

<span data-ttu-id="0d3a2-362">Bu olay bir iç FileX g/ç sürücüsü önyükleme kesimi okuma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-362">This event represents an internal FileX I/O driver boot sector read event.</span></span>

<span data-ttu-id="0d3a2-363">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-363">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-364">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-364">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-365">Bilgi alanı 2: arabellek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-365">Info Field 2: Buffer pointer.</span></span>
- <span data-ttu-id="0d3a2-366">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-366">Info Field 3: Not used.</span></span>
- <span data-ttu-id="0d3a2-367">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-367">Info Field 4: Not used.</span></span>

### <a name="internal-io-driver-release-sectors"></a><span data-ttu-id="0d3a2-368">İç g/ç sürücüsü sürüm kesimleri</span><span class="sxs-lookup"><span data-stu-id="0d3a2-368">Internal I/O Driver Release Sectors</span></span> 

#### <a name="internal-io-driver-release-sectors"></a><span data-ttu-id="0d3a2-369">İç g/ç sürücüsü sürüm kesimleri</span><span class="sxs-lookup"><span data-stu-id="0d3a2-369">Internal I/O driver release sectors</span></span> 

<span data-ttu-id="0d3a2-370">**Simge** ![ İç g/ç sürücüsü sürüm kesimleri simgesi](./media/user-guide/fx-events/image12.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-370">**Icon** ![Internal I / O driver release sectors icon](./media/user-guide/fx-events/image12.png)</span></span>

<span data-ttu-id="0d3a2-371">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-371">**Description**</span></span> 

<span data-ttu-id="0d3a2-372">Bu olay bir iç FileX g/ç sürücüsü sürüm kesimleri olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-372">This event represents an internal FileX I/O driver release sectors event.</span></span>

<span data-ttu-id="0d3a2-373">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-373">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-374">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-374">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-375">Bilgi alanı 2: sektör.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-375">Info Field 2: Sector.</span></span>
- <span data-ttu-id="0d3a2-376">Bilgi alanı 3: sektör sayısı.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-376">Info Field 3: Number of sectors.</span></span>
- <span data-ttu-id="0d3a2-377">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-377">Info Field 4: Not used.</span></span>

### <a name="internal-io-driver-boot-sector-write"></a><span data-ttu-id="0d3a2-378">İç g/ç sürücüsü önyükleme kesimi yazma</span><span class="sxs-lookup"><span data-stu-id="0d3a2-378">Internal I/O Driver Boot Sector Write</span></span>

#### <a name="internal-io-driver-boot-sector-write"></a><span data-ttu-id="0d3a2-379">İç g/ç sürücüsü önyükleme kesimi yazma</span><span class="sxs-lookup"><span data-stu-id="0d3a2-379">Internal I/O driver boot sector write</span></span> 

<span data-ttu-id="0d3a2-380">**Simge** ![ İç g/ç sürücüsü önyükleme kesimi yazma simgesi](./media/user-guide/fx-events/image13.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-380">**Icon** ![Internal I / O driver boot sector write icon](./media/user-guide/fx-events/image13.png)</span></span>

<span data-ttu-id="0d3a2-381">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-381">**Description**</span></span> 

<span data-ttu-id="0d3a2-382">Bu olay bir iç FileX g/ç sürücüsü önyükleme kesimi yazma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-382">This event represents an internal FileX I/O driver boot sector write event.</span></span>

<span data-ttu-id="0d3a2-383">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-383">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-384">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-384">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-385">Bilgi alanı 2: arabellek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-385">Info Field 2: Buffer pointer.</span></span>
- <span data-ttu-id="0d3a2-386">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-386">Info Field 3: Not used.</span></span>
- <span data-ttu-id="0d3a2-387">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-387">Info Field 4: Not used.</span></span>

### <a name="internal-io-driver-un-initialize"></a><span data-ttu-id="0d3a2-388">İç g/ç sürücüsü başlatması geri al</span><span class="sxs-lookup"><span data-stu-id="0d3a2-388">Internal I/O Driver Un-initialize</span></span> 

#### <a name="internal-io-driver-un-initialize"></a><span data-ttu-id="0d3a2-389">İç g/ç sürücüsü başlatması geri al</span><span class="sxs-lookup"><span data-stu-id="0d3a2-389">Internal I/O driver un-initialize</span></span> 

<span data-ttu-id="0d3a2-390">**Simge** ![ İç g/ç sürücüsü başlatması kaldır simgesi](./media/user-guide/fx-events/image14.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-390">**Icon** ![Internal I / O driver un-initialize icon](./media/user-guide/fx-events/image14.png)</span></span>

<span data-ttu-id="0d3a2-391">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-391">**Description**</span></span> 

<span data-ttu-id="0d3a2-392">Bu olay iç bir FileX g/ç sürücüsü başlatma kaldırma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-392">This event represents an internal FileX I/O driver un-initialize event.</span></span>

<span data-ttu-id="0d3a2-393">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-393">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-394">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-394">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-395">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-395">Info Field 2: Not used.</span></span>
- <span data-ttu-id="0d3a2-396">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-396">Info Field 3: Not used.</span></span>
- <span data-ttu-id="0d3a2-397">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-397">Info Field 4: Not used.</span></span>
</blockquote></td>

### <a name="directory-attributes-read"></a><span data-ttu-id="0d3a2-398">Okunan dizin öznitelikleri</span><span class="sxs-lookup"><span data-stu-id="0d3a2-398">Directory Attributes Read</span></span> 

#### <a name="fx_directory_attributes_read"></a><span data-ttu-id="0d3a2-399">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="0d3a2-399">fx_directory_attributes_read</span></span> 

<span data-ttu-id="0d3a2-400">**Simge** ![ Dizin özniteliklerini oku simgesi](./media/user-guide/fx-events/image15.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-400">**Icon** ![Directory attributes read icon](./media/user-guide/fx-events/image15.png)</span></span>

<span data-ttu-id="0d3a2-401">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-401">**Description**</span></span> 

<span data-ttu-id="0d3a2-402">Bu olay, bir dizin özniteliklerini oku olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-402">This event represents a directory attributes read event.</span></span>

<span data-ttu-id="0d3a2-403">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-403">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-404">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-404">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-405">Bilgi alanı 2: Dizin adı Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-405">Info Field 2: Pointer to directory name.</span></span>
- <span data-ttu-id="0d3a2-406">Bilgi alanı 3: öznitelikler bit eşlemesi:</span><span class="sxs-lookup"><span data-stu-id="0d3a2-406">Info Field 3: Attributes bit map:</span></span>

  | <span data-ttu-id="0d3a2-407">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="0d3a2-407">Attribute</span></span>                         | <span data-ttu-id="0d3a2-408">Değer</span><span class="sxs-lookup"><span data-stu-id="0d3a2-408">Value</span></span>        |
  |---------------------------------- | --------|
  |  <span data-ttu-id="0d3a2-409">Salt Okunur</span><span class="sxs-lookup"><span data-stu-id="0d3a2-409">Read Only</span></span>                        | <span data-ttu-id="0d3a2-410">0x01</span><span class="sxs-lookup"><span data-stu-id="0d3a2-410">(0x01)</span></span>  |
  |  <span data-ttu-id="0d3a2-411">Gizli</span><span class="sxs-lookup"><span data-stu-id="0d3a2-411">Hidden</span></span>                           | <span data-ttu-id="0d3a2-412">0x02 şeklindedir</span><span class="sxs-lookup"><span data-stu-id="0d3a2-412">(0x02)</span></span>  |
  |  <span data-ttu-id="0d3a2-413">Sistem</span><span class="sxs-lookup"><span data-stu-id="0d3a2-413">System</span></span>                           | <span data-ttu-id="0d3a2-414">(0x04)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-414">(0x04)</span></span>  |
  |  <span data-ttu-id="0d3a2-415">Birim</span><span class="sxs-lookup"><span data-stu-id="0d3a2-415">Volume</span></span>                           | <span data-ttu-id="0d3a2-416">(0x08)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-416">(0x08)</span></span>  |
  |  <span data-ttu-id="0d3a2-417">Dizin</span><span class="sxs-lookup"><span data-stu-id="0d3a2-417">Directory</span></span>                        | <span data-ttu-id="0d3a2-418">0x10</span><span class="sxs-lookup"><span data-stu-id="0d3a2-418">(0x10)</span></span>  |
  |  <span data-ttu-id="0d3a2-419">Arşiv</span><span class="sxs-lookup"><span data-stu-id="0d3a2-419">Archive</span></span>                          | <span data-ttu-id="0d3a2-420">0x20</span><span class="sxs-lookup"><span data-stu-id="0d3a2-420">(0x20)</span></span>  |
- <span data-ttu-id="0d3a2-421">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-421">Info Field 4: Not used.</span></span>

### <a name="directory-attributes-set"></a><span data-ttu-id="0d3a2-422">Dizin öznitelikleri kümesi</span><span class="sxs-lookup"><span data-stu-id="0d3a2-422">Directory Attributes Set</span></span> 

#### <a name="fx_directory_attributes_set"></a><span data-ttu-id="0d3a2-423">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="0d3a2-423">fx_directory_attributes_set</span></span> 

<span data-ttu-id="0d3a2-424">**Simge** ![ Öznitelik kümesi simgesi](./media/user-guide/fx-events/image16.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-424">**Icon** ![Attributes set icon](./media/user-guide/fx-events/image16.png)</span></span>

<span data-ttu-id="0d3a2-425">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-425">**Description**</span></span> 

<span data-ttu-id="0d3a2-426">Bu olay Dizin özniteliklerini ayarlama olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-426">This event represents a directory a directory attributes set event.</span></span>

<span data-ttu-id="0d3a2-427">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-427">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-428">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-428">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-429">Bilgi alanı 2: Dizin adı Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-429">Info Field 2: Pointer to directory name.</span></span>
- <span data-ttu-id="0d3a2-430">Bilgi alanı 3: öznitelikler bit eşlemesi:</span><span class="sxs-lookup"><span data-stu-id="0d3a2-430">Info Field 3: Attributes bit map:</span></span>

  |  <span data-ttu-id="0d3a2-431">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="0d3a2-431">Attribute</span></span>                        | <span data-ttu-id="0d3a2-432">Değer</span><span class="sxs-lookup"><span data-stu-id="0d3a2-432">Value</span></span>        |
  |---------------------------------- | --------|
  |  <span data-ttu-id="0d3a2-433">Salt Okunur</span><span class="sxs-lookup"><span data-stu-id="0d3a2-433">Read Only</span></span>                        | <span data-ttu-id="0d3a2-434">0x01</span><span class="sxs-lookup"><span data-stu-id="0d3a2-434">(0x01)</span></span>  |
  |  <span data-ttu-id="0d3a2-435">Gizli</span><span class="sxs-lookup"><span data-stu-id="0d3a2-435">Hidden</span></span>                           | <span data-ttu-id="0d3a2-436">0x02 şeklindedir</span><span class="sxs-lookup"><span data-stu-id="0d3a2-436">(0x02)</span></span>  |
  |  <span data-ttu-id="0d3a2-437">Sistem</span><span class="sxs-lookup"><span data-stu-id="0d3a2-437">System</span></span>                           | <span data-ttu-id="0d3a2-438">(0x04)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-438">(0x04)</span></span>  |
  |  <span data-ttu-id="0d3a2-439">Arşiv</span><span class="sxs-lookup"><span data-stu-id="0d3a2-439">Archive</span></span>                          | <span data-ttu-id="0d3a2-440">0x20</span><span class="sxs-lookup"><span data-stu-id="0d3a2-440">(0x20)</span></span>  |
- <span data-ttu-id="0d3a2-441">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-441">Info Field 4: Not used.</span></span>

### <a name="directory-create"></a><span data-ttu-id="0d3a2-442">Dizin oluşturma</span><span class="sxs-lookup"><span data-stu-id="0d3a2-442">Directory Create</span></span> 

#### <a name="fx_directory_create"></a><span data-ttu-id="0d3a2-443">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="0d3a2-443">fx_directory_create</span></span>

<span data-ttu-id="0d3a2-444">**Simge** ![ Dizin oluşturma simgesi](./media/user-guide/fx-events/image17.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-444">**Icon** ![Directory create icon](./media/user-guide/fx-events/image17.png)</span></span>

<span data-ttu-id="0d3a2-445">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-445">**Description**</span></span> 

<span data-ttu-id="0d3a2-446">Bu olay bir dizin oluşturma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-446">This event represents a directory create event.</span></span>

<span data-ttu-id="0d3a2-447">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-447">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-448">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-448">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-449">Bilgi alanı 2: Dizin adı Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-449">Info Field 2: Pointer to directory name.</span></span>
- <span data-ttu-id="0d3a2-450">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-450">Info Field 3: Not used.</span></span>
- <span data-ttu-id="0d3a2-451">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-451">Info Field 4: Not used.</span></span>

### <a name="directory-default-get"></a><span data-ttu-id="0d3a2-452">Dizin varsayılan Get</span><span class="sxs-lookup"><span data-stu-id="0d3a2-452">Directory Default Get</span></span> 

#### <a name="fx_directory_default_get"></a><span data-ttu-id="0d3a2-453">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="0d3a2-453">fx_directory_default_get</span></span> 

<span data-ttu-id="0d3a2-454">**Simge** ![ Dizin varsayılanı al simgesi](./media/user-guide/fx-events/image18.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-454">**Icon** ![Directory default get icon](./media/user-guide/fx-events/image18.png)</span></span>

<span data-ttu-id="0d3a2-455">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-455">**Description**</span></span> 

<span data-ttu-id="0d3a2-456">Bu olay, dizin varsayılan kümesi olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-456">This event represents a directory default set event.</span></span>

<span data-ttu-id="0d3a2-457">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-457">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-458">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-458">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-459">Bilgi alanı 2: dönüş yolu adı Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-459">Info Field 2: Pointer to return path name.</span></span>
- <span data-ttu-id="0d3a2-460">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-460">Info Field 3: Not used.</span></span>
- <span data-ttu-id="0d3a2-461">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-461">Info Field 4: Not used.</span></span>

### <a name="directory-default-set"></a><span data-ttu-id="0d3a2-462">Dizin varsayılan kümesi</span><span class="sxs-lookup"><span data-stu-id="0d3a2-462">Directory Default Set</span></span> 

#### <a name="fx_directory_default_set"></a><span data-ttu-id="0d3a2-463">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="0d3a2-463">fx_directory_default_set</span></span> 

<span data-ttu-id="0d3a2-464">**Simge** ![ Dizin varsayılan kümesi simgesi](./media/user-guide/fx-events/image19.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-464">**Icon** ![Directory default set icon](./media/user-guide/fx-events/image19.png)</span></span>

<span data-ttu-id="0d3a2-465">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-465">**Description**</span></span> 

<span data-ttu-id="0d3a2-466">Bu olay, dizin varsayılan kümesi olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-466">This event represents a directory default set event.</span></span>

<span data-ttu-id="0d3a2-467">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-467">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-468">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-468">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-469">Bilgi alanı 2: yeni varsayılan yol adı Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-469">Info Field 2: Pointer to new default path name.</span></span>
- <span data-ttu-id="0d3a2-470">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-470">Info Field 3: Not used.</span></span>
- <span data-ttu-id="0d3a2-471">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-471">Info Field 4: Not used.</span></span>

### <a name="directory-delete"></a><span data-ttu-id="0d3a2-472">Dizin silme</span><span class="sxs-lookup"><span data-stu-id="0d3a2-472">Directory Delete</span></span> 

#### <a name="fx_directory_delete"></a><span data-ttu-id="0d3a2-473">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="0d3a2-473">fx_directory_delete</span></span>

<span data-ttu-id="0d3a2-474">**Simge** ![ Dizin silme simgesi](./media/user-guide/fx-events/image20.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-474">**Icon** ![Directory delete icon](./media/user-guide/fx-events/image20.png)</span></span>

<span data-ttu-id="0d3a2-475">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-475">**Description**</span></span> 

<span data-ttu-id="0d3a2-476">Bu olay bir dizin silme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-476">This event represents a directory delete event.</span></span>

<span data-ttu-id="0d3a2-477">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-477">**Information Fields**</span></span>
- <span data-ttu-id="0d3a2-478">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-478">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-479">Bilgi alanı 2: Dizin adı Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-479">Info Field 2: Pointer to directory name.</span></span>
- <span data-ttu-id="0d3a2-480">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-480">Info Field 3: Not used.</span></span>
- <span data-ttu-id="0d3a2-481">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-481">Info Field 4: Not used.</span></span>

### <a name="directory-first-entry-find"></a><span data-ttu-id="0d3a2-482">Dizin Ilk giriş bulma</span><span class="sxs-lookup"><span data-stu-id="0d3a2-482">Directory First Entry Find</span></span> 

#### <a name="fx_directory_first_entry_find"></a><span data-ttu-id="0d3a2-483">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="0d3a2-483">fx_directory_first_entry_find</span></span>

<span data-ttu-id="0d3a2-484">**Simge** ![ Dizin ilk girişi bul simgesi](./media/user-guide/fx-events/image21.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-484">**Icon** ![Directory first entry find icon](./media/user-guide/fx-events/image21.png)</span></span>

<span data-ttu-id="0d3a2-485">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-485">**Description**</span></span> 

<span data-ttu-id="0d3a2-486">Bu olay bir dizin ilk girdi bul olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-486">This event represents a directory first entry find event.</span></span>

<span data-ttu-id="0d3a2-487">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-487">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-488">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-488">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-489">Bilgi alanı 2: Dizin adı Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-489">Info Field 2: Pointer to directory name.</span></span>
- <span data-ttu-id="0d3a2-490">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-490">Info Field 3: Not used.</span></span>
- <span data-ttu-id="0d3a2-491">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-491">Info Field 4: Not used.</span></span>

### <a name="directory-first-full-entry-find"></a><span data-ttu-id="0d3a2-492">Dizinin Ilk tam girişi bulma</span><span class="sxs-lookup"><span data-stu-id="0d3a2-492">Directory First Full Entry Find</span></span> 

#### <a name="fx_directory_first_full_entry_find"></a><span data-ttu-id="0d3a2-493">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="0d3a2-493">fx_directory_first_full_entry_find</span></span>

<span data-ttu-id="0d3a2-494">**Simge** ![ Dizinin ilk tam giriş bul simgesi](./media/user-guide/fx-events/image22.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-494">**Icon** ![Directory first full entry find icon](./media/user-guide/fx-events/image22.png)</span></span>

<span data-ttu-id="0d3a2-495">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-495">**Description**</span></span> 

<span data-ttu-id="0d3a2-496">Bu olay, bir dizinin ilk tam girdi bul olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-496">This event represents a directory first full entry find event.</span></span>

<span data-ttu-id="0d3a2-497">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-497">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-498">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-498">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-499">Bilgi alanı 2: Dizin adı Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-499">Info Field 2: Pointer to directory name.</span></span>
- <span data-ttu-id="0d3a2-500">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-500">Info Field 3: Not used.</span></span>
- <span data-ttu-id="0d3a2-501">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-501">Info Field 4: Not used.</span></span>

### <a name="directory-information-get"></a><span data-ttu-id="0d3a2-502">Dizin bilgileri al</span><span class="sxs-lookup"><span data-stu-id="0d3a2-502">Directory Information Get</span></span> 

#### <a name="fx_directory_information_get"></a><span data-ttu-id="0d3a2-503">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="0d3a2-503">fx_directory_information_get</span></span>

<span data-ttu-id="0d3a2-504">**Simge** ![ Dizin bilgileri al simgesi](./media/user-guide/fx-events/image23.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-504">**Icon** ![Directory information get icon](./media/user-guide/fx-events/image23.png)</span></span>

<span data-ttu-id="0d3a2-505">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-505">**Description**</span></span> 

<span data-ttu-id="0d3a2-506">Bu olay bir dizin bilgileri al olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-506">This event represents a directory information get event.</span></span>

<span data-ttu-id="0d3a2-507">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-507">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-508">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-508">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-509">Bilgi alanı 2: Dizin adı Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-509">Info Field 2: Pointer to directory name.</span></span>
- <span data-ttu-id="0d3a2-510">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-510">Info Field 3: Not used.</span></span>
- <span data-ttu-id="0d3a2-511">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-511">Info Field 4: Not used.</span></span>

### <a name="directory-local-path-clear"></a><span data-ttu-id="0d3a2-512">Dizin yerel yolu temizle</span><span class="sxs-lookup"><span data-stu-id="0d3a2-512">Directory Local Path Clear</span></span> 

#### <a name="fx_directory_local_path_clear"></a><span data-ttu-id="0d3a2-513">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="0d3a2-513">fx_directory_local_path_clear</span></span>

<span data-ttu-id="0d3a2-514">**Simge** ![ Dizin yerel yolu temizle simgesi](./media/user-guide/fx-events/image24.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-514">**Icon** ![Directory local path clear icon](./media/user-guide/fx-events/image24.png)</span></span>

<span data-ttu-id="0d3a2-515">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-515">**Description**</span></span> 

<span data-ttu-id="0d3a2-516">Bu olay, Dizin yerel yolu temizle olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-516">This event represents a directory local path clear event.</span></span>

<span data-ttu-id="0d3a2-517">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-517">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-518">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-518">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-519">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-519">Info Field 2: Not used.</span></span>
- <span data-ttu-id="0d3a2-520">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-520">Info Field 3: Not used.</span></span>
- <span data-ttu-id="0d3a2-521">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-521">Info Field 4: Not used.</span></span>

### <a name="directory-local-path-get"></a><span data-ttu-id="0d3a2-522">Dizin yerel yolu al</span><span class="sxs-lookup"><span data-stu-id="0d3a2-522">Directory Local Path Get</span></span> 

#### <a name="fx_directory_local_path_get"></a><span data-ttu-id="0d3a2-523">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="0d3a2-523">fx_directory_local_path_get</span></span>

<span data-ttu-id="0d3a2-524">**Simge** ![ Dizin yerel yolu al simgesi](./media/user-guide/fx-events/image25.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-524">**Icon** ![Directory local path get icon](./media/user-guide/fx-events/image25.png)</span></span>

<span data-ttu-id="0d3a2-525">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-525">**Description**</span></span> 

<span data-ttu-id="0d3a2-526">Bu olay bir dizin yerel yolu al olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-526">This event represents a directory local path get event.</span></span>

<span data-ttu-id="0d3a2-527">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-527">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-528">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-528">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-529">Bilgi alanı 2: dönüş yolu adı Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-529">Info Field 2: Pointer to return path name.</span></span>
- <span data-ttu-id="0d3a2-530">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-530">Info Field 3: Not used.</span></span>
- <span data-ttu-id="0d3a2-531">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-531">Info Field 4: Not used.</span></span>

### <a name="directory-local-path-restore"></a><span data-ttu-id="0d3a2-532">Dizin yerel yolunu geri yükleme</span><span class="sxs-lookup"><span data-stu-id="0d3a2-532">Directory Local Path Restore</span></span> 

#### <a name="fx_directory_local_path_restore"></a><span data-ttu-id="0d3a2-533">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="0d3a2-533">fx_directory_local_path_restore</span></span>

<span data-ttu-id="0d3a2-534">**Simge** ![ Dizin yerel yolu geri yükleme simgesi](./media/user-guide/fx-events/image26.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-534">**Icon** ![Directory local path restore icon](./media/user-guide/fx-events/image26.png)</span></span>

<span data-ttu-id="0d3a2-535">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-535">**Description**</span></span> 

<span data-ttu-id="0d3a2-536">Bu olay, Dizin yerel yolu geri yükleme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-536">This event represents a directory local path restore event.</span></span>

<span data-ttu-id="0d3a2-537">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-537">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-538">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-538">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-539">Bilgi alanı 2: yerel yol yapısına yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-539">Info Field 2: Pointer to local path structure.</span></span>
- <span data-ttu-id="0d3a2-540">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-540">Info Field 3: Not used.</span></span>
- <span data-ttu-id="0d3a2-541">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-541">Info Field 4: Not used.</span></span>

### <a name="directory-local-path-set"></a><span data-ttu-id="0d3a2-542">Dizin yerel yol kümesi</span><span class="sxs-lookup"><span data-stu-id="0d3a2-542">Directory Local Path Set</span></span> 

#### <a name="fx_directory_local_path_set"></a><span data-ttu-id="0d3a2-543">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="0d3a2-543">fx_directory_local_path_set</span></span>

<span data-ttu-id="0d3a2-544">**Simge** ![ Dizin yerel yolu kümesi simgesi](./media/user-guide/fx-events/image27.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-544">**Icon** ![Directory local path set icon](./media/user-guide/fx-events/image27.png)</span></span>

<span data-ttu-id="0d3a2-545">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-545">**Description**</span></span> 

<span data-ttu-id="0d3a2-546">Bu olay bir dizin yerel yol kümesi olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-546">This event represents a directory local path set event.</span></span>

<span data-ttu-id="0d3a2-547">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-547">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-548">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-548">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-549">Bilgi alanı 2: yerel yol yapısına yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-549">Info Field 2: Pointer to local path structure.</span></span>
- <span data-ttu-id="0d3a2-550">Bilgi alanı 3: yeni yol adı Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-550">Info Field 3: Pointer to new path name.</span></span>
- <span data-ttu-id="0d3a2-551">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-551">Info Field 4: Not used.</span></span>

### <a name="directory-long-name-get"></a><span data-ttu-id="0d3a2-552">Dizin uzun adı Al</span><span class="sxs-lookup"><span data-stu-id="0d3a2-552">Directory Long Name Get</span></span> 

#### <a name="fx_directory_long_name_get"></a><span data-ttu-id="0d3a2-553">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="0d3a2-553">fx_directory_long_name_get</span></span>

<span data-ttu-id="0d3a2-554">**Simge** ![ Dizin uzun adı Al simgesi](./media/user-guide/fx-events/image28.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-554">**Icon** ![Directory long name get icon](./media/user-guide/fx-events/image28.png)</span></span>

<span data-ttu-id="0d3a2-555">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-555">**Description**</span></span> 

<span data-ttu-id="0d3a2-556">Bu olay bir dizin uzun adı Al olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-556">This event represents a directory long name get event.</span></span>

<span data-ttu-id="0d3a2-557">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-557">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-558">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-558">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-559">Bilgi alanı 2: kısa dosya adı Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-559">Info Field 2: Pointer to short file name.</span></span>
- <span data-ttu-id="0d3a2-560">Bilgi alanı 3: uzun dosya adı Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-560">Info Field 3: Pointer to long file name.</span></span>
- <span data-ttu-id="0d3a2-561">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-561">Info Field 4: Not used.</span></span>

### <a name="directory-name-test"></a><span data-ttu-id="0d3a2-562">Dizin adı sınaması</span><span class="sxs-lookup"><span data-stu-id="0d3a2-562">Directory Name Test</span></span> 

#### <a name="fx_directory_name_test"></a><span data-ttu-id="0d3a2-563">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="0d3a2-563">fx_directory_name_test</span></span>

<span data-ttu-id="0d3a2-564">**Simge** ![ Dizin adı test simgesi](./media/user-guide/fx-events/image29.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-564">**Icon** ![Directory name test icon](./media/user-guide/fx-events/image29.png)</span></span>

<span data-ttu-id="0d3a2-565">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-565">**Description**</span></span> 

<span data-ttu-id="0d3a2-566">Bu olay bir dizin adı sınama olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-566">This event represents a directory name test event.</span></span>

<span data-ttu-id="0d3a2-567">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-567">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-568">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-568">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-569">Bilgi alanı 2: Dizin adı Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-569">Info Field 2: Pointer to directory name.</span></span>
- <span data-ttu-id="0d3a2-570">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-570">Info Field 3: Not used.</span></span>
- <span data-ttu-id="0d3a2-571">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-571">Info Field 4: Not used.</span></span>

### <a name="directory-next-entry-find"></a><span data-ttu-id="0d3a2-572">Dizin sonraki giriş bul</span><span class="sxs-lookup"><span data-stu-id="0d3a2-572">Directory Next Entry Find</span></span> 

#### <a name="fx_directory_next_entry_find"></a><span data-ttu-id="0d3a2-573">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="0d3a2-573">fx_directory_next_entry_find</span></span>

<span data-ttu-id="0d3a2-574">**Simge** ![ Dizin sonraki giriş bul simgesi](./media/user-guide/fx-events/image30.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-574">**Icon** ![Directory next entry find icon](./media/user-guide/fx-events/image30.png)</span></span>

<span data-ttu-id="0d3a2-575">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-575">**Description**</span></span> 

<span data-ttu-id="0d3a2-576">Bu olay bir dizin sonraki girişi bul olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-576">This event represents a directory next entry find event.</span></span>

<span data-ttu-id="0d3a2-577">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-577">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-578">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-578">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-579">Bilgi alanı 2: Dizin adı Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-579">Info Field 2: Pointer to directory name.</span></span>
- <span data-ttu-id="0d3a2-580">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-580">Info Field 3: Not used.</span></span>
- <span data-ttu-id="0d3a2-581">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-581">Info Field 4: Not used.</span></span>

### <a name="directory-next-full-entry-find"></a><span data-ttu-id="0d3a2-582">Dizin bir sonraki tam girdi bul</span><span class="sxs-lookup"><span data-stu-id="0d3a2-582">Directory Next Full Entry Find</span></span> 

#### <a name="fx_directory_next_full_entry_find"></a><span data-ttu-id="0d3a2-583">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="0d3a2-583">fx_directory_next_full_entry_find</span></span>

<span data-ttu-id="0d3a2-584">**Simge** ![ Dizin bir sonraki tam giriş bul simgesi](./media/user-guide/fx-events/image31.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-584">**Icon** ![Directory next full entry find icon](./media/user-guide/fx-events/image31.png)</span></span>

<span data-ttu-id="0d3a2-585">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-585">**Description**</span></span>

<span data-ttu-id="0d3a2-586">Bu olay, bir dizinin bir sonraki tam giriş bul olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-586">This event represents a directory next full entry find event.</span></span>

<span data-ttu-id="0d3a2-587">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-587">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-588">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-588">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-589">Bilgi alanı 2: Dizin adı Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-589">Info Field 2: Pointer to directory name.</span></span>
- <span data-ttu-id="0d3a2-590">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-590">Info Field 3: Not used.</span></span>
- <span data-ttu-id="0d3a2-591">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-591">Info Field 4: Not used.</span></span>

### <a name="directory-rename"></a><span data-ttu-id="0d3a2-592">Dizin yeniden adlandırma</span><span class="sxs-lookup"><span data-stu-id="0d3a2-592">Directory Rename</span></span> 

#### <a name="fx_directory_rename-event"></a><span data-ttu-id="0d3a2-593">fx_directory_rename olayı</span><span class="sxs-lookup"><span data-stu-id="0d3a2-593">fx_directory_rename event</span></span>

<span data-ttu-id="0d3a2-594">**Simge** ![ Dizin yeniden adlandırma simgesi](./media/user-guide/fx-events/image32.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-594">**Icon** ![Directory rename icon](./media/user-guide/fx-events/image32.png)</span></span>

<span data-ttu-id="0d3a2-595">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-595">**Description**</span></span>

<span data-ttu-id="0d3a2-596">Bu olay bir dizin yeniden adlandırma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-596">This event represents a directory rename event.</span></span>

<span data-ttu-id="0d3a2-597">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-597">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-598">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-598">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-599">Bilgi alanı 2: eski dizin adı Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-599">Info Field 2: Pointer to old directory name.</span></span>
- <span data-ttu-id="0d3a2-600">Bilgi alanı 3: yeni dizin adı Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-600">Info Field 3: Pointer to new directory name.</span></span>
- <span data-ttu-id="0d3a2-601">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-601">Info Field 4: Not used.</span></span>

### <a name="directory-short-name-get"></a><span data-ttu-id="0d3a2-602">Dizin kısa adı Al</span><span class="sxs-lookup"><span data-stu-id="0d3a2-602">Directory Short Name Get</span></span> 

#### <a name="fx_directory_short_name_get"></a><span data-ttu-id="0d3a2-603">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="0d3a2-603">fx_directory_short_name_get</span></span>

<span data-ttu-id="0d3a2-604">**Simge** ![ Dizin kısa adı Al simgesi](./media/user-guide/fx-events/image33.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-604">**Icon** ![Directory short name get icon](./media/user-guide/fx-events/image33.png)</span></span>

<span data-ttu-id="0d3a2-605">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-605">**Description**</span></span>

<span data-ttu-id="0d3a2-606">Bu olay bir dizin kısa adı Get olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-606">This event represents a directory short name get event.</span></span>

<span data-ttu-id="0d3a2-607">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-607">**Information Fields**</span></span> 

- <span data-ttu-id="0d3a2-608">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-608">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-609">Bilgi alanı 2: uzun dosya adı Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-609">Info Field 2: Pointer to long file name.</span></span>
- <span data-ttu-id="0d3a2-610">Bilgi alanı 3: kısa dosya adı Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-610">Info Field 3: Pointer to short file name.</span></span>
- <span data-ttu-id="0d3a2-611">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-611">Info Field 4: Not used.</span></span>

### <a name="file-allocate"></a><span data-ttu-id="0d3a2-612">Dosya ayırma</span><span class="sxs-lookup"><span data-stu-id="0d3a2-612">File Allocate</span></span> 

#### <a name="fx_file_allocate"></a><span data-ttu-id="0d3a2-613">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="0d3a2-613">fx_file_allocate</span></span>

<span data-ttu-id="0d3a2-614">**Simge** ![ Dosya ayırma simgesi](./media/user-guide/fx-events/image34.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-614">**Icon** ![File allocate icon](./media/user-guide/fx-events/image34.png)</span></span>

<span data-ttu-id="0d3a2-615">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-615">**Description**</span></span>

<span data-ttu-id="0d3a2-616">Bu olay bir dosya ayırma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-616">This event represents a file allocate event.</span></span>

<span data-ttu-id="0d3a2-617">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-617">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-618">Bilgi alanı 1: dosya Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-618">Info Field 1: Pointer to the file.</span></span>
- <span data-ttu-id="0d3a2-619">Bilgi alanı 2: Istenen boyut.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-619">Info Field 2: Requested size.</span></span>
- <span data-ttu-id="0d3a2-620">Bilgi alanı 3: geçerli boyut.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-620">Info Field 3: Current size.</span></span>
- <span data-ttu-id="0d3a2-621">Bilgi alanı 4: yeni boyut.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-621">Info Field 4: New size.</span></span>

### <a name="file-attributes-read"></a><span data-ttu-id="0d3a2-622">Okunan dosya öznitelikleri</span><span class="sxs-lookup"><span data-stu-id="0d3a2-622">File Attributes Read</span></span> 

#### <a name="fx_file_attributes_read"></a><span data-ttu-id="0d3a2-623">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="0d3a2-623">fx_file_attributes_read</span></span>

<span data-ttu-id="0d3a2-624">**Simge** ![ Dosya öznitelikleri okuma simgesi](./media/user-guide/fx-events/image35.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-624">**Icon** ![File attributes read icon](./media/user-guide/fx-events/image35.png)</span></span>

<span data-ttu-id="0d3a2-625">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-625">**Description**</span></span>

<span data-ttu-id="0d3a2-626">Bu olay bir dosya öznitelikleri okuma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-626">This event represents a file attributes read event.</span></span>

<span data-ttu-id="0d3a2-627">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-627">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-628">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-628">Info Field 1: Pointer to the media.</span></span> 
- <span data-ttu-id="0d3a2-629">Bilgi alanı 2: öznitelikler bit eşlemesi:</span><span class="sxs-lookup"><span data-stu-id="0d3a2-629">Info Field 2: Attributes bit map:</span></span>

  |  <span data-ttu-id="0d3a2-630">Attriancak</span><span class="sxs-lookup"><span data-stu-id="0d3a2-630">Attribut</span></span>                         | <span data-ttu-id="0d3a2-631">Değer</span><span class="sxs-lookup"><span data-stu-id="0d3a2-631">Value</span></span>        |
  |---------------------------------- | --------|
  |  <span data-ttu-id="0d3a2-632">Salt Okunur</span><span class="sxs-lookup"><span data-stu-id="0d3a2-632">Read Only</span></span>                        | <span data-ttu-id="0d3a2-633">0x01</span><span class="sxs-lookup"><span data-stu-id="0d3a2-633">(0x01)</span></span>  |
  |  <span data-ttu-id="0d3a2-634">Gizli</span><span class="sxs-lookup"><span data-stu-id="0d3a2-634">Hidden</span></span>                           | <span data-ttu-id="0d3a2-635">0x02 şeklindedir</span><span class="sxs-lookup"><span data-stu-id="0d3a2-635">(0x02)</span></span>  |
  |  <span data-ttu-id="0d3a2-636">Sistem</span><span class="sxs-lookup"><span data-stu-id="0d3a2-636">System</span></span>                           | <span data-ttu-id="0d3a2-637">(0x04)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-637">(0x04)</span></span>  |
  |  <span data-ttu-id="0d3a2-638">Birim</span><span class="sxs-lookup"><span data-stu-id="0d3a2-638">Volume</span></span>                           | <span data-ttu-id="0d3a2-639">(0x08)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-639">(0x08)</span></span>  |
  |  <span data-ttu-id="0d3a2-640">Dizin</span><span class="sxs-lookup"><span data-stu-id="0d3a2-640">Directory</span></span>                        | <span data-ttu-id="0d3a2-641">0x10</span><span class="sxs-lookup"><span data-stu-id="0d3a2-641">(0x10)</span></span>  |
  |  <span data-ttu-id="0d3a2-642">Arşiv</span><span class="sxs-lookup"><span data-stu-id="0d3a2-642">Archive</span></span>                          | <span data-ttu-id="0d3a2-643">0x20</span><span class="sxs-lookup"><span data-stu-id="0d3a2-643">(0x20)</span></span>  |
- <span data-ttu-id="0d3a2-644">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-644">Info Field 3: Not used.</span></span>
- <span data-ttu-id="0d3a2-645">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-645">Info Field 4: Not used.</span></span>

### <a name="file-attributes-set"></a><span data-ttu-id="0d3a2-646">Dosya öznitelikleri kümesi</span><span class="sxs-lookup"><span data-stu-id="0d3a2-646">File Attributes Set</span></span> 

#### <a name="fx_file_attributes_set"></a><span data-ttu-id="0d3a2-647">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="0d3a2-647">fx_file_attributes_set</span></span>

<span data-ttu-id="0d3a2-648">**Simge** ![ Dosya öznitelikleri kümesi simgesi](./media/user-guide/fx-events/image36.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-648">**Icon** ![File attributes set icon](./media/user-guide/fx-events/image36.png)</span></span>

<span data-ttu-id="0d3a2-649">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-649">**Description**</span></span> 

<span data-ttu-id="0d3a2-650">Bu olay bir dosya öznitelikleri ayarlama olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-650">This event represents a file attributes set event.</span></span>

<span data-ttu-id="0d3a2-651">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-651">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-652">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-652">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-653">Bilgi alanı 2: dosya adı Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-653">Info Field 2: Pointer to file name.</span></span> 
- <span data-ttu-id="0d3a2-654">Bilgi alanı 3: öznitelikler bit eşlemesi:</span><span class="sxs-lookup"><span data-stu-id="0d3a2-654">Info Field 3: Attributes bit map:</span></span>

  | <span data-ttu-id="0d3a2-655">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="0d3a2-655">Attribute</span></span>                         | <span data-ttu-id="0d3a2-656">Değer</span><span class="sxs-lookup"><span data-stu-id="0d3a2-656">Value</span></span>        |
  |---------------------------------- | --------|
  |  <span data-ttu-id="0d3a2-657">Salt Okunur</span><span class="sxs-lookup"><span data-stu-id="0d3a2-657">Read Only</span></span>                        | <span data-ttu-id="0d3a2-658">0x01</span><span class="sxs-lookup"><span data-stu-id="0d3a2-658">(0x01)</span></span>  |
  |  <span data-ttu-id="0d3a2-659">Gizli</span><span class="sxs-lookup"><span data-stu-id="0d3a2-659">Hidden</span></span>                           | <span data-ttu-id="0d3a2-660">0x02 şeklindedir</span><span class="sxs-lookup"><span data-stu-id="0d3a2-660">(0x02)</span></span>  |
  |  <span data-ttu-id="0d3a2-661">Sistem</span><span class="sxs-lookup"><span data-stu-id="0d3a2-661">System</span></span>                           | <span data-ttu-id="0d3a2-662">(0x04)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-662">(0x04)</span></span>  |
  |  <span data-ttu-id="0d3a2-663">Arşiv</span><span class="sxs-lookup"><span data-stu-id="0d3a2-663">Archive</span></span>                          | <span data-ttu-id="0d3a2-664">0x20</span><span class="sxs-lookup"><span data-stu-id="0d3a2-664">(0x20)</span></span>  |
- <span data-ttu-id="0d3a2-665">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-665">Info Field 4: Not used.</span></span>

### <a name="file-best-effort-allocate"></a><span data-ttu-id="0d3a2-666">Dosya En Iyi çaba ayırma</span><span class="sxs-lookup"><span data-stu-id="0d3a2-666">File Best Effort Allocate</span></span> 

#### <a name="fx_file_best_effort_allocate"></a><span data-ttu-id="0d3a2-667">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="0d3a2-667">fx_file_best_effort_allocate</span></span>

<span data-ttu-id="0d3a2-668">**Simge** ![ Dosya en iyi çaba ayırma simgesi](./media/user-guide/fx-events/image37.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-668">**Icon** ![File best effort allocate icon](./media/user-guide/fx-events/image37.png)</span></span>

<span data-ttu-id="0d3a2-669">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-669">**Description**</span></span> 

<span data-ttu-id="0d3a2-670">Bu olay bir dosya en iyi çaba ayırma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-670">This event represents a file best effort allocate event.</span></span>

<span data-ttu-id="0d3a2-671">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-671">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-672">Bilgi alanı 1: dosya Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-672">Info Field 1: Pointer to the file.</span></span>
- <span data-ttu-id="0d3a2-673">Bilgi alanı 2: Istenen boyut.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-673">Info Field 2: Requested size.</span></span>
- <span data-ttu-id="0d3a2-674">Bilgi alanı 3: ayrılan gerçek boyut.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-674">Info Field 3: Actual size allocated.</span></span>
- <span data-ttu-id="0d3a2-675">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-675">Info Field 4: Not used.</span></span>

### <a name="file-close"></a><span data-ttu-id="0d3a2-676">Dosya Kapat</span><span class="sxs-lookup"><span data-stu-id="0d3a2-676">File Close</span></span> 

#### <a name="fx_file_close"></a><span data-ttu-id="0d3a2-677">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="0d3a2-677">fx_file_close</span></span>

<span data-ttu-id="0d3a2-678">**Simge** ![ Dosya Kapat simgesi](./media/user-guide/fx-events/image38.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-678">**Icon** ![File close icon](./media/user-guide/fx-events/image38.png)</span></span>

<span data-ttu-id="0d3a2-679">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-679">**Description**</span></span> 

<span data-ttu-id="0d3a2-680">Bu olay bir dosya kapatma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-680">This event represents a file close event.</span></span>

<span data-ttu-id="0d3a2-681">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-681">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-682">Bilgi alanı 1: dosya Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-682">Info Field 1: Pointer to the file.</span></span>
- <span data-ttu-id="0d3a2-683">Bilgi alanı 2: dosya boyutu.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-683">Info Field 2: File size.</span></span>
- <span data-ttu-id="0d3a2-684">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-684">Info Field 3: Not used.</span></span>
- <span data-ttu-id="0d3a2-685">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-685">Info Field 4: Not used.</span></span>

### <a name="file-create"></a><span data-ttu-id="0d3a2-686">Dosya oluşturma</span><span class="sxs-lookup"><span data-stu-id="0d3a2-686">File Create</span></span>

#### <a name="fx_file_create"></a><span data-ttu-id="0d3a2-687">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="0d3a2-687">fx_file_create</span></span>

<span data-ttu-id="0d3a2-688">**Simge** ![ Dosya oluşturma simgesi](./media/user-guide/fx-events/image39.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-688">**Icon** ![File create icon](./media/user-guide/fx-events/image39.png)</span></span>

<span data-ttu-id="0d3a2-689">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-689">**Description**</span></span>

<span data-ttu-id="0d3a2-690">Bu olay bir dosya oluşturma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-690">This event represents a file create event.</span></span>

<span data-ttu-id="0d3a2-691">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-691">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-692">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-692">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-693">Bilgi alanı 2: dosya adı Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-693">Info Field 2: Pointer to file name.</span></span>
- <span data-ttu-id="0d3a2-694">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-694">Info Field 3: Not used.</span></span>
- <span data-ttu-id="0d3a2-695">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-695">Info Field 4: Not used.</span></span>

### <a name="file-date-time-set"></a><span data-ttu-id="0d3a2-696">Dosya tarih saat kümesi</span><span class="sxs-lookup"><span data-stu-id="0d3a2-696">File Date Time Set</span></span> 

#### <a name="fx_file_date_time_set"></a><span data-ttu-id="0d3a2-697">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="0d3a2-697">fx_file_date_time_set</span></span>

<span data-ttu-id="0d3a2-698">**Simge** ![ Dosya tarih saat kümesi simgesi](./media/user-guide/fx-events/image40.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-698">**Icon** ![File date time set icon](./media/user-guide/fx-events/image40.png)</span></span>

<span data-ttu-id="0d3a2-699">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-699">**Description**</span></span>

<span data-ttu-id="0d3a2-700">Bu olay bir dosya tarih/saat kümesi olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-700">This event represents a file date/time set event.</span></span>

<span data-ttu-id="0d3a2-701">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-701">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-702">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-702">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-703">Bilgi alanı 2: dosya adı Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-703">Info Field 2: Pointer to file name.</span></span>
- <span data-ttu-id="0d3a2-704">Bilgi alanı 3: yıl.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-704">Info Field 3: Year.</span></span>
- <span data-ttu-id="0d3a2-705">Bilgi alanı 4: ay.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-705">Info Field 4: Month.</span></span>

### <a name="file-delete"></a><span data-ttu-id="0d3a2-706">Dosya silme</span><span class="sxs-lookup"><span data-stu-id="0d3a2-706">File Delete</span></span> 

#### <a name="fx_file_delete"></a><span data-ttu-id="0d3a2-707">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="0d3a2-707">fx_file_delete</span></span>

<span data-ttu-id="0d3a2-708">**Simge** ![ Dosya silme simgesi](./media/user-guide/fx-events/image41.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-708">**Icon** ![File delete icon](./media/user-guide/fx-events/image41.png)</span></span>

<span data-ttu-id="0d3a2-709">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-709">**Description**</span></span>

<span data-ttu-id="0d3a2-710">Bu olay bir dosya silme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-710">This event represents a file delete event.</span></span>

<span data-ttu-id="0d3a2-711">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-711">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-712">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-712">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-713">Bilgi alanı 2: dosya adı Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-713">Info Field 2: Pointer to file name.</span></span>
- <span data-ttu-id="0d3a2-714">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-714">Info Field 3: Not used.</span></span>
- <span data-ttu-id="0d3a2-715">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-715">Info Field 4: Not used.</span></span>

### <a name="file-open"></a><span data-ttu-id="0d3a2-716">Dosya açık</span><span class="sxs-lookup"><span data-stu-id="0d3a2-716">File Open</span></span> 

#### <a name="fx_file_open"></a><span data-ttu-id="0d3a2-717">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="0d3a2-717">fx_file_open</span></span>

<span data-ttu-id="0d3a2-718">**Simge** ![ Dosya aç simgesi](./media/user-guide/fx-events/image42.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-718">**Icon** ![File open icon](./media/user-guide/fx-events/image42.png)</span></span>

<span data-ttu-id="0d3a2-719">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-719">**Description**</span></span>

<span data-ttu-id="0d3a2-720">Bu olay bir dosya açma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-720">This event represents a file open event.</span></span>

<span data-ttu-id="0d3a2-721">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-721">**Information Fields**</span></span> 

- <span data-ttu-id="0d3a2-722">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-722">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-723">Bilgi alanı 2: dosya denetim bloğu Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-723">Info Field 2: Pointer to the file control block.</span></span>
- <span data-ttu-id="0d3a2-724">Bilgi alanı 3: dosya adı Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-724">Info Field 3: Pointer to file name.</span></span>
- <span data-ttu-id="0d3a2-725">Bilgi alanı 4: açık tür:</span><span class="sxs-lookup"><span data-stu-id="0d3a2-725">Info Field 4: Open type:</span></span>

  |  <span data-ttu-id="0d3a2-726">Açık tür</span><span class="sxs-lookup"><span data-stu-id="0d3a2-726">Open Type</span></span>                        | <span data-ttu-id="0d3a2-727">Değer</span><span class="sxs-lookup"><span data-stu-id="0d3a2-727">Value</span></span>        |
  |---------------------------------- | --------|
  |  <span data-ttu-id="0d3a2-728">Okuma için aç</span><span class="sxs-lookup"><span data-stu-id="0d3a2-728">Open for Read</span></span>                    | <span data-ttu-id="0d3a2-729">-</span><span class="sxs-lookup"><span data-stu-id="0d3a2-729">(0x00)</span></span>  |
  |  <span data-ttu-id="0d3a2-730">Yazma için aç</span><span class="sxs-lookup"><span data-stu-id="0d3a2-730">Open for Write</span></span>                   | <span data-ttu-id="0d3a2-731">0x01</span><span class="sxs-lookup"><span data-stu-id="0d3a2-731">(0x01)</span></span>  |
  |  <span data-ttu-id="0d3a2-732">Okuma için hızlı aç</span><span class="sxs-lookup"><span data-stu-id="0d3a2-732">Fast Open for Read</span></span>               | <span data-ttu-id="0d3a2-733">0x02 şeklindedir</span><span class="sxs-lookup"><span data-stu-id="0d3a2-733">(0x02)</span></span>  |

### <a name="file-read"></a><span data-ttu-id="0d3a2-734">Dosya okuma</span><span class="sxs-lookup"><span data-stu-id="0d3a2-734">File Read</span></span> 

#### <a name="fx_file_read"></a><span data-ttu-id="0d3a2-735">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="0d3a2-735">fx_file_read</span></span>

<span data-ttu-id="0d3a2-736">**Simge** ![ Dosya okuma simgesi](./media/user-guide/fx-events/image43.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-736">**Icon** ![File read icon](./media/user-guide/fx-events/image43.png)</span></span>

<span data-ttu-id="0d3a2-737">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-737">**Description**</span></span>

<span data-ttu-id="0d3a2-738">Bu olay bir dosya okuma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-738">This event represents a file read event.</span></span>

<span data-ttu-id="0d3a2-739">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-739">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-740">Bilgi alanı 1: dosya Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-740">Info Field 1: Pointer to the file.</span></span>
- <span data-ttu-id="0d3a2-741">Bilgi alanı 2: arabellek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-741">Info Field 2: Buffer pointer.</span></span>
- <span data-ttu-id="0d3a2-742">Bilgi alanı 3: Istek boyutu.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-742">Info Field 3: Request size.</span></span>
- <span data-ttu-id="0d3a2-743">Bilgi alanı 4: gerçek boyut okuma.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-743">Info Field 4: Actual size read.</span></span>

### <a name="file-relative-seek"></a><span data-ttu-id="0d3a2-744">Dosya göreli arama</span><span class="sxs-lookup"><span data-stu-id="0d3a2-744">File Relative Seek</span></span> 

#### <a name="fx_file_relative_seek"></a><span data-ttu-id="0d3a2-745">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="0d3a2-745">fx_file_relative_seek</span></span>

<span data-ttu-id="0d3a2-746">**Simge** ![ Dosya göreli arama simgesi](./media/user-guide/fx-events/image44.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-746">**Icon** ![File relative seek icon](./media/user-guide/fx-events/image44.png)</span></span>

<span data-ttu-id="0d3a2-747">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-747">**Description**</span></span>

<span data-ttu-id="0d3a2-748">Bu olay bir dosya göreli arama olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-748">This event represents a file relative seek event.</span></span>

<span data-ttu-id="0d3a2-749">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-749">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-750">Bilgi alanı 1: dosya Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-750">Info Field 1: Pointer to the file.</span></span>
- <span data-ttu-id="0d3a2-751">Bilgi alanı 2: bayt kayması.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-751">Info Field 2: Byte offset.</span></span>
- <span data-ttu-id="0d3a2-752">Bilgi alanı 3: şuradan ara:</span><span class="sxs-lookup"><span data-stu-id="0d3a2-752">Info Field 3: Seek from:</span></span>

  | <span data-ttu-id="0d3a2-753">Olay</span><span class="sxs-lookup"><span data-stu-id="0d3a2-753">Event</span></span>                             | <span data-ttu-id="0d3a2-754">Değer</span><span class="sxs-lookup"><span data-stu-id="0d3a2-754">Value</span></span>        |
  |---------------------------------- | --------|
  |  <span data-ttu-id="0d3a2-755">Başlangıçtan itibaren</span><span class="sxs-lookup"><span data-stu-id="0d3a2-755">From Beginning</span></span>                   | <span data-ttu-id="0d3a2-756">-</span><span class="sxs-lookup"><span data-stu-id="0d3a2-756">(0x00)</span></span>  |
  |  <span data-ttu-id="0d3a2-757">Uçtan uca</span><span class="sxs-lookup"><span data-stu-id="0d3a2-757">From End</span></span>                         | <span data-ttu-id="0d3a2-758">0x01</span><span class="sxs-lookup"><span data-stu-id="0d3a2-758">(0x01)</span></span>  | 
  |  <span data-ttu-id="0d3a2-759">İleri</span><span class="sxs-lookup"><span data-stu-id="0d3a2-759">Forward</span></span>                          | <span data-ttu-id="0d3a2-760">0x02 şeklindedir</span><span class="sxs-lookup"><span data-stu-id="0d3a2-760">(0x02)</span></span>  |
  |  <span data-ttu-id="0d3a2-761">Geri</span><span class="sxs-lookup"><span data-stu-id="0d3a2-761">Backward</span></span>                         | <span data-ttu-id="0d3a2-762">(0x03)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-762">(0x03)</span></span>  |
- <span data-ttu-id="0d3a2-763">Bilgi alanı 4: önceki fark.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-763">Info Field 4: Previous offset.</span></span>

### <a name="file-rename"></a><span data-ttu-id="0d3a2-764">Dosya yeniden adlandırma</span><span class="sxs-lookup"><span data-stu-id="0d3a2-764">File Rename</span></span> 

#### <a name="fx_file_rename"></a><span data-ttu-id="0d3a2-765">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="0d3a2-765">fx_file_rename</span></span>

<span data-ttu-id="0d3a2-766">**Simge** ![ Dosya yeniden adlandırma simgesi](./media/user-guide/fx-events/image45.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-766">**Icon** ![File rename icon](./media/user-guide/fx-events/image45.png)</span></span>

<span data-ttu-id="0d3a2-767">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-767">**Description**</span></span>

<span data-ttu-id="0d3a2-768">Bu olay bir dosya yeniden adlandırma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-768">This event represents a file rename event.</span></span>

<span data-ttu-id="0d3a2-769">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-769">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-770">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-770">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-771">Bilgi alanı 2: eski dosya adı Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-771">Info Field 2: Pointer to old file name.</span></span>
- <span data-ttu-id="0d3a2-772">Bilgi alanı 3: yeni dosya adı Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-772">Info Field 3: Pointer to new file name.</span></span>
- <span data-ttu-id="0d3a2-773">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-773">Info Field 4: Not used.</span></span>

### <a name="file-seek"></a><span data-ttu-id="0d3a2-774">Dosya ara</span><span class="sxs-lookup"><span data-stu-id="0d3a2-774">File Seek</span></span> 

#### <a name="fx_file_seek"></a><span data-ttu-id="0d3a2-775">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="0d3a2-775">fx_file_seek</span></span>

<span data-ttu-id="0d3a2-776">**Simge** ![ Dosya arama simgesi](./media/user-guide/fx-events/image46.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-776">**Icon** ![File seek icon](./media/user-guide/fx-events/image46.png)</span></span>

<span data-ttu-id="0d3a2-777">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-777">**Description**</span></span>

<span data-ttu-id="0d3a2-778">Bu olay bir dosya arama olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-778">This event represents a file seek event.</span></span>

<span data-ttu-id="0d3a2-779">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-779">**Information Fields**</span></span> 

- <span data-ttu-id="0d3a2-780">Bilgi alanı 1: dosya Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-780">Info Field 1: Pointer to the file.</span></span>
- <span data-ttu-id="0d3a2-781">Bilgi alanı 2: bayt kayması.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-781">Info Field 2: Byte offset.</span></span>
- <span data-ttu-id="0d3a2-782">Bilgi alanı 3: önceki fark.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-782">Info Field 3: Previous offset.</span></span>
- <span data-ttu-id="0d3a2-783">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-783">Info Field 4: Not used.</span></span>

### <a name="file-truncate"></a><span data-ttu-id="0d3a2-784">Dosya kesme</span><span class="sxs-lookup"><span data-stu-id="0d3a2-784">File Truncate</span></span> 

#### <a name="fx_file_truncate"></a><span data-ttu-id="0d3a2-785">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="0d3a2-785">fx_file_truncate</span></span>

<span data-ttu-id="0d3a2-786">**Simge** ![ Dosya kesme simgesi](./media/user-guide/fx-events/image47.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-786">**Icon** ![File truncate icon](./media/user-guide/fx-events/image47.png)</span></span>

<span data-ttu-id="0d3a2-787">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-787">**Description**</span></span>

<span data-ttu-id="0d3a2-788">Bu olay bir dosya Truncate olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-788">This event represents a file truncate event.</span></span>

<span data-ttu-id="0d3a2-789">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-789">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-790">Bilgi alanı 1: dosya Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-790">Info Field 1: Pointer to the file.</span></span>
- <span data-ttu-id="0d3a2-791">Bilgi alanı 2: Istenen boyut.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-791">Info Field 2: Requested size.</span></span>
- <span data-ttu-id="0d3a2-792">Bilgi alanı 3: önceki boyut.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-792">Info Field 3: Previous size.</span></span>
- <span data-ttu-id="0d3a2-793">Bilgi alanı 4: yeni boyut.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-793">Info Field 4: New size.</span></span>

### <a name="file-truncate-release"></a><span data-ttu-id="0d3a2-794">Dosya kesme sürümü</span><span class="sxs-lookup"><span data-stu-id="0d3a2-794">File Truncate Release</span></span> 

#### <a name="fx_file_truncate_release"></a><span data-ttu-id="0d3a2-795">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="0d3a2-795">fx_file_truncate_release</span></span> 

<span data-ttu-id="0d3a2-796">**Simge** ![ Dosya kesme sürümü simgesi](./media/user-guide/fx-events/image48.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-796">**Icon** ![File truncate release icon](./media/user-guide/fx-events/image48.png)</span></span>

<span data-ttu-id="0d3a2-797">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-797">**Description**</span></span>

<span data-ttu-id="0d3a2-798">Bu olay bir dosya Truncate Release olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-798">This event represents a file truncate release event.</span></span>

<span data-ttu-id="0d3a2-799">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-799">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-800">Bilgi alanı 1: dosya Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-800">Info Field 1: Pointer to the file.</span></span>
- <span data-ttu-id="0d3a2-801">Bilgi alanı 2: Istenen boyut.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-801">Info Field 2: Requested size.</span></span>
- <span data-ttu-id="0d3a2-802">Bilgi alanı 3: önceki boyut.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-802">Info Field 3: Previous size.</span></span>
- <span data-ttu-id="0d3a2-803">Bilgi alanı 4: yeni boyut.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-803">Info Field 4: New size.</span></span>

### <a name="file-write"></a><span data-ttu-id="0d3a2-804">Dosya yazma</span><span class="sxs-lookup"><span data-stu-id="0d3a2-804">File Write</span></span> 

#### <a name="fx_file_write"></a><span data-ttu-id="0d3a2-805">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="0d3a2-805">fx_file_write</span></span> 

<span data-ttu-id="0d3a2-806">**Simge** ![ Dosya yazma simgesi](./media/user-guide/fx-events/image49.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-806">**Icon** ![File write icon](./media/user-guide/fx-events/image49.png)</span></span>

<span data-ttu-id="0d3a2-807">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-807">**Description**</span></span>

<span data-ttu-id="0d3a2-808">Bu olay bir dosya yazma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-808">This event represents a file write event.</span></span>

<span data-ttu-id="0d3a2-809">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-809">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-810">Bilgi alanı 1: dosya Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-810">Info Field 1: Pointer to the file.</span></span>
- <span data-ttu-id="0d3a2-811">Bilgi alanı 2: arabellek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-811">Info Field 2: Buffer pointer.</span></span>
- <span data-ttu-id="0d3a2-812">Bilgi alanı 3: Istek boyutu.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-812">Info Field 3: Request size.</span></span>
- <span data-ttu-id="0d3a2-813">Bilgi alanı 4: gerçek boyut yazıldı.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-813">Info Field 4: Actual size written.</span></span>

### <a name="media-abort"></a><span data-ttu-id="0d3a2-814">Medya Iptali</span><span class="sxs-lookup"><span data-stu-id="0d3a2-814">Media Abort</span></span> 

#### <a name="fx_media_abort"></a><span data-ttu-id="0d3a2-815">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="0d3a2-815">fx_media_abort</span></span> 

<span data-ttu-id="0d3a2-816">**Simge** ![ Medya iptali simgesi](./media/user-guide/fx-events/image50.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-816">**Icon** ![Media abort icon](./media/user-guide/fx-events/image50.png)</span></span>

<span data-ttu-id="0d3a2-817">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-817">**Description**</span></span>

<span data-ttu-id="0d3a2-818">Bu olay bir medya iptali olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-818">This event represents a media abort event.</span></span>

<span data-ttu-id="0d3a2-819">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-819">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-820">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-820">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-821">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-821">Info Field 2: Not used.</span></span>
- <span data-ttu-id="0d3a2-822">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-822">Info Field 3: Not used.</span></span>
- <span data-ttu-id="0d3a2-823">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-823">Info Field 4: Not used.</span></span>

### <a name="media-cache-invalidate"></a><span data-ttu-id="0d3a2-824">Medya önbelleği geçersiz kıl</span><span class="sxs-lookup"><span data-stu-id="0d3a2-824">Media Cache Invalidate</span></span>

#### <a name="fx_media_cache_invalidate"></a><span data-ttu-id="0d3a2-825">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="0d3a2-825">fx_media_cache_invalidate</span></span>

<span data-ttu-id="0d3a2-826">**Simge** ![ Medya önbelleği geçersiz kıl simgesi](./media/user-guide/fx-events/image51.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-826">**Icon** ![Media cache invalidate icon](./media/user-guide/fx-events/image51.png)</span></span>

<span data-ttu-id="0d3a2-827">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-827">**Description**</span></span>

<span data-ttu-id="0d3a2-828">Bu olay, bir medya önbelleği geçersiz kılan olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-828">This event represents a media cache invalidate event.</span></span>

<span data-ttu-id="0d3a2-829">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-829">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-830">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-830">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-831">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-831">Info Field 2: Not used.</span></span>
- <span data-ttu-id="0d3a2-832">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-832">Info Field 3: Not used.</span></span>
- <span data-ttu-id="0d3a2-833">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-833">Info Field 4: Not used.</span></span>

### <a name="media-check"></a><span data-ttu-id="0d3a2-834">Medya denetimi</span><span class="sxs-lookup"><span data-stu-id="0d3a2-834">Media Check</span></span> 

#### <a name="fx_media_check"></a><span data-ttu-id="0d3a2-835">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="0d3a2-835">fx_media_check</span></span>

<span data-ttu-id="0d3a2-836">**Simge** ![ Medya onay simgesi](./media/user-guide/fx-events/image52.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-836">**Icon** ![Media check icon](./media/user-guide/fx-events/image52.png)</span></span>

<span data-ttu-id="0d3a2-837">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-837">**Description**</span></span>

<span data-ttu-id="0d3a2-838">Bu olay bir medya denetimi olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-838">This event represents a media check event.</span></span>

<span data-ttu-id="0d3a2-839">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-839">**Information Fields**</span></span> 

- <span data-ttu-id="0d3a2-840">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-840">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-841">Bilgi alanı 2: karalama bellek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-841">Info Field 2: Scratch memory pointer.</span></span>
- <span data-ttu-id="0d3a2-842">Bilgi alanı 3: boş bellek boyutu.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-842">Info Field 3: Scratch memory size.</span></span>
- <span data-ttu-id="0d3a2-843">Bilgi alanı 4: hatalar bit eşlem:</span><span class="sxs-lookup"><span data-stu-id="0d3a2-843">Info Field 4: Errors bit map:</span></span>

  | <span data-ttu-id="0d3a2-844">Hata türü</span><span class="sxs-lookup"><span data-stu-id="0d3a2-844">Error type</span></span>                        | <span data-ttu-id="0d3a2-845">Değer</span><span class="sxs-lookup"><span data-stu-id="0d3a2-845">Value</span></span>        |
  |---------------------------------- | --------|
  |  <span data-ttu-id="0d3a2-846">FAT zinciri hatası</span><span class="sxs-lookup"><span data-stu-id="0d3a2-846">FAT Chain Error</span></span>                  | <span data-ttu-id="0d3a2-847">0x01</span><span class="sxs-lookup"><span data-stu-id="0d3a2-847">(0x01)</span></span>  |
  |  <span data-ttu-id="0d3a2-848">Dizin hatası</span><span class="sxs-lookup"><span data-stu-id="0d3a2-848">Directory Error</span></span>                  | <span data-ttu-id="0d3a2-849">0x02 şeklindedir</span><span class="sxs-lookup"><span data-stu-id="0d3a2-849">(0x02)</span></span>  |
  |  <span data-ttu-id="0d3a2-850">Kayıp küme hatası</span><span class="sxs-lookup"><span data-stu-id="0d3a2-850">Lost Cluster Error</span></span>               | <span data-ttu-id="0d3a2-851">(0x04)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-851">(0x04)</span></span>  |
  |  <span data-ttu-id="0d3a2-852">Dosya boyutu hatası</span><span class="sxs-lookup"><span data-stu-id="0d3a2-852">File Size Error</span></span>                  | <span data-ttu-id="0d3a2-853">(0x08)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-853">(0x08)</span></span>  |

### <a name="media-close"></a><span data-ttu-id="0d3a2-854">Medya kapatma</span><span class="sxs-lookup"><span data-stu-id="0d3a2-854">Media Close</span></span> 

#### <a name="fx_media_close"></a><span data-ttu-id="0d3a2-855">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="0d3a2-855">fx_media_close</span></span>

<span data-ttu-id="0d3a2-856">**Simge** ![ Medya kapatma simgesi](./media/user-guide/fx-events/image53.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-856">**Icon** ![Media Close icon](./media/user-guide/fx-events/image53.png)</span></span>

<span data-ttu-id="0d3a2-857">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-857">**Description**</span></span>

<span data-ttu-id="0d3a2-858">Bu olay bir medya kapatma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-858">This event represents a media close event.</span></span>

<span data-ttu-id="0d3a2-859">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-859">**Information Fields**</span></span> 

- <span data-ttu-id="0d3a2-860">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-860">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-861">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-861">Info Field 2: Not used.</span></span>
- <span data-ttu-id="0d3a2-862">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-862">Info Field 3: Not used.</span></span>
- <span data-ttu-id="0d3a2-863">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-863">Info Field 4: Not used.</span></span>

### <a name="media-flush"></a><span data-ttu-id="0d3a2-864">Medya Temizleme</span><span class="sxs-lookup"><span data-stu-id="0d3a2-864">Media Flush</span></span> 

#### <a name="fx_media_flush"></a><span data-ttu-id="0d3a2-865">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="0d3a2-865">fx_media_flush</span></span>

<span data-ttu-id="0d3a2-866">**Simge** ![ Medya Temizleme simgesi](./media/user-guide/fx-events/image54.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-866">**Icon** ![Media flush icon](./media/user-guide/fx-events/image54.png)</span></span>

<span data-ttu-id="0d3a2-867">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-867">**Description**</span></span>

<span data-ttu-id="0d3a2-868">Bu olay bir medya Temizleme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-868">This event represents a media flush event.</span></span>

<span data-ttu-id="0d3a2-869">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-869">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-870">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-870">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-871">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-871">Info Field 2: Not used.</span></span>
- <span data-ttu-id="0d3a2-872">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-872">Info Field 3: Not used.</span></span>
- <span data-ttu-id="0d3a2-873">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-873">Info Field 4: Not used.</span></span>

### <a name="media-format"></a><span data-ttu-id="0d3a2-874">Medya biçimi</span><span class="sxs-lookup"><span data-stu-id="0d3a2-874">Media Format</span></span> 

#### <a name="fx_media_format"></a><span data-ttu-id="0d3a2-875">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="0d3a2-875">fx_media_format</span></span>

<span data-ttu-id="0d3a2-876">**Simge** ![ Medya biçimi simgesi](./media/user-guide/fx-events/image55.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-876">**Icon** ![Media format icon](./media/user-guide/fx-events/image55.png)</span></span>

<span data-ttu-id="0d3a2-877">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-877">**Description**</span></span>

<span data-ttu-id="0d3a2-878">Bu olay bir medya biçimi olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-878">This event represents a media format event.</span></span>

<span data-ttu-id="0d3a2-879">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-879">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-880">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-880">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-881">Bilgi alanı 2: kök girişlerinin sayısı.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-881">Info Field 2: Number of root entries.</span></span>
- <span data-ttu-id="0d3a2-882">Bilgi alanı 3: kesimler.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-882">Info Field 3: Sectors.</span></span>
- <span data-ttu-id="0d3a2-883">Bilgi alanı 4: küme başına kesimler.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-883">Info Field 4: Sectors per cluster.</span></span>

### <a name="media-open"></a><span data-ttu-id="0d3a2-884">Medya açık</span><span class="sxs-lookup"><span data-stu-id="0d3a2-884">Media Open</span></span> 

#### <a name="fx_media_open"></a><span data-ttu-id="0d3a2-885">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="0d3a2-885">fx_media_open</span></span>

<span data-ttu-id="0d3a2-886">**Simge** ![ Medya açma simgesi](./media/user-guide/fx-events/image56.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-886">**Icon** ![Media open icon](./media/user-guide/fx-events/image56.png)</span></span>

<span data-ttu-id="0d3a2-887">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-887">**Description**</span></span>

<span data-ttu-id="0d3a2-888">Bu olay medya açık olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-888">This event represents a media open event.</span></span>

<span data-ttu-id="0d3a2-889">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-889">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-890">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-890">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-891">Bilgi alanı 2: medya sürücüsü girişi Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-891">Info Field 2: Pointer to media driver entry.</span></span>
- <span data-ttu-id="0d3a2-892">Bilgi alanı 3: bellek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-892">Info Field 3: Memory pointer.</span></span>
- <span data-ttu-id="0d3a2-893">Bilgi alanı 4: bellek boyutu.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-893">Info Field 4: Memory size.</span></span>

### <a name="media-read-media-read"></a><span data-ttu-id="0d3a2-894">Medya okuma medya okuma</span><span class="sxs-lookup"><span data-stu-id="0d3a2-894">Media Read Media Read</span></span> 

#### <a name="fx_media_read"></a><span data-ttu-id="0d3a2-895">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="0d3a2-895">fx_media_read</span></span>

<span data-ttu-id="0d3a2-896">**Simge** ![ Medya okuma simgesi](./media/user-guide/fx-events/image57.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-896">**Icon** ![Media read icon](./media/user-guide/fx-events/image57.png)</span></span>

<span data-ttu-id="0d3a2-897">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-897">**Description**</span></span>

<span data-ttu-id="0d3a2-898">Bu olay bir medya okuma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-898">This event represents a media read event.</span></span>

<span data-ttu-id="0d3a2-899">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-899">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-900">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-900">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-901">Bilgi alanı 2: mantıksal kesim.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-901">Info Field 2: Logical sector.</span></span>
- <span data-ttu-id="0d3a2-902">Bilgi alanı 3: arabellek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-902">Info Field 3: Buffer pointer.</span></span>
- <span data-ttu-id="0d3a2-903">Bilgi alanı 4: okunan baytlar.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-903">Info Field 4: Bytes read.</span></span>

### <a name="media-space-available"></a><span data-ttu-id="0d3a2-904">Kullanılabilir medya alanı</span><span class="sxs-lookup"><span data-stu-id="0d3a2-904">Media Space Available</span></span> 

#### <a name="fx_media_space_available"></a><span data-ttu-id="0d3a2-905">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="0d3a2-905">fx_media_space_available</span></span>

<span data-ttu-id="0d3a2-906">**Simge** ![ Medya alanı kullanılabilir simgesi](./media/user-guide/fx-events/image58.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-906">**Icon** ![Media space available icon](./media/user-guide/fx-events/image58.png)</span></span>

<span data-ttu-id="0d3a2-907">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-907">**Description**</span></span>

<span data-ttu-id="0d3a2-908">Bu olay, kullanılabilir bir medya alanı olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-908">This event represents a media space available event.</span></span>

<span data-ttu-id="0d3a2-909">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-909">**Information Fields**</span></span> 

- <span data-ttu-id="0d3a2-910">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-910">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-911">Bilgi alanı 2: kullanılabilir bayt işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-911">Info Field 2: Available bytes pointer.</span></span>
- <span data-ttu-id="0d3a2-912">Bilgi alanı 3: boş küme sayısı.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-912">Info Field 3: Number of free clusters.</span></span>
- <span data-ttu-id="0d3a2-913">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-913">Info Field 4: Not used.</span></span>

### <a name="media-volume-get"></a><span data-ttu-id="0d3a2-914">Medya birimi al</span><span class="sxs-lookup"><span data-stu-id="0d3a2-914">Media Volume Get</span></span> 

#### <a name="fx_media_volume_get"></a><span data-ttu-id="0d3a2-915">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="0d3a2-915">fx_media_volume_get</span></span>

<span data-ttu-id="0d3a2-916">**Simge** ![ Medya birimi al simgesi](./media/user-guide/fx-events/image59.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-916">**Icon** ![Media volume get icon](./media/user-guide/fx-events/image59.png)</span></span>

<span data-ttu-id="0d3a2-917">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-917">**Description**</span></span>

<span data-ttu-id="0d3a2-918">Bu olay bir medya birimi Get olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-918">This event represents a media volume get event.</span></span>

<span data-ttu-id="0d3a2-919">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-919">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-920">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-920">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-921">Bilgi alanı 2: birim adı Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-921">Info Field 2: Pointer to volume name.</span></span>
- <span data-ttu-id="0d3a2-922">Bilgi alanı 3: birim kaynağı.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-922">Info Field 3: Volume source.</span></span>
- <span data-ttu-id="0d3a2-923">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-923">Info Field 4: Not used.</span></span>

### <a name="media-volume-set"></a><span data-ttu-id="0d3a2-924">Medya birimi kümesi</span><span class="sxs-lookup"><span data-stu-id="0d3a2-924">Media Volume Set</span></span> 

#### <a name="fx_media_volume_set"></a><span data-ttu-id="0d3a2-925">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="0d3a2-925">fx_media_volume_set</span></span>

<span data-ttu-id="0d3a2-926">**Simge** ![ Medya birimi kümesi simgesi](./media/user-guide/fx-events/image60.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-926">**Icon** ![Media volume set icon](./media/user-guide/fx-events/image60.png)</span></span>

<span data-ttu-id="0d3a2-927">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-927">**Description**</span></span>

<span data-ttu-id="0d3a2-928">Bu olay bir medya birimi ayarlama olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-928">This event represents a media volume set event.</span></span>

<span data-ttu-id="0d3a2-929">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-929">**Information Fields**</span></span> 
- <span data-ttu-id="0d3a2-930">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-930">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-931">Bilgi alanı 2: birim adı Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-931">Info Field 2: Pointer to volume name.</span></span>
- <span data-ttu-id="0d3a2-932">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-932">Info Field 3: Not used.</span></span>
- <span data-ttu-id="0d3a2-933">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-933">Info Field 4: Not used.</span></span>

### <a name="media-write"></a><span data-ttu-id="0d3a2-934">Medya yazma</span><span class="sxs-lookup"><span data-stu-id="0d3a2-934">Media Write</span></span> 

#### <a name="fx_media_write"></a><span data-ttu-id="0d3a2-935">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="0d3a2-935">fx_media_write</span></span>

<span data-ttu-id="0d3a2-936">**Simge** ![ Medya yazma simgesi](./media/user-guide/fx-events/image61.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-936">**Icon** ![Media write icon](./media/user-guide/fx-events/image61.png)</span></span>

<span data-ttu-id="0d3a2-937">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-937">**Description**</span></span>

<span data-ttu-id="0d3a2-938">Bu olay bir medya yazma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-938">This event represents a media write event.</span></span>

<span data-ttu-id="0d3a2-939">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-939">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-940">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-940">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-941">Bilgi alanı 2: mantıksal kesim.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-941">Info Field 2: Logical sector.</span></span>
- <span data-ttu-id="0d3a2-942">Bilgi alanı 3: arabellek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-942">Info Field 3: Buffer pointer.</span></span>
- <span data-ttu-id="0d3a2-943">Bilgi alanı 4: yazılan baytlar.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-943">Info Field 4: Bytes written.</span></span>

### <a name="system-date-get"></a><span data-ttu-id="0d3a2-944">Sistem tarihi al</span><span class="sxs-lookup"><span data-stu-id="0d3a2-944">System Date Get</span></span> 

#### <a name="fx_system_date_get"></a><span data-ttu-id="0d3a2-945">fx_system_date_get</span><span class="sxs-lookup"><span data-stu-id="0d3a2-945">fx_system_date_get</span></span> 

<span data-ttu-id="0d3a2-946">**Simge** ![ Sistem tarihi al simgesi](./media/user-guide/fx-events/image62.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-946">**Icon** ![System date get icon](./media/user-guide/fx-events/image62.png)</span></span>

<span data-ttu-id="0d3a2-947">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-947">**Description**</span></span>

<span data-ttu-id="0d3a2-948">Bu olay bir sistem tarihi al olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-948">This event represents a system date get event.</span></span>

<span data-ttu-id="0d3a2-949">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-949">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-950">Bilgi alanı 1: yıl.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-950">Info Field 1: Year.</span></span>
- <span data-ttu-id="0d3a2-951">Bilgi alanı 2: ay.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-951">Info Field 2: Month.</span></span>
- <span data-ttu-id="0d3a2-952">Bilgi alanı 3: gün.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-952">Info Field 3: Day.</span></span>
- <span data-ttu-id="0d3a2-953">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-953">Info Field 4: Not used.</span></span>

### <a name="system-date-set"></a><span data-ttu-id="0d3a2-954">Sistem tarihi kümesi</span><span class="sxs-lookup"><span data-stu-id="0d3a2-954">System Date Set</span></span> 

#### <a name="fx_system_date_set"></a><span data-ttu-id="0d3a2-955">fx_system_date_set</span><span class="sxs-lookup"><span data-stu-id="0d3a2-955">fx_system_date_set</span></span> 

<span data-ttu-id="0d3a2-956">**Simge** ![ Sistem tarihi kümesi simgesi](./media/user-guide/fx-events/image63.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-956">**Icon** ![System date set icon](./media/user-guide/fx-events/image63.png)</span></span>

<span data-ttu-id="0d3a2-957">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-957">**Description**</span></span>

<span data-ttu-id="0d3a2-958">Bu olay bir sistem tarihi kümesi olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-958">This event represents a system date set event.</span></span>

<span data-ttu-id="0d3a2-959">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-959">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-960">Bilgi alanı 1: yıl.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-960">Info Field 1: Year.</span></span>
- <span data-ttu-id="0d3a2-961">Bilgi alanı 2: ay.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-961">Info Field 2: Month.</span></span>
- <span data-ttu-id="0d3a2-962">Bilgi alanı 3: gün.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-962">Info Field 3: Day.</span></span>
- <span data-ttu-id="0d3a2-963">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-963">Info Field 4: Not used.</span></span>

### <a name="system-initialize"></a><span data-ttu-id="0d3a2-964">Sistem başlatma</span><span class="sxs-lookup"><span data-stu-id="0d3a2-964">System Initialize</span></span> 

#### <a name="fx_system_initialize"></a><span data-ttu-id="0d3a2-965">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="0d3a2-965">fx_system_initialize</span></span> 

<span data-ttu-id="0d3a2-966">**Simge** ![ Sistem başlatma simgesi](./media/user-guide/fx-events/image64.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-966">**Icon** ![System initialize icon](./media/user-guide/fx-events/image64.png)</span></span>

<span data-ttu-id="0d3a2-967">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-967">**Description**</span></span>

<span data-ttu-id="0d3a2-968">Bu olay bir sistem başlatma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-968">This event represents a system initialize event.</span></span>

<span data-ttu-id="0d3a2-969">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-969">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-970">Bilgi alanı 1: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-970">Info Field 1: Not used.</span></span>
- <span data-ttu-id="0d3a2-971">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-971">Info Field 2: Not used.</span></span>
- <span data-ttu-id="0d3a2-972">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-972">Info Field 3: Not used.</span></span>
- <span data-ttu-id="0d3a2-973">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-973">Info Field 4: Not used.</span></span>

### <a name="system-time-get"></a><span data-ttu-id="0d3a2-974">Sistem saati al</span><span class="sxs-lookup"><span data-stu-id="0d3a2-974">System Time Get</span></span> 

#### <a name="fx_system_time_get"></a><span data-ttu-id="0d3a2-975">fx_system_time_get</span><span class="sxs-lookup"><span data-stu-id="0d3a2-975">fx_system_time_get</span></span> 

<span data-ttu-id="0d3a2-976">**Simge** ![ Sistem saati al simgesi](./media/user-guide/fx-events/image65.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-976">**Icon** ![System time get icon](./media/user-guide/fx-events/image65.png)</span></span>

<span data-ttu-id="0d3a2-977">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-977">**Description**</span></span>

<span data-ttu-id="0d3a2-978">Bu olay bir sistem saati al olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-978">This event represents a system time get event.</span></span>

<span data-ttu-id="0d3a2-979">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-979">**Information Fields**</span></span> 

- <span data-ttu-id="0d3a2-980">Bilgi alanı 1: Saat.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-980">Info Field 1: Hour.</span></span>
- <span data-ttu-id="0d3a2-981">Bilgi alanı 2: dakika.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-981">Info Field 2: Minute.</span></span>
- <span data-ttu-id="0d3a2-982">Bilgi alanı 3: saniye.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-982">Info Field 3: Second.</span></span>
- <span data-ttu-id="0d3a2-983">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-983">Info Field 4: Not used.</span></span>

### <a name="system-time-set"></a><span data-ttu-id="0d3a2-984">Sistem zaman kümesi</span><span class="sxs-lookup"><span data-stu-id="0d3a2-984">System Time Set</span></span> 

#### <a name="fx_system_time_set"></a><span data-ttu-id="0d3a2-985">fx_system_time_set</span><span class="sxs-lookup"><span data-stu-id="0d3a2-985">fx_system_time_set</span></span> 

<span data-ttu-id="0d3a2-986">**Simge** ![ Sistem zaman kümesi simgesi](./media/user-guide/fx-events/image66.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-986">**Icon** ![System time set icon](./media/user-guide/fx-events/image66.png)</span></span>

<span data-ttu-id="0d3a2-987">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-987">**Description**</span></span>

<span data-ttu-id="0d3a2-988">Bu olay bir sistem zaman kümesi olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-988">This event represents a system time set event.</span></span>

<span data-ttu-id="0d3a2-989">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-989">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-990">Bilgi alanı 1: Saat.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-990">Info Field 1: Hour.</span></span>
- <span data-ttu-id="0d3a2-991">Bilgi alanı 2: dakika.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-991">Info Field 2: Minute.</span></span>
- <span data-ttu-id="0d3a2-992">Bilgi alanı 3: saniye.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-992">Info Field 3: Second.</span></span>
- <span data-ttu-id="0d3a2-993">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-993">Info Field 4: Not used.</span></span>

### <a name="unicode-directory-create"></a><span data-ttu-id="0d3a2-994">Unicode dizin oluşturma</span><span class="sxs-lookup"><span data-stu-id="0d3a2-994">Unicode Directory Create</span></span> 

#### <a name="fx_unicode_directory_create"></a><span data-ttu-id="0d3a2-995">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="0d3a2-995">fx_unicode_directory_create</span></span> 

<span data-ttu-id="0d3a2-996">**Simge** ![ Unicode dizin oluşturma simgesi](./media/user-guide/fx-events/image67.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-996">**Icon** ![Unicode directory create icon](./media/user-guide/fx-events/image67.png)</span></span>

<span data-ttu-id="0d3a2-997">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-997">**Description**</span></span>

<span data-ttu-id="0d3a2-998">Bu olay bir Unicode dizin oluşturma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-998">This event represents a Unicode directory create event.</span></span>

<span data-ttu-id="0d3a2-999">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-999">**Information Fields**</span></span> 

- <span data-ttu-id="0d3a2-1000">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1000">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-1001">Bilgi alanı 2: Unicode adı Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1001">Info Field 2: Pointer to Unicode name.</span></span>
- <span data-ttu-id="0d3a2-1002">Bilgi alanı 3: Unicode adının boyutu.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1002">Info Field 3: Size of Unicode name.</span></span>
- <span data-ttu-id="0d3a2-1003">Bilgi alanı 4: kısa ad Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1003">Info Field 4: Pointer to short name.</span></span>

### <a name="unicode-directory-rename"></a><span data-ttu-id="0d3a2-1004">Unicode dizin yeniden adlandırma</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1004">Unicode Directory Rename</span></span> 

#### <a name="fx_unicode_directory_rename"></a><span data-ttu-id="0d3a2-1005">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1005">fx_unicode_directory_rename</span></span>

<span data-ttu-id="0d3a2-1006">**Simge** ![ Unicode dizin yeniden adlandırma simgesi](./media/user-guide/fx-events/image68.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1006">**Icon** ![Unicode directory rename icon](./media/user-guide/fx-events/image68.png)</span></span>

<span data-ttu-id="0d3a2-1007">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1007">**Description**</span></span>

<span data-ttu-id="0d3a2-1008">Bu olay bir Unicode dizin yeniden adlandırma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1008">This event represents a Unicode directory rename event.</span></span>

<span data-ttu-id="0d3a2-1009">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1009">**Information Fields**</span></span> 

- <span data-ttu-id="0d3a2-1010">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1010">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-1011">Bilgi alanı 2: Unicode adı Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1011">Info Field 2: Pointer to Unicode name.</span></span>
- <span data-ttu-id="0d3a2-1012">Bilgi alanı 3: Unicode adının boyutu.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1012">Info Field 3: Size of Unicode name.</span></span>
- <span data-ttu-id="0d3a2-1013">Bilgi alanı 4: kısa ad Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1013">Info Field 4: Pointer to short name.</span></span>

### <a name="unicode-file-create"></a><span data-ttu-id="0d3a2-1014">Unicode dosya oluşturma</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1014">Unicode File Create</span></span> 

#### <a name="fx_unicode_file_create"></a><span data-ttu-id="0d3a2-1015">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1015">fx_unicode_file_create</span></span>

<span data-ttu-id="0d3a2-1016">**Simge** ![ Unicode dosya oluştur simgesi](./media/user-guide/fx-events/image69.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1016">**Icon** ![Unicode file create icon](./media/user-guide/fx-events/image69.png)</span></span>

<span data-ttu-id="0d3a2-1017">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1017">**Description**</span></span>

<span data-ttu-id="0d3a2-1018">Bu olay bir Unicode dosya oluşturma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1018">This event represents a Unicode file create event.</span></span>

<span data-ttu-id="0d3a2-1019">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1019">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-1020">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1020">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-1021">Bilgi alanı 2: Unicode adı Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1021">Info Field 2: Pointer to the Unicode name.</span></span>
- <span data-ttu-id="0d3a2-1022">Bilgi alanı 3: Unicode adının boyutu.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1022">Info Field 3: Size of Unicode name.</span></span>
- <span data-ttu-id="0d3a2-1023">Bilgi alanı 4: kısa ad Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1023">Info Field 4: Pointer to short name.</span></span>

### <a name="unicode-file-rename"></a><span data-ttu-id="0d3a2-1024">Unicode dosya yeniden adlandırma</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1024">Unicode File Rename</span></span> 

#### <a name="fx_unicode_file_rename"></a><span data-ttu-id="0d3a2-1025">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1025">fx_unicode_file_rename</span></span>

<span data-ttu-id="0d3a2-1026">**Simge** ![ Unicode dosya yeniden adlandırma simgesi](./media/user-guide/fx-events/image70.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1026">**Icon** ![Unicode file rename icon](./media/user-guide/fx-events/image70.png)</span></span>

<span data-ttu-id="0d3a2-1027">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1027">**Description**</span></span>

<span data-ttu-id="0d3a2-1028">Bu olay bir Unicode dosya yeniden adlandırma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1028">This event represents a Unicode file rename event.</span></span>

<span data-ttu-id="0d3a2-1029">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1029">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-1030">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1030">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-1031">Bilgi alanı 2: Unicode adı Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1031">Info Field 2: Pointer to Unicode name.</span></span>
- <span data-ttu-id="0d3a2-1032">Bilgi alanı 3: Unicode adının boyutu.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1032">Info Field 3: Size of Unicode name.</span></span>
- <span data-ttu-id="0d3a2-1033">Bilgi alanı 4: kısa ad Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1033">Info Field 4: Pointer to short name.</span></span>

### <a name="unicode-length-get"></a><span data-ttu-id="0d3a2-1034">Unicode uzunluğu al</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1034">Unicode Length Get</span></span> 

#### <a name="fx_unicode_length_get"></a><span data-ttu-id="0d3a2-1035">fx_unicode_length_get</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1035">fx_unicode_length_get</span></span>

<span data-ttu-id="0d3a2-1036">**Simge** ![ Unicode uzunluğu al simgesi](./media/user-guide/fx-events/image71.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1036">**Icon** ![Unicode length get icon](./media/user-guide/fx-events/image71.png)</span></span>

<span data-ttu-id="0d3a2-1037">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1037">**Description**</span></span>

<span data-ttu-id="0d3a2-1038">Bu olay bir Unicode uzunluğu Get olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1038">This event represents a Unicode length get event.</span></span>

<span data-ttu-id="0d3a2-1039">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1039">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-1040">Bilgi alanı 1: Unicode adı Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1040">Info Field 1: Pointer to the Unicode name.</span></span>
- <span data-ttu-id="0d3a2-1041">Bilgi alanı 2: Uzunluk.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1041">Info Field 2: Length.</span></span>
- <span data-ttu-id="0d3a2-1042">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1042">Info Field 3: Not used.</span></span>
- <span data-ttu-id="0d3a2-1043">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1043">Info Field 4: Not used.</span></span>

### <a name="unicode-name-get"></a><span data-ttu-id="0d3a2-1044">Unicode ad al</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1044">Unicode Name Get</span></span> 

#### <a name="fx_unicode_name_get"></a><span data-ttu-id="0d3a2-1045">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1045">fx_unicode_name_get</span></span>

<span data-ttu-id="0d3a2-1046">**Simge** ![ Unicode ad Al simgesi](./media/user-guide/fx-events/image72.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1046">**Icon** ![Unicode name get icon](./media/user-guide/fx-events/image72.png)</span></span>

<span data-ttu-id="0d3a2-1047">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1047">**Description**</span></span>

<span data-ttu-id="0d3a2-1048">Bu olay bir Unicode ad Get olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1048">This event represents a Unicode name get event.</span></span>

<span data-ttu-id="0d3a2-1049">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1049">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-1050">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1050">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-1051">Bilgi alanı 2: kaynak kısa adı.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1051">Info Field 2: Source short name.</span></span>
- <span data-ttu-id="0d3a2-1052">Bilgi alanı 3: hedef Unicode adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1052">Info Field 3: Destination Unicode name pointer.</span></span>
- <span data-ttu-id="0d3a2-1053">Bilgi alanı 4: hedef Unicode adı uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1053">Info Field 4: Destination Unicode name length.</span></span>

### <a name="unicode-short-name-get"></a><span data-ttu-id="0d3a2-1054">Unicode kısa ad al</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1054">Unicode Short Name Get</span></span> 

#### <a name="fx_unicode_short_name_get"></a><span data-ttu-id="0d3a2-1055">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1055">fx_unicode_short_name_get</span></span>

<span data-ttu-id="0d3a2-1056">**Simge** ![ Unicode kısa ad Al simgesi](./media/user-guide/fx-events/image73.png)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1056">**Icon** ![Unicode short name get icon](./media/user-guide/fx-events/image73.png)</span></span>

<span data-ttu-id="0d3a2-1057">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1057">**Description**</span></span>

<span data-ttu-id="0d3a2-1058">Bu olay Unicode kısa ad Get olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1058">This event represents a Unicode short name get event.</span></span>

<span data-ttu-id="0d3a2-1059">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1059">**Information Fields**</span></span>

- <span data-ttu-id="0d3a2-1060">Bilgi alanı 1: medyaya yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1060">Info Field 1: Pointer to the media.</span></span>
- <span data-ttu-id="0d3a2-1061">Bilgi alanı 2: kaynak Unicode adı Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1061">Info Field 2: Pointer to source Unicode name.</span></span>
- <span data-ttu-id="0d3a2-1062">Bilgi alanı 3: Unicode adının uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1062">Info Field 3: Length of Unicode name.</span></span>
- <span data-ttu-id="0d3a2-1063">Bilgi alanı 4: kısa ad Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-1063">Info Field 4: Pointer to short name.</span></span>