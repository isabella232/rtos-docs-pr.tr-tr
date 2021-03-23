---
title: Ek C-Gux pencere öğesi stilleri
description: GUX pencere öğesi stilleri hakkında bilgi edinin.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 83d5c5167739e91b7af8fce6b04213f610984fc6
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104827280"
---
# <a name="appendix-c---guix-widget-styles"></a>Ek C-Gux pencere öğesi stilleri

__***Genel stiller (çoğu pencere öğesi türü ile kullanılır):***__

**GX_STYLE_BORDER_NONE**
  - Değer: 0x00000000
  - Açıklama: kenarlığı olmayan bir pencere öğesi çizmek için bu stili kullanın.

**GX_STYLE_BORDER_RAISED**
  - Değer: 0x00000001
  - Açıklama: yükseltilmiş bir kenarlığa sahip pencere öğesi çizin.

**GX_STYLE_BORDER_RECESSED**
  - Değer: 0x00000002
  - Açıklama: bir kenar pencere öğesi ile yeniden oluşturulmuş bir kenarlık çizin.

**GX_STYLE_BORDER_THIN**
  - Değer: 0x00000004
  - Açıklama: tek piksellik genişlik kenarlığı çizin.

**GX_STYLE_BORDER_THICK** 
  - Değer: 0x00000008
  - Açıklama: kalın kenarlıklı pencere öğesi çizin.

**GX_STYLE_BORDER_MASK**
  - Değer: 0x0000000F
  - Açıklama: pencere öğesi stili üyesinin yalnızca stil alanlarını test etmek için kullanılan maske değeri.

**GX_STYLE_TRANSPARENT**
  - Değer: 0x10000000
  - Açıklama: en az kısmen saydam bir pencere öğesi oluşturun. Bu stil, pencere öğesi arka plan planı olarak yarı saydam bir pixelmap çizme pencere öğeleri de dahil olmak üzere tamamen donuk bir şekilde çizmediği zaman kullanılmalıdır. Bu stil bayrağı, pencere öğesi arka plan alanını yenilemek için pencere öğesi üst öğesinin çizilmek zorunda olduğunu bildirir.

**GX_STYLE_DRAW_SELECTED**
  - Değer: 0x20000000
  - Açıklama: pencere öğesinin seçili durum renkleri ve yazı tipleri kullanılarak çizilip çizilmeyeceğini belirtin. Farklı pencere öğesi türleri, pencere öğesinin Şu anda seçili olduğunu göstermek için DRAW_SELECTED stilini farklı şekillerde kullanır.

**GX_STYLE_ENABLED**
  - Değer: 0x40000000
  - Açıklama: pencere öğesinin kullanıcı giriş olaylarını kabul etmesine ve çıkış sinyalleri oluşturmasına izin veren pencere öğesini etkin olarak Işaretleyin.
  
**GX_STYLE_DYNAMICALLY_ALLOCATED**
  - Değer: 0x80000000
  - Açıklama: pencere öğesi denetim bloğu belleğinin pencere öğesi oluşturulduğunda gx_system_memory_allocator hizmeti kullanılarak dinamik olarak ayrıldığını ve pencere öğesi yok edildiğinde denetim blok belleği serbest bırakıldığını gösterir.

**GX_STYLE_USE_LOCAL_ALPHA**
  - Değer: 0x01000000
  - Açıklama: Gux çizim işlevlerini pencere öğesi çizerken yerel pencere öğesi Alfa değerini kullanmasını söyler. Bu bayrak normalde iç Gux mantığı tarafından pencere öğesi Soldurma animasyonlarını uygulamak için kullanılır.


__***Metin hizalama stilleri (metin çizimli tüm pencere öğeleri için uygulanan stiller):***__

**GX_STYLE_TEXT_LEFT**
  - Değer: 0x00001000
  - Açıklama: metin, pencere öğesi istemci alanı içinde sola hizalı olarak çizilir.

**GX_STYLE_TEXT_RIGHT** 
  - Değer: 0x00002000
  - Açıklama: metin, pencere öğesi istemci alanı içinde sağa hizalı olarak çizilir.

**GX_STYLE_TEXT_CENTER**
  - Değer: 0x00004000
  - Açıklama: metin, pencere öğesi istemci alanı içinde ortalanmış olarak çizilir.

**GX_STYLE_TEXT_COPY**
  - Değer: 0x00008000
  - Açıklama: varsayılan olarak, metin çizilen pencere öğeleri yalnızca uygulama tarafından geçirilen metne bir işaretçi tutar. Dize tablosunda tanımlanan statik olarak tanımlanmış metin için, pencere öğesinin atanan metnin özel bir kopyasını oluşturmak için bir neden yoktur. Ancak, bir pencere öğesine atanan metin sprintler () veya gx_utility_ltoa gibi işlevler kullanılarak dinamik olarak oluşturulduysa, pencere öğesine atanan metinlerin özel bir kopyasını tutmasına söylemek çok uygundur. Bu, uygulamanın metin dizesini tanımlarken otomatik veya geçici değişkenler kullanmasına izin verir. Bu, uygulamanın, dinamik olarak tanımlanan metni kullanan her metin pencere öğesi için statik olarak tanımlanmış karakter dizileri tanımlamak zorunda olacağını belirler. Bu stil bayrağı ayarlandığında pencere öğesi, atanan dizenin özel bir kopyasını tutmak için gereken bellek bloğunu dinamik olarak ayırmak üzere gx_system_memory_allocator işlevini kullanır. Bu nedenle, bu stil bayrağını kullanmak memory_allocator ve memory_deallocator işlevlerini tanımlayan uygulamada tahmin edilir. GX_STYLE_TEXT_COPY ayarlandıktan sonra temizlenmemelidir ve bunu yapmak öngörülemeyen sonuçlara neden olur.

__***Düğme stilleri (yalnızca Gux düğmesi pencere öğesi türleri için geçerlidir):***__

**GX_STYLE_BUTTON_PUSHED**
  - 0x00000010 değeri
  - Açıklama: düğmenin itilmiş veya seçili durumda olduğunu gösterir.

**GX_STYLE_BUTTON_TOGGLE**
  - Değer 0x00000020
  - Açıklama: düğme, her tıklama olayında itilmiş ve gönderilmemiş arasında durum olarak değişir. Bu stil, genellikle "CheckBox" stil düğmeleri ile kullanılır.

**GX_STYLE_BUTTON_RADIO**
  - Değer 0x00000040
  - Açıklama: Bu stil, düğmenin dışlandığını belirtir ve seçildiğinde tüm düğme eşdüzey öğelerinin seçimini kaldırın. Bu stil, genellikle "radyo düğmesi" stil düğmeleri ile kullanılır.

**GX_STYLE_BUTTON_EVENT_ON_PUSH**
  - Değer: 0x00000080
  - Açıklama: düğmenin başlangıçta gönderildiği bir tıklama olayı oluşturmadığını gösterir. Varsayılan işlem, düğme serbest bırakıldığında bir tıklama olayı oluşturmak olur.

**GX_STYLE_BUTTON_REPEAT**
  - Değer 0x00000100
  - Açıklama: Düğme itilmiş durumda tutulduğu zaman düğme üst öğesine yinelenen tıklama olaylarını göndermek gerektiğini gösterir.

__***Liste stilleri (yalnızca Gux listesi pencere öğesi türleri için geçerlidir):***__

**GX_STYLE_CENTER_SELECTED** 
  - Değer: 0x00000010
  - Açıklama: ayrılmış

**GX_STYLE_WRAP**
  - Değer 0x00000020
  - Açıklama: liste, başlangıç veya bitiş listesi dizininden aşağı kaydırıldığında liste alt öğelerinden baştan sona kaydırılır.

**GX_STYLE_FLICKABLE**
  - Değer: 0x00000040
  - Açıklama: ayrılmış

__***Pixelmap düğmesi ve simge düğmesi stilleri:***__

**GX_STYLE_HALIGN_CENTER**
  - Değer: 0x00010000
  - Açıklama: Bu düğme pixelmap, yatay eksende düğme sınırı içinde ortahizalı olmalıdır.

**GX_STYLE_HALIGN_LEFT**
  - Değer: 0x00020000
  - Açıklama: düğme pixelmap, Yatay eksenin düğme sınırı içinde sola hizalı olmalıdır.

**GX_STYLE_HALIGN_RIGHT**
  - Değer 0x00040000
  - Açıklama: düğme pixelmap, Yatay eksenin düğme sınırı içinde sağa hizalanmalıdır.

**GX_STYLE_VALIGN_CENTER**
  - Değer 0x00080000
  - Açıklama: Bu düğme pixelmap, dikey eksen üzerindeki düğme sınırı içinde ortahizalı olmalıdır.

**GX_STYLE_VALIGN_TOP**
  - Değer: 0x00100000
  - Açıklama: düğme pixelmap, dikey eksenin düğme sınırı içinde üste hizalı olmalıdır.

**GX_STYLE_VALIGN_BOTTOM**
  - Değer: 0x00200000
  - Açıklama: düğme pixelmap, dikey Yatay eksenin düğme sınırı içinde alta hizalı olmalıdır.

__***Kaydırıcı Stilleri (yalnızca GX_SLIDER ve türetilmiş pencere öğesi türleri için Appy):***__

**GX_STYLE_SHOW_NEEDLE**
  - Değer: 0x00000200
  - Açıklama: Bu stilin, iğne göstergesini çizmesi için bu stil dahil olmalıdır. Bu stil, uygulama kaydırıcı iğne 'yi devre dışı bırakmak isterse veya özel bir iğne göstergesi çizmek isterse devre dışı bırakılabilir.

**GX_STYLE_SHOW_TICKMARKS**
  - Değer: 0x00000400
  - Açıklama: kaydırıcı pencere öğesi, bu stil etkin olduğunda, kesikli değer çizgisi çizgilerinin yazılım çizimini oluşturacak.

**GX_STYLE_SLIDER_VERTICAL**
  - Değer 0x00000800
  - Açıklama: Dikey kaydırıcı oluşturmak için bu stil bayrağını ayarlayın ve yatay kaydırıcı oluşturmak için bu stil bayrağını temizleyin.

__***Sprite stilleri (yalnızca GX_SPRITE pencere öğesi türleri için geçerlidir):***__

**GX_STYLE_SPRITE_AUTO**
  - Değer: 0x00000010
  - Açıklama: sprite pencere öğesi GX_EVENT_SHOW olayını aldığında Sprite animasyonunun otomatik olarak çalışacağını gösterir.

**GX_STYLE_SPRITE_LOOP**
  - Değer: 0x00000020
  - Açıklama: Bu stille birlikte Sprite öğesi, uygulama tarafından durduruluncaya kadar Sprite animasyon kareleri aracılığıyla sürekli olarak döngü yapılır.

__***Pixelmap kaydırıcı stilleri:***__

**GX_STYLE_TILE_BACKGROUND**
  - Değer 0x00001000
  - Açıklama: kaydırıcı arka plan resmi, Sprite sınırlayıcı dikdörtgenini dolduracak şekilde döşenir. Bu, kaydırıcı arka planını dolduracak küçük dikey veya yatay bir şeritli görüntünün kullanılmasına izin verir.

__***Ek Ilerleme çubuğu stilleri:***__

**GX_STYLE_PROGRESS_PERCENT**
  - Değer: 0x00000010
  - Açıklama: Bu stil ayarlandığında, ilerleme çubuğu, bir ham değer yerine bir yüzde olarak çubuk değeri çizer. Metin, ilerleme çubuğu sınırlayıcı dikdörtgende ortalanır.

**GX_STYLE_PROGRESS_TEXT_DRAW**
  - Değer: 0x00000020
  - Açıklama: ilerleme çubuğu içinde ortalanan ondalık metin olarak geçerli ilerleme çubuğu değerini çizin.

**GX_STYLE_PROGRESS_VERTICAL**
  - Değer: 0x0000040
  - Açıklama: ilerlemenin dikey olarak yönlendirildiğini belirtin. Varsayılan değer yatay yöndir.

**GX_STYLE_PROGRESS_SEGMENT_FILL**:
  - **Değer**: 0x00000100
  - Açıklama: ilerleme çubuğu değeri, düz bir dolgu yerine bölümlenmiş dolgulu dikdörtgenlerle belirtilir.

__***Ek radyal Ilerleme çubuğu stilleri:***__

**GX_STYLE_RADIAL_PROGRESS_ALIAS**
  - Değer: 0x00000200
  - Açıklama: diğer ad yumuşatma fırçası stillerini kullanarak radyal ilerleme çubuğunu çizin. Bu daha fazla CPU bant genişliği gerektirir, ancak aynı zamanda bir Nicer görünümü oluşturur. Daha düşük performans CPU hedefleri için, bu stil bayrağını temizlemek daha hızlı çizim hızına neden olur.

**GX_STYLE_RADIAL_PROGRESS_ROUND**
  - Değer: 0x00000400
  - Açıklama: radyal ilerleme çubuğu yay çizerken yuvarlak çizgi sonu fırça stili kullanın. Varsayılan değer bir kare çizgisi sonu olur.

__***Ek metin girişi stilleri:***__

**GX_STYLE_ CURSOR_BLINK**
  - Değer: 0x00000040
  - Açıklama: metin girişi pencere öğesi imleci, faturalandırılmaktansa yanıp sönmenize ve kapanacaktır.

**GX_STYLE_ CURSOR_ALWAYS**
  - Değer: 0x00000080
  - Açıklama. Metin girişi pencere öğesi imleci normalde yalnızca pencere öğesi giriş odağa sahip olduğunda görüntülenir. Bu stil bayrağı imleci her zaman giriş odağının ne olursa olsun görünür hale getirir.

**GX_STYLE_TEXT_INPUT_NOTIFY_ALL**
  - Değer: 0x00000100
  - Açıklama: Bu stil bayrağıyla, metin girişi pencere öğesi tarafından anahtar aşağı olay her alındığında GX_EVENT_TEXT_EDITED olayı ayarlanır.

__***Ek pencere stilleri:***__

**GX_STYLE_TILE_WALLPAPER**
  - Değer: 0x00040000
  - Açıklama: pencere, atanan tüm duvar kağıdı görüntüsünü pencere istemci dikdörtgenini dolduracak şekilde döşemesini sağlar.

**GX_STYLE_AUTO_HSCROLL**
  - Değer: 0x00100000
  - Açıklama: gelecekte kullanılmak üzere ayrılmıştır.

**GX_STYLE_AUTO_VSCROLL**
  - Değer: 0x00200000
  - Açıklama: gelecekte kullanılmak üzere ayrılmıştır.

__***Ek menü stilleri:***__

**GX_STYLE_MENU_EXPANDED**
  - Değer: 0x00000010
  - Açıklama: Accordion Menü pencere öğesi başlangıçta genişletilmiş durumda.

__***Ek ağaç görünümü stilleri:***__

**GX_STYLE_TREE_VIEW_SHOW_ROOT_LINES**
  - Değer: 0x00000010
  - Açıklama: ağaç görünümü pencere öğesi düğüm simgesinden kök ağaç düğümüne çizgiler çizmelidir.

__***Ek kaydırma çubuğu stilleri:***__

**GX_SCROLLBAR_BACKGROUND_TILE**
  - Değer: 0x00010000
  - Açıklama: gelecekte kullanılmak üzere ayrılmıştır.

**GX_SCROLLBAR_RELATIVE_THUMB**
  - Değer: 0x00020000
  - Açıklama: ScrollBar Thumb Width (yatay kaydırma çubuğu için) veya yükseklik (dikey kaydırma çubuğu için), üst pencerenin görünür alanının, en düşük ve en fazla kaydırma çubuğu aralığına göre hesaplanır.

**GX_SCROLLBAR_END_BUTTONS**
  - Değer: 0x00040000
  - Açıklama: kaydırma çubuğu, ScrollBar bölgesinin her bir ucunda düğme oluşturur ve ekler.

**GX_SCROLLBAR_VERTICAL** 
  - Değer: 0x01000000
  - Açıklama: kaydırma çubuğu dikey olarak yönlendirilmelidir.

**GX_SCROLLBAR_HORIZONTAL**
  - Değer: 0x02000000
  - Açıklama: kaydırma çubuğu yatay olarak yönelimlidir.

__***Metin kaydırma tekerleği stilleri:***__

**GX_STYLE_TEXT_SCROLL_WHEEL_ROUND**
  - Değer: 0x00000200
  - Açıklama: kaydırma tekerleği, kaydırma tekerleğini yuvarlatılmış bir şekle sahip olacak şekilde görünmesini sağlamak için bir sinusoidal algoritmasını kullanır. Bu stil bayrağı, kaydırma tekerleği pencere öğesinin performansına önemli ölçüde ek yük ekleyebilir, ancak tekerlek 3B gerçekçi bir görünüm de verebilir.