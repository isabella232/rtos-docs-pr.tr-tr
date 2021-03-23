---
title: Bölüm 1-Azure RTOS NetX Duo LWM2M Istemcisine giriş
description: Bu bölümde, Azure RTOS NetX Duo hafif makinesine makine Protokolü istemcisine giriş yer almaktadır.
author: v-condav
ms.author: v-condav
ms.date: 01/22/2021
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 12f13c154668b3cadfae0924e59b55631dc27424
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825955"
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