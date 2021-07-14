---
title: NetX Azure RTOS anlama
description: Azure RTOS NetX, Azure RTOS ThreadX ile tamamen tümleştirilmiş ve desteklenen tüm işlemciler için kullanılabilen, TCP/IP protokolü standartlarının yüksek performanslı bir uygulamasıdır.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: 63fd212249da6154926684f9bc844d2c2a78e84e
ms.sourcegitcommit: dbbec3ba6a7eb6097c7888b235c433a2efd6e5b9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/14/2021
ms.locfileid: "113754854"
---
# <a name="overview-of-azure-rtos-netx"></a><span data-ttu-id="bae6e-103">Azure RTOS NetX'e genel bakış</span><span class="sxs-lookup"><span data-stu-id="bae6e-103">Overview of Azure RTOS NetX</span></span>

<span data-ttu-id="bae6e-104">Azure RTOS NetX, özellikle derin katıştırılmış, gerçek zamanlı ve IoT uygulamaları için tasarlanmış bir endüstriyel sınıf TCP/IP IPv4 tümleşik ağ yığınıdır.</span><span class="sxs-lookup"><span data-stu-id="bae6e-104">Azure RTOS NetX is an industrial grade TCP/IP IPv4 embedded network stack, designed specifically for deeply embedded, real-time, and IoT applications.</span></span> <span data-ttu-id="bae6e-105">Azure RTOS NetX, Microsoft'un özgün IPv4 ağ yığınıdır ve temel olarak bir ağ Azure RTOS.</span><span class="sxs-lookup"><span data-stu-id="bae6e-105">Azure RTOS NetX is Microsoft's original IPv4 network stack, and is essentially a subset of Azure RTOS.</span></span> <span data-ttu-id="bae6e-106">NetX; IPv4, TCP ve UDP gibi temel ağ protokollerinin yanı sıra ek, üst düzey eklenti protokollerinin eksiksiz bir paketini içeren katıştırılmış uygulamalar sağlar.</span><span class="sxs-lookup"><span data-stu-id="bae6e-106">NetX provides embedded applications with core network protocols such as IPv4, TCP, and UDP as well as a complete suite of additional, higher-level add-on protocols.</span></span> <span data-ttu-id="bae6e-107">Küçük bir ayak izi, hızlı yürütme ve üstün kullanım kolaylığı, NetX Azure RTOS en zorlu tümleşik IoT uygulamaları için ideal bir seçenektir.</span><span class="sxs-lookup"><span data-stu-id="bae6e-107">A small footprint, fast execution, and superior ease-of-use make Azure RTOS NetX an ideal choice for the most demanding embedded IoT applications.</span></span>

## <a name="api-protocols"></a><span data-ttu-id="bae6e-108">API protokolleri</span><span class="sxs-lookup"><span data-stu-id="bae6e-108">API protocols</span></span>
<span data-ttu-id="bae6e-109">Azure RTOS NetX aşağıdakiler için destek sağlar.</span><span class="sxs-lookup"><span data-stu-id="bae6e-109">Azure RTOS NetX provides support for the following.</span></span>

### <a name="telnet"></a><span data-ttu-id="bae6e-110">Telnet</span><span class="sxs-lookup"><span data-stu-id="bae6e-110">TELNET</span></span>

* <span data-ttu-id="bae6e-111">En az 0,5 KB ve 0,3 KB RAM ayak izi.</span><span class="sxs-lookup"><span data-stu-id="bae6e-111">Minimal 0.5 KB and 0.3 KB RAM footprint.</span></span>
* <span data-ttu-id="bae6e-112">İstemci ve sunucu desteği.</span><span class="sxs-lookup"><span data-stu-id="bae6e-112">Client and server support.</span></span>

### <a name="auto-ip"></a><span data-ttu-id="bae6e-113">Otomatik IP</span><span class="sxs-lookup"><span data-stu-id="bae6e-113">Auto IP</span></span>

* <span data-ttu-id="bae6e-114">Otomatik IPv4 adres ataması.</span><span class="sxs-lookup"><span data-stu-id="bae6e-114">Automatic IPv4 address assignment.</span></span>
* <span data-ttu-id="bae6e-115">En az 1,2 KB, 300 bayt RAM.</span><span class="sxs-lookup"><span data-stu-id="bae6e-115">Minimal 1.2 KB, 300 bytes of RAM.</span></span>

### <a name="http---hypertext-transfer-protocolhttp"></a><span data-ttu-id="bae6e-116">HTTP - Köprü Metni Aktarım Protokolü (HTTP)</span><span class="sxs-lookup"><span data-stu-id="bae6e-116">HTTP - Hypertext Transfer Protocol(HTTP)</span></span>

* <span data-ttu-id="bae6e-117">En az 2,8 KB ile 4,8KBFLASH, 0,4 KB ile 1,0 KB RAM ayak izi.</span><span class="sxs-lookup"><span data-stu-id="bae6e-117">Minimal 2.8 KB to 4.8KBFLASH, 0.4 KB to 1.0 KB RAM footprint.</span></span>
* <span data-ttu-id="bae6e-118">İstemci ve sunucu desteği.</span><span class="sxs-lookup"><span data-stu-id="bae6e-118">Client and server support.</span></span>

### <a name="smtp---simple-mail-transfer-protocol-smtp"></a><span data-ttu-id="bae6e-119">SMTP - Basit Posta Aktarım Protokolü (SMTP)</span><span class="sxs-lookup"><span data-stu-id="bae6e-119">SMTP - Simple Mail Transfer Protocol (SMTP)</span></span>

* <span data-ttu-id="bae6e-120">En az 4,1 KB ve 0,6 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="bae6e-120">Minimal 4.1 KB and 0.6 KB RAM footprint</span></span>
* <span data-ttu-id="bae6e-121">İstemci desteği</span><span class="sxs-lookup"><span data-stu-id="bae6e-121">Client support</span></span>

### <a name="dhcp---dynamic-host-configuration-protocol-dhcp"></a><span data-ttu-id="bae6e-122">DHCP - Dinamik Ana Bilgisayar Yapılandırma Protokolü (DHCP)</span><span class="sxs-lookup"><span data-stu-id="bae6e-122">DHCP - Dynamic Host Configuration Protocol (DHCP)</span></span>

* <span data-ttu-id="bae6e-123">En az 3,6 KB ile 4,6 KB FLASH, 2,7 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="bae6e-123">Minimal 3.6 KB to 4.6 KB FLASH, 2.7 KB RAM footprint</span></span>
* <span data-ttu-id="bae6e-124">İstemci ve sunucu desteği</span><span class="sxs-lookup"><span data-stu-id="bae6e-124">Client and server support</span></span>
* <span data-ttu-id="bae6e-125">IPv4 desteği</span><span class="sxs-lookup"><span data-stu-id="bae6e-125">IPv4 support</span></span>

### <a name="p0p3---post-office-protocol-version-3-pop3"></a><span data-ttu-id="bae6e-126">P0P3 - Office Protokolü Sürüm 3 (POP3) Sonrası</span><span class="sxs-lookup"><span data-stu-id="bae6e-126">P0P3 - Post Office Protocol Version 3 (POP3)</span></span>

* <span data-ttu-id="bae6e-127">En az 8,1 KB ve 1,4 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="bae6e-127">Minimal 8.1 KB and 1.4 KB RAM footprint</span></span>
* <span data-ttu-id="bae6e-128">İstemci desteği</span><span class="sxs-lookup"><span data-stu-id="bae6e-128">Client support</span></span>

### <a name="snmp---simple-network-management-protocol-snmp"></a><span data-ttu-id="bae6e-129">SNMP - Basit Ağ Yönetimi Protokolü (SNMP)</span><span class="sxs-lookup"><span data-stu-id="bae6e-129">SNMP - Simple Network Management Protocol (SNMP)</span></span>

* <span data-ttu-id="bae6e-130">En az 10,9 KB ve 2,6 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="bae6e-130">Minimal 10.9 KB and 2.6 KB RAM footprint</span></span>
* <span data-ttu-id="bae6e-131">VI, V2 ve V3 için aracı desteği</span><span class="sxs-lookup"><span data-stu-id="bae6e-131">Agent support for VI, V2, and V3</span></span>

### <a name="ftp-tftp---file-transfer-protocol-ftp-trivial-file-transfer-protocol-tftp"></a><span data-ttu-id="bae6e-132">FTP, TFTP - Dosya Aktarım Protokolü (FTP), Önemsiz Dosya Aktarım Protokolü (TFTP)</span><span class="sxs-lookup"><span data-stu-id="bae6e-132">FTP, TFTP - File Transfer Protocol (FTP), Trivial File Transfer Protocol (TFTP)</span></span>

* <span data-ttu-id="bae6e-133">FTP En Az 1,8 KB ile 7,2KBFLASH, 0,6 KB ile 2,1 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="bae6e-133">FTP Minimal 1.8 KB to 7.2KBFLASH, 0.6 KB to 2.1 KB RAM footprint</span></span>
* <span data-ttu-id="bae6e-134">TFTP Minimal 1,7 KB ile 2,4KBFLASH, 0,3 KB ile 1,8 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="bae6e-134">TFTP Minimal 1.7 KB to 2.4KBFLASH, 0.3 KB to 1.8 KB RAM footprint</span></span>
* <span data-ttu-id="bae6e-135">İstemci ve sunucu desteği</span><span class="sxs-lookup"><span data-stu-id="bae6e-135">Client and server support</span></span>

### <a name="ppp---polnt-to-point-protocol-ppp"></a><span data-ttu-id="bae6e-136">PPP - Polnt-To-PoInt Protokolü (PPP)</span><span class="sxs-lookup"><span data-stu-id="bae6e-136">PPP - Polnt-to-PoInt Protocol (PPP)</span></span>

* <span data-ttu-id="bae6e-137">En az 7,1 KB ve 3,8 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="bae6e-137">Minimal 7.1 KB and 3.8 KB RAM footprint</span></span>
* <span data-ttu-id="bae6e-138">Güvenilir ve güvenilir.</span><span class="sxs-lookup"><span data-stu-id="bae6e-138">Dependable and reliable.</span></span>

### <a name="sntp---simple-network-time-protocol-sntp"></a><span data-ttu-id="bae6e-139">SNTP - Basit Ağ Zamanı Protokolü (SNTP)</span><span class="sxs-lookup"><span data-stu-id="bae6e-139">SNTP - Simple Network Time Protocol (SNTP)</span></span>

* <span data-ttu-id="bae6e-140">En az 4 KB ve 0,5 KB RAM</span><span class="sxs-lookup"><span data-stu-id="bae6e-140">Minimal 4 KB and 0.5 KB RAM</span></span>
* <span data-ttu-id="bae6e-141">İstemci desteği</span><span class="sxs-lookup"><span data-stu-id="bae6e-141">Client support</span></span>

### <a name="azure-rtos-netx-api"></a><span data-ttu-id="bae6e-142">Azure RTOS NetX API'si</span><span class="sxs-lookup"><span data-stu-id="bae6e-142">Azure RTOS NetX API</span></span>

* <span data-ttu-id="bae6e-143">Hızlı, sıfır kopya API'si uygulaması</span><span class="sxs-lookup"><span data-stu-id="bae6e-143">Fast, zero-copy API implementation</span></span>
* <span data-ttu-id="bae6e-144">Eski yuva kodunun taşınabilirliği için isteğe bağlı BSD katmanı</span><span class="sxs-lookup"><span data-stu-id="bae6e-144">Optional BSD layer for porting legacy socket code</span></span>

### <a name="igmp---internet-group-management-protocol-igmp"></a><span data-ttu-id="bae6e-145">IGMP - İnternet Grup Yönetimi Protokolü (IGMP)</span><span class="sxs-lookup"><span data-stu-id="bae6e-145">IGMP - Internet Group Management Protocol (IGMP)</span></span>

* <span data-ttu-id="bae6e-146">En az 2,5 KB FLASH</span><span class="sxs-lookup"><span data-stu-id="bae6e-146">Minimal 2.5 KB FLASH</span></span>
* <span data-ttu-id="bae6e-147">IPv4 çok noktaya yayın grubu desteği</span><span class="sxs-lookup"><span data-stu-id="bae6e-147">IPv4 multicast group support</span></span>
* <span data-ttu-id="bae6e-148">I HIP IxANVL Doğrulandı</span><span class="sxs-lookup"><span data-stu-id="bae6e-148">IXIA IxANVL Validated</span></span>
* <span data-ttu-id="bae6e-149">İsteğe bağlı IGMP istatistikleri</span><span class="sxs-lookup"><span data-stu-id="bae6e-149">Optional IGMP statistics</span></span>
* <span data-ttu-id="bae6e-150">Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme</span><span class="sxs-lookup"><span data-stu-id="bae6e-150">System-level Trace via Azure RTOS TraceX</span></span>

### <a name="udp---user-datagram-protocol-udp"></a><span data-ttu-id="bae6e-151">UDP - Kullanıcı Veri Birimi Protokolü (UDP)</span><span class="sxs-lookup"><span data-stu-id="bae6e-151">UDP - User Datagram Protocol (UDP)</span></span>

* <span data-ttu-id="bae6e-152">Yuva başına en az 2,5 KB FLASH, 124 yuva bayt RAM</span><span class="sxs-lookup"><span data-stu-id="bae6e-152">Minimal 2.5 KB FLASH, 124 sockets bytes of RAM per socket</span></span>
* <span data-ttu-id="bae6e-153">Hızlı, kabloya yakın TCP paketi işleme:</span><span class="sxs-lookup"><span data-stu-id="bae6e-153">Fast, near wirespeed TCP packet processing:</span></span>
* <span data-ttu-id="bae6e-154">100 Mb/sn Ethernet üzerinde RX 95 Mb/sn, MCU @100MHz , %14 MCU Kullanımı</span><span class="sxs-lookup"><span data-stu-id="bae6e-154">RX 95 Mbps on 100 Mbps Ethernet, MCU @100MHz, 14% MCU Utilization</span></span>
* <span data-ttu-id="bae6e-155">100 Mb/sn Ethernet üzerinde TX 94 Mb/sn, MCU @100MHz , %10 MCU Kullanımı</span><span class="sxs-lookup"><span data-stu-id="bae6e-155">TX 94 Mbps on 100 Mbps Ethernet, MCU @100MHz, 10% MCU Utilization</span></span>
* <span data-ttu-id="bae6e-156">UDP Hızlı Yolu™ teknolojisi</span><span class="sxs-lookup"><span data-stu-id="bae6e-156">UDP Fast Path™ technology</span></span>
* <span data-ttu-id="bae6e-157">UDP sayısıyla ilgili sınır yok</span><span class="sxs-lookup"><span data-stu-id="bae6e-157">No limits on the number of UDP</span></span>
* <span data-ttu-id="bae6e-158">I HIP IxANVL Doğrulandı</span><span class="sxs-lookup"><span data-stu-id="bae6e-158">IXIA IxANVL Validated</span></span>
* <span data-ttu-id="bae6e-159">Yuva almada isteğe bağlı askıya alma</span><span class="sxs-lookup"><span data-stu-id="bae6e-159">Optional suspension on socket receive</span></span>
* <span data-ttu-id="bae6e-160">Tüm askıya almada isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="bae6e-160">Optional timeout on all suspension</span></span>
* <span data-ttu-id="bae6e-161">İsteğe bağlı UDP istatistikleri</span><span class="sxs-lookup"><span data-stu-id="bae6e-161">Optional UDP statistics</span></span>
* <span data-ttu-id="bae6e-162">Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme</span><span class="sxs-lookup"><span data-stu-id="bae6e-162">System-level Trace via Azure RTOS TraceX</span></span>

### <a name="tcp---transmission-control-protocol-tcp"></a><span data-ttu-id="bae6e-163">TCP - İletim Denetimi Protokolü (TCP)</span><span class="sxs-lookup"><span data-stu-id="bae6e-163">TCP - Transmission Control Protocol (TCP)</span></span>

* <span data-ttu-id="bae6e-164">En az 10,5K8 ile 12,5 KB FLASH, yuva başına 280 bayt RAM</span><span class="sxs-lookup"><span data-stu-id="bae6e-164">Minimal 10.5K8 to 12.5 KB FLASH, 280 bytes of RAM per socket</span></span>
* <span data-ttu-id="bae6e-165">Hızlı, neredeyse wlrespeed TCP paket işleme:</span><span class="sxs-lookup"><span data-stu-id="bae6e-165">Fast, near wlrespeed TCP packet processing:</span></span>
* <span data-ttu-id="bae6e-166">100 Mb/sn Ethernet üzerinde RX 93 Mb/sn, MCU @100MHz , %20 MCU Kullanımı</span><span class="sxs-lookup"><span data-stu-id="bae6e-166">RX 93 Mbps on 100 Mbps Ethernet, MCU @100MHz, 20% MCU Utilization</span></span>
* <span data-ttu-id="bae6e-167">100 Mb/sn Ethernet üzerinde TX 94 Mb/sn, MCU @100MHz , %27 MCU Kullanımı</span><span class="sxs-lookup"><span data-stu-id="bae6e-167">TX 94 Mbps on 100 Mbps Ethernet, MCU @100MHz, 27% MCU Utilization</span></span>
* <span data-ttu-id="bae6e-168">Güvenilir bağlantı</span><span class="sxs-lookup"><span data-stu-id="bae6e-168">Reliable connection</span></span>
* <span data-ttu-id="bae6e-169">TCP yuvalarının sayısıyla ilgili sınır yok</span><span class="sxs-lookup"><span data-stu-id="bae6e-169">No limits on the number of TCP sockets</span></span>
* <span data-ttu-id="bae6e-170">I HIP IxANVL Doğrulandı</span><span class="sxs-lookup"><span data-stu-id="bae6e-170">IXIA IxANVL Validated</span></span>
* <span data-ttu-id="bae6e-171">Yuva alma/iletmede isteğe bağlı askıya alma</span><span class="sxs-lookup"><span data-stu-id="bae6e-171">Optional suspension on socket receive/transmit</span></span>
* <span data-ttu-id="bae6e-172">Tüm askıya almada isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="bae6e-172">Optional timeout on all suspension</span></span>
* <span data-ttu-id="bae6e-173">İsteğe bağlı TCP istatistikleri</span><span class="sxs-lookup"><span data-stu-id="bae6e-173">Optional TCP statistics</span></span>
* <span data-ttu-id="bae6e-174">Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme</span><span class="sxs-lookup"><span data-stu-id="bae6e-174">System-level Trace via Azure RTOS TraceX</span></span>

### <a name="icmp---internet-control-message-protocol-icmp"></a><span data-ttu-id="bae6e-175">ICMP - İnternet Denetim İletisi Protokolü (ICMP)</span><span class="sxs-lookup"><span data-stu-id="bae6e-175">ICMP - Internet Control Message Protocol (ICMP)</span></span>

* <span data-ttu-id="bae6e-176">En az 2,5 KB FLASH</span><span class="sxs-lookup"><span data-stu-id="bae6e-176">Minimal 2.5 KB FLASH</span></span>
* <span data-ttu-id="bae6e-177">IPv4 desteği</span><span class="sxs-lookup"><span data-stu-id="bae6e-177">IPv4 support</span></span>
* <span data-ttu-id="bae6e-178">I HIP IxANVL Doğrulandı</span><span class="sxs-lookup"><span data-stu-id="bae6e-178">IXIA IxANVL Validated</span></span>
* <span data-ttu-id="bae6e-179">Ping isteği ve ping yanıtı</span><span class="sxs-lookup"><span data-stu-id="bae6e-179">Ping request and ping response</span></span>
* <span data-ttu-id="bae6e-180">Ping istekleri üzerinde isteğe bağlı iş parçacığının askıya alınması</span><span class="sxs-lookup"><span data-stu-id="bae6e-180">Optional thread suspension on ping requests</span></span>
* <span data-ttu-id="bae6e-181">Tüm askıya almada isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="bae6e-181">Optional timeout on all suspension</span></span>
* <span data-ttu-id="bae6e-182">İsteğe bağlı ICMP istatistikleri</span><span class="sxs-lookup"><span data-stu-id="bae6e-182">Optional ICMP statistics</span></span>
* <span data-ttu-id="bae6e-183">Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme</span><span class="sxs-lookup"><span data-stu-id="bae6e-183">System-level Trace via Azure RTOS TraceX</span></span>

### <a name="ipv4---internet-protocol-ip"></a><span data-ttu-id="bae6e-184">IPv4 - İnternet Protokolü (IP)</span><span class="sxs-lookup"><span data-stu-id="bae6e-184">IPv4 - Internet Protocol (IP)</span></span>

* <span data-ttu-id="bae6e-185">En az 3,5 KB ile 8,5 KB FLASH, 2 KB ile 3 KB RAM ayak izi.</span><span class="sxs-lookup"><span data-stu-id="bae6e-185">Minimal 3.5 KB to 8.5 KB FLASH, 2 KB to 3 KB RAM footprint.</span></span>
* <span data-ttu-id="bae6e-186">Piconet™ Mimarisi.</span><span class="sxs-lookup"><span data-stu-id="bae6e-186">Piconet™ Architecture.</span></span>
* <span data-ttu-id="bae6e-187">Hızlı, kablolara yakın performans.</span><span class="sxs-lookup"><span data-stu-id="bae6e-187">Fast, near wirespeed performance.</span></span>
* <span data-ttu-id="bae6e-188">Birden çok arabirim desteği.</span><span class="sxs-lookup"><span data-stu-id="bae6e-188">Multiple interface support.</span></span>
* <span data-ttu-id="bae6e-189">Çok girişli destek.</span><span class="sxs-lookup"><span data-stu-id="bae6e-189">Multi-homed support.</span></span>
* <span data-ttu-id="bae6e-190">Statik yönlendirme desteği.</span><span class="sxs-lookup"><span data-stu-id="bae6e-190">Static routing support.</span></span>
* <span data-ttu-id="bae6e-191">IP parçalanması/yeniden değerlendirme desteği.</span><span class="sxs-lookup"><span data-stu-id="bae6e-191">IP fragmentation/reassembly support.</span></span>
* <span data-ttu-id="bae6e-192">IPv4 Desteği.</span><span class="sxs-lookup"><span data-stu-id="bae6e-192">IPv4 Support.</span></span>
* <span data-ttu-id="bae6e-193">I HIP IxANVL Doğrulandı.</span><span class="sxs-lookup"><span data-stu-id="bae6e-193">IXIA IxANVL Validated.</span></span>
* <span data-ttu-id="bae6e-194">Aşama II Hazır Logo Sertifikası.</span><span class="sxs-lookup"><span data-stu-id="bae6e-194">Phase II Ready Logo Certification.</span></span>
* <span data-ttu-id="bae6e-195">İsteğe bağlı IP istatistikleri.</span><span class="sxs-lookup"><span data-stu-id="bae6e-195">Optional IP statistics.</span></span>
* <span data-ttu-id="bae6e-196">İyi tanımlanmış, sezgisel fiziksel katman sürücü arabirimi.</span><span class="sxs-lookup"><span data-stu-id="bae6e-196">Well defined, intuitive physical layer driver interface.</span></span>
* <span data-ttu-id="bae6e-197">Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme.</span><span class="sxs-lookup"><span data-stu-id="bae6e-197">System-level Trace via Azure RTOS TraceX.</span></span>

### <a name="arprarp---address-resolution-protocol-arp-reverse-address-resolution-protocol-rarp"></a><span data-ttu-id="bae6e-198">ARP/RARP - Adres Çözümleme Protokolü (ARP), Ters Adres Çözümleme Protokolü (RARP)</span><span class="sxs-lookup"><span data-stu-id="bae6e-198">ARP/RARP - Address Resolution Protocol (ARP), Reverse Address Resolution Protocol (RARP)</span></span>

* <span data-ttu-id="bae6e-199">En az 1,7 KB FLASH, RAM boyutu.</span><span class="sxs-lookup"><span data-stu-id="bae6e-199">Minimal 1.7 KB FLASH, RAM size.</span></span>
* <span data-ttu-id="bae6e-200">32 blt IPv4 ve 48 blt MAC adreslerinin dinamik çözünürlüğü.</span><span class="sxs-lookup"><span data-stu-id="bae6e-200">Dynamic resolution of 32-blt IPv4 and 48-blt MAC addresses.</span></span>
* <span data-ttu-id="bae6e-201">I HIP IxANVL Doğrulandı.</span><span class="sxs-lookup"><span data-stu-id="bae6e-201">IXIA IxANVL Validated.</span></span>
* <span data-ttu-id="bae6e-202">Esnek, kullanıcı tanımlı ARP önbelleği.</span><span class="sxs-lookup"><span data-stu-id="bae6e-202">Flexible, user-defined ARP cache.</span></span>
* <span data-ttu-id="bae6e-203">Gratuitous ARP desteği.</span><span class="sxs-lookup"><span data-stu-id="bae6e-203">Gratuitous ARP support.</span></span>
* <span data-ttu-id="bae6e-204">Uygulama tarafından belirlenen isteğe bağlı ARP/RARP istatistikleri.</span><span class="sxs-lookup"><span data-stu-id="bae6e-204">Optional ARP/RARP statistics determined by application.</span></span>
* <span data-ttu-id="bae6e-205">Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme.</span><span class="sxs-lookup"><span data-stu-id="bae6e-205">System-level Trace via Azure RTOS TraceX.</span></span>

### <a name="ethernet-wifi-bluetooth-le-154-etc"></a><span data-ttu-id="bae6e-206">ETHERNET, WiFi, BLUETOOTH LE, 15.4 vb.</span><span class="sxs-lookup"><span data-stu-id="bae6e-206">ETHERNET, WiFi, BLUETOOTH LE, 15.4, etc.</span></span>

## <a name="interoperability-verification"></a><span data-ttu-id="bae6e-207">Birlikte çalışabilirlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="bae6e-207">Interoperability verification</span></span>

<span data-ttu-id="bae6e-208">Azure RTOS NetX, RFC standartlarına uygundur ve çoğu satıcının cihazlarında tam birlikte çalışabilirlik sunar.</span><span class="sxs-lookup"><span data-stu-id="bae6e-208">Azure RTOS NetX conforms to RFC standards and offers complete interoperability with devices from most vendors.</span></span> <span data-ttu-id="bae6e-209">Azure RTOS NetX, NetX çekirdek TCP/IP protokolü uygulaması için sektör standardı IxANVL (Otomatik Ağ Doğrulama Kitaplığı) Azure RTOS kullanır.</span><span class="sxs-lookup"><span data-stu-id="bae6e-209">Azure RTOS NetX also utilizes the industry standard IxANVL (Automated Network Validation Library) for the Azure RTOS NetX core TCP/IP protocol implementation.</span></span>

## <a name="advanced-technology"></a><span data-ttu-id="bae6e-210">Gelişmiş teknoloji</span><span class="sxs-lookup"><span data-stu-id="bae6e-210">Advanced technology</span></span>

<span data-ttu-id="bae6e-211">Azure RTOS NetX, aşağıdakilere sahip gelişmiş bir teknolojidir.</span><span class="sxs-lookup"><span data-stu-id="bae6e-211">Azure RTOS NetX is advanced technology that includes the following.</span></span>
* <span data-ttu-id="bae6e-212">Piconet™ mimari.</span><span class="sxs-lookup"><span data-stu-id="bae6e-212">Piconet™ architecture.</span></span>
* <span data-ttu-id="bae6e-213">Otomatik ölçeklendirme.</span><span class="sxs-lookup"><span data-stu-id="bae6e-213">Automatic scaling.</span></span>
* <span data-ttu-id="bae6e-214">UDP Fast-Path Technology™.</span><span class="sxs-lookup"><span data-stu-id="bae6e-214">UDP Fast-Path Technology™.</span></span>
* <span data-ttu-id="bae6e-215">Esnek paket yönetimi.</span><span class="sxs-lookup"><span data-stu-id="bae6e-215">Flexible packet management.</span></span>
* <span data-ttu-id="bae6e-216">Sıfır kopya API'si ve uygulaması.</span><span class="sxs-lookup"><span data-stu-id="bae6e-216">Zero-copy API and implementation.</span></span>
* <span data-ttu-id="bae6e-217">Çok girişli destek.</span><span class="sxs-lookup"><span data-stu-id="bae6e-217">Multi-homed support.</span></span>
* <span data-ttu-id="bae6e-218">Tüm askıya almada isteğe bağlı zaman aşımı.</span><span class="sxs-lookup"><span data-stu-id="bae6e-218">Optional timeout on all suspension.</span></span>
* <span data-ttu-id="bae6e-219">Statik yönlendirme desteği.</span><span class="sxs-lookup"><span data-stu-id="bae6e-219">Static routing support.</span></span>
* <span data-ttu-id="bae6e-220">Azure RTOS TraceX sistem analizi desteği.</span><span class="sxs-lookup"><span data-stu-id="bae6e-220">Azure RTOS TraceX system analysis support.</span></span>
