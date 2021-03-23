---
title: Bölüm 1-Azure RTOS NetX Duo MTP Istemcisine giriş
description: Bu bölümde, Azure RTOS NetX Duo MTP Istemcisine giriş yer almaktadır.
author: v-condav
ms.author: v-condav
ms.date: 01/27/2021
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 5beec64bd6d74e3bed06be15255d6bd4a940ba64
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825805"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-ptp-client"></a>Bölüm 1-Azure RTOS NetX Duo MTP Istemcisine giriş

Azure RTOS NetX Duo PTP, Precision Time Protocol (PTP) sürüm 2 ' nin (IEEE 1588-2008) istemci bölümünü uygular. IPv4 veya IPv6 çok noktaya yayın paketleri aracılığıyla birbirleriyle iletişim kurarak yerel ağdaki mus 'Lar arasındaki saatleri eşleştirmek için kullanılır.

## <a name="netx-duo-ptp-client-setup"></a>NetX Duo PTP Istemci kurulumu

Doğru çalışması için, PTP istemci paketi bir NetX Duo IP örneğinin zaten oluşturulmuş olmasını gerektirir.

Varsayılan olarak, PTP istemcisi IPv4 çok noktaya yayın grubunu birleştirir. PTP Client 'ı bir IPv6 ağında çalıştırmak için, `NX_ENABLE_IPV6_MULTICAST` NetX Duo kitaplığı oluşturulurken tanımlanması gerekir.

PTP istemcisini oluştururken, uygulamanın gelen ve giden paketlerin zaman damgalarını işlemek için bir geri çağırma işlevi sağlaması gerekir. Yüksek çözünürlüğe ulaşmak için uygulamaların yüksek çözünürlüklü bir Zamanlayıcı kullanarak zaman damgası oluşturmasını öneririz. PTP on simülatörünü çalıştırmak için, yazılım tabanlı bir uygulama `nx_ptp_client_soft_clock_callback` sağlanır.

PTP Client, PTP iletileri iletmek için bir paket havuzu gerektirir. Paket havuzunun yük boyutu `NX_UDP_PACKET + NX_PTP_CLIENT_PACKET_DATA_SIZE` , IPv4 için 108 bayt ve IPv6 etkinse 128 bayt olmalıdır.

PTP Istemcisini oluşturduktan sonra uygulama, PTP istemcisini başlatabilir. Eşitleme, PTP Yardımcısı iş parçacığında yapılır. Olay geri çağırma işlevi belirtilebilir. Aşağıdaki olaylardan herhangi biri gerçekleştiğinde çağrılacaktır.
* Ana öğe seçildi; 
* Süre ayarlanır.
* Ana zaman aşımı.

## <a name="netx-duo-ptp-client-messages"></a>NetX Duo PTP Istemci Iletileri

NetX Duo MTP istemcisi yalnızca gecikmeli istek-yanıt mekanizmasını uygular. PTP istemcisi iki UDP bağlantı noktasını açar. *319* **olay** iletisi için ve **genel** ileti için *320* . Bu mekanizma için beş tür ileti vardır.

* **Duyurur**. Bu bir olay iletisidir. Ana saat seçimi için kullanılır.
* **Eşitleme**. Bu bir olay iletisidir. Kaynak zaman damgası göndermek ve ana sunucudan istemciye yol gecikmesini hesaplamak için kullanılır.
* **Follow_Up**. Bu, genel bir iletidir. Bu, isteğe bağlıdır ve ilgili eşitleme iletisindeki kaynak zaman damgasını düzeltmek için kullanılır. Yalnızca eşitleme bayrağıyla birlikte iki adımlı bit ayarlandığında gönderilir.
* **Delay_Req**. Bu bir olay iletisidir. Delay_Resp alma sırasında istemciden ana kadar yol gecikmesini hesaplamak için PTP istemcisinden gönderilir.
* **Delay_Resp**. Bu bir olay iletisidir. İstemciden istemciye yol gecikmesini hesaplamak için ana sunucudan istemciye gönderilir.

*Not, "en iyi ana saat" algoritması uygulanmadı. PTP istemcisi dinleme durumundayken yalnızca ilk ana saat kabul edilir.*

## <a name="netx-duo-ptp-client-clock-callback"></a>NetX Duo PTP Istemci saati geri araması
Saati ana sunucudan eşleştirmek için, PTP istemcisinin yerel bir saat olması gerekir. Bir saat geri çağırma işlevi, oluşturma sırasında PTP Client 'a geçirilir. Saat geri çağırma yordamının biçimi aşağıda tanımlanmıştır.
```C
UINT ptp_clock_callback(
    NX_PTP_CLIENT *client_ptr, 
    UINT operation,
    NX_PTP_TIME *time_ptr, 
    NX_PACKET *packet_ptr,
    VOID *callback_data);
```
Giriş parametreleri aşağıdaki gibi tanımlanır:
* *client_ptr* , PTP istemcisine işaret eder.
* *işlem* , geri çağırma işlemini belirtir; geçerli değerler aşağıdaki listede gösterildiği gibi tanımlanır.
  * **NX_PTP_CLIENT_CLOCK_INIT** Saati başlatın.
  * **NX_PTP_CLIENT_CLOCK_SET** Tarafından belirtilen geçerli zaman damgasını ayarla `time_ptr` .
  * **NX_PTP_CLIENT_CLOCK_GET** Geçerli zaman damgasını döndürür `time_ptr` .
  * **NX_PTP_CLIENT_CLOCK_PACKET_TS_EXTRACT** Zaman damgasını konumundan `packet_ptr` ayıklayın `time_ptr` .
  * **NX_PTP_CLIENT_CLOCK_ADJUST** Geçerli zaman damgasını *1* saniyeden az ayarlayın.
  * **NX_PTP_CLIENT_CLOCK_PACKET_TS_PREPARE** `packet_ptr` PTP Client ' ın aktarıldığı zaman damgasına bildirilmesini gerektiren öğesini işaretleyin.
  * **NX_PTP_CLIENT_CLOCK_SOFT_TIMER_UPDATE** Geçici zamanlayıcıyı güncelleştir. Bu, donanım saati tarafından yoksayılabilir.
* *time_ptr* zaman damgasına işaret eder.
* *packet_ptr* pakete işaret eder.
* *callback_data* , opak geri çağırma verilerine işaret eder.

NX_PTP_TIME veri türü aşağıdaki gibi tanımlanır.
```C
typedef struct NX_PTP_TIME_STRUCT
{
    /* The MSB of the number of seconds */
    LONG  second_high;

    /* The LSB of the number of seconds */
    ULONG second_low;

    /* The number of nanoseconds */
    LONG  nanosecond;
} NX_PTP_TIME;
```

## <a name="netx-duo-ptp-client-event-callback"></a>NetX Duo PTP Istemci olayı geri çağırması
Olay geri çağırma işlevi, uygulamayı MTP istemcisinin durumuna bildirmek için ayarlanabilir. Olay geri çağırma yordamının biçimi aşağıda gösterildiği gibi tanımlanmıştır.
```C
UINT event_callback(
    NX_PTP_CLIENT *client_ptr, 
    UINT event, 
    VOID *event_data, 
    VOID *callback_data);
```
Giriş parametreleri.
* *client_ptr* , PTP istemcisine işaret eder.
* *olay* , geri çağırma olayını belirtir, geçerli değerler şu şekilde tanımlanır:
  * **NX_PTP_CLIENT_EVENT_MASTER** Ana saat seçilidir.
  * **NX_PTP_CLIENT_EVENT_SYNC** PTP Client kalibre edilir.
  * **NX_PTP_CLIENT_EVENT_TIMEOUT** Ana saat zaman aşımı.
* *event_data* olayla ilgili verileri belirtir. Olay **NX_PTP_CLIENT_EVENT_MASTER** olduğunda, event_data örneğe işaret eder `NX_PTP_CLIENT_MASTER` . Olay **NX_PTP_CLIENT_EVENT_SYNC** olduğunda, olay verileri örneğe işaret eder `NX_PTP_CLIENT_SYNC` .

## <a name="netx-duo-ptp-client-communication"></a>NetX Duo PTP Istemci Iletişimi
Daha önce de belirtildiği gibi, NetX Duo MTP istemcisi yalnızca gecikmeli istek-yanıt mekanizmasını destekler. Bu mekanizma, istemci ile ana saat arasındaki ortalama yol gecikmesini aşağıda gösterildiği gibi ölçer:
1. İstemci ana bilgisayardan *duyuru* iletisi alır ve en iyi ana öğe olarak seçer.
1. İstemci, ana bilgisayardan *eşitleme* iletisi alır. *T1* zaman damgası, bu iletideki kaynak zaman damgasıdır. Bu ileti alındığında *T2* zaman damgası olarak yerel saatten okundu.
1. İstemci ana bilgisayardan *Follow_Up* ileti alır. Bu ileti isteğe bağlıdır ve yalnızca iki adım *eşitleme* bayrağıyla ayarlandığında geçerlidir. Sonra zaman damgası *T1* , bu iletideki kaynak zaman damgasına güncelleştirilir.
1. İstemci ana sunucuya *Delay_Req* ileti gönderir. İleti aktarıldığında *T3* zaman damgası yerel saatten okunurdur.
1. İstemci ana bilgisayardan *Delay_Resp* ileti alır. *T4* zaman damgası bu iletideki alma zaman damgasıdır.

Ortalama yol gecikmesi aşağıda gösterildiği gibi hesaplanır.
```C
<meanPathDelay>=[(t2-t1)+(t4-t3)]/2
```
Ana sunucudan gelen fark aşağıda gösterildiği gibi hesaplanır.
```C
<offsetFromMaster>=client_clock-master_clock
                  =(t2-t1)-<meanPathDelay>
```

> [!NOTE]
> ***CorrectionField** _, Calculation._ sırasında yok sayılır