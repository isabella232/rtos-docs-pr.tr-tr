---
title: Bölüm 4 - USBX Konak Hizmetlerinin Açıklaması
description: USBX Konak Hizmetleri hakkında bilgi öğrenin.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 6cbeff83d8e3812f13aa3f8f66d4013b70490d556911939186b4b43840aac50d
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116790692"
---
# <a name="chapter-4---description-of-usbx-host-services"></a>Bölüm 4 - USBX Konak Hizmetlerinin Açıklaması

## <a name="ux_host_stack_initialize"></a>ux_host_stack_initialize

Konak işlemi için USBX'i başlatma.

### <a name="prototype"></a>Prototype

```c
UINT ux_host_stack_initialize(
    UINT (*system_change_function)
    (ULONG, UX_HOST_CLASS *));
```

### <a name="description"></a>Description

Bu işlev USB konak yığınını başlatacak. Sağlanan bellek alanı USBX iç kullanımı için ayarlanmalıdır. Bu UX_SUCCESS döndürülürse, USBX konak denetleyicisi ve sınıf kaydı için hazırdır.

### <a name="input-parameter"></a>Giriş Parametresi

- **system_change_function** Cihaz değişikliklerini uygulamaya bildirmek için isteğe bağlı geri çağırma yordamının işaretçisi.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) Başarılı başlatma.
- **UX_MEMORY_INSUFFICIENT** (0x12) Bellek ayırma başarısız oldu.

### <a name="example"></a>Örnek

```c
UINT status;

/* Initialize USBX for host operation, without notification. */
status = ux_host_stack_initialize(UX_NULL);

/* If status equals UX_SUCCESS, USBX has been successfully initialized for host operation. */
```

## <a name="ux_host_stack_endpoint_transfer_abort"></a>ux_host_stack_endpoint_transfer_abort

Bir uç nokta için aktarım isteğine eklenmiş olan tüm işlemleri iptal edin.

### <a name="prototype"></a>Prototype

```c
UINT ux_host_stack_endpoint_transfer_abort(UX_ENDPOINT *endpoint);
```

### <a name="description"></a>Description

Bu işlev, bir uç noktasına eklenmiş olan belirli bir aktarım isteği için etkin veya bekleyen tüm işlemleri iptal eder. Aktarım isteğine bağlı bir geri çağırma işlevi vardır, geri çağırma işlevi de durum UX_TRANSACTION_ABORTED çağrılır.

### <a name="input-parameter"></a>Giriş Parametresi

- **uç nokta** Bir uç noktanın işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) Hata yok.
- **UX_ENDPOINT_HANDLE_UNKNOWN** (0x53) Uç nokta tanıtıcısı geçerli değil.

### <a name="example"></a>Örnek

```c
UX_HOST_CLASS_PRINTER *printer;
UINT status;

/* Get the instance for this class. */
printer = (UX_HOST_CLASS_PRINTER *) command ->
    ux_host_class_command_instance;

/* The printer is being shut down. */

printer -> printer_state = UX_HOST_CLASS_INSTANCE_SHUTDOWN;

/* We need to abort transactions on the bulk out pipe. */
status = ux_host_stack_endpoint_transfer_abort
    (printer -> printer_bulk_out_endpoint);

/* If status equals UX_SUCCESS, the operation was successful */
```

## <a name="ux_host_stack_class_get"></a>ux_host_stack_class_get

Sınıf kapsayıcısı işaretçisini elde edin.

### <a name="prototype"></a>Prototype

```c
UINT ux_host_stack_class_get(
    UCHAR *class_name,
    UX_HOST_CLASS **class);
```

### <a name="description"></a>Description

Bu işlev sınıf kapsayıcısı için bir işaretçi döndürür. Sınıf veya uygulama bir cihazı açmak istediği zaman örnekleri aramak için bir sınıfın KAPSAYıCısını USB yığınından almaları gerekir.

> [!NOTE]
> C dizesinin class_name NULL ile sonlandırılmalı ve uzunluğu (NULL-sonlandırıcının kendisi olmadan) UX_MAX_CLASS_NAME_LENGTH.

### <a name="parameters"></a>Parametreler

- **class_name** Sınıf adının işaretçisi.
- **class** Sınıfın adı için sınıf kapsayıcısını içeren işlev çağrısı tarafından güncelleştirilen bir işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) Hata yok, dönüşte sınıf alanı sınıf kapsayıcısı işaretçisi ile birlikte dosyalandı.
- **UX_HOST_CLASS_UNKNOWN** (0x59) Sınıfı yığın tarafından bilinmiyor.

### <a name="example"></a>Örnek

```c
UX_HOST_CLASS *printer_container;
UINT status;

/* Get the container for this class. */
status = ux_host_stack_class_get("ux_host_class_printer", &printer_container);

/* If status equals UX_SUCCESS, the operation was successful */
```

## <a name="ux_host_stack_class_register"></a>ux_host_stack_class_register

USB sınıfını USB yığınına kaydetme.

### <a name="prototype"></a>Prototype

```c
UINT ux_host_stack_class_register(
    UCHAR *class_name,
    UINT (*class_entry_address) (struct UX_HOST_CLASS_COMMAND_STRUCT *));
```

### <a name="description"></a>Description

Bu işlev BIR USB sınıfını USB yığınına kaydedmektedir. sınıfı, USB yığınının aşağıdaki gibi komutları göndermesi için bir giriş noktası belirterek.

- **UX_HOST_CLASS_COMMAND_QUERY**
- **UX_HOST_CLASS_COMMAND_ACTIVATE**
- **UX_HOST_CLASS_COMMAND_DESTROY**

> [!NOTE]
> Dizenin C *class_name* NULL ile sonlandırılmalı ve uzunluğu (NULL-sonlandırıcının kendisi olmadan) değerine göre **UX_MAX_CLASS_NAME_LENGTH.**

### <a name="parameters"></a>Parametreler

- **class_name** Sınıfın adına işaretçi, geçerli girişler USBX USB Sınıfları altında ux_system_initialize.c dosyasında bulunur.
- **class_entry_address** Sınıfının giriş işlevinin adresi.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) Sınıfı başarıyla yüklendi.
- **UX_MEMORY_ARRAY_FULL** (0x1a) Bu sınıfı depolamak için daha fazla bellek yok.
- **UX_HOST_CLASS_ALREADY_INSTALLED** (0x58) Konak sınıfı zaten yüklü.

### <a name="example"></a>Örnek:

```c
UINT status;

/* Register all the classes for this implementation. */
status = ux_host_stack_class_register("ux_host_class_hub", ux_host_class_hub_entry);

/* If status equals UX_SUCCESS, class was successfully installed. */
```

## <a name="ux_host_stack_class_instance_create"></a>ux_host_stack_class_instance_create

Bir sınıf kapsayıcısı için yeni bir sınıf örneği oluşturun.

### <a name="prototype"></a>Prototype

```c
UINT ux_host_stack_class_instance_create(
    UX_HOST_CLASS *class, 
    VOID *class_instance);
```

### <a name="description"></a>Description

Bu işlev, bir sınıf kapsayıcısı için yeni bir sınıf örneği oluşturur. Bir sınıfın örneği, sınıf karmaşıklığını azaltmak için sınıf kodunda yer alan bir örnek değildir. Bunun yerine, her sınıf örneği ana yığında bulunan sınıf kapsayıcısı ekli.

### <a name="parameters"></a>Parametreler

- **class** Sınıf kapsayıcısı işaretçisi.
- **class_instance** Oluşturulacak sınıf örneğine işaretçi.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) Sınıf örneği sınıf kapsayıcıya ekli.

### <a name="example"></a>Örnek

```c
UINT status;

UX_HOST_CLASS_PRINTER *printer;

/* Obtain memory for this class instance. */

printer = ux_memory_allocate(UX_NO_ALIGN, sizeof(UX_HOST_CLASS_PRINTER));

if (printer == UX_NULL)
    return(UX_MEMORY_INSUFFICIENT);

/* Store the class container into this instance. */
printer -> printer_class = command -> ux_host_class;

/* Create this class instance. */
status = ux_host_stack_class_instance_create(printer -> printer_class, (VOID *)printer);

/* If status equals UX_SUCCESS, the class instance was successfully created and attached to the class container. */
```

## <a name="ux_host_stack_class_instance_destroy"></a>ux_host_stack_class_instance_destroy

Sınıf kapsayıcısı için bir sınıf örneğini yok edin.

### <a name="prototype"></a>Prototype

```c
UINT ux_host_stack_class_instance_destroy(
    UX_HOST_CLASS *class, 
    VOID *class_instance);
```

### <a name="description"></a>Description

Bu işlev bir sınıf kapsayıcısı için bir sınıf örneğini yok eder.

### <a name="parameters"></a>Parametreler

- **class** Sınıf kapsayıcısı işaretçisi.
- **class_instance** Yok etmek için örneğin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) Sınıf örneği yok edildi.
- **UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) Sınıf örneği sınıf kapsayıcıya bağlı değil.

### <a name="example"></a>Örnek

```c
UINT status;
UX_HOST_CLASS_PRINTER *printer;

/* Get the instance for this class. */
printer = (UX_HOST_CLASS_PRINTER *) command -> ux_host_class_command_instance;

/* The printer is being shut down. */
printer -> printer_state = UX_HOST_CLASS_INSTANCE_SHUTDOWN;

/* Destroy the instance. */
status = ux_host_stack_class_instance_destroy(printer -> printer_class, (VOID *) printer);

/* If status equals UX_SUCCESS, the class instance was successfully destroyed. */
```

## <a name="ux_host_stack_class_instance_get"></a>ux_host_stack_class_instance_get

Belirli bir sınıf için bir sınıf örneği işaretçisi elde.

### <a name="prototype"></a>Prototype

```c
UINT ux_host_stack_class_instance_get(
    UX_HOST_CLASS *class,
    UINT class_index, 
    VOID **class_instance);
```

### <a name="description"></a>Description

Bu işlev, belirli bir sınıf için bir sınıf örneği işaretçisi döndürür. Bir sınıfın örneği, sınıf karmaşıklığını azaltmak için sınıf kodunda yer alan bir örnek değildir. Bunun yerine, her sınıf örneği sınıf kapsayıcısı ekli. Bu işlev, bir sınıf kapsayıcısı içindeki sınıf örneklerini aramak için kullanılır.

### <a name="parameters"></a>Parametreler

- **class** Sınıf kapsayıcısı işaretçisi.
- **class_index** Kapsayıcıya eklenmiş sınıflar listesinde işlev çağrısı tarafından kullanılacak dizin.
- **class_instance** İşlev çağrısı tarafından döndürülen örneğin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) Sınıf örneği bulundu.

- **UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) Sınıf kapsayıcısı ekli başka sınıf örneği yok.

### <a name="example"></a>Örnek

```c
UINT status;

UX_HOST_CLASS_PRINTER *printer;

/* Obtain memory for this class instance. */
printer = ux_memory_allocate(UX_NO_ALIGN, sizeof(UX_HOST_CLASS_PRINTER));

if (printer == UX_NULL) return(UX_MEMORY_INSUFFICIENT);

/* Search for instance index 2. */
status = ux_host_stack_class_instance_get(class, 2, (VOID *) printer);

/* If status equals UX_SUCCESS, the class instance was found. */
```

## <a name="ux_host_stack_device_configuration_get"></a>ux_host_stack_device_configuration_get

Yapılandırma kapsayıcısı işaretçisi elde edin.

### <a name="prototype"></a>Prototype

```c
UINT ux_host_stack_device_configuration_get(
    UX_DEVICE *device,
    UINT configuration_index, 
    UX_CONFIGURATION *configuration);
```

### <a name="description"></a>Description

Bu işlev, cihaz tanıtıcısı ve yapılandırma dizinini temel alan bir yapılandırma kapsayıcısı döndürür.

### <a name="parameters"></a>Parametreler

- **cihaz** İstenen yapılandırmanın sahibi olan cihaz kapsayıcısı işaretçisi.
- **configuration_index** Aranacak yapılandırma dizini.
- **yapılandırma** Döndürülacak yapılandırma kapsayıcısı işaretçisinin adresi.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) Yapılandırma bulundu.
- **UX_DEVICE_HANDLE_UNKNOWN** (0x50) Cihaz kapsayıcısı yok.
- **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) Dizin için yapılandırma tanıtıcısı yok.

### <a name="example"></a>Örnek

```c
UINT status;

UX_HOST_CLASS_PRINTER *printer;

/* If the device has been configured already, we don't need to do it
again. */

if (printer -> printer_device -> ux_device_state == UX_DEVICE_CONFIGURED)
    return(UX_SUCCESS);

/* A printer normally has one configuration, retrieve 1st configuration only. */

status = ux_host_stack_device_configuration_get(printer -> printer_device,
    0, configuration);

/* If status equals UX_SUCCESS, the configuration was found. */
```

## <a name="ux_host_stack_device_configuration_select"></a>ux_host_stack_device_configuration_select

Bir cihaz için belirli bir yapılandırma seçin.

### <a name="prototype"></a>Prototype

```c
UINT ux_host_stack_device_configuration_select (UX_CONFIGURATION *configuration);
```

### <a name="description"></a>Description

Bu işlev, bir cihaz için belirli bir yapılandırmayı seçer. Bu yapılandırma cihaza ayarlanırsa, varsayılan olarak cihazda her cihaz arabirimi ve ilişkili alternatif ayar 0 etkinleştirilir. Cihaz/arabirim sınıfı belirli bir arabirimin ayarını değiştirmek isterse, bir hizmet çağrısı **ux_host_stack_interface_setting_select** gerekir.

### <a name="parameters"></a>Parametreler

- **yapılandırma** Bu cihaz için etkinleştirilen yapılandırma kapsayıcısı işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) Yapılandırma seçimi başarılı oldu.
- **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) Yapılandırma tanıtıcısı yok.
- **UX_OVER_CURRENT_CONDITION** (0x43) Bu yapılandırma için veri veri 0x43 üzerinde bir koşul var.

### <a name="example"></a>Örnek

```c
UINT status;

UX_HOST_CLASS_PRINTER *printer;

/* If the device has been configured already, we don't need to do it again. */
if (printer -> printer_device -> ux_device_state == UX_DEVICE_CONFIGURED)
    return(UX_SUCCESS);

/* A printer normally has one configuration - retrieve 1st configuration only. */
status = ux_host_stack_device_configuration_get(printer -> printer_device, 0,configuration);

/* If status equals UX_SUCCESS, the configuration selection was successful. */

/* If valid configuration, ask USBX to set this configuration. */
status = ux_host_stack_device_configuration_select(configuration);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_stack_device_get"></a>ux_host_stack_device_get

Cihaz kapsayıcısı işaretçisi elde edin.

### <a name="prototype"></a>Prototype

```c
UINT ux_host_stack_device_get(
    ULONG device_index, 
    UX_DEVICE *device);
```

### <a name="description"></a>Description

Bu işlev, dizinine göre bir cihaz kapsayıcısı döndürür. Cihaz dizini 0 ile başlar. Birden fazla denetleyicimiz olabileceği ve bir byte dizininin yeterli olamayy olabileceği için dizinin bir ULONG olduğunu unutmayın. Cihaz dizini, bus'a özgü cihaz adresiyle karıştırılmamalıdır.

### <a name="parameters"></a>Parametreler

- **device_index** Cihazın dizini.
- **cihaz** Geri dönecek cihaz kapsayıcısı işaretçisinin adresi.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) Cihaz kapsayıcısı var ve döndürülür
- **UX_DEVICE_HANDLE_UNKNOWN** (0x50) Cihaz bilinmiyor

### <a name="example"></a>Örnek

```c
UINT status;

/* Locate the first device in USBX. */
status = ux_host_stack_device_get(0, device);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_stack_interface_endpoint_get"></a>ux_host_stack_interface_endpoint_get

Uç nokta kapsayıcısı al.

### <a name="prototype"></a>Prototype

```c
UINT ux_host_stack_interface_endpoint_get(
    UX_INTERFACE *interface,
    UINT endpoint_index,
    UX_ENDPOINT *endpoint);
```

### <a name="description"></a>Description

Bu işlev, arabirim tanıtıcısı ve uç nokta dizinini temel alan bir uç nokta kapsayıcısı döndürür. Arabirim için alternatif ayarın seçili olduğu veya varsayılan ayarın, uç noktaların aranmadan önce kullandığı varsayılır.

### <a name="parameters"></a>Parametreler

- **interface (arabirim)** İstenen uç noktayı içeren arabirim kapsayıcısı işaretçisi.
- **endpoint_index** Bu arabirimde uç noktanın dizini.
- **uç nokta** Döndürülacak uç nokta kapsayıcısı adresi.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) Uç nokta kapsayıcısı var ve döndürülür.
- **UX_INTERFACE_HANDLE_UNKNOWN** (0x52) Arabirimi yok.
- **UX_ENDPOINT_HANDLE_UNKNOWN** (0x53) Uç nokta dizini yok.

### <a name="example"></a>Örnek

```c
UINT status;
UX_HOST_CLASS_PRINTER *printer;

for(endpoint_index = 0;
    endpoint_index < printer -> printer_interface ->
        ux_interface_descriptor.bNumEndpoints;
    endpoint_index++)
{
    status = ux_host_stack_interface_endpoint_get (printer -> printer_interface,
        endpoint_index, &endpoint);

    if (status == UX_SUCCESS)
    {
        /* Check if endpoint is bulk and OUT. */
        if (((endpoint -> ux_endpoint_descriptor.bEndpointAddress &
            UX_ENDPOINT_DIRECTION) == UX_ENDPOINT_OUT) &&
            ((endpoint -> ux_endpoint_descriptor.bmAttributes &
            UX_MASK_ENDPOINT_TYPE) == UX_BULK_ENDPOINT))
        return(UX_SUCCESS);
    }
}
```

## <a name="ux_host_stack_hcd_register"></a>ux_host_stack_hcd_register

USB denetleyicisini USB yığınına kaydetme.

### <a name="prototype"></a>Prototype

```c
UINT ux_host_stack_hcd_register(
    UCHAR *hcd_name,
    UINT (*hcd_function)(struct UX_HCD_STRUCT *),
    ULONG hcd_param1, ULONG hcd_param2);
```

### <a name="description"></a>Description

Bu işlev USB denetleyicisini USB yığınına kaydedmektedir. Asıl olarak bu denetleyici tarafından kullanılan belleği ayırır ve başlatma komutunu denetleyiciye iletir.

### <a name="parameters"></a>Parametreler

- **hcd_name** Konak denetleyicisinin adı
- **hcd_function** Başlatmadan sorumlu konak denetleyicisinde işlevi.
- **hcd_param1** Hcd tarafından kullanılan G/Ç veya bellek kaynağı.
- **hcd_param2** Konak denetleyicisi tarafından kullanılan IRQ.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) Denetleyici düzgün şekilde başlatıldı.
- **UX_MEMORY_INSUFFICIENT** (0x12) Bu denetleyici için yeterli bellek yok.
- **UX_PORT_RESET_FAILED** (0x31) Denetleyici sıfırlanamadı.
- **UX_CONTROLLER_INIT_FAILED** (0x32) Denetleyici düzgün başlatılamadı.

### <a name="example"></a>Örnek

```c
UINT status;

/* Initialize a host controller mapped at address 0xd0000 and using IRQ 10. */

status = ux_host_stack_hcd_register("ux_hcd_controller",
    ux_hcd_controller_initialize, 0xd0000, 0x0a);

/* If status equals UX_SUCCESS, the controller was initialized properly. */

/* Note that the application must also setup a call to the
    interrupt handler for the controller.
    The function for the controller is called _ux_hch_controller_interrupt_handler. */
```

## <a name="ux_host_stack_configuration_interface_get"></a>ux_host_stack_configuration_interface_get

Arabirim kapsayıcısı işaretçisi elde edin.

### <a name="prototype"></a>Prototype

```c
UINT ux_host_stack_configuration_interface_get (
    UX_CONFIGURATION *configuration,
    UINT interface_index, 
    UINT alternate_setting_index, 
    UX_INTERFACE **interface);
```

### <a name="description"></a>Description

Bu işlev yapılandırma tanıtıcısı, arabirim dizini ve alternatif ayar dizini temel alan bir arabirim kapsayıcısı döndürür.

### <a name="parameters"></a>Parametreler

- **yapılandırma** Arabirimin sahibi olan yapılandırma kapsayıcısı işaretçisi.
- **interface_index** Aranacak arabirim dizini.
- **alternate_setting_index** Arama yapmak için arabirim içinde alternatif ayar.
- **interface (arabirim)** Döndürülacak arabirim kapsayıcı işaretçisinin adresi.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) Arabirim dizini için arabirim kapsayıcısı ve alternatif ayar bulundu ve döndürüldü.
- **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) Yapılandırma yok.
- **UX_INTERFACE_HANDLE_UNKNOWN** (0x52) Arabirim yok.

### <a name="example"></a>Örnek

```c
UINT status;

/* Search for the default alternate setting on the first interface for the printer. */
status = ux_host_stack_configuration_interface_get(configuration, 0, 0,
    &printer -> printer_interface);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_stack_interface_setting_select"></a>ux_host_stack_interface_setting_select

Arabirim için alternatif bir ayar seçin.

### <a name="prototype"></a>Prototype

```c
UINT ux_host_stack_interface_setting_select(UX_INTERFACE *interface);
```

### <a name="description"></a>Description

Bu işlev, seçilen yapılandırmaya ait belirli bir arabirim için belirli bir alternatif ayarı seçer. Bu işlev, varsayılan alternatif ayardan yeni bir ayara değiştirmek veya varsayılan alternatif ayara geri dönmek için kullanılır. Yeni bir alternatif ayar seçildiğinde, önceki uç nokta özellikleri geçersizdir ve yeniden yükleniyor olmalıdır.

### <a name="input-parameter"></a>Giriş Parametresi

- **interface (arabirim)** Alternatif ayarı seçilecek arabirim kapsayıcısı işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) Bu arabirim için alternatif ayar başarıyla seçildi.
- **UX_INTERFACE_HANDLE_UNKNOWN** (0x52) arabirim yok.

### <a name="example"></a>Örnek

```c
UINT status;

/* Select a new alternate setting for this interface. */
status = ux_host_stack_interface_setting_select(interface);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_stack_transfer_request_abort"></a>ux_host_stack_transfer_request_abort

Bekleyen bir aktarım isteğini iptal edin.

### <a name="prototype"></a>Prototype

```c
UINT ux_host_stack_transfer_request_abort(UX_TRANSFER REQUEST *transfer request);
```

### <a name="description"></a>Description

Bu işlev, daha önce gönderilen bir bekleyen aktarım isteğini iptal eder. Bu işlev yalnızca belirli bir aktarım isteğini iptal eder. İşleve geri çağrı UX_TRANSFER REQUEST_STATUS_ABORT durumuna sahip olur.

### <a name="parameters"></a>Parametreler

- **aktarım isteği** İptal edilecek aktarım isteğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) bu aktarım isteğinin USB aktarımı iptal edildi.

### <a name="example"></a>Örnek

```c
UINT status;

/* The following example illustrates this service. */
status = ux_host_stack_transfer_request_abort(transfer request);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_stack_transfer_request"></a>ux_host_stack_transfer_request

Bir USB aktarımı isteyin.

### <a name="prototype"></a>Prototype

```c
UINT ux_host_stack_transfer_request(UX_TRANSFER REQUEST *transfer request);
```

### <a name="description"></a>Description

Bu işlev bir USB işlemi gerçekleştirir. Girişte, aktarım isteği bu işlem için seçili uç nokta kanalını ve aktarımıyla ilişkili parametreleri (veri yükü, işlem uzunluğu) sağlar. Denetim kanalı için, işlem engelleniyor ve yalnızca denetim aktarımının üç aşaması tamamlandığında veya önceki bir hata varsa döndürülür. Diğer kanallar için, USB yığını işlemi USB üzerinde zamanlar, ancak tamamlanmasını beklemez. Engelleyici olmayan kanallara yönelik her aktarım isteğinin bir tamamlama yordamı işleyicisi belirtmesi vardır.

İşlev çağrısı döndüğünde, aktarım isteğinin durumu işlemin sonucunu içerdiğinden incelenmelidir.

### <a name="input-parameter"></a>Giriş parametresi

- **transfer_request** Aktarım isteğine yönelik işaretçi. Aktarım isteği, aktarım için gereken tüm gerekli bilgileri içerir.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) bu aktarım isteğinin USB aktarımı düzgün zamanlandı. Aktarım isteği tamamlandığında aktarım isteğinin durum kodu incelenmelidir.
- **UX_MEMORY_INSUFFICIENT** (0x12) gerekli denetleyici kaynaklarını ayırmak için yeterli bellek yok.
- **UX_TRANSFER_NOT_READY** (0x25) cihaz geçersiz bir durumda; bağlı, ÇÖZÜMLENMIŞ veya yapılandırılmış olmalıdır.

### <a name="example"></a>Örnek:

```c
UINT status;

/* Create a transfer request for the SET_CONFIGURATION request. No data for this request. */
transfer_request -> ux_transfer_request_requested_length = 0;
transfer_request -> ux_transfer_request_function = UX_SET_CONFIGURATION;
transfer_request -> ux_transfer_request_type =
    UX_REQUEST_OUT |
    UX_REQUEST_TYPE_STANDARD |
    UX_REQUEST_TARGET_DEVICE;

transfer_request -> ux_transfer_request_value = (USHORT)
    configuration -> ux_configuration_descriptor.bConfigurationValue;
transfer_request -> ux_transfer_request_index = 0;

/* Send request to HCD layer. */
status = ux_host_stack_transfer_request(transfer_request);

/* If status equals UX_SUCCESS, the operation was successful. */
```
