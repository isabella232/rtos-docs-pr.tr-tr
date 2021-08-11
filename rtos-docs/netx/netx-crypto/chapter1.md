---
title: Bölüm 1-Azure RTOS NetX şifrelemeye giriş
description: NetX şifre, veri şifreleme ve kimlik doğrulama hizmetleri sağlamak için tasarlanan, yüksek performanslı bir gerçek zamanlı şifreleme algoritmaları uygulamasıdır.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 1b5ee0336ba9e867a628dc5db4f0c029f68ff45c81d68ceb6299e3469d5e2b49
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116796812"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-crypto"></a>Bölüm 1-Azure RTOS NetX şifrelemeye giriş

Azure RTOS NetX şifresi, veri şifreleme ve kimlik doğrulama hizmetleri sağlamak için tasarlanmış, yüksek performanslı bir gerçek zamanlı şifreleme algoritmaları uygulamasıdır. NetX şifrelemesi, NetX güvenli TLS, DTLS ve IPSec modülleri için çalışmak üzere tasarlanmıştır. Uygulamalar, ağ güvenliği dışında tek başına bir modül olarak NetX şifrelemesi de kullanabilir.

## <a name="netx-crypto-unique-features"></a>NetX şifre benzersiz özellikleri

NetX şifrelemesi, neredeyse tüm C/C++ derleyicileri ile uyumlu standart C dilinde (C99) uygulanır. Modüler tasarımı, bir uygulamanın yalnızca kullanması gereken şifre algoritmalarından bağlantı sağlamasına izin verir, bu nedenle minimum kod boyutunu elde edin. Uygulama, 32 bitlik mikro işlemcilerle çalışacak şekilde tasarlanmıştır ve yalnızca temel matematik işlemlerini (toplama, çıkarma, çarpma, bölme, mantıksal ve, veya bit kaydırma işlemleri) kullanır. Tüm bu işlemler, 32 bitlik miktarlarla kullanılır ve NetX şifrelemesi en fazla 32 bit mikro işlemci arasında taşınabilir hale getirir. Uygulama, derin gömülü uygulamaları hedefleyen, kaynak kısıtlı mikro işlemcilerde çalışmak üzere özel olarak iyileştirilmiştir.

## <a name="algorithms-supported-by-netx-crypto"></a>NetX şifrelemesi tarafından desteklenen algoritmalar

NetX şifrelemesi, aşağıdaki şifreleme algoritmalarını destekler. NetX şifrelemesi, küçük bir bellek kaplama ve verimli yürütme gerektiren gerçek zamanlı bir işletim sistemi ve platformların kısıtlamaları dahilinde tüm genel önerilere ve temel gereksinimlere uyar.

| Algoritma       | Anahtar uzunluğu (bit)      |
| --------------- | ---------------------- |
| AES (CBC, MRK)   | 128, 192, 256          |
| AES (XCBC)       | 128                    |
| AES-CCM 8       | 128                    |
| 3DES (CBC)       | 192                    |
| HMAC-SHA1       | Herhangi bir uzunluk             |
| HMAC-SHA224     | Herhangi bir uzunluk             |
| HMAC-SHA256     | Herhangi bir uzunluk             |
| HMAC-SHA384     | Herhangi bir uzunluk             |
| HMAC-SHA512 OLUR     | Herhangi bir uzunluk             |
| HMAC-SHA512 OLUR/224 | Herhangi bir uzunluk             |
| HMAC-SHA512 OLUR/256 | Herhangi bir uzunluk             |
| HMAC-MD5        | Herhangi bir uzunluk             |
| RSA             | 1024, 2048, 3072, 4096 |

| Algoritma       | Özet uzunluğu (bit) | Blok boyutu (bit) |
| --------------- | -------------------- | ----------------- |
| SHA1            | 160                  | 512               |
| SHA224          | 224                  | 512               |
| SHA256          | 256                  | 512               |
| SHA384          | 384                  | 1024              |
| SHA512          | 512                  | 1024              |
| MD5             | 128                  | 512               |
| HMAC-SHA1       | 160                  | 512               |
| HMAC-SHA224     | 224                  | 512               |
| HMAC-SHA256     | 256                  | 512               |
| HMAC-SHA384     | 384                  | 1024              |
| HMAC-SHA512 OLUR     | 512                  | 1024              |
| HMAC-SHA512 OLUR/224 | 224                  | 1024              |
| HMAC-SHA512 OLUR/256 | 256                  | 1024              |
| HMAC-MD5        | 128                  | 512               |
| Eliptik Eğri  | P192/224/256/384/521 |                   |

## <a name="netx-crypto-requirements"></a>NetX şifreleme gereksinimleri

TBD: bellek gereksinimi.. Kesme/yeniden entrant güvenli mi? Tartışma gerekiyor

## <a name="netx-crypto-constraints"></a>NetX şifre kısıtlamaları

Yok.
