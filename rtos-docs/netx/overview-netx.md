---
title: Azure RTOS NetX 'i anlama
description: Azure RTOS NetX, Azure RTOS ThreadX ile tam olarak tümleştirilmiş ve desteklenen tüm işlemciler için kullanılabilen TCP/IP protokol standartlarının yüksek performanslı bir uygulamasıdır.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: 7c864c23f019e4841ddb3096fde663c8039baf44
ms.sourcegitcommit: 19d50693d8f5287ba6938ae1d23eef88435ed7b1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/28/2021
ms.locfileid: "108171327"
---
# <a name="overview-of-azure-rtos-netx"></a><span data-ttu-id="5d90c-103">Azure RTOS NetX 'e genel bakış</span><span class="sxs-lookup"><span data-stu-id="5d90c-103">Overview of Azure RTOS NetX</span></span>

<span data-ttu-id="5d90c-104">Azure RTOS NetX, özellikle derin gömülü, gerçek zamanlı ve IoT uygulamaları için tasarlanan bir endüstriyel sınıf TCP/IP IPv4 Embedded ağ yığınıdır.</span><span class="sxs-lookup"><span data-stu-id="5d90c-104">Azure RTOS NetX is an industrial grade TCP/IP IPv4 embedded network stack, designed specifically for deeply embedded, real-time, and IoT applications.</span></span> <span data-ttu-id="5d90c-105">Azure RTOS NetX, Microsoft 'un özgün IPv4 ağ yığınıdır ve aslında Azure RTOS 'ın bir alt kümesidir.</span><span class="sxs-lookup"><span data-stu-id="5d90c-105">Azure RTOS NetX is Microsoft's original IPv4 network stack, and is essentially a subset of Azure RTOS.</span></span> <span data-ttu-id="5d90c-106">NetX, IPv4, TCP ve UDP gibi çekirdek ağ protokollerine ve ek ve daha üst düzey eklenti protokollerinin eksiksiz bir paketine sahip gömülü uygulamalar sağlar.</span><span class="sxs-lookup"><span data-stu-id="5d90c-106">NetX provides embedded applications with core network protocols such as IPv4, TCP, and UDP as well as a complete suite of additional, higher-level add-on protocols.</span></span> <span data-ttu-id="5d90c-107">Küçük bir kaplama, Hızlı yürütme ve üstün kullanım kolaylığı, Azure RTOS NetX 'i en zorlu ekli IoT uygulamaları için ideal bir seçenek haline getirir.</span><span class="sxs-lookup"><span data-stu-id="5d90c-107">A small footprint, fast execution, and superior ease-of-use make Azure RTOS NetX an ideal choice for the most demanding embedded IoT applications.</span></span>

## <a name="api-protocols"></a><span data-ttu-id="5d90c-108">API protokolleri</span><span class="sxs-lookup"><span data-stu-id="5d90c-108">API protocols</span></span>

### <a name="telnet"></a><span data-ttu-id="5d90c-109">Sun</span><span class="sxs-lookup"><span data-stu-id="5d90c-109">TELNET</span></span>

* <span data-ttu-id="5d90c-110">Minimum 0,5 KB ve 0,3 KB RAM parmak izi.</span><span class="sxs-lookup"><span data-stu-id="5d90c-110">Minimal 0.5 KB and 0.3 KB RAM footprint.</span></span>
* <span data-ttu-id="5d90c-111">İstemci ve sunucu desteği.</span><span class="sxs-lookup"><span data-stu-id="5d90c-111">Client and server support.</span></span>

### <a name="auto-ip"></a><span data-ttu-id="5d90c-112">Otomatik IP</span><span class="sxs-lookup"><span data-stu-id="5d90c-112">Auto IP</span></span>

* <span data-ttu-id="5d90c-113">Otomatik IPv4 adresi ataması.</span><span class="sxs-lookup"><span data-stu-id="5d90c-113">Automatic IPv4 address assignment.</span></span>
* <span data-ttu-id="5d90c-114">Minimum 1,2 KB, 300 bayt RAM.</span><span class="sxs-lookup"><span data-stu-id="5d90c-114">Minimal 1.2 KB, 300 bytes of RAM.</span></span>

### <a name="http---hypertext-transfer-protocolhttp"></a><span data-ttu-id="5d90c-115">HTTP-Köprü Metni Aktarım Protokolü (HTTP)</span><span class="sxs-lookup"><span data-stu-id="5d90c-115">HTTP - Hypertext Transfer Protocol(HTTP)</span></span>

* <span data-ttu-id="5d90c-116">En az 2,8 KB-4.8 KBFLASH, 0,4 KB-1,0 KB-RAM ayak izi.</span><span class="sxs-lookup"><span data-stu-id="5d90c-116">Minimal 2.8 KB to 4.8KBFLASH, 0.4 KB to 1.0 KB RAM footprint.</span></span>
* <span data-ttu-id="5d90c-117">İstemci ve sunucu desteği.</span><span class="sxs-lookup"><span data-stu-id="5d90c-117">Client and server support.</span></span>

### <a name="smtp---simple-mail-transfer-protocol-smtp"></a><span data-ttu-id="5d90c-118">SMTP-Basit Posta Aktarım Protokolü (SMTP)</span><span class="sxs-lookup"><span data-stu-id="5d90c-118">SMTP - Simple Mail Transfer Protocol (SMTP)</span></span>

* <span data-ttu-id="5d90c-119">En az 4,1 KB ve 0,6 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="5d90c-119">Minimal 4.1 KB and 0.6 KB RAM footprint</span></span>
* <span data-ttu-id="5d90c-120">İstemci desteği</span><span class="sxs-lookup"><span data-stu-id="5d90c-120">Client support</span></span>

### <a name="dhcp---dynamic-host-configuration-protocol-dhcp"></a><span data-ttu-id="5d90c-121">DHCP-dinamik ana bilgisayar Yapılandırma Protokolü (DHCP)</span><span class="sxs-lookup"><span data-stu-id="5d90c-121">DHCP - Dynamic Host Configuration Protocol (DHCP)</span></span>

* <span data-ttu-id="5d90c-122">Minimum 3,6 KB-4,6 KB FLASH, 2,7 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="5d90c-122">Minimal 3.6 KB to 4.6 KB FLASH, 2.7 KB RAM footprint</span></span>
* <span data-ttu-id="5d90c-123">İstemci ve sunucu desteği</span><span class="sxs-lookup"><span data-stu-id="5d90c-123">Client and server support</span></span>
* <span data-ttu-id="5d90c-124">IPv4 desteği</span><span class="sxs-lookup"><span data-stu-id="5d90c-124">IPv4 support</span></span>

### <a name="p0p3---post-office-protocol-version-3-pop3"></a><span data-ttu-id="5d90c-125">P0P3-Postane Protokolü sürüm 3 (POP3)</span><span class="sxs-lookup"><span data-stu-id="5d90c-125">P0P3 - Post Office Protocol Version 3 (POP3)</span></span>

* <span data-ttu-id="5d90c-126">En az 8,1 KB ve 1,4 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="5d90c-126">Minimal 8.1 KB and 1.4 KB RAM footprint</span></span>
* <span data-ttu-id="5d90c-127">İstemci desteği</span><span class="sxs-lookup"><span data-stu-id="5d90c-127">Client support</span></span>

### <a name="snmp---simple-network-management-protocol-snmp"></a><span data-ttu-id="5d90c-128">SNMP-basit ağ Yönetim Protokolü (SNMP)</span><span class="sxs-lookup"><span data-stu-id="5d90c-128">SNMP - Simple Network Management Protocol (SNMP)</span></span>

* <span data-ttu-id="5d90c-129">En az 10,9 KB ve 2,6 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="5d90c-129">Minimal 10.9 KB and 2.6 KB RAM footprint</span></span>
* <span data-ttu-id="5d90c-130">VI, v2 ve v3 için aracı desteği</span><span class="sxs-lookup"><span data-stu-id="5d90c-130">Agent support for VI, V2, and V3</span></span>

### <a name="ftp-tftp---file-transfer-protocol-ftp-trivial-file-transfer-protocol-tftp"></a><span data-ttu-id="5d90c-131">FTP, TFTP-Dosya Aktarım Protokolü (FTP), Önemsiz Dosya Aktarım Protokolü (TFTP)</span><span class="sxs-lookup"><span data-stu-id="5d90c-131">FTP, TFTP - File Transfer Protocol (FTP), Trivial File Transfer Protocol (TFTP)</span></span>

* <span data-ttu-id="5d90c-132">FTP en az 1,8 KB-7.2 KBFLASH, 0,6 KB-2,1 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="5d90c-132">FTP Minimal 1.8 KB to 7.2KBFLASH, 0.6 KB to 2.1 KB RAM footprint</span></span>
* <span data-ttu-id="5d90c-133">TFTP en az 1,7 KB-2,4 KBFLASH, 0,3 KB-1,8 KB RAM ayak</span><span class="sxs-lookup"><span data-stu-id="5d90c-133">TFTP Minimal 1.7 KB to 2.4KBFLASH, 0.3 KB to 1.8 KB RAM footprint</span></span>
* <span data-ttu-id="5d90c-134">İstemci ve sunucu desteği</span><span class="sxs-lookup"><span data-stu-id="5d90c-134">Client and server support</span></span>

### <a name="ppp---polnt-to-point-protocol-ppp"></a><span data-ttu-id="5d90c-135">PPP-POlNT noktadan noktaya Protokolü (PPP)</span><span class="sxs-lookup"><span data-stu-id="5d90c-135">PPP - Polnt-to-PoInt Protocol (PPP)</span></span>

* <span data-ttu-id="5d90c-136">En az 7,1 KB ve 3,8 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="5d90c-136">Minimal 7.1 KB and 3.8 KB RAM footprint</span></span>
* <span data-ttu-id="5d90c-137">Güvenilir ve güvenilir.</span><span class="sxs-lookup"><span data-stu-id="5d90c-137">Dependable and reliable.</span></span>

### <a name="sntp---simple-network-time-protocol-sntp"></a><span data-ttu-id="5d90c-138">SNTP-basit ağ zaman Protokolü (SNTP)</span><span class="sxs-lookup"><span data-stu-id="5d90c-138">SNTP - Simple Network Time Protocol (SNTP)</span></span>

* <span data-ttu-id="5d90c-139">En az 4 KB ve 0,5 KB RAM</span><span class="sxs-lookup"><span data-stu-id="5d90c-139">Minimal 4 KB and 0.5 KB RAM</span></span>
* <span data-ttu-id="5d90c-140">İstemci desteği</span><span class="sxs-lookup"><span data-stu-id="5d90c-140">Client support</span></span>

### <a name="azure-rtos-netx-api"></a><span data-ttu-id="5d90c-141">Azure RTOS NetX API 'SI</span><span class="sxs-lookup"><span data-stu-id="5d90c-141">Azure RTOS NetX API</span></span>

* <span data-ttu-id="5d90c-142">Hızlı, sıfır kopya API 'SI uygulama</span><span class="sxs-lookup"><span data-stu-id="5d90c-142">Fast, zero-copy API implementation</span></span>
* <span data-ttu-id="5d90c-143">Eski yuva kodu taşıma için isteğe bağlı BSD katmanı</span><span class="sxs-lookup"><span data-stu-id="5d90c-143">Optional BSD layer for porting legacy socket code</span></span>

### <a name="igmp---internet-group-management-protocol-igmp"></a><span data-ttu-id="5d90c-144">IGMP-Internet Grup Yönetimi Protokolü (ıGMP)</span><span class="sxs-lookup"><span data-stu-id="5d90c-144">IGMP - Internet Group Management Protocol (IGMP)</span></span>

* <span data-ttu-id="5d90c-145">En az 2,5 KB FLASH</span><span class="sxs-lookup"><span data-stu-id="5d90c-145">Minimal 2.5 KB FLASH</span></span>
* <span data-ttu-id="5d90c-146">IPv4 çok noktaya yayın grubu desteği</span><span class="sxs-lookup"><span data-stu-id="5d90c-146">IPv4 multicast group support</span></span>
* <span data-ttu-id="5d90c-147">IXIA IxANVL doğrulanan</span><span class="sxs-lookup"><span data-stu-id="5d90c-147">IXIA IxANVL Validated</span></span>
* <span data-ttu-id="5d90c-148">İsteğe bağlı ıGMP istatistikleri</span><span class="sxs-lookup"><span data-stu-id="5d90c-148">Optional IGMP statistics</span></span>
* <span data-ttu-id="5d90c-149">Azure RTOS TraceX aracılığıyla sistem düzeyinde Izleme</span><span class="sxs-lookup"><span data-stu-id="5d90c-149">System-level Trace via Azure RTOS TraceX</span></span>

### <a name="udp---user-datagram-protocol-udp"></a><span data-ttu-id="5d90c-150">UDP-Kullanıcı veri birimi Protokolü (UDP)</span><span class="sxs-lookup"><span data-stu-id="5d90c-150">UDP - User Datagram Protocol (UDP)</span></span>

* <span data-ttu-id="5d90c-151">Yuva başına en az 2,5 KB FLASH, 124 yuva baytı</span><span class="sxs-lookup"><span data-stu-id="5d90c-151">Minimal 2.5 KB FLASH, 124 sockets bytes of RAM per socket</span></span>
* <span data-ttu-id="5d90c-152">Hızlı, neredeyse wıned TCP paket işleme:</span><span class="sxs-lookup"><span data-stu-id="5d90c-152">Fast, near wirespeed TCP packet processing:</span></span>
* <span data-ttu-id="5d90c-153">100 Mbps Ethernet, MCU @100MHz , 14% MCU kullanımı ÜZERINDE RX 95 Mbps</span><span class="sxs-lookup"><span data-stu-id="5d90c-153">RX 95 Mbps on 100 Mbps Ethernet, MCU @100MHz, 14% MCU Utilization</span></span>
* <span data-ttu-id="5d90c-154">TX 94 Mbps, 100 Mbps Ethernet, MCU @100MHz , 10% MCU kullanımı</span><span class="sxs-lookup"><span data-stu-id="5d90c-154">TX 94 Mbps on 100 Mbps Ethernet, MCU @100MHz, 10% MCU Utilization</span></span>
* <span data-ttu-id="5d90c-155">UDP hızlı yol™ teknolojisi</span><span class="sxs-lookup"><span data-stu-id="5d90c-155">UDP Fast Path™ technology</span></span>
* <span data-ttu-id="5d90c-156">UDP sayısıyla ilgili sınır yok</span><span class="sxs-lookup"><span data-stu-id="5d90c-156">No limits on the number of UDP</span></span>
* <span data-ttu-id="5d90c-157">IXIA IxANVL doğrulanan</span><span class="sxs-lookup"><span data-stu-id="5d90c-157">IXIA IxANVL Validated</span></span>
* <span data-ttu-id="5d90c-158">Yuva alma sırasında isteğe bağlı askıya alma</span><span class="sxs-lookup"><span data-stu-id="5d90c-158">Optional suspension on socket receive</span></span>
* <span data-ttu-id="5d90c-159">Tüm askıya alma sırasında isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="5d90c-159">Optional timeout on all suspension</span></span>
* <span data-ttu-id="5d90c-160">İsteğe bağlı UDP istatistikleri</span><span class="sxs-lookup"><span data-stu-id="5d90c-160">Optional UDP statistics</span></span>
* <span data-ttu-id="5d90c-161">Azure RTOS TraceX aracılığıyla sistem düzeyinde Izleme</span><span class="sxs-lookup"><span data-stu-id="5d90c-161">System-level Trace via Azure RTOS TraceX</span></span>

### <a name="tcp---transmission-control-protocol-tcp"></a><span data-ttu-id="5d90c-162">TCP-Iletim Denetim Protokolü (TCP)</span><span class="sxs-lookup"><span data-stu-id="5d90c-162">TCP - Transmission Control Protocol (TCP)</span></span>

* <span data-ttu-id="5d90c-163">Minimum 10,5 K8-12,5 KB FLASH, her yuva için 280 bayt RAM</span><span class="sxs-lookup"><span data-stu-id="5d90c-163">Minimal 10.5K8 to 12.5 KB FLASH, 280 bytes of RAM per socket</span></span>
* <span data-ttu-id="5d90c-164">Hızlı, neredeyse wlrespeed TCP paket işleme:</span><span class="sxs-lookup"><span data-stu-id="5d90c-164">Fast, near wlrespeed TCP packet processing:</span></span>
* <span data-ttu-id="5d90c-165">100 Mbps Ethernet, MCU @100MHz , 20% MCU ÜZERINDE RX 93 Mbps</span><span class="sxs-lookup"><span data-stu-id="5d90c-165">RX 93 Mbps on 100 Mbps Ethernet, MCU @100MHz, 20% MCU Utilization</span></span>
* <span data-ttu-id="5d90c-166">TX 94 Mbps, 100 Mbps Ethernet, MCU @100MHz , 27% MCU kullanımı</span><span class="sxs-lookup"><span data-stu-id="5d90c-166">TX 94 Mbps on 100 Mbps Ethernet, MCU @100MHz, 27% MCU Utilization</span></span>
* <span data-ttu-id="5d90c-167">Güvenilir bağlantı</span><span class="sxs-lookup"><span data-stu-id="5d90c-167">Reliable connection</span></span>
* <span data-ttu-id="5d90c-168">TCP yuvaları sayısında sınırsız</span><span class="sxs-lookup"><span data-stu-id="5d90c-168">No limits on the number of TCP sockets</span></span>
* <span data-ttu-id="5d90c-169">IXIA IxANVL doğrulanan</span><span class="sxs-lookup"><span data-stu-id="5d90c-169">IXIA IxANVL Validated</span></span>
* <span data-ttu-id="5d90c-170">Yuva alma/iletme sırasında isteğe bağlı askıya alma</span><span class="sxs-lookup"><span data-stu-id="5d90c-170">Optional suspension on socket receive/transmit</span></span>
* <span data-ttu-id="5d90c-171">Tüm askıya alma sırasında isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="5d90c-171">Optional timeout on all suspension</span></span>
* <span data-ttu-id="5d90c-172">İsteğe bağlı TCP istatistikleri</span><span class="sxs-lookup"><span data-stu-id="5d90c-172">Optional TCP statistics</span></span>
* <span data-ttu-id="5d90c-173">Azure RTOS TraceX aracılığıyla sistem düzeyinde Izleme</span><span class="sxs-lookup"><span data-stu-id="5d90c-173">System-level Trace via Azure RTOS TraceX</span></span>

### <a name="icmp---internet-control-message-protocol-icmp"></a><span data-ttu-id="5d90c-174">ICMP-Internet Denetim Iletisi Protokolü (ıCMP)</span><span class="sxs-lookup"><span data-stu-id="5d90c-174">ICMP - Internet Control Message Protocol (ICMP)</span></span>

* <span data-ttu-id="5d90c-175">En az 2,5 KB FLASH</span><span class="sxs-lookup"><span data-stu-id="5d90c-175">Minimal 2.5 KB FLASH</span></span>
* <span data-ttu-id="5d90c-176">IPv4 desteği</span><span class="sxs-lookup"><span data-stu-id="5d90c-176">IPv4 support</span></span>
* <span data-ttu-id="5d90c-177">IXIA IxANVL doğrulanan</span><span class="sxs-lookup"><span data-stu-id="5d90c-177">IXIA IxANVL Validated</span></span>
* <span data-ttu-id="5d90c-178">Ping isteği ve ping yanıtı</span><span class="sxs-lookup"><span data-stu-id="5d90c-178">Ping request and ping response</span></span>
* <span data-ttu-id="5d90c-179">Ping isteklerinde isteğe bağlı iş parçacığı askıya alma</span><span class="sxs-lookup"><span data-stu-id="5d90c-179">Optional thread suspension on ping requests</span></span>
* <span data-ttu-id="5d90c-180">Tüm askıya alma sırasında isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="5d90c-180">Optional timeout on all suspension</span></span>
* <span data-ttu-id="5d90c-181">İsteğe bağlı ıCMP istatistikleri</span><span class="sxs-lookup"><span data-stu-id="5d90c-181">Optional ICMP statistics</span></span>
* <span data-ttu-id="5d90c-182">Azure RTOS TraceX aracılığıyla sistem düzeyinde Izleme</span><span class="sxs-lookup"><span data-stu-id="5d90c-182">System-level Trace via Azure RTOS TraceX</span></span>

### <a name="ipv4---internet-protocol-ip"></a><span data-ttu-id="5d90c-183">IPv4-Internet Protokolü (IP)</span><span class="sxs-lookup"><span data-stu-id="5d90c-183">IPv4 - Internet Protocol (IP)</span></span>

* <span data-ttu-id="5d90c-184">Minimum 3,5 KB-8,5 KB FLASH, 2 KB-3 KB RAM ayak.</span><span class="sxs-lookup"><span data-stu-id="5d90c-184">Minimal 3.5 KB to 8.5 KB FLASH, 2 KB to 3 KB RAM footprint.</span></span>
* <span data-ttu-id="5d90c-185">Piconet™ mimarisi.</span><span class="sxs-lookup"><span data-stu-id="5d90c-185">Piconet™ Architecture.</span></span>
* <span data-ttu-id="5d90c-186">Hızlı, neredeyse wafklu performans.</span><span class="sxs-lookup"><span data-stu-id="5d90c-186">Fast, near wirespeed performance.</span></span>
* <span data-ttu-id="5d90c-187">Birden çok arabirim desteği.</span><span class="sxs-lookup"><span data-stu-id="5d90c-187">Multiple interface support.</span></span>
* <span data-ttu-id="5d90c-188">Çoklu bilgisayarlı destek.</span><span class="sxs-lookup"><span data-stu-id="5d90c-188">Multi-homed support.</span></span>
* <span data-ttu-id="5d90c-189">Statik yönlendirme desteği.</span><span class="sxs-lookup"><span data-stu-id="5d90c-189">Static routing support.</span></span>
* <span data-ttu-id="5d90c-190">IP parçalama/yeniden birleştirme desteği.</span><span class="sxs-lookup"><span data-stu-id="5d90c-190">IP fragmentation/reassembly support.</span></span>
* <span data-ttu-id="5d90c-191">IPv4 desteği.</span><span class="sxs-lookup"><span data-stu-id="5d90c-191">IPv4 Support.</span></span>
* <span data-ttu-id="5d90c-192">IXIA IxANVL doğrulanmadı.</span><span class="sxs-lookup"><span data-stu-id="5d90c-192">IXIA IxANVL Validated.</span></span>
* <span data-ttu-id="5d90c-193">Aşama II Ready Logo sertifikası.</span><span class="sxs-lookup"><span data-stu-id="5d90c-193">Phase II Ready Logo Certification.</span></span>
* <span data-ttu-id="5d90c-194">İsteğe bağlı IP istatistikleri.</span><span class="sxs-lookup"><span data-stu-id="5d90c-194">Optional IP statistics.</span></span>
* <span data-ttu-id="5d90c-195">İyi tanımlanmış, sezgisel fiziksel katman sürücüsü arabirimi.</span><span class="sxs-lookup"><span data-stu-id="5d90c-195">Well defined, intuitive physical layer driver interface.</span></span>
* <span data-ttu-id="5d90c-196">Azure RTOS TraceX aracılığıyla sistem düzeyinde Izleme.</span><span class="sxs-lookup"><span data-stu-id="5d90c-196">System-level Trace via Azure RTOS TraceX.</span></span>

### <a name="arprarp---address-resolution-protocol-arp-reverse-address-resolution-protocol-rarp"></a><span data-ttu-id="5d90c-197">ARP/RARP-Adres Çözümleme Protokolü (ARP), ters Adres Çözümleme Protokolü (RARP)</span><span class="sxs-lookup"><span data-stu-id="5d90c-197">ARP/RARP - Address Resolution Protocol (ARP), Reverse Address Resolution Protocol (RARP)</span></span>

* <span data-ttu-id="5d90c-198">Minimum 1,7 KB FLASH, RAM boyutu.</span><span class="sxs-lookup"><span data-stu-id="5d90c-198">Minimal 1.7 KB FLASH, RAM size.</span></span>
* <span data-ttu-id="5d90c-199">32-blt IPv4 ve 48-blt MAC adreslerinin dinamik çözünürlüğü.</span><span class="sxs-lookup"><span data-stu-id="5d90c-199">Dynamic resolution of 32-blt IPv4 and 48-blt MAC addresses.</span></span>
* <span data-ttu-id="5d90c-200">IXIA IxANVL doğrulanmadı.</span><span class="sxs-lookup"><span data-stu-id="5d90c-200">IXIA IxANVL Validated.</span></span>
* <span data-ttu-id="5d90c-201">Esnek, Kullanıcı tanımlı ARP önbelleği.</span><span class="sxs-lookup"><span data-stu-id="5d90c-201">Flexible, user-defined ARP cache.</span></span>
* <span data-ttu-id="5d90c-202">Gereksiz ARP desteği.</span><span class="sxs-lookup"><span data-stu-id="5d90c-202">Gratuitous ARP support.</span></span>
* <span data-ttu-id="5d90c-203">Uygulamaya göre belirlenen isteğe bağlı ARP/RARP istatistikleri.</span><span class="sxs-lookup"><span data-stu-id="5d90c-203">Optional ARP/RARP statistics determined by application.</span></span>
* <span data-ttu-id="5d90c-204">Azure RTOS TraceX aracılığıyla sistem düzeyinde Izleme.</span><span class="sxs-lookup"><span data-stu-id="5d90c-204">System-level Trace via Azure RTOS TraceX.</span></span>

### <a name="ethernet-wifi-bluetooth-le-154-etc"></a><span data-ttu-id="5d90c-205">ETHERNET, WiFi, BLUETOOTH LE, 15,4, vb.</span><span class="sxs-lookup"><span data-stu-id="5d90c-205">ETHERNET, WiFi, BLUETOOTH LE, 15.4, etc.</span></span>

## <a name="interoperability-verification"></a><span data-ttu-id="5d90c-206">Birlikte çalışabilirlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="5d90c-206">Interoperability verification</span></span>

<span data-ttu-id="5d90c-207">Azure RTOS NetX, RFC standartlarına uyar ve çoğu satıcının cihazlarıyla birlikte çalışabilirlik desteği sunar.</span><span class="sxs-lookup"><span data-stu-id="5d90c-207">Azure RTOS NetX conforms to RFC standards and offers complete interoperability with devices for most vendors.</span></span> <span data-ttu-id="5d90c-208">Azure RTOS NetX, Azure RTOS NetX Core TCP/IP protokol uygulamasının endüstri standardı IxANVL (otomatik ağ doğrulama kitaplığı) kullanır.</span><span class="sxs-lookup"><span data-stu-id="5d90c-208">Azure RTOS NetX also utilizes the industry standard IxANVL (Automated Network Validation Library) for the Azure RTOS NetX core TCP/IP protocol implementation.</span></span>

## <a name="advanced-technology"></a><span data-ttu-id="5d90c-209">Gelişmiş teknoloji</span><span class="sxs-lookup"><span data-stu-id="5d90c-209">Advanced technology</span></span>

<span data-ttu-id="5d90c-210">Azure RTOS NetX, aşağıdakileri içeren gelişmiş bir teknolojidir.</span><span class="sxs-lookup"><span data-stu-id="5d90c-210">Azure RTOS NetX is advanced technology that includes the following.</span></span>
* <span data-ttu-id="5d90c-211">Piconet™ mimarisi.</span><span class="sxs-lookup"><span data-stu-id="5d90c-211">Piconet™ architecture.</span></span>
* <span data-ttu-id="5d90c-212">Otomatik ölçeklendirme.</span><span class="sxs-lookup"><span data-stu-id="5d90c-212">Automatic scaling.</span></span>
* <span data-ttu-id="5d90c-213">UDP Fast-Path teknolojisi™.</span><span class="sxs-lookup"><span data-stu-id="5d90c-213">UDP Fast-Path Technology™.</span></span>
* <span data-ttu-id="5d90c-214">Esnek paket yönetimi.</span><span class="sxs-lookup"><span data-stu-id="5d90c-214">Flexible packet management.</span></span>
* <span data-ttu-id="5d90c-215">Sıfır-API ve uygulama kopyalama.</span><span class="sxs-lookup"><span data-stu-id="5d90c-215">Zero-copy API and implementation.</span></span>
* <span data-ttu-id="5d90c-216">Çoklu bilgisayarlı destek.</span><span class="sxs-lookup"><span data-stu-id="5d90c-216">Multi-homed support.</span></span>
* <span data-ttu-id="5d90c-217">Tüm askıya alma sırasında isteğe bağlı zaman aşımı.</span><span class="sxs-lookup"><span data-stu-id="5d90c-217">Optional timeout on all suspension.</span></span>
* <span data-ttu-id="5d90c-218">Statik yönlendirme desteği.</span><span class="sxs-lookup"><span data-stu-id="5d90c-218">Static routing support.</span></span>
* <span data-ttu-id="5d90c-219">Azure RTOS TraceX sistem analizi desteği.</span><span class="sxs-lookup"><span data-stu-id="5d90c-219">Azure RTOS TraceX system analysis support.</span></span>
