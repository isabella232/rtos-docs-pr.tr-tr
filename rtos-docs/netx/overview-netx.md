---
title: Azure RTOS NetX 'i anlama
description: Azure RTOS NetX, Azure RTOS ThreadX ile tam olarak tümleştirilmiş ve desteklenen tüm işlemciler için kullanılabilen TCP/IP protokol standartlarının yüksek performanslı bir uygulamasıdır.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: 029f73b755d5c40279125fb010ec35baaaf7f38d
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825583"
---
# <a name="overview-of-azure-rtos-netx"></a><span data-ttu-id="46820-103">Azure RTOS NetX 'e genel bakış</span><span class="sxs-lookup"><span data-stu-id="46820-103">Overview of Azure RTOS NetX</span></span>

<span data-ttu-id="46820-104">Azure RTOS NetX, özellikle derin gömülü, gerçek zamanlı ve IoT uygulamaları için tasarlanan bir endüstriyel sınıf TCP/IP IPv4 Embedded ağ yığınıdır.</span><span class="sxs-lookup"><span data-stu-id="46820-104">Azure RTOS NetX is an industrial grade TCP/IP IPv4 embedded network stack, designed specifically for deeply embedded, real-time, and IoT applications.</span></span> <span data-ttu-id="46820-105">Azure RTOS NetX, Microsoft 'un özgün IPv4 ağ yığınıdır ve aslında Azure RTOS 'ın bir alt kümesidir.</span><span class="sxs-lookup"><span data-stu-id="46820-105">Azure RTOS NetX is Microsoft's original IPv4 network stack, and is essentially a subset of Azure RTOS.</span></span> <span data-ttu-id="46820-106">NetX, IPv4, TCP ve UDP gibi çekirdek ağ protokollerine ve ek ve daha üst düzey eklenti protokollerinin eksiksiz bir paketine sahip gömülü uygulamalar sağlar.</span><span class="sxs-lookup"><span data-stu-id="46820-106">NetX provides embedded applications with core network protocols such as IPv4, TCP, and UDP as well as a complete suite of additional, higher-level add-on protocols.</span></span> <span data-ttu-id="46820-107">Küçük bir kaplama, Hızlı yürütme ve üstün kullanım kolaylığı, Azure RTOS NetX 'i en zorlu ekli IoT uygulamaları için ideal bir seçenek haline getirir.</span><span class="sxs-lookup"><span data-stu-id="46820-107">A small footprint, fast execution, and superior ease-of-use make Azure RTOS NetX an ideal choice for the most demanding embedded IoT applications.</span></span>

## <a name="api-protocols"></a><span data-ttu-id="46820-108">API protokolleri</span><span class="sxs-lookup"><span data-stu-id="46820-108">API protocols</span></span>

### <a name="telnet"></a><span data-ttu-id="46820-109">Sun</span><span class="sxs-lookup"><span data-stu-id="46820-109">TELNET</span></span>

* <span data-ttu-id="46820-110">En az 0,5 KB ve 0,3 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="46820-110">Minimal 0.5 KB and 0.3 KB RAM footprint</span></span>
* <span data-ttu-id="46820-111">İstemci ve sunucu desteği</span><span class="sxs-lookup"><span data-stu-id="46820-111">Client and server support</span></span>
* <span data-ttu-id="46820-112">Sezgisel Telnet API 'Leri *: \* nx_telnet_*</span><span class="sxs-lookup"><span data-stu-id="46820-112">Intuitive Telnet APIs: *nx_telnet_\**</span></span>

### <a name="auto-ip"></a><span data-ttu-id="46820-113">Otomatik IP</span><span class="sxs-lookup"><span data-stu-id="46820-113">Auto IP</span></span>

* <span data-ttu-id="46820-114">Otomatik IPv4 adresi ataması</span><span class="sxs-lookup"><span data-stu-id="46820-114">Automatic IPv4 address assignment</span></span>
* <span data-ttu-id="46820-115">En az 1,2 KB, 300 bayt RAM</span><span class="sxs-lookup"><span data-stu-id="46820-115">Minimal 1.2 KB, 300 bytes of RAM</span></span>
* <span data-ttu-id="46820-116">Sezgisel Oto IP API 'Leri *: \* nx_autoip_*</span><span class="sxs-lookup"><span data-stu-id="46820-116">Intuitive AutoIP APIs: *nx_autoip_\**</span></span>

### <a name="http---hypertext-transfer-protocolhttp"></a><span data-ttu-id="46820-117">HTTP-Köprü Metni Aktarım Protokolü (HTTP)</span><span class="sxs-lookup"><span data-stu-id="46820-117">HTTP - Hypertext Transfer Protocol(HTTP)</span></span>

* <span data-ttu-id="46820-118">En az 2,8 KB-4.8 KBFLASH, 0,4 KB-1,0 KB RAM ayak</span><span class="sxs-lookup"><span data-stu-id="46820-118">Minimal 2.8 KB to 4.8KBFLASH, 0.4 KB to 1.0 KB RAM footprint</span></span>
* <span data-ttu-id="46820-119">İstemci ve sunucu desteği</span><span class="sxs-lookup"><span data-stu-id="46820-119">Client and server support</span></span>
* <span data-ttu-id="46820-120">Sezgisel HTTP API 'Leri *: \* nx_http_*</span><span class="sxs-lookup"><span data-stu-id="46820-120">Intuitive HTTP APIs: *nx_http_\**</span></span>

### <a name="smtp---simple-mail-transfer-protocol-smtp"></a><span data-ttu-id="46820-121">SMTP-Basit Posta Aktarım Protokolü (SMTP)</span><span class="sxs-lookup"><span data-stu-id="46820-121">SMTP - Simple Mail Transfer Protocol (SMTP)</span></span>

* <span data-ttu-id="46820-122">En az 4,1 KB ve 0,6 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="46820-122">Minimal 4.1 KB and 0.6 KB RAM footprint</span></span>
* <span data-ttu-id="46820-123">İstemci desteği</span><span class="sxs-lookup"><span data-stu-id="46820-123">Client support</span></span>
* <span data-ttu-id="46820-124">Sezgisel SMTP API 'Leri *: \* nx_smtp_*</span><span class="sxs-lookup"><span data-stu-id="46820-124">Intuitive SMTP APIs: *nx_smtp_\**</span></span>

### <a name="dhcp---dynamic-host-configuration-protocol-dhcp"></a><span data-ttu-id="46820-125">DHCP-dinamik ana bilgisayar Yapılandırma Protokolü (DHCP)</span><span class="sxs-lookup"><span data-stu-id="46820-125">DHCP - Dynamic Host Configuration Protocol (DHCP)</span></span>

* <span data-ttu-id="46820-126">Minimum 3,6 KB-4,6 KB FLASH, 2,7 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="46820-126">Minimal 3.6 KB to 4.6 KB FLASH, 2.7 KB RAM footprint</span></span>
* <span data-ttu-id="46820-127">İstemci ve sunucu desteği</span><span class="sxs-lookup"><span data-stu-id="46820-127">Client and server support</span></span>
* <span data-ttu-id="46820-128">IPv4 desteği</span><span class="sxs-lookup"><span data-stu-id="46820-128">IPv4 support</span></span>
* <span data-ttu-id="46820-129">Sezgisel DHCP API 'Leri *: \* nx_dhcp_*</span><span class="sxs-lookup"><span data-stu-id="46820-129">Intuitive DHCP APIs: *nx_dhcp_\**</span></span>

### <a name="p0p3---post-office-protocol-version-3-pop3"></a><span data-ttu-id="46820-130">P0P3-Postane Protokolü sürüm 3 (POP3)</span><span class="sxs-lookup"><span data-stu-id="46820-130">P0P3 - Post Office Protocol Version 3 (POP3)</span></span>

* <span data-ttu-id="46820-131">En az 8,1 KB ve 1,4 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="46820-131">Minimal 8.1 KB and 1.4 KB RAM footprint</span></span>
* <span data-ttu-id="46820-132">İstemci desteği</span><span class="sxs-lookup"><span data-stu-id="46820-132">Client support</span></span>
* <span data-ttu-id="46820-133">Sezgisel P0P3 API 'Leri *: \* nx_pop3_*</span><span class="sxs-lookup"><span data-stu-id="46820-133">Intuitive P0P3 APIs: *nx_pop3_\**</span></span>

### <a name="snmp---simple-network-management-protocol-snmp"></a><span data-ttu-id="46820-134">SNMP-basit ağ Yönetim Protokolü (SNMP)</span><span class="sxs-lookup"><span data-stu-id="46820-134">SNMP - Simple Network Management Protocol (SNMP)</span></span>

* <span data-ttu-id="46820-135">En az 10,9 KB ve 2,6 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="46820-135">Minimal 10.9 KB and 2.6 KB RAM footprint</span></span>
* <span data-ttu-id="46820-136">VI, v2 ve v3 için aracı desteği</span><span class="sxs-lookup"><span data-stu-id="46820-136">Agent support for VI, V2, and V3</span></span>
* <span data-ttu-id="46820-137">Sezgisel SNMP API 'Leri *: \* nx_snmp_*</span><span class="sxs-lookup"><span data-stu-id="46820-137">Intuitive SNMP APIs: *nx_snmp_\**</span></span>

### <a name="ftp-tftp---file-transfer-protocol-ftp-trivial-file-transfer-protocol-tftp"></a><span data-ttu-id="46820-138">FTP, TFTP-Dosya Aktarım Protokolü (FTP), Önemsiz Dosya Aktarım Protokolü (TFTP)</span><span class="sxs-lookup"><span data-stu-id="46820-138">FTP, TFTP - File Transfer Protocol (FTP), Trivial File Transfer Protocol (TFTP)</span></span>

* <span data-ttu-id="46820-139">FTP en az 1,8 KB-7.2 KBFLASH, 0,6 KB-2,1 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="46820-139">FTP Minimal 1.8 KB to 7.2KBFLASH, 0.6 KB to 2.1 KB RAM footprint</span></span>
* <span data-ttu-id="46820-140">TFTP en az 1,7 KB-2,4 KBFLASH, 0,3 KB-1,8 KB RAM ayak</span><span class="sxs-lookup"><span data-stu-id="46820-140">TFTP Minimal 1.7 KB to 2.4KBFLASH, 0.3 KB to 1.8 KB RAM footprint</span></span>
* <span data-ttu-id="46820-141">İstemci ve sunucu desteği</span><span class="sxs-lookup"><span data-stu-id="46820-141">Client and server support</span></span>
* <span data-ttu-id="46820-142">Sezgisel FTP ve TFTP API 'Leri: <i>nx_ftp_ *</i> veya <i>nx_tftp_*</i></span><span class="sxs-lookup"><span data-stu-id="46820-142">Intuitive FTP and TFTP APIs: <i>nx_ftp_ *</i> or <i>nx_tftp_*</i></span></span>

### <a name="ppp---polnt-to-point-protocol-ppp"></a><span data-ttu-id="46820-143">PPP-POlNT noktadan noktaya Protokolü (PPP)</span><span class="sxs-lookup"><span data-stu-id="46820-143">PPP - Polnt-to-PoInt Protocol (PPP)</span></span>

* <span data-ttu-id="46820-144">En az 7,1 KB ve 3,8 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="46820-144">Minimal 7.1 KB and 3.8 KB RAM footprint</span></span>
* <span data-ttu-id="46820-145">Sezgisel PPP API 'Leri *: \* nx_ppp_*</span><span class="sxs-lookup"><span data-stu-id="46820-145">Intuitive PPP APIs: *nx_ppp_\**</span></span>

### <a name="sntp---simple-network-time-protocol-sntp"></a><span data-ttu-id="46820-146">SNTP-basit ağ zaman Protokolü (SNTP)</span><span class="sxs-lookup"><span data-stu-id="46820-146">SNTP - Simple Network Time Protocol (SNTP)</span></span>

* <span data-ttu-id="46820-147">En az 4 KB ve 0,5 KB RAM</span><span class="sxs-lookup"><span data-stu-id="46820-147">Minimal 4 KB and 0.5 KB RAM</span></span>
* <span data-ttu-id="46820-148">İstemci desteği</span><span class="sxs-lookup"><span data-stu-id="46820-148">Client support</span></span>
* <span data-ttu-id="46820-149">Sezgisel SNTP API 'Leri *: \* nx_sntp_*</span><span class="sxs-lookup"><span data-stu-id="46820-149">Intuitive SNTP APIs: *nx_sntp_\**</span></span>

### <a name="azure-rtos-netx-api"></a><span data-ttu-id="46820-150">Azure RTOS NetX API 'SI</span><span class="sxs-lookup"><span data-stu-id="46820-150">Azure RTOS NetX API</span></span>

* <span data-ttu-id="46820-151">Sezgisel ve tutarlı API</span><span class="sxs-lookup"><span data-stu-id="46820-151">Intuitive and consistent API</span></span>
* <span data-ttu-id="46820-152">İsim-fiil adlandırma kuralı</span><span class="sxs-lookup"><span data-stu-id="46820-152">Noun-verb naming convention</span></span>
* <span data-ttu-id="46820-153">Hızlı, sıfır kopya API 'SI uygulama</span><span class="sxs-lookup"><span data-stu-id="46820-153">Fast, zero-copy API implementation</span></span>
* <span data-ttu-id="46820-154">Azure RTOS NetX olarak kolayca tanımlanması için tüm API işlevlerinin önde gelen <i>nx_ \*</i> vardır</span><span class="sxs-lookup"><span data-stu-id="46820-154">All API functions have leading <i>nx_\*</i> to easily identify as Azure RTOS NetX</span></span>
* <span data-ttu-id="46820-155">API işlevlerinin engellenmesi isteğe bağlı bir iş parçacığı zaman aşımına sahiptir</span><span class="sxs-lookup"><span data-stu-id="46820-155">Blocking API functions have an optional thread timeout</span></span>
* <span data-ttu-id="46820-156">Eski yuva kodu taşıma için isteğe bağlı BSD katmanı</span><span class="sxs-lookup"><span data-stu-id="46820-156">Optional BSD layer for porting legacy socket code</span></span>

### <a name="igmp---internet-group-management-protocol-igmp"></a><span data-ttu-id="46820-157">IGMP-Internet Grup Yönetimi Protokolü (ıGMP)</span><span class="sxs-lookup"><span data-stu-id="46820-157">IGMP - Internet Group Management Protocol (IGMP)</span></span>

* <span data-ttu-id="46820-158">En az 2,5 KB FLASH</span><span class="sxs-lookup"><span data-stu-id="46820-158">Minimal 2.5 KB FLASH</span></span>
* <span data-ttu-id="46820-159">IPv4 çok noktaya yayın grubu desteği</span><span class="sxs-lookup"><span data-stu-id="46820-159">IPv4 multicast group support</span></span>
* <span data-ttu-id="46820-160">IXIA IxANVL doğrulanan</span><span class="sxs-lookup"><span data-stu-id="46820-160">IXIA IxANVL Validated</span></span>
* <span data-ttu-id="46820-161">İsteğe bağlı ıGMP istatistikleri</span><span class="sxs-lookup"><span data-stu-id="46820-161">Optional IGMP statistics</span></span>
* <span data-ttu-id="46820-162">Azure RTOS TraceX aracılığıyla sistem düzeyinde Izleme</span><span class="sxs-lookup"><span data-stu-id="46820-162">System-level Trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="46820-163">Sezgisel ıGMP API 'Leri *: \* nx_igmp_*</span><span class="sxs-lookup"><span data-stu-id="46820-163">Intuitive IGMP APIs: *nx_igmp_\**</span></span>

### <a name="udp---user-datagram-protocol-udp"></a><span data-ttu-id="46820-164">UDP-Kullanıcı veri birimi Protokolü (UDP)</span><span class="sxs-lookup"><span data-stu-id="46820-164">UDP - User Datagram Protocol (UDP)</span></span>

* <span data-ttu-id="46820-165">Yuva başına en az 2,5 KB FLASH, 124 yuva baytı</span><span class="sxs-lookup"><span data-stu-id="46820-165">Minimal 2.5 KB FLASH, 124 sockets bytes of RAM per socket</span></span>
* <span data-ttu-id="46820-166">Hızlı, neredeyse wıned TCP paket işleme:</span><span class="sxs-lookup"><span data-stu-id="46820-166">Fast, near wirespeed TCP packet processing:</span></span>
* <span data-ttu-id="46820-167">100 Mbps Ethernet, MCU @100MHz , 14% MCU kullanımı ÜZERINDE RX 95 Mbps</span><span class="sxs-lookup"><span data-stu-id="46820-167">RX 95 Mbps on 100 Mbps Ethernet, MCU @100MHz, 14% MCU Utilization</span></span>
* <span data-ttu-id="46820-168">TX 94 Mbps, 100 Mbps Ethernet, MCU @100MHz , 10% MCU kullanımı</span><span class="sxs-lookup"><span data-stu-id="46820-168">TX 94 Mbps on 100 Mbps Ethernet, MCU @100MHz, 10% MCU Utilization</span></span>
* <span data-ttu-id="46820-169">UDP hızlı yol™ teknolojisi</span><span class="sxs-lookup"><span data-stu-id="46820-169">UDP Fast Path™ technology</span></span>
* <span data-ttu-id="46820-170">UDP sayısıyla ilgili sınır yok</span><span class="sxs-lookup"><span data-stu-id="46820-170">No limits on the number of UDP</span></span>
* <span data-ttu-id="46820-171">IXIA IxANVL doğrulanan</span><span class="sxs-lookup"><span data-stu-id="46820-171">IXIA IxANVL Validated</span></span>
* <span data-ttu-id="46820-172">Yuva alma sırasında isteğe bağlı askıya alma</span><span class="sxs-lookup"><span data-stu-id="46820-172">Optional suspension on socket receive</span></span>
* <span data-ttu-id="46820-173">Tüm askıya alma sırasında isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="46820-173">Optional timeout on all suspension</span></span>
* <span data-ttu-id="46820-174">İsteğe bağlı UDP istatistikleri</span><span class="sxs-lookup"><span data-stu-id="46820-174">Optional UDP statistics</span></span>
* <span data-ttu-id="46820-175">Azure RTOS TraceX aracılığıyla sistem düzeyinde Izleme</span><span class="sxs-lookup"><span data-stu-id="46820-175">System-level Trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="46820-176">Sezgisel UDP API 'Leri *: \* nx_udp_*</span><span class="sxs-lookup"><span data-stu-id="46820-176">Intuitive UDP APIs: *nx_udp_\**</span></span>

### <a name="tcp---transmission-control-protocol-tcp"></a><span data-ttu-id="46820-177">TCP-Iletim Denetim Protokolü (TCP)</span><span class="sxs-lookup"><span data-stu-id="46820-177">TCP - Transmission Control Protocol (TCP)</span></span>

* <span data-ttu-id="46820-178">Minimum 10,5 K8-12,5 KB FLASH, her yuva için 280 bayt RAM</span><span class="sxs-lookup"><span data-stu-id="46820-178">Minimal 10.5K8 to 12.5 KB FLASH, 280 bytes of RAM per socket</span></span>
* <span data-ttu-id="46820-179">Hızlı, neredeyse wlrespeed TCP paket işleme:</span><span class="sxs-lookup"><span data-stu-id="46820-179">Fast, near wlrespeed TCP packet processing:</span></span>
* <span data-ttu-id="46820-180">100 Mbps Ethernet, MCU @100MHz , 20% MCU ÜZERINDE RX 93 Mbps</span><span class="sxs-lookup"><span data-stu-id="46820-180">RX 93 Mbps on 100 Mbps Ethernet, MCU @100MHz, 20% MCU Utilization</span></span>
* <span data-ttu-id="46820-181">TX 94 Mbps, 100 Mbps Ethernet, MCU @100MHz , 27% MCU kullanımı</span><span class="sxs-lookup"><span data-stu-id="46820-181">TX 94 Mbps on 100 Mbps Ethernet, MCU @100MHz, 27% MCU Utilization</span></span>
* <span data-ttu-id="46820-182">Güvenilir bağlantı</span><span class="sxs-lookup"><span data-stu-id="46820-182">Reliable connection</span></span>
* <span data-ttu-id="46820-183">TCP yuvaları sayısında sınırsız</span><span class="sxs-lookup"><span data-stu-id="46820-183">No limits on the number of TCP sockets</span></span>
* <span data-ttu-id="46820-184">IXIA IxANVL doğrulanan</span><span class="sxs-lookup"><span data-stu-id="46820-184">IXIA IxANVL Validated</span></span>
* <span data-ttu-id="46820-185">Yuva alma/iletme sırasında isteğe bağlı askıya alma</span><span class="sxs-lookup"><span data-stu-id="46820-185">Optional suspension on socket receive/transmit</span></span>
* <span data-ttu-id="46820-186">Tüm askıya alma sırasında isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="46820-186">Optional timeout on all suspension</span></span>
* <span data-ttu-id="46820-187">İsteğe bağlı TCP istatistikleri</span><span class="sxs-lookup"><span data-stu-id="46820-187">Optional TCP statistics</span></span>
* <span data-ttu-id="46820-188">Azure RTOS TraceX aracılığıyla sistem düzeyinde Izleme</span><span class="sxs-lookup"><span data-stu-id="46820-188">System-level Trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="46820-189">Sezgisel TCP API 'Leri *: \* nx_tcp_*</span><span class="sxs-lookup"><span data-stu-id="46820-189">Intuitive TCP APIs:  *nx_tcp_\**</span></span>

### <a name="icmp---internet-control-message-protocol-icmp"></a><span data-ttu-id="46820-190">ICMP-Internet Denetim Iletisi Protokolü (ıCMP)</span><span class="sxs-lookup"><span data-stu-id="46820-190">ICMP - Internet Control Message Protocol (ICMP)</span></span>

* <span data-ttu-id="46820-191">En az 2,5 KB FLASH</span><span class="sxs-lookup"><span data-stu-id="46820-191">Minimal 2.5 KB FLASH</span></span>
* <span data-ttu-id="46820-192">IPv4 desteği</span><span class="sxs-lookup"><span data-stu-id="46820-192">IPv4 support</span></span>
* <span data-ttu-id="46820-193">IXIA IxANVL doğrulanan</span><span class="sxs-lookup"><span data-stu-id="46820-193">IXIA IxANVL Validated</span></span>
* <span data-ttu-id="46820-194">Ping isteği ve ping yanıtı</span><span class="sxs-lookup"><span data-stu-id="46820-194">Ping request and ping response</span></span>
* <span data-ttu-id="46820-195">Ping isteklerinde isteğe bağlı iş parçacığı askıya alma</span><span class="sxs-lookup"><span data-stu-id="46820-195">Optional thread suspension on ping requests</span></span>
* <span data-ttu-id="46820-196">Tüm askıya alma sırasında isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="46820-196">Optional timeout on all suspension</span></span>
* <span data-ttu-id="46820-197">İsteğe bağlı ıCMP istatistikleri</span><span class="sxs-lookup"><span data-stu-id="46820-197">Optional ICMP statistics</span></span>
* <span data-ttu-id="46820-198">Azure RTOS TraceX aracılığıyla sistem düzeyinde Izleme</span><span class="sxs-lookup"><span data-stu-id="46820-198">System-level Trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="46820-199">Sezgisel ıCMP API 'Leri *: \* nx_icmp_*</span><span class="sxs-lookup"><span data-stu-id="46820-199">Intuitive ICMP APIs: *nx_icmp_\**</span></span>

### <a name="ipv4---internet-protocol-ip"></a><span data-ttu-id="46820-200">IPv4-Internet Protokolü (IP)</span><span class="sxs-lookup"><span data-stu-id="46820-200">IPv4 - Internet Protocol (IP)</span></span>

* <span data-ttu-id="46820-201">Minimum 3,5 KB-8,5 KB FLASH, 2 KB-3 KB RAM ayak</span><span class="sxs-lookup"><span data-stu-id="46820-201">Minimal 3.5 KB to 8.5 KB FLASH, 2 KB to 3 KB RAM footprint</span></span>
* <span data-ttu-id="46820-202">Piconet™ mimarisi</span><span class="sxs-lookup"><span data-stu-id="46820-202">Piconet™ Architecture</span></span>
* <span data-ttu-id="46820-203">Hızlı, neredeyse wafklu performans</span><span class="sxs-lookup"><span data-stu-id="46820-203">Fast, near wirespeed performance</span></span>
* <span data-ttu-id="46820-204">Birden çok arabirim desteği</span><span class="sxs-lookup"><span data-stu-id="46820-204">Multiple interface support</span></span>
* <span data-ttu-id="46820-205">Çok sayfalı destek</span><span class="sxs-lookup"><span data-stu-id="46820-205">Multihomed support</span></span>
* <span data-ttu-id="46820-206">Statik yönlendirme desteği</span><span class="sxs-lookup"><span data-stu-id="46820-206">Static routing support</span></span>
* <span data-ttu-id="46820-207">IP parçalama/yeniden birleştirme desteği</span><span class="sxs-lookup"><span data-stu-id="46820-207">IP fragmentation/reassembly support</span></span>
* <span data-ttu-id="46820-208">IPv4 desteği</span><span class="sxs-lookup"><span data-stu-id="46820-208">IPv4 Support</span></span>
* <span data-ttu-id="46820-209">IXIA IxANVL doğrulanan</span><span class="sxs-lookup"><span data-stu-id="46820-209">IXIA IxANVL Validated</span></span>
* <span data-ttu-id="46820-210">Aşama II Ready Logo sertifikası</span><span class="sxs-lookup"><span data-stu-id="46820-210">Phase II Ready Logo Certification</span></span>
* <span data-ttu-id="46820-211">İsteğe bağlı IP istatistikleri</span><span class="sxs-lookup"><span data-stu-id="46820-211">Optional IP statistics</span></span>
* <span data-ttu-id="46820-212">İyi tanımlanmış, sezgisel fiziksel katman sürücü arabirimi</span><span class="sxs-lookup"><span data-stu-id="46820-212">Well defined, intuitive physical layer driver interface</span></span>
* <span data-ttu-id="46820-213">Azure RTOS TraceX aracılığıyla sistem düzeyinde Izleme</span><span class="sxs-lookup"><span data-stu-id="46820-213">System-level Trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="46820-214">Sezgisel IP katmanı API 'leri *: \* nx_ip_*, *nxd_ip_ \**</span><span class="sxs-lookup"><span data-stu-id="46820-214">Intuitive IP layer APIs: *nx_ip_\**, *nxd_ip_\**</span></span>
* <span data-ttu-id="46820-215">TUV ve UL-ıEC 61508 SIL 4, ıEC 62304 Class C, ISO 26262 asıl D ve EN 50128 SW-SIL4 tarafından ön sertifikalı</span><span class="sxs-lookup"><span data-stu-id="46820-215">Pre-certified by TUV and UL to IEC 61508 SIL 4, IEC 62304 Class C, ISO 26262 ASIL D, and EN 50128 SW-SIL4</span></span>

### <a name="arprarp---address-resolution-protocol-arp-reverse-address-resolution-protocol-rarp"></a><span data-ttu-id="46820-216">ARP/RARP-Adres Çözümleme Protokolü (ARP), ters Adres Çözümleme Protokolü (RARP)</span><span class="sxs-lookup"><span data-stu-id="46820-216">ARP/RARP - Address Resolution Protocol (ARP), Reverse Address Resolution Protocol (RARP)</span></span>

* <span data-ttu-id="46820-217">Minimum 1,7 KB FLASH, RAM boyutu</span><span class="sxs-lookup"><span data-stu-id="46820-217">Minimal 1.7 KB FLASH, RAM size</span></span>
* <span data-ttu-id="46820-218">32-blt IPv4 ve 48-blt MAC adreslerinin dinamik çözünürlüğü</span><span class="sxs-lookup"><span data-stu-id="46820-218">Dynamic resolution of 32-blt IPv4 and 48-blt MAC addresses</span></span>
* <span data-ttu-id="46820-219">IXIA IxANVL doğrulanan</span><span class="sxs-lookup"><span data-stu-id="46820-219">IXIA IxANVL Validated</span></span>
* <span data-ttu-id="46820-220">Esnek, Kullanıcı tanımlı ARP önbelleği</span><span class="sxs-lookup"><span data-stu-id="46820-220">Flexible, user-defined ARP cache</span></span>
* <span data-ttu-id="46820-221">Gereksiz ARP desteği</span><span class="sxs-lookup"><span data-stu-id="46820-221">Gratuitous ARP support</span></span>
* <span data-ttu-id="46820-222">Uygulamaya göre belirlenen isteğe bağlı ARP/RARP istatistikleri</span><span class="sxs-lookup"><span data-stu-id="46820-222">Optional ARP/RARP statistics determined by application</span></span>
* <span data-ttu-id="46820-223">Azure RTOS TraceX aracılığıyla sistem düzeyinde Izleme</span><span class="sxs-lookup"><span data-stu-id="46820-223">System-level Trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="46820-224">Sezgisel ARP/RARP API 'leri *: \* nx_arp_*, *nx_rarp_ \**</span><span class="sxs-lookup"><span data-stu-id="46820-224">Intuitive ARP/RARP APIs: *nx_arp_\**, *nx_rarp_\**</span></span>

### <a name="ethernet-wifi-bluetooth-le-154-etc"></a><span data-ttu-id="46820-225">ETHERNET, WiFi, BLUETOOTH LE, 15,4, vb.</span><span class="sxs-lookup"><span data-stu-id="46820-225">ETHERNET, WiFi, BLUETOOTH LE, 15.4, etc.</span></span>

## <a name="small-footprint"></a><span data-ttu-id="46820-226">Küçük ayak izi</span><span class="sxs-lookup"><span data-stu-id="46820-226">Small-footprint</span></span>

<span data-ttu-id="46820-227">Azure RTOS NetX, temel IP ve UDP desteği için 9 KB 'den 15 KB 'a kadar yeniden küçük bir parmak izine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="46820-227">Azure RTOS NetX has a remarkably small footprint of 9 KB to 15 KB for basic IP and UDP support.</span></span> <span data-ttu-id="46820-228">TCP işlevselliği için 10 KB ila 13 KB 'lık yönerge alanı belleği gerekir.</span><span class="sxs-lookup"><span data-stu-id="46820-228">An additional 10 KB to 13 KB of instruction area memory is needed for TCP functionality.</span></span> <span data-ttu-id="46820-229">Azure RTOS NetX RAM kullanımı, genellikle 2,6 KB 'den 3,6 KB 'ye ve uygulama tarafından tanımlanan paket havuzu belleğine göre değişir.</span><span class="sxs-lookup"><span data-stu-id="46820-229">Azure RTOS NetX RAM usage typically ranges from 2.6 KB to 3.6 KB plus the packet pool memory, which is defined by the application.</span></span> <span data-ttu-id="46820-230">Azure RTOS ThreadX gibi Azure RTOS NetX boyutu, uygulama tarafından kullanılan hizmetlere göre otomatik olarak ölçeklendirilir.</span><span class="sxs-lookup"><span data-stu-id="46820-230">Like Azure RTOS ThreadX, the size of Azure RTOS NetX automatically scales based on the services used by the application.</span></span> <span data-ttu-id="46820-231">Bu, karmaşık yapılandırma ve derleme parametrelerine gerek duymayı neredeyse ortadan kaldırır, böylece geliştirici daha kolay hale getirir.</span><span class="sxs-lookup"><span data-stu-id="46820-231">This virtually eliminates the need for complicated configuration and build parameters, making things easier for the developer.</span></span>

## <a name="fast-execution"></a><span data-ttu-id="46820-232">Hızlı yürütme</span><span class="sxs-lookup"><span data-stu-id="46820-232">Fast execution</span></span>

<span data-ttu-id="46820-233">Azure RTOS NetX, sıfır kopya bir paket gönderme/alma uygulamasını sağlar ve en hızlı olası performansı elde etmek için Azure RTOS ThreadX ile büyük ölçüde tümleşiktir.</span><span class="sxs-lookup"><span data-stu-id="46820-233">Azure RTOS NetX provides a zero-copy packet send/receive implementation and is highly integrated with Azure RTOS ThreadX to achieve the fastest possible performance.</span></span> <span data-ttu-id="46820-234">Örneğin, Azure RTOS NetX genellikle işlemci döngülerinin yalnızca küçük bir yüzdesini kullanarak 80 MHz bir işlemcide (veya daha az) neredeyse Won 'a yönelik veri aktarımlarını elde edebilir.</span><span class="sxs-lookup"><span data-stu-id="46820-234">For example, Azure RTOS NetX can typically achieve near wirespeed data transfers on an 80-MHz processor (or less), while using only a small percentage of the processor cycles.</span></span>

## <a name="simple-easy-to-use"></a><span data-ttu-id="46820-235">Basit, kullanımı kolay</span><span class="sxs-lookup"><span data-stu-id="46820-235">Simple, easy-to-use</span></span>

<span data-ttu-id="46820-236">Azure RTOS NetX kullanımı basittir.</span><span class="sxs-lookup"><span data-stu-id="46820-236">Azure RTOS NetX is simple to use.</span></span> <span data-ttu-id="46820-237">Azure RTOS NetX API 'SI sezgisel ve yüksek işlevselliğe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="46820-237">The Azure RTOS NetX API is both intuitive and highly functional.</span></span> <span data-ttu-id="46820-238">API adları gerçek sözcüklerden oluşur ve "alfabe sonunda" değil, diğer ağ ürünlerinde ortak olan çok daha fazla kısaltılmış adlar değildir.</span><span class="sxs-lookup"><span data-stu-id="46820-238">The API names are made of real words and not “alphabet soup” or highly abbreviated names that are so common in other networking products.</span></span> <span data-ttu-id="46820-239">Tüm Azure RTOS NetX API 'Lerinin önde bir *nx_* vardır ve bir ad fiil adlandırma kuralını takip edin.</span><span class="sxs-lookup"><span data-stu-id="46820-239">All Azure RTOS NetX APIs have a leading *nx_* and follow a noun-verb naming convention.</span></span> <span data-ttu-id="46820-240">Ayrıca, API 'nin tamamında işlevsel bir tutarlılık vardır.</span><span class="sxs-lookup"><span data-stu-id="46820-240">Furthermore, there is a functional consistency throughout the API.</span></span> <span data-ttu-id="46820-241">Örneğin, askıya aldığı tüm API işlevlerinin aynı şekilde işlev gösteren isteğe bağlı bir zaman aşımı vardır.</span><span class="sxs-lookup"><span data-stu-id="46820-241">For example, all API functions that suspend have an optional timeout that functions in an identical manner.</span></span> <span data-ttu-id="46820-242">Eski uygulamalar için, Azure RTOS NetX, ek bir BSD soketi uyumlu katman sağlar.</span><span class="sxs-lookup"><span data-stu-id="46820-242">For legacy applications, Azure RTOS NetX offers an additional BSD socket compatible layer.</span></span> <span data-ttu-id="46820-243">Bu katman, geliştiricilerin büyük ağ uygulamalarını kolayca geçirmelerine yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="46820-243">This layer helps developers migrate large networking applications with ease.</span></span>

## <a name="interoperability-verification"></a><span data-ttu-id="46820-244">Birlikte çalışabilirlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="46820-244">Interoperability verification</span></span>

<span data-ttu-id="46820-245">Azure RTOS NetX, RFC standartlarına uyar ve çoğu satıcının cihazlarıyla birlikte çalışabilirlik desteği sunar.</span><span class="sxs-lookup"><span data-stu-id="46820-245">Azure RTOS NetX conforms to RFC standards and offers complete interoperability with devices for most vendors.</span></span> <span data-ttu-id="46820-246">Azure RTOS NetX, Azure RTOS NetX Core TCP/IP protokol uygulamasının endüstri standardı IxANVL (otomatik ağ doğrulama kitaplığı) kullanır.</span><span class="sxs-lookup"><span data-stu-id="46820-246">Azure RTOS NetX also utilizes the industry standard IxANVL (Automated Network Validation Library) for the Azure RTOS NetX core TCP/IP protocol implementation.</span></span>

## <a name="advanced-technology"></a><span data-ttu-id="46820-247">Gelişmiş teknoloji</span><span class="sxs-lookup"><span data-stu-id="46820-247">Advanced technology</span></span>

<span data-ttu-id="46820-248">Azure RTOS NetX, şunları içeren gelişmiş bir teknolojidir:</span><span class="sxs-lookup"><span data-stu-id="46820-248">Azure RTOS NetX is advanced technology that includes:</span></span>

* <span data-ttu-id="46820-249">Piconet™ mimarisi</span><span class="sxs-lookup"><span data-stu-id="46820-249">Piconet™ architecture</span></span>
* <span data-ttu-id="46820-250">Otomatik ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="46820-250">automatic scaling</span></span>
* <span data-ttu-id="46820-251">UDP Fast-Path teknolojisi™</span><span class="sxs-lookup"><span data-stu-id="46820-251">UDP Fast-Path Technology™</span></span>
* <span data-ttu-id="46820-252">esnek paket yönetimi</span><span class="sxs-lookup"><span data-stu-id="46820-252">flexible packet management</span></span>
* <span data-ttu-id="46820-253">sıfır-API ve uygulama kopyalama</span><span class="sxs-lookup"><span data-stu-id="46820-253">zero-copy API and implementation</span></span>
* <span data-ttu-id="46820-254">çok sayfalı destek</span><span class="sxs-lookup"><span data-stu-id="46820-254">multihomed support</span></span>
* <span data-ttu-id="46820-255">Tüm askıya alma sırasında isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="46820-255">optional timeout on all suspension</span></span>
* <span data-ttu-id="46820-256">Statik yönlendirme desteği</span><span class="sxs-lookup"><span data-stu-id="46820-256">static routing support</span></span>
* <span data-ttu-id="46820-257">Azure RTOS TraceX sistem analizi desteği</span><span class="sxs-lookup"><span data-stu-id="46820-257">Azure RTOS TraceX system analysis support</span></span>

## <a name="fastest-time-to-market"></a><span data-ttu-id="46820-258">En hızlı pazar süresi</span><span class="sxs-lookup"><span data-stu-id="46820-258">Fastest time-to-market</span></span>

<span data-ttu-id="46820-259">Azure RTOS NetX 'i yüklemek, öğrenmek, kullanmak, hata ayıklamak, doğrulamak, onaylamak ve sürdürmek kolaydır.</span><span class="sxs-lookup"><span data-stu-id="46820-259">Azure RTOS NetX is easy to install, learn, use, debug, verify, certify, and maintain.</span></span> <span data-ttu-id="46820-260">Sonuç olarak, Azure RTOS NetX, Broadcom, Gainspan ve benzeri birçok SoCs dahil olmak üzere katıştırılmış IoT cihazları için en popüler TCP/IP yığınlarından biridir.</span><span class="sxs-lookup"><span data-stu-id="46820-260">As a result, Azure RTOS NetX is one of the most popular TCP/IP stacks for embedded IoT devices, including many SoCs from Broadcom, Gainspan, and so forth.</span></span> <span data-ttu-id="46820-261">Tutarlı Pazar süresi avantajımız, şu şekilde oluşturulmuştur:</span><span class="sxs-lookup"><span data-stu-id="46820-261">Our consistent time-to-market advantage is built on:</span></span>

* <span data-ttu-id="46820-262">kalite belgeleri: lütfen [Azure RTOS NetX Kullanıcı Kılavuzumuzu](about-this-guide.md) gözden geçirin ve kendiniz görün!</span><span class="sxs-lookup"><span data-stu-id="46820-262">quality documentation – please review our [Azure RTOS NetX User Guide](about-this-guide.md) and see for yourself!</span></span>
* <span data-ttu-id="46820-263">Tüm kaynak kodu kullanılabilirliği</span><span class="sxs-lookup"><span data-stu-id="46820-263">complete source code availability</span></span>
* <span data-ttu-id="46820-264">kullanımı kolay API</span><span class="sxs-lookup"><span data-stu-id="46820-264">easy-to-use API</span></span>
* <span data-ttu-id="46820-265">kapsamlı ve gelişmiş özellik kümesi</span><span class="sxs-lookup"><span data-stu-id="46820-265">comprehensive and advanced feature set</span></span>

## <a name="one-simple-license"></a><span data-ttu-id="46820-266">Tek bir basit lisans</span><span class="sxs-lookup"><span data-stu-id="46820-266">One Simple License</span></span>

<span data-ttu-id="46820-267">Önceden lisanslanmış cihazlara dağıtıldığında, diğer tüm cihazların basit bir yıllık lisansa sahip olması için, kaynak kodu ve test lisansları için ücret ve maliyet kullanımı maliyeti yoktur.</span><span class="sxs-lookup"><span data-stu-id="46820-267">There is no cost to use and test the source code and no cost for production licenses when deployed to pre-licensed devices, all other devices need a simple annual license.</span></span>

## <a name="full-highest-quality-source-code"></a><span data-ttu-id="46820-268">Tam, en yüksek kaliteli kaynak kodu</span><span class="sxs-lookup"><span data-stu-id="46820-268">Full, highest-quality source code</span></span>

<span data-ttu-id="46820-269">Yıl boyunca, Azure RTOS NetX kaynak kodu, çubuğun kalitesini ve anlamayı kolay bir şekilde ayarladı.</span><span class="sxs-lookup"><span data-stu-id="46820-269">Throughout the years, Azure RTOS NetX source code has set the bar in quality and ease of understanding.</span></span> <span data-ttu-id="46820-270">Ayrıca, dosya başına bir işleve sahip olma kuralı, kolay kaynak gezintisi için sağlar.</span><span class="sxs-lookup"><span data-stu-id="46820-270">In addition, the convention of having one function per file provides for easy source navigation.</span></span>

## <a name="supports-most-popular-architectures"></a><span data-ttu-id="46820-271">Popüler mimarilerin çoğunu destekler</span><span class="sxs-lookup"><span data-stu-id="46820-271">Supports most popular architectures</span></span>

<span data-ttu-id="46820-272">Azure RTOS NetX, en popüler 32/64 bit mikro işlemciler, kullanıma hazır, tam olarak sınanmış ve aşağıdaki gelişmiş mimariler dahil olmak üzere tam olarak desteklenmiş şekilde çalışır:</span><span class="sxs-lookup"><span data-stu-id="46820-272">Azure RTOS NetX runs on most popular 32/64-bit microprocessors, out-of-the-box, fully tested and fully supported, including the following advanced architectures:</span></span>

<span data-ttu-id="46820-273">**Analog cihazlar**: parça, BlackICE, CM4xx</span><span class="sxs-lookup"><span data-stu-id="46820-273">**Analog Devices**: SHARC, Blackfin, CM4xx</span></span>

<span data-ttu-id="46820-274">**Andes Core**: RISC-V</span><span class="sxs-lookup"><span data-stu-id="46820-274">**Andes Core**: RISC-V</span></span>

<span data-ttu-id="46820-275">**Ambiqmicro**: Apollo MCUs</span><span class="sxs-lookup"><span data-stu-id="46820-275">**Ambiqmicro**: Apollo MCUs</span></span>

<span data-ttu-id="46820-276">**ARM**: ARM7, ARM9, ARM11, Cortex-M0/m3/M4/M7/A15/a5/A7/A8/A9/A5X 64-bı/A7x 64-bit/R4/R5, TrustZone ARMv8-ı</span><span class="sxs-lookup"><span data-stu-id="46820-276">**ARM**: ARM7, ARM9, ARM11, Cortex-M0/M3/M4/M7/A15/A5/A7/A8/A9/A5x 64-bi/A7x 64-bit/R4/R5, TrustZone ARMv8-M</span></span>

<span data-ttu-id="46820-277">**Temposunda**: xtensa, elmas</span><span class="sxs-lookup"><span data-stu-id="46820-277">**Cadence**: Xtensa, Diamond</span></span>

<span data-ttu-id="46820-278">**Ceva**: PSoC, PSoC 4, PSoC 5, PSoC 6, FM0 +, FM3, MF4, Werwifi</span><span class="sxs-lookup"><span data-stu-id="46820-278">**CEVA**: PSoC, PSoC 4, PSoC 5, PSoC 6, FM0+, FM3, MF4, WICED WiFi</span></span>

<span data-ttu-id="46820-279">**Cypress**: RISC-V</span><span class="sxs-lookup"><span data-stu-id="46820-279">**Cypress**: RISC-V</span></span>

<span data-ttu-id="46820-280">**Ensilica**: ESI-RISC</span><span class="sxs-lookup"><span data-stu-id="46820-280">**EnSilica**: eSi-RISC</span></span>

<span data-ttu-id="46820-281">**Infineon**: XMC1000, XMC4000, kanore</span><span class="sxs-lookup"><span data-stu-id="46820-281">**Infineon**: XMC1000, XMC4000, TriCore</span></span>

<span data-ttu-id="46820-282">**Intel; Intel FPGA**: x36/Pentium, XScale, NIOS II, Cyclone, varış a 10</span><span class="sxs-lookup"><span data-stu-id="46820-282">**Intel; Intel FPGA**: x36/Pentium, XScale, NIOS II, Cyclone, Arria 10</span></span>

<span data-ttu-id="46820-283">**Mikro yonga**: AVR32, ARM7, ARM9, Cortex-M3/M4/M7, SAM3/4/7/9/A/C/D/E/G/L/ZF, PIC24/PIC32</span><span class="sxs-lookup"><span data-stu-id="46820-283">**Microchip**: AVR32, ARM7, ARM9, Cortex-M3/M4/M7, SAM3/4/7/9/A/C/D/E/G/L/SV, PIC24/PIC32</span></span>

<span data-ttu-id="46820-284">**Mikro yarı**: RISC-V</span><span class="sxs-lookup"><span data-stu-id="46820-284">**Microsemi**: RISC-V</span></span>

<span data-ttu-id="46820-285">**NXP**: LPC, ARM7, ARM9, PowerPC, 68 K, I.MX, ColdFire, Kinetis Cortex-M3/M4</span><span class="sxs-lookup"><span data-stu-id="46820-285">**NXP**: LPC, ARM7, ARM9, PowerPC, 68 K, i.MX, ColdFire, Kinetis Cortex-M3/M4</span></span>

<span data-ttu-id="46820-286">**Renesas**: SH, HS, v850, RX, Rz, Synergy</span><span class="sxs-lookup"><span data-stu-id="46820-286">**Renesas**: SH, HS, V850, RX, RZ, Synergy</span></span>

<span data-ttu-id="46820-287">**Silicon Labs**: EFM32</span><span class="sxs-lookup"><span data-stu-id="46820-287">**Silicon Labs**: EFM32</span></span>

<span data-ttu-id="46820-288">**Synopsys**: Arc 600, 700, Arc Em, Arc HS</span><span class="sxs-lookup"><span data-stu-id="46820-288">**Synopsys**: ARC 600, 700, ARC EM, ARC HS</span></span>

<span data-ttu-id="46820-289">**St**: STM32, ARM7, ARM9, Cortex-M3/M4/M7</span><span class="sxs-lookup"><span data-stu-id="46820-289">**ST**: STM32, ARM7, ARM9, Cortex-M3/M4/M7</span></span>

<span data-ttu-id="46820-290">**TL**: C5xxx, C6xxx, Stellardo, Sitara, Tiva-C</span><span class="sxs-lookup"><span data-stu-id="46820-290">**Tl**: C5xxx, C6xxx, Stellaris, Sitara, Tiva-C</span></span>

<span data-ttu-id="46820-291">**Dalga bilgi işlem**: MIPS32 4k, 24 K, 34 k, 1004 k, ver 5k, mikro Aptiv, ınteraptiv, Proaptiv, M-class</span><span class="sxs-lookup"><span data-stu-id="46820-291">**Wave Computing**: MIPS32 4K, 24 K, 34 K, 1004 K, MIPS64 5K, microAptiv, interAptiv, proAptiv, M-Class</span></span>

<span data-ttu-id="46820-292">**Xilinx**: mikro Blaze, PowerPC 405, zynq, Zynq UltraSCALE</span><span class="sxs-lookup"><span data-stu-id="46820-292">**Xilinx**: MicroBlaze, PowerPC 405, ZYNQ, ZYNQ UltraSCALE</span></span>

<span data-ttu-id="46820-293">*Listelenen tüm zamanlama ve boyut rakamları tahminlerdir ve geliştirme platformunuzun farklı olabilir.*</span><span class="sxs-lookup"><span data-stu-id="46820-293">*All timing and size figures listed are estimates and may be different on your development platform.*</span></span>
