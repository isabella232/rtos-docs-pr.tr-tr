---
title: NetX Duo Azure RTOS anlama
description: Azure RTOS NetX Duo gelişmiş ve endüstriyel düzeyde bir TCP/IP ağ yığınıdır. Bu yığın özellikle derin eklenmiş gerçek zamanlı ve IoT uygulamaları için tasarlanmıştır.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: 6112ab5cb711ca1a5c83fd5cd4b43abc0302c6c5
ms.sourcegitcommit: f9d8cf23becf96d5bd6d31dd54f89c48962fd09b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111549347"
---
# <a name="overview-of-azure-rtos-netx-duo"></a><span data-ttu-id="f8560-103">Azure RTOS NetX Duo'ya genel bakış</span><span class="sxs-lookup"><span data-stu-id="f8560-103">Overview of Azure RTOS NetX Duo</span></span>

<span data-ttu-id="f8560-104">Azure RTOS NetX Duo ekli TCP/IP ağ yığını, Microsoft'un ayrıntılı, gerçek zamanlı ve IoT uygulamaları için özel olarak tasarlanmış gelişmiş, endüstriyel sınıf çift IPv4 ve IPv6 TCP/IP ağ yığınıdır.</span><span class="sxs-lookup"><span data-stu-id="f8560-104">Azure RTOS NetX Duo embedded TCP/IP network stack is Microsoft's advanced, industrial grade dual IPv4 and IPv6 TCP/IP network stack that is designed specifically for deeply embedded, real-time, and IoT applications.</span></span> <span data-ttu-id="f8560-105">NetX Duo; IPv4, IPv6, TCP ve UDP gibi temel ağ protokollerinin yanı sıra ek, üst düzey eklenti protokollerinin eksiksiz bir paketini içeren tümleşik uygulamalar sağlar.</span><span class="sxs-lookup"><span data-stu-id="f8560-105">NetX Duo provides embedded applications with core network protocols such as IPv4, IPv6, TCP, and UDP as well as a complete suite of additional, higher-level add-on protocols.</span></span> <span data-ttu-id="f8560-106">Azure RTOS NetX Duo, Azure RTOS NetX Secure IPsec ve Azure RTOS NetX Secure SSL/TLS/DTLS gibi ek ek güvenlik ürünleri aracılığıyla güvenlik sunar.</span><span class="sxs-lookup"><span data-stu-id="f8560-106">Azure RTOS NetX Duo offers security via additional add-on security products, including Azure RTOS NetX Secure IPsec and Azure RTOS NetX Secure SSL/TLS/DTLS.</span></span> <span data-ttu-id="f8560-107">Bunların hepsi küçük bir ayak izi, hızlı yürütme ve üstün kullanım kolaylığıyla bir araya Azure RTOS NetX Duo'yu en zorlu tümleşik IoT uygulamaları için ideal seçenektir.</span><span class="sxs-lookup"><span data-stu-id="f8560-107">All of this combined with an small footprint, fast execution, and superior ease-of-use make Azure RTOS NetX Duo the ideal choice for the most demanding embedded IoT applications.</span></span>

## <a name="api-protocols"></a><span data-ttu-id="f8560-108">API protokolleri</span><span class="sxs-lookup"><span data-stu-id="f8560-108">API protocols</span></span>

### <a name="mqtt"></a><span data-ttu-id="f8560-109">MQTT</span><span class="sxs-lookup"><span data-stu-id="f8560-109">MQTT</span></span>

* <span data-ttu-id="f8560-110">Mesajlaşma Kuyruğu Telemetri Taşıma (MQTT)</span><span class="sxs-lookup"><span data-stu-id="f8560-110">Messaging Queue Telemetry Transport (MQTT)</span></span>
* <span data-ttu-id="f8560-111">En az 2,7 KB FLASH</span><span class="sxs-lookup"><span data-stu-id="f8560-111">Minimal 2.7 KB FLASH</span></span>

### <a name="auto-ip"></a><span data-ttu-id="f8560-112">Otomatik IP</span><span class="sxs-lookup"><span data-stu-id="f8560-112">Auto IP</span></span>

* <span data-ttu-id="f8560-113">Otomatik IPv4 adres ataması</span><span class="sxs-lookup"><span data-stu-id="f8560-113">Automatic IPv4 address assignment</span></span>
* <span data-ttu-id="f8560-114">En az 1,2 KB, 300 bayt RAM</span><span class="sxs-lookup"><span data-stu-id="f8560-114">Minimal 1.2 KB, 300 bytes of RAM</span></span>

### <a name="http-https"></a><span data-ttu-id="f8560-115">HTTP, HTTPS</span><span class="sxs-lookup"><span data-stu-id="f8560-115">HTTP, HTTPS</span></span>

#### <a name="http-10"></a><span data-ttu-id="f8560-116">HTTP 1.0</span><span class="sxs-lookup"><span data-stu-id="f8560-116">HTTP 1.0</span></span>

* <span data-ttu-id="f8560-117">Köprü Metni Aktarım Protokolü (HTTP)</span><span class="sxs-lookup"><span data-stu-id="f8560-117">Hypertext Transfer Protocol(HTTP)</span></span>
* <span data-ttu-id="f8560-118">En az 2,8 KB - 4,8 KB FLASH / 0,4 KB ile 1,0 KB RAM</span><span class="sxs-lookup"><span data-stu-id="f8560-118">Minimal 2.8 KB to 4.8 KB FLASH / 0.4 KB to 1.0 KB RAM</span></span>
* <span data-ttu-id="f8560-119">İstemci ve sunucu desteği</span><span class="sxs-lookup"><span data-stu-id="f8560-119">Client and server support</span></span>

#### <a name="httphttps-11"></a><span data-ttu-id="f8560-120">HTTP/HTTPS 1.1</span><span class="sxs-lookup"><span data-stu-id="f8560-120">HTTP/HTTPS 1.1</span></span>

* <span data-ttu-id="f8560-121">Köprü Metni Aktarım Protokolü (HTTP)</span><span class="sxs-lookup"><span data-stu-id="f8560-121">Hypertext Transfer Protocol(HTTP)</span></span>
* <span data-ttu-id="f8560-122">En az 3,0 KB ile 9,5 KB FLASH / 0,5 KB ile 2 KB RAM arasında</span><span class="sxs-lookup"><span data-stu-id="f8560-122">Minimal 3.0 KB to 9.5 KB FLASH / 0.5 KB to 2 KB RAM</span></span>
* <span data-ttu-id="f8560-123">İstemci ve sunucu desteği</span><span class="sxs-lookup"><span data-stu-id="f8560-123">Client and server support</span></span>
* <span data-ttu-id="f8560-124">Birden çok gelen istemci oturumu</span><span class="sxs-lookup"><span data-stu-id="f8560-124">Multiple incoming client sessions</span></span>
* <span data-ttu-id="f8560-125">Düz metin ve şifrelenmiş HTTPS</span><span class="sxs-lookup"><span data-stu-id="f8560-125">Plain text and encrypted HTTPS</span></span>
* <span data-ttu-id="f8560-126">Kalıcı bağlantı desteği</span><span class="sxs-lookup"><span data-stu-id="f8560-126">Persistent connection support</span></span>
* <span data-ttu-id="f8560-127">Çok parçalı dosyayı karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="f8560-127">Multipart file upload</span></span>
* <span data-ttu-id="f8560-128">NetX Secure TLS Azure RTOS tam olarak tümleştirilmiştir</span><span class="sxs-lookup"><span data-stu-id="f8560-128">Fully integrated with Azure RTOS NetX Secure TLS</span></span>

### <a name="smtp"></a><span data-ttu-id="f8560-129">SMTP</span><span class="sxs-lookup"><span data-stu-id="f8560-129">SMTP</span></span>

* <span data-ttu-id="f8560-130">Basit Alışveriş Aktarım Protokolü (SMTP)</span><span class="sxs-lookup"><span data-stu-id="f8560-130">Simple Mall Transfer Protocol (SMTP)</span></span>
* <span data-ttu-id="f8560-131">En az 4,1 KB ve 0,6 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="f8560-131">Minimal 4.1 KB and 0.6 KB RAM footprint</span></span>
* <span data-ttu-id="f8560-132">İstemci desteği</span><span class="sxs-lookup"><span data-stu-id="f8560-132">Client support</span></span>

### <a name="dhcp"></a><span data-ttu-id="f8560-133">DHCP</span><span class="sxs-lookup"><span data-stu-id="f8560-133">DHCP</span></span>

* <span data-ttu-id="f8560-134">Dinamik Ana Bilgisayar Yapılandırma Protokolü (DHCP)</span><span class="sxs-lookup"><span data-stu-id="f8560-134">Dynamic Host Configuration Protocol (DHCP)</span></span>
* <span data-ttu-id="f8560-135">En az 3,6 KB ile 4,6 KB FLASH, 2,7 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="f8560-135">Minimal 3.6 KB to 4.6 KB FLASH, 2.7 KB RAM footprint</span></span>
* <span data-ttu-id="f8560-136">İstemci ve sunucu desteği</span><span class="sxs-lookup"><span data-stu-id="f8560-136">Client and server support</span></span>
* <span data-ttu-id="f8560-137">IPv4 ve IPv6 desteği</span><span class="sxs-lookup"><span data-stu-id="f8560-137">IPv4 and IPv6 support</span></span>

### <a name="nat"></a><span data-ttu-id="f8560-138">NAT</span><span class="sxs-lookup"><span data-stu-id="f8560-138">NAT</span></span>

* <span data-ttu-id="f8560-139">Ağ Adresi Çevirisi (NAT)</span><span class="sxs-lookup"><span data-stu-id="f8560-139">Network Address Translation (NAT)</span></span>
* <span data-ttu-id="f8560-140">En az 3,5K6 ve 0,6 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="f8560-140">Minimal 3.5K6 and 0.6 KB RAM footprint</span></span>
* <span data-ttu-id="f8560-141">IPv4 adres desteği</span><span class="sxs-lookup"><span data-stu-id="f8560-141">IPv4 address support</span></span>
* <span data-ttu-id="f8560-142">NAT yalnızca NetX Duo Azure RTOS kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="f8560-142">NAT is only available with Azure RTOS NetX Duo</span></span>

### <a name="snmp"></a><span data-ttu-id="f8560-143">SNMP</span><span class="sxs-lookup"><span data-stu-id="f8560-143">SNMP</span></span>

* <span data-ttu-id="f8560-144">Basit Ağ Yönetim Protokolü (SNMP)</span><span class="sxs-lookup"><span data-stu-id="f8560-144">Simple Network Management Protocol (SNMP)</span></span>
* <span data-ttu-id="f8560-145">En az 10,9 KB ve 2,6 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="f8560-145">Minimal 10.9 KB and 2.6 KB RAM footprint</span></span>
* <span data-ttu-id="f8560-146">VI, V2 ve V3 için aracı desteği</span><span class="sxs-lookup"><span data-stu-id="f8560-146">Agent support for VI, V2, and V3</span></span>

### <a name="dns-mdns-dns-sd"></a><span data-ttu-id="f8560-147">DNS, mDNS, DNS-SD</span><span class="sxs-lookup"><span data-stu-id="f8560-147">DNS, mDNS, DNS-SD</span></span>

* <span data-ttu-id="f8560-148">Etki Alanı Adı Sistemi (DNS)</span><span class="sxs-lookup"><span data-stu-id="f8560-148">Domain Name System (DNS)</span></span>
* <span data-ttu-id="f8560-149">Çok Noktaya Yayın Etki Alanı Adı Sistemi (mDNS)</span><span class="sxs-lookup"><span data-stu-id="f8560-149">Multicast Domain Name System (mDNS)</span></span>
* <span data-ttu-id="f8560-150">DNS tabanlı hizmet bulma (DNS-SD)</span><span class="sxs-lookup"><span data-stu-id="f8560-150">DNS-based service discovery (DNS-SD)</span></span>
* <span data-ttu-id="f8560-151">DNS En Az 2,4 KB ile 3 KB FLASH, 1 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="f8560-151">DNS Minimal 2.4 KB to 3 KB FLASH, 1 KB RAM footprint</span></span>
* <span data-ttu-id="f8560-152">İstemci desteği</span><span class="sxs-lookup"><span data-stu-id="f8560-152">Client support</span></span>
* <span data-ttu-id="f8560-153">mDNS ve DNS-SD yalnızca NetX Duo Azure RTOS kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="f8560-153">mDNS and DNS-SD are only available with Azure RTOS NetX Duo</span></span>

### <a name="pop3"></a><span data-ttu-id="f8560-154">POP3</span><span class="sxs-lookup"><span data-stu-id="f8560-154">POP3</span></span>

* <span data-ttu-id="f8560-155">Post Office Protocol Version 3 (POP3)</span><span class="sxs-lookup"><span data-stu-id="f8560-155">Post Office Protocol Version 3 (POP3)</span></span>
* <span data-ttu-id="f8560-156">En az 8,1 KB ve 1,4 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="f8560-156">Minimal 8.1 KB and 1.4 KB RAM footprint</span></span>
* <span data-ttu-id="f8560-157">İstemci desteği</span><span class="sxs-lookup"><span data-stu-id="f8560-157">Client support</span></span>

### <a name="telnet"></a><span data-ttu-id="f8560-158">Telnet</span><span class="sxs-lookup"><span data-stu-id="f8560-158">TELNET</span></span>

* <span data-ttu-id="f8560-159">En az 0,5 KB ve 0,3 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="f8560-159">Minimal 0.5 KB and 0.3 KB RAM footprint</span></span>
* <span data-ttu-id="f8560-160">İstemci ve sunucu desteği</span><span class="sxs-lookup"><span data-stu-id="f8560-160">Client and server support</span></span>
* <span data-ttu-id="f8560-161">Sezgisel Telnet API'leri: *nx_telnet_ \**</span><span class="sxs-lookup"><span data-stu-id="f8560-161">Intuitive Telnet APIs: *nx_telnet_\**</span></span>

### <a name="ftp-tftp"></a><span data-ttu-id="f8560-162">FTP, TFTP</span><span class="sxs-lookup"><span data-stu-id="f8560-162">FTP, TFTP</span></span>

* <span data-ttu-id="f8560-163">Dosya Aktarım Protokolü (FTP)</span><span class="sxs-lookup"><span data-stu-id="f8560-163">File Transfer Protocol (FTP)</span></span>
* <span data-ttu-id="f8560-164">Önemsiz Dosya Aktarım İletişim Kuralı (TFTP)</span><span class="sxs-lookup"><span data-stu-id="f8560-164">Trivial File Transfer Protocol (TFTP)</span></span>
* <span data-ttu-id="f8560-165">FTP En Az 1,8 KB ile 7,2 KB FLASH, 0,6 KB ile 2,1 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="f8560-165">FTP Minimal 1.8 KB to 7.2 KB FLASH, 0.6 KB to 2.1 KB RAM footprint</span></span>
* <span data-ttu-id="f8560-166">TFTP En Az 1,7 KB ile 2,4 KB FLASH, 0,3 KB ile 1,8 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="f8560-166">TFTP Minimal 1.7 KB to 2.4 KB FLASH, 0.3 KB to 1.8 KB RAM footprint</span></span>
* <span data-ttu-id="f8560-167">İstemci ve sunucu desteği</span><span class="sxs-lookup"><span data-stu-id="f8560-167">Client and server support</span></span>
* <span data-ttu-id="f8560-168">Sezgisel FTP ve TFTP *API'leri: nx_ftp_ \** veya *nx_tftp_ \**</span><span class="sxs-lookup"><span data-stu-id="f8560-168">Intuitive FTP and TFTP APIs: *nx_ftp_\** or *nx_tftp_\**</span></span>

### <a name="ppp-pppoe"></a><span data-ttu-id="f8560-169">PPP, PPPoE</span><span class="sxs-lookup"><span data-stu-id="f8560-169">PPP, PPPoE</span></span>

* <span data-ttu-id="f8560-170">Polnt-to-PoInt Protokolü (PPP)</span><span class="sxs-lookup"><span data-stu-id="f8560-170">Polnt-to-PoInt Protocol (PPP)</span></span>
* <span data-ttu-id="f8560-171">Noktadan Noktaya Protokolü Ethernet (PPPoE) üzerinden bağlantı</span><span class="sxs-lookup"><span data-stu-id="f8560-171">Point-to-Point Protocol over Ethernet(PPPoE)</span></span>
* <span data-ttu-id="f8560-172">En az 7,1 KB ve 3,8 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="f8560-172">Minimal 7.1 KB and 3.8 KB RAM footprint</span></span>
* <span data-ttu-id="f8560-173">Sezgisel PPP API'leri: *nx_ppp_ \**</span><span class="sxs-lookup"><span data-stu-id="f8560-173">Intuitive PPP APIs: *nx_ppp_\**</span></span>

* <span data-ttu-id="f8560-174">PPPoE yalnızca NetX Duo Azure RTOS kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="f8560-174">PPPoE is only available with Azure RTOS NetX Duo</span></span>

### <a name="sntp"></a><span data-ttu-id="f8560-175">SNTP</span><span class="sxs-lookup"><span data-stu-id="f8560-175">SNTP</span></span>

* <span data-ttu-id="f8560-176">Basit Ağ Zamanı Protokolü (SNTP)</span><span class="sxs-lookup"><span data-stu-id="f8560-176">Simple Network Time Protocol (SNTP)</span></span>
* <span data-ttu-id="f8560-177">En az 4 KB ve 0,5 KB RAM</span><span class="sxs-lookup"><span data-stu-id="f8560-177">Minimal 4 KB and 0.5 KB RAM</span></span>
* <span data-ttu-id="f8560-178">İstemci desteği</span><span class="sxs-lookup"><span data-stu-id="f8560-178">Client support</span></span>
* <span data-ttu-id="f8560-179">Sezgisel SNTP API'leri: *nx_sntp_ \**</span><span class="sxs-lookup"><span data-stu-id="f8560-179">Intuitive SNTP APIs: *nx_sntp_\**</span></span>

### <a name="azure-rtos-netx-duo-api"></a><span data-ttu-id="f8560-180">Azure RTOS NetX Duo API'si</span><span class="sxs-lookup"><span data-stu-id="f8560-180">Azure RTOS NetX Duo API</span></span>

* <span data-ttu-id="f8560-181">Sezgisel ve tutarlı API</span><span class="sxs-lookup"><span data-stu-id="f8560-181">Intuitive and consistent API</span></span>
* <span data-ttu-id="f8560-182">İsim-fiil adlandırma kuralı</span><span class="sxs-lookup"><span data-stu-id="f8560-182">Noun-verb naming convention</span></span>
* <span data-ttu-id="f8560-183">Hızlı, sıfır kopya API'si uygulaması</span><span class="sxs-lookup"><span data-stu-id="f8560-183">Fast, zero-copy API implementation</span></span>
* <span data-ttu-id="f8560-184">Tüm API'ler NetX <i>nx_ kolayca</i> tanımlamak için önde gelen Azure RTOS\* sahip</span><span class="sxs-lookup"><span data-stu-id="f8560-184">All APIs have leading <i>nx_\*</i> to easily identify as Azure RTOS NetX</span></span>
* <span data-ttu-id="f8560-185">Engelleme API'lerinde isteğe bağlı iş parçacığı zaman aşımı var</span><span class="sxs-lookup"><span data-stu-id="f8560-185">Blocking APIs have optional thread timeout</span></span>
* <span data-ttu-id="f8560-186">Daha [Azure RTOS için bkz. NetX Duo](about-this-guide.md) Kullanıcı Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="f8560-186">See [Azure RTOS NetX Duo User Guide](about-this-guide.md) for more details</span></span>
* <span data-ttu-id="f8560-187">Eski yuva kodunun taşınabilirliği için isteğe bağlı BSD katmanı</span><span class="sxs-lookup"><span data-stu-id="f8560-187">Optional BSD layer for porting legacy socket code</span></span>

### <a name="igmp"></a><span data-ttu-id="f8560-188">ıgmp</span><span class="sxs-lookup"><span data-stu-id="f8560-188">IGMP</span></span>

* <span data-ttu-id="f8560-189">Internet Grup Yönetimi Protokolü (IGMP)</span><span class="sxs-lookup"><span data-stu-id="f8560-189">Internet Group Management Protocol (IGMP)</span></span>
* <span data-ttu-id="f8560-190">En az 2,5 KB FLASH</span><span class="sxs-lookup"><span data-stu-id="f8560-190">Minimal 2.5 KB FLASH</span></span>
* <span data-ttu-id="f8560-191">IPv4 çok noktaya yayın grubu desteği</span><span class="sxs-lookup"><span data-stu-id="f8560-191">IPv4 multicast group support</span></span>
* <span data-ttu-id="f8560-192">I HIP IxANVL doğrulandı</span><span class="sxs-lookup"><span data-stu-id="f8560-192">IXIA IxANVL validated</span></span>
* <span data-ttu-id="f8560-193">İsteğe bağlı IGMP istatistikleri</span><span class="sxs-lookup"><span data-stu-id="f8560-193">Optional IGMP statistics</span></span>
* <span data-ttu-id="f8560-194">Azure RTOS ThreadX aracılığıyla sistem düzeyinde izleme</span><span class="sxs-lookup"><span data-stu-id="f8560-194">System-level trace via Azure RTOS ThreadX</span></span>
* <span data-ttu-id="f8560-195">Sezgisel IGMP API'leri: *nx_igmp_ \**</span><span class="sxs-lookup"><span data-stu-id="f8560-195">Intuitive IGMP APIs: *nx_igmp_\**</span></span>

### <a name="azure-rtos-netx-secure-dtls"></a><span data-ttu-id="f8560-196">Azure RTOS NetX Secure DTLS</span><span class="sxs-lookup"><span data-stu-id="f8560-196">Azure RTOS NetX Secure DTLS</span></span>

* <span data-ttu-id="f8560-197">Veri Birimi Aktarım Katmanı Güvenliği (DTLS) 1.0 ve 1.2</span><span class="sxs-lookup"><span data-stu-id="f8560-197">Datagram Transport Layer Security (DTLS) 1.0 and 1.2</span></span>
* <span data-ttu-id="f8560-198">En az 11 KB FLASH</span><span class="sxs-lookup"><span data-stu-id="f8560-198">Minimal 11 KB FLASH</span></span>
* <span data-ttu-id="f8560-199">Hızlı, yazılım RSA 2048 bit anahtar boyutu ~1 saniye @120MHz</span><span class="sxs-lookup"><span data-stu-id="f8560-199">Fast, software RSA 2048-bit key size ~1-second @120MHz</span></span>
* <span data-ttu-id="f8560-200">Kolaylaştırılmış X.509 Uygulaması</span><span class="sxs-lookup"><span data-stu-id="f8560-200">Streamlined X.509 Implementation</span></span>
* <span data-ttu-id="f8560-201">NetX Duo UDP Azure RTOS tam olarak tümleştirilmiştir</span><span class="sxs-lookup"><span data-stu-id="f8560-201">Fully integrated with Azure RTOS NetX Duo UDP sockets</span></span>
* <span data-ttu-id="f8560-202">Donanım Şifreleme Desteği</span><span class="sxs-lookup"><span data-stu-id="f8560-202">Hardware Crypto Support</span></span>
* <span data-ttu-id="f8560-203">Yazılım Şifreleme Desteği: RSA (tüm anahtar boyutları), AES, DES/3DES, ECC, HMAC, MD5, SHA-1, SHA-2 (SHA-224, SHA-256, SHA-384, SHA-512)</span><span class="sxs-lookup"><span data-stu-id="f8560-203">Software Crypto Support: RSA (all key sizes), AES, DES/3DES, ECC, HMAC, MD5, SHA-1, SHA-2 (SHA-224, SHA-256, SHA-384, SHA-512)</span></span>
* <span data-ttu-id="f8560-204">P eğrileri 192/224/256/384/521 dahil ECDSA (imzalama) ve ECDH (şifreleme) ile Üç Nokta Eğri Şifrelemesi (ECC)</span><span class="sxs-lookup"><span data-stu-id="f8560-204">Elliptic Curve Cryptography (ECC) with ECDSA (signing) and ECDH (encryption), including P-curves 192/224/256/384/521</span></span>
* <span data-ttu-id="f8560-205">Şifrelenmiş Anahtar Desteği (donanıma bağımlı)</span><span class="sxs-lookup"><span data-stu-id="f8560-205">Encrypted Key Support (hardware dependent)</span></span>

### <a name="azure-rtos-netx-secure-tls"></a><span data-ttu-id="f8560-206">Azure RTOS NetX Secure TLS</span><span class="sxs-lookup"><span data-stu-id="f8560-206">Azure RTOS NetX Secure TLS</span></span>

* <span data-ttu-id="f8560-207">Aktarım Katmanı Güvenliği (TLS) 1.0, 1.1 ve 1.2</span><span class="sxs-lookup"><span data-stu-id="f8560-207">Transport Layer Security (TLS) 1.0, 1.1, and 1.2</span></span>
* <span data-ttu-id="f8560-208">En az 8,8 KB FLASH</span><span class="sxs-lookup"><span data-stu-id="f8560-208">Minimal 8.8 KB FLASH</span></span>
* <span data-ttu-id="f8560-209">Hızlı, yazılım RSA 2048 bit anahtar boyutu ~1 saniye @120MHz</span><span class="sxs-lookup"><span data-stu-id="f8560-209">Fast, software RSA 2048-bit key size ~1-second @120MHz</span></span>
* <span data-ttu-id="f8560-210">Kolaylaştırılmış X.509 Uygulaması</span><span class="sxs-lookup"><span data-stu-id="f8560-210">Streamlined X.509 Implementation</span></span>
* <span data-ttu-id="f8560-211">NetX Duo TCP Azure RTOS tam olarak tümleştirilmiştir</span><span class="sxs-lookup"><span data-stu-id="f8560-211">Fully integrated with Azure RTOS NetX Duo TCP sockets</span></span>
* <span data-ttu-id="f8560-212">Donanım Şifreleme Desteği</span><span class="sxs-lookup"><span data-stu-id="f8560-212">Hardware Crypto Support</span></span>
* <span data-ttu-id="f8560-213">Yazılım Şifreleme Desteği: RSA (tüm anahtar boyutları), AES, DES/3DES, ECC, HMAC, MD5, SHA-1, SHA-2 (SHA-224, SHA-256, SHA-384, SHA-512)</span><span class="sxs-lookup"><span data-stu-id="f8560-213">Software Crypto Support: RSA (all key sizes), AES, DES/3DES, ECC, HMAC, MD5, SHA-1, SHA-2 (SHA-224, SHA-256, SHA-384, SHA-512)</span></span>
* <span data-ttu-id="f8560-214">P eğrileri 192/224/256/384/521 dahil ECDSA (imzalama) ve ECDH (şifreleme) ile Üç Nokta Eğri Şifrelemesi (ECC)</span><span class="sxs-lookup"><span data-stu-id="f8560-214">Elliptic Curve Cryptography (ECC) with ECDSA (signing) and ECDH (encryption), including P-curves 192/224/256/384/521</span></span>
* <span data-ttu-id="f8560-215">Şifrelenmiş Anahtar Desteği (donanıma bağımlı)</span><span class="sxs-lookup"><span data-stu-id="f8560-215">Encrypted Key Support (hardware dependent)</span></span>

### <a name="icmp"></a><span data-ttu-id="f8560-216">ICMP</span><span class="sxs-lookup"><span data-stu-id="f8560-216">ICMP</span></span>

* <span data-ttu-id="f8560-217">İnternet Denetim İletisi Protokolü (ICMP)</span><span class="sxs-lookup"><span data-stu-id="f8560-217">Internet Control Message Protocol (ICMP)</span></span>
* <span data-ttu-id="f8560-218">En az 2,5 KB FLASH</span><span class="sxs-lookup"><span data-stu-id="f8560-218">Minimal 2.5 KB FLASH</span></span>
* <span data-ttu-id="f8560-219">IPv4 ve IPv6 desteği</span><span class="sxs-lookup"><span data-stu-id="f8560-219">IPv4 and IPv6 support</span></span>
* <span data-ttu-id="f8560-220">I HIP IxANVL doğrulandı</span><span class="sxs-lookup"><span data-stu-id="f8560-220">IXIA IxANVL validated</span></span>
* <span data-ttu-id="f8560-221">Ping isteği ve ping yanıtı</span><span class="sxs-lookup"><span data-stu-id="f8560-221">Ping request and ping response</span></span>
* <span data-ttu-id="f8560-222">Ping istekleri üzerinde isteğe bağlı iş parçacığının askıya alınması</span><span class="sxs-lookup"><span data-stu-id="f8560-222">Optional thread suspension on ping requests</span></span>
* <span data-ttu-id="f8560-223">Tüm askıya almada isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="f8560-223">Optional timeout on all suspension</span></span>
* <span data-ttu-id="f8560-224">İsteğe bağlı ICMP istatistikleri</span><span class="sxs-lookup"><span data-stu-id="f8560-224">Optional ICMP statistics</span></span>
* <span data-ttu-id="f8560-225">Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme</span><span class="sxs-lookup"><span data-stu-id="f8560-225">System-level trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="f8560-226">Sezgisel ICMP API'leri: *nx_icmp_ \**</span><span class="sxs-lookup"><span data-stu-id="f8560-226">Intuitive ICMP APIs: *nx_icmp_\**</span></span>

### <a name="udp"></a><span data-ttu-id="f8560-227">UDP</span><span class="sxs-lookup"><span data-stu-id="f8560-227">UDP</span></span>

* <span data-ttu-id="f8560-228">Kullanıcı Veri Birimi Protokolü (UDP)</span><span class="sxs-lookup"><span data-stu-id="f8560-228">User Datagram Protocol (UDP)</span></span>
* <span data-ttu-id="f8560-229">Yuva başına en az 2,5 KB FLASH, 124 yuva bayt RAM</span><span class="sxs-lookup"><span data-stu-id="f8560-229">Minimal 2.5 KB FLASH, 124 sockets bytes of RAM per socket</span></span>
* <span data-ttu-id="f8560-230">Hızlı, kabloya yakın TCP paketi işleme:</span><span class="sxs-lookup"><span data-stu-id="f8560-230">Fast, near wirespeed TCP packet processing:</span></span>
    * <span data-ttu-id="f8560-231">100 Mb/sn Ethernet üzerinde RX 95 Mb/sn, MCU @100MHz , %14 MCU kullanımı</span><span class="sxs-lookup"><span data-stu-id="f8560-231">RX 95 Mbps on 100 Mbps Ethernet, MCU @100MHz, 14% MCU utilization</span></span>
    * <span data-ttu-id="f8560-232">100 Mb/sn Ethernet üzerinde TX 94 Mb/sn, MCU @100MHz , %10 MCU kullanımı</span><span class="sxs-lookup"><span data-stu-id="f8560-232">TX 94 Mbps on 100 Mbps Ethernet, MCU @100MHz, 10% MCU utilization</span></span>
* <span data-ttu-id="f8560-233">UDP Hızlı Yolu™ teknolojisi</span><span class="sxs-lookup"><span data-stu-id="f8560-233">UDP Fast Path™ technology</span></span>
* <span data-ttu-id="f8560-234">UDP sayısıyla ilgili sınır yok</span><span class="sxs-lookup"><span data-stu-id="f8560-234">No limits on the number of UDP</span></span>
* <span data-ttu-id="f8560-235">I HIP IxANVL doğrulandı</span><span class="sxs-lookup"><span data-stu-id="f8560-235">IXIA IxANVL validated</span></span>
* <span data-ttu-id="f8560-236">Yuva almada isteğe bağlı askıya alma</span><span class="sxs-lookup"><span data-stu-id="f8560-236">Optional suspension on socket receive</span></span>
* <span data-ttu-id="f8560-237">Tüm askıya almada isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="f8560-237">Optional timeout on all suspension</span></span>
* <span data-ttu-id="f8560-238">İsteğe bağlı UDP istatistikleri</span><span class="sxs-lookup"><span data-stu-id="f8560-238">Optional UDP statistics</span></span>
* <span data-ttu-id="f8560-239">Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme</span><span class="sxs-lookup"><span data-stu-id="f8560-239">System-level trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="f8560-240">Sezgisel UDP API'leri: *nx_udp_ \**</span><span class="sxs-lookup"><span data-stu-id="f8560-240">Intuitive UDP APIs: *nx_udp_\**</span></span>

### <a name="tcp"></a><span data-ttu-id="f8560-241">TCP</span><span class="sxs-lookup"><span data-stu-id="f8560-241">TCP</span></span>

* <span data-ttu-id="f8560-242">İletim Denetimi Protokolü (TCP)</span><span class="sxs-lookup"><span data-stu-id="f8560-242">Transmission Control Protocol (TCP)</span></span>
* <span data-ttu-id="f8560-243">En az 10,5K8 ile 12,5 KB FLASH, yuva başına 280 bayt RAM</span><span class="sxs-lookup"><span data-stu-id="f8560-243">Minimal 10.5K8 to 12.5 KB FLASH, 280 bytes of RAM per socket</span></span>
* <span data-ttu-id="f8560-244">Hızlı, neredeyse wlrespeed TCP paket işleme:</span><span class="sxs-lookup"><span data-stu-id="f8560-244">Fast, near wlrespeed TCP packet processing:</span></span>
    * <span data-ttu-id="f8560-245">100 Mb/sn Ethernet üzerinde RX 93 Mb/sn, MCU @100MHz , %20 MCU kullanımı</span><span class="sxs-lookup"><span data-stu-id="f8560-245">RX 93 Mbps on 100 Mbps Ethernet, MCU @100MHz, 20% MCU utilization</span></span>
    * <span data-ttu-id="f8560-246">100 Mb/sn Ethernet üzerinde TX 94 Mb/sn, MCU @100MHz , %27 MCU kullanımı</span><span class="sxs-lookup"><span data-stu-id="f8560-246">TX 94 Mbps on 100 Mbps Ethernet, MCU @100MHz, 27% MCU utilization</span></span>
* <span data-ttu-id="f8560-247">Güvenilir bağlantı</span><span class="sxs-lookup"><span data-stu-id="f8560-247">Reliable connection</span></span>
* <span data-ttu-id="f8560-248">TCP yuvalarının sayısıyla ilgili sınır yok</span><span class="sxs-lookup"><span data-stu-id="f8560-248">No limits on the number of TCP sockets</span></span>
* <span data-ttu-id="f8560-249">I HIP IxANVL doğrulandı</span><span class="sxs-lookup"><span data-stu-id="f8560-249">IXIA IxANVL validated</span></span>
* <span data-ttu-id="f8560-250">Yuva alma/iletmede isteğe bağlı askıya alma</span><span class="sxs-lookup"><span data-stu-id="f8560-250">Optional suspension on socket receive/transmit</span></span>
* <span data-ttu-id="f8560-251">Tüm askıya almada isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="f8560-251">Optional timeout on all suspension</span></span>
* <span data-ttu-id="f8560-252">İsteğe bağlı TCP istatistikleri</span><span class="sxs-lookup"><span data-stu-id="f8560-252">Optional TCP statistics</span></span>
* <span data-ttu-id="f8560-253">Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme</span><span class="sxs-lookup"><span data-stu-id="f8560-253">System-level trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="f8560-254">Sezgisel TCP API'leri: *nx_tcp_ \**</span><span class="sxs-lookup"><span data-stu-id="f8560-254">Intuitive TCP APIs: *nx_tcp_\**</span></span>

### <a name="arprarp"></a><span data-ttu-id="f8560-255">ARP/RARP</span><span class="sxs-lookup"><span data-stu-id="f8560-255">ARP/RARP</span></span>

* <span data-ttu-id="f8560-256">Adres Çözümleme Protokolü (ARP)</span><span class="sxs-lookup"><span data-stu-id="f8560-256">Address Resolution Protocol (ARP)</span></span>
* <span data-ttu-id="f8560-257">Ters Adres Çözümleme Protokolü (RARP)</span><span class="sxs-lookup"><span data-stu-id="f8560-257">Reverse Address Resolution Protocol (RARP)</span></span>
* <span data-ttu-id="f8560-258">En az 1,7 KB FLASH, RAM boyutu</span><span class="sxs-lookup"><span data-stu-id="f8560-258">Minimal 1.7 KB FLASH, RAM size</span></span>
* <span data-ttu-id="f8560-259">32 blt IPv4 ve 48 blt MAC adreslerinin dinamik çözümlemesi</span><span class="sxs-lookup"><span data-stu-id="f8560-259">Dynamic resolution of 32-blt IPv4 and 48-blt MAC addresses</span></span>
* <span data-ttu-id="f8560-260">I HIP IxANVL doğrulandı</span><span class="sxs-lookup"><span data-stu-id="f8560-260">IXIA IxANVL validated</span></span>
* <span data-ttu-id="f8560-261">Esnek, kullanıcı tanımlı ARP önbelleği</span><span class="sxs-lookup"><span data-stu-id="f8560-261">Flexible, user-defined ARP cache</span></span>
* <span data-ttu-id="f8560-262">Gratuitous ARP desteği</span><span class="sxs-lookup"><span data-stu-id="f8560-262">Gratuitous ARP support</span></span>
* <span data-ttu-id="f8560-263">Uygulama tarafından belirlenen isteğe bağlı ARP/RARP istatistikleri</span><span class="sxs-lookup"><span data-stu-id="f8560-263">Optional ARP/RARP statistics determined by application</span></span>
* <span data-ttu-id="f8560-264">Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme</span><span class="sxs-lookup"><span data-stu-id="f8560-264">System-level trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="f8560-265">Sezgisel ARP/RARP *API'leri: \* nx_arp_*, *\* nx_rarp_*</span><span class="sxs-lookup"><span data-stu-id="f8560-265">Intuitive ARP/RARP APIs: *nx_arp_\**, *nx_rarp_\**</span></span>

### <a name="ipv4-amp-ipv6"></a><span data-ttu-id="f8560-266">IPv4 &amp; IPv6</span><span class="sxs-lookup"><span data-stu-id="f8560-266">IPv4 &amp; IPv6</span></span>

* <span data-ttu-id="f8560-267">İnternet Protokolü (IP)</span><span class="sxs-lookup"><span data-stu-id="f8560-267">Internet Protocol (IP)</span></span>
* <span data-ttu-id="f8560-268">En az 3,5 KB ile 8,5 KB FLASH, 2 KB ile 3 KB RAM ayak izi</span><span class="sxs-lookup"><span data-stu-id="f8560-268">Minimal 3.5 KB to 8.5 KB FLASH, 2 KB to 3 KB RAM footprint</span></span>
* <span data-ttu-id="f8560-269">Piconet™ mimarisi</span><span class="sxs-lookup"><span data-stu-id="f8560-269">Piconet™ architecture</span></span>
* <span data-ttu-id="f8560-270">Hızlı, kablolara yakın performans</span><span class="sxs-lookup"><span data-stu-id="f8560-270">Fast, near wirespeed performance</span></span>
* <span data-ttu-id="f8560-271">Birden çok arabirim desteği</span><span class="sxs-lookup"><span data-stu-id="f8560-271">Multiple interface support</span></span>
* <span data-ttu-id="f8560-272">Birden çok ana bilgisayar desteği</span><span class="sxs-lookup"><span data-stu-id="f8560-272">Multihomed support</span></span>
* <span data-ttu-id="f8560-273">Statik yönlendirme desteği</span><span class="sxs-lookup"><span data-stu-id="f8560-273">Static routing support</span></span>
* <span data-ttu-id="f8560-274">IP parçalanması/yeniden değerlendirme desteği</span><span class="sxs-lookup"><span data-stu-id="f8560-274">IP fragmentation/reassembly support</span></span>
* <span data-ttu-id="f8560-275">IPv4 ve IPv6 adresi desteği</span><span class="sxs-lookup"><span data-stu-id="f8560-275">IPv4 and IPv6 address support</span></span>
* <span data-ttu-id="f8560-276">I HIP IxANVL doğrulandı</span><span class="sxs-lookup"><span data-stu-id="f8560-276">IXIA IxANVL validated</span></span>
* <span data-ttu-id="f8560-277">Aşama II IPv6 Hazır Logo Sertifikası</span><span class="sxs-lookup"><span data-stu-id="f8560-277">Phase II IPv6 Ready Logo Certification</span></span>
* <span data-ttu-id="f8560-278">İsteğe bağlı IP istatistikleri</span><span class="sxs-lookup"><span data-stu-id="f8560-278">Optional IP statistics</span></span>
* <span data-ttu-id="f8560-279">İyi tanımlanmış, sezgisel fiziksel katman sürücü arabirimi</span><span class="sxs-lookup"><span data-stu-id="f8560-279">Well defined, intuitive physical layer driver interface</span></span>
* <span data-ttu-id="f8560-280">Azure RTOS TraceX aracılığıyla sistem düzeyinde izleme</span><span class="sxs-lookup"><span data-stu-id="f8560-280">System-level trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="f8560-281">Sezgisel IP katmanı *API'leri: nx_ip_, \** *nxd_ip_ \** *\** , nxd_ipv6_</span><span class="sxs-lookup"><span data-stu-id="f8560-281">Intuitive IP layer APIs: *nx_ip_\**, *nxd_ip_\**, *nxd_ipv6_\**</span></span>
* <span data-ttu-id="f8560-282">TTROP ve UL tarafından IEC 61508 SIL 4, IEC 62304 Sınıf C, ISO 26262 SONA D ve EN 50128 SW-SIL4 için önceden sertifikalıdır</span><span class="sxs-lookup"><span data-stu-id="f8560-282">Pre-certified by TUV and UL to IEC 61508 SIL 4, IEC 62304 Class C, ISO 26262 ASIL D, and EN 50128 SW-SIL4</span></span>

### <a name="azure-rtos-netx-secure-ipsec"></a><span data-ttu-id="f8560-283">Azure RTOS NetX Güvenli IPSEC</span><span class="sxs-lookup"><span data-stu-id="f8560-283">Azure RTOS NetX Secure IPSEC</span></span>

* <span data-ttu-id="f8560-284">İnternet Protokolü Güvenliği (IPSEC)</span><span class="sxs-lookup"><span data-stu-id="f8560-284">Internet Protocol Security (IPSEC)</span></span>
* <span data-ttu-id="f8560-285">IP katmanı</span><span class="sxs-lookup"><span data-stu-id="f8560-285">IP layer</span></span>
* <span data-ttu-id="f8560-286">Donanım şifreleme desteği</span><span class="sxs-lookup"><span data-stu-id="f8560-286">Hardware crypto support</span></span>
* <span data-ttu-id="f8560-287">Yazılım şifreleme desteği, şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="f8560-287">Software crypto support, including:</span></span>
    * <span data-ttu-id="f8560-288">DES, 3DES</span><span class="sxs-lookup"><span data-stu-id="f8560-288">DES, 3DES</span></span>
    * <span data-ttu-id="f8560-289">AES</span><span class="sxs-lookup"><span data-stu-id="f8560-289">AES</span></span>
    * <span data-ttu-id="f8560-290">HMAC-MD5</span><span class="sxs-lookup"><span data-stu-id="f8560-290">HMAC-MD5</span></span>
    * <span data-ttu-id="f8560-291">HMAC-SHA1</span><span class="sxs-lookup"><span data-stu-id="f8560-291">HMAC-SHA1</span></span>
* <span data-ttu-id="f8560-292">İnternet Anahtar Exchange (IKE) Sürüm 2 desteği</span><span class="sxs-lookup"><span data-stu-id="f8560-292">Internet Key Exchange (IKE) Version 2 support</span></span>
* <span data-ttu-id="f8560-293">Sezgisel IPsec API'leri: *nx_ipsec_ \**</span><span class="sxs-lookup"><span data-stu-id="f8560-293">Intuitive IPsec APIs: *nx_ipsec_\**</span></span>
* <span data-ttu-id="f8560-294">IPsec yalnızca NetX Duo Azure RTOS kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="f8560-294">IPsec is only available with Azure RTOS NetX Duo</span></span>

## <a name="safe-and-secure"></a><span data-ttu-id="f8560-295">Kasa ve güvenli</span><span class="sxs-lookup"><span data-stu-id="f8560-295">Safe and secure</span></span>

<span data-ttu-id="f8560-296">Azure RTOS NetX Duo güvenlidir.</span><span class="sxs-lookup"><span data-stu-id="f8560-296">Azure RTOS NetX Duo is secure.</span></span> <span data-ttu-id="f8560-297">Bu güvenlik IPsec, SSL, TLS ve DTLS gibi eklenti güvenlik ürünleri aracılığıyla sağlanır.</span><span class="sxs-lookup"><span data-stu-id="f8560-297">This security is provided through add-on security products, including IPsec, SSL, TLS, and DTLS.</span></span> <span data-ttu-id="f8560-298">Ayrıca uygulamanın NetX Duo'ya tüm dış erişim üzerinde tam Azure RTOS güvenlik riski belirlemeyi çok daha kolay hale getirmiştir.</span><span class="sxs-lookup"><span data-stu-id="f8560-298">Also, the application has complete control over all external access to Azure RTOS NetX Duo, making security risk determination much easier.</span></span>

<span data-ttu-id="f8560-299">Microsoft Azure RTOS, OEM'lere iletişimin güvenliğini sağlamak ve temel MCU/MPU donanım koruma mekanizmalarını kullanarak kod ve veri yalıtımı oluşturmak için bileşenler sağlar.</span><span class="sxs-lookup"><span data-stu-id="f8560-299">Microsoft Azure RTOS provides OEMs with components to secure communication and to create code and data isolation using underlying MCU/MPU hardware protection mechanisms.</span></span> <span data-ttu-id="f8560-300">Son olarak cihaz oluşturucusu, cihazın kendi özel kullanım durumuyla ilişkili gelişen güvenlik gereksinimlerini tam olarak karşılamasını sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="f8560-300">It is ultimately the responsibility of the device builder to ensure the device fully meets the evolving security requirements associated with its specific use case.</span></span>


## <a name="interoperability-verification"></a><span data-ttu-id="f8560-301">Birlikte çalışabilirlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="f8560-301">Interoperability verification</span></span>

<span data-ttu-id="f8560-302">NetX Duo, RFC standartlarına uyar ve çoğu satıcının cihazlarıyla birlikte çalışabilirlik desteği sunar.</span><span class="sxs-lookup"><span data-stu-id="f8560-302">NetX Duo conforms to RFC standards and offers complete interoperability with devices for most vendors.</span></span>

![IPv6 Ready logosu](./media/overview-netx-duo/ipv6-ready-logo.png)

<span data-ttu-id="f8560-304">Azure RTOS NetX Duo, kapsamlı IPv6-Ready logo sertifikasına ulaşmak için yalnızca katıştırılmış TCP/IP yığınlarından biridir. Bu, IPv6 Forumu tarafından yönetilen ve doğrulanan uyumluluk ve birlikte çalışabilirlik testlerini geçti olduğunu kanıtlayın.</span><span class="sxs-lookup"><span data-stu-id="f8560-304">Azure RTOS NetX Duo is one of the only embedded TCP/IP stacks to achieve the rigorous IPv6-Ready Logo certification, evidence that it has passed conformance and interoperability tests, administered and validated by the IPv6 Forum.</span></span> <span data-ttu-id="f8560-305">NetX Duo Ayrıca, NetX Duo çekirdek TCP/IP protokol uygulamasının sektör standardı IxANVL (otomatik ağ doğrulama kitaplığı) kullanır.</span><span class="sxs-lookup"><span data-stu-id="f8560-305">NetX Duo also utilizes the industry standard IxANVL (Automated Network Validation Library) for the NetX Duo core TCP/IP protocol implementation.</span></span>

## <a name="comprehensive-iot-solution"></a><span data-ttu-id="f8560-306">Kapsamlı IoT çözümü</span><span class="sxs-lookup"><span data-stu-id="f8560-306">Comprehensive IoT solution</span></span>

<span data-ttu-id="f8560-307">NetX Duo, derin eklenmiş IoT uygulamaları için en kapsamlı TCP/IP ağıyla biridir.</span><span class="sxs-lookup"><span data-stu-id="f8560-307">NetX Duo has one of the most comprehensive TCP/IP networking for deeply embedded IoT applications.</span></span> <span data-ttu-id="f8560-308">Bu destek, aşağıdaki eklenti protokol ürünlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="f8560-308">This support includes the following add-on protocol products.</span></span>

<span data-ttu-id="f8560-309">MQTT, CoAP, LWM2M, 6LoWPAN, SSL/TLS/DTLS, IPSec, Oto IP, DHCP, DNS, mDNS, DNS-SD, FTP, HTTP, IPSec, NAT, POP3, PPP, PPPoE, SMTP, SNMP v1/2/3, Telnet, TFTP</span><span class="sxs-lookup"><span data-stu-id="f8560-309">MQTT, CoAP, LWM2M, 6LoWPAN, SSL/TLS/DTLS, IPsec, AutoIP, DHCP, DNS, mDNS, DNS-SD, FTP, HTTP, IPsec, NAT, POP3, PPP, PPPoE, SMTP, SNMP v1/2/3, Telnet, TFTP</span></span>

## <a name="advanced-technology"></a><span data-ttu-id="f8560-310">Gelişmiş teknoloji</span><span class="sxs-lookup"><span data-stu-id="f8560-310">Advanced technology</span></span>

<span data-ttu-id="f8560-311">Azure RTOS NetX Duo, şunları içeren gelişmiş bir teknolojidir:</span><span class="sxs-lookup"><span data-stu-id="f8560-311">Azure RTOS NetX Duo is advanced technology that includes:</span></span>

* <span data-ttu-id="f8560-312">Piconet™ mimarisi</span><span class="sxs-lookup"><span data-stu-id="f8560-312">Piconet™ architecture</span></span>
* <span data-ttu-id="f8560-313">Otomatik ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="f8560-313">Automatic scaling</span></span>
* <span data-ttu-id="f8560-314">UDP Fast-Path teknolojisi™</span><span class="sxs-lookup"><span data-stu-id="f8560-314">UDP Fast-Path Technology™</span></span>
* <span data-ttu-id="f8560-315">Esnek paket yönetimi</span><span class="sxs-lookup"><span data-stu-id="f8560-315">Flexible packet management</span></span>
* <span data-ttu-id="f8560-316">Sıfır-API ve uygulama kopyalama</span><span class="sxs-lookup"><span data-stu-id="f8560-316">Zero-copy API and implementation</span></span>
* <span data-ttu-id="f8560-317">Çok sayfalı destek</span><span class="sxs-lookup"><span data-stu-id="f8560-317">Multihomed support</span></span>
* <span data-ttu-id="f8560-318">Tüm askıya alma sırasında isteğe bağlı zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="f8560-318">Optional timeout on all suspension</span></span>
* <span data-ttu-id="f8560-319">Statik yönlendirme desteği</span><span class="sxs-lookup"><span data-stu-id="f8560-319">Static routing support</span></span>
* <span data-ttu-id="f8560-320">IPsec</span><span class="sxs-lookup"><span data-stu-id="f8560-320">IPsec</span></span>
* <span data-ttu-id="f8560-321">SSL/TLS/DTLS</span><span class="sxs-lookup"><span data-stu-id="f8560-321">SSL/TLS/DTLS</span></span>
* <span data-ttu-id="f8560-322">Azure RTOS TraceX sistem analizi desteği</span><span class="sxs-lookup"><span data-stu-id="f8560-322">Azure RTOS TraceX system analysis support</span></span>

## <a name="related-services"></a><span data-ttu-id="f8560-323">İlgili hizmetler</span><span class="sxs-lookup"><span data-stu-id="f8560-323">Related services</span></span>

### <a name="azure-iot"></a><span data-ttu-id="f8560-324">Azure IoT</span><span class="sxs-lookup"><span data-stu-id="f8560-324">Azure IoT</span></span>

<span data-ttu-id="f8560-325">NetX Duo, Azure IoT hizmetlerine bağlanmayı kolaylaştırmak amacıyla Azure RTOS ve Embedded C için Azure SDK arasında bağlama katmanı görevi gören platforma özel bir kitaplık olan Azure [RTOS Için Azure IoT ara yazılımı](https://github.com/azure-rtos/netxduo/blob/master/addons/azure_iot/docs/README.md)içerir.</span><span class="sxs-lookup"><span data-stu-id="f8560-325">NetX Duo includes [Azure IoT Middleware for Azure RTOS](https://github.com/azure-rtos/netxduo/blob/master/addons/azure_iot/docs/README.md), a platform-specific library that acts as a binding layer between the Azure RTOS and the Azure SDK for Embedded C to facilitate connectivity to Azure IoT services.</span></span> <span data-ttu-id="f8560-326">Azure IoT ara yazılımı amaçları şunlardır.</span><span class="sxs-lookup"><span data-stu-id="f8560-326">The goals of Azure IoT Middleware are the following.</span></span>
* <span data-ttu-id="f8560-327">Geliştiricilerin uygulamaları için ihtiyaç duyduğu akıllı istemci arabirimlerini (IoTHub_Client, DeviceProvisioning_Client) sağlayın.</span><span class="sxs-lookup"><span data-stu-id="f8560-327">Provide the smart client interfaces (IoTHub_Client, DeviceProvisioning_Client) that developers need for their applications.</span></span>
* <span data-ttu-id="f8560-328">Gömülü C SDK 'Sı ve platformu arasındaki etkileşimi düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="f8560-328">Orchestrate the interaction between the Embedded C SDK and the platform.</span></span>
* <span data-ttu-id="f8560-329">Azure RTOS platformu başlatma sağlayın.</span><span class="sxs-lookup"><span data-stu-id="f8560-329">Provide Azure RTOS platform initialization.</span></span>
* <span data-ttu-id="f8560-330">IoT Tak ve Kullan desteği.</span><span class="sxs-lookup"><span data-stu-id="f8560-330">IoT Plug and Play support.</span></span>
* <span data-ttu-id="f8560-331">Güvenlik özellikleri.</span><span class="sxs-lookup"><span data-stu-id="f8560-331">Security capabilities.</span></span>
* <span data-ttu-id="f8560-332">Kaynak sınırlaması fark edilir.</span><span class="sxs-lookup"><span data-stu-id="f8560-332">Resource limitation aware.</span></span>
* <span data-ttu-id="f8560-333">Protokol desteği.</span><span class="sxs-lookup"><span data-stu-id="f8560-333">Protocol support.</span></span>

![Azure RTOS NetX Duo ile Ilgili hizmetler](./media/overview-netx-duo/related-services.png)

### <a name="azure-defender"></a><span data-ttu-id="f8560-335">Azure Defender</span><span class="sxs-lookup"><span data-stu-id="f8560-335">Azure Defender</span></span>

<span data-ttu-id="f8560-336">IoT için Azure Defender güvenlik modülü, Azure RTOS cihazları için kapsamlı bir güvenlik çözümü sağlar.</span><span class="sxs-lookup"><span data-stu-id="f8560-336">The Azure Defender for IoT security module provides a comprehensive security solution for Azure RTOS devices.</span></span> <span data-ttu-id="f8560-337">Azure RTOS için güvenlik modülü, kötü amaçlı ağ etkinliği algılama, özel uyarı tabanlı cihaz davranışı taban çizgisi sağlar ve cihaz güvenliği Hygiene 'ın artırılmasına yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="f8560-337">The Security Module for Azure RTOS offers malicious network activity detection, custom alert based device behavior baselining, and helps improve device security hygiene.</span></span> <span data-ttu-id="f8560-338">[Azure RTOS güvenlik modülü](https://docs.microsoft.com/azure/asc-for-iot/iot-security-azure-rtos) hakkında daha fazla bilgi edinin veya [Azure RTOS hızlı başlangıç Için güvenlik yapılandırması modülünü](https://docs.microsoft.com/azure/asc-for-iot/quickstart-azure-rtos-security-module) kullanmaya başlayın.</span><span class="sxs-lookup"><span data-stu-id="f8560-338">Learn more about the [Security Module for Azure RTOS](https://docs.microsoft.com/azure/asc-for-iot/iot-security-azure-rtos) or get started with the [Configure Security Module for Azure RTOS](https://docs.microsoft.com/azure/asc-for-iot/quickstart-azure-rtos-security-module) quickstart.</span></span>

### <a name="device-update-for-iot-hub"></a><span data-ttu-id="f8560-339">IoT Hub için cihaz güncelleştirmesi</span><span class="sxs-lookup"><span data-stu-id="f8560-339">Device Update for IoT Hub</span></span>

<span data-ttu-id="f8560-340">[IoT Hub Için Azure cihaz güncelleştirmesi](https://docs.microsoft.com/azure/iot-hub-device-update/understand-device-update) , IoT cihazlarınız için kablosuz güncelleştirmeleri (OTA) dağıtmanıza olanak sağlayan bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="f8560-340">The [Azure Device Update for IoT Hub](https://docs.microsoft.com/azure/iot-hub-device-update/understand-device-update) is a service that enables you to deploy over-the-air updates (OTA) for your IoT devices.</span></span> <span data-ttu-id="f8560-341">IoT Hub modülü için cihaz güncelleştirmesi, Azure RTOS NetX Duo 'da IoT Hub aracısının cihaz güncelleştirme uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="f8560-341">The Device Update for IoT Hub module is the implementation of Device Update for IoT Hub Agent in Azure RTOS NetX Duo.</span></span> <span data-ttu-id="f8560-342">Cihaz oluşturucuların, uygulamasındaki cihaz güncelleştirme yeteneklerini tümleştirmeleri için basit API 'Ler sağlar.</span><span class="sxs-lookup"><span data-stu-id="f8560-342">It provides simple APIs for device builders to integrate the Device Update capability in their application.</span></span>

<span data-ttu-id="f8560-343">Cihazlarda AIR (OTA) güncelleştirmelerini yapılandırma, oluşturma ve dağıtma hakkında bilgi edinmek için Başlarken kılavuzlarını içeren anahtar yarı iletkeni değerlendirme panoları örneklerine bakın.</span><span class="sxs-lookup"><span data-stu-id="f8560-343">See the samples of key semiconductors evaluation boards that include the get started guides to learn configure, build and deploy the over-the-air (OTA) updates to the devices.</span></span>

<span data-ttu-id="f8560-344">[Azure RTOS ile IoT Hub Için cihaz güncelleştirme](https://docs.microsoft.com/azure/iot-hub-device-update/device-update-azure-real-time-operating-system)kullanma hakkında daha fazla bilgi edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8560-344">And you can learn more details about use [Device Update for IoT Hub with Azure RTOS](https://docs.microsoft.com/azure/iot-hub-device-update/device-update-azure-real-time-operating-system).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f8560-345">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f8560-345">Next steps</span></span>

<span data-ttu-id="f8560-346">NetX Duo hakkında daha fazla bilgi edinmek için [Azure RTOS NetX Duo Kullanıcı kılavuzuyla](about-this-guide.md)başlayın.</span><span class="sxs-lookup"><span data-stu-id="f8560-346">To learn more about NetX Duo, start with the [Azure RTOS NetX Duo User Guide](about-this-guide.md).</span></span>
