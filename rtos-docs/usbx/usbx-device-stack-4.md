---
title: Bölüm 4 - USBX Cihaz Hizmetleri Açıklaması
description: USBX Cihaz Hizmetleri hakkında bilgi edinebilirsiniz.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 9d88d9bd177a251a00fec6757fc1f1494b56bab9655a55f973481f273f0683ee
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116797561"
---
# <a name="description-of-usbx-device-services"></a>USBX Cihaz Hizmetleri açıklaması

### <a name="ux_device_stack_alternate_setting_get"></a>ux_device_stack_alternate_setting_get

Arabirim değeri için geçerli alternatif ayarı al

### <a name="prototype"></a>Prototype

```c
UINT ux_device_stack_alternate_setting_get(ULONG interface_value);
```

### <a name="description"></a>Description

Bu işlev USB ana bilgisayarı tarafından belirli bir arabirim değeri için geçerli alternatif ayarı elde etmek için kullanılır. Bir istek alınca denetleyici sürücüsü **GET_INTERFACE** çağrılır.

### <a name="input-parameter"></a>Giriş Parametresi

- **Interface_value** Geçerli alternatif ayarın sorgulandır olduğu arabirim değeri

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) Veri aktarımı tamamlandı.
- **UX_ERROR** (0xFF) Arabirim değeri yanlış.

### <a name="example"></a>Örnek

```c
ULONG interface_value;
UINT status;

/* The following example illustrates this service. */
status = ux_device_stack_alternate_setting_get(interface_value);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_alternate_setting_set"></a>ux_device_stack_alternate_setting_set

Arabirim değeri için geçerli alternatif ayarı ayarlama

### <a name="prototype"></a>Prototype

```c
UINT ux_device_stack_alternate_setting_set(
    ULONG interface_value, 
    ULONG alternate_setting_value);
```

### <a name="description"></a>Description

Bu işlev USB ana bilgisayarı tarafından belirli bir arabirim değeri için geçerli alternatif ayarı ayarlamak için kullanılır. Bir istek alınca denetleyici **SET_INTERFACE** çağrılır. Uygulama **SET_INTERFACE,** alternatif ayarların değerleri sınıfına uygulanır.

Cihaz yığını, bu **UX_SLAVE_CLASS_COMMAND_CHANGE** sahip olan sınıfa alternatif ayar değişikliğini yansıtacak bir uygulama verir.

### <a name="parameters"></a>Parametreler

- **interface_value:** Geçerli alternatif ayarın ayar olduğu arabirim değeri.
- **alternate_setting_value:** Yeni alternatif ayar değeri.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) Veri aktarımı tamamlandı.
- **UX_INTERFACE_HANDLE_UNKNOWN** (0x52) Arabirim ekli değil.
- **UX_FUNCTION_NOT_SUPPORTED** (0x54) Cihaz yapılandırılmadı.
- **UX_ERROR** (0xFF) Arabirim değeri yanlış.

### <a name="example"></a>Örnek

```c
ULONG interface_value;

ULONG alternate_setting_value;

/* The following example illustrates this service. */
status = ux_device_stack_alternate_setting_set(interface_value, alternate_setting_value);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_class_register"></a>ux_device_stack_class_register

Yeni bir USB cihaz sınıfı kaydetme

### <a name="prototype"></a>Prototype

```c
UINT ux_device_stack_class_register(
    UCHAR *class_name,
    UINT (*class_entry_function)(struct UX_SLAVE_CLASS_COMMAND_STRUCT *),
    ULONG configuration_number, 
    ULONG interface_number,  
    VOID *parameter);
```

### <a name="description"></a>Description

Bu işlev, uygulama tarafından yeni bir USB cihaz sınıfı kaydetmek için kullanılır. Bu kayıt, sınıfın bir örneğini değil bir sınıf kapsayıcısı başlatır. Bir sınıfın etkin bir iş parçacığı olmalı ve belirli bir arabirime bağlı olması gerekir.

Bazı sınıflar bir parametre veya parametre listesi bekler. Örneğin, cihaz depolama sınıfı öykünmeye çalıştığı depolama aygıtının geometrisini bekler. Bu nedenle parametre alanı sınıf gereksinimine bağlıdır ve sınıf değerleriyle doldurulmuş bir yapıya yönelik bir değer veya işaretçi olabilir.

> [!NOTE]
> Dizenin C class_name NULL ile sonlandırılmalı ve uzunluğu (NULL-sonlandırıcının kendisi olmadan) **UX_MAX_CLASS_NAME_LENGTH.**

### <a name="parameters"></a>Parametreler

- **class_name** Sınıf Adı
- **class_entry_function** sınıfının giriş işlevi.
- **configuration_number** Bu sınıfın ekli olduğu yapılandırma numarası.
- **interface_number** Bu sınıfın ekli olduğu arabirim numarası.
- **parametre** Sınıfa özgü parametre listesinin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) Sınıfı kaydedildi
- **UX_MEMORY_INSUFFICIENT** (0x12) Sınıf tablosunda hiç giriş kalmadı.
- **UX_THREAD_ERROR** (0x16) Sınıf iş parçacığı oluşturulamaz.

### <a name="example"></a>Örnek

```c
UINT status;

/* The following example illustrates this service. */

/* Initialize the device storage class. The class is connected with interface 1 */
status = ux_device_stack_class_register(_ux_system_slave_class_storage_name ux_device_class_storage_entry,
    1, 1, (VOID *)&parameter);
```

### <a name="ux_device_stack_class_unregister"></a>ux_device_stack_class_unregister

USB cihaz sınıfının kaydını geri ala

### <a name="prototype"></a>Prototype

```c
UINT ux_device_stack_class_unregister(
    UCHAR *class_name,
    UINT (*class_entry_function)(struct UX_SLAVE_CLASS_COMMAND_STRUCT*));
```

### <a name="description"></a>Description

Bu işlev, uygulama tarafından BIR USB cihaz sınıfının kaydının kaydının geri alımı için kullanılır.

> [!NOTE]
> Dizenin C class_name NULL ile sonlandırılmalı ve uzunluğu (NULL-sonlandırıcının kendisi olmadan) **UX_MAX_CLASS_NAME_LENGTH.**

### <a name="parameters"></a>Parametreler

- **class_name:** Sınıf Adı
- **class_entry_function:** sınıfının giriş işlevi.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) Sınıfın kaydı alındı.
- **UX_NO_CLASS_MATCH** (0x57) Sınıfı kayıtlı değil.

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

### <a name="description"></a>Description

Bu işlev, konak tarafından cihazda çalışan geçerli yapılandırmayı almak için kullanılır.

### <a name="input-parameter"></a>Giriş Parametresi

Hiçbiri

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) Veri aktarımı tamamlandı.

### <a name="example"></a>Örnek

```c
UINT status;

/* The following example illustrates this service. */
status = ux_device_stack_configuration_get();

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_configuration_set"></a>ux_device_stack_configuration_set

Geçerli yapılandırmayı ayarlama

### <a name="prototype"></a>Prototype

```c
UINT ux_device_stack_configuration_set(ULONG configuration_value);
```

### <a name="description"></a>Description

Bu işlev, konak tarafından cihazda çalışan geçerli yapılandırmayı ayarlamak için kullanılır. Bu komutun alımının ardından, USB cihaz yığını bu yapılandırmaya bağlı her arabirimin 0 alternatif ayarını etkinleştirir.

### <a name="input-parameter"></a>Giriş Parametresi

- **configuration_value** Konak tarafından seçilen yapılandırma değeri.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) Yapılandırma başarıyla ayarlanmıştır.

### <a name="example"></a>Örnek

```c
ULONG configuration_value;
UINT status;

/* The following example illustrates this service. */
status = ux_device_stack_configuration_set(configuration_value);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_descriptor_send"></a>ux_device_stack_descriptor_send

Ana bilgisayar için bir tanımlayıcı gönderme

### <a name="prototype"></a>Prototype

```c
UINT ux_device_stack_descriptor_send(
    ULONG descriptor_type, 
    ULONG request_index, 
    ULONG host_length);
```

### <a name="description"></a>Description

Bu işlev, cihaz tarafı tarafından konak için bir tanımlayıcıyı geri dönmek için kullanılır. Bu tanımlayıcı bir cihaz tanımlayıcısı, yapılandırma tanımlayıcısı veya dize tanımlayıcısı olabilir.

### <a name="parameters"></a>Parametreler

- **descriptor_type:** Tanımlayıcının türü. Aşağıdaki değerlerden biri olması gerekir.
  - **UX_DEVICE_DESCRIPTOR_ITEM**
  - **UX_CONFIGURATION_DESCRIPTOR_ITEM**
  - **UX_STRING_DESCRIPTOR_ITEM**
  - **UX_DEVICE_QUALIFIER_DESCRIPTOR_ITEM**
  - **UX_OTHER_SPEED_DESCRIPTOR_ITEM**
- **request_index:** Tanımlayıcının dizini.
- **host_length:** Konak için gereken uzunluk.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) Veri aktarımı tamamlandı.
- **UX_ERROR** (0xFF) Aktarım tamamlanmadı.

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

Cihaz yığınının bağlantısını kesme

### <a name="prototype"></a>Prototype

```c
UINT ux_device_stack_disconnect(VOID);
```

### <a name="description"></a>Description

VbUS yöneticisi, bir cihaz bağlantısı kesi olduğunda bu işlevi çağırıyor. Cihaz yığını, bu cihaza kayıtlı tüm sınıfları bilgilendir ve bundan sonra tüm cihaz kaynaklarını serbest bırakacak.

### <a name="input-parameter"></a>Giriş Parametresi

Hiçbiri

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) Cihazın bağlantısı kesildi.

### <a name="example"></a>Örnek

```c
UINT status;

/* The following example illustrates this service. */
status = ux_device_stack_disconnect();

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_endpoint_stall"></a>ux_device_stack_endpoint_stall

İstek uç noktası Durak koşulu

### <a name="prototype"></a>Prototype

```c
UINT ux_device_stack_endpoint_stall(UX_SLAVE_ENDPOINT*endpoint);
```

### <a name="description"></a>Description

Bu işlev USB cihaz sınıfı tarafından bir uç noktanın ana bilgisayara Bir Durak koşulu iade etmek zorunda olduğu zaman çağrılır.

### <a name="input-parameter"></a>Giriş Parametresi

- **uç nokta** Durak koşulu istenen uç nokta.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) Bu işlem başarılı oldu.
- **UX_ERROR** (0xFF) Cihaz geçersiz durumda.

### <a name="example"></a>Örnek

```c
UINT status;

/* The following example illustrates this service. */
status = ux_device_stack_endpoint_stall(endpoint);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_host_wakeup"></a>ux_device_stack_host_wakeup

Ana bilgisayarı uyandırma

### <a name="prototype"></a>Prototype

```c
UINT ux_device_stack_host_wakeup(VOID);
```

### <a name="description"></a>Description

Cihaz, ana bilgisayarı uyandırmak istediği zaman bu işlev çağrılır. Bu komut yalnızca cihaz askıya alma modunda olduğunda geçerlidir. USB ana bilgisayarlarını ne zaman uyandırmak istediği cihaz uygulamasına göre karar verir. Örneğin USB modem, telefon hattında bir RING sinyali algılayan bir ana bilgisayarı uyandırabilir.

### <a name="input-parameter"></a>Giriş Parametresi

Hiçbiri

### <a name="return-values"></a>Dönüş değerleri

- **UX_SUCCESS** (0x00) Çağrı başarılı oldu.
- **UX_FUNCTION_NOT_SUPPORTED** (0x54) Çağrı başarısız oldu (cihaz büyük olasılıkla askıya alınmış modda değil).

### <a name="example"></a>Örnek

```c
UINT status;

/* The following example illustrates this service. */
status = ux_device_stack_host_wakeup();

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_initialize"></a>ux_device_stack_initialize

USB cihaz yığınını başlatma

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

### <a name="description"></a>Description

Bu işlev, uygulama tarafından USB cihaz yığınını başlatmak için çağrılır. Hiçbir sınıfı veya denetleyiciyi başlatmaz. Bu, ayrı işlev çağrıları ile yapılması gerekir. Bu çağrı temel olarak USB işlevi için cihaz çerçevesiyle birlikte yığını sağlar. Her hız için tamamen ayrı cihaz çerçevesine sahip olma olasılığıyla hem yüksek hem de tam hızları destekler. Dize çerçevesi ve birden çok dil de destekler.

### <a name="parameters"></a>Parametreler

- **device_framework_high_speed:** Yüksek hızlı çerçevenin işaretçisi.
- **device_framework_length_high_speed:** Yüksek hızlı çerçevenin uzunluğu.
- **device_framework_full_speed:** Tam hızlı çerçevenin işaretçisi.
- **device_framework_length_full_speed:** Tam hızlı çerçevenin uzunluğu.
- **string_framework:** Dize çerçevesi işaretçisi.
- **string_framework_length:** Dize çerçevesinin uzunluğu.
- **language_id_framework:** Dize dili çerçevesinin işaretçisi.
- **language_id_framework_length:** Dize dili çerçevesinin uzunluğu.
- **ux_system_slave_change_function:** Cihaz durumu değişirken çağrılır.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) Bu işlem başarılı oldu.
- **UX_MEMORY_INSUFFICIENT** (0x12) Yığını başlatmak için yeterli bellek yok.
- **UX_DESCRIPTOR_CORRUPTED** (0x42) Tanımlayıcı geçersiz.

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

Denetleyici durumunu değiştirirken uygulama geri çağrı isteğinde olabilir. Denetleyici için iki ana eyalet vardır:

- **UX_DEVICE_SUSPENDED**
- **UX_DEVICE_RESUMED**

Uygulamanın Askıya Alma/Sürdürme sinyallerine ihtiyacı yoksa, bir UX_NULL sağlar.

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

### <a name="description"></a>Description

Bu işlev, bir arabirimin kaldırılması gerektiği zaman çağrılır. Arabirim, cihaz ayıklanan veya veri veri yol sıfırlaması yapılan veya yeni bir alternatif ayar olduğunda kaldırılan bir arabirimdir.

### <a name="input-parameter"></a>Giriş Parametresi

- **interface:** Kaldır için arabirim işaretçisi.

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

Geçerli arabirim değerini al

### <a name="prototype"></a>Prototype

```c
UINT ux_device_stack_interface_get(UINT interface_value);
```

### <a name="description"></a>Description

Konak geçerli arabirimi sorgularken bu işlev çağrılır. Cihaz geçerli arabirim değerini döndürür.

> [!NOTE]
> Bu işlev kullanım dışıdır. Eski yazılımlar için kullanılabilir, ancak yeni  yazılımlar bunun yerine ux_device_stack_alternate_setting_get kullandır.

### <a name="input-parameter"></a>Giriş Parametresi

- **interface_value** İade etmek için arabirim değeri.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) Bu işlem başarılı oldu.
- **UX_ERROR** (0xFF) Arabirim yok.

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

### <a name="description"></a>Description

Bu işlev, konak arabirim için alternatif ayarda değişiklik isteğinde olduğunda çağrılır.

### <a name="parameters"></a>Parametreler

- **device_framework:** Bu arabirim için cihaz çerçevesinin adresi.
- **device_framework_length:** Cihaz çerçevesinin uzunluğu.
- **alternate_setting_value:** Bu arabirim tarafından kullanılacak alternatif ayar değeri.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) Bu işlem başarılı oldu.
- **UX_ERROR** (0xFF) Arabirim yok.

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

Arabirim örneğine sahip olmak için sınıf aramaya başlama

### <a name="prototype"></a>Prototype

```c
UINT ux_device_stack_interface_start(UX_SLAVE_INTERFACE*interface);
```

### <a name="description"></a>Description

Bu işlev, konak tarafından bir arabirim seçildiğinde ve cihaz yığınının bu arabirim örneğine sahip olmak için bir cihaz sınıfı araması gerektirse çağrılır.

### <a name="input-parameter"></a>Giriş Parametresi

- **interface:** Oluşturulan arabirimin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) Bu işlem başarılı oldu.
- **UX_NO_CLASS_MATCH** (0x57) Bu arabirim için sınıf yok.

### <a name="example"></a>Örnek

```c
UINT status;

/* The following example illustrates this service. */
status = ux_device_stack_interface_start(interface);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_transfer_request"></a>ux_device_stack_transfer_request

Verileri ana bilgisayarla aktarma isteği

### <a name="prototype"></a>Prototype

```c
UINT ux_device_stack_transfer_request(
    UX_SLAVE_TRANSFER *transfer_request,
    ULONG slave_length, 
    ULONG host_length);
```

### <a name="description"></a>Description

Bu işlev, bir sınıf veya yığın konakta veri aktarımı yapmak istiyorsa çağrılır. Konak her zaman cihazı yoklar ancak cihaz verileri önceden hazırlar.

### <a name="parameters"></a>Parametreler

- **transfer_request:** Aktarım isteğinin işaretçisi.
- **slave_length:** Cihazın geri dönmek istediği uzunluk.
- **host_length:** Ana bilgisayar tarafından istenen uzunluk.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) Bu işlem başarılı oldu.
- **UX_TRANSFER_NOT_READY** (0x25) Cihaz geçersiz durumda; **İLIŞTIRILMIŞ,** **YALITILMIŞ** veya ADRESLI **olması gerekir.**
- **UX_ERROR** (0xFF) Aktarım hatası.

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

### <a name="description"></a>Description

Bu işlev, uygulamanın bir aktarım isteğini iptal etmesi veya yığının uç noktayla ilişkili bir aktarım isteğini durdurması gerekirken çağrılır.

### <a name="parameters"></a>Parametreler

- **transfer_request:** Aktarım isteğinin işaretçisi.
- **completion_code:** Bu aktarım isteğinin tamamlandıktan sonra sınıfına döndürülen hata kodu.

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

Yığını birimleştirme

### <a name="prototype"></a>Prototype

```c
UINT ux_device_stack_uninitialize();
```

### <a name="description"></a>Description

Bu işlev, bir uygulamanın USBX cihaz yığınını birimleştirmesi gerekirken çağrılır. Tüm cihaz yığını kaynakları serbest bırakılmış olur. Bu çağrı, tüm sınıfların kayıttan silindikten sonra ux_device_stack_class_unregister.

### <a name="parameters"></a>Parametreler

Hiçbiri

### <a name="return-value"></a>Dönüş Değeri

**UX_SUCCESS** (0x00) Bu işlem başarılı oldu.
