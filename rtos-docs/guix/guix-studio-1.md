---
title: GUIX Studio Kullanıcı Kılavuzu
description: Bu kılavuz, Microsoft'un GUIX çalışma zamanı kitaplığı için özel olarak tasarlanmış, Microsoft Windows tabanlı hızlı kullanıcı arabirimi geliştirme ortamı GUIX Studio hakkında kapsamlı bilgiler sağlar.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 2c36fb794816cb1acd51ec81f48c0dabe509336f27914050b6206f19bf8ceeff
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116789842"
---
# <a name="chapter-1-introduction-to-azure-rtos-guix-studio"></a>Bölüm 1: AZURE RTOS GUIX Studio'ya giriş

Azure RTOS GUIX Studio, microsoft tarafından Windows GUIX çalışma zamanı kitaplığı için özel olarak tasarlanmış microsoft tabanlı hızlı kullanıcı arabirimi geliştirme ortamıdır.

Katıştırılmış KULLANıCı Arabirimi Geliştiricileri GUIX Studio WYSIWYG ekran tasarımcısını kullanarak GUIX çalışma zamanı ortamını kullanarak ekli kullanıcı arabirimini hızlı bir şekilde oluşturabilir ve güncelleştirebilir. GUIX Studio tasarımları ,gxp uzantısına sahip bir GUIX Studio proje dosyasında kaydedilir ve korunur. Tasarımınız hedefte yürütme için hazır olduğunda GUIX Studio gerekli tüm kullanıcı arabirimi bilgilerini ve kodunu içeren C kodu üretir.

## <a name="guix-studio-requirements"></a>GUIX Studio Gereksinimleri

Microsoft'un GUIX Studio'nun düzgün çalışması için Windows *XP (veya* üzeri) gerekir. Sistemde en az 200 MB RAM, 2 GB kullanılabilir sabit disk alanı ve 256 renkle en az 1024x768 görüntüsü olmalıdır. Ek olarak, katıştırılmış uygulama *ThreadX/GUIX V6.0 veya* üzerinde çalışıyor olması gerekir.

Katıştırılmış kullanıcı arabirimi uygulamasını tek başına Bir Microsoft Windows yürütülebilir dosyası olarak derleyebilecek ve çalıştırabilecek bir derleyici veya Microsoft Windows yürütülebilir dosyası oluşturmak için C kaynak kodu derleyebilecek bir ortam da gerekir. GUIX Studio'ya dahil edilen değerlendirme paketi, sağlanan örnek uygulamaların her biri Visual Studio 2019 uyumlu proje dosyalarını ve çözümlerini de içerir. Farklı bir derleyici kullanıyorsanız, kendi proje dosyalarınızı oluşturmanız veya örnek uygulamalarınızı oluşturmak amacıyla dosya oluşturmanız ya da 'de de destek ile iletişim kurmanız https://aka.ms/azrtos-support gerekir.

## <a name="guix-studio-constraints"></a>GUIX Studio Kısıtlamaları

GUIX Studio kullanıcı arabirimi tasarım aracının aşağıdaki gibi çeşitli kısıtlamaları vardır:

- Proje başına en fazla 4 görüntü görüntülenir.
- GUIX Studio projesi başına en fazla 100.000 pencere öğesi.
- Renkler, yazı tipleri, piksel haritaları, dizeler gibi en fazla 100.000 ayrı kaynak.