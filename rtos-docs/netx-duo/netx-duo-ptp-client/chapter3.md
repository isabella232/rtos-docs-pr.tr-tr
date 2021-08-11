---
title: Bölüm 3 - NetX Duo PTP Azure RTOS Hizmetlerinin Açıklaması
description: Bu bölümde, tüm NetX Duo PTP istemci hizmetlerinin alfabetik sırada bir açıklaması yer almaktadır.
author: v-condav
ms.author: v-condav
ms.date: 01/27/2021
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 686db68181e3712f9f6a09a9f471626eff610fd7f45ec5b83ba56f8b7aa378cc
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116798019"
---
# <a name="chapter-3---description-of-azure-rtos-netx-duo-ptp-client-services"></a>Bölüm 3 - NetX Duo PTP Azure RTOS Hizmetlerinin Açıklaması

Bu bölümde, tüm NetX Duo PTP istemci hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklaması yer almaktadır.

[!NOTE]
> *Aşağıdaki API **işlevi açıklamalarında** yer alan Dönüş Değerleri bölümünde, **KALıN** olmayan değerler tamamen devre dışı **bırakılırken,** BOLD NX_DISABLE_ERROR_CHECKING API hata denetimi devre dışı bırakmak için kullanılan tanımdan etkilenmez.*

## <a name="nx_ptp_client_create"></a>nx_ptp_client_create

PTP istemci örneği oluşturun.

### <a name="prototype"></a>Prototype

```C
UINT nx_ptp_client_create(
    NX_PTP_CLIENT *client_ptr, NX_IP *ip_ptr, 
    UINT interface_index,
    NX_PACKET_POOL *packet_pool_ptr, 
    UINT thread_priority, 
    UCHAR *thread_stack, 
    UINT stack_size,
    NX_PTP_CLIENT_CLOCK_CALLBACK clock_callback, 
    VOID *clock_callback_data);
```

### <a name="description"></a>Description

Bu hizmet PTP istemcisinin bir örneğini oluşturur.

Uygulamanın önce bir IP örneği ve PTP istemcisinin paketleri iletmesi için bir paket havuzu oluşturması gerektiğini unutmayın. Paket havuzu için, uygulama IP örneğinde aynı paket havuzunu kullanabilir; veya PTP istemcisi için ayrılmış bir paket havuzu oluşturabilir.  Ayrılmış paket havuzu yaklaşımı, küçük paketler (IPv6 kullanılıyorsa 128 bayt paket veya yalnızca IPv4 için 108 bayt) kullanma avantajına sahiptir.

### <a name="input-parameters"></a>Giriş Parametreleri
* **client_ptr** Oluşturmak için PTP istemcisi işaretçisi
* **ip_ptr** IP örneğine işaretçi
* **interface_index** PTP ağ arabirimi dizini
* **packet_pool_ptr** İstemci paket havuzunun işaretçisi
* **thread_priority**  PTP iş parçacığının önceliği
* **thread_stack** İş parçacığı yığını işaretçisi
* **stack_size** İş parçacığı yığınının boyutu
* **clock_callback** PTP saat geri çağırma
* **clock_callback_data** Saat geri arama verileri

### <a name="return-values"></a>Dönüş Değerleri
* **NX_SUCCESS** (0x00) İstemcisi başarıyla oluşturuldu
* **NX_PTP_CLIENT_INSUFFICIENT_PACKET_PAYLOAD** (0xD04) Paket yükü çok küçük
* **NX_PTP_CLIENT_CLOCK_CALLBACK_FAILURE** geri 0xD05 üzerinde hata (0xD05) hatası
* **durum** NetX Duo ve ThreadX hizmet çağrılarının durum tamamlaması
* NX_PTR_ERROR (0x07) Geçersiz giriş işaretçisi parametresi
* NX_INVALID_INTERFACE (0x4C) Geçersiz arabirim

### <a name="allowed-from"></a>İzin Verilen
İş Parçacıkları

### <a name="example"></a>Örnek
```C
/* Create the PTP client instance */
status = nx_ptp_client_create(&ptp_client, &ip_0, 0, &pool_0, 
                              PTP_THREAD_PRIORITY, (UCHAR *)ptp_stack, sizeof(ptp_stack),
                              clock_callback, NX_NULL);

/* If the client was successfully created, status = NX_SUCCESS. */
```

## <a name="nx_ptp_client_delete"></a>nx_ptp_client_delete

PTP istemci örneğini siler.

### <a name="prototype"></a>Prototype

```C
UINT nx_ptp_client_delete(NX_PTP_CLIENT *client_ptr);
```

### <a name="description"></a>Description

Bu hizmet PTP istemcisinin bir örneğini siler.

### <a name="input-parameters"></a>Giriş Parametreleri
* **client_ptr** PtP istemcisinin silinecek işaretçisi

### <a name="return-values"></a>Dönüş Değerleri
* **NX_SUCCESS** (0x00) İstemcisi başarıyla silindi
* NX_PTR_ERROR (0x07) Geçersiz giriş işaretçisi parametresi

### <a name="allowed-from"></a>İzin Verilen
İş Parçacıkları

### <a name="example"></a>Örnek
```C
/* Delete the PTP client instance */
status = nx_ptp_client_delete(&ptp_client);

/* If the client was successfully deleted, status = NX_SUCCESS. */
```

## <a name="nx_ptp_client_master_info_get"></a>nx_ptp_client_master_info_get

Ana saat bilgilerini alır.

### <a name="prototype"></a>Prototype

```C
UINT nx_ptp_client_master_info_get(
    NX_PTP_CLIENT_MASTER *master_ptr, 
    NXD_ADDRESS *address, 
    UCHAR **port_identity, 
    UINT *port_identity_length, 
    UCHAR *priority1, 
    UCHAR *priority2, 
    UCHAR *clock_class, UCHAR *clock_accuracy, 
    USHORT *clock_variance, 
    UCHAR **grandmaster_identity,
    UINT *grandmaster_identity_length, 
    USHORT *steps_removed, 
    UCHAR *time_source);
```

### <a name="description"></a>Description
Bu hizmet ana saat bilgilerini alır. Ana denetim bloğu, olay geri çağırma işlevi aracılığıyla kullanıcı uygulamasına geçirildi.

### <a name="input-parameters"></a>Giriş Parametreleri
* **master_ptr** PTP ana saati işaretçisi
* **adres** Ana saatin adresi
* **port_identity** PTP ana bağlantı noktası ve kimliği
* **port_identity_length** PTP ana bağlantı noktası ve kimliğinin uzunluğu
* **priority1** PTP ana saatinin Priority1'i
* **priority2** PTP ana saatinin Önceliği2
* **clock_class** PTP ana saati sınıfı
* **clock_accuracy** PTP ana saatinin doğruluğu
* **clock_variance** PTP ana saatinin varyansı
* **grandmaster_identity** 14. saatin kimliği
* **grandmaster_identity_length** 1. Kimlik Uzunluğu
* **steps_removed** PTP üst bilgilerinden kaldırılan adımlar
* **time_source** Süreölçer tarafından kullanılan zamanlayıcı kaynağı

### <a name="return-values"></a>Dönüş Değerleri
* **NX_SUCCESS** (0x00) Ana saat bilgilerini başarıyla alın
* NX_PTR_ERROR (0x07) Geçersiz giriş işaretçisi parametresi

### <a name="allowed-from"></a>İzin Verilen
İş Parçacıkları

### <a name="example"></a>Örnek
```C
static UINT ptp_event_callback(NX_PTP_CLIENT *ptp_client_ptr, UINT event, VOID *event_data, VOID *callback_data)
{
NXD_ADDRESS address;
UCHAR *port_identity;
UINT port_identity_length;
UCHAR priority1, priority2;
UCHAR clock_class, clock_accuracy;
USHORT clock_variance;
UCHAR *grandmaster_identity;
UINT grandmaster_identity_length;
USHORT steps_removed;
UCHAR time_source;

    switch (event)
    {
        case NX_PTP_CLIENT_EVENT_MASTER:
        {
            status = nx_ptp_client_master_info_get((NX_PTP_CLIENT_MASTER *)event_data, 
                                                   &address, &port_identity,
                                                   &port_identity_length, &priority1, 
                                                   &priority2, &clock_class,
                                                   &clock_accuracy, &clock_variance, 
                                                   &grandmaster_identity,
                                                   &grandmaster_identity_length, 
                                                   &steps_removed, &time_source);

            /* If the master clock information was successfully get, status = NX_SUCCESS. */
            break;
        }

        /* Other event process. */
    }
}
```

## <a name="nx_ptp_client_packet_timestamp_notify"></a>nx_ptp_client_packet_timestamp_notify

PTP istemcisine paketin zaman damgasını bildir.

### <a name="prototype"></a>Prototype

```C
VOID nx_ptp_client_packet_timestamp_notify(
    NX_PTP_CLIENT *client_ptr, 
    NX_PACKET *packet_ptr, 
    NX_PTP_TIME *timestamp_ptr);
```

### <a name="description"></a>Description
Bu hizmet, PTP istemcisine paketin zaman damgasıyla iletil olduğunu belirtir. Bu hizmet, ağ sürücüsü için tasarlanmıştır ve paket iletilirken çağrılır. Zaman damgası genellikle donanım tarafından oluşturulur.

### <a name="input-parameters"></a>Giriş Parametreleri
* **client_ptr** Oluşturmak için PTP istemcisi işaretçisi
* **packet_ptr** İletilen PTP paketi işaretçisi
* **timestamp_ptr** PTP paketinin zaman damgasına işaretçi

### <a name="return-values"></a>Dönüş Değerleri
Hiçbiri

### <a name="allowed-from"></a>İzin Verilen
İş Parçacıkları

### <a name="example"></a>Örnek
```C
/* Call notification callback */
nx_ptp_client_packet_timestamp_notify(client_ptr, packet_ptr, &ts);
```

## <a name="nx_ptp_client_soft_clock_callback"></a>nx_ptp_client_soft_clock_callback

PTP saatinin yazılım uygulaması.

### <a name="prototype"></a>Prototype

```C
UINT nx_ptp_client_soft_clock_callback(
    NX_PTP_CLIENT *client_ptr, 
    UINT operation,
    NX_PTP_TIME *time_ptr, 
    NX_PACKET *packet_ptr,
    VOID *callback_data);
```

### <a name="description"></a>Description
Bu geri çağırma işlevi, PTP için düşük çözünürlüklü bir saat kaynağı simülasyonu işlevi gösterir. Bu yordam bir başvuru olarak sağlanır ve üretim için kullanılamaz.

### <a name="input-parameters"></a>Giriş Parametreleri
* **client_ptr** Oluşturmak için PTP istemcisi işaretçisi
* **işlemi** Geri çağırma işlemi, geçerli değerler şu şekilde tanımlanır:
  * **NX_PTP_CLIENT_CLOCK_INIT** Saati başlatma.
  * **NX_PTP_CLIENT_CLOCK_SET** tarafından belirtilen geçerli zaman damgasını `time_ptr` ayarlayın.
  * **NX_PTP_CLIENT_CLOCK_GET** Geçerli zaman damgasını olarak `time_ptr` iade.
  * **NX_PTP_CLIENT_CLOCK_PACKET_TS_EXTRACT** zaman damgasını 'den 'ye `packet_ptr` `time_ptr` ayıklar.
  * **NX_PTP_CLIENT_CLOCK_ADJUST** Geçerli zaman damgasını *1 saniyenin altında ayarlayın.*
  * **NX_PTP_CLIENT_CLOCK_PACKET_TS_PREPARE** İletilen `packet_ptr` zaman damgasını PTP istemcisine bildirmeyi gerektiren 'i işaretlendi.
  * **NX_PTP_CLIENT_CLOCK_SOFT_TIMER_UPDATE** Yazılım zamanlayıcıyı güncelleştirin. Donanım saati tarafından yoksayılabilir.
* **time_ptr** Zaman damgası işaretçisi.
* **packet_ptr** Paket işaretçisi.
* **callback_data** Opak geri çağırma verilerine işaretçi.

### <a name="return-values"></a>Dönüş Değerleri
* **NX_SUCCESS** (0x00) İşlem başarıyla
* **NX_PTP_PARAM_ERROR** (0xD03) Geçersiz parametre

### <a name="allowed-from"></a>İzin Verilen
PTP iç

### <a name="example"></a>Örnek
```C/* Create the PTP client instance */
status = nx_ptp_client_create(&ptp_client, &ip_0, 0, &pool_0, 
                              PTP_THREAD_PRIORITY, (UCHAR *)ptp_stack, sizeof(ptp_stack),
                              nx_ptp_client_soft_clock_callback, NX_NULL);

/* If the client was successfully created, status = NX_SUCCESS. */
```

## <a name="nx_ptp_client_start"></a>nx_ptp_client_start

PTP istemcisini başlatma.

### <a name="prototype"></a>Prototype

```C
UINT nx_ptp_client_start(
    NX_PTP_CLIENT *client_ptr, 
    UCHAR *client_port_identity_ptr, 
    UINT client_port_identity_length,
    UINT domain, 
    UINT transport_specific, 
    NX_PTP_CLIENT_EVENT_CALLBACK event_callback,
    VOID *event_callback_data)
```

### <a name="description"></a>Description
Bu hizmet, önceden oluşturulmuş bir PTP istemci örneğini başlatır.

### <a name="input-parameters"></a>Giriş Parametreleri
* **client_ptr** Oluşturmak için PTP istemcisi işaretçisi
* **client_port_identity_ptr** İstemci bağlantı noktası ve kimliği işaretçisi, NULL olabilir
* **client_port_identity_length** İstemci bağlantı noktası ve kimliği uzunluğu. NULL veya null ise client_port_identity_ptr (10) NX_PTP_CLOCK_PORT_IDENTITY_SIZE 0 olmalıdır
* **etki alanı** PTP saat etki alanı
* **transport_specific** 4 bit aktarıma özgü
* **event_callback** Olay üzerinde çağrılan geri çağırma işlevi
* **event_callback_data** Olay geri çağırma verileri

### <a name="return-values"></a>Dönüş Değerleri
* **NX_SUCCESS** (0x00) İstemcisi başarıyla başlatıldı
* **NX_PTP_CLIENT_ALREADY_STARTED** (0xD02) PTP istemcisi zaten başlatıldı
* **durum** NetX Duo ve ThreadX hizmet çağrılarının durum tamamlaması
* NX_PTR_ERROR (0x07) Geçersiz giriş işaretçisi parametresi

### <a name="allowed-from"></a>İzin Verilen
İş Parçacıkları

### <a name="example"></a>Örnek
```C
status = nx_ptp_client_start(&ptp_client, NX_NULL, 0, 0, 0, ptp_event_callback, NX_NULL);

/* If the client was successfully started, status = NX_SUCCESS. */
```

## <a name="nx_ptp_client_stop"></a>nx_ptp_client_stop

PTP istemcisini durdurun.  PTP istemcisi durdurulduktan sonra, PTP paketlerini işlemez ve PTP paketlerini iletmez.

### <a name="prototype"></a>Prototype

```C
UINT nx_ptp_client_stop(NX_PTP_CLIENT *client_ptr);
```

### <a name="description"></a>Description
Bu hizmet, önceden oluşturulmuş ve başlatılan bir PTP istemci örneğini durdurur.

### <a name="input-parameters"></a>Giriş Parametreleri
* **client_ptr** PtP istemcisinin durdurmak için işaretçisi

### <a name="return-values"></a>Dönüş Değerleri
* **NX_SUCCESS** (0x00) İstemcisi başarıyla durduruldu
* **NX_PTP_CLIENT_NOT_STARTED** (0xD01) İstemcisi başlamadı
* NX_PTR_ERROR (0x07) Geçersiz giriş işaretçisi parametresi

### <a name="allowed-from"></a>İzin Verilen
İş Parçacıkları

### <a name="example"></a>Örnek
```C
status = nx_ptp_client_stop(&ptp_client);

/* If the client was successfully stopped, status = NX_SUCCESS. */
```

## <a name="nx_ptp_client_sync_info_get"></a>nx_ptp_client_sync_info_get

Eşitleme bilgilerini al.

### <a name="prototype"></a>Prototype

```C
UINT nx_ptp_client_sync_info_get(
    NX_PTP_CLIENT_SYNC *sync_ptr, 
    USHORT *flags, 
    SHORT *utc_offset);
```

### <a name="description"></a>Description
Bu hizmet Eşitleme iletisi bilgilerini alır. Eşitleme denetim bloğu, olay geri çağırma işlevi aracılığıyla kullanıcı uygulamasına geçirildi.

### <a name="input-parameters"></a>Giriş Parametreleri
* **client_ptr** Oluşturmak için PTP istemcisi işaretçisi
* **bayraklar** Eşitleme iletisinde bayraklar
* **utc_offset** UTC ile UTC arasında uzaklık

### <a name="return-values"></a>Dönüş Değerleri
* **NX_SUCCESS** (0x00) Eşitleme bilgilerini başarıyla al
* NX_PTR_ERROR (0x07) Geçersiz giriş işaretçisi parametresi

### <a name="allowed-from"></a>İzin Verilen
İş Parçacıkları

### <a name="example"></a>Örnek
```C
static UINT ptp_event_callback(NX_PTP_CLIENT *ptp_client_ptr, UINT event, VOID *event_data, VOID *callback_data)
{
USHORT utc_offset;

    switch (event)
    {
        case NX_PTP_CLIENT_EVENT_SYNC:
        {
            nx_ptp_client_sync_info_get((NX_PTP_CLIENT_SYNC *)event_data, NX_NULL, &utc_offset);

            /* If the Sync information was successfully get, status = NX_SUCCESS. */
            break;
        }

        /* Other event process. */
    }
}
```

## <a name="nx_ptp_client_time_get"></a>nx_ptp_client_time_get

Geçerli saati al.

### <a name="prototype"></a>Prototype

```C
UINT nx_ptp_client_time_get(
    NX_PTP_CLIENT *client_ptr, 
    NX_PTP_TIME *time_ptr);
```

### <a name="description"></a>Description
Bu hizmet PTP saatinin geçerli değerini alır. PTP istemcisi ana saatle eşitlenmiş veya eşitlenmese de kullanılabilir.

### <a name="input-parameters"></a>Giriş Parametreleri
* **client_ptr** Oluşturmak için PTP istemcisi işaretçisi
* **time_ptr** PTP saati işaretçisi

### <a name="return-values"></a>Dönüş Değerleri
* **NX_SUCCESS** (0x00) İstemcisi başarıyla oluşturuldu
* NX_PTR_ERROR (0x07) Geçersiz giriş işaretçisi parametresi

### <a name="allowed-from"></a>İzin Verilen
İş Parçacıkları

### <a name="example"></a>Örnek
```C
/* Get the PTP clock */
nx_ptp_client_time_get(&ptp_client, &tm);
```

## <a name="nx_ptp_client_time_set"></a>nx_ptp_client_time_set

Geçerli saati ayarlayın.

### <a name="prototype"></a>Prototype

```C
UINT nx_ptp_client_time_set(
    NX_PTP_CLIENT *client_ptr, 
    NX_PTP_TIME *time_ptr);
```

### <a name="description"></a>Description
Bu hizmet PTP saatinin geçerli değerini ayarlar. PTP istemcisi başlamadan önce çağrılmalı.

### <a name="input-parameters"></a>Giriş Parametreleri
* **client_ptr** Oluşturmak için PTP istemcisi işaretçisi
* **time_ptr** PTP saati işaretçisi

### <a name="return-values"></a>Dönüş Değerleri
* **NX_SUCCESS** (0x00) İstemcisi başarıyla oluşturuldu
* **NX_PTP_CLIENT_ALREADY_STARTED** (0xD02) PTP istemcisi zaten başlatıldı
* NX_PTR_ERROR (0x07) Geçersiz giriş işaretçisi parametresi

### <a name="allowed-from"></a>İzin Verilen
İş Parçacıkları

### <a name="example"></a>Örnek
```C
/* Set current time before PTP client started.  */
status = nx_ptp_client_time_set(&ptp_client, &tm);
```

## <a name="nx_ptp_client_utility_convert_time_to_date"></a>nx_ptp_client_utility_convert_time_to_date

PTP saat bir UTC tarih ve saat dönüştürme.

### <a name="prototype"></a>Prototype

```C
UINT nx_ptp_client_utility_convert_time_to_date(
    NX_PTP_TIME *time_ptr, 
    LONG offset, 
    NX_PTP_DATE_TIME *date_time_ptr);
```

### <a name="description"></a>Description
Bu hizmet, PTP Time süresini UTC Tarih ve saatine dönüştürür.

### <a name="input-parameters"></a>Giriş Parametreleri
* **time_ptr** PTP saati işaretçisi
* **konum** PTP saati eklemek için imzalanan ikinci konum
* **date_time_ptr** Sonuç tarihi işaretçisi

### <a name="return-values"></a>Dönüş Değerleri
* **NX_SUCCESS** (0x00) istemci başarıyla oluşturuldu
* **Sonuç tarihi işaretçisi** (0xd03) geçersiz giriş parametresi
* NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi

### <a name="allowed-from"></a>İzin verilen
İş Parçacıkları

### <a name="example"></a>Örnek
```C
/* convert PTP time to UTC date and time */
status = nx_ptp_client_utility_convert_time_to_date(&tm, -ptp_utc_offset, &date);

/* If the time was successfully converted, status = NX_SUCCESS. */
```

## <a name="nx_ptp_client_utility_time_diff"></a>nx_ptp_client_utility_time_diff

İki PTP kez fark.

### <a name="prototype"></a>Prototype

```C
UINT nx_ptp_client_utility_time_diff(
    NX_PTP_TIME *time1_ptr, 
    NX_PTP_TIME *time2_ptr, 
    NX_PTP_TIME *result_ptr);
```

### <a name="description"></a>Description
Bu hizmet iki MTP saati arasındaki farkı hesaplar.

### <a name="input-parameters"></a>Giriş Parametreleri
* **time1_ptr** İlk PTP saati işaretçisi
* **time2_ptr** İkinci PTP saati işaretçisi
* **result_ptr** Result Time1-time2 işaretçisi

### <a name="return-values"></a>Dönüş Değerleri
* **NX_SUCCESS** (0x00) istemci başarıyla oluşturuldu
* NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi

### <a name="allowed-from"></a>İzin verilen
İş Parçacıkları

### <a name="example"></a>Örnek
```C
/* Diff time.  */
status = nx_ptp_client_utility_time_diff(&time1, &time2, &result);

/* If the calculation was successfully, status = NX_SUCCESS. */
```