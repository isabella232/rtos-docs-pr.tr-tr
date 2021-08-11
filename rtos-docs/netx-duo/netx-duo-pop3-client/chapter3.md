---
title: Bölüm 3 - POP3 İstemci hizmetlerinin açıklaması
description: Bu bölümde, tüm NetX Duo POP3 İstemci hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 07/09/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: c8608f3894eba4db557f0c67b1042f2c88362cb0ca4bf6034bff9ae591fe26bc
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116797186"
---
# <a name="chapter-3---description-of-pop3-client-services"></a>Bölüm 3 - POP3 İstemci Hizmetlerinin Açıklaması

Bu bölümde, tüm NetX Duo POP3 İstemci hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklaması yer almaktadır.

> [!NOTE]
> Aşağıdaki API açıklamalarında yer alan "Dönüş Değerleri" bölümünde, **KALıN**  olmayan değerler tamamen devre dışı bırakılırken, BOLD NX_DISABLE_ERROR_CHECKING API hata denetimlerini devre dışı bırakmak için kullanılan tanımdan etkilenmez.

## <a name="nx_pop3_client_create"></a>nx_pop3_client_create

IPv4 için POP3 İstemci örneği oluşturma

### <a name="prototype"></a>Prototype

```C
UINT nx_pop3_client_create(NX_POP3_CLIENT *client_ptr,
    UINT APOP_authentication, NX_IP *ip_ptr,
    NX_PACKET_POOL *packet_pool_ptr,
    ULONG server_ip_address, ULONG server_port,
    CHAR *client_name, CHAR *client_password);
```

### <a name="description"></a>Description

Bu hizmet POP3 İstemcisi'nin bir örneğini oluşturur. Yalnızca IPv4 POP3 sunucu adreslerini destekler.

Cihaz uygulamasının önce POP3 İstemcisi'nin paketleri iletmesi için bir IP örneği ve paket havuzu oluşturması gerektiğini unutmayın. Özel olarak POP3 İstemci görevi veya IP örneği oluşturmada kullanılan aynı paket havuzu tarafından kullanım için oluşturulan bu paket havuzu. Paket havuzu, Ethernet sürücü paket havuzuyla da paylaşılıyor olabilir, ancak bu, yükü POP3 İstemcisi'nin sunucuya görece küçük POP3 ileti paketleri göndermesi için potansiyel olarak büyük paket yükü almaya yönelik büyük paket havuzlarını kullanmanın dezavantajıdır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** Oluşturulan İstemci İşaretçisi
- **APOP_authentication** APOP kimlik doğrulamasını etkinleştirme
- **ip_ptr IP** örneğine işaretçi
- **packet_pool_ptr** İstemci paket havuzu işaretçisi
- **server_ip_address** POP3 sunucusu IPv4 adresi
- **server_port** POP3 sunucu bağlantı noktası
- **client_name** İstemci adı işaretçisi
- **client_password** İstemci parolası işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) İstemcisi başarıyla oluşturuldu
- **durum** NetX Duo ve ThreadX hizmet çağrılarının durum tamamlaması
- NX_PTR_ERROR (0x07) Geçersiz giriş işaretçisi parametresi
- NX_POP3_PARAM_ERROR (0xB1) İşaretçi olmayan giriş geçersiz

### <a name="allowed-from"></a>İzin Verilen

Uygulama kodu

### <a name="example"></a>Örnek

```C
/* Create the POP3 Client. Note that the Client uses its password for its APOP shared
    secret. */

/* Set up user defined callback services. */
/* Create username and password for our POP3 Client mail drop. */
#define LOCALHOST "recipient@expresslogic.com"
#define LOCALHOST_PASSWORD "pass"
#define POP3_SERVER_ADDRESS IP_ADDRESS(192,2,2,92)
#define POP3_SERVER_PORT 110

/* Create a NetX POP3 Client instance. */
status = nx_pop3_client_create(&demo_client,
    NX_FALSE /* disable APOP authentication */,
    &client_ip, &client_packet_pool,
    POP3_SERVER_ADDRESS, POP3_SERVER_PORT,
    LOCALHOST, LOCALHOST_PASSWORD);

/* If the Client was successfully created, status = NX_SUCCESS. */
```

## <a name="nxd_pop3_client_create"></a>nxd_pop3_client_create

IPv4 veya IPv6 için POP3 İstemci örneği oluşturma

### <a name="prototype"></a>Prototype

```C
UINT nxd_pop3_client_create(NX_POP3_CLIENT *client_ptr,
    UINT APOP_authentication, NX_IP *ip_ptr,
    NX_PACKET_POOL *packet_pool_ptr,
    NXD_ADDRESS *server_ip_address,
    ULONG server_port,
    CHAR *client_name, CHAR *client_password);
```

### <a name="description"></a>Description

Bu hizmet POP3 İstemcisi'nin bir örneğini oluşturur. Hem IPv4 hem de IPv6 POP3 sunucu adreslerini destekler. POP3 İstemcisi *oluşturma nx_pop3_client_create* daha fazla ayrıntı için daha önce açıklanan hizmet hizmet bilgilerine bakın.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** Oluşturulan İstemci İşaretçisi
- **APOP_authentication** APOP kimlik doğrulamasını etkinleştirme
- **ip_ptr** IP örneğine işaretçi
- **packet_pool_ptr** İstemci paket havuzu işaretçisi
- **server_ip_address** POP3 sunucusu IPv6 veya IPv4 adresi
- **server_port** POP3 sunucu bağlantı noktası
- **client_name**  İstemci adı işaretçisi
- **client_password** İstemci parolası işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) İstemcisi başarıyla oluşturuldu
- **durum** NetX Duo ve ThreadX hizmet çağrılarının durum tamamlaması
- NX_PTR_ERROR (0x07) Geçersiz giriş işaretçisi parametresi
- NX_POP3_PARAM_ERROR (0xB1) İşaretçi olmayan giriş geçersiz

### <a name="allowed-from"></a>İzin Verilen

Uygulama kodu

### <a name="example"></a>Örnek

```C
/* Create the POP3 Client. */

/* Create username and password for our POP3 Client mail drop. */
#define LOCALHOST "recipient@expresslogic.com"
#define LOCALHOST_PASSWORD "pass"
#define POP3_SERVER_PORT 110

/* Create a NetX POP3 Client instance. Also note the details of IPv6 address validation
    and enabling IPv6 and ICMPv6 services on the IP task are not shown here. See the
    NetX Duo User Guide for more details on this process.
*/
NXD_ADDRESS server_ip_address;

/* Set client IP interface address. */
server_ip_address.nxd_ip_version = NX_IP_VERSION_V6;
server_ip_address.nxd_ip_address.v6[0] = 0x20010db8;
server_ip_address.nxd_ip_address.v6[1] = 0xf101;
server_ip_address.nxd_ip_address.v6[2] = 0;
server_ip_address.nxd_ip_address.v6[3] = 0x101;
status = nxd_pop3_client_create(&demo_client,
    NX_FALSE /* disable APOP authentication */,
    &client_ip, &client_packet_pool,
    &server_ip_address, POP3_SERVER_PORT,
    LOCALHOST, LOCALHOST_PASSWORD);

/* If the Client was successfully created, status = NX_SUCCESS. */
```

## <a name="nx_pop3_client_delete"></a>nx_pop3_client_delete

POP3 İstemci örneğini silme

### <a name="prototype"></a>Prototype

```C
UINT nx_pop3_client_delete(NX_POP3_CLIENT *client_ptr);
```

### <a name="description"></a>Description

Bu hizmet, daha önce oluşturulmuş bir POP3 İstemcisini siler. Bu hizmet POP3 İstemci paket havuzunu silemez. Cihaz uygulaması, paket havuzu için artık kullanamaysa bu kaynağı ayrı ayrı silmelidir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** Silinecek İstemci işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) İstemcisi başarıyla silindi
- NX_PTR_ERROR (0x07) Geçersiz giriş işaretçisi parametresi

### <a name="allowed-from"></a>İzin Verilen

Uygulama kodu

### <a name="example"></a>Örnek

```C
/* Delete the POP3 Client. */
status = nx_pop3_client_delete (&demo_client);

/* If the Client was successfully deleted, status = NX_SUCCESS. */
```

## <a name="nx_pop3_client_mail_item_delete"></a>nx_pop3_client_mail_item_delete

İstemci posta planından belirtilen posta öğesini silme

### <a name="prototype"></a>Prototype

```C
UINT nx_pop3_client_mail_items_delete(NX_POP3_CLIENT *client_ptr,
    UINT mail_index);
```

### <a name="description"></a>Description

Bu hizmet, belirtilen posta öğesini İstemci posta planından siler. Bazı POP3 sunucuları İstemci tarafından istendikten sonra posta öğelerini otomatik olarak silese de, posta öğesi indirdikten sonra için tasarlanmıştır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** İstemci örneğine işaretçi
- **mail_index** İstemci maildrop'a dizin oluşturma

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Silme isteği başarılı
- **NX_POP3_INVALID_MAIL_ITEM**(0xB2) Geçersiz posta öğesi dizini
- **NX_POP3_INSUFFICIENT_PACKET_PAYLOAD**(0xB6) İstemci paketi yükü POP3 isteği için çok küçük.
- **NX_POP3_SERVER_ERROR_STATUS**(0xB4) Sunucu hata durumuyla yanıt verir
- NX_POP3_CLIENT_INVALID_INDEX(0xB8) Geçersiz posta dizini girişi
- NX_PTR_ERROR (0x07) Geçersiz giriş işaretçisi parametresi

### <a name="allowed-from"></a>İzin Verilen

Uygulama kodu

### <a name="example"></a>Örnek

```C
ULONG item_index;

/* Delete the POP3 Client mail item. */
status = nx_pop3_client_mail_item_delete(&demo_client, item_index);

/* If the server accepts the DELE request (and deletes the mail item), status =
    NX_SUCCESS. */
```

## <a name="nx_pop3_client_mail_item_get"></a>nx_pop3_client_mail_item_get

Belirtilen posta öğesini alma

### <a name="prototype"></a>Prototype

```C
UINT nx_pop3_client_mail_item_get(NX_POP3_CLIENT *client_ptr,
    UINT mail_item, ULONG *item_size);
```

### <a name="description"></a>Description

Bu hizmet, dizin öğesi tarafından belirtilen İstemci posta öğesinden bir posta öğesi almak için bir RETR isteği mail_item. ReTR isteği gönderdikten ve Sunucu'dan olumlu yanıt aldıktan sonra İstemci, nx_pop3_client_mail_item_message_get hizmetini kullanarak *posta iletisini indirmeye* başlayabilir. Hizmetin Sunucu yanıttan ayıklanan istenen posta öğesinin boyutunu da sağlar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** İstemci örneğine işaretçi
- **mail_item** İstemci maildrop'a dizin oluşturma
- **item_size** Posta iletisinin boyutunu gösteren işaretçi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Posta öğesi başarıyla alındı
- **NX_POP3_INVALID_MAIL_ITEM** (0xB2) Geçersiz posta öğesi dizini
- **NX_POP3_INSUFFICIENT_PACKET_PAYLOAD** (0xB6) İstemci paketi yükü POP3 isteği için çok küçük.
- **NX_POP3_SERVER_ERROR_STATUS** (0xB4) Sunucu hata durumuyla yanıt verir
- NX_POP3_CLIENT_INVALID_INDEX (0xB8) Geçersiz posta dizini girişi
- NX_PTR_ERROR (0x07) Geçersiz giriş işaretçisi parametresi

### <a name="allowed-from"></a>İzin Verilen

Uygulama kodu

### <a name="example"></a>Örnek

```C
ULONG item_size;

/* Retrieve the POP3 Client mail item. */
status = nx_pop3_client_mail_item_get (&demo_client, 1, &item_size);

/* If the mail item was successfully obtained, status = NX_SUCCESS. */
```

## <a name="nx_pop3_client_mail_items_get"></a>nx_pop3_client_mail_items_get

Maildrop'ta posta öğelerinin sayısını alma

### <a name="prototype"></a>Prototype

```C
UINT nx_pop3_client_mail_items_get(NX_POP3_CLIENT *client_ptr,
    UINT *number_mail_items,
    ULONG *maildrop_total_size);
```

### <a name="description"></a>Description

Bu hizmet, İstemci postası'dan posta öğelerinin sayısını ve posta iletisi verisi toplam boyutunu almak için bir STAT isteği yapar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** İstemci örneğine işaretçi
- **number_mail_item** İstemci postası'nın posta sayısı
- **maildrop_total_size** Tüm posta iletisinin boyutunu gösteren işaretçi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Posta öğesi başarıyla alındı
- **NX_POP3_INVALID_MAIL_ITEM** (0xB2) Geçersiz posta öğesi dizini
- **NX_POP3_INSUFFICIENT_PACKET_PAYLOAD** (0xB6) İstemci paketi yükü POP3 isteği için çok küçük.
- **NX_POP3_SERVER_ERROR_STATUS** (0xB4) Sunucu hata durumuyla yanıt verir
- NX_PTR_ERROR (0x07) Geçersiz giriş işaretçisi parametresi

### <a name="allowed-from"></a>İzin Verilen

Uygulama kodu

### <a name="example"></a>Örnek

```C
UINT number_mail_items;

ULONG maildrop_total_size;

/* Retrieve the size and number of items in POP3 Client maildrop. */

status = nx_pop3_client_mail_item_get (&demo_client, 1, &number_mail_items,
    &maildrop_total_size);

/* If the maildrop data was successfully obtained, status = NX_SUCCESS. */
```

## <a name="nx_pop3_client_mail_item_message_get"></a>nx_pop3_client_mail_item_message_get

Belirtilen posta öğesi iletisini alma

### <a name="prototype"></a>Prototype

```C
UINT nx_pop3_client_mail_item_message_get(
    NX_POP3_CLIENT *client_ptr,
    NX_PACKET **recv_packet_ptr,
    ULONG *bytes_retrieved,
    UINT *final_packet);
```

### <a name="description"></a>Description

Bu hizmet posta öğesi iletisini, posta iletisinin boyutunu ve posta iletisinde son paketse alır. Bu final_packet, NX_TRUE tarafından işaret recv_packet_ptr posta öğesi iletisinde son pakettir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** İstemci örneğine işaretçi
- **recv_packet_ptr** İleti verileri paketi alındı
- **number_mail_item** İstemci postası'nın posta sayısı
- **maildrop_total_size** Tüm posta iletisinin boyutunu gösteren işaretçi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Posta öğesi başarıyla alındı
- **NX_POP3_CLIENT_INVALID_STATE** (0xB7) İstemci paketi yükü POP3 isteği için çok küçük.
- NX_PTR_ERROR (0x07) Geçersiz giriş işaretçisi parametresi

### <a name="allowed-from"></a>İzin Verilen

Uygulama kodu

### <a name="example"></a>Örnek

```C
NX_PACKET *recv_packet_ptr;

ULONG bytes_retrieved;

UINT final_packet;

/* Retrieve the size and number of items in POP3 Client maildrop. */

status = nx_pop3_client_mail_item_message_get (&demo_client, &recv_packet_ptr,
    bytes_retrieved, final_packet);

/* If the maildrop message packet was successfully obtained, status = NX_SUCCESS. */
```

## <a name="nx_pop3_client_mail_item_size_get"></a>nx_pop3_client_mail_item_size_get

Belirtilen posta öğesinin boyutunu alma

### <a name="prototype"></a>Prototype

```C
UINT nx_pop3_client_mail_item_size_get(
    NX_POP3_CLIENT *client_ptr,
    UINT mail_item, ULONG *size);
```

### <a name="description"></a>Description

Bu hizmet, belirtilen posta öğesinin boyutunu almak için bir LIST isteği yapar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** İstemci örneğine işaretçi
- **mail_item** İstemci maildrop'a dizin oluşturma
- **boyut** Posta iletisinin boyutunu gösteren işaretçi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Posta öğesi başarıyla alındı
- **NX_POP3_INVALID_MAIL_ITEM** (0xB2) Geçersiz posta öğesi dizini
- **NX_POP3_INSUFFICIENT_PACKET_PAYLOAD** (0xB6) İstemci paketi yükü POP3 isteği için çok küçük.
- **NX_POP3_SERVER_ERROR_STATUS** (0xB4) Sunucu hata durumuyla yanıt verir
- NX_POP3_CLIENT_INVALID_INDEX (0xB8) Geçersiz posta dizini girişi
- NX_PTR_ERROR (0x07) Geçersiz giriş işaretçisi parametresi

### <a name="allowed-from"></a>İzin Verilen

Uygulama kodu

### <a name="example"></a>Örnek

```C
ULONG size;

UINT mail_item;

/* Retrieve the size of the specified mail item in POP3 Client maildrop. */

status = nx_pop3_client_mail_item_size_get (&demo_client, mail_item, &size);

/* If the maildrop message packet was successfully obtained, status = NX_SUCCESS. */
```
