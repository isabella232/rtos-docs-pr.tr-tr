---
title: Bölüm 11-olay izleme arabelleğinin biçimi
description: ThreadX tüm Azure RTOS ThreadX Hizmetleri, iş parçacığı durumu değişiklikleri ve Kullanıcı tanımlı olaylar için yerleşik olay izleme desteği sağlar.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: d11b827558e9c96df44f462329b7807a500a64a4
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104827575"
---
# <a name="chapter-11---format-of-event-trace-buffer"></a>Bölüm 11-olay izleme arabelleğinin biçimi

Azure RTOS ThreadX, tüm ThreadX Hizmetleri, iş parçacığı durumu değişiklikleri ve Kullanıcı tanımlı olaylar için yerleşik olay izleme desteği sağlar. Olay izlemeyi kullanmak için, tanımlanan **TX_ENABLE_EVENT_TRACE** Ile Threadx, NETX ve FileX kitaplıklarını oluşturmanız ve **_tx_trace_enable_** işlevini çağırarak izlemeyi etkinleştirmeniz yeterlidir. Bu bölümde bu işlem açıklanmaktadır.

## <a name="event-trace-format"></a>Olay Izleme biçimi

ThreadX olay izleme arabelleğinin biçimi üç bölüme bölünür, yani denetim üstbilgisi, nesne kayıt defteri ve izleme girdileri. Aşağıdaki, ThreadX olay izleme arabelleğinin genel yerleşimini anlatmaktadır:

**Denetim üst bilgisi**

**Nesne kayıt defteri girdisi 0**

**…**

**"N" nesne kayıt girdisi**

**Olay Izleme girdisi 0**

**…**

**Olay Izleme girdisi "n"**

### <a name="event-trace-control-header"></a>Olay Izleme denetim üst bilgisi

Denetim üst bilgisi, olay izleme arabelleğinin tam yerleşimini tanımlar. Bu, kaç tane ThreadX nesnesinin kaydedilebileceği ve kaç olay kaydedilebildiği de dahildir. Ayrıca, denetim üst bilgisi, izleme arabelleği öğelerinin nerede olduğunu tanımlar. Aşağıdaki veri yapısı denetim üstbilgisini tanımlar:

```c
typedef struct TX_TRACE_CONTROL_HEADER_STRUCT
{
    ULONG    tx_trace_control_header_id;
    ULONG    tx_trace_control_header_timer_valid_mask;
    ULONG    tx_trace_control_header_trace_base_address;
    ULONG    tx_trace_control_header_object_registry_start_pointer;
    USHORT   tx_trace_control_header_reserved1;
    USHORT   tx_trace_control_header_object_registry_name_size;
    ULONG    tx_trace_control_header_object_registry_end_pointer;
    ULONG    tx_trace_control_header_buffer_start_pointer;
    ULONG    tx_trace_control_header_buffer_end_pointer;
    ULONG    tx_trace_control_header_buffer_current_pointer;
    ULONG    tx_trace_control_header_reserved2;
    ULONG    tx_trace_control_header_reserved3;
    ULONG    tx_trace_control_header_reserved4;
} TX_TRACE_CONTROL_HEADER;
```

### <a name="control-header-id"></a>Denetim üst bilgi KIMLIĞI

Denetim üst bilgisi KIMLIĞI, 0x54585442 olan 32 bitlik ONALTıLı değerden oluşur ve bu da ***ASCII karakterlerine karşılık*** gelir. Bu değer 32 bitlik işaretsiz bir değişken olarak yazıldığı için, olay izleme arabelleğinin bitiliğini algılamak için de kullanılabilir. Örneğin, belleğin ilk dört bEvet değeri 0x54, 0x58, 0x54, 0x42 ise, olay izleme arabelleği big endian biçimde yazılmıştır. Aksi takdirde, olay izleme arabelleği little endian biçimde yazılmıştır.

### <a name="timer-valid-mask"></a>Süreölçer geçerli maskesi

Süreölçer geçerli maskesi, gerçek olay izleme girişlerinde kaç tane zaman damgasının geçerli olduğunu tanımlar. Örneğin, zaman damgası kaynağı 16 bit içeriyorsa, bu alandaki değer 0xFFFF olmalıdır. 32 bitlik bir zaman damgası kaynağı 0xFFFFFFFF değerine sahip olacaktır. Bu değer _ *_tx_port. h_* * içinde ***TX_TRACE_TIME_MASK** _ sabiti tarafından tanımlanır.

### <a name="trace-base-address"></a>İzleme temel adresi

İzleme arabelleği temel adresi, ***tx_trace_enable*** çağrısında izleme arabelleğinin başlangıcı olarak belirtilen uygulamanın adresidir. Bu adres, arabellekteki çeşitli öğeler için buffergöreli uzaklıklar türetmede analiz aracının tek kullanımı için korunur. Örneğin, izleme arabelleğindeki geçerli olayın arabellek göreli kayması, geçerli olay adresinden temel adresin basit çıkarma işlemi tarafından hesaplanır.

### <a name="registry-start-and-end-pointers"></a>Kayıt defteri başlangıç ve bitiş Işaretçileri

Kayıt defteri Başlangıç işaretçisi, ilk nesne kayıt defteri girdisinin adresini işaret ederken, kayıt defteri bitiş işaretçisi, e-mesajlaşma adresini gösterir. Son kayıt girişini takip/mediately. Bu değerler *tx_trace_enable* işleme sırasında kurulumlardır ve izleme süresi boyunca değiştirilmez.

### <a name="registry-name-size"></a>Kayıt defteri adı boyutu

Kayıt defteri adı boyutu, kayıt defteri girdisindeki her bir nesne adı için bayt cinsinden en büyük boyutu tanımlar ve ***TX_TRACE_OBJECT_REGISTRY_NAME** _ simgesiyle tanımlanır. Varsayılan değer 32 ' dir ve _*_tx_trace. h_*_' de tanımlanmıştır. Nesne adı, nesne oluşturulduğunda uygulama tarafından verilen ada karşılık gelir. Örneğin, bir iş parçacığının nesne kayıt defteri adı, uygulama tarafından _ *_tx_thread_create_* * çağrısı için sağlanan addır.

### <a name="buffer-start-and-end-pointers"></a>Arabellek başlangıç ve bitiş Işaretçileri

Olay izleme arabelleği Başlangıç işaretçisi, ilk izleme girişinin adresini işaret ederken, kayıt defteri bitiş işaretçisi, e-mesajlaşma adresini gösterir. son izleme girişini takip eden/mediately. Bu değerler, ***tx_trace_enable</*** işleme sırasında kurulumlardır ve izleme süresince değiştirilmez.

### <a name="current-buffer-pointer"></a>Geçerli arabellek Işaretçisi

Olay izleme arabelleği geçerli işaretçisi, en eski izleme girişinin adresini gösterir. İzleme girişleri döngüsel bir listede tutulduğundan, geçerli arabellek işaretçisi yazılacak sonraki izleme girişini de temsil eder. |

## <a name="event-trace-object-registry"></a>Olay Izleme nesnesi kayıt defteri

Olay izleme nesnesi kayıt defteri, uygulama tarafından oluşturulan nesnelere karşılık gelen ***n** _ nesne kayıt defteri girdilerini içerir. Nesne kayıt defterinin ana amacı, gerçek nesne adlarını izleme arabelleği girdilerinin nesne adresleriyle ilişkilendirmek için dış analiz araçlarına yöneliktir. Kayıt defteri girdilerinin sayısı, uygulama tarafından _ *_tx_trace_enable_** çağrısında belirtilir.

Her nesne kayıt girdisi, daha önce uygulama tarafından oluşturulan belirli bir ThreadX nesnesi hakkında bilgiler içerir. Aşağıdaki veri yapısı her nesne kayıt defteri girişini tanımlar:

```c
typedef struct TX_TRACE_OBJECT_REGISTRY_ENTRY_STRUCT
{
    UCHAR    tx_trace_object_registry_entry_object_available**;
    UCHAR    tx_trace_object_registry_entry_object_type**;
    UCHAR    tx_trace_object_registry_entry_object_reserved1;
    UCHAR    tx_trace_object_registry_entry_object_reserved2;
    ULONG    tx_trace_thread_registry_entry_object_pointer;
    ULONG    tx_trace_object_registry_entry_object_parameter_1;
    ULONG    tx_trace_object_registry_entry_object_parameter_2;
    UCHAR    tx_trace_thread_registry_entry_object_name[TX_TRACE_OBJECT_REGISTRY_NAME];

} TX_TRACE_OBJECT_REGISTRY_ENTRY;
```

### <a name="object-available-flag"></a>Nesne kullanılabilir bayrağı

Nesne kayıt defteri girişi varsa, nesne kullanılabilir bayrağı 1 olarak ayarlanır. Aksi takdirde, değer 1 değilse, nesne kayıt defteri girişi kullanılamaz. Girişin kullanılabilir olmasına rağmen yine de geçerli bilgiler içerebileceğini unutmayın.

### <a name="object-entry-type"></a>Nesne giriş türü

Nesne giriş türü, bu girişte nesnenin türünü tanımlar. Geçerli nesne türlerinin listesi aşağıda verilmiştir:

| **Değer** | **Nesne türü** |
|---------- | --------------- |
| 0         | Geçerli değil       |
| 1         | İş Parçacığı          |
| 2         | Zamanlayıcı |
| 3         | Kuyruk |
| 4         | Semafor |
| 5         | Mutex |
| 6         | Olay bayrakları grubu |
| 7         | Blok havuzu |
| 8         | Bayt havuzu |
| 9         | .. /Medya |
| 10        | Dosya |
| 11        | IP |
| 12        | Paket havuzu |
| 13        | TCP yuvası |
| 14        | UDP yuvası |
| 15-20     | Ayrılmıştır |  
| 21        | USB ana bilgisayar yığını cihazı |
| 22        | USB ana bilgisayar yığını arabirimi |
| 23        | USB ana bilgisayar uç noktası |
| 24        | USB ana bilgisayar sınıfı |
| 25        | USB cihazı |
| 26        | USB cihaz arabirimi |
| 27        | USB cihaz uç noktası |
| 28        | USB cihaz sınıfı |

### <a name="object-pointer"></a>Nesne Işaretçisi

Nesne işaretçisi, ThreadX API kullanarak nesneye erişmek için kullanılan nesne adresini belirtir.

### <a name="object-reserved-fields"></a>Nesne ayrılmış alanları

İş parçacıkları dışındaki tüm nesneler için, bu ayrılmış alanlar 0 olmalıdır. İş parçacıkları için, kayıt defterine girildiği sırada iş parçacığının önceliği, bu iki ayrılmış alana yerleştirilir.

### <a name="object-parameters"></a>Nesne parametreleri

Nesne parametreleri, nesne hakkında ek bilgiler içerir. Aşağıda her bir ThreadX nesnesi için ek bilgiler açıklanmaktadır:

| **Nesne türü**        | **Parametre 1**  | **Parametre 2** |
|----------------------- | ---------------- | --------------- |
| İş Parçacığı                 | Yığın başlangıcı      | Yığın boyutu |
| Zamanlayıcı                  | İlk ticks | Yeniden zamanlama Işaretleri |
| Kuyruk                  | Sıra boyutu | İleti boyutu |
| Semafor              | İlk örnekler | - |
| Mutex                  | Devralma bayrağı | - |
| Olay bayrakları grubu      | - | - |
| Blok havuzu             | Toplam blok sayısı | Blok Boyutu |
| Bayt havuzu              | Toplam bayt sayısı | - |
| .. /Medya                  | FAT önbellek boyutu | Kesim önbelleği boyutu |
| Dosya                   | - | - |
| IP                     | Yığın başlangıcı | Yığın boyutu |
| Paket havuzu            | Paket boyutu | Paket sayısı |
| TCP yuvası             | IP Adresi | Pencere boyutu |
| UDP yuvası             | IP Adresi | RX kuyruğu en yüksek |

### <a name="object-name"></a>Nesne adı

Nesne adı ThreadX nesnesinin adını içerir. Ad, nesne oluşturulduğu sırada ThreadX için girilen addır. Varsayılan olarak, nesne adının en fazla 32 karakter vardır. 32 karakterden büyük gerçek adlar kesilir.

## <a name="event-trace-entries"></a>Olay Izleme girdileri

Olay izleme girişleri, olay izleme arabelleğinin alt bölümünde bulunur. Girdiler, geçerli giriş işaretçisiyle en eski girişi işaret eden bir dairesel listede tutulur. Listedeki giriş sayısı ***tx_trace_enable*** çağrısıyla hesaplanır.

Her nesne kayıt girişi, belirli bir ThreadX izleme olayı hakkında bilgiler içerir. Aşağıdaki veri yapısı her izleme olayı girişini tanımlar:

```c
typedef struct TX_TRACE_BUFFER_ENTRY_STRUCT
{
    ULONG     tx_trace_buffer_entry_thread_pointer;
    ULONG     tx_trace_buffer_entry_thread_priority;
    ULONG     tx_trace_buffer_entry_event_id;
    ULONG     tx_trace_buffer_entry_time_stamp;
    ULONG     tx_trace_buffer_entry_information_field_1;
    ULONG     tx_trace_buffer_entry_information_field_2;
    ULONG     tx_trace_buffer_entry_information_field_3;
    ULONG     tx_trace_buffer_entry_information_field_4;
} TX_TRACE_BUFFER_ENTRY;
```

### <a name="thread-pointer"></a>İş parçacığı Işaretçisi

İş parçacığı işaretçisi, bu olay sırasında çalışan iş parçacığının adresini içerir. Başlatma sırasında olay oluştuysa (çalışan iş parçacığı yoksa), Bu işaretçinin değeri 0xF0F0F0F0 ' dır. Bir kesme hizmeti yordamı (ıSR) sırasında olay oluştuysa, Bu işaretçinin değeri 0xFFFFFFFF ' dir. Giriş henüz kullanılmıyorsa, Bu işaretçinin değeri 0 ' dır.

### <a name="thread-priority"></a>İş parçacığı önceliği

İş parçacığı öncelik alanı, bu olay sırasında çalışan iş parçacığının iş parçacığı önceliğini ve önalım eşiğini içerir. Bir kesme bağlamı varsa (iş parçacığı işaretçisi 0xFFFFFFFF), bu alanın değeri öncelik değildir ancak olay sırasında ***_tx_thread_current_ptr*** değeri olur. Aksi takdirde, bu alanın değeri 0 ' dır.

### <a name="event-id"></a>Olay Kimliği

Olay KIMLIĞI, gerçekleşen olayı belirtir. Geçerli ThreadX Trace olay kimlikleri 1 ila 1024 arasındadır. 1025 ve üzeri sürümlerde başlayan değerler kullanıcıya özgü olaylar için ayrılmıştır. Lütfen ThreadX olay kimliklerinin tamamının tanımının ***tx_trace. h*** dosyasına bakın.</td>

### <a name="information-fields-1-4"></a>Bilgi alanları (1-4)

Bilgi alanları, belirli olayla ilgili ek bilgiler içerir. Tanımlı ThreadX olay kimliklerinin her biri için bilgi alanlarının tamamının açıklaması için lütfen ***tx_trace. h*** dosyasına bakın.