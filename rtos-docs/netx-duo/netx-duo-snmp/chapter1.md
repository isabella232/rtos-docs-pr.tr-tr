---
title: Bölüm 1-Azure RTOS NetX Duo SNMP 'ye giriş
description: NetX Duo SNMP uygulamasının bir SNMP aracısının olması. Bir aracı SNMP yöneticisinin komutlarına yanıt vermemeye ve olay odaklı tuzakları göndermeye sorumludur.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 5760e35fdbe8d7b27e2ccc82abac37b1f6fb5118
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825781"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-snmp"></a><span data-ttu-id="6752a-104">Bölüm 1-Azure RTOS NetX Duo SNMP 'ye giriş</span><span class="sxs-lookup"><span data-stu-id="6752a-104">Chapter 1 - Introduction to Azure RTOS NetX Duo SNMP</span></span>

<span data-ttu-id="6752a-105">Basit Ağ Yönetim Protokolü (SNMP), internet 'teki cihazları yönetmek için tasarlanmış bir protokoldür.</span><span class="sxs-lookup"><span data-stu-id="6752a-105">The Simple Network Management Protocol (SNMP) is a protocol designed for managing devices on the internet.</span></span> <span data-ttu-id="6752a-106">SNMP, yönetim işlevini gerçekleştirmek için bağlantısız Kullanıcı Datagram Protokolü (UDP) hizmetlerinden yararlanan bir protokoldür.</span><span class="sxs-lookup"><span data-stu-id="6752a-106">SNMP is a protocol that utilizes the connectionless User Datagram Protocol (UDP) services to perform its management function.</span></span> <span data-ttu-id="6752a-107">Azure RTOS NetX Duo SNMP uygulamasının bir SNMP aracısının olması vardır.</span><span class="sxs-lookup"><span data-stu-id="6752a-107">The Azure RTOS NetX Duo SNMP implementation is that of an SNMP Agent.</span></span> <span data-ttu-id="6752a-108">Bir aracı SNMP yöneticisinin komutlarına yanıt vermemeye ve olay odaklı tuzakları göndermeye sorumludur.</span><span class="sxs-lookup"><span data-stu-id="6752a-108">An agent is responsible for responding to SNMP Manager’s commands and sending event driven traps.</span></span> 

<span data-ttu-id="6752a-109">NetX Duo SNMP, SNMP yöneticileriyle hem IPv4 hem de IPv6 iletişimini destekler.</span><span class="sxs-lookup"><span data-stu-id="6752a-109">NetX Duo SNMP supports both IPv4 and IPv6 communication with SNMP Managers.</span></span> <span data-ttu-id="6752a-110">NetX SNMP uygulamalarının NetX Duo SNMP 'de derlenmesi ve çalıştırması gerekir.</span><span class="sxs-lookup"><span data-stu-id="6752a-110">NetX SNMP applications should compile and run in NetX Duo SNMP.</span></span> <span data-ttu-id="6752a-111">Ancak, geliştiricinin eşdeğer "Duo" hizmetlerini kullanarak mevcut SNMP uygulamalarının bağlantı noktası olması önerilir.</span><span class="sxs-lookup"><span data-stu-id="6752a-111">However, the developer is encouraged to port existing SNMP applications to using the equivalent “duo” services.</span></span> <span data-ttu-id="6752a-112">Örneğin, SNMP tuzak iletileri gönderirken aşağıdaki ' Duo ' hizmetlerinin NetX eşdeğerini yerine girmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="6752a-112">For example, when sending SNMP trap messages, the following ‘duo’ services should replace their NetX equivalent:</span></span>

<span data-ttu-id="6752a-113">*nxd_snmp_object_trap_send*</span><span class="sxs-lookup"><span data-stu-id="6752a-113">*nxd_snmp_object_trap_send*</span></span>

<span data-ttu-id="6752a-114">*nxd_snmp_object_trapv2_send*</span><span class="sxs-lookup"><span data-stu-id="6752a-114">*nxd_snmp_object_trapv2_send*</span></span>

<span data-ttu-id="6752a-115">*nxd_snmp_object_trapv3_send*</span><span class="sxs-lookup"><span data-stu-id="6752a-115">*nxd_snmp_object_trapv3_send*</span></span>

<span data-ttu-id="6752a-116">Daha fazla ayrıntı için bu kullanıcı kılavuzunun başka bir yerinde **SNMP Aracısı hizmetleri açıklamasına** bakın.</span><span class="sxs-lookup"><span data-stu-id="6752a-116">For more details, see **Description of SNMP Agent Services** elsewhere in this User Guide for more details.</span></span>

## <a name="netx-duo-snmp-agent-requirements"></a><span data-ttu-id="6752a-117">NetX Duo SNMP Aracısı gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="6752a-117">NetX Duo SNMP Agent Requirements</span></span>

<span data-ttu-id="6752a-118">NetX Duo SNMP paketi bir IP örneğinin zaten oluşturulmuş olmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="6752a-118">The NetX Duo SNMP package requires that an IP instance has already been created.</span></span> <span data-ttu-id="6752a-119">Buna ek olarak, aynı IP örneğinde UDP 'nin etkinleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="6752a-119">In addition, UDP must be enabled on that same IP instance.</span></span>

<span data-ttu-id="6752a-120">NetX Duo SNMP aracısının birkaç ek gereksinimi vardır.</span><span class="sxs-lookup"><span data-stu-id="6752a-120">The NetX Duo SNMP Agent has several additional requirements.</span></span> <span data-ttu-id="6752a-121">İlk olarak, tüm SNMP Yöneticisi isteklerini işlemek için 161 numaralı bağlantı noktasına erişim gerektirir.</span><span class="sxs-lookup"><span data-stu-id="6752a-121">First, it requires access to port 161 for handling all SNMP manager requests.</span></span> <span data-ttu-id="6752a-122">Ayrıca, yöneticiye tuzak iletileri göndermek için 162 numaralı bağlantı noktasına erişim gerektirir.</span><span class="sxs-lookup"><span data-stu-id="6752a-122">It also requires access to port 162 for sending trap messages to the Manager.</span></span>

<span data-ttu-id="6752a-123">NetX Duo SNMP aracısını IPv6 üzerinden kullanmak ve IPv6 nesnelerini almak için, IPv6 'yı NetX Duo içinde etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6752a-123">To use NetX Duo SNMP Agent with over IPv6 and to obtain IPv6 objects, IPv6 must be enabled in NetX Duo.</span></span> <span data-ttu-id="6752a-124">IPv6 Hizmetleri için IP örneğini etkinleştirme hakkında ayrıntılı bilgi için bkz. ***NETX Duo Kullanıcı Kılavuzu*** .</span><span class="sxs-lookup"><span data-stu-id="6752a-124">See the ***NetX Duo User Guide*** for details on enabling the IP instance for IPv6 services.</span></span>

## <a name="netx-duo-snmp-constraints"></a><span data-ttu-id="6752a-125">NetX Duo SNMP kısıtlamaları</span><span class="sxs-lookup"><span data-stu-id="6752a-125">NetX Duo SNMP Constraints</span></span>

<span data-ttu-id="6752a-126">NetX Duo SNMP protokolü SNMP sürüm 1, 2 ve 3 ' ü uygular.</span><span class="sxs-lookup"><span data-stu-id="6752a-126">The NetX Duo SNMP protocol implements SNMP Version 1, 2, and 3.</span></span> <span data-ttu-id="6752a-127">SNMPv3 uygulama, MD5 ve SHA kimlik doğrulamasını ve DES şifrelemesini destekler.</span><span class="sxs-lookup"><span data-stu-id="6752a-127">The SNMPv3 implementation supports MD5 and SHA authentication, and DES encryption.</span></span> <span data-ttu-id="6752a-128">NetX Duo SNMP aracısının bu sürümü aşağıdaki kısıtlamalara sahiptir:</span><span class="sxs-lookup"><span data-stu-id="6752a-128">This version of the NetX Duo SNMP Agent has the following constraints:</span></span>

1. <span data-ttu-id="6752a-129">NetX IP örneği başına bir SNMP Aracısı</span><span class="sxs-lookup"><span data-stu-id="6752a-129">One SNMP Agent per NetX IP Instance</span></span>
2. <span data-ttu-id="6752a-130">RMON desteği yok</span><span class="sxs-lookup"><span data-stu-id="6752a-130">No support for RMON</span></span>
3. <span data-ttu-id="6752a-131">SNMP v3 bilgilendirme iletileri desteklenmez</span><span class="sxs-lookup"><span data-stu-id="6752a-131">SNMP v3 Inform messages are not supported</span></span>
4. <span data-ttu-id="6752a-132">DONUK ve NSAP veri türleri desteklenmez</span><span class="sxs-lookup"><span data-stu-id="6752a-132">OPAQUE and NSAP data types are not supported</span></span>
5. <span data-ttu-id="6752a-133">IPv6 adresleri sekizli dizeler olarak tanımlanır ve Biçim denetimi uygulamaya bırakılır.</span><span class="sxs-lookup"><span data-stu-id="6752a-133">IPv6 addresses are defined as octet strings, and format checking is left to the application.</span></span>

## <a name="snmp-object-names"></a><span data-ttu-id="6752a-134">SNMP nesne adları</span><span class="sxs-lookup"><span data-stu-id="6752a-134">SNMP Object Names</span></span>

<span data-ttu-id="6752a-135">SNMP protokolü, internet 'teki cihazları yönetmek için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="6752a-135">The SNMP protocol is designed to manage devices on the internet.</span></span> <span data-ttu-id="6752a-136">Bu işlemi gerçekleştirmek için, her SNMP yönetilen cihazının, RFC 1155 tarafından tanımlanan yönetim bilgileri (SMı) yapısı tarafından tanımlanan bir nesne kümesi vardır.</span><span class="sxs-lookup"><span data-stu-id="6752a-136">To accomplish this, each SNMP managed device has a set of objects that are defined by the Structure of Management Information (SMI) as defined by RFC 1155.</span></span> <span data-ttu-id="6752a-137">Yapı, aşağıdaki gibi görünen bir yapı hiyerarşik ağaç türüdür:</span><span class="sxs-lookup"><span data-stu-id="6752a-137">The structure is a hierarchical tree type of structure that looks like the following:</span></span>

![Yönetim bilgileri yapısının diyagramı.](media/image3.png)

<span data-ttu-id="6752a-139">Ağaçtaki her düğüm bir nesnedir.</span><span class="sxs-lookup"><span data-stu-id="6752a-139">Each node in the tree is an object.</span></span> <span data-ttu-id="6752a-140">Ağaçtaki "DOD" nesnesi, 1.3.6 gösterimi tarafından tanımlanır, ancak ağaçtaki "Internet" nesnesi 1.3.6.1 gösterimi tarafından tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="6752a-140">The “dod” object in the tree is identified by the notation 1.3.6, while the “internet” object in the tree is identified by the notation 1.3.6.1.</span></span> <span data-ttu-id="6752a-141">Tüm SNMP nesne adları 1.3.6 gösterimi ile başlar.</span><span class="sxs-lookup"><span data-stu-id="6752a-141">All SNMP object names begin with the notation 1.3.6.</span></span>

<span data-ttu-id="6752a-142">Bir SNMP Yöneticisi, cihazdaki hangi nesneyi almak veya ayarlamak istediğinizi belirtmek için bu nesne gösterimini kullanır.</span><span class="sxs-lookup"><span data-stu-id="6752a-142">An SNMP Manager uses this object notation to specify what object in the device it wishes to get or set.</span></span> <span data-ttu-id="6752a-143">NetX Duo SNMP Aracısı, bu tür yönetici isteklerini Yorumlar ve uygulamanın istenen işlemi gerçekleştirmesi için mekanizmalar sağlar.</span><span class="sxs-lookup"><span data-stu-id="6752a-143">The NetX Duo SNMP Agent interprets such manager requests and provides mechanisms for the application to perform the requested operation.</span></span>

## <a name="snmp-manager-requests"></a><span data-ttu-id="6752a-144">SNMP Yöneticisi Istekleri</span><span class="sxs-lookup"><span data-stu-id="6752a-144">SNMP Manager Requests</span></span>

<span data-ttu-id="6752a-145">SNMP 'nin cihazları yönetmek için basit bir mekanizması vardır.</span><span class="sxs-lookup"><span data-stu-id="6752a-145">The SNMP has a simple mechanism for managing devices.</span></span> <span data-ttu-id="6752a-146">SNMP Yöneticisi tarafından *161 numaralı bağlantı* noktasında SNMP cihazına VERILEN standart SNMP komutları kümesi vardır.</span><span class="sxs-lookup"><span data-stu-id="6752a-146">There is a set of standard SNMP commands that are issued by the SNMP Manager to the SNMP device on *port 161*.</span></span> <span data-ttu-id="6752a-147">Aşağıdakiler, temel SNMP Yöneticisi komutlarının bazılarını göstermektedir:</span><span class="sxs-lookup"><span data-stu-id="6752a-147">The following shows some of the basic SNMP Manager commands:</span></span>

| <span data-ttu-id="6752a-148">SNMP komutu</span><span class="sxs-lookup"><span data-stu-id="6752a-148">SNMP Command</span></span> | <span data-ttu-id="6752a-149">Anlamı</span><span class="sxs-lookup"><span data-stu-id="6752a-149">Meaning</span></span>                                                        |
|--------------|----------------------------------------------------------------|
| <span data-ttu-id="6752a-150">GET</span><span class="sxs-lookup"><span data-stu-id="6752a-150">GET</span></span>          | <span data-ttu-id="6752a-151">*Belirtilen nesneyi al*</span><span class="sxs-lookup"><span data-stu-id="6752a-151">*Get the specified object*</span></span>                                       |
| <span data-ttu-id="6752a-152">GETNEXT</span><span class="sxs-lookup"><span data-stu-id="6752a-152">GETNEXT</span></span>      | <span data-ttu-id="6752a-153">*Belirtilen nesne KIMLIĞINDEN sonraki mantıksal nesneyi al*</span><span class="sxs-lookup"><span data-stu-id="6752a-153">*Get the next logical object after the specified object ID*</span></span>      |
| <span data-ttu-id="6752a-154">GETBULK</span><span class="sxs-lookup"><span data-stu-id="6752a-154">GETBULK</span></span>      | <span data-ttu-id="6752a-155">*Belirtilen nesne KIMLIĞINDEN sonra birden çok mantıksal nesne al*</span><span class="sxs-lookup"><span data-stu-id="6752a-155">*Get the multiple logical objects after the specified object ID*</span></span> |
| <span data-ttu-id="6752a-156">SET</span><span class="sxs-lookup"><span data-stu-id="6752a-156">SET</span></span>          | <span data-ttu-id="6752a-157">*Belirtilen nesneyi ayarla*</span><span class="sxs-lookup"><span data-stu-id="6752a-157">*Set the specified object*</span></span>                                       |

<span data-ttu-id="6752a-158">Bu komutlar, soyut sözdizimi gösterimi bir (ASN. 1) biçiminde kodlanır ve SNMP Yöneticisi tarafından gönderilen UDP paketinin yükünde bulunur.</span><span class="sxs-lookup"><span data-stu-id="6752a-158">These commands are encoded in the Abstract Syntax Notation One (ASN.1) format and reside in the payload of the UDP packet sent by the SNMP Manager.</span></span> <span data-ttu-id="6752a-159">NetX Duo SNMP Aracısı isteği işler ve sonra ***nx_snmp_agent_create*** çağrısında belirtilen karşılık gelen işleme yordamını çağırır.</span><span class="sxs-lookup"><span data-stu-id="6752a-159">The NetX Duo SNMP Agent processes the request and then calls the corresponding handling routine specified in the ***nx_snmp_agent_create*** call.</span></span>

## <a name="netx-duo-snmp-agent-traps"></a><span data-ttu-id="6752a-160">NetX Duo SNMP aracı tuzakları</span><span class="sxs-lookup"><span data-stu-id="6752a-160">NetX Duo SNMP Agent Traps</span></span>

<span data-ttu-id="6752a-161">NetX Duo SNMP aracısı ayrıca bir olay SNMP yöneticisini zaman uyumsuz olarak uyarma yeteneği sağlar.</span><span class="sxs-lookup"><span data-stu-id="6752a-161">The NetX Duo SNMP Agent provides the ability to also alert an SNMP Manager of events asynchronously.</span></span> <span data-ttu-id="6752a-162">Bu, bir SNMP tuzağı komutu aracılığıyla yapılır.</span><span class="sxs-lookup"><span data-stu-id="6752a-162">This is done via an SNMP trap command.</span></span> <span data-ttu-id="6752a-163">SNMP Yöneticisi 'ne tuzak göndermek için her SNMP sürümü için benzersiz bir API vardır.</span><span class="sxs-lookup"><span data-stu-id="6752a-163">There is a unique API for each version of SNMP for sending traps to an SNMP Manager.</span></span> <span data-ttu-id="6752a-164">Varsayılan olarak, tuzaklar 162 numaralı bağlantı noktasında SNMP Yöneticisi 'ne gönderilir.</span><span class="sxs-lookup"><span data-stu-id="6752a-164">By default, the traps are sent to the SNMP Manager on port 162.</span></span>

<span data-ttu-id="6752a-165">NetX Duo SNMP Aracısı, SNMPv3 tuzak iletileri için ayrı güvenlik anahtarları sağlar.</span><span class="sxs-lookup"><span data-stu-id="6752a-165">The NetX Duo SNMP Agent provides separate security keys for SNMPv3 trap messages.</span></span> <span data-ttu-id="6752a-166">Bunu yapmak için SNMP uygulamasının, yönetici isteklerine yapılan yanıtlara uygulananlardan ayrı bir anahtar kümesi oluşturması gerekir.</span><span class="sxs-lookup"><span data-stu-id="6752a-166">To do so, the SNMP application must create a separate set of keys from those applied to responses to Manager requests.</span></span> <span data-ttu-id="6752a-167">Tuzak güvenliği, SNMP aracısının kimlik doğrulama ve gizlilik için aynı veya farklı parolaları kullanmasına olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="6752a-167">Trap security enables the SNMP Agent to use the same or different passwords for authentication and privacy.</span></span> <span data-ttu-id="6752a-168">Güvenlik anahtarları oluşturma hakkında daha fazla bilgi için, sonraki bölümde **NETX Duo SNMP kimlik doğrulaması ve şifreleme** bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="6752a-168">For more information on creating security keys, see **NetX Duo SNMP Authentication and Encryption** in the next section.</span></span>

<span data-ttu-id="6752a-169">Standart SNMP yakalama değişkenlerinin listesi *nxd_snmp. h* 'nin üstünde numaralandırılır:</span><span class="sxs-lookup"><span data-stu-id="6752a-169">A list of standard SNMP trap variables is enumerated at the top of *nxd_snmp.h:*</span></span>

| <span data-ttu-id="6752a-170">Değişkenler</span><span class="sxs-lookup"><span data-stu-id="6752a-170">Variables</span></span>                                 | <span data-ttu-id="6752a-171">Değer</span><span class="sxs-lookup"><span data-stu-id="6752a-171">Value</span></span>  |
|-------------------------------------------|---|
| <span data-ttu-id="6752a-172">#define NX_SNMP_TRAP_COLDSTART</span><span class="sxs-lookup"><span data-stu-id="6752a-172">#define NX_SNMP_TRAP_COLDSTART</span></span>            | <span data-ttu-id="6752a-173">0</span><span class="sxs-lookup"><span data-stu-id="6752a-173">0</span></span> |
| <span data-ttu-id="6752a-174">#define NX_SNMP_TRAP_WARMSTART</span><span class="sxs-lookup"><span data-stu-id="6752a-174">#define NX_SNMP_TRAP_WARMSTART</span></span>            | <span data-ttu-id="6752a-175">1</span><span class="sxs-lookup"><span data-stu-id="6752a-175">1</span></span> |
| <span data-ttu-id="6752a-176">#define NX_SNMP_TRAP_LINKDOWN</span><span class="sxs-lookup"><span data-stu-id="6752a-176">#define NX_SNMP_TRAP_LINKDOWN</span></span>             | <span data-ttu-id="6752a-177">2</span><span class="sxs-lookup"><span data-stu-id="6752a-177">2</span></span> |
| <span data-ttu-id="6752a-178">#define NX_SNMP_TRAP_LINKUP</span><span class="sxs-lookup"><span data-stu-id="6752a-178">#define NX_SNMP_TRAP_LINKUP</span></span>               | <span data-ttu-id="6752a-179">3</span><span class="sxs-lookup"><span data-stu-id="6752a-179">3</span></span> |
| <span data-ttu-id="6752a-180">#define NX_SNMP_TRAP_AUTHENTICATE_FAILURE</span><span class="sxs-lookup"><span data-stu-id="6752a-180">#define NX_SNMP_TRAP_AUTHENTICATE_FAILURE</span></span> | <span data-ttu-id="6752a-181">4</span><span class="sxs-lookup"><span data-stu-id="6752a-181">4</span></span> |
| <span data-ttu-id="6752a-182">#define NX_SNMP_TRAP_EGPNEIGHBORLOSS</span><span class="sxs-lookup"><span data-stu-id="6752a-182">#define NX_SNMP_TRAP_EGPNEIGHBORLOSS</span></span>      | <span data-ttu-id="6752a-183">5</span><span class="sxs-lookup"><span data-stu-id="6752a-183">5</span></span> |
| <span data-ttu-id="6752a-184">#define NX_SNMP_TRAP_ENTERPRISESPECIFIC</span><span class="sxs-lookup"><span data-stu-id="6752a-184">#define NX_SNMP_TRAP_ENTERPRISESPECIFIC</span></span>   | <span data-ttu-id="6752a-185">6</span><span class="sxs-lookup"><span data-stu-id="6752a-185">6</span></span> |

<span data-ttu-id="6752a-186">Bu değişkenleri tuzak iletisine eklemek için, *nx_snmp_agent_trapv2_send* (SNMPv2) veya *nx_snmp_agent_trapv3_send* (SNMPv3) içindeki trap_type giriş bağımsız değişkeni bu değişkenlerin numaralandırılmış değerine ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="6752a-186">To include these variables in the trap message, the trap_type input argument in *nx_snmp_agent_trapv2_send* (SNMPv2) or *nx_snmp_agent_trapv3_send* (SNMPv3) is set to the enumerated value of these variables.</span></span> <span data-ttu-id="6752a-187">Aşağıdaki bir örnek, bir soğuk başlatma olayının SNMP yöneticisini bilgilendirmek için aşağıda gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="6752a-187">An example is shown below for SNMPv2 to notify the SNMP Manager of a cold start event:</span></span>

```c
UINT trap_type = NX_SNMP_TRAP_COLDSTART;

status = nx_snmp_agent_trapv2_send(&my_agent, MIB_IP_ADDRESS,
                                  (UCHAR *)"public", trap_type,
                                  tx_time_get(), NX_NULL);

```

<span data-ttu-id="6752a-188">Tuzak iletisine özel değişkenler eklemek için trap_type giriş bağımsız değişkeni NX_SNMP_TRAP_CUSTOM olarak ayarlanır ve tuzak listesi giriş bağımsız değişkeni özel verileri içerir.</span><span class="sxs-lookup"><span data-stu-id="6752a-188">To include proprietary variables in the trap message, the trap_type input argument is set to NX_SNMP_TRAP_CUSTOM and the trap list input argument contains the proprietary data.</span></span> <span data-ttu-id="6752a-189">Tuzak iletisinin sistem zamanı (1.3.6.1.6.3.1.1.4.1.0) olarak içereceği unutulmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="6752a-189">Note that the trap message will contain as the system up time (1.3.6.1.6.3.1.1.4.1.0).</span></span> <span data-ttu-id="6752a-190">SNMPv2 için aşağıda bir örnek gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="6752a-190">An example is shown below for SNMPv2:</span></span>

```c
NX_SNMP_TRAP_OBJECT trap_list[3];
NX_SNMP_OBJECT_DATA trap_data0;

    /* Load the data into the OBJECT. */
    nx_snmp_object_id_get((void*)"1.3.6.1.4.1.7428.1.3.2.0", &trap_data0);

    /* Update the Trap Object with the object and OID. */
    trap_list[0].nx_snmp_object_string_ptr = (UCHAR *)"1.3.6.1.6.3.1.1.4.0";
    trap_list[0].nx_snmp_object_data  = &trap_data0;

    /* Null terminate the trap list. */
    trap_list[1].nx_snmp_object_string_ptr = NX_NULL;

    status = nx_snmp_agent_trapv2_send(&my_agent, MIB_IP_ADDRESS,
                                      (UCHAR *)"trapduo",
                                      NX_SNMP_TRAP_CUSTOM,
                                      tx_time_get(), trap_list);
```

## <a name="netx-duo-snmp-authentication-and-encryption"></a><span data-ttu-id="6752a-191">NetX Duo SNMP kimlik doğrulaması ve şifreleme</span><span class="sxs-lookup"><span data-stu-id="6752a-191">NetX Duo SNMP Authentication and Encryption</span></span>

<span data-ttu-id="6752a-192">*Temel* ve *Özet* gibi iki kimlik doğrulama özelliği vardır.</span><span class="sxs-lookup"><span data-stu-id="6752a-192">There are two flavors of authentication, namely *basic* and *digest*.</span></span> <span data-ttu-id="6752a-193">Temel kimlik doğrulaması, birçok protokolde bulunan basit bir düz metin *Kullanıcı adı* kimlik doğrulamasına eşdeğerdir.</span><span class="sxs-lookup"><span data-stu-id="6752a-193">Basic authentication is equivalent to a simple plain text *username* authentication found in many protocols.</span></span> <span data-ttu-id="6752a-194">SNMP temel kimlik doğrulamasında, Kullanıcı yalnızca sağlanan kullanıcı adının SNMP işlemlerini gerçekleştirmek için geçerli olduğunu doğrular.</span><span class="sxs-lookup"><span data-stu-id="6752a-194">In SNMP basic authentication, the user simply verifies that the supplied username is valid for performing SNMP operations.</span></span> <span data-ttu-id="6752a-195">Temel kimlik doğrulaması, 1 ve 2. SNMP sürümleri için tek seçenektir.</span><span class="sxs-lookup"><span data-stu-id="6752a-195">Basic authentication is the only option for SNMP versions 1 and 2.</span></span>

<span data-ttu-id="6752a-196">Temel kimlik doğrulamasının ana dezavantajı, Kullanıcı adı düz metin olarak iletilir.</span><span class="sxs-lookup"><span data-stu-id="6752a-196">The main disadvantage of basic authentication is the username is transmitted in plain text.</span></span> <span data-ttu-id="6752a-197">SNMPv3 Özet kimlik doğrulaması, Kullanıcı adını hiçbir şekilde düz metin halinde ileterek bu sorunu giderir.</span><span class="sxs-lookup"><span data-stu-id="6752a-197">The SNMPv3 digest authentication addresses this problem by never transmitting the username in plain text.</span></span> <span data-ttu-id="6752a-198">Bunun yerine, Kullanıcı adı, bağlam altyapısı ve diğer bilgilerden 96 bitlik bir ' Digest ' türetmek için bir algoritma kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6752a-198">Instead, an algorithm is used to derive a 96-bit ‘digest’ from the username, context engine, and other information.</span></span> <span data-ttu-id="6752a-199">NetX Duo SNMP Aracısı hem MD5 hem de SHA Özet algoritmalarını destekler.</span><span class="sxs-lookup"><span data-stu-id="6752a-199">The NetX Duo SNMP Agent supports both MD5 and SHA digest algorithms.</span></span>

<span data-ttu-id="6752a-200">Kimlik doğrulamasını etkinleştirmek için SNMP aracısının, *nx_snmp_agent_context_engine_set* hizmetini kullanarak kendi bağlam motoru kimliğini ayarlaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="6752a-200">To enable authentication, the SNMP Agent must set its Context Engine ID using the *nx_snmp_agent_context_engine_set* service.</span></span> <span data-ttu-id="6752a-201">Bağlam altyapısı KIMLIĞI, kimlik doğrulama anahtarı oluşturulurken kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6752a-201">The Context Engine ID is used in the creation of the authentication key.</span></span>

<span data-ttu-id="6752a-202">SNMPv3 veri şifrelemesi DES algoritması kullanılarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="6752a-202">Encryption of SNMPv3 data is available using the DES algorithm.</span></span> <span data-ttu-id="6752a-203">Şifreleme, kimlik doğrulamasının etkinleştirilmesini gerektirir (bir tane, kimlik doğrulama parametreleri ayarlamadan verileri şifreleyemez).</span><span class="sxs-lookup"><span data-stu-id="6752a-203">Encryption requires that authentication be enabled (one cannot encrypt data without setting the authentication parameters).</span></span>

<span data-ttu-id="6752a-204">Kimlik doğrulaması ve gizlilik anahtarları oluşturmak için aşağıdaki API kullanılır:</span><span class="sxs-lookup"><span data-stu-id="6752a-204">To create authentication and privacy keys, the following API are used:</span></span>

```c
UINT  _nx_snmp_agent_md5_key_create(NX_SNMP_AGENT *agent_ptr,
                                    UCHAR *password, NX_SNMP_SECURITY_KEY
                                   *destination_key)

UINT  _nx_snmp_agent_sha_key_create(NX_SNMP_AGENT *agent_ptr,
                                    UCHAR *password, NX_SNMP_SECURITY_KEY
                                   *destination_key)
```

<span data-ttu-id="6752a-205">Daha sonra, SNMP aracısının bu anahtarları kullanacak şekilde yapılandırılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="6752a-205">Next, the SNMP agent must be configured to use these keys.</span></span> <span data-ttu-id="6752a-206">SNMP aracısıyla bir anahtar kaydetmek için aşağıdaki API kullanılır:</span><span class="sxs-lookup"><span data-stu-id="6752a-206">To register a key with the SNMP agent, the following API are used:</span></span>

```c
UINT  _nx_snmp_agent_authenticate_key_use(NX_SNMP_AGENT *agent_ptr,
                                          NX_SNMP_SECURITY_KEY *key)

UINT  _nx_snmp_agent_privacy_key_use(NX_SNMP_AGENT *agent_ptr,
                                    NX_SNMP_SECURITY_KEY *key)
```

<span data-ttu-id="6752a-207">Tuzak iletileri için ayrı anahtarlar oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="6752a-207">Separate keys can be created for trap messages.</span></span> <span data-ttu-id="6752a-208">Tuzak iletileri için anahtar uygulamak için aşağıdaki API kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="6752a-208">To apply keys for trap messages the following API are available:</span></span>

```c
UINT  _nx_snmp_agent_auth_trap_key_use(NX_SNMP_AGENT *agent_ptr,
                                       NX_SNMP_SECURITY_KEY *key)

UINT  _nx_snmp_agent_priv_trap_key_use(NX_SNMP_AGENT *agent_ptr,
                                       NX_SNMP_SECURITY_KEY *key)
```

<span data-ttu-id="6752a-209">Yanıt iletileri ve tuzak göndermek için kimlik doğrulama veya şifrelemeyi devre dışı bırakmak için bu hizmetleri anahtar işaretçisi girişi NULL olarak ayarlanmış şekilde kullanın.</span><span class="sxs-lookup"><span data-stu-id="6752a-209">To disable authentication or encryption for response messages and sending traps, use these services with the key pointer input set to NULL.</span></span>

## <a name="netx-duo-snmp-community-strings"></a><span data-ttu-id="6752a-210">NetX Duo SNMP topluluk dizeleri</span><span class="sxs-lookup"><span data-stu-id="6752a-210">NetX Duo SNMP Community Strings</span></span>

<span data-ttu-id="6752a-211">NetX Duo SNMP Aracısı hem ortak hem de özel topluluk dizelerini destekler.</span><span class="sxs-lookup"><span data-stu-id="6752a-211">The NetX Duo SNMP Agent supports both public and private community strings.</span></span> <span data-ttu-id="6752a-212">Ortak dize, *nx_snmp_agent _public_string_set* hizmeti ile ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="6752a-212">The public string is set with the *nx_snmp_agent _public_string_set* service.</span></span> <span data-ttu-id="6752a-213">NetX Duo SNMP Aracısı özel dizesi *nx_snmp_agent_private_string_set* hizmeti kullanılarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="6752a-213">The NetX Duo SNMP Agent private string is set using the *nx_snmp_agent_private_string_set* service.</span></span>

## <a name="netx-duo-snmp-username-callback"></a><span data-ttu-id="6752a-214">NetX Duo SNMP Kullanıcı adı geri araması</span><span class="sxs-lookup"><span data-stu-id="6752a-214">NetX Duo SNMP Username Callback</span></span>

<span data-ttu-id="6752a-215">NetX Duo SNMP aracı paketi, uygulamanın, her SNMP Istemci isteğinin başlangıcında çağrılan bir Kullanıcı adı geri çağırması belirtmesini ( ***nx_snmp_agent_create*** çağrısı aracılığıyla) sağlar.</span><span class="sxs-lookup"><span data-stu-id="6752a-215">The NetX Duo SNMP Agent package allows the application to specify (via the ***nx_snmp_agent_create*** call) a username callback  that is called at the beginning of handling each SNMP Client request.</span></span>

<span data-ttu-id="6752a-216">Geri arama yordamı, NetX Duo SNMP aracısını Kullanıcı adıyla sağlar.</span><span class="sxs-lookup"><span data-stu-id="6752a-216">The callback routine provides the NetX Duo SNMP Agent with the username.</span></span> <span data-ttu-id="6752a-217">Sağlanan Kullanıcı adı geçerliyse veya isteğe yanıt vermek için Kullanıcı adı denetimi gerekli değilse, Kullanıcı adı geri çağırması **NX_SUCCESS** değerini döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="6752a-217">If the supplied username is valid or if no username check is necessary for the responding to the request, the username callback should return the value of **NX_SUCCESS**.</span></span> <span data-ttu-id="6752a-218">Aksi halde, belirtilen kullanıcı adının geçersiz olduğunu göstermek için yordam **NX_SNMP_ERROR** döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="6752a-218">Otherwise, the routine should return **NX_SNMP_ERROR** to indicate the specified username is invalid.</span></span>

<span data-ttu-id="6752a-219">Uygulama Kullanıcı adı geri çağırma yordamının biçimi aşağıda tanımlanmıştır:</span><span class="sxs-lookup"><span data-stu-id="6752a-219">The format of the application username callback routine is defined below:</span></span>

```c
UINT nx_snmp_agent_username_process(NX_SNMP_AGENT *agent_ptr,
                                    UCHAR *username);
```

<span data-ttu-id="6752a-220">Giriş parametreleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="6752a-220">The input parameters are defined as follows:</span></span>

| <span data-ttu-id="6752a-221">Parametre</span><span class="sxs-lookup"><span data-stu-id="6752a-221">Parameter</span></span> | <span data-ttu-id="6752a-222">Anlamı</span><span class="sxs-lookup"><span data-stu-id="6752a-222">Meaning</span></span>                                              |
|-----------|------------------------------------------------------|
| <span data-ttu-id="6752a-223">*agent_ptr*</span><span class="sxs-lookup"><span data-stu-id="6752a-223">*agent_ptr*</span></span> | <span data-ttu-id="6752a-224">SNMP Aracısı çağırma işaretçisi</span><span class="sxs-lookup"><span data-stu-id="6752a-224">Pointer to calling SNMP agent</span></span>                        |
| <span data-ttu-id="6752a-225">username</span><span class="sxs-lookup"><span data-stu-id="6752a-225">username</span></span>  | <span data-ttu-id="6752a-226">Gerekli Kullanıcı adına işaretçinin hedefi</span><span class="sxs-lookup"><span data-stu-id="6752a-226">Destination for the pointer to the required username</span></span> |

<span data-ttu-id="6752a-227">SNMPv1 ve SNMPv2/v2C oturumları için, uygulama, SNMP isteğinin geçerli bir topluluk dizesine sahip olup olmadığını anlamak üzere gelen bir SNMP isteğindeki topluluk dizesini incelemek ister.</span><span class="sxs-lookup"><span data-stu-id="6752a-227">For SNMPv1 and SNMPv2/v2C sessions, the application will want to examine the community string on an incoming SNMP request to determine if the SNMP request has a valid community string.</span></span> <span data-ttu-id="6752a-228">SNMP uygulamasının bunu yapması için çeşitli hizmetler vardır.</span><span class="sxs-lookup"><span data-stu-id="6752a-228">There are several services for the SNMP application to do this.</span></span>

<span data-ttu-id="6752a-229">SNMP uygulaması, geçerli SNMP Yöneticisi isteğinin bir GET (örn. GET, GETNEXT veya GETBULK) olduğunu veya bu hizmeti kullanarak istek türünü AYARLAMANıZı sağlayabilir:</span><span class="sxs-lookup"><span data-stu-id="6752a-229">The SNMP application can inquire if the current SNMP Manager request is a GET (e.g. GET, GETNEXT, or GETBULK) or SET type of request using this service:</span></span>

```c
UINT nx_snmp_agent_request_get_type_test(NX_SNMP_AGENT *agent_ptr,
                                         UINT *is_get_type);
```

<span data-ttu-id="6752a-230">İstek bir GET türüdür, uygulama, giriş topluluğu dizesini SNMP aracısının ortak dizesiyle karşılaştırmak ister:</span><span class="sxs-lookup"><span data-stu-id="6752a-230">If the request is a GET type, the application will want to compare the input community string to the SNMP Agent’s public string:</span></span>

```c
UINT nx_snmp_agent_public_string_test(NX_SNMP_AGENT *agent_ptr,
                                      UCHAR *username,
                                      UINT *is_public);
```

<span data-ttu-id="6752a-231">Benzer şekilde, istek bir küme türü ise, uygulama, giriş topluluğu dizesini SNMP aracısının özel dizesiyle karşılaştırmak ister:</span><span class="sxs-lookup"><span data-stu-id="6752a-231">Similarly if the request is a SET type, the application will want to compare the input community string to the SNMP Agent’s private string:</span></span>

```c
UINT nx_snmp_agent_private_string_test(NX_SNMP_AGENT *agent_ptr,
                                       UCHAR *username,
                                       UINT *is_private);
```

<span data-ttu-id="6752a-232">İs_public ve is_private dönüş değerleri, giriş topluluk dizesi geçerli bir genel veya özel topluluk dizesi ise sırasıyla gösterir.</span><span class="sxs-lookup"><span data-stu-id="6752a-232">The is_public and is_private return values indicate respectively if the input community string is a valid public or private community string.</span></span>

<span data-ttu-id="6752a-233">Kullanıcı adı geri çağırma yordamının dönüş değeri, Kullanıcı adının geçerli olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="6752a-233">The return value of the username callback routine indicates if the username is valid.</span></span> <span data-ttu-id="6752a-234">**NX_SUCCESS** değeri, Kullanıcı adı geçerliyse veya Kullanıcı adı geçersiz ise **NX_SNMP_ERROR** döndürülür.</span><span class="sxs-lookup"><span data-stu-id="6752a-234">The value **NX_SUCCESS** is returned if the username is valid, or **NX_SNMP_ERROR** if the username is invalid.</span></span>

## <a name="netx-duo-snmp-agent-get-callback"></a><span data-ttu-id="6752a-235">NetX Duo SNMP Aracısı geri arama al</span><span class="sxs-lookup"><span data-stu-id="6752a-235">NetX Duo SNMP Agent GET Callback</span></span>

<span data-ttu-id="6752a-236">Uygulamanın, SNMP yöneticisinden nesne al isteklerini işlemek için bir geri çağırma yordamı ayarlaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="6752a-236">The application must set a callback routine for handling GET object requests from the SNMP Manager.</span></span> <span data-ttu-id="6752a-237">Geri çağırma istekte belirtilen nesnenin değerini alır.</span><span class="sxs-lookup"><span data-stu-id="6752a-237">The callback retrieves the value of the object specified in the request.</span></span>

<span data-ttu-id="6752a-238">Uygulama GET isteği geri arama yordamı aşağıda tanımlanmıştır:</span><span class="sxs-lookup"><span data-stu-id="6752a-238">The application GET request callback routine is defined below:</span></span>

```c
UINT nx_snmp_agent_get_process(NX_SNMP_AGENT *agent_ptr,
                               UCHAR *object_requested,
                               NX_SNMP_OBJECT_DATA *object_data);
```

<span data-ttu-id="6752a-239">Giriş parametreleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="6752a-239">The input parameters are defined as follows:</span></span>

| <span data-ttu-id="6752a-240">Parametre</span><span class="sxs-lookup"><span data-stu-id="6752a-240">Parameter</span></span>        | <span data-ttu-id="6752a-241">Anlamı</span><span class="sxs-lookup"><span data-stu-id="6752a-241">Meaning</span></span> |
|------------------|----------------------------------|
| <span data-ttu-id="6752a-242">*agent_ptr*</span><span class="sxs-lookup"><span data-stu-id="6752a-242">*agent_ptr*</span></span>        | <span data-ttu-id="6752a-243">SNMP Aracısı çağırma işaretçisi</span><span class="sxs-lookup"><span data-stu-id="6752a-243">Pointer to calling SNMP agent</span></span> |
| <span data-ttu-id="6752a-244">object_requested</span><span class="sxs-lookup"><span data-stu-id="6752a-244">object_requested</span></span> | <span data-ttu-id="6752a-245">GET işleminin için olduğu nesne KIMLIĞINI temsil eden ASCII dizesi.</span><span class="sxs-lookup"><span data-stu-id="6752a-245">ASCII string representing the object ID the GET operation is for.</span></span> |
| <span data-ttu-id="6752a-246">object_data</span><span class="sxs-lookup"><span data-stu-id="6752a-246">object_data</span></span>      | <span data-ttu-id="6752a-247">Geri çağırma tarafından alınan değeri tutacak veri yapısı.</span><span class="sxs-lookup"><span data-stu-id="6752a-247">Data structure to hold the value retrieved by the callback.</span></span> <span data-ttu-id="6752a-248">Bu, aşağıda açıklanan bir dizi NetX Duo SNMP API 'SI ile ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="6752a-248">This can be set with a series of NetX Duo SNMP API’s described below.</span></span> |

> [!NOTE]
> <span data-ttu-id="6752a-249">*Sekizli dizeler için, nesnenin uzunluğu atanmalıdır; böylece iç işlev, geri aramanın bir length bağımsız değişkenine sahip olmadığı için uzunluğu ne kadar süreyle olduğunu bilir:*</span><span class="sxs-lookup"><span data-stu-id="6752a-249">*For octet strings, the object must be assigned the length so that the internal function knows how long the length is since the callback itself does not have a length argument:*</span></span>

```c
object_data -> nx_snmp_object_octet_string_size = mib2_mib[i].length;
```

<span data-ttu-id="6752a-250">Veri türü GET geri çağırması tarafından bilinmediğinden, veri türünü denetlemeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="6752a-250">Since the type of data is not known to the GET callback, there is no need to check the data type.</span></span> <span data-ttu-id="6752a-251">Uzunluk, boş ayrılmış sayısal türler veya dizeler üzerinde herhangi bir etkiye sahip olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="6752a-251">Length will not have any effect on numeric types or strings which are null delimited.</span></span>

<span data-ttu-id="6752a-252">Ardından iç işlevi çağırın:</span><span class="sxs-lookup"><span data-stu-id="6752a-252">Then call the internal function:</span></span>

```c
status = mib2_mib[i].object_get_callback)
                   (mib2_mib[i].object_value_ptr, object_data);
```

<span data-ttu-id="6752a-253">Geri çağırma işlevi istenen nesneyi bulamazsa, **NX_SNMP_ERROR_NOSUCHNAME** hata kodu döndürülmelidir.</span><span class="sxs-lookup"><span data-stu-id="6752a-253">If the callback function cannot find the requested object, the **NX_SNMP_ERROR_NOSUCHNAME** error code should be returned.</span></span> <span data-ttu-id="6752a-254">Başka bir hata algılanırsa, **NX_SNMP_ERROR** döndürülmelidir.</span><span class="sxs-lookup"><span data-stu-id="6752a-254">If any other error is detected, the **NX_SNMP_ERROR** should be returned.</span></span>

## <a name="netx-duo-snmp-agent-getnext-callback"></a><span data-ttu-id="6752a-255">NetX Duo SNMP Aracısı GETNEXT geri çağırma</span><span class="sxs-lookup"><span data-stu-id="6752a-255">NetX Duo SNMP Agent GETNEXT Callback</span></span>

<span data-ttu-id="6752a-256">Uygulamanın, SNMP yöneticisinden GETNEXT nesne istekleri için geri çağırma yordamını da ayarlaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="6752a-256">The application must also set the callback routine for GETNEXT object requests from the SNMP Manager.</span></span> <span data-ttu-id="6752a-257">GETNEXT geri çağırması, istek tarafından belirtilen sonraki nesnenin değerini alır.</span><span class="sxs-lookup"><span data-stu-id="6752a-257">The GETNEXT callback retrieves the value of the next object specified by the request.</span></span>

<span data-ttu-id="6752a-258">Application GETNEXT istek geri çağırma yordamı aşağıda tanımlanmıştır:</span><span class="sxs-lookup"><span data-stu-id="6752a-258">The application GETNEXT request callback routine is defined below:</span></span>

```c
UINT nx_snmp_agent_getnext_process(NX_SNMP_AGENT *agent_ptr,
                                   UCHAR *object_requested,
                                   NX_SNMP_OBJECT_DATA *object_data);
```

<span data-ttu-id="6752a-259">Giriş parametreleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="6752a-259">The input parameters are defined as follows:</span></span>

| <span data-ttu-id="6752a-260">Parametre</span><span class="sxs-lookup"><span data-stu-id="6752a-260">Parameter</span></span>        | <span data-ttu-id="6752a-261">Anlamı</span><span class="sxs-lookup"><span data-stu-id="6752a-261">Meaning</span></span> |
|------------------|-------------------------------------------|
| <span data-ttu-id="6752a-262">*agent_ptr*</span><span class="sxs-lookup"><span data-stu-id="6752a-262">*agent_ptr*</span></span>        | <span data-ttu-id="6752a-263">SNMP Aracısı çağırma işaretçisi</span><span class="sxs-lookup"><span data-stu-id="6752a-263">Pointer to calling SNMP agent</span></span> |
| <span data-ttu-id="6752a-264">object_requested</span><span class="sxs-lookup"><span data-stu-id="6752a-264">object_requested</span></span> | <span data-ttu-id="6752a-265">GETNEXT işleminin için olduğu nesne KIMLIĞINI temsil eden ASCII dizesi.</span><span class="sxs-lookup"><span data-stu-id="6752a-265">ASCII string representing the object ID the GETNEXT operation is for.</span></span> |
| <span data-ttu-id="6752a-266">object_data</span><span class="sxs-lookup"><span data-stu-id="6752a-266">object_data</span></span>      | <span data-ttu-id="6752a-267">Geri çağırma tarafından alınan değeri tutacak veri yapısı.</span><span class="sxs-lookup"><span data-stu-id="6752a-267">Data structure to hold the value retrieved by the callback.</span></span> <span data-ttu-id="6752a-268">Bu, aşağıda açıklanan bir dizi NetX Duo SNMP API 'SI ile ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="6752a-268">This can be set with a series of NetX Duo SNMP API’s described below.</span></span> |

<span data-ttu-id="6752a-269">Geri çağırmalar için aynı ile aynı, iç işlevin uzunluğunun length bir bağımsız değişkeni olmadığından, dizenin ne kadar süreyle olduğunu bilmesi için, sekizli dize verilerine sahip nesneler uzunluğa atanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6752a-269">Same as is true for GET callbacks, objects with octet string data must be assigned the length so that the internal function knows how long the length is since the callback itself does not have a length argument:</span></span>

```c
object_data -> nx_snmp_object_octet_string_size = mib2_mib[i].length;
```

<span data-ttu-id="6752a-270">Veri türü GET geri çağırması tarafından bilinmediğinden, veri türünü denetlemeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="6752a-270">Since the type of data is not known to the GET callback, there is no need to check the data type.</span></span> <span data-ttu-id="6752a-271">Uzunluk, boş ayrılmış sayısal türler veya dizeler üzerinde herhangi bir etkiye sahip olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="6752a-271">Length will not have any effect on numeric types or strings which are null delimited.</span></span>

<span data-ttu-id="6752a-272">Ardından iç işlevi çağırın:</span><span class="sxs-lookup"><span data-stu-id="6752a-272">Then call the internal function:</span></span>

```c
status = mib2_mib[i].object_get_callback)
                   (mib2_mib[i].object_value_ptr, object_data);
```

<span data-ttu-id="6752a-273">Geri çağırma işlevi istenen nesneyi bulamazsa, **NX_SNMP_ERROR_NOSUCHNAME** hata kodu döndürülmelidir.</span><span class="sxs-lookup"><span data-stu-id="6752a-273">If the callback function cannot find the requested object, the **NX_SNMP_ERROR_NOSUCHNAME** error code should be returned.</span></span> <span data-ttu-id="6752a-274">Başka bir hata algılanırsa, **NX_SNMP_ERROR** döndürülmelidir.</span><span class="sxs-lookup"><span data-stu-id="6752a-274">If any other error is detected, the **NX_SNMP_ERROR** should be returned.</span></span>

## <a name="netx-duo-snmp-agent-set-callback"></a><span data-ttu-id="6752a-275">NetX Duo SNMP Aracısı KÜMESI geri araması</span><span class="sxs-lookup"><span data-stu-id="6752a-275">NetX Duo SNMP Agent SET Callback</span></span>

<span data-ttu-id="6752a-276">Uygulama, SNMP yöneticisinden SET nesne isteklerini işlemek için geri çağırma yordamını ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6752a-276">The application should set the callback routine for handling SET object requests from the SNMP Manager.</span></span> <span data-ttu-id="6752a-277">SET callback, istek tarafından belirtilen nesnenin değerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="6752a-277">The SET callback sets the value of the object specified by the request.</span></span>

<span data-ttu-id="6752a-278">Uygulama KÜMESI isteği geri arama yordamı aşağıda tanımlanmıştır:</span><span class="sxs-lookup"><span data-stu-id="6752a-278">The application SET request callback routine is defined below:</span></span>

```c
UINT nx_snmp_agent_set_process(NX_SNMP_AGENT *agent_ptr,
                               UCHAR *object_requested,
                               NX_SNMP_OBJECT_DATA *object_data);
```

<span data-ttu-id="6752a-279">Giriş parametreleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="6752a-279">The input parameters are defined as follows:</span></span>

| <span data-ttu-id="6752a-280">Parametre</span><span class="sxs-lookup"><span data-stu-id="6752a-280">Parameter</span></span>        | <span data-ttu-id="6752a-281">Anlamı</span><span class="sxs-lookup"><span data-stu-id="6752a-281">Meaning</span></span> |
|------------------|-------- |
| <span data-ttu-id="6752a-282">*agent_ptr*</span><span class="sxs-lookup"><span data-stu-id="6752a-282">*agent_ptr*</span></span>      | <span data-ttu-id="6752a-283">SNMP Aracısı çağırma işaretçisi</span><span class="sxs-lookup"><span data-stu-id="6752a-283">Pointer to calling SNMP agent</span></span> |
| <span data-ttu-id="6752a-284">object_requested</span><span class="sxs-lookup"><span data-stu-id="6752a-284">object_requested</span></span> | <span data-ttu-id="6752a-285">KÜME işleminin için olduğu nesne KIMLIĞINI temsil eden ASCII dizesi.</span><span class="sxs-lookup"><span data-stu-id="6752a-285">ASCII string representing the object ID the SET operation is for.</span></span> |
| <span data-ttu-id="6752a-286">object_data</span><span class="sxs-lookup"><span data-stu-id="6752a-286">object_data</span></span>      | <span data-ttu-id="6752a-287">Belirtilen nesne için yeni değeri içeren veri yapısı.</span><span class="sxs-lookup"><span data-stu-id="6752a-287">Data structure that contains the new value for the specified object.</span></span> <span data-ttu-id="6752a-288">Gerçek işlem, aşağıda açıklanan NetX Duo SNMP API 'SI kullanılarak yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="6752a-288">The actual operation can be done using the NetX Duo SNMP API’s described below.</span></span> |

<span data-ttu-id="6752a-289">Sekizli dizeler için, küme geri çağrısının, SNMP Aracısı verileri ayrıştırdığından ve türü ve uzunluğu öğrendiğinden, MıB tablosunu verilerin uzunluğuyla güncelleştirmesi gerektiğini unutmayın:</span><span class="sxs-lookup"><span data-stu-id="6752a-289">Note that for octet strings, the SET callback should update the MIB table with the length of the data since the SNMP Agent has parsed the data and knows the type and length:</span></span>

```c
if (object_data -> nx_snmp_object_data_type ==
                           NX_SNMP_ANS1_OCTET_STRING)
{
    mib2_mib[i].length =
        object_data -> nx_snmp_object_octet_string_size;
}

object_data -> nx_snmp_object_octet_string_size =
                                 mib2_mib[i].length;
```

<span data-ttu-id="6752a-290">Geri çağırma işlevi istenen nesneyi bulamazsa, **NX_SNMP_ERROR_NOSUCHNAME** hata kodu döndürülmelidir.</span><span class="sxs-lookup"><span data-stu-id="6752a-290">If the callback function cannot find the requested object, the **NX_SNMP_ERROR_NOSUCHNAME** error code should be returned.</span></span>

<span data-ttu-id="6752a-291">NetX Duo SNMP ana bilgisayarı özel topluluk dizeleri oluşturup, küme isteğinin SNMP göndericisi eşleşen özel dizeye sahip değilse, bir **NX_SNMP_ERROR_NOACCESS** hatası döndürebilir.</span><span class="sxs-lookup"><span data-stu-id="6752a-291">If the NetX Duo SNMP host has created private community strings, and the SNMP sender of the SET request does not have the matching private string, it may return an **NX_SNMP_ERROR_NOACCESS** error.</span></span> <span data-ttu-id="6752a-292">Başka bir hata algılanırsa, **NX_SNMP_ERROR** döndürülmelidir.</span><span class="sxs-lookup"><span data-stu-id="6752a-292">If any other error is detected, the **NX_SNMP_ERROR** should be returned.</span></span>

> [!NOTE]
> <span data-ttu-id="6752a-293">*NetX Duo SNMP Aracısı, dağıtıma sahip bir SNMP MıB veritabanı sağlamasına rağmen öncelikli olarak test ve geliştirme amaçlıdır. Geliştirici, büyük olasılıkla profesyonel SNMP uygulaması için özel bir MıB veritabanı gerektirir.*</span><span class="sxs-lookup"><span data-stu-id="6752a-293">*Although NetX Duo SNMP Agent supplies an SNMP MIB database with the distribution, it is primarily for testing and development purposes. The developer will likely require a proprietary MIB database for a professional SNMP application.*</span></span>

## <a name="changing-snmp-version-at-run-time"></a><span data-ttu-id="6752a-294">Çalışma zamanında SNMP sürümünü değiştirme</span><span class="sxs-lookup"><span data-stu-id="6752a-294">Changing SNMP Version at Run Time</span></span>

<span data-ttu-id="6752a-295">SNMP Aracısı ana makinesi, *nx_snmp_agent_set_version* hizmetini kullanarak, çalışma zamanında üç sürümün her bırı için SNMP sürümünü değiştirebilir.</span><span class="sxs-lookup"><span data-stu-id="6752a-295">The SNMP Agent host can change SNMP version for each of the three versions at run time using the *nx_snmp_agent_set_version* service.</span></span> <span data-ttu-id="6752a-296">SNMP Aracısı, *NX_SNMP_AGENT_CREATE* SNMP Aracısı oluşturulduğunda varsayılan olarak üç sürüm için etkinleştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="6752a-296">The SNMP Agent is by default enabled for all three versions when the SNMP Agent is created in *nx_snmp_agent_create*.</span></span> <span data-ttu-id="6752a-297">Ancak, uygulama bunu tüm sürümlerin bir alt kümesiyle sınırlayabilir.</span><span class="sxs-lookup"><span data-stu-id="6752a-297">However, the application can limit that to a subset of all versions.</span></span>

> [!NOTE]
> <span data-ttu-id="6752a-298">*NX_SNMP_DISABLE_V1, NX_SNMP_DISABLE_V2 ve/veya NX_SNMP_DISABLE_V3 yapılandırma seçenekleri tanımlıysa, bu işlevin etkilenen sürümlerin etkinleştirilmesiyle hiçbir etkisi olmayacaktır.*</span><span class="sxs-lookup"><span data-stu-id="6752a-298">*If the configuration options NX_SNMP_DISABLE_V1, NX_SNMP_DISABLE_V2 and/or NX_SNMP_DISABLE_V3 are defined, this function will have no effect enabling the effected versions.*</span></span>

<span data-ttu-id="6752a-299">SNMP Aracısı, *nx_snmp_agent_get_current_version* hizmeti kullanılarak alınan en son SNMP paketinin SNMP sürümünü alabilir.</span><span class="sxs-lookup"><span data-stu-id="6752a-299">The SNMP Agent can retrieve the SNMP version of the latest SNMP packet received using the *nx_snmp_agent_get_current_version* service.</span></span>

## <a name="snmpv3-discovery"></a><span data-ttu-id="6752a-300">SNMPv3 bulma</span><span class="sxs-lookup"><span data-stu-id="6752a-300">SNMPv3 Discovery</span></span>

<span data-ttu-id="6752a-301">SNMPv3 için etkinleştirildiyse SNMP Aracısı, SNMP yöneticisinden bulma isteklerine yanıt verir.</span><span class="sxs-lookup"><span data-stu-id="6752a-301">The SNMP Agent, if enabled for SNMPv3, will respond to discovery requests from the SNMP Manager.</span></span> <span data-ttu-id="6752a-302">Bu tür bir istek, yetkili altyapı KIMLIĞI, Kullanıcı adı, önyükleme sayısı ve önyükleme süresi için null değerleri olan güvenlik parametresi verileri içerir.</span><span class="sxs-lookup"><span data-stu-id="6752a-302">Such a request contains security parameter data with null values for Authoritative Engine ID, user name, boot count and boot time.</span></span> <span data-ttu-id="6752a-303">Kimlik doğrulama parametreleri bulma iletisine uygulanmaz.</span><span class="sxs-lookup"><span data-stu-id="6752a-303">Authentication parameters are not applied to the DISCOVERY message.</span></span> <span data-ttu-id="6752a-304">İstekteki değişken bağlama listesi boş (sıfır öğe içeriyor).</span><span class="sxs-lookup"><span data-stu-id="6752a-304">The variable binding list in the request is empty (contains zero items).</span></span> <span data-ttu-id="6752a-305">SNMP Aracısı, sıfır önyükleme süresi ve sayısı ile yanıt verir ve bilinmeyen (null) bir altyapı KIMLIĞIYLE alınan isteklerin sayısı olan 1 item, *Usmstatsunknownengineıds*' ı içeren değişken bağlama listesidir.</span><span class="sxs-lookup"><span data-stu-id="6752a-305">The SNMP agent responds with a zero boot time and count, and the variable binding list containing 1 item, *usmStatsUnknownEngineIDs*, which is the count of requests received with an unknown (null) engine ID.</span></span> <span data-ttu-id="6752a-306">Tarayıcıdan/yöneticisinden sonraki GETNEXT isteğinde, önyükleme verileri ve güvenlik parametreleri yalnızca güvenlik etkinse doldurulur.</span><span class="sxs-lookup"><span data-stu-id="6752a-306">On the subsequent GETNEXT request from the Browser/Manager, the boot data and security parameters are filled in only if security is enabled.</span></span> <span data-ttu-id="6752a-307">Bu durumda, PDU 'da NotInTime veri güncelleştirmesi de gönderilir.</span><span class="sxs-lookup"><span data-stu-id="6752a-307">If so it will also send a NotInTime data update in the PDU.</span></span> <span data-ttu-id="6752a-308">Güvenlik parametreleri, örneğin, kimlik doğrulama aracının yöneticinin kimliğini yöneticiye kanıtlamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="6752a-308">The security parameters, e.g. authentication prove the identity of the Agent to the Manager.</span></span>

<span data-ttu-id="6752a-309">SNMPv3 kimlik doğrulaması hakkında daha ayrıntılı bilgi için, RFC 3414 "basit ağ yönetim protokolü 'nün (SNMPv3) 3. sürümü için Kullanıcı tabanlı güvenlik modelinde (USD) kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="6752a-309">More detailed information on SNMPv3 authentication is available in RFC 3414 “User-based Security Model (USM) for version 3 of the Simple Network Management Protocol (SNMPv3)”.</span></span>

## <a name="netx-duo-snmp-rfcs"></a><span data-ttu-id="6752a-310">NetX Duo SNMP RFC 'Leri</span><span class="sxs-lookup"><span data-stu-id="6752a-310">NetX Duo SNMP RFCs</span></span>

<span data-ttu-id="6752a-311">NetX Duo SNMP, RFC1155, RFC1157, RFC1215, RFC1901, RFC1905, RFC1906, RFC1907, RFC1908, RFC2571, RFC2572, RFC2574, RFC2575, RFC 3414 ve ilgili RFC 'Ler ile uyumludur.</span><span class="sxs-lookup"><span data-stu-id="6752a-311">NetX Duo SNMP is compliant with RFC1155, RFC1157, RFC1215, RFC1901, RFC1905, RFC1906, RFC1907, RFC1908, RFC2571, RFC2572, RFC2574, RFC2575, RFC 3414 and related RFCs.</span></span>
