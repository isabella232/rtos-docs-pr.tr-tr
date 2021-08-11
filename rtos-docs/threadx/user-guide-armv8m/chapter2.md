---
title: Bölüm 2-ARMv8-d için ThreadX desteği yükleme
description: Bu bölümde, ARMv8-e mimarisi için ThreadX kaynak kodunun nasıl yükleneceği ve kullanılacağı açıklanmaktadır.
author: v-condav
ms.author: v-condav
ms.date: 03/04/2021
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 085310acd5262226e9ff3af440a5f05268c7799e78eda81334a13b736222b95c
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116801963"
---
#  <a name="chapter-2--installing-threadx-support-for-armv8-m"></a>Bölüm 2 ARMv8-d için ThreadX desteğini yükleme

ARMv8-e mimarisini desteklemek için ek ThreadX kaynak kodu dosyaları vardır.

ThreadX güvenli modda çalıştırılabilmesi için bu ek dosyalar ve API 'Ler gerekli değildir. ThreadX 'i güvenli modda çalıştırmak için,  **_tx_port. h_ _ ' nin üstündeki *veya komut satırında veya proje ayarlarında sembol TX_SECURE_EXECUTION belirleyin. _* TX_SECURE_EXECUTION** tüm c ve derleme dosyaları için tanımlandığından emin olun. ThreadX ve Kullanıcı uygulaması güvenli modda yürütülür.

ThreadX ve Kullanıcı uygulamasını güvenli olmayan modda çalıştırmak ve güvenli olmayan çağrılabilir güvenli işlevleri desteklemek için lütfen aşağıdakileri yapın.

***Tx_thread_secure_stack. c*** dosyası güvenli uygulamaya eklenmelidir.

Aşağıdaki dosyalar ThreadX kitaplığına eklenmelidir.

- ***tx_secure_interface. h***
- ***txe_thread_secure_stack_allocate. c***
- ***txe_thread_secure_stack_free. c***
- ***tx_thread_secure_stack_allocate. s***
- ***tx_thread_secure_stack_free. s***

Aşağıdaki iki dosya, ThreadX kitaplığındaki genel dosyaları değiştirir.

- ***tx_thread_stack_error_handler. c***
- ***tx_thread_stack_error_notify. c***

## <a name="additional-threadx-sources-for-armv8-m"></a>ARMv8-d için ek ThreadX kaynakları

ARMv8-p TrustZone mimarisine yönelik ek ThreadX dosyaları aşağıda açıklanmıştır.

  | **Dosya adı**                            | **İçerik**                                                        |
  |------------------------------------------|---------------------------------------------------------------------|
  | ***tx_secure_interface. h***              | ThreadX güvenli olmayan çağrılabilir işlevleri tanımlayan dosya ekleme. |
  | ***txe_thread_secure_stack_allocate. c*** |  Güvenli yığın ayırma API 'SI için dosya denetleniyor. |
  | ***txe_thread_secure_stack_free. c***     |  Hata-güvenli yığın ücretsiz API 'SI için dosya denetleniyor. |
  | ***tx_thread_secure_stack_allocate. s***  |  Güvenli yığın ayırma hizmeti için güvenli olmayan veneer. |
  | ***tx_thread_secure_stack_free. s***      |  Güvenli yığın ücretsiz hizmeti için güvenli olmayan veneer. |
  | ***tx_thread_stack_error_handler. c***    |  İş parçacığı yığın hataları için işleyici. |
  | ***tx_thread_stack_error_notify. c***     |  İş parçacığı yığın hatalarını işlemek için bildirim geri aramasını kaydedin. |
