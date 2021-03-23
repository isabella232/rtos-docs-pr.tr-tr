---
title: Bölüm 1-Azure RTOS NetX güvenliğine giriş
description: Bu bölümde, Azure RTOS NetX güvenli 'ye giriş ve uygulamalarının ve avantajlarından ilgili bir açıklama yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 8f4c7a97564cd2f702f9887181b36297b42fa492
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825684"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-secure"></a>Bölüm 1-Azure RTOS NetX güvenliğine giriş

Azure RTOS NetX güvenli, tümleşik ThreadX tabanlı uygulamalar için özel olarak tasarlanan TLS/SSL dahil olmak üzere, şifreleme ağ güvenlik standartlarının yüksek performanslı bir gerçek zamanlı uygulamasıdır. Bu bölümde NetX güvenli 'ye giriş ve bunların uygulamalarının ve avantajlarının açıklaması yer almaktadır.

## <a name="netx-secure-unique-features"></a>NetX güvenli benzersiz özellikler

Diğer birçok TLS uygulamasının aksine, NetX Secure, çok çeşitli ekli donanım platformlarını desteklemek ve küçük mikro denetleyici uygulamalarından kolayca bulunan en güçlü katıştırılmış işlemciye kolayca ölçeklenebilmeniz için baştan sona tasarlanmıştır. Kod, ekli sistemlerin sınırlı kaynaklarıyla yazılır ve TLS üzerinden güvenli ağ iletişimleri sağlamak için gereken bellek parmak izini azaltmak için bir dizi yapılandırma seçeneği sunar.

## <a name="rfcs-supported-by-netx-secure"></a>NetX güvenli tarafından desteklenen RFC 'Ler 

NetX güvenli, TLS ile ilgili aşağıdaki protokolleri destekler. TLS ve şifrelemeye ilişkin çok sayıda RFC olduğundan liste kapsamlı değildir. NetX güvenli, küçük bellek ayak ve verimli yürütme ile gerçek zamanlı bir işletim sisteminin kısıtlamalarına göre tüm genel önerilere ve temel gereksinimlere uyar.

| RFC      | Açıklama                                                                                                 | Sayfa |
|----------|-------------------------------------------------------------------------------------------------------------|------|
| RFC 2104 | HMAC: Ileti kimlik doğrulaması için Keyed-Hashing                                                              | 33   |
| RFC 2246 | TLS protokol sürümü 1,0                                                                                | 19   |
| RFC 3268 | Aktarım Katmanı Güvenliği (TLS) için Gelişmiş Şifreleme Standardı (AES) Ciphersuites                          | 31   |
| RFC 3447 | Public-Key şifreleme standartları (PKCS) #1: RSA şifreleme özellikleri sürüm 2,1                    | 32   |
| RFC 4279 | TLS için önceden paylaşılan anahtar Ciphersuites                                                                         | 39   |
| RFC 4346 | Aktarım Katmanı Güvenliği (TLS) Protokolü sürüm 1,1                                                     | 19   |
| RFC 5246 | Aktarım Katmanı Güvenliği (TLS) Protokolü sürüm 1,2                                                     | 19   |
| RFC 5280 | X. 509.440 PKI sertifikaları (v3)                                                                                 | 41   |
| RFC 5746 | Aktarım Katmanı Güvenliği (TLS) yeniden anlaşması gösterge uzantısı                                           |      |
| RFC 5869 | HMAC tabanlı ayıklama ve genişletme anahtar türetme Işlevi (HKDF)                                                | 19   |
| RFC 6066<sup>1</sup> | Aktarım Katmanı Güvenliği (TLS) uzantıları: uzantı tanımları                                            | 19   |
| RFC 6234 | ABD güvenli karma algoritmaları (SHA ve SHA tabanlı HMAC ve HKDF)                                                 | 33   |
| RFC 8443 | Aktarım Katmanı Güvenliği (TLS) sürümleri 1,2 ve öncesi için Eliptik Eğri Şifreleme (ECC) şifre paketleri |      |
| RFC 8446 | Aktarım Katmanı Güvenliği (TLS) Protokolü sürüm 1,3                                                     | 19   |

1. Sürüm 6,0 itibariyle yalnızca RFC 6066 ' den Sunucu Adı Belirtme (SNı) uzantısı tam olarak desteklenmektedir.

## <a name="netx-secure-requirements"></a>NetX güvenli gereksinimleri

Düzgün çalışması için, NetX güvenli çalışma zamanı kitaplığı bir NetX IP örneğinin zaten oluşturulmuş olmasını gerektirir. Ayrıca, uygulamaya bağlı olarak bir veya daha fazla DER-Encoded X. 509.440 dijital sertifikası gerekir, bu, bir TLS örneğini belirlemek veya uzak bir ana bilgisayardan gelen sertifikaları doğrulamak için gereklidir. NetX güvenli paketinin daha fazla gereksinimi yoktur.

## <a name="netx-secure-constraints"></a>NetX güvenli kısıtlamalar

NetX güvenli protokolü, TLS 1,2 için RFC 5246 standartların ve TLS 1,3 için RFC 8446 'ın gereksinimlerini uygular ve isteğe bağlı (varsayılan olarak devre dışı) RFC 4346 (TLS 1,1) ve 2246 (TLS 1,0) ile geriye dönük uyumluluk sağlar. Ancak, aşağıdaki kısıtlamalar vardır:

- Yalnızca SHA-256 kullanan ciphersuites, TLS 1,2 ve TLS 1,3 için desteklenir. TLS 1,2 ' den önceki sürümlerde, TLS el sıkışması, TLS el sıkışma iletilerinin üzerinde oynanmadığını doğrulamak için sabit bir karma yordam kullanır. Sürüm 1,2 ' den başlayarak, el sıkışma ciphersuite ile birlikte sunulan karma yordamını kullanır. TLS, karma yordamın ne zaman kullanılacağını bilmez ve el sıkışma iletilerini önbelleğe almalıdır. Karma değeri SHA-256 olarak düzelterek NetX güvenli TLS, diğer TLS uygulamalarından daha küçük bir RAM parmak izi ile çalışabilir. Bu sınırlama, bellek kullanımının düzgün şekilde giderildiği bir sonraki sürümde kaldırılacaktır. * ÖNEMLI bir DIKKAT: Bu sınırlama **yalnızca** ciphersuite seçeneği için geçerlidir. X. 509.440 Sertifika imzaları aynı sınırlamaya tabi değildir ve desteklenen karma yordamlarından herhangi biri kullanılabilir.
- Gömülü cihazların doğası gereği, bazı uygulamaların 16KB 'LıK en fazla TLS kayıt boyutunu destekleyecek kaynaklara sahip olmayabilir. NetX Secure, yeterli kaynağa sahip cihazlarda 16KB kayıtlarını işleyebilir. TLS yeniden birleştirme arabelleği (bkz. *nx_secure_tls_session_packet_buffer_set* için API başvurusu **),** birlikte çalışabilirlik sorunları açısından 16kb 'den daha küçük bir boyuta ayarlanabilir. Yeniden birleştirme arabelleğinden daha büyük geçerli bir TLS kaydı alınmışsa, NetX güvenli TLS, TLS oturumunu bir hata ile iptal eder. Genel olarak, arabellek her zaman en az 18KB olarak ayarlanmalıdır (şifreleme dolgusu için 16KB TLS kayıt boyutu + 2KB) ve yalnızca denetimli ayarlarda daha küçük hale getirilir (örn. uzak ana bilgisayar, en fazla TLS kayıt boyutunu garanti eder).
  > [!NOTE]
  > Genel olarak, paket yeniden birleştirme arabelleği asla TLS en fazla kayıt boyutundan küçük olmamalıdır. Ancak, uzak ana bilgisayarın özellikleri iyi bilindiğinde (ör. tamamen kapalı bir sistemde), daha fazla RAM alanı yeniden kazanmak için boyut azaltılabilir.
- En az sertifika doğrulaması. NetX güvenliği, sertifikanın geçerli ve güvenilir bir sertifika yetkilisi tarafından imzalandığından emin olmak için bir sertifika üzerinde temel X. 509.952 zinciri doğrulaması yapar ve uygulamanın, uzak konağın Top-Level etki alanı adına göre karşılaştırılabilmesi için sertifika ortak adını sağlayabilir. Gerçek zamanlı bir saat varsa, sertifikanın sona erme tarihini doğrulamak için kullanılabilir (bkz. API nx_secure_tls_session_time_function_set). Bununla birlikte, sertifika uzantılarının ve diğer verilerin doğrulanması, uygulama uygulayıcısı 'nın sorumluluğundadır.
- Yazılım tabanlı şifreleme işlemciyi yoğun bir şekilde kullanır. NetX güvenli yazılım tabanlı şifreleme yordamları performans için iyileştirildi, ancak hedef işlemcinin gücüne bağlı olarak, bu performans çok uzun işlemlere neden olabilir. Donanım tabanlı şifreleme kullanılabilir olduğunda, NetX güvenli TLS 'nin en iyi performansı için kullanılmalıdır.
- TLS anlaşma kaydı parçalanması desteklenmiyor. Bazı TLS el ile kayıt iletileri çok büyükse, birden çok TLS kaydına ayrılabilir. NetX güvenli TLS Şu anda bunu bir hata olarak değerlendirir. Katıştırılmış sistemler için bellek gereksinimleri, büyük olasılıkla daha büyük bir el sıkışma kayıt iletisi de işlenemeyebilir, ancak sınırlandırma çok büyük sertifika zincirlerini kullanan belirli TLS konaklarıyla iletişim kurarken hatalara yol açabilir.
- Yerel depoda birden çok sertifika olduğunda, TLS sunucusu dinamik sertifika seçimini desteklemez. 
- X509 sertifikası KeyUsage gözlemlenmemiş. 
- ECDH tabanlı ciphersuites desteklenmez. Bunun yerine ECDHE kullanın.
