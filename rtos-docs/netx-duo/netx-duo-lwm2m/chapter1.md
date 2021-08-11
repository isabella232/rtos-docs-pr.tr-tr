---
title: Bölüm 1-Azure RTOS NetX Duo LWM2M Istemcisine giriş
description: Bu bölümde, Azure RTOS NetX Duo hafif makinesine makine Protokolü istemcisine giriş yer almaktadır.
author: v-condav
ms.author: v-condav
ms.date: 01/22/2021
ms.topic: article
ms.service: rtos
ms.openlocfilehash: a2722daac76632e492d0f9345103c45da9ba1b321e91c9c04e04c76463984c3a
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116783484"
---
# <a name="chapter-1--introduction-to-lwm2m-client"></a>Bölüm 1 LWM2M Istemcisine giriş

Azure RTOS NetX Duo LWM2M Client protokolü, hafif makinenin istemci bölümünü makine protokol standardına uygular. (LWM2M 1.0-20170208A)

## <a name="netx-lwm2m-client-requirements"></a>NetX LWM2M Istemci gereksinimleri

Düzgün çalışması için LWM2M Istemci çalışma zamanı kitaplığı bir NetX IP örneğinin zaten oluşturulmuş olmasını gerektirir. NetX LWM2M Istemci paketinin başka bir gereksinimi yoktur.

## <a name="netx-lwm2m-client-rfcs"></a>NetX LWM2M Istemci RFC 'Leri

LWM2M Istemcisi, OMA-TS-LightweightM2M-v1 \_ 0-20170208-A ve kısıtlanmış Uygulama Protokolü (CoAP) ile ilgili aşağıdaki RFC 'lerle uyumludur.

* RFC 7252 kısıtlı Uygulama Protokolü (CoAP)

* RFC 7641 kısıtlı uygulama protokolünde (CoAP) kaynakları gözlemleme

* RFC 6690 kısıtlı yeniden ortamları (çekirdek) bağlantı biçimi

Daha fazla bilgi için lütfen bkz. [OMA-TS-LightweightM2M-V1 \_ 0-2017208-A](http://www.openmobilealliance.org/release/LightweightM2M/V1_0-20170208-A/OMA-TS-LightweightM2M-V1_0-20170208-A.pdf).