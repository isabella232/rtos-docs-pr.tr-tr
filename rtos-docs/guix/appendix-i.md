---
title: Ek I-Gux bilgi yapıları
description: GUX bilgi yapıları hakkında bilgi edinin.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 03a10aeb65017befaf5e7b440046dbff9f9252ef
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104827209"
---
# <a name="appendix-i---guix-information-structures"></a><span data-ttu-id="7c4bf-103">Ek I-Gux bilgi yapıları</span><span class="sxs-lookup"><span data-stu-id="7c4bf-103">Appendix I - GUIX Information Structures</span></span> 

## <a name="gx_bidi_text_info"></a><span data-ttu-id="7c4bf-104">GX_BIDI_TEXT_INFO</span><span class="sxs-lookup"><span data-stu-id="7c4bf-104">GX_BIDI_TEXT_INFO</span></span> 

### <a name="definition"></a><span data-ttu-id="7c4bf-105">Tanım</span><span class="sxs-lookup"><span data-stu-id="7c4bf-105">Definition</span></span>

```c
typedef struct GX_BIDI_TEXT_INFO_STRUCT
{
    GX_STRING gx_bidi_text_info_text;
    GX_FONT  *gx_bidi_text_info_font;
    GX_VALUE  gx_bidi_text_info_display_width;
} GX_BIDI_TEXT_INFO;
```

### <a name="members"></a><span data-ttu-id="7c4bf-106">Üyeler</span><span class="sxs-lookup"><span data-stu-id="7c4bf-106">Members</span></span>

|                                    |                                                            |
| ---------------------------------- | ---------------------------------------------------------- |
| <span data-ttu-id="7c4bf-107">**gx_bidi_text_info_text**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-107">**gx_bidi_text_info_text**</span></span>               | <span data-ttu-id="7c4bf-108">Yeniden sıralama için metin</span><span class="sxs-lookup"><span data-stu-id="7c4bf-108">Text for reordering</span></span> |
| <span data-ttu-id="7c4bf-109">**gx_bidi_text_info_font**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-109">**gx_bidi_text_info_font**</span></span>               | <span data-ttu-id="7c4bf-110">Metni göstermek için kullanılan yazı tipi, satır sonu gerekmiyorsa GX_NULL olarak ayarlayın</span><span class="sxs-lookup"><span data-stu-id="7c4bf-110">Font used to display text, set it to GX_NULL if line breaking is not needed</span></span> |
| <span data-ttu-id="7c4bf-111">**gx_bidi_text_info_display_width**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-111">**gx_bidi_text_info_display_width**</span></span>      | <span data-ttu-id="7c4bf-112">Görüntüleme için kullanılabilir genişlik, satır sonu gerekmiyorsa-1 olarak ayarlayın</span><span class="sxs-lookup"><span data-stu-id="7c4bf-112">Available width for displaying, set it to -1 if line breaking is not needed</span></span> |

## <a name="gx_bidi_resolved_text_info"></a><span data-ttu-id="7c4bf-113">GX_BIDI_RESOLVED_TEXT_INFO</span><span class="sxs-lookup"><span data-stu-id="7c4bf-113">GX_BIDI_RESOLVED_TEXT_INFO</span></span> 

### <a name="definition"></a><span data-ttu-id="7c4bf-114">Tanım</span><span class="sxs-lookup"><span data-stu-id="7c4bf-114">Definition</span></span>

```c
typedef struct GX_BIDI_RESOLVED_TEXT_INFO_STRUCT
{
    GX_STRING                                *gx_bidi_resolved_text_info_text;
    UINT                                      gx_bidi_resolved_text_info_total_lines;
    struct GX_BIDI_RESOLVED_TEXT_INFO_STRUCT *gx_bidi_resolved_text_info_next;
} GX_BIDI_RESOLVED_TEXT_INFO;
```

### <a name="members"></a><span data-ttu-id="7c4bf-115">Üyeler</span><span class="sxs-lookup"><span data-stu-id="7c4bf-115">Members</span></span>

|                                    |                                                            |
| ---------------------------------- | ---------------------------------------------------------- |
| <span data-ttu-id="7c4bf-116">**gx_bidi_resolved_text_info_text**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-116">**gx_bidi_resolved_text_info_text**</span></span>             | <span data-ttu-id="7c4bf-117">Yeniden sıralanan bidi metni dizisine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="7c4bf-117">Pointer to the array of reordered bidi text</span></span> |
| <span data-ttu-id="7c4bf-118">**gx_bidi_resolved_text_info_total_lines**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-118">**gx_bidi_resolved_text_info_total_lines**</span></span>      | <span data-ttu-id="7c4bf-119">Tek bir paragraf için çözülen çift yönlü metnin toplam satırları</span><span class="sxs-lookup"><span data-stu-id="7c4bf-119">Total lines of resolved bidi text for one paragraph</span></span> |
| <span data-ttu-id="7c4bf-120">**gx_bidi_resolved_text_info_next**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-120">**gx_bidi_resolved_text_info_next**</span></span>             | <span data-ttu-id="7c4bf-121">Sonraki paragraf için çift yönlü metin bilgileri çözüldü</span><span class="sxs-lookup"><span data-stu-id="7c4bf-121">Resolved bidi text information for the next paragraph</span></span> |

## <a name="gx_circular_gauge_info"></a><span data-ttu-id="7c4bf-122">GX_CIRCULAR_GAUGE_INFO</span><span class="sxs-lookup"><span data-stu-id="7c4bf-122">GX_CIRCULAR_GAUGE_INFO</span></span>

### <a name="definition"></a><span data-ttu-id="7c4bf-123">Tanım</span><span class="sxs-lookup"><span data-stu-id="7c4bf-123">Definition</span></span>

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
### <a name="members"></a><span data-ttu-id="7c4bf-124">Üyeler</span><span class="sxs-lookup"><span data-stu-id="7c4bf-124">Members</span></span>

|                                                  |                                              |
| ------------------------------------------------ | -------------------------------------------- |
| <span data-ttu-id="7c4bf-125">**gx_circular_gauge_info_animation_steps**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-125">**gx_circular_gauge_info_animation_steps**</span></span>       | <span data-ttu-id="7c4bf-126">Geçerli iğne açısına göre yeni, atanan iğne açısına geçiş yaparken, iğne 'nin hareket ettirme toplam adım sayısı</span><span class="sxs-lookup"><span data-stu-id="7c4bf-126">Total steps the needle will travel through when moving from the current needle angle to a newly assigned needle angle</span></span> |
| <span data-ttu-id="7c4bf-127">**gx_circular_gauge_info_animation_delay**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-127">**gx_circular_gauge_info_animation_delay**</span></span>       | <span data-ttu-id="7c4bf-128">Animasyon adımları arasındaki gecikmede Gux saat Ticks sayısı</span><span class="sxs-lookup"><span data-stu-id="7c4bf-128">The number of GUIX clock ticks to delay between animation steps</span></span> |
| <span data-ttu-id="7c4bf-129">**gx_circular_gauge_info_needle_xpos**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-129">**gx_circular_gauge_info_needle_xpos**</span></span>           | <span data-ttu-id="7c4bf-130">Ölçer pencere öğesinin solundaki uzaklık, ölçer iğne 'nin ortasına kadar olan mesafe</span><span class="sxs-lookup"><span data-stu-id="7c4bf-130">The distance from the left of the gauge widget to the center-of-rotation of the gauge needle</span></span> |
| <span data-ttu-id="7c4bf-131">**gx_circular_gauge_info_needle_ypos**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-131">**gx_circular_gauge_info_needle_ypos**</span></span>           | <span data-ttu-id="7c4bf-132">Ölçer pencere öğesinin en üstünden ölçer iğne 'nin ortasına olan uzaklık</span><span class="sxs-lookup"><span data-stu-id="7c4bf-132">The distance from the top of the gauge widget to the center-of-rotation of the gauge needle</span></span> |
| <span data-ttu-id="7c4bf-133">**gx_circular_gauge_info_needle_xcor**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-133">**gx_circular_gauge_info_needle_xcor**</span></span>           | <span data-ttu-id="7c4bf-134">İğne resminin solundaki mesafe, ölçer iğne 'nin ortasına kadar</span><span class="sxs-lookup"><span data-stu-id="7c4bf-134">The distance from the left of the needle image to the center-of-rotation of the gauge needle</span></span> |
| <span data-ttu-id="7c4bf-135">**gx_circular_gauge_info_needle_ycor**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-135">**gx_circular_gauge_info_needle_ycor**</span></span>           | <span data-ttu-id="7c4bf-136">İğne resminin en üstünden ölçer iğne 'nin ortasına kadar olan mesafe</span><span class="sxs-lookup"><span data-stu-id="7c4bf-136">The distance from the top of the needle image to the center-of-rotation of the gauge needle</span></span> |
| <span data-ttu-id="7c4bf-137">**gx_circular_gauge_info_needle_pixelmap**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-137">**gx_circular_gauge_info_needle_pixelmap**</span></span>       | <span data-ttu-id="7c4bf-138">Ölçer iğne çizmek için kullanılacak olan pixelmap 'in kaynak KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="7c4bf-138">Resource ID of the pixelmap which will be used to draw the gauge needle.</span></span> <span data-ttu-id="7c4bf-139">Bu görüntü ölçer pencere öğesinin gerektiği şekilde döndürüldüğü şekilde döndürülecektir ve ölçer iğne herhangi bir konumda görüntülenir</span><span class="sxs-lookup"><span data-stu-id="7c4bf-139">This image will be rotated as needed by the gauge widget to display the gauge needle in any position</span></span> |

<span data-ttu-id="7c4bf-140">Aşağıdaki diyagramda XPos, YPos ve xcor ycor koordinatları gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="7c4bf-140">The diagram below illustrates the xpos, ypos, and xcor, ycor coordinates:</span></span>

![Iğne Y ve X koordinatları diyagramı](./media/guix/image8.png)

## <a name="gx_line_chart_info"></a><span data-ttu-id="7c4bf-142">GX_LINE_CHART_INFO</span><span class="sxs-lookup"><span data-stu-id="7c4bf-142">GX_LINE_CHART_INFO</span></span>

### <a name="definition"></a><span data-ttu-id="7c4bf-143">Tanım</span><span class="sxs-lookup"><span data-stu-id="7c4bf-143">Definition</span></span>

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

### <a name="members"></a><span data-ttu-id="7c4bf-144">Üyeler</span><span class="sxs-lookup"><span data-stu-id="7c4bf-144">Members</span></span>

|                                    |                                                            |
| ---------------------------------- | ---------------------------------------------------------- |
| <span data-ttu-id="7c4bf-145">**gx_line_chart_min_val**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-145">**gx_line_chart_min_val**</span></span>          | <span data-ttu-id="7c4bf-146">Ölçeklendirmeyi hesaplamak için kullanılan minimum veri değeri</span><span class="sxs-lookup"><span data-stu-id="7c4bf-146">The minimum data value, which is used to calculate scaling</span></span>
| <span data-ttu-id="7c4bf-147">**gx_line_chart_max_val**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-147">**gx_line_chart_max_val**</span></span>          | <span data-ttu-id="7c4bf-148">Ölçeklendirmeyi hesaplamak için kullanılan maksimum veri değeri</span><span class="sxs-lookup"><span data-stu-id="7c4bf-148">The maximum data value, which is used to calculate scaling</span></span> |
| <span data-ttu-id="7c4bf-149">**gx_line_chart_data**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-149">**gx_line_chart_data**</span></span>             | <span data-ttu-id="7c4bf-150">Tamsayı değerleri dizisine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="7c4bf-150">Pointer to an array of integer values.</span></span> <span data-ttu-id="7c4bf-151">Bunlar çizgi grafik pencere öğesi tarafından çizilen tamsayı değerlerdir</span><span class="sxs-lookup"><span data-stu-id="7c4bf-151">These are the integer values plotted by the line chart widget</span></span> |
| <span data-ttu-id="7c4bf-152">**gx_line_ <side> _margin**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-152">**gx_line_<side>_margin**</span></span>          | <span data-ttu-id="7c4bf-153">Grafik penceresi dış alanının gerçek grafik işleme alanına göre sınırı.</span><span class="sxs-lookup"><span data-stu-id="7c4bf-153">The offset from the chart window outer bound to the actual chart rendering area.</span></span> <span data-ttu-id="7c4bf-154">Grafik ekseni ve veri satırı her zaman bu iç sınır içinde çizilir. Bu, uygulamanın grafik penceresi içinde, ancak char grafikalanı dışında Etiketler ve diğer bilgiler çizmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="7c4bf-154">The chart axis and data line are always plotted within this inner boundary, which allows the application to draw labels and other information inside the chart window but outside the char graphing area</span></span> |
| <span data-ttu-id="7c4bf-155">**gx_line_chart_max_data_count**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-155">**gx_line_chart_max_data_count**</span></span>   | <span data-ttu-id="7c4bf-156">Mevcut olabilecek veri değerlerinin sayısı.</span><span class="sxs-lookup"><span data-stu-id="7c4bf-156">The number of data values which may be present.</span></span> <span data-ttu-id="7c4bf-157">Bu parametre, veri noktalarını çizmek için x ekseninin ölçeğini veya aralığını hesaplamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7c4bf-157">This parameter is used for calculating the x-axis scaling or interval for plotting data points.</span></span> |
| <span data-ttu-id="7c4bf-158">**gx_line_active_data_count**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-158">**gx_line_active_data_count**</span></span>      | <span data-ttu-id="7c4bf-159">Veri dizisinde gerçekten mevcut olan veri değerlerinin sayısı.</span><span class="sxs-lookup"><span data-stu-id="7c4bf-159">The number of data values that actually present in the data array.</span></span> <span data-ttu-id="7c4bf-160">Çizgi grafik, en fazla 100 değer çizmek için ölçeklendirilebilir (örneğin), ancak belirli bir güncelleştirmede daha az sayıda veri değeri bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="7c4bf-160">A line chart may be scaled to draw a maximum of 100 values (for example), but on any particular update a smaller number of data values may actually be present.</span></span> |
| <span data-ttu-id="7c4bf-161">**gx_line_axis_line_width**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-161">**gx_line_axis_line_width**</span></span>        | <span data-ttu-id="7c4bf-162">Yatay ve dikey ekseni çizmek için kullanılan çizginin genişliği</span><span class="sxs-lookup"><span data-stu-id="7c4bf-162">Width of the line used to draw the horizontal and vertical axis</span></span> |
| <span data-ttu-id="7c4bf-163">**gx_line_data_line_width**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-163">**gx_line_data_line_width**</span></span>        | <span data-ttu-id="7c4bf-164">Çizilen veri çizgisinin genişliği</span><span class="sxs-lookup"><span data-stu-id="7c4bf-164">Width of the plotted data line</span></span> |
| <span data-ttu-id="7c4bf-165">**gx_line_chart_axis_color**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-165">**gx_line_chart_axis_color**</span></span>       | <span data-ttu-id="7c4bf-166">Eksen çizgilerini çizmek için kullanılan rengin kaynak KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="7c4bf-166">Resource ID of the color used to draw the axis lines</span></span> |
| <span data-ttu-id="7c4bf-167">**gx_line_chart_line_color**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-167">**gx_line_chart_line_color**</span></span>       | <span data-ttu-id="7c4bf-168">Grafik veri çizgisini çizmek için kullanılan rengin kaynak KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="7c4bf-168">Resource ID of the color used to draw the chart data line</span></span> |

## <a name="gx_mouse_cursor_info"></a><span data-ttu-id="7c4bf-169">GX_MOUSE_CURSOR_INFO</span><span class="sxs-lookup"><span data-stu-id="7c4bf-169">GX_MOUSE_CURSOR_INFO</span></span> 

### <a name="definition"></a><span data-ttu-id="7c4bf-170">Tanım</span><span class="sxs-lookup"><span data-stu-id="7c4bf-170">Definition</span></span>

```c
typedef struct GX_MOUSE_CURSOR_INFO_STRUCT
{
    GX_RESOURCE_ID             gx_mouse_cursor_image_id;
    GX_VALUE                   gx_mouse_cursor_hotspot_x;
    GX_VALUE                   gx_mouse_cursor_hotspot_y;
} GX_MOUSE_CURSOR_INFO;
```

### <a name="members"></a><span data-ttu-id="7c4bf-171">Üyeler</span><span class="sxs-lookup"><span data-stu-id="7c4bf-171">Members</span></span>

|                                    |                                                            |
| ---------------------------------- | ---------------------------------------------------------- |
| <span data-ttu-id="7c4bf-172">**gx_mouse_cursor_image_id**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-172">**gx_mouse_cursor_image_id**</span></span>       | <span data-ttu-id="7c4bf-173">Fare resminin kaynak KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="7c4bf-173">Resource ID of the mouse image</span></span> |
| <span data-ttu-id="7c4bf-174">**gx_mouse_cursor_hotspot_x**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-174">**gx_mouse_cursor_hotspot_x**</span></span>      | <span data-ttu-id="7c4bf-175">Fare resminin solundaki fare resmi etkin noktası arasındaki fark</span><span class="sxs-lookup"><span data-stu-id="7c4bf-175">The offset from the left of the mouse image to the mouse image hotspot</span></span> |
| <span data-ttu-id="7c4bf-176">**gx_mouse_cursor_hotspot_y**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-176">**gx_mouse_cursor_hotspot_y**</span></span>      | <span data-ttu-id="7c4bf-177">Fare resminin en üstünden fare resmi etkin noktaya kadar olan fark</span><span class="sxs-lookup"><span data-stu-id="7c4bf-177">The offset from the top of the mouse image to the mouse image hotspot</span></span> |

## <a name="gx_pen_configuration"></a><span data-ttu-id="7c4bf-178">GX_PEN_CONFIGURATION</span><span class="sxs-lookup"><span data-stu-id="7c4bf-178">GX_PEN_CONFIGURATION</span></span> 

### <a name="definition"></a><span data-ttu-id="7c4bf-179">Tanım</span><span class="sxs-lookup"><span data-stu-id="7c4bf-179">Definition</span></span>

```c
typedef struct GX_PEN_CONFIGURATION_STRUCT
{
    GX_FIXED_VAL     gx_pen_configuration_min_drag_dist;
    UINT             gx_pen_configuration_max_pen_speed_ticks;
}GX_PEN_CONFIGURATION;
```

### <a name="members"></a><span data-ttu-id="7c4bf-180">Üyeler</span><span class="sxs-lookup"><span data-stu-id="7c4bf-180">Members</span></span>

|                                              |                                                  |
| -------------------------------------------- | ------------------------------------------------ |
| <span data-ttu-id="7c4bf-181">**gx_pen_configuration_min_drag_dist**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-181">**gx_pen_configuration_min_drag_dist**</span></span>       | <span data-ttu-id="7c4bf-182">Bir hareket olayı tetiklemek için Gux süreölçeri başına en az sürükleme uzaklığı.</span><span class="sxs-lookup"><span data-stu-id="7c4bf-182">The minimum drag distance per GUIX timer tick to trigger an FLICK event.</span></span> <span data-ttu-id="7c4bf-183">Sabit bir nokta veri türü değeri oluşturmak için GX_FIXED_VAL_MAKE çağırın</span><span class="sxs-lookup"><span data-stu-id="7c4bf-183">Call GX_FIXED_VAL_MAKE to make a fixed point data type value</span></span> |
| <span data-ttu-id="7c4bf-184">**gx_pen_configuration_max_pen_speed_ticks**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-184">**gx_pen_configuration_max_pen_speed_ticks**</span></span> | <span data-ttu-id="7c4bf-185">Bir hareket olayı tetiklemek için Gux süreölçer işaretleri cinsinden maksimum sürükleme hızı</span><span class="sxs-lookup"><span data-stu-id="7c4bf-185">The maximum drag speed in GUIX timer ticks to trigger an FLICK event</span></span> | 

## <a name="gx_pixelmap_slider_info"></a><span data-ttu-id="7c4bf-186">GX_PIXELMAP_SLIDER_INFO</span><span class="sxs-lookup"><span data-stu-id="7c4bf-186">GX_PIXELMAP_SLIDER_INFO</span></span> 

### <a name="definition"></a><span data-ttu-id="7c4bf-187">Tanım</span><span class="sxs-lookup"><span data-stu-id="7c4bf-187">Definition</span></span>

```c
typedef struct GX_PIXELMAP_SLIDER_INFO_STRUCT
{
    GX_RESOURCE_ID gx_pixelmap_slider_info_lower_background_pixelmap;
    GX_RESOURCE_ID gx_pixelmap_slider_info_upper_background_pixelmap;
    GX_RESOURCE_ID gx_pixelmap_slider_info_needle_pixelmap;
} GX_PIXELMAP_SLIDER_INFO;
```

### <a name="members"></a><span data-ttu-id="7c4bf-188">Üyeler</span><span class="sxs-lookup"><span data-stu-id="7c4bf-188">Members</span></span>

|                                                       |                                          |
| ----------------------------------------------------- | ---------------------------------------- |
| <span data-ttu-id="7c4bf-189">**gx_pixelmap_slider_info_lower_background_pixelmap**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-189">**gx_pixelmap_slider_info_lower_background_pixelmap**</span></span> | <span data-ttu-id="7c4bf-190">İğne 'dan önce arka planı doldurmak için pixelmap 'in kaynak KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="7c4bf-190">Resource ID of the pixelmap for filling the background before the needle.</span></span> <span data-ttu-id="7c4bf-191">Üst arka plan pixelmap ayarlanmamışsa, arka planı yalnızca iğne 'den önce ve sonra doldurmak için kullanılır</span><span class="sxs-lookup"><span data-stu-id="7c4bf-191">If upper background pixelmap is not set, it’s used for filling background both before and after the needle</span></span> |
| <span data-ttu-id="7c4bf-192">**gx_pixelmap_slider_info_upper_background_pixelmap**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-192">**gx_pixelmap_slider_info_upper_background_pixelmap**</span></span> | <span data-ttu-id="7c4bf-193">İğne 'tan sonra arka planı doldurmak için pixelmap 'in kaynak KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="7c4bf-193">Resource ID of the pixelmap for filling background after the needle</span></span> |
| <span data-ttu-id="7c4bf-194">**gx_pixelmap_slider_info_needle_pixelmap**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-194">**gx_pixelmap_slider_info_needle_pixelmap**</span></span>           | <span data-ttu-id="7c4bf-195">İğne pixelmap 'in kaynak KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="7c4bf-195">Resource ID of the needle pixelmap</span></span> |

## <a name="gx_progress_bar_info"></a><span data-ttu-id="7c4bf-196">GX_PROGRESS_BAR_INFO</span><span class="sxs-lookup"><span data-stu-id="7c4bf-196">GX_PROGRESS_BAR_INFO</span></span> 

### <a name="definition"></a><span data-ttu-id="7c4bf-197">**Tanım**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-197">**Definition**</span></span>

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

### <a name="members"></a><span data-ttu-id="7c4bf-198">Üyeler</span><span class="sxs-lookup"><span data-stu-id="7c4bf-198">Members</span></span>

|                                              |                                                  |
| -------------------------------------------- | ------------------------------------------------ |
| <span data-ttu-id="7c4bf-199">**gx_progress_bar_info_min_val**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-199">**gx_progress_bar_info_min_val**</span></span>             | <span data-ttu-id="7c4bf-200">Raporlanan en düşük değer</span><span class="sxs-lookup"><span data-stu-id="7c4bf-200">Minimum reported value</span></span> |
| <span data-ttu-id="7c4bf-201">**gx_progress_bar_info_max_val**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-201">**gx_progress_bar_info_max_val**</span></span>             | <span data-ttu-id="7c4bf-202">Raporlanan en yüksek değer</span><span class="sxs-lookup"><span data-stu-id="7c4bf-202">Maximum reported value</span></span> |
| <span data-ttu-id="7c4bf-203">**gx_progress_bar_info_current_val**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-203">**gx_progress_bar_info_current_val**</span></span>         | <span data-ttu-id="7c4bf-204">Geçerli değer</span><span class="sxs-lookup"><span data-stu-id="7c4bf-204">Current value</span></span> |
| <span data-ttu-id="7c4bf-205">**gx_progress_bar_info_font_id**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-205">**gx_progress_bar_info_font_id**</span></span>             | <span data-ttu-id="7c4bf-206">İlerleme çubuğu pencere öğesi içinde isteğe bağlı metin değerini çizmek için kullanılan yazı tipinin kaynak KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="7c4bf-206">Resource ID of the font, used to draw the optional text value within the progress bar widget</span></span>      |
| <span data-ttu-id="7c4bf-207">**gx_progress_bar_normal_text_color**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-207">**gx_progress_bar_normal_text_color**</span></span>        | <span data-ttu-id="7c4bf-208">İlerleme çubuğu pencere öğesi içinde isteğe bağlı metin çizimini tanımlamak için kullanılan, normal durumdaki metin renginin kaynak KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="7c4bf-208">Resource ID of the text color in normal state, used to define the optional text drawing within the progress bar widget</span></span> |
| <span data-ttu-id="7c4bf-209">**gx_progress_bar_selected_text_color**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-209">**gx_progress_bar_selected_text_color**</span></span>      | <span data-ttu-id="7c4bf-210">Pencere öğesi odaklanıldığında metin renginin kaynak KIMLIĞI, ilerleme çubuğu pencere öğesi içinde isteğe bağlı metin çizimini tanımlamak için kullanılır</span><span class="sxs-lookup"><span data-stu-id="7c4bf-210">Resource ID of the text color when the widget gain focus, used to define the optional text drawing within the progress bar widget</span></span> |
| <span data-ttu-id="7c4bf-211">**gx_progress_bar_disabled_text_color**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-211">**gx_progress_bar_disabled_text_color**</span></span>      | <span data-ttu-id="7c4bf-212">GX_STYLE_ENABLED etkin olmadığında metin renginin kaynak KIMLIĞI, ilerleme çubuğu pencere öğesi içinde isteğe bağlı metin çizimini tanımlamak için kullanılır</span><span class="sxs-lookup"><span data-stu-id="7c4bf-212">Resource ID of the text color when GX_STYLE_ENABLED is not active, used to define the optional text drawing within the progress bar widget</span></span> |
| <span data-ttu-id="7c4bf-213">**gx_progress_bar_fill_pixelmap**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-213">**gx_progress_bar_fill_pixelmap**</span></span>            | <span data-ttu-id="7c4bf-214">Arka plan doldurma için pixelmap 'in kaynak KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="7c4bf-214">Resource ID of the pixelmap for background filling</span></span>|

## <a name="gx_radial_progress_bar_info"></a><span data-ttu-id="7c4bf-215">GX_RADIAL_PROGRESS_BAR_INFO</span><span class="sxs-lookup"><span data-stu-id="7c4bf-215">GX_RADIAL_PROGRESS_BAR_INFO</span></span>

### <a name="definition"></a><span data-ttu-id="7c4bf-216">Tanım</span><span class="sxs-lookup"><span data-stu-id="7c4bf-216">Definition</span></span>

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

### <a name="members"></a><span data-ttu-id="7c4bf-217">Üyeler</span><span class="sxs-lookup"><span data-stu-id="7c4bf-217">Members</span></span>

|                                                   |                                              |
| ------------------------------------------------- | -------------------------------------------- |
| <span data-ttu-id="7c4bf-218">**gx_radial_progress_bar_info_xcenter**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-218">**gx_radial_progress_bar_info_xcenter**</span></span>           | <span data-ttu-id="7c4bf-219">X koordinatı içindeki pencere öğesi konumu</span><span class="sxs-lookup"><span data-stu-id="7c4bf-219">Widget position in x coordinate</span></span> |
| <span data-ttu-id="7c4bf-220">**gx_radial_progress_bar_info_ycenter**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-220">**gx_radial_progress_bar_info_ycenter**</span></span>           | <span data-ttu-id="7c4bf-221">Y koordinatı pencere öğesi konumu</span><span class="sxs-lookup"><span data-stu-id="7c4bf-221">Widget position in y coordinate</span></span>  |
| <span data-ttu-id="7c4bf-222">**gx_radial_progress_bar_info_radius**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-222">**gx_radial_progress_bar_info_radius**</span></span>            | <span data-ttu-id="7c4bf-223">İlerleme çemberin yarıçapı</span><span class="sxs-lookup"><span data-stu-id="7c4bf-223">Radius of the progress circle</span></span> |
| <span data-ttu-id="7c4bf-224">**gx_radial_progress_bar_info_current_val**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-224">**gx_radial_progress_bar_info_current_val**</span></span>       | <span data-ttu-id="7c4bf-225">[-360, 360] aralığıyla sınırlı geçerli değer, yer işareti konumu ve üst yayı bitiş noktası arasındaki angular Delta değerini gösterir. Negatif değer, bağlayıcının bağlantı konumundan başlayarak saat yönünde bir yönde çizilmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="7c4bf-225">Current value, limited to the range [-360, 360], indicates the angular delta between the anchor position and the end point of the upper arc. Negative value causes the arc to be drawn in a clockwise direction starting at the anchor position.</span></span> <span data-ttu-id="7c4bf-226">Pozitif değer, bağlayıcının bağlantı konumundan başlayarak saat yönünde bir yönde çizilmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="7c4bf-226">Positive value causes the arc to be drawn in a counter-clockwise direction starting at the anchor position.</span></span> <span data-ttu-id="7c4bf-227">Uygulama, ilerleme çubuğu pencere öğesine bir angular değeri atamak için belirtilen gerçek sözcüklü değeri ölçeklendirmelidir</span><span class="sxs-lookup"><span data-stu-id="7c4bf-227">The application must scale the real-word value being indicated to assign an angular value to the progress bar widget</span></span> |
| <span data-ttu-id="7c4bf-228">**gx_radial_progress_bar_anchor_val**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-228">**gx_radial_progress_bar_anchor_val**</span></span>             | <span data-ttu-id="7c4bf-229">Üst ilerleme yayı başlangıç açısı. Değer, doğru ve 90 dereceyle işaret eden 0 derecelik tamsayı derecesi cinsinden tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="7c4bf-229">Starting angle of the upper progress arc. The value is defined in terms of integer degree with 0 degree pointing to the right and 90 degree indicating straight up position.</span></span> |
| <span data-ttu-id="7c4bf-230">**gx_radial_progress_bar_font_id**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-230">**gx_radial_progress_bar_font_id**</span></span>                | <span data-ttu-id="7c4bf-231">İlerleme çubuğu pencere öğesi içinde isteğe bağlı metin değerini çizmek için kullanılan yazı tipinin kaynak KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="7c4bf-231">Resource ID of the font used to draw the optional text value within the progress bar widget</span></span> |
| <span data-ttu-id="7c4bf-232">**gx_radial_progress_bar_normal_text_color**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-232">**gx_radial_progress_bar_normal_text_color**</span></span>      | <span data-ttu-id="7c4bf-233">İlerleme çubuğu pencere öğesi içinde isteğe bağlı metin çizimini tanımlamak için kullanılan, normal durumdaki metin renginin kaynak KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="7c4bf-233">Resource ID of the text color in normal state, used to define the optional text drawing within the progress bar widget</span></span> |
| <span data-ttu-id="7c4bf-234">**gx_radial_progress_bar_selected_text_color**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-234">**gx_radial_progress_bar_selected_text_color**</span></span>    |<span data-ttu-id="7c4bf-235">Pencere öğesi odaklı metin renginin kaynak KIMLIĞI, ilerleme çubuğu pencere öğesi içinde isteğe bağlı metin çizimini tanımlamak için kullanılır</span><span class="sxs-lookup"><span data-stu-id="7c4bf-235">Resource ID of the text color when widget gain focus, used to define the optional text drawing within the progress bar widget</span></span> |
| <span data-ttu-id="7c4bf-236">**gx_radial_progress_bar_disabled_text_color**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-236">**gx_radial_progress_bar_disabled_text_color**</span></span>    | <span data-ttu-id="7c4bf-237">GX_STYLE_ENABLED etkin olmadığında metin renginin kaynak KIMLIĞI, ilerleme çubuğu pencere öğesi içinde isteğe bağlı metin çizimini tanımlamak için kullanılır</span><span class="sxs-lookup"><span data-stu-id="7c4bf-237">Resource ID of the text color when GX_STYLE_ENABLED is not active, used to define the optional text drawing within the progress bar widget</span></span> |
| <span data-ttu-id="7c4bf-238">**gx_radial_progress_bar_normal_brush_width**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-238">**gx_radial_progress_bar_normal_brush_width**</span></span>     | <span data-ttu-id="7c4bf-239">Düşük ilerleme çemberin genişliği</span><span class="sxs-lookup"><span data-stu-id="7c4bf-239">Width of the lower progress circle</span></span> |
| <span data-ttu-id="7c4bf-240">**gx_radial_progress_bar_selected_brush_width**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-240">**gx_radial_progress_bar_selected_brush_width**</span></span>   | <span data-ttu-id="7c4bf-241">Üstteki ilerleme yayı genişliği, üst yay daha dar, ile aynı veya daha büyük bir daireye eşit olabilir</span><span class="sxs-lookup"><span data-stu-id="7c4bf-241">Width of the upper progress arc, the upper arc may be narrower, the same as, or wider than the lower circle</span></span> |
| <span data-ttu-id="7c4bf-242">**gx_radial_progress_bar_normal_brush_color**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-242">**gx_radial_progress_bar_normal_brush_color**</span></span>     | <span data-ttu-id="7c4bf-243">Düşük ilerleme çemberi dolduracak rengin kaynak KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="7c4bf-243">Resource ID of the color to fill lower progress circle</span></span> |
| <span data-ttu-id="7c4bf-244">**gx_radial_progress_bar_selected_brush_color**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-244">**gx_radial_progress_bar_selected_brush_color**</span></span>   | <span data-ttu-id="7c4bf-245">Üst ilerleme yaya dolduracak rengin kaynak KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="7c4bf-245">Resource ID of the color to fill upper progress arc</span></span> |

## <a name="gx_radial_slider_info"></a><span data-ttu-id="7c4bf-246">GX_RADIAL_SLIDER_INFO</span><span class="sxs-lookup"><span data-stu-id="7c4bf-246">GX_RADIAL_SLIDER_INFO</span></span> 

### <a name="definition"></a><span data-ttu-id="7c4bf-247">Tanım</span><span class="sxs-lookup"><span data-stu-id="7c4bf-247">Definition</span></span>

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

### <a name="members"></a><span data-ttu-id="7c4bf-248">Üyeler</span><span class="sxs-lookup"><span data-stu-id="7c4bf-248">Members</span></span>

|                                               |                                                  |
| --------------------------------------------- | ------------------------------------------------ |
<span data-ttu-id="7c4bf-249">**gx_radial_slider_info_xcenter**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-249">**gx_radial_slider_info_xcenter**</span></span>               | <span data-ttu-id="7c4bf-250">Kaydırıcı pencere öğesinin sol tarafında bulunan kaydırıcı iğne 'nin ortasına mesafe</span><span class="sxs-lookup"><span data-stu-id="7c4bf-250">Distance from the left of the slider widget to the center-of-rotation of the slider needle</span></span> |
| <span data-ttu-id="7c4bf-251">**gx_radial_slider_info_ycenter**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-251">**gx_radial_slider_info_ycenter**</span></span>             | <span data-ttu-id="7c4bf-252">Kaydırıcı pencere öğesinin üstünden kaydırıcı iğne 'nin ortasına kadar uzaklık</span><span class="sxs-lookup"><span data-stu-id="7c4bf-252">Distance from the top of the slider widget to the center-of-rotation of the slider needle</span></span> |
| <span data-ttu-id="7c4bf-253">**gx_radial_slider_info_radius**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-253">**gx_radial_slider_info_radius**</span></span>              | <span data-ttu-id="7c4bf-254">Radyal kaydırıcı çemberin yarıçapı</span><span class="sxs-lookup"><span data-stu-id="7c4bf-254">Radius of the radial slider circle</span></span> |
| <span data-ttu-id="7c4bf-255">**gx_radial_slider_info_track_width**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-255">**gx_radial_slider_info_track_width**</span></span>         | <span data-ttu-id="7c4bf-256">Radyal kaydırıcı izlemenin genişliği</span><span class="sxs-lookup"><span data-stu-id="7c4bf-256">Width of radial slider track</span></span> |
| <span data-ttu-id="7c4bf-257">**gx_radial_slider_info_current_angle**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-257">**gx_radial_slider_info_current_angle**</span></span>       | <span data-ttu-id="7c4bf-258">Geçerli kaydırıcı açısı</span><span class="sxs-lookup"><span data-stu-id="7c4bf-258">Current slider angle</span></span> |
| <span data-ttu-id="7c4bf-259">**gx_radial_slider_info_min_angle**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-259">**gx_radial_slider_info_min_angle**</span></span>           | <span data-ttu-id="7c4bf-260">Minimum kaydırıcı açısı</span><span class="sxs-lookup"><span data-stu-id="7c4bf-260">Minimum slider angle</span></span> |
| <span data-ttu-id="7c4bf-261">**gx_radial_slider_info_max_angle**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-261">**gx_radial_slider_info_max_angle**</span></span>           | <span data-ttu-id="7c4bf-262">Maksimum kaydırıcı açısı</span><span class="sxs-lookup"><span data-stu-id="7c4bf-262">Maximum slider angle</span></span> |
| <span data-ttu-id="7c4bf-263">**gx_radial_slider_info_angle_list**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-263">**gx_radial_slider_info_angle_list**</span></span>          | <span data-ttu-id="7c4bf-264">Açı değeri listesi, küme açılarını tanımlar, ayarlandıysa, kaydırıcı açısı yalnızca tanımlı çapa açılarının biri olabilir</span><span class="sxs-lookup"><span data-stu-id="7c4bf-264">Angle value list, defines anchor angles, if set, slider angle can only be one of the defined anchor angles</span></span> |
| <span data-ttu-id="7c4bf-265">**gx_radial_slider_info_list_count**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-265">**gx_radial_slider_info_list_count**</span></span>          | <span data-ttu-id="7c4bf-266">Çapa açısı sayısı</span><span class="sxs-lookup"><span data-stu-id="7c4bf-266">Number of anchor angles</span></span> |
| <span data-ttu-id="7c4bf-267">**gx_radial_slider_info_background_pixelmap**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-267">**gx_radial_slider_info_background_pixelmap**</span></span> | <span data-ttu-id="7c4bf-268">Arka plan pixelmap kaynak KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="7c4bf-268">Resource ID of background pixelmap</span></span> |
| <span data-ttu-id="7c4bf-269">**gx_radial_slider_info_needle_pixelmap**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-269">**gx_radial_slider_info_needle_pixelmap**</span></span>     | <span data-ttu-id="7c4bf-270">İğne pixelmap kaynak KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="7c4bf-270">Resource ID of needle pixelmap</span></span> |

## <a name="gx_rectangle"></a><span data-ttu-id="7c4bf-271">GX_RECTANGLE</span><span class="sxs-lookup"><span data-stu-id="7c4bf-271">GX_RECTANGLE</span></span>

### <a name="definition"></a><span data-ttu-id="7c4bf-272">Tanım</span><span class="sxs-lookup"><span data-stu-id="7c4bf-272">Definition</span></span>

```c
typedef struct GX_RECTANGLE_STRUCT
{
    GX_VALUE gx_rectangle_left;
    GX_VALUE gx_rectangle_top;
    GX_VALUE gx_rectangle_right;
    GX_VALUE gx_rectangle_bottom;
} GX_RECTANGLE;
```

### <a name="members"></a><span data-ttu-id="7c4bf-273">Üyeler</span><span class="sxs-lookup"><span data-stu-id="7c4bf-273">Members</span></span>

|                                  |                         |
| -------------------------------- | ------------------------|
| <span data-ttu-id="7c4bf-274">**gx_rectangle_left**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-274">**gx_rectangle_left**</span></span>            | <span data-ttu-id="7c4bf-275">Dikdörtgenin sol tarafında</span><span class="sxs-lookup"><span data-stu-id="7c4bf-275">Left of the rectangle</span></span>   |  
| <span data-ttu-id="7c4bf-276">**gx_rectangle_top**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-276">**gx_rectangle_top**</span></span>             | <span data-ttu-id="7c4bf-277">Dikdörtgenin üstü</span><span class="sxs-lookup"><span data-stu-id="7c4bf-277">Top of the rectangle</span></span>    | 
| <span data-ttu-id="7c4bf-278">**gx_rectangle_right**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-278">**gx_rectangle_right**</span></span>           | <span data-ttu-id="7c4bf-279">Dikdörtgenin sağ</span><span class="sxs-lookup"><span data-stu-id="7c4bf-279">Right of the rectangle</span></span>  |
| <span data-ttu-id="7c4bf-280">**gx_rectangle_bottom**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-280">**gx_rectangle_bottom**</span></span>          | <span data-ttu-id="7c4bf-281">Dikdörtgenin altı</span><span class="sxs-lookup"><span data-stu-id="7c4bf-281">Bottom of the rectangle</span></span> |

## <a name="gx_rich_text_fonts"></a><span data-ttu-id="7c4bf-282">GX_RICH_TEXT_FONTS</span><span class="sxs-lookup"><span data-stu-id="7c4bf-282">GX_RICH_TEXT_FONTS</span></span> 

### <a name="definition"></a><span data-ttu-id="7c4bf-283">Tanım</span><span class="sxs-lookup"><span data-stu-id="7c4bf-283">Definition</span></span>

```c
typedef struct GX_RICH_TEXT_FONTS_STRUCT
{
    GX_RESOURCE_ID             gx_rich_text_fonts_normal_id;
    GX_RESOURCE_ID             gx_rich_text_fonts_bold_id;
    GX_RESOURCE_ID             gx_rich_text_fonts_italic_id;
    GX_RESOURCE_ID             gx_rich_text_fonts_bold_italic_id;
} GX_RICH_TEXT_FONTS;
```

### <a name="members"></a><span data-ttu-id="7c4bf-284">Üyeler</span><span class="sxs-lookup"><span data-stu-id="7c4bf-284">Members</span></span>

|                                    |                                                            |
| ---------------------------------- | ---------------------------------------------------------- |
| <span data-ttu-id="7c4bf-285">**gx_rich_text_fonts_normal_id**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-285">**gx_rich_text_fonts_normal_id**</span></span>   | <span data-ttu-id="7c4bf-286">Normal metin yazı tipinin kaynak KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="7c4bf-286">Resource ID of normal text font</span></span> |
| <span data-ttu-id="7c4bf-287">**gx_rich_text_fonts_bold_id**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-287">**gx_rich_text_fonts_bold_id**</span></span>     | <span data-ttu-id="7c4bf-288">Kalın metin yazı tipinin kaynak KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="7c4bf-288">Resource ID of bold text font</span></span> |
| <span data-ttu-id="7c4bf-289">**gx_rich_text_fonts_italic_id**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-289">**gx_rich_text_fonts_italic_id**</span></span>   | <span data-ttu-id="7c4bf-290">İtalik metin yazı tipinin kaynak KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="7c4bf-290">Resource ID of italic text font</span></span> |
| <span data-ttu-id="7c4bf-291">**gx_rich_text_fonts_bold_italic_id**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-291">**gx_rich_text_fonts_bold_italic_id**</span></span> | <span data-ttu-id="7c4bf-292">Kalın italik metin yazı tipinin kaynak KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="7c4bf-292">Resource ID of bold italic text font</span></span> |

## <a name="gx_scroll_info"></a><span data-ttu-id="7c4bf-293">GX_SCROLL_INFO</span><span class="sxs-lookup"><span data-stu-id="7c4bf-293">GX_SCROLL_INFO</span></span> 
### <a name="definition"></a><span data-ttu-id="7c4bf-294">**Tanım**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-294">**Definition**</span></span>

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

### <a name="members"></a><span data-ttu-id="7c4bf-295">Üyeler</span><span class="sxs-lookup"><span data-stu-id="7c4bf-295">Members</span></span>

|                         |                               |
| ----------------------- | ----------------------------- |
| <span data-ttu-id="7c4bf-296">**gx_scroll_value**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-296">**gx_scroll_value**</span></span>     | <span data-ttu-id="7c4bf-297">Geçerli kaydırma konumu</span><span class="sxs-lookup"><span data-stu-id="7c4bf-297">Current scroll position</span></span>       |
| <span data-ttu-id="7c4bf-298">**gx_scroll_minimum**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-298">**gx_scroll_minimum**</span></span>   | <span data-ttu-id="7c4bf-299">Raporlanan en düşük konum</span><span class="sxs-lookup"><span data-stu-id="7c4bf-299">Minimum reported position</span></span>     |
| <span data-ttu-id="7c4bf-300">**gx_scroll_maximum**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-300">**gx_scroll_maximum**</span></span>   | <span data-ttu-id="7c4bf-301">Raporlanan en yüksek konum</span><span class="sxs-lookup"><span data-stu-id="7c4bf-301">Maximum reported position</span></span>     |
| <span data-ttu-id="7c4bf-302">**gx_scroll_visible**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-302">**gx_scroll_visible**</span></span>   | <span data-ttu-id="7c4bf-303">Üst pencere görünür aralığı</span><span class="sxs-lookup"><span data-stu-id="7c4bf-303">Parent window visible range</span></span>   |
| <span data-ttu-id="7c4bf-304">**gx_scroll_increment**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-304">**gx_scroll_increment**</span></span> | <span data-ttu-id="7c4bf-305">Kaydırma çubuğu en küçük delta değeri</span><span class="sxs-lookup"><span data-stu-id="7c4bf-305">Scrollbar minimum delta value</span></span> |

## <a name="gx_scrollbar_appearance"></a><span data-ttu-id="7c4bf-306">GX_SCROLLBAR_APPEARANCE</span><span class="sxs-lookup"><span data-stu-id="7c4bf-306">GX_SCROLLBAR_APPEARANCE</span></span> 

### <a name="definition"></a><span data-ttu-id="7c4bf-307">Tanım</span><span class="sxs-lookup"><span data-stu-id="7c4bf-307">Definition</span></span>

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

### <a name="members"></a><span data-ttu-id="7c4bf-308">Üyeler</span><span class="sxs-lookup"><span data-stu-id="7c4bf-308">Members</span></span>

|                                          |                                                       |
| ---------------------------------------- | ----------------------------------------------------- |
| <span data-ttu-id="7c4bf-309">**gx_scroll_width**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-309">**gx_scroll_width**</span></span>                      | <span data-ttu-id="7c4bf-310">ScrollBar pencere öğesinin piksel cinsinden genişliği</span><span class="sxs-lookup"><span data-stu-id="7c4bf-310">Width of the scrollbar widget, in pixels</span></span> |
| <span data-ttu-id="7c4bf-311">**gx_scroll_thumb_width**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-311">**gx_scroll_thumb_width**</span></span>                | <span data-ttu-id="7c4bf-312">Kaydırma çubuğu üzerindeki slaytları piksel cinsinden gösteren Thumb düğmesinin genişliği.</span><span class="sxs-lookup"><span data-stu-id="7c4bf-312">Width of the thumb button which slides on the scrollbar, in pixels.</span></span> <span data-ttu-id="7c4bf-313">Bu değer genellikle toplam kaydırma çubuğu genişliğinden az sayıda piksel daha küçüktür</span><span class="sxs-lookup"><span data-stu-id="7c4bf-313">This value is usually some number of pixels less than the total scrollbar width</span></span> |
| <span data-ttu-id="7c4bf-314">**gx_scroll_thumb_travel_min**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-314">**gx_scroll_thumb_travel_min**</span></span>           | <span data-ttu-id="7c4bf-315">Kaydırma çubuğunun sonundan en küçük parmak izi düğmesi seyahat noktası arasındaki fark.</span><span class="sxs-lookup"><span data-stu-id="7c4bf-315">Offset from the end of scrollbar to minimum thumb button travel point.</span></span> <span data-ttu-id="7c4bf-316">Bu sınır, parmak izinin kaydırma çubuğunun çok sonuna kadar hareket etmelerini engellemek için kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="7c4bf-316">This limit can be used to prevent the thumb button from traveling to the very end of the scrollbar</span></span> |
| <span data-ttu-id="7c4bf-317">**gx_scroll_thumb_travel_max**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-317">**gx_scroll_thumb_travel_max**</span></span>           | <span data-ttu-id="7c4bf-318">Kaydırma çubuğunun sonundan en fazla kaydırma düğmesi seyahat noktası arasındaki fark.</span><span class="sxs-lookup"><span data-stu-id="7c4bf-318">Offset from the end of scrollbar to maximum thumb button travel point.</span></span> <span data-ttu-id="7c4bf-319">Bu sınır, parmak izinin kaydırma çubuğunun çok sonuna kadar hareket etmelerini engellemek için kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="7c4bf-319">This limit can be used to prevent the thumb button from traveling to the very end of the scrollbar</span></span> |
| <span data-ttu-id="7c4bf-320">**gx_scroll_thumb_border_style**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-320">**gx_scroll_thumb_border_style**</span></span>         | <span data-ttu-id="7c4bf-321">Thumb düğmesinin kenarlık stilleri</span><span class="sxs-lookup"><span data-stu-id="7c4bf-321">Border styles of thumb button</span></span> |
| <span data-ttu-id="7c4bf-322">**gx_scroll_fill_pixelmap**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-322">**gx_scroll_fill_pixelmap**</span></span>              | <span data-ttu-id="7c4bf-323">İsteğe bağlı pixelmap KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="7c4bf-323">Optional pixelmap ID.</span></span> <span data-ttu-id="7c4bf-324">Bu pixelmap KIMLIĞI sıfır değilse, ScrollBar ScrollBar arka planını çizmek için bu pixelmap 'i kullanır</span><span class="sxs-lookup"><span data-stu-id="7c4bf-324">If this pixelmap ID is not zero, the scrollbar uses this pixelmap to draw the scrollbar background</span></span> |
| <span data-ttu-id="7c4bf-325">**gx_scroll_thumb_pixelmap**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-325">**gx_scroll_thumb_pixelmap**</span></span>             | <span data-ttu-id="7c4bf-326">İsteğe bağlı pixelmap KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="7c4bf-326">Optional pixelmap ID.</span></span> <span data-ttu-id="7c4bf-327">Bu pixelmap KIMLIĞI sıfır değilse, kaydırma çubuğu parmak izi düğmesi kendisini çizmek için bu pixelmap 'i kullanır</span><span class="sxs-lookup"><span data-stu-id="7c4bf-327">If this pixelmap ID is not zero, the scrollbar thumb button uses this pixelmap to draw itself</span></span> |
| <span data-ttu-id="7c4bf-328">**gx_scroll_up_pixelmap**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-328">**gx_scroll_up_pixelmap**</span></span>                | <span data-ttu-id="7c4bf-329">İsteğe bağlı pixelmap KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="7c4bf-329">Optional pixelmap ID.</span></span> <span data-ttu-id="7c4bf-330">Bu pixelmap KIMLIĞI sıfır değilse, kaydırma çubuğu bu pixelmap KIMLIĞINI kullanarak kaydırma çubuğunu sola/yukarı ucu düğme çiz</span><span class="sxs-lookup"><span data-stu-id="7c4bf-330">If this pixelmap ID is not zero, the scrollbar uses this pixelmap ID to draw the scrollbar left/up end button</span></span> |
| <span data-ttu-id="7c4bf-331">**gx_scroll_down_pixelmap**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-331">**gx_scroll_down_pixelmap**</span></span>              | <span data-ttu-id="7c4bf-332">İsteğe bağlı pixelmap KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="7c4bf-332">Optional pixelmap ID.</span></span> <span data-ttu-id="7c4bf-333">Bu pixelmap KIMLIĞI sıfır değilse, kaydırma çubuğu bu pixelmap KIMLIĞINI kullanarak kaydırma çubuğunu sağ/aşağı uç düğmesini çizin</span><span class="sxs-lookup"><span data-stu-id="7c4bf-333">If this pixelmap ID is not zero, the scrollbar uses this pixelmap ID to draw the scrollbar right/down end button</span></span> |
| <span data-ttu-id="7c4bf-334">**gx_scroll_thumb_color**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-334">**gx_scroll_thumb_color**</span></span>                | <span data-ttu-id="7c4bf-335">Thumb düğmesini doldurmanız için kullanılan rengin kaynak KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="7c4bf-335">Resource ID of color used to fill thumb button</span></span> |
| <span data-ttu-id="7c4bf-336">**gx_scroll_thumb_border_color**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-336">**gx_scroll_thumb_border_color**</span></span>         | <span data-ttu-id="7c4bf-337">Thumb düğmesinin kenarlığını çizmek için kullanılan rengin kaynak KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="7c4bf-337">Resource ID of color used to draw the border of thumb button</span></span> | 
| <span data-ttu-id="7c4bf-338">**gx_scroll_button_color**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-338">**gx_scroll_button_color**</span></span>               | <span data-ttu-id="7c4bf-339">Kaydırma çubuğu bitiş düğmelerini dolduracak şekilde kullanılan rengin kaynak KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="7c4bf-339">Resource ID of color used to fill scrollbar end buttons</span></span> |

## <a name="gx_slider_info"></a><span data-ttu-id="7c4bf-340">GX_SLIDER_INFO</span><span class="sxs-lookup"><span data-stu-id="7c4bf-340">GX_SLIDER_INFO</span></span>

### <a name="definition"></a><span data-ttu-id="7c4bf-341">Tanım</span><span class="sxs-lookup"><span data-stu-id="7c4bf-341">Definition</span></span>

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

### <a name="members"></a><span data-ttu-id="7c4bf-342">Üyeler</span><span class="sxs-lookup"><span data-stu-id="7c4bf-342">Members</span></span>

|                                         |                                                        |
| --------------------------------------- | ------------------------------------------------------ |
| <span data-ttu-id="7c4bf-343">**gx_slider_info_min_val**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-343">**gx_slider_info_min_val**</span></span>              | <span data-ttu-id="7c4bf-344">Raporlanan en düşük değer</span><span class="sxs-lookup"><span data-stu-id="7c4bf-344">Minimum reported value</span></span> |
| <span data-ttu-id="7c4bf-345">**gx_slider_info_max_val**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-345">**gx_slider_info_max_val**</span></span>              | <span data-ttu-id="7c4bf-346">Raporlanan en yüksek değer</span><span class="sxs-lookup"><span data-stu-id="7c4bf-346">Maximum reported value</span></span> |
| <span data-ttu-id="7c4bf-347">**gx_slider_info_current_value**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-347">**gx_slider_info_current_value**</span></span>        | <span data-ttu-id="7c4bf-348">Geçerli değer</span><span class="sxs-lookup"><span data-stu-id="7c4bf-348">Current value</span></span> |
| <span data-ttu-id="7c4bf-349">**gx_slider_info_min_travel**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-349">**gx_slider_info_min_travel**</span></span>           | <span data-ttu-id="7c4bf-350">İğne seyahat sınırı</span><span class="sxs-lookup"><span data-stu-id="7c4bf-350">Needle travel limit</span></span> |
| <span data-ttu-id="7c4bf-351">**gx_slider_info_max_travel**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-351">**gx_slider_info_max_travel**</span></span>           | <span data-ttu-id="7c4bf-352">İğne seyahat sınırı</span><span class="sxs-lookup"><span data-stu-id="7c4bf-352">Needle travel limit</span></span> |
| <span data-ttu-id="7c4bf-353">**gx_slider_info_needle_width**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-353">**gx_slider_info_needle_width**</span></span>         | <span data-ttu-id="7c4bf-354">Piksel cinsinden iğne genişliği</span><span class="sxs-lookup"><span data-stu-id="7c4bf-354">Needle width in pixel</span></span> |
| <span data-ttu-id="7c4bf-355">**gx_slider_info_needle_height**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-355">**gx_slider_info_needle_height**</span></span>        | <span data-ttu-id="7c4bf-356">Piksel cinsinden iğne yüksekliği</span><span class="sxs-lookup"><span data-stu-id="7c4bf-356">Needle height in pixel</span></span> |
|<span data-ttu-id="7c4bf-357">**gx_slider_info_needle_inset**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-357">**gx_slider_info_needle_inset**</span></span>          | <span data-ttu-id="7c4bf-358">İğne çiz konumu.</span><span class="sxs-lookup"><span data-stu-id="7c4bf-358">Needle draw position.</span></span> <span data-ttu-id="7c4bf-359">GX_STYLE_SLIDER_VERTICAL ayarlandıysa, iğne çiz başlangıç konumundan sola doğru kaydırıcıyı belirtmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7c4bf-359">If GX_STYLE_SLIDER_VERTICAL is set, used to specify the offset from the needle draw start position to the slider left.</span></span> <span data-ttu-id="7c4bf-360">Else, iğne çizici başlangıç konumundan kaydırıcıyı üste kadar olan sapmayı belirtmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7c4bf-360">Else, used to specify the offset from the needle draw start position to the slider top.</span></span> |
| <span data-ttu-id="7c4bf-361">**gx_slider_info_needle_hotspot_offset**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-361">**gx_slider_info_needle_hotspot_offset**</span></span> | <span data-ttu-id="7c4bf-362">İğne hotpot_offset, iğne çizici başlangıç konumundan kaydırıcı etkin noktaya kadar olan sapmayı belirtmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7c4bf-362">Needle hotpot_offset, used to specify the offset from the needle draw start position to the slider hotspot.</span></span> |

## <a name="gx_sprite_frame"></a><span data-ttu-id="7c4bf-363">GX_SPRITE_FRAME</span><span class="sxs-lookup"><span data-stu-id="7c4bf-363">GX_SPRITE_FRAME</span></span>

### <a name="definition"></a><span data-ttu-id="7c4bf-364">Tanım</span><span class="sxs-lookup"><span data-stu-id="7c4bf-364">Definition</span></span>

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

### <a name="members"></a><span data-ttu-id="7c4bf-365">Üyeler</span><span class="sxs-lookup"><span data-stu-id="7c4bf-365">Members</span></span>

|                                          |                                                       |
| ---------------------------------------- | ----------------------------------------------------- |
| <span data-ttu-id="7c4bf-366">**gx_sprite_frame_pixelmap**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-366">**gx_sprite_frame_pixelmap**</span></span>             | <span data-ttu-id="7c4bf-367">Bu çerçeve için görüntülenecek pixelmap 'in kaynak KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="7c4bf-367">Resource ID of the pixelmap to be displayed for this frame.</span></span> <span data-ttu-id="7c4bf-368">KIMLIK 0 olabilir.</span><span class="sxs-lookup"><span data-stu-id="7c4bf-368">The ID can be 0.</span></span> |
| <span data-ttu-id="7c4bf-369">**gx_sprite_frame_x_offset**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-369">**gx_sprite_frame_x_offset**</span></span>             | <span data-ttu-id="7c4bf-370">Pixelmap 'i göstermek için sprite pencere öğesinin sol tarafındaki boşluğu</span><span class="sxs-lookup"><span data-stu-id="7c4bf-370">Offset from the sprite widget left to display the pixelmap</span></span> |
| <span data-ttu-id="7c4bf-371">**gx_sprite_frame_y_offset**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-371">**gx_sprite_frame_y_offset**</span></span>             | <span data-ttu-id="7c4bf-372">Pixelmap 'i göstermek için en üstteki Sprite pencere öğesi</span><span class="sxs-lookup"><span data-stu-id="7c4bf-372">Offset from the sprite widget top to display the pixelmap</span></span> |
| <span data-ttu-id="7c4bf-373">**gx_sprite_frame_delay**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-373">**gx_sprite_frame_delay**</span></span>                | <span data-ttu-id="7c4bf-374">Sonraki Sprite çerçevesine ilerletmeden önce bu kareyi görüntülendikten sonra, SX Zamanlayıcı işaretleri içinde gecikme değeri.</span><span class="sxs-lookup"><span data-stu-id="7c4bf-374">Delay value, in GUIX timer ticks, after displaying this frame before advancing to the next sprite frame</span></span> |
| <span data-ttu-id="7c4bf-375">**gx_sprite_frame_background_operation**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-375">**gx_sprite_frame_background_operation**</span></span> | <span data-ttu-id="7c4bf-376">Arka planın nasıl silineceğini tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="7c4bf-376">Define how the background should be erased.</span></span> <span data-ttu-id="7c4bf-377">Bu alan için olası değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="7c4bf-377">Possible values for this field are:</span></span><br /><span data-ttu-id="7c4bf-378">GX_SPRITE_BACKGROUND_NO_ACTION: çerçeveler arasında Fill yok</span><span class="sxs-lookup"><span data-stu-id="7c4bf-378">GX_SPRITE_BACKGROUND_NO_ACTION: No fill between frames</span></span><br /><span data-ttu-id="7c4bf-379">GX_SPRITE_BACKGROUND_SOLID_FILL: SPRITE arka planını yeniden Çiz</span><span class="sxs-lookup"><span data-stu-id="7c4bf-379">GX_SPRITE_BACKGROUND_SOLID_FILL: Redraw sprite background</span></span><br /><span data-ttu-id="7c4bf-380">GX_SPRITE_BACKGROUND_RESTORE: önceki pixelmap 'i geri yükle</span><span class="sxs-lookup"><span data-stu-id="7c4bf-380">GX_SPRITE_BACKGROUND_RESTORE: Restore previous pixelmap</span></span> |
| <span data-ttu-id="7c4bf-381">**gx_sprite_frame_alpha**</span><span class="sxs-lookup"><span data-stu-id="7c4bf-381">**gx_sprite_frame_alpha**</span></span>                | <span data-ttu-id="7c4bf-382">Görünen pixelmap 'e eklenecek alfa değeri.</span><span class="sxs-lookup"><span data-stu-id="7c4bf-382">Alpha value to be added to the displayed pixelmap.</span></span> <span data-ttu-id="7c4bf-383">255 değeri, ek bir alfa değeri eklenmesi gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="7c4bf-383">The value 255 specifies that no extra alpha value should be imposed.</span></span> <span data-ttu-id="7c4bf-384">Pixelmap bir alfa kanalı içeriyorsa, bu Alfa kanalı çerçeve Alpha değerine eklenir.</span><span class="sxs-lookup"><span data-stu-id="7c4bf-384">If the pixelmap includes an alpha channel, this alpha channel will be added to the frame alpha value.</span></span> |
