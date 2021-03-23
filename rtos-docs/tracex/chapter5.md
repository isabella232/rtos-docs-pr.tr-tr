---
title: Bölüm 5-izleme arabellekleri oluşturma
description: Bu bölümde, bir Azure RTOS TraceX olay arabelleğinin nasıl oluşturulacağı ve ayrıca arabelleğin temel biçimi açıklanmaktadır.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: f296137d23b9f3c1c4fd115947bb50a32b768123
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104827521"
---
# <a name="chapter-5---generating-trace-buffers"></a><span data-ttu-id="0c724-103">Bölüm 5-izleme arabellekleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="0c724-103">Chapter 5 - Generating trace buffers</span></span>

<span data-ttu-id="0c724-104">Bu bölümde, bir Azure RTOS TraceX olay arabelleğinin nasıl oluşturulacağı ve ayrıca arabelleğin temel biçimi açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="0c724-104">This chapter contains a description about how to build a Azure RTOS TraceX event buffer and also describes the underlying format of the buffer.</span></span>

## <a name="threadx-event-trace-support"></a><span data-ttu-id="0c724-105">ThreadX olay Izleme desteği</span><span class="sxs-lookup"><span data-stu-id="0c724-105">ThreadX Event Trace Support</span></span>

<span data-ttu-id="0c724-106">ThreadX tüm ThreadX Hizmetleri, iş parçacığı durumu değişiklikleri ve Kullanıcı tanımlı olaylar için yerleşik olay izleme desteği sağlar.</span><span class="sxs-lookup"><span data-stu-id="0c724-106">ThreadX provides built-in event trace support for all ThreadX services, thread state changes, and user-defined events.</span></span> <span data-ttu-id="0c724-107">ThreadX olay-izleme özelliği öncelikle uygulamadaki son "n" etkinliklerini çözümlemek üzere bir sonrası aracı olarak tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="0c724-107">The ThreadX event-trace capability is primarily designed as a post-mortem tool to analyze the last "n" activities in the application.</span></span> <span data-ttu-id="0c724-108">Bu bilgilerden, geliştirici sorunları ve/veya en iyi duruma getirme hedeflerini gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="0c724-108">From this information, the developer may spot problems and/or potential targets of optimization.</span></span>

<span data-ttu-id="0c724-109">TraceX, ThreadX tarafından oluşturulan olay izleme arabelleğini grafik olarak görüntüler.</span><span class="sxs-lookup"><span data-stu-id="0c724-109">TraceX graphically displays the event trace buffer built by ThreadX.</span></span> <span data-ttu-id="0c724-110">Aşağıda, arabelleğin nasıl oluşturulacağı ve arabelleğin temel biçiminin nasıl kullanılacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="0c724-110">The following describes how to build the buffer and describes the underlying format of the buffer.</span></span>

## <a name="enabling-event-trace"></a><span data-ttu-id="0c724-111">Olay Izlemeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="0c724-111">Enabling Event Trace</span></span>

<span data-ttu-id="0c724-112">Olay izlemeyi etkinleştirmek için zaman damgası sabitlerini tanımlayın, **TX_ENABLE_EVENT_TRACE** tanımlı olan threadx kitaplığını derleyin ve **tx_trace_enable** işlevini çağırarak izlemeyi etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="0c724-112">To enable event trace, define the time-stamp constants, build the ThreadX library with **TX_ENABLE_EVENT_TRACE** defined, and enable tracing by calling the **tx_trace_enable** function.</span></span>

## <a name="defining-time-stamp-constants"></a><span data-ttu-id="0c724-113">Time-Stamp sabitleri tanımlama</span><span class="sxs-lookup"><span data-stu-id="0c724-113">Defining Time-Stamp Constants</span></span>

<span data-ttu-id="0c724-114">Zaman damgası sabitleri, olay izleme girişlerinde kullanılan zaman damgası üzerinde geliştirici denetimi sağlamak üzere tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="0c724-114">The time-stamp constants are designed to provide the developer control over the time-stamp used in the event trace entries.</span></span> <span data-ttu-id="0c724-115">İki zaman damgası sabiti ve varsayılan değerleri aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="0c724-115">The two time-stamp constants and their default values are as follows:</span></span>

```c
#ifndef TX_TRACE_TIME_SOURCE
#define TX_TRACE_TIME_SOURCE ++_tx_trace_simulated_time
#endif
#ifndef TX_TRACE_TIME_MASK
#define TX_TRACE_TIME_MASK   0xFFFFFFFFUL
#endif
```

<span data-ttu-id="0c724-116">Yukarıdaki sabitler **tx_port. h** içinde tanımlanmıştır ve her bir olay üzerinde yalnızca bir tane tarafından artan bir "sahte" zaman damgası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0c724-116">The above constants are defined in **tx_port.h** and create a "fake" time-stamp that simply increments by one on each event.</span></span> <span data-ttu-id="0c724-117">Aşağıda gerçek bir zaman damgası tanımına bir örnek verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="0c724-117">The following is an example of an actual timestamp definition:</span></span>

```c
#ifndef TX_TRACE_TIME_SOURCE
#define TX_TRACE_TIME_SOURCE ((ULONG) 0x0x13000004)
#endif
#ifndef TX_TRACE_TIME_MASK
#define TX_TRACE_TIME_MASK 0xFFFFFFFFUL
#endif
```

<span data-ttu-id="0c724-118">Yukarıdaki sabitler, 0x13000004 adresini okuyarak elde edilen 32 bitlik bir süreölçer belirtir.</span><span class="sxs-lookup"><span data-stu-id="0c724-118">The above constants specify a 32-bit timer that is obtained by reading the address 0x13000004.</span></span> <span data-ttu-id="0c724-119">Uygulamaya özgü çoğu zaman damgalarının benzer bir biçimde kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0c724-119">Most application specific time-stamps should be setup in a similar fashion.</span></span>

## <a name="exporting-the-trace-buffer"></a><span data-ttu-id="0c724-120">Izleme arabelleğini dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="0c724-120">Exporting the Trace Buffer</span></span>

<span data-ttu-id="0c724-121">Trackingex, konakta bir ikili, Intel ONALTıLıK veya Motorola S-kayıt dosyası biçiminde izleme arabelleği gerektirir.</span><span class="sxs-lookup"><span data-stu-id="0c724-121">TraceX needs the trace buffer in a binary, Intel HEX, or Motorola S-Record file format on the host.</span></span> <span data-ttu-id="0c724-122">Bunu yapmanın en kolay yolu, hedefi durdurmaktır ve hata ayıklayıcıyı, ***tx_trace_enable*** işlevi için sağladığınız bellek alanının konaktaki bir dosyaya dökümünü almak için yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="0c724-122">The easiest way to accomplish this is to stop the target and instruct your debugger to dump the memory area you supplied to ***tx_trace_enable*** function into a file on the host.</span></span>

> [!WARNING]
><span data-ttu-id="0c724-123">***Bir izleme toplama kodunun içinde hedefi durdurmamaya dikkat edin. Bunun yapılması geçersiz izleme bilgilerine neden olabilir. Program ThreadX içinde durdurulmuşsa, izleme arabelleğinin dökümünü yapmadan önce herhangi bir izleme makrosunu bir araya adımla.***</span><span class="sxs-lookup"><span data-stu-id="0c724-123">***Be careful not to stop the target within a trace gathering code itself. Doing so can cause invalid trace information. If the program is halted within ThreadX, it is best to step over any trace insert macro before dumping the trace buffer.***</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0c724-124">*Ek D, izleme arabelleğinin çeşitli geliştirme araçları içinden nasıl dökümünü gösterir.*</span><span class="sxs-lookup"><span data-stu-id="0c724-124">*Appendix D shows how to dump the trace buffer from within a variety of development tools.*</span></span>

## <a name="extended-event-trace-api"></a><span data-ttu-id="0c724-125">Genişletilmiş olay Izleme API 'SI</span><span class="sxs-lookup"><span data-stu-id="0c724-125">Extended Event Trace API</span></span>

<span data-ttu-id="0c724-126">ThreadX, tanımlı **TX_ENABLE_EVENT_TRACE** ile oluşturulduğunda, uygulama için aşağıdaki yeni olay Izleme API 'leri kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="0c724-126">When ThreadX is built with **TX_ENABLE_EVENT_TRACE** defined, the following new event trace APIs are available to the application:</span></span>

- <span data-ttu-id="0c724-127">tx_trace_enable: *olay Izlemeyi etkinleştir*</span><span class="sxs-lookup"><span data-stu-id="0c724-127">tx_trace_enable: *Enable event tracing*</span></span>
- <span data-ttu-id="0c724-128">tx_trace_event_filter: *belirtilen olayları filtrele*</span><span class="sxs-lookup"><span data-stu-id="0c724-128">tx_trace_event_filter: *Filter specified event(s)*</span></span>
- <span data-ttu-id="0c724-129">tx_trace_event_unfilter: *belirtilen olayların filtreleneceğini kaldır*</span><span class="sxs-lookup"><span data-stu-id="0c724-129">tx_trace_event_unfilter: *Unfilter specified event(s)*</span></span>
- <span data-ttu-id="0c724-130">tx_trace_disable: *olay Izlemeyi devre dışı bırak*</span><span class="sxs-lookup"><span data-stu-id="0c724-130">tx_trace_disable: *Disable event tracing*</span></span>
- <span data-ttu-id="0c724-131">tx_trace_isr_enter_insert: *ISR ekleme Trace olayını girin*</span><span class="sxs-lookup"><span data-stu-id="0c724-131">tx_trace_isr_enter_insert: *Insert ISR enter trace event*</span></span>
- <span data-ttu-id="0c724-132">tx_trace_isr_exit_insert: *ISR çıkış izleme olayını Ekle*</span><span class="sxs-lookup"><span data-stu-id="0c724-132">tx_trace_isr_exit_insert: *Insert ISR exit trace event*</span></span>
- <span data-ttu-id="0c724-133">tx_trace_buffer_full_notify: *kayıt izleme arabelleği tam uygulama geri çağırması*</span><span class="sxs-lookup"><span data-stu-id="0c724-133">tx_trace_buffer_full_notify: *Register trace buffer full application callback*</span></span>
- <span data-ttu-id="0c724-134">tx_trace_user_event_insert: *Kullanıcı olayı Ekle*</span><span class="sxs-lookup"><span data-stu-id="0c724-134">tx_trace_user_event_insert: *Insert user event*</span></span>

### <a name="tx_trace_enable"></a><span data-ttu-id="0c724-135">tx_trace_enable</span><span class="sxs-lookup"><span data-stu-id="0c724-135">tx_trace_enable</span></span>

<span data-ttu-id="0c724-136">Olay izlemeyi etkinleştir</span><span class="sxs-lookup"><span data-stu-id="0c724-136">Enable event tracing</span></span>

#### <a name="prototype"></a><span data-ttu-id="0c724-137">Prototype</span><span class="sxs-lookup"><span data-stu-id="0c724-137">Prototype</span></span>

```c
UINT tx_trace_enable (VOID *trace_buffer_start,
     ULONG trace_buffer_size, ULONG registry_entries);
```

#### <a name="description"></a><span data-ttu-id="0c724-138">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0c724-138">Description</span></span>
<span data-ttu-id="0c724-139">Bu hizmet, ThreadX içinde olay izlemeye izin vermez.</span><span class="sxs-lookup"><span data-stu-id="0c724-139">This service enables event tracing inside ThreadX.</span></span> <span data-ttu-id="0c724-140">İzleme arabelleği ve en fazla ThreadX nesnesi sayısı uygulama tarafından sağlanır.</span><span class="sxs-lookup"><span data-stu-id="0c724-140">The trace buffer and the maximum number of ThreadX objects are supplied by the application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0c724-141">Etkinlik izlemeyi kullanabilmek için ThreadX kitaplığı ve uygulaması tanımlanmış **TX_ENABLE_EVENT_TRACE** oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0c724-141">The ThreadX library and application must be built with **TX_ENABLE_EVENT_TRACE** defined in order to use event tracing.</span></span>

#### <a name="input-parameters"></a><span data-ttu-id="0c724-142">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="0c724-142">Input Parameters</span></span>

- <span data-ttu-id="0c724-143">**trace_buffer_start**: Kullanıcı tarafından sağlanan izleme arabelleğinin başlangıcına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="0c724-143">**trace_buffer_start**: Pointer to the start of the user-supplied trace buffer.</span></span>
- <span data-ttu-id="0c724-144">**trace_buffer_size**: izleme arabelleği için bellekteki toplam bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="0c724-144">**trace_buffer_size**: Total number of bytes in the memory for the trace buffer.</span></span> <span data-ttu-id="0c724-145">İzleme arabelleğinin daha büyük olması, depolayabileceği daha fazla giriş olur.</span><span class="sxs-lookup"><span data-stu-id="0c724-145">The larger the trace buffer, the more entries it is able to store.</span></span>
- <span data-ttu-id="0c724-146">**registry_entries**: izleme kayıt defterinde tutulacak uygulama threadx nesnelerinin sayısı.</span><span class="sxs-lookup"><span data-stu-id="0c724-146">**registry_entries**: Number of application ThreadX objects to keep in the trace registry.</span></span> <span data-ttu-id="0c724-147">Kayıt defteri nesne adreslerini nesne adlarıyla ilişkilendirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0c724-147">The registry is used to correlate object addresses with object names.</span></span> <span data-ttu-id="0c724-148">Bu, GUI izleme çözümleme araçları için oldukça kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="0c724-148">This is highly useful for GUI trace analysis tools.</span></span>

#### <a name="return-values"></a><span data-ttu-id="0c724-149">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="0c724-149">Return Values</span></span>

- <span data-ttu-id="0c724-150">**TX_SUCCESS** (0x00) başarılı olay izleme etkin.</span><span class="sxs-lookup"><span data-stu-id="0c724-150">**TX_SUCCESS** (0x00) Successful event trace enable.</span></span>
- <span data-ttu-id="0c724-151">**TX_SIZE_ERROR** (0x05) belirtilen izleme arabelleği boyutu çok küçük.</span><span class="sxs-lookup"><span data-stu-id="0c724-151">**TX_SIZE_ERROR** (0x05) Specified trace buffer size is too small.</span></span> <span data-ttu-id="0c724-152">Bu, izleme üst bilgisi, nesne kayıt defteri ve en az bir izleme girdisi için yeterince büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0c724-152">It must be large enough for the trace header, the object registry, and at least one trace entry.</span></span>
- <span data-ttu-id="0c724-153">**TX_NOT_DONE** (0x20) olay izleme zaten etkin.</span><span class="sxs-lookup"><span data-stu-id="0c724-153">**TX_NOT_DONE** (0x20) Event tracing was already enabled.</span></span>
- <span data-ttu-id="0c724-154">**TX_FEATURE_NOT_ENABLED** (0xFF) sistem izleme etkin ile derlenmedi.</span><span class="sxs-lookup"><span data-stu-id="0c724-154">**TX_FEATURE_NOT_ENABLED** (0xFF) System was not compiled with trace enabled.</span></span>

#### <a name="allowed-from"></a><span data-ttu-id="0c724-155">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="0c724-155">Allowed From</span></span>

<span data-ttu-id="0c724-156">Başlatma ve iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="0c724-156">Initialization and threads</span></span>

#### <a name="example"></a><span data-ttu-id="0c724-157">Örnek</span><span class="sxs-lookup"><span data-stu-id="0c724-157">Example</span></span>

```c
UCHAR my_trace_buffer[64000];

/* Enable event tracing using the global "my_trace_buffer" memory and supporting a maximum of 30 ThreadX objects in the registry. */
status = tx_trace_enable (&my_trace_buffer, 64000, 30);

/* If status is TX_SUCCESS the event tracing is enabled. */
```

#### <a name="see-also"></a><span data-ttu-id="0c724-158">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="0c724-158">See Also</span></span>

<span data-ttu-id="0c724-159">tx_trace_event_filter, tx_trace_event_unfilter, tx_trace_disable, tx_trace_isr_enter_insert, tx_trace_isr_exit_insert, tx_trace_buffer_full_notify, tx_trace_user_event_insert</span><span class="sxs-lookup"><span data-stu-id="0c724-159">tx_trace_event_filter, tx_trace_event_unfilter, tx_trace_disable, tx_trace_isr_enter_insert, tx_trace_isr_exit_insert, tx_trace_buffer_full_notify, tx_trace_user_event_insert</span></span>

### <a name="tx_trace_event_filter"></a><span data-ttu-id="0c724-160">tx_trace_event_filter</span><span class="sxs-lookup"><span data-stu-id="0c724-160">tx_trace_event_filter</span></span>

<span data-ttu-id="0c724-161">Belirtilen olayları filtrele</span><span class="sxs-lookup"><span data-stu-id="0c724-161">Filter specified events</span></span>

#### <a name="prototype"></a><span data-ttu-id="0c724-162">Prototype</span><span class="sxs-lookup"><span data-stu-id="0c724-162">Prototype</span></span>

```c
UINT tx_trace_event_filter (ULONG  vent_filter_bits);
```

#### <a name="description"></a><span data-ttu-id="0c724-163">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0c724-163">Description</span></span>

<span data-ttu-id="0c724-164">Bu hizmet, belirtilen olayların etkin izleme arabelleğine eklenmesini, filtre uygular.</span><span class="sxs-lookup"><span data-stu-id="0c724-164">This service filters the specified event(s) from being inserted into the active trace buffer.</span></span> <span data-ttu-id="0c724-165">Varsayılan olarak, *tx_trace_enable* çağrıldıktan sonra hiçbir olay filtrelenmediğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="0c724-165">Note that by default no events are filtered after *tx_trace_enable* is called.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0c724-166">Etkinlik izlemeyi kullanabilmek için ThreadX kitaplığı ve uygulaması tanımlanmış **TX_ENABLE_EVENT_TRACE** oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0c724-166">The ThreadX library and application must be built with **TX_ENABLE_EVENT_TRACE** defined in order to use event tracing.</span></span>

#### <a name="input-parameters"></a><span data-ttu-id="0c724-167">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="0c724-167">Input Parameters</span></span>

- <span data-ttu-id="0c724-168">**event_filter_bits**: filtrelenecek olaylara karşılık gelen bitler.</span><span class="sxs-lookup"><span data-stu-id="0c724-168">**event_filter_bits**: Bits that correspond to events to filter.</span></span> <span data-ttu-id="0c724-169">Birden çok olay, uygun sabitleri bir araya getirerek filtrelenebilir.</span><span class="sxs-lookup"><span data-stu-id="0c724-169">Multiple events may be filtered by simply oring together the appropriate constants.</span></span> <span data-ttu-id="0c724-170">Bu değişken için geçerli sabitler aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="0c724-170">Valid constants for this variable are defined as follows:</span></span>

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

#### <a name="return-values"></a><span data-ttu-id="0c724-171">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="0c724-171">Return Values</span></span>

- <span data-ttu-id="0c724-172">**TX_SUCCESS** (0x00) başarılı olay filtresi.</span><span class="sxs-lookup"><span data-stu-id="0c724-172">**TX_SUCCESS** (0x00) Successful event filter.</span></span>
- <span data-ttu-id="0c724-173">**TX_FEATURE_NOT_ENABLED** (0xFF) sistem izleme etkin ile derlenmedi.</span><span class="sxs-lookup"><span data-stu-id="0c724-173">**TX_FEATURE_NOT_ENABLED** (0xFF) System was not compiled with trace enabled.</span></span>

#### <a name="allowed-from"></a><span data-ttu-id="0c724-174">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="0c724-174">Allowed From</span></span>

<span data-ttu-id="0c724-175">Başlatma ve iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="0c724-175">Initialization and threads</span></span>

#### <a name="example"></a><span data-ttu-id="0c724-176">Örnek</span><span class="sxs-lookup"><span data-stu-id="0c724-176">Example</span></span>

```c
/* Filter queue and byte pool events from trace buffer. */

status = tx_trace_event_filter (TX_TRACE_QUEUE_EVENTS | TX_TRACE_BYTE_POOL_EVENTS);

/* If status is TX_SUCCESS all queue and byte pool events are filtered. */
```

#### <a name="see-also"></a><span data-ttu-id="0c724-177">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="0c724-177">See Also</span></span>

<span data-ttu-id="0c724-178">tx_trace_enable, tx_trace_event_unfilter, tx_trace_disable, tx_trace_isr_enter_insert, tx_trace_isr_exit_insert, tx_trace_buffer_full_notify, tx_trace_user_event_insert</span><span class="sxs-lookup"><span data-stu-id="0c724-178">tx_trace_enable, tx_trace_event_unfilter, tx_trace_disable, tx_trace_isr_enter_insert, tx_trace_isr_exit_insert, tx_trace_buffer_full_notify, tx_trace_user_event_insert</span></span>

### <a name="tx_trace_event_unfilter"></a><span data-ttu-id="0c724-179">tx_trace_event_unfilter</span><span class="sxs-lookup"><span data-stu-id="0c724-179">tx_trace_event_unfilter</span></span>

<span data-ttu-id="0c724-180">Belirtilen olayların filtreleneceğini kaldır</span><span class="sxs-lookup"><span data-stu-id="0c724-180">Unfilter specified events</span></span>

#### <a name="prototype"></a><span data-ttu-id="0c724-181">Prototype</span><span class="sxs-lookup"><span data-stu-id="0c724-181">Prototype</span></span>

```c
UINT tx_trace_event_unfilter (ULONG event_unfilter_bits);
```

#### <a name="description"></a><span data-ttu-id="0c724-182">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0c724-182">Description</span></span>

<span data-ttu-id="0c724-183">Bu hizmet, belirtilen olayların (ler) etkin izleme arabelleğine eklenecekleri şekilde filtreleyeceğini kaldırır.</span><span class="sxs-lookup"><span data-stu-id="0c724-183">This service unfilters the specified event(s) such that they will be inserted into the active trace buffer.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0c724-184">Etkinlik izlemeyi kullanabilmek için ThreadX kitaplığı ve uygulaması tanımlanmış **TX_ENABLE_EVENT_TRACE** oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0c724-184">The ThreadX library and application must be built with **TX_ENABLE_EVENT_TRACE** defined in order to use event tracing.</span></span>

#### <a name="input-parameters"></a><span data-ttu-id="0c724-185">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="0c724-185">Input Parameters</span></span>

- <span data-ttu-id="0c724-186">**event_unfilter_bits**: filtreyi kaldırmak için olaylara karşılık gelen bitler.</span><span class="sxs-lookup"><span data-stu-id="0c724-186">**event_unfilter_bits**: Bits that correspond to events to unfilter.</span></span> <span data-ttu-id="0c724-187">Birden çok olaya, uygun sabitler yalnızca bir araya getirerek filtrelenebilir.</span><span class="sxs-lookup"><span data-stu-id="0c724-187">Multiple events may be unfiltered by simply or-ing together the appropriate constants.</span></span> <span data-ttu-id="0c724-188">Bu değişken için geçerli sabitler aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="0c724-188">Valid constants for this variable are defined as follows:</span></span>

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

#### <a name="return-values"></a><span data-ttu-id="0c724-189">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="0c724-189">Return Values</span></span>

- <span data-ttu-id="0c724-190">**TX_SUCCESS** (0x00) başarılı olay unfilter.</span><span class="sxs-lookup"><span data-stu-id="0c724-190">**TX_SUCCESS** (0x00) Successful event unfilter.</span></span>
- <span data-ttu-id="0c724-191">**TX_FEATURE_NOT_ENABLED** (0xFF) sistem izleme etkin ile derlenmedi.</span><span class="sxs-lookup"><span data-stu-id="0c724-191">**TX_FEATURE_NOT_ENABLED** (0xFF) System was not compiled with trace enabled.</span></span>

#### <a name="allowed-from"></a><span data-ttu-id="0c724-192">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="0c724-192">Allowed From</span></span>

<span data-ttu-id="0c724-193">Başlatma ve iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="0c724-193">Initialization and threads</span></span>

#### <a name="example"></a><span data-ttu-id="0c724-194">Örnek</span><span class="sxs-lookup"><span data-stu-id="0c724-194">Example</span></span>

```c
/* Un-filter queue and byte pool events from trace buffer. */ 
status = 
  tx_trace_event_unfilter (TX_TRACE_QUEUE_EVENTS | TX_TRACE_BYTE_POOL_EVENTS);

/* If status is TX_SUCCESS all queue and byte pool events are un-filtered. */
```

#### <a name="see-also"></a><span data-ttu-id="0c724-195">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="0c724-195">See Also</span></span>

<span data-ttu-id="0c724-196">tx_trace_enable, tx_trace_event_filter, tx_trace_disable, tx_trace_isr_enter_insert, tx_trace_isr_exit_insert, tx_trace_buffer_full_notify, tx_trace_user_event_insert</span><span class="sxs-lookup"><span data-stu-id="0c724-196">tx_trace_enable, tx_trace_event_filter, tx_trace_disable, tx_trace_isr_enter_insert, tx_trace_isr_exit_insert, tx_trace_buffer_full_notify, tx_trace_user_event_insert</span></span>

### <a name="tx_trace_disable"></a><span data-ttu-id="0c724-197">tx_trace_disable</span><span class="sxs-lookup"><span data-stu-id="0c724-197">tx_trace_disable</span></span>

#### <a name="disable-event-tracing"></a><span data-ttu-id="0c724-198">Olay izlemeyi devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="0c724-198">Disable event tracing</span></span>

#### <a name="prototype"></a><span data-ttu-id="0c724-199">Prototype</span><span class="sxs-lookup"><span data-stu-id="0c724-199">Prototype</span></span>

```c
UINT tx_trace_disable (VOID);
```

#### <a name="description"></a><span data-ttu-id="0c724-200">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0c724-200">Description</span></span>

<span data-ttu-id="0c724-201">Bu hizmet, ThreadX içindeki olay izlemeyi devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="0c724-201">This service disables event tracing inside ThreadX.</span></span> <span data-ttu-id="0c724-202">Bu, uygulamanın geçerli olay izleme arabelleğini dondurmak ve muhtemelen çalışma zamanı sırasında dışarıdan aktarımı istiyorsa yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="0c724-202">This can be useful if the application wants to freeze the current event trace buffer and possibly transport it externally during run-time.</span></span> <span data-ttu-id="0c724-203">Devre dışı bırakıldıktan sonra, yeniden izlemeye başlamak için **tx_trace_enable** çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="0c724-203">Once disabled, the **tx_trace_enable** can be called to start tracing again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0c724-204">Etkinlik izlemeyi kullanabilmek için ThreadX kitaplığı ve uygulaması tanımlanmış **TX_ENABLE_EVENT_TRACE** oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0c724-204">The ThreadX library and application must be built with **TX_ENABLE_EVENT_TRACE** defined in order to use event tracing.</span></span>

#### <a name="input-parameters"></a><span data-ttu-id="0c724-205">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="0c724-205">Input Parameters</span></span>

<span data-ttu-id="0c724-206">Yok.</span><span class="sxs-lookup"><span data-stu-id="0c724-206">None.</span></span>

#### <a name="return-values"></a><span data-ttu-id="0c724-207">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="0c724-207">Return Values</span></span>

- <span data-ttu-id="0c724-208">**TX_SUCCESS** (0x00) başarılı olay izleme devre dışı.</span><span class="sxs-lookup"><span data-stu-id="0c724-208">**TX_SUCCESS** (0x00) Successful event trace disable.</span></span>
- <span data-ttu-id="0c724-209">**TX_NOT_DONE** (0x20) olay izleme etkin değildi.</span><span class="sxs-lookup"><span data-stu-id="0c724-209">**TX_NOT_DONE** (0x20) Event tracing was not enabled.</span></span>
- <span data-ttu-id="0c724-210">**TX_FEATURE_NOT_ENABLED** (0xFF) sistem izleme etkin ile derlenmedi.</span><span class="sxs-lookup"><span data-stu-id="0c724-210">**TX_FEATURE_NOT_ENABLED** (0xFF) System was not compiled with trace enabled.</span></span>

#### <a name="allowed-from"></a><span data-ttu-id="0c724-211">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="0c724-211">Allowed From</span></span>

<span data-ttu-id="0c724-212">Başlatma ve iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="0c724-212">Initialization and threads</span></span>

#### <a name="example"></a><span data-ttu-id="0c724-213">Örnek</span><span class="sxs-lookup"><span data-stu-id="0c724-213">Example</span></span> 

```c
/* Disable event tracing. */ 
status = tx_trace_disable ();

/* If status is TX_SUCCESS the event tracing is disabled. */
```

#### <a name="see-also"></a><span data-ttu-id="0c724-214">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="0c724-214">See Also</span></span>

<span data-ttu-id="0c724-215">tx_trace_enable, tx_trace_event_filter, tx_trace_event_unfilter, tx_trace_isr_enter_insert, tx_trace_isr_exit_insert, tx_trace_buffer_full_notify, tx_trace_user_event_insert</span><span class="sxs-lookup"><span data-stu-id="0c724-215">tx_trace_enable, tx_trace_event_filter, tx_trace_event_unfilter, tx_trace_isr_enter_insert, tx_trace_isr_exit_insert, tx_trace_buffer_full_notify, tx_trace_user_event_insert</span></span>

### <a name="tx_trace_isr_enter_insert"></a><span data-ttu-id="0c724-216">tx_trace_isr_enter_insert</span><span class="sxs-lookup"><span data-stu-id="0c724-216">tx_trace_isr_enter_insert</span></span>

#### <a name="insert-isr-enter-event"></a><span data-ttu-id="0c724-217">ISR Enter olayı Ekle</span><span class="sxs-lookup"><span data-stu-id="0c724-217">Insert ISR enter event</span></span>

#### <a name="prototype"></a><span data-ttu-id="0c724-218">Prototype</span><span class="sxs-lookup"><span data-stu-id="0c724-218">Prototype</span></span>

```c
VOID tx_trace_isr_enter_insert (ULONG isr_id);
```

#### <a name="description"></a><span data-ttu-id="0c724-219">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0c724-219">Description</span></span>

<span data-ttu-id="0c724-220">Bu hizmet, hata izleme arabelleğine ıSR ENTER olayını ekler.</span><span class="sxs-lookup"><span data-stu-id="0c724-220">This service inserts the ISR enter event into the event trace buffer.</span></span> <span data-ttu-id="0c724-221">Bu, ıSR işlemenin başlangıcında uygulama tarafından çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0c724-221">It should be called by the application at the beginning of ISR processing.</span></span> <span data-ttu-id="0c724-222">Sağlanan parametre, uygulamaya yönelik belirli bir ıSR 'yi tanımlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="0c724-222">The supplied parameter should identify the specific ISR to the application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0c724-223">Etkinlik izlemeyi kullanabilmek için ThreadX kitaplığı ve uygulaması tanımlanmış **TX_ENABLE_EVENT_TRACE** oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0c724-223">The ThreadX library and application must be built with **TX_ENABLE_EVENT_TRACE** defined in order to use event tracing.</span></span>

#### <a name="input-parameters"></a><span data-ttu-id="0c724-224">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="0c724-224">Input Parameters</span></span> 
- <span data-ttu-id="0c724-225">**isr_id**: ISR 'yi tanımlayacak uygulamaya özgü değer.</span><span class="sxs-lookup"><span data-stu-id="0c724-225">**isr_id**: Application specific value to identify the ISR.</span></span>

#### <a name="return-values"></a><span data-ttu-id="0c724-226">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="0c724-226">Return Values</span></span>

<span data-ttu-id="0c724-227">**Hiçbiri**</span><span class="sxs-lookup"><span data-stu-id="0c724-227">**None**</span></span>

#### <a name="allowed-from"></a><span data-ttu-id="0c724-228">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="0c724-228">Allowed From</span></span> 

<span data-ttu-id="0c724-229">ISRs</span><span class="sxs-lookup"><span data-stu-id="0c724-229">ISRs</span></span>

#### <a name="example"></a><span data-ttu-id="0c724-230">Örnek</span><span class="sxs-lookup"><span data-stu-id="0c724-230">Example</span></span>

```c
/* Insert trace event to identify the application's ISR with an ID of 3. */

status = tx_trace_isr_enter_insert (3);

/* If status is TX_SUCCESS the ISR entry event was inserted. */
```

#### <a name="see-also"></a><span data-ttu-id="0c724-231">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="0c724-231">See Also</span></span>

<span data-ttu-id="0c724-232">tx_trace_enable, tx_trace_event_filter, tx_trace_event_unfilter, tx_trace_disable, tx_trace_isr_exit_insert, tx_trace_buffer_full_notify, tx_trace_user_event_insert</span><span class="sxs-lookup"><span data-stu-id="0c724-232">tx_trace_enable, tx_trace_event_filter, tx_trace_event_unfilter, tx_trace_disable, tx_trace_isr_exit_insert, tx_trace_buffer_full_notify, tx_trace_user_event_insert</span></span>

### <a name="tx_trace_isr_exit_insert"></a><span data-ttu-id="0c724-233">tx_trace_isr_exit_insert</span><span class="sxs-lookup"><span data-stu-id="0c724-233">tx_trace_isr_exit_insert</span></span>

#### <a name="insert-isr-exit-event"></a><span data-ttu-id="0c724-234">ISR çıkış olayı Ekle</span><span class="sxs-lookup"><span data-stu-id="0c724-234">Insert ISR exit event</span></span>

#### <a name="prototype"></a><span data-ttu-id="0c724-235">Prototype</span><span class="sxs-lookup"><span data-stu-id="0c724-235">Prototype</span></span>

```c
VOID tx_trace_isr_exit_insert (ULONG isr_id);
```

#### <a name="description"></a><span data-ttu-id="0c724-236">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0c724-236">Description</span></span>

<span data-ttu-id="0c724-237">Bu hizmet, hata izleme arabelleğine ıSR girişi olayını ekler.</span><span class="sxs-lookup"><span data-stu-id="0c724-237">This service inserts the ISR entry event into the event trace buffer.</span></span> <span data-ttu-id="0c724-238">Bu, ıSR işlemenin başlangıcında uygulama tarafından çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0c724-238">It should be called by the application at the beginning of ISR processing.</span></span> <span data-ttu-id="0c724-239">Sağlanan parametre, uygulamanın ıSR 'sini tanımlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="0c724-239">The supplied parameter should identify the ISR to the application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0c724-240">Etkinlik izlemeyi kullanabilmek için ThreadX kitaplığı ve uygulaması tanımlanmış **TX_ENABLE_EVENT_TRACE** oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0c724-240">The ThreadX library and application must be built with **TX_ENABLE_EVENT_TRACE** defined in order to use event tracing.</span></span>

#### <a name="input-parameters"></a><span data-ttu-id="0c724-241">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="0c724-241">Input Parameters</span></span> 

- <span data-ttu-id="0c724-242">**isr_id**: ISR 'yi tanımlayacak uygulamaya özgü değer.</span><span class="sxs-lookup"><span data-stu-id="0c724-242">**isr_id**: Application specific value to identify the ISR.</span></span>

#### <a name="return-values"></a><span data-ttu-id="0c724-243">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="0c724-243">Return Values</span></span>

<span data-ttu-id="0c724-244">**Hiçbiri**</span><span class="sxs-lookup"><span data-stu-id="0c724-244">**None**</span></span>

#### <a name="allowed-from"></a><span data-ttu-id="0c724-245">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="0c724-245">Allowed From</span></span>

<span data-ttu-id="0c724-246">ISRs</span><span class="sxs-lookup"><span data-stu-id="0c724-246">ISRs</span></span>

#### <a name="example"></a><span data-ttu-id="0c724-247">Örnek</span><span class="sxs-lookup"><span data-stu-id="0c724-247">Example</span></span>

```c
/* Insert trace event to identify the application's ISR with an ID of 3. */ 

status = tx_trace_isr_exit_insert (3);

/* If status is TX_SUCCESS the ISR exit event was inserted. */
```

#### <a name="see-also"></a><span data-ttu-id="0c724-248">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="0c724-248">See Also</span></span>

<span data-ttu-id="0c724-249">tx_trace_enable, tx_trace_event_filter, tx_trace_event_unfilter, tx_trace_disable, tx_trace_isr_enter_insert, tx_trace_buffer_full_notify, tx_trace_user_event_insert</span><span class="sxs-lookup"><span data-stu-id="0c724-249">tx_trace_enable, tx_trace_event_filter, tx_trace_event_unfilter, tx_trace_disable, tx_trace_isr_enter_insert, tx_trace_buffer_full_notify, tx_trace_user_event_insert</span></span>

### <a name="tx_trace_buffer_full_notify"></a><span data-ttu-id="0c724-250">tx_trace_buffer_full_notify</span><span class="sxs-lookup"><span data-stu-id="0c724-250">tx_trace_buffer_full_notify</span></span>

#### <a name="register-trace-buffer-full-application-callback"></a><span data-ttu-id="0c724-251">İzleme arabelleği tam uygulama geri aramasını Kaydet</span><span class="sxs-lookup"><span data-stu-id="0c724-251">Register trace buffer full application callback</span></span>

#### <a name="prototype"></a><span data-ttu-id="0c724-252">Prototype</span><span class="sxs-lookup"><span data-stu-id="0c724-252">Prototype</span></span>

```c
VOID tx_trace_buffer_full_notify (VOID (*full_buffer_callback)(VOID *));
```

#### <a name="description"></a><span data-ttu-id="0c724-253">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0c724-253">Description</span></span>

<span data-ttu-id="0c724-254">Bu hizmet, izleme arabelleği dolduğunda ThreadX tarafından çağrılan bir uygulama geri çağırma işlevini kaydeder.</span><span class="sxs-lookup"><span data-stu-id="0c724-254">This service registers an application callback function that is called by ThreadX when the trace buffer becomes full.</span></span> <span data-ttu-id="0c724-255">Uygulama daha sonra izlemeyi devre dışı bırakmayı ve/veya büyük olasılıkla yeni bir izleme arabelleği kurulumunu seçebilir.</span><span class="sxs-lookup"><span data-stu-id="0c724-255">The application can then choose to disable tracing and/or possibly setup a new trace buffer.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0c724-256">Etkinlik izlemeyi kullanabilmek için ThreadX kitaplığı ve uygulaması tanımlanmış **TX_ENABLE_EVENT_TRACE** oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0c724-256">The ThreadX library and application must be built with **TX_ENABLE_EVENT_TRACE** defined in order to use event tracing.</span></span>

#### <a name="input-parameters"></a><span data-ttu-id="0c724-257">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="0c724-257">Input Parameters</span></span>

- <span data-ttu-id="0c724-258">**full_buffer_callback**: izleme arabelleği dolduğunda çağrılacak uygulama işlevi.</span><span class="sxs-lookup"><span data-stu-id="0c724-258">**full_buffer_callback**: Application function to call when the trace buffer is full.</span></span> <span data-ttu-id="0c724-259">NULL değeri, bildirim geri aramasını devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="0c724-259">A value of NULL disables the notification callback.</span></span>

#### <a name="return-values"></a><span data-ttu-id="0c724-260">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="0c724-260">Return Values</span></span>

<span data-ttu-id="0c724-261">**Hiçbiri**</span><span class="sxs-lookup"><span data-stu-id="0c724-261">**None**</span></span>

#### <a name="allowed-from"></a><span data-ttu-id="0c724-262">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="0c724-262">Allowed From</span></span>

<span data-ttu-id="0c724-263">ISRs</span><span class="sxs-lookup"><span data-stu-id="0c724-263">ISRs</span></span>

#### <a name="example"></a><span data-ttu-id="0c724-264">Örnek</span><span class="sxs-lookup"><span data-stu-id="0c724-264">Example</span></span>

```c
y_trace_is_full(void *trace_buffer_start)

{

     /* Application specific processing goes here! */

}

/* Register the "my_trace_is_full" function to be called whenever the trace buffer fills. */

status = tx_trace_buffer_full_notify (my_trace_is_full);

/* If status is TX_SUCCESS the "my_trace_is_full" function is registered. */
```

#### <a name="see-also"></a><span data-ttu-id="0c724-265">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="0c724-265">See Also</span></span>

<span data-ttu-id="0c724-266">tx_trace_enable, tx_trace_event_filter, tx_trace_event_unfilter, tx_trace_disable, tx_trace_isr_enter_insert, tx_trace_isr_exit_insert, tx_trace_user_event_insert</span><span class="sxs-lookup"><span data-stu-id="0c724-266">tx_trace_enable, tx_trace_event_filter, tx_trace_event_unfilter, tx_trace_disable, tx_trace_isr_enter_insert, tx_trace_isr_exit_insert, tx_trace_user_event_insert</span></span>

### <a name="tx_trace_user_event_insert"></a><span data-ttu-id="0c724-267">tx_trace_user_event_insert</span><span class="sxs-lookup"><span data-stu-id="0c724-267">tx_trace_user_event_insert</span></span>

#### <a name="insert-user-event"></a><span data-ttu-id="0c724-268">Kullanıcı olayı Ekle</span><span class="sxs-lookup"><span data-stu-id="0c724-268">Insert user event</span></span>

#### <a name="prototype"></a><span data-ttu-id="0c724-269">Prototype</span><span class="sxs-lookup"><span data-stu-id="0c724-269">Prototype</span></span>

```c
UINT tx_trace_user_event_insert (ULONG event_id, 
   ULONG info_field_1, ULONG info_field_2,
   ULONG info_field_3, ULONG info_field_4);
```

#### <a name="description"></a><span data-ttu-id="0c724-270">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0c724-270">Description</span></span>

<span data-ttu-id="0c724-271">Bu hizmet, Kullanıcı olayını izleme arabelleğine ekler.</span><span class="sxs-lookup"><span data-stu-id="0c724-271">This service inserts the user event into the trace buffer.</span></span> <span data-ttu-id="0c724-272">Kullanıcı olay kimlikleri 4096 olarak tanımlanan sabit **TX_TRACE_USER_EVENT_START** daha büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0c724-272">User event IDs must be greater than the constant **TX_TRACE_USER_EVENT_START**, which is defined to be 4096.</span></span> <span data-ttu-id="0c724-273">En fazla Kullanıcı olayı, 65535 olarak tanımlanan sabit **TX_TRACE_USER_EVENT_END** tarafından tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="0c724-273">The maximum user event is defined by the constant **TX_TRACE_USER_EVENT_END**, which is defined to be 65535.</span></span> <span data-ttu-id="0c724-274">Bu aralıktaki tüm olaylar uygulama için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="0c724-274">All events within this range are available to the application.</span></span> <span data-ttu-id="0c724-275">Bilgi alanları uygulamaya özeldir.</span><span class="sxs-lookup"><span data-stu-id="0c724-275">The information fields are application specific.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0c724-276">Etkinlik izlemeyi kullanabilmek için ThreadX kitaplığı ve uygulaması tanımlanmış **TX_ENABLE_EVENT_TRACE** oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0c724-276">The ThreadX library and application must be built with **TX_ENABLE_EVENT_TRACE** defined in order to use event tracing.</span></span>

#### <a name="input-parameters"></a><span data-ttu-id="0c724-277">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="0c724-277">Input Parameters</span></span>

- <span data-ttu-id="0c724-278">**event_id**: uygulamaya özgü olay kimliği ve **TX_TRACE_USER_EVENT_START** sıfırdan büyük ve **TX_TRACE_USER_EVENT_END** küçük ya da buna eşit olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0c724-278">**event_id**: Application-specific event identification and must start be greater than **TX_TRACE_USER_EVENT_START** and less than or equal to **TX_TRACE_USER_EVENT_END**.</span></span>
- <span data-ttu-id="0c724-279">**info_field_1**: uygulamaya özgü bilgi alanı.</span><span class="sxs-lookup"><span data-stu-id="0c724-279">**info_field_1**: Application-specific information field.</span></span>
- <span data-ttu-id="0c724-280">**info_field_2**: uygulamaya özgü bilgi alanı.</span><span class="sxs-lookup"><span data-stu-id="0c724-280">**info_field_2**: Application-specific information field.</span></span>
- <span data-ttu-id="0c724-281">**info_field_3**: uygulamaya özgü bilgi alanı.</span><span class="sxs-lookup"><span data-stu-id="0c724-281">**info_field_3**: Application-specific information field.</span></span>
- <span data-ttu-id="0c724-282">**info_field_4**: uygulamaya özgü bilgi alanı.</span><span class="sxs-lookup"><span data-stu-id="0c724-282">**info_field_4**: Application-specific information field.</span></span>

#### <a name="return-values"></a><span data-ttu-id="0c724-283">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="0c724-283">Return Values</span></span>
- <span data-ttu-id="0c724-284">**TX_SUCCESS** (0x00) başarılı Kullanıcı olayı ekleme.</span><span class="sxs-lookup"><span data-stu-id="0c724-284">**TX_SUCCESS** (0x00) Successful user event insert.</span></span>
- <span data-ttu-id="0c724-285">**TX_NOT_DONE** (0x20) olay izleme etkin değil.</span><span class="sxs-lookup"><span data-stu-id="0c724-285">**TX_NOT_DONE** (0x20) Event tracing is not enabled.</span></span>
- <span data-ttu-id="0c724-286">**TX_FEATURE_NOT_ENABLED** (0xFF) sistem izleme etkin ile derlenmedi.</span><span class="sxs-lookup"><span data-stu-id="0c724-286">**TX_FEATURE_NOT_ENABLED** (0xFF) The system was not compiled with trace enabled.</span></span>

#### <a name="allowed-from"></a><span data-ttu-id="0c724-287">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="0c724-287">Allowed From</span></span>

<span data-ttu-id="0c724-288">Başlatma ve iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="0c724-288">Initialization and threads</span></span>

#### <a name="example"></a><span data-ttu-id="0c724-289">Örnek</span><span class="sxs-lookup"><span data-stu-id="0c724-289">Example</span></span>

```c
/* Insert user event 3000, with info fields of 1, 2, 3, 4. */ 

status = tx_trace_user_event_insert (3000, 1, 2, 3, 4);

/* If status is TX_SUCCESS the user event was inserted. */
```

#### <a name="see-also"></a><span data-ttu-id="0c724-290">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="0c724-290">See Also</span></span>

<span data-ttu-id="0c724-291">tx_trace_enable, tx_trace_event_filter, tx_trace_event_unfilter, tx_trace_disable, tx_trace_isr_enter_insert, tx_trace_isr_exit_insert, tx_trace_buffer_full_notify</span><span class="sxs-lookup"><span data-stu-id="0c724-291">tx_trace_enable, tx_trace_event_filter, tx_trace_event_unfilter, tx_trace_disable, tx_trace_isr_enter_insert, tx_trace_isr_exit_insert, tx_trace_buffer_full_notify</span></span>