---
title: Bölüm 2-Azure RTOS NetX şifre yüklemesi ve kullanımı
description: Bu bölümde, NetX şifreleme bileşeninin yüklenmesi, kurulumu ve kullanımı ile ilgili çeşitli sorunların bir açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 1616667c5efd73229ed69bcd4e5de5f80e5826f9
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826818"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-crypto"></a>Bölüm 2-Azure RTOS NetX şifre yüklemesi ve kullanımı

Bu bölümde, Azure RTOS NetX şifreleme bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların bir açıklaması yer almaktadır.

## <a name="product-distribution"></a>Ürün dağıtımı

Azure RTOS NetX şifrelemesi adresinde bulunabilir [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo) . Paket, kaynak dosyaları, içerme dosyaları ve bu belgeyi içeren bir PDF dosyasını aşağıdaki gibi içerir:

- **nx_crypto. h**: ortak API üstbilgi dosyası NETX şifreleme modülü
- **nx_crypto_ *. c/h**: NETX şifrelemesi için c/h kaynak dosyaları
- **nx_crypto_port. h**: tüm geliştirme araçlarını ve hedef belirli veri tanımlarını ve yapıları Içeren C üstbilgi dosyası.
- **NetX_Crypto_User_Guide.pdf**: NETX şifre modülünün PDF açıklaması.

## <a name="netx-crypto-installation"></a>NetX şifre yüklemesi

Daha önce bahsedilen tüm dağıtım, NetX Duo deposunun kök düzeyinde bulunan **crypto_libraries** dizininde mevcuttur.

NetX şifre kullanabilmesi için, daha önce bahsedilen dağıtımın tamamı, NetX 'in yüklü olduğu aynı dizin düzeyine kopyalanmalıdır. Örneğin, "\threadx\arm7\NetX" dizininde NetX yüklüyse nx_crypto *.* dizinler "\Threadx\arm7\netxşifre" dizinine kopyalanmalıdır.

Tek başına modda kullanılmak üzere NetX şifrelemesi için, daha önce bahsedilen dağıtımın tamamının uygulama projesine kopyalanması gerekir. Örneğin **crypto_libraries** dizin uygulama projesine kopyalanmalıdır ya da **crypto_libraries** dizine sahip bir kitaplık projesi oluşturulup uygulama projesine bağlanmalıdır. 

## <a name="using-netx-crypto"></a>NetX şifre kullanımı

NetX şifre kullanımı kolaydır. Temel olarak, uygulama kodu *nx_crypto. h* öğesini içermelidir.  *Nx_crypto. h* dahil olduğunda, uygulama kodu daha sonra bu kılavuzda belirtilen NETX şifre işlev çağrılarını yapabilir.

## <a name="configuration-options"></a>Yapılandırma seçenekleri

NetX şifrelemesi oluşturmak için birkaç yapılandırma seçeneği vardır. Aşağıda, her birinin ayrıntılı olarak açıklandığı tüm seçeneklerin bir listesi verilmiştir:

- **NX_CRYPTO_MAX_RSA_MODULUS_SIZE**: tanımlı, bu seçenek bit cinsinden beklenen maksimum RSA mod sayısını verir. 4096 bit mod için varsayılan değer 4096 ' dir. Diğer değerler 3072, 2048 veya 1024 (önerilmez) olabilir.
- **NX_CRYPTO_FIPS**: tanımlı, bu seçenek FIPS-Compliant kullanımı için gerekli ek güvenlik özelliklerini sunar. Bu seçenek FIPS olmayan derleme için etkinleştirilmemiş.
- **NX_CRYPTO_STANDALONE_ENABLE**: tanımlı, NETX şifrelemesi 'nin tek başına modda kullanılmasını sağlar (Azure RTOS olmadan). Varsayılan olarak bu simge tanımlı değildir.
