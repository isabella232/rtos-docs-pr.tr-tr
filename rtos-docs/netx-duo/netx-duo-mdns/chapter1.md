---
title: Bölüm 1-Azure RTOS NetX Duo mDNS/DNS-SD 'ye giriş
description: Azure RTOS NetX Duo mDNS/DNS-SD geleneksel DNS hizmetini genişletmektedir.
author: philmea
ms.author: philmea
ms.date: 07/09/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: b46539ee4d502fa4c90fb3392e25cd3bee40dc5b
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825925"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-mdnsdns-sd"></a><span data-ttu-id="76202-103">Bölüm 1-Azure RTOS NetX Duo mDNS/DNS-SD 'ye giriş</span><span class="sxs-lookup"><span data-stu-id="76202-103">Chapter 1 - Introduction to Azure RTOS NetX Duo mDNS/DNS-SD</span></span>

<span data-ttu-id="76202-104">MDNS ve DNS-SD, geleneksel DNS hizmetini artırmak için tasarlanan protokollerdir.</span><span class="sxs-lookup"><span data-stu-id="76202-104">The mDNS and DNS-SD are protocols designed to augment the traditional DNS service.</span></span> <span data-ttu-id="76202-105">mDNS, yerel ağdaki düğümlere konak adı ve hizmet araması sağlar.</span><span class="sxs-lookup"><span data-stu-id="76202-105">mDNS provides host name and service lookup to the nodes on the local network.</span></span> <span data-ttu-id="76202-106">Her düğüm, komşuları için sunduğu Hizmetleri duyurmak, komşularından sorgulara yanıt vermek ve uygulama uygulamalarında sorgu göndermesi için IPv4 veya IPv6 çok noktaya yayın kanalını kullanır.</span><span class="sxs-lookup"><span data-stu-id="76202-106">Each node uses IPv4 or IPv6 multicast channel to announce services it offers to its neighbors, responds to queries from its neighbors, and sends queries on behave of its applications.</span></span> <span data-ttu-id="76202-107">Tasarım gereği, mDNS dağıtılmış bir ortamda çalışır ve bu sayede merkezi bir hizmeti ortadan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="76202-107">By design, mDNS operates in a distributed environment, thus eliminates a centralized serve.</span></span>

<span data-ttu-id="76202-108">DNS-SD, mDNS 'in üzerine kurulmuştur.</span><span class="sxs-lookup"><span data-stu-id="76202-108">DNS-SD is built on top of mDNS.</span></span> <span data-ttu-id="76202-109">DNS-SD, düğümlerin yerel ağa sağladıkları Hizmetleri bildirmesini veya yerel ağdaki diğer düğümler tarafından sunulan hizmetleri keşfetmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="76202-109">DNS-SD allows nodes to announce services they provide to the local network or to discover services offered by other nodes on the local network.</span></span> <span data-ttu-id="76202-110">Belge boyunca *MDNs* terimi hem MDNs belirtimini hem de DNS-SD belirtimini kapsayan Hizmetleri ifade eder.</span><span class="sxs-lookup"><span data-stu-id="76202-110">Throughout the document, the term *mDNS* refers to the services that cover both the mDNS specification and the DNS-SD specification.</span></span>

## <a name="mdns-standard"></a><span data-ttu-id="76202-111">mDNS standardı</span><span class="sxs-lookup"><span data-stu-id="76202-111">mDNS Standard</span></span>

<span data-ttu-id="76202-112">NetX Duo mDNS/DNS-SD uygulamasının aşağıdaki RFC 'Lerle uyumlu olması:</span><span class="sxs-lookup"><span data-stu-id="76202-112">NetX Duo mDNS/DNS-SD implementation conforms to the following RFCs:</span></span>

- <span data-ttu-id="76202-113">RFC 6762: mDNS belirtimi</span><span class="sxs-lookup"><span data-stu-id="76202-113">RFC 6762: mDNS Specification</span></span>
- <span data-ttu-id="76202-114">RFC 6763: DNS-SD belirtimi</span><span class="sxs-lookup"><span data-stu-id="76202-114">RFC 6763: DNS-SD Specification</span></span>