---
title: Azure RTOS NetX Duo 'i anlama
description: Azure RTOS NetX Duo, özellikle de gömülü gerçek zamanlı ve IoT uygulamaları için özel olarak tasarlanan bir gelişmiş, endüstriyel sınıf TCP/IP ağ yığını.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: b40a57bf385ddcf623ff7cbe0d2e798c547227d7
ms.sourcegitcommit: dbbec3ba6a7eb6097c7888b235c433a2efd6e5b9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/14/2021
ms.locfileid: "113754905"
---
# <a name="overview-of-azure-rtos-netx-duo"></a><span data-ttu-id="e7400-103">Azure RTOS NetX Duo 'e genel bakış</span><span class="sxs-lookup"><span data-stu-id="e7400-103">Overview of Azure RTOS NetX Duo</span></span>

<span data-ttu-id="e7400-104">Azure RTOS NetX Duo katıştırılmış TCP/IP ağ yığını, özellikle de daha fazla gömülü, gerçek zamanlı ve IoT uygulamaları için tasarlanan Microsoft 'un gelişmiş, endüstriyel sınıf ikili IPv4 ve IPv6 TCP/IP ağ yığınıdır.</span><span class="sxs-lookup"><span data-stu-id="e7400-104">Azure RTOS NetX Duo embedded TCP/IP network stack is Microsoft's advanced, industrial grade dual IPv4 and IPv6 TCP/IP network stack that is designed specifically for deeply embedded, real-time, and IoT applications.</span></span> <span data-ttu-id="e7400-105">NetX Duo, IPv4, IPv6, TCP ve UDP gibi çekirdek ağ protokollerine ve ek ve daha üst düzey eklenti protokollerinin eksiksiz bir paketini içeren katıştırılmış uygulamalar sağlar.</span><span class="sxs-lookup"><span data-stu-id="e7400-105">NetX Duo provides embedded applications with core network protocols such as IPv4, IPv6, TCP, and UDP as well as a complete suite of additional, higher-level add-on protocols.</span></span> <span data-ttu-id="e7400-106">Azure RTOS NetX Duo, Azure RTOS NetX güvenli IPSec ve Azure RTOS NetX güvenli SSL/TLS/DTLS dahil ek eklenti güvenlik ürünleri aracılığıyla güvenlik sağlar.</span><span class="sxs-lookup"><span data-stu-id="e7400-106">Azure RTOS NetX Duo offers security via additional add-on security products, including Azure RTOS NetX Secure IPsec and Azure RTOS NetX Secure SSL/TLS/DTLS.</span></span> <span data-ttu-id="e7400-107">Bunun hepsi küçük bir ayak izi, Hızlı yürütme ve üstün kullanım kolaylığıyla Azure RTOS NetX Duo, en zorlu ekli IoT uygulamalarına yönelik ideal seçenektir.</span><span class="sxs-lookup"><span data-stu-id="e7400-107">All of this combined with an small footprint, fast execution, and superior ease-of-use make Azure RTOS NetX Duo the ideal choice for the most demanding embedded IoT applications.</span></span>

## <a name="api-protocols"></a><span data-ttu-id="e7400-108">API protokolleri</span><span class="sxs-lookup"><span data-stu-id="e7400-108">API protocols</span></span>

### <a name="mqtt"></a><span data-ttu-id="e7400-109">MQTT</span><span class="sxs-lookup"><span data-stu-id="e7400-109">MQTT</span></span>

* <span data-ttu-id="e7400-110">Mesajlaşma kuyruğu telemetri aktarımı (MQTT)</span><span class="sxs-lookup"><span data-stu-id="e7400-110">Messaging Queue Telemetry Transport (MQTT)</span></span>
* <span data-ttu-id="e7400-111">En az 2,7 KB FLASH</span><span class="sxs-lookup"><span data-stu-id="e7400-111">Minimal 2.7 KB FLASH</span></span>

### <a name="auto-ip"></a><span data-ttu-id="e7400-112">Otomatik IP</span><span class="sxs-lookup"><span data-stu-id="e7400-112">Auto IP</span></span>

* <span data-ttu-id="e7400-113">Otomatik IPv4 adresi ataması</span><span class="sxs-lookup"><span data-stu-id="e7400-113">Automatic IPv4 address assignment</span></span>
* <span data-ttu-id="e7400-114">En az 1,2 KB, 300 bayt RAM</span><span class="sxs-lookup"><span data-stu-id="e7400-114">Minimal 1.2 KB, 300 bytes of RAM</span></span>

### <a name="http-https"></a><span data-ttu-id="e7400-115">HTTP, HTTPS</span><span class="sxs-lookup"><span data-stu-id="e7400-115">HTTP, HTTPS</span></span>
<span data-ttu-id="e7400-116">NetX Duo, aşağıdaki HTTP/HTTPS protokollerini destekler.</span><span class="sxs-lookup"><span data-stu-id="e7400-116">NetX Duo supports the following HTTP/HTTPS protocols.</span></span>

#### <a name="http-10"></a><span data-ttu-id="e7400-117">HTTP 1,0</span><span class="sxs-lookup"><span data-stu-id="e7400-117">HTTP 1.0</span></span>

* <span data-ttu-id="e7400-118">Köprü Metni Aktarım Protokolü (HTTP)</span><span class="sxs-lookup"><span data-stu-id="e7400-118">Hypertext Transfer Protocol(HTTP)</span></span>
* <span data-ttu-id="e7400-119">Minimum 2,8 KB-4,8 KB, FLASH/0,4 KB ile 1,0 KB arasında</span><span class="sxs-lookup"><span data-stu-id="e7400-119">Minimal 2.8 KB to 4.8 KB FLASH / 0.4 KB to 1.0 KB RAM</span></span>
* <span data-ttu-id="e7400-120">İstemci ve sunucu desteği</span><span class="sxs-lookup"><span data-stu-id="e7400-120">Client and server support</span></span>

#### <a name="httphttps-11"></a><span data-ttu-id="e7400-121">HTTP/HTTPS 1,1</span><span class="sxs-lookup"><span data-stu-id="e7400-121">HTTP/HTTPS 1.1</span></span>

* <span data-ttu-id="e7400-122">Köprü Metni Aktarım Protokolü (HTTP)</span><span class="sxs-lookup"><span data-stu-id="e7400-122">Hypertext Transfer Protocol(HTTP)</span></span>
* <span data-ttu-id="e7400-123">Minimum 3,0 KB-9,5 KB FLASH/0,5 KB-2 KB RAM</span><span class="sxs-lookup"><span data-stu-id="e7400-123">Minimal 3.0 KB to 9.5 KB FLASH / 0.5 KB to 2 KB RAM</span></span>
* <span data-ttu-id="e7400-124">İstemci ve sunucu desteği</span><span class="sxs-lookup"><span data-stu-id="e7400-124">Client and server support</span></span>
* <span data-ttu-id="e7400-125">Birden çok gelen istemci oturumu</span><span class="sxs-lookup"><span data-stu-id="e7400-125">Multiple incoming client sessions</span></span>
* <span data-ttu-id="e7400-126">Düz metin ve şifreli HTTPS</span><span class="sxs-lookup"><span data-stu-id="e7400-126">Plain text and encrypted HTTPS</span></span>
* <span data-ttu-id="e7400-127">Kalıcı bağlantı desteği</span><span class="sxs-lookup"><span data-stu-id="e7400-127">Persistent connection support</span></span>
* <span data-ttu-id="e7400-128">Çok parçalı dosya yükleme</span><span class="sxs-lookup"><span data-stu-id="e7400-128">Multipart file upload</span></span>
* <span data-ttu-id="e7400-129">Azure RTOS NetX güvenli TLS ile tam olarak tümleşik</span><span class="sxs-lookup"><span data-stu-id="e7400-129">Fully integrated with Azure RTOS NetX Secure TLS</span></span>

### <a name="smtp"></a><span data-ttu-id="e7400-130">SMTP</span><span class="sxs-lookup"><span data-stu-id="e7400-130">SMTP</span></span>

* <span data-ttu-id="e7400-131">Basit küçük/küçük Aktarım Protokolü (SMTP)</span><span class="sxs-lookup"><span data-stu-id="e7400-131">Simple Mall Transfer Protocol (SMTP)</span></span>
* <span data-ttu-id="e7400-132">En az 4,1 KB ve 0,6 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="e7400-132">Minimal 4.1 KB and 0.6 KB RAM footprint</span></span>
* <span data-ttu-id="e7400-133">İstemci desteği</span><span class="sxs-lookup"><span data-stu-id="e7400-133">Client support</span></span>

### <a name="dhcp"></a><span data-ttu-id="e7400-134">DHCP</span><span class="sxs-lookup"><span data-stu-id="e7400-134">DHCP</span></span>

* <span data-ttu-id="e7400-135">Dinamik Ana Bilgisayar Yapılandırma Protokolü (DHCP)</span><span class="sxs-lookup"><span data-stu-id="e7400-135">Dynamic Host Configuration Protocol (DHCP)</span></span>
* <span data-ttu-id="e7400-136">Minimum 3,6 KB-4,6 KB FLASH, 2,7 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="e7400-136">Minimal 3.6 KB to 4.6 KB FLASH, 2.7 KB RAM footprint</span></span>
* <span data-ttu-id="e7400-137">İstemci ve sunucu desteği</span><span class="sxs-lookup"><span data-stu-id="e7400-137">Client and server support</span></span>
* <span data-ttu-id="e7400-138">IPv4 ve IPv6 desteği</span><span class="sxs-lookup"><span data-stu-id="e7400-138">IPv4 and IPv6 support</span></span>

### <a name="nat"></a><span data-ttu-id="e7400-139">NAT</span><span class="sxs-lookup"><span data-stu-id="e7400-139">NAT</span></span>

* <span data-ttu-id="e7400-140">Ağ Adresi Çevirisi (NAT)</span><span class="sxs-lookup"><span data-stu-id="e7400-140">Network Address Translation (NAT)</span></span>
* <span data-ttu-id="e7400-141">Minimum 3,5 K6 ve 0,6 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="e7400-141">Minimal 3.5K6 and 0.6 KB RAM footprint</span></span>
* <span data-ttu-id="e7400-142">IPv4 adresi desteği</span><span class="sxs-lookup"><span data-stu-id="e7400-142">IPv4 address support</span></span>
* <span data-ttu-id="e7400-143">NAT yalnızca Azure RTOS NetX Duo ile kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="e7400-143">NAT is only available with Azure RTOS NetX Duo</span></span>

### <a name="snmp"></a><span data-ttu-id="e7400-144">SNMP</span><span class="sxs-lookup"><span data-stu-id="e7400-144">SNMP</span></span>

* <span data-ttu-id="e7400-145">Basit Ağ Yönetim Protokolü (SNMP)</span><span class="sxs-lookup"><span data-stu-id="e7400-145">Simple Network Management Protocol (SNMP)</span></span>
* <span data-ttu-id="e7400-146">En az 10,9 KB ve 2,6 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="e7400-146">Minimal 10.9 KB and 2.6 KB RAM footprint</span></span>
* <span data-ttu-id="e7400-147">VI, v2 ve v3 için aracı desteği</span><span class="sxs-lookup"><span data-stu-id="e7400-147">Agent support for VI, V2, and V3</span></span>

### <a name="dns-mdns-dns-sd"></a><span data-ttu-id="e7400-148">DNS, mDNS, DNS-SD</span><span class="sxs-lookup"><span data-stu-id="e7400-148">DNS, mDNS, DNS-SD</span></span>

* <span data-ttu-id="e7400-149">Etki Alanı Adı Sistemi (DNS)</span><span class="sxs-lookup"><span data-stu-id="e7400-149">Domain Name System (DNS)</span></span>
* <span data-ttu-id="e7400-150">Çok noktaya yayın etki alanı adı sistemi (mDNS)</span><span class="sxs-lookup"><span data-stu-id="e7400-150">Multicast Domain Name System (mDNS)</span></span>
* <span data-ttu-id="e7400-151">DNS tabanlı hizmet bulma (DNS-SD)</span><span class="sxs-lookup"><span data-stu-id="e7400-151">DNS-based service discovery (DNS-SD)</span></span>
* <span data-ttu-id="e7400-152">DNS en az 2,4 KB-3 KB FLASH, 1 KB RAM ayak</span><span class="sxs-lookup"><span data-stu-id="e7400-152">DNS Minimal 2.4 KB to 3 KB FLASH, 1 KB RAM footprint</span></span>
* <span data-ttu-id="e7400-153">İstemci desteği</span><span class="sxs-lookup"><span data-stu-id="e7400-153">Client support</span></span>
* <span data-ttu-id="e7400-154">mDNS ve DNS-SD yalnızca Azure RTOS NetX Duo ile kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="e7400-154">mDNS and DNS-SD are only available with Azure RTOS NetX Duo</span></span>

### <a name="pop3"></a><span data-ttu-id="e7400-155">POP3</span><span class="sxs-lookup"><span data-stu-id="e7400-155">POP3</span></span>

* <span data-ttu-id="e7400-156">Post Office protokolü sürüm 3 (POP3)</span><span class="sxs-lookup"><span data-stu-id="e7400-156">Post Office Protocol Version 3 (POP3)</span></span>
* <span data-ttu-id="e7400-157">En az 8,1 KB ve 1,4 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="e7400-157">Minimal 8.1 KB and 1.4 KB RAM footprint</span></span>
* <span data-ttu-id="e7400-158">İstemci desteği</span><span class="sxs-lookup"><span data-stu-id="e7400-158">Client support</span></span>

### <a name="telnet"></a><span data-ttu-id="e7400-159">Sun</span><span class="sxs-lookup"><span data-stu-id="e7400-159">TELNET</span></span>

* <span data-ttu-id="e7400-160">En az 0,5 KB ve 0,3 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="e7400-160">Minimal 0.5 KB and 0.3 KB RAM footprint</span></span>
* <span data-ttu-id="e7400-161">İstemci ve sunucu desteği</span><span class="sxs-lookup"><span data-stu-id="e7400-161">Client and server support</span></span>
* <span data-ttu-id="e7400-162">Sezgisel Telnet API 'Leri *: \* nx_telnet_*</span><span class="sxs-lookup"><span data-stu-id="e7400-162">Intuitive Telnet APIs: *nx_telnet_\**</span></span>

### <a name="ftp-tftp"></a><span data-ttu-id="e7400-163">FTP, TFTP</span><span class="sxs-lookup"><span data-stu-id="e7400-163">FTP, TFTP</span></span>

* <span data-ttu-id="e7400-164">Dosya Aktarım Protokolü (FTP)</span><span class="sxs-lookup"><span data-stu-id="e7400-164">File Transfer Protocol (FTP)</span></span>
* <span data-ttu-id="e7400-165">Önemsiz Dosya Aktarım İletişim Kuralı (TFTP)</span><span class="sxs-lookup"><span data-stu-id="e7400-165">Trivial File Transfer Protocol (TFTP)</span></span>
* <span data-ttu-id="e7400-166">FTP en az 1,8 KB-7,2 KB FLASH, 0,6 KB ile 2,1 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="e7400-166">FTP Minimal 1.8 KB to 7.2 KB FLASH, 0.6 KB to 2.1 KB RAM footprint</span></span>
* <span data-ttu-id="e7400-167">TFTP en az 1,7 KB-2,4 KB FLASH, 0,3 KB ile 1,8 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="e7400-167">TFTP Minimal 1.7 KB to 2.4 KB FLASH, 0.3 KB to 1.8 KB RAM footprint</span></span>
* <span data-ttu-id="e7400-168">İstemci ve sunucu desteği</span><span class="sxs-lookup"><span data-stu-id="e7400-168">Client and server support</span></span>
* <span data-ttu-id="e7400-169">Sezgisel FTP ve TFTP API 'Leri *: \* nx_ftp_* veya *nx_tftp_ \**</span><span class="sxs-lookup"><span data-stu-id="e7400-169">Intuitive FTP and TFTP APIs: *nx_ftp_\** or *nx_tftp_\**</span></span>

### <a name="ppp-pppoe"></a><span data-ttu-id="e7400-170">PPP, PPPoE</span><span class="sxs-lookup"><span data-stu-id="e7400-170">PPP, PPPoE</span></span>

* <span data-ttu-id="e7400-171">POlNT noktadan noktaya Protokolü (PPP)</span><span class="sxs-lookup"><span data-stu-id="e7400-171">Polnt-to-PoInt Protocol (PPP)</span></span>
* <span data-ttu-id="e7400-172">Ethernet üzerinden Noktadan Noktaya Protokolü (PPPoE)</span><span class="sxs-lookup"><span data-stu-id="e7400-172">Point-to-Point Protocol over Ethernet(PPPoE)</span></span>
* <span data-ttu-id="e7400-173">En az 7,1 KB ve 3,8 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="e7400-173">Minimal 7.1 KB and 3.8 KB RAM footprint</span></span>
* <span data-ttu-id="e7400-174">Sezgisel PPP API 'Leri *: \* nx_ppp_*</span><span class="sxs-lookup"><span data-stu-id="e7400-174">Intuitive PPP APIs: *nx_ppp_\**</span></span>

* <span data-ttu-id="e7400-175">PPPoE yalnızca Azure RTOS NetX Duo ile kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="e7400-175">PPPoE is only available with Azure RTOS NetX Duo</span></span>

### <a name="sntp"></a><span data-ttu-id="e7400-176">SNTP</span><span class="sxs-lookup"><span data-stu-id="e7400-176">SNTP</span></span>

* <span data-ttu-id="e7400-177">Basit ağ zaman Protokolü (SNTP)</span><span class="sxs-lookup"><span data-stu-id="e7400-177">Simple Network Time Protocol (SNTP)</span></span>
* <span data-ttu-id="e7400-178">En az 4 KB ve 0,5 KB RAM</span><span class="sxs-lookup"><span data-stu-id="e7400-178">Minimal 4 KB and 0.5 KB RAM</span></span>
* <span data-ttu-id="e7400-179">İstemci desteği</span><span class="sxs-lookup"><span data-stu-id="e7400-179">Client support</span></span>
* <span data-ttu-id="e7400-180">Sezgisel SNTP API 'Leri *: \* nx_sntp_*</span><span class="sxs-lookup"><span data-stu-id="e7400-180">Intuitive SNTP APIs: *nx_sntp_\**</span></span>

### <a name="legacy-code-support"></a><span data-ttu-id="e7400-181">Eski kod desteği</span><span class="sxs-lookup"><span data-stu-id="e7400-181">Legacy code support</span></span>

* <span data-ttu-id="e7400-182">Eski yuva kodu taşıma için isteğe bağlı BSD katmanı</span><span class="sxs-lookup"><span data-stu-id="e7400-182">Optional BSD layer for porting legacy socket code</span></span>

### <a name="igmp"></a><span data-ttu-id="e7400-183">IGMP</span><span class="sxs-lookup"><span data-stu-id="e7400-183">IGMP</span></span>

* <span data-ttu-id="e7400-184">Internet Grup Yönetimi Protokolü (IGMP)</span><span class="sxs-lookup"><span data-stu-id="e7400-184">Internet Group Management Protocol (IGMP)</span></span>
* <span data-ttu-id="e7400-185">En az 2,5 KB FLASH</span><span class="sxs-lookup"><span data-stu-id="e7400-185">Minimal 2.5 KB FLASH</span></span>
* <span data-ttu-id="e7400-186">IPv4 çok noktaya yayın grubu desteği</span><span class="sxs-lookup"><span data-stu-id="e7400-186">IPv4 multicast group support</span></span>
* <span data-ttu-id="e7400-187">IXIA IxANVL doğrulanan</span><span class="sxs-lookup"><span data-stu-id="e7400-187">IXIA IxANVL validated</span></span>
* <span data-ttu-id="e7400-188">İsteğe bağlı ıGMP istatistikleri</span><span class="sxs-lookup"><span data-stu-id="e7400-188">Optional IGMP statistics</span></span>
* <span data-ttu-id="e7400-189">Azure RTOS ThreadX aracılığıyla sistem düzeyinde izleme</span><span class="sxs-lookup"><span data-stu-id="e7400-189">System-level trace via Azure RTOS ThreadX</span></span>
* <span data-ttu-id="e7400-190">Sezgisel ıGMP API 'Leri *: \* nx_igmp_*</span><span class="sxs-lookup"><span data-stu-id="e7400-190">Intuitive IGMP APIs: *nx_igmp_\**</span></span>

### <a name="azure-rtos-netx-secure-dtls"></a><span data-ttu-id="e7400-191">Azure RTOS NetX güvenli DTLS</span><span class="sxs-lookup"><span data-stu-id="e7400-191">Azure RTOS NetX Secure DTLS</span></span>

* <span data-ttu-id="e7400-192">Veri birimi Aktarım Katmanı Güvenliği (DTLS) 1,0 ve 1,2</span><span class="sxs-lookup"><span data-stu-id="e7400-192">Datagram Transport Layer Security (DTLS) 1.0 and 1.2</span></span>
* <span data-ttu-id="e7400-193">En az 11 KB FLASH</span><span class="sxs-lookup"><span data-stu-id="e7400-193">Minimal 11 KB FLASH</span></span>
* <span data-ttu-id="e7400-194">Fast, Software RSA 2048-bit anahtar boyutu ~ 1-saniye @120MHz</span><span class="sxs-lookup"><span data-stu-id="e7400-194">Fast, software RSA 2048-bit key size ~1-second @120MHz</span></span>
* <span data-ttu-id="e7400-195">Kolaylaştırılmış X. 509.440 uygulama</span><span class="sxs-lookup"><span data-stu-id="e7400-195">Streamlined X.509 Implementation</span></span>
* <span data-ttu-id="e7400-196">Azure RTOS NetX Duo UDP yuvaları ile tam olarak tümleşik</span><span class="sxs-lookup"><span data-stu-id="e7400-196">Fully integrated with Azure RTOS NetX Duo UDP sockets</span></span>
* <span data-ttu-id="e7400-197">Donanım şifreleme desteği</span><span class="sxs-lookup"><span data-stu-id="e7400-197">Hardware Crypto Support</span></span>
* <span data-ttu-id="e7400-198">Yazılım şifreleme desteği: RSA (tüm anahtar boyutları), AES, DES/3DES, ECC, HMAC, MD5, SHA-1, SHA-2 (SHA-224, SHA-256, SHA-384, SHA-512)</span><span class="sxs-lookup"><span data-stu-id="e7400-198">Software Crypto Support: RSA (all key sizes), AES, DES/3DES, ECC, HMAC, MD5, SHA-1, SHA-2 (SHA-224, SHA-256, SHA-384, SHA-512)</span></span>
* <span data-ttu-id="e7400-199">P eğrileri 192/224/256/384/521 dahil olmak üzere ECDSA (imzalama) ve ECDH (şifreleme) ile Eliptik Eğri Şifreleme (ECC)</span><span class="sxs-lookup"><span data-stu-id="e7400-199">Elliptic Curve Cryptography (ECC) with ECDSA (signing) and ECDH (encryption), including P-curves 192/224/256/384/521</span></span>
* <span data-ttu-id="e7400-200">Şifrelenmiş anahtar desteği (donanıma bağımlı)</span><span class="sxs-lookup"><span data-stu-id="e7400-200">Encrypted Key Support (hardware dependent)</span></span>

### <a name="azure-rtos-netx-secure-tls"></a><span data-ttu-id="e7400-201">Azure RTOS NetX Secure TLS</span><span class="sxs-lookup"><span data-stu-id="e7400-201">Azure RTOS NetX Secure TLS</span></span>

* <span data-ttu-id="e7400-202">Aktarım Katmanı Güvenliği (TLS) 1.0, 1.1 ve 1.2</span><span class="sxs-lookup"><span data-stu-id="e7400-202">Transport Layer Security (TLS) 1.0, 1.1, and 1.2</span></span>
* <span data-ttu-id="e7400-203">En az 8,8 KB FLASH</span><span class="sxs-lookup"><span data-stu-id="e7400-203">Minimal 8.8 KB FLASH</span></span>
* <span data-ttu-id="e7400-204">Hızlı, yazılım RSA 2048 bit anahtar boyutu ~1 saniye @120MHz</span><span class="sxs-lookup"><span data-stu-id="e7400-204">Fast, software RSA 2048-bit key size ~1-second @120MHz</span></span>
* <span data-ttu-id="e7400-205">Kolaylaştırılmış X.509 Uygulaması</span><span class="sxs-lookup"><span data-stu-id="e7400-205">Streamlined X.509 Implementation</span></span>
* <span data-ttu-id="e7400-206">NetX Duo TCP Azure RTOS tam olarak tümleştirilmiştir</span><span class="sxs-lookup"><span data-stu-id="e7400-206">Fully integrated with Azure RTOS NetX Duo TCP sockets</span></span>
* <span data-ttu-id="e7400-207">Donanım Şifreleme Desteği</span><span class="sxs-lookup"><span data-stu-id="e7400-207">Hardware Crypto Support</span></span>
* <span data-ttu-id="e7400-208">Yazılım Şifreleme Desteği: RSA (tüm anahtar boyutları), AES, DES/3DES, ECC, HMAC, MD5, SHA-1, SHA-2 (SHA-224, SHA-256, SHA-384, SHA-512)</span><span class="sxs-lookup"><span data-stu-id="e7400-208">Software Crypto Support: RSA (all key sizes), AES, DES/3DES, ECC, HMAC, MD5, SHA-1, SHA-2 (SHA-224, SHA-256, SHA-384, SHA-512)</span></span>
* <span data-ttu-id="e7400-209">P eğrileri 192/224/256/384/521 dahil ECDSA (imzalama) ve ECDH (şifreleme) ile Üç Nokta Eğri Şifrelemesi (ECC)</span><span class="sxs-lookup"><span data-stu-id="e7400-209">Elliptic Curve Cryptography (ECC) with ECDSA (signing) and ECDH (encryption), including P-curves 192/224/256/384/521</span></span>
* <span data-ttu-id="e7400-210">Şifrelenmiş Anahtar Desteği (donanıma bağımlı)</span><span class="sxs-lookup"><span data-stu-id="e7400-210">Encrypted Key Support (hardware dependent)</span></span>

### <a name="icmp"></a><span data-ttu-id="e7400-211">ICMP</span><span class="sxs-lookup"><span data-stu-id="e7400-211">ICMP</span></span>

* <span data-ttu-id="e7400-212">İnternet Denetim İletisi Protokolü (ICMP)</span><span class="sxs-lookup"><span data-stu-id="e7400-212">Internet Control Message Protocol (ICMP)</span></span>
* <span data-ttu-id="e7400-213">En az 2,5 KB FLASH</span><span class="sxs-lookup"><span data-stu-id="e7400-213">Minimal 2.5 KB FLASH</span></span>
* <span data-ttu-id="e7400-214">IPv4 ve IPv6 desteği</span><span class="sxs-lookup"><span data-stu-id="e7400-214">IPv4 and IPv6 support</span></span>
* <span data-ttu-id="e7400-215">I HIP IxANVL doğrulandı</span><span class="sxs-lookup"><span data-stu-id="e7400-215">IXIA IxANVL validated</span></span>
* <span data-ttu-id="e7400-216">Ping isteği ve ping yanıtı</span><span class="sxs-lookup"><span data-stu-id="e7400-216">Ping request and ping response</span></span>
* <span data-ttu-id="e7400-217">Ping istekleri üzerinde isteğe bağlı iş parçacığının askıya alınması</span><span class="sxs-lookup"><span data-stu-id="e7400-217">Optional thread suspension on ping requests</span></span>
* <span data-ttu-id="e7400-218">Tüm askıya almada isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="e7400-218">Optional timeout on all suspension</span></span>
* <span data-ttu-id="e7400-219">İsteğe bağlı ICMP istatistikleri</span><span class="sxs-lookup"><span data-stu-id="e7400-219">Optional ICMP statistics</span></span>
* <span data-ttu-id="e7400-220">Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme</span><span class="sxs-lookup"><span data-stu-id="e7400-220">System-level trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="e7400-221">Sezgisel ICMP API'leri: *nx_icmp_ \**</span><span class="sxs-lookup"><span data-stu-id="e7400-221">Intuitive ICMP APIs: *nx_icmp_\**</span></span>

### <a name="udp"></a><span data-ttu-id="e7400-222">UDP</span><span class="sxs-lookup"><span data-stu-id="e7400-222">UDP</span></span>

* <span data-ttu-id="e7400-223">Kullanıcı Veri Birimi Protokolü (UDP)</span><span class="sxs-lookup"><span data-stu-id="e7400-223">User Datagram Protocol (UDP)</span></span>
* <span data-ttu-id="e7400-224">En az 2,5 KB FLASH, yuva başına 124 yuva bayt RAM</span><span class="sxs-lookup"><span data-stu-id="e7400-224">Minimal 2.5 KB FLASH, 124 sockets bytes of RAM per socket</span></span>
* <span data-ttu-id="e7400-225">Hızlı, kabloya yakın TCP paket işleme:</span><span class="sxs-lookup"><span data-stu-id="e7400-225">Fast, near wirespeed TCP packet processing:</span></span>
    * <span data-ttu-id="e7400-226">100 Mb/sn Ethernet üzerinde RX 95 Mb/sn, MCU @100MHz , %14 MCU kullanımı</span><span class="sxs-lookup"><span data-stu-id="e7400-226">RX 95 Mbps on 100 Mbps Ethernet, MCU @100MHz, 14% MCU utilization</span></span>
    * <span data-ttu-id="e7400-227">100 Mb/sn Ethernet üzerinde TX 94 Mb/sn, MCU @100MHz , %10 MCU kullanımı</span><span class="sxs-lookup"><span data-stu-id="e7400-227">TX 94 Mbps on 100 Mbps Ethernet, MCU @100MHz, 10% MCU utilization</span></span>
* <span data-ttu-id="e7400-228">UDP Hızlı Yolu™ teknolojisi</span><span class="sxs-lookup"><span data-stu-id="e7400-228">UDP Fast Path™ technology</span></span>
* <span data-ttu-id="e7400-229">UDP sayısıyla ilgili sınır yok</span><span class="sxs-lookup"><span data-stu-id="e7400-229">No limits on the number of UDP</span></span>
* <span data-ttu-id="e7400-230">I HIP IxANVL doğrulandı</span><span class="sxs-lookup"><span data-stu-id="e7400-230">IXIA IxANVL validated</span></span>
* <span data-ttu-id="e7400-231">Yuva almada isteğe bağlı askıya alma</span><span class="sxs-lookup"><span data-stu-id="e7400-231">Optional suspension on socket receive</span></span>
* <span data-ttu-id="e7400-232">Tüm askıya almada isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="e7400-232">Optional timeout on all suspension</span></span>
* <span data-ttu-id="e7400-233">İsteğe bağlı UDP istatistikleri</span><span class="sxs-lookup"><span data-stu-id="e7400-233">Optional UDP statistics</span></span>
* <span data-ttu-id="e7400-234">Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme</span><span class="sxs-lookup"><span data-stu-id="e7400-234">System-level trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="e7400-235">Sezgisel UDP API'leri: *nx_udp_ \**</span><span class="sxs-lookup"><span data-stu-id="e7400-235">Intuitive UDP APIs: *nx_udp_\**</span></span>

### <a name="tcp"></a><span data-ttu-id="e7400-236">TCP</span><span class="sxs-lookup"><span data-stu-id="e7400-236">TCP</span></span>

* <span data-ttu-id="e7400-237">İletim Denetimi Protokolü (TCP)</span><span class="sxs-lookup"><span data-stu-id="e7400-237">Transmission Control Protocol (TCP)</span></span>
* <span data-ttu-id="e7400-238">En az 10,5K8 ile 12,5 KB FLASH, yuva başına 280 bayt RAM</span><span class="sxs-lookup"><span data-stu-id="e7400-238">Minimal 10.5K8 to 12.5 KB FLASH, 280 bytes of RAM per socket</span></span>
* <span data-ttu-id="e7400-239">Hızlı, neredeyse wlrespeed TCP paket işleme:</span><span class="sxs-lookup"><span data-stu-id="e7400-239">Fast, near wlrespeed TCP packet processing:</span></span>
    * <span data-ttu-id="e7400-240">100 Mb/sn Ethernet üzerinde RX 93 Mb/sn, MCU @100MHz , %20 MCU kullanımı</span><span class="sxs-lookup"><span data-stu-id="e7400-240">RX 93 Mbps on 100 Mbps Ethernet, MCU @100MHz, 20% MCU utilization</span></span>
    * <span data-ttu-id="e7400-241">100 Mb/sn Ethernet üzerinde TX 94 Mb/sn, MCU @100MHz , %27 MCU kullanımı</span><span class="sxs-lookup"><span data-stu-id="e7400-241">TX 94 Mbps on 100 Mbps Ethernet, MCU @100MHz, 27% MCU utilization</span></span>
* <span data-ttu-id="e7400-242">Güvenilir bağlantı</span><span class="sxs-lookup"><span data-stu-id="e7400-242">Reliable connection</span></span>
* <span data-ttu-id="e7400-243">TCP yuvalarının sayısıyla ilgili sınır yok</span><span class="sxs-lookup"><span data-stu-id="e7400-243">No limits on the number of TCP sockets</span></span>
* <span data-ttu-id="e7400-244">I HIP IxANVL doğrulandı</span><span class="sxs-lookup"><span data-stu-id="e7400-244">IXIA IxANVL validated</span></span>
* <span data-ttu-id="e7400-245">Yuva alma/iletmede isteğe bağlı askıya alma</span><span class="sxs-lookup"><span data-stu-id="e7400-245">Optional suspension on socket receive/transmit</span></span>
* <span data-ttu-id="e7400-246">Tüm askıya almada isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="e7400-246">Optional timeout on all suspension</span></span>
* <span data-ttu-id="e7400-247">İsteğe bağlı TCP istatistikleri</span><span class="sxs-lookup"><span data-stu-id="e7400-247">Optional TCP statistics</span></span>
* <span data-ttu-id="e7400-248">Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme</span><span class="sxs-lookup"><span data-stu-id="e7400-248">System-level trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="e7400-249">Sezgisel TCP API'leri: *nx_tcp_ \**</span><span class="sxs-lookup"><span data-stu-id="e7400-249">Intuitive TCP APIs: *nx_tcp_\**</span></span>

### <a name="arprarp"></a><span data-ttu-id="e7400-250">ARP/RARP</span><span class="sxs-lookup"><span data-stu-id="e7400-250">ARP/RARP</span></span>

* <span data-ttu-id="e7400-251">Adres Çözümleme Protokolü (ARP)</span><span class="sxs-lookup"><span data-stu-id="e7400-251">Address Resolution Protocol (ARP)</span></span>
* <span data-ttu-id="e7400-252">Ters Adres Çözümleme Protokolü (RARP)</span><span class="sxs-lookup"><span data-stu-id="e7400-252">Reverse Address Resolution Protocol (RARP)</span></span>
* <span data-ttu-id="e7400-253">En az 1,7 KB FLASH, RAM boyutu</span><span class="sxs-lookup"><span data-stu-id="e7400-253">Minimal 1.7 KB FLASH, RAM size</span></span>
* <span data-ttu-id="e7400-254">32 blt IPv4 ve 48 blt MAC adreslerinin dinamik çözümlemesi</span><span class="sxs-lookup"><span data-stu-id="e7400-254">Dynamic resolution of 32-blt IPv4 and 48-blt MAC addresses</span></span>
* <span data-ttu-id="e7400-255">I HIP IxANVL doğrulandı</span><span class="sxs-lookup"><span data-stu-id="e7400-255">IXIA IxANVL validated</span></span>
* <span data-ttu-id="e7400-256">Esnek, kullanıcı tanımlı ARP önbelleği</span><span class="sxs-lookup"><span data-stu-id="e7400-256">Flexible, user-defined ARP cache</span></span>
* <span data-ttu-id="e7400-257">Gratuitous ARP desteği</span><span class="sxs-lookup"><span data-stu-id="e7400-257">Gratuitous ARP support</span></span>
* <span data-ttu-id="e7400-258">Uygulama tarafından belirlenen isteğe bağlı ARP/RARP istatistikleri</span><span class="sxs-lookup"><span data-stu-id="e7400-258">Optional ARP/RARP statistics determined by application</span></span>
* <span data-ttu-id="e7400-259">Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme</span><span class="sxs-lookup"><span data-stu-id="e7400-259">System-level trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="e7400-260">Sezgisel ARP/RARP *API'leri: \* nx_arp_*, *\* nx_rarp_*</span><span class="sxs-lookup"><span data-stu-id="e7400-260">Intuitive ARP/RARP APIs: *nx_arp_\**, *nx_rarp_\**</span></span>

### <a name="ipv4-amp-ipv6"></a><span data-ttu-id="e7400-261">IPv4 &amp; IPv6</span><span class="sxs-lookup"><span data-stu-id="e7400-261">IPv4 &amp; IPv6</span></span>

* <span data-ttu-id="e7400-262">İnternet Protokolü (IP)</span><span class="sxs-lookup"><span data-stu-id="e7400-262">Internet Protocol (IP)</span></span>
* <span data-ttu-id="e7400-263">En az 3,5 KB ile 8,5 KB FLASH, 2 KB ile 3 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="e7400-263">Minimal 3.5 KB to 8.5 KB FLASH, 2 KB to 3 KB RAM footprint</span></span>
* <span data-ttu-id="e7400-264">Piconet™ mimarisi</span><span class="sxs-lookup"><span data-stu-id="e7400-264">Piconet™ architecture</span></span>
* <span data-ttu-id="e7400-265">Hızlı, kablolara yakın performans</span><span class="sxs-lookup"><span data-stu-id="e7400-265">Fast, near wirespeed performance</span></span>
* <span data-ttu-id="e7400-266">Birden çok arabirim desteği</span><span class="sxs-lookup"><span data-stu-id="e7400-266">Multiple interface support</span></span>
* <span data-ttu-id="e7400-267">Birden çok ana bilgisayar desteği</span><span class="sxs-lookup"><span data-stu-id="e7400-267">Multihomed support</span></span>
* <span data-ttu-id="e7400-268">Statik yönlendirme desteği</span><span class="sxs-lookup"><span data-stu-id="e7400-268">Static routing support</span></span>
* <span data-ttu-id="e7400-269">IP parçalanması/yeniden değerlendirme desteği</span><span class="sxs-lookup"><span data-stu-id="e7400-269">IP fragmentation/reassembly support</span></span>
* <span data-ttu-id="e7400-270">IPv4 ve IPv6 adresi desteği</span><span class="sxs-lookup"><span data-stu-id="e7400-270">IPv4 and IPv6 address support</span></span>
* <span data-ttu-id="e7400-271">I HIP IxANVL doğrulandı</span><span class="sxs-lookup"><span data-stu-id="e7400-271">IXIA IxANVL validated</span></span>
* <span data-ttu-id="e7400-272">Aşama II IPv6 Hazır Logo Sertifikası</span><span class="sxs-lookup"><span data-stu-id="e7400-272">Phase II IPv6 Ready Logo Certification</span></span>
* <span data-ttu-id="e7400-273">İsteğe bağlı IP istatistikleri</span><span class="sxs-lookup"><span data-stu-id="e7400-273">Optional IP statistics</span></span>
* <span data-ttu-id="e7400-274">İyi tanımlanmış, sezgisel fiziksel katman sürücü arabirimi</span><span class="sxs-lookup"><span data-stu-id="e7400-274">Well defined, intuitive physical layer driver interface</span></span>
* <span data-ttu-id="e7400-275">Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme</span><span class="sxs-lookup"><span data-stu-id="e7400-275">System-level trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="e7400-276">Sezgisel IP katmanı *API'leri: nx_ip_, \** *nxd_ip_ \** *\** , nxd_ipv6_</span><span class="sxs-lookup"><span data-stu-id="e7400-276">Intuitive IP layer APIs: *nx_ip_\**, *nxd_ip_\**, *nxd_ipv6_\**</span></span>
* <span data-ttu-id="e7400-277">TTROP ve UL tarafından IEC 61508 SIL 4, IEC 62304 Sınıf C, ISO 26262 SONA D ve EN 50128 SW-SIL4 için önceden sertifikalıdır</span><span class="sxs-lookup"><span data-stu-id="e7400-277">Pre-certified by TUV and UL to IEC 61508 SIL 4, IEC 62304 Class C, ISO 26262 ASIL D, and EN 50128 SW-SIL4</span></span>

### <a name="azure-rtos-netx-secure-ipsec"></a><span data-ttu-id="e7400-278">Azure RTOS NetX Güvenli IPSEC</span><span class="sxs-lookup"><span data-stu-id="e7400-278">Azure RTOS NetX Secure IPSEC</span></span>

* <span data-ttu-id="e7400-279">İnternet Protokolü Güvenliği (IPSEC)</span><span class="sxs-lookup"><span data-stu-id="e7400-279">Internet Protocol Security (IPSEC)</span></span>
* <span data-ttu-id="e7400-280">IP katmanı</span><span class="sxs-lookup"><span data-stu-id="e7400-280">IP layer</span></span>
* <span data-ttu-id="e7400-281">Donanım şifreleme desteği</span><span class="sxs-lookup"><span data-stu-id="e7400-281">Hardware crypto support</span></span>
* <span data-ttu-id="e7400-282">Yazılım şifreleme desteği, şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="e7400-282">Software crypto support, including:</span></span>
    * <span data-ttu-id="e7400-283">DES, 3DES</span><span class="sxs-lookup"><span data-stu-id="e7400-283">DES, 3DES</span></span>
    * <span data-ttu-id="e7400-284">AES</span><span class="sxs-lookup"><span data-stu-id="e7400-284">AES</span></span>
    * <span data-ttu-id="e7400-285">HMAC-MD5</span><span class="sxs-lookup"><span data-stu-id="e7400-285">HMAC-MD5</span></span>
    * <span data-ttu-id="e7400-286">HMAC-SHA1</span><span class="sxs-lookup"><span data-stu-id="e7400-286">HMAC-SHA1</span></span>
* <span data-ttu-id="e7400-287">İnternet Anahtar Exchange (IKE) Sürüm 2 desteği</span><span class="sxs-lookup"><span data-stu-id="e7400-287">Internet Key Exchange (IKE) Version 2 support</span></span>
* <span data-ttu-id="e7400-288">Sezgisel IPsec API'leri: *nx_ipsec_ \**</span><span class="sxs-lookup"><span data-stu-id="e7400-288">Intuitive IPsec APIs: *nx_ipsec_\**</span></span>
* <span data-ttu-id="e7400-289">IPsec yalnızca NetX Duo Azure RTOS kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="e7400-289">IPsec is only available with Azure RTOS NetX Duo</span></span>

## <a name="safe-and-secure"></a><span data-ttu-id="e7400-290">Kasa ve güvenli</span><span class="sxs-lookup"><span data-stu-id="e7400-290">Safe and secure</span></span>

<span data-ttu-id="e7400-291">Azure RTOS NetX Duo güvenlidir.</span><span class="sxs-lookup"><span data-stu-id="e7400-291">Azure RTOS NetX Duo is secure.</span></span> <span data-ttu-id="e7400-292">Bu güvenlik, IPsec, SSL, TLS ve DTLS gibi ek güvenlik ürünleri aracılığıyla sağlanır.</span><span class="sxs-lookup"><span data-stu-id="e7400-292">This security is provided through add-on security products, including IPsec, SSL, TLS, and DTLS.</span></span> <span data-ttu-id="e7400-293">Ayrıca uygulamanın NetX Duo'ya tüm dış erişim üzerinde tam Azure RTOS güvenlik riski belirlemeyi çok daha kolay hale getirmiştir.</span><span class="sxs-lookup"><span data-stu-id="e7400-293">Also, the application has complete control over all external access to Azure RTOS NetX Duo, making security risk determination much easier.</span></span>

<span data-ttu-id="e7400-294">Microsoft Azure RTOS, OEM'lere iletişimin güvenliğini sağlamak ve temel MCU/MPU donanım koruma mekanizmalarını kullanarak kod ve veri yalıtımı oluşturmak için bileşenler sağlar.</span><span class="sxs-lookup"><span data-stu-id="e7400-294">Microsoft Azure RTOS provides OEMs with components to secure communication and to create code and data isolation using underlying MCU/MPU hardware protection mechanisms.</span></span> <span data-ttu-id="e7400-295">Son olarak cihaz oluşturucusu, cihazın kendi özel kullanım durumuyla ilişkili gelişen güvenlik gereksinimlerini tam olarak karşılamasını sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="e7400-295">It is ultimately the responsibility of the device builder to ensure the device fully meets the evolving security requirements associated with its specific use case.</span></span>

## <a name="interoperability-verification"></a><span data-ttu-id="e7400-296">Birlikte çalışabilirlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="e7400-296">Interoperability verification</span></span>

<span data-ttu-id="e7400-297">NetX Duo RFC standartlarına uygundur ve çoğu satıcı için cihazlarla tam birlikte çalışabilirlik sunar.</span><span class="sxs-lookup"><span data-stu-id="e7400-297">NetX Duo conforms to RFC standards and offers complete interoperability with devices for most vendors.</span></span>

![IPv6 Hazır Logosu](./media/overview-netx-duo/ipv6-ready-logo.png)

<span data-ttu-id="e7400-299">Azure RTOS NetX Duo, sıkı IPv6-Ready Logo sertifikası elde etmek için ekli tek TCP/IP yığınlarından biri, uyumluluk ve birlikte çalışabilirlik testlerinden geçmiş olduğuna dair kanıt, IPv6 Forumu tarafından yönetildi ve doğrulandı.</span><span class="sxs-lookup"><span data-stu-id="e7400-299">Azure RTOS NetX Duo is one of the only embedded TCP/IP stacks to achieve the rigorous IPv6-Ready Logo certification, evidence that it has passed conformance and interoperability tests, administered and validated by the IPv6 Forum.</span></span> <span data-ttu-id="e7400-300">NetX Duo ayrıca NetX Duo çekirdek TCP/IP protokolü uygulaması için endüstri standardı IxANVL (Otomatik Ağ Doğrulama Kitaplığı) kullanır.</span><span class="sxs-lookup"><span data-stu-id="e7400-300">NetX Duo also utilizes the industry standard IxANVL (Automated Network Validation Library) for the NetX Duo core TCP/IP protocol implementation.</span></span>

## <a name="comprehensive-iot-solution"></a><span data-ttu-id="e7400-301">Kapsamlı IoT çözümü</span><span class="sxs-lookup"><span data-stu-id="e7400-301">Comprehensive IoT solution</span></span>

<span data-ttu-id="e7400-302">NetX Duo, derinden eklenmiş IoT uygulamaları için en kapsamlı TCP/IP ağlarından birini içerir.</span><span class="sxs-lookup"><span data-stu-id="e7400-302">NetX Duo has one of the most comprehensive TCP/IP networking for deeply embedded IoT applications.</span></span> <span data-ttu-id="e7400-303">Bu destek aşağıdaki eklenti protokol ürünlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="e7400-303">This support includes the following add-on protocol products.</span></span>

* <span data-ttu-id="e7400-304">MQTT</span><span class="sxs-lookup"><span data-stu-id="e7400-304">MQTT</span></span>
* <span data-ttu-id="e7400-305">CoAP</span><span class="sxs-lookup"><span data-stu-id="e7400-305">CoAP</span></span>
* <span data-ttu-id="e7400-306">LWM2M</span><span class="sxs-lookup"><span data-stu-id="e7400-306">LWM2M</span></span>
* <span data-ttu-id="e7400-307">6LoWPAN</span><span class="sxs-lookup"><span data-stu-id="e7400-307">6LoWPAN</span></span>
* <span data-ttu-id="e7400-308">SSL/TLS/DTLS</span><span class="sxs-lookup"><span data-stu-id="e7400-308">SSL/TLS/DTLS</span></span>
* <span data-ttu-id="e7400-309">IPsec</span><span class="sxs-lookup"><span data-stu-id="e7400-309">IPsec</span></span>
* <span data-ttu-id="e7400-310">AutoIP</span><span class="sxs-lookup"><span data-stu-id="e7400-310">AutoIP</span></span>
* <span data-ttu-id="e7400-311">DHCP</span><span class="sxs-lookup"><span data-stu-id="e7400-311">DHCP</span></span>
* <span data-ttu-id="e7400-312">DNS</span><span class="sxs-lookup"><span data-stu-id="e7400-312">DNS</span></span>
* <span data-ttu-id="e7400-313">Mdns</span><span class="sxs-lookup"><span data-stu-id="e7400-313">mDNS</span></span>
* <span data-ttu-id="e7400-314">DNS-SD</span><span class="sxs-lookup"><span data-stu-id="e7400-314">DNS-SD</span></span>
* <span data-ttu-id="e7400-315">FTP</span><span class="sxs-lookup"><span data-stu-id="e7400-315">FTP</span></span>
* <span data-ttu-id="e7400-316">HTTP</span><span class="sxs-lookup"><span data-stu-id="e7400-316">HTTP</span></span>
* <span data-ttu-id="e7400-317">IPsec</span><span class="sxs-lookup"><span data-stu-id="e7400-317">IPsec</span></span>
* <span data-ttu-id="e7400-318">NAT</span><span class="sxs-lookup"><span data-stu-id="e7400-318">NAT</span></span>
* <span data-ttu-id="e7400-319">POP3</span><span class="sxs-lookup"><span data-stu-id="e7400-319">POP3</span></span>
* <span data-ttu-id="e7400-320">Ppp</span><span class="sxs-lookup"><span data-stu-id="e7400-320">PPP</span></span>
* <span data-ttu-id="e7400-321">Pppoe</span><span class="sxs-lookup"><span data-stu-id="e7400-321">PPPoE</span></span>
* <span data-ttu-id="e7400-322">SMTP</span><span class="sxs-lookup"><span data-stu-id="e7400-322">SMTP</span></span>
* <span data-ttu-id="e7400-323">SNMP v1/2/3</span><span class="sxs-lookup"><span data-stu-id="e7400-323">SNMP v1/2/3</span></span>
* <span data-ttu-id="e7400-324">Telnet</span><span class="sxs-lookup"><span data-stu-id="e7400-324">Telnet</span></span>
* <span data-ttu-id="e7400-325">Tftp</span><span class="sxs-lookup"><span data-stu-id="e7400-325">TFTP</span></span>

## <a name="advanced-technology"></a><span data-ttu-id="e7400-326">Gelişmiş teknoloji</span><span class="sxs-lookup"><span data-stu-id="e7400-326">Advanced technology</span></span>

<span data-ttu-id="e7400-327">Azure RTOS NetX Duo, aşağıdakilere sahip gelişmiş bir teknolojidir.</span><span class="sxs-lookup"><span data-stu-id="e7400-327">Azure RTOS NetX Duo is advanced technology that includes the following.</span></span>

* <span data-ttu-id="e7400-328">Piconet™ mimarisi</span><span class="sxs-lookup"><span data-stu-id="e7400-328">Piconet™ architecture</span></span>
* <span data-ttu-id="e7400-329">Otomatik ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="e7400-329">Automatic scaling</span></span>
* <span data-ttu-id="e7400-330">UDP Fast-Path Technology™</span><span class="sxs-lookup"><span data-stu-id="e7400-330">UDP Fast-Path Technology™</span></span>
* <span data-ttu-id="e7400-331">Esnek paket yönetimi</span><span class="sxs-lookup"><span data-stu-id="e7400-331">Flexible packet management</span></span>
* <span data-ttu-id="e7400-332">Sıfır kopya API'si ve uygulaması</span><span class="sxs-lookup"><span data-stu-id="e7400-332">Zero-copy API and implementation</span></span>
* <span data-ttu-id="e7400-333">Birden çok ana bilgisayar desteği</span><span class="sxs-lookup"><span data-stu-id="e7400-333">Multihomed support</span></span>
* <span data-ttu-id="e7400-334">Tüm askıya almada isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="e7400-334">Optional timeout on all suspension</span></span>
* <span data-ttu-id="e7400-335">Statik yönlendirme desteği</span><span class="sxs-lookup"><span data-stu-id="e7400-335">Static routing support</span></span>
* <span data-ttu-id="e7400-336">IPsec</span><span class="sxs-lookup"><span data-stu-id="e7400-336">IPsec</span></span>
* <span data-ttu-id="e7400-337">SSL/TLS/DTLS</span><span class="sxs-lookup"><span data-stu-id="e7400-337">SSL/TLS/DTLS</span></span>
* <span data-ttu-id="e7400-338">Azure RTOS TraceX sistem analizi desteği</span><span class="sxs-lookup"><span data-stu-id="e7400-338">Azure RTOS TraceX system analysis support</span></span>

## <a name="related-services"></a><span data-ttu-id="e7400-339">İlgili hizmetler</span><span class="sxs-lookup"><span data-stu-id="e7400-339">Related services</span></span>

<span data-ttu-id="e7400-340">NetX Duo aşağıdaki ek hizmetleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="e7400-340">NetX Duo provides the following additional services.</span></span>

* <span data-ttu-id="e7400-341">Azure IoT Ara Yazılımı</span><span class="sxs-lookup"><span data-stu-id="e7400-341">Azure IoT Middleware</span></span>
* <span data-ttu-id="e7400-342">Azure Defender</span><span class="sxs-lookup"><span data-stu-id="e7400-342">Azure Defender</span></span>
* <span data-ttu-id="e7400-343">IoT Hub için cihaz güncelleştirmesi.</span><span class="sxs-lookup"><span data-stu-id="e7400-343">Device update for IoT Hub.</span></span>

### <a name="azure-iot-middleware"></a><span data-ttu-id="e7400-344">Azure IoT Ara Yazılımı</span><span class="sxs-lookup"><span data-stu-id="e7400-344">Azure IoT Middleware</span></span>

<span data-ttu-id="e7400-345">NetX Duo, Azure IoT hizmetleriyle bağlantıyı kolaylaştırmak için Azure RTOS ile Embedded C için Azure SDK arasında bağlama katmanı olarak hareket eden platforma özgü bir kitaplık olan Azure RTOS için [Azure IoT Ara](https://github.com/azure-rtos/netxduo/blob/master/addons/azure_iot/docs/README.md)Yazılımı'na sahiptir.</span><span class="sxs-lookup"><span data-stu-id="e7400-345">NetX Duo includes [Azure IoT Middleware for Azure RTOS](https://github.com/azure-rtos/netxduo/blob/master/addons/azure_iot/docs/README.md), a platform-specific library that acts as a binding layer between the Azure RTOS and the Azure SDK for Embedded C to facilitate connectivity to Azure IoT services.</span></span> <span data-ttu-id="e7400-346">Azure IoT Ara Yazılımı'nın hedefleri aşağıdaki gibidir.</span><span class="sxs-lookup"><span data-stu-id="e7400-346">The goals of Azure IoT Middleware are the following.</span></span>
* <span data-ttu-id="e7400-347">Geliştiricilerin uygulamaları için ihtiyaç IoTHub_Client (DeviceProvisioning_Client, uygulama arabirimi) akıllı istemci arabirimlerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="e7400-347">Provide the smart client interfaces (IoTHub_Client, DeviceProvisioning_Client) that developers need for their applications.</span></span>
* <span data-ttu-id="e7400-348">Embedded C SDK'sı ile platform arasındaki etkileşimi düzenleme.</span><span class="sxs-lookup"><span data-stu-id="e7400-348">Orchestrate the interaction between the Embedded C SDK and the platform.</span></span>
* <span data-ttu-id="e7400-349">Platform Azure RTOS sağlama.</span><span class="sxs-lookup"><span data-stu-id="e7400-349">Provide Azure RTOS platform initialization.</span></span>
* <span data-ttu-id="e7400-350">IoT Tak Çalıştır desteği.</span><span class="sxs-lookup"><span data-stu-id="e7400-350">IoT Plug and Play support.</span></span>
* <span data-ttu-id="e7400-351">Güvenlik özellikleri.</span><span class="sxs-lookup"><span data-stu-id="e7400-351">Security capabilities.</span></span>
* <span data-ttu-id="e7400-352">Kaynak sınırlamaya dikkat.</span><span class="sxs-lookup"><span data-stu-id="e7400-352">Resource limitation aware.</span></span>
* <span data-ttu-id="e7400-353">Protokol desteği.</span><span class="sxs-lookup"><span data-stu-id="e7400-353">Protocol support.</span></span>

![Azure RTOS NetX Duo ile İlgili Hizmetler](./media/overview-netx-duo/related-services.png)

### <a name="azure-defender"></a><span data-ttu-id="e7400-355">Azure Defender</span><span class="sxs-lookup"><span data-stu-id="e7400-355">Azure Defender</span></span>

<span data-ttu-id="e7400-356">Yeni IoT için Azure Defender modülü, cihazlarınız için kapsamlı bir güvenlik Azure RTOS sağlar.</span><span class="sxs-lookup"><span data-stu-id="e7400-356">The Azure Defender for IoT security module provides a comprehensive security solution for Azure RTOS devices.</span></span> <span data-ttu-id="e7400-357">Azure RTOS için Güvenlik Modülü kötü amaçlı ağ etkinliği algılama, özel uyarı tabanlı cihaz davranışı temel oluşturma ve cihaz güvenlik durumu iyileştirmeye yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="e7400-357">The Security Module for Azure RTOS offers malicious network activity detection, custom alert based device behavior baselining, and helps improve device security hygiene.</span></span> <span data-ttu-id="e7400-358">Azure RTOS için [Güvenlik Modülü hakkında](https://docs.microsoft.com/azure/asc-for-iot/iot-security-azure-rtos) daha fazla bilgi edinmek veya hızlı başlangıç için Güvenlik [Modülünü Azure RTOS](https://docs.microsoft.com/azure/asc-for-iot/quickstart-azure-rtos-security-module) başlama.</span><span class="sxs-lookup"><span data-stu-id="e7400-358">Learn more about the [Security Module for Azure RTOS](https://docs.microsoft.com/azure/asc-for-iot/iot-security-azure-rtos) or get started with the [Configure Security Module for Azure RTOS](https://docs.microsoft.com/azure/asc-for-iot/quickstart-azure-rtos-security-module) quickstart.</span></span>

### <a name="device-update-for-iot-hub"></a><span data-ttu-id="e7400-359">IoT Hub için Cihaz Güncelleştirmesi</span><span class="sxs-lookup"><span data-stu-id="e7400-359">Device Update for IoT Hub</span></span>

<span data-ttu-id="e7400-360">IoT Hub için [Azure Cihaz](https://docs.microsoft.com/azure/iot-hub-device-update/understand-device-update) Güncelleştirmesi, IoT cihazlarınız için havadan güncelleştirmeleri (OTA) dağıtmanıza olanak sağlayan bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="e7400-360">The [Azure Device Update for IoT Hub](https://docs.microsoft.com/azure/iot-hub-device-update/understand-device-update) is a service that enables you to deploy over-the-air updates (OTA) for your IoT devices.</span></span> <span data-ttu-id="e7400-361">IoT Hub için Cihaz Güncelleştirmesi modülü, NetX Duo'da IoT Hub Agent için Cihaz Azure RTOS uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="e7400-361">The Device Update for IoT Hub module is the implementation of Device Update for IoT Hub Agent in Azure RTOS NetX Duo.</span></span> <span data-ttu-id="e7400-362">Cihaz oluşturucularının Cihaz Güncelleştirmesi özelliğini uygulamalarıyla tümleştiren basit API'ler sağlar.</span><span class="sxs-lookup"><span data-stu-id="e7400-362">It provides simple APIs for device builders to integrate the Device Update capability in their application.</span></span>

<span data-ttu-id="e7400-363">Cihazlara havadan (OTA) güncelleştirmeleri yapılandırmayı, derlemeyi ve dağıtmayı öğrenmek için başlama kılavuzlarını içeren temel yarı iletken değerlendirme panoları örneklerine bakın.</span><span class="sxs-lookup"><span data-stu-id="e7400-363">See the samples of key semiconductors evaluation boards that include the get started guides to learn configure, build and deploy the over-the-air (OTA) updates to the devices.</span></span>

<span data-ttu-id="e7400-364">Ayrıca, Azure RTOS ile cihaz için [Cihaz Güncelleştirmesi'IoT Hub kullanma hakkında daha fazla Azure RTOS.](https://docs.microsoft.com/azure/iot-hub-device-update/device-update-azure-real-time-operating-system)</span><span class="sxs-lookup"><span data-stu-id="e7400-364">And you can learn more details about use [Device Update for IoT Hub with Azure RTOS](https://docs.microsoft.com/azure/iot-hub-device-update/device-update-azure-real-time-operating-system).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e7400-365">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e7400-365">Next steps</span></span>

<span data-ttu-id="e7400-366">NetX Duo hakkında daha fazla bilgi edinmek için netx [duo Azure RTOS kılavuzu ile çalışmaya başlayabilirsiniz.](about-this-guide.md)</span><span class="sxs-lookup"><span data-stu-id="e7400-366">To learn more about NetX Duo, start with the [Azure RTOS NetX Duo User Guide](about-this-guide.md).</span></span>
