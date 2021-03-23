---
title: Bölüm 2-Azure RTOS TraceX yükleme ve kullanımı
description: Bu bölümde, Azure RTOS TraceX sistem analizi aracının yüklenmesiyle, kurulumuyla ve kullanımıyla ilgili çeşitli sorunların açıklaması yer almaktadır.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: 05d7fe3df38c7e8a3480c8ea0d4922a109de9ede
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104827574"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-tracex"></a>Bölüm 2-Azure RTOS TraceX yükleme ve kullanımı

Bu bölümde, Azure RTOS TraceX sistem analizi aracının yüklenmesiyle, kurulumuyla ve kullanımıyla ilgili çeşitli sorunların açıklaması yer almaktadır. 

## <a name="product-distribution"></a>Ürün dağıtımı

Tracex 'yi arayarak veya doğrudan [tracex sayfasına](https://www.microsoft.com/p/azure-rtos-tracex/9nf1lfd5xxg3?activetab=pivot:overviewtab)giderek, [Microsoft App Store](https://microsoft.com/store/apps) 'dan trackingex uygulamasını elde edebilirsiniz. Ardından aşağıdakileri yapın.

1. Uygulama mağazasındaki TraceX sayfasında, TraceX **'yi yüklemek** için **Al veya Al** düğmesine tıklayın.

1. Tarayıcınız, aşağıdaki şekilde gösterildiği gibi Microsoft Store açmak isteyip istemediğinizi soran bir ileti görüntülenebilir. Varsa, **Aç** düğmesini seçin.
![Trackingex 'ı yüklemek için Aç ' ı seçin.](../guix/media/guix-studio/open-ms-store.png)

1. Yüklemesi tamamlandığında, **Başlat** düğmesini seçin. 

## <a name="using-tracex"></a>TraceX kullanma

TraceX 'in kullanılması, TraceX içinde bir izleme dosyası açmak kadar kolaydır! ***Start** _ düğmesini kullanarak tracex 'yi çalıştırın. Bu noktada, TraceX grafik kullanıcı arabirimini (GUI) gözlemleyeceksiniz. Artık var olan bir hedef izleme arabelleğini grafik olarak görüntülemek için TraceX kullanmaya hazırsınız. Bu, _ *_Dosya-> aç '_* a tıklayıp, ardından ikili izleme dosyasını girerek kolayca yapılır.

>[!IMPORTANT]
>*Ayrıca **, bir TRX** Uzantısı ile herhangi bir izleme dosyasına çift tıklayabilirsiniz ve bu da otomatik olarak tracex başlatılır.*

![TraceX GUI 'nin ekran görüntüsü.](./media/user-guide/screen_shot_8.png)

**ŞEKIL 1**

>[!IMPORTANT]
>*Hedef üzerinde ThreadX kullanarak izleme arabellekleri oluşturma yönergeleri için **Bölüm 5** ' e başvurun.*

## <a name="tracex-examples"></a>TraceX örnekleri

TraceX uygulamasını ilk kez çalıştırdığınızda veya TraceX uygulaması güncelleştirilirken, TraceX örnek izleme dosyalarını ve custom_events. trxc dosyasını yerel makinenizde Kullanıcı tanımlı bir dizine yüklemeniz istenir.

Bu yükleme adımı tamamlandıktan sonra, **TRX** uzantılı örnek izleme dosyaları, yükleme klasörünüzün **tracefiles** alt dizininde bulunur. Bu önceden oluşturulmuş örnekler, uygulamanızla birlikte çalışan ThreadX tarafından oluşturulan izleme arabelleklerinde TraceX kullanmaya rahat bir şekilde başlamanıza yardımcı olur.

Her zaman bir örnek izleme dosyası, ***demo_threadx. trx** _ dosyasıdır. Bu örnek izleme dosyası, _ThreadX Kullanıcı Kılavuzu * Bölüm 6 ' da açıklandığı gibi standart ThreadX tanıtımına yönelik yürütmeyi gösterir.

![Trackingex içindeki açık iletişim kutusunun ekran görüntüsü.](./media/user-guide/screen_shot_9.png)

**ŞEKIL 2**
