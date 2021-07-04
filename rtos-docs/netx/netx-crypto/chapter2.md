---
title: Bölüm 2 - NetX Şifrelemesi'Azure RTOS yükleme ve kullanma
description: Bu bölümde NetX Crypto bileşeninin yüklenmesi, kurulumu ve kullanımıyla ilgili çeşitli sorunların açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 3323af5eaf31ac9c167966522df6477c82e99fdc
ms.sourcegitcommit: c98e5360c9cedbe773af5a44f5163f563c85b570
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/24/2021
ms.locfileid: "110337015"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-crypto"></a>Bölüm 2 - NetX Şifrelemesi'Azure RTOS yükleme ve kullanma

Bu bölümde, NetX Crypto bileşeninin yüklenmesi, Azure RTOS ve kullanımı açık almaktadır.

## <a name="product-distribution"></a>Ürün Dağıtımı

Azure RTOS NetX Şifrelemesi şu [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo) şekildedir: . Paket kaynak dosyaları, ekleme dosyalarını ve bu belgeyi içeren bir PDF dosyasını aşağıdaki gibi içerir:

- **nx_crypto.h:** Genel API üst bilgi dosyası NetX Şifreleme modülü
- **nx_crypto_*.c/h:** NetX Crypto için C/H Kaynak dosyaları
- **nx_crypto_port.h:** Tüm geliştirme aracını içeren ve belirli veri tanımlarını ve yapılarını hedef alan C üst bilgi dosyası.
- **NetX_Crypto_User_Guide.pdf:** NetX Şifreleme Modülünün PDF açıklaması.

## <a name="netx-crypto-installation"></a>NetX Şifreleme Yüklemesi

Daha önce bahsedilen dağıtımın tamamı **NetX** Duo crypto_libraries kök düzeyinde mevcut olan bir dizinde mevcuttur.

NetX Şifrelemesini kullanmak için, daha önce bahsedilen dağıtımın tamamı NetX'in yüklü olduğu dizin düzeyine kopyalanır. Örneğin, "\threadx\arm7\NetX" dizininde NetX yüklüyse,*nx_crypto.* dizinleri "\threadx\arm7\NetXCrypto" dizinine kopyalanır.

NetX Şifrelemesi'nin tek başına modda kullanılası için, daha önce bahsedilen dağıtımın tamamı uygulama projesine kopyalanır. Örneğin **crypto_libraries** bir dizin uygulama projesine kopyalanmış olmalı veya crypto_libraries dizini olan **bir kitaplık** projesi oluşturularak uygulama projesine bağlan olmalıdır. 

## <a name="using-netx-crypto"></a>NetX Şifrelemesi Kullanma

Uygulama kodunun *nx_crypto.h içermesi gerekir.*  Uygulama *nx_crypto.h* ekli olduktan sonra, uygulama kodu bu kılavuzun devamlarında belirtilen NetX Crypto işlev çağrılarını mümkün hale gelir.

## <a name="configuration-options"></a>Yapılandırma Seçenekleri

NetX Şifrelemesi'nin inşası için çeşitli yapılandırma seçenekleri vardır. Aşağıda, her biri ayrıntılı olarak açıklanan tüm seçeneklerin listesi velanmıştır:

- **NX_CRYPTO_MAX_RSA_MODULUS_SIZE:** Tanımlanan, bu seçenek bit olarak beklenen en fazla RSA modu sağlar. Varsayılan değer 4096 bit mod için 4096'dır. Diğer değerler 3072, 2048 veya 1024 olabilir (önerilmez).
- **NX_CRYPTO_SELF_TEST:** Tanımlandı, NetX Şifreleme modülü için kendi kendine testlere olanak sağlar. **NX_CRYPTO_FIPS** simgesi artık kullanım dışı bırakıldı ve yeniden **adlandırıldı NX_CRYPTO_SELF_TEST**
- **NX_CRYPTO_STANDALONE_ENABLE:** Tanımlı, NetX Şifrelemesi'nin tek başına modda (tek başına şifreleme olmadan) Azure RTOS. Varsayılan olarak bu simge tanımlanmamıştır.
