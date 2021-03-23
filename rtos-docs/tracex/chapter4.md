---
title: Bölüm 4-Azure RTOS TraceX performans analizi
description: Bu bölümde, Azure RTOS TraceX Performans Analizi Aracı açıklanmaktadır.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: 6cf1b5bd5349efd97c3afc8a9e7f57f477f06f8f
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104827538"
---
# <a name="chapter-4---azure-rtos-tracex-performance-analysis"></a><span data-ttu-id="ca74c-103">Bölüm 4-Azure RTOS TraceX performans analizi</span><span class="sxs-lookup"><span data-stu-id="ca74c-103">Chapter 4 - Azure RTOS TraceX performance analysis</span></span>

<span data-ttu-id="ca74c-104">Bu bölümde, Azure RTOS TraceX Performans Analizi Aracı açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="ca74c-104">This chapter describes the Azure RTOS TraceX performance analysis tool:</span></span>

## <a name="performance-analysis"></a><span data-ttu-id="ca74c-105">Performans Analizi</span><span class="sxs-lookup"><span data-stu-id="ca74c-105">Performance Analysis</span></span>

<span data-ttu-id="ca74c-106">Trackingex, izleme dosyalarının yerleşik performans analizini sağlar.</span><span class="sxs-lookup"><span data-stu-id="ca74c-106">TraceX provides built-in performance analysis of trace files.</span></span> <span data-ttu-id="ca74c-107">*Yürütme profili*, *popüler hizmetler*, *Iş parçacığı yığını kullanımı* ve FileX ve NETX *İstatistikleri dahil* çeşitli *performans istatistikleri* gibi bilgiler kullanıma hazırdır.</span><span class="sxs-lookup"><span data-stu-id="ca74c-107">Information such as the *execution profile*, *popular services*, *thread stack usage*, and various *performance statistics,* including FileX and NetX statistics *,* are readily available.</span></span> <span data-ttu-id="ca74c-108">Bu bilgiler, ***Görünüm*** menüsü öğesi aracılığıyla kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ca74c-108">This information is available via the ***View*** menu item.</span></span> 


## <a name="execution-profile"></a><span data-ttu-id="ca74c-109">Yürütme profili</span><span class="sxs-lookup"><span data-stu-id="ca74c-109">Execution Profile</span></span>

<span data-ttu-id="ca74c-110">***Yürütme profili oluştur** _ düğmesini veya _*_Görünüm-yürütme profilini_\*_ seçtiğinizde, şu anda yüklü olan Izleme dosyası için trackingex yürütme profili sunulur.</span><span class="sxs-lookup"><span data-stu-id="ca74c-110">Selecting the ***Generate Execution Profile** _ button or _*_View -Execution Profile_\*_ presents the TraceX execution profile for the currently loaded trace file.</span></span> <span data-ttu-id="ca74c-111">Örnek ThreadX tanıtım izlemesi ile ilişkili yürütme profili _ \* Şekil 19 \* \* içinde gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ca74c-111">The execution profile associated with the sample ThreadX demonstration trace is shown in _\*Figure 19\*\*.</span></span>

![Örnek ThreadX tanıtım izlemesi ile ilişkili yürütme profilinin ekran görüntüsü.](./media/user-guide/execution_profile.png)

<span data-ttu-id="ca74c-113">**ŞEKIL 19**</span><span class="sxs-lookup"><span data-stu-id="ca74c-113">**FIGURE 19**</span></span>

<span data-ttu-id="ca74c-114">**Şekil 19** ' da gösterilen örnek, işlem zamanının yaklaşık %45 ' ının **_iş parçacığı 2_' nin içinde olduğunu *ve işlem zamanının yaklaşık %51 ' ının _*_iş parçacığı 1_ ' in içinde** olduğunu gösterir. Bu, izlemenin toplu iş parçacıklarının ileti gönderip almasını gösterdiği için bu mantıksal bir olaydır.</span><span class="sxs-lookup"><span data-stu-id="ca74c-114">The example shown in **Figure 19** indicates that nearly 45% of the processing time is inside of **_thread 2_*_ and nearly 51% of the processing time is inside of _*_thread 1_** This is logical since the bulk of the trace shows these threads sending and receiving messages.</span></span> <span data-ttu-id="ca74c-115">Kalan yürütme bağlamlarının Bu örnekte yalnızca az miktarda yürütme süresi vardır.</span><span class="sxs-lookup"><span data-stu-id="ca74c-115">The remaining execution contexts have only a small amount of execution time in this example.</span></span>

## <a name="popular-services"></a><span data-ttu-id="ca74c-116">Popüler hizmetler</span><span class="sxs-lookup"><span data-stu-id="ca74c-116">Popular Services</span></span>

<span data-ttu-id="ca74c-117">\***View->popüler hizmetler** _ seçeneğinin belirlenmesi, şu anda yüklü olan izleme dosyasındaki popüler hizmetleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="ca74c-117">Selecting \***View ->Popular Services** _ presents the popular services in the currently loaded trace file.</span></span> <span data-ttu-id="ca74c-118">Bu bilgiler varsayılan olarak tüm sistem için görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ca74c-118">By default, this information is displayed for the entire system.</span></span> <span data-ttu-id="ca74c-119">Ancak, belirli iş parçacıkları için popüler hizmetler de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ca74c-119">However, the popular services for specific threads are also available.</span></span> <span data-ttu-id="ca74c-120">Örnek ThreadX tanıtım izlemede popüler hizmetler _ \* şekil 20 \* \* ' de gösterilir.</span><span class="sxs-lookup"><span data-stu-id="ca74c-120">The popular services in the sample ThreadX demonstration trace are shown in _\*Figure 20\*\*.</span></span>

![Örnek ThreadX tanıtım izlemede popüler hizmetlerin ekran görüntüsü.](./media/user-guide/popular_services.png)

<span data-ttu-id="ca74c-122">**ŞEKIL 20**</span><span class="sxs-lookup"><span data-stu-id="ca74c-122">**FIGURE 20**</span></span>

<span data-ttu-id="ca74c-123">**Şekil 20** ' de gösterilen örnek, bu izlemede **_tx_queue_send_*_ ve _*_tx_queue_receive_** en popüler iki hizmet olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="ca74c-123">The example shown in **Figure 20** indicates that **_tx_queue_send_*_ and _*_tx_queue_receive_** are the two most popular services in this trace.</span></span> <span data-ttu-id="ca74c-124">Bu, izlemenin yakalandığı standart ThreadX gösterimi davranışıyla tutarlıdır.</span><span class="sxs-lookup"><span data-stu-id="ca74c-124">This is consistent with the behavior of the standard ThreadX demonstration from which this trace was captured.</span></span>

<span data-ttu-id="ca74c-125">Bu pencerenin üst kısmındaki aşağı açılan seçim listesi kullanılarak bu analizler için belirli iş parçacıkları seçilebilir.</span><span class="sxs-lookup"><span data-stu-id="ca74c-125">Specific threads can be selected for this analysis by using the drop down selection list at the top of this window.</span></span> <span data-ttu-id="ca74c-126">**Şekil 21** **_iş parçacığı 3_** için bu analizi gösterir.</span><span class="sxs-lookup"><span data-stu-id="ca74c-126">**Figure 21** shows this analysis for **_thread 3_**.</span></span>

![Bir TraceX popüler hizmetler için çözümlemenin ekran görüntüsü.](./media/user-guide/popular_services_thread3.png)

<span data-ttu-id="ca74c-128">**ŞEKIL 21**</span><span class="sxs-lookup"><span data-stu-id="ca74c-128">**FIGURE 21**</span></span>

## <a name="thread-stack-usage-analysis-for-thread-3"></a><span data-ttu-id="ca74c-129">İş parçacığı yığını kullanımı</span><span class="sxs-lookup"><span data-stu-id="ca74c-129">Thread Stack Usage</span></span> ![3. iş parçacığı için analiz.](./media/user-guide/screen_shot_17.png)

<span data-ttu-id="ca74c-131">\* Iş parçacığı **yığını kullanımını oluştur** _ düğmesini veya _*_Görünüm-> Iş parçacığı yığını kullanımı_*_ , izleme dosyasındaki her iş parçacığının yığın kullanımını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ca74c-131">Selecting the ***Generate Thread Stack Usage** _ button or _*_View -> Thread Stack Usage_\*_ presents the stack usage for each thread in the trace file.</span></span> <span data-ttu-id="ca74c-132">Bu, geçerli iş parçacığı yığın işaretçisi de dahil olmak üzere, dosyadaki izleme girdilerinin çoğunda bulunan ThreadX tarafından gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="ca74c-132">This is accomplished by ThreadX including the current thread stack pointer in many of the trace entries in the file.</span></span> <span data-ttu-id="ca74c-133">Yığın kullanımı %100, yığının taşdığını ve uygulamada düzeltilmesi gerektiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="ca74c-133">A stack usage of 100% indicates the stack has overflowed and must be corrected in the application.</span></span> <span data-ttu-id="ca74c-134">Bu izleme dosyasında iş parçacığı yürütmesi yoksa, bu iş parçacığı için yığın kullanımı %0 olarak gösterilir.</span><span class="sxs-lookup"><span data-stu-id="ca74c-134">If there is no thread execution within this trace file, the stack usage for that thread is shown at 0%.</span></span> <span data-ttu-id="ca74c-135">Örnek ThreadX tanıtım izlemede iş parçacığı yığını kullanımı _ \* şekil 22 \* \* içinde gösteriliyor.</span><span class="sxs-lookup"><span data-stu-id="ca74c-135">The thread stack usage in the sample ThreadX demonstration trace is shown in _\*Figure 22\*\*.</span></span>

![TraceX Iş parçacığı yığını kullanımının ekran görüntüsü.](./media/user-guide/thread_stack_usage.png)

<span data-ttu-id="ca74c-137">**ŞEKIL 22**</span><span class="sxs-lookup"><span data-stu-id="ca74c-137">**FIGURE 22**</span></span>

<span data-ttu-id="ca74c-138">**Şekil 22** ' de gösterilen örnek, bu izlemede en çok iş parçacığının %9 ve %12 yığın kullanımı arasında olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="ca74c-138">The example shown in **Figure 22** indicates that most threads in this trace have between 9% and 12% stack usage.</span></span>

## <a name="performance-statistics"></a><span data-ttu-id="ca74c-139">Performans Istatistikleri</span><span class="sxs-lookup"><span data-stu-id="ca74c-139">Performance Statistics</span></span>

<span data-ttu-id="ca74c-140">***Performans Istatistikleri oluştur** _ düğmesi veya _ *_View-> performans istatistikleri_** seçeneğinin belirlenmesi, şu anda yüklü olan izleme dosyasının performans istatistiklerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="ca74c-140">Selecting the ***Generate Performance Statistics** _ button or _ *_View -> Performance Statistics_** presents the performance statistics of the currently loaded trace file.</span></span> <span data-ttu-id="ca74c-141">Bu bilgiler varsayılan olarak tüm sistem için görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ca74c-141">By default, this information is displayed for the entire system.</span></span> <span data-ttu-id="ca74c-142">Ancak, performans istatistikleri her belirli iş parçacığı için de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ca74c-142">However, the performance statistics are also available for each specific thread.</span></span>

<span data-ttu-id="ca74c-143">Örnek ThreadX tanıtım izlemenin performans istatistikleri **Şekil 23**' te gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ca74c-143">The performance statistics of the sample ThreadX demonstration trace are shown in **Figure 23**.</span></span>

![TraceX performans istatistiklerinin ekran görüntüsü.](./media/user-guide/performance_statistics.png)

<span data-ttu-id="ca74c-145">**ŞEKIL 23**</span><span class="sxs-lookup"><span data-stu-id="ca74c-145">**FIGURE 23**</span></span>

<span data-ttu-id="ca74c-146">**Şekil 23** ' te gösterilen örnek, bu izleme dosyasında 18 bağlam anahtarı olduğunu ve beş iş parçacığı preemptions, 16 iş parçacığı getirilmesi, 19 iş parçacığı bağlantının sürdürülmesi ve üç kesme olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="ca74c-146">The example shown in **Figure 23** indicates that there were 18 context switches in this trace file, as well as five thread preemptions, 16 thread suspensions, 19 thread resumptions, and three interrupts.</span></span> <span data-ttu-id="ca74c-147">Bu izleme dosyasında herhangi bir öncelik sürümü bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="ca74c-147">There were no priority inversions found in this trace file.</span></span> <span data-ttu-id="ca74c-148">İki tür öncelik de vardır; Yani, *belirleyici* ve *belirleyici olmayan* iki kategori.</span><span class="sxs-lookup"><span data-stu-id="ca74c-148">Notice there are two categories of priority inversions, namely, *deterministic* and *nondeterministic*.</span></span> <span data-ttu-id="ca74c-149">Belirleyici öncelik Inversions, daha düşük öncelikli bir iş parçacığına ait olan bir mutex üzerinde bir iş parçacığının engellendiği öncelikli bir sürümdür.</span><span class="sxs-lookup"><span data-stu-id="ca74c-149">Deterministic priority inversions are priority inversion in which a thread is blocked on a mutex owned by a lower priority thread.</span></span> <span data-ttu-id="ca74c-150">Belirleyici olmayan bir öncelik, farklı bir öncelik iş parçacığının belirleyici bir öncelik veya sürüm sırasında çalıştığı yerdir.</span><span class="sxs-lookup"><span data-stu-id="ca74c-150">An nondeterministic priority inversion is where a different lower priority thread runs during a deterministic priority inversion.</span></span> <span data-ttu-id="ca74c-151">Daha sonra uygulamada öngörülemeyen zamanlama davranışına neden olabilir ve dikkatli araştırdık olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ca74c-151">The later can cause unforeseen timing behavior in the application and should be studied carefully.</span></span>

## <a name="filex-statistics"></a><span data-ttu-id="ca74c-152">FileX Istatistikleri</span><span class="sxs-lookup"><span data-stu-id="ca74c-152">FileX Statistics</span></span>

<span data-ttu-id="ca74c-153">\***View-> FileX STATISTICS** _ ' i seçmek, şu anda yüklü olan Izleme dosyasının FileX performans istatistiklerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="ca74c-153">Selecting \***View -> FileX Statistics** _ presents the FileX performance statistics of the currently loaded trace file.</span></span> <span data-ttu-id="ca74c-154">Bu bilgiler tüm sistemde, tüm açıldıklarında görüntülenir. /Media nesneleri.</span><span class="sxs-lookup"><span data-stu-id="ca74c-154">This information is displayed for the entire system, on all opened ../media objects.</span></span> <span data-ttu-id="ca74c-155">Örnek FileX tanıtım izlemesinin performans istatistikleri _ \* Şekil 24 \* \* içinde gösterilir.</span><span class="sxs-lookup"><span data-stu-id="ca74c-155">The performance statistics of the sample FileX demonstration trace are shown in _\*Figure 24\*\*.</span></span>

![FileX Istatistiklerinin ekran görüntüsü.](./media/user-guide/filex_statistics.png)

<span data-ttu-id="ca74c-157">**ŞEKIL 24**</span><span class="sxs-lookup"><span data-stu-id="ca74c-157">**FIGURE 24**</span></span>

<span data-ttu-id="ca74c-158">**Şekil 27** ' de gösterilen örnek 19 olduğunu gösterir. /Medya açılır, 19.. /Media kapanıyor, 19.. /Medya Temizleme, 18 dizin okuma, 19 Dizin yazma ve 18 Dizin önbellek isabetsizliği.</span><span class="sxs-lookup"><span data-stu-id="ca74c-158">The example shown in **Figure 27** indicates there were 19 ../media opens, 19 ../media closes, 19 ../media flushes, 18 directory reads, 19 directory writes, and 18 directory cache misses.</span></span> <span data-ttu-id="ca74c-159">Ek ton bilgileri, İstatistik penceresinde aşağı kaydırarak görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="ca74c-159">Additonal information can be viewed by scrolling down in the statistics window.</span></span>

## <a name="netx-statistics"></a><span data-ttu-id="ca74c-160">NetX Istatistikleri</span><span class="sxs-lookup"><span data-stu-id="ca74c-160">NetX Statistics</span></span>

<span data-ttu-id="ca74c-161">\***View-NetX STATISTICS** _ öğesinin seçilmesi, yüklü olan Izleme dosyasının NETX performans istatistiklerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="ca74c-161">Selecting \***View -NetX Statistics** _ presents the NetX performance statistics of the currently loaded trace file.</span></span> <span data-ttu-id="ca74c-162">Bu bilgiler tüm sistem için görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ca74c-162">This information is displayed for the entire system.</span></span> <span data-ttu-id="ca74c-163">Örnek NetX tanıtım izlemesinin performans istatistikleri _ \* Şekil 25 \* \* içinde gösterilir.</span><span class="sxs-lookup"><span data-stu-id="ca74c-163">The performance statistics of the sample NetX demonstration trace are shown in _\*Figure 25\*\*.</span></span>

![NetX Istatistiklerinin ekran görüntüsü.](./media/user-guide/netx_statistics.png)

<span data-ttu-id="ca74c-165">**ŞEKIL 25**</span><span class="sxs-lookup"><span data-stu-id="ca74c-165">**FIGURE 25**</span></span>

<span data-ttu-id="ca74c-166">**Şekil 25** ' te gösterilen örnek, ARP, PıNG veya UDP olayları olmadığını, ancak gönderilen 30 IP paketi olduğunu, 1.368 IP baytı gönderildiğini, 30 IP paketi alındığını ve 1.360 IP bayt alındığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ca74c-166">The example shown in **Figure 25** indicates there were no ARP, Ping, or UDP events, but there were 30 IP packets sent, 1,368 IP bytes sent, 30 IP packets received, and 1,360 IP bytes received.</span></span>

## <a name="trace-file-information"></a><span data-ttu-id="ca74c-167">İzleme dosyası bilgileri</span><span class="sxs-lookup"><span data-stu-id="ca74c-167">Trace File Information</span></span>

<span data-ttu-id="ca74c-168">\***View-> Izleme dosyası bilgilerini** seçin _, açılan izleme dosyası hakkında bazı temel bilgileri gösterir.</span><span class="sxs-lookup"><span data-stu-id="ca74c-168">Selecting \***View -> Trace File Information** _ presents some basic information about the opened trace file.</span></span> <span data-ttu-id="ca74c-169">Bu bilgiler, dosyanın bayt sırasını, zaman kaynağının boyutunu, her bir nesne adı için en fazla bayt sayısını ve tüm izleme dosyası işaretçilerinin temel adresini içerir.</span><span class="sxs-lookup"><span data-stu-id="ca74c-169">This information includes the byte order of the file, size of the time source, maximum number of bytes for each object name, and the base address of all trace file pointers.</span></span> <span data-ttu-id="ca74c-170">_ *Şekil 26*\* standart **_demo_threadx. trx_** izleme dosyası için izleme dosyası bilgilerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="ca74c-170">_ *Figure 26*\* shows the trace file information for the standard **_demo_threadx.trx_** trace file.</span></span>

![TraceX dosya bilgilerinin ekran görüntüsü.](./media/user-guide/trace_file_info.png)

<span data-ttu-id="ca74c-172">**ŞEKIL 26**</span><span class="sxs-lookup"><span data-stu-id="ca74c-172">**FIGURE 26**</span></span>

## <a name="raw-trace-dump"></a><span data-ttu-id="ca74c-173">Ham Izleme dökümü</span><span class="sxs-lookup"><span data-stu-id="ca74c-173">Raw Trace Dump</span></span>

<span data-ttu-id="ca74c-174">\***View-> ham Izleme dökümünü al**' ı seçtiğinizde, ham izleme dökümünü içeren dosyayı adlandırmak için bir iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ca74c-174">Selecting \***View -> Raw Trace Dump** _ presents a dialog to name the file containing the raw trace dump.</span></span> <span data-ttu-id="ca74c-175">Dosya adı ve yolu girildikten sonra, TraceX ham izleme dosyasını metin biçiminde oluşturur ve bunu göstermek için _*_notepad.exe_*_ başlatır.</span><span class="sxs-lookup"><span data-stu-id="ca74c-175">After the file name and path are entered, TraceX builds the raw trace file in text format and launches _*_notepad.exe_*_ to display it.</span></span> <span data-ttu-id="ca74c-176">_ *Şekil 27*\* standart **_demo_threadx. trx_** izleme dosyası için ham izleme dosyası dökümünü gösterir.</span><span class="sxs-lookup"><span data-stu-id="ca74c-176">_ *Figure 27*\* shows the raw trace file dump for the standard **_demo_threadx.trx_** trace file.</span></span>

![Ham izleme dökümünden oluşan ekran görüntüsü.](./media/user-guide/raw_trace_dump.png)

<span data-ttu-id="ca74c-178">**ŞEKIL 27**</span><span class="sxs-lookup"><span data-stu-id="ca74c-178">**FIGURE 27**</span></span>
