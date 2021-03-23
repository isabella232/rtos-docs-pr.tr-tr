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
# <a name="appendix-d---guix-brush-canvas-and-gradient-attributes"></a>Ek D-Gux fırçası, tuval ve gradyan öznitelikleri

__**Fırça stilleri:**__

**GX_BRUSH_OUTLINE**
- Değer: 0x0000
- Açıklama: Bu fırça stili, gx_canvas_rectangle_draw veya gx_canvas_polygon_draw gibi şekil çizim işlevleri için geçerlidir. Bu stil, isteğe bağlı olarak doldurulmanın yanı sıra şeklin ana hatlarıyla toplanmalıdır. GX_BRUSH_OUTLINE stili ayarlanmışsa ve GX_BRSUH_SOLID_FILL silinirse, şekil yalnızca Seviyelendirilmiş olur.

**GX_BRUSH_SOLID_FILL**
- Değer: 0x0001
- Açıklama: Bu fırça stili şekil çizim işlevlerine uygulanır ve istenen şeklin geçerli fırça dolgusu rengi kullanılarak bir düz renkle doldurulması gerektiğini gösterir.

**GX_BRUSH_PIXELMAP_FILL**
- Değer: 0x0002
- Açıklama: Bu fırça stili şekil çizim işlevlerine uygulanır ve istenen şeklin geçerli fırça pixelmap ile doldurulmuş olması gerektiğini gösterir.

**GX_BRUSH_ALIAS**
- Değer: 0x0004
- Açıklama: Bu fırça stili tüm çizgi çizme ve şekil anahatları için geçerlidir. Bu bayrak ayarlandıysa, satırlar ve anahatlar daha doğru bir şekilde çizilmiştir, ancak aynı zamanda diğer ad yumuşatma daha fazla olan çizim algoritmalarından daha fazla zaman alır. Bu stil bayrağı yalnızca 16 bit renk derinlikleri ve üzeri için kullanılır.

**GX_BRUSH_UNDERLINE**
- Değer: 0x0008
- Açıklama: Bu bayrak metin çizime uygulanır ve sonraki metnin çizilebileceğini belirtir.

**GX_BRUSH_ROUND**
- Değer: 0x0010
- Açıklama: Bu bayrak, çizgi çizme için geçerlidir ve çizgi uçlarının varsayılan kare şekli yerine bir yuvarlak veya dairesel şekille çizildiğini gösterir.

__**Tuval bayrakları:**__

**GX_CANVAS_SIMPLE**
- Değer: 0x01
- Açıklama: ekran çizimini devre dışı bırakmak için kullanılan bir bellek tuvali.

**GX_CANVAS_MANAGED**
- Değer: 0x02
- Açıklama: Bileşik yapı sürecinin bir parçası olarak veya tek tuvalli mimarilere yönelik arabellek geçiş işleminin bir parçası olarak etkin ekranı otomatik olarak temizlenen bir tuval.

**GX_CANVAS_VISIBLE**
- Değer: 0x04
- Açıklama: Bu bayrak, tuval çizim içeriklerinin kaybedilmesi gerekmeden bir tuvali açmak ve kapatmak için kullanılabilir.

**GX_CANVAS_MODIFIED**
- Değer: 0x08
- Açıklama: gelecekte kullanılmak üzere ayrılmıştır.

**GX_CANVAS_COMPOSITE**
- Değer: 0x20
- Açıklama: Bu bayrak, uygulama tarafından, birden çok yönetilen ve bileşik tuvalde bileşik bir sistem olan bir çoklu tuval sistemi yapılandırırken kullanılır ve bileşik donanım çerçeve arabelleğine dayalıdır.

__**Gradyan türleri:**__

**GX_GRADIENT_TYPE_VERTICAL**
- Değer: 0x01
- Açıklama: dikey bir harflerden oluşan harita gradyanı oluşturur.

**GX_GRADIENT_TYPE_ALPHA**
- Değer: 0x02
- Açıklama: Alfa harita stil degradesini oluşturma. Bu, şu anda desteklenen tek degrade stilidir.

**GX_GRADIENT_TYPE_MIRROR**
- Değer: 0x04
- Açıklama: Bu bayrak, degradenin genişlik/yükseklik aralığının ortasında üst sınır olmayacağını ve sağ/alt kenara ulaşan başlangıç değerine geri döneceğini gösterir. Bu stil bayrağı olmadan gradyan, GX_GRADIENT_TYPE_VERTICAL bayrağına bağlı olarak yukarıdan aşağıya veya soldan sağa doğrusal bir gradyan olur.