---
title: Bölüm 4-Azure RTOS NetX güvenli hizmetlerinin açıklaması
description: Bu bölüm, tüm NetX güvenli hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 80ec22058ab64ed0c6258bb3d9364ec44f9a741b
ms.sourcegitcommit: 4ebe7c51ba850951c6a9d0f15e22d07bb752bc28
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/20/2021
ms.locfileid: "110223401"
---
# <a name="chapter-4---description-of-azure-rtos-netx-secure-services"></a>Bölüm 4-Azure RTOS NetX güvenli hizmetlerinin açıklaması

Bu bölüm, tüm Azure RTOS NetX güvenli hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.

Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_SECURE_DISABLE_ERROR_CHECKING** makrodan etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.

- [nx_secure_crypto_table_self_test](#nx_secure_crypto_table_self_test)
  - Şifreleme yöntemlerinde self_test gerçekleştirme
- [nx_secure_module_hash_compute](#nx_secure_module_hash_compute)
  - Karma değeri user_supplied karma işlevi kullanılarak hesaplar
- [nx_secure_tls_active_certificate_set](#nx_secure_tls_active_certificate_set)
  - NetX güvenli TLS oturumu için etkin kimlik sertifikası ayarlama
- [nx_secure_tls_client_psk_set](#nx_secure_tls_client_psk_set)
  - NetX güvenli TLS Istemci oturumu için bir Pre_Shared anahtarı ayarlama
- [nx_secure_tls_initialize](#nx_secure_tls_initialize)
  - NetX güvenli TLS modülünü başlatır]
- [nx_secure_tls_local_certificate_add](#nx_secure_tls_local_certificate_add)
  - NetX güvenli TLS oturumuna yerel sertifika ekleme
- [nx_secure_tls_local_certificate_find](#nx_secure_tls_local_certificate_find)
  - Ortak ad ile bir NetX güvenli TLS oturumunda yerel bir sertifika bulun
- [nx_secure_tls_local_certificate_remove](#nx_secure_tls_local_certificate_remove)
  - NetX Secure TLS Oturumundan yerel sertifikayı kaldırma
- [nx_secure_tls_metadata_size_calculate](#nx_secure_tls_metadata_size_calculate)
  - NetX Güvenli TLS Oturumu için şifreleme meta verisi boyutunu hesaplama
- [nx_secure_tls_packet_allocate](#nx_secure_tls_packet_allocate)
  - NetX Güvenli TLS Oturumu için paket ayırma
- [nx_secure_tls_psk_add](#nx_secure_tls_psk_add)
  - NetX Pre_Shared TLS Oturumuna Bir Anahtar Ekleme
- [nx_secure_tls_remote_certificate_allocate](#nx_secure_tls_remote_certificate_allocate)
  - Uzak bir TLS ana bilgisayarı tarafından sağlanan sertifika için alan ayırma
- [nx_secure_tls_remote_certificate_buffer_allocate](#nx_secure_tls_remote_certificate_buffer_allocate)
  - Uzak bir TLS ana bilgisayarı tarafından sağlanan tüm sertifikalar için alan ayırma
- [nx_secure_tls_remote_certificate_free_all](#nx_secure_tls_remote_certificate_free_all)
  - Gelen sertifikalar için ayrılan boş alan
- [nx_secure_tls_server_certificate_add](#nx_secure_tls_server_certificate_add)
  - Sayısal tanımlayıcı kullanan TLS sunucuları için özel olarak sertifika ekleme
- [nx_secure_tls_server_certificate_find](#nx_secure_tls_server_certificate_find)
  - Sayısal tanımlayıcı kullanarak sertifika bulma
- [nx_secure_tls_server_certificate_remove](#nx_secure_tls_server_certificate_remove)
  - Sayısal tanımlayıcı kullanarak yerel sunucu sertifikasını kaldırma
- [nx_secure_tls_session_certificate_callback_set](#nx_secure_tls_session_certificate_callback_set)
  - Ek sertifika doğrulaması için kullanılacak TLS için bir geri çağırma ayarlayın
- [nx_secure_tls_session_client_callback_set](#nx_secure_tls_session_client_callback_set)
  - TLS Istemcisi el sıkışmasının başlangıcında çağırmak üzere TLS için bir geri çağırma ayarlayın
- [nx_secure_tls_session_x509_client_verify_configure](#nx_secure_tls_session_x509_client_verify_configure)
  - İstemci X. 509.440 doğrulamasını etkinleştir ve istemci sertifikaları için alan ayır
- [nx_secure_tls_session_client_verify_disable](#nx_secure_tls_session_client_verify_disable)
  - NetX güvenli TLS oturumu için Istemci sertifikası kimlik doğrulamasını devre dışı bırakma
- [nx_secure_tls_session_client_verify_enable](#nx_secure_tls_session_client_verify_enable)
  - NetX güvenli TLS oturumu için Istemci sertifikası kimlik doğrulamasını etkinleştir
- [nx_secure_tls_session_create](#nx_secure_tls_session_create)
  - Güvenli iletişim için bir NetX güvenli TLS oturumu oluşturun
- [nx_secure_tls_session_delete](#nx_secure_tls_session_delete)
  - NetX güvenli TLS oturumunu silme
- [nx_secure_tls_session_end](#nx_secure_tls_session_end)
  - Etkin bir NetX güvenli TLS oturumu sonlandır
- [nx_secure_tls_session_packet_buffer_set](#nx_secure_tls_session_packet_buffer_set)
  - NetX güvenli TLS oturumu için paket yeniden birleştirme arabelleğini ayarlama
- [nx_secure_tls_session_protocol_version_override](#nx_secure_tls_session_protocol_version_override)
  - NetX güvenli TLS oturumu için varsayılan TLS protokol sürümünü geçersiz kılın
- [nx_secure_tls_session_receive](#nx_secure_tls_session_receive)
  - NetX Güvenli TLS Oturumundan veri alma
- [nx_secure_tls_session_renegotiate_callback_set](#nx_secure_tls_session_renegotiate_callback_set)
  - Oturum yeniden görüşmenin başında çağrılan bir geri çağırma at atama
- [nx_secure_tls_session_renegotiate](#nx_secure_tls_session_renegotiate)
  - Uzak konakla oturum yeniden anlaşma başlatma
- [nx_secure_tls_session_reset](#nx_secure_tls_session_reset)
  - NetX Secure TLS Oturumunu temizleme ve sıfırlama
- [nx_secure_tls_session_send](#nx_secure_tls_session_send)
  - NetX Güvenli TLS Oturumu aracılığıyla veri gönderme
- [nx_secure_tls_session_server_callback_set](#nx_secure_tls_session_server_callback_set)
  - TLS Sunucusu el sıkışması başlangıcında çağırmak için TLS için bir geri çağırma ayarlayın
- [nx_secure_tls_session_sni_extension_parse](#nx_secure_tls_session_sni_extension_parse)
  - TLS İstemcisi Sunucu Adı Belirtme alınan bir Sunucu Adı Belirtme (SNI) uzantısını ayrıştırma
- [nx_secure_tls_session_sni_extension_set](#nx_secure_tls_session_sni_extension_set)
  - Uzak Sunucu Adı Belirtme (SNI) uzantısı DNS adı ayarlama
- [nx_secure_tls_session_start](#nx_secure_tls_session_start)
  - NetX Güvenli TLS Oturumu Başlatma
- [nx_secure_tls_session_time_function_set](#nx_secure_tls_session_time_function_set)
  - NetX Güvenli TLS Oturumuna zaman damgası işlevi atama
- [nx_secure_tls_trusted_certificate_add](#nx_secure_tls_trusted_certificate_add)
  - NetX güvenli TLS oturumuna güvenilen sertifika ekleme
- [nx_secure_tls_trusted_certificate_remove](#nx_secure_tls_trusted_certificate_remove)
  - Güvenilen sertifikayı NetX güvenli TLS oturumundan kaldır
- [nx_secure_x509_certificate_initialize](#nx_secure_x509_certificate_initialize)
  - NetX güvenli TLS için X. 509.440 sertifikasını başlatın
- [nx_secure_x509_common_name_dns_check](#nx_secure_x509_common_name_dns_check)
  - X. 509.440 sertifikasıyla DNS adını denetle
- [nx_secure_x509_crl_revocation_check](#nx_secure_x509_crl_revocation_check)
  - Sağlanan sertifika Iptal listesine (CRL) göre X. 509.440 sertifikasını denetle]
- [nx_secure_x509_dns_name_initialize](#nx_secure_x509_dns_name_initialize)
  - X. 509.440 DNS adı yapısını başlatma
- [nx_secure_x509_extended_key_usage_extension_parse](#nx_secure_x509_extended_key_usage_extension_parse)
  - X. 509.440 sertifikası içindeki X. 509.952 genişletilmiş anahtar kullanımı uzantısını bulma ve ayrıştırma
- [nx_secure_x509_extension_find](#nx_secure_x509_extension_find)
  - X. 509.440 sertifikasında bir X. 509.440 uzantısı bulun ve döndürün
- [nx_secure_x509_key_usage_extension_parse](#nx_secure_x509_key_usage_extension_parse)
  - X. 509.440 sertifikasında X. 509.440 anahtar kullanımı uzantısını bulma ve ayrıştırma

## <a name="nx_secure_crypto_table_self_test"></a>nx_secure_crypto_table_self_test

Şifre yöntemlerinde kendi kendine test gerçekleştirme

### <a name="prototype"></a>Prototype

```C
UINT nx_secure_crypto_table_self_test(
                                  const NX_SECURE_TLS_CRYPTO *crypto_table,
                                  VOID *metadata, UINT metadata_size);
```

### <a name="description"></a>Description

Bu hizmet, doğrulamak üzere kendi kendini test eden şifreleme yöntemi aracılığıyla çalışır. Kendi kendine test yalnızca NetX Secure kitaplığı tanımlandığı gibi sembolüyle NX_SECURE_POWER_ON_SELF_TEST_MODULE_INTEGRITY_CHECK kullanılabilir.

Desteklenen her şifreleme yöntemi için, kendi kendine test önceden tanımlanmış giriş verileri sağlar ve çıkışın önceden tanımlanmış beklenen değerle eşleştirildi.

NetX Secure şifreleme kendi kendine testi aşağıdaki algoritmaları ve anahtar boyutlarını destekler:

- DES: şifreleme ve şifre çözme
- Üçlü DES (3DES): şifreleme ve şifre çözme
- AES: CBC modunda ve sayaç modunda 128, 192,256 bit anahtar boyutu, şifreleme ve şifre çözme.
- HMAC-MD5: kimlik doğrulaması ve karma hesaplama
- HMAC-SHA: SHA1-96, SHA1-160, SHA2-256, SHA2-384, SHA2- 512, kimlik doğrulaması ve karma hesaplama
- MD5: kimlik doğrulaması
- Sözde rastgele İşlev (PRF): PRF_HMAC_SHA1 ve PRF_HMAC_SHA2-256
- RSA: 1024-, 2048-, 4096 bit RSA güç modulus işlemi
- SHA: SHA1 (96 ve 160 bit), SHA2 (256 bit, 384 bit, 512 bit) kimlik doğrulaması

Bu işlev, yukarıda listelenen şifreleme algoritmaları için yerleşik vektörlere sahiptir. Ancak yalnızca bu işleve geçirilen cipher_table *testlerini* içerir. Örneğin TLS oturumunda yalnızca şifreleme TLS_RSA_WITH_AES_128_CBC_SHA için bu işlev RSA (1024-, 2048-, 4096 bit), AES-CBC (128 bit) ve SHA1 üzerinde kendi kendine test gerçekleştirecek.

### <a name="parameters"></a>Parametreler

- **crypto_table** TLS oturumu tarafından kullanılan şifreleme tablosu işaretçisi. Bu, crypto_table() çağrısına geçirilen **_nx_secure_tls_session_create aynıdır._**
- **meta veriler** Şifreleme meta veri alanı için alan işaretçisi. .
- **metadata_size** Meta veri arabelleğinin boyutu.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SECURE_TLS_SUCCESS** (0x00) Sağlanan şifreleme yöntemleri başarıyla test edildi.
- **NX_PTR_ERROR** (0x07) geçersiz şifreleme yöntemi yapısı
- **NX_NOT_SUCCESSFUL** (0x43) şifreleme self test başarısız oluyor.

### <a name="allowed-from"></a>İzin verilen

Başlatma, Iş parçacıkları

### <a name="example"></a>Örnek

```C
/* crypto_tls_ciphers is the cipher table for the TLS session. */
/* metadata_buffer is the memory area used by the cipher functions. */

/* The following function verifies the supplied ciphersuties using the built-in
   self test. */

if (nx_secure_crypto_table_self_test(&crypto_tls_ciphers, metadata_buffer,
    sizeof(metadata_buffer)))
{
    printf("Crypto self test failed!\r\n");
    exit(0);
}
else
{
    printf("Crypto self test succeed!\r\n");
}

/* Now the ciphersuites are successfully test, it can be used in
   nx_secure_tls_session_create() */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_tls_session_create

## <a name="nx_secure_module_hash_compute"></a>nx_secure_module_hash_compute

Kullanıcı tarafından sağlanan karma işlevi kullanarak karma değeri hesaplar

### <a name="prototype"></a>Prototype

```C
UINT nx_secure_module_hash_compute(
                      NX_CRYPTO_METHOD *hamc_ptr,
                      UINT start_address, UINT end_address,
                      UCHAR *key, UINT key_length,
                      VOID *metadata, UINT metadata_size,
                      UCHAR *output_buffer, UINT output_buffer_size,
                      UINT *actual_size);
```

### <a name="description"></a>Description

Bu işlev, sağlanan HMAC şifre yöntemini ve anahtar dizesini kullanarak belirtilen bellek alanındaki veri akışının karma değerini hesaplar. Modül karma işlem işlevi yalnızca NetX güvenli kitaplığı tanımlanmakta olan şu sembol ile derleniyorsa kullanılabilir: NX_SECURE_POWER_ON_SELF_TEST_MODULE_INTEGRITY_CHECK

### <a name="parameters"></a>Parametreler

- **hmac_ptr** Karma değer hesaplama için kullanılan HMAC şifre yöntemine yönelik işaretçi.
- **start_address** Veri arabelleğinin başlangıç adresi
- **end_address** Veri arabelleğinin bitiş adresi. Karma hesaplamasının bu end_address verileri kapsamadığını unutmayın.
- **anahtar** HMAC hesaplamasında kullanılan anahtar dizesi.
- **key_length** Anahtar dizesinin bayt cinsinden boyutu
- **meta veriler** HMAC algoritması tarafından kullanılan alana yönelik işaretçi.
- **metadata_size** Meta veri arabelleğinin boyutu.
- **output_buffer** Karma çıkışın depolandığı bellek konumu.
- **output_buffer_size** Çıkış arabelleğinin bayt cinsinden kullanılabilir alanı
- **actual_size** İşlev tarafından döndürülen, output_buffer yazılan gerçek bayt sayısını belirtir.

### <a name="return-values"></a>Dönüş Değerleri

- **0** Karma değeri başarıyla hesaplandı.
- **1** Karma hesaplama başarısız oldu.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Define the HMAC SHA256 method */
NX_CRYPTO_METHOD hmac_sha256 =
{
    NX_CRYPTO_AUTHENTICATION_HMAC_SHA2_256,    /* HMAC SHA256 algorithm  */
    0,                                         /* Key size, not used     */
    0,                                         /* IV size, not used      */
    NX_CRYPTO_HMAC_SHA256_ICV_FULL_LEN_IN_BITS,/* Transmitted ICV size   */
    NX_CRYPTO_SHA2_BLOCK_SIZE_IN_BYTES,        /* Block size in bytes    */
    sizeof(NX_CRYPTO_SHA256_HMAC),             /* Metadata size in bytes */
    _nx_crypto_method_hmac_sha256_init,        /* HMAC SHA256 init       */
    _nx_crypto_method_hmac_sha256_cleanup,     /* HMAC SHA256 cleanup    */
    _nx_crypto_method_hmac_sha256_operation    /* HMAC SHA256 operation  */
};

/* Define the hash key being used. */
const CHAR hash_key = “my hash key”;

/* Define starting address. */
UINT starting_address = 0x10000;

/* Define the ending address.
   Note that the hash computation covers the memory location
   before the ending address. */
UINT ending_address = 0x11000;

/* Declare the output buffer. */
#define OUTPUT_BUFFER_SIZE
UCHAR output_buffer[OUTPUT_BUFFER_SIZE];

UINT actual_size;

/* Declare 1K bytes of metadata buffer area. */
UCHAR metadata_buffer[1024];

/* Compute the hash value of the data between 0x10000 – 0x10FFF */
nx_secure_module_hash_compute(&hmac_sha256,
                              starting_address, ending_address,
                              hash_key, strlen(hash_key),
                              metadata_buffer, sizeof(metadata_buffer),
                              output_buffer, OUTPUT_BUFFER_SIZE, &actual_size);

/* If this function returns “0”, the hash value has been computed and is stored
   in output_buffer. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_crypto_method_self_test

## <a name="nx_secure_tls_active_certificate_set"></a>nx_secure_tls_active_certificate_set

NetX Secure TLS Oturumu için etkin kimlik sertifikasını ayarlama

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_tls_active_certificate_set(
                   NX_SECURE_TLS_SESSION *tls_session,
                   NX_SECURE_X509_CERT *certificate);
```

### <a name="description"></a>Description

Bu hizmetin bir oturum geri çağırma içinde çağrılma amacı vardır (bkz. nx_secure_tls_session_client_callback_set ve nx_secure_tls_session_server_callback_set). Daha önce başlatılmış bir NX_SECURE_X509_CERT ile çağrıldık, bu sertifika varsayılan kimlik sertifikası yerine kullanılır. Çoğu durumda sertifikanın yerel depoya eklenmiş olması gerekir (bkz. nx_secure_tls_local_certificate_add) veya TLS el sıkışması başarısız olabilir.

Bu hizmet, TLS'nin birden çok kimlik sertifikasını desteklemesine izin vermek için tasarlanmıştır. Bu, sunucunun istemcinin giriş noktası bağlı olarak uzak istemciye sağılacak uygun bir sertifika seçerek birden çok ağ adresine hizmet sağlayan bir TLS sunucusu için yararlıdır. Bir TLS istemcisi için bu yordam, sunucu TLS el sıkışması içinde kendisini belirledikten sonra çalışma zamanında uzak bir sunucuya gönderilen sertifikayı değiştirmek için kullanılabilir (bu, TLS sunucusunun kullanım örneğinden daha nadirdir).

Birden çok sertifikanın aynı X.509 ayırt edici adını paylaşması durumunda, sertifikaların sertifikadan ayrı bir sayısal tanımlayıcıyı tanıtan nx_secure_tls_server_certificate_add kullanılarak ekleniyor olması gerekir.

### <a name="parameters"></a>Parametreler

- **session_ptr** Oturum geri çağırmaya geçirilen BIR TLS Oturumu örneğinin işaretçisi.
- **sertifika** Geçerli oturum için kullanılacak, başlatılan bir X.509 sertifikasının işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Sertifikanın oturuma başarıyla ataması.
- **NX_PTR_ERROR** (0x07) Geçersiz TLS oturumu veya sertifika işaretçisi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
#define TLS_SNI_SERVER_NAME “www.example.com”
#define TLS_DEFAULT_SERVER_CERT_ID 2
#define TLS_EXAMPLE_CERT_ID 3


/* Callback for ClientHello extensions processing. */
static ULONG tls_server_callback(NX_SECURE_TLS_SESSION *tls_session,
                                 NX_SECURE_TLS_HELLO_EXTENSION *extensions,
                                 UINT num_extensions)
{
NX_SECURE_X509_DNS_NAME dns_name;
INT compare_value;
UINT status;
NX_SECURE_X509_CERT *cert_ptr;

    /* Grab a pointer to our default certificate in case the SNI extension is not
       available or the specified server name is unknown. */
    nx_secure_tls_server_certificate_find(tls_session, &cert_ptr,
                                     TLS_DEFAULT_SERVER_CERT_ID);


    /* Process Server Name Indication extension. */
    status = _nx_secure_tls_session_sni_extension_parse(tls_session, extensions,
                                                    num_extensions, &dns_name);

    /* If no extension found, that is OK. Use default certificate. */
    if(status == NX_SUCCESS)
    {
          /* SNI extension found, select an active certificate based on the server
             name. */

          /* Make sure our SNI name matches. */
          compare_value = memcmp(dns_name.nx_secure_x509_dns_name,
                                TLS_SNI_SERVER_NAME, strlen(TLS_SNI_SERVER_NAME));

          if(compare_value == 0 && dns_name.nx_secure_x509_dns_name_length !=
             strlen(TLS_SNI_SERVER_NAME))
          {
             /* Found a match, find the certificate we want to use. */
             _nx_secure_tls_server_certificate_find(tls_session, &cert_ptr,
                                                      TLS_EXAMPLE_CERT_ID);
          }
          else
          {
             /* No matching server name found. The application may choose to simply
                provide the default certificate (and probably resulting in an error
                in the remote client) or returning an error here to end the
                handshake. A user-defined non-zero error code will be sufficient –
                the error code will abort the TLS handshake and be returned to the
                caller that started the server. */
                return(0x500);
          }
      }
      else
      {
      }
      /* Set the certificate we want to use. */
      nx_secure_tls_active_certificate_set(tls_session, cert_ptr);

      /* Return success to continue TLS handshake. */
      return(NX_SUCCESS);
}

/* Sockets, sessions, certificates defined in global static space to preserve
   application stack. */
NX_SECURE_TLS_SESSION server_tls_session;

/* Application where TLS session is started. */
void main()
{
    /* Create a TLS session for our socket. Ciphers and metadata defined
       elsewhere. See nx_secure_tls_session_create reference for more
       information. */
    status =  nx_secure_tls_session_create(&server_tls_session,
                                           &nx_crypto_tls_ciphers,
                                           server_crypto_metadata,
                                           sizeof(server_crypto_metadata));

    /* Check for error.  */
    if(status)
    {
        printf("Error in function nx_secure_tls_session_create: 0x%x\n", status);
    }

    /* Setup our packet reassembly buffer. See
       nx_secure_tls_session_packet_buffer_set for more information. */
    nx_secure_tls_session_packet_buffer_set(&server_tls_session,
                                      server_packet_buffer,
                                      sizeof(server_packet_buffer));


    /* Set callback for server TLS extension handling. */
    _nx_secure_tls_session_server_callback_set(&server_tls_session,
                                              tls_server_callback);

    /* Initialize our certificates – certificate data defined elsewhere. See
       section “Importing X.509 Certificates into NetX Secure” for more
       information. */
    nx_secure_x509_certificate_initialize(&default_certificate,
                                      default_cert_der,
                                      default _cert_der_len, NX_NULL, 0,
                                      default_cert_key_der,
                                      default_cert_key_der_len,
                                      NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add the certificate to the local store using a numeric ID. */
    nx_secure_tls_server_certificate_add(&server_tls_session,
                                         &default_certificate,
                                         TLS_DEFAULT_SERVER_CERT_ID);

    /* Alternative identity certificate, needs to have a private key! */
    nx_secure_x509_certificate_initialize(&example_certificate,
                                      example_cert_der,
                                      example cert_der_len, NX_NULL, 0,
                                      example_cert_key_der,
                                      example_cert_key_der_len,
                                      NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add the certificate to the local store using a numeric ID. */
    nx_secure_tls_server_certificate_add(&server_tls_session,
                                         &example_certificate,
                                         TLS_EXAMPLE_CERT_ID);

    /* Now we can start the TLS session as normal. */
       …
}
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_x509_certificate_initialize
- nx_secure_tls_local_certificate_add
- nx_secure_tls_session_client_callback_set
- nx_secure_tls_session_server_callback_set
- nx_secure_tls_server_certificate_add
- nx_secure_tls_server_certificate_find
- nx_secure_tls_server_certificate_remove

## <a name="nx_secure_tls_client_psk_set"></a>nx_secure_tls_client_psk_set

NetX güvenli TLS Istemci oturumu için önceden paylaşılan anahtar ayarlama

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_tls_client_psk_set(NX_SECURE_TLS_SESSION *session_ptr,
                              UCHAR *pre_shared_key, UINT psk_length,
                              UCHAR *psk_identity, UINT identity_length,
                              UCHAR *hint, UINT hint_length);
```

### <a name="description"></a>Description

Bu hizmet, bir TLS oturum denetim bloğuna önceden paylaşılan anahtar (PSK), kimlik dizesi ve kimlik ipucu ekler ve bu PSK 'yi sonraki TLS Istemci bağlantılarında kullanılacak şekilde ayarlar. PSK ciphersuites etkin ve kullanıldığında, bir dijital sertifika yerine PSK kullanılır.

Bu durumda, PSK, TLS Istemcisinin iletişim kurmasını istediği belirli bir uzak TLS sunucusuyla ilişkilendirilir. Bu API aracılığıyla ayarlanan PSK, sonraki TLS el sıkışması sırasında uzak TLS sunucu konağına sunulacaktır.

### <a name="parameters"></a>Parametreler

- **session_ptr** Daha önce oluşturulmuş bir TLS oturum örneğine yönelik işaretçi.
- **pre_shared_key** Gerçek PSK değeri.
- **psk_length** PSK değeri uzunluğu.
- **psk_identity** Bu PSK değerini tanımlamak için kullanılan dize.
- **identity_length** PSK kimliğinin uzunluğu.
- **İpucu** Bir TLS sunucusunda hangi sayıda PSKs arasından seçim yapmak gerektiğini göstermek için kullanılan dize.
- **hint_length** İpucu dizesinin uzunluğu.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) PSK 'nin başarılı bir şekilde eklenmesi.
- **NX_PTR_ERROR** (0x07) Geçersiz TLS oturum işaretçisi.
- **NX_SECURE_TLS_NO_MORE_PSK_SPACE** (0x125) Başka bir PSK ek olamaz.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* PSK value.  */
UCHAR psk[] = { 0x1a, 0x2b, 0x3c, 0x4d };

/* Add PSK to TLS session.  */
status =  nx_secure_tls_client_psk_set(&tls_session, psk, sizeof(psk), “psk_1”, 4,
“Client_identity”, 15);


/* If status is NX_SUCCESS the PSK was successfully added.  */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_tls_psk_add
- nx_secure_x509_certificate_initialize
- nx_secure_tls_session_create
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_local_certificate_add

## <a name="nx_secure_tls_initialize"></a>nx_secure_tls_initialize

NetX Secure TLS modülünü başlatıyor

### <a name="prototype"></a>Prototype

```C
VOID nx_secure_tls_initialize(VOID);
```

### <a name="description"></a>Description

Bu hizmet NetX Secure TLS modülünü başlatıyor. Diğer NetX Güvenli hizmetlere erişilmeden önce çağrılmaları gerekir.

### <a name="parameters"></a>Parametreler

Hiçbiri

### <a name="return-values"></a>Dönüş Değerleri

Hiçbiri

### <a name="allowed-from"></a>İzin Verilen

Başlatma, İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Initializes the TLS module. */
Nx_secure_tls_initialize();
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_tls_session_create

## <a name="nx_secure_tls_local_certificate_add"></a>nx_secure_tls_local_certificate_add

NetX Secure TLS Oturumuna yerel sertifika ekleme

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_tls_local_certificate_add(
              NX_SECURE_TLS_SESSION *session_ptr,
              NX_SECURE_X509_CERT *certificate_ptr);
```

### <a name="description"></a>Description

Bu hizmet, bir TLS NX_SECURE_X509_CERT yerel deposuna başlatılmış bir uygulama yapısı örneği ekler. Bu sertifika, TLS yığını tarafından TLS el sıkışması sırasında cihazı tanımlamak için (nx_secure_x509_certificate_initialize kullanılarak sertifika yapısının başlatılmış olması sırasında kimlik sertifikası olarak işaretlenmişse) veya TLS el sıkışması sırasında uzak ana bilgisayara sağlanan bir sertifika zincirinin parçası olarak bir sertifikayı verir olarak kullanabilir.

Aynı Ortak Ad ile birden çok yerel sertifika gerekirse, sertifikalar nx_secure_tls_server_certificate_add hizmeti kullanılarak eklenebilir (aşağıdaki uyarıya bakın). 

TLS sunucu modu için bir sertifika **gereklidir** .

Bir sertifika, TLS Istemci modu için *isteğe bağlıdır* .

> [!IMPORTANT]
> *Bu API, nx_secure_tls_server_certificate_add kullanırken aynı TLS oturumuyla kullanılmamalıdır. Sunucu sertifikası API 'SI her sertifika için benzersiz bir sayısal tanımlayıcı kullanır ve X. 509.440 ortak adına göre dizinleri nx_secure_tls_local_certificate_add. Yerel Sertifika Hizmetleri, yalnızca tek bir kimlik sertifikası kullanan uygulamalar için sayısal tanımlayıcıya uygun bir alternatif sağlar: ortak adı kullanarak, uygulamanın sayısal tanımlayıcıları izlememek zorunda olmaması gerekir.*

### <a name="parameters"></a>Parametreler

- **session_ptr** Daha önce oluşturulmuş bir TLS oturum örneğine yönelik işaretçi.
- **certificate_ptr** Başlatılmış bir TLS sertifikası örneğinin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- Sertifikanın başarılı bir şekilde eklenmesi **NX_SUCCESS** (0x00).
- **NX_INVALID_PARAMETERS** (0x4D) geçersiz veya yinelenen bir sertifika eklemeye çalıştı.
- **NX_PTR_ERROR** (0x07) geçersiz TLS oturumu veya sertifika işaretçisi.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Initialize certificate structure. */
status =  nx_secure_x509_certificate_initialize(&certificate, certificate_data,
500, private_key, 64);

/* Add certificate to TLS session.  */
status =  nx_secure_tls_local_certificate_add(&tls_session, &certificate);


/* If status is NX_SUCCESS the certificate was successfully added.  */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_x509_certificate_initialize
- nx_secure_tls_session_create
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_local_certificate_remove
- nx_secure_tls_local_certificate_find

## <a name="nx_secure_tls_local_certificate_find"></a>nx_secure_tls_local_certificate_find

Ortak ad ile bir NetX güvenli TLS oturumunda yerel bir sertifika bulun

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_tls_local_certificate_find(NX_SECURE_TLS_SESSION
                        *session_ptr, NX_SECURE_X509_CERT
                        **certificate, UCHAR *common_name, UINT
                        name_length);
```

### <a name="description"></a>Description

Bu hizmet, bir TLS oturumunun yerel cihaz sertifika deposundaki bir sertifikayı bulur ve depodaki NX_SECURE_X509_CERT yapısına bir işaretçi döndürür. Common_name parametresi ve uzunluğu (name_length), sertifikanın X. 509.440 konusunun ortak ad alanıyla eşleşen sertifikayı tanımlamak için kullanılır.

Aynı ortak ada sahip birden fazla sertifika varsa, yalnızca ilki döndürülür – bunun yerine *nx_secure_tls_server_certificate_find* kullanın.

> [!IMPORTANT]
> *Bu API, uygulama kullanılırken aynı TLS oturumuyla nx_secure_tls_server_certificate_add. Sunucu sertifikası API'si her sertifika için benzersiz bir sayısal tanımlayıcı kullanır nx_secure_tls_local_certificate_add X.509 Ortak Adını temel alan dizinleri kullanır. Yerel sertifika hizmetleri, yalnızca tek bir kimlik sertifikası kullanan uygulamalar için sayısal tanımlayıcıya uygun bir alternatif sağlar. Ortak Ad'ı kullanarak uygulamanın sayısal tanımlayıcıları izlemesi gerekli değildir.*

### <a name="parameters"></a>Parametreler

- **session_ptr** Daha önce oluşturulmuş bir TLS Oturumu örneğinin işaretçisi.
- **sertifika** İşaretçiyi, eşlene sertifikaya geri dön.
- **common_name** Eşecek Ortak Ad dizesi (DNS adı).
- **name_length** Dize common_name uzunluğu.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Sertifika bulundu ve işaretçi "certificate" parametresinde döndürüldü.
- **NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) Sağlanan Ortak Ad ile sertifika bulunamadı.
- **NX_PTR_ERROR** (0x07) Geçersiz TLS oturumu, sertifika işaretçisi veya ortak ad dizesi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
NX_SECURE_X509_CERT *certificate_ptr;

/* Initialize certificate structure. */
status =  nx_secure_x509_certificate_initialize(&certificate, certificate_data,
500, private_key, 64);

/* Add certificate to TLS session.  */
status =  nx_secure_tls_local_certificate_add(&tls_session, &certificate);


/* If status is NX_SUCCESS the certificate was successfully added.  */

status = nx_secure_tls_local_certificate_find(&tls_session, &certificate_ptr,
                                      “common name”, strlen(“common name”));

/* If status is NX_SUCCESS the variable “certificate_ptr” points to a certificate
   structure containing a certificate with the Common Name “common name”. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_x509_certificate_initialize
- nx_secure_tls_session_create
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_local_certificate_remove
- nx_secure_tls_local_certificate_add

## <a name="nx_secure_tls_local_certificate_remove"></a>nx_secure_tls_local_certificate_remove

NetX Secure TLS Oturumundan yerel sertifikayı kaldırma

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_tls_local_certificate_remove(NX_SECURE_TLS_SESSION
                  *session_ptr, UCHAR *common_name, UINT
                  common_name_length);
```

### <a name="description"></a>Description

Bu hizmet, sertifikadaki Ortak Ad alanına anahtarlanan bir TLS oturumundan yerel sertifika örneğini kaldırır.

> [!IMPORTANT]
> *Bu API, uygulama kullanılırken aynı TLS oturumuyla nx_secure_tls_server_certificate_add. Sunucu sertifikası API'si her sertifika için benzersiz bir sayısal tanımlayıcı kullanır nx_secure_tls_local_certificate_add X.509 Ortak Adını temel alan dizinleri kullanır. Yerel sertifika hizmetleri, yalnızca tek bir kimlik sertifikası kullanan uygulamalar için sayısal tanımlayıcıya uygun bir alternatif sağlar. Ortak Ad'ı kullanarak uygulamanın sayısal tanımlayıcıları izlemesi gerekli değildir.*

### <a name="parameters"></a>Parametreler

- **session_ptr** Daha önce oluşturulmuş bir TLS oturum örneğine yönelik işaretçi.
- **common_name** Kaldırılacak sertifikanın ortak ad değeri.
- **common_name_length** Ortak ad dizesinin uzunluğu.

### <a name="return-values"></a>Dönüş Değerleri

- Sertifikanın başarılı bir şekilde eklenmesi **NX_SUCCESS** (0x00).
- **NX_PTR_ERROR** (0x07) geçersiz TLS oturum işaretçisi.
- **NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) sertifikası bulunamadı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Add certificate to TLS session.  */
status =  nx_secure_tls_local_certificate_remove(&tls_session,
                                                “www.example.com”, 15);


/* If status is NX_SUCCESS the certificate was successfully removed.  */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_x509_certificate_initialize
- nx_secure_tls_session_create
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_local_certificate_add

## <a name="nx_secure_tls_metadata_size_calculate"></a>nx_secure_tls_metadata_size_calculate

NetX güvenli TLS oturumunun şifreleme meta verilerinin boyutunu hesaplama

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_tls_metadata_size_calculate(
                        const NX_SECURE_TLS_CRYPTO *crypto_table,
                        ULONG *metadata_size);
```

### <a name="description"></a>Description

Bu hizmet, belirli bir TLS oturumu ve TLS şifreleme tablosu için gereken şifreleme meta verilerinin boyutunu hesaplar ve döndürür (şifreleme şifresi tablosu hakkında daha fazla bilgi için "şifreleme yöntemleriyle TLS başlatılıyor" bölümüne bakın.

Bu hizmet, nx_secure_tls_session_create iletilen meta veri arabelleğinin boyutunu hesaplamak için istenen şifreleme tablosuyla çağrılmalıdır.

### <a name="parameters"></a>Parametreler

- **crypto_table** Tüm NetX güvenli TLS şifreleme tablosuna yönelik işaretçi.
- **metadata_size** Bayt cinsinden boyut hesaplamasının çıktısı.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) meta veri boyutunun başarıyla hesaplanması.
- **NX_PTR_ERROR** (0x07) geçersiz şifre tablosu veya dönüş boyutu işaretçisi.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Pointer to the platform-specific cipher table. */
extern nx_crypto_tls_ciphers;

/* Return variable for metadata size. */
ULONG crypto_metadata_size;

/* Calculate metadata size.  */
status =  nx_secure_tls_metadata_size_calculate(&nx_crypto_tls_ciphers,
                                                &crypto_metadata_size);


/* If status is NX_SUCCESS then crypto_metadata_size contains the size of the
   metadata buffer for the table nx_crypto_tls_ciphers.  */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_tls_session_create

## <a name="nx_secure_tls_packet_allocate"></a>nx_secure_tls_packet_allocate

NetX Güvenli TLS Oturumu için paket ayırma

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_tls_packet_allocate(NX_SECURE_TLS_SESSION *session_ptr,
                                    NX_PACKET_POOL *pool_ptr,
                                    NX_PACKET **packet_ptr,
                                    ULONG wait_option);
```

### <a name="description"></a>Description

Bu hizmet, belirtilen NX_PACKET TLS oturumu için belirtilen oturumdan bir NX_PACKET_POOL. Bu hizmet, bir TLS bağlantısı üzerinden gönderilecek veri paketlerini ayırmak için uygulama tarafından çağrılmalı. Bu hizmet çağrılmadan önce TLS oturumunun başlatılması gerekir.

Ayrılan paket düzgün şekilde başlatılır, böylece paket verileri doldurulduğunda TLS üst bilgisi ve alt bilgi verileri eklenebilir. Aksi takdirde davranış, ile *nx_packet_allocate.*

### <a name="parameters"></a>Parametreler

- **session_ptr** TLS Oturumu örneğinin işaretçisi.
- **pool_ptr** Paketin ayrıl NX_PACKET_POOL bir uygulamanın işaretçisi.
- **packet_ptr** Yeni ayrılan paketin çıkış işaretçisi.
- **wait_option** Paket ayırma için askıya alma seçeneği.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı paket ayırma.
- **NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) Temel paket ayırma başarısız oldu.
- **NX_SECURE_TLS_SESSION_UNINITIALIZED** (0x101) Sağlanan TLS oturumu başlatılmadı.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Allocate a new TLS packet from the previously created packet pool and
previously initialized TLS session.   */

status = nx_secure_tls_packet_allocate(&tls_session, &pool_0, &packet_ptr,
                                       NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the newly allocated packet pointer is found in the
variable packet_ptr.  */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_socket_receive
- nx_secure_x509_certificate_initialize
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_session_start
- nx_secure_tls_session_delete
- nx_secure_tls_session_receive
- nx_secure_tls_session_send
- nx_secure_tls_session_end
- nx_secure_tls_session_create

## <a name="nx_secure_tls_psk_add"></a>nx_secure_tls_psk_add

NetX güvenli TLS oturumuna önceden paylaşılan anahtar ekleme

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_tls_psk_add(NX_SECURE_TLS_SESSION *session_ptr,
                            UCHAR *pre_shared_key, UINT psk_length,
                            UCHAR *psk_identity, UINT
                            identity_length, UCHAR *hint, UINT
                            hint_length);
```

### <a name="description"></a>Description

Bu hizmet, bir TLS oturum denetim bloğuna önceden paylaşılan anahtar (PSK), kimlik dizesi ve kimlik ipucu ekler. PSK ciphersuites etkin ve kullanıldığında, bir dijital sertifika yerine PSK kullanılır.

### <a name="parameters"></a>Parametreler

- **session_ptr** Daha önce oluşturulmuş bir TLS oturum örneğine yönelik işaretçi.
- **pre_shared_key** Gerçek PSK değeri.
- **psk_length** PSK değeri uzunluğu.
- **psk_identity** Bu PSK değerini tanımlamak için kullanılan dize.
- **identity_length** PSK kimliğinin uzunluğu.
- **İpucu** Bir TLS sunucusunda hangi sayıda PSKs arasından seçim yapmak gerektiğini göstermek için kullanılan dize.
- **hint_length** İpucu dizesinin uzunluğu.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) PSK 'nin başarılı bir şekilde eklenmesi.
- **NX_PTR_ERROR** (0x07) geçersiz TLS oturum işaretçisi.
- **NX_SECURE_TLS_NO_MORE_PSK_SPACE** (0x125) başka bir PSK eklenemiyor.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* PSK value.  */
UCHAR psk[] = { 0x1a, 0x2b, 0x3c, 0x4d };

/* Add PSK to TLS session.  */
status =  nx_secure_tls_psk_add(&tls_session, psk, sizeof(psk), “psk_1”, 4,
“Client_identity”, 15);


/* If status is NX_SUCCESS the PSK was successfully added.  */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_tls_client_psk_set
- nx_secure_x509_certificate_initialize
- nx_secure_tls_session_create
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_local_certificate_add

## <a name="nx_secure_tls_remote_certificate_allocate"></a>nx_secure_tls_remote_certificate_allocate

Uzak bir TLS ana bilgisayarı tarafından sağlanan sertifika için alan ayırma

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_tls_remote_certificate_allocate(
                 NX_SECURE_TLS_SESSION *session_ptr,
                 NX_SECURE_X509_CERT *certificate_ptr,
                 UCHAR *raw_certificate_buffer,
                 UINT raw_buffer_size);
```

### <a name="description"></a>Description

Bu hizmet, TLS oturumu NX_SECURE_X509_CERT uzak konak tarafından sağlanan sertifikalar için alan ayrım yapmak amacıyla bir TLS oturumuna başlatlanmamış bir NX_SECURE_X509_CERT yapısı örneği ekler. Uzak sertifika verileri NetX Secure TLS tarafından ayrıştırıldı ve bu bilgiler bu işleve sağlanan sertifika yapısı örneğini doldurmak için kullanılır. Bu şekilde eklenen sertifikalar bağlantılı bir listeye yerleştirilir.

Uzak ana bilgisayarın birden çok sertifika sağlaması bekleniyorsa, tüm sertifikalar için alan ayırmak için bu işlev tekrar tekrar çağrılır. Ek sertifikalar, sertifika bağlantılı listesinin sonuna eklenir.

Uzak sertifikanın ayrılamaz olması, ÖNCEDEN Paylaşılan Anahtar (PSK) şifrelemesi kullandıkça TLS İstemci modunun TLS el sıkışması sırasında başarısız olmasına neden olur.

Bu *raw_certificate_buffer* parametresi, gelen uzak sertifikayı depolamak için ayrılan alanı belirtir. İmzalar için SHA-256 kullanan 2048 bit RSA anahtarları olan tipik sertifikalar 1000-2000 bayt aralığındadır. Arabellek en azından bu boyutu tutacak kadar büyük olmalı, ancak uzak konak sertifikalara bağlı olarak önemli ölçüde daha küçük veya daha büyük olabilir. Arabellek gelen sertifikayı tutmayacak kadar küçükse TLS el sıkışması bir hatayla sona erer.

TLS Sunucusu modu için, uzak sertifika ayırma yalnızca istemci sertifikası kimlik doğrulaması etkinse gereklidir.

### <a name="parameters"></a>Parametreler

- **session_ptr** Daha önce oluşturulmuş bir TLS Oturumu örneğinin işaretçisi.
- **certificate_ptr** Uninitialized X.509 Sertifika örneğinin işaretçisi.
- **raw_certificate_buffer** Uzak ana bilgisayardan alınan ayrıştırılmamış sertifikayı tutan bir arabellek işaretçisi.
- **raw_buffer_size** Ham sertifika arabelleğinin boyutu.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) sertifikanın başarıyla ayrılması.
- **NX_PTR_ERROR** (0x07) geçersiz TLS oturum işaretçisi.
- **NX_SECURE_TLS_INSUFFICIENT_CERT_SPACE** (0x12D) sağlanan arabellek çok küçük.
- **NX_INVALID_PARAMETERS** (0x4D) geçersiz bir sertifika eklemeye çalıştı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Certificate control block. */
NX_SECURE_X509_CERT certificate;

/* Buffer space to hold the incoming certificate. */
UCHAR certificate_buffer[2000];

/* Add certificate to TLS session.  */
status =  nx_secure_tls_remote_certificate_allocate(&tls_session, &certificate,
                                                    certificate_buffer,
                                                    sizeof(certificate_buffer));


/* If status is NX_SUCCESS the certificate was successfully allocated.  */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_x509_certificate_initialize,
- nx_secure_tls_session_create

## <a name="nx_secure_tls_remote_certificate_buffer_allocate"></a>nx_secure_tls_remote_certificate_buffer_allocate

Uzak bir TLS ana bilgisayarı tarafından belirtilen tüm sertifikalar için alan ayır

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_tls_remote_certificate_buffer_allocate(
                  NX_SECURE_TLS_SESSION *session_ptr,
                  UINT certs_number, VOID *certificate_buffer,
                  ULONG buffer_size);
```

### <a name="description"></a>Description

Bu hizmet, bir TLS Istemci örneğinde X. 509.440 kimlik doğrulaması ve doğrulama gerçekleştirmek için uzak sunucu konaklarından gelen sertifika zincirlerini işlemek üzere alan ayırır. TLS sunucu modu için, uzak sertifika ayırma yalnızca Client X. 509.440 sertifikası kimlik doğrulaması etkinse gereklidir – TLS sunucu örnekleri için, bunun yerine hizmet *nx_secure_tls_session_x509_client_verify_configure* kullanılmalıdır.

Bir önceden paylaşılan anahtar (PSK) ciphersuite kullanımda değilse, uzak sertifikaları ayıramaması TLS Istemci modunun TLS el sıkışması sırasında başarısız olmasına neden olur.

*Certificate_buffer* parametresi, gelen uzak sertifikaları ve bu sertifikalar için gereken denetim bloklarını depolamak için ayrılan alana işaret eder. Arabellek, her sertifikaya verilen eşit bir bölüme sahip sertifika (*certs_number*) sayısına bölünür. *Buffer_size* parametresi arabelleğin boyutunu gösterir. Aşağıdaki formül ile, gereken alan bulunabilir:

```C
buffer_size = (<expected max number of certificates in chain>) *
                 (sizeof(NX_SECURE_X509_CERT) + <max cert size>)
```

İmzalar için SHA-256 kullanan 2048 bitin RSA anahtarlarına sahip tipik sertifikalar, 1000-2000 bayt aralığındadır. Arabellek, her sertifika için en az sayıda tutmaya yetecek kadar büyük olmalıdır, ancak uzak ana bilgisayar sertifikalarına bağlı olarak, önemli ölçüde daha küçük veya daha büyük olabilir. Arabellek gelen sertifikayı tutmayacak kadar küçükse TLS el sıkışması bir hatayla sona erer.

### <a name="parameters"></a>Parametreler

- **session_ptr** Daha önce oluşturulmuş bir TLS Oturumu örneğinin işaretçisi.
- **certs_number** Sağlanan arabellekten ayrılacak sertifika sayısı.
- **certificate_buffer** Uzak bir konaktan alınan sertifikaları tutmak için bir arabelleğe işaretçi.
- **buffer_size** Sertifika arabelleğinin boyutu.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Sertifikanın başarıyla tahsisi.
- **NX_PTR_ERROR** (0x07) Geçersiz TLS oturumu veya arabellek işaretçisi.
- **NX_SECURE_TLS_INSUFFICIENT_CERT_SPACE** (0x12D) Sağlanan arabellek çok küçüktü.
- **NX_INVALID_PARAMETERS** (0x4D) Arabellek istenen sayıda sertifikayı tutmak için çok küçüktü.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Buffer space to hold the incoming certificates. */
#define CERTIFICATE_NUMBER    (2)
#define CERTIFICATE_SIZE      (2000)
#define BUFFER_SIZE           (CERTIFICATE_NUMBER * \
                              (sizeof(NX_SECURE_X509_CERT) + CERTIFICATE_SIZE))
UCHAR certificate_buffer[BUFFER_SIZE];

/* Add certificate to TLS session.  */
status =  nx_secure_tls_remote_certificate_buffer_allocate(&tls_session,
                                                      CERTIFICATE_NUMBER,
                                                      certificate_buffer,
                                                      BUFFER_SIZE);


/* If status is NX_SUCCESS the buffer was successfully allocated.  */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_x509_certificate_initialize
- nx_secure_tls_session_create

## <a name="nx_secure_tls_remote_certificate_free_all"></a>nx_secure_tls_remote_certificate_free_all

Gelen sertifikalar için ayrılan boş alan

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_tls_remote_certificate_free_all(
                  NX_SECURE_TLS_SESSION *session_ptr);
```

### <a name="description"></a>Description

Bu hizmet, belirli bir TLS Oturumuna ayrılmış olan tüm sertifika arabelleklerini nx_secure_tls_remote_certificate_allocated oturumun boş sertifika alanlarına döndürerek bu arabellekleri serbest bırakarak kullanılabilir. Bu, bir uygulamanın tlS oturum nesnesini silmeden yeniden kullanması ve bir tls ile yeniden oluşturması nx_secure_tls_session_delete nx_secure_tls_session_create.

TLS oturumu oturumda olduğu gibi sıfırlanır ve bu nedenle çoğu uygulamanın bu hizmeti nx_secure_tls_session_end uzak sertifika alanı otomatik olarak kurtarılır.

### <a name="parameters"></a>Parametreler

- **session_ptr** Daha önce oluşturulmuş bir TLS Oturumu örneğinin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı işlem.
- **NX_PTR_ERROR** (0x07) Geçersiz TLS oturum işaretçisi.
- **NX_INVALID_PARAMETERS** (0x4D) iç hata – sertifika deposu muhtemelen bozuk.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Certificate control block. */
NX_SECURE_X509_CERT certificate;

/* Buffer space to hold the incoming certificate. */
UCHAR certificate_buffer[2000];

/* Add certificate to TLS session.  */
status =  nx_secure_tls_remote_certificate_allocate(&tls_session, &certificate,
                                                    certificate_buffer,
                                                    sizeof(certificate_buffer));


/* If status is NX_SUCCESS the certificate was successfully allocated.  */

/* … TLS session setup, TCP connection, etc… */

/* End TLS session. */
nx_secure_tls_session_end(&tls_session, NX_WAIT_FOREVER);

/* Free up certificate buffers for next connection. */
nx_secure_tls_remote_certificate_free_all(&tls_session);
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_x509_certificate_initialize
- nx_secure_tls_session_create
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_session_end

## <a name="nx_secure_tls_server_certificate_add"></a>nx_secure_tls_server_certificate_add

Sayısal bir tanımlayıcı kullanarak TLS sunucuları için özel olarak bir sertifika ekleyin

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_tls_server_certificate_add(
                  NX_SECURE_TLS_SESSION *session_ptr,
                  NX_SECURE_X509_CERT *certificate, UINT cert_id);
```

### <a name="description"></a>Description

Bu hizmet, bir TLS oturumunun yerel deposuna bir sertifika eklemek için kullanılır (bkz. nx_secure_tls_local_certificate_add) sertifikanın içindeki X. 509.952 Subject (ortak ad) kullanarak depoyu dizinlemek yerine bir sayısal tanımlayıcı kullanarak. Sayısal tanımlayıcı sertifikadan ayrıdır ve birden çok sertifikanın bir TLS sunucusuna kimlik sertifikası olarak eklenmesine izin verir, ayrıca aynı ortak ada sahip birden çok sertifikanın aynı TLS oturumu yerel deposuna eklenmesine izin verir. Aynı hizmet istemci sertifikaları için kullanılabilir, ancak bir TLS istemcisinde birden çok kimlik sertifikası olması nadir bir durumdur.

Cert_id parametresi, uygulama tarafından atanan sıfır olmayan pozitif bir tamsayıdır. Gerçek değer (sıfırdan farklı) değil, ancak belirtilen TLS oturumunun deposunda benzersiz olması gerekir. Cert_id değeri, sırasıyla nx_secure_tls_server_certificate_find ve nx_secure_tls_server_certificate_remove kullanılarak yerel depodan sertifika bulmak ve kaldırmak için kullanılabilir.

> [!IMPORTANT]
> *Bu API, nx_secure_tls_local_certificate_add kullanırken aynı TLS oturumuyla kullanılmamalıdır. Nx_secure_tls_server_certificate_add API 'SI her sertifika için benzersiz bir sayısal tanımlayıcı ve X. 509.440 ortak adına göre yerel sertifika hizmetleri dizini kullanır. Sunucu sertifikası Hizmetleri, aynı yerel depoda paylaşılan verileri olan birden çok sertifikanın (özellikle ortak ad) bulunmasına izin verir. Bu, birden çok kimliği olan bir sunucu için faydalıdır.*

### <a name="parameters"></a>Parametreler

- **session_ptr** Daha önce oluşturulmuş bir TLS oturum örneğine yönelik işaretçi.
- **sertifika** Daha önce başlatılmış bir X. 509.440 sertifika örneğine yönelik işaretçi.
- **cert_id** Pozitif, sıfır olmayan, görece benzersiz sertifika kimliği numarası.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00)Başarılı işlem.
- **NX_PTR_ERROR** (0x07) Geçersiz TLS oturumu veya sertifika işaretçisi.
- **NX_SECURE_TLS_CERT_ID_INVALID** (0x138) Sağlanan sertifika kimliğinin Geçersiz bir değeri vardı (büyük olasılıkla 0).
- **NX_SECURE_TLS_CERT_ID_DUPLICATE** (0x139) Sağlanan sertifika kimliği yerel depoda zaten mevcut.
- **NX_INVALID_PARAMETERS(0x4D)** İç hata – sertifika deposu büyük olasılıkla bozuk.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Certificate control block. */
NX_SECURE_X509_CERT certificate;


/* Add certificate to TLS session.  */
status =  nx_secure_tls_server_certificate_add(&tls_session, &certificate, 0x12);


/* If status is NX_SUCCESS the certificate was successfully added with the ID
0x12.  */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_x509_certificate_initialize
- nx_secure_tls_local_certificate_add
- nx_secure_tls_active_certificate_set
- nx_secure_tls_server_certificate_find
- nx_secure_tls_server_certificate_remove

## <a name="nx_secure_tls_server_certificate_find"></a>nx_secure_tls_server_certificate_find

Sayısal tanımlayıcı kullanarak sertifika bulma

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_tls_server_certificate_find(
                  NX_SECURE_TLS_SESSION *session_ptr,
                  NX_SECURE_X509_CERT **certificate, UINT cert_id);
```

### <a name="description"></a>Description

Bu hizmet, sertifika içindeki X.509 Konu (Ortak Ad) kullanarak depo dizini oluşturma yerine sayısal tanımlayıcı kullanarak TLS oturumunun yerel depolama (bkz. nx_secure_tls_local_certificate_add) içinde bir sertifika bulmak için kullanılır.

Cert_id parametresi, sertifika tlS oturumu yerel deposuna kullanılarak ekleniyorsa uygulama tarafından atanan sıfır olmayan bir pozitif tamsayıdır nx_secure_tls_server_certificate_add.

> [!IMPORTANT]
> *Bu API, uygulama kullanılırken aynı TLS oturumuyla nx_secure_tls_local_certificate_add. Uygulama nx_secure_tls_server_certificate_add API'si, her sertifika için benzersiz bir sayısal tanımlayıcı ve X.509 Ortak Adı'nın temel alınan yerel sertifika hizmetleri dizinini kullanır. Sunucu sertifika hizmetleri, paylaşılan verilere sahip birden çok sertifikanın (özellikle Ortak Ad) aynı yerel depoda var olmasına olanak sağlar. Bu, birden çok kimli sunucu için yararlıdır.*

### <a name="parameters"></a>Parametreler

- **session_ptr** Daha önce oluşturulmuş bir TLS Oturumu örneğinin işaretçisi.
- **sertifika** Bulunan sertifikaya başvuru dönmek için X.509 sertifika işaretçisinin işaretçisi.
- **cert_id** Sıfır olmayan pozitif sertifika kimliği değeri.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı işlemi.
- **NX_PTR_ERROR** (0x07) geçersiz TLS oturumu veya sertifika işaretçisi.
- **NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) BELIRTILEN sertifika kimliği, belirtilen TLS oturumunun yerel deposundaki herhangi bir hiçbiriyle eşleşmedi.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
NX_SECURE_X509_CERT *certificate;


/* Find certificate in TLS session.  */
status =  nx_secure_tls_server_certificate_find(&tls_session, &certificate, 0x12);


/* If status is NX_SUCCESS the certificate was successfully found and a reference
returned in the certificate parameter.  */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_x509_certificate_initialize
- nx_secure_tls_local_certificate_add
- nx_secure_tls_active_certificate_set
- nx_secure_tls_server_certificate_add
- nx_secure_tls_server_certificate_remove

##  <a name="nx_secure_tls_server_certificate_remove"></a>nx_secure_tls_server_certificate_remove

Sayısal tanımlayıcıyı kullanarak yerel sunucu sertifikasını kaldırma

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_tls_server_certificate_remove(
                  NX_SECURE_TLS_SESSION *session_ptr, UINT cert_id);
```

### <a name="description"></a>Description

Bu hizmet, bir sertifikayı bir TLS oturumunun yerel deposundan kaldırmak için kullanılır (bkz. nx_secure_tls_local_certificate_add) sertifikanın içindeki X. 509.952 Subject (ortak ad) kullanarak depoyu dizinlemek yerine sayısal bir tanımlayıcı kullanarak.

Cert_id parametresi, sertifika, nx_secure_tls_server_certificate_add kullanılarak TLS oturumu yerel deposuna eklendiğinde, uygulama tarafından atanan sıfır olmayan pozitif bir tamsayıdır.

### <a name="parameters"></a>Parametreler

- **session_ptr** Daha önce oluşturulmuş bir TLS oturum örneğine yönelik işaretçi.
- **cert_id** Sıfır olmayan pozitif sertifika KIMLIĞI değeri.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı işlemi.
- **NX_PTR_ERROR** (0x07) geçersiz TLS oturumu.
- **NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) BELIRTILEN sertifika kimliği, belirtilen TLS oturumunun yerel deposundaki herhangi bir hiçbiriyle eşleşmedi.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Certificate control block. */
NX_SECURE_X509_CERT certificate;


/* Add certificate to TLS session with id 0x12.  */
status =  nx_secure_tls_server_certificate_add(&tls_session, &certificate, 0x12);
/* Use certificate in TLS session, etc… */

/* Remove certificate from TLS session with id 0x12.  */
status =  nx_secure_tls_server_certificate_remove(&tls_session, 0x12);


/* If status is NX_SUCCESS the certificate was successfully removed.  */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_x509_certificate_initialize
- nx_secure_tls_local_certificate_add
- nx_secure_tls_active_certificate_set
- nx_secure_tls_server_certificate_add
- nx_secure_tls_server_certificate_find

## <a name="nx_secure_tls_session_alert_value_get"></a>nx_secure_tls_session_alert_value_get

Uzak konak tarafından gönderilen TLS uyarı değerini ve düzeyini al

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_tls_session_alert_value_get(
                   NX_SECURE_TLS_SESSION *session_ptr,
                   UINT *alert_level, UINT *alert_value);
```

### <a name="description"></a>Description

Bu hizmet, uzak konak bir soruna veya hataya yanıt olarak uyarı gönderdiğinde TLS uyarı düzeyini ve değerini almak için kullanılır.

alert_level ve alert_value parametrelerinin değerleri yalnızca bu işlev, uzak konaktan bir uyarı alınarak uyarı alınarak NX_SECURE_TLS_ALERT_RECEIVED (0x114) durumu döndürülen bir TLS API çağrısından hemen sonra çağrılsa geçerlidir.

Yerel ana bilgisayar TLS bir uyarı gönderirse, TLS uyarı değerleri belirli saldırı türlerini (örneğin, "doldurma kahini" saldırısı veya benzeri) önlemek için kasıtlı olarak belirsiz bırakılana kadar, döndürülen hata kodları gerçek hatayı TLS uyarısının kendisine göre çok daha açıklayıcıdır.

Uyarı düzeyi yalnızca iki değerden birini alır: NX_SECURE_TLS_ALERT_LEVEL_WARNING (0x1) veya NX_SECURE_TLS_ALERT_LEVEL_FATAL (0x2). Bazı uzantı yapılandırma durumlarında uyarı olarak da düşünülebilir ancak genel olarak yalnızca CloseNotify Uyarısına (TLS oturumunun başarılı bir şekilde son verildiğini belirtmek için kullanılır) "Uyarı" düzeyi verilir. Uyarıların büyük çoğunluğu olası bir güvenlik hatasına işaret eden "Önemli" olur ve TLS bağlantısının (el sıkışma veya oturum) hemen kapatılmasına neden olur.

TLS uyarı değerleri TLS RFC'lerde tanımlanmıştır; rfc 5246 (TLSv1.2) listesinden başvuru için:

| Uyarı Adı                     | Değer | Açıklama                                                                                                                                                  |
| ---------------------------------- | --------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| close_notify                  | 0     | Hata yok, oturum sonunun başarılı olduğunu gösteriyor                                                                                                                   |
| unexpected_message            | 10    | TLS beklenmeyen veya sıranın dışında iletisi aldı                                                                                                           |
| bad_record_mac               | 20    | Şifre çözme ve/veya MAC doğrulaması başarısız oldu                                                                                                                    |
| decryption_failed_RESERVED   | 21    | **Kullanım dışı** Şifre çözme başarısız oldu (Oracle saldırılarını doldurma nedeniyle kullanım dışı)                                                                                      |
| record_overflow               | 22    | En fazla TLS kayıt boyutundan daha büyük olan bir kayıt alındı                                                                                        |
| decompression_failure         | 30    | TLS kaydının sıkıştırılması/sıkıştırması açılmasında bir sorunla karşılaşıldı                                                                                       |
| handshake_failure             | 40    | Farklı bir uyarı kapsamında olmayan bazı belirtilmeyen bir el sıkışma hatası oluştu                                                                            |
| no_certificate_RESERVED      | 41    | TLS 'de **kullanım dışı** (yalnızca SSL)                                                                                                                                 |
| bad_certificate               | 42    | Alınan bir sertifika geçersiz biçimlendirme veya imza içeriyordu                                                                                   |
| unsupported_certificate       | 43    | Geçersiz bir tür (örneğin, TLS sunucu kimlik doğrulaması için kullanılan yalnızca oturum açma sertifikası) olan bir sertifika alındı                                    |
| certificate_revoked           | 44    | Sertifika durumu (bir CRL veya OCSP tarafından sağlandığı gibi) "iptal edildi" olarak belirtilmiştir                                                                       |
| certificate_expired           | 45    | Alınan sertifika geçerli bir tarih aralığı dışındaydı (henüz geçerli değil veya kullanım tarihi belirtilmemiş)                                                                 |
| certificate_unknown           | 46    | Diğer uyarıların kapsamadığı bilinmeyen bir sertifika sorunuyla karşılaşıldı                                                                          |
| illegal_parameter             | 47    | TLS el sıkışması içinde bazı yapılandırma veya anlaşmalı değer geçersiz veya aralık dışında                                                                      |
| unknown_ca                    | 48    | Alınan kimlik sertifikası, güvenilen bir kök CA sertifikasına bir sertifika zinciri aracılığıyla izlenmedi.                                              |
| access_denied                 | 49    | Geçerli bir sertifikanın alınmıştır ancak uygulama erişim denetimi, istenen kaynaklar için sertifikanın geçersiz olduğunu gösterir.            |
| decode_error                  | 50    | TLS üst bilgisinde veya el sıkışma iletisinde yer alan bir alan veya değer aralık dışında veya geçersizdi ve bu da TLS kaydının kodunun çözülerek hataya neden oldu.                      |
| decrypt_error                 | 51    | TLS el sıkışması sırasında bir imza veya Tamamlandı ileti karması doğrulanamadı.                                                                         |
| export_restriction_RESERVED  | 60    | TLSv1.2'de KULLANıM DıŞı                                                                                                                                        |
| protocol_version              | 70    | El sıkışma sırasında anlaştırılacak TLS protokol sürümü tanınıyor ancak desteklenmiyor (örneğin TLSv1.0 sunulsa da etkinleştirilmedi).                       |
| insufficient_security         | 71    | Güvenli şifrelemelerin olmaması nedeniyle el sıkışması başarısız olduğunda gönderilir (örneğin, anahtar boyutu uygulama gereksinimleri için çok küçüktür)                                |
| internal_error                | 80    | TLS olmayan bazı hata (örneğin bellek ayırma sorunları, uygulama sorunları) bir TLS oturumunun bozuk olarak ortaya çıktı.                                         |
| user_canceled                 | 90    | El sıkışma işlemi tamamlanmadan önce TLS oturumu bir kullanıcı veya uygulama tarafından iptal edilirse döndürülür (CloseNotify'a benzer).                                 |
| no_renegotiation              | 100   | Uzak konağın, bir yeniden anlaşma isteğine yanıt olarak TLS yeniden anlaşma el sıkışmaları gerçekleştirmesini istemediğinden bağımsız olarak.                                 |
| unsupported_extension         | 110   | Bir TLS Istemcisi ilk ClientHello (sunucuda bir sorun olduğunu gösterir) için açıkça sorulmayan uzantıları içeren bir ServerHello alırsa gönderilir. |

### <a name="parameters"></a>Parametreler

- **session_ptr** Bir TLS oturum örneği işaretçisi.
- **alert_level** Alınan uyarının düzeyini döndürün (uyarı veya önemli).
- **alert_value** Alınan uyarının değerini döndürür (bkz. tablo).

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı işlemi.
- **NX_PTR_ERROR** (0x07) geçersiz TLS oturumu.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Return values. */
UINT status, alert_level, alert_value;


/* Start a TLS session.  */
status =  nx_secure_tls_session_start(&tls_session, &tcp_socket, NX_WAIT_FOREVER);

/* Check for “alert received” error. */
if(status == NX_SECURE_TLS_ALERT_RECEIVED)
{

        /* Get the alert level and value. */
        status =  nx_secure_tls_session_alert_value_get(&tls_session,
                                             &alert_level, &alert_value);

        /* Print out the received alert level and value. */
        printf("Alert recieved. Value: %d, Level: %d\n", alert_value,
                alert_level);
}
else if(status != NX_SUCCESS)
{
    /* Additional error handling. */
}
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_tls_session_start
- nx_secure_tls_session_send
- nx_secure_tls_session_receive

## <a name="nx_secure_tls_session_certificate_callback_set"></a>nx_secure_tls_session_certificate_callback_set

Ek sertifika doğrulaması için kullanılacak TLS için bir geri çağırma ayarlayın

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_tls_ session_certificate_callback_set (
                  NX_SECURE_TLS_SESSION *tls_session,
                  ULONG (*func_ptr)(NX_SECURE_TLS_SESSION *session,
                                    NX_SECURE_X509_CERT *certificate));
```

### <a name="description"></a>Description

Bu hizmet, uzak bir ana bilgisayardan bir sertifika alındığında, uygulamanın DNS doğrulaması, sertifika iptali ve sertifika ilkesi zorlaması gibi doğrulama denetimleri gerçekleştirmesine izin veren TLS oturumuna bir işlev işaretçisi atar.

NetX güvenli TLS, sertifikanın TLS güvenilen sertifika deposundaki bir sertifikaya izlenip izlenmemesini sağlamak için geri çağırma işlemini çağırmadan önce sertifikada temel X. 509.952 yolu doğrulamasını yapar, ancak diğer tüm doğrulamalar bu geri arama tarafından işlenir.

Geri arama, TLS oturum işaretçisini ve uzak ana bilgisayar kimliği sertifikası (sertifika zincirindeki yaprak) için bir işaretçi sağlar. Tüm doğrulama başarılı olursa geri çağırma NX_SUCCESS döndürmelidir, aksi takdirde doğrulama hatasını gösteren bir hata kodu döndürmelidir. NX_SUCCESS dışındaki herhangi bir değer, TLS el sıkışmasına hemen iptal edilmesini sağlar.

### <a name="parameters"></a>Parametreler

- **session_ptr** Daha önce oluşturulmuş bir TLS oturum örneğine yönelik işaretçi.
- **func_ptr** Sertifika doğrulama geri çağırma işlevinin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) İşlev işaretçisinin başarıyla ayırması.
- **NX_PTR_ERROR** (0x07) Geçersiz TLS oturum işaretçisi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Callback routine used to perform additional checks on a certificate. */
ULONG certificate_callback(NX_SECURE_TLS_SESSION *session, NX_SECURE_X509_CERT
*certificate)
{
    /* Certificate validation checking goes here. */
    return(NX_SUCCESS);
}

/* In TLS setup routine. */
{
        /* Add callback to TLS session.  */
        status =  nx_secure_tls_session_certificate_callback_set(&tls_session,
                                                            certificate_callback);

        /* If status is NX_SUCCESS the certificate callback was added.  */
}
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_tls_session_create
- nx_secure_x509_common_name_dns_check
- nx_secure_x509_crl_revocation_check

## <a name="nx_secure_tls_session_client_callback_set"></a>nx_secure_tls_session_client_callback_set

TLS İstemci el sıkışması başlangıcında çağırmak için TLS için bir geri çağırma ayarlayın

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_tls_ session_client_callback_set (
                  NX_SECURE_TLS_SESSION *tls_session,
                  ULONG (*func_ptr)(NX_SECURE_TLS_SESSION *tls_session,
                                    NX_SECURE_TLS_HELLO_EXTENSION
                                    *extensions, UINT num_extensions));
```

### <a name="description"></a>Description

Bu hizmet, BIR TLS İstemci el sıkışması ServerHelloDone iletisi aldığı zaman TLS'nin çağıracak olduğu bir TLS oturumuna işlev işaretçisi atar. Geri çağırma işlevi, bir uygulamanın alınan ServerHello iletilerinden giriş veya karar alma gerektiren tüm TLS uzantılarını işlemesini sağlar.

Geri çağırma TLS oturum denetim bloğu ve bir dizi farklı nesne NX_SECURE_TLS_HELLO_EXTENSION yürütülür. Uzantı nesneleri dizisinin, belirli bir uzantıyı bulup ayrıştıracak bir yardımcı işleve geçirileme amacı vardır. Şu anda NetX Secure'de TLS İstemcisi girişi gerektiren belirli uzantılar yoktur, ancak uygulama tasarımcılarının kullanılabilir hale gelen özel veya yeni uzantıları işlemesi için geri çağırma kullanılabilir. Merhaba iletilerde sağlanan TLS uzantılarını ayrıştıran örnek bir yardımcı işlev için bkz. *nx_secure_tls_session_sni_extension_parse.*.

İstemci geri çağırma, uzak sunucunun bir sertifika  isteğinde bulunuyor olması ve TLS İstemcisi'nin belirli bir sertifikayı seçmesine izin vermek için bilgi sağladığında TLS İstemcisi için nx_secure_tls_active_certificate_set kullanarak etkin kimlik sertifikasını seçmek için de kullanılabilir. Daha fazla bilgi için nx_secure_tls_active_certificate_set için başvuruya bakın.

### <a name="parameters"></a>Parametreler

- **session_ptr** Daha önce oluşturulmuş bir TLS Oturumu örneğinin işaretçisi.
- **func_ptr** TLS İstemci geri çağırma işlevinin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) İşlev işaretçisinin başarıyla ayırması.
- **NX_PTR_ERROR** (0x07) geçersiz TLS oturum işaretçisi.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Callback routine used to process ServerHello extensions and perform other
   runtime actions at the beginning of a TLS handshake (such as selecting an
   identify certificate to provide to the server). */

ULONG tls_client_callback(NX_SECURE_TLS_SESSION *session,
                          NX_SECURE_TLS_HELLO_EXTENSION *extensions, UINT
                          num_extensions)
{

    /* Extension parsing would go here. */

    /* Set an active identity certificate – the certificate should have been added
       to the local store at application start with
       nx_secure_tls_local_certificate_add. */
    nx_secure_tls_active_certificate_set(session, &global_identity_certificate);

    return(NX_SUCCESS);
}

/* TLS setup routine. */
UINT tls_setup(NX_SECURE_TLS_SESSION *tls_session)
{
    /* Add callback to TLS session.  */
    status =  nx_secure_tls_session_client_callback_set(tls_session,
                                                        client_callback);

    /* If status is NX_SUCCESS the callback was added and will be invoked once
       a ServerHelloDone message is received. */

    return(status);
}
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_tls_session_create
- nx_secure_tls_session_server_callback_set
- nx_secure_tls_active_certificate_set

## <a name="nx_secure_tls_session_x509_client_verify_configure"></a>nx_secure_tls_session_x509_client_verify_configure

İstemci X. 509.440 doğrulamasını etkinleştir ve istemci sertifikaları için alan ayır

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_tls_session_x509_client_verify_configure(
                  NX_SECURE_TLS_SESSION *session_ptr,
                  UINT certs_number, VOID *certificate_buffer,
                  ULONG buffer_size);
```

### <a name="description"></a>Description

Bu hizmet, bir TLS sunucu örneği için isteğe bağlı X. 509.440 Istemci kimlik doğrulamasını sunar. Ayrıca, uzak istemci konaktan gelen sertifika zincirlerini işlemek için gereken alanı ayırır. Uzak istemci tarafından sağlanan sertifikalar, hizmet nx_secure_tls_trusted_certificate_add atanmış olan TLS sunucusu örneğinin güvenilen sertifikalarına karşı doğrulanır *.*

TLS Istemci modu için, uzak sertifika ayırma gereklidir ve bunun yerine hizmet *nx_secure_tls_remote_certificate_buffer_allocate* kullanılmalıdır. Bir TLS Istemci örneğinde X. 509.440 Istemci kimlik doğrulamasının etkinleştirilmesi hiçbir etkiye sahip olmayacaktır.

*Certificate_buffer* parametresi, gelen uzak sertifikaları ve bu sertifikalar için gereken denetim bloklarını depolamak için ayrılan alana işaret eder. Arabellek, her sertifikaya verilen eşit bir bölüme sahip sertifika (*certs_number*) sayısına bölünür. *Buffer_size* parametresi arabelleğin boyutunu gösterir. Aşağıdaki formül ile, gereken alan bulunabilir:

```C
buffer_size = (<expected max number of certificates in chain>) *
             (sizeof(NX_SECURE_X509_CERT) + <max cert size>)
```

İmzalar için SHA-256 kullanan 2048 bitin RSA anahtarlarına sahip tipik sertifikalar, 1000-2000 bayt aralığındadır. Arabellek, her sertifika için en az sayıda tutmaya yetecek kadar büyük olmalıdır, ancak uzak ana bilgisayar sertifikalarına bağlı olarak, önemli ölçüde daha küçük veya daha büyük olabilir. Arabellek gelen sertifikayı tutmak için çok küçük olduğunda, TLS el sıkışması bir hatayla sona erdirmek için kullanılır.

### <a name="parameters"></a>Parametreler

- **session_ptr** Daha önce oluşturulmuş bir TLS oturum örneğine yönelik işaretçi.
- **certs_number** Sağlanan arabellekten ayrılacak sertifika sayısı.
- **certificate_buffer** Uzak bir konaktan alınan sertifikaları tutmak için bir arabelleğe işaretçi.
- **buffer_size** Sertifika arabelleğinin boyutu.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00)Başarılı sertifika ayırma.
- **NX_PTR_ERROR** (0x07) Geçersiz TLS oturumu veya arabellek işaretçisi.
- **NX_SECURE_TLS_INSUFFICIENT_CERT_SPACE** (0x12D) Sağlanan arabellek çok küçüktü.
- **NX_INVALID_PARAMETERS** (0x4D) Arabellek istenen sayıda sertifikayı tutmak için çok küçüktü.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Buffer space to hold the incoming certificates. */
#define CERTIFICATE_NUMBER    (2)
#define CERTIFICATE_SIZE      (2000)
#define BUFFER_SIZE          (CERTIFICATE_NUMBER * \
                                (sizeof(NX_SECURE_X509_CERT) + CERTIFICATE_SIZE))
UCHAR certificate_buffer[BUFFER_SIZE];

/* Enable X.509 Client verification and allocate certificate space in our TLS
   Server session.  */
status =  nx_secure_tls_session_x509_client_verify_configure(&tls_session,
                                                    CERTIFICATE_NUMBER,
                                                    certificate_buffer,
                                                    BUFFER_SIZE);


/* If status is NX_SUCCESS the buffer was successfully allocated.  */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_x509_certificate_initialize
- nx_secure_tls_session_create
- nx_secure_tls_remote_certificate_buffer_allocate

## <a name="nx_secure_tls_session_client_verify_disable"></a>nx_secure_tls_session_client_verify_disable

NetX Güvenli TLS Oturumu için İstemci Sertifikası Kimlik Doğrulamasını Devre Dışı Bırakma

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_tls_session_client_verify_disable(
                              NX_SECURE_TLS_SESSION *session_ptr);
```

### <a name="description"></a>Description

Bu hizmet, belirli bir TLS oturumu için İstemci Sertifikası Kimlik Doğrulamasını devre dışı bırakıyor. Daha fazla nx_secure_tls_session_client_verify_enable için bkz. Nx_secure_tls_session_client_verify_enable.

### <a name="parameters"></a>Parametreler

- **session_ptr** TLS Oturumu örneğinin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı durum değişikliği.
- **NX_PTR_ERROR** (0x07) Geçersiz TLS oturum işaretçisi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Disable client certificate authentication for this TLS session.   */
status = nx_secure_tls_session_client_verify_disable(&tls_session);

/* Any new TLS Server sessions using the tls_session control block will not
request certificates from the remote TLS client.  */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_tls_session_client_verify_enable
- nx_secure_tls_session_start
- nx_secure_tls_session_create

## <a name="nx_secure_tls_session_client_verify_enable"></a>nx_secure_tls_session_client_verify_enable

NetX güvenli TLS oturumu için Istemci sertifikası kimlik doğrulamasını etkinleştir

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_tls_session_client_verify_enable(
                                NX_SECURE_TLS_SESSION *session_ptr);
```

### <a name="description"></a>Description

Bu hizmet belirli bir TLS oturumu için Istemci sertifikası kimlik doğrulamasını mümkün bir şekilde sunar. Bir TLS sunucu örneği için Istemci sertifikası kimlik doğrulamasını etkinleştirme, TLS sunucusunun ilk TLS el sıkışması sırasında herhangi bir uzak TLS Istemcisinden sertifika istemesine neden olur. Uzak TLS Istemcisinden alınan sertifikaya, TLS sunucusunun Istemcinin sertifikaya sahip olduğunu doğrulamak için kullandığı bir CertificateVerify iletisi (Bu sertifikayla ilişkili özel anahtara erişimi vardır) ile birlikte gönderilir.

Belirtilen sertifika doğrulanırsa ve bir X. 509.952 sertifika zinciri aracılığıyla TLS sunucusu güvenilen sertifika deposundaki bir sertifikaya geri izleniyorsa, uzak TLS Istemcisinin kimliği doğrulanır ve el sıkışma devam eder. Sertifikayı veya CertificateVerify iletisini işlerken herhangi bir hata olması durumunda, TLS anlaşması bir hatayla biter.

> [!NOTE]
> *TLS sunucusunda, güvenilir depodaki en az bir sertifika nx_secure_tls_trusted_certificate_add ile eklenmiş olmalıdır veya kimlik doğrulama her zaman başarısız olur.*

### <a name="parameters"></a>Parametreler

- **session_ptr** Bir TLS oturum örneği işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı durum değişikliği.
- **NX_PTR_ERROR** (0x07) geçersiz TLS oturum işaretçisi.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Add a trusted certificate so the TLS Server has something to verify against. */
status = nx_secure_tls_trusted_certificate_add(&tls_session,
                                               &trusted_certificate);

/* Disable client certificate authentication for this TLS session.   */
status = nx_secure_tls_session_client_verify_enable(&tls_session);

/* Any new TLS Server sessions using the tls_session control block will now
request and verify certificates from the remote TLS client.  */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_tls_session_client_verify_enable
- nx_secure_tls_session_start
- nx_secure_tls_session_create
- nx_secure_tls_trusted_certificate_add

## <a name="nx_secure_tls_session_create"></a>nx_secure_tls_session_create

Güvenli iletişim için bir NetX güvenli TLS oturumu oluşturun

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_tls_session_create(NX_SECURE_TLS_SESSION *session_ptr
                                   NX_SECURE_TLS_CRYPTO *cipher_table,
                                   VOID *encryption_metadata_area,
                                   ULONG encryption_metadata_size);
```

### <a name="description"></a>Description

Bu hizmet, bir NX_SECURE_TLS_SESSION üzerinden güvenli TLS iletişimleri kurmada kullanmak üzere bir ağ yapısı örneği başlatıyor.

yöntemi, TLS NX_SECURE_TLS_CRYPTO kullanılabilen şifreleme yöntemleriyle doldurulan bir nesne alır. Bu *encryption_metadata_area,* hesaplamalar için tablodaki şifreleme yöntemleri tarafından kullanılan "meta veriler" için TLS tarafından NX_SECURE_TLS_CRYPTO bir arabelleğe gösterir. Tablonun boyutu, nx_secure_tls_metadata_size_calculate kullanılarak belirlenecektir. Daha fazla ayrıntı için Bölüm 3'te "NetX Secure TLS'de Şifreleme" bölümüne bakın.

### <a name="parameters"></a>Parametreler

- **session_ptr** TLS Oturumu örneğinin işaretçisi.
- **cipher_table** TLS şifreleme yöntemlerinin işaretçisi.
- **encryption_metadata_area** Şifreleme meta verileri için alan işaretçisi.
- **encryption_metadata_size** Meta veri arabelleğinin boyutu.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00)TLS oturumunun başarıyla başlatılıyor.
- **NX_PTR_ERROR** (0x07) Geçersiz bir işaretçi kullanmayı denedi.
- **NX_INVALID_PARAMETERS** (0x4D) Meta veri arabelleği verilen yöntemler için çok küçüktü.
- **NX_SECURE_TLS_UNSUPPORTED_CIPHER** (0x106) TLS'nin etkin sürümü için gerekli bir şifreleme yöntemi, şifreleme tablosunda sağlanmadı.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Reference the platform-specific TLS cryptographic method table. */
extern const NX_SECURE_TLS_CRYPTO nx_crypto_tls_ciphers;

/* Declare a buffer for the cryptographic metadata. The size should be calculated
   using nx_secure_tls_metadata_size_calculate. */
UCHAR crypto_metadata[4500];

/* Initialize TLS session.  */
status =  nx_secure_tls_session_create(&tls_session,
                                       &nx_crypto_tls_ciphers,
                                       crypto_metadata,
                                       sizeof(crypto_metadata));


/* If status is NX_SUCCESS the TLS Session was successfully initialized.  */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_x509_certificate_initialize
- nx_secure_tls_metadata_size_calculate
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_session_start
- nx_secure_tls_session_end
- nx_secure_tls_session_send
- nx_secure_tls_session_receive
- nx_secure_tls_session_delete
- Bölüm 3 ' te NetX güvenli TLS 'de şifreleme

## <a name="nx_secure_tls_session_delete"></a>nx_secure_tls_session_delete

NetX güvenli TLS oturumunu silme

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_tls_session_delete(NX_SECURE_TLS_SESSION *session_ptr);
```

### <a name="description"></a>Description

Bu hizmet, bir NX_SECURE_TLS_SESSION yapısı örneğiyle temsil edilen bir TLS oturumunu siler ve o oturum örneğine ait tüm sistem kaynaklarını serbest bırakır.

### <a name="parameters"></a>Parametreler

- **session_ptr** Bir TLS oturum örneği işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- TLS oturumunun başarıyla başlatılmasından **NX_SUCCESS** (0x00).
- **NX_PTR_ERROR** (0x07) geçersiz bir Işaretçi kullanmaya çalıştı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Delete TLS session.  */
status =  nx_secure_tls_session_delete(&tls_session);


/* If status is NX_SUCCESS the TLS Session was successfully deleted.  */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_x509_certificate_initialize
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_session_start
- nx_secure_tls_session_end
- nx_secure_tls_session_send
- nx_secure_tls_session_receive
- nx_secure_tls_session_create

## <a name="nx_secure_tls_session_end"></a>nx_secure_tls_session_end

Etkin bir NetX güvenli TLS oturumu sonlandır

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_tls_session_end(NX_SECURE_TLS_SESSION *session_ptr,
                                    ULONG wait_option);
```

### <a name="description"></a>Description

Bu hizmet, TLS CloseNotify iletisini uzak ana bilgisayara göndererek bir NX_SECURE_TLS_SESSION yapısı örneği tarafından temsil edilen bir TLS oturumunu sonlandırır. Ardından hizmet, uzak ana bilgisayarın kendi CloseNotify iletisiyle yanıt vermesini bekler.

Uzak konak bir CloseNotify iletisi göndermse TLS bunu bir hata ve olası bir güvenlik ihlali olarak kabul ederek güvenli bağlantı için dönüş değerinin denetlen önemlidir. wait_option  parametresi, çağrıyı çağıran iş parçacığına denetim döndürmeden önce hizmetin yanıt için ne kadar beklemesi gerektiğini kontrol etmek için kullanılabilir.

### <a name="parameters"></a>Parametreler

- **session_ptr** TLS Oturumu örneğinin işaretçisi.
- **wait_option** Hizmetin uzak konaktan ne kadar süreyle yanıt beklemesi gerektiğini gösterir.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) TLS oturumunun başarıyla başlatılıyor.
- **NX_SECURE_TLS_NO_CLOSE_RESPONSE** (0x113) Zaman dışından uzak konaktan yanıt almadı.
- **NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) CloseNotify iletisi göndermek için bir paket ayrılamadı.
- **NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) TCP yuvası üzerinden CloseNotify iletisi gönderildi.
- **NX_PTR_ERROR** (0x07) Geçersiz bir işaretçi kullanmayı denedi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* End TLS session.  */
status =  nx_secure_tls_session_end(&tls_session, NX_WAIT_FOREVER);


/* If status is NX_SUCCESS the TLS Session was successfully ended.  */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_x509_certificate_initialize
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_session_start
- nx_secure_tls_session_delete
- nx_secure_tls_session_send
- nx_secure_tls_session_receive
- nx_secure_tls_session_create

## <a name="nx_secure_tls_session_packet_buffer_set"></a>nx_secure_tls_session_packet_buffer_set

NetX Güvenli TLS Oturumu için paket yeniden değerlendirme arabelleği ayarlama

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_tls_session_packet_buffer_set(
                                    NX_SECURE_TLS_SESSION *session_ptr,
                                    UCHAR *buffer_ptr,
                                    ULONG buffer_size);
```

### <a name="description"></a>Description

Bu hizmet, bir paket yeniden birleştirme arabelleğini bir TLS oturumuyla ilişkilendirir. Gelen TLS kayıtlarının şifresini çözmek ve ayrıştırmak için, her bir kayıttaki verilerin temel alınan TCP paketlerinden bir araya gelmelidir. TLS kayıtlarının boyutu 16KB 'a kadar olabilir (genellikle çok daha küçüktür), bu nedenle tek bir TCP paketine uyamayabilir.

Gelen ileti boyutunun, 16KB olan TLS kayıt sınırından küçük olacağını biliyorsanız, arabellek boyutu daha küçük hale getirilebilir, ancak bilinmeyen gelen verileri işlemek için arabelleğin mümkün olduğunca büyük olması gerekir. Gelen bir kayıt sağlanan arabellekten fazlaysa, TLS oturumu bir hatayla sona acaktır.

### <a name="parameters"></a>Parametreler

- **session_ptr** Bir TLS oturum örneği işaretçisi.
- **buffer_ptr** Paket yeniden birleştirme için kullanılacak TLS arabelleği işaretçisi.
- **Buffer_size** Sağlanan arabelleğin bayt cinsinden boyutu.

### <a name="return-values"></a>Dönüş Değerleri

- TLS oturumunun başarıyla başlatılmasından **NX_SUCCESS** (0x00).
- **NX_INVALID_PARAMETERS** (0x4D) geçersiz arabellek veya TLS oturum işaretçisi.
- **NX_PTR_ERROR** (0x07) geçersiz bir Işaretçi kullanmaya çalıştı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Buffer for TLS packet reassembly. */
UCHAR tls_packet_buffer[16384];
/* Assign buffer to TLS session.  */
status =  nx_secure_tls_session_packet_buffer_set(&tls_session, tls_packet_buffer,
                                                  sizeof(tls_packet_buffer));


/* If status is NX_SUCCESS the buffer was successfully added.  */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_x509_certificate_initialize
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_session_start
- nx_secure_tls_session_delete
- nx_secure_tls_session_send
- nx_secure_tls_session_receive
- nx_secure_tls_session_create

## <a name="nx_secure_tls_session_protocol_version_override"></a>nx_secure_tls_session_protocol_version_override

NetX Güvenli TLS Oturumu için varsayılan TLS protokol sürümünü geçersiz kılma

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_tls_session_protocol_version_override(
                              NX_SECURE_TLS_SESSION *session_ptr,
                              USHORT protocol_version);
```

### <a name="description"></a>Description

Bu hizmet, belirli bir oturum tarafından kullanılan varsayılan (en yeni) TLS protokol sürümünü geçersiz kılar. Bu, NetX Secure TLS'nin derleme zamanında daha yeni TLS sürümlerini devre dışı bırakmadan belirli bir TLS Oturumu için daha eski bir TLS sürümünü kullanmasına olanak sağlar. Bu, TLS'nin en yeni sürümünü desteklemeen eski bir ana bilgisayarla iletişim kurması gerektirilen uygulamalarda yararlı olabilir.

> [!IMPORTANT]
> *Sürüm 5.11SP3'te NetX Secure TLS RFC 7507'yi destekler (aşağıdaki nota bakın) ve bu API ile eski bir sürümde yapılan geçersiz kılmalar ClientHello'da geri dönüş SCSV'si gönderilir. Sunucu daha yeni bir TLS sürümünü destekliyorsa ve ClientHello'ya geri dönüş SCSV'si dahil edilirse, bu sunucu TLS el sıkışmayı "Uygunsuz Geri Dönüş" uyarısıyla iptal eder. SCSV yalnızca sürüm geçersiz kılma özelliği tlS'nin etkin olandan eski bir sürümü olduğunda gönderilir (örneğin, sürümü TLS 1.2 olarak geçersiz kılarsanız, SCSV gönderilmez).*

protocol_version parametresi için geçerli değerler şu makrolardır: NX_SECURE_TLS_VERSION_TLS_1_0, NX_SECURE_TLS_VERSION_TLS_1_1 ve NX_SECURE_TLS_VERSION_TLS_1_2.

Bu NX_SECURE_TLS_DISABLE_TLS_1_1 NX_SECURE_TLS_ENABLE_TLS_1_0, uygulamaya derlenmiş TLS sürümlerini kontrol etmek için kullanılabilir. TLS sürüm 1.2 her zaman etkindir.

Uzak ana bilgisayar sağlanan sürümü desteklemezse bağlantının başarısız olacağını unutmayın. Yalnızca verilen geçersiz kılma sürümü NetX Secure TLS tarafından anılacaktır.

> [!IMPORTANT]
> RFC 7507: TLS Geri Dönüş SCSV. Bu RFC, başlangıçta protokol eski sürüm düşürme anlaşmalarını hatalı bir şekilde ele alan ve bunun yerine geçerli olmayan ClientHello iletilerini reddeden sunuculardan kaynaklanan bir güvenlik sorununu azaltmak için tanıtıldı. Bu eski sunucularla uyumlu olmaya devam etmek için bazı TLS istemci uygulamaları ile başarısız el sıkışmalarını ve eski TLS sürümünü yeniden denemeye başladı (örneğin TLS 1.2 başarısız oldu, bu nedenle TLS 1.1'i deneyin). Bu geçici çözüm, yeni bir sorun ortaya sunmuştur; bir saldırgan, sunucu daha yeni TLS sürümünü desteklense bile, sunucu bağlantısının başarısız olmasına neden olan bir ağ veya paket hatası ile yapay bir istemciyi indirgemeye zorlayabilir. Daha eski bir sürüme indirgenerek saldırgan, söz konusu sürümdeki zayıf yönleriyle yararlanabilir (SSLv3<sup>21</sup> , özellıkle de çıkış saldırılarına karşı zayıfdır). Bu durumu engellemek için, RFC 7507 ' de, bir TLS istemcisi desteklediği en yeni sürüm olmayan bir TLS<sup></sup> sürümünü kullanırken TLS sunucusuna bildiren "GERI dönüş SCSV" bir ClientHello Bu şekilde, daha yeni bir sürümü destekleyen bir sunucu, geri dönüş SCSV 'i içeren bir ClientHello reddedebilir ve düşürme saldırılarının başarılı olmasını önler.

21. NetX Secure, POOıDLE gibi bilinen ciddi zayıf yanlar nedeniyle SSLv3 uygulamaz.

22. Sözde ciphersuite veya SCSV (sinyal şifreleme paketi değeri), eski TLS sürümlerinde kullanılamayan özelliklerle ilgili etkin TLS uygulamalarını işaret etmek için kullanılan ayrılmış bir ciphersuite numarasıdır. Geri dönüş SCSV ve TLS_EMPTY_RENEGOTIATION_INFO_SCSV (RFC 5746) örnektir.

### <a name="parameters"></a>Parametreler

- **session_ptr** Bir TLS oturum örneği işaretçisi.
- **protocol_version** Kullanılacak belirli TLS sürümü için TLS sürümü makrosu.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı durum değişikliği.
- **NX_PTR_ERROR** (0x07) geçersiz TLS oturum işaretçisi.
- **NX_SECURE_TLS_UNSUPPORTED_TLS_VERSION** (0x110) bilinen ancak desteklenmeyen TLS sürümü.
- **NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0x10F) geçersiz protokol sürümü.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Set the protocol version to be used to TLSv1.1. */
status = nx_secure_tls_session_protocol_version_override(&tls_session,
                                              NX_SECURE_TLS_VERSION_TLS_1_1);

/* This TLS Session will use TLSv1.1 for the handshake and TLS session. */
status = nx_secure_tls_session_start(&tls_session, &tcp_socket, NX_WAIT_FOREVER);
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_tls_session_start
- nx_secure_tls_session_create

## <a name="nx_secure_tls_session_receive"></a>nx_secure_tls_session_receive

NetX güvenli TLS oturumundan veri alma

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_tls_session_receive(NX_SECURE_TLS_SESSION *session_ptr,
                                    NX_PACKET **packet_ptr,
                                    ULONG wait_option);
```

### <a name="description"></a>Description

Bu hizmet, belirtilen etkin TLS oturumundan verileri alır ve bu verilerin şifresini, NX_PACKET parametresindeki çağırana sağlamadan önce işleme alır. Belirtilen oturumda hiçbir veri sıraya alınmaz, çağrı sağlanan bekleme seçeneğine göre askıya alınır.

> [!IMPORTANT]
> *Bir NX_SUCCESS döndürülürse, uygulama artık gerekli olmadığı zaman alınan paketi serbest bırakmakla sorumludur.*

### <a name="parameters"></a>Parametreler

- **session_ptr** TLS Oturumu örneğinin işaretçisi.
- **packet_ptr** Ayrılmış bir TLS paket işaretçisinin işaretçisi.
- **wait_option** Hizmetin, geri dönmeden önce uzak konaktan bir paket için ne kadar beklemesi gerektiğini gösterir.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) TLS oturumunun başarıyla başlatılıyor.
- **NX_NO_PACKET** (0x01) Veri alınmamıştır.
- **NX_NOT_CONNECTED** (0x38) Temel ALıNAN TCP yuvası artık bağlı değil.
- **NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0x108) Alınan ileti kimlik doğrulaması karma denetimi başarısız oldu.
- **NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0x10F) Alınan ileti üst bilgisinde bilinmeyen bir protokol sürümü içeriyordu.
- **NX_SECURE_TLS_ALERT_RECEIVED** (0x114) Uzak konaktan bir TLS uyarısı alındı.
- **NX_PTR_ERROR** (0x07) Geçersiz bir işaretçi kullanmayı denedi.
- **NX_SECURE_TLS_SESSION_UNINITIALIZED** (0x101) Sağlanan TLS oturumu başlatılmadı.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Receive a packet from an active TLS session previously created and started with
nx_secure_tls_session_start. Wait until a packet is received, blocking otherwise.
*/
status =  nx_secure_tls_session_receive(&tls_session, &packet_ptr,
NX_WAIT_FOREVER);


/* If status is NX_SUCCESS the received packet is pointed to by  "packet_ptr". */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_socket_receive
- nx_secure_x509_certificate_initialize
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_session_start
- nx_secure_tls_session_delete
- nx_secure_tls_session_send
- nx_secure_tls_session_end
- nx_secure_tls_session_create

## <a name="nx_secure_tls_session_renegotiate_callback_set"></a>nx_secure_tls_session_renegotiate_callback_set

Oturum yeniden anlaşması başlangıcında çağrılacak bir geri çağırma atayın

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_tls_ session_renegotiate_callback_set (
                  NX_SECURE_TLS_SESSION *tls_session,
                  ULONG (*func_ptr)(struct NX_SECURE_TLS_SESSION_struct
                  *session));
```

### <a name="description"></a>Description

Bu hizmet, uzak ana bilgisayardan bir oturum yeniden anlaşma el sıkışma iletisi alındığında çağrılacak bir TLS oturumuna geri çağırma işlemi atar.

Geri çağırma işlevi, bir yeniden anlaşma anlaşmasını oluşturan uygulamaya bildirim olarak tasarlanmıştır. uygulama, geri aramadan sıfır olmayan bir değer döndürerek TLS oturumunu sonlandırarak TLS oturumunun bir hata ile sonlanmasına neden olacak. Uygulama yeniden anlaşmaya devam etmek isterse, geri çağırma NX_SUCCESS döndürmelidir.

> [!NOTE]
> *TLS yeniden anlaşması semantiği nedeniyle, uzak sunucudan bir HelloRequest alındığında, ancak istemci yeniden anlaşmayı başlattığında değil, NetX güvenli TLS Istemcileri için geri arama çağrılacaktır. NetX güvenli TLS sunucularında, bir yeniden anlaşma ClientHello alındığında (etkin bir TLS oturumu bağlamında alınan herhangi bir ClientHello) geri çağırma işlemi çağrılır. Bu, TLS sunucusu uzak istemcinin yanıt verdiği bir merhaba Istek göndereceği için, geri aramanın uzak ana bilgisayar veya yerel uygulamanın yeniden anlaşmayı başlattığını belirtir.*

NetX güvenli TLS, yeniden anlaşma el sıkışmaları 'nın ortadaki adam saldırılarına maruz olmamasını sağlamak için, RFC 5746 ' den güvenli yeniden anlaşma alma uzantısını uygular.

### <a name="parameters"></a>Parametreler

- **session_ptr** TLS oturum örneği işaretçisi.
- **func_ptr** Geri arama işlevine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) geri aramanın başarıyla atanması.
- **NX_PTR_ERROR** (0x07) geri çağırma IşLEVI veya TLS oturumu için geçersiz bir Işaretçi kullanmayı denedi.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Simple callback notifying the user that a renegotiation is starting. */
ULONG tls_renegotiation_callback(NX_SECURE_TLS_SESSION *session)
{
    printf("Renegotiation initiated by remote host\n");

    return(NX_SUCCESS);
}

/* Establish a TLS session with a remote host (TLS Client) */
status =  nx_secure_tls_session_create(&tls_session,
                                       &nx_crypto_tls_ciphers,
                                       crypto_metadata,
                                       sizeof(crypto_metadata));


/* Set callback for renegotiation notification. */
status = nx_secure_tls_session_renegotiate_callback_set(&tls_session,
                                                tls_renegotiation_callback);
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_tls_session_create
- nx_secure_tls_session_start
- nx_secure_tls_session_receive
- nx_secure_tls_session_send
- nx_secure_tls_session_renegotiate

## <a name="nx_secure_tls_session_renegotiate"></a>nx_secure_tls_session_renegotiate

Uzak konakla oturum yeniden anlaşma başlatma

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_tls_ session_renegotiate (
                  NX_SECURE_TLS_SESSION *tls_session,
                  UINT wait_option);
```

### <a name="description"></a>Description

Bu hizmet, bağlı uzak TLS *ana bilgisayarıyla* oturum yeniden anlaşmaları başlatıyor. Yeniden anlaşma, önceden kurulmuş bir TLS oturumu bağlamında ikinci bir TLS el sıkışması oluşur. Yeni oturum anahtarları oluşturulana ve ChangeCipherSpec iletileri değiştirilene kadar yeni el sıkışma iletilerinin her biri TLS oturumu kullanılarak şifrelenir ve bu sırada tüm iletileri şifrelemek için yeni anahtarlar kullanılır.

TLS oturumu kurulduktan sonra herhangi bir zamanda yeniden görüşme başlatabilirsiniz. TLS el sıkışması sırasında veya TLS oturumu kurulmadan önce yeniden anlaşma denenirse hiçbir işlem olmaz.

> [!NOTE]
> *Bu hizmet çağrıldığında tüm TLS el sıkışması gerçekleştirilir, bu nedenle tamamlanma süresi ve döndürülen durum geçerli TLS ayarlarına ve oturum parametrelerine bağlı olarak değişir.*

NetX Secure TLS, yeniden anlaşma el sıkışmalarının ortadaki adam saldırılarına maruz olmadığını güvence altına almak için RFC 5746'dan Güvenli Yeniden Anlaşma Kimlik Doğrulama Uzantısı'nın uygulanmasını sağlar.

### <a name="parameters"></a>Parametreler

- **session_ptr** TLS Oturumu örneğinin işaretçisi.
- **wait_option** Hizmetin, geri dönmeden önce uzak konaktan bir paket için ne kadar beklemesi gerektiğini gösterir. Bu, TLS içindeki tüm NetX hizmetlerine geçirildi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı yeniden yapılanma.
- **NX_NO_PACKET** (0x01) Veri alınmamıştır.
- **NX_NOT_CONNECTED** (0x38) Temel ALıNAN TCP yuvası artık bağlı değil.
- **NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0x108) Alınan ileti kimlik doğrulaması karma denetimi başarısız oldu.
- **NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0x10F) Alınan ileti üst bilgisinde bilinmeyen bir protokol sürümü içeriyordu.
- **NX_SECURE_TLS_ALERT_RECEIVED** (0x114) Uzak konaktan bir TLS uyarısı alındı.
- **NX_SECURE_TLS_RENEGOTIATION_SESSION_INACTIVE** (0x134) Yerel veya uzak TLS oturumu devre dışıdır ve bu da yeniden görüşmeyi imkansız hale gelir.
- **NX_SECURE_TLS_RENEGOTIATION_FAILURE** (0x13a) uzak ana BILGISAYAR, SCSV veya güvenli yeniden anlaşma uzantısı sağlamadı ve bu nedenle yeniden anlaşma yapılamaz.
- **NX_PTR_ERROR** (0x07) geçersiz bir Işaretçi kullanmaya çalıştı.
- **NX_SECURE_TLS_SESSION_UNINITIALIZED** (0x101) sağlanan TLS oturumu başlatılmadı.
- **NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) temel alınan paket ayırması başarısız oldu.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Establish a TLS session with a remote host (TLS Client) */
status =  nx_secure_tls_session_create(&tls_session,
                                       &nx_crypto_tls_ciphers,
                                       crypto_metadata,
                                       sizeof(crypto_metadata));


/* Setup a client socket connection.  */
status = nx_tcp_client_socket_connect(&tcp_socket, server_ipv4_address,
REMOTE_SERVER_PORT, NX_WAIT_FOREVER);

/* Start the TLS session. */
status = nx_secure_tls_session_start(&tls_session, &tcp_socket, NX_WAIT_FOREVER);

/* Send some data in the first TLS session. (Check “status” for errors…)*/
status = nx_secure_tls_packet_allocate(&tls_session, &pool_0, &send_packet,
                                       NX_WAIT_FOREVER);
status = nx_packet_data_append(send_packet, "Hello there!\r\n", 14, &pool_0,
                               NX_WAIT_FOREVER);
status = nx_secure_tls_session_send(&tls_session, send_packet,
                                    NX_IP_PERIODIC_RATE);

/* Now renegotiate the session. */
status  = nx_secure_tls_session_renegotiate(&tls_session, NX_WAIT_FOREVER);

/* If status == NX_SUCCESS, new TLS session keys have been generated. */

/* Send some data in the new TLS session. This will be encrypted using the new
   keys. */
status = nx_secure_tls_packet_allocate(&tls_session, &pool_0, &send_packet,
                                       NX_WAIT_FOREVER);
status = nx_packet_data_append(send_packet, "Another message…\r\n", 18, &pool_0,
                               NX_WAIT_FOREVER);
status = nx_secure_tls_session_send(&tls_session, send_packet,
                                    NX_IP_PERIODIC_RATE);
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_tls_session_create
- nx_secure_tls_session_start
- nx_secure_tls_session_receive
- nx_secure_tls_session_send
- nx_secure_tls_session_renegotiation_callback_set

## <a name="nx_secure_tls_session_reset"></a>nx_secure_tls_session_reset

NetX güvenli TLS oturumunu Temizleme ve sıfırlama

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_tls_session_reset (NX_SECURE_TLS_SESSION *session_ptr);
```

### <a name="description"></a>Description

Bu hizmet bir TLS oturumunu temizler ve mevcut bir TLS oturum nesnesinin yeni bir oturum için yeniden kullanılabilmesi için oturum oluşturulmuşdaymışsınız gibi durumu sıfırlar.

### <a name="parameters"></a>Parametreler

- **session_ptr** Bir TLS oturum örneği işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- TLS oturumunun başarıyla başlatılmasından **NX_SUCCESS** (0x00).
- **NX_INVALID_PARAMETERS** (0x4D) geçersiz TLS oturum işaretçisi.
- **NX_PTR_ERROR** (0x07) geçersiz bir Işaretçi kullanmaya çalıştı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Reset a TLS session.  */
status =  nx_secure_tls_session_reset(&tls_session);


/* If status is NX_SUCCESS the session was successfully reset and may be reused.*/
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_x509_certificate_initialize
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_session_start
- nx_secure_tls_session_delete
- nx_secure_tls_session_send
- nx_secure_tls_session_receive
- nx_secure_tls_session_create

## <a name="nx_secure_tls_session_send"></a>nx_secure_tls_session_send

NetX Güvenli TLS Oturumu aracılığıyla veri gönderme

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_tls_session_send(NX_SECURE_TLS_SESSION *session_ptr,
                                    NX_PACKET *packet_ptr,
                                    ULONG wait_option);
```

### <a name="description"></a>Description

Bu hizmet, belirtilen etkin TLS NX_PACKET kullanarak ve uzak ana bilgisayara göndermeden önce bu verilerin şifrelemesi işlemesi için sağlanan hizmette verileri gönderir. Alıcının son tanıtan pencere boyutu bu istekten küçükse, hizmet belirtilen bekleme seçeneklerine göre isteğe bağlı olarak askıya alır.

> [!IMPORTANT]
> *Bir hata döndürül olmadığı sürece, uygulama bu çağrıdan sonra paketi serbest bırakmamalı. Ağ sürücüsü iletimden sonra paketi serbest bıraktıracak olduğundan, bunu yapmak öngörülemeyen sonuçlara neden olur.*

### <a name="parameters"></a>Parametreler

- **session_ptr** TLS Oturumu örneğinin işaretçisi.
- **packet_ptr** Gönderilecek verileri içeren bir TLS paketinin işaretçisi.
- **wait_option** İstek, alıcının pencere boyutundan büyükse hizmetin nasıl davranacağını tanımlar.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) TLS oturumunun başarıyla başlatılıyor.
- **NX_NO_PACKET** (0x01) Veri alınmamıştır.
- **NX_NOT_CONNECTED** (0x38) Temel ALıNAN TCP yuvası artık bağlı değil.
- **NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) Temel ALıNAN TCP yuvası gönderme işlemi başarısız oldu.
- **NX_PTR_ERROR** (0x07) Geçersiz bir işaretçi kullanmayı denedi.
- **NX_SECURE_TLS_SESSION_UNINITIALIZED** (0x101) Sağlanan TLS oturumu başlatılmadı.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Send a packet using an active TLS session previously created and started with
nx_secure_tls_session_start. Wait until a packet is sent, blocking otherwise.   */
status =  nx_secure_tls_session_send(&tls_session, &packet_ptr, NX_WAIT_FOREVER);


/* If status is NX_SUCCESS the packet has been sent. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_socket_receive
- nx_secure_x509_certificate_initialize
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_packet_allocate
- nx_secure_tls_session_start
- nx_secure_tls_session_delete
- nx_secure_tls_session_receive
- nx_secure_tls_session_end
- nx_secure_tls_session_create

## <a name="nx_secure_tls_session_server_callback_set"></a>nx_secure_tls_session_server_callback_set

TLS sunucusu el sıkışmasının başlangıcında çağırmak üzere TLS için bir geri çağırma ayarlayın

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_tls_ session_server_callback_set (
                 NX_SECURE_TLS_SESSION *tls_session,
                 ULONG (*func_ptr)(NX_SECURE_TLS_SESSION *tls_session,
                                   NX_SECURE_TLS_HELLO_EXTENSION
                                   *extensions, UINT num_extensions));
```

### <a name="description"></a>Description

Bu hizmet, TLS sunucusu el sıkışması bir ClientHello iletisi aldığında TLS 'nin çağıracağı bir TLS oturumuna bir işlev işaretçisi atar. Geri arama işlevi, bir uygulamanın giriş veya karar verme gerektiren alınan ClientHello iletisindeki TLS uzantılarını işlemesini sağlar.

Geri çağırma, TLS oturum denetim bloğu ve NX_SECURE_TLS_HELLO_EXTENSION nesnelerinden oluşan bir dizi ile yürütülür. Uzantı nesnelerinin dizisi, belirli bir uzantıyı bulacak ve ayrıştıracak bir yardımcı işleve geçirilmesi amaçlanmıştır. Merhaba iletilerde sunulan TLS uzantılarını ayrıştırır örnek bir yardımcı işlev için bkz. *nx_secure_tls_session_sni_extension_parse*.

Sunucu geri çağırması, TLS sunucusu için *nx_secure_tls_active_certificate_set* kullanarak etkin kimlik sertifikasını seçmek için de kullanılabilir. Bu, çoğu zaman bir Sunucu Adı Belirtme (SNı) uzantısına yanıt olarak oluşur ve bu da bir TLS Istemcisinin hangi sunucuyu iletişim kurmaya çalıştığını belirlemesine izin verir. Daha fazla bilgi için *nx_secure_tls_session_sni_extension_parse* ve *nx_secure_tls_active_certificate_set* başvurularına bakın.

### <a name="parameters"></a>Parametreler

- **session_ptr** Daha önce oluşturulmuş bir TLS oturum örneğine yönelik işaretçi.
- **func_ptr** TLS Sunucusu geri çağırma işlevinin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) İşlev işaretçisinin başarıyla ayırması.
- **NX_PTR_ERROR** (0x07) Geçersiz TLS oturum işaretçisi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Application-supplied function to map server DNS name to a specific certificate
   ID. The certificate ID is supplied by the application when the certificate is
   added with nx_secure_tls_server_certificate_add. */
UINT application_find_id_by_dns_name(NX_SECURE_X509_DNS_NAME *dns_name)
{
    if(strncmp(dns_name->nx_secure_x509_dns_name, “server_name”,
               dns_name->nx_secure_x509_dns_name_length) == 0)
    {
        /* DNS name matches one we know, return it’s ID. */
        return(0x12);
    }

    /* Unknown DNS name, return 0 to indicate no matching ID found. */
    return(0);
}

/* Callback routine used to process ClientHello extensions and perform other
   runtime actions at the beginning of a TLS handshake (such as selecting an
   identify certificate to provide to the client). */
ULONG tls_server_callback(NX_SECURE_TLS_SESSION *session,
                          NX_SECURE_TLS_HELLO_EXTENSION *extensions, UINT
                          num_extensions)
{
UINT status;
NX_SECURE_X509_DNS_NAME dns_name;
UINT cert_id;
NX_SECURE_X509_CERT *certificate;


    /* Find and parse a Server Name Indication (SNI) extension. */
    status = nx_secure_tls_session_sni_extension_parse(session, extensions,
                                                       num_extensions, &dns_name);

    if(status != NX_SUCCESS && status != NX_SECURE_TLS_EXTENSION_NOT_FOUND)
    {
        /* Parsed an invalid extension, return the error. */
        return(status);
    }

    if(status == NX_SECURE_TLS_EXTENSION_NOT_FOUND)
    {
            /* SNI extension not found, just return success to use the default
               certificate. */
            return(NX_SUCCESS);
    }

    /* Find the application-supplied numeric identifier for the specified DNS
       name provided by the remote client. */
    cert_id = application_find_id_by_dns_name(&dns_name);

    /* If cert_id is 0, just use the default identity certificate added with
       nx_secure_tls_local_certificate_add. */
    if(cert_id != 0)
    {
        /* Application found a matching name, find the certificate in our
           store. */
        status = nx_secure_tls_server_certificate_find(tls_session, &certificate,
                                                       cert_id);

        if(status != NX_SUCCESS)
        {
            /* Didn’t find a valid certificate with the supplied ID. Return an
               error so TLS can shut down the handshake. */
            return(NX_SECURE_TLS_CERTIFICATE_NOT_FOUND);
        }

        /* Set the active identity certificate – the certificate should have been
           added to the local store at application start with
           nx_secure_tls_local_certificate_add. */
        nx_secure_tls_active_certificate_set(session, certificate);
    }

    return(NX_SUCCESS);
}

/* TLS setup routine. */
UINT tls_setup(NX_SECURE_TLS_SESSION *tls_session)
{
        /* Add callback to TLS session.  */
        status =  nx_secure_tls_session_server_callback_set(tls_session,
                                                            server_callback);

        /* If status is NX_SUCCESS the callback was added and will be invoked
           immediately after a ClientHello message is received. */

        return(status);
}
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_tls_session_create
- nx_secure_tls_session_client_callback_set
- nx_secure_tls_active_certificate_set
- nx_secure_tls_session_sni_extension_parse
- nx_secure_tls_server_certificate_add
- nx_secure_tls_server_certificate_find

## <a name="nx_secure_tls_session_sni_extension_parse"></a>nx_secure_tls_session_sni_extension_parse

TLS İstemcisi Sunucu Adı Belirtme alınan bir Sunucu Adı Belirtme (SNI) uzantısını ayrıştırma

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_tls_session_sni_extension_parse(
                                    NX_SECURE_TLS_SESSION *session_ptr,
                                    NX_SECURE_TLS_HELLO_EXTENSION
                                    *extensions,
                                    UINT num_extensions,
                                    NX_SECURE_X509_DNS_NAME *dns_name);
```

### <a name="description"></a>Description

Bu hizmetin, bir TLS Sunucusu oturum geri çağırması içinde çağrılarak bir TLS oturumuna çağrıl nx_secure_tls_session_server_callback_set. Geri çağırma, uzak bir TLS istemcisinde ClientHello iletisinin alımından sonra çağrılır ve bir dizi kullanılabilir uzantı (ve dizide uzantı sayısı) sağlanır. Bu dizi ve uzunluğu, mevcut bir SNI uzantısı olup olmadığını belirlemek için doğrudan bu yordama geçirebilirsiniz; yoksa NX_SECURE_TLS_EXTENSION_NOT_FOUND yalnızca istemcinin SNI uzantısını provice almayı tercih etmiş olduğunu gösterir (bu bir hata değildir).

SNI uzantısı bulunursa TLS istemcisi tarafından sağlanan X.509 DNS adı, dns_name döndürülür. Şu anda SNI uzantısı yalnızca tek bir DNS adı girişi sağlar ve bu giriş TLS sunucusu tarafından uzak istemciye hangi kimlik sertifikasının gönderileceğini belirlemek için kullanılabilir.**

Bu NX_SECURE_X509_DNS_NAME, dns adını yalnızca nx_secure_x509_dns_name alanında UCHAR dizesi  olarak ve *nx_secure_x509_dns_name_length.* Makro NX_SECURE_X509_DNS_NAME_MAX arabelleğinin boyutunu nx_secure_x509_dns_name sağlar.

### <a name="parameters"></a>Parametreler

- **session_ptr** TLS Oturumu örneğinin işaretçisi.
- **Uzantılar** Bir TLS Merhaba uzantısı dizisine yönelik işaretçi (oturum geri çağırmada).
- **num_extensions** Dizideki uzantı sayısı (oturum geri çağrısından).
- **dns_name** SNı uzantısında sağlanan DNS adını döndürür.

### <a name="return-values"></a>Dönüş Değerleri

- Uzantının başarılı ayrıştırması **NX_SUCCESS** (0x00).
- **NX_PTR_ERROR** (0x07) geçersiz uzantılar DIZISI veya TLS oturum işaretçisi.
- **NX_SECURE_TLS_EXTENSION_NOT_FOUND** (0x136) SNI uzantısı bulunamadı.
- **NX_SECURE_TLS_SNI_EXTENSION_INVALID** (0x137) SNI uzantı biçimi geçersizdi.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_tls_session_server_callback_set
- nx_secure_tls_session_client_callback_set
- nx_secure_tls_server_callback_set
- nx_secure_tls_active_certificate_set

## <a name="nx_secure_tls_session_sni_extension_set"></a>nx_secure_tls_session_sni_extension_set

Bir Sunucu Adı Belirtme (SNı) uzantısı DNS adını uzak bir sunucuya göndermek üzere ayarla

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_tls_session_sni_extension_set(
                                    NX_SECURE_TLS_SESSION *session_ptr,
                                    NX_SECURE_X509_DNS_NAME *dns_name);
```

### <a name="description"></a>Description

Bu hizmet, bir TLS Istemci uygulamasının, Sunucu Adı Belirtme (SNı) TLS uzantısını kullanarak uzak bir TLS sunucusuna tercih edilen sunucu DNS adı sağlamasına izin verir. SNı uzantısı, sunucunun belirtilen sunucu tercihini temel alarak uygun kimlik sertifikası ve parametrelerini seçmesine olanak tanır. SNı uzantısı Şu anda yalnızca gönderilecek tek bir DNS adını, dolayısıyla tekil ad parametresini destekliyor. Dns_name parametresi *nx_secure_x509_dns_name_initialize* birlikte başlatılmalıdır ve istemcinin tercih edilen sunucusunu içerecek şekilde olmalıdır. Uzantı adını kaldırmak için bu hizmeti NX_NULL bir "dns_name" parametre değeri ile çağırmanız yeterlidir.

NX_SECURE_X509_DNS_NAME yapısı, DNS adını alan  *nx_secure_x509_dns_name* BIR uşar dizesi olarak ve *nx_secure_x509_dns_name_length* ad dizesinin uzunluğu olarak içerir. Makro NX_SECURE_X509_DNS_NAME_MAX arabelleğinin boyutunu nx_secure_x509_dns_name sağlar.

> [!NOTE]
> *Bu yordam, çağrılmadan nx_secure_tls_session_start veya ClientHello SNI uzantısını içermez.*

### <a name="parameters"></a>Parametreler

- **session_ptr** TLS Oturumu örneğinin işaretçisi.
- **dns_name** Uygulama tarafından sağlanan DNS adı.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) DNS sunucusu adı başarıyla ekleme.
- **NX_PTR_ERROR** (0x07) Geçersiz DNS adı veya TLS oturum işaretçisi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
#define TLS_SNI_SERVER_NAME “www.example.com”

NX_SECURE_X509_DNS_NAME dns_name;
NX_SECURE_TLS_SESSION client_tls_session;

/* Application where TLS session is started. */
void main()
{
    /* Create a TLS session for our socket. Ciphers and metadata defined
       elsewhere. See nx_secure_tls_session_create reference for more
       information. */
    status =  nx_secure_tls_session_create(&client_tls_session,
                                           &nx_crypto_tls_ciphers,
                                           server_crypto_metadata,
                                           sizeof(server_crypto_metadata));


    /* Initialize the DNS server name we want to send in the SNI extension. */
    nx_secure_x509_dns_name_initialize(&dns_name, TLS_SNI_SERVER_NAME,
                                    strlen(TLS_SNI_SERVER_NAME));

    /* The SNI server name needs to be set prior to starting the TLS session. */
    nx_secure_tls_session_sni_extension_set(&tls_session, &dns_name);

   /* Start TLS session as normal. */
}
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_tls_session_start
- nx_secure_x509_dns_name_initialize

## <a name="nx_secure_tls_session_start"></a>nx_secure_tls_session_start

NetX Güvenli TLS Oturumu Başlatma

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_tls_session_start(NX_SECURE_TLS_SESSION *session_ptr,
                                  NX_TCP_SOCKET *tcp_socket_ptr,
                                  ULONG wait_option);
```

### <a name="description"></a>Description

Bu hizmet, sağlanan TLS oturum denetim bloğu ve bağlı bir TCP yuvası kullanarak bir TLS oturumu başlatır. Tcp bağlantısının başarılı bir çağrıdan sonra ya nx_tcp_client_socket_connect veya nx_tcp_server_socket_accept.

Bu hizmet, TCP yuvasından TLS oturumunun türünü (İstemci veya Sunucu) belirler.

Bekleme seçeneği, TLS el sıkışması devam ederken hizmetin nasıl davranacağını tanımlar.

### <a name="parameters"></a>Parametreler

- **session_ptr** TLS Oturumu örneğinin işaretçisi.
- **tcp_socket_ptr** Bağlı bir TCP yuvasının işaretçisi.
- **wait_option** TLS el sıkışması devam ederken hizmetin nasıl davranacağını tanımlar.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) TLS oturumunun başarıyla başlatılıyor.
- **NX_NOT_CONNECTED** (0x38) Temel ALıNAN TCP yuvası artık bağlı değil.
- **NX_SECURE_TLS_UNRECOGNIZED_MESSAGE_TYPE** (0x102) ALıNAN bir TLS ileti türü yanlış.
- **NX_SECURE_TLS_UNSUPPORTED_CIPHER** (0x106) uzak ana bilgisayar tarafından sağlanmış bir şifre desteklenmez.
- TLS el sıkışması sırasında **NX_SECURE_TLS_HANDSHAKE_FAILURE** (0x107) ileti işleme başarısız oldu.
- **NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0x108) gelen bir ILETI karma Mac denetiminde başarısız oldu.
- **NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) temel alınan TCP yuvası gönderme başarısız oldu.
- **NX_SECURE_TLS_INCORRECT_MESSAGE_LENGTH** (0x10a) gelen iletide geçersiz uzunluk alanı vardı.
- **NX_SECURE_TLS_BAD_CIPHERSPEC** (0x10b) gelen bir Changecyaspec iletisi hatalı.
- **NX_SECURE_TLS_INVALID_SERVER_CERT** (0x10c) uzak TLS sunucusunu tanımlamak Için gelen bir TLS sertifikası kullanılamaz.
- **NX_SECURE_TLS_UNSUPPORTED_PUBLIC_CIPHER** (0x10d) uzak ana bilgisayar tarafından sunulan ortak anahtar şifresi desteklenmez.
- **NX_SECURE_TLS_NO_SUPPORTED_CIPHERS** (0x10e) uzak ana bilgisayar, NETX güvenli TLS yığını tarafından desteklenen ciphersuites belirtti.
- **NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0x10F) ALıNAN bir TLS iletisinde üst bilgisinde BILINMEYEN bir TLS sürümü vardı.
- **NX_SECURE_TLS_UNSUPPORTED_TLS_VERSION** (0x110) ALıNAN bir TLS iletisinde, üstbilgisinde bilinen ancak desteklenmeyen bir TLS sürümü vardı.
- **NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) BIR iç TLS paket ayırması başarısız oldu.
- **NX_SECURE_TLS_INVALID_CERTIFICATE** (0x112) uzak ana bilgisayar geçersiz bir sertifika sağladı.
- **NX_SECURE_TLS_ALERT_RECEIVED** (0x114) uzak ana bilgisayar bir hatayı BELIRTEN ve TLS oturumunu sonlandıran bir uyarı gönderdi.
- **NX_SECURE_TLS_MISSING_CRYPTO_ROUTINE** (0x13b) ciphersuite tablosundaki BIR girdinin null işlev işaretçisi vardı.
- **NX_SECURE_TLS_INAPPROPRIATE_FALLBACK** (0x146) BIR uzak TLS ClientHello, GERI dönüş SCSV bir sürüm geri dönüşü içeriyordu.
- **NX_PTR_ERROR** (0x07) geçersiz bir Işaretçi kullanmaya çalıştı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
NX_TCP_SOCKET tcp_socket;
NX_SECURE_TLS_SESSION tls_session;
NX_SECURE_X509_CERT certificate;

/* Initialize the TLS session structure. */
nx_secure_tls_session_create(&tls_session,
                              &nx_crypto_tls_ciphers,
                              crypto_metadata,
                              sizeof(crypto_metadata));

/* Setup the TLS packet reassembly buffer. */
status = nx_secure_tls_session_packet_buffer_set(&tls_session, tls_packet_buffer,
                                                 sizeof(tls_packet_buffer));

/* Initialize a certificate for the TLS server. */
status =  nx_secure_x509_certificate_initialize(&certificate, certificate_data, 500,
NX_NULL, 0, private_key, 64);

/* If status is NX_SUCCESS, certificate is initialized. */

/* Add the certificate a local certificate to identify this TLS server. */
status = nx_secure_tls_add_local_certificate(&tls_session, &certificate);

/* If status is NX_SUCCESS, certificate was added successfully. */

/* Create and start a TCP socket as a server. */
/* NOTE: This assumes an IP instance called “ip_0” has already been created. */

/* Create a TCP server socket on the previously created IP instance, with normal
   delivery, IP fragmentation enabled, default time to live, a 8192-byte receive
   window, no urgent callback routine, and the "client_disconnect" routine to
   handle disconnection initiated from the other end of the connection.  */
status =  nx_tcp_socket_create(&ip_0, &tcp_socket, "TLS Server Socket", NX_IP_NORMAL,
                               NX_FRAGMENT_OKAY, NX_IP_TIME_TO_LIVE, 8192, NX_NULL,
                               NX_NULL);

/* If status is NX_SUCCESS, the TCP socket was created successfully. */

/* Start up a TCP server socket by listening on port 443 with a listen queue of
   size 5. */
status =  nx_tcp_server_socket_listen(&ip_0, 443, &tcp_socket, 5, NX_NULL);

/* Application main loop. */
while(1)
{
        /* Accept incoming requests on the TCP socket. */
        status =  nx_tcp_server_socket_accept(&tcp_socket, NX_WAIT_FOREVER);

        /* At this point, the TCP socket should be established (but not the TLS
        session yet). */

        /* Start the TLS session on our active TCP socket. */
        status = nx_secure_tls_session_start(&tls_session, &tcp_socket,
                                             NX_WAIT_FOREVER);

        /* At this point, if status is NX_SUCCESS, the TLS session has been
           established.  Application may now send/receive data through this
           channel. */

        /* Send and receive data using the TLS session. */
        /* Allocate TLS packets using nx_secure_tls_packet_allocate, write data with
           nx_packet_data_append, read data with nx_packet_data_extract_offset. */

        /* Send TLS data. */
        nx_secure_tls_session_send(&tls_session, &send_packet, NX_WAIT_FOREVER);

        nx_secure_tls_session_receive(&tls_session, &receive_packet_ptr,
        NX_WAIT_FOREVER);


        /* Once all application data is sent/received, end the TLS session. */
        status = nx_secure_tls_session_end(&tls_session);

        /* If status is NX_SUCCESS, the TLS session has been closed properly. */

        /* Now disconnect the TCP server socket from the client.  */
        nx_tcp_socket_disconnect(&tcp_socket, 200);

        /* Unaccept the TCP server socket.  Note that unaccept is called even if
           disconnect or accept fails.  */
        nx_tcp_server_socket_unaccept(&tcp_socket);

        /* Setup server socket for listening with this socket again.  */
        nx_tcp_server_socket_relisten(&ip_0, 443, &tcp_socket);
}

/* When the server application is shut down, clean up the TLS session. */
nx_secure_tls_session_delete(&tls_session);

/* Finally, clean up the TCP socket as well. */
nx_tcp_socket_delete(&tcp_socket);
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_socket_receive
- nx_secure_x509_certificate_initialize
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_session_send
- nx_secure_tls_session_delete
- nx_secure_tls_session_receive
- nx_secure_tls_packet_allocate
- nx_secure_tls_session_end
- nx_secure_tls_session_create
- nx_tcp_socket_accept
- nx_tcp_socket_listen
- nx_tcp_socket_disconnect
- nx_tcp_socket_unaccept
- nx_tcp_socket_relisten
- nx_tcp_socket_delete
- nx_packet_allocate
- nx_packet_data_append
- nx_packet_data_extract_offset

## <a name="nx_secure_tls_session_time_function_set"></a>nx_secure_tls_session_time_function_set

NetX Secure TLS Oturumuna zaman damgası işlevi atama

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_tls_time_function_set(
                              NX_SECURE_TLS_SESSION *session_ptr,
                              ULONG (*time_func_ptr)(void));
```

### <a name="description"></a>Description

Bu işlev, ÇEŞITLI TLS el sıkışma iletilerinde ve sertifikaların doğrulanmasında kullanılan geçerli saati almak için TLS'nin çağıracak bir işlev işaretçisi ayarlar.

Bu işlevin, TLS RFC 5246 ' de ClientHello gereksinimlere göre geçerli GMT 'yi UNIX 32 bit biçiminde (gece yarısından itibaren 1, 1970, UTC, daha fazla saniyeler yok saydıktan sonra saniye) döndürmesi beklenir.

Zaman damgası işlevi atanmamışsa, TLS el sıkışmasındaki zaman damgası için 0 değeri kullanılır ve sertifika süre sonu denetimi çalışmaz.

### <a name="parameters"></a>Parametreler

- **session_ptr** Bir TLS oturum örneği işaretçisi.
- **time_func_ptr** UNIX 32 bit biçiminde geçerli saati (GMT) döndüren bir işlev işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- TLS oturumunun başarıyla başlatılmasından **NX_SUCCESS** (0x00).
- **NX_INVALID_PARAMETERS** (0x4D) geçersiz TLS oturum işaretçisi.
- **NX_PTR_ERROR** (0x07) geçersiz bir Işaretçi kullanmaya çalıştı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* This function returns a 32-bit UNIX-style representation of the current GMT
   time. */
ULONG get_gmt_time(void)
{
ULONG time_value;

   /* Platform-specific time calculation goes here… */

   return(time_value);
}

/* Reset a TLS session.  */
status =  nx_secure_tls_timestamp_function_set(&tls_session, get_gmt_time);


/* If status is NX_SUCCESS the function was successfully added.*/
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_x509_certificate_initialize
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_session_start
- nx_secure_tls_session_delete
- nx_secure_tls_session_sendnx_secure_tls_session_receive
- nx_secure_tls_session_create

## <a name="nx_secure_tls_trusted_certificate_add"></a>nx_secure_tls_trusted_certificate_add

NetX güvenli TLS oturumuna güvenilen sertifika ekleme

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_tls_trusted_certificate_add(NX_SECURE_TLS_SESSION
                            *session_ptr, NX_SECURE_X509_CERT *certificate_ptr);
```

### <a name="description"></a>Description

Bu hizmet, bir TLS oturumuna başlatılmış bir NX_SECURE_X509_CERT yapısı örneği ekler. Bu sertifika, TLS el sıkışması sırasında uzak ana bilgisayar tarafından sağlanan sertifikaları doğrulamak için TLS yığını tarafından kullanılır.

TLS Istemci modu için güvenilen sertifikalar gereklidir.

Güvenilen sertifikalar yalnızca istemci sertifikası kimlik doğrulaması etkinse TLS sunucu modu için gereklidir.

### <a name="parameters"></a>Parametreler

- **session_ptr** Daha önce oluşturulmuş bir TLS Oturumu örneğinin işaretçisi.
- **certificate_ptr** Başlatılan bir TLS Sertifika örneğinin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Sertifika başarıyla eksildi.
- **NX_INVALID_PARAMETERS** (0x4D) Geçersiz sertifika eklemeye çalıştı.
- **NX_PTR_ERROR** (0x07) Geçersiz TLS oturum işaretçisi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Initialize certificate structure. */
status = nx_secure_x509_certificate_initialize(&certificate, certificate_data,
                                               certificate_buffer,
                                               sizeof(certificate_buffer), 500,
                                               private_key, 64);

/* Add certificate to TLS session.  */
status =  nx_secure_tls_trusted_certificate_add(&tls_session, &certificate);


/* If status is NX_SUCCESS the certificate was successfully added.  */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_x509_certificate_initialize
- nx_secure_tls_session_create
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_trusted_certificate_remove

## <a name="nx_secure_tls_trusted_certificate_remove"></a>nx_secure_tls_trusted_certificate_remove

NetX Secure TLS Oturumundan güvenilen sertifikayı kaldırma

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_tls_trusted_certificate_remove(
                                    NX_SECURE_TLS_SESSION *session_ptr,
                                    UCHAR *common_name,
                                    UINT common_name_length);
```

### <a name="description"></a>Description

Bu hizmet, sertifikadaki Ortak Ad alanına anahtarlanan bir TLS oturumundan güvenilen bir sertifikayı kaldırır.

### <a name="parameters"></a>Parametreler

- **session_ptr** Daha önce oluşturulmuş bir TLS Oturumu örneğinin işaretçisi.
- **common_name** Kaldırılacak sertifikanın Ortak Ad değeri.
- **common_name_length** Ortak Ad dizesinin uzunluğu.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Sertifika başarıyla eksildi.
- **NX_PTR_ERROR** (0x07) Geçersiz TLS oturum işaretçisi.
- **NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) Sertifikası bulunamadı.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Remove certificate from TLS session.  */
status =  nx_secure_tls_trusted_certificate_remove(&tls_session,
                                                “www.example.com”, 15);


/* If status is NX_SUCCESS the certificate was successfully removed.  */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_x509_certificate_initialize
- nx_secure_tls_session_create
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_trusted_certificate_add

## <a name="nx_secure_x509_certificate_initialize"></a>nx_secure_x509_certificate_initialize

NetX güvenli TLS için X. 509.440 sertifikasını başlatın

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_x509_certificate_initialize(
                  NX_SECURE_X509_CERT *certificate_ptr,
                  const UCHAR *certificate_data,
                  USHORT certificate_data_length,
                  UCHAR *raw_data_buffer,
                  USHORT buffer_size,
                  const UCHAR *private_key_data,
                  USHORT private_key_data_length,
                  UINT private_key_type);
```

### <a name="description"></a>Description

Bu hizmet, bir TLS oturumunda kullanılmak üzere ikili kodlanmış X. 509.952 dijital sertifikasından bir NX_SECURE_X509_CERT yapısını başlatır.

Sertifika verileri, DER kodlu ikili biçimde geçerli bir X. 509.952 dijital sertifikası **olmalıdır** . Veriler, bu verilere yönelik bir uşar işaretçisi sağlandığı sürece herhangi bir kaynaktan (ör. dosya sistemi, derlenmiş sabit arabellek, vb.) oluşabilir.

*Raw_data_buffer* parametresi ve boyutu, sertifika verilerinin ayrıştırılmadan önce kopyalandığı ayrılmış bir arabelleği belirten isteğe bağlı parametrelerdir. Raw_data_buffer NX_NULL olarak geçirilirse NX_SECURE_X509_CERT yapısı doğrudan certificate_data dizisine işaret eder (Bu durumda buffer_size yok sayılır). Raw_data_buffer NX_NULL olarak geçirilirse certificate_data işaretçisi tarafından işaret edilen ***verileri değiştirmeyin veya*** sertifika işleme muhtemelen başarısız olur!

Özel anahtar parametresi yerel kimlik sertifikalarına yöneliktir. özel anahtar, sunucular tarafından bir istemciden gelen anahtar verilerinin şifresini çözmek (sunucunun ortak anahtarı kullanılarak şifrelenir) ve istemciler tarafından sunucu istemci sertifikası istediğinde bir sunucuya kimliklerini doğrulamak için kullanılır. Bu API 'ye özel anahtar eklemek, ilişkili sertifikayı bir TLS uygulaması için kimlik sertifikası olarak otomatik olarak işaretler. Sertifikaları diğer amaçlar için başlatırken (örn. güvenilen mağaza), *private_key_data* parametresi null, 0 olarak *private_key_data_length* ve *private_key_type* NX_SECURE_X509_KEY_TYPE_NONE olarak geçirilmelidir.

*Private_key_type* parametresi, özel anahtarın biçimlendirmesini belirtir. Örneğin, özel anahtar DER ile kodlanmış PKCS#1 biçimli bir RSA özel anahtarı ise, netx secure olarak bilinen bir tür olan private_key_type, hemen ayrıştıracak ve daha sonra kullanmak üzere kaydedecek olan NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER olarak geçirilmelidir.

Bu private_key_type, belirli anahtar biçimlerine veya diğer ihtiyaçlarına sahip platformlar ve uygulamalar için kullanıcı tanımlı anahtar türleri<sup>23'ü</sup> de destekler. Örneğin, donanım tabanlı bir şifreleme altyapısı NetX Secure yazılımı tarafından anlaşılmayan belirli bir biçim kullanabilir veya bir özel anahtar şifrelenir veya bir şifreleme belirteci ile temsil edilir. Bu durum Güvenilir Platform Modülü (TPM) veya PKCS#11 şifreleme donanımıyla da olabilir. Kullanıcı tanımlı bir anahtar türü kullanılırken, anahtar verileri uygun şifreleme yordamına tam olarak geçirılır. Örneğin, herhangi bir ayrıştırma veya işleme olmadan doğrudan şifreleme tablosunda TLS'ye sağlanan RSA şifreleme yordamına bir RSA özel anahtarı geçirilebilirsiniz. Kullanıcı tanımlı anahtar türü de şifreleme yordamına geçirildi (RSA söz konusu ise bu "op" parametresidir).

Kullanıcı tanımlı anahtar aralığı, 0000-0xFFFF FFFF aralığından 32 bitlik bir imzasız tamsayının üst 0x0001 kapsar. 0000'0x0001 küçük değerler NetX Secure kullanımı için ayrılmıştır.

Kullanıcı tanımlı anahtar türleri, ham özel anahtar verilerini işlemek için özel şifreleme yordamları gerektiren gelişmiş bir özelliktir. Bu özel şeye ihtiyacınız varsa lütfen Express Logic temsilcinize başvurun.

### <a name="parameters"></a>Parametreler

- **certificate_ptr** Uninitialized X.509 Sertifika örneğinin işaretçisi.
- **certificate_data** DER ile kodlanmış X.509 ikili verileri işaretçisi.
- **raw_data_buffer** İsteğe bağlı ayrılmış sertifika veri arabelleği işaretçisi.
- **buffer_size** İsteğe bağlı ayrılmış sertifika veri arabelleğinin boyutu.
- **certificate_data_length** Sertifika ikili verilerinin bayt cinsinden uzunluğu.
- **private_key_data** İsteğe bağlı özel anahtar verilerine işaretçi.
- **private_key_data_length** Özel anahtar verisi uzunluğu.
- **private_key_type** Anahtar türü tanımlayıcısı.

### <a name="return-values"></a>Dönüş Değerleri

- Sertifikanın başarılı bir şekilde eklenmesi **NX_SUCCESS** (0x00).
- **NX_PTR_ERROR** (0x07) geçersiz bir Işaretçi kullanmaya çalıştı.
- **NX_SECURE_TLS_INVALID_CERTIFICATE** (0x112) SERTIFIKA verileri der-Encoded X. 509.952 sertifikası içermiyordu.
- **NX_SECURE_TLS_UNSUPPORTED_PUBLIC_CIPHER** (0x10d) sertifikada NETX güvenli tarafından desteklenen bir ortak anahtar şifresi yoktu.
- **NX_SECURE_X509_INVALID_CERTIFICATE_SEQUENCE** (0x186) özel anahtar veya sertifika GEÇERLI bir ASN. 1 sırası içermiyordu.
- **NX_SECURE_PKCS1_INVALID_PRIVATE_KEY** (0x18a) belirtilen özel anahtar GEÇERLI bir PKCS # 1 RSA anahtarı değildi.
- **NX_SECURE_X509_INVALID_PRIVATE_KEY_TYPE** (0x19d) belirtilen özel anahtar türü kullanıcı tanımlı değildi ve bilinen hiçbir türle eşleşmedi.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Initialize certificate structure. The certificate structure will point directly
   into the certificate_data array since we are passing the raw_data_buffer as
   NX_NULL. This certificate has a private key so it will be used to identify this
   device. */
status =  nx_secure_x509_certificate_initialize(&certificate, certificate_data,
500, NX_NULL, 0, private_key, 64, NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);


/* If status is NX_SUCCESS the certificate was successfully initialized.  */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_local_certificate_add
- nx_secure_tls_session_create
- nx_secure_tls_remote_certificate_allocate
- Bölüm 3 ' te X. 509.440 sertifikalarını NetX güvenli olarak içeri aktarma.

## <a name="nx_secure_x509_common_name_dns_check"></a>nx_secure_x509_common_name_dns_check

X. 509.440 sertifikasıyla DNS adını denetle

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_x509_common_name_dns_check(
                        NX_SECURE_X509_CERT *certificate,
                        const UCHAR *dns_tld, UINT dns_tld_length);
```

### <a name="description"></a>Description

Bu hizmet, uzak bir ana bilgisayarın DNS doğrulaması amacıyla arayan tarafından belirtilen bir üst etki alanı adına (TLD) karşı bir sertifikanın ortak adını denetler. Bu yardımcı program işlevi, uygulama tarafından verilen bir sertifika doğrulama geri çağırma yordamının içinden çağrılması amaçlanmıştır. TLD adı, uzak ana bilgisayara erişmek için kullanılan URL 'nin en üst bölümü olmalıdır ("." ilk eğik çizgiden önce ayrılmış dize). Ortak ad bir joker karakter (örn *. example.com) içeriyorsa, joker karakter aynı soneke sahip herhangi biriyle eşleşir. Joker karakter eşleştirmesi için yalnızca ilk joker ("*") ile karşılaşılan (sağdan sola okuma) değerlendirildiğini unutmayın; Örneğin, ABC. *. example. com, ". example.com" ile biten *Tüm* ad ile eşleşir.

Ortak ad, belirtilen dizeyle eşleşmezse, "subjectAltName" uzantısı ayrıştırılır (sertifikada varsa) ve herhangi bir DNSName girdisi de karşılaştırılır. Bu girdilerden hiçbiri eşleşmezse bir hata döndürülür.

Beklenen sertifikalarda ortak adın (ve subjectAltName girdilerinin) biçimini anlamak önemlidir. Örneğin, bazı sertifikalar ham IP adresi veya joker karakter kullanabilir. DNS TLD dizesi, alınan sertifikalarda beklenen değerlerle eş olacak şekilde biçimlendirildi olmalıdır.

### <a name="parameters"></a>Parametreler

- **certificate_ptr** X.509 Sertifika örneğinin işaretçisi.
- **dns_tld** Top-Level etki alanı adını seçin.
- **dns_tld_length** TLD dizesinin uzunluğu.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Ortak Ad veya subjectAltName ile başarılı karşılaştırma.
- **NX_SECURE_X509_CERTIFICATE_DNS_MISMATCH** (0x195) Eşleşen ad bulunamadı.
- **NX_PTR_ERROR** (0x07) Geçersiz bir işaretçi kullanmayı denedi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Callback routine used to perform additional checks on a certificate. */
ULONG certificate_callback(NX_SECURE_TLS_SESSION *session, NX_SECURE_X509_CERT
*certificate)
{
ULONG status;
UCHAR *tld = “www.example.com”;

    /* Check our DNS TLD against the certificate provided by the
       remote TLS host. */
    status = nx_secure_x509_common_name_dns_check(certificate, tld, strlen(tld));

        if(status != NX_SUCCESS)
        {
            /* TLD did not match any names in the certificate. */
            return(status);
        }

        /* DNS validation and any other checks were successful. */
        return(NX_SUCCESS);
}

…

/* Add callback to TLS session in TLS setup routine.  */
status =  nx_secure_tls_session_certificate_callback_set(&tls_session,
                                                         certificate_callback);
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_tls_session_create
- nx_secure_tls_session_certificate_callback_set
- nx_secure_x509_crl_revocation_check

## <a name="nx_secure_x509_crl_revocation_check"></a>nx_secure_x509_crl_revocation_check

Sağlanan bir Sertifika İptal Listesi (CRL) için X.509 Sertifikasını denetleme

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_x509_crl_revocation_check(const UCHAR *crl_data,
                              UINT crl_length,
                              NX_SECURE_X509_CERTIFICATE_STORE *store,
                              NX_SECURE_X509_CERT *certificate);
```

### <a name="description"></a>Description

Bu hizmet DER kodlanmış Sertifika İptal Listesi alır ve bu listede belirli bir sertifikayı arar. CRL'nin sertifikayı teslim alan kişi, sağlanan bir sertifika deposuna göre doğrulanır, CRL'nin sertifikayı teslim alanla aynı olduğu doğrulanır ve iptal edilen sertifika listesinde arama yapmak için söz konusu sertifikanın seri numarası kullanılır. Sertifikayı alanlar eşlenirse, imza  onaylar ve sertifika listede yoksa, çağrı başarılı olur. Diğer tüm durumlar bir hatanın döndürül yollarına neden olur.

### <a name="parameters"></a>Parametreler

- **crl_data** DER ile kodlanmış CRL'nin işaretçisi.
- **crl_length** CRL verilerinin bayt cinsinden uzunluğu.
- **Mağaza** X. 509.440 sertifika deposuna yönelik işaretçi.
- **certificate_ptr** X. 509.440 sertifika örneği işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) sertifikanın iptal edilmediğini doğrulama başarılı oldu.
- **NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) CRL veren sertifikası bulunamadı.
- **NX_SECURE_TLS_ISSUER_CERTIFICATE_NOT_FOUND** 0x11b) sertifika veren sertifikası bulunamadı.
- **NX_SECURE_X509_ASN1_LENGTH_TOO_LONG** (0x182) CRL ASN. 1, geçersiz bir uzunluk alanı içeriyordu.
- **NX_SECURE_X509_UNEXPECTED_ASN1_TAG (0x189)** CRL geçersiz ASN. 1 içeriyordu.
- **NX_SECURE_X509_CHAIN_VERIFY_FAILURE** (0x18C) bir sertifika zinciri doğrulaması başarısız oldu.
- **NX_SECURE_X509_CRL_ISSUER_MISMATCH** (0x197) CRL ve sertifika verenler eşleşmedi.
- **NX_SECURE_X509_CRL_SIGNATURE_CHECK_FAILED** 0x198) CRL imzası geçersizdi.
- **NX_SECURE_X509_CRL_CERTIFICATE_REVOKED** (0x199) denetlenen sertifika CRL 'de bulundu ve bu nedenle iptal edildi.
- **NX_PTR_ERROR** (0x07) geçersiz bir Işaretçi kullanmaya çalıştı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* CRL obtained for the expected certificate issuer through some means (downloaded
   from server manually, obtained from CRL endpoint, etc…) */
const UCHAR *crl_data;
UINT crl_length = 300;

/* Callback routine used to perform additional checks on a certificate. */
ULONG certificate_callback(NX_SECURE_TLS_SESSION *session, NX_SECURE_X509_CERT
*certificate)
{
ULONG status;
NX_SECURE_X509_CERTIFICATE_STORE *store;

    /* Obtain a certificate store to check against. In the certificate callback,
       it usually makes the most sense to use the store associated with the TLS
       session. */
    store = &session -> nx_secure_tls_credentials.nx_secure_tls_certificate_store;

    /* Check our certificate against the CRL and TLS certificate store. */
    status = nx_secure_x509_crl_revocation_check(crl, crl_length, store,
                                                 certificate);

        if(status != NX_SUCCESS)
        {
            if(status == NX_SECURE_X509_CRL_CERTIFICATE_REVOKED)
            {
                /* Certificate was revoked. */
               return(status);
            }
            else
            {
               /* CRL was invalid or some other issue. In this case the certificate
                  may still be valid since the CRL itself was a problem. At this
                  point it is up to the application to decide whether to continue
                  with the TLS handshake. For this example, assume certificate is
                  valid (faulty CRL is a possible Denial-of-Service attack).*/
               status = NX_SUCCESS;
        }

    /* Other certificate checking can go here. */

    /* Return status of certificate checks. */
    return(status);
}

…

/* Add callback to TLS session in TLS setup routine.  */
status =  nx_secure_tls_session_certificate_callback_set(&tls_session,
                                                         certificate_callback);
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_tls_session_create
- nx_secure_tls_session_certificate_callback_set
- nx_secure_x509_common_name_dns_check

## <a name="nx_secure_x509_dns_name_initialize"></a>nx_secure_x509_dns_name_initialize

X. 509.440 DNS adı yapısını başlatma

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_x509_dns_name_initialize(
                        NX_SECURE_X509_DNS_NAME *dns_name,
                        const UCHAR *name_string, UINT length);
```

### <a name="description"></a>Description

Bu hizmet belirli bir ad biçimi gerektiren belirli API hizmetleriyle kullanılmak üzere bir X. 509.440 DNS adı başlatır. Örneğin, *nx_secure_tls_sni_extension_parse* hizmeti, TLS el sıkışması sırasında NX_SECURE_X509_DNS_NAME uzantısında uzak bir ana bilgisayar tarafından sağlanan adla eşleşmesi için Sunucu Adı Belirtme nesnesi bekler. DNS adı yalnızca uzunluğu olan bir karakter dizesidir. Bir DNS adının izin verilen en uzun uzunluğu (ve NX_SECURE_X509_DNS_NAME'daki iç arabelleğin boyutu) makro NX_SECURE_X509_DNS_NAME_MAX (varsayılan 100 bayt) tarafından denetlenmektedir.

### <a name="parameters"></a>Parametreler

- **dns_name** Başlat için DNS ad yapısı.
- **name_string** DNS ad dizesi verileri.
- **uzunluk** Ad dizesinin uzunluğu.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı başlatma.
- **NX_SECURE_X509_NAME_STRING_TOO_LONG** (0x19E) Verilen ad dizesi NX_SECURE_X509_DNS_NAME_MAX.
- **NX_PTR_ERROR** (0x07) Geçersiz bir işaretçi kullanmayı denedi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
NX_SECURE_X509_DNS_NAME dns_name;

/* Initialize DNS name. */
status = nx_secure_x509_dns_name_initialize(&dns_name, “www.example.com”,
                                            strlen(“www.example.com”);

/* Use initialized DNS name to send the Server Name Indication extension to the
   remote TLS server. */
status = nx_secure_tls_session_sni_extension_set(&tls_session, &dns_name);
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_tls_session_create
- nx_secure_tls_session_sni_extension_parse
- nx_secure_tls_session_sni_extension_set

## <a name="nx_secure_x509_extended_key_usage_extension_parse"></a>nx_secure_x509_extended_key_usage_extension_parse

X.509 sertifikasında X.509 genişletilmiş anahtar kullanımı uzantısını bulma ve ayrıştırma

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_x509_extended_key_usage_extension_parse(
                        NX_SECURE_X509_CERT *certificate,
                        UINT key_usage);
```

### <a name="description"></a>Description

Bu hizmetin bir sertifika doğrulama geri çağırma içinde çağrılma amacı vardır (bkz. *nx_secure_tls_session_certificate_callback_set).* Bir X.509 sertifikası içinde belirli bir genişletilmiş anahtar kullanımı OID'sını aratır ve OID'nin mevcut olup olmadığını gösterir. key_usage parametresi, değişken uzunluklu OID dizelerini parametre olarak geçirmemek için NetX Secure X.509 ve TLS tarafından dahili olarak kullanılan OID'lere bir tamsayı eşlemesidir.

Genişletilmiş anahtar kullanım uzantısı için ilgili OID'ler aşağıdaki tabloda verilmiştir. Alınan bir TLS sunucu sertifikasında genişletilmiş anahtar kullanımını kontrol etmek isteyen tipik bir TLS İstemcisi uygulaması, uzantı mevcutsa ancak OID mevcutsa NX_SECURE_TLS_X509_TYPE_PKIX_KP_SERVER_AUTH, sertifikanın ana bilgisayarı TLS sunucusu olarak tanımlay için geçersiz olarak kabul edilir ve sertifika doğrulama geri çağırma bir hata döndürür. Uzantının kendisi eksikse, TLS el sıkışması ile devam edilip edilmeyeceğini uygulamaya göre yapılır.

Sertifika doğrulama geri çağrısında hata dönüş kodu NX_SECURE_X509_KEY_USAGE_ERROR, uygulama kullanımı için ayrılmıştır. Anahtar kullanımını denetlerken bir hata oluşursa, hatanın nedenini göstermek için bu değer geri aramadan döndürülür.

| NetX güvenli tanımlayıcısı                                | OID değeri         | Description                                      |
| --------------------------------------------------------- | --------------------- | ---------------------------------------------------- |
| NX_SECURE_TLS_X509_TYPE_PKIX_KP_SERVER_AUTH   | 1.3.6.1.5.5.7.3.1 | Sertifika, bir TLS sunucusunu tanımlamak için kullanılabilir |
| NX_SECURE_TLS_X509_TYPE_PKIX_KP_CLIENT_AUTH   | 1.3.6.1.5.5.7.3.2 | Sertifika, bir TLS istemcisini tanımlamak için kullanılabilir |
| NX_SECURE_TLS_X509_TYPE_PKIX_KP_CODE_SIGNING  | 1.3.6.1.5.5.7.3.3 | Sertifika, kodu imzalamak için kullanılabilir             |
| NX_SECURE_TLS_X509_TYPE_PKIX_KP_EMAIL_PROTECT | 1.3.6.1.5.5.7.3.4 | Sertifika, e-postaları imzalamak için kullanılabilir           |
| NX_SECURE_TLS_X509_TYPE_PKIX_KP_TIME_STAMPING | 1.3.6.1.5.5.7.3.8 | Sertifika, zaman damgalarını imzalamak için kullanılabilir       |
| NX_SECURE_TLS_X509_TYPE_PKIX_KP_OCSP_SIGNING  | 1.3.6.1.5.5.7.3.9 | OCSP yanıtlarını imzalamak için sertifika kullanılabilir   |

X.509 Genişletilmiş Anahtar Kullanımı Uzantısı için OID'ler ve eşlemeler

### <a name="parameters"></a>Parametreler

- **sertifika** Doğrulanan sertifikanın işaretçisi.
- **key_usage** Yukarıdaki tablodan OID tamsayı eşlemesi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Belirtilen anahtar kullanımı OID bulundu.
- **NX_SECURE_X509_MULTIBYTE_TAG_UNSUPPORTED** (0x181) ASN.1 çoklu bayt etiketiyle karşılaşıldı (desteklenmeyen sertifika).
- **NX_SECURE_X509_ASN1_LENGTH_TOO_LONG** (0x182) Invaild ASN.1 alanıyla karşılaşıldı (geçersiz sertifika).
- **NX_SECURE_X509_INVALID_TAG_CLASS** (0x190) Geçersiz ASN.1 etiket sınıfıyla karşılaşıldı (geçersiz sertifika).
- **NX_SECURE_X509_INVALID_EXTENSION_SEQUENCE** (0x192) Geçersiz uzantıyla karşılaşıldı (geçersiz sertifika).
- **NX_SECURE_X509_EXTENSION_NOT_FOUND** (0x19B) Genişletilmiş Anahtar Kullanımı uzantısı sağlanan sertifikada bulunamadı.
- **NX_PTR_ERROR** (0x07) Geçersiz sertifika işaretçisi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
ULONG certificate_verification_callback(NX_SECURE_TLS_SESSION *session, NX_SECURE_X509_CERT* certificate)
{
UINT status;

    /* Extended key usage - look for specific OIDs. */
    status = nx_secure_x509_extended_key_usage_extension_parse(certificate,
                        NX_SECURE_TLS_X509_TYPE_PKIX_KP_SERVER_AUTH);

    if(status != NX_SUCCESS)
    {
        if(NX_SECURE_X509_EXT_KEY_USAGE_NOT_FOUND)
        {
            printf("Extended key usage extension not found or specified key usage OID not
                    provided in extension.\n");
            /* The certificate was valid but the specified OID was not found. The
               application can decide whether to continue or abort the TLS handshake. */
            return(NX_SECURE_X509_KEY_USAGE_ERROR);
        }
        else
        {
            /* The extension or certificate was invalid. */
            return(status);
        }
    }

    /* The specified OID was found, return success! */
    return(NX_SUCCESS);
}
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_tls_session_certificate_callback_set
- nx_secure_x509_key_usage_extension_parse
- nx_secure_x509_crl_revocation_check
- nx_secure_x509_common_name_dns_check
- nx_secure_x509_extension_find

## <a name="nx_secure_x509_extension_find"></a>nx_secure_x509_extension_find

X. 509.440 sertifikasında bir X. 509.440 uzantısı bulun ve döndürün

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_x509_extension_find(
                        NX_SECURE_X509_CERT *certificate,
                        NX_SECURE_X509_EXTENSION *extension,
                        USHORT extension_id);
```

### <a name="description"></a>Description

Bu hizmetin bir sertifika doğrulama geri çağırması içinden çağrılması amaçlanmıştır (bkz. *nx_secure_tls_session_certificate_callback_set)* ve gelişmiş bir X. 509.440 hizmetidir.

İşlevi, bir OID 'ye dayalı bir X. 509.440 sertifikası içindeki belirli bir uzantıyı arar ve OID 'nin mevcut ham uzantı verilerine yönelik başvuruları içeren bir yapıyla birlikte, OID 'nin var olup olmadığını döndürür. Extension_id parametresi, değişken uzunluklu OID dizelerinin parametre olarak geçirilmesini önlemek için NetX güvenli X. 509.440 ve TLS tarafından dahili olarak kullanılan OID 'lerin bir tamsayı eşlemesidir.

Belirli Uzantılar için belirtilen yardımcı işlevler ( *nx_secure_x509_key_usage_extension_parse*) çağrısı, dahili olarak uzantı verilerini almak için nx_secure_x509_extension_find.

Bilinen X. 509.440 uzantıları için ilgili OID 'ler aşağıdaki tabloda verilmiştir.

NX_SECURE_X509_EXTENSION yapısı, X. 509.952 sertifikasına, *nx_secure_x509_key_usage_extension_parse* gibi yardımcı işlevlere, ham uzantının der kodlu ASN. 1 verilerini hızlıca çözmesini sağlayan işaretçiler içerir.

Belirli uzantılar hakkında daha fazla bilgi için bkz. RFC 5280 (X. 509.440 belirtimi) veya varsa uygun yardımcı işlevleri başvurusu.

NetX Secure X. 509.440 sürümünün geçerli sürümü, X. 509.440 uzantıları için sınırlı desteğe sahip. Daha sonra daha fazla yardımcı işlev eklenecektir.

> [!IMPORTANT]
> *Bu hizmet, X. 509.440 uzantılarına ve DER kodlu ASN. 1 ' i bilen kullanıcılara yönelik gelişmiş bir özelliktir. Bu kullanıcıların, NetX Secure X. 509.952 'in Şu anda yardımcı işlevler sağlamayan uzantılara erişmesini sağlamak için sağlanmıştır. Yardımcı işlevleri olmayan bu uzantılar için ham DER kodlu ASN. 1 ' i kendiniz ayrıştırmanıza gerek olacaktır.*

| NetX güvenli tanımlayıcısı                              | OID değeri | Description                                                                    | Yardımcı işlevi? |
| ------------------------------------------------------- | ------------- | ---------------------------------------------------------------------------------- | -------------------- |
| NX_SECURE_TLS_X509_TYPE_DIRECTORY_ATTRIBUTES  | 2.5.29.9  | Dizin öznitelikleri – sertifika konusu hakkında temel bilgi öznitelikleri  | No               |
| NX_SECURE_TLS_X509_TYPE_SUBJECT_KEY_ID       | 2.5.29.14 | Belirli bir ortak anahtarı tanımlamak için kullanılır                                         | No               |
| NX_SECURE_TLS_X509_TYPE_KEY_USAGE             | 2.5.29.15 | Sertifika ortak anahtarı için geçerli kullanımlar hakkında bilgi sağlar              | Yes              |
| NX_SECURE_TLS_X509_TYPE_SUBJECT_ALT_NAME     | 2.5.29.17 | Sertifikayı tanımlamak için alternatif DNS adları sağlar                     | Evet<sup>24</sup>        |
| NX_SECURE_TLS_X509_TYPE_ISSUER_ALT_NAME      | 2.5.29.18 | Sertifikayı vereni tanımlamak için alternatif DNS adları sağlar            | No               |
| NX_SECURE_TLS_X509_TYPE_BASIC_CONSTRAINTS     | 2.5.29.19 | Temel sertifika kullanım kısıtlaması bilgilerini sağlar                        | No               |
| NX_SECURE_TLS_X509_TYPE_NAME_CONSTRAINTS      | 2.5.29.30 | Sertifika adlarını belirli etki alanlarıyla sınırlamak için kullanılır                        | No               |
| NX_SECURE_TLS_X509_TYPE_CRL_DISTRIBUTION      | 2.5.29.31 | CRL dağıtımı için URL'ler sağlar                                             | No               |
| NX_SECURE_TLS_X509_TYPE_CERTIFICATE_POLICIES  | 2.5.29.32 | Büyük PKI sistemleri için sertifika ilkeleri listesi                             | No               |
| NX_SECURE_TLS_X509_TYPE_CERT_POLICY_MAPPINGS | 2.5.29.33 | CA sertifika ilkelerinin listesi                                                | No               |
| NX_SECURE_TLS_X509_TYPE_AUTHORITY_KEY_ID     | 2.5.29.35 | Bir sertifika imzasıyla ilişkili belirli bir ortak anahtarı tanımlamak için kullanılır | No               |
| NX_SECURE_TLS_X509_TYPE_POLICY_CONSTRAINTS    | 2.5.29.36 | CA ilkesi kısıtlamaları                                                          | No               |
| NX_SECURE_TLS_X509_TYPE_EXTENDED_KEY_USAGE   | 2.5.29.37 | Ek OID tabanlı anahtar kullanımı bilgileri                                     | Yes              |
| NX_SECURE_TLS_X509_TYPE_FRESHEST_CRL          | 2.5.29.46 | Delta CRL 'Leri alma hakkında bilgi sağlar                                  | No               |
| NX_SECURE_TLS_X509_TYPE_INHIBIT_ANYPOLICY     | 2.5.29.54 | AnyPolicy 'in kullanılamayacağını gösteren CA sertifikası alanı                  | No               |

X.509 Uzantıları için OID'ler ve eşlemeler

24. SubjectAltName uzantısı, hizmet hizmet denetiminde DNS adı denetimi kapsamında ayrıştır nx_secure_x509_common_name_dns_check.

### <a name="parameters"></a>Parametreler

- **sertifika** Doğrulanan sertifikanın işaretçisi.
- **uzantı** Uzantı veri işaretçisi ve uzunluğu içeren dönüş yapısı.
- **extension_id** Yukarıdaki tablodan OID tamsayı eşlemesi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Belirtilen uzantı OID bulundu ve veriler döndürüldü.
- **NX_SECURE_X509_MULTIBYTE_TAG_UNSUPPORTED** (0x181) ASN.1 çoklu bayt etiketiyle karşılaşıldı (desteklenmeyen sertifika).
- **NX_SECURE_X509_ASN1_LENGTH_TOO_LONG** (0x182) Invaild ASN.1 alanıyla karşılaşıldı (geçersiz sertifika).
- **NX_SECURE_X509_INVALID_TAG_CLASS** (0x190) Geçersiz ASN.1 etiket sınıfıyla karşılaşıldı (geçersiz sertifika).
- **NX_SECURE_X509_INVALID_EXTENSION_SEQUENCE** (0x192) Geçersiz uzantıyla karşılaşıldı
- **NX_SECURE_X509_EXTENSION_NOT_FOUND** (0x19B) Verilen uzantı OID'i sağlanan sertifikada bulunamadı.
- **NX_PTR_ERROR** (0x07) Geçersiz sertifika veya uzantı işaretçisi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Function to parse a Basic Constraints X.509 extension. */
UINT _basic_constraints_extension_parse(NX_SECURE_X509_CERT *certificate)
{
const UCHAR             *current_buffer;
ULONG                    length;
UINT                     status;
NX_SECURE_X509_EXTENSION extension_data;

    /* Find the Basic Constraints extension in the certificate. */
    status = _nx_secure_x509_extension_find(certificate, &extension_data,
                              NX_SECURE_TLS_X509_TYPE_BASIC_CONSTRAINTS);

    /* See if extension present - it might be OK if not present! */
    if (status != NX_SUCCESS)
    {
        return(status);
    }

    /* The extension_data structure now points to the raw extension ASN.1
      (DER-encoded). */
    current_buffer = extension_data.nx_secure_x509_extension_data;
    length = extension_data.nx_secure_x509_extension_data_length;

   /* Extension ASN.1 parsing… */

   return(NX_SUCCESS);
}
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_tls_session_certificate_callback_set
- nx_secure_x509_key_usage_extension_parse
- nx_secure_x509_crl_revocation_check
- nx_secure_x509_common_name_dns_check
- nx_secure_x509_extended_key_usage_extension_parse

## <a name="nx_secure_x509_key_usage_extension_parse"></a>nx_secure_x509_key_usage_extension_parse

X.509 sertifikasında X.509 Anahtar Kullanımı uzantısını bulma ve ayrıştırma

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_x509_key_usage_extension_parse(
                        NX_SECURE_X509_CERT *certificate,
                        USHORT *bitfield);
```

### <a name="description"></a>Description

Bu hizmetin bir sertifika doğrulama geri çağırması içinden çağrılması amaçlanmıştır (bkz. *nx_secure_tls_session_certificate_callback_set)*. Anahtar kullanımı uzantısını arar ve bulunursa "bit alanından" parametresindeki anahtar kullanımı bitalanını döndürür.

X. 509.440 belirtimi (RFC 5280) tarafından tanımlanan bitler aşağıdaki tabloda verilmiştir. Bit düzeyinde AND ve uygun bit maskesi (sıfır olmayan), her bitin değerini verir.

Bit alanından 'ın der-Encoding değeri, diğer sıfırları ortadan kaldırdığına göre, ham sertifika verilerinde bitlerin gerçek konumunun kodu çözülmüş bit alanından ' daki konumlarından farklı olacaktır. Sağlanan bit maskeleri, ham der kodlu sertifika verileriyle değil, yalnızca *nx_secure_x509_key_usage_extension_parse* tarafından döndürülen kodu çözülmüş bit alanından üzerinde kullanılmak üzere tasarlanmıştır.

Sertifika doğrulama geri çağrısında hata dönüş kodu NX_SECURE_X509_KEY_USAGE_ERROR, uygulama kullanımı için ayrılmıştır. Anahtar kullanımını denetlerken bir hata oluşursa, hatanın nedenini göstermek için bu değer geri aramadan döndürülür.

| NetX güvenli tanımlayıcısı                            | Bit konumu | Description                                                                                                                                                  |
| ----------------------------------------------------- | ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| NX_SECURE_X509_KEY_USAGE_DIGITAL_SIGNATURE  | 0            | Sertifika, dijital imzalar için kullanılabilir                                                                                                               |
| NX_SECURE_X509_KEY_USAGE_NON_REPUDIATION    | 1            | Sertifika, sertifikalar ve CRL 'Ler dışında dijital imzaları doğrulamak için kullanılabilir                                                              |
| NX_SECURE_X509_KEY_USAGE_KEY_ENCIPHERMENT   | 2            | Sertifika, simetrik anahtarları şifrelemek için kullanılabilir (anahtar aktarımı)                                                                                            |
| NX_SECURE_X509_KEY_USAGE_DATA_ENCIPHERMENT  | 3            | Sertifika, ham Kullanıcı verilerini doğrudan şifrelemek için kullanılabilir (seyrek)                                                                                         |
| NX_SECURE_X509_KEY_USAGE_KEY_AGREEMENT      | 4            | Sertifika, anahtar anlaşması için kullanılabilir (Diffie-Hellman ' de olduğu gibi)                                                                                           |
| NX_SECURE_X509_KEY_USAGE_KEY_CERT_SIGN     | 5            | Sertifika, diğer sertifikaları imzalamak ve doğrulamak için kullanılabilir (sertifika bir CA veya ICA sertifikasıdır).                                                  |
| NX_SECURE_X509_KEY_USAGE_CRL_SIGN           | 6            | CRL'lerde imzaları doğrulamak için sertifika ortak anahtarı kullanılır                                                                                                  |
| NX_SECURE_X509_KEY_USAGE_ENCIPHER_ONLY      | 7            | Anahtar Sözleşmesi biti (bit 4) ile kullanılır– ayar olduğunda, sertifika anahtarı yalnızca anahtar sözleşmesi sırasında şifrelemek için kullanılabilir. Anahtar Sözleşmesi biti ayarlanmamışsa tanımsız. |
| NX_SECURE_X509_KEY_USAGE_DECIPHER_ONLY      | 8            | Anahtar Sözleşmesi biti (bit 4) ile kullanılır– ayar olduğunda, sertifika anahtarı yalnızca anahtar sözleşmesi sırasında şifresini çözmek için kullanılabilir. Anahtar Sözleşmesi biti ayarlanmamışsa tanımsız. |

X.509 Anahtar Kullanımı Uzantısı için Bit maskeleri ve değerleri

### <a name="parameters"></a>Parametreler

- **sertifika** Doğrulanan sertifikanın işaretçisi.
- **bitfield** Uzantıdan bitfield'in tamamını iade.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Anahtar kullanım uzantısı bulundu ve bitfield döndürüldü.
- **NX_SECURE_X509_MULTIBYTE_TAG_UNSUPPORTED** (0x181) ASN.1 çoklu bayt etiketiyle karşılaşıldı (desteklenmeyen sertifika).
- **NX_SECURE_X509_ASN1_LENGTH_TOO_LONG** (0x182) Invaild ASN.1 alanıyla karşılaşıldı (geçersiz sertifika).
- **NX_SECURE_X509_INVALID_TAG_CLASS** (0x190) Geçersiz ASN.1 etiket sınıfıyla karşılaşıldı (geçersiz sertifika).
- **NX_SECURE_X509_INVALID_EXTENSION_SEQUENCE** (0x192) Geçersiz uzantıyla karşılaşıldı (geçersiz sertifika).
- **NX_SECURE_X509_EXTENSION_NOT_FOUND** (0x19B)Anahtar Kullanımı uzantısı sağlanan sertifikada bulunamadı.
- **NX_PTR_ERROR** (0x07) Geçersiz sertifika veya bitfield işaretçisi.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
ULONG certificate_verification_callback(NX_SECURE_TLS_SESSION *session,
  NX_SECURE_X509_CERT* certificate)
{
UINT status;
USHORT key_usage_bitfield;

    /* Key usage – extract key usage bitfield. */
    status = nx_secure_x509_key_usage_extension_parse(certificate, &key_usage_bitfield);

   /* Check certificate for a few specific key usage bits. */
   if((key_usage_bitfield & NX_SECURE_X509_KEY_USAGE_DIGITAL_SIGNATURE) == 0 ||
      (key_usage_bitfield & NX_SECURE_X509_KEY_USAGE_NON_REPUDIATION)   == 0 ||
      (key_usage_bitfield & NX_SECURE_X509_KEY_USAGE_KEY_ENCIPHERMENT)  == 0)
    {
        printf("Expected key usage bitfield bits not set!\n");
        return(NX_SECURE_X509_KEY_USAGE_ERROR);
    }

    /* The specified bits were set, return success! */
    return(NX_SUCCESS);
}
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_tls_session_certificate_callback_set
- nx_secure_x509_extended_key_usage_extension_parse
- nx_secure_x509_crl_revocation_check
- nx_secure_x509_common_name_dns_check
- nx_secure_x509_extension_find
