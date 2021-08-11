---
title: Bölüm 5-izleme arabellekleri oluşturma
description: Bu bölümde, bir Azure RTOS TraceX olay arabelleğinin nasıl oluşturulacağı ve ayrıca arabelleğin temel biçimi açıklanmaktadır.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: 7d5c90675728fc7e374d625f5a9ae27340268ca8398200c68fb7113a84aa2983
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116801796"
---
# <a name="chapter-5---generating-trace-buffers"></a>Bölüm 5-izleme arabellekleri oluşturma

Bu bölümde, bir Azure RTOS TraceX olay arabelleğinin nasıl oluşturulacağı ve ayrıca arabelleğin temel biçimi açıklanmaktadır.

## <a name="threadx-event-trace-support"></a>ThreadX olay Izleme desteği

ThreadX tüm ThreadX Hizmetleri, iş parçacığı durumu değişiklikleri ve Kullanıcı tanımlı olaylar için yerleşik olay izleme desteği sağlar. ThreadX olay-izleme özelliği öncelikle uygulamadaki son "n" etkinliklerini çözümlemek üzere bir sonrası aracı olarak tasarlanmıştır. Bu bilgilerden, geliştirici sorunları ve/veya en iyi duruma getirme hedeflerini gösterebilir.

TraceX, ThreadX tarafından oluşturulan olay izleme arabelleğini grafik olarak görüntüler. Aşağıda, arabelleğin nasıl oluşturulacağı ve arabelleğin temel biçiminin nasıl kullanılacağı açıklanmaktadır.

## <a name="enabling-event-trace"></a>Olay Izlemeyi etkinleştirme

Olay izlemeyi etkinleştirmek için zaman damgası sabitlerini tanımlayın, **TX_ENABLE_EVENT_TRACE** tanımlı olan threadx kitaplığını derleyin ve **tx_trace_enable** işlevini çağırarak izlemeyi etkinleştirin.

## <a name="defining-time-stamp-constants"></a>Time-Stamp sabitleri tanımlama

Zaman damgası sabitleri, olay izleme girişlerinde kullanılan zaman damgası üzerinde geliştirici denetimi sağlamak üzere tasarlanmıştır. İki zaman damgası sabiti ve varsayılan değerleri aşağıdaki gibidir:

```c
#ifndef TX_TRACE_TIME_SOURCE
#define TX_TRACE_TIME_SOURCE ++_tx_trace_simulated_time
#endif
#ifndef TX_TRACE_TIME_MASK
#define TX_TRACE_TIME_MASK   0xFFFFFFFFUL
#endif
```

Yukarıdaki sabitler **tx_port. h** içinde tanımlanmıştır ve her bir olay üzerinde yalnızca bir tane tarafından artan bir "sahte" zaman damgası oluşturur. Aşağıda gerçek bir zaman damgası tanımına bir örnek verilmiştir:

```c
#ifndef TX_TRACE_TIME_SOURCE
#define TX_TRACE_TIME_SOURCE ((ULONG) 0x0x13000004)
#endif
#ifndef TX_TRACE_TIME_MASK
#define TX_TRACE_TIME_MASK 0xFFFFFFFFUL
#endif
```

Yukarıdaki sabitler, 0x13000004 adresini okuyarak elde edilen 32 bitlik bir süreölçer belirtir. Uygulamaya özgü çoğu zaman damgalarının benzer bir biçimde kurulması gerekir.

## <a name="exporting-the-trace-buffer"></a>Izleme arabelleğini dışarı aktarma

Trackingex, konakta bir ikili, Intel ONALTıLıK veya Motorola S-kayıt dosyası biçiminde izleme arabelleği gerektirir. Bunu yapmanın en kolay yolu, hedefi durdurmaktır ve hata ayıklayıcıyı, ***tx_trace_enable*** işlevi için sağladığınız bellek alanının konaktaki bir dosyaya dökümünü almak için yönlendirir.

> [!WARNING]
>***Bir izleme toplama kodunun içinde hedefi durdurmamaya dikkat edin. Bunun yapılması geçersiz izleme bilgilerine neden olabilir. Program ThreadX içinde durdurulmuşsa, izleme arabelleğinin dökümünü yapmadan önce herhangi bir izleme makrosunu bir araya adımla.***

> [!IMPORTANT]
> *Ek D, izleme arabelleğinin çeşitli geliştirme araçları içinden nasıl dökümünü gösterir.*

## <a name="extended-event-trace-api"></a>Genişletilmiş olay Izleme API 'SI

ThreadX, tanımlı **TX_ENABLE_EVENT_TRACE** ile oluşturulduğunda, uygulama için aşağıdaki yeni olay Izleme API 'leri kullanılabilir:

- tx_trace_enable: *olay Izlemeyi etkinleştir*
- tx_trace_event_filter: *belirtilen olayları filtrele*
- tx_trace_event_unfilter: *belirtilen olayların filtreleneceğini kaldır*
- tx_trace_disable: *olay Izlemeyi devre dışı bırak*
- tx_trace_isr_enter_insert: *ISR ekleme Trace olayını girin*
- tx_trace_isr_exit_insert: *ISR çıkış izleme olayını Ekle*
- tx_trace_buffer_full_notify: *kayıt izleme arabelleği tam uygulama geri çağırması*
- tx_trace_user_event_insert: *Kullanıcı olayı Ekle*

### <a name="tx_trace_enable"></a>tx_trace_enable

Olay izlemeyi etkinleştir

#### <a name="prototype"></a>Prototype

```c
UINT tx_trace_enable (VOID *trace_buffer_start,
     ULONG trace_buffer_size, ULONG registry_entries);
```

#### <a name="description"></a>Description
Bu hizmet, ThreadX içinde olay izlemeye izin vermez. İzleme arabelleği ve en fazla ThreadX nesnesi sayısı uygulama tarafından sağlanır.

> [!IMPORTANT]
> Etkinlik izlemeyi kullanabilmek için ThreadX kitaplığı ve uygulaması tanımlanmış **TX_ENABLE_EVENT_TRACE** oluşturulmalıdır.

#### <a name="input-parameters"></a>Giriş Parametreleri

- **trace_buffer_start**: Kullanıcı tarafından sağlanan izleme arabelleğinin başlangıcına yönelik işaretçi.
- **trace_buffer_size**: izleme arabelleği için bellekteki toplam bayt sayısı. İzleme arabelleğinin daha büyük olması, depolayabileceği daha fazla giriş olur.
- **registry_entries**: izleme kayıt defterinde tutulacak uygulama threadx nesnelerinin sayısı. Kayıt defteri nesne adreslerini nesne adlarıyla ilişkilendirmek için kullanılır. Bu, GUI izleme çözümleme araçları için oldukça kullanışlıdır.

#### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı olay izleme etkin.
- **TX_SIZE_ERROR** (0x05) belirtilen izleme arabelleği boyutu çok küçük. Bu, izleme üst bilgisi, nesne kayıt defteri ve en az bir izleme girdisi için yeterince büyük olmalıdır.
- **TX_NOT_DONE** (0x20) olay izleme zaten etkin.
- **TX_FEATURE_NOT_ENABLED** (0xFF) sistem izleme etkin ile derlenmedi.

#### <a name="allowed-from"></a>İzin verilen

Başlatma ve iş parçacıkları

#### <a name="example"></a>Örnek

```c
UCHAR my_trace_buffer[64000];

/* Enable event tracing using the global "my_trace_buffer" memory and supporting a maximum of 30 ThreadX objects in the registry. */
status = tx_trace_enable (&my_trace_buffer, 64000, 30);

/* If status is TX_SUCCESS the event tracing is enabled. */
```

#### <a name="see-also"></a>Ayrıca Bkz.

tx_trace_event_filter, tx_trace_event_unfilter, tx_trace_disable, tx_trace_isr_enter_insert, tx_trace_isr_exit_insert, tx_trace_buffer_full_notify, tx_trace_user_event_insert

### <a name="tx_trace_event_filter"></a>tx_trace_event_filter

Belirtilen olayları filtrele

#### <a name="prototype"></a>Prototype

```c
UINT tx_trace_event_filter (ULONG  vent_filter_bits);
```

#### <a name="description"></a>Description

Bu hizmet, belirtilen olayların etkin izleme arabelleğine eklenmesini, filtre uygular. Varsayılan olarak, *tx_trace_enable* çağrıldıktan sonra hiçbir olay filtrelenmediğini unutmayın.

> [!IMPORTANT]
> Etkinlik izlemeyi kullanabilmek için ThreadX kitaplığı ve uygulaması tanımlanmış **TX_ENABLE_EVENT_TRACE** oluşturulmalıdır.

#### <a name="input-parameters"></a>Giriş Parametreleri

- **event_filter_bits**: filtrelenecek olaylara karşılık gelen bitler. Birden çok olay, uygun sabitleri bir araya getirerek filtrelenebilir. Bu değişken için geçerli sabitler aşağıdaki gibi tanımlanır:

```c
TX_TRACE_ALL_EVENTS                   0x000007FF
TX_TRACE_INTERNAL_EVENTS              0x00000001
TX_TRACE_BLOCK_POOL_EVENTS            0x00000002
TX_TRACE_BYTE_POOL_EVENTS             0x00000004
TX_TRACE_EVENT_FLAGS_EVENTS           0x00000008
TX_TRACE_INTERRUPT_CONTROL_EVENT      0x00000010
TX_TRACE_MUTEX_EVENTS                 0x00000020
TX_TRACE_QUEUE_EVENTS                 0x00000040
TX_TRACE_SEMAPHORE_EVENTS             0x00000080
TX_TRACE_THREAD_EVENTS                0x00000100
TX_TRACE_TIME_EVENTS                  0x00000200
TX_TRACE_TIMER_EVENTS                 0x00000400
FX_TRACE_ALL_EVENTS                   0x00007800
FX_TRACE_INTERNAL_EVENTS              0x00000800
FX_TRACE_MEDIA_EVENTS                 0x00001000
FX_TRACE_DIRECTORY_EVENTS             0x00002000
FX_TRACE_FILE_EVENTS                  0x00004000
NX_TRACE_ALL_EVENTS                   0x00FF8000
NX_TRACE_INTERNAL_EVENTS              0x00008000
NX_TRACE_ARP_EVENTS                   0x00010000
NX_TRACE_ICMP_EVENTS                  0x00020000
NX_TRACE_IGMP_EVENTS                  0x00040000
NX_TRACE_IP_EVENTS                    0x00080000
NX_TRACE_PACKET_EVENTS                0x00100000
NX_TRACE_RARP_EVENTS                  0x00200000
NX_TRACE_TCP_EVENTS                   0x00400000
NX_TRACE_UDP_EVENTS                   0x00800000
UX_TRACE_ALL_EVENTS                   0x7F000000
UX_TRACE_ERRORS                       0x01000000
UX_TRACE_HOST_STACK_EVENTS            0x02000000
UX_TRACE_DEVICE_STACK_EVENTS          0x04000000
UX_TRACE_HOST_CONTROLLER_EVENTS       0x08000000
UX_TRACE_DEVICE_CONTROLLER_EVENTS     0x10000000
UX_TRACE_HOST_CLASS_EVENTS            0x20000000
UX_TRACE_DEVICE_CLASS_EVENTS          0x40000000
```

#### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı olay filtresi.
- **TX_FEATURE_NOT_ENABLED** (0xFF) sistem izleme etkin ile derlenmedi.

#### <a name="allowed-from"></a>İzin verilen

Başlatma ve iş parçacıkları

#### <a name="example"></a>Örnek

```c
/* Filter queue and byte pool events from trace buffer. */

status = tx_trace_event_filter (TX_TRACE_QUEUE_EVENTS | TX_TRACE_BYTE_POOL_EVENTS);

/* If status is TX_SUCCESS all queue and byte pool events are filtered. */
```

#### <a name="see-also"></a>Ayrıca Bkz.

tx_trace_enable, tx_trace_event_unfilter, tx_trace_disable, tx_trace_isr_enter_insert, tx_trace_isr_exit_insert, tx_trace_buffer_full_notify, tx_trace_user_event_insert

### <a name="tx_trace_event_unfilter"></a>tx_trace_event_unfilter

Belirtilen olayların filtreleneceğini kaldır

#### <a name="prototype"></a>Prototype

```c
UINT tx_trace_event_unfilter (ULONG event_unfilter_bits);
```

#### <a name="description"></a>Description

Bu hizmet, belirtilen olayların (ler) etkin izleme arabelleğine eklenecekleri şekilde filtreleyeceğini kaldırır.

> [!IMPORTANT]
> Etkinlik izlemeyi kullanabilmek için ThreadX kitaplığı ve uygulaması tanımlanmış **TX_ENABLE_EVENT_TRACE** oluşturulmalıdır.

#### <a name="input-parameters"></a>Giriş Parametreleri

- **event_unfilter_bits**: filtreyi kaldırmak için olaylara karşılık gelen bitler. Birden çok olaya, uygun sabitler yalnızca bir araya getirerek filtrelenebilir. Bu değişken için geçerli sabitler aşağıdaki gibi tanımlanır:

```c
TX_TRACE_ALL_EVENTS                  0x000007FF
TX_TRACE_INTERNAL_EVENTS             0x00000001
TX_TRACE_BLOCK_POOL_EVENTS           0x00000002
TX_TRACE_BYTE_POOL_EVENTS            0x00000004
TX_TRACE_EVENT_FLAGS_EVENTS          0x00000008
TX_TRACE_INTERRUPT_CONTROL_EVENT     0x00000010
TX_TRACE_MUTEX_EVENTS                0x00000020
TX_TRACE_QUEUE_EVENTS                0x00000040
TX_TRACE_SEMAPHORE_EVENTS            0x00000080
TX_TRACE_THREAD_EVENTS               0x00000100
TX_TRACE_TIME_EVENTS                 0x00000200
TX_TRACE_TIMER_EVENTS                0x00000400
FX_TRACE_ALL_EVENTS                  0x00007800
FX_TRACE_INTERNAL_EVENTS             0x00000800
FX_TRACE_MEDIA_EVENTS                0x00001000
FX_TRACE_DIRECTORY_EVENTS            0x00002000
FX_TRACE_FILE_EVENTS                 0x00004000
NX_TRACE_ALL_EVENTS                  0x00FF8000
NX_TRACE_INTERNAL_EVENTS             0x00008000
NX_TRACE_ARP_EVENTS                  0x00010000
NX_TRACE_ICMP_EVENTS                 0x00020000
NX_TRACE_IGMP_EVENTS                 0x00040000
NX_TRACE_IP_EVENTS                   0x00080000
NX_TRACE_PACKET_EVENTS               0x00100000
NX_TRACE_RARP_EVENTS                 0x00200000
NX_TRACE_TCP_EVENTS                  0x00400000
NX_TRACE_UDP_EVENTS                  0x00800000
UX_TRACE_ALL_EVENTS                  0x7F000000
UX_TRACE_ERRORS                      0x01000000
UX_TRACE_HOST_STACK_EVENTS           0x02000000
UX_TRACE_DEVICE_STACK_EVENTS         0x04000000
UX_TRACE_HOST_CONTROLLER_EVENTS      0x08000000
UX_TRACE_DEVICE_CONTROLLER_EVENTS    0x10000000
UX_TRACE_HOST_CLASS_EVENTS           0x20000000
UX_TRACE_DEVICE_CLASS_EVENTS         0x40000000
```

#### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı olay unfilter.
- **TX_FEATURE_NOT_ENABLED** (0xFF) sistem izleme etkin ile derlenmedi.

#### <a name="allowed-from"></a>İzin verilen

Başlatma ve iş parçacıkları

#### <a name="example"></a>Örnek

```c
/* Un-filter queue and byte pool events from trace buffer. */ 
status = 
  tx_trace_event_unfilter (TX_TRACE_QUEUE_EVENTS | TX_TRACE_BYTE_POOL_EVENTS);

/* If status is TX_SUCCESS all queue and byte pool events are un-filtered. */
```

#### <a name="see-also"></a>Ayrıca Bkz.

tx_trace_enable, tx_trace_event_filter, tx_trace_disable, tx_trace_isr_enter_insert, tx_trace_isr_exit_insert, tx_trace_buffer_full_notify, tx_trace_user_event_insert

### <a name="tx_trace_disable"></a>tx_trace_disable

#### <a name="disable-event-tracing"></a>Olay izlemeyi devre dışı bırak

#### <a name="prototype"></a>Prototype

```c
UINT tx_trace_disable (VOID);
```

#### <a name="description"></a>Description

Bu hizmet, ThreadX içindeki olay izlemeyi devre dışı bırakır. Bu, uygulamanın geçerli olay izleme arabelleğini dondurmak ve muhtemelen çalışma zamanı sırasında dışarıdan aktarımı istiyorsa yararlı olabilir. Devre dışı bırakıldıktan sonra, yeniden izlemeye başlamak için **tx_trace_enable** çağrılabilir.

> [!IMPORTANT]
> Etkinlik izlemeyi kullanabilmek için ThreadX kitaplığı ve uygulaması tanımlanmış **TX_ENABLE_EVENT_TRACE** oluşturulmalıdır.

#### <a name="input-parameters"></a>Giriş Parametreleri

Yok.

#### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı olay izleme devre dışı.
- **TX_NOT_DONE** (0x20) olay izleme etkin değildi.
- **TX_FEATURE_NOT_ENABLED** (0xFF) sistem izleme etkin ile derlenmedi.

#### <a name="allowed-from"></a>İzin verilen

Başlatma ve iş parçacıkları

#### <a name="example"></a>Örnek 

```c
/* Disable event tracing. */ 
status = tx_trace_disable ();

/* If status is TX_SUCCESS the event tracing is disabled. */
```

#### <a name="see-also"></a>Ayrıca Bkz.

tx_trace_enable, tx_trace_event_filter, tx_trace_event_unfilter, tx_trace_isr_enter_insert, tx_trace_isr_exit_insert, tx_trace_buffer_full_notify, tx_trace_user_event_insert

### <a name="tx_trace_isr_enter_insert"></a>tx_trace_isr_enter_insert

#### <a name="insert-isr-enter-event"></a>ISR Enter olayı Ekle

#### <a name="prototype"></a>Prototype

```c
VOID tx_trace_isr_enter_insert (ULONG isr_id);
```

#### <a name="description"></a>Description

Bu hizmet, hata izleme arabelleğine ıSR ENTER olayını ekler. Bu, ıSR işlemenin başlangıcında uygulama tarafından çağrılmalıdır. Sağlanan parametre, uygulamaya yönelik belirli bir ıSR 'yi tanımlamalıdır.

> [!IMPORTANT]
> Etkinlik izlemeyi kullanabilmek için ThreadX kitaplığı ve uygulaması tanımlanmış **TX_ENABLE_EVENT_TRACE** oluşturulmalıdır.

#### <a name="input-parameters"></a>Giriş Parametreleri 
- **isr_id**: ISR 'yi tanımlayacak uygulamaya özgü değer.

#### <a name="return-values"></a>Dönüş Değerleri

**Hiçbiri**

#### <a name="allowed-from"></a>İzin verilen 

ISRs

#### <a name="example"></a>Örnek

```c
/* Insert trace event to identify the application's ISR with an ID of 3. */

status = tx_trace_isr_enter_insert (3);

/* If status is TX_SUCCESS the ISR entry event was inserted. */
```

#### <a name="see-also"></a>Ayrıca Bkz.

tx_trace_enable, tx_trace_event_filter, tx_trace_event_unfilter, tx_trace_disable, tx_trace_isr_exit_insert, tx_trace_buffer_full_notify, tx_trace_user_event_insert

### <a name="tx_trace_isr_exit_insert"></a>tx_trace_isr_exit_insert

#### <a name="insert-isr-exit-event"></a>ISR çıkış olayı Ekle

#### <a name="prototype"></a>Prototype

```c
VOID tx_trace_isr_exit_insert (ULONG isr_id);
```

#### <a name="description"></a>Description

Bu hizmet, hata izleme arabelleğine ıSR girişi olayını ekler. Bu, ıSR işlemenin başlangıcında uygulama tarafından çağrılmalıdır. Sağlanan parametre, uygulamanın ıSR 'sini tanımlamalıdır.

> [!IMPORTANT]
> Etkinlik izlemeyi kullanabilmek için ThreadX kitaplığı ve uygulaması tanımlanmış **TX_ENABLE_EVENT_TRACE** oluşturulmalıdır.

#### <a name="input-parameters"></a>Giriş Parametreleri 

- **isr_id**: ISR 'yi tanımlayacak uygulamaya özgü değer.

#### <a name="return-values"></a>Dönüş Değerleri

**Hiçbiri**

#### <a name="allowed-from"></a>İzin verilen

ISRs

#### <a name="example"></a>Örnek

```c
/* Insert trace event to identify the application's ISR with an ID of 3. */ 

status = tx_trace_isr_exit_insert (3);

/* If status is TX_SUCCESS the ISR exit event was inserted. */
```

#### <a name="see-also"></a>Ayrıca Bkz.

tx_trace_enable, tx_trace_event_filter, tx_trace_event_unfilter, tx_trace_disable, tx_trace_isr_enter_insert, tx_trace_buffer_full_notify, tx_trace_user_event_insert

### <a name="tx_trace_buffer_full_notify"></a>tx_trace_buffer_full_notify

#### <a name="register-trace-buffer-full-application-callback"></a>İzleme arabelleği tam uygulama geri aramasını Kaydet

#### <a name="prototype"></a>Prototype

```c
VOID tx_trace_buffer_full_notify (VOID (*full_buffer_callback)(VOID *));
```

#### <a name="description"></a>Description

Bu hizmet, izleme arabelleği dolduğunda ThreadX tarafından çağrılan bir uygulama geri çağırma işlevini kaydeder. Uygulama daha sonra izlemeyi devre dışı bırakmayı ve/veya büyük olasılıkla yeni bir izleme arabelleği kurulumunu seçebilir.

> [!IMPORTANT]
> Etkinlik izlemeyi kullanabilmek için ThreadX kitaplığı ve uygulaması tanımlanmış **TX_ENABLE_EVENT_TRACE** oluşturulmalıdır.

#### <a name="input-parameters"></a>Giriş Parametreleri

- **full_buffer_callback**: izleme arabelleği dolduğunda çağrılacak uygulama işlevi. NULL değeri, bildirim geri aramasını devre dışı bırakır.

#### <a name="return-values"></a>Dönüş Değerleri

**Hiçbiri**

#### <a name="allowed-from"></a>İzin verilen

ISRs

#### <a name="example"></a>Örnek

```c
y_trace_is_full(void *trace_buffer_start)

{

     /* Application specific processing goes here! */

}

/* Register the "my_trace_is_full" function to be called whenever the trace buffer fills. */

status = tx_trace_buffer_full_notify (my_trace_is_full);

/* If status is TX_SUCCESS the "my_trace_is_full" function is registered. */
```

#### <a name="see-also"></a>Ayrıca Bkz.

tx_trace_enable, tx_trace_event_filter, tx_trace_event_unfilter, tx_trace_disable, tx_trace_isr_enter_insert, tx_trace_isr_exit_insert, tx_trace_user_event_insert

### <a name="tx_trace_user_event_insert"></a>tx_trace_user_event_insert

#### <a name="insert-user-event"></a>Kullanıcı olayı Ekle

#### <a name="prototype"></a>Prototype

```c
UINT tx_trace_user_event_insert (ULONG event_id, 
   ULONG info_field_1, ULONG info_field_2,
   ULONG info_field_3, ULONG info_field_4);
```

#### <a name="description"></a>Description

Bu hizmet, Kullanıcı olayını izleme arabelleğine ekler. Kullanıcı olay kimlikleri 4096 olarak tanımlanan sabit **TX_TRACE_USER_EVENT_START** daha büyük olmalıdır. En fazla Kullanıcı olayı, 65535 olarak tanımlanan sabit **TX_TRACE_USER_EVENT_END** tarafından tanımlanır. Bu aralıktaki tüm olaylar uygulama için kullanılabilir. Bilgi alanları uygulamaya özeldir.

> [!IMPORTANT]
> Etkinlik izlemeyi kullanabilmek için ThreadX kitaplığı ve uygulaması tanımlanmış **TX_ENABLE_EVENT_TRACE** oluşturulmalıdır.

#### <a name="input-parameters"></a>Giriş Parametreleri

- **event_id**: uygulamaya özgü olay kimliği ve **TX_TRACE_USER_EVENT_START** sıfırdan büyük ve **TX_TRACE_USER_EVENT_END** küçük ya da buna eşit olmalıdır.
- **info_field_1**: uygulamaya özgü bilgi alanı.
- **info_field_2**: uygulamaya özgü bilgi alanı.
- **info_field_3**: uygulamaya özgü bilgi alanı.
- **info_field_4**: uygulamaya özgü bilgi alanı.

#### <a name="return-values"></a>Dönüş Değerleri
- **TX_SUCCESS** (0x00) başarılı Kullanıcı olayı ekleme.
- **TX_NOT_DONE** (0x20) olay izleme etkin değil.
- **TX_FEATURE_NOT_ENABLED** (0xFF) sistem izleme etkin ile derlenmedi.

#### <a name="allowed-from"></a>İzin verilen

Başlatma ve iş parçacıkları

#### <a name="example"></a>Örnek

```c
/* Insert user event 3000, with info fields of 1, 2, 3, 4. */ 

status = tx_trace_user_event_insert (3000, 1, 2, 3, 4);

/* If status is TX_SUCCESS the user event was inserted. */
```

#### <a name="see-also"></a>Ayrıca Bkz.

tx_trace_enable, tx_trace_event_filter, tx_trace_event_unfilter, tx_trace_disable, tx_trace_isr_enter_insert, tx_trace_isr_exit_insert, tx_trace_buffer_full_notify