---
title: Bölüm 1-Azure RTOS NetX BSD 'ye giriş
description: Azure RTOS NetX BSD yuvaları API 'SI karmaşık pozisyon sarmalayıcısı, bazı sınırlamalara sahip temel BSD yuvaları API çağrılarının bazılarını destekler ve altındaki NetX temel öğelerini kullanır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: fce781ac97ae75c4148614453eeb35c3064f8849
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825607"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-bsd"></a><span data-ttu-id="581e3-103">Bölüm 1-Azure RTOS NetX BSD 'ye giriş</span><span class="sxs-lookup"><span data-stu-id="581e3-103">Chapter 1 - Introduction to Azure RTOS NetX BSD</span></span>

<span data-ttu-id="581e3-104">NetX BSD yuvaları API 'SI karmaşık pozisyon sarmalayıcısı, bazı sınırlamalara sahip olan temel BSD yuvaları API çağrılarının bazılarını destekler ve altındaki NetX temelleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="581e3-104">The NetX BSD Sockets API Compliancy Wrapper supports some of the basic BSD Sockets API calls with some limitations and utilizes NetX primitives underneath.</span></span> <span data-ttu-id="581e3-105">Bu sarmalayıcı iç NetX temelleri kullandığından ve temel NetX hata denetimini atladığı için bu BSD yuvaları API Uyumluluk katmanının tipik BSD uygulamalarından hızlı veya biraz daha hızlı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="581e3-105">This BSD Sockets API compatibility layer should perform as fast or slightly faster than typical BSD implementations, since this Wrapper utilizes internal NetX primitives and bypasses basic NetX error checking.</span></span>

## <a name="bsd-sockets-api-compliancy-wrapper-source"></a><span data-ttu-id="581e3-106">BSD yuvaları API Karmaşıkkonum sarmalayıcı kaynağı</span><span class="sxs-lookup"><span data-stu-id="581e3-106">BSD Sockets API Compliancy Wrapper Source</span></span>

<span data-ttu-id="581e3-107">BSD sarmalayıcısı kaynak kodu basitlik için tasarlanmıştır ve yalnızca iki dosyadan oluşur *nx_bsd. h* ve *nx_bsd. c*.</span><span class="sxs-lookup"><span data-stu-id="581e3-107">The BSD Wrapper source code is designed for simplicity and is comprised of only two files, *nx_bsd.h* and *nx_bsd.c*.</span></span> <span data-ttu-id="581e3-108">*Nx_bsd. h* dosyası tüm gerekli BSD yuvaları API sarmalayıcı sabitlerini ve alt yordam prototiplerini tanımlar, ancak *nx_bsd. c* gerçek BSD yuvaları API uyumluluğu kaynak kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="581e3-108">The *nx_bsd.h* file defines all the necessary BSD Sockets API Wrapper constants and subroutine prototypes, while *nx_bsd.c* contains the actual BSD Sockets API compatibility source code.</span></span> <span data-ttu-id="581e3-109">Bu BSD sarmalayıcı kaynak dosyaları tüm NetX destek paketlerinde ortaktır.</span><span class="sxs-lookup"><span data-stu-id="581e3-109">These BSD Wrapper source files are common to all NetX support packages.</span></span>

<span data-ttu-id="581e3-110">Paket aşağıdakilerden oluşur:</span><span class="sxs-lookup"><span data-stu-id="581e3-110">The package consists of:</span></span>

- <span data-ttu-id="581e3-111">**nx_bsd. c**: sarmalayıcı kaynak kodu</span><span class="sxs-lookup"><span data-stu-id="581e3-111">**nx_bsd.c**: Wrapper source code</span></span>
- <span data-ttu-id="581e3-112">**nx_bsd. h**: Ana üstbilgi dosyası</span><span class="sxs-lookup"><span data-stu-id="581e3-112">**nx_bsd.h**: Main header file</span></span>

<span data-ttu-id="581e3-113">Örnek demo programları:</span><span class="sxs-lookup"><span data-stu-id="581e3-113">Sample demo programs:</span></span>

- <span data-ttu-id="581e3-114">**bsd_demo_tcp. c**: *tek bir TCP sunucusu ve istemcisiyle demo*</span><span class="sxs-lookup"><span data-stu-id="581e3-114">**bsd_demo_tcp.c**: *Demo with a single TCP server and client*</span></span>
- <span data-ttu-id="581e3-115">**bsd_demo_udp. c**: *iki UDP ISTEMCISI ve bir UDP sunucusu ile demo*</span><span class="sxs-lookup"><span data-stu-id="581e3-115">**bsd_demo_udp.c**: *Demo with two UDP clients and a UDP server*</span></span>
