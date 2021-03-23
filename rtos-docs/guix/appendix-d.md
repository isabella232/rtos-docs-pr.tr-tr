---
title: Ek D-Gux fırçası, tuval ve gradyan öznitelikleri
description: GUX fırçası, tuval ve gradyan öznitelikleri hakkında bilgi edinin.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 19c0687a54be244ae395124664b4b6da0f4e90b6
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104827275"
---
# <a name="appendix-d---guix-brush-canvas-and-gradient-attributes"></a><span data-ttu-id="e35ee-103">Ek D-Gux fırçası, tuval ve gradyan öznitelikleri</span><span class="sxs-lookup"><span data-stu-id="e35ee-103">Appendix D - GUIX Brush, Canvas and Gradient Attributes</span></span>

<span data-ttu-id="e35ee-104">__**Fırça stilleri:**__</span><span class="sxs-lookup"><span data-stu-id="e35ee-104">__**Brush Styles:**__</span></span>

<span data-ttu-id="e35ee-105">**GX_BRUSH_OUTLINE**</span><span class="sxs-lookup"><span data-stu-id="e35ee-105">**GX_BRUSH_OUTLINE**</span></span>
- <span data-ttu-id="e35ee-106">Değer: 0x0000</span><span class="sxs-lookup"><span data-stu-id="e35ee-106">Value: 0x0000</span></span>
- <span data-ttu-id="e35ee-107">Açıklama: Bu fırça stili, gx_canvas_rectangle_draw veya gx_canvas_polygon_draw gibi şekil çizim işlevleri için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="e35ee-107">Description: This brush style applies to shape drawing functions such as gx_canvas_rectangle_draw or gx_canvas_polygon_draw.</span></span> <span data-ttu-id="e35ee-108">Bu stil, isteğe bağlı olarak doldurulmanın yanı sıra şeklin ana hatlarıyla toplanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e35ee-108">This style indicateds the shape should be outlined, in addition to optionally being fill.</span></span> <span data-ttu-id="e35ee-109">GX_BRUSH_OUTLINE stili ayarlanmışsa ve GX_BRSUH_SOLID_FILL silinirse, şekil yalnızca Seviyelendirilmiş olur.</span><span class="sxs-lookup"><span data-stu-id="e35ee-109">If the GX_BRUSH_OUTLINE style is set and the GX_BRSUH_SOLID_FILL is cleared, the shape is only outlined.</span></span>

<span data-ttu-id="e35ee-110">**GX_BRUSH_SOLID_FILL**</span><span class="sxs-lookup"><span data-stu-id="e35ee-110">**GX_BRUSH_SOLID_FILL**</span></span>
- <span data-ttu-id="e35ee-111">Değer: 0x0001</span><span class="sxs-lookup"><span data-stu-id="e35ee-111">Value: 0x0001</span></span>
- <span data-ttu-id="e35ee-112">Açıklama: Bu fırça stili şekil çizim işlevlerine uygulanır ve istenen şeklin geçerli fırça dolgusu rengi kullanılarak bir düz renkle doldurulması gerektiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="e35ee-112">Description: This brush style applies to shape drawing functions, and indicates that the requested shape should be filled with a solid color using the current brush fill color.</span></span>

<span data-ttu-id="e35ee-113">**GX_BRUSH_PIXELMAP_FILL**</span><span class="sxs-lookup"><span data-stu-id="e35ee-113">**GX_BRUSH_PIXELMAP_FILL**</span></span>
- <span data-ttu-id="e35ee-114">Değer: 0x0002</span><span class="sxs-lookup"><span data-stu-id="e35ee-114">Value: 0x0002</span></span>
- <span data-ttu-id="e35ee-115">Açıklama: Bu fırça stili şekil çizim işlevlerine uygulanır ve istenen şeklin geçerli fırça pixelmap ile doldurulmuş olması gerektiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="e35ee-115">Description: This brush style applies to shape drawing functions, and indicates that the requested shape should be pattern filled with the current brush pixelmap.</span></span>

<span data-ttu-id="e35ee-116">**GX_BRUSH_ALIAS**</span><span class="sxs-lookup"><span data-stu-id="e35ee-116">**GX_BRUSH_ALIAS**</span></span>
- <span data-ttu-id="e35ee-117">Değer: 0x0004</span><span class="sxs-lookup"><span data-stu-id="e35ee-117">Value: 0x0004</span></span>
- <span data-ttu-id="e35ee-118">Açıklama: Bu fırça stili tüm çizgi çizme ve şekil anahatları için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="e35ee-118">Description: This brush style applies to all line drawing and shape outlines.</span></span> <span data-ttu-id="e35ee-119">Bu bayrak ayarlandıysa, satırlar ve anahatlar daha doğru bir şekilde çizilmiştir, ancak aynı zamanda diğer ad yumuşatma daha fazla olan çizim algoritmalarından daha fazla zaman alır.</span><span class="sxs-lookup"><span data-stu-id="e35ee-119">If this flag is set, lines and outlines are drawing with the more accurate but also more time consuming anti-aliased drawing algorithms.</span></span> <span data-ttu-id="e35ee-120">Bu stil bayrağı yalnızca 16 bit renk derinlikleri ve üzeri için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e35ee-120">This style flag is only used for 16-bpp color depths and higher.</span></span>

<span data-ttu-id="e35ee-121">**GX_BRUSH_UNDERLINE**</span><span class="sxs-lookup"><span data-stu-id="e35ee-121">**GX_BRUSH_UNDERLINE**</span></span>
- <span data-ttu-id="e35ee-122">Değer: 0x0008</span><span class="sxs-lookup"><span data-stu-id="e35ee-122">Value: 0x0008</span></span>
- <span data-ttu-id="e35ee-123">Açıklama: Bu bayrak metin çizime uygulanır ve sonraki metnin çizilebileceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="e35ee-123">Description: This flag applies to text drawing, and indicates that subsequent text drawn should be underlined.</span></span>

<span data-ttu-id="e35ee-124">**GX_BRUSH_ROUND**</span><span class="sxs-lookup"><span data-stu-id="e35ee-124">**GX_BRUSH_ROUND**</span></span>
- <span data-ttu-id="e35ee-125">Değer: 0x0010</span><span class="sxs-lookup"><span data-stu-id="e35ee-125">Value: 0x0010</span></span>
- <span data-ttu-id="e35ee-126">Açıklama: Bu bayrak, çizgi çizme için geçerlidir ve çizgi uçlarının varsayılan kare şekli yerine bir yuvarlak veya dairesel şekille çizildiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="e35ee-126">Description: This flag applies to line drawing, and indicates that line ends are drawn with a round or circular shape, rather than the default square shape.</span></span>

<span data-ttu-id="e35ee-127">__**Tuval bayrakları:**__</span><span class="sxs-lookup"><span data-stu-id="e35ee-127">__**Canvas Flags:**__</span></span>

<span data-ttu-id="e35ee-128">**GX_CANVAS_SIMPLE**</span><span class="sxs-lookup"><span data-stu-id="e35ee-128">**GX_CANVAS_SIMPLE**</span></span>
- <span data-ttu-id="e35ee-129">Değer: 0x01</span><span class="sxs-lookup"><span data-stu-id="e35ee-129">Value: 0x01</span></span>
- <span data-ttu-id="e35ee-130">Açıklama: ekran çizimini devre dışı bırakmak için kullanılan bir bellek tuvali.</span><span class="sxs-lookup"><span data-stu-id="e35ee-130">Description: A memory canvas which is used to off-screen drawing.</span></span>

<span data-ttu-id="e35ee-131">**GX_CANVAS_MANAGED**</span><span class="sxs-lookup"><span data-stu-id="e35ee-131">**GX_CANVAS_MANAGED**</span></span>
- <span data-ttu-id="e35ee-132">Değer: 0x02</span><span class="sxs-lookup"><span data-stu-id="e35ee-132">Value: 0x02</span></span>
- <span data-ttu-id="e35ee-133">Açıklama: Bileşik yapı sürecinin bir parçası olarak veya tek tuvalli mimarilere yönelik arabellek geçiş işleminin bir parçası olarak etkin ekranı otomatik olarak temizlenen bir tuval.</span><span class="sxs-lookup"><span data-stu-id="e35ee-133">Description: A canvas which automatically flushed to the active display, either as part of the composite building process or as part of the buffer toggle operation for single-canvas architectures.</span></span>

<span data-ttu-id="e35ee-134">**GX_CANVAS_VISIBLE**</span><span class="sxs-lookup"><span data-stu-id="e35ee-134">**GX_CANVAS_VISIBLE**</span></span>
- <span data-ttu-id="e35ee-135">Değer: 0x04</span><span class="sxs-lookup"><span data-stu-id="e35ee-135">Value: 0x04</span></span>
- <span data-ttu-id="e35ee-136">Açıklama: Bu bayrak, tuval çizim içeriklerinin kaybedilmesi gerekmeden bir tuvali açmak ve kapatmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e35ee-136">Description: This flag can be used to turn on and off a canvas, without losing the canvas drawing contents.</span></span>

<span data-ttu-id="e35ee-137">**GX_CANVAS_MODIFIED**</span><span class="sxs-lookup"><span data-stu-id="e35ee-137">**GX_CANVAS_MODIFIED**</span></span>
- <span data-ttu-id="e35ee-138">Değer: 0x08</span><span class="sxs-lookup"><span data-stu-id="e35ee-138">Value: 0x08</span></span>
- <span data-ttu-id="e35ee-139">Açıklama: gelecekte kullanılmak üzere ayrılmıştır.</span><span class="sxs-lookup"><span data-stu-id="e35ee-139">Description: Reserved for future use.</span></span>

<span data-ttu-id="e35ee-140">**GX_CANVAS_COMPOSITE**</span><span class="sxs-lookup"><span data-stu-id="e35ee-140">**GX_CANVAS_COMPOSITE**</span></span>
- <span data-ttu-id="e35ee-141">Değer: 0x20</span><span class="sxs-lookup"><span data-stu-id="e35ee-141">Value: 0x20</span></span>
- <span data-ttu-id="e35ee-142">Açıklama: Bu bayrak, uygulama tarafından, birden çok yönetilen ve bileşik tuvalde bileşik bir sistem olan bir çoklu tuval sistemi yapılandırırken kullanılır ve bileşik donanım çerçeve arabelleğine dayalıdır.</span><span class="sxs-lookup"><span data-stu-id="e35ee-142">Description: This flag is used by the application when configuring a multiple-canvas system which will composite multiple managed canvases into the composite canvas, and the composite is the driven to the hardware frame buffer.</span></span>

<span data-ttu-id="e35ee-143">__**Gradyan türleri:**__</span><span class="sxs-lookup"><span data-stu-id="e35ee-143">__**Gradient Types:**__</span></span>

<span data-ttu-id="e35ee-144">**GX_GRADIENT_TYPE_VERTICAL**</span><span class="sxs-lookup"><span data-stu-id="e35ee-144">**GX_GRADIENT_TYPE_VERTICAL**</span></span>
- <span data-ttu-id="e35ee-145">Değer: 0x01</span><span class="sxs-lookup"><span data-stu-id="e35ee-145">Value: 0x01</span></span>
- <span data-ttu-id="e35ee-146">Açıklama: dikey bir harflerden oluşan harita gradyanı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e35ee-146">Description: Creates a vertical alphamap gradient.</span></span>

<span data-ttu-id="e35ee-147">**GX_GRADIENT_TYPE_ALPHA**</span><span class="sxs-lookup"><span data-stu-id="e35ee-147">**GX_GRADIENT_TYPE_ALPHA**</span></span>
- <span data-ttu-id="e35ee-148">Değer: 0x02</span><span class="sxs-lookup"><span data-stu-id="e35ee-148">Value: 0x02</span></span>
- <span data-ttu-id="e35ee-149">Açıklama: Alfa harita stil degradesini oluşturma.</span><span class="sxs-lookup"><span data-stu-id="e35ee-149">Description: Creats an alpha-map style gradient.</span></span> <span data-ttu-id="e35ee-150">Bu, şu anda desteklenen tek degrade stilidir.</span><span class="sxs-lookup"><span data-stu-id="e35ee-150">This is currently the only gradient style supported.</span></span>

<span data-ttu-id="e35ee-151">**GX_GRADIENT_TYPE_MIRROR**</span><span class="sxs-lookup"><span data-stu-id="e35ee-151">**GX_GRADIENT_TYPE_MIRROR**</span></span>
- <span data-ttu-id="e35ee-152">Değer: 0x04</span><span class="sxs-lookup"><span data-stu-id="e35ee-152">Value: 0x04</span></span>
- <span data-ttu-id="e35ee-153">Açıklama: Bu bayrak, degradenin genişlik/yükseklik aralığının ortasında üst sınır olmayacağını ve sağ/alt kenara ulaşan başlangıç değerine geri döneceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="e35ee-153">Description: This flag indicates that the gradient should peak at the center of the width/height range, and return to the starting value as it reaches the right/bottom edge.</span></span> <span data-ttu-id="e35ee-154">Bu stil bayrağı olmadan gradyan, GX_GRADIENT_TYPE_VERTICAL bayrağına bağlı olarak yukarıdan aşağıya veya soldan sağa doğrusal bir gradyan olur.</span><span class="sxs-lookup"><span data-stu-id="e35ee-154">Without this style flag, the gradient will be a linear gradient from top-to-bottom or left-to-right, depending on the GX_GRADIENT_TYPE_VERTICAL flag.</span></span>