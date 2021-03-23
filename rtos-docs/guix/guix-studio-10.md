---
title: Basit örnek proje
description: Bu bölümde, GUıDX Studio 'da örnek projenin nasıl oluşturulduğu ve Gux üzerinde örnek yürütülmesi açıklanmaktadır.
author: jdeere5220
ms.author: kemaxwel
ms.date: 9/30/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 3661396f097e0ed7bd872fae01a7bec9212001b9
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826428"
---
# <a name="chapter-10-example-project"></a><span data-ttu-id="dced1-103">Bölüm 10: örnek proje</span><span class="sxs-lookup"><span data-stu-id="dced1-103">Chapter 10: Example Project</span></span>

<span data-ttu-id="dced1-104">Bu bölümde, GUıDX Studio 'da örnek projenin nasıl oluşturulduğu ve Gux üzerinde örnek yürütülmesi açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="dced1-104">This chapter describes how to create an example project in GUIX Studio and execute the example on GUIX.</span></span>

## <a name="create-new-project"></a><span data-ttu-id="dced1-105">Yeni Proje Oluştur</span><span class="sxs-lookup"><span data-stu-id="dced1-105">Create New Project</span></span>

<span data-ttu-id="dced1-106">İlk adım yeni bir proje oluşturuyor ve projenin destekleyeceği ekranları ve dilleri yapılandırıyor.</span><span class="sxs-lookup"><span data-stu-id="dced1-106">The first step is creating a new project and configuring the displays and languages that the project will support.</span></span> <span data-ttu-id="dced1-107">GUX Studio 'Yu ilk kez başlattığınızda, ***son projeler*** ekranını görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="dced1-107">When you first start GUIX Studio, you will see the ***Recent Projects*** screen:</span></span>

![GUX Studio son projeler iletişim kutusunun ekran görüntüsü.](./media/guix-studio/recent_projects.png)

<span data-ttu-id="dced1-109">**Şekil 10,1**</span><span class="sxs-lookup"><span data-stu-id="dced1-109">**Figure 10.1**</span></span>

<span data-ttu-id="dced1-110">\***Yeni proje oluştur** _... öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="dced1-110">Click on the \***Create New Project** _…</span></span> <span data-ttu-id="dced1-111">düğmesini başlatın.</span><span class="sxs-lookup"><span data-stu-id="dced1-111">button to begin a new project.</span></span> <span data-ttu-id="dced1-112">Burada gösterilen _ *_New GUıDX projesi_*\* iletişim kutusu görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="dced1-112">You will be presented with the _ *_New GUIX Project_*\* dialog, shown here:</span></span>

![GUX Studio yeni proje oluştur iletişim kutusunun ekran görüntüsü.](./media/guix-studio/create_new_project.png)

<span data-ttu-id="dced1-114">**Şekil 10,2**</span><span class="sxs-lookup"><span data-stu-id="dced1-114">**Figure 10.2**</span></span>

<span data-ttu-id="dced1-115">Proje adı olarak "***new_example***" adını yazın.</span><span class="sxs-lookup"><span data-stu-id="dced1-115">Type the name "***new_example***" as the project name.</span></span> <span data-ttu-id="dced1-116">Proje adları, standart C değişken adlandırma kuralları, yani özel veya ayrılmış karakter kullanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="dced1-116">Project names should use standard C variable naming rules, that is, no special or reserved characters.</span></span> <span data-ttu-id="dced1-117">Projenin kaydedileceği konumun yolunu yazın.</span><span class="sxs-lookup"><span data-stu-id="dced1-117">Type the path to the location where the project should be saved.</span></span> <span data-ttu-id="dced1-118">Yolun geçerli bir dosya sistemi dizini olması gerekir, diğer bir deyişle, yoksa Gux Studio dizini oluşturmaz.</span><span class="sxs-lookup"><span data-stu-id="dced1-118">The path must be a valid file system directory, that is, GUIX Studio will not create the directory if it does not exist.</span></span> <span data-ttu-id="dced1-119">Projeyi oluşturmak için "Tamam" a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="dced1-119">Click "OK" to create the project.</span></span>

<span data-ttu-id="dced1-120">Gösterilen sonraki ekran, burada gösterilen proje yapılandırma ekranıdır:</span><span class="sxs-lookup"><span data-stu-id="dced1-120">The next screen shown is the Project Configuration screen, shown here:</span></span>

![GUX Studio proje yapılandırma iletişim kutusunun ekran görüntüsü.](./media/guix-studio/config_new_project.png)

<span data-ttu-id="dced1-122">**Şekil 10,3**</span><span class="sxs-lookup"><span data-stu-id="dced1-122">**Figure 10.3**</span></span>

<span data-ttu-id="dced1-123">Bu iletişim kutusu, projenizin kaç tane görüntülediğini belirtmenizi ve her bir görüntü için bir ad vermenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="dced1-123">This dialog allows you to specify how many displays your project will support, and give a name to each display.</span></span> <span data-ttu-id="dced1-124">Her bir ekran tarafından desteklenen renk biçimini belirtmeniz gerekir ve isteğe bağlı olarak her bir ekran için Studio tarafından oluşturulan çıkış dosyaları için bir yol adı yazın.</span><span class="sxs-lookup"><span data-stu-id="dced1-124">You must specify the color format supported by each display, and optionally type a pathname for the output files generated by Studio for each display.</span></span> <span data-ttu-id="dced1-125">Çıkış dosyaları için varsayılan dizin "***. \\***", yani C çıktı dosyaları projenin kendisiyle aynı dizine yazılır.</span><span class="sxs-lookup"><span data-stu-id="dced1-125">The default directory for the output files is "***.\\***", meaning the C output files are written to the same directory as the project itself.</span></span>

<span data-ttu-id="dced1-126">Bu örnekte, \* ekran **sayısı** _ ' i "1" olarak ayarlayın, görünen ad alanına "_*_main_display_*_" adını yazın ve "_*_tuval belleğini ayır_*_" seçeneğini işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="dced1-126">For this example, leave the ***Number of Displays** _ set to "1", type the name "_*_main_display_*_" in the display name field, and check "_*_allocate canvas memory_\*_".</span></span> <span data-ttu-id="dced1-127">Çözümleme, renk biçimi ve dizin alanlarını varsayılan değerlerinde bırakın ve _ *_Tamam_* \* öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="dced1-127">Leave the resolution, color format, and directory fields at their default values, and click _\*_OK_\*\*.</span></span>

<span data-ttu-id="dced1-128">Artık Şekil 10,4 ' de gösterildiği gibi, projenizi Studio IDE ile açık olarak görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="dced1-128">You should now see your project open with the Studio IDE, as shown in figure 10.4:</span></span>

![Studio IDE ile açılmış projenin ekran görüntüsü.](./media/guix-studio/initial_screen.png)

<span data-ttu-id="dced1-130">**Şekil 10,4**</span><span class="sxs-lookup"><span data-stu-id="dced1-130">**Figure 10.4**</span></span>

<span data-ttu-id="dced1-131">Yeni bir proje oluşturduğunuzda, GUıDX Studio otomatik olarak projeniz için başlangıç noktası olarak varsayılan bir pencere oluşturur.</span><span class="sxs-lookup"><span data-stu-id="dced1-131">When you create a new project, GUIX Studio automatically creates a default window as the starting point for your project.</span></span> <span data-ttu-id="dced1-132">Bu gri kutu, sizin için oluşturulan varsayılan pencere, *hedef görünüm* içinde ortalandı.</span><span class="sxs-lookup"><span data-stu-id="dced1-132">This gray box is the default window created for you, centered within the *Target View*.</span></span>

<span data-ttu-id="dced1-133">Bu pencere seçili değilse, pencerenin çevresine kesikli seçim kutusu çizilmek üzere pencereye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="dced1-133">If this window is not selected, click on the window so that the dashed selection box is drawn around the window.</span></span> <span data-ttu-id="dced1-134">Şimdi ***Özellikler Görünümü** _ ' de, _*_pencere öğesi adı_*_, _*_pencere öğesi kimliği_*_, _*_sol_*_, _*_üst_*_, _*_Genişlik_*_, _*_Yükseklik_*_ ve _ *_Border_** öğesini aşağıda gösterilen ayarlarla eşleşecek şekilde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="dced1-134">Now in the ***Properties View** _, change the _*_Widget Name_*_, _*_Widget Id_*_, _*_Left_*_, _*_Top_*_, _*_Width_*_, _*_Height_*_, and _ *_Border_** to match those settings shown below.</span></span> <span data-ttu-id="dced1-135">Bu değişiklikleri yaparken, değişikliklerinizin hedef görünümde hemen etkili olduğunu görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="dced1-135">As you make these changes, you should see your changes immediately taking effect within the Target View.</span></span>

![Özellikler Görünümü iletişim kutusunun ekran görüntüsü.](./media/guix-studio/initial_window_properties.png)

<span data-ttu-id="dced1-137">**Şekil 10,5**</span><span class="sxs-lookup"><span data-stu-id="dced1-137">**Figure 10.5**</span></span>

<span data-ttu-id="dced1-138">Bir sonraki adımda, bir \***GX_ICON** _ pencere öğesi içinde kullanılacak bir pixelmap kaynağı ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="dced1-138">Next we will add a pixelmap resource to be used within a \***GX_ICON** _ widget.</span></span> <span data-ttu-id="dced1-139">Bu örnekte ince çalışacak şekilde Gux Studio dağıtımlarınız ile çeşitli simgeler sağlanır.</span><span class="sxs-lookup"><span data-stu-id="dced1-139">Several icons are provided with your GUIX Studio distribution that will work fine for this example.</span></span> <span data-ttu-id="dced1-140">_*_Pixelmaps_*_ kaynak görünümü genişletin ve _ *_Yeni pixelmap Ekle_*\* düğmesine tıklayın:</span><span class="sxs-lookup"><span data-stu-id="dced1-140">Expand your _*_Pixelmaps_*_ Resource View and click the _ *_Add New Pixelmap_*\* button:</span></span>

![Yeni pixelmap Ekle düğmesinin ekran görüntüsü.](./media/guix-studio/image74.jpg)

<span data-ttu-id="dced1-142">GUX Studio yükleme klasörünüze gidin ve ***./Graphics/simgeler** _ klasörü içinde _*_i_history_lg.png_\*_ adlı dosyayı seçin.</span><span class="sxs-lookup"><span data-stu-id="dced1-142">Browse to your GUIX Studio installation folder, and within the ***./graphics/icons** _ folder select the file named _*_i_history_lg.png_\*_.</span></span> <span data-ttu-id="dced1-143">Bu kaynağı projenize eklemek için _*_Aç_*_ ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="dced1-143">Click _*_Open_*_ to add this resource to your project.</span></span> <span data-ttu-id="dced1-144">_ *_Pixelmaps_*\* kaynak görünümü artık yeni eklenen simge görüntüsünün önizlemesini göstermelidir:</span><span class="sxs-lookup"><span data-stu-id="dced1-144">Your _ *_Pixelmaps_*\* Resource View should now show a preview of the newly added icon image:</span></span>

![Pixelmaps Kaynak Görünümü ekran görüntüsü.](./media/guix-studio/example_add_pixelmap.png)

<span data-ttu-id="dced1-146">**Şekil 10,6**</span><span class="sxs-lookup"><span data-stu-id="dced1-146">**Figure 10.6**</span></span>

<span data-ttu-id="dced1-147">Bu yeni görüntü kaynağını daha sonra UI tasarımımızın bir parçası olarak kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="dced1-147">We will use this new image resource later as part of our UI design.</span></span>

<span data-ttu-id="dced1-148">Bir pixelmap kaynağı eklemeye benzer şekilde, bu yazı tipini tasarımımızda daha sonra kullanabilmemiz için araç kutusu 'na yeni bir yazı tipi kaynağı ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="dced1-148">Similar to adding a pixelmap resource, we will add a new font resource to our toolbox so that we can use this font later in our design.</span></span> <span data-ttu-id="dced1-149">***Fonts** _ kaynak görünümü genişletin ve _*_Yeni yazı tipi Ekle_\*_ düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="dced1-149">Expand the ***Fonts** _ Resource View and click on the _*_Add New Font_\*_ button.</span></span> <span data-ttu-id="dced1-150">Bu eylem, yazı tipi _*_Ekle/Düzenle_*_ iletişim kutusunu çağırır.</span><span class="sxs-lookup"><span data-stu-id="dced1-150">This action will invoke the _*_Add/Edit_*_ font dialog.</span></span> <span data-ttu-id="dced1-151">Ardından, Gux Studio yükleme klasöründe sunulan Gux yazı tiplerine gidin _\*_ . \\ yazı tipleri \\ _ verasans_ ve _ _veraıt. ttf_*adlı TrueType yazı tipi dosyasını seçin\*\*_._* Yazı tipi adı alanına "_MEDIUM_ITALIC_*_"_* yazı tipini yazın ve yükseklik alanına "_30_\* \*" yazın.</span><span class="sxs-lookup"><span data-stu-id="dced1-151">Next, browse to the supplied GUIX fonts in the GUIX Studio installation folder, _\*_.\\fonts\\verasans_ *_, and select the TrueType font file named _*_VeraIt.ttf_*_. Type font the font name "_*_MEDIUM_ITALIC_*_" in the font name field, and type "_*_30_\*\*" in the height field.</span></span> <span data-ttu-id="dced1-152">İletişim kutusu artık şöyle görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="dced1-152">Your dialog should now look like this:</span></span>

![Yazı tipi düzenleme iletişim kutusunun ekran görüntüsü.](./media/guix-studio/example_add_font.png)

<span data-ttu-id="dced1-154">**Şekil 10,7**</span><span class="sxs-lookup"><span data-stu-id="dced1-154">**Figure 10.7**</span></span>

<span data-ttu-id="dced1-155">Bu yazı tipini projenize eklemek için ***Tamam*** ' ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="dced1-155">Click ***OK*** to add this font to your project.</span></span> <span data-ttu-id="dced1-156">Artık Kaynak Görünümü yazı tipini görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="dced1-156">You should now see the font in your Resource View:</span></span>

![Kaynak Görünümü yazı tiplerinin ekran görüntüsü.](./media/guix-studio/example_font_added.png)

<span data-ttu-id="dced1-158">**Şekil 10,8**</span><span class="sxs-lookup"><span data-stu-id="dced1-158">**Figure 10.8**</span></span>

<span data-ttu-id="dced1-159">Bu yeni yazı tipini, Kullanıcı arabirimi tasarımımızda daha sonra kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="dced1-159">We will use this new font later in our UI design.</span></span>

<span data-ttu-id="dced1-160">Artık yeni kaynakların mevcut olduğuna göre, bu kaynakları kullanan ekranlarımıza bazı alt pencere öğeleri eklememiz gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="dced1-160">Now that we have some new resources available, we need to add some child widgets to our screen that can utilize these resources.</span></span> <span data-ttu-id="dced1-161">Hedef görünümdeki pencereye sağ tıklayarak "\***hello_world** _" adlı önceden oluşturulmuş pencereyi seçin.</span><span class="sxs-lookup"><span data-stu-id="dced1-161">Select the previously created window named "\***hello_world** _" by right-clicking on the window in the Target View.</span></span> <span data-ttu-id="dced1-162">Artık görüntülenen açılır menüde, yeni bir _ *_GX_PROMPT_*\* pencere öğesi eklemek ve pencere öğesini arka plan penceresine eklemek için menü komutunu _*_Ekle, metin, komut istemi_*_ ' ni seçin.</span><span class="sxs-lookup"><span data-stu-id="dced1-162">In the pop-up menu that is now displayed, select the menu command _*_Insert, Text, Prompt_*_ to insert a new _ *_GX_PROMPT_*\* widget and attach the widget to the background window.</span></span> <span data-ttu-id="dced1-163">Pencereniz şu şekilde görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="dced1-163">Your window should now look like this:</span></span>

![Istem seçimine sahip bir açılan menünün ekran görüntüsü](./media/guix-studio/image78.jpg)

<span data-ttu-id="dced1-165">**Şekil 10,9**</span><span class="sxs-lookup"><span data-stu-id="dced1-165">**Figure 10.9**</span></span>

<span data-ttu-id="dced1-166">_ *_Fonts_*\* kaynak görünümü içindeki "\***MEDIUM_ITALIC** _" adlı yazı tipine tıklayın ve yazı tipini komut istemi pencere öğesine sürükleyin ve bırakın.</span><span class="sxs-lookup"><span data-stu-id="dced1-166">Click on the font named "***MEDIUM_ITALIC** _" in the _ *_Fonts_** Resource View, and drag and drop the font on the prompt widget.</span></span> <span data-ttu-id="dced1-167">Sonra, istemi yeniden boyutlandırmak, istem saydamlığını ayarlamak ve istem metnini ve stilini değiştirmek için Şekil 10,10 ' de gösterilen istem özelliklerini düzenleyin:</span><span class="sxs-lookup"><span data-stu-id="dced1-167">Next, edit the prompt properties as shown in figure 10.10 to resize the prompt, set the prompt transparency, and change the prompt text and style:</span></span>

![İstem için özellikler görünümünün ekran görüntüsü.](./media/guix-studio/image79.jpg)

<span data-ttu-id="dced1-169">**Şekil 10,10**</span><span class="sxs-lookup"><span data-stu-id="dced1-169">**Figure 10.10**</span></span>

<span data-ttu-id="dced1-170">Bu ayarların her birini ekran çözünürlüğünüzle ilgili olarak görmek için Özellikler görünümünde dikey olarak kaydırma yapmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="dced1-170">You may need to scroll vertically in the Properties View to see each of these settings depending on your screen resolution.</span></span> <span data-ttu-id="dced1-171">Bu değişiklikleri yaptıktan sonra, hedef görünümlerinizin şu şekilde görünmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="dced1-171">After making these changes, your Target View should now look like this:</span></span>

![Merhaba Dünya seçime sahip bir açılır menünün ekran görüntüsü.](./media/guix-studio/image80.jpg)

<span data-ttu-id="dced1-173">**Şekil 10,11**</span><span class="sxs-lookup"><span data-stu-id="dced1-173">**Figure 10.11**</span></span>

<span data-ttu-id="dced1-174">Daha sonra ekrana bir simge düğme stili pencere öğesi yerleştireceğiz.</span><span class="sxs-lookup"><span data-stu-id="dced1-174">Next we will place an Icon Button style widget on the screen.</span></span> <span data-ttu-id="dced1-175">Üzerine tıklayarak arka plan penceresini seçin ve pencereye yeni bir _*_GX_ICON_BUTTON_*_ eklemek için en üst düzey menü veya sağ tıklama açılan menüsünü kullanın. (**Ekle, düğme, simge düğmesi** _) seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="dced1-175">Select the background window by clicking on it, and use either the top-level menu or the right-click pop-up menu to select ***Insert, Button, Icon Button** _ to add a new _*_GX_ICON_BUTTON_\*_ to the window.</span></span> <span data-ttu-id="dced1-176">Daha önce eklediğimiz _ *_I_HISTORY_LG_*\* adlı simgeye tıklayın ve simgeyi simge düğmesine sürükleyin.</span><span class="sxs-lookup"><span data-stu-id="dced1-176">Click on the Icon named _ *_I_HISTORY_LG_*\* that we added earlier and drag it to the icon button.</span></span> <span data-ttu-id="dced1-177">Özellikler görünümünü kullanarak, simge konumunu ve boyutunu aşağıda göster olarak ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="dced1-177">Using the properties view, adjust the icon position and size as show below:</span></span>

![Simge düğmesi stili pencere öğesi için özellikler görünümünün ekran görüntüsü.](./media/guix-studio/image81.jpg)

<span data-ttu-id="dced1-179">**Şekil 10,12**</span><span class="sxs-lookup"><span data-stu-id="dced1-179">**Figure 10.12**</span></span>

<span data-ttu-id="dced1-180">Ekranınız şu şekilde görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="dced1-180">Your screen should now look like this:</span></span>

![Merhaba Dünya ve Pano simgesiyle açılan menünün ekran görüntüsü.](./media/guix-studio/image82.jpg)

<span data-ttu-id="dced1-182">**Şekil 10,13**</span><span class="sxs-lookup"><span data-stu-id="dced1-182">**Figure 10.13**</span></span>

<span data-ttu-id="dced1-183">Bu, basit örnek ekran tasarımı için bu tamamlamayı arayacağız.</span><span class="sxs-lookup"><span data-stu-id="dced1-183">We will call this complete for the simple example screen design.</span></span> <span data-ttu-id="dced1-184">Gerçek uygulama ekranlarınız büyük olasılıkla çok daha karmaşık olacaktır, ancak bu, kendi uygulama ekranlarınızı oluşturmak için Gux Studio 'Yu nasıl kullanacağınızı göstermek için yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="dced1-184">Your actual application screens will likely be much more sophisticated, but this is enough to show you how to use GUIX Studio to create your own application screens.</span></span>

## <a name="generate-resource-and-application-code"></a><span data-ttu-id="dced1-185">Kaynak ve uygulama kodu oluştur</span><span class="sxs-lookup"><span data-stu-id="dced1-185">Generate Resource and Application Code</span></span>

<span data-ttu-id="dced1-186">Sonraki adım, katıştırılmış Gux çalışma zamanı Kullanıcı arabirimini tanımlayan kaynak dosyası ve belirtim dosyası oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="dced1-186">The next step is to generate the resource file and specification file that define the embedded GUIX run-time UI.</span></span> <span data-ttu-id="dced1-187">Çıkış dosyalarınızı oluşturmak için proje görünümündeki ***main_display** _ düğümüne sağ tıklayıp _ *_kaynak dosyaları oluştur_** komutunu seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="dced1-187">To generate your output files you will need right-click on the ***main_display** _ node in the Project View, and select the _ *_Generate Resource Files_** command.</span></span> <span data-ttu-id="dced1-188">Şekil 10,14 ' de gösterildiği gibi, kaynak dosyalarınızın oluşturulduğunu belirten bir bilgi penceresi gözlemleyeceksiniz:</span><span class="sxs-lookup"><span data-stu-id="dced1-188">You will observe an information window that indicates your resource files have been generated, as shown in figure 10.14:</span></span>

![Bildirim iletişim kutusunun ekran görüntüsü.](./media/guix-studio/image83.jpg)

<span data-ttu-id="dced1-190">**Şekil 10,14**</span><span class="sxs-lookup"><span data-stu-id="dced1-190">**Figure 10.14**</span></span>

<span data-ttu-id="dced1-191">Bu bildirimi kapatmak için ***Tamam** _ ' e tıklayın ve _*_main_display_*_ düğümüne sağ tıklayıp _ *_Belirtim dosyaları oluştur_** komutunu seçerek aynı yordamı kullanın.</span><span class="sxs-lookup"><span data-stu-id="dced1-191">Click ***OK** _ to dismiss this notification, and use the same procedure to right-click on the _*_main_display_*_ node and select the _ *_Generate Specification Files_** command.</span></span> <span data-ttu-id="dced1-192">Benzer bir bildirim penceresi gözlemleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dced1-192">You should observe a similar notification window.</span></span> <span data-ttu-id="dced1-193">Basit UI uygulama dosyalarınızı oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="dced1-193">You have now generated your simple UI application files.</span></span>

## <a name="create-user-supplied-code"></a><span data-ttu-id="dced1-194">Kullanıcı tarafından sağlanan kod oluştur</span><span class="sxs-lookup"><span data-stu-id="dced1-194">Create User Supplied Code</span></span>

<span data-ttu-id="dced1-195">Sonraki adım, Gux Studio tarafından üretilen ekran tasarımını çağırabilecek kendi uygulama dosyanızı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="dced1-195">The next step is to create your own application file that will invoke the GUIX Studio-generated screen design.</span></span> <span data-ttu-id="dced1-196">Tercih ettiğiniz düzenleyiciyi kullanarak, ***new_example. c*** adlı bir kaynak dosya oluşturun ve bu dosyaya aşağıdaki kaynak kodu girin:</span><span class="sxs-lookup"><span data-stu-id="dced1-196">Using your preferred editor, create a source file named ***new_example.c***, and enter the following source code into this file:</span></span>

```C

/* This is an example of the GUIX graphics framework in Win32. */
/* Include system files. */

#include <stdio.h>
#include "tx_api.h"
#include "gx_api.h"

/* Include GUIX resource and specification files for example. */

#include "new_example_resources.h"
#include "new_example_specifications.h"

/* Define the new example thread control block and stack. */

TX_THREAD new_example_thread;
UCHAR new_example_thread_stack[4096];

/* Define the root window pointer. */

GX_WINDOW_ROOT *root_window;

/* Define function prototypes. */

VOID new_example_thread_entry(ULONG thread_input);
UINT win32_graphics_driver_setup_24bpp(GX_DISPLAY *display);

int main()
{
    /* Enter the ThreadX kernel. */
    tx_kernel_enter();
    return(0);
}

VOID tx_application_define(void *first_unused_memory)
{
    /* Create the new example thread. */
    tx_thread_create(&new_example_thread, "GUIX New Example Thread", 
                      new_example_thread_entry, 0, 
                      new_example_thread_stack, sizeof(new_example_thread_stack),
                      1, 1, TX_NO_TIME_SLICE, TX_AUTO_START);
}

VOID new_example_thread_entry(ULONG thread_input)
{

    /* Initialize the GUIX library */
    gx_system_initialize();

    /* Configure the main display. */
    gx_studio_display_configure(MAIN_DISPLAY,                      /* Display to configure*/
                                win32_graphics_driver_setup_24bpp, /* Driver to use */
                                LANGUAGE_ENGLISH,                  /* Language to install */
                                MAIN_DISPLAY_DEFAULT_THEME,        /* Theme to install */
                                &root_window);                     /* Root window pointer */

    /* Create the screen - attached to root window. */

    gx_studio_named_widget_create("hello_world", (GX_WIDGET *) root_window, GX_NULL);

    /* Show the root window to make it visible. */
    gx_widget_show(root_window);

    /* Let GUIX run. */
    gx_system_start();

}
```

<span data-ttu-id="dced1-197">Yukarıdaki kaynak kodu, `GUIX New Example Thread` 4k baytlık yığın boyutuyla adlı tipik bir ThreadX iş parçacığı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="dced1-197">The source code above creates a typical ThreadX thread named `GUIX New Example Thread` with a stack size of 4K bytes.</span></span> <span data-ttu-id="dced1-198">İlginç işler ***new_example_thread_entry*** adlı işlevde başlar.</span><span class="sxs-lookup"><span data-stu-id="dced1-198">The interesting work begins in the function named ***new_example_thread_entry***.</span></span> <span data-ttu-id="dced1-199">Bu işlev, Gux 'e özgü iş parçacığının çalışmaya başladığı yerdir.</span><span class="sxs-lookup"><span data-stu-id="dced1-199">This function is where the GUIX specific thread begins to run.</span></span>

<span data-ttu-id="dced1-200">İlk çağrı ***gx_system_initialize*** adlı işleve yapılır.</span><span class="sxs-lookup"><span data-stu-id="dced1-200">The first call is to the function named ***gx_system_initialize***.</span></span> <span data-ttu-id="dced1-201">Bu çağrı, Gux kitaplığını ilk kullanım için hazırlamak üzere diğer bir GUıDX API 'Leri çağrılmadan önce her zaman gereklidir.</span><span class="sxs-lookup"><span data-stu-id="dced1-201">This call is always required before any other GUIX APIs are invoked to prepare the GUIX library for first use.</span></span>

<span data-ttu-id="dced1-202">Sonra, örnek ***gx_studio_display_configure*** işlevini çağırır.</span><span class="sxs-lookup"><span data-stu-id="dced1-202">Next, the example calls the function ***gx_studio_display_configure***.</span></span> <span data-ttu-id="dced1-203">Bu işlev, GUıDX görüntüleme örneğini oluşturur, uygulama dizesi tablosunun istenen dilini yüklerse, istenen temayı görüntüleme kaynaklarından yüklerse ve bu görüntü için oluşturulan kök penceresine bir işaretçi döndürüyor.</span><span class="sxs-lookup"><span data-stu-id="dced1-203">This function creates the GUIX display instance, installs the requested language of the application string table, installs the requested theme from the display resources, and returns a pointer to the root window that has been created for this display.</span></span> <span data-ttu-id="dced1-204">Kök pencere, uygulamamız görüntülenecek olan tüm üst düzey ekranların üst öğesi olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="dced1-204">The root window is used as the parent of all top-level screens that our application will display.</span></span>

<span data-ttu-id="dced1-205">Daha sonra örnek, _ *_hello_world_*\* ekranımız bir örnek oluşturmak için \***gx_studio_named_widget_create** _ ' i çağırır.</span><span class="sxs-lookup"><span data-stu-id="dced1-205">Next the example calls ***gx_studio_named_widget_create** _ to create an instance of our _ *_hello_world_** screen.</span></span> <span data-ttu-id="dced1-206">Bu işlev, tanımladığımız bir ekran örneği oluşturmak için Gux Studio tarafından ürettiği veri yapılarını ve kaynağını kullanır.</span><span class="sxs-lookup"><span data-stu-id="dced1-206">This function uses the data structures and resource produces by GUIX Studio to create an instance of the screen as we have defined it.</span></span> <span data-ttu-id="dced1-207">Bu işlev çağrısına ikinci parametre olarak kök pencere işaretçisini geçirdik, yani ekranın kök pencereye hemen eklenmesini istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="dced1-207">We pass the root window pointer as the second parameter to this function call, meaning we want the screen to be immediately attached to the root window.</span></span> <span data-ttu-id="dced1-208">Son parametre, oluşturulan ekrana bir işaretçi tutmak istiyorsam kullanılabilecek, isteğe bağlı bir dönüş işaretçisidir.</span><span class="sxs-lookup"><span data-stu-id="dced1-208">The last parameter is an optional return pointer that can be used if we want to keep a pointer to the created screen.</span></span>

<span data-ttu-id="dced1-209">Next ***gx_widget_show** _ çağrılır, bu, kök pencereyi ve tüm alt öğelerini _ *_hello_world_** ekranı gibi görünür hale getirir.</span><span class="sxs-lookup"><span data-stu-id="dced1-209">Next ***gx_widget_show** _ is called, which makes the root window and all of its children, including the _ *_hello_world_** screen, visible.</span></span>

<span data-ttu-id="dced1-210">Son olarak, örnek ***gx_system_start*** çağırır.</span><span class="sxs-lookup"><span data-stu-id="dced1-210">Finally, the example calls ***gx_system_start***.</span></span> <span data-ttu-id="dced1-211">Bu işlev, GUıDX sistem olay işleme döngüsünü yürütmeye başlıyor.</span><span class="sxs-lookup"><span data-stu-id="dced1-211">This function begins executing the GUIX system event processing loop.</span></span>

## <a name="build-and-run-the-example"></a><span data-ttu-id="dced1-212">Örneği derleyin ve çalıştırın</span><span class="sxs-lookup"><span data-stu-id="dced1-212">Build and Run the Example</span></span>

<span data-ttu-id="dced1-213">Örnek oluşturma ve çalıştırma, derleme araçlarınız ve ortamınıza özeldir.</span><span class="sxs-lookup"><span data-stu-id="dced1-213">Building and running the example is specific to your build tools and environment.</span></span> <span data-ttu-id="dced1-214">Ancak genel işlemi tanımlayabiliriz:</span><span class="sxs-lookup"><span data-stu-id="dced1-214">However we can define the general process:</span></span>

1. <span data-ttu-id="dced1-215">Yeni bir dizin ve uygulama projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="dced1-215">Create a new directory and application project</span></span>
1. <span data-ttu-id="dced1-216">Bu dosyaları projeye ekleyin:</span><span class="sxs-lookup"><span data-stu-id="dced1-216">Add these files to the project:</span></span>

    <span data-ttu-id="dced1-217">**new_example_resources. c**</span><span class="sxs-lookup"><span data-stu-id="dced1-217">**new_example_resources.c**</span></span>

    <span data-ttu-id="dced1-218">**new_example_specification. c**</span><span class="sxs-lookup"><span data-stu-id="dced1-218">**new_example_specification.c**</span></span>

    <span data-ttu-id="dced1-219">**new_example. c**</span><span class="sxs-lookup"><span data-stu-id="dced1-219">**new_example.c**</span></span>

1. <span data-ttu-id="dced1-220">GUX Studio yükleme yolundan Win32 çalışma zamanı destek dosyalarını ekleyin ***./win32_runtime***.</span><span class="sxs-lookup"><span data-stu-id="dced1-220">Add the Win32 run-time support files from the GUIX Studio installation path ***./win32_runtime***.</span></span> <span data-ttu-id="dced1-221">Bu, ThreadX ve GUıDX Win32 üst bilgisini ve çalışma zamanı kitaplık dosyalarını içerir.</span><span class="sxs-lookup"><span data-stu-id="dced1-221">This includes the ThreadX and GUIX Win32 header and run-time library files.</span></span>
1. <span data-ttu-id="dced1-222">GUX Win32 kitaplığı 'nı (***GX. lib***) projeye ekleme</span><span class="sxs-lookup"><span data-stu-id="dced1-222">Add the GUIX Win32 library (***gx.lib***) to the project</span></span>
1. <span data-ttu-id="dced1-223">Projeye ThreadX Win32 kitaplığını (***TX. lib***) ekleme</span><span class="sxs-lookup"><span data-stu-id="dced1-223">Add the ThreadX Win32 library (***tx.lib***) to the project</span></span>
1. <span data-ttu-id="dced1-224">Uygulamayı derleyin, bağlayın ve çalıştırın!</span><span class="sxs-lookup"><span data-stu-id="dced1-224">Compile, Link, and Run the application!</span></span>
