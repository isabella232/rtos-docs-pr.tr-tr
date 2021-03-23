---
title: GUX Studio açıklaması
description: Bu bölüm, GUıDX Studio Sistem Analizi aracının bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 89bbcd51c22dddef6e420750e8c8805a66344335
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826369"
---
# <a name="chapter-3-description-of-guix-studio"></a><span data-ttu-id="a2f44-103">Bölüm 3: Gux Studio 'nun açıklaması</span><span class="sxs-lookup"><span data-stu-id="a2f44-103">Chapter 3: Description of GUIX Studio</span></span>

<span data-ttu-id="a2f44-104">Bu bölüm, GUıDX Studio Sistem Analizi aracının bir açıklamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="a2f44-104">This chapter contains a description of the GUIX Studio system analysis tool.</span></span> <span data-ttu-id="a2f44-105">Bu bölümde GUI 'nin Genel işlevselliğinin açıklaması bulunur.</span><span class="sxs-lookup"><span data-stu-id="a2f44-105">A description of the overall functionality of the GUI is found in this chapter.</span></span> 

## <a name="guix-studio-views"></a><span data-ttu-id="a2f44-106">GUX Studio görünümleri</span><span class="sxs-lookup"><span data-stu-id="a2f44-106">GUIX Studio Views</span></span>

<span data-ttu-id="a2f44-107">"**Toolbar** _, _*_proje görünümü_*_, _\*_Özellikler görünümü_*_, _*_hedef görünümü_*_ ve _*_kaynak görünümü_\*_ gibi, guıdx Studio Kullanıcı arabiriminin beş ana alanı vardır.</span><span class="sxs-lookup"><span data-stu-id="a2f44-107">There are five principal areas of the GUIX Studio UI, namely the ***Toolbar** _, _*_Project View_*_, _*_Properties View_*_, _*_Target View_*_, and _*_Resource View_\*_.</span></span> <span data-ttu-id="a2f44-108">_ *_Şekil 2_*\* temel Gux STUDIO Kullanıcı arabirimini gösterir.</span><span class="sxs-lookup"><span data-stu-id="a2f44-108">_ *_Figure 2_*\* shows the basic GUIX Studio UI.</span></span> <span data-ttu-id="a2f44-109">Görünümlerin her biri, aşağıdaki alt bölümlerde daha ayrıntılı bir şekilde ele alınmıştır.</span><span class="sxs-lookup"><span data-stu-id="a2f44-109">Each of the views is further discussed in the following sub-sections.</span></span>

![Temel Gux Studio Kullanıcı arabiriminin ekran görüntüsü.](./media/guix-studio/image_10.png)

<span data-ttu-id="a2f44-111">**Şekil 2**</span><span class="sxs-lookup"><span data-stu-id="a2f44-111">**Figure 2**</span></span>

### <a name="title"></a><span data-ttu-id="a2f44-112">Başlık</span><span class="sxs-lookup"><span data-stu-id="a2f44-112">Title</span></span>

- <span data-ttu-id="a2f44-113">GUX Studio 18: ***title** _, şu anda _ \*_Şekil 2_\** ' nin en üstünde gösterildiği gibi, açık projenin yanı sıra Gux Studio sürümünü de görüntüler.</span><span class="sxs-lookup"><span data-stu-id="a2f44-113">GUIX Studio 18: The ***Title** _ displays the GUIX Studio version as well as the currently open project, as shown at the top of _ *_Figure 2_** previously.</span></span>

### <a name="toolbar"></a><span data-ttu-id="a2f44-114">Araç Çubuğu</span><span class="sxs-lookup"><span data-stu-id="a2f44-114">Toolbar</span></span>

<span data-ttu-id="a2f44-115">\***Toolbar** _, _ \*_Şekil 3_\* \* ' de gösterildiği gibi, Gux Studio geliştiricisi için kullanılabilen düğmeleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="a2f44-115">The ***Toolbar** _ shows the buttons available to the GUIX Studio developer, as shown in _*_Figure 3_\*\*.</span></span>

![GUX Studio Toolbar 'ın ekran görüntüsü.](./media/guix-studio/image11.jpg)

<span data-ttu-id="a2f44-117">**Şekil 3**</span><span class="sxs-lookup"><span data-stu-id="a2f44-117">**Figure 3**</span></span>

<span data-ttu-id="a2f44-118">Araç çubuğu düğmeleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="a2f44-118">The toolbar buttons are defined as follows:</span></span>

![Yeni düğmesi](./media/guix-studio/new-button.png) <span data-ttu-id="a2f44-120">Yeni bir Gux Studio projesi oluşturur</span><span class="sxs-lookup"><span data-stu-id="a2f44-120">Creates a new GUIX Studio project</span></span>

![Aç düğmesi](./media/guix-studio/open-button.png) <span data-ttu-id="a2f44-122">Mevcut bir Gux Studio projesini açar</span><span class="sxs-lookup"><span data-stu-id="a2f44-122">Opens an existing GUIX Studio project</span></span>

![Kaydet düğmesi](./media/guix-studio/save-button.png) <span data-ttu-id="a2f44-124">Projeyi kaydeder</span><span class="sxs-lookup"><span data-stu-id="a2f44-124">Saves the project</span></span>

![Kes düğmesi](./media/guix-studio/cut-button.png) <span data-ttu-id="a2f44-126">Alt öğeleri içeren seçili pencere öğesini kes</span><span class="sxs-lookup"><span data-stu-id="a2f44-126">Cut widget selected, including children</span></span>

![Kopyala düğmesini](./media/guix-studio/copy-button.png) <span data-ttu-id="a2f44-128">Alt öğeler de dahil olmak üzere seçili pencere öğesini Kopyala</span><span class="sxs-lookup"><span data-stu-id="a2f44-128">Copy selected widget, including children</span></span>

![Yapıştır düğmesi](./media/guix-studio/paste-button.png) <span data-ttu-id="a2f44-130">Pencere öğesini ve alt öğeleri Yapıştır</span><span class="sxs-lookup"><span data-stu-id="a2f44-130">Paste widget and children</span></span>

![Sola Hizala düğmesi](./media/guix-studio/left-align-button.png) <span data-ttu-id="a2f44-132">Seçili pencere öğelerini Sola Hizala</span><span class="sxs-lookup"><span data-stu-id="a2f44-132">Left-align selected widgets</span></span>

![Sağa Hizala düğmesi](./media/guix-studio/right-align-button.png) <span data-ttu-id="a2f44-134">Seçili pencere öğelerini Sağa Hizala</span><span class="sxs-lookup"><span data-stu-id="a2f44-134">Right-align selected widgets</span></span>

![Üste Hizala düğmesi](./media/guix-studio/top-align-button.png) <span data-ttu-id="a2f44-136">Seçili pencere öğelerini Üste Hizala</span><span class="sxs-lookup"><span data-stu-id="a2f44-136">Top-align selected widgets</span></span>

![Alt hizalama düğmesi](./media/guix-studio/bottom-align-button.png) <span data-ttu-id="a2f44-138">Seçili pencere öğelerini Alta Hizala</span><span class="sxs-lookup"><span data-stu-id="a2f44-138">Bottom-align selected widgets</span></span>

![Dikey boşluk düğmesi](./media/guix-studio/space-vertically-button.png) <span data-ttu-id="a2f44-140">Seçilen pencere öğelerini dikey olarak eşit alan</span><span class="sxs-lookup"><span data-stu-id="a2f44-140">Equally space selected widgets vertically</span></span>

![Yatay boşluk düğmesi](./media/guix-studio/space-horizontally-button.png) <span data-ttu-id="a2f44-142">Seçilen pencere öğelerini yatay olarak eşit alan</span><span class="sxs-lookup"><span data-stu-id="a2f44-142">Equally space selected widgets horizontally</span></span>

![Eşit genişlik düğmesi](./media/guix-studio/equal-width-button.png) <span data-ttu-id="a2f44-144">Seçili pencere öğelerini eşit genişliğe getir</span><span class="sxs-lookup"><span data-stu-id="a2f44-144">Make selected widgets equal width</span></span>

![Eşit yükseklik düğmesi](./media/guix-studio/equal-height-button.png) <span data-ttu-id="a2f44-146">Seçili Pencere öğelerinin yüksekliğini eşit yap</span><span class="sxs-lookup"><span data-stu-id="a2f44-146">Make selected widgets equal height</span></span>

![Öne taşı düğmesi](./media/guix-studio/move-front-button.png) <span data-ttu-id="a2f44-148">Seçili pencere öğelerini öne taşı</span><span class="sxs-lookup"><span data-stu-id="a2f44-148">Move selected widgets to front</span></span>

![Geri taşı düğmesi](./media/guix-studio/move-back-button.png) <span data-ttu-id="a2f44-150">Seçili pencere öğelerini arkaya taşı</span><span class="sxs-lookup"><span data-stu-id="a2f44-150">Move selected widgets to back</span></span>

![Boyut düğmesi](./media/guix-studio/size-button.png) <span data-ttu-id="a2f44-152">Seçilen pencere öğesini içerik yakınlaştırma hedef ekranına Boyutlandır</span><span class="sxs-lookup"><span data-stu-id="a2f44-152">Size selected widget to content Zoom out target screen</span></span>

![Uzaklaştır düğmesi](./media/guix-studio/zoom-out-button.png) <span data-ttu-id="a2f44-154">Hedef ekranı uzaklaştır</span><span class="sxs-lookup"><span data-stu-id="a2f44-154">Zoom out target screen</span></span>

![Yakınlaştır düğmesi](./media/guix-studio/zoom-in-button.png) <span data-ttu-id="a2f44-156">Hedef ekranda Yakınlaştır</span><span class="sxs-lookup"><span data-stu-id="a2f44-156">Zoom in target screen</span></span>

![Kaydet düğmesi](./media/guix-studio/record-button.png) <span data-ttu-id="a2f44-158">Makroyu kaydet</span><span class="sxs-lookup"><span data-stu-id="a2f44-158">Record Macro</span></span>

![Kayıttan yürütme düğmesi](./media/guix-studio/playback-button.png) <span data-ttu-id="a2f44-160">Kayıttan yürütme makrosu</span><span class="sxs-lookup"><span data-stu-id="a2f44-160">Playback Macro</span></span>

![Çalıştır düğmesi](./media/guix-studio/run-button.png) <span data-ttu-id="a2f44-162">Uygulamayı çalıştır</span><span class="sxs-lookup"><span data-stu-id="a2f44-162">Run Application</span></span>

![Hakkında düğmesi](./media/guix-studio/about-button.png) <span data-ttu-id="a2f44-164">GUX Studio hakkında</span><span class="sxs-lookup"><span data-stu-id="a2f44-164">About GUIX Studio</span></span>

### <a name="project-view"></a><span data-ttu-id="a2f44-165">Proje görünümü</span><span class="sxs-lookup"><span data-stu-id="a2f44-165">Project View</span></span>

<span data-ttu-id="a2f44-166">\***Proje görünümü** _ ekli Kullanıcı arabirimini oluşturan hiyerarşik liste Gux nesnelerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="a2f44-166">The \***Project View** _ shows the hierarchical list GUIX objects that comprise the embedded UI.</span></span> <span data-ttu-id="a2f44-167">Yeni Gux nesneleri, üst nesneye tıklayıp _*_Ekle_*_ menüsünden bir nesne seçilerek (ya da nesneye sağ tıklayıp sağ tıklama menüsünden seçilerek) eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="a2f44-167">New GUIX objects can be added by clicking on the parent object and then selecting an object from the _*_Insert_*_ menu (or by right-clicking on the object and selecting from the right-click menu).</span></span> <span data-ttu-id="a2f44-168">Aşağıdaki _\*_Şekil 4_\*_ ' te Gux Studio _ *_proje görünümü_* \* gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="a2f44-168">_*_Figure 4_*_ below shows the GUIX Studio _\*_Project View_\*\*.</span></span>

![GUX Studio proje görünümünün ekran görüntüsü.](./media/guix-studio/image_35.png)

<span data-ttu-id="a2f44-170">**Şekil 4**</span><span class="sxs-lookup"><span data-stu-id="a2f44-170">**Figure 4**</span></span>

### <a name="properties-view"></a><span data-ttu-id="a2f44-171">Özellikler Görünümü</span><span class="sxs-lookup"><span data-stu-id="a2f44-171">Properties View</span></span>

<span data-ttu-id="a2f44-172">***Özellikler Görünümü** _, şu anda seçili olan Gux nesnesinin ayrıntılı özellik bilgilerini gösterir. Bu, _*_proje görünümü_*_ aracılığıyla veya _*_hedef görünümdeki_\*_ nesneye doğrudan tıklanarak seçilebilir.</span><span class="sxs-lookup"><span data-stu-id="a2f44-172">The ***Properties View** _ shows detailed property information of the currently selected GUIX object, which can be selected via the _*_Project View_*_ or by clicking directly on the object in the _*_Target View_\*_.</span></span> <span data-ttu-id="a2f44-173">Aşağıdaki _\*_Şekil 5_\*_ ' te Gux Studio _ *_Özellikler Görünümü_* \* gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="a2f44-173">_*_Figure 5_*_ below shows the GUIX Studio _\*_Properties View_\*\*.</span></span>

![GUX Studio özellikleri görünümünün ekran görüntüsü.](./media/guix-studio/image36.jpg)

<span data-ttu-id="a2f44-175">**Şekil 5**</span><span class="sxs-lookup"><span data-stu-id="a2f44-175">**Figure 5**</span></span>

### <a name="target-view"></a><span data-ttu-id="a2f44-176">Hedef görünüm</span><span class="sxs-lookup"><span data-stu-id="a2f44-176">Target View</span></span>

<span data-ttu-id="a2f44-177">\***Target View** _, WYSIWYG ekran tasarımı ve düzen alanıdır.</span><span class="sxs-lookup"><span data-stu-id="a2f44-177">The \***Target View** _ is the WYSIWYG screen design and layout area.</span></span> <span data-ttu-id="a2f44-178">Bu görünüm, hedef donanımınızın fiziksel görüntüsünü veya görüntülenmesini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="a2f44-178">This view is meant to represent the physical display or displays available on your target hardware.</span></span> <span data-ttu-id="a2f44-179">Nesneler, basit fare işlemleri aracılığıyla seçilebilir, taşınabilir, yeniden boyutlandırılabilir, vb. olabilir.</span><span class="sxs-lookup"><span data-stu-id="a2f44-179">Objects can be selected, moved, resized, etc. via simple mouse operations.</span></span> <span data-ttu-id="a2f44-180">Ayrıca, hizalama ve Z düzeni düğme işlemleri hedef görünümdeki seçili nesneler üzerinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a2f44-180">In addition, alignment and Z-order button operations are available on selected objects in the Target View.</span></span> <span data-ttu-id="a2f44-181">_*_Hedef görünümde_*_ bir nesnenin seçilmesi, bu nesnenin Özellikler _*_görünümünde_*_ görüntülenmesine neden olur.</span><span class="sxs-lookup"><span data-stu-id="a2f44-181">Selecting an object in the _*_Target View_*_ will also result in the properties for that object to be displayed in the _*_Properties View_*_.</span></span> <span data-ttu-id="a2f44-182">Aşağıdaki _\*_Şekil 6_\*_ ' da Gux Studio _ *_hedef görünümü_* \* gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="a2f44-182">_*_Figure 6_*_ below shows the GUIX Studio _\*_Target View_\*\*.</span></span>

![GUX Studio hedef görünümünün ekran görüntüsü.](./media/guix-studio/image_37.png)

<span data-ttu-id="a2f44-184">**Şekil 6**</span><span class="sxs-lookup"><span data-stu-id="a2f44-184">**Figure 6**</span></span>

### <a name="resource-view"></a><span data-ttu-id="a2f44-185">Kaynak Görünümü</span><span class="sxs-lookup"><span data-stu-id="a2f44-185">Resource View</span></span>

<span data-ttu-id="a2f44-186">\***Kaynak görünümü** _, her bir ekran için tanımlanan uygulama ekranları için kullanılabilir kaynakları (renkler, yazı tipleri, pixelharitalar ve dizeler) yönetmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a2f44-186">The \***Resource View** _ is used to manage the resources (colors, fonts, pixelmaps, and strings) available to applications screens defined for each display.</span></span> <span data-ttu-id="a2f44-187">Kaynak görünümü grup üst bilgilerine tıklayarak her bir grubu genişletebilir ve grup içeriğini inceleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2f44-187">You can click on the resource view group headers to expand each group and examine the group contents.</span></span> <span data-ttu-id="a2f44-188">Aşağıdaki _\*_Şekil 7 '_\*_ de Gux Studio _ *_kaynak görünümü_* \* gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="a2f44-188">_*_Figure 7_*_ below shows the GUIX Studio _\*_Resource View_\*\*.</span></span>

![GUX Studio Kaynak Görünümü ekran görüntüsü.](./media/guix-studio/image38.jpg)

<span data-ttu-id="a2f44-190">**Şekil 7**</span><span class="sxs-lookup"><span data-stu-id="a2f44-190">**Figure 7**</span></span>

<span data-ttu-id="a2f44-191">Kaynak gruplarının başlığı geçerli tema adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="a2f44-191">The title of the resource groups indicates current theme name.</span></span> <span data-ttu-id="a2f44-192">Çoklu Temalar varsa, yukarı ve aşağı oka tıklayarak Temalar arasında geçiş yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2f44-192">If multi themes available, you are able to switch between themes by clicking on the up and down arrow.</span></span>

<span data-ttu-id="a2f44-193">Yukarıdaki görünümde bulunan her kaynak grubu grup üstbilgisine tıklanarak genişletilebilir veya daraltılabilirler.</span><span class="sxs-lookup"><span data-stu-id="a2f44-193">Each resource group in the view above can be expanded or collapsed by clicking on the group header.</span></span> <span data-ttu-id="a2f44-194">Bir sonraki bölümde, her bir kaynak grubunun daha ayrıntılı bir açıklaması aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="a2f44-194">A more detailed description of each resource groups follows in the next chapter.</span></span>

## <a name="the-guix-studio-project"></a><span data-ttu-id="a2f44-195">GUX Studio projesi</span><span class="sxs-lookup"><span data-stu-id="a2f44-195">The GUIX Studio Project</span></span>

<span data-ttu-id="a2f44-196">Bir Gux Studio projesi, UI ekran tasarımı ve UI kaynakları hakkındaki bilgileri saklar.</span><span class="sxs-lookup"><span data-stu-id="a2f44-196">A GUIX Studio project maintains information about your UI screen design and UI resources.</span></span> <span data-ttu-id="a2f44-197">Proje verileri, uzantısı "olan bir XML biçimi dosyasına kaydedilir. ***GXP***".</span><span class="sxs-lookup"><span data-stu-id="a2f44-197">The project data is saved to an XML format file with the extension ".***gxp***".</span></span> <span data-ttu-id="a2f44-198">Proje dosyası bir XML şema dosyası olduğundan, sürümü oluşturulmuş ve diğer herhangi bir kaynak dosyayla benzer şekilde paylaşılabilir.</span><span class="sxs-lookup"><span data-stu-id="a2f44-198">Since the project file is an XML schema file, it can be versioned controlled and shared similar to any other source file.</span></span>

<span data-ttu-id="a2f44-199">GUX Studio 'Yu kullanmaya ilk kez başladığınızda, dağıtımla birlikte sunulan örnek projelerden birini açmanız veya yeni bir proje oluşturmanız gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="a2f44-199">When you first start using GUIX Studio, you will need to either open one of the example projects provided with the distribution or create a new project.</span></span> <span data-ttu-id="a2f44-200">Tüm çalışmanız proje veri dosyasına kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="a2f44-200">All of your work is saved to the project data file.</span></span>

<span data-ttu-id="a2f44-201">GUX Studio Ayrıca ANSI C kaynak dosyaları da üretir.</span><span class="sxs-lookup"><span data-stu-id="a2f44-201">GUIX Studio also produces ANSI C source files.</span></span> <span data-ttu-id="a2f44-202">Bu kaynak dosyalar, tasarlanan ekranları açıklayan uygulama kaynaklarınızı ya da veri yapılarını içerir.</span><span class="sxs-lookup"><span data-stu-id="a2f44-202">These source files contain either your application resources or data structures describing your designed screens.</span></span> <span data-ttu-id="a2f44-203">GUX Studio Ayrıca, uygulama ekranlarınızı dinamik olarak oluşturmak için oluşturulan veri yapılarını kullanmayı bildiğiniz bu oluşturulmuş kaynak dosyaları API işlevlerine yazar.</span><span class="sxs-lookup"><span data-stu-id="a2f44-203">GUIX Studio also writes to these generated source files API functions that know to utilize the generated data structures to dynamically create your application screens.</span></span> <span data-ttu-id="a2f44-204">Uygulama yazılımınız, Gux Studio içinde tasarladığınız ekranları oluşturmak için yalnızca belirtilen API işlevlerini çağırır.</span><span class="sxs-lookup"><span data-stu-id="a2f44-204">Your application software will simply invoke the provided API functions to create the screens you have designed within GUIX Studio.</span></span>

<span data-ttu-id="a2f44-205">Kullanıcı arabiriminizi tasarlarken ilerlemeniz durumunda, tasarladığınız arabirimi derleyip çalıştırmanıza imkan tanıyan Gux uyumlu çıkış dosyalarını oluşturmak için düzenli aralıklarla Gux Studio 'Yu kullanmak isteyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="a2f44-205">As you progress in designing your user interface, you will periodically want to use GUIX Studio to generate the GUIX compatible output files that will allow you to build and run the interface you have designed.</span></span> <span data-ttu-id="a2f44-206">Hedef donanımınız ya da Windows masaüstünüzde, ThreadX ve GUıDX benzetimi yapan kaynak dosyaları derleyip çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2f44-206">You can compile and run the generated source files for either your target hardware or on your Windows desktop that simulates ThreadX and GUIX.</span></span>

## <a name="guix-studio-project-organization"></a><span data-ttu-id="a2f44-207">GUX Studio Proje organizasyonu</span><span class="sxs-lookup"><span data-stu-id="a2f44-207">GUIX Studio Project Organization</span></span>

<span data-ttu-id="a2f44-208">GUX Studio 'nun nasıl etkin bir şekilde kullanıldığını ve Gux Studio IDE 'nin Proje görünümünde sunulan bilgileri anlamayı anlamak için, bir Gux Studio projesinin temel organizasyonu hakkında bilgi sahibi olmanız faydalı olur.</span><span class="sxs-lookup"><span data-stu-id="a2f44-208">It is helpful to have some knowledge of the basic organization of a GUIX Studio project to understand how to use GUIX Studio effectively and to understand the information presented in the Project View of the GUIX Studio IDE.</span></span> <span data-ttu-id="a2f44-209">Proje görünümü, projenizde bulunan tüm bilgilerin Özet görsel gösterimidir.</span><span class="sxs-lookup"><span data-stu-id="a2f44-209">The Project View is a summary visual representation of all of the information contained in your project.</span></span>

<span data-ttu-id="a2f44-210">Projeyi açıklamadan önce, birkaç terim tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a2f44-210">Before describing the project, it is necessary to define few terms.</span></span> <span data-ttu-id="a2f44-211">İlk olarak, **görüntü** terimi fiziksel bir görüntüleme cihazının anlamı olacak şekilde kullanıyoruz.</span><span class="sxs-lookup"><span data-stu-id="a2f44-211">First, we use the term **Display** to mean a physical display device.</span></span> <span data-ttu-id="a2f44-212">Bu çoğunlukla bir LCD görüntü aygıtıdır, ancak diğer teknolojiyi kullanıyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="a2f44-212">This is most often an LCD display device but it could be using other technology.</span></span> <span data-ttu-id="a2f44-213">Bir sonraki terim, en üst düzey bir Gux nesnesi olan, genellikle bir Gux penceresi ve ilişkili alt öğelerinden oluşan bir **ekrandır**.</span><span class="sxs-lookup"><span data-stu-id="a2f44-213">The next term is **Screen**, which mean a top-level GUIX object, usually a GUIX Window, and all of its associated child elements.</span></span> <span data-ttu-id="a2f44-214">Ekran, çalışma zamanında tanımlanabilen ve değiştirilebilen bir yazılım yapısıdır.</span><span class="sxs-lookup"><span data-stu-id="a2f44-214">A Screen is a software construct that can be defined and modified at runtime.</span></span> <span data-ttu-id="a2f44-215">Son olarak, bir **Tema** kaynak koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="a2f44-215">Finally, a **Theme** is a collection of resources.</span></span> <span data-ttu-id="a2f44-216">Bir tema, birlikte iyi çalışmak ve son kullanıcıyı tutarlı bir görünüm ile sunmak için tasarlanan renk tanımları, yazı tipi tanımları ve pixelmap tanımlarının bir tablosunu içerir.</span><span class="sxs-lookup"><span data-stu-id="a2f44-216">A theme includes a table of color definitions, font definitions, and pixelmap definitions that are designed to work well together and present your end user with a consistent look and feel.</span></span>

<span data-ttu-id="a2f44-217">Bu proje, proje adı, desteklenen ekran sayısı, her bir ekran için çözünürlük ve renk biçimi, desteklenen dillerin sayısı ve desteklenen her dilin adı gibi bir genel bilgiler kümesi içerir.</span><span class="sxs-lookup"><span data-stu-id="a2f44-217">The project first includes a set of global information such as the project name, number of displays supported, the resolution and color format of each display, the number of languages supported, the name of each supported language.</span></span> <span data-ttu-id="a2f44-218">Proje adı, Proje görünümünde görünen ilk düğümdür.</span><span class="sxs-lookup"><span data-stu-id="a2f44-218">The project name is the first node displayed in the Project View.</span></span>

<span data-ttu-id="a2f44-219">Ardından Proje, 4 fiziksel ekran için gereken tüm bilgileri ve her bir ekran için kullanılabilen ekranları ve kaynakları düzenler.</span><span class="sxs-lookup"><span data-stu-id="a2f44-219">The project next organizes all of the information required for up to 4 physical displays and the screens and resources available to each display.</span></span> <span data-ttu-id="a2f44-220">Görünen adlar proje görünüm ağacındaki bir sonraki düzey düğümlerdir.</span><span class="sxs-lookup"><span data-stu-id="a2f44-220">The display names are the next level nodes in the Project View tree.</span></span>

<span data-ttu-id="a2f44-221">GUX Studio uygulamasının benzersiz bir özelliği, her biri kendi x, y çözünürlüğü, renk biçimi, ekranları ve kaynakları olan birden çok fiziksel ekran için yerleşik desteğe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="a2f44-221">A unique feature of the GUIX Studio application is built-in support for multiple physical displays, each with its own x,y resolution, color format, screens, and resources.</span></span> <span data-ttu-id="a2f44-222">GUX uygulamalarının büyük çoğunluğu yalnızca bir fiziksel görüntü kullanır, ancak bu özellik, birden çok eş zamanlı fiziksel ekranı desteklemesi gereken bir ürünü oluşturmak için önemlidir.</span><span class="sxs-lookup"><span data-stu-id="a2f44-222">While the vast majority of GUIX applications utilize only one physical display, this capability is important for those making a product that must support multiple simultaneous physical displays.</span></span>

<span data-ttu-id="a2f44-223">Her bir görüntüleme tanımının altında, bu ekran için tanımlanan en üst düzey pencereler veya ekranlar bulunur.</span><span class="sxs-lookup"><span data-stu-id="a2f44-223">Beneath each display definition are the top-level windows or screens defined for that display.</span></span> <span data-ttu-id="a2f44-224">Ekran tanımları, her ekranda alt pencere öğelerinin sayısına ve iç içe olmasına bağlı olarak herhangi bir düzeye yuvalanmış olabilir.</span><span class="sxs-lookup"><span data-stu-id="a2f44-224">The screen definitions can be nested to any level depending on the number and nesting of child widgets on each screen.</span></span>

<span data-ttu-id="a2f44-225">Bu ekran ve alt pencere öğesi organizasyonu Proje görünümünde grafiksel bir şekilde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="a2f44-225">This screen and child widget organization is displayed in a graphical manner in the Project View.</span></span>

<span data-ttu-id="a2f44-226">Her bir ekran ile ilişkili Temalar, görüntüleme tarafından desteklenen temalardır ve her temayı oluşturan kaynak içeridir.</span><span class="sxs-lookup"><span data-stu-id="a2f44-226">Also associated with each display are the Themes supported by the display and the resource content composing each Theme.</span></span> <span data-ttu-id="a2f44-227">Projenizde birden çok ekran varsa, bir ekran ve sonra başka bir görüntü seçtiğinizde Kaynak Görünümü içeriğini değiştirdiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="a2f44-227">If your project includes multiple displays, you will notice that the Resource View changes its content when you select one display and then another.</span></span> <span data-ttu-id="a2f44-228">Bunun nedeni, kaynak içeriğinin her bir görüntüleme ile bağlantılı olmasından kaynaklanır.</span><span class="sxs-lookup"><span data-stu-id="a2f44-228">This is because the resource content is linked to each display.</span></span> <span data-ttu-id="a2f44-229">Yalnızca renk biçimi farklı olabilir, ancak kullanmayı seçtiğiniz pixelmaps, renkler ve yazı tipleri bir fiziksel görüntü ile diğerine farklılık gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="a2f44-229">Not only the color format may be different, but the pixelmaps, colors, and fonts you choose to use may vary from one physical display to another.</span></span>

<span data-ttu-id="a2f44-230">Proje tarafından tutulan son bileşen, her bir ekran ile ilişkili dize tablosu verileri olur.</span><span class="sxs-lookup"><span data-stu-id="a2f44-230">The final component maintained by the project is the string table data associated with each display.</span></span> <span data-ttu-id="a2f44-231">Ekranlar çok farklı x ve y çözünürlüklerine sahip olduğundan, dize verileri projede tanımlanan her bir ekran için bağımsız olarak korunur.</span><span class="sxs-lookup"><span data-stu-id="a2f44-231">Since displays can be of very different x,y resolutions, the string data is maintained independently for each display defined in the project.</span></span>
