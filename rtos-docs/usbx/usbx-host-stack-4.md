---
title: Bölüm 4-USBX konak hizmetlerinin açıklaması
description: USBX konak hizmetleri hakkında bilgi edinin.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: d730658c07f3cd7cec8c75a47818314bdc63f35a
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104828456"
---
# <a name="chapter-4---description-of-usbx-host-services"></a>Bölüm 4-USBX konak hizmetlerinin açıklaması

## <a name="ux_host_stack_initialize"></a>ux_host_stack_initialize

Konak işlemi için USBX 'i başlatın.

### <a name="prototype"></a>Prototype

```c
UINT ux_host_stack_initialize(
    UINT (*system_change_function)
    (ULONG, UX_HOST_CLASS *));
```

### <a name="description"></a>Açıklama

Bu işlev, USB ana bilgisayar yığınını başlatacak. Sağlanan bellek alanı, USBX iç kullanımı için kurulum olacaktır. UX_SUCCESS döndürülürse, USBX konak denetleyicisi ve sınıf kaydı için hazırlayın.

### <a name="input-parameter"></a>Giriş parametresi

- **system_change_function** Cihaz değişikliklerinin uygulamasına bildirimde bulunmak için isteğe bağlı geri arama yordamının işaretçisi.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) başarıyla başlatıldı.
- **UX_MEMORY_INSUFFICIENT** (0x12) bir bellek ayırma başarısız oldu.

### <a name="example"></a>Örnek

```c
UINT status;

/* Initialize USBX for host operation, without notification. */
status = ux_host_stack_initialize(UX_NULL);

/* If status equals UX_SUCCESS, USBX has been successfully initialized for host operation. */
```

## <a name="ux_host_stack_endpoint_transfer_abort"></a>ux_host_stack_endpoint_transfer_abort

Bir uç nokta için aktarım isteğine bağlı tüm işlemleri iptal edin.

### <a name="prototype"></a>Prototype

```c
UINT ux_host_stack_endpoint_transfer_abort(UX_ENDPOINT *endpoint);
```

### <a name="description"></a>Açıklama

Bu işlev, bir uç noktaya bağlı belirli bir aktarım isteği için etkin veya bekleyen tüm işlemleri iptal eder. Aktarım isteğinde bir geri çağırma işlevi eklenmiş, geri çağırma işlevi UX_TRANSACTION_ABORTED durumuyla çağrılır.

### <a name="input-parameter"></a>Giriş parametresi

- **uç nokta** Uç nokta işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- Hata **UX_SUCCESS** (0x00).
- **UX_ENDPOINT_HANDLE_UNKNOWN** (0x53) uç noktası tanıtıcısı geçerli değil.

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

Bir sınıf kapsayıcısının işaretçisini alır.

### <a name="prototype"></a>Prototype

```c
UINT ux_host_stack_class_get(
    UCHAR *class_name,
    UX_HOST_CLASS **class);
```

### <a name="description"></a>Açıklama

Bu işlev, sınıf kapsayıcısına bir işaretçi döndürür. Bir sınıf veya uygulama bir cihazı açmak istediğinde örnekleri aramak için bir sınıfın kapsayıcısını USB yığınından alması gerekir.

> [!NOTE]
> Class_name C dizesi NULL ile sonlandırılmış olmalı ve bunun uzunluğu (NULL-Sonlandırıcı kendisi olmadan) UX_MAX_CLASS_NAME_LENGTH daha büyük olmamalıdır.

### <a name="parameters"></a>Parametreler

- **class_name** Sınıf adı işaretçisi.
- **sınıf** Sınıf adı için sınıf kapsayıcısını içeren işlev çağrısı tarafından güncelleştirilmiş bir işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) hata yok, return üzerinde sınıf alanı sınıf kapsayıcısının işaretçisi ile dosyalandı.
- **UX_HOST_CLASS_UNKNOWN** (0x59) sınıfı yığın tarafından bilinmiyor.

### <a name="example"></a>Örnek

```c
UX_HOST_CLASS *printer_container;
UINT status;

/* Get the container for this class. */
status = ux_host_stack_class_get("ux_host_class_printer", &printer_container);

/* If status equals UX_SUCCESS, the operation was successful */
```

## <a name="ux_host_stack_class_register"></a>ux_host_stack_class_register

USB yığınına USB sınıfı kaydedin.

### <a name="prototype"></a>Prototype

```c
UINT ux_host_stack_class_register(
    UCHAR *class_name,
    UINT (*class_entry_address) (struct UX_HOST_CLASS_COMMAND_STRUCT *));
```

### <a name="description"></a>Açıklama

Bu işlev USB yığınına USB sınıfı kaydeder. Sınıfı, USB yığınının aşağıdaki gibi komutları gönderebilmesi için bir giriş noktası belirtmelidir.

- **UX_HOST_CLASS_COMMAND_QUERY**
- **UX_HOST_CLASS_COMMAND_ACTIVATE**
- **UX_HOST_CLASS_COMMAND_DESTROY**

> [!NOTE]
> *Class_name* C dizesi null ile sonlandırılmış olmalı ve bunun uzunluğu (null-Sonlandırıcı kendisi olmadan) **UX_MAX_CLASS_NAME_LENGTH** daha büyük olmamalıdır.

### <a name="parameters"></a>Parametreler

- **class_name** Sınıfın adı işaretçisi, geçerli girdiler, USBX USB sınıfları altındaki ux_system_initialize. c dosyasında bulunur.
- **class_entry_address** Sınıfın giriş işlevinin adresi.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) sınıfı başarıyla yüklendi.
- **UX_MEMORY_ARRAY_FULL** (0x1A) bu sınıfı depolamak için daha fazla bellek yok.
- **UX_HOST_CLASS_ALREADY_INSTALLED** (0x58) konak sınıfı zaten yüklü.

### <a name="example"></a>Örnek:

```c
UINT status;

/* Register all the classes for this implementation. */
status = ux_host_stack_class_register("ux_host_class_hub", ux_host_class_hub_entry);

/* If status equals UX_SUCCESS, class was successfully installed. */
```

## <a name="ux_host_stack_class_instance_create"></a>ux_host_stack_class_instance_create

Sınıf kapsayıcısı için yeni bir sınıf örneği oluşturun.

### <a name="prototype"></a>Prototype

```c
UINT ux_host_stack_class_instance_create(
    UX_HOST_CLASS *class, 
    VOID *class_instance);
```

### <a name="description"></a>Açıklama

Bu işlev, sınıf kapsayıcısı için yeni bir sınıf örneği oluşturur. Sınıf karmaşıklığını azaltmak için sınıfın örneği sınıf kodunda yer alır. Bunun yerine, her bir sınıf örneği, ana yığında bulunan sınıf kapsayıcısına iliştirilir.

### <a name="parameters"></a>Parametreler

- **sınıf** Sınıf kapsayıcısının işaretçisi.
- **class_instance** Oluşturulacak sınıf örneğine yönelik işaretçi.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) sınıf örneği sınıf kapsayıcısına iliştirildi.

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

### <a name="description"></a>Açıklama

Bu işlev, sınıf kapsayıcısı için bir sınıf örneğini yok eder.

### <a name="parameters"></a>Parametreler

- **sınıf** Sınıf kapsayıcısının işaretçisi.
- **class_instance** Yok edilecek örneğe yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) sınıf örneği yok edildi.
- **UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) sınıf örneği sınıf kapsayıcısına eklenmez.

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

Belirli bir sınıf için bir sınıf örneği işaretçisi alır.

### <a name="prototype"></a>Prototype

```c
UINT ux_host_stack_class_instance_get(
    UX_HOST_CLASS *class,
    UINT class_index, 
    VOID **class_instance);
```

### <a name="description"></a>Açıklama

Bu işlev, belirli bir sınıf için bir sınıf örneği işaretçisi döndürür. Sınıf karmaşıklığını azaltmak için sınıfın örneği sınıf kodunda yer alır. Bunun yerine, her bir sınıf örneği sınıf kapsayıcısına iliştirilir. Bu işlev, sınıf kapsayıcısı içinde sınıf örnekleri aramak için kullanılır.

### <a name="parameters"></a>Parametreler

- **sınıf** Sınıf kapsayıcısının işaretçisi.
- **class_index** Kapsayıcıya iliştirilmiş sınıfların listesi içindeki işlev çağrısı tarafından kullanılacak dizin.
- **class_instance** İşlev çağrısının döndürdüğü örneğe yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) sınıf örneği bulundu.

- **UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) sınıf kapsayıcısına iliştirilmiş daha fazla sınıf örneği yok.

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

Yapılandırma kapsayıcısına yönelik bir işaretçi alır.

### <a name="prototype"></a>Prototype

```c
UINT ux_host_stack_device_configuration_get(
    UX_DEVICE *device,
    UINT configuration_index, 
    UX_CONFIGURATION *configuration);
```

### <a name="description"></a>Açıklama

Bu işlev bir cihaz tanıtıcısına ve bir yapılandırma dizinine bağlı olarak bir yapılandırma kapsayıcısı döndürür.

### <a name="parameters"></a>Parametreler

- **cihaz** İstenen yapılandırmanın sahibi olan cihaz kapsayıcısının işaretçisi.
- **configuration_index** Aranacak yapılandırmanın dizini.
- **yapılandırma** Döndürülecek Yapılandırma kapsayıcısının işaretçisinin adresi.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) yapılandırma bulundu.
- **UX_DEVICE_HANDLE_UNKNOWN** (0x50) cihaz kapsayıcısı yok.
- **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) dizin için yapılandırma tanıtıcısı yok.

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

### <a name="description"></a>Açıklama

Bu işlev, bir cihaz için belirli bir yapılandırma seçer. Bu yapılandırma cihaza ayarlandığında, varsayılan olarak, her cihaz arabirimi ve ilişkili alternatif ayarı 0 ' da cihazda etkinleştirilir. Cihaz/arabirim sınıfı belirli bir arabirimin ayarını değiştirmeyi istiyorsa, bir **ux_host_stack_interface_setting_select** hizmet çağrısı vermesi gerekir.

### <a name="parameters"></a>Parametreler

- **yapılandırma** Bu cihaz için etkinleştirilecek Yapılandırma kapsayıcısına yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) yapılandırma seçimi başarılı oldu.
- **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) yapılandırma tanıtıcısı yok.
- **UX_OVER_CURRENT_CONDITION** (0x43) Bu yapılandırma için veri yolunda geçerli bir durum var.

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

Cihaz kapsayıcısı için bir işaretçi alır.

### <a name="prototype"></a>Prototype

```c
UINT ux_host_stack_device_get(
    ULONG device_index, 
    UX_DEVICE *device);
```

### <a name="description"></a>Açıklama

Bu işlev, dizinine göre bir cihaz kapsayıcısı döndürür. Cihaz dizini 0 ile başlar. Birkaç denetleyicimiz olduğundan ve bir bayt dizini yeterince bulunmayabilir, dizinin bir ULONG olduğunu unutmayın. Cihaz dizini, veri yoluna özgü olan cihaz adresiyle karıştırılmamalıdır.

### <a name="parameters"></a>Parametreler

- **device_index** Cihazın dizini.
- **cihaz** Döndürülecek cihaz kapsayıcısının işaretçisinin adresi.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) cihaz kapsayıcısı var ve döndürülür
- **UX_DEVICE_HANDLE_UNKNOWN** (0x50) cihaz bilinmiyor

### <a name="example"></a>Örnek

```c
UINT status;

/* Locate the first device in USBX. */
status = ux_host_stack_device_get(0, device);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_stack_interface_endpoint_get"></a>ux_host_stack_interface_endpoint_get

Bir uç nokta kapsayıcısı alın.

### <a name="prototype"></a>Prototype

```c
UINT ux_host_stack_interface_endpoint_get(
    UX_INTERFACE *interface,
    UINT endpoint_index,
    UX_ENDPOINT *endpoint);
```

### <a name="description"></a>Açıklama

Bu işlev, arabirim tanıtıcısına ve bir uç nokta dizinine göre bir uç nokta kapsayıcısı döndürür. Bu, arabirim için alternatif ayarların seçildiği veya aranmakta olan bitiş noktaları öncesinde varsayılan ayar kullanıldığı varsayılır.

### <a name="parameters"></a>Parametreler

- **arabirim** İstenen uç noktayı içeren arabirim kapsayıcısının işaretçisi.
- **endpoint_index** Bu arabirimdeki uç noktanın dizini.
- **uç nokta** Döndürülecek uç nokta kapsayıcısının adresi.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) uç nokta kapsayıcısı var ve döndürülür.
- **UX_INTERFACE_HANDLE_UNKNOWN** (0x52) belirtilen arabirim yok.
- **UX_ENDPOINT_HANDLE_UNKNOWN** (0x53) uç noktası dizini yok.

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

USB yığınına USB denetleyicisi kaydedin.

### <a name="prototype"></a>Prototype

```c
UINT ux_host_stack_hcd_register(
    UCHAR *hcd_name,
    UINT (*hcd_function)(struct UX_HCD_STRUCT *),
    ULONG hcd_param1, ULONG hcd_param2);
```

### <a name="description"></a>Açıklama

Bu işlev USB yığınına USB denetleyicisi kaydeder. Bu, genellikle bu denetleyici tarafından kullanılan belleği ayırır ve başlatma komutunu denetleyiciye geçirir.

### <a name="parameters"></a>Parametreler

- **hcd_name** Konak denetleyicisinin adı
- **hcd_function** Başlangıçtan sorumlu ana bilgisayar denetleyicisindeki işlev.
- **hcd_param1** HCD tarafından kullanılan GÇ veya bellek kaynağı.
- **hcd_param2** Konak denetleyicisi tarafından kullanılan IRQ.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) denetleyici düzgün şekilde başlatıldı.
- **UX_MEMORY_INSUFFICIENT** (0x12) Bu denetleyici için yeterli bellek yok.
- **UX_PORT_RESET_FAILED** (0x31) denetleyicinin sıfırlanması başarısız oldu.
- **UX_CONTROLLER_INIT_FAILED** (0x32) denetleyici düzgün şekilde başlatılamadı.

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

Arabirim kapsayıcısı işaretçisi alın.

### <a name="prototype"></a>Prototype

```c
UINT ux_host_stack_configuration_interface_get (
    UX_CONFIGURATION *configuration,
    UINT interface_index, 
    UINT alternate_setting_index, 
    UX_INTERFACE **interface);
```

### <a name="description"></a>Açıklama

Bu işlev, bir yapılandırma tanıtıcısına, bir arabirim dizinine ve alternatif ayar dizinine göre bir arabirim kapsayıcısı döndürür.

### <a name="parameters"></a>Parametreler

- **yapılandırma** Arabirime sahip olan Yapılandırma kapsayıcısına yönelik işaretçi.
- **interface_index** Aranacak arabirim dizini.
- **alternate_setting_index** Arama için arabirim içindeki alternatif ayar.
- **arabirim** Döndürülecek arabirim kapsayıcısı işaretçisinin adresi.

### <a name="return-values"></a>Dönüş Değerleri

- **UX_SUCCESS** (0x00) arabirim dizini için arabirim kapsayıcısı ve alternatif ayar bulundu ve döndürüldü.
- **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) yapılandırma yok.
- **UX_INTERFACE_HANDLE_UNKNOWN** (0x52) arabirim yok.

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

### <a name="description"></a>Açıklama

Bu işlev, seçilen yapılandırmaya ait belirli bir arabirim için belirli bir alternatif ayarı seçer. Bu işlev, varsayılan alternatif ayarından yeni bir ayara geçmek veya varsayılan alternatif ayara geri dönmek için kullanılır. Yeni bir alternatif ayar seçildiğinde, önceki uç nokta özellikleri geçersizdir ve yeniden yüklenmelidir.

### <a name="input-parameter"></a>Giriş parametresi

- **arabirim** Alternatif ayarı seçilecek olan arabirim kapsayıcısına yönelik işaretçi.

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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
