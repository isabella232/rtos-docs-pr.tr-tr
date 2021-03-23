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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

Bu işlev ses arabirimine yazar. Çağrı engellenmemiş. Uygulama, ses akışı arabirimi için uygun alternatif ayarın seçildiğinden emin olmalıdır.

### <a name="parameters"></a>Parametreler

- **Ses**: ses sınıfı örneğine yönelik işaretçi
- **audio_transfer_request**: ses aktarım yapısına yönelik işaretçi

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS**: (0x00) veri aktarımı tamamlandı.
- **UX_FUNCTION_NOT_SUPPORTED**: (0x54) işlev desteklenmiyor.
- **ux_host_CLASS_AUDIO_WRONG_INTERFACE**: (0x81) arabirimi yanlış.

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

Ses denetim arabiriminden belirli bir denetim alın.

### <a name="prototype"></a>Prototype

```C
UINT ux_host_class_audio_control_get(
    UX_HOST_CLASS_AUDIO *audio,
    UX_HOST_CLASS_AUDIO_CONTROL *audio_control)
```

### <a name="description"></a>Açıklama

Bu işlev, ses denetim arabiriminden belirli bir denetimi okur.

### <a name="parameters"></a>Parametreler

- **Ses**: ses sınıfı örneğine yönelik işaretçi
- **audio_control**: ses denetimi yapısına yönelik işaretçi

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS**: (0x00) veri aktarımı tamamlandı
- **UX_FUNCTION_NOT_SUPPORTED**: (0x54) işlev desteklenmiyor
- **UX_HOST_CLASS_AUDIO_WRONG_INTERFACE**: (0x81) arabirim yanlış

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

Ses denetim arabirimine belirli bir denetim ayarlayın.

### <a name="prototype"></a>Prototype

```C
UINT ux_host_class_audio_control_value_set(
    UX_HOST_CLASS_AUDIO *audio,
    UX_HOST_CLASS_AUDIO_CONTROL *audio_control)
```

* * Açıklama * *

Bu işlev, ses denetim arabirimine belirli bir denetim ayarlar.

### <a name="parameters"></a>Parametreler

- **Ses**: ses sınıfı örneğine yönelik işaretçi
- **audio_control**: ses denetimi yapısına yönelik işaretçi

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS**: (0x00) veri aktarımı tamamlandı
- **UX_FUNCTION_NOT_SUPPORTED**: (0x54) işlev desteklenmiyor
- **UX_HOST_CLASS_AUDIO_WRONG_INTERFACE**: (0x81) arabirim yanlış

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

### <a name="description"></a>Açıklama

Bu işlev, ses akış arabiriminin uygun alternatif ayar arabirimini belirli bir örnekleme yapısına göre ayarlar.

### <a name="parameters"></a>Parametreler

- **Ses**: ses sınıfı örneğine yönelik işaretçi.
- **audio_sampling**: ses örnekleme yapısına yönelik işaretçi.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS**: (0x00) veri aktarımı tamamlandı
- **UX_FUNCTION_NOT_SUPPORTED**: (0x54) işlev desteklenmiyor
- **UX_HOST_CLASS_AUDIO_WRONG_INTERFACE**: (0x81) arabirim yanlış
- **UX_NO_ALTERNATE_SETTING**: (0x5E) örnekleme değerleri için alternatif ayar yok

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

Ses akışı arabiriminin olası örnekleme ayarlarını öğrenin.

### <a name="prototype"></a>Prototype

```C
UINT ux_host_class_audio_streaming_sampling_get(
    UX_HOST_CLASS_AUDIO *audio,
    UX_HOST_CLASS_AUDIO_SAMPLING_CHARACTERISTICS *audio_sampling)
```

### <a name="description"></a>Açıklama

Bu işlev, bir diğeri, ses akış arabiriminin alternatif ayarlarında bulunan tüm olası örnekleme ayarlarını alır. İşlev ilk kez kullanıldığında, çağırma yapısı işaretçisindeki tüm alanların sıfırlanması gerekir. Bu işlev, alternatif ayarların sonuna ulaşılmadığı takdirde, return üzerinde belirli bir akış değeri kümesi döndürür. Bu işlev yeniden kullanıldığında, sonraki örnekleme değerlerini bulmak için önceki örnekleme değerleri kullanılacaktır.

### <a name="parameters"></a>Parametreler

- **Ses**: ses sınıfı örneğine yönelik işaretçi.
- **audio_sampling**: ses örnekleme yapısına yönelik işaretçi.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS**: (0x00) veri aktarımı tamamlandı
- **UX_FUNCTION_NOT_SUPPORTED**: (0x54) işlev desteklenmiyor
- **UX_HOST_CLASS_AUDIO_WRONG_INTERFACE**: (0x81) arabirim yanlış
- **UX_NO_ALTERNATE_SETTING**: (0x5E) örnekleme değerleri için alternatif ayar yok

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

### <a name="description"></a>Açıklama

Bu işlev, asix arabiriminden okur. Çağrı engelleniyor ve yalnızca bir hata olduğunda ya da aktarım tamamlandığında döndürülür.

### <a name="parameters"></a>Parametreler

- **asix**: aaltısınıf örneği işaretçisi.
- **data_pointer**: veri yükünün arabellek adresine yönelik işaretçi.
- **requested_length**: alınacak uzunluk.
- **actual_length**: Uzunluk gerçekten alındı.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS**: (0x00) veri aktarımı tamamlandı.
- **UX_TRANSFER_TIMEOUT**: (0x5c) aktarım zaman aşımı, okuma tamamlanmadı.

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

### <a name="description"></a>Açıklama

Bu işlev, asix arabirimine yazar. Çağrı engellenmeyen bir.

### <a name="parameters"></a>Parametreler

- **asix**: aaltısınıf örneği işaretçisi.
- **paket**: NETX veri paketi

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS**: (0x00) veri aktarımı tamamlandı.
- **UX_ERROR**: (0xFF) aktarma istendi.

### <a name="example"></a>Örnek

```C
UINT status;

/* The following example illustrates this service. */

status = ux_host_class_asix_write(asix, packet);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_pima_session_open"></a>ux_host_class_pima_session_open

Başlatıcı ve Yanıtlayıcı arasında bir oturum açın.

### <a name="prototype"></a>Prototype

```C
UINT ux_host_class_pima_session_open(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session)
```

### <a name="description"></a>Açıklama

Bu işlev, bir PIMA başlatıcısı ile bir PIMA Yanıtlayıcısı arasında bir oturum açar. Bir oturum başarıyla açıldıktan sonra, çoğu PIMA komutları yürütülebilir.

### <a name="parameters"></a>Parametreler

- **Pima**: Pima sınıfı örneğine yönelik işaretçi.
- **pima_sessio**: Pima oturumu< işaretçisi

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS**: (0x00) oturum başarıyla açıldı
- **UX_HOST_CLASS_PIMA_RC_SESSION_ALREADY_OPENED**: (0X201e) oturum zaten açık

### <a name="example"></a>Örnek

```C
/* Open a pima session. */

status = ux_host_class_pima_session_open(pima, pima_session);

if (status != UX_SUCCESS)
    return(UX_PICTBRIDGE_ERROR_SESSION_NOT_OPEN);
```

## <a name="ux_host_class_pima_session_close"></a>ux_host_class_pima_session_close

Başlatıcı ve Yanıtlayıcı arasında bir oturumu kapatın.

### <a name="prototype"></a>Prototype

```C
UINT ux_host_class_pima_session_close(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session)
```

### <a name="description"></a>Açıklama

Bu işlev, daha önce bir PIMA başlatıcısı ve bir PIMA Yanıtlayıcısı arasında açılan bir oturumu kapatır. Bir oturum kapatıldıktan sonra, çoğu PIMA komutları artık yürütülemez.

### <a name="parameters"></a>Parametreler

- **Pima**: Pima sınıfı örneğine yönelik işaretçi.
- **pima_session**: Pima oturumuna yönelik işaretçi.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS**: (0x00) oturum kapatıldı.
- **UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) oturum açılmadı.

### <a name="example"></a>Örnek

```C
/* Close the pima session. */

status = ux_host_class_pima_session_close(pima, pima_session);
```

## <a name="ux_host_class_pima_storage_ids_get"></a>ux_host_class_pima_storage_ids_get

Yanıtlayanın depolama KIMLIĞI dizisini edinin.

### <a name="prototype"></a>Prototype

```C
UINT ux_host_class_pima_storage_ids_get(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    ULONG *storage_ids_array,
    ULONG storage_id_length)
```

### <a name="description"></a>Açıklama

Bu işlev, yanıtlayanın depolama KIMLIĞI dizisini edinir.

### <a name="parameters"></a>Parametreler

- **Pima**: Pima sınıfı örneğine yönelik işaretçi.
- **pima_session**: Pima oturumuna yönelik işaretçi
- **storage_ids_array**: depolama kimliklerinin döndürüldüğü dizi
- **storage_id_length**: depolama dizisinin uzunluğu

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS**: (0x00) depolama kimliği dizisi doldurulmuş
- **UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) oturum açılmadı
- **UX_MEMORY_INSUFFICIENT**: (0x12) Pima komutu oluşturmak için yeterli bellek yok.

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

Yanıtlayanın depolama bilgilerini alın.

### <a name="prototype"></a>Prototype

```C
UINT ux_host_class_pima_storage_info_get(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    ULONG storage_id,
    UX_HOST_CLASS_PIMA_STORAGE *storage)
```

### <a name="description"></a>Açıklama

Bu işlev, *storage_id* bir depolama kapsayıcısı için depolama bilgilerini edinir.

### <a name="parameters"></a>Parametreler

- **Pima**: Pima sınıfı örneğine yönelik işaretçi.
- **pima_session**: Pima oturumuna yönelik işaretçi
- **storage_id**: depolama kapsayıcısının kimliği
- **depolama**: depolama bilgileri kapsayıcısına yönelik işaretçi

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS**: (0x00) depolama bilgileri alındı
- **UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) oturum açılmadı
- **UX_MEMORY_INSUFFICIENT** (0x12) Pima komutu oluşturmak için yeterli bellek yok.

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

Yanıtlayıcı 'dan bir depolama kapsayıcısındaki nesne sayısını alın.

### <a name="prototype"></a>Prototype

```C
UINT ux_host_class_pima_num_objects_get(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    ULONG storage_id,
    ULONG object_format_code)
```

### <a name="description"></a>Açıklama

Bu işlev, belirli bir biçim kodu ile eşleşen storage_id belirli bir depolama kapsayıcısında depolanan nesne sayısını alır. Nesne sayısı, pima_session yapısının ux_host_class_pima_session_nb_objects: alanına döndürülür.

### <a name="parameters"></a>Parametreler

- **Pima**: Pima sınıfı örneğine yönelik işaretçi.
- **pima_session**: Pima oturumuna yönelik işaretçi
- **storage_id**: depolama kapsayıcısının kimliği
- **object_format_code**: nesne biçimi kodu filtresi.

Nesne biçim kodları aşağıdaki değerlerden birine sahip olabilir.

| Nesne biçim kodu               | Açıklama   |     USBX kodu                          |
|----------------------------------|---------------|------------------------------------------|
| 0x3000                           | Tanımsız tanımsız görüntü olmayan nesne | UX_HOST_CLASS_PIMA_OFC_UNDEFINED   |
| 0x3001                           | İlişki Ilişkilendirmesi (ör. klasörü) | UX_HOST_CLASS_PIMA_OFC_ASSOCIATION |
| 0x3002                           | Betik cihazı-modele özgü betik | UX_HOST_CLASS_PIMA_OFC_SCRIPT      |
| 0x3003                           | Yürütülebilir cihaz modeline özgü ikili yürütülebilir dosya | UX_HOST_CLASS_PIMA_OFC_EXECUTABLE  |
| 0x3004                           | Metin metin dosyası  |   UX_HOST_CLASS_PIMA_OFC_TEXT        |
| 0x3005                           | HTML köprü metni biçimlendirme dili dosyası (metin) | UX_HOST_CLASS_PIMA_OFC_HTML        |
| 0x3006                           | DPOF dijital yazdırma sırası biçim dosyası (metin) | UX_HOST_CLASS_PIMA_OFC_DPOF        |
| 0x3007                           | AıFF ses klibi  |  UX_HOST_CLASS_PIMA_OFC_AIFF        |
| 0x3008                           | WAV ses klibi   |  UX_HOST_CLASS_PIMA_OFC_WAV         |
| 0x3009                           | MP3 ses klibi   |  UX_HOST_CLASS_PIMA_OFC_MP3         |
| 0x300A                           | AVI video klibi   |  UX_HOST_CLASS_PIMA_OFC_AVI         |
| 0x300B                           | MPEG video klibi  |  UX_HOST_CLASS_PIMA_OFC_MPEG        |
| 0x300C                           | ASF Microsoft Gelişmiş akış biçimi (video) | UX_HOST_CLASS_PIMA_OFC_ASF         |
| 0x3800                           | Tanımsız bilinmeyen görüntü nesnesi | UX_HOST_CLASS_PIMA_OFC_QT          |
| 0x3801                           | EXIF/JPEG takas edilebilir dosya biçimi, JEIDA standart | UX_HOST_CLASS_PIMA_OFC_EXIF_JPEG   |
| 0x3802                           | Elektronik Fotoğrafçılık için TIFF/EP etiketi resim dosyası biçimi | UX_HOST_CLASS_PIMA_OFC_TIFF_EP     |
| 0x3803                           | FlashPix yapılandırılmış depolama görüntü biçimi | UX_HOST_CLASS_PIMA_OFC_FLASHPIX    |
| 0x3804                           | BMP Microsoft Windows bit eşlem dosyası | UX_HOST_CLASS_PIMA_OFC_BMP         |
| 0x3805                           | CFF Canon kamera resim dosyası biçimi | UX_HOST_CLASS_PIMA_OFC_CIFF        |
| 0x3806                           | Tanımsız ayrılmış |  |
| 0x3807                           | GIF Grafik Değişim Biçimi | UX_HOST_CLASS_PIMA_OFC_GIF         |
| 0x3808                           | JJPEG dosya değişim biçimi | UX_HOST_CLASS_PIMA_OFC_JFIF        |
| 0x3809                           | PCD PhotoCD Image Pac | UX_HOST_CLASS_PIMA_OFC_PCD         |
| 0x380A                           | PICT QuickDraw resim biçimi | UX_HOST_CLASS_PIMA_OFC_PICT        |
| 0x380B                           | PNG Taşınabilir Ağ Grafikleri | UX_HOST_CLASS_PIMA_OFC_PNG         |
| 0x380C                           | Tanımsız ayrılmış |   |
| 0x380D                           | TIFF etiketi resim dosyası biçimi | UX_HOST_CLASS_PIMA_OFC_TIFF        |
| 0x380E                           | Bilgi teknolojisi için TIFF/It etiketi görüntü dosyası biçimi (grafik sanatları) | UX_HOST_CLASS_PIMA_OFC_TIFF_IT     |
| 0x380F                           | JP2 JPEG2000 ana hat dosyası biçimi | UX_HOST_CLASS_PIMA_OFC_JP2         |
| 0x3810                           | JPX JPEG2000 genişletilmiş dosya biçimi | UX_HOST_CLASS_PIMA_OFC_JPX         |
| 0011 MSN ile diğer tüm kodlar | Gelecekte kullanılmak üzere hiçbir tanımsız ayrılmış |                                    |
| MSN 1011 ile diğer tüm kodlar | Satıcı tanımlı satıcı tanımlı tür: görüntü |                                    |

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS**: (0x00) veri aktarımı tamamlandı.
- **UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) oturum açılmadı
- **UX_MEMORY_INSUFFICIENT**: (0x12) Pima komutu oluşturmak için yeterli bellek yok.

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

Yanıtlayanın nesne tutamaçlarını alın.

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

### <a name="description"></a>Açıklama

Storage_id parametresiyle belirtilen depolama kapsayıcısında bulunan nesne tanıtıcılarının dizisini döndürür. Tüm mağazaların içindeki toplanmış bir liste isteniyorsa, bu değer 0xFFFFFFFF olarak ayarlanmalıdır.

### <a name="parameters"></a>Parametreler

- **Pima**: Pima sınıfı örneğine yönelik işaretçi.
- **pima_session**: Pima oturumuna yönelik işaretçi
- **object_handes_array**: tanıtıcıların döndürüldüğü dizi
- **object_handles_length**: dizinin uzunluğu
- **storage_id**: depolama kapsayıcısının kimliği
- **object_format_code**: nesne için biçim kodu (bkz. işlev için tablo ux_host_class_pima_num_objects_get)
- **object_handle_association**: isteğe bağlı nesne ilişkilendirme değeri

Nesne tanıtıcısı ilişkilendirmesi aşağıdaki tablodaki değerden biri olabilir:

| Ilişki kodu                        | AssociationType      | Yorum       |
|----------------------------------------|----------------------|----------------------|
| 0x0000                                 | Tanımlayan            | Tanımlayan            |
| 0x0001                                 | GenericFolder        | Kullanılmıyor               |
| 0x0002                                 | Albümün                | Ayrılmıştır             |
| 0x0003                                 | TimeSequence         | DefaultPlaybackDelta |
| 0x0004                                 | Horizontalpanoramik  | Kullanılmıyor               |
| 0x0005                                 | Verticalpanoramik    | Kullanılmıyor               |
| 0x0006                                 | 2Dpanoramik          | Imaperrow         |
| 0x0007                                 | Anlari verileri        | Tanımlayan            |
| Bit 15 olan diğer tüm değerler 0 olarak ayarlanmıştır  | Ayrılmıştır             | Tanımlayan            |
| Bit 15 olan tüm değerler 1 olarak ayarlanmıştır        | Satıcı tanımlı       | Satıcı tanımlı       |

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS**: (0x00) veri aktarımı tamamlandı.
- **UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) oturum açılmadı
- **UX_MEMORY_INSUFFICIENT**: (0x12) Pima komutu oluşturmak için yeterli bellek yok.

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

Yanıtlayanın nesne bilgilerini alın.

### <a name="prototype"></a>Prototype

```C
UINT ux_host_class_pima_object_info_get(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    ULONG object_handle,
    UX_HOST_CLASS_PIMA_OBJECT *object)
```

### <a name="description"></a>Açıklama

Bu işlev, nesne tanıtıcısı için nesne bilgilerini edinir.

### <a name="parameters"></a>Parametreler

- **Pima**: Pima sınıfı örneğine yönelik işaretçi.
- **pima_session**: Pima oturumuna yönelik işaretçi
- **object_handle**: nesnenin tanıtıcısı
- **nesne**: nesne bilgisi kapsayıcısının işaretçisi

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS**: (0x00) veri aktarımı tamamlandı.
- **UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) oturum açılmadı
- **UX_MEMORY_INSUFFICIENT**: (0x12) Pima komutu oluşturmak için yeterli bellek yok.

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

Nesne bilgilerini Yanıtlayıcıya gönderin.

### <a name="prototype"></a>Prototype

```C
UINT ux_host_class_pima_object_info_send(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    ULONG storage_id,
    ULONG parent_object_id,
    UX_HOST_CLASS_PIMA_OBJECT *object)
```

### <a name="description"></a>Açıklama

Bu işlev, storage_id değer bir depolama kapsayıcısı için depolama bilgilerini gönderir. Başlatıcı, bir nesneyi yanıtlayanın göndermeden önce bu komutu kullanmalıdır.

### <a name="parameters"></a>Parametreler

- **Pima**: Pima sınıfı örneğine yönelik işaretçi.
- **pima_session**: Pima oturumuna yönelik işaretçi.
- **storage_id**: hedef depolama kimliği.
- **parent_object_id**: nesnenin yerleştirilmesi gereken yanıtlayana ObjectHandle.
- **nesne**: nesne bilgisi kapsayıcısının işaretçisi.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS**: (0x00) veri aktarımı tamamlandı.
- **UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) oturum açılmadı
- **UX_MEMORY_INSUFFICIENT**: (0x12) Pima komutu oluşturmak için yeterli bellek yok.

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

Yanıtlayanda depolanan bir nesneyi açın.

### <a name="prototype"></a>Prototype

```C
UINT ux_host_class_pima_object_open(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    ULONG object_handle,
    UX_HOST_CLASS_PIMA_OBJECT *object)
```

### <a name="description"></a>Açıklama

Bu işlev, okumadan veya yazmadan önce Yanıtlayıcı üzerinde bir nesne açar.

### <a name="parameters"></a>Parametreler

- **Pima**: Pima sınıfı örneğine yönelik işaretçi.
- **pima_session**: Pima oturumuna yönelik işaretçi.
- **object_handle**: nesnenin tanıtıcısı.
- **objec**: nesne bilgisi kapsayıcısına yönelik işaretçi.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS**: (0x00) veri aktarımı tamamlandı.
- **UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) oturum açılmadı
- **UX_HOST_CLASS_PIMA_RC_OBJECT_ALREADY_OPENED**: (0X2021) nesne zaten açık.
- **UX_MEMORY_INSUFFICIENT**: (0x12) Pima komutu oluşturmak için yeterli bellek yok.

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

Yanıtlayanda depolanan bir nesne alın.

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

### <a name="description"></a>Açıklama

Bu işlev, Yanıtlayıcıda bir nesne alır.

### <a name="parameters"></a>Parametreler

- **Pima**: Pima sınıfı örneğine yönelik işaretçi.
- **pima_session**: Pima oturumuna yönelik işaretçi
- **object_handle**: nesnenin tanıtıcısı
- **nesne**: nesne bilgisi kapsayıcısının işaretçisi
- **object_buffer**: nesne verilerinin adresi
- **object_buffer_length**: istenen nesne uzunluğu
- **object_actual_length**: döndürülen nesne uzunluğu

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS**: (0x00) nesne aktarıldı
- **UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) oturum açılmadı
- **UX_HOST_CLASS_PIMA_RC_OBJECT_NOT_OPENED**: (0X2023) nesnesi açılmadı.
- **UX_HOST_CLASS_PIMA_RC_ACCESS_DENIED**: (0x200f) nesne erişimi reddedildi
- **UX_HOST_CLASS_PIMA_RC_INCOMPLETE_TRANSFER**: (0x2007) aktarım tamamlanmadı
- **UX_MEMORY_INSUFFICIENT**: (0x12) Pima komutu oluşturmak için yeterli bellek yok.
- **UX_TRANSFER_ERROR**: (0x23) nesne okunurken aktarım hatası oluştu

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

Yanıtlayanda depolanan bir nesne gönderin.

### <a name="prototype"></a>Prototype

```C
UINT ux_host_class_pima_object_send(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    UX_HOST_CLASS_PIMA_OBJECT *object,
    UCHAR *object_buffer, ULONG object_buffer_length)
```

### <a name="description"></a>Açıklama

Bu işlev, Yanıtlayıcıya bir nesnesi gönderir.

### <a name="parameters"></a>Parametreler

- **Pima**: Pima sınıfı örneğine yönelik işaretçi.
- **pima_sessio**: Pima oturumuna yönelik işaretçi
- **object_handle**: nesnenin tanıtıcısı
- **nesne**: nesne bilgisi kapsayıcısının işaretçisi
- **object_buffer**: nesne verilerinin adresi
- **object_buffer_length**: istenen nesne uzunluğu

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS**: (0x00) veri aktarımı tamamlandı.
- **UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) oturum açılmadı
- **UX_HOST_CLASS_PIMA_RC_OBJECT_NOT_OPENED**: (0X2023) nesnesi açılmadı.
- **UX_HOST_CLASS_PIMA_RC_ACCESS_DENIED**: (0x200f) nesne erişimi reddedildi
- **UX_HOST_CLASS_PIMA_RC_INCOMPLETE_TRANSFER**: (0x2007) aktarım tamamlanmadı
- **UX_MEMORY_INSUFFICIENT**: (0x12) Pima komutu oluşturmak için yeterli bellek yok.
- **UX_TRANSFER_ERROR**: (0x23) nesne yazılırken aktarım hatası

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

Yanıtlayanın içinde depolanan bir Thumb nesnesi alın.

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

### <a name="description"></a>Açıklama

Bu işlev, Yanıtlayıcıda bir Thumb nesnesi alır.

### <a name="parameters"></a>Parametreler

- **Pima**: Pima sınıfı örneğine yönelik işaretçi.
- **pima_session**: Pima oturumuna yönelik işaretçi.
- **object_handle**: nesnenin tanıtıcısı.
- **nesne**: nesne bilgisi kapsayıcısının işaretçisi.
- **thumb_buffer**: Thumb nesne verilerinin adresi.
- **thumb_buffer_length**: parmak nesnesi uzunluğu istendi.
- **thumb_actual_length**: döndürülen Thumb nesnesinin uzunluğu.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS**: (0x00) veri aktarımı tamamlandı.
- **UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) oturum açılmadı.
- **UX_HOST_CLASS_PIMA_RC_OBJECT_NOT_OPENED**: (0X2023) nesnesi açılmadı.
- **UX_HOST_CLASS_PIMA_RC_ACCESS_DENIED**: (0x200f) nesne erişimi reddedildi.
- **UX_HOST_CLASS_PIMA_RC_INCOMPLETE_TRANSFER**: (0x2007) aktarma tamamlanmadı.
- **UX_MEMORY_INSUFFICIENT**: (0x12) Pima komutu oluşturmak için yeterli bellek yok.
- **UX_TRANSFER_ERROR**: (0x23) nesne okunurken aktarım hatası oluştu.

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

Yanıtlayanda depolanan bir nesneyi silin.

### <a name="prototype"></a>Prototype

```C
UINT ux_host_class_pima_object_delete(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    ULONG object_handle)
```

### <a name="description"></a>Açıklama

Bu işlev, Yanıtlayıcıda bir nesneyi siler

### <a name="parameters"></a>Parametreler

- **Pima**: Pima sınıfı örneğine yönelik işaretçi.
- **pima_session**: Pima oturumuna yönelik işaretçi
- **object_handle**: nesnenin tanıtıcısı

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS**: (0x00) nesne silindi.
- **UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) oturum açılmadı.
- **UX_HOST_CLASS_PIMA_RC_ACCESS_DENIED**: (0x200f) nesne silinemiyor.
- **UX_MEMORY_INSUFFICIENT**: (0x12) Pima komutu oluşturmak için yeterli bellek yok.

### <a name="example"></a>Örnek

```C
/* Delete the object. */
status = ux_host_class_pima_object_delete(pima, pima_session, object_handle, pima_object);

/* Check status. */
if (status != UX_SUCCESS)
    return(status);
```

## <a name="ux_host_class_pima_object_close"></a>ux_host_class_pima_object_close

Yanıtlayanın içinde depolanan bir nesneyi kapatma

### <a name="prototype"></a>Prototype

```C
UINT ux_host_class_pima_object_close(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    ULONG object_handle, UX_HOST_CLASS_PIMA_OBJECT *object)
```

### <a name="description"></a>Açıklama

Bu işlev, yanıtlayanın bir nesnesini kapatır.

### <a name="parameters"></a>Parametreler

- **Pima**: Pima sınıfı örneğine yönelik işaretçi.
- **pima_session**: Pima oturumuna yönelik işaretçi.
- **object_handle**: nesnenin tanıtıcısı.
- **nesne**: nesne işaretçisi.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS**: (0x00) nesne kapatıldı.
- **UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) oturum açılmadı.
- **UX_HOST_CLASS_PIMA_RC_OBJECT_NOT_OPENED**: (0X2023) nesnesi açılmadı.
- **UX_MEMORY_INSUFFICIENT**: (0x12) Pima komutu oluşturmak için yeterli bellek yok.

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

### <a name="description"></a>Açıklama

Bu işlev genel seri arabiriminden okur. Çağrı engelleniyor ve yalnızca bir hata olduğunda ya da aktarım tamamlandığında döndürülür.

### <a name="parameters"></a>Parametreler

- **gser**: gser sınıfı örneğine yönelik işaretçi.
- **interface_index**: okunacak arabirim dizini.
- **data_pointer**: veri yükünün arabellek adresine yönelik işaretçi.
- **requested_length**: alınacak uzunluk.
- **actual_length**: Uzunluk gerçekten alındı.

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS**: (0x00) veri aktarımı tamamlandı.
- **UX_TRANSFER_TIMEOUT**: (0x5c) aktarım zaman aşımı, okuma tamamlanmadı.

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

### <a name="description"></a>Açıklama

Bu işlev genel seri arabirimine yazar. Çağrı engelleniyor ve yalnızca bir hata olduğunda ya da aktarım tamamlandığında döndürülür.

### <a name="parameters"></a>Parametreler

- **gser**: gser sınıfı örneğine yönelik işaretçi.
- **interface_index**: yazılacak arabirim.
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
status = ux_host_class_cdc_acm_write(gser, data_pointer, requested_length, &actual_length);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_gser_ioctl"></a>ux_host_class_gser_ioctl

Genel seri arabirimine bir ıOCTL işlevi gerçekleştirin.

### <a name="prototype"></a>Prototype

```C
UINT ux_host_class_gser_ioctl(
    UX_HOST_CLASS_GSER *gser,
    ULONG ioctl_function,
    VOID *parameter)
```

### <a name="description"></a>Açıklama

Bu işlev, gser arabirimine belirli bir IOCTL işlevi gerçekleştirir. Çağrı engelleniyor ve yalnızca bir hata olduğunda ya da komut tamamlandığında döndürülür.

### <a name="parameters"></a>Parametreler

- **gser**: gser sınıfı örneğine yönelik işaretçi.
- **ioctl_function**: gerçekleştirilecek IOCTL işlevi. İzin verilen IOCTL işlevlerinden biri için aşağıdaki tabloya bakın.
- **parametre**: IOCTL 'ye özgü bir parametreye pointerto

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS**: (0x00) veri aktarımı tamamlandı.
- **UX_MEMORY_INSUFFICIENT**: (0x12) yeterli bellek yok.
- **UX_HOST_CLASS_UNKNOWN**: (0x59) yanlış sınıf örneği
- **UX_FUNCTION_NOT_SUPPORTED**: (0x54) bilinmeyen IOCTL işlevi.

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

Genel Seri arabirimde almayı Başlat

### <a name="prototype"></a>Prototype

```C
UINT ux_host_class_gser_reception_start(
    UX_HOST_CLASS_GSER *gser,
    UX_HOST_CLASS_GSER_RECEPTION *gser_reception)
```

### <a name="description"></a>Açıklama

Bu işlev, genel seri sınıf arabirimindeki alımı başlatır. Bu işlev, engellenmemiş alım için izin verir. Bir arabellek alındığında uygulamaya çağrılan bir geri çağırma işlemi.

### <a name="parameters"></a>Parametreler

- **gser** Gser sınıfı örneğine yönelik işaretçi.
- **gser_reception** Alım parametrelerini içeren yapı

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) veri aktarımı tamamlandı.
- **UX_HOST_CLASS_UNKNOWN** (0x59) yanlış sınıf örneği
- **UX_ERROR** (0x01) hatası

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

Genel Seri arabirimde alımı durdur

### <a name="prototype"></a>Prototype

```C
UINT ux_host_class_gser_reception_stop(
    UX_HOST_CLASS_GSER *gser,
    UX_HOST_CLASS_GSER_RECEPTION *gser_reception)
```

### <a name="description"></a>Açıklama

Bu işlev, genel seri sınıf arabirimindeki alımı sonlandırır.

### <a name="parameters"></a>Parametreler

- **gser** Gser sınıfı örneğine yönelik işaretçi.
- **gser_reception** Alım parametrelerini içeren yapı

### <a name="return-value"></a>Dönüş Değeri

- **UX_SUCCESS** (0x00) veri aktarımı tamamlandı.
- **UX_HOST_CLASS_UNKNOWN** (0x59) yanlış sınıf örneği
- **UX_ERROR** (0x01) hatası

### <a name="example"></a>Örnek

```C
/* Stops the reception for gser. */
ux_host_class_gser_reception_stop(gser, &gser_reception);
```
