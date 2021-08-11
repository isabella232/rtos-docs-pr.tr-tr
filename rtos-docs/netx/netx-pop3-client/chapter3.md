---
title: Bölüm 3-Azure RTOS NetX POP3 Istemci hizmetlerinin açıklaması
description: Bu bölüm, tüm Azure RTOS NetX POP3 Istemci hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: f68d6ac942c829dbf6eb9be334328b1b58a47ea370a73d37f471ec32cd46a360
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116782396"
---
# <a name="chapter-3---description-of-azure-rtos-netx-pop3-client-services"></a>Bölüm 3-Azure RTOS NetX POP3 Istemci hizmetlerinin açıklaması

Bu bölüm, tüm Azure RTOS NetX POP3 Istemci hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.

Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_DISABLE_ERROR_CHECKING** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.

- nx_pop3_client_create: *BIR POP3 Istemci örneği oluşturma*
- nx_pop3_client_delete: *BIR POP3 istemci örneğini silme*
- nx_pop3_client_ mail_item_get: *sunucu maildrop 'dan bir istemci posta öğesini silme*
- nx_pop3_client_mail_item_get: *belirli bir posta iletisi boyutunu alın*
- nx_pop3_client_mail_items_get: *maildrop 'daki posta öğelerinin sayısını alma*
- nx_pop3_client_mail_item_message _get: *belirli bir posta Iletisini indirin*
- nx_pop3_client_mail_item_size_get: *belirli bir posta öğesinin boyutunu alma*

## <a name="nx_pop3_client_create"></a>nx_pop3_client_create

POP3 Istemci örneği oluşturma

### <a name="prototype"></a>Prototype

```c
UINT nx_pop3_client_create(NX_POP3_CLIENT *client_ptr,
                        UINT APOP_authentication, NX_IP *ip_ptr,
                        NX_PACKET_POOL *packet_pool_ptr,
                        ULONG server_ip_address,
                        ULONG server_port,
                        CHAR *client_name, CHAR *client_password);
```

### <a name="description"></a>Description

Bu hizmet, POP3 Istemcisinin bir örneğini oluşturur ve yapılandırmasını giriş parametreleriyle ayarlar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr**: oluşturulacak istemciye yönelik işaretçi
- **APOP_authentication**: APOP kimlik doğrulamasını etkinleştir
- **ip_ptr**: IP örneğine yönelik işaretçi
- **packet_pool_ptr**: istemci paket havuzuna yönelik işaretçi
- **server_ip_address**: POP3 sunucu adresi
- **SERVER_PORT**: POP3 sunucu bağlantı noktası
- **client_name**: istemci adı işaretçisi
- **client_password**: istemci parolası işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) istemci başarıyla oluşturuldu
- **durum**: NETX ve threadx hizmeti çağrılarının durum bitimi
- NX_PTR_ERROR: (0x07) geçersiz giriş işaretçisi parametresi
- NX_POP3_PARAM_ERROR: (0xB1) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

Uygulama kodu

### <a name="example"></a>Örnek

```c
/* Create the POP3 Client. */

/* Create username and password for our POP3 Client mail drop. */
#define LOCALHOST                   "recipient@expresslogic.com"
#define LOCALHOST_PASSWORD          "pass"
#define POP3_SERVER_ADDRESS         IP_ADDRESS(192,2,2,92
#define POP3_SERVER_PORT            110

/* Create a NetX POP3 Client instance. */
ULONG server_ip_address = IP_ADDRESS(1,2,3,4);
status = nx_pop3_client_create(&demo_client,
        NX_FALSE /* disable APOP authentication */,
        &client_ip, &client_packet_pool,
        server_ip_address, POP3_SERVER_PORT,
        LOCALHOST, LOCALHOST_PASSWORD);

/* If the Client was successfully created, status = NX_SUCCESS. */
```

## <a name="nx_pop3_client_delete"></a>nx_pop3_client_delete

POP3 Istemci örneğini silme

### <a name="prototype"></a>Prototype

```c
UINT nx_pop3_client_delete(NX_POP3_CLIENT *client_ptr)
```

### <a name="description"></a>Description

Bu hizmet önceden oluşturulmuş bir POP3 Istemcisini siler. Bu hizmet POP3 Istemci paket havuzunu silmez. Cihaz uygulamasının artık paket havuzu için kullanımı gerekmiyorsa, bu kaynağı ayrı olarak silmesi gerekir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr**: silinecek istemciye yönelik işaretçi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) istemci başarıyla silindi
- NX_PTR_ERROR: (0x07) geçersiz giriş işaretçisi parametresi

### <a name="allowed-from"></a>İzin verilen

Uygulama kodu

### <a name="example"></a>Örnek

```c
/* Delete the POP3 Client. */
status = nx_pop3_client_delete (&demo_client);

/* If the Client was successfully deleted, status = NX_SUCCESS. */
```

## <a name="nx_pop3_client_mail_item_delete"></a>nx_pop3_client_mail_item_delete

Istemci maildrop 'tan belirtilen bir posta öğesini silme

### <a name="prototype"></a>Prototype

```c
UINT nx_pop3_client_mail_items_delete(NX_POP3_CLIENT *client_ptr,
                                    UINT mail_index)
```

### <a name="description"></a>Description

Bu hizmet, belirtilen posta öğesini Istemci maildrop 'dan siler. Posta öğesi indirildikten sonra, bazı POP3 sunucuları, Istemci tarafından istendikten sonra posta öğelerini otomatik olarak silebilir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr**: istemci örneğine yönelik işaretçi
- **mail_index**: istemci maildrop 'a Dizin

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) silme isteği başarılı
- **NX_POP3_INVALID_MAIL_ITEM**: (0Xb2) geçersiz posta öğesi dizini
- **NX_POP3_INSUFFICIENT_PACKET_PAYLOAD**: (0Xb6) istemci paket yükü POP3 isteği için çok küçük.
- **NX_POP3_SERVER_ERROR_STATUS**: (0Xb4) sunucu, hata durumuyla yanıt verir
- NX_POP3_CLIENT_INVALID_INDEX: (0xB8) geçersiz posta dizini girişi
- NX_PTR_ERROR: (0x07) geçersiz giriş işaretçisi parametresi

### <a name="allowed-from"></a>İzin verilen

Uygulama kodu

### <a name="example"></a>Örnek

```c
ULONG     item_index;

/* Delete the POP3 Client mail item. */
status = nx_pop3_client_mail_item_delete(&demo_client, item_index);

/* If the server accepts the DELE request (and deletes the mail item), status = 
   NX_SUCCESS. */
```

## <a name="nx_pop3_client_mail_item_get"></a>nx_pop3_client_mail_item_get

Belirtilen posta öğesini alma

### <a name="prototype"></a>Prototype

```c
UINT nx_pop3_client_mail_item_get(NX_POP3_CLIENT *client_ptr,
                                UINT mail_item, ULONG *item_size)
```

### <a name="description"></a>Description

Bu hizmet, Dizin mail_item tarafından belirtilen Istemci maildrop öğesinden bir posta öğesi almaya yönelik bir RETR isteği yapar. Bir RETR isteği yaptıktan ve sunucudan olumlu bir yanıt aldıktan sonra Istemci, *nx_pop3_client_mail_item_message_get* hizmetini kullanarak posta iletisini indirmeye başlayabilir. Hizmetin, sunucu yanıtlarından ayıklanan istenen posta öğesinin boyutunu da sağladığı unutulmamalıdır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr**: istemci örneğine yönelik işaretçi
- **mail_item**: istemci maildrop 'a Dizin
- **item_size**: posta iletisi boyutu işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) posta öğesi başarıyla alındı
- **NX_POP3_INVALID_MAIL_ITEM**: (0Xb2) geçersiz posta öğesi dizini
- **NX_POP3_INSUFFICIENT_PACKET_PAYLOAD**: (0Xb6) istemci paket yükü POP3 isteği için çok küçük.
- **NX_POP3_SERVER_ERROR_STATUS**: (0Xb4) sunucu, hata durumuyla yanıt verir
- NX_POP3_CLIENT_INVALID_INDEX: (0xB8) geçersiz posta dizini girişi
- NX_PTR_ERROR: (0x07) geçersiz giriş işaretçisi parametresi

### <a name="allowed-from"></a>İzin verilen

Uygulama kodu

### <a name="example"></a>Örnek

```c
ULONG     item_size;

/* Retrieve the POP3 Client mail item. */
status = nx_pop3_client_mail_item_get (&demo_client, 1, &item_size);

/* If the mail item was successfully obtained, status = NX_SUCCESS. */
```

## <a name="nx_pop3_client_mail_items_get"></a>nx_pop3_client_mail_items_get

Maildrop 'daki posta öğelerinin sayısını alma

### <a name="prototype"></a>Prototype

```c
UINT nx_pop3_client_mail_items_get(NX_POP3_CLIENT *client_ptr,
                                UINT *number_mail_items,
                                ULONG *maildrop_total_size)
```

### <a name="description"></a>Description

Bu hizmet, posta öğelerinin sayısını ve Istemci maildrop 'tan gelen posta iletisi verilerinin toplam boyutunu almak için bir STAT isteği yapar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr**: istemci örneğine yönelik işaretçi
- **number_mail_item**: istemci maildrop 'daki posta sayısı
- **maildrop_total_size**: tüm posta iletisinin boyutu işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) posta öğesi başarıyla alındı
- **NX_POP3_INVALID_MAIL_ITEM:**(0xB2) Geçersiz posta öğesi dizini
- **NX_POP3_INSUFFICIENT_PACKET_PAYLOAD:**(0xB6) İSTEMCI paket yükü POP3 isteği için çok küçük.
- **NX_POP3_SERVER_ERROR_STATUS:**(0xB4) Sunucu hata durumuyla yanıt verir 
- NX_PTR_ERROR: (0x07) Geçersiz giriş işaretçisi parametresi

### <a name="allowed-from"></a>İzin Verilen

Uygulama kodu

### <a name="example"></a>Örnek

```c
UINT      number_mail_items;
ULONG     maildrop_total_size;

/* Retrieve the size and number of items in POP3 Client maildrop. */
status = nx_pop3_client_mail_item_get (&demo_client, 1, &number_mail_items,
                                        &maildrop_total_size);

/* If the maildrop data was successfully obtained, status = NX_SUCCESS. */
```

## <a name="nx_pop3_client_mail_item_message_get"></a>nx_pop3_client_mail_item_message_get

Belirtilen posta öğesi iletisini alma

### <a name="prototype"></a>Prototype

```c
UINT nx_pop3_client_mail_item_message_get(
                NX_POP3_CLIENT *client_ptr,
                NX_PACKET **recv_packet_ptr,
                ULONG *bytes_retrieved,
                UINT *final_packet)
```

### <a name="description"></a>Description

Bu hizmet posta öğesi iletisini, posta iletisinin boyutunu ve posta iletisinde son paketse alır. Bu `final_packet` NX_TRUE tarafından işaret eden `recv_packet_ptr` paket, posta öğesi iletisinde son pakettir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr:** İstemci örneğine işaretçi
- **recv_packet_ptr:** İleti verileri paketi alındı
- **number_mail_item:** İstemci postası'nın posta sayısı
- **maildrop_total_size:** Tüm posta iletisinin boyutunu gösteren işaretçi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:**(0x00) Posta öğesi başarıyla alındı
- **NX_POP3_CLIENT_INVALID_STATE:**(0xB7) POP3 isteği için çok küçük istemci paket yükü.
- NX_PTR_ERROR (0x07) Geçersiz giriş işaretçisi parametresi

### <a name="allowed-from"></a>İzin Verilen

Uygulama kodu

### <a name="example"></a>Örnek

```c
NX_PACKET     *recv_packet_ptr;
ULONG         bytes_retrieved;
UINT          final_packet;

/* Retrieve the size and number of items in POP3 Client maildrop. */
status = nx_pop3_client_mail_item_message_get (&demo_client, &recv_packet_ptr,
                                                bytes_retrieved, final_packet);

/* If the maildrop message packet was successfully obtained, status = NX_SUCCESS. */
```

## <a name="nx_pop3_client_mail_item_size_get"></a>nx_pop3_client_mail_item_size_get

Belirtilen posta öğesinin boyutunu alma

### <a name="prototype"></a>Prototype

```c
UINT nx_pop3_client_mail_item_size_get(
                NX_POP3_CLIENT *client_ptr,
                UINT mail_item, ULONG *size)
```

### <a name="description"></a>Description

Bu hizmet, belirtilen posta öğesinin boyutunu almak için bir LIST isteği yapar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr:** İstemci örneğine işaretçi
- **mail_item:** İstemci postade dizin oluşturma
- **boyut:** Posta iletisinin boyutunu gösteren işaretçi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:**(0x00) Posta öğesi başarıyla alındı
- **NX_POP3_INVALID_MAIL_ITEM:**(0xB2) Geçersiz posta öğesi dizini
- **NX_POP3_INSUFFICIENT_PACKET_PAYLOAD:**(0xB6) İSTEMCI paket yükü POP3 isteği için çok küçük.
- **NX_POP3_SERVER_ERROR_STATUS:**(0xB4) Sunucu hata durumuyla yanıt verir
- NX_POP3_CLIENT_INVALID_INDEX: (0xB8) Geçersiz posta dizini girişi
- NX_PTR_ERROR: (0x07) Geçersiz giriş işaretçisi parametresi

### <a name="allowed-from"></a>İzin Verilen

Uygulama kodu

### <a name="example"></a>Örnek

```c
ULONG     size;
UINT      mail_item;

/* Retrieve the size of the specified mail item in POP3 Client maildrop. */
status = nx_pop3_client_mail_item_size_get (&demo_client, mail_item, &size);

/* If the maildrop message packet was successfully obtained, status = NX_SUCCESS. */
```
