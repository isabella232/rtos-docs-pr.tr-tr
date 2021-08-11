---
title: Bölüm 3 - USBX Cihaz Yığınının İşlevsel Bileşenleri
description: Bu bölümde, işlevsel bir perspektiften yüksek performanslı USBX ekli USB cihaz yığınının açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 104badcbf1ec682cd8b09008578ba91768834d694473ecccf59e35637dfd9f3c
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116791366"
---
# <a name="chapter-3---functional-components-of-usbx-device-stack"></a>Bölüm 3 - USBX Cihaz Yığınının İşlevsel Bileşenleri

Bu bölümde, işlevsel bir perspektiften yüksek performanslı USBX ekli USB cihaz yığınının açıklaması yer almaktadır.

## <a name="execution-overview"></a>Yürütmeye Genel Bakış

Cihaz için USBX çeşitli bileşenlerden oluşur.

- Başlatma
- Uygulama arabirimi çağrıları
- Cihaz Sınıfları
- USB Cihaz Yığını
- Cihaz denetleyicisi
- VBUS yöneticisi

Aşağıdaki diyagramda USBX Cihaz yığınını göstermektedir.

![USBX Cihaz Yığını](media/usbx-device-stack/usbx-device-stack.png)

### <a name="initialization"></a>Başlatma

USBX'i etkinleştirmek için işlev ***ux_system_initialize*** çağrılmalı. Bu işlev USBX'in bellek kaynaklarını başlatıyor.

USBX cihaz olanaklarını etkinleştirmek için, ***ux_device_stack_initialize*** çağrılma gerekir. Bu işlev, ThreadX iş parçacıkları, mutex'ler ve semaforlar gibi USBX cihaz yığını tarafından kullanılan tüm kaynakları başlatacak.

USB cihaz denetleyicisini ve bir veya daha fazla USB sınıflarını etkinleştirmek uygulama başlatmaya bağlı olur. USB ana bilgisayar tarafının aksine, cihaz tarafında herhangi bir anda çalışan yalnızca bir USB denetleyici sürücüsü olabilir. Sınıflar yığına kaydedildiklerinde ve cihaz denetleyicilerini başlatma işlevi çağrıldığı zaman, veri sistemi etkindir ve yığın, veri verisi sıfırlama ve konak numaralama komutlarını yanıtlar.

### <a name="application-interface-calls"></a>Uygulama Arabirimi Çağrıları

USBX'te iki API düzeyi vardır.

- USB Cihaz Yığını API'leri
- USB Cihaz Sınıfı API'leri

Normalde, bir USBX uygulamasının USB cihaz yığını API'lerinin herhangi birini çağıran bir uygulama olması gerekir. Çoğu uygulama yalnızca USB Sınıfı API'lerine erişecek.

### <a name="usb-device-stack-apis"></a>USB Cihaz Yığını API'leri

Cihaz yığını API'leri, sınıflar ve cihaz çerçevesi gibi USBX cihaz bileşenlerinin kaydından sorumludur.

### <a name="usb-device-class-apis"></a>USB Cihaz Sınıfı API'leri

Sınıf API'leri her USB sınıfına çok özeldir. USB sınıflarının yaygın API'lerinin çoğu, bir cihazı açma/kapatma ve cihazdan okuma ve yazma gibi hizmetler sağladı. API'ler doğası gereği konak tarafına benzer.

## <a name="device-framework"></a>Cihaz Çerçevesi

USB cihaz tarafı, cihaz çerçevesinin tanımından sorumludur. Cihaz çerçevesi aşağıdaki bölümlerde açıklandığı gibi üç kategoriye ayrılır.

### <a name="definition-of-the-components-of-the-device-framework"></a>Cihaz Çerçevesi Bileşenlerinin Tanımı

Cihaz çerçevesinin her bir bileşeninin tanımı, cihazın doğası ve cihaz tarafından kullanılan kaynaklarla ilgilidir. Ana kategoriler aşağıda ve aşağıda ve liste listelerinde ve listelerinde ve listelerinde yer almaktadır.

- Cihaz Tanımlayıcısı
- Yapılandırma Tanımlayıcısı
- Arabirim Tanımlayıcısı
- Uç Nokta Tanımlayıcısı

USBX hem yüksek hem de tam hız için cihaz bileşeni tanımını destekler (düşük hız, tam hızda olduğu gibi kabul edilir). Bu, cihazın yüksek hızlı veya tam hızlı bir ana bilgisayara bağlandığında farklı çalışmasına olanak sağlar. Tipik farklar her uç noktanın boyutu ve cihaz tarafından tüketilen güçtür.

Cihaz bileşeninin tanımı, USB belirtimlerini izleyen bir byte dizesi biçimi alır. Tanım bitişiktir ve çerçevenin bellekte temsil edilen sırası, numaralama sırasında ana bilgisayar için döndürülenle aynı olur.

Aşağıda, yüksek hızlı USB Flash Disk için bir cihaz çerçevesi örneği ve ardından ve bir örnek ve ardından ve bir örnek ve bir usb flash disk ve daha fazla bilgi edinebilirsiniz.

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

### <a name="definition-of-the-strings-of-the-device-framework"></a>Cihaz Çerçevesi Dizelerinin Tanımı

Dizeler bir cihazda isteğe bağlıdır. Bunların amacı, USB ana bilgisayarının Unicode dizeleri aracılığıyla cihazın üreticisi, ürün adı ve düzeltme numarası hakkında bilgi sahibi olduğunu bilmektir.

Ana dizeler, cihaz tanımlayıcılarında gömülü dizinlerdir. Ek dize dizinleri ayrı arabirimlere katıştırabilirsiniz.

Yukarıdaki cihaz çerçevesinin cihaz tanımlayıcısına eklenmiş üç dize dizini olduğunu varsayarak, dize çerçevesi tanımı bu örnek koda benzer olabilir.

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

Her hız için farklı dizeler kullanılmalıdır, dizinler hızdan bağımsız olduğu için farklı dizinler kullanılmalıdır.

Dizenin kodlaması UNICODE tabanlıdır. UNICODE kodlama standardı hakkında daha fazla bilgi için aşağıdaki yayına bakın:

*The Unicode Standard, Worldwide Character Encoding, Version 1., Volumes 1 and 2, The Unicode Consortium, Addison-Wesley Publishing Company, Reading MA.*

### <a name="definition-of-the-languages-supported-by-the-device-for-each-string"></a>Her Dize için Cihaz Tarafından Desteklenen Dillerin Tanımı

VARSAYıLAN dil İngilizce olsa da USBX birden çok dili destekleyene sahip. Dize tanımlayıcıları için her dilin tanımı, aşağıdaki gibi tanımlanan bir dil tanımı dizisi şeklindedir.

```c
#define LANGUAGE_ID_FRAMEWORK_LENGTH 2
UCHAR language_id_framework[] = {
    /* English. */
    0x09, 0x04
};
```

Ek dilleri desteklemek için dil kodunu varsayılan İngilizce kodun ardından çift bayt tanımı eklemeniz gerekir. Dil kodu, belgede Microsoft tarafından tanımlanmıştır.

*Windows 95 ve Windows NT Için Uluslararası Yazılım Geliştirme, Nadine International, Microsoft Press, Redmond WA*

## <a name="vbus-manager"></a>VBUS Yöneticisi

ÇOĞU USB cihaz tasarımında VBUS, USB Cihazı çekirdeğinin parçası değildir, bunun yerine çizgi sinyalini izleyen bir dış GPIO'ya bağlanır.

Sonuç olarak VBUS'nin cihaz denetleyicisi sürücüsünden ayrı olarak yönetilmelidir.

Cihaz denetleyicisine VBUS G/A0 adresini sağlamak uygulamaya bağlı olur. VBUS, cihaz denetleyicisi başlatmadan önce başlatılmış olmalıdır.

VBUS'u izlemek için platform belirtimsine bağlı olarak, VBUS GÇ başlatıldıktan sonra denetleyici sürücüsünün VBUS sinyallerini işlemesine izin verebilirsiniz veya bu mümkün yoksa uygulamanın VBUS'u işlemek için kodu belirtmesi gerekir.

Uygulama VBUS'u tek başına işlemek isterse, tek gereksinimi cihazın ***ayık*** ux_device_stack_disconnect işlevi çağırarak çağrısı yapmaktır. Denetleyici, BUS RESET onaylama/deassert sinyali algılandığında uyandırıldığından, bir cihaz ekildiğinde denetleyiciye bildirmeye gerek yoktur.
