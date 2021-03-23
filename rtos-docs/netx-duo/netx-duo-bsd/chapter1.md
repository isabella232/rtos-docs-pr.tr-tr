---
title: Bölüm 1-Azure RTOS NetX Duo BSD 'ye giriş
description: BSD yuvası API 'SI karmaşık pozisyon sarmalayıcısı, bazı sınırlamalar içeren ve Azure RTOS NetX Duo temel sürümlerini kullanan bazı temel BSD yuvası API çağrılarını destekler.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: e89018dffd2f9f9065efab2ecabdf4364c4f89a3
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826159"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-bsd"></a><span data-ttu-id="e623f-103">Bölüm 1-Azure RTOS NetX Duo BSD 'ye giriş</span><span class="sxs-lookup"><span data-stu-id="e623f-103">Chapter 1 - Introduction to Azure RTOS NetX Duo BSD</span></span>

<span data-ttu-id="e623f-104">BSD yuvası API 'SI karmaşık pozisyon sarmalayıcısı, bazı sınırlamalar içeren ve Azure RTOS NetX Duo temel sürümlerini kullanan bazı temel BSD yuvası API çağrılarını destekler.</span><span class="sxs-lookup"><span data-stu-id="e623f-104">The BSD Socket API Compliancy Wrapper supports some of the basic BSD Socket API calls, with some limitations and utilizes Azure RTOS NetX Duo primitives underneath.</span></span>

## <a name="bsd-socket-api-compliancy-wrapper-source"></a><span data-ttu-id="e623f-105">BSD yuvası API 'SI karmaşık pozisyon sarmalayıcı kaynağı</span><span class="sxs-lookup"><span data-stu-id="e623f-105">BSD Socket API Compliancy Wrapper Source</span></span>

<span data-ttu-id="e623f-106">Sarmalayıcı kaynak kodu basitlik için tasarlanmıştır ve iki dosyadan oluşur; yani *nxd_bsd. h* ve *nxd_bsd. c*.</span><span class="sxs-lookup"><span data-stu-id="e623f-106">The Wrapper source code is designed for simplicity and is comprised of two files, namely *nxd_bsd.h* and *nxd_bsd.c*.</span></span> <span data-ttu-id="e623f-107">*Nxd_bsd. h* dosyası, tüm gerekli BSD yuvası API sarmalayıcı sabitlerini ve alt yordam prototiplerini tanımlar, ancak *nxd_bsd. c* gerçek BSD yuvası API 'si uyumluluk kaynak kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="e623f-107">The *nxd_bsd.h* file defines all the necessary BSD Socket API wrapper constants and subroutine prototypes, while *nxd_bsd.c* contains the actual BSD Socket API compatibility source code.</span></span> <span data-ttu-id="e623f-108">Bu sarmalayıcı kaynak dosyaları tüm NetX Duo destek paketlerinde ortaktır.</span><span class="sxs-lookup"><span data-stu-id="e623f-108">These Wrapper source files are common to all NetX Duo support packages.</span></span>

<span data-ttu-id="e623f-109">Paket aşağıdakilerden oluşur:</span><span class="sxs-lookup"><span data-stu-id="e623f-109">The package consists of:</span></span>

- <span data-ttu-id="e623f-110">**nxd_bsd. c**: sarmalayıcı kaynak kodu</span><span class="sxs-lookup"><span data-stu-id="e623f-110">**nxd_bsd.c**: Wrapper source code</span></span>
- <span data-ttu-id="e623f-111">**nxd_bsd. h**: Ana üstbilgi dosyası</span><span class="sxs-lookup"><span data-stu-id="e623f-111">**nxd_bsd.h**: Main header file</span></span>

<span data-ttu-id="e623f-112">Örnek demo programları:</span><span class="sxs-lookup"><span data-stu-id="e623f-112">Sample demo programs:</span></span>

- <span data-ttu-id="e623f-113">**bsd_demo_udp. c**: *iki UDP eşiyle demo (yalnızca IPv4)*</span><span class="sxs-lookup"><span data-stu-id="e623f-113">**bsd_demo_udp.c**: *Demo with two UDP peers (IPv4 only)*</span></span>
- <span data-ttu-id="e623f-114">**bsd_demo_tcp. c**: *tek bir TCP sunucusu ve istemcisiyle demo*</span><span class="sxs-lookup"><span data-stu-id="e623f-114">**bsd_demo_tcp.c**: *Demo with a single TCP server and client*</span></span>
- <span data-ttu-id="e623f-115">**bsd_demo_raw. c**: *iki ham eş ile demo*</span><span class="sxs-lookup"><span data-stu-id="e623f-115">**bsd_demo_raw.c**: *Demo with two RAW peers*</span></span>