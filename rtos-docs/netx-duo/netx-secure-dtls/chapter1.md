---
title: Bölüm 1-Azure RTOS NetX güvenli DTLS 'ye giriş
description: Azure RTOS NetX güvenli DTLS, katıştırılmış ThreadX tabanlı uygulamalar için tasarlanan veri birimi Aktarım katmanı güvenlik protokolünün gerçek zamanlı bir uygulamasıdır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: a7fe51fd1e141c0c525a98986ca3058732b61843f8bd79bf24fc5ac986147501
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116797050"
---
# <a name="chapter-1-introduction-to-azure-rtos-netx-secure-dtls"></a>Bölüm 1: Azure RTOS NetX güvenli DTLS 'ye giriş

Azure RTOS NetX güvenli DTLS, katıştırılmış ThreadX tabanlı uygulamalar için özel olarak tasarlanan veri birimi Aktarım katmanı güvenlik protokolünün yüksek performanslı gerçek zamanlı uygulamasıdır. Bu bölüm NetX güvenli DTLS 'ye giriş ve uygulamalarının ve avantajlarından oluşan bir açıklama içerir.

## <a name="netx-secure-unique-features"></a>NetX güvenli benzersiz özellikler

Diğer TLS/DTLS uygulamalarından farklı olarak, NetX güvenli, çok çeşitli ekli donanım platformlarını destekleyecek ve küçük mikro denetleyicili uygulamalardan sunulan en güçlü katıştırılmış işlemciye kolayca ölçeklendirebilmeniz için baştan sona tasarlanmıştır. Kod, ekli sistemlerin sınırlı kaynaklarıyla yazılır ve TLS veya DTLS üzerinden güvenli ağ iletişimleri sağlamak için gereken bellek parmak izini azaltmak için bir dizi yapılandırma seçeneği sunar.

## <a name="rfcs-supported-by-netx-secure"></a>NetX güvenli tarafından desteklenen RFC 'Ler

NetX güvenli, TLS ve DTLS ile ilgili aşağıdaki protokolleri destekler. TLS/DTLS ve şifrelemeye ilişkin çok sayıda RFC olduğundan, liste kapsamlı değildir. NetX güvenli, küçük bellek ayak ve verimli yürütme ile gerçek zamanlı bir işletim sisteminin kısıtlamalarına göre tüm genel önerilere ve temel gereksinimlere uyar.


| RFC | Description |
| --- | ----------- |
| RFC 6347 | Veri birimi Aktarım Katmanı Güvenliği sürüm 1,2. |
| RFC 2246 | TLS protokol sürümü 1,0|
| RFC 4346 | Aktarım Katmanı Güvenliği (TLS) Protokolü sürüm 1,1 |
| RFC 5246 | Aktarım Katmanı Güvenliği (TLS) Protokolü sürüm 1,2 |
| RFC 5280 | X. 509.440 PKI sertifikaları (v3) |
| RFC 3268 | Aktarım Katmanı Güvenliği (TLS) için Gelişmiş Şifreleme Standardı (AES) Ciphersuites |
| RFC 3447 | Public-Key şifreleme standartları (PKCS) #1: RSA şifreleme özellikleri sürüm 2,1 |
| RFC 2104 | HMAC: Ileti kimlik doğrulaması için Keyed-Hashing |
| RFC 6234 | ABD güvenli karma algoritmaları (SHA ve SHA tabanlı HMAC ve HKDF) |
| RFC 4279 | TLS için önceden paylaşılan anahtar Ciphersuites |

## <a name="netx-secure-dtls-requirements"></a>NetX güvenli DTLS gereksinimleri

Düzgün çalışması için, NetX güvenli çalışma zamanı kitaplığı bir NetX IP örneğinin zaten oluşturulmuş olmasını gerektirir. Ayrıca, uygulamaya bağlı olarak, bir veya daha fazla DER-Encoded X. 509.952 dijital sertifikası, bir TLS/DTLS örneğini tanımlamak ya da uzak bir ana bilgisayardan gelen sertifikaları doğrulamak için gereklidir. NetX güvenli paketinin daha fazla gereksinimi yoktur.

## <a name="netx-secure-dtls-constraints"></a>NetX güvenli DTLS kısıtlamaları

NetX Secure DTLS Protokolü, DTLS 1,2 için RFC 6347 standardının gereksinimlerini uygular. Ancak, aşağıdaki kısıtlamalar vardır:

1. Gömülü cihazların doğası gereği, bazı uygulamaların 16KB 'lik en fazla TLS/DTLS kayıt boyutunu desteklemeye yönelik kaynakları bulunmayabilir. NetX Secure, yeterli kaynağa sahip cihazlarda 16KB kayıtlarını işleyebilir.
2. En az sertifika doğrulaması. NetX güvenliği, sertifikanın geçerli ve güvenilir bir sertifika yetkilisi tarafından imzalandığından emin olmak için bir sertifika üzerinde temel X. 509.952 zinciri doğrulaması yapar ve uygulamanın, uzak konağın Top-Level etki alanı adına göre karşılaştırılabilmesi için sertifika ortak adını sağlayabilir. Bununla birlikte, sertifika uzantılarının ve diğer verilerin doğrulanması, uygulama uygulayıcısı 'nın sorumluluğundadır.
3. Yazılım tabanlı şifreleme işlemciyi yoğun bir şekilde kullanır. NetX güvenli yazılım tabanlı şifreleme yordamları performans için iyileştirildi, ancak hedef işlemcinin gücüne bağlı olarak, bu performans çok uzun işlemlere neden olabilir. Donanım tabanlı şifreleme kullanılabilir olduğunda, NetX güvenli DTLS 'nin en iyi performansı için kullanılmalıdır.
