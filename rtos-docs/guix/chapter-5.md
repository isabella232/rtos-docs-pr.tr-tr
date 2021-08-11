---
title: Bölüm 5 - GUIX Görüntü Sürücüleri
description: GUIX Görüntüleme sürücüleri, soyut çizim tuvali ile fiziksel görüntü donanımı arasındaki yazılım arabirimini tanımlar.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 804187ce8562e274205e97448da77d29f99016072c137cb3c4f1f42dac58c432
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116788550"
---
# <a name="chapter-5---guix-display-drivers"></a>Bölüm 5 - GUIX Görüntü Sürücüleri

GUIX Görüntüleme sürücüleri, soyut çizim tuvali ile fiziksel görüntü donanımı arasındaki yazılım arabirimini tanımlar. GUIX görüntü sürücüsü, tuval belleğinde piksel renk bilgilerini gerçekten değiştiren ve tuval belleğini çift arabelleğe alınan sistemlerde fiziksel görüntüleme çerçevesi arabelleğine aktaran en düşük düzeyli çizim işlevlerini gerçekleştirir.

GUIX Görüntüleme sürücüleri, fiziksel görüntüleme parametrelerini içeren bir yapı ve alt düzey sürücü işlevlerine bir dizi işlev işaretçisi ile tanımlanır. Bu dolaylı işlev işaretçileri kullanılarak soyut tuval ve pencere öğesi çizim işlevleri, donanım ayrıntılarından tamamen bağımsız hale gelir.

GUIX, desteklenen her renk derinliği ve renk biçimi için eksiksiz, tam işlevsel, varsayılan bir çizim işlevleri kümesi sağlar. Belirli bir donanım hızlandırma özelliğine veya donanıma özgü diğer önemli noktalara sahip bir görüntü sürücüsü uygulanırken, bu varsayılan çizim işlevleri normalde son sürücü uygulaması için yeterlidir. Bu en basit sürücüler için, normalde sürücü yazılımında uygulanması gereken tek işlev, donanım aygıtını yapılandırmak için bir işlevdir. Bu genellikle, ÇEŞITLI donanım yazmazlarını BAŞLATMAyı içerir ve BU DAH ekran saatini, görüntüleme boyutlarını vb. tanımlar. Diğer tüm işlevler için sürücü uygulaması, istenen renk derinliği GX_DISPLAY için varsayılan işlev uygulamalarına yönelik işlev işaretçilerini başlatmanız gerekir.

Özel bir görüntü sürücüsü uygulanırken, en iyi yöntem önce, desteklemek istediğiniz renk derinliği için varsayılan yazılım uygulamasıyla görüntü sürücüsü çizim işlev işaretçilerinizi başlatmak ve ardından özel işlev uygulamalarınızı çağırmayı istediğiniz bu işlev işaretçilerini (varsa) değiştirmektir. Bu soruna yardımcı olmak için desteklenen her renk derinliği ve biçimi için varsayılan bir kurulum işlevi vardır. Örneğin, 16 bit 5:6:5 biçimli RGB görüntü sürücüsü yazıyorsanız, özel sürücün normalde ilk olarak bu renk derinliği için genel kurulum yordamını çağırmaktır:

UINT my_custom_565_display_driver(GX_DISPLAY *display)

```c
{
      
      // perform standard function pointer setup
      
      _gx_display_driver_565rgb_setup(display, GX_NULL,
      
             my_buffertoggle);

}
```

Yukarıdaki my_buffer_toggle parametresi, görüntü sürücüsü arabelleği geçiş işlevinizin işaretçisidir (sürücü tek arabelleğe GX_NULL ve doğrudan donanım çerçevesi arabelleğine çiziyorsa bu işlev için geçerli olabilir).

Özel bir görüntü sürücüsü yazıyorsanız, gx_display.h üst bilgi dosyasını özel sürücü kaynağınıza dahil etmek gerekir. Bu dosya, uygulama düzeyi yazılım için kullanılabilir bir iç kullanım üst bilgi dosyasıdır.

GUIX görüntü düzeyi çizim işlevleri, bir veri yapısına işaretçi olarak **GX_DRAW_CONTEXT** alır. Bu **GX_DRAW_CONTEXT,** kullanılan fırça ve renklerle birlikte geçerli çizim işlemi için kırpma koordinatlarını tanımlar. Her çizim işlevi, işlev gereksinimlerine özgü ek parametreler girişi olarak alır.

GX_DISPLAY **sürücü** giriş noktasının imzası olarak tanımlanır

```c
UINT <device>_graphics_driver_<format>(GX_DISPLAY *diplay)
```

Bu işlevin adı tamamen uygulayıcıya bağlıyken GUIX ile sağlanan sürücülerin kuralı, yukarıdaki alan için alan ve renk biçiminde donanıma özgü bir cihaz <device> <format> adı kullanmaktır.

Bu işlevin giriş **olarak GX_DISPLAY** yapılandırmayı başlatması ve gerekli donanım kurulumunu gerçekleştirmesi gerekir. Bu **GX_DISPLAY** aşağıdaki alanları içerir.

| &nbsp; |
| --- | --- |
| ULONG gx_display_id <br/> Bu, belirli bir sürücünün birden fazla örneğinin oluşturulmuş olduğu durumlarda uygulama tarafından kullanım için bir alandır. |
| CHAR *gx_display_name <br/> Sürücüyü tanımlamak için kullanılan isteğe bağlı bir ad. |
| GX_DISPLAY *gx_display_created_next <br/> Bu alan GUIX tarafından başlatılır ve tüm örnek örneklerinin listesini oluşturmak ve GX_DISPLAY kullanılır. |
| GX_DISPLAY *gx_display_created_previous <br/> Bu alan GUIX tarafından başlatılır ve tüm örnek örneklerinin listesini oluşturmak ve GX_DISPLAY kullanılır. |
| GX_VALUE gx_display_color_format <br/> Bu alan, bu sürücü tarafından desteklenen grafik veri biçimini yansıtacak. Renk biçimi türleri gx_api.h üst bilgi dosyasında tanımlanır. |
| GX_VALUE gx_display_width <br/> Bu alan, piksel cinsinden fiziksel görüntüleme genişliğini tutmak için başlatılmış olmalıdır. |
| GX_VALUE gx_display_height <br/> Bu alan, piksel cinsinden fiziksel ekran yüksekliğini tutmak için başlatılmış olmalıdır. |
| GX_COLOR *gx_display_color_table <br/> Bu, renk kimliği değerlerini belirli renk değerlerine renk biçimine dönüştürmek için kullanılan bir tablonun işaretçisidir. |
| GX_PIXELMAP *gx_display_pixelmap_table <br/> Bu, bu görüntü için etkin piksel haritası tablosuna bir işaretçidir. |
| GX_FONT *gx_display_font_table <br/> Bu, bu görüntü için etkin yazı tipi tablosuna bir işaretçidir. |
| GX_COLOR *gx_display_palette <br/> Palet modu sürücüleri için bu, etkin renk paletinin işaretçisidir. Bir renk paleti kullanmayan sürücüler için bu işaretçi GX_NULL. |
| UINT gx_display_pixelmap_table_size <br/> Etkin piksel haritası tablosunda girdi sayısı. |
| UINT gx_display_font_table_size <br/> Etkin yazı tipi tablosunda girdi sayısı. |
| UINT gx_display_palette_size <br/> Renk paletinde girdi sayısı (varsa). |
| ULONG gx_display_handle <br/> Ekranı belirten benzersiz *bir tanımlayıcı* veya tanıtıcı.
| UINT gx_display_driver_ready <br/> Bu alan, sürücü işlem için hazır olduğunda GUIX'e sinyal gönderir. Bazı durumlarda, sürücü birkaç başlatma ve yapılandırma düzeyi gerektirir ve bu süre boyunca GUIX sürücünün kullanılmasına çalışmaz. Sürücü çizim isteklerine hizmet vermeye hazır olduğunda bu bayrağın 1 olarak ayarlanmış olması gerekir. |
| VOID *gx_display_driver_data <br/> Bu alan, sürücü uygulaması tarafından kullanım içindir. Sürücünün GX_DISPLAY yapısında mevcut olan ek bilgileri oluşturması ve buna başvurması gerekirse, sürücü için alan ayırmalı ve bu yapı alanını kullanarak bu ek verilere işaret edin. Sürücüye özgü ek verilere örnek olarak sürücü tarafından kullanılan DMA kanalı veya görüntüleme çerçevesi arabelleğinin bağlı olduğu SPI kanalı yer almaktadır. |
| VOID (*gx_display_driver_drawing_initiate)(yapı GX_DISPLAY_STRUCT *tuval GX_CANVAS_STRUCT) <br/> Bu, NULL olmayan bir işlev işaretçisi tarafından gx_canvas_drawing_initiate çağrılır. Grafik hızlandırıcısı veya donanım grafik görüntüleme listesi kullanan görüntü sürücüleri için, bu işlev yeni bir görüntüleme listesi başlamak için kullanılabilir. Bu işlev işaretçisi NULL olabilir. |
| VOID (*gx_display_driver_palette_set)(yapı GX_DISPLAY_STRUCT *display, GX_COLOR *palette, INT count) <br/> Bu, bir işleve renk paleti yüklemek için bir işaretçidir. Sürücü paletde (renk arama tablosu veya CLUT olarak da adlandırılan) çalışmadıkça bu işlev NULL olur. |
| VOID (*gx_display_driver_simple_line_draw)(GX_DRAW_CONTECT *context, INT x1, INTy1, INT x2, INT y2) <br/> Bu, bir işlevin diğer addan koruma özelliğine sahip olmayan genel çizgi çizimi uygulamasına işaret ediyor. Bu işlevin varsayılan uygulamaları, desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (*gx_display_driver_simple_wide_line_draw)(GX_DRAW_CONTECT *context, INT x1, INTy1, INT x2, INT y2) <br/> Bu, bir işlevin genel geniş çizgi çizimi uygulamak için bir işaretçidir, diğer addan koruma yoktur. Bu işlevin varsayılan uygulamaları, desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (*gx_display_driver_anti_aliased_line_draw)(GX_DRAW_CONTECT *context, INT x1, INTy1, INT x2, INT y2) <br/> Bu, genel diğer addan koruma çizgi çizimi uygulamak için bir işlevin işaretçisidir. Bu işlevin varsayılan uygulamaları, desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (*gx_display_driver_anti_aliased_wide_line_draw)(GX_DRAW_CONTECT *context, INT x1, INTy1, INT x2, INT y2) <br/> Bu, genel diğer addan koruma uygulanmış geniş çizgi çizimi uygulamak için bir işlevin işaretçisidir. Bu işlevin varsayılan uygulamaları, desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (*gx_display_driver_horizonal_line_draw)(GX_DRAW_CONTECT *context, INT x1, INT x2, INT y) <br/> Bu, yatay çizgi çiziminin özel büyük/küçük harflerini uygulamak için bir işlevin işaretçisidir. Bu işlevin varsayılan uygulamaları, desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (*gx_display_driver_horizonal_pixelmap_line_draw)(GX_DRAW_CONTECT *context, INT x1, INT x2, INT y, GX_PIXELMAP *map) <br/> Bu, tek bir piksel haritası satırı çizmeyi uygulamak için bir işlevin işaretçisidir. Bu işlev, desenleri doldurmak için dahili olarak kullanılır. Bu işlevin varsayılan uygulamaları, desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (*gx_display_driver_vertical_line_draw)(GX_DRAW_CONTECT *context, INT y1, INT y2, INT x) <br/> Bu, yatay çizgi çiziminin özel büyük/küçük harflerini uygulamak için bir işlevin işaretçisidir. Bu işlevin varsayılan uygulamaları, desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (*gx_display_driver_horizonal_pattern_line_draw)(GX_DRAW_CONTECT *context, INT x1, INT x2, INT y) <br/> Bu, yatay desen çizgi çizimi uygulamak için bir işlevin işaretçisidir. Bu işlevin varsayılan uygulamaları, desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (*gx_display_driver_vertical_pattern_line_draw)(GX_DRAW_CONTECT *bağlam, INT y1, INT y2, INT x) <br/> Bu, dikey desen çizgi çizimi uygulamak için bir işlevin işaretçisidir. Bu işlevin varsayılan uygulamaları, desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (*gx_display_driver_canvas_copy)(yapı GX_CANVAS_STRUCT *kaynak, yapı GX_CANVAS_STRUCT *dest) <br/> Bu, tuval verilerini bir tuvalden diğerine kopyalamak için bir işlevin işaretçisidir. Kaynak tuvalde kopyalama alanı tanımlamak için geçersiz dikdörtgen kullanılır. Bu işlevin varsayılan uygulamaları, desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (*gx_display_driver_canvas_blend)(yapı GX_CANVAS_STRUCT *kaynak, yapı GX_CANVAS_STRUCT *dest) <br/> Bu, hedef tuvalde var olan verilerle birlikte kaynak tuvalden alfa karışımı tuval verilerine bir işlevin işaretçisidir. Blend alanı tanımlamak için kaynak tuval geçersiz dikdörtgen kullanılır. Bu işlevin varsayılan uygulamaları, desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (*gx_display_driver_pixelmap_blend)(GX_DRAW_CONTEXT *context, INT xpos, INT ypos, GX_PIXELMAP *pmp, GX_UBYTE alpha) <br/> Bu, çizim bağlamı tarafından tanımlanan arka plan tuvali üzerinde piksel haritasını karıştırmak için bir işlevin işaretçisidir. Sağlanan alfa değeri, piksel haritası verisinde yer alan bir alfa kanalına ek olarak olabilir. Bu işlevin varsayılan uygulamaları, desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (*gx_display_driver_pixelmap_draw)(GX_DRAW_CONTEXT *context, INT xpos, INT ypos, GX_PIXELMAP *pmp) <br/> Bu, çizim bağlamı tarafından tanımlanan tuvale piksel haritası çizmek için bir işlevin işaretçisidir. Bu işlevin varsayılan uygulamaları, desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (*gx_display_driver_jpeg_draw)(GX_DRAW_CONTEXT *context, INT xpos, INT ypos, GX_PIXELMAP *pmp) <br/> Bu, jpg görüntüsünün kodunu çözmek ve doğrudan tuvale işlemek için bir işlevin işaretçisidir. Bu işlev yalnızca GX_SOFTWARE_DECODER_SUPPORT sağlanır. Bu işlev işaretçisi NULL olur. Bu işlevin varsayılan uygulamaları, desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (*gx_display_driver_png_draw)(GX_DRAW_CONTEXT *context, INT xpos, INT ypos, GX_PIXELMAP *pmp) <br/> Bu, bir png görüntüsünün kodunu çözmek ve doğrudan tuvale işlemek için bir işlevin işaretçisidir. Bu işlev yalnızca GX_SOFTWARE_DECODER_SUPPORT sağlanır. Bu işlev işaretçisi NULL olur. Bu işlevin varsayılan uygulamaları, desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (*gx_display_driver_pixelmap_rotate)(GX_DRAW_CONTEXT *bağlam, INT xpos, INT ypos, GX_PIXELMAP *pmp INT açısı, INT rot_cx, INT rot_cy) <br/> Bu, bir pixemap'i döndürmek ve sonucu doğrudan tuvale işlemek için bir işlevin işaretçisidir. Bu işlev, desteklenen her renk derinliği gx_canvas_pixelmap_rotate renk biçimi için APIDefault uygulamaları tarafından çağrılır. |
| VOID *gx_display_driver_pixel_write)(GX_DRAW_CONTEXT *bağlam, INT x, INT y, GX_COLOR rengi) <br/> Bu, tuval belleğine bir piksel yazmak için bir işlevin işaretçisidir. Bu işlevin varsayılan uygulamaları, desteklenen her renk derinliği ve renk biçimi için sağlanır. <br/>
| VOID *gx_display_driver_block_move)(GX_DRAW_CONTEXT*context,GX_RECTANGLE *block, INT xshift, INT yshift) <br/> Bu, tuval içindeki piksel bloklarını taşımaya veya kaydırmaya yönelik bir işlev işaretçisidir. Bu işlev öncelikli olarak bir pencere içeriğini hızla kaydırmak için kullanılır. Bu işlevin varsayılan uygulamaları, desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (*gx_display_driver_pixel_blend)(GX_DRAW_CONTEXT *context, INT x, INT y, GX_COLOR color, GX_UBYTE alpha) <br/> Bu işlev, gelen piksel renk değerini tuval belleğinde x,y konumundaki mevcut renk değeriyle alfasayısal olarak karıştırmak için kullanılır. Bu işlevin varsayılan uygulamaları, desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| GX_COLOR (*gx_display_driver_native_color_get)(GX_COLOR rawcolor) <br/> Bu işlev, GUIX tarafından dahili olarak kullanılan 32 bit A:R:G:B renk biçimini tuvalin ve ekranın yerel renk biçimine dönüştürür. Daha düşük renk derinliklerinde çalışan görüntü sürücüleri için bazı renk bilgileri kaybı bekleniyor. Bu işlevin varsayılan uygulamaları, desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| USHORT (*gx_display_driver_row_pitch_get)(USHORT genişliği) <br/> İstenen tuval genişliğine göre grafik verisi satırlarından birinin baytı sayısını veya adımlarını döndürür. Bu işlev, tuval oluşturmak için gereken bellek alanı boyutunu hesaplamak için kullanılır. Donanım taraması satır hizalama kısıtlamaları nedeniyle satır perdesi ve genişlik her zaman aynı değildir. Bu işlevin varsayılan uygulamaları, desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (*gx_display_driver_buffer_toggle)(yapı GX_CANVAS_STRUCT *tuval, GX_RECTANGLE *dirty_area) <br/> Bu, çift arabelleğe alan bellek sistemleri için çalışan ve görünür çerçeve arabellekleri arasında geçiş yapmak için bir işlevin işaretçisidir. Bu işlev önce donanıma yeni çerçeve arabelleği kullanmaya başlamasını, ardından yeni görünür arabelleğin değiştirilmiş bölümünü kopyalayıp yardımcı arabelleğe kopyalayıp iki arabelleğin eşit durumda kalmasını sağlar. | 
| VOID (*gx_display_driver_polygon_draw)(GX_DRAW_CONTEXT *bağlam, INT num_points, GX_POINT *köşeler <br/> Çokgen çizmek için bir işlevin işaretçisi. Bu işlevin varsayılan uygulamaları, desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (*gx_display_driver_polygon_fill)(GX_DRAW_CONTEXT *bağlam, INT num_points, GX_POINT *köşeler <br/> Doldurulmuş bir çokgen çizmek için bir işlevin işaretçisi. Bu işlevin varsayılan uygulamaları, desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (*gx_display_driver_circle_draw)(GX_DRAW_CONTEXT *context, INT xcenter, INT ycenter, UINT r) <br/> Daire çizmek için işlev işaretçisi. Bu işlevin varsayılan uygulamaları, desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (*gx_display_driver_anti_aliased_circle_draw) (GX_DRAW_CONTEXT * bağlam, INT xcenter, INT ycenter, UINT r) <br/> Diğer addan koruma dairesini çizmek için bir işlevin işaretçisi. Bu işlevin varsayılan uygulamaları, desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (*gx_display_driver_wide_circle_draw)(GX_DRAW_CONTEXT *context, INT xcenter, INT ycenter, UINT r) <br/> Geniş ana hatlı bir daire çizmek için bir işlevin işaretçisi. Bu işlevin varsayılan uygulamaları, desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (*gx_display_driver_wide_anti_aliased_circle_draw) (GX_DRAW_CONTEXT* bağlam, INT xcenter, INT ycenter, UINT r) <br/> Bir işlevin işaretçisi, geniş bir ana hat ile diğer addan korumalı bir daire çizin. Bu işlevin varsayılan uygulamaları, desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (*gx_display_driver_circle_fill)(GX_DRAW_CONTEXT *context, INT xcenter, INT ycenter, UINT r) <br/> Doldurulmuş daire çizmek için bir işlevin işaretçisi. Bu işlevin varsayılan uygulamaları, desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (*gx_display_driver_arc_draw)(GX_DRAW_CONTEXT *context, INT xcenter, INT ycenter, UINT r, INT start_angle, INT end_angle) <br/> Yay çizmek için bir işlevin işaretçisi. Bu işlevin varsayılan uygulamaları, desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (*gx_display_driver_anti_aliased_arc_draw)(GX_DRAW_CONTEXT *context, INT xcenter, INT ycenter, UINT r, INT start_angle, INTend_angle) <br/> Diğer addan koruma yay çizmek için bir işlevin işaretçisi. Bu işlevin varsayılan uygulamaları, desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (*gx_display_driver_wide_arc_draw)(GX_DRAW_CONTEXT *context, INT xcenter, INT ycenter, UINT r, INT start_angle, INT end_angle) <br/> Geniş bir ana hat ile bir yay çizmek için işlev işaretçisi. Bu işlevin varsayılan uygulamaları, desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (*gx_display_driver_anti_aliased_wide_arc_draw)(GX_DRAW_CONTEXT *context, INT xcenter, INT ycenter, UINT r, INT start_angle, INTend_angle) <br/> Diğer addan koruma yay çizmek için bir işlevin işaretçisi. Bu işlevin varsayılan uygulamaları, desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (*gx_display_driver_arc_fill)(GX_DRAW_CONTEXT *context, INT xcenter, INT ycenter, UINT r, INT start_angle, INT end_angle) <br/> Dolgulu bir yay çizmek için bir işlevin işaretçisi. Bu işlevin varsayılan uygulamaları, desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (*gx_display_driver_pie_fill)(GX_DRAW_CONTEXT *context, INT xcenter, INT ycenter, UINT r, INT start_angle, INT end_angle) <br/> Doldurulmuş bir pasta çizmek için işlev işaretçisi. Bu işlevin varsayılan uygulamaları, desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (*gx_display_driver_ellipse_draw)(GX_DRAW_CONTEXT *context, INT xcenter, INT ycenter, INT a, INT b) <br/> Üç nokta çizmek için işlev işaretçisi. Bu işlevin varsayılan uygulamaları, desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (*gx_display_driver_anti_aliased_ellipse_draw)(GX_DRAW_CONTEXT *context, INT xcenter, INT ycenter, INT a, INT b) <br/> Üç nokta çizmek için işlev işaretçisi. Bu işlevin varsayılan uygulamaları, desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (*gx_display_driver_wide_ellipse_draw)(GX_DRAW_CONTEXT *context, INT xcenter, INT ycenter, INT a, INT b) <br/> Geniş bir ana hat ile üç nokta çizmek için işlev işaretçisi. Bu işlevin varsayılan uygulamaları, desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (*gx_display_driver_anti_aliased_wide_ellipse_draw)(GX_DRAW_CONTEXT *context, INT xcenter, INT ycenter, INT a, INT b) <br/> Geniş bir ana hat ile üç nokta çizmek için işlev işaretçisi. Bu işlevin varsayılan uygulamaları, desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (*gx_display_driver_ellipse_fill)(GX_DRAW_CONTEXT *context, INT xcenter, INT ycenter, INT a, INT b) <br/> Doldurulmuş bir üç nokta çizmek için işlev işaretçisi. Bu işlevin varsayılan uygulamaları, desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (*gx_display_driver_8bit_glyph_draw)(GX_DRAW_CONTEXT *bağlam, GX_RECTANGLE *draw_area, GX_POINT *map_offset, constGX_GLYPH *glyph) <br/> Geçerli çizim bağlamının fırçasını kullanarak tuvalde 1 8 bitlik diğer ad metin glifi çizmek için işlev işaretçisi. Bu işlevin varsayılan uygulamaları desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (* gx_display_driver_4bit_glyph_draw) (GX_DRAW_CONTEXT * bağlam, GX_RECTANGLE * draw_area, GX_POINT * map_offset, const GX_GLYPH * karakter) <br/> Geçerli çizim bağlamının fırçasını kullanarak tuvalde 1 4 bitlik diğer ad metin glifi çizmek için işlev işaretçisi. Bu işlevin varsayılan uygulamaları desteklenen her renk derinliği ve renk biçimi için sağlanır. |
| VOID (* gx_display_driver_1bit_glyph_draw) (GX_DRAW_CONTEXT * bağlam, GX_RECTANGLE * draw_area, GX_POINT * map_offset, const GX_GLYPH * karakter) <br/> Geçerli çizim bağlamının fırçasını kullanarak tuvale 1 1 bitlik tek renkli metin karakteri çizmek için işlev işaretçisi. Bu işlevin varsayılan uygulamaları desteklenen her renk derinliği ve renk biçimi için sağlanır. |


