---
title: USBX konak sınıfları API 'SI
description: Bu bölümde, USBX konak sınıflarının tüm sunulan API 'Leri ele alınmaktadır.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 39f3a71c28dd14e0093f72d1a3b1ff6837c6f1f7
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104828114"
---
# <a name="chapter-2-usbx-host-classes-api"></a><span data-ttu-id="5e16f-103">Bölüm 2: USBX konak sınıfları API 'SI</span><span class="sxs-lookup"><span data-stu-id="5e16f-103">Chapter 2: USBX Host Classes API</span></span>

<span data-ttu-id="5e16f-104">Bu bölümde, USBX konak sınıflarının tüm sunulan API 'Leri ele alınmaktadır.</span><span class="sxs-lookup"><span data-stu-id="5e16f-104">This chapter covers all the exposed APIs of the USBX host classes.</span></span> <span data-ttu-id="5e16f-105">Her sınıf için aşağıdaki API 'Ler ayrıntılı olarak açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="5e16f-105">The following APIs for each class are described in detail.</span></span>

- <span data-ttu-id="5e16f-106">Yazıcı sınıfı</span><span class="sxs-lookup"><span data-stu-id="5e16f-106">Printer class</span></span>
- <span data-ttu-id="5e16f-107">Ses sınıfı</span><span class="sxs-lookup"><span data-stu-id="5e16f-107">Audio class</span></span>
- <span data-ttu-id="5e16f-108">Asix sınıfı</span><span class="sxs-lookup"><span data-stu-id="5e16f-108">Asix class</span></span>
- <span data-ttu-id="5e16f-109">Pima/PTP sınıfı</span><span class="sxs-lookup"><span data-stu-id="5e16f-109">Pima/PTP class</span></span>
- <span data-ttu-id="5e16f-110">Prolific sınıfı</span><span class="sxs-lookup"><span data-stu-id="5e16f-110">Prolific class</span></span>
- <span data-ttu-id="5e16f-111">Genel seri sınıf</span><span class="sxs-lookup"><span data-stu-id="5e16f-111">Generic Serial class</span></span>

## <a name="ux_host_class_printer_read"></a><span data-ttu-id="5e16f-112">ux_host_class_printer_read</span><span class="sxs-lookup"><span data-stu-id="5e16f-112">ux_host_class_printer_read</span></span>

<span data-ttu-id="5e16f-113">Yazıcı arabiriminden okuyun.</span><span class="sxs-lookup"><span data-stu-id="5e16f-113">Read from the printer interface.</span></span>

### <a name="prototype"></a><span data-ttu-id="5e16f-114">Prototype</span><span class="sxs-lookup"><span data-stu-id="5e16f-114">Prototype</span></span>

```C
UINT ux_host_class_printer_read(
    UX_HOST_CLASS_PRINTER *printer,
    UCHAR *data_pointer,
    ULONG requested_length,
    ULONG *actual_length)
```

### <a name="description"></a><span data-ttu-id="5e16f-115">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5e16f-115">Description</span></span>

<span data-ttu-id="5e16f-116">Bu işlev, yazıcı arabiriminden okur.</span><span class="sxs-lookup"><span data-stu-id="5e16f-116">This function reads from the printer interface.</span></span> <span data-ttu-id="5e16f-117">Çağrı engelleniyor ve yalnızca bir hata olduğunda ya da aktarım tamamlandığında döndürülür.</span><span class="sxs-lookup"><span data-stu-id="5e16f-117">The call is blocking and only returns when there is either an error or when the transfer is complete.</span></span> <span data-ttu-id="5e16f-118">Okumaya yalnızca çift yönlü yazıcılarda izin verilir.</span><span class="sxs-lookup"><span data-stu-id="5e16f-118">A read is allowed only on bi-directional printers.</span></span>

### <a name="parameters"></a><span data-ttu-id="5e16f-119">Parametreler</span><span class="sxs-lookup"><span data-stu-id="5e16f-119">Parameters</span></span>

- <span data-ttu-id="5e16f-120">**Yazıcı**: yazıcı sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-120">**printer**: Pointer to the printer class instance.</span></span>
- <span data-ttu-id="5e16f-121">**data_pointer**: veri yükünün arabellek adresine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-121">**data_pointer**: Pointer to the buffer address of the data payload.</span></span>
- <span data-ttu-id="5e16f-122">**requested_length**: alınacak uzunluk.</span><span class="sxs-lookup"><span data-stu-id="5e16f-122">**requested_length**: Length to be received.</span></span>
- <span data-ttu-id="5e16f-123">**actual_length**: Uzunluk gerçekten alındı.</span><span class="sxs-lookup"><span data-stu-id="5e16f-123">**actual_length**: Length actually received.</span></span>

### <a name="return-value"></a><span data-ttu-id="5e16f-124">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="5e16f-124">Return Value</span></span>

- <span data-ttu-id="5e16f-125">**UX_SUCCESS**: (0x00) veri aktarımı tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="5e16f-125">**UX_SUCCESS**:  (0x00) The data transfer was completed.</span></span>
- <span data-ttu-id="5e16f-126">**UX_FUNCTION_NOT_SUPPORTED**: (0x54) Yazıcı çift yönlü olmadığından işlev desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="5e16f-126">**UX_FUNCTION_NOT_SUPPORTED**: (0x54) Function not supported because the printer is not bi-directional.</span></span>
- <span data-ttu-id="5e16f-127">**UX_TRANSFER_TIMEOUT**: (0x5c) aktarım zaman aşımı, okuma tamamlanmadı.</span><span class="sxs-lookup"><span data-stu-id="5e16f-127">**UX_TRANSFER_TIMEOUT**: (0x5c) Transfer timeout, reading incomplete.</span></span>

### <a name="example"></a><span data-ttu-id="5e16f-128">Örnek</span><span class="sxs-lookup"><span data-stu-id="5e16f-128">Example</span></span>

```C
UINT status;

/* The following example illustrates this service. */
status = ux_host_class_printer_read(printer, data_pointer, requested_length, &actual_length);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_printer_write"></a><span data-ttu-id="5e16f-129">ux_host_class_printer_write</span><span class="sxs-lookup"><span data-stu-id="5e16f-129">ux_host_class_printer_write</span></span>

<span data-ttu-id="5e16f-130">Yazıcı arabirimine yazın.</span><span class="sxs-lookup"><span data-stu-id="5e16f-130">Write to the printer interface.</span></span>

### <a name="prototype"></a><span data-ttu-id="5e16f-131">Prototype</span><span class="sxs-lookup"><span data-stu-id="5e16f-131">Prototype</span></span>

```C
UINT ux_host_class_printer_write(
    UX_HOST_CLASS_PRINTER *printer,
    UCHAR *data_pointer,  
    ULONG requested_length,
    ULONG *actual_length)
```

### <a name="description"></a><span data-ttu-id="5e16f-132">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5e16f-132">Description</span></span>

<span data-ttu-id="5e16f-133">Bu işlev, yazıcı arabirimine yazar.</span><span class="sxs-lookup"><span data-stu-id="5e16f-133">This function writes to the printer interface.</span></span> <span data-ttu-id="5e16f-134">Çağrı engelleniyor ve yalnızca bir hata olduğunda ya da aktarım tamamlandığında döndürülür.</span><span class="sxs-lookup"><span data-stu-id="5e16f-134">The call is blocking and only returns when there is either an error or when the transfer is complete.</span></span>

### <a name="parameters"></a><span data-ttu-id="5e16f-135">Parametreler</span><span class="sxs-lookup"><span data-stu-id="5e16f-135">Parameters</span></span>

- <span data-ttu-id="5e16f-136">**Yazıcı**: yazıcı sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-136">**printer**: Pointer to the printer class instance.</span></span>
- <span data-ttu-id="5e16f-137">**data_pointer**: veri yükünün arabellek adresine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-137">**data_pointer**: Pointer to the buffer address of the data payload.</span></span>
- <span data-ttu-id="5e16f-138">**requested_length**: gönderilecek uzunluk.</span><span class="sxs-lookup"><span data-stu-id="5e16f-138">**requested_length**: Length to be sent.</span></span>
- <span data-ttu-id="5e16f-139">**actual_length**: Uzunluk gerçekten gönderildi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-139">**actual_length**: Length actually sent.</span></span>

### <a name="return-value"></a><span data-ttu-id="5e16f-140">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="5e16f-140">Return Value</span></span>

- <span data-ttu-id="5e16f-141">**UX_SUCCESS**: (0x00) veri aktarımı tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="5e16f-141">**UX_SUCCESS**: (0x00) The data transfer was completed.</span></span>
- <span data-ttu-id="5e16f-142">**UX_TRANSFER_TIMEOUT**: (0x5c) aktarım zaman aşımı, yazma tamamlanmamış.</span><span class="sxs-lookup"><span data-stu-id="5e16f-142">**UX_TRANSFER_TIMEOUT**: (0x5c) Transfer timeout, writing incomplete.</span></span>

### <a name="example"></a><span data-ttu-id="5e16f-143">Örnek</span><span class="sxs-lookup"><span data-stu-id="5e16f-143">Example</span></span>

```C
UINT status;

/* The following example illustrates this service. */
status = ux_host_class_printer_write(printer, data_pointer, requested_length, &actual_length);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_printer_soft_reset"></a><span data-ttu-id="5e16f-144">ux_host_class_printer_soft_reset</span><span class="sxs-lookup"><span data-stu-id="5e16f-144">ux_host_class_printer_soft_reset</span></span>

<span data-ttu-id="5e16f-145">Yazıcıya yazılımdan sıfırlama işlemi gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="5e16f-145">Perform a soft reset to the printer.</span></span>

### <a name="prototype"></a><span data-ttu-id="5e16f-146">Prototype</span><span class="sxs-lookup"><span data-stu-id="5e16f-146">Prototype</span></span>

```C
UINT ux_host_class_printer_soft_reset(UX_HOST_CLASS_PRINTER *printer)
```

### <a name="description"></a><span data-ttu-id="5e16f-147">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5e16f-147">Description</span></span>

<span data-ttu-id="5e16f-148">Bu işlev, yazıcıya geçici bir sıfırlama işlemi gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="5e16f-148">This function performs a soft reset to the printer.</span></span>

### <a name="input-parameter"></a><span data-ttu-id="5e16f-149">Giriş parametresi</span><span class="sxs-lookup"><span data-stu-id="5e16f-149">Input Parameter</span></span>

- <span data-ttu-id="5e16f-150">**Yazıcı**: yazıcı sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-150">**printer**: Pointer to the printer class instance.</span></span>

### <a name="return-value"></a><span data-ttu-id="5e16f-151">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="5e16f-151">Return Value</span></span>

- <span data-ttu-id="5e16f-152">**UX_SUCCESS**: (0x00) sıfırlama tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="5e16f-152">**UX_SUCCESS**: (0x00)The reset was completed.</span></span>
- <span data-ttu-id="5e16f-153">**UX_TRANSFER_TIMEOUT**: (0x5c) aktarım zaman aşımı, sıfırlama tamamlanmadı.</span><span class="sxs-lookup"><span data-stu-id="5e16f-153">**UX_TRANSFER_TIMEOUT**: (0x5c) Transfer timeout, reset not completed.</span></span>

### <a name="example"></a><span data-ttu-id="5e16f-154">Örnek</span><span class="sxs-lookup"><span data-stu-id="5e16f-154">Example</span></span>

```C
UINT status;

/* The following example illustrates this service. */
status = ux_host_class_printer_soft_reset(printer);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_printer_status_get"></a><span data-ttu-id="5e16f-155">ux_host_class_printer_status_get</span><span class="sxs-lookup"><span data-stu-id="5e16f-155">ux_host_class_printer_status_get</span></span>

<span data-ttu-id="5e16f-156">Yazıcı durumunu al</span><span class="sxs-lookup"><span data-stu-id="5e16f-156">Get the printer status</span></span>

### <a name="prototype"></a><span data-ttu-id="5e16f-157">Prototype</span><span class="sxs-lookup"><span data-stu-id="5e16f-157">Prototype</span></span>

```C
UINT ux_host_class_printer_status_get( 
    UX_HOST_CLASS_PRINTER *printer,
    ULONG *printer_status)
```

### <a name="description"></a><span data-ttu-id="5e16f-158">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5e16f-158">Description</span></span>

<span data-ttu-id="5e16f-159">Bu işlev, yazıcı durumunu alır.</span><span class="sxs-lookup"><span data-stu-id="5e16f-159">This function obtains the printer status.</span></span> <span data-ttu-id="5e16f-160">Yazıcı durumu, LPT durumuna (1284 standart) benzer.</span><span class="sxs-lookup"><span data-stu-id="5e16f-160">The printer status is similar to the LPT status (1284 standard).</span></span>

### <a name="parameters"></a><span data-ttu-id="5e16f-161">Parametreler</span><span class="sxs-lookup"><span data-stu-id="5e16f-161">Parameters</span></span>

- <span data-ttu-id="5e16f-162">**Yazıcı**: yazıcı sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-162">**printer**: Pointer to the printer class instance.</span></span>
- <span data-ttu-id="5e16f-163">**printer_status**: döndürülecek durumun adresi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-163">**printer_status**: Address of the status to be returned.</span></span>

### <a name="return-value"></a><span data-ttu-id="5e16f-164">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="5e16f-164">Return Value</span></span>

- <span data-ttu-id="5e16f-165">**UX_SUCCESS** (0x00): sıfırlama tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="5e16f-165">**UX_SUCCESS** (0x00): The reset was completed.</span></span>
- <span data-ttu-id="5e16f-166">**UX_MEMORY_INSUFFICIENT**: (0x12) işlemi gerçekleştirmek için yeterli bellek yok.</span><span class="sxs-lookup"><span data-stu-id="5e16f-166">**UX_MEMORY_INSUFFICIENT**: (0x12) Not enough memory to perform the operation.</span></span>
- <span data-ttu-id="5e16f-167">**UX_TRANSFER_TIMEOUT**: (0x5c) aktarım zaman aşımı, sıfırlama tamamlanmadı</span><span class="sxs-lookup"><span data-stu-id="5e16f-167">**UX_TRANSFER_TIMEOUT**: (0x5c) Transfer timeout, reset not completed</span></span>

### <a name="example"></a><span data-ttu-id="5e16f-168">Örnek</span><span class="sxs-lookup"><span data-stu-id="5e16f-168">Example</span></span>

```C
UINT status;

/* The following example illustrates this service. */
status = ux_host_class_printer_status_get(printer, printer_status);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_printer_device_id_get"></a><span data-ttu-id="5e16f-169">ux_host_class_printer_device_id_get</span><span class="sxs-lookup"><span data-stu-id="5e16f-169">ux_host_class_printer_device_id_get</span></span>

<span data-ttu-id="5e16f-170">Yazıcı cihaz kimliğini alın.</span><span class="sxs-lookup"><span data-stu-id="5e16f-170">Get the printer device id.</span></span>

### <a name="prototype"></a><span data-ttu-id="5e16f-171">Prototype</span><span class="sxs-lookup"><span data-stu-id="5e16f-171">Prototype</span></span>

```C
UINT ux_host_class_printer_device_id_get( 
    UX_HOST_CLASS_PRINTER *printer,
    UCHAR *descriptor_buffer, 
    ULONG length)
```

### <a name="description"></a><span data-ttu-id="5e16f-172">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5e16f-172">Description</span></span>

<span data-ttu-id="5e16f-173">Bu işlev, yazıcı IEEE 1284 cihaz KIMLIĞI dizesini (big endian biçimindeki ilk iki baytın uzunluğu dahil) alır.</span><span class="sxs-lookup"><span data-stu-id="5e16f-173">This function obtains the printer IEEE 1284 device ID string (including length in the first two bytes in big endian format).</span></span>

### <a name="parameters"></a><span data-ttu-id="5e16f-174">Parametreler</span><span class="sxs-lookup"><span data-stu-id="5e16f-174">Parameters</span></span>

- <span data-ttu-id="5e16f-175">**Yazıcı**: yazıcı sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-175">**printer**: Pointer to the printer class instance.</span></span>
- <span data-ttu-id="5e16f-176">**descriptor_buffer**: IEEE 1284 cihaz kimliği dizesini (biçim olarak ilk iki baytın uzunluğu dahil) dolduracak bir arabelleğin işaretçisi</span><span class="sxs-lookup"><span data-stu-id="5e16f-176">**descriptor_buffer**: Pointer to a buffer to fill IEEE 1284 device ID string (including length in the first two bytes in BE format)</span></span> 
- <span data-ttu-id="5e16f-177">**uzunluk**: arabelleğin bayt cinsinden uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="5e16f-177">**length**: Length of buffer in bytes.</span></span>

### <a name="return-value"></a><span data-ttu-id="5e16f-178">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="5e16f-178">Return Value</span></span>

- <span data-ttu-id="5e16f-179">**UX_SUCCESS** (0x00): işlem başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="5e16f-179">**UX_SUCCESS** (0x00): The operation was successful.</span></span>
- <span data-ttu-id="5e16f-180">**UX_MEMORY_INSUFFICIENT**: (0x12) işlemi gerçekleştirmek için yeterli bellek yok.</span><span class="sxs-lookup"><span data-stu-id="5e16f-180">**UX_MEMORY_INSUFFICIENT**: (0x12) Not enough memory to perform the operation.</span></span>
- <span data-ttu-id="5e16f-181">**UX_TRANSFER_TIMEOUT**: (0x5c) aktarım zaman aşımı, istek tamamlanmadı</span><span class="sxs-lookup"><span data-stu-id="5e16f-181">**UX_TRANSFER_TIMEOUT**: (0x5c) Transfer timeout, request not completed</span></span>
- <span data-ttu-id="5e16f-182">**UX_TRANSFER_NOT_READY**: (0x25) cihaz geçersiz bir durumda, bağlı, ÇÖZÜMLENMIŞ veya yapılandırılmış olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5e16f-182">**UX_TRANSFER_NOT_READY**: (0x25) The device was in an invalid state – must be ATTACHED,ADDRESSED, or CONFIGURED.</span></span>
- <span data-ttu-id="5e16f-183">**UX_TRANSFER_STALL**: (0x21) aktarım durduruldu.</span><span class="sxs-lookup"><span data-stu-id="5e16f-183">**UX_TRANSFER_STALL**: (0x21) Transfer stalled.</span></span>
- <span data-ttu-id="5e16f-184">**TX_WAIT_ABORTED** (0x1A) askıya alma başka bir iş parçacığı, ZAMANLAYıCı veya ISR tarafından iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-184">**TX_WAIT_ABORTED** (0x1A) Suspension was aborted by another thread, timer, or ISR.</span></span>
- <span data-ttu-id="5e16f-185">**TX_SEMAPHORE_ERROR** (0x0C) geçersiz sayma semaforu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-185">**TX_SEMAPHORE_ERROR** (0x0C) Invalid counting semaphore pointer.</span></span>
- <span data-ttu-id="5e16f-186">**TX_WAIT_ERROR** (0x04) TX_NO_WAIT dışında bir bekleme seçeneği, iş parçacığından oluşan bir çağrıda belirtildi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-186">**TX_WAIT_ERROR** (0x04) A wait option other than TX_NO_WAIT was specified on a call from a non-thread.</span></span>

### <a name="example"></a><span data-ttu-id="5e16f-187">Örnek</span><span class="sxs-lookup"><span data-stu-id="5e16f-187">Example</span></span>

```C
UINT status;

/* The following example illustrates this service. */
status = ux_host_class_printer_device_id_get(printer, descriptor_buffer, length);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_audio_read"></a><span data-ttu-id="5e16f-188">ux_host_class_audio_read</span><span class="sxs-lookup"><span data-stu-id="5e16f-188">ux_host_class_audio_read</span></span>

<span data-ttu-id="5e16f-189">Ses arabiriminden okuyun.</span><span class="sxs-lookup"><span data-stu-id="5e16f-189">Read from the audio interface.</span></span>

### <a name="prototype"></a><span data-ttu-id="5e16f-190">Prototype</span><span class="sxs-lookup"><span data-stu-id="5e16f-190">Prototype</span></span>

```C
UINT ux_host_class_audio_read(
    UX_HOST_CLASS_AUDIO *audio,
    UX_HOST_CLASS_AUDIO_TRANSFER_REQUEST
    *audio_transfer_request)
```

### <a name="description"></a><span data-ttu-id="5e16f-191">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5e16f-191">Description</span></span>

<span data-ttu-id="5e16f-192">Bu işlev ses arabiriminden okur.</span><span class="sxs-lookup"><span data-stu-id="5e16f-192">This function reads from the audio interface.</span></span> <span data-ttu-id="5e16f-193">Çağrı engellenmemiş.</span><span class="sxs-lookup"><span data-stu-id="5e16f-193">The call is non-blocking.</span></span> <span data-ttu-id="5e16f-194">Uygulama, ses akışı arabirimi için uygun alternatif ayarın seçildiğinden emin olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5e16f-194">The application must ensure that the appropriate alternate setting has been selected for the audio streaming interface.</span></span>

### <a name="parameters"></a><span data-ttu-id="5e16f-195">Parametreler</span><span class="sxs-lookup"><span data-stu-id="5e16f-195">Parameters</span></span>

- <span data-ttu-id="5e16f-196">**Ses**: ses sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-196">**audio**: Pointer to the audio class instance.</span></span>
- <span data-ttu-id="5e16f-197">**audio_transfer_request**: ses aktarım yapısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-197">**audio_transfer_request**: Pointer to the audio transfer structure.</span></span>

### <a name="return-value"></a><span data-ttu-id="5e16f-198">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="5e16f-198">Return Value</span></span>

- <span data-ttu-id="5e16f-199">**UX_SUCCESS**: (0x00) veri aktarımı tamamlandı</span><span class="sxs-lookup"><span data-stu-id="5e16f-199">**UX_SUCCESS**: (0x00) The data transfer was completed</span></span>
- <span data-ttu-id="5e16f-200">**UX_FUNCTION_NOT_SUPPORTED**"(0x54) işlevi desteklenmiyor</span><span class="sxs-lookup"><span data-stu-id="5e16f-200">**UX_FUNCTION_NOT_SUPPORTED**" (0x54) Function not supported</span></span>

### <a name="example"></a><span data-ttu-id="5e16f-201">Örnek</span><span class="sxs-lookup"><span data-stu-id="5e16f-201">Example</span></span>

```C
/* The following example reads from the audio interface. */

audio_transfer_request.ux_host_class_audio_transfer_request_completion_function = tx_audio_transfer_completion_function;
audio_transfer_request.ux_host_class_audio_transfer_request_class_instance = audio;
audio_transfer_request.ux_host_class_audio_transfer_request_next_audio_audio_transfer_request = UX_NULL;
audio_transfer_request.ux_host_class_audio_transfer_request_data_pointer = audio_buffer;
audio_transfer_request.ux_host_class_audio_transfer_request_requested_length = requested_length;
audio_transfer_request.ux_host_class_audio_transfer_request_packet_length = AUDIO_FRAME_LENGTH;

status = ux_host_class_audio_read(audio, audio_transfer_request);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_audio_write"></a><span data-ttu-id="5e16f-202">ux_host_class_audio_write</span><span class="sxs-lookup"><span data-stu-id="5e16f-202">ux_host_class_audio_write</span></span>

<span data-ttu-id="5e16f-203">Ses arabirimine yazın.</span><span class="sxs-lookup"><span data-stu-id="5e16f-203">Write to the audio interface.</span></span>

### <a name="prototype"></a><span data-ttu-id="5e16f-204">Prototype</span><span class="sxs-lookup"><span data-stu-id="5e16f-204">Prototype</span></span>

```C
UINT ux_host_class_audio_write(
    UX_HOST_CLASS_AUDIO *audio,
    UX_HOST_CLASS_AUDIO_TRANSFER_REQUEST *audio_transfer_request)
```

### <a name="description"></a><span data-ttu-id="5e16f-205">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5e16f-205">Description</span></span>

<span data-ttu-id="5e16f-206">Bu işlev ses arabirimine yazar.</span><span class="sxs-lookup"><span data-stu-id="5e16f-206">This function writes to the audio interface.</span></span> <span data-ttu-id="5e16f-207">Çağrı engellenmemiş.</span><span class="sxs-lookup"><span data-stu-id="5e16f-207">The call is non-blocking.</span></span> <span data-ttu-id="5e16f-208">Uygulama, ses akışı arabirimi için uygun alternatif ayarın seçildiğinden emin olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5e16f-208">The application must ensure that the appropriate alternate setting has been selected for the audio streaming interface.</span></span>

### <a name="parameters"></a><span data-ttu-id="5e16f-209">Parametreler</span><span class="sxs-lookup"><span data-stu-id="5e16f-209">Parameters</span></span>

- <span data-ttu-id="5e16f-210">**Ses**: ses sınıfı örneğine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="5e16f-210">**audio**: Pointer to the audio class instance</span></span>
- <span data-ttu-id="5e16f-211">**audio_transfer_request**: ses aktarım yapısına yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="5e16f-211">**audio_transfer_request**: Pointer to the audio transfer structure</span></span>

### <a name="return-value"></a><span data-ttu-id="5e16f-212">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="5e16f-212">Return Value</span></span>

- <span data-ttu-id="5e16f-213">**UX_SUCCESS**: (0x00) veri aktarımı tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="5e16f-213">**UX_SUCCESS**: (0x00) The data transfer was completed.</span></span>
- <span data-ttu-id="5e16f-214">**UX_FUNCTION_NOT_SUPPORTED**: (0x54) işlev desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="5e16f-214">**UX_FUNCTION_NOT_SUPPORTED**: (0x54) Function not supported.</span></span>
- <span data-ttu-id="5e16f-215">**ux_host_CLASS_AUDIO_WRONG_INTERFACE**: (0x81) arabirimi yanlış.</span><span class="sxs-lookup"><span data-stu-id="5e16f-215">**ux_host_CLASS_AUDIO_WRONG_INTERFACE**: (0x81) Interface incorrect.</span></span>

### <a name="example"></a><span data-ttu-id="5e16f-216">Örnek</span><span class="sxs-lookup"><span data-stu-id="5e16f-216">Example</span></span>

```C
UINT status;

/* The following example writes to the audio interface */

audio_transfer_request.ux_host_class_audio_transfer_request_completion_function = tx_audio_transfer_completion_function;
audio_transfer_request.ux_host_class_audio_transfer_request_class_instance = audio;
audio_transfer_request.ux_host_class_audio_transfer_request_next_audio_audio_transfer_request = UX_NULL;
audio_transfer_request.ux_host_class_audio_transfer_request_data_pointer = audio_buffer;
audio_transfer_request.ux_host_class_audio_transfer_request_requested_length = requested_length;
audio_transfer_request.ux_host_class_audio_transfer_request_packet_length = AUDIO_FRAME_LENGTH;
status = ux_host_class_audio_write(audio, audio_transfer_request);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_audio_control_get"></a><span data-ttu-id="5e16f-217">ux_host_class_audio_control_get</span><span class="sxs-lookup"><span data-stu-id="5e16f-217">ux_host_class_audio_control_get</span></span>

<span data-ttu-id="5e16f-218">Ses denetim arabiriminden belirli bir denetim alın.</span><span class="sxs-lookup"><span data-stu-id="5e16f-218">Get a specific control from the audio control interface.</span></span>

### <a name="prototype"></a><span data-ttu-id="5e16f-219">Prototype</span><span class="sxs-lookup"><span data-stu-id="5e16f-219">Prototype</span></span>

```C
UINT ux_host_class_audio_control_get(
    UX_HOST_CLASS_AUDIO *audio,
    UX_HOST_CLASS_AUDIO_CONTROL *audio_control)
```

### <a name="description"></a><span data-ttu-id="5e16f-220">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5e16f-220">Description</span></span>

<span data-ttu-id="5e16f-221">Bu işlev, ses denetim arabiriminden belirli bir denetimi okur.</span><span class="sxs-lookup"><span data-stu-id="5e16f-221">This function reads a specific control from the audio control interface.</span></span>

### <a name="parameters"></a><span data-ttu-id="5e16f-222">Parametreler</span><span class="sxs-lookup"><span data-stu-id="5e16f-222">Parameters</span></span>

- <span data-ttu-id="5e16f-223">**Ses**: ses sınıfı örneğine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="5e16f-223">**audio**: Pointer to the audio class instance</span></span>
- <span data-ttu-id="5e16f-224">**audio_control**: ses denetimi yapısına yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="5e16f-224">**audio_control**: Pointer to the audio control structure</span></span>

### <a name="return-value"></a><span data-ttu-id="5e16f-225">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="5e16f-225">Return Value</span></span>

- <span data-ttu-id="5e16f-226">**UX_SUCCESS**: (0x00) veri aktarımı tamamlandı</span><span class="sxs-lookup"><span data-stu-id="5e16f-226">**UX_SUCCESS**: (0x00) The data transfer was completed</span></span>
- <span data-ttu-id="5e16f-227">**UX_FUNCTION_NOT_SUPPORTED**: (0x54) işlev desteklenmiyor</span><span class="sxs-lookup"><span data-stu-id="5e16f-227">**UX_FUNCTION_NOT_SUPPORTED**: (0x54) Function not supported</span></span>
- <span data-ttu-id="5e16f-228">**UX_HOST_CLASS_AUDIO_WRONG_INTERFACE**: (0x81) arabirim yanlış</span><span class="sxs-lookup"><span data-stu-id="5e16f-228">**UX_HOST_CLASS_AUDIO_WRONG_INTERFACE**: (0x81) Interface incorrect</span></span>

### <a name="example"></a><span data-ttu-id="5e16f-229">Örnek</span><span class="sxs-lookup"><span data-stu-id="5e16f-229">Example</span></span>

```C
UINT status;

/* The following example reads the volume control from a stereo USB speaker. */

UX_HOST_CLASS_AUDIO_CONTROL audio_control;

audio_control.ux_host_class_audio_control_channel = 1;
audio_control.ux_host_class_audio_control = UX_HOST_CLASS_AUDIO_VOLUME_CONTROL;

status = ux_host_class_audio_control_get(audio, &audio_control);

/* If status equals UX_SUCCESS, the operation was successful. */

audio_control.ux_host_class_audio_control_channel = 2;
audio_control.ux_host_class_audio_control = UX_HOST_CLASS_AUDIO_VOLUME_CONTROL;

status = ux_host_class_audio_control_get(audio, &audio_control);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_audio_control_value_set"></a><span data-ttu-id="5e16f-230">ux_host_class_audio_control_value_set</span><span class="sxs-lookup"><span data-stu-id="5e16f-230">ux_host_class_audio_control_value_set</span></span>

<span data-ttu-id="5e16f-231">Ses denetim arabirimine belirli bir denetim ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="5e16f-231">Set a specific control to the audio control interface.</span></span>

### <a name="prototype"></a><span data-ttu-id="5e16f-232">Prototype</span><span class="sxs-lookup"><span data-stu-id="5e16f-232">Prototype</span></span>

```C
UINT ux_host_class_audio_control_value_set(
    UX_HOST_CLASS_AUDIO *audio,
    UX_HOST_CLASS_AUDIO_CONTROL *audio_control)
```

<span data-ttu-id="5e16f-233">\* \* Açıklama \* \*</span><span class="sxs-lookup"><span data-stu-id="5e16f-233">\*\*Description \*\*</span></span>

<span data-ttu-id="5e16f-234">Bu işlev, ses denetim arabirimine belirli bir denetim ayarlar.</span><span class="sxs-lookup"><span data-stu-id="5e16f-234">This function sets a specific control to the audio control interface.</span></span>

### <a name="parameters"></a><span data-ttu-id="5e16f-235">Parametreler</span><span class="sxs-lookup"><span data-stu-id="5e16f-235">Parameters</span></span>

- <span data-ttu-id="5e16f-236">**Ses**: ses sınıfı örneğine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="5e16f-236">**audio**: Pointer to the audio class instance</span></span>
- <span data-ttu-id="5e16f-237">**audio_control**: ses denetimi yapısına yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="5e16f-237">**audio_control**: Pointer to the audio control structure</span></span>

### <a name="return-value"></a><span data-ttu-id="5e16f-238">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="5e16f-238">Return Value</span></span>

- <span data-ttu-id="5e16f-239">**UX_SUCCESS**: (0x00) veri aktarımı tamamlandı</span><span class="sxs-lookup"><span data-stu-id="5e16f-239">**UX_SUCCESS**: (0x00) The data transfer was completed</span></span>
- <span data-ttu-id="5e16f-240">**UX_FUNCTION_NOT_SUPPORTED**: (0x54) işlev desteklenmiyor</span><span class="sxs-lookup"><span data-stu-id="5e16f-240">**UX_FUNCTION_NOT_SUPPORTED**: (0x54) Function not supported</span></span>
- <span data-ttu-id="5e16f-241">**UX_HOST_CLASS_AUDIO_WRONG_INTERFACE**: (0x81) arabirim yanlış</span><span class="sxs-lookup"><span data-stu-id="5e16f-241">**UX_HOST_CLASS_AUDIO_WRONG_INTERFACE**: (0x81) Interface incorrect</span></span>

### <a name="example"></a><span data-ttu-id="5e16f-242">Örnek</span><span class="sxs-lookup"><span data-stu-id="5e16f-242">Example</span></span>

```C
/* The following example sets the volume control of a stereo USB speaker. */

UX_HOST_CLASS_AUDIO_CONTROL audio_control;

UINT status;

audio_control.ux_host_class_audio_control_channel = 1;
audio_control.ux_host_class_audio_control = UX_HOST_CLASS_AUDIO_VOLUME_CONTROL;
audio_control.ux_host_class_audio_control_cur = 0xf000;

status = ux_host_class_audio_control_value_set(audio, &audio_control);
/* If status equals UX_SUCCESS, the operation was successful. */

current_volume = audio_control.audio_control_cur;
audio_control.ux_host_class_audio_control_channel = 2;
audio_control.ux_host_class_audio_control = UX_HOST_CLASS_AUDIO_VOLUME_CONTROL;
audio_control.ux_host_class_audio_control_cur = 0xf000;

status = ux_host_class_audio_control_value_set(audio, &audio_control);
/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_audio_streaming_sampling_set"></a><span data-ttu-id="5e16f-243">ux_host_class_audio_streaming_sampling_set</span><span class="sxs-lookup"><span data-stu-id="5e16f-243">ux_host_class_audio_streaming_sampling_set</span></span>

<span data-ttu-id="5e16f-244">Ses akışı arabiriminin alternatif ayar arabirimini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="5e16f-244">Set an alternate setting interface of the audio streaming interface.</span></span>

### <a name="prototype"></a><span data-ttu-id="5e16f-245">Prototype</span><span class="sxs-lookup"><span data-stu-id="5e16f-245">Prototype</span></span>

```C
UINT ux_host_class_audio_streaming_sampling_set
    (UX_HOST_CLASS_AUDIO *audio,
    UX_HOST_CLASS_AUDIO_SAMPLING *audio_sampling)
```

### <a name="description"></a><span data-ttu-id="5e16f-246">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5e16f-246">Description</span></span>

<span data-ttu-id="5e16f-247">Bu işlev, ses akış arabiriminin uygun alternatif ayar arabirimini belirli bir örnekleme yapısına göre ayarlar.</span><span class="sxs-lookup"><span data-stu-id="5e16f-247">This function sets the appropriate alternate setting interface of the audio streaming interface according to a specific sampling structure.</span></span>

### <a name="parameters"></a><span data-ttu-id="5e16f-248">Parametreler</span><span class="sxs-lookup"><span data-stu-id="5e16f-248">Parameters</span></span>

- <span data-ttu-id="5e16f-249">**Ses**: ses sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-249">**audio**: Pointer to the audio class instance.</span></span>
- <span data-ttu-id="5e16f-250">**audio_sampling**: ses örnekleme yapısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-250">**audio_sampling**: Pointer to the audio sampling structure.</span></span>

### <a name="return-value"></a><span data-ttu-id="5e16f-251">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="5e16f-251">Return Value</span></span>

- <span data-ttu-id="5e16f-252">**UX_SUCCESS**: (0x00) veri aktarımı tamamlandı</span><span class="sxs-lookup"><span data-stu-id="5e16f-252">**UX_SUCCESS**: (0x00) The data transfer was completed</span></span>
- <span data-ttu-id="5e16f-253">**UX_FUNCTION_NOT_SUPPORTED**: (0x54) işlev desteklenmiyor</span><span class="sxs-lookup"><span data-stu-id="5e16f-253">**UX_FUNCTION_NOT_SUPPORTED**: (0x54) Function not supported</span></span>
- <span data-ttu-id="5e16f-254">**UX_HOST_CLASS_AUDIO_WRONG_INTERFACE**: (0x81) arabirim yanlış</span><span class="sxs-lookup"><span data-stu-id="5e16f-254">**UX_HOST_CLASS_AUDIO_WRONG_INTERFACE**: (0x81) Interface incorrect</span></span>
- <span data-ttu-id="5e16f-255">**UX_NO_ALTERNATE_SETTING**: (0x5E) örnekleme değerleri için alternatif ayar yok</span><span class="sxs-lookup"><span data-stu-id="5e16f-255">**UX_NO_ALTERNATE_SETTING**: (0x5e) No alternate setting for the sampling values</span></span>

### <a name="example"></a><span data-ttu-id="5e16f-256">Örnek</span><span class="sxs-lookup"><span data-stu-id="5e16f-256">Example</span></span>

```C
/* The following example sets the alternate setting interface of a stereo USB speaker. */

UX_HOST_CLASS_AUDIO_SAMPLING audio_sampling;

UINT status;

sampling.ux_host_class_audio_sampling_channels = 2;
sampling.ux_host_class_audio_sampling_frequency = AUDIO_FREQUENCY;
sampling. ux_host_class_audio_sampling_resolution = 16;

status = ux_host_class_audio_streaming_sampling_set(audio, &sampling);
/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_audio_streaming_sampling_get"></a><span data-ttu-id="5e16f-257">ux_host_class_audio_streaming_sampling_get</span><span class="sxs-lookup"><span data-stu-id="5e16f-257">ux_host_class_audio_streaming_sampling_get</span></span>

<span data-ttu-id="5e16f-258">Ses akışı arabiriminin olası örnekleme ayarlarını öğrenin.</span><span class="sxs-lookup"><span data-stu-id="5e16f-258">Get possible sampling settings of audio streaming interface.</span></span>

### <a name="prototype"></a><span data-ttu-id="5e16f-259">Prototype</span><span class="sxs-lookup"><span data-stu-id="5e16f-259">Prototype</span></span>

```C
UINT ux_host_class_audio_streaming_sampling_get(
    UX_HOST_CLASS_AUDIO *audio,
    UX_HOST_CLASS_AUDIO_SAMPLING_CHARACTERISTICS *audio_sampling)
```

### <a name="description"></a><span data-ttu-id="5e16f-260">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5e16f-260">Description</span></span>

<span data-ttu-id="5e16f-261">Bu işlev, bir diğeri, ses akış arabiriminin alternatif ayarlarında bulunan tüm olası örnekleme ayarlarını alır.</span><span class="sxs-lookup"><span data-stu-id="5e16f-261">This function gets, one by one, all the possible sampling settings available in each of the alternate settings of the audio streaming interface.</span></span> <span data-ttu-id="5e16f-262">İşlev ilk kez kullanıldığında, çağırma yapısı işaretçisindeki tüm alanların sıfırlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5e16f-262">The first time the function is used, all the fields in the calling structure pointer must be reset.</span></span> <span data-ttu-id="5e16f-263">Bu işlev, alternatif ayarların sonuna ulaşılmadığı takdirde, return üzerinde belirli bir akış değeri kümesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="5e16f-263">The function will return a specific set of streaming values upon return unless the end of the alternate settings has been reached.</span></span> <span data-ttu-id="5e16f-264">Bu işlev yeniden kullanıldığında, sonraki örnekleme değerlerini bulmak için önceki örnekleme değerleri kullanılacaktır.</span><span class="sxs-lookup"><span data-stu-id="5e16f-264">When this function is reused, the previous sampling values will be used to find the next sampling values.</span></span>

### <a name="parameters"></a><span data-ttu-id="5e16f-265">Parametreler</span><span class="sxs-lookup"><span data-stu-id="5e16f-265">Parameters</span></span>

- <span data-ttu-id="5e16f-266">**Ses**: ses sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-266">**audio**: Pointer to the audio class instance.</span></span>
- <span data-ttu-id="5e16f-267">**audio_sampling**: ses örnekleme yapısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-267">**audio_sampling**: Pointer to the audio sampling structure.</span></span>

### <a name="return-value"></a><span data-ttu-id="5e16f-268">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="5e16f-268">Return Value</span></span>

- <span data-ttu-id="5e16f-269">**UX_SUCCESS**: (0x00) veri aktarımı tamamlandı</span><span class="sxs-lookup"><span data-stu-id="5e16f-269">**UX_SUCCESS**: (0x00) The data transfer was completed</span></span>
- <span data-ttu-id="5e16f-270">**UX_FUNCTION_NOT_SUPPORTED**: (0x54) işlev desteklenmiyor</span><span class="sxs-lookup"><span data-stu-id="5e16f-270">**UX_FUNCTION_NOT_SUPPORTED**: (0x54) Function not supported</span></span>
- <span data-ttu-id="5e16f-271">**UX_HOST_CLASS_AUDIO_WRONG_INTERFACE**: (0x81) arabirim yanlış</span><span class="sxs-lookup"><span data-stu-id="5e16f-271">**UX_HOST_CLASS_AUDIO_WRONG_INTERFACE**: (0x81) Interface incorrect</span></span>
- <span data-ttu-id="5e16f-272">**UX_NO_ALTERNATE_SETTING**: (0x5E) örnekleme değerleri için alternatif ayar yok</span><span class="sxs-lookup"><span data-stu-id="5e16f-272">**UX_NO_ALTERNATE_SETTING**: (0x5e) No alternate setting for the sampling values</span></span>

### <a name="example"></a><span data-ttu-id="5e16f-273">Örnek</span><span class="sxs-lookup"><span data-stu-id="5e16f-273">Example</span></span>

```C
/* The following example gets the sampling values for the first alternate setting interface of a stereo USB speaker. */

UX_HOST_CLASS_AUDIO_SAMPLING_CHARACTERISTICS audio_sampling;

UINT status;

sampling.ux_host_class_audio_sampling_channels=0;
sampling.ux_host_class_audio_sampling_frequency_low=0;
sampling.ux_host_class_audio_sampling_frequency_high=0;
sampling.ux_host_class_audio_sampling_resolution=0;

status = ux_host_class_audio_streaming_sampling_get(audio, &sampling);

/* If status equals UX_SUCCESS, the operation was successful and information could be displayed as follows:

printf("Number of channels %d, Resolution %d bits, frequency range %d-%d\n",
    sampling.audio_channels, sampling.audio_resolution,
    sampling.audio_frequency_low, sampling.audio_frequency_high);

*/
```

## <a name="ux_host_class_asix_read"></a><span data-ttu-id="5e16f-274">ux_host_class_asix_read</span><span class="sxs-lookup"><span data-stu-id="5e16f-274">ux_host_class_asix_read</span></span>

<span data-ttu-id="5e16f-275">Asix arabiriminden okuyun.</span><span class="sxs-lookup"><span data-stu-id="5e16f-275">Read from the asix interface.</span></span>

### <a name="prototype"></a><span data-ttu-id="5e16f-276">Prototype</span><span class="sxs-lookup"><span data-stu-id="5e16f-276">Prototype</span></span>

```C
UINT ux_host_class_asix_read(
    UX_HOST_CLASS_ASIX *asix,
    UCHAR *data_pointer,
    ULONG requested_length,
    ULONG *actual_length)
```

### <a name="description"></a><span data-ttu-id="5e16f-277">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5e16f-277">Description</span></span>

<span data-ttu-id="5e16f-278">Bu işlev, asix arabiriminden okur.</span><span class="sxs-lookup"><span data-stu-id="5e16f-278">This function reads from the asix interface.</span></span> <span data-ttu-id="5e16f-279">Çağrı engelleniyor ve yalnızca bir hata olduğunda ya da aktarım tamamlandığında döndürülür.</span><span class="sxs-lookup"><span data-stu-id="5e16f-279">The call is blocking and only returns when there is either an error or when the transfer is complete.</span></span>

### <a name="parameters"></a><span data-ttu-id="5e16f-280">Parametreler</span><span class="sxs-lookup"><span data-stu-id="5e16f-280">Parameters</span></span>

- <span data-ttu-id="5e16f-281">**asix**: aaltısınıf örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-281">**asix**: Pointer to the asix class instance.</span></span>
- <span data-ttu-id="5e16f-282">**data_pointer**: veri yükünün arabellek adresine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-282">**data_pointer**: Pointer to the buffer address of the data payload.</span></span>
- <span data-ttu-id="5e16f-283">**requested_length**: alınacak uzunluk.</span><span class="sxs-lookup"><span data-stu-id="5e16f-283">**requested_length**: Length to be received.</span></span>
- <span data-ttu-id="5e16f-284">**actual_length**: Uzunluk gerçekten alındı.</span><span class="sxs-lookup"><span data-stu-id="5e16f-284">**actual_length**: Length actually received.</span></span>

### <a name="return-value"></a><span data-ttu-id="5e16f-285">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="5e16f-285">Return Value</span></span>

- <span data-ttu-id="5e16f-286">**UX_SUCCESS**: (0x00) veri aktarımı tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="5e16f-286">**UX_SUCCESS**: (0x00) The data transfer was completed.</span></span>
- <span data-ttu-id="5e16f-287">**UX_TRANSFER_TIMEOUT**: (0x5c) aktarım zaman aşımı, okuma tamamlanmadı.</span><span class="sxs-lookup"><span data-stu-id="5e16f-287">**UX_TRANSFER_TIMEOUT**: (0x5c) Transfer timeout, reading incomplete.</span></span>

### <a name="example"></a><span data-ttu-id="5e16f-288">Örnek</span><span class="sxs-lookup"><span data-stu-id="5e16f-288">Example</span></span>

```C
UINT status;

/* The following example illustrates this service. */

status = ux_host_class_asix_read(asix, data_pointer, requested_length, &actual_length);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_asix_write"></a><span data-ttu-id="5e16f-289">ux_host_class_asix_write</span><span class="sxs-lookup"><span data-stu-id="5e16f-289">ux_host_class_asix_write</span></span>

<span data-ttu-id="5e16f-290">Asix arabirimine yazın.</span><span class="sxs-lookup"><span data-stu-id="5e16f-290">Write to the asix interface.</span></span>

### <a name="prototype"></a><span data-ttu-id="5e16f-291">Prototype</span><span class="sxs-lookup"><span data-stu-id="5e16f-291">Prototype</span></span>

```C
UINT ux_host_class_asix_write(
    VOID *asix_class,
    NX_PACKET *packet)
```

### <a name="description"></a><span data-ttu-id="5e16f-292">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5e16f-292">Description</span></span>

<span data-ttu-id="5e16f-293">Bu işlev, asix arabirimine yazar.</span><span class="sxs-lookup"><span data-stu-id="5e16f-293">This function writes to the asix interface.</span></span> <span data-ttu-id="5e16f-294">Çağrı engellenmeyen bir.</span><span class="sxs-lookup"><span data-stu-id="5e16f-294">The call is non blocking.</span></span>

### <a name="parameters"></a><span data-ttu-id="5e16f-295">Parametreler</span><span class="sxs-lookup"><span data-stu-id="5e16f-295">Parameters</span></span>

- <span data-ttu-id="5e16f-296">**asix**: aaltısınıf örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-296">**asix**: Pointer to the asix class instance.</span></span>
- <span data-ttu-id="5e16f-297">**paket**: NETX veri paketi</span><span class="sxs-lookup"><span data-stu-id="5e16f-297">**packet**: Netx data packet</span></span>

### <a name="return-value"></a><span data-ttu-id="5e16f-298">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="5e16f-298">Return Value</span></span>

- <span data-ttu-id="5e16f-299">**UX_SUCCESS**: (0x00) veri aktarımı tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="5e16f-299">**UX_SUCCESS**: (0x00) The data transfer was completed.</span></span>
- <span data-ttu-id="5e16f-300">**UX_ERROR**: (0xFF) aktarma istendi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-300">**UX_ERROR**: (0xFF) Transfer could not be requested.</span></span>

### <a name="example"></a><span data-ttu-id="5e16f-301">Örnek</span><span class="sxs-lookup"><span data-stu-id="5e16f-301">Example</span></span>

```C
UINT status;

/* The following example illustrates this service. */

status = ux_host_class_asix_write(asix, packet);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_pima_session_open"></a><span data-ttu-id="5e16f-302">ux_host_class_pima_session_open</span><span class="sxs-lookup"><span data-stu-id="5e16f-302">ux_host_class_pima_session_open</span></span>

<span data-ttu-id="5e16f-303">Başlatıcı ve Yanıtlayıcı arasında bir oturum açın.</span><span class="sxs-lookup"><span data-stu-id="5e16f-303">Open a session between Initiator and Responder.</span></span>

### <a name="prototype"></a><span data-ttu-id="5e16f-304">Prototype</span><span class="sxs-lookup"><span data-stu-id="5e16f-304">Prototype</span></span>

```C
UINT ux_host_class_pima_session_open(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session)
```

### <a name="description"></a><span data-ttu-id="5e16f-305">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5e16f-305">Description</span></span>

<span data-ttu-id="5e16f-306">Bu işlev, bir PIMA başlatıcısı ile bir PIMA Yanıtlayıcısı arasında bir oturum açar.</span><span class="sxs-lookup"><span data-stu-id="5e16f-306">This function opens a session between a PIMA Initiator and a PIMA Responder.</span></span> <span data-ttu-id="5e16f-307">Bir oturum başarıyla açıldıktan sonra, çoğu PIMA komutları yürütülebilir.</span><span class="sxs-lookup"><span data-stu-id="5e16f-307">Once a session is successfully opened, most PIMA commands can be executed.</span></span>

### <a name="parameters"></a><span data-ttu-id="5e16f-308">Parametreler</span><span class="sxs-lookup"><span data-stu-id="5e16f-308">Parameters</span></span>

- <span data-ttu-id="5e16f-309">**Pima**: Pima sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-309">**pima**: Pointer to the pima class instance.</span></span>
- <span data-ttu-id="5e16f-310">**pima_sessio**: Pima oturumu< işaretçisi</span><span class="sxs-lookup"><span data-stu-id="5e16f-310">**pima_sessio**: Pointer to PIMA session<</span></span>

### <a name="return-value"></a><span data-ttu-id="5e16f-311">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="5e16f-311">Return Value</span></span>

- <span data-ttu-id="5e16f-312">**UX_SUCCESS**: (0x00) oturum başarıyla açıldı</span><span class="sxs-lookup"><span data-stu-id="5e16f-312">**UX_SUCCESS**: (0x00) Session successfully opened</span></span>
- <span data-ttu-id="5e16f-313">**UX_HOST_CLASS_PIMA_RC_SESSION_ALREADY_OPENED**: (0X201e) oturum zaten açık</span><span class="sxs-lookup"><span data-stu-id="5e16f-313">**UX_HOST_CLASS_PIMA_RC_SESSION_ALREADY_OPENED**: (0x201E) Session already opened</span></span>

### <a name="example"></a><span data-ttu-id="5e16f-314">Örnek</span><span class="sxs-lookup"><span data-stu-id="5e16f-314">Example</span></span>

```C
/* Open a pima session. */

status = ux_host_class_pima_session_open(pima, pima_session);

if (status != UX_SUCCESS)
    return(UX_PICTBRIDGE_ERROR_SESSION_NOT_OPEN);
```

## <a name="ux_host_class_pima_session_close"></a><span data-ttu-id="5e16f-315">ux_host_class_pima_session_close</span><span class="sxs-lookup"><span data-stu-id="5e16f-315">ux_host_class_pima_session_close</span></span>

<span data-ttu-id="5e16f-316">Başlatıcı ve Yanıtlayıcı arasında bir oturumu kapatın.</span><span class="sxs-lookup"><span data-stu-id="5e16f-316">Close a session between Initiator and Responder.</span></span>

### <a name="prototype"></a><span data-ttu-id="5e16f-317">Prototype</span><span class="sxs-lookup"><span data-stu-id="5e16f-317">Prototype</span></span>

```C
UINT ux_host_class_pima_session_close(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session)
```

### <a name="description"></a><span data-ttu-id="5e16f-318">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5e16f-318">Description</span></span>

<span data-ttu-id="5e16f-319">Bu işlev, daha önce bir PIMA başlatıcısı ve bir PIMA Yanıtlayıcısı arasında açılan bir oturumu kapatır.</span><span class="sxs-lookup"><span data-stu-id="5e16f-319">This function closes a session that was previously opened between a PIMA Initiator and a PIMA Responder.</span></span> <span data-ttu-id="5e16f-320">Bir oturum kapatıldıktan sonra, çoğu PIMA komutları artık yürütülemez.</span><span class="sxs-lookup"><span data-stu-id="5e16f-320">Once a session is closed, most PIMA commands can no longer be executed.</span></span>

### <a name="parameters"></a><span data-ttu-id="5e16f-321">Parametreler</span><span class="sxs-lookup"><span data-stu-id="5e16f-321">Parameters</span></span>

- <span data-ttu-id="5e16f-322">**Pima**: Pima sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-322">**pima**: Pointer to the pima class instance.</span></span>
- <span data-ttu-id="5e16f-323">**pima_session**: Pima oturumuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-323">**pima_session**: Pointer to PIMA session.</span></span>

### <a name="return-value"></a><span data-ttu-id="5e16f-324">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="5e16f-324">Return Value</span></span>

- <span data-ttu-id="5e16f-325">**UX_SUCCESS**: (0x00) oturum kapatıldı.</span><span class="sxs-lookup"><span data-stu-id="5e16f-325">**UX_SUCCESS**: (0x00) The session was closed.</span></span>
- <span data-ttu-id="5e16f-326">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) oturum açılmadı.</span><span class="sxs-lookup"><span data-stu-id="5e16f-326">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) Session not opened.</span></span>

### <a name="example"></a><span data-ttu-id="5e16f-327">Örnek</span><span class="sxs-lookup"><span data-stu-id="5e16f-327">Example</span></span>

```C
/* Close the pima session. */

status = ux_host_class_pima_session_close(pima, pima_session);
```

## <a name="ux_host_class_pima_storage_ids_get"></a><span data-ttu-id="5e16f-328">ux_host_class_pima_storage_ids_get</span><span class="sxs-lookup"><span data-stu-id="5e16f-328">ux_host_class_pima_storage_ids_get</span></span>

<span data-ttu-id="5e16f-329">Yanıtlayanın depolama KIMLIĞI dizisini edinin.</span><span class="sxs-lookup"><span data-stu-id="5e16f-329">Obtain the storage ID array from Responder.</span></span>

### <a name="prototype"></a><span data-ttu-id="5e16f-330">Prototype</span><span class="sxs-lookup"><span data-stu-id="5e16f-330">Prototype</span></span>

```C
UINT ux_host_class_pima_storage_ids_get(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    ULONG *storage_ids_array,
    ULONG storage_id_length)
```

### <a name="description"></a><span data-ttu-id="5e16f-331">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5e16f-331">Description</span></span>

<span data-ttu-id="5e16f-332">Bu işlev, yanıtlayanın depolama KIMLIĞI dizisini edinir.</span><span class="sxs-lookup"><span data-stu-id="5e16f-332">This function obtains the storage ID array from the responder.</span></span>

### <a name="parameters"></a><span data-ttu-id="5e16f-333">Parametreler</span><span class="sxs-lookup"><span data-stu-id="5e16f-333">Parameters</span></span>

- <span data-ttu-id="5e16f-334">**Pima**: Pima sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-334">**pima**: Pointer to the pima class instance.</span></span>
- <span data-ttu-id="5e16f-335">**pima_session**: Pima oturumuna yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="5e16f-335">**pima_session**: Pointer to PIMA session</span></span>
- <span data-ttu-id="5e16f-336">**storage_ids_array**: depolama kimliklerinin döndürüldüğü dizi</span><span class="sxs-lookup"><span data-stu-id="5e16f-336">**storage_ids_array**: Array where storage IDs will be returned</span></span>
- <span data-ttu-id="5e16f-337">**storage_id_length**: depolama dizisinin uzunluğu</span><span class="sxs-lookup"><span data-stu-id="5e16f-337">**storage_id_length**: Length of the storage array</span></span>

### <a name="return-value"></a><span data-ttu-id="5e16f-338">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="5e16f-338">Return Value</span></span>

- <span data-ttu-id="5e16f-339">**UX_SUCCESS**: (0x00) depolama kimliği dizisi doldurulmuş</span><span class="sxs-lookup"><span data-stu-id="5e16f-339">**UX_SUCCESS**: (0x00) The storage ID array has been populated</span></span>
- <span data-ttu-id="5e16f-340">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) oturum açılmadı</span><span class="sxs-lookup"><span data-stu-id="5e16f-340">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) Session not opened</span></span>
- <span data-ttu-id="5e16f-341">**UX_MEMORY_INSUFFICIENT**: (0x12) Pima komutu oluşturmak için yeterli bellek yok.</span><span class="sxs-lookup"><span data-stu-id="5e16f-341">**UX_MEMORY_INSUFFICIENT**: (0x12) Not enough memory to create PIMA command.</span></span>

### <a name="example"></a><span data-ttu-id="5e16f-342">Örnek</span><span class="sxs-lookup"><span data-stu-id="5e16f-342">Example</span></span>

```C
/* Get the number of storage IDs. */
status = ux_host_class_pima_storage_ids_get(pima, pima_session,
    pictbridge ->ux_pictbridge_storage_ids, 64);

if (status != UX_SUCCESS)
{
    /* Close the pima session. */
    status = ux_host_class_pima_session_close(pima, pima_session);

    return(UX_PICTBRIDGE_ERROR_STORE_NOT_AVAILABLE);
}
```

## <a name="ux_host_class_pima_storage_info_get"></a><span data-ttu-id="5e16f-343">ux_host_class_pima_storage_info_get</span><span class="sxs-lookup"><span data-stu-id="5e16f-343">ux_host_class_pima_storage_info_get</span></span>

<span data-ttu-id="5e16f-344">Yanıtlayanın depolama bilgilerini alın.</span><span class="sxs-lookup"><span data-stu-id="5e16f-344">Obtain the storage information from Responder.</span></span>

### <a name="prototype"></a><span data-ttu-id="5e16f-345">Prototype</span><span class="sxs-lookup"><span data-stu-id="5e16f-345">Prototype</span></span>

```C
UINT ux_host_class_pima_storage_info_get(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    ULONG storage_id,
    UX_HOST_CLASS_PIMA_STORAGE *storage)
```

### <a name="description"></a><span data-ttu-id="5e16f-346">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5e16f-346">Description</span></span>

<span data-ttu-id="5e16f-347">Bu işlev, *storage_id* bir depolama kapsayıcısı için depolama bilgilerini edinir.</span><span class="sxs-lookup"><span data-stu-id="5e16f-347">This function obtains the storage information for a storage container of value *storage_id*.</span></span>

### <a name="parameters"></a><span data-ttu-id="5e16f-348">Parametreler</span><span class="sxs-lookup"><span data-stu-id="5e16f-348">Parameters</span></span>

- <span data-ttu-id="5e16f-349">**Pima**: Pima sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-349">**pima**: Pointer to the pima class instance.</span></span>
- <span data-ttu-id="5e16f-350">**pima_session**: Pima oturumuna yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="5e16f-350">**pima_session**: Pointer to PIMA session</span></span>
- <span data-ttu-id="5e16f-351">**storage_id**: depolama kapsayıcısının kimliği</span><span class="sxs-lookup"><span data-stu-id="5e16f-351">**storage_id**: ID of the storage container</span></span>
- <span data-ttu-id="5e16f-352">**depolama**: depolama bilgileri kapsayıcısına yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="5e16f-352">**storage**: Pointer to storage information container</span></span>

### <a name="return-value"></a><span data-ttu-id="5e16f-353">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="5e16f-353">Return Value</span></span>

- <span data-ttu-id="5e16f-354">**UX_SUCCESS**: (0x00) depolama bilgileri alındı</span><span class="sxs-lookup"><span data-stu-id="5e16f-354">**UX_SUCCESS**: (0x00) The storage information was retrieved</span></span>
- <span data-ttu-id="5e16f-355">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) oturum açılmadı</span><span class="sxs-lookup"><span data-stu-id="5e16f-355">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) Session not opened</span></span>
- <span data-ttu-id="5e16f-356">**UX_MEMORY_INSUFFICIENT** (0x12) Pima komutu oluşturmak için yeterli bellek yok.</span><span class="sxs-lookup"><span data-stu-id="5e16f-356">**UX_MEMORY_INSUFFICIENT** (0x12) Not enough memory to create PIMA command.</span></span>

### <a name="example"></a><span data-ttu-id="5e16f-357">Örnek</span><span class="sxs-lookup"><span data-stu-id="5e16f-357">Example</span></span>

```C
/* Get the first storage ID info container. */
status = ux_host_class_pima_storage_info_get(pima, pima_session,
    pictbridge ->ux_pictbridge_storage_ids[0],
    (UX_HOST_CLASS_PIMA_STORAGE *)pictbridge ->ux_pictbridge_storage);

if (status != UX_SUCCESS)
{
    /* Close the pima session. */
    status = ux_host_class_pima_session_close(pictbridge ->
        ux_pictbridge_pima, pima_session);
    return(UX_PICTBRIDGE_ERROR_STORE_NOT_AVAILABLE);
}
```

## <a name="ux_host_class_pima_num_objects_get"></a><span data-ttu-id="5e16f-358">ux_host_class_pima_num_objects_get</span><span class="sxs-lookup"><span data-stu-id="5e16f-358">ux_host_class_pima_num_objects_get</span></span>

<span data-ttu-id="5e16f-359">Yanıtlayıcı 'dan bir depolama kapsayıcısındaki nesne sayısını alın.</span><span class="sxs-lookup"><span data-stu-id="5e16f-359">Obtain the number of objects on a storage container from Responder.</span></span>

### <a name="prototype"></a><span data-ttu-id="5e16f-360">Prototype</span><span class="sxs-lookup"><span data-stu-id="5e16f-360">Prototype</span></span>

```C
UINT ux_host_class_pima_num_objects_get(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    ULONG storage_id,
    ULONG object_format_code)
```

### <a name="description"></a><span data-ttu-id="5e16f-361">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5e16f-361">Description</span></span>

<span data-ttu-id="5e16f-362">Bu işlev, belirli bir biçim kodu ile eşleşen storage_id belirli bir depolama kapsayıcısında depolanan nesne sayısını alır.</span><span class="sxs-lookup"><span data-stu-id="5e16f-362">This function obtains the number of objects stored on a specific storage container of value storage_id matching a specific format code.</span></span> <span data-ttu-id="5e16f-363">Nesne sayısı, pima_session yapısının ux_host_class_pima_session_nb_objects: alanına döndürülür.</span><span class="sxs-lookup"><span data-stu-id="5e16f-363">The number of objects is returned in the field: ux_host_class_pima_session_nb_objects of the pima_session structure.</span></span>

### <a name="parameters"></a><span data-ttu-id="5e16f-364">Parametreler</span><span class="sxs-lookup"><span data-stu-id="5e16f-364">Parameters</span></span>

- <span data-ttu-id="5e16f-365">**Pima**: Pima sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-365">**pima**: Pointer to the pima class instance.</span></span>
- <span data-ttu-id="5e16f-366">**pima_session**: Pima oturumuna yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="5e16f-366">**pima_session**: Pointer to PIMA session</span></span>
- <span data-ttu-id="5e16f-367">**storage_id**: depolama kapsayıcısının kimliği</span><span class="sxs-lookup"><span data-stu-id="5e16f-367">**storage_id**: ID of the storage container</span></span>
- <span data-ttu-id="5e16f-368">**object_format_code**: nesne biçimi kodu filtresi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-368">**object_format_code**: Objects format code filter.</span></span>

<span data-ttu-id="5e16f-369">Nesne biçim kodları aşağıdaki değerlerden birine sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="5e16f-369">The Object Format Codes can have one of the following values.</span></span>

| <span data-ttu-id="5e16f-370">Nesne biçim kodu</span><span class="sxs-lookup"><span data-stu-id="5e16f-370">Object Format Code</span></span>               | <span data-ttu-id="5e16f-371">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5e16f-371">Description</span></span>   |     <span data-ttu-id="5e16f-372">USBX kodu</span><span class="sxs-lookup"><span data-stu-id="5e16f-372">USBX code</span></span>                          |
|----------------------------------|---------------|------------------------------------------|
| <span data-ttu-id="5e16f-373">0x3000</span><span class="sxs-lookup"><span data-stu-id="5e16f-373">0x3000</span></span>                           | <span data-ttu-id="5e16f-374">Tanımsız tanımsız görüntü olmayan nesne</span><span class="sxs-lookup"><span data-stu-id="5e16f-374">Undefined Undefined non-image object</span></span> | <span data-ttu-id="5e16f-375">UX_HOST_CLASS_PIMA_OFC_UNDEFINED</span><span class="sxs-lookup"><span data-stu-id="5e16f-375">UX_HOST_CLASS_PIMA_OFC_UNDEFINED</span></span>   |
| <span data-ttu-id="5e16f-376">0x3001</span><span class="sxs-lookup"><span data-stu-id="5e16f-376">0x3001</span></span>                           | <span data-ttu-id="5e16f-377">İlişki Ilişkilendirmesi (ör. klasörü)</span><span class="sxs-lookup"><span data-stu-id="5e16f-377">Association Association (e.g. folder)</span></span> | <span data-ttu-id="5e16f-378">UX_HOST_CLASS_PIMA_OFC_ASSOCIATION</span><span class="sxs-lookup"><span data-stu-id="5e16f-378">UX_HOST_CLASS_PIMA_OFC_ASSOCIATION</span></span> |
| <span data-ttu-id="5e16f-379">0x3002</span><span class="sxs-lookup"><span data-stu-id="5e16f-379">0x3002</span></span>                           | <span data-ttu-id="5e16f-380">Betik cihazı-modele özgü betik</span><span class="sxs-lookup"><span data-stu-id="5e16f-380">Script Device-model specific script</span></span> | <span data-ttu-id="5e16f-381">UX_HOST_CLASS_PIMA_OFC_SCRIPT</span><span class="sxs-lookup"><span data-stu-id="5e16f-381">UX_HOST_CLASS_PIMA_OFC_SCRIPT</span></span>      |
| <span data-ttu-id="5e16f-382">0x3003</span><span class="sxs-lookup"><span data-stu-id="5e16f-382">0x3003</span></span>                           | <span data-ttu-id="5e16f-383">Yürütülebilir cihaz modeline özgü ikili yürütülebilir dosya</span><span class="sxs-lookup"><span data-stu-id="5e16f-383">Executable Device model-specific binary executable</span></span> | <span data-ttu-id="5e16f-384">UX_HOST_CLASS_PIMA_OFC_EXECUTABLE</span><span class="sxs-lookup"><span data-stu-id="5e16f-384">UX_HOST_CLASS_PIMA_OFC_EXECUTABLE</span></span>  |
| <span data-ttu-id="5e16f-385">0x3004</span><span class="sxs-lookup"><span data-stu-id="5e16f-385">0x3004</span></span>                           | <span data-ttu-id="5e16f-386">Metin metin dosyası</span><span class="sxs-lookup"><span data-stu-id="5e16f-386">Text Text file</span></span>  |   <span data-ttu-id="5e16f-387">UX_HOST_CLASS_PIMA_OFC_TEXT</span><span class="sxs-lookup"><span data-stu-id="5e16f-387">UX_HOST_CLASS_PIMA_OFC_TEXT</span></span>        |
| <span data-ttu-id="5e16f-388">0x3005</span><span class="sxs-lookup"><span data-stu-id="5e16f-388">0x3005</span></span>                           | <span data-ttu-id="5e16f-389">HTML köprü metni biçimlendirme dili dosyası (metin)</span><span class="sxs-lookup"><span data-stu-id="5e16f-389">HTML HyperText Markup Language file (text)</span></span> | <span data-ttu-id="5e16f-390">UX_HOST_CLASS_PIMA_OFC_HTML</span><span class="sxs-lookup"><span data-stu-id="5e16f-390">UX_HOST_CLASS_PIMA_OFC_HTML</span></span>        |
| <span data-ttu-id="5e16f-391">0x3006</span><span class="sxs-lookup"><span data-stu-id="5e16f-391">0x3006</span></span>                           | <span data-ttu-id="5e16f-392">DPOF dijital yazdırma sırası biçim dosyası (metin)</span><span class="sxs-lookup"><span data-stu-id="5e16f-392">DPOF Digital Print Order Format file (text)</span></span> | <span data-ttu-id="5e16f-393">UX_HOST_CLASS_PIMA_OFC_DPOF</span><span class="sxs-lookup"><span data-stu-id="5e16f-393">UX_HOST_CLASS_PIMA_OFC_DPOF</span></span>        |
| <span data-ttu-id="5e16f-394">0x3007</span><span class="sxs-lookup"><span data-stu-id="5e16f-394">0x3007</span></span>                           | <span data-ttu-id="5e16f-395">AıFF ses klibi</span><span class="sxs-lookup"><span data-stu-id="5e16f-395">AIFF Audio clip</span></span>  |  <span data-ttu-id="5e16f-396">UX_HOST_CLASS_PIMA_OFC_AIFF</span><span class="sxs-lookup"><span data-stu-id="5e16f-396">UX_HOST_CLASS_PIMA_OFC_AIFF</span></span>        |
| <span data-ttu-id="5e16f-397">0x3008</span><span class="sxs-lookup"><span data-stu-id="5e16f-397">0x3008</span></span>                           | <span data-ttu-id="5e16f-398">WAV ses klibi</span><span class="sxs-lookup"><span data-stu-id="5e16f-398">WAV Audio clip</span></span>   |  <span data-ttu-id="5e16f-399">UX_HOST_CLASS_PIMA_OFC_WAV</span><span class="sxs-lookup"><span data-stu-id="5e16f-399">UX_HOST_CLASS_PIMA_OFC_WAV</span></span>         |
| <span data-ttu-id="5e16f-400">0x3009</span><span class="sxs-lookup"><span data-stu-id="5e16f-400">0x3009</span></span>                           | <span data-ttu-id="5e16f-401">MP3 ses klibi</span><span class="sxs-lookup"><span data-stu-id="5e16f-401">MP3 Audio clip</span></span>   |  <span data-ttu-id="5e16f-402">UX_HOST_CLASS_PIMA_OFC_MP3</span><span class="sxs-lookup"><span data-stu-id="5e16f-402">UX_HOST_CLASS_PIMA_OFC_MP3</span></span>         |
| <span data-ttu-id="5e16f-403">0x300A</span><span class="sxs-lookup"><span data-stu-id="5e16f-403">0x300A</span></span>                           | <span data-ttu-id="5e16f-404">AVI video klibi</span><span class="sxs-lookup"><span data-stu-id="5e16f-404">AVI Video clip</span></span>   |  <span data-ttu-id="5e16f-405">UX_HOST_CLASS_PIMA_OFC_AVI</span><span class="sxs-lookup"><span data-stu-id="5e16f-405">UX_HOST_CLASS_PIMA_OFC_AVI</span></span>         |
| <span data-ttu-id="5e16f-406">0x300B</span><span class="sxs-lookup"><span data-stu-id="5e16f-406">0x300B</span></span>                           | <span data-ttu-id="5e16f-407">MPEG video klibi</span><span class="sxs-lookup"><span data-stu-id="5e16f-407">MPEG Video clip</span></span>  |  <span data-ttu-id="5e16f-408">UX_HOST_CLASS_PIMA_OFC_MPEG</span><span class="sxs-lookup"><span data-stu-id="5e16f-408">UX_HOST_CLASS_PIMA_OFC_MPEG</span></span>        |
| <span data-ttu-id="5e16f-409">0x300C</span><span class="sxs-lookup"><span data-stu-id="5e16f-409">0x300C</span></span>                           | <span data-ttu-id="5e16f-410">ASF Microsoft Gelişmiş akış biçimi (video)</span><span class="sxs-lookup"><span data-stu-id="5e16f-410">ASF Microsoft Advanced Streaming Format (video)</span></span> | <span data-ttu-id="5e16f-411">UX_HOST_CLASS_PIMA_OFC_ASF</span><span class="sxs-lookup"><span data-stu-id="5e16f-411">UX_HOST_CLASS_PIMA_OFC_ASF</span></span>         |
| <span data-ttu-id="5e16f-412">0x3800</span><span class="sxs-lookup"><span data-stu-id="5e16f-412">0x3800</span></span>                           | <span data-ttu-id="5e16f-413">Tanımsız bilinmeyen görüntü nesnesi</span><span class="sxs-lookup"><span data-stu-id="5e16f-413">Undefined Unknown image object</span></span> | <span data-ttu-id="5e16f-414">UX_HOST_CLASS_PIMA_OFC_QT</span><span class="sxs-lookup"><span data-stu-id="5e16f-414">UX_HOST_CLASS_PIMA_OFC_QT</span></span>          |
| <span data-ttu-id="5e16f-415">0x3801</span><span class="sxs-lookup"><span data-stu-id="5e16f-415">0x3801</span></span>                           | <span data-ttu-id="5e16f-416">EXIF/JPEG takas edilebilir dosya biçimi, JEIDA standart</span><span class="sxs-lookup"><span data-stu-id="5e16f-416">EXIF/JPEG Exchangeable File Format, JEIDA standard</span></span> | <span data-ttu-id="5e16f-417">UX_HOST_CLASS_PIMA_OFC_EXIF_JPEG</span><span class="sxs-lookup"><span data-stu-id="5e16f-417">UX_HOST_CLASS_PIMA_OFC_EXIF_JPEG</span></span>   |
| <span data-ttu-id="5e16f-418">0x3802</span><span class="sxs-lookup"><span data-stu-id="5e16f-418">0x3802</span></span>                           | <span data-ttu-id="5e16f-419">Elektronik Fotoğrafçılık için TIFF/EP etiketi resim dosyası biçimi</span><span class="sxs-lookup"><span data-stu-id="5e16f-419">TIFF/EP Tag Image File Format for Electronic Photography</span></span> | <span data-ttu-id="5e16f-420">UX_HOST_CLASS_PIMA_OFC_TIFF_EP</span><span class="sxs-lookup"><span data-stu-id="5e16f-420">UX_HOST_CLASS_PIMA_OFC_TIFF_EP</span></span>     |
| <span data-ttu-id="5e16f-421">0x3803</span><span class="sxs-lookup"><span data-stu-id="5e16f-421">0x3803</span></span>                           | <span data-ttu-id="5e16f-422">FlashPix yapılandırılmış depolama görüntü biçimi</span><span class="sxs-lookup"><span data-stu-id="5e16f-422">FlashPix Structured Storage Image Format</span></span> | <span data-ttu-id="5e16f-423">UX_HOST_CLASS_PIMA_OFC_FLASHPIX</span><span class="sxs-lookup"><span data-stu-id="5e16f-423">UX_HOST_CLASS_PIMA_OFC_FLASHPIX</span></span>    |
| <span data-ttu-id="5e16f-424">0x3804</span><span class="sxs-lookup"><span data-stu-id="5e16f-424">0x3804</span></span>                           | <span data-ttu-id="5e16f-425">BMP Microsoft Windows bit eşlem dosyası</span><span class="sxs-lookup"><span data-stu-id="5e16f-425">BMP Microsoft Windows Bitmap file</span></span> | <span data-ttu-id="5e16f-426">UX_HOST_CLASS_PIMA_OFC_BMP</span><span class="sxs-lookup"><span data-stu-id="5e16f-426">UX_HOST_CLASS_PIMA_OFC_BMP</span></span>         |
| <span data-ttu-id="5e16f-427">0x3805</span><span class="sxs-lookup"><span data-stu-id="5e16f-427">0x3805</span></span>                           | <span data-ttu-id="5e16f-428">CFF Canon kamera resim dosyası biçimi</span><span class="sxs-lookup"><span data-stu-id="5e16f-428">CIFF Canon Camera Image File Format</span></span> | <span data-ttu-id="5e16f-429">UX_HOST_CLASS_PIMA_OFC_CIFF</span><span class="sxs-lookup"><span data-stu-id="5e16f-429">UX_HOST_CLASS_PIMA_OFC_CIFF</span></span>        |
| <span data-ttu-id="5e16f-430">0x3806</span><span class="sxs-lookup"><span data-stu-id="5e16f-430">0x3806</span></span>                           | <span data-ttu-id="5e16f-431">Tanımsız ayrılmış</span><span class="sxs-lookup"><span data-stu-id="5e16f-431">Undefined Reserved</span></span> |  |
| <span data-ttu-id="5e16f-432">0x3807</span><span class="sxs-lookup"><span data-stu-id="5e16f-432">0x3807</span></span>                           | <span data-ttu-id="5e16f-433">GIF Grafik Değişim Biçimi</span><span class="sxs-lookup"><span data-stu-id="5e16f-433">GIF Graphics Interchange Format</span></span> | <span data-ttu-id="5e16f-434">UX_HOST_CLASS_PIMA_OFC_GIF</span><span class="sxs-lookup"><span data-stu-id="5e16f-434">UX_HOST_CLASS_PIMA_OFC_GIF</span></span>         |
| <span data-ttu-id="5e16f-435">0x3808</span><span class="sxs-lookup"><span data-stu-id="5e16f-435">0x3808</span></span>                           | <span data-ttu-id="5e16f-436">JJPEG dosya değişim biçimi</span><span class="sxs-lookup"><span data-stu-id="5e16f-436">JFIF JPEG File Interchange Format</span></span> | <span data-ttu-id="5e16f-437">UX_HOST_CLASS_PIMA_OFC_JFIF</span><span class="sxs-lookup"><span data-stu-id="5e16f-437">UX_HOST_CLASS_PIMA_OFC_JFIF</span></span>        |
| <span data-ttu-id="5e16f-438">0x3809</span><span class="sxs-lookup"><span data-stu-id="5e16f-438">0x3809</span></span>                           | <span data-ttu-id="5e16f-439">PCD PhotoCD Image Pac</span><span class="sxs-lookup"><span data-stu-id="5e16f-439">PCD PhotoCD Image Pac</span></span> | <span data-ttu-id="5e16f-440">UX_HOST_CLASS_PIMA_OFC_PCD</span><span class="sxs-lookup"><span data-stu-id="5e16f-440">UX_HOST_CLASS_PIMA_OFC_PCD</span></span>         |
| <span data-ttu-id="5e16f-441">0x380A</span><span class="sxs-lookup"><span data-stu-id="5e16f-441">0x380A</span></span>                           | <span data-ttu-id="5e16f-442">PICT QuickDraw resim biçimi</span><span class="sxs-lookup"><span data-stu-id="5e16f-442">PICT Quickdraw Image Format</span></span> | <span data-ttu-id="5e16f-443">UX_HOST_CLASS_PIMA_OFC_PICT</span><span class="sxs-lookup"><span data-stu-id="5e16f-443">UX_HOST_CLASS_PIMA_OFC_PICT</span></span>        |
| <span data-ttu-id="5e16f-444">0x380B</span><span class="sxs-lookup"><span data-stu-id="5e16f-444">0x380B</span></span>                           | <span data-ttu-id="5e16f-445">PNG Taşınabilir Ağ Grafikleri</span><span class="sxs-lookup"><span data-stu-id="5e16f-445">PNG Portable Network Graphics</span></span> | <span data-ttu-id="5e16f-446">UX_HOST_CLASS_PIMA_OFC_PNG</span><span class="sxs-lookup"><span data-stu-id="5e16f-446">UX_HOST_CLASS_PIMA_OFC_PNG</span></span>         |
| <span data-ttu-id="5e16f-447">0x380C</span><span class="sxs-lookup"><span data-stu-id="5e16f-447">0x380C</span></span>                           | <span data-ttu-id="5e16f-448">Tanımsız ayrılmış</span><span class="sxs-lookup"><span data-stu-id="5e16f-448">Undefined Reserved</span></span> |   |
| <span data-ttu-id="5e16f-449">0x380D</span><span class="sxs-lookup"><span data-stu-id="5e16f-449">0x380D</span></span>                           | <span data-ttu-id="5e16f-450">TIFF etiketi resim dosyası biçimi</span><span class="sxs-lookup"><span data-stu-id="5e16f-450">TIFF Tag Image File Format</span></span> | <span data-ttu-id="5e16f-451">UX_HOST_CLASS_PIMA_OFC_TIFF</span><span class="sxs-lookup"><span data-stu-id="5e16f-451">UX_HOST_CLASS_PIMA_OFC_TIFF</span></span>        |
| <span data-ttu-id="5e16f-452">0x380E</span><span class="sxs-lookup"><span data-stu-id="5e16f-452">0x380E</span></span>                           | <span data-ttu-id="5e16f-453">Bilgi teknolojisi için TIFF/It etiketi görüntü dosyası biçimi (grafik sanatları)</span><span class="sxs-lookup"><span data-stu-id="5e16f-453">TIFF/IT Tag Image File Format for Information Technology (graphic arts)</span></span> | <span data-ttu-id="5e16f-454">UX_HOST_CLASS_PIMA_OFC_TIFF_IT</span><span class="sxs-lookup"><span data-stu-id="5e16f-454">UX_HOST_CLASS_PIMA_OFC_TIFF_IT</span></span>     |
| <span data-ttu-id="5e16f-455">0x380F</span><span class="sxs-lookup"><span data-stu-id="5e16f-455">0x380F</span></span>                           | <span data-ttu-id="5e16f-456">JP2 JPEG2000 ana hat dosyası biçimi</span><span class="sxs-lookup"><span data-stu-id="5e16f-456">JP2 JPEG2000 Baseline File Format</span></span> | <span data-ttu-id="5e16f-457">UX_HOST_CLASS_PIMA_OFC_JP2</span><span class="sxs-lookup"><span data-stu-id="5e16f-457">UX_HOST_CLASS_PIMA_OFC_JP2</span></span>         |
| <span data-ttu-id="5e16f-458">0x3810</span><span class="sxs-lookup"><span data-stu-id="5e16f-458">0x3810</span></span>                           | <span data-ttu-id="5e16f-459">JPX JPEG2000 genişletilmiş dosya biçimi</span><span class="sxs-lookup"><span data-stu-id="5e16f-459">JPX JPEG2000 Extended File Format</span></span> | <span data-ttu-id="5e16f-460">UX_HOST_CLASS_PIMA_OFC_JPX</span><span class="sxs-lookup"><span data-stu-id="5e16f-460">UX_HOST_CLASS_PIMA_OFC_JPX</span></span>         |
| <span data-ttu-id="5e16f-461">0011 MSN ile diğer tüm kodlar</span><span class="sxs-lookup"><span data-stu-id="5e16f-461">All other codes with MSN of 0011</span></span> | <span data-ttu-id="5e16f-462">Gelecekte kullanılmak üzere hiçbir tanımsız ayrılmış</span><span class="sxs-lookup"><span data-stu-id="5e16f-462">Any Undefined Reserved for future use</span></span> |                                    |
| <span data-ttu-id="5e16f-463">MSN 1011 ile diğer tüm kodlar</span><span class="sxs-lookup"><span data-stu-id="5e16f-463">All other codes with MSN of 1011</span></span> | <span data-ttu-id="5e16f-464">Satıcı tanımlı satıcı tanımlı tür: görüntü</span><span class="sxs-lookup"><span data-stu-id="5e16f-464">Any Vendor-Defined Vendor-Defined type: Image</span></span> |                                    |

### <a name="return-value"></a><span data-ttu-id="5e16f-465">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="5e16f-465">Return Value</span></span>

- <span data-ttu-id="5e16f-466">**UX_SUCCESS**: (0x00) veri aktarımı tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="5e16f-466">**UX_SUCCESS**: (0x00) The data transfer was completed.</span></span>
- <span data-ttu-id="5e16f-467">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) oturum açılmadı</span><span class="sxs-lookup"><span data-stu-id="5e16f-467">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) Session not opened</span></span>
- <span data-ttu-id="5e16f-468">**UX_MEMORY_INSUFFICIENT**: (0x12) Pima komutu oluşturmak için yeterli bellek yok.</span><span class="sxs-lookup"><span data-stu-id="5e16f-468">**UX_MEMORY_INSUFFICIENT**: (0x12) Not enough memory to create PIMA command.</span></span>

### <a name="example"></a><span data-ttu-id="5e16f-469">Örnek</span><span class="sxs-lookup"><span data-stu-id="5e16f-469">Example</span></span>

```C
/* Get the number of objects on all containers matching a SCRIPT object. */
status = ux_host_class_pima_num_objects_get(pima, pima_session,
    UX_PICTBRIDGE_ALL_CONTAINERS, UX_PICTBRIDGE_OBJECT_SCRIPT);

if (status != UX_SUCCESS)
{
    /* Close the pima session. */
    status = ux_**host_class_pima_session_close(pima, pima_session);

    return(UX_PICTBRIDGE_ERROR_STORE_NOT_AVAILABLE);
} else
    /* The number of objects is returned in the field: pima_session -> ux_host_class_pima_session_nb_objects */
```

## <a name="ux_host_class_pima_object_handles_get"></a><span data-ttu-id="5e16f-470">ux_host_class_pima_object_handles_get</span><span class="sxs-lookup"><span data-stu-id="5e16f-470">ux_host_class_pima_object_handles_get</span></span>

<span data-ttu-id="5e16f-471">Yanıtlayanın nesne tutamaçlarını alın.</span><span class="sxs-lookup"><span data-stu-id="5e16f-471">Obtain object handles from Responder.</span></span>

### <a name="prototype"></a><span data-ttu-id="5e16f-472">Prototype</span><span class="sxs-lookup"><span data-stu-id="5e16f-472">Prototype</span></span>

```C
UINT ux_host_class_pima_object_handles_get(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    ULONG *object_handles_array,
    ULONG object_handles_length,
    ULONG storage_id,
    ULONG object_format_code,
    ULONG object_handle_association)
```

### <a name="description"></a><span data-ttu-id="5e16f-473">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5e16f-473">Description</span></span>

<span data-ttu-id="5e16f-474">Storage_id parametresiyle belirtilen depolama kapsayıcısında bulunan nesne tanıtıcılarının dizisini döndürür.</span><span class="sxs-lookup"><span data-stu-id="5e16f-474">Returns an array of Object Handles present in the storage container indicated by the storage_id parameter.</span></span> <span data-ttu-id="5e16f-475">Tüm mağazaların içindeki toplanmış bir liste isteniyorsa, bu değer 0xFFFFFFFF olarak ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5e16f-475">If an aggregated list across all stores is desired, this value shall be set to 0xFFFFFFFF.</span></span>

### <a name="parameters"></a><span data-ttu-id="5e16f-476">Parametreler</span><span class="sxs-lookup"><span data-stu-id="5e16f-476">Parameters</span></span>

- <span data-ttu-id="5e16f-477">**Pima**: Pima sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-477">**pima**: Pointer to the pima class instance.</span></span>
- <span data-ttu-id="5e16f-478">**pima_session**: Pima oturumuna yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="5e16f-478">**pima_session**: Pointer to PIMA session</span></span>
- <span data-ttu-id="5e16f-479">**object_handes_array**: tanıtıcıların döndürüldüğü dizi</span><span class="sxs-lookup"><span data-stu-id="5e16f-479">**object_handes_array**: Array where handles are returned</span></span>
- <span data-ttu-id="5e16f-480">**object_handles_length**: dizinin uzunluğu</span><span class="sxs-lookup"><span data-stu-id="5e16f-480">**object_handles_length**: Length of the array</span></span>
- <span data-ttu-id="5e16f-481">**storage_id**: depolama kapsayıcısının kimliği</span><span class="sxs-lookup"><span data-stu-id="5e16f-481">**storage_id**: ID of the storage container</span></span>
- <span data-ttu-id="5e16f-482">**object_format_code**: nesne için biçim kodu (bkz. işlev için tablo ux_host_class_pima_num_objects_get)</span><span class="sxs-lookup"><span data-stu-id="5e16f-482">**object_format_code**: Format code for object (see table for function ux_host_class_pima_num_objects_get)</span></span>
- <span data-ttu-id="5e16f-483">**object_handle_association**: isteğe bağlı nesne ilişkilendirme değeri</span><span class="sxs-lookup"><span data-stu-id="5e16f-483">**object_handle_association**: Optional object association value</span></span>

<span data-ttu-id="5e16f-484">Nesne tanıtıcısı ilişkilendirmesi aşağıdaki tablodaki değerden biri olabilir:</span><span class="sxs-lookup"><span data-stu-id="5e16f-484">The object handle association can be one of the value from the table below:</span></span>

| <span data-ttu-id="5e16f-485">Ilişki kodu</span><span class="sxs-lookup"><span data-stu-id="5e16f-485">AssociationCode</span></span>                        | <span data-ttu-id="5e16f-486">AssociationType</span><span class="sxs-lookup"><span data-stu-id="5e16f-486">AssociationType</span></span>      | <span data-ttu-id="5e16f-487">Yorum</span><span class="sxs-lookup"><span data-stu-id="5e16f-487">Interpretation</span></span>       |
|----------------------------------------|----------------------|----------------------|
| <span data-ttu-id="5e16f-488">0x0000</span><span class="sxs-lookup"><span data-stu-id="5e16f-488">0x0000</span></span>                                 | <span data-ttu-id="5e16f-489">Tanımlayan</span><span class="sxs-lookup"><span data-stu-id="5e16f-489">Undefined</span></span>            | <span data-ttu-id="5e16f-490">Tanımlayan</span><span class="sxs-lookup"><span data-stu-id="5e16f-490">Undefined</span></span>            |
| <span data-ttu-id="5e16f-491">0x0001</span><span class="sxs-lookup"><span data-stu-id="5e16f-491">0x0001</span></span>                                 | <span data-ttu-id="5e16f-492">GenericFolder</span><span class="sxs-lookup"><span data-stu-id="5e16f-492">GenericFolder</span></span>        | <span data-ttu-id="5e16f-493">Kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="5e16f-493">Unused</span></span>               |
| <span data-ttu-id="5e16f-494">0x0002</span><span class="sxs-lookup"><span data-stu-id="5e16f-494">0x0002</span></span>                                 | <span data-ttu-id="5e16f-495">Albümün</span><span class="sxs-lookup"><span data-stu-id="5e16f-495">Album</span></span>                | <span data-ttu-id="5e16f-496">Ayrılmıştır</span><span class="sxs-lookup"><span data-stu-id="5e16f-496">Reserved</span></span>             |
| <span data-ttu-id="5e16f-497">0x0003</span><span class="sxs-lookup"><span data-stu-id="5e16f-497">0x0003</span></span>                                 | <span data-ttu-id="5e16f-498">TimeSequence</span><span class="sxs-lookup"><span data-stu-id="5e16f-498">TimeSequence</span></span>         | <span data-ttu-id="5e16f-499">DefaultPlaybackDelta</span><span class="sxs-lookup"><span data-stu-id="5e16f-499">DefaultPlaybackDelta</span></span> |
| <span data-ttu-id="5e16f-500">0x0004</span><span class="sxs-lookup"><span data-stu-id="5e16f-500">0x0004</span></span>                                 | <span data-ttu-id="5e16f-501">Horizontalpanoramik</span><span class="sxs-lookup"><span data-stu-id="5e16f-501">HorizontalPanoramic</span></span>  | <span data-ttu-id="5e16f-502">Kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="5e16f-502">Unused</span></span>               |
| <span data-ttu-id="5e16f-503">0x0005</span><span class="sxs-lookup"><span data-stu-id="5e16f-503">0x0005</span></span>                                 | <span data-ttu-id="5e16f-504">Verticalpanoramik</span><span class="sxs-lookup"><span data-stu-id="5e16f-504">VerticalPanoramic</span></span>    | <span data-ttu-id="5e16f-505">Kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="5e16f-505">Unused</span></span>               |
| <span data-ttu-id="5e16f-506">0x0006</span><span class="sxs-lookup"><span data-stu-id="5e16f-506">0x0006</span></span>                                 | <span data-ttu-id="5e16f-507">2Dpanoramik</span><span class="sxs-lookup"><span data-stu-id="5e16f-507">2DPanoramic</span></span>          | <span data-ttu-id="5e16f-508">Imaperrow</span><span class="sxs-lookup"><span data-stu-id="5e16f-508">ImagesPerRow</span></span>         |
| <span data-ttu-id="5e16f-509">0x0007</span><span class="sxs-lookup"><span data-stu-id="5e16f-509">0x0007</span></span>                                 | <span data-ttu-id="5e16f-510">Anlari verileri</span><span class="sxs-lookup"><span data-stu-id="5e16f-510">AncillaryData</span></span>        | <span data-ttu-id="5e16f-511">Tanımlayan</span><span class="sxs-lookup"><span data-stu-id="5e16f-511">Undefined</span></span>            |
| <span data-ttu-id="5e16f-512">Bit 15 olan diğer tüm değerler 0 olarak ayarlanmıştır</span><span class="sxs-lookup"><span data-stu-id="5e16f-512">All other values with bit 15 set to 0</span></span>  | <span data-ttu-id="5e16f-513">Ayrılmıştır</span><span class="sxs-lookup"><span data-stu-id="5e16f-513">Reserved</span></span>             | <span data-ttu-id="5e16f-514">Tanımlayan</span><span class="sxs-lookup"><span data-stu-id="5e16f-514">Undefined</span></span>            |
| <span data-ttu-id="5e16f-515">Bit 15 olan tüm değerler 1 olarak ayarlanmıştır</span><span class="sxs-lookup"><span data-stu-id="5e16f-515">All values with bit 15 set to 1</span></span>        | <span data-ttu-id="5e16f-516">Satıcı tanımlı</span><span class="sxs-lookup"><span data-stu-id="5e16f-516">Vendor-Defined</span></span>       | <span data-ttu-id="5e16f-517">Satıcı tanımlı</span><span class="sxs-lookup"><span data-stu-id="5e16f-517">Vendor-Defined</span></span>       |

### <a name="return-value"></a><span data-ttu-id="5e16f-518">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="5e16f-518">Return Value</span></span>

- <span data-ttu-id="5e16f-519">**UX_SUCCESS**: (0x00) veri aktarımı tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="5e16f-519">**UX_SUCCESS**: (0x00) The data transfer was completed.</span></span>
- <span data-ttu-id="5e16f-520">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) oturum açılmadı</span><span class="sxs-lookup"><span data-stu-id="5e16f-520">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) Session not opened</span></span>
- <span data-ttu-id="5e16f-521">**UX_MEMORY_INSUFFICIENT**: (0x12) Pima komutu oluşturmak için yeterli bellek yok.</span><span class="sxs-lookup"><span data-stu-id="5e16f-521">**UX_MEMORY_INSUFFICIENT**: (0x12) Not enough memory to create PIMA command.</span></span>

### <a name="example"></a><span data-ttu-id="5e16f-522">Örnek</span><span class="sxs-lookup"><span data-stu-id="5e16f-522">Example</span></span>

```C
/* Get the array of objects handles on the container. */
status = ux_**host_class_pima_object_handles_get(pima, pima_session,
    pictbridge ->ux_pictbridge_object_handles_array,
    4 * pima_session ->ux_host_class_pima_session_nb_objects,
    UX_PICTBRIDGE_ALL_CONTAINERS,
    UX_PICTBRIDGE_OBJECT_SCRIPT, 0);

if (status != UX_SUCCESS)
{
    /* Close the pima session. */
    status = ux_host_class_pima_session_close(pima, pima_session);
    return(UX_PICTBRIDGE_ERROR_STORE_NOT_AVAILABLE);
}
```

## <a name="ux_host_class_pima_object_info_get"></a><span data-ttu-id="5e16f-523">ux_host_class_pima_object_info_get</span><span class="sxs-lookup"><span data-stu-id="5e16f-523">ux_host_class_pima_object_info_get</span></span>

<span data-ttu-id="5e16f-524">Yanıtlayanın nesne bilgilerini alın.</span><span class="sxs-lookup"><span data-stu-id="5e16f-524">Obtain the object information from Responder.</span></span>

### <a name="prototype"></a><span data-ttu-id="5e16f-525">Prototype</span><span class="sxs-lookup"><span data-stu-id="5e16f-525">Prototype</span></span>

```C
UINT ux_host_class_pima_object_info_get(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    ULONG object_handle,
    UX_HOST_CLASS_PIMA_OBJECT *object)
```

### <a name="description"></a><span data-ttu-id="5e16f-526">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5e16f-526">Description</span></span>

<span data-ttu-id="5e16f-527">Bu işlev, nesne tanıtıcısı için nesne bilgilerini edinir.</span><span class="sxs-lookup"><span data-stu-id="5e16f-527">This function obtains the object information for an object handle.</span></span>

### <a name="parameters"></a><span data-ttu-id="5e16f-528">Parametreler</span><span class="sxs-lookup"><span data-stu-id="5e16f-528">Parameters</span></span>

- <span data-ttu-id="5e16f-529">**Pima**: Pima sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-529">**pima**: Pointer to the pima class instance.</span></span>
- <span data-ttu-id="5e16f-530">**pima_session**: Pima oturumuna yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="5e16f-530">**pima_session**: Pointer to PIMA session</span></span>
- <span data-ttu-id="5e16f-531">**object_handle**: nesnenin tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="5e16f-531">**object_handle**: Handle of the object</span></span>
- <span data-ttu-id="5e16f-532">**nesne**: nesne bilgisi kapsayıcısının işaretçisi</span><span class="sxs-lookup"><span data-stu-id="5e16f-532">**object**: Pointer to object information container</span></span>

### <a name="return-value"></a><span data-ttu-id="5e16f-533">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="5e16f-533">Return Value</span></span>

- <span data-ttu-id="5e16f-534">**UX_SUCCESS**: (0x00) veri aktarımı tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="5e16f-534">**UX_SUCCESS**: (0x00) The data transfer was completed.</span></span>
- <span data-ttu-id="5e16f-535">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) oturum açılmadı</span><span class="sxs-lookup"><span data-stu-id="5e16f-535">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) Session not opened</span></span>
- <span data-ttu-id="5e16f-536">**UX_MEMORY_INSUFFICIENT**: (0x12) Pima komutu oluşturmak için yeterli bellek yok.</span><span class="sxs-lookup"><span data-stu-id="5e16f-536">**UX_MEMORY_INSUFFICIENT**: (0x12) Not enough memory to create PIMA command.</span></span>

### <a name="example"></a><span data-ttu-id="5e16f-537">Örnek</span><span class="sxs-lookup"><span data-stu-id="5e16f-537">Example</span></span>

```C
/* We search for an object that is a picture or a script. */
object_index = 0;

while (object_index < pima_session -> ux_host_class_pima_session_nb_objects)
{
    /* Get the object info structure. */
    status = ux_**host_class_pima_object_info_get(pima, pima_session,
        pictbridge -> ux_pictbridge_object_handles_array[object_index], 
        pima_object);

    if (status != UX_SUCCESS)
    {
        /* Close the pima session. */
        status = ux_host_class_pima_session_close(pima, pima_session);

        return(UX_PICTBRIDGE_ERROR_INVALID_OBJECT_HANDLE );
    }
}
```

## <a name="ux_host_class_pima_object_info_send"></a><span data-ttu-id="5e16f-538">ux_host_class_pima_object_info_send</span><span class="sxs-lookup"><span data-stu-id="5e16f-538">ux_host_class_pima_object_info_send</span></span>

<span data-ttu-id="5e16f-539">Nesne bilgilerini Yanıtlayıcıya gönderin.</span><span class="sxs-lookup"><span data-stu-id="5e16f-539">Send the object information to Responder.</span></span>

### <a name="prototype"></a><span data-ttu-id="5e16f-540">Prototype</span><span class="sxs-lookup"><span data-stu-id="5e16f-540">Prototype</span></span>

```C
UINT ux_host_class_pima_object_info_send(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    ULONG storage_id,
    ULONG parent_object_id,
    UX_HOST_CLASS_PIMA_OBJECT *object)
```

### <a name="description"></a><span data-ttu-id="5e16f-541">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5e16f-541">Description</span></span>

<span data-ttu-id="5e16f-542">Bu işlev, storage_id değer bir depolama kapsayıcısı için depolama bilgilerini gönderir.</span><span class="sxs-lookup"><span data-stu-id="5e16f-542">This function sends the storage information for a storage container of value storage_id.</span></span> <span data-ttu-id="5e16f-543">Başlatıcı, bir nesneyi yanıtlayanın göndermeden önce bu komutu kullanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5e16f-543">The Initiator should use this command before sending an object to the responder.</span></span>

### <a name="parameters"></a><span data-ttu-id="5e16f-544">Parametreler</span><span class="sxs-lookup"><span data-stu-id="5e16f-544">Parameters</span></span>

- <span data-ttu-id="5e16f-545">**Pima**: Pima sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-545">**pima**: Pointer to the pima class instance.</span></span>
- <span data-ttu-id="5e16f-546">**pima_session**: Pima oturumuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-546">**pima_session**: Pointer to PIMA session.</span></span>
- <span data-ttu-id="5e16f-547">**storage_id**: hedef depolama kimliği.</span><span class="sxs-lookup"><span data-stu-id="5e16f-547">**storage_id**: Destination storage ID.</span></span>
- <span data-ttu-id="5e16f-548">**parent_object_id**: nesnenin yerleştirilmesi gereken yanıtlayana ObjectHandle.</span><span class="sxs-lookup"><span data-stu-id="5e16f-548">**parent_object_id**: Parent ObjectHandle on Responder where object should be placed.</span></span>
- <span data-ttu-id="5e16f-549">**nesne**: nesne bilgisi kapsayıcısının işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-549">**object**: Pointer to object information container.</span></span>

### <a name="return-value"></a><span data-ttu-id="5e16f-550">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="5e16f-550">Return Value</span></span>

- <span data-ttu-id="5e16f-551">**UX_SUCCESS**: (0x00) veri aktarımı tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="5e16f-551">**UX_SUCCESS**: (0x00) The data transfer was completed.</span></span>
- <span data-ttu-id="5e16f-552">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) oturum açılmadı</span><span class="sxs-lookup"><span data-stu-id="5e16f-552">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) Session not opened</span></span>
- <span data-ttu-id="5e16f-553">**UX_MEMORY_INSUFFICIENT**: (0x12) Pima komutu oluşturmak için yeterli bellek yok.</span><span class="sxs-lookup"><span data-stu-id="5e16f-553">**UX_MEMORY_INSUFFICIENT**: (0x12) Not enough memory to create PIMA command.</span></span>

### <a name="example"></a><span data-ttu-id="5e16f-554">Örnek</span><span class="sxs-lookup"><span data-stu-id="5e16f-554">Example</span></span>

```C
/* Send a script info. */
status = ux_host_class_pima_object_info_send(pima, pima_session,
    0, 0, pima_object);

if (status != UX_SUCCESS)
{
    /* Close the pima session. */
    status = ux_host_class_pima_session_close(pima, pima_session);

    return(UX_ERROR);
}
```

## <a name="ux_host_class_pima_object_open"></a><span data-ttu-id="5e16f-555">ux_host_class_pima_object_open</span><span class="sxs-lookup"><span data-stu-id="5e16f-555">ux_host_class_pima_object_open</span></span>

<span data-ttu-id="5e16f-556">Yanıtlayanda depolanan bir nesneyi açın.</span><span class="sxs-lookup"><span data-stu-id="5e16f-556">Open an object stored in the Responder.</span></span>

### <a name="prototype"></a><span data-ttu-id="5e16f-557">Prototype</span><span class="sxs-lookup"><span data-stu-id="5e16f-557">Prototype</span></span>

```C
UINT ux_host_class_pima_object_open(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    ULONG object_handle,
    UX_HOST_CLASS_PIMA_OBJECT *object)
```

### <a name="description"></a><span data-ttu-id="5e16f-558">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5e16f-558">Description</span></span>

<span data-ttu-id="5e16f-559">Bu işlev, okumadan veya yazmadan önce Yanıtlayıcı üzerinde bir nesne açar.</span><span class="sxs-lookup"><span data-stu-id="5e16f-559">This function opens an object on the responder before reading or writing.</span></span>

### <a name="parameters"></a><span data-ttu-id="5e16f-560">Parametreler</span><span class="sxs-lookup"><span data-stu-id="5e16f-560">Parameters</span></span>

- <span data-ttu-id="5e16f-561">**Pima**: Pima sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-561">**pima**: Pointer to the pima class instance.</span></span>
- <span data-ttu-id="5e16f-562">**pima_session**: Pima oturumuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-562">**pima_session**: Pointer to PIMA session.</span></span>
- <span data-ttu-id="5e16f-563">**object_handle**: nesnenin tanıtıcısı.</span><span class="sxs-lookup"><span data-stu-id="5e16f-563">**object_handle**: handle of the object.</span></span>
- <span data-ttu-id="5e16f-564">**objec**: nesne bilgisi kapsayıcısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-564">**objec**: Pointer to object information container.</span></span>

### <a name="return-value"></a><span data-ttu-id="5e16f-565">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="5e16f-565">Return Value</span></span>

- <span data-ttu-id="5e16f-566">**UX_SUCCESS**: (0x00) veri aktarımı tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="5e16f-566">**UX_SUCCESS**: (0x00) The data transfer was completed.</span></span>
- <span data-ttu-id="5e16f-567">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) oturum açılmadı</span><span class="sxs-lookup"><span data-stu-id="5e16f-567">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) Session not opened</span></span>
- <span data-ttu-id="5e16f-568">**UX_HOST_CLASS_PIMA_RC_OBJECT_ALREADY_OPENED**: (0X2021) nesne zaten açık.</span><span class="sxs-lookup"><span data-stu-id="5e16f-568">**UX_HOST_CLASS_PIMA_RC_OBJECT_ALREADY_OPENED**: (0x2021) Object already opened.</span></span>
- <span data-ttu-id="5e16f-569">**UX_MEMORY_INSUFFICIENT**: (0x12) Pima komutu oluşturmak için yeterli bellek yok.</span><span class="sxs-lookup"><span data-stu-id="5e16f-569">**UX_MEMORY_INSUFFICIENT**: (0x12) Not enough memory to create PIMA command.</span></span>

### <a name="example"></a><span data-ttu-id="5e16f-570">Örnek</span><span class="sxs-lookup"><span data-stu-id="5e16f-570">Example</span></span>

```C
/* Open the object. */

status = ux_host_class_pima_object_open(pima, pima_session,
    object_handle, pima_object);

/* Check status. */
if (status != UX_SUCCESS)
    return(status);
```

## <a name="ux_host_class_pima_object_get"></a><span data-ttu-id="5e16f-571">ux_host_class_pima_object_get</span><span class="sxs-lookup"><span data-stu-id="5e16f-571">ux_host_class_pima_object_get</span></span>

<span data-ttu-id="5e16f-572">Yanıtlayanda depolanan bir nesne alın.</span><span class="sxs-lookup"><span data-stu-id="5e16f-572">Get an object stored in the Responder.</span></span>

### <a name="prototype"></a><span data-ttu-id="5e16f-573">Prototype</span><span class="sxs-lookup"><span data-stu-id="5e16f-573">Prototype</span></span>

```C
UINT ux_host_class_pima_object_get(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    ULONG object_handle,
    UX_HOST_CLASS_PIMA_OBJECT *object,
    UCHAR *object_buffer,
    ULONG object_buffer_length,
    ULONG *object_actual_length)
```

### <a name="description"></a><span data-ttu-id="5e16f-574">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5e16f-574">Description</span></span>

<span data-ttu-id="5e16f-575">Bu işlev, Yanıtlayıcıda bir nesne alır.</span><span class="sxs-lookup"><span data-stu-id="5e16f-575">This function gets an object on the responder.</span></span>

### <a name="parameters"></a><span data-ttu-id="5e16f-576">Parametreler</span><span class="sxs-lookup"><span data-stu-id="5e16f-576">Parameters</span></span>

- <span data-ttu-id="5e16f-577">**Pima**: Pima sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-577">**pima**: Pointer to the pima class instance.</span></span>
- <span data-ttu-id="5e16f-578">**pima_session**: Pima oturumuna yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="5e16f-578">**pima_session**: Pointer to PIMA session</span></span>
- <span data-ttu-id="5e16f-579">**object_handle**: nesnenin tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="5e16f-579">**object_handle**: handle of the object</span></span>
- <span data-ttu-id="5e16f-580">**nesne**: nesne bilgisi kapsayıcısının işaretçisi</span><span class="sxs-lookup"><span data-stu-id="5e16f-580">**object**: Pointer to object information container</span></span>
- <span data-ttu-id="5e16f-581">**object_buffer**: nesne verilerinin adresi</span><span class="sxs-lookup"><span data-stu-id="5e16f-581">**object_buffer**: Address of object data</span></span>
- <span data-ttu-id="5e16f-582">**object_buffer_length**: istenen nesne uzunluğu</span><span class="sxs-lookup"><span data-stu-id="5e16f-582">**object_buffer_length**: Requested length of object</span></span>
- <span data-ttu-id="5e16f-583">**object_actual_length**: döndürülen nesne uzunluğu</span><span class="sxs-lookup"><span data-stu-id="5e16f-583">**object_actual_length**: Length of object returned</span></span>

### <a name="return-value"></a><span data-ttu-id="5e16f-584">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="5e16f-584">Return Value</span></span>

- <span data-ttu-id="5e16f-585">**UX_SUCCESS**: (0x00) nesne aktarıldı</span><span class="sxs-lookup"><span data-stu-id="5e16f-585">**UX_SUCCESS**: (0x00) The object was transfered</span></span>
- <span data-ttu-id="5e16f-586">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) oturum açılmadı</span><span class="sxs-lookup"><span data-stu-id="5e16f-586">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) Session not opened</span></span>
- <span data-ttu-id="5e16f-587">**UX_HOST_CLASS_PIMA_RC_OBJECT_NOT_OPENED**: (0X2023) nesnesi açılmadı.</span><span class="sxs-lookup"><span data-stu-id="5e16f-587">**UX_HOST_CLASS_PIMA_RC_OBJECT_NOT_OPENED**: (0x2023) Object not opened.</span></span>
- <span data-ttu-id="5e16f-588">**UX_HOST_CLASS_PIMA_RC_ACCESS_DENIED**: (0x200f) nesne erişimi reddedildi</span><span class="sxs-lookup"><span data-stu-id="5e16f-588">**UX_HOST_CLASS_PIMA_RC_ACCESS_DENIED**: (0x200f) Access to object denied</span></span>
- <span data-ttu-id="5e16f-589">**UX_HOST_CLASS_PIMA_RC_INCOMPLETE_TRANSFER**: (0x2007) aktarım tamamlanmadı</span><span class="sxs-lookup"><span data-stu-id="5e16f-589">**UX_HOST_CLASS_PIMA_RC_INCOMPLETE_TRANSFER**: (0x2007) Transfer is incomplete</span></span>
- <span data-ttu-id="5e16f-590">**UX_MEMORY_INSUFFICIENT**: (0x12) Pima komutu oluşturmak için yeterli bellek yok.</span><span class="sxs-lookup"><span data-stu-id="5e16f-590">**UX_MEMORY_INSUFFICIENT**: (0x12) Not enough memory to create PIMA command.</span></span>
- <span data-ttu-id="5e16f-591">**UX_TRANSFER_ERROR**: (0x23) nesne okunurken aktarım hatası oluştu</span><span class="sxs-lookup"><span data-stu-id="5e16f-591">**UX_TRANSFER_ERROR**: (0x23) Transfer error while reading object</span></span>

### <a name="example"></a><span data-ttu-id="5e16f-592">Örnek</span><span class="sxs-lookup"><span data-stu-id="5e16f-592">Example</span></span>

```C
/* Open the object. */

status = ux_host_class_pima_object_open(pima, pima_session,
    object_handle, pima_object);

/* Check status. */
if (status != UX_SUCCESS)
    return(status);

/* Set the object buffer pointer. */
object_buffer = pima_object ->ux_host_class_pima_object_buffer;

/* Obtain all the object data. */
while(object_length != 0)
{
    /* Calculate what length to request. */
    if (object_length > UX_PICTBRIDGE_MAX_PIMA_OBJECT_BUFFER)
        /* Request maximum length. */
        requested_length = UX_PICTBRIDGE_MAX_PIMA_OBJECT_BUFFER;
    else
        /* Request remaining length. */
        requested_length = object_length;

    /* Get the object data. */
    status = ux_host_class_pima_object_get(pima, pima_session,
        object_handle, pima_object, object_buffer,
        requested_length, &actual_length);

    if (status != UX_SUCCESS)
    {
        /* We had a problem, abort the transfer. */
        ux_host_class_pima_object_transfer_abort(pima, pima_session,
            object_handle, pima_object);

        /* And close the object. */
        ux_host_class_pima_object_close(pima, pima_session,
            object_handle, pima_object, object);

        return(status);

    }

    /* We have received some data, update the length remaining. */
    object_length -= actual_length;

    /* Update the buffer address. */
    object_buffer += actual_length;

}

/* Close the object. */
status = ux_host_class_pima_object_close(pima, pima_session,
    object_handle, pima_object, object);
```

## <a name="ux_host_class_pima_object_send"></a><span data-ttu-id="5e16f-593">ux_host_class_pima_object_send</span><span class="sxs-lookup"><span data-stu-id="5e16f-593">ux_host_class_pima_object_send</span></span>

<span data-ttu-id="5e16f-594">Yanıtlayanda depolanan bir nesne gönderin.</span><span class="sxs-lookup"><span data-stu-id="5e16f-594">Send an object stored in the Responder.</span></span>

### <a name="prototype"></a><span data-ttu-id="5e16f-595">Prototype</span><span class="sxs-lookup"><span data-stu-id="5e16f-595">Prototype</span></span>

```C
UINT ux_host_class_pima_object_send(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    UX_HOST_CLASS_PIMA_OBJECT *object,
    UCHAR *object_buffer, ULONG object_buffer_length)
```

### <a name="description"></a><span data-ttu-id="5e16f-596">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5e16f-596">Description</span></span>

<span data-ttu-id="5e16f-597">Bu işlev, Yanıtlayıcıya bir nesnesi gönderir.</span><span class="sxs-lookup"><span data-stu-id="5e16f-597">This function sends an object to the responder.</span></span>

### <a name="parameters"></a><span data-ttu-id="5e16f-598">Parametreler</span><span class="sxs-lookup"><span data-stu-id="5e16f-598">Parameters</span></span>

- <span data-ttu-id="5e16f-599">**Pima**: Pima sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-599">**pima**: Pointer to the pima class instance.</span></span>
- <span data-ttu-id="5e16f-600">**pima_sessio**: Pima oturumuna yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="5e16f-600">**pima_sessio**: Pointer to PIMA session</span></span>
- <span data-ttu-id="5e16f-601">**object_handle**: nesnenin tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="5e16f-601">**object_handle**: handle of the object</span></span>
- <span data-ttu-id="5e16f-602">**nesne**: nesne bilgisi kapsayıcısının işaretçisi</span><span class="sxs-lookup"><span data-stu-id="5e16f-602">**object**: Pointer to object information container</span></span>
- <span data-ttu-id="5e16f-603">**object_buffer**: nesne verilerinin adresi</span><span class="sxs-lookup"><span data-stu-id="5e16f-603">**object_buffer**: Address of object data</span></span>
- <span data-ttu-id="5e16f-604">**object_buffer_length**: istenen nesne uzunluğu</span><span class="sxs-lookup"><span data-stu-id="5e16f-604">**object_buffer_length**: Requested length of object</span></span>

### <a name="return-value"></a><span data-ttu-id="5e16f-605">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="5e16f-605">Return Value</span></span>

- <span data-ttu-id="5e16f-606">**UX_SUCCESS**: (0x00) veri aktarımı tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="5e16f-606">**UX_SUCCESS**: (0x00) The data transfer was completed.</span></span>
- <span data-ttu-id="5e16f-607">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) oturum açılmadı</span><span class="sxs-lookup"><span data-stu-id="5e16f-607">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) Session not opened</span></span>
- <span data-ttu-id="5e16f-608">**UX_HOST_CLASS_PIMA_RC_OBJECT_NOT_OPENED**: (0X2023) nesnesi açılmadı.</span><span class="sxs-lookup"><span data-stu-id="5e16f-608">**UX_HOST_CLASS_PIMA_RC_OBJECT_NOT_OPENED**: (0x2023) Object not opened.</span></span>
- <span data-ttu-id="5e16f-609">**UX_HOST_CLASS_PIMA_RC_ACCESS_DENIED**: (0x200f) nesne erişimi reddedildi</span><span class="sxs-lookup"><span data-stu-id="5e16f-609">**UX_HOST_CLASS_PIMA_RC_ACCESS_DENIED**: (0x200f) Access to object denied</span></span>
- <span data-ttu-id="5e16f-610">**UX_HOST_CLASS_PIMA_RC_INCOMPLETE_TRANSFER**: (0x2007) aktarım tamamlanmadı</span><span class="sxs-lookup"><span data-stu-id="5e16f-610">**UX_HOST_CLASS_PIMA_RC_INCOMPLETE_TRANSFER**: (0x2007) Transfer is incomplete</span></span>
- <span data-ttu-id="5e16f-611">**UX_MEMORY_INSUFFICIENT**: (0x12) Pima komutu oluşturmak için yeterli bellek yok.</span><span class="sxs-lookup"><span data-stu-id="5e16f-611">**UX_MEMORY_INSUFFICIENT**: (0x12) Not enough memory to create PIMA command.</span></span>
- <span data-ttu-id="5e16f-612">**UX_TRANSFER_ERROR**: (0x23) nesne yazılırken aktarım hatası</span><span class="sxs-lookup"><span data-stu-id="5e16f-612">**UX_TRANSFER_ERROR**: (0x23) Transfer error while writing object</span></span>

### <a name="example"></a><span data-ttu-id="5e16f-613">Örnek</span><span class="sxs-lookup"><span data-stu-id="5e16f-613">Example</span></span>

```C
/* Open the object. */
status = ux_host_class_pima_object_open(pima, pima_session,
    object_handle, pima_object);

/* Get the object length. */
object_length = pima_object ->ux_host_class_pima_object_compressed_size;

/* Recall the object buffer address. */
pima_object_buffer = pima_object ->ux_host_class_pima_object_buffer;

/* Send all the object data. */
while(object_length != 0)
{
    /* Calculate what length to request. */
    if (object_length > UX_PICTBRIDGE_MAX_PIMA_OBJECT_BUFFER)
        /* Request maximum length. */
        requested_length = UX_PICTBRIDGE_MAX_PIMA_OBJECT_BUFFER;
    else
        /* Request remaining length. */
        requested_length = object_length;

    /* Send the object data. */
    status = ux_host_class_pima_object_send(pima,
        pima_session, pima_object,
        pima_object_buffer, requested_length);

    if (status != UX_SUCCESS)
    {
        /* Abort the transfer. */
        ux_host_class_pima_object_transfer_abort(pima, pima_session,
            object_handle, pima_object);

        /* Return status. */
        return(status);
    }

    /* We have sent some data, update the length remaining. */
    object_length -= requested_length;
}

/* Close the object. */
status = ux_host_class_pima_object_close(pima, pima_session, object_handle,
    pima_object, object);
```

## <a name="ux_host_class_pima_thumb_get"></a><span data-ttu-id="5e16f-614">ux_host_class_pima_thumb_get</span><span class="sxs-lookup"><span data-stu-id="5e16f-614">ux_host_class_pima_thumb_get</span></span>

<span data-ttu-id="5e16f-615">Yanıtlayanın içinde depolanan bir Thumb nesnesi alın.</span><span class="sxs-lookup"><span data-stu-id="5e16f-615">Get a thumb object stored in the Responder.</span></span>

### <a name="prototype"></a><span data-ttu-id="5e16f-616">Prototype</span><span class="sxs-lookup"><span data-stu-id="5e16f-616">Prototype</span></span>

```C
UINT ux_host_class_pima_thumb_get(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    ULONG object_handle,
    UX_HOST_CLASS_PIMA_OBJECT *object,
    UCHAR *thumb_buffer, ULONG thumb_buffer_length,
    ULONG *thumb_actual_length)
```

### <a name="description"></a><span data-ttu-id="5e16f-617">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5e16f-617">Description</span></span>

<span data-ttu-id="5e16f-618">Bu işlev, Yanıtlayıcıda bir Thumb nesnesi alır.</span><span class="sxs-lookup"><span data-stu-id="5e16f-618">This function gets a thumb object on the responder.</span></span>

### <a name="parameters"></a><span data-ttu-id="5e16f-619">Parametreler</span><span class="sxs-lookup"><span data-stu-id="5e16f-619">Parameters</span></span>

- <span data-ttu-id="5e16f-620">**Pima**: Pima sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-620">**pima**: Pointer to the pima class instance.</span></span>
- <span data-ttu-id="5e16f-621">**pima_session**: Pima oturumuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-621">**pima_session**: Pointer to PIMA session.</span></span>
- <span data-ttu-id="5e16f-622">**object_handle**: nesnenin tanıtıcısı.</span><span class="sxs-lookup"><span data-stu-id="5e16f-622">**object_handle**: handle of the object.</span></span>
- <span data-ttu-id="5e16f-623">**nesne**: nesne bilgisi kapsayıcısının işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-623">**object**: Pointer to object information container.</span></span>
- <span data-ttu-id="5e16f-624">**thumb_buffer**: Thumb nesne verilerinin adresi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-624">**thumb_buffer**: Address of thumb object data.</span></span>
- <span data-ttu-id="5e16f-625">**thumb_buffer_length**: parmak nesnesi uzunluğu istendi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-625">**thumb_buffer_length**: Requested length of thumb object.</span></span>
- <span data-ttu-id="5e16f-626">**thumb_actual_length**: döndürülen Thumb nesnesinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="5e16f-626">**thumb_actual_length**: Length of thumb object returned.</span></span>

### <a name="return-value"></a><span data-ttu-id="5e16f-627">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="5e16f-627">Return Value</span></span>

- <span data-ttu-id="5e16f-628">**UX_SUCCESS**: (0x00) veri aktarımı tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="5e16f-628">**UX_SUCCESS**: (0x00) The data transfer was completed.</span></span>
- <span data-ttu-id="5e16f-629">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) oturum açılmadı.</span><span class="sxs-lookup"><span data-stu-id="5e16f-629">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) Session not opened.</span></span>
- <span data-ttu-id="5e16f-630">**UX_HOST_CLASS_PIMA_RC_OBJECT_NOT_OPENED**: (0X2023) nesnesi açılmadı.</span><span class="sxs-lookup"><span data-stu-id="5e16f-630">**UX_HOST_CLASS_PIMA_RC_OBJECT_NOT_OPENED**: (0x2023) Object not opened.</span></span>
- <span data-ttu-id="5e16f-631">**UX_HOST_CLASS_PIMA_RC_ACCESS_DENIED**: (0x200f) nesne erişimi reddedildi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-631">**UX_HOST_CLASS_PIMA_RC_ACCESS_DENIED**: (0x200f) Access to object denied.</span></span>
- <span data-ttu-id="5e16f-632">**UX_HOST_CLASS_PIMA_RC_INCOMPLETE_TRANSFER**: (0x2007) aktarma tamamlanmadı.</span><span class="sxs-lookup"><span data-stu-id="5e16f-632">**UX_HOST_CLASS_PIMA_RC_INCOMPLETE_TRANSFER**: (0x2007) Transfer is incomplete.</span></span>
- <span data-ttu-id="5e16f-633">**UX_MEMORY_INSUFFICIENT**: (0x12) Pima komutu oluşturmak için yeterli bellek yok.</span><span class="sxs-lookup"><span data-stu-id="5e16f-633">**UX_MEMORY_INSUFFICIENT**: (0x12) Not enough memory to create PIMA command.</span></span>
- <span data-ttu-id="5e16f-634">**UX_TRANSFER_ERROR**: (0x23) nesne okunurken aktarım hatası oluştu.</span><span class="sxs-lookup"><span data-stu-id="5e16f-634">**UX_TRANSFER_ERROR**: (0x23) Transfer error while reading object.</span></span>

### <a name="example"></a><span data-ttu-id="5e16f-635">Örnek</span><span class="sxs-lookup"><span data-stu-id="5e16f-635">Example</span></span>

```C
/* Get the thumb object data. */

status = ux_host_class_pima_thumb_get(pima, pima_session,
    object_handle, pima_object, object_buffer,
    requested_length, &actual_length);

if (status != UX_SUCCESS)
{
    /* And close the object. */
    ux_host_class_pima_object_close(pima, pima_session, object_handle, pima_object, object);

    return(status);
}
```

## <a name="ux_host_class_pima_object_delete"></a><span data-ttu-id="5e16f-636">ux_host_class_pima_object_delete</span><span class="sxs-lookup"><span data-stu-id="5e16f-636">ux_host_class_pima_object_delete</span></span>

<span data-ttu-id="5e16f-637">Yanıtlayanda depolanan bir nesneyi silin.</span><span class="sxs-lookup"><span data-stu-id="5e16f-637">Delete an object stored in the Responder.</span></span>

### <a name="prototype"></a><span data-ttu-id="5e16f-638">Prototype</span><span class="sxs-lookup"><span data-stu-id="5e16f-638">Prototype</span></span>

```C
UINT ux_host_class_pima_object_delete(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    ULONG object_handle)
```

### <a name="description"></a><span data-ttu-id="5e16f-639">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5e16f-639">Description</span></span>

<span data-ttu-id="5e16f-640">Bu işlev, Yanıtlayıcıda bir nesneyi siler</span><span class="sxs-lookup"><span data-stu-id="5e16f-640">This function deletes an object on the responder</span></span>

### <a name="parameters"></a><span data-ttu-id="5e16f-641">Parametreler</span><span class="sxs-lookup"><span data-stu-id="5e16f-641">Parameters</span></span>

- <span data-ttu-id="5e16f-642">**Pima**: Pima sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-642">**pima**: Pointer to the pima class instance.</span></span>
- <span data-ttu-id="5e16f-643">**pima_session**: Pima oturumuna yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="5e16f-643">**pima_session**: Pointer to PIMA session</span></span>
- <span data-ttu-id="5e16f-644">**object_handle**: nesnenin tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="5e16f-644">**object_handle**: handle of the object</span></span>

### <a name="return-value"></a><span data-ttu-id="5e16f-645">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="5e16f-645">Return Value</span></span>

- <span data-ttu-id="5e16f-646">**UX_SUCCESS**: (0x00) nesne silindi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-646">**UX_SUCCESS**: (0x00) The object was deleted.</span></span>
- <span data-ttu-id="5e16f-647">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) oturum açılmadı.</span><span class="sxs-lookup"><span data-stu-id="5e16f-647">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) Session not opened.</span></span>
- <span data-ttu-id="5e16f-648">**UX_HOST_CLASS_PIMA_RC_ACCESS_DENIED**: (0x200f) nesne silinemiyor.</span><span class="sxs-lookup"><span data-stu-id="5e16f-648">**UX_HOST_CLASS_PIMA_RC_ACCESS_DENIED**: (0x200f) Cannot delete object.</span></span>
- <span data-ttu-id="5e16f-649">**UX_MEMORY_INSUFFICIENT**: (0x12) Pima komutu oluşturmak için yeterli bellek yok.</span><span class="sxs-lookup"><span data-stu-id="5e16f-649">**UX_MEMORY_INSUFFICIENT**: (0x12) Not enough memory to create PIMA command.</span></span>

### <a name="example"></a><span data-ttu-id="5e16f-650">Örnek</span><span class="sxs-lookup"><span data-stu-id="5e16f-650">Example</span></span>

```C
/* Delete the object. */
status = ux_host_class_pima_object_delete(pima, pima_session, object_handle, pima_object);

/* Check status. */
if (status != UX_SUCCESS)
    return(status);
```

## <a name="ux_host_class_pima_object_close"></a><span data-ttu-id="5e16f-651">ux_host_class_pima_object_close</span><span class="sxs-lookup"><span data-stu-id="5e16f-651">ux_host_class_pima_object_close</span></span>

<span data-ttu-id="5e16f-652">Yanıtlayanın içinde depolanan bir nesneyi kapatma</span><span class="sxs-lookup"><span data-stu-id="5e16f-652">Close an object stored in the Responder</span></span>

### <a name="prototype"></a><span data-ttu-id="5e16f-653">Prototype</span><span class="sxs-lookup"><span data-stu-id="5e16f-653">Prototype</span></span>

```C
UINT ux_host_class_pima_object_close(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    ULONG object_handle, UX_HOST_CLASS_PIMA_OBJECT *object)
```

### <a name="description"></a><span data-ttu-id="5e16f-654">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5e16f-654">Description</span></span>

<span data-ttu-id="5e16f-655">Bu işlev, yanıtlayanın bir nesnesini kapatır.</span><span class="sxs-lookup"><span data-stu-id="5e16f-655">This function closes an object on the responder.</span></span>

### <a name="parameters"></a><span data-ttu-id="5e16f-656">Parametreler</span><span class="sxs-lookup"><span data-stu-id="5e16f-656">Parameters</span></span>

- <span data-ttu-id="5e16f-657">**Pima**: Pima sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-657">**pima**: Pointer to the pima class instance.</span></span>
- <span data-ttu-id="5e16f-658">**pima_session**: Pima oturumuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-658">**pima_session**: Pointer to PIMA session.</span></span>
- <span data-ttu-id="5e16f-659">**object_handle**: nesnenin tanıtıcısı.</span><span class="sxs-lookup"><span data-stu-id="5e16f-659">**object_handle**: Handle of the object.</span></span>
- <span data-ttu-id="5e16f-660">**nesne**: nesne işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-660">**object**: Pointer to object.</span></span>

### <a name="return-value"></a><span data-ttu-id="5e16f-661">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="5e16f-661">Return Value</span></span>

- <span data-ttu-id="5e16f-662">**UX_SUCCESS**: (0x00) nesne kapatıldı.</span><span class="sxs-lookup"><span data-stu-id="5e16f-662">**UX_SUCCESS**: (0x00) The object was closed.</span></span>
- <span data-ttu-id="5e16f-663">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) oturum açılmadı.</span><span class="sxs-lookup"><span data-stu-id="5e16f-663">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) Session not opened.</span></span>
- <span data-ttu-id="5e16f-664">**UX_HOST_CLASS_PIMA_RC_OBJECT_NOT_OPENED**: (0X2023) nesnesi açılmadı.</span><span class="sxs-lookup"><span data-stu-id="5e16f-664">**UX_HOST_CLASS_PIMA_RC_OBJECT_NOT_OPENED**: (0x2023) Object not opened.</span></span>
- <span data-ttu-id="5e16f-665">**UX_MEMORY_INSUFFICIENT**: (0x12) Pima komutu oluşturmak için yeterli bellek yok.</span><span class="sxs-lookup"><span data-stu-id="5e16f-665">**UX_MEMORY_INSUFFICIENT**: (0x12) Not enough memory to create PIMA command.</span></span>

### <a name="example"></a><span data-ttu-id="5e16f-666">Örnek</span><span class="sxs-lookup"><span data-stu-id="5e16f-666">Example</span></span>

```C
/* Close the object. */
status = ux_host_class_pima_object_close(pima, pima_session, object_handle, object);
```

## <a name="ux_host_class_gser_read"></a><span data-ttu-id="5e16f-667">ux_host_class_gser_read</span><span class="sxs-lookup"><span data-stu-id="5e16f-667">ux_host_class_gser_read</span></span>

<span data-ttu-id="5e16f-668">Genel seri arabiriminden okuyun.</span><span class="sxs-lookup"><span data-stu-id="5e16f-668">Read from the generic serial interface.</span></span>

### <a name="prototype"></a><span data-ttu-id="5e16f-669">Prototype</span><span class="sxs-lookup"><span data-stu-id="5e16f-669">Prototype</span></span>

```C
UINT ux_host_class_gser_read(
    UX_HOST_CLASS_GSER *gser,
    ULONG interface_index,
    UCHAR *data_pointer,
    ULONG requested_length,
    ULONG *actual_length)
```

### <a name="description"></a><span data-ttu-id="5e16f-670">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5e16f-670">Description</span></span>

<span data-ttu-id="5e16f-671">Bu işlev genel seri arabiriminden okur.</span><span class="sxs-lookup"><span data-stu-id="5e16f-671">This function reads from the generic serial interface.</span></span> <span data-ttu-id="5e16f-672">Çağrı engelleniyor ve yalnızca bir hata olduğunda ya da aktarım tamamlandığında döndürülür.</span><span class="sxs-lookup"><span data-stu-id="5e16f-672">The call is blocking and only returns when there is either an error or when the transfer is complete.</span></span>

### <a name="parameters"></a><span data-ttu-id="5e16f-673">Parametreler</span><span class="sxs-lookup"><span data-stu-id="5e16f-673">Parameters</span></span>

- <span data-ttu-id="5e16f-674">**gser**: gser sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-674">**gser**: Pointer to the gser class instance.</span></span>
- <span data-ttu-id="5e16f-675">**interface_index**: okunacak arabirim dizini.</span><span class="sxs-lookup"><span data-stu-id="5e16f-675">**interface_index**: Interface index to read from.</span></span>
- <span data-ttu-id="5e16f-676">**data_pointer**: veri yükünün arabellek adresine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-676">**data_pointer**: Pointer to the buffer address of the data payload.</span></span>
- <span data-ttu-id="5e16f-677">**requested_length**: alınacak uzunluk.</span><span class="sxs-lookup"><span data-stu-id="5e16f-677">**requested_length**: Length to be received.</span></span>
- <span data-ttu-id="5e16f-678">**actual_length**: Uzunluk gerçekten alındı.</span><span class="sxs-lookup"><span data-stu-id="5e16f-678">**actual_length**: Length actually received.</span></span>

### <a name="return-value"></a><span data-ttu-id="5e16f-679">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="5e16f-679">Return Value</span></span>

- <span data-ttu-id="5e16f-680">**UX_SUCCESS**: (0x00) veri aktarımı tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="5e16f-680">**UX_SUCCESS**: (0x00) The data transfer was completed.</span></span>
- <span data-ttu-id="5e16f-681">**UX_TRANSFER_TIMEOUT**: (0x5c) aktarım zaman aşımı, okuma tamamlanmadı.</span><span class="sxs-lookup"><span data-stu-id="5e16f-681">**UX_TRANSFER_TIMEOUT**: (0x5c) Transfer timeout, reading incomplete.</span></span>

### <a name="example"></a><span data-ttu-id="5e16f-682">Örnek</span><span class="sxs-lookup"><span data-stu-id="5e16f-682">Example</span></span>

```C
UINT status;

/* The following example illustrates this service. */
status = ux_host_class_gser_read(cdc_acm, interface_index,data_pointer, requested_length, &actual_length);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_gser_write"></a><span data-ttu-id="5e16f-683">ux_host_class_gser_write</span><span class="sxs-lookup"><span data-stu-id="5e16f-683">ux_host_class_gser_write</span></span>

<span data-ttu-id="5e16f-684">Genel seri arabirimine yazın.</span><span class="sxs-lookup"><span data-stu-id="5e16f-684">Write to the generic serial interface.</span></span>

### <a name="prototype"></a><span data-ttu-id="5e16f-685">Prototype</span><span class="sxs-lookup"><span data-stu-id="5e16f-685">Prototype</span></span>

```C
UINT ux_host_class_gser_write(
    UX_HOST_CLASS_GSER *gser,
    ULONG interface_index,
    UCHAR *data_pointer,
    ULONG requested_length,
    ULONG *actual_length)
```

### <a name="description"></a><span data-ttu-id="5e16f-686">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5e16f-686">Description</span></span>

<span data-ttu-id="5e16f-687">Bu işlev genel seri arabirimine yazar.</span><span class="sxs-lookup"><span data-stu-id="5e16f-687">This function writes to the generic serial interface.</span></span> <span data-ttu-id="5e16f-688">Çağrı engelleniyor ve yalnızca bir hata olduğunda ya da aktarım tamamlandığında döndürülür.</span><span class="sxs-lookup"><span data-stu-id="5e16f-688">The call is blocking and only returns when there is either an error or when the transfer is complete.</span></span>

### <a name="parameters"></a><span data-ttu-id="5e16f-689">Parametreler</span><span class="sxs-lookup"><span data-stu-id="5e16f-689">Parameters</span></span>

- <span data-ttu-id="5e16f-690">**gser**: gser sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-690">**gser**: Pointer to the gser class instance.</span></span>
- <span data-ttu-id="5e16f-691">**interface_index**: yazılacak arabirim.</span><span class="sxs-lookup"><span data-stu-id="5e16f-691">**interface_index**: Interface to which to write.</span></span>
- <span data-ttu-id="5e16f-692">**data_pointer**: veri yükünün arabellek adresine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-692">**data_pointer**: Pointer to the buffer address of the data payload.</span></span>
- <span data-ttu-id="5e16f-693">**requested_length**: gönderilecek uzunluk.</span><span class="sxs-lookup"><span data-stu-id="5e16f-693">**requested_length**: Length to be sent.</span></span>
- <span data-ttu-id="5e16f-694">**actual_length**: Uzunluk gerçekten gönderildi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-694">**actual_length**: Length actually sent.</span></span>

### <a name="return-value"></a><span data-ttu-id="5e16f-695">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="5e16f-695">Return Value</span></span>

- <span data-ttu-id="5e16f-696">**UX_SUCCESS**: (0x00) veri aktarımı tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="5e16f-696">**UX_SUCCESS**: (0x00) The data transfer was completed.</span></span>
- <span data-ttu-id="5e16f-697">**UX_TRANSFER_TIMEOUT**: (0x5c) aktarım zaman aşımı, yazma tamamlanmamış.</span><span class="sxs-lookup"><span data-stu-id="5e16f-697">**UX_TRANSFER_TIMEOUT**: (0x5c) Transfer timeout, writing incomplete.</span></span>

### <a name="example"></a><span data-ttu-id="5e16f-698">Örnek</span><span class="sxs-lookup"><span data-stu-id="5e16f-698">Example</span></span>

```C
UINT status;

/* The following example illustrates this service. */
status = ux_host_class_cdc_acm_write(gser, data_pointer, requested_length, &actual_length);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_gser_ioctl"></a><span data-ttu-id="5e16f-699">ux_host_class_gser_ioctl</span><span class="sxs-lookup"><span data-stu-id="5e16f-699">ux_host_class_gser_ioctl</span></span>

<span data-ttu-id="5e16f-700">Genel seri arabirimine bir ıOCTL işlevi gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="5e16f-700">Perform an IOCTL function to the generic serial interface.</span></span>

### <a name="prototype"></a><span data-ttu-id="5e16f-701">Prototype</span><span class="sxs-lookup"><span data-stu-id="5e16f-701">Prototype</span></span>

```C
UINT ux_host_class_gser_ioctl(
    UX_HOST_CLASS_GSER *gser,
    ULONG ioctl_function,
    VOID *parameter)
```

### <a name="description"></a><span data-ttu-id="5e16f-702">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5e16f-702">Description</span></span>

<span data-ttu-id="5e16f-703">Bu işlev, gser arabirimine belirli bir IOCTL işlevi gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="5e16f-703">This function performs a specific ioctl function to the gser interface.</span></span> <span data-ttu-id="5e16f-704">Çağrı engelleniyor ve yalnızca bir hata olduğunda ya da komut tamamlandığında döndürülür.</span><span class="sxs-lookup"><span data-stu-id="5e16f-704">The call is blocking and only returns when there is either an error or when the command is completed.</span></span>

### <a name="parameters"></a><span data-ttu-id="5e16f-705">Parametreler</span><span class="sxs-lookup"><span data-stu-id="5e16f-705">Parameters</span></span>

- <span data-ttu-id="5e16f-706">**gser**: gser sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-706">**gser**: Pointer to the gser class instance.</span></span>
- <span data-ttu-id="5e16f-707">**ioctl_function**: gerçekleştirilecek IOCTL işlevi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-707">**ioctl_function**: ioctl function to be performed.</span></span> <span data-ttu-id="5e16f-708">İzin verilen IOCTL işlevlerinden biri için aşağıdaki tabloya bakın.</span><span class="sxs-lookup"><span data-stu-id="5e16f-708">See table below for one of the allowed ioctl functions.</span></span>
- <span data-ttu-id="5e16f-709">**parametre**: IOCTL 'ye özgü bir parametreye pointerto</span><span class="sxs-lookup"><span data-stu-id="5e16f-709">**parameter**: Pointerto a parameter specific to the ioctl</span></span>

### <a name="return-value"></a><span data-ttu-id="5e16f-710">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="5e16f-710">Return Value</span></span>

- <span data-ttu-id="5e16f-711">**UX_SUCCESS**: (0x00) veri aktarımı tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="5e16f-711">**UX_SUCCESS**: (0x00) The data transfer was completed.</span></span>
- <span data-ttu-id="5e16f-712">**UX_MEMORY_INSUFFICIENT**: (0x12) yeterli bellek yok.</span><span class="sxs-lookup"><span data-stu-id="5e16f-712">**UX_MEMORY_INSUFFICIENT**: (0x12) Not enough memory.</span></span>
- <span data-ttu-id="5e16f-713">**UX_HOST_CLASS_UNKNOWN**: (0x59) yanlış sınıf örneği</span><span class="sxs-lookup"><span data-stu-id="5e16f-713">**UX_HOST_CLASS_UNKNOWN**: (0x59) Wrong class instance</span></span>
- <span data-ttu-id="5e16f-714">**UX_FUNCTION_NOT_SUPPORTED**: (0x54) bilinmeyen IOCTL işlevi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-714">**UX_FUNCTION_NOT_SUPPORTED**: (0x54) Unknown IOCTL function.</span></span>

### <a name="ioctl-functions"></a><span data-ttu-id="5e16f-715">IOCTL işlevleri</span><span class="sxs-lookup"><span data-stu-id="5e16f-715">IOCTL functions</span></span>

- <span data-ttu-id="5e16f-716">UX_HOST_CLASS_GSER_IOCTL_SET_LINE_CODING</span><span class="sxs-lookup"><span data-stu-id="5e16f-716">UX_HOST_CLASS_GSER_IOCTL_SET_LINE_CODING</span></span>
- <span data-ttu-id="5e16f-717">UX_HOST_CLASS_GSER_IOCTL_GET_LINE_CODING</span><span class="sxs-lookup"><span data-stu-id="5e16f-717">UX_HOST_CLASS_GSER_IOCTL_GET_LINE_CODING</span></span>
- <span data-ttu-id="5e16f-718">UX_HOST_CLASS_GSER_IOCTL_SET_LINE_STATE</span><span class="sxs-lookup"><span data-stu-id="5e16f-718">UX_HOST_CLASS_GSER_IOCTL_SET_LINE_STATE</span></span>
- <span data-ttu-id="5e16f-719">UX_HOST_CLASS_GSER_IOCTL_SEND_BREAK</span><span class="sxs-lookup"><span data-stu-id="5e16f-719">UX_HOST_CLASS_GSER_IOCTL_SEND_BREAK</span></span>
- <span data-ttu-id="5e16f-720">UX_HOST_CLASS_GSER_IOCTL_ABORT_IN_PIPE</span><span class="sxs-lookup"><span data-stu-id="5e16f-720">UX_HOST_CLASS_GSER_IOCTL_ABORT_IN_PIPE</span></span>
- <span data-ttu-id="5e16f-721">UX_HOST_CLASS_GSER_IOCTL_ABORT_OUT_PIPE</span><span class="sxs-lookup"><span data-stu-id="5e16f-721">UX_HOST_CLASS_GSER_IOCTL_ABORT_OUT_PIPE</span></span>
- <span data-ttu-id="5e16f-722">UX_HOST_CLASS_GSER_IOCTL_NOTIFICATION_CALLBACK</span><span class="sxs-lookup"><span data-stu-id="5e16f-722">UX_HOST_CLASS_GSER_IOCTL_NOTIFICATION_CALLBACK</span></span>
- <span data-ttu-id="5e16f-723">UX_HOST_CLASS_GSER_IOCTL_GET_DEVICE_STATUS</span><span class="sxs-lookup"><span data-stu-id="5e16f-723">UX_HOST_CLASS_GSER_IOCTL_GET_DEVICE_STATUS</span></span>

### <a name="example"></a><span data-ttu-id="5e16f-724">Örnek</span><span class="sxs-lookup"><span data-stu-id="5e16f-724">Example</span></span>

```C
UINT status;

/* The following example illustrates this service. */

status = ux_host_class_gser_ioctl(gser,
    UX_HOST_CLASS_GSER_IOCTL_GET_LINE_CODING,
    (VOID *)&line_coding);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_gser_reception_start"></a><span data-ttu-id="5e16f-725">ux_host_class_gser_reception_start</span><span class="sxs-lookup"><span data-stu-id="5e16f-725">ux_host_class_gser_reception_start</span></span>

<span data-ttu-id="5e16f-726">Genel Seri arabirimde almayı Başlat</span><span class="sxs-lookup"><span data-stu-id="5e16f-726">Start reception on the generic serial interface</span></span>

### <a name="prototype"></a><span data-ttu-id="5e16f-727">Prototype</span><span class="sxs-lookup"><span data-stu-id="5e16f-727">Prototype</span></span>

```C
UINT ux_host_class_gser_reception_start(
    UX_HOST_CLASS_GSER *gser,
    UX_HOST_CLASS_GSER_RECEPTION *gser_reception)
```

### <a name="description"></a><span data-ttu-id="5e16f-728">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5e16f-728">Description</span></span>

<span data-ttu-id="5e16f-729">Bu işlev, genel seri sınıf arabirimindeki alımı başlatır.</span><span class="sxs-lookup"><span data-stu-id="5e16f-729">This function starts the reception on the generic serial class interface.</span></span> <span data-ttu-id="5e16f-730">Bu işlev, engellenmemiş alım için izin verir.</span><span class="sxs-lookup"><span data-stu-id="5e16f-730">This function allows for non-blocking reception.</span></span> <span data-ttu-id="5e16f-731">Bir arabellek alındığında uygulamaya çağrılan bir geri çağırma işlemi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-731">When a buffer is received, a callback in invoked into the application.</span></span>

### <a name="parameters"></a><span data-ttu-id="5e16f-732">Parametreler</span><span class="sxs-lookup"><span data-stu-id="5e16f-732">Parameters</span></span>

- <span data-ttu-id="5e16f-733">**gser** Gser sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-733">**gser** Pointer to the gser class instance.</span></span>
- <span data-ttu-id="5e16f-734">**gser_reception** Alım parametrelerini içeren yapı</span><span class="sxs-lookup"><span data-stu-id="5e16f-734">**gser_reception** Structure containing the reception parameters</span></span>

### <a name="return-value"></a><span data-ttu-id="5e16f-735">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="5e16f-735">Return Value</span></span>

- <span data-ttu-id="5e16f-736">**UX_SUCCESS** (0x00) veri aktarımı tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="5e16f-736">**UX_SUCCESS** (0x00) The data transfer was completed.</span></span>
- <span data-ttu-id="5e16f-737">**UX_HOST_CLASS_UNKNOWN** (0x59) yanlış sınıf örneği</span><span class="sxs-lookup"><span data-stu-id="5e16f-737">**UX_HOST_CLASS_UNKNOWN** (0x59) Wrong class instance</span></span>
- <span data-ttu-id="5e16f-738">**UX_ERROR** (0x01) hatası</span><span class="sxs-lookup"><span data-stu-id="5e16f-738">**UX_ERROR** (0x01) Error</span></span>

### <a name="example"></a><span data-ttu-id="5e16f-739">Örnek</span><span class="sxs-lookup"><span data-stu-id="5e16f-739">Example</span></span>

```C
/* Start the reception for gser. AT commands are on interface 2. */
gser_reception.ux_host_class_gser_reception_interface_index =
    UX_DEMO_GSER_AT_INTERFACE;
gser_reception.ux_host_class_gser_reception_block_size =
    UX_DEMO_RECEPTION_BLOCK_SIZE;
gser_reception.ux_host_class_gser_reception_data_buffer =
    gser_reception_buffer;
gser_reception.ux_host_class_gser_reception_data_buffer_size =
    UX_DEMO_RECEPTION_BUFFER_SIZE;
gser_reception.ux_host_class_gser_reception_callback =
    tx_demo_thread_callback;

ux_host_class_gser_reception_start(gser, &gser_reception);
```

## <a name="ux_host_class_gser_reception_stop"></a><span data-ttu-id="5e16f-740">ux_host_class_gser_reception_stop</span><span class="sxs-lookup"><span data-stu-id="5e16f-740">ux_host_class_gser_reception_stop</span></span>

<span data-ttu-id="5e16f-741">Genel Seri arabirimde alımı durdur</span><span class="sxs-lookup"><span data-stu-id="5e16f-741">Stop reception on the generic serial interface</span></span>

### <a name="prototype"></a><span data-ttu-id="5e16f-742">Prototype</span><span class="sxs-lookup"><span data-stu-id="5e16f-742">Prototype</span></span>

```C
UINT ux_host_class_gser_reception_stop(
    UX_HOST_CLASS_GSER *gser,
    UX_HOST_CLASS_GSER_RECEPTION *gser_reception)
```

### <a name="description"></a><span data-ttu-id="5e16f-743">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5e16f-743">Description</span></span>

<span data-ttu-id="5e16f-744">Bu işlev, genel seri sınıf arabirimindeki alımı sonlandırır.</span><span class="sxs-lookup"><span data-stu-id="5e16f-744">This function stops the reception on the generic serial class interface.</span></span>

### <a name="parameters"></a><span data-ttu-id="5e16f-745">Parametreler</span><span class="sxs-lookup"><span data-stu-id="5e16f-745">Parameters</span></span>

- <span data-ttu-id="5e16f-746">**gser** Gser sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="5e16f-746">**gser** Pointer to the gser class instance.</span></span>
- <span data-ttu-id="5e16f-747">**gser_reception** Alım parametrelerini içeren yapı</span><span class="sxs-lookup"><span data-stu-id="5e16f-747">**gser_reception** Structure containing the reception parameters</span></span>

### <a name="return-value"></a><span data-ttu-id="5e16f-748">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="5e16f-748">Return Value</span></span>

- <span data-ttu-id="5e16f-749">**UX_SUCCESS** (0x00) veri aktarımı tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="5e16f-749">**UX_SUCCESS** (0x00) The data transfer was completed.</span></span>
- <span data-ttu-id="5e16f-750">**UX_HOST_CLASS_UNKNOWN** (0x59) yanlış sınıf örneği</span><span class="sxs-lookup"><span data-stu-id="5e16f-750">**UX_HOST_CLASS_UNKNOWN** (0x59) Wrong class instance</span></span>
- <span data-ttu-id="5e16f-751">**UX_ERROR** (0x01) hatası</span><span class="sxs-lookup"><span data-stu-id="5e16f-751">**UX_ERROR** (0x01) Error</span></span>

### <a name="example"></a><span data-ttu-id="5e16f-752">Örnek</span><span class="sxs-lookup"><span data-stu-id="5e16f-752">Example</span></span>

```C
/* Stops the reception for gser. */
ux_host_class_gser_reception_stop(gser, &gser_reception);
```
