---
title: Bölüm 4-Azure RTOS NetX şifreleme API 'SI açıklaması
description: Azure RTOS NetX şifreleme API 'SI açıklaması
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 04e732bc1fd6012636aab3a57391829f529724cf
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826812"
---
# <a name="chapter-4---azure-rtos-netx-crypto-api-description"></a><span data-ttu-id="51eee-103">Bölüm 4-Azure RTOS NetX şifreleme API 'SI açıklaması</span><span class="sxs-lookup"><span data-stu-id="51eee-103">Chapter 4 - Azure RTOS NetX Crypto API description</span></span>

## <a name="nx_crypto_initialize"></a><span data-ttu-id="51eee-104">nx_crypto_initialize</span><span class="sxs-lookup"><span data-stu-id="51eee-104">nx_crypto_initialize</span></span>

<span data-ttu-id="51eee-105">NetX güvenli kitaplığını başlatır</span><span class="sxs-lookup"><span data-stu-id="51eee-105">Initializes the NetX Secure Library</span></span>

### <a name="prototype"></a><span data-ttu-id="51eee-106">Prototype</span><span class="sxs-lookup"><span data-stu-id="51eee-106">Prototype</span></span>

```c
UINT nx_crypto_initialize(VOID);
```

### <a name="description"></a><span data-ttu-id="51eee-107">Açıklama</span><span class="sxs-lookup"><span data-stu-id="51eee-107">Description</span></span>

<span data-ttu-id="51eee-108">Bu işlev, Azure RTOS NetX şifre kitaplığı modülünü başlatır.</span><span class="sxs-lookup"><span data-stu-id="51eee-108">This function initializes the Azure RTOS NetX Crypto library module.</span></span> <span data-ttu-id="51eee-109">Diğer şifreleme işlevlerinin hiçbirini kullanmadan önce, uygulamanın başlatma işlemini gerçekleştirmek ve kitaplığın bütünlüğünü doğrulamak için bu işlevi çağırması gerekir.</span><span class="sxs-lookup"><span data-stu-id="51eee-109">Before using any of the other cryptographic functions, the application must call this function to perform initialization and to validate the integrity of the library.</span></span> <span data-ttu-id="51eee-110">Diğer NetX şifreleme hizmetlerini kullanmadan önce bu işlevi çağırmaya yönelik hata döndürülmeyecektir.</span><span class="sxs-lookup"><span data-stu-id="51eee-110">Failure to call this function before using other NetX Crypto services will result in errors being returned.</span></span>

### <a name="parameters"></a><span data-ttu-id="51eee-111">Parametreler</span><span class="sxs-lookup"><span data-stu-id="51eee-111">Parameters</span></span>

- <span data-ttu-id="51eee-112">**Hiçbiri**</span><span class="sxs-lookup"><span data-stu-id="51eee-112">**None**</span></span>

### <a name="return-values"></a><span data-ttu-id="51eee-113">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="51eee-113">Return Values</span></span>

- <span data-ttu-id="51eee-114">**NX_CRYPTO_SUCCESS** (0x00) başarıyla başlatılmış NETX şifre kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="51eee-114">**NX_CRYPTO_SUCCESS** (0x00) Successful initialized NetX Crypto library.</span></span> <span data-ttu-id="51eee-115">Kitaplık işlevleri artık hazırdır ve kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="51eee-115">The library functions are now ready, and can be used.</span></span>
- <span data-ttu-id="51eee-116">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifreleme kitaplığı başlatılamıyor veya bütünlük denetimini yapamıyor.</span><span class="sxs-lookup"><span data-stu-id="51eee-116">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library fails to initialize, or fails the integrity check.</span></span> <span data-ttu-id="51eee-117">Uygulama bu kitaplığı kullanamıyor.</span><span class="sxs-lookup"><span data-stu-id="51eee-117">Application cannot use this library.</span></span>

### <a name="example"></a><span data-ttu-id="51eee-118">Örnek</span><span class="sxs-lookup"><span data-stu-id="51eee-118">Example</span></span>

<span data-ttu-id="51eee-119">TODO</span><span class="sxs-lookup"><span data-stu-id="51eee-119">TODO</span></span>

## <a name="nx_crypto_module_state_get"></a><span data-ttu-id="51eee-120">nx_crypto_module_state_get</span><span class="sxs-lookup"><span data-stu-id="51eee-120">nx_crypto_module_state_get</span></span>

<span data-ttu-id="51eee-121">FIPS etkin modülünün geçerli durumunu alma</span><span class="sxs-lookup"><span data-stu-id="51eee-121">Retrieve the current status of the FIPS-enabled module</span></span>

### <a name="prototype"></a><span data-ttu-id="51eee-122">Prototype</span><span class="sxs-lookup"><span data-stu-id="51eee-122">Prototype</span></span>

```c
UINT nx_crypto_module_state_get(VOID);
```

### <a name="description"></a><span data-ttu-id="51eee-123">Açıklama</span><span class="sxs-lookup"><span data-stu-id="51eee-123">Description</span></span>

<span data-ttu-id="51eee-124">Bu hizmet yalnızca FIPS derleme kitaplığı 'nda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="51eee-124">This service is only available in the FIPS build library.</span></span> <span data-ttu-id="51eee-125">NetX şifre kitaplığının geçerli durumunun durumunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="51eee-125">It returns the state of the current state of the NetX Crypto library.</span></span>

### <a name="parameters"></a><span data-ttu-id="51eee-126">Parametreler</span><span class="sxs-lookup"><span data-stu-id="51eee-126">Parameters</span></span>

- <span data-ttu-id="51eee-127">**Hiçbiri**</span><span class="sxs-lookup"><span data-stu-id="51eee-127">**None**</span></span>

### <a name="return-values"></a><span data-ttu-id="51eee-128">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="51eee-128">Return Values</span></span>

- <span data-ttu-id="51eee-129">**Durum bayrağı:**</span><span class="sxs-lookup"><span data-stu-id="51eee-129">**Status Flag:**</span></span>
  - <span data-ttu-id="51eee-130">NX_CRYPTO_LIBRARY_STATE_UNINITIALIZED 0x00000001</span><span class="sxs-lookup"><span data-stu-id="51eee-130">NX_CRYPTO_LIBRARY_STATE_UNINITIALIZED 0x00000001</span></span>
  - <span data-ttu-id="51eee-131">NX_CRYPTO_LIBRARY_STATE_POST_IN_PROGRESS 0x00000002</span><span class="sxs-lookup"><span data-stu-id="51eee-131">NX_CRYPTO_LIBRARY_STATE_POST_IN_PROGRESS 0x00000002</span></span>
  - <span data-ttu-id="51eee-132">NX_CRYPTO_LIBRARY_STATE_INTEGRITY_TEST_FAILED 0x00000004</span><span class="sxs-lookup"><span data-stu-id="51eee-132">NX_CRYPTO_LIBRARY_STATE_INTEGRITY_TEST_FAILED 0x00000004</span></span>
  - <span data-ttu-id="51eee-133">NX_CRYPTO_LIBRARY_STATE_FUNCTIONAL_TEST_FAILED 0x00000008</span><span class="sxs-lookup"><span data-stu-id="51eee-133">NX_CRYPTO_LIBRARY_STATE_FUNCTIONAL_TEST_FAILED 0x00000008</span></span>
  - <span data-ttu-id="51eee-134">NX_CRYPTO_LIBRARY_STATE_OPERATIONAL 0x80000000</span><span class="sxs-lookup"><span data-stu-id="51eee-134">NX_CRYPTO_LIBRARY_STATE_OPERATIONAL 0x80000000</span></span>
- <span data-ttu-id="51eee-135">**Diğer tüm değerler geçersiz.**</span><span class="sxs-lookup"><span data-stu-id="51eee-135">**All other values are invalid.**</span></span>

### <a name="example"></a><span data-ttu-id="51eee-136">Örnek</span><span class="sxs-lookup"><span data-stu-id="51eee-136">Example</span></span>

<span data-ttu-id="51eee-137">TODO</span><span class="sxs-lookup"><span data-stu-id="51eee-137">TODO</span></span>

## <a name="_nx_crypto_method_aes_init"></a><span data-ttu-id="51eee-138">_nx_crypto_method_aes_init</span><span class="sxs-lookup"><span data-stu-id="51eee-138">_nx_crypto_method_aes_init</span></span>

<span data-ttu-id="51eee-139">AES şifreleme denetim bloğunu başlatır</span><span class="sxs-lookup"><span data-stu-id="51eee-139">Initializes the AES crypto control block</span></span>

### <a name="prototype"></a><span data-ttu-id="51eee-140">Prototype</span><span class="sxs-lookup"><span data-stu-id="51eee-140">Prototype</span></span>

```c
UINT _nx_crypto_method_aes_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size);
```

### <a name="description"></a><span data-ttu-id="51eee-141">Açıklama</span><span class="sxs-lookup"><span data-stu-id="51eee-141">Description</span></span>

<span data-ttu-id="51eee-142">Bu işlev, AES denetim bloğunu verilen anahtar dizesiyle başlatır.</span><span class="sxs-lookup"><span data-stu-id="51eee-142">This function initializes the AES control block with the given key string.</span></span> <span data-ttu-id="51eee-143">AES denetim bloğu başlatıldıktan sonra, sonraki AES işlemi aynı anahtar ve anahtar boyutunu kullanacaktır.</span><span class="sxs-lookup"><span data-stu-id="51eee-143">Once the AES control block is initialized, subsequent AES operation will be using the same key and key size.</span></span>

<span data-ttu-id="51eee-144">Uygulama birden çok AES denetim bloğu oluşturabilir, her biri bir oturumu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="51eee-144">Application may create multiple AES control blocks, each represents a session.</span></span> <span data-ttu-id="51eee-145">Bir denetim bloğuna bir anahtar atanır.</span><span class="sxs-lookup"><span data-stu-id="51eee-145">A key is assigned to a control block.</span></span> <span data-ttu-id="51eee-146">Sonraki şifreleme veya şifre çözme işlemi, AES denetim bloğunu yeniden başlatmaya gerek kalmadan aynı AES denetim bloğuna başvurabilir.</span><span class="sxs-lookup"><span data-stu-id="51eee-146">Subsequent encryption or decryption operation can reference to the same AES control block without the need to re-initialize the AES control block.</span></span> <span data-ttu-id="51eee-147">Oturumun anahtarı değiştirilirse, uygulamanın, güncelleştirilmiş anahtarla AES denetim bloğunu yeniden başlatması gerekir.</span><span class="sxs-lookup"><span data-stu-id="51eee-147">If the key for the session is changed, application needs to re-initialize AES control block with the updated key.</span></span>

<span data-ttu-id="51eee-148">_ *Nx_crypto_method_aes_init ()* çağrısı, önceden yapılandırılmış bir anahtarı ve anahtar boyutunu yeni anahtara otomatik olarak güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="51eee-148">Calling _ *nx_crypto_method_aes_init()* automatically updates a previously configured key and key size to the new key.</span></span>

### <a name="parameters"></a><span data-ttu-id="51eee-149">Parametreler</span><span class="sxs-lookup"><span data-stu-id="51eee-149">Parameters</span></span>

- <span data-ttu-id="51eee-150">**yöntemi** Geçerli bir AES şifreleme yöntemi denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-150">**method** Pointer to a valid AES crypto method control block.</span></span> <span data-ttu-id="51eee-151">Aşağıdaki önceden tanımlanmış AES şifreleme yöntemleri kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="51eee-151">The following pre-defined AES crypto methods are available:</span></span>
  - <span data-ttu-id="51eee-152">*crypto_method_aes_cbc_128*</span><span class="sxs-lookup"><span data-stu-id="51eee-152">*crypto_method_aes_cbc_128*</span></span>
  - <span data-ttu-id="51eee-153">*crypto_method_aes_cbc_192*</span><span class="sxs-lookup"><span data-stu-id="51eee-153">*crypto_method_aes_cbc_192*</span></span>
  - <span data-ttu-id="51eee-154">*crypto_method_aes_cbc_256*</span><span class="sxs-lookup"><span data-stu-id="51eee-154">*crypto_method_aes_cbc_256*</span></span>
  - <span data-ttu-id="51eee-155">*crypto_method_aes_ctr_128*</span><span class="sxs-lookup"><span data-stu-id="51eee-155">*crypto_method_aes_ctr_128*</span></span>
  - <span data-ttu-id="51eee-156">*crypto_method_aes_ctr_192*</span><span class="sxs-lookup"><span data-stu-id="51eee-156">*crypto_method_aes_ctr_192*</span></span>
  - <span data-ttu-id="51eee-157">*crypto_method_aes_ctr_256*</span><span class="sxs-lookup"><span data-stu-id="51eee-157">*crypto_method_aes_ctr_256*</span></span>
  - <span data-ttu-id="51eee-158">*crypto_method_aes_xcbc_128*</span><span class="sxs-lookup"><span data-stu-id="51eee-158">*crypto_method_aes_xcbc_128*</span></span>
  - <span data-ttu-id="51eee-159">*crypto_method_aes_ccm_8_128*</span><span class="sxs-lookup"><span data-stu-id="51eee-159">*crypto_method_aes_ccm_8_128*</span></span>
- <span data-ttu-id="51eee-160">**anahtar** AES anahtarını içeren bir arabelleğe işaret eder</span><span class="sxs-lookup"><span data-stu-id="51eee-160">**key** Points to a buffer containing the AES key</span></span>
- <span data-ttu-id="51eee-161">**key_size_in_bits** Anahtarın bit cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-161">**key_size_in_bits** Size of the key, in bits.</span></span> <span data-ttu-id="51eee-162">Geçerli değerler:</span><span class="sxs-lookup"><span data-stu-id="51eee-162">Valid values are:</span></span>
  - <span data-ttu-id="51eee-163">*NX_CRYPTO_AES_KEY_SIZE_128_BITS*</span><span class="sxs-lookup"><span data-stu-id="51eee-163">*NX_CRYPTO_AES_KEY_SIZE_128_BITS*</span></span>
  - <span data-ttu-id="51eee-164">*NX_CRYPTO_AES_KEY_SIZE_192_BITS*</span><span class="sxs-lookup"><span data-stu-id="51eee-164">*NX_CRYPTO_AES_KEY_SIZE_192_BITS*</span></span>
  - <span data-ttu-id="51eee-165">*NX_CRYPTO_AES_KEY_SIZE_256_BITS*</span><span class="sxs-lookup"><span data-stu-id="51eee-165">*NX_CRYPTO_AES_KEY_SIZE_256_BITS*</span></span>
  - <span data-ttu-id="51eee-166">**Diğer tüm değerler geçersiz.**</span><span class="sxs-lookup"><span data-stu-id="51eee-166">**All other values are invalid.**</span></span>
- <span data-ttu-id="51eee-167">**tanıtıcı** Bu hizmet, çağırana bir tanıtıcı döndürür.</span><span class="sxs-lookup"><span data-stu-id="51eee-167">**handle** This service returns a handle to the caller.</span></span> <span data-ttu-id="51eee-168">Tanıtıcı uygulamaya bağımlıdır ve bu uygulamada kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="51eee-168">The handle is implementation-dependent, and is not being used in this implementation.</span></span> <span data-ttu-id="51eee-169">Uygulama tanıtıcı için NULL değer geçirecektir.</span><span class="sxs-lookup"><span data-stu-id="51eee-169">Application shall pass NULL for the handle.</span></span>
- <span data-ttu-id="51eee-170">**crypto_metadata** AES denetim bloğu için geçerli bir bellek alanı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="51eee-170">**crypto_metadata** Pointer to a valid memory space for the AES control block.</span></span> <span data-ttu-id="51eee-171">Bellek alanının başlangıç adresi 4 bayt hizalı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-171">The starting address of the memory space must be 4-byte aligned.</span></span>
- <span data-ttu-id="51eee-172">**crypto_metadata_size** Crypto_metadata alanının bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-172">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="51eee-173">AES için meta veri boyutu *sizeof olmalıdır (NX_AES)*</span><span class="sxs-lookup"><span data-stu-id="51eee-173">For AES, the metadata size must be *sizeof(NX_AES)*</span></span>

### <a name="return-values"></a><span data-ttu-id="51eee-174">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="51eee-174">Return Values</span></span>

- <span data-ttu-id="51eee-175">**NX_CRYPTO_SUCCESS** (0x00) anahtar ve anahtar boyutuyla AES denetim bloğunun başarılı bir şekilde başlatılması.</span><span class="sxs-lookup"><span data-stu-id="51eee-175">**NX_CRYPTO_SUCCESS** (0x00) Successful initialization of the AES control block with the key and key size.</span></span>
- <span data-ttu-id="51eee-176">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-176">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="51eee-177">**NX_PTR_ERROR (0x07)** Anahtar için geçersiz işaretçi veya crypto_metadata ya da crypto_metadata_size geçersiz veya crypto_metadata 4 baytlık hizalı değil.</span><span class="sxs-lookup"><span data-stu-id="51eee-177">**NX_PTR_ERROR (0x07)** Invalid pointer to the key, or invalid crypto_metadata or crypto_metadata_size, or crypto_metadata is not 4-byte aligned.</span></span>
- <span data-ttu-id="51eee-178">**NX_CRYPTO_UNSUPPORTED_KEY_SIZE** (0x20002) anahtar boyutu AES için geçerli değil.</span><span class="sxs-lookup"><span data-stu-id="51eee-178">**NX_CRYPTO_UNSUPPORTED_KEY_SIZE** (0x20002) Key size is not a valid for AES.</span></span>

## <a name="_nx_crypto_method_aes_operation"></a><span data-ttu-id="51eee-179">_nx_crypto_method_aes_operation</span><span class="sxs-lookup"><span data-stu-id="51eee-179">_nx_crypto_method_aes_operation</span></span>

<span data-ttu-id="51eee-180">AES işlemi gerçekleştirin (şifreleme veya şifre çözme).</span><span class="sxs-lookup"><span data-stu-id="51eee-180">Perform an AES operation (encryption or decryption).</span></span>

### <a name="prototype"></a><span data-ttu-id="51eee-181">Prototype</span><span class="sxs-lookup"><span data-stu-id="51eee-181">Prototype</span></span>

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

### <a name="description"></a><span data-ttu-id="51eee-182">Açıklama</span><span class="sxs-lookup"><span data-stu-id="51eee-182">Description</span></span>

<span data-ttu-id="51eee-183">Bu işlev AES şifreleme veya şifre çözme işlemi gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="51eee-183">This function performs AES encryption or decryption operation.</span></span> <span data-ttu-id="51eee-184">AES denetim bloğunun _ *nx_crypto_method_aes_init ()* ile başlatılmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="51eee-184">The AES control block must have been initialized with _ *nx_crypto_method_aes_init()*.</span></span> <span data-ttu-id="51eee-185">Gerçekleştirilecek AES algoritması, *Yöntem* denetim bloğunda belirtilen algoritmayı temel alır.</span><span class="sxs-lookup"><span data-stu-id="51eee-185">The AES algorithm to be performed is based on the algorithm specified in the *method* control block.</span></span>

<span data-ttu-id="51eee-186">Giriş arabelleği boyutu 16 baytın katlarından biri olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-186">The input buffer size must be a multiple of 16 bytes.</span></span> <span data-ttu-id="51eee-187">Şifresi çözülen verilerin boyutu, giriş veri boyutunun aynı boyutudur.</span><span class="sxs-lookup"><span data-stu-id="51eee-187">The size of the decrypted data is the same size of the input data size.</span></span> <span data-ttu-id="51eee-188">Şifrelenmiş veriler, AES blok boyutunun bir çift katı elde etmek için doldurulmuştur, doldurma, çıkış arabelleğine dahil edilir ve uygulama tarafından işlenmelidir.</span><span class="sxs-lookup"><span data-stu-id="51eee-188">If the encrypted data was padded to achieve an even multiple of the AES block size, the padding will be included in the output buffer and must be handled by the application.</span></span>

<span data-ttu-id="51eee-189">Bu işlem durum bilgilerini saklar ve AES denetim bloğunda anahtar malzemesini değiştirmez.</span><span class="sxs-lookup"><span data-stu-id="51eee-189">This operation does not keep state information, and does not alter the key material in the AES control block.</span></span>

<span data-ttu-id="51eee-190">Op NX_CRYPTO_SET_ADDITIONAL_DATA ve algoritm AES-CCM8 olduğunda, giriş ek verilere işaret eder ve input_length_in_byte ek verilerin uzunluktadır.</span><span class="sxs-lookup"><span data-stu-id="51eee-190">When the op is NX_CRYPTO_SET_ADDITIONAL_DATA and algoritm is AES-CCM8, the input points to additional data and input_length_in_byte is the length of additional data.</span></span>

### <a name="parameters"></a><span data-ttu-id="51eee-191">Parametreler</span><span class="sxs-lookup"><span data-stu-id="51eee-191">Parameters</span></span>

- <span data-ttu-id="51eee-192">**op** Gerçekleştirilecek işlemin türü.</span><span class="sxs-lookup"><span data-stu-id="51eee-192">**op** Type of operation to perform.</span></span> <span data-ttu-id="51eee-193">Geçerli işletim amaçları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="51eee-193">Valid opertions are:</span></span>
  - <span data-ttu-id="51eee-194">*NX_CRYPTO_ENCRYPT*</span><span class="sxs-lookup"><span data-stu-id="51eee-194">*NX_CRYPTO_ENCRYPT*</span></span>
  - <span data-ttu-id="51eee-195">*NX_CRYPTO_DECRYPT*</span><span class="sxs-lookup"><span data-stu-id="51eee-195">*NX_CRYPTO_DECRYPT*</span></span>
  - <span data-ttu-id="51eee-196">*NX_CRYPTO_AUTHENTICATE (yalnızca AES-XCBC)*</span><span class="sxs-lookup"><span data-stu-id="51eee-196">*NX_CRYPTO_AUTHENTICATE (AES-XCBC only)*</span></span>
  - <span data-ttu-id="51eee-197">*NX_CRYPTO_SET_ADDITIONAL_DATA (yalnızca AES-CCM8)*</span><span class="sxs-lookup"><span data-stu-id="51eee-197">*NX_CRYPTO_SET_ADDITIONAL_DATA (AES-CCM8 only)*</span></span>
- <span data-ttu-id="51eee-198">**tanıtıcı** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-198">**handle** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="51eee-199">Geçirilen tüm değerler sessizce yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="51eee-199">Any values passed in are silently ignored.</span></span>
- <span data-ttu-id="51eee-200">**yöntemi** Geçerli AES şifreleme yöntemine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-200">**method** Pointer to the valid AES crypto method.</span></span> <span data-ttu-id="51eee-201">Burada kullanılan şifreleme yöntemi, *nx_crypto_method_aes_init ()* içinde kullanılan aynı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-201">The crypto method used here must be the same used in the *nx_crypto_method_aes_init().*</span></span>
- <span data-ttu-id="51eee-202">**input_data** Şifrelenmiş metin verileri içeren bir arabelleğe işaret eder.</span><span class="sxs-lookup"><span data-stu-id="51eee-202">**input_data** Points to a buffer containing encrypted text data.</span></span> <span data-ttu-id="51eee-203">Giriş arabelleğinde kısıtlama yoktur.</span><span class="sxs-lookup"><span data-stu-id="51eee-203">There are not restrictions on input buffer.</span></span>
- <span data-ttu-id="51eee-204">**input_data_size** Giriş verilerinin bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-204">**input_data_size** Size of the input data, in bytes.</span></span> <span data-ttu-id="51eee-205">Giriş verisi boyutu 16 baytın katlarından biri olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-205">The input data size must be a multiple of 16 bytes.</span></span>
- <span data-ttu-id="51eee-206">**iv_ptr** Ilk vektör işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="51eee-206">**iv_ptr** Pointer to the Initial Vector.</span></span> <span data-ttu-id="51eee-207">IV arabelleğinde kısıtlama yoktur.</span><span class="sxs-lookup"><span data-stu-id="51eee-207">There are no restrictions on the IV buffer.</span></span>
- <span data-ttu-id="51eee-208">**iv_size** Başlangıçtaki vektör bloğunun boyutu, bayt cinsinden bu alanın 16 olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="51eee-208">**iv_size** Size of the Initial Vector block, in bytes This field must be 16.</span></span>
- <span data-ttu-id="51eee-209">**output_buffer** Şifresiz metin verilerini depolamak için AES için bellek alanı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="51eee-209">**output_buffer** Pointer to the memory area for AES to store the clear text data.</span></span> <span data-ttu-id="51eee-210">Uygulama, çıkış arabelleği için alan ayırmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-210">Application must allocate space for the output buffer.</span></span> <span data-ttu-id="51eee-211">Çıkış arabelleği, giriş arabelleğiyle çakışabilir.</span><span class="sxs-lookup"><span data-stu-id="51eee-211">Output buffer may overlap with input buffer.</span></span> <span data-ttu-id="51eee-212">Aynı başlangıç adresini paylaştıkları takdirde çıkış arabelleği giriş arabelleğiyle çakışabilir.</span><span class="sxs-lookup"><span data-stu-id="51eee-212">The output buffer may overlap with the input buffer if they share the same starting address.</span></span>
- <span data-ttu-id="51eee-213">**output_buffer_size** Çıkış arabelleğinin bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-213">**output_buffer_size** Size of the output buffer in bytes.</span></span> <span data-ttu-id="51eee-214">Çıkış arabelleği boyutunun en az girdi arabellek boyutuyla aynı olması ve çıkış arabelleği boyutunun 16 baytın katlarından biri olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="51eee-214">Output buffer size must be at least the same of the input buffer size, and the output buffer size must be a multiple of 16 bytes.</span></span>
- <span data-ttu-id="51eee-215">**crypto_metadata** *_Nx_crypto_method_aes_init () \* \** içinde kullanılan AES denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-215">**crypto_metadata** Pointer to the AES control block used in *_nx_crypto_method_aes_init()\*.\**</span></span>
- <span data-ttu-id="51eee-216">**crypto_metadata_size** Crypto_metadata alanının bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-216">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="51eee-217">AES için meta veri boyutu *sizeof (NX_AES)* olmalıdır</span><span class="sxs-lookup"><span data-stu-id="51eee-217">For AES, the metadata size must *sizeof(NX_AES)*</span></span>
- <span data-ttu-id="51eee-218">**packet_ptr** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-218">**packet_ptr** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="51eee-219">Geçirilen tüm değerler sessizce yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="51eee-219">Any values passed in are silently ignored.</span></span>
- <span data-ttu-id="51eee-220">**nx_crypto_hw_process_callback** -Bu alan, NETX şifreleme kitaplığının yazılım uygulamasında kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-220">**nx_crypto_hw_process_callback** - This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="51eee-221">Geçirilen tüm değerler sessizce yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="51eee-221">Any values passed in are silently ignored.</span></span>

### <a name="return-values"></a><span data-ttu-id="51eee-222">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="51eee-222">Return Values</span></span>

- <span data-ttu-id="51eee-223">**NX_CRYPTO_SUCCESS** (0x00), AES işlemini başarıyla yürütüldü.</span><span class="sxs-lookup"><span data-stu-id="51eee-223">**NX_CRYPTO_SUCCESS** (0x00) Successfully executed the AES operation.</span></span>
- <span data-ttu-id="51eee-224">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-224">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="51eee-225">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi veya uzunluğu geçersiz.</span><span class="sxs-lookup"><span data-stu-id="51eee-225">**NX_PTR_ERROR** (0x07) Invalid input pointer or invalid length.</span></span>
- <span data-ttu-id="51eee-226">**NX_CRYPTO_INVALID_ALGORITHM** (0x20004) geçersiz AES algoritması belirtildi \* \*.</span><span class="sxs-lookup"><span data-stu-id="51eee-226">**NX_CRYPTO_INVALID_ALGORITHM** (0x20004) Invalid AES algorithm being specified\*\*.</span></span>

## <a name="_nx_crypto_method_aes_cleanup"></a><span data-ttu-id="51eee-227">_nx_crypto_method_aes_cleanup</span><span class="sxs-lookup"><span data-stu-id="51eee-227">_nx_crypto_method_aes_cleanup</span></span>

<span data-ttu-id="51eee-228">AES denetim bloğunu temizleyin.</span><span class="sxs-lookup"><span data-stu-id="51eee-228">Clean up the AES control block.</span></span>

### <a name="prototype"></a><span data-ttu-id="51eee-229">Prototype</span><span class="sxs-lookup"><span data-stu-id="51eee-229">Prototype</span></span>

```c
UINT _nx_crypto_method_aes_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a><span data-ttu-id="51eee-230">Açıklama</span><span class="sxs-lookup"><span data-stu-id="51eee-230">Description</span></span>

<span data-ttu-id="51eee-231">Uygulama, bu AES oturumunun artık gerekli olmadığını belirlediğinde AES denetim bloğunu temizlemek için bu işlevi çağırır.</span><span class="sxs-lookup"><span data-stu-id="51eee-231">Application calls this function to clean up the AES control block after it determines this AES session is no longer needed.</span></span>

### <a name="parameters"></a><span data-ttu-id="51eee-232">Parametreler</span><span class="sxs-lookup"><span data-stu-id="51eee-232">Parameters</span></span>

- <span data-ttu-id="51eee-233">**crypto_metadata** *_Nx_crypto_method_aes_init () \* \** içinde kullanılan AES denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-233">**crypto_metadata** Pointer to the AES control block used in *_nx_crypto_method_aes_init()\*.\**</span></span>

### <a name="return-values"></a><span data-ttu-id="51eee-234">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="51eee-234">Return Values</span></span>

- <span data-ttu-id="51eee-235">**NX_CRYPTO_SUCCESS** (0x00) AES oturumu başarıyla temizlendi.</span><span class="sxs-lookup"><span data-stu-id="51eee-235">**NX_CRYPTO_SUCCESS** (0x00) Successfully cleaned up the AES session.</span></span>
- <span data-ttu-id="51eee-236">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-236">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>

## <a name="_nx_crypto_method_3des_init"></a><span data-ttu-id="51eee-237">_nx_crypto_method_3des_init</span><span class="sxs-lookup"><span data-stu-id="51eee-237">_nx_crypto_method_3des_init</span></span>

<span data-ttu-id="51eee-238">3DES denetim bloğunu başlatın.</span><span class="sxs-lookup"><span data-stu-id="51eee-238">Initialize the 3DES control block.</span></span>

### <a name="prototype"></a><span data-ttu-id="51eee-239">Prototype</span><span class="sxs-lookup"><span data-stu-id="51eee-239">Prototype</span></span>

```c
UINT _nx_crypto_method_3des_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size);
```

### <a name="description"></a><span data-ttu-id="51eee-240">Açıklama</span><span class="sxs-lookup"><span data-stu-id="51eee-240">Description</span></span>

<span data-ttu-id="51eee-241">Bu işlev, Üçlü DES (3DES) denetim bloğunu verilen üç anahtar dizesi ile başlatır.</span><span class="sxs-lookup"><span data-stu-id="51eee-241">This function initializes the Triple DES (3DES) control block with the given three key strings.</span></span> <span data-ttu-id="51eee-242">Anahtar dizeleri her biri 8 bayt olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-242">The key strings must be 8 bytes each.</span></span> <span data-ttu-id="51eee-243">Üç DES tuşu, 24 baytlık bir arabelleğin bitişik belleğine birleştirilmiş olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-243">The three DES keys must be concatenated into contiguous memory of 24-byte buffer.</span></span> <span data-ttu-id="51eee-244">FIPS uyumlu derleme için, üç anahtar her birinden farklı olmalıdır veya işlev NX_CRYPTO_INVALID_KEY hatası döndürür.</span><span class="sxs-lookup"><span data-stu-id="51eee-244">For FIPS-compliant build, the three keys must be different from each or the function will return the NX_CRYPTO_INVALID_KEY error.</span></span> <span data-ttu-id="51eee-245">3DES denetim bloğu başlatıldıktan sonra, sonraki 3DES işlemleri de aynı anahtarları kullanır.</span><span class="sxs-lookup"><span data-stu-id="51eee-245">Once the 3DES control block is initialized, subsequent 3DES operations will use the same keys.</span></span>

<span data-ttu-id="51eee-246">Bir uygulama, her biri bir oturumu temsil eden birden çok 3DES denetim bloğu oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="51eee-246">An application may create multiple 3DES control blocks, each representing a session.</span></span> <span data-ttu-id="51eee-247">Bir denetim bloğuna bir anahtar atanır ve sonraki şifreleme veya şifre çözme işlemleri yeniden başlatmaya gerek kalmadan aynı denetim bloğuna başvurabilir.</span><span class="sxs-lookup"><span data-stu-id="51eee-247">A key is assigned to a control block and subsequent encryption or decryption operations can reference the same control block without needing to re-initialize.</span></span> <span data-ttu-id="51eee-248">Bir oturumun anahtarı değiştirilirse, uygulamanın denetim bloğunu güncelleştirilmiş anahtarla yeniden başlatması gerekir.</span><span class="sxs-lookup"><span data-stu-id="51eee-248">If the key for a session is changed, the application will need to re-initialize the control block with the updated key.</span></span>

<span data-ttu-id="51eee-249">_ *Nx_crypto_method_3des_init ()* çağrısı, önceden yapılandırılmış bir anahtarı yeni anahtarlara otomatik olarak güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="51eee-249">Calling _ *nx_crypto_method_3des_init()* automatically updates a previously configured key to the new keys.</span></span>

### <a name="parameters"></a><span data-ttu-id="51eee-250">Parametreler</span><span class="sxs-lookup"><span data-stu-id="51eee-250">Parameters</span></span>

- <span data-ttu-id="51eee-251">**yöntemi** Geçerli bir 3DES şifreleme yöntemi denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-251">**method** Pointer to a valid 3DES crypto method control block.</span></span> <span data-ttu-id="51eee-252">Aşağıdaki önceden tanımlanmış 3DES şifreleme yöntemi kullanılabilir: ***crypto_method_3des***</span><span class="sxs-lookup"><span data-stu-id="51eee-252">The following pre-defined 3DES crypto method is available: ***crypto_method_3des***</span></span>
- <span data-ttu-id="51eee-253">**anahtar** Üç (3) DES anahtarını içeren bir arabelleğe işaret eder</span><span class="sxs-lookup"><span data-stu-id="51eee-253">**key** Points to a buffer containing the three (3) DES key</span></span>
- <span data-ttu-id="51eee-254">**key_size_in_bits** 192 (3 anahtar, her 64 bit) olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-254">**key_size_in_bits** Must be 192 (3 keys, each 64 bits).</span></span>
- <span data-ttu-id="51eee-255">**tanıtıcı** Bu hizmet, çağırana bir tanıtıcı döndürür.</span><span class="sxs-lookup"><span data-stu-id="51eee-255">**handle** This service returns a handle to the caller.</span></span> <span data-ttu-id="51eee-256">Tanıtıcı, başlatılan 3DES denetim bloğunu tanımlar.</span><span class="sxs-lookup"><span data-stu-id="51eee-256">The handle identifies the 3DES control block being initialized.</span></span> <span data-ttu-id="51eee-257">Sonraki 3DES işlemleri (şifreleme, şifre çözme ve temizleme), 3DES denetim bloğuna erişmek için bu tanıtıcıyı kullanır</span><span class="sxs-lookup"><span data-stu-id="51eee-257">Subsequent 3DES operations (encryption, decryption, and cleanup) use this handle to access the 3DES control block</span></span>
- <span data-ttu-id="51eee-258">**crypto_metadata** 3DES denetim bloğu için geçerli bir bellek alanı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="51eee-258">**crypto_metadata** Pointer to a valid memory space for the 3DES control block.</span></span> <span data-ttu-id="51eee-259">Bellek alanının başlangıç adresi 4 bayt hizalı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-259">The starting address of the memory space must be 4-byte aligned.</span></span>
- <span data-ttu-id="51eee-260">**crypto_metadata_size** Crypto_metadata alanının bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-260">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="51eee-261">3DES için meta veri boyutu *sizeof olmalıdır (NX_3DES)*</span><span class="sxs-lookup"><span data-stu-id="51eee-261">For 3DES, the metadata size must be *sizeof(NX_3DES)*</span></span>

### <a name="return-value"></a><span data-ttu-id="51eee-262">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="51eee-262">Return Value</span></span>

- <span data-ttu-id="51eee-263">Anahtar ve anahtar boyutuyla 3DES denetim bloğunun başarılı bir şekilde başlatılması **NX_CRYPTO_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="51eee-263">**NX_CRYPTO_SUCCESS** (0x00) Successful initialization of the 3DES control block with the key and key size.</span></span>
- <span data-ttu-id="51eee-264">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-264">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="51eee-265">**NX_PTR_ERROR (0x07)** Anahtar için geçersiz işaretçi veya crypto_metadata ya da crypto_metadata_size geçersiz veya crypto_metadata 4 baytlık hizalı değil.</span><span class="sxs-lookup"><span data-stu-id="51eee-265">**NX_PTR_ERROR (0x07)** Invalid pointer to the key, or invalid crypto_metadata or crypto_metadata_size, or crypto_metadata is not 4-byte aligned.</span></span>
- <span data-ttu-id="51eee-266">**NX_CRYPTO_UNSUPPORTED_KEY_SIZE** (0x20002) anahtar boyutu 3DES için geçerli değil.</span><span class="sxs-lookup"><span data-stu-id="51eee-266">**NX_CRYPTO_UNSUPPORTED_KEY_SIZE** (0x20002) Key size is not a valid for 3DES.</span></span>

## <a name="_nx_crypto_method_3des_operation"></a><span data-ttu-id="51eee-267">_nx_crypto_method_3des_operation</span><span class="sxs-lookup"><span data-stu-id="51eee-267">_nx_crypto_method_3des_operation</span></span>

<span data-ttu-id="51eee-268">3DES ile şifreleme veya şifre çözme.</span><span class="sxs-lookup"><span data-stu-id="51eee-268">Encrypt or Decrypt with 3DES.</span></span>

### <a name="prototype"></a><span data-ttu-id="51eee-269">Prototype</span><span class="sxs-lookup"><span data-stu-id="51eee-269">Prototype</span></span>

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

### <a name="description"></a><span data-ttu-id="51eee-270">Açıklama</span><span class="sxs-lookup"><span data-stu-id="51eee-270">Description</span></span>

<span data-ttu-id="51eee-271">Bu işlev 3DES şifrelemesini veya şifre çözme işlemini gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="51eee-271">This function performs 3DES encryption or decryption operation.</span></span> <span data-ttu-id="51eee-272">3DES denetim bloğunun _ *nx_crypto_method_3des_init ()* ile başlatılmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="51eee-272">The 3DES control block must have been initialized with _ *nx_crypto_method_3des_init()*.</span></span> <span data-ttu-id="51eee-273">Gerçekleştirilecek 3DES algoritması, *Yöntem* denetim bloğunda belirtilen algoritmayı temel alır.</span><span class="sxs-lookup"><span data-stu-id="51eee-273">The 3DES algorithm to be performed is based on the algorithm specified in the *method* control block.</span></span>

<span data-ttu-id="51eee-274">Giriş arabelleği boyutu 8 baytın katlarından biri olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-274">The input buffer size must be a multiple of 8 bytes.</span></span> <span data-ttu-id="51eee-275">Şifresi çözülen verilerin boyutu, giriş veri boyutunun aynı boyutudur.</span><span class="sxs-lookup"><span data-stu-id="51eee-275">The size of the decrypted data is the same size of the input data size.</span></span> <span data-ttu-id="51eee-276">Şifrelenmiş veriler, 3DES blok boyutundan oluşan çift bir değeri elde etmek için doldurulmuştur, doldurma, çıkış arabelleğine dahil edilir ve uygulama tarafından işlenmelidir.</span><span class="sxs-lookup"><span data-stu-id="51eee-276">If the encrypted data was padded to achieve an even multiple of the 3DES block size, the padding will be included in the output buffer and must be handled by the application.</span></span>

<span data-ttu-id="51eee-277">Bu işlem durum bilgilerini saklar ve 3DES denetim bloğunda anahtar malzemesini değiştirmez.</span><span class="sxs-lookup"><span data-stu-id="51eee-277">This operation does not keep state information, and does not alter the key material in the 3DES control block.</span></span>

### <a name="parameters"></a><span data-ttu-id="51eee-278">Parametreler</span><span class="sxs-lookup"><span data-stu-id="51eee-278">Parameters</span></span>

- <span data-ttu-id="51eee-279">**op** Gerçekleştirilecek işlemin türü.</span><span class="sxs-lookup"><span data-stu-id="51eee-279">**op** Type of operation to perform.</span></span> <span data-ttu-id="51eee-280">Geçerli işlemler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="51eee-280">Valid operations are:</span></span>
  - <span data-ttu-id="51eee-281">*NX_CRYPTO_ENCRYPT*</span><span class="sxs-lookup"><span data-stu-id="51eee-281">*NX_CRYPTO_ENCRYPT*</span></span>
  - <span data-ttu-id="51eee-282">*NX_CRYPTO_DECRYPT*</span><span class="sxs-lookup"><span data-stu-id="51eee-282">*NX_CRYPTO_DECRYPT*</span></span>
- <span data-ttu-id="51eee-283">**tanıtıcı** *_Nx_crypto_method_3des_init ()* tarafından başlatılan tanıtıcı.</span><span class="sxs-lookup"><span data-stu-id="51eee-283">**handle** The handle initialized by *_nx_crypto_method_3des_init()*.</span></span>
- <span data-ttu-id="51eee-284">**yöntemi** Geçerli 3DES şifreleme yöntemine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-284">**method** Pointer to the valid 3DES crypto method.</span></span> <span data-ttu-id="51eee-285">Burada kullanılan şifreleme yöntemi, *nx_crypto_method_3des_init ()* içinde kullanılan aynı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-285">The crypto method used here must be the same used in the *nx_crypto_method_3des_init().*</span></span>
- <span data-ttu-id="51eee-286">**input_data** Şifrelenmiş metin verileri içeren bir arabelleğe işaret eder.</span><span class="sxs-lookup"><span data-stu-id="51eee-286">**input_data** Points to a buffer containing encrypted text data.</span></span>
<span data-ttu-id="51eee-287">Giriş arabelleğinde kısıtlama yoktur.</span><span class="sxs-lookup"><span data-stu-id="51eee-287">There are not restrictions on input buffer.</span></span>
- <span data-ttu-id="51eee-288">**input_data_size** Giriş verilerinin bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-288">**input_data_size** Size of the input data, in bytes.</span></span> <span data-ttu-id="51eee-289">Giriş veri boyutu 8 baytın katlarından biri olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-289">The input data size must be a multiple of 8 bytes.</span></span>
- <span data-ttu-id="51eee-290">**iv_ptr** Ilk vektör işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="51eee-290">**iv_ptr** Pointer to the Initial Vector.</span></span> <span data-ttu-id="51eee-291">IV arabelleğinde kısıtlama yoktur.</span><span class="sxs-lookup"><span data-stu-id="51eee-291">There are no restrictions on the IV buffer.</span></span>
- <span data-ttu-id="51eee-292">**iv_size** Ilk vektör bloğunun boyutu, bayt cinsinden bu alanın 8 olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="51eee-292">**iv_size** Size of the Initial Vector block, in bytes This field must be 8.</span></span>
- <span data-ttu-id="51eee-293">**output_buffer** Şifresiz metin verilerini depolamak için 3DES bellek alanına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-293">**output_buffer** Pointer to the memory area for 3DES to store the clear text data.</span></span> <span data-ttu-id="51eee-294">Uygulama, çıkış arabelleği için alan ayırmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-294">Application must allocate space for the output buffer.</span></span> <span data-ttu-id="51eee-295">Çıkış arabelleği, giriş arabelleğiyle çakışabilir.</span><span class="sxs-lookup"><span data-stu-id="51eee-295">Output buffer may overlap with input buffer.</span></span> <span data-ttu-id="51eee-296">Aynı başlangıç adresini paylaştıkları takdirde çıkış arabelleği giriş arabelleğiyle çakışabilir.</span><span class="sxs-lookup"><span data-stu-id="51eee-296">The output buffer may overlap with the input buffer if they share the same starting address.</span></span>
- <span data-ttu-id="51eee-297">**output_buffer_size** Çıkış arabelleğinin bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-297">**output_buffer_size** Size of the output buffer in bytes.</span></span> <span data-ttu-id="51eee-298">Çıkış arabelleği boyutunun en az girdi arabellek boyutuyla aynı olması ve çıkış arabelleği boyutunun 8 baytın katlarından biri olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="51eee-298">Output buffer size must be at least the same of the input buffer size, and the output buffer size must be a multiple of 8 bytes.</span></span>
- <span data-ttu-id="51eee-299">**crypto_metadata** *_Nx_crypto_method_3des_init ()* IÇINDE kullanılan 3DES denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-299">**crypto_metadata** Pointer to the 3DES control block used in *_nx_crypto_method_3des_init()*.</span></span>
- <span data-ttu-id="51eee-300">**crypto_metadata_size** Crypto_metadata alanının bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-300">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="51eee-301">3DES için meta veri boyutu *sizeof olmalıdır (NX_3DES)*</span><span class="sxs-lookup"><span data-stu-id="51eee-301">For 3DES, the metadata size must be *sizeof(NX_3DES)*</span></span>
- <span data-ttu-id="51eee-302">**packet_ptr** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-302">**packet_ptr** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="51eee-303">Geçirilen tüm değerler sessizce yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="51eee-303">Any values passed in are silently ignored.</span></span>
- <span data-ttu-id="51eee-304">**nx_crypto_hw_process_callback** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-304">**nx_crypto_hw_process_callback** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="51eee-305">Geçirilen tüm değerler sessizce yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="51eee-305">Any values passed in are silently ignored.</span></span>

### <a name="description"></a><span data-ttu-id="51eee-306">Açıklama</span><span class="sxs-lookup"><span data-stu-id="51eee-306">Description</span></span>

<span data-ttu-id="51eee-307">Bu işlev 3DES şifrelemesini gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="51eee-307">This function performs 3DES encryption.</span></span> <span data-ttu-id="51eee-308">3DES denetim bloğunun _ *nx_crypto_moethod_3des_init ()* ile başlatılmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="51eee-308">The 3DES control block must have been initialized with _ *nx_crypto_moethod_3des_init()*.</span></span> <span data-ttu-id="51eee-309">Bu işlem durum bilgilerini saklar ve 3DES denetim bloğunda anahtar malzemesini değiştirmez.</span><span class="sxs-lookup"><span data-stu-id="51eee-309">This operation does not keep state information, and does not alter the key material in the 3DES control block.</span></span> <span data-ttu-id="51eee-310">Bu işlev tarafından, çağıranın, şifreleme işlemini çağırmadan önce doldurmayı işlemesi gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="51eee-310">Note that padding is not added by this function so the caller will need to handle padding before invoking the encryption operation.</span></span>

### <a name="return-values"></a><span data-ttu-id="51eee-311">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="51eee-311">Return Values</span></span>

- <span data-ttu-id="51eee-312">Anahtar ve anahtar boyutuyla 3DES denetim bloğunun başarılı bir şekilde başlatılması **NX_CRYPTO_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="51eee-312">**NX_CRYPTO_SUCCESS** (0x00) Successful initialization of the 3DES control block with the key and key size.</span></span>
- <span data-ttu-id="51eee-313">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-313">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="51eee-314">**NX_PTR_ERROR (0x07)** Anahtar için geçersiz işaretçi veya crypto_metadata ya da crypto_metadata_size geçersiz veya crypto_metadata 4 baytlık hizalı değil.</span><span class="sxs-lookup"><span data-stu-id="51eee-314">**NX_PTR_ERROR (0x07)** Invalid pointer to the key, or invalid crypto_metadata or crypto_metadata_size, or crypto_metadata is not 4-byte aligned.</span></span>

## <a name="_nx_crypto_method_3des_cleanup"></a><span data-ttu-id="51eee-315">_nx_crypto_method_3des_cleanup</span><span class="sxs-lookup"><span data-stu-id="51eee-315">_nx_crypto_method_3des_cleanup</span></span>

<span data-ttu-id="51eee-316">3DES denetim bloğunu temizleyin.</span><span class="sxs-lookup"><span data-stu-id="51eee-316">Clean up the 3DES control block.</span></span>

### <a name="prototype"></a><span data-ttu-id="51eee-317">Prototype</span><span class="sxs-lookup"><span data-stu-id="51eee-317">Prototype</span></span>

```c
UINT _nx_crypto_method_3des_cleanup(VOID *crypto_metadata);
```

### <a name="description"></a><span data-ttu-id="51eee-318">Açıklama</span><span class="sxs-lookup"><span data-stu-id="51eee-318">Description</span></span>

<span data-ttu-id="51eee-319">Uygulama, bu 3DES oturumunun daha sonra gerekli olmadığını belirlerse, 3DES denetim bloğunu temizlemek için bu işlevi çağırır.</span><span class="sxs-lookup"><span data-stu-id="51eee-319">Application calls this function to clean up the 3DES control block after it determines this 3DES session is no longer needed.</span></span>

### <a name="parameters"></a><span data-ttu-id="51eee-320">Parametreler</span><span class="sxs-lookup"><span data-stu-id="51eee-320">Parameters</span></span>

- <span data-ttu-id="51eee-321">**tanıtıcı** *_Nx_crypto_method_3des_init ()* tarafından başlatılan tanıtıcı.</span><span class="sxs-lookup"><span data-stu-id="51eee-321">**handle** The handle initialized by *_nx_crypto_method_3des_init()*.</span></span>

### <a name="return-values"></a><span data-ttu-id="51eee-322">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="51eee-322">Return Values</span></span>

- <span data-ttu-id="51eee-323">**NX_CRYPTO_SUCCESS** (0x00), 3Des oturumunun başarıyla temizlendi.</span><span class="sxs-lookup"><span data-stu-id="51eee-323">**NX_CRYPTO_SUCCESS** (0x00) Successfully cleaned up the 3DES session.</span></span>
- <span data-ttu-id="51eee-324">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-324">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>

## <a name="_nx_crypto_method_drbg_init"></a><span data-ttu-id="51eee-325">_nx_crypto_method_drbg_init</span><span class="sxs-lookup"><span data-stu-id="51eee-325">_nx_crypto_method_drbg_init</span></span>

<span data-ttu-id="51eee-326">DRBG şifreleme denetim bloğunu başlatır</span><span class="sxs-lookup"><span data-stu-id="51eee-326">Initializes the DRBG crypto control block</span></span>

### <a name="prototype"></a><span data-ttu-id="51eee-327">Prototype</span><span class="sxs-lookup"><span data-stu-id="51eee-327">Prototype</span></span>

```c
UINT _nx_crypto_method_drbg_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size);
```

### <a name="description"></a><span data-ttu-id="51eee-328">Açıklama</span><span class="sxs-lookup"><span data-stu-id="51eee-328">Description</span></span>

<span data-ttu-id="51eee-329">Bu işlev, DRBG denetim bloğunu verilen anahtar dizesiyle başlatır.</span><span class="sxs-lookup"><span data-stu-id="51eee-329">This function initializes the DRBG control block with the given key string.</span></span> <span data-ttu-id="51eee-330">DRBG denetim bloğu başlatıldıktan sonra, sonraki DRBG işlemi aynı denetim bloğunu kullanıyor olacaktır.</span><span class="sxs-lookup"><span data-stu-id="51eee-330">Once the DRBG control block is initialized, subsequent DRBG operation shall be using the same control block.</span></span>

<span data-ttu-id="51eee-331">Uygulama birden çok DRBG denetim bloğu oluşturabilir, her biri bir oturumu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="51eee-331">Application may create multiple DRBG control blocks, each represents a session.</span></span> <span data-ttu-id="51eee-332">DRBG denetim bloğunun başlatılması yeni bir karma hesaplama oturumu başlatır.</span><span class="sxs-lookup"><span data-stu-id="51eee-332">Initializing the DRBG control block starts a new hash computation session.</span></span> <span data-ttu-id="51eee-333">DRBG denetim bloğunu yeniden başlatmak geçerli oturum ve yıldızların yeni bir kopyasını terk eden.</span><span class="sxs-lookup"><span data-stu-id="51eee-333">Re-initializing the DRBG control block abandons the current session and stars a new one.</span></span>

### <a name="parameters"></a><span data-ttu-id="51eee-334">Parametreler</span><span class="sxs-lookup"><span data-stu-id="51eee-334">Parameters</span></span>

- <span data-ttu-id="51eee-335">**yöntemi** Geçerli bir DRBG şifreleme yöntemi denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-335">**method** Pointer to a valid DRBG crypto method control block.</span></span> <span data-ttu-id="51eee-336">Aşağıdaki önceden tanımlanmış şifreleme yöntemleri kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="51eee-336">The following pre-defined crypto methods are available:</span></span>
  - <span data-ttu-id="51eee-337">*crypto_method_drbg*</span><span class="sxs-lookup"><span data-stu-id="51eee-337">*crypto_method_drbg*</span></span>
- <span data-ttu-id="51eee-338">**anahtar** Bu alan DRBG için kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-338">**key** This field is not used for DRBG.</span></span>
- <span data-ttu-id="51eee-339">**key_size_in_bits** Bu alan DRBG için kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-339">**key_size_in_bits** This field is not used for DRBG.</span></span>
- <span data-ttu-id="51eee-340">**tanıtıcı** Bu hizmet, çağırana bir tanıtıcı döndürür.</span><span class="sxs-lookup"><span data-stu-id="51eee-340">**handle** This service returns a handle to the caller.</span></span> <span data-ttu-id="51eee-341">Tanıtıcı uygulamaya bağımlıdır ve bu uygulamada kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="51eee-341">The handle is implementation-dependent and is not being used in this implementation.</span></span> <span data-ttu-id="51eee-342">Uygulama tanıtıcı için NULL değer geçirecektir.</span><span class="sxs-lookup"><span data-stu-id="51eee-342">Application shall pass NULL for the handle.</span></span>
- <span data-ttu-id="51eee-343">**crypto_metadata** DRBG denetim bloğu için geçerli bir bellek alanı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="51eee-343">**crypto_metadata** Pointer to a valid memory space for the DRBG control block.</span></span> <span data-ttu-id="51eee-344">Bellek alanının başlangıç adresi 4 bayt hizalı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-344">The starting address of the memory space must be 4-byte aligned.</span></span>
- <span data-ttu-id="51eee-345">**crypto_metadata_size** Crypto_metadata alanının bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-345">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="51eee-346">DRBG için meta veri boyutu *sizeof olmalıdır (NX_CRYPTO_DRBG)*</span><span class="sxs-lookup"><span data-stu-id="51eee-346">For DRBG, the metadata size must be *sizeof(NX_CRYPTO_DRBG)*</span></span>

### <a name="return-values"></a><span data-ttu-id="51eee-347">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="51eee-347">Return Values</span></span>

- <span data-ttu-id="51eee-348">Anahtar ve anahtar boyutuyla DRBG denetim bloğunun başarılı bir şekilde başlatılması **NX_CRYPTO_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="51eee-348">**NX_CRYPTO_SUCCESS** (0x00) Successful initialization of the DRBG control block with the key and key size.</span></span>
- <span data-ttu-id="51eee-349">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-349">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="51eee-350">**NX_PTR_ERROR** (0x07) anahtar için geçersiz işaretçi veya geçersiz crypto_metadata veya crypto_metadata_size ya da crypto_metadata 4 bayt hizalı değil.</span><span class="sxs-lookup"><span data-stu-id="51eee-350">**NX_PTR_ERROR** (0x07) Invalid pointer to the key, or invalid crypto_metadata or crypto_metadata_size, or crypto_metadata is not 4-byte aligned.</span></span>

## <a name="_nx_crypto_method_drbg_operation"></a><span data-ttu-id="51eee-351">_nx_crypto_method_drbg_operation</span><span class="sxs-lookup"><span data-stu-id="51eee-351">_nx_crypto_method_drbg_operation</span></span>

<span data-ttu-id="51eee-352">DRBG işlemi gerçekleştir</span><span class="sxs-lookup"><span data-stu-id="51eee-352">Perform DRBG operation</span></span>

### <a name="prototype"></a><span data-ttu-id="51eee-353">Prototype</span><span class="sxs-lookup"><span data-stu-id="51eee-353">Prototype</span></span>

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

### <a name="description"></a><span data-ttu-id="51eee-354">Açıklama</span><span class="sxs-lookup"><span data-stu-id="51eee-354">Description</span></span>

<span data-ttu-id="51eee-355">Bu işlev DRBG işlemini gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="51eee-355">This function performs DRBG operation.</span></span> <span data-ttu-id="51eee-356">DRBG denetim bloğunun _ *nx_crypto_method_drbg_init ()* ile başlatılmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="51eee-356">The DRBG control block must have been initialized with _ *nx_crypto_method_drbg_init()*.</span></span> <span data-ttu-id="51eee-357">Gerçekleştirilecek DRBG algoritması, *Yöntem* denetim bloğunda belirtilen algoritmayı temel alır.</span><span class="sxs-lookup"><span data-stu-id="51eee-357">The DRBG algorithm to be performed is based on the algorithm specified in the *method* control block.</span></span> <span data-ttu-id="51eee-358">Varsayılan olarak, DRBG için AES-128 kullanılır.</span><span class="sxs-lookup"><span data-stu-id="51eee-358">By default AES-128 is used for DRBG.</span></span>

<span data-ttu-id="51eee-359">İşlem NX_CRYPTO_DRBG_OPTIONS_SET olduğunda, giriş NX_CRYPTO_DRBG_OPTIONS yapısına işaret eder.</span><span class="sxs-lookup"><span data-stu-id="51eee-359">When the operation is NX_CRYPTO_DRBG_OPTIONS_SET, the input points to NX_CRYPTO_DRBG_OPTIONS structure.</span></span> <span data-ttu-id="51eee-360">İşlem NX_CRYPTO_DRBG_INSTANTIATE olduğunda, anahtar nonce 'e işaret eder, giriş noktaları kişiselleştirme dizesine işaret eder.</span><span class="sxs-lookup"><span data-stu-id="51eee-360">When the operation is NX_CRYPTO_DRBG_INSTANTIATE, the key points to nonce, input points to personalization string.</span></span> <span data-ttu-id="51eee-361">İşlem NX_CRYPTO_DRBG_RESEED veya NX_CRYPTO_DRBG_GENERATE, giriş ek girişe işaret eder.</span><span class="sxs-lookup"><span data-stu-id="51eee-361">When the operation is NX_CRYPTO_DRBG_RESEED or NX_CRYPTO_DRBG_GENERATE, the input points to additional input.</span></span>

### <a name="parameters"></a><span data-ttu-id="51eee-362">Parametreler</span><span class="sxs-lookup"><span data-stu-id="51eee-362">Parameters</span></span>

- <span data-ttu-id="51eee-363">**op** Gerçekleştirilecek işlemin türü.</span><span class="sxs-lookup"><span data-stu-id="51eee-363">**op** Type of operation to perform.</span></span> <span data-ttu-id="51eee-364">Geçerli işlem:</span><span class="sxs-lookup"><span data-stu-id="51eee-364">Valid operation is:</span></span>
  - <span data-ttu-id="51eee-365">*NX_CRYPTO_DRBG_OPTIONS_SET*</span><span class="sxs-lookup"><span data-stu-id="51eee-365">*NX_CRYPTO_DRBG_OPTIONS_SET*</span></span>
  - <span data-ttu-id="51eee-366">*NX_CRYPTO_DRBG_INSTANTIATE*</span><span class="sxs-lookup"><span data-stu-id="51eee-366">*NX_CRYPTO_DRBG_INSTANTIATE*</span></span>
  - <span data-ttu-id="51eee-367">*NX_CRYPTO_DRBG_RESEED NX_CRYPTO_DRBG_GENERATE*</span><span class="sxs-lookup"><span data-stu-id="51eee-367">*NX_CRYPTO_DRBG_RESEED NX_CRYPTO_DRBG_GENERATE*</span></span>
- <span data-ttu-id="51eee-368">**tanıtıcı** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-368">**handle** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="51eee-369">Geçirilen tüm değerler sessizce yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="51eee-369">Any values passed in are silently ignored.</span></span>
- <span data-ttu-id="51eee-370">**yöntemi** Geçerli DRBG şifre yöntemine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-370">**method** Pointer to the valid DRBG crypto method.</span></span> <span data-ttu-id="51eee-371">Burada kullanılan şifreleme yöntemi _ *nx_crypto_method_drbg_init ()* içinde kullanılan aynı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-371">The crypto method used here must be the same used in the _ *nx_crypto_method_drbg_init().*</span></span>
- <span data-ttu-id="51eee-372">**anahtar** Örnek oluşturma işlemi için nonce işaretçisine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-372">**key** Pointer to the the nonce for the instantiate operation.</span></span> <span data-ttu-id="51eee-373">Bu alan diğer işlemler için kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-373">This field is not used for other operations.</span></span>
- <span data-ttu-id="51eee-374">**key_size_in_bits** Nonce 'in bit cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-374">**key_size_in_bits** Size of the nonce, in bits.</span></span> <span data-ttu-id="51eee-375">Bu alan diğer işlemler için kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-375">This field is not used for other operations.</span></span>
- <span data-ttu-id="51eee-376">**giriş** Op NX_CRYPTO_DRBG_OPTIONS_SET olduğunda, bu alan DRBG seçeneklerine işaret eder.</span><span class="sxs-lookup"><span data-stu-id="51eee-376">**input** When op is NX_CRYPTO_DRBG_OPTIONS_SET, this field points to DRBG options.</span></span> <span data-ttu-id="51eee-377">Op NX_CRYPTO_DRBG_INSTANTIATE olduğunda, bu alan kişiselleştirme dizesine işaret eder.</span><span class="sxs-lookup"><span data-stu-id="51eee-377">When op is NX_CRYPTO_DRBG_INSTANTIATE, this field points to personalization string.</span></span> <span data-ttu-id="51eee-378">Op NX_CRYPTO_DRBG_RESEED veya NX_CRYPTO_DRBG_GENERATE olduğunda, bu alan ek giriş verilerine işaret eder.</span><span class="sxs-lookup"><span data-stu-id="51eee-378">When op is NX_CRYPTO_DRBG_RESEED or NX_CRYPTO_DRBG_GENERATE, this field points to additional input data.</span></span>
- <span data-ttu-id="51eee-379">**input_length_in_byte** Giriş verilerinin bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-379">**input_length_in_byte** Size of the input data, in bytes.</span></span>
- <span data-ttu-id="51eee-380">**iv_ptr** Bu alan DRBG için kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-380">**iv_ptr** This field is not used for DRBG.</span></span>
- <span data-ttu-id="51eee-381">**Çıkış** Op NX_CRYPTO_DRBG_GENERATE olduğunda, bu alan oluşturulan DRBG için bellek alanını gösterir.</span><span class="sxs-lookup"><span data-stu-id="51eee-381">**output** When op is NX_CRYPTO_DRBG_GENERATE, this field points to the memory area for the generated DRBG.</span></span> <span data-ttu-id="51eee-382">Aksi takdirde, bu alan kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-382">Otherwise, this field is not used.</span></span>
- <span data-ttu-id="51eee-383">**output_length_in_byte** Çıkış arabelleğinin bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-383">**output_length_in_byte** Size of the output buffer in bytes.</span></span>
- <span data-ttu-id="51eee-384">**crypto_metadata** *_Nx_crypto_method_drbg_init ()* içinde kullanılan drbg denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-384">**crypto_metadata** Pointer to the DRBG control block used in *_nx_crypto_method_drbg_init()*.</span></span>
- <span data-ttu-id="51eee-385">**crypto_metadata_size** Crypto_metadata alanının bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-385">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="51eee-386">DRBG için meta veri boyutu *sizeof (NX_CRYPTO_DRBG)* olmalıdır</span><span class="sxs-lookup"><span data-stu-id="51eee-386">For DRBG, the metadata size must *sizeof(NX_CRYPTO_DRBG)*</span></span>
- <span data-ttu-id="51eee-387">**packet_ptr** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-387">**packet_ptr** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="51eee-388">Geçirilen tüm değerler sessizce yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="51eee-388">Any values passed in are silently ignored.</span></span>
- <span data-ttu-id="51eee-389">**nx_crypto_hw_process_callback** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-389">**nx_crypto_hw_process_callback** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="51eee-390">Geçirilen tüm değerler sessizce yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="51eee-390">Any values passed in are silently ignored.</span></span>

### <a name="return-values"></a><span data-ttu-id="51eee-391">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="51eee-391">Return Values</span></span>

- <span data-ttu-id="51eee-392">**NX_CRYPTO_SUCCESS** (0x00) drbg işlemi başarıyla yürütüldü.</span><span class="sxs-lookup"><span data-stu-id="51eee-392">**NX_CRYPTO_SUCCESS** (0x00) Successfully executed the DRBG operation.</span></span>
- <span data-ttu-id="51eee-393">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-393">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="51eee-394">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi veya uzunluğu geçersiz.</span><span class="sxs-lookup"><span data-stu-id="51eee-394">**NX_PTR_ERROR** (0x07) Invalid input pointer or invalid length.</span></span>
- <span data-ttu-id="51eee-395">**NX_CRYPTO_INVALID_ALGORITHM** (0x20004) geçersiz drbg algoritması belirtildi.</span><span class="sxs-lookup"><span data-stu-id="51eee-395">**NX_CRYPTO_INVALID_ALGORITHM** (0x20004) Invalid DRBG algorithm being specified.</span></span>
- <span data-ttu-id="51eee-396">**NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) geçersiz çıkış arabelleği boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-396">**NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) Invalid output buffer size.</span></span>

## <a name="_nx_crypto_method_drbg_cleanup"></a><span data-ttu-id="51eee-397">_nx_crypto_method_drbg_cleanup</span><span class="sxs-lookup"><span data-stu-id="51eee-397">_nx_crypto_method_drbg_cleanup</span></span>

<span data-ttu-id="51eee-398">DRBG denetim bloğunu temizleyin.</span><span class="sxs-lookup"><span data-stu-id="51eee-398">Clean up the DRBG control block.</span></span>

### <a name="prototype"></a><span data-ttu-id="51eee-399">Prototype</span><span class="sxs-lookup"><span data-stu-id="51eee-399">Prototype</span></span>

```c
UINT _nx_crypto_method_drbg_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a><span data-ttu-id="51eee-400">Açıklama</span><span class="sxs-lookup"><span data-stu-id="51eee-400">Description</span></span>

<span data-ttu-id="51eee-401">Uygulama, bu DRBG oturumunun artık gerekli olmadığını belirlediğinde DRBG denetim bloğunu temizlemek için bu işlevi çağırır.</span><span class="sxs-lookup"><span data-stu-id="51eee-401">Application calls this function to clean up the DRBG control block after it determines this DRBG session is no longer needed.</span></span>

### <a name="parameters"></a><span data-ttu-id="51eee-402">Parametreler</span><span class="sxs-lookup"><span data-stu-id="51eee-402">Parameters</span></span>

- <span data-ttu-id="51eee-403">**crypto_metadata** *_Nx_crypto_method_drbg_init ()* içinde kullanılan drbg denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-403">**crypto_metadata** Pointer to the DRBG control block used in *_nx_crypto_method_drbg_init()*.</span></span>

### <a name="return-values"></a><span data-ttu-id="51eee-404">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="51eee-404">Return Values</span></span>

- <span data-ttu-id="51eee-405">**NX_CRYPTO_SUCCESS** (0x00) drbg oturumunun başarıyla temizlendi.</span><span class="sxs-lookup"><span data-stu-id="51eee-405">**NX_CRYPTO_SUCCESS** (0x00) Successfully cleaned up the DRBG session.</span></span>
- <span data-ttu-id="51eee-406">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-406">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>

## <a name="_nx_crypto_method_ecdh_init"></a><span data-ttu-id="51eee-407">_nx_crypto_method_ecdh_init</span><span class="sxs-lookup"><span data-stu-id="51eee-407">_nx_crypto_method_ecdh_init</span></span>

<span data-ttu-id="51eee-408">ECDH şifre denetim bloğunu başlatır</span><span class="sxs-lookup"><span data-stu-id="51eee-408">Initializes the ECDH crypto control block</span></span>

### <a name="prototype"></a><span data-ttu-id="51eee-409">Prototype</span><span class="sxs-lookup"><span data-stu-id="51eee-409">Prototype</span></span>

```c
UINT _nx_crypto_method_ecdh_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size);
```

### <a name="description"></a><span data-ttu-id="51eee-410">Açıklama</span><span class="sxs-lookup"><span data-stu-id="51eee-410">Description</span></span>

<span data-ttu-id="51eee-411">Bu işlev, ECDH denetim bloğunu verilen anahtar dizesiyle başlatır.</span><span class="sxs-lookup"><span data-stu-id="51eee-411">This function initializes the ECDH control block with the given key string.</span></span> <span data-ttu-id="51eee-412">ECDH denetim bloğu başlatıldıktan sonra, sonraki ECDH işlemi aynı denetim bloğunu kullanıyor olacaktır.</span><span class="sxs-lookup"><span data-stu-id="51eee-412">Once the ECDH control block is initialized, subsequent ECDH operation shall be using the same control block.</span></span>

<span data-ttu-id="51eee-413">Uygulama birden fazla ECDH denetim bloğu oluşturabilir, her biri bir oturumu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="51eee-413">Application may create multiple ECDH control blocks, each represents a session.</span></span> <span data-ttu-id="51eee-414">ECDH denetim bloğunun başlatılması yeni bir karma hesaplama oturumu başlatır.</span><span class="sxs-lookup"><span data-stu-id="51eee-414">Initializing the ECDH control block starts a new hash computation session.</span></span> <span data-ttu-id="51eee-415">ECDH denetim bloğunu yeniden başlatmak, geçerli oturumu ve yıldızları yeni bir kez terk edin.</span><span class="sxs-lookup"><span data-stu-id="51eee-415">Re-initializing the ECDH control block abandons the current session and stars a new one.</span></span>

### <a name="parameters"></a><span data-ttu-id="51eee-416">Parametreler</span><span class="sxs-lookup"><span data-stu-id="51eee-416">Parameters</span></span>

- <span data-ttu-id="51eee-417">**yöntemi** Geçerli bir ECDH şifreleme yöntemi denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-417">**method** Pointer to a valid ECDH crypto method control block.</span></span> <span data-ttu-id="51eee-418">Aşağıdaki önceden tanımlanmış şifreleme yöntemleri kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="51eee-418">The following pre-defined crypto methods are available:</span></span>
  - <span data-ttu-id="51eee-419">*crypto_method_ecdh*</span><span class="sxs-lookup"><span data-stu-id="51eee-419">*crypto_method_ecdh*</span></span>
- <span data-ttu-id="51eee-420">**anahtar** Bu alan ECDH için kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-420">**key** This field is not used for ECDH.</span></span>
- <span data-ttu-id="51eee-421">**key_size_in_bits** Bu alan ECDH için kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-421">**key_size_in_bits** This field is not used for ECDH.</span></span>
- <span data-ttu-id="51eee-422">**tanıtıcı** Bu hizmet, çağırana bir tanıtıcı döndürür.</span><span class="sxs-lookup"><span data-stu-id="51eee-422">**handle** This service returns a handle to the caller.</span></span> <span data-ttu-id="51eee-423">Tanıtıcı uygulamaya bağımlıdır ve bu uygulamada kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="51eee-423">The handle is implementation-dependent and is not being used in this implementation.</span></span> <span data-ttu-id="51eee-424">Uygulama tanıtıcı için NULL değer geçirecektir.</span><span class="sxs-lookup"><span data-stu-id="51eee-424">Application shall pass NULL for the handle.</span></span>
- <span data-ttu-id="51eee-425">**crypto_metadata** ECDH denetim bloğu için geçerli bir bellek alanı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="51eee-425">**crypto_metadata** Pointer to a valid memory space for the ECDH control block.</span></span> <span data-ttu-id="51eee-426">Bellek alanının başlangıç adresi 4 bayt hizalı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-426">The starting address of the memory space must be 4-byte aligned.</span></span>
- <span data-ttu-id="51eee-427">**crypto_metadata_size** Crypto_metadata alanının bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-427">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="51eee-428">ECDH için meta veri boyutu *sizeof olmalıdır (NX_CRYPTO_ECDH)*</span><span class="sxs-lookup"><span data-stu-id="51eee-428">For ECDH, the metadata size must be *sizeof(NX_CRYPTO_ECDH)*</span></span>

### <a name="return-values"></a><span data-ttu-id="51eee-429">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="51eee-429">Return Values</span></span>

- <span data-ttu-id="51eee-430">Anahtar ve anahtar boyutuyla ECDH denetim bloğunun başarılı bir şekilde başlatılması **NX_CRYPTO_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="51eee-430">**NX_CRYPTO_SUCCESS** (0x00) Successful initialization of the ECDH control block with the key and key size.</span></span>
- <span data-ttu-id="51eee-431">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-431">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="51eee-432">**NX_PTR_ERROR** (0x07) anahtar için geçersiz işaretçi veya geçersiz crypto_metadata veya crypto_metadata_size ya da crypto_metadata 4 bayt hizalı değil.</span><span class="sxs-lookup"><span data-stu-id="51eee-432">**NX_PTR_ERROR** (0x07) Invalid pointer to the key, or invalid crypto_metadata or crypto_metadata_size, or crypto_metadata is not 4-byte aligned.</span></span>

## <a name="_nx_crypto_method_ecdh_operation"></a><span data-ttu-id="51eee-433">_nx_crypto_method_ecdh_operation</span><span class="sxs-lookup"><span data-stu-id="51eee-433">_nx_crypto_method_ecdh_operation</span></span>

<span data-ttu-id="51eee-434">ECDH işlemi gerçekleştir</span><span class="sxs-lookup"><span data-stu-id="51eee-434">Perform ECDH operation</span></span>

### <a name="prototype"></a><span data-ttu-id="51eee-435">Prototype</span><span class="sxs-lookup"><span data-stu-id="51eee-435">Prototype</span></span>

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

### <a name="description"></a><span data-ttu-id="51eee-436">Açıklama</span><span class="sxs-lookup"><span data-stu-id="51eee-436">Description</span></span>

<span data-ttu-id="51eee-437">Bu işlev ECDH işlemini gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="51eee-437">This function performs ECDH operation.</span></span> <span data-ttu-id="51eee-438">ECDH denetim bloğunun _ *nx_crypto_method_ecdh_init ()* ile başlatılmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="51eee-438">The ECDH control block must have been initialized with _ *nx_crypto_method_ecdh_init()*.</span></span> <span data-ttu-id="51eee-439">Gerçekleştirilecek ECDH algoritması, *Yöntem* denetim bloğunda belirtilen algoritmayı temel alır.</span><span class="sxs-lookup"><span data-stu-id="51eee-439">The ECDH algorithm to be performed is based on the algorithm specified in the *method* control block.</span></span>

<span data-ttu-id="51eee-440">İşlem NX_CRYPTO_EC_CURVE_SET olduğunda, giriş Eliptik Eğri Şifreleme yöntemine işaret eder.</span><span class="sxs-lookup"><span data-stu-id="51eee-440">When the operation is NX_CRYPTO_EC_CURVE_SET, the input points to Elliptic Curve crypto method.</span></span> <span data-ttu-id="51eee-441">İşlem NX_CRYPTO_EC_KEY_PAIR_GENERATE olduğunda, çıkış NX_CRYPTO_EXTENDED_OUTPUT yapısına işaret eder ve anahtar çifti nx_crypto_extended_output_data kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="51eee-441">When the operation is NX_CRYPTO_EC_KEY_PAIR_GENERATE, the output points to NX_CRYPTO_EXTENDED_OUTPUT structure and the key pair is copied to nx_crypto_extended_output_data.</span></span> <span data-ttu-id="51eee-442">İşlem NX_CRYPTO_DH_SETUP olduğunda, ortak anahtar nx_crypto_extended_output_data döndürülür.</span><span class="sxs-lookup"><span data-stu-id="51eee-442">When the operation is NX_CRYPTO_DH_SETUP, the public key is returned to nx_crypto_extended_output_data.</span></span> <span data-ttu-id="51eee-443">İşlem NX_CRYPTO_DH_KEY_PAIR_IMPORT olduğunda, girişte ortak anahtar ve anahtar noktaları özel anahtara işaret eder.</span><span class="sxs-lookup"><span data-stu-id="51eee-443">When the operation is NX_CRYPTO_DH_KEY_PAIR_IMPORT, the input points to public key and key points to private key.</span></span> <span data-ttu-id="51eee-444">İşlem NX_CRYPTO_DH_PRIVATE_KEY_EXPORT, özel anahtar nx_crypto_extended_output_data kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="51eee-444">When the operation is NX_CRYPTO_DH_PRIVATE_KEY_EXPORT, the private key is copied to nx_crypto_extended_output_data.</span></span> <span data-ttu-id="51eee-445">İşlem NX_CRYPTO_DH_CALCULATE olduğunda, giriş uzak ortak anahtara ve paylaşılan gizliliğe nx_crypto_extended_output_data kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="51eee-445">When the operation is NX_CRYPTO_DH_CALCULATE, the input points to remote public key and the shared secret is copied to nx_crypto_extended_output_data.</span></span>

### <a name="parameters"></a><span data-ttu-id="51eee-446">Parametreler</span><span class="sxs-lookup"><span data-stu-id="51eee-446">Parameters</span></span>

- <span data-ttu-id="51eee-447">**op** Gerçekleştirilecek işlemin türü.</span><span class="sxs-lookup"><span data-stu-id="51eee-447">**op** Type of operation to perform.</span></span> <span data-ttu-id="51eee-448">Geçerli işlem:</span><span class="sxs-lookup"><span data-stu-id="51eee-448">Valid operation is:</span></span>
  - <span data-ttu-id="51eee-449">*NX_CRYPTO_EC_CURVE_SET*</span><span class="sxs-lookup"><span data-stu-id="51eee-449">*NX_CRYPTO_EC_CURVE_SET*</span></span>
  - <span data-ttu-id="51eee-450">*NX_CRYPTO_DH_SETUP*</span><span class="sxs-lookup"><span data-stu-id="51eee-450">*NX_CRYPTO_DH_SETUP*</span></span>
  - <span data-ttu-id="51eee-451">*NX_CRYPTO_DH_CALCULATE*</span><span class="sxs-lookup"><span data-stu-id="51eee-451">*NX_CRYPTO_DH_CALCULATE*</span></span>
  - <span data-ttu-id="51eee-452">*NX_CRYPTO_DH_KEY_PAIR_IMPOPRT*</span><span class="sxs-lookup"><span data-stu-id="51eee-452">*NX_CRYPTO_DH_KEY_PAIR_IMPOPRT*</span></span>
  - <span data-ttu-id="51eee-453">*NX_CRYPTO_DH_KEY_PAIR_GENERATE*</span><span class="sxs-lookup"><span data-stu-id="51eee-453">*NX_CRYPTO_DH_KEY_PAIR_GENERATE*</span></span>
  - <span data-ttu-id="51eee-454">*NX_CRYPTO_DH_PRIVATE_KEY_EXPORT*</span><span class="sxs-lookup"><span data-stu-id="51eee-454">*NX_CRYPTO_DH_PRIVATE_KEY_EXPORT*</span></span>
- <span data-ttu-id="51eee-455">**tanıtıcı** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-455">**handle** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="51eee-456">Geçirilen tüm değerler sessizce yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="51eee-456">Any values passed in are silently ignored.</span></span>
- <span data-ttu-id="51eee-457">**yöntemi** Geçerli ECDH şifre yöntemine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-457">**method** Pointer to the valid ECDH crypto method.</span></span> <span data-ttu-id="51eee-458">Burada kullanılan şifreleme yöntemi _ *nx_crypto_method_ecdh_init ()* içinde kullanılan aynı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-458">The crypto method used here must be the same used in the _ *nx_crypto_method_ecdh_init().*</span></span>
- <span data-ttu-id="51eee-459">**anahtar** Op NX_CRYPTO_DH_IMPORT_KEY_PAIR olduğunda, bu alan özel anahtara işaret eder.</span><span class="sxs-lookup"><span data-stu-id="51eee-459">**key** When op is NX_CRYPTO_DH_IMPORT_KEY_PAIR, this field points to private key.</span></span> <span data-ttu-id="51eee-460">Aksi takdirde, bu alan ECDH için kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-460">Otherwise, this field is not used for ECDH.</span></span>
- <span data-ttu-id="51eee-461">**key_size_in_bits** Anahtarın bit cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-461">**key_size_in_bits** Size of the key, in bits.</span></span>
- <span data-ttu-id="51eee-462">**giriş** Op NX_CRYPTO_EC_CURVE_SET olduğunda, bu alan Eliptik Eğri Şifreleme yöntemine işaret eder.</span><span class="sxs-lookup"><span data-stu-id="51eee-462">**input** When op is NX_CRYPTO_EC_CURVE_SET, this field points to Elliptic Curve crypto method.</span></span> <span data-ttu-id="51eee-463">Op NX_CRYPTO_DH_SETUP olduğunda, bu alan kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-463">When op is NX_CRYPTO_DH_SETUP, this field is not used.</span></span> <span data-ttu-id="51eee-464">Op NX_CRYPTO_DH_CALCULATE olduğunda, bu alan girdi metin verileri içeren bir arabelleğe işaret eder.</span><span class="sxs-lookup"><span data-stu-id="51eee-464">When op is NX_CRYPTO_DH_CALCULATE, this field points to a buffer containing input text data.</span></span> <span data-ttu-id="51eee-465">Op NX_CRYPTO_DH_IMPORT_KEY_PAIR olduğunda, bu alan ortak anahtara işaret eder.</span><span class="sxs-lookup"><span data-stu-id="51eee-465">When op is NX_CRYPTO_DH_IMPORT_KEY_PAIR, this field points to public key.</span></span>
- <span data-ttu-id="51eee-466">**input_length_in_byte** Giriş verilerinin bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-466">**input_length_in_byte** Size of the input data, in bytes.</span></span>
- <span data-ttu-id="51eee-467">**iv_ptr** Bu alan ECDH için kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-467">**iv_ptr** This field is not used for ECDH.</span></span>
- <span data-ttu-id="51eee-468">**Çıkış** Op NX_CRYPTO_EC_CURVE_SET veya NX_CRYPTO_DH_IMPORT_KEY_PAIR, bu alan kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-468">**output** When op is NX_CRYPTO_EC_CURVE_SET or NX_CRYPTO_DH_IMPORT_KEY_PAIR, this field is not used.</span></span> <span data-ttu-id="51eee-469">Op NX_CRYPTO_DH_SETUP olduğunda, bu alan oluşturulan ECDH ortak anahtarı için bellek alanını gösterir.</span><span class="sxs-lookup"><span data-stu-id="51eee-469">When op is NX_CRYPTO_DH_SETUP, this field points to the memory area for the generated ECDH public key.</span></span> <span data-ttu-id="51eee-470">Op NX_CRYPTO_DH_CALCULATE olduğunda, bu alan oluşturulan ECDH paylaşılan gizliliğiyle ilgili bellek alanını gösterir.</span><span class="sxs-lookup"><span data-stu-id="51eee-470">When op is NX_CRYPTO_DH_CALCULATE, this field points to the memory area for the generated ECDH shared secret.</span></span>
- <span data-ttu-id="51eee-471">**output_length_in_byte** Çıkış arabelleğinin bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-471">**output_length_in_byte** Size of the output buffer in bytes.</span></span>
- <span data-ttu-id="51eee-472">**crypto_metadata** *_Nx_crypto_method_ecdh_init ()* içinde kullanılan ECDH denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-472">**crypto_metadata** Pointer to the ECDH control block used in *_nx_crypto_method_ecdh_init()*.</span></span>
- <span data-ttu-id="51eee-473">**crypto_metadata_size** Crypto_metadata alanının bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-473">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="51eee-474">ECDH için meta veri boyutu sizeof olmalıdır *(NX_CRYPTO_ECDH)*</span><span class="sxs-lookup"><span data-stu-id="51eee-474">For ECDH, the metadata size must *sizeof(NX_CRYPTO_ECDH)*</span></span>
- <span data-ttu-id="51eee-475">**packet_ptr** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-475">**packet_ptr** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="51eee-476">Geçirilen tüm değerler sessizce yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="51eee-476">Any values passed in are silently ignored.</span></span>
- <span data-ttu-id="51eee-477">**nx_crypto_hw_process_callback** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-477">**nx_crypto_hw_process_callback** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="51eee-478">Geçirilen tüm değerler sessizce yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="51eee-478">Any values passed in are silently ignored.</span></span>

### <a name="return-values"></a><span data-ttu-id="51eee-479">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="51eee-479">Return Values</span></span>

- <span data-ttu-id="51eee-480">**NX_CRYPTO_SUCCESS** (0x00) ECDH işlemi başarıyla yürütüldü.</span><span class="sxs-lookup"><span data-stu-id="51eee-480">**NX_CRYPTO_SUCCESS** (0x00) Successfully executed the ECDH operation.</span></span>
- <span data-ttu-id="51eee-481">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-481">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="51eee-482">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi veya uzunluğu geçersiz.</span><span class="sxs-lookup"><span data-stu-id="51eee-482">**NX_PTR_ERROR** (0x07) Invalid input pointer or invalid length.</span></span>
- <span data-ttu-id="51eee-483">**NX_CRYPTO_INVALID_ALGORITHM** (0x20004) geçersiz ECDH algoritması belirtildi.</span><span class="sxs-lookup"><span data-stu-id="51eee-483">**NX_CRYPTO_INVALID_ALGORITHM** (0x20004) Invalid ECDH algorithm being specified.</span></span>
- <span data-ttu-id="51eee-484">**NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) geçersiz çıkış arabelleği boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-484">**NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) Invalid output buffer size.</span></span>

## <a name="_nx_crypto_method_ecdh_cleanup"></a><span data-ttu-id="51eee-485">_nx_crypto_method_ecdh_cleanup</span><span class="sxs-lookup"><span data-stu-id="51eee-485">_nx_crypto_method_ecdh_cleanup</span></span>

<span data-ttu-id="51eee-486">ECDH denetim bloğunu temizleyin.</span><span class="sxs-lookup"><span data-stu-id="51eee-486">Clean up the ECDH control block.</span></span>

### <a name="prototype"></a><span data-ttu-id="51eee-487">Prototype</span><span class="sxs-lookup"><span data-stu-id="51eee-487">Prototype</span></span>

```c
UINT _nx_crypto_method_ecdh_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a><span data-ttu-id="51eee-488">Açıklama</span><span class="sxs-lookup"><span data-stu-id="51eee-488">Description</span></span>

<span data-ttu-id="51eee-489">Uygulama, bu ECDH oturumu artık gerekli olmadığını belirledikten sonra ECDH denetim bloğunu temizlemek için bu işlevi çağırır.</span><span class="sxs-lookup"><span data-stu-id="51eee-489">Application calls this function to clean up the ECDH control block after it determines this ECDH session is no longer needed.</span></span>

### <a name="parameters"></a><span data-ttu-id="51eee-490">Parametreler</span><span class="sxs-lookup"><span data-stu-id="51eee-490">Parameters</span></span>

- <span data-ttu-id="51eee-491">**crypto_metadata** *_Nx_crypto_method_ecdh_init ()* içinde kullanılan ECDH denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-491">**crypto_metadata** Pointer to the ECDH control block used in *_nx_crypto_method_ecdh_init()*.</span></span>

### <a name="return-values"></a><span data-ttu-id="51eee-492">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="51eee-492">Return Values</span></span>

- <span data-ttu-id="51eee-493">**NX_CRYPTO_SUCCESS** (0x00) ECDH oturumu başarıyla temizlendi.</span><span class="sxs-lookup"><span data-stu-id="51eee-493">**NX_CRYPTO_SUCCESS** (0x00) Successfully cleaned up the ECDH session.</span></span>
- <span data-ttu-id="51eee-494">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-494">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>

## <a name="_nx_crypto_method_ecdsa_init"></a><span data-ttu-id="51eee-495">_nx_crypto_method_ecdsa_init</span><span class="sxs-lookup"><span data-stu-id="51eee-495">_nx_crypto_method_ecdsa_init</span></span>

<span data-ttu-id="51eee-496">ECDSA şifreleme denetim bloğunu başlatır</span><span class="sxs-lookup"><span data-stu-id="51eee-496">Initializes the ECDSA crypto control block</span></span>

### <a name="prototype"></a><span data-ttu-id="51eee-497">Prototype</span><span class="sxs-lookup"><span data-stu-id="51eee-497">Prototype</span></span>

```c
UINT _nx_crypto_method_ecdsa_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size);
```

### <a name="description"></a><span data-ttu-id="51eee-498">Açıklama</span><span class="sxs-lookup"><span data-stu-id="51eee-498">Description</span></span>

<span data-ttu-id="51eee-499">Bu işlev, ECDSA denetim bloğunu verilen anahtar dizesiyle başlatır.</span><span class="sxs-lookup"><span data-stu-id="51eee-499">This function initializes the ECDSA control block with the given key string.</span></span> <span data-ttu-id="51eee-500">ECDSA denetim bloğu başlatıldıktan sonra, sonraki ECDSA işlemi aynı denetim bloğunu kullanıyor olacaktır.</span><span class="sxs-lookup"><span data-stu-id="51eee-500">Once the ECDSA control block is initialized, subsequent ECDSA operation shall be using the same control block.</span></span>

<span data-ttu-id="51eee-501">Uygulama birden fazla ECDSA denetim bloğu oluşturabilir, her biri bir oturumu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="51eee-501">Application may create multiple ECDSA control blocks, each represents a session.</span></span> <span data-ttu-id="51eee-502">ECDSA denetim bloğunun başlatılması yeni bir karma hesaplama oturumu başlatır.</span><span class="sxs-lookup"><span data-stu-id="51eee-502">Initializing the ECDSA control block starts a new hash computation session.</span></span> <span data-ttu-id="51eee-503">ECDSA denetim bloğunun yeniden başlatılması geçerli oturum ve yıldızların yeni bir kopyasını terk eden.</span><span class="sxs-lookup"><span data-stu-id="51eee-503">Re-initializing the ECDSA control block abandons the current session and stars a new one.</span></span>

### <a name="parameters"></a><span data-ttu-id="51eee-504">Parametreler</span><span class="sxs-lookup"><span data-stu-id="51eee-504">Parameters</span></span>

- <span data-ttu-id="51eee-505">**yöntemi** Geçerli bir ECDSA şifreleme yöntemi denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-505">**method** Pointer to a valid ECDSA crypto method control block.</span></span> <span data-ttu-id="51eee-506">Aşağıdaki önceden tanımlanmış şifreleme yöntemleri kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="51eee-506">The following pre-defined crypto methods are available:</span></span>
  - <span data-ttu-id="51eee-507">*crypto_method_ecdsa*</span><span class="sxs-lookup"><span data-stu-id="51eee-507">*crypto_method_ecdsa*</span></span>
- <span data-ttu-id="51eee-508">**anahtar** Bu alan ECDSA için kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-508">**key** This field is not used for ECDSA.</span></span>
- <span data-ttu-id="51eee-509">**key_size_in_bits** Bu alan ECDSA için kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-509">**key_size_in_bits** This field is not used for ECDSA.</span></span>
- <span data-ttu-id="51eee-510">**tanıtıcı** Bu hizmet, çağırana bir tanıtıcı döndürür.</span><span class="sxs-lookup"><span data-stu-id="51eee-510">**handle** This service returns a handle to the caller.</span></span> <span data-ttu-id="51eee-511">Tanıtıcı uygulamaya bağımlıdır ve bu uygulamada kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="51eee-511">The handle is implementation-dependent and is not being used in this implementation.</span></span> <span data-ttu-id="51eee-512">Uygulama tanıtıcı için NULL değer geçirecektir.</span><span class="sxs-lookup"><span data-stu-id="51eee-512">Application shall pass NULL for the handle.</span></span>
- <span data-ttu-id="51eee-513">**crypto_metadata** ECDSA denetim bloğu için geçerli bir bellek alanı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="51eee-513">**crypto_metadata** Pointer to a valid memory space for the ECDSA control block.</span></span> <span data-ttu-id="51eee-514">Bellek alanının başlangıç adresi 4 bayt hizalı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-514">The starting address of the memory space must be 4-byte aligned.</span></span>
- <span data-ttu-id="51eee-515">**crypto_metadata_size** Crypto_metadata alanının bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-515">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="51eee-516">ECDSA için meta veri boyutu *sizeof olmalıdır (NX_CRYPTO_ECDSA)*</span><span class="sxs-lookup"><span data-stu-id="51eee-516">For ECDSA, the metadata size must be *sizeof(NX_CRYPTO_ECDSA)*</span></span>

### <a name="return-values"></a><span data-ttu-id="51eee-517">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="51eee-517">Return Values</span></span>

- <span data-ttu-id="51eee-518">Anahtar ve anahtar boyutuyla ECDSA denetim bloğunun başarılı bir şekilde başlatılması **NX_CRYPTO_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="51eee-518">**NX_CRYPTO_SUCCESS** (0x00) Successful initialization of the ECDSA control block with the key and key size.</span></span>
- <span data-ttu-id="51eee-519">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-519">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="51eee-520">**NX_PTR_ERROR** (0x07) anahtar için geçersiz işaretçi veya geçersiz crypto_metadata veya crypto_metadata_size ya da crypto_metadata 4 bayt hizalı değil.</span><span class="sxs-lookup"><span data-stu-id="51eee-520">**NX_PTR_ERROR** (0x07) Invalid pointer to the key, or invalid crypto_metadata or crypto_metadata_size, or crypto_metadata is not 4-byte aligned.</span></span>

## <a name="_nx_crypto_method_ecdsa_operation"></a><span data-ttu-id="51eee-521">_nx_crypto_method_ecdsa_operation</span><span class="sxs-lookup"><span data-stu-id="51eee-521">_nx_crypto_method_ecdsa_operation</span></span>

<span data-ttu-id="51eee-522">ECDSA işlemi gerçekleştir</span><span class="sxs-lookup"><span data-stu-id="51eee-522">Perform ECDSA operation</span></span>

### <a name="prototype"></a><span data-ttu-id="51eee-523">Prototype</span><span class="sxs-lookup"><span data-stu-id="51eee-523">Prototype</span></span>

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

### <a name="description"></a><span data-ttu-id="51eee-524">Açıklama</span><span class="sxs-lookup"><span data-stu-id="51eee-524">Description</span></span>

<span data-ttu-id="51eee-525">Bu işlev ECDSA işlemini gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="51eee-525">This function performs ECDSA operation.</span></span> <span data-ttu-id="51eee-526">ECDSA denetim bloğunun _ *nx_crypto_method_ecdsa_init ()* ile başlatılmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="51eee-526">The ECDSA control block must have been initialized with _ *nx_crypto_method_ecdsa_init()*.</span></span> <span data-ttu-id="51eee-527">Gerçekleştirilecek ECDSA algoritması, *Yöntem* denetim bloğunda belirtilen algoritmayı temel alır.</span><span class="sxs-lookup"><span data-stu-id="51eee-527">The ECDSA algorithm to be performed is based on the algorithm specified in the *method* control block.</span></span>

<span data-ttu-id="51eee-528">İşlem NX_CRYPTO_EC_CURVE_SET olduğunda, giriş Eliptik Eğri Şifreleme yöntemine işaret eder.</span><span class="sxs-lookup"><span data-stu-id="51eee-528">When the operation is NX_CRYPTO_EC_CURVE_SET, the input points to Elliptic Curve crypto method.</span></span> <span data-ttu-id="51eee-529">İşlem NX_CRYPTO_EC_KEY_PAIR_GENERATE olduğunda, çıkış NX_CRYPTO_EXTENDED_OUTPUT yapısına işaret eder ve anahtar çifti nx_crypto_extended_output_data kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="51eee-529">When the operation is NX_CRYPTO_EC_KEY_PAIR_GENERATE, the output points to NX_CRYPTO_EXTENDED_OUTPUT structure and the key pair is copied to nx_crypto_extended_output_data.</span></span>

### <a name="parameters"></a><span data-ttu-id="51eee-530">Parametreler</span><span class="sxs-lookup"><span data-stu-id="51eee-530">Parameters</span></span>

- <span data-ttu-id="51eee-531">**op** Gerçekleştirilecek işlemin türü.</span><span class="sxs-lookup"><span data-stu-id="51eee-531">**op** Type of operation to perform.</span></span> <span data-ttu-id="51eee-532">Geçerli işlem:</span><span class="sxs-lookup"><span data-stu-id="51eee-532">Valid operation is:</span></span>
  - <span data-ttu-id="51eee-533">*NX_CRYPTO_EC_CURVE_SET*</span><span class="sxs-lookup"><span data-stu-id="51eee-533">*NX_CRYPTO_EC_CURVE_SET*</span></span>
  - <span data-ttu-id="51eee-534">*NX_CRYPTO_AUTHENTICATE*</span><span class="sxs-lookup"><span data-stu-id="51eee-534">*NX_CRYPTO_AUTHENTICATE*</span></span>
  - <span data-ttu-id="51eee-535">*NX_CRYPTO_VERIFY*</span><span class="sxs-lookup"><span data-stu-id="51eee-535">*NX_CRYPTO_VERIFY*</span></span>
- <span data-ttu-id="51eee-536">**tanıtıcı** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-536">**handle** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="51eee-537">Geçirilen tüm değerler sessizce yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="51eee-537">Any values passed in are silently ignored.</span></span>
- <span data-ttu-id="51eee-538">**yöntemi** Geçerli ECDSA şifreleme yöntemine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-538">**method** Pointer to the valid ECDSA crypto method.</span></span> <span data-ttu-id="51eee-539">Burada kullanılan şifreleme yöntemi _ *nx_crypto_method_ecdsa_init ()* içinde kullanılan aynı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-539">The crypto method used here must be the same used in the _ *nx_crypto_method_ecdsa_init().*</span></span>
- <span data-ttu-id="51eee-540">**anahtar** Op NX_CRYPTO_VERIFY, anahtarı işaret eder.</span><span class="sxs-lookup"><span data-stu-id="51eee-540">**key** Points to the key when op is NX_CRYPTO_VERIFY.</span></span> <span data-ttu-id="51eee-541">Anahtar arabelleğinde kısıtlama yoktur.</span><span class="sxs-lookup"><span data-stu-id="51eee-541">There are not restrictions on key buffer.</span></span> <span data-ttu-id="51eee-542">Bu alan, diğer op değerleri için kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-542">This field is not used for other values of op.</span></span>
- <span data-ttu-id="51eee-543">**key_size_in_bits** Anahtarın bit cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-543">**key_size_in_bits** Size of the key, in bits.</span></span>
- <span data-ttu-id="51eee-544">**giriş** Op NX_CRYPTO_EC_CURVE_SET olduğunda, bu alan Eliptik Eğri Şifreleme yöntemine işaret eder.</span><span class="sxs-lookup"><span data-stu-id="51eee-544">**input** When op is NX_CRYPTO_EC_CURVE_SET, this field points to Elliptic Curve crypto method.</span></span> <span data-ttu-id="51eee-545">Aksi takdirde, bu alan giriş metin verilerini içeren bir arabelleğe işaret eder.</span><span class="sxs-lookup"><span data-stu-id="51eee-545">Otherwise, this field points to a buffer containing input text data.</span></span>
- <span data-ttu-id="51eee-546">**input_length_in_byte** Giriş verilerinin bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-546">**input_length_in_byte** Size of the input data, in bytes.</span></span>
- <span data-ttu-id="51eee-547">**iv_ptr** Bu alan ECDSA için kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-547">**iv_ptr** This field is not used for ECDSA.</span></span>
- <span data-ttu-id="51eee-548">**Çıkış** Op NX_CRYPTO_EC_CURVE_SET olduğunda, bu alan kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-548">**output** When op is NX_CRYPTO_EC_CURVE_SET, this field is not used.</span></span> <span data-ttu-id="51eee-549">Op NX_CRYPTO_AUTHENTICATE olduğunda, bu alan oluşturulan ECDSA imzasının bellek alanını gösterir.</span><span class="sxs-lookup"><span data-stu-id="51eee-549">When op is NX_CRYPTO_AUTHENTICATE, this field points to the memory area for the generated ECDSA signature.</span></span> <span data-ttu-id="51eee-550">Op NX_CRYPTO_VERIFY olduğunda, bu alan doğrulanan ECDSA imzasının bellek alanını gösterir.</span><span class="sxs-lookup"><span data-stu-id="51eee-550">When op is NX_CRYPTO_VERIFY, this field points to the memory area for the verified ECDSA signature.</span></span>
- <span data-ttu-id="51eee-551">**output_length_in_byte** Çıkış arabelleğinin bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-551">**output_length_in_byte** Size of the output buffer in bytes.</span></span>
- <span data-ttu-id="51eee-552">**crypto_metadata** *_Nx_crypto_method_ecdsa_init ()* içinde kullanılan ECDSA denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-552">**crypto_metadata** Pointer to the ECDSA control block used in *_nx_crypto_method_ecdsa_init()*.</span></span>
- <span data-ttu-id="51eee-553">**crypto_metadata_size** Crypto_metadata alanının bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-553">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="51eee-554">ECDSA için meta veri boyutu sizeof olmalıdır *(NX_CRYPTO_ECDSA)*</span><span class="sxs-lookup"><span data-stu-id="51eee-554">For ECDSA, the metadata size must *sizeof(NX_CRYPTO_ECDSA)*</span></span>
- <span data-ttu-id="51eee-555">**packet_ptr** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-555">**packet_ptr** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="51eee-556">Geçirilen tüm değerler sessizce yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="51eee-556">Any values passed in are silently ignored.</span></span>
- <span data-ttu-id="51eee-557">**nx_crypto_hw_process_callback** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-557">**nx_crypto_hw_process_callback** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="51eee-558">Geçirilen tüm değerler sessizce yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="51eee-558">Any values passed in are silently ignored.</span></span>

### <a name="return-values"></a><span data-ttu-id="51eee-559">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="51eee-559">Return Values</span></span>

- <span data-ttu-id="51eee-560">**NX_CRYPTO_SUCCESS** (0x00) ECDSA işlemini başarıyla yürütüldü.</span><span class="sxs-lookup"><span data-stu-id="51eee-560">**NX_CRYPTO_SUCCESS** (0x00) Successfully executed the ECDSA operation.</span></span>
- <span data-ttu-id="51eee-561">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-561">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="51eee-562">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi veya uzunluğu geçersiz.</span><span class="sxs-lookup"><span data-stu-id="51eee-562">**NX_PTR_ERROR** (0x07) Invalid input pointer or invalid length.</span></span>
- <span data-ttu-id="51eee-563">**NX_CRYPTO_INVALID_ALGORITHM** (0x20004) GEÇERSIZ ECDSA algoritması belirtildi.</span><span class="sxs-lookup"><span data-stu-id="51eee-563">**NX_CRYPTO_INVALID_ALGORITHM** (0x20004) Invalid ECDSA algorithm being specified.</span></span>
- <span data-ttu-id="51eee-564">**NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) geçersiz çıkış arabelleği boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-564">**NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) Invalid output buffer size.</span></span>

## <a name="_nx_crypto_method_ecdsa_cleanup"></a><span data-ttu-id="51eee-565">_nx_crypto_method_ecdsa_cleanup</span><span class="sxs-lookup"><span data-stu-id="51eee-565">_nx_crypto_method_ecdsa_cleanup</span></span>

<span data-ttu-id="51eee-566">ECDSA denetim bloğunu temizleyin.</span><span class="sxs-lookup"><span data-stu-id="51eee-566">Clean up the ECDSA control block.</span></span>

### <a name="prototype"></a><span data-ttu-id="51eee-567">Prototype</span><span class="sxs-lookup"><span data-stu-id="51eee-567">Prototype</span></span>

```c
UINT _nx_crypto_method_ecdsa_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a><span data-ttu-id="51eee-568">Açıklama</span><span class="sxs-lookup"><span data-stu-id="51eee-568">Description</span></span>

<span data-ttu-id="51eee-569">Uygulama, bu ECDSA oturumunun artık gerekli olmadığını belirlediğinde ECDSA denetim bloğunu temizlemek için bu işlevi çağırır.</span><span class="sxs-lookup"><span data-stu-id="51eee-569">Application calls this function to clean up the ECDSA control block after it determines this ECDSA session is no longer needed.</span></span>

### <a name="parameters"></a><span data-ttu-id="51eee-570">Parametreler</span><span class="sxs-lookup"><span data-stu-id="51eee-570">Parameters</span></span>

- <span data-ttu-id="51eee-571">**crypto_metadata** *_Nx_crypto_method_ecdsa_init ()* içinde kullanılan ECDSA denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-571">**crypto_metadata** Pointer to the ECDSA control block used in *_nx_crypto_method_ecdsa_init()*.</span></span>

### <a name="return-values"></a><span data-ttu-id="51eee-572">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="51eee-572">Return Values</span></span>

- <span data-ttu-id="51eee-573">**NX_CRYPTO_SUCCESS** (0x00) ECDSA oturumu başarıyla temizlendi.</span><span class="sxs-lookup"><span data-stu-id="51eee-573">**NX_CRYPTO_SUCCESS** (0x00) Successfully cleaned up the ECDSA session.</span></span>
- <span data-ttu-id="51eee-574">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-574">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>

## <a name="_nx_crypto_method_hmac_md5_init"></a><span data-ttu-id="51eee-575">_nx_crypto_method_hmac_md5_init</span><span class="sxs-lookup"><span data-stu-id="51eee-575">_nx_crypto_method_hmac_md5_init</span></span>

<span data-ttu-id="51eee-576">HMAC MD5 şifreleme denetim bloğunu başlatır</span><span class="sxs-lookup"><span data-stu-id="51eee-576">Initializes the HMAC MD5 crypto control block</span></span>

### <a name="prototype"></a><span data-ttu-id="51eee-577">Prototype</span><span class="sxs-lookup"><span data-stu-id="51eee-577">Prototype</span></span>

```c
UINT _nx_crypto_method_hmac_md5_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size);
```

### <a name="description"></a><span data-ttu-id="51eee-578">Açıklama</span><span class="sxs-lookup"><span data-stu-id="51eee-578">Description</span></span>

<span data-ttu-id="51eee-579">Bu işlev, HMAC MD5 denetim bloğunu verilen anahtar dizesiyle başlatır.</span><span class="sxs-lookup"><span data-stu-id="51eee-579">This function initializes the HMAC MD5 control block with the given key string.</span></span> <span data-ttu-id="51eee-580">HMAC MD5 denetim bloğu başlatıldıktan sonra, sonraki HMAC MD5 işlemi aynı denetim bloğunu kullanıyor olacaktır.</span><span class="sxs-lookup"><span data-stu-id="51eee-580">Once the HMAC MD5 control block is initialized, subsequent HMAC MD5 operation shall be using the same control block.</span></span>

<span data-ttu-id="51eee-581">Uygulama birden çok HMAC MD5 denetim bloğu oluşturabilir, her biri bir oturumu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="51eee-581">Application may create multiple HMAC MD5 control blocks, each represents a session.</span></span> <span data-ttu-id="51eee-582">HMAC MD5 denetim bloğunun başlatılması yeni bir karma hesaplama oturumu başlatır.</span><span class="sxs-lookup"><span data-stu-id="51eee-582">Initializing the HMAC MD5 control block starts a new hash computation session.</span></span> <span data-ttu-id="51eee-583">HMAC MD5 denetim bloğunu yeniden başlatmak geçerli oturumu ve yıldızları yeni bir kez terk edin.</span><span class="sxs-lookup"><span data-stu-id="51eee-583">Re-initializing the HMAC MD5 control block abandons the current session and stars a new one.</span></span>

### <a name="parameters"></a><span data-ttu-id="51eee-584">Parametreler</span><span class="sxs-lookup"><span data-stu-id="51eee-584">Parameters</span></span>

- <span data-ttu-id="51eee-585">**yöntemi** Geçerli bir HMAC MD5 şifreleme yöntemi denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="51eee-585">**method** Pointer to a valid HMAC MD5 crypto method control block.</span></span>
<span data-ttu-id="51eee-586">Aşağıdaki önceden tanımlanmış şifreleme yöntemleri kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="51eee-586">The following pre-defined crypto methods are available:</span></span>
  - <span data-ttu-id="51eee-587">*crypto_method_hmac_md5*</span><span class="sxs-lookup"><span data-stu-id="51eee-587">*crypto_method_hmac_md5*</span></span>
- <span data-ttu-id="51eee-588">**anahtar** Anahtarı işaret eder.</span><span class="sxs-lookup"><span data-stu-id="51eee-588">**key** Points to the key.</span></span> <span data-ttu-id="51eee-589">Anahtar arabelleğinde kısıtlama yoktur.</span><span class="sxs-lookup"><span data-stu-id="51eee-589">There are not restrictions on key buffer.</span></span>
- <span data-ttu-id="51eee-590">**key_size_in_bits** Anahtarın bit cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-590">**key_size_in_bits** Size of the key, in bits.</span></span>
- <span data-ttu-id="51eee-591">**tanıtıcı** Bu hizmet, çağırana bir tanıtıcı döndürür.</span><span class="sxs-lookup"><span data-stu-id="51eee-591">**handle** This service returns a handle to the caller.</span></span> <span data-ttu-id="51eee-592">Tanıtıcı uygulamaya bağımlıdır ve bu uygulamada kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="51eee-592">The handle is implementation-dependent and is not being used in this implementation.</span></span> <span data-ttu-id="51eee-593">Uygulama tanıtıcı için NULL değer geçirecektir.</span><span class="sxs-lookup"><span data-stu-id="51eee-593">Application shall pass NULL for the handle.</span></span>
- <span data-ttu-id="51eee-594">**crypto_metadata** HMAC MD5 denetim bloğu için geçerli bir bellek alanı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="51eee-594">**crypto_metadata** Pointer to a valid memory space for the HMAC MD5 control block.</span></span> <span data-ttu-id="51eee-595">Bellek alanının başlangıç adresi 4 bayt hizalı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-595">The starting address of the memory space must be 4-byte aligned.</span></span>
- <span data-ttu-id="51eee-596">**crypto_metadata_size** Crypto_metadata alanının bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-596">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="51eee-597">HMAC MD5 için meta veri boyutu *sizeof olmalıdır (NX_CRYPTO_MD5_HMAC)*</span><span class="sxs-lookup"><span data-stu-id="51eee-597">For HMAC MD5, the metadata size must be *sizeof(NX_CRYPTO_MD5_HMAC)*</span></span>

### <a name="return-values"></a><span data-ttu-id="51eee-598">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="51eee-598">Return Values</span></span>

- <span data-ttu-id="51eee-599">**NX_CRYPTO_SUCCESS** (0x00) anahtar ve anahtar boyutuyla HMAC MD5 denetim bloğunun başarılı bir şekilde başlatılması.</span><span class="sxs-lookup"><span data-stu-id="51eee-599">**NX_CRYPTO_SUCCESS** (0x00) Successful initialization of the HMAC MD5 control block with the key and key size.</span></span>
- <span data-ttu-id="51eee-600">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-600">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="51eee-601">**NX_PTR_ERROR** (0x07) anahtar için geçersiz işaretçi veya geçersiz crypto_metadata veya crypto_metadata_size ya da crypto_metadata 4 bayt hizalı değil.</span><span class="sxs-lookup"><span data-stu-id="51eee-601">**NX_PTR_ERROR** (0x07) Invalid pointer to the key, or invalid crypto_metadata or crypto_metadata_size, or crypto_metadata is not 4-byte aligned.</span></span>

## <a name="_nx_crypto_method_hmac_md5_operation"></a><span data-ttu-id="51eee-602">_nx_crypto_method_hmac_md5_operation</span><span class="sxs-lookup"><span data-stu-id="51eee-602">_nx_crypto_method_hmac_md5_operation</span></span>

<span data-ttu-id="51eee-603">HMAC MD5 karma işlemi gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="51eee-603">Perform an HMAC MD5 hash operation.</span></span>

### <a name="prototype"></a><span data-ttu-id="51eee-604">Prototype</span><span class="sxs-lookup"><span data-stu-id="51eee-604">Prototype</span></span>

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

### <a name="description"></a><span data-ttu-id="51eee-605">Açıklama</span><span class="sxs-lookup"><span data-stu-id="51eee-605">Description</span></span>

<span data-ttu-id="51eee-606">Bu işlev HMAC MD5 karma işlemini gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="51eee-606">This function performs HMAC MD5 hash operation.</span></span> <span data-ttu-id="51eee-607">HMAC MD5 denetim bloğunun _ *nx_crypto_method_hmac_md5_init ()* ile başlatılmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="51eee-607">The HMAC MD5 control block must have been initialized with _ *nx_crypto_method_hmac_md5_init()*.</span></span> <span data-ttu-id="51eee-608">Gerçekleştirilecek HMAC MD5 algoritması, *Yöntem* denetim bloğunda belirtilen algoritmayı temel alır.</span><span class="sxs-lookup"><span data-stu-id="51eee-608">The HMAC MD5 algorithm to be performed is based on the algorithm specified in the *method* control block.</span></span>

<span data-ttu-id="51eee-609">Son *NX_CRYPTO_HASH_CALCULATE* işlemi için, çıkış arabelleği boyutu 16 bayt olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-609">For the final *NX_CRYPTO_HASH_CALCULATE* operation, the output buffer size must be 16 bytes.</span></span>

<span data-ttu-id="51eee-610">Bu işlem durum bilgilerini saklar ve HMAC MD5 denetim bloğunda anahtar malzemesini değiştirmez.</span><span class="sxs-lookup"><span data-stu-id="51eee-610">This operation does not keep state information, and does not alter the key material in the HMAC MD5 control block.</span></span>

### <a name="parameters"></a><span data-ttu-id="51eee-611">Parametreler</span><span class="sxs-lookup"><span data-stu-id="51eee-611">Parameters</span></span>

- <span data-ttu-id="51eee-612">**op** Gerçekleştirilecek işlemin türü.</span><span class="sxs-lookup"><span data-stu-id="51eee-612">**op** Type of operation to perform.</span></span> <span data-ttu-id="51eee-613">Geçerli işlem:</span><span class="sxs-lookup"><span data-stu-id="51eee-613">Valid operation is:</span></span>
  - <span data-ttu-id="51eee-614">*NX_CRYPTO_HASH_INITIALIZE*</span><span class="sxs-lookup"><span data-stu-id="51eee-614">*NX_CRYPTO_HASH_INITIALIZE*</span></span>
  - <span data-ttu-id="51eee-615">*NX_CRYPTO_HASH_UPDATE*</span><span class="sxs-lookup"><span data-stu-id="51eee-615">*NX_CRYPTO_HASH_UPDATE*</span></span>
  - <span data-ttu-id="51eee-616">*NX_CRYPTO_HASH_CALCULATE*</span><span class="sxs-lookup"><span data-stu-id="51eee-616">*NX_CRYPTO_HASH_CALCULATE*</span></span>
- <span data-ttu-id="51eee-617">**tanıtıcı** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-617">**handle** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="51eee-618">Geçirilen tüm değerler sessizce yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="51eee-618">Any values passed in are silently ignored.</span></span>
- <span data-ttu-id="51eee-619">**yöntemi** Geçerli HMAC MD5 şifreleme yöntemine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-619">**method** Pointer to the valid HMAC MD5 crypto method.</span></span> <span data-ttu-id="51eee-620">Burada kullanılan şifreleme yöntemi, *nx_crypto_method_hmac_md5_init ()* içinde kullanılan aynı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-620">The crypto method used here must be the same used in the *nx_crypto_method_hmac_md5_init().*</span></span>
- <span data-ttu-id="51eee-621">**anahtar** Anahtarı işaret eder.</span><span class="sxs-lookup"><span data-stu-id="51eee-621">**key** Points to the key.</span></span> <span data-ttu-id="51eee-622">Anahtar arabelleğinde kısıtlama yoktur.</span><span class="sxs-lookup"><span data-stu-id="51eee-622">There are not restrictions on key buffer.</span></span>
- <span data-ttu-id="51eee-623">**key_size_in_bits** Anahtarın bit cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-623">**key_size_in_bits** Size of the key, in bits.</span></span>
- <span data-ttu-id="51eee-624">**input_data** Girdi metin verileri içeren bir arabelleğe işaret eder.</span><span class="sxs-lookup"><span data-stu-id="51eee-624">**input_data** Points to a buffer containing input text data.</span></span> <span data-ttu-id="51eee-625">Giriş arabelleğinde kısıtlama yoktur.</span><span class="sxs-lookup"><span data-stu-id="51eee-625">There are not restrictions on input buffer.</span></span>
- <span data-ttu-id="51eee-626">**input_data_size** Giriş verilerinin bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-626">**input_data_size** Size of the input data, in bytes.</span></span>
- <span data-ttu-id="51eee-627">**iv_ptr** Bu alan HMAC MD5 için kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-627">**iv_ptr** This field is not used for HMAC MD5.</span></span>
- <span data-ttu-id="51eee-628">**iv_size** Bu alan HMAC MD5 için kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-628">**iv_size** This field is not used for HMAC MD5.</span></span>
- <span data-ttu-id="51eee-629">**output_buffer** Oluşturulan HMAC MD5 karması için bellek alanına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-629">**output_buffer** Pointer to the memory area for the generated HMAC MD5 hash.</span></span>
- <span data-ttu-id="51eee-630">**output_buffer_size** Çıkış arabelleğinin bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-630">**output_buffer_size** Size of the output buffer in bytes.</span></span>
- <span data-ttu-id="51eee-631">**crypto_metadata** *_Nx_crypto_method_hmac_md5_init ()* IÇINDE kullanılan HMAC MD5 denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-631">**crypto_metadata** Pointer to the HMAC MD5 control block used in *_nx_crypto_method_hmac_md5_init()*.</span></span>
- <span data-ttu-id="51eee-632">**crypto_metadata_size** Crypto_metadata alanının bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-632">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="51eee-633">HMAC MD5 için meta veri boyutu sizeof olmalıdır *(NX_CRYPTO_MD5_HMAC)*</span><span class="sxs-lookup"><span data-stu-id="51eee-633">For HMAC MD5, the metadata size must *sizeof(NX_CRYPTO_MD5_HMAC)*</span></span>
- <span data-ttu-id="51eee-634">**packet_ptr** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-634">**packet_ptr** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="51eee-635">Geçirilen tüm değerler sessizce yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="51eee-635">Any values passed in are silently ignored.</span></span>
- <span data-ttu-id="51eee-636">**nx_crypto_hw_process_callback** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-636">**nx_crypto_hw_process_callback** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="51eee-637">Geçirilen tüm değerler sessizce yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="51eee-637">Any values passed in are silently ignored.</span></span>

### <a name="return-values"></a><span data-ttu-id="51eee-638">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="51eee-638">Return Values</span></span>

- <span data-ttu-id="51eee-639">**NX_CRYPTO_SUCCESS** (0x00) HMAC MD5 işlemini başarıyla yürütüldü.</span><span class="sxs-lookup"><span data-stu-id="51eee-639">**NX_CRYPTO_SUCCESS** (0x00) Successfully executed the HMAC MD5 operation.</span></span>
- <span data-ttu-id="51eee-640">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-640">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="51eee-641">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi veya uzunluğu geçersiz.</span><span class="sxs-lookup"><span data-stu-id="51eee-641">**NX_PTR_ERROR** (0x07) Invalid input pointer or invalid length.</span></span>
- <span data-ttu-id="51eee-642">**NX_CRYPTO_INVALID_ALGORITHM** (0x20004) GEÇERSIZ HMAC MD5 algoritması belirtildi.</span><span class="sxs-lookup"><span data-stu-id="51eee-642">**NX_CRYPTO_INVALID_ALGORITHM** (0x20004) Invalid HMAC MD5 algorithm being specified.</span></span>
- <span data-ttu-id="51eee-643">**NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) geçersiz çıkış arabelleği boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-643">**NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) Invalid output buffer size.</span></span>

## <a name="_nx_crypto_method_hmac_sha1_init"></a><span data-ttu-id="51eee-644">_nx_crypto_method_hmac_sha1_init</span><span class="sxs-lookup"><span data-stu-id="51eee-644">_nx_crypto_method_hmac_sha1_init</span></span>

<span data-ttu-id="51eee-645">HMAC SHA1 şifreleme denetim bloğunu başlatır</span><span class="sxs-lookup"><span data-stu-id="51eee-645">Initializes the HMAC SHA1 crypto control block</span></span>

### <a name="prototype"></a><span data-ttu-id="51eee-646">Prototype</span><span class="sxs-lookup"><span data-stu-id="51eee-646">Prototype</span></span>

```c
UINT _nx_crypto_method_hmac_sha1_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size);
```

### <a name="description"></a><span data-ttu-id="51eee-647">Açıklama</span><span class="sxs-lookup"><span data-stu-id="51eee-647">Description</span></span>

<span data-ttu-id="51eee-648">Bu işlev, HMAC SHA1 denetim bloğunu verilen anahtar dizesiyle başlatır.</span><span class="sxs-lookup"><span data-stu-id="51eee-648">This function initializes the HMAC SHA1 control block with the given key string.</span></span> <span data-ttu-id="51eee-649">HMAC SHA1 denetim bloğu başlatıldıktan sonra, sonraki HMAC SHA1 işlemi aynı denetim bloğunu kullanıyor olacaktır.</span><span class="sxs-lookup"><span data-stu-id="51eee-649">Once the HMAC SHA1 control block is initialized, subsequent HMAC SHA1 operation shall be using the same control block.</span></span>

<span data-ttu-id="51eee-650">Uygulama birden çok HMAC SHA1 denetim bloğu oluşturabilir, her biri bir oturumu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="51eee-650">Application may create multiple HMAC SHA1 control blocks, each represents a session.</span></span> <span data-ttu-id="51eee-651">HMAC SHA1 denetim bloğunu başlatmak yeni bir karma hesaplama oturumu başlatır.</span><span class="sxs-lookup"><span data-stu-id="51eee-651">Initializing the HMAC SHA1 control block starts a new hash computation session.</span></span> <span data-ttu-id="51eee-652">HMAC SHA1 denetim bloğunu yeniden başlatmak, geçerli oturumu ve yıldızları yeni bir kez terk.</span><span class="sxs-lookup"><span data-stu-id="51eee-652">Re-initializing the HMAC SHA1 control block abandons the current session and stars a new one.</span></span>

### <a name="parameters"></a><span data-ttu-id="51eee-653">Parametreler</span><span class="sxs-lookup"><span data-stu-id="51eee-653">Parameters</span></span>

- <span data-ttu-id="51eee-654">**yöntemi** Geçerli bir HMAC SHA1 şifreleme yöntemi denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="51eee-654">**method** Pointer to a valid HMAC SHA1 crypto method control block.</span></span> <span data-ttu-id="51eee-655">Aşağıdaki önceden tanımlanmış şifreleme yöntemleri kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="51eee-655">The following pre-defined crypto methods are available:</span></span>
  - <span data-ttu-id="51eee-656">*crypto_method_hmac_sha1*</span><span class="sxs-lookup"><span data-stu-id="51eee-656">*crypto_method_hmac_sha1*</span></span>
- <span data-ttu-id="51eee-657">**anahtar** Anahtarı işaret eder.</span><span class="sxs-lookup"><span data-stu-id="51eee-657">**key** Points to the key.</span></span> <span data-ttu-id="51eee-658">Anahtar arabelleğinde kısıtlama yoktur.</span><span class="sxs-lookup"><span data-stu-id="51eee-658">There are not restrictions on key buffer.</span></span>
- <span data-ttu-id="51eee-659">**key_size_in_bits** Anahtarın bit cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-659">**key_size_in_bits** Size of the key, in bits.</span></span>
- <span data-ttu-id="51eee-660">**tanıtıcı** Bu hizmet, çağırana bir tanıtıcı döndürür.</span><span class="sxs-lookup"><span data-stu-id="51eee-660">**handle** This service returns a handle to the caller.</span></span> <span data-ttu-id="51eee-661">Tanıtıcı uygulamaya bağımlıdır ve bu uygulamada kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="51eee-661">The handle is implementation-dependent and is not being used in this implementation.</span></span> <span data-ttu-id="51eee-662">Uygulama tanıtıcı için NULL değer geçirecektir.</span><span class="sxs-lookup"><span data-stu-id="51eee-662">Application shall pass NULL for the handle.</span></span>
- <span data-ttu-id="51eee-663">**crypto_metadata** HMAC SHA1 denetim bloğu için geçerli bir bellek alanı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="51eee-663">**crypto_metadata** Pointer to a valid memory space for the HMAC SHA1 control block.</span></span> <span data-ttu-id="51eee-664">Bellek alanının başlangıç adresi 4 bayt hizalı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-664">The starting address of the memory space must be 4-byte aligned.</span></span>
- <span data-ttu-id="51eee-665">**crypto_metadata_size** Crypto_metadata alanının bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-665">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="51eee-666">HMAC SHA1 için, meta veri boyutu sizeof olmalıdır *(NX_CRYPTO_SHA1_HMAC)*</span><span class="sxs-lookup"><span data-stu-id="51eee-666">For HMAC SHA1, the metadata size must be *sizeof(NX_CRYPTO_SHA1_HMAC)*</span></span>

### <a name="return-values"></a><span data-ttu-id="51eee-667">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="51eee-667">Return Values</span></span>

- <span data-ttu-id="51eee-668">**NX_CRYPTO_SUCCESS** (0x00) anahtar ve anahtar boyutuyla HMAC SHA1control bloğunun başarıyla başlatılması.</span><span class="sxs-lookup"><span data-stu-id="51eee-668">**NX_CRYPTO_SUCCESS** (0x00) Successful initialization of the HMAC SHA1control block with the key and key size.</span></span>
- <span data-ttu-id="51eee-669">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-669">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="51eee-670">**NX_PTR_ERROR** (0x07) anahtar için geçersiz işaretçi veya geçersiz crypto_metadata veya crypto_metadata_size ya da crypto_metadata 4 bayt hizalı değil.</span><span class="sxs-lookup"><span data-stu-id="51eee-670">**NX_PTR_ERROR** (0x07) Invalid pointer to the key, or invalid crypto_metadata or crypto_metadata_size, or crypto_metadata is not 4-byte aligned.</span></span>

## <a name="_nx_crypto_method_hmac_sha1_operation"></a><span data-ttu-id="51eee-671">_nx_crypto_method_hmac_sha1_operation</span><span class="sxs-lookup"><span data-stu-id="51eee-671">_nx_crypto_method_hmac_sha1_operation</span></span>

<span data-ttu-id="51eee-672">HMAC SHA1 karma işlemi gerçekleştir</span><span class="sxs-lookup"><span data-stu-id="51eee-672">Perform HMAC SHA1 hash operation</span></span>

### <a name="prototype"></a><span data-ttu-id="51eee-673">Prototype</span><span class="sxs-lookup"><span data-stu-id="51eee-673">Prototype</span></span>

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

### <a name="description"></a><span data-ttu-id="51eee-674">Açıklama</span><span class="sxs-lookup"><span data-stu-id="51eee-674">Description</span></span>

<span data-ttu-id="51eee-675">Bu işlev HMAC SHA1 karma işlem gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="51eee-675">This function performs HMAC SHA1 hash operation.</span></span> <span data-ttu-id="51eee-676">HMAC SHA1 denetim bloğunun _ *nx_crypto_method_hmac_sha1_init ()* ile başlatılmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="51eee-676">The HMAC SHA1 control block must have been initialized with _ *nx_crypto_method_hmac_sha1_init()*.</span></span> <span data-ttu-id="51eee-677">Gerçekleştirilecek HMAC SHA1 algoritması, *Yöntem* denetim bloğunda belirtilen algoritmayı temel alır.</span><span class="sxs-lookup"><span data-stu-id="51eee-677">The HMAC SHA1 algorithm to be performed is based on the algorithm specified in the *method* control block.</span></span>

<span data-ttu-id="51eee-678">Son *NX_CRYPTO_HASH_CALCULATE* işlemi için, çıkış arabelleği boyutu 20 bayt olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-678">For the final *NX_CRYPTO_HASH_CALCULATE* operation, the output buffer size must be 20 bytes.</span></span>

### <a name="parameters"></a><span data-ttu-id="51eee-679">Parametreler</span><span class="sxs-lookup"><span data-stu-id="51eee-679">Parameters</span></span>

- <span data-ttu-id="51eee-680">**op** Gerçekleştirilecek işlemin türü.</span><span class="sxs-lookup"><span data-stu-id="51eee-680">**op** Type of operation to perform.</span></span> <span data-ttu-id="51eee-681">Geçerli işlem:</span><span class="sxs-lookup"><span data-stu-id="51eee-681">Valid operation is:</span></span>
  - <span data-ttu-id="51eee-682">*NX_CRYPTO_HASH_INITIALIZE*</span><span class="sxs-lookup"><span data-stu-id="51eee-682">*NX_CRYPTO_HASH_INITIALIZE*</span></span>
  - <span data-ttu-id="51eee-683">*NX_CRYPTO_HASH_UPDATE*</span><span class="sxs-lookup"><span data-stu-id="51eee-683">*NX_CRYPTO_HASH_UPDATE*</span></span>
  - <span data-ttu-id="51eee-684">*NX_CRYPTO_HASH_CALCULATE*</span><span class="sxs-lookup"><span data-stu-id="51eee-684">*NX_CRYPTO_HASH_CALCULATE*</span></span>
- <span data-ttu-id="51eee-685">**tanıtıcı** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-685">**handle** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="51eee-686">Geçirilen tüm değerler sessizce yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="51eee-686">Any values passed in are silently ignored.</span></span>
- <span data-ttu-id="51eee-687">**yöntemi** Geçerli HMAC SHA1 şifreleme yöntemine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-687">**method** Pointer to the valid HMAC SHA1 crypto method.</span></span> <span data-ttu-id="51eee-688">Burada kullanılan şifreleme yöntemi _ *nx_crypto_method_hmac_sha1_init ()* içinde kullanılan aynı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-688">The crypto method used here must be the same used in the _ *nx_crypto_method_hmac_sha1_init().*</span></span>
- <span data-ttu-id="51eee-689">**anahtar** Anahtarı işaret eder.</span><span class="sxs-lookup"><span data-stu-id="51eee-689">**key** Points to the key.</span></span> <span data-ttu-id="51eee-690">Anahtar arabelleğinde kısıtlama yoktur.</span><span class="sxs-lookup"><span data-stu-id="51eee-690">There are not restrictions on key buffer.</span></span>
- <span data-ttu-id="51eee-691">**key_size_in_bits** Anahtarın bit cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-691">**key_size_in_bits** Size of the key, in bits.</span></span>
- <span data-ttu-id="51eee-692">**input_data** Girdi metin verileri içeren bir arabelleğe işaret eder.</span><span class="sxs-lookup"><span data-stu-id="51eee-692">**input_data** Points to a buffer containing input text data.</span></span> <span data-ttu-id="51eee-693">Giriş arabelleğinde kısıtlama yoktur.</span><span class="sxs-lookup"><span data-stu-id="51eee-693">There are not restrictions on input buffer.</span></span>
- <span data-ttu-id="51eee-694">**input_data_size** Giriş verilerinin bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-694">**input_data_size** Size of the input data, in bytes.</span></span>
- <span data-ttu-id="51eee-695">**iv_ptr** Bu alan HMAC SHA1 için kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-695">**iv_ptr** This field is not used for HMAC SHA1.</span></span>
- <span data-ttu-id="51eee-696">**iv_size** Bu alan HMAC SHA1 için kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-696">**iv_size** This field is not used for HMAC SHA1.</span></span>
- <span data-ttu-id="51eee-697">**output_buffer** Oluşturulan HMAC SHA1 karması için bellek alanına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-697">**output_buffer** Pointer to the memory area for the generated HMAC SHA1 hash.</span></span>
- <span data-ttu-id="51eee-698">**output_buffer_size** Çıkış arabelleğinin bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-698">**output_buffer_size** Size of the output buffer in bytes.</span></span>
- <span data-ttu-id="51eee-699">**crypto_metadata** *_Nx_crypto_method_hmac_sha1_init ()* IÇINDE kullanılan HMAC SHA1 denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-699">**crypto_metadata** Pointer to the HMAC SHA1 control block used in *_nx_crypto_method_hmac_sha1_init()*.</span></span>
- <span data-ttu-id="51eee-700">**crypto_metadata_size** Crypto_metadata alanının bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-700">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="51eee-701">HMAC SHA1 için, meta veri boyutu *sizeof olmalıdır (NX_CRYPTO_SHA1_HMAC)*</span><span class="sxs-lookup"><span data-stu-id="51eee-701">For HMAC SHA1, the metadata size must *sizeof(NX_CRYPTO_SHA1_HMAC)*</span></span>
- <span data-ttu-id="51eee-702">**packet_ptr** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-702">**packet_ptr** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="51eee-703">Geçirilen tüm değerler sessizce yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="51eee-703">Any values passed in are silently ignored.</span></span>
- <span data-ttu-id="51eee-704">**nx_crypto_hw_process_callback** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-704">**nx_crypto_hw_process_callback** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="51eee-705">Geçirilen tüm değerler sessizce yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="51eee-705">Any values passed in are silently ignored.</span></span>

### <a name="return-values"></a><span data-ttu-id="51eee-706">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="51eee-706">Return Values</span></span>

- <span data-ttu-id="51eee-707">**NX_CRYPTO_SUCCESS** (0x00) HMAC SHA1 işlemini başarıyla yürütüldü.</span><span class="sxs-lookup"><span data-stu-id="51eee-707">**NX_CRYPTO_SUCCESS** (0x00) Successfully executed the HMAC SHA1 operation.</span></span>
- <span data-ttu-id="51eee-708">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-708">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="51eee-709">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi veya uzunluğu geçersiz.</span><span class="sxs-lookup"><span data-stu-id="51eee-709">**NX_PTR_ERROR** (0x07) Invalid input pointer or invalid length.</span></span>
- <span data-ttu-id="51eee-710">**NX_CRYPTO_INVALID_ALGORITHM** (0x20004) GEÇERSIZ HMAC SHA1 algoritması belirtildi.</span><span class="sxs-lookup"><span data-stu-id="51eee-710">**NX_CRYPTO_INVALID_ALGORITHM** (0x20004) Invalid HMAC SHA1 algorithm being specified.</span></span>
- <span data-ttu-id="51eee-711">**NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) geçersiz çıkış arabelleği boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-711">**NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) Invalid output buffer size.</span></span>

## <a name="_nx_crypto_method_hmac_sha1_cleanup"></a><span data-ttu-id="51eee-712">_nx_crypto_method_hmac_sha1_cleanup</span><span class="sxs-lookup"><span data-stu-id="51eee-712">_nx_crypto_method_hmac_sha1_cleanup</span></span>

<span data-ttu-id="51eee-713">HMAC SHA1 denetim bloğunu temizleyin.</span><span class="sxs-lookup"><span data-stu-id="51eee-713">Clean up the HMAC SHA1 control block.</span></span>

### <a name="prototype"></a><span data-ttu-id="51eee-714">Prototype</span><span class="sxs-lookup"><span data-stu-id="51eee-714">Prototype</span></span>

```c
UINT _nx_crypto_method_hmac_sha1_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a><span data-ttu-id="51eee-715">Açıklama</span><span class="sxs-lookup"><span data-stu-id="51eee-715">Description</span></span>

<span data-ttu-id="51eee-716">Uygulama bu HMAC SHA1 denetim bloğunu, bu HMAC SHA1 oturumunun artık gerekli olmadığını belirledikten sonra temizlemek için bu işlevi çağırır.</span><span class="sxs-lookup"><span data-stu-id="51eee-716">Application calls this function to clean up the HMAC SHA1 control block after it determines this HMAC SHA1 session is no longer needed.</span></span>

### <a name="parameters"></a><span data-ttu-id="51eee-717">Parametreler</span><span class="sxs-lookup"><span data-stu-id="51eee-717">Parameters</span></span>

- <span data-ttu-id="51eee-718">**crypto_metadata** *_Nx_crypto_method_hmac_sha1_init ()* IÇINDE kullanılan HMAC SHA1 denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-718">**crypto_metadata** Pointer to the HMAC SHA1 control block used in *_nx_crypto_method_hmac_sha1_init()*.</span></span>

### <a name="return-values"></a><span data-ttu-id="51eee-719">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="51eee-719">Return Values</span></span>

- <span data-ttu-id="51eee-720">**NX_CRYPTO_SUCCESS** (0x00) HMAC SHA1 oturumunun başarıyla temizlendi.</span><span class="sxs-lookup"><span data-stu-id="51eee-720">**NX_CRYPTO_SUCCESS** (0x00) Successfully cleaned up the HMAC SHA1 session.</span></span>
- <span data-ttu-id="51eee-721">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-721">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>

## <a name="_nx_crypto_method_hmac_sha256_init"></a><span data-ttu-id="51eee-722">_nx_crypto_method_hmac_sha256_init</span><span class="sxs-lookup"><span data-stu-id="51eee-722">_nx_crypto_method_hmac_sha256_init</span></span>

<span data-ttu-id="51eee-723">HMAC SHA256 şifre denetim bloğunu başlatır</span><span class="sxs-lookup"><span data-stu-id="51eee-723">Initializes the HMAC SHA256 crypto control block</span></span>

### <a name="prototype"></a><span data-ttu-id="51eee-724">Prototype</span><span class="sxs-lookup"><span data-stu-id="51eee-724">Prototype</span></span>

```c
UINT _nx_crypto_method_hmac_sha256_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size);
```

### <a name="description"></a><span data-ttu-id="51eee-725">Açıklama</span><span class="sxs-lookup"><span data-stu-id="51eee-725">Description</span></span>

<span data-ttu-id="51eee-726">Bu işlev, HMAC SHA256 denetim bloğunu verilen anahtar dizesiyle başlatır.</span><span class="sxs-lookup"><span data-stu-id="51eee-726">This function initializes the HMAC SHA256 control block with the given key string.</span></span> <span data-ttu-id="51eee-727">HMAC SHA256 denetim bloğu başlatıldıktan sonra, sonraki HMAC SHA256 işlemi aynı denetim bloğunu kullanıyor olacaktır.</span><span class="sxs-lookup"><span data-stu-id="51eee-727">Once the HMAC SHA256 control block is initialized, subsequent HMAC SHA256 operation shall be using the same control block.</span></span>

<span data-ttu-id="51eee-728">Uygulama birden çok HMAC SHA256 denetim bloğu oluşturabilir, her biri bir oturumu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="51eee-728">Application may create multiple HMAC SHA256 control blocks, each represents a session.</span></span> <span data-ttu-id="51eee-729">HMAC SH256 denetim bloğunun başlatılması yeni bir karma hesaplama oturumu başlatır.</span><span class="sxs-lookup"><span data-stu-id="51eee-729">Initializing the HMAC SH256 control block starts a new hash computation session.</span></span> <span data-ttu-id="51eee-730">HMAC SHA256 denetim bloğunu yeniden başlatmak, geçerli oturum ve yıldızların yeni bir anahtarla yeni bir anahtarla bir yenisini terk edin.</span><span class="sxs-lookup"><span data-stu-id="51eee-730">Re-initializing the HMAC SHA256 control block abandons the current session and stars a new one with a new key.</span></span>

### <a name="parameters"></a><span data-ttu-id="51eee-731">Parametreler</span><span class="sxs-lookup"><span data-stu-id="51eee-731">Parameters</span></span>

- <span data-ttu-id="51eee-732">**yöntemi** Geçerli bir HMAC SHA256 şifreleme yöntemi denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-732">**method** Pointer to a valid HMAC SHA256 crypto method control block.</span></span> <span data-ttu-id="51eee-733">Aşağıdaki önceden tanımlanmış şifreleme yöntemleri kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="51eee-733">The following pre-defined crypto methods are available:</span></span>
  - <span data-ttu-id="51eee-734">*crypto_method_hmac_sha224*</span><span class="sxs-lookup"><span data-stu-id="51eee-734">*crypto_method_hmac_sha224*</span></span>
  - <span data-ttu-id="51eee-735">*crypto_method_hmac_sha256*</span><span class="sxs-lookup"><span data-stu-id="51eee-735">*crypto_method_hmac_sha256*</span></span>
- <span data-ttu-id="51eee-736">**anahtar** Anahtarı işaret eder.</span><span class="sxs-lookup"><span data-stu-id="51eee-736">**key** Points to the key.</span></span> <span data-ttu-id="51eee-737">Anahtar arabelleğinde kısıtlama yoktur.</span><span class="sxs-lookup"><span data-stu-id="51eee-737">There are not restrictions on key buffer.</span></span>
- <span data-ttu-id="51eee-738">**key_size_in_bits** Anahtarın bit cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-738">**key_size_in_bits** Size of the key, in bits.</span></span>
- <span data-ttu-id="51eee-739">**tanıtıcı** Bu hizmet, çağırana bir tanıtıcı döndürür.</span><span class="sxs-lookup"><span data-stu-id="51eee-739">**handle** This service returns a handle to the caller.</span></span> <span data-ttu-id="51eee-740">Tanıtıcı uygulamaya bağımlıdır ve bu uygulamada kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="51eee-740">The handle is implementation-dependent and is not being used in this implementation.</span></span> <span data-ttu-id="51eee-741">Uygulama tanıtıcı için NULL değer geçirecektir.</span><span class="sxs-lookup"><span data-stu-id="51eee-741">Application shall pass NULL for the handle.</span></span>
- <span data-ttu-id="51eee-742">**crypto_metadata** HMAC SHA256 denetim bloğu için geçerli bir bellek alanı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="51eee-742">**crypto_metadata** Pointer to a valid memory space for the HMAC SHA256 control block.</span></span> <span data-ttu-id="51eee-743">Bellek alanının başlangıç adresi 4 bayt hizalı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-743">The starting address of the memory space must be 4-byte aligned.</span></span>
- <span data-ttu-id="51eee-744">**crypto_metadata_size** Crypto_metadata alanının bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-744">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="51eee-745">HMAC SHA256 için meta veri boyutu *sizeof olmalıdır (NX_CRYTPO_SHA256_HMAC)*</span><span class="sxs-lookup"><span data-stu-id="51eee-745">For HMAC SHA256, the metadata size must be *sizeof(NX_CRYTPO_SHA256_HMAC)*</span></span>

### <a name="return-values"></a><span data-ttu-id="51eee-746">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="51eee-746">Return Values</span></span>

- <span data-ttu-id="51eee-747">**NX_CRYPTO_SUCCESS** (0x00) anahtar ve anahtar boyutuyla HMAC SHA256 denetim bloğunun başarıyla başlatılması.</span><span class="sxs-lookup"><span data-stu-id="51eee-747">**NX_CRYPTO_SUCCESS** (0x00) Successful initialization of the HMAC SHA256 control block with the key and key size.</span></span>
- <span data-ttu-id="51eee-748">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-748">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="51eee-749">**NX_PTR_ERROR** (0x07) anahtar için geçersiz işaretçi veya geçersiz crypto_metadata veya crypto_metadata_size ya da crypto_metadata 4 bayt hizalı değil.</span><span class="sxs-lookup"><span data-stu-id="51eee-749">**NX_PTR_ERROR** (0x07) Invalid pointer to the key, or invalid crypto_metadata or crypto_metadata_size, or crypto_metadata is not 4-byte aligned.</span></span>

## <a name="_nx_crypto_method_hmac_sha256_operation"></a><span data-ttu-id="51eee-750">_nx_crypto_method_hmac_sha256_operation</span><span class="sxs-lookup"><span data-stu-id="51eee-750">_nx_crypto_method_hmac_sha256_operation</span></span>

<span data-ttu-id="51eee-751">HMAC SHA256 karma işlemi gerçekleştir</span><span class="sxs-lookup"><span data-stu-id="51eee-751">Perform HMAC SHA256 hash operation</span></span>

### <a name="prototype"></a><span data-ttu-id="51eee-752">Prototype</span><span class="sxs-lookup"><span data-stu-id="51eee-752">Prototype</span></span>

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

### <a name="description"></a><span data-ttu-id="51eee-753">Açıklama</span><span class="sxs-lookup"><span data-stu-id="51eee-753">Description</span></span>

<span data-ttu-id="51eee-754">Bu işlev HMAC SHA256 karma işlemi gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="51eee-754">This function performs HMAC SHA256 hash operation.</span></span> <span data-ttu-id="51eee-755">HMAC SHA256 denetim bloğu _ *nx_crypto_method_hmac_sha256_init ()* ile başlatılmış olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-755">The HMAC SHA256 control block must have been initialized with _ *nx_crypto_method_hmac_sha256_init()*.</span></span> <span data-ttu-id="51eee-756">Gerçekleştirilecek HMAC SHA256 algoritması, *Yöntem* denetim bloğunda belirtilen algoritmayı temel alır.</span><span class="sxs-lookup"><span data-stu-id="51eee-756">The HMAC SHA256 algorithm to be performed is based on the algorithm specified in the *method* control block.</span></span>

<span data-ttu-id="51eee-757">Son *NX_CRYPTO_HASH_CALCULATE* işlemi için, çıkış ARABELLEĞI boyutu SHA256 için 32 bayt veya SHA224 için 28 bayt olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-757">For the final *NX_CRYPTO_HASH_CALCULATE* operation, the output buffer size must be 32 bytes for SHA256, or 28 bytes for SHA224.</span></span>

### <a name="parameters"></a><span data-ttu-id="51eee-758">Parametreler</span><span class="sxs-lookup"><span data-stu-id="51eee-758">Parameters</span></span>

- <span data-ttu-id="51eee-759">**op** Gerçekleştirilecek işlemin türü.</span><span class="sxs-lookup"><span data-stu-id="51eee-759">**op** Type of operation to perform.</span></span> <span data-ttu-id="51eee-760">Geçerli işlem:</span><span class="sxs-lookup"><span data-stu-id="51eee-760">Valid operation is:</span></span>
  - <span data-ttu-id="51eee-761">*NX_CRYPTO_HASH_INITIALIZE*</span><span class="sxs-lookup"><span data-stu-id="51eee-761">*NX_CRYPTO_HASH_INITIALIZE*</span></span>
  - <span data-ttu-id="51eee-762">*NX_CRYPTO_HASH_UPDATE*</span><span class="sxs-lookup"><span data-stu-id="51eee-762">*NX_CRYPTO_HASH_UPDATE*</span></span>
  - <span data-ttu-id="51eee-763">*NX_CRYPTO_HASH_CALCULATE*</span><span class="sxs-lookup"><span data-stu-id="51eee-763">*NX_CRYPTO_HASH_CALCULATE*</span></span>
- <span data-ttu-id="51eee-764">**tanıtıcı** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-764">**handle** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="51eee-765">Geçirilen tüm değerler sessizce yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="51eee-765">Any values passed in are silently ignored.</span></span>
- <span data-ttu-id="51eee-766">**yöntemi** Geçerli HMAC SHA256 şifre yöntemine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-766">**method** Pointer to the valid HMAC SHA256 crypto method.</span></span> <span data-ttu-id="51eee-767">Burada kullanılan şifreleme yöntemi _ *nx_crypto_method_hmac_sha256_init ()* içinde kullanılan aynı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-767">The crypto method used here must be the same used in the _ *nx_crypto_method_hmac_sha256_init().*</span></span>
- <span data-ttu-id="51eee-768">**anahtar** Anahtarı işaret eder.</span><span class="sxs-lookup"><span data-stu-id="51eee-768">**key** Points to the key.</span></span> <span data-ttu-id="51eee-769">Anahtar arabelleğinde kısıtlama yoktur.</span><span class="sxs-lookup"><span data-stu-id="51eee-769">There are not restrictions on key buffer.</span></span>
- <span data-ttu-id="51eee-770">**key_size_in_bits** Anahtarın bit cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-770">**key_size_in_bits** Size of the key, in bits.</span></span>
- <span data-ttu-id="51eee-771">**input_data** Girdi metin verileri içeren bir arabelleğe işaret eder.</span><span class="sxs-lookup"><span data-stu-id="51eee-771">**input_data** Points to a buffer containing input text data.</span></span> <span data-ttu-id="51eee-772">Giriş arabelleğinde kısıtlama yoktur.</span><span class="sxs-lookup"><span data-stu-id="51eee-772">There are not restrictions on input buffer.</span></span>
- <span data-ttu-id="51eee-773">**input_data_size** Giriş verilerinin bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-773">**input_data_size** Size of the input data, in bytes.</span></span>
- <span data-ttu-id="51eee-774">**iv_ptr** Bu alan HMAC SHA256 için kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-774">**iv_ptr** This field is not used for HMAC SHA256.</span></span>
- <span data-ttu-id="51eee-775">**iv_size** Bu alan HMAC SHA256 için kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-775">**iv_size** This field is not used for HMAC SHA256.</span></span>
- <span data-ttu-id="51eee-776">**output_buffer** Oluşturulan HMAC SHA256 karması için bellek alanına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-776">**output_buffer** Pointer to the memory area for the generated HMAC SHA256 hash.</span></span>
- <span data-ttu-id="51eee-777">**output_buffer_size** Çıkış arabelleğinin bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-777">**output_buffer_size** Size of the output buffer in bytes.</span></span>
- <span data-ttu-id="51eee-778">**crypto_metadata** *_Nx_crypto_method_hmac_sha256_init ()* IÇINDE kullanılan HMAC SHA256 denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-778">**crypto_metadata** Pointer to the HMAC SHA256 control block used in *_nx_crypto_method_hmac_sha256_init()*.</span></span>
- <span data-ttu-id="51eee-779">**crypto_metadata_size** Crypto_metadata alanının bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-779">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="51eee-780">HMAC SHA256 için meta veri boyutu sizeof olmalıdır *(NX_CRYPTO_SHA256_HMAC)*</span><span class="sxs-lookup"><span data-stu-id="51eee-780">For HMAC SHA256, the metadata size must *sizeof(NX_CRYPTO_SHA256_HMAC)*</span></span>
- <span data-ttu-id="51eee-781">**packet_ptr** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-781">**packet_ptr** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="51eee-782">Geçirilen tüm değerler sessizce yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="51eee-782">Any values passed in are silently ignored.</span></span>
- <span data-ttu-id="51eee-783">**nx_crypto_hw_process_callback** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-783">**nx_crypto_hw_process_callback** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="51eee-784">Geçirilen tüm değerler sessizce yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="51eee-784">Any values passed in are silently ignored.</span></span>

### <a name="return-values"></a><span data-ttu-id="51eee-785">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="51eee-785">Return Values</span></span>

- <span data-ttu-id="51eee-786">**NX_CRYPTO_SUCCESS** (0x00) HMAC SHA256 işlemini başarıyla yürütüldü.</span><span class="sxs-lookup"><span data-stu-id="51eee-786">**NX_CRYPTO_SUCCESS** (0x00) Successfully executed the HMAC SHA256 operation.</span></span>
- <span data-ttu-id="51eee-787">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-787">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="51eee-788">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi veya uzunluğu geçersiz.</span><span class="sxs-lookup"><span data-stu-id="51eee-788">**NX_PTR_ERROR** (0x07) Invalid input pointer or invalid length.</span></span>
- <span data-ttu-id="51eee-789">**NX_CRYPTO_INVALID_ALGORITHM** (0x20004) GEÇERSIZ HMAC SHA256 algoritması belirtildi.</span><span class="sxs-lookup"><span data-stu-id="51eee-789">**NX_CRYPTO_INVALID_ALGORITHM** (0x20004) Invalid HMAC SHA256 algorithm being specified.</span></span>
- <span data-ttu-id="51eee-790">**NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) geçersiz çıkış arabelleği boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-790">**NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) Invalid output buffer size.</span></span>

## <a name="_nx_crypto_method_hmac_sha256_cleanup"></a><span data-ttu-id="51eee-791">_nx_crypto_method_hmac_sha256_cleanup</span><span class="sxs-lookup"><span data-stu-id="51eee-791">_nx_crypto_method_hmac_sha256_cleanup</span></span>

<span data-ttu-id="51eee-792">HMAC SHA256 denetim bloğunu temizleyin.</span><span class="sxs-lookup"><span data-stu-id="51eee-792">Clean up the HMAC SHA256 control block.</span></span>

### <a name="prototype"></a><span data-ttu-id="51eee-793">Prototype</span><span class="sxs-lookup"><span data-stu-id="51eee-793">Prototype</span></span>

```c
UINT _nx_crypto_method_hmac_sha256_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a><span data-ttu-id="51eee-794">Açıklama</span><span class="sxs-lookup"><span data-stu-id="51eee-794">Description</span></span>

<span data-ttu-id="51eee-795">Uygulama, bu HMAC SHA256 oturumunun artık gerekli olmadığını belirlediğinde HMAC SHA256 denetim bloğunu temizlemek için bu işlevi çağırır.</span><span class="sxs-lookup"><span data-stu-id="51eee-795">Application calls this function to clean up the HMAC SHA256 control block after it determines this HMAC SHA256 session is no longer needed.</span></span>

### <a name="parameters"></a><span data-ttu-id="51eee-796">Parametreler</span><span class="sxs-lookup"><span data-stu-id="51eee-796">Parameters</span></span>

- <span data-ttu-id="51eee-797">**crypto_metadata** *_Nx_crypto_method_hmac_sha256_init ()* IÇINDE kullanılan HMAC SHA256 denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-797">**crypto_metadata** Pointer to the HMAC SHA256 control block used in *_nx_crypto_method_hmac_sha256_init()*.</span></span>

### <a name="return-values"></a><span data-ttu-id="51eee-798">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="51eee-798">Return Values</span></span>

- <span data-ttu-id="51eee-799">**NX_CRYPTO_SUCCESS** (0x00) HMAC SHA256 oturumu başarıyla temizlendi.</span><span class="sxs-lookup"><span data-stu-id="51eee-799">**NX_CRYPTO_SUCCESS** (0x00) Successfully cleaned up the HMAC SHA256 session.</span></span>
- <span data-ttu-id="51eee-800">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-800">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>

## <a name="_nx_crypto_method_hmac_sha512_init"></a><span data-ttu-id="51eee-801">_nx_crypto_method_hmac_sha512_init</span><span class="sxs-lookup"><span data-stu-id="51eee-801">_nx_crypto_method_hmac_sha512_init</span></span>

<span data-ttu-id="51eee-802">HMAC SHA512 olur şifre denetim bloğunu başlatır</span><span class="sxs-lookup"><span data-stu-id="51eee-802">Initializes the HMAC SHA512 crypto control block</span></span>

### <a name="prototype"></a><span data-ttu-id="51eee-803">Prototype</span><span class="sxs-lookup"><span data-stu-id="51eee-803">Prototype</span></span>

```c
UINT _nx_crypto_method_hmac_sha512_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size);
```

### <a name="description"></a><span data-ttu-id="51eee-804">Açıklama</span><span class="sxs-lookup"><span data-stu-id="51eee-804">Description</span></span>

<span data-ttu-id="51eee-805">Bu işlev, HMAC SHA512 olur denetim bloğunu verilen anahtar dizesiyle başlatır.</span><span class="sxs-lookup"><span data-stu-id="51eee-805">This function initializes the HMAC SHA512 control block with the given key string.</span></span> <span data-ttu-id="51eee-806">HMAC SHA512 olur denetim bloğu başlatıldıktan sonra, sonraki HMAC SHA512 olur işlemi aynı denetim bloğunu kullanıyor olacaktır.</span><span class="sxs-lookup"><span data-stu-id="51eee-806">Once the HMAC SHA512 control block is initialized, subsequent HMAC SHA512 operation shall be using the same control block.</span></span>

<span data-ttu-id="51eee-807">Uygulama birden çok HMAC SHA512 olur denetim bloğu oluşturabilir, her biri bir oturumu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="51eee-807">Application may create multiple HMAC SHA512 control blocks, each represents a session.</span></span> <span data-ttu-id="51eee-808">HMAC SH512 denetim bloğunun başlatılması yeni bir karma hesaplama oturumu başlatır.</span><span class="sxs-lookup"><span data-stu-id="51eee-808">Initializing the HMAC SH512 control block starts a new hash computation session.</span></span> <span data-ttu-id="51eee-809">HMAC SHA512 olur denetim bloğunu yeniden başlatmak, geçerli oturum ve yıldızların yeni bir anahtarla yeni bir anahtarla bir yenisini terk edin.</span><span class="sxs-lookup"><span data-stu-id="51eee-809">Re-initializing the HMAC SHA512 control block abandons the current session and stars a new one with a new key.</span></span>

### <a name="parameters"></a><span data-ttu-id="51eee-810">Parametreler</span><span class="sxs-lookup"><span data-stu-id="51eee-810">Parameters</span></span>

- <span data-ttu-id="51eee-811">**yöntemi** Geçerli bir HMAC SHA512 olur şifreleme yöntemi denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-811">**method** Pointer to a valid HMAC SHA512 crypto method control block.</span></span> <span data-ttu-id="51eee-812">Aşağıdaki önceden tanımlanmış şifreleme yöntemleri kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="51eee-812">The following pre-defined crypto methods are available:</span></span>
  - <span data-ttu-id="51eee-813">*crypto_method_hmac_sha384*</span><span class="sxs-lookup"><span data-stu-id="51eee-813">*crypto_method_hmac_sha384*</span></span>
  - <span data-ttu-id="51eee-814">*crypto_method_hmac_sha512*</span><span class="sxs-lookup"><span data-stu-id="51eee-814">*crypto_method_hmac_sha512*</span></span>
- <span data-ttu-id="51eee-815">**anahtar** Anahtarı işaret eder.</span><span class="sxs-lookup"><span data-stu-id="51eee-815">**key** Points to the key.</span></span> <span data-ttu-id="51eee-816">Anahtar arabelleğinde kısıtlama yoktur.</span><span class="sxs-lookup"><span data-stu-id="51eee-816">There are not restrictions on key buffer.</span></span>
- <span data-ttu-id="51eee-817">**key_size_in_bits** Anahtarın bit cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-817">**key_size_in_bits** Size of the key, in bits.</span></span>
- <span data-ttu-id="51eee-818">**tanıtıcı** Bu hizmet, çağırana bir tanıtıcı döndürür.</span><span class="sxs-lookup"><span data-stu-id="51eee-818">**handle** This service returns a handle to the caller.</span></span> <span data-ttu-id="51eee-819">Tanıtıcı uygulamaya bağımlıdır ve bu uygulamada kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="51eee-819">The handle is implementation-dependent, and is not being used in this implementation.</span></span> <span data-ttu-id="51eee-820">Uygulama tanıtıcı için NULL değer geçirecektir.</span><span class="sxs-lookup"><span data-stu-id="51eee-820">Application shall pass NULL for the handle.</span></span>
- <span data-ttu-id="51eee-821">**crypto_metadata** HMAC SHA512 olur denetim bloğu için geçerli bir bellek alanı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="51eee-821">**crypto_metadata** Pointer to a valid memory space for the HMAC SHA512 control block.</span></span> <span data-ttu-id="51eee-822">Bellek alanının başlangıç adresi 4 bayt hizalı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-822">The starting address of the memory space must be 4-byte aligned.</span></span>
- <span data-ttu-id="51eee-823">**crypto_metadata_size** Crypto_metadata alanının bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-823">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="51eee-824">HMAC SHA512 olur için meta veri boyutu *sizeof olmalıdır (NX_CRYPTO_SHA512_HMAC)*</span><span class="sxs-lookup"><span data-stu-id="51eee-824">For HMAC SHA512, the metadata size must be *sizeof(NX_CRYPTO_SHA512_HMAC)*</span></span>

### <a name="return-values"></a><span data-ttu-id="51eee-825">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="51eee-825">Return Values</span></span>

- <span data-ttu-id="51eee-826">**NX_CRYPTO_SUCCESS** (0x00) anahtar ve anahtar boyutuyla HMAC SHA512 olur denetim bloğunun başarıyla başlatılması.</span><span class="sxs-lookup"><span data-stu-id="51eee-826">**NX_CRYPTO_SUCCESS** (0x00) Successful initialization of the HMAC SHA512 control block with the key and key size.</span></span>
- <span data-ttu-id="51eee-827">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-827">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="51eee-828">**NX_PTR_ERROR** (0x07) anahtar için geçersiz işaretçi veya geçersiz crypto_metadata veya crypto_metadata_size ya da crypto_metadata 4 bayt hizalı değil.</span><span class="sxs-lookup"><span data-stu-id="51eee-828">**NX_PTR_ERROR** (0x07) Invalid pointer to the key, or invalid crypto_metadata or crypto_metadata_size, or crypto_metadata is not 4-byte aligned.</span></span>

## <a name="_nx_crypto_method_hmac_sha512_operation"></a><span data-ttu-id="51eee-829">_nx_crypto_method_hmac_sha512_operation</span><span class="sxs-lookup"><span data-stu-id="51eee-829">_nx_crypto_method_hmac_sha512_operation</span></span>

<span data-ttu-id="51eee-830">HMAC SHA512 olur karma işlemi gerçekleştir</span><span class="sxs-lookup"><span data-stu-id="51eee-830">Perform HMAC SHA512 hash operation</span></span>

### <a name="prototype"></a><span data-ttu-id="51eee-831">Prototype</span><span class="sxs-lookup"><span data-stu-id="51eee-831">Prototype</span></span>

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

### <a name="description"></a><span data-ttu-id="51eee-832">Açıklama</span><span class="sxs-lookup"><span data-stu-id="51eee-832">Description</span></span>

<span data-ttu-id="51eee-833">Bu işlev HMAC SHA512 olur karma işlemi gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="51eee-833">This function performs HMAC SHA512 hash operation.</span></span> <span data-ttu-id="51eee-834">HMAC SHA512 olur denetim bloğu _ *nx_crypto_method_hmac_sha512_init ()* ile başlatılmış olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-834">The HMAC SHA512 control block must have been initialized with _ *nx_crypto_method_hmac_sha512_init()*.</span></span> <span data-ttu-id="51eee-835">Gerçekleştirilecek HMAC SHA512 olur algoritması, *Yöntem* denetim bloğunda belirtilen algoritmayı temel alır.</span><span class="sxs-lookup"><span data-stu-id="51eee-835">The HMAC SHA512 algorithm to be performed is based on the algorithm specified in the *method* control block.</span></span>

<span data-ttu-id="51eee-836">Son *NX_CRYPTO_HASH_CALCULATE* işlemi için, çıkış ARABELLEĞI boyutu sha512 olur için 64 bayt veya SHA384 için 48 bayt olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-836">For the final *NX_CRYPTO_HASH_CALCULATE* operation, the output buffer size must be 64 bytes for SHA512, or 48 bytes for SHA384.</span></span>

### <a name="parameters"></a><span data-ttu-id="51eee-837">Parametreler</span><span class="sxs-lookup"><span data-stu-id="51eee-837">Parameters</span></span>

- <span data-ttu-id="51eee-838">**op** Gerçekleştirilecek işlemin türü.</span><span class="sxs-lookup"><span data-stu-id="51eee-838">**op** Type of operation to perform.</span></span> <span data-ttu-id="51eee-839">Geçerli işlem:</span><span class="sxs-lookup"><span data-stu-id="51eee-839">Valid operation is:</span></span>
  - <span data-ttu-id="51eee-840">*NX_CRYPTO_HASH_INITIALIZE*</span><span class="sxs-lookup"><span data-stu-id="51eee-840">*NX_CRYPTO_HASH_INITIALIZE*</span></span>
  - <span data-ttu-id="51eee-841">*NX_CRYPTO_HASH_UPDATE*</span><span class="sxs-lookup"><span data-stu-id="51eee-841">*NX_CRYPTO_HASH_UPDATE*</span></span>
  - <span data-ttu-id="51eee-842">*NX_CRYPTO_HASH_CALCULATE*</span><span class="sxs-lookup"><span data-stu-id="51eee-842">*NX_CRYPTO_HASH_CALCULATE*</span></span>
- <span data-ttu-id="51eee-843">**tanıtıcı** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-843">**handle** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="51eee-844">Geçirilen tüm değerler sessizce yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="51eee-844">Any values passed in are silently ignored.</span></span>
- <span data-ttu-id="51eee-845">**yöntemi** Geçerli HMAC SHA512 olur şifre yöntemine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-845">**method** Pointer to the valid HMAC SHA512 crypto method.</span></span> <span data-ttu-id="51eee-846">Burada kullanılan şifreleme yöntemi _ *nx_crypto_method_hmac_sha512_init ()* içinde kullanılan aynı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-846">The crypto method used here must be the same used in the _ *nx_crypto_method_hmac_sha512_init().*</span></span>
- <span data-ttu-id="51eee-847">**anahtar** Anahtarı işaret eder.</span><span class="sxs-lookup"><span data-stu-id="51eee-847">**key** Points to the key.</span></span> <span data-ttu-id="51eee-848">Anahtar arabelleğinde kısıtlama yoktur.</span><span class="sxs-lookup"><span data-stu-id="51eee-848">There are not restrictions on key buffer.</span></span>
- <span data-ttu-id="51eee-849">**key_size_in_bits** Anahtarın bit cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-849">**key_size_in_bits** Size of the key, in bits.</span></span>
- <span data-ttu-id="51eee-850">**input_data** Girdi metin verileri içeren bir arabelleğe işaret eder.</span><span class="sxs-lookup"><span data-stu-id="51eee-850">**input_data** Points to a buffer containing input text data.</span></span> <span data-ttu-id="51eee-851">Giriş arabelleğinde kısıtlama yoktur.</span><span class="sxs-lookup"><span data-stu-id="51eee-851">There are not restrictions on input buffer.</span></span>
- <span data-ttu-id="51eee-852">**input_data_size** Giriş verilerinin bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-852">**input_data_size** Size of the input data, in bytes.</span></span>
- <span data-ttu-id="51eee-853">**iv_ptr** Bu alan HMAC SHA512 olur için kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-853">**iv_ptr** This field is not used for HMAC SHA512.</span></span>
- <span data-ttu-id="51eee-854">**iv_size** Bu alan HMAC SHA512 olur için kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-854">**iv_size** This field is not used for HMAC SHA512.</span></span>
- <span data-ttu-id="51eee-855">**output_buffer** Oluşturulan HMAC SHA512 olur karması için bellek alanına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-855">**output_buffer** Pointer to the memory area for the generated HMAC SHA512 hash.</span></span>
- <span data-ttu-id="51eee-856">**output_buffer_size** Çıkış arabelleğinin bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-856">**output_buffer_size** Size of the output buffer in bytes.</span></span>
- <span data-ttu-id="51eee-857">**crypto_metadata** *_Nx_crypto_method_hmac_sha512_init ()* IÇINDE kullanılan HMAC SHA512 olur denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-857">**crypto_metadata** Pointer to the HMAC SHA512 control block used in *_nx_crypto_method_hmac_sha512_init()*.</span></span>
- <span data-ttu-id="51eee-858">**crypto_metadata_size** Crypto_metadata alanının bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-858">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="51eee-859">HMAC SHA512 olur için meta veri boyutu sizeof olmalıdır *(NX_CRYPTO_SHA512_HMAC)*</span><span class="sxs-lookup"><span data-stu-id="51eee-859">For HMAC SHA512, the metadata size must *sizeof(NX_CRYPTO_SHA512_HMAC)*</span></span>
- <span data-ttu-id="51eee-860">**packet_ptr** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-860">**packet_ptr** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="51eee-861">Geçirilen tüm değerler sessizce yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="51eee-861">Any values passed in are silently ignored.</span></span>
- <span data-ttu-id="51eee-862">**nx_crypto_hw_process_callback** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-862">**nx_crypto_hw_process_callback** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="51eee-863">Geçirilen tüm değerler sessizce yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="51eee-863">Any values passed in are silently ignored.</span></span>

### <a name="return-values"></a><span data-ttu-id="51eee-864">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="51eee-864">Return Values</span></span>

- <span data-ttu-id="51eee-865">**NX_CRYPTO_SUCCESS** (0x00) HMAC SHA512 olur işlemini başarıyla yürütüldü.</span><span class="sxs-lookup"><span data-stu-id="51eee-865">**NX_CRYPTO_SUCCESS** (0x00) Successfully executed the HMAC SHA512 operation.</span></span>
- <span data-ttu-id="51eee-866">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-866">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="51eee-867">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi veya uzunluğu geçersiz.</span><span class="sxs-lookup"><span data-stu-id="51eee-867">**NX_PTR_ERROR** (0x07) Invalid input pointer or invalid length.</span></span>
- <span data-ttu-id="51eee-868">**NX_CRYPTO_INVALID_ALGORITHM** (0x20004) GEÇERSIZ HMAC SHA512 olur algoritması belirtildi.</span><span class="sxs-lookup"><span data-stu-id="51eee-868">**NX_CRYPTO_INVALID_ALGORITHM** (0x20004) Invalid HMAC SHA512 algorithm being specified.</span></span>
- <span data-ttu-id="51eee-869">**NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) geçersiz çıkış arabelleği boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-869">**NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) Invalid output buffer size.</span></span>

## <a name="_nx_crypto_method_hmac_sha512_cleanup"></a><span data-ttu-id="51eee-870">_nx_crypto_method_hmac_sha512_cleanup</span><span class="sxs-lookup"><span data-stu-id="51eee-870">_nx_crypto_method_hmac_sha512_cleanup</span></span>

<span data-ttu-id="51eee-871">HMAC SHA512 olur denetim bloğunu temizleyin.</span><span class="sxs-lookup"><span data-stu-id="51eee-871">Clean up the HMAC SHA512 control block.</span></span>

### <a name="prototype"></a><span data-ttu-id="51eee-872">Prototype</span><span class="sxs-lookup"><span data-stu-id="51eee-872">Prototype</span></span>

```c
UINT _nx_crypto_method_hmac_sha512_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a><span data-ttu-id="51eee-873">Açıklama</span><span class="sxs-lookup"><span data-stu-id="51eee-873">Description</span></span>

<span data-ttu-id="51eee-874">Uygulama, bu HMAC SHA512 olur oturumunun artık gerekli olmadığını belirlediğinde HMAC SHA512 olur denetim bloğunu temizlemek için bu işlevi çağırır.</span><span class="sxs-lookup"><span data-stu-id="51eee-874">Application calls this function to clean up the HMAC SHA512 control block after it determines this HMAC SHA512 session is no longer needed.</span></span>

### <a name="parameters"></a><span data-ttu-id="51eee-875">Parametreler</span><span class="sxs-lookup"><span data-stu-id="51eee-875">Parameters</span></span>

- <span data-ttu-id="51eee-876">**crypto_metadata** *_Nx_crypto_method_hmac_sha512_init ()* IÇINDE kullanılan HMAC SHA512 olur denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-876">**crypto_metadata** Pointer to the HMAC SHA512 control block used in *_nx_crypto_method_hmac_sha512_init()*.</span></span>

### <a name="return-values"></a><span data-ttu-id="51eee-877">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="51eee-877">Return Values</span></span>

- <span data-ttu-id="51eee-878">**NX_CRYPTO_SUCCESS** (0x00) HMAC SHA512 olur oturumu başarıyla temizlendi.</span><span class="sxs-lookup"><span data-stu-id="51eee-878">**NX_CRYPTO_SUCCESS** (0x00) Successfully cleaned up the HMAC SHA512 session.</span></span>
- <span data-ttu-id="51eee-879">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-879">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>

### <a name="example"></a><span data-ttu-id="51eee-880">Örnek</span><span class="sxs-lookup"><span data-stu-id="51eee-880">Example</span></span> 

## <a name="_nx_crypto_method_md5_init"></a><span data-ttu-id="51eee-881">_nx_crypto_method_md5_init</span><span class="sxs-lookup"><span data-stu-id="51eee-881">_nx_crypto_method_md5_init</span></span>

<span data-ttu-id="51eee-882">MD5 şifreleme denetim bloğunu başlatır</span><span class="sxs-lookup"><span data-stu-id="51eee-882">Initializes the MD5 crypto control block</span></span>

### <a name="prototype"></a><span data-ttu-id="51eee-883">Prototype</span><span class="sxs-lookup"><span data-stu-id="51eee-883">Prototype</span></span>

```c
UINT _nx_crypto_method_md5_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size);
```

### <a name="description"></a><span data-ttu-id="51eee-884">Açıklama</span><span class="sxs-lookup"><span data-stu-id="51eee-884">Description</span></span>

<span data-ttu-id="51eee-885">Bu işlev, MD5 denetim bloğunu verilen anahtar dizesiyle başlatır.</span><span class="sxs-lookup"><span data-stu-id="51eee-885">This function initializes the MD5 control block with the given key string.</span></span> <span data-ttu-id="51eee-886">MD5 denetim bloğu başlatıldıktan sonra, sonraki MD5 işlemi aynı denetim bloğunu kullanıyor olacaktır.</span><span class="sxs-lookup"><span data-stu-id="51eee-886">Once the MD5 control block is initialized, subsequent MD5 operation shall be using the same control block.</span></span>

<span data-ttu-id="51eee-887">Uygulama birden çok MD5 denetim bloğu oluşturabilir, her biri bir oturumu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="51eee-887">Application may create multiple MD5 control blocks, each represents a session.</span></span> <span data-ttu-id="51eee-888">MD5 denetim bloğunun başlatılması yeni bir karma hesaplama oturumu başlatır.</span><span class="sxs-lookup"><span data-stu-id="51eee-888">Initializing the MD5 control block starts a new hash computation session.</span></span> <span data-ttu-id="51eee-889">MD5 denetim bloğunu yeniden başlatmak, geçerli oturumu ve yıldızları yeni bir kez geri başlatmakta.</span><span class="sxs-lookup"><span data-stu-id="51eee-889">Re-initializing the MD5 control block abandons the current session and stars a new one.</span></span>

### <a name="parameters"></a><span data-ttu-id="51eee-890">Parametreler</span><span class="sxs-lookup"><span data-stu-id="51eee-890">Parameters</span></span>

- <span data-ttu-id="51eee-891">**yöntemi** Geçerli bir MD5 şifreleme yöntemi denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-891">**method** Pointer to a valid MD5 crypto method control block.</span></span> <span data-ttu-id="51eee-892">Aşağıdaki önceden tanımlanmış şifreleme yöntemleri kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="51eee-892">The following pre-defined crypto methods are available:</span></span>
  - <span data-ttu-id="51eee-893">*crypto_method_md5*</span><span class="sxs-lookup"><span data-stu-id="51eee-893">*crypto_method_md5*</span></span>
- <span data-ttu-id="51eee-894">**anahtar** Bu alan MD5 için kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-894">**key** This field is not used for MD5.</span></span>
- <span data-ttu-id="51eee-895">**key_size_in_bits** Bu alan MD5 için kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="51eee-895">**key_size_in_bits** This field is not used for MD5</span></span>
- <span data-ttu-id="51eee-896">**tanıtıcı** Bu hizmet, çağırana bir tanıtıcı döndürür.</span><span class="sxs-lookup"><span data-stu-id="51eee-896">**handle** This service returns a handle to the caller.</span></span> <span data-ttu-id="51eee-897">Tanıtıcı uygulamaya bağımlıdır ve bu uygulamada kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="51eee-897">The handle is implementation-dependent and is not being used in this implementation.</span></span> <span data-ttu-id="51eee-898">Uygulama tanıtıcı için NULL değer geçirecektir.</span><span class="sxs-lookup"><span data-stu-id="51eee-898">Application shall pass NULL for the handle.</span></span>
- <span data-ttu-id="51eee-899">**crypto_metadata** MD5 denetim bloğu için geçerli bir bellek alanı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="51eee-899">**crypto_metadata** Pointer to a valid memory space for the MD5 control block.</span></span> <span data-ttu-id="51eee-900">Bellek alanının başlangıç adresi 4 bayt hizalı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-900">The starting address of the memory space must be 4-byte aligned.</span></span>
- <span data-ttu-id="51eee-901">**crypto_metadata_size** Crypto_metadata alanının bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-901">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="51eee-902">MD5 için meta veri boyutu *sizeof olmalıdır (NX_CRYPTO_MD5)*</span><span class="sxs-lookup"><span data-stu-id="51eee-902">For MD5, the metadata size must be *sizeof(NX_CRYPTO_MD5)*</span></span>

### <a name="return-values"></a><span data-ttu-id="51eee-903">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="51eee-903">Return Values</span></span>

- <span data-ttu-id="51eee-904">Anahtar ve anahtar boyutuyla, MD5 denetim bloğunun başarılı bir şekilde başlatılması **NX_CRYPTO_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="51eee-904">**NX_CRYPTO_SUCCESS** (0x00) Successful initialization of the MD5 control block with the key and key size.</span></span>
- <span data-ttu-id="51eee-905">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-905">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="51eee-906">**NX_PTR_ERROR** (0x07) anahtar için geçersiz işaretçi veya geçersiz crypto_metadata veya crypto_metadata_size ya da crypto_metadata 4 bayt hizalı değil.</span><span class="sxs-lookup"><span data-stu-id="51eee-906">**NX_PTR_ERROR** (0x07) Invalid pointer to the key, or invalid crypto_metadata or crypto_metadata_size, or crypto_metadata is not 4-byte aligned.</span></span>

### <a name="example"></a><span data-ttu-id="51eee-907">Örnek</span><span class="sxs-lookup"><span data-stu-id="51eee-907">Example</span></span>

## <a name="_nx_crypto_method_md5_operation"></a><span data-ttu-id="51eee-908">_nx_crypto_method_md5_operation</span><span class="sxs-lookup"><span data-stu-id="51eee-908">_nx_crypto_method_md5_operation</span></span>

<span data-ttu-id="51eee-909">MD5 karma işlemi gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="51eee-909">Perform an MD5 hash operation.</span></span>

### <a name="prototype"></a><span data-ttu-id="51eee-910">Prototype</span><span class="sxs-lookup"><span data-stu-id="51eee-910">Prototype</span></span>

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

### <a name="description"></a><span data-ttu-id="51eee-911">Açıklama</span><span class="sxs-lookup"><span data-stu-id="51eee-911">Description</span></span>

<span data-ttu-id="51eee-912">Bu işlev, MD5 karma işlemini gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="51eee-912">This function performs MD5 hash operation.</span></span> <span data-ttu-id="51eee-913">MD5 denetim bloğunun _ *nx_crypto_method_md5_init ()* ile başlatılmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="51eee-913">The MD5 control block must have been initialized with _ *nx_crypto_method_md5_init()*.</span></span> <span data-ttu-id="51eee-914">Gerçekleştirilecek MD5 algoritması, *Yöntem* denetim bloğunda belirtilen algoritmayı temel alır.</span><span class="sxs-lookup"><span data-stu-id="51eee-914">The MD5 algorithm to be performed is based on the algorithm specified in the *method* control block.</span></span>

<span data-ttu-id="51eee-915">Son *NX_CRYPTO_HASH_CALCULATE* işlemi için, çıkış arabelleği boyutu 16 bayt olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-915">For the final *NX_CRYPTO_HASH_CALCULATE* operation, the output buffer size must be 16 bytes.</span></span>

<span data-ttu-id="51eee-916">Bu işlem durum bilgilerini tutar ve MD5 denetim bloğunda anahtar malzemesini değiştirmez.</span><span class="sxs-lookup"><span data-stu-id="51eee-916">This operation does not keep state information and does not alter the key material in the MD5 control block.</span></span>

### <a name="parameters"></a><span data-ttu-id="51eee-917">Parametreler</span><span class="sxs-lookup"><span data-stu-id="51eee-917">Parameters</span></span>

- <span data-ttu-id="51eee-918">**op** Gerçekleştirilecek işlemin türü.</span><span class="sxs-lookup"><span data-stu-id="51eee-918">**op** Type of operation to perform.</span></span> <span data-ttu-id="51eee-919">Geçerli işlem:</span><span class="sxs-lookup"><span data-stu-id="51eee-919">Valid operation is:</span></span>
  - <span data-ttu-id="51eee-920">*NX_CRYPTO_HASH_INITIALIZE*</span><span class="sxs-lookup"><span data-stu-id="51eee-920">*NX_CRYPTO_HASH_INITIALIZE*</span></span>
  - <span data-ttu-id="51eee-921">*NX_CRYPTO_HASH_UPDATE*</span><span class="sxs-lookup"><span data-stu-id="51eee-921">*NX_CRYPTO_HASH_UPDATE*</span></span>
  - <span data-ttu-id="51eee-922">*NX_CRYPTO_HASH_CALCULATE*</span><span class="sxs-lookup"><span data-stu-id="51eee-922">*NX_CRYPTO_HASH_CALCULATE*</span></span>
- <span data-ttu-id="51eee-923">**tanıtıcı** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-923">**handle** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="51eee-924">Geçirilen tüm değerler sessizce yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="51eee-924">Any values passed in are silently ignored.</span></span>
- <span data-ttu-id="51eee-925">**yöntemi** Geçerli MD5 şifreleme yöntemine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-925">**method** Pointer to the valid MD5 crypto method.</span></span> <span data-ttu-id="51eee-926">Burada kullanılan şifreleme yöntemi _ *nx_crypto_method_md5_init ()* içinde kullanılan aynı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-926">The crypto method used here must be the same used in the _ *nx_crypto_method_md5_init().*</span></span>
- <span data-ttu-id="51eee-927">**input_data** Girdi metin verileri içeren bir arabelleğe işaret eder.</span><span class="sxs-lookup"><span data-stu-id="51eee-927">**input_data** Points to a buffer containing input text data.</span></span> <span data-ttu-id="51eee-928">Giriş arabelleğinde kısıtlama yoktur.</span><span class="sxs-lookup"><span data-stu-id="51eee-928">There are not restrictions on input buffer.</span></span>
- <span data-ttu-id="51eee-929">**input_data_size** Giriş verilerinin bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-929">**input_data_size** Size of the input data, in bytes.</span></span>
- <span data-ttu-id="51eee-930">**iv_ptr** Bu alan MD5 için kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-930">**iv_ptr** This field is not used for MD5.</span></span>
- <span data-ttu-id="51eee-931">**iv_size** Bu alan MD5 için kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-931">**iv_size** This field is not used for MD5.</span></span>
- <span data-ttu-id="51eee-932">**output_buffer** Oluşturulan MD5 karması için bellek alanına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-932">**output_buffer** Pointer to the memory area for the generated MD5 hash.</span></span>
- <span data-ttu-id="51eee-933">**output_buffer_size** Çıkış arabelleğinin bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-933">**output_buffer_size** Size of the output buffer in bytes.</span></span> <span data-ttu-id="51eee-934">MD5 için arabellek boyutu 16 bayt olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-934">For MD5 the buffer size must be 16 bytes.</span></span>
- <span data-ttu-id="51eee-935">**crypto_metadata** *_Nx_crypto_method_md5_init ()* IÇINDE kullanılan MD5 denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-935">**crypto_metadata** Pointer to the MD5 control block used in *_nx_crypto_method_md5_init()*.</span></span>
- <span data-ttu-id="51eee-936">**crypto_metadata_size** Crypto_metadata alanının bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-936">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="51eee-937">MD5 için meta veri boyutu *sizeof (NX_CRYPTO_MD5)* olmalıdır</span><span class="sxs-lookup"><span data-stu-id="51eee-937">For MD5, the metadata size must *sizeof(NX_CRYPTO_MD5)*</span></span>
- <span data-ttu-id="51eee-938">**packet_ptr** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-938">**packet_ptr** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="51eee-939">Geçirilen tüm değerler sessizce yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="51eee-939">Any values passed in are silently ignored.</span></span>
- <span data-ttu-id="51eee-940">**nx_crypto_hw_process_callback** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-940">**nx_crypto_hw_process_callback** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="51eee-941">Geçirilen tüm değerler sessizce yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="51eee-941">Any values passed in are silently ignored.</span></span>

### <a name="return-values"></a><span data-ttu-id="51eee-942">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="51eee-942">Return Values</span></span>

- <span data-ttu-id="51eee-943">**NX_CRYPTO_SUCCESS** (0x00), MD5 işlemini başarıyla yürütüldü.</span><span class="sxs-lookup"><span data-stu-id="51eee-943">**NX_CRYPTO_SUCCESS** (0x00) Successfully executed the MD5 operation.</span></span>
- <span data-ttu-id="51eee-944">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-944">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="51eee-945">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi veya uzunluğu geçersiz.</span><span class="sxs-lookup"><span data-stu-id="51eee-945">**NX_PTR_ERROR** (0x07) Invalid input pointer or invalid length.</span></span>
- <span data-ttu-id="51eee-946">**NX_CRYPTO_INVALID_ALGORITHM** (0x20004) geçersiz MD5 algoritması belirtildi.</span><span class="sxs-lookup"><span data-stu-id="51eee-946">**NX_CRYPTO_INVALID_ALGORITHM** (0x20004) Invalid MD5 algorithm being specified.</span></span>
- <span data-ttu-id="51eee-947">**NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) geçersiz çıkış arabelleği boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-947">**NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) Invalid output buffer size.</span></span>

## <a name="_nx_crypto_method_md5_cleanup"></a><span data-ttu-id="51eee-948">_nx_crypto_method_md5_cleanup</span><span class="sxs-lookup"><span data-stu-id="51eee-948">_nx_crypto_method_md5_cleanup</span></span>

<span data-ttu-id="51eee-949">MD5 denetim bloğunu temizleyin.</span><span class="sxs-lookup"><span data-stu-id="51eee-949">Clean up the MD5 control block.</span></span>

### <a name="prototype"></a><span data-ttu-id="51eee-950">Prototype</span><span class="sxs-lookup"><span data-stu-id="51eee-950">Prototype</span></span>

```c
UINT _nx_crypto_method_md5_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a><span data-ttu-id="51eee-951">Açıklama</span><span class="sxs-lookup"><span data-stu-id="51eee-951">Description</span></span>

<span data-ttu-id="51eee-952">Uygulama, MD5 denetim bloğunu, bu MD5 oturumunun artık gerekli olmadığını belirledikten sonra temizlemek için bu işlevi çağırır.</span><span class="sxs-lookup"><span data-stu-id="51eee-952">Application calls this function to clean up the MD5 control block after it determines this MD5 session is no longer needed.</span></span>

### <a name="parameters"></a><span data-ttu-id="51eee-953">Parametreler</span><span class="sxs-lookup"><span data-stu-id="51eee-953">Parameters</span></span>

- <span data-ttu-id="51eee-954">**crypto_metadata** *_Nx_crypto_method_md5_init ()* IÇINDE kullanılan MD5 denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-954">**crypto_metadata** Pointer to the MD5 control block used in *_nx_crypto_method_md5_init()*.</span></span>

### <a name="return-values"></a><span data-ttu-id="51eee-955">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="51eee-955">Return Values</span></span>

- <span data-ttu-id="51eee-956">**NX_CRYPTO_SUCCESS** (0x00) MD5 oturumu başarıyla temizlendi.</span><span class="sxs-lookup"><span data-stu-id="51eee-956">**NX_CRYPTO_SUCCESS** (0x00) Successfully cleaned up the MD5 session.</span></span>
- <span data-ttu-id="51eee-957">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-957">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>

## <a name="_nx_crypto_method_sha1_init"></a><span data-ttu-id="51eee-958">_nx_crypto_method_sha1_init</span><span class="sxs-lookup"><span data-stu-id="51eee-958">_nx_crypto_method_sha1_init</span></span>

<span data-ttu-id="51eee-959">SHA1 şifreleme denetim bloğunu başlatır</span><span class="sxs-lookup"><span data-stu-id="51eee-959">Initializes the SHA1 crypto control block</span></span>

### <a name="prototype"></a><span data-ttu-id="51eee-960">Prototype</span><span class="sxs-lookup"><span data-stu-id="51eee-960">Prototype</span></span>

```c
UINT _nx_crypto_method_sha1_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size);
```

### <a name="description"></a><span data-ttu-id="51eee-961">Açıklama</span><span class="sxs-lookup"><span data-stu-id="51eee-961">Description</span></span>

<span data-ttu-id="51eee-962">Bu işlev, SHA1 denetim bloğunu verilen anahtar dizesiyle başlatır.</span><span class="sxs-lookup"><span data-stu-id="51eee-962">This function initializes the SHA1 control block with the given key string.</span></span> <span data-ttu-id="51eee-963">SHA1 denetim bloğu başlatıldıktan sonra, sonraki SHA1 işlemi aynı denetim bloğunu kullanıyor olacaktır.</span><span class="sxs-lookup"><span data-stu-id="51eee-963">Once the SHA1 control block is initialized, subsequent SHA1 operation shall be using the same control block.</span></span>

<span data-ttu-id="51eee-964">Uygulama birden çok SHA1 denetim bloğu oluşturabilir, her biri bir oturumu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="51eee-964">Application may create multiple SHA1 control blocks, each represents a session.</span></span> <span data-ttu-id="51eee-965">SHA1 denetim bloğunu başlatmak yeni bir karma hesaplama oturumu başlatır.</span><span class="sxs-lookup"><span data-stu-id="51eee-965">Initializing the SHA1 control block starts a new hash computation session.</span></span> <span data-ttu-id="51eee-966">SHA1 denetim bloğunu yeniden başlatmak, geçerli oturumu ve yıldızları yeni bir kez terk.</span><span class="sxs-lookup"><span data-stu-id="51eee-966">Re-initializing the SHA1 control block abandons the current session and stars a new one.</span></span>

### <a name="parameters"></a><span data-ttu-id="51eee-967">Parametreler</span><span class="sxs-lookup"><span data-stu-id="51eee-967">Parameters</span></span>

- <span data-ttu-id="51eee-968">**yöntemi** Geçerli bir SHA1 şifreleme yöntemi denetim bloğuna işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-968">**method** Pointer to a valid SHA1 crypto method control block.</span></span> <span data-ttu-id="51eee-969">Aşağıdaki önceden tanımlanmış şifreleme yöntemleri kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="51eee-969">The following pre-defined crypto methods are available:</span></span>
  - <span data-ttu-id="51eee-970">*crypto_method_sha1*</span><span class="sxs-lookup"><span data-stu-id="51eee-970">*crypto_method_sha1*</span></span>
- <span data-ttu-id="51eee-971">**anahtar** Bu alan SHA1 için kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-971">**key** This field is not used for SHA1.</span></span>
- <span data-ttu-id="51eee-972">**key_size_in_bits** Bu alan SHA1 için kullanılmaz</span><span class="sxs-lookup"><span data-stu-id="51eee-972">**key_size_in_bits** This field is not used for SHA1</span></span>
- <span data-ttu-id="51eee-973">**tanıtıcı** Bu hizmet, çağırana bir tanıtıcı döndürür.</span><span class="sxs-lookup"><span data-stu-id="51eee-973">**handle** This service returns a handle to the caller.</span></span> <span data-ttu-id="51eee-974">Tanıtıcı uygulamaya bağımlıdır ve bu uygulamada kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="51eee-974">The handle is implementation-dependent and is not being used in this implementation.</span></span> <span data-ttu-id="51eee-975">Uygulama tanıtıcı için NULL değer geçirecektir.</span><span class="sxs-lookup"><span data-stu-id="51eee-975">Application shall pass NULL for the handle.</span></span>
- <span data-ttu-id="51eee-976">**crypto_metadata** SHA1 denetim bloğu için geçerli bir bellek alanı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="51eee-976">**crypto_metadata** Pointer to a valid memory space for the SHA1 control block.</span></span> <span data-ttu-id="51eee-977">Bellek alanının başlangıç adresi 4 bayt hizalı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-977">The starting address of the memory space must be 4-byte aligned.</span></span>
- <span data-ttu-id="51eee-978">**crypto_metadata_size** Crypto_metadata alanının bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-978">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="51eee-979">SHA1 için meta veri boyutu *sizeof olmalıdır (NX_CRYPTO_SHA1)*</span><span class="sxs-lookup"><span data-stu-id="51eee-979">For SHA1, the metadata size must be *sizeof(NX_CRYPTO_SHA1)*</span></span>

### <a name="return-values"></a><span data-ttu-id="51eee-980">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="51eee-980">Return Values</span></span>

- <span data-ttu-id="51eee-981">Anahtar ve anahtar boyutuyla SHA1control bloğunun başarıyla başlatılması **NX_CRYPTO_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="51eee-981">**NX_CRYPTO_SUCCESS** (0x00) Successful initialization of the SHA1control block with the key and key size.</span></span>
- <span data-ttu-id="51eee-982">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-982">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="51eee-983">**NX_PTR_ERROR** (0x07) anahtar için geçersiz işaretçi veya geçersiz crypto_metadata veya crypto_metadata_size ya da crypto_metadata 4 bayt hizalı değil.</span><span class="sxs-lookup"><span data-stu-id="51eee-983">**NX_PTR_ERROR** (0x07) Invalid pointer to the key, or invalid crypto_metadata or crypto_metadata_size, or crypto_metadata is not 4-byte aligned.</span></span>

## <a name="_nx_crypto_method_sha1_operation"></a><span data-ttu-id="51eee-984">_nx_crypto_method_sha1_operation</span><span class="sxs-lookup"><span data-stu-id="51eee-984">_nx_crypto_method_sha1_operation</span></span>

<span data-ttu-id="51eee-985">SHA1 karma işlemi gerçekleştir</span><span class="sxs-lookup"><span data-stu-id="51eee-985">Perform SHA1 hash operation</span></span>

### <a name="prototype"></a><span data-ttu-id="51eee-986">Prototype</span><span class="sxs-lookup"><span data-stu-id="51eee-986">Prototype</span></span>

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

### <a name="description"></a><span data-ttu-id="51eee-987">Açıklama</span><span class="sxs-lookup"><span data-stu-id="51eee-987">Description</span></span>

<span data-ttu-id="51eee-988">Bu işlev, SHA1 karma işlemini gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="51eee-988">This function performs SHA1 hash operation.</span></span> <span data-ttu-id="51eee-989">SHA1 denetim bloğunun _ *nx_crypto_method_sha1_init ()* ile başlatılmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="51eee-989">The SHA1 control block must have been initialized with _ *nx_crypto_method_sha1_init()*.</span></span> <span data-ttu-id="51eee-990">Gerçekleştirilecek SHA1 algoritması, *Yöntem* denetim bloğunda belirtilen algoritmayı temel alır.</span><span class="sxs-lookup"><span data-stu-id="51eee-990">The SHA1 algorithm to be performed is based on the algorithm specified in the *method* control block.</span></span>

<span data-ttu-id="51eee-991">Son *NX_CRYPTO_HASH_CALCULATE* işlemi için, çıkış arabelleği boyutu 20 bayt olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-991">For the final *NX_CRYPTO_HASH_CALCULATE* operation, the output buffer size must be 20 bytes.</span></span>

### <a name="parameters"></a><span data-ttu-id="51eee-992">Parametreler</span><span class="sxs-lookup"><span data-stu-id="51eee-992">Parameters</span></span>

- <span data-ttu-id="51eee-993">**op** Gerçekleştirilecek işlemin türü.</span><span class="sxs-lookup"><span data-stu-id="51eee-993">**op** Type of operation to perform.</span></span> <span data-ttu-id="51eee-994">Geçerli işlem:</span><span class="sxs-lookup"><span data-stu-id="51eee-994">Valid operation is:</span></span>
  - <span data-ttu-id="51eee-995">*NX_CRYPTO_HASH_INITIALIZE*</span><span class="sxs-lookup"><span data-stu-id="51eee-995">*NX_CRYPTO_HASH_INITIALIZE*</span></span>
  - <span data-ttu-id="51eee-996">*NX_CRYPTO_HASH_UPDATE*</span><span class="sxs-lookup"><span data-stu-id="51eee-996">*NX_CRYPTO_HASH_UPDATE*</span></span>
  - <span data-ttu-id="51eee-997">*NX_CRYPTO_HASH_CALCULATE*</span><span class="sxs-lookup"><span data-stu-id="51eee-997">*NX_CRYPTO_HASH_CALCULATE*</span></span>
- <span data-ttu-id="51eee-998">**tanıtıcı** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-998">**handle** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="51eee-999">Geçirilen tüm değerler sessizce yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="51eee-999">Any values passed in are silently ignored.</span></span>
- <span data-ttu-id="51eee-1000">**yöntemi** Geçerli SHA1 şifreleme yöntemine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-1000">**method** Pointer to the valid SHA1 crypto method.</span></span> <span data-ttu-id="51eee-1001">Burada kullanılan şifreleme yöntemi, *nx_crypto_method_sha1_init ()* içinde kullanılan aynı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-1001">The crypto method used here must be the same used in the *nx_crypto_method_sha1_init().*</span></span>
- <span data-ttu-id="51eee-1002">**input_data** Girdi metin verileri içeren bir arabelleğe işaret eder.</span><span class="sxs-lookup"><span data-stu-id="51eee-1002">**input_data** Points to a buffer containing input text data.</span></span> <span data-ttu-id="51eee-1003">Giriş arabelleğinde kısıtlama yoktur.</span><span class="sxs-lookup"><span data-stu-id="51eee-1003">There are not restrictions on input buffer.</span></span>
- <span data-ttu-id="51eee-1004">**input_data_size** Giriş verilerinin bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-1004">**input_data_size** Size of the input data, in bytes.</span></span>
- <span data-ttu-id="51eee-1005">**iv_ptr** Bu alan SHA1 için kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-1005">**iv_ptr** This field is not used for SHA1.</span></span>
- <span data-ttu-id="51eee-1006">**iv_size** Bu alan SHA1 için kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-1006">**iv_size** This field is not used for SHA1.</span></span>
- <span data-ttu-id="51eee-1007">**output_buffer** Oluşturulan SHA1 karması için bellek alanına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-1007">**output_buffer** Pointer to the memory area for the generated SHA1 hash.</span></span>
- <span data-ttu-id="51eee-1008">**output_buffer_size** Çıkış arabelleğinin bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-1008">**output_buffer_size** Size of the output buffer in bytes.</span></span> <span data-ttu-id="51eee-1009">SHA1 için arabellek boyutu 20 bayt olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-1009">For SHA1 the buffer size must be 20 bytes.</span></span>
- <span data-ttu-id="51eee-1010">**crypto_metadata** *_Nx_crypto_method_sha1_init ()* IÇINDE kullanılan SHA1 denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-1010">**crypto_metadata** Pointer to the SHA1 control block used in *_nx_crypto_method_sha1_init()*.</span></span>
- <span data-ttu-id="51eee-1011">**crypto_metadata_size** Crypto_metadata alanının bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-1011">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="51eee-1012">SHA1 için meta veri boyutu *sizeof (NX_CRYPTO_SHA1)* olmalıdır</span><span class="sxs-lookup"><span data-stu-id="51eee-1012">For SHA1, the metadata size must *sizeof(NX_CRYPTO_SHA1)*</span></span>
- <span data-ttu-id="51eee-1013">**packet_ptr** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-1013">**packet_ptr** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="51eee-1014">Geçirilen tüm değerler sessizce yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="51eee-1014">Any values passed in are silently ignored.</span></span>
- <span data-ttu-id="51eee-1015">**nx_crypto_hw_process_callback** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-1015">**nx_crypto_hw_process_callback** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="51eee-1016">Geçirilen tüm değerler sessizce yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="51eee-1016">Any values passed in are silently ignored.</span></span>

### <a name="return-values"></a><span data-ttu-id="51eee-1017">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="51eee-1017">Return Values</span></span>

- <span data-ttu-id="51eee-1018">**NX_CRYPTO_SUCCESS** (0x00), SHA1 işlemini başarıyla yürütüldü.</span><span class="sxs-lookup"><span data-stu-id="51eee-1018">**NX_CRYPTO_SUCCESS** (0x00) Successfully executed the SHA1 operation.</span></span>
- <span data-ttu-id="51eee-1019">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-1019">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="51eee-1020">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi veya uzunluğu geçersiz.</span><span class="sxs-lookup"><span data-stu-id="51eee-1020">**NX_PTR_ERROR** (0x07) Invalid input pointer or invalid length.</span></span>
- <span data-ttu-id="51eee-1021">**NX_CRYPTO_INVALID_ALGORITHM** (0x20004) geçersiz SHA1 algoritması belirtildi.</span><span class="sxs-lookup"><span data-stu-id="51eee-1021">**NX_CRYPTO_INVALID_ALGORITHM** (0x20004) Invalid SHA1 algorithm being specified.</span></span>
- <span data-ttu-id="51eee-1022">**NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) geçersiz çıkış arabelleği boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-1022">**NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) Invalid output buffer size.</span></span>

### <a name="example"></a><span data-ttu-id="51eee-1023">Örnek</span><span class="sxs-lookup"><span data-stu-id="51eee-1023">Example</span></span>

## <a name="_nx_crypto_method_sha1_cleanup"></a><span data-ttu-id="51eee-1024">_nx_crypto_method_sha1_cleanup</span><span class="sxs-lookup"><span data-stu-id="51eee-1024">_nx_crypto_method_sha1_cleanup</span></span>

<span data-ttu-id="51eee-1025">SHA1 denetim bloğunu temizleyin.</span><span class="sxs-lookup"><span data-stu-id="51eee-1025">Clean up the SHA1 control block.</span></span>

### <a name="prototype"></a><span data-ttu-id="51eee-1026">Prototype</span><span class="sxs-lookup"><span data-stu-id="51eee-1026">Prototype</span></span>

```c
UINT _nx_crypto_method_sha1_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a><span data-ttu-id="51eee-1027">Açıklama</span><span class="sxs-lookup"><span data-stu-id="51eee-1027">Description</span></span>

<span data-ttu-id="51eee-1028">Uygulama, bu SHA1 oturumunun artık gerekli olmadığını belirlediğinde SHA1 denetim bloğunu temizlemek için bu işlevi çağırır.</span><span class="sxs-lookup"><span data-stu-id="51eee-1028">Application calls this function to clean up the SHA1 control block after it determines this SHA1 session is no longer needed.</span></span>

### <a name="parameters"></a><span data-ttu-id="51eee-1029">Parametreler</span><span class="sxs-lookup"><span data-stu-id="51eee-1029">Parameters</span></span>

- <span data-ttu-id="51eee-1030">**crypto_metadata** *_Nx_crypto_method_sha1_init ()* IÇINDE kullanılan SHA1 denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-1030">**crypto_metadata** Pointer to the SHA1 control block used in *_nx_crypto_method_sha1_init()*.</span></span>

### <a name="return-values"></a><span data-ttu-id="51eee-1031">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="51eee-1031">Return Values</span></span>

- <span data-ttu-id="51eee-1032">**NX_CRYPTO_SUCCESS** (0x00), SHA1 oturumunun başarıyla temizlendi.</span><span class="sxs-lookup"><span data-stu-id="51eee-1032">**NX_CRYPTO_SUCCESS** (0x00) Successfully cleaned up the SHA1 session.</span></span>
- <span data-ttu-id="51eee-1033">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-1033">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>

## <a name="_nx_crypto_method_sha256_init"></a><span data-ttu-id="51eee-1034">_nx_crypto_method_sha256_init</span><span class="sxs-lookup"><span data-stu-id="51eee-1034">_nx_crypto_method_sha256_init</span></span>

<span data-ttu-id="51eee-1035">SHA256 şifre denetim bloğunu başlatır</span><span class="sxs-lookup"><span data-stu-id="51eee-1035">Initializes the SHA256 crypto control block</span></span>

### <a name="prototype"></a><span data-ttu-id="51eee-1036">Prototype</span><span class="sxs-lookup"><span data-stu-id="51eee-1036">Prototype</span></span>

```c
UINT _nx_crypto_method_sha256_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size)
```

### <a name="description"></a><span data-ttu-id="51eee-1037">Açıklama</span><span class="sxs-lookup"><span data-stu-id="51eee-1037">Description</span></span>

<span data-ttu-id="51eee-1038">Bu işlev, SHA256 denetim bloğunu verilen anahtar dizesiyle başlatır.</span><span class="sxs-lookup"><span data-stu-id="51eee-1038">This function initializes the SHA256 control block with the given key string.</span></span> <span data-ttu-id="51eee-1039">SHA256 denetim bloğu başlatıldıktan sonra, sonraki SHA256 işlemi aynı denetim bloğunu kullanıyor olacaktır.</span><span class="sxs-lookup"><span data-stu-id="51eee-1039">Once the SHA256 control block is initialized, subsequent SHA256 operation shall be using the same control block.</span></span>

<span data-ttu-id="51eee-1040">Uygulama birden çok SHA256 denetim bloğu oluşturabilir, her biri bir oturumu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="51eee-1040">Application may create multiple SHA256 control blocks, each represents a session.</span></span> <span data-ttu-id="51eee-1041">SHA256 denetim bloğunu başlatmak yeni bir karma hesaplama oturumu başlatır.</span><span class="sxs-lookup"><span data-stu-id="51eee-1041">Initializing the SHA256 control block starts a new hash computation session.</span></span> <span data-ttu-id="51eee-1042">SHA256 denetim bloğunu yeniden başlatmak geçerli oturumu ve yıldızları yeni bir kez terk edin.</span><span class="sxs-lookup"><span data-stu-id="51eee-1042">Re-initializing the SHA256 control block abandons the current session and stars a new one.</span></span>

### <a name="parameters"></a><span data-ttu-id="51eee-1043">Parametreler</span><span class="sxs-lookup"><span data-stu-id="51eee-1043">Parameters</span></span>

- <span data-ttu-id="51eee-1044">**yöntemi** Geçerli bir SHA256 şifreleme yöntemi denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-1044">**method** Pointer to a valid SHA256 crypto method control block.</span></span> <span data-ttu-id="51eee-1045">Aşağıdaki önceden tanımlanmış şifreleme yöntemleri kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="51eee-1045">The following pre-defined crypto methods are available:</span></span>
  - <span data-ttu-id="51eee-1046">*crypto_method_sha256*</span><span class="sxs-lookup"><span data-stu-id="51eee-1046">*crypto_method_sha256*</span></span>
  - <span data-ttu-id="51eee-1047">*crypto_method_sha224*</span><span class="sxs-lookup"><span data-stu-id="51eee-1047">*crypto_method_sha224*</span></span>
- <span data-ttu-id="51eee-1048">**anahtar** Bu alan SHA256 için kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-1048">**key** This field is not used for SHA256.</span></span>
- <span data-ttu-id="51eee-1049">**key_size_in_bits** Bu alan SHA256 için kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="51eee-1049">**key_size_in_bits** This field is not used for SHA256</span></span>
- <span data-ttu-id="51eee-1050">**tanıtıcı** Bu hizmet, çağırana bir tanıtıcı döndürür.</span><span class="sxs-lookup"><span data-stu-id="51eee-1050">**handle** This service returns a handle to the caller.</span></span> <span data-ttu-id="51eee-1051">Tanıtıcı uygulamaya bağımlıdır ve bu uygulamada kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="51eee-1051">The handle is implementation-dependent and is not being used in this implementation.</span></span> <span data-ttu-id="51eee-1052">Uygulama tanıtıcı için NULL değer geçirecektir.</span><span class="sxs-lookup"><span data-stu-id="51eee-1052">Application shall pass NULL for the handle.</span></span>
- <span data-ttu-id="51eee-1053">**crypto_metadata** SHA256 denetim bloğu için geçerli bir bellek alanı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="51eee-1053">**crypto_metadata** Pointer to a valid memory space for the SHA256 control block.</span></span> <span data-ttu-id="51eee-1054">Bellek alanının başlangıç adresi 4 bayt hizalı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-1054">The starting address of the memory space must be 4-byte aligned.</span></span>
- <span data-ttu-id="51eee-1055">**crypto_metadata_size** Crypto_metadata alanının bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-1055">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="51eee-1056">SHA256 için meta veri boyutu *sizeof olmalıdır (NX_CRYPTO_SHA256)*</span><span class="sxs-lookup"><span data-stu-id="51eee-1056">For SHA256, the metadata size must be *sizeof(NX_CRYPTO_SHA256)*</span></span>

### <a name="return-values"></a><span data-ttu-id="51eee-1057">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="51eee-1057">Return Values</span></span>

- <span data-ttu-id="51eee-1058">Anahtar ve anahtar boyutuyla SHA256 denetim bloğunun başarılı bir şekilde başlatılması **NX_CRYPTO_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="51eee-1058">**NX_CRYPTO_SUCCESS** (0x00) Successful initialization of the SHA256 control block with the key and key size.</span></span>
- <span data-ttu-id="51eee-1059">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-1059">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="51eee-1060">**NX_PTR_ERROR** (0x07) anahtar için geçersiz işaretçi veya geçersiz crypto_metadata veya crypto_metadata_size ya da crypto_metadata 4 bayt hizalı değil.</span><span class="sxs-lookup"><span data-stu-id="51eee-1060">**NX_PTR_ERROR** (0x07) Invalid pointer to the key, or invalid crypto_metadata or crypto_metadata_size, or crypto_metadata is not 4-byte aligned.</span></span>

## <a name="_nx_crypto_method_sha256_operation"></a><span data-ttu-id="51eee-1061">_nx_crypto_method_sha256_operation</span><span class="sxs-lookup"><span data-stu-id="51eee-1061">_nx_crypto_method_sha256_operation</span></span>

<span data-ttu-id="51eee-1062">SHA256 karma işlemi gerçekleştir</span><span class="sxs-lookup"><span data-stu-id="51eee-1062">Perform SHA256 hash operation</span></span>

### <a name="prototype"></a><span data-ttu-id="51eee-1063">Prototype</span><span class="sxs-lookup"><span data-stu-id="51eee-1063">Prototype</span></span>

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

### <a name="description"></a><span data-ttu-id="51eee-1064">Açıklama</span><span class="sxs-lookup"><span data-stu-id="51eee-1064">Description</span></span>

<span data-ttu-id="51eee-1065">Bu işlev SHA256 karma işlem gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="51eee-1065">This function performs SHA256 hash operation.</span></span> <span data-ttu-id="51eee-1066">SHA256 denetim bloğu _ ***nx_crypto_method_sha256_init ()*** ile başlatılmış olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-1066">The SHA256 control block must have been initialized with _ ***nx_crypto_method_sha256_init()***.</span></span> <span data-ttu-id="51eee-1067">Gerçekleştirilecek SHA256 algoritması, *Yöntem* denetim bloğunda belirtilen algoritmayı temel alır.</span><span class="sxs-lookup"><span data-stu-id="51eee-1067">The SHA256 algorithm to be performed is based on the algorithm specified in the *method* control block.</span></span>

<span data-ttu-id="51eee-1068">Son *NX_CRYPTO_HASH_CALCULATE* işlemi için, çıkış ARABELLEĞI boyutu SHA256 için 32 bayt veya SHA224 için 28 bayt olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-1068">For the final *NX_CRYPTO_HASH_CALCULATE* operation, the output buffer size must be 32 bytes for SHA256, or 28 bytes for SHA224.</span></span>

### <a name="parameters"></a><span data-ttu-id="51eee-1069">Parametreler</span><span class="sxs-lookup"><span data-stu-id="51eee-1069">Parameters</span></span>

- <span data-ttu-id="51eee-1070">**op** Gerçekleştirilecek işlemin türü.</span><span class="sxs-lookup"><span data-stu-id="51eee-1070">**op** Type of operation to perform.</span></span> <span data-ttu-id="51eee-1071">Geçerli işlem:</span><span class="sxs-lookup"><span data-stu-id="51eee-1071">Valid operation is:</span></span>
  - <span data-ttu-id="51eee-1072">*NX_CRYPTO_HASH_INITIALIZE*</span><span class="sxs-lookup"><span data-stu-id="51eee-1072">*NX_CRYPTO_HASH_INITIALIZE*</span></span>
  - <span data-ttu-id="51eee-1073">*NX_CRYPTO_HASH_UPDATE*</span><span class="sxs-lookup"><span data-stu-id="51eee-1073">*NX_CRYPTO_HASH_UPDATE*</span></span>
  - <span data-ttu-id="51eee-1074">*NX_CRYPTO_HASH_CALCULATE*</span><span class="sxs-lookup"><span data-stu-id="51eee-1074">*NX_CRYPTO_HASH_CALCULATE*</span></span>
- <span data-ttu-id="51eee-1075">**tanıtıcı** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-1075">**handle** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="51eee-1076">Geçirilen tüm değerler sessizce yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="51eee-1076">Any values passed in are silently ignored.</span></span>
- <span data-ttu-id="51eee-1077">**yöntemi** Geçerli SHA256 şifre yöntemine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-1077">**method** Pointer to the valid SHA256 crypto method.</span></span> <span data-ttu-id="51eee-1078">Burada kullanılan şifreleme yöntemi _ *nx_crypto_method_sha256_init ()* içinde kullanılan aynı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-1078">The crypto method used here must be the same used in the _ *nx_crypto_method_sha256_init().*</span></span>
- <span data-ttu-id="51eee-1079">**input_data** Girdi metin verileri içeren bir arabelleğe işaret eder.</span><span class="sxs-lookup"><span data-stu-id="51eee-1079">**input_data** Points to a buffer containing input text data.</span></span> <span data-ttu-id="51eee-1080">Giriş arabelleğinde kısıtlama yoktur.</span><span class="sxs-lookup"><span data-stu-id="51eee-1080">There are not restrictions on input buffer.</span></span>
- <span data-ttu-id="51eee-1081">**input_data_size** Giriş verilerinin bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-1081">**input_data_size** Size of the input data, in bytes.</span></span>
- <span data-ttu-id="51eee-1082">**iv_ptr** Bu alan SHA256 için kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-1082">**iv_ptr** This field is not used for SHA256.</span></span>
- <span data-ttu-id="51eee-1083">**iv_size** Bu alan SHA256 için kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-1083">**iv_size** This field is not used for SHA256.</span></span>
- <span data-ttu-id="51eee-1084">**output_buffer** Oluşturulan SHA256 karması için bellek alanına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-1084">**output_buffer** Pointer to the memory area for the generated SHA256 hash.</span></span>
- <span data-ttu-id="51eee-1085">**output_buffer_size** Çıkış arabelleğinin bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-1085">**output_buffer_size** Size of the output buffer in bytes.</span></span> <span data-ttu-id="51eee-1086">SHA256 için arabellek boyutu 32 bayt olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-1086">For SHA256 the buffer size must be 32 bytes.</span></span> <span data-ttu-id="51eee-1087">SHA224 için arabellek boyutu 28 bayt olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-1087">For SHA224 the buffer size must be 28 bytes.</span></span>
- <span data-ttu-id="51eee-1088">**crypto_metadata** *_Nx_crypto_method_sha2_init ()* IÇINDE kullanılan SHA2 denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-1088">**crypto_metadata** Pointer to the SHA2 control block used in *_nx_crypto_method_sha2_init()*.</span></span>
- <span data-ttu-id="51eee-1089">**crypto_metadata_size** Crypto_metadata alanının bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-1089">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="51eee-1090">SHA256 için meta veri boyutu sizeof olmalıdır *(NX_CRYPTO_SHA256)*</span><span class="sxs-lookup"><span data-stu-id="51eee-1090">For SHA256, the metadata size must *sizeof(NX_CRYPTO_SHA256)*</span></span>
- <span data-ttu-id="51eee-1091">**packet_ptr** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-1091">**packet_ptr** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="51eee-1092">Geçirilen tüm değerler sessizce yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="51eee-1092">Any values passed in are silently ignored.</span></span>
- <span data-ttu-id="51eee-1093">**nx_crypto_hw_process_callback** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-1093">**nx_crypto_hw_process_callback** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="51eee-1094">Geçirilen tüm değerler sessizce yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="51eee-1094">Any values passed in are silently ignored.</span></span>

### <a name="return-values"></a><span data-ttu-id="51eee-1095">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="51eee-1095">Return Values</span></span>

- <span data-ttu-id="51eee-1096">**NX_CRYPTO_SUCCESS** (0x00) SHA256 işlemini başarıyla yürütüldü.</span><span class="sxs-lookup"><span data-stu-id="51eee-1096">**NX_CRYPTO_SUCCESS** (0x00) Successfully executed the SHA256 operation.</span></span>
- <span data-ttu-id="51eee-1097">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-1097">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="51eee-1098">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi veya uzunluğu geçersiz.</span><span class="sxs-lookup"><span data-stu-id="51eee-1098">**NX_PTR_ERROR** (0x07) Invalid input pointer or invalid length.</span></span>
- <span data-ttu-id="51eee-1099">**NX_CRYPTO_INVALID_ALGORITHM** (0x20004) geçersiz SHA256 algoritması belirtildi.</span><span class="sxs-lookup"><span data-stu-id="51eee-1099">**NX_CRYPTO_INVALID_ALGORITHM** (0x20004) Invalid SHA256 algorithm being specified.</span></span>
- <span data-ttu-id="51eee-1100">**NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) geçersiz çıkış arabelleği boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-1100">**NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) Invalid output buffer size.</span></span>

## <a name="_nx_crypto_method_sha256_cleanup"></a><span data-ttu-id="51eee-1101">_nx_crypto_method_sha256_cleanup</span><span class="sxs-lookup"><span data-stu-id="51eee-1101">_nx_crypto_method_sha256_cleanup</span></span>

<span data-ttu-id="51eee-1102">SHA256 denetim bloğunu temizleyin.</span><span class="sxs-lookup"><span data-stu-id="51eee-1102">Clean up the SHA256 control block.</span></span>

### <a name="prototype"></a><span data-ttu-id="51eee-1103">Prototype</span><span class="sxs-lookup"><span data-stu-id="51eee-1103">Prototype</span></span>

```c
UINT _nx_crypto_method_sha256_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a><span data-ttu-id="51eee-1104">Açıklama</span><span class="sxs-lookup"><span data-stu-id="51eee-1104">Description</span></span>

<span data-ttu-id="51eee-1105">Uygulama, bu SHA256 oturumunun artık gerekli olmadığını belirledikten sonra SHA256 denetim bloğunu temizlemek için bu işlevi çağırır.</span><span class="sxs-lookup"><span data-stu-id="51eee-1105">Application calls this function to clean up the SHA256 control block after it determines this SHA256 session is no longer needed.</span></span>

### <a name="parameters"></a><span data-ttu-id="51eee-1106">Parametreler</span><span class="sxs-lookup"><span data-stu-id="51eee-1106">Parameters</span></span>

- <span data-ttu-id="51eee-1107">**crypto_metadata** *_Nx_crypto_method_sha256_init ()* IÇINDE kullanılan SHA256 denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-1107">**crypto_metadata** Pointer to the SHA256 control block used in *_nx_crypto_method_sha256_init()*.</span></span>

### <a name="return-values"></a><span data-ttu-id="51eee-1108">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="51eee-1108">Return Values</span></span>

- <span data-ttu-id="51eee-1109">**NX_CRYPTO_SUCCESS** (0x00) SHA256 oturumu başarıyla temizlendi.</span><span class="sxs-lookup"><span data-stu-id="51eee-1109">**NX_CRYPTO_SUCCESS** (0x00) Successfully cleaned up the SHA256 session.</span></span>
- <span data-ttu-id="51eee-1110">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-1110">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>

## <a name="_nx_crypto_method_sha512_init"></a><span data-ttu-id="51eee-1111">_nx_crypto_method_sha512_init</span><span class="sxs-lookup"><span data-stu-id="51eee-1111">_nx_crypto_method_sha512_init</span></span>

<span data-ttu-id="51eee-1112">SHA512 olur şifre denetim bloğunu başlatır</span><span class="sxs-lookup"><span data-stu-id="51eee-1112">Initializes the SHA512 crypto control block</span></span>

### <a name="prototype"></a><span data-ttu-id="51eee-1113">Prototype</span><span class="sxs-lookup"><span data-stu-id="51eee-1113">Prototype</span></span>

```c
UINT _nx_crypto_method_sha512_init(
    struct NX_CRYPTO_METHOD_STRUCT *method,
    UCHAR *key,
    NX_CRYPTO_KEY_SIZE key_size_in_bits,
    VOID **handle,
    VOID *crypto_metadata,
    ULONG crypto_metadata_size);
```

### <a name="description"></a><span data-ttu-id="51eee-1114">Açıklama</span><span class="sxs-lookup"><span data-stu-id="51eee-1114">Description</span></span>

<span data-ttu-id="51eee-1115">Bu işlev, SHA512 olur denetim bloğunu verilen anahtar dizesiyle başlatır.</span><span class="sxs-lookup"><span data-stu-id="51eee-1115">This function initializes the SHA512 control block with the given key string.</span></span> <span data-ttu-id="51eee-1116">SHA512 olur denetim bloğu başlatıldıktan sonra, sonraki SHA512 olur işlemi aynı denetim bloğunu kullanıyor olacaktır.</span><span class="sxs-lookup"><span data-stu-id="51eee-1116">Once the SHA512 control block is initialized, subsequent SHA512 operation shall be using the same control block.</span></span>

<span data-ttu-id="51eee-1117">Uygulama birden çok SHA512 olur denetim bloğu oluşturabilir, her biri bir oturumu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="51eee-1117">Application may create multiple SHA512 control blocks, each represents a session.</span></span> <span data-ttu-id="51eee-1118">SHA512 olur denetim bloğunu başlatmak yeni bir karma hesaplama oturumu başlatır.</span><span class="sxs-lookup"><span data-stu-id="51eee-1118">Initializing the SHA512 control block starts a new hash computation session.</span></span> <span data-ttu-id="51eee-1119">SHA512 olur denetim bloğunu yeniden başlatmak geçerli oturumu ve yıldızları yeni bir kez terk edin.</span><span class="sxs-lookup"><span data-stu-id="51eee-1119">Re-initializing the SHA512 control block abandons the current session and stars a new one.</span></span>

### <a name="parameters"></a><span data-ttu-id="51eee-1120">Parametreler</span><span class="sxs-lookup"><span data-stu-id="51eee-1120">Parameters</span></span>

- <span data-ttu-id="51eee-1121">**yöntemi** Geçerli bir SHA512 olur şifreleme yöntemi denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-1121">**method** Pointer to a valid SHA512 crypto method control block.</span></span> <span data-ttu-id="51eee-1122">Aşağıdaki önceden tanımlanmış şifreleme yöntemleri kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="51eee-1122">The following pre-defined crypto methods are available:</span></span>
  - <span data-ttu-id="51eee-1123">*crypto_method_sha512*</span><span class="sxs-lookup"><span data-stu-id="51eee-1123">*crypto_method_sha512*</span></span>
  - <span data-ttu-id="51eee-1124">*crypto_method_sha384*</span><span class="sxs-lookup"><span data-stu-id="51eee-1124">*crypto_method_sha384*</span></span>
- <span data-ttu-id="51eee-1125">**anahtar** Bu alan SHA512 olur için kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-1125">**key** This field is not used for SHA512.</span></span>
- <span data-ttu-id="51eee-1126">**key_size_in_bits** Bu alan SHA512 olur için kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="51eee-1126">**key_size_in_bits** This field is not used for SHA512</span></span>
- <span data-ttu-id="51eee-1127">**tanıtıcı** Bu hizmet, çağırana bir tanıtıcı döndürür.</span><span class="sxs-lookup"><span data-stu-id="51eee-1127">**handle** This service returns a handle to the caller.</span></span> <span data-ttu-id="51eee-1128">Tanıtıcı uygulamaya bağımlıdır ve bu uygulamada kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="51eee-1128">The handle is implementation-dependent and is not being used in this implementation.</span></span> <span data-ttu-id="51eee-1129">Uygulama tanıtıcı için NULL değer geçirecektir.</span><span class="sxs-lookup"><span data-stu-id="51eee-1129">Application shall pass NULL for the handle.</span></span>
- <span data-ttu-id="51eee-1130">**crypto_metadata** SHA512 olur denetim bloğu için geçerli bir bellek alanı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="51eee-1130">**crypto_metadata** Pointer to a valid memory space for the SHA512 control block.</span></span> <span data-ttu-id="51eee-1131">Bellek alanının başlangıç adresi 4 bayt hizalı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-1131">The starting address of the memory space must be 4-byte aligned.</span></span>
- <span data-ttu-id="51eee-1132">**crypto_metadata_size** Crypto_metadata alanının bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-1132">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="51eee-1133">SHA512 olur için meta veri boyutu *sizeof olmalıdır (NX_CRYPTO_SHA512)*</span><span class="sxs-lookup"><span data-stu-id="51eee-1133">For SHA512, the metadata size must be *sizeof(NX_CRYPTO_SHA512)*</span></span>

### <a name="return-values"></a><span data-ttu-id="51eee-1134">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="51eee-1134">Return Values</span></span>

- <span data-ttu-id="51eee-1135">Anahtar ve anahtar boyutuyla SHA512 olur denetim bloğunun başarılı bir şekilde başlatılması **NX_CRYPTO_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="51eee-1135">**NX_CRYPTO_SUCCESS** (0x00) Successful initialization of the SHA512 control block with the key and key size.</span></span>
- <span data-ttu-id="51eee-1136">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-1136">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="51eee-1137">**NX_PTR_ERROR** (0x07) anahtar için geçersiz işaretçi veya geçersiz crypto_metadata veya crypto_metadata_size ya da crypto_metadata 4 bayt hizalı değil.</span><span class="sxs-lookup"><span data-stu-id="51eee-1137">**NX_PTR_ERROR** (0x07) Invalid pointer to the key, or invalid crypto_metadata or crypto_metadata_size, or crypto_metadata is not 4-byte aligned.</span></span>

## <a name="_nx_crypto_method_sha512_operation"></a><span data-ttu-id="51eee-1138">_nx_crypto_method_sha512_operation</span><span class="sxs-lookup"><span data-stu-id="51eee-1138">_nx_crypto_method_sha512_operation</span></span>

<span data-ttu-id="51eee-1139">SHA512 olur karma işlemi gerçekleştir</span><span class="sxs-lookup"><span data-stu-id="51eee-1139">Perform SHA512 hash operation</span></span>

### <a name="prototype"></a><span data-ttu-id="51eee-1140">Prototype</span><span class="sxs-lookup"><span data-stu-id="51eee-1140">Prototype</span></span>

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

### <a name="description"></a><span data-ttu-id="51eee-1141">Açıklama</span><span class="sxs-lookup"><span data-stu-id="51eee-1141">Description</span></span>

<span data-ttu-id="51eee-1142">Bu işlev SHA512 olur karma işlem gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="51eee-1142">This function performs SHA512 hash operation.</span></span> <span data-ttu-id="51eee-1143">SHA512 olur denetim bloğu _ *nx_crypto_method_sha512_init ()* ile başlatılmış olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-1143">The SHA512 control block must have been initialized with _ *nx_crypto_method_sha512_init()*.</span></span> <span data-ttu-id="51eee-1144">Gerçekleştirilecek SHA512 olur algoritması, *Yöntem* denetim bloğunda belirtilen algoritmayı temel alır.</span><span class="sxs-lookup"><span data-stu-id="51eee-1144">The SHA512 algorithm to be performed is based on the algorithm specified in the *method* control block.</span></span>

<span data-ttu-id="51eee-1145">Son *NX_CRYPTO_HASH_CALCULATE* işlemi için, çıkış ARABELLEĞI boyutu sha512 olur için 64 bayt veya SHA384 için 48 bayt olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-1145">For the final *NX_CRYPTO_HASH_CALCULATE* operation, the output buffer size must be 64 bytes for SHA512, or 48 bytes for SHA384.</span></span>

### <a name="parameters"></a><span data-ttu-id="51eee-1146">Parametreler</span><span class="sxs-lookup"><span data-stu-id="51eee-1146">Parameters</span></span>

- <span data-ttu-id="51eee-1147">**op** Gerçekleştirilecek işlemin türü.</span><span class="sxs-lookup"><span data-stu-id="51eee-1147">**op** Type of operation to perform.</span></span> <span data-ttu-id="51eee-1148">Geçerli işlem:</span><span class="sxs-lookup"><span data-stu-id="51eee-1148">Valid operation is:</span></span>
  - <span data-ttu-id="51eee-1149">*NX_CRYPTO_HASH_INITIALIZE*</span><span class="sxs-lookup"><span data-stu-id="51eee-1149">*NX_CRYPTO_HASH_INITIALIZE*</span></span>
  - <span data-ttu-id="51eee-1150">*NX_CRYPTO_HASH_UPDATE*</span><span class="sxs-lookup"><span data-stu-id="51eee-1150">*NX_CRYPTO_HASH_UPDATE*</span></span>
  - <span data-ttu-id="51eee-1151">*NX_CRYPTO_HASH_CALCULATE*</span><span class="sxs-lookup"><span data-stu-id="51eee-1151">*NX_CRYPTO_HASH_CALCULATE*</span></span>
- <span data-ttu-id="51eee-1152">**tanıtıcı** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-1152">**handle** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="51eee-1153">Geçirilen tüm değerler sessizce yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="51eee-1153">Any values passed in are silently ignored.</span></span>
- <span data-ttu-id="51eee-1154">**yöntemi** Geçerli SHA512 olur şifre yöntemine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-1154">**method** Pointer to the valid SHA512 crypto method.</span></span> <span data-ttu-id="51eee-1155">Burada kullanılan şifreleme yöntemi _ *nx_crypto_method_sha512_init ()* içinde kullanılan aynı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-1155">The crypto method used here must be the same used in the _ *nx_crypto_method_sha512_init().*</span></span>
- <span data-ttu-id="51eee-1156">**input_data** Girdi metin verileri içeren bir arabelleğe işaret eder.</span><span class="sxs-lookup"><span data-stu-id="51eee-1156">**input_data** Points to a buffer containing input text data.</span></span> <span data-ttu-id="51eee-1157">Giriş arabelleğinde kısıtlama yoktur.</span><span class="sxs-lookup"><span data-stu-id="51eee-1157">There are not restrictions on input buffer.</span></span>
- <span data-ttu-id="51eee-1158">**input_data_size** Giriş verilerinin bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-1158">**input_data_size** Size of the input data, in bytes.</span></span>
- <span data-ttu-id="51eee-1159">**iv_ptr** Bu alan SHA512 olur için kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-1159">**iv_ptr** This field is not used for SHA512.</span></span>
- <span data-ttu-id="51eee-1160">**iv_size** Bu alan SHA512 olur için kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-1160">**iv_size** This field is not used for SHA512.</span></span>
- <span data-ttu-id="51eee-1161">**output_buffer** Oluşturulan SHA512 olur karması için bellek alanına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-1161">**output_buffer** Pointer to the memory area for the generated SHA512 hash.</span></span>
- <span data-ttu-id="51eee-1162">**output_buffer_size** Çıkış arabelleğinin bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-1162">**output_buffer_size** Size of the output buffer in bytes.</span></span> <span data-ttu-id="51eee-1163">SHA512 olur için arabellek boyutu 64 bayt olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-1163">For SHA512 the buffer size must be 64 bytes.</span></span> <span data-ttu-id="51eee-1164">SHA384 için arabellek boyutu 48 bayt olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51eee-1164">For SHA384 the buffer size must be 48 bytes.</span></span>
- <span data-ttu-id="51eee-1165">**crypto_metadata** *_Nx_crypto_method_sha512_init ()* IÇINDE kullanılan SHA512 olur denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-1165">**crypto_metadata** Pointer to the SHA512 control block used in *_nx_crypto_method_sha512_init()*.</span></span>
- <span data-ttu-id="51eee-1166">**crypto_metadata_size** Crypto_metadata alanının bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-1166">**crypto_metadata_size** Size, in bytes, of the crypto_metadata area.</span></span> <span data-ttu-id="51eee-1167">SHA512 olur için meta veri boyutu sizeof olmalıdır *(NX_CRYPTO_SHA512)*</span><span class="sxs-lookup"><span data-stu-id="51eee-1167">For SHA512, the metadata size must *sizeof(NX_CRYPTO_SHA512)*</span></span>
- <span data-ttu-id="51eee-1168">**packet_ptr** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-1168">**packet_ptr** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="51eee-1169">Geçirilen tüm değerler sessizce yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="51eee-1169">Any values passed in are silently ignored.</span></span>
- <span data-ttu-id="51eee-1170">**nx_crypto_hw_process_callback** Bu alan, NetX şifreleme kitaplığının yazılım uygulamasında kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-1170">**nx_crypto_hw_process_callback** This field is not used in the software implementation of NetX Crypto library.</span></span> <span data-ttu-id="51eee-1171">Geçirilen tüm değerler sessizce yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="51eee-1171">Any values passed in are silently ignored.</span></span>

### <a name="return-values"></a><span data-ttu-id="51eee-1172">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="51eee-1172">Return Values</span></span>

- <span data-ttu-id="51eee-1173">**NX_CRYPTO_SUCCESS** (0x00) SHA512 olur işlemini başarıyla yürütüldü.</span><span class="sxs-lookup"><span data-stu-id="51eee-1173">**NX_CRYPTO_SUCCESS** (0x00) Successfully executed the SHA512 operation.</span></span>
- <span data-ttu-id="51eee-1174">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-1174">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>
- <span data-ttu-id="51eee-1175">**NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi veya uzunluğu geçersiz.</span><span class="sxs-lookup"><span data-stu-id="51eee-1175">**NX_PTR_ERROR** (0x07) Invalid input pointer or invalid length.</span></span>
- <span data-ttu-id="51eee-1176">**NX_CRYPTO_INVALID_ALGORITHM** (0x20004) geçersiz SHA512 olur algoritması belirtildi.</span><span class="sxs-lookup"><span data-stu-id="51eee-1176">**NX_CRYPTO_INVALID_ALGORITHM** (0x20004) Invalid SHA512 algorithm being specified.</span></span>
- <span data-ttu-id="51eee-1177">**NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) geçersiz çıkış arabelleği boyutu.</span><span class="sxs-lookup"><span data-stu-id="51eee-1177">**NX_CRYPTO_INVALID_BUFFER_SIZE** (0x20005) Invalid output buffer size.</span></span>

## <a name="_nx_crypto_method_sha512_cleanup"></a><span data-ttu-id="51eee-1178">_nx_crypto_method_sha512_cleanup</span><span class="sxs-lookup"><span data-stu-id="51eee-1178">_nx_crypto_method_sha512_cleanup</span></span>

<span data-ttu-id="51eee-1179">SHA512 olur denetim bloğunu temizleyin.</span><span class="sxs-lookup"><span data-stu-id="51eee-1179">Clean up the SHA512 control block.</span></span>

### <a name="prototype"></a><span data-ttu-id="51eee-1180">Prototype</span><span class="sxs-lookup"><span data-stu-id="51eee-1180">Prototype</span></span>

```c
UINT _nx_crypto_method_sha512_cleanup(VOID* crypto_metadata);
```

### <a name="description"></a><span data-ttu-id="51eee-1181">Açıklama</span><span class="sxs-lookup"><span data-stu-id="51eee-1181">Description</span></span>

<span data-ttu-id="51eee-1182">Uygulama, bu SHA512 olur oturumunun artık gerekli olmadığını belirledikten sonra SHA512 olur denetim bloğunu temizlemek için bu işlevi çağırır.</span><span class="sxs-lookup"><span data-stu-id="51eee-1182">Application calls this function to clean up the SHA512 control block after it determines this SHA512 session is no longer needed.</span></span>

### <a name="parameters"></a><span data-ttu-id="51eee-1183">Parametreler</span><span class="sxs-lookup"><span data-stu-id="51eee-1183">Parameters</span></span>

- <span data-ttu-id="51eee-1184">**crypto_metadata** *_Nx_crypto_method_sha512_init ()* IÇINDE kullanılan SHA512 olur denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="51eee-1184">**crypto_metadata** Pointer to the SHA512 control block used in *_nx_crypto_method_sha512_init()*.</span></span>

### <a name="return-values"></a><span data-ttu-id="51eee-1185">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="51eee-1185">Return Values</span></span>

- <span data-ttu-id="51eee-1186">**NX_CRYPTO_SUCCESS** (0x00) SHA512 olur oturumu başarıyla temizlendi.</span><span class="sxs-lookup"><span data-stu-id="51eee-1186">**NX_CRYPTO_SUCCESS** (0x00) Successfully cleaned up the SHA512 session.</span></span>
- <span data-ttu-id="51eee-1187">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) şifre kitaplığı geçersiz bir durumda ve kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="51eee-1187">**NX_CRYPTO_INVALID_LIBRARY** (0x20001) The crypto library is in an invalid state and cannot be used.</span></span>