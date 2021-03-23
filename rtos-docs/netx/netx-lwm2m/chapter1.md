---
title: Bölüm 1-Azure RTOS NetX LWM2M 'a giriş
description: Azure RTOS NetX LWM2M protokolü, hafif makinenin istemci bölümünü makine protokol standardına uygular.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: c29af430975266eed684bd1de38d9e5d7e2586a6
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826710"
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