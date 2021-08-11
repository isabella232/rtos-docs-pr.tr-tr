---
title: Ek F-Gux RTOS bağlama hizmetleri
description: GUX RTOS bağlama hizmetleri hakkında bilgi edinin.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 7928e1781be03969de25901ebbe728e6554e96befb59c860f4ea53663c28932d
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116784606"
---
# <a name="appendix-f---guix-rtos-binding-services"></a>Ek F-Gux RTOS bağlama hizmetleri

GUX, temel alınan RTOS tarafından sağlanan iş parçacığı veya görev Hizmetleri, mutex, olay kuyruğu ve zamanlama Hizmetleri gerektirir. Varsayılan olarak Gux, bu hizmetleri sağlamak için ThreadX gerçek zamanlı işletim sistemini kullanacak şekilde yapılandırılmıştır. Farklı bir işletim sistemine Gux bağlantı noktası için, geliştirici, ThreadX bağımlılıklarını kaldırmak için GX_DISABLE_THREADX_BINDING ön işlemci yönergesini tanımlamalıdır ve Gux kitaplığını yeniden derlemelidir. Ayrıca, geliştiricinin aşağıdaki makro tanımlarını ve destekleyici işlevleri sağlaması gerekir. Bu makro tanımlarının örnekleri ve destekleyici işlevler, örnek bir genel RTO 'lar tümleştirmesi sağlayan gx_system_rtos_bind. h ve gx_system_rtos_bind. c dosyalarında bulunabilir.

Sistem tümleştirme makroları:

**GX_RTOS_BINDING_INITIALIZE**

Bu makro sistem başlatma sırasında çağrılır. Bu makro, kullanılmadan önce RTO 'lar sistem hizmetlerinizi veya RTO 'lar kaynaklarınızı hazırlamak için gereken herhangi bir işlevi çağırmak üzere tanımlanmalıdır. Bu, Gux 'in kullanacağı RTO 'lar kaynaklarını hazırlamak için bağlamanın fırsatına sahiptir.

**GX_SYSTEM_THREAD_START**

Bu makro, Gux görevi veya iş parçacığının yürütülmeye başlaması gerektiğinde çağrılır. Bu makro, çalışan Gux iş parçacığını başlatacak bir işlevi çağırmak için tanımlanmalıdır. GUX iş parçacığına giriş noktası çağrılan işleve geçirilir. Çağrılan işlevin imzası olmalıdır

**UINT *function_name*(void (thread_entry_point) (void));**

Bu işlev, iş parçacığı başarıyla başlatılmışsa veya GX_FAILURE GX_SUCCESS döndürmelidir.

**GX_EVENT_PUSH**

Bu makro, bir olayı Gux tarafından kullanılan FıFO olay kuyruğuna göndermek için çağrılır. Yeni bir RTOS 'a taşıma yaparken, bu olay kuyruğunu iş parçacığı güvenli bir şekilde uygulamak sizin sorumluluğunuzdadır. GX_EVENT yapılar bu kuyruğa kopyalanmalıdır ve bu kuyruktan kopyalanmalıdır, yani Gux olayları olay üreticisi görünümünden otomatik değişkenler olduğundan, GX_EVENT işaretçilerin bir sırası çalışmaz. Bu makro tarafından çağrılan işlevin imzası şu olmalıdır:

**UINT *function_name* (GX_EVENT *event_ptr);**

Olay olay kuyruğuna itilse, bu işlev GX_SUCCESS döndürmelidir, aksi takdirde GX_FAILURE döndürmelidir.

**GX_EVENT_POP**

Bu makro, GUIX olay kuyruğundan baş (en eski) olayı kaldırmak ve istenen konuma kopyalamak için çağrılır. Bu işlev, şu anda olay kuyruğunda hiçbir olay yoksa bir olayı bloke edebilir veya bekleyebilir. Bu makro tarafından çağrılan işlevin imzası olmalıdır

UINT function_name (GX_EVENT * put_event, GX_BOOL bekle)

Wait parametresi = = GX_TRUE, işlev bir olay sağlanana kadar döndürülmemelidir. Wait parametresi GX_FALSE ise, işlev hemen veya bir olay olmadan hemen döndürmelidir.

Kuyruktan bir olay alınırsa, put_event konumuna kopyalanması ve dönüş durumunun GX_SUCCESS olması gerekir. Aksi takdirde, dönüş durumu GX_FAILURE olmalıdır.

**GX_EVENT_FOLD**

Bu makro, bir olayı FıFO olay kuyruğuna katlamak için GUıDX tarafından çağrılır. Bir olayın katlaması, aynı türde bir olay kuyrukta zaten mevcutsa, bu girişin yeni olayın yükünü içerecek şekilde güncelleştirilmesi anlamına gelir. Kuyrukta aynı türden mevcut bir olay bulunamazsa, sıraya yeni bir olay gönderilir. 

Olay katlama özelliğini uygulayamayacağı bağlamalar için, GX_EVENT_PUSH çağırmak kabul edilebilir.

**GX_TIMER_START**

Bu makro, GUıDX ' in dönemsel süreölçer girişi alması gerektiğinde çağrılır. Bu makro alt düzey RTOS dönemsel Zamanlayıcı hizmetini başlatan bir hizmeti çağırmalıdır. RTOS Zamanlayıcı hizmeti kolayca durdurulup başlayamadığında, bu hizmeti her zaman çalışır durumda bırakmak kabul edilebilir ancak daha az verimlidir.

Düşük düzey RTOS Zamanlayıcı hizmetinin süresi dolduğunda, bağlama Gux sistem işlevini çağırmalıdır _gx_system_timer_expiration (0); Bu işlevi düzenli aralıklarla çağırmak, üst düzey Gux Zamanlayıcı pencere öğesi Zamanlayıcı hizmetlerinin hangi sürücülerindedir.

**GX_TIMER_STOP**

Bu makro, GUIX 'in artık düzenli bir zamanlayıcıya ihtiyaç duymuyorsa çağrılır (yani, etkin bir Gux zamanlayıcının çalışması yoktur). RTOS Zamanlayıcı hizmeti kolayca durdurulup başlayamıyorsa, bu hizmeti her zaman çalışır durumda bırakmak ve hiçbir şey yapmak için bu makroyu tanımlamak kabul edilebilir ancak daha az verimlidir.

**GX_SYSTEM_MUTEX_LOCK**

Bu makro, kritik kod bölümleri sırasında, diğer bir görevin ortak veri yapılarını önceden oluşmasını ve değiştirmesini engellemek için, büyük olasılıkla bozulmaya neden olabilir. Bu makro uygun RTOS kaynak kilitleme hizmetini uygulayan bir işlev çağırmalıdır.

GUX iş parçacığı dışında hiçbir şekilde Gux API hizmeti kullanmıyorsanız, hiçbir şey yapmak için bu makroyu tanımlayabilirsiniz.

**GX_SYSTEM_MUTEX_UNLOCK**

Bu makro, kritik kod bölümlerinin sonunda çağrılır ve uygun temel alınan RTOS hizmetini kullanarak Gux kaynağının kilidini açmanız gerekir. GUX iş parçacığı dışında hiçbir şekilde Gux API hizmeti kullanmıyorsanız, hiçbir şey yapmak için bu makroyu tanımlayabilirsiniz.

**GX_SYSTEM_TIME_GET**

Bu makro, genellikle sistem başlangıcından bu yana gerçekleşen alt düzey Zamanlayıcı kesmelerinin sayısı olan "sistem işaretleri" olan geçerli sistem saatini döndüren bir işlevi çağırmalıdır. Bu hizmet, dokunma girişi hareketleri için dokunma olayı kalem hızını hesaplamak için kullanılır. Bu makro tarafından çağrılan işlevin imzası şu olmalıdır:

**ULONG *function_name*(VOID);**

**GX_CURRENT_THREAD**

Bu makro, yürütülmekte olan iş parçacığını belirlemek için çağrılır. Bu makro tarafından çağrılan hizmetin bir void * döndürmesi gerekir, yani işletim sisteminiz tarafından geçerli yürütme iş parçacığını tanımlamak için kullanılan veri türünün GUX olarak döndürülmek üzere void * olarak dönüştürülmesi gerekir.

Bir genel RTOS bağlamasının tamamı bir örneği, dosyalanmış gx_system_rtos_bind. h ve gx_system_rtos_bind. c ' de uygulanır