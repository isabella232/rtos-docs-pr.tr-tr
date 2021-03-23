---
title: Azure RTOS USBX cihaz yığını Kullanıcı Kılavuzu
description: Bu kılavuz, Microsoft 'un yüksek performanslı USB Foundation yazılımı olan Azure RTOS USBX hakkında kapsamlı bilgiler sağlar
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: c8e9360c8b72adbc41f840a48e333668c489399e
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825427"
---
# <a name="azure-rtos-usbx-device-stack-user-guide"></a><span data-ttu-id="1f75f-103">Azure RTOS USBX cihaz yığını Kullanıcı Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="1f75f-103">Azure RTOS USBX Device Stack User Guide</span></span>

<span data-ttu-id="1f75f-104">Bu kılavuz, Microsoft 'un yüksek performanslı USB Foundation yazılımı olan Azure RTOS USBX hakkında kapsamlı bilgiler sağlar.</span><span class="sxs-lookup"><span data-stu-id="1f75f-104">This guide provides comprehensive information about Azure RTOS USBX, the high performance USB foundation software from Microsoft.</span></span>

<span data-ttu-id="1f75f-105">Katıştırılmış gerçek zamanlı yazılım geliştiricisi için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="1f75f-105">It is intended for the embedded real-time software developer.</span></span> <span data-ttu-id="1f75f-106">Geliştirici standart gerçek zamanlı işletim sistemi işlevleriyle, USB belirtimine ve C programlama diline tanıdık gelmelidir.</span><span class="sxs-lookup"><span data-stu-id="1f75f-106">The developer should be familiar with standard real-time operating system functions, the USB specification, and the C programming language.</span></span>

<span data-ttu-id="1f75f-107">USB ile ilgili teknik bilgiler için, bkz. indirilebilecek USB belirtimi ve USB sınıfı belirtimleri https://www.USB.org/developers</span><span class="sxs-lookup"><span data-stu-id="1f75f-107">For technical information related to USB, see the USB specification and USB Class specifications that can be downloaded at https://www.USB.org/developers</span></span>

## <a name="organization"></a><span data-ttu-id="1f75f-108">Kuruluş</span><span class="sxs-lookup"><span data-stu-id="1f75f-108">Organization</span></span>

- <span data-ttu-id="1f75f-109">[**Bölüm 1**](usbx-device-stack-1.md) -Azure RTOS USBX 'e giriş içerir</span><span class="sxs-lookup"><span data-stu-id="1f75f-109">[**Chapter 1**](usbx-device-stack-1.md) - contains an introduction to Azure RTOS USBX</span></span>

- <span data-ttu-id="1f75f-110">[**Bölüm 2**](usbx-device-stack-2.md) -Azure RTOS USBX 'ı threadx uygulamanızla birlikte yüklemek ve kullanmak için temel adımları sağlar</span><span class="sxs-lookup"><span data-stu-id="1f75f-110">[**Chapter 2**](usbx-device-stack-2.md) - gives the basic steps to install and use Azure RTOS USBX with your ThreadX application</span></span>

- <span data-ttu-id="1f75f-111">[**Bölüm 3**](usbx-device-stack-3.md) -Azure RTOS USBX cihaz yığınının işlevsel bileşenlerini açıklar</span><span class="sxs-lookup"><span data-stu-id="1f75f-111">[**Chapter 3**](usbx-device-stack-3.md) - describes the functional components of the Azure RTOS USBX device stack</span></span>

- <span data-ttu-id="1f75f-112">[**Bölüm 4**](usbx-device-stack-4.md) -Azure RTOS USBX cihaz yığını hizmetlerini açıklar</span><span class="sxs-lookup"><span data-stu-id="1f75f-112">[**Chapter 4**](usbx-device-stack-4.md) - describes the Azure RTOS USBX device stack services</span></span>

- <span data-ttu-id="1f75f-113">[**Bölüm 5**](usbx-device-stack-5.md) -API 'leri dahil olmak üzere her BIR Azure RTOS USBX cihaz sınıfını açıklar</span><span class="sxs-lookup"><span data-stu-id="1f75f-113">[**Chapter 5**](usbx-device-stack-5.md) - describes each Azure RTOS USBX device class including their APIs</span></span>

## <a name="customer-support-center"></a><span data-ttu-id="1f75f-114">Müşteri Destek Merkezi</span><span class="sxs-lookup"><span data-stu-id="1f75f-114">Customer Support Center</span></span>

<span data-ttu-id="1f75f-115">Lütfen buradaki adımları kullanarak sorularınız için Azure portalı üzerinden bir destek bileti bildirin.</span><span class="sxs-lookup"><span data-stu-id="1f75f-115">Please submit a support ticket through the Azure Portal for questions or help using the steps here.</span></span> <span data-ttu-id="1f75f-116">Destek isteğinizi daha verimli bir şekilde çözebilmemiz için lütfen aşağıdaki bilgileri bir e-posta iletisiyle bize girin:</span><span class="sxs-lookup"><span data-stu-id="1f75f-116">Please supply us with the following information in an email message so we can more efficiently resolve your support request:</span></span>

1. <span data-ttu-id="1f75f-117">Sorunun sıklığı ve güvenilir bir şekilde yeniden oluşturulup oluşturulamayacağından ilgili ayrıntılı bir açıklama.</span><span class="sxs-lookup"><span data-stu-id="1f75f-117">A detailed description of the problem, including frequency of occurrence and whether it can be reliably reproduced.</span></span>
2. <span data-ttu-id="1f75f-118">Uygulamada ve/veya Azure RTOS ThreadX üzerinde yapılan tüm değişikliklere ilişkin ayrıntılı bir açıklama, bundan önce sorun.</span><span class="sxs-lookup"><span data-stu-id="1f75f-118">A detailed description of any changes to the application and/or Azure RTOS ThreadX that preceded the problem.</span></span>
3. <span data-ttu-id="1f75f-119">**_Tx_version_id** dizesinin içeriği, dağılımının **_tx_port. h_** dosyasında bulunur.</span><span class="sxs-lookup"><span data-stu-id="1f75f-119">The contents of the **_tx_version_id** string found in the **_tx_port.h_** file of your distribution.</span></span> <span data-ttu-id="1f75f-120">Bu dize, çalışma zamanı ortamınız hakkında bize değerli bilgiler sağlayacaktır.</span><span class="sxs-lookup"><span data-stu-id="1f75f-120">This string will provide us valuable information regarding your run-time environment.</span></span>
4. <span data-ttu-id="1f75f-121">*_Tx_build_options* **ulong** değişkeninin RAM 'e ait içerik.</span><span class="sxs-lookup"><span data-stu-id="1f75f-121">The contents in RAM of the *_tx_build_options* **ULONG** variable.</span></span> <span data-ttu-id="1f75f-122">Bu değişken, Azure RTOS ThreadX Kitaplığınızın nasıl oluşturulduğunu öğrenmek için bize bilgi verecektir.</span><span class="sxs-lookup"><span data-stu-id="1f75f-122">This variable will give us information on how your Azure RTOS ThreadX library was built.</span></span>
