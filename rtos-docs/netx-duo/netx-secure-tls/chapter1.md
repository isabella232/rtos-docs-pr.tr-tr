---
title: Bölüm 1 - NetX Secure Azure RTOS giriş
description: Bu bölümde NetX Secure'Azure RTOS giriş ve uygulamalarının ve avantajlarının açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 1d6b0f23d7353626f340fe0ab93ee1e04800edaaa1f00da49afd83f84339df86
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116791610"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-secure"></a>Bölüm 1 - NetX Secure Azure RTOS giriş

Azure RTOS NetX Secure, ekli ThreadX tabanlı uygulamalar için özel olarak tasarlanmış TLS/SSL dahil olmak üzere şifreleme ağ güvenlik standartlarının yüksek performanslı gerçek zamanlı bir uygulamasıdır. Bu bölümde NetX Secure'e giriş ve uygulamalarının ve avantajlarının açıklaması yer almaktadır.

## <a name="netx-secure-unique-features"></a>NetX Secure Benzersiz Özellikleri

Diğer çoğu TLS uygulamasından farklı olarak NetX Secure, çok çeşitli tümleşik donanım platformlarını destekleyecek şekilde tasarlanmıştır ve küçük mikro denetleyici uygulamalardan kullanılabilen en güçlü tümleşik işlemcilere kadar kolayca ölçeklendirebilirsiniz. Kod, tümleşik sistemlerin sınırlı kaynaklarıyla yazılır ve TLS üzerinden güvenli ağ iletişimi sağlamak için gereken bellek ayak izini azaltmak için bir dizi yapılandırma seçeneği sunar.

## <a name="rfcs-supported-by-netx-secure"></a>NetX Secure Tarafından Desteklenen RFC'ler 

NetX Secure, TLS ile ilgili aşağıdaki protokolleri destekler. TLS ve şifrelemeyle ilgili çok sayıda RFC olduğu için liste mutlaka kapsamlı değildir. NetX Secure, küçük bellek ayak izine ve verimli yürütmeye sahip gerçek zamanlı bir işletim sisteminin kısıtlamaları dahilinde tüm genel önerileri ve temel gereksinimleri izler.

| RFC      | Description                                                                                                 | Sayfa |
|----------|-------------------------------------------------------------------------------------------------------------|------|
| RFC 2104 | HMAC: Keyed-Hashing Kimlik Doğrulaması için yapılandırma                                                              | 33   |
| RFC 2246 | TLS Protokolü Sürüm 1.0                                                                                | 19   |
| RFC 3268 | Gelişmiş Şifreleme Standardı Katmanı Güvenliği (TLS) için Gelişmiş Şifreleme Standardı (AES) Şifrelemeleri                          | 31   |
| RFC 3447 | Public-Key Şifreleme Standartları (PKCS) #1: RSA Şifreleme Belirtimleri Sürüm 2.1                    | 32   |
| RFC 4279 | TLS için Önceden Paylaşılan Anahtar Şifrelemeleri                                                                         | 39   |
| RFC 4346 | Aktarım Katmanı Güvenliği (TLS) Protokolü Sürüm 1.1                                                     | 19   |
| RFC 5246 | Aktarım Katmanı Güvenliği (TLS) Protokolü Sürüm 1.2                                                     | 19   |
| RFC 5280 | X.509 PKI Sertifikaları (v3)                                                                                 | 41   |
| RFC 5746 | Aktarım Katmanı Güvenliği (TLS) Yeniden Yapılanma Göstergesi Uzantısı                                           |      |
| RFC 5869 | HMAC Tabanlı Ayıklama ve Genişletme Anahtarı Türetme İşlevi (HKDF)                                                | 19   |
| RFC 6066<sup>1</sup> | Aktarım Katmanı Güvenliği (TLS) Uzantıları: Uzantı Tanımları                                            | 19   |
| RFC 6234 | ABD Güvenli Karma Algoritmaları (SHA ve SHA tabanlı HMAC ve HKDF)                                                 | 33   |
| RFC 8443 | Aktarım Katmanı Güvenliği (TLS) 1.2 ve Önceki Sürümler için Eliptik Eğri Şifrelemesi (ECC) Şifreleme Paketleri |      |
| RFC 8446 | Aktarım Katmanı Güvenliği (TLS) Protokolü Sürüm 1.3                                                     | 19   |

1. Sürüm 6.0'dan itibaren yalnızca RFC 6066'dan Sunucu Adı Belirtme (SNI) uzantısı tam olarak de destekleni.

## <a name="netx-secure-requirements"></a>NetX Güvenli Gereksinimleri

NetX Secure çalışma zamanı kitaplığının düzgün çalışması için bir NetX IP örneğinin önceden oluşturulmuş olması gerekir. Ayrıca, uygulamaya bağlı olarak bir TLS örneğini tanımlamak veya uzak bir konaktan gelen sertifikaları doğrulamak için bir veya daha fazla DER kodlanmış X.509 Dijital Sertifika gerekir. NetX Secure paketinin başka bir gereksinimleri yoktur.

## <a name="netx-secure-constraints"></a>NetX Güvenli Kısıtlamaları

NetX Secure protokolü, TLS 1.2 ve RFC 8446 için RFC 5246 Standartlarının gereksinimlerini uygulamanın yanı sıra Isteğe bağlı (varsayılan olarak devre dışı) RFC 4346 (TLS 1.1) ve 2246 (TLS 1.0) ile geriye dönük uyumluluk sağlar. Ancak, aşağıdaki kısıtlamalar vardır:

- YALNıZCA SHA-256 kullanan şifreler TLS 1.2 ve TLS 1.3 için de destek sağlar. TLS 1.2'den önceki sürümlerde TLS el sıkışması, TLS el sıkışma iletilerinin değiştirilmediğini doğrulamak için sabit bir karma yordamı kullanır. Sürüm 1.2'den başlayarak, el sıkışması şifreleme ile sağlanan karma yordamını kullanır. TLS hangi karma yordamının kullan olacağını önceden bilmiyor ve el sıkışma iletilerini önbelleğe alıyor olması gerekir. NetX Secure TLS, karma değeri SHA-256'ya düzelterek diğer TLS uygulamalarına göre daha küçük bir RAM ayak iziyle işlev görüyor. Bellek kullanımı düzgün bir şekilde ele alındıktan sonra bu sınırlama gelecekteki bir sürümde kaldırılacaktır. *ÖNEMLİ NOT: Bu sınırlama **yalnızca** şifre seçimi için geçerlidir. X.509 sertifika imzaları aynı sınırlamaya tabi değildir ve desteklenen karma yordamlardan herhangi biri kullanılabilir.
- Katıştırılmış cihazların yapısı nedeniyle, bazı uygulamalar maksimum 16 KB TLS kayıt boyutunu destekleyecek kaynaklara sahip olabilir. NetX Secure, yeterli kaynaklara sahip cihazlarda 16 KB'lık kayıtları işebilir. TLS yeniden derleme arabelleği (bkz. *nx_secure_tls_session_packet_buffer_set* API **başvurusu)** birlikte çalışabilirlik sorunları riskiyle 16 KB'den küçük bir boyuta ayarlanmış olabilir. Yeniden değerlendirme arabelleğinden daha büyük geçerli bir TLS kaydı alındı ise NetX Secure TLS, TLS oturumunu bir hatayla iptal eder. Genel olarak, arabelleğin her zaman en az 18 KB (şifreleme doldurma için 16 KB TLS kayıt boyutu + 2 KB) olarak ayarlanmış olması ve yalnızca denetimli ayarlarda daha küçük olması gerekir (örneğin uzak konak maksimum TLS kayıt boyutunu garantiler).
  > [!NOTE]
  > Genel olarak, paket yeniden değerlendirme arabelleği hiçbir zaman TLS maksimum kayıt boyutundan küçük olmayacaktır. Ancak uzak ana bilgisayarın özellikleri iyi biliniyorsa (örneğin, tamamen kapalı bir sistemde) ram alanı kazanmak için boyut azaltabilirsiniz.
- En düşük sertifika doğrulaması. NetX Secure, sertifikanın güvenilir bir Sertifika Yetkilisi tarafından geçerli ve imzalanmış olduğundan emin olmak için bir sertifika üzerinde temel X.509 zincir doğrulaması gerçekleştirecek ve uzak ana bilgisayarın Top-Level Etki Alanı Adı ile karşılaştıracak uygulama için sertifika Ortak Adı'na sahip olabilir. Gerçek zamanlı bir saat varsa, sertifika sona erme tarihini doğrulamak için kullanılabilir (bkz. API nx_secure_tls_session_time_function_set). Ancak, sertifika uzantılarının ve diğer verilerin doğrulanması uygulama uygulayıcının sorumluluğundadır.
- Yazılım tabanlı şifreleme yoğun işlemci içerir. NetX Secure yazılım tabanlı şifreleme yordamları performans için iyileştirilmiştir, ancak hedef işlemcinin gücüne bağlı olarak bu performans çok uzun işlemlere neden olabilir. Donanım tabanlı şifreleme kullanılabilir olduğunda NetX Secure TLS'nin en iyi performansı için kullanılmalıdır.
- TLS El Sıkışma Kaydı parçalanması desteklenmiyor. Bazı TLS el sıkışma kaydı iletileri çok büyükse, bunlar birden çok TLS kaydı arasında bölünüyor olabilir – NetX Secure TLS şu anda bunu bir hata olarak ele alır. Katıştırılmış sistemler için bellek gereksinimleri, büyük el sıkışma kayıt iletisi büyük olasılıkla yine de iş edilemez, ancak sınırlama aşırı büyük sertifika zincirleri kullanan belirli TLS konakları ile iletişim kurarken hatalara neden olabilir.
- Yerel depoda birden çok sertifika olduğunda TLS sunucusu dinamik sertifika seçimini desteklemez. 
- X509 Sertifika AnahtarıKusage gözlemlenmez. 
- ECDH tabanlı şifreler desteklenmiyor. Bunun yerine ECDHE kullanın.
