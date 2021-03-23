---
title: Ek C-Gux pencere öğesi stilleri
description: GUX pencere öğesi stilleri hakkında bilgi edinin.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 83d5c5167739e91b7af8fce6b04213f610984fc6
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104827280"
---
# <a name="appendix-c---guix-widget-styles"></a><span data-ttu-id="5d14a-103">Ek C-Gux pencere öğesi stilleri</span><span class="sxs-lookup"><span data-stu-id="5d14a-103">Appendix C - GUIX Widget Styles</span></span>

<span data-ttu-id="5d14a-104">__***Genel stiller (çoğu pencere öğesi türü ile kullanılır):***__</span><span class="sxs-lookup"><span data-stu-id="5d14a-104">__***General Styles (Used with most widget types):***__</span></span>

<span data-ttu-id="5d14a-105">**GX_STYLE_BORDER_NONE**</span><span class="sxs-lookup"><span data-stu-id="5d14a-105">**GX_STYLE_BORDER_NONE**</span></span>
  - <span data-ttu-id="5d14a-106">Değer: 0x00000000</span><span class="sxs-lookup"><span data-stu-id="5d14a-106">Value: 0x00000000</span></span>
  - <span data-ttu-id="5d14a-107">Açıklama: kenarlığı olmayan bir pencere öğesi çizmek için bu stili kullanın.</span><span class="sxs-lookup"><span data-stu-id="5d14a-107">Description: Use this style to draw a widget with no border.</span></span>

<span data-ttu-id="5d14a-108">**GX_STYLE_BORDER_RAISED**</span><span class="sxs-lookup"><span data-stu-id="5d14a-108">**GX_STYLE_BORDER_RAISED**</span></span>
  - <span data-ttu-id="5d14a-109">Değer: 0x00000001</span><span class="sxs-lookup"><span data-stu-id="5d14a-109">Value: 0x00000001</span></span>
  - <span data-ttu-id="5d14a-110">Açıklama: yükseltilmiş bir kenarlığa sahip pencere öğesi çizin.</span><span class="sxs-lookup"><span data-stu-id="5d14a-110">Description: Draw widget with a raised border.</span></span>

<span data-ttu-id="5d14a-111">**GX_STYLE_BORDER_RECESSED**</span><span class="sxs-lookup"><span data-stu-id="5d14a-111">**GX_STYLE_BORDER_RECESSED**</span></span>
  - <span data-ttu-id="5d14a-112">Değer: 0x00000002</span><span class="sxs-lookup"><span data-stu-id="5d14a-112">Value: 0x00000002</span></span>
  - <span data-ttu-id="5d14a-113">Açıklama: bir kenar pencere öğesi ile yeniden oluşturulmuş bir kenarlık çizin.</span><span class="sxs-lookup"><span data-stu-id="5d14a-113">Description: Draw widget with a recessed border.</span></span>

<span data-ttu-id="5d14a-114">**GX_STYLE_BORDER_THIN**</span><span class="sxs-lookup"><span data-stu-id="5d14a-114">**GX_STYLE_BORDER_THIN**</span></span>
  - <span data-ttu-id="5d14a-115">Değer: 0x00000004</span><span class="sxs-lookup"><span data-stu-id="5d14a-115">Value: 0x00000004</span></span>
  - <span data-ttu-id="5d14a-116">Açıklama: tek piksellik genişlik kenarlığı çizin.</span><span class="sxs-lookup"><span data-stu-id="5d14a-116">Description: Draw a one-pixel width border.</span></span>

<span data-ttu-id="5d14a-117">**GX_STYLE_BORDER_THICK**</span><span class="sxs-lookup"><span data-stu-id="5d14a-117">**GX_STYLE_BORDER_THICK**</span></span> 
  - <span data-ttu-id="5d14a-118">Değer: 0x00000008</span><span class="sxs-lookup"><span data-stu-id="5d14a-118">Value: 0x00000008</span></span>
  - <span data-ttu-id="5d14a-119">Açıklama: kalın kenarlıklı pencere öğesi çizin.</span><span class="sxs-lookup"><span data-stu-id="5d14a-119">Description: Draw widget with a thick border.</span></span>

<span data-ttu-id="5d14a-120">**GX_STYLE_BORDER_MASK**</span><span class="sxs-lookup"><span data-stu-id="5d14a-120">**GX_STYLE_BORDER_MASK**</span></span>
  - <span data-ttu-id="5d14a-121">Değer: 0x0000000F</span><span class="sxs-lookup"><span data-stu-id="5d14a-121">Value: 0x0000000f</span></span>
  - <span data-ttu-id="5d14a-122">Açıklama: pencere öğesi stili üyesinin yalnızca stil alanlarını test etmek için kullanılan maske değeri.</span><span class="sxs-lookup"><span data-stu-id="5d14a-122">Description: Mask value used to test only the style fields of the widget style member.</span></span>

<span data-ttu-id="5d14a-123">**GX_STYLE_TRANSPARENT**</span><span class="sxs-lookup"><span data-stu-id="5d14a-123">**GX_STYLE_TRANSPARENT**</span></span>
  - <span data-ttu-id="5d14a-124">Değer: 0x10000000</span><span class="sxs-lookup"><span data-stu-id="5d14a-124">Value: 0x10000000</span></span>
  - <span data-ttu-id="5d14a-125">Açıklama: en az kısmen saydam bir pencere öğesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5d14a-125">Description: Create a widget that is at least partially transparent.</span></span> <span data-ttu-id="5d14a-126">Bu stil, pencere öğesi arka plan planı olarak yarı saydam bir pixelmap çizme pencere öğeleri de dahil olmak üzere tamamen donuk bir şekilde çizmediği zaman kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5d14a-126">This style should be used when a widget does not draw itself fully opaque, including widgets that draw a semi-transparent pixelmap as the widget background.</span></span> <span data-ttu-id="5d14a-127">Bu stil bayrağı, pencere öğesi arka plan alanını yenilemek için pencere öğesi üst öğesinin çizilmek zorunda olduğunu bildirir.</span><span class="sxs-lookup"><span data-stu-id="5d14a-127">This style flag informs GUIX that the widget parent must be drawn to refresh the widget background area.</span></span>

<span data-ttu-id="5d14a-128">**GX_STYLE_DRAW_SELECTED**</span><span class="sxs-lookup"><span data-stu-id="5d14a-128">**GX_STYLE_DRAW_SELECTED**</span></span>
  - <span data-ttu-id="5d14a-129">Değer: 0x20000000</span><span class="sxs-lookup"><span data-stu-id="5d14a-129">Value: 0x20000000</span></span>
  - <span data-ttu-id="5d14a-130">Açıklama: pencere öğesinin seçili durum renkleri ve yazı tipleri kullanılarak çizilip çizilmeyeceğini belirtin.</span><span class="sxs-lookup"><span data-stu-id="5d14a-130">Description: Specify that the widget should be drawn using selected state colors and fonts.</span></span> <span data-ttu-id="5d14a-131">Farklı pencere öğesi türleri, pencere öğesinin Şu anda seçili olduğunu göstermek için DRAW_SELECTED stilini farklı şekillerde kullanır.</span><span class="sxs-lookup"><span data-stu-id="5d14a-131">Different widget types use the DRAW_SELECTED style in different ways to indicate the widget is currently selected.</span></span>

<span data-ttu-id="5d14a-132">**GX_STYLE_ENABLED**</span><span class="sxs-lookup"><span data-stu-id="5d14a-132">**GX_STYLE_ENABLED**</span></span>
  - <span data-ttu-id="5d14a-133">Değer: 0x40000000</span><span class="sxs-lookup"><span data-stu-id="5d14a-133">Value: 0x40000000</span></span>
  - <span data-ttu-id="5d14a-134">Açıklama: pencere öğesinin kullanıcı giriş olaylarını kabul etmesine ve çıkış sinyalleri oluşturmasına izin veren pencere öğesini etkin olarak Işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="5d14a-134">Description: Mark the widget as enabled, which allows the widget to accept user input events and generate output signals.</span></span>
  
<span data-ttu-id="5d14a-135">**GX_STYLE_DYNAMICALLY_ALLOCATED**</span><span class="sxs-lookup"><span data-stu-id="5d14a-135">**GX_STYLE_DYNAMICALLY_ALLOCATED**</span></span>
  - <span data-ttu-id="5d14a-136">Değer: 0x80000000</span><span class="sxs-lookup"><span data-stu-id="5d14a-136">Value: 0x80000000</span></span>
  - <span data-ttu-id="5d14a-137">Açıklama: pencere öğesi denetim bloğu belleğinin pencere öğesi oluşturulduğunda gx_system_memory_allocator hizmeti kullanılarak dinamik olarak ayrıldığını ve pencere öğesi yok edildiğinde denetim blok belleği serbest bırakıldığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="5d14a-137">Description: Indicates the widget control block memory is dynamically allocated using the gx_system_memory_allocator service when the widget is created, and the control block memory is freed if the widget is destroyed.</span></span>

<span data-ttu-id="5d14a-138">**GX_STYLE_USE_LOCAL_ALPHA**</span><span class="sxs-lookup"><span data-stu-id="5d14a-138">**GX_STYLE_USE_LOCAL_ALPHA**</span></span>
  - <span data-ttu-id="5d14a-139">Değer: 0x01000000</span><span class="sxs-lookup"><span data-stu-id="5d14a-139">Value: 0x01000000</span></span>
  - <span data-ttu-id="5d14a-140">Açıklama: Gux çizim işlevlerini pencere öğesi çizerken yerel pencere öğesi Alfa değerini kullanmasını söyler.</span><span class="sxs-lookup"><span data-stu-id="5d14a-140">Description: Instructs GUIX drawing functions to use the local widget alpha value when drawing the widget.</span></span> <span data-ttu-id="5d14a-141">Bu bayrak normalde iç Gux mantığı tarafından pencere öğesi Soldurma animasyonlarını uygulamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5d14a-141">This flag is normally used by the internal GUIX logic to implement widget fading animations.</span></span>


<span data-ttu-id="5d14a-142">__***Metin hizalama stilleri (metin çizimli tüm pencere öğeleri için uygulanan stiller):***__</span><span class="sxs-lookup"><span data-stu-id="5d14a-142">__***Text Alignment Styles (styles applied to all widgets that draw text):***__</span></span>

<span data-ttu-id="5d14a-143">**GX_STYLE_TEXT_LEFT**</span><span class="sxs-lookup"><span data-stu-id="5d14a-143">**GX_STYLE_TEXT_LEFT**</span></span>
  - <span data-ttu-id="5d14a-144">Değer: 0x00001000</span><span class="sxs-lookup"><span data-stu-id="5d14a-144">Value: 0x00001000</span></span>
  - <span data-ttu-id="5d14a-145">Açıklama: metin, pencere öğesi istemci alanı içinde sola hizalı olarak çizilir.</span><span class="sxs-lookup"><span data-stu-id="5d14a-145">Description: Text is drawn left-aligned within the widget client area.</span></span>

<span data-ttu-id="5d14a-146">**GX_STYLE_TEXT_RIGHT**</span><span class="sxs-lookup"><span data-stu-id="5d14a-146">**GX_STYLE_TEXT_RIGHT**</span></span> 
  - <span data-ttu-id="5d14a-147">Değer: 0x00002000</span><span class="sxs-lookup"><span data-stu-id="5d14a-147">Value: 0x00002000</span></span>
  - <span data-ttu-id="5d14a-148">Açıklama: metin, pencere öğesi istemci alanı içinde sağa hizalı olarak çizilir.</span><span class="sxs-lookup"><span data-stu-id="5d14a-148">Description: Text is drawn right-aligned within the widget client area.</span></span>

<span data-ttu-id="5d14a-149">**GX_STYLE_TEXT_CENTER**</span><span class="sxs-lookup"><span data-stu-id="5d14a-149">**GX_STYLE_TEXT_CENTER**</span></span>
  - <span data-ttu-id="5d14a-150">Değer: 0x00004000</span><span class="sxs-lookup"><span data-stu-id="5d14a-150">Value: 0x00004000</span></span>
  - <span data-ttu-id="5d14a-151">Açıklama: metin, pencere öğesi istemci alanı içinde ortalanmış olarak çizilir.</span><span class="sxs-lookup"><span data-stu-id="5d14a-151">Description: Text is drawn center-aligned within the widget client area.</span></span>

<span data-ttu-id="5d14a-152">**GX_STYLE_TEXT_COPY**</span><span class="sxs-lookup"><span data-stu-id="5d14a-152">**GX_STYLE_TEXT_COPY**</span></span>
  - <span data-ttu-id="5d14a-153">Değer: 0x00008000</span><span class="sxs-lookup"><span data-stu-id="5d14a-153">Value: 0x00008000</span></span>
  - <span data-ttu-id="5d14a-154">Açıklama: varsayılan olarak, metin çizilen pencere öğeleri yalnızca uygulama tarafından geçirilen metne bir işaretçi tutar.</span><span class="sxs-lookup"><span data-stu-id="5d14a-154">Description: By default, widgets that draw text keep only a pointer to the text which is passed in by the application.</span></span> <span data-ttu-id="5d14a-155">Dize tablosunda tanımlanan statik olarak tanımlanmış metin için, pencere öğesinin atanan metnin özel bir kopyasını oluşturmak için bir neden yoktur.</span><span class="sxs-lookup"><span data-stu-id="5d14a-155">For statically defined text that is defined within the string table, there is no reason for the widget to make a private copy of the text assigned.</span></span> <span data-ttu-id="5d14a-156">Ancak, bir pencere öğesine atanan metin sprintler () veya gx_utility_ltoa gibi işlevler kullanılarak dinamik olarak oluşturulduysa, pencere öğesine atanan metinlerin özel bir kopyasını tutmasına söylemek çok uygundur.</span><span class="sxs-lookup"><span data-stu-id="5d14a-156">However, if the text assigned to a widget is created dynamically using functions like sprint() or gx_utility_ltoa, then it is often convenient to tell the widget to keep it’s own private copy of any text assigned.</span></span> <span data-ttu-id="5d14a-157">Bu, uygulamanın metin dizesini tanımlarken otomatik veya geçici değişkenler kullanmasına izin verir. Bu, uygulamanın, dinamik olarak tanımlanan metni kullanan her metin pencere öğesi için statik olarak tanımlanmış karakter dizileri tanımlamak zorunda olacağını belirler.</span><span class="sxs-lookup"><span data-stu-id="5d14a-157">This allows the application to use automatic or temporary variables when defining the text string, when the application would otherwise be required to define statically defined character arrays for each text widget that is using dynamically defined text.</span></span> <span data-ttu-id="5d14a-158">Bu stil bayrağı ayarlandığında pencere öğesi, atanan dizenin özel bir kopyasını tutmak için gereken bellek bloğunu dinamik olarak ayırmak üzere gx_system_memory_allocator işlevini kullanır.</span><span class="sxs-lookup"><span data-stu-id="5d14a-158">When this style flag is set, the widget will use the gx_system_memory_allocator function to dynamically allocate the memory block needed to hold a private copy of the assigned string.</span></span> <span data-ttu-id="5d14a-159">Bu nedenle, bu stil bayrağını kullanmak memory_allocator ve memory_deallocator işlevlerini tanımlayan uygulamada tahmin edilir.</span><span class="sxs-lookup"><span data-stu-id="5d14a-159">Therefore using this style flag is predicated on the application defining memory_allocator and memory_deallocator functions.</span></span> <span data-ttu-id="5d14a-160">GX_STYLE_TEXT_COPY ayarlandıktan sonra temizlenmemelidir ve bunu yapmak öngörülemeyen sonuçlara neden olur.</span><span class="sxs-lookup"><span data-stu-id="5d14a-160">GX_STYLE_TEXT_COPY should not be cleared after it has been set, and doing so will cause unpredictable results.</span></span>

<span data-ttu-id="5d14a-161">__***Düğme stilleri (yalnızca Gux düğmesi pencere öğesi türleri için geçerlidir):***__</span><span class="sxs-lookup"><span data-stu-id="5d14a-161">__***Button Styles (apply only to GUIX button widget types):***__</span></span>

<span data-ttu-id="5d14a-162">**GX_STYLE_BUTTON_PUSHED**</span><span class="sxs-lookup"><span data-stu-id="5d14a-162">**GX_STYLE_BUTTON_PUSHED**</span></span>
  - <span data-ttu-id="5d14a-163">0x00000010 değeri</span><span class="sxs-lookup"><span data-stu-id="5d14a-163">Value 0x00000010</span></span>
  - <span data-ttu-id="5d14a-164">Açıklama: düğmenin itilmiş veya seçili durumda olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="5d14a-164">Description: Indicates the button is in the pushed or selected state.</span></span>

<span data-ttu-id="5d14a-165">**GX_STYLE_BUTTON_TOGGLE**</span><span class="sxs-lookup"><span data-stu-id="5d14a-165">**GX_STYLE_BUTTON_TOGGLE**</span></span>
  - <span data-ttu-id="5d14a-166">Değer 0x00000020</span><span class="sxs-lookup"><span data-stu-id="5d14a-166">Value 0x00000020</span></span>
  - <span data-ttu-id="5d14a-167">Açıklama: düğme, her tıklama olayında itilmiş ve gönderilmemiş arasında durum olarak değişir.</span><span class="sxs-lookup"><span data-stu-id="5d14a-167">Description: Button will switch status between pushed and unpushed on every click event.</span></span> <span data-ttu-id="5d14a-168">Bu stil, genellikle "CheckBox" stil düğmeleri ile kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5d14a-168">This style is commonly used with “checkbox” style buttons.</span></span>

<span data-ttu-id="5d14a-169">**GX_STYLE_BUTTON_RADIO**</span><span class="sxs-lookup"><span data-stu-id="5d14a-169">**GX_STYLE_BUTTON_RADIO**</span></span>
  - <span data-ttu-id="5d14a-170">Değer 0x00000040</span><span class="sxs-lookup"><span data-stu-id="5d14a-170">Value 0x00000040</span></span>
  - <span data-ttu-id="5d14a-171">Açıklama: Bu stil, düğmenin dışlandığını belirtir ve seçildiğinde tüm düğme eşdüzey öğelerinin seçimini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="5d14a-171">Description: This style indicates the button will be exclusive, and deselect any button siblings when selected.</span></span> <span data-ttu-id="5d14a-172">Bu stil, genellikle "radyo düğmesi" stil düğmeleri ile kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5d14a-172">This style is commonly used with “radio button” style buttons.</span></span>

<span data-ttu-id="5d14a-173">**GX_STYLE_BUTTON_EVENT_ON_PUSH**</span><span class="sxs-lookup"><span data-stu-id="5d14a-173">**GX_STYLE_BUTTON_EVENT_ON_PUSH**</span></span>
  - <span data-ttu-id="5d14a-174">Değer: 0x00000080</span><span class="sxs-lookup"><span data-stu-id="5d14a-174">Value: 0x00000080</span></span>
  - <span data-ttu-id="5d14a-175">Açıklama: düğmenin başlangıçta gönderildiği bir tıklama olayı oluşturmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="5d14a-175">Description: Indicates the button generates a click event when initially pushed.</span></span> <span data-ttu-id="5d14a-176">Varsayılan işlem, düğme serbest bırakıldığında bir tıklama olayı oluşturmak olur.</span><span class="sxs-lookup"><span data-stu-id="5d14a-176">The default operation is to generate a click event when the button is released.</span></span>

<span data-ttu-id="5d14a-177">**GX_STYLE_BUTTON_REPEAT**</span><span class="sxs-lookup"><span data-stu-id="5d14a-177">**GX_STYLE_BUTTON_REPEAT**</span></span>
  - <span data-ttu-id="5d14a-178">Değer 0x00000100</span><span class="sxs-lookup"><span data-stu-id="5d14a-178">Value 0x00000100</span></span>
  - <span data-ttu-id="5d14a-179">Açıklama: Düğme itilmiş durumda tutulduğu zaman düğme üst öğesine yinelenen tıklama olaylarını göndermek gerektiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="5d14a-179">Description: Indicates the button should send repeated click events to the button parent when the button is held in the pushed state.</span></span>

<span data-ttu-id="5d14a-180">__***Liste stilleri (yalnızca Gux listesi pencere öğesi türleri için geçerlidir):***__</span><span class="sxs-lookup"><span data-stu-id="5d14a-180">__***List Styles (apply only to GUIX list widget types):***__</span></span>

<span data-ttu-id="5d14a-181">**GX_STYLE_CENTER_SELECTED**</span><span class="sxs-lookup"><span data-stu-id="5d14a-181">**GX_STYLE_CENTER_SELECTED**</span></span> 
  - <span data-ttu-id="5d14a-182">Değer: 0x00000010</span><span class="sxs-lookup"><span data-stu-id="5d14a-182">Value: 0x00000010</span></span>
  - <span data-ttu-id="5d14a-183">Açıklama: ayrılmış</span><span class="sxs-lookup"><span data-stu-id="5d14a-183">Description: Reserved</span></span>

<span data-ttu-id="5d14a-184">**GX_STYLE_WRAP**</span><span class="sxs-lookup"><span data-stu-id="5d14a-184">**GX_STYLE_WRAP**</span></span>
  - <span data-ttu-id="5d14a-185">Değer 0x00000020</span><span class="sxs-lookup"><span data-stu-id="5d14a-185">Value 0x00000020</span></span>
  - <span data-ttu-id="5d14a-186">Açıklama: liste, başlangıç veya bitiş listesi dizininden aşağı kaydırıldığında liste alt öğelerinden baştan sona kaydırılır.</span><span class="sxs-lookup"><span data-stu-id="5d14a-186">Description: The list children wrap from start to end when the list is dragged or scrolled past the starting or ending list index.</span></span>

<span data-ttu-id="5d14a-187">**GX_STYLE_FLICKABLE**</span><span class="sxs-lookup"><span data-stu-id="5d14a-187">**GX_STYLE_FLICKABLE**</span></span>
  - <span data-ttu-id="5d14a-188">Değer: 0x00000040</span><span class="sxs-lookup"><span data-stu-id="5d14a-188">Value: 0x00000040</span></span>
  - <span data-ttu-id="5d14a-189">Açıklama: ayrılmış</span><span class="sxs-lookup"><span data-stu-id="5d14a-189">Description: Reserved</span></span>

<span data-ttu-id="5d14a-190">__***Pixelmap düğmesi ve simge düğmesi stilleri:***__</span><span class="sxs-lookup"><span data-stu-id="5d14a-190">__***Pixelmap Button and Icon Button Styles:***__</span></span>

<span data-ttu-id="5d14a-191">**GX_STYLE_HALIGN_CENTER**</span><span class="sxs-lookup"><span data-stu-id="5d14a-191">**GX_STYLE_HALIGN_CENTER**</span></span>
  - <span data-ttu-id="5d14a-192">Değer: 0x00010000</span><span class="sxs-lookup"><span data-stu-id="5d14a-192">Value: 0x00010000</span></span>
  - <span data-ttu-id="5d14a-193">Açıklama: Bu düğme pixelmap, yatay eksende düğme sınırı içinde ortahizalı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5d14a-193">Description: The button pixelmap should be center aligned within the button boundary on the horizontal axis.</span></span>

<span data-ttu-id="5d14a-194">**GX_STYLE_HALIGN_LEFT**</span><span class="sxs-lookup"><span data-stu-id="5d14a-194">**GX_STYLE_HALIGN_LEFT**</span></span>
  - <span data-ttu-id="5d14a-195">Değer: 0x00020000</span><span class="sxs-lookup"><span data-stu-id="5d14a-195">Value: 0x00020000</span></span>
  - <span data-ttu-id="5d14a-196">Açıklama: düğme pixelmap, Yatay eksenin düğme sınırı içinde sola hizalı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5d14a-196">Description: The button pixelmap should be left aligned within the button boundary on the horizontal axis.</span></span>

<span data-ttu-id="5d14a-197">**GX_STYLE_HALIGN_RIGHT**</span><span class="sxs-lookup"><span data-stu-id="5d14a-197">**GX_STYLE_HALIGN_RIGHT**</span></span>
  - <span data-ttu-id="5d14a-198">Değer 0x00040000</span><span class="sxs-lookup"><span data-stu-id="5d14a-198">Value 0x00040000</span></span>
  - <span data-ttu-id="5d14a-199">Açıklama: düğme pixelmap, Yatay eksenin düğme sınırı içinde sağa hizalanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5d14a-199">Description: The button pixelmap should be right aligned within the button boundary on the horizontal axis.</span></span>

<span data-ttu-id="5d14a-200">**GX_STYLE_VALIGN_CENTER**</span><span class="sxs-lookup"><span data-stu-id="5d14a-200">**GX_STYLE_VALIGN_CENTER**</span></span>
  - <span data-ttu-id="5d14a-201">Değer 0x00080000</span><span class="sxs-lookup"><span data-stu-id="5d14a-201">Value 0x00080000</span></span>
  - <span data-ttu-id="5d14a-202">Açıklama: Bu düğme pixelmap, dikey eksen üzerindeki düğme sınırı içinde ortahizalı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5d14a-202">Description: The button pixelmap should be center aligned within the button boundary on the vertical axis.</span></span>

<span data-ttu-id="5d14a-203">**GX_STYLE_VALIGN_TOP**</span><span class="sxs-lookup"><span data-stu-id="5d14a-203">**GX_STYLE_VALIGN_TOP**</span></span>
  - <span data-ttu-id="5d14a-204">Değer: 0x00100000</span><span class="sxs-lookup"><span data-stu-id="5d14a-204">Value: 0x00100000</span></span>
  - <span data-ttu-id="5d14a-205">Açıklama: düğme pixelmap, dikey eksenin düğme sınırı içinde üste hizalı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5d14a-205">Description: The button pixelmap should be top aligned within the button boundary on the vertical axis.</span></span>

<span data-ttu-id="5d14a-206">**GX_STYLE_VALIGN_BOTTOM**</span><span class="sxs-lookup"><span data-stu-id="5d14a-206">**GX_STYLE_VALIGN_BOTTOM**</span></span>
  - <span data-ttu-id="5d14a-207">Değer: 0x00200000</span><span class="sxs-lookup"><span data-stu-id="5d14a-207">Value: 0x00200000</span></span>
  - <span data-ttu-id="5d14a-208">Açıklama: düğme pixelmap, dikey Yatay eksenin düğme sınırı içinde alta hizalı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5d14a-208">Description: The button pixelmap should be bottom aligned within the button boundary on the vertical horizontal axis.</span></span>

<span data-ttu-id="5d14a-209">__***Kaydırıcı Stilleri (yalnızca GX_SLIDER ve türetilmiş pencere öğesi türleri için Appy):***__</span><span class="sxs-lookup"><span data-stu-id="5d14a-209">__***Slider Styles (Appy only to GX_SLIDER and derived widget types):***__</span></span>

<span data-ttu-id="5d14a-210">**GX_STYLE_SHOW_NEEDLE**</span><span class="sxs-lookup"><span data-stu-id="5d14a-210">**GX_STYLE_SHOW_NEEDLE**</span></span>
  - <span data-ttu-id="5d14a-211">Değer: 0x00000200</span><span class="sxs-lookup"><span data-stu-id="5d14a-211">Value: 0x00000200</span></span>
  - <span data-ttu-id="5d14a-212">Açıklama: Bu stilin, iğne göstergesini çizmesi için bu stil dahil olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5d14a-212">Description: This style must be included for the slider to draw the needle indicator.</span></span> <span data-ttu-id="5d14a-213">Bu stil, uygulama kaydırıcı iğne 'yi devre dışı bırakmak isterse veya özel bir iğne göstergesi çizmek isterse devre dışı bırakılabilir.</span><span class="sxs-lookup"><span data-stu-id="5d14a-213">This style can be disabled if the application wants to disable the slider needle or draw a custom needle indicator.</span></span>

<span data-ttu-id="5d14a-214">**GX_STYLE_SHOW_TICKMARKS**</span><span class="sxs-lookup"><span data-stu-id="5d14a-214">**GX_STYLE_SHOW_TICKMARKS**</span></span>
  - <span data-ttu-id="5d14a-215">Değer: 0x00000400</span><span class="sxs-lookup"><span data-stu-id="5d14a-215">Value: 0x00000400</span></span>
  - <span data-ttu-id="5d14a-216">Açıklama: kaydırıcı pencere öğesi, bu stil etkin olduğunda, kesikli değer çizgisi çizgilerinin yazılım çizimini oluşturacak.</span><span class="sxs-lookup"><span data-stu-id="5d14a-216">Description: The slider widget will do software drawing of dashed tickmark lines when this style is enabled.</span></span>

<span data-ttu-id="5d14a-217">**GX_STYLE_SLIDER_VERTICAL**</span><span class="sxs-lookup"><span data-stu-id="5d14a-217">**GX_STYLE_SLIDER_VERTICAL**</span></span>
  - <span data-ttu-id="5d14a-218">Değer 0x00000800</span><span class="sxs-lookup"><span data-stu-id="5d14a-218">Value 0x00000800</span></span>
  - <span data-ttu-id="5d14a-219">Açıklama: Dikey kaydırıcı oluşturmak için bu stil bayrağını ayarlayın ve yatay kaydırıcı oluşturmak için bu stil bayrağını temizleyin.</span><span class="sxs-lookup"><span data-stu-id="5d14a-219">Description: Set this style flag to create a vertical slider, and clear this style flag to create a horizontal slider.</span></span>

<span data-ttu-id="5d14a-220">__***Sprite stilleri (yalnızca GX_SPRITE pencere öğesi türleri için geçerlidir):***__</span><span class="sxs-lookup"><span data-stu-id="5d14a-220">__***Sprite Styles (Applies only to GX_SPRITE widget types):***__</span></span>

<span data-ttu-id="5d14a-221">**GX_STYLE_SPRITE_AUTO**</span><span class="sxs-lookup"><span data-stu-id="5d14a-221">**GX_STYLE_SPRITE_AUTO**</span></span>
  - <span data-ttu-id="5d14a-222">Değer: 0x00000010</span><span class="sxs-lookup"><span data-stu-id="5d14a-222">Value: 0x00000010</span></span>
  - <span data-ttu-id="5d14a-223">Açıklama: sprite pencere öğesi GX_EVENT_SHOW olayını aldığında Sprite animasyonunun otomatik olarak çalışacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="5d14a-223">Description: Indicates the sprite animation will run automatically when the sprite widget received the GX_EVENT_SHOW event.</span></span>

<span data-ttu-id="5d14a-224">**GX_STYLE_SPRITE_LOOP**</span><span class="sxs-lookup"><span data-stu-id="5d14a-224">**GX_STYLE_SPRITE_LOOP**</span></span>
  - <span data-ttu-id="5d14a-225">Değer: 0x00000020</span><span class="sxs-lookup"><span data-stu-id="5d14a-225">Value: 0x00000020</span></span>
  - <span data-ttu-id="5d14a-226">Açıklama: Bu stille birlikte Sprite öğesi, uygulama tarafından durduruluncaya kadar Sprite animasyon kareleri aracılığıyla sürekli olarak döngü yapılır.</span><span class="sxs-lookup"><span data-stu-id="5d14a-226">Description: With this style, the sprite widget will continuously loop through sprite animation frames until the sprite is stopped by the application.</span></span>

<span data-ttu-id="5d14a-227">__***Pixelmap kaydırıcı stilleri:***__</span><span class="sxs-lookup"><span data-stu-id="5d14a-227">__***Pixelmap Slider Styles:***__</span></span>

<span data-ttu-id="5d14a-228">**GX_STYLE_TILE_BACKGROUND**</span><span class="sxs-lookup"><span data-stu-id="5d14a-228">**GX_STYLE_TILE_BACKGROUND**</span></span>
  - <span data-ttu-id="5d14a-229">Değer 0x00001000</span><span class="sxs-lookup"><span data-stu-id="5d14a-229">Value 0x00001000</span></span>
  - <span data-ttu-id="5d14a-230">Açıklama: kaydırıcı arka plan resmi, Sprite sınırlayıcı dikdörtgenini dolduracak şekilde döşenir.</span><span class="sxs-lookup"><span data-stu-id="5d14a-230">Description: The slider background image is tiled to fill the sprite bounding rectangle.</span></span> <span data-ttu-id="5d14a-231">Bu, kaydırıcı arka planını dolduracak küçük dikey veya yatay bir şeritli görüntünün kullanılmasına izin verir.</span><span class="sxs-lookup"><span data-stu-id="5d14a-231">This allows a small vertical or horizontal stripe image to be used to fill the slider background.</span></span>

<span data-ttu-id="5d14a-232">__***Ek Ilerleme çubuğu stilleri:***__</span><span class="sxs-lookup"><span data-stu-id="5d14a-232">__***Additional Progress Bar Styles:***__</span></span>

<span data-ttu-id="5d14a-233">**GX_STYLE_PROGRESS_PERCENT**</span><span class="sxs-lookup"><span data-stu-id="5d14a-233">**GX_STYLE_PROGRESS_PERCENT**</span></span>
  - <span data-ttu-id="5d14a-234">Değer: 0x00000010</span><span class="sxs-lookup"><span data-stu-id="5d14a-234">Value: 0x00000010</span></span>
  - <span data-ttu-id="5d14a-235">Açıklama: Bu stil ayarlandığında, ilerleme çubuğu, bir ham değer yerine bir yüzde olarak çubuk değeri çizer.</span><span class="sxs-lookup"><span data-stu-id="5d14a-235">Description: When this style is set, the progress bar will draw  bar value as a percentage rather than a raw value.</span></span> <span data-ttu-id="5d14a-236">Metin, ilerleme çubuğu sınırlayıcı dikdörtgende ortalanır.</span><span class="sxs-lookup"><span data-stu-id="5d14a-236">The text is centered in the progress bar bounding rectangle.</span></span>

<span data-ttu-id="5d14a-237">**GX_STYLE_PROGRESS_TEXT_DRAW**</span><span class="sxs-lookup"><span data-stu-id="5d14a-237">**GX_STYLE_PROGRESS_TEXT_DRAW**</span></span>
  - <span data-ttu-id="5d14a-238">Değer: 0x00000020</span><span class="sxs-lookup"><span data-stu-id="5d14a-238">Value: 0x00000020</span></span>
  - <span data-ttu-id="5d14a-239">Açıklama: ilerleme çubuğu içinde ortalanan ondalık metin olarak geçerli ilerleme çubuğu değerini çizin.</span><span class="sxs-lookup"><span data-stu-id="5d14a-239">Description: Draw the current progress bar value as decimal text centered within the progress bar.</span></span>

<span data-ttu-id="5d14a-240">**GX_STYLE_PROGRESS_VERTICAL**</span><span class="sxs-lookup"><span data-stu-id="5d14a-240">**GX_STYLE_PROGRESS_VERTICAL**</span></span>
  - <span data-ttu-id="5d14a-241">Değer: 0x0000040</span><span class="sxs-lookup"><span data-stu-id="5d14a-241">Value: 0x0000040</span></span>
  - <span data-ttu-id="5d14a-242">Açıklama: ilerlemenin dikey olarak yönlendirildiğini belirtin.</span><span class="sxs-lookup"><span data-stu-id="5d14a-242">Description: Indicate the progress is vertically oriented.</span></span> <span data-ttu-id="5d14a-243">Varsayılan değer yatay yöndir.</span><span class="sxs-lookup"><span data-stu-id="5d14a-243">The default is horizontal orientation.</span></span>

<span data-ttu-id="5d14a-244">**GX_STYLE_PROGRESS_SEGMENT_FILL**:</span><span class="sxs-lookup"><span data-stu-id="5d14a-244">**GX_STYLE_PROGRESS_SEGMENT_FILL**:</span></span>
  - <span data-ttu-id="5d14a-245">**Değer**: 0x00000100</span><span class="sxs-lookup"><span data-stu-id="5d14a-245">**Value**: 0x00000100</span></span>
  - <span data-ttu-id="5d14a-246">Açıklama: ilerleme çubuğu değeri, düz bir dolgu yerine bölümlenmiş dolgulu dikdörtgenlerle belirtilir.</span><span class="sxs-lookup"><span data-stu-id="5d14a-246">Description: The progress bar value is indicated with segmented filled rectangles, rather than a solid fill.</span></span>

<span data-ttu-id="5d14a-247">__***Ek radyal Ilerleme çubuğu stilleri:***__</span><span class="sxs-lookup"><span data-stu-id="5d14a-247">__***Additional Radial Progress Bar Styles:***__</span></span>

<span data-ttu-id="5d14a-248">**GX_STYLE_RADIAL_PROGRESS_ALIAS**</span><span class="sxs-lookup"><span data-stu-id="5d14a-248">**GX_STYLE_RADIAL_PROGRESS_ALIAS**</span></span>
  - <span data-ttu-id="5d14a-249">Değer: 0x00000200</span><span class="sxs-lookup"><span data-stu-id="5d14a-249">Value: 0x00000200</span></span>
  - <span data-ttu-id="5d14a-250">Açıklama: diğer ad yumuşatma fırçası stillerini kullanarak radyal ilerleme çubuğunu çizin.</span><span class="sxs-lookup"><span data-stu-id="5d14a-250">Description: Draw the radial progress bar using anti-aliased brush styles.</span></span> <span data-ttu-id="5d14a-251">Bu daha fazla CPU bant genişliği gerektirir, ancak aynı zamanda bir Nicer görünümü oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5d14a-251">This requires more CPU bandwidth but also produces a nicer appearance.</span></span> <span data-ttu-id="5d14a-252">Daha düşük performans CPU hedefleri için, bu stil bayrağını temizlemek daha hızlı çizim hızına neden olur.</span><span class="sxs-lookup"><span data-stu-id="5d14a-252">For lower performance CPU targets, clearing this style flag will result in faster drawing speed.</span></span>

<span data-ttu-id="5d14a-253">**GX_STYLE_RADIAL_PROGRESS_ROUND**</span><span class="sxs-lookup"><span data-stu-id="5d14a-253">**GX_STYLE_RADIAL_PROGRESS_ROUND**</span></span>
  - <span data-ttu-id="5d14a-254">Değer: 0x00000400</span><span class="sxs-lookup"><span data-stu-id="5d14a-254">Value: 0x00000400</span></span>
  - <span data-ttu-id="5d14a-255">Açıklama: radyal ilerleme çubuğu yay çizerken yuvarlak çizgi sonu fırça stili kullanın. Varsayılan değer bir kare çizgisi sonu olur.</span><span class="sxs-lookup"><span data-stu-id="5d14a-255">Description: Use a round line end brush style when drawing the radial progress bar arc. The default is a square line end.</span></span>

<span data-ttu-id="5d14a-256">__***Ek metin girişi stilleri:***__</span><span class="sxs-lookup"><span data-stu-id="5d14a-256">__***Additional Text Input Styles:***__</span></span>

<span data-ttu-id="5d14a-257">**GX_STYLE_ CURSOR_BLINK**</span><span class="sxs-lookup"><span data-stu-id="5d14a-257">**GX_STYLE_ CURSOR_BLINK**</span></span>
  - <span data-ttu-id="5d14a-258">Değer: 0x00000040</span><span class="sxs-lookup"><span data-stu-id="5d14a-258">Value: 0x00000040</span></span>
  - <span data-ttu-id="5d14a-259">Açıklama: metin girişi pencere öğesi imleci, faturalandırılmaktansa yanıp sönmenize ve kapanacaktır.</span><span class="sxs-lookup"><span data-stu-id="5d14a-259">Description: The text input widget cursor will flash on and off rather than being steady.</span></span>

<span data-ttu-id="5d14a-260">**GX_STYLE_ CURSOR_ALWAYS**</span><span class="sxs-lookup"><span data-stu-id="5d14a-260">**GX_STYLE_ CURSOR_ALWAYS**</span></span>
  - <span data-ttu-id="5d14a-261">Değer: 0x00000080</span><span class="sxs-lookup"><span data-stu-id="5d14a-261">Value: 0x00000080</span></span>
  - <span data-ttu-id="5d14a-262">Açıklama.</span><span class="sxs-lookup"><span data-stu-id="5d14a-262">Description.</span></span> <span data-ttu-id="5d14a-263">Metin girişi pencere öğesi imleci normalde yalnızca pencere öğesi giriş odağa sahip olduğunda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="5d14a-263">The text input widget cursor is normally only displayed when the widget owns input focus.</span></span> <span data-ttu-id="5d14a-264">Bu stil bayrağı imleci her zaman giriş odağının ne olursa olsun görünür hale getirir.</span><span class="sxs-lookup"><span data-stu-id="5d14a-264">This style flag will make the cursor always visible regardless of input focus.</span></span>

<span data-ttu-id="5d14a-265">**GX_STYLE_TEXT_INPUT_NOTIFY_ALL**</span><span class="sxs-lookup"><span data-stu-id="5d14a-265">**GX_STYLE_TEXT_INPUT_NOTIFY_ALL**</span></span>
  - <span data-ttu-id="5d14a-266">Değer: 0x00000100</span><span class="sxs-lookup"><span data-stu-id="5d14a-266">Value: 0x00000100</span></span>
  - <span data-ttu-id="5d14a-267">Açıklama: Bu stil bayrağıyla, metin girişi pencere öğesi tarafından anahtar aşağı olay her alındığında GX_EVENT_TEXT_EDITED olayı ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="5d14a-267">Description: With this style flag set the GX_EVENT_TEXT_EDITED event every time key down event is received by the text input widget.</span></span>

<span data-ttu-id="5d14a-268">__***Ek pencere stilleri:***__</span><span class="sxs-lookup"><span data-stu-id="5d14a-268">__***Additional Window Styles:***__</span></span>

<span data-ttu-id="5d14a-269">**GX_STYLE_TILE_WALLPAPER**</span><span class="sxs-lookup"><span data-stu-id="5d14a-269">**GX_STYLE_TILE_WALLPAPER**</span></span>
  - <span data-ttu-id="5d14a-270">Değer: 0x00040000</span><span class="sxs-lookup"><span data-stu-id="5d14a-270">Value: 0x00040000</span></span>
  - <span data-ttu-id="5d14a-271">Açıklama: pencere, atanan tüm duvar kağıdı görüntüsünü pencere istemci dikdörtgenini dolduracak şekilde döşemesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="5d14a-271">Description: The window will tile any assigned wallpaper image to fill the window client rectangle.</span></span>

<span data-ttu-id="5d14a-272">**GX_STYLE_AUTO_HSCROLL**</span><span class="sxs-lookup"><span data-stu-id="5d14a-272">**GX_STYLE_AUTO_HSCROLL**</span></span>
  - <span data-ttu-id="5d14a-273">Değer: 0x00100000</span><span class="sxs-lookup"><span data-stu-id="5d14a-273">Value: 0x00100000</span></span>
  - <span data-ttu-id="5d14a-274">Açıklama: gelecekte kullanılmak üzere ayrılmıştır.</span><span class="sxs-lookup"><span data-stu-id="5d14a-274">Description: Reserved for future use.</span></span>

<span data-ttu-id="5d14a-275">**GX_STYLE_AUTO_VSCROLL**</span><span class="sxs-lookup"><span data-stu-id="5d14a-275">**GX_STYLE_AUTO_VSCROLL**</span></span>
  - <span data-ttu-id="5d14a-276">Değer: 0x00200000</span><span class="sxs-lookup"><span data-stu-id="5d14a-276">Value: 0x00200000</span></span>
  - <span data-ttu-id="5d14a-277">Açıklama: gelecekte kullanılmak üzere ayrılmıştır.</span><span class="sxs-lookup"><span data-stu-id="5d14a-277">Description: Reserved for future use.</span></span>

<span data-ttu-id="5d14a-278">__***Ek menü stilleri:***__</span><span class="sxs-lookup"><span data-stu-id="5d14a-278">__***Additional Menu Styles:***__</span></span>

<span data-ttu-id="5d14a-279">**GX_STYLE_MENU_EXPANDED**</span><span class="sxs-lookup"><span data-stu-id="5d14a-279">**GX_STYLE_MENU_EXPANDED**</span></span>
  - <span data-ttu-id="5d14a-280">Değer: 0x00000010</span><span class="sxs-lookup"><span data-stu-id="5d14a-280">Value: 0x00000010</span></span>
  - <span data-ttu-id="5d14a-281">Açıklama: Accordion Menü pencere öğesi başlangıçta genişletilmiş durumda.</span><span class="sxs-lookup"><span data-stu-id="5d14a-281">Description: Accordion menu widget is initially in expanded state.</span></span>

<span data-ttu-id="5d14a-282">__***Ek ağaç görünümü stilleri:***__</span><span class="sxs-lookup"><span data-stu-id="5d14a-282">__***Additional Tree View Styles:***__</span></span>

<span data-ttu-id="5d14a-283">**GX_STYLE_TREE_VIEW_SHOW_ROOT_LINES**</span><span class="sxs-lookup"><span data-stu-id="5d14a-283">**GX_STYLE_TREE_VIEW_SHOW_ROOT_LINES**</span></span>
  - <span data-ttu-id="5d14a-284">Değer: 0x00000010</span><span class="sxs-lookup"><span data-stu-id="5d14a-284">Value: 0x00000010</span></span>
  - <span data-ttu-id="5d14a-285">Açıklama: ağaç görünümü pencere öğesi düğüm simgesinden kök ağaç düğümüne çizgiler çizmelidir.</span><span class="sxs-lookup"><span data-stu-id="5d14a-285">Description: Tree view widget should draw lines from node icon to root tree node.</span></span>

<span data-ttu-id="5d14a-286">__***Ek kaydırma çubuğu stilleri:***__</span><span class="sxs-lookup"><span data-stu-id="5d14a-286">__***Additional Scrollbar Styles:***__</span></span>

<span data-ttu-id="5d14a-287">**GX_SCROLLBAR_BACKGROUND_TILE**</span><span class="sxs-lookup"><span data-stu-id="5d14a-287">**GX_SCROLLBAR_BACKGROUND_TILE**</span></span>
  - <span data-ttu-id="5d14a-288">Değer: 0x00010000</span><span class="sxs-lookup"><span data-stu-id="5d14a-288">Value: 0x00010000</span></span>
  - <span data-ttu-id="5d14a-289">Açıklama: gelecekte kullanılmak üzere ayrılmıştır.</span><span class="sxs-lookup"><span data-stu-id="5d14a-289">Description: Reserved for future use.</span></span>

<span data-ttu-id="5d14a-290">**GX_SCROLLBAR_RELATIVE_THUMB**</span><span class="sxs-lookup"><span data-stu-id="5d14a-290">**GX_SCROLLBAR_RELATIVE_THUMB**</span></span>
  - <span data-ttu-id="5d14a-291">Değer: 0x00020000</span><span class="sxs-lookup"><span data-stu-id="5d14a-291">Value: 0x00020000</span></span>
  - <span data-ttu-id="5d14a-292">Açıklama: ScrollBar Thumb Width (yatay kaydırma çubuğu için) veya yükseklik (dikey kaydırma çubuğu için), üst pencerenin görünür alanının, en düşük ve en fazla kaydırma çubuğu aralığına göre hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="5d14a-292">Description: The scrollbar thumb width (for a horizontal scroll bar) or height (for a vertical scroll bar) are calculated based on the ratio of the visible area of the parent window to the min and max scrollbar range.</span></span>

<span data-ttu-id="5d14a-293">**GX_SCROLLBAR_END_BUTTONS**</span><span class="sxs-lookup"><span data-stu-id="5d14a-293">**GX_SCROLLBAR_END_BUTTONS**</span></span>
  - <span data-ttu-id="5d14a-294">Değer: 0x00040000</span><span class="sxs-lookup"><span data-stu-id="5d14a-294">Value: 0x00040000</span></span>
  - <span data-ttu-id="5d14a-295">Açıklama: kaydırma çubuğu, ScrollBar bölgesinin her bir ucunda düğme oluşturur ve ekler.</span><span class="sxs-lookup"><span data-stu-id="5d14a-295">Description: The scrollbar automatically creates and attaches buttons at each end of the scrollbar region.</span></span>

<span data-ttu-id="5d14a-296">**GX_SCROLLBAR_VERTICAL**</span><span class="sxs-lookup"><span data-stu-id="5d14a-296">**GX_SCROLLBAR_VERTICAL**</span></span> 
  - <span data-ttu-id="5d14a-297">Değer: 0x01000000</span><span class="sxs-lookup"><span data-stu-id="5d14a-297">Value: 0x01000000</span></span>
  - <span data-ttu-id="5d14a-298">Açıklama: kaydırma çubuğu dikey olarak yönlendirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="5d14a-298">Description: The scrollbar is vertically oriented.</span></span>

<span data-ttu-id="5d14a-299">**GX_SCROLLBAR_HORIZONTAL**</span><span class="sxs-lookup"><span data-stu-id="5d14a-299">**GX_SCROLLBAR_HORIZONTAL**</span></span>
  - <span data-ttu-id="5d14a-300">Değer: 0x02000000</span><span class="sxs-lookup"><span data-stu-id="5d14a-300">Value: 0x02000000</span></span>
  - <span data-ttu-id="5d14a-301">Açıklama: kaydırma çubuğu yatay olarak yönelimlidir.</span><span class="sxs-lookup"><span data-stu-id="5d14a-301">Description: The scrollbar is horizontally oriented.</span></span>

<span data-ttu-id="5d14a-302">__***Metin kaydırma tekerleği stilleri:***__</span><span class="sxs-lookup"><span data-stu-id="5d14a-302">__***Text Scroll Wheel Styles:***__</span></span>

<span data-ttu-id="5d14a-303">**GX_STYLE_TEXT_SCROLL_WHEEL_ROUND**</span><span class="sxs-lookup"><span data-stu-id="5d14a-303">**GX_STYLE_TEXT_SCROLL_WHEEL_ROUND**</span></span>
  - <span data-ttu-id="5d14a-304">Değer: 0x00000200</span><span class="sxs-lookup"><span data-stu-id="5d14a-304">Value: 0x00000200</span></span>
  - <span data-ttu-id="5d14a-305">Açıklama: kaydırma tekerleği, kaydırma tekerleğini yuvarlatılmış bir şekle sahip olacak şekilde görünmesini sağlamak için bir sinusoidal algoritmasını kullanır.</span><span class="sxs-lookup"><span data-stu-id="5d14a-305">Description: The scroll wheel uses a Sinusoidal algorithm to make the scroll wheel appear to have a rounded shape.</span></span> <span data-ttu-id="5d14a-306">Bu stil bayrağı, kaydırma tekerleği pencere öğesinin performansına önemli ölçüde ek yük ekleyebilir, ancak tekerlek 3B gerçekçi bir görünüm de verebilir.</span><span class="sxs-lookup"><span data-stu-id="5d14a-306">This style flag can add significant overhead to the performance of the scroll wheel widget, but can also give the wheel a 3D realistic appearance.</span></span>