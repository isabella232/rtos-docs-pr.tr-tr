---
title: Bölüm 3-USBX cihaz yığınının Işlevsel bileşenleri
description: Bu bölüm, işlevsel bir perspektiften yüksek performanslı bir USBX Embedded USB cihaz yığınının açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: dc57f3e0f6aa6731f4aaedee8169313ca7276cff
ms.sourcegitcommit: 1aeca2f91960856d8cc24fef65f909639e527599
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/31/2021
ms.locfileid: "106082209"
---
# <a name="chapter-3---functional-components-of-usbx-device-stack"></a>Bölüm 3-USBX cihaz yığınının Işlevsel bileşenleri

Bu bölüm, işlevsel bir perspektiften yüksek performanslı bir USBX Embedded USB cihaz yığınının açıklamasını içerir.

## <a name="execution-overview"></a>Yürütmeye genel bakış

Cihaz için USBX birkaç bileşenden oluşur.

- Başlatma
- Uygulama arabirimi çağrıları
- Cihaz sınıfları
- USB cihaz yığını
- Cihaz denetleyicisi
- VBUS Yöneticisi

Aşağıdaki diyagramda, USBX cihaz yığını gösterilmektedir.

![USBX cihaz yığını](media/usbx-device-stack/usbx-device-stack.png)

### <a name="initialization"></a>Başlatma

USBX ' i etkinleştirmek için ***ux_system_initialize*** işlevi çağrılmalıdır. Bu işlev, USBX bellek kaynaklarını başlatır.

USBX cihaz tesislerini etkinleştirmek için ***ux_device_stack_initialize*** işlevi çağrılmalıdır. Bu işlev, USBX cihaz yığını tarafından kullanılan ve ThreadX iş parçacıkları, zaman uyumu sağlayıcılar ve semaforlar gibi tüm kaynakları başlatacak.

Bu, USB cihaz denetleyicisini ve bir veya daha fazla USB sınıfını etkinleştirmek için uygulama başlatma 'ya kadar sürer. USB ana bilgisayar tarafının aksine, cihaz tarafında herhangi bir anda yalnızca bir USB denetleyici sürücüsü çalışıyor olabilir. Sınıflar yığına kaydedildiğinde ve cihaz denetleyicisi başlatma işlevi çağrıldığında, veri yolu etkin olur ve yığın veri yolu sıfırlama ve konak listeleme komutlarına yanıt gönderir.

### <a name="application-interface-calls"></a>Uygulama arabirimi çağrıları

USBX içinde iki API düzeyi vardır.

- USB cihaz yığını API 'Leri
- USB cihaz sınıfı API 'Leri

Normalde, bir USBX uygulamasının USB cihaz yığını API 'Lerinden herhangi birini çağırması gerekmez. Çoğu uygulama yalnızca USB sınıfı API 'Lerine erişir.

### <a name="usb-device-stack-apis"></a>USB cihaz yığını API 'Leri

Cihaz yığını API 'Leri, sınıflar ve cihaz çerçevesi gibi USBX cihaz bileşenlerinin kaydı yapmaktan sorumludur.

### <a name="usb-device-class-apis"></a>USB cihaz sınıfı API 'Leri

Sınıf API 'Leri her USB sınıfına çok özeldir. USB sınıfları için ortak API 'lerin çoğu, bir cihazı açma/kapatma ve bir cihazdan okuma ve bir cihaza yazma gibi hizmetleri sağlamıştır. API 'Ler ana bilgisayar tarafına benzer şekilde benzerdir.

## <a name="device-framework"></a>Cihaz çerçevesi

USB cihaz tarafı, cihaz çerçevesinin tanımından sorumludur. Cihaz çerçevesi, aşağıdaki bölümlerde açıklandığı gibi üç kategoriye ayrılmıştır.

### <a name="definition-of-the-components-of-the-device-framework"></a>Cihaz çerçevesi bileşenlerinin tanımı

Cihaz çerçevesinin her bileşeninin tanımı, cihazın doğası ve cihaz tarafından kullanılan kaynaklar ile ilgilidir. Ana kategoriler aşağıda verilmiştir.

- Cihaz tanımlayıcısı
- Yapılandırma tanımlayıcısı
- Arabirim tanımlayıcısı
- Uç nokta tanımlayıcısı

USBX hem yüksek hem de tam hızda cihaz bileşeni tanımını destekler (düşük hız tam hızda aynı şekilde kabul edilir). Bu, cihazın yüksek hızda veya tam hızlı ana bilgisayara bağlıyken farklı şekilde çalışmasını sağlar. Tipik farklılıklar, her uç noktanın boyutudur ve cihaz tarafından tüketilen güçlerdir.

Cihaz bileşeninin tanımı, USB belirtimini izleyen bir bayt dizesi biçimini alır. Tanım bitişik ve çerçevenin bellekte temsil edildiği sıra, numaralandırma sırasında ana bilgisayara döndürülen ile aynı olacaktır.

Yüksek hızlı USB flash disk için bir cihaz çerçevesi örneği aşağıda verilmiştir.

```c
#define DEVICE_FRAMEWORK_LENGTH_HIGH_SPEED 60
UCHAR device_framework_high_speed[] = {
    /* Device descriptor */
    0x12, 0x01, 0x00, 0x02, 0x00, 0x00, 0x00, 0x40, 0x0a, 0x07, 0x25, 0x40, 0x01, 0x00, 0x01, 0x02, 0x03, 0x01,

    /* Device qualifier descriptor */
    0x0a, 0x06, 0x00, 0x02, 0x00, 0x00, 0x00, 0x40, 0x01, 0x00,

    /* Configuration descriptor */
    0x09, 0x02, 0x20, 0x00, 0x01, 0x01, 0x00, 0xc0, 0x32,

    /* Interface descriptor */
    0x09, 0x04, 0x00, 0x00, 0x02, 0x08, 0x06, 0x50, 0x00,

    /* Endpoint descriptor (Bulk Out) */
    0x07, 0x05, 0x01, 0x02, 0x00, 0x02, 0x00,

    /* Endpoint descriptor (Bulk In) */
    0x07, 0x05, 0x82, 0x02, 0x00, 0x02, 0x00
};
```

### <a name="definition-of-the-strings-of-the-device-framework"></a>Cihaz çerçevesi dizelerinin tanımı

Dizeler bir cihazda isteğe bağlıdır. Bu kişilerin amacı, USB konağının cihaz üreticisi, ürün adı ve Unicode dizeleri aracılığıyla düzeltme numarası hakkında bilgi sahibi sağlamaktır.

Ana dizeler, cihaz tanımlayıcılarında gömülü olan dizinlerdir. Ek dizeler dizinleri tek tek arabirimlere katıştırılabilir.

Yukarıdaki cihaz çerçevesinin cihaz tanımlayıcısına eklenmiş üç dize dizini olduğunu varsayarsak, dize çerçevesi tanımı bu örnek koda benzeyebilir.

```c
/* String Device Framework:
    Byte 0 and 1: Word containing the language ID: 0x0904 for US
    Byte 2 : Byte containing the index of the descriptor
    Byte 3 : Byte containing the length of the descriptor string
*/

#define STRING_FRAMEWORK_LENGTH 38
UCHAR string_framework[] = {
    /* Manufacturer string descriptor: Index 1 */
    0x09, 0x04, 0x01, 0x0c,
    0x45, 0x78, 0x70, 0x72, 0x65, 0x73, 0x20, 0x4c,
    0x6f, 0x67, 0x69, 0x63,

    /* Product string descriptor: Index 2 */
    0x09, 0x04, 0x02, 0x0c,
    0x4D, 0x4C, 0x36, 0x39, 0x36, 0x35, 0x30, 0x30,
    0x20, 0x53, 0x44, 0x4B,

    /* Serial Number string descriptor: Index 3 */
    0x09, 0x04, 0x03, 0x04,
    0x30, 0x30, 0x30, 0x31
};
```

Her hız için farklı dizelerin kullanılması gerekiyorsa, dizinlerin hız belirsiz olduğu için farklı dizinlerin kullanılması gerekir.

Dizenin kodlaması UNICODE tabanlıdır. UNICODE kodlama standardı hakkında daha fazla bilgi için aşağıdaki yayına başvurun:

*Unicode standart, dünya çapındaki karakter kodlaması, sürüm 1., birimler 1 ve 2, Unicode konsorsiyum, Addison-Wesley yayımlama şirketi, okuma MA.*

### <a name="definition-of-the-languages-supported-by-the-device-for-each-string"></a>Her dize için cihaz tarafından desteklenen dillerin tanımı

USBX 'in varsayılan değer olan Ingilizce olmasına rağmen birden çok dili destekleme yeteneği vardır. Dize tanımlayıcıları için her dilin tanımı, aşağıdaki şekilde tanımlanan bir dil tanımı dizisi biçimindedir.

```c
#define LANGUAGE_ID_FRAMEWORK_LENGTH 2
UCHAR language_id_framework[] = {
    /* English. */
    0x09, 0x04
};
```

Ek dilleri desteklemek için, varsayılan Ingilizce kodundan sonra dil kodu çift baytlı tanımını eklemeniz yeterlidir. Dil kodu belge içinde Microsoft tarafından tanımlandı.

*Windows 95 ve Windows NT, Nadine Kano, Microsoft Press, Redmond WA için uluslararası yazılım geliştirme*

## <a name="vbus-manager"></a>VBUS Yöneticisi

Çoğu USB cihaz tasarımlarında, VBUS, USB cihaz çekirdeği 'nin bir parçası değildir, bunun yerine çizgi sinyalini izleyen bir harici GıO 'a bağlanır.

Sonuç olarak, VBUS 'ın cihaz denetleyicisi sürücüsünden ayrı olarak yönetilmesi gerekir.

Bu, cihaz denetleyicisine VBUS GÇ adresini sağlamak için uygulamaya çalışır. Cihaz denetleyicisi başlatılmadan önce VBUS başlatılmalıdır.

Sanal veri izleme platformu belirtimine bağlı olarak, VBUS GÇ başlatıldıktan sonra denetleyici sürücüsünün VBUS sinyalleri işlemesini sağlamak mümkündür veya bu mümkün değilse, uygulamanın VBUS işleme kodunu sağlaması gerekir.

Uygulama VBUS 'ı kendisine göre işlemesini istiyorsa, tek gereksinimi, bir cihazın ayıklandığını algıladığında işlevi ***ux_device_stack_disconnect*** çağırmalıdır. Bir cihaz takıldığında denetleyiciyi bilgilendirmek gerekli değildir çünkü veri yolu SıFıRLAMA onayı/kaldırma sinyali algılandığında denetleyici uyandırır.
