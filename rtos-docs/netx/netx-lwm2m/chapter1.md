---
title: Bölüm 1-Azure RTOS NetX LWM2M 'a giriş
description: Azure RTOS NetX LWM2M protokolü, hafif makinenin istemci bölümünü makine protokol standardına uygular.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: fe9c90ec10b241c72c71882b28b5fe0e3e60e3913435ec27f797eade4ca4eca5
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116784929"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-lwm2m"></a>Bölüm 1-Azure RTOS NetX LWM2M 'a giriş

Azure RTOS NetX LWM2M protokolü, hafif makinenin istemci bölümünü makine protokol standardına uygular.

## <a name="netx-lwm2m-requirements"></a>NetX LWM2M gereksinimleri

NetX LWM2M çalışma zamanı kitaplığı düzgün şekilde çalışması için bir NetX IP örneğinin zaten oluşturulmuş olmasını gerektirir. NetX LWM2M paketinin daha fazla gereksinimi yoktur.

## <a name="netx-lwm2m-rfcs"></a>NetX LWM2M RFC 'Leri

NetX LWM2M, OMA-TS-LightweightM2M-V1_0 -20170208-A ve kısıtlanmış Uygulama Protokolü (CoAP) ile ilgili aşağıdaki RFC 'lerle uyumludur:

- **RFC 7252**: kısıtlanmış Uygulama Protokolü (coap)

- **RFC 7641**: kısıtlanmış uygulama protokolündeki (coap) kaynakları gözlemleme

- **RFC 6690**: kısıtlanmış yeniden oluşan ortamlar (çekirdek) bağlantı biçimi