---
title: Bölüm 4-USBX cihaz hizmetlerinin açıklaması
description: USBX cihaz hizmetleri hakkında bilgi edinin.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: d4aea7470ba2d9075296164b9d1fb61db4f88523
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104828138"
---
# <a name="description-of-usbx-device-services"></a>USBX cihaz hizmetlerinin açıklaması

### <a name="ux_device_stack_alternate_setting_get"></a>ux_device_stack_alternate_setting_get

Bir arabirim değeri için geçerli alternatif ayarı al

### <a name="prototype"></a>Prototype

```c
UINT ux_device_stack_alternate_setting_get(ULONG interface_value);
```

### <a name="description"></a>Açıklama

Bu işlev, USB ana bilgisayarı tarafından belirli bir arabirim değeri için geçerli alternatif ayarı elde etmek üzere kullanılır. Bir **GET_INTERFACE** isteği alındığında denetleyici sürücü tarafından çağrılır.

### <a name="input-parameter"></a>Giriş parametresi

- **Interface_value** Geçerli alternatif ayarın sorgulandığı arabirim değeri

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) veri aktarımı tamamlandı.
- **UX_ERROR** (0xFF) yanlış arabirim değeri.

### <a name="example"></a>Örnek

```c
ULONG interface_value;
UINT status;

/* The following example illustrates this service. */
status = ux_device_stack_alternate_setting_get(interface_value);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_alternate_setting_set"></a>ux_device_stack_alternate_setting_set

Bir arabirim değeri için geçerli alternatif ayarı ayarla

### <a name="prototype"></a>Prototype

```c
UINT ux_device_stack_alternate_setting_set(
    ULONG interface_value, 
    ULONG alternate_setting_value);
```

### <a name="description"></a>Açıklama

Bu işlev, USB ana bilgisayarı tarafından belirli bir arabirim değeri için geçerli alternatif ayarı ayarlamak üzere kullanılır. Bir **SET_INTERFACE** isteği alındığında denetleyici sürücü tarafından çağrılır. **SET_INTERFACE** tamamlandığında, alternatif ayarların değerleri sınıfa uygulanır.

Cihaz yığını, alternatif ayarın değiştirilmesini yansıtmak için bu arabirime sahip olan sınıfa bir **UX_SLAVE_CLASS_COMMAND_CHANGE** yayımlayacak.

### <a name="parameters"></a>Parametreler

- **interface_value**: geçerli alternatif ayarın ayarlandığı arabirim değeri.
- **alternate_setting_value**: yeni alternatif ayar değeri.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) veri aktarımı tamamlandı.
- **UX_INTERFACE_HANDLE_UNKNOWN** (0x52) hiç arabirim eklenmedi.
- **UX_FUNCTION_NOT_SUPPORTED** (0x54) cihaz yapılandırılmadı.
- **UX_ERROR** (0xFF) yanlış arabirim değeri.

### <a name="example"></a>Örnek

```c
ULONG interface_value;

ULONG alternate_setting_value;

/* The following example illustrates this service. */
status = ux_device_stack_alternate_setting_set(interface_value, alternate_setting_value);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_class_register"></a>ux_device_stack_class_register

Yeni bir USB cihaz sınıfı Kaydet

### <a name="prototype"></a>Prototype

```c
UINT ux_device_stack_class_register(
    UCHAR *class_name,
    UINT (*class_entry_function)(struct UX_SLAVE_CLASS_COMMAND_STRUCT *),
    ULONG configuration_number, 
    ULONG interface_number,  
    VOID *parameter);
```

### <a name="description"></a>Açıklama

Bu işlev, uygulama tarafından yeni bir USB cihaz sınıfı kaydetmek için kullanılır. Bu kayıt, sınıfının bir örneğini değil, bir sınıf kapsayıcısını başlatır. Bir sınıf etkin bir iş parçacığına sahip olmalı ve belirli bir arabirime eklenmelidir.

Bazı sınıflar bir parametre veya parametre listesi bekler. Örneğin, cihaz depolama sınıfı, öykünmeye çalıştığı depolama cihazının geometrisini bekler. Bu nedenle parametre alanı, sınıf gereksinimine bağımlıdır ve sınıf değerleriyle doldurulmuş bir yapı için bir değer veya işaretçi olabilir.

> [!NOTE]
> Class_name C dizesi NULL ile sonlandırılmış olmalı ve bunun uzunluğu (NULL-Sonlandırıcı kendisi olmadan) **UX_MAX_CLASS_NAME_LENGTH** daha büyük olmamalıdır.

### <a name="parameters"></a>Parametreler

- **class_name** Sınıf adı
- **class_entry_function** Sınıfın giriş işlevi.
- **configuration_number** Bu sınıfın iliştirildiği yapılandırma numarası.
- **interface_number** Bu sınıfın iliştirildiği arabirim numarası.
- **parametre** Sınıfa özgü bir parametre listesi işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) sınıf kaydettirildi
- **UX_MEMORY_INSUFFICIENT** (0x12) sınıf tablosunda hiçbir giriş kalmadı.
- **UX_THREAD_ERROR** (0x16) bir sınıf iş parçacığı oluşturamaz.

### <a name="example"></a>Örnek

```c
UINT status;

/* The following example illustrates this service. */

/* Initialize the device storage class. The class is connected with interface 1 */
status = ux_device_stack_class_register(_ux_system_slave_class_storage_name ux_device_class_storage_entry,
    1, 1, (VOID *)&parameter);
```

### <a name="ux_device_stack_class_unregister"></a>ux_device_stack_class_unregister

USB cihaz sınıfının kaydını silme

### <a name="prototype"></a>Prototype

```c
UINT ux_device_stack_class_unregister(
    UCHAR *class_name,
    UINT (*class_entry_function)(struct UX_SLAVE_CLASS_COMMAND_STRUCT*));
```

### <a name="description"></a>Açıklama

Bu işlev, uygulama tarafından USB cihaz sınıfının kaydını silmek için kullanılır.

> [!NOTE]
> Class_name C dizesi NULL ile sonlandırılmış olmalı ve bunun uzunluğu (NULL-Sonlandırıcı kendisi olmadan) **UX_MAX_CLASS_NAME_LENGTH** daha büyük olmamalıdır.

### <a name="parameters"></a>Parametreler

- **class_name**: sınıf adı
- **class_entry_function**: sınıfının giriş işlevi.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) sınıfın kaydı silindi.
- **UX_NO_CLASS_MATCH** (0x57) Sınıf kayıtlı değil.

### <a name="example"></a>Örnek

```c
/* The following example illustrates this service. */

/* Unitialize the device storage class. */
status = ux_device_stack_class_unregister(_ux_system_slave_class_storage_name, ux_device_class_storage_entry);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_configuration_get"></a>ux_device_stack_configuration_get

Geçerli yapılandırmayı al

### <a name="prototype"></a>Prototype

```c
UINT ux_device_stack_configuration_get(VOID);
```

### <a name="description"></a>Açıklama

Bu işlev, ana bilgisayar tarafından cihazda çalışan geçerli yapılandırmayı almak için kullanılır.

### <a name="input-parameter"></a>Giriş parametresi

Yok

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) veri aktarımı tamamlandı.

### <a name="example"></a>Örnek

```c
UINT status;

/* The following example illustrates this service. */
status = ux_device_stack_configuration_get();

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_configuration_set"></a>ux_device_stack_configuration_set

Geçerli yapılandırmayı ayarla

### <a name="prototype"></a>Prototype

```c
UINT ux_device_stack_configuration_set(ULONG configuration_value);
```

### <a name="description"></a>Açıklama

Bu işlev, ana bilgisayar tarafından cihazda çalışan geçerli yapılandırmayı ayarlamak için kullanılır. Bu komutun alınması sırasında, USB cihaz yığını bu yapılandırmaya bağlı her arabirimin 0 alternatif ayarını etkinleştireceğiz.

### <a name="input-parameter"></a>Giriş parametresi

- **configuration_value** Konak tarafından seçilen yapılandırma değeri.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) yapılandırma başarıyla ayarlandı.

### <a name="example"></a>Örnek

```c
ULONG configuration_value;
UINT status;

/* The following example illustrates this service. */
status = ux_device_stack_configuration_set(configuration_value);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_descriptor_send"></a>ux_device_stack_descriptor_send

Konağa tanımlayıcı gönder

### <a name="prototype"></a>Prototype

```c
UINT ux_device_stack_descriptor_send(
    ULONG descriptor_type, 
    ULONG request_index, 
    ULONG host_length);
```

### <a name="description"></a>Açıklama

Bu işlev, konak için bir tanımlayıcı döndürmek üzere cihaz tarafında kullanılır. Bu tanımlayıcı bir cihaz tanımlayıcısı, bir yapılandırma tanımlayıcısı veya dize tanımlayıcı olabilir.

### <a name="parameters"></a>Parametreler

- **descriptor_type**: tanımlayıcının türü. Aşağıdaki değerlerden biri olmalıdır.
  - **UX_DEVICE_DESCRIPTOR_ITEM**
  - **UX_CONFIGURATION_DESCRIPTOR_ITEM**
  - **UX_STRING_DESCRIPTOR_ITEM**
  - **UX_DEVICE_QUALIFIER_DESCRIPTOR_ITEM**
  - **UX_OTHER_SPEED_DESCRIPTOR_ITEM**
- **request_index**: tanımlayıcının dizini.
- **host_length**: konağın gerektirdiği uzunluk.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) veri aktarımı tamamlandı.
- **UX_ERROR** (0xFF) aktarma tamamlanmadı.

### <a name="example"></a>Örnek

```c
ULONG descriptor_type;
ULONG request_index;
ULONG host_length;
UINT status;

/* The following example illustrates this service. */
status = ux_device_stack_descriptor_send(descriptor_type, request_index, host_length);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_disconnect"></a>ux_device_stack_disconnect

Cihaz yığınının bağlantısını kes

### <a name="prototype"></a>Prototype

```c
UINT ux_device_stack_disconnect(VOID);
```

### <a name="description"></a>Açıklama

Bir cihaz bağlantısının kesilmesi durumunda VBUS Yöneticisi bu işlevi çağırır. Cihaz yığını, bu cihaza kayıtlı tüm sınıfları bilgilendirir ve sonra tüm cihaz kaynaklarını serbest bırakacaktır.

### <a name="input-parameter"></a>Giriş parametresi

Yok

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) cihazın bağlantısı kesildi.

### <a name="example"></a>Örnek

```c
UINT status;

/* The following example illustrates this service. */
status = ux_device_stack_disconnect();

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_endpoint_stall"></a>ux_device_stack_endpoint_stall

İstek uç noktası kabini koşulu

### <a name="prototype"></a>Prototype

```c
UINT ux_device_stack_endpoint_stall(UX_SLAVE_ENDPOINT*endpoint);
```

### <a name="description"></a>Açıklama

Bu işlev, bir uç noktanın konağa bir kabin koşulu döndürmesi gerektiğinde USB cihaz sınıfı tarafından çağrılır.

### <a name="input-parameter"></a>Giriş parametresi

- **uç nokta** Kabin koşulunun istendiği uç nokta.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) Bu işlem başarılı oldu.
- **UX_ERROR** (0xFF) cihaz geçersiz bir durumda.

### <a name="example"></a>Örnek

```c
UINT status;

/* The following example illustrates this service. */
status = ux_device_stack_endpoint_stall(endpoint);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_host_wakeup"></a>ux_device_stack_host_wakeup

Konağı uyandırma

### <a name="prototype"></a>Prototype

```c
UINT ux_device_stack_host_wakeup(VOID);
```

### <a name="description"></a>Açıklama

Bu işlev, cihaz ana bilgisayarı uyandırmayı istediğinde çağrılır. Bu komut yalnızca cihaz askıda kalma modundayken geçerlidir. Bu cihaz, USB konağını uyku modundan çıkarmak isteyip istemediğinize karar vermek için kullanılır. Örneğin, bir USB Modem, telefon hattında halka sinyali algıladığında bir ana bilgisayarı uyandırabilirler.

### <a name="input-parameter"></a>Giriş parametresi

Yok

### <a name="return-values"></a>Dönüş değerleri

- **UX_SUCCESS** (0x00) çağrı başarılı oldu.
- **UX_FUNCTION_NOT_SUPPORTED** (0x54) çağrı başarısız oldu (cihaz muhtemelen askıya alınmış modda değildi).

### <a name="example"></a>Örnek

```c
UINT status;

/* The following example illustrates this service. */
status = ux_device_stack_host_wakeup();

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_initialize"></a>ux_device_stack_initialize

USB cihaz yığınını Başlat

### <a name="prototype"></a>Prototype

```c
UINT ux_device_stack_initialize(
    UCHAR *device_framework_high_speed,
    ULONG device_framework_length_high_speed,
    UCHAR *device_framework_full_speed,
    ULONG device_framework_length_full_speed,
    UCHAR *string_framework,
    ULONG string_framework_length,
    UCHAR *language_id_framework,
    ULONG language_id_framework_length),
    UINT (*ux_system_slave_change_function)(ULONG)));
```

### <a name="description"></a>Açıklama

Bu işlev, USB cihaz yığınını başlatmak için uygulama tarafından çağırılır. Herhangi bir sınıfı veya denetleyicisi başlatmaz. Bu, ayrı işlev çağrılarında yapılmalıdır. Bu çağrı, genellikle, USB işlevinin cihaz çerçevesi ile yığın sağlar. Her hız için tamamen ayrı ayrı cihaz çerçevesine sahip olma olasılığa sahip hem yüksek hem de tam hızları destekler. Dize çerçevesi ve birden çok dil desteklenir.

### <a name="parameters"></a>Parametreler

- **device_framework_high_speed**: yüksek hız çerçevesine yönelik işaretçi.
- **device_framework_length_high_speed**: yüksek hız çerçevesinin uzunluğu.
- **device_framework_full_speed**: tam hız çerçevesine yönelik işaretçi.
- **device_framework_length_full_speed**: tam hız çerçevesinin uzunluğu.
- **string_framework**: dize çerçevesi işaretçisi.
- **string_framework_length**: dize çerçevesinin uzunluğu.
- **language_id_framework**: dize Language Framework işaretçisi.
- **language_id_framework_length**: dize dili çerçevesinin uzunluğu.
- **ux_system_slave_change_function**: cihaz durumu değiştiğinde çağrılacak işlev.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) Bu işlem başarılı oldu.
- **UX_MEMORY_INSUFFICIENT** (0x12) yığının başlatılması için yeterli bellek yok.
- **UX_DESCRIPTOR_CORRUPTED** (0x42) tanımlayıcı geçersiz.

### <a name="example"></a>Örnek

```c
/* Example of a device framework */

#define DEVICE_FRAMEWORK_LENGTH_FULL_SPEED 50

UCHAR device_framework_full_speed[] = {
    /* Device descriptor */
    0x12, 0x01, 0x10, 0x01, 0x00, 0x00, 0x00, 0x08,
    0xec, 0x08, 0x10, 0x00, 0x00, 0x00, 0x00, 0x00,
    0x00, 0x01,

    /* Configuration descriptor */
    0x09, 0x02, 0x20, 0x00, 0x01, 0x01, 0x00, 0xc0,
    0x32,

    /* Interface descriptor */
    0x09, 0x04, 0x00, 0x00, 0x02, 0x08, 0x06, 0x50,
    0x00,

    /* Endpoint descriptor (Bulk Out) */
    0x07, 0x05, 0x01, 0x02, 0x40, 0x00, 0x00,

    /* Endpoint descriptor (Bulk In) */
    0x07, 0x05, 0x82, 0x02, 0x40, 0x00, 0x00
};

#define DEVICE_FRAMEWORK_LENGTH_HIGH_SPEED 60

UCHAR device_framework_high_speed[] = {
    /* Device descriptor */
    0x12, 0x01, 0x00, 0x02, 0x00, 0x00, 0x00, 0x40,
    0x0a, 0x07, 0x25, 0x40, 0x01, 0x00, 0x01, 0x02,
    0x03, 0x01,

    /* Device qualifier descriptor */
    0x0a, 0x06, 0x00, 0x02, 0x00, 0x00, 0x00, 0x40,
    0x01, 0x00,

    /* Configuration descriptor */
    0x09, 0x02, 0x20, 0x00, 0x01, 0x01, 0x00, 0xc0,
    0x32,

    /* Interface descriptor */
    0x09, 0x04, 0x00, 0x00, 0x02, 0x08, 0x06, 0x50,
    0x00,

    /* Endpoint descriptor (Bulk Out) */
    0x07, 0x05, 0x01, 0x02, 0x00, 0x02, 0x00,

    /* Endpoint descriptor (Bulk In) */
    0x07, 0x05, 0x82, 0x02, 0x00, 0x02, 0x00
};

/* String Device Framework:
    Byte 0 and 1: Word containing the language ID: 0x0904 for US
    Byte 2 : Byte containing the index of the descriptor
    Byte 3 : Byte containing the length of the descriptor string */

#define STRING_FRAMEWORK_LENGTH 38 UCHAR string_framework[] = {
    /* Manufacturer string descriptor: Index 1 */
    0x09, 0x04, 0x01, 0x0c,
    0x45, 0x78, 0x70, 0x72,0x65, 0x73, 0x20, 0x4c,
    0x6f, 0x67, 0x69, 0x63,

    /* Product string descriptor: Index 2 */
    0x09, 0x04, 0x02, 0x0c,
    0x4D, 0x4C, 0x36, 0x39, 0x36, 0x35, 0x30, 0x30,
    0x20, 0x53, 0x44, 0x4B,

    /* Serial Number string descriptor: Index 3 */
    0x09, 0x04, 0x03, 0x04,
    0x30, 0x30, 0x30, 0x31
};

/* Multiple languages are supported on the device, to add a language besides English, 
  the Unicode language code must be appended to the language_id_framework array 
  and the length adjusted accordingly. */

#define LANGUAGE_ID_FRAMEWORK_LENGTH 2

UCHAR language_id_framework[] = {
    /* English. */
    0x09, 0x04
};
```

Bu uygulama, denetleyici durumunu değiştirdiğinde bir geri arama isteğinde bulunabilir. Denetleyicinin iki ana durumu şunlardır:

- **UX_DEVICE_SUSPENDED**
- **UX_DEVICE_RESUMED**

Uygulamanın askıya alma/sürdürülme sinyalleri gerekmiyorsa, bir UX_NULL işlevi sağlar.

```c
UINT status;

/* The code below is required for installing the device portion of USBX. 
    There is no call back for device status change in this example. */
status = ux_device_stack_initialize(&device_framework_high_speed,
    DEVICE_FRAMEWORK_LENGTH_HIGH_SPEED, &device_framework_full_speed,
    DEVICE_FRAMEWORK_LENGTH_FULL_SPEED, &string_framework,
    STRING_FRAMEWORK_LENGTH, &language_id_framework,
    LANGUAGE_ID_FRAMEWORK_LENGTH, UX_NULL);

/* If status equals UX_SUCCESS, initialization was successful. */
```

### <a name="ux_device_stack_interface_delete"></a>ux_device_stack_interface_delete

Yığın arabirimini silme

### <a name="prototype"></a>Prototype

```c
UINT ux_device_stack_interface_delete(UX_SLAVE_INTERFACE*interface);
```

### <a name="description"></a>Açıklama

Bu işlev, bir arabirim kaldırılması gerektiğinde çağrılır. Bir cihaz ayıklanırken veya bir veri yolu sıfırlaması sonrasında ya da yeni bir alternatif ayar olduğunda arabirim kaldırılır.

### <a name="input-parameter"></a>Giriş parametresi

- **arabirim**: kaldırılacak arabirime yönelik işaretçi.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) Bu işlem başarılı oldu.

### <a name="example"></a>Örnek

```c
UINT status;

/* The following example illustrates this service. */
status = ux_device_stack_interface_delete(interface);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_interface_get"></a>ux_device_stack_interface_get

Geçerli arabirim değerini Al

### <a name="prototype"></a>Prototype

```c
UINT ux_device_stack_interface_get(UINT interface_value);
```

### <a name="description"></a>Açıklama

Bu işlev, ana bilgisayar geçerli arabirimi sorguladığında çağrılır. Cihaz geçerli arabirim değerini döndürür.

> [!NOTE]
> Bu işlev kullanım dışıdır. Bu, eski yazılımlar için kullanılabilir, ancak yeni yazılımların bunun yerine ***ux_device_stack_alternate_setting_get*** işlevini kullanması gerekir.

### <a name="input-parameter"></a>Giriş parametresi

- **interface_value** Döndürülecek arabirim değeri.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) Bu işlem başarılı oldu.
- **UX_ERROR** (0xFF) arabirim yok.

### <a name="example"></a>Örnek

```c
ULONG interface_value;

UINT status;

/* The following example illustrates this service. */
status = ux_device_stack_interface_get(interface_value);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_interface_set"></a>ux_device_stack_interface_set

Arabirimin alternatif ayarını değiştirme

### <a name="prototype"></a>Prototype

```c
UINT ux_device_stack_interface_set(
    UCHAR *device_framework,
    ULONG device_framework_length, 
    ULONG alternate_setting_value);
```

### <a name="description"></a>Açıklama

Bu işlev, ana bilgisayar arabirim için alternatif ayarda bir değişiklik istediğinde çağrılır.

### <a name="parameters"></a>Parametreler

- **device_framework**: Bu arabirim için cihaz çerçevesinin adresi.
- **device_framework_length**: cihaz çerçevesinin uzunluğu.
- **alternate_setting_value**: Bu arabirim tarafından kullanılacak alternatif ayar değeri.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) Bu işlem başarılı oldu.
- **UX_ERROR** (0xFF) arabirim yok.

### <a name="example"></a>Örnek

```c
UCHAR * device_framework
ULONG device_framework_length;
ULONG alternate_setting_value;
UINT status;

/* The following example illustrates this service. */
status = ux_device_stack_interface_set(device_framework,
    device_framework_length, alternate_setting_value);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_interface_start"></a>ux_device_stack_interface_start

Arabirim örneğine sahip bir sınıf için Aramayı başlatma

### <a name="prototype"></a>Prototype

```c
UINT ux_device_stack_interface_start(UX_SLAVE_INTERFACE*interface);
```

### <a name="description"></a>Açıklama

Bu işlev, ana bilgisayar tarafından bir arabirim seçildiğinde ve cihaz yığınının bu arabirim örneğine sahip olmak için bir cihaz sınıfı araması gerektiğinde çağrılır.

### <a name="input-parameter"></a>Giriş parametresi

- **arabirim**: oluşturulan arabirime yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) Bu işlem başarılı oldu.
- **UX_NO_CLASS_MATCH** (0x57) Bu arabirim için hiçbir sınıf yok.

### <a name="example"></a>Örnek

```c
UINT status;

/* The following example illustrates this service. */
status = ux_device_stack_interface_start(interface);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_transfer_request"></a>ux_device_stack_transfer_request

Konağa veri aktarma isteği

### <a name="prototype"></a>Prototype

```c
UINT ux_device_stack_transfer_request(
    UX_SLAVE_TRANSFER *transfer_request,
    ULONG slave_length, 
    ULONG host_length);
```

### <a name="description"></a>Açıklama

Bu işlev, bir sınıf veya yığın konağa veri aktarmak istediğinde çağrılır. Konak, cihazı her zaman yoklar, ancak cihaz verileri önceden hazırlayabilir.

### <a name="parameters"></a>Parametreler

- **transfer_request**: aktarım isteğine yönelik işaretçi.
- **slave_length**: cihazın geri dönmek istediği uzunluk.
- **host_length**: konağın istediği uzunluk.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) Bu işlem başarılı oldu.
- **UX_TRANSFER_NOT_READY** (0x25) cihaz geçersiz bir durumda; **eklenmiş**, **yapılandırılmış** veya **Çözümlenmiş** olmalıdır.
- **UX_ERROR** (0xFF) aktarım hatası.

### <a name="example"></a>Örnek

```c
UINT status;

/* The following example illustrates how to transfer more data than an application requests. */
while(total_length) {
    /* How much can we send in this transfer? */
    if (total_length > UX_SLAVE_CLASS_STORAGE_BUFFER_SIZE)
        transfer_length = UX_SLAVE_CLASS_STORAGE_BUFFER_SIZE;
    else
        transfer_length = total_length;

   /* Copy the Storage Buffer into the transfer request memory. */
   ux_utility_memory_copy(transfer_request ->  ux_slave_transfer_request_data_pointer,
       media_memory, transfer_length);

   /* Send the data payload back to the caller. */
   status = ux_device_transfer_request(transfer_request,
       transfer_length, transfer_length);

   /* If status equals UX_SUCCESS, the operation was successful. */

   /* Update the buffer address.  */
    media_memory += transfer_length;

   /* Update the length to remain. */
    total_length -= transfer_length;
}
```

### <a name="ux_device_stack_transfer_abort"></a>ux_device_stack_transfer_abort

Aktarım isteğini iptal etme

### <a name="prototype"></a>Prototype

```c
UINT ux_device_stack_transfer_abort(
    UX_SLAVE_TRANSFER *transfer_request, 
    ULONG completion_code);
```

### <a name="description"></a>Açıklama

Bu işlev, bir uygulamanın bir aktarım isteğini iptal etmek gerektiğinde veya yığının bir uç noktayla ilişkili bir aktarım isteğini iptal etmek gerektiğinde çağrılır.

### <a name="parameters"></a>Parametreler

- **transfer_request**: aktarım isteğine yönelik işaretçi.
- **completion_code**: Bu aktarım isteğinin tamamlanmasını bekleyen sınıfa döndürülecek hata kodu.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) Bu işlem başarılı oldu.

### <a name="example"></a>Örnek

```c
UINT status;

/* The following example illustrates how to abort a transfer when a
    bus reset has been detected on the bus. */
status = ux_device_stack_transfer_abort(transfer_request, UX_TRANSFER_BUS_RESET);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_uninitialize"></a>ux_device_stack_uninitialize

Yığın kaldırma

### <a name="prototype"></a>Prototype

```c
UINT ux_device_stack_uninitialize();
```

### <a name="description"></a>Açıklama

Bu işlev, bir uygulamanın USBX cihaz yığınını geri almaması gerektiğinde çağrılır – tüm cihaz yığını kaynakları serbest bırakılır. Bu, tüm sınıfların ux_device_stack_class_unregister aracılığıyla kaydolduktan sonra çağrılmalıdır.

### <a name="parameters"></a>Parametreler

Hiçbiri

### <a name="return-value"></a>Dönüş Değeri

**UX_SUCCESS** (0x00) Bu işlem başarılı oldu.
