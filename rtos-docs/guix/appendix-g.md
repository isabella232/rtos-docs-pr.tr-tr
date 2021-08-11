---
title: Ek G-Gux yazı tipi yapısı
description: GUX yazı tipi yapısı hakkında bilgi edinin.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 4c7cedb49268f97f8e1fc4cd28329b0b61e697d57562865896f0502bdd1d45f1
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116784198"
---
# <a name="appendix-g---guix-font-structure"></a>Ek G-Gux yazı tipi yapısı

GUX yazı tipleri normalde Gux Studio uygulaması tarafından oluşturulur ve yazı tipi glifleri Gux görüntü sürücüsü tarafından işlenir. Uygulama yazılımı yalnızca her metin görüntüleme pencere öğesinin kullanması gereken yazı tipi ve renkleri belirtmelidir. GUX yazı tipi veri yapıları, tamamlanma açısından burada belgelenmiştir ve geliştiricilerin diğer yazı tiplerini Gux yazı tipi biçiminde oluşturmak veya dönüştürmek için kendi yöntemlerini oluşturmalarına olanak tanır.

Her Gux yazı tipi bir GX_FONT yapısıyla başlar. GX_FONT yapısı, yazı tipi içinde içerilen karakter ve yazı tipinin çizgi yüksekliği gibi genel yazı tipi parametrelerini tanımlar. GX_FONT yapısı bir GX_GLYPH yapıları dizisine işaret eder. Her GX_GLYPH yapısı, belirli bir karakter glifinde genişlik, yükseklik ve taban çizgisi sapmasını tanımlar. GX_GLYPH yapı aynı zamanda gerçek glif bit eşlem verilerini de işaret eder (boşluk karakterleri için NULL olabilir).

Gx_api. h içinde bulunan GX_FONT yapısı şu şekilde bildirilmiştir:

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

Gx_font_format alanı, gx_api. h üstbilgi dosyasında tanımlandığı şekilde piksel başına bit ve diğer bayrakları tanımlar.

Gx_font_prespace, çok satırlı bir metin görüntüsüne her metin satırının üzerinde atlanacak piksel alanını tanımlar.

Gx_font_postspace alanı, çok satırlı bir metin görüntüsüne ait her metin satırının altına atlanacak piksel alanını tanımlar.

Gx_font_line_height alanı, yazı tipindeki en uzun glifin yüksekliğini tanımlar.

Gx_font_baseline alanı, en üstteki karakter piksel satırından yazı tipi taban çizgisi arasındaki mesafeyi piksel cinsinden tanımlar.

Gx_font_first_glyph alanı, bu yazı tipi sayfasında bulunan ilk Unicode karakter kodlamasını tanımlar.

Gx_font_last_glyph alanı, bu yazı tipi sayfasında yer alan son Unicode karakter kodlamasını tanımlar.

Gx_font_glyphs işaretçi bir GX_GLYPH yapıları dizisine işaret eder. Bu dizi, bu yazı tipi sayfasında bulunan karakter sayısına eşit olmalıdır, yani (gx_font_last_glyph – gx_font_first_glyph) + 1.

Gx_font_next_page üyesi birden çok sayfa yazı tipi için kullanılır. Birden çok sayfa yazı tipi, genişletilmiş karakter kümeleri için ve GX_GLYPH yapısı dizilerinin boyutunu iyileştirmek için kullanılır. Yazı tipinin tüm karakterleri bir yazı tipi sayfasında yer alıyorsa veya söz konusu yazı tipinin son sayfası ise gx_font_next_page üyesi GX_NULL olarak ayarlanır.

Yukarıda belirtildiği gibi, yukarıdaki GX_FONT yapısı bir GX_GLYPHS yapıları dizisine yönelik bir işaretçi içerir. Yazı tipi sayfasındaki her karakter için bir GX_GLYPH yapısı olmalıdır. GX_GLYPH yapısı şu şekilde tanımlanır:

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

Gx_glyph_map işaretçi, glif bit eşlemini işaret eder. Bu işaretçi, boşluk karakterleri için GX_NULL olabilir. Bit eşlem verileri 1 BPP, 2 BPP, 4 BPP veya 8 BPP alfa değeri olarak kodlanır. 1 bitlik veriler için 1 değeri, pikselin ön plan rengine yazılması gerektiğini gösterir ve 0 değeri pikselin saydam olduğunu gösterir. 8 bit veriler için değerler 0 (tamamen saydam) ile 255 (tamamen opag) arasındadır. Tüm ara değer, kenar yumuşatma uygulanmış yazı tipleri için bir karıştırma değeri temsil eder. Glif bit eşlem verileri her zaman, 8 ' den az BPP veri değeri kullanan biçimler için tam bayt hizalamasına doldurulur.

Gx_glyph_ascent ve gx_glyph_descent değerleri, yazı tipi taban çizgisine göre glifi dikey olarak konumlandırır.

Gx_glyph_width ve gx_glyph_height değerleri, glif bit eşlem verilerinin boyutunu belirtir.

Gx_glyph_advance değeri, glifi çizdikten sonra çizim konumunu ilerletmek için piksel genişliğini belirtir (glif genişliğine eşit olmayabilir).

Gx_glyph_leading değeri, glifi işlemeden önce x yönünde ilerlemek için pikselleri belirtir.