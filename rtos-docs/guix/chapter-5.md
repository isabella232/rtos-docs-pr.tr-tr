---
title: Bölüm 5-Gux görüntüleme sürücüleri
description: GUX görüntü sürücüleri, soyut çizim tuvali ile fiziksel görüntü donanımı arasındaki yazılım arabirimini tanımlar.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 7c8f509aee1892693c22f8cfba3207158de4a1e9
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104827173"
---
# <a name="chapter-5---guix-display-drivers"></a>Bölüm 5-Gux görüntüleme sürücüleri

GUX görüntü sürücüleri, soyut çizim tuvali ile fiziksel görüntü donanımı arasındaki yazılım arabirimini tanımlar. GUX görüntü sürücüsü, tuval belleğindeki piksel renk bilgilerini değiştiren ve tuval belleğini çift arabellekli sistemlerdeki fiziksel görüntü çerçeve arabelleğine aktarabilen en düşük düzey çizim işlevlerini uygular.

GUX görüntü sürücüleri, fiziksel görüntüleme parametrelerini ve alt düzey sürücü işlevlerine bir işlev işaretçileri kümesini içeren bir yapı tarafından tanımlanır. Bu dolaylı işlev işaretçilerini kullanarak, soyut tuval ve pencere öğesi çizim işlevleri, donanım ayrıntılarından tamamen bağımsız yapılır.

GUX desteklenen her renk derinliği ve renk biçimi için eksiksiz, tam işlevli, varsayılan bir çizim işlevleri kümesi sağlar. Belirli bir donanım hızlandırma özelliği veya donanıma özgü bazı hususlar olmadan bir görüntüleme sürücüsü uygularken, bu varsayılan çizim işlevleri genellikle son sürücü uygulaması için yeterlidir. Bu en basit sürücü için, normalde sürücü yazılımında uygulanması gereken tek işlev, donanım cihazını yapılandırmak için bir işlevdir. Bu çoğunlukla, LCD görüntüleme saati, görüntüleme boyutları vb. tanımlamak için çeşitli donanım kayıtları başlatmayı içerir. Diğer tüm işlevler için, sürücü uygulaması yalnızca istenen renk derinliği ve biçimi için GX_DISPLAY işlevi işaretçilerini varsayılan işlev uygulamalarına başlatacak.

Özel bir görüntüleme sürücüsü uygularken, en iyi uygulama, öncelikle, desteklemek istediğiniz renk derinliğine yönelik varsayılan yazılım uygulamasıyla görüntü sürücüsü çizimi işlev işaretçilerinizi başlatmasıdır, ardından özel işlev uygulamalarınızı (varsa) çağırmak istediğiniz yerde bu işlev işaretçilerini değiştirir. Buna yardımcı olması için desteklenen her renk derinliği ve biçimi için varsayılan bir kurulum işlevi mevcuttur. Örneğin, 16 bit 5:6:5 biçimli bir RGB görüntü sürücüsü yazıyorsanız, özel sürücünüzün normal olarak bu renk derinliği için genel Kurulum yordamını çağırması gerekir:

UINT my_custom_565_display_driver (GX_DISPLAY * görüntüle)

```c
{
      
      // perform standard function pointer setup
      
      _gx_display_driver_565rgb_setup(display, GX_NULL,
      
             my_buffertoggle);

}
```

Yukarıdaki my_buffer_toggle parametresi, görüntü sürücü arabelleği geçiş işlevinizin bir işaretçisidir (sürücünüz tek arabelleğe alınıyorsa ve doğrudan donanım çerçeve arabelleğine çizerek GX_NULL olabilir).

Özel bir görüntüleme sürücüsü yazıyorsanız, bir iç kullanım üst bilgisi dosyası olan, uygulama düzeyinde yazılım için kullanılamayan gx_display. h üstbilgi dosyasını özel sürücü kaynağınıza eklemeniz gerekir.

GUX görüntüleme düzeyi çizim işlevleri bir **GX_DRAW_CONTEXT** yapısına bir işaretçi girişi olarak alır. **GX_DRAW_CONTEXT** yapısı, kullanılan fırça ve renklerle birlikte geçerli çizim işleminin kırpma koordinatlarını tanımlar. Her çizim işlevi, işlev gereksinimlerine özel giriş ek parametreleri olarak alır.

**GX_DISPLAY** sürücü giriş noktasının imzası şöyle tanımlanır

```c
UINT <device>_graphics_driver_<format>(GX_DISPLAY *diplay)
```

Bu işlevin adı kendi uygulayıcısı 'na tamamen sahip olsa da, GUıDX ile birlikte sunulan sürücülerin kuralı, <device> alan ve yukarıdaki alana ait renk biçiminde donanıma özgü bir cihaz adı kullanmaktır <format> .

Bu işlev, giriş olarak girilen **GX_DISPLAY** yapısını başlatmalıdır ve gerekli tüm donanım ayarlarını gerçekleştirmelidir. **GX_DISPLAY** yapısı aşağıdaki alanları içerir.

| &nbsp; |
| --- | --- |
| ULONG gx_display_id <br/> Bu, belirli bir sürücünün birden fazla örneğinin oluşturulduğu durumlarda uygulama tarafından kullanılmak üzere bir alandır. |
| CHAR * gx_display_name <br/> Sürücüyü tanımlamak için kullanılan isteğe bağlı bir ad. |
| GX_DISPLAY * gx_display_created_next <br/> Bu alan, GUIX tarafından başlatılır ve tüm GX_DISPLAY örneklerinin bir listesini oluşturmak ve korumak için kullanılır. |
| GX_DISPLAY * gx_display_created_previous <br/> Bu alan, GUIX tarafından başlatılır ve tüm GX_DISPLAY örneklerinin bir listesini oluşturmak ve korumak için kullanılır. |
| GX_VALUE gx_display_color_format <br/> Bu alan, bu sürücü tarafından desteklenen grafik veri biçimini yansıtmalıdır. Renk biçimi türleri gx_api. h üstbilgi dosyasında tanımlanmıştır. |
| GX_VALUE gx_display_width <br/> Bu alan, fiziksel görüntüleme genişliğini piksel cinsinden tutacak şekilde başlatılmalıdır. |
| GX_VALUE gx_display_height <br/> Bu alan, fiziksel görüntüleme yüksekliğini piksel cinsinden tutacak şekilde başlatılmalıdır. |
| GX_COLOR * gx_display_color_table <br/> Bu, renk kimliği değerlerini renk biçimine özgü renk değerlerine dönüştürmek için kullanılan bir tabloya yönelik bir işaretçidir. |
| GX_PIXELMAP * gx_display_pixelmap_table <br/> Bu, bu görüntü için etkin pixelmap tablosuna yönelik bir işaretçidir. |
| GX_FONT * gx_display_font_table <br/> Bu, bu görüntü için etkin yazı tipi tablosunun bir işaretçisidir. |
| GX_COLOR * gx_display_palette <br/> Palet modu sürücüleri için bu, etkin renk paleti için bir işaretçidir. Renk paleti kullanmayan sürücüler için bu işaretçi GX_NULL. |
| UINT gx_display_pixelmap_table_size <br/> Etkin pixelmap tablosundaki girdi sayısı. |
| UINT gx_display_font_table_size <br/> Etkin yazı tipi tablosundaki girdi sayısı. |
| UINT gx_display_palette_size <br/> Renk paletindeki giriş sayısı (varsa). |
| ULONG gx_display_handle <br/> Görünümü belirten benzersiz bir tanımlayıcı veya *tanıtıcı*.
| UINT gx_display_driver_ready <br/> Bu alan, sürücü işleme için hazırsanız Gux 'e işaret etmek için kullanılır. Bazı durumlarda, sürücü birkaç başlatma ve yapılandırma düzeyi gerektirebilir ve bu süre, Gux 'in sürücüyü kullanmayı denememelidir. Sürücü, çizim isteklerine hizmet etmeye hazırsanız, bu bayrak 1 olarak ayarlanmalıdır. |
| VOID * gx_display_driver_data <br/> Bu alan, sürücü uygulamasının kullanımına yöneliktir. Sürücünün GX_DISPLAY yapıda bulunmayan ek bilgiler oluşturması ve başvurması gerekiyorsa, sürücü için alan ayırmayı ve bu yapı alanını kullanarak bu ek verileri işaret etmesi gerekir. Sürücüye özgü ek verilere bir örnek, sürücü tarafından kullanılan DMA kanalını veya görüntüleme çerçevesi arabelleğinin bağlı olduğu SPI kanalını içerebilir. |
| VOID (* gx_display_driver_drawing_initiate) (struct GX_DISPLAY_STRUCT * Display, struct GX_CANVAS_STRUCT * Canvas) <br/> Bu, NULL değilse gx_canvas_drawing_initiate işlevi tarafından çağrıldığında bir işlev işaretçisidir. Grafik hızlandırıcısı veya donanım grafik görüntüleme listesi kullanan ekran sürücüleri için, bu işlev yeni bir görüntüleme listesi başlatmak üzere kullanılabilir. Bu işlev işaretçisi NULL olabilir. |
| VOID (* gx_display_driver_palette_set) (struct GX_DISPLAY_STRUCT * Display, GX_COLOR * palette, ıNT Count) <br/> Bu, bir renk paleti yüklemeye yönelik bir işleve yönelik bir işaretçidir. Bu işlev, sürücü Palette (renk arama tablosu veya CLUT olarak da bilinir) modunda işlem yaptığı müddetçe boştur. |
| VOID (* gx_display_driver_simple_line_draw) (GX_DRAW_CONTECT * bağlam, INT x1, INTy1, INT x2, INT Y2) <br/> Bu, genel çizgi çizimi uygulamak için bir işlev işaretçisidir, hiçbir kenar yumuşatma yoktur. Bu işlevin varsayılan uygulamaları desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (* gx_display_driver_simple_wide_line_draw) (GX_DRAW_CONTECT * bağlam, INT x1, INTy1, INT x2, INT Y2) <br/> Bu, genel geniş çizgi çizimi uygulamak için bir işlev işaretçisidir, hiçbir kenar yumuşatma yoktur. Bu işlevin varsayılan uygulamaları desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (* gx_display_driver_anti_aliased_line_draw) (GX_DRAW_CONTECT * bağlam, INT x1, INTy1, INT x2, INT Y2) <br/> Bu, genel ve daha fazla diğer çizgi çizimi uygulayan bir işleve yönelik bir işaretçidir. Bu işlevin varsayılan uygulamaları desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (* gx_display_driver_anti_aliased_wide_line_draw) (GX_DRAW_CONTECT * bağlam, INT x1, INTy1, INT x2, INT Y2) <br/> Bu, genel ve daha fazla sayıda geniş çizgi çizimi uygulayan bir işleve yönelik bir işaretçidir. Bu işlevin varsayılan uygulamaları desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (* gx_display_driver_horizonal_line_draw) (GX_DRAW_CONTECT * bağlam, INT x1, INT x2, INT y) <br/> Bu, yatay çizgi çiziminin özel durumunu uygulamak için bir işleve yönelik bir işaretçidir. Bu işlevin varsayılan uygulamaları desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (* gx_display_driver_horizonal_pixelmap_line_draw) (GX_DRAW_CONTECT * bağlam, INT x1, INT x2, INT y, GX_PIXELMAP * Map) <br/> Bu, tek bir pixelmap satırı çizimini uygulamak için bir işlev işaretçisidir. Bu işlev, model doldurma şekilleri için dahili olarak kullanılır. Bu işlevin varsayılan uygulamaları desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (* gx_display_driver_vertical_line_draw) (GX_DRAW_CONTECT * bağlam, INT Y1, INT Y2, ıNT x) <br/> Bu, yatay çizgi çiziminin özel durumunu uygulamak için bir işleve yönelik bir işaretçidir. Bu işlevin varsayılan uygulamaları desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (* gx_display_driver_horizonal_pattern_line_draw) (GX_DRAW_CONTECT * bağlam, INT x1, INT x2, INT y) <br/> Bu, yatay kalıp çizgisi çizimi uygulayan bir işleve yönelik bir işaretçidir. Bu işlevin varsayılan uygulamaları desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (* gx_display_driver_vertical_pattern_line_draw) (GX_DRAW_CONTECT * bağlam, INT Y1, INT Y2, ıNT x) <br/> Bu, dikey kalıp çizgisi çizimi uygulayan bir işleve yönelik bir işaretçidir. Bu işlevin varsayılan uygulamaları desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (* gx_display_driver_canvas_copy) (struct GX_CANVAS_STRUCT * Source, struct GX_CANVAS_STRUCT * dest) <br/> Bu, tuval verilerini bir tuvalden diğerine kopyalamak için bir işlev işaretçisidir. Kaynak tuvali geçersiz dikdörtgen, kopyalama alanını tanımlamak için kullanılır. Bu işlevin varsayılan uygulamaları desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (* gx_display_driver_canvas_blend) (struct GX_CANVAS_STRUCT * Source, struct GX_CANVAS_STRUCT * dest) <br/> Bu, hedef tuvaldeki mevcut verilerle birlikte kaynak tuvalinden, tuval verilerini Alpha Blend için bir işleve yönelik bir işaretçidir. Kaynak tuvali geçersiz dikdörtgen Blend alanını tanımlamak için kullanılır. Bu işlevin varsayılan uygulamaları desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (* gx_display_driver_pixelmap_blend) (GX_DRAW_CONTEXT * bağlam, INT XPos, INT YPos, GX_PIXELMAP * PMP, GX_UBYTE Alpha) <br/> Bu, çizim bağlamı tarafından tanımlanan arka plan tuvalindeki bir pixelmap 'i Blend işlevinin bir işaretçisidir. Sağlanan alfa değeri, pixelmap verilerinde bulunan bir alfa kanalına ek olarak olabilir. Bu işlevin varsayılan uygulamaları desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (* gx_display_driver_pixelmap_draw) (GX_DRAW_CONTEXT * bağlam, INT XPos, INT YPos, GX_PIXELMAP * PMP) <br/> Bu, çizim bağlamı tarafından tanımlanan tuvale bir pixelmap çizme işlevine yönelik bir işaretçidir. Bu işlevin varsayılan uygulamaları desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (* gx_display_driver_jpeg_draw) (GX_DRAW_CONTEXT * bağlam, INT XPos, INT YPos, GX_PIXELMAP * PMP) <br/> Bu, bir jpg görüntüsünün kodunu çözmek ve doğrudan tuvale işlemek için bir işleve yönelik bir işaretçidir. Bu işlev yalnızca GX_SOFTWARE_DECODER_SUPPORT tanımlanmışsa sağlanır. Bu işlev işaretçisi NULL olmalıdır. Bu işlevin varsayılan uygulamaları desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (* gx_display_driver_png_draw) (GX_DRAW_CONTEXT * bağlam, INT XPos, INT YPos, GX_PIXELMAP * PMP) <br/> Bu, bir PNG görüntüsünün kodunu çözmek ve doğrudan tuvale işlemek için bir işleve yönelik bir işaretçidir. Bu işlev yalnızca GX_SOFTWARE_DECODER_SUPPORT tanımlanmışsa sağlanır. Bu işlev işaretçisi NULL olmalıdır. Bu işlevin varsayılan uygulamaları desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (* gx_display_driver_pixelmap_rotate) (GX_DRAW_CONTEXT * bağlam, INT XPos, INT YPos, GX_PIXELMAP * PMP INT açılı, INT rot_cx, INT rot_cy) <br/> Bu, bir Pikselleştirme döndürmek ve sonucu doğrudan tuvale işlemek için bir işleve yönelik bir işaretçidir. Bu işlev, desteklenen her renk derinliği ve renk biçimi için bu işlevin gx_canvas_pixelmap_rotate APIDefault uygulamaları tarafından çağrılır. |
| VOID * gx_display_driver_pixel_write) (GX_DRAW_CONTEXT * bağlam, ıNT x, INT y, GX_COLOR Color) <br/> Bu, tuval belleğine bir piksel yazmak için bir işleve yönelik bir işaretçidir. Bu işlevin varsayılan uygulamaları desteklenen her renk derinliği ve renk biçimi için sağlanır. <br/>
| VOID * gx_display_driver_block_move) (GX_DRAW_CONTEXT * bağlam, GX_RECTANGLE * Block, ıNT xshıft, ıNT en Shift) <br/> Bu, bir tuval içindeki piksel bloğunu taşımak veya kaydırmak için bir işlev işaretçisidir. Bu işlev öncelikle bir pencere içeriğini hızlı bir şekilde kaydırmak için kullanılır. Bu işlevin varsayılan uygulamaları desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (* gx_display_driver_pixel_blend) (GX_DRAW_CONTEXT * bağlam, ıNT x, INT y, GX_COLOR Color, GX_UBYTE Alpha) <br/> Bu işlev, x, y konumundaki tuval belleğindeki mevcut renk değeri ile gelen piksel renk değerini Alfa Blend için kullanılır. Bu işlevin varsayılan uygulamaları desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| GX_COLOR (* gx_display_driver_native_color_get) (GX_COLOR rawcolor) <br/> Bu işlev, Gux tarafından dahili olarak kullanılan 32-bit A:R: G:B renk biçiminden rengi tuvalin ve görüntülemenin yerel renk biçimine dönüştürür. Daha düşük renk derinliğinde çalışan görüntüleme sürücüleri için bazı renk bilgisi kaybı beklenmektedir. Bu işlevin varsayılan uygulamaları desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| USHORT (* gx_display_driver_row_pitch_get) (USHORT Width) <br/> İstenen tuval genişliği verilen bir grafik verileri satırının bayt sayısını veya bir görünümünü döndürür. Bu işlev, bir tuval oluşturmak için gereken bellek alanının boyutunu hesaplamak için kullanılır. Donanım tarama çizgisi hizalama kısıtlamaları nedeniyle satır aralığı ve genişlik her zaman aynı değildir. Bu işlevin varsayılan uygulamaları desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (* gx_display_driver_buffer_toggle) (yapı GX_CANVAS_STRUCT * tuval, GX_RECTANGLE * dirty_area) <br/> Bu, Çift arabellekli bellek sistemleri için çalışan ve görünür çerçeve arabellekleri arasında geçiş yapmak için bir işleve yönelik bir işaretçidir. Bu işlevin ilk olarak yeni çerçeve arabelleğini kullanmaya başlamasını, ardından iki arabelleğin eşitlenmiş durumda kalmasını sağlamak için yeni görünür arabelleğin değiştirilen bölümünü yardımcı arabelleğe kopyalamasını sağlamanız gerekir. | 
| VOID (* gx_display_driver_polygon_draw) (GX_DRAW_CONTEXT * bağlam, INT num_points, GX_POINT * köşeleri <br/> Çokgen çizmek için işlev işaretçisi. Bu işlevin varsayılan uygulamaları desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (* gx_display_driver_polygon_fill) (GX_DRAW_CONTEXT * bağlam, INT num_points, GX_POINT * köşeleri <br/> Doldurulmuş çokgen çizmek için işlev işaretçisi. Bu işlevin varsayılan uygulamaları desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (* gx_display_driver_circle_draw) (GX_DRAW_CONTEXT * bağlam, INT xcenter, ıNT i Center, UINT r) <br/> Bir daire çizmek için işlev işaretçisi. Bu işlevin varsayılan uygulamaları desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (* gx_display_driver_anti_aliased_circle_draw) (GX_DRAW_CONTEXT * bağlam, INT xcenter, ıNT i Center, UINT r) <br/> Kenar yumuşatma uygulanmış bir daire çizmek için bir işlev işaretçisi. Bu işlevin varsayılan uygulamaları desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (* gx_display_driver_wide_circle_draw) (GX_DRAW_CONTEXT * bağlam, INT xcenter, ıNT i Center, UINT r) <br/> Geniş bir ana hattı olan bir daire çizmek için bir işlev işaretçisi. Bu işlevin varsayılan uygulamaları desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (* gx_display_driver_wide_anti_aliased_circle_draw) (GX_DRAW_CONTEXT * bağlam, INT xcenter, ıNT i Center, UINT r) <br/> Geniş bir anahatsız bir kenar yumuşatma çemberi çizmek için bir işlev işaretçisi. Bu işlevin varsayılan uygulamaları desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (* gx_display_driver_circle_fill) (GX_DRAW_CONTEXT * bağlam, INT xcenter, ıNT i Center, UINT r) <br/> Dolgulu bir daire çizmek için işlev işaretçisi. Bu işlevin varsayılan uygulamaları desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (* gx_display_driver_arc_draw) (GX_DRAW_CONTEXT * bağlam, INT xcenter, ıNT i Center, UINT r, INT start_angle, INT end_angle) <br/> Bir yay çizmek için işlev işaretçisi. Bu işlevin varsayılan uygulamaları desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (* gx_display_driver_anti_aliased_arc_draw) (GX_DRAW_CONTEXT * bağlam, INT xcenter, ıNT i Center, UINT r, INT start_angle, INTend_angle) <br/> Kenar yumuşatma uygulanmış bir yay çizmek için bir işlev işaretçisi. Bu işlevin varsayılan uygulamaları desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (* gx_display_driver_wide_arc_draw) (GX_DRAW_CONTEXT * bağlam, INT xcenter, ıNT i Center, UINT r, INT start_angle, INT end_angle) <br/> Geniş bir ana hattı olan bir yay çizmek için işlev işaretçisi. Bu işlevin varsayılan uygulamaları desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (* gx_display_driver_anti_aliased_wide_arc_draw) (GX_DRAW_CONTEXT * bağlam, INT xcenter, ıNT i Center, UINT r, INT start_angle, INTend_angle) <br/> Kenar yumuşatma uygulanmış bir yay çizmek için bir işlev işaretçisi. Bu işlevin varsayılan uygulamaları desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (* gx_display_driver_arc_fill) (GX_DRAW_CONTEXT * bağlam, INT xcenter, ıNT i Center, UINT r, INT start_angle, INT end_angle) <br/> Doldurulmuş bir yay çizmek için işlev işaretçisi. Bu işlevin varsayılan uygulamaları desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (* gx_display_driver_pie_fill) (GX_DRAW_CONTEXT * bağlam, INT xcenter, ıNT i Center, UINT r, INT start_angle, INT end_angle) <br/> Doldurulmuş bir pasta çizmek için işlev işaretçisi. Bu işlevin varsayılan uygulamaları desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (* gx_display_driver_ellipse_draw) (GX_DRAW_CONTEXT * bağlam, INT xcenter, int i Center, INT a, INT b) <br/> Elips çizmek için işlev işaretçisi. Bu işlevin varsayılan uygulamaları desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (* gx_display_driver_anti_aliased_ellipse_draw) (GX_DRAW_CONTEXT * bağlam, INT xcenter, int i Center, INT a, INT b) <br/> Elips çizmek için işlev işaretçisi. Bu işlevin varsayılan uygulamaları desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (* gx_display_driver_wide_ellipse_draw) (GX_DRAW_CONTEXT * bağlam, INT xcenter, int i Center, INT a, INT b) <br/> Geniş bir anahatta Elips çizmek için bir işlev işaretçisi. Bu işlevin varsayılan uygulamaları desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (* gx_display_driver_anti_aliased_wide_ellipse_draw) (GX_DRAW_CONTEXT * bağlam, INT xcenter, int i Center, INT a, INT b) <br/> Geniş bir anahatta Elips çizmek için bir işlev işaretçisi. Bu işlevin varsayılan uygulamaları desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (* gx_display_driver_ellipse_fill) (GX_DRAW_CONTEXT * bağlam, INT xcenter, int i Center, INT a, INT b) <br/> Dolgulu bir elips çizmek için işlev işaretçisi. Bu işlevin varsayılan uygulamaları desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (* gx_display_driver_8bit_glyph_draw) (GX_DRAW_CONTEXT * bağlam, GX_RECTANGLE * draw_area, GX_POINT * map_offset, constGX_GLYPH * karakter) <br/> Geçerli çizim bağlamının fırçasını kullanarak tuvalde 1 8 bitlik diğer ad metin glifi çizmek için işlev işaretçisi. Bu işlevin varsayılan uygulamaları desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (* gx_display_driver_4bit_glyph_draw) (GX_DRAW_CONTEXT * bağlam, GX_RECTANGLE * draw_area, GX_POINT * map_offset, const GX_GLYPH * karakter) <br/> Geçerli çizim bağlamının fırçasını kullanarak tuvalde 1 4 bitlik diğer ad metin glifi çizmek için işlev işaretçisi. Bu işlevin varsayılan uygulamaları desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (* gx_display_driver_1bit_glyph_draw) (GX_DRAW_CONTEXT * bağlam, GX_RECTANGLE * draw_area, GX_POINT * map_offset, const GX_GLYPH * karakter) <br/> Geçerli çizim bağlamının fırçasını kullanarak tuvale 1 1 bitlik tek renkli metin karakteri çizmek için işlev işaretçisi. Bu işlevin varsayılan uygulamaları desteklenen her renk derinliği ve renk biçimi için sağlanır. |


