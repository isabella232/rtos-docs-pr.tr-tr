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
# <a name="chapter-1--introduction-to-lwm2m-client"></a><span data-ttu-id="68ad1-103">Bölüm 1 LWM2M Istemcisine giriş</span><span class="sxs-lookup"><span data-stu-id="68ad1-103">Chapter 1  Introduction to LWM2M Client</span></span>

<span data-ttu-id="68ad1-104">Azure RTOS NetX Duo LWM2M Client protokolü, hafif makinenin istemci bölümünü makine protokol standardına uygular.</span><span class="sxs-lookup"><span data-stu-id="68ad1-104">The Azure RTOS NetX Duo LWM2M Client Protocol implements the client part of the Lightweight Machine to Machine protocol standard.</span></span> <span data-ttu-id="68ad1-105">(LWM2M 1.0-20170208A)</span><span class="sxs-lookup"><span data-stu-id="68ad1-105">(LWM2M 1.0-20170208A)</span></span>

## <a name="netx-lwm2m-client-requirements"></a><span data-ttu-id="68ad1-106">NetX LWM2M Istemci gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="68ad1-106">NetX LWM2M Client Requirements</span></span>

<span data-ttu-id="68ad1-107">Düzgün çalışması için LWM2M Istemci çalışma zamanı kitaplığı bir NetX IP örneğinin zaten oluşturulmuş olmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="68ad1-107">In order to function properly, the LWM2M Client run-time library requires that a NetX IP instance has already been created.</span></span> <span data-ttu-id="68ad1-108">NetX LWM2M Istemci paketinin başka bir gereksinimi yoktur.</span><span class="sxs-lookup"><span data-stu-id="68ad1-108">The NetX LWM2M Client package has no further requirements.</span></span>

## <a name="netx-lwm2m-client-rfcs"></a><span data-ttu-id="68ad1-109">NetX LWM2M Istemci RFC 'Leri</span><span class="sxs-lookup"><span data-stu-id="68ad1-109">NetX LWM2M Client RFCs</span></span>

<span data-ttu-id="68ad1-110">LWM2M Istemcisi, OMA-TS-LightweightM2M-v1 \_ 0-20170208-A ve kısıtlanmış Uygulama Protokolü (CoAP) ile ilgili aşağıdaki RFC 'lerle uyumludur.</span><span class="sxs-lookup"><span data-stu-id="68ad1-110">LWM2M Client is compliant with OMA-TS-LightweightM2M-V1\_0-20170208-A and the following RFCs related to the Constrained Application Protocol (CoAP).</span></span>

* <span data-ttu-id="68ad1-111">RFC 7252 kısıtlı Uygulama Protokolü (CoAP)</span><span class="sxs-lookup"><span data-stu-id="68ad1-111">RFC 7252 The Constrained Application Protocol (CoAP)</span></span>

* <span data-ttu-id="68ad1-112">RFC 7641 kısıtlı uygulama protokolünde (CoAP) kaynakları gözlemleme</span><span class="sxs-lookup"><span data-stu-id="68ad1-112">RFC 7641 Observing Resources in the Constrained Application Protocol (CoAP)</span></span>

* <span data-ttu-id="68ad1-113">RFC 6690 kısıtlı yeniden ortamları (çekirdek) bağlantı biçimi</span><span class="sxs-lookup"><span data-stu-id="68ad1-113">RFC 6690 Constrained RESTful Environments (CoRE) Link Format</span></span>

<span data-ttu-id="68ad1-114">Daha fazla bilgi için lütfen bkz. [OMA-TS-LightweightM2M-V1 \_ 0-2017208-A](http://www.openmobilealliance.org/release/LightweightM2M/V1_0-20170208-A/OMA-TS-LightweightM2M-V1_0-20170208-A.pdf).</span><span class="sxs-lookup"><span data-stu-id="68ad1-114">For more information, please see [OMA-TS-LightweightM2M-V1\_0-2017208-A](http://www.openmobilealliance.org/release/LightweightM2M/V1_0-20170208-A/OMA-TS-LightweightM2M-V1_0-20170208-A.pdf).</span></span>