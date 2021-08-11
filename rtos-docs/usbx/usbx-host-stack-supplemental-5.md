---
title: USBX OTG
description: USBX, DONANıM tasarımında OTG uyumlu bir USB denetleyicisi kullanılabilir olduğunda USB'nin OTG işlevlerini destekler.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: bb9a0b98ed3f843ee690dfe419a3684562f1255e6839ddb06ded9d8f6023adcc
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116798274"
---
# <a name="chapter-5-usbx-otg"></a>Bölüm 5: USBX OTG

USBX, DONANıM tasarımında OTG uyumlu bir USB denetleyicisi kullanılabilir olduğunda USB'nin OTG işlevlerini destekler.

USBX, çekirdek USB yığınında OTG'yi destekler. Ancak OTG'nin çalışması için belirli bir USB denetleyicisi gerekir. USBX OTG denetleyici işlevleri, usbx_otg ***bulunabilir.*** Geçerli USBX sürümü yalnızca tam OTG özelliklerine sahip NXP LPC3131'i destekler.

Normal denetleyici sürücü işlevleri (ana bilgisayar veya cihaz) standart USBX usbx_device_controllers ve usbx_host_controllers'de bulunabilir, ancak ***usbx_otg*** dizini USB denetleyicisiyle ilişkili belirli OTG işlevlerini içerir.

Her zamanki konak/cihaz işlevlerine ek olarak BIR OTG denetleyicisi için dört işlev kategorisi vardır.

- VBUS'a özgü işlevler
- Denetleyiciyi Başlatma ve Durdurma
- USB rol yöneticisi
- Kesme işleyicileri

## <a name="vbus-functions"></a>VBUS işlevleri

VbUS'un durumunu güç yönetimi gereksinimlerine göre değiştirmek için her denetleyicinin bir VBUS yöneticisi olması gerekir. Genellikle bu işlev yalnızca VBUS'u açma veya kapatma işlemini gerçekleştirir

## <a name="start-and-stop-the-controller"></a>Denetleyiciyi Başlatma ve Durdurma

Normal bir USB uygulamasından farklı olarak, OTG, rol değiştinde ana bilgisayar ve/veya cihaz yığınının etkinleştirilmesini ve devre dışı bırakılabilir.

## <a name="usb-role-manager"></a>USB rolü Yöneticisi

USB rol yöneticisi, USB'nin durumunu değiştirmek için komutları alır. Aşağıdaki tabloda verilenlere ve bu tabloda verilenlerden geçişler gereken birkaç eyalet vardır.

| Durum                    | Değer | Açıklama                                           |
| ------------------------ | ----- | ----------------------------------------------------- |
| UX_OTG_IDLE            | 0     | Cihaz Boşta. Hiçbir şeye bağlı değil |
| UX_OTG_IDLE_TO_HOST  | 1     | Cihaz A türü bağlayıcı ile bağlandı             |
| UX_OTG_IDLE_TO_SLAVE | 2     | Cihaz B türü bağlayıcı ile bağlandı             |
| UX_OTG_HOST_TO_IDLE  | 3     | Konak cihazın bağlantısı kesildi                          |
| UX_OTG_HOST_TO_SLAVE | 4     | Konaktan Bağımlıya rol değiştirme                          |
| UX_OTG_SLAVE_TO_IDLE | 5     | Bağımlı cihazın bağlantısı kesildi                          |
| UX_OTG_SLAVE_TO_HOST | 6     | Bağımlıdan Konak'a rol değiştirme                          |

## <a name="interrupt-handlers"></a>Kesme işleyicileri

OTG için hem ana bilgisayar hem de cihaz denetleyicisi sürücüleri, geleneksel USB kesintilerinin ötesindeki sinyalleri, özellikle de SRP ve VBUS'den gelen sinyalleri izlemek için farklı kesme işleyicileri gerekir.

USB OTG denetleyicisi başlatma. Burada örnek olarak NXP LPC3131'i kullanıyoruz.

```C
/* Initialize the LPC3131 OTG controller. */
status = ux_otg_lpc3131_initialize(0x19000000, lpc3131_vbus_function,
    tx_demo_change_mode_callback);
```

Bu örnekte, VBUS işlevini ve mod değişikliği için bir geri çağırma (konaktan bağımlıya veya tam tersi) geçerek LPC3131'i OTG modunda başlatacağız.

Geri çağırma işlevi yalnızca yeni modu kaydetmeli ve yeni durumu harekete geçsin diye bekleyen bir iş parçacığını uyandırmalı.

```C
void tx_demo_change_mode_callback(ULONG mode)
{
    /* Simply save the otg mode. */
    otg_mode = mode;

    /* Wake up the thread that is waiting. */
    ux_utility_semaphore_put(&mode_change_semaphore);
}
```

Geçirilen mod değeri aşağıdaki değerlere sahip olabilir.

- UX_OTG_MODE_IDLE
- UX_OTG_MODE_SLAVE
- UX_OTG_MODE_HOST

Uygulama, değişkene bakarak cihazın ne olduğunu her zaman kontrol edebilirsiniz.

```C
ux_system_otg ->ux_system_otg_device_type
```

Değerleri aşağıdakilerden biri olabilir.

- UX_OTG_DEVICE_A
- UX_OTG_DEVICE_B
- UX_OTG_DEVICE_IDLE

USB OTG konak cihazı her zaman komutunu kullanarak rol değiştirme işlemi isteyebilirsiniz.

```C
/* Ask the stack to perform a HNP swap with the device. We relinquish the host role to A device. */

ux_host_stack_role_swap(storage ->ux_host_class_storage_device);
```

Bağımlı bir cihaz için verilen komut yoktur ancak bağımlı cihaz rolü değiştirmek için bir durum ayarlayacaktır. Bu durum konak tarafından bir GET_STATUS ve değiştirme işlemi başlatılır.

```C
/* We are a B device, ask for role swap. The next GET_STATUS from the host will get the status change and do the HNP. */

ux_system_otg ->ux_system_otg_slave_role_swap_flag =
    UX_OTG_HOST_REQUEST_FLAG;
```
