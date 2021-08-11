---
title: Bölüm 4-Azure RTOS NetX şifreleme API 'SI açıklaması
description: Azure RTOS NetX şifreleme API 'SI açıklaması
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 5bd4cdae28a293ec9ef259bbd29fdb8f8d6dc43f964cbc184290b82ee8f590a3
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116788821"
---
# <a name="chapter-4---azure-rtos-netx-crypto-api-description"></a>Bölüm 4-Azure RTOS NetX şifreleme API 'SI açıklaması

## <a name="nx_crypto_initialize"></a>nx_crypto_initialize

NetX güvenli kitaplığını başlatır

### <a name="prototype"></a>Prototype

```c
UINT nx_crypto_initialize(VOID);
```

### <a name="description"></a>Description

Bu işlev, Azure RTOS NetX şifre kitaplığı modülünü başlatır. Diğer şifreleme işlevlerinin hiçbirini kullanmadan önce, uygulamanın başlatma işlemini gerçekleştirmek ve kitaplığın bütünlüğünü doğrulamak için bu işlevi çağırması gerekir. Diğer NetX şifreleme hizmetlerini kullanmadan önce bu işlevi çağırmaya yönelik hata döndürülmeyecektir.

### <a name="parameters"></a>Parametreler

- **Hiçbiri**

### <a name="return-values"></a>Dönüş Değerleri

- **NX_CRYPTO_SUCCESS** (0x00) başarıyla başlatılmış NETX şifre kitaplığı. Kitaplık işlevleri artık hazırdır ve kullanılabilir.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifreleme kitaplığı başlatılamıyor veya bütünlük denetimini yapamıyor. Uygulama bu kitaplığı kullanamıyor.

### <a name="example"></a>Örnek

TODO

## <a name="nx_crypto_module_state_get"></a>nx_crypto_module_state_get

FIPS etkin modülünün geçerli durumunu alma

### <a name="prototype"></a>Prototype

```c
UINT nx_crypto_module_state_get(VOID);
```

### <a name="description"></a>Description

Bu hizmet yalnızca FIPS derleme kitaplığı 'nda kullanılabilir. NetX şifre kitaplığının geçerli durumunun durumunu döndürür.

### <a name="parameters"></a>Parametreler

- **Hiçbiri**

### <a name="return-values"></a>Dönüş Değerleri

- **Durum bayrağı:**
  - NX_CRYPTO_LIBRARY_STATE_UNINITIALIZED 0x00000001
  - NX_CRYPTO_LIBRARY_STATE_POST_IN_PROGRESS 0x00000002
  - NX_CRYPTO_LIBRARY_STATE_INTEGRITY_TEST_FAILED 0x00000004
  - NX_CRYPTO_LIBRARY_STATE_FUNCTIONAL_TEST_FAILED 0x00000008
  - NX_CRYPTO_LIBRARY_STATE_OPERATIONAL 0x80000000
- **Diğer tüm değerler geçersiz.**

### <a name="example"></a>Örnek

TODO

## <a name="_nx_crypto_method_aes_init"></a>_nx_crypto_method_aes_init

AES şifreleme denetim bloğunu başlatır

### <a name="prototype"></a>Prototype

```c
UINT _nx_crypto_method_aes_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size);
```

### <a name="description"></a>Description

Bu işlev, AES denetim bloğunu verilen anahtar dizesiyle başlatır. AES denetim bloğu başlatıldıktan sonra, sonraki AES işlemi aynı anahtar ve anahtar boyutunu kullanacaktır.

Uygulama birden çok AES denetim bloğu oluşturabilir, her biri bir oturumu temsil eder. Bir denetim bloğuna bir anahtar atanır. Sonraki şifreleme veya şifre çözme işlemi, AES denetim bloğunu yeniden başlatmaya gerek kalmadan aynı AES denetim bloğuna başvurabilir. Oturumun anahtarı değiştirilirse, uygulamanın, güncelleştirilmiş anahtarla AES denetim bloğunu yeniden başlatması gerekir.

_ *Nx_crypto_method_aes_init ()* çağrısı, önceden yapılandırılmış bir anahtarı ve anahtar boyutunu yeni anahtara otomatik olarak güncelleştirir.

### <a name="parameters"></a>Parametreler

- **yöntemi** Geçerli bir AES şifreleme yöntemi denetim bloğuna işaretçi. Aşağıdaki önceden tanımlanmış AES şifreleme yöntemleri kullanılabilir:
  - *crypto_method_aes_cbc_128*
  - *crypto_method_aes_cbc_192*
  - *crypto_method_aes_cbc_256*
  - *crypto_method_aes_ctr_128*
  - *crypto_method_aes_ctr_192*
  - *crypto_method_aes_ctr_256*
  - *crypto_method_aes_xcbc_128*
  - *crypto_method_aes_ccm_8_128*
- **anahtar** AES anahtarını içeren bir arabelleğe işaret eder
- **key_size_in_bits** Anahtarın bit cinsinden boyutu. Geçerli değerler:
  - *NX_CRYPTO_AES_KEY_SIZE_128_BITS*
  - *NX_CRYPTO_AES_KEY_SIZE_192_BITS*
  - *NX_CRYPTO_AES_KEY_SIZE_256_BITS*
  - **Diğer tüm değerler geçersiz.**
- **tanıtıcı** Bu hizmet, çağırana bir tanıtıcı döndürür. Tanıtıcı uygulamaya bağımlıdır ve bu uygulamada kullanılmıyor. Uygulama tanıtıcı için NULL değer geçirecektir.
- **crypto_metadata** AES denetim bloğu için geçerli bir bellek alanı işaretçisi. Bellek alanının başlangıç adresi 4 bayt hizalı olmalıdır.
- **crypto_metadata_size** Crypto_metadata alanının bayt cinsinden boyutu. AES için meta veri boyutu *sizeof olmalıdır (NX_AES)*

### <a name="return-values"></a>Dönüş Değerleri

- **NX_CRYPTO_SUCCESS** (0x00) anahtar ve anahtar boyutuyla AES denetim bloğunun başarılı bir şekilde başlatılması.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.
- **NX_PTR_ERROR (0x07)** Anahtar için geçersiz işaretçi veya crypto_metadata ya da crypto_metadata_size geçersiz veya crypto_metadata 4 baytlık hizalı değil.
- **NX_CRYPTO_UNSUPPORTED_KEY_SIZE** (0x20002) anahtar boyutu AES için geçerli değil.

## <a name="_nx_crypto_method_aes_operation"></a>_nx_crypto_method_aes_operation

AES işlemi gerçekleştirin (şifreleme veya şifre çözme).

### <a name="prototype"></a>Prototype

```c
UINT _nx_crypto_method_aes_operation(UINT op,
    VOID *handle,
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    UCHAR *input,
    ULONG input_length_in_byte,
    UCHAR *iv_ptr,
    UCHAR *output,
    ULONG output_length_in_byte,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size,
    VOID *packet_ptr,
    VOID (*nx_crypto_hw_process_callback)(VOID *packet_ptr, UINT status));
```

### <a name="description"></a>Description

Bu işlev AES şifreleme veya şifre çözme işlemi gerçekleştirir. AES denetim bloğunun _ *nx_crypto_method_aes_init ()* ile başlatılmış olması gerekir. Gerçekleştirilecek AES algoritması, *Yöntem* denetim bloğunda belirtilen algoritmayı temel alır.

Giriş arabelleği boyutu 16 baytın katlarından biri olmalıdır. Şifresi çözülen verilerin boyutu, giriş veri boyutunun aynı boyutudur. Şifrelenmiş veriler, AES blok boyutunun bir çift katı elde etmek için doldurulmuştur, doldurma, çıkış arabelleğine dahil edilir ve uygulama tarafından işlenmelidir.

Bu işlem durum bilgilerini saklar ve AES denetim bloğunda anahtar malzemesini değiştirmez.

Op NX_CRYPTO_SET_ADDITIONAL_DATA ve algoritm AES-CCM8 olduğunda, giriş ek verilere işaret eder ve input_length_in_byte ek verilerin uzunluktadır.

### <a name="parameters"></a>Parametreler

- **op** Gerçekleştirilecek işlemin türü. Geçerli işletim amaçları şunlardır:
  - *NX_CRYPTO_ENCRYPT*
  - *NX_CRYPTO_DECRYPT*
  - *NX_CRYPTO_AUTHENTICATE (yalnızca AES-XCBC)*
  - *NX_CRYPTO_SET_ADDITIONAL_DATA (yalnızca AES-CCM8)*
- **tanıtıcı** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz. Geçirilen tüm değerler sessizce yok sayılır.
- **yöntemi** Geçerli AES şifreleme yöntemine yönelik işaretçi. Burada kullanılan şifreleme yöntemi, *nx_crypto_method_aes_init ()* içinde kullanılan aynı olmalıdır.
- **input_data** Şifrelenmiş metin verileri içeren bir arabelleğe işaret eder. Giriş arabelleğinde kısıtlama yoktur.
- **input_data_size** Giriş verilerinin bayt cinsinden boyutu. Giriş verisi boyutu 16 baytın katlarından biri olmalıdır.
- **iv_ptr** Ilk vektör işaretçisi. IV arabelleğinde kısıtlama yoktur.
- **iv_size** Başlangıçtaki vektör bloğunun boyutu, bayt cinsinden bu alanın 16 olması gerekir.
- **output_buffer** Şifresiz metin verilerini depolamak için AES için bellek alanı işaretçisi. Uygulama, çıkış arabelleği için alan ayırmalıdır. Çıkış arabelleği, giriş arabelleğiyle çakışabilir. Aynı başlangıç adresini paylaştıkları takdirde çıkış arabelleği giriş arabelleğiyle çakışabilir.
- **output_buffer_size** Çıkış arabelleğinin bayt cinsinden boyutu. Çıkış arabelleği boyutunun en az girdi arabellek boyutuyla aynı olması ve çıkış arabelleği boyutunun 16 baytın katlarından biri olması gerekir.
- **crypto_metadata** *_Nx_crypto_method_aes_init () \* \** içinde kullanılan AES denetim bloğuna yönelik işaretçi.
- **crypto_metadata_size** Crypto_metadata alanının bayt cinsinden boyutu. AES için meta veri boyutu *sizeof (NX_AES)* olmalıdır
- **packet_ptr** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz. Geçirilen tüm değerler sessizce yok sayılır.
- **nx_crypto_hw_process_callback** -Bu alan, NETX şifreleme kitaplığının yazılım uygulamasında kullanılmaz. Geçirilen tüm değerler sessizce yok sayılır.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_CRYPTO_SUCCESS** (0x00), AES işlemini başarıyla yürütüldü.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.
- **NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi veya uzunluğu geçersiz.
- **NX_CRYPTO_INVALID_ALGORITHM** (0x20004) geçersiz AES algoritması belirtildi * *.

## <a name="_nx_crypto_method_aes_cleanup"></a>_nx_crypto_method_aes_cleanup

AES denetim bloğunu temizleyin.

### <a name="prototype"></a>Prototype

```c
UINT _nx_crypto_method_aes_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a>Description

Uygulama, bu AES oturumunun artık gerekli olmadığını belirlediğinde AES denetim bloğunu temizlemek için bu işlevi çağırır.

### <a name="parameters"></a>Parametreler

- **crypto_metadata** *_Nx_crypto_method_aes_init () \* \** içinde kullanılan AES denetim bloğuna yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_CRYPTO_SUCCESS** (0x00) AES oturumu başarıyla temizlendi.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.

## <a name="_nx_crypto_method_3des_init"></a>_nx_crypto_method_3des_init

3DES denetim bloğunu başlatın.

### <a name="prototype"></a>Prototype

```c
UINT _nx_crypto_method_3des_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size);
```

### <a name="description"></a>Description

Bu işlev, Üçlü DES (3DES) denetim bloğunu verilen üç anahtar dizesi ile başlatır. Anahtar dizeleri her biri 8 bayt olmalıdır. Üç DES tuşu, 24 baytlık bir arabelleğin bitişik belleğine birleştirilmiş olmalıdır. FIPS uyumlu derleme için, üç anahtar her birinden farklı olmalıdır veya işlev NX_CRYPTO_INVALID_KEY hatası döndürür. 3DES denetim bloğu başlatıldıktan sonra, sonraki 3DES işlemleri de aynı anahtarları kullanır.

Bir uygulama, her biri bir oturumu temsil eden birden çok 3DES denetim bloğu oluşturabilir. Bir denetim bloğuna bir anahtar atanır ve sonraki şifreleme veya şifre çözme işlemleri yeniden başlatmaya gerek kalmadan aynı denetim bloğuna başvurabilir. Bir oturumun anahtarı değiştirilirse, uygulamanın denetim bloğunu güncelleştirilmiş anahtarla yeniden başlatması gerekir.

_ *Nx_crypto_method_3des_init ()* çağrısı, önceden yapılandırılmış bir anahtarı yeni anahtarlara otomatik olarak güncelleştirir.

### <a name="parameters"></a>Parametreler

- **yöntemi** Geçerli bir 3DES şifreleme yöntemi denetim bloğuna işaretçi. Aşağıdaki önceden tanımlanmış 3DES şifreleme yöntemi kullanılabilir: ***crypto_method_3des***
- **anahtar** Üç (3) DES anahtarını içeren bir arabelleğe işaret eder
- **key_size_in_bits** 192 (3 anahtar, her 64 bit) olmalıdır.
- **tanıtıcı** Bu hizmet, çağırana bir tanıtıcı döndürür. Tanıtıcı, başlatılan 3DES denetim bloğunu tanımlar. Sonraki 3DES işlemleri (şifreleme, şifre çözme ve temizleme), 3DES denetim bloğuna erişmek için bu tanıtıcıyı kullanır
- **crypto_metadata** 3DES denetim bloğu için geçerli bir bellek alanı işaretçisi. Bellek alanının başlangıç adresi 4 bayt hizalı olmalıdır.
- **crypto_metadata_size** Crypto_metadata alanının bayt cinsinden boyutu. 3DES için meta veri boyutu *sizeof olmalıdır (NX_3DES)*

### <a name="return-value"></a>Dönüş Değeri

- Anahtar ve anahtar boyutuyla 3DES denetim bloğunun başarılı bir şekilde başlatılması **NX_CRYPTO_SUCCESS** (0x00).
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.
- **NX_PTR_ERROR (0x07)** Anahtar için geçersiz işaretçi veya crypto_metadata ya da crypto_metadata_size geçersiz veya crypto_metadata 4 baytlık hizalı değil.
- **NX_CRYPTO_UNSUPPORTED_KEY_SIZE** (0x20002) anahtar boyutu 3DES için geçerli değil.

## <a name="_nx_crypto_method_3des_operation"></a>_nx_crypto_method_3des_operation

3DES ile şifreleme veya şifre çözme.

### <a name="prototype"></a>Prototype

```c
UINT _nx_crypto_method_3des_operation(UINT op,
    VOID *handle,
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    UCHAR *input,
    ULONG input_length_in_byte,
    UCHAR *iv_ptr,
    UCHAR *output,
    ULONG output_length_in_byte,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size,
    VOID *packet_ptr,
    VOID (*nx_crypto_hw_process_callback)(VOID *packet_ptr, UINT
    status));
```

### <a name="description"></a>Description

Bu işlev 3DES şifrelemesini veya şifre çözme işlemini gerçekleştirir. 3DES denetim bloğunun _ *nx_crypto_method_3des_init ()* ile başlatılmış olması gerekir. Gerçekleştirilecek 3DES algoritması, *Yöntem* denetim bloğunda belirtilen algoritmayı temel alır.

Giriş arabelleği boyutu 8 baytın katlarından biri olmalıdır. Şifresi çözülen verilerin boyutu, giriş veri boyutunun aynı boyutudur. Şifrelenmiş veriler, 3DES blok boyutundan oluşan çift bir değeri elde etmek için doldurulmuştur, doldurma, çıkış arabelleğine dahil edilir ve uygulama tarafından işlenmelidir.

Bu işlem durum bilgilerini saklar ve 3DES denetim bloğunda anahtar malzemesini değiştirmez.

### <a name="parameters"></a>Parametreler

- **op** Gerçekleştirilecek işlemin türü. Geçerli işlemler şunlardır:
  - *NX_CRYPTO_ENCRYPT*
  - *NX_CRYPTO_DECRYPT*
- **tanıtıcı** *_Nx_crypto_method_3des_init ()* tarafından başlatılan tanıtıcı.
- **yöntemi** Geçerli 3DES şifreleme yöntemine yönelik işaretçi. Burada kullanılan şifreleme yöntemi, *nx_crypto_method_3des_init ()* içinde kullanılan aynı olmalıdır.
- **input_data** Şifrelenmiş metin verileri içeren bir arabelleğe işaret eder.
Giriş arabelleğinde kısıtlama yoktur.
- **input_data_size** Giriş verilerinin bayt cinsinden boyutu. Giriş veri boyutu 8 baytın katlarından biri olmalıdır.
- **iv_ptr** Ilk vektör işaretçisi. IV arabelleğinde kısıtlama yoktur.
- **iv_size** Ilk vektör bloğunun boyutu, bayt cinsinden bu alanın 8 olması gerekir.
- **output_buffer** Şifresiz metin verilerini depolamak için 3DES bellek alanına yönelik işaretçi. Uygulama, çıkış arabelleği için alan ayırmalıdır. Çıkış arabelleği, giriş arabelleğiyle çakışabilir. Aynı başlangıç adresini paylaştıkları takdirde çıkış arabelleği giriş arabelleğiyle çakışabilir.
- **output_buffer_size** Çıkış arabelleğinin bayt cinsinden boyutu. Çıkış arabelleği boyutunun en az girdi arabellek boyutuyla aynı olması ve çıkış arabelleği boyutunun 8 baytın katlarından biri olması gerekir.
- **crypto_metadata** *_Nx_crypto_method_3des_init ()* IÇINDE kullanılan 3DES denetim bloğuna yönelik işaretçi.
- **crypto_metadata_size** Crypto_metadata alanının bayt cinsinden boyutu. 3DES için meta veri boyutunun *sizeof(NX_3DES) olması gerekir*
- **packet_ptr** Bu alan, NetX Şifreleme kitaplığının yazılım uygulamasında kullanılmaz. Geçirilen tüm değerler sessizce yoksayılır.
- **nx_crypto_hw_process_callback** Bu alan, NetX Şifreleme kitaplığının yazılım uygulamasında kullanılmaz. Geçirilen tüm değerler sessizce yoksayılır.

### <a name="description"></a>Description

Bu işlev 3DES şifrelemesi gerçekleştirir. 3DES denetim bloğu _ *nx_crypto_moethod_3des_init() ile başlatılmış olması gerekir.* Bu işlem durum bilgilerini tutmaz ve 3DES denetim bloğunda anahtar malzemeyi değiştirmez. Doldurmanın bu işlev tarafından eklenmez, bu nedenle çağıranın şifreleme işlemi çağrılmadan önce doldurmayı işlemesi gerekir.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_CRYPTO_SUCCESS** (0x00) Anahtar ve anahtar boyutuyla 3DES denetim bloğu başarıyla başlatıldı.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) Şifreleme kitaplığı geçersiz durumda ve kullanılamaz.
- **NX_PTR_ERROR (0x07)** Anahtarın geçersiz işaretçisi veya geçersiz crypto_metadata veya crypto_metadata_size veya crypto_metadata 4 bayta hizalanmamış.

## <a name="_nx_crypto_method_3des_cleanup"></a>_nx_crypto_method_3des_cleanup

3DES denetim bloğu'ları temizleyin.

### <a name="prototype"></a>Prototype

```c
UINT _nx_crypto_method_3des_cleanup(VOID *crypto_metadata);
```

### <a name="description"></a>Description

Uygulama, bu 3DES oturumuna artık gerek olmadığını tespit ettikten sonra 3DES denetim bloğunun temizlenmesi için bu işlevi çağırıyor.

### <a name="parameters"></a>Parametreler

- **handle (tanıtıcı)** *_nx_crypto_method_3des_init() tarafından başlatılan tanıtıcı.*

### <a name="return-values"></a>Dönüş Değerleri

- **NX_CRYPTO_SUCCESS** (0x00) 3DES oturumu başarıyla temizlendi.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) Şifreleme kitaplığı geçersiz durumda ve kullanılamaz.

## <a name="_nx_crypto_method_drbg_init"></a>_nx_crypto_method_drbg_init

DRBG şifreleme denetim bloğu başlatılır

### <a name="prototype"></a>Prototype

```c
UINT _nx_crypto_method_drbg_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size);
```

### <a name="description"></a>Description

Bu işlev, VERILEN anahtar dizesiyle DRBG denetim bloğu başlatılır. DRBG denetim bloğu başlatıldıktan sonra, sonraki DRBG işlemi aynı denetim bloğu kullanıyor olur.

Uygulama birden çok DRBG denetim bloğu oluşturabilir ve her biri bir oturumu temsil eder. DRBG denetim bloğu başlatılırken yeni bir karma hesaplama oturumu başlatılır. DRBG denetim bloğu yeniden başlatıla, geçerli oturumdan vazgeçer ve yeni bir oturum sağlar.

### <a name="parameters"></a>Parametreler

- **yöntem** Geçerli bir DRBG şifreleme yöntemi denetim bloğuna işaretçi. Aşağıdaki önceden tanımlanmış şifreleme yöntemleri kullanılabilir:
  - *crypto_method_drbg*
- **anahtar** Bu alan DRBG için kullanılmaz.
- **key_size_in_bits** Bu alan DRBG için kullanılmaz.
- **handle (tanıtıcı)** Bu hizmet çağıranın tanıtıcısı döndürür. Tanıtıcı uygulamaya bağımlıdır ve bu uygulamada kullanılmaz. Uygulama tanıtıcı için NULL değerini geçsin.
- **crypto_metadata** DRBG denetim bloğu için geçerli bir bellek alanı işaretçisi. Bellek alanı başlangıç adresi 4 bayta hizalanmış olması gerekir.
- **crypto_metadata_size** Veri alanı bayt cinsinden crypto_metadata. DRBG için meta veri boyutu *sizeof(NX_CRYPTO_DRBG)*

### <a name="return-values"></a>Dönüş Değerleri

- **NX_CRYPTO_SUCCESS** (0x00) Anahtar ve anahtar boyutuyla DRBG denetim bloğu başarıyla başlatılacak.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) Şifreleme kitaplığı geçersiz durumda ve kullanılamaz.
- **NX_PTR_ERROR** (0x07) Anahtar için geçersiz işaretçi ya da geçersiz crypto_metadata veya crypto_metadata_size veya crypto_metadata 4-byte hizalanmamış.

## <a name="_nx_crypto_method_drbg_operation"></a>_nx_crypto_method_drbg_operation

DRBG işlemi gerçekleştirme

### <a name="prototype"></a>Prototype

```c
UINT __nx_crypto_method_drbg_operation(UINT op,
    VOID *handle,
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    UCHAR *input,
    ULONG input_length_in_byte,
    UCHAR *iv_ptr,
    UCHAR *output,
    ULONG output_length_in_byte,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size,
    VOID *packet_ptr,
    VOID (*nx_crypto_hw_process_callback)(VOID *packet_ptr, UINT
    status));
```

### <a name="description"></a>Description

Bu işlev DRBG işlemini gerçekleştirir. DRBG denetim bloğu _ *nx_crypto_method_drbg_init() ile başlatılmış olması gerekir.* Gerçekleştirilecek DRBG algoritması, yöntem denetim bloğunda belirtilen *algoritmaya* dayalıdır. Varsayılan olarak DRBG için AES-128 kullanılır.

İşlem başarısız NX_CRYPTO_DRBG_OPTIONS_SET, giriş bir yapıya NX_CRYPTO_DRBG_OPTIONS eder. İşlem başarısız NX_CRYPTO_DRBG_INSTANTIATE, giriş kişiselleştirme dizesini ifade eder. İşlem bir NX_CRYPTO_DRBG_RESEED NX_CRYPTO_DRBG_GENERATE ek girişe doğru ilerler.

### <a name="parameters"></a>Parametreler

- **op (op)** Gerçekleştirecek işlem türü. Geçerli işlem:
  - *NX_CRYPTO_DRBG_OPTIONS_SET*
  - *NX_CRYPTO_DRBG_INSTANTIATE*
  - *NX_CRYPTO_DRBG_RESEED NX_CRYPTO_DRBG_GENERATE*
- **handle (tanıtıcı)** Bu alan, NetX Şifreleme kitaplığının yazılım uygulamasında kullanılmaz. Geçirilen tüm değerler sessizce yoksayılır.
- **yöntem** Geçerli DRBG şifreleme yönteminin işaretçisi. Burada kullanılan şifreleme yöntemi , _ *nx_crypto_method_drbg_init() içinde aynı şekilde kullanılmalıdır.*
- **anahtar** Örnek işlem için nonce işaretçisi. Bu alan diğer işlemler için kullanılmaz.
- **key_size_in_bits** Bit olarak nonce boyutu. Bu alan diğer işlemler için kullanılmaz.
- **input (giriş)** İşlem tamam NX_CRYPTO_DRBG_OPTIONS_SET bu alan DRBG seçeneklerine sahiptir. İşlem NX_CRYPTO_DRBG_INSTANTIATE, bu alan kişiselleştirme dizesini ifade ediyor. İşlem, NX_CRYPTO_DRBG_RESEED NX_CRYPTO_DRBG_GENERATE ek giriş verilerine yöneliktir.
- **input_length_in_byte** Giriş verisi boyutu (bayt cinsinden).
- **iv_ptr** Bu alan DRBG için kullanılmaz.
- **output (çıktı)** İşlem NX_CRYPTO_DRBG_GENERATE, bu alan oluşturulan DRBG için bellek alanını kullanır. Aksi takdirde, bu alan kullanılmaz.
- **output_length_in_byte** Çıkış arabelleğinin bayt cinsinden boyutu.
- **crypto_metadata** _nx_crypto_method_drbg_init() içinde kullanılan DRBG *denetim bloğuna işaretçi.*
- **crypto_metadata_size** Veri alanı bayt cinsinden crypto_metadata. DRBG için meta veri boyutunun *boyutof(NX_CRYPTO_DRBG) olması gerekir*
- **packet_ptr** Bu alan, NetX Şifreleme kitaplığının yazılım uygulamasında kullanılmaz. Geçirilen tüm değerler sessizce yoksayılır.
- **nx_crypto_hw_process_callback** Bu alan, NetX Şifreleme kitaplığının yazılım uygulamasında kullanılmaz. Geçirilen tüm değerler sessizce yoksayılır.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_CRYPTO_SUCCESS** (0x00) DRBG işlemi başarıyla yürütülür.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) Şifreleme kitaplığı geçersiz durumda ve kullanılamaz.
- **NX_PTR_ERROR** (0x07) Geçersiz giriş işaretçisi veya geçersiz uzunluk.
- **NX_CRYPTO_INVALID_ALGORITHM** (0x20004) Geçersiz DRBG algoritması belirtiliyor.
- **NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) Geçersiz çıkış arabellek boyutu.

## <a name="_nx_crypto_method_drbg_cleanup"></a>_nx_crypto_method_drbg_cleanup

DRBG denetim bloğu temizleme.

### <a name="prototype"></a>Prototype

```c
UINT _nx_crypto_method_drbg_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a>Description

Uygulama, bu DRBG oturumunun artık gerekli olmadığını belirlediğinde DRBG denetim bloğunu temizlemek için bu işlevi çağırır.

### <a name="parameters"></a>Parametreler

- **crypto_metadata** *_Nx_crypto_method_drbg_init ()* içinde kullanılan drbg denetim bloğuna yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_CRYPTO_SUCCESS** (0x00) drbg oturumunun başarıyla temizlendi.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.

## <a name="_nx_crypto_method_ecdh_init"></a>_nx_crypto_method_ecdh_init

ECDH şifre denetim bloğunu başlatır

### <a name="prototype"></a>Prototype

```c
UINT _nx_crypto_method_ecdh_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size);
```

### <a name="description"></a>Description

Bu işlev, ECDH denetim bloğunu verilen anahtar dizesiyle başlatır. ECDH denetim bloğu başlatıldıktan sonra, sonraki ECDH işlemi aynı denetim bloğunu kullanıyor olacaktır.

Uygulama birden fazla ECDH denetim bloğu oluşturabilir, her biri bir oturumu temsil eder. ECDH denetim bloğunun başlatılması yeni bir karma hesaplama oturumu başlatır. ECDH denetim bloğunu yeniden başlatmak, geçerli oturumu ve yıldızları yeni bir kez terk edin.

### <a name="parameters"></a>Parametreler

- **yöntemi** Geçerli bir ECDH şifreleme yöntemi denetim bloğuna yönelik işaretçi. Aşağıdaki önceden tanımlanmış şifreleme yöntemleri kullanılabilir:
  - *crypto_method_ecdh*
- **anahtar** Bu alan ECDH için kullanılmaz.
- **key_size_in_bits** Bu alan ECDH için kullanılmaz.
- **tanıtıcı** Bu hizmet, çağırana bir tanıtıcı döndürür. Tanıtıcı uygulamaya bağımlıdır ve bu uygulamada kullanılmıyor. Uygulama tanıtıcı için NULL değer geçirecektir.
- **crypto_metadata** ECDH denetim bloğu için geçerli bir bellek alanı işaretçisi. Bellek alanının başlangıç adresi 4 bayt hizalı olmalıdır.
- **crypto_metadata_size** Crypto_metadata alanının bayt cinsinden boyutu. ECDH için meta veri boyutu *sizeof olmalıdır (NX_CRYPTO_ECDH)*

### <a name="return-values"></a>Dönüş Değerleri

- Anahtar ve anahtar boyutuyla ECDH denetim bloğunun başarılı bir şekilde başlatılması **NX_CRYPTO_SUCCESS** (0x00).
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.
- **NX_PTR_ERROR** (0x07) anahtar için geçersiz işaretçi veya geçersiz crypto_metadata veya crypto_metadata_size ya da crypto_metadata 4 bayt hizalı değil.

## <a name="_nx_crypto_method_ecdh_operation"></a>_nx_crypto_method_ecdh_operation

ECDH işlemi gerçekleştir

### <a name="prototype"></a>Prototype

```c
UINT _nx_crypto_method_ecdh_operation(UINT op,
    VOID *handle,
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    UCHAR *input,
    ULONG input_length_in_byte,
    UCHAR *iv_ptr,
    UCHAR *output,
    ULONG output_length_in_byte,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size,
    VOID *packet_ptr,
    VOID (*nx_crypto_hw_process_callback)(VOID *packet_ptr, UINT
    status));
```

### <a name="description"></a>Description

Bu işlev ECDH işlemini gerçekleştirir. ECDH denetim bloğunun _ *nx_crypto_method_ecdh_init ()* ile başlatılmış olması gerekir. Gerçekleştirilecek ECDH algoritması, *Yöntem* denetim bloğunda belirtilen algoritmayı temel alır.

İşlem NX_CRYPTO_EC_CURVE_SET olduğunda, giriş Eliptik Eğri Şifreleme yöntemine işaret eder. İşlem NX_CRYPTO_EC_KEY_PAIR_GENERATE olduğunda, çıkış NX_CRYPTO_EXTENDED_OUTPUT yapısına işaret eder ve anahtar çifti nx_crypto_extended_output_data kopyalanır. İşlem NX_CRYPTO_DH_SETUP olduğunda, ortak anahtar nx_crypto_extended_output_data döndürülür. İşlem NX_CRYPTO_DH_KEY_PAIR_IMPORT olduğunda, girişte ortak anahtar ve anahtar noktaları özel anahtara işaret eder. İşlem NX_CRYPTO_DH_PRIVATE_KEY_EXPORT, özel anahtar nx_crypto_extended_output_data kopyalanır. İşlem NX_CRYPTO_DH_CALCULATE olduğunda, giriş uzak ortak anahtara ve paylaşılan gizliliğe nx_crypto_extended_output_data kopyalanır.

### <a name="parameters"></a>Parametreler

- **op** Gerçekleştirilecek işlemin türü. Geçerli işlem:
  - *NX_CRYPTO_EC_CURVE_SET*
  - *NX_CRYPTO_DH_SETUP*
  - *NX_CRYPTO_DH_CALCULATE*
  - *NX_CRYPTO_DH_KEY_PAIR_IMPOPRT*
  - *NX_CRYPTO_DH_KEY_PAIR_GENERATE*
  - *NX_CRYPTO_DH_PRIVATE_KEY_EXPORT*
- **tanıtıcı** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz. Geçirilen tüm değerler sessizce yok sayılır.
- **yöntemi** Geçerli ECDH şifre yöntemine yönelik işaretçi. Burada kullanılan şifreleme yöntemi _ *nx_crypto_method_ecdh_init ()* içinde kullanılan aynı olmalıdır.
- **anahtar** Op NX_CRYPTO_DH_IMPORT_KEY_PAIR olduğunda, bu alan özel anahtara işaret eder. Aksi takdirde, bu alan ECDH için kullanılmaz.
- **key_size_in_bits** Anahtarın bit cinsinden boyutu.
- **giriş** Op NX_CRYPTO_EC_CURVE_SET olduğunda, bu alan Eliptik Eğri Şifreleme yöntemine işaret eder. Op NX_CRYPTO_DH_SETUP olduğunda, bu alan kullanılmaz. Op NX_CRYPTO_DH_CALCULATE olduğunda, bu alan girdi metin verileri içeren bir arabelleğe işaret eder. Op NX_CRYPTO_DH_IMPORT_KEY_PAIR olduğunda, bu alan ortak anahtara işaret eder.
- **input_length_in_byte** Giriş verilerinin bayt cinsinden boyutu.
- **iv_ptr** Bu alan ECDH için kullanılmaz.
- **Çıkış** Op NX_CRYPTO_EC_CURVE_SET veya NX_CRYPTO_DH_IMPORT_KEY_PAIR, bu alan kullanılmaz. Op NX_CRYPTO_DH_SETUP olduğunda, bu alan oluşturulan ECDH ortak anahtarı için bellek alanını gösterir. Op NX_CRYPTO_DH_CALCULATE olduğunda, bu alan oluşturulan ECDH paylaşılan gizliliğiyle ilgili bellek alanını gösterir.
- **output_length_in_byte** Çıkış arabelleğinin bayt cinsinden boyutu.
- **crypto_metadata** *_Nx_crypto_method_ecdh_init ()* içinde kullanılan ECDH denetim bloğuna yönelik işaretçi.
- **crypto_metadata_size** Crypto_metadata alanının bayt cinsinden boyutu. ECDH için meta veri boyutu sizeof olmalıdır *(NX_CRYPTO_ECDH)*
- **packet_ptr** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz. Geçirilen tüm değerler sessizce yok sayılır.
- **nx_crypto_hw_process_callback** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz. Geçirilen tüm değerler sessizce yok sayılır.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_CRYPTO_SUCCESS** (0x00) ECDH işlemi başarıyla yürütüldü.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.
- **NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi veya uzunluğu geçersiz.
- **NX_CRYPTO_INVALID_ALGORITHM** (0x20004) geçersiz ECDH algoritması belirtildi.
- **NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) geçersiz çıkış arabelleği boyutu.

## <a name="_nx_crypto_method_ecdh_cleanup"></a>_nx_crypto_method_ecdh_cleanup

ECDH denetim bloğunu temizleyin.

### <a name="prototype"></a>Prototype

```c
UINT _nx_crypto_method_ecdh_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a>Description

Uygulama, bu ECDH oturumu artık gerekli olmadığını belirledikten sonra ECDH denetim bloğunu temizlemek için bu işlevi çağırır.

### <a name="parameters"></a>Parametreler

- **crypto_metadata** *_Nx_crypto_method_ecdh_init ()* içinde kullanılan ECDH denetim bloğuna yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_CRYPTO_SUCCESS** (0x00) ECDH oturumu başarıyla temizlendi.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.

## <a name="_nx_crypto_method_ecdsa_init"></a>_nx_crypto_method_ecdsa_init

ECDSA şifreleme denetim bloğunu başlatır

### <a name="prototype"></a>Prototype

```c
UINT _nx_crypto_method_ecdsa_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size);
```

### <a name="description"></a>Description

Bu işlev, ECDSA denetim bloğunu verilen anahtar dizesiyle başlatır. ECDSA denetim bloğu başlatıldıktan sonra, sonraki ECDSA işlemi aynı denetim bloğunu kullanıyor olacaktır.

Uygulama birden çok ECDSA denetim bloğu oluşturabilir ve her biri bir oturumu temsil eder. ECDSA denetim bloğu başlatılırken yeni bir karma hesaplama oturumu başlatılır. ECDSA denetim bloğu yeniden başlatıldı, geçerli oturumdan vazgeçer ve yeni bir oturum başlar.

### <a name="parameters"></a>Parametreler

- **yöntem** Geçerli bir ECDSA şifreleme yöntemi denetim bloğuna işaretçi. Aşağıdaki önceden tanımlanmış şifreleme yöntemleri kullanılabilir:
  - *crypto_method_ecdsa*
- **anahtar** Bu alan ECDSA için kullanılmaz.
- **key_size_in_bits** Bu alan ECDSA için kullanılmaz.
- **handle (tanıtıcı)** Bu hizmet çağıranın tanıtıcısı döndürür. Tanıtıcı uygulamaya bağımlıdır ve bu uygulamada kullanılmaz. Uygulama tanıtıcı için NULL değerini geçsin.
- **crypto_metadata** ECDSA denetim bloğu için geçerli bir bellek alanı işaretçisi. Bellek alanı başlangıç adresi 4 bayta hizalanmış olması gerekir.
- **crypto_metadata_size** Veri alanı bayt cinsinden crypto_metadata. ECDSA için meta veri boyutunun *sizeof(NX_CRYPTO_ECDSA) olması gerekir*

### <a name="return-values"></a>Dönüş Değerleri

- **NX_CRYPTO_SUCCESS** (0x00) ANAHTAR ve anahtar boyutuyla ECDSA denetim bloğu başarıyla başlatıldı.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) Şifreleme kitaplığı geçersiz durumda ve kullanılamaz.
- **NX_PTR_ERROR** (0x07) Anahtar için geçersiz işaretçi ya da geçersiz crypto_metadata veya crypto_metadata_size veya crypto_metadata 4-byte hizalanmamış.

## <a name="_nx_crypto_method_ecdsa_operation"></a>_nx_crypto_method_ecdsa_operation

ECDSA işlemi gerçekleştirme

### <a name="prototype"></a>Prototype

```c
UINT _nx_crypto_method_ecdsa_operation(UINT op,
    VOID *handle,
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    UCHAR *input,
    ULONG input_length_in_byte,
    UCHAR *iv_ptr,
    UCHAR *output,
    ULONG output_length_in_byte,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size,
    VOID *packet_ptr,
    VOID (*nx_crypto_hw_process_callback)(VOID *packet_ptr, UINT
    status));
```

### <a name="description"></a>Description

Bu işlev ECDSA işlemini gerçekleştirir. ECDSA denetim bloğu _ *nx_crypto_method_ecdsa_init() ile başlatılmış olması gerekir.* Gerçekleştirilecek ECDSA algoritması, yöntem denetim bloğunda belirtilen *algoritmaya* dayalıdır.

İşlem başarısız NX_CRYPTO_EC_CURVE_SET, giriş Üç Nokta Eğrisi şifreleme yönteminin olduğunu ifade eder. İşlem başarısız NX_CRYPTO_EC_KEY_PAIR_GENERATE, çıkış NX_CRYPTO_EXTENDED_OUTPUT ve anahtar çifti nx_crypto_extended_output_data.

### <a name="parameters"></a>Parametreler

- **op (op)** Gerçekleştirecek işlem türü. Geçerli işlem:
  - *NX_CRYPTO_EC_CURVE_SET*
  - *NX_CRYPTO_AUTHENTICATE*
  - *NX_CRYPTO_VERIFY*
- **handle (tanıtıcı)** Bu alan, NetX Şifreleme kitaplığının yazılım uygulamasında kullanılmaz. Geçirilen tüm değerler sessizce yoksayılır.
- **yöntem** Geçerli ECDSA şifreleme yönteminin işaretçisi. Burada kullanılan şifreleme yöntemi _ *nx_crypto_method_ecdsa_init() içinde kullanılanla aynı olması gerekir.*
- **anahtar** İşlem doğru olduğunda anahtarı NX_CRYPTO_VERIFY. Anahtar arabelleğiyle ilgili kısıtlamalar yoktur. Bu alan diğer op değerleri için kullanılmaz.
- **key_size_in_bits** Bit olarak anahtarın boyutu.
- **input (giriş)** İşlem tamam NX_CRYPTO_EC_CURVE_SET, bu alan Eliptik Eğri şifreleme yöntemini ifade ediyor. Aksi takdirde, bu alan giriş metin verilerini içeren bir arabelleği belirtir.
- **input_length_in_byte** Giriş verisi boyutu (bayt cinsinden).
- **iv_ptr** Bu alan ECDSA için kullanılmaz.
- **output (çıktı)** İşlem NX_CRYPTO_EC_CURVE_SET bu alan kullanılmaz. İşlem tamam NX_CRYPTO_AUTHENTICATE, bu alan oluşturulan ECDSA imzası için bellek alanını kullanır. İşlem tamamlandıktan NX_CRYPTO_VERIFY, bu alan doğrulanmış ECDSA imzası için bellek alanını belirtir.
- **output_length_in_byte** Çıkış arabelleğinin bayt cinsinden boyutu.
- **crypto_metadata** _nx_crypto_method_ecdsa_init() içinde kullanılan ECDSA *denetim bloğuna işaretçi.*
- **crypto_metadata_size** Veri alanı bayt cinsinden crypto_metadata. ECDSA için meta veri boyutunun *boyutof(NX_CRYPTO_ECDSA) olması gerekir*
- **packet_ptr** Bu alan, NetX Şifreleme kitaplığının yazılım uygulamasında kullanılmaz. Geçirilen tüm değerler sessizce yoksayılır.
- **nx_crypto_hw_process_callback** Bu alan, NetX Şifreleme kitaplığının yazılım uygulamasında kullanılmaz. Geçirilen tüm değerler sessizce yoksayılır.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_CRYPTO_SUCCESS** (0x00) ECDSA işlemi başarıyla yürütülür.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) Şifreleme kitaplığı geçersiz durumda ve kullanılamaz.
- **NX_PTR_ERROR** (0x07) Geçersiz giriş işaretçisi veya geçersiz uzunluk.
- **NX_CRYPTO_INVALID_ALGORITHM** (0x20004) Geçersiz ECDSA algoritması belirtiliyor.
- **NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) Geçersiz çıkış arabellek boyutu.

## <a name="_nx_crypto_method_ecdsa_cleanup"></a>_nx_crypto_method_ecdsa_cleanup

ECDSA denetim bloğu temizleyin.

### <a name="prototype"></a>Prototype

```c
UINT _nx_crypto_method_ecdsa_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a>Description

Uygulama, bu ECDSA oturumuna artık gerek olmadığını tespit ettikten sonra ECDSA denetim bloğunun temizlenmesi için bu işlevi çağırıyor.

### <a name="parameters"></a>Parametreler

- **crypto_metadata** _nx_crypto_method_ecdsa_init() içinde kullanılan ECDSA *denetim bloğuna işaretçi.*

### <a name="return-values"></a>Dönüş Değerleri

- **NX_CRYPTO_SUCCESS** (0x00) ECDSA oturumu başarıyla temizlendi.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) Şifreleme kitaplığı geçersiz durumda ve kullanılamaz.

## <a name="_nx_crypto_method_hmac_md5_init"></a>_nx_crypto_method_hmac_md5_init

HMAC MD5 şifreleme denetim bloğu başlatılır

### <a name="prototype"></a>Prototype

```c
UINT _nx_crypto_method_hmac_md5_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size);
```

### <a name="description"></a>Description

Bu işlev, HMAC MD5 denetim bloğuna verilen anahtar dizesiyle başlatılır. HMAC MD5 denetim bloğu başlatıldıktan sonra, sonraki HMAC MD5 işlemi aynı denetim bloğu kullanıyor olur.

Uygulama birden çok HMAC MD5 denetim bloğu oluşturabilir ve her biri bir oturumu temsil eder. HMAC MD5 denetim bloğu başlatılırken yeni bir karma hesaplama oturumu başlatılır. HMAC MD5 denetim bloğu yeniden başlatıldı, geçerli oturumdan vazgeçer ve yeni bir oturum sunar.

### <a name="parameters"></a>Parametreler

- **yöntem** Geçerli bir HMAC MD5 şifreleme yöntemi denetim bloğuna işaretçi.
Aşağıdaki önceden tanımlanmış şifreleme yöntemleri kullanılabilir:
  - *crypto_method_hmac_md5*
- **anahtar** anahtarına puanlar. Anahtar arabelleğiyle ilgili kısıtlamalar yoktur.
- **key_size_in_bits** Bit olarak anahtarın boyutu.
- **handle (tanıtıcı)** Bu hizmet çağıranın tanıtıcısı döndürür. Tanıtıcı uygulamaya bağımlıdır ve bu uygulamada kullanılmaz. Uygulama tanıtıcı için NULL değerini geçsin.
- **crypto_metadata** HMAC MD5 denetim bloğu için geçerli bir bellek alanı işaretçisi. Bellek alanı başlangıç adresi 4 bayta hizalanmış olması gerekir.
- **crypto_metadata_size** Veri alanı bayt cinsinden crypto_metadata. HMAC MD5 için meta veri boyutunun *sizeof(NX_CRYPTO_MD5_HMAC) olması gerekir*

### <a name="return-values"></a>Dönüş Değerleri

- **NX_CRYPTO_SUCCESS** (0x00) Anahtar ve anahtar boyutu ile HMAC MD5 denetim bloğu başarıyla başlatıldı.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) Şifreleme kitaplığı geçersiz durumda ve kullanılamaz.
- **NX_PTR_ERROR** (0x07) Anahtar için geçersiz işaretçi ya da geçersiz crypto_metadata veya crypto_metadata_size veya crypto_metadata 4-byte hizalanmamış.

## <a name="_nx_crypto_method_hmac_md5_operation"></a>_nx_crypto_method_hmac_md5_operation

HMAC MD5 karma işlemi gerçekleştirin.

### <a name="prototype"></a>Prototype

```c
UINT _nx_crypto_method_hmac_md5_operation(UINT op,
    VOID *handle,
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    UCHAR *input,
    ULONG input_length_in_byte,
    UCHAR *iv_ptr,
    UCHAR *output,
    ULONG output_length_in_byte,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size,
    VOID *packet_ptr,
    VOID (*nx_crypto_hw_process_callback)(VOID *packet_ptr, UINT
    status));
```

### <a name="description"></a>Description

Bu işlev HMAC MD5 karma işlemini gerçekleştirir. HMAC MD5 denetim bloğu _ *nx_crypto_method_hmac_md5_init() ile başlatılmış olması gerekir.* Gerçekleştirilecek HMAC MD5 algoritması, yöntem denetim bloğunda belirtilen *algoritmaya* dayalıdır.

Son işlem *NX_CRYPTO_HASH_CALCULATE* arabellek boyutu 16 bayt olmalıdır.

Bu işlem durum bilgilerini tutmaz ve HMAC MD5 denetim bloğunda anahtar malzemeyi değiştirmez.

### <a name="parameters"></a>Parametreler

- **op (op)** Gerçekleştirecek işlem türü. Geçerli işlem:
  - *NX_CRYPTO_HASH_INITIALIZE*
  - *NX_CRYPTO_HASH_UPDATE*
  - *NX_CRYPTO_HASH_CALCULATE*
- **handle (tanıtıcı)** Bu alan, NetX Şifreleme kitaplığının yazılım uygulamasında kullanılmaz. Geçirilen tüm değerler sessizce yoksayılır.
- **yöntem** Geçerli HMAC MD5 şifreleme yönteminin işaretçisi. Burada kullanılan şifreleme yöntemi, *nx_crypto_method_hmac_md5_init() içinde de aynı şekilde kullanılmalıdır.*
- **anahtar** anahtarına puanlar. Anahtar arabelleğiyle ilgili kısıtlamalar yoktur.
- **key_size_in_bits** Bit olarak anahtarın boyutu.
- **input_data** Giriş metin verilerini içeren bir arabelleği belirtir. Giriş arabelleğiyle ilgili bir kısıtlama yoktur.
- **input_data_size** Giriş verisi boyutu (bayt cinsinden).
- **iv_ptr** Bu alan HMAC MD5 için kullanılmaz.
- **iv_size** Bu alan HMAC MD5 için kullanılmaz.
- **output_buffer** Oluşturulan HMAC MD5 karması için bellek alanına işaretçi.
- **output_buffer_size** Çıkış arabelleğinin bayt cinsinden boyutu.
- **crypto_metadata** _nx_crypto_method_hmac_md5_init() içinde kullanılan HMAC MD5 *denetim bloğuna işaretçi.*
- **crypto_metadata_size** Veri alanı bayt cinsinden crypto_metadata. HMAC MD5 için meta veri boyutunun *boyutof(NX_CRYPTO_MD5_HMAC) olması gerekir*
- **packet_ptr** Bu alan, NetX Şifreleme kitaplığının yazılım uygulamasında kullanılmaz. Geçirilen tüm değerler sessizce yoksayılır.
- **nx_crypto_hw_process_callback** Bu alan, NetX Şifreleme kitaplığının yazılım uygulamasında kullanılmaz. Geçirilen tüm değerler sessizce yoksayılır.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_CRYPTO_SUCCESS** (0x00) HMAC MD5 işlemi başarıyla yürütülür.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) Şifreleme kitaplığı geçersiz durumda ve kullanılamaz.
- **NX_PTR_ERROR** (0x07) Geçersiz giriş işaretçisi veya geçersiz uzunluk.
- **NX_CRYPTO_INVALID_ALGORITHM** (0x20004) Geçersiz HMAC MD5 algoritması belirtiliyor.
- **NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) Geçersiz çıkış arabellek boyutu.

## <a name="_nx_crypto_method_hmac_sha1_init"></a>_nx_crypto_method_hmac_sha1_init

HMAC SHA1 şifreleme denetim bloğu başlatılır

### <a name="prototype"></a>Prototype

```c
UINT _nx_crypto_method_hmac_sha1_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size);
```

### <a name="description"></a>Description

Bu işlev, HMAC SHA1 denetim bloğuna verilen anahtar dizesiyle başlatılır. HMAC SHA1 denetim bloğu başlatıldıktan sonra, sonraki HMAC SHA1 işlemi aynı denetim bloğu kullanıyor olur.

Uygulama birden çok HMAC SHA1 denetim bloğu oluşturabilir ve her biri bir oturumu temsil eder. HMAC SHA1 denetim bloğu başlatılırken yeni bir karma hesaplama oturumu başlatılır. HMAC SHA1 denetim bloğu yeniden başlatıla, geçerli oturumdan vazgeçer ve yeni bir oturum sunar.

### <a name="parameters"></a>Parametreler

- **yöntem** Geçerli bir HMAC SHA1 şifreleme yöntemi denetim bloğuna işaretçi. Aşağıdaki önceden tanımlanmış şifreleme yöntemleri kullanılabilir:
  - *crypto_method_hmac_sha1*
- **anahtar** anahtarına puanlar. Anahtar arabelleğiyle ilgili kısıtlamalar yoktur.
- **key_size_in_bits** Bit olarak anahtarın boyutu.
- **handle (tanıtıcı)** Bu hizmet çağıranın tanıtıcısı döndürür. Tanıtıcı uygulamaya bağımlıdır ve bu uygulamada kullanılmaz. Uygulama tanıtıcı için NULL değerini geçsin.
- **crypto_metadata** HMAC SHA1 denetim bloğu için geçerli bir bellek alanı işaretçisi. Bellek alanı başlangıç adresi 4 bayta hizalanmış olması gerekir.
- **crypto_metadata_size** Veri alanı bayt cinsinden crypto_metadata. HMAC SHA1 için meta veri boyutu *boyutof(NX_CRYPTO_SHA1_HMAC)*

### <a name="return-values"></a>Dönüş Değerleri

- **NX_CRYPTO_SUCCESS** (0x00) Anahtar ve anahtar boyutu ile HMAC SHA1control bloğu başarıyla başlatılacak.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) Şifreleme kitaplığı geçersiz durumda ve kullanılamaz.
- **NX_PTR_ERROR** (0x07) Anahtar için geçersiz işaretçi ya da geçersiz crypto_metadata veya crypto_metadata_size veya crypto_metadata 4-byte hizalanmamış.

## <a name="_nx_crypto_method_hmac_sha1_operation"></a>_nx_crypto_method_hmac_sha1_operation

HMAC SHA1 karma işlemi gerçekleştirme

### <a name="prototype"></a>Prototype

```c
UINT _nx_crypto_method_hmac_sha1_operation(UINT op,
    VOID *handle,
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    UCHAR *input,
    ULONG input_length_in_byte,
    UCHAR *iv_ptr,
    UCHAR *output,
    ULONG output_length_in_byte,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size,
    VOID *packet_ptr,
    VOID (*nx_crypto_hw_process_callback)(VOID *packet_ptr, UINT
    status));
```

### <a name="description"></a>Description

Bu işlev HMAC SHA1 karma işlemini gerçekleştirir. HMAC SHA1 denetim bloğu _ *nx_crypto_method_hmac_sha1_init() ile başlatılmış olması gerekir.* Gerçekleştirilecek HMAC SHA1 algoritması, yöntem denetim bloğunda belirtilen *algoritmaya* dayalıdır.

Son işlem *NX_CRYPTO_HASH_CALCULATE* arabellek boyutu 20 bayt olmalıdır.

### <a name="parameters"></a>Parametreler

- **op (op)** Gerçekleştirecek işlem türü. Geçerli işlem:
  - *NX_CRYPTO_HASH_INITIALIZE*
  - *NX_CRYPTO_HASH_UPDATE*
  - *NX_CRYPTO_HASH_CALCULATE*
- **handle (tanıtıcı)** Bu alan, NetX Şifreleme kitaplığının yazılım uygulamasında kullanılmaz. Geçirilen tüm değerler sessizce yoksayılır.
- **yöntem** Geçerli HMAC SHA1 şifreleme yönteminin işaretçisi. Burada kullanılan şifreleme yöntemi, _ *nx_crypto_method_hmac_sha1_init() içinde kullanılanla aynı olması gerekir.*
- **anahtar** anahtarına puanlar. Anahtar arabelleğiyle ilgili kısıtlamalar yoktur.
- **key_size_in_bits** Bit olarak anahtarın boyutu.
- **input_data** Giriş metin verilerini içeren bir arabelleği belirtir. Giriş arabelleğiyle ilgili bir kısıtlama yoktur.
- **input_data_size** Giriş verisi boyutu (bayt cinsinden).
- **iv_ptr** Bu alan HMAC SHA1 için kullanılmaz.
- **iv_size** Bu alan HMAC SHA1 için kullanılmaz.
- **output_buffer** Oluşturulan HMAC SHA1 karması için bellek alanına işaretçi.
- **output_buffer_size** Çıkış arabelleğinin bayt cinsinden boyutu.
- **crypto_metadata** _nx_crypto_method_hmac_sha1_init() içinde kullanılan HMAC SHA1 *denetim bloğuna işaretçi.*
- **crypto_metadata_size** Veri alanı bayt cinsinden crypto_metadata. HMAC SHA1 için, meta veri boyutu *sizeof olmalıdır (NX_CRYPTO_SHA1_HMAC)*
- **packet_ptr** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz. Geçirilen tüm değerler sessizce yok sayılır.
- **nx_crypto_hw_process_callback** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz. Geçirilen tüm değerler sessizce yok sayılır.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_CRYPTO_SUCCESS** (0x00) HMAC SHA1 işlemini başarıyla yürütüldü.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.
- **NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi veya uzunluğu geçersiz.
- **NX_CRYPTO_INVALID_ALGORITHM** (0x20004) GEÇERSIZ HMAC SHA1 algoritması belirtildi.
- **NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) geçersiz çıkış arabelleği boyutu.

## <a name="_nx_crypto_method_hmac_sha1_cleanup"></a>_nx_crypto_method_hmac_sha1_cleanup

HMAC SHA1 denetim bloğunu temizleyin.

### <a name="prototype"></a>Prototype

```c
UINT _nx_crypto_method_hmac_sha1_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a>Description

Uygulama bu HMAC SHA1 denetim bloğunu, bu HMAC SHA1 oturumunun artık gerekli olmadığını belirledikten sonra temizlemek için bu işlevi çağırır.

### <a name="parameters"></a>Parametreler

- **crypto_metadata** *_Nx_crypto_method_hmac_sha1_init ()* IÇINDE kullanılan HMAC SHA1 denetim bloğuna yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_CRYPTO_SUCCESS** (0x00) HMAC SHA1 oturumunun başarıyla temizlendi.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.

## <a name="_nx_crypto_method_hmac_sha256_init"></a>_nx_crypto_method_hmac_sha256_init

HMAC SHA256 şifre denetim bloğunu başlatır

### <a name="prototype"></a>Prototype

```c
UINT _nx_crypto_method_hmac_sha256_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size);
```

### <a name="description"></a>Description

Bu işlev, HMAC SHA256 denetim bloğunu verilen anahtar dizesiyle başlatır. HMAC SHA256 denetim bloğu başlatıldıktan sonra, sonraki HMAC SHA256 işlemi aynı denetim bloğunu kullanıyor olacaktır.

Uygulama birden çok HMAC SHA256 denetim bloğu oluşturabilir, her biri bir oturumu temsil eder. HMAC SH256 denetim bloğunun başlatılması yeni bir karma hesaplama oturumu başlatır. HMAC SHA256 denetim bloğunu yeniden başlatmak, geçerli oturum ve yıldızların yeni bir anahtarla yeni bir anahtarla bir yenisini terk edin.

### <a name="parameters"></a>Parametreler

- **yöntemi** Geçerli bir HMAC SHA256 şifreleme yöntemi denetim bloğuna işaretçi. Aşağıdaki önceden tanımlanmış şifreleme yöntemleri kullanılabilir:
  - *crypto_method_hmac_sha224*
  - *crypto_method_hmac_sha256*
- **anahtar** Anahtarı işaret eder. Anahtar arabelleğinde kısıtlama yoktur.
- **key_size_in_bits** Anahtarın bit cinsinden boyutu.
- **tanıtıcı** Bu hizmet, çağırana bir tanıtıcı döndürür. Tanıtıcı uygulamaya bağımlıdır ve bu uygulamada kullanılmıyor. Uygulama tanıtıcı için NULL değer geçirecektir.
- **crypto_metadata** HMAC SHA256 denetim bloğu için geçerli bir bellek alanı işaretçisi. Bellek alanının başlangıç adresi 4 bayt hizalı olmalıdır.
- **crypto_metadata_size** Crypto_metadata alanının bayt cinsinden boyutu. HMAC SHA256 için meta veri boyutu *sizeof olmalıdır (NX_CRYTPO_SHA256_HMAC)*

### <a name="return-values"></a>Dönüş Değerleri

- **NX_CRYPTO_SUCCESS** (0x00) anahtar ve anahtar boyutuyla HMAC SHA256 denetim bloğunun başarıyla başlatılması.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.
- **NX_PTR_ERROR** (0x07) anahtar için geçersiz işaretçi veya geçersiz crypto_metadata veya crypto_metadata_size ya da crypto_metadata 4 bayt hizalı değil.

## <a name="_nx_crypto_method_hmac_sha256_operation"></a>_nx_crypto_method_hmac_sha256_operation

HMAC SHA256 karma işlemi gerçekleştir

### <a name="prototype"></a>Prototype

```c
UINT _nx_crypto_method_hmac_sha256_operation(UINT op,
    VOID *handle,
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    UCHAR *input,
    ULONG input_length_in_byte,
    UCHAR *iv_ptr,
    UCHAR *output,
    ULONG output_length_in_byte,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size,
    VOID *packet_ptr,
    VOID (*nx_crypto_hw_process_callback)(VOID *packet_ptr, UINT
    status));
```

### <a name="description"></a>Description

Bu işlev HMAC SHA256 karma işlemi gerçekleştirir. HMAC SHA256 denetim bloğu _ *nx_crypto_method_hmac_sha256_init ()* ile başlatılmış olmalıdır. Gerçekleştirilecek HMAC SHA256 algoritması, *Yöntem* denetim bloğunda belirtilen algoritmayı temel alır.

Son *NX_CRYPTO_HASH_CALCULATE* işlemi için, çıkış ARABELLEĞI boyutu SHA256 için 32 bayt veya SHA224 için 28 bayt olmalıdır.

### <a name="parameters"></a>Parametreler

- **op** Gerçekleştirilecek işlemin türü. Geçerli işlem:
  - *NX_CRYPTO_HASH_INITIALIZE*
  - *NX_CRYPTO_HASH_UPDATE*
  - *NX_CRYPTO_HASH_CALCULATE*
- **tanıtıcı** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz. Geçirilen tüm değerler sessizce yok sayılır.
- **yöntemi** Geçerli HMAC SHA256 şifre yöntemine yönelik işaretçi. Burada kullanılan şifreleme yöntemi _ *nx_crypto_method_hmac_sha256_init ()* içinde kullanılan aynı olmalıdır.
- **anahtar** Anahtarı işaret eder. Anahtar arabelleğinde kısıtlama yoktur.
- **key_size_in_bits** Anahtarın bit cinsinden boyutu.
- **input_data** Girdi metin verileri içeren bir arabelleğe işaret eder. Giriş arabelleğinde kısıtlama yoktur.
- **input_data_size** Giriş verilerinin bayt cinsinden boyutu.
- **iv_ptr** Bu alan HMAC SHA256 için kullanılmaz.
- **iv_size** Bu alan HMAC SHA256 için kullanılmaz.
- **output_buffer** Oluşturulan HMAC SHA256 karması için bellek alanına yönelik işaretçi.
- **output_buffer_size** Çıkış arabelleğinin bayt cinsinden boyutu.
- **crypto_metadata** *_Nx_crypto_method_hmac_sha256_init ()* IÇINDE kullanılan HMAC SHA256 denetim bloğuna yönelik işaretçi.
- **crypto_metadata_size** Crypto_metadata alanının bayt cinsinden boyutu. HMAC SHA256 için meta veri boyutu sizeof olmalıdır *(NX_CRYPTO_SHA256_HMAC)*
- **packet_ptr** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz. Geçirilen tüm değerler sessizce yok sayılır.
- **nx_crypto_hw_process_callback** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz. Geçirilen tüm değerler sessizce yok sayılır.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_CRYPTO_SUCCESS** (0x00) HMAC SHA256 işlemini başarıyla yürütüldü.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.
- **NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi veya uzunluğu geçersiz.
- **NX_CRYPTO_INVALID_ALGORITHM** (0x20004) GEÇERSIZ HMAC SHA256 algoritması belirtildi.
- **NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) geçersiz çıkış arabelleği boyutu.

## <a name="_nx_crypto_method_hmac_sha256_cleanup"></a>_nx_crypto_method_hmac_sha256_cleanup

HMAC SHA256 denetim bloğunu temizleyin.

### <a name="prototype"></a>Prototype

```c
UINT _nx_crypto_method_hmac_sha256_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a>Description

Uygulama, bu HMAC SHA256 oturumunun artık gerekli olmadığını belirlediğinde HMAC SHA256 denetim bloğunu temizlemek için bu işlevi çağırır.

### <a name="parameters"></a>Parametreler

- **crypto_metadata** *_Nx_crypto_method_hmac_sha256_init ()* IÇINDE kullanılan HMAC SHA256 denetim bloğuna yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_CRYPTO_SUCCESS** (0x00) HMAC SHA256 oturumu başarıyla temizlendi.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.

## <a name="_nx_crypto_method_hmac_sha512_init"></a>_nx_crypto_method_hmac_sha512_init

HMAC SHA512 olur şifre denetim bloğunu başlatır

### <a name="prototype"></a>Prototype

```c
UINT _nx_crypto_method_hmac_sha512_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size);
```

### <a name="description"></a>Description

Bu işlev, HMAC SHA512 olur denetim bloğunu verilen anahtar dizesiyle başlatır. HMAC SHA512 olur denetim bloğu başlatıldıktan sonra, sonraki HMAC SHA512 olur işlemi aynı denetim bloğunu kullanıyor olacaktır.

Uygulama birden çok HMAC SHA512 olur denetim bloğu oluşturabilir, her biri bir oturumu temsil eder. HMAC SH512 denetim bloğunun başlatılması yeni bir karma hesaplama oturumu başlatır. HMAC SHA512 olur denetim bloğunu yeniden başlatmak, geçerli oturum ve yıldızların yeni bir anahtarla yeni bir anahtarla bir yenisini terk edin.

### <a name="parameters"></a>Parametreler

- **yöntemi** Geçerli bir HMAC SHA512 olur şifreleme yöntemi denetim bloğuna işaretçi. Aşağıdaki önceden tanımlanmış şifreleme yöntemleri kullanılabilir:
  - *crypto_method_hmac_sha384*
  - *crypto_method_hmac_sha512*
- **anahtar** Anahtarı işaret eder. Anahtar arabelleğinde kısıtlama yoktur.
- **key_size_in_bits** Anahtarın bit cinsinden boyutu.
- **tanıtıcı** Bu hizmet, çağırana bir tanıtıcı döndürür. Tanıtıcı uygulamaya bağımlıdır ve bu uygulamada kullanılmıyor. Uygulama tanıtıcı için NULL değer geçirecektir.
- **crypto_metadata** HMAC SHA512 olur denetim bloğu için geçerli bir bellek alanı işaretçisi. Bellek alanının başlangıç adresi 4 bayt hizalı olmalıdır.
- **crypto_metadata_size** Crypto_metadata alanının bayt cinsinden boyutu. HMAC SHA512 olur için meta veri boyutu *sizeof olmalıdır (NX_CRYPTO_SHA512_HMAC)*

### <a name="return-values"></a>Dönüş Değerleri

- **NX_CRYPTO_SUCCESS** (0x00) anahtar ve anahtar boyutuyla HMAC SHA512 olur denetim bloğunun başarıyla başlatılması.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.
- **NX_PTR_ERROR** (0x07) anahtar için geçersiz işaretçi veya geçersiz crypto_metadata veya crypto_metadata_size ya da crypto_metadata 4 bayt hizalı değil.

## <a name="_nx_crypto_method_hmac_sha512_operation"></a>_nx_crypto_method_hmac_sha512_operation

HMAC SHA512 olur karma işlemi gerçekleştir

### <a name="prototype"></a>Prototype

```c
UINT _nx_crypto_method_hmac_sha512_operation(UINT op,
    VOID *handle,
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    UCHAR *input,
    ULONG input_length_in_byte,
    UCHAR *iv_ptr,
    UCHAR *output,
    ULONG output_length_in_byte,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size,
    VOID *packet_ptr,
    VOID (*nx_crypto_hw_process_callback)(VOID *packet_ptr, UINT
    status));
```

### <a name="description"></a>Description

Bu işlev HMAC SHA512 olur karma işlemi gerçekleştirir. HMAC SHA512 olur denetim bloğu _ *nx_crypto_method_hmac_sha512_init ()* ile başlatılmış olmalıdır. Gerçekleştirilecek HMAC SHA512 olur algoritması, *Yöntem* denetim bloğunda belirtilen algoritmayı temel alır.

Son *NX_CRYPTO_HASH_CALCULATE* işlemi için, çıkış ARABELLEĞI boyutu sha512 olur için 64 bayt veya SHA384 için 48 bayt olmalıdır.

### <a name="parameters"></a>Parametreler

- **op** Gerçekleştirilecek işlemin türü. Geçerli işlem:
  - *NX_CRYPTO_HASH_INITIALIZE*
  - *NX_CRYPTO_HASH_UPDATE*
  - *NX_CRYPTO_HASH_CALCULATE*
- **tanıtıcı** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz. Geçirilen tüm değerler sessizce yok sayılır.
- **yöntemi** Geçerli HMAC SHA512 olur şifre yöntemine yönelik işaretçi. Burada kullanılan şifreleme yöntemi _ *nx_crypto_method_hmac_sha512_init ()* içinde kullanılan aynı olmalıdır.
- **anahtar** Anahtarı işaret eder. Anahtar arabelleğinde kısıtlama yoktur.
- **key_size_in_bits** Anahtarın bit cinsinden boyutu.
- **input_data** Girdi metin verileri içeren bir arabelleğe işaret eder. Giriş arabelleğinde kısıtlama yoktur.
- **input_data_size** Giriş verilerinin bayt cinsinden boyutu.
- **iv_ptr** Bu alan HMAC SHA512 olur için kullanılmaz.
- **iv_size** Bu alan HMAC SHA512 olur için kullanılmaz.
- **output_buffer** Oluşturulan HMAC SHA512 olur karması için bellek alanına yönelik işaretçi.
- **output_buffer_size** Çıkış arabelleğinin bayt cinsinden boyutu.
- **crypto_metadata** *_Nx_crypto_method_hmac_sha512_init ()* IÇINDE kullanılan HMAC SHA512 olur denetim bloğuna yönelik işaretçi.
- **crypto_metadata_size** Crypto_metadata alanının bayt cinsinden boyutu. HMAC SHA512 olur için meta veri boyutu sizeof olmalıdır *(NX_CRYPTO_SHA512_HMAC)*
- **packet_ptr** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz. Geçirilen tüm değerler sessizce yok sayılır.
- **nx_crypto_hw_process_callback** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz. Geçirilen tüm değerler sessizce yok sayılır.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_CRYPTO_SUCCESS** (0x00) HMAC SHA512 olur işlemini başarıyla yürütüldü.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.
- **NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi veya uzunluğu geçersiz.
- **NX_CRYPTO_INVALID_ALGORITHM** (0x20004) GEÇERSIZ HMAC SHA512 olur algoritması belirtildi.
- **NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) geçersiz çıkış arabelleği boyutu.

## <a name="_nx_crypto_method_hmac_sha512_cleanup"></a>_nx_crypto_method_hmac_sha512_cleanup

HMAC SHA512 olur denetim bloğunu temizleyin.

### <a name="prototype"></a>Prototype

```c
UINT _nx_crypto_method_hmac_sha512_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a>Description

Uygulama, bu HMAC SHA512 olur oturumunun artık gerekli olmadığını belirlediğinde HMAC SHA512 olur denetim bloğunu temizlemek için bu işlevi çağırır.

### <a name="parameters"></a>Parametreler

- **crypto_metadata** *_Nx_crypto_method_hmac_sha512_init ()* IÇINDE kullanılan HMAC SHA512 olur denetim bloğuna yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_CRYPTO_SUCCESS** (0x00) HMAC SHA512 olur oturumu başarıyla temizlendi.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.

### <a name="example"></a>Örnek 

## <a name="_nx_crypto_method_md5_init"></a>_nx_crypto_method_md5_init

MD5 şifreleme denetim bloğunu başlatır

### <a name="prototype"></a>Prototype

```c
UINT _nx_crypto_method_md5_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size);
```

### <a name="description"></a>Description

Bu işlev, MD5 denetim bloğunu verilen anahtar dizesiyle başlatır. MD5 denetim bloğu başlatıldıktan sonra, sonraki MD5 işlemi aynı denetim bloğunu kullanıyor olacaktır.

Uygulama birden çok MD5 denetim bloğu oluşturabilir, her biri bir oturumu temsil eder. MD5 denetim bloğunun başlatılması yeni bir karma hesaplama oturumu başlatır. MD5 denetim bloğunu yeniden başlatmak, geçerli oturumu ve yıldızları yeni bir kez geri başlatmakta.

### <a name="parameters"></a>Parametreler

- **yöntemi** Geçerli bir MD5 şifreleme yöntemi denetim bloğuna yönelik işaretçi. Aşağıdaki önceden tanımlanmış şifreleme yöntemleri kullanılabilir:
  - *crypto_method_md5*
- **anahtar** Bu alan MD5 için kullanılmaz.
- **key_size_in_bits** Bu alan MD5 için kullanılmıyor
- **tanıtıcı** Bu hizmet, çağırana bir tanıtıcı döndürür. Tanıtıcı uygulamaya bağımlıdır ve bu uygulamada kullanılmıyor. Uygulama tanıtıcı için NULL değer geçirecektir.
- **crypto_metadata** MD5 denetim bloğu için geçerli bir bellek alanı işaretçisi. Bellek alanının başlangıç adresi 4 bayt hizalı olmalıdır.
- **crypto_metadata_size** Crypto_metadata alanının bayt cinsinden boyutu. MD5 için meta veri boyutu *sizeof olmalıdır (NX_CRYPTO_MD5)*

### <a name="return-values"></a>Dönüş Değerleri

- Anahtar ve anahtar boyutuyla, MD5 denetim bloğunun başarılı bir şekilde başlatılması **NX_CRYPTO_SUCCESS** (0x00).
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.
- **NX_PTR_ERROR** (0x07) anahtar için geçersiz işaretçi veya geçersiz crypto_metadata veya crypto_metadata_size ya da crypto_metadata 4 bayt hizalı değil.

### <a name="example"></a>Örnek

## <a name="_nx_crypto_method_md5_operation"></a>_nx_crypto_method_md5_operation

MD5 karma işlemi gerçekleştirin.

### <a name="prototype"></a>Prototype

```c
UINT _nx_crypto_method_md5_operation(UINT op,
    VOID *handle,
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    UCHAR *input,
    ULONG input_length_in_byte,
    UCHAR *iv_ptr,
    UCHAR *output,
    ULONG output_length_in_byte,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size,
    VOID *packet_ptr,
    VOID (*nx_crypto_hw_process_callback)(VOID *packet_ptr, UINT
    status));
```

### <a name="description"></a>Description

Bu işlev, MD5 karma işlemini gerçekleştirir. MD5 denetim bloğunun _ *nx_crypto_method_md5_init ()* ile başlatılmış olması gerekir. Gerçekleştirilecek MD5 algoritması, *Yöntem* denetim bloğunda belirtilen algoritmayı temel alır.

Son *NX_CRYPTO_HASH_CALCULATE* işlemi için, çıkış arabelleği boyutu 16 bayt olmalıdır.

Bu işlem durum bilgilerini tutar ve MD5 denetim bloğunda anahtar malzemesini değiştirmez.

### <a name="parameters"></a>Parametreler

- **op** Gerçekleştirilecek işlemin türü. Geçerli işlem:
  - *NX_CRYPTO_HASH_INITIALIZE*
  - *NX_CRYPTO_HASH_UPDATE*
  - *NX_CRYPTO_HASH_CALCULATE*
- **tanıtıcı** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz. Geçirilen tüm değerler sessizce yok sayılır.
- **yöntemi** Geçerli MD5 şifreleme yöntemine yönelik işaretçi. Burada kullanılan şifreleme yöntemi _ *nx_crypto_method_md5_init ()* içinde kullanılan aynı olmalıdır.
- **input_data** Girdi metin verileri içeren bir arabelleğe işaret eder. Giriş arabelleğinde kısıtlama yoktur.
- **input_data_size** Giriş verilerinin bayt cinsinden boyutu.
- **iv_ptr** Bu alan MD5 için kullanılmaz.
- **iv_size** Bu alan MD5 için kullanılmaz.
- **output_buffer** Oluşturulan MD5 karması için bellek alanına yönelik işaretçi.
- **output_buffer_size** Çıkış arabelleğinin bayt cinsinden boyutu. MD5 için arabellek boyutu 16 bayt olmalıdır.
- **crypto_metadata** *_Nx_crypto_method_md5_init ()* IÇINDE kullanılan MD5 denetim bloğuna yönelik işaretçi.
- **crypto_metadata_size** Crypto_metadata alanının bayt cinsinden boyutu. MD5 için meta veri boyutu *sizeof (NX_CRYPTO_MD5)* olmalıdır
- **packet_ptr** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz. Geçirilen tüm değerler sessizce yok sayılır.
- **nx_crypto_hw_process_callback** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz. Geçirilen tüm değerler sessizce yok sayılır.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_CRYPTO_SUCCESS** (0x00), MD5 işlemini başarıyla yürütüldü.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.
- **NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi veya uzunluğu geçersiz.
- **NX_CRYPTO_INVALID_ALGORITHM** (0x20004) geçersiz MD5 algoritması belirtildi.
- **NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) geçersiz çıkış arabelleği boyutu.

## <a name="_nx_crypto_method_md5_cleanup"></a>_nx_crypto_method_md5_cleanup

MD5 denetim bloğunu temizleyin.

### <a name="prototype"></a>Prototype

```c
UINT _nx_crypto_method_md5_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a>Description

Uygulama, MD5 denetim bloğunu, bu MD5 oturumunun artık gerekli olmadığını belirledikten sonra temizlemek için bu işlevi çağırır.

### <a name="parameters"></a>Parametreler

- **crypto_metadata** *_Nx_crypto_method_md5_init ()* IÇINDE kullanılan MD5 denetim bloğuna yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_CRYPTO_SUCCESS** (0x00) MD5 oturumu başarıyla temizlendi.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.

## <a name="_nx_crypto_method_sha1_init"></a>_nx_crypto_method_sha1_init

SHA1 şifreleme denetim bloğunu başlatır

### <a name="prototype"></a>Prototype

```c
UINT _nx_crypto_method_sha1_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size);
```

### <a name="description"></a>Description

Bu işlev, SHA1 denetim bloğunu verilen anahtar dizesiyle başlatır. SHA1 denetim bloğu başlatıldıktan sonra, sonraki SHA1 işlemi aynı denetim bloğunu kullanıyor olacaktır.

Uygulama birden çok SHA1 denetim bloğu oluşturabilir, her biri bir oturumu temsil eder. SHA1 denetim bloğunu başlatmak yeni bir karma hesaplama oturumu başlatır. SHA1 denetim bloğunu yeniden başlatmak, geçerli oturumu ve yıldızları yeni bir kez terk.

### <a name="parameters"></a>Parametreler

- **yöntemi** Geçerli bir SHA1 şifreleme yöntemi denetim bloğuna işaretçi. Aşağıdaki önceden tanımlanmış şifreleme yöntemleri kullanılabilir:
  - *crypto_method_sha1*
- **anahtar** Bu alan SHA1 için kullanılmaz.
- **key_size_in_bits** Bu alan SHA1 için kullanılmaz
- **tanıtıcı** Bu hizmet, çağırana bir tanıtıcı döndürür. Tanıtıcı uygulamaya bağımlıdır ve bu uygulamada kullanılmıyor. Uygulama tanıtıcı için NULL değer geçirecektir.
- **crypto_metadata** SHA1 denetim bloğu için geçerli bir bellek alanı işaretçisi. Bellek alanının başlangıç adresi 4 bayt hizalı olmalıdır.
- **crypto_metadata_size** Crypto_metadata alanının bayt cinsinden boyutu. SHA1 için meta veri boyutu *sizeof olmalıdır (NX_CRYPTO_SHA1)*

### <a name="return-values"></a>Dönüş Değerleri

- Anahtar ve anahtar boyutuyla SHA1control bloğunun başarıyla başlatılması **NX_CRYPTO_SUCCESS** (0x00).
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.
- **NX_PTR_ERROR** (0x07) anahtar için geçersiz işaretçi veya geçersiz crypto_metadata veya crypto_metadata_size ya da crypto_metadata 4 bayt hizalı değil.

## <a name="_nx_crypto_method_sha1_operation"></a>_nx_crypto_method_sha1_operation

SHA1 karma işlemi gerçekleştir

### <a name="prototype"></a>Prototype

```c
UINT _nx_crypto_method_sha1_operation(UINT op,
    VOID *handle,
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    UCHAR *input,
    ULONG input_length_in_byte,
    UCHAR *iv_ptr,
    UCHAR *output,
    ULONG output_length_in_byte,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size,
    VOID *packet_ptr,
    VOID (*nx_crypto_hw_process_callback)(VOID *packet_ptr, UINT
    status));
```

### <a name="description"></a>Description

Bu işlev, SHA1 karma işlemini gerçekleştirir. SHA1 denetim bloğunun _ *nx_crypto_method_sha1_init ()* ile başlatılmış olması gerekir. Gerçekleştirilecek SHA1 algoritması, *Yöntem* denetim bloğunda belirtilen algoritmayı temel alır.

Son *NX_CRYPTO_HASH_CALCULATE* işlemi için, çıkış arabelleği boyutu 20 bayt olmalıdır.

### <a name="parameters"></a>Parametreler

- **op** Gerçekleştirilecek işlemin türü. Geçerli işlem:
  - *NX_CRYPTO_HASH_INITIALIZE*
  - *NX_CRYPTO_HASH_UPDATE*
  - *NX_CRYPTO_HASH_CALCULATE*
- **tanıtıcı** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz. Geçirilen tüm değerler sessizce yok sayılır.
- **yöntemi** Geçerli SHA1 şifreleme yöntemine yönelik işaretçi. Burada kullanılan şifreleme yöntemi, *nx_crypto_method_sha1_init() içinde aynı şekilde kullanılmalıdır.*
- **input_data** Giriş metin verilerini içeren bir arabelleği belirtir. Giriş arabelleğiyle ilgili bir kısıtlama yoktur.
- **input_data_size** Giriş verisi boyutu (bayt cinsinden).
- **iv_ptr** Bu alan SHA1 için kullanılmaz.
- **iv_size** Bu alan SHA1 için kullanılmaz.
- **output_buffer** Oluşturulan SHA1 karması için bellek alanına işaretçi.
- **output_buffer_size** Çıkış arabelleğinin bayt cinsinden boyutu. SHA1 için arabellek boyutu 20 bayt olmalıdır.
- **crypto_metadata** _nx_crypto_method_sha1_init() içinde kullanılan SHA1 *denetim bloğuna işaretçi.*
- **crypto_metadata_size** Veri alanı bayt cinsinden crypto_metadata. SHA1 için meta veri boyutunun *boyutof(NX_CRYPTO_SHA1) olması gerekir*
- **packet_ptr** Bu alan, NetX Şifreleme kitaplığının yazılım uygulamasında kullanılmaz. Geçirilen tüm değerler sessizce yoksayılır.
- **nx_crypto_hw_process_callback** Bu alan, NetX Şifreleme kitaplığının yazılım uygulamasında kullanılmaz. Geçirilen tüm değerler sessizce yoksayılır.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_CRYPTO_SUCCESS** (0x00) SHA1 işlemi başarıyla yürütülür.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) Şifreleme kitaplığı geçersiz durumda ve kullanılamaz.
- **NX_PTR_ERROR** (0x07) Geçersiz giriş işaretçisi veya geçersiz uzunluk.
- **NX_CRYPTO_INVALID_ALGORITHM** (0x20004) Geçersiz SHA1 algoritması belirtiliyor.
- **NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) Geçersiz çıkış arabellek boyutu.

### <a name="example"></a>Örnek

## <a name="_nx_crypto_method_sha1_cleanup"></a>_nx_crypto_method_sha1_cleanup

SHA1 denetim bloğu temizleme.

### <a name="prototype"></a>Prototype

```c
UINT _nx_crypto_method_sha1_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a>Description

Uygulama, bu SHA1 oturumunun artık gerekli olmadığını tespit ettikten sonra SHA1 denetim bloğunun temizlenmesi için bu işlevi çağırıyor.

### <a name="parameters"></a>Parametreler

- **crypto_metadata** _nx_crypto_method_sha1_init() içinde kullanılan SHA1 *denetim bloğuna işaretçi.*

### <a name="return-values"></a>Dönüş Değerleri

- **NX_CRYPTO_SUCCESS** (0x00) SHA1 oturumu başarıyla temizlendi.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) Şifreleme kitaplığı geçersiz durumda ve kullanılamaz.

## <a name="_nx_crypto_method_sha256_init"></a>_nx_crypto_method_sha256_init

SHA256 şifreleme denetim bloğu başlatılır

### <a name="prototype"></a>Prototype

```c
UINT _nx_crypto_method_sha256_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size)
```

### <a name="description"></a>Description

Bu işlev, SHA256 denetim bloğuna verilen anahtar dizesiyle başlatılır. SHA256 denetim bloğu başlatıldıktan sonra, sonraki SHA256 işlemi aynı denetim bloğu kullanıyor olur.

Uygulama birden çok SHA256 denetim bloğu oluşturabilir ve her biri bir oturumu temsil eder. SHA256 denetim bloğu başlatılırken yeni bir karma hesaplama oturumu başlatılır. SHA256 denetim bloğu yeniden başlatıla, geçerli oturumdan vazgeçer ve yeni bir oturum sağlar.

### <a name="parameters"></a>Parametreler

- **yöntem** Geçerli bir SHA256 şifreleme yöntemi denetim bloğuna işaretçi. Aşağıdaki önceden tanımlanmış şifreleme yöntemleri kullanılabilir:
  - *crypto_method_sha256*
  - *crypto_method_sha224*
- **anahtar** Bu alan SHA256 için kullanılmaz.
- **key_size_in_bits** Bu alan SHA256 için kullanılmaz
- **handle (tanıtıcı)** Bu hizmet çağıranın tanıtıcısı döndürür. Tanıtıcı uygulamaya bağımlıdır ve bu uygulamada kullanılmaz. Uygulama tanıtıcı için NULL değerini geçsin.
- **crypto_metadata** SHA256 denetim bloğu için geçerli bir bellek alanı işaretçisi. Bellek alanı başlangıç adresi 4 bayta hizalanmış olması gerekir.
- **crypto_metadata_size** Veri alanı bayt cinsinden crypto_metadata. SHA256 için meta veri boyutunun *sizeof(NX_CRYPTO_SHA256) olması gerekir*

### <a name="return-values"></a>Dönüş Değerleri

- **NX_CRYPTO_SUCCESS** (0x00) ANAHTAR ve anahtar boyutuyla SHA256 denetim bloğu başarıyla başlatılacak.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) Şifreleme kitaplığı geçersiz durumda ve kullanılamaz.
- **NX_PTR_ERROR** (0x07) Anahtar için geçersiz işaretçi ya da geçersiz crypto_metadata veya crypto_metadata_size veya crypto_metadata 4-byte hizalanmamış.

## <a name="_nx_crypto_method_sha256_operation"></a>_nx_crypto_method_sha256_operation

SHA256 karma işlemi gerçekleştirme

### <a name="prototype"></a>Prototype

```c
UINT _nx_crypto_method_sha256_operation(UINT op,
    VOID *handle,
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    UCHAR *input,
    ULONG input_length_in_byte,
    UCHAR *iv_ptr,
    UCHAR *output,
    ULONG output_length_in_byte,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size,
    VOID *packet_ptr,
    VOID (*nx_crypto_hw_process_callback)(VOID *packet_ptr, UINT
    status));
```

### <a name="description"></a>Description

Bu işlev SHA256 karma işlemini gerçekleştirir. SHA256 denetim bloğu _ ***nx_crypto_method_sha256_init() ile başlatılmış olması gerekir.*** Gerçekleştirilecek SHA256 algoritması, yöntem denetim bloğunda belirtilen *algoritmaya* dayalıdır.

Son işlem *NX_CRYPTO_HASH_CALCULATE,* çıkış arabellek boyutu SHA256 için 32 bayt veya SHA224 için 28 bayt olmalıdır.

### <a name="parameters"></a>Parametreler

- **op (op)** Gerçekleştirecek işlem türü. Geçerli işlem:
  - *NX_CRYPTO_HASH_INITIALIZE*
  - *NX_CRYPTO_HASH_UPDATE*
  - *NX_CRYPTO_HASH_CALCULATE*
- **handle (tanıtıcı)** Bu alan, NetX Şifreleme kitaplığının yazılım uygulamasında kullanılmaz. Geçirilen tüm değerler sessizce yoksayılır.
- **yöntem** Geçerli SHA256 şifreleme yönteminin işaretçisi. Burada kullanılan şifreleme yöntemi , _ *nx_crypto_method_sha256_init() içinde aynı şekilde kullanılmalıdır.*
- **input_data** Giriş metin verilerini içeren bir arabelleği belirtir. Giriş arabelleğiyle ilgili bir kısıtlama yoktur.
- **input_data_size** Giriş verisi boyutu (bayt cinsinden).
- **iv_ptr** Bu alan SHA256 için kullanılmaz.
- **iv_size** Bu alan SHA256 için kullanılmaz.
- **output_buffer** Oluşturulan SHA256 karması için bellek alanına işaretçi.
- **output_buffer_size** Çıkış arabelleğinin bayt cinsinden boyutu. SHA256 için arabellek boyutu 32 bayt olmalıdır. SHA224 için arabellek boyutu 28 bayt olmalıdır.
- **crypto_metadata** _nx_crypto_method_sha2_init() içinde kullanılan SHA2 *denetim bloğuna işaretçi.*
- **crypto_metadata_size** Veri alanı bayt cinsinden crypto_metadata. SHA256 için meta veri boyutunun *boyutof(NX_CRYPTO_SHA256) olması gerekir*
- **packet_ptr** Bu alan, NetX Şifreleme kitaplığının yazılım uygulamasında kullanılmaz. Geçirilen tüm değerler sessizce yoksayılır.
- **nx_crypto_hw_process_callback** Bu alan, NetX Şifreleme kitaplığının yazılım uygulamasında kullanılmaz. Geçirilen tüm değerler sessizce yoksayılır.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_CRYPTO_SUCCESS** (0x00) SHA256 işlemi başarıyla yürütülür.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) Şifreleme kitaplığı geçersiz durumda ve kullanılamaz.
- **NX_PTR_ERROR** (0x07) Geçersiz giriş işaretçisi veya geçersiz uzunluk.
- **NX_CRYPTO_INVALID_ALGORITHM** (0x20004) Geçersiz SHA256 algoritması belirtiliyor.
- **NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) Geçersiz çıkış arabellek boyutu.

## <a name="_nx_crypto_method_sha256_cleanup"></a>_nx_crypto_method_sha256_cleanup

SHA256 denetim bloğunu temizleyin.

### <a name="prototype"></a>Prototype

```c
UINT _nx_crypto_method_sha256_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a>Description

Uygulama, bu SHA256 oturumunun artık gerekli olmadığını belirledikten sonra SHA256 denetim bloğunu temizlemek için bu işlevi çağırır.

### <a name="parameters"></a>Parametreler

- **crypto_metadata** *_Nx_crypto_method_sha256_init ()* IÇINDE kullanılan SHA256 denetim bloğuna yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_CRYPTO_SUCCESS** (0x00) SHA256 oturumu başarıyla temizlendi.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.

## <a name="_nx_crypto_method_sha512_init"></a>_nx_crypto_method_sha512_init

SHA512 olur şifre denetim bloğunu başlatır

### <a name="prototype"></a>Prototype

```c
UINT _nx_crypto_method_sha512_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size);
```

### <a name="description"></a>Description

Bu işlev, SHA512 olur denetim bloğunu verilen anahtar dizesiyle başlatır. SHA512 olur denetim bloğu başlatıldıktan sonra, sonraki SHA512 olur işlemi aynı denetim bloğunu kullanıyor olacaktır.

Uygulama birden çok SHA512 olur denetim bloğu oluşturabilir, her biri bir oturumu temsil eder. SHA512 olur denetim bloğunu başlatmak yeni bir karma hesaplama oturumu başlatır. SHA512 olur denetim bloğunu yeniden başlatmak geçerli oturumu ve yıldızları yeni bir kez terk edin.

### <a name="parameters"></a>Parametreler

- **yöntemi** Geçerli bir SHA512 olur şifreleme yöntemi denetim bloğuna yönelik işaretçi. Aşağıdaki önceden tanımlanmış şifreleme yöntemleri kullanılabilir:
  - *crypto_method_sha512*
  - *crypto_method_sha384*
- **anahtar** Bu alan SHA512 olur için kullanılmaz.
- **key_size_in_bits** Bu alan SHA512 olur için kullanılmıyor
- **tanıtıcı** Bu hizmet, çağırana bir tanıtıcı döndürür. Tanıtıcı uygulamaya bağımlıdır ve bu uygulamada kullanılmıyor. Uygulama tanıtıcı için NULL değer geçirecektir.
- **crypto_metadata** SHA512 olur denetim bloğu için geçerli bir bellek alanı işaretçisi. Bellek alanının başlangıç adresi 4 bayt hizalı olmalıdır.
- **crypto_metadata_size** Crypto_metadata alanının bayt cinsinden boyutu. SHA512 olur için meta veri boyutu *sizeof olmalıdır (NX_CRYPTO_SHA512)*

### <a name="return-values"></a>Dönüş Değerleri

- Anahtar ve anahtar boyutuyla SHA512 olur denetim bloğunun başarılı bir şekilde başlatılması **NX_CRYPTO_SUCCESS** (0x00).
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.
- **NX_PTR_ERROR** (0x07) anahtar için geçersiz işaretçi veya geçersiz crypto_metadata veya crypto_metadata_size ya da crypto_metadata 4 bayt hizalı değil.

## <a name="_nx_crypto_method_sha512_operation"></a>_nx_crypto_method_sha512_operation

SHA512 olur karma işlemi gerçekleştir

### <a name="prototype"></a>Prototype

```c
UINT _nx_crypto_method_sha512_operation(UINT op,
    VOID *handle,
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    UCHAR *input,
    ULONG input_length_in_byte,
    UCHAR *iv_ptr,
    UCHAR *output,
    ULONG output_length_in_byte,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size,
    VOID *packet_ptr,
    VOID (*nx_crypto_hw_process_callback)(VOID *packet_ptr, UINT status));
```

### <a name="description"></a>Description

Bu işlev SHA512 olur karma işlem gerçekleştirir. SHA512 olur denetim bloğu _ *nx_crypto_method_sha512_init ()* ile başlatılmış olmalıdır. Gerçekleştirilecek SHA512 olur algoritması, *Yöntem* denetim bloğunda belirtilen algoritmayı temel alır.

Son *NX_CRYPTO_HASH_CALCULATE* işlemi için, çıkış ARABELLEĞI boyutu sha512 olur için 64 bayt veya SHA384 için 48 bayt olmalıdır.

### <a name="parameters"></a>Parametreler

- **op** Gerçekleştirilecek işlemin türü. Geçerli işlem:
  - *NX_CRYPTO_HASH_INITIALIZE*
  - *NX_CRYPTO_HASH_UPDATE*
  - *NX_CRYPTO_HASH_CALCULATE*
- **tanıtıcı** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz. Geçirilen tüm değerler sessizce yok sayılır.
- **yöntemi** Geçerli SHA512 olur şifre yöntemine yönelik işaretçi. Burada kullanılan şifreleme yöntemi _ *nx_crypto_method_sha512_init ()* içinde kullanılan aynı olmalıdır.
- **input_data** Girdi metin verileri içeren bir arabelleğe işaret eder. Giriş arabelleğinde kısıtlama yoktur.
- **input_data_size** Giriş verilerinin bayt cinsinden boyutu.
- **iv_ptr** Bu alan SHA512 olur için kullanılmaz.
- **iv_size** Bu alan SHA512 olur için kullanılmaz.
- **output_buffer** Oluşturulan SHA512 olur karması için bellek alanına yönelik işaretçi.
- **output_buffer_size** Çıkış arabelleğinin bayt cinsinden boyutu. SHA512 olur için arabellek boyutu 64 bayt olmalıdır. SHA384 için arabellek boyutu 48 bayt olmalıdır.
- **crypto_metadata** *_Nx_crypto_method_sha512_init ()* IÇINDE kullanılan SHA512 olur denetim bloğuna yönelik işaretçi.
- **crypto_metadata_size** Crypto_metadata alanının bayt cinsinden boyutu. SHA512 olur için meta veri boyutu sizeof olmalıdır *(NX_CRYPTO_SHA512)*
- **packet_ptr** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz. Geçirilen tüm değerler sessizce yok sayılır.
- **nx_crypto_hw_process_callback** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz. Geçirilen tüm değerler sessizce yok sayılır.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_CRYPTO_SUCCESS** (0x00) SHA512 olur işlemini başarıyla yürütüldü.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.
- **NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi veya uzunluğu geçersiz.
- **NX_CRYPTO_INVALID_ALGORITHM** (0x20004) geçersiz SHA512 olur algoritması belirtildi.
- **NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) geçersiz çıkış arabelleği boyutu.

## <a name="_nx_crypto_method_sha512_cleanup"></a>_nx_crypto_method_sha512_cleanup

SHA512 olur denetim bloğunu temizleyin.

### <a name="prototype"></a>Prototype

```c
UINT _nx_crypto_method_sha512_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a>Description

Uygulama, bu SHA512 olur oturumunun artık gerekli olmadığını belirledikten sonra SHA512 olur denetim bloğunu temizlemek için bu işlevi çağırır.

### <a name="parameters"></a>Parametreler

- **crypto_metadata** *_Nx_crypto_method_sha512_init ()* IÇINDE kullanılan SHA512 olur denetim bloğuna yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_CRYPTO_SUCCESS** (0x00) SHA512 olur oturumu başarıyla temizlendi.
- **NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.