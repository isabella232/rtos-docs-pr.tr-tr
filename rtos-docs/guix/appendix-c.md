---
title: Ek C - GUIX Pencere Öğesi Stilleri
description: GUIX pencere öğesi stilleri hakkında bilgi edinebilirsiniz.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 9519d68af64b777e34deb1bf11e6962e78a96b86bdbfd90f5b379c5b56c92268
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116784657"
---
# <a name="appendix-c---guix-widget-styles"></a>Ek C - GUIX Pencere Öğesi Stilleri

__***Genel Stiller (Çoğu pencere öğesi türüyle kullanılır):***__

**GX_STYLE_BORDER_NONE**
  - Değer: 0x00000000
  - Açıklama: Kenarlıkları olan bir pencere öğesi çizmek için bu stili kullanın.

**GX_STYLE_BORDER_RAISED**
  - Değer: 0x00000001
  - Açıklama: Yükseltilmiş kenarlıkla pencere öğesi çizin.

**GX_STYLE_BORDER_RECESSED**
  - Değer: 0x00000002
  - Açıklama: Kenarlıkla pencere öğesi çizme.

**GX_STYLE_BORDER_THIN**
  - Değer: 0x00000004
  - Açıklama: Bir piksel genişlik kenarlık çizin.

**GX_STYLE_BORDER_THICK** 
  - Değer: 0x00000008
  - Açıklama: Kalın kenarlıklı pencere öğesi çizin.

**GX_STYLE_BORDER_MASK**
  - Değer: 0x0000000f
  - Açıklama: Pencere öğesi stili üyesinin yalnızca stil alanlarını test etmek için kullanılan değeri maskeleme.

**GX_STYLE_TRANSPARENT**
  - Değer: 0x10000000
  - Açıklama: En azından kısmen saydam bir pencere öğesi oluşturun. Bu stil, pencere öğesi arka planı olarak yarı saydam bir piksel haritası çizen pencere öğeleri de dahil olmak üzere bir pencere öğesi kendisini tamamen opak çizmezken kullanılmalıdır. Bu stil bayrağı GUIX'e pencere öğesi arka plan alanı yenilemek için pencere öğesi üst öğesi çizilecek konusunda bilgi sağlar.

**GX_STYLE_DRAW_SELECTED**
  - Değer: 0x20000000
  - Açıklama: Pencere öğesi seçilen durum renkleri ve yazı tipleri kullanılarak çizilmelidir. Farklı pencere öğesi türleri DRAW_SELECTED pencere öğesi seçili olduğunu belirtmek için farklı şekillerde DRAW_SELECTED stili kullanır.

**GX_STYLE_ENABLED**
  - Değer: 0x40000000
  - Açıklama: Pencere öğelerini etkin olarak işaretle, bu pencere öğesi kullanıcı giriş olaylarını kabul eder ve çıkış sinyalleri oluşturur.
  
**GX_STYLE_DYNAMICALLY_ALLOCATED**
  - Değer: 0x80000000
  - Açıklama: Pencere öğesi oluşturulduğunda gx_system_memory_allocator hizmeti kullanılarak pencere öğesi denetim bloğu belleğinin dinamik olarak serbest bırakıldığından ve pencere öğesi yok edilirse denetim bloğu belleğinin serbest bırakıldığından gösterir.

**GX_STYLE_USE_LOCAL_ALPHA**
  - Değer: 0x01000000
  - Açıklama: GUIX çizim işlevlerine pencere öğesi çizimini gerçekleştirirken yerel pencere öğesi alfa değerini kullanma talimatı verir. Bu bayrak normalde iç GUIX mantığı tarafından pencere öğesi soluk görüntü animasyonları uygulamak için kullanılır.


__***Metin Hizalama Stilleri (metin çizen tüm pencere öğelerine uygulanan stiller):***__

**GX_STYLE_TEXT_LEFT**
  - Değer: 0x00001000
  - Açıklama: Metin, pencere öğesi istemci alanı içinde sola hizalanmış şekilde çizilir.

**GX_STYLE_TEXT_RIGHT** 
  - Değer: 0x00002000
  - Açıklama: Metin, pencere öğesi istemci alanı içinde sağa hizalanmış şekilde çizilir.

**GX_STYLE_TEXT_CENTER**
  - Değer: 0x00004000
  - Açıklama: Metin, pencere öğesi istemci alanı içinde orta hizalı olarak çizilir.

**GX_STYLE_TEXT_COPY**
  - Değer: 0x00008000
  - Açıklama: Varsayılan olarak, metin çizen pencere öğeleri yalnızca uygulama tarafından geçirilen metnin işaretçisini kullanır. Dize tablosunda tanımlanan statik olarak tanımlanmış metinler için, pencere öğesi tarafından atanan metnin özel bir kopyasının olması için bir neden yoktur. Ancak, bir pencere öğesine atanan metin sprint() veya gx_utility_ltoa gibi işlevler kullanılarak dinamik olarak oluşturulursa, pencere öğesine atanan herhangi bir metnin kendi özel kopyasını tutması genellikle kullanışlı olur. Bu, uygulamanın metin dizesini tanımlarken otomatik veya geçici değişkenleri kullanmalarını sağlar. Aksi takdirde uygulamanın dinamik olarak tanımlanmış metin kullanan her metin pencere öğesi için statik olarak tanımlanmış karakter dizileri tanımlaması gerekir. Bu stil bayrağını ayarlayıp pencere öğesi gx_system_memory_allocator dizenin özel kopyasını tutmak için gereken bellek bloğuna dinamik olarak ayırmak için gx_system_memory_allocator işlevini kullanır. Bu nedenle bu stil bayrağının kullanımı, uygulamanın işlev ve işlev memory_allocator memory_deallocator gerekir. GX_STYLE_TEXT_COPY, ayardan sonra temizilemeyecektir ve bunu yapmak öngörülemeyen sonuçlara neden olur.

__***Düğme Stilleri (yalnızca GUIX düğme pencere öğesi türleri için geçerlidir):***__

**GX_STYLE_BUTTON_PUSHED**
  - Değer 0x00000010
  - Açıklama: Düğmenin iletili veya seçili durumda olduğunu gösterir.

**GX_STYLE_BUTTON_TOGGLE**
  - Değer 0x00000020
  - Açıklama: Her tıklama olayında düğmenin durumu, ertelenmiş ve geri alındı olarak değiştirilir. Bu stil genellikle "onay kutusu" stil düğmeleriyle kullanılır.

**GX_STYLE_BUTTON_RADIO**
  - Değer 0x00000040
  - Açıklama: Bu stil düğmenin dışlamalı olacağını ve seçildiğinde tüm düğme eşleri seçiminin kaldır olacağını gösterir. Bu stil genellikle "radyo düğmesi" stil düğmeleriyle kullanılır.

**GX_STYLE_BUTTON_EVENT_ON_PUSH**
  - Değer: 0x00000080
  - Açıklama: Düğmenin ilk kez birlikte bir tıklama olayı oluştur olduğunu gösterir. Varsayılan işlem, düğme serbest bırakıldığında bir tıklama olayı oluşturmaktır.

**GX_STYLE_BUTTON_REPEAT**
  - Değer 0x00000100
  - Açıklama: Düğme gönderme durumuna geldiğinde düğmenin üst öğeye yinelenen tıklama olayları göndermesi gerektiğini gösterir.

__***Liste Stilleri (yalnızca GUIX listesi pencere öğesi türleri için geçerlidir):***__

**GX_STYLE_CENTER_SELECTED** 
  - Değer: 0x00000010
  - Açıklama: Ayrılmış

**GX_STYLE_WRAP**
  - Değer 0x00000020
  - Açıklama: Liste, başlangıç veya bitiş listesi dizininin sonuna sürüklendikten veya kaydırıldıklarından alt altları baştan sona kaydırıldı.

**GX_STYLE_FLICKABLE**
  - Değer: 0x00000040
  - Açıklama: Ayrılmış

__***Piksel Haritası Düğmesi ve Simge Düğmesi Stilleri:***__

**GX_STYLE_HALIGN_CENTER**
  - Değer: 0x00010000
  - Açıklama: Piksel haritası düğmesinin, yatay eksende düğme sınırı içinde orta hizalanması gerekir.

**GX_STYLE_HALIGN_LEFT**
  - Değer: 0x00020000
  - Açıklama: Düğme piksel haritası, yatay eksende düğme sınırı içinde hizalanmış şekilde bırakıldığında.

**GX_STYLE_HALIGN_RIGHT**
  - Değer 0x00040000
  - Açıklama: Düğme piksel haritası, yatay eksende düğme sınırı içinde sağa hizalanmış olması gerekir.

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