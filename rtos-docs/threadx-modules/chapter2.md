---
title: Bölüm 2-modül gereksinimleri
description: Bu makale, bir ThreadX modülü oluşturma gereksinimlerinin bir açıklamasıdır.
author: philmea
ms.author: philmea
ms.date: 06/08/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 32288d78ceffb74ab088a1d720dbac657f6d3ed4
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825493"
---
# <a name="chapter-2---module-requirements"></a>Bölüm 2-modül gereksinimleri

Bir ThreadX modülü, modülün temel özelliklerini tanımlayan bir giriş içerir. Girişin ardından modülün yönerge alanı gelir. Modüller yerinde çalıştırılabilir veya yürütmeden önce modül belleği alanına, Modül Yöneticisi tarafından yüklenmiş olabilir. Tek gereksinim, girişin her zaman modülün ilk adresinde yer aldığı gereksinimdir. Şekil 2 ' de temel bir modül düzeni gösterilmektedir.

| Modül düzeni |
|:---:|
| \[modül girişi\]         |
| \[Modül yönerge alanı\] |
| \[Modül RAM alanı\]         |

**Şekil 2** -modül düzeni

> [!NOTE]
> Modüller, uygun konumdan bağımsız kod ve veri derleyicisi/bağlayıcı seçenekleriyle oluşturulmalıdır. Bu, modülün herhangi bir bellek alanında yürütülmesini mümkün.

Bir modül iş parçacığı oluşturulduğunda, iş parçacığı bellek korumalı çekirdekte olduğunda kullanılmak üzere ikinci bir yığın alanı ayrılır. İş parçacığının Çekirdek yığın alanı boyutu,  **_txm_module_port. h_ _ içindeki TXM_MODULE_KERNEL_STACK_SIZE kullanılarak Kullanıcı tarafından yapılandırılabilir *. Bu, bir modül iş parçacığı oluştururken, _ tx_thread_create çağrılırken Kullanıcı tarafından belirtilen yığın yalnızca modülde kullanıldığında daha küçük bir yığın boyutunun kullanılmasına izin verir*** .

> [!NOTE]
> Modül iş parçacığı yığınının en üstü iş parçacığı girişi bilgi yapısını (**TXM_MODULE_THREAD_ENTRY_INFO**) içerir, bu nedenle kullanılabilir yığın boyutu bu yapının boyutuyla azaltılır. Bir modülde iş parçacığı oluştururken, yığın boyutunu en az bu yapının boyutuyla artırın.

Bir ThreadX modülü oluşturmak ve oluşturmak için aşağıdaki adımlar gereklidir (her adım aşağıda daha ayrıntılı olarak açıklanmıştır).

1. Modüldeki tüm C dosyalarının **_txm_module. h_** dahil etmeden önce **TXM_MODULE** #define gerekir. Bu, derlenen kaynak dosyasında veya proje ayarlarının bir parçası olarak gerçekleştirilebilir. Bunun yapılması, ThreadX API çağrılarını, gerçek API işlevine çağrıyı gerçekleştirmek üzere yerleşik modül yöneticisindeki dağıtım işlevini çağıran API 'nin modüle özgü sürümüne yeniden eşler.
2. Her modülün, modülün özelliklerini ve kaynak ihtiyaçlarını tanımlayan ilk yönerge alanı adresinde bir girişi olması gerekir.
3. Her modülün, bu girişi modül yönerge alanının başlangıcında bağlanması gerekir.
4. Her modülün, ThreadX ile etkileşim kurmak için kullanılan modüle özgü işlevleri içeren bir modül kitaplığına (***TXD. a***) bağlanması gerekir.

## <a name="module-sources"></a>Modül kaynakları

ThreadX modüllerinin, doğrudan modül kaynak kodu ile bağlanması ve konumlandırılabilir şekilde tasarlanan kendi kaynak dosyaları kümesi vardır. Bu dosyalar ayrı modülle ve yerleşik Modül Yöneticisi arasında köprü sağlar. Modül dosyaları aşağıdaki gibidir.

| Dosya Adı | İçindekiler |
|---|---|
| **txm_module. h** | Modül bilgilerini tanımlayan dosya ekleme. |
| **txm_module_port. h** | Bağlantı noktasına özgü modül bilgilerini tanımlayan dosya ekleme. |
| **txm_module_user. h** | Kullanıcının özelleştirebileceği değerleri tanımlar ve belirler. |
| **txm_module_initialize. s [1] [3]** | Başlangıç modülüne iç işlevleri çağırır. |
| **txm_module_preamble. \{ s/S/68\}** | Modül girişi derleme dosyası. Bu dosya, modüle özgü çeşitli öznitelikleri tanımlar ve modül uygulama kodu ile bağlantılıdır. |
| **txm_module_application_request. c [1]** | Modül uygulama isteği işlevi, yerleşik koda uygulamaya özgü bir istek gönderir. |
| **txm_module_callback_request_thread_entry. c &nbsp; [1]** | Modül tarafından istenen geri çağırmaları, zamanlayıcılar ve bildirim geri çağırmaları dahil olmak üzere işlemeden sorumlu modül geri çağırma iş parçacığı. |
| **txm_ *. c [1] [2]** | Standart ThreadX API hizmetleri, bu, çekirdek Dispatcher 'ı çağırır.
| **txm_module_object_allocate. c [1]** | Manager bellek havuzunda bulunan modül nesnelerine bellek ayırmak için modül işlevi. |
| **txm_module_object_deallocate. c [1]** | Manager bellek havuzunda bulunan modül nesneleri için belleği serbest bırakmak için modül işlevi. |
| **txm_module_object_pointer_get. c [1]** | Bir sistem nesnesine bir işaretçi almak için modül işlevi. |
| **txm_module_object_pointer_get_extended. c [1]** | Bir sistem nesnesine bir işaretçi almak için modül işlevi, ad uzunluğu güvenliği. |
| **txm_module_thread_shell_entry. c [1]** | Modül iş parçacığı giriş işlevi. |
| **txm_module_thread_system_suspend. c [1]** | Bir iş parçacığını askıya almak için modül işlevi. |

**[1]** **_TXD. a_** kitaplığında bulunuyor.

**[2]** bu dosyalar THREADX API dosyalarıyla aynı ada sahip ve **tx_** ön eki yerine **txm_** ön ekine sahip.

**[3]** **txm_module_initialize. s** dosyası yalnızca ARM araçlarını kullanan bağlantı noktaları içindir.

## <a name="module-preamble"></a>Modül girişi

Modül girişi, modülün özelliklerini ve kaynaklarını tanımlar. İlk iş parçacığı girişi işlevi ve iş parçacığıyla ilişkili ilk bellek alanı gibi bilgiler giriş bölümünde tanımlanmıştır. Bağlantı noktasına özgü giriş örnekleri [ek](appendix.md). Şekil 3 ' te, genel hedef için örnek bir ThreadX modülü girişi gösterilmektedir (* ile başlayan satırlar genellikle uygulama tarafından değiştirilen değerlerdir):

```c
    AREA Init, CODE, READONLY

    /* Define public symbols. */
    EXPORT __txm_module_preamble

    /* Define application-specific start/stop entry points for the module. */
    IMPORT demo_module_start

    /* Define common external refrences. */
    IMPORT _txm_module_thread_shell_entry
    IMPORT _txm_module_callback_request_thread_entry
    IMPORT |Image$$ER_RO$$Length|
    IMPORT |Image$$ER_RW$$Length|

__txm_module_preamble
    DCD     0x4D4F4455                                  ; Module ID
    DCD     0x6                                         ; Module Major Version
    DCD     0x1                                         ; Module Minor Version
    DCD     32                                          ; Module Preamble Size in 32-bit words
*   DCD     0x12345678                                  ; Module ID (application defined)
*   DCD     0x01000001                                  ; Module Properties where:
                                                        ; Bits 31-24: Compiler ID
                                                        ;   0 -> IAR
                                                        ;   1 -> ARM
                                                        ;   2 -> GNU
                                                        ;   Bits 23-1: Reserved
                                                        ;   Bit 0: 0 -> Privileged mode execution (no MMU protection)
                                                        ;          1 -> User mode execution (MMU protection)
    DCD     _txm_module_thread_shell_entry - . + .      ; Module Shell Entry Point
*   DCD     demo_module_start - . + .                   ; Module Start Thread Entry Point
    DCD     0                                           ; Module Stop Thread Entry Point
*   DCD     1                                           ; Module Start/Stop Thread Priority
*   DCD     2048                                        ; Module Start/Stop Thread Stack Size
    DCD     _txm_module_callback_request_thread_entry - . + . ; Module Callback Thread Entry
    DCD     1                                            ; Module Callback Thread Priority
    DCD     2048                                         ; Module Callback Thread Stack Size
    DCD     |Image$$ER_RO$$Length|                       ; Module Code Size
    DCD     |Image$$ER_RW$$Length|                       ; Module Data Size
    DCD     0                                            ; Reserved 0
    DCD     0                                            ; Reserved 1
    DCD     0                                            ; Reserved 2
    DCD     0                                            ; Reserved 3
    DCD     0                                            ; Reserved 4
    DCD     0                                            ; Reserved 5
    DCD     0                                            ; Reserved 6
    DCD     0                                            ; Reserved 7
    DCD     0                                            ; Reserved 8
    DCD     0                                            ; Reserved 9
    DCD     0                                            ; Reserved 10
    DCD     0                                            ; Reserved 11
    DCD     0                                            ; Reserved 12
    DCD     0                                            ; Reserved 13
    DCD     0                                            ; Reserved 14
    DCD     0                                            ; Reserved 15
    END
```

**Şekil 3**

Çoğu durumda, geliştiricinin yalnızca modülün başlangıç iş parçacığını (konum 0x1C), modül KIMLIĞINI (konum 0x10), başlatma/durdurma iş parçacığı önceliği ($ 24) ve başlatma/durdurma iş parçacığı yığın boyutunu (% $ $ $ $ $ $ $ $ $ $ $ $ $ $ $ $) Yukarıdaki Gösterim, modülün başlangıç iş parçacığının ***demo_module_start** _, modül kimliği _*_0x12345678_*_ ve başlangıç iş parçacığının önceliği _*_1_*_ ve _ *_2048_** bayt yığın boyutu olacak şekilde ayarlanır.

Bazı uygulamalar isteğe bağlı olarak, Modül Yöneticisi modülü durduğunda yürütülen bir durdurma iş parçacığını tanımlayabilir. Ayrıca, bazı uygulamalar aşağıdaki şekilde tanımlanan modül özellikleri alanını kullanabilir.

## <a name="module-properties-bit-map"></a>Modül özellikleri bit eşlemesi

Aşağıdaki tabloda, Özellikler bit eşlemesinin bir örneği gösterilmektedir. Bağlantı noktasına özgü özellikler bit eşlemleri [ek](appendix.md).

| Sürümleri | Değer | Anlamı |
|---|---|---|
| 0 | 0<br />1 | Ayrıcalıklı mod yürütme<br />Kullanıcı modu yürütme |
| 1 | 0<br />1 | MPU koruması yok<br />MPU koruması (Kullanıcı modunun seçili olması gerekir) |
| 2 | 0<br />1 | Paylaşılan/dış bellek erişimini devre dışı bırak<br />Paylaşılan/dış bellek erişimini etkinleştir |
| [23-3] | 0 | Ayrılmıştır
| [31-24] | <br />0x01<br />0x02<br />0x03 | **Derleyici KIMLIĞI**<br />IAR dili<br />ARM<br />GNU |


## <a name="module-linker-control-file"></a>Modül bağlayıcı denetim dosyası

Modül oluşturulurken modül girişi diğer kod bölümünden önce yerleştirilmelidir. Modül, konum bağımsız kod ve veri bölümleriyle oluşturulmalıdır. Bağlantı noktasına özgü örnek bağlayıcı dosyaları [ek](appendix.md).

## <a name="module-threadx-library"></a>Modül ThreadX kitaplığı

Her modülün özel, modül merkezli bir ThreadX kitaplığına bağlanması gerekir. Bu kitaplık, yerleşik koddaki ThreadX hizmetlerine erişim sağlar. Erişimin büyük bir çoğunluğu ***txm_ \* . c*** dosyaları aracılığıyla gerçekleştirilir. Aşağıda, ThreadX API işlevi **_tx_thread_relinquish_* _ ( _*_ \_ txm_thread_relinquish. c \* * * *) için modül erişim çağrısının bir örneği verilmiştir.

```c
(_txm_module_kernel_call_dispatcher)(TXM_THREAD_RELINQUISH_CALL, 0, 0, 0);
```

Bu örnekte, Modül Yöneticisi tarafından sağlanan işlev işaretçisi, ***tx_thread_relinquish*** HIZMETIYLE Ilişkili kimlikle Modül Yöneticisi dağıtım işlevini çağırmak için kullanılır. Bu hizmet hiçbir parametre alır.

## <a name="module-example"></a>Modül örneği

Aşağıda bir modül biçiminde standart ThreadX tanıtımı örneği verilmiştir. Standart ThreadX tanıtımı ve modül gösterimi arasındaki temel farklılıklar şunlardır.

1. ***Tx_api. h** _ ile _ *_txm_module. h_* arasında değişiklik*
2. **_Txm_module. h 'den_** önceki **#define TXM_MODULE** eklenmesi
3. ***Main** _ ve _ *tx_application_define** **_demo_module_start_** ile değiştirme
4. Nesneler yerine ThreadX nesnelerine *işaretçiler* bildirme.

```c
/* Specify that this is a module! */
#define TXM_MODULE

/* Include the ThreadX module header. */
#include "txm_module.h"

/* Define constants. */
#define DEMO_STACK_SIZE         1024
#define DEMO_BYTE_POOL_SIZE     9120
#define DEMO_BLOCK_POOL_SIZE    100
#define DEMO_QUEUE_SIZE         100

/* Define the pool space in the bss section of the module. ULONG is used to
   get word alignment. */
   
ULONG                   demo_module_pool_space[DEMO_BYTE_POOL_SIZE / 4];

/* Define the ThreadX object control block pointers. */

TX_THREAD               *thread_0;
TX_THREAD               *thread_1;
TX_THREAD               *thread_2;
TX_THREAD               *thread_3;
TX_THREAD               *thread_4;
TX_THREAD               *thread_5;
TX_THREAD               *thread_6;
TX_THREAD               *thread_7;
TX_QUEUE                *queue_0;
TX_SEMAPHORE            *semaphore_0;
TX_MUTEX                *mutex_0;
TX_EVENT_FLAGS_GROUP    *event_flags_0;
TX_BYTE_POOL            *byte_pool_0;
TX_BLOCK_POOL           *block_pool_0;


/* Define the counters used in the demo application. */
ULONG       thread_0_counter;
ULONG       thread_1_counter;
ULONG       thread_1_messages_sent;
ULONG       thread_2_counter;
ULONG       thread_2_messages_received;
ULONG       thread_3_counter;
ULONG       thread_4_counter;
ULONG       thread_5_counter;
ULONG       thread_6_counter;
ULONG       thread_7_counter;
ULONG       semaphore_0_puts;
ULONG       event_0_sets;
ULONG       queue_0_sends;

/* Define thread prototypes. */

void    thread_0_entry(ULONG thread_input);
void    thread_1_entry(ULONG thread_input);
void    thread_2_entry(ULONG thread_input);
void    thread_3_and_4_entry(ULONG thread_input);
void    thread_5_entry(ULONG thread_input);
void    thread_6_and_7_entry(ULONG thread_input);

/* Define notify functions. */

void semaphore_0_notify(TX_SEMAPHORE *semaphore_ptr)
{
    if (semaphore_ptr == semaphore_0)
        semaphore_0_puts++;
}


void event_0_notify(TX_EVENT_FLAGS_GROUP *event_flag_group_ptr)
{
    if (event_flag_group_ptr == event_flags_0)
        event_0_sets++;
}


void queue_0_notify(TX_QUEUE *queue_ptr)
{
    if (queue_ptr == queue_0)
        queue_0_sends++;
}

/* Define the module start function. */
void demo_module_start(ULONG id)
{
    CHAR *pointer;

    /* Allocate all the objects. In memory protection mode,
        modules cannot allocate control blocks within their
        own memory area so they cannot corrupt the resident
        portion of ThreadX by corrupting the control block(s). */
    txm_module_object_allocate(&thread_0, sizeof(TX_THREAD));
    txm_module_object_allocate(&thread_1, sizeof(TX_THREAD));
    txm_module_object_allocate(&thread_2, sizeof(TX_THREAD));
    txm_module_object_allocate(&thread_3, sizeof(TX_THREAD));
    txm_module_object_allocate(&thread_4, sizeof(TX_THREAD));
    txm_module_object_allocate(&thread_5, sizeof(TX_THREAD));
    txm_module_object_allocate(&thread_6, sizeof(TX_THREAD));
    txm_module_object_allocate(&thread_7, sizeof(TX_THREAD));
    txm_module_object_allocate(&queue_0, sizeof(TX_QUEUE));
    txm_module_object_allocate(&semaphore_0, sizeof(TX_SEMAPHORE));
    txm_module_object_allocate(&mutex_0, sizeof(TX_MUTEX));
    txm_module_object_allocate(&event_flags_0, sizeof(TX_EVENT_FLAGS_GROUP));
    txm_module_object_allocate(&byte_pool_0, sizeof(TX_BYTE_POOL));
    txm_module_object_allocate(&block_pool_0, sizeof(TX_BLOCK_POOL));

    /* Create a byte memory pool from which to allocate the thread stacks. */
    tx_byte_pool_create(byte_pool_0, "module byte pool 0",
        demo_module_pool_space, DEMO_BYTE_POOL_SIZE);

    /* Allocate the stack for thread 0. */
    tx_byte_allocate(byte_pool_0, (VOID **) &pointer,
        DEMO_STACK_SIZE, TX_NO_WAIT);

    /* Create thread 0. */
    tx_thread_create(thread_0, "module thread 0", thread_0_entry, 0,
        pointer, DEMO_STACK_SIZE,
        1, 1, TX_NO_TIME_SLICE, TX_AUTO_START);

    /* Allocate the stack for thread 1. */
    tx_byte_allocate(byte_pool_0, (VOID **) &pointer,
        DEMO_STACK_SIZE, TX_NO_WAIT);

    /* Create threads 1 and 2. These threads pass information through
        a ThreadX message queue. It is also interesting to note that
        these threads have a time slice. */
    tx_thread_create(thread_1, "module thread 1", thread_1_entry, 1,
        pointer, DEMO_STACK_SIZE,
        16, 16, 4, TX_AUTO_START);

    /* Allocate the stack and create thread 2. */
    tx_byte_allocate(byte_pool_0, (VOID **) &pointer,
        DEMO_STACK_SIZE, TX_NO_WAIT);
    tx_thread_create(thread_2, "module thread 2", thread_2_entry, 2,
        pointer, DEMO_STACK_SIZE,
        16, 16, 4, TX_AUTO_START);

    /* Allocate the stack for thread 3. */
    tx_byte_allocate(byte_pool_0, (VOID **) &pointer,
        DEMO_STACK_SIZE, TX_NO_WAIT);

    /* Create threads 3 and 4. These threads compete for a ThreadX
        counting semaphore. An interesting thing here is that both threads
        share the same instruction area. */
    tx_thread_create(thread_3, "module thread 3",
        thread_3_and_4_entry, 3,
        pointer, DEMO_STACK_SIZE,
        8, 8, TX_NO_TIME_SLICE, TX_AUTO_START);

    /* Allocate the stack and create thread 4. */
    tx_byte_allocate(byte_pool_0, (VOID **) &pointer,
        DEMO_STACK_SIZE, TX_NO_WAIT);
    tx_thread_create(thread_4, "module thread 4",
        thread_3_and_4_entry, 4,
        pointer, DEMO_STACK_SIZE,
        8, 8, TX_NO_TIME_SLICE, TX_AUTO_START);

    /* Allocate the stack for thread 5. */
    tx_byte_allocate(byte_pool_0, (VOID **) &pointer,
        DEMO_STACK_SIZE, TX_NO_WAIT);

    /* Create thread 5. This thread simply pends on an event flag which
        will be set by thread 0. */
    tx_thread_create(thread_5, "module thread 5", thread_5_entry, 5,
        pointer, DEMO_STACK_SIZE,
        4, 4, TX_NO_TIME_SLICE, TX_AUTO_START);

    /* Allocate the stack for thread 6. */
    tx_byte_allocate(byte_pool_0, (VOID **) &pointer,
        DEMO_STACK_SIZE, TX_NO_WAIT);

    /* Create threads 6 and 7. These threads compete for a ThreadX mutex. */
    tx_thread_create(thread_6, "module thread 6",
        thread_6_and_7_entry, 6,
        pointer, DEMO_STACK_SIZE,
        8, 8, TX_NO_TIME_SLICE, TX_AUTO_START);

    /* Allocate the stack and create thread 7. */
    tx_byte_allocate(byte_pool_0, (VOID **) &pointer,
        DEMO_STACK_SIZE, TX_NO_WAIT);
    tx_thread_create(thread_7, "module thread 7",
        thread_6_and_7_entry, 7,
        pointer, DEMO_STACK_SIZE,
        8, 8, TX_NO_TIME_SLICE, TX_AUTO_START);

    /* Allocate the message queue. */
    tx_byte_allocate(byte_pool_0, (VOID **) &pointer,
        DEMO_QUEUE_SIZE*sizeof(ULONG), TX_NO_WAIT);

    /* Create the message queue shared by threads 1 and 2. */
    tx_queue_create(queue_0, "module queue 0", TX_1_ULONG, pointer,
        DEMO_QUEUE_SIZE*sizeof(ULONG));

    /* Register queue send callback. */
    tx_queue_send_notify(queue_0, queue_0_notify);

    /* Create the semaphore used by threads 3 and 4. */
    tx_semaphore_create(semaphore_0, "module semaphore 0", 1);

    /* Register semaphore put callback. */
    tx_semaphore_put_notify(semaphore_0, semaphore_0_notify);

    /* Create the event flags group used by threads 1 and 5. */
    tx_event_flags_create(event_flags_0, "module event flags 0");

    /* Register event flag set callback. */
    tx_event_flags_set_notify(event_flags_0, event_0_notify);

    /* Create the mutex used by thread 6 and 7 without priority
        inheritance. */
    tx_mutex_create(mutex_0, "module mutex 0", TX_NO_INHERIT);

    /* Allocate the memory for a small block pool. */
    tx_byte_allocate(byte_pool_0, (VOID **) &pointer,
        DEMO_BLOCK_POOL_SIZE, TX_NO_WAIT);

    /* Create a block memory pool. */
    tx_block_pool_create(block_pool_0, "module block pool 0",
        sizeof(ULONG), pointer, DEMO_BLOCK_POOL_SIZE);

    /* Allocate a block. */
    tx_block_allocate(block_pool_0, (VOID **) &pointer,
        TX_NO_WAIT);

    /* Release the block back to the pool. */
    tx_block_release(pointer);

}

/* Define all the threads. */

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

        /* Set event flag 0 to wake up thread 5. */
        status = tx_event_flags_set(event_flags_0, 0x1, TX_OR);

        /* Check status. */
        if (status != TX_SUCCESS)
            break;
    }
}

void thread_1_entry(ULONG thread_input)
{
    UINT status;

    /* This thread simply sends messages to a queue shared by
       thread 2. */
    while(1)
    {
        /* Increment the thread counter. */
        thread_1_counter++;

        /* Send message to queue 0. */
        status = tx_queue_send(queue_0, &thread_1_messages_sent,
            TX_WAIT_FOREVER);

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
        status = tx_queue_receive(queue_0, &received_message, TX_WAIT_FOREVER);

        /* Check completion status and make sure the message is what
           we expected. */
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
        status = tx_semaphore_get(semaphore_0, TX_WAIT_FOREVER);

        /* Check status. */
        if (status != TX_SUCCESS)
            break;

        /* Sleep for 2 ticks to hold the semaphore. */
        tx_thread_sleep(2);

        /* Release the semaphore. */
        status = tx_semaphore_put(semaphore_0);

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
        status = tx_event_flags_get(event_flags_0, 0x1, TX_OR_CLEAR,
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
        status = tx_mutex_get(mutex_0, TX_WAIT_FOREVER);

        /* Check status. */
        if (status != TX_SUCCESS)
            break;

        /* Get the mutex again with suspension. This shows that an
           owning thread may retrieve the mutex it owns multiple times. */
        status = tx_mutex_get(mutex_0, TX_WAIT_FOREVER);

        /* Check status. */
        if (status != TX_SUCCESS)
            break;

        /* Sleep for 2 ticks to hold the mutex. */
        tx_thread_sleep(2);

        /* Release the mutex. */
        status = tx_mutex_put(mutex_0);

        /* Check status. */
        if (status != TX_SUCCESS)
            break;

        /* Release the mutex again. This will actually release ownership
           since it was obtained twice. */
        status = tx_mutex_put(mutex_0);

        /* Check status. */
        if (status != TX_SUCCESS)
            break;
    }
}
```

## <a name="building-modules"></a>Modüller oluşturma

Modül oluşturmak kullanılan araç zincirine bağımlıdır. Bkz. bağlantı noktasına özgü örnekler için [ek](appendix.md) . Tüm bağlantı noktalarına yapılan ortak etkinlikler şunlardır.

- Modül kitaplığı oluşturma
- Modül uygulaması oluşturma

Her modülün bir **txm_module_preamble** olması gerekir (özellikle modül için kurulum) ve modül kitaplığı (örneğin, **_TXI. a_**).
