---
title: Bölüm 4-Azure RTOS ThreadX hizmetlerinin açıklaması
description: Bu bölüm, tüm Azure RTOS ThreadX hizmetlerinin alfabetik sırada bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 60ecc96df07b1f77b9b448814c4420133f3e2afc
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825457"
---
# <a name="chapter-4---description-of-azure-rtos-threadx-services"></a>Bölüm 4-Azure RTOS ThreadX hizmetlerinin açıklaması

Bu bölüm, tüm Azure RTOS ThreadX hizmetlerinin alfabetik sırada bir açıklamasını içerir. Adları, benzer tüm hizmetlerin birlikte gruplanabilmesi için tasarlanmıştır. Aşağıdaki açıklamaların "dönüş değerleri" bölümünde, **kalın yazı** DEĞERLERI, API hata denetimini devre dışı bırakmak için kullanılan tanımlama **TX_DISABLE_ERROR_CHECKING** etkilenmez; kalın olmayan içinde gösterilen değerler tamamen devre dışı bırakılır. Buna ek olarak, "**önalım olası**" başlığı altında listelenen bir "**Evet**" seçeneği, hizmeti çağırmanın daha yüksek öncelikli bir iş parçacığını sürdürüleceği ve bu nedenle çağıran iş parçacığını öncelik verme gösterir.

## <a name="tx_block_allocate"></a>tx_block_allocate

Sabit boyutlu bellek bloğunu ayır

### <a name="prototype"></a>Prototype

```c
UINT tx_block_allocate(
    TX_BLOCK_POOL *pool_ptr, 
    VOID **block_ptr,
    ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen bellek havuzundan sabit boyutlu bir bellek bloğu ayırır. Bellek bloğunun gerçek boyutu bellek havuzu oluşturma sırasında belirlenir.

> [!IMPORTANT]
> *Uygulama kodunun ayrılan bellek bloğunun dışına yazmadığından emin olmak önemlidir. Bu durumda, bir komşu (genellikle sonraki) bellek bloğunda bozulma oluşur. Sonuçlar tahmin edilemez ve genellikle önemli olur!*

### <a name="parameters"></a>Parametreler

- **pool_ptr** <br>Önceden oluşturulmuş bir bellek blok havuzuna yönelik işaretçi.
- **block_ptr** <br>Hedef blok işaretçisine yönelik işaretçi. Başarılı bir ayırma sırasında, ayrılan bellek bloğunun adresi bu parametrenin gösterdiği yere yerleştirilir.
- **wait_option** <br>Kullanılabilir bellek bloğu yoksa hizmetin nasıl davranacağını tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **TX_NO_WAIT** (0x00000000)- **TX_NO_WAIT** seçilmesi, başarılı olup olmamasına bakılmaksızın bu hizmetten anında dönüşte sonuçlanır. *Bu, hizmet iş parçacığından çağrıldığında geçerli olan tek seçenektir; Örneğin, başlatma, süreölçer veya ISR*.
  - **TX_WAIT_FOREVER** (0xFFFFFFF)- **TX_WAIT_FOREVER** seçme, bir bellek bloğu kullanılabilir olana kadar çağıran iş parçacığının süresiz olarak askıda kalmasına neden olur.
  - *zaman aşımı değeri* (0x00000001-0xfffffffe)-sayısal bir değer (1-0XFFFFFFFE) seçildiğinde, bellek bloğu beklenirken askıya alınması için en fazla Zamanlayıcı sayısını belirtir.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS**    (0x00) başarılı bellek bloğu ayırması.
- **TX_DELETED**    (0x01) bellek bloğu havuzu, iş parçacığı askıya alınırken silindi.
- **TX_NO_MEMORY**  (0x10) hizmeti, belirli bir süre içinde beklenecek bir bellek bloğunu ayıramadı.
- **TX_WAIT_ABORTED**   (0x1A) askıya alma başka bir iş parçacığı, ZAMANLAYıCı veya ISR tarafından iptal edildi.
- **TX_POOL_ERROR** (0x02) geçersiz bellek bloğu havuz işaretçisi.
- **TX_WAIT_ERROR** (0x04) TX_NO_WAIT dışında bir bekleme seçeneği, iş parçacığından oluşan bir çağrıda belirtildi.
- **TX_PTR_ERROR**  (0x03) hedef işaretçisine geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="preemption-possible"></a>Önalım mümkün

Yes

### <a name="example"></a>Örnek

```c
TX_BLOCK_POOL my_pool;
unsigned char *memory_ptr;

UINT status;

/* Allocate a memory block from my_pool. Assume that the pool has
already been created with a call to tx_block_pool_create. */

status = tx_block_allocate(&my_pool, (VOID **) &memory_ptr,
  TX_NO_WAIT);

/* If status equals TX_SUCCESS, memory_ptr contains the address of
the allocated block of memory. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_block_pool_create
- tx_block_pool_delete
- tx_block_pool_info_get
- tx_block_pool_performance_info_get
- tx_block_pool_performance_system_info_get
- tx_block_pool_prioritize
- tx_block_release

## <a name="tx_block_pool_create"></a>tx_block_pool_create

Sabit boyutlu bellek blokları Havuzu Oluştur

### <a name="prototype"></a>Prototype

```c
UINT tx_block_pool_create(
    TX_BLOCK_POOL pool_ptr,
    CHAR name_ptr, 
    ULONG block_size,
    VOID pool_start, 
    ULONG pool_size);
```

### <a name="description"></a>Açıklama

Bu hizmet sabit boyutlu bellek blokları havuzu oluşturur. Belirtilen bellek alanı, formülü kullanılarak olabildiğince çok sabit boyutlu bellek bloklarına ayrılmıştır:

**Toplam blok** = (**toplam bayt**)/(**blok boyutu** + sizeof (void *))

> [!NOTE]
>* Her bellek bloğunda, kullanıcıya görünmeyen bir ek yük işaretçisi bulunur ve önceki formülde "sizeof (void *)"* ile temsil edilir.

### <a name="parameters"></a>Parametreler

- **pool_ptr**  Bellek blok havuzu denetim bloğunun işaretçisi.
- **name_ptr**  Bellek bloğu havuzunun adı işaretçisi.
- **block_size**    Her bir bellek bloğundaki bayt sayısı.
- **pool_start**    Bellek bloğu havuzunun başlangıç adresi. Başlangıç adresi ULONG veri türünün boyutuna hizalanmalıdır.
- **pool_size** Bellek blok havuzu için kullanılabilen toplam bayt sayısı.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS**    (0x00) başarılı bellek bloğu havuzu oluşturma.
- **TX_POOL_ERROR** (0x02) geçersiz bellek bloğu havuz işaretçisi. İşaretçi NULL ya da havuz zaten oluşturulmuş.
- **TX_PTR_ERROR**  (0x03) havuzun başlangıç adresi geçersiz.
- **TX_CALLER_ERROR**   (0x13) Bu hizmet için geçersiz çağrı.
- **TX_SIZE_ERROR** (0x05) havuzun boyutu geçersiz.

### <a name="allowed-from"></a>İzin verilen

Başlatma ve iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```c
TX_BLOCK_POOL my_pool;

UINT status;

/* Create a memory pool whose total size is 1000 bytes starting at
address 0x100000. Each block in this pool is defined to be 50 bytes
long. */
status = tx_block_pool_create(&my_pool, "my_pool_name",
  50, (VOID *) 0x100000, 1000);

/* If status equals TX_SUCCESS, my_pool contains 18 memory blocks
of 50 bytes each. The reason there are not 20 blocks in the pool is
because of the one overhead pointer associated with each block. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_block_allocate, tx_block_pool_delete
- tx_block_pool_info_get, tx_block_pool_performance_info_get
- tx_block_pool_performance_system_info_get
- tx_block_pool_prioritize, tx_block_release

## <a name="tx_block_pool_delete"></a>tx_block_pool_delete

Bellek blok havuzunu Sil

### <a name="prototype"></a>Prototype

```c
UINT tx_block_pool_delete(TX_BLOCK_POOL *pool_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen blok bellek havuzunu siler. Bu havuzdan bir bellek bloğunun beklediği tüm iş parçacıkları sürdürülür ve **TX_DELETED** bir dönüş durumu verilir.

> [!NOTE]
> *Bu hizmet tamamlandıktan sonra kullanılabilir olan havuz ile ilişkili bellek alanını yönetmek uygulamanın sorumluluğundadır. Ayrıca, uygulamanın silinen bir havuzun veya eski bellek bloklarının kullanımını engellemesi gerekir.*

### <a name="parameters"></a>Parametreler

- **pool_ptr** Önceden oluşturulmuş bir bellek blok havuzuna yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı bellek blok havuzu silme.
- **TX_POOL_ERROR** (0x02) geçersiz bellek bloğu havuz işaretçisi.
- **TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Yes

### <a name="example"></a>Örnek

```c
TX_BLOCK_POOL my_pool;

UINT           status;

/* Delete entire memory block
pool. Assume that the pool has already been created with a call to
tx_block_pool_create. */
status = tx_block_pool_delete(&my_pool);

/* If status equals TX_SUCCESS, the memory block pool is deleted.*/
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_block_allocate
- tx_block_pool_create
- tx_block_pool_info_get, tx_block_pool_performance_info_get
- tx_block_pool_performance_system_info_get
- tx_block_pool_prioritize, tx_block_release

## <a name="tx_block_pool_info_get"></a>tx_block_pool_info_get

Blok havuzu hakkında bilgi alma

### <a name="prototype"></a>Prototype

```c
UINT tx_block_pool_info_get(
    TX_BLOCK_POOL *pool_ptr, 
    CHAR **name,
    ULONG *available, 
    ULONG *total_blocks,
    TX_THREAD **first_suspended,
    ULONG *suspended_count,
    TX_BLOCK_POOL **next_pool);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen blok bellek havuzu hakkında bilgi alır.

### <a name="parameters"></a>Parametreler

- **pool_ptr**  Daha önce oluşturulan bellek bloğu havuzuna yönelik işaretçi.
- **ad**  Blok havuzunun adına işaretçi için hedef işaretçisi.
- **kullanılabilir** Blok havuzundaki kullanılabilir blok sayısı için hedef işaretçisi.
- **total_blocks**  Blok havuzundaki toplam blok sayısı için hedef işaretçisi.
- **first_suspended**   Bu blok havuzunun askıya alma listesindeki ilk iş parçacığına işaretçi için hedef işaretçisi.
- **suspended_count**   Bu blok havuzunda Şu anda askıya alınmış iş parçacığı sayısı için hedef işaretçisi.
- **next_pool** Sonraki oluşturulan blok havuzunun işaretçisi için hedef işaretçisi.

> [!NOTE]
> *Herhangi bir parametre için TX_NULL sağlamak, parametrenin gerekli olmadığını gösterir.*

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı blok havuzu bilgileri alma.
- **TX_POOL_ERROR** (0x02) geçersiz bellek bloğu havuz işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="example"></a>Örnek

```c
TX_BLOCK_POOL my_pool;
CHAR *name;
ULONG available;
ULONG total_blocks;
TX_THREAD *first_suspended;
ULONG suspended_count;
TX_BLOCK_POOL *next_pool;
UINT status;

/* Retrieve information about the previously created
block pool "my_pool." */
status = tx_block_pool_info_get(&my_pool, &name,
  &available,&total_blocks,
  &first_suspended, &suspended_count,
  &next_pool);

/* If status equals TX_SUCCESS, the information requested is
valid. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_block_allocate
- tx_block_pool_create
- tx_block_pool_delete
- tx_block_pool_info_get, tx_block_pool_performance_info_get
- tx_block_pool_performance_system_info_get
- tx_block_pool_prioritize, tx_block_release

## <a name="tx_block_pool_performance_info_get"></a>tx_block_pool_performance_info_get

Blok havuzu performans bilgilerini al

### <a name="prototype"></a>Prototype

```c
UINT tx_block_pool_performance_info_get(
    TX_BLOCK_POOL *pool_ptr,
    ULONG *allocates, 
    ULONG *releases,
    ULONG *suspensions, 
    ULONG *timeouts));
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen bellek bloğu havuzuyla ilgili performans bilgilerini alır.

> [!IMPORTANT]
> *ThreadX kitaplığı ve uygulaması,*  *performans bilgilerini döndürmek için bu hizmetin tanımlanmış* TX_BLOCK_POOL_ENABLE_PERFORMANCE_INFO oluşturulmalıdır.

### <a name="parameters"></a>Parametreler

- **pool_ptr**  Daha önce oluşturulan bellek bloğu havuzuna yönelik işaretçi.
- **ayırır** Bu havuzda gerçekleştirilen ayırma isteklerinin sayısı için hedef işaretçisi.
- **yayınlar**  Bu havuzda gerçekleştirilen yayın isteği sayısı için hedef işaretçisi.
- **getirilmesi**   Bu havuzdaki iş parçacığı ayırma getirilmesi sayısı için hedef işaretçisi.
- **zaman aşımları**  Bu havuzdaki askıya alma zaman aşımı sayısını ayır için hedef işaretçisi.

>[!NOTE]
> *Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.*

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS**    (0x00) başarılı blok havuz performansı al.
- **TX_PTR_ERROR**  (0x03) geçersiz blok havuzu işaretçisi.
- **TX_FEATURE_NOT_ENABLED**    (0xFF) sistem, etkin performans bilgileri ile derlenmedi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="example"></a>Örnek

```c
TX_BLOCK_POOL my_pool;
ULONG allocates;
ULONG releases;
ULONG suspensions;
ULONG timeouts;

/* Retrieve performance information on the previously created block
pool. */
status = tx_block_pool_performance_info_get(&my_pool, &allocates,
  &releases,
  &suspensions,
  &timeouts);

/* If status is TX_SUCCESS the performance information was successfully retrieved. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_block_allocate
- tx_block_pool_create
- tx_block_pool_delete
- tx_block_pool_info_get
- tx_block_pool_performance_info_get
- tx_block_pool_performance_system_info_get
- tx_block_release

## <a name="tx_block_pool_performance_system_info_get"></a>tx_block_pool_performance_system_info_get

Blok havuzu sistem performans bilgilerini al

### <a name="prototype"></a>Prototype

```c
UINT tx_block_pool_performance_system_info_get(
    ULONG *allocates,
    ULONG *releases, 
    ULONG *suspensions, 
    ULONG *timeouts);
```

### <a name="description"></a>Açıklama

Bu hizmet, uygulamadaki tüm bellek blok havuzlarıyla ilgili performans bilgilerini alır.

> [!IMPORTANT]
> *ThreadX kitaplığı ve uygulaması,*  *performans bilgilerini döndürmek için bu hizmetin tanımlanmış* TX_BLOCK_POOL_ENABLE_PERFORMANCE_INFO oluşturulmalıdır.

### <a name="parameters"></a>Parametreler

- **ayırır** Tüm blok havuzlarında gerçekleştirilen toplam ayırma isteği sayısının hedefi işaretçisi.
- **yayınlar**  Tüm blok havuzlarında gerçekleştirilen yayın isteklerinin toplam sayısı için hedef işaretçisi.
- **getirilmesi**   Tüm blok havuzlarındaki iş parçacığı ayırma getirilmesi toplam sayısı için hedef işaretçisi.
- **zaman aşımları**  Tüm blok havuzlarında askıya alınma zaman aşımlarının toplam sayısını ayırmak için hedef işaretçisi.

> [!NOTE]
> *Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.*

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı blok havuzu sistem performansı al.
- **TX_FEATURE_NOT_ENABLED** (0xFF) sistem, etkin performans bilgileri ile derlenmedi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="example"></a>Örnek

```c
ULONG       allocates;
ULONG       releases;
ULONG       suspensions;
ULONG       timeouts;

/* Retrieve performance information on all the block pools in
the system. */
status = tx_block_pool_performance_system_info_get(&allocates,
    &releases,&suspensions, &timeouts);

/* If status is TX_SUCCESS the performance information was
successfully retrieved. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_block_allocate
- tx_block_pool_create
- tx_block_pool_delete
- tx_block_pool_info_get
- tx_block_pool_performance_info_get
- tx_block_pool_prioritize
- tx_block_release

## <a name="tx_block_pool_prioritize"></a>tx_block_pool_prioritize

Blok havuzunu askıya alma listesini önceliklendir

### <a name="prototype"></a>Prototype

```c
UINT tx_block_pool_prioritize(TX_BLOCK_POOL *pool_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, askıya alma listesinin önünde bu havuzdaki bellek bloğu için en yüksek öncelikli iş parçacığını askıya aldı. Diğer tüm iş parçacıkları ' de askıya alındığı FıFO sırasında kalır.

### <a name="parameters"></a>Parametreler

- **pool_ptr** Bellek blok havuzu denetim bloğunun işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı blok havuzu önceliği.
- **TX_POOL_ERROR** (0x02) geçersiz bellek bloğu havuz işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek
```c
TX_BLOCK_POOL my_pool;
UINT status;

/* Ensure that the highest priority thread will receive
the next free block in this pool. */
status = tx_block_pool_prioritize(&my_pool);

/* If status equals TX_SUCCESS, the highest priority
suspended thread is at the front of the list. The
next tx_block_release call will wake up this thread. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_block_allocate
- tx_block_pool_create
- tx_block_pool_delete
- tx_block_pool_info_get
- tx_block_pool_performance_info_get
- tx_block_pool_performance_system_info_get
- tx_block_release

## <a name="tx_block_release"></a>tx_block_release

Sabit boyutlu bellek bloğunu serbest bırakma

### <a name="prototype"></a>Prototype

```c
UINT tx_block_release(VOID *block_ptr);
``````

### <a name="description"></a>Açıklama

Bu hizmet önceden ayrılmış bir bloğu, ilişkili bellek havuzuna geri yayınlar. Bu havuzdan bellek blokları bekleyen bir veya daha fazla iş parçacığı varsa, askıya alınan ilk iş parçacığına bu bellek bloğu verilir ve devam edilir.

>[!IMPORTANT]
>*Uygulamanın, havuza geri sunulduktan sonra bir bellek bloğu alanını kullanmasını engellemesi gerekir.*

### <a name="parameters"></a>Parametreler

- **block_ptr** Önceden ayrılmış bellek bloğuna yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı bellek bloğu sürümü.
- **TX_PTR_ERROR** (0x03) bellek bloğunun işaretçisi geçersiz.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="preemption-possible"></a>Önalım mümkün

Yes

### <a name="example"></a>Örnek

```c
TX_BLOCK_POOL my_pool;
unsigned char *memory_ptr;
UINT status;

/* Release a memory block back to my_pool. Assume that the
pool has been created and the memory block has been
allocated. */
status = tx_block_release((VOID *) memory_ptr);

/* If status equals TX_SUCCESS, the block of memory pointed
to by memory_ptr has been returned to the pool. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_block_allocate
- tx_block_pool_create
- tx_block_pool_delete
- tx_block_pool_info_get
- tx_block_pool_performance_info_get
- tx_block_pool_performance_system_info_get
- tx_block_pool_prioritize

## <a name="tx_byte_allocate"></a>tx_byte_allocate

Bellek baytları ayır

### <a name="prototype"></a>Prototype

```c
UINT tx_byte_allocate(
    TX_BYTE_POOL *pool_ptr,
    VOID **memory_ptr, 
    ULONG memory_size,
    ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen bellek bayt havuzundan belirtilen sayıda bayt ayırır.

> [!IMPORTANT]
> *Uygulama kodunun ayrılan bellek bloğunun dışına yazmadığından emin olmak önemlidir. Bu durumda, bir komşu (genellikle sonraki) bellek bloğunda bozulma oluşur. Sonuçlar tahmin edilemez ve genellikle önemli olur!*

> [!NOTE]
> *Bu hizmetin performansı, blok boyutunun ve havuzdaki parçalanma miktarının bir işlevidir. Bu nedenle, bu hizmet yürütmenin zaman kritik iş parçacıkları sırasında kullanılmamalıdır.*

### <a name="parameters"></a>Parametreler

- **pool_ptr** <br>Önceden oluşturulmuş bir bellek blok havuzuna yönelik işaretçi.
- **memory_ptr** <br>Hedef bellek işaretçisine yönelik işaretçi. Başarılı bir ayırma sırasında, ayrılan bellek alanının adresi bu parametrenin işaret ettiği yere yerleştirilir.
- **memory_size** <br>İstenen bayt sayısı.
- **wait_option** <br>Yeterli kullanılabilir bellek yoksa hizmetin nasıl davranacağını tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **TX_NO_WAIT** (0x00000000)- **TX_NO_WAIT** seçilmesi, başarılı olup olmamasına bakılmaksızın bu hizmetten anında geri dönüş sonucunu verir. *Bu, hizmet başlatma işleminden çağrıldığında geçerli tek seçenektir.*
  - **TX_WAIT_FOREVER** 0xFFFFFFFF)- **TX_WAIT_FOREVER** seçilmesi, çağıran iş parçacığının yeterli bellek kullanılabilir olana kadar süresiz olarak askıda kalmasına neden olur.
  - *zaman aşımı değeri* (0x00000001-0xfffffffe)-sayısal bir değer (1-0XFFFFFFFE) seçildiğinde, bellek beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı bellek ayırması.
- **TX_DELETED** (0x01) bellek havuzu, iş parçacığı askıya alınırken silindi.
- **TX_NO_MEMORY** (0x10) hizmeti, belleği, belirtilen süre içinde beklemek için ayıramadı.
- **TX_WAIT_ABORTED** (0x1A) askıya alma başka bir iş parçacığı, ZAMANLAYıCı veya ISR tarafından iptal edildi.
- **TX_POOL_ERROR** (0x02) geçersiz bellek havuzu işaretçisi.
- **TX_PTR_ERROR** (0x03) hedef işaretçisine geçersiz işaretçi.
- **TX_SIZE_ERROR** (0x05) istenen boyut sıfır veya havuzdan büyük.
- **TX_WAIT_ERROR** (0x04) TX_NO_WAIT dışında bir bekleme seçeneği, iş parçacığından oluşan bir çağrıda belirtildi.
- **TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

Başlatma ve iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Yes

### <a name="example"></a>Örnek
```c
TX_BYTE_POOL my_pool;
unsigned char*memory_ptr;
UINT status;
/* Allocate a 112 byte memory area from my_pool. Assume
that the pool has already been created with a call to
tx_byte_pool_create. */
status = tx_byte_allocate(&my_pool, (VOID **) &memory_ptr,
    112, TX_NO_WAIT);

/* If status equals TX_SUCCESS, memory_ptr contains the
address of the allocated memory area. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_byte_pool_create
- tx_byte_pool_delete
- tx_byte_pool_info_get
- tx_byte_pool_performance_info_get
- tx_byte_pool_performance_system_info_get
- tx_byte_pool_prioritize
- tx_byte_release

## <a name="tx_byte_pool_create"></a>tx_byte_pool_create

Bayt bellek havuzu oluştur

### <a name="prototype"></a>Prototype

```c
UINT tx_byte_pool_create(
    TX_BYTE_POOL *pool_ptr,
    CHAR *name_ptr, 
    VOID *pool_start,
    ULONG pool_size);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen alanda bir bellek bayt havuzu oluşturur. İlk olarak havuz, temel olarak bir çok büyük ücretsiz bloğundan oluşur. Ancak, ayırmalar yapıldığından havuz daha küçük bloklar halinde bozulur.

### <a name="parameters"></a>Parametreler

- **pool_ptr** Bellek havuzu denetim bloğu işaretçisi.
- **name_ptr** Bellek havuzunun adı işaretçisi.
- **pool_start** Bellek havuzunun başlangıç adresi. Başlangıç adresi ULONG veri türünün boyutuna hizalanmalıdır.
- **pool_size** Bellek havuzu için kullanılabilen toplam bayt sayısı.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı bellek havuzu oluşturma.
- **TX_POOL_ERROR** (0x02) geçersiz bellek havuzu işaretçisi. İşaretçi NULL ya da havuz zaten oluşturulmuş.
- **TX_PTR_ERROR** (0x03) havuzun başlangıç adresi geçersiz.
- **TX_SIZE_ERROR** (0x05) havuzun boyutu geçersiz.
- **TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

Başlatma ve iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```c
TX_BYTE_POOL my_pool;
UINT status;
/* Create a memory pool whose total size is 2000 bytes
starting at address 0x500000. */
status = tx_byte_pool_create(&my_pool, "my_pool_name",
    (VOID *) 0x500000, 2000);

/* If status equals TX_SUCCESS, my_pool is available for
allocating memory. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_byte_allocate
- tx_byte_pool_delete
- tx_byte_pool_info_get
- tx_byte_pool_performance_info_get
- tx_byte_pool_performance_system_info_get
- tx_byte_pool_prioritize
- tx_byte_release

## <a name="tx_byte_pool_delete"></a>tx_byte_pool_delete

Bellek bayt havuzunu Sil

### <a name="prototype"></a>Prototype

```c
UINT tx_byte_pool_delete(TX_BYTE_POOL *pool_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen bellek bayt havuzunu siler. Bu havuzdan bellek beklemeyi askıya alınmış tüm iş parçacıkları sürdürülür ve **TX_DELETED** bir dönüş durumu verilir.

> [!IMPORTANT]
> *Bu hizmet tamamlandıktan sonra kullanılabilir olan havuz ile ilişkili bellek alanını yönetmek uygulamanın sorumluluğundadır. Ayrıca, uygulamanın silinen bir havuzun veya daha önce ayrılmış belleğin kullanımını önlemesi gerekir.*

### <a name="parameters"></a>Parametreler

- **pool_ptr** Daha önce oluşturulmuş bir bellek havuzuna yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı bellek havuzu silme.
- **TX_POOL_ERROR** (0x02) geçersiz bellek havuzu işaretçisi.
- **TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Yes

### <a name="example"></a>Örnek

```c
TX_BYTE_POOL my_pool;
UINT status;
/* Delete entire memory pool. Assume that the pool has already
been created with a call to tx_byte_pool_create. */
status = tx_byte_pool_delete(&my_pool);

/* If status equals TX_SUCCESS, memory pool is deleted. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_byte_allocate
- tx_byte_pool_create
- tx_byte_pool_info_get
- tx_byte_pool_performance_info_get
- tx_byte_pool_performance_system_info_get
- tx_byte_pool_prioritize
- tx_byte_release

## <a name="tx_byte_pool_info_get"></a>tx_byte_pool_info_get

Bayt havuzu hakkında bilgi alın

### <a name="prototype"></a>Prototype

```c
UINT tx_byte_pool_info_get(
    TX_BYTE_POOL *pool_ptr, 
    CHAR **name,
    ULONG *available, 
    ULONG *fragments,
    TX_THREAD **first_suspended,
    ULONG *suspended_count,
    TX_BYTE_POOL **next_pool);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen bellek bayt havuzu hakkında bilgi alır.

### <a name="parameters"></a>Parametreler

- **pool_ptr** Daha önce oluşturulmuş bellek havuzu işaretçisi.
- **ad** Bayt havuzunun adı işaretçisinin hedefi işaretçisi.
- **kullanılabilir** Havuzdaki kullanılabilir bayt sayısı için hedef işaretçisi.
- **parçalar** Bayt havuzundaki toplam bellek parçası sayısının hedefi işaretçisi.
- **first_suspended** Bu bayt havuzunun askıya alma listesindeki iş parçacığına işaretçi için hedef işaretçisi.
- **suspended_count** Bu bayt havuzunda Şu anda askıya alınan iş parçacığı sayısı için hedef işaretçisi.
- **next_pool** Sonraki oluşturulan bayt havuzunun işaretçisi için hedef işaretçisi.

> [!NOTE]
> *Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.*

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı havuz bilgileri alma.
- **TX_POOL_ERROR** (0x02) geçersiz bellek havuzu işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```c
TX_BYTE_POOL my_pool;
CHAR *name;
ULONG available;
ULONG fragments;
TX_THREAD *first_suspended;
ULONG suspended_count;
TX_BYTE_POOL *next_pool;
UINT status;

/* Retrieve information about the previously created
block pool "my_pool." */
status = tx_byte_pool_info_get(&my_pool, &name,
  &available, &fragments,
  &first_suspended, &suspended_count,
  &next_pool);

/* If status equals TX_SUCCESS, the information requested is
valid. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_byte_allocate
- tx_byte_pool_create
- tx_byte_pool_delete
- tx_byte_pool_performance_info_get
- tx_byte_pool_performance_system_info_get
- tx_byte_pool_prioritize
- tx_byte_release

## <a name="tx_byte_pool_performance_info_get"></a>tx_byte_pool_performance_info_get

Bayt havuzu performans bilgilerini al

### <a name="prototype"></a>Prototype

```c
UINT tx_byte_pool_performance_info_get(
    TX_BYTE_POOL *pool_ptr,
    ULONG *allocates, 
    ULONG *releases,
    ULONG *fragments_searched, 
    ULONG *merges, 
    ULONG *splits,
    ULONG *suspensions, 
    ULONG *timeouts);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen bellek bayt havuzuyla ilgili performans bilgilerini alır.

> [!IMPORTANT]
> *ThreadX kitaplığı ve uygulaması,*  *performans bilgilerini döndürmek için bu hizmetin tanımlanmış* TX_BYTE_POOL_ENABLE_PERFORMANCE_INFO oluşturulmalıdır.

### <a name="parameters"></a>Parametreler

- **pool_ptr** Daha önce oluşturulan bellek bayt havuzu işaretçisi.
- **ayırır** Bu havuzda gerçekleştirilen ayırma isteklerinin sayısı için hedef işaretçisi.
- **yayınlar** Bu havuzda gerçekleştirilen yayın isteği sayısı için hedef işaretçisi.
- **fragments_searched** Bu havuzdaki ayırma istekleri sırasında aranan iç bellek parçacıklarının sayısı için hedef işaretçisi.
- **birleştirmeler** Bu havuzdaki ayırma istekleri sırasında birleştirilmiş iç bellek blokları sayısı için hedef işaretçisi.
- **böler** Bu havuzdaki ayırma istekleri sırasında oluşturulan iç bellek blokları sayısı (parçalar) için hedef işaretçisi.
- **getirilmesi** Bu havuzdaki iş parçacığı ayırma getirilmesi sayısı için hedef işaretçisi.
- **zaman aşımları** Bu havuzdaki askıya alma zaman aşımı sayısını ayır için hedef işaretçisi.

> [!NOTE]
> *Herhangi bir parametre için TX_NULL sağlamak, parametrenin gerekli olmadığını gösterir.*

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı bayt havuzu performans Get.
- **TX_PTR_ERROR** (0x03) geçersiz bayt havuzu işaretçisi.
- **TX_FEATURE_NOT_ENABLED** (0xFF) sistem, etkin performans bilgileri ile derlenmedi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="example"></a>Örnek

```c
TX_BYTE_POOL my_pool;
ULONG fragments_searched;
ULONG merges;
ULONG splits;
ULONG allocates;
ULONG releases;
ULONG suspensions;
ULONG timeouts;

/* Retrieve performance information on the previously created byte
pool. */
status = tx_byte_pool_performance_info_get(&my_pool,
  &fragments_searched,
  &merges, &splits,
  &allocates, &releases,
  &suspensions,&timeouts);

/* If status is TX_SUCCESS the performance information was
successfully retrieved. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- tx_byte_allocate
- tx_byte_pool_create
- tx_byte_pool_delete
- tx_byte_pool_info_get
- tx_byte_pool_performance_system_info_get
- tx_byte_pool_prioritize
- tx_byte_release

## <a name="tx_byte_pool_performance_system_info_get"></a>tx_byte_pool_performance_system_info_get

Bayt havuzu sistem performans bilgilerini al

### <a name="prototype"></a>Prototype

```c
UINT tx_byte_pool_performance_system_info_get(
    ULONG *allocates,
    ULONG *releases, 
    ULONG *fragments_searched, 
    ULONG *merges,
    ULONG *splits, 
    ULONG *suspensions, 
    ULONG *timeouts);
```
### <a name="description"></a>Açıklama

Bu hizmet sistemdeki tüm bellek bayt havuzlarıyla ilgili performans bilgilerini alır.

> [!IMPORTANT]
> *ThreadX kitaplığı ve uygulaması,*  *performans bilgilerini döndürmek için bu hizmetin tanımlanmış* TX_BYTE_POOL_ENABLE_PERFORMANCE_INFO oluşturulmalıdır.

### <a name="parameters"></a>Parametreler

- **ayırır** Bu havuzda gerçekleştirilen ayırma isteklerinin sayısı için hedef işaretçisi.
- **yayınlar** Bu havuzda gerçekleştirilen yayın isteği sayısı için hedef işaretçisi.
- **fragments_searched** Tüm bayt havuzlarındaki ayırma istekleri sırasında aranan iç bellek parçacıklarının toplam sayısı için hedef işaretçisi.
- **birleştirmeler** Tüm bayt havuzlarındaki ayırma istekleri sırasında birleştirilmiş iç bellek bloklarının toplam sayısı için hedef işaretçisi.
- **böler** Tüm bayt havuzlarındaki ayırma istekleri sırasında oluşturulan toplam iç bellek bloğu sayısı (parça) için hedef işaretçisi.
- **getirilmesi** Tüm bayt havuzlarındaki iş parçacığı ayırma getirilmesi toplam sayısı için hedef işaretçisi.
- **zaman aşımları** Tüm bayt havuzlarında askıya alınma zaman aşımlarının toplam sayısını ayırmak için hedef işaretçisi.

> [!NOTE]
> *Herhangi bir parametre için TX_NULL sağlamak, parametrenin gerekli olmadığını gösterir.*

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı bayt havuzu performans Get.
- **TX_FEATURE_NOT_ENABLED** (0xFF) sistem, etkin performans bilgileri ile derlenmedi.

### <a name="allowed-from"></a>İzin verilen

 Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="example"></a>Örnek

```c
ULONG fragments_searched;
ULONG merges;
ULONG splits;
ULONG allocates;
ULONG releases;
ULONG suspensions;
ULONG timeouts;

/* Retrieve performance information on all byte pools in the
system. */
status =
tx_byte_pool_performance_system_info_get(&fragments_searched,
  &merges, &splits, &allocates, &releases,
  &suspensions, &timeouts);

/* If status is TX_SUCCESS the performance information was
successfully retrieved. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_byte_allocate
- tx_byte_pool_create
- tx_byte_pool_delete
- tx_byte_pool_info_get
- tx_byte_pool_performance_info_get
- tx_byte_pool_prioritize
- tx_byte_release

## <a name="tx_byte_pool_prioritize"></a>tx_byte_pool_prioritize

Bayt havuzunun askıya alınma listesini önceliklendir

### <a name="prototype"></a>Prototype

```c
UINT tx_byte_pool_prioritize(TX_BYTE_POOL *pool_ptr);
```
### <a name="description"></a>Açıklama

Bu hizmet, bu havuzdaki bellek için askıya alınan en yüksek öncelikli iş parçacığını askıya alma listesinin önüne koyar. Diğer tüm iş parçacıkları ' de askıya alındığı FıFO sırasında kalır.

### <a name="parameters"></a>Parametreler

- **pool_ptr** Bellek havuzu denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı bellek havuzu önceliği belirleme.
- **TX_POOL_ERROR** (0x02) geçersiz bellek havuzu işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```c
TX_BYTE_POOL my_pool;
UINT status;

/* Ensure that the highest priority thread will receive
the next free memory from this pool. */
status = tx_byte_pool_prioritize(&my_pool);

/* If status equals TX_SUCCESS, the highest priority
suspended thread is at the front of the list. The
next tx_byte_release call will wake up this thread,
if there is enough memory to satisfy its request. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_byte_allocate
- tx_byte_pool_create
- tx_byte_pool_delete
- tx_byte_pool_info_get
- tx_byte_pool_performance_info_get
- tx_byte_pool_performance_system_info_get
- tx_byte_release

## <a name="tx_byte_release"></a>tx_byte_release

Baytları bellek havuzuna geri bırakma

### <a name="prototype"></a>Prototype

```c
UINT tx_byte_release(VOID *memory_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet önceden ayrılmış bir bellek alanını ilişkili havuzuna geri yayınlar. Bu havuzdan bellek beklemeyi askıya alınmış bir veya daha fazla iş parçacığı varsa, askıya alınan her iş parçacığına bellek verilir ve bellek tükenene veya daha fazla askıya alınmış iş parçacığı kalmayana kadar devam sürdürülür. Askıya alınan iş parçacıkları için bellek ayırma işlemi, her zaman askıya alınan ilk iş parçacığı ile başlar.

> [!IMPORTANT]
> *Uygulamanın, serbest bırakıldıktan sonra bellek alanını kullanmasını önleyecek olması gerekir.*

### <a name="parameters"></a>Parametreler

- **memory_ptr** Önceden ayrılmış bellek alanına yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı bellek sürümü.
- **TX_PTR_ERROR** (0x03) geçersiz bellek alanı işaretçisi.
- **TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

Başlatma ve iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Yes

### <a name="example"></a>Örnek

```c
unsigned char *memory_ptr;
UINT status;

/* Release a memory back to my_pool. Assume that the memory
area was previously allocated from my_pool. */
status = tx_byte_release((VOID *) memory_ptr);

/* If status equals TX_SUCCESS, the memory pointed to by
memory_ptr has been returned to the pool. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_byte_allocate
- tx_byte_pool_create
- tx_byte_pool_delete
- tx_byte_pool_info_get
- tx_byte_pool_performance_info_get
- tx_byte_pool_performance_system_info_get
- tx_byte_pool_prioritize

## <a name="tx_event_flags_create"></a>tx_event_flags_create

Olay bayrakları grubu oluştur

### <a name="prototype"></a>Prototype

```c
UINT tx_event_flags_create(
    TX_EVENT_FLAGS_GROUP *group_ptr,
    CHAR *name_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet bir 32 olay bayrağı grubu oluşturur. Gruptaki tüm 32 olay bayrakları sıfır olarak başlatılır. Her olay bayrağı tek bir bit ile temsil edilir.

### <a name="parameters"></a>Parametreler

- **group_ptr** Olay bayrakları Grup denetim bloğuna yönelik işaretçi.
- **name_ptr** Olay bayrakları grubunun adı işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı olay grubu oluşturma.
- **TX_GROUP_ERROR** (0x06) geçersiz olay grubu işaretçisi. İşaretçi **null** ya da olay grubu zaten oluşturulmuş.
- **TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

Başlatma ve iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```c
TX_EVENT_FLAGS_GROUP my_event_group;
UINT status;

/* Create an event flags group. */
status = tx_event_flags_create(&my_event_group,
  "my_event_group_name");

/* If status equals TX_SUCCESS, my_event_group is ready
for get and set services. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_event_flags_delete
- tx_event_flags_get
- tx_event_flags_info_get
- tx_event_flags_performance_info_get
- tx_event_flags_performance_system_info_get
- tx_event_flags_set
- tx_event_flags_set_notify

## <a name="tx_event_flags_delete"></a>tx_event_flags_delete

Olay bayrakları grubunu sil

### <a name="prototype"></a>Prototype

```c
UINT tx_event_flags_delete(TX_EVENT_FLAGS_GROUP *group_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen olay bayrakları grubunu siler. Bu gruptan gelen olayların beklediği tüm iş parçacıkları sürdürülür ve TX_DELETED bir dönüş durumu verilir.

>[!IMPORTANT]
> *Uygulama, olay bayrakları grubu silinmeden önce bu olay bayrakları grubu için bir küme bildirme geri çağrısının tamamlandığını (veya devre dışı) içerdiğinden emin olmalıdır. Ayrıca, uygulamanın, silinen bir olay bayrakları grubunun gelecekteki tüm kullanımını önlemesi gerekir.*

### <a name="parameters"></a>Parametreler

- **group_ptr** Daha önce oluşturulmuş bir olay bayrakları grubuna yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı olay bayrakları grubu silme.
- **TX_GROUP_ERROR** (0x06) geçersiz olay bayrakları grup işaretçisi.
- **TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Yes

### <a name="example"></a>Örnek

```c
TX_EVENT_FLAGS_GROUP my_event_flags_group;
UINT status;

/* Delete event flags group. Assume that the group has
already been created with a call to
tx_event_flags_create. */
status = tx_event_flags_delete(&my_event_flags_group);

/* If status equals TX_SUCCESS, the event flags group is
deleted. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_event_flags_create
- tx_event_flags_get
- tx_event_flags_info_get
- tx_event_flags_performance_info_get
- tx_event_flags_performance_system_info_get
- tx_event_flags_set
- tx_event_flags_set_notify

## <a name="tx_event_flags_get"></a>tx_event_flags_get

Olay bayrakları grubundan olay bayraklarını al

### <a name="prototype"></a>Prototype

```c
UINT tx_event_flags_get(
    TX_EVENT_FLAGS_GROUP *group_ptr,
    ULONG requested_flags, 
    UINT get_option,
    ULONG *actual_flags_ptr, 
    ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen olay bayrakları grubundan olay bayraklarını alır. Her olay bayrakları grubu 32 olay bayrağını içerir. Her bayrak tek bir bit ile temsil edilir. Bu hizmet, giriş parametreleri tarafından seçilen çeşitli olay bayrağı kombinasyonlarını alabilir.

### <a name="parameters"></a>Parametreler

- **group_ptr** <br>Daha önce oluşturulmuş bir olay bayrakları grubuna yönelik işaretçi.
- **requested_flags** <br>İstenen olay bayraklarını temsil eden 32 bitlik işaretsiz değişken.
- **get_option** <br>İstenen olay bayraklarının tümünün veya herhangi birinin gerekli olup olmadığını belirtir. Aşağıdakiler geçerli seçimlerdir:

  - **TX_AND** (0x02)
  - **TX_AND_CLEAR** (0x03)
  - **TX_OR** (0x00)
  - **TX_OR_CLEAR** (0x01)

    TX_AND veya TX_AND_CLEAR seçilmesi, tüm olay bayraklarının grupta mevcut olması gerektiğini belirtir. TX_OR veya TX_OR_CLEAR seçilmesi herhangi bir olay bayrağının tatmin edici olduğunu belirtir. TX_AND_CLEAR veya TX_OR_CLEAR belirtilirse, isteği karşılayan olay bayrakları temizlenir (sıfır olarak ayarlanır).

- **actual_flags_ptr** <br>Alınan olay bayraklarının yerleştirildiği hedefin hedefi işaretçisi. Alınan gerçek bayrakların istenmedi bayrakları içerebileceğini unutmayın.
- **wait_option**  <br>Seçilen olay bayrakları ayarlanmamışsa hizmetin nasıl davranacağını tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **TX_NO_WAIT** (0x00000000)-TX_NO_WAIT seçilmesi, başarılı olup olmamasına bakılmaksızın bu hizmetten anında geri dönüş sonucunu verir. Bu, hizmet iş parçacığından çağrıldığında tek geçerli seçenektir; Örneğin, başlatma, süreölçer veya ıSR.
  - **TX_WAIT_FOREVER** zaman aşımı değeri (0xffffffff)-TX_WAIT_FOREVER seçilmesi, çağıran iş parçacığının olay bayrakları kullanılabilir olana kadar süresiz olarak askıda kalmasına neden olur.
  - zaman aşımı değeri (0x00000001-0xFFFFFFFE)-sayısal bir değer (1-0xFFFFFFFE) seçildiğinde, olay bayrakları beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı olay bayrakları al.
- İş parçacığı askıya alınırken **TX_DELETED** (0x01) olay bayrakları grubu silindi.
- **TX_NO_EVENTS** (0x07) hizmeti, belirtilen olayları beklemek için belirtilen süre içinde alamadı.
- **TX_WAIT_ABORTED** (0x1A) askıya alma başka bir iş parçacığı, ZAMANLAYıCı veya ISR tarafından iptal edildi.
- **TX_GROUP_ERROR** (0x06) geçersiz olay bayrakları grup işaretçisi.
- **TX_PTR_ERROR** (0x03) gerçek olay bayrakları için geçersiz işaretçi.
- **TX_WAIT_ERROR** (0x04) TX_NO_WAIT dışında bir bekleme seçeneği, iş parçacığından oluşan bir çağrıda belirtildi.
- **TX_OPTION_ERROR** (0x08) geçersiz Get-OPTION belirtildi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="preemption-possible"></a>Önalım mümkün

Yes

### <a name="example"></a>Örnek

```c
TX_EVENT_FLAGS_GROUP my_event_flags_group;
ULONG actual_events;
UINT status;

/* Request that event flags 0, 4, and 8 are all set. Also,
if they are set they should be cleared. If the event
flags are not set, this service suspends for a maximum of
20 timer-ticks. */
status = tx_event_flags_get(&my_event_flags_group, 0x111,
    TX_AND_CLEAR, &actual_events, 20);

/* If status equals TX_SUCCESS, actual_events contains the
actual events obtained. */
```

**Ayrıca bkz.**

- tx_event_flags_create
- tx_event_flags_delete
- tx_event_flags_info_get
- tx_event_flags_performance_info_get
- tx_event_flags_performance_system_info_get
- tx_event_flags_set
- tx_event_flags_set_notify

### <a name="tx_event_flags_info_get"></a>tx_event_flags_info_get

Olay bayrakları grubu hakkında bilgi al

**Prototype**

```c
UINT tx_event_flags_info_get(
    TX_EVENT_FLAGS_GROUP *group_ptr,
    CHAR **name, ULONG *current_flags,
    TX_THREAD **first_suspended,
    ULONG *suspended_count,
    TX_EVENT_FLAGS_GROUP **next_group);
```

**Açıklama**

Bu hizmet, belirtilen olay bayrakları grubu hakkında bilgi alır.

**Parametreler**

- **group_ptr** Olay bayrakları Grup denetim bloğuna yönelik işaretçi.
- **ad** Olay bayrakları grubunun adına işaretçi için hedef işaretçisi.
- **current_flags** Olay bayrakları grubundaki geçerli küme bayrakları için hedef işaretçisi.
- **first_suspended** Bu olay bayrakları grubunun askıya alma listesindeki ilk iş parçacığına işaretçi için hedef işaretçisi.
- **suspended_count** Bu olay bayrakları grubunda askıya alınmış olan iş parçacığı sayısı için hedef işaretçisi.
- **next_group** Sonraki oluşturulan olay bayrakları grubunun işaretçisi için hedef işaretçisi.

> [!NOTE]
> *Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.*

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı olay grubu bilgilerini alma.
- **TX_GROUP_ERROR** (0x06) geçersiz olay grubu işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```c
TX_EVENT_FLAGS_GROUP my_event_group;
CHAR *name;
ULONG current_flags;
TX_THREAD *first_suspended;
ULONG suspended_count;
TX_EVENT_FLAGS_GROUP *next_group;
UINT status;

/* Retrieve information about the previously created
event flags group "my_event_group." */
status = tx_event_flags_info_get(&my_event_group, &name,
    &current_flags,
    &first_suspended, &suspended_count,
    &next_group);
/* If status equals TX_SUCCESS, the information requested is
valid. */
```
**Ayrıca bkz.**

- tx_event_flags_create
- tx_event_flags_delete
- tx_event_flags_get
- tx_event_flags_performance_info_get
- tx_event_flags_performance_system_info_get
- tx_event_flags_set
- tx_event_flags_set_notify

### <a name="tx_event_flags_performance_info_get"></a>tx_event_flags_performance_info_get

Olay bayrakları grubu performans bilgilerini al

### <a name="prototype"></a>Prototype

```c
UINT tx_event_flags_performance_info_get(
    TX_EVENT_FLAGS_GROUP *group_ptr,
    ULONG *sets, ULONG *gets,
    ULONG *suspensions, 
    ULONG *timeouts);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen olay bayrakları grubuyla ilgili performans bilgilerini alır.

> [!IMPORTANT]
> *Threadx kitaplığı ve uygulaması* , *performans bilgilerini döndürmek için bu hizmetin tanımlanmış* **TX_EVENT_FLAGS_ENABLE_PERFORMANCE_INFO** oluşturulmalıdır.

### <a name="parameters"></a>Parametreler

- **group_ptr** Daha önce oluşturulan olay bayrakları grubuna yönelik işaretçi.
- **Ayarlar** Bu grupta gerçekleştirilen olay bayrak kümesi isteklerinin sayısı için hedef işaretçisi.
- **alır** Bu grupta gerçekleştirilen olay bayrakları Al istekleri için hedef işaretçisi.
- **getirilmesi** Bu gruptaki iş parçacığı olay bayraklarının sayısı için hedef işaretçisi getirilmesi al.
- **zaman aşımları** Olay bayraklarının sayısı için hedefin işaretçisi bu gruptaki askıya alma zaman aşımlarını al.

> [!NOTE]
> *Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.*

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı olay bayrakları grup performansı al.
- **TX_PTR_ERROR** (0x03) geçersiz olay bayrakları grup işaretçisi.
- **TX_FEATURE_NOT_ENABLED** (0xFF) sistem, etkin performans bilgileri ile derlenmedi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="example"></a>Örnek

```c
TX_EVENT_FLAGS_GROUP my_event_flag_group;
ULONG sets;
ULONG gets;
ULONG suspensions;
ULONG timeouts;

/* Retrieve performance information on the previously created event
flag group. */
status = tx_event_flags_performance_info_get(&my_event_flag_group,
    &sets, &gets, &suspensions,
    &timeouts);

/* If status is TX_SUCCESS the performance information was successfully
retrieved. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_event_flags_create
- tx_event_flags_delete
- tx_event_flags_get
- tx_event_flags_info_get
- tx_event_flags_performance_system_info_get
- tx_event_flags_set
- tx_event_flags_set_notify

## <a name="tx_event_flags_performance_system_info_get"></a>tx_event_flags_performance_system_info_get

Performans sistemi bilgilerini al

### <a name="prototype"></a>Prototype

```c
UINT tx_event_flags_performance_system_info_get(
    ULONG *sets,
    ULONG *gets,
    ULONG *suspensions, 
    ULONG *timeouts);
```

### <a name="description"></a>Açıklama

Bu hizmet sistemdeki tüm olay bayrakları gruplarıyla ilgili performans bilgilerini alır.

> [!IMPORTANT]
> *Threadx kitaplığı ve uygulaması* , *performans bilgilerini döndürmek için bu hizmetin tanımlanmış* **TX_EVENT_FLAGS_ENABLE_PERFORMANCE_INFO** oluşturulmalıdır.

### <a name="parameters"></a>Parametreler

- **Ayarlar** Tüm gruplarda gerçekleştirilen olay bayrakları kümesi isteklerinin toplam sayısı için hedef işaretçisi.
- **alır** Tüm gruplarda gerçekleştirilen olay bayraklarının toplam sayısı için hedef işaretçisi.
- **getirilmesi** İş parçacığı olay bayraklarının toplam sayısı için hedef işaretçisi tüm gruplar üzerinde getirilmesi alır.
- **zaman aşımları** Toplam olay bayrakları sayısı için hedefin işaretçisi tüm gruplardaki askıya alınma zaman aşımlarını alır.

> [!NOTE]
> *Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.*

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı olay bayrakları sistem performansı al.
- **TX_FEATURE_NOT_ENABLED** (0xFF) sistem, etkin performans bilgileri ile derlenmedi.

### <a name="example"></a>Örnek

```c
ULONG sets;
ULONG gets;
ULONG suspensions;
ULONG timeouts;

/* Retrieve performance information on all previously created event
flag groups. */
status = tx_event_flags_performance_system_info_get(&sets, &gets,
    &suspensions, &timeouts);

/* If status is TX_SUCCESS the performance information was
successfully retrieved. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_event_flags_create
- tx_event_flags_delete
- tx_event_flags_get
- tx_event_flags_info_get
- tx_event_flags_performance_info_get
- tx_event_flags_set
- tx_event_flags_set_notify

## <a name="tx_event_flags_set"></a>tx_event_flags_set

Olay bayrakları grubundaki olay bayraklarını ayarlama

### <a name="prototype"></a>Prototype

```c
UINT tx_event_flags_set(
    TX_EVENT_FLAGS_GROUP *group_ptr,
    ULONG flags_to_set,
    UINT set_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen set-Option öğesine bağlı olarak bir olay bayrakları grubundaki olay bayraklarını ayarlar veya temizler. Olay bayrakları isteği artık karşılanan tüm askıya alınmış iş parçacıkları devam ettirildi.

### <a name="parameters"></a>Parametreler

- **group_ptr** <br>Önceden oluşturulan olay bayrakları Grup denetim bloğuna yönelik işaretçi.
- **flags_to_set** <br>Belirlenen küme seçeneğinin üzerine ayarlanacak veya temizlenecek olay bayraklarını belirtir.
- **set_option** <br>Belirtilen olay bayraklarının, grubun geçerli olay bayraklarına mi yoksa ORed mi olduğunu belirtir. Aşağıdakiler geçerli seçimlerdir:
  - **TX_AND** (0x02)
  - **TX_OR** (0x00)

  TX_AND seçilirse, belirtilen olay bayraklarının gruptaki geçerli olay bayraklarına ait olduğunu **ve** bulunduğunu belirtir. Bu seçenek, genellikle bir gruptaki olay bayraklarını temizlemek için kullanılır. Aksi takdirde, TX_OR belirtilirse, belirtilen olay bayrakları gruptaki geçerli olayla **birlikte olur.**

### <a name="return-values"></a>Dönüş Değerleri
- **TX_SUCCESS** (0x00) başarılı olay bayrakları kümesi.
- **TX_GROUP_ERROR** (0x06) olay bayrakları grubuna yönelik geçersiz işaretçi.
- **TX_OPTION_ERROR** (0x08) geçersiz set-OPTION belirtildi.

### <a name="preemption-possible"></a>Önalım mümkün

Yes

### <a name="example"></a>Örnek

```c
TX_EVENT_FLAGS_GROUP my_event_flags_group;
UINT status;

/* Set event flags 0, 4, and 8. */
status = tx_event_flags_set(&my_event_flags_group,
    0x111, TX_OR);

/* If status equals TX_SUCCESS, the event flags have been
set and any suspended thread whose request was satisfied
has been resumed. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_event_flags_create
- tx_event_flags_delete
- tx_event_flags_get
- tx_event_flags_info_get
- tx_event_flags_performance_info_get
- tx_event_flags_performance_system_info_get
- tx_event_flags_set_notify

## <a name="tx_event_flags_set_notify"></a>tx_event_flags_set_notify

Olay bayrakları ayarlandığında uygulamaya bildir

### <a name="prototype"></a>Prototype

```c
UINT tx_event_flags_set_notify(
    TX_EVENT_FLAGS_GROUP *group_ptr,
    VOID (*events_set_notify)(TX_EVENT_FLAGS_GROUP *));
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen olay bayrakları grubunda bir veya daha fazla olay bayrağı ayarlandığında çağrılan bir bildirim geri arama işlevini kaydeder. Bildirim geri çağrısının işlenmesi,

### <a name="parameters"></a>Parametreler
- **group_ptr** Daha önce oluşturulan olay bayrakları grubuna yönelik işaretçi.
- **events_set_notify** Uygulamanın olay bayrakları kümesi bildirim işlevine yönelik işaretçi. Bu değer TX_NULL, bildirim devre dışı bırakılır.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) olay bayrakları ayarlama bildiriminin başarılı kaydı.
- **TX_GROUP_ERROR** (0x06) geçersiz olay bayrakları grup işaretçisi.
- **TX_FEATURE_NOT_ENABLED** (0xFF) sistem bildirim özellikleri devre dışı olarak derlendi.

### <a name="example"></a>Örnek

```c
TX_EVENT_FLAGS_GROUP my_group;

/* Register the "my_event_flags_set_notify" function for monitoring
event flags set in the event flags group "my_group." */
status = tx_event_flags_set_notify(&my_group, my_event_flags_set_notify);

/* If status is TX_SUCCESS the event flags set notification function
was successfully registered. */
void my_event_flags_set_notify(TX_EVENT_FLAGS_GROUP *group_ptr)

/* One or more event flags was set in this group! */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_event_flags_create
- tx_event_flags_delete
- tx_event_flags_get
- tx_event_flags_info_get
- tx_event_flags_performance_info_get
- tx_event_flags_performance_system_info_get
- tx_event_flags_set

## <a name="tx_interrupt_control"></a>tx_interrupt_control

Kesmeleri etkinleştirme ve devre dışı bırakma

### <a name="prototype"></a>Prototype

```c
UINT tx_interrupt_control(UINT new_posture);
```

### <a name="description"></a>Açıklama

Bu hizmet, *new_posture* giriş parametresi tarafından belirtilen kesintileri etkinleştirilir veya devre dışı bırakır.

> [!NOTE]
> *Bu hizmet bir uygulama iş parçacığından çağrılırsa, kesme sonrası bu iş parçacığı bağlamının bir parçası olarak kalır. Örneğin, iş parçacığı kesintileri devre dışı bırakmak ve sonra askıya almak için bu yordamı çağırırsa, kesintiler yeniden devre dışı bırakılır.*

> [!WARNING]
> *Bu hizmet, başlatma sırasında kesmeleri etkinleştirmek için kullanılmamalıdır! Bunun yapılması öngörülemeyen sonuçlara neden olabilir.*

### <a name="parameters"></a>Parametreler

- **new_posture** Bu parametre, kesmelerin devre dışı veya etkin olup olmadığını belirtir. Yasal değerler **TX_INT_DISABLE** ve **TX_INT_ENABLE** içerir. Bu parametrelerin gerçek değerleri bağlantı noktasına özeldir. Bunlara ek olarak, bazı işleme mimarileri ek kesme devre dışı bırakmayı destekleyebilir.

### <a name="return-values"></a>Dönüş Değerleri
- **önceki duruşunu** Bu hizmet, çağırana bir önceki kesme sonrası döndürür. Bu, hizmet kullanıcılarının kesintiler devre dışı bırakıldıktan sonra önceki duruşunu geri yüklemesine olanak tanır.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, zamanlayıcılar ve ISRs

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```c
UINT my_old_posture;

/* Lockout interrupts */
my_old_posture = tx_interrupt_control(TX_INT_DISABLE);

/* Perform critical operations that need interrupts
locked-out.... */

/* Restore previous interrupt lockout posture. */
tx_interrupt_control(my_old_posture);
```

### <a name="see-also"></a>Ayrıca Bkz.

Yok

## <a name="tx_mutex_create"></a>tx_mutex_create

Karşılıklı dışlama mutex oluştur

### <a name="prototype"></a>Prototype

```c
UINT tx_mutex_create(
    TX_MUTEX *mutex_ptr,
    CHAR *name_ptr, 
    UINT priority_inherit);
```

### <a name="description"></a>Açıklama

Bu hizmet, kaynak koruması için iş parçacıkları arası karşılıklı dışlama için bir mutex oluşturur.

### <a name="parameters"></a>Parametreler

- **mutex_ptr** Mutex denetim bloğunun işaretçisi.
- **name_ptr** Mutex adı işaretçisi.
- **priority_inherit** Bu mutex 'in öncelik devralmayı destekleyip desteklemediğini belirtir. Bu değer TX_INHERIT, öncelikli devralma desteklenir. Ancak TX_NO_INHERIT belirtilirse, bu mutex tarafından öncelik devralımı desteklenmez.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı mutex oluşturma.
- **TX_MUTEX_ERROR** (0x1C) geçersiz MUTEX işaretçisi. İşaretçi NULL ya da mutex zaten oluşturulmuş.
- **TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.
- **TX_INHERIT_ERROR** (0x1F) geçersiz öncelik devralma parametresi.

### <a name="allowed-from"></a>İzin verilen

Başlatma ve iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```c
TX_MUTEX my_mutex;
UINT status;

/* Create a mutex to provide protection over a
common resource. */
status = tx_mutex_create(&my_mutex,"my_mutex_name",
    TX_NO_INHERIT);

/* If status equals TX_SUCCESS, my_mutex is ready for
use. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_mutex_delete
- tx_mutex_get
- tx_mutex_info_get
- tx_mutex_performance_info_get
- tx_mutex_performance_system_info_get
- tx_mutex_prioritize
- tx_mutex_put

## <a name="tx_mutex_delete"></a>tx_mutex_delete

Karşılıklı dışlama mutex 'i Sil

### <a name="prototype"></a>Prototype

```c
UINT tx_mutex_delete(TX_MUTEX *mutex_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen mutex 'i siler. Mutex bekleniyor olan tüm iş parçacıkları sürdürülür ve **TX_DELETED** dönüş durumu verilir.

> [!NOTE]
> *Silinen bir mutex 'in kullanımını önleyen uygulamanın sorumluluğundadır.*

### <a name="parameters"></a>Parametreler

- **mutex_ptr** Daha önce oluşturulmuş bir mutex işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı mutex silme.
- **TX_MUTEX_ERROR** (0x1C) geçersiz MUTEX işaretçisi.
- **TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Yes

### <a name="example"></a>Örnek

```c
TX_MUTEX my_mutex;
UINT status;

/* Delete a mutex. Assume that the mutex
has already been created. */
status = tx_mutex_delete(&my_mutex);

/* If status equals TX_SUCCESS, the mutex is
deleted. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_mutex_create
- tx_mutex_get
- tx_mutex_info_get
- tx_mutex_performance_info_get
- tx_mutex_performance_system_info_get
- tx_mutex_prioritize
- tx_mutex_put

## <a name="tx_mutex_get"></a>tx_mutex_get

Mutex sahipliğini al

### <a name="prototype"></a>Prototype

```c
UINT tx_mutex_get(
    TX_MUTEX *mutex_ptr, 
    ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen mutex 'in özel sahipliğini almaya çalışır. Çağıran iş parçacığı zaten mutex 'e sahipse, bir iç sayaç artırılır ve başarılı bir durum döndürülür.

Mutex, başka bir iş parçacığına aitse ve bu iş parçacığı daha yüksek önceliktir ve öncelikli devralma, karşılıklı dışlama oluşturma sırasında belirtilmişse, daha düşük öncelikli iş parçacığının önceliği geçici olarak çağıran iş parçacığından çıkarılır.

> [!NOTE]
> *Prioritykalýtým ile bir mutex sahibi olan düşük öncelikli iş parçacığının önceliği, zaman uyumu sahipliği sırasında asla bir dış iş parçacığı tarafından değiştirilmemelidir.*

### <a name="parameters"></a>Parametreler

- **mutex_ptr**   <br>Daha önce oluşturulmuş bir mutex işaretçisi.
- **wait_option** <br>Mutex 'in zaten başka bir iş parçacığı tarafından sahiplendiyse hizmetin nasıl davranacağını tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **TX_NO_WAIT** (0x00000000)-TX_NO_WAIT seçilmesi, başarılı olup olmamasına bakılmaksızın bu hizmetten anında geri dönüş sonucunu verir. *Bu, hizmet başlatma işleminden çağrıldığında geçerli tek seçenektir.*
  - **TX_WAIT_FOREVER** zaman aşımı değeri (0xffffffff)- **TX_WAIT_FOREVER** seçilmesi, çağıran iş parçacığının mutex kullanılabilir olana kadar süresiz olarak askıda kalmasına neden olur.
  - zaman aşımı değeri (0x00000001-0xFFFFFFFE)-sayısal bir değer (1-0xFFFFFFFE) seçilirse, mutex beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı mutex al işlemi.
- **TX_DELETED** (0x01) mutex 'i iş parçacığı askıya alınırken silindi.
- **TX_NOT_AVAILABLE** (0x1d) hizmeti, mutex 'in sahipliğini, belirtilen süre içinde beklemek için alamadı.
- **TX_WAIT_ABORTED** (0x1A) askıya alma başka bir iş parçacığı, ZAMANLAYıCı veya ISR tarafından iptal edildi.
- **TX_MUTEX_ERROR** (0x1C) geçersiz MUTEX işaretçisi.
- **TX_WAIT_ERROR** (0x04) TX_NO_WAIT dışında bir bekleme seçeneği, iş parçacığından oluşan bir çağrıda belirtildi.
- **TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

Başlatma ve iş parçacıkları ve zamanlayıcılar

### <a name="preemption-possible"></a>Önalım mümkün

Yes

### <a name="example"></a>Örnek

```c
TX_MUTEX my_mutex;
UINT status;

/* Obtain exclusive ownership of the mutex "my_mutex".
If the mutex "my_mutex" is not available, suspend until it
becomes available. */
status = tx_mutex_get(&my_mutex, TX_WAIT_FOREVER);
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_mutex_create
- tx_mutex_delete
- tx_mutex_info_get
- tx_mutex_performance_info_get
- tx_mutex_performance_system_info_get
- tx_mutex_prioritize
- tx_mutex_put

## <a name="tx_mutex_info_get"></a>tx_mutex_info_get

Mutex hakkında bilgi alın

### <a name="prototype"></a>Prototype

```c
UINT tx_mutex_info_get(
    TX_MUTEX *mutex_ptr, 
    CHAR **name,
    ULONG *count, 
    TX_THREAD **owner,
    TX_THREAD **first_suspended,
    ULONG *suspended_count, 
    TX_MUTEX **next_mutex);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen mutex 'ten bilgileri alır.

### <a name="parameters"></a>Parametreler

- **mutex_ptr** Mutex denetim bloğunun işaretçisi.
- **ad** Mutex 'in adına işaretçi için hedef işaretçisi.
- **sayı** Mutex 'in sahiplik sayısı için hedef işaretçisi.
- **sahip** Sahibi olan iş parçacığının işaretçisi için hedef işaretçisi.
- **first_suspended** Bu mutex 'in askıya alma listesindeki ilk iş parçacığına işaretçi için hedef işaretçisi.
- **suspended_count** Bu mutex üzerinde şu anda askıya alınan iş parçacığı sayısı için hedef işaretçisi.
- **next_mutex** Sonraki oluşturulan mutex işaretçisinin işaretçisi için hedef işaretçisi.

> [!NOTE]
> *Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.*

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı mutex bilgisi alma.
- **TX_MUTEX_ERROR** (0x1C) geçersiz MUTEX işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

**Örnek**

```c
TX_MUTEX my_mutex;
CHAR *name;
ULONG count;
TX_THREAD *owner;
TX_THREAD *first_suspended;
ULONG suspended_count;
TX_MUTEX *next_mutex;
UINT status;

/* Retrieve information about the previously created
mutex "my_mutex." */
status = tx_mutex_info_get(&my_mutex, &name,
    &count, &owner,
    &first_suspended, &suspended_count,
    &next_mutex);

/* If status equals TX_SUCCESS, the information requested is
valid. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_mutex_create
- tx_mutex_delete
- tx_mutex_get
- tx_mutex_performance_info_get
- tx_mutex_performance_system_info_get
- tx_mutex_prioritize
- tx_mutex_put

## <a name="tx_mutex_performance_info_get"></a>tx_mutex_performance_info_get

Mutex performans bilgilerini al

### <a name="prototype"></a>Prototype

```c
UINT tx_mutex_performance_info_get(
    TX_MUTEX *mutex_ptr, 
    ULONG *puts,
    ULONG *gets, 
    ULONG *suspensions, 
    ULONG *timeouts,
    ULONG *inversions, 
    ULONG *inheritances);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen mutex hakkında performans bilgilerini alır.

> [!IMPORTANT]
> *Işparçacığıx kitaplığı ve uygulaması ile*  * oluşturulmalıdır Bu hizmetin performans bilgilerini döndürmesi için **TX_MUTEX_ENABLE_PERFORMANCE_INFO** _ _defined. *

### <a name="parameters"></a>Parametreler

- **mutex_ptr** Önceden oluşturulmuş mutex için işaretçi.
- **koyar** Bu mutex üzerinde gerçekleştirilen PUT isteği sayısı için hedef işaretçisi.
- **alır** Bu mutex üzerinde gerçekleştirilen GET isteklerinin sayısı için hedef işaretçisi.
- **getirilmesi** Bu mutex üzerinde getirilmesi al iş parçacığı mutex 'in sayısı için hedef işaretçisi.
- **zaman aşımları** Bu mutex üzerinde askıya alma zaman aşımı sayısı için hedef işaretçisi.
- **Inversions** Bu mutex 'teki iş parçacığı önceliği ınsürümlerin sayısı için hedef işaretçisi.
- **Inheritances** Bu mutex 'teki iş parçacığı önceliği devralma işlemlerinin sayısı için hedef işaretçisi.

> [!NOTE]
> *Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.*

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı mutex performansı Get.
- **TX_PTR_ERROR** (0x03) geçersiz mutex işaretçisi.
- **TX_FEATURE_NOT_ENABLED** (0xFF) sistem, etkin performans bilgileri ile derlenmedi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="example"></a>Örnek

```c
TX_MUTEX my_mutex;
ULONG puts;
ULONG gets;
ULONG suspensions;
ULONG timeouts;
ULONG inversions;
ULONG inheritances;

/* Retrieve performance information on the previously created
mutex. */
status = tx_mutex_performance_info_get(&my_mutex_ptr, &puts, &gets,
    &suspensions, &timeouts, &inversions, &inheritances);

/* If status is TX_SUCCESS the performance information was
successfully retrieved. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_mutex_create
- tx_mutex_delete
- tx_mutex_get
- tx_mutex_info_get
- tx_mutex_performance_system_info_get
- tx_mutex_prioritize
- tx_mutex_put

## <a name="tx_mutex_performance_system_info_get"></a>tx_mutex_performance_system_info_get

Mutex sistem performans bilgilerini al

### <a name="prototype"></a>Prototype

```c
UINT tx_mutex_performance_system_info_get(
    ULONG *puts, 
    ULONG *gets,
    ULONG *suspensions, 
    ULONG *timeouts,
    ULONG *inversions, 
    ULONG *inheritances);
```

### <a name="description"></a>Açıklama

Bu hizmet, sistemdeki tüm zaman uyumu sağlayıcılar hakkındaki performans bilgilerini alır.

> [!IMPORTANT]
> *ThreadX kitaplığı ve uygulaması,*  *performans bilgilerini döndürmek için bu hizmetin tanımlanmış* TX_MUTEX_ENABLE_PERFORMANCE_INFO oluşturulmalıdır.

### <a name="parameters"></a>Parametreler

- **koyar** Tüm zaman uyumu sağlayıcılar üzerinde gerçekleştirilen put isteklerinin toplam sayısı için hedef işaretçisi.
- **alır** Tüm zaman uyumu sağlayıcılar üzerinde gerçekleştirilen GET isteklerinin toplam sayısı için hedef işaretçisi.
- **getirilmesi** Tüm zaman uyumu sağlayıcılar üzerinde getirilmesi al toplam iş parçacığı mutex için hedef işaretçisi.
- **zaman aşımları** Tüm zaman uyumu sağlayıcılar üzerinde askıya alma zaman aşımı sayısı için hedef işaretçisi.
- **Inversions** Tüm zaman uyumu sağlayıcılar üzerinde iş parçacığı önceliği Inversions 'lerin toplam sayısı için hedef işaretçisi.
- **Inheritances** Tüm zaman uyumu sağlayıcılar üzerinde iş parçacığı önceliği devralma işlemlerinin toplam sayısı için hedef işaretçisi.

> [!NOTE]
> *Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.*

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı mutex sistem performansı al.
- **TX_FEATURE_NOT_ENABLED** (0xFF) sistem, etkin performans bilgileri ile derlenmedi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="example"></a>Örnek

```c
ULONG puts;
ULONG gets;
ULONG suspensions;
ULONG timeouts;
ULONG inversions;
ULONG inheritances;

/* Retrieve performance information on all previously created
mutexes. */
status = tx_mutex_performance_system_info_get(&puts, &gets,
    &suspensions, &timeouts,
    &inversions, &inheritances);

/* If status is TX_SUCCESS the performance information was
successfully retrieved. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_mutex_create
- tx_mutex_delete
- tx_mutex_get
- tx_mutex_info_get
- tx_mutex_performance_info_get
- tx_mutex_prioritize
- tx_mutex_put

## <a name="tx_mutex_prioritize"></a>tx_mutex_prioritize

Mutex askıya alma listesini önceliklendir

### <a name="prototype"></a>Prototype

```c
UINT tx_mutex_prioritize(TX_MUTEX *mutex_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, askıya alma listesinin önünde mutex 'in sahipliği için askıya alınan en yüksek öncelik iş parçacığını koyar. Diğer tüm iş parçacıkları ' de askıya alındığı FıFO sırasında kalır.

### <a name="parameters"></a>Parametreler

- **mutex_ptr** Daha önce oluşturulmuş mutex işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı karşılıklı dışlama önceliği.
- **TX_MUTEX_ERROR** (0x1C) geçersiz MUTEX işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```c
TX_MUTEX my_mutex;
UINT status;

/* Ensure that the highest priority thread will receive
ownership of the mutex when it becomes available. */
status = tx_mutex_prioritize(&my_mutex);

/* If status equals TX_SUCCESS, the highest priority
suspended thread is at the front of the list. The
next tx_mutex_put call that releases ownership of the
mutex will give ownership to this thread and wake it
up. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_mutex_create
- tx_mutex_delete
- tx_mutex_get
- tx_mutex_info_get
- tx_mutex_performance_info_get
- tx_mutex_performance_system_info_get
- tx_mutex_put

## <a name="tx_mutex_put"></a>tx_mutex_put

Mutex 'in sahipliğini serbest bırakma

### <a name="prototype"></a>Prototype

```c
UINT tx_mutex_put(TX_MUTEX *mutex_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen mutex 'in sahiplik sayısını azaltır. Sahiplik sayısı sıfırsa, mutex kullanılabilir hale getirilir.

> [!NOTE]
> *Karşılıklı dışlama oluşturma sırasında öncelik devralma seçilmişse, serbest bırakma iş parçacığının önceliği, başlangıçta mutex 'in sahipliğini aldığında sahip olduğu önceliğe geri yüklenecektir. Mutex 'in sahipliği sırasında, serbest bırakma iş parçacığında yapılan diğer tüm öncelik değişiklikleri geri alınabilir.*

### <a name="parameters"></a>Parametreler
- daha önce oluşturulmuş olan mutex Işaretçisine mutex_ptr.

### <a name="return-values"></a>Dönüş Değerleri
- **TX_SUCCESS** (0x00) başarılı mutex sürümü.
- **TX_NOT_OWNED** (0x1E) mutex 'i arayana ait değil.
- **TX_MUTEX_ERROR** (0x1C) MUTEX için geçersiz işaretçi.
- **TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

Başlatma ve iş parçacıkları ve zamanlayıcılar

### <a name="preemption-possible"></a>Önalım mümkün

Yes

### <a name="example"></a>Örnek

```c
TX_MUTEX my_mutex;
UINT status;

/* Release ownership of "my_mutex." */
status = tx_mutex_put(&my_mutex);

/* If status equals TX_SUCCESS, the mutex ownership
count has been decremented and if zero, released. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_mutex_create
- tx_mutex_delete
- tx_mutex_get
- tx_mutex_info_get
- tx_mutex_performance_info_get
- tx_mutex_performance_system_info_get
- tx_mutex_prioritize

## <a name="tx_queue_create"></a>tx_queue_create

İleti kuyruğu oluştur

### <a name="prototype"></a>Prototype

```c
UINT tx_queue_create(
    TX_QUEUE *queue_ptr, 
    CHAR *name_ptr,
    UINT message_size,
    VOID *queue_start, 
    ULONG queue_size);
```

### <a name="description"></a>Açıklama

Bu hizmet, genellikle karşılıklı iş parçacığı iletişimi için kullanılan bir ileti kuyruğu oluşturur. Toplam ileti sayısı, belirtilen ileti boyutundan ve sıradaki toplam bayt sayısından hesaplanır.

> [!NOTE]
> *Kuyruğun bellek alanında belirtilen toplam bayt sayısı, belirtilen ileti boyutuyla eşit olarak bölünemiyor ise, bellek alanındaki kalan baytlar kullanılmaz.*

### <a name="parameters"></a>Parametreler

- **queue_ptr** İleti kuyruğu denetim bloğunun işaretçisi.
- **name_ptr** İleti sırasının adı işaretçisi.
- **message_size** Kuyruktaki her iletinin boyutunu belirtir. İleti boyutları 1 32 bitlik sözcükten 16 32 bit sözcüklere kadar değişir. Geçerli ileti boyutu seçenekleri, 1 ile 16 arasında (dahil) sayısal değerlerdir.
- **queue_start** İleti sırasının başlangıç adresi. Başlangıç adresi ULONG veri türünün boyutuna hizalanmalıdır.
- **queue_size** İleti kuyruğu için kullanılabilen toplam bayt sayısı.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı ileti kuyruğu oluşturma.
- **TX_QUEUE_ERROR** (0x09) geçersiz ileti kuyruğu işaretçisi. İşaretçi NULL ya da sıra zaten oluşturulmuş.
- **TX_PTR_ERROR** (0x03) ileti sırasının başlangıç adresi geçersiz.
- **TX_SIZE_ERROR** (0x05) Ileti sırasının boyutu geçersiz.
- **TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

Başlatma ve iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```c
TX_QUEUE my_queue;
UINT status;

/* Create a message queue whose total size is 2000 bytes
starting at address 0x300000. Each message in this
queue is defined to be 4 32-bit words long. */
status = tx_queue_create(&my_queue, "my_queue_name",
    4, (VOID *) 0x300000, 2000);

/* If status equals TX_SUCCESS, my_queue contains room
for storing 125 messages (2000 bytes/ 16 bytes per
message). */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_queue_delete
- tx_queue_flush
- tx_queue_front_send
- tx_queue_info_get
- tx_queue_performance_info_get
- tx_queue_performance_system_info_get
- tx_queue_prioritize
- tx_queue_receive
- tx_queue_send
- tx_queue_send_notify

## <a name="tx_queue_delete"></a>tx_queue_delete

İleti kuyruğunu sil

### <a name="prototype"></a>Prototype

```c
UINT tx_queue_delete(TX_QUEUE *queue_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen ileti sırasını siler. Bu kuyruktan bir ileti beklemeden askıya alınmış tüm iş parçacıkları sürdürülür ve TX_DELETED dönüş durumu verilir.

>[!IMPORTANT]
> *Uygulama, kuyruk silinmeden önce bu sıra için gönderilen bildirim geri çağrısının tamamlandı (veya devre dışı) olduğundan emin olmalıdır. Ayrıca, uygulamanın, silinen bir kuyruğun gelecekteki kullanımını önlemesi gerekir.* <br><br>*Ayrıca, bu hizmet tamamlandıktan sonra kullanılabilir olan Kuyrukla ilişkili bellek alanını yönetmek için uygulamanın sorumluluğundadır.*

### <a name="parameters"></a>Parametreler

- **queue_ptr** Önceden oluşturulmuş bir ileti kuyruğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı ileti sırası silme işlemi.
- **TX_QUEUE_ERROR** (0x09) geçersiz ileti kuyruğu işaretçisi.
- **TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Yes

### <a name="example"></a>Örnek

```c
TX_QUEUE my_queue;
UINT status;

/* Delete entire message queue. Assume that the queue
has already been created with a call to
tx_queue_create. */
status = tx_queue_delete(&my_queue);

/* If status equals TX_SUCCESS, the message queue is
deleted. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_queue_create
- tx_queue_flush
- tx_queue_front_send
- tx_queue_info_get
- tx_queue_performance_info_get
- tx_queue_performance_system_info_get
- tx_queue_prioritize
- tx_queue_receive
- tx_queue_send
- tx_queue_send_notify

## <a name="tx_queue_flush"></a>tx_queue_flush

İleti sırasındaki boş iletiler

### <a name="prototype"></a>Prototype

```c
UINT tx_queue_flush(TX_QUEUE *queue_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen ileti kuyruğunda depolanan tüm iletileri siler.

Sıra doluysa, askıya alınmış tüm iş parçacıklarının iletileri atılır. Askıya alınan her iş parçacığı daha sonra ileti gönderme işleminin başarılı olduğunu belirten bir dönüş durumuyla sürdürülür. Sıra boşsa, bu hizmet hiçbir şey yapmaz.

### <a name="parameters"></a>Parametreler

- **queue_ptr** Önceden oluşturulmuş bir ileti kuyruğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı ileti kuyruğu Temizleme.
- **TX_QUEUE_ERROR** (0x09) geçersiz ileti kuyruğu işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="preemption-possible"></a>Önalım mümkün

Yes

### <a name="example"></a>Örnek

```c
TX_QUEUE my_queue;
UINT status;

/* Flush out all pending messages in the specified message
queue. Assume that the queue has already been created
with a call to tx_queue_create. */
status = tx_queue_flush(&my_queue);

/* If status equals TX_SUCCESS, the message queue is
empty. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_queue_create
- tx_queue_delete
- tx_queue_front_send
- tx_queue_info_get
- tx_queue_performance_info_get
- tx_queue_performance_system_info_get
- tx_queue_prioritize
- tx_queue_receive
- tx_queue_send
- tx_queue_send_notify

## <a name="tx_queue_front_send"></a>tx_queue_front_send

Kuyruğun önüne ileti gönder

### <a name="prototype"></a>Prototype

```c
UINT tx_queue_front_send(
    TX_QUEUE *queue_ptr,
    VOID *source_ptr, 
    ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen ileti sırasının ön konumuna bir ileti gönderir. İleti, kaynak işaretçi tarafından belirtilen bellek alanından kuyruğun önüne **kopyalanır** .

### <a name="parameters"></a>Parametreler

- **queue_ptr** <br>İleti kuyruğu denetim bloğunun işaretçisi.
- **source_ptr** <br>İleti işaretçisi.
- **wait_option**  <br>İleti kuyruğu doluysa hizmetin nasıl davranacağını tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **TX_NO_WAIT** (0x00000000)-TX_NO_WAIT seçilmesi, başarılı olup olmamasına bakılmaksızın bu hizmetten anında geri dönüş sonucunu verir. *Bu, hizmet iş parçacığından çağrıldığında tek geçerli seçenektir; Örneğin, başlatma, süreölçer veya ıSR.*
  - **TX_WAIT_FOREVER** (0xffffffff)-TX_WAIT_FOREVER seçilmesi, sıraya alan alana kadar çağıran iş parçacığının sonsuza kadar süresiz olarak askıda kalmasına neden olur.
  - zaman aşımı değeri (0x00000001-0xFFFFFFFE)-sayısal bir değer (1-0xFFFFFFFE) seçilirse, kuyrukta Oda beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) Ileti gönderme başarılı oldu.
- **TX_DELETED** (0x01) ileti kuyruğu, iş parçacığı askıya alınırken silindi.
- **TX_QUEUE_FULL** (0x0B) hizmeti, belirtilen süre boyunca sıra dolu olduğundan ileti gönderemedi.
- **TX_WAIT_ABORTED** (0x1A) askıya alma başka bir iş parçacığı, ZAMANLAYıCı veya ISR tarafından iptal edildi.
- **TX_QUEUE_ERROR** (0x09) geçersiz ileti kuyruğu işaretçisi.
- **TX_PTR_ERROR** (0x03) Ileti için geçersiz kaynak işaretçisi.
- **TX_WAIT_ERROR** (0x04) TX_NO_WAIT dışında bir bekleme seçeneği, iş parçacığından oluşan bir çağrıda belirtildi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="preemption-possible"></a>Önalım mümkün

Yes

### <a name="example"></a>Örnek

```c
TX_QUEUE my_queue;
UINT status;
ULONG my_message[4];

/* Send a message to the front of "my_queue." Return
immediately, regardless of success. This wait
option is used for calls from initialization, timers,
and ISRs. */
status = tx_queue_front_send(&my_queue, my_message,
    TX_NO_WAIT);

/* If status equals TX_SUCCESS, the message is at the front
of the specified queue. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_queue_create
- tx_queue_delete
- tx_queue_flush
- tx_queue_info_get
- tx_queue_performance_info_get
- tx_queue_performance_system_info_get
- tx_queue_prioritize
- tx_queue_receive
- tx_queue_send
- tx_queue_send_notify

## <a name="tx_queue_info_get"></a>tx_queue_info_get

Kuyruk hakkında bilgi alma

### <a name="prototype"></a>Prototype

```c
UINT tx_queue_info_get(
    TX_QUEUE *queue_ptr, 
    CHAR **name,
    ULONG *enqueued, 
    ULONG *available_storage
    TX_THREAD **first_suspended, 
    ULONG *suspended_count,
    TX_QUEUE **next_queue);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen ileti kuyruğu hakkında bilgi alır.

### <a name="parameters"></a>Parametreler

- **queue_ptr** Önceden oluşturulmuş bir ileti kuyruğu işaretçisi.
- **ad** Kuyruğun adına işaretçi için hedef işaretçisi.
- **sıraya alındı** Şu anda kuyruktaki ileti sayısı için hedef işaretçisi.
- **available_storage** Kuyruğun Şu anda alanı bulunan ileti sayısı için hedef işaretçisi.
- **first_suspended** Bu sıranın askıya alma listesindeki iş parçacığına işaretçi için hedef işaretçisi.
- **suspended_count** Bu sırada askıya alınmış olan iş parçacığı sayısı için hedef işaretçisi.
- **next_queue** Sonraki oluşturulan sıranın işaretçisi için hedef işaretçisi.

> [!NOTE]
> *Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.*

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı kuyruk bilgileri alma.
- **TX_QUEUE_ERROR** (0x09) geçersiz ileti kuyruğu işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```c
TX_QUEUE my_queue;
CHAR *name;
ULONG enqueued;
ULONG available_storage;
TX_THREAD *first_suspended;
ULONG suspended_count;
TX_QUEUE *next_queue;
UINT status;

/* Retrieve information about the previously created
message queue "my_queue." */
status = tx_queue_info_get(&my_queue, &name,
    &enqueued, &available_storage,
    &first_suspended, &suspended_count,
    &next_queue);

/* If status equals TX_SUCCESS, the information requested is
valid. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_queue_create
- tx_queue_delete
- tx_queue_flush
- tx_queue_front_send
- tx_queue_performance_info_get
- tx_queue_performance_system_info_get
- tx_queue_prioritize
- tx_queue_receive
- tx_queue_send
- tx_queue_send_notify

## <a name="tx_queue_performance_info_get"></a>tx_queue_performance_info_get

Sıra performans bilgilerini al

### <a name="prototype"></a>Prototype

```c
UINT tx_queue_performance_info_get(
    TX_QUEUE *queue_ptr,
    ULONG *messages_sent, 
    ULONG *messages_received,
    ULONG *empty_suspensions, 
    ULONG *full_suspensions,
    ULONG *full_errors, 
    ULONG *timeouts);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen sıra hakkındaki performans bilgilerini alır.

> [!IMPORTANT]
> *Işparçacığıx kitaplığı ve uygulaması ile*  * oluşturulmalıdır Bu hizmetin performans bilgilerini döndürmesi için **TX_QUEUE_ENABLE_PERFORMANCE_INFO** _ _defined. *

### <a name="parameters"></a>Parametreler

- **queue_ptr** Önceden oluşturulmuş sıranın işaretçisi.
- **messages_sent** Bu kuyrukta gerçekleştirilen gönderme isteklerinin sayısı için hedef işaretçisi.
- **messages_received** Bu kuyrukta gerçekleştirilen alma isteği sayısı için hedef işaretçisi.
- **empty_suspensions** Bu kuyruktaki kuyruk boş getirilmesi sayısı için hedef işaretçisi.
- **full_suspensions** Bu kuyruktaki sıra Full getirilmesi sayısı için hedef işaretçisi.
- **full_errors** Bu kuyruktaki sıranın tam hatalarının sayısı için hedef işaretçisi.
- **zaman aşımları** Bu kuyruktaki iş parçacığı askıya alma zaman aşımı sayısı için hedef işaretçisi.

> [!NOTE]
> *Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.*

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı kuyruk performansı alma.
- **TX_PTR_ERROR** (0x03) geçersiz kuyruk işaretçisi.
- **TX_FEATURE_NOT_ENABLED** (0xFF) sistem, etkin performans bilgileri ile derlenmedi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="example"></a>Örnek

```c
TX_QUEUE my_queue;
ULONG messages_sent;
ULONG messages_received;
ULONG empty_suspensions;
ULONG full_suspensions;
ULONG full_errors;
ULONG timeouts;

/* Retrieve performance information on the previously created
queue. */
status = tx_queue_performance_info_get(&my_queue, &messages_sent,
    &messages_received, &empty_suspensions,
    &full_suspensions, &full_errors, &timeouts);

/* If status is TX_SUCCESS the performance information was
successfully retrieved. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_queue_create
- tx_queue_delete
- tx_queue_flush
- tx_queue_front_send
- tx_queue_info_get
- tx_queue_performance_system_info_get
- tx_queue_prioritize
- tx_queue_receive
- tx_queue_send
- tx_queue_send_notify

## <a name="tx_queue_performance_system_info_get"></a>tx_queue_performance_system_info_get

Sıra sistemi performans bilgilerini al

### <a name="prototype"></a>Prototype

```c
UINT tx_queue_performance_system_info_get(
    ULONG *messages_sent,
    ULONG *messages_received, 
    ULONG *empty_suspensions,
    ULONG *full_suspensions, 
    ULONG *full_errors,
    ULONG *timeouts);
```

### <a name="description"></a>Açıklama

Bu hizmet sistemdeki tüm kuyruklarla ilgili performans bilgilerini alır.

> [!IMPORTANT]
> *Işparçacığıx kitaplığı ve uygulaması ile*  * oluşturulmalıdır Bu hizmetin performans bilgilerini döndürmesi için **TX_QUEUE_ENABLE_PERFORMANCE_INFO** _ _defined. *

### <a name="parameters"></a>Parametreler

- **messages_sent** Tüm kuyruklarda gerçekleştirilen gönderme isteklerinin toplam sayısı için hedef işaretçisi.
- **messages_received** Tüm kuyruklarda gerçekleştirilen Alım isteklerinin toplam sayısı için hedef işaretçisi.
- **empty_suspensions** Tüm kuyruklarda boş sıranın toplam sayısı için hedef işaretçisi. getirilmesi.
- **full_suspensions** Tüm kuyruklarda toplam Queue Full getirilmesi için hedef işaretçisi.
- **full_errors** Tüm sıralarda toplam sıra tam hatalarının toplam sayısı için hedef işaretçisi.
- **zaman aşımları** Tüm sıralarda toplam iş parçacığı askıya alma zaman aşımı sayısı için hedef işaretçisi.

> [!NOTE]
> *Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.*

**Dönüş değerleri**

- **TX_SUCCESS** (0x00) başarılı kuyruk sistem performansı alma.
- **TX_FEATURE_NOT_ENABLED** (0xFF) sistem, etkin performans bilgileri ile derlenmedi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="example"></a>Örnek

```c
ULONG messages_sent;
ULONG messages_received;
ULONG empty_suspensions;
ULONG full_suspensions;
ULONG full_errors;
ULONG timeouts;

/* Retrieve performance information on all previously created
queues. */
status = tx_queue_performance_system_info_get(&messages_sent,
    &messages_received, &empty_suspensions,
    &full_suspensions, &full_errors, &timeouts);

/* If status is TX_SUCCESS the performance information was
successfully retrieved. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_queue_create
- tx_queue_delete
- tx_queue_flush
- tx_queue_front_send
- tx_queue_info_get
- tx_queue_performance_info_get
- tx_queue_prioritize
- tx_queue_receive
- tx_queue_send
- tx_queue_send_notify

## <a name="tx_queue_prioritize"></a>tx_queue_prioritize

Sıra askıya alma listesini önceliklendir

### <a name="prototype"></a>Prototype

```c
UINT tx_queue_prioritize(TX_QUEUE *queue_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, askıya alma listesinin önünde bu kuyruğa bir ileti (veya bir ileti yerleştirmek için) için askıya alınan en yüksek öncelik iş parçacığını yerleştirir.

Diğer tüm iş parçacıkları ' de askıya alındığı FıFO sırasında kalır.

### <a name="parameters"></a>Parametreler

- **queue_ptr** Önceden oluşturulmuş bir ileti kuyruğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı kuyruk önceliği belirleme.
- **TX_QUEUE_ERROR** (0x09) geçersiz ileti kuyruğu işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```c
TX_QUEUE my_queue;
UINT status;

/* Ensure that the highest priority thread will receive
the next message placed on this queue. */
status = tx_queue_prioritize(&my_queue);

/* If status equals TX_SUCCESS, the highest priority
suspended thread is at the front of the list. The
next tx_queue_send or tx_queue_front_send call made
to this queue will wake up this thread. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_queue_create
- tx_queue_delete
- tx_queue_flush
- tx_queue_front_send
- tx_queue_info_get
- tx_queue_performance_info_get
- tx_queue_performance_system_info_get
- tx_queue_receive
- tx_queue_send
- tx_queue_send_notify

## <a name="tx_queue_receive"></a>tx_queue_receive

İleti kuyruğundan ileti al

### <a name="prototype"></a>Prototype

```c
UINT tx_queue_receive(
    TX_QUEUE *queue_ptr,
    VOID *destination_ptr, 
    ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen ileti sırasından bir ileti alır. Alınan ileti, kuyruktan hedef işaretçi tarafından belirtilen bellek alanına **kopyalanır** . Bu ileti daha sonra kuyruktan kaldırılır.

> [!IMPORTANT]
> *Belirtilen hedef bellek alanı iletiyi tutabilecek kadar büyük olmalıdır; yani, ileti hedefi tarafından*  * işaret edilen **destination_ptr** _ _must en azından bu sıranın ileti boyutu kadar büyük olmalıdır. Aksi takdirde, hedef yeterince büyük değilse, aşağıdaki bellek alanında bellek bozulması oluşur. *

### <a name="parameters"></a>Parametreler

- **queue_ptr** <br>Önceden oluşturulmuş bir ileti kuyruğu işaretçisi.
- **destination_ptr** <br>İletinin kopyalanacağı konum.
- **wait_option** <br>İleti sırası boş ise hizmetin nasıl davranacağını tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **TX_NO_WAIT** (0x00000000)-TX_NO_WAIT seçilmesi, başarılı olup olmamasına bakılmaksızın bu hizmetten anında geri dönüş sonucunu verir. Bu, hizmet iş parçacığından çağrıldığında tek geçerli seçenektir; Örneğin, başlatma, süreölçer veya ıSR.
  - **TX_WAIT_FOREVER** (0xffffffff)-TX_WAIT_FOREVER seçme, çağıran iş parçacığının bir ileti kullanılabilir olana kadar süresiz olarak askıda kalmasına neden olur.
  - zaman aşımı değeri (0x00000001-0xFFFFFFFE)-sayısal bir değer (1-0xFFFFFFFE) seçildiğinde, ileti beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.

### <a name="return-values"></a>Dönüş Değerleri

- İleti başarıyla alımı **TX_SUCCESS** (0x00).
- **TX_DELETED** (0x01) ileti kuyruğu, iş parçacığı askıya alınırken silindi.
- **TX_QUEUE_EMPTY** (0X0a) hizmeti, belirtilen sürenin süresi boyunca sıra boş olduğundan bir iletiyi alamadı.
- **TX_WAIT_ABORTED** (0x1A) askıya alma başka bir iş parçacığı, ZAMANLAYıCı veya ISR tarafından iptal edildi.
- **TX_QUEUE_ERROR** (0x09) geçersiz ileti kuyruğu işaretçisi.
- **TX_PTR_ERROR** (0x03) Ileti için geçersiz hedef işaretçisi.
- **TX_WAIT_ERROR** (0x04) TX_NO_WAIT dışında bir bekleme seçeneği, iş parçacığından oluşan bir çağrıda belirtildi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="preemption-possible"></a>Önalım mümkün

Yes

### <a name="example"></a>Örnek

```c
TX_QUEUE my_queue;
UINT status;
ULONG my_message[4];

/* Retrieve a message from "my_queue." If the queue is
empty, suspend until a message is present. Note that
this suspension is only possible from application
threads. */
status = tx_queue_receive(&my_queue, my_message,
    TX_WAIT_FOREVER);

/* If status equals TX_SUCCESS, the message is in
"my_message." */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_queue_create
- tx_queue_delete
- tx_queue_flush
- tx_queue_front_send
- tx_queue_info_get
- tx_queue_performance_info_get
- tx_queue_performance_system_info_get
- tx_queue_prioritize
- tx_queue_send
- tx_queue_send_notify

## <a name="tx_queue_send"></a>tx_queue_send

İletiyi ileti kuyruğuna gönder

### <a name="prototype"></a>Prototype

```c
UINT tx_queue_send(
    TX_QUEUE *queue_ptr,
    VOID *source_ptr, 
    ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen ileti kuyruğuna bir ileti gönderir. Gönderilen ileti, kaynak işaretçi tarafından belirtilen bellek alanından kuyruğa **kopyalanır** .

### <a name="parameters"></a>Parametreler
- **queue_ptr** <br>Önceden oluşturulmuş bir ileti kuyruğu işaretçisi.
- **source_ptr** <br>İleti işaretçisi.
- **wait_option** <br>İleti kuyruğu doluysa hizmetin nasıl davranacağını tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **TX_NO_WAIT** (0x00000000)-TX_NO_WAIT seçilmesi, başarılı olup olmamasına bakılmaksızın bu hizmetten anında geri dönüş sonucunu verir. *Bu, hizmet iş parçacığından çağrıldığında geçerli olan tek seçenektir; Örneğin, başlatma, süreölçer veya ISR*.
  - **TX_WAIT_FOREVER** (0xffffffff)-TX_WAIT_FOREVER seçilmesi, sıraya alan alana kadar çağıran iş parçacığının sonsuza kadar süresiz olarak askıda kalmasına neden olur.
  - zaman aşımı değeri (0x00000001-0xFFFFFFFE)-sayısal bir değer (1-0xFFFFFFFE) seçilirse, kuyrukta Oda beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) Ileti gönderme başarılı oldu.
- **TX_DELETED** (0x01) ileti kuyruğu, iş parçacığı askıya alınırken silindi.
- **TX_QUEUE_FULL** (0x0B) hizmeti, belirtilen süre boyunca sıra dolu olduğundan ileti gönderemedi.
- **TX_WAIT_ABORTED** (0x1A) askıya alma başka bir iş parçacığı, ZAMANLAYıCı veya ISR tarafından iptal edildi.
- **TX_QUEUE_ERROR** (0x09) geçersiz ileti kuyruğu işaretçisi.
- **TX_PTR_ERROR** (0x03) Ileti için geçersiz kaynak işaretçisi.
- **TX_WAIT_ERROR** (0x04) TX_NO_WAIT dışında bir bekleme seçeneği, iş parçacığından oluşan bir çağrıda belirtildi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="preemption-possible"></a>Önalım mümkün

Yes

### <a name="example"></a>Örnek

```c
TX_QUEUE my_queue;
UINT status;
ULONG my_message[4];

/* Send a message to "my_queue." Return immediately,
regardless of success. This wait option is used for
calls from initialization, timers, and ISRs. */
status = tx_queue_send(&my_queue, my_message, TX_NO_WAIT);

/* If status equals TX_SUCCESS, the message is in the
queue. */
```

**Ayrıca bkz.**

- tx_queue_create
- tx_queue_delete
- tx_queue_flush
- tx_queue_front_send
- tx_queue_info_get
- tx_queue_performance_info_get
- tx_queue_performance_system_info_get
- tx_queue_prioritize
- tx_queue_receive
- tx_queue_send_notify

## <a name="tx_queue_send_notify"></a>tx_queue_send_notify

İleti kuyruğa gönderildiğinde uygulamayı bilgilendir

### <a name="prototype"></a>Prototype

```c
UINT tx_queue_send_notify(
    TX_QUEUE *queue_ptr,
    VOID (*queue_send_notify)(TX_QUEUE *));
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen sıraya bir ileti gönderildiğinde çağrılan bir bildirim geri arama işlevini kaydeder. Bildirim geri çağrısının işlenmesi uygulama tarafından tanımlanır.

>[!NOTE]
> *Uygulamanın kuyruk gönderme bildirimi geri çağırması, askıya alma seçeneğiyle herhangi bir ThreadX API çağrısı yapılmasına izin verilmez.*

### <a name="parameters"></a>Parametreler

- **queue_ptr** Önceden oluşturulmuş sıranın işaretçisi.
- **queue_send_notify** Uygulamanın kuyruk gönderme bildirimi işlevine yönelik işaretçi. Bu değer TX_NULL, bildirim devre dışı bırakılır.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) kuyruk gönderme bildiriminin başarıyla kaydı.
- **TX_QUEUE_ERROR** (0x09) geçersiz kuyruk işaretçisi.
- **TX_FEATURE_NOT_ENABLED** (0xFF) sistem bildirim özellikleri devre dışı olarak derlendi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="example"></a>Örnek

```c
TX_QUEUE my_queue;
/* Register the "my_queue_send_notify" function for monitoring
messages sent to the queue "my_queue." */
status = tx_queue_send_notify(&my_queue, my_queue_send_notify);

/* If status is TX_SUCCESS the queue send notification function was
successfully registered. */
void my_queue_send_notify(TX_QUEUE *queue_ptr)
{
    /* A message was just sent to this queue! */
}
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_queue_create
- tx_queue_delete
- tx_queue_flush
- tx_queue_front_send
- tx_queue_info_get
- tx_queue_performance_info_get
- tx_queue_performance_system_info_get
- tx_queue_prioritize
- tx_queue_receive
- tx_queue_send

## <a name="tx_semaphore_ceiling_put"></a>tx_semaphore_ceiling_put

Tavan ile sayım semafora bir örnek yerleştirme

### <a name="prototype"></a>Prototype

```c
UINT tx_semaphore_ceiling_put(
    TX_SEMAPHORE *semaphore_ptr,
    ULONG ceiling);
```

### <a name="description"></a>Açıklama

Bu hizmet, gerçekte belirtilen sayım semafora bir örnek koyar ve bu da gerçekteki sayım semaforu bir tane artırır. Sayım semaforun geçerli değeri belirtilen tavan değerinden büyük veya bu değere eşitse, örnek yerleştirmeyecektir ve bir TX_CEILING_EXCEEDED hatası döndürülür.

### <a name="parameters"></a>Parametreler

- **semaphore_ptr** Daha önce oluşturulan semafor işaretçisi.
- **tavan** Semafor için izin verilen üst sınır (geçerli değer aralığı 1 ile 0xFFFFFFFF arasında).

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS (0x00)** Başarılı semafor tavan koyma.
- **TX_CEILING_EXCEEDED** (0x21) PUT isteği tavan aşıyor.
- **TX_INVALID_CEILING** (0x22) tavan için geçersiz sıfır değeri sağlandı.
- **TX_SEMAPHORE_ERROR** (0x0C) geçersiz semafor işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="example"></a>Örnek

```c
TX_SEMAPHORE my_semaphore;

/* Increment the counting semaphore "my_semaphore" but make sure
that it never exceeds 7 as specified in the call. */
status = tx_semaphore_ceiling_put(&my_semaphore, 7);

/* If status is TX_SUCCESS the semaphore count has been
incremented. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_semaphore_create
- tx_semaphore_delete
- tx_semaphore_get
- tx_semaphore_info_get
- tx_semaphore_performance_info_get
- tx_semaphore_performance_system_info_get
- tx_semaphore_prioritize
- tx_semaphore_put
- tx_semaphore_put_notify

## <a name="tx_semaphore_create"></a>tx_semaphore_create

Sayım semaforu oluştur

### <a name="prototype"></a>Prototype

```c
UINT tx_semaphore_create(
    TX_SEMAPHORE *semaphore_ptr,
    CHAR *name_ptr, 
    ULONG initial_count);
```

### <a name="description"></a>Açıklama

Bu hizmet, iş parçacıkları arası eşitleme için bir sayım semaforu oluşturur. İlk semafor sayısı bir giriş parametresi olarak belirtilir.

### <a name="parameters"></a>Parametreler

- **semaphore_ptr** Semafor denetim bloğu işaretçisi.
- **name_ptr** Semafor adı işaretçisi.
- **initial_count** Bu semafor için başlangıç sayısını belirtir. Yasal değerler 0x00000000 ile 0xFFFFFFFF arasında değişir.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı semafor oluşturma.
- **TX_SEMAPHORE_ERROR** (0x0C) geçersiz semafor işaretçisi. İşaretçi NULL ya da semafor zaten oluşturulmuş.
- **TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

Başlatma ve iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```c
TX_SEMAPHORE my_semaphore;
UINT status;

/* Create a counting semaphore whose initial value is 1.
This is typically the technique used to make a binary
semaphore. Binary semaphores are used to provide
protection over a common resource. */
status = tx_semaphore_create(&my_semaphore,
    "my_semaphore_name", 1);

/* If status equals TX_SUCCESS, my_semaphore is ready for
use. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_semaphore_ceiling_put
- tx_semaphore_delete
- tx_semaphore_get
- tx_semaphore_info_get
- tx_semaphore_performance_info_get
- tx_semaphore_performance_system_info_get
- tx_semaphore_prioritize
- tx_semaphore_put
- tx_semaphore_put_notify

## <a name="tx_semaphore_delete"></a>tx_semaphore_delete

Sayım semaforu Sil

### <a name="prototype"></a>Prototype
```c
UINT tx_semaphore_delete(TX_SEMAPHORE *semaphore_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen sayım semaforu siler. Bir semafor örneği için bekleyen askıya alınan tüm iş parçacıkları sürdürülür ve TX_DELETED dönüş durumu verilir.

> [!IMPORTANT]
> *Uygulama, semafor silinmeden önce Bu semafor için bir put bildirimi geri çağrısının tamamlandığından (veya devre dışı bırakıldığından) emin olmalıdır. Ayrıca, uygulamanın, silinen semaforun gelecekteki tüm kullanımını önlemesi gerekir.*

### <a name="parameters"></a>Parametreler

- **semaphore_ptr** Daha önce oluşturulmuş bir semafor işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) semafor silme işlemi başarılı sayılıyor.
- **TX_SEMAPHORE_ERROR** (0x0C) geçersiz sayma semaforu işaretçisi.
- **TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Yes

### <a name="example"></a>Örnek

```c
TX_SEMAPHORE my_semaphore;
UINT status;

/* Delete counting semaphore. Assume that the counting
semaphore has already been created. */
status = tx_semaphore_delete(&my_semaphore);

/* If status equals TX_SUCCESS, the counting semaphore is
deleted. */
```

**Ayrıca bkz.**

- tx_semaphore_ceiling_put
- tx_semaphore_create
- tx_semaphore_get
- tx_semaphore_info_get
- tx_semaphore_performance_info_get
- tx_semaphore_performance_system_info_get
- tx_semaphore_prioritize
- tx_semaphore_put
- tx_semaphore_put_notify

## <a name="tx_semaphore_get"></a>tx_semaphore_get

Sayım semafordan örnek al

### <a name="prototype"></a>Prototype

```c
UINT tx_semaphore_get(
    TX_SEMAPHORE *semaphore_ptr,
    ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen sayım semafordan bir örnek (tek bir sayı) alır. Sonuç olarak, belirtilen Semaforun sayısı bir ile azaltılır.

### <a name="parameters"></a>Parametreler

- **semaphore_ptr** <br>Önceden oluşturulmuş bir sayım semaforu işaretçisi.
- **wait_option** <br>Semaforun kullanılabilir bir örneği yoksa hizmetin nasıl davranacağını tanımlar; Yani, semafor sayısı sıfırdır. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **TX_NO_WAIT** (0x00000000)-TX_NO_WAIT seçilmesi, başarılı olup olmamasına bakılmaksızın bu hizmetten anında geri dönüş sonucunu verir. *Bu, hizmet iş parçacığından çağrıldığında tek geçerli seçenektir; Örneğin, başlatma, süreölçer veya ıSR.*
  - **TX_WAIT_FOREVER** (0xffffffff)-TX_WAIT_FOREVER seçilmesi, çağıran iş parçacığının bir semafor örneği kullanılabilir olana kadar süresiz olarak askıda kalmasına neden olur.
  - zaman aşımı değeri (0x00000001-0xFFFFFFFE)-sayısal bir değer (1-0xFFFFFFFE) seçildiğinde, bir semafor örneği beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) bir semafor örneğinin başarıyla alımı.
- İş parçacığı askıya alınırken **TX_DELETED** (0x01) sayım semaforu silindi.
- **TX_NO_INSTANCE** (0x0D) hizmeti, sayım semaforun bir örneğini alamadı (semafor sayısı, belirtilen süre içinde beklenecek şekilde sıfır).
- **TX_WAIT_ABORTED** (0x1A) askıya alma başka bir iş parçacığı, ZAMANLAYıCı veya ISR tarafından iptal edildi.
- **TX_SEMAPHORE_ERROR** (0x0C) geçersiz sayma semaforu işaretçisi.
- **TX_WAIT_ERROR** (0x04) TX_NO_WAIT dışında bir bekleme seçeneği, iş parçacığından oluşan bir çağrıda belirtildi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="preemption-possible"></a>Önalım mümkün

Yes

### <a name="example"></a>Örnek

```c
TX_SEMAPHORE my_semaphore;
UINT status;

/* Get a semaphore instance from the semaphore
"my_semaphore." If the semaphore count is zero,
suspend until an instance becomes available.
Note that this suspension is only possible from
application threads. */
status = tx_semaphore_get(&my_semaphore, TX_WAIT_FOREVER);

/* If status equals TX_SUCCESS, the thread has obtained
an instance of the semaphore. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_semaphore_ceiling_put
- tx_semaphore_create
- tx_semahore_delete
- tx_semaphore_info_get
- tx_semaphore_performance_info_get
- tx_semaphore_prioritize
- tx_semaphore_put
- tx_semaphore_put_notify

## <a name="tx_semaphore_info_get"></a>tx_semaphore_info_get

Semafor hakkında bilgi alın

### <a name="prototype"></a>Prototype

```c
UINT tx_semaphore_info_get(
    TX_SEMAPHORE *semaphore_ptr,
    CHAR **name, ULONG *current_value,
    TX_THREAD **first_suspended,
    ULONG *suspended_count,
    TX_SEMAPHORE **next_semaphore);
```

### <a name="description"></a>Açıklama

Bu hizmet belirtilen semafor hakkında bilgi alır.

### <a name="parameters"></a>Parametreler

- **semaphore_ptr** Semafor denetim bloğu işaretçisi.
- **ad** Semafor adı işaretçisinin hedefi işaretçisi.
- **Current_value** Geçerli semafor sayısı için hedef işaretçisi.
- **first_suspended** Bu semaforun askıya alma listesindeki iş parçacığına işaretçi için hedef işaretçisi.
- **suspended_count** Bu semaforda Şu anda askıya alınan iş parçacığı sayısı için hedef işaretçisi.
- **next_semaphore** Sonraki oluşturulan semaforun işaretçisi için hedef işaretçisi.

> [!NOTE]
> *Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.*

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) bilgileri alma.

- **TX_SEMAPHORE_ERROR** (0x0C) geçersiz semafor işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```c
TX_SEMAPHORE my_semaphore;
CHAR *name;
ULONG current_value;
TX_THREAD *first_suspended;
ULONG suspended_count;
TX_SEMAPHORE *next_semaphore;
UINT status;

/* Retrieve information about the previously created
semaphore "my_semaphore." */
status = tx_semaphore_info_get(&my_semaphore, &name,
    &current_value,
    &first_suspended, &suspended_count,
    &next_semaphore);

/* If status equals TX_SUCCESS, the information requested is
valid. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_semaphore_ceiling_put
- tx_semaphore_create
- tx_semaphore_delete
- tx_semaphore_get
- tx_semaphore_performance_info_get
- tx_semaphore_performance_system_info_get
- tx_semaphore_prioritize
- tx_semaphore_put
- tx_semaphore_put_notify

## <a name="tx_semaphore_performance_info_get"></a>tx_semaphore_performance_info_get

Semafor performans bilgilerini al

### <a name="prototype"></a>Prototype

```c
UINT tx_semaphore_performance_info_get(
    TX_SEMAPHORE *semaphore_ptr,
    ULONG *puts, 
    ULONG *gets,
    ULONG *suspensions, 
    ULONG *timeouts);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen semafor hakkında performans bilgilerini alır.

> [!IMPORTANT]
> *Işparçacığıx kitaplığı ve uygulaması ile*  * oluşturulmalıdır Bu hizmetin performans bilgilerini döndürmesi için **TX_SEMAPHORE_ENABLE_PERFORMANCE_INFO** _ _defined. *

**Parametreler**

-  **semaphore_ptr** Daha önce oluşturulan semafor işaretçisi.
-  **koyar** Bu semafor üzerinde gerçekleştirilen PUT isteği sayısı için hedef işaretçisi.
-  **alır** Bu semafor üzerinde gerçekleştirilen GET isteklerinin sayısı için hedef işaretçisi.
-  **getirilmesi** Bu semaforda iş parçacığı getirilmesi sayısı için hedef işaretçisi.
-  **zaman aşımları** Bu semaforda iş parçacığı askıya alma zaman aşımı sayısı için hedef işaretçisi.

> [!NOTE]
> *Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.*

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı semafor performansı al.
- **TX_PTR_ERROR** (0x03) geçersiz semafor işaretçisi.
- **TX_FEATURE_NOT_ENABLED** (0xFF) sistem, etkin performans bilgileri ile derlenmedi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="example"></a>Örnek

```c
TX_SEMAPHORE my_semaphore;
ULONG puts;
ULONG gets;
ULONG suspensions;
ULONG timeouts;

/* Retrieve performance information on the previously created
semaphore. */
status = tx_semaphore_performance_info_get(&my_semaphore, &puts,
    &gets, &suspensions, &timeouts);

/* If status is TX_SUCCESS the performance information was
successfully retrieved. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_semaphore_ceiling_put
- tx_semaphore_create
- tx_semaphore_delete
- tx_semaphore_get
- tx_semaphore_info_get
- tx_semaphore_performance_system_info_get
- tx_semaphore_prioritize
- tx_semaphore_put
- tx_semaphore_put_notify

## <a name="tx_semaphore_performance_system_info_get"></a>tx_semaphore_performance_system_info_get

Semafor sistem performans bilgilerini al

### <a name="prototype"></a>Prototype

```c
UINT tx_semaphore_performance_system_info_get(
    ULONG *puts,
    ULONG *gets, 
    ULONG *suspensions, 
    ULONG *timeouts);
```

### <a name="description"></a>Açıklama

Bu hizmet sistemdeki tüm Semaforlar hakkındaki performans bilgilerini alır.

> [!IMPORTANT]
> *Işparçacığıx kitaplığı ve uygulaması ile*  * oluşturulmalıdır Bu hizmetin performans bilgilerini döndürmesi için **TX_SEMAPHORE_ENABLE_PERFORMANCE_INFO** _ _defined *

### <a name="parameters"></a>Parametreler

- **koyar** Tüm Semaforlarda gerçekleştirilen put isteklerinin toplam sayısı için hedef işaretçisi.
- **alır** Tüm Semaforlarda gerçekleştirilen GET isteklerinin toplam sayısı için hedef işaretçisi.
- **getirilmesi** Tüm Semaforlarda toplam iş parçacığı getirilmesi sayısı için hedef işaretçisi.
- **zaman aşımları** Tüm Semaforlarda toplam iş parçacığı askıya alma zaman aşımı sayısı için hedef işaretçisi.

> [!NOTE]
> *Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.*

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) sistem performansı al.
- **TX_FEATURE_NOT_ENABLED** (0xFF) sistem, etkin performans bilgileri ile derlenmedi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="example"></a>Örnek

```c
ULONG puts;
ULONG gets;
ULONG suspensions;
ULONG timeouts;

/* Retrieve performance information on all previously created
semaphores. */
status = tx_semaphore_performance_system_info_get(&puts, &gets,
    &suspensions, &timeouts);

/* If status is TX_SUCCESS the performance information was
successfully retrieved. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_semaphore_ceiling_put
- tx_semaphore_create
- tx_semaphore_delete
- tx_semaphore_get
- tx_semaphore_info_get
- tx_semaphore_performance_info_get
- tx_semaphore_prioritize
- tx_semaphore_put
- tx_semaphore_put_notify

## <a name="tx_semaphore_prioritize"></a>tx_semaphore_prioritize

Semafor askıya alma listesini önceliklendir

### <a name="prototype"></a>Prototype

```c
UINT tx_semaphore_prioritize(TX_SEMAPHORE *semaphore_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, askıya alma listesinin önündeki semafor örneği için askıya alınan en yüksek öncelik iş parçacığını koyar. Diğer tüm iş parçacıkları ' de askıya alındığı FıFO sırasında kalır.

### <a name="parameters"></a>Parametreler

- **semaphore_ptr** Daha önce oluşturulmuş bir semafor işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı semafor önceliği belirleme.
- **TX_SEMAPHORE_ERROR** (0x0C) geçersiz sayma semaforu işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```c
TX_SEMAPHORE my_semaphore;
UINT status;

/* Ensure that the highest priority thread will receive
the next instance of this semaphore. */
status = tx_semaphore_prioritize(&my_semaphore);

/* If status equals TX_SUCCESS, the highest priority
suspended thread is at the front of the list. The
next tx_semaphore_put call made to this semaphore will
wake up this thread. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_semaphore_create
- tx_semaphore_delete
- tx_semaphore_get
- tx_semaphore_info_get
- tx_semaphore_put

## <a name="tx_semaphore_put"></a>tx_semaphore_put

Sayım semafora bir örnek yerleştirme

### <a name="prototype"></a>Prototype

```c
UINT tx_semaphore_put(TX_SEMAPHORE *semaphore_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, gerçekte belirtilen sayım semafora bir örnek koyar ve bu da gerçekteki sayım semaforu bir tane artırır.

> [!NOTE]
> *Semaforun hepsi (OxFFFFFFFF) olduğunda bu hizmet çağrılırsa, yeni PUT işlemi semaforun sıfıra sıfırlanmasına neden olur.*

### <a name="parameters"></a>Parametreler

- **semaphore_ptr** Önceden oluşturulan sayım semaforu denetim bloğuna yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı semafor put.
- **TX_SEMAPHORE_ERROR** (0x0C) semaforu saymak için geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="preemption-possible"></a>Önalım mümkün

Yes

### <a name="example"></a>Örnek

```c
TX_SEMAPHORE my_semaphore;
UINT status;

/* Increment the counting semaphore "my_semaphore." */
status = tx_semaphore_put(&my_semaphore);

/* If status equals TX_SUCCESS, the semaphore count has
been incremented. Of course, if a thread was waiting,
it was given the semaphore instance and resumed. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_semaphore_ceiling_put
- tx_semaphore_create
- tx_semaphore_delete
- tx_semaphore_info_get
- tx_semaphore_performance_info_get
- tx_semaphore_performance_system_info_get
- tx_semaphore_prioritize
- tx_semaphore_get
- tx_semaphore_put_notify

## <a name="tx_semaphore_put_notify"></a>tx_semaphore_put_notify

Semafor yerleştirayarlandığında uygulamaya bildir

### <a name="prototype"></a>Prototype

```c
UINT tx_semaphore_put_notify(
    TX_SEMAPHORE *semaphore_ptr,
    VOID (*semaphore_put_notify)(TX_SEMAPHORE *));
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen semafor her gerçekleştiğinde çağrılan bir bildirim geri çağırma işlevini kaydeder. Bildirim geri çağrısının işlenmesi uygulama tarafından tanımlanır.

> [!NOTE]
> *Uygulamanın semafor bildirimi geri çağrısının askıya alma seçeneği ile herhangi bir ThreadX API çağrısı yapılmasına izin verilmez.*

### <a name="parameters"></a>Parametreler

- **semaphore_ptr** Daha önce oluşturulan semafor işaretçisi.
- **semaphore_put_notify** Uygulamanın semafor put bildirimi işlevine yönelik işaretçi. Bu değer TX_NULL, bildirim devre dışı bırakılır.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) semafor put bildiriminin başarıyla kaydı.
- **TX_SEMAPHORE_ERROR** (0x0C) geçersiz semafor işaretçisi.
- **TX_FEATURE_NOT_ENABLED** (0xFF) sistem bildirim özellikleri devre dışı olarak derlendi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="example"></a>Örnek

```c
TX_SEMAPHORE my_semaphore;

/* Register the "my_semaphore_put_notify" function for monitoring
the put operations on the semaphore "my_semaphore." */
status = tx_semaphore_put_notify(&my_semaphore, my_semaphore_put_notify);

/* If status is TX_SUCCESS the semaphore put notification function
was successfully registered. */
void my_semaphore_put_notify(TX_SEMAPHORE *semaphore_ptr)
{
    /* The semaphore was just put! */
}
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_semaphore_ceiling_put
- tx_semaphore_create
- tx_semaphore_delete
- tx_semaphore_get
- tx_semaphore_info_get
- tx_semaphore_performance_info_get
- tx_semaphore_performance_system_info_get
- tx_semaphore_prioritize
- tx_semaphore_put

## <a name="tx_thread_create"></a>tx_thread_create

Uygulama iş parçacığı oluştur

### <a name="prototype"></a>Prototype

```c
UINT tx_thread_create(
    TX_THREAD *thread_ptr,
    CHAR *name_ptr, 
    VOID (*entry_function)(ULONG),
    ULONG entry_input, 
    VOID *stack_start,
    ULONG stack_size, 
    UINT priority,
    UINT preempt_threshold, 
    ULONG time_slice,
    UINT auto_start);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen görev girişi işlevinde yürütmeyi Başlatan bir uygulama iş parçacığı oluşturur. Yığın, öncelik, önalım-Threshold ve zaman dilimi, giriş parametreleri tarafından belirtilen özniteliklerin arasındadır. Ayrıca, iş parçacığının ilk yürütme durumu da belirtilir.

**Parametreler**

- **thread_ptr** İş parçacığı denetim bloğu işaretçisi.
- **name_ptr** İş parçacığının adı işaretçisi.
- **entry_function** İş parçacığı yürütmesi için ilk C işlevini belirtir. Bir iş parçacığı bu giriş işlevinden döndüğünde, *tamamlanmış* bir duruma konur ve süresiz olarak askıya alınır.
- **entry_input** İlk yürütüldüğünde iş parçacığının giriş işlevine geçirilen 32 bitlik bir değer. Bu giriş için kullanım, uygulama tarafından özel olarak belirlenir.
- **stack_start** Yığının bellek alanının başlangıç adresi.
- **stack_size** Yığın bellek alanındaki bayt sayısı. İş parçacığının yığın alanı, en kötü durum işlevi çağrı iç içe ve yerel değişken kullanımını işleyecek kadar büyük olmalıdır.
- **Öncelik** İş parçacığının sayısal önceliği. Geçerli değerler 0 ile (TX_MAX_PRIORITES-1) arasındadır; burada 0 değeri, en yüksek önceliği temsil eder.
- **preempt_threshold** Devre dışı önalım en yüksek öncelik düzeyi (0 ila (TX_MAX_PRIORITIES-1)). Bu iş parçacığını yalnızca bu düzeyden daha yüksek öncelikler için izin verilir. Bu değer, belirtilen önceliğe eşit veya ondan küçük olmalıdır. İş parçacığı önceliğine eşit bir değer önalım eşiğini devre dışı bırakır.
- **time_slice** Aynı önceliğe sahip diğer hazırlık iş parçacıklarıyla çalışma şansı verilmeye başlamadan önce bu iş parçacığının çalışmasına izin verilen zamanlayıcı sayısı-işaretleri. Önalım-Threshold kullanmanın zaman dilimini devre dışı bıraktığını unutmayın. Yasal zaman dilimi değerleri 1 ile 0xFFFFFFFF (dahil) arasındadır. **TX_NO_TIME_SLICE** değeri (0 değeri), bu iş parçacığının zaman dilimzamanını devre dışı bırakır.

  > [!NOTE]
  > *Zaman dilimletmek, daha hafif bir sistem yükü miktarına neden olur.   Zaman dilimi yalnızca birden çok iş parçacığının aynı önceliğe sahip olduğu durumlarda faydalıdır, benzersiz önceliğe sahip iş parçacıkları zaman dilimi atanmamalıdır.*

- **auto_start** İş parçacığının hemen başlatılıp başlatılmayacağını veya askıya alınma durumuna yerleştirilip yerleştirilmeyeceğini belirtir. Yasal seçenekler **TX_AUTO_START** (0x01) ve **TX_DONT_START** (0x00). TX_DONT_START belirtilirse, uygulamanın iş parçacığının çalışması için daha sonra tx_thread_resume çağırması gerekir.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı iş parçacığı oluşturma.
- **TX_THREAD_ERROR** (0x0E) geçersiz iş parçacığı denetim işaretçisi. İşaretçi NULL ya da iş parçacığı zaten oluşturulmuş.
- **TX_PTR_ERROR** (0x03) giriş noktasının başlangıç adresi geçersiz veya yığın alanı geçersiz, genellikle null.
- **TX_SIZE_ERROR** (0x05) yığın alanının boyutu geçersiz. İş parçacıklarının yürütülmesi için en az **TX_MINIMUM_STACK** bayt olması gerekir.
- **TX_PRIORITY_ERROR** (0X0f) geçersiz iş parçacığı önceliği (0-(TX_MAX_PRIORITIES-1) aralığı dışında bir değer.
- **TX_THRESH_ERROR** (0x18) geçersiz preemptionthreshold belirtildi. Bu değer, iş parçacığının ilk önceliğine eşit veya ondan küçük geçerli bir öncelik olmalıdır.
- **TX_START_ERROR** (0x10) geçersiz otomatik başlatma seçimi.
- **TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

Başlatma ve iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Yes

### <a name="example"></a>Örnek

```c
TX_THREAD my_thread;
UINT status;

/* Create a thread of priority 15 whose entry point is
"my_thread_entry". This thread’s stack area is 1000
bytes in size, starting at address 0x400000. The
preemption-threshold is setup to allow preemption of threads
with priorities ranging from 0 through 14. Time-slicing is
disabled. This thread is automatically put into a ready
condition. */
status = tx_thread_create(&my_thread, "my_thread_name",
    my_thread_entry, 0x1234,
    (VOID *) 0x400000, 1000,
    15, 15, TX_NO_TIME_SLICE,
    TX_AUTO_START);

/* If status equals TX_SUCCESS, my_thread is ready
for execution! */

...

/* Thread’s entry function. When "my_thread" actually
begins execution, control is transferred to this
function. */

VOID my_thread_entry (ULONG initial_input)
{
    /* When we get here, the value of initial_input is
    0x1234. See how this was specified during
    creation. */
    /* The real work of the thread, including calls to
    other function should be called from here! */
    /* When this function returns, the corresponding
    thread is placed into a "completed" state. */
}
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_thread_delete
- tx_thread_entry_exit_notify
- tx_thread_identify
- tx_thread_info_get
- tx_thread_performance_info_get
- tx_thread_performance_system_info_get
- tx_thread_preemption_change
- tx_thread_priority_change
- tx_thread_relinquish
- tx_thread_reset
- tx_thread_resume
- tx_thread_sleep
- tx_thread_stack_error_notify
- tx_thread_suspend
- tx_thread_terminate
- tx_thread_time_slice_change
- tx_thread_wait_abort

## <a name="tx_thread_delete"></a>tx_thread_delete

Uygulama iş parçacığını Sil

### <a name="prototype"></a>Prototype

```c
UINT tx_thread_delete(TX_THREAD *thread_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen uygulama iş parçacığını siler. Belirtilen iş parçacığının sonlandırılmış veya tamamlanmış durumda olması gerektiğinden, bu hizmet kendisini silmeye çalışan bir iş parçacığından çağrılamaz.

> [!NOTE]
> *Bu hizmet tamamlandıktan sonra kullanılabilir olan iş parçacığının yığınında ilişkili bellek alanını yönetmek uygulamanın sorumluluğundadır. Ayrıca, uygulamanın silinen bir iş parçacığının kullanımını önlemesi gerekir.*

### <a name="parameters"></a>Parametreler

- **thread_ptr** Daha önce oluşturulmuş bir uygulama iş parçacığına işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı iş parçacığı silme.
- **TX_THREAD_ERROR** (0x0E) geçersiz uygulama iş parçacığı işaretçisi.
- **TX_DELETE_ERROR** (0x11) belirtilen iş parçacığı sonlandırılmış veya tamamlanmış durumda değil.
- **TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları ve zamanlayıcılar

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```c
TX_THREAD my_thread;
UINT status;

/* Delete an application thread whose control block is
"my_thread". Assume that the thread has already been
created with a call to tx_thread_create. */
status = tx_thread_delete(&my_thread);

/* If status equals TX_SUCCESS, the application thread is
deleted. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_thread_create
- tx_thread_entry_exit_notify
- tx_thread_identify
- tx_thread_info_get
- tx_thread_performance_info_get
- tx_thread_performance_system_info_get
- tx_thread_preemption_change
- tx_thread_priority_change
- tx_thread_relinquish
- tx_thread_reset
- tx_thread_resume
- tx_thread_sleep
- tx_thread_stack_error_notify
- tx_thread_suspend
- tx_thread_terminate
- tx_thread_time_slice_change
- tx_thread_wait_abort

## <a name="tx_thread_entry_exit_notify"></a>tx_thread_entry_exit_notify

İş parçacığı girdisi ve çıkış sonrasında uygulamayı bilgilendir

### <a name="prototype"></a>Prototype

```c
UINT tx_thread_entry_exit_notify(
    TX_THREAD *thread_ptr,
    VOID (*entry_exit_notify)(TX_THREAD *, UINT));
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen iş parçacığı girildiğinde veya çıktığında çağrılan bir bildirim geri arama işlevini kaydeder. Bildirim geri çağrısının işlenmesi uygulama tarafından tanımlanır.

> [!NOTE]
> Uygulamanın iş parçacığı giriş/çıkış bildirimi geri çağrısının askıya alma seçeneği ile herhangi bir ThreadX API çağrısı yapılmasına izin verilmez.

### <a name="parameters"></a>Parametreler

- **thread_ptr** Daha önce oluşturulmuş iş parçacığına yönelik işaretçi.
- **entry_exit_notify** Uygulamanın iş parçacığı giriş/çıkış bildirimi işlevine yönelik işaretçi. Giriş/çıkış bildirimi işlevinin ikinci parametresi, bir giriş veya çıkış varsa belirler. **TX_THREAD_ENTRY** (0x00) değeri, iş parçacığının girildiğini belirtir, ancak değer **TX_THREAD_EXIT** (0x01), iş parçacığının çıkış olduğunu gösterir. Bu değer **TX_NULL**, bildirim devre dışı bırakılır.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) iş parçacığı giriş/çıkış bildirimi işlevinin başarıyla kaydı.
- **TX_THREAD_ERROR** (0x0E) geçersiz iş parçacığı işaretçisi.
- **TX_FEATURE_NOT_ENABLED** (0xFF) sistem bildirim özellikleri devre dışı olarak derlendi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="example"></a>Örnek

```c
TX_THREAD my_thread;
/* Register the "my_entry_exit_notify" function for monitoring
the entry/exit of the thread "my_thread." */
status = tx_thread_entry_exit_notify(&my_thread,
    my_entry_exit_notify);

/* If status is TX_SUCCESS the entry/exit notification function was
successfully registered. */
void my_entry_exit_notify(TX_THREAD *thread_ptr, UINT condition)
{
    /* Determine if the thread was entered or exited. */
    if (condition == TX_THREAD_ENTRY)
        /* Thread entry! */
    else if (condition == TX_THREAD_EXIT)
        /* Thread exit! */
}
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_thread_create
- tx_thread_delete
- tx_thread_entry_exit_notify
- tx_thread_identify
- tx_thread_info_get
- tx_thread_performance_info_get
- tx_thread_performance_system_info_get
- tx_thread_preemption_change
- tx_thread_priority_change
- tx_thread_relinquish
- tx_thread_reset
- tx_thread_resume
- tx_thread_sleep
- tx_thread_stack_error_notify
- tx_thread_suspend
- tx_thread_terminate
- tx_thread_time_slice_change
- tx_thread_wait_abort

## <a name="tx_thread_identify"></a>tx_thread_identify

Şu anda yürütülmekte olan iş parçacığına olan işaretçiyi alır

### <a name="prototype"></a>Prototype

```c
TX_THREAD* tx_thread_identify(VOID);
```
### <a name="description"></a>Açıklama

Bu hizmet şu anda yürütülmekte olan iş parçacığına bir işaretçi döndürür. İş parçacığı yürütülerek, bu hizmet null bir işaretçi döndürür.

> [!NOTE]
> *Bu hizmet bir ıSR 'den çağrılırsa, dönüş değeri yürütülen kesme işleyicisinden önce çalışan iş parçacığını temsil eder.*

### <a name="parameters"></a>Parametreler

Hiçbiri

### <a name="retuen-values"></a>Retuen değerleri

- **iş parçacığı işaretçisi** Şu anda yürütülmekte olan iş parçacığına yönelik işaretçi. İş parçacığı yürütülerek, dönüş değeri **TX_NULL**.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları ve ISRs

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

TX_THREAD * my_thread_ptr;

```c
TX_THREAD *my_thread_ptr;

/* Find out who we are! */
my_thread_ptr = tx_thread_identify();

/* If my_thread_ptr is non-null, we are currently executing
from that thread or an ISR that interrupted that thread.
Otherwise, this service was called
from an ISR when no thread was running when the
interrupt occurred. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_thread_create
- tx_thread_delete
- tx_thread_entry_exit_notify
- tx_thread_info_get
- tx_thread_performance_info_get
- tx_thread_performance_system_info_get
- tx_thread_preemption_change
- tx_thread_priority_change
- tx_thread_relinquish
- tx_thread_reset
- tx_thread_resume
- tx_thread_sleep
- tx_thread_stack_error_notify
- tx_thread_suspend
- tx_thread_terminate
- tx_thread_time_slice_change
- tx_thread_wait_abort

## <a name="tx_thread_info_get"></a>tx_thread_info_get

İş parçacığı hakkında bilgi alma

### <a name="prototype"></a>Prototype

```c
UINT tx_thread_info_get(
    TX_THREAD *thread_ptr, 
    CHAR **name,
    UINT *state, 
    ULONG *run_count,
    UINT *priority,
    UINT *preemption_threshold,
    ULONG *time_slice,
    TX_THREAD **next_thread,
    TX_THREAD **suspended_thread);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen iş parçacığı hakkındaki bilgileri alır.

### <a name="parameters"></a>Parametreler
- **thread_ptr** İş parçacığı denetim bloğu işaretçisi.
- **ad** İş parçacığının adına işaretçi için hedef işaretçisi.
- **durum** İş parçacığının geçerli yürütme durumu için hedef işaretçisi. Olası değerler aşağıdaki gibidir.
    - **TX_READY** (0x00)
    - **TX_COMPLETED** (0x01)
    - **TX_TERMINATED** (0x02)
    - **TX_SUSPENDED** (0x03)
    - **TX_SLEEP** (0x04)
    - **TX_QUEUE_SUSP** (0x05)
    - **TX_SEMAPHORE_SUSP** (0x06)
    - **TX_EVENT_FLAG** (0x07)
    - **TX_BLOCK_MEMORY** (0x08)
    - **TX_BYTE_MEMORY** (0x09)
    - **TX_MUTEX_SUSP** (0x0D)  

- **run_count** İş parçacığının çalışma sayısı için hedef işaretçisi.
- **Öncelik** İş parçacığının önceliği için hedef işaretçisi.
- **preemption_threshold** İş parçacığının önalım-Threshold hedefi işaretçisi.
**time_slice** İş parçacığının zaman dilimi için hedef işaretçisi.
**next_thread** Sonraki oluşturulan iş parçacığı işaretçisinin hedefi işaretçisi.

**suspended_thread** Askıya alma listesindeki bir sonraki iş parçacığına işaretçi için hedef işaretçisi.

> [!NOTE]
> *Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.*

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı iş parçacığı bilgileri alma.
- **TX_THREAD_ERROR** (0x0E) geçersiz iş parçacığı denetim işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```c
TX_THREAD my_thread;
CHAR *name;
UINT state;
ULONG run_count;
UINT priority;
UINT preemption_threshold;
UINT time_slice;
TX_THREAD *next_thread;
TX_THREAD *suspended_thread;
UINT status;

/* Retrieve information about the previously created
thread "my_thread." */

status = tx_thread_info_get(&my_thread, &name,
    &state, &run_count,
    &priority, &preemption_threshold,
    &time_slice, &next_thread,&suspended_thread);

/* If status equals TX_SUCCESS, the information requested is
valid. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_thread_create
- tx_thread_delete
- tx_thread_entry_exit_notify
- tx_thread_identify
- tx_thread_performance_info_get
- tx_thread_performance_system_info_get
- tx_thread_preemption_change
- tx_thread_priority_change
- tx_thread_relinquish
- tx_thread_reset
- tx_thread_resume
- tx_thread_sleep
- tx_thread_stack_error_notify
- tx_thread_suspend
- tx_thread_terminate
- tx_thread_time_slice_change
- tx_thread_wait_abort

## <a name="tx_thread_performance_info_get"></a>tx_thread_performance_info_get

İş parçacığı performans bilgilerini al

### <a name="prototype"></a>Prototype

```c
UINT tx_thread_performance_info_get(
    TX_THREAD *thread_ptr,
    LONG *resumptions, 
    ULONG *suspensions,
    ULONG *solicited_preemptions, 
    ULONG *interrupt_preemptions,
    ULONG *priority_inversions, 
    ULONG *time_slices,
    ULONG *relinquishes, 
    ULONG *timeouts, 
    ULONG *wait_aborts,
    TX_THREAD **last_preempted_by);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen iş parçacığıyla ilgili performans bilgilerini alır.

> [!IMPORTANT]
> *Işparçacığıx kitaplığı ve uygulaması ile*  * oluşturulmalıdır Bu hizmetin performans bilgilerini döndürmesi için _ _defined **TX_THREAD_ENABLE_PERFORMANCE_INFO**. *

### <a name="parameters"></a>Parametreler
- **thread_ptr** Daha önce oluşturulmuş iş parçacığına yönelik işaretçi.
- **bağlantının sürdürülmesi** Bu iş parçacığının bağlantının sürdürülmesi sayısı için hedef işaretçisi.
- **getirilmesi** Bu iş parçacığının getirilmesi sayısı için hedef işaretçisi.
- **solicited_preemptions** Bu iş parçacığı tarafından yapılan bir ThreadX API hizmeti çağrısının sonucu olarak, preemptions sayısı için hedef işaretçisi.
- **interrupt_preemptions** Bu iş parçacığının preemptions sayısı için hedef işaretçisi, kesme işlemenin sonucu olarak.
- **priority_inversions** Bu iş parçacığının öncelik Inin sayısı için hedef işaretçisi.
- **time_slices** Bu iş parçacığının zaman dilimlerinin sayısı için hedef işaretçisi.
- **relinquishes** Bu iş parçacığı tarafından gerçekleştirilen iş parçacığı relini sayısı için hedef işaretçisi.
- **zaman aşımları** Bu iş parçacığında askıya alınma zaman aşımları sayısı için hedef işaretçisi.
- **wait_aborts** Bu iş parçacığında gerçekleştirilen bekleme iptal sayısı için hedef işaretçisi.
- **last_preempted_by** Bu iş parçacığını en son alan iş parçacığı işaretçisinin hedefi işaretçisi.

> [!NOTE]
> *Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.*

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı iş parçacığı performansı al.
- **TX_PTR_ERROR** (0x03) geçersiz iş parçacığı işaretçisi.
- **TX_FEATURE_NOT_ENABLED** (0xFF) sistem, etkin performans bilgileri ile derlenmedi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="example"></a>Örnek

```c
TX_THREAD my_thread;
ULONG resumptions;
ULONG suspensions;
ULONG solicited_preemptions;
ULONG interrupt_preemptions;
ULONG priority_inversions;
ULONG time_slices;
ULONG relinquishes;
ULONG timeouts;
ULONG wait_aborts;
TX_THREAD *last_preempted_by;

/* Retrieve performance information on the previously created
thread. */

status = tx_thread_performance_info_get(&my_thread, &resumptions,
    &suspensions,
    &solicited_preemptions, &interrupt_preemptions,
    &priority_inversions, &time_slices,
    &relinquishes, &timeouts,
    &wait_aborts, &last_preempted_by);

/* If status is TX_SUCCESS the performance information was
successfully retrieved. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_thread_create
- tx_thread_delete
- tx_thread_entry_exit_notify
- tx_thread_identify
- tx_thread_info_get
- tx_thread_performance_system_info_get
- tx_thread_preemption_change
- tx_thread_priority_change
- tx_thread_relinquish
- tx_thread_reset
- tx_thread_resume
- tx_thread_sleep
- tx_thread_stack_error_notify
- tx_thread_suspend
- tx_thread_terminate
- tx_thread_time_slice_change
- tx_thread_wait_abort

## <a name="tx_thread_performance_system_info_get"></a>tx_thread_performance_system_info_get

İş parçacığı sistemi performans bilgilerini al

### <a name="prototype"></a>Prototype

```c
UINT tx_thread_performance_system_info_get(
    ULONG *resumptions,
    ULONG *suspensions, 
    ULONG *solicited_preemptions,
    ULONG *interrupt_preemptions, 
    ULONG *priority_inversions,
    ULONG *time_slices, 
    ULONG *relinquishes, 
    ULONG *timeouts,
    ULONG *wait_aborts, 
    ULONG *non_idle_returns,
    ULONG *idle_returns);
```

### <a name="description"></a>Açıklama

Bu hizmet, sistemdeki tüm iş parçacıkları hakkındaki performans bilgilerini alır.

*Işparçacığıx kitaplığı ve uygulaması ile oluşturulmalıdır*

*Bu hizmetin performans bilgilerini döndürmesi için _ _defined **TX_THREAD_ENABLE_PERFORMANCE_INFO**. *

### <a name="parameters"></a>Parametreler

- **bağlantının sürdürülmesi** Toplam iş parçacığı sayısı için hedef işaretçisi bağlantının sürdürülmesi.
- **getirilmesi** Toplam iş parçacığı sayısı için hedef işaretçisi getirilmesi.
- **solicited_preemptions** Bir ThreadX API hizmetini çağıran iş parçacığının bir sonucu olarak preemptions iş parçacığı toplam sayısı için hedef işaretçisi.
- **interrupt_preemptions** Kesme işlemenin sonucu olarak preemptions iş parçacığı toplam sayısı için hedef işaretçisi.
- **priority_inversions** Toplam iş parçacığı önceliği ınsürümlerin sayısı için hedef işaretçisi.
- **time_slices** İş parçacığı zaman dilimlerinin toplam sayısı için hedef işaretçisi.
- **relinquishes** Toplam iş parçacığı yeniden sayısı için hedef işaretçisi.
- **zaman aşımları** Toplam iş parçacığı askıya alma zaman aşımı sayısı için hedef işaretçisi.
- **wait_aborts** Toplam iş parçacığı bekleme sayısı için hedef işaretçisi.
- **non_idle_returns** Başka bir iş parçacığı yürütülmeye hazırlandığınızda, bir iş parçacığının sisteme kaç kez geri döndüğünü gösteren hedef işaretçisi.
- **idle_returns** Başka bir iş parçacığı yürütülmeye hazırlanana olmadığında, bir iş parçacığının sisteme döndürdüğü süre için hedef işaretçisi (boş sistem).

> [!NOTE]
> *Herhangi bir parametre için **TX_NULL** sağlama, parametrenin gerekli olmadığını gösterir.*

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı iş parçacığı sistem performansı al.
- **TX_FEATURE_NOT_ENABLED** (0xFF) sistem, etkin performans bilgileri ile derlenmedi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="example"></a>Örnek

```c
ULONG resumptions;
ULONG suspensions;
ULONG solicited_preemptions;
ULONG interrupt_preemptions;
ULONG priority_inversions;
ULONG time_slices;
ULONG relinquishes;
ULONG timeouts;
ULONG wait_aborts;
ULONG non_idle_returns;
ULONG idle_returns;

/* Retrieve performance information on all previously created
thread. */

status = tx_thread_performance_system_info_get(&resumptions,
    &suspensions,
    &solicited_preemptions, &interrupt_preemptions,
    &priority_inversions, &time_slices, &relinquishes,
    &timeouts, &wait_aborts, &non_idle_returns,
    &idle_returns);

/* If status is TX_SUCCESS the performance information was
successfully retrieved. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_thread_create
- tx_thread_delete
- tx_thread_entry_exit_notify
- tx_thread_identify
- tx_thread_info_get
- tx_thread_performance_info_get
- tx_thread_preemption_change
- tx_thread_priority_change
- tx_thread_relinquish
- tx_thread_reset
- tx_thread_resume
- tx_thread_sleep
- tx_thread_stack_error_notify
- tx_thread_suspend
- tx_thread_terminate
- tx_thread_time_slice_change
- tx_thread_wait_abort

## <a name="tx_thread_preemption_change"></a>tx_thread_preemption_change

Önalım-uygulama iş parçacığının eşiğini değiştirme

### <a name="prototype"></a>Prototype

```c
UINT tx_thread_preemption_change(
    TX_THREAD *thread_ptr,
    UINT new_threshold, 
    UINT *old_threshold);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen iş parçacığının önalım eşiğini değiştirir. Önalım-Threshold, önalım-Threshold değerine eşit veya daha küçük olan iş parçacıkları tarafından belirtilen iş parçacığının önalım ' i engelliyor.

>[!NOTE]
> *Önalım-Threshold kullanılması, belirtilen iş parçacığı için zaman dilimini devre dışı bırakır.*

### <a name="parameters"></a>Parametreler
- **thread_ptr** Daha önce oluşturulmuş bir uygulama iş parçacığına işaretçi.
- **new_threshold** Yeni önalım-Threshold öncelik düzeyi (0 ila (TX_MAX_PRIORITIES-1)).
- **old_threshold** Önceki önalım-Threshold döndürecek bir konum işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı önalım-eşik değişikliği.
- **TX_THREAD_ERROR** (0x0E) geçersiz uygulama iş parçacığı işaretçisi.
- **TX_THRESH_ERROR** (0x18) belirtilen yeni önalım-Threshold geçerli iş parçacığı önceliğine göre geçerli bir iş parçacığı önceliği ((0 ila (**TX_MAX_PRIORITIES**-1) veya daha büyük (düşük öncelik) değil.
- **TX_PTR_ERROR** (0x03) önceki preemptionthreshold depolama konumuna yönelik geçersiz işaretçi.
- **TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları ve zamanlayıcılar

### <a name="preemption-possible"></a>Önalım mümkün

Yes

### <a name="example"></a>Örnek

```c
TX_THREAD my_thread;
UINT my_old_threshold;
UINT status;

/* Disable all preemption of the specified thread. The
current preemption-threshold is returned in
"my_old_threshold". Assume that "my_thread" has
already been created. */

status = tx_thread_preemption_change(&my_thread,
    0, &my_old_threshold);

/* If status equals TX_SUCCESS, the application thread is
non-preemptable by another thread. Note that ISRs are
not prevented by preemption disabling. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_thread_create
- tx_thread_delete
- tx_thread_entry_exit_notify
- tx_thread_identify
- tx_thread_info_get
- tx_thread_performance_info_get
- tx_thread_performance_system_info_get
- tx_thread_priority_change
- tx_thread_relinquish
- tx_thread_reset
- tx_thread_resume
- tx_thread_sleep
- tx_thread_stack_error_notify
- tx_thread_suspend
- tx_thread_terminate
- tx_thread_time_slice_change
- tx_thread_wait_abort

## <a name="tx_thread_priority_change"></a>tx_thread_priority_change

Uygulama iş parçacığının önceliğini değiştirme

### <a name="prototype"></a>Prototype

```c
UINT tx_thread_priority_change(
    TX_THREAD *thread_ptr,
    UINT new_priority, 
    UINT *old_priority);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen iş parçacığının önceliğini değiştirir. Geçerli öncelikler 0 ile (TX_MAX_PRIORITES-1) arasındadır; burada 0 en yüksek öncelik düzeyini temsil eder.

> [!IMPORTANT]
> * Belirtilen iş parçacığının önalım-Threshold değeri otomatik olarak yeni önceliğe ayarlanır. Yeni bir eşik isteniyorsa, bu call._ sonra ***tx_thread_preemption_change** _ hizmetinin kullanılması gerekir

### <a name="parameters"></a>Parametreler

- **thread_ptr** Daha önce oluşturulmuş bir uygulama iş parçacığına işaretçi.
- **new_priority** Yeni iş parçacığı öncelik düzeyi (0 ila (TX_MAX_PRIORITIES-1)).
- **old_priority** İş parçacığının önceki önceliğini döndürmek için bir konum işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı öncelik değişikliği.
- **TX_THREAD_ERROR** (0x0E) geçersiz uygulama iş parçacığı işaretçisi.
- **TX_PRIORITY_ERROR** (0x0F) belirtilen yeni öncelik geçerli değil ((0-(TX_MAX_PRIORITIES-1) dışında bir değer).
- **TX_PTR_ERROR** (0x03) önceki öncelikli depolama konumuna yönelik geçersiz işaretçi.
- **TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları ve zamanlayıcılar

### <a name="preemption-possible"></a>Önalım mümkün

Yes

### <a name="example"></a>Örnek

```c
TX_THREAD my_thread;
UINT my_old_priority;
UINT status;

/* Change the thread represented by "my_thread" to priority
0. */

status = tx_thread_priority_change(&my_thread,
    0, &my_old_priority);

/* If status equals TX_SUCCESS, the application thread is
now at the highest priority level in the system. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- tx_thread_create
- tx_thread_delete
- tx_thread_entry_exit_notify
- tx_thread_identify
- tx_thread_info_get
- tx_thread_performance_info_get
- tx_thread_performance_system_info_get
- tx_thread_preemption_change
- tx_thread_relinquish
- tx_thread_reset
- tx_thread_resume
- tx_thread_sleep
- tx_thread_stack_error_notify
- tx_thread_suspend
- tx_thread_terminate
- tx_thread_time_slice_change
- tx_thread_wait_abort

## <a name="tx_thread_relinquish"></a>tx_thread_relinquish

Diğer uygulama iş parçacıklarıyla denetimi yeniden oluşturma

### <a name="prototype"></a>Prototype

```c
VOID tx_thread_relinquish(VOID);
```

### <a name="description"></a>Açıklama

Bu hizmet, aynı veya daha yüksek önceliğe sahip başka bir hazırlık iş parçacığına işlemci denetimini yeniden oluşturur.

> [!NOTE]
> *Aynı önceliğe sahip iş parçacıklarıyla, bu hizmetin aynı önceliğe sahip iş parçacıklarından de daha fazla denetim, geçerli iş parçacığının önalım-Threshold ayarı nedeniyle yürütmenin en yüksek öncelikli iş parçacığına karşı çalışmasını engelledi.*

### <a name="parameters"></a>Parametreler

Hiçbiri

### <a name="return-values"></a>Dönüş Değerleri

Yok

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Yes

### <a name="examples"></a>Örnekler

```c
ULONG run_counter_1 = 0;
ULONG run_counter_2 = 0;

/* Example of two threads relinquishing control to
each other in an infinite loop. Assume that
both of these threads are ready and have the same
priority. The run counters will always stay within one
of each other. */

VOID my_first_thread(ULONG thread_input)
{
    /* Endless loop of relinquish. */
    while(1)
    {
        /* Increment the run counter. */
        run_counter_1++;

        /* Relinquish control to other thread. */
        tx_thread_relinquish();
    }
}

VOID my_second_thread(ULONG thread_input)
{

    /* Endless loop of relinquish. */
    while(1)
    {
        /* Increment the run counter. */
        run_counter_2++;

        /* Relinquish control to other thread. */
        tx_thread_relinquish();
    }
}
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_thread_create
- tx_thread_delete
- tx_thread_entry_exit_notify
- tx_thread_identify
- tx_thread_info_get
- tx_thread_performance_info_get
- tx_thread_performance_system_info_get
- tx_thread_preemption_change
- tx_thread_priority_change
- tx_thread_reset
- tx_thread_resume
- tx_thread_sleep
- tx_thread_stack_error_notify
- tx_thread_suspend
- tx_thread_terminate
- tx_thread_time_slice_change
- tx_thread_wait_abort

## <a name="tx_thread_reset"></a>tx_thread_reset

İş parçacığını Sıfırla

### <a name="prototype"></a>Prototype

```c
UINT tx_thread_reset(TX_THREAD *thread_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen iş parçacığını iş parçacığı oluşturma sırasında tanımlanan giriş noktasında yürütülecek şekilde sıfırlar. İş parçacığı sıfırlanmak için bir **TX_COMPLETED** veya **TX_TERMINATED** durumunda olmalıdır

> [!IMPORTANT]
> *Yeniden yürütülmesi için iş parçacığının sürdürülmeye devam etmelidir.*

### <a name="parameters"></a>Parametreler

- **thread_ptr** Daha önce oluşturulmuş bir iş parçacığına işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı iş parçacığı sıfırlaması.
- **TX_NOT_DONE** (0x20) belirtilen iş parçacığı **TX_COMPLETED** veya **TX_TERMINATED** durumunda değil.
- **TX_THREAD_ERROR** (0x0E) geçersiz iş parçacığı işaretçisi.
- **TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

TX_THREAD my_thread;

```c
TX_THREAD my_thread;

/* Reset the previously created thread "my_thread." */

status = tx_thread_reset(&my_thread);

/* If status is TX_SUCCESS the thread is reset. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_thread_create
- tx_thread_delete
- tx_thread_entry_exit_notify
- tx_thread_identify
- tx_thread_info_get
- tx_thread_performance_info_get
- tx_thread_preformance_system_info_get
- tx_thread_preemption_change
- tx_thread_priority_change
- tx_thread_relinquish
- tx_thread_resume
- tx_thread_sleep
- tx_thread_stack_error_notify
- tx_thread_suspend
- tx_thread_terminate
- tx_thread_time_slice_change
- tx_thread_wait_abort

## <a name="tx_thread_resume"></a>tx_thread_resume

Askıya alınmış uygulama iş parçacığını sürdürür

### <a name="prototype"></a>Prototype

```c
UINT tx_thread_resume(TX_THREAD *thread_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, daha önce bir ***tx_thread_suspend*** çağrısıyla askıya alınmış bir iş parçacığını yürütmeye devam eder veya hazırlar. Ayrıca, bu hizmet otomatik başlatma olmadan oluşturulan iş parçacıklarını sürdürür.

### <a name="parameters"></a>Parametreler

- **thread_ptr** Askıya alınmış bir uygulama iş parçacığına yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı iş parçacığı özgeçmişi.
- **TX_SUSPEND_LIFTED** (0x19) daha önce Gecikmeli askıya alma yükseltilmemiş idi.
- **TX_THREAD_ERROR** (0x0E) geçersiz uygulama iş parçacığı işaretçisi.
- **TX_RESUME_ERROR** (0x12) belirtilen iş parçacığı askıya alınmaz veya daha önce **_tx_thread_suspend_** dışında bir hizmet tarafından askıya alındı.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="preemption-possible"></a>Önalım mümkün

Yes

TX_THREAD my_thread;

### <a name="example"></a>Örnek

```c
TX_THREAD my_thread;
UINT status;

/* Resume the thread represented by "my_thread". */
status = tx_thread_resume(&my_thread);

/* If status equals TX_SUCCESS, the application thread is
now ready to execute. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_thread_create
- tx_thread_delete
- tx_thread_entry_exit_notify
- tx_thread_identify
- tx_thread_info_get
- tx_thread_performance_info_get
- tx_thread_performance_system_info_get
- tx_thread_preemption_change
- tx_thread_priority_change
- tx_thread_relinquish
- tx_thread_reset
- tx_thread_sleep
- tx_thread_stack_error_notify
- tx_thread_suspend
- tx_thread_terminate
- tx_thread_time_slice_change
- tx_thread_wait_abort

## <a name="tx_thread_sleep"></a>tx_thread_sleep

Belirtilen süre boyunca geçerli iş parçacığını askıya al

### <a name="prototype"></a>Prototype

```c
UINT tx_thread_sleep(ULONG timer_ticks);
```

### <a name="description"></a>Açıklama

Bu hizmet, çağıran iş parçacığının belirtilen sayıda süreölçer onay işareti için askıda olmasına neden olur. Süreölçer Tick ile ilişkili fiziksel sürenin miktarı uygulamaya özgüdür. Bu hizmet, yalnızca bir uygulama iş parçacığından çağrılabilir.

### <a name="parameters"></a>Parametreler

- **timer_ticks** Çağıran uygulama iş parçacığını askıya almak için 0 ile 0xFFFFFFFF arasında değişen Zamanlayıcı onay işaretleri sayısı. 0 belirtilirse, hizmet hemen döndürür.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı iş parçacığı uykusu.
- **TX_WAIT_ABORTED** (0x1A) askıya alma başka bir iş parçacığı, ZAMANLAYıCı veya ISR tarafından iptal edildi.
- **TX_CALLER_ERROR** (0x13) hizmet iş parçacığından çağırılır.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Yes

### <a name="example"></a>Örnek

```c
UINT status;

/* Make the calling thread sleep for 100
timer-ticks. */
status = tx_thread_sleep(100);

/* If status equals TX_SUCCESS, the currently running
application thread slept for the specified number of
timer-ticks. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_thread_create, tx_thread_delete
- tx_thread_entry_exit_notify
- tx_thread_identify
- tx_thread_info_get
- tx_thread_performance_info_get
- tx_thread_performance_system_info_get
- tx_thread_preemption_change
- tx_thread_priority_change
- tx_thread_relinquish
- tx_thread_reset
- tx_thread_resume
- tx_thread_stack_error_notify
- tx_thread_suspend
- tx_thread_terminate
- tx_thread_time_slice_change
- tx_thread_wait_abort

## <a name="tx_thread_stack_error_notify"></a>tx_thread_stack_error_notify

İş parçacığı yığınını kaydet hata bildirimi geri araması

### <a name="prototype"></a>Prototype

```c
UINT tx_thread_stack_error_notify(VOID (*error_handler)(TX_THREAD *));
```

### <a name="description"></a>Açıklama

Bu hizmet, iş parçacığı yığın hatalarını işlemek için bir bildirim geri çağırma işlevi kaydeder. ThreadX, yürütme sırasında bir iş parçacığı yığını hatası algıladığında, hatayı işlemek için bu bildirim işlevini çağırır. Hatanın işlenmesi uygulama tarafından tamamen tanımlanmıştır. Sistemin tamamını sıfırlamak için ihlal iş parçacığını askıya almadan herhangi bir şey yapılabilir.

> [!IMPORTANT]
> *Bu hizmetin performans bilgilerini döndürmesi* Için *threadx kitaplığı,* **TX_ENABLE_STACK_CHECKING** tanımlanmış olarak oluşturulmalıdır.

### <a name="parameters"></a>Parametreler
- **error_handler** Uygulamanın yığın hata işleme işlevine yönelik işaretçi. Bu değer TX_NULL, bildirim devre dışı bırakılır.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı iş parçacığı sıfırlaması.
- **TX_FEATURE_NOT_ENABLED** (0xFF) sistem, etkin performans bilgileri ile derlenmedi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="example"></a>Örnek

```c
void my_stack_error_handler(TX_THREAD *thread_ptr);

/* Register the "my_stack_error_handler" function with ThreadX
so that thread stack errors can be handled by the application. */
status = tx_thread_stack_error_notify(my_stack_error_handler);

/* If status is TX_SUCCESS the stack error handler is registered.*/
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_thread_create
- tx_thread_delete
- tx_thread_entry_exit_notify
- tx_thread_identify
- tx_thread_info_get
- tx_thread_performance_info_get
- tx_thread_preformance_system_info_get
- tx_thread_preemption_change
- tx_thread_priority_change
- tx_thread_relinquish
- tx_thread_reset
- tx_thread_resume
- tx_thread_sleep
- tx_thread_suspend
- tx_thread_terminate
- tx_thread_time_slice_change
- tx_thread_wait_abort

## <a name="tx_thread_suspend"></a>tx_thread_suspend

Uygulama iş parçacığını askıya al

### <a name="prototype"></a>Prototype

```c
UINT tx_thread_suspend(TX_THREAD *thread_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet belirtilen uygulama iş parçacığını askıya alır. Bir iş parçacığı, kendisini askıya almak için bu hizmeti çağırabilir.

> [!NOTE]
> *Belirtilen iş parçacığı başka bir nedenle zaten askıya alınmışsa, önceki askıya alma yükseltilmemiş olana kadar bu askıya alma işlemi dahili olarak tutulur. Bu gerçekleştiğinde, belirtilen iş parçacığının koşulsuz olarak askıya alınması gerçekleştirilir. Daha fazla koşulsuz askıya alma isteği etkisizdir.*

Askıya alındıktan sonra, yeniden yürütmek için iş parçacığının ***tx_thread_resume*** tarafından sürdürülmeye devam etmelidir.

### <a name="parameters"></a>Parametreler

- **thread_ptr** Uygulama iş parçacığı işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı iş parçacığı askıya alma.
- **TX_THREAD_ERROR** (0x0E) geçersiz uygulama iş parçacığı işaretçisi.
- **TX_SUSPEND_ERROR** (0x14) belirtilen iş parçacığı sonlandırılmış veya tamamlanmış durumda.
- **TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="preemption-possible"></a>Önalım mümkün

Yes

### <a name="example"></a>Örnek

```c
TX_THREAD my_thread;
UINT status;

/* Suspend the thread represented by "my_thread". */
status = tx_thread_suspend(&my_thread);

/* If status equals TX_SUCCESS, the application thread is
unconditionally suspended. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_thread_create
- tx_thread_delete
- tx_thread_entry_exit_notify
- tx_thread_identify
- tx_thread_info_get
- tx_thread_performance_info_get
- tx_thread_performance_system_info_get
- tx_thread_preemption_change
- tx_thread_priority_change
- tx_thread_relinquish
- tx_thread_reset
- tx_thread_resume
- tx_thread_sleep
- tx_thread_stack_error_notify
- tx_thread_terminate
- tx_thread_time_slice_change
- tx_thread_wait_abort

## <a name="tx_thread_terminate"></a>tx_thread_terminate

Uygulama iş parçacığını sonlandırır

### <a name="prototype"></a>Prototype

```c
UINT tx_thread_terminate(TX_THREAD *thread_ptr);
```
### <a name="description"></a>Açıklama

Bu hizmet, iş parçacığının askıya alınmadığına bakılmaksızın belirtilen uygulama iş parçacığını sonlandırır. Bir iş parçacığı, kendisini sonlandırmak için bu hizmeti çağırabilir.

> [!NOTE]
> *İş parçacığının sonlandırma için uygun bir durumda olduğundan emin olmak uygulamanın sorumluluğundadır. Örneğin, bir iş parçacığı kritik uygulama işlemleri sırasında veya bu tür işlemleri bilinmeyen bir durumda bırakabileceği diğer ara yazılım bileşenleri içinde sonlandırmamalıdır.*

> [!IMPORTANT]
> *Sonlandırıldıktan sonra, yeniden yürütülmesi için iş parçacığının sıfırlanması gerekir.*

### <a name="parameters"></a>Parametreler

- **thread_ptr** Uygulama iş parçacığı işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri
- **TX_SUCCESS** (0x00) başarılı iş parçacığı sonlandırılır.
- **TX_THREAD_ERROR** (0x0E) geçersiz uygulama iş parçacığı işaretçisi.
- **TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları ve zamanlayıcılar

### <a name="preemption-possible"></a>Önalım mümkün

Yes

### <a name="example"></a>Örnek

```c
TX_THREAD my_thread;
UINT status;

/* Terminate the thread represented by "my_thread". */
status = tx_thread_terminate(&my_thread);

/* If status equals TX_SUCCESS, the thread is terminated
and cannot execute again until it is reset. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_thread_create tx_thread_delete
- tx_thread_entry_exit_notify
- tx_thread_identify
- tx_thread_info_get
- tx_thread_performance_info_get
- tx_thread_performance_system_info_get
- tx_thread_preemption_change
- tx_thread_priority_change
- tx_thread_relinquish
- tx_thread_reset
- tx_thread_resume
- tx_thread_sleep
- tx_thread_stack_error_notify
- tx_thread_suspend
- tx_thread_time_slice_change
- tx_thread_wait_abort

## <a name="tx_thread_time_slice_change"></a>tx_thread_time_slice_change

Değişiklik saati-uygulama iş parçacığının dilimi

### <a name="prototype"></a>Prototype

```c
UINT tx_thread_time_slice_change(
    TX_THREAD *thread_ptr,
    ULONG new_time_slice, 
    ULONG *old_time_slice);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen uygulama iş parçacığının zaman dilimini değiştirir. Bir iş parçacığı için zaman dilimi seçme, aynı veya daha yüksek önceliklerin diğer iş parçacıklarının yürütme şansı olması için belirtilen sayıda süreölçer işareti yürütümeyeceğini yöntem.

> [!NOTE]
> *Önalım-Threshold kullanılması, belirtilen iş parçacığı için zaman dilimini devre dışı bırakır.*

### <a name="parameters"></a>Parametreler

- **thread_ptr** Uygulama iş parçacığı işaretçisi.
- **new_time_slice** Yeni zaman dilimi değeri. Yasal değerler 1 ile 0xFFFFFFFF arasında TX_NO_TIME_SLICE ve sayısal değerleri içerir.
- **old_time_slice** Belirtilen iş parçacığının önceki timeslice değerini depolamak için konum işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı zaman dilimi şansı.
- **TX_THREAD_ERROR** (0x0E) geçersiz uygulama iş parçacığı işaretçisi.
- **TX_PTR_ERROR** (0x03) önceki zaman dilimi depolama konumuna yönelik geçersiz işaretçi.
- **TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları ve zamanlayıcılar

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```c
TX_THREAD my_thread;
ULONG my_old_time_slice;
UINT status;

/* Change the time-slice of the thread associated with
"my_thread" to 20. This will mean that "my_thread"
can only run for 20 timer-ticks consecutively before
other threads of equal or higher priority get a chance
to run. */
status = tx_thread_time_slice_change(&my_thread, 20,
    &my_old_time_slice);

/* If status equals TX_SUCCESS, the thread’s time-slice
has been changed to 20 and the previous time-slice is
in "my_old_time_slice." */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_thread_create
- tx_thread_delete
- tx_thread_entry_exit_notify
- tx_thread_identify
- tx_thread_info_get
- tx_thread_performance_info_get
- tx_thread_performance_system_info_get
- tx_thread_preemption_change
- tx_thread_priority_change
- tx_thread_relinquish
- tx_thread_reset
- tx_thread_resume
- tx_thread_sleep
- tx_thread_stack_error_notify
- tx_thread_suspend
- tx_thread_terminate
- tx_thread_wait_abort

## <a name="tx_thread_wait_abort"></a>tx_thread_wait_abort

Belirtilen iş parçacığını askıya alma işlemini durdur

### <a name="prototype"></a>Prototype

```c
UINT tx_thread_wait_abort(TX_THREAD *thread_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen iş parçacığının uyku veya diğer nesne askıya alınma işlemini iptal eder. Bekleme iptal edildiğinde, iş parçacığının beklediği hizmetten bir **TX_WAIT_ABORTED** değeri döndürülür.

> [!NOTE]
> *Bu hizmet, tx_thread_suspend hizmeti tarafından yapılan açık askıya alma sürümü oluşturmaz.*

### <a name="parameters"></a>Parametreler

- **thread_ptr** Daha önce oluşturulmuş bir uygulama iş parçacığına işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı iş parçacığı bekleme iptali.
- **TX_THREAD_ERROR** (0x0E) geçersiz uygulama iş parçacığı işaretçisi.
- **TX_WAIT_ABORT_ERROR** (0x1B) belirtilen iş parçacığı bekleme durumunda değil.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="preemption-possible"></a>Önalım mümkün
Yes

### <a name="example"></a>Örnek

```c
TX_THREAD my_thread;
UINT status;

/* Abort the suspension condition of "my_thread." */
status = tx_thread_wait_abort(&my_thread);

/* If status equals TX_SUCCESS, the thread is now ready
again, with a return value showing its suspension
was aborted (TX_WAIT_ABORTED). */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_thread_create
- tx_thread_delete
- tx_thread_entry_exit_notify
- tx_thread_identify
- tx_thread_info_get
- tx_thread_performance_info_get
- tx_thread_performance_system_info_get
- tx_thread_preemption_change
- tx_thread_priority_change
- tx_thread_relinquish
- tx_thread_reset
- tx_thread_resume
- tx_thread_sleep
- tx_thread_stack_error_notify
- tx_thread_suspend
- tx_thread_terminate
- tx_thread_time_slice_change

## <a name="tx_time_get"></a>tx_time_get

Geçerli saati alır

Uygulama zamanlayıcıları

### <a name="prototype"></a>Prototype

```c
ULONG tx_time_get(VOID);
```

### <a name="description"></a>Açıklama

Bu hizmet, iç sistem saatinin içeriğini döndürür. Her timertick, iç sistem saatini bir artırır. Sistem saati, başlatma sırasında sıfır olarak ayarlanır ve hizmet ***tx_time_set*** belirli bir değere değiştirilebilir.

> [!NOTE]
> *Her Zamanlayıcı-onay her temsil eden gerçek zaman uygulamaya özgüdür.*

**Parametreler**

Yok

### <a name="return-values"></a>Dönüş Değerleri

- **sistem saat işaretleri** İç, ücretsiz çalışan, sistem saatinin değeri.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="preemption-possible"></a>Önalım mümkün
Hayır

### <a name="example"></a>Örnek

```c
ULONG current_time;

/* Pickup the current system time, in timer-ticks. */
current_time = tx_time_get();

/* Current time now contains a copy of the internal system
clock. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_time_set

## <a name="tx_time_set"></a>tx_time_set

Geçerli saati ayarlar

### <a name="prototype"></a>Prototype

```c
VOID tx_time_set(ULONG new_time);
```

### <a name="description"></a>Açıklama

Bu hizmet, iç sistem saatini belirtilen değere ayarlar. Her Zamanlayıcı-onay, iç sistem saatini bir artırır.

> [!NOTE]
> *Her Zamanlayıcı-onay her temsil eden gerçek zaman uygulamaya özgüdür.*

### <a name="parameters"></a>Parametreler

- **new_time** Yeni saat, sistem saatine koymak için geçerli değerler 0 ile 0xFFFFFFFF arasındadır.

### <a name="return-values"></a>Dönüş Değerleri

Yok

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, zamanlayıcılar ve ISRs

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```c
/* Set the internal system time to 0x1234. */
tx_time_set(0x1234);

/* Current time now contains 0x1234 until the next timer
interrupt. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_time_get

## <a name="tx_timer_activate"></a>tx_timer_activate

Uygulama zamanlayıcısını etkinleştir

### <a name="prototype"></a>Prototype

```c
UINT tx_timer_activate(TX_TIMER *timer_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen uygulama zamanlayıcısını etkinleştirir. Aynı anda süresi dolan zamanlayıcılar için geçen süre sonu yordamları, etkinleştirildikleri sırada yürütülür.

> [!NOTE]
> *Süre sonu bir tek kararlı Zamanlayıcı, ile*  * sıfırlanması gerekir **tx_timer_change** _ _before yeniden etkinleştirilebilir. *

### <a name="parameters"></a>Parametreler

- **timer_ptr** Daha önce oluşturulmuş bir uygulama süreölçeri işaretçisi.

**Dönüş değerleri**

- **TX_SUCCESS** (0x00) başarılı uygulama süreölçeri etkinleştirmesi.
- **TX_TIMER_ERROR** (0x15) geçersiz uygulama süreölçeri işaretçisi.
- **TX_ACTIVATE_ERROR** (0x17) Zamanlayıcı zaten etkin veya zaten süresi geçmiş tek bir görüntü süreölçeri.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```c
TX_TIMER my_timer;
UINT status;

/* Activate an application timer. Assume that the
application timer has already been created. */
status = tx_timer_activate(&my_timer);

/* If status equals TX_SUCCESS, the application timer is
now active. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_timer_change
- tx_timer_create
- tx_timer_deactivate
- tx_timer_delete
- tx_timer_info_get
- tx_timer_performance_info_get
- tx_timer_performance_system_info_get

## <a name="tx_timer_change"></a>tx_timer_change

Uygulama zamanlayıcısını değiştirme

### <a name="prototype"></a>Prototype

```c
UINT tx_timer_change(
    TX_TIMER *timer_ptr,
    ULONG initial_ticks, 
    ULONG reschedule_ticks);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen uygulama süreölçerinin süre sonu özelliklerini değiştirir. Bu hizmet çağrılmadan önce zamanlayıcı devre dışı bırakılmalıdır.

> [!NOTE]
> *Öğesine*  * bir çağrı Zamanlayıcıyı yeniden başlatmak için bu hizmetten sonra **tx_timer_activate** _ _Service gereklidir. *

### <a name="parameters"></a>Parametreler

- **timer_ptr** Zamanlayıcı denetim bloğunun işaretçisi.
- **initial_ticks** Zamanlayıcı süre sonu için başlangıç onay işareti sayısını belirtir. Yasal değerler 1 ile 0xFFFFFFFF arasındadır.
- **reschedule_ticks** İlk süre sonra tüm süreölçer süre sonları için onay işareti sayısını belirtir. Bu parametre için bir sıfır, zamanlayıcının *tek bir görüntü* süreölçeri olmasını sağlar. Aksi takdirde, düzenli zamanlayıcılar için 1 ile 0xFFFFFFFF arasında geçerli değerler değişir.

> [!NOTE]
> *Süre sonu bir tek kararlı Zamanlayıcı, ile* 
* sıfırlanması gerekir **tx_timer_change** _ _before yeniden etkinleştirilebilir. *

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı uygulama süreölçeri değişikliği.
- **TX_TIMER_ERROR** (0x15) geçersiz uygulama süreölçeri işaretçisi.
- **TX_TICK_ERROR** (0x16) ilk Ticks için geçersiz değer (sıfır) sağlandı.
- **TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, zamanlayıcılar ve ISRs

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```c
TX_TIMER my_timer;
UINT status;

/* Change a previously created and now deactivated timer
to expire every 50 timer ticks, including the initial
expiration. */
status = tx_timer_change(&my_timer,50, 50);

/* If status equals TX_SUCCESS, the specified timer is
changed to expire every 50 ticks. */

/* Activate the specified timer to get it started again. */
status = tx_timer_activate(&my_timer);
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_timer_activate
- tx_timer_create
- tx_timer_deactivate
- tx_timer_delete
- tx_timer_info_get
- tx_timer_performance_info_get
- tx_timer_performance_system_info_get

## <a name="tx_timer_create"></a>tx_timer_create

Uygulama süreölçeri oluştur

### <a name="prototype"></a>Prototype

```c
UINT tx_timer_create(
    TX_TIMER *timer_ptr, 
    CHAR *name_ptr,
    VOID (*expiration_function)(ULONG),
    ULONG expiration_input, 
    ULONG initial_ticks,
    ULONG reschedule_ticks, 
    UINT auto_activate);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen süre sonu işleviyle ve periyodik olarak bir uygulama süreölçeri oluşturur.

### <a name="parameters"></a>Parametreler

- **timer_ptr** Zamanlayıcı denetim bloğu işaretçisi
- **name_ptr** Süreölçerin adı işaretçisi.
- **expiration_function** Süreölçerin süresi dolduğunda çağrılacak uygulama işlevi.
- **expiration_input** Zamanlayıcı süresi dolduğunda sona erme işlevine geçirilecek giriş.
- **initial_ticks** Zamanlayıcı süre sonu için başlangıç onay işareti sayısını belirtir. Yasal değerler 1 ile 0xFFFFFFFF arasındadır.
- **reschedule_ticks** İlk süre sonra tüm süreölçer süre sonları için onay işareti sayısını belirtir. Bu parametre için bir sıfır, zamanlayıcının *tek bir görüntü* süreölçeri olmasını sağlar. Aksi takdirde, düzenli zamanlayıcılar için 1 ile 0xFFFFFFFF arasında geçerli değerler değişir.

  > [!NOTE]
  > *Tek bir anlık zamanlayıcı süresi dolduktan sonra, yeniden etkinleştirilmeden önce tx_timer_change aracılığıyla sıfırlanması gerekir.*

- **Auto_Activate** Süreölçerin oluşturma sırasında otomatik olarak etkinleştirildiğini belirler. Bu değer **TX_AUTO_ACTIVATE** (0x01), süreölçer etkin hale getirilir. Aksi takdirde, **TX_NO_ACTIVATE** (0x00) değeri seçilirse, süreölçer etkin olmayan bir durumda oluşturulur. Bu durumda, süreölçer 'in gerçekten başlatılmış olması için sonraki bir **_tx_timer_activate_** hizmet çağrısı gerekir.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı uygulama süreölçeri oluşturma.
- **TX_TIMER_ERROR** (0x15) geçersiz uygulama süreölçeri işaretçisi. İşaretçi NULL ya da süreölçer zaten oluşturulmuş.
- **TX_TICK_ERROR** (0x16) ilk Ticks için geçersiz değer (sıfır) sağlandı.
- **TX_ACTIVATE_ERROR** (0x17) geçersiz etkinleştirme seçildi.
- **TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

Başlatma ve iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```c
TX_TIMER my_timer;
UINT status;

/* Create an application timer that executes
"my_timer_function" after 100 ticks initially and then
after every 25 ticks. This timer is specified to start
immediately! */
status = tx_timer_create(&my_timer,"my_timer_name",
    my_timer_function, 0x1234, 100, 25,
    TX_AUTO_ACTIVATE);

/* If status equals TX_SUCCESS, my_timer_function will
be called 100 timer ticks later and then called every
25 timer ticks. Note that the value 0x1234 is passed to
my_timer_function every time it is called. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_timer_activate
- tx_timer_change
- tx_timer_deactivate
- tx_timer_delete
- tx_timer_info_get
- tx_timer_performance_info_get
- tx_timer_performance_system_info_get

## <a name="tx_timer_deactivate"></a>tx_timer_deactivate

Uygulama zamanlayıcısını devre dışı bırak

### <a name="prototype"></a>Prototype

```c
UINT tx_timer_deactivate(TX_TIMER *timer_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen uygulama zamanlayıcısını devre dışı bırakır. Süreölçer zaten devre dışı bırakılmışsa, bu hizmetin bir etkisi yoktur.

### <a name="parameters"></a>Parametreler

- **timer_ptr** Daha önce oluşturulmuş bir uygulama süreölçeri işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı uygulama süreölçeri devre dışı bırakma.
- **TX_TIMER_ERROR** (0x15) geçersiz uygulama süreölçeri işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```c
TX_TIMER my_timer;
UINT status;

/* Deactivate an application timer. Assume that the
application timer has already been created. */
status = tx_timer_deactivate(&my_timer);

/* If status equals TX_SUCCESS, the application timer is
now deactivated. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_timer_activate
- tx_timer_change
- tx_timer_create
- tx_timer_delete
- tx_timer_info_get
- tx_timer_performance_info_get
- tx_timer_performance_system_info_get

## <a name="tx_timer_delete"></a>tx_timer_delete

Uygulama zamanlayıcısını Sil

### <a name="prototype"></a>Prototype

```c
UINT tx_timer_delete(TX_TIMER *timer_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen uygulama zamanlayıcısını siler.

> [!NOTE]
> *Silinen bir zamanlayıcının kullanımını önleyen uygulamanın sorumluluğundadır.*

### <a name="parameters"></a>Parametreler

- **timer_ptr** Daha önce oluşturulmuş bir uygulama süreölçeri işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı uygulama süreölçeri silme.
- **TX_TIMER_ERROR** (0x15) geçersiz uygulama süreölçeri işaretçisi.
- **TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```c
TX_TIMER my_timer;
UINT status;

/* Delete application timer. Assume that the application
timer has already been created. */
status = tx_timer_delete(&my_timer);

/* If status equals TX_SUCCESS, the application timer is
deleted. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_timer_activate
- tx_timer_change
- tx_timer_create
- tx_timer_deactivate
- tx_timer_info_get
- tx_timer_performance_info_get
- tx_timer_performance_system_info_get

## <a name="tx_timer_info_get"></a>tx_timer_info_get

Uygulama süreölçeri hakkında bilgi alma

### <a name="prototype"></a>Prototype

```c
UINT tx_timer_info_get(
    TX_TIMER *timer_ptr, 
    CHAR **name,
    UINT *active,
    ULONG *remaining_ticks,
    ULONG *reschedule_ticks,
    TX_TIMER **next_timer);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen uygulama süreölçeri hakkında bilgi alır.

### <a name="parameters"></a>Parametreler

- **timer_ptr** Daha önce oluşturulmuş bir uygulama süreölçeri işaretçisi.
- **ad** Süreölçerin adına işaretçi için hedef işaretçisi.
- **etkin** Süreölçer etkin göstergesi için hedef işaretçisi. Süreölçer devre dışı bırakılırsa veya bu hizmet zamanlayıcının kendisinden çağrılırsa bir **TX_FALSE** değeri döndürülür. Aksi takdirde, süreölçer etkin ise bir **TX_TRUE** değeri döndürülür.
- **remaining_ticks** Süreölçer süresi dolmadan önce bırakılan Zamanlayıcı onay işareti sayısı için hedef işaretçisi.
- **reschedule_ticks** Bu süreölçeri otomatik olarak yeniden çizelgelemek için kullanılacak süreölçer onay işareti sayısı için hedef işaretçisi. Değer sıfırsa, süreölçer tek bir çekmeydir ve yeniden planlanmayacaktır.
- **next_timer** Sonraki oluşturulan uygulama süreölçerinin işaretçisi için hedef işaretçisi.

> [!NOTE]
> *Herhangi bir parametre için **TX_NULL** sağlama, parametrenin gerekli olmadığını gösterir.*

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı Zamanlayıcı bilgisi alma.
- **TX_TIMER_ERROR** (0x15) geçersiz uygulama süreölçeri işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```c
TX_TIMER my_timer;
CHAR *name;
UINT active;
ULONG remaining_ticks;
ULONG reschedule_ticks;
TX_TIMER *next_timer;
UINT status;

/* Retrieve information about the previously created
application timer "my_timer." */
status = tx_timer_info_get(&my_timer, &name,
    &active,&remaining_ticks,
    &reschedule_ticks,
    &next_timer);

/* If status equals TX_SUCCESS, the information requested is
valid. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_timer_activate
- tx_timer_change
- tx_timer_create
- tx_timer_deactivate
- tx_timer_delete
- tx_timer_info_get
- tx_timer_performance_info_get
- tx_timer_performance_system_info_get

## <a name="tx_timer_performance_info_get"></a>tx_timer_performance_info_get

Zamanlayıcı performans bilgilerini al

### <a name="prototype"></a>Prototype

```c
UINT tx_timer_performance_info_get(
    TX_TIMER *timer_ptr,
    ULONG *activates, 
    ULONG *reactivates,
    ULONG *deactivates, 
    ULONG *expirations,
    ULONG *expiration_adjusts);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen uygulama süreölçeri hakkında performans bilgilerini alır.

> [!IMPORTANT]
> *Işparçacığıx kitaplığı ve uygulaması ile*  * oluşturulmalıdır Bu hizmetin performans bilgilerini döndürmesi için **TX_TIMER_ENABLE_PERFORMANCE_INFO** _ _defined. *

### <a name="parameters"></a>Parametreler
- **timer_ptr** Daha önce oluşturulan Zamanlayıcı işaretçisi.
- **etkinleştirir** Bu zamanlayıcıda gerçekleştirilen etkinleştirme isteklerinin sayısı için hedef işaretçisi.
- yeniden **etkinleştirir** Bu dönemsel süreölçer üzerinde gerçekleştirilen otomatik yeniden etkinleştirme sayısı için hedef işaretçisi.
- **devre dışı bırakır** Bu zamanlayıcıda gerçekleştirilen devre dışı bırakma isteklerinin sayısı için hedef işaretçisi.
- **süre sonları** Bu zamanlayıcının süre sonu sayısı için hedef işaretçisi.
- **expiration_adjusts** Bu zamanlayıcıda gerçekleştirilen iç süre sonu ayarlamaları sayısı için hedef işaretçisi. Bu ayarlamalar, varsayılan Zamanlayıcı listesi boyutundan daha büyük olan zamanlayıcılar için süreölçer kesme işlemi sırasında yapılır (varsayılan süre sonu 32 ' den büyük olan zamanlayıcılar).

> NOTUN *Herhangi bir parametre için TX_NULL sağlamak, parametrenin gerekli olmadığını gösterir.*

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı Zamanlayıcı performansı al.
- **TX_PTR_ERROR** (0x03) geçersiz süreölçer işaretçisi.
- **TX_FEATURE_NOT_ENABLED** (0xFF) sistem, etkin performans bilgileri ile derlenmedi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="example"></a>Örnek

```c
TX_TIMER my_timer;
ULONG activates;
ULONG reactivates;
ULONG deactivates;
ULONG expirations;
ULONG expiration_adjusts;

/* Retrieve performance information on the previously created
timer. */
status = tx_timer_performance_info_get(&my_timer, &activates,
    &reactivates,&deactivates, &expirations,
    &expiration_adjusts);

/* If status is TX_SUCCESS the performance information was
successfully retrieved. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_timer_activate
- tx_timer_change
- tx_timer_create
- tx_timer_deactivate
- tx_timer_delete
- tx_timer_info_get
- tx_timer_performance_system_info_get

## <a name="tx_timer_performance_system_info_get"></a>tx_timer_performance_system_info_get

Zamanlayıcı sistemi performans bilgilerini al

### <a name="prototype"></a>Prototype

```c
UINT tx_timer_performance_system_info_get(
    ULONG *activates,
    ULONG *reactivates, 
    ULONG *deactivates,
    ULONG *expirations, 
    ULONG *expiration_adjusts);
```

### <a name="description"></a>Açıklama

Bu hizmet, sistemdeki tüm uygulama zamanlayıcıları hakkındaki performans bilgilerini alır.

> [!IMPORTANT]
> *ThreadX kitaplığı ve uygulaması,*  *performans bilgilerini döndürmek için bu hizmetin tanımlanmış* TX_TIMER_ENABLE_PERFORMANCE_INFO oluşturulmalıdır.

**Parametreler**

- **etkinleştirir** Tüm zamanlayıcılar üzerinde gerçekleştirilen etkinleştirme isteklerinin toplam sayısı için hedef işaretçisi.
- yeniden **etkinleştirir** Tüm düzenli zamanlayıcıların toplam otomatik yeniden etkinleştirme sayısı için hedef işaretçisi.
- **devre dışı bırakır** Tüm zamanlayıcılar üzerinde gerçekleştirilen devre dışı bırakma isteklerinin toplam sayısı için hedef işaretçisi.
- **süre sonları** Tüm zamanlayıcılar üzerindeki toplam süre sonu sayısının hedefi işaretçisi.
- **expiration_adjusts** Tüm zamanlayıcılar üzerinde gerçekleştirilen toplam iç sona erme ayarlamaları sayısı için hedef işaretçisi. Bu ayarlamalar, varsayılan Zamanlayıcı listesi boyutundan daha büyük olan zamanlayıcılar için süreölçer kesme işlemi sırasında yapılır (varsayılan süre sonu 32 ' den büyük olan zamanlayıcılar).

> [!NOTE]
> *Herhangi bir parametre için **TX_NULL** sağlama, parametrenin gerekli olmadığını gösterir.*

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı Zamanlayıcı sistem performansı al.
- **TX_FEATURE_NOT_ENABLED** (0xFF) sistem, etkin performans bilgileri ile derlenmedi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="example"></a>Örnek

```c
ULONG activates;
ULONG reactivates;
ULONG deactivates;
ULONG expirations;
ULONG expiration_adjusts;

/* Retrieve performance information on all previously created
timers. */
status = tx_timer_performance_system_info_get(&activates,
    &reactivates, &deactivates, &expirations,
    &expiration_adjusts);

/* If status is TX_SUCCESS the performance information was
successfully retrieved. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- tx_timer_activate
- tx_timer_change
- tx_timer_create
- tx_timer_deactivate
- tx_timer_delete
- tx_timer_info_get
- tx_timer_performance_info_get
