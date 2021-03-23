---
title: Ek D-döküm ve izleme arabelleği
description: Azure RTOS ThreadX tarafından oluşturulan izleme arabelleğinin ana bilgisayardaki bir dosyaya dökümünü almak, kullanılan özel geliştirme aracı tarafından belirtilen komutlar ve/veya yardımcı programlar aracılığıyla yapılır.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: 30f6b5e329feeb2dca37dda391fd738aba587c9a
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104827724"
---
# <a name="appendix-d---dumping-and-trace-buffer"></a><span data-ttu-id="5cd4c-103">Ek D-döküm ve izleme arabelleği</span><span class="sxs-lookup"><span data-stu-id="5cd4c-103">Appendix D - Dumping and trace buffer</span></span>

<span data-ttu-id="5cd4c-104">Azure RTOS ThreadX tarafından oluşturulan izleme arabelleğinin ana bilgisayardaki bir dosyaya dökümünü almak, kullanılan özel geliştirme aracı tarafından belirtilen komutlar ve/veya yardımcı programlar aracılığıyla yapılır.</span><span class="sxs-lookup"><span data-stu-id="5cd4c-104">Dumping the trace buffer created by Azure RTOS ThreadX to a file on the host computer is done via commands and/or utilities provided by the specific development tool being used.</span></span> <span data-ttu-id="5cd4c-105">Bu ek, ThreadX ile kullanılan daha popüler geliştirme araçlarından bazılarının bir izleme arabelleğinin bir konak dosyasına dökümünü alma örnekleri içerir.</span><span class="sxs-lookup"><span data-stu-id="5cd4c-105">This appendix contains examples of dumping a trace buffer to a host file in some of the more popular development tools used with ThreadX.</span></span> 

## <a name="benchx-tools"></a><span data-ttu-id="5cd4c-106">BenchX araçları</span><span class="sxs-lookup"><span data-stu-id="5cd4c-106">BenchX Tools</span></span>

<span data-ttu-id="5cd4c-107">İzleme arabelleği, aşağıda gösterildiği gibi _ *_bellek görünümü_* \* Içindeki \***dosya depolama** _ düğmesine tıklayarak benchx araçlarıyla kolayca bir ana bilgisayar dosyasına dökülebilir:</span><span class="sxs-lookup"><span data-stu-id="5cd4c-107">The trace buffer can be dumped to a host file easily with the BenchX tools by selecting the ***Store Memory To File** _ button within the _*_Memory View_\*\*, as shown below:</span></span>

![BenchX araçlarındaki bellek görünümünün ekran görüntüsü.](./media/user-guide/image642.jpg)

<span data-ttu-id="5cd4c-109">Bu noktada, izleme arabelleği adresini, boyutunu, hedef dosya adını (yol dahil) belirtin ve aşağıda gösterildiği gibi ***Kaydet*** düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="5cd4c-109">At this point, specify the trace buffer address, size, destination file name (including path), and select the ***Save*** button as shown below.</span></span> <span data-ttu-id="5cd4c-110">Bu işlem, TraceX içinde görüntülenmek üzere ikili izleme dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5cd4c-110">This will create the binary trace file for viewing within TraceX.</span></span>

![BenchX araçları Kaydet iletişim kutusunun ekran görüntüsü.](./media/user-guide/image643.jpg)

## <a name="realview-tools"></a><span data-ttu-id="5cd4c-112">RealView araçları</span><span class="sxs-lookup"><span data-stu-id="5cd4c-112">RealView Tools</span></span>

<span data-ttu-id="5cd4c-113">Aşağıdaki komutu, RealView içinde komut satırı istemine girerek, izleme arabelleği ARM RealView araçlarıyla kolayca bir ana bilgisayar dosyasına dökülebilir:</span><span class="sxs-lookup"><span data-stu-id="5cd4c-113">The trace buffer can be dumped to a host file easily with the ARM RealView tools by entering the following command at the command-line prompt in RealView:</span></span>

```c 
> WRITEFILE,raw trace_file.trx=0x6860..0xE560
```

<span data-ttu-id="5cd4c-114">Tamamlandıktan sonra, ***trace_file. trx*** dosyası, 0x6860 adresinden başlayarak bulunan izleme arabelleğini Içerir ve 0xE560 adresine gider.</span><span class="sxs-lookup"><span data-stu-id="5cd4c-114">Upon completion, the file ***trace_file.trx*** will contain the trace buffer that is located starting at the address 0x6860 and goes up to address 0xE560.</span></span> <span data-ttu-id="5cd4c-115">Bu dosya TraceX tarafından görüntülenmek için hazırlanıyor.</span><span class="sxs-lookup"><span data-stu-id="5cd4c-115">This file is ready for viewing by TraceX.</span></span>

## <a name="iar-tools"></a><span data-ttu-id="5cd4c-116">IAR araçları</span><span class="sxs-lookup"><span data-stu-id="5cd4c-116">IAR Tools</span></span>

<span data-ttu-id="5cd4c-117">İzleme arabelleği ıAR araçlarıyla kolayca bir ana bilgisayar dosyasına dökülebilir, bu da bellek görünümüne sağ tıklayıp ***bellek kaydet*** ' i seçerek...</span><span class="sxs-lookup"><span data-stu-id="5cd4c-117">The trace buffer can be dumped to a host file easily with the IAR tools by simply right-clicking in the memory view and selecting the ***Memory Save…***</span></span> <span data-ttu-id="5cd4c-118">seçeneğini aşağıda gösterildiği gibi yapın.</span><span class="sxs-lookup"><span data-stu-id="5cd4c-118">option, as shown below.</span></span>

![IAR araçlarında bellek kaydetme seçeneğinin ekran görüntüsü.](./media/user-guide/image0_311.jpg)

<span data-ttu-id="5cd4c-120">Bu, \***bellek kaydetme** _ iletişim kutusunun görüntülenmesine neden olur.</span><span class="sxs-lookup"><span data-stu-id="5cd4c-120">This results in the \***Memory Save** _ dialog to be displayed.</span></span> <span data-ttu-id="5cd4c-121">Başlangıç ve bitiş adresini ve izleme dosyası adını girin, sonra _*_Kaydet_*_ düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="5cd4c-121">Enter the starting and ending address and the trace file name, then select the _*_Save_*_ button.</span></span> <span data-ttu-id="5cd4c-122">Aşağıda gösterilen örnekte, ıAR araçları, belirtilen izleme arabelleğini _ *_trace_file. hex_* \* DOSYASıNDAKI Intel onaltılı kayıtlarına kaydeder.</span><span class="sxs-lookup"><span data-stu-id="5cd4c-122">In the example shown below, the IAR tools save the specified trace buffer into Intel HEX records in the file _\*_trace_file.hex_\*\*.</span></span>

![IAR araçları bellek kaydetme iletişim kutusunun ekran görüntüsü.](./media/user-guide/image648.jpg)

<span data-ttu-id="5cd4c-124">Bu noktada, izleme arabelleği konaktaki ***trace_file. hex*** dosyasında kaydedilir ve tracex ile görüntülenmek üzere hazırlandık.</span><span class="sxs-lookup"><span data-stu-id="5cd4c-124">At this point, we have the trace buffer saved in the ***trace_file.hex*** file on the host and is ready for viewing with TraceX.</span></span>

## <a name="codewarrior-tools"></a><span data-ttu-id="5cd4c-125">CodeWarrior araçları</span><span class="sxs-lookup"><span data-stu-id="5cd4c-125">CodeWarrior Tools</span></span>

<span data-ttu-id="5cd4c-126">İzleme arabelleği, komut penceresine \***Save** _ komutunu girerek, CodeWarrior araçlarıyla kolayca bir ana bilgisayar dosyasına dökülebilir.</span><span class="sxs-lookup"><span data-stu-id="5cd4c-126">The trace buffer can be dumped to a host file easily with the CodeWarrior tools by entering the \***save** _ command in the Command Window.</span></span> <span data-ttu-id="5cd4c-127">Aşağıdaki örnek _ *_Save_*\* komutu, izleme arabelleğinin 0x102200 ' da başlayacağını ve 0x109f00 ' da bittiğini varsayar:</span><span class="sxs-lookup"><span data-stu-id="5cd4c-127">The following example _ *_save_*\* command assumes the trace buffer starts at 0x102200 and ends at 0x109F00:</span></span>

```c
> save –b p:0x102200..0x109F00 trace_file.trx -a 32bit
```

<span data-ttu-id="5cd4c-128">Bu, izleme arabelleğinin konaktaki ***trace_file. trx*** dosyasına kaydedilmesine neden olur.</span><span class="sxs-lookup"><span data-stu-id="5cd4c-128">This results in the trace buffer being saved in the file ***trace_file.trx*** on the host.</span></span>

## <a name="mplab-tools"></a><span data-ttu-id="5cd4c-129">MPLAB araçları</span><span class="sxs-lookup"><span data-stu-id="5cd4c-129">MPLAB Tools</span></span>

<span data-ttu-id="5cd4c-130">MPLAB, dışa aktarma tablosu aracılığıyla, bir konak dosyasına herhangi bir bellek aralığının dışarı aktarılmasını sağlayan bir TraceX uyumlu izleme dosyası oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="5cd4c-130">MPLAB can create a TraceX-compatible trace file through its Export Table utility, which allows the export of any range of memory to a host file.</span></span> <span data-ttu-id="5cd4c-131">Bu yardımcı programı, TraceX için bir izleme dosyası oluşturmak üzere kullanmak için aşağıdaki gibi ilerleyin:</span><span class="sxs-lookup"><span data-stu-id="5cd4c-131">To use this utility to create a trace file for TraceX, proceed as follows:</span></span>

<span data-ttu-id="5cd4c-132">**1. adım** Görüntüle-> belleği ' nı seçerek bir bellek penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="5cd4c-132">**Step 1** Open a memory window by selecting View -> Memory.</span></span>

![Görünüm menüsünde seçilen belleğin ekran görüntüsü.](./media/user-guide/image0_316.jpg)

<span data-ttu-id="5cd4c-134">**2. adım** Seçeneklerin bir listesini görüntülemek için **bellek görünümü** ' ne sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5cd4c-134">**Step 2** Right-click within the **Memory View** to display a list of options.</span></span> <span data-ttu-id="5cd4c-135">Bayt görüntüleme seçeneğini belirlemek için **görüntü biçimini belirtin-1 bayt** .</span><span class="sxs-lookup"><span data-stu-id="5cd4c-135">Specify **Display Format -1 Byte** to select byte display..</span></span>

![Görüntüleme biçimi seçeneği belirlenmiş bellek görünümünün ekran görüntüsü.](./media/user-guide/image650.png)

![Git iletişim kutusunun ekran görüntüsü.](./media/user-guide/image651.jpg)

<span data-ttu-id="5cd4c-138">**3. adım** **Bellek görünümü** penceresinde tekrar sağ tıklayın ve olay arabelleğinin adresini belirtmenizi sağlayan bir iletişim kutusu açan **Git**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="5cd4c-138">**Step 3** Right-click again within the **Memory View** Window and select **Go To**, which opens a dialog box that enables you to specify the address of the event buffer.</span></span> <span data-ttu-id="5cd4c-139">Bu örnekte görüntülenmekte olan **_event_buffer_** gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="5cd4c-139">This example shows **_event_buffer_** being displayed.</span></span>

![Bellek görünümünün git seçeneği seçili olan ekran görüntüsü.](./media/user-guide/image0_312.jpg)

![Görüntülenmekte olan event_buffer gösteren bir örnek ekran görüntüsü.](./media/user-guide/image653.png)

<span data-ttu-id="5cd4c-142">**4. adım** Bu, her zaman BTXT... dizesi olan izleme arabelleğinin ilk konumunun içeriğini vurgular.</span><span class="sxs-lookup"><span data-stu-id="5cd4c-142">**Step 4** This highlights the contents of the first location of the trace buffer, which is always the string BTXT….</span></span>

![İzleme arabelleğinin ilk konumunun ekran görüntüsü.](./media/user-guide/image0_313.jpg)

<span data-ttu-id="5cd4c-144">**5. adım** Şimdi, Seçenekler menüsünü açmak için tekrar sağ tıklayın ve **tabloyu dışarı aktar**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="5cd4c-144">**Step 5** Now, right-click again to bring up the options menu, and select **Export Table**.</span></span>

![Tablo ver seçeneğinin seçili olduğu bellek görünümünün ekran görüntüsü.](./media/user-guide/image0_314.jpg)

<span data-ttu-id="5cd4c-146">**6. adım** Bu, gösterilen şekilde **dışa aktarma tablosunu** getirir.</span><span class="sxs-lookup"><span data-stu-id="5cd4c-146">**Step 6** This brings up the **Export Table** dialog, as shown.</span></span> <span data-ttu-id="5cd4c-147">Dışarı aktarılacak adres aralığını belirtin.</span><span class="sxs-lookup"><span data-stu-id="5cd4c-147">Specify the range of addresses to export.</span></span> <span data-ttu-id="5cd4c-148">8K izleme arabelleği için, bu örnekte olduğu gibi, 0xA00006AC ' nin 0xA00026AC aralığını belirtin ve oluşturulacak ana bilgisayar dosyası için bir ad girin (Bu örnekte demo_threadx. trx).</span><span class="sxs-lookup"><span data-stu-id="5cd4c-148">For an 8K trace buffer, as is the case in this example, specify the range 0xA00006AC to 0xA00026AC, and enter a name for the host file to be created (demo_threadx.trx in this example).</span></span>

<span data-ttu-id="5cd4c-149">! [[Farklı ver iletişim kutusunun ekran görüntüsü.](./media/user-guide/image656.jpg)</span><span class="sxs-lookup"><span data-stu-id="5cd4c-149">![[Screenshot of the Export As dialog.](./media/user-guide/image656.jpg)</span></span>

<span data-ttu-id="5cd4c-150">**Adım 7** Konakta **demo_threadx. trx** adlı bir dosya oluşturulacaktır ve bu dosya tracex tarafından açılabilir.</span><span class="sxs-lookup"><span data-stu-id="5cd4c-150">**Step 7** A file named **demo_threadx.trx** will be created on the host, and this file can be opened by TraceX.</span></span>

## <a name="ghs-tools"></a><span data-ttu-id="5cd4c-151">GHS araçları</span><span class="sxs-lookup"><span data-stu-id="5cd4c-151">GHS Tools</span></span>

<span data-ttu-id="5cd4c-152">İzleme arabelleği, hata ayıklama komut penceresinde komut satırı isteminde aşağıdaki komutu girerek, GHS araçlarıyla kolayca bir ana bilgisayar dosyasına dökülebilir:</span><span class="sxs-lookup"><span data-stu-id="5cd4c-152">The trace buffer can be dumped to a host file easily with the GHS tools by entering the following command at the command-line prompt in the debug command window:</span></span>

```c
memdump raw c:releasethreadxdemo_threadx.trx event_buffer 32768
```

<span data-ttu-id="5cd4c-153">Tamamlandıktan sonra, **demo_threadx. trx** dosyası, 32.768 bayt boyutunda event_buffer bulunan ve tracex tarafından görüntülenmek üzere hazırlanmakta olan izleme arabelleğini içerecektir.</span><span class="sxs-lookup"><span data-stu-id="5cd4c-153">Upon completion, the file **demo_threadx.trx** will contain the trace buffer that is located in the event_buffer with a size of 32,768 bytes and is ready for viewing by TraceX.</span></span>

## <a name="renesas-hew"></a><span data-ttu-id="5cd4c-154">Renesas HEW</span><span class="sxs-lookup"><span data-stu-id="5cd4c-154">Renesas HEW</span></span>

<span data-ttu-id="5cd4c-155">İzleme arabelleği, aşağıdaki üç adımı (ve alt adımları) izleyerek Renasas HEW araçlarıyla kolayca bir ana bilgisayar dosyasına dökülebilir:</span><span class="sxs-lookup"><span data-stu-id="5cd4c-155">The trace buffer can be dumped to a host file easily with the Renasas HEW tools by following the three steps (and substeps) below:</span></span>

<span data-ttu-id="5cd4c-156">**1. adım** Bellek penceresini açın.</span><span class="sxs-lookup"><span data-stu-id="5cd4c-156">**Step 1** Open Memory Window.</span></span>

<span data-ttu-id="5cd4c-157">! [[Bellek penceresinin ekran görüntüsü.](./media/user-guide/image657.jpg)</span><span class="sxs-lookup"><span data-stu-id="5cd4c-157">![[Screenshot of the Memory Window.](./media/user-guide/image657.jpg)</span></span>

<span data-ttu-id="5cd4c-158">**2. adım** İmleci bellek penceresinde yerleştirin ve sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5cd4c-158">**Step 2** Place cursor within memory window and right click.</span></span>

![Kaydet seçeneği belirlenmiş olan bellek penceresinin ekran görüntüsü.](./media/user-guide/image0_315.jpg)

<span data-ttu-id="5cd4c-160">**3. adım** Kaydet ' i seçin, ardından belleği farklı Kaydet penceresinde aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="5cd4c-160">**Step 3** Select Save, then in the Save Memory As window do the following:</span></span>

- <span data-ttu-id="5cd4c-161">Dosya biçimi seçin: Ikili.</span><span class="sxs-lookup"><span data-stu-id="5cd4c-161">Select File format: Binary.</span></span>
- <span data-ttu-id="5cd4c-162">Dosya adını belirtin: Istendiği gibi</span><span class="sxs-lookup"><span data-stu-id="5cd4c-162">Specify Filename: As Desired</span></span>
- <span data-ttu-id="5cd4c-163">Başlangıç adresini belirtin: trace_buffer</span><span class="sxs-lookup"><span data-stu-id="5cd4c-163">Specify Start address: trace_buffer</span></span>
- <span data-ttu-id="5cd4c-164">Bitiş adresini belirtin: (trace_buffer + boyut)</span><span class="sxs-lookup"><span data-stu-id="5cd4c-164">Specify End address: (trace_buffer+size)</span></span>
- <span data-ttu-id="5cd4c-165">Erişim boyutunu belirtin: 1</span><span class="sxs-lookup"><span data-stu-id="5cd4c-165">Specify Access size: 1</span></span>
- <span data-ttu-id="5cd4c-166">Kaydet’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5cd4c-166">Click Save</span></span>

![Belleği Kaydet iletişim kutusunun ekran görüntüsü.](./media/user-guide/image659.jpg)