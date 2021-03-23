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
# <a name="chapter-11---format-of-event-trace-buffer"></a><span data-ttu-id="5f2d1-103">Bölüm 11-olay izleme arabelleğinin biçimi</span><span class="sxs-lookup"><span data-stu-id="5f2d1-103">Chapter 11 - Format of event trace buffer</span></span>

<span data-ttu-id="5f2d1-104">Azure RTOS ThreadX, tüm ThreadX Hizmetleri, iş parçacığı durumu değişiklikleri ve Kullanıcı tanımlı olaylar için yerleşik olay izleme desteği sağlar.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-104">Azure RTOS ThreadX provides built-in event trace support for all ThreadX services, thread state changes, and user-defined events.</span></span> <span data-ttu-id="5f2d1-105">Olay izlemeyi kullanmak için, tanımlanan **TX_ENABLE_EVENT_TRACE** Ile Threadx, NETX ve FileX kitaplıklarını oluşturmanız ve **_tx_trace_enable_** işlevini çağırarak izlemeyi etkinleştirmeniz yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-105">To use event trace, simply build the ThreadX, NetX, and FileX libraries with **TX_ENABLE_EVENT_TRACE** defined and enable tracing by calling the **_tx_trace_enable_** function.</span></span> <span data-ttu-id="5f2d1-106">Bu bölümde bu işlem açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-106">This chapter describes that process.</span></span>

## <a name="event-trace-format"></a><span data-ttu-id="5f2d1-107">Olay Izleme biçimi</span><span class="sxs-lookup"><span data-stu-id="5f2d1-107">Event Trace Format</span></span>

<span data-ttu-id="5f2d1-108">ThreadX olay izleme arabelleğinin biçimi üç bölüme bölünür, yani denetim üstbilgisi, nesne kayıt defteri ve izleme girdileri.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-108">The format of the ThreadX event trace buffer is divided into three sections, namely the control header, object registry, and the trace entries.</span></span> <span data-ttu-id="5f2d1-109">Aşağıdaki, ThreadX olay izleme arabelleğinin genel yerleşimini anlatmaktadır:</span><span class="sxs-lookup"><span data-stu-id="5f2d1-109">The following describes the general layout of the ThreadX event trace buffer:</span></span>

<span data-ttu-id="5f2d1-110">**Denetim üst bilgisi**</span><span class="sxs-lookup"><span data-stu-id="5f2d1-110">**Control Header**</span></span>

<span data-ttu-id="5f2d1-111">**Nesne kayıt defteri girdisi 0**</span><span class="sxs-lookup"><span data-stu-id="5f2d1-111">**Object Registry Entry 0**</span></span>

<span data-ttu-id="5f2d1-112">**…**</span><span class="sxs-lookup"><span data-stu-id="5f2d1-112">**…**</span></span>

<span data-ttu-id="5f2d1-113">**"N" nesne kayıt girdisi**</span><span class="sxs-lookup"><span data-stu-id="5f2d1-113">**Object Register Entry "n"**</span></span>

<span data-ttu-id="5f2d1-114">**Olay Izleme girdisi 0**</span><span class="sxs-lookup"><span data-stu-id="5f2d1-114">**Event Trace Entry 0**</span></span>

<span data-ttu-id="5f2d1-115">**…**</span><span class="sxs-lookup"><span data-stu-id="5f2d1-115">**…**</span></span>

<span data-ttu-id="5f2d1-116">**Olay Izleme girdisi "n"**</span><span class="sxs-lookup"><span data-stu-id="5f2d1-116">**Event Trace Entry "n"**</span></span>

### <a name="event-trace-control-header"></a><span data-ttu-id="5f2d1-117">Olay Izleme denetim üst bilgisi</span><span class="sxs-lookup"><span data-stu-id="5f2d1-117">Event Trace Control Header</span></span>

<span data-ttu-id="5f2d1-118">Denetim üst bilgisi, olay izleme arabelleğinin tam yerleşimini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-118">The control header defines the exact layout of the event trace buffer.</span></span> <span data-ttu-id="5f2d1-119">Bu, kaç tane ThreadX nesnesinin kaydedilebileceği ve kaç olay kaydedilebildiği de dahildir.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-119">This includes how many ThreadX objects can be registered as well as how many events can be recorded.</span></span> <span data-ttu-id="5f2d1-120">Ayrıca, denetim üst bilgisi, izleme arabelleği öğelerinin nerede olduğunu tanımlar.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-120">In addition, the control header defines where each of the elements of the trace buffer resides.</span></span> <span data-ttu-id="5f2d1-121">Aşağıdaki veri yapısı denetim üstbilgisini tanımlar:</span><span class="sxs-lookup"><span data-stu-id="5f2d1-121">The following data structure defines the control header:</span></span>

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

### <a name="control-header-id"></a><span data-ttu-id="5f2d1-122">Denetim üst bilgi KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="5f2d1-122">Control Header ID</span></span>

<span data-ttu-id="5f2d1-123">Denetim üst bilgisi KIMLIĞI, 0x54585442 olan 32 bitlik ONALTıLı değerden oluşur ve bu da ***ASCII karakterlerine karşılık*** gelir.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-123">The control header ID consists of the 32-bit HEX value of 0x54585442, which corresponds to the ASCII characters ***TXTB***.</span></span> <span data-ttu-id="5f2d1-124">Bu değer 32 bitlik işaretsiz bir değişken olarak yazıldığı için, olay izleme arabelleğinin bitiliğini algılamak için de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-124">Since this value is written as a 32-bit unsigned variable, it can also be used to detect the endianness of the event trace buffer.</span></span> <span data-ttu-id="5f2d1-125">Örneğin, belleğin ilk dört bEvet değeri 0x54, 0x58, 0x54, 0x42 ise, olay izleme arabelleği big endian biçimde yazılmıştır.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-125">For example, if the value in the first four byes of memory is 0x54, 0x58, 0x54, 0x42, the event trace buffer was written in big endian format.</span></span> <span data-ttu-id="5f2d1-126">Aksi takdirde, olay izleme arabelleği little endian biçimde yazılmıştır.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-126">Otherwise, the event trace buffer was written in little endian format.</span></span>

### <a name="timer-valid-mask"></a><span data-ttu-id="5f2d1-127">Süreölçer geçerli maskesi</span><span class="sxs-lookup"><span data-stu-id="5f2d1-127">Timer Valid Mask</span></span>

<span data-ttu-id="5f2d1-128">Süreölçer geçerli maskesi, gerçek olay izleme girişlerinde kaç tane zaman damgasının geçerli olduğunu tanımlar.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-128">The timer valid mask defines how many bits of the timestamp in the actual event trace entries are valid.</span></span> <span data-ttu-id="5f2d1-129">Örneğin, zaman damgası kaynağı 16 bit içeriyorsa, bu alandaki değer 0xFFFF olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-129">For example, if the time-stamp source has 16-bits, the value in this field should be 0xFFFF.</span></span> <span data-ttu-id="5f2d1-130">32 bitlik bir zaman damgası kaynağı 0xFFFFFFFF değerine sahip olacaktır.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-130">A 32-bit time-stamp source would have a value of 0xFFFFFFFF.</span></span> <span data-ttu-id="5f2d1-131">Bu değer _ *_tx_port. h_* \* içinde \***TX_TRACE_TIME_MASK** _ sabiti tarafından tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-131">This value is defined by the ***TX_TRACE_TIME_MASK** _ constant in _*_tx_port.h_\*\*.</span></span>

### <a name="trace-base-address"></a><span data-ttu-id="5f2d1-132">İzleme temel adresi</span><span class="sxs-lookup"><span data-stu-id="5f2d1-132">Trace Base Address</span></span>

<span data-ttu-id="5f2d1-133">İzleme arabelleği temel adresi, ***tx_trace_enable*** çağrısında izleme arabelleğinin başlangıcı olarak belirtilen uygulamanın adresidir.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-133">The trace buffer base address is the address the application specified as the start of the trace buffer in the ***tx_trace_enable*** call.</span></span> <span data-ttu-id="5f2d1-134">Bu adres, arabellekteki çeşitli öğeler için buffergöreli uzaklıklar türetmede analiz aracının tek kullanımı için korunur.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-134">This address is maintained for the sole use of the analysis tool to derive bufferrelative offsets for the various elements in the buffer.</span></span> <span data-ttu-id="5f2d1-135">Örneğin, izleme arabelleğindeki geçerli olayın arabellek göreli kayması, geçerli olay adresinden temel adresin basit çıkarma işlemi tarafından hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-135">For example, the buffer relative offset of the current event in the trace buffer is calculated by simple subtraction of the base address from the current event address.</span></span>

### <a name="registry-start-and-end-pointers"></a><span data-ttu-id="5f2d1-136">Kayıt defteri başlangıç ve bitiş Işaretçileri</span><span class="sxs-lookup"><span data-stu-id="5f2d1-136">Registry Start and End Pointers</span></span>

<span data-ttu-id="5f2d1-137">Kayıt defteri Başlangıç işaretçisi, ilk nesne kayıt defteri girdisinin adresini işaret ederken, kayıt defteri bitiş işaretçisi, e-mesajlaşma adresini gösterir. Son kayıt girişini takip/mediately.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-137">The registry start pointer points to the address of the first object registry entry, while the registry end pointer points to the address im../mediately following the last register entry.</span></span> <span data-ttu-id="5f2d1-138">Bu değerler *tx_trace_enable* işleme sırasında kurulumlardır ve izleme süresi boyunca değiştirilmez.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-138">These values are setup during the *tx_trace_enable* processing and are not changed throughout the duration of tracing.</span></span>

### <a name="registry-name-size"></a><span data-ttu-id="5f2d1-139">Kayıt defteri adı boyutu</span><span class="sxs-lookup"><span data-stu-id="5f2d1-139">Registry Name Size</span></span>

<span data-ttu-id="5f2d1-140">Kayıt defteri adı boyutu, kayıt defteri girdisindeki her bir nesne adı için bayt cinsinden en büyük boyutu tanımlar ve \***TX_TRACE_OBJECT_REGISTRY_NAME** _ simgesiyle tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-140">The registry name size defines maximum size in bytes for each object name in the registry entry and is defined by the symbol \***TX_TRACE_OBJECT_REGISTRY_NAME** _.</span></span> <span data-ttu-id="5f2d1-141">Varsayılan değer 32 ' dir ve _*_tx_trace. h_*_' de tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-141">The default value is 32 and is defined in _*_tx_trace.h_*_.</span></span> <span data-ttu-id="5f2d1-142">Nesne adı, nesne oluşturulduğunda uygulama tarafından verilen ada karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-142">The object name corresponds to the name given by the application when the object was created.</span></span> <span data-ttu-id="5f2d1-143">Örneğin, bir iş parçacığının nesne kayıt defteri adı, uygulama tarafından _ *_tx_thread_create_* \* çağrısı için sağlanan addır.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-143">For example, the object registry name for a thread is the name supplied by the application to the _\*_tx_thread_create_\*\*call.</span></span>

### <a name="buffer-start-and-end-pointers"></a><span data-ttu-id="5f2d1-144">Arabellek başlangıç ve bitiş Işaretçileri</span><span class="sxs-lookup"><span data-stu-id="5f2d1-144">Buffer Start and End Pointers</span></span>

<span data-ttu-id="5f2d1-145">Olay izleme arabelleği Başlangıç işaretçisi, ilk izleme girişinin adresini işaret ederken, kayıt defteri bitiş işaretçisi, e-mesajlaşma adresini gösterir. son izleme girişini takip eden/mediately.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-145">The event trace buffer start pointer points to the address of the first trace entry, while the registry end pointer points to the address im../mediately following the last trace entry.</span></span> <span data-ttu-id="5f2d1-146">Bu değerler, ***tx_trace_enable</*** işleme sırasında kurulumlardır ve izleme süresince değiştirilmez.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-146">These values are setup during the ***tx_trace_enable</*** processing and are not changed throughout the duration of tracing.</span></span>

### <a name="current-buffer-pointer"></a><span data-ttu-id="5f2d1-147">Geçerli arabellek Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="5f2d1-147">Current Buffer Pointer</span></span>

<span data-ttu-id="5f2d1-148">Olay izleme arabelleği geçerli işaretçisi, en eski izleme girişinin adresini gösterir.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-148">The event trace buffer current pointer points to the address of the oldest trace entry.</span></span> <span data-ttu-id="5f2d1-149">İzleme girişleri döngüsel bir listede tutulduğundan, geçerli arabellek işaretçisi yazılacak sonraki izleme girişini de temsil eder.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-149">Since the trace entries are maintained in a circular list, the current buffer pointer is also represents the next trace entry to be written.</span></span> |

## <a name="event-trace-object-registry"></a><span data-ttu-id="5f2d1-150">Olay Izleme nesnesi kayıt defteri</span><span class="sxs-lookup"><span data-stu-id="5f2d1-150">Event Trace Object Registry</span></span>

<span data-ttu-id="5f2d1-151">Olay izleme nesnesi kayıt defteri, uygulama tarafından oluşturulan nesnelere karşılık gelen \***n** _ nesne kayıt defteri girdilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-151">The event trace object registry contains \***n** _ object registry entries that correspond to the objects created by the application.</span></span> <span data-ttu-id="5f2d1-152">Nesne kayıt defterinin ana amacı, gerçek nesne adlarını izleme arabelleği girdilerinin nesne adresleriyle ilişkilendirmek için dış analiz araçlarına yöneliktir.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-152">The main purpose of the object registry is for external analysis tools to correlate actual object names with the object addresses of the trace buffer entries.</span></span> <span data-ttu-id="5f2d1-153">Kayıt defteri girdilerinin sayısı, uygulama tarafından _ *_tx_trace_enable_*\* çağrısında belirtilir.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-153">The number of registry entries is specified by the application in the _ *_tx_trace_enable_*\* call.</span></span>

<span data-ttu-id="5f2d1-154">Her nesne kayıt girdisi, daha önce uygulama tarafından oluşturulan belirli bir ThreadX nesnesi hakkında bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-154">Each object register entry contains information about a specific ThreadX object previously created by the application.</span></span> <span data-ttu-id="5f2d1-155">Aşağıdaki veri yapısı her nesne kayıt defteri girişini tanımlar:</span><span class="sxs-lookup"><span data-stu-id="5f2d1-155">The following data structure defines each object registry entry:</span></span>

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

### <a name="object-available-flag"></a><span data-ttu-id="5f2d1-156">Nesne kullanılabilir bayrağı</span><span class="sxs-lookup"><span data-stu-id="5f2d1-156">Object Available Flag</span></span>

<span data-ttu-id="5f2d1-157">Nesne kayıt defteri girişi varsa, nesne kullanılabilir bayrağı 1 olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-157">The object available flag is set to 1 if the object registry entry is available.</span></span> <span data-ttu-id="5f2d1-158">Aksi takdirde, değer 1 değilse, nesne kayıt defteri girişi kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-158">Otherwise, if the value is not 1, the object registry entry is not available.</span></span> <span data-ttu-id="5f2d1-159">Girişin kullanılabilir olmasına rağmen yine de geçerli bilgiler içerebileceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-159">Note that the entry could still contain valid information even though it is available.</span></span>

### <a name="object-entry-type"></a><span data-ttu-id="5f2d1-160">Nesne giriş türü</span><span class="sxs-lookup"><span data-stu-id="5f2d1-160">Object Entry Type</span></span>

<span data-ttu-id="5f2d1-161">Nesne giriş türü, bu girişte nesnenin türünü tanımlar.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-161">The object entry type identifies the type of object in this entry.</span></span> <span data-ttu-id="5f2d1-162">Geçerli nesne türlerinin listesi aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="5f2d1-162">The following is a list of the valid object types:</span></span>

| <span data-ttu-id="5f2d1-163">**Değer**</span><span class="sxs-lookup"><span data-stu-id="5f2d1-163">**Value**</span></span> | <span data-ttu-id="5f2d1-164">**Nesne türü**</span><span class="sxs-lookup"><span data-stu-id="5f2d1-164">**Object Type**</span></span> |
|---------- | --------------- |
| <span data-ttu-id="5f2d1-165">0</span><span class="sxs-lookup"><span data-stu-id="5f2d1-165">0</span></span>         | <span data-ttu-id="5f2d1-166">Geçerli değil</span><span class="sxs-lookup"><span data-stu-id="5f2d1-166">Not Valid</span></span>       |
| <span data-ttu-id="5f2d1-167">1</span><span class="sxs-lookup"><span data-stu-id="5f2d1-167">1</span></span>         | <span data-ttu-id="5f2d1-168">İş Parçacığı</span><span class="sxs-lookup"><span data-stu-id="5f2d1-168">Thread</span></span>          |
| <span data-ttu-id="5f2d1-169">2</span><span class="sxs-lookup"><span data-stu-id="5f2d1-169">2</span></span>         | <span data-ttu-id="5f2d1-170">Zamanlayıcı</span><span class="sxs-lookup"><span data-stu-id="5f2d1-170">Timer</span></span> |
| <span data-ttu-id="5f2d1-171">3</span><span class="sxs-lookup"><span data-stu-id="5f2d1-171">3</span></span>         | <span data-ttu-id="5f2d1-172">Kuyruk</span><span class="sxs-lookup"><span data-stu-id="5f2d1-172">Queue</span></span> |
| <span data-ttu-id="5f2d1-173">4</span><span class="sxs-lookup"><span data-stu-id="5f2d1-173">4</span></span>         | <span data-ttu-id="5f2d1-174">Semafor</span><span class="sxs-lookup"><span data-stu-id="5f2d1-174">Semaphore</span></span> |
| <span data-ttu-id="5f2d1-175">5</span><span class="sxs-lookup"><span data-stu-id="5f2d1-175">5</span></span>         | <span data-ttu-id="5f2d1-176">Mutex</span><span class="sxs-lookup"><span data-stu-id="5f2d1-176">Mutex</span></span> |
| <span data-ttu-id="5f2d1-177">6</span><span class="sxs-lookup"><span data-stu-id="5f2d1-177">6</span></span>         | <span data-ttu-id="5f2d1-178">Olay bayrakları grubu</span><span class="sxs-lookup"><span data-stu-id="5f2d1-178">Event Flags Group</span></span> |
| <span data-ttu-id="5f2d1-179">7</span><span class="sxs-lookup"><span data-stu-id="5f2d1-179">7</span></span>         | <span data-ttu-id="5f2d1-180">Blok havuzu</span><span class="sxs-lookup"><span data-stu-id="5f2d1-180">Block Pool</span></span> |
| <span data-ttu-id="5f2d1-181">8</span><span class="sxs-lookup"><span data-stu-id="5f2d1-181">8</span></span>         | <span data-ttu-id="5f2d1-182">Bayt havuzu</span><span class="sxs-lookup"><span data-stu-id="5f2d1-182">Byte Pool</span></span> |
| <span data-ttu-id="5f2d1-183">9</span><span class="sxs-lookup"><span data-stu-id="5f2d1-183">9</span></span>         | <span data-ttu-id="5f2d1-184">.. /Medya</span><span class="sxs-lookup"><span data-stu-id="5f2d1-184">../media</span></span> |
| <span data-ttu-id="5f2d1-185">10</span><span class="sxs-lookup"><span data-stu-id="5f2d1-185">10</span></span>        | <span data-ttu-id="5f2d1-186">Dosya</span><span class="sxs-lookup"><span data-stu-id="5f2d1-186">File</span></span> |
| <span data-ttu-id="5f2d1-187">11</span><span class="sxs-lookup"><span data-stu-id="5f2d1-187">11</span></span>        | <span data-ttu-id="5f2d1-188">IP</span><span class="sxs-lookup"><span data-stu-id="5f2d1-188">IP</span></span> |
| <span data-ttu-id="5f2d1-189">12</span><span class="sxs-lookup"><span data-stu-id="5f2d1-189">12</span></span>        | <span data-ttu-id="5f2d1-190">Paket havuzu</span><span class="sxs-lookup"><span data-stu-id="5f2d1-190">Packet Pool</span></span> |
| <span data-ttu-id="5f2d1-191">13</span><span class="sxs-lookup"><span data-stu-id="5f2d1-191">13</span></span>        | <span data-ttu-id="5f2d1-192">TCP yuvası</span><span class="sxs-lookup"><span data-stu-id="5f2d1-192">TCP Socket</span></span> |
| <span data-ttu-id="5f2d1-193">14</span><span class="sxs-lookup"><span data-stu-id="5f2d1-193">14</span></span>        | <span data-ttu-id="5f2d1-194">UDP yuvası</span><span class="sxs-lookup"><span data-stu-id="5f2d1-194">UDP Socket</span></span> |
| <span data-ttu-id="5f2d1-195">15-20</span><span class="sxs-lookup"><span data-stu-id="5f2d1-195">15-20</span></span>     | <span data-ttu-id="5f2d1-196">Ayrılmıştır</span><span class="sxs-lookup"><span data-stu-id="5f2d1-196">Reserved</span></span> |  
| <span data-ttu-id="5f2d1-197">21</span><span class="sxs-lookup"><span data-stu-id="5f2d1-197">21</span></span>        | <span data-ttu-id="5f2d1-198">USB ana bilgisayar yığını cihazı</span><span class="sxs-lookup"><span data-stu-id="5f2d1-198">USB Host Stack Device</span></span> |
| <span data-ttu-id="5f2d1-199">22</span><span class="sxs-lookup"><span data-stu-id="5f2d1-199">22</span></span>        | <span data-ttu-id="5f2d1-200">USB ana bilgisayar yığını arabirimi</span><span class="sxs-lookup"><span data-stu-id="5f2d1-200">USB Host Stack Interface</span></span> |
| <span data-ttu-id="5f2d1-201">23</span><span class="sxs-lookup"><span data-stu-id="5f2d1-201">23</span></span>        | <span data-ttu-id="5f2d1-202">USB ana bilgisayar uç noktası</span><span class="sxs-lookup"><span data-stu-id="5f2d1-202">USB Host Endpoint</span></span> |
| <span data-ttu-id="5f2d1-203">24</span><span class="sxs-lookup"><span data-stu-id="5f2d1-203">24</span></span>        | <span data-ttu-id="5f2d1-204">USB ana bilgisayar sınıfı</span><span class="sxs-lookup"><span data-stu-id="5f2d1-204">USB Host Class</span></span> |
| <span data-ttu-id="5f2d1-205">25</span><span class="sxs-lookup"><span data-stu-id="5f2d1-205">25</span></span>        | <span data-ttu-id="5f2d1-206">USB cihazı</span><span class="sxs-lookup"><span data-stu-id="5f2d1-206">USB Device</span></span> |
| <span data-ttu-id="5f2d1-207">26</span><span class="sxs-lookup"><span data-stu-id="5f2d1-207">26</span></span>        | <span data-ttu-id="5f2d1-208">USB cihaz arabirimi</span><span class="sxs-lookup"><span data-stu-id="5f2d1-208">USB Device Interface</span></span> |
| <span data-ttu-id="5f2d1-209">27</span><span class="sxs-lookup"><span data-stu-id="5f2d1-209">27</span></span>        | <span data-ttu-id="5f2d1-210">USB cihaz uç noktası</span><span class="sxs-lookup"><span data-stu-id="5f2d1-210">USB Device Endpoint</span></span> |
| <span data-ttu-id="5f2d1-211">28</span><span class="sxs-lookup"><span data-stu-id="5f2d1-211">28</span></span>        | <span data-ttu-id="5f2d1-212">USB cihaz sınıfı</span><span class="sxs-lookup"><span data-stu-id="5f2d1-212">USB Device Class</span></span> |

### <a name="object-pointer"></a><span data-ttu-id="5f2d1-213">Nesne Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="5f2d1-213">Object Pointer</span></span>

<span data-ttu-id="5f2d1-214">Nesne işaretçisi, ThreadX API kullanarak nesneye erişmek için kullanılan nesne adresini belirtir.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-214">The object pointer specifies the object address that is used for accessing the object using the ThreadX API.</span></span>

### <a name="object-reserved-fields"></a><span data-ttu-id="5f2d1-215">Nesne ayrılmış alanları</span><span class="sxs-lookup"><span data-stu-id="5f2d1-215">Object Reserved Fields</span></span>

<span data-ttu-id="5f2d1-216">İş parçacıkları dışındaki tüm nesneler için, bu ayrılmış alanlar 0 olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-216">For all objects other than threads, these reserved fields should be 0.</span></span> <span data-ttu-id="5f2d1-217">İş parçacıkları için, kayıt defterine girildiği sırada iş parçacığının önceliği, bu iki ayrılmış alana yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-217">For threads, the priority of the thread at the time it is entered into the registry is placed in these two reserved fields.</span></span>

### <a name="object-parameters"></a><span data-ttu-id="5f2d1-218">Nesne parametreleri</span><span class="sxs-lookup"><span data-stu-id="5f2d1-218">Object Parameters</span></span>

<span data-ttu-id="5f2d1-219">Nesne parametreleri, nesne hakkında ek bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-219">The object parameters contain supplemental information about the object.</span></span> <span data-ttu-id="5f2d1-220">Aşağıda her bir ThreadX nesnesi için ek bilgiler açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="5f2d1-220">The following describes the supplemental information for each ThreadX object:</span></span>

| <span data-ttu-id="5f2d1-221">**Nesne türü**</span><span class="sxs-lookup"><span data-stu-id="5f2d1-221">**Object Type**</span></span>        | <span data-ttu-id="5f2d1-222">**Parametre 1**</span><span class="sxs-lookup"><span data-stu-id="5f2d1-222">**Parameter 1**</span></span>  | <span data-ttu-id="5f2d1-223">**Parametre 2**</span><span class="sxs-lookup"><span data-stu-id="5f2d1-223">**Parameter 2**</span></span> |
|----------------------- | ---------------- | --------------- |
| <span data-ttu-id="5f2d1-224">İş Parçacığı</span><span class="sxs-lookup"><span data-stu-id="5f2d1-224">Thread</span></span>                 | <span data-ttu-id="5f2d1-225">Yığın başlangıcı</span><span class="sxs-lookup"><span data-stu-id="5f2d1-225">Stack Start</span></span>      | <span data-ttu-id="5f2d1-226">Yığın boyutu</span><span class="sxs-lookup"><span data-stu-id="5f2d1-226">Stack Size</span></span> |
| <span data-ttu-id="5f2d1-227">Zamanlayıcı</span><span class="sxs-lookup"><span data-stu-id="5f2d1-227">Timer</span></span>                  | <span data-ttu-id="5f2d1-228">İlk ticks</span><span class="sxs-lookup"><span data-stu-id="5f2d1-228">Initial Ticks</span></span> | <span data-ttu-id="5f2d1-229">Yeniden zamanlama Işaretleri</span><span class="sxs-lookup"><span data-stu-id="5f2d1-229">Reschedule Ticks</span></span> |
| <span data-ttu-id="5f2d1-230">Kuyruk</span><span class="sxs-lookup"><span data-stu-id="5f2d1-230">Queue</span></span>                  | <span data-ttu-id="5f2d1-231">Sıra boyutu</span><span class="sxs-lookup"><span data-stu-id="5f2d1-231">Queue Size</span></span> | <span data-ttu-id="5f2d1-232">İleti boyutu</span><span class="sxs-lookup"><span data-stu-id="5f2d1-232">Message Size</span></span> |
| <span data-ttu-id="5f2d1-233">Semafor</span><span class="sxs-lookup"><span data-stu-id="5f2d1-233">Semaphore</span></span>              | <span data-ttu-id="5f2d1-234">İlk örnekler</span><span class="sxs-lookup"><span data-stu-id="5f2d1-234">Initial Instances</span></span> | - |
| <span data-ttu-id="5f2d1-235">Mutex</span><span class="sxs-lookup"><span data-stu-id="5f2d1-235">Mutex</span></span>                  | <span data-ttu-id="5f2d1-236">Devralma bayrağı</span><span class="sxs-lookup"><span data-stu-id="5f2d1-236">Inheritance Flag</span></span> | - |
| <span data-ttu-id="5f2d1-237">Olay bayrakları grubu</span><span class="sxs-lookup"><span data-stu-id="5f2d1-237">Event Flags Group</span></span>      | - | - |
| <span data-ttu-id="5f2d1-238">Blok havuzu</span><span class="sxs-lookup"><span data-stu-id="5f2d1-238">Block Pool</span></span>             | <span data-ttu-id="5f2d1-239">Toplam blok sayısı</span><span class="sxs-lookup"><span data-stu-id="5f2d1-239">Total Blocks</span></span> | <span data-ttu-id="5f2d1-240">Blok Boyutu</span><span class="sxs-lookup"><span data-stu-id="5f2d1-240">Block Size</span></span> |
| <span data-ttu-id="5f2d1-241">Bayt havuzu</span><span class="sxs-lookup"><span data-stu-id="5f2d1-241">Byte Pool</span></span>              | <span data-ttu-id="5f2d1-242">Toplam bayt sayısı</span><span class="sxs-lookup"><span data-stu-id="5f2d1-242">Total Bytes</span></span> | - |
| <span data-ttu-id="5f2d1-243">.. /Medya</span><span class="sxs-lookup"><span data-stu-id="5f2d1-243">../media</span></span>                  | <span data-ttu-id="5f2d1-244">FAT önbellek boyutu</span><span class="sxs-lookup"><span data-stu-id="5f2d1-244">Fat Cache Size</span></span> | <span data-ttu-id="5f2d1-245">Kesim önbelleği boyutu</span><span class="sxs-lookup"><span data-stu-id="5f2d1-245">Sector Cache Size</span></span> |
| <span data-ttu-id="5f2d1-246">Dosya</span><span class="sxs-lookup"><span data-stu-id="5f2d1-246">File</span></span>                   | - | - |
| <span data-ttu-id="5f2d1-247">IP</span><span class="sxs-lookup"><span data-stu-id="5f2d1-247">IP</span></span>                     | <span data-ttu-id="5f2d1-248">Yığın başlangıcı</span><span class="sxs-lookup"><span data-stu-id="5f2d1-248">Stack Start</span></span> | <span data-ttu-id="5f2d1-249">Yığın boyutu</span><span class="sxs-lookup"><span data-stu-id="5f2d1-249">Stack Size</span></span> |
| <span data-ttu-id="5f2d1-250">Paket havuzu</span><span class="sxs-lookup"><span data-stu-id="5f2d1-250">Packet Pool</span></span>            | <span data-ttu-id="5f2d1-251">Paket boyutu</span><span class="sxs-lookup"><span data-stu-id="5f2d1-251">Packet Size</span></span> | <span data-ttu-id="5f2d1-252">Paket sayısı</span><span class="sxs-lookup"><span data-stu-id="5f2d1-252">Number of Packets</span></span> |
| <span data-ttu-id="5f2d1-253">TCP yuvası</span><span class="sxs-lookup"><span data-stu-id="5f2d1-253">TCP Socket</span></span>             | <span data-ttu-id="5f2d1-254">IP Adresi</span><span class="sxs-lookup"><span data-stu-id="5f2d1-254">IP address</span></span> | <span data-ttu-id="5f2d1-255">Pencere boyutu</span><span class="sxs-lookup"><span data-stu-id="5f2d1-255">Window Size</span></span> |
| <span data-ttu-id="5f2d1-256">UDP yuvası</span><span class="sxs-lookup"><span data-stu-id="5f2d1-256">UDP Socket</span></span>             | <span data-ttu-id="5f2d1-257">IP Adresi</span><span class="sxs-lookup"><span data-stu-id="5f2d1-257">IP address</span></span> | <span data-ttu-id="5f2d1-258">RX kuyruğu en yüksek</span><span class="sxs-lookup"><span data-stu-id="5f2d1-258">RX Queue Max</span></span> |

### <a name="object-name"></a><span data-ttu-id="5f2d1-259">Nesne adı</span><span class="sxs-lookup"><span data-stu-id="5f2d1-259">Object Name</span></span>

<span data-ttu-id="5f2d1-260">Nesne adı ThreadX nesnesinin adını içerir.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-260">The object name contains the name of the ThreadX object.</span></span> <span data-ttu-id="5f2d1-261">Ad, nesne oluşturulduğu sırada ThreadX için girilen addır.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-261">The name is the name provided to ThreadX at the time the object was created.</span></span> <span data-ttu-id="5f2d1-262">Varsayılan olarak, nesne adının en fazla 32 karakter vardır.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-262">By default, the object name has a maximum of 32 characters.</span></span> <span data-ttu-id="5f2d1-263">32 karakterden büyük gerçek adlar kesilir.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-263">Actual names greater than 32 characters are truncated.</span></span>

## <a name="event-trace-entries"></a><span data-ttu-id="5f2d1-264">Olay Izleme girdileri</span><span class="sxs-lookup"><span data-stu-id="5f2d1-264">Event Trace Entries</span></span>

<span data-ttu-id="5f2d1-265">Olay izleme girişleri, olay izleme arabelleğinin alt bölümünde bulunur.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-265">The event trace entries are found in the bottom portion of the event trace buffer.</span></span> <span data-ttu-id="5f2d1-266">Girdiler, geçerli giriş işaretçisiyle en eski girişi işaret eden bir dairesel listede tutulur.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-266">The entries are maintained in a circular list, with the current entry pointer pointing to the oldest entry.</span></span> <span data-ttu-id="5f2d1-267">Listedeki giriş sayısı ***tx_trace_enable*** çağrısıyla hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-267">The number of entries in the list is calculated by the ***tx_trace_enable*** call.</span></span>

<span data-ttu-id="5f2d1-268">Her nesne kayıt girişi, belirli bir ThreadX izleme olayı hakkında bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-268">Each object register entry contains information about a specific ThreadX trace event.</span></span> <span data-ttu-id="5f2d1-269">Aşağıdaki veri yapısı her izleme olayı girişini tanımlar:</span><span class="sxs-lookup"><span data-stu-id="5f2d1-269">The following data structure defines each trace event entry:</span></span>

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

### <a name="thread-pointer"></a><span data-ttu-id="5f2d1-270">İş parçacığı Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="5f2d1-270">Thread Pointer</span></span>

<span data-ttu-id="5f2d1-271">İş parçacığı işaretçisi, bu olay sırasında çalışan iş parçacığının adresini içerir.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-271">The thread pointer contains the address of the thread running at the time of this event.</span></span> <span data-ttu-id="5f2d1-272">Başlatma sırasında olay oluştuysa (çalışan iş parçacığı yoksa), Bu işaretçinin değeri 0xF0F0F0F0 ' dır.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-272">If the event occurred during initialization (no thread running), the value of this pointer is 0xF0F0F0F0.</span></span> <span data-ttu-id="5f2d1-273">Bir kesme hizmeti yordamı (ıSR) sırasında olay oluştuysa, Bu işaretçinin değeri 0xFFFFFFFF ' dir.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-273">If the event occurred during an Interrupt Service Routine (ISR), the value of this pointer is 0xFFFFFFFF.</span></span> <span data-ttu-id="5f2d1-274">Giriş henüz kullanılmıyorsa, Bu işaretçinin değeri 0 ' dır.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-274">If the entry has not yet been used, the value of this pointer is 0.</span></span>

### <a name="thread-priority"></a><span data-ttu-id="5f2d1-275">İş parçacığı önceliği</span><span class="sxs-lookup"><span data-stu-id="5f2d1-275">Thread Priority</span></span>

<span data-ttu-id="5f2d1-276">İş parçacığı öncelik alanı, bu olay sırasında çalışan iş parçacığının iş parçacığı önceliğini ve önalım eşiğini içerir.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-276">The thread priority field contains the thread priority and preemption-threshold of the thread that was running at the time of this event.</span></span> <span data-ttu-id="5f2d1-277">Bir kesme bağlamı varsa (iş parçacığı işaretçisi 0xFFFFFFFF), bu alanın değeri öncelik değildir ancak olay sırasında ***_tx_thread_current_ptr*** değeri olur.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-277">If an interrupt context is present (thread pointer is 0xFFFFFFFF), the value of this field is not the priority but instead the value of ***_tx_thread_current_ptr*** at the time of the event.</span></span> <span data-ttu-id="5f2d1-278">Aksi takdirde, bu alanın değeri 0 ' dır.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-278">Otherwise, the value of this field is 0.</span></span>

### <a name="event-id"></a><span data-ttu-id="5f2d1-279">Olay Kimliği</span><span class="sxs-lookup"><span data-stu-id="5f2d1-279">Event ID</span></span>

<span data-ttu-id="5f2d1-280">Olay KIMLIĞI, gerçekleşen olayı belirtir.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-280">The event ID specifies the event that took place.</span></span> <span data-ttu-id="5f2d1-281">Geçerli ThreadX Trace olay kimlikleri 1 ila 1024 arasındadır.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-281">Valid ThreadX trace event IDs range from 1 through 1024.</span></span> <span data-ttu-id="5f2d1-282">1025 ve üzeri sürümlerde başlayan değerler kullanıcıya özgü olaylar için ayrılmıştır.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-282">Values starting at 1025 and above are reserved for user-specific events.</span></span> <span data-ttu-id="5f2d1-283">Lütfen ThreadX olay kimliklerinin tamamının tanımının ***tx_trace. h*** dosyasına bakın.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-283">Please refer to the ***tx_trace.h*** file for the complete definition of ThreadX event IDs.</span></span></td>

### <a name="information-fields-1-4"></a><span data-ttu-id="5f2d1-284">Bilgi alanları (1-4)</span><span class="sxs-lookup"><span data-stu-id="5f2d1-284">Information Fields (1-4)</span></span>

<span data-ttu-id="5f2d1-285">Bilgi alanları, belirli olayla ilgili ek bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-285">The information fields contain additional information about the specific event.</span></span> <span data-ttu-id="5f2d1-286">Tanımlı ThreadX olay kimliklerinin her biri için bilgi alanlarının tamamının açıklaması için lütfen ***tx_trace. h*** dosyasına bakın.</span><span class="sxs-lookup"><span data-stu-id="5f2d1-286">Please refer to the ***tx_trace.h*** file for the complete description of the information fields for each of the defined ThreadX event IDs.</span></span>