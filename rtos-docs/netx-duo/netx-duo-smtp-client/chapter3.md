---
title: Bölüm 3-SMTP Istemci hizmetlerinin Istemci açıklaması
description: Bu bölüm, tipik bir SMTP Istemci uygulamasında kullanım sırasına göre tüm NetX Duo SMTP Istemci hizmetlerinin (aşağıda listelenmiştir) açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 07/09/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: f590ba5a4c020b4a0aec6628a89c0e5f0f8579d9
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825787"
---
# <a name="chapter-3---client-description-of-smtp-client-services"></a>Bölüm 3-SMTP Istemci hizmetlerinin Istemci açıklaması

Bu bölüm, tipik bir SMTP Istemci uygulamasında kullanım sırasına göre tüm NetX Duo SMTP Istemci hizmetlerinin (aşağıda listelenmiştir) açıklamasını içerir.

> [!NOTE]
> Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **_NX_DISABLE_ERROR_CHECKING_** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.

## <a name="nxd_smtp_client_create"></a>nxd_smtp_client_create

SMTP Istemci örneği oluşturma

### <a name="prototype"></a>Prototype

```C
UINT nxd_smtp_client_create(NX_SMTP_CLIENT *client_ptr,
    NX_IP *ip_ptr, NX_PACKET_POOL
    *client_packet_pool_ptr,
    CHAR *username, CHAR *password,
    CHAR *from_address,
    CHAR *client_domain,
    UINT authentication_type, NXD_ADDRESS *server_address,
    UINT port);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen IP örneğinde bir SMTP Istemci örneği oluşturur.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** SMTP Istemci denetim bloğu işaretçisi;
- **ip_ptr** IP örneği işaretçisi;
- **packet_pool_ptr** Istemci paket havuzu işaretçisi;
- **Kullanıcı adı** Kimlik doğrulaması için NULL ile sonlandırılmış * * Kullanıcı adı
- **parola** Kimlik doğrulaması için NULL ile sonlandırılmış parola
- **from_address** NULL ile sonlandırılmış gönderenin adresi
- **client_domain** NULL ile sonlandırılmış etki alanı adı
- **authentication_type** İstemci kimlik doğrulaması türü. Desteklenen türler şunlardır:
  - NX_SMTP_CLIENT_AUTH_LOGIN
  - NX_SMTP_CLIENT_AUTH_PLAIN
  - NX_SMTP_CLIENT_AUTH_NONE
- **server_address** SMTP sunucusu IP adresi işaretçisi
- **SERVER_PORT** SMTP sunucusu TCP bağlantı noktası

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) SMTP istemcisi başarıyla oluşturuldu. TCP yuvası oluşturma durumu
- NX_SMTP_INVALID_PARAM (0xA5) geçersiz işaretçi girişi
- NX_IP_ADDRESS_ERROR (0x21) geçersiz IP adresi türü
- NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi

### <a name="allowed-from"></a>İzin verilen

Uygulama kodu

### <a name="example"></a>Örnek

```C
/* Create the SMTP Client instance. */
NX_PACKET_POOL client_packet_pool;
NX_IP client_ip;
NX_SMTP_CLIENT demo_client;

#define USERNAME “myusername”
#define PASSWORD “mypassword”
#define FROM_ADDRESS “<myname@mycompany.com>”
#define LOCAL_DOMAIN “mycompany.com”
#define SERVER_PORT 25

/* Define client authentication type as LOGIN. 
    If not specified or unknown the SMTP Client will set it to PLAIN. */
#define CLIENT_AUTHENTICATION_TYPE NX_SMTP_CLIENT_AUTH_LOGIN

NXD_ADDRESS server_ip_address;

#ifdef USE_IPV6
    /* Set up the Server IPv6 address. */
    server_ip_address.nxd_ip_version = NX_IP_VERSION_V6;
    server_ip_address.nxd_ip_address.v6[0] = 0x20010db8;
    server_ip_address.nxd_ip_address.v6[1] = 0xf101;
    server_ip_address.nxd_ip_address.v6[2] = 0;
    server_ip_address.nxd_ip_address.v6[3] = 0x106;
#else
    server_ip_address.nxd_ip_version = NX_IP_VERSION_V4;
    server_ip_address.nxd_ip_address.v4 = SERVER_IP_ADDRESS;
#endif

status = nxd_smtp_client_create(&demo_client, &client_ip, &client_packet_pool,
    USERNAME, PASSWORD, FROM_ADDRESS,
    LOCAL_DOMAIN, CLIENT_AUTHENTICATION_TYPE,
    &server_ip_address, SERVER_PORT);

/* If an SMTP Client instance was successfully created, status = NX_SUCCESS. */
```

## <a name="nx_smtp_client_delete"></a>nx_smtp_client_delete

SMTP Istemci örneğini silme

### <a name="prototype"></a>Prototype

```C
UINT nx_smtp_client_delete(NX_SMTP_CLIENT *client_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, önceden oluşturulmuş bir SMTP Istemci örneğini siler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** SMTP Istemci örneği işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) istemci başarıyla silindi
- NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Delete the SMTP Client instance “my_client.” */

NX_SMTP_CLIENT demo_client;

status = nx_smtp_client_delete(&demo_client);

/* If an SMTP Client instance was successfully deleted, status = NX_SUCCESS. */
```

## <a name="nx_smtp_mail_send"></a>nx_smtp_mail_send

SMTP posta öğesi oluşturma ve gönderme

### <a name="prototype"></a>Prototype

```C
UINT nx_smtp_mail_send(NX_SMTP_CLIENT *client_ptr,
    CHAR *recipient_address,
    UINT priority, CHAR *subject,
    CHAR *mail_body,
    UINT mail_body_length);
```

### <a name="description"></a>Açıklama

Bu hizmet bir SMTP posta öğesi oluşturur ve gönderir. SMTP Istemcisi SMTP sunucusuyla bir TCP bağlantısı kurar ve bir dizi SMTP komutu gönderir. Herhangi bir hatayla karşılaşılmaz, posta iletisini sunucuya iletir. Posta başarıyla gönderiliyorsa bağımsız olarak TCP bağlantısını sonlandırır ve posta aktarımının sonucunu gösteren bir durum döndürür. Uygulama, sınır olmadan gönderilmesi gereken çok sayıda posta iletisi için bu hizmeti çağırabilir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** SMTP Istemcisi işaretçisi
- **recipient_address** NULL ile sonlandırılmış alıcı adresi.
- **Konu** NULL ile sonlandırılmış konu satırı metni;.
- **Öncelik** Postanın teslim edileceği öncelik düzeyi
- **mail_body** Posta iletisi işaretçisi
- **mail_body_length** Posta iletisinin boyutu

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) posta başarıyla gönderildi
- SMTP oturumunun SMTP oturumu durumu sonucu için **NX_SMTP_CLIENT_NOT_INITIALIZED** (0xB2) SMTP istemci örneği başlatılmadı
- NX_PTR_ERROR (0x07) geçersiz işaretçi parametresi
- NX_SMTP_INVALID_PARAM (0xA5) geçersiz işaretçi girişi
- NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Create and send a Client mail item. */

#define RECIPIENT_ADDRESS “<your@yourcompany.com>”
#define SUBJECT “NetX Duo SMTP Client Demo”
#define MAIL_BODY "NetX Duo SMTP client is an SMTP client ” \
    “implementation for embedded devices \r\n” \
    "to send email to SMTP servers.\r\n"

status = nx_smtp_mail_send(&demo_client, RECIPIENT_ADDRESS,
    NX_SMTP_MAIL_PRIORITY_NORMAL,
    SUBJECT_LINE, MAIL_BODY,
    sizeof(MAIL_BODY) - 1);

/* Return status being NX_SUCCESS indicates the mail has been
    successfully sent. */
```
