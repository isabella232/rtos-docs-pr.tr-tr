---
title: Bölüm 4-Azure RTOS NetX güvenli DTLS hizmetlerinin açıklaması
description: Bu bölümde, alfabetik sırada listelenen tüm Azure RTOS NetX güvenli DTLS hizmetlerinin açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: e795a5fa35a4590e508c7fe2eec53f5494809657
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825690"
---
# <a name="chapter-4-description-of-azure-rtos-netx-secure-dtls-services"></a>Bölüm 4: Azure RTOS NetX güvenli DTLS hizmetlerinin açıklaması

Bu bölüm, tüm Azure RTOS NetX güvenli DTLS hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.

Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_SECURE_DISABLE_ERROR_CHECKING** makrodan etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.

- [nx_secure_dtls_client_session_start](#nx_secure_dtls_client_session_start)
- [nx_secure_dtls_packet_allocate](#nx_secure_dtls_packet_allocate)
- [nx_secure_dtls_psk_add](#nx_secure_dtls_psk_add)
- [nx_secure_dtls_server_create](#nx_secure_dtls_server_create)
- [nx_secure_dtls_server_delete](#nx_secure_dtls_server_delete)
- [nx_secure_dtls_server_local_certificate_add](#nx_secure_dtls_server_local_certificate_add)
- [nx_secure_dtls_server_local_certificate_remove](#nx_secure_dtls_server_local_certificate_remove)
- [nx_secure_dtls_server_notify_set](#nx_secure_dtls_server_notify_set)
- [nx_secure_dtls_server_psk_add](#nx_secure_dtls_server_psk_add)
- [nx_secure_dtls_server_session_send](#nx_secure_dtls_server_session_send)
- [nx_secure_dtls_server_session_start](#nx_secure_dtls_server_session_start)
- [nx_secure_dtls_server_start](#nx_secure_dtls_server_start)
- [nx_secure_dtls_server_stop](#nx_secure_dtls_server_stop)
- [nx_secure_dtls_server_trusted_certificate_add](#nx_secure_dtls_server_trusted_certificate_add)
- [nx_secure_dtls_server_trusted_certificate_remove](#nx_secure_dtls_server_trusted_certificate_remove)
- [nx_secure_dtls_server_x509_client_verify_configure](#nx_secure_dtls_server_x509_client_verify_configure)
- [nx_secure_dtls_server_x509_client_verify_disable](#nx_secure_dtls_server_x509_client_verify_disable)
- [nx_secure_dtls_session_client_info_get](#nx_secure_dtls_session_client_info_get)
- [nx_secure_dtls_session_create](#nx_secure_dtls_session_create)
- [nx_secure_dtls_session_delete](#nx_secure_dtls_session_delete)
- [nx_secure_dtls_session_end](#nx_secure_dtls_session_end)
- [nx_secure_dtls_session_local_certificate_add](#nx_secure_dtls_session_local_certificate_add)
- [nx_secure_dtls_session_local_certificate_remove](#nx_secure_dtls_session_local_certificate_remove)
- [nx_secure_dtls_session_receive](#nx_secure_dtls_session_receive)
- [nx_secure_dtls_session_reset](#nx_secure_dtls_session_reset)
- [nx_secure_dtls_ session_send](#nx_secure_dtls_-session_send)
- [nx_secure_dtls_session_trusted_certificate_add](#nx_secure_dtls_session_trusted_certificate_add)
- [nx_secure_dtls_session_trusted_certificate_remove](#nx_secure_dtls_session_trusted_certificate_remove)


## <a name="nx_secure_dtls_client_session_start"></a>nx_secure_dtls_client_session_start

NetX güvenli DTLS Istemci oturumu başlatma

### <a name="prototype"></a>Prototype

```C
UINT nx_secure_dtls_client_session_start(
                        NX_SECURE_DTLS_SESSION *dtls_session,
                        NX_UDP_SOCKET *udp_socket,
                        NXD_ADDRESS *ip_address, UINT port,
                        UINT wait_option);

```

### <a name="description"></a>Açıklama

Bu hizmet, ağ iletişimleri için belirtilen UDP yuvasını kullanarak, belirtilen IP adresi ve UDP bağlantı noktasındaki sunucuya bağlanan bir DTLS Istemci oturumu başlatır.

Bu hizmet nx_secure_dtls_session_create kullanılarak çağrılmadan önce DTLS oturum denetim bloğunun başlatılmış olması gerekir. Ayrıca, DTLS Istemcisi nx_secure_dtls_session_trusted_certificate_add veya önceden paylaşılan anahtarlar etkin ve yapılandırılmış olarak oturum için en az bir güvenilir CA sertifikası eklenmiş olmasını gerektirir.

### <a name="parameters"></a>Parametreler

- **dtls_session** Daha önce başlatılmış olan DTLS oturum yapısına yönelik işaretçi.
- **udp_socket** Uzak DTLS sunucusuyla ağ iletişimi kurmak için kullanılacak UDP yuvası başlatıldı.
- **ip_address** Uzak DTLS sunucusunun adresini içeren IP adresi yapısına yönelik işaretçi.
- **bağlantı noktası** Uzak DTLS sunucusuyla ağ iletişimi kurmak için kullanılacak UDP yuvası başlatıldı.
- **wait_option** Bağlantı girişimi için askıya alma seçeneği.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) sertifikanın oturumun başarıyla atanması.
- **NX_NOT_CONNECTED** (0x38) sunucuya, belirtilen adreste ve bağlantı noktasında ulaşılamıyor.
- **NX_SECURE_TLS_UNRECOGNIZED_MESSAGE_TYPE** (0x102) ALıNAN bir TLS/DTLS ileti türü yanlış.
- **NX_SECURE_TLS_UNSUPPORTED_CIPHER** (0x106) uzak ana bilgisayar tarafından sağlanmış bir şifre desteklenmez.
- TLS el sıkışması sırasında **NX_SECURE_TLS_HANDSHAKE_FAILURE** (0x107) ileti işleme başarısız oldu.
- **NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0x108) gelen bir ILETI karma Mac denetiminde başarısız oldu.
- **NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) temel alınan TCP yuvası gönderme başarısız oldu.
- **NX_SECURE_TLS_INCORRECT_MESSAGE_LENGTH** (0x10a) gelen iletide geçersiz uzunluk alanı vardı.
- **NX_SECURE_TLS_BAD_CIPHERSPEC** (0x10b) gelen bir Changecyaspec iletisi hatalı.
- **NX_SECURE_TLS_INVALID_SERVER_CERT** (0x10c) uzak DTLS sunucusunu tanımlamak Için gelen bir TLS sertifikası kullanılamaz.
- **NX_SECURE_TLS_UNSUPPORTED_PUBLIC_CIPHER** (0x10d) uzak ana bilgisayar tarafından sunulan ortak anahtar şifresi desteklenmez.
- **NX_SECURE_TLS_NO_SUPPORTED_CIPHERS** (0x10e) uzak ana bilgisayar, NETX GÜVENLI DTLS yığını tarafından desteklenen bir ciphersuites belirtti.
- **NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0x10F) ALıNAN DTLS iletisinin üstbilgisinde bilinmeyen DTLS sürümü vardı.
- **NX_SECURE_TLS_UNSUPPORTED_TLS_VERSION** (0x110) ALıNAN DTLS iletisi üstbilgisinde bilinen ancak desteklenmeyen bir DTLS sürümü vardı.
- **NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) BIR iç TLS paket ayırması başarısız oldu.
- **NX_SECURE_TLS_INVALID_CERTIFICATE** (0x112) uzak ana bilgisayar geçersiz bir sertifika sağladı.
- **NX_SECURE_TLS_ALERT_RECEIVED** (0x114) uzak ana bilgisayar bir hatayı BELIRTEN ve TLS oturumunu sonlandıran bir uyarı gönderdi.
- **NX_SECURE_TLS_MISSING_CRYPTO_ROUTINE** (0x13b) ciphersuite tablosundaki BIR girdinin null işlev işaretçisi vardı.
- **NX_PTR_ERROR** (0x07) geçersiz oturum, yuva veya adres işaretçisi.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Sockets, sessions, certificates defined in global static space to preserve
   application stack. */
NX_SECURE_DTLS_SESSION client_dtls_session;

/* Trusted certificate structure and raw data. */
NX_SECURE_X509_CERT trusted_cert;
const UCHAR trusted_cert_der = { … };

/* Cryptography routines and crypto work buffers. */
extern const NX_SECURE_TLS_CRYPTO nx_crypto_tls_ciphers;
UCHAR crypto_metadata[9000];

/* Packet reassembly buffer for decryption. */
UCHAR packet_buffer[4000];

/* Remote certificate buffer for incoming certificates. */
#define REMOTE_CERT_SIZE (sizeof(NX_SECURE_X509_CERT) + 2000)
#define REMOTE_CERT_NUMBER  (3)
UCHAR remote_certs_buffer[REMOTE_CERT_SIZE * REMOTE_CERT_NUMBER];

/* Application thread where TLS session is started. */
void application_thread()
{
NXD_ADDRESS server_ip;

    /* Create a TLS session for our socket. Ciphers and metadata defined
       elsewhere. See nx_secure_tls_session_create reference for more
       information. */
    status =  nx_secure_dtls_session_create(&client_dtls_session,
                                           &nx_crypto_tls_ciphers,
                                           crypto_metadata,
                                           sizeof(crypto_metadata),
                                           packet_buffer,
                                           sizeof(packet_buffer),
                                           REMOTE_CERT_NUMBER,
                                           remote_certs_buffer,
                                           sizeof(remote_certs_buffer));

    /* Check for error.  */
    if(status)
    {
        printf("Error in function nx_secure_dtls_session_create: 0x%x\n", status);
    }

    /* Initialize our trusted certificate. See section “Importing X.509
       Certificates into NetX Secure” for more information. */
    nx_secure_x509_certificate_initialize(&trusted_certificate,
                                      trusted_cert_der,
                                      trusted_cert_der_len,
                                      NX_NULL, 0, NX_NULL, 0,
                                      NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add the certificate to the local store using a numeric ID. */
    nx_secure_dtls_session_trusted_certificate_add(&client_dtls_session,
                                                   &certificate, 1);

    /* Set up IP address of remote host. */
    server_ip.nxd_ip_version = NX_IP_VERSION_V4;
    server_ip.nxd_ip_address.v4 = IP_ADDRESS(192, 168, 1, 150);


    /* Now we can start the DTLS session as normal. */
    status =  nx_secure_dtls_client_session_start(&client_dtls_session,
                                                  &udp_socket, &server_ip,
                                                  4443,
                                                  NX_IP_PERIODIC_RATE);

    if(status != NX_SUCCESS)
    {
      /* Error! */
      return(status);
    }

    /* Add data to send packet as usual for NX_PACKET and send to server.  */
    status = nx_secure_dtls_session_send(&client_dtls_session, &send_packet,
                                                        &server_ip, 4443);

    /* Receive response from server. */
    status = nx_secure_dtls_session_receive(&client_dtls_session, &receive_packet,
                                                            NX_IP_PERIODIC_RATE);

    /* Process response. */

    /* Shut down DTLS session. */
    status = nx_secure_dtls_session_end(&client_dtls_session, NX_IP_PERIODIC_RATE);

    /* Clean up. */
    status = nx_secure_dtls_session_delete(&client_dtls_session);

}

```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_dtls_session_receive, nx_secure_dtls_session_send,
- nx_secure_dtls_session_create

## <a name="nx_secure_dtls_packet_allocate"></a>nx_secure_dtls_packet_allocate

NetX güvenli DTLS oturumu için bir paket ayırın

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_dtls_packet_allocate(
                              NX_SECURE_DTLS_SESSION *session_ptr,
                         NX_PACKET_POOL *pool_ptr,
                         NX_PACKET **packet_ptr,
                              ULONG wait_option);

```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen NX_PACKET_POOL belirtilen etkin DTLS oturumu için bir NX_PACKET ayırır. Bu hizmet, bir DTLS bağlantısı üzerinden gönderilecek veri paketleri ayırmak için uygulama tarafından çağrılmalıdır. Bu hizmet çağrılmadan önce DTLS oturumunun başlatılmış olması gerekir.

Ayrılan paket düzgün bir şekilde başlatılır, böylece DTLS üstbilgi ve altbilgi verileri, paket verileri doldurulduktan sonra eklenebilir. Davranış, *nx_packet_allocate* benzer şekilde benzerdir.

### <a name="parameters"></a>Parametreler

- **session_ptr** DTLS oturum örneği işaretçisi.
- **pool_ptr** Paketin ayırabileceği bir NX_PACKET_POOL işaretçisi.
- **packet_ptr** Yeni ayrılmış pakete çıkış işaretçisi.
- **wait_option** Paket ayırması için askıya alma seçeneği.


### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı paket ayırması.
- **NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) temel alınan paket ayırması başarısız oldu.
- **NX_SECURE_TLS_SESSION_UNINITIALIZED** (0x101) sağlanan DTLS oturumu başlatılmadı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Allocate a new DTLS packet from the previously created packet pool and
previously initialized DTLS session.   */

status = nx_secure_dtls_packet_allocate(&dtls_session, &pool_0, &packet_ptr,
                                                              NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the newly allocated packet pointer is found in
the variable packet_ptr.  */

```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_x509_certificate_initialize, nx_secure_dtls_session_create,
- nx_secure_dtls_session_trusted_certificate_add,
- nx_secure_dtls_session_send, nx_secure_dtls_session_receive,
- nx_secure_dtls_session_end, nx_secure_dtls_session_delete

## <a name="nx_secure_dtls_psk_add"></a>nx_secure_dtls_psk_add

NetX güvenli DTLS oturumuna önceden paylaşılan anahtar ekleme

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_dtls_psk_add(NX_SECURE_DTLS_SESSION *session_ptr,
                            UCHAR *pre_shared_key, UINT psk_length,
                            UCHAR *psk_identity, UINT
                            identity_length, UCHAR *hint, UINT
                            hint_length);
```

### <a name="description"></a>Açıklama

Bu hizmet, bir DTLS oturum denetim bloğuna bir önceden paylaşılan anahtar (PSK), kimlik dizesi ve kimlik ipucu ekler. PSK ciphersuites etkin ve kullanıldığında, bir dijital sertifika yerine PSK kullanılır.

### <a name="parameters"></a>Parametreler

- **session_ptr** Daha önce oluşturulmuş bir DTLS oturum örneğine yönelik işaretçi.
- **pre_shared_key** Gerçek PSK değeri.
- **psk_length** PSK değeri uzunluğu.
- **psk_identity** Bu PSK değerini tanımlamak için kullanılan dize.
- **identity_length** PSK kimliğinin uzunluğu.
- **İpucu** Bir TLS sunucusunda hangi sayıda PSKs arasından seçim yapmak gerektiğini göstermek için kullanılan dize.
- **hint_length** İpucu dizesinin uzunluğu.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) PSK 'nin başarılı bir şekilde eklenmesi.
- **NX_PTR_ERROR** (0x07) geçersiz DTLS oturum işaretçisi.
- **NX_SECURE_TLS_NO_MORE_PSK_SPACE** (0x125) başka bir PSK eklenemiyor.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* PSK value.  */
UCHAR psk[] = { 0x1a, 0x2b, 0x3c, 0x4d };

/* Add PSK to DTLS session.  */
status =  nx_secure_dtls_psk_add(&dtls_session, psk,
                            sizeof(psk), “psk_1”, 4,
                            “Client_identity”, 15);


/* If status is NX_SUCCESS the PSK was successfully added.  */


```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_dtls_server_psk_add, nx_secure_dtls_client_session_create

## <a name="nx_secure_dtls_server_create"></a>nx_secure_dtls_server_create

NetX güvenli DTLS sunucusu oluşturma

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_dtls_server_create(
                NX_SECURE_DTLS_SERVER *server_ptr, NX_IP *ip_ptr,
                UINT port, ULONG timeout, VOID *session_buffer,
                UINT session_buffer_size,
                const NX_SECURE_TLS_CRYPTO *crypto_table,
                VOID *crypto_metadata_buffer, ULONG crypto_metadata_size,
                UCHAR *packet_reassembly_buffer,
                UINT packet_reassembly_buffer_size,
                UINT (*connect_notify)(
                              NX_SECURE_DTLS_SESSION *dtls_session,
                              NXD_ADDRESS *ip_address, UINT port),
                UINT (*receive_notify)(
                              NX_SECURE_DTLS_SESSION *dtls_session)));

```

### <a name="description"></a>Açıklama

Bu hizmet, belirli bir UDP bağlantı noktasındaki gelen DTLS isteklerini işlemek için bir DTLS sunucusu örneği oluşturur. UDP 'nin durum bilgisiz olması nedeniyle, birden fazla istemciden alınan DTLS istekleri, diğer DTLS oturumları etkinken tek bir bağlantı noktasında gelebilir. Bu nedenle, sunucu etkin oturumları sürdürmek ve gelen iletileri doğru işleyiciye yönlendirmek için gereklidir.

İp_ptr parametresi, DTLS sunucusuyla ilişkili iç UDP yuvası için kullanılacak bir NX_IP örneğini işaret eder (ve NX_SECURE_DTLS_SERVER denetim bloğunda depolanır). IP örneği ve bağlantı noktası, sunucunun nx_secure_dtls_server_start hizmeti ile örneği oluşturulan UDP arabirimini tanımlamak için kullanılır.

Oturum arabelleği parametresi, DTLS sunucusu için tüm olası aynı DTLS oturumlarının denetim bloklarını tutmak için kullanılır. NX_SECURE_DTLS_SESSION denetim bloğu yapısının boyutunun bir daha katı olan bir boyutla ayrılmalıdır.

Gerekli meta veri boyutunu hesaplamak için, API nx_secure_tls_metadata_size_calculate kullanılabilir.

Packet_reassembly_buffer parametresi, şifreleme amacıyla UDP datagramlarını tam DTLS kaydına yeniden birleştirmek için DTLS tarafından kullanılır ve en büyük beklenen DTLS kaydına uyum sağlayacak kadar büyük olmalıdır (16KB, en büyük kayıt boyutudur, ancak birçok uygulama bu çok fazla veriyi tek bir kayıtta göndermez).

Connect_notify geri çağırma yordamı, her yeni DTLS istemcisi sunucuya bağlandığında çağrılır. Bu, uygulama, Service *nx_secure_dtls_server_session_start* kullanarak DTLS oturumunu başlatacak. Oturum geri çağırmada başlatılmayabilir, ancak geri çağırma, tüm alt düzey ağ işlemlerini (örn. UDP) işlemek için kullanılan IP iş parçacığını (veya uygulama tarafından oluşturulan adanmış DTLS iş parçacığını) bildirmek için kullanılmalıdır. Bu, DTLS oturum parametresini kaydetme (geri çağırmaya bir parametre olarak sunulur) ve diğer iş parçacığında nx_secure_dtls_server_session_start çağırma kadar kolay olabilir. Connect_notify geri çağırma genellikle NX_SUCCESS döndürmelidir.

Receive_notify geri çağırma yordamı, mevcut bir DTLS oturumuyla eşleşen bir DTLS kaydı alındığında çağrılır (var olan bir oturumu tanımlamak için uzak ana bilgisayar IP adresi ve bağlantı noktası kullanılır). Bu, DTLS üzerinden şifrelenen ve gönderilen "uygulama verilerini" temsil eder. Uygulamanın alınan verileri almak için, belirtilen DTLS oturumunda hizmet *nx_secure_dtls_session_receive* çağrısı gerekir. Connect_receive geri çağırmada olduğu gibi, geri çağırma IP iş parçacığından çağrıldığında ileti işlemeyi işlemek için oturumun başka bir iş parçacığına geçirilmesi önerilir. Receive_notify geri çağırma genellikle NX_SUCCESS döndürmelidir.

### <a name="parameters"></a>Parametreler

- **server_ptr** Daha önce oluşturulmuş bir DTLS sunucu örneğine yönelik işaretçi.
- **ip_ptr** DTLS sunucusu için ağ arabirimi olarak kullanılacak başlatılmış bir NX_IP denetim bloğunun işaretçisi.
- **bağlantı noktası** DTLS sunucusu UDP yuvasının bağlandığı yerel UDP bağlantı noktası.
- **zaman aşımı** Ağ işlemleri için kullanılacak zaman aşımı değeri.
- **session_buffer** Bu DTLS sunucu örneğine atanan tüm NX_SECURE_DTLS_SESSION örnekleri için denetim blokları içeren arabellek alanı.
- **session_buffer_size** Oturum arabelleğinin boyutu. Bu, DTLS sunucusuna atanan DTLS oturumlarının sayısını belirler.
- **crypto_table** Tüm şifreleme işlemleri için kullanılan TLS/DTLS Şifreleme tablosu yapısına yönelik işaretçi.
- **crypto_metadata_buffer** Şifreleme işlemi hesaplamaları ve durum bilgileri için arabellek alanı.
- **crypto_metadata_size** Meta veri arabelleğinin boyutu.
- **packet_reassembly_buffer** DTLS tarafından, IP verilerini şifre çözme için DTLS kayıtlarına yeniden birleştirmek üzere kullanılan arabellek.
- **packet_reassembly_buffer_size** Yeniden birleştirme arabelleğinin boyutu. Genellikle 16KB 'den büyük olmalıdır, ancak uygulamaya bağlı olarak daha küçük olabilir.
- **connect_notify** Uzak DTLS Istemcisi bu DTLS sunucusuna bağlanmaya çalıştığında, geri arama yordamı çağrılır.
- **receive_notify** Mevcut bir DTLS oturumu üzerinden uygulama verileri alındığında çağrı çağrılır.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) DTLS sunucusu başarıyla oluşturuldu.
- **NX_PTR_ERROR** (0x07) geçersiz işaretçi geçirildi.
- **NX_INVALID_PARAMETERS** (0x4D) oturumlar, paket yeniden birleştirme veya şifreleme için yeterli arabellek alanı yok.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
#define DTLS_SERVER_SESSION (3)

/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Allocate space for DTLS sessions in the DTLS server. */
UCHAR dtls_server_session_buffer[sizeof(NX_SECURE_DTLS_SESSION)
                                        * DTLS_SERVER_SESSIONS];

/* Flag used to indicate that a DTLS Client has connected. */
UINT connect_flag = 0;

/* Flag used to indicate application data reception. */
UINT receive_flag = 0;

/* Pointer to newly-connected DTLS session.
   NOTE: In practice this should be an array or list in case a new connection is
         attempted while a previous session is being started. */
NX_SECURE_DTLS_SESSION *new_dtls_session;

/* Pointer to session for application data receive.
   NOTE: Should be an array or list as
   with new_dtls_session */
NX_SECURE_DTLS_SESSION *receive_dtls_session;

/* Connect notify callback routine. */
UINT dtls_server_connect_notify(NX_SECURE_DTLS_SESSION *dtls_session, NXD_ADDRESS
    *ip_address, UINT port)
{
    /* NOTE: proper inter-thread communication procedures (e.g. mutex handling)
             Omitted for clarity. */

    /* Notify application thread that a connection request has been received. */
    connect_flag = 1;
    new_dtls_session = dtls_session;

    return(NX_SUCCESS);
}

/* Receive notify callback routine invoked when DTLS application data is received
   on an existing DTLS server session. */
UINT dtls_server_receive_notify(NX_SECURE_DTLS_SESSION *dtls_session)
{
    /* Receive and process DTLS record.
       NOTE: Mutex handling omitted for clarity. */
    receive_flag = 1;
    receive_dtls_session = dtls_session;

    return(NX_SUCCESS);
}

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
    NX_PACKET *send_packet;
    NX_PACKET *receive_packet;
    UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                LOCAL_SERVER_PORT,
                                NX_IP_PERIODIC_RATE, dtls_server_session_buffer,
                                sizeof(dtls_server_session_buffer),
                                &tls_crypto_table, crypto_metadata_buffer,
                                sizeof(crypto_metadata_buffer), packet_buffer,
                                sizeof(packet_buffer),
                                dtls_server_connect_notify,
                                dtls_server_receive_notify);

    /* Initialize local server identity certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&certificate, device_cert_der,
                        device_cert_der_len, NX_NULL, 0,
                        device_cert_key_der, device_cert_key_der_len,
                        NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_local_certificate_add(&dtls_server,
                                                    &certificate, 1);

    /* Start server. */
    status = nx_secure_dtls_server_start(&dtls_server);

    /* Loop continuously to handle incoming data. */
    while(1)
    {
        /* Check for new connections. Muxtex handling omitted for clarity. */
        if(connect_flag)
        {
            /* We have a new connection attempt, start the DTLS session. */
            status = nx_secure_dtls_server_session_start(new_dtls_session,
                                                    NX_IP_PERIODIC_RATE);

        }

        /* Check for received application data. */
        if(receive_flag)
        {
            /* We have received data over a previously-established DTLS session.
               Mutex handling omitted for clarity. */
            Status = nx_secure_dtls_session_receive(receive_dtls_session,
                                                        &receive_packet,
                                                           NX_IP_PERIODIC_RATE);

            /* Process received data… */

            /* Prepare and send response to client. */
        status = nx_secure_dtls_packet_allocate(receive_dtls_session, &packet_pool,
                                                   &send_packet, NX_IP_PERIODIC_RATE);

        /* Check for errors and prepare response data
        (e.g. nx_packet_data_append). */

        /* Send response to client. */
        status = nx_secure_dtls_server_session_send(receive_dtls_session,
                                                            send_packet);

        }

        /* If not processing connections or received data,
        let the thread sleep. */
        if(!connect_flag && !receive_flag)
        {
            tx_thread_sleep(100);
        }
    }

    /* Server processing is done, stop the server
    instance from accepting requests. */
    status = nx_secure_dtls_server_stop(&dtls_server);

    /* If we exit the processing loop, clean up the server. */
    status = nx_secure_dtls_server_delete(&dtls_server);
}

```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_dtls_server_start, nx_secure_dtls_server_delete,
- nx_secure_dtls_session_receive, nx_secure_dtls_server_session_send,
- nx_secure_dtls_server_session_start,
- nx_secure_dtls_server_session_stop,
- nx_secure_dtls_server_local_certificate_add

## <a name="nx_secure_dtls_server_delete"></a>nx_secure_dtls_server_delete

NetX güvenli DTLS sunucusu tarafından kullanılan kaynakları boşaltma

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_dtls_server_delete(NX_SECURE_DTLS_SERVER *server_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, sunucu tarafından kullanılan iç UDP yuvası dahil olmak üzere bir DTLS sunucu örneğine ayrılan kaynakları boşaltır.

### <a name="parameters"></a>Parametreler

- **server_ptr** Daha önce oluşturulmuş bir DTLS sunucu örneğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) sunucu başarıyla silindi.
- **NX_PTR_ERROR** (0x07) geçersiz işaretçi geçirildi.
- **NX_STILL_BOUND** (0x42) UDP yuvası hala bağımlı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
#define DTLS_SERVER_SESSION (3)

/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Allocate space for DTLS sessions in the DTLS server. */
UCHAR dtls_server_session_buffer[sizeof(NX_SECURE_DTLS_SESSION)
                                        * DTLS_SERVER_SESSIONS];

/* Flag used to indicate that a DTLS Client has connected. */
UINT connect_flag = 0;

/* Flag used to indicate application data reception. */
UINT receive_flag = 0;

/* Pointer to newly-connected DTLS session.
   NOTE: In practice this should be an array or list in case a new connection is
         attempted while a previous session is being started. */
NX_SECURE_DTLS_SESSION *new_dtls_session;

/* Pointer to session for application data receive.
NOTE: Should be an array or list as
   with new_dtls_session */
NX_SECURE_DTLS_SESSION *receive_dtls_session;

/* Connect notify callback routine. */
UINT dtls_server_connect_notify(NX_SECURE_DTLS_SESSION *dtls_session, NXD_ADDRESS
*ip_address, UINT port)
{
    /* NOTE: proper inter-thread communication procedures (e.g. mutex handling)
             Omitted for clarity. */

    /* Notify application thread that a connection request has been received. */
    connect_flag = 1;
    new_dtls_session = dtls_session;

    return(NX_SUCCESS);
}

/* Receive notify callback routine invoked when DTLS application data is received
   on an existing DTLS server session. */
UINT dtls_server_receive_notify(NX_SECURE_DTLS_SESSION *dtls_session)
{
    /* Receive and process DTLS record.
       NOTE: Mutex handling omitted for clarity. */
    receive_flag = 1;
    receive_dtls_session = dtls_session;

    return(NX_SUCCESS);
}

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
    NX_PACKET *send_packet;
    NX_PACKET *receive_packet;
    UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                            LOCAL_SERVER_PORT,
                                            NX_IP_PERIODIC_RATE,
                                            dtls_server_session_buffer,
                                            sizeof(dtls_server_session_buffer),
                                            &tls_crypto_table,
                                            crypto_metadata_buffer,
                                            sizeof(crypto_metadata_buffer),
                                            packet_buffer, sizeof(packet_buffer),
                                            dtls_server_connect_notify,
                                            dtls_server_receive_notify);


    /* Check for errors. */

    /* Initialize local server identity certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&certificate, device_cert_der,
                                            device_cert_der_len,
                                            NX_NULL, 0,
                                            device_cert_key_der,
                                            device_cert_key_der_len,
                                            NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_local_certificate_add(&dtls_server,
                                                    &certificate, 1);


    /* Start server. */
    status = nx_secure_dtls_server_start(&dtls_server);

    /* Loop continuously to handle incoming data. */
    while(1)
    {
        /* Check for new connections. Muxtex handling omitted for clarity. */
        if(connect_flag)
        {
            /* We have a new connection attempt, start the DTLS session. */
            status = nx_secure_dtls_server_session_start(new_dtls_session,
                                                    NX_IP_PERIODIC_RATE);
        }

        /* Check for received application data. */
        if(receive_flag)
        {
            /* We have received data over a previously-established DTLS session.
               Mutex handling omitted for clarity. */
            Status = nx_secure_dtls_session_receive(receive_dtls_session,
                                                        &receive_packet,
                                                         NX_IP_PERIODIC_RATE);

            /* Process received data… */

            /* Prepare and send response to client. */
        status = nx_secure_dtls_packet_allocate(receive_dtls_session,
                                                        &packet_pool,
                                                        &send_packet,
                                                        NX_IP_PERIODIC_RATE);

        /* Send response to client. */
        status = nx_secure_dtls_server_session_send(receive_dtls_session,
                                                            send_packet);

        }

        /* If not processing connections or received data, let the thread sleep. */
        if(!connect_flag && !receive_flag)
        {
            tx_thread_sleep(100);
        }
    }

    /* If we exit the processing loop, clean up the server. */
    status = nx_secure_dtls_server_delete(&dtls_server);
}

```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_dtls_server_start, nx_secure_dtls_server_create,
- nx_secure_dtls_session_receive, nx_secure_dtls_server_session_send,
- nx_secure_dtls_server_session_start

## <a name="nx_secure_dtls_server_local_certificate_add"></a>nx_secure_dtls_server_local_certificate_add

NetX güvenli DTLS sunucusuna yerel sunucu kimlik sertifikası ekleme

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_dtls_server_local_certificate_add(
                                   NX_SECURE_DTLS_SERVER *server_ptr,
                                 NX_SECURE_X509_CERT *certificate,
                                 UINT cert_id);

```

### <a name="description"></a>Açıklama

Bu hizmet bir DTLS sunucu örneğine yerel sunucu kimlik sertifikası ekler. Diğer bir kimlik doğrulama mekanizması (ör. önceden paylaşılan anahtarlar) kullanılmadığı takdirde, istemcilerin bir DTLS sunucusuna bağlanması için en az bir kimlik sertifikası gereklidir.

Cert_id parametresi, sertifika için sayısal, sıfır olmayan bir tanıtıcıdır. Bu, DTLS sunucu deposunda aynı X. 509.440 ortak adına sahip birden çok kimlik sertifikası bulunan olayda kolayca kaldırılmasını veya bu durumda bulunabilmesini sağlar. X. 509.440 sunucu sertifikaları hakkında daha fazla bilgi için NetX güvenli TLS Kullanıcı Kılavuzu 'na bakın.

### <a name="parameters"></a>Parametreler

- **server_ptr** Daha önce oluşturulmuş bir DTLS sunucu örneğine yönelik işaretçi.
- **sertifika** Daha önce başlatılmış bir X. 509.440 sertifika yapısına yönelik işaretçi.
- **cert_id** Bu DTLS sunucusunda bu sertifika için sıfır olmayan sayısal benzersiz tanımlayıcı.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) DTLS sunucusuna sertifikanın başarıyla eklenmesi.
- **NX_PTR_ERROR** (0x07) geçersiz işaretçi geçirildi.
- **NX_INVALID_PARAMETERS** (0x4D) BIR sertifika kimliği (0) geçirildi.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

* Daha kapsamlı bir örnek için bkz. *nx_secure_dtls_server_create* başvurusu.

```C
/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Certificate control block and data. */
NX_SECURE_X509_CERT certificate;
UCHAR certificate_der_data[] = { … };
UCHAR certificate_key_der_data[] = { … };

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                    LOCAL_SERVER_PORT,
                                    NX_IP_PERIODIC_RATE,
                                    dtls_server_session_buffer,
                                    sizeof(dtls_server_session_buffer),
                                    &tls_crypto_table,
                                    crypto_metadata_buffer,
                                    sizeof(crypto_metadata_buffer),
                                    packet_buffer,
                                    sizeof(packet_buffer),
                                    dtls_server_connect_notify,
                                    dtls_server_receive_notify);

    /* Check for errors. */

    /* Initialize local server identity certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&certificate,
                            certificate_der_data,
                            sizeof(certificate_der_data),
                            NX_NULL, 0,
                            certificate_key_der_data,
                            sizeof(certificate_key_der_data),
                            NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_local_certificate_add(&dtls_server,
                                                    &certificate, 1);

    /* Start server. */
    status = nx_secure_dtls_server_start(&dtls_server);

    /* Loop continuously to handle incoming data. */
    while(1)
    {
        /* Process incoming requests and data. */
    }

}

```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_dtls_server_start, nx_secure_dtls_server_create,
- nx_secure_dtls_session_receive, nx_secure_dtls_server_session_send,
- nx_secure_dtls_server_session_start,
- nx_secure_dtls_server_local_certificate_remove,
- nx_secure_x509_certificate_initialize

## <a name="nx_secure_dtls_server_local_certificate_remove"></a>nx_secure_dtls_server_local_certificate_remove

NetX güvenli DTLS sunucusundan yerel sunucu kimlik sertifikasını kaldırma

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_dtls_server_local_certificate_remove(
                                   NX_SECURE_DTLS_SERVER *server_ptr,
                                   UCHAR *common_name,
                                   UINT common_name_length,
                                   UINT cert_id);

```

### <a name="description"></a>Açıklama

Bu hizmet, bir DTLS sunucu örneğinden yerel sunucu kimlik sertifikasını kaldırır. Diğer bir kimlik doğrulama mekanizması (ör. önceden paylaşılan anahtarlar) kullanılmadığı takdirde, istemcilerin bir DTLS sunucusuna bağlanması için en az bir kimlik sertifikası gereklidir.

Kaldırılacak sertifika, X. 509.440 ortak adı ya da *nx_secure_dtls_server_local_certificate_add* çağrısında atanan sayısal cert_id tarafından belirlenebilir. Cert_id yalnızca sertifikayı tanımlamak için kullanılır ve uygulama tarafından korunur. Sayısal sertifika tanımlayıcısı yerine ortak ad kullanılırsa, cert_id parametresi 0 olarak ayarlanmalıdır.

> [!NOTE]
> Bir DTLS el sıkışması işlenirken bir sertifikayı kaldırmak beklenmeyen davranışlara neden olur. Sertifikalar kaldırılmadan önce hizmet *nx_secure_dtls_server_stop* çağrılmalıdır.

### <a name="parameters"></a>Parametreler

- **server_ptr** Daha önce oluşturulmuş bir DTLS sunucu örneğine yönelik işaretçi.
- **common_name** Kaldırılacak sertifikanın X. 509.440 CommonName. Bu kullanılırsa, cert_id sıfır olarak geçirin.
- **common_name_length** Bayt cinsinden common_name dize uzunluğu.
- **cert_id** Bu DTLS sunucusunda bu sertifika için sıfır olmayan sayısal benzersiz tanımlayıcı. Bu kullanılırsa, common_name parametresi için NX_NULL geçirin.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) DTLS sunucusundan sertifikanın başarıyla kaldırılması.
- **NX_PTR_ERROR** (0x07) geçersiz işaretçi geçirildi.
- **NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) VERILEN DTLS sunucusunda cert_id veya common_name eşleşen bir sertifika bulunamadı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Certificate control block and data. */
NX_SECURE_X509_CERT certificate;
UCHAR certificate_der_data[] = { … };
UCHAR certificate_key_der_data[] = { … };

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
    UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                LOCAL_SERVER_PORT, NX_IP_PERIODIC_RATE,
                                dtls_server_session_buffer,
                                sizeof(dtls_server_session_buffer),
                                &tls_crypto_table, crypto_metadata_buffer,
                                sizeof(crypto_metadata_buffer), packet_buffer,
                                sizeof(packet_buffer),
                                dtls_server_connect_notify,
                                dtls_server_receive_notify);

    /* Check for errors. */

    /* Initialize local server identity certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&certificate,
                                        certificate_der_data,
                                        sizeof(certificate_der_data),
                                        NX_NULL, 0, certificate_key_der_data,
                                        sizeof(certificate_key_der_data),
                                        NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_local_certificate_add(&dtls_server,
                                                     &certificate, 1);

    /* Start server. */
    status = nx_secure_dtls_server_start(&dtls_server);

    /* Process client requests, etc… */

    /* Stop the server before removing a certificate. */
    Status = nx_secure_dtls_server_stop(&dtls_server);

    /* At some point in the future we decide to remove the certificate we added.
    We can use the certificate identifier we passed into the call to
    nx_secure_dtls_local_certificate_add (value = 1); */
    status = nx_secure_dtls_server_local_certificate_remove(&dtls_server,
                                                          NX_NULL, 0, 1);

}

```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_dtls_server_start, nx_secure_dtls_server_create,
- nx_secure_dtls_server_session_start,
- nx_secure_dtls_server_session_stop,
- nx_secure_dtls_server_local_certificate_add,
- nx_secure_x509_certificate_initialize

## <a name="nx_secure_dtls_server_notify_set"></a>nx_secure_dtls_server_notify_set

NetX güvenli DTLS sunucusuna isteğe bağlı bildirim geri çağırma yordamlarını atama

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_dtls_server_notify_set(
                         NX_SECURE_DTLS_SERVER *server_ptr,
                         UINT (*disconnect_notify)(
                                      NX_SECURE_DTLS_SESSION *dtls_session),
                         UINT (*error_notify)(
                                      NX_SECURE_DTLS_SESSION *dtls_session,
                                      UINT error_code));

```

### <a name="description"></a>Açıklama

Bu hizmet, bir DTLS sunucusuna isteğe bağlı bildirim geri çağırma yordamlarını eklemek için kullanılabilir. Yalnızca bir geri çağırma isteniyorsa, geri çağırma parametresi NX_NULL olarak geçirilebilir.

Disconnect_notify geri çağırması, uzak bir istemci bir DTLS oturumunu sona erdirdiğinde çağrılır. Dtls_session parametresi, kapatılan oturum örneğidir. Geri çağırma genellikle NX_SUCCESS döndürmelidir.

Error_notify geri çağırma, bir DTLS hatası veya zaman aşımı oluştuğunda çağrılır. Dtls_session parametresi, hatanın gerçekleştiği oturum örneğidir ve error_code soruna neden olan hatanın sayısal durum kodudur (bkz. Ek A)

NetX güvenli döndürülen hata kodları listesi için hata kodları). Geri çağırma genellikle NX_SUCCESS döndürmelidir.

### <a name="parameters"></a>Parametreler

- **server_ptr** Daha önce oluşturulmuş bir DTLS sunucu örneğine yönelik işaretçi.
- **disconnect_notify** Bir uzak istemci ana bilgisayarı bir DTLS oturumunu her kapattığında, geri çağırma yordamı çağrılır.
- **error_notify** DTLS bir hata veya zaman aşımıyla karşılaştığında çağrılan geri çağırma yordamı.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) geri çağırma yordamlarının başarıyla atanması.
- **NX_PTR_ERROR** (0x07) geçersiz işaretçi geçirildi.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

UINT disconnect_notify(NX_SECURE_DTLS_SESSION *dtls_session)
{
NXD_ADDRESS client_ip_addr;
UINT client_port;
UINT local_port;

    /* We have received a disconnection notice (CloseNotify message) from a
       remote client. Application can use the dtls_session parameter for any
       desired processing. */

    /* See what client disconnected by extracting its IP address and port.
       NOTE: depending on how the session ended, the client information may
             no longer be available. */
    status  = nx_secure_dtls_session_client_info_get(dtls_session,
                                                    &ip_addr,
                                                    &client_port,
                                                    &local_port);

    return(NX_SUCCESS);
}

UINT error_notify(NX_SECURE_DTLS_SESSION *dtls_session, UINT error_code)
{
    /* The DTLS server has encountered an error or timeout condition. We
    can use the error_code parameter to determine the error and we
    can insect the dtls_session for more information. */

    return(NX_SUCCESS);
}

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
    UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                LOCAL_SERVER_PORT,
                                NX_IP_PERIODIC_RATE,
                                dtls_server_session_buffer,
                                sizeof(dtls_server_session_buffer),
                                &tls_crypto_table,
                                crypto_metadata_buffer,
                                sizeof(crypto_metadata_buffer),
                                packet_buffer,
                                sizeof(packet_buffer),
                                dtls_server_connect_notify,
                                dtls_server_receive_notify);

    /* Check for errors. */

    /* Other setup (e.g. certificates) goes here … */

    status = nx_secure_dtls_server_notify_set(&dtls_server, disconnect_notify,
                                                                 error_notify);

    /* Start server. */
    status = nx_secure_dtls_server_start(&dtls_server);

    /* Process client requests, etc… */

}

```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_dtls_server_start, nx_secure_dtls_server_create,
- nx_secure_dtls_server_session_start,
- nx_secure_dtls_server_session_stop

## <a name="nx_secure_dtls_server_psk_add"></a>nx_secure_dtls_server_psk_add

NetX güvenli DTLS sunucusuna önceden paylaşılan anahtar ekleme

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_dtls_server_psk_add(
                                NX_SECURE_DTLS_SERVER *server_ptr,
                                UCHAR *pre_shared_key, UINT psk_length,
                                UCHAR *psk_identity,
                                UINT identity_length, UCHAR *hint,
                                UINT hint_length);

```

### <a name="description"></a>Açıklama

Bu hizmet, bir DTLS sunucu denetim bloğuna bir önceden paylaşılan anahtar (PSK), kimlik dizesi ve kimlik ipucu ekler. PSK ciphersuites etkin ve kullanıldığında, bir dijital sertifika yerine PSK kullanılır.

Eklenen PSK, DTLS sunucusuna atanan tüm DTLS oturumlarında çoğaltılır (nx_secure_dtls_server_create çağrısında verilen oturum arabelleği aracılığıyla).

### <a name="parameters"></a>Parametreler

- **server_ptr** Daha önce oluşturulmuş bir DTLS sunucu örneğine yönelik işaretçi.
- **pre_shared_key** Gerçek PSK değeri.
- **psk_length** PSK değeri uzunluğu.
- **psk_identity** Bu PSK değerini tanımlamak için kullanılan dize.
- **identity_length** PSK kimliğinin uzunluğu.
- **İpucu** Bir TLS sunucusunda hangi sayıda PSKs arasından seçim yapmak gerektiğini göstermek için kullanılan dize.
- **hint_length** İpucu dizesinin uzunluğu.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) PSK 'nin başarılı bir şekilde eklenmesi.
- **NX_PTR_ERROR** (0x07) geçersiz DTLS sunucu işaretçisi.
- **NX_SECURE_TLS_NO_MORE_PSK_SPACE** (0x125) başka bir PSK eklenemiyor.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* PSK value.  */
UCHAR psk[] = { 0x1a, 0x2b, 0x3c, 0x4d };

/* Add PSK to DTLS session.  */
status =  nx_secure_dtls_server_psk_add(&dtls_server, psk, sizeof(psk), “psk_1”,
   4, “Client_identity”, 15);


/* If status is NX_SUCCESS the PSK was successfully added.  */

```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_dtls_psk_add, nx_secure_dtls_server_create

## <a name="nx_secure_dtls_server_session_send"></a>nx_secure_dtls_server_session_send

NetX güvenli DTLS sunucusuyla kurulu bir DTLS oturumu üzerinden veri gönderme

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_dtls_server_session_send(
                                NX_SECURE_DTLS_SESSION *session_ptr,
                               NX_PACKET *packet_ptr);

```

### <a name="description"></a>Açıklama

Bu hizmet, uzak DTLS Istemci konağına, belirlenen DTLS sunucusu oturumu üzerinden bir veri paketi gönderir. Kullanılan oturum, nx_secure_dtls_session_create için sunulan receive_notify geri çağırma yordamında elde edilir.

Pakette belirtilen veriler, *nx_secure_dtls_packet_allocate* kullanılarak ayrılması gereken DTLS oturum şifreleme parametreleri ve yordamları kullanılarak şifrelenir ve ardından DTLS sunucusu iç UDP bağlantı noktası üzerinden uzak ana bilgisayara, eklenen istemcinin IP adresine ve bağlantı noktasına (DTLS oturumunda depolanır) gönderilir.

### <a name="parameters"></a>Parametreler

- **session_ptr** Uygulama tarafından sunulan receive_notify geri çağırma yordamından alınan DTLS oturum örneği işaretçisi.
- **packet_ptr** Daha önce ayrılan ve uygulama verileriyle doldurulmuş bir NX_PACKET örneğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) DTLS sunucusu başarıyla oluşturuldu.
- **NX_PTR_ERROR** (0x07) geçersiz işaretçi geçirildi.
- **NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) temel alınan UDP gönderme işleminde bir hata oluştu.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
#define DTLS_SERVER_SESSION (3)

/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Flag used to indicate application data reception. */
UINT receive_flag = 0;

/* Pointer to session for application data receive.
   NOTE: Should be an array or list as
   with new_dtls_session */
NX_SECURE_DTLS_SESSION *receive_dtls_session;


/* Receive notify callback routine invoked when DTLS application data is received
   on an existing DTLS server session. */
UINT dtls_server_receive_notify(NX_SECURE_DTLS_SESSION *dtls_session)
{
    /* Receive and process DTLS record.
       NOTE: Mutex handling omitted for clarity. */
    receive_flag = 1;
    receive_dtls_session = dtls_session;

    return(NX_SUCCESS);
}

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
    NX_PACKET *send_packet;
    NX_PACKET *receive_packet;
    UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                LOCAL_SERVER_PORT,
                                NX_IP_PERIODIC_RATE,
                                dtls_server_session_buffer,
                                sizeof(dtls_server_session_buffer),
                                &tls_crypto_table,
                                crypto_metadata_buffer,
                                sizeof(crypto_metadata_buffer),
                                packet_buffer,
                                sizeof(packet_buffer),
                                dtls_server_connect_notify,
                                dtls_server_receive_notify);

    /* Check for errors. */

    /* Initialize local server identity certificate with key
    and add to server. */
    status = nx_secure_x509_certificate_initialize(&certificate,
                                        device_cert_der,
                                        device_cert_der_len,
                                        NX_NULL,
                                        0, device_cert_key_der,
                                        device_cert_key_der_len,
                                        NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_local_certificate_add(&dtls_server,
                                                    &certificate, 1);


    /* Start server. */
    status = nx_secure_dtls_server_start(&dtls_server);

    /* Loop continuously to handle incoming data. */
    while(1)
    {
        /* Check for new connections. Muxtex handling omitted for clarity. */
        if(connect_flag)
        {
            /* We have a new connection attempt, start the DTLS session. */
            status = nx_secure_dtls_server_session_start(new_dtls_session,
                                                    NX_IP_PERIODIC_RATE);

            /* Check for errors. */
        }

        /* Check for received application data. */
        if(receive_flag)
        {
            /* We have received data over a previously-established DTLS session.
               Mutex handling omitted for clarity. */
            Status = nx_secure_dtls_session_receive(receive_dtls_session,
                                                    &receive_packet,
                                                    NX_IP_PERIODIC_RATE);

            /* Process received data… */

            /* Prepare and send response to client. */
        status = nx_secure_dtls_packet_allocate(receive_dtls_session,
                                                &packet_pool,
                                                &send_packet,
                                                NX_IP_PERIODIC_RATE);

        /* Check for errors and prepare response data
        (e.g. nx_packet_data_append). */

        /* Send response to client. */
        status = nx_secure_dtls_server_session_send(receive_dtls_session,
                                                            send_packet);

}

/* If not processing connections or received data, let the thread sleep. */
if(!connect_flag && !receive_flag)
{
    tx_thread_sleep(100);
}
    }

    /* Server processing is done, stop the server instance
    from accepting requests. */
    status = nx_secure_dtls_server_stop(&dtls_server);

    /* If we exit the processing loop, clean up the server. */
    status = nx_secure_dtls_server_delete(&dtls_server);
}

```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_dtls_server_start, nx_secure_dtls_server_delete,
- nx_secure_dtls_session_receive, nx_secure_dtls_server_session_create,
- nx_secure_dtls_server_session_start, nx_secure_dtls_server_session_stop,
- nx_secure_dtls_server_local_certificate_add

## <a name="nx_secure_dtls_server_session_start"></a>nx_secure_dtls_server_session_start

NetX güvenli DTLS sunucusundan DTLS oturumu başlatma

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_dtls_server_session_start(
                 NX_SECURE_DTLS_SESSION *session_ptr, UINT wait_option);

```

### <a name="description"></a>Açıklama

Bu hizmet, uzak bir DTLS Istemcisi sunucuya bağlanıp bir DTLS bağlantısı talep edildiğinde sunucu tarafı DTLS anlaşmasını gerçekleştirerek bir DTLS sunucu oturumu başlatır.

DTLS oturumu nx_secure_dtls_server_create için sunulan connect_notify geri çağırma yordamında alınır.

### <a name="parameters"></a>Parametreler

- **session_ptr** DTLS sunucusundan alınan DTLS oturum örneğinin işaretçisi connect_notify geri çağırma.
- **wait_option** Ağ işlemleri için kullanılacak ThreadX bekleme değeri.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) DTLS sunucusu başarıyla oluşturuldu.
- **NX_PTR_ERROR** (0x07) geçersiz işaretçi geçirildi.
- **NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) BIR DTLS el sıkışma paketi ayıramadı (paket havuzu boş).
- **NX_SECURE_TLS_INVALID_PACKET** (0x104) geçerli bir DTLS kaydı olmayan veri alındı.
- **NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0x108) DTLS kaydı düzgün bir şekilde karıştırılıp (şifreleme hatası) başarısız oldu.
- **NX_SECURE_TLS_PADDING_CHECK_FAILED** (0x12a) şifreleme doldurma denetimi hatası.
- **NX_SECURE_TLS_ALERT_RECEIVED** (0x114), DTLS el sıkışması sırasında uzak ana bilgisayardan bir uyarı alındı.
- **NX_SECURE_TLS_UNRECOGNIZED_MESSAGE_TYPE** (0x102), DTLS el sıkışması sırasında tanınmayan bir ileti aldı.
- **NX_SECURE_TLS_INCORRECT_MESSAGE_LENGTH** (0x10a), geçersiz uzunluğa sahıp bır DTLS kaydı alındı.
- **NX_SECURE_TLS_NO_SUPPORTED_CIPHERS** (0x10e), desteklenen DTLS cipherpaketlerine sahip olmayan bir ClientHello aldı.
- **NX_SECURE_TLS_BAD_COMPRESSION_METHOD** (0x118) bilinmeyen bir sıkıştırma yöntemiyle bir ClientHello alındı.
- **NX_SECURE_TLS_HANDSHAKE_FAILURE** (0X107) genel (belirtilmemiş) el sıkışma hatası, genellikle uzantı işleme sorunları nedeniyle.
- **NX_SECURE_TLS_UNSUPPORTED_FEATURE** (0x130) DTLS el sıkışması sırasında henüz desteklenmeyen bir özellik çağrılmıştı.
- **NX_SECURE_TLS_UNKNOWN_CIPHERSUITE** (0x105) bilinmeyen bir ciphersuite ile karşılaşıldı (iç şifreleme hatası belirtildi).
- **NX_SECURE_TLS_PROTOCOL_VERSION_CHANGED** (0x12e) eşleşmeyen DTLS sürümüne sahıp bır DTLS kaydı alındı.
- **NX_SECURE_TLS_FINISHED_HASH_FAILURE** (0x115) DTLS el sıkışma karmasını doğrulayamadı, oturum geçersiz.
- **NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) iç UDP gönderme başarısız oldu.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
#define DTLS_SERVER_SESSION (3)

/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Allocate space for DTLS sessions in the DTLS server. */
UCHAR dtls_server_session_buffer[sizeof(NX_SECURE_DTLS_SESSION)
* DTLS_SERVER_SESSIONS];

/* Flag used to indicate that a DTLS Client has connected. */
UINT connect_flag = 0;

/* Flag used to indicate application data reception. */
UINT receive_flag = 0;

/* Pointer to newly-connected DTLS session.
   NOTE: In practice this should be an array or list in case a new connection is
         attempted while a previous session is being started. */
NX_SECURE_DTLS_SESSION *new_dtls_session;

/* Pointer to session for application data receive.
   NOTE: Should be an array or list as
   with new_dtls_session */
NX_SECURE_DTLS_SESSION *receive_dtls_session;

/* Connect notify callback routine. */
UINT dtls_server_connect_notify(NX_SECURE_DTLS_SESSION *dtls_session,
                                    NXD_ADDRESS *ip_address, UINT port)
{
    /* NOTE: proper inter-thread communication procedures (e.g. mutex handling)
             Omitted for clarity. */

    /* Notify application thread that a connection request has been received. */
    connect_flag = 1;
    new_dtls_session = dtls_session;

    return(NX_SUCCESS);
}

/* Receive notify callback routine invoked when DTLS application data is received
   on an existing DTLS server session. */
UINT dtls_server_receive_notify(NX_SECURE_DTLS_SESSION *dtls_session)
{
    /* Receive and process DTLS record.
       NOTE: Mutex handling omitted for clarity. */
    receive_flag = 1;
    receive_dtls_session = dtls_session;

    return(NX_SUCCESS);
}

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
    NX_PACKET *send_packet;
    NX_PACKET *receive_packet;
    UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                LOCAL_SERVER_PORT, NX_IP_PERIODIC_RATE,
                                dtls_server_session_buffer,
                                sizeof(dtls_server_session_buffer),
                                &tls_crypto_table, crypto_metadata_buffer,
                                sizeof(crypto_metadata_buffer), packet_buffer,
                                sizeof(packet_buffer),
                                dtls_server_connect_notify,
                                dtls_server_receive_notify);

    /* Initialize local server identity certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&certificate, device_cert_der,
                                            device_cert_der_len, NX_NULL, 0,
                                            device_cert_key_der,
                                            device_cert_key_der_len,
                                            NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_local_certificate_add(&dtls_server,
                                                    &certificate, 1);

    /* Start server. */
    status = nx_secure_dtls_server_start(&dtls_server);

    /* Loop continuously to handle incoming data. */
    while(1)
    {
        /* Check for new connections. Muxtex handling omitted for clarity. */
        if(connect_flag)
        {
            /* We have a new connection attempt, start the DTLS session. */
            status = nx_secure_dtls_server_session_start(new_dtls_session,
                                                    NX_IP_PERIODIC_RATE);
        }

        /* Check for received application data. */
        if(receive_flag)
        {
            /* We have received data over a previously-established DTLS session.
               Mutex handling omitted for clarity. */
            Status = nx_secure_dtls_session_receive(receive_dtls_session,
                                                        &receive_packet,
                                                        NX_IP_PERIODIC_RATE);

            /* Process received data… */

            /* Prepare and send response to client. */
            status = nx_secure_dtls_packet_allocate(receive_dtls_session,
                                                    &packet_pool, &send_packet,
                                                    NX_IP_PERIODIC_RATE);

            /* Check for errors and prepare response data
            (e.g. nx_packet_data_append). */

            /* Send response to client. */
            status = nx_secure_dtls_server_session_send(receive_dtls_session,
                                                                send_packet);

        }

        /* If not processing connections or received data, let the thread sleep. */
        if(!connect_flag && !receive_flag)
        {
            tx_thread_sleep(100);
        }
    }

    /* Server processing is done,
    stop the server instance from accepting requests. */
    status = nx_secure_dtls_server_stop(&dtls_server);

    /* If we exit the processing loop, clean up the server. */
    status = nx_secure_dtls_server_delete(&dtls_server);
}

```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_dtls_server_start, nx_secure_dtls_server_delete,
- nx_secure_dtls_session_receive, nx_secure_dtls_server_session_send,
- nx_secure_dtls_server_session_create, nx_secure_dtls_server_session_stop,
- nx_secure_dtls_server_local_certificate_add

## <a name="nx_secure_dtls_server_start"></a>nx_secure_dtls_server_start

Yapılandırılmış UDP bağlantı noktasında dinleme yapan bir NetX güvenli DTLS sunucu örneği başlatın

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_dtls_server_start(
                  NX_SECURE_DTLS_SERVER *server_ptr);

```

### <a name="description"></a>Açıklama

Bu hizmet bir DTLS sunucusu başlatır. Çağrı geri döndüğünde, sunucu etkindir ve DTLS istemcilerinden gelen istekleri işlemeye başlayacaktır. Sunucu örneği, hizmet *nx_secure_dtls_server_create* yapılandırılmış olmalıdır.

> [!NOTE]
> Bu hizmet, iç DTLS sunucusu UDP bağlantı noktasını yapılandırılmış yerel bağlantı noktasına bağlar, bu nedenle karşılaşılan çoğu sorun UDP iletişimleri ve ağ yapılandırması ile yapılır.

### <a name="parameters"></a>Parametreler

- **server_ptr** Daha önce oluşturulmuş bir DTLS sunucu örneğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) sunucu başarıyla başlatıldı.
- **NX_PTR_ERROR** (0x07) geçersiz işaretçi geçirildi.
- **NX_NOT_ENABLED** (0x14) UDP etkin değil.
- **NX_NO_FREE_PORTS** (0x45) kullanılabilir UDP bağlantı noktası yok.
- **NX_INVALID_PORT** (0x46) geçersiz UDP bağlantı noktası.
- **NX_ALREADY_BOUND** (0x22) UDP bağlantı noktası zaten bağlıydı.
- **NX_PORT_UNAVAILABLE** (0x23) UDP bağlantı noktası kullanılamaz.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
#define DTLS_SERVER_SESSION (3)

/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Allocate space for DTLS sessions in the DTLS server. */
UCHAR dtls_server_session_buffer[sizeof(NX_SECURE_DTLS_SESSION)
                                        * DTLS_SERVER_SESSIONS];

/* Flag used to indicate that a DTLS Client has connected. */
UINT connect_flag = 0;

/* Flag used to indicate application data reception. */
UINT receive_flag = 0;

/* Pointer to newly-connected DTLS session.
   NOTE: In practice this should be an array or list in case a new connection is
         attempted while a previous session is being started. */
NX_SECURE_DTLS_SESSION *new_dtls_session;

/* Pointer to session for application data receive.
   NOTE: Should be an array or list as
   with new_dtls_session */
NX_SECURE_DTLS_SESSION *receive_dtls_session;

/* Connect notify callback routine. */
UINT dtls_server_connect_notify(NX_SECURE_DTLS_SESSION *dtls_session,
                                    NXD_ADDRESS *ip_address, UINT port)
{
    /* NOTE: proper inter-thread communication procedures (e.g. mutex handling)
             Omitted for clarity. */

    /* Notify application thread that a connection request has been received. */
    connect_flag = 1;
    new_dtls_session = dtls_session;

    return(NX_SUCCESS);
}

/* Receive notify callback routine invoked when DTLS application data is received
   on an existing DTLS server session. */
UINT dtls_server_receive_notify(NX_SECURE_DTLS_SESSION *dtls_session)
{
    /* Receive and process DTLS record.
       NOTE: Mutex handling omitted for clarity. */
    receive_flag = 1;
    receive_dtls_session = dtls_session;

    return(NX_SUCCESS);
}

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
    NX_PACKET *send_packet;
    NX_PACKET *receive_packet;
    UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                    LOCAL_SERVER_PORT,
                                    NX_IP_PERIODIC_RATE,
                                    dtls_server_session_buffer,
                                    sizeof(dtls_server_session_buffer),
                                    &tls_crypto_table,
                                    crypto_metadata_buffer,
                                    sizeof(crypto_metadata_buffer),
                                    packet_buffer,
                                    sizeof(packet_buffer),
                                    dtls_server_connect_notify,
                                    dtls_server_receive_notify);

    /* Initialize local server identity certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&certificate, device_cert_der,
                                            device_cert_der_len,
                                            NX_NULL, 0,
                                            device_cert_key_der,
                                            device_cert_key_der_len,
                                            NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_local_certificate_add(&dtls_server,
                                                        &certificate, 1);

    /* Start server. */
    status = nx_secure_dtls_server_start(&dtls_server);

    /* Loop continuously to handle incoming data. */
    while(1)
    {
        /* Check for new connections. Muxtex handling omitted for clarity. */
        if(connect_flag)
        {
            /* We have a new connection attempt, start the DTLS session. */
            status = nx_secure_dtls_server_session_start(new_dtls_session,
                                            NX_IP_PERIODIC_RATE);

            /* Check for errors. */
        }

        /* Check for received application data. */
        if(receive_flag)
        {
            /* We have received data over a previously-established DTLS session.
               Mutex handling omitted for clarity. */
            Status = nx_secure_dtls_session_receive(receive_dtls_session,
                                                        &receive_packet,
                                                        NX_IP_PERIODIC_RATE);

            /* Process received data… */

            /* Prepare and send response to client. */
            status = nx_secure_dtls_packet_allocate(receive_dtls_session, &packet_pool,
                &send_packet, NX_IP_PERIODIC_RATE);

            /* Check for errors and prepare response data
                (e.g. nx_packet_data_append). */

            /* Send response to client. */
            status = nx_secure_dtls_server_session_send(receive_dtls_session,
                send_packet);
        }

        /* If not processing connections or received data, let the thread sleep. */
        if(!connect_flag && !receive_flag)
        {
            tx_thread_sleep(100);
        }
    }

    /* If we exit the processing loop, clean up the server. */
    status = nx_secure_dtls_server_delete(&dtls_server);
}

```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_dtls_server_stop, nx_secure_dtls_server_create,
- nx_secure_dtls_server_delete, nx_secure_dtls_session_receive,
- nx_secure_dtls_server_session_send,
- nx_secure_dtls_server_session_start

## <a name="nx_secure_dtls_server_stop"></a>nx_secure_dtls_server_stop

Etkin bir NetX güvenli DTLS sunucu örneğini durdur

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_dtls_server_stop(NX_SECURE_DTLS_SERVER *server_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, bir DTLS sunucusunun UDP bağlantı noktasını yapılandırma bölümünde dinleme yaptığı ve tüm devam eden DTLS iletişimlerini sıfırlayıp tüm devam eden DTLS oturumlarını sıfırlamasından yanıt vermez.

### <a name="parameters"></a>Parametreler

- **server_ptr** Etkin bir DTLS sunucu örneği işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) sunucu başarıyla durdu.
- **NX_PTR_ERROR** (0x07) geçersiz işaretçi geçirildi.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
#define DTLS_SERVER_SESSION (3)

/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Allocate space for DTLS sessions in the DTLS server. */
UCHAR dtls_server_session_buffer[sizeof(NX_SECURE_DTLS_SESSION)
                                        * DTLS_SERVER_SESSIONS];

/* Flag used to indicate that a DTLS Client has connected. */
UINT connect_flag = 0;

/* Flag used to indicate application data reception. */
UINT receive_flag = 0;

/* Pointer to newly-connected DTLS session.
   NOTE: In practice this should be an array or list in case a new connection is
         attempted while a previous session is being started. */
NX_SECURE_DTLS_SESSION *new_dtls_session;

/* Pointer to session for application data receive.
   NOTE: Should be an array or list as
   with new_dtls_session */
NX_SECURE_DTLS_SESSION *receive_dtls_session;

/* Connect notify callback routine. */
UINT dtls_server_connect_notify(NX_SECURE_DTLS_SESSION *dtls_session,
                                    NXD_ADDRESS *ip_address, UINT port)
{
    /* NOTE: proper inter-thread communication procedures (e.g. mutex handling)
             Omitted for clarity. */

    /* Notify application thread that a connection request has been received. */
    connect_flag = 1;
    new_dtls_session = dtls_session;

    return(NX_SUCCESS);
}

/* Receive notify callback routine invoked when DTLS application data is received
   on an existing DTLS server session. */
UINT dtls_server_receive_notify(NX_SECURE_DTLS_SESSION *dtls_session)
{
    /* Receive and process DTLS record.
       NOTE: Mutex handling omitted for clarity. */
    receive_flag = 1;
    receive_dtls_session = dtls_session;

    return(NX_SUCCESS);
}

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
    NX_PACKET *send_packet;
    NX_PACKET *receive_packet;
    UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                    LOCAL_SERVER_PORT,
                                    NX_IP_PERIODIC_RATE,
                                    dtls_server_session_buffer,
                                    sizeof(dtls_server_session_buffer),
                                    &tls_crypto_table,
                                    crypto_metadata_buffer,
                                    sizeof(crypto_metadata_buffer),
                                    packet_buffer,
                                    sizeof(packet_buffer),
                                    dtls_server_connect_notify,
                                    dtls_server_receive_notify);

    /* Check for errors. */

    /* Initialize local server identity certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&certificate, device_cert_der,
                                            device_cert_der_len,
                                            NX_NULL, 0,
                                            device_cert_key_der,
                                            device_cert_key_der_len,
                                            NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_local_certificate_add(&dtls_server,
                                                        &certificate, 1);


    /* Start server. */
    status = nx_secure_dtls_server_start(&dtls_server);

    /* Loop continuously to handle incoming data. */
    while(1)
    {
        /* Check for new connections. Muxtex handling omitted for clarity. */
        if(connect_flag)
        {
            /* We have a new connection attempt, start the DTLS session. */
            status = nx_secure_dtls_server_session_start(new_dtls_session,
                                            NX_IP_PERIODIC_RATE);

            /* Check for errors. */
        }

        /* Check for received application data. */
        if(receive_flag)
        {
            /* We have received data over a previously-established DTLS session.
               Mutex handling omitted for clarity. */
            Status = nx_secure_dtls_session_receive(receive_dtls_session,
                                                    &receive_packet,
                                                    NX_IP_PERIODIC_RATE);

            /* Process received data… */

            /* Prepare and send response to client. */
            status = nx_secure_dtls_packet_allocate(receive_dtls_session,
                                                &packet_pool,
                                                &send_packet,
                                                NX_IP_PERIODIC_RATE);

            /* Check for errors and prepare response data
            (e.g. nx_packet_data_append). */

            /* Send response to client. */
            status = nx_secure_dtls_server_session_send(receive_dtls_session,
                send_packet);

        }

        /* If not processing connections or received data, let the thread sleep. */
        if(!connect_flag && !receive_flag)
        {
            tx_thread_sleep(100);
        }
    }

    /* We have exited the processing loop, stop the server. */
    status = nx_secure_dtls_server_stop(&dtls_server);

    /* If we exit the processing loop, clean up the server. */
    status = nx_secure_dtls_server_delete(&dtls_server);
}

```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_dtls_server_start, nx_secure_dtls_server_create,
- nx_secure_dtls_server_delete, nx_secure_dtls_session_receive,
- nx_secure_dtls_server_session_send,
- nx_secure_dtls_server_session_start

## <a name="nx_secure_dtls_server_trusted_certificate_add"></a>nx_secure_dtls_server_trusted_certificate_add

NetX güvenli DTLS sunucusuna güvenilir bir CA sertifikası ekleme

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_dtls_server_trusted_certificate_add(
                                         NX_SECURE_DTLS_SERVER *server_ptr,
                                         NX_SECURE_X509_CERT *certificate,
                                         UINT cert_id);

```

### <a name="description"></a>Açıklama

Bu hizmet, bir DTLS sunucu örneğine güvenilir bir CA veya ara CA sertifikası ekler ve tüm iç DTLS sunucusu oturumlarına atanır. Bu yalnızca, *nx_secure_dtls_server_x509_client_verify_configure* kullanılarak X. 509.440 istemci sertifikası kimlik doğrulamasının etkinleştirilmesi durumunda gereklidir. Eklenen sertifika, gelen Client X. 509.440 sertifikalarını doğrulamak için kullanılacaktır.

Cert_id parametresi, sertifika için sayısal, sıfır olmayan bir tanıtıcıdır. Bu, DTLS sunucu deposunda aynı X. 509.440 ortak adına sahip birden çok kimlik sertifikası bulunan olayda kolayca kaldırılmasını veya bu durumda bulunabilmesini sağlar. X. 509.440 sunucu sertifikaları hakkında daha fazla bilgi için NetX güvenli TLS Kullanıcı Kılavuzu 'na bakın.

### <a name="parameters"></a>Parametreler

- **server_ptr** Daha önce oluşturulmuş bir DTLS sunucu örneğine yönelik işaretçi.
- **sertifika** Daha önce başlatılmış bir X. 509.440 sertifika yapısına yönelik işaretçi.
- **cert_id** Bu DTLS sunucusunda bu sertifika için sıfır olmayan sayısal benzersiz tanımlayıcı.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) DTLS sunucusuna sertifikanın başarıyla eklenmesi.
- **NX_PTR_ERROR** (0x07) geçersiz işaretçi geçirildi.
- **NX_INVALID_PARAMETERS** (0x4D) BIR sertifika kimliği (0) geçirildi.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

* Daha kapsamlı bir örnek için bkz. *nx_secure_dtls_server_create* başvurusu.

```C
/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Certificate control block and data. */
NX_SECURE_X509_CERT trusted_ca_certificate;
UCHAR certificate_der_data[] = { … };

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                LOCAL_SERVER_PORT,
                                NX_IP_PERIODIC_RATE,
                                dtls_server_session_buffer,
                                sizeof(dtls_server_session_buffer),
                                &tls_crypto_table,
                                crypto_metadata_buffer,
                                sizeof(crypto_metadata_buffer),
                                packet_buffer,
                                sizeof(packet_buffer),
                                dtls_server_connect_notify,
                                dtls_server_receive_notify);

    /* Check for errors. */

    /* Initialize trusted certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&trusted_ca_certificate,
                                            certificate_der_data,
                                            sizeof(certificate_der_data),
                                            NX_NULL, 0, NX_NULL,
                                            0, NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add trusted CA certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_trusted_certificate_add(&dtls_server,
                                            &trusted_ca_certificate, 1);

    /* Start server. */
    status = nx_secure_dtls_server_start(&dtls_server);

    /* Loop continuously to handle incoming data. */
    while(1)
    {
        /* Process incoming requests and data. */
    }

}

```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_dtls_server_start, nx_secure_dtls_server_create,
- nx_secure_dtls_session_receive, nx_secure_dtls_server_session_send,
- nx_secure_dtls_server_session_start,
- nx_secure_dtls_server_local_certificate_add,
- nx_secure_dtls_server_trusted_certificate_remove,
- nx_secure_x509_certificate_initialize

## <a name="nx_secure_dtls_server_trusted_certificate_remove"></a>nx_secure_dtls_server_trusted_certificate_remove

NetX güvenli DTLS sunucusundan güvenilir bir CA sertifikasını kaldırma

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_dtls_server_trusted_certificate_remove(
                                NX_SECURE_DTLS_SERVER *server_ptr,
                                UCHAR *common_name,
                                UINT common_name_length,
                                UINT cert_id);

```

### <a name="description"></a>Açıklama

Bu hizmet, bir DTLS sunucu örneğinden güvenilir bir CA sertifikasını kaldırır. Güvenilen CA sertifikaları yalnızca, *nx_secure_dtls_server_x509_client_verify_configure* çağırarak X. 509.440 istemci sertifikası doğrulamasının etkinleştirildiği DTLS sunucusu için gereklidir.

Kaldırılacak sertifika, X. 509.440 ortak adı ya da *nx_secure_dtls_server_trusted_certificate_add* çağrısında atanan sayısal cert_id tarafından belirlenebilir. Cert_id yalnızca sertifikayı tanımlamak için kullanılır ve uygulama tarafından korunur. Sayısal sertifika tanımlayıcısı yerine ortak ad kullanılırsa, cert_id parametresi 0 olarak ayarlanmalıdır.

> [!NOTE]
> Bir DTLS el sıkışması işlenirken bir sertifikayı kaldırmak beklenmedik davranışa neden olabilir. Sertifikalar kaldırılmadan önce hizmet *nx_secure_dtls_server_stop* çağrılmalıdır.

### <a name="parameters"></a>Parametreler

- **server_ptr** Daha önce oluşturulmuş bir DTLS sunucu örneğine yönelik işaretçi.
- **common_name** Kaldırılacak sertifikanın X. 509.440 CommonName. Bu kullanılırsa, cert_id sıfır olarak geçirin.
- **common_name_length** Bayt cinsinden common_name dize uzunluğu.
- **cert_id** Bu DTLS sunucusunda bu sertifika için sıfır olmayan sayısal benzersiz tanımlayıcı. Bu kullanılırsa, common_name parametresi için NX_NULL geçirin.


### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) DTLS sunucusundan sertifikanın başarıyla kaldırılması.
- **NX_PTR_ERROR** (0x07) geçersiz işaretçi geçirildi.
- **NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) VERILEN DTLS sunucusunda cert_id veya common_name eşleşen bir sertifika bulunamadı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Certificate control block and data. */
NX_SECURE_X509_CERT trusted_ca_certificate;
UCHAR certificate_der_data[] = { … };

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                    LOCAL_SERVER_PORT,
                                    NX_IP_PERIODIC_RATE,
                                    dtls_server_session_buffer,
                                    sizeof(dtls_server_session_buffer),
                                    &tls_crypto_table,
                                    crypto_metadata_buffer,
                                    sizeof(crypto_metadata_buffer),
                                    packet_buffer,
                                    sizeof(packet_buffer),
                                    dtls_server_connect_notify,
                                    dtls_server_receive_notify);

    /* Check for errors. */

    /* Initialize trusted certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&trusted_ca_certificate,
                                                    certificate_der_data,
                                                    sizeof(certificate_der_data),
                                                    NX_NULL, 0, NX_NULL, 0,
                                                    NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_trusted_certificate_add(&dtls_server,
                                                       &trusted_ca_certificate, 1);

    /* Start server. */
    status = nx_secure_dtls_server_start(&dtls_server);

    /* Process client requests, etc… */

    /* Stop the server before removing a certificate. */
    Status = nx_secure_dtls_server_stop(&dtls_server);


/* At some point in the future we decide to remove the certificate we added. We can
       use the certificate identifier we passed into the call to
       nx_secure_dtls_trusted_certificate_add (value = 1); */
    status = nx_secure_dtls_server_trusted_certificate_remove(&dtls_server,
                                                          NX_NULL, 0, 1);

}

```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_dtls_server_start, nx_secure_dtls_server_create,
- nx_secure_dtls_server_session_start,
- nx_secure_dtls_server_session_stop,
- nx_secure_dtls_server_trusted_certificate_add,
- nx_secure_x509_certificate_initialize

## <a name="nx_secure_dtls_server_x509_client_verify_configure"></a>nx_secure_dtls_server_x509_client_verify_configure

İstemci sertifikaları istemek ve doğrulamak için bir NetX güvenli DTLS sunucusu yapılandırma

### <a name="prototype"></a>Prototype

```C
UINT nx_secure_dtls_server_x509_client_verify_configure(
                           NX_SECURE_DTLS_SERVER *server_ptr,
                               UINT certs_per_session,
                               UCHAR *certs_buffer, ULONG buffer_size);

```

### <a name="description"></a>Açıklama

Bu hizmet DTLS Istemci sertifikalarını istemek ve doğrulamak üzere bir DTLS sunucusunu yapılandırır. Bu isteğe bağlı özellik, istemci kimlik doğrulaması için diğer mekanizmaların yerine X. 509.440 sertifikaları istendiğinde kullanılır (örneğin, önceden paylaşılan bir anahtar).

> [!IMPORTANT]
> *Bu hizmeti kullanarak istemci sertifikalarını doğrulamak üzere bir DTLS sunucusu yapılandırıldığında, nx_secure_dtls_server_trusted_certificate_add kullanarak sunucuya en az bir güvenilir CA sertifikası eklenmelidir veya istemci sertifikalarını güvenilir depoya doğrulayamayacak olduğundan sunucu tüm gelen istemci bağlantılarını reddeder.*

Bu hizmet çağrıldıktan sonra DTLS sunucu örneği (başlatıldıktan sonra) DTLS el sıkışmasının bir parçası olarak istemci sertifikaları ister. İstemcinin bir kimlik sertifikası (ve uygulanabilirse ilişkili sertifika zinciri) ile düzgün şekilde yapılandırıldığı varsayılarak, DTLS sunucusu, istemci sertifikası verilerini işlemek için belleğin ayrılmasını gerektirir. Bu bellek *certs_buffer* parametresi olarak geçirilir.

Certs_buffer bir DTLS istemcisinden beklenen en büyük sertifika zincirini, her *zaman DTLS sunucusu oturumlarının sayısını* kapsayacak şekilde boyutlandırılmalıdır. Arabellek, bir Istemci sertifika zincirindeki beklenen en fazla sertifika sayısını temsil eden *certs_per_session* parametresi kullanılarak kullanılabilir Oturumlar arasında bölünür. Arabellek Ayrıca, sertifika verilerini ayrıştırmak için kullanılan NX_SECURE_X509_CERT veri yapısına boşluk sağlamalıdır.

Uygun arabellek boyutunu hesaplamak aşağıdaki formül ile yapılabilir:

```C
buffer_size = (# of DTLS sessions in server) *
                (certs_per_session) *
                (    maximum expected certificate size +
                      sizeof(NX_SECURE_X509_CERT)    )

```

- DTLS oturumlarının sayısı, nx_secure_dtls_server_create iletilen oturum arabelleğinin boyutuna göre belirlenir.
- certs_per_session, herhangi bir istemci sertifika zincirindeki beklenen en fazla sertifika sayısına ayarlanmalıdır.
- En büyük beklenen sertifika boyutu uygulamaya, anahtar boyutlarına ve diğer faktörlere bağlıdır, ancak 2KB genellikle yeterlidir.

### <a name="parameters"></a>Parametreler

- **server_ptr** Daha önce oluşturulmuş bir DTLS sunucu örneğine yönelik işaretçi.
- **certs_per_session** Her DTLS sunucu oturumuna ayrılacak sertifika sayısı.
- **certs_buffer** Gelen sertifika verileri için arabellek alanı.
- **Buffer_size** Sertifika arabelleğinin boyutu.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) X. 509.440 Istemci doğrulamasının başarılı yapılandırması.
- **NX_PTR_ERROR** (0x07) geçersiz işaretçi geçirildi.
- **NX_INVALID_PARAMETERS** (0x4D) geçersiz sertifika deposu (DTLSserver örneği başlatılmadı mi?).

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Configure number of sessions per server. */
#define DTLS_SERVER_SESSIONS 3

/* Define parameters for X.509 client verification. */
#define MAX_CERT_SIZE         (2000)       /* 2KB expected maximum certificate size. */
#define CERTS_PER_SESSION (3)            /* Assume maximum chain length of 3 certificates. */
#define CERT_BUFFER_SIZE     (DTLS_SERVER_SESSIONS * CERTS_PER_SESSION * \
 (MAX_CERT_SIZE + sizeof(NX_SECURE_X509_CERT))

/* Define our incoming certificate buffer. */
UCHAR client_certs_buffer[CERT_BUFFER_SIZE];

/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Certificate control block and data. */
NX_SECURE_X509_CERT trusted_ca_certificate;
UCHAR certificate_der_data[] = { … };

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                    LOCAL_SERVER_PORT,
                                    NX_IP_PERIODIC_RATE,
                                    dtls_server_session_buffer,
                                    sizeof(dtls_server_session_buffer),
                                    &tls_crypto_table,
                                    crypto_metadata_buffer,
                                    sizeof(crypto_metadata_buffer),
                                    packet_buffer,
                                    sizeof(packet_buffer),
                                    dtls_server_connect_notify,
                                    dtls_server_receive_notify);

    /* Check for errors. */

    /* Initialize trusted certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&trusted_ca_certificate,
                                    certificate_der_data,
                                    sizeof(certificate_der_data),
                                    NX_NULL, 0,
                                    NX_NULL, 0, NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_trusted_certificate_add(&dtls_server,
                                                &trusted_ca_certificate, 1);

    /* Configure client X.509 authentication and verification. */
    status = nx_secure_dtls_server_x509_client_verify_configure(&dtls_server,
        CERTS_PER_SESSION,
        client_certs_buffer,
        sizeof(client_certs_buffer));

    /* Start server. */
    status = nx_secure_dtls_server_start(&dtls_server);

    /* Process client requests, etc… */
}

```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_dtls_server_x509_client_verify_disable,
- nx_secure_dtls_server_start, nx_secure_dtls_server_create,
- nx_secure_dtls_server_session_start,
- nx_secure_dtls_server_session_stop,
- nx_secure_dtls_server_trusted_certificate_add,
- nx_secure_x509_certificate_initialize

## <a name="nx_secure_dtls_server_x509_client_verify_disable"></a>nx_secure_dtls_server_x509_client_verify_disable

NetX güvenli DTLS sunucusu için Client X. 509.952 sertifikası doğrulamasını devre dışı bırakır

### <a name="prototype"></a>Prototype

```C
UINT nx_secure_dtls_server_x509_client_verify_disable(
                           NX_SECURE_DTLS_SERVER *server_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, bir DTLS sunucusunda X. 509.440 Istemci sertifikası doğrulamasını devre dışı bırakır. X. 509.440 Istemci sertifikası doğrulaması etkinleştirilmemişse hizmetin hiçbir etkisi yoktur.

> [!NOTE]
> Etkin bir DTLS sunucu örneğinde istemci kimlik doğrulamasının devre dışı bırakılması öngörülemeyen davranışlara neden olabilir. Sunucu durumunu değiştirmeden önce nx_secure_dtls_server_stop hizmeti çağrılmalıdır.

### <a name="parameters"></a>Parametreler

- **server_ptr** Daha önce oluşturulmuş bir DTLS sunucu örneğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- X. 509.440 istemci kimlik doğrulamasının başarıyla devre dışı bırakılması **NX_SUCCESS** (0x00).
- **NX_PTR_ERROR** (0x07) geçersiz işaretçi geçirildi.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Configure number of sessions per server. */
#define DTLS_SERVER_SESSIONS 3

/* Define parameters for X.509 client verification. */
#define MAX_CERT_SIZE         (2000)       /* 2KB expected maximum certificate size. */
#define CERTS_PER_SESSION (3)            /* Assume maximum chain length of 3 certificates. */
#define CERT_BUFFER_SIZE     (DTLS_SERVER_SESSIONS * CERTS_PER_SESSION * \
 (MAX_CERT_SIZE + sizeof(NX_SECURE_X509_CERT))

/* Define our incoming certificate buffer. */
UCHAR client_certs_buffer[CERT_BUFFER_SIZE];

/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Certificate control block and data. */
NX_SECURE_X509_CERT trusted_ca_certificate;
UCHAR certificate_der_data[] = { … };

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                    LOCAL_SERVER_PORT,
                                    NX_IP_PERIODIC_RATE,
                                    dtls_server_session_buffer,
                                    sizeof(dtls_server_session_buffer),
                                    &tls_crypto_table,
                                    crypto_metadata_buffer,
                                    sizeof(crypto_metadata_buffer),
                                    packet_buffer,
                                    sizeof(packet_buffer),
                                    dtls_server_connect_notify,
                                    dtls_server_receive_notify);

    /* Check for errors. */

    /* Initialize trusted certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&trusted_ca_certificate,
                                    certificate_der_data,
                        sizeof(certificate_der_data), NX_NULL, 0,
                        NX_NULL, 0, NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_trusted_certificate_add(&dtls_server,
                                            &trusted_ca_certificate, 1);

    /* Configure client X.509 authentication and verification. */
    status = nx_secure_dtls_server_x509_client_verify_configure(&dtls_server,
        CERTS_PER_SESSION,
        client_certs_buffer,
        sizeof(client_certs_buffer));

    /* Start server. */
    status = nx_secure_dtls_server_start(&dtls_server);

    /* Process client requests, etc… */

    /* Stop the server before changing state. */
    status = nx_secure_dtls_server_stop(&dtls_server);

    /* Disable X.509 authentication and verification. */
    status = nx_secure_dtls_server_x509_client_verify_disable(&dtls_server);

}

```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_dtls_server_x509_client_verify_configure,
- nx_secure_dtls_server_start, nx_secure_dtls_server_create,
- nx_secure_dtls_server_session_start,
- nx_secure_dtls_server_session_stop,
- nx_secure_dtls_server_trusted_certificate_add,
- nx_secure_x509_certificate_initialize

## <a name="nx_secure_dtls_session_client_info_get"></a>nx_secure_dtls_session_client_info_get

Bir DTLS sunucu oturumundan uzak istemci bilgilerini al

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_dtls_session_client_info_get(
                                    NX_SECURE_DTLS_SESSION *session_ptr,
                                    NXD_ADDRESS *client_ip_address,
                                    UINT *client_port, UINT *local_port);

```

### <a name="description"></a>Açıklama

Bu hizmet, belirli bir DTLS sunucusu oturumuna bağlı olan bir DTLS Istemcisiyle ilgili ağ bilgilerini döndürür. Döndürülen bilgiler, uzak istemcinin IP adresinden ve UDP bağlantı noktasından ve istemcinin bağlı olduğu yerel sunucu bağlantı noktasından oluşur.

Genel olarak, DTLS oturum örneği, DTLS bildirim geri çağırma yordamlarından birini çağırmada elde edilen bir işlem olacaktır (örn. connect_notify veya receive_notify geri çağrılar nx_secure_dtls_server_create).

### <a name="parameters"></a>Parametreler

- **session_ptr** Etkin bir DTLS sunucu oturumu örneği işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) sunucu başarıyla silindi.
- **NX_PTR_ERROR** (0x07) geçersiz işaretçi geçirildi.
- **NX_INVALID_SOCKET** (0x13) ilişkili UDP yuvası geçerli değil (oturum başlatılmamış mi?).
- **NX_NOT_CONNECTED** (0x38) UDP yuvası bağlı değil – istemci bağlantısı bırakılmıştı veya henüz kurulmadı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
#define DTLS_SERVER_SESSION (3)

/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Allocate space for DTLS sessions in the DTLS server. */
UCHAR dtls_server_session_buffer[sizeof(NX_SECURE_DTLS_SESSION)
                                        * DTLS_SERVER_SESSIONS];

/* Flag used to indicate that a DTLS Client has connected. */
UINT connect_flag = 0;

/* Flag used to indicate application data reception. */
UINT receive_flag = 0;

/* Pointer to newly-connected DTLS session.
   NOTE: In practice this should be an array
   or list in case a new connection is
   attempted while a previous session is being started. */
NX_SECURE_DTLS_SESSION *new_dtls_session;

/* Pointer to session for application data receive.
NOTE: Should be an array or list as
   with new_dtls_session */
NX_SECURE_DTLS_SESSION *receive_dtls_session;

/* Connect notify callback routine. */
UINT dtls_server_connect_notify(NX_SECURE_DTLS_SESSION *dtls_session, NXD_ADDRESS
                                                            *ip_address, UINT port)
{
    /* NOTE: proper inter-thread communication procedures (e.g. mutex handling)
             Omitted for clarity. */

    /* Notify application thread that a connection request has been received. */
    connect_flag = 1;
    new_dtls_session = dtls_session;

    return(NX_SUCCESS);
}

/* Receive notify callback routine invoked when DTLS application data is received
   on an existing DTLS server session. */
UINT dtls_server_receive_notify(NX_SECURE_DTLS_SESSION *dtls_session)
{
    NXD_ADDRESS client_ip;
    UINT client_port, server_port;

    /* Get DTLS client information which can be used in filtering or associating
       the DTLS session with application data (e.g. a session pointer table). */
    status = nx_secure_dtls_session_client_info_get(dtls_session, &client_ip,
   &client_port, &server_port);

    /* Receive and process DTLS record.
       NOTE: Mutex handling omitted for clarity. */
    receive_flag = 1;
    receive_dtls_session = dtls_session;

    return(NX_SUCCESS);
}

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
    NX_PACKET *send_packet;
    NX_PACKET *receive_packet;
    UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                            LOCAL_SERVER_PORT,
                                            NX_IP_PERIODIC_RATE,
                                            dtls_server_session_buffer,
                                            sizeof(dtls_server_session_buffer),
                                            &tls_crypto_table,
                                            crypto_metadata_buffer,
                                            sizeof(crypto_metadata_buffer),
                                            packet_buffer,
                                            sizeof(packet_buffer),
                                            dtls_server_connect_notify,
                                            dtls_server_receive_notify);

    /* Check for errors. */

    /* Initialize local server identity certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&certificate,
                                            device_cert_der,
                                            device_cert_der_len,
                                            NX_NULL, 0,
                                            device_cert_key_der,
                                            device_cert_key_der_len,
                                            NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_local_certificate_add(&dtls_server,
                                                        &certificate, 1);


    /* Start server. */
    status = nx_secure_dtls_server_start(&dtls_server);

    /* Loop continuously to handle incoming data. */
    while(1)
    {
        /* Check for new connections. Muxtex handling omitted for clarity. */
        if(connect_flag)
        {
            /* We have a new connection attempt, start the DTLS session. */
            status = nx_secure_dtls_server_session_start(new_dtls_session,
                                            NX_IP_PERIODIC_RATE);

            /* Check for errors. */
        }

        /* Check for received application data. */
        if(receive_flag)
        {
            /* We have received data over a previously-established DTLS session.
               Mutex handling omitted for clarity. */
            Status = nx_secure_dtls_session_receive(receive_dtls_session,
                                                    &receive_packet,
                                                    NX_IP_PERIODIC_RATE);

            /* Process received data… */

            /* Prepare and send response to client. */
            status = nx_secure_dtls_packet_allocate(receive_dtls_session,
                                                &packet_pool,
                                                &send_packet,
                                                NX_IP_PERIODIC_RATE);

            /* Check for errors and prepare response data
            (e.g. nx_packet_data_append). */

            /* Send response to client. */
            status = nx_secure_dtls_server_session_send(receive_dtls_session,
                send_packet);
        }

        /* If not processing connections or received data, let the thread sleep. */
        if(!connect_flag && !receive_flag)
        {
            tx_thread_sleep(100);
        }
    }

    /* If we exit the processing loop, clean up the server. */
    status = nx_secure_dtls_server_delete(&dtls_server);
}

```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_dtls_server_start, nx_secure_dtls_server_stop,
- nx_secure_dtls_server_create, nx_secure_dtls_server_delete,
- nx_secure_dtls_session_receive, nx_secure_dtls_server_session_send,
- nx_secure_dtls_server_session_start

## <a name="nx_secure_dtls_session_create"></a>nx_secure_dtls_session_create

NetX güvenli DTLS oturumu oluşturma ve yapılandırma

### <a name="prototype"></a>Prototype

```C
UINT nx_secure_dtls_session_create(
                        NX_SECURE_DTLS_SESSION *dtls_session,
                        const NX_SECURE_TLS_CRYPTO *crypto_table,
                        VOID *metadata_buffer, ULONG metadata_size,
                        UCHAR *packet_reassembly_buffer,
                        UINT packet_reassembly_buffer_size,
                        UINT certs_number,
                        UCHAR *remote_certificate_buffer,
                        ULONG remote_certificate_buffer_size));

```

### <a name="description"></a>Açıklama

Bu hizmet bir DTLS oturumu oluşturur ve yapılandırır. Genel olarak, DTLS sunucu oturumları DTLS sunucu mekanizması (bkz. *nx_secure_dtls_server_create*) ile yönetildiği için bu durum genellikle DTLS istemci oturumları oluşturmak için kullanılır, ancak bir uygulamanın tek bir tek başına DTLS sunucu oturumu örneği oluşturması gereken durumlarda bu hizmet, bu <sup>hizmetin kullanılabileceği durumlar</sup>olabilir.

Parametreler, bir DTLS oturumunun örneğini oluşturmak için gereken bilgileri ve bellek ayırmayı yapılandırır. Crypto_table parametresi, TLS/DTLS şifrelemesi ve kimlik doğrulaması için gerekli tüm şifreleme yordamlarını içeren bir TLS tablosudur. Metadata_buffer şifreleme kullanıcıları için kullanılır (NetX güvenli TLS kullanıcı kılavuzunda nx_secure_tls_metadata_size_calculate bakın) ve packet_reassembly_buffer, UDP datagramlarını şifre çözme için tamamen bir DTLS kaydına yeniden birleştirmek için kullanılır.

Certs_number ve remote_certificate_buffer, gelen DTLS sunucusu sertifika zincirini depolamak ve işlemek için alan gerektiren DTLS Istemcileri için gereklidir. Arabelleğin bağlanacağı her sunucu için, Sertifika zincirinin beklenen en büyük boyutuna uyum sağlaması gerekir. Arabellek, beklenen sertifika sayısına (certs_number parametresi) bölünür ve ayrıca sertifika başına bir NX_SECURE_X509_CERT yapısını tutabilecek kadar büyük olmalıdır. Arabellek boyutu aşağıdaki formül kullanılarak belirlenebilir:

```C
remote_certificate_buffer_size = (certs_number) *
                 (maximum cert size + sizeof(NX_SECURE_X509_CERT))
```

- certs_number, sunucunun sertifika zincirindeki beklenen en fazla sertifika sayısıdır
- En büyük sertifika boyutu, kullanılan anahtarların boyutuna ve sertifikadaki bilgilere bağlıdır, ancak 2KB genellikle yeterlidir.

**7** Bu yordam ile DTLS sunucu oturumları oluşturma önerilmez ve bazı sınırlamalar gelir. Birincil sorun, oturumun ek istemci bağlantılarını düzgün bir şekilde işleyememesi gerekir. UDP bağlantısı olmadığından, önceki bir DTLS oturumu hala etkin olduğunda, sunucu oturumunun bir hata ile sonlanmasına neden olacak şekilde sunucunun UDP bağlantı noktasına yasal olarak veri gönderebileceği anlamına gelir.

### <a name="parameters"></a>Parametreler

- **dtls_session** Başlatılmamış DTLS oturum yapısına yönelik işaretçi.
- **crypto_table** Tüm şifreleme işlemleri için kullanılan TLS/DTLS Şifreleme tablosu yapısına yönelik işaretçi.
- **crypto_metadata_buffer** Şifreleme işlemi hesaplamaları ve durum bilgileri için arabellek alanı.
- **crypto_metadata_size** Meta veri arabelleğinin boyutu.
- **packet_reassembly_buffer** DTLS tarafından, IP verilerini şifre çözme için DTLS kayıtlarına yeniden birleştirmek üzere kullanılan arabellek.
- **packet_reassembly_buffer_size** Yeniden birleştirme arabelleğinin boyutu. Genellikle 16KB 'den büyük olmalıdır, ancak uygulamaya bağlı olarak daha küçük olabilir.
- **certs_number** Uzak sunucunun sertifika zincirindeki en fazla beklenen sertifika sayısı.
- **remote_certificate_buffer** Gelen sertifika verileri için arabellek alanı.
- **remote_certificate_buffer_size** Sertifika arabelleğinin boyutu.


### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı oturum oluşturma.
- **NX_PTR_ERROR** (0x07) geçersiz oturum veya arabellek işaretçisi.
- **NX_INVALID_PARAMETERS** (0x4D) paket yeniden birleştirme, sertifikalar veya şifreleme için yeterli arabellek alanı yok.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Sockets, sessions, certificates defined in global static space to preserve
   application stack. */
NX_SECURE_DTLS_SESSION client_dtls_session;

/* Trusted certificate structure and raw data. */
NX_SECURE_X509_CERT trusted_cert;
const UCHAR trusted_cert_der = { … };

/* Cryptography routines and crypto work buffers. */
extern const NX_SECURE_TLS_CRYPTO nx_crypto_tls_ciphers;
UCHAR crypto_metadata[9000];

/* Packet reassembly buffer for decryption. */
UCHAR packet_buffer[4000];

/* Remote certificate buffer for incoming certificates. */
#define REMOTE_CERT_SIZE (sizeof(NX_SECURE_X509_CERT) + 2000)
#define REMOTE_CERT_NUMBER  (3)
UCHAR remote_certs_buffer[REMOTE_CERT_SIZE * REMOTE_CERT_NUMBER];

/* Application thread where TLS session is started. */
void application_thread()
{
NXD_ADDRESS server_ip;

    /* Create a TLS session for our socket. Ciphers and metadata defined
    elsewhere. See nx_secure_tls_session_create reference for more
    information. */
        status =  nx_secure_dtls_session_create(&client_dtls_session,
                                            &nx_crypto_tls_ciphers,
                                            crypto_metadata,
                                            sizeof(crypto_metadata),
                                            packet_buffer,
                                            sizeof(packet_buffer),
                                            REMOTE_CERT_NUMBER,
                                            remote_certs_buffer,
                                            sizeof(remote_certs_buffer));

    /* Check for error.  */
    if(status)
    {
        printf("Error in function nx_secure_dtls_session_create: 0x%x\n", status);
    }

    /* Initialize our trusted certificate. See section “Importing X.509
    Certificates into NetX Secure” for more information. */
    nx_secure_x509_certificate_initialize(&trusted_certificate,
                                    trusted_cert_der,
                                    trusted_cert_der_len,
                                    NX_NULL, 0, NX_NULL, 0,
                                    NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add the certificate to the local store using a numeric ID. */
    nx_secure_dtls_session_trusted_certificate_add(&client_dtls_session,
    &certificate, 1);

    /* Set up IP address of remote host. */
    server_ip.nxd_ip_version = NX_IP_VERSION_V4;
    server_ip.nxd_ip_address.v4 = IP_ADDRESS(192, 168, 1, 150);


    /* Now we can start the DTLS session as normal. */
    status =  nx_secure_dtls_client_session_start(&client_dtls_session,
                                            &udp_socket, &server_ip,
                                            4443,
                                            NX_IP_PERIODIC_RATE);

    if(status != NX_SUCCESS)
    {
        /* Error! */
        return(status);
    }

    /* Add data to send packet as usual for NX_PACKET and send to server.  */
    status = nx_secure_dtls_session_send(&client_dtls_session,
                                                &send_packet,
                                                &server_ip, 4443);

    /* Receive response from server. */
    status = nx_secure_dtls_session_receive(&client_dtls_session,
                                            &receive_packet,
                                            NX_IP_PERIODIC_RATE);

    /* Process response. */

    /* Shut down DTLS session. */
        status = nx_secure_dtls_session_end(&client_dtls_session,
                                            NX_IP_PERIODIC_RATE);

    /* Clean up. */
        status = nx_secure_dtls_session_delete(&client_dtls_session);

}

```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_dtls_client_session_start, nx_secure_dtls_session_receive,
- nx_secure_dtls_session_send

## <a name="nx_secure_dtls_session_delete"></a>nx_secure_dtls_session_delete

NetX güvenli DTLS oturumu tarafından kullanılan kaynakları boşaltma

### <a name="prototype"></a>Prototype

```C
UINT nx_secure_dtls_session_delete(
                        NX_SECURE_DTLS_SESSION *dtls_session);

```

### <a name="description"></a>Açıklama

Bu hizmet, bir DTLS oturumunu siler ve oluşturulduğu zaman ayrılan kaynakları serbest bırakır.

### <a name="parameters"></a>Parametreler

- **dtls_session** Daha önce başlatılmış olan DTLS oturum yapısına yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) oturumu başarıyla silindi.
- **NX_PTR_ERROR** (0x07) geçersiz oturum veya arabellek işaretçisi.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Sockets, sessions, certificates defined in global static space to preserve
   application stack. */
NX_SECURE_DTLS_SESSION client_dtls_session;

/* Trusted certificate structure and raw data. */
NX_SECURE_X509_CERT trusted_cert;
const UCHAR trusted_cert_der = { … };

/* Cryptography routines and crypto work buffers. */
extern const NX_SECURE_TLS_CRYPTO nx_crypto_tls_ciphers;
UCHAR crypto_metadata[9000];

/* Packet reassembly buffer for decryption. */
UCHAR packet_buffer[4000];

/* Remote certificate buffer for incoming certificates. */
#define REMOTE_CERT_SIZE (sizeof(NX_SECURE_X509_CERT) + 2000)
#define REMOTE_CERT_NUMBER  (3)
UCHAR remote_certs_buffer[REMOTE_CERT_SIZE * REMOTE_CERT_NUMBER];

/* Application thread where TLS session is started. */
void application_thread()
{
    NXD_ADDRESS server_ip;

    /* Create a TLS session for our socket. Ciphers and metadata defined
    elsewhere. See nx_secure_tls_session_create reference for more
    information. */
        status =  nx_secure_dtls_session_create(&client_dtls_session,
                                            &nx_crypto_tls_ciphers,
                                            crypto_metadata,
                                            sizeof(crypto_metadata),
                                            packet_buffer,
                                            sizeof(packet_buffer),
                                            REMOTE_CERT_NUMBER,
                                            remote_certs_buffer,
                                            sizeof(remote_certs_buffer));

    /* Check for error.  */
    if(status)
    {
        printf("Error in function nx_secure_dtls_session_create: 0x%x\n", status);
    }

    /* Initialize our trusted certificate. See section “Importing X.509
    Certificates into NetX Secure” for more information. */
        nx_secure_x509_certificate_initialize(&trusted_certificate,
                                        trusted_cert_der,
                                        trusted_cert_der_len,
                                        NX_NULL, 0, NX_NULL, 0,
                                        NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add the certificate to the local store using a numeric ID. */
    nx_secure_dtls_session_trusted_certificate_add(&client_dtls_session,
                                                        &certificate, 1);

    /* Set up IP address of remote host. */
    server_ip.nxd_ip_version = NX_IP_VERSION_V4;
    server_ip.nxd_ip_address.v4 = IP_ADDRESS(192, 168, 1, 150);


    /* Now we can start the DTLS session as normal. */
    status =  nx_secure_dtls_client_session_start(&client_dtls_session,
                                                    &udp_socket,
                                                    &server_ip, 4443,
                                                    NX_IP_PERIODIC_RATE);

    if(status != NX_SUCCESS)
    {
        /* Error! */
        return(status);
    }

    /* Add data to send packet as usual for NX_PACKET and send to server.  */
    status = nx_secure_dtls_session_send(&client_dtls_session, &send_packet,
                                                        &server_ip, 4443);

        /* Receive response from server. */
        status = nx_secure_dtls_session_receive(&client_dtls_session,
                                                &receive_packet,
                                                NX_IP_PERIODIC_RATE);

    /* Process response. */

    /* Shut down DTLS session. */
        status = nx_secure_dtls_session_end(&client_dtls_session,
                                            NX_IP_PERIODIC_RATE);

    /* Clean up. */
        status = nx_secure_dtls_session_delete(&client_dtls_session);

}

```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_dtls_client_session_start, nx_secure_dtls_session_receive,
- nx_secure_dtls_session_send, nx_secure_dtls_session_delete

## <a name="nx_secure_dtls_session_end"></a>nx_secure_dtls_session_end

Etkin bir NetX güvenli DTLS oturumunu kapatma

### <a name="prototype"></a>Prototype

```C
UINT nx_secure_dtls_session_end(NX_SECURE_DTLS_SESSION *dtls_session,
                                UINT wait_option);

```

### <a name="description"></a>Açıklama

Bu hizmet, uzak konağa bir TLS/DTLS CloseNotify uyarısı göndererek etkin bir DTLS oturumunu sonlandırır. Kullanılan IP adresi ve bağlantı noktası, önceki nx_secure_dtls_session_send çağrısında kullanılan olanlardır.

### <a name="parameters"></a>Parametreler

- **dtls_session** Daha önce başlatılmış olan DTLS oturum yapısına yönelik işaretçi.
- **wait_option** Ağ işlemleri için kullanılacak ThreadX bekleme değeri.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) oturumu başarıyla silindi.
- **NX_PTR_ERROR** (0x07) geçersiz oturum veya arabellek işaretçisi.
- **NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0X111), CloseNotify uyarısı için paket (ler) ayıramadı.
- **NX_SECURE_TLS_UNKNOWN_CIPHERSUITE** (0x105) büyük olasılıkla iç hata – şifreleme yordamı tanınmıyor.
- Temel alınan UDP gönderimi **NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) başarısız oldu.
- **NX_IP_ADDRESS_ERROR** (0x21) uzak ana bilgisayar IP adresi hatası.
- **NX_NOT_BOUND** (0x24) temel alınan UDP yuvası, bağlantı noktasına bağlanmadı.
- **NX_INVALID_PORT** (0x46) geçersiz UDP bağlantı noktası.
- **NX_PORT_UNAVAILABLE** (0x23) UDP bağlantı noktası kullanılamaz.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Sockets, sessions, certificates defined in global static space to preserve
   application stack. */
NX_SECURE_DTLS_SESSION client_dtls_session;

/* Trusted certificate structure and raw data. */
NX_SECURE_X509_CERT trusted_cert;
const UCHAR trusted_cert_der = { … };

/* Cryptography routines and crypto work buffers. */
extern const NX_SECURE_TLS_CRYPTO nx_crypto_tls_ciphers;
UCHAR crypto_metadata[9000];

/* Packet reassembly buffer for decryption. */
UCHAR packet_buffer[4000];

/* Remote certificate buffer for incoming certificates. */
#define REMOTE_CERT_SIZE (sizeof(NX_SECURE_X509_CERT) + 2000)
#define REMOTE_CERT_NUMBER  (3)
UCHAR remote_certs_buffer[REMOTE_CERT_SIZE * REMOTE_CERT_NUMBER];

/* Application thread where TLS session is started. */
void application_thread()
{
    NXD_ADDRESS server_ip;

    /* Create a TLS session for our socket. Ciphers and metadata defined
    elsewhere. See nx_secure_tls_session_create reference for more
    information. */
    status =  nx_secure_dtls_session_create(&client_dtls_session,
                                        &nx_crypto_tls_ciphers,
                                        crypto_metadata,
                                        sizeof(crypto_metadata),
                                        packet_buffer,
                                        sizeof(packet_buffer),
                                        REMOTE_CERT_NUMBER,
                                        remote_certs_buffer,
                                        sizeof(remote_certs_buffer));

    /* Check for error.  */
    if(status)
    {
        printf("Error in function nx_secure_dtls_session_create: 0x%x\n", status);
    }

    /* Initialize our trusted certificate. See section “Importing X.509
            Certificates into NetX Secure” for more information. */
        nx_secure_x509_certificate_initialize(&trusted_certificate,
                                    trusted_cert_der,
                                    trusted_cert_der_len, NX_NULL,
                                    0, NX_NULL, 0,
                                    NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add the certificate to the local store using a numeric ID. */
    nx_secure_dtls_session_trusted_certificate_add(&client_dtls_session,
                                                        &certificate, 1);

    /* Set up IP address of remote host. */
    server_ip.nxd_ip_version = NX_IP_VERSION_V4;
    server_ip.nxd_ip_address.v4 = IP_ADDRESS(192, 168, 1, 150);


    /* Now we can start the DTLS session as normal. */
    status =  nx_secure_dtls_client_session_start(&client_dtls_session,
                                        &udp_socket, &server_ip, 4443,
                                        NX_IP_PERIODIC_RATE);

    if(status != NX_SUCCESS)
    {
        /* Error! */
        return(status);
    }

    /* Add data to send packet as usual for NX_PACKET and send to server.  */
    status = nx_secure_dtls_session_send(&client_dtls_session,
                                                &send_packet,
                                                &server_ip, 4443);

    /* Receive response from server. */
        status = nx_secure_dtls_session_receive(&client_dtls_session,
                                                    &receive_packet,
                                                    NX_IP_PERIODIC_RATE);

    /* Process response. */

    /* Shut down DTLS session. */
    status = nx_secure_dtls_session_end(&client_dtls_session,
                                        NX_IP_PERIODIC_RATE);

    /* Clean up. */
    status = nx_secure_dtls_session_delete(&client_dtls_session);

    }

```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_dtls_client_session_start, nx_secure_dtls_session_receive,
- nx_secure_dtls_session_send, nx_secure_dtls_session_delete

## <a name="nx_secure_dtls_session_local_certificate_add"></a>nx_secure_dtls_session_local_certificate_add

NetX güvenli DTLS oturumuna yerel kimlik sertifikası ekleme

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_dtls_session_local_certificate_add(
                            NX_SECURE_DTLS_SESSION *session_ptr,
                            NX_SECURE_X509_CERT *certificate,
                            UINT cert_id);

```

### <a name="description"></a>Açıklama

Bu hizmet bir DTLS oturum örneğine yerel kimlik sertifikası ekler. Genel olarak, bu hizmet bir DTLS Istemci oturumunun bir uzak sunucu konağına kimlik sertifikası sağlaması gerektiğinde kullanılacaktır. Bu, DTLS için isteğe bağlı bir yapılandırmadır. bu nedenle, DTLS Istemcileri için genellikle bir sertifika gerekli değildir. Kimlik sertifikası, ilişkili bir özel anahtar gerektirir.

Cert_id parametresi, sertifika için sayısal, sıfır olmayan bir tanıtıcıdır. Bu, DTLS sertifika deposunda aynı X. 509.440 ortak adına sahip birden çok kimlik sertifikası bulunan olayda kolayca kaldırılmasını veya bu durumda bulunabilmesini sağlar. X. 509.440 sertifikaları hakkında daha fazla bilgi için NetX güvenli TLS Kullanıcı Kılavuzu 'na bakın.

### <a name="parameters"></a>Parametreler

- **session_ptr** Daha önce oluşturulmuş bir DTLS oturum örneğine yönelik işaretçi.
- **sertifika** Daha önce başlatılmış bir X. 509.440 sertifika yapısına yönelik işaretçi.
- **cert_id** Bu DTLS sunucusunda bu sertifika için sıfır olmayan sayısal benzersiz tanımlayıcı.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) DTLS oturumunun sertifikasının başarılı bir şekilde eklenmesi.
- **NX_PTR_ERROR** (0x07) geçersiz işaretçi geçirildi.
- **NX_INVALID_PARAMETERS** (0x4D) BIR sertifika kimliği (0) geçirildi.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

* Daha kapsamlı bir örnek için bkz. *nx_secure_dtls_session_create* başvurusu.

```C
/* Our DTLS Server instance. */
NX_SECURE_DTLS_SESSION dtls_client;

/* Certificate control block and data. Identity
certificates require a private key. */
NX_SECURE_X509_CERT certificate;
UCHAR certificate_der_data[] = { … };
UCHAR certificate_key_der_data[] = { … };


/* Application thread where TLS session is started. */
void application_thread()
{
NXD_ADDRESS server_ip;

/* Create a TLS session for our socket. Ciphers and metadata defined
   elsewhere. See nx_secure_tls_session_create reference for more
   information. */
    status =  nx_secure_dtls_session_create(&client_dtls_session,
                                        &nx_crypto_tls_ciphers,
                                        crypto_metadata,
                                        sizeof(crypto_metadata),
                                        packet_buffer,
                                        sizeof(packet_buffer),
                                        REMOTE_CERT_NUMBER,
                                        remote_certs_buffer,
                                        sizeof(remote_certs_buffer));

    /* Check for error.  */
    if(status)
{
    printf("Error in function nx_secure_dtls_session_create: 0x%x\n", status);
}

/* Initialize our trusted certificate. See section “Importing X.509
   Certificates into NetX Secure” for more information. */
    nx_secure_x509_certificate_initialize(&trusted_certificate,
                                    trusted_cert_der,
                                    trusted_cert_der_len,
                                    NX_NULL, 0, NX_NULL, 0,
                                    NX_SECURE_X509_KEY_TYPE_NONE);

/* Add the certificate to the local store using a numeric ID. */
    nx_secure_dtls_session_trusted_certificate_add(&client_dtls_session,
                                                              &certificate, 1);

    /* Initialize local server identity certificate with key and
    add to server. */
    status = nx_secure_x509_certificate_initialize(&certificate,
                        certificate_der_data,
                        sizeof(certificate_der_data),
                        NX_NULL, 0,
                        certificate_key_der_data,
                        sizeof(certificate_key_der_data),
                        NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_session_local_certificate_add(&dtls_client,
                                                    &certificate, 1);

/* Set up IP address of remote host. */
server_ip.nxd_ip_version = NX_IP_VERSION_V4;
server_ip.nxd_ip_address.v4 = IP_ADDRESS(192, 168, 1, 150);


/* Now we can start the DTLS session as normal. */
status =  nx_secure_dtls_client_session_start(&client_dtls_session,
                                    &udp_socket, &server_ip, 4443,
                                    NX_IP_PERIODIC_RATE);


    /* Process responses, etc…*/
}

```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_dtls_session_create, nx_secure_dtls_session_receive,
- nx_secure_dtls_session_send, nx_secure_dtls_session_start,
- nx_secure_dtls_session_local_certificate_remove,
- nx_secure_x509_certificate_initialize

## <a name="nx_secure_dtls_session_local_certificate_remove"></a>nx_secure_dtls_session_local_certificate_remove

NetX güvenli DTLS oturumundan yerel kimlik sertifikasını kaldırma

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_dtls_session_local_certificate_remove(
                                         NX_SECURE_DTLS_SESSION *session_ptr,
                                         UCHAR *common_name,
                                         UINT common_name_length, UINT cert_id);

```

### <a name="description"></a>Açıklama

Bu hizmet, bir sertifika KIMLIĞI numarası (sertifika nx_secure_dtls_session_local_certificate_add ile eklendiğinde atanır) veya X. 509.440 CommonName alanı kullanarak bir DTLS oturum örneğinden yerel kimlik sertifikasını kaldırır.

Common_name sertifikayla eşleştirmek için kullanılırsa, cert_id parametresi 0 olarak ayarlanmalıdır. Cert_id kullanılırsa, common_name NX_NULL bir değer geçirmelidir.

Cert_id parametresi, sertifika için sayısal, sıfır olmayan bir tanıtıcıdır. Bu, DTLS sertifika deposunda aynı X. 509.440 ortak adına sahip birden çok kimlik sertifikası bulunan olayda kolayca kaldırılmasını veya bu durumda bulunabilmesini sağlar. X. 509.440 sertifikaları hakkında daha fazla bilgi için NetX güvenli TLS Kullanıcı Kılavuzu 'na bakın.

### <a name="parameters"></a>Parametreler

- **session_ptr** Daha önce oluşturulmuş bir DTLS oturum örneğine yönelik işaretçi.
- **common_name** Eşleştirilecek CommonName dizesinin işaretçisi.
- **common_name_length** Common_name dizesinin uzunluğu.
- **cert_id** Bu DTLS sunucusunda bu sertifika için sıfır olmayan sayısal benzersiz tanımlayıcı.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) DTLS oturumundan sertifika başarıyla silindi.
- **NX_PTR_ERROR** (0x07) geçersiz işaretçi geçirildi.
- **NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) VERILEN DTLS oturumunda cert_id veya common_name eşleşen bir sertifika bulunamadı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

* Daha kapsamlı bir örnek için bkz. *nx_secure_dtls_session_create* başvurusu.

```C

/* Our DTLS Server instance. */
NX_SECURE_DTLS_SESSION dtls_client;

/* Certificate control block and data.
Identity certificates require a private key. */
NX_SECURE_X509_CERT certificate;
UCHAR certificate_der_data[] = { … };
UCHAR certificate_key_der_data[] = { … };


/* Application thread where TLS session is started. */
void application_thread()
{
    NXD_ADDRESS server_ip;

    /* Create a TLS session for our socket. Ciphers and metadata defined
    elsewhere. See nx_secure_tls_session_create reference for more
    information. */
        status =  nx_secure_dtls_session_create(&client_dtls_session,
                                            &nx_crypto_tls_ciphers,
                                            crypto_metadata,
                                            sizeof(crypto_metadata),
                                            packet_buffer,
                                            sizeof(packet_buffer),
                                            REMOTE_CERT_NUMBER,
                                            remote_certs_buffer,
                                            sizeof(remote_certs_buffer));

    /* Check for error.  */
    if(status)
    {
        printf("Error in function nx_secure_dtls_session_create: 0x%x\n", status);
    }

    /* Initialize our trusted certificate. See section “Importing X.509
    Certificates into NetX Secure” for more information. */
        nx_secure_x509_certificate_initialize(&trusted_certificate,
                                    trusted_cert_der,
                                    trusted_cert_der_len, NX_NULL,
                                    0, NX_NULL, 0,
                                    NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add the certificate to the local store using a numeric ID. */
        nx_secure_dtls_session_trusted_certificate_add(&client_dtls_session,
                                                            &certificate, 1);

        /* Initialize local server identity certificate with key
        and add to server. */
        status = nx_secure_x509_certificate_initialize(&certificate,
                                certificate_der_data,
                                sizeof(certificate_der_data),
                                NX_NULL, 0,
                                certificate_key_der_data,
                                sizeof(certificate_key_der_data),
                                NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

        /* Add local server identity certificate to DTLS server with ID of 1. */
        status = nx_secure_dtls_session_local_certificate_add(&dtls_client,
                                                            &certificate, 1);

    /* Set up IP address of remote host. */
    server_ip.nxd_ip_version = NX_IP_VERSION_V4;
    server_ip.nxd_ip_address.v4 = IP_ADDRESS(192, 168, 1, 150);


    /* Now we can start the DTLS session as normal. */
    status =  nx_secure_dtls_client_session_start(&client_dtls_session,
        &udp_socket, &server_ip, 4443,
        NX_IP_PERIODIC_RATE);

        /* Process responses, etc…*/

    /* At some point in the future,
    we decide to remove the certificate using the ID of 1
    when it was added to the session. */
        status = nx_secure_dtls_session_local_certificate_remove(&client_dtls_session,
                                                                NX_NULL, 0, 1);
}

```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_dtls_session_create, nx_secure_dtls_session_receive,
- nx_secure_dtls_session_send, nx_secure_dtls_session_start,
- nx_secure_dtls_session_local_certificate_add,
- nx_secure_x509_certificate_initialize

## <a name="nx_secure_dtls_session_receive"></a>nx_secure_dtls_session_receive

Belirlenen bir NetX güvenli DTLS oturumu üzerinden uygulama verileri alma

### <a name="prototype"></a>Prototype

```C
UINT nx_secure_dtls_session_receive(
                                NX_SECURE_DTLS_SESSION *dtls_session,
                                NX_PACKET **packet_ptr_ptr,
                                UINT wait_option);

```

### <a name="description"></a>Açıklama

Bu hizmet, etkin bir DTLS oturumu tarafından alınan uygulama verilerini döndürür. DTLS oturumu bir DTLS sunucu oturumu (bir DTLS sunucu örneğiyle yönetilen) ya da DTLS Istemci oturumu olabilir. Döndürülen paket, NX_PACKET API hizmetlerinden herhangi biri kullanılarak işlenebilir (daha fazla bilgi için bkz. NetX belgeleri).

### <a name="parameters"></a>Parametreler

- **dtls_session** Daha önce başlatılmış olan DTLS oturum yapısına yönelik işaretçi.
- **packet_ptr_ptr** Dönüş paketi için NX_PACKET işaretçisine yönelik işaretçi.
- **wait_option** Ağ işlemleri için kullanılacak ThreadX bekleme değeri.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) uygulama veri paketinin başarılı bir şekilde alındı.
- **NX_PTR_ERROR** (0x07) geçersiz oturum veya paket işaretçisi.
- **NX_NOT_ENABLED** (0x14) UDP etkin değil.
- **NX_NOT_BOUND** (0x24) UDP yuvası bağlantı noktasına bağlanmadı.
- **NX_SECURE_TLS_INVALID_PACKET** (0x104) geçerli bir DTLS kaydı olmayan veri alındı.
- **NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0x108) DTLS kaydı düzgün bir şekilde karıştırılıp (şifreleme hatası) başarısız oldu.
- **NX_SECURE_TLS_PADDING_CHECK_FAILED** (0x12a) şifreleme doldurma denetimi hatası.
- **NX_SECURE_TLS_ALERT_RECEIVED** (0x114) uzak ana bilgisayardan bir uyarı alındı.
- **NX_SECURE_TLS_UNRECOGNIZED_MESSAGE_TYPE**    (0x102) tanınmayan bir ileti aldı.
- **NX_SECURE_TLS_INCORRECT_MESSAGE_LENGTH** (0x10a), geçersiz uzunluğa sahıp bır DTLS kaydı alındı.
- **NX_SECURE_TLS_UNKNOWN_CIPHERSUITE** (0x105) bilinmeyen bir ciphersuite ile karşılaşıldı (iç şifreleme hatasını gösterir).
- **NX_SECURE_TLS_PROTOCOL_VERSION_CHANGED** (0x12e) eşleşmeyen DTLS sürümüne sahıp bır DTLS kaydı alındı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Sockets, sessions, certificates defined in global static space to preserve
   application stack. */
NX_SECURE_DTLS_SESSION client_dtls_session;

/* Trusted certificate structure and raw data. */
NX_SECURE_X509_CERT trusted_cert;
const UCHAR trusted_cert_der = { … };

/* Cryptography routines and crypto work buffers. */
extern const NX_SECURE_TLS_CRYPTO nx_crypto_tls_ciphers;
UCHAR crypto_metadata[9000];

/* Packet reassembly buffer for decryption. */
UCHAR packet_buffer[4000];

/* Remote certificate buffer for incoming certificates. */
#define REMOTE_CERT_SIZE (sizeof(NX_SECURE_X509_CERT) + 2000)
#define REMOTE_CERT_NUMBER  (3)
UCHAR remote_certs_buffer[REMOTE_CERT_SIZE * REMOTE_CERT_NUMBER];

/* Application thread where TLS session is started. */
void application_thread()
{
    NXD_ADDRESS server_ip;

    /* Create a TLS session for our socket. Ciphers and metadata defined
    elsewhere. See nx_secure_tls_session_create reference for more
    information. */
    status =  nx_secure_dtls_session_create(&client_dtls_session,
                                        &nx_crypto_tls_ciphers,
                                        crypto_metadata,
                                        sizeof(crypto_metadata),
                                        packet_buffer,
                                        sizeof(packet_buffer),
                                        REMOTE_CERT_NUMBER,
                                        remote_certs_buffer,
                                        sizeof(remote_certs_buffer));

    /* Check for error.  */
    if(status)
    {
    printf("Error in function nx_secure_dtls_session_create: 0x%x\n", status);
    }

    /* Initialize our trusted certificate. See section “Importing X.509
            Certificates into NetX Secure” for more information. */
        nx_secure_x509_certificate_initialize(&trusted_certificate,
                                    trusted_cert_der,
                                    trusted_cert_der_len, NX_NULL,
                                    0, NX_NULL, 0,
                                    NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add the certificate to the local store using a numeric ID. */
    nx_secure_dtls_session_trusted_certificate_add(&client_dtls_session,
                                                        &certificate, 1);

    /* Set up IP address of remote host. */
    server_ip.nxd_ip_version = NX_IP_VERSION_V4;
    server_ip.nxd_ip_address.v4 = IP_ADDRESS(192, 168, 1, 150);


    /* Now we can start the DTLS session as normal. */
    status =  nx_secure_dtls_client_session_start(&client_dtls_session,
                                        &udp_socket, &server_ip, 4443,
                                        NX_IP_PERIODIC_RATE);

    if(status != NX_SUCCESS)
    {
        /* Error! */
        return(status);
    }

    /* Add data to send packet as usual for NX_PACKET and send to server.  */
    status = nx_secure_dtls_session_send(&client_dtls_session, &send_packet,
                                                        &server_ip, 4443);

    /* Receive response from server. */
    status = nx_secure_dtls_session_receive(&client_dtls_session, &receive_packet,
                                                            NX_IP_PERIODIC_RATE);

    /* Process response. */

    /* Shut down DTLS session. */
    status = nx_secure_dtls_session_end(&client_dtls_session, NX_IP_PERIODIC_RATE);

    /* Clean up. */
    status = nx_secure_dtls_session_delete(&client_dtls_session);

}

```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_dtls_client_session_start, nx_secure_dtls_session_end,
- nx_secure_dtls_session_send, nx_secure_dtls_session_delete

## <a name="nx_secure_dtls_session_reset"></a>nx_secure_dtls_session_reset

NetX güvenli DTLS oturum örneğindeki verileri temizleme

### <a name="prototype"></a>Prototype

```C
UINT nx_secure_dtls_session_reset(NX_SECURE_DTLS_SESSION *dtls_session);
```

### <a name="description"></a>Açıklama

Bu hizmet, bir DTLS oturumunu sıfırlar, tüm kısa ömürlü şifreleme verilerini temizleyerek yapının yeni bir oturum için yeniden kullanılmasına izin verir. Kalıcı veriler (örn. sertifika depoları) korunur, böylece nx_secure_dtls_session_create tekrar tekrar çağrılmamalıdır.

### <a name="parameters"></a>Parametreler

- **dtls_session** Daha önce başlatılmış olan DTLS oturum yapısına yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı oturum sıfırlama.
- **NX_PTR_ERROR** (0x07) geçersiz oturum veya arabellek işaretçisi.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Sockets, sessions, certificates defined in global static space to preserve
   application stack. */
NX_SECURE_DTLS_SESSION client_dtls_session;

/* Trusted certificate structure and raw data. */
NX_SECURE_X509_CERT trusted_cert;
const UCHAR trusted_cert_der = { … };

/* Cryptography routines and crypto work buffers. */
extern const NX_SECURE_TLS_CRYPTO nx_crypto_tls_ciphers;
UCHAR crypto_metadata[9000];

/* Packet reassembly buffer for decryption. */
UCHAR packet_buffer[4000];

/* Remote certificate buffer for incoming certificates. */
#define REMOTE_CERT_SIZE (sizeof(NX_SECURE_X509_CERT) + 2000)
#define REMOTE_CERT_NUMBER  (3)
UCHAR remote_certs_buffer[REMOTE_CERT_SIZE * REMOTE_CERT_NUMBER];

/* Application thread where TLS session is started. */
void application_thread()
{
    NXD_ADDRESS server_ip;

    /* Create a TLS session for our socket. Ciphers and metadata defined
    elsewhere. See nx_secure_tls_session_create reference for more
    information. */
    status =  nx_secure_dtls_session_create(&client_dtls_session,
                                        &nx_crypto_tls_ciphers,
                                        crypto_metadata,
                                        sizeof(crypto_metadata),
                                        packet_buffer,
                                        sizeof(packet_buffer),
                                        REMOTE_CERT_NUMBER,
                                        remote_certs_buffer,
                                        sizeof(remote_certs_buffer));

    /* Check for error.  */
    if(status)
    {
    printf("Error in function nx_secure_dtls_session_create: 0x%x\n", status);
    }

    /* Initialize our trusted certificate. See section “Importing X.509
            Certificates into NetX Secure” for more information. */
        nx_secure_x509_certificate_initialize(&trusted_certificate,
                                    trusted_cert_der,
                                    trusted_cert_der_len, NX_NULL,
                                    0, NX_NULL, 0,
                                    NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add the certificate to the local store using a numeric ID. */
    nx_secure_dtls_session_trusted_certificate_add(&client_dtls_session,
                                                        &certificate, 1);

    /* Set up IP address of remote host. */
    server_ip.nxd_ip_version = NX_IP_VERSION_V4;
    server_ip.nxd_ip_address.v4 = IP_ADDRESS(192, 168, 1, 150);


    /* Now we can start the DTLS session as normal. */
    status =  nx_secure_dtls_client_session_start(&client_dtls_session,
                                        &udp_socket, &server_ip, 4443,
                                        NX_IP_PERIODIC_RATE);

    if(status != NX_SUCCESS)
    {
        /* Error! */
        return(status);
    }

    /* Add data to send packet as usual for NX_PACKET and send to server.  */
    status = nx_secure_dtls_session_send(&client_dtls_session, &send_packet,
                                                        &server_ip, 4443);

    /* Receive response from server. */
        status = nx_secure_dtls_session_receive(&client_dtls_session,
                                                    &receive_packet,
                                                    NX_IP_PERIODIC_RATE);

    /* Process response. */

    /* Shut down DTLS session. */
    status = nx_secure_dtls_session_reset(&client_dtls_session);

    /* A new session can now be started using the same structure. */
    status =  nx_secure_dtls_client_session_start(&client_dtls_session,



    /* Clean up. */
    status = nx_secure_dtls_session_delete(&client_dtls_session);

}

```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_dtls_client_session_start, nx_secure_dtls_session_receive,
- nx_secure_dtls_session_send, nx_secure_dtls_session_delete

## <a name="nx_secure_dtls_-session_send"></a>nx_secure_dtls_ session_send

Bir DTLS oturumu üzerinden veri gönderme

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_dtls_session_send(NX_SECURE_DTLS_SESSION *session_ptr,
                                          NX_PACKET *packet_ptr,
                                          NXD_ADDRESS *ip_address, UINT port);

```

### <a name="description"></a>Açıklama

Bu hizmet, belirlenen bir DTLS oturumu üzerinden, belirtilen IP adresi ve bağlantı noktasındaki uzak DTLS ana bilgisayarına bir veri paketi gönderir. Kullanılan oturum, etkin bir DTLS Istemci oturumundur. IP adresi ve bağlantı noktasının durum bilgisiz doğası nedeniyle sağlandığını, ancak genellikle nx_secure_dtls_session_start oturumu başlatmak için kullanılan adresle ve bağlantı noktasıyla eşleşmesi gerektiğini unutmayın.

Pakette belirtilen veriler, *nx_secure_dtls_packet_allocate* kullanılarak ayrılması gereken DTLS oturum şifreleme parametreleri ve yordamları kullanılarak şifrelenir ve ardından DTLS oturumunun UDP yuvası üzerinden uzak konağa gönderilir.

### <a name="parameters"></a>Parametreler

- **session_ptr** Etkin bir DTLS istemci oturumu örneği işaretçisi.
- **packet_ptr** Daha önce ayrılan ve uygulama verileriyle doldurulmuş bir NX_PACKET örneğine yönelik işaretçi.
- **ip_address** Uzak konağın IP adresini içeren NXD_ADDRESS yapısına yönelik işaretçi.
- **bağlantı noktası** Uzak konaktaki UDP bağlantı noktası.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) paketin başarıyla gönderilmesi.
- **NX_PTR_ERROR** (0x07) geçersiz işaretçi geçirildi.
- **NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) temel alınan UDP gönderme işleminde bir hata oluştu.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Sockets, sessions, certificates defined in global static space to preserve
   application stack. */
NX_SECURE_DTLS_SESSION client_dtls_session;

/* Trusted certificate structure and raw data. */
NX_SECURE_X509_CERT trusted_cert;
const UCHAR trusted_cert_der = { … };

/* Cryptography routines and crypto work buffers. */
extern const NX_SECURE_TLS_CRYPTO nx_crypto_tls_ciphers;
UCHAR crypto_metadata[9000];

/* Packet reassembly buffer for decryption. */
UCHAR packet_buffer[4000];

/* Remote certificate buffer for incoming certificates. */
#define REMOTE_CERT_SIZE (sizeof(NX_SECURE_X509_CERT) + 2000)
#define REMOTE_CERT_NUMBER  (3)
UCHAR remote_certs_buffer[REMOTE_CERT_SIZE * REMOTE_CERT_NUMBER];

/* Application thread where TLS session is started. */
void application_thread()
{
    NXD_ADDRESS server_ip;

    /* Create a TLS session for our socket. Ciphers and metadata defined
    elsewhere. See nx_secure_tls_session_create reference for more
    information. */
        status =  nx_secure_dtls_session_create(&client_dtls_session,
                                            &nx_crypto_tls_ciphers,
                                            crypto_metadata,
                                            sizeof(crypto_metadata),
                                            packet_buffer,
                                            sizeof(packet_buffer),
                                            REMOTE_CERT_NUMBER,
                                            remote_certs_buffer,
                                            sizeof(remote_certs_buffer));

    /* Check for error.  */
    if(status)
    {
        printf("Error in function nx_secure_dtls_session_create: 0x%x\n", status);
    }

    /* Initialize our trusted certificate. See section “Importing X.509
    Certificates into NetX Secure” for more information. */
        nx_secure_x509_certificate_initialize(&trusted_certificate,
                                    trusted_cert_der,
                                    trusted_cert_der_len, NX_NULL,
                                    0, NX_NULL, 0,
                                    NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add the certificate to the local store using a numeric ID. */
    nx_secure_dtls_session_trusted_certificate_add(&client_dtls_session,
                                                        &certificate, 1);

    /* Set up IP address of remote host. */
    server_ip.nxd_ip_version = NX_IP_VERSION_V4;
    server_ip.nxd_ip_address.v4 = IP_ADDRESS(192, 168, 1, 150);


    /* Now we can start the DTLS session as normal. */
    status =  nx_secure_dtls_client_session_start(&client_dtls_session,
                                        &udp_socket, &server_ip, 4443,
                                        NX_IP_PERIODIC_RATE);

    if(status != NX_SUCCESS)
    {
    /* Error! */
    return(status);
    }

    /* Add data to send packet as usual for NX_PACKET and send to server.  */
    status = nx_secure_dtls_session_send(&client_dtls_session, &send_packet,
                                                        &server_ip, 4443);

        /* Receive response from server. */
        status = nx_secure_dtls_session_receive(&client_dtls_session,
                                                    &receive_packet,
                                                    NX_IP_PERIODIC_RATE);

    /* Process response. */

    /* Shut down DTLS session. */
        status = nx_secure_dtls_session_end(&client_dtls_session,
                                            NX_IP_PERIODIC_RATE);

    /* Clean up. */
        status = nx_secure_dtls_session_delete(&client_dtls_session);

}

```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_dtls_client_session_start, nx_secure_dtls_session_receive,
- nx_secure_dtls_session_create

## <a name="nx_secure_dtls_session_trusted_certificate_add"></a>nx_secure_dtls_session_trusted_certificate_add

NetX güvenli DTLS oturumuna güvenilir bir CA sertifikası ekleme

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_dtls_session_trusted_certificate_add(
                                         NX_SECURE_DTLS_SESSION *session_ptr,
                                         NX_SECURE_X509_CERT *certificate,
                                         UINT cert_id);

```

### <a name="description"></a>Açıklama

Bu hizmet, bir DTLS oturum örneğine güvenilir bir CA veya ara CA X. 509.440 sertifikası ekler. Alternatif bir kimlik doğrulama mekanizması kullanılmamışsa (ör. önceden paylaşılan anahtarlar), uzak sunucu sertifikalarını doğrulamak için bir DTLS Istemcisi en az bir güvenilen sertifika gerektirir. Güvenilen bir sertifika genellikle özel bir anahtara sahip değildir.

Cert_id parametresi, sertifika için sayısal, sıfır olmayan bir tanıtıcıdır. Bu, DTLS sertifika deposunda aynı X. 509.440 ortak adına sahip birden çok kimlik sertifikası bulunan olayda kolayca kaldırılmasını veya bu durumda bulunabilmesini sağlar. X. 509.440 sertifikaları hakkında daha fazla bilgi için NetX güvenli TLS Kullanıcı Kılavuzu 'na bakın.

### <a name="parameters"></a>Parametreler

- **session_ptr** Daha önce oluşturulmuş bir DTLS oturum örneğine yönelik işaretçi.
- **sertifika** Daha önce başlatılmış bir X. 509.440 sertifika yapısına yönelik işaretçi.
- **cert_id** Bu DTLS sunucusunda bu sertifika için sıfır olmayan sayısal benzersiz tanımlayıcı.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) DTLS oturumunun sertifikasının başarılı bir şekilde eklenmesi.
- **NX_PTR_ERROR** (0x07) geçersiz işaretçi geçirildi.
- **NX_INVALID_PARAMETERS** (0x4D) BIR sertifika kimliği (0) geçirildi.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

* Daha kapsamlı bir örnek için bkz. *nx_secure_dtls_session_create* başvurusu.

```C
/* Our DTLS Server instance. */
NX_SECURE_DTLS_SESSION dtls_client;

/* Certificate control block and data.
Identity certificates require a private key. */
NX_SECURE_X509_CERT certificate;
UCHAR certificate_der_data[] = { … };
UCHAR certificate_key_der_data[] = { … };


/* Application thread where TLS session is started. */
void application_thread()
{
NXD_ADDRESS server_ip;

    /* Create a TLS session for our socket. Ciphers and metadata defined
       elsewhere. See nx_secure_tls_session_create reference for more
       information. */
    status =  nx_secure_dtls_session_create(&client_dtls_session,
                                            &nx_crypto_tls_ciphers,
                                            crypto_metadata,
                                            sizeof(crypto_metadata),
                                            packet_buffer,
                                            sizeof(packet_buffer),
                                            REMOTE_CERT_NUMBER,
                                            remote_certs_buffer,
                                            sizeof(remote_certs_buffer));

    /* Check for error.  */
    if(status)
    {
        printf("Error in function nx_secure_dtls_session_create: 0x%x\n", status);
    }

    /* Initialize our trusted certificate. See section “Importing X.509
   Certificates into NetX Secure” for more information. */
    nx_secure_x509_certificate_initialize(&trusted_certificate,
                                            trusted_cert_der,
                                            trusted_cert_der_len,
                                            NX_NULL, 0, NX_NULL, 0,
                                            NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add the certificate to the trusted store using a numeric ID. */
    nx_secure_dtls_session_trusted_certificate_add(&client_dtls_session,
                                                      &certificate, 1);

    /* Initialize local server identity certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&certificate,
                                            certificate_der_data,
                                            sizeof(certificate_der_data),
                                            NX_NULL, 0,
                                            certificate_key_der_data,
                                            sizeof(certificate_key_der_data),
                                            NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_session_local_certificate_add(&dtls_client,
                                                        &certificate, 1);

    /* Set up IP address of remote host. */
    server_ip.nxd_ip_version = NX_IP_VERSION_V4;
    server_ip.nxd_ip_address.v4 = IP_ADDRESS(192, 168, 1, 150);

    /* Now we can start the DTLS session as normal. */
    status =  nx_secure_dtls_client_session_start(&client_dtls_session,
         &udp_socket, &server_ip, 4443,
         NX_IP_PERIODIC_RATE);


    /* Process responses, etc…*/
}

```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_dtls_session_create, nx_secure_dtls_session_receive,
- nx_secure_dtls_session_send, nx_secure_dtls_session_start,
- nx_secure_dtls_session_trusted_certificate_remove,
- nx_secure_x509_certificate_initialize

## <a name="nx_secure_dtls_session_trusted_certificate_remove"></a>nx_secure_dtls_session_trusted_certificate_remove

NetX güvenli DTLS oturumundan güvenilir bir CA sertifikasını kaldırma

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_dtls_session_trusted_certificate_remove(
                            NX_SECURE_DTLS_SESSION *session_ptr,
                            UCHAR *common_name,
                            UINT common_name_length, UINT cert_id);

```

### <a name="description"></a>Açıklama

Bu hizmet, bir sertifika KIMLIĞI numarası (sertifika nx_secure_dtls_session_trusted_certificate_add ile eklendiğinde atanır) veya X. 509.440 CommonName alanı kullanarak bir DTLS oturum örneğinden güvenilir bir CA sertifikasını kaldırır.

Common_name sertifikayla eşleştirmek için kullanılırsa, cert_id parametresi 0 olarak ayarlanmalıdır. Cert_id kullanılırsa, common_name NX_NULL bir değer geçirmelidir.

Cert_id parametresi, sertifika için sayısal, sıfır olmayan bir tanıtıcıdır. Bu, DTLS sertifika deposunda aynı X. 509.440 ortak adına sahip birden çok kimlik sertifikası bulunan olayda kolayca kaldırılmasını veya bu durumda bulunabilmesini sağlar. X. 509.440 sertifikaları hakkında daha fazla bilgi için NetX güvenli TLS Kullanıcı Kılavuzu 'na bakın.

### <a name="parameters"></a>Parametreler

- **session_ptr** Daha önce oluşturulmuş bir DTLS oturum örneğine yönelik işaretçi.
- **common_name** Eşleştirilecek CommonName dizesinin işaretçisi.
- **common_name_length** Common_name dizesinin uzunluğu.
- **cert_id** Bu DTLS sunucusunda bu sertifika için sıfır olmayan sayısal benzersiz tanımlayıcı.


### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) DTLS oturumundan sertifika başarıyla silindi.
- **NX_PTR_ERROR** (0x07) geçersiz işaretçi geçirildi.
- **NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) VERILEN DTLS oturumunda cert_id veya common_name eşleşen bir sertifika bulunamadı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

* Daha kapsamlı bir örnek için bkz. *nx_secure_dtls_session_create* başvurusu.

```C
/* Our DTLS Server instance. */
NX_SECURE_DTLS_SESSION dtls_client;

/* Certificate control block and data. Identity certificates require a private key. */
NX_SECURE_X509_CERT certificate;
UCHAR certificate_der_data[] = { … };
UCHAR certificate_key_der_data[] = { … };


/* Application thread where TLS session is started. */
void application_thread()
{
    NXD_ADDRESS server_ip;

    /* Create a TLS session for our socket. Ciphers and metadata defined
    elsewhere. See nx_secure_tls_session_create reference for more
    information. */
        status =  nx_secure_dtls_session_create(&client_dtls_session,
                                            &nx_crypto_tls_ciphers,
                                            crypto_metadata,
                                            sizeof(crypto_metadata),
                                            packet_buffer,
                                            sizeof(packet_buffer),
                                            REMOTE_CERT_NUMBER,
                                            remote_certs_buffer,
                                            sizeof(remote_certs_buffer));

    /* Check for error.  */
    if(status)
    {
        printf("Error in function nx_secure_dtls_session_create: 0x%x\n", status);
    }

    /* Initialize our trusted certificate. See section “Importing X.509
    Certificates into NetX Secure” for more information. */
        nx_secure_x509_certificate_initialize(&trusted_certificate,
                                    trusted_cert_der,
                                    trusted_cert_der_len, NX_NULL, 0,
                                    NX_NULL, 0,
                                    NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add the certificate to the local store using a numeric ID. */
        nx_secure_dtls_session_trusted_certificate_add(&client_dtls_session,
                                                            &certificate, 1);

    /* Initialize local server identity certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&certificate,
                                            certificate_der_data,
                                            sizeof(certificate_der_data),
                                            NX_NULL, 0,
                                            certificate_key_der_data,
                                            sizeof(certificate_key_der_data),
                                            NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_session_local_certificate_add(&dtls_client,
                                                        &certificate, 1);

    /* Set up IP address of remote host. */
    server_ip.nxd_ip_version = NX_IP_VERSION_V4;
    server_ip.nxd_ip_address.v4 = IP_ADDRESS(192, 168, 1, 150);


    /* Now we can start the DTLS session as normal. */
    status =  nx_secure_dtls_client_session_start(&client_dtls_session,
                                        &udp_socket, &server_ip, 4443,
                                        NX_IP_PERIODIC_RATE);

    /* Process responses, etc…*/

    /* At some point in the future,
    we decide to remove the certificate using the ID of 1
    when it was added to the session. */
    status = nx_secure_dtls_session_trusted_certificate_remove(&client_dtls_session,
                                                                    NX_NULL, 0, 1);
}

```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_secure_dtls_session_create, nx_secure_dtls_session_receive,
- nx_secure_dtls_session_send, nx_secure_dtls_session_start,
- nx_secure_dtls_session_trusted_certificate_add,
- nx_secure_x509_certificate_initialize
