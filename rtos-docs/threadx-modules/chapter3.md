---
title: Bölüm 3 - Modül Yöneticisi gereksinimleri
description: Bu makale, ThreadX Modül Yöneticisi'ni inşa için gereken adımların bir açıklamasıdır.
author: philmea
ms.author: philmea
ms.date: 07/15/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 6c4d0993284c8e0b8264020d721ac12bdfe8117df4480fb54ee4d5b20a1f677e
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116799192"
---
# <a name="chapter-3---module-manager-requirements"></a>Bölüm 3 - Modül Yöneticisi gereksinimleri

ThreadX Modül Yöneticisi, ThreadX RTOS ile birlikte uygulamanın yerleşik bölümünde bulunur. Modülü başlatmanın yanı sıra ThreadX API hizmetleri için tüm modül isteklerinin sahasını oluşturmak ve gönderme sorumluluğundadır.

> [!NOTE]
> ThreadX Modül **Yöneticisi kaynak** dosyaları (C ve derleme) ThreadX kitaplık projesi " tx "**eklenmiştir.**

ThreadX Modül Yöneticisi'ni derlerken aşağıdaki adımlar gereklidir (her adım aşağıda daha ayrıntılı olarak açıklanmıştır).

1. Denetim **TX_THREAD** modül bilgilerini içerecek şekilde genişletiliyor olması gerekir. Bunu yapmanın en kolay yolu, tx_port.h _ **dosyasındaki** **_TX_THREAD_EXTENSION_2 tanımını txm_module_port.h_** dosyasında bulunan _ TX_THREAD_EXTENSION_2 **_ile değiştirmektir._** Bağlantı [noktasına özgü](appendix.md) uzantılar için eke bakın.

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

   aşağıdaki uzantılar ***tx_port.h içinde tanımlanmalıdır.***

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

2. C ve ***txm_module_manager_ \**** tüm dosyaları ThreadX kitaplık projesi **_tx'e ekleyin._**
3. Tüm kitaplıkları ve yürütülebilir projeleri yeniden oluşturma. NetX Duo gerekli ise, tüm Module ve Module Manager C kodu tanımlanmış **bir** TXM_MODULE_ENABLE_NETX_DUO gerekir.

## <a name="module-manager-sources"></a>Modül Yöneticisi kaynakları

ThreadX Modül Yöneticisi, bağlantılı olacak ve yerleşik ThreadX koduyla doğrudan birlikte olacak şekilde tasarlanmış bir kaynak dosya kümesine sahip. Bu dosyalar, modülden sonraki ThreadX API isteklerini bir modül başlatma ve alan özelliği sağlar. Modül yöneticisi dosyaları aşağıdaki gibidir.

| **Dosya Adı** |  **İçerik** |
|-------------- | ------------- |
| ***txm_module.h*** | Modül bilgilerini tanımlayan dosyayı dahil edin (modül kaynak koduna da dahildir). |
| ***txm_module_manager_dispatch.h*** | Gönderme yardımcı işlevlerini tanımlayan dosyayı dahil edin.|
| ***txm_module_manager_util.h*** | İşlevler için dahili yardımcı makroları tanımlayan & dahil edin. |
| ***txm_module_port.h*** | Bağlantı noktasına özgü modül bilgilerini tanımlayan dosyayı dahil edin (modül kaynak koduna da dahildir). |
| ***tx_initialize_low_level. \[ s,S,68 \]** _ | Mevcut ThreadX kitaplık dosyasını değiştirir. Modül yöneticisi ve bellek özel durumları için vektör tablosu ve ek vektör işleyicileri güncelleştirildi. _This dosyası yalnızca Cortex-A7/ARM, Cortex-M7/ARM, Cortex-R4/ARM, Cortex-R4/IAR, MCF544xx/GHS, RX63/IAR, RX65N/IAR içindedir.*|
| ***tx_thread_context_restore.s** _ | Mevcut ThreadX kitaplık dosyasını değiştirir. Kesme işlemeden sonra iş parçacığı bağlamını geri yükleme. _This dosyası yalnızca Cortex-A7/ARM, Cortex-R4/ARM, Cortex-R4/IAR içindedir.*|
| ***tx_thread_schedule. \[ s,S,68\]*** | Mevcut ThreadX kitaplık dosyasını değiştirir. Bu durumda bellek yönetimi kayıtlarını güncelleştirmek için kullanılan genişletilmiş zamanlayıcı kodu. |
| ***tx_thread_stack_build.s** _ | Mevcut ThreadX kitaplık dosyasını değiştirir. Bir iş parçacığının yığın çerçevesini derleme. _This dosyası yalnızca Cortex-A7/ARM, Cortex-R4/ARM, Cortex-R4/IAR içindedir.*|
| ***txm_module_manager_thread_stack_build. \[ s,S,68\]*** | Tüm modül ilk yığınlarını derlemek, konumdan bağımsız veri erişimi için kurulum içerir. |
| ***txm_module_manager_user_mode_entry. \[ s,S \]** _ | Modülün çekirdek moduna girmelerini sağlar. _This dosyası yalnızca Cortex-A7/ARM, Cortex-R4/ARM, Cortex-R4/IAR içindedir.*|
| ***txm_module_manager_alignment_adjust.c*** | Bağlantı noktasına özgü hizalama gereksinimlerini işleme.|
| ***txm_module_manager_application_request.c*** | Yerleşik koda yönelik uygulamaya özgü istekleri işleme. |
| ***txm_module_manager_callback_request.c*** | Bir modüle geri çağırma isteği gönderir. |
| ***txm_module_manager_event_flags_notify_trampoline.c*** | ThreadX'den olay bayrakları ayarlanmış bildirim çağrısını işleme. |
| ***txm_module_manager_external_memory_enable.c*** | Modülün erişebilirsiniz paylaşılan bir bellek alanı için bellek yönetim tablosunda bir giriş oluşturur. |
| ***txm_module_manager_file_load.c*** | Bir ikili modül dosyasını ayırarak modül bellek alanına yükler ve yürütme için hazırlar. |
| ***txm_module_manager_in_place_load.c*** | Modül veri alanı ayırır ve sağlanan kod adreslerinden modül yürütmeye hazırlar. |
| ***txm_module_manager_initialize.c*** | Modül yükleme ve çalıştırma için kullanılabilen modül bellek alanı belirtimi de dahil olmak üzere Modül Yöneticisi'ni başlatılır. |
| ***txm_module_manager_initialize_mmu.c** _ | MMU'su başlatma. Kullanıcılar bu dosyayı bellek eşlemelerine göre düzenleyebilir. _This dosyası yalnızca Cortex-A7/ARM'de* |
| ***txm_module_manager_mm_initialize.c** _ | MPU/MMU'su başlat. Kullanıcılar bu dosyayı bellek eşlemelerine göre düzenleyebilir. _This dosyası yalnızca Cortex-A7/ARM'de* |
| ***txm_module_manager_kernel_dispatch.c*** | İstek kimliğine bağlı olarak modül API isteklerini işleme. |
| ***txm_module_manager_maximum_module_priority_set.c*** | Bir modülde izin verilen en yüksek iş parçacığı önceliğini ayarlar. |
| ***txm_module_manager_memory_fault_handler.c*** | Yürütme modülünde algılanan bellek hatalarını işleme. |
| ***txm_module_manager_memory_fault_notify.c*** | Bellek hatası oluştuğunda bir uygulama bildirimi geri aramasını kaydeden. |
| ***txm_module_manager_memory_load.c*** | Modülün kodunu ve verilerini ayırarak yükler ve modülü yürütmeye hazırlar. |
| ***txm_module_manager_mm_register_setup.c*** | Kodun ve verilerin yükleniyor olduğu yere göre modül için MPU/MMU yazmacalarını ayarlar. |
| ***txm_module_manager_object_allocate.c*** | Modül nesnesi için bellek ayırır. |
| ***txm_module_manager_object_deallocate.c*** | Bir modül nesnesi için belleğin taşınmasını sağlar. |
| ***txm_module_manager_object_pointer_get.c*** | Sağlanan nesne türünü ve adını arar ve bulunursa nesne işaretçisini döndürür. |
| ***txm_module_manager_object_pointer_get_extended.c*** | Sağlanan nesne türünü ve adını arar ve bulunursa nesne işaretçisini döndürür. Güvenlik için belirtilen ad uzunluğu. |
| ***txm_module_manager_object_pool_create.c***  | Modülün veri alanı dışında modül uygulamalarının ayıra bir nesne havuzu oluşturur. |
| ***txm_module_manager_properties_get.c*** | Belirtilen modülün özelliklerini alır. |
| ***txm_module_manager_queue_notify_trampoline.c*** | ThreadX'den gelen kuyruk bildirim çağrısını işleme. |
| ***txm_module_manager_semaphore_notify_trampoline.c*** | ThreadX'den semafor koy bildirim çağrısını işleme.|
| ***txm_module_manager_start.c*** | Bir modülün yürütülmesini başlatır. |
| ***txm_module_manager_stop.c*** | Modülün yürütülmesini durdurur. |
| ***txm_module_manager_thread_create.c*** | Tüm modül iş parçacıklarını oluşturur. |
| ***txm_module_manager_thread_notify_trampoline.c*** | ThreadX'den iş parçacığı giriş/çıkış bildirim çağrısını işleme. |
| ***txm_module_manager_thread_reset.c*** | Modül iş parçacığını sıfırlama. |
| ***txm_module_manager_timer_notify_trampoline.c*** | ThreadX'den zamanlayıcı süre sonu işlemlerini işleme. |
| ***txm_module_manager_unload.c*** | Modülü modül bellek alanından kaldırıyor. |
| ***txm_module_manager_util.c*** | Yönetici için iç yardımcı işlevleri. |

## <a name="module-manager-initialization"></a>Modül Yöneticisi başlatma

Uygulamanın yerleşik bölümü, modül yöneticisi başlatma işlevinin çağrısından ***txm_module_manager_initialize.*** Bu işlev, modül belleğini ayrı ayrı bulunduracak bellek alanı ayarlama da dahil olmak üzere modülleri yükleme ve kaldırma için iç yapıları ayarlar.

## <a name="module-manager-loading"></a>Modül Yöneticisi yüklemesi

Modül Yöneticisi, ikili modül dosyalarından veya yerleşik kod alanında zaten mevcut olan bir modül kodu bölümünden modülleri modül belleğine dinamik olarak yük bindirebilirsiniz. Buna ek olarak, modül yöneticisi yerinde kod yürütebilirsiniz, yani modül belleğinde yalnızca modül verileri ayrılır ve kod yürütmesi yerinde yapılır. Aşağıdaki Modül Yöneticisi yükleme API'si işlevleri kullanılabilir.

* ***txm_module_manager_file_load***

* ***txm_module_manager_in_place_load***

* ***txm_module_manager_memory_load***

Modül Yöneticisi'nin bellek korumalı sürümü ayrıca modülün düzgün hizalamayla yüklendiğinden ve bellek yönetimi yazmaylarının her modül için düzgün şekilde ayarlanmalarını sağlar. Modül ön ek seçenekleri aracılığıyla bellek koruması etkinleştirildiğinde, modül belleği erişimi modül kodu ve veri alanlarıyla kısıtlanır.

## <a name="module-manager-starting"></a>Modül Yöneticisi başlatiliyor

Modül Yöneticisi, daha önce yüklenmiş bir modülün yürütülmesini api işlevi ***txm_module_manager_start*** başlatılır. Bu işlev, modül yürütmeyi başlatmak için modülü modül ön sırasında belirtilen başlangıç konuma giren bir iş parçacığı oluşturur. Bu iş parçacığının öncelik ve yığın boyutu da modül önamble içinde belirtilir.

## <a name="module-manager-stopping"></a>Modül Yöneticisi durduruluyor

Modül Yöneticisi, daha önce yüklenmiş ve yürütülen bir modülün yürütülmesini txm_module_manager_stop ***sonlandırılır.*** Bu API işlevi ilk olarak başlangıç iş parçacığını sonlandırılır ve siler. Modül ön ekli bir durdurma iş parçacığı belirtirse, bu iş parçacığı oluşturulur ve yürütülür. Modül Yöneticisi, durdurma iş parçacığının tamamlanması için sabit bir süre bekler. Tamamlandıktan sonra, modül tarafından oluşturulan tüm sistem kaynakları silinir ve modül, yeniden başlatılacak veya kaldırılacak şekilde uyku durumuna yerleştirilir.

## <a name="module-manager-unloading"></a>Modül Yöneticisi'ni kaldırma

Modül Yöneticisi, daha önce yüklenmiş olan ancak modülünü txm_module_manager_unload ***yürütmez.*** Bu API, modülle ilişkili tüm belleği serbest bırakarak gelecekte başka bir modülle birlikte kullanmak üzere serbest bıraktır.

## <a name="module-manager-requests"></a>Modül Yöneticisi istekleri

Modül Yöneticisi'ne modüller tarafından yapılan istekler, modüle Modül Yöneticisi tarafından sağlanan bir işlev işaretçisi aracılığıyla Module Manager dispatch işlevini çağıran tüm ThreadX çağrılarını eşleten ***txm_module.h'de*** makrolar aracılığıyla yapılır.

İş parçacığını çağıran modül  aracılığıyla txm_module_application_request uygulamaya özgü ek hizmetler, ThreadX API'si için kullanılan makro mekanizması tarafından kullanılmaktadır. Varsayılan olarak, Module Manager'daki bu işleme işlevi boştur ve uygulamanın uygulamaya özgü istekleri işlemesi için gerekli kodu ekleyen şekilde tasarlanmıştır.

İstek Modül Yöneticisi tarafından uygulanmazsa, Modül Yöneticisi **TX_NOT_AVAILABLE** hata durumu değeri döndürülür. Modül, modülün erişiminin kapsamı dışında bir işlem isteğinde bulunursa da bu hata kodu döndürülür. Örneğin, modülün, modülün kod alanı dışında zamanlayıcı denetim bloğu veya geri çağırma adresiyle zamanlayıcı oluşturmasına izin verilmez.

## <a name="module-manager-example"></a>Modül Yöneticisi örneği

Aşağıda, daha önce Bölüm 2'de tanımlanan örnek modülü başlatan bir Modül Yöneticisi kodu örneği yer almaktadır. Modülün büyük ihtimalle hata ayıklayıcısı tarafından ROM adresine yüklenmiş olduğu varsayılır 0x00800000.

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

## <a name="module-manager-building"></a>Modül Yöneticisi bina

İş ***txm_module_manager_ \**** dosyaları ThreadX kitaplığına eklenmiştir.

ThreadX Module Manager uygulaması, ***tx.a*** ThreadX kitaplığıyla bağlantılı bir veya daha fazla uygulama dosyası olan standart ThreadX uygulamasıyla etkili bir şekilde aynıdır. Modül yöneticisi uygulaması, kullanılan araç zincirine bağlıdır. Bağlantı [noktasına özgü](appendix.md) örnekler için eke bakın.
