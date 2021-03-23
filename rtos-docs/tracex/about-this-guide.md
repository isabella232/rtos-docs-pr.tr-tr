---
title: Azure RTOS TraceX Kullanıcı Kılavuzu
description: Bu kılavuz, Microsoft 'un Microsoft Windows tabanlı Sistem Analizi Aracı olan Azure RTOS TraceX hakkında kapsamlı bilgiler içerir.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: 92d886b19a0c67292cd4f6a5f8bd7f9d3106374b
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104827869"
---
# <a name="about-this-guide"></a><span data-ttu-id="d9a45-103">Bu kılavuz hakkında</span><span class="sxs-lookup"><span data-stu-id="d9a45-103">About this guide</span></span>

<span data-ttu-id="d9a45-104">Bu kılavuz, Microsoft Azure RTOS için Microsoft Windows tabanlı Sistem Analizi Aracı olan Azure RTOS TraceX hakkında kapsamlı bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="d9a45-104">This guide contains comprehensive information about Azure RTOS TraceX, the Microsoft Windows-based system analysis tool for Microsoft Azure RTOS.</span></span>

<span data-ttu-id="d9a45-105">Azure RTOS ThreadX Real-Time Işletim sistemi (RTOS) ve eklenti bileşenleri kullanılarak eklenmiş gerçek zamanlı yazılım geliştiricisi için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="d9a45-105">It is intended for the embedded real-time software developer using Azure RTOS ThreadX Real-Time Operating System (RTOS) and add-on components.</span></span> <span data-ttu-id="d9a45-106">Geliştirici standart Azure RTOS ThreadX Azure RTOS FileX ve Azure RTOS NetX kavramlarını tanımanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d9a45-106">The developer should be familiar with standard Azure RTOS ThreadX Azure RTOS FileX, and Azure RTOS NetX concepts.</span></span>

## <a name="organization"></a><span data-ttu-id="d9a45-107">Kuruluş</span><span class="sxs-lookup"><span data-stu-id="d9a45-107">Organization</span></span>

- <span data-ttu-id="d9a45-108">[Bölüm 1](chapter1.md) -Azure RTOS tracex 'a yönelik temel bir genel bakış içerir ve gerçek zamanlı geliştirmeyle ilişkilerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="d9a45-108">[Chapter 1](chapter1.md) - contains an basic overview of Azure RTOS TraceX and describes its relationship to real-time development.</span></span>
- <span data-ttu-id="d9a45-109">[Bölüm 2](chapter2.md) -uygulamanızı doğrudan kutudan çözümlemek için Azure RTOS tracex 'i yüklemek ve kullanmak üzere temel adımları sağlar.</span><span class="sxs-lookup"><span data-stu-id="d9a45-109">[Chapter 2](chapter2.md) - gives the basic steps to install and use Azure RTOS TraceX to analyze your application right out of the box.</span></span>
- <span data-ttu-id="d9a45-110">[Bölüm 3](chapter3.md) -Azure RTOS tracex 'nin ana özelliklerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="d9a45-110">[Chapter 3](chapter3.md) - describes the main features of Azure RTOS TraceX.</span></span>
- <span data-ttu-id="d9a45-111">[Bölüm 4](chapter4.md) -Azure RTOS tracex 'in performans analizi özellikleri hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="d9a45-111">[Chapter 4](chapter4.md) - details performance analysis features of Azure RTOS TraceX.</span></span>
- <span data-ttu-id="d9a45-112">[Bölüm 5](chapter5.md) -Azure RTOS tracex tarafından görüntülenebilen bir izleme arabelleği oluşturmak için Azure RTOS threadx, Azure RTOS FileX ve Azure RTOS NETX 'in nasıl ayarlanacağını açıklar.</span><span class="sxs-lookup"><span data-stu-id="d9a45-112">[Chapter 5](chapter5.md) - describes how to set up Azure RTOS ThreadX, Azure RTOS FileX, and Azure RTOS NetX in order to generate a trace buffer that is viewable by Azure RTOS TraceX.</span></span>
- <span data-ttu-id="d9a45-113">[Bölüm 6](chapter6.md) -Azure RTOS tracex olaylarını ayrıntılı olarak açıklar.</span><span class="sxs-lookup"><span data-stu-id="d9a45-113">[Chapter 6](chapter6.md) - describes Azure RTOS TraceX events in detail.</span></span>
- <span data-ttu-id="d9a45-114">[Bölüm 7](chapter7.md) -Azure RTOS FileX olaylarını ayrıntılı olarak açıklar.</span><span class="sxs-lookup"><span data-stu-id="d9a45-114">[Chapter 7](chapter7.md) - describes Azure RTOS FileX events in detail.</span></span>
- <span data-ttu-id="d9a45-115">[Bölüm 8](chapter8.md) -Azure RTOS NETX olaylarını ayrıntılı olarak açıklar.</span><span class="sxs-lookup"><span data-stu-id="d9a45-115">[Chapter 8](chapter8.md) - describes Azure RTOS NetX events in detail.</span></span>
- <span data-ttu-id="d9a45-116">[Bölüm 9](chapter9.md) -Azure RTOS USBX olaylarını ayrıntılı olarak açıklar.</span><span class="sxs-lookup"><span data-stu-id="d9a45-116">[Chapter 9](chapter9.md) - describes Azure RTOS USBX events in detail.</span></span>
- <span data-ttu-id="d9a45-117">[Bölüm 10](chapter10.md) -özel Kullanıcı olaylarının ayrıntılı olarak oluşturulmasını açıklar.</span><span class="sxs-lookup"><span data-stu-id="d9a45-117">[Chapter 10](chapter10.md) - describes creating custom user events in detail.</span></span>
- <span data-ttu-id="d9a45-118">[Bölüm 11](chapter11.md) -iç izleme arabelleğini ayrıntılı olarak açıklar.</span><span class="sxs-lookup"><span data-stu-id="d9a45-118">[Chapter 11](chapter11.md) - describes the internal trace buffer in detail.</span></span>
- <span data-ttu-id="d9a45-119">[Ek A](appendix-a.md) -Azure RTOS threadx bağlantı noktasına özgü bir dosya, izleme olaylarını toplamak için zaman damgası kaynağıdır.</span><span class="sxs-lookup"><span data-stu-id="d9a45-119">[Appendix A](appendix-a.md) - Azure RTOS ThreadX port-specific file with its time-stamp source for gathering trace events.</span></span>
- <span data-ttu-id="d9a45-120">[Ek B](appendix-b.md) -Azure RTOS threadx *tx_trace. h* dosyası olay izleme arabelleği ile ilgili uygulama ayrıntılarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="d9a45-120">[Appendix B](appendix-b.md) - Azure RTOS ThreadX *tx_trace.h* file that shows implementation details regarding the event trace buffer.</span></span>
- <span data-ttu-id="d9a45-121">[Ek C](appendix-c.md) -çeşitli dosya biçimlerini uygun Azure RTOS tracex ikili dosyalarına dönüştürmek için komut satırı yardımcı programlarını özetler.</span><span class="sxs-lookup"><span data-stu-id="d9a45-121">[Appendix C](appendix-c.md) - Summarizes command line utilities for converting various file formats into proper Azure RTOS TraceX binary files.</span></span>
- <span data-ttu-id="d9a45-122">[Ek D](appendix-d.md) -çeşitli geliştirme araçlarından izleme dosyalarını dökme örnekleri.</span><span class="sxs-lookup"><span data-stu-id="d9a45-122">[Appendix D](appendix-d.md) - Examples of dumping trace files from various development tools.</span></span>

## <a name="guide-conventions"></a><span data-ttu-id="d9a45-123">Kılavuz kuralları</span><span class="sxs-lookup"><span data-stu-id="d9a45-123">Guide Conventions</span></span>

<span data-ttu-id="d9a45-124">*İtalik* yazı tipi, kitap başlıklarını belirtir, önemli sözcükleri vurgular ve değişkenleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="d9a45-124">*Italics* - Typeface denotes book titles, emphasizes important words, and indicates variables.</span></span>

<span data-ttu-id="d9a45-125">**Kalın** yazı tipi, dosya adlarını, anahtar sözcükleri ve önemli sözcükleri ve değişkenleri daha fazla vurgulamaktadır.</span><span class="sxs-lookup"><span data-stu-id="d9a45-125">**Boldface** - Typeface denotes file names, key words, and further emphasizes important words and variables.</span></span>

> [!NOTE]
> <span data-ttu-id="d9a45-126">Notun bilgilerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="d9a45-126">Indicates information of note.</span></span>

## <a name="customer-support-center"></a><span data-ttu-id="d9a45-127">Müşteri Destek Merkezi</span><span class="sxs-lookup"><span data-stu-id="d9a45-127">Customer Support Center</span></span>

<span data-ttu-id="d9a45-128">Lütfen buradaki adımları kullanarak sorularınız için Azure portalı üzerinden bir destek bileti bildirin.</span><span class="sxs-lookup"><span data-stu-id="d9a45-128">Please submit a support ticket through the Azure Portal for questions or help using the steps here.</span></span> <span data-ttu-id="d9a45-129">Destek isteğinizi daha verimli bir şekilde çözebilmemiz için lütfen aşağıdaki bilgileri bir e-posta iletisiyle bize girin:</span><span class="sxs-lookup"><span data-stu-id="d9a45-129">Please supply us with the following information in an email message so we can more efficiently resolve your support request:</span></span>

1. <span data-ttu-id="d9a45-130">Sorunun sıklığı ve güvenilir bir şekilde yeniden oluşturulup oluşturulamayacağından ilgili ayrıntılı bir açıklama.</span><span class="sxs-lookup"><span data-stu-id="d9a45-130">A detailed description of the problem, including frequency of occurrence and whether it can be reliably reproduced.</span></span>
2. <span data-ttu-id="d9a45-131">Uygulamada ve/veya Azure RTOS ThreadX üzerinde yapılan tüm değişikliklere ilişkin ayrıntılı bir açıklama, bundan önce sorun.</span><span class="sxs-lookup"><span data-stu-id="d9a45-131">A detailed description of any changes to the application and/or Azure RTOS ThreadX that preceded the problem.</span></span>
3. <span data-ttu-id="d9a45-132">*_Tx_version_id* dizesinin içeriği, dağılımının *tx_port. h* dosyasında bulunur.</span><span class="sxs-lookup"><span data-stu-id="d9a45-132">The contents of the *_tx_version_id* string found in the *tx_port.h* file of your distribution.</span></span> <span data-ttu-id="d9a45-133">Bu dize, çalışma zamanı ortamınız hakkında bize değerli bilgiler sağlayacaktır.</span><span class="sxs-lookup"><span data-stu-id="d9a45-133">This string will provide us valuable information regarding your run-time environment.</span></span>
4. <span data-ttu-id="d9a45-134">*_Tx_build_options* ulong değişkeninin RAM 'e ait içerik.</span><span class="sxs-lookup"><span data-stu-id="d9a45-134">The contents in RAM of the *_tx_build_options* ULONG variable.</span></span> <span data-ttu-id="d9a45-135">Bu değişken, Azure RTOS ThreadX Kitaplığınızın nasıl oluşturulduğunu öğrenmek için bize bilgi verecektir.</span><span class="sxs-lookup"><span data-stu-id="d9a45-135">This variable will give us information on how your Azure RTOS ThreadX library was built.</span></span>
