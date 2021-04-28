---
title: Azure RTOS NetX Duo 'i anlama
description: Azure RTOS NetX Duo, özellikle de gömülü gerçek zamanlı ve IoT uygulamaları için özel olarak tasarlanan bir gelişmiş, endüstriyel sınıf TCP/IP ağ yığını.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: e3fe3bcc602f409cc76f3be47aca865bf8116697
ms.sourcegitcommit: 19d50693d8f5287ba6938ae1d23eef88435ed7b1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/28/2021
ms.locfileid: "108171344"
---
# <a name="overview-of-azure-rtos-netx-duo"></a><span data-ttu-id="cc19b-103">Azure RTOS NetX Duo 'e genel bakış</span><span class="sxs-lookup"><span data-stu-id="cc19b-103">Overview of Azure RTOS NetX Duo</span></span>

<span data-ttu-id="cc19b-104">Azure RTOS NetX Duo katıştırılmış TCP/IP ağ yığını, özellikle de daha fazla gömülü, gerçek zamanlı ve IoT uygulamaları için tasarlanan Microsoft 'un gelişmiş, endüstriyel sınıf ikili IPv4 ve IPv6 TCP/IP ağ yığınıdır.</span><span class="sxs-lookup"><span data-stu-id="cc19b-104">Azure RTOS NetX Duo embedded TCP/IP network stack is Microsoft's advanced, industrial grade dual IPv4 and IPv6 TCP/IP network stack that is designed specifically for deeply embedded, real-time, and IoT applications.</span></span> <span data-ttu-id="cc19b-105">NetX Duo, IPv4, IPv6, TCP ve UDP gibi çekirdek ağ protokollerine ve ek ve daha üst düzey eklenti protokollerinin eksiksiz bir paketini içeren katıştırılmış uygulamalar sağlar.</span><span class="sxs-lookup"><span data-stu-id="cc19b-105">NetX Duo provides embedded applications with core network protocols such as IPv4, IPv6, TCP, and UDP as well as a complete suite of additional, higher-level add-on protocols.</span></span> <span data-ttu-id="cc19b-106">Azure RTOS NetX Duo, Azure RTOS NetX güvenli IPSec ve Azure RTOS NetX güvenli SSL/TLS/DTLS dahil ek eklenti güvenlik ürünleri aracılığıyla güvenlik sağlar.</span><span class="sxs-lookup"><span data-stu-id="cc19b-106">Azure RTOS NetX Duo offers security via additional add-on security products, including Azure RTOS NetX Secure IPsec and Azure RTOS NetX Secure SSL/TLS/DTLS.</span></span> <span data-ttu-id="cc19b-107">Bunun hepsi küçük bir ayak izi, Hızlı yürütme ve üstün kullanım kolaylığıyla Azure RTOS NetX Duo, en zorlu ekli IoT uygulamalarına yönelik ideal seçenektir.</span><span class="sxs-lookup"><span data-stu-id="cc19b-107">All of this combined with an small footprint, fast execution, and superior ease-of-use make Azure RTOS NetX Duo the ideal choice for the most demanding embedded IoT applications.</span></span>

## <a name="api-protocols"></a><span data-ttu-id="cc19b-108">API protokolleri</span><span class="sxs-lookup"><span data-stu-id="cc19b-108">API protocols</span></span>

### <a name="mqtt"></a><span data-ttu-id="cc19b-109">MQTT</span><span class="sxs-lookup"><span data-stu-id="cc19b-109">MQTT</span></span>

* <span data-ttu-id="cc19b-110">Mesajlaşma kuyruğu telemetri aktarımı (MQTT)</span><span class="sxs-lookup"><span data-stu-id="cc19b-110">Messaging Queue Telemetry Transport (MQTT)</span></span>
* <span data-ttu-id="cc19b-111">En az 2,7 KB FLASH</span><span class="sxs-lookup"><span data-stu-id="cc19b-111">Minimal 2.7 KB FLASH</span></span>

### <a name="auto-ip"></a><span data-ttu-id="cc19b-112">Otomatik IP</span><span class="sxs-lookup"><span data-stu-id="cc19b-112">Auto IP</span></span>

* <span data-ttu-id="cc19b-113">Otomatik IPv4 adresi ataması</span><span class="sxs-lookup"><span data-stu-id="cc19b-113">Automatic IPv4 address assignment</span></span>
* <span data-ttu-id="cc19b-114">En az 1,2 KB, 300 bayt RAM</span><span class="sxs-lookup"><span data-stu-id="cc19b-114">Minimal 1.2 KB, 300 bytes of RAM</span></span>

### <a name="http-https"></a><span data-ttu-id="cc19b-115">HTTP, HTTPS</span><span class="sxs-lookup"><span data-stu-id="cc19b-115">HTTP, HTTPS</span></span>

#### <a name="http-10"></a><span data-ttu-id="cc19b-116">HTTP 1,0</span><span class="sxs-lookup"><span data-stu-id="cc19b-116">HTTP 1.0</span></span>

* <span data-ttu-id="cc19b-117">Köprü Metni Aktarım Protokolü (HTTP)</span><span class="sxs-lookup"><span data-stu-id="cc19b-117">Hypertext Transfer Protocol(HTTP)</span></span>
* <span data-ttu-id="cc19b-118">Minimum 2,8 KB-4,8 KB, FLASH/0,4 KB ile 1,0 KB arasında</span><span class="sxs-lookup"><span data-stu-id="cc19b-118">Minimal 2.8 KB to 4.8 KB FLASH / 0.4 KB to 1.0 KB RAM</span></span>
* <span data-ttu-id="cc19b-119">İstemci ve sunucu desteği</span><span class="sxs-lookup"><span data-stu-id="cc19b-119">Client and server support</span></span>

#### <a name="httphttps-11"></a><span data-ttu-id="cc19b-120">HTTP/HTTPS 1,1</span><span class="sxs-lookup"><span data-stu-id="cc19b-120">HTTP/HTTPS 1.1</span></span>

* <span data-ttu-id="cc19b-121">Köprü Metni Aktarım Protokolü (HTTP)</span><span class="sxs-lookup"><span data-stu-id="cc19b-121">Hypertext Transfer Protocol(HTTP)</span></span>
* <span data-ttu-id="cc19b-122">Minimum 3,0 KB-9,5 KB FLASH/0,5 KB-2 KB RAM</span><span class="sxs-lookup"><span data-stu-id="cc19b-122">Minimal 3.0 KB to 9.5 KB FLASH / 0.5 KB to 2 KB RAM</span></span>
* <span data-ttu-id="cc19b-123">İstemci ve sunucu desteği</span><span class="sxs-lookup"><span data-stu-id="cc19b-123">Client and server support</span></span>
* <span data-ttu-id="cc19b-124">Birden çok gelen istemci oturumu</span><span class="sxs-lookup"><span data-stu-id="cc19b-124">Multiple incoming client sessions</span></span>
* <span data-ttu-id="cc19b-125">Düz metin ve şifreli HTTPS</span><span class="sxs-lookup"><span data-stu-id="cc19b-125">Plain text and encrypted HTTPS</span></span>
* <span data-ttu-id="cc19b-126">Kalıcı bağlantı desteği</span><span class="sxs-lookup"><span data-stu-id="cc19b-126">Persistent connection support</span></span>
* <span data-ttu-id="cc19b-127">Çok parçalı dosya yükleme</span><span class="sxs-lookup"><span data-stu-id="cc19b-127">Multipart file upload</span></span>
* <span data-ttu-id="cc19b-128">Azure RTOS NetX güvenli TLS ile tam olarak tümleşik</span><span class="sxs-lookup"><span data-stu-id="cc19b-128">Fully integrated with Azure RTOS NetX Secure TLS</span></span>

### <a name="smtp"></a><span data-ttu-id="cc19b-129">SMTP</span><span class="sxs-lookup"><span data-stu-id="cc19b-129">SMTP</span></span>

* <span data-ttu-id="cc19b-130">Basit küçük/küçük Aktarım Protokolü (SMTP)</span><span class="sxs-lookup"><span data-stu-id="cc19b-130">Simple Mall Transfer Protocol (SMTP)</span></span>
* <span data-ttu-id="cc19b-131">En az 4,1 KB ve 0,6 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="cc19b-131">Minimal 4.1 KB and 0.6 KB RAM footprint</span></span>
* <span data-ttu-id="cc19b-132">İstemci desteği</span><span class="sxs-lookup"><span data-stu-id="cc19b-132">Client support</span></span>

### <a name="dhcp"></a><span data-ttu-id="cc19b-133">DHCP</span><span class="sxs-lookup"><span data-stu-id="cc19b-133">DHCP</span></span>

* <span data-ttu-id="cc19b-134">Dinamik Ana Bilgisayar Yapılandırma Protokolü (DHCP)</span><span class="sxs-lookup"><span data-stu-id="cc19b-134">Dynamic Host Configuration Protocol (DHCP)</span></span>
* <span data-ttu-id="cc19b-135">Minimum 3,6 KB-4,6 KB FLASH, 2,7 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="cc19b-135">Minimal 3.6 KB to 4.6 KB FLASH, 2.7 KB RAM footprint</span></span>
* <span data-ttu-id="cc19b-136">İstemci ve sunucu desteği</span><span class="sxs-lookup"><span data-stu-id="cc19b-136">Client and server support</span></span>
* <span data-ttu-id="cc19b-137">IPv4 ve IPv6 desteği</span><span class="sxs-lookup"><span data-stu-id="cc19b-137">IPv4 and IPv6 support</span></span>

### <a name="nat"></a><span data-ttu-id="cc19b-138">NAT</span><span class="sxs-lookup"><span data-stu-id="cc19b-138">NAT</span></span>

* <span data-ttu-id="cc19b-139">Ağ Adresi Çevirisi (NAT)</span><span class="sxs-lookup"><span data-stu-id="cc19b-139">Network Address Translation (NAT)</span></span>
* <span data-ttu-id="cc19b-140">Minimum 3,5 K6 ve 0,6 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="cc19b-140">Minimal 3.5K6 and 0.6 KB RAM footprint</span></span>
* <span data-ttu-id="cc19b-141">IPv4 adresi desteği</span><span class="sxs-lookup"><span data-stu-id="cc19b-141">IPv4 address support</span></span>
* <span data-ttu-id="cc19b-142">NAT yalnızca Azure RTOS NetX Duo ile kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="cc19b-142">NAT is only available with Azure RTOS NetX Duo</span></span>

### <a name="snmp"></a><span data-ttu-id="cc19b-143">SNMP</span><span class="sxs-lookup"><span data-stu-id="cc19b-143">SNMP</span></span>

* <span data-ttu-id="cc19b-144">Basit Ağ Yönetim Protokolü (SNMP)</span><span class="sxs-lookup"><span data-stu-id="cc19b-144">Simple Network Management Protocol (SNMP)</span></span>
* <span data-ttu-id="cc19b-145">En az 10,9 KB ve 2,6 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="cc19b-145">Minimal 10.9 KB and 2.6 KB RAM footprint</span></span>
* <span data-ttu-id="cc19b-146">VI, v2 ve v3 için aracı desteği</span><span class="sxs-lookup"><span data-stu-id="cc19b-146">Agent support for VI, V2, and V3</span></span>

### <a name="dns-mdns-dns-sd"></a><span data-ttu-id="cc19b-147">DNS, mDNS, DNS-SD</span><span class="sxs-lookup"><span data-stu-id="cc19b-147">DNS, mDNS, DNS-SD</span></span>

* <span data-ttu-id="cc19b-148">Etki Alanı Adı Sistemi (DNS)</span><span class="sxs-lookup"><span data-stu-id="cc19b-148">Domain Name System (DNS)</span></span>
* <span data-ttu-id="cc19b-149">Çok noktaya yayın etki alanı adı sistemi (mDNS)</span><span class="sxs-lookup"><span data-stu-id="cc19b-149">Multicast Domain Name System (mDNS)</span></span>
* <span data-ttu-id="cc19b-150">DNS tabanlı hizmet bulma (DNS-SD)</span><span class="sxs-lookup"><span data-stu-id="cc19b-150">DNS-based service discovery (DNS-SD)</span></span>
* <span data-ttu-id="cc19b-151">DNS en az 2,4 KB-3 KB FLASH, 1 KB RAM ayak</span><span class="sxs-lookup"><span data-stu-id="cc19b-151">DNS Minimal 2.4 KB to 3 KB FLASH, 1 KB RAM footprint</span></span>
* <span data-ttu-id="cc19b-152">İstemci desteği</span><span class="sxs-lookup"><span data-stu-id="cc19b-152">Client support</span></span>
* <span data-ttu-id="cc19b-153">mDNS ve DNS-SD yalnızca Azure RTOS NetX Duo ile kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="cc19b-153">mDNS and DNS-SD are only available with Azure RTOS NetX Duo</span></span>

### <a name="p0p3"></a><span data-ttu-id="cc19b-154">P0P3</span><span class="sxs-lookup"><span data-stu-id="cc19b-154">P0P3</span></span>

* <span data-ttu-id="cc19b-155">Postane Protokolü sürüm 3 (POP3)</span><span class="sxs-lookup"><span data-stu-id="cc19b-155">Post Office Protocol Version 3 (POP3)</span></span>
* <span data-ttu-id="cc19b-156">En az 8,1 KB ve 1,4 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="cc19b-156">Minimal 8.1 KB and 1.4 KB RAM footprint</span></span>
* <span data-ttu-id="cc19b-157">İstemci desteği</span><span class="sxs-lookup"><span data-stu-id="cc19b-157">Client support</span></span>

### <a name="telnet"></a><span data-ttu-id="cc19b-158">Sun</span><span class="sxs-lookup"><span data-stu-id="cc19b-158">TELNET</span></span>

* <span data-ttu-id="cc19b-159">En az 0,5 KB ve 0,3 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="cc19b-159">Minimal 0.5 KB and 0.3 KB RAM footprint</span></span>
* <span data-ttu-id="cc19b-160">İstemci ve sunucu desteği</span><span class="sxs-lookup"><span data-stu-id="cc19b-160">Client and server support</span></span>
* <span data-ttu-id="cc19b-161">Sezgisel Telnet API 'Leri *: \* nx_telnet_*</span><span class="sxs-lookup"><span data-stu-id="cc19b-161">Intuitive Telnet APIs: *nx_telnet_\**</span></span>

### <a name="ftp-tftp"></a><span data-ttu-id="cc19b-162">FTP, TFTP</span><span class="sxs-lookup"><span data-stu-id="cc19b-162">FTP, TFTP</span></span>

* <span data-ttu-id="cc19b-163">Dosya Aktarım Protokolü (FTP)</span><span class="sxs-lookup"><span data-stu-id="cc19b-163">File Transfer Protocol (FTP)</span></span>
* <span data-ttu-id="cc19b-164">Önemsiz Dosya Aktarım İletişim Kuralı (TFTP)</span><span class="sxs-lookup"><span data-stu-id="cc19b-164">Trivial File Transfer Protocol (TFTP)</span></span>
* <span data-ttu-id="cc19b-165">FTP en az 1,8 KB-7,2 KB FLASH, 0,6 KB ile 2,1 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="cc19b-165">FTP Minimal 1.8 KB to 7.2 KB FLASH, 0.6 KB to 2.1 KB RAM footprint</span></span>
* <span data-ttu-id="cc19b-166">TFTP en az 1,7 KB-2,4 KB FLASH, 0,3 KB ile 1,8 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="cc19b-166">TFTP Minimal 1.7 KB to 2.4 KB FLASH, 0.3 KB to 1.8 KB RAM footprint</span></span>
* <span data-ttu-id="cc19b-167">İstemci ve sunucu desteği</span><span class="sxs-lookup"><span data-stu-id="cc19b-167">Client and server support</span></span>
* <span data-ttu-id="cc19b-168">Sezgisel FTP ve TFTP API 'Leri *: \* nx_ftp_* veya *nx_tftp_ \**</span><span class="sxs-lookup"><span data-stu-id="cc19b-168">Intuitive FTP and TFTP APIs: *nx_ftp_\** or *nx_tftp_\**</span></span>

### <a name="ppp-pppoe"></a><span data-ttu-id="cc19b-169">PPP, PPPoE</span><span class="sxs-lookup"><span data-stu-id="cc19b-169">PPP, PPPoE</span></span>

* <span data-ttu-id="cc19b-170">POlNT noktadan noktaya Protokolü (PPP)</span><span class="sxs-lookup"><span data-stu-id="cc19b-170">Polnt-to-PoInt Protocol (PPP)</span></span>
* <span data-ttu-id="cc19b-171">Ethernet üzerinden Noktadan Noktaya Protokolü (PPPoE)</span><span class="sxs-lookup"><span data-stu-id="cc19b-171">Point-to-Point Protocol over Ethernet(PPPoE)</span></span>
* <span data-ttu-id="cc19b-172">En az 7,1 KB ve 3,8 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="cc19b-172">Minimal 7.1 KB and 3.8 KB RAM footprint</span></span>
* <span data-ttu-id="cc19b-173">Sezgisel PPP API 'Leri *: \* nx_ppp_*</span><span class="sxs-lookup"><span data-stu-id="cc19b-173">Intuitive PPP APIs: *nx_ppp_\**</span></span>

* <span data-ttu-id="cc19b-174">PPPoE yalnızca Azure RTOS NetX Duo ile kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="cc19b-174">PPPoE is only available with Azure RTOS NetX Duo</span></span>

### <a name="sntp"></a><span data-ttu-id="cc19b-175">SNTP</span><span class="sxs-lookup"><span data-stu-id="cc19b-175">SNTP</span></span>

* <span data-ttu-id="cc19b-176">Basit ağ zaman Protokolü (SNTP)</span><span class="sxs-lookup"><span data-stu-id="cc19b-176">Simple Network Time Protocol (SNTP)</span></span>
* <span data-ttu-id="cc19b-177">En az 4 KB ve 0,5 KB RAM</span><span class="sxs-lookup"><span data-stu-id="cc19b-177">Minimal 4 KB and 0.5 KB RAM</span></span>
* <span data-ttu-id="cc19b-178">İstemci desteği</span><span class="sxs-lookup"><span data-stu-id="cc19b-178">Client support</span></span>
* <span data-ttu-id="cc19b-179">Sezgisel SNTP API 'Leri *: \* nx_sntp_*</span><span class="sxs-lookup"><span data-stu-id="cc19b-179">Intuitive SNTP APIs: *nx_sntp_\**</span></span>

### <a name="azure-rtos-netx-duo-api"></a><span data-ttu-id="cc19b-180">Azure RTOS NetX Duo API 'SI</span><span class="sxs-lookup"><span data-stu-id="cc19b-180">Azure RTOS NetX Duo API</span></span>

* <span data-ttu-id="cc19b-181">Sezgisel ve tutarlı API</span><span class="sxs-lookup"><span data-stu-id="cc19b-181">Intuitive and consistent API</span></span>
* <span data-ttu-id="cc19b-182">İsim-fiil adlandırma kuralı</span><span class="sxs-lookup"><span data-stu-id="cc19b-182">Noun-verb naming convention</span></span>
* <span data-ttu-id="cc19b-183">Hızlı, sıfır kopya API 'SI uygulama</span><span class="sxs-lookup"><span data-stu-id="cc19b-183">Fast, zero-copy API implementation</span></span>
* <span data-ttu-id="cc19b-184">Azure RTOS NetX olarak kolayca tanımlanabilmesi için tüm API 'Lerin önde gelen <i>nx_ \*</i></span><span class="sxs-lookup"><span data-stu-id="cc19b-184">All APIs have leading <i>nx_\*</i> to easily identify as Azure RTOS NetX</span></span>
* <span data-ttu-id="cc19b-185">API 'Lerin engellenmesi isteğe bağlı iş parçacığı zaman aşımına uğradı</span><span class="sxs-lookup"><span data-stu-id="cc19b-185">Blocking APIs have optional thread timeout</span></span>
* <span data-ttu-id="cc19b-186">Daha fazla bilgi için bkz. [Azure RTOS NetX Duo Kullanıcı Kılavuzu](about-this-guide.md)</span><span class="sxs-lookup"><span data-stu-id="cc19b-186">See [Azure RTOS NetX Duo User Guide](about-this-guide.md) for more details</span></span>
* <span data-ttu-id="cc19b-187">Eski yuva kodu taşıma için isteğe bağlı BSD katmanı</span><span class="sxs-lookup"><span data-stu-id="cc19b-187">Optional BSD layer for porting legacy socket code</span></span>

### <a name="igmp"></a><span data-ttu-id="cc19b-188">IGMP</span><span class="sxs-lookup"><span data-stu-id="cc19b-188">IGMP</span></span>

* <span data-ttu-id="cc19b-189">Internet Grup Yönetimi Protokolü (IGMP)</span><span class="sxs-lookup"><span data-stu-id="cc19b-189">Internet Group Management Protocol (IGMP)</span></span>
* <span data-ttu-id="cc19b-190">En az 2,5 KB FLASH</span><span class="sxs-lookup"><span data-stu-id="cc19b-190">Minimal 2.5 KB FLASH</span></span>
* <span data-ttu-id="cc19b-191">IPv4 çok noktaya yayın grubu desteği</span><span class="sxs-lookup"><span data-stu-id="cc19b-191">IPv4 multicast group support</span></span>
* <span data-ttu-id="cc19b-192">IXIA IxANVL doğrulanan</span><span class="sxs-lookup"><span data-stu-id="cc19b-192">IXIA IxANVL validated</span></span>
* <span data-ttu-id="cc19b-193">İsteğe bağlı ıGMP istatistikleri</span><span class="sxs-lookup"><span data-stu-id="cc19b-193">Optional IGMP statistics</span></span>
* <span data-ttu-id="cc19b-194">Azure RTOS ThreadX aracılığıyla sistem düzeyinde izleme</span><span class="sxs-lookup"><span data-stu-id="cc19b-194">System-level trace via Azure RTOS ThreadX</span></span>
* <span data-ttu-id="cc19b-195">Sezgisel ıGMP API 'Leri *: \* nx_igmp_*</span><span class="sxs-lookup"><span data-stu-id="cc19b-195">Intuitive IGMP APIs: *nx_igmp_\**</span></span>

### <a name="azure-rtos-netx-secure-dtls"></a><span data-ttu-id="cc19b-196">Azure RTOS NetX güvenli DTLS</span><span class="sxs-lookup"><span data-stu-id="cc19b-196">Azure RTOS NetX Secure DTLS</span></span>

* <span data-ttu-id="cc19b-197">Veri birimi Aktarım Katmanı Güvenliği (DTLS) 1,0 ve 1,2</span><span class="sxs-lookup"><span data-stu-id="cc19b-197">Datagram Transport Layer Security (DTLS) 1.0 and 1.2</span></span>
* <span data-ttu-id="cc19b-198">En az 11 KB FLASH</span><span class="sxs-lookup"><span data-stu-id="cc19b-198">Minimal 11 KB FLASH</span></span>
* <span data-ttu-id="cc19b-199">Fast, Software RSA 2048-bit anahtar boyutu ~ 1-saniye @120MHz</span><span class="sxs-lookup"><span data-stu-id="cc19b-199">Fast, software RSA 2048-bit key size ~1-second @120MHz</span></span>
* <span data-ttu-id="cc19b-200">Kolaylaştırılmış X. 509.440 uygulama</span><span class="sxs-lookup"><span data-stu-id="cc19b-200">Streamlined X.509 Implementation</span></span>
* <span data-ttu-id="cc19b-201">Azure RTOS NetX Duo UDP yuvaları ile tam olarak tümleşik</span><span class="sxs-lookup"><span data-stu-id="cc19b-201">Fully integrated with Azure RTOS NetX Duo UDP sockets</span></span>
* <span data-ttu-id="cc19b-202">Donanım şifreleme desteği</span><span class="sxs-lookup"><span data-stu-id="cc19b-202">Hardware Crypto Support</span></span>
* <span data-ttu-id="cc19b-203">Yazılım şifreleme desteği: RSA (tüm anahtar boyutları), AES, DES/3DES, ECC, HMAC, MD5, SHA-1, SHA-2 (SHA-224, SHA-256, SHA-384, SHA-512)</span><span class="sxs-lookup"><span data-stu-id="cc19b-203">Software Crypto Support: RSA (all key sizes), AES, DES/3DES, ECC, HMAC, MD5, SHA-1, SHA-2 (SHA-224, SHA-256, SHA-384, SHA-512)</span></span>
* <span data-ttu-id="cc19b-204">P eğrileri 192/224/256/384/521 dahil olmak üzere ECDSA (imzalama) ve ECDH (şifreleme) ile Eliptik Eğri Şifreleme (ECC)</span><span class="sxs-lookup"><span data-stu-id="cc19b-204">Elliptic Curve Cryptography (ECC) with ECDSA (signing) and ECDH (encryption), including P-curves 192/224/256/384/521</span></span>
* <span data-ttu-id="cc19b-205">Şifrelenmiş anahtar desteği (donanıma bağımlı)</span><span class="sxs-lookup"><span data-stu-id="cc19b-205">Encrypted Key Support (hardware dependent)</span></span>

### <a name="azure-rtos-netx-secure-tls"></a><span data-ttu-id="cc19b-206">Azure RTOS NetX güvenli TLS</span><span class="sxs-lookup"><span data-stu-id="cc19b-206">Azure RTOS NetX Secure TLS</span></span>

* <span data-ttu-id="cc19b-207">Aktarım Katmanı Güvenliği (TLS) 1,0, 1,1 ve 1,2</span><span class="sxs-lookup"><span data-stu-id="cc19b-207">Transport Layer Security (TLS) 1.0, 1.1, and 1.2</span></span>
* <span data-ttu-id="cc19b-208">En az 8,8 KB FLASH</span><span class="sxs-lookup"><span data-stu-id="cc19b-208">Minimal 8.8 KB FLASH</span></span>
* <span data-ttu-id="cc19b-209">Fast, Software RSA 2048-bit anahtar boyutu ~ 1-saniye @120MHz</span><span class="sxs-lookup"><span data-stu-id="cc19b-209">Fast, software RSA 2048-bit key size ~1-second @120MHz</span></span>
* <span data-ttu-id="cc19b-210">Kolaylaştırılmış X. 509.440 uygulama</span><span class="sxs-lookup"><span data-stu-id="cc19b-210">Streamlined X.509 Implementation</span></span>
* <span data-ttu-id="cc19b-211">Azure RTOS NetX Duo TCP yuvaları ile tam olarak tümleşik</span><span class="sxs-lookup"><span data-stu-id="cc19b-211">Fully integrated with Azure RTOS NetX Duo TCP sockets</span></span>
* <span data-ttu-id="cc19b-212">Donanım şifreleme desteği</span><span class="sxs-lookup"><span data-stu-id="cc19b-212">Hardware Crypto Support</span></span>
* <span data-ttu-id="cc19b-213">Yazılım şifreleme desteği: RSA (tüm anahtar boyutları), AES, DES/3DES, ECC, HMAC, MD5, SHA-1, SHA-2 (SHA-224, SHA-256, SHA-384, SHA-512)</span><span class="sxs-lookup"><span data-stu-id="cc19b-213">Software Crypto Support: RSA (all key sizes), AES, DES/3DES, ECC, HMAC, MD5, SHA-1, SHA-2 (SHA-224, SHA-256, SHA-384, SHA-512)</span></span>
* <span data-ttu-id="cc19b-214">P eğrileri 192/224/256/384/521 dahil olmak üzere ECDSA (imzalama) ve ECDH (şifreleme) ile Eliptik Eğri Şifreleme (ECC)</span><span class="sxs-lookup"><span data-stu-id="cc19b-214">Elliptic Curve Cryptography (ECC) with ECDSA (signing) and ECDH (encryption), including P-curves 192/224/256/384/521</span></span>
* <span data-ttu-id="cc19b-215">Şifrelenmiş anahtar desteği (donanıma bağımlı)</span><span class="sxs-lookup"><span data-stu-id="cc19b-215">Encrypted Key Support (hardware dependent)</span></span>

### <a name="icmp"></a><span data-ttu-id="cc19b-216">ICMP</span><span class="sxs-lookup"><span data-stu-id="cc19b-216">ICMP</span></span>

* <span data-ttu-id="cc19b-217">Internet Denetim Iletisi Protokolü (ıCMP)</span><span class="sxs-lookup"><span data-stu-id="cc19b-217">Internet Control Message Protocol (ICMP)</span></span>
* <span data-ttu-id="cc19b-218">En az 2,5 KB FLASH</span><span class="sxs-lookup"><span data-stu-id="cc19b-218">Minimal 2.5 KB FLASH</span></span>
* <span data-ttu-id="cc19b-219">IPv4 ve IPv6 desteği</span><span class="sxs-lookup"><span data-stu-id="cc19b-219">IPv4 and IPv6 support</span></span>
* <span data-ttu-id="cc19b-220">IXIA IxANVL doğrulanan</span><span class="sxs-lookup"><span data-stu-id="cc19b-220">IXIA IxANVL validated</span></span>
* <span data-ttu-id="cc19b-221">Ping isteği ve ping yanıtı</span><span class="sxs-lookup"><span data-stu-id="cc19b-221">Ping request and ping response</span></span>
* <span data-ttu-id="cc19b-222">Ping isteklerinde isteğe bağlı iş parçacığı askıya alma</span><span class="sxs-lookup"><span data-stu-id="cc19b-222">Optional thread suspension on ping requests</span></span>
* <span data-ttu-id="cc19b-223">Tüm askıya alma sırasında isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="cc19b-223">Optional timeout on all suspension</span></span>
* <span data-ttu-id="cc19b-224">İsteğe bağlı ıCMP istatistikleri</span><span class="sxs-lookup"><span data-stu-id="cc19b-224">Optional ICMP statistics</span></span>
* <span data-ttu-id="cc19b-225">Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme</span><span class="sxs-lookup"><span data-stu-id="cc19b-225">System-level trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="cc19b-226">Sezgisel ıCMP API 'Leri *: \* nx_icmp_*</span><span class="sxs-lookup"><span data-stu-id="cc19b-226">Intuitive ICMP APIs: *nx_icmp_\**</span></span>

### <a name="udp"></a><span data-ttu-id="cc19b-227">UDP</span><span class="sxs-lookup"><span data-stu-id="cc19b-227">UDP</span></span>

* <span data-ttu-id="cc19b-228">Kullanıcı veri birimi Protokolü (UDP)</span><span class="sxs-lookup"><span data-stu-id="cc19b-228">User Datagram Protocol (UDP)</span></span>
* <span data-ttu-id="cc19b-229">Yuva başına en az 2,5 KB FLASH, 124 yuva baytı</span><span class="sxs-lookup"><span data-stu-id="cc19b-229">Minimal 2.5 KB FLASH, 124 sockets bytes of RAM per socket</span></span>
* <span data-ttu-id="cc19b-230">Hızlı, neredeyse wıned TCP paket işleme:</span><span class="sxs-lookup"><span data-stu-id="cc19b-230">Fast, near wirespeed TCP packet processing:</span></span>
    * <span data-ttu-id="cc19b-231">100 Mbps Ethernet, MCU @100MHz , 14% MCU kullanımı ÜZERINDE RX 95 Mbps</span><span class="sxs-lookup"><span data-stu-id="cc19b-231">RX 95 Mbps on 100 Mbps Ethernet, MCU @100MHz, 14% MCU utilization</span></span>
    * <span data-ttu-id="cc19b-232">TX 94 Mbps, 100 Mbps Ethernet, MCU @100MHz , 10% MCU kullanımı</span><span class="sxs-lookup"><span data-stu-id="cc19b-232">TX 94 Mbps on 100 Mbps Ethernet, MCU @100MHz, 10% MCU utilization</span></span>
* <span data-ttu-id="cc19b-233">UDP hızlı yol™ teknolojisi</span><span class="sxs-lookup"><span data-stu-id="cc19b-233">UDP Fast Path™ technology</span></span>
* <span data-ttu-id="cc19b-234">UDP sayısıyla ilgili sınır yok</span><span class="sxs-lookup"><span data-stu-id="cc19b-234">No limits on the number of UDP</span></span>
* <span data-ttu-id="cc19b-235">IXIA IxANVL doğrulanan</span><span class="sxs-lookup"><span data-stu-id="cc19b-235">IXIA IxANVL validated</span></span>
* <span data-ttu-id="cc19b-236">Yuva alma sırasında isteğe bağlı askıya alma</span><span class="sxs-lookup"><span data-stu-id="cc19b-236">Optional suspension on socket receive</span></span>
* <span data-ttu-id="cc19b-237">Tüm askıya alma sırasında isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="cc19b-237">Optional timeout on all suspension</span></span>
* <span data-ttu-id="cc19b-238">İsteğe bağlı UDP istatistikleri</span><span class="sxs-lookup"><span data-stu-id="cc19b-238">Optional UDP statistics</span></span>
* <span data-ttu-id="cc19b-239">Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme</span><span class="sxs-lookup"><span data-stu-id="cc19b-239">System-level trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="cc19b-240">Sezgisel UDP API 'Leri *: \* nx_udp_*</span><span class="sxs-lookup"><span data-stu-id="cc19b-240">Intuitive UDP APIs: *nx_udp_\**</span></span>

### <a name="tcp"></a><span data-ttu-id="cc19b-241">TCP</span><span class="sxs-lookup"><span data-stu-id="cc19b-241">TCP</span></span>

* <span data-ttu-id="cc19b-242">İletim Denetimi Protokolü (TCP)</span><span class="sxs-lookup"><span data-stu-id="cc19b-242">Transmission Control Protocol (TCP)</span></span>
* <span data-ttu-id="cc19b-243">Minimum 10,5 K8-12,5 KB FLASH, her yuva için 280 bayt RAM</span><span class="sxs-lookup"><span data-stu-id="cc19b-243">Minimal 10.5K8 to 12.5 KB FLASH, 280 bytes of RAM per socket</span></span>
* <span data-ttu-id="cc19b-244">Hızlı, neredeyse wlrespeed TCP paket işleme:</span><span class="sxs-lookup"><span data-stu-id="cc19b-244">Fast, near wlrespeed TCP packet processing:</span></span>
    * <span data-ttu-id="cc19b-245">100 Mbps Ethernet, MCU @100MHz , 20% MCU ÜZERINDE RX 93 Mbps</span><span class="sxs-lookup"><span data-stu-id="cc19b-245">RX 93 Mbps on 100 Mbps Ethernet, MCU @100MHz, 20% MCU utilization</span></span>
    * <span data-ttu-id="cc19b-246">TX 94 Mbps, 100 Mbps Ethernet, MCU @100MHz , 27% MCU kullanımı</span><span class="sxs-lookup"><span data-stu-id="cc19b-246">TX 94 Mbps on 100 Mbps Ethernet, MCU @100MHz, 27% MCU utilization</span></span>
* <span data-ttu-id="cc19b-247">Güvenilir bağlantı</span><span class="sxs-lookup"><span data-stu-id="cc19b-247">Reliable connection</span></span>
* <span data-ttu-id="cc19b-248">TCP yuvaları sayısında sınırsız</span><span class="sxs-lookup"><span data-stu-id="cc19b-248">No limits on the number of TCP sockets</span></span>
* <span data-ttu-id="cc19b-249">IXIA IxANVL doğrulanan</span><span class="sxs-lookup"><span data-stu-id="cc19b-249">IXIA IxANVL validated</span></span>
* <span data-ttu-id="cc19b-250">Yuva alma/iletme sırasında isteğe bağlı askıya alma</span><span class="sxs-lookup"><span data-stu-id="cc19b-250">Optional suspension on socket receive/transmit</span></span>
* <span data-ttu-id="cc19b-251">Tüm askıya alma sırasında isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="cc19b-251">Optional timeout on all suspension</span></span>
* <span data-ttu-id="cc19b-252">İsteğe bağlı TCP istatistikleri</span><span class="sxs-lookup"><span data-stu-id="cc19b-252">Optional TCP statistics</span></span>
* <span data-ttu-id="cc19b-253">Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme</span><span class="sxs-lookup"><span data-stu-id="cc19b-253">System-level trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="cc19b-254">Sezgisel TCP API 'Leri *: \* nx_tcp_*</span><span class="sxs-lookup"><span data-stu-id="cc19b-254">Intuitive TCP APIs: *nx_tcp_\**</span></span>

### <a name="arprarp"></a><span data-ttu-id="cc19b-255">ARP/RARP</span><span class="sxs-lookup"><span data-stu-id="cc19b-255">ARP/RARP</span></span>

* <span data-ttu-id="cc19b-256">Adres Çözümleme Protokolü (ARP)</span><span class="sxs-lookup"><span data-stu-id="cc19b-256">Address Resolution Protocol (ARP)</span></span>
* <span data-ttu-id="cc19b-257">Ters Adres Çözümleme Protokolü (RARP)</span><span class="sxs-lookup"><span data-stu-id="cc19b-257">Reverse Address Resolution Protocol (RARP)</span></span>
* <span data-ttu-id="cc19b-258">Minimum 1,7 KB FLASH, RAM boyutu</span><span class="sxs-lookup"><span data-stu-id="cc19b-258">Minimal 1.7 KB FLASH, RAM size</span></span>
* <span data-ttu-id="cc19b-259">32-blt IPv4 ve 48-blt MAC adreslerinin dinamik çözünürlüğü</span><span class="sxs-lookup"><span data-stu-id="cc19b-259">Dynamic resolution of 32-blt IPv4 and 48-blt MAC addresses</span></span>
* <span data-ttu-id="cc19b-260">IXIA IxANVL doğrulanan</span><span class="sxs-lookup"><span data-stu-id="cc19b-260">IXIA IxANVL validated</span></span>
* <span data-ttu-id="cc19b-261">Esnek, Kullanıcı tanımlı ARP önbelleği</span><span class="sxs-lookup"><span data-stu-id="cc19b-261">Flexible, user-defined ARP cache</span></span>
* <span data-ttu-id="cc19b-262">Gereksiz ARP desteği</span><span class="sxs-lookup"><span data-stu-id="cc19b-262">Gratuitous ARP support</span></span>
* <span data-ttu-id="cc19b-263">Uygulamaya göre belirlenen isteğe bağlı ARP/RARP istatistikleri</span><span class="sxs-lookup"><span data-stu-id="cc19b-263">Optional ARP/RARP statistics determined by application</span></span>
* <span data-ttu-id="cc19b-264">Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme</span><span class="sxs-lookup"><span data-stu-id="cc19b-264">System-level trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="cc19b-265">Sezgisel ARP/RARP API 'leri *: \* nx_arp_*, *nx_rarp_ \**</span><span class="sxs-lookup"><span data-stu-id="cc19b-265">Intuitive ARP/RARP APIs: *nx_arp_\**, *nx_rarp_\**</span></span>

### <a name="ipv4-amp-ipv6"></a><span data-ttu-id="cc19b-266">IPv4 &amp; IPv6</span><span class="sxs-lookup"><span data-stu-id="cc19b-266">IPv4 &amp; IPv6</span></span>

* <span data-ttu-id="cc19b-267">Internet Protokolü (IP)</span><span class="sxs-lookup"><span data-stu-id="cc19b-267">Internet Protocol (IP)</span></span>
* <span data-ttu-id="cc19b-268">Minimum 3,5 KB-8,5 KB FLASH, 2 KB-3 KB RAM ayak</span><span class="sxs-lookup"><span data-stu-id="cc19b-268">Minimal 3.5 KB to 8.5 KB FLASH, 2 KB to 3 KB RAM footprint</span></span>
* <span data-ttu-id="cc19b-269">Piconet™ mimarisi</span><span class="sxs-lookup"><span data-stu-id="cc19b-269">Piconet™ architecture</span></span>
* <span data-ttu-id="cc19b-270">Hızlı, neredeyse wafklu performans</span><span class="sxs-lookup"><span data-stu-id="cc19b-270">Fast, near wirespeed performance</span></span>
* <span data-ttu-id="cc19b-271">Birden çok arabirim desteği</span><span class="sxs-lookup"><span data-stu-id="cc19b-271">Multiple interface support</span></span>
* <span data-ttu-id="cc19b-272">Çok sayfalı destek</span><span class="sxs-lookup"><span data-stu-id="cc19b-272">Multihomed support</span></span>
* <span data-ttu-id="cc19b-273">Statik yönlendirme desteği</span><span class="sxs-lookup"><span data-stu-id="cc19b-273">Static routing support</span></span>
* <span data-ttu-id="cc19b-274">IP parçalama/yeniden birleştirme desteği</span><span class="sxs-lookup"><span data-stu-id="cc19b-274">IP fragmentation/reassembly support</span></span>
* <span data-ttu-id="cc19b-275">IPv4 ve IPv6 adresi desteği</span><span class="sxs-lookup"><span data-stu-id="cc19b-275">IPv4 and IPv6 address support</span></span>
* <span data-ttu-id="cc19b-276">IXIA IxANVL doğrulanan</span><span class="sxs-lookup"><span data-stu-id="cc19b-276">IXIA IxANVL validated</span></span>
* <span data-ttu-id="cc19b-277">Phase II IPv6 Ready Logo sertifikası</span><span class="sxs-lookup"><span data-stu-id="cc19b-277">Phase II IPv6 Ready Logo Certification</span></span>
* <span data-ttu-id="cc19b-278">İsteğe bağlı IP istatistikleri</span><span class="sxs-lookup"><span data-stu-id="cc19b-278">Optional IP statistics</span></span>
* <span data-ttu-id="cc19b-279">İyi tanımlanmış, sezgisel fiziksel katman sürücü arabirimi</span><span class="sxs-lookup"><span data-stu-id="cc19b-279">Well defined, intuitive physical layer driver interface</span></span>
* <span data-ttu-id="cc19b-280">Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme</span><span class="sxs-lookup"><span data-stu-id="cc19b-280">System-level trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="cc19b-281">Sezgisel IP katmanı API 'leri *: \* nx_ip_*, *nxd_ip_ \**, *nxd_ipv6_ \**</span><span class="sxs-lookup"><span data-stu-id="cc19b-281">Intuitive IP layer APIs: *nx_ip_\**, *nxd_ip_\**, *nxd_ipv6_\**</span></span>
* <span data-ttu-id="cc19b-282">TUV ve UL-ıEC 61508 SIL 4, ıEC 62304 Class C, ISO 26262 asıl D ve EN 50128 SW-SIL4 tarafından ön sertifikalı</span><span class="sxs-lookup"><span data-stu-id="cc19b-282">Pre-certified by TUV and UL to IEC 61508 SIL 4, IEC 62304 Class C, ISO 26262 ASIL D, and EN 50128 SW-SIL4</span></span>

### <a name="azure-rtos-netx-secure-ipsec"></a><span data-ttu-id="cc19b-283">Azure RTOS NetX güvenli ıPSEC</span><span class="sxs-lookup"><span data-stu-id="cc19b-283">Azure RTOS NetX Secure IPSEC</span></span>

* <span data-ttu-id="cc19b-284">Internet Protokolü güvenliği (ıPSEC)</span><span class="sxs-lookup"><span data-stu-id="cc19b-284">Internet Protocol Security (IPSEC)</span></span>
* <span data-ttu-id="cc19b-285">IP katmanı</span><span class="sxs-lookup"><span data-stu-id="cc19b-285">IP layer</span></span>
* <span data-ttu-id="cc19b-286">Donanım şifreleme desteği</span><span class="sxs-lookup"><span data-stu-id="cc19b-286">Hardware crypto support</span></span>
* <span data-ttu-id="cc19b-287">Aşağıdakiler dahil olmak üzere yazılım şifreleme desteği:</span><span class="sxs-lookup"><span data-stu-id="cc19b-287">Software crypto support, including:</span></span>
    * <span data-ttu-id="cc19b-288">DES, 3DES</span><span class="sxs-lookup"><span data-stu-id="cc19b-288">DES, 3DES</span></span>
    * <span data-ttu-id="cc19b-289">AES</span><span class="sxs-lookup"><span data-stu-id="cc19b-289">AES</span></span>
    * <span data-ttu-id="cc19b-290">HMAC-MD5</span><span class="sxs-lookup"><span data-stu-id="cc19b-290">HMAC-MD5</span></span>
    * <span data-ttu-id="cc19b-291">HMAC-SHA1</span><span class="sxs-lookup"><span data-stu-id="cc19b-291">HMAC-SHA1</span></span>
* <span data-ttu-id="cc19b-292">İnternet Anahtar Değişimi (ıKE) sürüm 2 desteği</span><span class="sxs-lookup"><span data-stu-id="cc19b-292">Internet Key Exchange (IKE) Version 2 support</span></span>
* <span data-ttu-id="cc19b-293">Sezgisel IPSec API 'Leri *: \* nx_ipsec_*</span><span class="sxs-lookup"><span data-stu-id="cc19b-293">Intuitive IPsec APIs: *nx_ipsec_\**</span></span>
* <span data-ttu-id="cc19b-294">IPSec yalnızca Azure RTOS NetX Duo ile kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="cc19b-294">IPsec is only available with Azure RTOS NetX Duo</span></span>

## <a name="safe-and-secure"></a><span data-ttu-id="cc19b-295">Güvenli ve güvenli</span><span class="sxs-lookup"><span data-stu-id="cc19b-295">Safe and secure</span></span>

<span data-ttu-id="cc19b-296">Azure RTOS NetX Duo güvenlidir.</span><span class="sxs-lookup"><span data-stu-id="cc19b-296">Azure RTOS NetX Duo is secure.</span></span> <span data-ttu-id="cc19b-297">Bu güvenlik, IPSec, SSL, TLS ve DTLS dahil eklenti güvenlik ürünleri aracılığıyla sağlanır.</span><span class="sxs-lookup"><span data-stu-id="cc19b-297">This security is provided through add-on security products, including IPsec, SSL, TLS, and DTLS.</span></span> <span data-ttu-id="cc19b-298">Ayrıca, uygulamanın Azure RTOS NetX Duo 'e yönelik tüm dış erişimlere yönelik tümüyle denetimi vardır ve güvenlik riski belirleme çok daha kolay hale getirir.</span><span class="sxs-lookup"><span data-stu-id="cc19b-298">Also, the application has complete control over all external access to Azure RTOS NetX Duo, making security risk determination much easier.</span></span>

<span data-ttu-id="cc19b-299">Microsoft Azure RTOS, OEM 'Lere iletişim sağlamak ve temel alınan MCU/MPU donanım koruma mekanizmalarını kullanarak kod ve veri yalıtımı oluşturmak için bileşenleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="cc19b-299">Microsoft Azure RTOS provides OEMs with components to secure communication and to create code and data isolation using underlying MCU/MPU hardware protection mechanisms.</span></span> <span data-ttu-id="cc19b-300">Cihazın, belirli kullanım durumuyla ilişkili gelişen güvenlik gereksinimlerini tam olarak karşıladığından emin olmak için, bu son olarak cihaz oluşturucunun sorumluluğundadır.</span><span class="sxs-lookup"><span data-stu-id="cc19b-300">It is ultimately the responsibility of the device builder to ensure the device fully meets the evolving security requirements associated with its specific use case.</span></span>


## <a name="interoperability-verification"></a><span data-ttu-id="cc19b-301">Birlikte çalışabilirlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="cc19b-301">Interoperability verification</span></span>

<span data-ttu-id="cc19b-302">NetX Duo, RFC standartlarına uyar ve çoğu satıcının cihazlarıyla birlikte çalışabilirlik desteği sunar.</span><span class="sxs-lookup"><span data-stu-id="cc19b-302">NetX Duo conforms to RFC standards and offers complete interoperability with devices for most vendors.</span></span>

![IPv6 Ready logosu](./media/overview-netx-duo/ipv6-ready-logo.png)

<span data-ttu-id="cc19b-304">Azure RTOS NetX Duo, kapsamlı IPv6-Ready logo sertifikasına ulaşmak için yalnızca katıştırılmış TCP/IP yığınlarından biridir. Bu, IPv6 Forumu tarafından yönetilen ve doğrulanan uyumluluk ve birlikte çalışabilirlik testlerini geçti olduğunu kanıtlayın.</span><span class="sxs-lookup"><span data-stu-id="cc19b-304">Azure RTOS NetX Duo is one of the only embedded TCP/IP stacks to achieve the rigorous IPv6-Ready Logo certification, evidence that it has passed conformance and interoperability tests, administered and validated by the IPv6 Forum.</span></span> <span data-ttu-id="cc19b-305">NetX Duo Ayrıca, NetX Duo çekirdek TCP/IP protokol uygulamasının sektör standardı IxANVL (otomatik ağ doğrulama kitaplığı) kullanır.</span><span class="sxs-lookup"><span data-stu-id="cc19b-305">NetX Duo also utilizes the industry standard IxANVL (Automated Network Validation Library) for the NetX Duo core TCP/IP protocol implementation.</span></span>

## <a name="comprehensive-iot-solution"></a><span data-ttu-id="cc19b-306">Kapsamlı IoT çözümü</span><span class="sxs-lookup"><span data-stu-id="cc19b-306">Comprehensive IoT solution</span></span>

<span data-ttu-id="cc19b-307">NetX Duo, derin eklenmiş IoT uygulamaları için en kapsamlı TCP/IP ağıyla biridir.</span><span class="sxs-lookup"><span data-stu-id="cc19b-307">NetX Duo has one of the most comprehensive TCP/IP networking for deeply embedded IoT applications.</span></span> <span data-ttu-id="cc19b-308">Bu destek, aşağıdaki eklenti protokol ürünlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="cc19b-308">This support includes the following add-on protocol products.</span></span>

<span data-ttu-id="cc19b-309">MQTT, CoAP, LWM2M, 6LoWPAN, SSL/TLS/DTLS, IPSec, Oto IP, DHCP, DNS, mDNS, DNS-SD, FTP, HTTP, IPSec, NAT, POP3, PPP, PPPoE, SMTP, SNMP v1/2/3, Telnet, TFTP</span><span class="sxs-lookup"><span data-stu-id="cc19b-309">MQTT, CoAP, LWM2M, 6LoWPAN, SSL/TLS/DTLS, IPsec, AutoIP, DHCP, DNS, mDNS, DNS-SD, FTP, HTTP, IPsec, NAT, POP3, PPP, PPPoE, SMTP, SNMP v1/2/3, Telnet, TFTP</span></span>

## <a name="advanced-technology"></a><span data-ttu-id="cc19b-310">Gelişmiş teknoloji</span><span class="sxs-lookup"><span data-stu-id="cc19b-310">Advanced technology</span></span>

<span data-ttu-id="cc19b-311">Azure RTOS NetX Duo, şunları içeren gelişmiş bir teknolojidir:</span><span class="sxs-lookup"><span data-stu-id="cc19b-311">Azure RTOS NetX Duo is advanced technology that includes:</span></span>

* <span data-ttu-id="cc19b-312">Piconet™ mimarisi</span><span class="sxs-lookup"><span data-stu-id="cc19b-312">Piconet™ architecture</span></span>
* <span data-ttu-id="cc19b-313">Otomatik ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="cc19b-313">Automatic scaling</span></span>
* <span data-ttu-id="cc19b-314">UDP Fast-Path teknolojisi™</span><span class="sxs-lookup"><span data-stu-id="cc19b-314">UDP Fast-Path Technology™</span></span>
* <span data-ttu-id="cc19b-315">Esnek paket yönetimi</span><span class="sxs-lookup"><span data-stu-id="cc19b-315">Flexible packet management</span></span>
* <span data-ttu-id="cc19b-316">Sıfır-API ve uygulama kopyalama</span><span class="sxs-lookup"><span data-stu-id="cc19b-316">Zero-copy API and implementation</span></span>
* <span data-ttu-id="cc19b-317">Çok sayfalı destek</span><span class="sxs-lookup"><span data-stu-id="cc19b-317">Multihomed support</span></span>
* <span data-ttu-id="cc19b-318">Tüm askıya alma sırasında isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="cc19b-318">Optional timeout on all suspension</span></span>
* <span data-ttu-id="cc19b-319">Statik yönlendirme desteği</span><span class="sxs-lookup"><span data-stu-id="cc19b-319">Static routing support</span></span>
* <span data-ttu-id="cc19b-320">IPsec</span><span class="sxs-lookup"><span data-stu-id="cc19b-320">IPsec</span></span>
* <span data-ttu-id="cc19b-321">SSL/TLS/DTLS</span><span class="sxs-lookup"><span data-stu-id="cc19b-321">SSL/TLS/DTLS</span></span>
* <span data-ttu-id="cc19b-322">Azure RTOS TraceX sistem analizi desteği</span><span class="sxs-lookup"><span data-stu-id="cc19b-322">Azure RTOS TraceX system analysis support</span></span>

## <a name="related-services"></a><span data-ttu-id="cc19b-323">İlgili hizmetler</span><span class="sxs-lookup"><span data-stu-id="cc19b-323">Related services</span></span>

<span data-ttu-id="cc19b-324">IoT RTOS güvenlik modülü için Azure Güvenlik Merkezi, Azure RTOS cihazları için kapsamlı bir güvenlik çözümü sağlar.</span><span class="sxs-lookup"><span data-stu-id="cc19b-324">The Azure Security Center for IoT RTOS security module provides a comprehensive security solution for Azure RTOS devices.</span></span> <span data-ttu-id="cc19b-325">Azure RTOS için güvenlik modülü, kötü amaçlı ağ etkinliği algılama, özel uyarı tabanlı cihaz davranışı taban çizgisi sağlar ve cihaz güvenliği Hygiene 'ın artırılmasına yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="cc19b-325">The Security Module for Azure RTOS offers malicious network activity detection, custom alert based device behavior baselining, and helps improve device security hygiene.</span></span> <span data-ttu-id="cc19b-326">[Azure RTOS güvenlik modülü](https://docs.microsoft.com/azure/asc-for-iot/iot-security-azure-rtos) hakkında daha fazla bilgi edinin veya [Azure RTOS hızlı başlangıç Için güvenlik yapılandırması modülünü](https://docs.microsoft.com/azure/asc-for-iot/quickstart-azure-rtos-security-module) kullanmaya başlayın.</span><span class="sxs-lookup"><span data-stu-id="cc19b-326">Learn more about the [Security Module for Azure RTOS](https://docs.microsoft.com/azure/asc-for-iot/iot-security-azure-rtos) or get started with the [Configure Security Module for Azure RTOS](https://docs.microsoft.com/azure/asc-for-iot/quickstart-azure-rtos-security-module) quickstart.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc19b-327">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cc19b-327">Next steps</span></span>

<span data-ttu-id="cc19b-328">NetX Duo hakkında daha fazla bilgi edinmek için [Azure RTOS NetX Duo Kullanıcı kılavuzuyla](about-this-guide.md)başlayın.</span><span class="sxs-lookup"><span data-stu-id="cc19b-328">To learn more about NetX Duo, start with the [Azure RTOS NetX Duo User Guide](about-this-guide.md).</span></span>
