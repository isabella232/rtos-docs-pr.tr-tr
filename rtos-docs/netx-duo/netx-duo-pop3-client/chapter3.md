---
title: Bölüm 3-POP3 Istemci hizmetlerinin açıklaması
description: Bu bölüm, tüm NetX Duo POP3 Istemci hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 07/09/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 1f7681c8f3fe161db8a37a82574ab7d5e9bf348e
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825841"
---
# <a name="chapter-3---description-of-pop3-client-services"></a>Bölüm 3-POP3 Istemci hizmetlerinin açıklaması

Bu bölüm, tüm NetX Duo POP3 Istemci hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.

> [!NOTE]
> Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_DISABLE_ERROR_CHECKING** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.

## <a name="nx_pop3_client_create"></a>nx_pop3_client_create

IPv4 için bir POP3 Istemci örneği oluşturma

### <a name="prototype"></a>Prototype

```C
UINT nx_pop3_client_create(NX_POP3_CLIENT *client_ptr,
    UINT APOP_authentication, NX_IP *ip_ptr,
    NX_PACKET_POOL *packet_pool_ptr,
    ULONG server_ip_address, ULONG server_port,
    CHAR *client_name, CHAR *client_password);
```

### <a name="description"></a>Açıklama

Bu hizmet, POP3 Istemcisinin bir örneğini oluşturur. Yalnızca IPv4 POP3 sunucu adreslerini destekler.

Cihaz uygulamasının, paketleri iletmek için POP3 Istemcisi için bir IP örneği ve bir paket havuzu oluşturması gerektiğini unutmayın. Bu paket havuzu, yalnızca POP3 Istemci görevi veya IP örneği oluşturmada kullanılan paket havuzu tarafından kullanılmak üzere oluşturulur. Paket havuzu, Ethernet sürücü paketi havuzuyla de paylaşılabilir, ancak bu, yükü, POP3 Istemcisinin sunucuya görece küçük ve büyük boyutlu paketler alması amaçlanan büyük paket havuzları kullanmanın dezavantajudur.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** Oluşturulacak Istemci işaretçisi
- **APOP_authentication** APOP kimlik doğrulamasını etkinleştir
- IP örneğine **Ip_ptr işaretçisi**
- **packet_pool_ptr** Istemci paket havuzu işaretçisi
- **server_ip_address** POP3 sunucusu IPv4 adresi
- **SERVER_PORT** POP3 sunucu bağlantı noktası
- **client_name** Istemci adı işaretçisi
- **client_password** Istemci parolası işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) istemci başarıyla oluşturuldu
- **durum** NetX Duo ve ThreadX hizmeti çağrılarının durum bitimi
- NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi
- NX_POP3_PARAM_ERROR (0xB1) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

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

IPv4 veya IPv6 için bir POP3 Istemci örneği oluşturma

### <a name="prototype"></a>Prototype

```C
UINT nxd_pop3_client_create(NX_POP3_CLIENT *client_ptr,
    UINT APOP_authentication, NX_IP *ip_ptr,
    NX_PACKET_POOL *packet_pool_ptr,
    NXD_ADDRESS *server_ip_address,
    ULONG server_port,
    CHAR *client_name, CHAR *client_password);
```

### <a name="description"></a>Açıklama

Bu hizmet, POP3 Istemcisinin bir örneğini oluşturur. Hem IPv4 hem de IPv6 POP3 sunucu adreslerini destekler. POP3 Istemcisi oluşturma işlemi hakkında daha fazla bilgi için daha önce açıklanan *nx_pop3_client_create* hizmetine bakın.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** Oluşturulacak Istemci işaretçisi
- **APOP_authentication** APOP kimlik doğrulamasını etkinleştir
- **ip_ptr** IP örneği işaretçisi
- **packet_pool_ptr** Istemci paket havuzu işaretçisi
- **server_ip_address** POP3 sunucusu IPv6 veya IPv4 adresi
- **SERVER_PORT** POP3 sunucu bağlantı noktası
- **client_name**  Istemci adı işaretçisi
- **client_password** Istemci parolası işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) istemci başarıyla oluşturuldu
- **durum** NetX Duo ve ThreadX hizmeti çağrılarının durum bitimi
- NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi
- NX_POP3_PARAM_ERROR (0xB1) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

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

POP3 Istemci örneğini silme

### <a name="prototype"></a>Prototype

```C
UINT nx_pop3_client_delete(NX_POP3_CLIENT *client_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet önceden oluşturulmuş bir POP3 Istemcisini siler. Bu hizmet POP3 Istemci paket havuzunu silmez. Cihaz uygulamasının artık paket havuzu için kullanımı gerekmiyorsa, bu kaynağı ayrı olarak silmesi gerekir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** Silinecek Istemci işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) istemci başarıyla silindi
- NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi

### <a name="allowed-from"></a>İzin verilen

Uygulama kodu

### <a name="example"></a>Örnek

```C
/* Delete the POP3 Client. */
status = nx_pop3_client_delete (&demo_client);

/* If the Client was successfully deleted, status = NX_SUCCESS. */
```

## <a name="nx_pop3_client_mail_item_delete"></a>nx_pop3_client_mail_item_delete

Istemci maildrop 'tan belirtilen bir posta öğesini silme

### <a name="prototype"></a>Prototype

```C
UINT nx_pop3_client_mail_items_delete(NX_POP3_CLIENT *client_ptr,
    UINT mail_index);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen posta öğesini Istemci maildrop 'dan siler. Posta öğesi indirildikten sonra, bazı POP3 sunucuları, Istemci tarafından istendikten sonra posta öğelerini otomatik olarak silebilir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** Istemci örneği işaretçisi
- **mail_index** Istemci maildrop 'a Dizin

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) silme isteği başarılı oldu
- **NX_POP3_INVALID_MAIL_ITEM**(0xB2) geçersiz posta öğesi dizini
- **NX_POP3_INSUFFICIENT_PACKET_PAYLOAD**(0xb6) istemci PAKETI yükü POP3 isteği için çok küçük.
- **NX_POP3_SERVER_ERROR_STATUS**(0xb4) sunucu, hata durumuyla yanıt verir
- NX_POP3_CLIENT_INVALID_INDEX (0xB8) geçersiz posta dizini girişi
- NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi

### <a name="allowed-from"></a>İzin verilen

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

### <a name="description"></a>Açıklama

Bu hizmet, Dizin mail_item tarafından belirtilen Istemci maildrop öğesinden bir posta öğesi almaya yönelik bir RETR isteği yapar. Bir RETR isteği yaptıktan ve sunucudan olumlu bir yanıt aldıktan sonra Istemci, *nx_pop3_client_mail_item_message_get* hizmetini kullanarak posta iletisini indirmeye başlayabilir. Hizmetin, sunucu yanıtlarından ayıklanan istenen posta öğesinin boyutunu da sağladığı unutulmamalıdır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** Istemci örneği işaretçisi
- **mail_item** Istemci maildrop 'a Dizin
- **item_size** Posta iletisi boyutu işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) posta öğesi başarıyla alındı
- **NX_POP3_INVALID_MAIL_ITEM** (0xB2) geçersiz posta öğesi dizini
- **NX_POP3_INSUFFICIENT_PACKET_PAYLOAD** (0xb6) istemci PAKETI yükü POP3 isteği için çok küçük.
- **NX_POP3_SERVER_ERROR_STATUS** (0xb4) sunucu, hata durumuyla yanıt verir
- NX_POP3_CLIENT_INVALID_INDEX (0xB8) geçersiz posta dizini girişi
- NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi

### <a name="allowed-from"></a>İzin verilen

Uygulama kodu

### <a name="example"></a>Örnek

```C
ULONG item_size;

/* Retrieve the POP3 Client mail item. */
status = nx_pop3_client_mail_item_get (&demo_client, 1, &item_size);

/* If the mail item was successfully obtained, status = NX_SUCCESS. */
```

## <a name="nx_pop3_client_mail_items_get"></a>nx_pop3_client_mail_items_get

Maildrop 'daki posta öğelerinin sayısını alma

### <a name="prototype"></a>Prototype

```C
UINT nx_pop3_client_mail_items_get(NX_POP3_CLIENT *client_ptr,
    UINT *number_mail_items,
    ULONG *maildrop_total_size);
```

### <a name="description"></a>Açıklama

Bu hizmet, posta öğelerinin sayısını ve Istemci maildrop 'tan gelen posta iletisi verilerinin toplam boyutunu almak için bir STAT isteği yapar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** Istemci örneği işaretçisi
- **number_mail_item** Istemci maildrop 'daki posta sayısı
- **maildrop_total_size** Tüm posta iletisinin boyutu işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) posta öğesi başarıyla alındı
- **NX_POP3_INVALID_MAIL_ITEM** (0xB2) geçersiz posta öğesi dizini
- **NX_POP3_INSUFFICIENT_PACKET_PAYLOAD** (0xb6) istemci PAKETI yükü POP3 isteği için çok küçük.
- **NX_POP3_SERVER_ERROR_STATUS** (0xb4) sunucu, hata durumuyla yanıt verir
- NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi

### <a name="allowed-from"></a>İzin verilen

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

Belirtilen posta öğesi iletisini Al

### <a name="prototype"></a>Prototype

```C
UINT nx_pop3_client_mail_item_message_get(
    NX_POP3_CLIENT *client_ptr,
    NX_PACKET **recv_packet_ptr,
    ULONG *bytes_retrieved,
    UINT *final_packet);
```

### <a name="description"></a>Açıklama

Bu hizmet posta öğesi iletisini, posta iletisinin boyutunu ve posta iletisindeki son paket ise alır. Final_packet NX_TRUE recv_packet_ptr tarafından işaret edilen paket, posta öğesi iletisindeki son pakettir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** Istemci örneği işaretçisi
- **recv_packet_ptr** İleti verisi paketi alındı
- **number_mail_item** Istemci maildrop 'daki posta sayısı
- **maildrop_total_size** Tüm posta iletisinin boyutu işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) posta öğesi başarıyla alındı
- **NX_POP3_CLIENT_INVALID_STATE** (0xb7) istemci PAKETI yükü POP3 isteği için çok küçük.
- NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi

### <a name="allowed-from"></a>İzin verilen

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

Belirtilen posta öğesinin boyutunu al

### <a name="prototype"></a>Prototype

```C
UINT nx_pop3_client_mail_item_size_get(
    NX_POP3_CLIENT *client_ptr,
    UINT mail_item, ULONG *size);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen posta öğesinin boyutunu almak için bir LISTE isteği oluşturur.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** Istemci örneği işaretçisi
- **mail_item** Istemci maildrop 'a Dizin
- **Boyut** Posta iletisi boyutu işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) posta öğesi başarıyla alındı
- **NX_POP3_INVALID_MAIL_ITEM** (0xB2) geçersiz posta öğesi dizini
- **NX_POP3_INSUFFICIENT_PACKET_PAYLOAD** (0xb6) istemci PAKETI yükü POP3 isteği için çok küçük.
- **NX_POP3_SERVER_ERROR_STATUS** (0xb4) sunucu, hata durumuyla yanıt verir
- NX_POP3_CLIENT_INVALID_INDEX (0xB8) geçersiz posta dizini girişi
- NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi

### <a name="allowed-from"></a>İzin verilen

Uygulama kodu

### <a name="example"></a>Örnek

```C
ULONG size;

UINT mail_item;

/* Retrieve the size of the specified mail item in POP3 Client maildrop. */

status = nx_pop3_client_mail_item_size_get (&demo_client, mail_item, &size);

/* If the maildrop message packet was successfully obtained, status = NX_SUCCESS. */
```
