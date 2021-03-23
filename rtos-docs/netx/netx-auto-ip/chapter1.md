---
title: Bölüm 1-Azure RTOS NetX oto 'ya giriş
description: Azure RTOS NetX otomatik IP protokolü, yerel bir ağ üzerinde IPv4 adreslerini dinamik olarak yapılandırmak için tasarlanan bir protokoldür.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: c26b4112814bb586e056246d68c2597d56df6085
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826849"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-autoip"></a><span data-ttu-id="dccb5-103">Bölüm 1-Azure RTOS NetX oto 'ya giriş</span><span class="sxs-lookup"><span data-stu-id="dccb5-103">Chapter 1 - Introduction to Azure RTOS NetX AutoIP</span></span>
  
<span data-ttu-id="dccb5-104">Azure RTOS NetX otomatik IP protokolü, yerel bir ağ üzerinde IPv4 adreslerini dinamik olarak yapılandırmak için tasarlanan bir protokoldür.</span><span class="sxs-lookup"><span data-stu-id="dccb5-104">The Azure RTOS NetX AutoIP Protocol is a protocol designed for dynamically configuring IPv4 addresses on a local network.</span></span> <span data-ttu-id="dccb5-105">Otomatikten otomatik IP adresi atama işlevini gerçekleştirmek için ARP yeteneklerini kullanan basit bir protokoldür.</span><span class="sxs-lookup"><span data-stu-id="dccb5-105">AutoIP is a simple protocol that utilizes ARP capabilities to perform its automatic IP address assignment function.</span></span> <span data-ttu-id="dccb5-106">Oto, 169.254.1.0 ile 169.254.254.255 arasındaki adresleri ayırır.</span><span class="sxs-lookup"><span data-stu-id="dccb5-106">AutoIP allocates addresses in the range of 169.254.1.0 through 169.254.254.255.</span></span>

## <a name="autoip-requirements"></a><span data-ttu-id="dccb5-107">Oto IP gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="dccb5-107">AutoIP Requirements</span></span>

<span data-ttu-id="dccb5-108">NetX Oto IP paketinin düzgün çalışması için bir NetX IP örneğinin zaten oluşturulmuş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="dccb5-108">In order to function properly, the NetX AutoIP package requires that a NetX IP instance has already been created.</span></span> <span data-ttu-id="dccb5-109">Ayrıca, ARP aynı IP örneğinde etkinleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="dccb5-109">In addition, ARP must be enabled on that same IP instance.</span></span> <span data-ttu-id="dccb5-110">NetX Oto IP paketinin daha fazla gereksinimi yoktur.</span><span class="sxs-lookup"><span data-stu-id="dccb5-110">The NetX AutoIP package has no further requirements.</span></span>

## <a name="autoip-constraints"></a><span data-ttu-id="dccb5-111">Oto IP kısıtlamaları</span><span class="sxs-lookup"><span data-stu-id="dccb5-111">AutoIP Constraints</span></span> 

<span data-ttu-id="dccb5-112">NetX Oto IP protokolü RFC3927 standart gereksinimlerini uygular.</span><span class="sxs-lookup"><span data-stu-id="dccb5-112">The NetX AutoIP protocol implements the requirements of the RFC3927 standard.</span></span> <span data-ttu-id="dccb5-113">Ancak, aşağıdaki kısıtlamalar vardır:</span><span class="sxs-lookup"><span data-stu-id="dccb5-113">However, there are the following constraints:</span></span>

1. <span data-ttu-id="dccb5-114">NetX DHCP kullanılıyorsa, DHCP iş parçacığının hem NetX IP örneği iş parçacığından hem de Oto IP iş parçacığından daha yüksek bir önceliğe sahip oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="dccb5-114">If NetX DHCP is used, the DHCP thread must be created with a higher priority than both the NetX IP instance thread and the AutoIP thread.</span></span>
1. <span data-ttu-id="dccb5-115">NetX Oto, eski IP adreslerinin kullanılmaya devam etmesi için bir mekanizma sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="dccb5-115">NetX AutoIP does not provide a mechanism for old IP addresses to continue being used.</span></span>
1. <span data-ttu-id="dccb5-116">IP adresi değiştiğinde, uygulama var olan herhangi bir TCP bağlantısını kapatmaktan ve yeni IP adresinde yeniden oluşturmaya sorumludur.</span><span class="sxs-lookup"><span data-stu-id="dccb5-116">When the IP address changes, the application is responsible for tearing down any existing TCP connections and re-establishing them on the new IP address.</span></span>

## <a name="autoip-protocol-implementation"></a><span data-ttu-id="dccb5-117">Oto IP protokol uygulamasını</span><span class="sxs-lookup"><span data-stu-id="dccb5-117">AutoIP Protocol Implementation</span></span>

<span data-ttu-id="dccb5-118">NetX Oto IP Protokolü ilk olarak 169.254.1.0 ile 169.254.254.255 arasındaki Oto IP IPv4 adres aralığı içinde bir rastgele adres seçer.</span><span class="sxs-lookup"><span data-stu-id="dccb5-118">The NetX AutoIP protocol first selects a random address within the AutoIP IPv4 address range of 169.254.1.0 through 169.254.254.255.</span></span> <span data-ttu-id="dccb5-119">Alternatif olarak, uygulama bir başlangıç IP adresini ***nx_auto_ip_start*** işlevine vererek zorlayabilir.</span><span class="sxs-lookup"><span data-stu-id="dccb5-119">Alternatively, the application may force a starting IP address by providing it to the ***nx_auto_ip_start*** function.</span></span> <span data-ttu-id="dccb5-120">Bu, bir önceki çalıştırmada bir Oto IP adresinin başarıyla kullanıldığı durumlarda faydalıdır.</span><span class="sxs-lookup"><span data-stu-id="dccb5-120">This is useful in situations where an AutoIP address was successfully used in a prior run.</span></span>

<span data-ttu-id="dccb5-121">Bir Oto IP adresi seçildikten sonra NetX Oto, seçili adres için bir dizi ARP araştırmalarını gönderir.</span><span class="sxs-lookup"><span data-stu-id="dccb5-121">Once an AutoIP address is selected, NetX AutoIP sends out a series of ARP probes for the selected address.</span></span> <span data-ttu-id="dccb5-122">Bir ARP araştırması, gönderen adresi 0.0.0.0 olarak ayarlanmış bir ARP isteği iletisinden ve hedef adres istenen bir IP adresine ayarlı.</span><span class="sxs-lookup"><span data-stu-id="dccb5-122">An ARP probe consists of an ARP request message with the sender address set to 0.0.0.0 and the target address set to the desired AutoIP address.</span></span> <span data-ttu-id="dccb5-123">Bu ARP araştırmalarının bir serisi gönderilir (gerçek sayı, tanımlama NX_AUTO_IP_PROBE_NUM tarafından belirlenir).</span><span class="sxs-lookup"><span data-stu-id="dccb5-123">A series of these ARP probes are sent (the actual number is determined by the define NX_AUTO_IP_PROBE_NUM).</span></span> <span data-ttu-id="dccb5-124">Başka bir ağ düğümü bu araştırmasına yanıt verirse veya aynı adres için aynı araştırma gönderirse, Oto IP IPv4 adres aralığı içinde yeni bir Oto IP adresi rastgele seçilir ve araştırma işlemi yinelenir.</span><span class="sxs-lookup"><span data-stu-id="dccb5-124">If another network node responds to this probe or sends an identical probe for the same address, a new AutoIP address is randomly selected within the AutoIP IPv4 address range and the probe processing repeats.</span></span>

<span data-ttu-id="dccb5-125">NX_AUTO_IP_PROBE_NUM araştırmaları herhangi bir yanıt olmadan gönderilirse, NetX Oto, seçili adres için bir dizi ARP duyuruları yayınlar.</span><span class="sxs-lookup"><span data-stu-id="dccb5-125">If NX_AUTO_IP_PROBE_NUM probes are sent without any responses, NetX AutoIP issues a series of ARP announcements for the selected address.</span></span> <span data-ttu-id="dccb5-126">Bir ARP duyurusu, ARP iletisinde hem gönderen hem de hedef adresi olan bir ARP istek iletisinden, seçili Oto IP adresine ayarlanmış olarak oluşur.</span><span class="sxs-lookup"><span data-stu-id="dccb5-126">An ARP announcement consists of an ARP request message with both the sender and target address in the ARP message set to the selected AutoIP address.</span></span> <span data-ttu-id="dccb5-127">Tanımlama NX_AUTO_IP_ANNOUNCE_NUM karşılık gelen bir dizi ARP duyurusu iletisi gönderilir.</span><span class="sxs-lookup"><span data-stu-id="dccb5-127">A series of ARP announcement messages are sent, corresponding to the define NX_AUTO_IP_ANNOUNCE_NUM.</span></span> <span data-ttu-id="dccb5-128">Başka bir ağ düğümü bir bildirme iletisine yanıt verirse veya aynı adres için özdeş bir duyuru gönderirse, Oto IP IPv4 adres aralığı içinde yeni bir Oto IP adresi rastgele seçilir ve araştırma işlemi baştan başlar.</span><span class="sxs-lookup"><span data-stu-id="dccb5-128">If another network node responds to an announce message or sends an identical announcement for the same address, a new AutoIP address is randomly selected within the AutoIP IPv4 address range and the probe processing starts over.</span></span>

<span data-ttu-id="dccb5-129">Araştırma ve duyuru algılanan herhangi bir çakışma olmadan tamamlandığında, seçilen Oto IP adresi geçerli kabul edilir ve ilişkili IP örneği bu adresle birlikte ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="dccb5-129">When the probe and announcement completes without any detected conflicts, the selected AutoIP address is considered valid and the associated IP instance is setup with this address.</span></span>

## <a name="autoip-address-change"></a><span data-ttu-id="dccb5-130">Oto IP adresi değişikliği</span><span class="sxs-lookup"><span data-stu-id="dccb5-130">AutoIP Address Change</span></span>

<span data-ttu-id="dccb5-131">Daha önce bahsedildiği gibi, NetX Oto, başarılı araştırma ve duyuru işlemeden sonra IP örnek adresini değiştirir.</span><span class="sxs-lookup"><span data-stu-id="dccb5-131">As mentioned before, NetX AutoIP changes the IP instance address after successful probe and announcement processing.</span></span> <span data-ttu-id="dccb5-132">Bu durum için izleme, önemli değildir.</span><span class="sxs-lookup"><span data-stu-id="dccb5-132">Monitoring for this case is not terribly important.</span></span> <span data-ttu-id="dccb5-133">Ancak, daha sonra, Oto IP adresinin değiştirilmesini sağlamak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="dccb5-133">However, it is possible to have the AutoIP address change in the future.</span></span> <span data-ttu-id="dccb5-134">Olası nedenler, gelecekteki Oto IP adresi çakışmalarını ve DHCP adres çözümlemesini de kapsar.</span><span class="sxs-lookup"><span data-stu-id="dccb5-134">Potential causes include future AutoIP address conflicts as well as DHCP address resolution.</span></span> <span data-ttu-id="dccb5-135">Bu olası durumları düzgün bir şekilde işlemek için, uygulamanın herhangi bir IP adresi değişikliğini ve tümünü uyarmak üzere aşağıdaki NetX API 'sini kullanması gerekir:</span><span class="sxs-lookup"><span data-stu-id="dccb5-135">In order to process these potential situations properly, the application should use the following NetX API to alert it of any and all IP address changes:</span></span>

```c
nx_ip_address_change_notify(NX_IP *ip_ptr,
                            VOID (*ip_address_change_notify)(NX_IP *,VOID*),
                            VOID *additional_info);
```

<span data-ttu-id="dccb5-136">Sağlanan *ip_address_change_notify* Işlevindeki Işleme NETX yeniden BAŞLATıLMALıDıR veya DHCP 'nin IP adresini daha sonra çözümlediği takdirde devre dışı bırakmalıdır.</span><span class="sxs-lookup"><span data-stu-id="dccb5-136">The processing in the supplied *ip_address_change_notify* function must either restart the NetX AutoIP processor or disable it if DHCP has subsequently resolved the IP address.</span></span> <span data-ttu-id="dccb5-137">Örnek işleme için lütfen *küçük örnek sistem* bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="dccb5-137">Please refer to the *Small Example System* section for sample processing.</span></span>

## <a name="autoip-rfcs"></a><span data-ttu-id="dccb5-138">Oto IP RFC 'Leri</span><span class="sxs-lookup"><span data-stu-id="dccb5-138">AutoIP RFCs</span></span>

<span data-ttu-id="dccb5-139">NetX oto RFC3927 ve ilgili RFC 'Ler ile uyumludur.</span><span class="sxs-lookup"><span data-stu-id="dccb5-139">NetX AutoIP is compliant with RFC3927 and related RFCs.</span></span>