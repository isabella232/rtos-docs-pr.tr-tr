---
title: Bölüm 3-USBX DPUMP sınıfı konuları
description: USBX, konak ve cihaz tarafı için bir DPUMP sınıfı içerir. Bu sınıf kendi kendine standart bir sınıf değildir, bunun yerine iki toplu kanal kullanarak basit bir cihaz oluşturmayı ve bu iki kanal üzerinde veri göndermeyi ve geriye doğru göndermeyi gösteren bir örnek.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 7d453d9ee19b9bc7ca7809102f087f46fdde05dc62b756d9eb3f38f493805be4
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116791162"
---
# <a name="chapter-3---usbx-dpump-class-considerations"></a>Bölüm 3-USBX DPUMP sınıfı konuları

USBX, konak ve cihaz tarafı için bir **DPUMP** sınıfı içerir. Bu sınıf kendi kendine standart bir sınıf değildir, bunun yerine iki toplu kanal kullanarak basit bir cihaz oluşturmayı ve bu iki kanal üzerinde veri göndermeyi ve geriye doğru göndermeyi gösteren bir örnek. **DPUMP** sınıfı, özel bir sınıf veya eski RS232 cihazları başlatmak için kullanılabilir.

USB DPUMP akış grafiği:

![USB DPUMP Flow grafiği](./media/usbx-device-stack-supplemental/usb-dpump-flow-chart.png)

## <a name="usbx-dpump-device-class"></a>USBX DPUMP cihaz sınıfı

Device **DPUMP** sınıfı, USB konakla bağlantı kurulduğunda başlatılan bir iş parçacığı kullanır. İş parçacığı, toplu çıkış uç noktasında gelen bir paketi bekler. Paket alındığında, içeriği toplu uç nokta arabelleğine kopyalar ve bu uç noktada, konağın bu uç noktadan okuma isteği vermesini bekleyen bir işlem gönderir. Bu, toplu ve toplu uç noktalar arasında bir geri döngü mekanizması sağlar.
