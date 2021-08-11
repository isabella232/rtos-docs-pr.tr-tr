---
title: Bölüm 5-USBX konak sınıfları API 'SI
description: USBX konak sınıfları API 'SI hakkında bilgi edinin.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 62750ab4a5540b243665a7a7d9000a0d60c4435313b6de2e1579ae7f1c20fe55
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116790675"
---
# <a name="chapter-5---usbx-host-classes-api"></a>Bölüm 5-USBX konak sınıfları API 'SI

Bu bölümde, USBX konak sınıflarının tüm sunulan API 'Leri ele alınmaktadır. Her sınıf için aşağıdaki API 'Ler ayrıntılı olarak açıklanmıştır.

- HID sınıfı
- CDC-ACM sınıfı
- CDC-ECD sınıfı
- Depolama sınıfı

## <a name="ux_host_class_hid_client_register"></a>ux_host_class_hid_client_register

HID sınıfına bir HID istemcisini kaydedin.

### <a name="prototype"></a>Prototype

```c
UINT ux_host_class_hid_client_register(
    UCHAR *hid_client_name,
    UINT (*hid_client_handler)
    (struct UX_HOST_CLASS_HID_CLIENT_COMMAND_STRUCT *));
```

### <a name="description"></a>Description

Bu işlev, bir HID istemcisini HID sınıfına kaydetmek için kullanılır. HID sınıfının, bu cihazdan veri istenmeden önce bir HID aygıtı ile HID istemcisi arasında bir eşleşme bulması gerekir.

> [!NOTE]
> Hid_client_name C dizesi NULL ile sonlandırılmış olmalı ve bunun uzunluğu (NULL-Sonlandırıcı kendisi olmadan) **UX_HOST_CLASS_HID_MAX_CLIENT_NAME_LENGTH** daha büyük olmamalıdır.

### <a name="parameters"></a>Parametreler

- **hid_client_name** HID istemci adı işaretçisi.
- **hid_client_handler** HID istemci işleyicisine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) veri aktarımı tamamlandı
- İstemci için **UX_MEMORY_INSUFFICIENT** (0x12) bellek ayırması başarısız oldu.
- **UX_MEMORY_ARRAY_FULL** (0x1A) en fazla istemci zaten kayıtlı.
- **UX_HOST_CLASS_ALREADY_INSTALLED** (0x58) Bu sınıf zaten var

### <a name="example"></a>Örnek

```c
UINT status;

/* The following example illustrates how to register a HID client, in
this case a USB mouse, to the HID class. */

status = ux_host_class_hid_client_register("ux_host_class_hid_client_mouse",
    ux_host_class_hid_mouse_entry);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_hid_report_callback_register"></a>ux_host_class_hid_report_callback_register

HID sınıfından bir geri çağırma kaydeder.

### <a name="prototype"></a>Prototype

```c
UINT ux_host_class_hid_report_callback_register(
    UX_HOST_CLASS_HID *hid,
    UX_HOST_CLASS_HID_REPORT_CALLBACK *call_back);
```

### <a name="description"></a>Description

Bu işlev, bir rapor alındığında, HID sınıfından bir geri çağırma işlemini HID istemcisine kaydetmek için kullanılır.

### <a name="parameters"></a>Parametreler

- **HID** HID sınıfı örneğine yönelik işaretçi
- **call_back** Call_back yapısına yönelik işaretçi

### <a name="return-values"></a>Dönüş değerleri

- **UX_SUCCESS** (0x00) veri aktarımı tamamlandı
- **UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) geçersiz HID örneği.
- Rapor geri çağırma kaydında **UX_HOST_CLASS_HID_REPORT_ERROR** (0x79) hatası.

### <a name="example"></a>Örnek

```c
UINT status;

/* This example illustrates how to register a HID client, in this case a USB mouse, to the HID class. In this case, the HID client is asking the HID class to call the client for each usage received in the HID report. */

call_back.ux_host_class_hid_report_callback_id = 0;
call_back.ux_host_class_hid_report_callback_function = ux_host_class_hid_mouse_callback;

call_back.ux_host_class_hid_report_callback_buffer = UX_NULL;
call_back.ux_host_class_hid_report_callback_flags = UX_HOST_CLASS_HID_REPORT_INDIVIDUAL_USAGE;

call_back.ux_host_class_hid_report_callback_length = 0;

status = ux_host_class_hid_report_callback_register(hid, &call_back);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_hid_periodic_report_start"></a>ux_host_class_hid_periodic_report_start

Bir HID sınıf örneği için dönemsel uç noktayı başlatın.

### <a name="prototype"></a>Prototype

```c
UINT ux_host_class_hid_periodic_report_start(UX_HOST_CLASS_HID *hid);
```

### <a name="description"></a>Description

Bu işlev, bu HID istemcisine bağlanan HID sınıfının örneği için dönemsel (kesme) uç noktasını başlatmak için kullanılır. HID sınıfı, HID istemcisi etkinleştirilinceye kadar düzenli bitiş noktasını başlatamıyor ve bu nedenle bu uç noktayı rapor almak için başlatmak üzere HID istemcisine bırakılır.

### <a name="input-parameter"></a>Giriş parametresi

- **HID** HID sınıfı örneğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) düzenli raporlama başarıyla başlatıldı.
- düzenli raporda **ux_host_class_hid_PERIODIC_REPORT_ERROR** (0x7A) hatası.
- **UX_HOST_CLASS_INSTANCE_UNKNOWN** (0X5B) HID sınıfı örneği yok.

### <a name="example"></a>Örnek

```c
UINT status;

/* The following example illustrates how to start the periodic
endpoint. */

status = ux_host_class_hid_periodic_report_start(hid);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_hid_periodic_report_stop"></a>ux_host_class_hid_periodic_report_stop

Bir HID sınıf örneği için dönemsel uç noktayı durdurun.

### <a name="prototype"></a>Prototype

```c
UINT ux_host_class_hid_periodic_report_stop(UX_HOST_CLASS_HID *hid);
```

### <a name="description"></a>Description

Bu işlev, bu HID istemcisine bağlanan HID sınıfının örneği için periyodik (kesme) uç noktasını durdurmak üzere kullanılır. HID istemcisi devre dışı bırakılana kadar HID sınıfı, tüm kaynakları serbest bırakılıncaya ve bu nedenle bu uç noktayı durdurmak için HID istemcisine bırakılıncaya kadar, düzenli bitiş noktasını durduramıyor.

### <a name="input-parameter"></a>Giriş parametresi

- **HID** HID sınıfı örneğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) düzenli raporlama başarıyla durduruldu.
- düzenli raporda **ux_host_class_hid_PERIODIC_REPORT_ERROR** (0x7A) hatası.
- **UX_HOST_CLASS_INSTANCE_UNKNOWN** (0X5B) HID sınıfı örneği yok

### <a name="example"></a>Örnek

```c
UINT status;

/* The following example illustrates how to stop the periodic endpoint. */

status = ux_host_class_hid_periodic_report_stop(hid);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_hid_report_get"></a>ux_host_class_hid_report_get

Bir HID sınıf örneğinden rapor alın.

### <a name="prototype"></a>Prototype

```c
UINT ux_host_class_hid_report_get(
    UX_HOST_CLASS_HID *hid,
    UX_HOST_CLASS_HID_CLIENT_REPORT *client_report);
```

### <a name="description"></a>Description

Bu işlev, düzenli bitiş noktasına bağlı olmadan doğrudan cihazdan rapor almak için kullanılır. Bu rapor, denetim uç noktasından geliyor, ancak işlemi, düzenli uç noktada gelmekle aynı.

### <a name="parameters"></a>Parametreler

- **HID** HID sınıfı örneğine yönelik işaretçi.
- **client_report** HID istemci raporuna yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) rapor başarıyla alındı.
- **UX_HOST_CLASS_HID_REPORT_ERROR** (0x70) istemci raporu geçersiz ya da aktarım sırasında hata oluştu.
- **UX_HOST_CLASS_INSTANCE_UNKNOWN** (0X5B) HID sınıfı örneği yok.
- **UX_BUFFER_OVERFLOW** (0x5D) sağlanan arabellek sıkıştırılmamış rapora uyum sağlayacak kadar büyük değil.

### <a name="example"></a>Örnek

```c
UX_HOST_CLASS_HID_CLIENT_REPORT input_report;

UINT status;

/* The following example illustrates how to get a report. */

input_report.ux_host_class_hid_client_report = hid_report;
input_report.ux_host_class_hid_client_report_buffer = buffer;
input_report.ux_host_class_hid_client_report_length = length;
input_report.ux_host_class_hid_client_flags = UX_HOST_CLASS_HID_REPORT_INDIVIDUAL_USAGE;

status = ux_host_class_hid_report_get(hid, &input_report);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_hid_report_set"></a>ux_host_class_hid_report_set

Rapor gönderme

### <a name="prototype"></a>Prototype

```c
UINT ux_host_class_hid_report_set(
    UX_HOST_CLASS_HID *hid,
    UX_HOST_CLASS_HID_CLIENT_REPORT *client_report);
```

### <a name="description"></a>Description

Bu işlev, bir raporu doğrudan cihaza göndermek için kullanılır.

### <a name="parameters"></a>Parametreler

- **HID** HID sınıfı örneğine yönelik işaretçi.
- **client_report** HID istemci raporuna yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) rapor başarıyla gönderildi.
- **UX_HOST_CLASS_HID_REPORT_ERROR** (0x70) istemci raporu geçersiz ya da aktarım sırasında hata oluştu.
- **UX_HOST_CLASS_INSTANCE_UNKNOWN** (0X5B) HID sınıfı örneği yok.
- **UX_HOST_CLASS_HID_REPORT_OVERFLOW** (0x5D) sağlanan arabellek sıkıştırılmamış rapora uyum sağlayacak kadar büyük değil.

### <a name="example"></a>Örnek

```c
/* The following example illustrates how to send a report. */

UX_HOST_CLASS_HID_CLIENT_REPORT input_report;

input_report.ux_host_class_hid_client_report = hid_report;
input_report.ux_host_class_hid_client_report_buffer = buffer;
input_report.ux_host_class_hid_client_report_length = length;
input_report.ux_host_class_hid_client_report_flags = UX_HOST_CLASS_HID_REPORT_INDIVIDUAL_USAGE;

status = ux_host_class_hid_report_set(hid, &input_report);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_hid_mouse_buttons_get"></a>ux_host_class_hid_mouse_buttons_get

Fare düğmelerini al.

### <a name="prototype"></a>Prototype

```c
UINT ux_host_class_hid_mouse_buttons_get(
    UX_HOST_CLASS_HID_MOUSE *mouse_instance,
    ULONG *mouse_buttons);
```

### <a name="description"></a>Description

Bu işlev, fare düğmelerini almak için kullanılır

### <a name="parameters"></a>Parametreler

- **mouse_instance** HID fare örneğine yönelik işaretçi.
- **mouse_buttons** Dönüş düğmelerinin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) Fare düğmesi başarıyla alındı.
- **UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) GIZLI SıNıF örneği yok.

### <a name="example"></a>Örnek

```c
/* The following example illustrates how to obtain mouse buttons. */

UX_HOST_CLASS_HID_MOUSE *mouse_instance;

ULONG mouse_buttons;

status = ux_host_class_hid_mouse_button_get(mouse_instance, &mouse_buttons);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_hid_mouse_position_get"></a>ux_host_class_hid_mouse_position_get

Fare konumunu al.

### <a name="prototype"></a>Prototype

```c
UINT ux_host_class_hid_mouse_position_get(
    UX_HOST_CLASS_HID_MOUSE *mouse_instance,
    SLONG *mouse_x_position, 
    SLONG *mouse_y_position);
```

### <a name="description"></a>Description

Bu işlev, x ve y koordinatlarında fare & için kullanılır.

### <a name="parameters"></a>Parametreler

- **mouse_instance** MOUSE fare örneğinin işaretçisi.
- **mouse_x_position** x koordinatı işaretçisi.
- **mouse_y_position** y koordinatı işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) X Y &amp; koordinatları başarıyla alındı.
- **UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) GIZLI SıNıF örneği yok.

### <a name="example"></a>Örnek

```c
/* The following example illustrates how to obtain mouse coordinates. */

UX_HOST_CLASS_HID_MOUSE *mouse_instance;

SLONG mouse_x_position;
SLONG mouse_y_position;

status = ux_host_class_hid_mouse_position_get(mouse_instance,
    &mouse_x_position, &mouse_y_position);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_hid_keyboard_key_get"></a>ux_host_class_hid_keyboard_key_get

Klavye anahtarını ve durumunu al.

### <a name="prototype"></a>Prototype

```c
UINT ux_host_class_hid_keyboard_key_get(
    UX_HOST_CLASS_HID_KEYBOARD *keyboard_instance,
    ULONG *keyboard_key, 
    ULONG *keyboard_state);
```

### <a name="description"></a>Description

Bu işlev, klavye anahtarını ve durumunu almak için kullanılır.

### <a name="parameters"></a>Parametreler

- **keyboard_instance** THE KLAVYE örneğinin işaretçisi.
- **keyboard_key** Klavye tuşu kapsayıcısı işaretçisi.
- **keyboard_state** Klavye durumu kapsayıcısı işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) Anahtarı ve durumu başarıyla alındı.
- **UX_ERROR** (0xff) Bildirecek bir şey yok.
- **UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) GIZLI SıNıF örneği yok.

Klavye durumu aşağıdaki değerlere sahip olabilir.

- **UX_HID_KEYBOARD_STATE_KEY_UP** 0x10000
- **UX_HID_KEYBOARD_STATE_NUM_LOCK** 0x0001
- **UX_HID_KEYBOARD_STATE_CAPS_LOCK** 0x0002
- **UX_HID_KEYBOARD_STATE_SCROLL_LOCK** 0x0004
- **UX_HID_KEYBOARD_STATE_MASK_LOCK** 0x0007
- **UX_HID_KEYBOARD_STATE_LEFT_SHIFT** 0x0100
- **UX_HID_KEYBOARD_STATE_RIGHT_SHIFT** 0x0200
- **UX_HID_KEYBOARD_STATE_SHIFT** 0x0300
- **UX_HID_KEYBOARD_STATE_LEFT_ALT** 0x0400
- **UX_HID_KEYBOARD_STATE_RIGHT_ALT** 0x0800
- **UX_HID_KEYBOARD_STATE_ALT** 0x0a00
- **UX_HID_KEYBOARD_STATE_LEFT_CTRL** 0x1000
- **UX_HID_KEYBOARD_STATE_RIGHT_CTRL** 0x2000
- **UX_HID_KEYBOARD_STATE_CTRL** 0x3000
- **UX_HID_KEYBOARD_STATE_LEFT_GUI** 0x4000
- **UX_HID_KEYBOARD_STATE_RIGHT_GUI** 0x8000
- **UX_HID_KEYBOARD_STATE_GUI** 0xa000

### <a name="example"></a>Örnek

```c
while (1)
{

    /* Get a key/state from the keyboard. */
    status = ux_host_class_hid_keyboard_key_get(keyboard,
        &keyboard_char, &keyboard_state);

    /* Check if there is something. */
    if (status == UX_SUCCESS)
    {

        #ifdef UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE
            if (keyboard_state & UX_HID_KEYBOARD_STATE_KEY_UP)
            {
                /* The key was released. */
            } else
            {
                /* The key was pressed. */
            }
        #endif

        /* We have a character in the queue. */
        keyboard_queue[keyboard_queue_index] = (UCHAR) keyboard_char;

        /* Can we accept more ? */
        if(keyboard_queue_index < 1024)
            keyboard_queue_index++;
    }

    tx_thread_sleep(10);

}
```

## <a name="ux_host_class_hid_keyboard_ioctl"></a>ux_host_class_hid_keyboard_ioctl

KEYBOARD klavyesi için bir IOCTL işlevi gerçekleştirin.

### <a name="prototype"></a>Prototype

```c
UINT ux_host_class_hid_keyboard_ioctl(
    UX_HOST_CLASS_HID_KEYBOARD *keyboard_instance,
    ULONG ioctl_function, VOID *parameter);
```

### <a name="description"></a>Description

Bu işlev, BELIRLI bir ioctl işlevini KEYBOARD klavyesi üzerinde gerçekleştirir. Çağrı engelliyor ve yalnızca bir hata olduğunda veya komut tamamlandığında döndürür.

### <a name="parameters"></a>Parametreler

- **keyboard_instance** THE KLAVYE örneğinin işaretçisi.
- **ioctl_function** ioctl işlevini kullanın. İzin verilen ioctl işlevlerinden biri için aşağıdaki tabloya bakın.
- **parametre** ioctl'ye özgü bir parametrenin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) ioctl işlevi başarıyla tamamlandı.
- **UX_FUNCTION_NOT_SUPPORTED** (0x54) Bilinmeyen IOCTL işlevi

### <a name="ioctl-functions"></a>IOCTL işlevleri

- UX_HID_KEYBOARD_IOCTL_SET_LAYOUT
- UX_HID_KEYBOARD_IOCTL_KEY_DECODING_ENABLE
- UX_HID_KEYBOARD_IOCTL_KEY_DECODING_DISABLE

### <a name="example--change-keyboard-layout"></a>Örnek – klavye düzenini değiştirme

```c
UINT status;

/* This example shows usage of the SET_LAYOUT IOCTL function.
    USBX receives raw key values from the device (these raw values
    are defined in the HID usage table specification) and optionally
    decodes them for application usage. The decoding is performed
    based on a set of arrays that act as maps – which array is used
    depends on the raw key value (i.e. keypad and non-keypad) and
    the current state of the keyboard (i.e. shift, caps lock, etc.). */

/* When the shift condition is not present and the raw key value
    is not within the keypad value range, this array will be used to decode the raw key value. */

static UCHAR keyboard_layout_raw_to_unshifted_map[] =
{
    0,0,0,0,
    'a','b','c','d','e','f','g',
    'h','i','j','k','l','m','n',
    'o','p','q','r','s','t',
    'u','v','w','x','y','z',
    '1','2','3','4','5','6','7','8','9','0',
    0x0d,0x1b,0x08,0x07,0x20,'-','=','[',']',
    '\\','#',';',0x27,'`',',','.','/',0xf0,
    0xbb,0xbc,0xbd,0xbe,0xbf,0xc0,0xc1,0xc2,0xc3,0xc4,0xc5,0xc6,
    0x00,0xf1,0x00,0xd2,0xc7,0xc9,0xd3,0xcf,0xd1,0xcd,0xcd,0xd0,0xc8,0xf2,
    '/','*','-','+',
    0x0d,'1','2','3','4','5','6','7','8','9','0','.','\\',0x00,0x00,'=',
    0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,
};

/* When the shift condition is present and the raw key value
    is not within the keypad value range, this array will be used to decode the raw key value. */

static UCHAR keyboard_layout_raw_to_shifted_map[] =
{
    0,0,0,0,
    'A','B','C','D','E','F','G',
    'H','I','J','K','L','M','N',
    'O','P','Q','R','S','T',
    'U','V','W','X','Y','Z',
    '!','@','#','$','%','^','&','*','(',')',
    0x0d,0x1b,0x08,0x07,0x20,'_','+','{','}',
    '|','~',':','"','~','<','>','?',0xf0,
    0xbb,0xbc,0xbd,0xbe,0xbf,0xc0,0xc1,0xc2,0xc3,0xc4,0xc5,0xc6,
    0x00,0xf1,0x00,0xd2,0xc7,0xc9,0xd3,0xcf,0xd1,0xcd,0xcd,0xd0,0xc8,0xf2,
    '/','*','-','+',
    0x0d,'1','2','3','4','5','6','7','8','9','0','.','\\',0x00,0x00,'=',
    0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,
};

/* When numlock is on and the raw key value is within the keypad
    value range, this array will be used to decode the raw key value. */

static UCHAR keyboard_layout_raw_to_numlock_on_map[] =
{
    '/','*','-','+',
    0x0d,'1','2','3','4','5','6','7','8','9','0','.','\\',0x00,0x00,'=',
};

/* When numlock is off and the raw key value is within the keypad value
    range, this array will be used to decode the raw key value. */
static UCHAR keyboard_layout_raw_to_numlock_off_map[] =
{
    '/','*','-','+',
    0x0d,0xcf,0xd0,0xd1,0xcb,'5',0xcd,0xc7,0xc8,0xc9,0xd2,0xd3,'\\',0x00,0x
    00,'=',
};

/* Specify the keyboard layout for USBX usage. */
static UX_HOST_CLASS_HID_KEYBOARD_LAYOUT keyboard_layout =
{
    keyboard_layout_raw_to_shifted_map,
    keyboard_layout_raw_to_unshifted_map,
    keyboard_layout_raw_to_numlock_on_map,
    keyboard_layout_raw_to_numlock_off_map,
    /* The maximum raw key value. Values larger than this are discarded. */
    UX_HID_KEYBOARD_KEYS_UPPER_RANGE,
    /* The raw key value for the letter 'a'. */
    UX_HID_KEYBOARD_KEY_LETTER_A,
    /* The raw key value for the letter 'z'. */
    UX_HID_KEYBOARD_KEY_LETTER_Z,
    /* The lower range raw key value for keypad keys - inclusive. */
    UX_HID_KEYBOARD_KEYS_KEYPAD_LOWER_RANGE,
    /* The upper range raw key value for keypad keys. */
    UX_HID_KEYBOARD_KEYS_KEYPAD_UPPER_RANGE
};

/* Call the IOCTL function to change the keyboard layout. */
status = ux_host_class_hid_keyboard_ioctl(keyboard,
    UX_HID_KEYBOARD_IOCTL_SET_LAYOUT, (VOID *)&keyboard_layout);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="example--disable-keyboard-key-decode"></a>Örnek – klavye tuşu kodunu devre dışı bırakma

```c
UINT status;

/* The following example illustrates IOCTL function of Disable key decode from keyboard layout. */
status = ux_host_class_hid_keyboard_ioctl(keyboard,
    UX_HID_KEYBOARD_IOCTL_DISABLE_KEYS_DECODE, UX_NULL);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_hid_remote_control_usage_get"></a>ux_host_class_hid_remote_control_usage_get

Uzaktan denetim kullanımını al

### <a name="prototype"></a>Prototype

```c
UINT ux_host_class_hid_remote_control_usage_get(
    UX_HOST_CLASS_HID_REMOTE_CONTROL *remote_control_instance,
    LONG *usage, 
    ULONG *value);
```

### <a name="description"></a>Description

Bu işlev, uzaktan denetim kullanımlarını almak için kullanılır.

### <a name="parameters"></a>Parametreler

- **remote_control_instance** UZAKTAN UZAKTAN denetim örneğinin işaretçisi.
- **kullanım** Kullanımın işaretçisi.
- **value (değer)** Kullanım değerinin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) Veri aktarımı tamamlandı.
- **UX_ERROR** (0xff) Bildirecek bir şey yok.
- **UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) GIZLI SıNıF örneği yok.

Tüm olası kullanımların listesi bu kullanıcı kılavuzuna sığmayacak kadar uzundur. Tam bir açıklama için ux_host_class_hid.h tüm olası değerler kümesine sahiptir.

### <a name="example"></a>Örnek

```c
/* Read usages and values as the user changes the vol/bass/treble buttons on the speaker */

while (remote_control != UX_NULL)
{
    status = ux_host_class_hid_remote_control_usage_get(remote_control, &usage, &value);
    if (status == UX_SUCCESS)
    {
        /* We have something coming from the HID remote control,
        we filter the usage here and only allow the
        volume usage which can be VOLUME, VOLUME_INCREMENT or VOLUME_DECREMENT */
        switch(usage)
        {
            case UX_HOST_CLASS_HID_CONSUMER_VOLUME :
            case UX_HOST_CLASS_HID_CONSUMER_VOLUME_INCREMENT :
            case UX_HOST_CLASS_HID_CONSUMER_VOLUME_DECREMENT :

            if (value<0x80)
            {
                if (current_volume + audio_control.ux_host_class_audio_control_res < 0xffff)
                    current_volume = current_volume + audio_control.ux_host_class_audio_control_res;
                } else {
                if (current_volume > audio_control.ux_host_class_audio_control_res)
                    current_volume = current_volumeaudio_control.ux_host_class_audio_control_res;
            }

            audio_control.ux_host_class_audio_control_channel = 1;
            audio_control.ux_host_class_audio_control = UX_HOST_CLASS_AUDIO_VOLUME_CONTROL;
            audio_control.ux_host_class_audio_control_cur = current_volume;
            status = ux_host_class_audio_control_value_set(audio, &audio_control);
            audio_control.ux_host_class_audio_control_channel = 2;
            audio_control.ux_host_class_audio_control = UX_HOST_CLASS_AUDIO_VOLUME_CONTROL;
            audio_control.ux_host_class_audio_control_cur = current_volume;
            status = ux_host_class_audio_control_value_set(audio, &audio_control);
            break;

        }
    }
    tx_thread_sleep(10);

}
```

### <a name="ux_host_class_cdc_acm_read"></a>ux_host_class_cdc_acm_read

Cdc_acm arabiriminden okuyun.

### <a name="prototype"></a>Prototype

```c
UINT ux_host_class_cdc_acm_read(
    UX_HOST_CLASS_CDC_ACM *cdc_acm,
    UCHAR *data_pointer,
    ULONG requested_length,
    ULONG *actual_length);
```

### <a name="description"></a>Description

Bu işlev, cdc_acm okur. Çağrı engelliyor ve yalnızca bir hata olduğunda veya aktarım tamamlandığında döndürür.

> [!Note]
> Bu işlevler, ham toplu verileri cihazdan okur, bu nedenle arabellek dolu olana veya cihaz aktarımı kısa bir paketle (Sıfır Uzunluk Paketi dahil) sonlandırana kadar beklemede tutar. Daha fazla ayrıntı için lütfen Toplu [**Aktarımda Dikkat Edilmesi Gereken Genel Noktalar'a bakın.**](usbx-device-stack-5.md#general-considerations-for-bulk-transfer)

### <a name="parameters"></a>Parametreler

- **cdc_acm** Cdc_acm sınıfı örneğine işaretçi.
- **data_pointer** Veri yükünün arabellek adresinin işaretçisi.
- **requested_length** Alınan uzunluk.
- **actual_length** Aslında uzunluk alındı.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) Veri aktarımı tamamlandı.
- **UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) cdc_acm örneği geçersiz.
- **UX_TRANSFER_TIMEOUT** (0x5c) Aktarım zaman aşımı, okuma tamamlanmamış.

### <a name="example"></a>Örnek

```c
UINT status;

/* The following example illustrates this service. */

status = ux_host_class_cdc_acm_read(cdc_acm, data_pointer,
    requested_length, &actual_length);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_cdc_acm_write"></a>ux_host_class_cdc_acm_write

Cdc_acm arabirimine yazma

### <a name="prototype"></a>Prototype

```c
UINT ux_host_class_cdc_acm_write(
    UX_HOST_CLASS_CDC_ACM *cdc_acm,
    UCHAR *data_pointer, 
    ULONG requested_length, 
    ULONG *actual_length);
```

### <a name="description"></a>Description

Bu işlev, cdc_acm yazar. Çağrı engelliyor ve yalnızca bir hata olduğunda veya aktarım tamamlandığında döndürür.

### <a name="parameters"></a>Parametreler

- **cdc_acm** Cdc_acm sınıfı örneğine işaretçi.
- **data_pointer** Veri yükünün arabellek adresinin işaretçisi.
- **requested_length** Gönderilecek uzunluk.
- **actual_length** Aslında gönderilen uzunluk.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) Veri aktarımı tamamlandı.
- **UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) cdc_acm örneği geçersiz.
- **UX_TRANSFER_TIMEOUT** (0x5c) Aktarım zaman aşımı, yazma eksik.

### <a name="example"></a>Örnek

```c
UINT status;

/* The following example illustrates this service. */

status = ux_host_class_cdc_acm_write(cdc_acm, data_pointer,
    requested_length, &actual_length);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_cdc_acm_ioctl"></a>ux_host_class_cdc_acm_ioctl

Cdc_acm arabirimine bir IOCTL işlevi gerçekleştirin.

### <a name="prototype"></a>Prototype

```c
UINT ux_host_class_cdc_acm_ioctl(
    UX_HOST_CLASS_CDC_ACM *cdc_acm,
    ULONG ioctl_function, 
    VOID *parameter);
```

### <a name="description"></a>Description

Bu işlev, belirli bir ioctl işlevini cdc_acm gerçekleştirir. Çağrı engelliyor ve yalnızca bir hata olduğunda veya komut tamamlandığında döndürür.

### <a name="parameters"></a>Parametreler

- **cdc_acm** Cdc_acm sınıfı örneğine işaretçi.
- **ioctl_function** ioctl işlevini kullanın. İzin verilen ioctl işlevlerinden biri için aşağıdaki tabloya bakın.
- **parametre** ioctl'ye özgü parametre işaretçisi

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) Veri aktarımı tamamlandı.
- **UX_MEMORY_INSUFFICIENT** (0x12) Yeterli bellek yok.
- **UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) CDC-ACM örneği geçersiz durumda.
- **UX_FUNCTION_NOT_SUPPORTED** (0x54) Bilinmeyen IOCTL işlevi.

### <a name="ioctl-functions"></a>IOCTL işlevleri:

- UX_HOST_CLASS_CDC_ACM_IOCTL_SET_LINE_CODING
- UX_HOST_CLASS_CDC_ACM_IOCTL_GET_LINE_CODING
- UX_HOST_CLASS_CDC_ACM_IOCTL_SET_LINE_STATE
- UX_HOST_CLASS_CDC_ACM_IOCTL_SEND_BREAK
- UX_HOST_CLASS_CDC_ACM_IOCTL_ABORT_IN_PIPE
- UX_HOST_CLASS_CDC_ACM_IOCTL_ABORT_OUT_PIPE
- UX_HOST_CLASS_CDC_ACM_IOCTL_NOTIFICATION_CALLBACK
- UX_HOST_CLASS_CDC_ACM_IOCTL_GET_DEVICE_STATUS

```c
UINT status;

/* The following example illustrates this service. */

status = ux_host_class_cdc_acm_ioctl(cdc_acm,
    UX_HOST_CLASS_CDC_ACM_IOCTL_GET_LINE_CODING, (VOID *)&line_coding);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_cdc_acm_reception_start"></a>ux_host_class_cdc_acm_reception_start

Cihazdan verilerin arka planda alımını başlar.

### <a name="prototype"></a>Prototype

```c
UINT ux_host_class_cdc_acm_reception_start(
    UX_HOST_CLASS_CDC_ACM *cdc_acm,
    UX_HOST_CLASS_CDC_ACM_RECEPTION *cdc_acm_reception);
```

### <a name="description"></a>Description

Bu işlev, USBX'in arka planda cihazdan sürekli veri okuması sağlar. Her işlem tamamlandıktan sonra, cdc_acm_reception  uygulamanın işlem verilerini daha fazla işlemesi için bu işlemde belirtilen geri çağırma çağrılır.

> [!NOTE]
> **ux_host_class_cdc_acm_read,** arka plan sinyal alımı kullanılırken kullanılmamalı.

### <a name="parameters"></a>Parametreler

- **cdc_acm** Cdc_acm sınıfı örneğine işaretçi.
- **cdc_acm_reception** Arka plan alımının davranışını tanımlayan değerleri içeren parametre işaretçisi. Bu parametrenin düzeni şu şekildedir:

```c
typedef struct UX_HOST_CLASS_CDC_ACM_RECEPTION_STRUCT
{
    ULONG ux_host_class_cdc_acm_reception_state;
    ULONG ux_host_class_cdc_acm_reception_block_size;
    UCHAR *ux_host_class_cdc_acm_reception_data_buffer;
    ULONG ux_host_class_cdc_acm_reception_data_buffer_size;
    UCHAR *ux_host_class_cdc_acm_reception_data_head;
    UCHAR *ux_host_class_cdc_acm_reception_data_tail;
    VOID (*ux_host_class_cdc_acm_reception_callback)(struct UX_HOST_CLASS_CDC_ACM_STRUCT *cdc_acm,
        UINT status, UCHAR *reception_buffer, ULONG reception_size);
} UX_HOST_CLASS_CDC_ACM_RECEPTION;
```

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) Arka plan sinyal alımı başarıyla başlatıldı.
- **UX_HOST_CLASS_INSTANCE _UNKNOWN** (0x5b) Yanlış sınıf örneği.

```c
UINT status;
UX_HOST_CLASS_CDC_ACM_RECEPTION cdc_acm_reception;

/* Setup the background reception parameter. */

/* Set the desired max read size for each transaction.
    For example, if this value is 64, then the maximum amount of
    data received from the device in a single transaction is 64.
    If the amount of data received from the device is less than this value,
    the callback will still be invoked with the actual amount of data received. */
cdc_acm_reception.ux_host_class_cdc_acm_reception_block_size = block_size;

/* Set the buffer where the data from the device is read to. */
cdc_acm_reception.ux_host_class_cdc_acm_reception_data_buffer = cdc_acm_reception_buffer;

/* Set the size of the data reception buffer.
    Note that this should be at least as large as ux_host_class_cdc_acm_reception_block_size. */
cdc_acm_reception.ux_host_class_cdc_acm_reception_data_buffer_size = cdc_acm_reception_buffer_size;

/* Set the callback that is to be invoked upon each reception transfer completion. */
cdc_acm_reception.ux_host_class_cdc_acm_reception_callback = reception_callback;

/* Start background reception using the values we defined in the reception parameter. */
status = ux_host_class_cdc_acm_reception_start(cdc_acm_host_data, &cdc_acm_reception);

/* If status equals UX_SUCCESS, background reception has successfully started. */
```

## <a name="ux_host_class_cdc_acm_reception_stop"></a>ux_host_class_cdc_acm_reception_stop

Paketlerin arka plan alımını durdurur.

### <a name="prototype"></a>Prototype

```c
UINT ux_host_class_cdc_acm_reception_stop(
    UX_HOST_CLASS_CDC_ACM *cdc_acm,
    UX_HOST_CLASS_CDC_ACM_RECEPTION *cdc_acm_reception);
```

### <a name="description"></a>Description

Bu işlev, USBX'in önceden tarafından başlatılan arka plan alımını **durdurması** ux_host_class_cdc_acm_reception_start.

### <a name="parameters"></a>Parametreler

- **cdc_acm** Cdc_acm sınıfı örneğine işaretçi.
- **cdc_acm_reception** Arka plan alımını başlatmak için kullanılan aynı parametrenin işaretçisi. Bu parametrenin düzeni şu şekildedir:

```c
typedef struct UX_HOST_CLASS_CDC_ACM_RECEPTION_STRUCT
{
    ULONG ux_host_class_cdc_acm_reception_state;
    ULONG ux_host_class_cdc_acm_reception_block_size;
    UCHAR *ux_host_class_cdc_acm_reception_data_buffer;
    ULONG ux_host_class_cdc_acm_reception_data_buffer_size;
    UCHAR *ux_host_class_cdc_acm_reception_data_head;
    UCHAR *ux_host_class_cdc_acm_reception_data_tail;
    VOID (*ux_host_class_cdc_acm_reception_callback)(
            struct UX_HOST_CLASS_CDC_ACM_STRUCT *cdc_acm, UINT status,
            UCHAR *reception_buffer, ULONG reception_size);
} UX_HOST_CLASS_CDC_ACM_RECEPTION;
```

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) Arka plan sinyal başarıyla durduruldu.
- **UX_HOST_CLASS_INSTANCE _UNKNOWN** (0x5b) Yanlış sınıf örneği.

```c
UINT status;
UX_HOST_CLASS_CDC_ACM_RECEPTION cdc_acm_reception;

/* Stop background reception. The reception parameter should be the same
    that was passed to ux_host_class_cdc_acm_reception_start. */
status = ux_host_class_cdc_acm_reception_stop(cdc_acm, &cdc_acm_reception);

/* If status equals UX_SUCCESS, background reception has successfully stopped. */
```
