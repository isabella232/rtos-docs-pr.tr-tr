---
title: Ek H - GUIX Build-Time Yapılandırma bayrakları
description: GUIX derleme zamanı yapılandırma bayrakları hakkında bilgi.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 2b48491e3c601aeb68ecef00fd0f25d93cda6e64
ms.sourcegitcommit: 62cfdf02628530807f4d9c390d6ab623e2973fee
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/05/2021
ms.locfileid: "115177771"
---
# <a name="appendix-h---guix-build-time-configuration-flags"></a>Ek H - GUIX Build-Time Yapılandırma bayrakları

GUIX, çeşitli koşullu derleme seçeneklerini ve yapılandırma değerlerini destekler. Bu koşullu ve yapılandırma değerleri için varsayılan ayar, gx_user.h üst bilgi dosyanıza veya derleyici komut satırınıza önceden tanımlayarak geçersiz kılınabilir.

**GX_DISABLE_THREADX_BINDING**
- Varsayılan: Tanımsız
- Açıklama: Bu koşullu, varsayılan ThreadX RTOS bağlamasını devre dışı bırakmak için kullanılabilir. GUIX'i ThreadX dışında bir RTOS ile çalıştırmak #define GX_DISABLE_THREADX_BINDING kendi RTOS bağlama hizmetlerinizi sağlamanız gerekir.

GX_SYSTEM_TIMER_MS
- Varsayılan: 20
- Açıklama: Bu değer, istenen GUIX zamanlayıcı aralığını veya duyarlığı tanımlar.

TX_TIMER_TICKS_PER_SECOND
- Varsayılan: 100
- Açıklama: Bu değer, TX zamanlayıcı kesme sıklığı sayısını tanımlar. Varsayılan ThreadX aralık süreölçeri 10 ms olduğu için bu değer varsayılan olarak 100-Frequency değerini kullanır.

GX_DISABLE_MULTITHREAD_SUPPORT
- Varsayılan: Tanımlanmadı
- Açıklama: Bu derleme zamanı koşullu ayarı, GUIX API'sini eşzamanlı olarak çağrıp birden çok iş parçacığı için GUIX API desteğini devre dışı bırakmak için kullanılabilir. GUIX API'sini yalnızca bir uygulama iş parçacığı kullanırsa, kritik kod bölümlerinin korunmasıyla ilişkili sistem yükünü azaltmak için bu bayrağı tanımlamanız gerekir.

GX_DISABLE_UTF8_SUPPORT
- Varsayılan: Tanımlanmadı.
- Açıklama: Bu derleme zamanı koşullu, UTF8 biçimli dize kodlaması için GUIX iç desteğini kaldırmak için kullanılabilir. Uygulamanıza yalnızca M- 0xff karakter değerleri kullanıyorsanız, bu #define UTF8 biçim dizesi kodlamasını desteklemeyle ilişkili kod boyutunu ve ek yükünü azaltır.

GX_DISABLE_ARC_DRAWING_SUPPORT
- Varsayılan: Tanımlanmadı.
- Açıklama: Bu koşul; arc-drawing işlevleri daire, yay, pasta ve GX_DISPLAY desteği kaldırılarak GUIX kitaplığı kod boyutunu ve yapı boyutunu azaltmak için kullanılabilir. Bu işlevler varsayılan GUIX pencere öğesi kümesi tarafından gerekli değildir.

GX_DISABLE_SOFTWARE_DECODER_SUPPORT
- Varsayılan: Tanımlanmadı.
- Açıklama: Bu koşullu, GUIX kitaplık çalışma zamanı jpeg ve png yazılım kod çözücü desteğini kaldırmak için tanımlanabilir. Uygulamanız jpg veya png dosyalarının çalışma zamanı kodunu çözmesini gerektirmezse, yani uygulamanız Studio tarafından üretilen RAW biçimli piksel haritalarını kullanmaz ve bir dış dosya sisteminden görüntü dosyalarını okumazsa GUIX kitaplığı ayak izini azaltmak için bu #define'i açabilirsiniz.

GX_DISABLE_BINARY_RESOURCE_SUPPORT
- Varsayılan: Tanımlanmadı
- Açıklama: Bu koşullu, ikili kaynak verilerini yüklemeye ilişkin GUIX kitaplık desteğini kaldırmak için kullanılabilir. İkili kaynaklar, kaynak verilerini GUIX uygulamanıza bağlama çalışma zamanı yapmak için kullanılabilir. Yalnızca C kaynak kodu biçimi kaynak dosyalarını kullanıyorsanız GUIX kitaplığı ayak izinizi azaltmak için bu koşullu kodu tanımlayabilirsiniz.

GX_DISABLE_BRUSH_ALPHA_SUPPORT
- Varsayılan: Tanımlanmadı.
- Açıklama: GUIX, 16 bpp ve daha yüksek renk derinliğinde çalıştırarak isteğe bağlı olarak çizim bağlam fırçaları tarafından tanımlanan alfa değerine sahip ark olmayan grafikler, piksel haritaları ve yazı tiplerini çizmeyi destekler. Bu çizim modunu desteklemek küçük bir çalışma zamanı ek yükü ve kitaplık ayak izi artışına neden olur ve alfa karıştırma çizim desteğine gerek yoksa bu bayrak tanımlayarak ortadan kaldırabilirsiniz. Alfa kanalı, diğer addan koruma yazı tipleri ve diğer diğer addan koruma çizim modlarına sahip piksel haritalarının bu koşullu ayardan bağımsız olarak hala destek altında olduğunu unutmayın.

GX_DISABLE_THREADX_TIMER_SOURCE
- Varsayılan: Tanımlanmadı.
- Açıklama: Bu koşullu, ThreadX zamanlayıcı kaynağını devre dışı bırakmak için kullanılabilir. Farklı bir GX_DISABLE_THREADX_TIMER_SOURCE kullanmak istediğiniz zamanlayıcısı tanımlamanız gerekir.

GX_REPEAT_BUTTON_INITIAL_TICS
- Varsayılan: 10.
- Açıklama: Bir düğmenin stil GX_STYLE_BUTTON_REPEAT, bu değer yinelenen olay göndermeye başlamadan önce düğmenin ne kadar GX_EVENT_CLICKED tanımlar.

GX_MAX_QUEUE_EVENTS
- Varsayılan: 48.
- Açıklama: GUIX olay kuyruğu boyutunu olay yapısı girişlerinin birimlerinde tanımlar. Olay kuyruğu taşması durumunda kuyruğa iletilen olaylar atılır ve GX_SYSTEM_ERROR işlevi gx_system_event_send() işlevi tarafından döndürülür.

GX_MAX_DIRTY_AREAS
- Varsayılan: 64.
- Açıklama: Bir tuval tarafından korunan en fazla benzersiz kirli liste girdisi sayısını tanımlar. Kirli liste taştığında GUIX varsayılan olarak tuval kök penceresini kirli olarak işaretler ve bu da tek tek alt pencere öğelerini çizmekten daha az verimlidir.

GX_MAX_CONTEXT_NESTING
- Varsayılan: 8.
- Açıklama: Çizim bağlam yığınının en büyük iç içe yerleştirmesini tanımlar. Bu, kullanıcı arabirimi tanımında üst/alt/alt/alt pencere öğelerinin iç içe yerleştirme üst öğelerine eşdeğerdir.

GX_MAX_INPUT_CAPTURE_NESTING
- Varsayılan: 4.
- Açıklama: Kullanıcı girişini (fare ve klavye) yakalayan pencere öğelerinin listesini korumak için kullanılan yığının boyutunu tanımlar.

GX_SYSTEM_THREAD_PRIORITY
- Varsayılan: 16.
- Açıklama: gx_system_initialize() sırasında oluşturulan GUIX iş parçacığının önceliğini tanımlar.

GX_SYSTEM_THREAD_TIMESLICE
- Varsayılan: 10.
- Açıklama: GUIX iş parçacığı zaman çerçevelerini RTOS zamanlayıcı saat işaretlerini bakımından tanımlar. GuiX iş parçacığıyla aynı önceliğe sahip diğer iş parçacıkları tanımlanmışsa, bu değer bu rakip iş parçacıklarına CPU denetimi verilmesi sıklıklarını belirler.

GX_CURSOR_BLINK_INTERVAL
- Varsayılan: 20.
- Açıklama: Metin girişi pencere öğeleri için giriş imlecinin yanıp sönme hızını tanımlar. Bu değer, varsayılan olarak 50 ms olarak tanımlayan GUIX zamanlayıcı tık sayısı bakımındandır, dolayısıyla 20 değeri, giriş imlecinin saniyede bir yanıp söner olduğunu gösterir.

GX_MULTI_LINE_INDEX_CACHE_SIZE
- Varsayılan: 32.
- Açıklama: Çok satırlı metin görünümü ve çok satırlı metin girişi pencere öğeleri tarafından bakımı yapılan liste-başlangıç dizin önbelleğinin boyutunu tanımlar. Bu önbellek, çok satırlı metin pencere öğeleri için hızlı dikey kaydırma gerçekleştirmek için kullanılır. En iyi performans için, önbellek boyutu uygulama tarafından tanımlanan en büyük çok satırlı metin pencere öğesi görünür satır sayısından büyük ayarlanmalıdır. Örneğin, herhangi bir metin pencere öğesi için en çok görünen satırlar 20 satır ise, uygulama 32 önbellek boyutu (varsayılan) tanımlayabilir ve bu da GUIX'in tüm satır başlangıç dizinlerini yeniden hesaplamadan dikey olarak kaydırmaya olanak sağlar.

GX_MULTI_LINE_TEXT_BUTTON_MAX_LINES
- Varsayılan: 4.
- Açıklama: Çok satırlı metin düğmesi denetim bloğu, düğme tarafından görüntülenecek her metin satırına bir işaretçi sağlar. Bu değer, en kötü büyük/küçük harf çok satırlı metin düğmesi için gereken metin işaretçilerinin sayısını belirler.

GX_POLYGON_MAX_EDGE_NUM
- Varsayılan: 10.
- Açıklama: Bu değer GUIX tarafından çizilen en karmaşık çokgeni belirler. Çokgen çizim algoritması, çokgen kenarlarını tanımlamak için gereken çizgileri belirler ve bu tanım, desteklenebilecek en fazla kenar sayısını tanımlar.

GX_NUMERIC_SCROLL_WHEEL_STRING_BUFFER_SIZE
- Varsayılan: 16.
- Açıklama: Bir sayı kaydırma tekerleği için kaydırma tekerleği pencere öğesi tamsayı değerlerini ascii dizelere dönüştürür. Bu değer, atanan tamsayı değerlerini görüntülemek için gereken dizenin maksimum uzunluğunu belirler.

GX_DEFAULT_CIRCULAR_GAUGE_ANIMATION_DELAY
- Varsayılan: 5.
- Açıklama: Son ve geçerli angular konum arasındaki iğne hareketine animasyon ek olarak yapılandırılan döngüsel ölçer güncelleştirmeleri arasındaki GUIX zamanlayıcı tık sayısını (50 ms) tanımlar.

GX_NUMERIC_PROMPT_BUFFER_SIZE
- Varsayılan: 16.
- Açıklama: Sayısal bir istem, istem için atanan tamsayı değerini bir ascii dizesine dönüştürmek için bir arabellek ayırır. Bu tanım, bu karakter arabelleğinin boyutunu tanımlar.

GX_ANIMATION_POOL_SIZE
- Varsayılan: 6.
- Açıklama: GUIX, gx_system_animation_get ve gx_system_animation_free() API'leri kullanılarak animasyon bilgi yapılarının dinamik olarak gx_system_animation_get ve döndürülebilirsiniz. Bu tanım, bu animasyon denetim bloğu havuzunun boyutunu tanımlar.

GX_MOUSE_SUPPORT
- Varsayılan: Tanımlanmadı.
- Açıklama: Bu tanım, fare girişi desteği sağlar. Yazılım faresi, görüntü sürücüsünün fare imlecini çizmesini ve izlemesini gerektirir ve bu da görüntü sürücüsüne ek yük getirir. Bu tanım yalnızca bir farenin (dokunmatik ekran değil) desteklenemeli olduğu zaman tanımlanmalıdır.

GX_HARDWARE_MOUSE_SUPPORT
- Varsayılan: Tanımlanmadı.
- Açıklama: Bu tanım tanımlandığı zaman GUIX görüntü sürücüsü, donanım fare imleci çizim desteğini kullanır. Bu, fare imlecinin altındaki tuval belleğini yakalamak için gereken belleği azaltır ve fare katmanı grafik katmanını destekleyen donanım hedefleri için sistem performansını artırır.

GX_FONT_KERNING_SUPPORT
- Varsayılan: Tanımlanmadı.
- Açıklama: Bu tanım, yazı tipi karakter oluşturma desteğini etkinleştirmek için tanımlanabilir. Yazı tipi karakter aralığı, belirli karakter birleşimleri için karakter aralığını iyiler. Bu destek çalışma zamanı dize çizim işlevlerine küçük miktarda ek yük getirir ve yazı tipi veri yapılarının boyutuna küçük bir miktar ekler.

GX_WIDGET_USER_DATA
- Varsayılan: Tanımlanmadı.
- Açıklama: Tanımlandı ise, bu denetim bloğuna kullanıcı tanımlı bir GX_WIDGET ekler. Bu veri alanı GUIX Studio'nun özellikler görünümü kullanılarak atanabilir. Bu veri alanı GUIX tarafından dahili olarak yoksayılır, ancak uygulama yazılımı tarafından birçok amaçla kullanılabilir.

GUIX_5_4_0_COMPATIBILITY
- Varsayılan: Tanımlanmadı.
- Açıklama: Belirli GUI API'leri, devre dışı bırakılmış metin renkleri desteği eklemek ve sabit nokta eşleşme parametreleri kullanılarak belirli matematik işlevlerinin doğruluğunu artırmak için 5.4.0 yayından sonra değiştirilmiştir. Bu değişiklikler, 5.4.0'dan sonraki GUIX kitaplık yayınlarını önceki sürümlerle uyumsuz hale geldi. Ancak, bu #define'i açık bırakarak, kitaplık API'ler <= 5.4.0 sürümüyle tamamen uyumlu olacak şekilde derlenmiş olabilir. Başka bir ifadeyle, mevcut uygulamalarda en son GUIX kitaplık sürümüyle derlemek için herhangi bir değişiklik gerekmez.

GX_MAX_STRING_LENGTH
- Varsayılan: 102400
- Açıklama: Geçersiz dizeleri test etmek için kullanılan bir dizenin maksimum uzunluğunu tanımlar. Giriş dizesi maksimum dize uzunluğunu aşarsa geçersiz olarak kabul edilir.