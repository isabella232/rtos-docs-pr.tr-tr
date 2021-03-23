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
# <a name="chapter-1---introduction-to-azure-rtos-netx-lwm2m"></a><span data-ttu-id="85973-103">Bölüm 1-Azure RTOS NetX LWM2M 'a giriş</span><span class="sxs-lookup"><span data-stu-id="85973-103">Chapter 1 - Introduction to Azure RTOS NetX LWM2M</span></span>

<span data-ttu-id="85973-104">Azure RTOS NetX LWM2M protokolü, hafif makinenin istemci bölümünü makine protokol standardına uygular.</span><span class="sxs-lookup"><span data-stu-id="85973-104">The Azure RTOS NetX LWM2M Protocol implements the client part of the Lightweight Machine to Machine protocol standard.</span></span>

## <a name="netx-lwm2m-requirements"></a><span data-ttu-id="85973-105">NetX LWM2M gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="85973-105">NetX LWM2M Requirements</span></span>

<span data-ttu-id="85973-106">NetX LWM2M çalışma zamanı kitaplığı düzgün şekilde çalışması için bir NetX IP örneğinin zaten oluşturulmuş olmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="85973-106">In order to function properly, the NetX LWM2M run-time library requires that a NetX IP instance has already been created.</span></span> <span data-ttu-id="85973-107">NetX LWM2M paketinin daha fazla gereksinimi yoktur.</span><span class="sxs-lookup"><span data-stu-id="85973-107">The NetX LWM2M package has no further requirements.</span></span>

## <a name="netx-lwm2m-rfcs"></a><span data-ttu-id="85973-108">NetX LWM2M RFC 'Leri</span><span class="sxs-lookup"><span data-stu-id="85973-108">NetX LWM2M RFCs</span></span>

<span data-ttu-id="85973-109">NetX LWM2M, OMA-TS-LightweightM2M-V1_0 -20170208-A ve kısıtlanmış Uygulama Protokolü (CoAP) ile ilgili aşağıdaki RFC 'lerle uyumludur:</span><span class="sxs-lookup"><span data-stu-id="85973-109">NetX LWM2M is compliant with OMA-TS-LightweightM2M-V1_0-20170208-A and the following RFCs related to the Constrained Application Protocol (CoAP):</span></span>

- <span data-ttu-id="85973-110">**RFC 7252**: kısıtlanmış Uygulama Protokolü (coap)</span><span class="sxs-lookup"><span data-stu-id="85973-110">**RFC 7252**: The Constrained Application Protocol (CoAP)</span></span>

- <span data-ttu-id="85973-111">**RFC 7641**: kısıtlanmış uygulama protokolündeki (coap) kaynakları gözlemleme</span><span class="sxs-lookup"><span data-stu-id="85973-111">**RFC 7641**: Observing Resources in the Constrained Application Protocol (CoAP)</span></span>

- <span data-ttu-id="85973-112">**RFC 6690**: kısıtlanmış yeniden oluşan ortamlar (çekirdek) bağlantı biçimi</span><span class="sxs-lookup"><span data-stu-id="85973-112">**RFC 6690**: Constrained RESTful Environments (CoRE) Link Format</span></span>