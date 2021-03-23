---
title: Ek H-Gux Build-Time yapılandırma bayrakları
description: GUX derleme zamanı yapılandırma bayrakları hakkında bilgi edinin.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 65095e326bc6809eba6e9472e2d74325351354ca
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826416"
---
# <a name="appendix-h---guix-build-time-configuration-flags"></a>Ek H-Gux Build-Time yapılandırma bayrakları

GUX, çeşitli koşullu derleme seçeneklerini ve yapılandırma değerlerini destekler. Bu Koşullular ve yapılandırma değerlerinin varsayılan ayarı, gx_user. h üstbilgi dosyanızda ya da derleyici komut satırınızla değeri önceden tanımlayarak geçersiz kılınabilir.

**GX_DISABLE_THREADX_BINDING**
- Varsayılan: tanımsız
- Açıklama: Bu koşullu varsayılan ThreadX RTOS bağlamasını devre dışı bırakmak için kullanılabilir. GUX ' i ThreadX dışında bir RTOS ile çalıştırmak istiyorsanız, GX_DISABLE_THREADX_BINDING #define ve kendi RTOS bağlama hizmetlerinizi sağlamanız gerekir.

GX_SYSTEM_TIMER_MS
- Varsayılan: 20
- Açıklama: Bu değer istenen GUıDX Zamanlayıcı aralığını veya duyarlılığını tanımlar.

TX_TIMER_TICKS_PER_SECOND
- Varsayılan: 100
- Açıklama: Bu değer, TX süreölçer kesmesi frequences sayısını tanımlar. Varsayılan ThreadX Interval Zamanlayıcı 10 MS olduğundan, bu değer varsayılan olarak 100-Hz sıklık olur.

GX_SYSTEM_TIMER_TICKS
- Varsayılan: ((GX_SYSTEM_TIMER_MS * TX_TIMER_TICKS_PER_SECOND)/1000)
- Açıklama: Bu değer, Gux Zamanlayıcı çentik başına temel alınan RTOS zamanlayıcı sayısı sayısını tanımlar. Varsayılan değer 2 ' dir; yani Gux Zamanlayıcı aralığı 2 ThreadX Zamanlayıcı kesme aralıkları veya varsayılan olarak 20 MS 'dir.

GX_DISABLE_MULTITHREAD_SUPPORT
- Varsayılan: tanımlı değil
- Açıklama: Bu derleme zamanı koşulu, Gux API 'YI aynı anda çağıran birden çok iş parçacığı için Gux API desteğini devre dışı bırakmak için kullanılabilir. Yalnızca bir uygulama iş parçacığı Gux API 'sini kullanmıyorsa, kritik kod bölümlerinin korunmasıyla ilişkili sistem yükünü azaltmak için bu bayrağı tanımlamanız gerekir.

GX_DISABLE_UTF8_SUPPORT
- Varsayılan: tanımlı değil.
- Açıklama: Bu derleme zamanı koşulu, UTF8 biçim dizesi kodlamasının Gux iç desteğini kaldırmak için kullanılabilir. Uygulamanızda yalnızca bir karakter değerleri kullanıyorsanız, bu #define açmak, UTF8 biçim dizesi kodlamasının desteklenmeyle ilişkili kod boyutunu ve ek yükü azaltır.

GX_DISABLE_ARC_DRAWING_SUPPORT
- Varsayılan: tanımlı değil.
- Açıklama: Bu koşullu, yay çizim işlevlerinin daire, yay, pasta ve elips desteğini kaldırarak Gux kitaplık kodu boyutunu ve GX_DISPLAY yapısı boyutunu azaltmak için kullanılabilir. Bu işlevler varsayılan Gux pencere öğesi kümesi için gerekli değildir.

GX_DISABLE_SOFTWARE_DECODER_SUPPORT
- Varsayılan: tanımlı değil.
- Açıklama: Bu koşullu, Gux Kitaplığı çalışma zamanı JPEG ve PNG yazılım kod çözücüsü desteğini kaldırmak için tanımlanabilir. Uygulamanız jpg veya PNG dosyaları için çalışma zamanı kodu çözme gerektirmiyorsa, uygulamanız Studio tarafından üretilen ham biçim pixelmaps kullanmaz ve bir dış FileSystem 'dan görüntü dosyalarını okumadığından, bu #define açıp Gux kitaplık ayak izini azaltabilirsiniz.

GX_DISABLE_BINARY_RESOURCE_SUPPORT
- Varsayılan: tanımlı değil
- Açıklama: Bu koşullu kaynak verilerini yüklemek için Gux kitaplığı desteğini kaldırmak için bu koşullu kullanılabilir. İkili kaynaklar, GUıDX uygulamanızla kaynak verilerinin çalışma zamanı bağlamasını yapmak için kullanılabilir. Yalnızca C kaynak kodu biçim kaynak dosyalarını kullanıyorsanız, bu koşullu kitaplığı, GUıDX kitaplığı parmak izini azaltmak için tanımlayabilirsiniz.

GX_DISABLE_BRUSH_ALPHA_SUPPORT
- Varsayılan: tanımlı değil.
- Açıklama: 16 BPP ve daha yüksek renk derinliğinde çalışırken, GUIX isteğe bağlı olarak, çizim bağlamı fırçası tarafından tanımlanan bir alfa değeri ile yay olmayan grafikleri, pixelharitaları ve yazı tiplerini çizmeyi destekler. Bu çizim modunu desteklemek, küçük bir çalışma zamanı ek yükü ve kitaplık kaplama artışı sunarak, Alfa karıştırma çizimi desteği gerektirmiyorsa bu bayrak tanımlayarak ortadan kaldırılabilir. Bu koşullu ayardan bağımsız olarak, alfa kanalı, daha fazla diğer ad ve diğer ad ve diğer ad ve diğer ad ve diğer ad ve diğer ad ve diğer adlandırma çizim modları ile

GX_DISABLE_THREADX_TIMER_SOURCE
- Varsayılan: tanımlı değil.
- Açıklama: Bu koşullu, ThreadX Zamanlayıcı kaynağını devre dışı bırakmak için kullanılabilir. Farklı bir Zamanlayıcı kaynağı kullanmak istiyorsanız GX_DISABLE_THREADX_TIMER_SOURCE tanımlamanız gerekir.

GX_REPEAT_BUTTON_INITIAL_TICS
- Varsayılan: 10.
- Açıklama: bir düğmenin stil GX_STYLE_BUTTON_REPEAT varsa, bu değer düğmenin yinelenen GX_EVENT_CLICKED olayları gönderilmeye başlamadan önce bekleyeceği süreyi tanımlar.

GX_MAX_QUEUE_EVENTS
- Varsayılan: 48.
- Açıklama: Gux olay sırasının boyutunu olay yapısı girdileri birimi cinsinden tanımlar. Olay sırası taşarsa, kuyruğa gönderilen olaylar atılır ve GX_SYSTEM_ERROR gx_system_event_send () işlevi tarafından döndürülür.

GX_MAX_DIRTY_AREAS
- Varsayılan: 64.
- Açıklama: bir tuval tarafından korunabilir olan en fazla benzersiz kirli liste girişi sayısını tanımlar. Kirli liste taştığında, Gux varsayılan olarak tuval kök penceresini kirli olarak işaretleyerek, ayrı alt pencere öğeleri çizenden daha az verimlidir.

GX_MAX_CONTEXT_NESTING
- Varsayılan: 8.
- Açıklama: çizim bağlamı yığınının iç içe geçme sayısını tanımlar. Bu, Kullanıcı arabirimi tanımı içindeki üst/alt öğe/alt öğe öğelerinin iç içe geçme değerine eşdeğerdir.

GX_MAX_INPUT_CAPTURE_NESTING
- Varsayılan: 4.
- Açıklama: Kullanıcı girişini yakalayan Pencere öğelerinin listesini korumak için kullanılan yığının boyutunu tanımlar (fare ve klavye).

GX_SYSTEM_THREAD_PRIORITY
- Varsayılan: 16.
- Açıklama: gx_system_initialize () sırasında oluşturulan Gux iş parçacığının önceliğini tanımlar.

GX_SYSTEM_THREAD_TIMESLICE
- Varsayılan: 10.
- Açıklama: RTOS Zamanlayıcı işaretleri açısından Gux iş parçacığı timeslice tanımlar. Diğer iş parçacıkları, Gux iş parçacığıyla aynı önceliğe sahip ise, bu değer, bu rekabet iş parçacıklarının ne sıklıkta CPU denetimi verildiğini belirler.

GX_CURSOR_BLINK_INTERVAL
- Varsayılan: 20.
- Açıklama: giriş imleci metin girişi pencere öğeleri için yanıp sönme hızını tanımlar. Bu değer, varsayılan olarak 50 ms olarak tanımlanmakta olan GUıDX Zamanlayıcı işaretleri açısından, bu nedenle 20 değeri giriş imlecinin saniye başına yanıp sönmesini gösterir.

GX_MULTI_LINE_INDEX_CACHE_SIZE
- Varsayılan: 32.
- Açıklama: çok satırlı metin görünümü ve çok satırlı metin girişi pencere öğeleri tarafından tutulan liste başlangıç dizini önbelleğinin boyutunu tanımlar. Bu önbellek, çok satırlı metin pencere öğelerinin hızlı dikey kaydırmasını gerçekleştirmek için kullanılır. En iyi performansı elde etmek için, önbellek boyutu, uygulama tarafından tanımlanan en büyük çok satırlı metin pencere öğesinin görünür satır sayısından daha büyük ayarlanmalıdır. Örneğin, herhangi bir metin pencere öğesi için en görünür satırlar 20 satırtır, uygulama 32 (varsayılan) önbellek boyutunu tanımlayabilir ve bu da Gux 'in tüm satır başlangıç dizinlerini yeniden hesaplamadan dikey olarak kaymasını sağlar.

GX_MULTI_LINE_TEXT_BUTTON_MAX_LINES
- Varsayılan: 4.
- Açıklama: çok satırlı metin düğmesi denetim bloğu, düğme tarafından gösterilecek her metin satırının işaretçisini tutar. Bu değer, en kötü durum çok satırlı metin düğmesi için gereken metin işaretçilerinin sayısını belirler.

GX_POLYGON_MAX_EDGE_NUM
- Varsayılan: 10.
- Açıklama: Bu değer, GUıDX tarafından çizilemeyen en karmaşık çokgeni belirler. Çokgen çizim algoritması, çokgen kenarlarını tanımlamak için gereken satırları belirler ve bu tanım, desteklenebilir en fazla kenar sayısını tanımlar.

GX_NUMERIC_SCROLL_WHEEL_STRING_BUFFER_SIZE
- Varsayılan: 16.
- Açıklama: bir sayı kaydırma tekerleği Için, kaydırma tekerleği pencere öğesi tamsayı değerlerini ASCII dizelerine dönüştürür. Bu değer, atanan tamsayı değerlerini göstermek için gereken en fazla dize uzunluğunu belirler.

GX_DEFAULT_CIRCULAR_GAUGE_ANIMATION_DELAY
- Varsayılan: 5.
- Açıklama: son ve geçerli angular konumu arasındaki iğne hareketine animasyon uygulamak için yapılandırılmış bir dairesel ölçerin güncelleştirmeleri arasında Gux sayaç işaretleri (50 MS) sayısını tanımlar.

GX_NUMERIC_PROMPT_BUFFER_SIZE
- Varsayılan: 16.
- Açıklama: bir sayısal istem, komut istemine atanan bir tamsayı değerini bir ASCII dizesine dönüştürmek için bir arabellek ayırır. Bu tanım, bu karakter arabelleğinin boyutunu tanımlar.

GX_ANIMATION_POOL_SIZE
- Varsayılan: 6.
- Açıklama: GUıDX, gx_system_animation_get ve gx_system_animation_free () API 'Lerini kullanarak animasyon bilgi yapılarının dinamik olarak ayrılabileceği ve döndürülebilecek bir animasyon havuzu tanımlar. Bu tanım, bu animasyon denetim bloğu havuzunun boyutunu tanımlar.

GX_MOUSE_SUPPORT
- Varsayılan: tanımlı değil.
- Açıklama: Bu tanım fare girişi desteğini sunar. Yazılım faresi, görüntü sürücüsünün görüntü sürücüsüne ek yük ekleyen fare imlecini çizmesini ve izlemesini gerektirir. Bu tanım yalnızca bir fare (dokunmatik ekran değil) desteklenmelidir.

GX_HARDWARE_MOUSE_SUPPORT
- Varsayılan: tanımlı değil.
- Açıklama: Bu tanım tanımlandığında Gux görüntü sürücüsü, donanım fare imleç çizim desteğini kullanır. Bu, fare imlecinin altındaki tuval belleğini yakalamak için gereken belleği azaltır ve bu donanım hedeflerinin bir fare kaplama grafik katmanını desteklediği sistem performansını geliştirir.

GX_FONT_KERNING_SUPPORT
- Varsayılan: tanımlı değil.
- Açıklama: Bu tanım, yazı tipi karakter aralığı desteğini etkinleştirmek için tanımlanabilir. Yazı tipi aralığı, belirli glif birleşimleri için glif aralığını geliştirir. Bu destek, çalışma zamanı dize çizim işlevlerine az miktarda yük ekler ve ayrıca yazı tipi veri yapılarına küçük miktarda boyut ekler.

GX_WIDGET_USER_DATA
- Varsayılan: tanımlı değil.
- Açıklama: tanımlanmışsa, GX_WIDGET denetim bloğuna Kullanıcı tanımlı bir veri alanı ekler. Bu veri alanı, GUıDX Studio içindeki Özellikler Görünümü kullanılarak atanabilir. Bu veri alanı, GUıDX tarafından dahili olarak yok sayılır, ancak uygulama yazılımı tarafından birçok amaçla kullanılabilir.

GUIX_5_4_0_COMPATIBILITY
- Varsayılan: tanımlı değil.
- Açıklama: devre dışı bırakılan metin renkleri için destek eklemek ve sabit noktalı eşleşme parametreleri kullanarak belirli matematik işlevlerinin doğruluğunu artırmak için Release 5.4.0 sonrasında bazı GUI API 'Leri değiştirilmiştir. Bu değişiklikler, 5.4.0 sonrasında Gux kitaplık yayınlarını, önceki sürümlerde uyumsuz hale getirir. Ancak, bu #define etkinleştirerek kitaplık, API 'Lerin en son Gux kitaplığı sürümüyle derlemek için mevcut uygulamalarda hiçbir değişiklik gerekmeyeceği anlamına gelen <= 5.4.0 sürümleriyle tamamen uyumlu olacak şekilde oluşturulabilir.

GX_MAX_STRING_LENGTH
- Varsayılan: 102400
- Açıklama: geçersiz dizeleri test etmek için kullanılan bir dizenin uzunluk üst sınırını tanımlar. Giriş dizesi en fazla dize uzunluğunu aşalıyorsa, geçersiz hale gelir.