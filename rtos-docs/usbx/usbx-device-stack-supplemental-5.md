---
title: Bölüm 5-USBX OTG
description: Donanım tasarımında bir OTG uyumlu USB denetleyicisi varsa, USBX 'in USB 'nin OTG işlevlerini nasıl desteklediğini öğrenin.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 64a3c44f84b9ffca31d9e616d14d3d5d87c56bd7
ms.sourcegitcommit: 60ad844b58639d88830f2660ab0c4ff86b92c10f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2021
ms.locfileid: "106550329"
---
# <a name="chapter-5---usbx-otg"></a>Bölüm 5-USBX OTG

USBX, donanım tasarımında bir OTG uyumlu USB denetleyicisi varsa, USB 'nin OTG işlevlerini destekler.

USBX, çekirdek USB yığınında OTG 'yi destekler. Ancak OTG 'nin çalışması için, belirli bir USB denetleyicisi gerekir. USBX OTG denetleyici işlevleri usbx_otg dizininde bulunabilir. Geçerli USBX sürümü yalnızca tam OTG özelliklerine sahip NXP LPC3131 destekler.

Normal denetleyici sürücü işlevleri (konak veya cihaz) hala standart USBX usbx_device_controllers ve usbx_host_controllers bulunabilir ancak usbx_otg Dizin, USB denetleyicisiyle ilişkili belirli OTG işlevlerini içerir.

Her zamanki ana bilgisayar/cihaz işlevlerine ek olarak, bir OTG denetleyicisi için dört işlev kategorisi vardır.

- VBUS 'a özgü işlevler
- Denetleyiciyi başlatma ve durdurma
- USB rol yöneticisi
- Kesme işleyicileri

## <a name="vbus-functions"></a>VBUS işlevleri

Her denetleyicinin, VBUS 'ın durumunu güç yönetimi gereksinimlerine göre değiştirmesi için bir VBUS Yöneticisi olması gerekir. Genellikle, bu işlev yalnızca VBUS 'ı açmayı veya kapatmayı gerçekleştirir.

## <a name="start-and-stop-the-controller"></a>Denetleyiciyi başlatma ve durdurma

Normal bir USB uygulamasından farklı olarak, OTG, rol değiştiğinde konağın ve/veya cihaz yığınının etkinleştirilmesini ve devre dışı olmasını gerektirir.

## <a name="usb-role-manager"></a>USB rol yöneticisi

USB rol yöneticisi, USB 'nin durumunu değiştirmek için komutları alır. Ve arasında geçiş gerektiren birkaç durum vardır:

| Durum                    | Değer | Açıklama                                           |
| ------------------------ | ----- | ----------------------------------------------------- |
| UX_OTG_IDLE            | 0     | Cihaz boşta. Hiçbir şeye bağlanmadı |
| UX_OTG_IDLE_TO_HOST  | 1     | Cihaz, bağlayıcı türüyle bağlandı             |
| UX_OTG_IDLE_TO_SLAVE | 2     | Cihaz, tür B Bağlayıcısı ile bağlandı             |
| UX_OTG_HOST_TO_IDLE  | 3     | Ana cihazın bağlantısı kesildi                          |
| UX_OTG_HOST_TO_SLAVE | 4     | Rol, konaktan bağımlı olarak takas                          |
| UX_OTG_SLAVE_TO_IDLE | 5     | Bağımlı cihazın bağlantısı kesildi                          |
| UX_OTG_SLAVE_TO_HOST | 6     | Rolü bağımlı sunucudan konağa değiştirme                          |

## <a name="interrupt-handlers"></a>Kesme işleyicileri

OTG için hem konak hem de cihaz denetleyicisi sürücüleri, SRP ve VBUS nedeniyle belirli sinyallere göre geleneksel USB kesmelerinin ötesinde sinyalleri izlemek için farklı kesme işleyicileri gerektirir.

USB OTG denetleyicisi başlatma. Burada örnek olarak NXP LPC3131 kullanıyoruz.

```C
/* Initialize the LPC3131 OTG controller. */
status = ux_otg_lpc3131_initialize(0x19000000, lpc3131_vbus_function,
    tx_demo_change_mode_callback);
```

Bu örnekte, VBUS işlevini ve mod değişikliği (konaktan bağımlı veya tam tersi) için bir geri çağırma geçirerek OTG modunda LPC3131 'i başlatacağız.

Geri çağırma işlevi yalnızca yeni modu kaydedip yeni durumu uygulamak için bekleyen bir iş parçacığını uyandırmalıdır.

```C
void tx_demo_change_mode_callback(ULONG mode) {
    /* Simply save the otg mode. */
    otg_mode = mode;

    /* Wake up the thread that is waiting. */
    ux_utility_semaphore_put(&mode_change_semaphore);
}
```

Geçirilen mod değeri aşağıdaki değerlere sahip olabilir.

- **UX_OTG_MODE_IDLE**
- **UX_OTG_MODE_SLAVE**
- **UX_OTG_MODE_HOST**

Uygulama, şu değişkene bakarak cihazın ne olduğunu her zaman denetleyebilir:

```C
_ux_system_otg -> ux_system_otg_device_type
```

Değerleri aşağıdakilerden herhangi biri olabilir.

- **UX_OTG_DEVICE_A**
- **UX_OTG_DEVICE_B**
- **UX_OTG_DEVICE_IDLE**

Bir USB OTG ana bilgisayar cihazı, aşağıdaki komutu vererek her zaman bir rol takası isteyebilir.

```C
/* Ask the stack to perform a HNP swap with the device. We relinquish the host role to A device. */
ux_host_stack_role_swap(storage -> ux_host_class_storage_device);
```

Bir bağımlı cihaz için, soruna bir komut yoktur, ancak bağımlı cihaz, **GET_STATUS** bir sorun olduğunda ana bilgisayar tarafından çekilecek rolü değiştirmek için bir durum ayarlayabilir ve ardından takas başlatılır.

```C
/* We are a B device, ask for role swap.
   The next GET_STATUS from the host will get the status change and do the HNP. */
_ux_system_otg -> ux_system_otg_slave_role_swap_flag =
    UX_OTG_HOST_REQUEST_FLAG;
```
