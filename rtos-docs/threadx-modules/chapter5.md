---
title: Bölüm 5-Modül Yöneticisi API 'Leri
author: philmea
description: Bu makale, uygulamanın yerleşik bölümünün kullanabildiği Modül Yöneticisi API 'lerinin bir özetidir.
ms.author: philmea
ms.date: 07/15/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: ca0fee443c23fd1bdd34651f4a7b31cf71f886f0
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825486"
---
# <a name="chapter-5---module-manager-apis"></a>Bölüm 5-Modül Yöneticisi API 'Leri

## <a name="summary-of-module-manager-apis"></a>Modül Yöneticisi API 'Lerinin Özeti

Uygulamanın yerleşik bölümü için aşağıdaki gibi çeşitli ek API 'Ler mevcuttur.

- ***txm_module_manager_external_memory_enable** _-_Enable modül erişimi paylaşılan bir bellek alanına erişebilir *
- *Fılex * ile dosya **txm_module_manager_file_load** _-_Load modülü
- ***txm_module_manager_in_place_load** _-_Load modül verileri, yerinde yürütme *
- ***txm_module_manager_initialize** _-_Initialize Modül Yöneticisi *
- ***txm_module_manager_mm_initialize** _-bellek yönetimi donanımı _Initialize *
- ***txm_module_manager_maximum_module_priority_set** _-bir modülde izin verilen en fazla iş parçacığı önceliği _Set.
- ***txm_module_manager_memory_fault_notify** _-bellek hatasında bir uygulama geri çağırması _Register
- ***txm_module_manager_memory_load** _-modülü bellekten _Load *
- ***txm_module_manager_object_pool_create** _-modüller için bir nesne havuzu _Create
- ***txm_module_manager_properties_get** _-_Get modül özellikleri *
- ***txm_module_manager_start** _-belirtilen modülün _Start yürütmesi *
- ***txm_module_manager_stop** _-belirtilen modülün _Stop yürütmesi *
- ***txm_module_manager_unload** _-modülü _Unload *

---

## <a name="txm_module_manager_external_memory_enable"></a>txm_module_manager_external_memory_enable

Modülü paylaşılan bir bellek alanına erişmek için etkinleştirin.

### <a name="prototype"></a>Prototype

```c
UINT txm_module_manager_external_memory_enable(
     TXM_MODULE_INSTANCE *module_instance,
     VOID *start_address,
     ULONG length,
     UINT attributes);
```

### <a name="description"></a>Açıklama

Bu hizmet, modülün erişebileceği paylaşılan bellek bölgesi için bellek yönetimi donanım tablosunda bir giriş oluşturur.

### <a name="input-parameters"></a>Giriş parametreleri

- **module_instance** Modülün örneğine yönelik işaretçi.
- **start_address** Paylaşılan bellek bölgesinin başlangıç adresi.
- **uzunluk** Paylaşılan bellek bölgesinin uzunluğu.
- **öznitelikler** Bellek bölgesinin öznitelikleri (önbellek, okuma, yazma, vb.). Öznitelikler, bağlantı noktasına özeldir; bkz. öznitelik biçimi için [ek](appendix.md) .

### <a name="return-values"></a>Dönüş değerleri

- **TX_SUCCESS** (0x00) bellek girdisi başarıyla oluşturuldu.
- **TX_NOT_AVAILABLE** (0x1d) Manager başlatılmadı veya özellik kullanılamıyor.
- **TX_PTR_ERROR** (0x03) geçersiz modül örneği.
- **TX_START_ERROR** (0x10) modül yüklü durumda değil.
- **TXM_MODULE_ALIGNMENT_ERROR** (0xf0) geçersiz başlangıç adresi hizalaması.
- **TXM_MODULE_INVALID_PROPERTIES** (0xF3) uyumsuz Özellikler.

### <a name="allowed-from"></a>İzin verilen

Başlatma ve iş parçacıkları

### <a name="example"></a>Örnek

```c
TXM_MODULE_INSTANCE my_module;

/* Initialize the module manager with 64KB of RAM starting at address 0x64010000. */
txm_module_manager_initialize((VOID *) 0x64010000, 0x10000);

/* Load the module that has its code area at address 0x080F0000. */
txm_module_manager_in_place_load(&my_module, "my module", (VOID *) 0x080F0000);

/* Create a shared memory space 256 bytes long at address 0x64005000
   with read & write, no execute, outer & inner write back cache
   attributes. Note that these attributes are port-specific. */
txm_module_manager_external_memory_enable(&my_module, (VOID*)0x64005000, 256, 0x3F);
```

---

## <a name="txm_module_manager_file_load"></a>txm_module_manager_file_load

Modülü FileX aracılığıyla dosyadan yükleyin.

### <a name="prototype"></a>Prototype

```c
UINT txm_module_manager_file_load(
    TXM_MODULE_INSTANCE *module_instance,
    CHAR *module_name,
    FX_MEDIA *media_ptr,
    CHAR *file_name);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen dosyada bulunan modülün ikili görüntüsünü modül bellek alanına yükler ve yürütülmek üzere hazırlar. Belirtilen medyanın zaten açık olduğu varsayılır.

> [!NOTE]
> Dosyayı yüklemek için FileX sistemi kullanılır. FileX erişimini etkinleştirmek için modül, modül kitaplığı, Modül Yöneticisi ve ThreadX kitaplığı (Modül Yöneticisi kaynaklarıyla birlikte), projelerde tanımlanmış **FX_FILEX_PRESENT** oluşturulmalıdır.

### <a name="input-parameters"></a>Giriş parametreleri

- **module_instance** Modülün örneğine yönelik işaretçi.
- **module_name** Modülün adı.
- **media_ptr** Zaten açılmış FileX medyası işaretçisi.
- **file_name** Modülün ikili dosyasının adı.

### <a name="return-values"></a>Dönüş değerleri

- **TX_SUCCESS** (0x00) başarılı modül yüklemesi.
- **TX_CALLER_ERROR** (0x13) geçersiz çağrı.
- **TX_NOT_AVAILABLE** (0x1d) Yöneticisi başlatılmadı.
- **TX_NO_MEMORY** (0x10) modülü yüklemek için yeterli bellek yok.
- **TX_NOT_DONE** (0x20) medya açık değil, dosya bulunamadı veya dosya geçersiz.
- **TX_PTR_ERROR** (0x03) geçersiz modül işaretçisi.
- **TXM_MODULE_ALIGNMENT_ERROR** (0xf0) geçersiz hizalama.
- **TXM_MODULE_ALREADY_LOADED** (0xf1) modülü zaten yüklü.
- **TXM_MODULE_INVALID** (0xF2) | Geçersiz modül girişi.
- **TXM_MODULE_INVALID_PROPERTIES** (0xF3) uyumsuz Özellikler.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
TXM_MODULE_INSTANCE my_module;

/* Initialize the module manager. */
status = txm_module_manager_initialize((VOID*)0x64010000,0x10000);

/* Load the module from a binary file. */
status = txm_module_manager_file_load(&my_module, "my module",
                                      &sdio_disk, "demo_thread_module.bin");

/* Start the module. */
status = txm_module_manager_start(&my_module);
```

### <a name="see-also"></a>Ayrıca bkz.

- txm_module_manager_in_place_load
- txm_module_manager_memory_load
- txm_module_manager_unload

---

## <a name="txm_module_manager_in_place_load"></a>txm_module_manager_in_place_load

Yalnızca modül verilerini yükle, modülü mevcut konumda Yürüt.

### <a name="prototype"></a>Prototype

```c
UINT txm_module_manager_in_place_load(
    TXM_MODULE_INSTANCE *module_instance,
    CHAR *module_name,
    VOID *location);
```

### <a name="description"></a>Açıklama

Bu hizmet, modülün veri alanını yalnızca modül bellek alanına yükler ve yürütülmek üzere hazırlar. Modül kodu yürütme, belirtilen konumdaki modül girişi tarafından belirtilen adres uzaklığında yerinde olacaktır.

### <a name="input-parameters"></a>Giriş parametreleri

- **module_instance** Modülün örneğine yönelik işaretçi.
- **module_name** Modülün adı.
- **konum** Modülün kod alanına yönelik işaretçi, giriş ilk.

### <a name="return-values"></a>Dönüş değerleri

- **TX_SUCCESS** (0x00) başarılı modül yüklemesi.
- **TX_CALLER_ERROR** (0x13) geçersiz çağrı.
- **TX_NOT_AVAILABLE** (0x1d) Yöneticisi başlatılmadı.
- **TX_NO_MEMORY** (0x10) modülü yüklemek için yeterli bellek yok.
- **TX_PTR_ERROR** (0x03) geçersiz işaretçi, modül örneği veya modül girişi.
- **TXM_MODULE_ALIGNMENT_ERROR** (0xf0) geçersiz hizalama.
- **TXM_MODULE_ALREADY_LOADED** (0xf1) modülü zaten yüklü.
- **TXM_MODULE_INVALID** (0xF2) geçersiz modül girişi.
- **TXM_MODULE_INVALID_PROPERTIES** (0xF3) uyumsuz Özellikler.

### <a name="allowed-from"></a>İzin verilen

Başlatma ve iş parçacıkları

### <a name="example"></a>Örnek

```c
TXM_MODULE_INSTANCE my_module;

/* Initialize the module manager with 64KB of RAM starting at address 0x64010000. */
txm_module_manager_initialize((VOID *) 0x64010000, 0x10000);

/* Load the module that has its code area at address 0x080F0000. */
txm_module_manager_in_place_load(&my_module, "my module", (VOID *) 0x080F0000);

/* Start the module. */
txm_module_manager_start(&my_module);
```

### <a name="see-also"></a>Ayrıca bkz.

- txm_module_manager_file_load
- txm_module_manager_memory_load
- txm_module_manager_unload

---

## <a name="txm_module_manager_initialize"></a>txm_module_manager_initialize

Modül Yöneticisini başlatın.

### <a name="prototype"></a>Prototype

```c
UINT txm_module_manager_initialize(
    VOID *module_memory_start,
    ULONG module_memory_size);
```

### <a name="description"></a>Açıklama

Bu hizmet modül yöneticisinin iç kaynaklarını, modülleri yüklemek için kullanılan bellek alanı dahil olmak üzere başlatır.

### <a name="input-parameters"></a>Giriş parametreleri

- **module_memory_start** Modül belleğinin başlangıcına yönelik işaretçi.
- **module_memory_size** Modül belleğinin bayt cinsinden boyutu.

### <a name="return-values"></a>Dönüş değerleri

- **TX_SUCCESS** (0x00) başarıyla başlatıldı.
- **TX_CALLER_ERROR** (0x13) geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

Başlatma ve iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Initialize the module manager with 64KB of RAM starting at
   address 0x64010000. */
txm_module_manager_initialize((VOID *) 0x64010000, 0x10000);
```

### <a name="see-also"></a>Ayrıca bkz.

- txm_module_manager_object_pool_create

---

## <a name="txm_module_manager_initialize_mmu"></a>txm_module_manager_initialize_mmu

Bellek yönetimi donanımını başlatın.

### <a name="prototype"></a>Prototype

```c
UINT txm_module_manager_initialize_mmu(VOID);
```

### <a name="description"></a>Açıklama

Bu hizmet, MMU başlatır.

### <a name="input-parameters"></a>Giriş parametreleri

yok

### <a name="return-values"></a>Dönüş değerleri

- **TX_SUCCESS** (0x00) başarıyla başlatıldı.
- **TX_CALLER_ERROR** (0x13) geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

Başlatma ve Iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Initialize the module manager with 64KB of RAM starting at address 0x64010000. */
txm_module_manager_initialize((VOID *) 0x64010000, 0x10000);

/* Initialize the MMU. */
txm_module_manager_initialize_mmu();
```

---

## <a name="txm_module_manager_maximum_module_priority_set"></a>txm_module_manager_maximum_module_priority_set

Bir modülde izin verilen en fazla iş parçacığı önceliğini ayarlayın.

### <a name="prototype"></a>Prototype

```c
UINT txm_module_manager_maximum_module_priority_set(
         TXM_MODULE_INSTANCE *module_instance,
         UINT priority);
```

### <a name="description"></a>Açıklama

Bu hizmet, bir modülde izin verilen en fazla iş parçacığı önceliğini ayarlar.

### <a name="input-parameters"></a>Giriş parametreleri

- **module_instance** Modülün örneğine yönelik işaretçi.
- **Öncelik** En fazla iş parçacığı önceliği.

### <a name="return-values"></a>Dönüş değerleri

- **TX_SUCCESS** (0x00) başarıyla başlatıldı.
- **TX_NOT_AVAILABLE** (0x1d) Yöneticisi başlatılmadı.
- **TX_PTR_ERROR** (0x03) geçersiz modül örneği.
- **TX_START_ERROR** (0x10) modül yüklü durumda değil.

### <a name="allowed-from"></a>İzin verilen

Başlatma ve iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Load the module that has its code area at address 0x080F0000. */
txm_module_manager_in_place_load(&my_module, "my module", (VOID *) 0x080F0000);

/* Set the maximum thread priority in my_module to 5. */
txm_module_manager_maximum_module_priority_set(&my_module, 5);
```

---

## <a name="txm_module_manager_memory_fault_notify"></a>txm_module_manager_memory_fault_notify

Bellek hatasında bir uygulama geri araması kaydedin.

### <a name="prototype"></a>Prototype

```c
UINT txm_module_manager_memory_fault_notify(
     VOID (*notify_function)(TX_THREAD *, MODULE_INSTANCE *));
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen uygulama belleği hata bildirimi geri arama işlevini Modül Yöneticisi ile kaydeder. Bir bellek hatası oluşursa, bu işlev sorunlu iş parçacığına ve soruna neden olan iş parçacığına karşılık gelen modül örneğine yönelik bir işaretçi ile çağırılır. Modül Yöneticisi işlemi, sorunlu iş parçacığını otomatik olarak sonlandırır, ancak modüldeki diğer iş parçacıklarını bırakır. Bellek hatası ile ilişkili modülle ne yapacağına karar vermek uygulamaya kadar yapılır.

Bellek hatası hakkında belirli bilgiler için lütfen iç **_txm_module_manager_memory_fault_info** yapısına bakın.

> [!NOTE]
> Bellek hatası bildirimi geri çağırma işlevi doğrudan bellek hatası özel durumuyla yürütülür, bu nedenle yalnızca kesme hizmeti yordamlarından Izin verilen ThreadX API 'Leri çağrılabilir. Bu nedenle, soruna neden olan modülün durdurulması ve kaldırılması için, uygulama bildirimi geri çağrısının bir uygulama görevine bir sinyal gönderilmesi gerekir, böylece modülün durdurulup bellekten kaldırılabilir.

### <a name="input-parameters"></a>Giriş parametreleri

- **notify_function** Uygulamanın bellek hatası bildirimi geri çağırması için işlev işaretçisi. NULL değer sağlama, bellek hata bildirimini devre dışı bırakır.

### <a name="return-values"></a>Dönüş değerleri

- **TX_SUCCESS** (0x00) başarılı bildirim işlevi kaydı.

### <a name="allowed-from"></a>İzin verilen

Başlatma ve iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Register a memory fault callback. */
txm_module_manager_memory_fault_notify(my_memory_fault_handler);
```

---

## <a name="txm_module_manager_memory_load"></a>txm_module_manager_memory_load

Modülü bellekten yükleyin.

### <a name="prototype"></a>Prototype

```c
UINT txm_module_manager_memory_load (
    TXM_MODULE_INSTANCE *module_instance,
    CHAR *module_name,
    VOID *location);
```

### <a name="description"></a>Açıklama

Bu hizmet, modülün kodunu ve veri alanını ***txm_module_manager_initialize*** tarafından ayarlanan modül bellek alanına yükler ve yürütülmek üzere hazırlar.

### <a name="input-parameters"></a>Giriş parametreleri

- **module_instance** Modülün örneğine yönelik işaretçi.
- **module_name** Modülün adı.
- **konum** Modülün kod alanına yönelik işaretçi, giriş ilk.

### <a name="return-values"></a>Dönüş değerleri

- **TX_SUCCESS** (0x00) başarılı modül yüklemesi.
- **TX_CALLER_ERROR** (0x13) geçersiz çağrı.
- **TX_NOT_AVAILABLE** (0x1d) Yöneticisi başlatılmadı.
- **TX_NO_MEMORY** (0x10) modülü yüklemek için yeterli bellek yok.
- **TX_PTR_ERROR** (0x03) geçersiz işaretçi, modül örneği veya modül girişi.
- **TXM_MODULE_ALIGNMENT_ERROR** (0xf0) geçersiz hizalama.
- **TXM_MODULE_ALREADY_LOADED** (0xf1) modülü zaten yüklü.
- **TXM_MODULE_INVALID** (0xF2) geçersiz modül girişi.
- **TXM_MODULE_INVALID_PROPERTIES** (0xF3) uyumsuz Özellikler.

### <a name="allowed-from"></a>İzin verilen

Başlatma ve iş parçacıkları

### <a name="example"></a>Örnek

```c
TXM_MODULE_INSTANCE     my_module;

/* Initialize the module manager with 64KB of RAM starting at address 0x64010000. */
txm_module_manager_initialize((VOID *) 0x64010000, 0x10000);

/* Load the module that has its code area at address 0x080F0000. */
 txm_module_manager_memory_load(&my_module, "my module", (VOID *) 0x080F0000);
```

### <a name="see-also"></a>Ayrıca bkz.

- txm_module_manager_file_load
- txm_module_manager_in_place_load
- txm_module_manager_unload

---

## <a name="txm_module_manager_object_pool_create"></a>txm_module_manager_object_pool_create

Modüller için bir nesne havuzu oluşturun.

### <a name="prototype"></a>Prototype

```c
UINT txm_module_manager_object_pool_create(
    VOID *pool_memory_start,
    ULONG pool_memory_size);
```

### <a name="description"></a>Açıklama

Bu hizmet, modüllerin ThreadX/NetX nesneleri ayırabilecek bir modül Yöneticisi nesne bellek havuzu oluşturur ve bu sayede sistem nesnesini modülün bellek alanından ayırır.

### <a name="input-parameters"></a>Giriş parametreleri

- **pool_memory_start** Nesne belleğinin başlangıcına yönelik işaretçi.
- **pool_memory_size** Nesne bellek havuzunun bayt cinsinden boyutu.

### <a name="return-values"></a>Dönüş değerleri

- **TX_SUCCESS** (0x00) başarıyla başlatıldı.
- **TX_CALLER_ERROR** (0x13) geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

Başlatma ve iş parçacıkları

### <a name="example"></a>Örnek

```c
TXM_MODULE_INSTANCE my_module;

/* Initialize the module manager with 64KB of RAM starting at address 0x64010000. */
txm_module_manager_initialize((VOID *) 0x64010000, 0x10000);

/* Create an object memory pool in the next 64KB of memory. */
txm_module_manager_object_pool_create((VOID *) 0x64020000, 0x10000);
```

### <a name="see-also"></a>Ayrıca bkz.

- txm_module_manager_initialize

---

## <a name="txm_module_manager_properties_get"></a>txm_module_manager_properties_get

Modül özelliklerini al.

### <a name="prototype"></a>Prototype

```c
UINT txm_module_manager_properties_get(
    TXM_MODULE_INSTANCE *module_instance,
    ULONG *module_properties_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, bir modülün (giriş bölümünde belirtilen) özellikleri döndürür.

### <a name="input-parameters"></a>Giriş parametreleri

- **module_instance** Modül örneğine yönelik işaretçi.
- **module_properties_ptr** Modülün özellikleri için hedef işaretçisi.

### <a name="return-values"></a>Dönüş değerleri

- **TX_SUCCESS** (0x00) başarıyla başlatıldı.
- **TX_PTR_ERROR** (0x03) geçersiz işaretçi.
- **TX_CALLER_ERROR** (0x13) geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
TXM_MODULE_INSTANCE     my_module;
ULONG                   module_properties;

/* Initialize the module manager with 64KB of RAM starting at address 0x64010000. */
txm_module_manager_initialize((VOID *) 0x64010000, 0x10000);

/* Create an object memory pool in the next 64KB of memory. */
txm_module_manager_object_pool_create((VOID *) 0x64020000, 0x10000);

/* Load the module that has its code area at address 0x080F0000. */
txm_module_manager_in_place_load(&my_module, "my module", (VOID *) 0x080F0000);

/* Get module properties. */
txm_module_manager_properties_get(&my_module, &module_properties);
```

---

## <a name="txm_module_manager_start"></a>txm_module_manager_start

Modülün yürütülmesini başlatın.

### <a name="prototype"></a>Prototype

```c
UINT txm_module_manager_start(TXM_MODULE_INSTANCE *module_instance);
```

### <a name="description"></a>Açıklama

Bu hizmet belirtilen, zaten yüklü olan modülün yürütülmesini başlatır.

### <a name="input-parameters"></a>Giriş parametreleri

- **module_instance** Daha önce yüklenmiş modül örneğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş değerleri

- **TX_SUCCESS** (0x00) başarılı modül başladı.
- **TX_CALLER_ERROR** (0x13) geçersiz çağrı.
- **TX_NOT_AVAILABLE** (0x1d) Yöneticisi başlatılmadı.
- **TX_PTR_ERROR** (0x03) geçersiz işaretçi veya modül örneği.
- **TX_START_ERROR** (0x10) modülü zaten başlatılmış.

### <a name="allowed-from"></a>İzin verilen

Başlatma ve iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Start the module. */
txm_module_manager_start(&my_module);

/* Let the module run for a while. */
tx_thread_sleep(2000);

/* Stop the module. */
txm_module_manager_stop(&my_module);

/* Unload the module. */
txm_module_manager_unload(&my_module);
```

### <a name="see-also"></a>Ayrıca bkz.

- txm_module_manager_stop

---

## <a name="txm_module_manager_stop"></a>txm_module_manager_stop

Modülün yürütülmesini durdurun.

### <a name="prototype"></a>Prototype

```c
UINT txm_module_manager_stop(TXM_MODULE_INSTANCE *module_instance);
```

### <a name="description"></a>Açıklama

Bu hizmet daha önce yüklenmiş ve başlatılmış bir modülü durduruyor. Modül durdurulduğunda modülün isteğe bağlı durdurma iş parçacığını yürütme, tüm iş parçacıklarını sonlandırma ve modülle ilişkili tüm kaynakları silme dahildir.

### <a name="input-parameters"></a>Giriş parametreleri

- **module_instance** Modül örneğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş değerleri

- **TX_SUCCESS** (0x00) başarılı modül durdu.
- **TX_CALLER_ERROR** (0x13) geçersiz çağrı.
- **TX_NOT_AVAILABLE** (0x1d) Yöneticisi başlatılmadı.
- **TX_PTR_ERROR** (0x03) geçersiz işaretçi veya modül örneği.
- **TX_START_ERROR** (0x10) modül başlatılmadı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Start the module. */
txm_module_manager_start(&my_module);

/* Let the module run for a while. */
tx_thread_sleep(20000);

/* Stop the module. */
txm_module_manager_stop(&my_module);

/* Unload the module. */
txm_module_manager_unload(&my_module);
```

### <a name="see-also"></a>Ayrıca bkz.

- txm_module_manager_start

---

## <a name="txm_module_manager_unload"></a>txm_module_manager_unload

Modülü kaldırın.

### <a name="prototype"></a>Prototype

```c
UINT txm_module_manager_unload(TXM_MODULE_INSTANCE *module_instance);
```

### <a name="description"></a>Açıklama

Bu hizmet, daha önce yüklenmiş ve durdurulmuş modülünü kaldırır ve tüm ilişkili modül bellek kaynaklarını serbest bırakır.

### <a name="input-parameters"></a>Giriş parametreleri

- **module_instance** Modülün örneğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş değerleri

- **TX_SUCCESS** 0x00) başarılı modül yüklemesi.
- **TX_CALLER_ERROR** (0x13) geçersiz çağrı.
- **TX_NOT_AVAILABLE** (0x1d) Yöneticisi başlatılmadı.
- **TX_NOT_DONE** (0x20) geçersiz modül veya modül durdurulmadı.
- **TX_PTR_ERROR** (0x03) geçersiz işaretçi veya modül örneği.

### <a name="allowed-from"></a>İzin verilen

Başlatma ve iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Stop the module. */
txm_module_manager_stop(&my_module);

/* Unload the module. */
status = txm_module_manager_unload(&my_module);
```

### <a name="see-also"></a>Ayrıca bkz.

- txm_module_manager_file_load
- txm_module_manager_in_place_load
- txm_module_manager_memory_load
- txm_module_manager_stop
