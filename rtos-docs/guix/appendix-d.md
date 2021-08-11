---
title: Ek D - GUIX Fırça, Tuval ve Gradyan Öznitelikleri
description: GUIX fırça, tuval ve gradyan öznitelikleri hakkında bilgi öğrenin.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 9fbc98f1094cab6be4bc0826fef7c0feb77b50b066b22342cd52404bd85ff98e
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116784640"
---
# <a name="appendix-d---guix-brush-canvas-and-gradient-attributes"></a>Ek D - GUIX Fırça, Tuval ve Gradyan Öznitelikleri

__**Fırça Stilleri:**__

**GX_BRUSH_OUTLINE**
- Değer: 0x0000
- Açıklama: Bu fırça stili, gx_canvas_rectangle_draw veya gx_canvas_polygon_draw. Bu stil, isteğe bağlı olarak doldurmaya ek olarak şeklin ana hatlarını da belirtmektedir. GX_BRUSH_OUTLINE stili ayarlanırsa ve GX_BRSUH_SOLID_FILL temizse, şekil yalnızca ana hatlarıyla açık olur.

**GX_BRUSH_SOLID_FILL**
- Değer: 0x0001
- Açıklama: Bu fırça stili şekil çizim işlevleri için geçerlidir ve istenen şeklin geçerli fırça dolgusu rengi kullanılarak düz bir renkle doldurulması gerektiğini gösterir.

**GX_BRUSH_PIXELMAP_FILL**
- Değer: 0x0002
- Açıklama: Bu fırça stili şekil çizme işlevleri için geçerlidir ve istenen şeklin geçerli fırça piksel haritasıyla doldurulması gerektiğini gösterir.

**GX_BRUSH_ALIAS**
- Değer: 0x0004
- Açıklama: Bu fırça stili tüm çizgi çizim ve şekil ana hatları için geçerlidir. Bu bayrak ayarlanırsa, çizgiler ve ana hatlar daha doğru ancak aynı zamanda diğer adlara sahip çizim algoritmalarını daha fazla zaman alan çizimlerdir. Bu stil bayrağı yalnızca 16 bpp renk derinliği ve üzerinde kullanılır.

**GX_BRUSH_UNDERLINE**
- Değer: 0x0008
- Açıklama: Bu bayrak metin çizimi için geçerlidir ve çizilen sonraki metnin altı çizili olması gerektiğini gösterir.

**GX_BRUSH_ROUND**
- Değer: 0x0010
- Açıklama: Bu bayrak çizgi çizimi için geçerlidir ve çizgi uçların varsayılan kare şekli yerine yuvarlak veya dairesel bir şekille çizilir.

__**Tuval Bayrakları:**__

**GX_CANVAS_SIMPLE**
- Değer: 0x01
- Açıklama: Ekran dışı çizim için kullanılan bir bellek tuvali.

**GX_CANVAS_MANAGED**
- Değer: 0x02
- Açıklama: Bileşik bina işleminin bir parçası olarak veya tek tuval mimarileri için arabelleğe geçiş işleminin bir parçası olarak etkin görüntüye otomatik olarak boşaltan tuval.

**GX_CANVAS_VISIBLE**
- Değer: 0x04
- Açıklama: Bu bayrak, tuval çizim içeriğini kaybetmeden tuvali açmak ve kapatmak için kullanılabilir.

**GX_CANVAS_MODIFIED**
- Değer: 0x08
- Açıklama: Gelecekte kullanılmak üzere ayrılmıştır.

**GX_CANVAS_COMPOSITE**
- Değer: 0x20
- Açıklama: Bu bayrak, bileşik tuvalde birden çok yönetilen tuvali bileşik olarak kabul etmek için çoklu tuval sistemi yapılandırırken uygulama tarafından kullanılır ve bileşik, donanım çerçevesi arabelleğine yönlendirilendir.

__**Gradyan Türleri:**__

**GX_GRADIENT_TYPE_VERTICAL**
- Değer: 0x01
- Açıklama: Dikey bir alfa harita gradyanı oluşturur.

**GX_GRADIENT_TYPE_ALPHA**
- Değer: 0x02
- Açıklama: Bir alfa-harita stili gradyanı oluşturur. Şu anda desteklenen tek gradyan stili bu.

**GX_GRADIENT_TYPE_MIRROR**
- Değer: 0x04
- Açıklama: Bu bayrak gradyanın genişlik/yükseklik aralığının merkezinde zirveye ulaşması ve sağ/alt kenarına ulaştığında başlangıç değerine dönmesi gerektiğini belirtir. Bu stil bayrağı olmadan, geçiş bayrağına bağlı olarak gradyan, üstten aşağıya veya soldan sağa GX_GRADIENT_TYPE_VERTICAL olur.