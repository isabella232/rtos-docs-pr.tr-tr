---
title: Ek A - Azure RTOS NetX Secure dönüş/hata kodları
description: NetX Güvenli Dönüş/Hata Kodları
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 3957075f2b2e83f70bbd5f267cac41f003eb7d93722a3b2247b2a33226b4dfc5
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116791763"
---
# <a name="appendix-a---azure-rtos-netx-secure-returnerror-codes"></a>Ek A - Azure RTOS NetX Secure dönüş/hata kodları

## <a name="netx-secure-tls-return-codes"></a>NetX Secure TLS dönüş kodları

Aşağıdaki Tablo 1'de, NetX Secure TLS hizmetleri tarafından Azure RTOS olası hata kodları listelenmiştir. Hizmetlerin TCP/IP hata kodları da dönebilirsiniz. TLS değerleri 0x101 başlar ve TCP/IP değerleri de 0x100. X.509 dönüş değerleri ilk olarak 0x181. TCP/IP dönüş değerleri hakkında bilgi için NetX TCP/IP belgelerine bakın ve X.509 değerleri için aşağıya bakın.

| Hata Adı                                             | Değer  | Açıklama                                                                                                                                                    |
| ---------------------------------------------------------- | ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| NX_SECURE_TLS_SUCCESS                              | 0x00  | İşlev başarıyla döndürüldü. (Diğer NX_SUCCESS).                                                                                                         |
| NX_SECURE_TLS_SESSION_UNINITIALIZED               | 0x101  | TlS ana döngüsü, uninitialized socket ile çağrılır.                                                                                                               |
| NX_SECURE_TLS_UNRECOGNIZED_MESSAGE_TYPE          | 0x102  | TLS kayıt katmanı tanınmayan bir ileti türü aldı.                                                                                                       |
| NX_SECURE_TLS_INVALID_STATE                       | 0x103  | İç hata - durum tanınmıyor.                                                                                                                        |
| NX_SECURE_TLS_INVALID_PACKET                      | 0x104  | İç hata - alınan paket TLS verileri içermedi.                                                                                                    |
| NX_SECURE_TLS_UNKNOWN_CIPHERSUITE                 | 0x105  | Seçilen şifreleme desteklenmiyor- sunucu için iç hata, istemci için uzak ana bilgisayarın hatalı bir şifreleme gönderdiği anlamına gelir (hata veya saldırı).            |
| NX_SECURE_TLS_UNSUPPORTED_CIPHER                  | 0x106  | Şifreleme veya şifre çözme işlemi yaparken, seçilen şifreleme devre dışı bırakılır veya kullanılamaz.                                                                           |
| NX_SECURE_TLS_HANDSHAKE_FAILURE                   | 0x107  | El sıkışma sırasında ileti işlemede bir şey başarısız oldu.                                                                                              |
| NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE           | 0x108  | Gelen kayıtta, bizim oluşturulan kayıtla eşleşmeen bir MAC vardı.                                                                                         |
| NX_SECURE_TLS_TCP_SEND_FAILED                    | 0x109  | Bir kaydın giden TCP gönderme işlemi bir nedenle başarısız oldu.                                                                                                     |
| NX_SECURE_TLS_INCORRECT_MESSAGE_LENGTH            | 0x10A  | Gelen iletinin uzunluğu yanlıştı (genellikle sertifika iletisinde olduğu gibi üst bilgide yer alan iletilerden farklı bir uzunluk)                               |
| NX_SECURE_TLS_BAD_CIPHERSPEC                      | 0x10B  | Gelen bir ChangeCipherSpec iletisi yanlıştı.                                                                                                           |
| NX_SECURE_TLS_INVALID_SERVER_CERT                | 0x10C  | Gelen sunucu sertifikası düzgün ayrıştırmdı.                                                                                                       |
| NX_SECURE_TLS_UNSUPPORTED_PUBLIC_CIPHER          | 0x10D  | Sunucu tarafından sağlanan ve desteklememiz gereken ortak anahtar işlemi belirtilen bir sertifika.                                                                        |
| NX_SECURE_TLS_NO_SUPPORTED_CIPHERS               | 0x10E  | Desteklenen şifrelemelere sahip bir ClientHello alındı.                                                                                                        |
| NX_SECURE_TLS_UNKNOWN_TLS_VERSION                | 0x10F  | Gelen kayıt, tanınmaz bir TLS sürümüne sahipti.                                                                                                   |
| NX_SECURE_TLS_UNSUPPORTED_TLS_VERSION            | 0x110  | Gelen kayıt geçerli bir TLS sürümüne sahipti ancak bu sürüm desteklenmiyor.                                                                                     |
| NX_SECURE_TLS_ALLOCATE_PACKET_FAILED             | 0x111 | TLS iletisi için iç paket ayırma işlemi başarısız oldu.                                                                                                        |
| NX_SECURE_TLS_INVALID_CERTIFICATE                 | 0x112  | X509 sertifikası doğru ayrıştırmdı.                                                                                                                  |
| NX_SECURE_TLS_NO_CLOSE_RESPONSE                  | 0x113 | TLS oturumu kapatılıyorsa, uzak konaktan CloseNotify almadı.                                                                               |
| NX_SECURE_TLS_ALERT_RECEIVED                      | 0x114 | Uzak konak bir hata olduğunu belirten ve bağlantıyı kapatan bir uyarı gönderdi.                                                                                |
| NX_SECURE_TLS_FINISHED_HASH_FAILURE              | 0x115  | Alınan Son ileti karması yerel olarak oluşturulan karma değerle eşle değil, el sıkışma bozulması.                                                              |
| NX_SECURE_TLS_UNKNOWN_CERT_SIG_ALGORITHM         | 0x116 | Doğrulama sırasında bir sertifikanın desteklenmeyen bir imza algoritması vardı.                                                                                     |
| NX_SECURE_TLS_CERTIFICATE_SIG_CHECK_FAILED       | 0x117  | Sertifika imzası doğrulama denetimi başarısız oldu - sertifika verileri imzayla eşleşmedi.                                                                 |
| NX_SECURE_TLS_BAD_COMPRESSION_METHOD              | 0x118  | Desteklenmeyen sıkıştırma yöntemiyle bir Merhaba iletisi alındı.                                                                                              |
| NX_SECURE_TLS_CERTIFICATE_NOT_FOUND               | 0x119  | Sertifika listesinde bir işlemde eşleşen bir sertifika bulunamadı.                                                                                     |
| NX_SECURE_TLS_INVALID_SELF_SIGNED_CERT           | 0x11A  | Uzak konak otomatik olarak imzalanan bir sertifika gönderdi ve NX_SECURE_ALLOW_SELF_SIGNED_CERTIFICATES tanımlı değil.                                              |
| NX_SECURE_TLS_ISSUER_CERTIFICATE_NOT_FOUND       | 0x11B  | Yerel güvenilen depoda yer alan bir sertifikayı ile uzak sertifika alındı.                                                                              |
| NX_SECURE_TLS_OUT_OF_ORDER_MESSAGE               | 0x11C  | DTLS iletisi yanlış sırada alındı; büyük olasılıkla hata veri birimi bırakıldı.                                                                    |
| NX_SECURE_TLS_INVALID_REMOTE_HOST                 | 0x11D  | Tanımayarak uzak bir konaktan bir paket alındı.                                                                                            |
| NX_SECURE_TLS_INVALID_EPOCH                        | 0x11E  | Bir DTLS iletisi alındı ve bir DTLS oturumuyla eşlandı ama yanlış dönem vardı ve yoksayıldı.                                                   |
| NX_SECURE_TLS_REPEAT_MESSAGE_RECEIVED             | 0x11F  | Daha önce gördük, yoksayarak bir dizi numarası ile bir DTLS iletisi alındı.                                                                           |
| NX_SECURE_TLS_NEED_DTLS_SESSION                   | 0x120  | DTLS için başlatılmamış bir DTLS API'sinde TLS oturumu kullanıldı.                                                                                       |
| NX_SECURE_TLS_NEED_TLS_SESSION                    | 0x121  | TLS oturumu TLS için değil DTLS için başlatılan bir TLS API'de kullanıldı.                                                                                |
| NX_SECURE_TLS_SEND_ADDRESS_MISMATCH               | 0x122  | Çağıran, oturumla eşleşmeen bir IP adresi veya bağlantı noktası ile DTLS oturumu üzerinden veri göndermeye çalıştı.                                                  |
| NX_SECURE_TLS_NO_FREE_DTLS_SESSIONS              | 0x123  | Yeni bir bağlantı önbellekten DTLS oturumu almaya çalıştı ama hiç boş yoktu.                                                                        |
| NX_SECURE_DTLS_SESSION_NOT_FOUND                  | 0x124  | Çağıran bir DTLS oturumu aradı, ancak verilen IP adresi ve bağlantı noktası önbellekte hiçbir girdiyle eşleşmedi.                                             |
| NX_SECURE_TLS_NO_MORE_PSK_SPACE                  | 0x125  | Çağıran TLS oturumuna PSK eklemeye çalıştı ancak verilen oturumda daha fazla alan yoktu.                                                          |
| NX_SECURE_TLS_NO_MATCHING_PSK                     | 0x126  | Uzak konak, yerel depomuzda hiçbir ile eşleşmeen bir PSK kimlik ipucu sağladı.                                                                         |
| NX_SECURE_TLS_CLOSE_NOTIFY_RECEIVED               | 0x127  | TLS oturumu, uzak konaktan oturumun tamam olduğunu belirten bir CloseNotify uyarısı aldı.                                                           |
| NX_SECURE_TLS_NO_AVAILABLE_SESSIONS               | 0x128  | Bir bağlantıyı işlemek için TLS nesnesinde TLS oturumu yoktur.                                                                                         |
| NX_SECURE_TLS_NO_CERT_SPACE_ALLOCATED            | 0x129  | Gelen uzak sertifikalar için sertifika alanı tahsis edildi.                                                                                          |
| NX_SECURE_TLS_PADDING_CHECK_FAILED                | 0x12A  | Gelen iletide şifreleme doldurma doğru değil.                                                                                                    |
| NX_SECURE_TLS_UNSUPPORTED_CERT_SIGN_TYPE         | 0x12B  | CertificateVerifyRequest işleme sırasında, uzak sunucu tarafından desteklenen bir sertifika türü sağlanmamıştır.                                                    |
| NX_SECURE_TLS_UNSUPPORTED_CERT_SIGN_ALG          | 0x12C  | CertificateVerifyRequest işleme sırasında, uzak sunucu tarafından desteklenen bir imza algoritması sağlanmamıştır.                                                 |
| NX_SECURE_TLS_INSUFFICIENT_CERT_SPACE             | 0x12D  | Bir sertifika için yeterli sertifika arabellek alanı ayrılamadı.                                                                                              |
| NX_SECURE_TLS_PROTOCOL_VERSION_CHANGED            | 0x12E  | Gelen TLS kaydında protokol sürümü, kurulan oturumun sürümüyle eşleşmedi.                                                          |
| NX_SECURE_TLS_NO_RENEGOTIATION_ERROR              | 0x12F  | HelloRequest iletisi alındı, ancak yeniden anlaşma yok.                                                                                           |
| NX_SECURE_TLS_UNSUPPORTED_FEATURE                  | 0x130  | TLS oturumu veya el sıkışması sırasında devre dışı bırakılmış bir özellikle karşılaşıldı.                                                                                |
| NX_SECURE_TLS_CERTIFICATE_VERIFY_FAILURE          | 0x131  | Uzak bir İstemciden gelen CertificateVerify iletisi İstemci sertifikasını doğrulanamadı.                                                                     |
| NX_SECURE_TLS_EMPTY_REMOTE_CERTIFICATE_RECEIVED  | 0x132  | Uzak konak boş bir sertifika iletisi gönderdi.                                                                                                            |
| NX_SECURE_TLS_RENEGOTIATION_EXTENSION_ERROR       | 0x133  | Güvenli Yeniden Yoklama Göstergesi uzantısını işleme veya gönderme sırasında bir hata oluştu.                                                                      |
| NX_SECURE_TLS_RENEGOTIATION_SESSION_INACTIVE      | 0x134  | Oturum yeniden görüşme girişimi, etkin olan bir TLS oturumuyla başarısız oldu.                                                                                 |
| NX_SECURE_TLS_PACKET_BUFFER_TOO_SMALL            | 0x135  | TLS, atanan paket arabelleği için çok büyük bir kayıt aldı. Kayıt işlenemedi.                                                    |
| NX_SECURE_TLS_EXTENSION_NOT_FOUND                 | 0x136  | TLS el sıkışması sırasında uzak konaktan belirtilen bir uzantı alınmmıştır.                                                                          |
| NX_SECURE_TLS_SNI_EXTENSION_INVALID               | 0x137  | TLS, geçersiz bir Sunucu Adı Belirtme aldı.                                                                                                      |
| NX_SECURE_TLS_CERT_ID_INVALID                     | 0x138  | Uygulama, geçersiz sertifika kimliği değerine (büyük olasılıkla 0) sahip bir sunucu sertifikası eklemeye çalıştı.                                                                 |
| NX_SECURE_TLS_CERT_ID_DUPLICATE                   | 0x139  | Uygulama, yerel depoda zaten var olan bir sertifika kimliğine sahip bir sunucu sertifikası eklemeye çalıştı.                                                        |
| NX_SECURE_TLS_RENEGOTIATION_FAILURE                | 0x13A  | Uzak konak Güvenli Yeniden Yapılanma Göstergesi Uzantısını veya SCSV sözde şifrelemeyi sağlamadı, bu nedenle güvenli yeniden yapılanma gerçekleştirilemez.      |
| NX_SECURE_TLS_MISSING_CRYPTO_ROUTINE              | 0x13B  | Şifreleme işlemi gerçekleştirmeye çalışırken, şifreleme tablosu (veya işlev işaretçilerinden biri) girişlerinden biri hatalı şekilde NULL olarak ayarlanmıştır. |
| NX_SECURE_TLS_EMPTY_EC_GROUP                      | 0x13C  | ECC şifrelemesi ayarlanmıştır ancak desteklenen bir EC grubu yoktur.                                                                                                             |
| NX_SECURE_TLS_EMPTY_EC_POINT_FORMAT              | 0x13D  | ECC şifrelemesi ayarlanmıştır ancak desteklenen EC noktası biçimi yoktur.                                                                                                      |
| NX_SECURE_TLS_BAD_SERVERHELLO_KEYSHARE            | 0x13E  | Uzak bir sunucudan gelen TLS 1.3 KeyShare uzantısında sunucu beklememiz gereken bir şeyi sağladı.                                                         |
| NX_SECURE_TLS_INSUFFICIENT_METADATA_SPACE         | 0x13F  | TLS şifreleme yordamları için uygulama tarafından sağlanan "meta veriler" çok küçüktü.                                                                             |
| NX_SECURE_TLS_POST_HANDSHAKE_RECEIVED             | 0x140  | Hata değil, uygulama verileri alınana kadar işlemeye devam etmek için bir gösterge.                                                                    |
| NX_SECURE_TLS_BAD_CLIENTHELLO_KEYSHARE            | 0x141  | Uzak istemcinin TLS 1.3 KeyShare uzantısında, istemci beklememiz gereken bir şeyi sağladı.                                                         |
| NX_SECURE_TLS_1_3_UNKNOWN_CIPHERSUITE            | 0x142  | TLS 1.3 kullanırken bilinmeyen şifreleme alındı.                                                                                                              |
| NX_SECURE_TLS_INVALID_SESSION_TICKET              | 0x143  | Hatalı veya geçersiz parametrelerle NewSessionTicket iletisi alındı.                                                                                      |
| NX_SECURE_TLS_MISSING_EXTENSION                    | 0x144  | İletide belirli bir uzantı atladı.                                                                                                                  |
| NX_SECURE_TLS_CERTIFICATE_REQUIRED                 | 0x145  | Sunucu boş bir sertifika aldı.                                                                                                                         |
| NX_SECURE_TLS_UNEXPECTED_CLIENTHELLO               | 0x146  | TLS 1.3 Sunucusu yeniden yapılanma için ClientHello'yu alır.                                                                                                         |
| NX_SECURE_TLS_INAPPROPRIATE_FALLBACK               | 0x147  | Uzak İstemci uygun olmayan bir TLS sürümü eski sürüme düşürme girişiminde bulundu.                                                                                               |
| NX_SECURE_TLS_BAD_CLIENTHELLO_PSK_EXTENSION      | 0x148  | Uzak istemcinin TLS 1.3 PSK uzantısında, istemci beklememiz gereken bir şeyi sağladı.                                                              |
| NX_SECURE_TLS_PSK_BINDER_MISMATCH                 | 0x149  | Uzak istemcinin TLS 1.3 PSK uzantısında, istemci hatalı bir PSK bağlayıcı değeri sağladı.                                                                  |
| NX_SECURE_TLS_CRYPTO_KEYS_TOO_LARGE              | 0x14A  | TLS oturum anahtarları oluşturmak için anahtar arabelleği çok küçüktü ve bu da NX_SECURE_TLS_KEY_MATERIAL_SIZE.                                     |
| NX_SECURE_TLS_UNSUPPORTED_ECC_CURVE               | 0x14B  | Uzak konak bir sertifika sağladı veya ECC eğrisi ile desteklenen bir şifreleme seçti.                                                         |
| NX_SECURE_TLS_UNSUPPORTED_ECC_FORMAT              | 0x14C  | Desteklenen bir eğri türü veya ECC biçimiyle karşılaşıldı.                                                                                                 |
| NX_SECURE_TLS_UNSUPPORTED_SIGNATURE_ALGORITHM     | 0x14D  | Desteklenmeyen bir imza algoritmasıyla karşılaşıldı (anahtar değişiminde veya sertifika olmayan diğer durumlarda kullanılır).                                                |
| NX_SECURE_TLS_SIGNATURE_VERIFICATION_ERROR        | 0x14E  | İmza doğrulama denetimi başarısız oldu (anahtar değişiminde veya diğer sertifika dışı durumlarda kullanılır).                                                                    |
| NX_SECURE_TLS_UNEXPECTED_MESSAGE                   | 0x14F  | TLS uzak konaktan beklenmeyen bir ileti aldı.                                                                                                      |
| NX_SECURE_TLS_AEAD_DECRYPT_FAIL                   | 0x150  | Gelen kayıt AEAD şifrelemeleriyle bütünlük denetimi geçmedi.                                                                                            |
| NX_SECURE_TLS_RECORD_OVERFLOW                      | 0x151  | Uzunluğu çok uzun olan bir TLSCiphertext kaydı alındı.                                                                                                   |
| NX_SECURE_TLS_HANDSHAKE_FRAGMENT_RECEIVED         | 0x152  | Parçalı bir el sıkışma iletisi alındı- durum makinesinin daha yüksek bir düzeyinde uygun eylemi at.                                                     |

| Hata Adı                                             | Değer  | Açıklama                                                                                                                                                    |
| ---------------------------------------------------------- | ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| NX_SECURE_TLS_SUCCESS                               | 0x00   | İşlev başarıyla döndürüldü. (Diğer NX_SUCCESS).                                                                                                         |
| NX_SECURE_TLS_SESSION_UNINITIALIZED                | 0x101  | TlS ana döngüsü, uninitialized socket ile çağrılır.                                                                                                               |
| NX_SECURE_TLS_UNRECOGNIZED_MESSAGE_TYPE           | 0x102  | TLS kayıt katmanı tanınmayan bir ileti türü aldı.                                                                                                       |
| NX_SECURE_TLS_INVALID_STATE                        | 0x103  | İç hata - durum tanınmıyor.                                                                                                                        |
| NX_SECURE_TLS_INVALID_PACKET                       | 0x104  | İç hata - alınan paket TLS verileri içermedi.                                                                                                    |
| NX_SECURE_TLS_UNKNOWN_CIPHERSUITE                  | 0x105  | Seçilen şifreleme desteklenmiyor- sunucu için iç hata, istemci için uzak ana bilgisayarın hatalı bir şifreleme gönderdiği anlamına gelir (hata veya saldırı).            |
| NX_SECURE_TLS_UNSUPPORTED_CIPHER                   | 0x106  | Şifreleme veya şifre çözme işlemi yaparken, seçilen şifreleme devre dışı bırakılır veya kullanılamaz.                                                                           |
| NX_SECURE_TLS_HANDSHAKE_FAILURE                    | 0x107  | El sıkışma sırasında ileti işlemede bir şey başarısız oldu.                                                                                              |
| NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE            | 0x108  | Gelen kayıtta, bizim oluşturulan kayıtla eşleşmeen bir MAC vardı.                                                                                         |
| NX_SECURE_TLS_TCP_SEND_FAILED                     | 0x109  | Bir kaydın giden TCP gönderme işlemi bir nedenle başarısız oldu.                                                                                                     |
| NX_SECURE_TLS_INCORRECT_MESSAGE_LENGTH            | 0x10A  | Gelen iletinin uzunluğu yanlıştı (genellikle sertifika iletisinde olduğu gibi üst bilgide yer alan iletilerden farklı bir uzunluk)                                |
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
| NX_SECURE_TLS_UNSUPPORTED_SIGNATURE_ALGORITHM     | 0x14D  | Desteklenmeyen bir imza algoritmasıyla karşılaşıldı (anahtar değişiminde veya sertifika olmayan diğer durumlarda kullanılır).                                                |
| NX_SECURE_TLS_SIGNATURE_VERIFICATION_ERROR        | 0x14E  | İmza doğrulama denetimi başarısız oldu (anahtar değişiminde veya diğer sertifika dışı durumlarda kullanılır).                                                                    |
| NX_SECURE_TLS_UNEXPECTED_MESSAGE                   | 0x14F  | TLS uzak konaktan beklenmeyen bir ileti aldı.                                                                                                      |
| NX_SECURE_TLS_AEAD_DECRYPT_FAIL                   | 0x150  | Gelen kayıt AEAD şifrelemeleriyle bütünlük denetimi geçmedi.                                                                                            |
| NX_SECURE_TLS_RECORD_OVERFLOW                      | 0x151  | Uzunluğu çok uzun olan bir TLSCiphertext kaydı alındı.                                                                                                   |
| NX_SECURE_TLS_HANDSHAKE_FRAGMENT_RECEIVED         | 0x152  | Parçalı bir el sıkışma iletisi alındı- durum makinesinin daha yüksek bir düzeyinde uygun eylemi at.                                                     |

**Tablo 1 – NetX Secure TLS hata dönüş kodları**

## <a name="netx-secure-x509-return-codes"></a>NetX Secure X.509 Dönüş Kodları

Aşağıdaki Tablo 2'de NetX Secure X.509 hizmetleri tarafından döndürülecek olası hata kodları listelenmiştir. Hizmetlerin başka hata kodları da getirebilirsiniz. X.509 dönüş değerleri 0x181, TLS değerleri 0x101 başlar ve TCP/IP değerleri 0x100. TCP/IP dönüş değerleri ve üzeri TLS dönüş değerleri hakkında bilgi için NetX TCP/IP belgelerine bakın.

| Hata Adı                                   | Değer | Açıklama                                                                                                        |
| ------------------------------------------------ | --------- | ---------------------------------------------------------------------------------------------------------------------- |
| NX_SECURE_X509_SUCCESS                        | 0x00      | Başarılı dönüş durumu. (Diğer NX_SUCCESS)                                                                        |
| NX_SECURE_X509_MULTIBYTE_TAG_UNSUPPORTED    | 0x181     | Çok baytlı ASN.1 etiketiyle karşılaştık; şu anda desteklenmiyor.                                                       |
| NX_SECURE_X509_ASN1_LENGTH_TOO_LONG        | 0x182     | Bizim işleyemeyecek kadar uzun bir değerle karşılaştınız.                                                                  |
| NX_SECURE_X509_FOUND_NON_ZERO_PADDING      | 0x183     | 0 doldurma değeri bekleniyordu- farklı bir şey var.                                                               |
| NX_SECURE_X509_MISSING_PUBLIC_KEY           | 0x184     | X509 bir ortak anahtar bekledi ama bir anahtar bulamadı.                                                                        |
| NX_SECURE_X509_INVALID_PUBLIC_KEY           | 0x185     | Ortak anahtar bulundu, ancak geçersiz veya yanlış bir biçime sahip.                                                      |
| NX_SECURE_X509_INVALID_CERTIFICATE_SEQUENCE | 0x186     | Üst düzey ASN.1 bloğu bir dizi değil, geçersiz X509 sertifikası.                                                |
| NX_SECURE_X509_MISSING_SIGNATURE_ALGORITHM  | 0x187     | İmza algoritması tanımlayıcısı beklenildi, bulamadı.                                                           |
| NX_SECURE_X509_INVALID_CERTIFICATE_DATA     | 0x188     | Sertifika kimliği verileri geçersiz biçimde.                                                                     |
| NX_SECURE_X509_UNEXPECTED_ASN1_TAG          | 0x189     | X509 biçimi için belirli bir ASN.1 etiketi bekliyordunuz ama başka bir şey var.                                      |
| NX_SECURE_PKCS1_INVALID_PRIVATE_KEY         | 0x18A     | PKCS#1 özel anahtar dosyası geçirildi, ancak biçimlendirme yanlıştı.                                            |
| NX_SECURE_X509_CHAIN_TOO_SHORT              | 0x18B     | Bir X509 sertifika zinciri, zincirleme bina sırasında zincirin tamamını tutacak kadar kısaydı.                                |
| NX_SECURE_X509_CHAIN_VERIFY_FAILURE         | 0x18C     | Bir X509 sertifika zinciri doğrulanamadı (hepsini yakalama hatası).                                                 |
| NX_SECURE_X509_PKCS7_PARSING_FAILED         | 0x18D     | X.509 kodlanmış PKCS #7 ayrıştırılamadı.                                                                     |
| NX_SECURE_X509_CERTIFICATE_NOT_FOUND        | 0x18E     | Bir sertifikayı aramada eşleşen bir giriş bulunamadı.                                                              |
| NX_SECURE_X509_INVALID_VERSION               | 0x18F     | Sertifika, verilen sürümle uyumlu olmayan bir alan dahil edildi.                                           |
| NX_SECURE_X509_INVALID_TAG_CLASS            | 0x190     | Sertifika, geçersiz etiket sınıfı değerine sahip bir ASN.1 etiketi içeriyor.                                                   |
| NX_SECURE_X509_INVALID_EXTENSIONS            | 0x191     | Sertifika bir uzantı TLV içeriyor ancak dizi içermedi.                                          |
| NX_SECURE_X509_INVALID_EXTENSION_SEQUENCE   | 0x192     | Sertifika, geçersiz X.509 olan bir uzantı dizisi içeriyor.                                                   |
| NX_SECURE_X509_CERTIFICATE_EXPIRED           | 0x193     | Sertifikanın geçerli saatten daha kısa bir "sonrası değil" alanı vardı.                                             |
| NX_SECURE_X509_CERTIFICATE_NOT_YET_VALID   | 0x194     | Bir sertifikanın "önceki değil" alanı geçerli zamandan büyüktü.                                         |
| NX_SECURE_X509_CERTIFICATE_DNS_MISMATCH     | 0x195     | Sertifika Ortak Adı veya Konu Alt Adı, verilen bir DNS TLD ile eşleşmedi.                                           |
| NX_SECURE_X509_INVALID_DATE_FORMAT          | 0x196     | Sertifika, tanınmış biçimde değil bir tarih alanı içeriyor.                                               |
| NX_SECURE_X509_CRL_ISSUER_MISMATCH          | 0x197     | Sağlanan bir CRL ve sertifika aynı Sertifika Yetkilisi tarafından sağlanmaz.                                      |
| NX_SECURE_X509_CRL_SIGNATURE_CHECK_FAILED  | 0x198     | CrL imza denetimi, sertifikayı alan için başarısız oldu.                                                                       |
| NX_SECURE_X509_CRL_CERTIFICATE_REVOKED      | 0x199     | Geçerli bir CRL'de bir sertifika bulundu ve bu nedenle iptal edildi.                                                 |
| NX_SECURE_X509_WRONG_SIGNATURE_METHOD       | 0x19A     | İmzayı doğrulamaya çalışırken imza yöntemi beklenen yöntemle eşleşmedi.                          |
| NX_SECURE_X509_EXTENSION_NOT_FOUND          | 0x19B     | Uzantıyı bulmak için eşleşen kimliği olan bir uzantı bulunamadı.                                                |
| NX_SECURE_X509_ALT_NAME_NOT_FOUND          | 0x19C     | subjectAltName uzantısında bir ad arandı ancak bulunamadı.                                               |
| NX_SECURE_X509_INVALID_PRIVATE_KEY_TYPE    | 0x19D     | Verilen özel anahtar türü bilinmiyor veya geçersizdi.                                                                         |
| NX_SECURE_X509_NAME_STRING_TOO_LONG        | 0x19E     | İç arabellek (DNS adı vb.) için çok uzun olan bir ad dizesi geçirildi.                                        |
| NX_SECURE_X509_EXT_KEY_USAGE_NOT_FOUND    | 0x19F     | Genişletilmiş Anahtar Kullanımı uzantısını aramada belirtilen anahtar kullanımı OID'i bulunamadı.                               |
| NX_SECURE_X509_KEY_USAGE_ERROR              | 0x1A0     | Sertifika doğrulama denetimi sırasında anahtar kullanımında hata olması durumunda uygulama geri çağırma tarafından döndürülebilir. |

**Tablo 2 – NetX Secure X.509 hata dönüş kodları**
