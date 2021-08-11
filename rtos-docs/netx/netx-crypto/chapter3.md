---
title: Bölüm 3 - NetX Şifrelemesi Azure RTOS işlevsel açıklaması
description: Bu bölümde NetX Şifrelemesi'nin işlevsel bir açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 8aa49c130dc2802e95620ccdd4f4d9398c3fd2e55f5896d004e47baa72829848
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116796782"
---
# <a name="chapter-3---functional-description-of-azure-rtos-netx-crypto"></a>Bölüm 3 - NetX Şifrelemesi Azure RTOS işlevsel açıklaması

## <a name="execution-overview"></a>Yürütmeye Genel Bakış

Bu bölümde NetX Crypto için Azure RTOS açıklaması yer almaktadır. NetX Şifreleme uygulamasında iki temel program yürütme türü vardır: başlatma ve uygulama arabirimi çağrıları.

*NetX Şifrelemesi tek başına şifreleme kitaplığı olarak veya ThreadX, NetX ve/veya NetX Secure ile kullanılabilir.*

## <a name="aes"></a>AES

- **Algoritma Standardı:** NetX Şifrelemesi, NIST FIPS 197'ye göre AES'yi şu bağlantılarda bulunabilir: [http://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.197.pdf](http://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.197.pdf)
- **Desteklenen Anahtar Uzunlukları:** 128, 192, 256
- **Desteklenen Modlar:**
  - CBC, CTR, (Anahtar uzunluğu 128-, 192-, 256 bit)
  - XCBC (yalnızca anahtar uzunluğu 128 bit),
  - CCM8 (yalnızca anahtar uzunluğu 128 bit)
- **Bellek Gereksinimleri:** Uygulama, giriş arabelleği ve çıkış arabelleği ile AES denetim yapısını belirtir. AES denetim yapısı, API'ye yapılan çağrılar arasında AES algoritma durumunu sürdürür. Giriş arabelleği şifrelenen veya şifresi çözülecek verileri içerir ve rastgele boyut olabilir. Çıktı arabelleği AES tarafından AES tarafından işlenen verileri depolamak için kullanılır. Çıkış arabelleği boyutu, giriş arabelleği boyutundan küçük olmalı ve AES blok boyutunun 16 bayt'ın katları olmalıdır. Giriş ve çıkış arabellekleri bitişik bellek olmalı ve özel olarak yerinde şifreleme (giriş ve çıkış için aynı bellek kullanılarak) dışında çakışmaz. Yerinde şifrelerken, çıkış arabelleği giriş arabelleğiyle tam olarak aynı konumda başlar ve giriş arabelleğinden küçük değildir. AES şifrelemesi yerinde çalışırken fazladan karalama belleği gerekmez.

## <a name="3des"></a>3DES

- **Algoritma Standardı:** NetX Crypto, NIST Özel Yayını 800-67 rev 2: "Üçlü Veri Şifreleme Algoritması (TDES) Blok Şifrelemesi için öneri" konularına göre Tripple *DES'i (3DES olarak* da bilinir) uygulamaya almaktadır: [https://csrc.nist.gov/publications/detail/sp/800-67/rev-2/final](https://csrc.nist.gov/publications/detail/sp/800-67/rev-2/final)
- **Desteklenen Anahtar Uzunluğu:** 64 * 3 = 192
- **Bellek Yeniden Kullanımı:**: Yok

NetX Crypto'da "3DES" terimi, "TDES" ile birbirinin yerine kullanılır.

## <a name="md5"></a>MD5

- **Algoritma Standardı:** NetX Crypto, RFC 1321'e göre *MD5'i kullanır: "MD5 Message-Digest Algoritması"*
- **Bellek Gereksinimi:** Uygulamanın, MD5 işlemleri arasında durumu korumak için kullanılan bir MD5 denetim bloğu yapısı temini gerekir.

## <a name="sha1-sha256512"></a>SHA1, SHA256/512

- **Algoritma Standardı:** NetX Crypto, NIST FIPS 180-4 yayınına göre SHA1/256/512'yi uygulamaya almaktadır: "*Güvenli* Karma Standart ", burada bulunabilir: [http://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.180-4.pdf](http://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.180-4.pdf)
- **Karma blok boyutu:**:
  - SHA1: 160 bit karma değeri
  - SHA 224: 224 bit karma değeri
  - SHA 256: 256 bit karma değeri
  - SHA 384: 384 bit karma değeri
  - SHA 512: 512 bit karma değeri
  - SHA 512/224: 224 bit karma değeri
  - SHA 512/256: 256 bit karma değeri

  NetX Crypto'da SHA256 yordamları SHA256 ve SHA224'e sahip olmak için kullanılır. SHA512 yordamları SHA512, SHA384, SHA512/224 ve SHA512/256'yı teslim etmek için kullanılır.
- **Bellek Gereksinimi:** Uygulama, işlemler arasındaki durumu korumak için bir SHA denetim bloğu yapısı sağlamış olması gerekir.

## <a name="rsa"></a>RSA

- **Standart:** NetX Crypto, RFC 8017 olarak yayımlanan ve şu bağlantılarda da buluna standart "*PKCS #1 v2.2: RSA Şifreleme* Standardı " ile RSA'yi uygulamaya almaktadır: [https://www.emc.com/collateral/white-papers/h11300-pkcs-1v2-2-rsa-cryptography-standard-wp.pdf](https://www.emc.com/collateral/white-papers/h11300-pkcs-1v2-2-rsa-cryptography-standard-wp.pdf)
- **Bellek Gereksinimi:** Uygulamanın işlemler arasındaki durumu korumak ve ara hesaplamalar için gerekli "karalama" arabellek alanı sağlamak için bir RSA denetim bloğu yapısı sağlaması gerekir.

## <a name="hmac"></a>Hmac

- **Standart:** NetX Crypto, HMAC'i FIPS PUB 198-1: "*Keyed-Hash İleti Kimlik Doğrulama Kodu (HMAC) " (HMAC)*", şu bağlantılarda bulunabilir: [https://csrc.nist.gov/csrc/media/publications/fips/198/1/final/documents/fips-198-1_final.pdf](https://csrc.nist.gov/csrc/media/publications/fips/198/1/final/documents/fips-198-1_final.pdf)
- **Bellek Gereksinimi:** Uygulama, işlemler arasındaki durumu korumak için bir HMAC denetim bloğu yapısı sağlamış olması gerekir. Sağlanan gerçek denetim bloğu, istenen temel karma işlemine (sha1, MD5 gibi) bağlıdır.

## <a name="elliptic-curve"></a>Üç Nokta Eğrisi

- **Standart:** NetX Şifrelemesi Üç Nokta Eğrisi'ne uygulanır. Desteklenen adlandırılmış eğriler (yalnızca asal alan):
  - P-192
  - P-224
  - P-256
  - P-384
  - P-521

   > [!TIP]
   > Sıkıştırılmamış biçim desteklenmektedir. SEC1-v1'in 2.3.3 ve 2.3.4 bölümüne bakın: [http://www.secg.org/sec1-v2.pdf](http://www.secg.org/sec1-v2.pdf)

- **Bellek Gereksinimi:** Hiçbiri

## <a name="ecdsa"></a>Ecdsa

- **Standart:** NetX Crypto, FIPS PUB 186-4'e göre ECDSA'yı uygulamaya almaktadır: "*Digital Signature Standard (DSS)*", which can found at: [https://nvlpubs.nist.gov/nistpubs/fips/nist.fips.186-4.pdf](https://nvlpubs.nist.gov/nistpubs/fips/nist.fips.186-4.pdf)
- **Bellek Gereksinimi:** Uygulama, işlemler arasındaki durumu korumak için bir ECDSA denetim bloğu yapısı sağlamış olması gerekir.

## <a name="ecdh"></a>Ecdh

> [!IMPORTANT]
> Bu Azure RTOS 6.0'da ECDH yordamları yalnızca ECDHE şifrelemesi için statik özel anahtarla ECDH olarak kullanılmalıdır ve giriş noktası doğrulamasının güvenli olması gerekir.

- **Standart:** NetX Crypto, FIPS PUB 800-56Ar2:"Recommendation for Pair-Wise Key Establishment Schemes Using Discrete Logarithm Cryptography" (Ayrık Logarithm Şifrelemesi Kullanarak Pair-Wise Anahtar Oluşturma Şemaları için Öneri) bağlantısına göre ECDH'yi uygulamaya almaktadır. Bu şemada şu bilgiler bulunabilir: [https://nvlpubs.nist.gov/nistpubs/specialpublications/nist.sp.800-56ar2.pdf](https://nvlpubs.nist.gov/nistpubs/specialpublications/nist.sp.800-56ar2.pdf)
- **Bellek Gereksinimi:** Uygulama, işlemler arasındaki durumu korumak için bir ECDH denetim bloğu yapısı sağlamış olması gerekir.

## <a name="drbg"></a>DRBG

- **Standart:** NetX Crypto, FIPS PUB 800-90Ar1: "Belirlenimci Rastgele Bit Oluşturucuları Kullanarak Rastgele Sayı Oluşturma Önerisi" bağlantısına göre DRBG'yi şu bağlantılarda bulunabilir: [https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-90Ar1.pdf](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-90Ar1.pdf)
- **Bellek Gereksinimi:** Uygulama, işlemler arasında durumu korumak için bir DRBG denetim bloğu yapısı sağlamış olması gerekir.

## <a name="fips-compliant"></a>FIPS-Compliant

NetX Crypto FIPS 140-2