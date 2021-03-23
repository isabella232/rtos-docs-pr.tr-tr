---
title: Bölüm 3-Azure RTOS NetX Duo MTP Istemci hizmetlerinin açıklaması
description: Bu bölüm, tüm NetX Duo MTP istemci hizmetlerinin alfabetik sırada bir açıklamasını içerir.
author: v-condav
ms.author: v-condav
ms.date: 01/27/2021
ms.topic: article
ms.service: rtos
ms.openlocfilehash: b4cdeca81c157934e35a219cd5535ec38f2c0746
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825804"
---
# <a name="chapter-3---description-of-azure-rtos-netx-duo-ptp-client-services"></a>Bölüm 3-Azure RTOS NetX Duo MTP Istemci hizmetlerinin açıklaması

Bu bölüm, tüm NetX Duo MTP istemci hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.

[!NOTE]
> *Aşağıdaki API işlevi açıklamalarındaki **dönüş değerleri** bölümünde **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_DISABLE_ERROR_CHECKING** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.*

## <a name="nx_ptp_client_create"></a>nx_ptp_client_create

Bir PTP istemci örneği oluşturun.

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

### <a name="description"></a>Açıklama

Bu hizmet, PTP Client 'ın bir örneğini oluşturur.

Uygulamanın, bir IP örneği ve MTP istemcisinin paketleri aktarabilmesi için bir paket havuzu oluşturması gerektiğini unutmayın. Uygulama, paket havuzu için IP örneğinde aynı paket havuzunu kullanabilir. veya, PTP istemcisi için adanmış bir paket havuzu oluşturabilir.  Adanmış paket havuzu yaklaşımı, küçük paketleri (IPv6 kullanılıyorsa 128 bayt paketi veya yalnızca IPv4 için 108 bayt) kullanmanın avantajlarından yararlanır.

### <a name="input-parameters"></a>Giriş Parametreleri
* **client_ptr** Oluşturulacak PTP Client işaretçisi
* **ip_ptr** IP örneği işaretçisi
* **interface_index** PTP Network arabiriminin dizini
* **packet_pool_ptr** İstemci paket havuzu işaretçisi
* **thread_priority**  PTP iş parçacığının önceliği
* **thread_stack** İş parçacığı yığını işaretçisi
* **stack_size** İş parçacığı yığınının boyutu
* **clock_callback** PTP Clock geri çağırma
* **clock_callback_data** Saat geri çağırması için veriler

### <a name="return-values"></a>Dönüş Değerleri
* **NX_SUCCESS** (0x00) istemci başarıyla oluşturuldu
* **NX_PTP_CLIENT_INSUFFICIENT_PACKET_PAYLOAD** (0xd04) paket yükü çok küçük
* **NX_PTP_CLIENT_CLOCK_CALLBACK_FAILURE** (0xd05) saat geri aramasında hata
* **durum** NetX Duo ve ThreadX hizmeti çağrılarının durum bitimi
* NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi
* NX_INVALID_INTERFACE (0x4C) geçersiz arabirim

### <a name="allowed-from"></a>İzin verilen
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

Bir PTP istemci örneğini siler.

### <a name="prototype"></a>Prototype

```C
UINT nx_ptp_client_delete(NX_PTP_CLIENT *client_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, PTP istemcisinin bir örneğini siler.

### <a name="input-parameters"></a>Giriş Parametreleri
* **client_ptr** Silinecek PTP Client işaretçisi

### <a name="return-values"></a>Dönüş Değerleri
* **NX_SUCCESS** (0x00) istemci başarıyla silindi
* NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi

### <a name="allowed-from"></a>İzin verilen
İş Parçacıkları

### <a name="example"></a>Örnek
```C
/* Delete the PTP client instance */
status = nx_ptp_client_delete(&ptp_client);

/* If the client was successfully deleted, status = NX_SUCCESS. */
```

## <a name="nx_ptp_client_master_info_get"></a>nx_ptp_client_master_info_get

Ana saat bilgilerini alın.

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

### <a name="description"></a>Açıklama
Bu hizmet, ana saat bilgilerini alır. Ana denetim bloğu, olay geri çağırma işlevi aracılığıyla kullanıcı uygulamasına geçirilir.

### <a name="input-parameters"></a>Giriş Parametreleri
* **master_ptr** PTP ana saati işaretçisi
* **Adres** Ana saatin adresi
* **port_identity** PTP ana bağlantı noktası ve kimliği
* **port_identity_length** PTP ana bağlantı noktasının ve kimliğin uzunluğu
* **Priority1** Priority1 of PTP Master saati
* **priority2** Priority2 of PTP Master saati
* **clock_class** PTP Master saatinin sınıfı
* **clock_accuracy** PTP Master saatinin doğruluğu
* **clock_variance** PTP Master saatinin varyansı
* **grandmaster_identity** Ana saatin kimliği
* **grandmaster_identity_length** Ana kimliğin uzunluğu
* **steps_removed** Adımlar, PTP başlığından kaldırıldı
* **time_source** Ana saat tarafından kullanılan zamanlayıcı kaynağı

### <a name="return-values"></a>Dönüş Değerleri
* **NX_SUCCESS** (0x00) ana saat bilgilerini başarıyla alın
* NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi

### <a name="allowed-from"></a>İzin verilen
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

PTP Client 'ı paketin zaman damgasına bildirme.

### <a name="prototype"></a>Prototype

```C
VOID nx_ptp_client_packet_timestamp_notify(
    NX_PTP_CLIENT *client_ptr, 
    NX_PACKET *packet_ptr, 
    NX_PTP_TIME *timestamp_ptr);
```

### <a name="description"></a>Açıklama
Bu hizmet, PTP istemcisine paketin zaman damgasıyla iletildiğini bildirir. Bu hizmet ağ sürücüsü için tasarlanmıştır ve paket iletildiğinde çağrılır. Zaman damgası genellikle donanım tarafından oluşturulur.

### <a name="input-parameters"></a>Giriş Parametreleri
* **client_ptr** Oluşturulacak PTP Client işaretçisi
* **packet_ptr** Aktarılan PTP paketi işaretçisi
* **timestamp_ptr** MTP paketinin zaman damgası işaretçisi

### <a name="return-values"></a>Dönüş Değerleri
Yok

### <a name="allowed-from"></a>İzin verilen
İş Parçacıkları

### <a name="example"></a>Örnek
```C
/* Call notification callback */
nx_ptp_client_packet_timestamp_notify(client_ptr, packet_ptr, &ts);
```

## <a name="nx_ptp_client_soft_clock_callback"></a>nx_ptp_client_soft_clock_callback

Bir PTP saatinin yazılım uygulama.

### <a name="prototype"></a>Prototype

```C
UINT nx_ptp_client_soft_clock_callback(
    NX_PTP_CLIENT *client_ptr, 
    UINT operation,
    NX_PTP_TIME *time_ptr, 
    NX_PACKET *packet_ptr,
    VOID *callback_data);
```

### <a name="description"></a>Açıklama
Bu geri çağırma işlevi, PTP için benzetimli düşük çözünürlüklü saat kaynağı olarak görev yapar. Bu yordam bir başvuru olarak sağlanır ve üretim için kullanılamaz.

### <a name="input-parameters"></a>Giriş Parametreleri
* **client_ptr** Oluşturulacak PTP Client işaretçisi
* **işlem** Geri çağırma işlemi, geçerli değerler şu şekilde tanımlanır:
  * **NX_PTP_CLIENT_CLOCK_INIT** Saati başlatın.
  * **NX_PTP_CLIENT_CLOCK_SET** Tarafından belirtilen geçerli zaman damgasını ayarla `time_ptr` .
  * **NX_PTP_CLIENT_CLOCK_GET** Geçerli zaman damgasını döndürür `time_ptr` .
  * **NX_PTP_CLIENT_CLOCK_PACKET_TS_EXTRACT** Zaman damgasını konumundan `packet_ptr` ayıklayın `time_ptr` .
  * **NX_PTP_CLIENT_CLOCK_ADJUST** Geçerli zaman damgasını *1* saniyeden az ayarlayın.
  * **NX_PTP_CLIENT_CLOCK_PACKET_TS_PREPARE** `packet_ptr` PTP Client ' ın aktarıldığı zaman damgasına bildirilmesini gerektiren öğesini işaretleyin.
  * **NX_PTP_CLIENT_CLOCK_SOFT_TIMER_UPDATE** Geçici zamanlayıcıyı güncelleştir. Bu, donanım saati tarafından yoksayılabilir.
* **time_ptr** Zaman damgası işaretçisi.
* **packet_ptr** Paket işaretçisi.
* **callback_data** Donuk geri çağırma verileri işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri
* Işlem başarıyla **NX_SUCCESS** (0x00)
* **NX_PTP_PARAM_ERROR** (0xd03) geçersiz parametre

### <a name="allowed-from"></a>İzin verilen
PTP iç

### <a name="example"></a>Örnek
```C/* Create the PTP client instance */
status = nx_ptp_client_create(&ptp_client, &ip_0, 0, &pool_0, 
                              PTP_THREAD_PRIORITY, (UCHAR *)ptp_stack, sizeof(ptp_stack),
                              nx_ptp_client_soft_clock_callback, NX_NULL);

/* If the client was successfully created, status = NX_SUCCESS. */
```

## <a name="nx_ptp_client_start"></a>nx_ptp_client_start

PTP Client 'ı başlatın.

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

### <a name="description"></a>Açıklama
Bu hizmet daha önce oluşturulmuş bir PTP istemci örneğini başlatır.

### <a name="input-parameters"></a>Giriş Parametreleri
* **client_ptr** Oluşturulacak PTP Client işaretçisi
* **client_port_identity_ptr** İstemci bağlantı noktası ve kimlik işaretçisi, NULL olabilir
* **client_port_identity_length** İstemci bağlantı noktası ve kimlik uzunluğu. Client_port_identity_ptr NULL veya NX_PTP_CLOCK_PORT_IDENTITY_SIZE (10) ise 0 olmalıdır
* **etki alanı** PTP saat etki alanı
* **transport_specific** 4 bit aktarıma özgü
* **event_callback** Geri çağırma işlevi olayda çağrıldı
* **event_callback_data** Olay geri çağırması için veriler

### <a name="return-values"></a>Dönüş Değerleri
* **NX_SUCCESS** (0x00) istemci başarıyla başlatıldı
* **NX_PTP_CLIENT_ALREADY_STARTED** (0xd02) MTP istemcisi zaten başlatılmış
* **durum** NetX Duo ve ThreadX hizmeti çağrılarının durum bitimi
* NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi

### <a name="allowed-from"></a>İzin verilen
İş Parçacıkları

### <a name="example"></a>Örnek
```C
status = nx_ptp_client_start(&ptp_client, NX_NULL, 0, 0, 0, ptp_event_callback, NX_NULL);

/* If the client was successfully started, status = NX_SUCCESS. */
```

## <a name="nx_ptp_client_stop"></a>nx_ptp_client_stop

PTP Client 'ı durdurun.  PTP Client durdurulduktan sonra, PTP paketlerini işlemez veya PTP paketlerini iletmez.

### <a name="prototype"></a>Prototype

```C
UINT nx_ptp_client_stop(NX_PTP_CLIENT *client_ptr);
```

### <a name="description"></a>Açıklama
Bu hizmet daha önce oluşturulmuş ve başlatılmış bir PTP istemci örneğini durduruyor.

### <a name="input-parameters"></a>Giriş Parametreleri
* **client_ptr** Durdurulacak PTP Client işaretçisi

### <a name="return-values"></a>Dönüş Değerleri
* **NX_SUCCESS** (0x00) istemci başarıyla durduruldu
* **NX_PTP_CLIENT_NOT_STARTED** (0xd01) istemci başlatılmadı
* NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi

### <a name="allowed-from"></a>İzin verilen
İş Parçacıkları

### <a name="example"></a>Örnek
```C
status = nx_ptp_client_stop(&ptp_client);

/* If the client was successfully stopped, status = NX_SUCCESS. */
```

## <a name="nx_ptp_client_sync_info_get"></a>nx_ptp_client_sync_info_get

Eşitleme bilgilerini alın.

### <a name="prototype"></a>Prototype

```C
UINT nx_ptp_client_sync_info_get(
    NX_PTP_CLIENT_SYNC *sync_ptr, 
    USHORT *flags, 
    SHORT *utc_offset);
```

### <a name="description"></a>Açıklama
Bu hizmet, eşitleme iletisi bilgilerini alır. Eşitleme denetim bloğu, olay geri çağırma işlevi aracılığıyla kullanıcı uygulamasına geçirilir.

### <a name="input-parameters"></a>Giriş Parametreleri
* **client_ptr** Oluşturulacak PTP Client işaretçisi
* **bayraklar** Eşitleme iletisindeki bayraklar
* **utc_offset** Day ile UTC arasındaki fark

### <a name="return-values"></a>Dönüş Değerleri
* **NX_SUCCESS** (0x00) eşitleme bilgilerini başarıyla alın
* NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi

### <a name="allowed-from"></a>İzin verilen
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

### <a name="description"></a>Açıklama
Bu hizmet, PTP saatinin geçerli değerini alır. Her ne zaman bir PTP istemcisi ana saatle eşitlenmez.

### <a name="input-parameters"></a>Giriş Parametreleri
* **client_ptr** Oluşturulacak PTP Client işaretçisi
* **time_ptr** PTP saati işaretçisi

### <a name="return-values"></a>Dönüş Değerleri
* **NX_SUCCESS** (0x00) istemci başarıyla oluşturuldu
* NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi

### <a name="allowed-from"></a>İzin verilen
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

### <a name="description"></a>Açıklama
Bu hizmet, PTP saatinin geçerli değerini ayarlar. PTP Client başlamadan önce çağrılması gerekir.

### <a name="input-parameters"></a>Giriş Parametreleri
* **client_ptr** Oluşturulacak PTP Client işaretçisi
* **time_ptr** PTP saati işaretçisi

### <a name="return-values"></a>Dönüş Değerleri
* **NX_SUCCESS** (0x00) istemci başarıyla oluşturuldu
* **NX_PTP_CLIENT_ALREADY_STARTED** (0xd02) MTP istemcisi zaten başlatılmış
* NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi

### <a name="allowed-from"></a>İzin verilen
İş Parçacıkları

### <a name="example"></a>Örnek
```C
/* Set current time before PTP client started.  */
status = nx_ptp_client_time_set(&ptp_client, &tm);
```

## <a name="nx_ptp_client_utility_convert_time_to_date"></a>nx_ptp_client_utility_convert_time_to_date

PTP Time saatini UTC Tarih ve saatine dönüştürür.

### <a name="prototype"></a>Prototype

```C
UINT nx_ptp_client_utility_convert_time_to_date(
    NX_PTP_TIME *time_ptr, 
    LONG offset, 
    NX_PTP_DATE_TIME *date_time_ptr);
```

### <a name="description"></a>Açıklama
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

### <a name="description"></a>Açıklama
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