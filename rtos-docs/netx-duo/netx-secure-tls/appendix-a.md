---
title: Ek A-Azure RTOS NetX güvenli dönüş/hata kodları
description: NetX güvenli dönüş/hata kodları
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: c1b9c17bb1cea50cc45b15622e82112c144e21ad
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826956"
---
# <a name="appendix-a---azure-rtos-netx-secure-returnerror-codes"></a>Ek A-Azure RTOS NetX güvenli dönüş/hata kodları

## <a name="netx-secure-tls-return-codes"></a>NetX güvenli TLS dönüş kodları

Aşağıdaki tablo 1, Azure RTOS NetX güvenli TLS Hizmetleri tarafından döndürülebilecek olası hata kodlarını listeler. Hizmetlerin TCP/IP hata kodları da döndürebileceğini unutmayın – TLS değerleri 0x101 ' den başlar ve TCP/IP değerleri 0x100 ' den fazla olabilir. X. 509.952 dönüş değerleri 0x181 ' den başlar. TCP/IP dönüş değerleri hakkında bilgi edinmek için NetX TCP/IP belgelerine başvurun ve X. 509.440 değerleri için aşağıya bakın.

| Hata adı                                             | Değer  | Açıklama                                                                                                                                                    |
| ---------------------------------------------------------- | ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| NX_SECURE_TLS_SUCCESS                              | -  | İşlev başarıyla döndürüldü. (NX_SUCCESS ile aynı).                                                                                                         |
| NX_SECURE_TLS_SESSION_UNINITIALIZED               | 0x101  | TLS ana döngüsü başlatılmamış yuva ile çağrıldı.                                                                                                               |
| NX_SECURE_TLS_UNRECOGNIZED_MESSAGE_TYPE          | 0x102  | TLS kayıt katmanı tanınmayan bir ileti türü aldı.                                                                                                       |
| NX_SECURE_TLS_INVALID_STATE                       | 0x103  | İç hata-durum tanınmıyor.                                                                                                                        |
| NX_SECURE_TLS_INVALID_PACKET                      | 0x104  | İç hata-alınan paket TLS verisi içermiyordu.                                                                                                    |
| NX_SECURE_TLS_UNKNOWN_CIPHERSUITE                 | 0x105  | Seçilen ciphersuite desteklenmiyor-sunucu için iç hata, istemci için uzak konağın bozuk bir ciphersuite (hata veya saldırı) gönderdiği anlamına gelir.            |
| NX_SECURE_TLS_UNSUPPORTED_CIPHER                  | 0x106  | Şifreleme veya şifre çözme işlemleri yaparken, seçilen şifre devre dışı veya kullanılamaz.                                                                           |
| NX_SECURE_TLS_HANDSHAKE_FAILURE                   | 0x107  | El sıkışma sırasında ileti işleme bir şey başarısız oldu.                                                                                              |
| NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE           | 0x108  | Gelen bir kayıt, oluşturulduğumuz bir MAC 'e sahipti.                                                                                         |
| NX_SECURE_TLS_TCP_SEND_FAILED                    | 0x109  | Bir kaydın giden TCP gönderimi bir nedenle başarısız oldu.                                                                                                     |
| NX_SECURE_TLS_INCORRECT_MESSAGE_LENGTH            | 0x10A  | Gelen bir ileti yanlış uzunluğa sahipti (genellikle üst bilgide bir uzunluk, sertifika iletilerinde olduğu gibi)                               |
| NX_SECURE_TLS_BAD_CIPHERSPEC                      | 0x10B  | Gelen bir Changecyaspec iletisi hatalı.                                                                                                           |
| NX_SECURE_TLS_INVALID_SERVER_CERT                | 0x10C  | Gelen sunucu sertifikası doğru bir şekilde ayrıştırılamadı.                                                                                                       |
| NX_SECURE_TLS_UNSUPPORTED_PUBLIC_CIPHER          | 0x10D  | Sunucu tarafından sağlanmış bir sertifika, desteklemediğimiz bir ortak anahtar işlemi belirtti.                                                                        |
| NX_SECURE_TLS_NO_SUPPORTED_CIPHERS               | 0x10E  | Desteklenen cipherpaketlerine sahip olmayan bir ClientHello alındı.                                                                                                        |
| NX_SECURE_TLS_UNKNOWN_TLS_VERSION                | 0x10F  | Gelen bir kayıt, tanınmayan bir TLS sürümüne sahipti.                                                                                                   |
| NX_SECURE_TLS_UNSUPPORTED_TLS_VERSION            | 0x110  | Gelen bir kayıt geçerli bir TLS sürümüne sahipti, ancak bu desteklenmez.                                                                                     |
| NX_SECURE_TLS_ALLOCATE_PACKET_FAILED             | 0x111 | TLS iletisi için bir iç paket ayırması başarısız oldu.                                                                                                        |
| NX_SECURE_TLS_INVALID_CERTIFICATE                 | 0x112  | X509 sertifikası doğru bir şekilde ayrıştırılamadı.                                                                                                                  |
| NX_SECURE_TLS_NO_CLOSE_RESPONSE                  | 0x113 | Bir TLS oturumu kapatma sırasında uzak ana bilgisayardan bir CloseNotify almadı.                                                                               |
| NX_SECURE_TLS_ALERT_RECEIVED                      | 0x114 | Uzak ana bilgisayar bir hata belirten ve bağlantıyı kapatan bir uyarı gönderdi.                                                                                |
| NX_SECURE_TLS_FINISHED_HASH_FAILURE              | 0x115  | Alınan son ileti karması, yerel olarak oluşturulan karma sıkışma bozulması ile eşleşmiyor.                                                              |
| NX_SECURE_TLS_UNKNOWN_CERT_SIG_ALGORITHM         | 0x116 | Doğrulama sırasında bir sertifika, desteklenmeyen bir imza algoritmasına sahipti.                                                                                     |
| NX_SECURE_TLS_CERTIFICATE_SIG_CHECK_FAILED       | 0x117  | Sertifika imzası doğrulama denetimi başarısız oldu-sertifika verileri imzayla eşleşmedi.                                                                 |
| NX_SECURE_TLS_BAD_COMPRESSION_METHOD              | 0x118  | Desteklenmeyen bir sıkıştırma yöntemiyle bir merhaba iletisi alındı.                                                                                              |
| NX_SECURE_TLS_CERTIFICATE_NOT_FOUND               | 0x119  | Sertifika listesindeki bir işlemde, eşleşen bir sertifika bulunamadı.                                                                                     |
| NX_SECURE_TLS_INVALID_SELF_SIGNED_CERT           | 0x11A  | Uzak ana bilgisayar otomatik olarak imzalanan bir sertifika gönderdi ve NX_SECURE_ALLOW_SELF_SIGNED_CERTIFICATES tanımlı değil.                                              |
| NX_SECURE_TLS_ISSUER_CERTIFICATE_NOT_FOUND       | 0x11B  | Yerel güvenilen depoda olmayan bir veren ile uzak bir sertifika alındı.                                                                              |
| NX_SECURE_TLS_OUT_OF_ORDER_MESSAGE               | 0x11C  | Bir DTLS iletisi yanlış sırada alındı-bırakılan bir veri birimi büyük olasılıkla olabilir.                                                                    |
| NX_SECURE_TLS_INVALID_REMOTE_HOST                 | 0x11D  | Tanımadığınız bir uzak ana bilgisayardan paket alındı.                                                                                            |
| NX_SECURE_TLS_INVALID_EPOCH                        | 0x11E  | DTLS iletisi alındı ve bir DTLS oturumuyla eşleşti, ancak süresi yanlış ve göz ardı edilmelidir.                                                   |
| NX_SECURE_TLS_REPEAT_MESSAGE_RECEIVED             | 0x11F  | Zaten görtiğimiz bir sıra numarası ile bir DTLS iletisi alındı, yok sayın.                                                                           |
| NX_SECURE_TLS_NEED_DTLS_SESSION                   | 0x120  | DTLS API 'sinde DTLS için başlatılmamış bir TLS oturumu kullanıldı.                                                                                       |
| NX_SECURE_TLS_NEED_TLS_SESSION                    | 0x121  | TLS değil, DTLS için başlatılan TLS API 'sinde bir TLS oturumu kullanıldı.                                                                                |
| NX_SECURE_TLS_SEND_ADDRESS_MISMATCH               | 0x122  | Çağıran, oturumla eşleşmeyen bir IP adresi veya bağlantı noktasıyla bir DTLS oturumu üzerinden veri gönderilmeye çalıştı.                                                  |
| NX_SECURE_TLS_NO_FREE_DTLS_SESSIONS              | 0x123  | Yeni bir bağlantı önbellekten DTLS oturumu almaya çalıştı, ancak hiç boş yoktu.                                                                        |
| NX_SECURE_DTLS_SESSION_NOT_FOUND                  | 0x124  | Çağıran bir DTLS oturumu aradı, ancak verilen IP adresi ve bağlantı noktası önbellekteki girdilerle eşleşmedi.                                             |
| NX_SECURE_TLS_NO_MORE_PSK_SPACE                  | 0x125  | Çağıran bir TLS oturumuna PSK eklemeyi denedi ancak belirtilen oturumda daha fazla alan yoktu.                                                          |
| NX_SECURE_TLS_NO_MATCHING_PSK                     | 0x126  | Uzak ana bilgisayar, yerel depomızdan hiçbiriyle eşleşmeyen bir PSK kimlik ipucu sağladı.                                                                         |
| NX_SECURE_TLS_CLOSE_NOTIFY_RECEIVED               | 0x127  | Bir TLS oturumu, oturum tamamlandığını belirten uzak ana bilgisayardan bir CloseNotify uyarısı aldı.                                                           |
| NX_SECURE_TLS_NO_AVAILABLE_SESSIONS               | 0x128  | Bir bağlantıyı işlemek için TLS nesnesinde bir TLS oturumu yok.                                                                                         |
| NX_SECURE_TLS_NO_CERT_SPACE_ALLOCATED            | 0x129  | Gelen uzak sertifikalar için hiçbir sertifika alanı ayrılmadı.                                                                                          |
| NX_SECURE_TLS_PADDING_CHECK_FAILED                | 0x12A  | Gelen iletide şifreleme doldurma doğru değildi.                                                                                                    |
| NX_SECURE_TLS_UNSUPPORTED_CERT_SIGN_TYPE         | 0x12B  | Bir CertificateVerifyRequest işlenirken, uzak sunucu tarafından desteklenen bir sertifika türü sağlanmadı.                                                    |
| NX_SECURE_TLS_UNSUPPORTED_CERT_SIGN_ALG          | 0x12C  | Bir CertificateVerifyRequest işlenirken, uzak sunucu tarafından desteklenen imza algoritması sağlanmadı.                                                 |
| NX_SECURE_TLS_INSUFFICIENT_CERT_SPACE             | 0x12D  | Bir sertifika için ayrılan yeterli sertifika arabelleği alanı yok.                                                                                              |
| NX_SECURE_TLS_PROTOCOL_VERSION_CHANGED            | 0x12E  | Gelen bir TLS kaydındaki protokol sürümü, belirlenen oturumun sürümüyle eşleşmedi.                                                          |
| NX_SECURE_TLS_NO_RENEGOTIATION_ERROR              | 0x12F  | Bir merhaba Istek iletisi alındı, ancak yeniden anlaşıyoruz.                                                                                           |
| NX_SECURE_TLS_UNSUPPORTED_FEATURE                  | 0x130  | Bir TLS oturumu veya el sıkışma sırasında devre dışı bırakılmış bir özelliğe rastlandı.                                                                                |
| NX_SECURE_TLS_CERTIFICATE_VERIFY_FAILURE          | 0x131  | Uzak bir Istemciden bir CertificateVerify iletisi, Istemci sertifikasını doğrulayamadı.                                                                     |
| NX_SECURE_TLS_EMPTY_REMOTE_CERTIFICATE_RECEIVED  | 0x132  | Uzak ana bilgisayar boş bir sertifika iletisi gönderdi.                                                                                                            |
| NX_SECURE_TLS_RENEGOTIATION_EXTENSION_ERROR       | 0x133  | Güvenli bir Renegotation gösterge uzantısı işlenirken veya gönderilirken hata oluştu.                                                                      |
| NX_SECURE_TLS_RENEGOTIATION_SESSION_INACTIVE      | 0x134  | Oturum yeniden anlaşması, etkin olmayan bir TLS oturumu ile yapılmaya çalışılıyor.                                                                                 |
| NX_SECURE_TLS_PACKET_BUFFER_TOO_SMALL            | 0x135  | TLS, atanan paket arabelleği için çok büyük bir kayıt aldı. Kayıt işlenemedi.                                                    |
| NX_SECURE_TLS_EXTENSION_NOT_FOUND                 | 0x136  | TLS anlaşması sırasında uzak konaktan belirtilen bir uzantı alınmadı.                                                                          |
| NX_SECURE_TLS_SNI_EXTENSION_INVALID               | 0x137  | TLS geçersiz bir Sunucu Adı Belirtme uzantısı aldı.                                                                                                      |
| NX_SECURE_TLS_CERT_ID_INVALID                     | 0x138  | Uygulama, geçersiz bir sertifika KIMLIĞI değeri (0) olan bir sunucu sertifikası eklemeye çalıştı.                                                                 |
| NX_SECURE_TLS_CERT_ID_DUPLICATE                   | 0x139  | Uygulama, yerel depoda zaten bir sertifika KIMLIĞINE sahip bir sunucu sertifikası eklemeye çalıştı.                                                        |
| NX_SECURE_TLS_RENEGOTIATION_FAILURE                | 0x13A  | Uzak ana bilgisayar güvenli yeniden anlaşma bildirimi uzantısını veya SCSV sözde ciphersuite 'i sağlamadı, böylece güvenli yeniden anlaşma gerçekleştirilemiyor.      |
| NX_SECURE_TLS_MISSING_CRYPTO_ROUTINE              | 0x13B  | Şifreleme işlemi gerçekleştirmeye çalışırken, ciphersuite tablosundaki girdilerden biri (veya işlev işaretçilerinden biri) yanlış olarak NULL olarak ayarlanmıştır. |
| NX_SECURE_TLS_EMPTY_EC_GROUP                      | 0x13C  | ECC ciphersuite ayarlanmış ancak desteklenen EC grubu yok.                                                                                                             |
| NX_SECURE_TLS_EMPTY_EC_POINT_FORMAT              | 0x13D  | ECC ciphersuite ayarlanmış ancak desteklenen EC noktası biçimi yok.                                                                                                      |
| NX_SECURE_TLS_BAD_SERVERHELLO_KEYSHARE            | 0x13E  | Uzak bir sunucudan bir TLS 1,3 KeyShare uzantısında, sunucu beklemediğimiz bir şey sağladı.                                                         |
| NX_SECURE_TLS_INSUFFICIENT_METADATA_SPACE         | 0x13F  | TLS şifreleme yordamları için uygulama tarafından sağlanan "metadata" çok küçük.                                                                             |
| NX_SECURE_TLS_POST_HANDSHAKE_RECEIVED             | 0x140  | Bir hata değil, uygulama verileri alınana kadar işleme devam etmek için bir gösterge.                                                                    |
| NX_SECURE_TLS_BAD_CLIENTHELLO_KEYSHARE            | 0x141  | Uzak bir istemciden bir TLS 1,3 KeyShare uzantısında, istemci beklemediğimiz bir şey sağladı.                                                         |
| NX_SECURE_TLS_1_3_UNKNOWN_CIPHERSUITE            | 0x142  | TLS 1,3 kullanılırken bilinmeyen ciphersuite alındı.                                                                                                              |
| NX_SECURE_TLS_INVALID_SESSION_TICKET              | 0x143  | Yanlış veya geçersiz parametrelere sahip bir Newsessionbilet iletisi alındı.                                                                                      |
| NX_SECURE_TLS_MISSING_EXTENSION                    | 0x144  | İletide belirli bir uzantı kaçırıldı.                                                                                                                  |
| NX_SECURE_TLS_CERTIFICATE_REQUIRED                 | 0x145  | Sunucu boş bir sertifika aldı.                                                                                                                         |
| NX_SECURE_TLS_UNEXPECTED_CLIENTHELLO               | 0x146  | TLS 1,3 sunucusu yeniden anlaşma için ClientHello alır.                                                                                                         |
| NX_SECURE_TLS_INAPPROPRIATE_FALLBACK               | 0x147  | Uzak Istemci uygunsuz bir TLS sürümü düşürme girişiminde bulunuldu.                                                                                               |
| NX_SECURE_TLS_BAD_CLIENTHELLO_PSK_EXTENSION      | 0x148  | Uzak bir istemciden TLS 1,3 PSK uzantısında, istemci beklemediğimiz bir şey sağladı.                                                              |
| NX_SECURE_TLS_PSK_BINDER_MISMATCH                 | 0x149  | Uzak bir istemciden bir TLS 1,3 PSK uzantısında, istemci hatalı bir PSK Ciltçi değeri sağladı.                                                                  |
| NX_SECURE_TLS_CRYPTO_KEYS_TOO_LARGE              | 0x14A  | TLS oturum anahtarları oluşturma girişiminde, anahtar arabelleği çok küçük NX_SECURE_TLS_KEY_MATERIAL_SIZE artmıştı.                                     |
| NX_SECURE_TLS_UNSUPPORTED_ECC_CURVE               | 0x14B  | Uzak ana bilgisayar bir sertifika sağladı veya desteklenmeyen bir ECC eğrisi ile ciphersuite seçti.                                                         |
| NX_SECURE_TLS_UNSUPPORTED_ECC_FORMAT              | 0x14C  | Desteklenmeyen bir eğri türü veya ECC biçimi ile karşılaşıldı.                                                                                                 |
| NX_SECURE_TLS_UNSUPPORTED_SIGNATURE_ALGORITHM     | 0x14D  | Desteklenmeyen bir imza algoritması ile karşılaşıldı (anahtar değişim veya sertifika olmayan diğer durumlarda kullanılır).                                                |
| NX_SECURE_TLS_SIGNATURE_VERIFICATION_ERROR        | 0x14E  | İmza doğrulama denetimi başarısız oldu (anahtar değişim veya diğer sertifika olmayan durumlarda kullanılır).                                                                    |
| NX_SECURE_TLS_UNEXPECTED_MESSAGE                   | 0x14F  | TLS uzak ana bilgisayardan beklenmeyen bir ileti aldı.                                                                                                      |
| NX_SECURE_TLS_AEAD_DECRYPT_FAIL                   | 0x150  | Gelen bir kayıt, AEAD şifrelemeleri ile bütünlük denetimini geçirmedi.                                                                                            |
| NX_SECURE_TLS_RECORD_OVERFLOW                      | 0x151  | Uzunluğu çok uzun olan bir Tlscbir metin kaydı alındı.                                                                                                   |
| NX_SECURE_TLS_HANDSHAKE_FRAGMENT_RECEIVED         | 0x152  | Parçalanmış bir el sıkışma iletisi alındı-durum makinesinin daha yüksek bir düzeyinde uygun eylemi gerçekleştirin.                                                     |

| Hata adı                                             | Değer  | Açıklama                                                                                                                                                    |
| ---------------------------------------------------------- | ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| NX_SECURE_TLS_SUCCESS                               | -   | İşlev başarıyla döndürüldü. (NX_SUCCESS ile aynı).                                                                                                         |
| NX_SECURE_TLS_SESSION_UNINITIALIZED                | 0x101  | TLS ana döngüsü başlatılmamış yuva ile çağrıldı.                                                                                                               |
| NX_SECURE_TLS_UNRECOGNIZED_MESSAGE_TYPE           | 0x102  | TLS kayıt katmanı tanınmayan bir ileti türü aldı.                                                                                                       |
| NX_SECURE_TLS_INVALID_STATE                        | 0x103  | İç hata-durum tanınmıyor.                                                                                                                        |
| NX_SECURE_TLS_INVALID_PACKET                       | 0x104  | İç hata-alınan paket TLS verisi içermiyordu.                                                                                                    |
| NX_SECURE_TLS_UNKNOWN_CIPHERSUITE                  | 0x105  | Seçilen ciphersuite desteklenmiyor-sunucu için iç hata, istemci için uzak konağın bozuk bir ciphersuite (hata veya saldırı) gönderdiği anlamına gelir.            |
| NX_SECURE_TLS_UNSUPPORTED_CIPHER                   | 0x106  | Şifreleme veya şifre çözme işlemleri yaparken, seçilen şifre devre dışı veya kullanılamaz.                                                                           |
| NX_SECURE_TLS_HANDSHAKE_FAILURE                    | 0x107  | El sıkışma sırasında ileti işleme bir şey başarısız oldu.                                                                                              |
| NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE            | 0x108  | Gelen bir kayıt, oluşturulduğumuz bir MAC 'e sahipti.                                                                                         |
| NX_SECURE_TLS_TCP_SEND_FAILED                     | 0x109  | Bir kaydın giden TCP gönderimi bir nedenle başarısız oldu.                                                                                                     |
| NX_SECURE_TLS_INCORRECT_MESSAGE_LENGTH            | 0x10A  | Gelen bir ileti yanlış uzunluğa sahipti (genellikle üst bilgide bir uzunluk, sertifika iletilerinde olduğu gibi)                                |
| NX_SECURE_TLS_BAD_CIPHERSPEC                       | 0x10B  | Gelen bir Changecyaspec iletisi hatalı.                                                                                                           |
| NX_SECURE_TLS_INVALID_SERVER_CERT                 | 0x10C  | Gelen sunucu sertifikası doğru bir şekilde ayrıştırılamadı.                                                                                                       |
| NX_SECURE_TLS_UNSUPPORTED_PUBLIC_CIPHER           | 0x10D  | Sunucu tarafından sağlanmış bir sertifika, desteklemediğimiz bir ortak anahtar işlemi belirtti.                                                                        |
| NX_SECURE_TLS_NO_SUPPORTED_CIPHERS                | 0x10E  | Desteklenen cipherpaketlerine sahip olmayan bir ClientHello alındı.                                                                                                        |
| NX_SECURE_TLS_UNKNOWN_TLS_VERSION                 | 0x10F  | Gelen bir kayıt, tanınmayan bir TLS sürümüne sahipti.                                                                                                   |
| NX_SECURE_TLS_UNSUPPORTED_TLS_VERSION             | 0x110  | Gelen bir kayıt geçerli bir TLS sürümüne sahipti, ancak bu desteklenmez.                                                                                     |
| NX_SECURE_TLS_ALLOCATE_PACKET_FAILED              | 0x111  | TLS iletisi için bir iç paket ayırması başarısız oldu.                                                                                                        |
| NX_SECURE_TLS_INVALID_CERTIFICATE                  | 0x112  | X509 sertifikası doğru bir şekilde ayrıştırılamadı.                                                                                                                  |
| NX_SECURE_TLS_NO_CLOSE_RESPONSE                   | 0x113  | Bir TLS oturumu kapatma sırasında uzak ana bilgisayardan bir CloseNotify almadı.                                                                               |
| NX_SECURE_TLS_ALERT_RECEIVED                       | 0x114  | Uzak ana bilgisayar bir hata belirten ve bağlantıyı kapatan bir uyarı gönderdi.                                                                                |
| NX_SECURE_TLS_FINISHED_HASH_FAILURE               | 0x115  | Alınan son ileti karması, yerel olarak oluşturulan karma sıkışma bozulması ile eşleşmiyor.                                                              |
| NX_SECURE_TLS_UNKNOWN_CERT_SIG_ALGORITHM         | 0x116  | Doğrulama sırasında bir sertifika, desteklenmeyen bir imza algoritmasına sahipti.                                                                                     |
| NX_SECURE_TLS_CERTIFICATE_SIG_CHECK_FAILED       | 0x117  | Sertifika imzası doğrulama denetimi başarısız oldu-sertifika verileri imzayla eşleşmedi.                                                                 |
| NX_SECURE_TLS_BAD_COMPRESSION_METHOD              | 0x118  | Desteklenmeyen bir sıkıştırma yöntemiyle bir merhaba iletisi alındı.                                                                                              |
| NX_SECURE_TLS_CERTIFICATE_NOT_FOUND               | 0x119  | Sertifika listesindeki bir işlemde, eşleşen bir sertifika bulunamadı.                                                                                     |
| NX_SECURE_TLS_INVALID_SELF_SIGNED_CERT           | 0x11A  | Uzak ana bilgisayar otomatik olarak imzalanan bir sertifika gönderdi ve NX_SECURE_ALLOW_SELF_SIGNED_CERTIFICATES tanımlı değil.                                              |
| NX_SECURE_TLS_ISSUER_CERTIFICATE_NOT_FOUND       | 0x11B  | Yerel güvenilen depoda olmayan bir veren ile uzak bir sertifika alındı.                                                                              |
| NX_SECURE_TLS_OUT_OF_ORDER_MESSAGE               | 0x11C  | Bir DTLS iletisi yanlış sırada alındı-bırakılan bir veri birimi büyük olasılıkla olabilir.                                                                    |
| NX_SECURE_TLS_INVALID_REMOTE_HOST                 | 0x11D  | Tanımadığınız bir uzak ana bilgisayardan paket alındı.                                                                                            |
| NX_SECURE_TLS_INVALID_EPOCH                        | 0x11E  | DTLS iletisi alındı ve bir DTLS oturumuyla eşleşti, ancak süresi yanlış ve göz ardı edilmelidir.                                                   |
| NX_SECURE_TLS_REPEAT_MESSAGE_RECEIVED             | 0x11F  | Zaten görtiğimiz bir sıra numarası ile bir DTLS iletisi alındı, yok sayın.                                                                           |
| NX_SECURE_TLS_NEED_DTLS_SESSION                   | 0x120  | DTLS API 'sinde DTLS için başlatılmamış bir TLS oturumu kullanıldı.                                                                                       |
| NX_SECURE_TLS_NEED_TLS_SESSION                    | 0x121  | TLS değil, DTLS için başlatılan TLS API 'sinde bir TLS oturumu kullanıldı.                                                                                |
| NX_SECURE_TLS_SEND_ADDRESS_MISMATCH               | 0x122  | Çağıran, oturumla eşleşmeyen bir IP adresi veya bağlantı noktasıyla bir DTLS oturumu üzerinden veri gönderilmeye çalıştı.                                                  |
| NX_SECURE_TLS_NO_FREE_DTLS_SESSIONS              | 0x123  | Yeni bir bağlantı önbellekten DTLS oturumu almaya çalıştı, ancak hiç boş yoktu.                                                                        |
| NX_SECURE_DTLS_SESSION_NOT_FOUND                  | 0x124  | Çağıran bir DTLS oturumu aradı, ancak verilen IP adresi ve bağlantı noktası önbellekteki girdilerle eşleşmedi.                                             |
| NX_SECURE_TLS_NO_MORE_PSK_SPACE                  | 0x125  | Çağıran bir TLS oturumuna PSK eklemeyi denedi ancak belirtilen oturumda daha fazla alan yoktu.                                                          |
| NX_SECURE_TLS_NO_MATCHING_PSK                     | 0x126  | Uzak ana bilgisayar, yerel depomızdan hiçbiriyle eşleşmeyen bir PSK kimlik ipucu sağladı.                                                                         |
| NX_SECURE_TLS_CLOSE_NOTIFY_RECEIVED               | 0x127  | Bir TLS oturumu, oturum tamamlandığını belirten uzak ana bilgisayardan bir CloseNotify uyarısı aldı.                                                           |
| NX_SECURE_TLS_NO_AVAILABLE_SESSIONS               | 0x128  | Bir bağlantıyı işlemek için TLS nesnesinde bir TLS oturumu yok.                                                                                         |
| NX_SECURE_TLS_NO_CERT_SPACE_ALLOCATED            | 0x129  | Gelen uzak sertifikalar için hiçbir sertifika alanı ayrılmadı.                                                                                          |
| NX_SECURE_TLS_PADDING_CHECK_FAILED                | 0x12A  | Gelen iletide şifreleme doldurma doğru değildi.                                                                                                    |
| NX_SECURE_TLS_UNSUPPORTED_CERT_SIGN_TYPE         | 0x12B  | Bir CertificateVerifyRequest işlenirken, uzak sunucu tarafından desteklenen bir sertifika türü sağlanmadı.                                                    |
| NX_SECURE_TLS_UNSUPPORTED_CERT_SIGN_ALG          | 0x12C  | Bir CertificateVerifyRequest işlenirken, uzak sunucu tarafından desteklenen imza algoritması sağlanmadı.                                                 |
| NX_SECURE_TLS_INSUFFICIENT_CERT_SPACE             | 0x12D  | Bir sertifika için ayrılan yeterli sertifika arabelleği alanı yok.                                                                                              |
| NX_SECURE_TLS_PROTOCOL_VERSION_CHANGED            | 0x12E  | Gelen bir TLS kaydındaki protokol sürümü, belirlenen oturumun sürümüyle eşleşmedi.                                                          |
| NX_SECURE_TLS_NO_RENEGOTIATION_ERROR              | 0x12F  | Bir merhaba Istek iletisi alındı, ancak yeniden anlaşıyoruz.                                                                                           |
| NX_SECURE_TLS_UNSUPPORTED_FEATURE                  | 0x130  | Bir TLS oturumu veya el sıkışma sırasında devre dışı bırakılmış bir özelliğe rastlandı.                                                                                |
| NX_SECURE_TLS_CERTIFICATE_VERIFY_FAILURE          | 0x131  | Uzak bir Istemciden bir CertificateVerify iletisi, Istemci sertifikasını doğrulayamadı.                                                                     |
| NX_SECURE_TLS_EMPTY_REMOTE_CERTIFICATE_RECEIVED  | 0x132  | Uzak ana bilgisayar boş bir sertifika iletisi gönderdi.                                                                                                            |
| NX_SECURE_TLS_RENEGOTIATION_EXTENSION_ERROR       | 0x133  | Güvenli bir Renegotation gösterge uzantısı işlenirken veya gönderilirken hata oluştu.                                                                      |
| NX_SECURE_TLS_RENEGOTIATION_SESSION_INACTIVE      | 0x134  | Oturum yeniden anlaşması, etkin olmayan bir TLS oturumu ile yapılmaya çalışılıyor.                                                                                 |
| NX_SECURE_TLS_PACKET_BUFFER_TOO_SMALL            | 0x135  | TLS, atanan paket arabelleği için çok büyük bir kayıt aldı. Kayıt işlenemedi.                                                    |
| NX_SECURE_TLS_EXTENSION_NOT_FOUND                 | 0x136  | TLS anlaşması sırasında uzak konaktan belirtilen bir uzantı alınmadı.                                                                          |
| NX_SECURE_TLS_SNI_EXTENSION_INVALID               | 0x137  | TLS geçersiz bir Sunucu Adı Belirtme uzantısı aldı.                                                                                                      |
| NX_SECURE_TLS_CERT_ID_INVALID                     | 0x138  | Uygulama, geçersiz bir sertifika KIMLIĞI değeri (0) olan bir sunucu sertifikası eklemeye çalıştı.                                                                 |
| NX_SECURE_TLS_CERT_ID_DUPLICATE                   | 0x139  | Uygulama, yerel depoda zaten bir sertifika KIMLIĞINE sahip bir sunucu sertifikası eklemeye çalıştı.                                                        |
| NX_SECURE_TLS_RENEGOTIATION_FAILURE                | 0x13A  | Uzak ana bilgisayar güvenli yeniden anlaşma bildirimi uzantısını veya SCSV sözde ciphersuite 'i sağlamadı, böylece güvenli yeniden anlaşma gerçekleştirilemiyor.      |
| NX_SECURE_TLS_MISSING_CRYPTO_ROUTINE              | 0x13B  | Şifreleme işlemi gerçekleştirmeye çalışırken, ciphersuite tablosundaki girdilerden biri (veya işlev işaretçilerinden biri) yanlış olarak NULL olarak ayarlanmıştır. |
| NX_SECURE_TLS_EMPTY_EC_GROUP                      | 0x13C  | ECC ciphersuite ayarlanmış ancak desteklenen EC grubu yok.                                                                                                             |
| NX_SECURE_TLS_EMPTY_EC_POINT_FORMAT              | 0x13D  | ECC ciphersuite ayarlanmış ancak desteklenen EC noktası biçimi yok.                                                                                                      |
| NX_SECURE_TLS_BAD_SERVERHELLO_KEYSHARE            | 0x13E  | Uzak bir sunucudan bir TLS 1,3 KeyShare uzantısında, sunucu beklemediğimiz bir şey sağladı.                                                         |
| NX_SECURE_TLS_INSUFFICIENT_METADATA_SPACE         | 0x13F  | TLS şifreleme yordamları için uygulama tarafından sağlanan "metadata" çok küçük.                                                                             |
| NX_SECURE_TLS_POST_HANDSHAKE_RECEIVED             | 0x140  | Bir hata değil, uygulama verileri alınana kadar işleme devam etmek için bir gösterge.                                                                    |
| NX_SECURE_TLS_BAD_CLIENTHELLO_KEYSHARE            | 0x141  | Uzak bir istemciden bir TLS 1,3 KeyShare uzantısında, istemci beklemediğimiz bir şey sağladı.                                                         |
| NX_SECURE_TLS_1_3_UNKNOWN_CIPHERSUITE            | 0x142  | TLS 1,3 kullanılırken bilinmeyen ciphersuite alındı.                                                                                                              |
| NX_SECURE_TLS_INVALID_SESSION_TICKET              | 0x143  | Yanlış veya geçersiz parametrelere sahip bir Newsessionbilet iletisi alındı.                                                                                      |
| NX_SECURE_TLS_MISSING_EXTENSION                    | 0x144  | İletide belirli bir uzantı kaçırıldı.                                                                                                                  |
| NX_SECURE_TLS_CERTIFICATE_REQUIRED                 | 0x145  | Sunucu boş bir sertifika aldı.                                                                                                                         |
| NX_SECURE_TLS_UNEXPECTED_CLIENTHELLO               | 0x146  | TLS 1,3 sunucusu yeniden anlaşma için ClientHello alır.                                                                                                         |
| NX_SECURE_TLS_INAPPROPRIATE_FALLBACK               | 0x147  | Uzak Istemci uygunsuz bir TLS sürümü düşürme girişiminde bulunuldu.                                                                                               |
| NX_SECURE_TLS_BAD_CLIENTHELLO_PSK_EXTENSION      | 0x148  | Uzak bir istemciden TLS 1,3 PSK uzantısında, istemci beklemediğimiz bir şey sağladı.                                                              |
| NX_SECURE_TLS_PSK_BINDER_MISMATCH                 | 0x149  | Uzak bir istemciden bir TLS 1,3 PSK uzantısında, istemci hatalı bir PSK Ciltçi değeri sağladı.                                                                  |
| NX_SECURE_TLS_CRYPTO_KEYS_TOO_LARGE              | 0x14A  | TLS oturum anahtarları oluşturma girişiminde, anahtar arabelleği çok küçük NX_SECURE_TLS_KEY_MATERIAL_SIZE artmıştı.                                     |
| NX_SECURE_TLS_UNSUPPORTED_ECC_CURVE               | 0x14B  | Uzak ana bilgisayar bir sertifika sağladı veya desteklenmeyen bir ECC eğrisi ile ciphersuite seçti.                                                         |
| NX_SECURE_TLS_UNSUPPORTED_ECC_FORMAT              | 0x14C  | Desteklenmeyen bir eğri türü veya ECC biçimi ile karşılaşıldı.                                                                                                 |
| NX_SECURE_TLS_UNSUPPORTED_SIGNATURE_ALGORITHM     | 0x14D  | Desteklenmeyen bir imza algoritması ile karşılaşıldı (anahtar değişim veya sertifika olmayan diğer durumlarda kullanılır).                                                |
| NX_SECURE_TLS_SIGNATURE_VERIFICATION_ERROR        | 0x14E  | İmza doğrulama denetimi başarısız oldu (anahtar değişim veya diğer sertifika olmayan durumlarda kullanılır).                                                                    |
| NX_SECURE_TLS_UNEXPECTED_MESSAGE                   | 0x14F  | TLS uzak ana bilgisayardan beklenmeyen bir ileti aldı.                                                                                                      |
| NX_SECURE_TLS_AEAD_DECRYPT_FAIL                   | 0x150  | Gelen bir kayıt, AEAD şifrelemeleri ile bütünlük denetimini geçirmedi.                                                                                            |
| NX_SECURE_TLS_RECORD_OVERFLOW                      | 0x151  | Uzunluğu çok uzun olan bir Tlscbir metin kaydı alındı.                                                                                                   |
| NX_SECURE_TLS_HANDSHAKE_FRAGMENT_RECEIVED         | 0x152  | Parçalanmış bir el sıkışma iletisi alındı-durum makinesinin daha yüksek bir düzeyinde uygun eylemi gerçekleştirin.                                                     |

**Tablo 1 – NetX güvenli TLS hata dönüş kodları**

## <a name="netx-secure-x509-return-codes"></a>NetX Secure X. 509.440 dönüş kodları

Aşağıdaki tablo 2, NetX Secure X. 509.440 Hizmetleri tarafından döndürülebilecek olası hata kodlarını listeler. Hizmetlerin diğer hata kodlarını da döndürebileceğini unutmayın. X. 509.952 dönüş değerleri 0x181 ' den başlayarak, TLS değerleri 0x101 ' den başlar ve TCP/IP değerleri 0x100 ' den fazla. TCP/IP dönüş değerleri ve üzeri TLS dönüş değerleri hakkında bilgi için NetX TCP/IP belgelerine bakın.

| Hata adı                                   | Değer | Açıklama                                                                                                        |
| ------------------------------------------------ | --------- | ---------------------------------------------------------------------------------------------------------------------- |
| NX_SECURE_X509_SUCCESS                        | -      | Başarılı dönüş durumu. (NX_SUCCESS ile aynı)                                                                        |
| NX_SECURE_X509_MULTIBYTE_TAG_UNSUPPORTED    | 0x181     | Multi-Byte ASN. 1 etiketiyle karşılaştık. Şu anda desteklenmiyor.                                                       |
| NX_SECURE_X509_ASN1_LENGTH_TOO_LONG        | 0x182     | İşleyebileceğinden daha uzun bir uzunluk değeriyle karşılaşıldı.                                                                  |
| NX_SECURE_X509_FOUND_NON_ZERO_PADDING      | 0x183     | 0 doldurma değeri bekleniyor-farklı bir şey alındı.                                                               |
| NX_SECURE_X509_MISSING_PUBLIC_KEY           | 0x184     | X509 ortak anahtar bekliyordu, ancak bir tane bulamadı.                                                                        |
| NX_SECURE_X509_INVALID_PUBLIC_KEY           | 0x185     | Ortak anahtar bulundu, ancak geçersiz veya biçimi hatalı.                                                      |
| NX_SECURE_X509_INVALID_CERTIFICATE_SEQUENCE | 0x186     | Üst düzey ASN. 1 bloğu bir sıra-geçersiz x509 sertifikası değil.                                                |
| NX_SECURE_X509_MISSING_SIGNATURE_ALGORITHM  | 0x187     | İmza algoritması tanımlayıcısı beklenirken, bulunamadı.                                                           |
| NX_SECURE_X509_INVALID_CERTIFICATE_DATA     | 0x188     | Sertifika kimliği verileri geçersiz bir biçimde.                                                                     |
| NX_SECURE_X509_UNEXPECTED_ASN1_TAG          | 0x189     | X509 biçimi için belirli bir ASN. 1 etiketi bekliyorduk, ancak başka bir şey var.                                      |
| NX_SECURE_PKCS1_INVALID_PRIVATE_KEY         | 0x18A     | PKCS # 1 özel anahtar dosyası geçirildi, ancak biçimlendirme yanlış.                                            |
| NX_SECURE_X509_CHAIN_TOO_SHORT              | 0x18B     | X509 sertifika zinciri zincir oluşturma sırasında tüm zinciri tutmak için çok kısaydı.                                |
| NX_SECURE_X509_CHAIN_VERIFY_FAILURE         | 0x18C     | X509 sertifika zinciri doğrulanamadı (catch-all Error).                                                 |
| NX_SECURE_X509_PKCS7_PARSING_FAILED         | 0x18D     | X. 509.952 PKCS # 7 kodlu imzayı ayrıştırma başarısız oldu.                                                                     |
| NX_SECURE_X509_CERTIFICATE_NOT_FOUND        | 0x18E     | Bir sertifika aranırken, eşleşen bir giriş bulunamadı.                                                              |
| NX_SECURE_X509_INVALID_VERSION               | 0x18F     | Sertifika, belirtilen sürümle uyumlu olmayan bir alan içeriyordu.                                           |
| NX_SECURE_X509_INVALID_TAG_CLASS            | 0x190     | Sertifika, geçersiz bir etiket sınıfı değeri olan bir ASN. 1 etiketi içeriyordu.                                                   |
| NX_SECURE_X509_INVALID_EXTENSIONS            | 0x191     | Bir sertifika, bir dizi uzantısı olan, ancak bir sıra içermeyen bir uzantıya dahil edilmiştir.                                          |
| NX_SECURE_X509_INVALID_EXTENSION_SEQUENCE   | 0x192     | Sertifika, geçersiz X. 509.440 olan bir uzantı dizisine dahil edildi.                                                   |
| NX_SECURE_X509_CERTIFICATE_EXPIRED           | 0x193     | Sertifikada, geçerli saatten daha az bir "değil" alanı vardı.                                             |
| NX_SECURE_X509_CERTIFICATE_NOT_YET_VALID   | 0x194     | Sertifikada, geçerli saatten daha büyük bir "değil" alanı vardı.                                         |
| NX_SECURE_X509_CERTIFICATE_DNS_MISMATCH     | 0x195     | Sertifika ortak adı veya konu alt adı, verilen bir DNS TLD ile eşleşmedi.                                           |
| NX_SECURE_X509_INVALID_DATE_FORMAT          | 0x196     | Bir sertifika, tanınmayan biçimde olmayan bir tarih alanı içeriyordu.                                               |
| NX_SECURE_X509_CRL_ISSUER_MISMATCH          | 0x197     | Belirtilen bir CRL ve sertifika aynı sertifika yetkilisi tarafından verilmemiş.                                      |
| NX_SECURE_X509_CRL_SIGNATURE_CHECK_FAILED  | 0x198     | Bir CRL imza denetimi, veren tarafından başarısız oldu.                                                                       |
| NX_SECURE_X509_CRL_CERTIFICATE_REVOKED      | 0x199     | Geçerli bir CRL 'de bir sertifika bulundu ve bu nedenle iptal edildi.                                                 |
| NX_SECURE_X509_WRONG_SIGNATURE_METHOD       | 0x19A     | Bir imzayı doğrulamaya çalışırken imza yöntemi beklenen yöntemle eşleşmedi.                          |
| NX_SECURE_X509_EXTENSION_NOT_FOUND          | 0x19B     | Uzantı aranırken, eşleşen KIMLIĞE sahip bir uzantı bulunamadı.                                                |
| NX_SECURE_X509_ALT_NAME_NOT_FOUND          | 0x19C     | SubjectAltName uzantısında bir ad arandı, ancak bulunamadı.                                               |
| NX_SECURE_X509_INVALID_PRIVATE_KEY_TYPE    | 0x19D     | Verilen özel anahtar türü bilinmiyor veya geçersiz.                                                                         |
| NX_SECURE_X509_NAME_STRING_TOO_LONG        | 0x19E     | İç arabellek (DNS adı vb.) için çok uzun olan bir ad dizesi geçildi.                                        |
| NX_SECURE_X509_EXT_KEY_USAGE_NOT_FOUND    | 0x19F     | Genişletilmiş anahtar kullanımı uzantısını aramada, belirtilen anahtar kullanımı OID 'si bulunamadı.                               |
| NX_SECURE_X509_KEY_USAGE_ERROR              | 0x1A0     | Sertifika doğrulama denetimi sırasında anahtar kullanımında bir hata oluşursa, uygulama geri çağırması tarafından döndürülmek üzere. |

**Tablo 2 – NetX güvenli X. 509.440 hata dönüş kodları**
