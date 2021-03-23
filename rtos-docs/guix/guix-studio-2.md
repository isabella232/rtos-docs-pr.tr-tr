---
title: GUX Studio 'nun yüklenmesi ve kullanımı
description: Bu bölümde, Gux Studio UI sistem tasarımı aracının yüklenmesiyle, kurulumuyla ve kullanımıyla ilgili çeşitli sorunların açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: d7b5f94c26842b408ea1b00aeeb78e111bea3623
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104827167"
---
# <a name="chapter-2-installation-and-use-of-guix-studio"></a>Bölüm 2: Gux Studio 'Yu yükleme ve kullanma

Bu bölümde, Gux Studio UI sistem tasarımı aracının yüklenmesiyle, kurulumuyla ve kullanımıyla ilgili çeşitli sorunların açıklaması yer almaktadır. 

## <a name="product-distribution"></a>Ürün dağıtımı

GUX Studio uygulamasını, Gux Studio 'yu arayarak veya doğrudan [Gux Studio sayfasına](https://www.microsoft.com/p/azure-rtos-guix-studio/9pbm1k1r7q0f?activetab=pivot:overviewtab)giderek [Microsoft App Store](https://microsoft.com/store/apps) 'dan edinebilirsiniz. Ardından aşağıdakileri yapın.

1. Uygulama mağazasındaki Gux Studio sayfasında, Gux Studio 'Yu indirmek için **Al** veya **Yükle** düğmesine tıklayın.

1. Tarayıcınız, aşağıdaki şekilde gösterildiği gibi Microsoft Store açmak isteyip istemediğinizi soran bir ileti görüntülenebilir. Varsa, **Aç** düğmesini seçin.
![GUX Studio 'Yu yüklemek için Aç ' ı seçin.](./media/guix-studio/open-ms-store.png)

1. Yüklemesi tamamlandığında, **Başlat** düğmesini seçin.

1. GUX Studio ilk kez başlatıldığında, Gux deposunu yerel bilgisayarınıza kopyalamak isteyip istemediğinizi soran bir iletişim kutusu görüntüler. Depoyu kopyalamayı seçebilirsiniz, depoyu zaten Klonladığınız yere işaret edebilir veya depoyu hiç kopyalamamanız tercih edebilirsiniz (Bu durumda, bilgisayarınızda bir örnek proje yüklü).
![Depoyu kopyalamayı seçin, zaten kopyalanmış bir depoyu işaret edin veya atlayın.](./media/guix-studio/clone-repo.png)

> ![!NOTE]
> Bu iletişim kutusuna, Gux Stuido ana menüsünden **Yapılandır** ' ı ve ardından **Gux deposu**' nu seçerek dilediğiniz zaman geri dönebilirsiniz.

Başlangıç işlemi tamamlandıktan sonra, Gux Studio 'Yu kullanmaya hazırlanın.

## <a name="using-guix-studio"></a>GUX Studio 'Yu kullanma

GUX Studio 'Yu kullanmak kolay bir şekilde, "***Başlat***" düğmesi aracılığıyla Gux Studio 'yu çalıştırmak yeterlidir. Bu noktada, Gux Studio Kullanıcı arabirimini gözlemleyeceksiniz. Artık, yerleşik kullanıcı arabirimini grafiksel olarak oluşturmak için Gux Studio 'Yu kullanmaya hazırsınız. Buradan yeni bir proje oluşturursunuz veya Gux örnek projeleri de dahil olmak üzere mevcut bir projeyi açarsınız.

> [!NOTE]
> Ayrıca, "**GXP**" uzantılı bir Gux Studio proje dosyasına çift tıklayarak Gux Studio 'yu otomatik olarak başlatabilir ve başvurulan projeyi açabilirsiniz.

## <a name="guix-studio-project-samples"></a>GUX Studio proje örnekleri

"***GXP**_"_ uzantısına sahip bir dizi örnek Gux Studio proje dosyası, yüklemenizin " * _Samples_* *" alt dizininde bulunur. Önceden oluşturulmuş bu örnek projeler, Gux Studio 'Yu kullanmaya rahat bir şekilde başlamanıza yardımcı olur.

Her zaman bulunan örnek bir proje dosyası ***Samples/demo_guix_simple/guix_simple. GXP** _ dosyasıdır. Bu örnek proje dosyası, bu belgenin _ *_Bölüm 7_** bölümünde açıklandığı gibi basıt bır GUıDX Kullanıcı arabirimi tanımını gösterir.

![GUX Studio Kullanıcı arabiriminin ekran görüntüsü.](./media/guix-studio/image_10.png)

**Şekil 1**

## <a name="keyboard-shortcuts"></a>Klavye Kısayolları

- **CTRL + N:** Yeni proje
- **CTRL + O:** Projeyi aç
- **CTRL + S:** Projeyi Kaydet
- **CTRL + SHIFT + S:** Projeyi farklı kaydet
- **Alt + F4:** Çıkıp
