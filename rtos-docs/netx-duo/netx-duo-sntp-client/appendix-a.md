---
title: Ek A-Azure RTOS NetX Duo SNTP önemli hata kodları
description: Aşağıdaki hata kodları, Azure RTOS NetX Duo SNTP Istemcisinin geçerli sunucu ile zaman güncellerinin iptal edilmesine neden olur.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 065e7a3e65b3cf8d7fcfb34bb9568a673791609a
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825762"
---
# <a name="appendix-a---azure-rtos-netx-duo-sntp-fatal-error-codes"></a><span data-ttu-id="ae784-103">Ek A-Azure RTOS NetX Duo SNTP önemli hata kodları</span><span class="sxs-lookup"><span data-stu-id="ae784-103">Appendix A - Azure RTOS NetX Duo SNTP Fatal Error Codes</span></span>

<span data-ttu-id="ae784-104">Aşağıdaki hata kodları, Azure RTOS NetX Duo SNTP Istemcisinin geçerli sunucu ile zaman güncellerinin iptal edilmesine neden olur.</span><span class="sxs-lookup"><span data-stu-id="ae784-104">The following error codes will result in the Azure RTOS NetX Duo SNTP Client aborting time updates with the current server.</span></span> <span data-ttu-id="ae784-105">Sunucunun, kullanılabilir sunucuların SNTP Istemci listesinden kaldırılıp kaldırılamayacağına karar vermek veya listedeki bir sonraki kullanılabilir sunucuya geçiş yapmak, uygulamaya bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="ae784-105">It is up to the application to decide if the server should be removed from the SNTP Client list of available servers, or simply switch to the next available server on the list.</span></span> <span data-ttu-id="ae784-106">Her hata durumunun tanımı \* nxd_sntp_client. h içinde tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="ae784-106">The definition of each error status is defined in \*nxd_sntp_client.h.</span></span> *

<span data-ttu-id="ae784-107">SNTP Istemcisi, aşağıdaki listeden uygulamaya bir hata döndürürse, sunucunun büyük olasılıkla başka bir sunucu ile değiştirilmeleri gerekir.</span><span class="sxs-lookup"><span data-stu-id="ae784-107">When the SNTP Client returns an error from the list below to the application, the Server should probably be replaced with another Server.</span></span> <span data-ttu-id="ae784-108">NX_SNTP_KOD_REMOVE_SERVER hata durumunun, ayarlamak için bir deölüm işleyicisinin (geri çağırma işlevi) SNTP istemci öpücük 'ye kaldığını unutmayın:</span><span class="sxs-lookup"><span data-stu-id="ae784-108">Note that the NX_SNTP_KOD_REMOVE_SERVER error status is left to the SNTP Client kiss of death handler (callback function) to set:</span></span>

- <span data-ttu-id="ae784-109">NX_SNTP_KOD_REMOVE_SERVER 0xD0C</span><span class="sxs-lookup"><span data-stu-id="ae784-109">NX_SNTP_KOD_REMOVE_SERVER 0xD0C</span></span>  
- <span data-ttu-id="ae784-110">NX_SNTP_SERVER_AUTH_FAIL 0xD0D</span><span class="sxs-lookup"><span data-stu-id="ae784-110">NX_SNTP_SERVER_AUTH_FAIL 0xD0D</span></span>  
- <span data-ttu-id="ae784-111">NX_SNTP_INVALID_NTP_VERSION 0xD11</span><span class="sxs-lookup"><span data-stu-id="ae784-111">NX_SNTP_INVALID_NTP_VERSION 0xD11</span></span>  
- <span data-ttu-id="ae784-112">NX_SNTP_INVALID_SERVER_MODE 0xD12</span><span class="sxs-lookup"><span data-stu-id="ae784-112">NX_SNTP_INVALID_SERVER_MODE 0xD12</span></span>  
- <span data-ttu-id="ae784-113">NX_SNTP_INVALID_SERVER_STRATUM 0xD15</span><span class="sxs-lookup"><span data-stu-id="ae784-113">NX_SNTP_INVALID_SERVER_STRATUM 0xD15</span></span>  

<span data-ttu-id="ae784-114">SNTP Istemcisi, aşağıdaki listeden uygulamaya bir hata döndürürse, sunucu yalnızca geçici olarak geçerli saat güncelleştirmeleri sağlayamayabilir ve kaldırılması gerekebilir:</span><span class="sxs-lookup"><span data-stu-id="ae784-114">When the SNTP Client returns an error from the list below to the application, the Server may only temporarily be unable to provide valid time updates and need not be removed:</span></span>

- <span data-ttu-id="ae784-115">HNX_SNTP_NO_UNICAST_FROM_SERVER 0xD09</span><span class="sxs-lookup"><span data-stu-id="ae784-115">HNX_SNTP_NO_UNICAST_FROM_SERVER 0xD09</span></span>  
- <span data-ttu-id="ae784-116">NX_SNTP_SERVER_CLOCK_NOT_SYNC 0xD0A</span><span class="sxs-lookup"><span data-stu-id="ae784-116">NX_SNTP_SERVER_CLOCK_NOT_SYNC 0xD0A</span></span>  
- <span data-ttu-id="ae784-117">NX_SNTP_KOD_SERVER_NOT_AVAILABLE 0xD0B</span><span class="sxs-lookup"><span data-stu-id="ae784-117">NX_SNTP_KOD_SERVER_NOT_AVAILABLE 0xD0B</span></span>  
- <span data-ttu-id="ae784-118">NX_SNTP_OVER_BAD_UPDATE_LIMIT 0xD17</span><span class="sxs-lookup"><span data-stu-id="ae784-118">NX_SNTP_OVER_BAD_UPDATE_LIMIT 0xD17</span></span>  
- <span data-ttu-id="ae784-119">NX_SNTP_BAD_SERVER_ROOT_DISPERSION 0xD16</span><span class="sxs-lookup"><span data-stu-id="ae784-119">NX_SNTP_BAD_SERVER_ROOT_DISPERSION 0xD16</span></span>  
- <span data-ttu-id="ae784-120">NX_SNTP_INVALID_RTT_TIME 0xD21</span><span class="sxs-lookup"><span data-stu-id="ae784-120">NX_SNTP_INVALID_RTT_TIME 0xD21</span></span>  
- <span data-ttu-id="ae784-121">NX_SNTP_KOD_SERVER_NOT_AVAILABLE 0xD24</span><span class="sxs-lookup"><span data-stu-id="ae784-121">NX_SNTP_KOD_SERVER_NOT_AVAILABLE 0xD24</span></span>