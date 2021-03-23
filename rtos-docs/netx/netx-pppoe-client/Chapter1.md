---
title: Bölüm 1-Azure RTOS NetX PPPoE Istemcisine giriş
description: Bu bölümde, Azure RTOS NetX PPPoE modülünün ayrıntıları yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 07/13/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: bbf1e064bb38754bd67b279a0fd60d46d3d6d557
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826644"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-pppoe-client"></a><span data-ttu-id="dcc60-103">Bölüm 1-Azure RTOS NetX PPPoE Istemcisine giriş</span><span class="sxs-lookup"><span data-stu-id="dcc60-103">Chapter 1 - Introduction to Azure RTOS NetX PPPoE Client</span></span>

<span data-ttu-id="dcc60-104">Ethernet üzerinden PPP (PPPoE), ana bilgisayarların geleneksel karakter tabanlı seri hat iletişimi yerine Ethernet aracılığıyla PPP sunucusuna bağlanmasına olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="dcc60-104">PPP over Ethernet (PPPoE) allows hosts to connect to PPP server via Ethernet instead of the traditional character-based serial line communication.</span></span>  <span data-ttu-id="dcc60-105">PPPoE teknik ayrıntıları, RFC 2516: Ethernet üzerinden PPP (PPPoE) Iletmek için bir yöntem olarak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="dcc60-105">The technical details of PPPoE are described in RFC 2516:  A Method for Transmitting PPP over Ethernet (PPPoE).</span></span> <span data-ttu-id="dcc60-106">Bu belge, Azure RTOS NetX PPPoE modülünün ayrıntılarına odaklanır.</span><span class="sxs-lookup"><span data-stu-id="dcc60-106">This document focuses on the details of  Azure RTOS NetX PPPoE module.</span></span>

<span data-ttu-id="dcc60-107">Ethernet üzerinden noktadan noktaya bağlantı sağlamak için her PPP oturumunun, uzak eşin Ethernet adresini öğrenmeli ve benzersiz bir oturum tanımlayıcısı kurması gerekir.</span><span class="sxs-lookup"><span data-stu-id="dcc60-107">To provide a point-to-point connection over Ethernet, each PPP session must learn the Ethernet address of the remote peer, as well as establish a unique session identifier.</span></span>

<span data-ttu-id="dcc60-108">RFC 2516 ' e göre, PPPoE iki aşamadan oluşur: bulma aşaması ve PPPoE oturum aşaması.</span><span class="sxs-lookup"><span data-stu-id="dcc60-108">According to RFC 2516, PPPoE consists of two stages: the Discovery stage, and PPPoE Session stage.</span></span> <span data-ttu-id="dcc60-109">Bir ana bilgisayar (istemci) bir PPP oturumu başlatmak isterse, önce PPPoE sunucusunu bulmak için bulma işlemini gerçekleştirmelidir.</span><span class="sxs-lookup"><span data-stu-id="dcc60-109">When a host (client) wishes to start a PPP session, it must first perform Discovery to find PPPoE server.</span></span> <span data-ttu-id="dcc60-110">Bu adım Ayrıca, sunucunun ve istemcinin diğer Ethernet MAC adreslerini ve SESSION_ID belirlemesine izin verir ve bu da PPP oturumunun geri kalanı için kullanılacaktır.</span><span class="sxs-lookup"><span data-stu-id="dcc60-110">This step also allows the server and the client to identify each other’s Ethernet MAC address and SESSION_ID, which will be used for the rest of the PPP session.</span></span>

<span data-ttu-id="dcc60-111">Ethernet çerçevesi aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="dcc60-111">An Ethernet frame is as follows:</span></span>

![Ethernet çerçevesi](media/ethernet-frame.png)

<span data-ttu-id="dcc60-113">PPPoE için Ethernet yükü aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="dcc60-113">The Ethernet payload for PPPoE is as follows:</span></span>

![Ethernet yükü](media/ethernet-payload.png)

## <a name="pppoe-discovery-stage"></a><span data-ttu-id="dcc60-115">PPPoE bulma aşaması</span><span class="sxs-lookup"><span data-stu-id="dcc60-115">PPPoE Discovery Stage</span></span>

<span data-ttu-id="dcc60-116">PPPoE bulma aşaması, istemcilerin, değiştirilen PPP çerçevelerinden önce bir oturum oluşturmak için ağ üzerindeki tüm kullanılabilir sunuculardan bir sunucu seçmesine olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="dcc60-116">The PPPoE Discovery stage allows clients to select a server from all available servers on the network, effectively to create a session prior to PPP frames being exchanged.</span></span>  <span data-ttu-id="dcc60-117">Keşif aşamasının sonunda, hem istemci hem de sunucu benzersiz bir oturum KIMLIĞI üzerinde anlaşacaktır ve her iki taraf da eşin MAC adresini bilmelidir.</span><span class="sxs-lookup"><span data-stu-id="dcc60-117">At the end of the discovery stage, both the client and the server shall agree on a unique session ID, and both sides need to know peer’s MAC address.</span></span>

| <span data-ttu-id="dcc60-118">Bulma Iletisi</span><span class="sxs-lookup"><span data-stu-id="dcc60-118">Discovery Message</span></span> | <span data-ttu-id="dcc60-119">Kod</span><span class="sxs-lookup"><span data-stu-id="dcc60-119">Code</span></span> | <span data-ttu-id="dcc60-120">Yön</span><span class="sxs-lookup"><span data-stu-id="dcc60-120">Direction</span></span> |
| ----------------- | ---- | --------- |
| <span data-ttu-id="dcc60-121">PPPoE etkin bulma başlatma (PADı)</span><span class="sxs-lookup"><span data-stu-id="dcc60-121">PPPoE Active Discovery Initiation (PADI)</span></span> | <span data-ttu-id="dcc60-122">0x09</span><span class="sxs-lookup"><span data-stu-id="dcc60-122">0x09</span></span> | <span data-ttu-id="dcc60-123">Istemciden yayına</span><span class="sxs-lookup"><span data-stu-id="dcc60-123">From Client to broadcast</span></span> |
| <span data-ttu-id="dcc60-124">PPPoE etkin bulma teklifi (PADO)</span><span class="sxs-lookup"><span data-stu-id="dcc60-124">PPPoE Active Discovery Offer (PADO)</span></span> | <span data-ttu-id="dcc60-125">0x07</span><span class="sxs-lookup"><span data-stu-id="dcc60-125">0x07</span></span> | <span data-ttu-id="dcc60-126">Sunucudan Istemciye</span><span class="sxs-lookup"><span data-stu-id="dcc60-126">From Server to Client</span></span> |
| <span data-ttu-id="dcc60-127">PPPoE etkin bulma Isteği (PADR)</span><span class="sxs-lookup"><span data-stu-id="dcc60-127">PPPoE Active Discovery Request (PADR)</span></span> | <span data-ttu-id="dcc60-128">0x19</span><span class="sxs-lookup"><span data-stu-id="dcc60-128">0x19</span></span> | <span data-ttu-id="dcc60-129">Istemciden sunucuya</span><span class="sxs-lookup"><span data-stu-id="dcc60-129">From Client to Server</span></span> |
| <span data-ttu-id="dcc60-130">PPPOE etkin bulma oturumu-onay (Pad)</span><span class="sxs-lookup"><span data-stu-id="dcc60-130">PPPOE Active Discovery Session-confirmation (PADS)</span></span> | <span data-ttu-id="dcc60-131">0x65</span><span class="sxs-lookup"><span data-stu-id="dcc60-131">0x65</span></span> | <span data-ttu-id="dcc60-132">Sunucudan Istemciye</span><span class="sxs-lookup"><span data-stu-id="dcc60-132">From Server to Client</span></span> |
| <span data-ttu-id="dcc60-133">PPPoE etkin bulma sona erdir (TıT)</span><span class="sxs-lookup"><span data-stu-id="dcc60-133">PPPoE Active Discovery Terminate (PADT)</span></span> | <span data-ttu-id="dcc60-134">0xa7</span><span class="sxs-lookup"><span data-stu-id="dcc60-134">0xa7</span></span> | <span data-ttu-id="dcc60-135">, Sunucu veya istemciden başlatılabilir</span><span class="sxs-lookup"><span data-stu-id="dcc60-135">Can be initiated from either server or client</span></span> |

<span data-ttu-id="dcc60-136">Tüm bulma Ethernet çerçevelerinin ETHER_TYPE alanı 0x8863 değerine ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="dcc60-136">All Discovery Ethernet frames have the ETHER_TYPE field set to the value 0x8863.</span></span>

## <a name="pppoe-session-message"></a><span data-ttu-id="dcc60-137">PPPoE oturum Iletisi</span><span class="sxs-lookup"><span data-stu-id="dcc60-137">PPPoE Session Message</span></span>

<span data-ttu-id="dcc60-138">İstemci ve sunucu bir oturum oluşturduktan sonra, PPP çerçeveleri, PPPoE oturum iletileri olarak aktarılabilir.</span><span class="sxs-lookup"><span data-stu-id="dcc60-138">After the client and the server create a session, PPP frames can be transferred as PPPoE Session messages.</span></span>  <span data-ttu-id="dcc60-139">Bir oturum sırasında, SESSION_ID değişmemelidir ve bulma aşamasında sunucunun atandığı değer olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="dcc60-139">During a session, the SESSION_ID must not change and must be the value the server assigned during the Discovery stage.</span></span>

<span data-ttu-id="dcc60-140">Tüm PPPoE oturum Ethernet çerçevelerinin ETHER_TYPE alanı 0x8864 değerine ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="dcc60-140">All PPPoE Session Ethernet frames have the ETHER_TYPE field set to the value 0x8864.</span></span>
