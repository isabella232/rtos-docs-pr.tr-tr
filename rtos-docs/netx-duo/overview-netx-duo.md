---
title: Azure RTOS NetX Duo 'i anlama
description: Azure RTOS NetX Duo, özellikle de gömülü gerçek zamanlı ve IoT uygulamaları için özel olarak tasarlanan bir gelişmiş, endüstriyel sınıf TCP/IP ağ yığını.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: 2339da391e52b437a2111ae439cccf41e038bdcf
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826926"
---
# <a name="overview-of-azure-rtos-netx-duo"></a><span data-ttu-id="d69f0-103">Azure RTOS NetX Duo 'e genel bakış</span><span class="sxs-lookup"><span data-stu-id="d69f0-103">Overview of Azure RTOS NetX Duo</span></span>

<span data-ttu-id="d69f0-104">Azure RTOS NetX Duo katıştırılmış TCP/IP ağ yığını, özellikle de daha fazla gömülü, gerçek zamanlı ve IoT uygulamaları için tasarlanan Microsoft 'un gelişmiş, endüstriyel sınıf ikili IPv4 ve IPv6 TCP/IP ağ yığınıdır.</span><span class="sxs-lookup"><span data-stu-id="d69f0-104">Azure RTOS NetX Duo embedded TCP/IP network stack is Microsoft's advanced, industrial grade dual IPv4 and IPv6 TCP/IP network stack that is designed specifically for deeply embedded, real-time, and IoT applications.</span></span> <span data-ttu-id="d69f0-105">NetX Duo, IPv4, IPv6, TCP ve UDP gibi çekirdek ağ protokollerine ve ek ve daha üst düzey eklenti protokollerinin eksiksiz bir paketini içeren katıştırılmış uygulamalar sağlar.</span><span class="sxs-lookup"><span data-stu-id="d69f0-105">NetX Duo provides embedded applications with core network protocols such as IPv4, IPv6, TCP, and UDP as well as a complete suite of additional, higher-level add-on protocols.</span></span> <span data-ttu-id="d69f0-106">Azure RTOS NetX Duo, Azure RTOS NetX güvenli IPSec ve Azure RTOS NetX güvenli SSL/TLS/DTLS dahil ek eklenti güvenlik ürünleri aracılığıyla güvenlik sağlar.</span><span class="sxs-lookup"><span data-stu-id="d69f0-106">Azure RTOS NetX Duo offers security via additional add-on security products, including Azure RTOS NetX Secure IPsec and Azure RTOS NetX Secure SSL/TLS/DTLS.</span></span> <span data-ttu-id="d69f0-107">Bunun hepsi küçük bir ayak izi, Hızlı yürütme ve üstün kullanım kolaylığıyla Azure RTOS NetX Duo, en zorlu ekli IoT uygulamalarına yönelik ideal seçenektir.</span><span class="sxs-lookup"><span data-stu-id="d69f0-107">All of this combined with an small footprint, fast execution, and superior ease-of-use make Azure RTOS NetX Duo the ideal choice for the most demanding embedded IoT applications.</span></span>

## <a name="api-protocols"></a><span data-ttu-id="d69f0-108">API protokolleri</span><span class="sxs-lookup"><span data-stu-id="d69f0-108">API protocols</span></span>

### <a name="mqtt"></a><span data-ttu-id="d69f0-109">MQTT</span><span class="sxs-lookup"><span data-stu-id="d69f0-109">MQTT</span></span>

* <span data-ttu-id="d69f0-110">Mesajlaşma kuyruğu telemetri aktarımı (MQTT)</span><span class="sxs-lookup"><span data-stu-id="d69f0-110">Messaging Queue Telemetry Transport (MQTT)</span></span>
* <span data-ttu-id="d69f0-111">En az 2,7 KB FLASH</span><span class="sxs-lookup"><span data-stu-id="d69f0-111">Minimal 2.7 KB FLASH</span></span>
* <span data-ttu-id="d69f0-112">Sezgisel MQTT API 'Leri: *nx_mqtt_*\*</span><span class="sxs-lookup"><span data-stu-id="d69f0-112">Intuitive MQTT APIs: *nx_mqtt_*\*</span></span>

### <a name="auto-ip"></a><span data-ttu-id="d69f0-113">Otomatik IP</span><span class="sxs-lookup"><span data-stu-id="d69f0-113">Auto IP</span></span>

* <span data-ttu-id="d69f0-114">Otomatik IPv4 adresi ataması</span><span class="sxs-lookup"><span data-stu-id="d69f0-114">Automatic IPv4 address assignment</span></span>
* <span data-ttu-id="d69f0-115">En az 1,2 KB, 300 bayt RAM</span><span class="sxs-lookup"><span data-stu-id="d69f0-115">Minimal 1.2 KB, 300 bytes of RAM</span></span>
* <span data-ttu-id="d69f0-116">Sezgisel Oto IP API 'Leri *: \* nx_autoip_*</span><span class="sxs-lookup"><span data-stu-id="d69f0-116">Intuitive AutoIP APIs: *nx_autoip_\**</span></span>

### <a name="http-https"></a><span data-ttu-id="d69f0-117">HTTP, HTTPS</span><span class="sxs-lookup"><span data-stu-id="d69f0-117">HTTP, HTTPS</span></span>

#### <a name="http-10"></a><span data-ttu-id="d69f0-118">HTTP 1,0</span><span class="sxs-lookup"><span data-stu-id="d69f0-118">HTTP 1.0</span></span>

* <span data-ttu-id="d69f0-119">Köprü Metni Aktarım Protokolü (HTTP)</span><span class="sxs-lookup"><span data-stu-id="d69f0-119">Hypertext Transfer Protocol(HTTP)</span></span>
* <span data-ttu-id="d69f0-120">Minimum 2,8 KB-4,8 KB, FLASH/0,4 KB ile 1,0 KB arasında</span><span class="sxs-lookup"><span data-stu-id="d69f0-120">Minimal 2.8 KB to 4.8 KB FLASH / 0.4 KB to 1.0 KB RAM</span></span>
* <span data-ttu-id="d69f0-121">İstemci ve sunucu desteği</span><span class="sxs-lookup"><span data-stu-id="d69f0-121">Client and server support</span></span>
* <span data-ttu-id="d69f0-122">Sezgisel API 'Ler *: \* nx_http_*</span><span class="sxs-lookup"><span data-stu-id="d69f0-122">Intuitive APIs: *nx_http_\**</span></span>

#### <a name="httphttps-11"></a><span data-ttu-id="d69f0-123">HTTP/HTTPS 1,1</span><span class="sxs-lookup"><span data-stu-id="d69f0-123">HTTP/HTTPS 1.1</span></span>

* <span data-ttu-id="d69f0-124">Köprü Metni Aktarım Protokolü (HTTP)</span><span class="sxs-lookup"><span data-stu-id="d69f0-124">Hypertext Transfer Protocol(HTTP)</span></span>
* <span data-ttu-id="d69f0-125">Minimum 3,0 KB-9,5 KB FLASH/0,5 KB-2 KB RAM</span><span class="sxs-lookup"><span data-stu-id="d69f0-125">Minimal 3.0 KB to 9.5 KB FLASH / 0.5 KB to 2 KB RAM</span></span>
* <span data-ttu-id="d69f0-126">İstemci ve sunucu desteği</span><span class="sxs-lookup"><span data-stu-id="d69f0-126">Client and server support</span></span>
* <span data-ttu-id="d69f0-127">Birden çok gelen istemci oturumu</span><span class="sxs-lookup"><span data-stu-id="d69f0-127">Multiple incoming client sessions</span></span>
* <span data-ttu-id="d69f0-128">Düz metin ve şifreli HTTPS</span><span class="sxs-lookup"><span data-stu-id="d69f0-128">Plain text and encrypted HTTPS</span></span>
* <span data-ttu-id="d69f0-129">Kalıcı bağlantı desteği</span><span class="sxs-lookup"><span data-stu-id="d69f0-129">Persistent connection support</span></span>
* <span data-ttu-id="d69f0-130">Çok parçalı dosya yükleme</span><span class="sxs-lookup"><span data-stu-id="d69f0-130">Multipart file upload</span></span>
* <span data-ttu-id="d69f0-131">Azure RTOS NetX güvenli TLS ile tam olarak tümleşik</span><span class="sxs-lookup"><span data-stu-id="d69f0-131">Fully integrated with Azure RTOS NetX Secure TLS</span></span>
* <span data-ttu-id="d69f0-132">Sezgisel API 'Ler *: \* nx_web_http*</span><span class="sxs-lookup"><span data-stu-id="d69f0-132">Intuitive APIs: *nx_web_http\**</span></span>

### <a name="smtp"></a><span data-ttu-id="d69f0-133">SMTP</span><span class="sxs-lookup"><span data-stu-id="d69f0-133">SMTP</span></span>

* <span data-ttu-id="d69f0-134">Basit küçük/küçük Aktarım Protokolü (SMTP)</span><span class="sxs-lookup"><span data-stu-id="d69f0-134">Simple Mall Transfer Protocol (SMTP)</span></span>
* <span data-ttu-id="d69f0-135">En az 4,1 KB ve 0,6 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="d69f0-135">Minimal 4.1 KB and 0.6 KB RAM footprint</span></span>
* <span data-ttu-id="d69f0-136">İstemci desteği</span><span class="sxs-lookup"><span data-stu-id="d69f0-136">Client support</span></span>
* <span data-ttu-id="d69f0-137">Sezgisel SMTP API 'Leri *: \* nx_smtp_*</span><span class="sxs-lookup"><span data-stu-id="d69f0-137">Intuitive SMTP APIs: *nx_smtp_\**</span></span>

### <a name="dhcp"></a><span data-ttu-id="d69f0-138">DHCP</span><span class="sxs-lookup"><span data-stu-id="d69f0-138">DHCP</span></span>

* <span data-ttu-id="d69f0-139">Dinamik Ana Bilgisayar Yapılandırma Protokolü (DHCP)</span><span class="sxs-lookup"><span data-stu-id="d69f0-139">Dynamic Host Configuration Protocol (DHCP)</span></span>
* <span data-ttu-id="d69f0-140">Minimum 3,6 KB-4,6 KB FLASH, 2,7 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="d69f0-140">Minimal 3.6 KB to 4.6 KB FLASH, 2.7 KB RAM footprint</span></span>
* <span data-ttu-id="d69f0-141">İstemci ve sunucu desteği</span><span class="sxs-lookup"><span data-stu-id="d69f0-141">Client and server support</span></span>
* <span data-ttu-id="d69f0-142">IPv4 ve IPv6 desteği</span><span class="sxs-lookup"><span data-stu-id="d69f0-142">IPv4 and IPv6 support</span></span>
* <span data-ttu-id="d69f0-143">Sezgisel DHCP API 'Leri *: \* nx_dhcp_*</span><span class="sxs-lookup"><span data-stu-id="d69f0-143">Intuitive DHCP APIs: *nx_dhcp_\**</span></span>

### <a name="nat"></a><span data-ttu-id="d69f0-144">NAT</span><span class="sxs-lookup"><span data-stu-id="d69f0-144">NAT</span></span>

* <span data-ttu-id="d69f0-145">Ağ Adresi Çevirisi (NAT)</span><span class="sxs-lookup"><span data-stu-id="d69f0-145">Network Address Translation (NAT)</span></span>
* <span data-ttu-id="d69f0-146">Minimum 3,5 K6 ve 0,6 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="d69f0-146">Minimal 3.5K6 and 0.6 KB RAM footprint</span></span>
* <span data-ttu-id="d69f0-147">IPv4 adresi desteği</span><span class="sxs-lookup"><span data-stu-id="d69f0-147">IPv4 address support</span></span>
* <span data-ttu-id="d69f0-148">Sezgisel NAT API 'Leri *: \* nx_nat_*</span><span class="sxs-lookup"><span data-stu-id="d69f0-148">Intuitive NAT APIs: *nx_nat_\**</span></span>
* <span data-ttu-id="d69f0-149">NAT yalnızca Azure RTOS NetX Duo ile kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="d69f0-149">NAT is only available with Azure RTOS NetX Duo</span></span>

### <a name="snmp"></a><span data-ttu-id="d69f0-150">SNMP</span><span class="sxs-lookup"><span data-stu-id="d69f0-150">SNMP</span></span>

* <span data-ttu-id="d69f0-151">Basit Ağ Yönetim Protokolü (SNMP)</span><span class="sxs-lookup"><span data-stu-id="d69f0-151">Simple Network Management Protocol (SNMP)</span></span>
* <span data-ttu-id="d69f0-152">En az 10,9 KB ve 2,6 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="d69f0-152">Minimal 10.9 KB and 2.6 KB RAM footprint</span></span>
* <span data-ttu-id="d69f0-153">VI, v2 ve v3 için aracı desteği</span><span class="sxs-lookup"><span data-stu-id="d69f0-153">Agent support for VI, V2, and V3</span></span>
* <span data-ttu-id="d69f0-154">Sezgisel SNMP API 'Leri *: \* nx_snmp_*</span><span class="sxs-lookup"><span data-stu-id="d69f0-154">Intuitive SNMP APIs: *nx_snmp_\**</span></span>

### <a name="dns-mdns-dns-sd"></a><span data-ttu-id="d69f0-155">DNS, mDNS, DNS-SD</span><span class="sxs-lookup"><span data-stu-id="d69f0-155">DNS, mDNS, DNS-SD</span></span>

* <span data-ttu-id="d69f0-156">Etki Alanı Adı Sistemi (DNS)</span><span class="sxs-lookup"><span data-stu-id="d69f0-156">Domain Name System (DNS)</span></span>
* <span data-ttu-id="d69f0-157">Çok noktaya yayın etki alanı adı sistemi (mDNS)</span><span class="sxs-lookup"><span data-stu-id="d69f0-157">Multicast Domain Name System (mDNS)</span></span>
* <span data-ttu-id="d69f0-158">DNS tabanlı hizmet bulma (DNS-SD)</span><span class="sxs-lookup"><span data-stu-id="d69f0-158">DNS-based service discovery (DNS-SD)</span></span>
* <span data-ttu-id="d69f0-159">DNS en az 2,4 KB-3 KB FLASH, 1 KB RAM ayak</span><span class="sxs-lookup"><span data-stu-id="d69f0-159">DNS Minimal 2.4 KB to 3 KB FLASH, 1 KB RAM footprint</span></span>
* <span data-ttu-id="d69f0-160">İstemci desteği</span><span class="sxs-lookup"><span data-stu-id="d69f0-160">Client support</span></span>
* <span data-ttu-id="d69f0-161">Sezgisel API 'Ler *: \* nx_dns_*</span><span class="sxs-lookup"><span data-stu-id="d69f0-161">Intuitive APIs: *nx_dns_\**</span></span>
* <span data-ttu-id="d69f0-162">mDNS ve DNS-SD yalnızca Azure RTOS NetX Duo ile kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="d69f0-162">mDNS and DNS-SD are only available with Azure RTOS NetX Duo</span></span>

### <a name="p0p3"></a><span data-ttu-id="d69f0-163">P0P3</span><span class="sxs-lookup"><span data-stu-id="d69f0-163">P0P3</span></span>

* <span data-ttu-id="d69f0-164">Postane Protokolü sürüm 3 (POP3)</span><span class="sxs-lookup"><span data-stu-id="d69f0-164">Post Office Protocol Version 3 (POP3)</span></span>
* <span data-ttu-id="d69f0-165">En az 8,1 KB ve 1,4 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="d69f0-165">Minimal 8.1 KB and 1.4 KB RAM footprint</span></span>
* <span data-ttu-id="d69f0-166">İstemci desteği</span><span class="sxs-lookup"><span data-stu-id="d69f0-166">Client support</span></span>
* <span data-ttu-id="d69f0-167">Sezgisel P0P3 API 'Leri *: \* nx_pop3_*</span><span class="sxs-lookup"><span data-stu-id="d69f0-167">Intuitive P0P3 APIs: *nx_pop3_\**</span></span>

### <a name="telnet"></a><span data-ttu-id="d69f0-168">Sun</span><span class="sxs-lookup"><span data-stu-id="d69f0-168">TELNET</span></span>

* <span data-ttu-id="d69f0-169">En az 0,5 KB ve 0,3 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="d69f0-169">Minimal 0.5 KB and 0.3 KB RAM footprint</span></span>
* <span data-ttu-id="d69f0-170">İstemci ve sunucu desteği</span><span class="sxs-lookup"><span data-stu-id="d69f0-170">Client and server support</span></span>
* <span data-ttu-id="d69f0-171">Sezgisel Telnet API 'Leri *: \* nx_telnet_*</span><span class="sxs-lookup"><span data-stu-id="d69f0-171">Intuitive Telnet APIs: *nx_telnet_\**</span></span>

### <a name="ftp-tftp"></a><span data-ttu-id="d69f0-172">FTP, TFTP</span><span class="sxs-lookup"><span data-stu-id="d69f0-172">FTP, TFTP</span></span>

* <span data-ttu-id="d69f0-173">Dosya Aktarım Protokolü (FTP)</span><span class="sxs-lookup"><span data-stu-id="d69f0-173">File Transfer Protocol (FTP)</span></span>
* <span data-ttu-id="d69f0-174">Önemsiz Dosya Aktarım İletişim Kuralı (TFTP)</span><span class="sxs-lookup"><span data-stu-id="d69f0-174">Trivial File Transfer Protocol (TFTP)</span></span>
* <span data-ttu-id="d69f0-175">FTP en az 1,8 KB-7,2 KB FLASH, 0,6 KB ile 2,1 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="d69f0-175">FTP Minimal 1.8 KB to 7.2 KB FLASH, 0.6 KB to 2.1 KB RAM footprint</span></span>
* <span data-ttu-id="d69f0-176">TFTP en az 1,7 KB-2,4 KB FLASH, 0,3 KB ile 1,8 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="d69f0-176">TFTP Minimal 1.7 KB to 2.4 KB FLASH, 0.3 KB to 1.8 KB RAM footprint</span></span>
* <span data-ttu-id="d69f0-177">İstemci ve sunucu desteği</span><span class="sxs-lookup"><span data-stu-id="d69f0-177">Client and server support</span></span>
* <span data-ttu-id="d69f0-178">Sezgisel FTP ve TFTP API 'Leri *: \* nx_ftp_* veya *nx_tftp_ \**</span><span class="sxs-lookup"><span data-stu-id="d69f0-178">Intuitive FTP and TFTP APIs: *nx_ftp_\** or *nx_tftp_\**</span></span>

### <a name="ppp-pppoe"></a><span data-ttu-id="d69f0-179">PPP, PPPoE</span><span class="sxs-lookup"><span data-stu-id="d69f0-179">PPP, PPPoE</span></span>

* <span data-ttu-id="d69f0-180">POlNT noktadan noktaya Protokolü (PPP)</span><span class="sxs-lookup"><span data-stu-id="d69f0-180">Polnt-to-PoInt Protocol (PPP)</span></span>
* <span data-ttu-id="d69f0-181">Ethernet üzerinden Noktadan Noktaya Protokolü (PPPoE)</span><span class="sxs-lookup"><span data-stu-id="d69f0-181">Point-to-Point Protocol over Ethernet(PPPoE)</span></span>
* <span data-ttu-id="d69f0-182">En az 7,1 KB ve 3,8 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="d69f0-182">Minimal 7.1 KB and 3.8 KB RAM footprint</span></span>
* <span data-ttu-id="d69f0-183">Sezgisel PPP API 'Leri *: \* nx_ppp_*</span><span class="sxs-lookup"><span data-stu-id="d69f0-183">Intuitive PPP APIs: *nx_ppp_\**</span></span>

* <span data-ttu-id="d69f0-184">PPPoE yalnızca Azure RTOS NetX Duo ile kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="d69f0-184">PPPoE is only available with Azure RTOS NetX Duo</span></span>

### <a name="sntp"></a><span data-ttu-id="d69f0-185">SNTP</span><span class="sxs-lookup"><span data-stu-id="d69f0-185">SNTP</span></span>

* <span data-ttu-id="d69f0-186">Basit ağ zaman Protokolü (SNTP)</span><span class="sxs-lookup"><span data-stu-id="d69f0-186">Simple Network Time Protocol (SNTP)</span></span>
* <span data-ttu-id="d69f0-187">En az 4 KB ve 0,5 KB RAM</span><span class="sxs-lookup"><span data-stu-id="d69f0-187">Minimal 4 KB and 0.5 KB RAM</span></span>
* <span data-ttu-id="d69f0-188">İstemci desteği</span><span class="sxs-lookup"><span data-stu-id="d69f0-188">Client support</span></span>
* <span data-ttu-id="d69f0-189">Sezgisel SNTP API 'Leri *: \* nx_sntp_*</span><span class="sxs-lookup"><span data-stu-id="d69f0-189">Intuitive SNTP APIs: *nx_sntp_\**</span></span>

### <a name="azure-rtos-netx-duo-api"></a><span data-ttu-id="d69f0-190">Azure RTOS NetX Duo API 'SI</span><span class="sxs-lookup"><span data-stu-id="d69f0-190">Azure RTOS NetX Duo API</span></span>

* <span data-ttu-id="d69f0-191">Sezgisel ve tutarlı API</span><span class="sxs-lookup"><span data-stu-id="d69f0-191">Intuitive and consistent API</span></span>
* <span data-ttu-id="d69f0-192">İsim-fiil adlandırma kuralı</span><span class="sxs-lookup"><span data-stu-id="d69f0-192">Noun-verb naming convention</span></span>
* <span data-ttu-id="d69f0-193">Hızlı, sıfır kopya API 'SI uygulama</span><span class="sxs-lookup"><span data-stu-id="d69f0-193">Fast, zero-copy API implementation</span></span>
* <span data-ttu-id="d69f0-194">Azure RTOS NetX olarak kolayca tanımlanabilmesi için tüm API 'Lerin önde gelen <i>nx_ \*</i></span><span class="sxs-lookup"><span data-stu-id="d69f0-194">All APIs have leading <i>nx_\*</i> to easily identify as Azure RTOS NetX</span></span>
* <span data-ttu-id="d69f0-195">API 'Lerin engellenmesi isteğe bağlı iş parçacığı zaman aşımına uğradı</span><span class="sxs-lookup"><span data-stu-id="d69f0-195">Blocking APIs have optional thread timeout</span></span>
* <span data-ttu-id="d69f0-196">Daha fazla bilgi için bkz. [Azure RTOS NetX Duo Kullanıcı Kılavuzu](about-this-guide.md)</span><span class="sxs-lookup"><span data-stu-id="d69f0-196">See [Azure RTOS NetX Duo User Guide](about-this-guide.md) for more details</span></span>
* <span data-ttu-id="d69f0-197">Eski yuva kodu taşıma için isteğe bağlı BSD katmanı</span><span class="sxs-lookup"><span data-stu-id="d69f0-197">Optional BSD layer for porting legacy socket code</span></span>

### <a name="igmp"></a><span data-ttu-id="d69f0-198">IGMP</span><span class="sxs-lookup"><span data-stu-id="d69f0-198">IGMP</span></span>

* <span data-ttu-id="d69f0-199">Internet Grup Yönetimi Protokolü (IGMP)</span><span class="sxs-lookup"><span data-stu-id="d69f0-199">Internet Group Management Protocol (IGMP)</span></span>
* <span data-ttu-id="d69f0-200">En az 2,5 KB FLASH</span><span class="sxs-lookup"><span data-stu-id="d69f0-200">Minimal 2.5 KB FLASH</span></span>
* <span data-ttu-id="d69f0-201">IPv4 çok noktaya yayın grubu desteği</span><span class="sxs-lookup"><span data-stu-id="d69f0-201">IPv4 multicast group support</span></span>
* <span data-ttu-id="d69f0-202">IXIA IxANVL doğrulanan</span><span class="sxs-lookup"><span data-stu-id="d69f0-202">IXIA IxANVL validated</span></span>
* <span data-ttu-id="d69f0-203">İsteğe bağlı ıGMP istatistikleri</span><span class="sxs-lookup"><span data-stu-id="d69f0-203">Optional IGMP statistics</span></span>
* <span data-ttu-id="d69f0-204">Azure RTOS ThreadX aracılığıyla sistem düzeyinde izleme</span><span class="sxs-lookup"><span data-stu-id="d69f0-204">System-level trace via Azure RTOS ThreadX</span></span>
* <span data-ttu-id="d69f0-205">Sezgisel ıGMP API 'Leri *: \* nx_igmp_*</span><span class="sxs-lookup"><span data-stu-id="d69f0-205">Intuitive IGMP APIs: *nx_igmp_\**</span></span>

### <a name="azure-rtos-netx-secure-dtls"></a><span data-ttu-id="d69f0-206">Azure RTOS NetX güvenli DTLS</span><span class="sxs-lookup"><span data-stu-id="d69f0-206">Azure RTOS NetX Secure DTLS</span></span>

* <span data-ttu-id="d69f0-207">Veri birimi Aktarım Katmanı Güvenliği (DTLS) 1,0 ve 1,2</span><span class="sxs-lookup"><span data-stu-id="d69f0-207">Datagram Transport Layer Security (DTLS) 1.0 and 1.2</span></span>
* <span data-ttu-id="d69f0-208">En az 11 KB FLASH</span><span class="sxs-lookup"><span data-stu-id="d69f0-208">Minimal 11 KB FLASH</span></span>
* <span data-ttu-id="d69f0-209">Fast, Software RSA 2048-bit anahtar boyutu ~ 1-saniye @120MHz</span><span class="sxs-lookup"><span data-stu-id="d69f0-209">Fast, software RSA 2048-bit key size ~1-second @120MHz</span></span>
* <span data-ttu-id="d69f0-210">Kolaylaştırılmış X. 509.440 uygulama</span><span class="sxs-lookup"><span data-stu-id="d69f0-210">Streamlined X.509 Implementation</span></span>
* <span data-ttu-id="d69f0-211">Azure RTOS NetX Duo UDP yuvaları ile tam olarak tümleşik</span><span class="sxs-lookup"><span data-stu-id="d69f0-211">Fully integrated with Azure RTOS NetX Duo UDP sockets</span></span>
* <span data-ttu-id="d69f0-212">Donanım şifreleme desteği</span><span class="sxs-lookup"><span data-stu-id="d69f0-212">Hardware Crypto Support</span></span>
* <span data-ttu-id="d69f0-213">Yazılım şifreleme desteği: RSA (tüm anahtar boyutları), AES, DES/3DES, ECC, HMAC, MD5, SHA-1, SHA-2 (SHA-224, SHA-256, SHA-384, SHA-512)</span><span class="sxs-lookup"><span data-stu-id="d69f0-213">Software Crypto Support: RSA (all key sizes), AES, DES/3DES, ECC, HMAC, MD5, SHA-1, SHA-2 (SHA-224, SHA-256, SHA-384, SHA-512)</span></span>
* <span data-ttu-id="d69f0-214">P eğrileri 192/224/256/384/521 dahil olmak üzere ECDSA (imzalama) ve ECDH (şifreleme) ile Eliptik Eğri Şifreleme (ECC)</span><span class="sxs-lookup"><span data-stu-id="d69f0-214">Elliptic Curve Cryptography (ECC) with ECDSA (signing) and ECDH (encryption), including P-curves 192/224/256/384/521</span></span>
* <span data-ttu-id="d69f0-215">Şifrelenmiş anahtar desteği (donanıma bağımlı)</span><span class="sxs-lookup"><span data-stu-id="d69f0-215">Encrypted Key Support (hardware dependent)</span></span>

### <a name="azure-rtos-netx-secure-tls"></a><span data-ttu-id="d69f0-216">Azure RTOS NetX güvenli TLS</span><span class="sxs-lookup"><span data-stu-id="d69f0-216">Azure RTOS NetX Secure TLS</span></span>

* <span data-ttu-id="d69f0-217">Aktarım Katmanı Güvenliği (TLS) 1,0, 1,1 ve 1,2</span><span class="sxs-lookup"><span data-stu-id="d69f0-217">Transport Layer Security (TLS) 1.0, 1.1, and 1.2</span></span>
* <span data-ttu-id="d69f0-218">En az 8,8 KB FLASH</span><span class="sxs-lookup"><span data-stu-id="d69f0-218">Minimal 8.8 KB FLASH</span></span>
* <span data-ttu-id="d69f0-219">Fast, Software RSA 2048-bit anahtar boyutu ~ 1-saniye @120MHz</span><span class="sxs-lookup"><span data-stu-id="d69f0-219">Fast, software RSA 2048-bit key size ~1-second @120MHz</span></span>
* <span data-ttu-id="d69f0-220">Kolaylaştırılmış X. 509.440 uygulama</span><span class="sxs-lookup"><span data-stu-id="d69f0-220">Streamlined X.509 Implementation</span></span>
* <span data-ttu-id="d69f0-221">Azure RTOS NetX Duo TCP yuvaları ile tam olarak tümleşik</span><span class="sxs-lookup"><span data-stu-id="d69f0-221">Fully integrated with Azure RTOS NetX Duo TCP sockets</span></span>
* <span data-ttu-id="d69f0-222">Donanım şifreleme desteği</span><span class="sxs-lookup"><span data-stu-id="d69f0-222">Hardware Crypto Support</span></span>
* <span data-ttu-id="d69f0-223">Yazılım şifreleme desteği: RSA (tüm anahtar boyutları), AES, DES/3DES, ECC, HMAC, MD5, SHA-1, SHA-2 (SHA-224, SHA-256, SHA-384, SHA-512)</span><span class="sxs-lookup"><span data-stu-id="d69f0-223">Software Crypto Support: RSA (all key sizes), AES, DES/3DES, ECC, HMAC, MD5, SHA-1, SHA-2 (SHA-224, SHA-256, SHA-384, SHA-512)</span></span>
* <span data-ttu-id="d69f0-224">P eğrileri 192/224/256/384/521 dahil olmak üzere ECDSA (imzalama) ve ECDH (şifreleme) ile Eliptik Eğri Şifreleme (ECC)</span><span class="sxs-lookup"><span data-stu-id="d69f0-224">Elliptic Curve Cryptography (ECC) with ECDSA (signing) and ECDH (encryption), including P-curves 192/224/256/384/521</span></span>
* <span data-ttu-id="d69f0-225">Şifrelenmiş anahtar desteği (donanıma bağımlı)</span><span class="sxs-lookup"><span data-stu-id="d69f0-225">Encrypted Key Support (hardware dependent)</span></span>

### <a name="icmp"></a><span data-ttu-id="d69f0-226">ICMP</span><span class="sxs-lookup"><span data-stu-id="d69f0-226">ICMP</span></span>

* <span data-ttu-id="d69f0-227">Internet Denetim Iletisi Protokolü (ıCMP)</span><span class="sxs-lookup"><span data-stu-id="d69f0-227">Internet Control Message Protocol (ICMP)</span></span>
* <span data-ttu-id="d69f0-228">En az 2,5 KB FLASH</span><span class="sxs-lookup"><span data-stu-id="d69f0-228">Minimal 2.5 KB FLASH</span></span>
* <span data-ttu-id="d69f0-229">IPv4 ve IPv6 desteği</span><span class="sxs-lookup"><span data-stu-id="d69f0-229">IPv4 and IPv6 support</span></span>
* <span data-ttu-id="d69f0-230">IXIA IxANVL doğrulanan</span><span class="sxs-lookup"><span data-stu-id="d69f0-230">IXIA IxANVL validated</span></span>
* <span data-ttu-id="d69f0-231">Ping isteği ve ping yanıtı</span><span class="sxs-lookup"><span data-stu-id="d69f0-231">Ping request and ping response</span></span>
* <span data-ttu-id="d69f0-232">Ping isteklerinde isteğe bağlı iş parçacığı askıya alma</span><span class="sxs-lookup"><span data-stu-id="d69f0-232">Optional thread suspension on ping requests</span></span>
* <span data-ttu-id="d69f0-233">Tüm askıya alma sırasında isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="d69f0-233">Optional timeout on all suspension</span></span>
* <span data-ttu-id="d69f0-234">İsteğe bağlı ıCMP istatistikleri</span><span class="sxs-lookup"><span data-stu-id="d69f0-234">Optional ICMP statistics</span></span>
* <span data-ttu-id="d69f0-235">Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme</span><span class="sxs-lookup"><span data-stu-id="d69f0-235">System-level trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="d69f0-236">Sezgisel ıCMP API 'Leri *: \* nx_icmp_*</span><span class="sxs-lookup"><span data-stu-id="d69f0-236">Intuitive ICMP APIs: *nx_icmp_\**</span></span>

### <a name="udp"></a><span data-ttu-id="d69f0-237">UDP</span><span class="sxs-lookup"><span data-stu-id="d69f0-237">UDP</span></span>

* <span data-ttu-id="d69f0-238">Kullanıcı veri birimi Protokolü (UDP)</span><span class="sxs-lookup"><span data-stu-id="d69f0-238">User Datagram Protocol (UDP)</span></span>
* <span data-ttu-id="d69f0-239">Yuva başına en az 2,5 KB FLASH, 124 yuva baytı</span><span class="sxs-lookup"><span data-stu-id="d69f0-239">Minimal 2.5 KB FLASH, 124 sockets bytes of RAM per socket</span></span>
* <span data-ttu-id="d69f0-240">Hızlı, neredeyse wıned TCP paket işleme:</span><span class="sxs-lookup"><span data-stu-id="d69f0-240">Fast, near wirespeed TCP packet processing:</span></span>
    * <span data-ttu-id="d69f0-241">100 Mbps Ethernet, MCU @100MHz , 14% MCU kullanımı ÜZERINDE RX 95 Mbps</span><span class="sxs-lookup"><span data-stu-id="d69f0-241">RX 95 Mbps on 100 Mbps Ethernet, MCU @100MHz, 14% MCU utilization</span></span>
    * <span data-ttu-id="d69f0-242">TX 94 Mbps, 100 Mbps Ethernet, MCU @100MHz , 10% MCU kullanımı</span><span class="sxs-lookup"><span data-stu-id="d69f0-242">TX 94 Mbps on 100 Mbps Ethernet, MCU @100MHz, 10% MCU utilization</span></span>
* <span data-ttu-id="d69f0-243">UDP hızlı yol™ teknolojisi</span><span class="sxs-lookup"><span data-stu-id="d69f0-243">UDP Fast Path™ technology</span></span>
* <span data-ttu-id="d69f0-244">UDP sayısıyla ilgili sınır yok</span><span class="sxs-lookup"><span data-stu-id="d69f0-244">No limits on the number of UDP</span></span>
* <span data-ttu-id="d69f0-245">IXIA IxANVL doğrulanan</span><span class="sxs-lookup"><span data-stu-id="d69f0-245">IXIA IxANVL validated</span></span>
* <span data-ttu-id="d69f0-246">Yuva alma sırasında isteğe bağlı askıya alma</span><span class="sxs-lookup"><span data-stu-id="d69f0-246">Optional suspension on socket receive</span></span>
* <span data-ttu-id="d69f0-247">Tüm askıya alma sırasında isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="d69f0-247">Optional timeout on all suspension</span></span>
* <span data-ttu-id="d69f0-248">İsteğe bağlı UDP istatistikleri</span><span class="sxs-lookup"><span data-stu-id="d69f0-248">Optional UDP statistics</span></span>
* <span data-ttu-id="d69f0-249">Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme</span><span class="sxs-lookup"><span data-stu-id="d69f0-249">System-level trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="d69f0-250">Sezgisel UDP API 'Leri *: \* nx_udp_*</span><span class="sxs-lookup"><span data-stu-id="d69f0-250">Intuitive UDP APIs: *nx_udp_\**</span></span>

### <a name="tcp"></a><span data-ttu-id="d69f0-251">TCP</span><span class="sxs-lookup"><span data-stu-id="d69f0-251">TCP</span></span>

* <span data-ttu-id="d69f0-252">İletim Denetimi Protokolü (TCP)</span><span class="sxs-lookup"><span data-stu-id="d69f0-252">Transmission Control Protocol (TCP)</span></span>
* <span data-ttu-id="d69f0-253">Minimum 10,5 K8-12,5 KB FLASH, her yuva için 280 bayt RAM</span><span class="sxs-lookup"><span data-stu-id="d69f0-253">Minimal 10.5K8 to 12.5 KB FLASH, 280 bytes of RAM per socket</span></span>
* <span data-ttu-id="d69f0-254">Hızlı, neredeyse wlrespeed TCP paket işleme:</span><span class="sxs-lookup"><span data-stu-id="d69f0-254">Fast, near wlrespeed TCP packet processing:</span></span>
    * <span data-ttu-id="d69f0-255">100 Mbps Ethernet, MCU @100MHz , 20% MCU ÜZERINDE RX 93 Mbps</span><span class="sxs-lookup"><span data-stu-id="d69f0-255">RX 93 Mbps on 100 Mbps Ethernet, MCU @100MHz, 20% MCU utilization</span></span>
    * <span data-ttu-id="d69f0-256">TX 94 Mbps, 100 Mbps Ethernet, MCU @100MHz , 27% MCU kullanımı</span><span class="sxs-lookup"><span data-stu-id="d69f0-256">TX 94 Mbps on 100 Mbps Ethernet, MCU @100MHz, 27% MCU utilization</span></span>
* <span data-ttu-id="d69f0-257">Güvenilir bağlantı</span><span class="sxs-lookup"><span data-stu-id="d69f0-257">Reliable connection</span></span>
* <span data-ttu-id="d69f0-258">TCP yuvaları sayısında sınırsız</span><span class="sxs-lookup"><span data-stu-id="d69f0-258">No limits on the number of TCP sockets</span></span>
* <span data-ttu-id="d69f0-259">IXIA IxANVL doğrulanan</span><span class="sxs-lookup"><span data-stu-id="d69f0-259">IXIA IxANVL validated</span></span>
* <span data-ttu-id="d69f0-260">Yuva alma/iletme sırasında isteğe bağlı askıya alma</span><span class="sxs-lookup"><span data-stu-id="d69f0-260">Optional suspension on socket receive/transmit</span></span>
* <span data-ttu-id="d69f0-261">Tüm askıya alma sırasında isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="d69f0-261">Optional timeout on all suspension</span></span>
* <span data-ttu-id="d69f0-262">İsteğe bağlı TCP istatistikleri</span><span class="sxs-lookup"><span data-stu-id="d69f0-262">Optional TCP statistics</span></span>
* <span data-ttu-id="d69f0-263">Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme</span><span class="sxs-lookup"><span data-stu-id="d69f0-263">System-level trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="d69f0-264">Sezgisel TCP API 'Leri *: \* nx_tcp_*</span><span class="sxs-lookup"><span data-stu-id="d69f0-264">Intuitive TCP APIs: *nx_tcp_\**</span></span>

### <a name="arprarp"></a><span data-ttu-id="d69f0-265">ARP/RARP</span><span class="sxs-lookup"><span data-stu-id="d69f0-265">ARP/RARP</span></span>

* <span data-ttu-id="d69f0-266">Adres Çözümleme Protokolü (ARP)</span><span class="sxs-lookup"><span data-stu-id="d69f0-266">Address Resolution Protocol (ARP)</span></span>
* <span data-ttu-id="d69f0-267">Ters Adres Çözümleme Protokolü (RARP)</span><span class="sxs-lookup"><span data-stu-id="d69f0-267">Reverse Address Resolution Protocol (RARP)</span></span>
* <span data-ttu-id="d69f0-268">Minimum 1,7 KB FLASH, RAM boyutu</span><span class="sxs-lookup"><span data-stu-id="d69f0-268">Minimal 1.7 KB FLASH, RAM size</span></span>
* <span data-ttu-id="d69f0-269">32-blt IPv4 ve 48-blt MAC adreslerinin dinamik çözünürlüğü</span><span class="sxs-lookup"><span data-stu-id="d69f0-269">Dynamic resolution of 32-blt IPv4 and 48-blt MAC addresses</span></span>
* <span data-ttu-id="d69f0-270">IXIA IxANVL doğrulanan</span><span class="sxs-lookup"><span data-stu-id="d69f0-270">IXIA IxANVL validated</span></span>
* <span data-ttu-id="d69f0-271">Esnek, Kullanıcı tanımlı ARP önbelleği</span><span class="sxs-lookup"><span data-stu-id="d69f0-271">Flexible, user-defined ARP cache</span></span>
* <span data-ttu-id="d69f0-272">Gereksiz ARP desteği</span><span class="sxs-lookup"><span data-stu-id="d69f0-272">Gratuitous ARP support</span></span>
* <span data-ttu-id="d69f0-273">Uygulamaya göre belirlenen isteğe bağlı ARP/RARP istatistikleri</span><span class="sxs-lookup"><span data-stu-id="d69f0-273">Optional ARP/RARP statistics determined by application</span></span>
* <span data-ttu-id="d69f0-274">Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme</span><span class="sxs-lookup"><span data-stu-id="d69f0-274">System-level trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="d69f0-275">Sezgisel ARP/RARP API 'leri *: \* nx_arp_*, *nx_rarp_ \**</span><span class="sxs-lookup"><span data-stu-id="d69f0-275">Intuitive ARP/RARP APIs: *nx_arp_\**, *nx_rarp_\**</span></span>

### <a name="ipv4-amp-ipv6"></a><span data-ttu-id="d69f0-276">IPv4 &amp; IPv6</span><span class="sxs-lookup"><span data-stu-id="d69f0-276">IPv4 &amp; IPv6</span></span>

* <span data-ttu-id="d69f0-277">Internet Protokolü (IP)</span><span class="sxs-lookup"><span data-stu-id="d69f0-277">Internet Protocol (IP)</span></span>
* <span data-ttu-id="d69f0-278">Minimum 3,5 KB-8,5 KB FLASH, 2 KB-3 KB RAM ayak</span><span class="sxs-lookup"><span data-stu-id="d69f0-278">Minimal 3.5 KB to 8.5 KB FLASH, 2 KB to 3 KB RAM footprint</span></span>
* <span data-ttu-id="d69f0-279">Piconet™ mimarisi</span><span class="sxs-lookup"><span data-stu-id="d69f0-279">Piconet™ architecture</span></span>
* <span data-ttu-id="d69f0-280">Hızlı, neredeyse wafklu performans</span><span class="sxs-lookup"><span data-stu-id="d69f0-280">Fast, near wirespeed performance</span></span>
* <span data-ttu-id="d69f0-281">Birden çok arabirim desteği</span><span class="sxs-lookup"><span data-stu-id="d69f0-281">Multiple interface support</span></span>
* <span data-ttu-id="d69f0-282">Çok sayfalı destek</span><span class="sxs-lookup"><span data-stu-id="d69f0-282">Multihomed support</span></span>
* <span data-ttu-id="d69f0-283">Statik yönlendirme desteği</span><span class="sxs-lookup"><span data-stu-id="d69f0-283">Static routing support</span></span>
* <span data-ttu-id="d69f0-284">IP parçalama/yeniden birleştirme desteği</span><span class="sxs-lookup"><span data-stu-id="d69f0-284">IP fragmentation/reassembly support</span></span>
* <span data-ttu-id="d69f0-285">IPv4 ve IPv6 adresi desteği</span><span class="sxs-lookup"><span data-stu-id="d69f0-285">IPv4 and IPv6 address support</span></span>
* <span data-ttu-id="d69f0-286">IXIA IxANVL doğrulanan</span><span class="sxs-lookup"><span data-stu-id="d69f0-286">IXIA IxANVL validated</span></span>
* <span data-ttu-id="d69f0-287">Phase II IPv6 Ready Logo sertifikası</span><span class="sxs-lookup"><span data-stu-id="d69f0-287">Phase II IPv6 Ready Logo Certification</span></span>
* <span data-ttu-id="d69f0-288">İsteğe bağlı IP istatistikleri</span><span class="sxs-lookup"><span data-stu-id="d69f0-288">Optional IP statistics</span></span>
* <span data-ttu-id="d69f0-289">İyi tanımlanmış, sezgisel fiziksel katman sürücü arabirimi</span><span class="sxs-lookup"><span data-stu-id="d69f0-289">Well defined, intuitive physical layer driver interface</span></span>
* <span data-ttu-id="d69f0-290">Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme</span><span class="sxs-lookup"><span data-stu-id="d69f0-290">System-level trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="d69f0-291">Sezgisel IP katmanı API 'leri *: \* nx_ip_*, *nxd_ip_ \**, *nxd_ipv6_ \**</span><span class="sxs-lookup"><span data-stu-id="d69f0-291">Intuitive IP layer APIs: *nx_ip_\**, *nxd_ip_\**, *nxd_ipv6_\**</span></span>
* <span data-ttu-id="d69f0-292">TUV ve UL-ıEC 61508 SIL 4, ıEC 62304 Class C, ISO 26262 asıl D ve EN 50128 SW-SIL4 tarafından ön sertifikalı</span><span class="sxs-lookup"><span data-stu-id="d69f0-292">Pre-certified by TUV and UL to IEC 61508 SIL 4, IEC 62304 Class C, ISO 26262 ASIL D, and EN 50128 SW-SIL4</span></span>

### <a name="azure-rtos-netx-secure-ipsec"></a><span data-ttu-id="d69f0-293">Azure RTOS NetX güvenli ıPSEC</span><span class="sxs-lookup"><span data-stu-id="d69f0-293">Azure RTOS NetX Secure IPSEC</span></span>

* <span data-ttu-id="d69f0-294">Internet Protokolü güvenliği (ıPSEC)</span><span class="sxs-lookup"><span data-stu-id="d69f0-294">Internet Protocol Security (IPSEC)</span></span>
* <span data-ttu-id="d69f0-295">IP katmanı</span><span class="sxs-lookup"><span data-stu-id="d69f0-295">IP layer</span></span>
* <span data-ttu-id="d69f0-296">Donanım şifreleme desteği</span><span class="sxs-lookup"><span data-stu-id="d69f0-296">Hardware crypto support</span></span>
* <span data-ttu-id="d69f0-297">Aşağıdakiler dahil olmak üzere yazılım şifreleme desteği:</span><span class="sxs-lookup"><span data-stu-id="d69f0-297">Software crypto support, including:</span></span>
    * <span data-ttu-id="d69f0-298">DES, 3DES</span><span class="sxs-lookup"><span data-stu-id="d69f0-298">DES, 3DES</span></span>
    * <span data-ttu-id="d69f0-299">AES</span><span class="sxs-lookup"><span data-stu-id="d69f0-299">AES</span></span>
    * <span data-ttu-id="d69f0-300">HMAC-MD5</span><span class="sxs-lookup"><span data-stu-id="d69f0-300">HMAC-MD5</span></span>
    * <span data-ttu-id="d69f0-301">HMAC-SHA1</span><span class="sxs-lookup"><span data-stu-id="d69f0-301">HMAC-SHA1</span></span>
* <span data-ttu-id="d69f0-302">İnternet Anahtar Değişimi (ıKE) sürüm 2 desteği</span><span class="sxs-lookup"><span data-stu-id="d69f0-302">Internet Key Exchange (IKE) Version 2 support</span></span>
* <span data-ttu-id="d69f0-303">Sezgisel IPSec API 'Leri *: \* nx_ipsec_*</span><span class="sxs-lookup"><span data-stu-id="d69f0-303">Intuitive IPsec APIs: *nx_ipsec_\**</span></span>
* <span data-ttu-id="d69f0-304">IPSec yalnızca Azure RTOS NetX Duo ile kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="d69f0-304">IPsec is only available with Azure RTOS NetX Duo</span></span>

## <a name="small-footprint"></a><span data-ttu-id="d69f0-305">Küçük ayak izi</span><span class="sxs-lookup"><span data-stu-id="d69f0-305">Small-footprint</span></span>

<span data-ttu-id="d69f0-306">Azure RTOS NetX Duo, temel IP ve UDP desteği için 9 KB 'den 15 KB 'a kadar bir renetme sahiptir.</span><span class="sxs-lookup"><span data-stu-id="d69f0-306">Azure RTOS NetX Duo has a remarkably small footprint of 9 KB to 15 KB for basic IP and UDP support.</span></span> <span data-ttu-id="d69f0-307">TCP işlevselliği için 10 KB ila 13 KB 'lık yönerge alanı belleği gerekir.</span><span class="sxs-lookup"><span data-stu-id="d69f0-307">An additional 10 KB to 13 KB of instruction area memory is needed for TCP functionality.</span></span> <span data-ttu-id="d69f0-308">Azure RTOS NetX Duo RAM kullanımı, genellikle 2,6 KB 'den 3,6 KB 'ye ve uygulama tarafından tanımlanan paket havuzu belleğine göre değişir.</span><span class="sxs-lookup"><span data-stu-id="d69f0-308">Azure RTOS NetX Duo RAM usage typically ranges from 2.6 KB to 3.6 KB plus the packet pool memory, which is defined by the application.</span></span> <span data-ttu-id="d69f0-309">Azure RTOS ThreadX gibi Azure RTOS NetX Duo boyutu, uygulama tarafından kullanılan hizmetlere göre otomatik olarak ölçeklendirilir.</span><span class="sxs-lookup"><span data-stu-id="d69f0-309">Like Azure RTOS ThreadX, the size of Azure RTOS NetX Duo automatically scales based on the services used by the application.</span></span> <span data-ttu-id="d69f0-310">Bu, karmaşık yapılandırma ve derleme parametrelerine gerek duymayı neredeyse ortadan kaldırır, böylece geliştirici daha kolay hale getirir.</span><span class="sxs-lookup"><span data-stu-id="d69f0-310">This virtually eliminates the need for complicated configuration and build parameters, making things easier for the developer.</span></span>

## <a name="fast-execution"></a><span data-ttu-id="d69f0-311">Hızlı yürütme</span><span class="sxs-lookup"><span data-stu-id="d69f0-311">Fast execution</span></span>

<span data-ttu-id="d69f0-312">Azure RTOS NetX Duo, en hızlı olası performansı elde etmek için Azure RTOS ThreadX ile yüksek düzeyde tümleştirilmiş, sıfır kopya bir paket gönderme/alma uygulamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="d69f0-312">Azure RTOS NetX Duo provides a zero-copy packet send/receive implementation, highly integrated with Azure RTOS ThreadX, to achieve the fastest possible performance.</span></span> <span data-ttu-id="d69f0-313">Örneğin, Azure RTOS NetX Duo, genellikle işlemci döngülerinin yalnızca küçük bir yüzdesini kullanarak 80 MHz (veya daha az) bir işlemcide neredeyse Won 'a yönelik veri aktarımları elde edebilir.</span><span class="sxs-lookup"><span data-stu-id="d69f0-313">For example, Azure RTOS NetX Duo can typically achieve near wirespeed data transfers on an 80 MHz (or less) processor, while using only a small percentage of the processor cycles.</span></span>

## <a name="simple-easy-to-use"></a><span data-ttu-id="d69f0-314">Basit, kullanımı kolay</span><span class="sxs-lookup"><span data-stu-id="d69f0-314">Simple, easy-to-use</span></span>

<span data-ttu-id="d69f0-315">Azure RTOS NetX Duo API 'SI sezgisel, kolay ve yüksek işlevselliğe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="d69f0-315">The Azure RTOS NetX Duo API is intuitive, straightforward,  and highly functional.</span></span>

<span data-ttu-id="d69f0-316">API adları, diğer ağ ürünlerinde yaygın olarak kullanılan "alfabe dışı" veya son derece kısaltılmış adlarla değil, gerçek sözcüklerden oluşur.</span><span class="sxs-lookup"><span data-stu-id="d69f0-316">The API names are made of real words and not the “alphabet soup” or highly abbreviated names that are so common in other networking products.</span></span> <span data-ttu-id="d69f0-317">Tüm Azure RTOS NetX Duo API 'Lerinde önde gelen bir *nx_* ve bir ad fiil adlandırma kuralı takip ediyoruz.</span><span class="sxs-lookup"><span data-stu-id="d69f0-317">All Azure RTOS NetX Duo APIs have a leading *nx_* and follow a noun-verb naming convention.</span></span> <span data-ttu-id="d69f0-318">Ayrıca, API 'nin tamamında işlevsel bir tutarlılık vardır.</span><span class="sxs-lookup"><span data-stu-id="d69f0-318">Furthermore, there is a functional consistency throughout the API.</span></span> <span data-ttu-id="d69f0-319">Örneğin, askıya aldığı tüm API işlevlerinin aynı şekilde çalışan isteğe bağlı bir zaman aşımı vardır.</span><span class="sxs-lookup"><span data-stu-id="d69f0-319">For example, all API functions that suspend have an optional timeout that operates in an identical manner.</span></span>

<span data-ttu-id="d69f0-320">Eski uygulamalar için, Azure RTOS NetX Duo, ek bir BSD soketi uyumlu katman sağlar.</span><span class="sxs-lookup"><span data-stu-id="d69f0-320">For legacy applications, Azure RTOS NetX Duo offers an additional BSD socket compatible layer.</span></span> <span data-ttu-id="d69f0-321">Bu katman, geliştiricilerin büyük ağ uygulamalarını kolayca geçirmelerine yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="d69f0-321">This layer helps developers migrate large networking applications with ease.</span></span>

## <a name="safe-and-secure"></a><span data-ttu-id="d69f0-322">Güvenli ve güvenli</span><span class="sxs-lookup"><span data-stu-id="d69f0-322">Safe and secure</span></span>

<span data-ttu-id="d69f0-323">Azure RTOS NetX Duo güvenlidir.</span><span class="sxs-lookup"><span data-stu-id="d69f0-323">Azure RTOS NetX Duo is secure.</span></span> <span data-ttu-id="d69f0-324">Bu güvenlik, IPSec, SSL, TLS ve DTLS dahil eklenti güvenlik ürünleri aracılığıyla sağlanır.</span><span class="sxs-lookup"><span data-stu-id="d69f0-324">This security is provided through add-on security products, including IPsec, SSL, TLS, and DTLS.</span></span> <span data-ttu-id="d69f0-325">Ayrıca, uygulamanın Azure RTOS NetX Duo 'e yönelik tüm dış erişimlere yönelik tümüyle denetimi vardır ve güvenlik riski belirleme çok daha kolay hale getirir.</span><span class="sxs-lookup"><span data-stu-id="d69f0-325">Also, the application has complete control over all external access to Azure RTOS NetX Duo, making security risk determination much easier.</span></span>

<span data-ttu-id="d69f0-326">Microsoft Azure RTOS, OEM 'Lere iletişim sağlamak ve temel alınan MCU/MPU donanım koruma mekanizmalarını kullanarak kod ve veri yalıtımı oluşturmak için bileşenleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="d69f0-326">Microsoft Azure RTOS provides OEMs with components to secure communication and to create code and data isolation using underlying MCU/MPU hardware protection mechanisms.</span></span> <span data-ttu-id="d69f0-327">Cihazın, belirli kullanım durumuyla ilişkili gelişen güvenlik gereksinimlerini tam olarak karşıladığından emin olmak için, bu son olarak cihaz oluşturucunun sorumluluğundadır.</span><span class="sxs-lookup"><span data-stu-id="d69f0-327">It is ultimately the responsibility of the device builder to ensure the device fully meets the evolving security requirements associated with its specific use case.</span></span>

## <a name="pre-certified--by-tuv-and-ul-to-many-safety-standards"></a><span data-ttu-id="d69f0-328">TUV ve UL ile birçok güvenlik standartlarına ön sertifikalı</span><span class="sxs-lookup"><span data-stu-id="d69f0-328">Pre-certified  by TUV and UL to many safety standards</span></span>

<span data-ttu-id="d69f0-329">Azure RTOS NetX Duo, SGS-TUV Saar tarafından, ıEC-61508 SIL 4, ıEC-62304 SW Safety Class C, ISO 26262 asıl D ve EN 50128 'e göre güvenlik açısından kritik sistemlerde kullanılmak üzere sertifikalandırilmiştir.</span><span class="sxs-lookup"><span data-stu-id="d69f0-329">Azure RTOS NetX Duo has been certified by SGS-TUV  Saar for use in safety-critical systems, according to IEC-61508 SIL 4, IEC-62304 SW Safety Class C, ISO 26262 ASIL D and EN 50128.</span></span> <span data-ttu-id="d69f0-330">Sertifika, Azure RTOS NetX Duo 'un, "elektrik, elektronik ve programlanabilir elektronik güvenliği ile ilgili sistemlerin Işlevsel güvenliği" için, ıEC-61508, ıEC-62304, ISO 26262 ve 50128 EN yüksek güvenlik bütünlüğü düzeyleri için güvenlikle ilgili yazılımlar geliştirmede kullanılabileceğini onaylar.</span><span class="sxs-lookup"><span data-stu-id="d69f0-330">The certification confirms that Azure RTOS NetX Duo can be used in the development of safety-related software for the highest safety integrity levels of IEC-61508, IEC-62304, ISO 26262 and EN 50128 for the “Functional Safety of electrical, electronic, and programmable electronic safety-related systems.”</span></span> <span data-ttu-id="d69f0-331">Almanya 'nın SGS-Group ve TUV Saarland 'ın Birleşik bir tezi aracılığıyla oluşturulan SGS-TUV Saar, dünya çapındaki güvenlikle ilgili sistemler için eklenmiş yazılımları test etmek, denetlemek, doğrulamak ve sertifika almak için önde gelen acalacaklandırılan şirkete gelmiştir.</span><span class="sxs-lookup"><span data-stu-id="d69f0-331">SGS-TUV Saar, formed through a joint venture of Germany’s SGS-Group and TUV Saarland, has become the leading accredited, independent company for testing, auditing, verifying, and certifying embedded software for safety-related systems worldwide.</span></span> <span data-ttu-id="d69f0-332">Endüstriyel güvenlik standardı IEC 61508 ve bundan türetilmiş tüm standartlar, IEC-62304, ISO 26262 ve en 50128 dahil, elektrik, elektronik ve programlanabilir elektronik güvenliği ile ilgili tıbbi cihazların, işlem denetim sistemlerinin, endüstriyel makinelerin, otomobil ve demiryolu denetim sistemlerinin işlevsel güvenlik düzeyini güvence altına almak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d69f0-332">The industrial safety standard IEC 61508, and all standards that are derived from it, including IEC-62304, ISO 26262 and EN 50128, are used to assure the functional safety of electrical, electronic, and programmable electronic safety-related medical devices, process control systems, industrial machinery, automobiles and railway control systems.</span></span>

:::image type="content" source="media/overview-netx-duo/partener-logo-sgs-tuv-saar.png" alt-text="SGS-TUV sertifikası":::

<span data-ttu-id="d69f0-334">Azure RTOS NetX Duo, UL 60730-1 Ek H, CSA E60730-1 Ek H, ıEC 60730-1 Ek H, UL 60335-1 ek R, ıEC 60335-1 ek R ve, programlanabilir bileşenlerde yazılım için ul 1998 güvenlik standartları ile uyumlu bir şekilde tanınıyor.</span><span class="sxs-lookup"><span data-stu-id="d69f0-334">Azure RTOS NetX Duo has been recognized by UL for compliance with UL 60730-1 Annex H, CSA E60730-1 Annex H, IEC 60730-1 Annex H, UL 60335-1 Annex R, IEC 60335-1 Annex R, and UL 1998 safety standards for software in programmable components.</span></span> <span data-ttu-id="d69f0-335">UL, en fazla uzman sürmek güvenlik çözümleri sunan küresel, bağımsız bir güvenlik bilimi şirketidir. Bu, elektrik, yenilenebilir enerji ve Nanotechnology için genel olarak elektrik 'yi benimseme özelliğine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="d69f0-335">UL is a global, independent, safety-science company with more than a century of expertise innovating safety solutions, ranging from the public adoption of electricity to breakthroughs in sustainability, renewable energy, and nanotechnology.</span></span>

:::image type="content" source="media/overview-netx-duo/cru-logo-certification.png" alt-text="CRU UL sertifikası":::

<span data-ttu-id="d69f0-337">TUV ve UL sertifikalarıyla ilişkili yapıtlar (sertifika, güvenlik el kitabı, test raporu vb.) satış için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d69f0-337">Artifacts (Certificate, Safety Manual, Test Report, etc.) associated with the TUV and UL certifications are available for sale.</span></span>

<span data-ttu-id="d69f0-338">Uygulamanın ek sertifikaya ihtiyacı olduğu durumlarda, gerçek donanım platformunu kullanarak ve hatta uygulama kodunu kapsayan çeşitli standartlara anahtar sertifikası sağlamak için Microsoft aracılığıyla bir sertifika hizmeti kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d69f0-338">In cases where the application needs additional certification, a certification service is available through Microsoft for providing turn-key certification to various standards using the actual hardware platform and even covering the application code.</span></span> <span data-ttu-id="d69f0-339">Sertifika hizmetimiz hakkında daha fazla bilgi için bizimle iletişime geçin.</span><span class="sxs-lookup"><span data-stu-id="d69f0-339">Contact us for more details on our certification service.</span></span>

## <a name="eal4-common-criteria-security-certification"></a><span data-ttu-id="d69f0-340">EAL4 + ortak ölçütler güvenlik sertifikası</span><span class="sxs-lookup"><span data-stu-id="d69f0-340">EAL4+ Common Criteria security certification</span></span>

<span data-ttu-id="d69f0-341">Azure RTOS, EAL4 + ortak ölçütler güvenlik sertifikası elde etti.</span><span class="sxs-lookup"><span data-stu-id="d69f0-341">Azure RTOS has achieved EAL4+ Common Criteria security certification.</span></span> <span data-ttu-id="d69f0-342">Evalution (TOE) hedefi Azure RTOS ThreadX, Azure RTOS NetX Duo, Azure RTOS NetX güvenli TLS ve Azure RTOS NetX MQTT ' i içerir.</span><span class="sxs-lookup"><span data-stu-id="d69f0-342">The Target of Evalution (TOE) covers Azure RTOS ThreadX, Azure RTOS NetX Duo, Azure RTOS NetX Secure TLS, and Azure RTOS NetX MQTT.</span></span> <span data-ttu-id="d69f0-343">Bu, derin eklenmiş sensörler, cihazlar, uç yönlendiriciler ve ağ geçitleri için gereken en yaygın IoT protokollerini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d69f0-343">This represents the most typical IoT protocols required by deeply embedded sensors, devices, edge routers, and gateways.</span></span>

:::image type="content" source="media/overview-netx-duo/eal-logo-certification.png" alt-text="EAL sertifikası":::

<span data-ttu-id="d69f0-345">Microsoft Azure RTOS SC güvenlik sertifikası için kullanılan BT güvenlik değerlendirme olanağı, en parlama BV ' dir ve sertifika yetkilisi de bir Ttıt.</span><span class="sxs-lookup"><span data-stu-id="d69f0-345">The IT Security Evaluation Facility used for the Microsoft Azure RTOS SC security certification is Brightsight BV and the Certification Authority is SERTIT.</span></span>

## <a name="fips-140-2-validated"></a><span data-ttu-id="d69f0-346">FIPS 140-2 doğrulanan</span><span class="sxs-lookup"><span data-stu-id="d69f0-346">FIPS 140-2 Validated</span></span>

<span data-ttu-id="d69f0-347">Azure RTOS NetX şifre kitaplıkları, şifreleme modülleri için gereksinimleri belirten, yazılım için Federal bilgi Işleme standartlaştırma 140-2 (FIPS 140-2) sertifikası elde edin.</span><span class="sxs-lookup"><span data-stu-id="d69f0-347">Azure RTOS NetX Crypto libraries have achieved Federal Information Processing Standardization 140-2 (FIPS 140-2) Certification for software, which specifies requirements for cryptography modules.</span></span> <span data-ttu-id="d69f0-348">FIPS 140-2, şifreleme gücü ve özellikleri ile ilgili belirli standartları karşılamak için şifreleme tabanlı güvenlik kullanan tüm federal kamu kuruluşlarını ve departmanları gerektirir.</span><span class="sxs-lookup"><span data-stu-id="d69f0-348">FIPS 140-2 requires all federal government agencies and departments that use cryptographic-based security to meet specific standards related to encryption strength and capabilities.</span></span> <span data-ttu-id="d69f0-349">Bu şifreleme tabanlı güvenlik standartları, Kanada ve Avrupa Birliği 'nde de tanınır.</span><span class="sxs-lookup"><span data-stu-id="d69f0-349">These cryptographic-based security standards are also recognized in Canada and the European Union.</span></span>

<span data-ttu-id="d69f0-350">Azure RTOS NetX şifre kitaplıkları için kullanılan bilgi güvenliği değerlendirme laboratuvarı atsec idi ve sertifika yetkilisi ulusal standartlar ve Teknoloji Enstitüsü (NıST).</span><span class="sxs-lookup"><span data-stu-id="d69f0-350">The Information Security evaluation lab used for Azure RTOS NetX Crypto libraries was atsec and the certification authority is The National Institute of Standards and Technology (NIST).</span></span> <span data-ttu-id="d69f0-351">Ek ayrıntılar için [NIST Web sitesini](https://csrc.nist.gov/projects/cryptographic-module-validation-program/Certificate/3394) gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="d69f0-351">Review the [NIST website](https://csrc.nist.gov/projects/cryptographic-module-validation-program/Certificate/3394) for additional details.</span></span>

## <a name="interoperability-verification"></a><span data-ttu-id="d69f0-352">Birlikte çalışabilirlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="d69f0-352">Interoperability verification</span></span>

<span data-ttu-id="d69f0-353">NetX Duo, RFC standartlarına uyar ve çoğu satıcının cihazlarıyla birlikte çalışabilirlik desteği sunar.</span><span class="sxs-lookup"><span data-stu-id="d69f0-353">NetX Duo conforms to RFC standards and offers complete interoperability with devices for most vendors.</span></span>

![IPv6 Ready logosu](./media/overview-netx-duo/ipv6-ready-logo.png)

<span data-ttu-id="d69f0-355">Azure RTOS NetX Duo, kapsamlı IPv6-Ready logo sertifikasına ulaşmak için yalnızca katıştırılmış TCP/IP yığınlarından biridir. Bu, IPv6 Forumu tarafından yönetilen ve doğrulanan uyumluluk ve birlikte çalışabilirlik testlerini geçti olduğunu kanıtlayın.</span><span class="sxs-lookup"><span data-stu-id="d69f0-355">Azure RTOS NetX Duo is one of the only embedded TCP/IP stacks to achieve the rigorous IPv6-Ready Logo certification, evidence that it has passed conformance and interoperability tests, administered and validated by the IPv6 Forum.</span></span> <span data-ttu-id="d69f0-356">NetX Duo Ayrıca, NetX Duo çekirdek TCP/IP protokol uygulamasının sektör standardı IxANVL (otomatik ağ doğrulama kitaplığı) kullanır.</span><span class="sxs-lookup"><span data-stu-id="d69f0-356">NetX Duo also utilizes the industry standard IxANVL (Automated Network Validation Library) for the NetX Duo core TCP/IP protocol implementation.</span></span>

## <a name="comprehensive-iot-solution"></a><span data-ttu-id="d69f0-357">Kapsamlı IoT çözümü</span><span class="sxs-lookup"><span data-stu-id="d69f0-357">Comprehensive IoT solution</span></span>

<span data-ttu-id="d69f0-358">Azure RTOS NetX Duo, temel IP ve UDP desteği için 9 KB 'den 15 KB 'a kadar bir renetme sahiptir.</span><span class="sxs-lookup"><span data-stu-id="d69f0-358">Azure RTOS NetX Duo has a remarkably small footprint of 9 KB to 15 KB for basic IP and UDP support.</span></span> <span data-ttu-id="d69f0-359">NetX Duo, derin eklenmiş IoT uygulamaları için en kapsamlı TCP/IP ağıyla biridir.</span><span class="sxs-lookup"><span data-stu-id="d69f0-359">NetX Duo has one of the most comprehensive TCP/IP networking for deeply embedded IoT applications.</span></span> <span data-ttu-id="d69f0-360">Bu destek, aşağıdaki eklenti protokol ürünlerini içerir:</span><span class="sxs-lookup"><span data-stu-id="d69f0-360">This support includes the following add-on protocol products:</span></span>

<span data-ttu-id="d69f0-361">MQTT, CoAP, LWM2M, 6LoWPAN, SSL/TLS/DTLS, IPSec, Oto IP, DHCP, DNS, mDNS, DNS-SD, FTP, HTTP, IPSec, NAT, POP3, PPP, PPPoE, SMTP, SNMP v1/2/3, Telnet, TFTP</span><span class="sxs-lookup"><span data-stu-id="d69f0-361">MQTT, CoAP, LWM2M, 6LoWPAN, SSL/TLS/DTLS, IPsec, AutoIP, DHCP, DNS, mDNS, DNS-SD, FTP, HTTP, IPsec, NAT, POP3, PPP, PPPoE, SMTP, SNMP v1/2/3, Telnet, TFTP</span></span>

## <a name="advanced-technology"></a><span data-ttu-id="d69f0-362">Gelişmiş teknoloji</span><span class="sxs-lookup"><span data-stu-id="d69f0-362">Advanced technology</span></span>

<span data-ttu-id="d69f0-363">Azure RTOS NetX Duo, şunları içeren gelişmiş bir teknolojidir:</span><span class="sxs-lookup"><span data-stu-id="d69f0-363">Azure RTOS NetX Duo is advanced technology that includes:</span></span>

* <span data-ttu-id="d69f0-364">Piconet™ mimarisi</span><span class="sxs-lookup"><span data-stu-id="d69f0-364">Piconet™ architecture</span></span>
* <span data-ttu-id="d69f0-365">Otomatik ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="d69f0-365">Automatic scaling</span></span>
* <span data-ttu-id="d69f0-366">UDP Fast-Path teknolojisi™</span><span class="sxs-lookup"><span data-stu-id="d69f0-366">UDP Fast-Path Technology™</span></span>
* <span data-ttu-id="d69f0-367">Esnek paket yönetimi</span><span class="sxs-lookup"><span data-stu-id="d69f0-367">Flexible packet management</span></span>
* <span data-ttu-id="d69f0-368">Sıfır-API ve uygulama kopyalama</span><span class="sxs-lookup"><span data-stu-id="d69f0-368">Zero-copy API and implementation</span></span>
* <span data-ttu-id="d69f0-369">Çok sayfalı destek</span><span class="sxs-lookup"><span data-stu-id="d69f0-369">Multihomed support</span></span>
* <span data-ttu-id="d69f0-370">Tüm askıya alma sırasında isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="d69f0-370">Optional timeout on all suspension</span></span>
* <span data-ttu-id="d69f0-371">Statik yönlendirme desteği</span><span class="sxs-lookup"><span data-stu-id="d69f0-371">Static routing support</span></span>
* <span data-ttu-id="d69f0-372">IPsec</span><span class="sxs-lookup"><span data-stu-id="d69f0-372">IPsec</span></span>
* <span data-ttu-id="d69f0-373">SSL/TLS/DTLS</span><span class="sxs-lookup"><span data-stu-id="d69f0-373">SSL/TLS/DTLS</span></span>
* <span data-ttu-id="d69f0-374">Azure RTOS TraceX sistem analizi desteği</span><span class="sxs-lookup"><span data-stu-id="d69f0-374">Azure RTOS TraceX system analysis support</span></span>

## <a name="fastest-time-to-market"></a><span data-ttu-id="d69f0-375">En hızlı pazar süresi</span><span class="sxs-lookup"><span data-stu-id="d69f0-375">Fastest time-to-market</span></span>

<span data-ttu-id="d69f0-376">Azure RTOS NetX Duo yüklemek, öğrenmek, kullanmak, hata ayıklamak, doğrulamak, onaylamak ve sürdürmek kolaydır.</span><span class="sxs-lookup"><span data-stu-id="d69f0-376">Azure RTOS NetX Duo is easy to install, learn, use, debug, verify, certify and maintain.</span></span> <span data-ttu-id="d69f0-377">Sonuç olarak, NetX Duo, Broadcom ve Gainspan gibi birçok SoCs dahil olmak üzere, gömülü IoT cihazları için en popüler TCP/IP yığınlarından biridir. Tutarlı Pazar süresi avantajımız, şu şekilde oluşturulmuştur:</span><span class="sxs-lookup"><span data-stu-id="d69f0-377">As a result, NetX Duo is one of the most popular TCP/IP stacks for embedded IoT devices, including many SoCs from Broadcom, Gainspan, etc. Our consistent time-to-market advantage is built on:</span></span>

* <span data-ttu-id="d69f0-378">Kalite belgeleri: lütfen [Azure RTOS NetX Duo Kullanıcı Kılavuzumuzu](about-this-guide.md) gözden geçirin ve kendiniz görün!</span><span class="sxs-lookup"><span data-stu-id="d69f0-378">Quality documentation – please review our [Azure RTOS NetX Duo User Guide](about-this-guide.md) and see for yourself!</span></span>
* <span data-ttu-id="d69f0-379">Tüm kaynak kodu kullanılabilirliği</span><span class="sxs-lookup"><span data-stu-id="d69f0-379">Complete source code availability</span></span>
* <span data-ttu-id="d69f0-380">Kullanımı kolay API</span><span class="sxs-lookup"><span data-stu-id="d69f0-380">Easy-to-use API</span></span>
* <span data-ttu-id="d69f0-381">Kapsamlı ve gelişmiş özellik kümesi</span><span class="sxs-lookup"><span data-stu-id="d69f0-381">Comprehensive and advanced feature set</span></span>

## <a name="one-simple-license"></a><span data-ttu-id="d69f0-382">Tek bir basit lisans</span><span class="sxs-lookup"><span data-stu-id="d69f0-382">One Simple License</span></span>

<span data-ttu-id="d69f0-383">Önceden lisanslanmış cihazlara dağıtıldığında, diğer tüm cihazların basit bir yıllık lisansa sahip olması için, kaynak kodu ve test lisansları için ücret ve maliyet kullanımı maliyeti yoktur.</span><span class="sxs-lookup"><span data-stu-id="d69f0-383">There is no cost to use and test the source code and no cost for production licenses when deployed to pre-licensed devices, all other devices need a simple annual license.</span></span>

## <a name="full-highest-quality-source-code"></a><span data-ttu-id="d69f0-384">Tam, en yüksek kaliteli kaynak kodu</span><span class="sxs-lookup"><span data-stu-id="d69f0-384">Full, highest-quality source code</span></span>

<span data-ttu-id="d69f0-385">Yıl boyunca, Azure RTOS NetX Duo kaynak kodu, çubuğun kalitesini ve anlamayı kolay bir şekilde ayarladı.</span><span class="sxs-lookup"><span data-stu-id="d69f0-385">Throughout the years, Azure RTOS NetX Duo source code has set the bar in quality and ease of understanding.</span></span> <span data-ttu-id="d69f0-386">Ayrıca, dosya başına bir işleve sahip olma kuralı, kolay kaynak gezintisi için sağlar.</span><span class="sxs-lookup"><span data-stu-id="d69f0-386">In addition, the convention of having one function per file provides for easy source navigation.</span></span>

## <a name="supports-most-popular-architectures"></a><span data-ttu-id="d69f0-387">Popüler mimarilerin çoğunu destekler</span><span class="sxs-lookup"><span data-stu-id="d69f0-387">Supports most popular architectures</span></span>

<span data-ttu-id="d69f0-388">Azure RTOS NetX Duo, aşağıdaki gelişmiş mimariler de dahil olmak üzere en popüler 32/64 bit mikro işlemciler üzerinde çalışır ve tamamen sınanmış ve tam olarak desteklenmektedir:</span><span class="sxs-lookup"><span data-stu-id="d69f0-388">Azure RTOS NetX Duo runs on most popular 32/64-bit microprocessors out-of-the-box, fully tested and fully supported, including the following advanced architectures:</span></span>

<span data-ttu-id="d69f0-389">**Analog cihazlar**: parça, BlackICE, CM4xx</span><span class="sxs-lookup"><span data-stu-id="d69f0-389">**Analog Devices**: SHARC, Blackfin, CM4xx</span></span>

<span data-ttu-id="d69f0-390">**Andes Core**: RISC-V</span><span class="sxs-lookup"><span data-stu-id="d69f0-390">**Andes Core**: RISC-V</span></span>

<span data-ttu-id="d69f0-391">**Ambiqmicro**: Pollo MCUs</span><span class="sxs-lookup"><span data-stu-id="d69f0-391">**Ambiqmicro**: pollo MCUs</span></span>

<span data-ttu-id="d69f0-392">**ARM**: RM7, ARM9, ARM11, Cortex-M0/m3/M4/M7/A15/a5/A7/A8/A9/A5X 64-bı/A7x 64-bit/R4/R5, TrustZone ARMv8-ı</span><span class="sxs-lookup"><span data-stu-id="d69f0-392">**ARM**: RM7, ARM9, ARM11, Cortex-M0/M3/M4/M7/A15/A5/A7/A8/A9/A5x 64-bi/A7x 64-bit/R4/R5, TrustZone ARMv8-M</span></span>

<span data-ttu-id="d69f0-393">**Temposunda**: xtensa, elmas</span><span class="sxs-lookup"><span data-stu-id="d69f0-393">**Cadence**: Xtensa, Diamond</span></span>

<span data-ttu-id="d69f0-394">**Ceva**: PSoC, PSoC 4, PSoC 5, PSoC 6, FM0 +, FM3, MF4, Werwifi</span><span class="sxs-lookup"><span data-stu-id="d69f0-394">**CEVA**: PSoC, PSoC 4, PSoC 5, PSoC 6, FM0+, FM3, MF4, WICED WiFi</span></span>

<span data-ttu-id="d69f0-395">**Cypress**: RISC-V</span><span class="sxs-lookup"><span data-stu-id="d69f0-395">**Cypress**: RISC-V</span></span>

<span data-ttu-id="d69f0-396">**Ensilica**: ESI-RISC</span><span class="sxs-lookup"><span data-stu-id="d69f0-396">**EnSilica**: eSi-RISC</span></span>

<span data-ttu-id="d69f0-397">**Infineon**: XMC1000, XMC4000, kanore</span><span class="sxs-lookup"><span data-stu-id="d69f0-397">**Infineon**: XMC1000, XMC4000, TriCore</span></span>

<span data-ttu-id="d69f0-398">**Intel & Intel FPGA**: X36/Pentium, XSCALE, NIOS II, Cyclone, varış a 10</span><span class="sxs-lookup"><span data-stu-id="d69f0-398">**Intel & Intel FPGA**: x36/Pentium, XScale, NIOS II, Cyclone, Arria 10</span></span>

<span data-ttu-id="d69f0-399">**Mikro yonga**: AVR32, ARM7, ARM9, Cortex-M3/M4/M7, SAM3/4/7/9/A/C/D/E/G/L/ZF, PIC24/PIC32</span><span class="sxs-lookup"><span data-stu-id="d69f0-399">**Microchip**: AVR32, ARM7, ARM9, Cortex-M3/M4/M7, SAM3/4/7/9/A/C/D/E/G/L/SV, PIC24/PIC32</span></span>

<span data-ttu-id="d69f0-400">**Mikro yarı**: RISC-V</span><span class="sxs-lookup"><span data-stu-id="d69f0-400">**Microsemi**: RISC-V</span></span>

<span data-ttu-id="d69f0-401">**NXP**: LPC, ARM7, ARM9, PowerPC, 68 K, I.MX, ColdFire, Kinetis Cortex-M3/M4</span><span class="sxs-lookup"><span data-stu-id="d69f0-401">**NXP**: LPC, ARM7, ARM9, PowerPC, 68 K, i.MX, ColdFire, Kinetis Cortex-M3/M4</span></span>

<span data-ttu-id="d69f0-402">**Renesas**: SH, HS, v850, RX, Rz, Synergy</span><span class="sxs-lookup"><span data-stu-id="d69f0-402">**Renesas**: SH, HS, V850, RX, RZ, Synergy</span></span>

<span data-ttu-id="d69f0-403">**Silicon** Labs: EFM32</span><span class="sxs-lookup"><span data-stu-id="d69f0-403">**Silicon** Labs: EFM32</span></span>

<span data-ttu-id="d69f0-404">**Synopsys**: Arc 600, 700, Arc Em, Arc HS</span><span class="sxs-lookup"><span data-stu-id="d69f0-404">**Synopsys**: ARC 600, 700, ARC EM, ARC HS</span></span>

<span data-ttu-id="d69f0-405">**St**: STM32, ARM7, ARM9, Cortex-M3/M4/M7</span><span class="sxs-lookup"><span data-stu-id="d69f0-405">**ST**: STM32, ARM7, ARM9, Cortex-M3/M4/M7</span></span>

<span data-ttu-id="d69f0-406">**TL**: C5xxx, C6xxx, Stellardo, Sitara, Tiva-C</span><span class="sxs-lookup"><span data-stu-id="d69f0-406">**Tl**: C5xxx, C6xxx, Stellaris, Sitara, Tiva-C</span></span>

<span data-ttu-id="d69f0-407">**Dalga bilgi işlem**: MIPS32 4k, 24 K, 34 k, 1004 k, ver 5k, mikro Aptiv, ınteraptiv, Proaptiv, M-class</span><span class="sxs-lookup"><span data-stu-id="d69f0-407">**Wave Computing**: MIPS32 4K, 24 K, 34 K, 1004 K, MIPS64 5K, microAptiv, interAptiv, proAptiv, M-Class</span></span>

<span data-ttu-id="d69f0-408">**Xilinx**: mikro Blaze, PowerPC 405, zynq, Zynq UltraSCALE</span><span class="sxs-lookup"><span data-stu-id="d69f0-408">**Xilinx**: MicroBlaze, PowerPC 405, ZYNQ, ZYNQ UltraSCALE</span></span>

<span data-ttu-id="d69f0-409">*Listelenen tüm zamanlama ve boyut rakamları tahminlerdir ve geliştirme platformunuzun farklı olabilir.*</span><span class="sxs-lookup"><span data-stu-id="d69f0-409">*All timing and size figures listed are estimates and may be different on your development platform.*</span></span>

## <a name="related-services"></a><span data-ttu-id="d69f0-410">İlgili hizmetler</span><span class="sxs-lookup"><span data-stu-id="d69f0-410">Related services</span></span>

<span data-ttu-id="d69f0-411">IoT RTOS güvenlik modülü için Azure Güvenlik Merkezi, Azure RTOS cihazları için kapsamlı bir güvenlik çözümü sağlar.</span><span class="sxs-lookup"><span data-stu-id="d69f0-411">The Azure Security Center for IoT RTOS security module provides a comprehensive security solution for Azure RTOS devices.</span></span> <span data-ttu-id="d69f0-412">Azure RTOS için güvenlik modülü, kötü amaçlı ağ etkinliği algılama, özel uyarı tabanlı cihaz davranışı taban çizgisi sağlar ve cihaz güvenliği Hygiene 'ın artırılmasına yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="d69f0-412">The Security Module for Azure RTOS offers malicious network activity detection, custom alert based device behavior baselining, and helps improve device security hygiene.</span></span> <span data-ttu-id="d69f0-413">[Azure RTOS güvenlik modülü](https://docs.microsoft.com/azure/asc-for-iot/iot-security-azure-rtos) hakkında daha fazla bilgi edinin veya [Azure RTOS hızlı başlangıç Için güvenlik yapılandırması modülünü](https://docs.microsoft.com/azure/asc-for-iot/quickstart-azure-rtos-security-module) kullanmaya başlayın.</span><span class="sxs-lookup"><span data-stu-id="d69f0-413">Learn more about the [Security Module for Azure RTOS](https://docs.microsoft.com/azure/asc-for-iot/iot-security-azure-rtos) or get started with the [Configure Security Module for Azure RTOS](https://docs.microsoft.com/azure/asc-for-iot/quickstart-azure-rtos-security-module) quickstart.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d69f0-414">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d69f0-414">Next steps</span></span>

<span data-ttu-id="d69f0-415">NetX Duo hakkında daha fazla bilgi edinmek için [Azure RTOS NetX Duo Kullanıcı kılavuzuyla](about-this-guide.md)başlayın.</span><span class="sxs-lookup"><span data-stu-id="d69f0-415">To learn more about NetX Duo, start with the [Azure RTOS NetX Duo User Guide](about-this-guide.md).</span></span>
