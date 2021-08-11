---
title: Bölüm 6-Azure RTOS ThreadX için tanıtım sistemi
description: Bu bölüm, tüm Azure RTOS ThreadX işlemci desteği paketleriyle birlikte sunulan tanıtım sisteminin bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 67054d67d0a6babc50a489c4ec4b738abf3efccab10060d307106e8344b00d02
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116783382"
---
# <a name="chapter-6---demonstration-system-for-azure-rtos-threadx"></a>Bölüm 6-Azure RTOS ThreadX için tanıtım sistemi

Bu bölüm, tüm Azure RTOS ThreadX işlemci desteği paketleriyle birlikte sunulan tanıtım sisteminin bir açıklamasını içerir.

## <a name="overview"></a>Genel Bakış

Her ThreadX ürün dağıtımı, desteklenen tüm mikro işlemcilerde çalışan bir tanıtım sistemi içerir.

Bu örnek sistem, ***demo_threadx. c*** dağıtım dosyasında tanımlanmıştır ve threadx 'in gömülü bir çoklu iş parçacıklı ortamda nasıl kullanıldığını göstermek için tasarlanmıştır. Tanıtım, başlatma, sekiz iş parçacığı, bir bayt havuzu, bir blok havuzu, bir kuyruk, bir semafor, bir mutex ve bir olay bayrakları grubundan oluşur.

> [!NOTE]
> *İş parçacığının yığın boyutu dışında, tanıtım uygulaması tüm ThreadX desteklenen işlemcilerde aynıdır.*

Bu bölümün geri kalanında başvurulan satır numaraları dahil olmak üzere ***demo_threadx. c*** öğesinin tüm listesi.

## <a name="application-define"></a>Uygulama tanımlama

***Tx_application_define*** işlevi, temel threadx başlatma işlemi tamamlandıktan sonra yürütülür. İş parçacıkları, kuyruklar, Semaforlar, zaman uyumu sağlayıcılar, olay bayrakları ve bellek havuzları dahil olmak üzere tüm ilk sistem kaynaklarını ayarlamaktan sorumludur.

Tanıtım sisteminin ***tx_application_define** _ (_line numaraları 60-164 *), tanıtım nesnelerini aşağıdaki sırayla oluşturur:

- byte_pool_0
- thread_0
- thread_1
- thread_2
- thread_3
- thread_4
- thread_5
- thread_6
- thread_7
- queue_0
- semaphore_0
- event_flags_0
- mutex_0
- block_pool_0

Tanıtım sistemi başka hiçbir ek ThreadX nesnesi oluşturmaz. Ancak gerçek bir uygulama, iş parçacıklarının yürütülmesi sırasında çalışma zamanı sırasında sistem nesneleri oluşturabilir.

### <a name="initial-execution"></a>İlk yürütme

Tüm iş parçacıkları **TX_AUTO_START** seçeneğiyle oluşturulur. Bu, başlangıçta yürütülmeye hazırmasını sağlar. ***Tx_application_define*** tamamlandıktan sonra Denetim, iş parçacığı zamanlayıcısına aktarılır ve her bir iş parçacığına buradan gönderilir.

İş parçacıklarının yürütülme sırası önceliklerine göre ve oluşturuldukları sırada belirlenir. Tanıtım sisteminde, en yüksek önceliğe sahip olduğundan (*1 önceliğiyle oluşturulmuştur*), ilk olarak ***thread_0*** yürütülür. ***Thread_0*** askıya aldıktan sonra, ***thread_5*** yürütülür ve ardından ***thread_3** _, _*_thread_4_*_, _*_thread_6_*_, _* _thread_7_* *, ***thread_1**_, ve finally _ *_thread_2_* * yürütülür.

> [!NOTE]
> ***Thread_3** ve **thread_4** aynı önceliğe sahip olsa da (her ikisi de 8 önceliğiyle oluşturulmuştur), ilk olarak **thread_3** yürütülür. Bunun nedeni **thread_3** oluşturulması ve **thread_4** önce hazırlanmaya gelmiştir. Eşit önceliğe sahip iş parçacıkları bir FıFO olarak yürütülür.*

## <a name="thread-0"></a>İş parçacığı 0

İşlevi ***thread_0_entry*** iş parçacığının giriş noktasını işaretler *(satırlar 167-190*). ***Thread_0*** , tanıtım sisteminde yürütülecek ilk iş parçacığıdır. İşlem basittir: sayacını artırır, 10 Zamanlayıcı onay işaretleri için uyku moduna geçer, ***thread_5*** uyanma için bir olay bayrağı ayarlar ve sonra diziyi yineler.

***Thread_0*** , sistemdeki en yüksek öncelikli iş parçacığıdır. İstenen uyku süresi sona erdiğinde, gösteride çalışan diğer iş parçacıklarını da çalışır hale gelir.

## <a name="thread-1"></a>İş parçacığı 1

***Thread_1_entry** _ işlevi iş parçacığının giriş noktasını işaretler _(satırlar 193-216 *). ***Thread_1*** , tanıtım sisteminde yürütülecek ikinci-son iş parçacığıdır. İşlemesi, sayacını arttırmadan, ***thread_2*** bir ileti göndermekten (** ***queue_0***) ve diziyi tekrarlarından oluşur. ***Thread_1**_ _*_queue_0_*_ dolduğunda her zaman askıya alınır (_line 207 *).

## <a name="thread-2"></a>İş parçacığı 2

İşlevi ***thread_2_entry*** iş parçacığının giriş noktasını işaretler *(satırlar 219-243*). ***Thread_2*** , tanıtım sisteminde yürütülecek son iş parçacığıdır. İşlemesi, sayacını arttırmadan, ***thread_1*** ( ***queue_0***) bir ileti almaya ve sırayı tekrarlamadan oluşur. ***Thread_2** _ _*_queue_0_*_ boş olduğunda askıya alınır (_line 233 *).

***Thread_1** _ ve _ *_thread_2_**, tanıtım sisteminde en düşük önceliği (* öncelik 16 *) paylaşmasına rağmen *3 ve 4 iş parçacıklarında*

, aynı zamanda yalnızca yürütme için hazırlanma iş parçacıklarından oluşur. Bunlar aynı zamanda, zaman dilimle oluşturulan tek iş parçacıklarında (*satırlar 87 ve 93*). Diğer iş parçacığı yürütülmeden önce, her iş parçacığının en fazla 4 süreölçer işareti yürütmesine izin verilir.

## <a name="threads-3-and-4"></a>İş parçacıkları 3 ve 4

İşlev ***thread_3_and_4_entry*** hem ***thread_3** _ hem de _ *_thread_4_** giriş noktasını işaretler (satırlar 246-280). Her iki iş parçacığı da 8 önceliğine sahiptir ve bu, tanıtım sistemindeki üçüncü ve dördüncü iş parçacıklarının yürütülmesine neden olur. Her iş parçacığı için işleme aynıdır: sayacını artırma, ***semaphore_0*** alma, 2 Zamanlayıcı onay işareti için uyuyan, ***semaphore_0*** serbest bırakma ve sırayı yineleme. Her bir iş parçacığının ***semaphore_0*** kullanılamadığı zaman askıya aldığından emin olun (satır 264).

Ayrıca, her iki iş parçacığı de ana işlemleri için aynı işlevi kullanır.
Bu, her ikisi de kendi benzersiz yığınına sahip olduğundan ve C doğal olarak yeniden alındığından, sorun yoktur. Her bir iş parçacığı, ne zaman iş parçacığı giriş parametresi (satır 258), ne zaman oluşturulduklarında (satır 102 ve 109) inceleyerek olduğunu belirler.

> [!NOTE]
> *İş parçacığı yürütme sırasında geçerli iş parçacığı noktasını almak ve bunu denetim bloğunun adresiyle karşılaştırmak, iş parçacığı kimliğini belirleyebilmek için de makul bir işlem olur.*

## <a name="thread-5"></a>İş parçacığı 5

İşlevi ***thread_5_entry*** iş parçacığının giriş noktasını işaretler (satırlar 283-305). ***Thread_5*** , tanıtım sisteminde yürütülecek ikinci iş parçacığıdır. İşlemesi, sayacını arttırmadan, ***thread_0*** ( ***event_flags_0*** aracılığıyla) bir olay bayrağını almaya ve sırayı tekrarlamadan oluşur. ***Thread_5*** , ***event_flags_0*** içindeki olay bayrağını her ne zaman askıya alacağını (satır 298) unutmayın.

## <a name="threads-6-and-7"></a>İş parçacıkları 6 ve 7

İşlev ***thread_6_and_7_entry*** hem ***thread_6** _ hem de _ *_thread_7_** giriş noktasını işaretler (satırlar 307-358). Her iki iş parçacığı da 8 önceliğine sahiptir ve bu da, tanıtım sistemindeki beşinci ve altıncı iş parçacıklarını yürütür. Her iş parçacığı için işleme aynıdır: sayacını artırma, iki kez ***mutex_0*** alma, 2 Zamanlayıcı işareti için uyuyan, ***mutex_0*** iki kez serbest bırakma ve diziyi yineleme. Her bir iş parçacığının ***mutex_0*** kullanılamadığı zaman askıya aldığından emin olun (satır 325).

Ayrıca, her iki iş parçacığı de ana işlemleri için aynı işlevi kullanır. Bu, her ikisi de kendi benzersiz yığınına sahip olduğundan ve C doğal olarak yeniden alındığından, sorun yoktur.
Her bir iş parçacığı, ne zaman iş parçacığı giriş parametresi (satır 319), ne zaman oluşturulduklarında (satır 126 ve 133) inceleyerek olduğunu belirler.

## <a name="observing-the-demonstration"></a>Tanıtımı gözlemleme

Tanıtım iş parçacıklarının her biri kendi benzersiz sayacını arttırır.
Demo işlemini denetlemek için aşağıdaki sayaçlar incelenmeyebilir:

- thread_0_counter
- thread_1_counter
- thread_2_counter
- thread_3_counter
- thread_4_counter
- thread_5_counter
- thread_6_counter
- thread_7_counter

Bu sayaçların her biri, tanıtım yürütüldüğünde, ***thread_1_counter** _ ve _ *_thread_2_counter_** en hızlı hızda artan şekilde artmaya devam etmelidir.

## <a name="distribution-file-demo_threadxc"></a>Dağıtım dosyası: demo_threadx. c

Bu bölümde, bu bölüm boyunca başvurulan satır numaraları dahil olmak üzere ***demo_threadx. c***' nin tüm listesi görüntülenir.

```c
/* This is a small demo of the high-performance ThreadX kernel. It includes examples of eight
threads of different priorities, using a message queue, semaphore, mutex, event flags group,
byte pool, and block pool. */

#include "tx_api.h"

#define DEMO_STACK_SIZE 1024
#define DEMO_BYTE_POOL_SIZE 9120
#define DEMO_BLOCK_POOL_SIZE 100
#define DEMO_QUEUE_SIZE 100

/* Define the ThreadX object control blocks... */

TX_THREAD thread_0;
TX_THREAD thread_1;
TX_THREAD thread_2;
TX_THREAD thread_3;
TX_THREAD thread_4;
TX_THREAD thread_5;
TX_THREAD thread_6;
TX_THREAD thread_7;
TX_QUEUE queue_0;
TX_SEMAPHORE semaphore_0;
TX_MUTEX mutex_0;
TX_EVENT_FLAGS_GROUP event_flags_0;
TX_BYTE_POOL byte_pool_0;
TX_BLOCK_POOL block_pool_0;

/* Define the counters used in the demo application... */

ULONG thread_0_counter;
ULONG thread_1_counter;
ULONG thread_1_messages_sent;
ULONG thread_2_counter;
ULONG thread_2_messages_received;
ULONG thread_3_counter;
ULONG thread_4_counter;
ULONG thread_5_counter;
ULONG thread_6_counter;
ULONG thread_7_counter;

/* Define thread prototypes. */

void thread_0_entry(ULONG thread_input);
void thread_1_entry(ULONG thread_input);
void thread_2_entry(ULONG thread_input);
void thread_3_and_4_entry(ULONG thread_input);
void thread_5_entry(ULONG thread_input);
void thread_6_and_7_entry(ULONG thread_input);


/* Define main entry point. */

int main()
{
    /* Enter the ThreadX kernel. */
    tx_kernel_enter();
}

/* Define what the initial system looks like. */
void tx_application_define(void *first_unused_memory)
{

    CHAR *pointer;

    /* Create a byte memory pool from which to allocate the thread stacks. */
    tx_byte_pool_create(&byte_pool_0, "byte pool 0", first_unused_memory,
        DEMO_BYTE_POOL_SIZE);

    /* Put system definition stuff in here, e.g., thread creates and other assorted
        create information. */

    /* Allocate the stack for thread 0. */
    tx_byte_allocate(&byte_pool_0, &pointer, DEMO_STACK_SIZE, TX_NO_WAIT);

    /* Create the main thread. */
    tx_thread_create(&thread_0, "thread 0", thread_0_entry, 0,
        pointer, DEMO_STACK_SIZE,
        1, 1, TX_NO_TIME_SLICE, TX_AUTO_START);

    /* Allocate the stack for thread 1. */
    tx_byte_allocate(&byte_pool_0, &pointer, DEMO_STACK_SIZE, TX_NO_WAIT);

    /* Create threads 1 and 2. These threads pass information through a ThreadX
        message queue. It is also interesting to note that these threads have a time
        slice. */
    tx_thread_create(&thread_1, "thread 1", thread_1_entry, 1,
        pointer, DEMO_STACK_SIZE,
        16, 16, 4, TX_AUTO_START);

    /* Allocate the stack for thread 2. */
    tx_byte_allocate(&byte_pool_0, &pointer, DEMO_STACK_SIZE, TX_NO_WAIT);
        tx_thread_create(&thread_2, "thread 2", thread_2_entry, 2,
        pointer, DEMO_STACK_SIZE,
        16, 16, 4, TX_AUTO_START);

    /* Allocate the stack for thread 3. */
    tx_byte_allocate(&byte_pool_0, &pointer, DEMO_STACK_SIZE, TX_NO_WAIT);

    /* Create threads 3 and 4. These threads compete for a ThreadX counting semaphore.
        An interesting thing here is that both threads share the same instruction area. */
    tx_thread_create(&thread_3, "thread 3", thread_3_and_4_entry, 3,
        pointer, DEMO_STACK_SIZE,
        8, 8, TX_NO_TIME_SLICE, TX_AUTO_START);

    /* Allocate the stack for thread 4. */
    tx_byte_allocate(&byte_pool_0, &pointer, DEMO_STACK_SIZE, TX_NO_WAIT);

    tx_thread_create(&thread_4, "thread 4", thread_3_and_4_entry, 4,
        pointer, DEMO_STACK_SIZE,
        8, 8, TX_NO_TIME_SLICE, TX_AUTO_START);

    /* Allocate the stack for thread 5. */
    tx_byte_allocate(&byte_pool_0, &pointer, DEMO_STACK_SIZE, TX_NO_WAIT);

    /* Create thread 5. This thread simply pends on an event flag, which will be set
        by thread_0. */
    tx_thread_create(&thread_5, "thread 5", thread_5_entry, 5,
        pointer, DEMO_STACK_SIZE,
        4, 4, TX_NO_TIME_SLICE, TX_AUTO_START);

    /* Allocate the stack for thread 6. */
    tx_byte_allocate(&byte_pool_0, &pointer, DEMO_STACK_SIZE, TX_NO_WAIT);

    /* Create threads 6 and 7. These threads compete for a ThreadX mutex. */
    tx_thread_create(&thread_6, "thread 6", thread_6_and_7_entry, 6,
        pointer, DEMO_STACK_SIZE,
        8, 8, TX_NO_TIME_SLICE, TX_AUTO_START);

    /* Allocate the stack for thread 7. */
    tx_byte_allocate(&byte_pool_0, &pointer, DEMO_STACK_SIZE, TX_NO_WAIT);

    tx_thread_create(&thread_7, "thread 7", thread_6_and_7_entry, 7,
        pointer, DEMO_STACK_SIZE,
        8, 8, TX_NO_TIME_SLICE, TX_AUTO_START);

    /* Allocate the message queue. */
    tx_byte_allocate(&byte_pool_0, &pointer, DEMO_QUEUE_SIZE*sizeof(ULONG), TX_NO_WAIT);

    /* Create the message queue shared by threads 1 and 2. */
    tx_queue_create(&queue_0, "queue 0", TX_1_ULONG, pointer, DEMO_QUEUE_SIZE*sizeof(ULONG));

    /* Create the semaphore used by threads 3 and 4. */
    tx_semaphore_create(&semaphore_0, "semaphore 0", 1);

    /* Create the event flags group used by threads 1 and 5. */
    tx_event_flags_create(&event_flags_0, "event flags 0");

    /* Create the mutex used by thread 6 and 7 without priority inheritance. */
    tx_mutex_create(&mutex_0, "mutex 0", TX_NO_INHERIT);

    /* Allocate the memory for a small block pool. */
    tx_byte_allocate(&byte_pool_0, &pointer, DEMO_BLOCK_POOL_SIZE, TX_NO_WAIT);

    /* Create a block memory pool to allocate a message buffer from. */
    tx_block_pool_create(&block_pool_0, "block pool 0", sizeof(ULONG), pointer,
        DEMO_BLOCK_POOL_SIZE);

    /* Allocate a block and release the block memory. */
    tx_block_allocate(&block_pool_0, &pointer, TX_NO_WAIT);

    /* Release the block back to the pool. */
    tx_block_release(pointer);
}

/* Define the test threads. */
void thread_0_entry(ULONG thread_input)
{
    UINT status;


    /* This thread simply sits in while-forever-sleep loop. */
    while(1)
    {

        /* Increment the thread counter. */
        thread_0_counter++;

        /* Sleep for 10 ticks. */
        tx_thread_sleep(10);

        /* Set event flag 0 to wakeup thread 5. */
        status = tx_event_flags_set(&event_flags_0, 0x1, TX_OR);

        /* Check status. */
        if (status != TX_SUCCESS)
            break;
    }
}


void thread_1_entry(ULONG thread_input)
{
    UINT status;


    /* This thread simply sends messages to a queue shared by thread 2. */
    while(1)
    {
        /* Increment the thread counter. */
        thread_1_counter++;

        /* Send message to queue 0. */
        status = tx_queue_send(&queue_0, &thread_1_messages_sent, TX_WAIT_FOREVER);

        /* Check completion status. */
        if (status != TX_SUCCESS)
            break;

        /* Increment the message sent. */
        thread_1_messages_sent++;
    }
}


void thread_2_entry(ULONG thread_input)
{
    ULONG received_message;
    UINT status;

    /* This thread retrieves messages placed on the queue by thread 1. */
    while(1)
    {
        /* Increment the thread counter. */
        thread_2_counter++;

        /* Retrieve a message from the queue. */
        status = tx_queue_receive(&queue_0, &received_message, TX_WAIT_FOREVER);

        /* Check completion status and make sure the message is what we
        expected. */
        if ((status != TX_SUCCESS) || (received_message != thread_2_messages_received))
            break;

        /* Otherwise, all is okay. Increment the received message count. */
        thread_2_messages_received++;
    }
}


void thread_3_and_4_entry(ULONG thread_input)
{
    UINT status;


    /* This function is executed from thread 3 and thread 4. As the loop
    below shows, these function compete for ownership of semaphore_0. */
    while(1)
    {
        /* Increment the thread counter. */
        if (thread_input == 3)
            thread_3_counter++;
        else
            thread_4_counter++;

        /* Get the semaphore with suspension. */
        status = tx_semaphore_get(&semaphore_0, TX_WAIT_FOREVER);

        /* Check status. */
        if (status != TX_SUCCESS)
            break;

        /* Sleep for 2 ticks to hold the semaphore. */
        tx_thread_sleep(2);

        /* Release the semaphore. */
        status = tx_semaphore_put(&semaphore_0);

        /* Check status. */
        if (status != TX_SUCCESS)
            break;
    }
}


void thread_5_entry(ULONG thread_input)
{
    UINT status;
    ULONG actual_flags;


    /* This thread simply waits for an event in a forever loop. */
    while(1)
    {
        /* Increment the thread counter. */
        thread_5_counter++;

        /* Wait for event flag 0. */
        status = tx_event_flags_get(&event_flags_0, 0x1, TX_OR_CLEAR,
            &actual_flags, TX_WAIT_FOREVER);

        /* Check status. */
        if ((status != TX_SUCCESS) || (actual_flags != 0x1))
            break;
    }
}

void thread_6_and_7_entry(ULONG thread_input)
{
    UINT status;

    /* This function is executed from thread 6 and thread 7. As the loop
        below shows, these function compete for ownership of mutex_0. */
    while(1)
    {
        /* Increment the thread counter. */
        if (thread_input == 6)
            thread_6_counter++;
        else
            thread_7_counter++;

        /* Get the mutex with suspension. */
        status = tx_mutex_get(&mutex_0, TX_WAIT_FOREVER);

        /* Check status. */
        if (status != TX_SUCCESS)
            break;

        /* Get the mutex again with suspension. This shows
            that an owning thread may retrieve the mutex it
            owns multiple times. */
        status = tx_mutex_get(&mutex_0, TX_WAIT_FOREVER);

        /* Check status. */
        if (status != TX_SUCCESS)
            break;

        /* Sleep for 2 ticks to hold the mutex. */
        tx_thread_sleep(2);

        /* Release the mutex. */
        status = tx_mutex_put(&mutex_0);

        /* Check status. */
        if (status != TX_SUCCESS)
            break;

        /* Release the mutex again. This will actually
            release ownership since it was obtained twice. */
        status = tx_mutex_put(&mutex_0);

        /* Check status. */
        if (status != TX_SUCCESS)
            break;
    }
}
```
