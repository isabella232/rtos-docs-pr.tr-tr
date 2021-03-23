---
title: Ek B-Azure RTOS NetX Duo DHCPv6 sunucusu durum kodları
description: Bu bölümde tüm NetX Duo DHCPv6 sunucusu durum kodlarının açıklaması yer almaktadır
author: philmea
ms.author: philmea
ms.date: 06/08/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 7c79a0c0bc9acfcfca69c7333d30cd7cab35ba5f
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826057"
---
# <a name="appendix-b---azure-rtos-netx-duo-dhcpv6-server-status-codes"></a><span data-ttu-id="cbe6b-103">Ek B-Azure RTOS NetX Duo DHCPv6 sunucusu durum kodları</span><span class="sxs-lookup"><span data-stu-id="cbe6b-103">Appendix B - Azure RTOS NetX Duo DHCPv6 server status codes</span></span>

| <span data-ttu-id="cbe6b-104">Name</span><span class="sxs-lookup"><span data-stu-id="cbe6b-104">Name</span></span>              | <span data-ttu-id="cbe6b-105">Kod</span><span class="sxs-lookup"><span data-stu-id="cbe6b-105">Code</span></span>            | <span data-ttu-id="cbe6b-106">Açıklama</span><span class="sxs-lookup"><span data-stu-id="cbe6b-106">Description</span></span> |
| ------------------- | ------------------- | --------------- |
| <span data-ttu-id="cbe6b-107">Başarılı</span><span class="sxs-lookup"><span data-stu-id="cbe6b-107">Success</span></span> | <span data-ttu-id="cbe6b-108">0</span><span class="sxs-lookup"><span data-stu-id="cbe6b-108">0</span></span> | <span data-ttu-id="cbe6b-109">Başarılı</span><span class="sxs-lookup"><span data-stu-id="cbe6b-109">Success</span></span> |
| <span data-ttu-id="cbe6b-110">Belirtilmeyen hata</span><span class="sxs-lookup"><span data-stu-id="cbe6b-110">Unspecified Failure</span></span> | <span data-ttu-id="cbe6b-111">1</span><span class="sxs-lookup"><span data-stu-id="cbe6b-111">1</span></span> | <span data-ttu-id="cbe6b-112">Hata, neden belirtilmemiş; Bu durum kodu, Istemci isteğine diğer kodlarla eşleşmeyen genel bir hata olduğunu göstermek için sunucu tarafından ayarlanır</span><span class="sxs-lookup"><span data-stu-id="cbe6b-112">Failure, reason unspecified; this status code is set by the Server to indicate a general failure in granting the Client request not matching the other codes</span></span> |
| <span data-ttu-id="cbe6b-113">NoAddress kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="cbe6b-113">NoAddress Available</span></span> | <span data-ttu-id="cbe6b-114">2</span><span class="sxs-lookup"><span data-stu-id="cbe6b-114">2</span></span> | <span data-ttu-id="cbe6b-115">Sunucu, Istemciye atanacak bir adrese sahip değil</span><span class="sxs-lookup"><span data-stu-id="cbe6b-115">Server has no addresses available to assign to the Client</span></span> |
| <span data-ttu-id="cbe6b-116">NoBinding</span><span class="sxs-lookup"><span data-stu-id="cbe6b-116">NoBinding</span></span> | <span data-ttu-id="cbe6b-117">3</span><span class="sxs-lookup"><span data-stu-id="cbe6b-117">3</span></span> | <span data-ttu-id="cbe6b-118">İstemci IA adresi (bağlama) kullanılamıyor, örneğin, istenen IP adresi sunucunun kiralanmasını veya başka bir Istemciye atanabileceği için kullanılamıyor.</span><span class="sxs-lookup"><span data-stu-id="cbe6b-118">Client IA address (binding) is not available e.g. the requested IP address is not available for the Server to lease or assigned to another Client.</span></span> |
| <span data-ttu-id="cbe6b-119">NotOnLink</span><span class="sxs-lookup"><span data-stu-id="cbe6b-119">NotOnLink</span></span> | <span data-ttu-id="cbe6b-120">4</span><span class="sxs-lookup"><span data-stu-id="cbe6b-120">4</span></span> | <span data-ttu-id="cbe6b-121">Adresin ön eki, IP adresinin bir açık bağlantı adresi olmadığını belirtir</span><span class="sxs-lookup"><span data-stu-id="cbe6b-121">The prefix for the address indicates the IP address is not an on link address</span></span> |
| <span data-ttu-id="cbe6b-122">UseMulticast</span><span class="sxs-lookup"><span data-stu-id="cbe6b-122">UseMulticast</span></span> | <span data-ttu-id="cbe6b-123">5</span><span class="sxs-lookup"><span data-stu-id="cbe6b-123">5</span></span> | <span data-ttu-id="cbe6b-124">*All_DHCP_Relay_Agents_and_Servers* çok noktaya yayın adresi yerine sunucunun tek noktaya yayın adresini kullanarak istemci iletisi almak için yanıt olarak bir sunucu tarafından gönderilir</span><span class="sxs-lookup"><span data-stu-id="cbe6b-124">Sent by a Server in response to receiving a Client message using the Server’s unicast address instead of the *All_DHCP_Relay_Agents_and_Servers* multicast address</span></span> |