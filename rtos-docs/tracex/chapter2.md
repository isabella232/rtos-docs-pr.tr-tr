---
title: Bölüm 2-Azure RTOS TraceX yükleme ve kullanımı
description: Bu bölümde, Azure RTOS TraceX sistem analizi aracının yüklenmesiyle, kurulumuyla ve kullanımıyla ilgili çeşitli sorunların açıklaması yer almaktadır.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: 05d7fe3df38c7e8a3480c8ea0d4922a109de9ede
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104827574"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-tracex"></a><span data-ttu-id="c099a-103">Bölüm 2-Azure RTOS TraceX yükleme ve kullanımı</span><span class="sxs-lookup"><span data-stu-id="c099a-103">Chapter 2 - Installation and use of Azure RTOS TraceX</span></span>

<span data-ttu-id="c099a-104">Bu bölümde, Azure RTOS TraceX sistem analizi aracının yüklenmesiyle, kurulumuyla ve kullanımıyla ilgili çeşitli sorunların açıklaması yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="c099a-104">This chapter contains a description of various issues related to installation, setup, and usage of the Azure RTOS TraceX system analysis tool.</span></span> 

## <a name="product-distribution"></a><span data-ttu-id="c099a-105">Ürün dağıtımı</span><span class="sxs-lookup"><span data-stu-id="c099a-105">Product Distribution</span></span>

<span data-ttu-id="c099a-106">Tracex 'yi arayarak veya doğrudan [tracex sayfasına](https://www.microsoft.com/p/azure-rtos-tracex/9nf1lfd5xxg3?activetab=pivot:overviewtab)giderek, [Microsoft App Store](https://microsoft.com/store/apps) 'dan trackingex uygulamasını elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c099a-106">You can obtain the TraceX app from the [Microsoft App Store](https://microsoft.com/store/apps) by searching for TraceX, or by going directly to [the TraceX page](https://www.microsoft.com/p/azure-rtos-tracex/9nf1lfd5xxg3?activetab=pivot:overviewtab).</span></span> <span data-ttu-id="c099a-107">Ardından aşağıdakileri yapın.</span><span class="sxs-lookup"><span data-stu-id="c099a-107">Then do the following.</span></span>

1. <span data-ttu-id="c099a-108">Uygulama mağazasındaki TraceX sayfasında, TraceX **'yi yüklemek** için **Al veya Al** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c099a-108">From the TraceX page in the App Store, click the **Get** or **Install** button to install TraceX.</span></span>

1. <span data-ttu-id="c099a-109">Tarayıcınız, aşağıdaki şekilde gösterildiği gibi Microsoft Store açmak isteyip istemediğinizi soran bir ileti görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="c099a-109">Your browser may display a message asking if you want to open the Microsoft Store, as shown in the figure below.</span></span> <span data-ttu-id="c099a-110">Varsa, **Aç** düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="c099a-110">If it does, choose the **Open** button.</span></span>
<span data-ttu-id="c099a-111">![Trackingex 'ı yüklemek için Aç ' ı seçin.](../guix/media/guix-studio/open-ms-store.png)</span><span class="sxs-lookup"><span data-stu-id="c099a-111">![Choose Open to install TraceX.](../guix/media/guix-studio/open-ms-store.png)</span></span>

1. <span data-ttu-id="c099a-112">Yüklemesi tamamlandığında, **Başlat** düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="c099a-112">When the install finishes, choose the **Launch** button.</span></span> 

## <a name="using-tracex"></a><span data-ttu-id="c099a-113">TraceX kullanma</span><span class="sxs-lookup"><span data-stu-id="c099a-113">Using TraceX</span></span>

<span data-ttu-id="c099a-114">TraceX 'in kullanılması, TraceX içinde bir izleme dosyası açmak kadar kolaydır!</span><span class="sxs-lookup"><span data-stu-id="c099a-114">Using TraceX is as easy as opening a trace file inside TraceX!</span></span> <span data-ttu-id="c099a-115">\***Start** _ düğmesini kullanarak tracex 'yi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="c099a-115">Run TraceX via the \***Start** _ button.</span></span> <span data-ttu-id="c099a-116">Bu noktada, TraceX grafik kullanıcı arabirimini (GUI) gözlemleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="c099a-116">At this point you will observe the TraceX graphic user interface (GUI).</span></span> <span data-ttu-id="c099a-117">Artık var olan bir hedef izleme arabelleğini grafik olarak görüntülemek için TraceX kullanmaya hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="c099a-117">You are now ready to use TraceX to graphically view an existing target trace buffer.</span></span> <span data-ttu-id="c099a-118">Bu, _ *_Dosya-> aç '_* a tıklayıp, ardından ikili izleme dosyasını girerek kolayca yapılır.</span><span class="sxs-lookup"><span data-stu-id="c099a-118">This is easily done by clicking _ *_File -> Open,_*\* then entering the binary trace file.</span></span>

>[!IMPORTANT]
><span data-ttu-id="c099a-119">*Ayrıca **, bir TRX** Uzantısı ile herhangi bir izleme dosyasına çift tıklayabilirsiniz ve bu da otomatik olarak tracex başlatılır.*</span><span class="sxs-lookup"><span data-stu-id="c099a-119">*You can also double-click on any trace file with an extension of **trx,** which will automatically launch TraceX.*</span></span>

![TraceX GUI 'nin ekran görüntüsü.](./media/user-guide/screen_shot_8.png)

<span data-ttu-id="c099a-121">**ŞEKIL 1**</span><span class="sxs-lookup"><span data-stu-id="c099a-121">**FIGURE 1**</span></span>

>[!IMPORTANT]
><span data-ttu-id="c099a-122">*Hedef üzerinde ThreadX kullanarak izleme arabellekleri oluşturma yönergeleri için **Bölüm 5** ' e başvurun.*</span><span class="sxs-lookup"><span data-stu-id="c099a-122">*Refer to **Chapter 5** for instructions on how to generate trace buffers on the target using ThreadX.*</span></span>

## <a name="tracex-examples"></a><span data-ttu-id="c099a-123">TraceX örnekleri</span><span class="sxs-lookup"><span data-stu-id="c099a-123">TraceX Examples</span></span>

<span data-ttu-id="c099a-124">TraceX uygulamasını ilk kez çalıştırdığınızda veya TraceX uygulaması güncelleştirilirken, TraceX örnek izleme dosyalarını ve custom_events. trxc dosyasını yerel makinenizde Kullanıcı tanımlı bir dizine yüklemeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="c099a-124">The first time you run the TraceX application, or when the TraceX application is updated, you will be prompted to install the TraceX example trace files and the custom_events.trxc file to a user-defined directory on your local machine.</span></span>

<span data-ttu-id="c099a-125">Bu yükleme adımı tamamlandıktan sonra, **TRX** uzantılı örnek izleme dosyaları, yükleme klasörünüzün **tracefiles** alt dizininde bulunur.</span><span class="sxs-lookup"><span data-stu-id="c099a-125">After this installation step in completed, the example trace files with the extension **trx** are found in the **TraceFiles** subdirectory of your installation folder.</span></span> <span data-ttu-id="c099a-126">Bu önceden oluşturulmuş örnekler, uygulamanızla birlikte çalışan ThreadX tarafından oluşturulan izleme arabelleklerinde TraceX kullanmaya rahat bir şekilde başlamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="c099a-126">These pre-built examples will help you get comfortable with using TraceX on the trace buffers generated by ThreadX running with your application.</span></span>

<span data-ttu-id="c099a-127">Her zaman bir örnek izleme dosyası, \***demo_threadx. trx** _ dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="c099a-127">One example trace file always present is the file \***demo_threadx.trx** _.</span></span> <span data-ttu-id="c099a-128">Bu örnek izleme dosyası, _ThreadX Kullanıcı Kılavuzu \* Bölüm 6 ' da açıklandığı gibi standart ThreadX tanıtımına yönelik yürütmeyi gösterir.</span><span class="sxs-lookup"><span data-stu-id="c099a-128">This example trace file shows the execution of the standard ThreadX demo, as described in Chapter 6 of the _ThreadX User Guide\*.</span></span>

![Trackingex içindeki açık iletişim kutusunun ekran görüntüsü.](./media/user-guide/screen_shot_9.png)

<span data-ttu-id="c099a-130">**ŞEKIL 2**</span><span class="sxs-lookup"><span data-stu-id="c099a-130">**FIGURE 2**</span></span>
