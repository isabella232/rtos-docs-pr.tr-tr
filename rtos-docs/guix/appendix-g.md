---
title: Ek G-Gux yazı tipi yapısı
description: GUX yazı tipi yapısı hakkında bilgi edinin.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: b5f0232e6c21851014b85cfe7b07795062fd1e8d
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104827268"
---
# <a name="appendix-g---guix-font-structure"></a><span data-ttu-id="d2051-103">Ek G-Gux yazı tipi yapısı</span><span class="sxs-lookup"><span data-stu-id="d2051-103">Appendix G - GUIX Font Structure</span></span>

<span data-ttu-id="d2051-104">GUX yazı tipleri normalde Gux Studio uygulaması tarafından oluşturulur ve yazı tipi glifleri Gux görüntü sürücüsü tarafından işlenir.</span><span class="sxs-lookup"><span data-stu-id="d2051-104">GUIX fonts are normally produced by the GUIX Studio application, and font glyphs are rendered by the GUIX display driver.</span></span> <span data-ttu-id="d2051-105">Uygulama yazılımı yalnızca her metin görüntüleme pencere öğesinin kullanması gereken yazı tipi ve renkleri belirtmelidir.</span><span class="sxs-lookup"><span data-stu-id="d2051-105">The application software need only specify the font and colors that each text display widget should use.</span></span> <span data-ttu-id="d2051-106">GUX yazı tipi veri yapıları, tamamlanma açısından burada belgelenmiştir ve geliştiricilerin diğer yazı tiplerini Gux yazı tipi biçiminde oluşturmak veya dönüştürmek için kendi yöntemlerini oluşturmalarına olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="d2051-106">The GUIX font data structures are documented here for completeness, and to enable developers to create their own methods for generating or converting other fonts into the GUIX font format.</span></span>

<span data-ttu-id="d2051-107">Her Gux yazı tipi bir GX_FONT yapısıyla başlar.</span><span class="sxs-lookup"><span data-stu-id="d2051-107">Each GUIX font starts with a GX_FONT structure.</span></span> <span data-ttu-id="d2051-108">GX_FONT yapısı, yazı tipi içinde içerilen karakter ve yazı tipinin çizgi yüksekliği gibi genel yazı tipi parametrelerini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="d2051-108">The GX_FONT structure defines global font parameters, such as the character included within the font and the line height of the font.</span></span> <span data-ttu-id="d2051-109">GX_FONT yapısı bir GX_GLYPH yapıları dizisine işaret eder.</span><span class="sxs-lookup"><span data-stu-id="d2051-109">The GX_FONT structure points at an array of GX_GLYPH structures.</span></span> <span data-ttu-id="d2051-110">Her GX_GLYPH yapısı, belirli bir karakter glifinde genişlik, yükseklik ve taban çizgisi sapmasını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="d2051-110">Each GX_GLYPH structure defines the width, height, and baseline offset of one specific character glyph.</span></span> <span data-ttu-id="d2051-111">GX_GLYPH yapı aynı zamanda gerçek glif bit eşlem verilerini de işaret eder (boşluk karakterleri için NULL olabilir).</span><span class="sxs-lookup"><span data-stu-id="d2051-111">The GX_GLYPH structure also points to the actual glyph bitmap data (which may be NULL for whitespace characters).</span></span>

<span data-ttu-id="d2051-112">Gx_api. h içinde bulunan GX_FONT yapısı şu şekilde bildirilmiştir:</span><span class="sxs-lookup"><span data-stu-id="d2051-112">The GX_FONT structure, contained in gx_api.h, is declared as follows:</span></span>

```c
typedef struct GX_FONT_STRUCT
{
    GX_UBYTE                     gx_font_format
    GX_UBYTE                     gx_font_prespace
    GX_UBYTE                     gx_font_postspace
    GX_UBYTE                     gx_font_line_height 
    GX_UBYTE                     gx_font_baseline
    USHORT                       gx_font_first_glyph
    USHORT                       gx_font_last_glyph 
    GX_CONST GX_GLYPH           *gx_font_glyphs
    const struct GX_FONT_STRUCT *gx_font_next_page
} GX_FONT;
```

<span data-ttu-id="d2051-113">Gx_font_format alanı, gx_api. h üstbilgi dosyasında tanımlandığı şekilde piksel başına bit ve diğer bayrakları tanımlar.</span><span class="sxs-lookup"><span data-stu-id="d2051-113">The gx_font_format field defines the font bits-per-pixel and other flags, as defined in the gx_api.h header file.</span></span>

<span data-ttu-id="d2051-114">Gx_font_prespace, çok satırlı bir metin görüntüsüne her metin satırının üzerinde atlanacak piksel alanını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="d2051-114">The gx_font_prespace defines the pixel space to skip above each line of text in a multi-line text display.</span></span>

<span data-ttu-id="d2051-115">Gx_font_postspace alanı, çok satırlı bir metin görüntüsüne ait her metin satırının altına atlanacak piksel alanını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="d2051-115">The gx_font_postspace field defines the pixel space to skip below each line of text in a multi-line text display.</span></span>

<span data-ttu-id="d2051-116">Gx_font_line_height alanı, yazı tipindeki en uzun glifin yüksekliğini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="d2051-116">The gx_font_line_height field defines the height of the tallest glyph in the font.</span></span>

<span data-ttu-id="d2051-117">Gx_font_baseline alanı, en üstteki karakter piksel satırından yazı tipi taban çizgisi arasındaki mesafeyi piksel cinsinden tanımlar.</span><span class="sxs-lookup"><span data-stu-id="d2051-117">The gx_font_baseline field defines the distance, in pixels, from the top row of glyph pixels to the font baseline.</span></span>

<span data-ttu-id="d2051-118">Gx_font_first_glyph alanı, bu yazı tipi sayfasında bulunan ilk Unicode karakter kodlamasını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="d2051-118">The gx_font_first_glyph field defines the first Unicode character encoding included in this font page.</span></span>

<span data-ttu-id="d2051-119">Gx_font_last_glyph alanı, bu yazı tipi sayfasında yer alan son Unicode karakter kodlamasını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="d2051-119">The gx_font_last_glyph field defines the last Unicode character encoding included in this font page.</span></span>

<span data-ttu-id="d2051-120">Gx_font_glyphs işaretçi bir GX_GLYPH yapıları dizisine işaret eder.</span><span class="sxs-lookup"><span data-stu-id="d2051-120">The gx_font_glyphs pointer points to an array of GX_GLYPH structures.</span></span> <span data-ttu-id="d2051-121">Bu dizi, bu yazı tipi sayfasında bulunan karakter sayısına eşit olmalıdır, yani</span><span class="sxs-lookup"><span data-stu-id="d2051-121">This array must be equal in size to the number of characters contained on this font page, i.e</span></span> <span data-ttu-id="d2051-122">(gx_font_last_glyph – gx_font_first_glyph) + 1.</span><span class="sxs-lookup"><span data-stu-id="d2051-122">(gx_font_last_glyph – gx_font_first_glyph) + 1.</span></span>

<span data-ttu-id="d2051-123">Gx_font_next_page üyesi birden çok sayfa yazı tipi için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d2051-123">The gx_font_next_page member is used for multiple page fonts.</span></span> <span data-ttu-id="d2051-124">Birden çok sayfa yazı tipi, genişletilmiş karakter kümeleri için ve GX_GLYPH yapısı dizilerinin boyutunu iyileştirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d2051-124">Multiple page fonts are used for extended character sets and to optimize the size of the GX_GLYPH structure arrays.</span></span> <span data-ttu-id="d2051-125">Yazı tipinin tüm karakterleri bir yazı tipi sayfasında yer alıyorsa veya söz konusu yazı tipinin son sayfası ise gx_font_next_page üyesi GX_NULL olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="d2051-125">If all of the characters of the font are contained within one font page, or if this is the last page of the font in question, the gx_font_next_page member is set to GX_NULL.</span></span>

<span data-ttu-id="d2051-126">Yukarıda belirtildiği gibi, yukarıdaki GX_FONT yapısı bir GX_GLYPHS yapıları dizisine yönelik bir işaretçi içerir.</span><span class="sxs-lookup"><span data-stu-id="d2051-126">As noted above, the GX_FONT structure above contains a pointer to an array of GX_GLYPHS structures.</span></span> <span data-ttu-id="d2051-127">Yazı tipi sayfasındaki her karakter için bir GX_GLYPH yapısı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d2051-127">There must be one GX_GLYPH structure for each character on the font page.</span></span> <span data-ttu-id="d2051-128">GX_GLYPH yapısı şu şekilde tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="d2051-128">The GX_GLYPH structure is defined as:</span></span>

```c
typedef struct GX_GLYPH_STRUCT
{
    GX_CONST GX_UBYTE *gx_glyph_map;
    GX_BYTE            gx_glyph_ascent;
    GX_BYTE            gx_glyph_descent;
    GX_BYTE            gx_glyph_advance;
    GX_BYTE            gx_glyph_leading;
    GX_UBYTE           gx_glyph_width;
    GX_UBYTE           gx_glyph_height;
} GX_GLYPH;
```

<span data-ttu-id="d2051-129">Gx_glyph_map işaretçi, glif bit eşlemini işaret eder.</span><span class="sxs-lookup"><span data-stu-id="d2051-129">The gx_glyph_map pointer points to the glyph bitmap.</span></span> <span data-ttu-id="d2051-130">Bu işaretçi, boşluk karakterleri için GX_NULL olabilir.</span><span class="sxs-lookup"><span data-stu-id="d2051-130">This pointer may be GX_NULL for whitespace characters.</span></span> <span data-ttu-id="d2051-131">Bit eşlem verileri 1 BPP, 2 BPP, 4 BPP veya 8 BPP alfa değeri olarak kodlanır.</span><span class="sxs-lookup"><span data-stu-id="d2051-131">The bitmap data is encoded as 1 bpp, 2 bpp, 4 bpp, or 8 bpp alpha values.</span></span> <span data-ttu-id="d2051-132">1 bitlik veriler için 1 değeri, pikselin ön plan rengine yazılması gerektiğini gösterir ve 0 değeri pikselin saydam olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="d2051-132">For 1 bit data, a value of 1 indicates that the pixel should be written in the foreground color, and a value of 0 indicates that the pixel is transparent.</span></span> <span data-ttu-id="d2051-133">8 bit veriler için değerler 0 (tamamen saydam) ile 255 (tamamen opag) arasındadır.</span><span class="sxs-lookup"><span data-stu-id="d2051-133">For 8 bit data, the values range from 0 (fully transparent) to 255 (fully opague).</span></span> <span data-ttu-id="d2051-134">Tüm ara değer, kenar yumuşatma uygulanmış yazı tipleri için bir karıştırma değeri temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d2051-134">All intermediate value represent a blending value for anti-aliased fonts.</span></span> <span data-ttu-id="d2051-135">Glif bit eşlem verileri her zaman, 8 ' den az BPP veri değeri kullanan biçimler için tam bayt hizalamasına doldurulur.</span><span class="sxs-lookup"><span data-stu-id="d2051-135">The glyph bitmap data is always padded to full byte alignment for formats using less than 8bpp data values.</span></span>

<span data-ttu-id="d2051-136">Gx_glyph_ascent ve gx_glyph_descent değerleri, yazı tipi taban çizgisine göre glifi dikey olarak konumlandırır.</span><span class="sxs-lookup"><span data-stu-id="d2051-136">The gx_glyph_ascent and gx_glyph_descent values position the glyph vertically with respect to the font baseline.</span></span>

<span data-ttu-id="d2051-137">Gx_glyph_width ve gx_glyph_height değerleri, glif bit eşlem verilerinin boyutunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="d2051-137">The gx_glyph_width and gx_glyph_height values specify the size of the glyph bitmap data.</span></span>

<span data-ttu-id="d2051-138">Gx_glyph_advance değeri, glifi çizdikten sonra çizim konumunu ilerletmek için piksel genişliğini belirtir (glif genişliğine eşit olmayabilir).</span><span class="sxs-lookup"><span data-stu-id="d2051-138">The gx_glyph_advance value specifies the pixel width to advance the drawing position after drawing the glyph (this may not be equal to the glyph width).</span></span>

<span data-ttu-id="d2051-139">Gx_glyph_leading değeri, glifi işlemeden önce x yönünde ilerlemek için pikselleri belirtir.</span><span class="sxs-lookup"><span data-stu-id="d2051-139">The gx_glyph_leading value specifies the pixels to advance in the x-direction prior to rendering the glyph.</span></span>