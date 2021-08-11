---
title: Bölüm 4 - NetX Azure RTOS DTLS hizmetlerinin açıklaması
description: Bu bölümde, Tüm NetX Azure RTOS DTLS hizmetlerinin alfabetik sırada listelenmiş bir açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 45966e7c8ea9be18bf294e8a7540e7226e803f29ae4f3ad3faaa29e4939c2ed8
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116801860"
---
# <a name="chapter-4-description-of-azure-rtos-netx-secure-dtls-services"></a>Bölüm 4: NetX Azure RTOS DTLS hizmetlerinin açıklaması

Bu bölümde Tüm NetX Secure DTLS Azure RTOS (aşağıda listelenmiştir) alfabetik sırada bir açıklama yer almaktadır.

Aşağıdaki API açıklamalarında yer alan "Dönüş Değerleri" bölümünde, **KALıN**  olmayan değerler tamamen devre dışı bırakılırken, BOLD NX_SECURE_DISABLE_ERROR_CHECKING api hata denetimi devre dışı bırakmak için kullanılan NX_SECURE_DISABLE_ERROR_CHECKING makros undan etkilenmez.

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

NetX Güvenli DTLS İstemci Oturumu Başlatma

### <a name="prototype"></a>Prototype

```C
UINT nx_secure_dtls_client_session_start(
                        NX_SECURE_DTLS_SESSION *dtls_session,
                        NX_UDP_SOCKET *udp_socket,
                        NXD_ADDRESS *ip_address, UINT port,
                        UINT wait_option);

```

### <a name="description"></a>Description

Bu hizmet, ağ iletişimleri için sağlanan UDP yuvasını kullanarak sağlanan IP adresi ve UDP bağlantı noktası üzerinden sunucuya bağlanarak bir DTLS İstemci oturumu başlatır.

Bu hizmeti nx_secure_dtls_session_create kullanarak çağırmadan önce DTLS oturum nx_secure_dtls_session_create. Ayrıca, DTLS İstemcisi, oturuma en az bir güvenilen CA sertifikasının nx_secure_dtls_session_trusted_certificate_add veya Önceden Paylaşılan Anahtarlar'ın etkinleştirilmesini ve yapılandırılmasını gerektirir.

### <a name="parameters"></a>Parametreler

- **dtls_session** Daha önce başlatılan bir DTLS Oturumu yapısının işaretçisi.
- **udp_socket** Uzak DTLS sunucusuyla ağ iletişimleri kurmak için kullanılacak başlatılmış UDP yuvası.
- **ip_address** Uzak DTLS sunucusunun adresini içeren IP adresi yapısına işaretçi.
- **bağlantı noktası** Uzak DTLS sunucusuyla ağ iletişimleri kurmak için kullanılacak başlatılmış UDP yuvası.
- **wait_option** Bağlantı girişimi için askıya alma seçeneği.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Sertifikanın oturuma başarıyla ataması.
- **NX_NOT_CONNECTED** (0x38) Sunucuya verilen adres ve bağlantı noktası ile ulaşamaz.
- **NX_SECURE_TLS_UNRECOGNIZED_MESSAGE_TYPE** (0x102) Alınan TLS/DTLS ileti türü yanlış.
- **NX_SECURE_TLS_UNSUPPORTED_CIPHER** (0x106) Uzak konak tarafından sağlanan bir şifreleme desteklenmiyor.
- **NX_SECURE_TLS_HANDSHAKE_FAILURE** (0x107) TLS el sıkışması sırasında ileti işleme başarısız oldu.
- **NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0x108) Gelen ileti bir karma MAC denetimi başarısız oldu.
- **NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) Temel alınan bir TCP yuvası gönderme işlemi başarısız oldu.
- **NX_SECURE_TLS_INCORRECT_MESSAGE_LENGTH** (0x10A) Gelen iletinin uzunluk alanı geçersizdi.
- **NX_SECURE_TLS_BAD_CIPHERSPEC** (0x10B) Gelen bir ChangeCipherSpec iletisi yanlış.
- **NX_SECURE_TLS_INVALID_SERVER_CERT** (0x10C) Gelen TLS sertifikası, uzak DTLS sunucusunu tanımlamak için kullanılamaz.
- **NX_SECURE_TLS_UNSUPPORTED_PUBLIC_CIPHER** (0x10D) Uzak konak tarafından sağlanan ortak anahtar şifrelemesi desteklenmez.
- **NX_SECURE_TLS_NO_SUPPORTED_CIPHERS** (0x10E) Uzak konak NetX Secure DTLS yığını tarafından desteklenen şifreleme olmadığını belirtti.
- **NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0x10F) alınan bir DTLS iletisi üst bilgisinde bilinmeyen bir DTLS sürümüne sahipti.
- **NX_SECURE_TLS_UNSUPPORTED_TLS_VERSION** (0x110) alınan bir DTLS iletisi üst bilgisinde bilinen ancak desteklenmeyen bir DTLS sürümüne sahipti.
- **NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) bir iç TLS paket ayırması başarısız oldu.
- **NX_SECURE_TLS_INVALID_CERTIFICATE** (0x112) Uzak konak geçersiz bir sertifika sağladı.
- **NX_SECURE_TLS_ALERT_RECEIVED** (0x114) Uzak konak bir hata belirten bir uyarı gönderdi ve TLS oturumunu sonlandı.
- **NX_SECURE_TLS_MISSING_CRYPTO_ROUTINE** (0x13B) Şifreleme tablosuna bir giriş NULL işlev işaretçisine sahipti.
- **NX_PTR_ERROR** (0x07) Geçersiz oturum, yuva veya adres işaretçisi.

### <a name="allowed-from"></a>İzin Verilen

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

NetX Güvenli DTLS Oturumu için paket ayırma

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_dtls_packet_allocate(
                              NX_SECURE_DTLS_SESSION *session_ptr,
                         NX_PACKET_POOL *pool_ptr,
                         NX_PACKET **packet_ptr,
                              ULONG wait_option);

```

### <a name="description"></a>Description

Bu hizmet, belirtilen NX_PACKET DTLS oturumu için belirtilen oturumdan bir NX_PACKET_POOL. Bu hizmet, bir DTLS bağlantısı üzerinden gönderilecek veri paketlerini ayırmak için uygulama tarafından çağrılmalı. Bu hizmet çağrılmadan önce DTLS oturumunun başlatılması gerekir.

Paket verileri doldurulduğunda DTLS üst bilgisi ve alt bilgi verileri eklenebilmek için ayrılan paket düzgün bir şekilde başlatılır. Aksi takdirde davranış, ile *nx_packet_allocate.*

### <a name="parameters"></a>Parametreler

- **session_ptr** DTLS Oturumu örneğinin işaretçisi.
- **pool_ptr** Paketin ayrıl NX_PACKET_POOL bir uygulamanın işaretçisi.
- **packet_ptr** Yeni ayrılan paketin çıkış işaretçisi.
- **wait_option** Paket ayırma için askıya alma seçeneği.


### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı paket ayırma.
- **NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) Temel paket ayırma başarısız oldu.
- **NX_SECURE_TLS_SESSION_UNINITIALIZED** (0x101) Sağlanan DTLS oturumu başlatılmadı.

### <a name="allowed-from"></a>İzin Verilen

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

NetX Güvenli DTLS Oturumuna Önceden Paylaşılan Anahtar Ekleme

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_dtls_psk_add(NX_SECURE_DTLS_SESSION *session_ptr,
                            UCHAR *pre_shared_key, UINT psk_length,
                            UCHAR *psk_identity, UINT
                            identity_length, UCHAR *hint, UINT
                            hint_length);
```

### <a name="description"></a>Description

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

### <a name="description"></a>Description

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

### <a name="description"></a>Description

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

### <a name="description"></a>Description

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

### <a name="description"></a>Description

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

### <a name="description"></a>Description

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

### <a name="description"></a>Description

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

### <a name="description"></a>Description

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

### <a name="description"></a>Description

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

### <a name="description"></a>Description

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

### <a name="description"></a>Description

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

NetX Güvenli DTLS Sunucusuna güvenilen CA sertifikası ekleme

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_dtls_server_trusted_certificate_add(
                                         NX_SECURE_DTLS_SERVER *server_ptr,
                                         NX_SECURE_X509_CERT *certificate,
                                         UINT cert_id);

```

### <a name="description"></a>Description

Bu hizmet, bir DTLS Sunucusu örneğine güvenilir bir CA veya ara CA sertifikası ekler ve tüm iç DTLS sunucu oturumlarına atanır. Bu yalnızca X.509 İstemci sertifikası kimlik doğrulaması *nx_secure_dtls_server_x509_client_verify_configure.* Eklenen sertifika, gelen İstemci X.509 sertifikalarını doğrulamak için kullanılır.

Cert_id parametresi, sertifika için sıfır olmayan sayısal bir tanımlayıcıdır. Bu, DTLS sunucu depolamada aynı X.509 Ortak Adına sahip birden çok kimlik sertifikası olması durumunda sertifikanın kolayca kaldırılmasına veya bulunamasını sağlar. X.509 sunucu sertifikaları hakkında daha fazla bilgi için bkz. NetX Secure TLS Kullanıcı Kılavuzu.

### <a name="parameters"></a>Parametreler

- **server_ptr** Daha önce oluşturulmuş bir DTLS Sunucusu örneğinin işaretçisi.
- **sertifika** Daha önce başlatılan bir X.509 sertifika yapısının işaretçisi.
- **cert_id** Bu DTLS sunucusunda bu sertifika için sıfır olmayan sayısal benzersiz tanımlayıcı.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) DTLS sunucusuna başarılı bir şekilde sertifika ekleme.
- **NX_PTR_ERROR** (0x07) Geçersiz işaretçi geçirildi.
- **NX_INVALID_PARAMETERS** (0x4D) 0 sertifika kimliği geçirildi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

*Daha eksiksiz bir *nx_secure_dtls_server_create* için başvuruya bakın.

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

NetX Güvenli DTLS Sunucusundan güvenilen CA sertifikasını kaldırma

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_dtls_server_trusted_certificate_remove(
                                NX_SECURE_DTLS_SERVER *server_ptr,
                                UCHAR *common_name,
                                UINT common_name_length,
                                UINT cert_id);

```

### <a name="description"></a>Description

Bu hizmet, bir DTLS Sunucusu örneğinden güvenilen CA sertifikasını kaldırır. Güvenilen CA sertifikaları yalnızca X.509 İstemci sertifikası doğrulamasının nx_secure_dtls_server_x509_client_verify_configure çağrısıyla etkinleştirdiği bir DTLS *Sunucusu için* gereklidir.

Kaldırılacak sertifika, X.509 Ortak Adı ile veya cert_id çağrısında atanmış olan sayısal *nx_secure_dtls_server_trusted_certificate_add.* Bu cert_id yalnızca sertifikayı tanımlamak için kullanılır ve uygulama tarafından korunur. Sayısal sertifika tanımlayıcısı yerine Ortak Ad kullanılıyorsa, cert_id parametresi 0 olarak ayar olmalıdır.

> [!NOTE]
> DTLS el sıkışması işlenirken sertifikanın kaldırılması beklenmeyen davranışlara neden olabilir. Sertifikalar *nx_secure_dtls_server_stop* önce hizmetin çağrılsı gerekir.

### <a name="parameters"></a>Parametreler

- **server_ptr** Daha önce oluşturulmuş bir DTLS Sunucusu örneğinin işaretçisi.
- **common_name** Kaldırlanacak sertifikanın X.509 CommonName. Bu kullanılırsa, cert_id olarak geçiş.
- **common_name_length** Bayt cinsinden common_name dizenin uzunluğu.
- **cert_id** Bu DTLS sunucusunda bu sertifika için sıfır olmayan sayısal benzersiz tanımlayıcı. Bu kullanılırsa, NX_NULL parametresi için common_name geçiş.


### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) DTLS sunucusundan sertifika başarıyla kaldırıldı.
- **NX_PTR_ERROR** (0x07) Geçersiz işaretçi geçirildi.
- **NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) Verilen DTLS sunucusunda cert_id veya common_name eşleşen sertifika bulunamadı.

### <a name="allowed-from"></a>İzin Verilen

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

İstemci sertifikalarını talep etmek ve doğrulamak için NetX Secure DTLS Sunucusu yapılandırma

### <a name="prototype"></a>Prototype

```C
UINT nx_secure_dtls_server_x509_client_verify_configure(
                           NX_SECURE_DTLS_SERVER *server_ptr,
                               UINT certs_per_session,
                               UCHAR *certs_buffer, ULONG buffer_size);

```

### <a name="description"></a>Description

Bu hizmet, DTLS İstemci sertifikalarını talep etmek ve doğrulamak için bir DTLS Sunucusu yapılandırıyor. Bu isteğe bağlı özellik, diğer mekanizmalar (ör. Önceden Paylaşılan Anahtar) yerine istemci kimlik doğrulaması için X.509 sertifikaları istenebilir.

> [!IMPORTANT]
> *Bir DTLS Sunucusu bu hizmeti kullanarak istemci sertifikalarını doğrulamak üzere yapılandırıldığında, nx_secure_dtls_server_trusted_certificate_add kullanılarak sunucuya en az bir güvenilen CA sertifikası eklenmiştir; yoksa sunucu, istemci sertifikalarını güvenilir depoya karşı doğrulayamadığı için gelen tüm istemci bağlantılarını reddeder.*

Bu hizmeti çağıran DTLS Sunucusu örneği (başlatıldıktan sonra) DTLS el sıkışması kapsamında istemci sertifikaları isteği gönderir. İstemcinin bir kimlik sertifikasıyla (ve uygun olduğunda ilişkili sertifika zinciriyle) düzgün yapılandırıldığında, DTLS Sunucusu istemci sertifika verilerini işlemesi için bellek ayrılır. Bu bellek, certs_buffer *geçirildi.*

Bu certs_buffer DTLS istemcisinde beklenen en büyük sertifika zincirine uyum sağlayacak şekilde boyutlandırılacak şekilde, *DTLS sunucu oturumlarının sayısıyla aynı olacak şekilde boyutlandırılacaktır.* Arabellek, bir İstemci sertifika zincirinde *beklenen en certs_per_session* sertifika sayısını temsil eden certs_per_session parametresi kullanılarak kullanılabilir oturumlara bölündü. Arabelleğin, sertifika verilerini ayrıştırmak NX_SECURE_X509_CERT veri yapısı için de alan sağlaması gerekir.

Uygun arabellek boyutunun hesaplanması şu formülle yapılabilir:

```C
buffer_size = (# of DTLS sessions in server) *
                (certs_per_session) *
                (    maximum expected certificate size +
                      sizeof(NX_SECURE_X509_CERT)    )

```

- DTLS oturumlarının sayısı, oturum arabelleğine geçirilen oturum arabelleğinin boyutuna nx_secure_dtls_server_create.
- certs_per_session, herhangi bir istemci sertifika zincirinde beklenen en fazla sertifika sayısına ayar gerekir.
- Beklenen en büyük sertifika boyutu uygulamaya, anahtar boyutlarına ve diğer faktörlere bağlıdır, ancak genel olarak 2 KB yeterlidir.

### <a name="parameters"></a>Parametreler

- **server_ptr** Daha önce oluşturulmuş bir DTLS Sunucusu örneğinin işaretçisi.
- **certs_per_session** Her DTLS sunucu oturumuna ayrılacak sertifika sayısı.
- **certs_buffer** Gelen sertifika verileri için arabellek alanı.
- **buffer_size** Sertifika arabelleğinin boyutu.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) X.509 İstemci doğrulamasının başarılı yapılandırması.
- **NX_PTR_ERROR** (0x07) Geçersiz işaretçi geçirildi.
- **NX_INVALID_PARAMETERS** (0x4D) Geçersiz sertifika deposu (DTLSserver örneği yeni değil mi?).

### <a name="allowed-from"></a>İzin Verilen

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

NetX Secure DTLS Sunucusu için istemci X.509 sertifika doğrulamasını devre dışı bırakma

### <a name="prototype"></a>Prototype

```C
UINT nx_secure_dtls_server_x509_client_verify_disable(
                           NX_SECURE_DTLS_SERVER *server_ptr);
```

### <a name="description"></a>Description

Bu hizmet, bir DTLS Sunucusunda X.509 İstemci sertifikası doğrulamasını devre dışı bırakıyor. X.509 İstemci sertifikası doğrulaması etkinleştirilmediyse hizmetin hiçbir etkisi olmaz.

> [!NOTE]
> Etkin bir DTLS Sunucusu örneğinde istemci kimlik doğrulamasını devre dışı bırakmak öngörülemeyen bir davranışa neden olabilir. Sunucu nx_secure_dtls_server_stop önce hizmet çağrılır.

### <a name="parameters"></a>Parametreler

- **server_ptr** Daha önce oluşturulmuş bir DTLS Sunucusu örneğinin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) X.509 istemci kimlik doğrulamasının devre dışı bırakılması başarılı.
- **NX_PTR_ERROR** (0x07) Geçersiz işaretçi geçirildi.

### <a name="allowed-from"></a>İzin Verilen

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

DTLS Sunucusu oturumundan uzak istemci bilgilerini al

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_dtls_session_client_info_get(
                                    NX_SECURE_DTLS_SESSION *session_ptr,
                                    NXD_ADDRESS *client_ip_address,
                                    UINT *client_port, UINT *local_port);

```

### <a name="description"></a>Description

Bu hizmet, belirli bir DTLS Sunucusu oturumuna bağlı bir DTLS İstemcisi hakkında ağ bilgilerini döndürür. Döndürülen bilgiler uzak istemcinin IP adresini ve UDP bağlantı noktasının yanı sıra istemcinin bağlı olduğu yerel sunucu bağlantı noktasını içerir.

Genel olarak, DTLS oturum örneği DTLS bildirim geri çağırma yordamlarından birinin çağrılarak elde edilen örnektir (örneğin, connect_notify veya receive_notify geri çağırmaları nx_secure_dtls_server_create).

### <a name="parameters"></a>Parametreler

- **session_ptr** Etkin bir DTLS sunucusu oturum örneğinin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Sunucunun başarıyla silinmesi.
- **NX_PTR_ERROR** (0x07) Geçersiz işaretçi geçirildi.
- **NX_INVALID_SOCKET** (0x13) İlişkili UDP yuvası geçerli değil (oturum başlatılmadı?).
- **NX_NOT_CONNECTED** (0x38) UDP yuvası bağlı değil – istemci bağlantısı bırakıldı veya henüz kurulmadı.

### <a name="allowed-from"></a>İzin Verilen

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

NetX Güvenli DTLS Oturumu oluşturma ve yapılandırma

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

### <a name="description"></a>Description

Bu hizmet bir DTLS oturumu oluşturur ve yapılandırr. Genellikle, DTLS Sunucusu oturumları DTLS Sunucusu mekanizmasıyla yönetiliyorsa (bkz. *nx_secure_dtls_server_create)* DTLS İstemci oturumları oluşturmak için kullanılır, ancak bir uygulamanın tek bir tek başına DTLS Sunucusu oturum örneği oluşturması gereken örnekler olabilir ve bu durumda bu hizmet <sup>7</sup>kullanılabilir.

Parametreler, bir DTLS oturumunun örneğini almak için gereken bilgileri ve bellek ayırmayı yapılandırıyor. Bu crypto_table, TLS/DTLS şifrelemesi ve kimlik doğrulaması için gereken tüm şifreleme yordamlarını içeren bir TLS tablosudur. Şifreleme metadata_buffer şifrelemek için kullanılır (NetX Güvenli TLS Kullanıcı Kılavuzu'nx_secure_tls_metadata_size_calculate'da nx_secure_tls_metadata_size_calculate'a bakın) ve packet_reassembly_buffer, UDP veri birimlerini şifre çözme için eksiksiz bir DTLS kaydı olarak yeniden bir hale almak için kullanılır.

Gelen DTLS certs_number remote_certificate_buffer zincirini depolamak ve işlemesi için alana ihtiyaç olan DTLS İstemcileri için gerekli olan certs_number ve yapılandırma bilgileri gereklidir. Arabelleğin bağlanacağı herhangi bir sunucu için sertifika zincirinin beklenen en büyük boyutuna uygun olması gerekir. Arabellek, beklenen sertifika sayısına (certs_number parametresi) bölündü ve ayrıca sertifika başına bir sertifika yapısına sahip NX_SECURE_X509_CERT kadar büyük olmalıdır. Arabellek boyutu aşağıdaki formül kullanılarak belirlenebilirsiniz:

```C
remote_certificate_buffer_size = (certs_number) *
                 (maximum cert size + sizeof(NX_SECURE_X509_CERT))
```

- certs_number, sunucunun sertifika zincirinde beklenen en fazla sertifika sayısıdır
- En büyük sertifika boyutu kullanılan anahtarların boyutuna ve sertifikanın bilgilerine bağlıdır, ancak genel olarak 2 KB yeterlidir.

**7** Bu yordamla DTLS Sunucusu oturumlarının oluşturulması önerilmez ve bazı sınırlamalarla birlikte gelir. Birincil sorun, oturumun ek istemci bağlantılarını uygun şekilde işlemeyecek olmasıdır. UDP bağlantısız olduğu için ikinci bir istemci, önceki bir DTLS oturumu hala etkin olduğunda sunucunun UDP bağlantı noktasına yasal olarak veri gönderebilir ve bu da sunucu oturumunun bir hatayla bitimini sağlar.

### <a name="parameters"></a>Parametreler

- **dtls_session** Uninitialized DTLS Oturum yapısının işaretçisi.
- **crypto_table** Tüm şifreleme işlemleri için kullanılan TLS/DTLS şifreleme tablosu yapısının işaretçisi.
- **crypto_metadata_buffer** Şifreleme işlemi hesaplamaları ve durum bilgileri için arabellek alanı.
- **crypto_metadata_size** Meta veri arabelleğinin boyutu.
- **packet_reassembly_buffer** DTLS tarafından UDP verilerini şifre çözme için DTLS kayıtlarına yeniden bir arada olmak için kullanılan arabellek.
- **packet_reassembly_buffer_size** Yeniden değerlendirme arabelleğinin boyutu. Genellikle 16 KB'den büyük olmalı, ancak uygulamaya bağlı olarak daha küçük olabilir.
- **certs_number** Uzak sunucunun sertifika zincirinde beklenen en fazla sertifika sayısı.
- **remote_certificate_buffer** Gelen sertifika verileri için arabellek alanı.
- **remote_certificate_buffer_size** Sertifika arabelleğinin boyutu.


### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Oturumun başarıyla oluşturulması.
- **NX_PTR_ERROR** (0x07) Geçersiz oturum veya arabellek işaretçisi.
- **NX_INVALID_PARAMETERS** (0x4D) Paket yeniden değerlendirme, sertifikalar veya şifreleme için yeterli arabellek alanı yok.

### <a name="allowed-from"></a>İzin Verilen

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

- nx_secure_dtls_client_session_start,nx_secure_dtls_session_receive,
- nx_secure_dtls_session_send

## <a name="nx_secure_dtls_session_delete"></a>nx_secure_dtls_session_delete

NetX Secure DTLS Oturumu tarafından kullanılan kaynakları serbest bırak

### <a name="prototype"></a>Prototype

```C
UINT nx_secure_dtls_session_delete(
                        NX_SECURE_DTLS_SESSION *dtls_session);

```

### <a name="description"></a>Description

Bu hizmet bir DTLS oturumunu serek, oluşturulduğunda ayrılan tüm kaynakları serbest bırakarak.

### <a name="parameters"></a>Parametreler

- **dtls_session** Daha önce başlatılan bir DTLS Oturumu yapısının işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Oturum başarıyla silindi.
- **NX_PTR_ERROR** (0x07) Geçersiz oturum veya arabellek işaretçisi.

### <a name="allowed-from"></a>İzin Verilen

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

Etkin bir NetX Secure DTLS Oturumunu kapatma

### <a name="prototype"></a>Prototype

```C
UINT nx_secure_dtls_session_end(NX_SECURE_DTLS_SESSION *dtls_session,
                                UINT wait_option);

```

### <a name="description"></a>Description

Bu hizmet, uzak ana bilgisayara BIR TLS/DTLS CloseNotify uyarısı göndererek etkin bir DTLS oturumunu sonlar. Kullanılan IP adresi ve bağlantı noktası, önceki çağrıda kullanılan ip nx_secure_dtls_session_send.

### <a name="parameters"></a>Parametreler

- **dtls_session** Daha önce başlatılan bir DTLS Oturumu yapısının işaretçisi.
- **wait_option** Ağ işlemleri için kullanmak üzere ThreadX bekleme değeri.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Oturum başarıyla silindi.
- **NX_PTR_ERROR** (0x07) Geçersiz oturum veya arabellek işaretçisi.
- **NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) CloseNotify uyarısı için paket ayrılamadı.
- **NX_SECURE_TLS_UNKNOWN_CIPHERSUITE** (0x105) Büyük olasılıkla iç hata – şifreleme yordamı tanınmıyor.
- **NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) Temel UDP gönderme işlemi başarısız oldu.
- **NX_IP_ADDRESS_ERROR** ana 0x21 IP adresiyle ilgili hata .
- **NX_NOT_BOUND** (0x24) Temel ALıNAN UDP yuvası bağlantı noktasına bağlı değil.
- **NX_INVALID_PORT** (0x46) Geçersiz UDP bağlantı noktası.
- **NX_PORT_UNAVAILABLE** (0x23) UDP bağlantı noktası kullanılamaz.

### <a name="allowed-from"></a>İzin Verilen

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

NetX Secure DTLS Oturumuna yerel kimlik sertifikası ekleme

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_dtls_session_local_certificate_add(
                            NX_SECURE_DTLS_SESSION *session_ptr,
                            NX_SECURE_X509_CERT *certificate,
                            UINT cert_id);

```

### <a name="description"></a>Description

Bu hizmet bir DTLS Oturumu örneğine yerel kimlik sertifikası ekler. Genel olarak, bir DTLS İstemcisi oturumunun uzak sunucu ana bilgisayarına bir kimlik sertifikası sağlaması gerekirken bu hizmet kullanılır. Bu, DTLS için isteğe bağlı bir yapılandırmadır, bu nedenle DTLS İstemcileri için genellikle bir sertifika gerekmez. Kimlik sertifikası, ilişkili bir özel anahtar gerektirir.

Cert_id parametresi, sertifika için sıfır olmayan sayısal bir tanımlayıcıdır. Bu, DTLS sertifika depolamada aynı X.509 Ortak Adına sahip birden çok kimlik sertifikası olması durumunda sertifikanın kolayca kaldırılmasına veya bulunamasını sağlar. X.509 sertifikaları hakkında daha fazla bilgi için bkz. NetX Secure TLS Kullanıcı Kılavuzu.

### <a name="parameters"></a>Parametreler

- **session_ptr** Daha önce oluşturulmuş bir DTLS Oturumu örneğinin işaretçisi.
- **sertifika** Daha önce başlatılan bir X.509 sertifika yapısının işaretçisi.
- **cert_id** Bu DTLS sunucusunda bu sertifika için sıfır olmayan sayısal benzersiz tanımlayıcı.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) DTLS oturumuna başarılı bir şekilde sertifika ekleme.
- **NX_PTR_ERROR** (0x07) Geçersiz işaretçi geçirildi.
- **NX_INVALID_PARAMETERS** (0x4D) 0 sertifika kimliği geçirildi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

*Daha eksiksiz bir *nx_secure_dtls_session_create* için başvuruya bakın.

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

NetX Secure DTLS Oturumundan yerel kimlik sertifikasını kaldırma

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_dtls_session_local_certificate_remove(
                                         NX_SECURE_DTLS_SESSION *session_ptr,
                                         UCHAR *common_name,
                                         UINT common_name_length, UINT cert_id);

```

### <a name="description"></a>Description

Bu hizmet, bir sertifika kimliği numarası (sertifika nx_secure_dtls_session_local_certificate_add ile eklenmiştir) veya X.509 CommonName alanını kullanarak DTLS Oturumu örneğinden yerel kimlik sertifikasını kaldırır.

Sertifika common_name için kullanılacaksa, cert_id parametresi 0 olarak ayar olmalıdır. Bu cert_id, common_name değerine NX_NULL.

Cert_id parametresi, sertifika için sıfır olmayan sayısal bir tanımlayıcıdır. Bu, DTLS sertifika depolamada aynı X.509 Ortak Adına sahip birden çok kimlik sertifikası olması durumunda sertifikanın kolayca kaldırılmasına veya bulunamasını sağlar. X.509 sertifikaları hakkında daha fazla bilgi için bkz. NetX Secure TLS Kullanıcı Kılavuzu.

### <a name="parameters"></a>Parametreler

- **session_ptr** Daha önce oluşturulmuş bir DTLS Oturumu örneğinin işaretçisi.
- **common_name** Eşleşmek için CommonName dizesinin işaretçisi.
- **common_name_length** Dizenin common_name.
- **cert_id** Bu DTLS sunucusunda bu sertifika için sıfır olmayan sayısal benzersiz tanımlayıcı.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) DTLS oturumundan sertifika başarıyla kaldırıldı.
- **NX_PTR_ERROR** (0x07) Geçersiz işaretçi geçirildi.
- **NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) Verilen DTLS oturumunda cert_id veya common_name eşleşen sertifika bulunamadı.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

*Daha eksiksiz bir *nx_secure_dtls_session_create* için başvuruya bakın.

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

NetX Güvenli DTLS Oturumu üzerinden uygulama verilerini alma

### <a name="prototype"></a>Prototype

```C
UINT nx_secure_dtls_session_receive(
                                NX_SECURE_DTLS_SESSION *dtls_session,
                                NX_PACKET **packet_ptr_ptr,
                                UINT wait_option);

```

### <a name="description"></a>Description

Bu hizmet, etkin bir DTLS Oturumu tarafından alınan uygulama verilerini döndürür. DTLS Oturumu bir DTLS Sunucusu oturumu (DTLS Sunucusu örneği tarafından yönetilen) veya bir DTLS İstemci oturumu olabilir. Döndürülen paket, api hizmetlerinde herhangi bir NX_PACKET işlenebilir (daha fazla bilgi için NetX belgelerine bakın).

### <a name="parameters"></a>Parametreler

- **dtls_session** Daha önce başlatılan bir DTLS Oturumu yapısının işaretçisi.
- **packet_ptr_ptr** Dönüş paketi için NX_PACKET işaretçisi.
- **wait_option** Ağ işlemleri için kullanmak üzere ThreadX bekleme değeri.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Uygulama veri paketi başarıyla alındı.
- **NX_PTR_ERROR** (0x07) Geçersiz oturum veya paket işaretçisi.
- **NX_NOT_ENABLED** (0x14) UDP etkin değil.
- **NX_NOT_BOUND** (0x24) UDP yuvası bağlantı noktasına bağlı değil.
- **NX_SECURE_TLS_INVALID_PACKET** (0x104) geçerli bir DTLS kaydı olan verileri geri aldı.
- **NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0x108) DTLS kaydı düzgün karmalanamadı (şifreleme hatası).
- **NX_SECURE_TLS_PADDING_CHECK_FAILED** (0x12A) Şifreleme doldurma denetimi hatası.
- **NX_SECURE_TLS_ALERT_RECEIVED** (0x114) uzak konaktan bir uyarıyı geri aldı.
- **NX_SECURE_TLS_UNRECOGNIZED_MESSAGE_TYPE**    (0x102) Tanınmayan bir ileti aldı.
- **NX_SECURE_TLS_INCORRECT_MESSAGE_LENGTH** (0x10A) geçersiz uzunlukta bir DTLS kaydını geri aldı.
- **NX_SECURE_TLS_UNKNOWN_CIPHERSUITE** (0x105) Bilinmeyen bir şifrelemeyle karşılaşıldı (iç şifreleme hatası olduğunu gösterir).
- **NX_SECURE_TLS_PROTOCOL_VERSION_CHANGED** (0x12E) bir DTLS kaydını eşleşmeyen DTLS sürümüyle geri aldı.

### <a name="allowed-from"></a>İzin Verilen

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

NetX Secure DTLS Oturumu örneğinde verileri temizleme

### <a name="prototype"></a>Prototype

```C
UINT nx_secure_dtls_session_reset(NX_SECURE_DTLS_SESSION *dtls_session);
```

### <a name="description"></a>Description

Bu hizmet bir DTLS oturumunu sıfırlar, kısa ömürlü tüm şifreleme verilerini temizler ve yapının yeni bir oturum için yeniden kullanılmaktadır. Kalıcı veriler (örn. sertifika depoları) korunur, böylece nx_secure_dtls_session_create tekrar tekrar çağrılmaması gerekir.

### <a name="parameters"></a>Parametreler

- **dtls_session** Daha önce başlatılan bir DTLS Oturumu yapısının işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Oturumun başarıyla sıfırlanır.
- **NX_PTR_ERROR** (0x07) Geçersiz oturum veya arabellek işaretçisi.

### <a name="allowed-from"></a>İzin Verilen

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

DTLS oturumu üzerinden veri gönderme

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_dtls_session_send(NX_SECURE_DTLS_SESSION *session_ptr,
                                          NX_PACKET *packet_ptr,
                                          NXD_ADDRESS *ip_address, UINT port);

```

### <a name="description"></a>Description

Bu hizmet, verilen IP adresi ve bağlantı noktası üzerinden uzak bir DTLS ana bilgisayarına, kurulan bir DTLS Oturumu üzerinden bir veri paketi gönderir. Kullanılan oturum etkin bir DTLS İstemci oturumu. IP adresinin ve bağlantı noktasının UDP'nin durum bilgisiz yapısı nedeniyle sağlanmıştır, ancak genel olarak, udp'de oturumu başlatmak için kullanılan adres ve bağlantı noktasıyla nx_secure_dtls_session_start.

*nx_secure_dtls_packet_allocate* kullanılarak ayrılmış olması gereken pakette sağlanan veriler, DTLS oturum şifreleme parametreleri ve yordamları kullanılarak şifrelenir ve ardından DTLS Oturumunun UDP yuvası üzerinden uzak ana bilgisayara gönderilir.

### <a name="parameters"></a>Parametreler

- **session_ptr** Etkin bir DTLS istemci oturumu örneğinin işaretçisi.
- **packet_ptr** Daha önce ayrılmış NX_PACKET uygulama verileriyle doldurulmuş bir örnek işaretçisi.
- **ip_address** Uzak ana NXD_ADDRESS IP adresini içeren bir ana bilgisayar yapısına işaretçi.
- **bağlantı noktası** Uzak konakta UDP bağlantı noktası.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Paketin başarılı bir şekilde göndermesi.
- **NX_PTR_ERROR** (0x07) Geçersiz işaretçi geçirildi.
- **NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) Temel ALıNAN UDP gönderme işlemi sırasında bir hata oluştu.

### <a name="allowed-from"></a>İzin Verilen

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

NetX Güvenli DTLS Oturumuna güvenilen CA sertifikası ekleme

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_dtls_session_trusted_certificate_add(
                                         NX_SECURE_DTLS_SESSION *session_ptr,
                                         NX_SECURE_X509_CERT *certificate,
                                         UINT cert_id);

```

### <a name="description"></a>Description

Bu hizmet, bir DTLS Oturumu örneğine güvenilir bir CA veya ara CA X.509 sertifikası ekler. DTLS İstemcisi, alternatif bir kimlik doğrulama mekanizması kullanılmadıkça (ör. Önceden Paylaşılan Anahtarlar) uzak sunucu sertifikalarını doğrulamak için en az bir güvenilen sertifika gerektirir. Güvenilen sertifikanın genellikle özel anahtarı olmaz.

Cert_id parametresi, sertifika için sıfır olmayan sayısal bir tanımlayıcıdır. Bu, DTLS sertifika depolamada aynı X.509 Ortak Adına sahip birden çok kimlik sertifikası olması durumunda sertifikanın kolayca kaldırılmasına veya bulunamasını sağlar. X.509 sertifikaları hakkında daha fazla bilgi için bkz. NetX Secure TLS Kullanıcı Kılavuzu.

### <a name="parameters"></a>Parametreler

- **session_ptr** Daha önce oluşturulmuş bir DTLS Oturumu örneğinin işaretçisi.
- **sertifika** Daha önce başlatılan bir X.509 sertifika yapısının işaretçisi.
- **cert_id** Bu DTLS sunucusunda bu sertifika için sıfır olmayan sayısal benzersiz tanımlayıcı.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) DTLS oturumuna başarılı bir şekilde sertifika ekleme.
- **NX_PTR_ERROR** (0x07) Geçersiz işaretçi geçirildi.
- **NX_INVALID_PARAMETERS** (0x4D) 0 sertifika kimliği geçirildi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

*Daha eksiksiz bir *nx_secure_dtls_session_create* için başvuruya bakın.

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

NetX Güvenli DTLS Oturumundan güvenilen CA sertifikasını kaldırma

### <a name="prototype"></a>Prototype

```C
UINT  nx_secure_dtls_session_trusted_certificate_remove(
                            NX_SECURE_DTLS_SESSION *session_ptr,
                            UCHAR *common_name,
                            UINT common_name_length, UINT cert_id);

```

### <a name="description"></a>Description

Bu hizmet, bir sertifika kimliği numarası (sertifika nx_secure_dtls_session_trusted_certificate_add ile eklenmiştir) veya X.509 CommonName alanını kullanarak bir DTLS Oturumu örneğinden güvenilen CA sertifikasını kaldırır.

Sertifika common_name için kullanılacaksa, cert_id parametresi 0 olarak ayar olmalıdır. Bu cert_id, common_name değerine NX_NULL.

Cert_id parametresi, sertifika için sıfır olmayan sayısal bir tanımlayıcıdır. Bu, DTLS sertifika depolamada aynı X.509 Ortak Adına sahip birden çok kimlik sertifikası olması durumunda sertifikanın kolayca kaldırılmasına veya bulunamasını sağlar. X.509 sertifikaları hakkında daha fazla bilgi için bkz. NetX Secure TLS Kullanıcı Kılavuzu.

### <a name="parameters"></a>Parametreler

- **session_ptr** Daha önce oluşturulmuş bir DTLS Oturumu örneğinin işaretçisi.
- **common_name** Eşleşmek için CommonName dizesinin işaretçisi.
- **common_name_length** Dizenin common_name.
- **cert_id** Bu DTLS sunucusunda bu sertifika için sıfır olmayan sayısal benzersiz tanımlayıcı.


### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) DTLS oturumundan sertifika başarıyla kaldırıldı.
- **NX_PTR_ERROR** (0x07) Geçersiz işaretçi geçirildi.
- **NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) Verilen DTLS oturumunda cert_id veya common_name eşleşen sertifika bulunamadı.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

*Daha eksiksiz bir *nx_secure_dtls_session_create* için başvuruya bakın.

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
