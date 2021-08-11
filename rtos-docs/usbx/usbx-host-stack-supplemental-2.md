---
title: USBX konak sınıfları API 'SI
description: Bu bölümde, USBX konak sınıflarının tüm sunulan API 'Leri ele alınmaktadır.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 28e733e37b06da7053f238e23e2b8b8046df2dd9940e50cd0321ccf15c27ec47
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116802116"
---
# <a name="chapter-2-usbx-host-classes-api"></a>Bölüm 2: USBX konak sınıfları API 'SI

Bu bölümde, USBX konak sınıflarının tüm sunulan API 'Leri ele alınmaktadır. Her sınıf için aşağıdaki API 'Ler ayrıntılı olarak açıklanmıştır.

- Yazıcı sınıfı
- Ses sınıfı
- Asix sınıfı
- Pima/PTP sınıfı
- Prolific sınıfı
- Genel seri sınıf

## <a name="ux_host_class_printer_read"></a>ux_host_class_printer_read

Yazıcı arabiriminden okuyun.

### <a name="prototype"></a>Prototype

```C
UINT ux_host_class_printer_read(
    UX_HOST_CLASS_PRINTER *printer,
    UCHAR *data_pointer,
    ULONG requested_length,
    ULONG *actual_length)
```

### <a name="description"></a>Description

Bu işlev, yazıcı arabiriminden okur. Çağrı engelleniyor ve yalnızca bir hata olduğunda ya da aktarım tamamlandığında döndürülür. Okumaya yalnızca çift yönlü yazıcılarda izin verilir.

### <a name="parameters"></a>Parametreler

- **Yazıcı**: yazıcı sınıfı örneğine yönelik işaretçi.
- **data_pointer**: veri yükünün arabellek adresine yönelik işaretçi.
- **requested_length**: alınacak uzunluk.
- **actual_length**: Uzunluk gerçekten alındı.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS**: (0x00) veri aktarımı tamamlandı.
- **UX_FUNCTION_NOT_SUPPORTED**: (0x54) Yazıcı çift yönlü olmadığından işlev desteklenmiyor.
- **UX_TRANSFER_TIMEOUT**: (0x5c) aktarım zaman aşımı, okuma tamamlanmadı.

### <a name="example"></a>Örnek

```C
UINT status;

/* The following example illustrates this service. */
status = ux_host_class_printer_read(printer, data_pointer, requested_length, &actual_length);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_printer_write"></a>ux_host_class_printer_write

Yazıcı arabirimine yazın.

### <a name="prototype"></a>Prototype

```C
UINT ux_host_class_printer_write(
    UX_HOST_CLASS_PRINTER *printer,
    UCHAR *data_pointer,  
    ULONG requested_length,
    ULONG *actual_length)
```

### <a name="description"></a>Description

Bu işlev, yazıcı arabirimine yazar. Çağrı engelleniyor ve yalnızca bir hata olduğunda ya da aktarım tamamlandığında döndürülür.

### <a name="parameters"></a>Parametreler

- **Yazıcı**: yazıcı sınıfı örneğine yönelik işaretçi.
- **data_pointer**: veri yükünün arabellek adresine yönelik işaretçi.
- **requested_length**: gönderilecek uzunluk.
- **actual_length**: Uzunluk gerçekten gönderildi.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS**: (0x00) veri aktarımı tamamlandı.
- **UX_TRANSFER_TIMEOUT**: (0x5c) aktarım zaman aşımı, yazma tamamlanmamış.

### <a name="example"></a>Örnek

```C
UINT status;

/* The following example illustrates this service. */
status = ux_host_class_printer_write(printer, data_pointer, requested_length, &actual_length);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_printer_soft_reset"></a>ux_host_class_printer_soft_reset

Yazıcıya yazılımdan sıfırlama işlemi gerçekleştirin.

### <a name="prototype"></a>Prototype

```C
UINT ux_host_class_printer_soft_reset(UX_HOST_CLASS_PRINTER *printer)
```

### <a name="description"></a>Description

Bu işlev, yazıcıya geçici bir sıfırlama işlemi gerçekleştirir.

### <a name="input-parameter"></a>Giriş parametresi

- **Yazıcı**: yazıcı sınıfı örneğine yönelik işaretçi.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS**: (0x00) sıfırlama tamamlandı.
- **UX_TRANSFER_TIMEOUT**: (0x5c) aktarım zaman aşımı, sıfırlama tamamlanmadı.

### <a name="example"></a>Örnek

```C
UINT status;

/* The following example illustrates this service. */
status = ux_host_class_printer_soft_reset(printer);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_printer_status_get"></a>ux_host_class_printer_status_get

Yazıcı durumunu al

### <a name="prototype"></a>Prototype

```C
UINT ux_host_class_printer_status_get( 
    UX_HOST_CLASS_PRINTER *printer,
    ULONG *printer_status)
```

### <a name="description"></a>Description

Bu işlev, yazıcı durumunu alır. Yazıcı durumu, LPT durumuna (1284 standart) benzer.

### <a name="parameters"></a>Parametreler

- **Yazıcı**: yazıcı sınıfı örneğine yönelik işaretçi.
- **printer_status**: döndürülecek durumun adresi.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00): sıfırlama tamamlandı.
- **UX_MEMORY_INSUFFICIENT**: (0x12) işlemi gerçekleştirmek için yeterli bellek yok.
- **UX_TRANSFER_TIMEOUT**: (0x5c) aktarım zaman aşımı, sıfırlama tamamlanmadı

### <a name="example"></a>Örnek

```C
UINT status;

/* The following example illustrates this service. */
status = ux_host_class_printer_status_get(printer, printer_status);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_printer_device_id_get"></a>ux_host_class_printer_device_id_get

Yazıcı cihaz kimliğini alın.

### <a name="prototype"></a>Prototype

```C
UINT ux_host_class_printer_device_id_get( 
    UX_HOST_CLASS_PRINTER *printer,
    UCHAR *descriptor_buffer, 
    ULONG length)
```

### <a name="description"></a>Description

Bu işlev, yazıcı IEEE 1284 cihaz KIMLIĞI dizesini (big endian biçimindeki ilk iki baytın uzunluğu dahil) alır.

### <a name="parameters"></a>Parametreler

- **Yazıcı**: yazıcı sınıfı örneğine yönelik işaretçi.
- **descriptor_buffer**: IEEE 1284 cihaz kimliği dizesini (biçim olarak ilk iki baytın uzunluğu dahil) dolduracak bir arabelleğin işaretçisi 
- **uzunluk**: arabelleğin bayt cinsinden uzunluğu.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00): işlem başarılı oldu.
- **UX_MEMORY_INSUFFICIENT**: (0x12) işlemi gerçekleştirmek için yeterli bellek yok.
- **UX_TRANSFER_TIMEOUT**: (0x5c) aktarım zaman aşımı, istek tamamlanmadı
- **UX_TRANSFER_NOT_READY**: (0x25) cihaz geçersiz bir durumda, bağlı, ÇÖZÜMLENMIŞ veya yapılandırılmış olmalıdır.
- **UX_TRANSFER_STALL**: (0x21) aktarım durduruldu.
- **TX_WAIT_ABORTED** (0x1A) askıya alma başka bir iş parçacığı, ZAMANLAYıCı veya ISR tarafından iptal edildi.
- **TX_SEMAPHORE_ERROR** (0x0C) geçersiz sayma semaforu işaretçisi.
- **TX_WAIT_ERROR** (0x04) TX_NO_WAIT dışında bir bekleme seçeneği, iş parçacığından oluşan bir çağrıda belirtildi.

### <a name="example"></a>Örnek

```C
UINT status;

/* The following example illustrates this service. */
status = ux_host_class_printer_device_id_get(printer, descriptor_buffer, length);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_audio_read"></a>ux_host_class_audio_read

Ses arabiriminden okuyun.

### <a name="prototype"></a>Prototype

```C
UINT ux_host_class_audio_read(
    UX_HOST_CLASS_AUDIO *audio,
    UX_HOST_CLASS_AUDIO_TRANSFER_REQUEST
    *audio_transfer_request)
```

### <a name="description"></a>Description

Bu işlev ses arabiriminden okur. Çağrı engellenmemiş. Uygulama, ses akışı arabirimi için uygun alternatif ayarın seçildiğinden emin olmalıdır.

### <a name="parameters"></a>Parametreler

- **Ses**: ses sınıfı örneğine yönelik işaretçi.
- **audio_transfer_request**: ses aktarım yapısına yönelik işaretçi.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS**: (0x00) veri aktarımı tamamlandı
- **UX_FUNCTION_NOT_SUPPORTED**"(0x54) işlevi desteklenmiyor

### <a name="example"></a>Örnek

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

## <a name="ux_host_class_audio_write"></a>ux_host_class_audio_write

Ses arabirimine yazın.

### <a name="prototype"></a>Prototype

```C
UINT ux_host_class_audio_write(
    UX_HOST_CLASS_AUDIO *audio,
    UX_HOST_CLASS_AUDIO_TRANSFER_REQUEST *audio_transfer_request)
```

### <a name="description"></a>Description

Bu işlev ses arabirimine yazar. Çağrı engelleyici değil. Uygulama, ses akışı arabirimi için uygun alternatif ayarın seçildiğinden emin olmalı.

### <a name="parameters"></a>Parametreler

- **audio:** Ses sınıfı örneğinin işaretçisi
- **audio_transfer_request:** Ses aktarım yapısının işaretçisi

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS:**(0x00) Veri aktarımı tamamlandı.
- **UX_FUNCTION_NOT_SUPPORTED:**(0x54) İşlevi desteklenmiyor.
- **ux_host_CLASS_AUDIO_WRONG_INTERFACE:**(0x81) Arabirim yanlış.

### <a name="example"></a>Örnek

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

## <a name="ux_host_class_audio_control_get"></a>ux_host_class_audio_control_get

Ses denetimi arabiriminden belirli bir denetim elde etmek.

### <a name="prototype"></a>Prototype

```C
UINT ux_host_class_audio_control_get(
    UX_HOST_CLASS_AUDIO *audio,
    UX_HOST_CLASS_AUDIO_CONTROL *audio_control)
```

### <a name="description"></a>Description

Bu işlev, ses denetimi arabiriminden belirli bir denetimi okur.

### <a name="parameters"></a>Parametreler

- **audio:** Ses sınıfı örneğinin işaretçisi
- **audio_control:** Ses denetimi yapısının işaretçisi

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS:**(0x00) Veri aktarımı tamamlandı
- **UX_FUNCTION_NOT_SUPPORTED:**(0x54) İşlevi desteklenmiyor
- **UX_HOST_CLASS_AUDIO_WRONG_INTERFACE:**(0x81) Arabirim yanlış

### <a name="example"></a>Örnek

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

## <a name="ux_host_class_audio_control_value_set"></a>ux_host_class_audio_control_value_set

Ses denetimi arabirimine belirli bir denetim ayarlayın.

### <a name="prototype"></a>Prototype

```C
UINT ux_host_class_audio_control_value_set(
    UX_HOST_CLASS_AUDIO *audio,
    UX_HOST_CLASS_AUDIO_CONTROL *audio_control)
```

**Açıklama **

Bu işlev, ses denetimi arabirimine belirli bir denetim ayarlar.

### <a name="parameters"></a>Parametreler

- **audio:** Ses sınıfı örneğinin işaretçisi
- **audio_control:** Ses denetimi yapısının işaretçisi

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS:**(0x00) Veri aktarımı tamamlandı
- **UX_FUNCTION_NOT_SUPPORTED:**(0x54) İşlevi desteklenmiyor
- **UX_HOST_CLASS_AUDIO_WRONG_INTERFACE:**(0x81) Arabirim yanlış

### <a name="example"></a>Örnek

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

## <a name="ux_host_class_audio_streaming_sampling_set"></a>ux_host_class_audio_streaming_sampling_set

Ses akışı arabiriminin alternatif ayar arabirimini ayarlayın.

### <a name="prototype"></a>Prototype

```C
UINT ux_host_class_audio_streaming_sampling_set
    (UX_HOST_CLASS_AUDIO *audio,
    UX_HOST_CLASS_AUDIO_SAMPLING *audio_sampling)
```

### <a name="description"></a>Description

Bu işlev, belirli bir örnekleme yapısına göre ses akışı arabiriminin uygun alternatif ayar arabirimini ayarlar.

### <a name="parameters"></a>Parametreler

- **audio:** Ses sınıfı örneğinin işaretçisi.
- **audio_sampling:** Ses örnekleme yapısının işaretçisi.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS:**(0x00) Veri aktarımı tamamlandı
- **UX_FUNCTION_NOT_SUPPORTED:**(0x54) İşlevi desteklenmiyor
- **UX_HOST_CLASS_AUDIO_WRONG_INTERFACE:**(0x81) Arabirim yanlış
- **UX_NO_ALTERNATE_SETTING:**(0x5e) Örnekleme değerleri için alternatif ayar yok

### <a name="example"></a>Örnek

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

## <a name="ux_host_class_audio_streaming_sampling_get"></a>ux_host_class_audio_streaming_sampling_get

Ses akışı arabiriminin olası örnekleme ayarlarını alın.

### <a name="prototype"></a>Prototype

```C
UINT ux_host_class_audio_streaming_sampling_get(
    UX_HOST_CLASS_AUDIO *audio,
    UX_HOST_CLASS_AUDIO_SAMPLING_CHARACTERISTICS *audio_sampling)
```

### <a name="description"></a>Description

Bu işlev, ses akışı arabiriminin alternatif ayarlarının her birsinde kullanılabilen tüm olası örnekleme ayarlarını tek tek alır. İşlev ilk kez kullanılırken, çağrı yapısı işaretçisinde tüm alanların sıfır olması gerekir. İşlev, alternatif ayarların sonuna ulaşıldı değilse, dönüşte belirli bir akış değerleri kümesi geri döner. Bu işlev yeniden kullanılırken, sonraki örnekleme değerlerini bulmak için önceki örnekleme değerleri kullanılır.

### <a name="parameters"></a>Parametreler

- **audio:** Ses sınıfı örneğinin işaretçisi.
- **audio_sampling:** Ses örnekleme yapısının işaretçisi.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS:**(0x00) Veri aktarımı tamamlandı
- **UX_FUNCTION_NOT_SUPPORTED:**(0x54) İşlevi desteklenmiyor
- **UX_HOST_CLASS_AUDIO_WRONG_INTERFACE:**(0x81) Arabirim yanlış
- **UX_NO_ALTERNATE_SETTING:**(0x5e) Örnekleme değerleri için alternatif ayar yok

### <a name="example"></a>Örnek

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

## <a name="ux_host_class_asix_read"></a>ux_host_class_asix_read

Asix arabiriminden okuyun.

### <a name="prototype"></a>Prototype

```C
UINT ux_host_class_asix_read(
    UX_HOST_CLASS_ASIX *asix,
    UCHAR *data_pointer,
    ULONG requested_length,
    ULONG *actual_length)
```

### <a name="description"></a>Description

Bu işlev asix arabiriminden okur. Çağrı engelliyor ve yalnızca bir hata olduğunda veya aktarım tamamlandığında döndürür.

### <a name="parameters"></a>Parametreler

- **asix:** asix sınıf örneğinin işaretçisi.
- **data_pointer:** Veri yükünün arabellek adresinin işaretçisi.
- **requested_length:** Alınan uzunluk.
- **actual_length:** Uzunluk gerçekten alındı.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS:**(0x00) Veri aktarımı tamamlandı.
- **UX_TRANSFER_TIMEOUT:**(0x5c) Aktarım zaman aşımı, okuma tamamlanmamış.

### <a name="example"></a>Örnek

```C
UINT status;

/* The following example illustrates this service. */

status = ux_host_class_asix_read(asix, data_pointer, requested_length, &actual_length);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_asix_write"></a>ux_host_class_asix_write

Asix arabirimine yazın.

### <a name="prototype"></a>Prototype

```C
UINT ux_host_class_asix_write(
    VOID *asix_class,
    NX_PACKET *packet)
```

### <a name="description"></a>Description

Bu işlev asix arabirimine yazar. Çağrı engelleyici değil.

### <a name="parameters"></a>Parametreler

- **asix:** asix sınıf örneğinin işaretçisi.
- **paket:** Netx veri paketi

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS:**(0x00) Veri aktarımı tamamlandı.
- **UX_ERROR:**(0xFF) Aktarım isteğine neden oldu.

### <a name="example"></a>Örnek

```C
UINT status;

/* The following example illustrates this service. */

status = ux_host_class_asix_write(asix, packet);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_pima_session_open"></a>ux_host_class_pima_session_open

Başlatıcı ile Yanıtlayıcı arasında bir oturum açın.

### <a name="prototype"></a>Prototype

```C
UINT ux_host_class_pima_session_open(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session)
```

### <a name="description"></a>Description

Bu işlev, PIMA Başlatıcısı ile PIMA Yanıtlayıcı arasında bir oturum açar. Bir oturum başarıyla açıldıktan sonra PIMA komutlarının çoğu yürütülebilirsiniz.

### <a name="parameters"></a>Parametreler

- **pima:** pima sınıfı örneğinin işaretçisi.
- **pima_sessio:** PIMA oturum işaretçisi<

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS:**(0x00) Oturum başarıyla açıldı
- **UX_HOST_CLASS_PIMA_RC_SESSION_ALREADY_OPENED:**(0x201E) Oturum zaten açık

### <a name="example"></a>Örnek

```C
/* Open a pima session. */

status = ux_host_class_pima_session_open(pima, pima_session);

if (status != UX_SUCCESS)
    return(UX_PICTBRIDGE_ERROR_SESSION_NOT_OPEN);
```

## <a name="ux_host_class_pima_session_close"></a>ux_host_class_pima_session_close

Başlatıcı ile Yanıtlayıcı arasındaki oturumu kapatın.

### <a name="prototype"></a>Prototype

```C
UINT ux_host_class_pima_session_close(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session)
```

### <a name="description"></a>Description

Bu işlev daha önce PIMA Başlatıcısı ile PIMA Yanıtlayıcı arasında açılmış olan bir oturumu kapatır. Bir oturum kapatılana kadar çoğu PIMA komutu artık yürütülemeyecektir.

### <a name="parameters"></a>Parametreler

- **pima:** pima sınıfı örneğinin işaretçisi.
- **pima_session:** PIMA oturumunun işaretçisi.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS:**(0x00) Oturum kapatıldı.
- **UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN:**(0x2003) Oturum açık değil.

### <a name="example"></a>Örnek

```C
/* Close the pima session. */

status = ux_host_class_pima_session_close(pima, pima_session);
```

## <a name="ux_host_class_pima_storage_ids_get"></a>ux_host_class_pima_storage_ids_get

Yanıtlayan'dan depolama kimliği dizisini alın.

### <a name="prototype"></a>Prototype

```C
UINT ux_host_class_pima_storage_ids_get(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    ULONG *storage_ids_array,
    ULONG storage_id_length)
```

### <a name="description"></a>Description

Bu işlev yanıtlayandan depolama kimliği dizisini elde ediyor.

### <a name="parameters"></a>Parametreler

- **pima:** pima sınıfı örneğinin işaretçisi.
- **pima_session:** PIMA oturumu işaretçisi
- **storage_ids_array:** Depolama kimlikleri döndürülecek dizi
- **storage_id_length:** Depolama dizisinin uzunluğu

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS:**(0x00) Depolama Kimliği dizisi doldurulmuş
- **UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN:**(0x2003) Oturum açılamıyor
- **UX_MEMORY_INSUFFICIENT:**(0x12) PIMA komutu oluşturmak için yeterli bellek yok.

### <a name="example"></a>Örnek

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

## <a name="ux_host_class_pima_storage_info_get"></a>ux_host_class_pima_storage_info_get

Yanıtlayan'dan depolama bilgilerini alın.

### <a name="prototype"></a>Prototype

```C
UINT ux_host_class_pima_storage_info_get(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    ULONG storage_id,
    UX_HOST_CLASS_PIMA_STORAGE *storage)
```

### <a name="description"></a>Description

Bu işlev, değeri olan bir depolama kapsayıcısı için depolama bilgilerini *storage_id.*

### <a name="parameters"></a>Parametreler

- **pima:** pima sınıfı örneğinin işaretçisi.
- **pima_session:** PIMA oturumu işaretçisi
- **storage_id:** Depolama kapsayıcısı kimliği
- **depolama:** Depolama bilgileri kapsayıcısı işaretçisi

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS:**(0x00) Depolama bilgileri alındı
- **UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN:**(0x2003) Oturum açılamıyor
- **UX_MEMORY_INSUFFICIENT** (0x12) PIMA komutu oluşturmak için yeterli bellek yok.

### <a name="example"></a>Örnek

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

## <a name="ux_host_class_pima_num_objects_get"></a>ux_host_class_pima_num_objects_get

Yanıtlayan'dan bir depolama kapsayıcısı üzerinde nesne sayısını alın.

### <a name="prototype"></a>Prototype

```C
UINT ux_host_class_pima_num_objects_get(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    ULONG storage_id,
    ULONG object_format_code)
```

### <a name="description"></a>Description

Bu işlev, belirli bir biçim koduyla eşleşen belirli bir depolama kapsayıcısı storage_id nesne sayısını elde eder. Nesne sayısı şu alanda döndürülür: ux_host_class_pima_session_nb_objects yapısının pima_session döndürülür.

### <a name="parameters"></a>Parametreler

- **pima:** pima sınıfı örneğinin işaretçisi.
- **pima_session:** PIMA oturumu işaretçisi
- **storage_id:** Depolama kapsayıcısı kimliği
- **object_format_code:** Nesneler kod filtresini biçimlendirin.

Nesne Biçim Kodları aşağıdaki değerlerden birini kullanabilir.

| Nesne Biçim Kodu               | Description   |     USBX kodu                          |
|----------------------------------|---------------|------------------------------------------|
| 0x3000                           | Tanımsız Tanımlanmamış görüntü olmayan nesne | UX_HOST_CLASS_PIMA_OFC_UNDEFINED   |
| 0x3001                           | İlişki İlişkisi (örn. klasör) | UX_HOST_CLASS_PIMA_OFC_ASSOCIATION |
| 0x3002                           | Betik Cihaz modeline özgü betik | UX_HOST_CLASS_PIMA_OFC_SCRIPT      |
| 0x3003                           | Yürütülebilir Cihaz modeline özgü ikili yürütülebilir dosya | UX_HOST_CLASS_PIMA_OFC_EXECUTABLE  |
| 0x3004                           | Metin Metni dosyası  |   UX_HOST_CLASS_PIMA_OFC_TEXT        |
| 0x3005                           | HTML Köprü Metni Biçimlendirme Dili dosyası (metin) | UX_HOST_CLASS_PIMA_OFC_HTML        |
| 0x3006                           | DPOF Digital Print Order Format dosyası (metin) | UX_HOST_CLASS_PIMA_OFC_DPOF        |
| 0x3007                           | AIFF Ses klibi  |  UX_HOST_CLASS_PIMA_OFC_AIFF        |
| 0x3008                           | WAV Ses klibi   |  UX_HOST_CLASS_PIMA_OFC_WAV         |
| 0x3009                           | MP3 Ses klibi   |  UX_HOST_CLASS_PIMA_OFC_MP3         |
| 0x300A                           | AVI Video klibi   |  UX_HOST_CLASS_PIMA_OFC_AVI         |
| 0x300B                           | MPEG Video klibi  |  UX_HOST_CLASS_PIMA_OFC_MPEG        |
| 0x300C                           | ASF Microsoft Gelişmiş Akış Biçimi (video) | UX_HOST_CLASS_PIMA_OFC_ASF         |
| 0x3800                           | Tanımsız Bilinmeyen görüntü nesnesi | UX_HOST_CLASS_PIMA_OFC_QT          |
| 0x3801                           | EXIF/JPEG Değiştirilebilir Dosya Biçimi, JEIDA standardı | UX_HOST_CLASS_PIMA_OFC_EXIF_JPEG   |
| 0x3802                           | Elektronik Görüntü Için TIFF/EP Etiket Görüntü Dosyası Biçimi | UX_HOST_CLASS_PIMA_OFC_TIFF_EP     |
| 0x3803                           | FlashPix Yapılandırılmış Depolama Biçimi | UX_HOST_CLASS_PIMA_OFC_FLASHPIX    |
| 0x3804                           | BMP Microsoft Windows Bit Eşlem dosyası | UX_HOST_CLASS_PIMA_OFC_BMP         |
| 0x3805                           | CIFF Canon Kamera Görüntüsü Dosya Biçimi | UX_HOST_CLASS_PIMA_OFC_CIFF        |
| 0x3806                           | Tanımsız Ayrılmış |  |
| 0x3807                           | GIF Grafik Değişim Biçimi | UX_HOST_CLASS_PIMA_OFC_GIF         |
| 0x3808                           | JFIF JPEG Dosya Değişim Biçimi | UX_HOST_CLASS_PIMA_OFC_JFIF        |
| 0x3809                           | PCD PhotoCD Görüntü Pac | UX_HOST_CLASS_PIMA_OFC_PCD         |
| 0x380A                           | PICT Hızlı Çizim Görüntü Biçimi | UX_HOST_CLASS_PIMA_OFC_PICT        |
| 0x380B                           | PNG Taşınabilir Ağ Grafikleri | UX_HOST_CLASS_PIMA_OFC_PNG         |
| 0x380C                           | Tanımsız Ayrılmış |   |
| 0x380D                           | TIFF Etiketi Görüntü Dosyası Biçimi | UX_HOST_CLASS_PIMA_OFC_TIFF        |
| 0x380E                           | Bilgi Teknolojisi için TIFF/IT Etiketi Görüntü Dosyası Biçimi (grafik grafik) | UX_HOST_CLASS_PIMA_OFC_TIFF_IT     |
| 0x380F                           | JP2 JPEG2000 Temel Dosya Biçimi | UX_HOST_CLASS_PIMA_OFC_JP2         |
| 0x3810                           | JPX JPEG2000 Genişletilmiş Dosya Biçimi | UX_HOST_CLASS_PIMA_OFC_JPX         |
| 0011'in MSN'i ile diğer tüm kodlar | Gelecekte kullanmak üzere Tanımlanmamış Tüm Ayrılmışlar |                                    |
| 1011'in MSN'sinde diğer tüm kodlar | Satıcı Tanımlı Satıcı Tanımlı türler: Görüntü |                                    |

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS:**(0x00) Veri aktarımı tamamlandı.
- **UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN:**(0x2003) Oturum açılamıyor
- **UX_MEMORY_INSUFFICIENT:**(0x12) PIMA komutu oluşturmak için yeterli bellek yok.

### <a name="example"></a>Örnek

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

## <a name="ux_host_class_pima_object_handles_get"></a>ux_host_class_pima_object_handles_get

Yanıtlayan'dan nesne tanıtıcılarını alın.

### <a name="prototype"></a>Prototype

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

### <a name="description"></a>Description

storage_id parametresi tarafından belirtilen depolama kapsayıcısı içinde mevcut nesne storage_id döndürür. Tüm depolar genelinde toplu bir liste istenirse, bu değer 0xFFFFFFFF.

### <a name="parameters"></a>Parametreler

- **pima:** pima sınıfı örneğinin işaretçisi.
- **pima_session:** PIMA oturumu işaretçisi
- **object_handes_array:** Tanıtıcıların döndürül olduğu dizi
- **object_handles_length:** Dizinin uzunluğu
- **storage_id:** Depolama kapsayıcısı kimliği
- **object_format_code:** Nesne için kodu biçimlendirme (işlev kodu için tabloya ux_host_class_pima_num_objects_get)
- **object_handle_association:** İsteğe bağlı nesne ilişkilendirme değeri

Nesne tanıtıcısı ilişkilendirmesi aşağıdaki tabloda yer alan değerlerden biri olabilir:

| AssociationCode                        | Associationtype      | Yorum       |
|----------------------------------------|----------------------|----------------------|
| 0x0000                                 | Tanımsız            | Tanımsız            |
| 0x0001                                 | GenericFolder        | Kullanılmıyor               |
| 0x0002                                 | Albüm                | Ayrılmıştır             |
| 0x0003                                 | TimeSequence         | DefaultPlaybackDelta |
| 0x0004                                 | HorizontalPanoramic  | Kullanılmıyor               |
| 0x0005                                 | VerticalPanoramic    | Kullanılmıyor               |
| 0x0006                                 | 2DPanoramic          | ImagesPerRow         |
| 0x0007                                 | AncillaryData        | Tanımsız            |
| Bit 15 olan diğer tüm değerler 0 olarak ayarlanmıştır  | Ayrılmıştır             | Tanımsız            |
| Bit 15 değeri 1 olan tüm değerler        | Satıcı Tanımlı       | Satıcı Tanımlı       |

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS:**(0x00) Veri aktarımı tamamlandı.
- **UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN:**(0x2003) Oturum açılamıyor
- **UX_MEMORY_INSUFFICIENT:**(0x12) PIMA komutu oluşturmak için yeterli bellek yok.

### <a name="example"></a>Örnek

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

## <a name="ux_host_class_pima_object_info_get"></a>ux_host_class_pima_object_info_get

Yanıtlayan'dan nesne bilgilerini alın.

### <a name="prototype"></a>Prototype

```C
UINT ux_host_class_pima_object_info_get(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    ULONG object_handle,
    UX_HOST_CLASS_PIMA_OBJECT *object)
```

### <a name="description"></a>Description

Bu işlev, bir nesne tanıtıcısı için nesne bilgilerini elde eder.

### <a name="parameters"></a>Parametreler

- **pima:** pima sınıfı örneğinin işaretçisi.
- **pima_session:** PIMA oturumu işaretçisi
- **object_handle:** Nesnenin tanıtıcısı
- **object**: Nesne bilgisi kapsayıcısı işaretçisi

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS:**(0x00) Veri aktarımı tamamlandı.
- **UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN:**(0x2003) Oturum açılamıyor
- **UX_MEMORY_INSUFFICIENT:**(0x12) PIMA komutu oluşturmak için yeterli bellek yok.

### <a name="example"></a>Örnek

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

## <a name="ux_host_class_pima_object_info_send"></a>ux_host_class_pima_object_info_send

Nesne bilgilerini Yanıtlayan'a gönderin.

### <a name="prototype"></a>Prototype

```C
UINT ux_host_class_pima_object_info_send(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    ULONG storage_id,
    ULONG parent_object_id,
    UX_HOST_CLASS_PIMA_OBJECT *object)
```

### <a name="description"></a>Description

Bu işlev, bir depolama kapsayıcısı için depolama bilgilerini storage_id. Başlatıcı, yanıtlayıcıya nesne göndermeden önce bu komutu kullan gerekir.

### <a name="parameters"></a>Parametreler

- **pima:** pima sınıfı örneğinin işaretçisi.
- **pima_session:** PIMA oturumunun işaretçisi.
- **storage_id:** Hedef depolama kimliği.
- **parent_object_id:** Nesnenin yerleştiril gerektiği Yanıtlayan'da Üst ObjectHandle.
- **object:** Nesne bilgisi kapsayıcısı işaretçisi.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS:**(0x00) Veri aktarımı tamamlandı.
- **UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN:**(0x2003) Oturum açılamıyor
- **UX_MEMORY_INSUFFICIENT:**(0x12) PIMA komutu oluşturmak için yeterli bellek yok.

### <a name="example"></a>Örnek

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

## <a name="ux_host_class_pima_object_open"></a>ux_host_class_pima_object_open

Yanıtlayan'da depolanan bir nesneyi açın.

### <a name="prototype"></a>Prototype

```C
UINT ux_host_class_pima_object_open(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    ULONG object_handle,
    UX_HOST_CLASS_PIMA_OBJECT *object)
```

### <a name="description"></a>Description

Bu işlev okuma veya yazmadan önce yanıtlayanda bir nesnesi açar.

### <a name="parameters"></a>Parametreler

- **pima:** pima sınıfı örneğinin işaretçisi.
- **pima_session:** PIMA oturumunun işaretçisi.
- **object_handle:** nesnesinin tanıtıcısı.
- **objectc:** Nesne bilgisi kapsayıcısı işaretçisi.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS:**(0x00) Veri aktarımı tamamlandı.
- **UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN:**(0x2003) Oturum açılamıyor
- **UX_HOST_CLASS_PIMA_RC_OBJECT_ALREADY_OPENED:**(0x2021) Nesnesi zaten açılmış.
- **UX_MEMORY_INSUFFICIENT:**(0x12) PIMA komutu oluşturmak için yeterli bellek yok.

### <a name="example"></a>Örnek

```C
/* Open the object. */

status = ux_host_class_pima_object_open(pima, pima_session,
    object_handle, pima_object);

/* Check status. */
if (status != UX_SUCCESS)
    return(status);
```

## <a name="ux_host_class_pima_object_get"></a>ux_host_class_pima_object_get

Yanıtlayan'da depolanan bir nesneyi al.

### <a name="prototype"></a>Prototype

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

### <a name="description"></a>Description

Bu işlev yanıtlayanda bir nesnesi alır.

### <a name="parameters"></a>Parametreler

- **pima:** pima sınıfı örneğinin işaretçisi.
- **pima_session:** PIMA oturumu işaretçisi
- **object_handle:** nesnesinin tanıtıcısı
- **object**: Nesne bilgisi kapsayıcısı işaretçisi
- **object_buffer:** Nesne verisi adresi
- **object_buffer_length:** İstenen nesne uzunluğu
- **object_actual_length:** Döndürülen nesnenin uzunluğu

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS:**(0x00) Nesne aktarıldı
- **UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN:**(0x2003) Oturum açılamıyor
- **UX_HOST_CLASS_PIMA_RC_OBJECT_NOT_OPENED:**(0x2023) Nesne açılamıyor.
- **UX_HOST_CLASS_PIMA_RC_ACCESS_DENIED:**(0x200f) Nesne erişimi reddedildi
- **UX_HOST_CLASS_PIMA_RC_INCOMPLETE_TRANSFER:**(0x2007) Aktarım tamamlanmadı
- **UX_MEMORY_INSUFFICIENT:**(0x12) PIMA komutu oluşturmak için yeterli bellek yok.
- **UX_TRANSFER_ERROR:**(0x23) Nesne okurken aktarım hatası

### <a name="example"></a>Örnek

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

## <a name="ux_host_class_pima_object_send"></a>ux_host_class_pima_object_send

Yanıtlayan'da depolanan bir nesneyi gönderin.

### <a name="prototype"></a>Prototype

```C
UINT ux_host_class_pima_object_send(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    UX_HOST_CLASS_PIMA_OBJECT *object,
    UCHAR *object_buffer, ULONG object_buffer_length)
```

### <a name="description"></a>Description

Bu işlev yanıtlayana bir nesnesi gönderir.

### <a name="parameters"></a>Parametreler

- **pima:** pima sınıfı örneğinin işaretçisi.
- **pima_sessio:** PIMA oturumunun işaretçisi
- **object_handle:** nesnesinin tanıtıcısı
- **object**: Nesne bilgisi kapsayıcısı işaretçisi
- **object_buffer:** Nesne verisi adresi
- **object_buffer_length:** İstenen nesne uzunluğu

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS:**(0x00) Veri aktarımı tamamlandı.
- **UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN:**(0x2003) Oturum açılamıyor
- **UX_HOST_CLASS_PIMA_RC_OBJECT_NOT_OPENED:**(0x2023) Nesne açılamıyor.
- **UX_HOST_CLASS_PIMA_RC_ACCESS_DENIED:**(0x200f) Nesne erişimi reddedildi
- **UX_HOST_CLASS_PIMA_RC_INCOMPLETE_TRANSFER:**(0x2007) Aktarım tamamlanmadı
- **UX_MEMORY_INSUFFICIENT:**(0x12) PIMA komutu oluşturmak için yeterli bellek yok.
- **UX_TRANSFER_ERROR:**(0x23) Nesne yazarken aktarım hatası

### <a name="example"></a>Örnek

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

## <a name="ux_host_class_pima_thumb_get"></a>ux_host_class_pima_thumb_get

Yanıtlayan'da depolanan bir parmak nesnesi elde edersiniz.

### <a name="prototype"></a>Prototype

```C
UINT ux_host_class_pima_thumb_get(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    ULONG object_handle,
    UX_HOST_CLASS_PIMA_OBJECT *object,
    UCHAR *thumb_buffer, ULONG thumb_buffer_length,
    ULONG *thumb_actual_length)
```

### <a name="description"></a>Description

Bu işlev yanıtlayanda bir parmak nesnesi alır.

### <a name="parameters"></a>Parametreler

- **pima:** pima sınıfı örneğinin işaretçisi.
- **pima_session:** PIMA oturumunun işaretçisi.
- **object_handle:** nesnesinin tanıtıcısı.
- **object:** Nesne bilgisi kapsayıcısı işaretçisi.
- **thumb_buffer:** Parmak nesne verisi adresi.
- **thumb_buffer_length:** İstenen başparmak nesnesi uzunluğu.
- **thumb_actual_length:** Döndürülen başparmak nesnesinin uzunluğu.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS:**(0x00) Veri aktarımı tamamlandı.
- **UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN:**(0x2003) Oturum açık değil.
- **UX_HOST_CLASS_PIMA_RC_OBJECT_NOT_OPENED:**(0x2023) Nesne açılamıyor.
- **UX_HOST_CLASS_PIMA_RC_ACCESS_DENIED:**(0x200f) Nesne erişimi reddedildi.
- **UX_HOST_CLASS_PIMA_RC_INCOMPLETE_TRANSFER:**(0x2007) Aktarım tamamlanmadı.
- **UX_MEMORY_INSUFFICIENT:**(0x12) PIMA komutu oluşturmak için yeterli bellek yok.
- **UX_TRANSFER_ERROR:**(0x23) Nesne okurken aktarım hatası.

### <a name="example"></a>Örnek

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

## <a name="ux_host_class_pima_object_delete"></a>ux_host_class_pima_object_delete

Yanıtlayan'da depolanan bir nesneyi silin.

### <a name="prototype"></a>Prototype

```C
UINT ux_host_class_pima_object_delete(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    ULONG object_handle)
```

### <a name="description"></a>Description

Bu işlev yanıtlayanda bir nesneyi siler

### <a name="parameters"></a>Parametreler

- **pima:** pima sınıfı örneğinin işaretçisi.
- **pima_session:** PIMA oturumu işaretçisi
- **object_handle:** nesnesinin tanıtıcısı

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS:**(0x00) Nesne silindi.
- **UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN:**(0x2003) Oturum açık değil.
- **UX_HOST_CLASS_PIMA_RC_ACCESS_DENIED:**(0x200f) Nesne silinamadı.
- **UX_MEMORY_INSUFFICIENT:**(0x12) PIMA komutu oluşturmak için yeterli bellek yok.

### <a name="example"></a>Örnek

```C
/* Delete the object. */
status = ux_host_class_pima_object_delete(pima, pima_session, object_handle, pima_object);

/* Check status. */
if (status != UX_SUCCESS)
    return(status);
```

## <a name="ux_host_class_pima_object_close"></a>ux_host_class_pima_object_close

Yanıtlayan'da depolanan bir nesneyi kapatma

### <a name="prototype"></a>Prototype

```C
UINT ux_host_class_pima_object_close(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    ULONG object_handle, UX_HOST_CLASS_PIMA_OBJECT *object)
```

### <a name="description"></a>Description

Bu işlev yanıtlayanda bir nesneyi kapatır.

### <a name="parameters"></a>Parametreler

- **pima:** pima sınıfı örneğinin işaretçisi.
- **pima_session:** PIMA oturumunun işaretçisi.
- **object_handle:** Nesnenin tanıtıcısı.
- **object:** Nesnenin işaretçisi.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS:**(0x00) Nesne kapatıldı.
- **UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN:**(0x2003) Oturum açık değil.
- **UX_HOST_CLASS_PIMA_RC_OBJECT_NOT_OPENED:**(0x2023) Nesne açılamıyor.
- **UX_MEMORY_INSUFFICIENT:**(0x12) PIMA komutu oluşturmak için yeterli bellek yok.

### <a name="example"></a>Örnek

```C
/* Close the object. */
status = ux_host_class_pima_object_close(pima, pima_session, object_handle, object);
```

## <a name="ux_host_class_gser_read"></a>ux_host_class_gser_read

Genel seri arabiriminden okuyun.

### <a name="prototype"></a>Prototype

```C
UINT ux_host_class_gser_read(
    UX_HOST_CLASS_GSER *gser,
    ULONG interface_index,
    UCHAR *data_pointer,
    ULONG requested_length,
    ULONG *actual_length)
```

### <a name="description"></a>Description

Bu işlev genel seri arabiriminden okur. Çağrı engelliyor ve yalnızca bir hata olduğunda veya aktarım tamamlandığında döndürür.

### <a name="parameters"></a>Parametreler

- **gser:** gser sınıf örneğinin işaretçisi.
- **interface_index:** Okunan arabirim dizini.
- **data_pointer:** Veri yükünün arabellek adresinin işaretçisi.
- **requested_length:** Alınan uzunluk.
- **actual_length:** Uzunluk gerçekten alındı.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS:**(0x00) Veri aktarımı tamamlandı.
- **UX_TRANSFER_TIMEOUT:**(0x5c) Aktarım zaman aşımı, okuma tamamlanmamış.

### <a name="example"></a>Örnek

```C
UINT status;

/* The following example illustrates this service. */
status = ux_host_class_gser_read(cdc_acm, interface_index,data_pointer, requested_length, &actual_length);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_gser_write"></a>ux_host_class_gser_write

Genel seri arabirimine yazın.

### <a name="prototype"></a>Prototype

```C
UINT ux_host_class_gser_write(
    UX_HOST_CLASS_GSER *gser,
    ULONG interface_index,
    UCHAR *data_pointer,
    ULONG requested_length,
    ULONG *actual_length)
```

### <a name="description"></a>Description

Bu işlev genel seri arabirimine yazar. Çağrı engelliyor ve yalnızca bir hata olduğunda veya aktarım tamamlandığında döndürür.

### <a name="parameters"></a>Parametreler

- **gser:** gser sınıf örneğinin işaretçisi.
- **interface_index:** Yazacak arabirim.
- **data_pointer:** Veri yükünün arabellek adresinin işaretçisi.
- **requested_length:** Gönderilecek uzunluk.
- **actual_length:** Uzunluk aslında gönderilir.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS:**(0x00) Veri aktarımı tamamlandı.
- **UX_TRANSFER_TIMEOUT:**(0x5c) Aktarım zaman aşımı, yazma eksik.

### <a name="example"></a>Örnek

```C
UINT status;

/* The following example illustrates this service. */
status = ux_host_class_cdc_acm_write(gser, data_pointer, requested_length, &actual_length);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_gser_ioctl"></a>ux_host_class_gser_ioctl

Genel seri arabirime bir IOCTL işlevi gerçekleştirin.

### <a name="prototype"></a>Prototype

```C
UINT ux_host_class_gser_ioctl(
    UX_HOST_CLASS_GSER *gser,
    ULONG ioctl_function,
    VOID *parameter)
```

### <a name="description"></a>Description

Bu işlev, gser arabirimine belirli bir ioctl işlevini gerçekleştirir. Çağrı engelliyor ve yalnızca bir hata olduğunda veya komut tamamlandığında döndürür.

### <a name="parameters"></a>Parametreler

- **gser:** gser sınıf örneğinin işaretçisi.
- **ioctl_function:** gerçekleştirilecek ioctl işlevi. İzin verilen ioctl işlevlerinden biri için aşağıdaki tabloya bakın.
- **parameter:** ioctl'ye özgü bir parametrenin işaretçisi

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS:**(0x00) Veri aktarımı tamamlandı.
- **UX_MEMORY_INSUFFICIENT:**(0x12) Yeterli bellek yok.
- **UX_HOST_CLASS_UNKNOWN:**(0x59) Yanlış sınıf örneği
- **UX_FUNCTION_NOT_SUPPORTED:**(0x54) Bilinmeyen IOCTL işlevi.

### <a name="ioctl-functions"></a>IOCTL işlevleri

- UX_HOST_CLASS_GSER_IOCTL_SET_LINE_CODING
- UX_HOST_CLASS_GSER_IOCTL_GET_LINE_CODING
- UX_HOST_CLASS_GSER_IOCTL_SET_LINE_STATE
- UX_HOST_CLASS_GSER_IOCTL_SEND_BREAK
- UX_HOST_CLASS_GSER_IOCTL_ABORT_IN_PIPE
- UX_HOST_CLASS_GSER_IOCTL_ABORT_OUT_PIPE
- UX_HOST_CLASS_GSER_IOCTL_NOTIFICATION_CALLBACK
- UX_HOST_CLASS_GSER_IOCTL_GET_DEVICE_STATUS

### <a name="example"></a>Örnek

```C
UINT status;

/* The following example illustrates this service. */

status = ux_host_class_gser_ioctl(gser,
    UX_HOST_CLASS_GSER_IOCTL_GET_LINE_CODING,
    (VOID *)&line_coding);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_gser_reception_start"></a>ux_host_class_gser_reception_start

Genel seri arabiriminde alımı başlatma

### <a name="prototype"></a>Prototype

```C
UINT ux_host_class_gser_reception_start(
    UX_HOST_CLASS_GSER *gser,
    UX_HOST_CLASS_GSER_RECEPTION *gser_reception)
```

### <a name="description"></a>Description

Bu işlev, genel seri sınıf arabiriminde sinyal alımını başlatır. Bu işlev engelleyici olmayan sinyal alımına olanak sağlar. Bir arabellek alınca, içinde bir geri çağırma uygulamaya çağrılır.

### <a name="parameters"></a>Parametreler

- **gser** gser sınıfı örneğinin işaretçisi.
- **gser_reception** Sinyal parametrelerini içeren yapı

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) Veri aktarımı tamamlandı.
- **UX_HOST_CLASS_UNKNOWN** (0x59) Yanlış sınıf örneği
- **UX_ERROR** (0x01) Hatası

### <a name="example"></a>Örnek

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

## <a name="ux_host_class_gser_reception_stop"></a>ux_host_class_gser_reception_stop

Genel seri arabirimde alımı durdurma

### <a name="prototype"></a>Prototype

```C
UINT ux_host_class_gser_reception_stop(
    UX_HOST_CLASS_GSER *gser,
    UX_HOST_CLASS_GSER_RECEPTION *gser_reception)
```

### <a name="description"></a>Description

Bu işlev, genel seri sınıf arabiriminde alımı durdurur.

### <a name="parameters"></a>Parametreler

- **gser** gser sınıfı örneğinin işaretçisi.
- **gser_reception** Sinyal parametrelerini içeren yapı

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) Veri aktarımı tamamlandı.
- **UX_HOST_CLASS_UNKNOWN** (0x59) Yanlış sınıf örneği
- **UX_ERROR** (0x01) Hatası

### <a name="example"></a>Örnek

```C
/* Stops the reception for gser. */
ux_host_class_gser_reception_stop(gser, &gser_reception);
```
