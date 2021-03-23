---
title: Bölüm 3-Azure RTOS NetX şifrelemesi için Işlevsel açıklama
description: Bu bölüm NetX şifrelemesi için işlevsel bir açıklama içerir.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 4ecdbfe99daa000d109908f834b139dcaf321491
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825594"
---
# <a name="chapter-3---functional-description-of-azure-rtos-netx-crypto"></a>Bölüm 3-Azure RTOS NetX şifrelemesi için Işlevsel açıklama

## <a name="execution-overview"></a>Yürütmeye genel bakış

Bu bölüm, Azure RTOS NetX şifrelemesi için işlevsel bir açıklama içerir. NetX şifre uygulamasında iki adet program yürütme türü vardır: başlatma ve uygulama arabirimi çağrıları.

*NetX şifrelemesi tek başına bir şifreleme kitaplığı olarak kullanılabilir veya ThreadX, NetX ve/veya NetX güvenli ile kullanılabilir.*

## <a name="aes"></a>AES

- **Algoritma standardı:**: NETX şifre, şu adreste bulunan nıst FIPS 197 'e göre AES uygular: [http://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.197.pdf](http://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.197.pdf)
- **Desteklenen anahtar uzunlukları**: 128, 192, 256
- **Desteklenen modlar**:
  - CBC, MRK, (anahtar uzunluğu 128-, 192-, 256-bit)
  - XCBC (yalnızca anahtar uzunluğu 128-bit),
  - CCM8 (yalnızca anahtar uzunluğu 128-bit)
- **Bellek gereksinimleri**: uygulama giriş arabelleğini ve çıkış arabelleğini ve bir AES denetim yapısını belirtir. AES denetim yapısı, API çağrıları arasında AES algoritma durumunu korur. Giriş arabelleği şifrelenecek veya şifresinin çözülebilecek verileri içerir ve rastgele bir boyut olabilir. Çıktı arabelleği, AES tarafından işlenmekte olan verileri depolamak için AES tarafından kullanılır. Çıkış arabellek boyutu, giriş arabelleği boyutundan küçük olmamalı ve 16 baytlık bir, AES blok boyutu olmalıdır. Giriş ve çıkış arabelleklerinin, yerinde şifreleme özel durumu dışında (giriş ve çıkış için aynı belleği kullanarak) bitişik bellek olması ve çakışmayabilir. Yerinde şifreleme yapıldığında, çıkış arabelleği giriş arabelleği ile tam olarak aynı konumda başlar ve giriş arabelleğinden küçük olmaması gerekir. AES şifrelemesi yerinde çalışırken ek karalama belleği gerekli değildir.

## <a name="3des"></a>3DES

- **Algoritma standardı**: NETX ŞIFRESI, NIST özel yayını 800-67 Rev 2: *"Recommendataion", "Üçlü Veri şifreleme algoritması (Tdes) için*), şurada bulunabilir: [https://csrc.nist.gov/publications/detail/sp/800-67/rev-2/final](https://csrc.nist.gov/publications/detail/sp/800-67/rev-2/final)
- **Anahtar uzunluğu destekleniyor**: 64 * 3 = 192
- **Bellek Requreiment:**: None

NetX şifrelemesi ' nde, "3DES" terimi "TDES" ile birbirinin yerine kullanılır.

## <a name="md5"></a>MD5

- **Algoritma standardı**: NETX ŞIFRE, RFC 1321 ' e göre MD5 uygular: *"MD5 Message-Digest algoritması"*
- **Bellek gereksinimi**: uygulama, MD5 işlemleri arasında durumu korumak için kullanılan bir MD5 denetim bloğu yapısı sağlamalıdır.

## <a name="sha1-sha256512"></a>SHA1, SHA256/512

- **Algoritma standardı:** NetX şifrelemesi, NıST FIPS yayını 180-4 ' a göre SHA1/256/512 ' yi uygular: "*güvenli karma standart*", şurada bulunabilir: [http://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.180-4.pdf](http://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.180-4.pdf)
- **Karma blok boyutu:**:
  - SHA1:160 bit karma değeri
  - SHA 224:224 bit karma değeri
  - SHA 256:256 bit karma değeri
  - SHA 384:384 bit karma değeri
  - SHA 512:512 bit karma değeri
  - SHA 512/224:224 bitleri karma değeri
  - SHA 512/256:256 bitleri karma değeri

  NetX şifrelemesi ' nde, SHA256 yordamları hadn SHA256 ve SHA224 için kullanılır. SHA512 olur yordamları, SHA512 olur, SHA384, SHA512 olur/224 ve SHA512 olur/256 için kullanılır.
- **Bellek gereksinimi:** Uygulamanın, işlemler arasında durumu korumak için bir SHA denetim bloğu yapısı sağlaması gerekir.

## <a name="rsa"></a>RSA

- **Standart:** NetX şifrelemesi, RFC 8017 olarak yayınlanan ve ayrıca şurada bulunan standart "*PKCS #1 v 2.2: RSA şifreleme standardı*" ÖĞESINE göre RSA uygular: [https://www.emc.com/collateral/white-papers/h11300-pkcs-1v2-2-rsa-cryptography-standard-wp.pdf](https://www.emc.com/collateral/white-papers/h11300-pkcs-1v2-2-rsa-cryptography-standard-wp.pdf)
- **Bellek gereksinimi:** Uygulama, işlemler arasında durumu korumak için bir RSA denetim bloğu yapısı sağlamalıdır ve ara hesaplamalar için gerekli "boş" arabellek alanı sağlamak için gereklidir.

## <a name="hmac"></a>HMAC

- **Standart:** NetX şifrelemesi FIPS PUB 198-1: "*Keyed-Hash ileti kimlik doğrulama kodu (HMAC)*" ÖĞESINE göre HMAC uygular: [https://csrc.nist.gov/csrc/media/publications/fips/198/1/final/documents/fips-198-1_final.pdf](https://csrc.nist.gov/csrc/media/publications/fips/198/1/final/documents/fips-198-1_final.pdf)
- **Bellek gereksinimi:** Uygulamanın, işlemler arasında durumu korumak için HMAC denetim bloğu yapısı sağlaması gerekir. Sağlanan gerçek denetim bloğu, istenen temel karma işleme (ör. SHA1, MD5) bağlıdır.

## <a name="elliptic-curve"></a>Eliptik Eğri

- **Standart:** NetX şifre eliptik eğri uygular. Desteklenen adlandırılmış eğriler şunlardır: (yalnızca ana alan):
  - P-192
  - P-224
  - P-256
  - P-384
  - P-521

   > [!TIP]
   > Sıkıştırılmamış biçim destekleniyor. Bkz. Bölüm 2.3.3 ve 2.3.4 in SEC1-v1: [http://www.secg.org/sec1-v2.pdf](http://www.secg.org/sec1-v2.pdf)

- **Bellek gereksinimi:** Seçim

## <a name="ecdsa"></a>ECDSA

- **Standart:** NetX şifrelemesi, şu adreste bulunan FIPS PUB 186-4: "*dijital Imza standardı (DSS)*" UYARıNCA ECDSA 'yı uygular: [https://nvlpubs.nist.gov/nistpubs/fips/nist.fips.186-4.pdf](https://nvlpubs.nist.gov/nistpubs/fips/nist.fips.186-4.pdf)
- **Bellek gereksinimi:** Uygulamanın, işlemler arasında durumu korumak için bir ECDSA denetim bloğu yapısı sağlaması gerekir.

## <a name="ecdh"></a>ECDH

> [!IMPORTANT]
> Azure RTOS 6,0 ' de ECDH yordamları yalnızca ECDHE şifrelemesi için kullanılmalıdır, statik bir özel anahtarla ECDH, giriş noktası doğrulamasının güvenli olmasını gerektirir.

- **Standart:** NetX şifrelemesi, şu adreste bulunabilir: "ayrık bir şifreleme şifrelemesi kullanarak Pair-Wise anahtar oluşturma şemaları için öneri" ile ECDH uygular. [https://nvlpubs.nist.gov/nistpubs/specialpublications/nist.sp.800-56ar2.pdf](https://nvlpubs.nist.gov/nistpubs/specialpublications/nist.sp.800-56ar2.pdf)
- **Bellek gereksinimi:** Uygulamanın, işlemler arasında durumu korumak için bir ECDH denetim bloğu yapısı sağlaması gerekir.

## <a name="drbg"></a>DRBG

- **Standart:** NetX şifrelemesi, şu adreste bulunabilen, FIPS 'nin 800-90Ar1: "rastgele sayı oluşturma önerisi" belirleyici bir bit oluşturanlar kullanılarak ayarlanabilir. [https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-90Ar1.pdf](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-90Ar1.pdf)
- **Bellek gereksinimi:** Uygulamanın, işlemler arasında durumu korumak için bir DRBG denetim bloğu yapısı sağlaması gerekir.

## <a name="fips-compliant"></a>FIPS-Compliant

NetX şifre FIPS 140-2