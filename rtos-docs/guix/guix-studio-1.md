---
title: GUX Studio Kullanıcı Kılavuzu
description: Bu kılavuz, Microsoft 'un Gux çalışma zamanı kitaplığı için özel olarak tasarlanan Microsoft Windows tabanlı Hızlı Kullanıcı arabirimi geliştirme ortamı olan Gux Studio hakkında kapsamlı bilgiler sağlar.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 6a5d628581d4c6b44ff093bac45790d6e2755349
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104827172"
---
# <a name="chapter-1-introduction-to-azure-rtos-guix-studio"></a>Bölüm 1: Azure RTOS Gux Studio 'ya giriş

Azure RTOS Gux Studio, Microsoft 'un Gux çalışma zamanı kitaplığı için özel olarak tasarlanan Microsoft Windows tabanlı bir hızlı UI geliştirme ortamıdır.

Ekli UI geliştiricileri, Gux çalışma zamanı ortamını kullanarak kendi yerleşik kullanıcı arabirimini hızlıca oluşturmak ve güncelleştirmek için Gux Studio WYSıWYG ekran Tasarımcısı ' nı kullanabilir. GUX Studio tasarımları,. GXP uzantısına sahip bir Gux Studio proje dosyasında kaydedilir ve saklanır. Tasarımınız hedefte yürütmeye hazırsa, GUıDX Studio tüm gerekli Kullanıcı arabirimi bilgilerini ve kodu içeren C kodu oluşturur.

## <a name="guix-studio-requirements"></a>GUX Studio gereksinimleri

Microsoft 'un Gux Studio 'nun düzgün çalışması için *WINDOWS XP* (veya üzeri) gerekir. Sistemde en az 200 MB RAM, 2 GB kullanılabilir sabit disk alanı ve en az 256 renk içeren 1024x768 ekran görüntülenebilir. Ayrıca, ekli uygulamanın *threadx/Gux v 6.0* veya sonraki sürümlerinde çalışıyor olması gerekir.

Katıştırılmış UI uygulamasını bağımsız bir Microsoft Windows yürütülebilir dosyası olarak derleyip çalıştırmak istiyorsanız, bir Microsoft Windows yürütülebilir dosyası üretmek için C kaynak kodu derlenebilecek bir derleyici veya yapı ortamı da gerekir. GUX Studio 'Ya dahil edilen değerlendirme paketi ayrıca, Visual Studio 2019 uyumlu proje dosyalarını ve sağlanan her bir örnek uygulama için çözümleri içerir. Farklı bir derleyici kullanıyorsanız, kendi proje dosyalarınızı oluşturmanız veya örnek uygulamalarınızı oluşturma amacıyla dosyaları yapmanız veya ' de desteğe başvurmanız gerekir https://aka.ms/azrtos-support .

## <a name="guix-studio-constraints"></a>GUX Studio kısıtlamaları

GUX Studio UI tasarım aracında aşağıdaki gibi çeşitli kısıtlamalar vardır:

- Proje başına en fazla 4 ekran görüntülenir.
- GUX Studio projesi başına en fazla 100.000 pencere öğesi.
- En fazla 100.000 farklı kaynak, örneğin, renkler, yazı tipleri, pixelmaps, dizeler vb.