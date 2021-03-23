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
# <a name="chapter-3---functional-description-of-azure-rtos-netx-crypto"></a><span data-ttu-id="07db2-103">Bölüm 3-Azure RTOS NetX şifrelemesi için Işlevsel açıklama</span><span class="sxs-lookup"><span data-stu-id="07db2-103">Chapter 3 - Functional description of Azure RTOS NetX Crypto</span></span>

## <a name="execution-overview"></a><span data-ttu-id="07db2-104">Yürütmeye genel bakış</span><span class="sxs-lookup"><span data-stu-id="07db2-104">Execution Overview</span></span>

<span data-ttu-id="07db2-105">Bu bölüm, Azure RTOS NetX şifrelemesi için işlevsel bir açıklama içerir.</span><span class="sxs-lookup"><span data-stu-id="07db2-105">This chapter contains a functional description of Azure RTOS NetX Crypto.</span></span> <span data-ttu-id="07db2-106">NetX şifre uygulamasında iki adet program yürütme türü vardır: başlatma ve uygulama arabirimi çağrıları.</span><span class="sxs-lookup"><span data-stu-id="07db2-106">There are two primary types of program execution in a NetX Crypto application: initialization and application interface calls.</span></span>

<span data-ttu-id="07db2-107">*NetX şifrelemesi tek başına bir şifreleme kitaplığı olarak kullanılabilir veya ThreadX, NetX ve/veya NetX güvenli ile kullanılabilir.*</span><span class="sxs-lookup"><span data-stu-id="07db2-107">*NetX Crypto can be used as a standalone cryptographic library, or can be used with ThreadX, NetX, and/or NetX Secure.*</span></span>

## <a name="aes"></a><span data-ttu-id="07db2-108">AES</span><span class="sxs-lookup"><span data-stu-id="07db2-108">AES</span></span>

- <span data-ttu-id="07db2-109">**Algoritma standardı:**: NETX şifre, şu adreste bulunan nıst FIPS 197 'e göre AES uygular: [http://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.197.pdf](http://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.197.pdf)</span><span class="sxs-lookup"><span data-stu-id="07db2-109">**Algorithm Standard:**:  NetX Crypto implements AES according to NIST FIPS 197, which can be found at: [http://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.197.pdf](http://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.197.pdf)</span></span>
- <span data-ttu-id="07db2-110">**Desteklenen anahtar uzunlukları**: 128, 192, 256</span><span class="sxs-lookup"><span data-stu-id="07db2-110">**Key Lengths Supported**: 128, 192, 256</span></span>
- <span data-ttu-id="07db2-111">**Desteklenen modlar**:</span><span class="sxs-lookup"><span data-stu-id="07db2-111">**Modes Supported**:</span></span>
  - <span data-ttu-id="07db2-112">CBC, MRK, (anahtar uzunluğu 128-, 192-, 256-bit)</span><span class="sxs-lookup"><span data-stu-id="07db2-112">CBC, CTR, (Key length 128-, 192-, 256-bit)</span></span>
  - <span data-ttu-id="07db2-113">XCBC (yalnızca anahtar uzunluğu 128-bit),</span><span class="sxs-lookup"><span data-stu-id="07db2-113">XCBC (key length 128-bit only),</span></span>
  - <span data-ttu-id="07db2-114">CCM8 (yalnızca anahtar uzunluğu 128-bit)</span><span class="sxs-lookup"><span data-stu-id="07db2-114">CCM8 (key length 128-bit only)</span></span>
- <span data-ttu-id="07db2-115">**Bellek gereksinimleri**: uygulama giriş arabelleğini ve çıkış arabelleğini ve bir AES denetim yapısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="07db2-115">**Memory Requirements**: Application specifies input buffer and output buffer and an AES control structure.</span></span> <span data-ttu-id="07db2-116">AES denetim yapısı, API çağrıları arasında AES algoritma durumunu korur.</span><span class="sxs-lookup"><span data-stu-id="07db2-116">The AES control structure maintains AES algorithm state between calls to the API.</span></span> <span data-ttu-id="07db2-117">Giriş arabelleği şifrelenecek veya şifresinin çözülebilecek verileri içerir ve rastgele bir boyut olabilir.</span><span class="sxs-lookup"><span data-stu-id="07db2-117">The input buffer contains data to be encrypted or decrypted, and can be arbitrary size.</span></span> <span data-ttu-id="07db2-118">Çıktı arabelleği, AES tarafından işlenmekte olan verileri depolamak için AES tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="07db2-118">The output buffer is used by AES to store data being processed by AES.</span></span> <span data-ttu-id="07db2-119">Çıkış arabellek boyutu, giriş arabelleği boyutundan küçük olmamalı ve 16 baytlık bir, AES blok boyutu olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="07db2-119">The output buffer size must be no smaller than the input buffer size, and must be a multiple of 16 bytes, the AES block size.</span></span> <span data-ttu-id="07db2-120">Giriş ve çıkış arabelleklerinin, yerinde şifreleme özel durumu dışında (giriş ve çıkış için aynı belleği kullanarak) bitişik bellek olması ve çakışmayabilir.</span><span class="sxs-lookup"><span data-stu-id="07db2-120">The input and output buffers must be contiguous memory and may not overlap, except in the special case of encrypting in-place (using the same memory for input and output).</span></span> <span data-ttu-id="07db2-121">Yerinde şifreleme yapıldığında, çıkış arabelleği giriş arabelleği ile tam olarak aynı konumda başlar ve giriş arabelleğinden küçük olmaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="07db2-121">When encrypting in-place, the output buffer starts at exactly the same location as the input buffer, and must be no smaller than the input buffer.</span></span> <span data-ttu-id="07db2-122">AES şifrelemesi yerinde çalışırken ek karalama belleği gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="07db2-122">When AES encryption operates in-place no extra scratch memory is required.</span></span>

## <a name="3des"></a><span data-ttu-id="07db2-123">3DES</span><span class="sxs-lookup"><span data-stu-id="07db2-123">3DES</span></span>

- <span data-ttu-id="07db2-124">**Algoritma standardı**: NETX ŞIFRESI, NIST özel yayını 800-67 Rev 2: *"Recommendataion", "Üçlü Veri şifreleme algoritması (Tdes) için*), şurada bulunabilir: [https://csrc.nist.gov/publications/detail/sp/800-67/rev-2/final](https://csrc.nist.gov/publications/detail/sp/800-67/rev-2/final)</span><span class="sxs-lookup"><span data-stu-id="07db2-124">**Algorithm Standard**: NetX Crypto implements Tripple DES(TDES, also known as 3DES) according to NIST Special Publication 800-67 rev 2: *"Recommendataion for the Triple Data Encryption Algorithm (TDES) Block Cipher"*, which can be found at: [https://csrc.nist.gov/publications/detail/sp/800-67/rev-2/final](https://csrc.nist.gov/publications/detail/sp/800-67/rev-2/final)</span></span>
- <span data-ttu-id="07db2-125">**Anahtar uzunluğu destekleniyor**: 64 \* 3 = 192</span><span class="sxs-lookup"><span data-stu-id="07db2-125">**Key Length Supported**: 64 \* 3 = 192</span></span>
- <span data-ttu-id="07db2-126">**Bellek Requreiment:**: None</span><span class="sxs-lookup"><span data-stu-id="07db2-126">**Memory Requreiment:**: None</span></span>

<span data-ttu-id="07db2-127">NetX şifrelemesi ' nde, "3DES" terimi "TDES" ile birbirinin yerine kullanılır.</span><span class="sxs-lookup"><span data-stu-id="07db2-127">In NetX Crypto, the term "3DES" is used interchangeably with "TDES".</span></span>

## <a name="md5"></a><span data-ttu-id="07db2-128">MD5</span><span class="sxs-lookup"><span data-stu-id="07db2-128">MD5</span></span>

- <span data-ttu-id="07db2-129">**Algoritma standardı**: NETX ŞIFRE, RFC 1321 ' e göre MD5 uygular: *"MD5 Message-Digest algoritması"*</span><span class="sxs-lookup"><span data-stu-id="07db2-129">**Algorithm Standard**: NetX Crypto implements MD5 according to RFC 1321: *"The MD5 Message-Digest Algorithm"*</span></span>
- <span data-ttu-id="07db2-130">**Bellek gereksinimi**: uygulama, MD5 işlemleri arasında durumu korumak için kullanılan bir MD5 denetim bloğu yapısı sağlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="07db2-130">**Memory Requirement**: The application must supply an MD5 control block structure, used to maintain state between MD5 operations.</span></span>

## <a name="sha1-sha256512"></a><span data-ttu-id="07db2-131">SHA1, SHA256/512</span><span class="sxs-lookup"><span data-stu-id="07db2-131">SHA1, SHA256/512</span></span>

- <span data-ttu-id="07db2-132">**Algoritma standardı:** NetX şifrelemesi, NıST FIPS yayını 180-4 ' a göre SHA1/256/512 ' yi uygular: "*güvenli karma standart*", şurada bulunabilir: [http://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.180-4.pdf](http://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.180-4.pdf)</span><span class="sxs-lookup"><span data-stu-id="07db2-132">**Algorithm Standard:** NetX Crypto implements SHA1/256/512 according to NIST FIPS publication 180-4: "*Secure Hash Standard*", which can be found at: [http://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.180-4.pdf](http://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.180-4.pdf)</span></span>
- <span data-ttu-id="07db2-133">**Karma blok boyutu:**:</span><span class="sxs-lookup"><span data-stu-id="07db2-133">**Hash block size:**:</span></span>
  - <span data-ttu-id="07db2-134">SHA1:160 bit karma değeri</span><span class="sxs-lookup"><span data-stu-id="07db2-134">SHA1: 160 bits hash value</span></span>
  - <span data-ttu-id="07db2-135">SHA 224:224 bit karma değeri</span><span class="sxs-lookup"><span data-stu-id="07db2-135">SHA 224: 224 bits hash value</span></span>
  - <span data-ttu-id="07db2-136">SHA 256:256 bit karma değeri</span><span class="sxs-lookup"><span data-stu-id="07db2-136">SHA 256: 256 bits hash value</span></span>
  - <span data-ttu-id="07db2-137">SHA 384:384 bit karma değeri</span><span class="sxs-lookup"><span data-stu-id="07db2-137">SHA 384: 384 bits hash value</span></span>
  - <span data-ttu-id="07db2-138">SHA 512:512 bit karma değeri</span><span class="sxs-lookup"><span data-stu-id="07db2-138">SHA 512: 512 bits hash value</span></span>
  - <span data-ttu-id="07db2-139">SHA 512/224:224 bitleri karma değeri</span><span class="sxs-lookup"><span data-stu-id="07db2-139">SHA 512/224: 224 bits hash value</span></span>
  - <span data-ttu-id="07db2-140">SHA 512/256:256 bitleri karma değeri</span><span class="sxs-lookup"><span data-stu-id="07db2-140">SHA 512/256: 256 bits hash value</span></span>

  <span data-ttu-id="07db2-141">NetX şifrelemesi ' nde, SHA256 yordamları hadn SHA256 ve SHA224 için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="07db2-141">In NetX Crypto, SHA256 routines are used to hadn SHA256 and SHA224.</span></span> <span data-ttu-id="07db2-142">SHA512 olur yordamları, SHA512 olur, SHA384, SHA512 olur/224 ve SHA512 olur/256 için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="07db2-142">SHA512 routines are used to hand SHA512, SHA384, SHA512/224 and SHA512/256.</span></span>
- <span data-ttu-id="07db2-143">**Bellek gereksinimi:** Uygulamanın, işlemler arasında durumu korumak için bir SHA denetim bloğu yapısı sağlaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="07db2-143">**Memory Requirement:** The application must provide a SHA control block structure for maintaining state between operations.</span></span>

## <a name="rsa"></a><span data-ttu-id="07db2-144">RSA</span><span class="sxs-lookup"><span data-stu-id="07db2-144">RSA</span></span>

- <span data-ttu-id="07db2-145">**Standart:** NetX şifrelemesi, RFC 8017 olarak yayınlanan ve ayrıca şurada bulunan standart "*PKCS #1 v 2.2: RSA şifreleme standardı*" ÖĞESINE göre RSA uygular: [https://www.emc.com/collateral/white-papers/h11300-pkcs-1v2-2-rsa-cryptography-standard-wp.pdf](https://www.emc.com/collateral/white-papers/h11300-pkcs-1v2-2-rsa-cryptography-standard-wp.pdf)</span><span class="sxs-lookup"><span data-stu-id="07db2-145">**Standard:** NetX Crypto implements RSA according to the standard "*PKCS #1 v2.2: RSA Cryptography Standard*", which is published as RFC 8017 and can also be found at: [https://www.emc.com/collateral/white-papers/h11300-pkcs-1v2-2-rsa-cryptography-standard-wp.pdf](https://www.emc.com/collateral/white-papers/h11300-pkcs-1v2-2-rsa-cryptography-standard-wp.pdf)</span></span>
- <span data-ttu-id="07db2-146">**Bellek gereksinimi:** Uygulama, işlemler arasında durumu korumak için bir RSA denetim bloğu yapısı sağlamalıdır ve ara hesaplamalar için gerekli "boş" arabellek alanı sağlamak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="07db2-146">**Memory Requirement:** The application must provide an RSA control block structure for maintaining state between operations and to provide necessary "scratch" buffer space for intermediate calculations.</span></span>

## <a name="hmac"></a><span data-ttu-id="07db2-147">HMAC</span><span class="sxs-lookup"><span data-stu-id="07db2-147">HMAC</span></span>

- <span data-ttu-id="07db2-148">**Standart:** NetX şifrelemesi FIPS PUB 198-1: "*Keyed-Hash ileti kimlik doğrulama kodu (HMAC)*" ÖĞESINE göre HMAC uygular: [https://csrc.nist.gov/csrc/media/publications/fips/198/1/final/documents/fips-198-1_final.pdf](https://csrc.nist.gov/csrc/media/publications/fips/198/1/final/documents/fips-198-1_final.pdf)</span><span class="sxs-lookup"><span data-stu-id="07db2-148">**Standard:** NetX Crypto implements HMAC according to FIPS PUB 198-1: "*The Keyed-Hash Message Authentication Code (HMAC)*", which can be found at: [https://csrc.nist.gov/csrc/media/publications/fips/198/1/final/documents/fips-198-1_final.pdf](https://csrc.nist.gov/csrc/media/publications/fips/198/1/final/documents/fips-198-1_final.pdf)</span></span>
- <span data-ttu-id="07db2-149">**Bellek gereksinimi:** Uygulamanın, işlemler arasında durumu korumak için HMAC denetim bloğu yapısı sağlaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="07db2-149">**Memory Requirement:** The application must provide an HMAC control block structure for maintaining state between operations.</span></span> <span data-ttu-id="07db2-150">Sağlanan gerçek denetim bloğu, istenen temel karma işleme (ör. SHA1, MD5) bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="07db2-150">The actual control block supplied depends on the desired underlying hash operation (e.g. SHA1, MD5).</span></span>

## <a name="elliptic-curve"></a><span data-ttu-id="07db2-151">Eliptik Eğri</span><span class="sxs-lookup"><span data-stu-id="07db2-151">Elliptic Curve</span></span>

- <span data-ttu-id="07db2-152">**Standart:** NetX şifre eliptik eğri uygular.</span><span class="sxs-lookup"><span data-stu-id="07db2-152">**Standard:** NetX Crypto implements Elliptic Curve.</span></span> <span data-ttu-id="07db2-153">Desteklenen adlandırılmış eğriler şunlardır: (yalnızca ana alan):</span><span class="sxs-lookup"><span data-stu-id="07db2-153">The supported named curves are (prime field only):</span></span>
  - <span data-ttu-id="07db2-154">P-192</span><span class="sxs-lookup"><span data-stu-id="07db2-154">P-192</span></span>
  - <span data-ttu-id="07db2-155">P-224</span><span class="sxs-lookup"><span data-stu-id="07db2-155">P-224</span></span>
  - <span data-ttu-id="07db2-156">P-256</span><span class="sxs-lookup"><span data-stu-id="07db2-156">P-256</span></span>
  - <span data-ttu-id="07db2-157">P-384</span><span class="sxs-lookup"><span data-stu-id="07db2-157">P-384</span></span>
  - <span data-ttu-id="07db2-158">P-521</span><span class="sxs-lookup"><span data-stu-id="07db2-158">P-521</span></span>

   > [!TIP]
   > <span data-ttu-id="07db2-159">Sıkıştırılmamış biçim destekleniyor.</span><span class="sxs-lookup"><span data-stu-id="07db2-159">Uncompressed format is supported.</span></span> <span data-ttu-id="07db2-160">Bkz. Bölüm 2.3.3 ve 2.3.4 in SEC1-v1: [http://www.secg.org/sec1-v2.pdf](http://www.secg.org/sec1-v2.pdf)</span><span class="sxs-lookup"><span data-stu-id="07db2-160">See section 2.3.3 and 2.3.4 of SEC1-v1: [http://www.secg.org/sec1-v2.pdf](http://www.secg.org/sec1-v2.pdf)</span></span>

- <span data-ttu-id="07db2-161">**Bellek gereksinimi:** Seçim</span><span class="sxs-lookup"><span data-stu-id="07db2-161">**Memory Requirement:** None</span></span>

## <a name="ecdsa"></a><span data-ttu-id="07db2-162">ECDSA</span><span class="sxs-lookup"><span data-stu-id="07db2-162">ECDSA</span></span>

- <span data-ttu-id="07db2-163">**Standart:** NetX şifrelemesi, şu adreste bulunan FIPS PUB 186-4: "*dijital Imza standardı (DSS)*" UYARıNCA ECDSA 'yı uygular: [https://nvlpubs.nist.gov/nistpubs/fips/nist.fips.186-4.pdf](https://nvlpubs.nist.gov/nistpubs/fips/nist.fips.186-4.pdf)</span><span class="sxs-lookup"><span data-stu-id="07db2-163">**Standard:** NetX Crypto implements ECDSA according to FIPS PUB 186-4: "*Digital Signature Standard (DSS)*", which can be found at: [https://nvlpubs.nist.gov/nistpubs/fips/nist.fips.186-4.pdf](https://nvlpubs.nist.gov/nistpubs/fips/nist.fips.186-4.pdf)</span></span>
- <span data-ttu-id="07db2-164">**Bellek gereksinimi:** Uygulamanın, işlemler arasında durumu korumak için bir ECDSA denetim bloğu yapısı sağlaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="07db2-164">**Memory Requirement:** The application must provide an ECDSA control block structure for maintaining state between operations.</span></span>

## <a name="ecdh"></a><span data-ttu-id="07db2-165">ECDH</span><span class="sxs-lookup"><span data-stu-id="07db2-165">ECDH</span></span>

> [!IMPORTANT]
> <span data-ttu-id="07db2-166">Azure RTOS 6,0 ' de ECDH yordamları yalnızca ECDHE şifrelemesi için kullanılmalıdır, statik bir özel anahtarla ECDH, giriş noktası doğrulamasının güvenli olmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="07db2-166">In Azure RTOS 6.0, ECDH routines should only be used for ECDHE cryptography as ECDH with a static private key requires input point validation to be secure.</span></span>

- <span data-ttu-id="07db2-167">**Standart:** NetX şifrelemesi, şu adreste bulunabilir: "ayrık bir şifreleme şifrelemesi kullanarak Pair-Wise anahtar oluşturma şemaları için öneri" ile ECDH uygular. [https://nvlpubs.nist.gov/nistpubs/specialpublications/nist.sp.800-56ar2.pdf](https://nvlpubs.nist.gov/nistpubs/specialpublications/nist.sp.800-56ar2.pdf)</span><span class="sxs-lookup"><span data-stu-id="07db2-167">**Standard:** NetX Crypto implements ECDH according to FIPS PUB 800-56Ar2: "Recommendation for Pair-Wise Key Establishment Schemes Using Discrete Logarithm Cryptography", which can be found at: [https://nvlpubs.nist.gov/nistpubs/specialpublications/nist.sp.800-56ar2.pdf](https://nvlpubs.nist.gov/nistpubs/specialpublications/nist.sp.800-56ar2.pdf)</span></span>
- <span data-ttu-id="07db2-168">**Bellek gereksinimi:** Uygulamanın, işlemler arasında durumu korumak için bir ECDH denetim bloğu yapısı sağlaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="07db2-168">**Memory Requirement:** The application must provide an ECDH control block structure for maintaining state between operations.</span></span>

## <a name="drbg"></a><span data-ttu-id="07db2-169">DRBG</span><span class="sxs-lookup"><span data-stu-id="07db2-169">DRBG</span></span>

- <span data-ttu-id="07db2-170">**Standart:** NetX şifrelemesi, şu adreste bulunabilen, FIPS 'nin 800-90Ar1: "rastgele sayı oluşturma önerisi" belirleyici bir bit oluşturanlar kullanılarak ayarlanabilir. [https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-90Ar1.pdf](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-90Ar1.pdf)</span><span class="sxs-lookup"><span data-stu-id="07db2-170">**Standard:** NetX Crypto implements DRBG according to FIPS PUB 800-90Ar1: "Recommendation for Random Number Generation Using Deterministic Random Bit Generators", which can be found at: [https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-90Ar1.pdf](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-90Ar1.pdf)</span></span>
- <span data-ttu-id="07db2-171">**Bellek gereksinimi:** Uygulamanın, işlemler arasında durumu korumak için bir DRBG denetim bloğu yapısı sağlaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="07db2-171">**Memory Requirement:** The application must provide an DRBG control block structure for maintaining state between operations.</span></span>

## <a name="fips-compliant"></a><span data-ttu-id="07db2-172">FIPS-Compliant</span><span class="sxs-lookup"><span data-stu-id="07db2-172">FIPS-Compliant</span></span>

<span data-ttu-id="07db2-173">NetX şifre FIPS 140-2</span><span class="sxs-lookup"><span data-stu-id="07db2-173">NetX Crypto FIPS 140-2</span></span>