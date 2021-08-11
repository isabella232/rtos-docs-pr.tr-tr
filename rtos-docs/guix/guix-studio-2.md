---
title: GUIX Studio'yu Yükleme ve Kullanma
description: Bu bölümde GUIX Studio kullanıcı arabirimi sistem tasarım aracının yüklenmesi, kurulumu ve kullanımıyla ilgili çeşitli sorunların açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 55d2b0ac08bdceebdf286effe4bbc679320541243ff78359deafe0858a7b597e
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116786481"
---
# <a name="chapter-2-installation-and-use-of-guix-studio"></a>Bölüm 2: GUIX Studio'yu Yükleme ve Kullanma

Bu bölümde GUIX Studio kullanıcı arabirimi sistem tasarım aracının yüklenmesi, kurulumu ve kullanımıyla ilgili çeşitli sorunların açıklaması yer almaktadır. 

## <a name="product-distribution"></a>Ürün Dağıtımı

GUIX Studio uygulamasını [Microsoft](https://microsoft.com/store/apps) App Store GUIX Studio'yu arayarak veya [doğrudan GUIX Studio sayfasına gidip edinebilirsiniz.](https://www.microsoft.com/p/azure-rtos-guix-studio/9pbm1k1r7q0f?activetab=pivot:overviewtab) Ardından aşağıdaki adımları gerçekleştirin.

1. GuiX Studio'yu indirmek için App Store veya  Yükle  düğmesine tıklayın.

1. Tarayıcınız, aşağıdaki şekilde gösterildiği gibi tarayıcıyı açmak Microsoft Store bir ileti indirebilirsiniz. Varsa Aç **düğmesini** seçin.
![GUIX Studio'yu yüklemek için Aç'ı seçin.](./media/guix-studio/open-ms-store.png)

1. Yükleme tamam olduğunda Başlat **düğmesini** seçin.

1. GUIX Studio ilk kez başlatıcıda, GUIX repo'yu yerel bilgisayarınıza klonlamak istediğinize soran bir iletişim kutusu görüntülenir. Depoyu kopyalamayı, depoyu zaten klonlamış olduğunuz yere işaret edin veya depoyu kopyalamayı seçmeyebilirsiniz (bu durumda, bilgisayarınızda bir örnek proje yüklenir).
![Repo klonlamayı seçin, önceden kopyalanmış bir repoya işaret gelin veya atlayabilirsiniz.](./media/guix-studio/clone-repo.png)

> ![!NOTE]
> GUIX Stuado'nun ana menüsünden  Yapılandır'ı ve ardından GUIX Deposu'yu seçerek istediğiniz zaman bu **iletişim kutusuna dönebilirsiniz.**

Başlatma işlemi tamam olduktan sonra GUIX Studio'yu kullanmaya hazır hale geleceksiniz.

## <a name="using-guix-studio"></a>GUIX Studio'yu kullanma

GUIX Studio'yu kullanmak kolaydır. GuiX Studio'yu " Başlat"***düğmesiyle*** çalıştırmanız gerekir. Bu noktada GUIX Studio kullanıcı arabirimini gözlemlersiniz. Artık ekli kullanıcı arabiriminizi grafiksel olarak oluşturmak için GUIX Studio'yu kullanmaya hazır oluruz. Buradan yeni bir proje oluşturabilir veya GUIX örnek projeleri de dahil olmak üzere mevcut bir projeyi açacağız.

> [!NOTE]
> Ayrıca GUIX Studio'yu otomatik olarak başlatacak ve başvurulan projeyi açacak olan "**gxp"** uzantısına sahip herhangi bir GUIX Studio proje dosyasına çift tıkabilirsiniz.

## <a name="guix-studio-project-samples"></a>GUIX Studio Project Örnekleri

Yüklemenizin _"_ Örnekler **" alt dizininde "***gxp**" uzantısına sahip bir dizi örnek GUIX Studio proje * dosyası bulunur. Bu önceden hazır örnek projeler GUIX Studio'yu kullanma konusunda size yardımcı olacaktır.

Her zaman mevcut olan örnek proje dosyalarından biri ***samples/demo_guix_simple/guix_simple.gxp** _ dosyasıdır. Bu örnek proje dosyası, bu belgenin _ Bölüm *_7_** bölümünde açıklandığı gibi basit bir GUIX kullanıcı arabiriminin tanımını gösterir.

![GUIX Studio kullanıcı arabiriminin ekran görüntüsü.](./media/guix-studio/image_10.png)

**Şekil 1**

## <a name="keyboard-shortcuts"></a>Klavye Kısayolları

- **Ctrl + N:** Yeni Project
- **Ctrl + O:** Açık Project
- **Ctrl + S:** Project
- **Ctrl + Shift + S:** Farklı Project Kaydet
- **Alt + F4:** Çıkış
