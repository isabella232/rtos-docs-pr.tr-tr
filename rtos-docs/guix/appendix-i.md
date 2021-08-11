---
title: Ek I-Gux bilgi yapıları
description: GUX bilgi yapıları hakkında bilgi edinin.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 8730dbfc49ed51716f32c118a25ebffc907b19a54d98d83ede4155f87fbecb7b
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116784175"
---
# <a name="appendix-i---guix-information-structures"></a>Ek I-Gux bilgi yapıları 

## <a name="gx_bidi_text_info"></a>GX_BIDI_TEXT_INFO 

### <a name="definition"></a>Tanım

```c
typedef struct GX_BIDI_TEXT_INFO_STRUCT
{
    GX_STRING gx_bidi_text_info_text;
    GX_FONT  *gx_bidi_text_info_font;
    GX_VALUE  gx_bidi_text_info_display_width;
} GX_BIDI_TEXT_INFO;
```
| Üyeler | Description |
| ---------------------------------- | ---------------------------------------------------------- |
| **gx_bidi_text_info_text**               | Yeniden sıralama için metin |
| **gx_bidi_text_info_font**               | Metni göstermek için kullanılan yazı tipi, satır sonu gerekmiyorsa GX_NULL olarak ayarlayın |
| **gx_bidi_text_info_display_width**      | Görüntüleme için kullanılabilir genişlik, satır sonu gerekmiyorsa-1 olarak ayarlayın |

## <a name="gx_bidi_resolved_text_info"></a>GX_BIDI_RESOLVED_TEXT_INFO 

### <a name="definition"></a>Tanım

```c
typedef struct GX_BIDI_RESOLVED_TEXT_INFO_STRUCT
{
    GX_STRING                                *gx_bidi_resolved_text_info_text;
    UINT                                      gx_bidi_resolved_text_info_total_lines;
    struct GX_BIDI_RESOLVED_TEXT_INFO_STRUCT *gx_bidi_resolved_text_info_next;
} GX_BIDI_RESOLVED_TEXT_INFO;
```

| Üyeler | Description |
| ---------------------------------- | ---------------------------------------------------------- |
| **gx_bidi_resolved_text_info_text**             | Yeniden sıralanan bidi metni dizisine yönelik işaretçi |
| **gx_bidi_resolved_text_info_total_lines**      | Tek bir paragraf için çözülen çift yönlü metnin toplam satırları |
| **gx_bidi_resolved_text_info_next**             | Sonraki paragraf için çift yönlü metin bilgileri çözüldü |

## <a name="gx_circular_gauge_info"></a>GX_CIRCULAR_GAUGE_INFO

### <a name="definition"></a>Tanım

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

| Üyeler | Description |
| ------------------------------------------------ | -------------------------------------------- |
| **gx_circular_gauge_info_animation_steps**       | Geçerli iğne açısına göre yeni, atanan iğne açısına geçiş yaparken, iğne 'nin hareket ettirme toplam adım sayısı |
| **gx_circular_gauge_info_animation_delay**       | Animasyon adımları arasındaki gecikmede Gux saat Ticks sayısı |
| **gx_circular_gauge_info_needle_xpos**           | Ölçer pencere öğesinin solundaki uzaklık, ölçer iğne 'nin ortasına kadar olan mesafe |
| **gx_circular_gauge_info_needle_ypos**           | Ölçer pencere öğesinin en üstünden ölçer iğne 'nin ortasına olan uzaklık |
| **gx_circular_gauge_info_needle_xcor**           | İğne resminin solundaki mesafe, ölçer iğne 'nin ortasına kadar |
| **gx_circular_gauge_info_needle_ycor**           | İğne resminin en üstünden ölçer iğne 'nin ortasına kadar olan mesafe |
| **gx_circular_gauge_info_needle_pixelmap**       | Ölçer iğne çizmek için kullanılacak olan pixelmap 'in kaynak KIMLIĞI. Bu görüntü ölçer pencere öğesinin gerektiği şekilde döndürüldüğü şekilde döndürülecektir ve ölçer iğne herhangi bir konumda görüntülenir |

Aşağıdaki diyagramda XPos, YPos ve xcor ycor koordinatları gösterilmektedir:

![Iğne Y ve X koordinatları diyagramı](./media/guix/image8.png)

## <a name="gx_line_chart_info"></a>GX_LINE_CHART_INFO

### <a name="definition"></a>Tanım

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

| Üyeler | Description |
| ---------------------------------- | ---------------------------------------------------------- |
| **gx_line_chart_min_val**          | Ölçeklendirmeyi hesaplamak için kullanılan minimum veri değeri
| **gx_line_chart_max_val**          | Ölçeklendirmeyi hesaplamak için kullanılan maksimum veri değeri |
| **gx_line_chart_data**             | Tamsayı değerleri dizisine yönelik işaretçi. Bunlar çizgi grafik pencere öğesi tarafından çizilen tamsayı değerlerdir |
| **gx_line_ <side> _margin**          | Grafik penceresi dış alanının gerçek grafik işleme alanına göre sınırı. Grafik ekseni ve veri satırı her zaman bu iç sınır içinde çizilir. Bu, uygulamanın grafik penceresi içinde, ancak char grafikalanı dışında Etiketler ve diğer bilgiler çizmesini sağlar. |
| **gx_line_chart_max_data_count**   | Mevcut olabilecek veri değerlerinin sayısı. Bu parametre, veri noktalarını çizmek için x ekseninin ölçeğini veya aralığını hesaplamak için kullanılır. |
| **gx_line_active_data_count**      | Veri dizisinde gerçekten mevcut olan veri değerlerinin sayısı. Çizgi grafik, en fazla 100 değer çizmek için ölçeklendirilebilir (örneğin), ancak belirli bir güncelleştirmede daha az sayıda veri değeri bulunabilir. |
| **gx_line_axis_line_width**        | Yatay ve dikey ekseni çizmek için kullanılan çizginin genişliği |
| **gx_line_data_line_width**        | Çizilen veri çizgisinin genişliği |
| **gx_line_chart_axis_color**       | Eksen çizgilerini çizmek için kullanılan rengin kaynak KIMLIĞI |
| **gx_line_chart_line_color**       | Grafik veri çizgisini çizmek için kullanılan rengin kaynak KIMLIĞI |

## <a name="gx_mouse_cursor_info"></a>GX_MOUSE_CURSOR_INFO 

### <a name="definition"></a>Tanım

```c
typedef struct GX_MOUSE_CURSOR_INFO_STRUCT
{
    GX_RESOURCE_ID             gx_mouse_cursor_image_id;
    GX_VALUE                   gx_mouse_cursor_hotspot_x;
    GX_VALUE                   gx_mouse_cursor_hotspot_y;
} GX_MOUSE_CURSOR_INFO;
```

| Üyeler | Description |
| ---------------------------------- | ---------------------------------------------------------- |
| **gx_mouse_cursor_image_id**       | Fare resminin kaynak KIMLIĞI |
| **gx_mouse_cursor_hotspot_x**      | Fare resminin solundaki fare resmi etkin noktası arasındaki fark |
| **gx_mouse_cursor_hotspot_y**      | Fare resminin en üstünden fare resmi etkin noktaya kadar olan fark |

## <a name="gx_pen_configuration"></a>GX_PEN_CONFIGURATION 

### <a name="definition"></a>Tanım

```c
typedef struct GX_PEN_CONFIGURATION_STRUCT
{
    GX_FIXED_VAL     gx_pen_configuration_min_drag_dist;
    UINT             gx_pen_configuration_max_pen_speed_ticks;
}GX_PEN_CONFIGURATION;
```

| Üyeler | Description |
| -------------------------------------------- | ------------------------------------------------ |
| **gx_pen_configuration_min_drag_dist**       | Bir hareket olayı tetiklemek için Gux süreölçeri başına en az sürükleme uzaklığı. Sabit bir nokta veri türü değeri oluşturmak için GX_FIXED_VAL_MAKE çağırın |
| **gx_pen_configuration_max_pen_speed_ticks** | Bir hareket olayı tetiklemek için Gux süreölçer işaretleri cinsinden maksimum sürükleme hızı | 

## <a name="gx_pixelmap_slider_info"></a>GX_PIXELMAP_SLIDER_INFO 

### <a name="definition"></a>Tanım

```c
typedef struct GX_PIXELMAP_SLIDER_INFO_STRUCT
{
    GX_RESOURCE_ID gx_pixelmap_slider_info_lower_background_pixelmap;
    GX_RESOURCE_ID gx_pixelmap_slider_info_upper_background_pixelmap;
    GX_RESOURCE_ID gx_pixelmap_slider_info_needle_pixelmap;
} GX_PIXELMAP_SLIDER_INFO;
```

| Üyeler | Description |
| ----------------------------------------------------- | ---------------------------------------- |
| **gx_pixelmap_slider_info_lower_background_pixelmap** | İğne 'dan önce arka planı doldurmak için pixelmap 'in kaynak KIMLIĞI. Üst arka plan pixelmap ayarlanmamışsa, arka planı yalnızca iğne 'den önce ve sonra doldurmak için kullanılır |
| **gx_pixelmap_slider_info_upper_background_pixelmap** | İğne 'tan sonra arka planı doldurmak için pixelmap 'in kaynak KIMLIĞI |
| **gx_pixelmap_slider_info_needle_pixelmap**           | Iğne piksel haritasının kaynak kimliği |

## <a name="gx_progress_bar_info"></a>GX_PROGRESS_BAR_INFO 

### <a name="definition"></a>**Tanım**

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

| Üyeler | Description |
| -------------------------------------------- | ------------------------------------------------ |
| **gx_progress_bar_info_min_val**             | Bildirilen minimum değer |
| **gx_progress_bar_info_max_val**             | Bildirilen maksimum değer |
| **gx_progress_bar_info_current_val**         | Geçerli değer |
| **gx_progress_bar_info_font_id**             | İlerleme çubuğu pencere öğesi içinde isteğe bağlı metin değerini çizmek için kullanılan yazı tipinin kaynak kimliği      |
| **gx_progress_bar_normal_text_color**        | Normal durumdaki metin renginin kaynak kimliği, ilerleme çubuğu pencere öğesi içinde isteğe bağlı metin çizimini tanımlamak için kullanılır |
| **gx_progress_bar_selected_text_color**      | Pencere öğesi odağında metin renginin kaynak kimliği, ilerleme çubuğu pencere öğesi içinde isteğe bağlı metin çizimini tanımlamak için kullanılır |
| **gx_progress_bar_disabled_text_color**      | Çalışma alanı etkin değilken metin renginin GX_STYLE_ENABLED kimliği, ilerleme çubuğu pencere öğesi içinde isteğe bağlı metin çizimini tanımlamak için kullanılır |
| **gx_progress_bar_fill_pixelmap**            | Arka plan doldurma için piksel haritasının kaynak kimliği|

## <a name="gx_radial_progress_bar_info"></a>GX_RADIAL_PROGRESS_BAR_INFO

### <a name="definition"></a>Tanım

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

| Üyeler | Description |
| ------------------------------------------------- | -------------------------------------------- |
| **gx_radial_progress_bar_info_xcenter**           | x koordinatı içinde pencere öğesi konumu |
| **gx_radial_progress_bar_info_ycenter**           | y koordinatı içinde pencere öğesi konumu  |
| **gx_radial_progress_bar_info_radius**            | İlerleme dairesinin yarıçapı |
| **gx_radial_progress_bar_info_current_val**       | [-360, 360] aralığıyla sınırlı olan geçerli değer, yer işareti konumu ile üst yay bitiş noktası arasındaki angular deltayı gösterir. Negatif değer, yaynın sabit noktası konumundan başlayarak saat yönünde çizilir. Pozitif değer, sabit noktası konumundan başlayarak yaynın saat yönünün tersine doğru çizilir. Uygulama, ilerleme çubuğu pencere öğesine angular değer atamak için gösterilen gerçek sözcük değerini ölçeklendirmeli |
| **gx_radial_progress_bar_anchor_val**             | Üst ilerleme yayının başlangıç açısı. Değer, sağa işaret eden 0 derece ve düz yukarı konumu gösteren 90 derece ile tamsayı derecesi olarak tanımlanır. |
| **gx_radial_progress_bar_font_id**                | İlerleme çubuğu pencere öğesi içinde isteğe bağlı metin değerini çizmek için kullanılan yazı tipinin kaynak kimliği |
| **gx_radial_progress_bar_normal_text_color**      | Normal durumdaki metin renginin kaynak kimliği, ilerleme çubuğu pencere öğesi içinde isteğe bağlı metin çizimini tanımlamak için kullanılır |
| **gx_radial_progress_bar_selected_text_color**    |Pencere öğesi odağında metin renginin kaynak kimliği, ilerleme çubuğu pencere öğesi içinde isteğe bağlı metin çizimini tanımlamak için kullanılır |
| **gx_radial_progress_bar_disabled_text_color**    | Çalışma alanı etkin değilken metin renginin GX_STYLE_ENABLED kimliği, ilerleme çubuğu pencere öğesi içinde isteğe bağlı metin çizimini tanımlamak için kullanılır |
| **gx_radial_progress_bar_normal_brush_width**     | Daha düşük ilerleme dairesinin genişliği |
| **gx_radial_progress_bar_selected_brush_width**   | Üst ilerleme yayının genişliği, üst yay alt daireyle aynı şekilde daha dar veya daha geniş olabilir |
| **gx_radial_progress_bar_normal_brush_color**     | Daha düşük ilerleme dairesini doldurmak için rengin kaynak kimliği |
| **gx_radial_progress_bar_selected_brush_color**   | Üst ilerleme yayının doldurulacak rengin kaynak kimliği |

## <a name="gx_radial_slider_info"></a>GX_RADIAL_SLIDER_INFO 

### <a name="definition"></a>Tanım

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

| Üyeler | Description |
| --------------------------------------------- | ------------------------------------------------ |
**gx_radial_slider_info_xcenter**               | Kaydırıcı pencere öğesinden kaydırıcı iğnenin döndürme merkezine uzaklık |
| **gx_radial_slider_info_ycenter**             | Kaydırıcı pencere öğesinden en üst kısmından kaydırıcı iğnenin döndürme merkezine uzaklık |
| **gx_radial_slider_info_radius**              | Radyal kaydırıcı dairenin yarıçapı |
| **gx_radial_slider_info_track_width**         | Radyal kaydırıcı izlemenin genişliği |
| **gx_radial_slider_info_current_angle**       | Geçerli kaydırıcı açısı |
| **gx_radial_slider_info_min_angle**           | En düşük kaydırıcı açısı |
| **gx_radial_slider_info_max_angle**           | Maksimum kaydırıcı açısı |
| **gx_radial_slider_info_angle_list**          | Açılı değer listesi, sabit noktası açılarını tanımlar; ayarlanırsa kaydırıcı açısı tanımlı sabit noktası açılarından yalnızca biri olabilir |
| **gx_radial_slider_info_list_count**          | Yer noktası açılarının sayısı |
| **gx_radial_slider_info_background_pixelmap** | Arka plan piksel haritasının kaynak kimliği |
| **gx_radial_slider_info_needle_pixelmap**     | Iğne piksel haritasının kaynak kimliği |

## <a name="gx_rectangle"></a>GX_RECTANGLE

### <a name="definition"></a>Tanım

```c
typedef struct GX_RECTANGLE_STRUCT
{
    GX_VALUE gx_rectangle_left;
    GX_VALUE gx_rectangle_top;
    GX_VALUE gx_rectangle_right;
    GX_VALUE gx_rectangle_bottom;
} GX_RECTANGLE;
```

| Üyeler | Description |
| -------------------------------- | ------------------------|
| **gx_rectangle_left**            | Dikdörtgenin sol   |  
| **gx_rectangle_top**             | Dikdörtgenin üst kısmında    | 
| **gx_rectangle_right**           | Dikdörtgenin sağ  |
| **gx_rectangle_bottom**          | Dikdörtgenin alt kısmında |

## <a name="gx_rich_text_fonts"></a>GX_RICH_TEXT_FONTS 

### <a name="definition"></a>Tanım

```c
typedef struct GX_RICH_TEXT_FONTS_STRUCT
{
    GX_RESOURCE_ID             gx_rich_text_fonts_normal_id;
    GX_RESOURCE_ID             gx_rich_text_fonts_bold_id;
    GX_RESOURCE_ID             gx_rich_text_fonts_italic_id;
    GX_RESOURCE_ID             gx_rich_text_fonts_bold_italic_id;
} GX_RICH_TEXT_FONTS;
```

| Üyeler | Description |
| ---------------------------------- | ---------------------------------------------------------- |
| **gx_rich_text_fonts_normal_id**   | Normal metin yazı tipi kaynak kimliği |
| **gx_rich_text_fonts_bold_id**     | Kalın metin yazı tipi kaynak kimliği |
| **gx_rich_text_fonts_italic_id**   | İtalik metin yazı tipinin kaynak KIMLIĞI |
| **gx_rich_text_fonts_bold_italic_id** | Kalın italik metin yazı tipinin kaynak KIMLIĞI |

## <a name="gx_scroll_info"></a>GX_SCROLL_INFO 
### <a name="definition"></a>**Tanım**

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

| Üyeler | Description |
| ----------------------- | ----------------------------- |
| **gx_scroll_value**     | Geçerli kaydırma konumu       |
| **gx_scroll_minimum**   | Raporlanan en düşük konum     |
| **gx_scroll_maximum**   | Raporlanan en yüksek konum     |
| **gx_scroll_visible**   | Üst pencere görünür aralığı   |
| **gx_scroll_increment** | Kaydırma çubuğu en küçük delta değeri |

## <a name="gx_scrollbar_appearance"></a>GX_SCROLLBAR_APPEARANCE 

### <a name="definition"></a>Tanım

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

| Üyeler | Description |
| ---------------------------------------- | ----------------------------------------------------- |
| **gx_scroll_width**                      | ScrollBar pencere öğesinin piksel cinsinden genişliği |
| **gx_scroll_thumb_width**                | Kaydırma çubuğu üzerindeki slaytları piksel cinsinden gösteren Thumb düğmesinin genişliği. Bu değer genellikle toplam kaydırma çubuğu genişliğinden az sayıda piksel daha küçüktür |
| **gx_scroll_thumb_travel_min**           | Kaydırma çubuğunun sonundan en küçük parmak izi düğmesi seyahat noktası arasındaki fark. Bu sınır, parmak izinin kaydırma çubuğunun çok sonuna kadar hareket etmelerini engellemek için kullanılabilir |
| **gx_scroll_thumb_travel_max**           | Kaydırma çubuğunun sonundan en fazla kaydırma düğmesi seyahat noktası arasındaki fark. Bu sınır, parmak izinin kaydırma çubuğunun çok sonuna kadar hareket etmelerini engellemek için kullanılabilir |
| **gx_scroll_thumb_border_style**         | Thumb düğmesinin kenarlık stilleri |
| **gx_scroll_fill_pixelmap**              | İsteğe bağlı pixelmap KIMLIĞI. Bu pixelmap KIMLIĞI sıfır değilse, ScrollBar ScrollBar arka planını çizmek için bu pixelmap 'i kullanır |
| **gx_scroll_thumb_pixelmap**             | İsteğe bağlı pixelmap KIMLIĞI. Bu pixelmap KIMLIĞI sıfır değilse, kaydırma çubuğu parmak izi düğmesi kendisini çizmek için bu pixelmap 'i kullanır |
| **gx_scroll_up_pixelmap**                | İsteğe bağlı pixelmap KIMLIĞI. Bu pixelmap KIMLIĞI sıfır değilse, kaydırma çubuğu bu pixelmap KIMLIĞINI kullanarak kaydırma çubuğunu sola/yukarı ucu düğme çiz |
| **gx_scroll_down_pixelmap**              | İsteğe bağlı pixelmap KIMLIĞI. Bu pixelmap KIMLIĞI sıfır değilse, kaydırma çubuğu bu pixelmap KIMLIĞINI kullanarak kaydırma çubuğunu sağ/aşağı uç düğmesini çizin |
| **gx_scroll_thumb_color**                | Thumb düğmesini doldurmanız için kullanılan rengin kaynak KIMLIĞI |
| **gx_scroll_thumb_border_color**         | Thumb düğmesinin kenarlığını çizmek için kullanılan rengin kaynak KIMLIĞI | 
| **gx_scroll_button_color**               | Kaydırma çubuğu bitiş düğmelerini dolduracak şekilde kullanılan rengin kaynak KIMLIĞI |

## <a name="gx_slider_info"></a>GX_SLIDER_INFO

### <a name="definition"></a>Tanım

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

| Üyeler | Description |
| --------------------------------------- | ------------------------------------------------------ |
| **gx_slider_info_min_val**              | Raporlanan en düşük değer |
| **gx_slider_info_max_val**              | Raporlanan en yüksek değer |
| **gx_slider_info_current_value**        | Geçerli değer |
| **gx_slider_info_min_travel**           | İğne seyahat sınırı |
| **gx_slider_info_max_travel**           | İğne seyahat sınırı |
| **gx_slider_info_needle_width**         | Piksel cinsinden iğne genişliği |
| **gx_slider_info_needle_height**        | Piksel cinsinden iğne yüksekliği |
|**gx_slider_info_needle_inset**          | İğne çiz konumu. GX_STYLE_SLIDER_VERTICAL ayarlandıysa, iğne çiz başlangıç konumundan sola doğru kaydırıcıyı belirtmek için kullanılır. Else, iğne çizici başlangıç konumundan kaydırıcıyı üste kadar olan sapmayı belirtmek için kullanılır. |
| **gx_slider_info_needle_hotspot_offset** | İğne hotpot_offset, iğne çizici başlangıç konumundan kaydırıcı etkin noktaya kadar olan sapmayı belirtmek için kullanılır. |

## <a name="gx_sprite_frame"></a>GX_SPRITE_FRAME

### <a name="definition"></a>Tanım

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

| Üyeler | Description |
| ---------------------------------------- | ----------------------------------------------------- |
| **gx_sprite_frame_pixelmap**             | Bu çerçeve için görüntülenecek pixelmap 'in kaynak KIMLIĞI. KIMLIK 0 olabilir. |
| **gx_sprite_frame_x_offset**             | Pixelmap 'i göstermek için sprite pencere öğesinin sol tarafındaki boşluğu |
| **gx_sprite_frame_y_offset**             | Pixelmap 'i göstermek için en üstteki Sprite pencere öğesi |
| **gx_sprite_frame_delay**                | Sonraki Sprite çerçevesine ilerletmeden önce bu kareyi görüntülendikten sonra, SX Zamanlayıcı işaretleri içinde gecikme değeri. |
| **gx_sprite_frame_background_operation** | Arka planın nasıl silineceğini tanımlayın. Bu alan için olası değerler şunlardır:<br />GX_SPRITE_BACKGROUND_NO_ACTION: çerçeveler arasında Fill yok<br />GX_SPRITE_BACKGROUND_SOLID_FILL: SPRITE arka planını yeniden Çiz<br />GX_SPRITE_BACKGROUND_RESTORE: önceki pixelmap 'i geri yükle |
| **gx_sprite_frame_alpha**                | Görünen pixelmap 'e eklenecek alfa değeri. 255 değeri, ek bir alfa değeri eklenmesi gerektiğini belirtir. Pixelmap bir alfa kanalı içeriyorsa, bu Alfa kanalı çerçeve Alpha değerine eklenir. |
