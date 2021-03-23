---
title: GUX Studio 'nun yüklenmesi ve kullanımı
description: Bu bölümde, Gux Studio UI sistem tasarımı aracının yüklenmesiyle, kurulumuyla ve kullanımıyla ilgili çeşitli sorunların açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: d7b5f94c26842b408ea1b00aeeb78e111bea3623
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104827167"
---
# <a name="chapter-2-installation-and-use-of-guix-studio"></a><span data-ttu-id="bb9ac-103">Bölüm 2: Gux Studio 'Yu yükleme ve kullanma</span><span class="sxs-lookup"><span data-stu-id="bb9ac-103">Chapter 2: Installation and Use of GUIX Studio</span></span>

<span data-ttu-id="bb9ac-104">Bu bölümde, Gux Studio UI sistem tasarımı aracının yüklenmesiyle, kurulumuyla ve kullanımıyla ilgili çeşitli sorunların açıklaması yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="bb9ac-104">This chapter contains a description of various issues related to installation, setup, and usage of the GUIX Studio UI system design tool.</span></span> 

## <a name="product-distribution"></a><span data-ttu-id="bb9ac-105">Ürün dağıtımı</span><span class="sxs-lookup"><span data-stu-id="bb9ac-105">Product Distribution</span></span>

<span data-ttu-id="bb9ac-106">GUX Studio uygulamasını, Gux Studio 'yu arayarak veya doğrudan [Gux Studio sayfasına](https://www.microsoft.com/p/azure-rtos-guix-studio/9pbm1k1r7q0f?activetab=pivot:overviewtab)giderek [Microsoft App Store](https://microsoft.com/store/apps) 'dan edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb9ac-106">You can obtain the GUIX Studio app from the [Microsoft App Store](https://microsoft.com/store/apps) by searching for GUIX Studio, or by going directly to [the GUIX Studio page](https://www.microsoft.com/p/azure-rtos-guix-studio/9pbm1k1r7q0f?activetab=pivot:overviewtab).</span></span> <span data-ttu-id="bb9ac-107">Ardından aşağıdakileri yapın.</span><span class="sxs-lookup"><span data-stu-id="bb9ac-107">Then do the following.</span></span>

1. <span data-ttu-id="bb9ac-108">Uygulama mağazasındaki Gux Studio sayfasında, Gux Studio 'Yu indirmek için **Al** veya **Yükle** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bb9ac-108">From the GUIX Studio page in the App Store, click the **Get** or **Install** button to download GUIX Studio.</span></span>

1. <span data-ttu-id="bb9ac-109">Tarayıcınız, aşağıdaki şekilde gösterildiği gibi Microsoft Store açmak isteyip istemediğinizi soran bir ileti görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="bb9ac-109">Your browser may display a message asking if you want to open the Microsoft Store, as shown in the figure below.</span></span> <span data-ttu-id="bb9ac-110">Varsa, **Aç** düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="bb9ac-110">If it does, choose the **Open** button.</span></span>
<span data-ttu-id="bb9ac-111">![GUX Studio 'Yu yüklemek için Aç ' ı seçin.](./media/guix-studio/open-ms-store.png)</span><span class="sxs-lookup"><span data-stu-id="bb9ac-111">![Choose Open to install GUIX Studio.](./media/guix-studio/open-ms-store.png)</span></span>

1. <span data-ttu-id="bb9ac-112">Yüklemesi tamamlandığında, **Başlat** düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="bb9ac-112">When the install finishes, choose the **Launch** button.</span></span>

1. <span data-ttu-id="bb9ac-113">GUX Studio ilk kez başlatıldığında, Gux deposunu yerel bilgisayarınıza kopyalamak isteyip istemediğinizi soran bir iletişim kutusu görüntüler.</span><span class="sxs-lookup"><span data-stu-id="bb9ac-113">The first time that GUIX Studio launches, it displays a dialog box asking if you want to clone the GUIX repo to your local computer.</span></span> <span data-ttu-id="bb9ac-114">Depoyu kopyalamayı seçebilirsiniz, depoyu zaten Klonladığınız yere işaret edebilir veya depoyu hiç kopyalamamanız tercih edebilirsiniz (Bu durumda, bilgisayarınızda bir örnek proje yüklü).</span><span class="sxs-lookup"><span data-stu-id="bb9ac-114">You can either choose to clone the repository, point to where you have already cloned the repo, or choose not to clone the repo at all (in which case, one example project is installed on your computer).</span></span>
<span data-ttu-id="bb9ac-115">![Depoyu kopyalamayı seçin, zaten kopyalanmış bir depoyu işaret edin veya atlayın.](./media/guix-studio/clone-repo.png)</span><span class="sxs-lookup"><span data-stu-id="bb9ac-115">![Choose to clone the repo, point to an already-cloned repo, or skip.](./media/guix-studio/clone-repo.png)</span></span>

> <span data-ttu-id="bb9ac-116">!</span><span class="sxs-lookup"><span data-stu-id="bb9ac-116">!</span></span>[!NOTE]
> <span data-ttu-id="bb9ac-117">Bu iletişim kutusuna, Gux Stuido ana menüsünden **Yapılandır** ' ı ve ardından **Gux deposu**' nu seçerek dilediğiniz zaman geri dönebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb9ac-117">You can return to this dialog box at any time by choosing **Configure** from the main menu of GUIX Stuido, followed by **GUIX Repository**.</span></span>

<span data-ttu-id="bb9ac-118">Başlangıç işlemi tamamlandıktan sonra, Gux Studio 'Yu kullanmaya hazırlanın.</span><span class="sxs-lookup"><span data-stu-id="bb9ac-118">After the startup process is finished, you will be ready to use GUIX Studio.</span></span>

## <a name="using-guix-studio"></a><span data-ttu-id="bb9ac-119">GUX Studio 'Yu kullanma</span><span class="sxs-lookup"><span data-stu-id="bb9ac-119">Using GUIX Studio</span></span>

<span data-ttu-id="bb9ac-120">GUX Studio 'Yu kullanmak kolay bir şekilde, "***Başlat***" düğmesi aracılığıyla Gux Studio 'yu çalıştırmak yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="bb9ac-120">Using GUIX Studio is easy - simply run GUIX Studio via the "***Start***" button.</span></span> <span data-ttu-id="bb9ac-121">Bu noktada, Gux Studio Kullanıcı arabirimini gözlemleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="bb9ac-121">At this point you will observe the GUIX Studio UI.</span></span> <span data-ttu-id="bb9ac-122">Artık, yerleşik kullanıcı arabirimini grafiksel olarak oluşturmak için Gux Studio 'Yu kullanmaya hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="bb9ac-122">You are now ready to use GUIX Studio to graphically create your embedded UI.</span></span> <span data-ttu-id="bb9ac-123">Buradan yeni bir proje oluşturursunuz veya Gux örnek projeleri de dahil olmak üzere mevcut bir projeyi açarsınız.</span><span class="sxs-lookup"><span data-stu-id="bb9ac-123">From here you create a new project or open an existing project, including the GUIX example projects.</span></span>

> [!NOTE]
> <span data-ttu-id="bb9ac-124">Ayrıca, "**GXP**" uzantılı bir Gux Studio proje dosyasına çift tıklayarak Gux Studio 'yu otomatik olarak başlatabilir ve başvurulan projeyi açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb9ac-124">You can also double-click on any GUIX Studio project file with an extension of "**gxp,**" which will automatically launch GUIX Studio and open the referenced project.</span></span>

## <a name="guix-studio-project-samples"></a><span data-ttu-id="bb9ac-125">GUX Studio proje örnekleri</span><span class="sxs-lookup"><span data-stu-id="bb9ac-125">GUIX Studio Project Samples</span></span>

<span data-ttu-id="bb9ac-126">"\***GXP**_"_ uzantısına sahip bir dizi örnek Gux Studio proje dosyası, yüklemenizin " \* _Samples_\* \*" alt dizininde bulunur.</span><span class="sxs-lookup"><span data-stu-id="bb9ac-126">A series of example GUIX Studio project files with the extension "\***gxp**_" are found in the "_\*_Samples_\*\*" sub-directory of your installation.</span></span> <span data-ttu-id="bb9ac-127">Önceden oluşturulmuş bu örnek projeler, Gux Studio 'Yu kullanmaya rahat bir şekilde başlamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="bb9ac-127">These pre-built example projects will help you get comfortable with using GUIX Studio.</span></span>

<span data-ttu-id="bb9ac-128">Her zaman bulunan örnek bir proje dosyası \***Samples/demo_guix_simple/guix_simple. GXP** _ dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="bb9ac-128">One example project file that is always present is the file \***samples/demo_guix_simple/guix_simple.gxp** _.</span></span> <span data-ttu-id="bb9ac-129">Bu örnek proje dosyası, bu belgenin _ *_Bölüm 7_*\* bölümünde açıklandığı gibi basıt bır GUıDX Kullanıcı arabirimi tanımını gösterir.</span><span class="sxs-lookup"><span data-stu-id="bb9ac-129">This example project file shows the definition of a simple GUIX UI, as described in _ *_Chapter 7_*\* of this document.</span></span>

![GUX Studio Kullanıcı arabiriminin ekran görüntüsü.](./media/guix-studio/image_10.png)

<span data-ttu-id="bb9ac-131">**Şekil 1**</span><span class="sxs-lookup"><span data-stu-id="bb9ac-131">**Figure 1**</span></span>

## <a name="keyboard-shortcuts"></a><span data-ttu-id="bb9ac-132">Klavye Kısayolları</span><span class="sxs-lookup"><span data-stu-id="bb9ac-132">Keyboard Shortcuts</span></span>

- <span data-ttu-id="bb9ac-133">**CTRL + N:** Yeni proje</span><span class="sxs-lookup"><span data-stu-id="bb9ac-133">**Ctrl + N:** New Project</span></span>
- <span data-ttu-id="bb9ac-134">**CTRL + O:** Projeyi aç</span><span class="sxs-lookup"><span data-stu-id="bb9ac-134">**Ctrl + O:** Open Project</span></span>
- <span data-ttu-id="bb9ac-135">**CTRL + S:** Projeyi Kaydet</span><span class="sxs-lookup"><span data-stu-id="bb9ac-135">**Ctrl + S:** Save Project</span></span>
- <span data-ttu-id="bb9ac-136">**CTRL + SHIFT + S:** Projeyi farklı kaydet</span><span class="sxs-lookup"><span data-stu-id="bb9ac-136">**Ctrl + Shift + S:** Save Project As</span></span>
- <span data-ttu-id="bb9ac-137">**Alt + F4:** Çıkıp</span><span class="sxs-lookup"><span data-stu-id="bb9ac-137">**Alt + F4:** Exit</span></span>
