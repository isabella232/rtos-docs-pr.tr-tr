---
title: Ek I-Gux bilgi yapıları
description: GUX bilgi yapıları hakkında bilgi edinin.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: dc7775cdde8f1aa89ca650561713f54ac6c069eb
ms.sourcegitcommit: 60ad844b58639d88830f2660ab0c4ff86b92c10f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2021
ms.locfileid: "106550227"
---
# <a name="appendix-i---guix-information-structures"></a><span data-ttu-id="365fd-103">Ek I-Gux bilgi yapıları</span><span class="sxs-lookup"><span data-stu-id="365fd-103">Appendix I - GUIX Information Structures</span></span> 

## <a name="gx_bidi_text_info"></a><span data-ttu-id="365fd-104">GX_BIDI_TEXT_INFO</span><span class="sxs-lookup"><span data-stu-id="365fd-104">GX_BIDI_TEXT_INFO</span></span> 

### <a name="definition"></a><span data-ttu-id="365fd-105">Tanım</span><span class="sxs-lookup"><span data-stu-id="365fd-105">Definition</span></span>

```c
typedef struct GX_BIDI_TEXT_INFO_STRUCT
{
    GX_STRING gx_bidi_text_info_text;
    GX_FONT  *gx_bidi_text_info_font;
    GX_VALUE  gx_bidi_text_info_display_width;
} GX_BIDI_TEXT_INFO;
```
| <span data-ttu-id="365fd-106">Üyeler</span><span class="sxs-lookup"><span data-stu-id="365fd-106">Members</span></span> | <span data-ttu-id="365fd-107">Açıklama</span><span class="sxs-lookup"><span data-stu-id="365fd-107">Description</span></span> |
| ---------------------------------- | ---------------------------------------------------------- |
| <span data-ttu-id="365fd-108">**gx_bidi_text_info_text**</span><span class="sxs-lookup"><span data-stu-id="365fd-108">**gx_bidi_text_info_text**</span></span>               | <span data-ttu-id="365fd-109">Yeniden sıralama için metin</span><span class="sxs-lookup"><span data-stu-id="365fd-109">Text for reordering</span></span> |
| <span data-ttu-id="365fd-110">**gx_bidi_text_info_font**</span><span class="sxs-lookup"><span data-stu-id="365fd-110">**gx_bidi_text_info_font**</span></span>               | <span data-ttu-id="365fd-111">Metni göstermek için kullanılan yazı tipi, satır sonu gerekmiyorsa GX_NULL olarak ayarlayın</span><span class="sxs-lookup"><span data-stu-id="365fd-111">Font used to display text, set it to GX_NULL if line breaking is not needed</span></span> |
| <span data-ttu-id="365fd-112">**gx_bidi_text_info_display_width**</span><span class="sxs-lookup"><span data-stu-id="365fd-112">**gx_bidi_text_info_display_width**</span></span>      | <span data-ttu-id="365fd-113">Görüntüleme için kullanılabilir genişlik, satır sonu gerekmiyorsa-1 olarak ayarlayın</span><span class="sxs-lookup"><span data-stu-id="365fd-113">Available width for displaying, set it to -1 if line breaking is not needed</span></span> |

## <a name="gx_bidi_resolved_text_info"></a><span data-ttu-id="365fd-114">GX_BIDI_RESOLVED_TEXT_INFO</span><span class="sxs-lookup"><span data-stu-id="365fd-114">GX_BIDI_RESOLVED_TEXT_INFO</span></span> 

### <a name="definition"></a><span data-ttu-id="365fd-115">Tanım</span><span class="sxs-lookup"><span data-stu-id="365fd-115">Definition</span></span>

```c
typedef struct GX_BIDI_RESOLVED_TEXT_INFO_STRUCT
{
    GX_STRING                                *gx_bidi_resolved_text_info_text;
    UINT                                      gx_bidi_resolved_text_info_total_lines;
    struct GX_BIDI_RESOLVED_TEXT_INFO_STRUCT *gx_bidi_resolved_text_info_next;
} GX_BIDI_RESOLVED_TEXT_INFO;
```

| <span data-ttu-id="365fd-116">Üyeler</span><span class="sxs-lookup"><span data-stu-id="365fd-116">Members</span></span> | <span data-ttu-id="365fd-117">Açıklama</span><span class="sxs-lookup"><span data-stu-id="365fd-117">Description</span></span> |
| ---------------------------------- | ---------------------------------------------------------- |
| <span data-ttu-id="365fd-118">**gx_bidi_resolved_text_info_text**</span><span class="sxs-lookup"><span data-stu-id="365fd-118">**gx_bidi_resolved_text_info_text**</span></span>             | <span data-ttu-id="365fd-119">Yeniden sıralanan bidi metni dizisine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="365fd-119">Pointer to the array of reordered bidi text</span></span> |
| <span data-ttu-id="365fd-120">**gx_bidi_resolved_text_info_total_lines**</span><span class="sxs-lookup"><span data-stu-id="365fd-120">**gx_bidi_resolved_text_info_total_lines**</span></span>      | <span data-ttu-id="365fd-121">Tek bir paragraf için çözülen çift yönlü metnin toplam satırları</span><span class="sxs-lookup"><span data-stu-id="365fd-121">Total lines of resolved bidi text for one paragraph</span></span> |
| <span data-ttu-id="365fd-122">**gx_bidi_resolved_text_info_next**</span><span class="sxs-lookup"><span data-stu-id="365fd-122">**gx_bidi_resolved_text_info_next**</span></span>             | <span data-ttu-id="365fd-123">Sonraki paragraf için çift yönlü metin bilgileri çözüldü</span><span class="sxs-lookup"><span data-stu-id="365fd-123">Resolved bidi text information for the next paragraph</span></span> |

## <a name="gx_circular_gauge_info"></a><span data-ttu-id="365fd-124">GX_CIRCULAR_GAUGE_INFO</span><span class="sxs-lookup"><span data-stu-id="365fd-124">GX_CIRCULAR_GAUGE_INFO</span></span>

### <a name="definition"></a><span data-ttu-id="365fd-125">Tanım</span><span class="sxs-lookup"><span data-stu-id="365fd-125">Definition</span></span>

```c
typedef struct GX_CIRCULAR_GAUGE_INFO_STRUCT
{
    INT             gx_circular_gauge_info_animation_steps;
    INT             gx_circular_gauge_info_animation_delay;
    GX_VALUE        gx_circular_gauge_info_needle_xpos;
    GX_VALUE        gx_circular_gauge_info_needle_ypos;
    GX_VALUE        gx_circular_gauge_info_needle_xcor;
    GX_VALUE        gx_circular_gauge_info_needle_ycor;
    GX_RESOURCE_ID  gx_circular_gauge_info_needle_pixelmap;
} GX_CIRCULAR_GAUGE_INFO;
```

| <span data-ttu-id="365fd-126">Üyeler</span><span class="sxs-lookup"><span data-stu-id="365fd-126">Members</span></span> | <span data-ttu-id="365fd-127">Açıklama</span><span class="sxs-lookup"><span data-stu-id="365fd-127">Description</span></span> |
| ------------------------------------------------ | -------------------------------------------- |
| <span data-ttu-id="365fd-128">**gx_circular_gauge_info_animation_steps**</span><span class="sxs-lookup"><span data-stu-id="365fd-128">**gx_circular_gauge_info_animation_steps**</span></span>       | <span data-ttu-id="365fd-129">Geçerli iğne açısına göre yeni, atanan iğne açısına geçiş yaparken, iğne 'nin hareket ettirme toplam adım sayısı</span><span class="sxs-lookup"><span data-stu-id="365fd-129">Total steps the needle will travel through when moving from the current needle angle to a newly assigned needle angle</span></span> |
| <span data-ttu-id="365fd-130">**gx_circular_gauge_info_animation_delay**</span><span class="sxs-lookup"><span data-stu-id="365fd-130">**gx_circular_gauge_info_animation_delay**</span></span>       | <span data-ttu-id="365fd-131">Animasyon adımları arasındaki gecikmede Gux saat Ticks sayısı</span><span class="sxs-lookup"><span data-stu-id="365fd-131">The number of GUIX clock ticks to delay between animation steps</span></span> |
| <span data-ttu-id="365fd-132">**gx_circular_gauge_info_needle_xpos**</span><span class="sxs-lookup"><span data-stu-id="365fd-132">**gx_circular_gauge_info_needle_xpos**</span></span>           | <span data-ttu-id="365fd-133">Ölçer pencere öğesinin solundaki uzaklık, ölçer iğne 'nin ortasına kadar olan mesafe</span><span class="sxs-lookup"><span data-stu-id="365fd-133">The distance from the left of the gauge widget to the center-of-rotation of the gauge needle</span></span> |
| <span data-ttu-id="365fd-134">**gx_circular_gauge_info_needle_ypos**</span><span class="sxs-lookup"><span data-stu-id="365fd-134">**gx_circular_gauge_info_needle_ypos**</span></span>           | <span data-ttu-id="365fd-135">Ölçer pencere öğesinin en üstünden ölçer iğne 'nin ortasına olan uzaklık</span><span class="sxs-lookup"><span data-stu-id="365fd-135">The distance from the top of the gauge widget to the center-of-rotation of the gauge needle</span></span> |
| <span data-ttu-id="365fd-136">**gx_circular_gauge_info_needle_xcor**</span><span class="sxs-lookup"><span data-stu-id="365fd-136">**gx_circular_gauge_info_needle_xcor**</span></span>           | <span data-ttu-id="365fd-137">İğne resminin solundaki mesafe, ölçer iğne 'nin ortasına kadar</span><span class="sxs-lookup"><span data-stu-id="365fd-137">The distance from the left of the needle image to the center-of-rotation of the gauge needle</span></span> |
| <span data-ttu-id="365fd-138">**gx_circular_gauge_info_needle_ycor**</span><span class="sxs-lookup"><span data-stu-id="365fd-138">**gx_circular_gauge_info_needle_ycor**</span></span>           | <span data-ttu-id="365fd-139">İğne resminin en üstünden ölçer iğne 'nin ortasına kadar olan mesafe</span><span class="sxs-lookup"><span data-stu-id="365fd-139">The distance from the top of the needle image to the center-of-rotation of the gauge needle</span></span> |
| <span data-ttu-id="365fd-140">**gx_circular_gauge_info_needle_pixelmap**</span><span class="sxs-lookup"><span data-stu-id="365fd-140">**gx_circular_gauge_info_needle_pixelmap**</span></span>       | <span data-ttu-id="365fd-141">Ölçer iğne çizmek için kullanılacak olan pixelmap 'in kaynak KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="365fd-141">Resource ID of the pixelmap which will be used to draw the gauge needle.</span></span> <span data-ttu-id="365fd-142">Bu görüntü ölçer pencere öğesinin gerektiği şekilde döndürüldüğü şekilde döndürülecektir ve ölçer iğne herhangi bir konumda görüntülenir</span><span class="sxs-lookup"><span data-stu-id="365fd-142">This image will be rotated as needed by the gauge widget to display the gauge needle in any position</span></span> |

<span data-ttu-id="365fd-143">Aşağıdaki diyagramda XPos, YPos ve xcor ycor koordinatları gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="365fd-143">The diagram below illustrates the xpos, ypos, and xcor, ycor coordinates:</span></span>

![Iğne Y ve X koordinatları diyagramı](./media/guix/image8.png)

## <a name="gx_line_chart_info"></a><span data-ttu-id="365fd-145">GX_LINE_CHART_INFO</span><span class="sxs-lookup"><span data-stu-id="365fd-145">GX_LINE_CHART_INFO</span></span>

### <a name="definition"></a><span data-ttu-id="365fd-146">Tanım</span><span class="sxs-lookup"><span data-stu-id="365fd-146">Definition</span></span>

```c
typedef struct GX_LINE_CHART_INFO_STRUCT
{
    INT            gx_line_chart_min_val;
    INT            gx_line_chart_max_val;
    INT           *gx_line_chart_data;
    GX_VALUE       gx_line_left_margin;
    GX_VALUE       gx_line_top_margin;
    GX_VALUE       gx_line_right_margin;
    GX_VALUE       gx_line_bottom_margin;
    GX_VALUE       gx_line_chart_max_data_count;
    GX_VALUE       gx_line_chart_active_data_count;
    GX_VALUE       gx_line_chart_axis_line_width;
    GX_VALUE       gx_line_chart_data_line_width;
    GX_RESOURCE_ID gx_line_chart_axis_color;
    GX_RESOURCE_ID gx_line_chart_line_color;
} GX_LINE_CHART_INFO;
```

| <span data-ttu-id="365fd-147">Üyeler</span><span class="sxs-lookup"><span data-stu-id="365fd-147">Members</span></span> | <span data-ttu-id="365fd-148">Açıklama</span><span class="sxs-lookup"><span data-stu-id="365fd-148">Description</span></span> |
| ---------------------------------- | ---------------------------------------------------------- |
| <span data-ttu-id="365fd-149">**gx_line_chart_min_val**</span><span class="sxs-lookup"><span data-stu-id="365fd-149">**gx_line_chart_min_val**</span></span>          | <span data-ttu-id="365fd-150">Ölçeklendirmeyi hesaplamak için kullanılan minimum veri değeri</span><span class="sxs-lookup"><span data-stu-id="365fd-150">The minimum data value, which is used to calculate scaling</span></span>
| <span data-ttu-id="365fd-151">**gx_line_chart_max_val**</span><span class="sxs-lookup"><span data-stu-id="365fd-151">**gx_line_chart_max_val**</span></span>          | <span data-ttu-id="365fd-152">Ölçeklendirmeyi hesaplamak için kullanılan maksimum veri değeri</span><span class="sxs-lookup"><span data-stu-id="365fd-152">The maximum data value, which is used to calculate scaling</span></span> |
| <span data-ttu-id="365fd-153">**gx_line_chart_data**</span><span class="sxs-lookup"><span data-stu-id="365fd-153">**gx_line_chart_data**</span></span>             | <span data-ttu-id="365fd-154">Tamsayı değerleri dizisine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="365fd-154">Pointer to an array of integer values.</span></span> <span data-ttu-id="365fd-155">Bunlar çizgi grafik pencere öğesi tarafından çizilen tamsayı değerlerdir</span><span class="sxs-lookup"><span data-stu-id="365fd-155">These are the integer values plotted by the line chart widget</span></span> |
| <span data-ttu-id="365fd-156">**gx_line_ <side> _margin**</span><span class="sxs-lookup"><span data-stu-id="365fd-156">**gx_line_<side>_margin**</span></span>          | <span data-ttu-id="365fd-157">Grafik penceresi dış alanının gerçek grafik işleme alanına göre sınırı.</span><span class="sxs-lookup"><span data-stu-id="365fd-157">The offset from the chart window outer bound to the actual chart rendering area.</span></span> <span data-ttu-id="365fd-158">Grafik ekseni ve veri satırı her zaman bu iç sınır içinde çizilir. Bu, uygulamanın grafik penceresi içinde, ancak char grafikalanı dışında Etiketler ve diğer bilgiler çizmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="365fd-158">The chart axis and data line are always plotted within this inner boundary, which allows the application to draw labels and other information inside the chart window but outside the char graphing area</span></span> |
| <span data-ttu-id="365fd-159">**gx_line_chart_max_data_count**</span><span class="sxs-lookup"><span data-stu-id="365fd-159">**gx_line_chart_max_data_count**</span></span>   | <span data-ttu-id="365fd-160">Mevcut olabilecek veri değerlerinin sayısı.</span><span class="sxs-lookup"><span data-stu-id="365fd-160">The number of data values which may be present.</span></span> <span data-ttu-id="365fd-161">Bu parametre, veri noktalarını çizmek için x ekseninin ölçeğini veya aralığını hesaplamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="365fd-161">This parameter is used for calculating the x-axis scaling or interval for plotting data points.</span></span> |
| <span data-ttu-id="365fd-162">**gx_line_active_data_count**</span><span class="sxs-lookup"><span data-stu-id="365fd-162">**gx_line_active_data_count**</span></span>      | <span data-ttu-id="365fd-163">Veri dizisinde gerçekten mevcut olan veri değerlerinin sayısı.</span><span class="sxs-lookup"><span data-stu-id="365fd-163">The number of data values that actually present in the data array.</span></span> <span data-ttu-id="365fd-164">Çizgi grafik, en fazla 100 değer çizmek için ölçeklendirilebilir (örneğin), ancak belirli bir güncelleştirmede daha az sayıda veri değeri bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="365fd-164">A line chart may be scaled to draw a maximum of 100 values (for example), but on any particular update a smaller number of data values may actually be present.</span></span> |
| <span data-ttu-id="365fd-165">**gx_line_axis_line_width**</span><span class="sxs-lookup"><span data-stu-id="365fd-165">**gx_line_axis_line_width**</span></span>        | <span data-ttu-id="365fd-166">Yatay ve dikey ekseni çizmek için kullanılan çizginin genişliği</span><span class="sxs-lookup"><span data-stu-id="365fd-166">Width of the line used to draw the horizontal and vertical axis</span></span> |
| <span data-ttu-id="365fd-167">**gx_line_data_line_width**</span><span class="sxs-lookup"><span data-stu-id="365fd-167">**gx_line_data_line_width**</span></span>        | <span data-ttu-id="365fd-168">Çizilen veri çizgisinin genişliği</span><span class="sxs-lookup"><span data-stu-id="365fd-168">Width of the plotted data line</span></span> |
| <span data-ttu-id="365fd-169">**gx_line_chart_axis_color**</span><span class="sxs-lookup"><span data-stu-id="365fd-169">**gx_line_chart_axis_color**</span></span>       | <span data-ttu-id="365fd-170">Eksen çizgilerini çizmek için kullanılan rengin kaynak KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="365fd-170">Resource ID of the color used to draw the axis lines</span></span> |
| <span data-ttu-id="365fd-171">**gx_line_chart_line_color**</span><span class="sxs-lookup"><span data-stu-id="365fd-171">**gx_line_chart_line_color**</span></span>       | <span data-ttu-id="365fd-172">Grafik veri çizgisini çizmek için kullanılan rengin kaynak KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="365fd-172">Resource ID of the color used to draw the chart data line</span></span> |

## <a name="gx_mouse_cursor_info"></a><span data-ttu-id="365fd-173">GX_MOUSE_CURSOR_INFO</span><span class="sxs-lookup"><span data-stu-id="365fd-173">GX_MOUSE_CURSOR_INFO</span></span> 

### <a name="definition"></a><span data-ttu-id="365fd-174">Tanım</span><span class="sxs-lookup"><span data-stu-id="365fd-174">Definition</span></span>

```c
typedef struct GX_MOUSE_CURSOR_INFO_STRUCT
{
    GX_RESOURCE_ID             gx_mouse_cursor_image_id;
    GX_VALUE                   gx_mouse_cursor_hotspot_x;
    GX_VALUE                   gx_mouse_cursor_hotspot_y;
} GX_MOUSE_CURSOR_INFO;
```

| <span data-ttu-id="365fd-175">Üyeler</span><span class="sxs-lookup"><span data-stu-id="365fd-175">Members</span></span> | <span data-ttu-id="365fd-176">Açıklama</span><span class="sxs-lookup"><span data-stu-id="365fd-176">Description</span></span> |
| ---------------------------------- | ---------------------------------------------------------- |
| <span data-ttu-id="365fd-177">**gx_mouse_cursor_image_id**</span><span class="sxs-lookup"><span data-stu-id="365fd-177">**gx_mouse_cursor_image_id**</span></span>       | <span data-ttu-id="365fd-178">Fare resminin kaynak KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="365fd-178">Resource ID of the mouse image</span></span> |
| <span data-ttu-id="365fd-179">**gx_mouse_cursor_hotspot_x**</span><span class="sxs-lookup"><span data-stu-id="365fd-179">**gx_mouse_cursor_hotspot_x**</span></span>      | <span data-ttu-id="365fd-180">Fare resminin solundaki fare resmi etkin noktası arasındaki fark</span><span class="sxs-lookup"><span data-stu-id="365fd-180">The offset from the left of the mouse image to the mouse image hotspot</span></span> |
| <span data-ttu-id="365fd-181">**gx_mouse_cursor_hotspot_y**</span><span class="sxs-lookup"><span data-stu-id="365fd-181">**gx_mouse_cursor_hotspot_y**</span></span>      | <span data-ttu-id="365fd-182">Fare resminin en üstünden fare resmi etkin noktaya kadar olan fark</span><span class="sxs-lookup"><span data-stu-id="365fd-182">The offset from the top of the mouse image to the mouse image hotspot</span></span> |

## <a name="gx_pen_configuration"></a><span data-ttu-id="365fd-183">GX_PEN_CONFIGURATION</span><span class="sxs-lookup"><span data-stu-id="365fd-183">GX_PEN_CONFIGURATION</span></span> 

### <a name="definition"></a><span data-ttu-id="365fd-184">Tanım</span><span class="sxs-lookup"><span data-stu-id="365fd-184">Definition</span></span>

```c
typedef struct GX_PEN_CONFIGURATION_STRUCT
{
    GX_FIXED_VAL     gx_pen_configuration_min_drag_dist;
    UINT             gx_pen_configuration_max_pen_speed_ticks;
}GX_PEN_CONFIGURATION;
```

| <span data-ttu-id="365fd-185">Üyeler</span><span class="sxs-lookup"><span data-stu-id="365fd-185">Members</span></span> | <span data-ttu-id="365fd-186">Açıklama</span><span class="sxs-lookup"><span data-stu-id="365fd-186">Description</span></span> |
| -------------------------------------------- | ------------------------------------------------ |
| <span data-ttu-id="365fd-187">**gx_pen_configuration_min_drag_dist**</span><span class="sxs-lookup"><span data-stu-id="365fd-187">**gx_pen_configuration_min_drag_dist**</span></span>       | <span data-ttu-id="365fd-188">Bir hareket olayı tetiklemek için Gux süreölçeri başına en az sürükleme uzaklığı.</span><span class="sxs-lookup"><span data-stu-id="365fd-188">The minimum drag distance per GUIX timer tick to trigger an FLICK event.</span></span> <span data-ttu-id="365fd-189">Sabit bir nokta veri türü değeri oluşturmak için GX_FIXED_VAL_MAKE çağırın</span><span class="sxs-lookup"><span data-stu-id="365fd-189">Call GX_FIXED_VAL_MAKE to make a fixed point data type value</span></span> |
| <span data-ttu-id="365fd-190">**gx_pen_configuration_max_pen_speed_ticks**</span><span class="sxs-lookup"><span data-stu-id="365fd-190">**gx_pen_configuration_max_pen_speed_ticks**</span></span> | <span data-ttu-id="365fd-191">Bir hareket olayı tetiklemek için Gux süreölçer işaretleri cinsinden maksimum sürükleme hızı</span><span class="sxs-lookup"><span data-stu-id="365fd-191">The maximum drag speed in GUIX timer ticks to trigger an FLICK event</span></span> | 

## <a name="gx_pixelmap_slider_info"></a><span data-ttu-id="365fd-192">GX_PIXELMAP_SLIDER_INFO</span><span class="sxs-lookup"><span data-stu-id="365fd-192">GX_PIXELMAP_SLIDER_INFO</span></span> 

### <a name="definition"></a><span data-ttu-id="365fd-193">Tanım</span><span class="sxs-lookup"><span data-stu-id="365fd-193">Definition</span></span>

```c
typedef struct GX_PIXELMAP_SLIDER_INFO_STRUCT
{
    GX_RESOURCE_ID gx_pixelmap_slider_info_lower_background_pixelmap;
    GX_RESOURCE_ID gx_pixelmap_slider_info_upper_background_pixelmap;
    GX_RESOURCE_ID gx_pixelmap_slider_info_needle_pixelmap;
} GX_PIXELMAP_SLIDER_INFO;
```

| <span data-ttu-id="365fd-194">Üyeler</span><span class="sxs-lookup"><span data-stu-id="365fd-194">Members</span></span> | <span data-ttu-id="365fd-195">Açıklama</span><span class="sxs-lookup"><span data-stu-id="365fd-195">Description</span></span> |
| ----------------------------------------------------- | ---------------------------------------- |
| <span data-ttu-id="365fd-196">**gx_pixelmap_slider_info_lower_background_pixelmap**</span><span class="sxs-lookup"><span data-stu-id="365fd-196">**gx_pixelmap_slider_info_lower_background_pixelmap**</span></span> | <span data-ttu-id="365fd-197">İğne 'dan önce arka planı doldurmak için pixelmap 'in kaynak KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="365fd-197">Resource ID of the pixelmap for filling the background before the needle.</span></span> <span data-ttu-id="365fd-198">Üst arka plan pixelmap ayarlanmamışsa, arka planı yalnızca iğne 'den önce ve sonra doldurmak için kullanılır</span><span class="sxs-lookup"><span data-stu-id="365fd-198">If upper background pixelmap is not set, it’s used for filling background both before and after the needle</span></span> |
| <span data-ttu-id="365fd-199">**gx_pixelmap_slider_info_upper_background_pixelmap**</span><span class="sxs-lookup"><span data-stu-id="365fd-199">**gx_pixelmap_slider_info_upper_background_pixelmap**</span></span> | <span data-ttu-id="365fd-200">İğne 'tan sonra arka planı doldurmak için pixelmap 'in kaynak KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="365fd-200">Resource ID of the pixelmap for filling background after the needle</span></span> |
| <span data-ttu-id="365fd-201">**gx_pixelmap_slider_info_needle_pixelmap**</span><span class="sxs-lookup"><span data-stu-id="365fd-201">**gx_pixelmap_slider_info_needle_pixelmap**</span></span>           | <span data-ttu-id="365fd-202">İğne pixelmap 'in kaynak KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="365fd-202">Resource ID of the needle pixelmap</span></span> |

## <a name="gx_progress_bar_info"></a><span data-ttu-id="365fd-203">GX_PROGRESS_BAR_INFO</span><span class="sxs-lookup"><span data-stu-id="365fd-203">GX_PROGRESS_BAR_INFO</span></span> 

### <a name="definition"></a><span data-ttu-id="365fd-204">**Tanım**</span><span class="sxs-lookup"><span data-stu-id="365fd-204">**Definition**</span></span>

```c
typedef struct GX_PROGRESS_BAR_INFO_STRUCT
{
    INT gx_progress_bar_info_min_val;
    INT gx_progress_bar_info_max_val;
    INT gx_progress_bar_info_current_val;
    GX_RESOURCE_ID gx_progress_bar_font_id;
    GX_RESOURCE_ID gx_progress_bar_normal_text_color;
    GX_RESOURCE_ID gx_progress_bar_selected_text_color;
    GX_RESOURCE_ID gx_progress_bar_disabled_text_color;
    GX_RESOURCE_ID gx_progress_bar_fill_pixelmap;
} GX_PROGRESS_BAR_INFO;
```

| <span data-ttu-id="365fd-205">Üyeler</span><span class="sxs-lookup"><span data-stu-id="365fd-205">Members</span></span> | <span data-ttu-id="365fd-206">Açıklama</span><span class="sxs-lookup"><span data-stu-id="365fd-206">Description</span></span> |
| -------------------------------------------- | ------------------------------------------------ |
| <span data-ttu-id="365fd-207">**gx_progress_bar_info_min_val**</span><span class="sxs-lookup"><span data-stu-id="365fd-207">**gx_progress_bar_info_min_val**</span></span>             | <span data-ttu-id="365fd-208">Raporlanan en düşük değer</span><span class="sxs-lookup"><span data-stu-id="365fd-208">Minimum reported value</span></span> |
| <span data-ttu-id="365fd-209">**gx_progress_bar_info_max_val**</span><span class="sxs-lookup"><span data-stu-id="365fd-209">**gx_progress_bar_info_max_val**</span></span>             | <span data-ttu-id="365fd-210">Raporlanan en yüksek değer</span><span class="sxs-lookup"><span data-stu-id="365fd-210">Maximum reported value</span></span> |
| <span data-ttu-id="365fd-211">**gx_progress_bar_info_current_val**</span><span class="sxs-lookup"><span data-stu-id="365fd-211">**gx_progress_bar_info_current_val**</span></span>         | <span data-ttu-id="365fd-212">Geçerli değer</span><span class="sxs-lookup"><span data-stu-id="365fd-212">Current value</span></span> |
| <span data-ttu-id="365fd-213">**gx_progress_bar_info_font_id**</span><span class="sxs-lookup"><span data-stu-id="365fd-213">**gx_progress_bar_info_font_id**</span></span>             | <span data-ttu-id="365fd-214">İlerleme çubuğu pencere öğesi içinde isteğe bağlı metin değerini çizmek için kullanılan yazı tipinin kaynak KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="365fd-214">Resource ID of the font, used to draw the optional text value within the progress bar widget</span></span>      |
| <span data-ttu-id="365fd-215">**gx_progress_bar_normal_text_color**</span><span class="sxs-lookup"><span data-stu-id="365fd-215">**gx_progress_bar_normal_text_color**</span></span>        | <span data-ttu-id="365fd-216">İlerleme çubuğu pencere öğesi içinde isteğe bağlı metin çizimini tanımlamak için kullanılan, normal durumdaki metin renginin kaynak KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="365fd-216">Resource ID of the text color in normal state, used to define the optional text drawing within the progress bar widget</span></span> |
| <span data-ttu-id="365fd-217">**gx_progress_bar_selected_text_color**</span><span class="sxs-lookup"><span data-stu-id="365fd-217">**gx_progress_bar_selected_text_color**</span></span>      | <span data-ttu-id="365fd-218">Pencere öğesi odaklanıldığında metin renginin kaynak KIMLIĞI, ilerleme çubuğu pencere öğesi içinde isteğe bağlı metin çizimini tanımlamak için kullanılır</span><span class="sxs-lookup"><span data-stu-id="365fd-218">Resource ID of the text color when the widget gain focus, used to define the optional text drawing within the progress bar widget</span></span> |
| <span data-ttu-id="365fd-219">**gx_progress_bar_disabled_text_color**</span><span class="sxs-lookup"><span data-stu-id="365fd-219">**gx_progress_bar_disabled_text_color**</span></span>      | <span data-ttu-id="365fd-220">GX_STYLE_ENABLED etkin olmadığında metin renginin kaynak KIMLIĞI, ilerleme çubuğu pencere öğesi içinde isteğe bağlı metin çizimini tanımlamak için kullanılır</span><span class="sxs-lookup"><span data-stu-id="365fd-220">Resource ID of the text color when GX_STYLE_ENABLED is not active, used to define the optional text drawing within the progress bar widget</span></span> |
| <span data-ttu-id="365fd-221">**gx_progress_bar_fill_pixelmap**</span><span class="sxs-lookup"><span data-stu-id="365fd-221">**gx_progress_bar_fill_pixelmap**</span></span>            | <span data-ttu-id="365fd-222">Arka plan doldurma için pixelmap 'in kaynak KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="365fd-222">Resource ID of the pixelmap for background filling</span></span>|

## <a name="gx_radial_progress_bar_info"></a><span data-ttu-id="365fd-223">GX_RADIAL_PROGRESS_BAR_INFO</span><span class="sxs-lookup"><span data-stu-id="365fd-223">GX_RADIAL_PROGRESS_BAR_INFO</span></span>

### <a name="definition"></a><span data-ttu-id="365fd-224">Tanım</span><span class="sxs-lookup"><span data-stu-id="365fd-224">Definition</span></span>

```c
typedef struct GX_RADIAL_PROGRESS_BAR_INFO_STRUCT
{
    GX_VALUE       gx_radial_progress_bar_info_xcenter;
    GX_VALUE       gx_radial_progress_bar_info_ycenter;
    GX_VALUE       gx_radial_progress_bar_info_radius;
    GX_VALUE       gx_radial_progress_bar_info_current_val;
    GX_VALUE       gx_radial_progress_bar_info_anchor_val;
    GX_RESOURCE_ID gx_radial_progress_bar_info_font_id;
    GX_RESOURCE_ID gx_radial_progress_bar_info_normal_text_color;
    GX_RESOURCE_ID gx_radial_progress_bar_info_selected_text_color;
    GX_RESOURCE_ID gx_radial_progress_bar_info_disabled_text_color;
    GX_VALUE       gx_radial_progress_bar_info_normal_brush_width;
    GX_VALUE       gx_radial_progress_bar_info_selected_brush_width;
    GX_RESOURCE_ID gx_radial_progress_bar_info_normal_brush_color;
    GX_RESOURCE_ID gx_radial_progress_bar_info_selected_brush_color;
} GX_RADIAL_PROGRESS_BAR_INFO;
```

| <span data-ttu-id="365fd-225">Üyeler</span><span class="sxs-lookup"><span data-stu-id="365fd-225">Members</span></span> | <span data-ttu-id="365fd-226">Açıklama</span><span class="sxs-lookup"><span data-stu-id="365fd-226">Description</span></span> |
| ------------------------------------------------- | -------------------------------------------- |
| <span data-ttu-id="365fd-227">**gx_radial_progress_bar_info_xcenter**</span><span class="sxs-lookup"><span data-stu-id="365fd-227">**gx_radial_progress_bar_info_xcenter**</span></span>           | <span data-ttu-id="365fd-228">X koordinatı içindeki pencere öğesi konumu</span><span class="sxs-lookup"><span data-stu-id="365fd-228">Widget position in x coordinate</span></span> |
| <span data-ttu-id="365fd-229">**gx_radial_progress_bar_info_ycenter**</span><span class="sxs-lookup"><span data-stu-id="365fd-229">**gx_radial_progress_bar_info_ycenter**</span></span>           | <span data-ttu-id="365fd-230">Y koordinatı pencere öğesi konumu</span><span class="sxs-lookup"><span data-stu-id="365fd-230">Widget position in y coordinate</span></span>  |
| <span data-ttu-id="365fd-231">**gx_radial_progress_bar_info_radius**</span><span class="sxs-lookup"><span data-stu-id="365fd-231">**gx_radial_progress_bar_info_radius**</span></span>            | <span data-ttu-id="365fd-232">İlerleme çemberin yarıçapı</span><span class="sxs-lookup"><span data-stu-id="365fd-232">Radius of the progress circle</span></span> |
| <span data-ttu-id="365fd-233">**gx_radial_progress_bar_info_current_val**</span><span class="sxs-lookup"><span data-stu-id="365fd-233">**gx_radial_progress_bar_info_current_val**</span></span>       | <span data-ttu-id="365fd-234">[-360, 360] aralığıyla sınırlı geçerli değer, yer işareti konumu ve üst yayı bitiş noktası arasındaki angular Delta değerini gösterir. Negatif değer, bağlayıcının bağlantı konumundan başlayarak saat yönünde bir yönde çizilmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="365fd-234">Current value, limited to the range [-360, 360], indicates the angular delta between the anchor position and the end point of the upper arc. Negative value causes the arc to be drawn in a clockwise direction starting at the anchor position.</span></span> <span data-ttu-id="365fd-235">Pozitif değer, bağlayıcının bağlantı konumundan başlayarak saat yönünde bir yönde çizilmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="365fd-235">Positive value causes the arc to be drawn in a counter-clockwise direction starting at the anchor position.</span></span> <span data-ttu-id="365fd-236">Uygulama, ilerleme çubuğu pencere öğesine bir angular değeri atamak için belirtilen gerçek sözcüklü değeri ölçeklendirmelidir</span><span class="sxs-lookup"><span data-stu-id="365fd-236">The application must scale the real-word value being indicated to assign an angular value to the progress bar widget</span></span> |
| <span data-ttu-id="365fd-237">**gx_radial_progress_bar_anchor_val**</span><span class="sxs-lookup"><span data-stu-id="365fd-237">**gx_radial_progress_bar_anchor_val**</span></span>             | <span data-ttu-id="365fd-238">Üst ilerleme yayı başlangıç açısı. Değer, doğru ve 90 dereceyle işaret eden 0 derecelik tamsayı derecesi cinsinden tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="365fd-238">Starting angle of the upper progress arc. The value is defined in terms of integer degree with 0 degree pointing to the right and 90 degree indicating straight up position.</span></span> |
| <span data-ttu-id="365fd-239">**gx_radial_progress_bar_font_id**</span><span class="sxs-lookup"><span data-stu-id="365fd-239">**gx_radial_progress_bar_font_id**</span></span>                | <span data-ttu-id="365fd-240">İlerleme çubuğu pencere öğesi içinde isteğe bağlı metin değerini çizmek için kullanılan yazı tipinin kaynak KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="365fd-240">Resource ID of the font used to draw the optional text value within the progress bar widget</span></span> |
| <span data-ttu-id="365fd-241">**gx_radial_progress_bar_normal_text_color**</span><span class="sxs-lookup"><span data-stu-id="365fd-241">**gx_radial_progress_bar_normal_text_color**</span></span>      | <span data-ttu-id="365fd-242">İlerleme çubuğu pencere öğesi içinde isteğe bağlı metin çizimini tanımlamak için kullanılan, normal durumdaki metin renginin kaynak KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="365fd-242">Resource ID of the text color in normal state, used to define the optional text drawing within the progress bar widget</span></span> |
| <span data-ttu-id="365fd-243">**gx_radial_progress_bar_selected_text_color**</span><span class="sxs-lookup"><span data-stu-id="365fd-243">**gx_radial_progress_bar_selected_text_color**</span></span>    |<span data-ttu-id="365fd-244">Pencere öğesi odaklı metin renginin kaynak KIMLIĞI, ilerleme çubuğu pencere öğesi içinde isteğe bağlı metin çizimini tanımlamak için kullanılır</span><span class="sxs-lookup"><span data-stu-id="365fd-244">Resource ID of the text color when widget gain focus, used to define the optional text drawing within the progress bar widget</span></span> |
| <span data-ttu-id="365fd-245">**gx_radial_progress_bar_disabled_text_color**</span><span class="sxs-lookup"><span data-stu-id="365fd-245">**gx_radial_progress_bar_disabled_text_color**</span></span>    | <span data-ttu-id="365fd-246">GX_STYLE_ENABLED etkin olmadığında metin renginin kaynak KIMLIĞI, ilerleme çubuğu pencere öğesi içinde isteğe bağlı metin çizimini tanımlamak için kullanılır</span><span class="sxs-lookup"><span data-stu-id="365fd-246">Resource ID of the text color when GX_STYLE_ENABLED is not active, used to define the optional text drawing within the progress bar widget</span></span> |
| <span data-ttu-id="365fd-247">**gx_radial_progress_bar_normal_brush_width**</span><span class="sxs-lookup"><span data-stu-id="365fd-247">**gx_radial_progress_bar_normal_brush_width**</span></span>     | <span data-ttu-id="365fd-248">Düşük ilerleme çemberin genişliği</span><span class="sxs-lookup"><span data-stu-id="365fd-248">Width of the lower progress circle</span></span> |
| <span data-ttu-id="365fd-249">**gx_radial_progress_bar_selected_brush_width**</span><span class="sxs-lookup"><span data-stu-id="365fd-249">**gx_radial_progress_bar_selected_brush_width**</span></span>   | <span data-ttu-id="365fd-250">Üstteki ilerleme yayı genişliği, üst yay daha dar, ile aynı veya daha büyük bir daireye eşit olabilir</span><span class="sxs-lookup"><span data-stu-id="365fd-250">Width of the upper progress arc, the upper arc may be narrower, the same as, or wider than the lower circle</span></span> |
| <span data-ttu-id="365fd-251">**gx_radial_progress_bar_normal_brush_color**</span><span class="sxs-lookup"><span data-stu-id="365fd-251">**gx_radial_progress_bar_normal_brush_color**</span></span>     | <span data-ttu-id="365fd-252">Düşük ilerleme çemberi dolduracak rengin kaynak KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="365fd-252">Resource ID of the color to fill lower progress circle</span></span> |
| <span data-ttu-id="365fd-253">**gx_radial_progress_bar_selected_brush_color**</span><span class="sxs-lookup"><span data-stu-id="365fd-253">**gx_radial_progress_bar_selected_brush_color**</span></span>   | <span data-ttu-id="365fd-254">Üst ilerleme yaya dolduracak rengin kaynak KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="365fd-254">Resource ID of the color to fill upper progress arc</span></span> |

## <a name="gx_radial_slider_info"></a><span data-ttu-id="365fd-255">GX_RADIAL_SLIDER_INFO</span><span class="sxs-lookup"><span data-stu-id="365fd-255">GX_RADIAL_SLIDER_INFO</span></span> 

### <a name="definition"></a><span data-ttu-id="365fd-256">Tanım</span><span class="sxs-lookup"><span data-stu-id="365fd-256">Definition</span></span>

```c
typedef struct GX_RADIAL_SLIDER_INFO_STRUCT
{
    GX_VALUE       gx_radial_slider_info_xcenter;
    GX_VALUE       gx_radial_slider_info_ycenter;
    USHORT         gx_radial_slider_info_radius;
    USHORT         gx_radial_slider_info_track_width;
    GX_VALUE       gx_radial_slider_info_current_angle;
    GX_VALUE       gx_radial_slider_info_min_angle;
    GX_VALUE       gx_radial_slider_info_max_angle;
    GX_VALUE      *gx_radial_slider_info_angle_list;
    USHORT         gx_radial_slider_info_list_cont;
    GX_RESOURCE_ID gx_radial_slider_info_background_pixelmap;
    GX_RESOURCE_ID gx_radial_slider_info_needle_pixelmap;
} GX_RADIAL_SLIDER_INFO;
```

| <span data-ttu-id="365fd-257">Üyeler</span><span class="sxs-lookup"><span data-stu-id="365fd-257">Members</span></span> | <span data-ttu-id="365fd-258">Açıklama</span><span class="sxs-lookup"><span data-stu-id="365fd-258">Description</span></span> |
| --------------------------------------------- | ------------------------------------------------ |
<span data-ttu-id="365fd-259">**gx_radial_slider_info_xcenter**</span><span class="sxs-lookup"><span data-stu-id="365fd-259">**gx_radial_slider_info_xcenter**</span></span>               | <span data-ttu-id="365fd-260">Kaydırıcı pencere öğesinin sol tarafında bulunan kaydırıcı iğne 'nin ortasına mesafe</span><span class="sxs-lookup"><span data-stu-id="365fd-260">Distance from the left of the slider widget to the center-of-rotation of the slider needle</span></span> |
| <span data-ttu-id="365fd-261">**gx_radial_slider_info_ycenter**</span><span class="sxs-lookup"><span data-stu-id="365fd-261">**gx_radial_slider_info_ycenter**</span></span>             | <span data-ttu-id="365fd-262">Kaydırıcı pencere öğesinin üstünden kaydırıcı iğne 'nin ortasına kadar uzaklık</span><span class="sxs-lookup"><span data-stu-id="365fd-262">Distance from the top of the slider widget to the center-of-rotation of the slider needle</span></span> |
| <span data-ttu-id="365fd-263">**gx_radial_slider_info_radius**</span><span class="sxs-lookup"><span data-stu-id="365fd-263">**gx_radial_slider_info_radius**</span></span>              | <span data-ttu-id="365fd-264">Radyal kaydırıcı çemberin yarıçapı</span><span class="sxs-lookup"><span data-stu-id="365fd-264">Radius of the radial slider circle</span></span> |
| <span data-ttu-id="365fd-265">**gx_radial_slider_info_track_width**</span><span class="sxs-lookup"><span data-stu-id="365fd-265">**gx_radial_slider_info_track_width**</span></span>         | <span data-ttu-id="365fd-266">Radyal kaydırıcı izlemenin genişliği</span><span class="sxs-lookup"><span data-stu-id="365fd-266">Width of radial slider track</span></span> |
| <span data-ttu-id="365fd-267">**gx_radial_slider_info_current_angle**</span><span class="sxs-lookup"><span data-stu-id="365fd-267">**gx_radial_slider_info_current_angle**</span></span>       | <span data-ttu-id="365fd-268">Geçerli kaydırıcı açısı</span><span class="sxs-lookup"><span data-stu-id="365fd-268">Current slider angle</span></span> |
| <span data-ttu-id="365fd-269">**gx_radial_slider_info_min_angle**</span><span class="sxs-lookup"><span data-stu-id="365fd-269">**gx_radial_slider_info_min_angle**</span></span>           | <span data-ttu-id="365fd-270">Minimum kaydırıcı açısı</span><span class="sxs-lookup"><span data-stu-id="365fd-270">Minimum slider angle</span></span> |
| <span data-ttu-id="365fd-271">**gx_radial_slider_info_max_angle**</span><span class="sxs-lookup"><span data-stu-id="365fd-271">**gx_radial_slider_info_max_angle**</span></span>           | <span data-ttu-id="365fd-272">Maksimum kaydırıcı açısı</span><span class="sxs-lookup"><span data-stu-id="365fd-272">Maximum slider angle</span></span> |
| <span data-ttu-id="365fd-273">**gx_radial_slider_info_angle_list**</span><span class="sxs-lookup"><span data-stu-id="365fd-273">**gx_radial_slider_info_angle_list**</span></span>          | <span data-ttu-id="365fd-274">Açı değeri listesi, küme açılarını tanımlar, ayarlandıysa, kaydırıcı açısı yalnızca tanımlı çapa açılarının biri olabilir</span><span class="sxs-lookup"><span data-stu-id="365fd-274">Angle value list, defines anchor angles, if set, slider angle can only be one of the defined anchor angles</span></span> |
| <span data-ttu-id="365fd-275">**gx_radial_slider_info_list_count**</span><span class="sxs-lookup"><span data-stu-id="365fd-275">**gx_radial_slider_info_list_count**</span></span>          | <span data-ttu-id="365fd-276">Çapa açısı sayısı</span><span class="sxs-lookup"><span data-stu-id="365fd-276">Number of anchor angles</span></span> |
| <span data-ttu-id="365fd-277">**gx_radial_slider_info_background_pixelmap**</span><span class="sxs-lookup"><span data-stu-id="365fd-277">**gx_radial_slider_info_background_pixelmap**</span></span> | <span data-ttu-id="365fd-278">Arka plan pixelmap kaynak KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="365fd-278">Resource ID of background pixelmap</span></span> |
| <span data-ttu-id="365fd-279">**gx_radial_slider_info_needle_pixelmap**</span><span class="sxs-lookup"><span data-stu-id="365fd-279">**gx_radial_slider_info_needle_pixelmap**</span></span>     | <span data-ttu-id="365fd-280">İğne pixelmap kaynak KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="365fd-280">Resource ID of needle pixelmap</span></span> |

## <a name="gx_rectangle"></a><span data-ttu-id="365fd-281">GX_RECTANGLE</span><span class="sxs-lookup"><span data-stu-id="365fd-281">GX_RECTANGLE</span></span>

### <a name="definition"></a><span data-ttu-id="365fd-282">Tanım</span><span class="sxs-lookup"><span data-stu-id="365fd-282">Definition</span></span>

```c
typedef struct GX_RECTANGLE_STRUCT
{
    GX_VALUE gx_rectangle_left;
    GX_VALUE gx_rectangle_top;
    GX_VALUE gx_rectangle_right;
    GX_VALUE gx_rectangle_bottom;
} GX_RECTANGLE;
```

| <span data-ttu-id="365fd-283">Üyeler</span><span class="sxs-lookup"><span data-stu-id="365fd-283">Members</span></span> | <span data-ttu-id="365fd-284">Açıklama</span><span class="sxs-lookup"><span data-stu-id="365fd-284">Description</span></span> |
| -------------------------------- | ------------------------|
| <span data-ttu-id="365fd-285">**gx_rectangle_left**</span><span class="sxs-lookup"><span data-stu-id="365fd-285">**gx_rectangle_left**</span></span>            | <span data-ttu-id="365fd-286">Dikdörtgenin sol tarafında</span><span class="sxs-lookup"><span data-stu-id="365fd-286">Left of the rectangle</span></span>   |  
| <span data-ttu-id="365fd-287">**gx_rectangle_top**</span><span class="sxs-lookup"><span data-stu-id="365fd-287">**gx_rectangle_top**</span></span>             | <span data-ttu-id="365fd-288">Dikdörtgenin üstü</span><span class="sxs-lookup"><span data-stu-id="365fd-288">Top of the rectangle</span></span>    | 
| <span data-ttu-id="365fd-289">**gx_rectangle_right**</span><span class="sxs-lookup"><span data-stu-id="365fd-289">**gx_rectangle_right**</span></span>           | <span data-ttu-id="365fd-290">Dikdörtgenin sağ</span><span class="sxs-lookup"><span data-stu-id="365fd-290">Right of the rectangle</span></span>  |
| <span data-ttu-id="365fd-291">**gx_rectangle_bottom**</span><span class="sxs-lookup"><span data-stu-id="365fd-291">**gx_rectangle_bottom**</span></span>          | <span data-ttu-id="365fd-292">Dikdörtgenin altı</span><span class="sxs-lookup"><span data-stu-id="365fd-292">Bottom of the rectangle</span></span> |

## <a name="gx_rich_text_fonts"></a><span data-ttu-id="365fd-293">GX_RICH_TEXT_FONTS</span><span class="sxs-lookup"><span data-stu-id="365fd-293">GX_RICH_TEXT_FONTS</span></span> 

### <a name="definition"></a><span data-ttu-id="365fd-294">Tanım</span><span class="sxs-lookup"><span data-stu-id="365fd-294">Definition</span></span>

```c
typedef struct GX_RICH_TEXT_FONTS_STRUCT
{
    GX_RESOURCE_ID             gx_rich_text_fonts_normal_id;
    GX_RESOURCE_ID             gx_rich_text_fonts_bold_id;
    GX_RESOURCE_ID             gx_rich_text_fonts_italic_id;
    GX_RESOURCE_ID             gx_rich_text_fonts_bold_italic_id;
} GX_RICH_TEXT_FONTS;
```

| <span data-ttu-id="365fd-295">Üyeler</span><span class="sxs-lookup"><span data-stu-id="365fd-295">Members</span></span> | <span data-ttu-id="365fd-296">Açıklama</span><span class="sxs-lookup"><span data-stu-id="365fd-296">Description</span></span> |
| ---------------------------------- | ---------------------------------------------------------- |
| <span data-ttu-id="365fd-297">**gx_rich_text_fonts_normal_id**</span><span class="sxs-lookup"><span data-stu-id="365fd-297">**gx_rich_text_fonts_normal_id**</span></span>   | <span data-ttu-id="365fd-298">Normal metin yazı tipinin kaynak KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="365fd-298">Resource ID of normal text font</span></span> |
| <span data-ttu-id="365fd-299">**gx_rich_text_fonts_bold_id**</span><span class="sxs-lookup"><span data-stu-id="365fd-299">**gx_rich_text_fonts_bold_id**</span></span>     | <span data-ttu-id="365fd-300">Kalın metin yazı tipinin kaynak KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="365fd-300">Resource ID of bold text font</span></span> |
| <span data-ttu-id="365fd-301">**gx_rich_text_fonts_italic_id**</span><span class="sxs-lookup"><span data-stu-id="365fd-301">**gx_rich_text_fonts_italic_id**</span></span>   | <span data-ttu-id="365fd-302">İtalik metin yazı tipinin kaynak KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="365fd-302">Resource ID of italic text font</span></span> |
| <span data-ttu-id="365fd-303">**gx_rich_text_fonts_bold_italic_id**</span><span class="sxs-lookup"><span data-stu-id="365fd-303">**gx_rich_text_fonts_bold_italic_id**</span></span> | <span data-ttu-id="365fd-304">Kalın italik metin yazı tipinin kaynak KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="365fd-304">Resource ID of bold italic text font</span></span> |

## <a name="gx_scroll_info"></a><span data-ttu-id="365fd-305">GX_SCROLL_INFO</span><span class="sxs-lookup"><span data-stu-id="365fd-305">GX_SCROLL_INFO</span></span> 
### <a name="definition"></a><span data-ttu-id="365fd-306">**Tanım**</span><span class="sxs-lookup"><span data-stu-id="365fd-306">**Definition**</span></span>

```c
typedef struct GX_SCROLL_INFO_STRUCT
{
    INT      gx_scroll_value;
    INT      gx_scroll_minimum;
    INT      gx_scroll_maximum;
    GX_VALUE gx_scroll_visible;
    GX_VALUE gx_scroll_increment;
} GX_SCROLL_INFO;
```

| <span data-ttu-id="365fd-307">Üyeler</span><span class="sxs-lookup"><span data-stu-id="365fd-307">Members</span></span> | <span data-ttu-id="365fd-308">Açıklama</span><span class="sxs-lookup"><span data-stu-id="365fd-308">Description</span></span> |
| ----------------------- | ----------------------------- |
| <span data-ttu-id="365fd-309">**gx_scroll_value**</span><span class="sxs-lookup"><span data-stu-id="365fd-309">**gx_scroll_value**</span></span>     | <span data-ttu-id="365fd-310">Geçerli kaydırma konumu</span><span class="sxs-lookup"><span data-stu-id="365fd-310">Current scroll position</span></span>       |
| <span data-ttu-id="365fd-311">**gx_scroll_minimum**</span><span class="sxs-lookup"><span data-stu-id="365fd-311">**gx_scroll_minimum**</span></span>   | <span data-ttu-id="365fd-312">Raporlanan en düşük konum</span><span class="sxs-lookup"><span data-stu-id="365fd-312">Minimum reported position</span></span>     |
| <span data-ttu-id="365fd-313">**gx_scroll_maximum**</span><span class="sxs-lookup"><span data-stu-id="365fd-313">**gx_scroll_maximum**</span></span>   | <span data-ttu-id="365fd-314">Raporlanan en yüksek konum</span><span class="sxs-lookup"><span data-stu-id="365fd-314">Maximum reported position</span></span>     |
| <span data-ttu-id="365fd-315">**gx_scroll_visible**</span><span class="sxs-lookup"><span data-stu-id="365fd-315">**gx_scroll_visible**</span></span>   | <span data-ttu-id="365fd-316">Üst pencere görünür aralığı</span><span class="sxs-lookup"><span data-stu-id="365fd-316">Parent window visible range</span></span>   |
| <span data-ttu-id="365fd-317">**gx_scroll_increment**</span><span class="sxs-lookup"><span data-stu-id="365fd-317">**gx_scroll_increment**</span></span> | <span data-ttu-id="365fd-318">Kaydırma çubuğu en küçük delta değeri</span><span class="sxs-lookup"><span data-stu-id="365fd-318">Scrollbar minimum delta value</span></span> |

## <a name="gx_scrollbar_appearance"></a><span data-ttu-id="365fd-319">GX_SCROLLBAR_APPEARANCE</span><span class="sxs-lookup"><span data-stu-id="365fd-319">GX_SCROLLBAR_APPEARANCE</span></span> 

### <a name="definition"></a><span data-ttu-id="365fd-320">Tanım</span><span class="sxs-lookup"><span data-stu-id="365fd-320">Definition</span></span>

```c
typedef struct GX_SCROLLBAR_APPEARANCE_STRUCT
{
    GX_VALUE       gx_scroll_width;
    GX_VALUE       gx_scroll_thumb_width;
    GX_VALUE       gx_scroll_thumb_travel_min;
    GX_VALUE       gx_scroll_thumb_travel_max;
    GX_UBYTE       gx_scroll_thumb_border_style;
    GX_RESOURCE_ID gx_scroll_fill_pixelmap;
    GX_RESOURCE_ID gx_scroll_thumb_pixelmap;
    GX_RESOURCE_ID gx_scroll_up_pixelmap;
    GX_RESOURCE_ID gx_scroll_down_pixelmap;
    GX_RESOURCE_ID gx_scroll_thumb_color;
    GX_RESOURCE_ID gx_scroll_thumb_border_color;
    GX_RESOURCE_ID gx_scroll_button_color;
} GX_SCROLLBAR_APPEARANCE;
```

| <span data-ttu-id="365fd-321">Üyeler</span><span class="sxs-lookup"><span data-stu-id="365fd-321">Members</span></span> | <span data-ttu-id="365fd-322">Açıklama</span><span class="sxs-lookup"><span data-stu-id="365fd-322">Description</span></span> |
| ---------------------------------------- | ----------------------------------------------------- |
| <span data-ttu-id="365fd-323">**gx_scroll_width**</span><span class="sxs-lookup"><span data-stu-id="365fd-323">**gx_scroll_width**</span></span>                      | <span data-ttu-id="365fd-324">ScrollBar pencere öğesinin piksel cinsinden genişliği</span><span class="sxs-lookup"><span data-stu-id="365fd-324">Width of the scrollbar widget, in pixels</span></span> |
| <span data-ttu-id="365fd-325">**gx_scroll_thumb_width**</span><span class="sxs-lookup"><span data-stu-id="365fd-325">**gx_scroll_thumb_width**</span></span>                | <span data-ttu-id="365fd-326">Kaydırma çubuğu üzerindeki slaytları piksel cinsinden gösteren Thumb düğmesinin genişliği.</span><span class="sxs-lookup"><span data-stu-id="365fd-326">Width of the thumb button which slides on the scrollbar, in pixels.</span></span> <span data-ttu-id="365fd-327">Bu değer genellikle toplam kaydırma çubuğu genişliğinden az sayıda piksel daha küçüktür</span><span class="sxs-lookup"><span data-stu-id="365fd-327">This value is usually some number of pixels less than the total scrollbar width</span></span> |
| <span data-ttu-id="365fd-328">**gx_scroll_thumb_travel_min**</span><span class="sxs-lookup"><span data-stu-id="365fd-328">**gx_scroll_thumb_travel_min**</span></span>           | <span data-ttu-id="365fd-329">Kaydırma çubuğunun sonundan en küçük parmak izi düğmesi seyahat noktası arasındaki fark.</span><span class="sxs-lookup"><span data-stu-id="365fd-329">Offset from the end of scrollbar to minimum thumb button travel point.</span></span> <span data-ttu-id="365fd-330">Bu sınır, parmak izinin kaydırma çubuğunun çok sonuna kadar hareket etmelerini engellemek için kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="365fd-330">This limit can be used to prevent the thumb button from traveling to the very end of the scrollbar</span></span> |
| <span data-ttu-id="365fd-331">**gx_scroll_thumb_travel_max**</span><span class="sxs-lookup"><span data-stu-id="365fd-331">**gx_scroll_thumb_travel_max**</span></span>           | <span data-ttu-id="365fd-332">Kaydırma çubuğunun sonundan en fazla kaydırma düğmesi seyahat noktası arasındaki fark.</span><span class="sxs-lookup"><span data-stu-id="365fd-332">Offset from the end of scrollbar to maximum thumb button travel point.</span></span> <span data-ttu-id="365fd-333">Bu sınır, parmak izinin kaydırma çubuğunun çok sonuna kadar hareket etmelerini engellemek için kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="365fd-333">This limit can be used to prevent the thumb button from traveling to the very end of the scrollbar</span></span> |
| <span data-ttu-id="365fd-334">**gx_scroll_thumb_border_style**</span><span class="sxs-lookup"><span data-stu-id="365fd-334">**gx_scroll_thumb_border_style**</span></span>         | <span data-ttu-id="365fd-335">Thumb düğmesinin kenarlık stilleri</span><span class="sxs-lookup"><span data-stu-id="365fd-335">Border styles of thumb button</span></span> |
| <span data-ttu-id="365fd-336">**gx_scroll_fill_pixelmap**</span><span class="sxs-lookup"><span data-stu-id="365fd-336">**gx_scroll_fill_pixelmap**</span></span>              | <span data-ttu-id="365fd-337">İsteğe bağlı pixelmap KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="365fd-337">Optional pixelmap ID.</span></span> <span data-ttu-id="365fd-338">Bu pixelmap KIMLIĞI sıfır değilse, ScrollBar ScrollBar arka planını çizmek için bu pixelmap 'i kullanır</span><span class="sxs-lookup"><span data-stu-id="365fd-338">If this pixelmap ID is not zero, the scrollbar uses this pixelmap to draw the scrollbar background</span></span> |
| <span data-ttu-id="365fd-339">**gx_scroll_thumb_pixelmap**</span><span class="sxs-lookup"><span data-stu-id="365fd-339">**gx_scroll_thumb_pixelmap**</span></span>             | <span data-ttu-id="365fd-340">İsteğe bağlı pixelmap KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="365fd-340">Optional pixelmap ID.</span></span> <span data-ttu-id="365fd-341">Bu pixelmap KIMLIĞI sıfır değilse, kaydırma çubuğu parmak izi düğmesi kendisini çizmek için bu pixelmap 'i kullanır</span><span class="sxs-lookup"><span data-stu-id="365fd-341">If this pixelmap ID is not zero, the scrollbar thumb button uses this pixelmap to draw itself</span></span> |
| <span data-ttu-id="365fd-342">**gx_scroll_up_pixelmap**</span><span class="sxs-lookup"><span data-stu-id="365fd-342">**gx_scroll_up_pixelmap**</span></span>                | <span data-ttu-id="365fd-343">İsteğe bağlı pixelmap KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="365fd-343">Optional pixelmap ID.</span></span> <span data-ttu-id="365fd-344">Bu pixelmap KIMLIĞI sıfır değilse, kaydırma çubuğu bu pixelmap KIMLIĞINI kullanarak kaydırma çubuğunu sola/yukarı ucu düğme çiz</span><span class="sxs-lookup"><span data-stu-id="365fd-344">If this pixelmap ID is not zero, the scrollbar uses this pixelmap ID to draw the scrollbar left/up end button</span></span> |
| <span data-ttu-id="365fd-345">**gx_scroll_down_pixelmap**</span><span class="sxs-lookup"><span data-stu-id="365fd-345">**gx_scroll_down_pixelmap**</span></span>              | <span data-ttu-id="365fd-346">İsteğe bağlı pixelmap KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="365fd-346">Optional pixelmap ID.</span></span> <span data-ttu-id="365fd-347">Bu pixelmap KIMLIĞI sıfır değilse, kaydırma çubuğu bu pixelmap KIMLIĞINI kullanarak kaydırma çubuğunu sağ/aşağı uç düğmesini çizin</span><span class="sxs-lookup"><span data-stu-id="365fd-347">If this pixelmap ID is not zero, the scrollbar uses this pixelmap ID to draw the scrollbar right/down end button</span></span> |
| <span data-ttu-id="365fd-348">**gx_scroll_thumb_color**</span><span class="sxs-lookup"><span data-stu-id="365fd-348">**gx_scroll_thumb_color**</span></span>                | <span data-ttu-id="365fd-349">Thumb düğmesini doldurmanız için kullanılan rengin kaynak KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="365fd-349">Resource ID of color used to fill thumb button</span></span> |
| <span data-ttu-id="365fd-350">**gx_scroll_thumb_border_color**</span><span class="sxs-lookup"><span data-stu-id="365fd-350">**gx_scroll_thumb_border_color**</span></span>         | <span data-ttu-id="365fd-351">Thumb düğmesinin kenarlığını çizmek için kullanılan rengin kaynak KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="365fd-351">Resource ID of color used to draw the border of thumb button</span></span> | 
| <span data-ttu-id="365fd-352">**gx_scroll_button_color**</span><span class="sxs-lookup"><span data-stu-id="365fd-352">**gx_scroll_button_color**</span></span>               | <span data-ttu-id="365fd-353">Kaydırma çubuğu bitiş düğmelerini dolduracak şekilde kullanılan rengin kaynak KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="365fd-353">Resource ID of color used to fill scrollbar end buttons</span></span> |

## <a name="gx_slider_info"></a><span data-ttu-id="365fd-354">GX_SLIDER_INFO</span><span class="sxs-lookup"><span data-stu-id="365fd-354">GX_SLIDER_INFO</span></span>

### <a name="definition"></a><span data-ttu-id="365fd-355">Tanım</span><span class="sxs-lookup"><span data-stu-id="365fd-355">Definition</span></span>

```c
typedef struct GX_SLIDER_INFO_STRUCT
{
    INT      gx_slider_info_min_val;
    INT      gx_slider_info_max_val;
    INT      gx_slider_info_current_val;
    INT      gx_slider_info_increment;
    GX_VALUE gx_slider_info_min_travel;
    GX_VALUE gx_slider_info_max_travel;
    GX_VALUE gx_slider_info_needle_width;
    GX_VALUE gx_slider_info_needle_height;
    GX_VALUE gx_slider_info_needle_inset;
    GX_VALUE gx_slider_info_needle_hotspot_offset;
} GX_SLIDER_INFO;
```

| <span data-ttu-id="365fd-356">Üyeler</span><span class="sxs-lookup"><span data-stu-id="365fd-356">Members</span></span> | <span data-ttu-id="365fd-357">Açıklama</span><span class="sxs-lookup"><span data-stu-id="365fd-357">Description</span></span> |
| --------------------------------------- | ------------------------------------------------------ |
| <span data-ttu-id="365fd-358">**gx_slider_info_min_val**</span><span class="sxs-lookup"><span data-stu-id="365fd-358">**gx_slider_info_min_val**</span></span>              | <span data-ttu-id="365fd-359">Raporlanan en düşük değer</span><span class="sxs-lookup"><span data-stu-id="365fd-359">Minimum reported value</span></span> |
| <span data-ttu-id="365fd-360">**gx_slider_info_max_val**</span><span class="sxs-lookup"><span data-stu-id="365fd-360">**gx_slider_info_max_val**</span></span>              | <span data-ttu-id="365fd-361">Raporlanan en yüksek değer</span><span class="sxs-lookup"><span data-stu-id="365fd-361">Maximum reported value</span></span> |
| <span data-ttu-id="365fd-362">**gx_slider_info_current_value**</span><span class="sxs-lookup"><span data-stu-id="365fd-362">**gx_slider_info_current_value**</span></span>        | <span data-ttu-id="365fd-363">Geçerli değer</span><span class="sxs-lookup"><span data-stu-id="365fd-363">Current value</span></span> |
| <span data-ttu-id="365fd-364">**gx_slider_info_min_travel**</span><span class="sxs-lookup"><span data-stu-id="365fd-364">**gx_slider_info_min_travel**</span></span>           | <span data-ttu-id="365fd-365">İğne seyahat sınırı</span><span class="sxs-lookup"><span data-stu-id="365fd-365">Needle travel limit</span></span> |
| <span data-ttu-id="365fd-366">**gx_slider_info_max_travel**</span><span class="sxs-lookup"><span data-stu-id="365fd-366">**gx_slider_info_max_travel**</span></span>           | <span data-ttu-id="365fd-367">İğne seyahat sınırı</span><span class="sxs-lookup"><span data-stu-id="365fd-367">Needle travel limit</span></span> |
| <span data-ttu-id="365fd-368">**gx_slider_info_needle_width**</span><span class="sxs-lookup"><span data-stu-id="365fd-368">**gx_slider_info_needle_width**</span></span>         | <span data-ttu-id="365fd-369">Piksel cinsinden iğne genişliği</span><span class="sxs-lookup"><span data-stu-id="365fd-369">Needle width in pixel</span></span> |
| <span data-ttu-id="365fd-370">**gx_slider_info_needle_height**</span><span class="sxs-lookup"><span data-stu-id="365fd-370">**gx_slider_info_needle_height**</span></span>        | <span data-ttu-id="365fd-371">Piksel cinsinden iğne yüksekliği</span><span class="sxs-lookup"><span data-stu-id="365fd-371">Needle height in pixel</span></span> |
|<span data-ttu-id="365fd-372">**gx_slider_info_needle_inset**</span><span class="sxs-lookup"><span data-stu-id="365fd-372">**gx_slider_info_needle_inset**</span></span>          | <span data-ttu-id="365fd-373">İğne çiz konumu.</span><span class="sxs-lookup"><span data-stu-id="365fd-373">Needle draw position.</span></span> <span data-ttu-id="365fd-374">GX_STYLE_SLIDER_VERTICAL ayarlandıysa, iğne çiz başlangıç konumundan sola doğru kaydırıcıyı belirtmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="365fd-374">If GX_STYLE_SLIDER_VERTICAL is set, used to specify the offset from the needle draw start position to the slider left.</span></span> <span data-ttu-id="365fd-375">Else, iğne çizici başlangıç konumundan kaydırıcıyı üste kadar olan sapmayı belirtmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="365fd-375">Else, used to specify the offset from the needle draw start position to the slider top.</span></span> |
| <span data-ttu-id="365fd-376">**gx_slider_info_needle_hotspot_offset**</span><span class="sxs-lookup"><span data-stu-id="365fd-376">**gx_slider_info_needle_hotspot_offset**</span></span> | <span data-ttu-id="365fd-377">İğne hotpot_offset, iğne çizici başlangıç konumundan kaydırıcı etkin noktaya kadar olan sapmayı belirtmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="365fd-377">Needle hotpot_offset, used to specify the offset from the needle draw start position to the slider hotspot.</span></span> |

## <a name="gx_sprite_frame"></a><span data-ttu-id="365fd-378">GX_SPRITE_FRAME</span><span class="sxs-lookup"><span data-stu-id="365fd-378">GX_SPRITE_FRAME</span></span>

### <a name="definition"></a><span data-ttu-id="365fd-379">Tanım</span><span class="sxs-lookup"><span data-stu-id="365fd-379">Definition</span></span>

```c
typedef struct GX_SPRITE_FRAME_STRUCT
{
    GX_RESOURCE_ID gx_sprite_frame_pixelmap;
    GX_VALUE gx_sprite_frame_x_offset;
    GX_VALUE gx_sprite_frame_y_offset;
    UINT gx_sprite_frame_delay;
    UINT gx_sprite_frame_background_operation;
    UCHAR gx_sprite_frame_alpha;
} GX_SPRITE_FRAME;
```

| <span data-ttu-id="365fd-380">Üyeler</span><span class="sxs-lookup"><span data-stu-id="365fd-380">Members</span></span> | <span data-ttu-id="365fd-381">Açıklama</span><span class="sxs-lookup"><span data-stu-id="365fd-381">Description</span></span> |
| ---------------------------------------- | ----------------------------------------------------- |
| <span data-ttu-id="365fd-382">**gx_sprite_frame_pixelmap**</span><span class="sxs-lookup"><span data-stu-id="365fd-382">**gx_sprite_frame_pixelmap**</span></span>             | <span data-ttu-id="365fd-383">Bu çerçeve için görüntülenecek pixelmap 'in kaynak KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="365fd-383">Resource ID of the pixelmap to be displayed for this frame.</span></span> <span data-ttu-id="365fd-384">KIMLIK 0 olabilir.</span><span class="sxs-lookup"><span data-stu-id="365fd-384">The ID can be 0.</span></span> |
| <span data-ttu-id="365fd-385">**gx_sprite_frame_x_offset**</span><span class="sxs-lookup"><span data-stu-id="365fd-385">**gx_sprite_frame_x_offset**</span></span>             | <span data-ttu-id="365fd-386">Pixelmap 'i göstermek için sprite pencere öğesinin sol tarafındaki boşluğu</span><span class="sxs-lookup"><span data-stu-id="365fd-386">Offset from the sprite widget left to display the pixelmap</span></span> |
| <span data-ttu-id="365fd-387">**gx_sprite_frame_y_offset**</span><span class="sxs-lookup"><span data-stu-id="365fd-387">**gx_sprite_frame_y_offset**</span></span>             | <span data-ttu-id="365fd-388">Pixelmap 'i göstermek için en üstteki Sprite pencere öğesi</span><span class="sxs-lookup"><span data-stu-id="365fd-388">Offset from the sprite widget top to display the pixelmap</span></span> |
| <span data-ttu-id="365fd-389">**gx_sprite_frame_delay**</span><span class="sxs-lookup"><span data-stu-id="365fd-389">**gx_sprite_frame_delay**</span></span>                | <span data-ttu-id="365fd-390">Sonraki Sprite çerçevesine ilerletmeden önce bu kareyi görüntülendikten sonra, SX Zamanlayıcı işaretleri içinde gecikme değeri.</span><span class="sxs-lookup"><span data-stu-id="365fd-390">Delay value, in GUIX timer ticks, after displaying this frame before advancing to the next sprite frame</span></span> |
| <span data-ttu-id="365fd-391">**gx_sprite_frame_background_operation**</span><span class="sxs-lookup"><span data-stu-id="365fd-391">**gx_sprite_frame_background_operation**</span></span> | <span data-ttu-id="365fd-392">Arka planın nasıl silineceğini tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="365fd-392">Define how the background should be erased.</span></span> <span data-ttu-id="365fd-393">Bu alan için olası değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="365fd-393">Possible values for this field are:</span></span><br /><span data-ttu-id="365fd-394">GX_SPRITE_BACKGROUND_NO_ACTION: çerçeveler arasında Fill yok</span><span class="sxs-lookup"><span data-stu-id="365fd-394">GX_SPRITE_BACKGROUND_NO_ACTION: No fill between frames</span></span><br /><span data-ttu-id="365fd-395">GX_SPRITE_BACKGROUND_SOLID_FILL: SPRITE arka planını yeniden Çiz</span><span class="sxs-lookup"><span data-stu-id="365fd-395">GX_SPRITE_BACKGROUND_SOLID_FILL: Redraw sprite background</span></span><br /><span data-ttu-id="365fd-396">GX_SPRITE_BACKGROUND_RESTORE: önceki pixelmap 'i geri yükle</span><span class="sxs-lookup"><span data-stu-id="365fd-396">GX_SPRITE_BACKGROUND_RESTORE: Restore previous pixelmap</span></span> |
| <span data-ttu-id="365fd-397">**gx_sprite_frame_alpha**</span><span class="sxs-lookup"><span data-stu-id="365fd-397">**gx_sprite_frame_alpha**</span></span>                | <span data-ttu-id="365fd-398">Görünen pixelmap 'e eklenecek alfa değeri.</span><span class="sxs-lookup"><span data-stu-id="365fd-398">Alpha value to be added to the displayed pixelmap.</span></span> <span data-ttu-id="365fd-399">255 değeri, ek bir alfa değeri eklenmesi gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="365fd-399">The value 255 specifies that no extra alpha value should be imposed.</span></span> <span data-ttu-id="365fd-400">Pixelmap bir alfa kanalı içeriyorsa, bu Alfa kanalı çerçeve Alpha değerine eklenir.</span><span class="sxs-lookup"><span data-stu-id="365fd-400">If the pixelmap includes an alpha channel, this alpha channel will be added to the frame alpha value.</span></span> |
