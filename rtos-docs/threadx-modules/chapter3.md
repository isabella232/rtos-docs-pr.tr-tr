---
title: Bölüm 3-Modül Yöneticisi gereksinimleri
description: Bu makale, ThreadX modül yöneticisini oluşturmak için gereken adımların bir açıklamasıdır.
author: philmea
ms.author: philmea
ms.date: 07/15/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: e8ea1a05096b5975de203648fddfb19c1a6105e0
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826596"
---
# <a name="chapter-3---module-manager-requirements"></a>Bölüm 3-Modül Yöneticisi gereksinimleri

ThreadX Modül Yöneticisi, ThreadX RTOS ile birlikte uygulamanın yerleşik bölümünde bulunur. Modülün başlatılmasının yanı sıra ThreadX API hizmetleri için tüm modül isteklerini alan ve gönderen bir sorumludur.

> [!NOTE]
> ThreadX modül **Yöneticisi** kaynak dosyaları (C ve derleme), threadx kitaplığı projesine "**TX**" eklenmelidir.

ThreadX modül yöneticisini oluşturmak için aşağıdaki adımlar gereklidir (her adım aşağıda daha ayrıntılı olarak açıklanmıştır).

1. **TX_THREAD** denetim bloğu modül bilgilerini içerecek şekilde genişletilmelidir. Bunu yapmanın en kolay yolu, **_tx_port. h_*_ dosyasındaki*** **TX_THREAD_EXTENSION_2** tanımını **_txm_module_port. h_** içinde bulunan _ TX_THREAD_EXTENSION_2 değiştirecek şekilde kullanmaktır. Bkz. bağlantı noktasına özgü uzantılar için [ek](appendix.md) .

Örnek uzantı:

   ```c
   #define TX_THREAD_EXTENSION_2                     \
       VOID      tx_thread_module_instance_ptr;      \
       VOID      tx_thread_module_entry_info_ptr;    \
       ULONG     tx_thread_module_current_user_mode; \
       ULONG     tx_thread_module_user_mode;         \
       VOID     *tx_thread_module_kernel_stack_start;\
       VOID     *tx_thread_module_kernel_stack_end;  \
       ULONG     tx_thread_module_kernel_stack_size; \
       VOID     *tx_thread_module_stack_ptr;         \
       VOID     *tx_thread_module_stack_start;       \
       VOID     *tx_thread_module_stack_end;         \
       ULONG     tx_thread_module_stack_size;        \
       VOID     *tx_thread_module_reserved;
   ```

   Aşağıdaki uzantıların ***tx_port. h*** içinde tanımlanması gerekir.

   ```c
   #define TX_EVENT_FLAGS_GROUP_EXTENSION  VOID    *tx_event_flags_group_module_instance; \
        VOID   (*tx_event_flags_group_set_module_notify)(struct TX_EVENT_FLAGS_GROUP_STRUCT *group_ptr);

   #define TX_QUEUE_EXTENSION              VOID    *tx_queue_module_instance; \
        VOID   (*tx_queue_send_module_notify)(struct TX_QUEUE_STRUCT *queue_ptr);

   #define TX_SEMAPHORE_EXTENSION          VOID    *tx_semaphore_module_instance; \
        VOID   (*tx_semaphore_put_module_notify)(struct TX_SEMAPHORE_STRUCT *semaphore_ptr);

   #define TX_TIMER_EXTENSION              VOID    *tx_timer_module_instance; \
        VOID   (*tx_timer_module_expiration_function)(ULONG id);
   ```

2. Tüm ***txm_module_manager_ \**** C ve derleme dosyalarını threadx kitaplığı proje **_TX_** öğesine ekleyin.
3. Tüm kitaplıkları ve yürütülebilir projeleri yeniden derleyin. NetX Duo gerekliyse, tüm modül ve Modül Yöneticisi C kodu, **TXM_MODULE_ENABLE_NETX_DUO** tanımlanmış olarak oluşturulmalıdır.

## <a name="module-manager-sources"></a>Modül Yöneticisi Kaynakları

ThreadX Modül Yöneticisi, bağlantılı ve doğrudan yerleşik ThreadX kodu ile konumlandırılabilir şekilde tasarlanan bir kaynak dosyalar kümesine sahiptir. Bu dosyalar modülden bir modül ve alan izleyen ThreadX API istekleri başlatma yeteneği sağlar. Modül Yöneticisi dosyaları aşağıdaki gibidir.

| **Dosya adı** |  **İçerik** |
|-------------- | ------------- |
| ***txm_module. h*** | Modül bilgilerini tanımlayan dosyayı (modül kaynak koduna da dahil) içerir. |
| ***txm_module_manager_dispatch. h*** | Dağıtım Yardımcısı işlevlerini tanımlayan içerme dosyası.|
| ***txm_module_manager_util. h*** | İç yardımcı program Yardımcısı makrolarını & işlevleri tanımlayan dosya ekleme. |
| ***txm_module_port. h*** | Bağlantı noktasına özgü modül bilgilerini tanımlayan dosyayı (modül kaynak koduna da dahil olmak üzere) içerir. |
| ***tx_initialize_low_level. \[ s, S, 68 \]** _ | Var olan ThreadX kitaplık dosyasının yerini alır. Modül Yöneticisi ve bellek özel durumları için güncelleştirilmiş vektör tablosu ve ek vektör işleyicileri. _This dosya yalnızca Cortex-A7/ARM, Cortex-M7/ARM, Cortex-R4/ARM, Cortex-R4/IAR, MCF544xx/GHS, RX63/IAR, RX65N/IAR. *|
| ***tx_thread_context_restore. s** _ | Var olan ThreadX kitaplık dosyasının yerini alır. Kesme işleminden sonra iş parçacığı bağlamını geri yükleyin. _This dosya yalnızca Cortex-A7/ARM, Cortex-R4/ARM, Cortex-R4/IAR içinde. *|
| ***tx_thread_schedule. \[ s, S, 68\]*** | Var olan ThreadX kitaplık dosyasının yerini alır. Bu durumda bellek yönetimi kayıtlarını güncelleştirmek için kullanılan genişletilmiş Zamanlayıcı kodu. |
| ***tx_thread_stack_build. s** _ | Var olan ThreadX kitaplık dosyasının yerini alır. Bir iş parçacığının yığın çerçevesini oluşturur. _This dosya yalnızca Cortex-A7/ARM, Cortex-R4/ARM, Cortex-R4/IAR içinde. *|
| ***txm_module_manager_thread_stack_build. \[ s, S, 68\]*** | Tüm modül ilk yığınlarını oluşturur, konuma bağımsız veri erişimi için kurulum 'u içerir. |
| ***txm_module_manager_user_mode_entry. \[ s, S \]** _ | Modülün çekirdek moduna girmesine izin verir. _This dosya yalnızca Cortex-A7/ARM, Cortex-R4/ARM, Cortex-R4/IAR içinde. *|
| ***txm_module_manager_alignment_adjust. c*** | Bağlantı noktasına özgü hizalama gereksinimlerini işler.|
| ***txm_module_manager_application_request. c*** | Yerleşik koda uygulamaya özgü istekleri işler. |
| ***txm_module_manager_callback_request. c*** | Bir modüle geri çağırma isteği gönderir. |
| ***txm_module_manager_event_flags_notify_trampoline. c*** | Etkinlik bayraklarını, ThreadX 'den bildirim çağrısını ayarla olarak işler. |
| ***txm_module_manager_external_memory_enable. c*** | Modülün erişebileceği paylaşılan bellek alanı için bellek yönetimi tablosunda bir giriş oluşturur. |
| ***txm_module_manager_file_load. c*** | Modül bellek alanına bir ikili modül dosyası ayırır ve yükler ve yürütülmek üzere hazırlar. |
| ***txm_module_manager_in_place_load. c*** | Modül veri alanını ayırır ve sağlanan kod adresinden modül yürütmesi için hazırlar. |
| ***txm_module_manager_initialize. c*** | Modülleri yüklemek ve çalıştırmak için kullanılabilir modül belleği alanının belirtimi dahil olmak üzere modül yöneticisini başlatır. |
| ***txm_module_manager_initialize_mmu. c** _ | MMU 'i başlatın. Kullanıcılar, bu dosyayı bellek haritalarına göre düzenleyebilir. _This dosya yalnızca Cortex-A7/ARM * |
| ***txm_module_manager_mm_initialize. c** _ | MPU/MMU 'i başlatın. Kullanıcılar, bu dosyayı bellek haritalarına göre düzenleyebilir. _This dosya yalnızca Cortex-A7/ARM * |
| ***txm_module_manager_kernel_dispatch. c*** | İstek KIMLIĞINE göre modül API 'SI isteklerini işler. |
| ***txm_module_manager_maximum_module_priority_set. c*** | Bir modülde izin verilen en fazla iş parçacığı önceliğini ayarlar. |
| ***txm_module_manager_memory_fault_handler. c*** | Yürütülen modülde algılanan bellek hatalarını işler. |
| ***txm_module_manager_memory_fault_notify. c*** | Bir bellek hatası oluştuğunda uygulama bildirimi geri aramasını kaydeder. |
| ***txm_module_manager_memory_load. c*** | Modülün kodunu ve verilerini ayırır ve yükler ve modülü yürütülmek üzere hazırlar. |
| ***txm_module_manager_mm_register_setup. c*** | Modül için kod ve verilerin yüklendiği yere bağlı olarak, modül için MPU/MMU yazmaçlarını ayarlar. |
| ***txm_module_manager_object_allocate. c*** | Bir modül nesnesi için belleği ayırır. |
| ***txm_module_manager_object_deallocate. c*** | Modül nesnesi için belleği ayırır. |
| ***txm_module_manager_object_pointer_get. c*** | Sağlanan nesne türünü ve adını arar ve bulunursa, nesne işaretçisini döndürür. |
| ***txm_module_manager_object_pointer_get_extended. c*** | Sağlanan nesne türünü ve adını arar ve bulunursa, nesne işaretçisini döndürür. Güvenlik için ad uzunluğu belirtildi. |
| ***txm_module_manager_object_pool_create. c***  | Modül uygulamalarının ayırabilecek modül veri alanı dışında bir nesne havuzu oluşturur. |
| ***txm_module_manager_properties_get. c*** | Belirtilen modülün özelliklerini alır. |
| ***txm_module_manager_queue_notify_trampoline. c*** | ThreadX 'den kuyruk bildirim çağrısını işler. |
| ***txm_module_manager_semaphore_notify_trampoline. c*** | ThreadX 'ten semafor put bildirim çağrısını işler.|
| ***txm_module_manager_start. c*** | Bir modülün yürütülmesini başlatır. |
| ***txm_module_manager_stop. c*** | Modülün yürütülmesini durduruyor. |
| ***txm_module_manager_thread_create. c*** | Tüm modül iş parçacıklarını oluşturur. |
| ***txm_module_manager_thread_notify_trampoline. c*** | ThreadX iş parçacığı giriş/çıkış bildirimi çağrısını işler. |
| ***txm_module_manager_thread_reset. c*** | Modül iş parçacığını sıfırlayın. |
| ***txm_module_manager_timer_notify_trampoline. c*** | ThreadX 'den süreölçer süre sonlarını işler. |
| ***txm_module_manager_unload. c*** | Modülü modül bellek alanından kaldırır. |
| ***txm_module_manager_util. c*** | Yöneticinin iç yardımcı işlevleri. |

## <a name="module-manager-initialization"></a>Modül Yöneticisi başlatma

Uygulamanın yerleşik bölümü, ***Txm_module_manager_initialize*** Modül Yöneticisi başlatma işlevinin çağrılmasından sorumludur. Bu işlev, modül belleği ayırmak için kullanılan bellek alanını ayarlama da dahil olmak üzere modülleri yükleme ve kaldırma için iç yapıları ayarlar.

## <a name="module-manager-loading"></a>Modül Yöneticisi yükleniyor

Modül Yöneticisi, ikili modül dosyalarından veya yerleşik kod alanında zaten mevcut olan bir modül kodu bölümünden modül belleğine dinamik olarak modül yükleyebilir. Ayrıca, Modül Yöneticisi kodu yerinde yürütebilir, diğer bir deyişle modül belleğinde yalnızca modül verileri ayrılır ve kod yürütme yerinde yapılır. Aşağıdaki Modül Yöneticisi yük API işlevleri kullanılabilir.

* ***txm_module_manager_file_load***

* ***txm_module_manager_in_place_load***

* ***txm_module_manager_memory_load***

Modül yöneticisinin bellek korumalı sürümü aynı zamanda modülün uygun hizalamayla yüklendiğinden ve bellek yönetimi saklayıcıları her modül için doğru şekilde kurulduğundan emin olur. Bellek koruması modül girişi seçenekleri aracılığıyla etkinleştirildiğinde modül belleği erişimi modül kodu ve veri alanlarıyla kısıtlıdır.

## <a name="module-manager-starting"></a>Modül Yöneticisi başlatılıyor

Modül Yöneticisi, ***txm_module_manager_start*** API işlevi aracılığıyla önceden yüklenmiş bir modülün yürütülmesini başlatır. Modül yürütmeyi başlatmak için, bu işlev modül girişi içinde belirtilen başlangıç konumunda modülü giren bir iş parçacığı oluşturur. Bu iş parçacığının öncelik ve yığın boyutu Ayrıca modül girişi içinde de belirtilir.

## <a name="module-manager-stopping"></a>Modül Yöneticisi durduruluyor

Modül Yöneticisi, ***txm_module_manager_stop*** işlevi aracılığıyla daha önce yüklenmiş ve yürütülen bir modülün yürütülmesini sonlandırır. Bu API işlevi ilk olarak sonlanır ve başlangıç iş parçacığını siler. Modül girişi bir durdurma iş parçacığını belirtiyorsa, bu iş parçacığı oluşturulup yürütülür. Modül Yöneticisi durdurma iş parçacığının tamamlaması için sabit bir süre bekler. Tamamlandıktan sonra, modül tarafından oluşturulan tüm sistem kaynakları silinir ve modül, yeniden başlatılabilir veya bellekten kaldırılabileceği bir etkin durumdan konur.

## <a name="module-manager-unloading"></a>Modül yöneticisini kaldırma

Modül Yöneticisi, daha önce yüklenmiş ancak ***txm_module_manager_unload*** işlevi aracılığıyla bir modül yürütmez modülünü kaldırır. Bu API, modülle ilişkili tüm belleği yayınlar ve gelecekte başka bir modülle kullanılmak üzere serbest bırakır.

## <a name="module-manager-requests"></a>Modül Yöneticisi istekleri

Modül Yöneticisi 'ne modüller tarafından yapılan istekler, Modül Yöneticisi tarafından modüle sağlanan bir işlev işaretçisi aracılığıyla Modül Yöneticisi gönderme işlevini çağıran ***txm_module. h*** içindeki makrolar aracılığıyla yapılır.

***Txm_module_application_request*** çağıran modül aracılığıyla yapılan uygulamaya özgü ek hizmetler, THREADX API 'si için kullanılan aynı makro mekanizması tarafından işlenir. Varsayılan olarak, modül yöneticisindeki bu işleme işlevi boştur ve uygulamanın uygulamaya özgü istekleri işlemek için gerekli kodu eklemesi için tasarlanmıştır.

İstek Modül Yöneticisi tarafından uygulanmadığından, Modül Yöneticisi tarafından **TX_NOT_AVAILABLE** hata durumu değeri döndürülür. Modül erişimi kapsamı dışında bir işlem isterse, bu hata kodu da döndürülür. Örneğin, bir modülün, Zamanlayıcı denetim bloğu veya geri çağırma adresiyle modülün kod alanı dışında bir Zamanlayıcı oluşturmasına izin verilmez.

## <a name="module-manager-example"></a>Modül Yöneticisi örneği

Aşağıda, Bölüm 2 ' de daha önce tanımlanan örnek modülünü Başlatan modül yöneticisi kodunun bir örneği verilmiştir. Modülün zaten yüklü olduğu varsayılır, bu da hata ayıklayıcının, 0x00800000 ROM adresidir.

```c
#include "tx_api.h"
#include "txm_module.h"

#define DEMO_STACK_SIZE 1024

/* Define the ThreadX object control blocks. */
TX_THREAD   module_manager;

/* Define thread prototype. */
void        module_manager_entry(ULONG thread_input);

/* Define the module object pool area. */
UCHAR       object_memory[8192];

/* Define the module data pool area. */
#define MODULE_DATA_SIZE 65536
UCHAR       module_data_area[MODULE_DATA_SIZE];

/* Define module instances. */
TXM_MODULE_INSTANCE     my_module1;
TXM_MODULE_INSTANCE     my_module2;

/* Define the count of memory faults. */
ULONG memory_faults;

/* Define fault handler. */
VOID module_fault_handler(TX_THREAD *thread, TXM_MODULE_INSTANCE *module)
{
    /* Just increment the fault counter. */
    memory_faults++;
}

/* Define main entry point. */
int main()
{
    /* Enter the ThreadX kernel. */
    tx_kernel_enter();
}

/* Define what the initial system looks like. */
void tx_application_define(void *first_unused_memory)
{
    /* Create the module manager thread. */
    tx_thread_create(&module_manager, "Module Manager Thread", module_manager_entry, 0,
                    first_unused_memory, DEMO_STACK_SIZE,
                    1, 1, TX_NO_TIME_SLICE, TX_AUTO_START);
}

/* Define the test threads. */
void module_manager_entry(ULONG thread_input)
{
    /* Initialize the module manager. */
    txm_module_manager_initialize((VOID *) module_data_area, MODULE_DATA_SIZE);

    /* Create a pool for module objects. */
    txm_module_manager_object_pool_create(object_memory, sizeof(object_memory));

    /* Register a fault handler. */
    txm_module_manager_memory_fault_notify(module_fault_handler);

    /* Load the module that is already there,
        in this example it is placed at 0x00800000. */
    txm_module_manager_in_place_load(&my_module1, "my module1", (VOID *) 0x00800000);

    /* Load a second instance of the module. */
    txm_module_manager_in_place_load(&my_module2, "my module2", (VOID *) 0x00800000);

    /* Enable shared memory region for module2. */
    txm_module_manager_external_memory_enable(&my_module2, (void*)0x20600000, 0x010000, 0x3F);

    /* Start the modules. */
    txm_module_manager_start(&my_module1);
    txm_module_manager_start(&my_module2);

    /* Sleep for a while and let the modules run... */
    tx_thread_sleep(300);

    /* Stop the modules. */
    txm_module_manager_stop(&my_module1);
    txm_module_manager_stop(&my_module2);

    /* Unload the modules. */
    txm_module_manager_unload(&my_module1);
    txm_module_manager_unload(&my_module2);

    /* Reload the modules. */
    txm_module_manager_in_place_load(&my_module2, "my module2", (VOID *) 0x00800000);
    txm_module_manager_in_place_load(&my_module1, "my module1", (VOID *) 0x00800000);

    /* Give both modules shared memory. */
    txm_module_manager_external_memory_enable(&my_module2, (void*)0x20600000, 0x010000, 0x3F);
    txm_module_manager_external_memory_enable(&my_module1, (void*)0x20600000, 0x010000, 0x3F);

    /* Set maximum module1 priority to 5. */
    txm_module_manager_maximum_module_priority_set(&my_module1, 5);

    /* Start the modules again. */
    txm_module_manager_start(&my_module2);
    txm_module_manager_start(&my_module1);

    /* Now just spin... */
    while(1)
    {
        tx_thread_sleep(100);

        /* Threads 0 and 5 in module1 are not created because they violate the maximum priority. */
    }
}
```

## <a name="module-manager-building"></a>Modül Yöneticisi oluşturma

***Txm_module_manager_ \**** kaynak dosyaları threadx kitaplığına eklenmelidir.

Bir ThreadX Modül Yöneticisi uygulaması, bir veya daha fazla uygulama dosyası olan ThreadX Kitaplığı ***TX. a*** ile birlikte bağlantılı bir standart threadx uygulamasıyla aynı şekilde aynıdır. Modül Yöneticisi uygulaması derleme, kullanılan araç zincirine bağımlıdır. Bkz. bağlantı noktasına özgü örnekler için [ek](appendix.md) .
