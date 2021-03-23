---
title: Bölüm 1-NetX HTTP 'ye giriş
description: Bu belge, HTTP 'nin Web 'de içerik aktarmak için tasarlanan bir protokol olduğunu açıklayacak.
author: philmea
ms.author: philmea
ms.date: 06/08/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 6137cc0d8deb753d784be844d5abc7778dd62295
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826717"
---
# <a name="chapter-1---introduction-to-netx-http"></a><span data-ttu-id="d5d61-103">Bölüm 1-NetX HTTP 'ye giriş</span><span class="sxs-lookup"><span data-stu-id="d5d61-103">Chapter 1 - Introduction to NetX HTTP</span></span>

<span data-ttu-id="d5d61-104">Köprü Metni Aktarım Protokolü (HTTP), Web üzerinde içerik aktarmak için tasarlanan bir protokoldür.</span><span class="sxs-lookup"><span data-stu-id="d5d61-104">The Hypertext Transfer Protocol (HTTP) is a protocol designed for transferring content on the Web.</span></span> <span data-ttu-id="d5d61-105">HTTP, içerik aktarım işlevini gerçekleştirmek için güvenilir Iletim Denetimi Protokolü (TCP) hizmetlerinden yararlanan basit bir protokoldür.</span><span class="sxs-lookup"><span data-stu-id="d5d61-105">HTTP is a simple protocol that utilizes reliable Transmission Control Protocol (TCP) services to perform its content transfer function.</span></span> <span data-ttu-id="d5d61-106">Bu nedenle, HTTP son derece güvenilir bir içerik aktarım protokolüdür.</span><span class="sxs-lookup"><span data-stu-id="d5d61-106">Because of this, HTTP is a highly reliable content transfer protocol.</span></span> <span data-ttu-id="d5d61-107">HTTP, en çok kullanılan uygulama protokollerinden biridir.</span><span class="sxs-lookup"><span data-stu-id="d5d61-107">HTTP is one of the most used application protocols.</span></span> <span data-ttu-id="d5d61-108">Web 'deki tüm işlemler HTTP protokolünü kullanır.</span><span class="sxs-lookup"><span data-stu-id="d5d61-108">All operations on the Web utilize the HTTP protocol.</span></span>

## <a name="http-requirements"></a><span data-ttu-id="d5d61-109">HTTP gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="d5d61-109">HTTP Requirements</span></span>

<span data-ttu-id="d5d61-110">NetX HTTP paketi, düzgün çalışması için bir NetX (sürüm 5,2 veya üzeri) yüklü olmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="d5d61-110">In order to function properly, the NetX HTTP package requires that a NetX (version 5.2 or later) is installed.</span></span> <span data-ttu-id="d5d61-111">Buna ek olarak, bir IP örneği zaten oluşturulmalı ve TCP 'nin aynı IP örneğinde etkinleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="d5d61-111">In addition, an IP instance must already be created and TCP must be enabled on that same IP instance.</span></span> <span data-ttu-id="d5d61-112">Bölüm **2** ' de "küçük örnek sistem" bölümündeki tanıtım dosyası bunun nasıl yapıldığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="d5d61-112">The demo file in section “Small Example System” in **Chapter 2** will demonstrate how this is done.</span></span>

<span data-ttu-id="d5d61-113">NetX HTTP paketinin HTTP Istemci bölümünün başka gereksinimi yoktur.</span><span class="sxs-lookup"><span data-stu-id="d5d61-113">The HTTP Client portion of the NetX HTTP package has no further requirements.</span></span>

<span data-ttu-id="d5d61-114">NetX HTTP paketinin HTTP Sunucusu bölümünde birkaç ek gereksinim vardır.</span><span class="sxs-lookup"><span data-stu-id="d5d61-114">The HTTP Server portion of the NetX HTTP package has several additional requirements.</span></span> <span data-ttu-id="d5d61-115">İlk olarak, tüm Istemci HTTP isteklerini işlemek için TCP 'nin *iyi bilinen bağlantı noktası 80* ' e tam erişim gerektirir.</span><span class="sxs-lookup"><span data-stu-id="d5d61-115">First, it requires complete access to TCP *well-known port 80* for handling all Client HTTP requests.</span></span> <span data-ttu-id="d5d61-116">HTTP sunucusu Ayrıca, FileX Embedded dosya sistemiyle kullanılmak üzere tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="d5d61-116">The HTTP Server is also designed for use with the FileX embedded file system.</span></span> <span data-ttu-id="d5d61-117">FileX yoksa, Kullanıcı kendi ortamlarında kullanılan FileX bölümlerinin bağlantı noktasını alabilir.</span><span class="sxs-lookup"><span data-stu-id="d5d61-117">If FileX is not available, the user may port the portions of FileX used to their own environment.</span></span> <span data-ttu-id="d5d61-118">Bu, bu kılavuzun sonraki bölümlerinde ele alınmıştır.</span><span class="sxs-lookup"><span data-stu-id="d5d61-118">This is discussed in later sections of this guide.</span></span>

## <a name="http-constraints"></a><span data-ttu-id="d5d61-119">HTTP kısıtlamaları</span><span class="sxs-lookup"><span data-stu-id="d5d61-119">HTTP Constraints</span></span> 

<span data-ttu-id="d5d61-120">NetX HTTP protokolü, HTTP 1,0 standardını uygular.</span><span class="sxs-lookup"><span data-stu-id="d5d61-120">The NetX HTTP protocol implements the HTTP 1.0 standard.</span></span> <span data-ttu-id="d5d61-121">Ancak, aşağıdaki kısıtlamalar vardır:</span><span class="sxs-lookup"><span data-stu-id="d5d61-121">However, there are following constraints:</span></span>

1.  <span data-ttu-id="d5d61-122">Kalıcı bağlantılar desteklenmiyor</span><span class="sxs-lookup"><span data-stu-id="d5d61-122">Persistent connections are not supported</span></span>

2.  <span data-ttu-id="d5d61-123">İstek ardışık düzen oluşturma desteklenmiyor</span><span class="sxs-lookup"><span data-stu-id="d5d61-123">Request pipelining is not supported</span></span>

3.  <span data-ttu-id="d5d61-124">HTTP sunucusu hem temel hem de MD5 Özet kimlik doğrulamasını destekler, ancak MD5-sess içermez.</span><span class="sxs-lookup"><span data-stu-id="d5d61-124">The HTTP Server supports both basic and MD5 digest authentication, but not MD5-sess.</span></span> <span data-ttu-id="d5d61-125">Mevcut olduğunda, HTTP Istemcisi yalnızca temel kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="d5d61-125">At present, the HTTP Client supports only basic authentication.</span></span>

4.  <span data-ttu-id="d5d61-126">İçerik sıkıştırması desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="d5d61-126">No content compression is supported.</span></span>

5.  <span data-ttu-id="d5d61-127">Izleme, Seçenekler ve bağlantı istekleri desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="d5d61-127">TRACE, OPTIONS, and CONNECT requests are not supported.</span></span>

6.  <span data-ttu-id="d5d61-128">HTTP sunucusu veya Istemcisiyle ilişkili paket havuzu, HTTP üst bilgisinin tamamını tutabilecek kadar büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d5d61-128">The packet pool associated with the HTTP Server or Client must be large enough to hold the complete HTTP header.</span></span>

7.  <span data-ttu-id="d5d61-129">HTTP Istemci Hizmetleri yalnızca içerik aktarımına yöneliktir; Bu pakette sunulan bir görüntüleme yardımcı programı yoktur.</span><span class="sxs-lookup"><span data-stu-id="d5d61-129">HTTP Client services are for content transfer only—there are no display utilities provided in this package.</span></span>

## <a name="http-url-resource-names"></a><span data-ttu-id="d5d61-130">HTTP URL 'SI (kaynak adları)</span><span class="sxs-lookup"><span data-stu-id="d5d61-130">HTTP URL (Resource Names)</span></span>

<span data-ttu-id="d5d61-131">HTTP protokolü, Web 'de içerik aktarmak için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="d5d61-131">The HTTP protocol is designed to transfer content on Web.</span></span> <span data-ttu-id="d5d61-132">İstenen içerik Evrensel Kaynak Bulucu (URL) tarafından belirtilir.</span><span class="sxs-lookup"><span data-stu-id="d5d61-132">The requested content is specified by the Universal Resource Locator (URL).</span></span> <span data-ttu-id="d5d61-133">Bu, her HTTP isteğinin birincil bileşenidir.</span><span class="sxs-lookup"><span data-stu-id="d5d61-133">This is the primary component of every HTTP request.</span></span> <span data-ttu-id="d5d61-134">URL 'Ler her zaman bir "/" karakteriyle başlar ve genellikle HTTP sunucusundaki dosyalara karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="d5d61-134">URLs always start with a “/” character and typically correspond to files on the HTTP Server.</span></span> <span data-ttu-id="d5d61-135">Ortak HTTP dosya uzantıları aşağıda gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="d5d61-135">Common HTTP file extensions are shown below:</span></span>

- <span data-ttu-id="d5d61-136">**. htm (veya. html)** Köprü Metni Biçimlendirme Dili (HTML)</span><span class="sxs-lookup"><span data-stu-id="d5d61-136">**.htm (or .html)** Hypertext Markup Language (HTML)</span></span>
- <span data-ttu-id="d5d61-137">**. txt** Düz ASCII metni</span><span class="sxs-lookup"><span data-stu-id="d5d61-137">**.txt** Plain ASCII text</span></span>
- <span data-ttu-id="d5d61-138">**. gif** İkili GIF resmi</span><span class="sxs-lookup"><span data-stu-id="d5d61-138">**.gif** Binary GIF image</span></span>
- <span data-ttu-id="d5d61-139">**. XBM** İkili Xbit eşlem resmi</span><span class="sxs-lookup"><span data-stu-id="d5d61-139">**.xbm** Binary Xbitmap image</span></span>

## <a name="http-client-requests"></a><span data-ttu-id="d5d61-140">HTTP Istemci Istekleri</span><span class="sxs-lookup"><span data-stu-id="d5d61-140">HTTP Client Requests</span></span>

<span data-ttu-id="d5d61-141">HTTP, Web içeriği istemek için basit bir mekanizmaya sahiptir.</span><span class="sxs-lookup"><span data-stu-id="d5d61-141">The HTTP has a simple mechanism for requesting Web content.</span></span> <span data-ttu-id="d5d61-142">Temel olarak *BILINEN TCP bağlantı noktası 80*' de bir bağlantı başarıyla kurulduktan sonra istemci tarafından VERILEN standart http komutları kümesi vardır.</span><span class="sxs-lookup"><span data-stu-id="d5d61-142">There is basically a set of standard HTTP commands that are issued by the Client after a connection has been successfully established on the TCP *well-known port 80*.</span></span> <span data-ttu-id="d5d61-143">Aşağıdakiler, temel HTTP komutlarının bazılarını göstermektedir:</span><span class="sxs-lookup"><span data-stu-id="d5d61-143">The following shows some of the basic HTTP commands:</span></span>

- <span data-ttu-id="d5d61-144">Kaynağı al HTTP/1.0 *belirtilen kaynağı al*</span><span class="sxs-lookup"><span data-stu-id="d5d61-144">GET resource HTTP/1.0 *Get the specified resource*</span></span>
- <span data-ttu-id="d5d61-145">Kaynak SONRASı HTTP/1.0 *belirtilen kaynağı al ve ekli GIRIŞI http sunucusuna geçir*</span><span class="sxs-lookup"><span data-stu-id="d5d61-145">POST resource HTTP/1.0 *Get the specified resource and pass attached input to the HTTP Server*</span></span>
- <span data-ttu-id="d5d61-146">BAŞ kaynak HTTP/1.0 *, http sunucusu tarafından BIR Get, ancak içerik döndürülmüyor gibi değerlendirildi*</span><span class="sxs-lookup"><span data-stu-id="d5d61-146">HEAD resource HTTP/1.0 *Treated like a GET but not content is returned by the HTTP Server*</span></span>
- <span data-ttu-id="d5d61-147">Kaynak YERLEŞTIRME HTTP/1.0 *kaynak kaynağı http sunucusuna*</span><span class="sxs-lookup"><span data-stu-id="d5d61-147">PUT resource HTTP/1.0 *Place resource on HTTP Server*</span></span>
- <span data-ttu-id="d5d61-148">Kaynağı SIL HTTP/1.0 *sunucuda kaynağı Sil*</span><span class="sxs-lookup"><span data-stu-id="d5d61-148">DELETE resource HTTP/1.0 *Delete resource on the Server*</span></span>

<span data-ttu-id="d5d61-149">Bu ASCII komutları, HTTP sunucusu ile HTTP işlemleri gerçekleştirmek için Web tarayıcıları ve NetX HTTP Istemci Hizmetleri tarafından dahili olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d5d61-149">These ASCII commands are generated internally by Web browsers and the NetX HTTP Client services to perform HTTP operations with an HTTP Server.</span></span>

>[!NOTE] 
> <span data-ttu-id="d5d61-150">HTTP Istemci uygulaması varsayılan bağlantı noktası 80 ' dir.</span><span class="sxs-lookup"><span data-stu-id="d5d61-150">The HTTP Client application default to the connect port of 80.</span></span> <span data-ttu-id="d5d61-151">Ancak, *nx_http_client_set_connect_port* hizmetini kullanarak çalışma zamanında bağlantı bağlantı noktasını http sunucusu ile değiştirebilir.</span><span class="sxs-lookup"><span data-stu-id="d5d61-151">However, it can change the connect port to the HTTP Server at runtime using the *nx_http_client_set_connect_port* service.</span></span> <span data-ttu-id="d5d61-152">Bu hizmetin daha fazla ayrıntı için bkz. Bölüm 4.</span><span class="sxs-lookup"><span data-stu-id="d5d61-152">See Chapter 4 for more details of this service.</span></span> <span data-ttu-id="d5d61-153">Bu, zaman zaman Istemci bağlantıları için alternatif bağlantı noktaları kullanan Web sunucularına uyum sağlar.</span><span class="sxs-lookup"><span data-stu-id="d5d61-153">This is to accommodate web servers that occasionally use alternate ports for Client connections.</span></span>

## <a name="http-server-responses"></a><span data-ttu-id="d5d61-154">HTTP sunucusu yanıtları</span><span class="sxs-lookup"><span data-stu-id="d5d61-154">HTTP Server Responses</span></span>

<span data-ttu-id="d5d61-155">HTTP sunucusu, Istemci komut yanıtlarını göndermek için *TANıNMıŞ TCP bağlantı noktası 80* ' ü kullanır.</span><span class="sxs-lookup"><span data-stu-id="d5d61-155">The HTTP Server utilizes the same *well-known TCP port 80* to send Client command responses.</span></span> <span data-ttu-id="d5d61-156">HTTP sunucusu Client komutunu işlediğinde, 3 basamaklı bir sayısal durum kodu içeren bir ASCII yanıt dizesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="d5d61-156">Once the HTTP Server processes the Client command, it returns an ASCII response string that includes a 3-digit numeric status code.</span></span> <span data-ttu-id="d5d61-157">Sayısal yanıt, HTTP Istemci yazılımı tarafından işlemin başarılı veya başarısız olup olmadığını tespit etmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d5d61-157">The numeric response is used by the HTTP Client software to determine whether the operation succeeded or failed.</span></span> <span data-ttu-id="d5d61-158">Istemci komutlarına yönelik çeşitli HTTP sunucu yanıtlarının listesi aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="d5d61-158">Following is a list of various HTTP Server responses to Client commands:</span></span>

- <span data-ttu-id="d5d61-159">200 *isteği başarılı* oldu</span><span class="sxs-lookup"><span data-stu-id="d5d61-159">200 *Request was successful*</span></span>
- <span data-ttu-id="d5d61-160">400 *isteği düzgün biçimlendirilmemiş*</span><span class="sxs-lookup"><span data-stu-id="d5d61-160">400 *Request was not formed properly*</span></span>
- <span data-ttu-id="d5d61-161">401 *yetkisiz istek, istemcinin kimlik doğrulaması gönderebilmesi gerekir*</span><span class="sxs-lookup"><span data-stu-id="d5d61-161">401 *Unauthorized request, client needs to send authentication*</span></span>
- <span data-ttu-id="d5d61-162">404 *belirtilen kaynak bulunamadı*</span><span class="sxs-lookup"><span data-stu-id="d5d61-162">404 *Specified resource in request was not found*</span></span>
- <span data-ttu-id="d5d61-163">500 *Iç http sunucusu hatası*</span><span class="sxs-lookup"><span data-stu-id="d5d61-163">500 *Internal HTTP Server error*</span></span>
- <span data-ttu-id="d5d61-164">501 *ISTEğI http sunucusu tarafından uygulanmadı*</span><span class="sxs-lookup"><span data-stu-id="d5d61-164">501 *Request not implemented by HTTP Server*</span></span>
- <span data-ttu-id="d5d61-165">502 *hizmeti kullanılamıyor*</span><span class="sxs-lookup"><span data-stu-id="d5d61-165">502 *Service is not available*</span></span>

<span data-ttu-id="d5d61-166">Örneğin, "test.htm" dosyasını yERLEşTIRMEk için başarılı bir Istemci isteği "HTTP/1.0 200 Tamam" iletisiyle yanıt verdi.</span><span class="sxs-lookup"><span data-stu-id="d5d61-166">For example, a successful Client request to PUT the file “test.htm” is responded with the message “HTTP/1.0 200 OK.”</span></span>

## <a name="http-communication"></a><span data-ttu-id="d5d61-167">HTTP Iletişimi</span><span class="sxs-lookup"><span data-stu-id="d5d61-167">HTTP Communication</span></span>

<span data-ttu-id="d5d61-168">Daha önce belirtildiği gibi, HTTP sunucusu, Istemci isteklerini alan *iyi BILINEN TCP bağlantı noktası 80* ' ü kullanır.</span><span class="sxs-lookup"><span data-stu-id="d5d61-168">As mentioned previously, the HTTP Server utilizes the *well-known TCP port 80* to field Client requests.</span></span> <span data-ttu-id="d5d61-169">HTTP Istemcileri, kullanılabilir herhangi bir TCP bağlantı noktasını kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="d5d61-169">HTTP Clients may use any available TCP port.</span></span> <span data-ttu-id="d5d61-170">HTTP olaylarının genel sırası aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="d5d61-170">The general sequence of HTTP events is as follows:</span></span>

<span data-ttu-id="d5d61-171">**Http get isteği**:</span><span class="sxs-lookup"><span data-stu-id="d5d61-171">**HTTP GET Request**:</span></span>

1.  <span data-ttu-id="d5d61-172">İstemci, 80 numaralı sunucu bağlantı noktasına TCP Connect sorunları.</span><span class="sxs-lookup"><span data-stu-id="d5d61-172">Client issues TCP connect to Server port 80.</span></span>

2.  <span data-ttu-id="d5d61-173">İstemci "**Get Resource http/1.0**" isteği gönderir (diğer üst bilgi bilgileriyle birlikte).</span><span class="sxs-lookup"><span data-stu-id="d5d61-173">Client sends “**GET resource HTTP/1.0**” request (along with other header information).</span></span>

3.  <span data-ttu-id="d5d61-174">Sunucu "**http/1.0 200 Tamam**" iletisini, daha sonra kaynak içeriği (varsa) tarafından hemen izlenir.</span><span class="sxs-lookup"><span data-stu-id="d5d61-174">Server builds an “**HTTP/1.0 200 OK**” message with additional information followed immediately by the resource content (if any).</span></span>

4.  <span data-ttu-id="d5d61-175">Sunucu bir bağlantı kesmeyi gerçekleştiriyor.</span><span class="sxs-lookup"><span data-stu-id="d5d61-175">Server performs a disconnection.</span></span>

5.  <span data-ttu-id="d5d61-176">İstemci bir bağlantı kesilmesi gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="d5d61-176">Client performs a disconnection.</span></span>

<span data-ttu-id="d5d61-177">**Http put isteği**:</span><span class="sxs-lookup"><span data-stu-id="d5d61-177">**HTTP PUT Request**:</span></span>

1. <span data-ttu-id="d5d61-178">İstemci, 80 numaralı sunucu bağlantı noktasına TCP Connect sorunları.</span><span class="sxs-lookup"><span data-stu-id="d5d61-178">Client issues TCP connect to Server port 80.</span></span>

2. <span data-ttu-id="d5d61-179">İstemci "**PUT Resource http/1.0**" isteği ve diğer başlık bilgilerini ve ardından kaynak içeriğini gönderir.</span><span class="sxs-lookup"><span data-stu-id="d5d61-179">Client sends “**PUT resource HTTP/1.0**” request, along with other header information, and followed by the resource content.</span></span>

3. <span data-ttu-id="d5d61-180">Sunucu, daha sonra kaynak içeriği tarafından izlenen ek bilgiler içeren bir "**http/1.0 200 Tamam**" iletisi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d5d61-180">Server builds an “**HTTP/1.0 200 OK**” message with additional information followed immediately by the resource content.</span></span>

4. <span data-ttu-id="d5d61-181">Sunucu bir bağlantı kesmeyi gerçekleştiriyor.</span><span class="sxs-lookup"><span data-stu-id="d5d61-181">Server performs a disconnection.</span></span>

5. <span data-ttu-id="d5d61-182">İstemci bir bağlantı kesilmesi gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="d5d61-182">Client performs a disconnection.</span></span>

>[!NOTE] 
> <span data-ttu-id="d5d61-183">Daha önce bahsedildiği gibi, HTTP Istemcisi varsayılan bağlantı bağlantı noktasını 80 ' dan başka bir bağlantı noktasına değiştirerek istemcilere bağlanmak için alternatif bağlantı noktaları kullanan Web sunucularının *nx_http_client_set_connect_port* .</span><span class="sxs-lookup"><span data-stu-id="d5d61-183">As mentioned previously, the HTTP Client can change the default connect port from 80 to another port using the *nx_http_client_set_connect_port* for web servers that use alternate ports to connect to clients.</span></span>

## <a name="http-authentication"></a><span data-ttu-id="d5d61-184">HTTP kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="d5d61-184">HTTP Authentication</span></span>

<span data-ttu-id="d5d61-185">HTTP kimlik doğrulaması isteğe bağlıdır ve tüm Web istekleri için gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="d5d61-185">HTTP authentication is optional and isn’t required for all Web requests.</span></span> <span data-ttu-id="d5d61-186">*Temel* ve *Özet* gibi iki kimlik doğrulama özelliği vardır.</span><span class="sxs-lookup"><span data-stu-id="d5d61-186">There are two flavors of authentication, namely *basic* and *digest*.</span></span> <span data-ttu-id="d5d61-187">Temel kimlik doğrulaması, birçok protokolde bulunan *ad* ve *parola* kimlik doğrulamasına eşdeğerdir.</span><span class="sxs-lookup"><span data-stu-id="d5d61-187">Basic authentication is equivalent to the *name* and *password* authentication found in many protocols.</span></span> <span data-ttu-id="d5d61-188">HTTP temel kimlik doğrulamasında ad ve parolalar, Base64 biçiminde birleştirilir ve kodlanır.</span><span class="sxs-lookup"><span data-stu-id="d5d61-188">In HTTP basic authentication, the name and passwords are concatenated and encoded in the base64 format.</span></span> <span data-ttu-id="d5d61-189">Temel kimlik doğrulamasının ana dezavantajı, bu ad ve parolanın istekte openly olarak aktarılmasıdır.</span><span class="sxs-lookup"><span data-stu-id="d5d61-189">The main disadvantage of basic authentication is the name and password are transmitted openly in the request.</span></span> <span data-ttu-id="d5d61-190">Bu, ad ve parolanın çalınabilmesini kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="d5d61-190">This makes it somewhat easy for the name and password to be stolen.</span></span> <span data-ttu-id="d5d61-191">Özet kimlik doğrulaması, istekte hiçbir şekilde adı ve parolayı ileterek bu sorunu giderir.</span><span class="sxs-lookup"><span data-stu-id="d5d61-191">Digest authentication addresses this problem by never transmitting the name and password in the request.</span></span> <span data-ttu-id="d5d61-192">Bunun yerine, ad, parola ve diğer bilgilerden 128 bitlik bir anahtar veya Özet türetmek için bir algoritma kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d5d61-192">Instead, an algorithm is used to derive a 128-bit key or digest from the name, password, and other information.</span></span> <span data-ttu-id="d5d61-193">NetX HTTP sunucusu standart MD5 Özet algoritmasını destekler.</span><span class="sxs-lookup"><span data-stu-id="d5d61-193">The NetX HTTP Server supports the standard MD5 digest algorithm.</span></span>

<span data-ttu-id="d5d61-194">Kimlik doğrulaması ne zaman gerekir?</span><span class="sxs-lookup"><span data-stu-id="d5d61-194">When is authentication required?</span></span> <span data-ttu-id="d5d61-195">Temel olarak, HTTP sunucusu, istenen bir kaynağın kimlik doğrulaması gerektirip gerektirmediğini belirler.</span><span class="sxs-lookup"><span data-stu-id="d5d61-195">Basically, the HTTP Server decides if a requested resource requires authentication.</span></span> <span data-ttu-id="d5d61-196">Kimlik doğrulaması gerekliyse ve Istemci isteği uygun kimlik doğrulamasını içermiyorsa, gerekli kimlik doğrulama türüne sahip "HTTP/1.0 401 Yetkisiz" yanıtı Istemciye gönderilir.</span><span class="sxs-lookup"><span data-stu-id="d5d61-196">If authentication is required and the Client request did not include the proper authentication, a “HTTP/1.0 401 Unauthorized” response with the type of authentication required is sent to the Client.</span></span> <span data-ttu-id="d5d61-197">Daha sonra Istemci, doğru kimlik doğrulamasıyla yeni bir istek oluşturacak şekilde beklenir.</span><span class="sxs-lookup"><span data-stu-id="d5d61-197">The Client is then expected to form a new request with the proper authentication.</span></span>

## <a name="http-authentication-callback"></a><span data-ttu-id="d5d61-198">HTTP kimlik doğrulaması geri araması</span><span class="sxs-lookup"><span data-stu-id="d5d61-198">HTTP Authentication Callback</span></span>

<span data-ttu-id="d5d61-199">Daha önce belirtildiği gibi, HTTP kimlik doğrulaması isteğe bağlıdır ve tüm Web aktarımları için gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="d5d61-199">As mentioned before, HTTP authentication is optional and isn’t required on all Web transfers.</span></span> <span data-ttu-id="d5d61-200">Ayrıca, kimlik doğrulama genellikle kaynağa bağımlıdır.</span><span class="sxs-lookup"><span data-stu-id="d5d61-200">In addition, authentication is typically resource dependent.</span></span> <span data-ttu-id="d5d61-201">Sunucu üzerindeki bazı kaynaklara erişim için kimlik doğrulaması gerekir, diğerleri desteklemez.</span><span class="sxs-lookup"><span data-stu-id="d5d61-201">Access of some resources on the Server require authentication, while others do not.</span></span> <span data-ttu-id="d5d61-202">NetX HTTP sunucu paketi, uygulamanın, her HTTP Istemci isteğini işlemenin başlangıcında çağrılan bir kimlik doğrulama geri çağırma yordamı ( ***nx_http_server_create*** çağrısı aracılığıyla) belirtmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="d5d61-202">The NetX HTTP Server package allows the application to specify (via the ***nx_http_server_create*** call) an authentication callback routine that is called at the beginning of handling each HTTP Client request.</span></span>

<span data-ttu-id="d5d61-203">Geri arama yordamı, NetX HTTP sunucusunu kaynakla ilişkili Kullanıcı adı, parola ve bölge dizeleri sağlar ve gereken kimlik doğrulaması türünü döndürür.</span><span class="sxs-lookup"><span data-stu-id="d5d61-203">The callback routine provides the NetX HTTP Server with the username, password, and realm strings associated with the resource and return the type of authentication necessary.</span></span> <span data-ttu-id="d5d61-204">Kaynak için kimlik doğrulaması gerekli değilse, kimlik doğrulama geri araması **NX_HTTP_DONT_AUTHENTICATE** değerini döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="d5d61-204">If no authentication is necessary for the resource, the authentication callback should return the value of **NX_HTTP_DONT_AUTHENTICATE**.</span></span> <span data-ttu-id="d5d61-205">Aksi halde, belirtilen kaynak için temel kimlik doğrulaması gerekliyse, yordam **NX_HTTP_BASIC_AUTHENTICATE** döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="d5d61-205">Otherwise, if basic authentication is required for the specified resource, the routine should return **NX_HTTP_BASIC_AUTHENTICATE**.</span></span> <span data-ttu-id="d5d61-206">Son olarak, MD5 Özet kimlik doğrulaması gerekliyse, geri arama yordamı **NX_HTTP_DIGEST_AUTHENTICATE** döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="d5d61-206">And finally, if MD5 digest authentication is required, the callback routine should return **NX_HTTP_DIGEST_AUTHENTICATE**.</span></span> <span data-ttu-id="d5d61-207">HTTP sunucusu tarafından sunulan herhangi bir kaynak için kimlik doğrulaması gerekmiyorsa, geri çağırma gerekmez ve HTTP sunucusu oluşturma çağrısına boş bir işaretçi sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d5d61-207">If no authentication is required for any resource provided by the HTTP Server, the callback is not needed and a NULL pointer can be provided to the HTTP Server create call.</span></span>

<span data-ttu-id="d5d61-208">Uygulama kimlik doğrulaması geri arama yordamının biçimi çok basittir ve aşağıda tanımlanmıştır:</span><span class="sxs-lookup"><span data-stu-id="d5d61-208">The format of the application authenticate callback routine is very simple and is defined below:</span></span>

```c
UINT nx_http_server_authentication_check (NX_HTTP_SERVER *server_ptr,
                                         UINT request_type, CHAR *resource,
                                         CHAR **name, CHAR **password,
                                         CHAR **realm);
```

<span data-ttu-id="d5d61-209">Giriş parametreleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="d5d61-209">The input parameters are defined as follows:</span></span>

- <span data-ttu-id="d5d61-210">*request_type* HTTP Istemci isteğini belirtir, geçerli istekler şu şekilde tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="d5d61-210">*request_type* Specifies the HTTP Client request, valid requests are defined as:</span></span>
  - <span data-ttu-id="d5d61-211">**NX_HTTP_SERVER_GET_REQUEST**</span><span class="sxs-lookup"><span data-stu-id="d5d61-211">**NX_HTTP_SERVER_GET_REQUEST**</span></span>
  - <span data-ttu-id="d5d61-212">**NX_HTTP_SERVER_POST_REQUEST**</span><span class="sxs-lookup"><span data-stu-id="d5d61-212">**NX_HTTP_SERVER_POST_REQUEST**</span></span>
  - <span data-ttu-id="d5d61-213">**NX_HTTP_SERVER_HEAD_REQUEST**</span><span class="sxs-lookup"><span data-stu-id="d5d61-213">**NX_HTTP_SERVER_HEAD_REQUEST**</span></span>
  - <span data-ttu-id="d5d61-214">**NX_HTTP_SERVER_PUT_REQUEST**</span><span class="sxs-lookup"><span data-stu-id="d5d61-214">**NX_HTTP_SERVER_PUT_REQUEST**</span></span>
  - <span data-ttu-id="d5d61-215">**NX_HTTP_SERVER_DELETE_REQUEST**</span><span class="sxs-lookup"><span data-stu-id="d5d61-215">**NX_HTTP_SERVER_DELETE_REQUEST**</span></span>
- <span data-ttu-id="d5d61-216">*kaynak* Belirli bir kaynak istendi.</span><span class="sxs-lookup"><span data-stu-id="d5d61-216">*resource* Specific resource requested.</span></span>
- <span data-ttu-id="d5d61-217">*ad* Gerekli Kullanıcı adına işaretçinin hedefi.</span><span class="sxs-lookup"><span data-stu-id="d5d61-217">*name* Destination for the pointer to the required username.</span></span>
- <span data-ttu-id="d5d61-218">*parola* Gerekli parolaya yönelik işaretçinin hedefi.</span><span class="sxs-lookup"><span data-stu-id="d5d61-218">*password* Destination for the pointer to the required password.</span></span>
- <span data-ttu-id="d5d61-219">*bölge* Bu kimlik doğrulaması için bölge işaretçisinin hedefi.</span><span class="sxs-lookup"><span data-stu-id="d5d61-219">*realm* Destination for the pointer to the realm for this authentication.</span></span>

<span data-ttu-id="d5d61-220">Kimlik doğrulama yordamının dönüş değeri, kimlik doğrulamasının gerekli olup olmadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="d5d61-220">The return value of the authentication routine specifies if authentication is required.</span></span> <span data-ttu-id="d5d61-221">kimlik doğrulama geri çağırma yordamı tarafından **NX_HTTP_DONT_AUTHENTICATE** döndürülürse ad, parola ve bölge işaretçileri kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="d5d61-221">name, password, and realm pointers are not used if **NX_HTTP_DONT_AUTHENTICATE** is returned by the authentication callback routine.</span></span> <span data-ttu-id="d5d61-222">Aksi halde, HTTP sunucu geliştiricisi, *nx_http_server. h* içinde tanımlanan **NX_HTTP_MAX_USERNAME** ve **NX_HTTP_MAX_PASSWORD** kimlik doğrulama geri aramasında belirtilen Kullanıcı adı ve parola için yeterince büyük olduğundan emin olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d5d61-222">Otherwise the HTTP server developer must ensure that **NX_HTTP_MAX_USERNAME** and **NX_HTTP_MAX_PASSWORD** defined in *nx_http_server.h* are large enough for the username and password specified in the authentication callback.</span></span> <span data-ttu-id="d5d61-223">Bunların ikisi de varsayılan olarak 20 karakter olacak şekilde ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="d5d61-223">These are both defaulted to size 20 chars.</span></span>

## <a name="http-invalid-usernamepassword-callback"></a><span data-ttu-id="d5d61-224">HTTP geçersiz Kullanıcı adı/parola geri çağırması</span><span class="sxs-lookup"><span data-stu-id="d5d61-224">HTTP Invalid Username/Password Callback</span></span>

<span data-ttu-id="d5d61-225">HTTP sunucusu bir Istemci isteğinde geçersiz bir Kullanıcı adı ve parola birleşimi alırsa NetX HTTP sunucusunda isteğe bağlı geçersiz Kullanıcı adı/parola geri çağırması çağrılır.</span><span class="sxs-lookup"><span data-stu-id="d5d61-225">The optional invalid username/password callback in NetX HTTP Server is invoked if HTTP server receives an invalid username and password combination in a Client request.</span></span> <span data-ttu-id="d5d61-226">HTTP sunucusu uygulaması HTTP sunucusu ile bir geri çağırma kaydederse, *nx_http_server_get_process*, *nx_http_server_put_process* veya nx_http_server_delete_process ' de temel veya Özet kimlik doğrulaması başarısız olursa çağrılacaktır *.*</span><span class="sxs-lookup"><span data-stu-id="d5d61-226">If the HTTP server application registers a callback with HTTP server it will be invoked if either basic or digest authentication fails *in nx_http_server_get_process*, in *nx_http_server_put_process,* or *in nx_http_server_delete_process.*</span></span>

<span data-ttu-id="d5d61-227">HTTP sunucusuyla bir geri çağırma kaydetmek için, NetX HTTP sunucusunda aşağıdaki hizmet tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="d5d61-227">To register a callback with the HTTP server, the following service is defined in NetX HTTP Server.</span></span>

```c
UINT nx_http_server_invalid_userpassword_notify_set (NX_HTTP_SERVER *http_server_ptr,
                                                    UINT *invalid_username_password_callback)
                                                    (CHAR *resource,
                                                    ULONG *client_nx_address,
                                                    UINT request_type));
```
<span data-ttu-id="d5d61-228">İstek türleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="d5d61-228">The request types are defined as follows:</span></span>

- <span data-ttu-id="d5d61-229">**NX_HTTP_SERVER_GET_REQUEST**</span><span class="sxs-lookup"><span data-stu-id="d5d61-229">**NX_HTTP_SERVER_GET_REQUEST**</span></span>
- <span data-ttu-id="d5d61-230">**NX_HTTP_SERVER_POST_REQUEST**</span><span class="sxs-lookup"><span data-stu-id="d5d61-230">**NX_HTTP_SERVER_POST_REQUEST**</span></span>
- <span data-ttu-id="d5d61-231">**NX_HTTP_SERVER_HEAD_REQUEST**</span><span class="sxs-lookup"><span data-stu-id="d5d61-231">**NX_HTTP_SERVER_HEAD_REQUEST**</span></span>
- <span data-ttu-id="d5d61-232">**NX_HTTP_SERVER_PUT_REQUEST**</span><span class="sxs-lookup"><span data-stu-id="d5d61-232">**NX_HTTP_SERVER_PUT_REQUEST**</span></span>
- <span data-ttu-id="d5d61-233">**NX_HTTP_SERVER_DELETE_REQUEST**</span><span class="sxs-lookup"><span data-stu-id="d5d61-233">**NX_HTTP_SERVER_DELETE_REQUEST**</span></span>

## <a name="http-insert-gmt-date-header-callback"></a><span data-ttu-id="d5d61-234">HTTP ekleme GMT Tarih üst bilgisi geri araması</span><span class="sxs-lookup"><span data-stu-id="d5d61-234">HTTP Insert GMT Date Header Callback</span></span>

<span data-ttu-id="d5d61-235">NetX HTTP sunucusunda, yanıt iletilerinde bir tarih üst bilgisi eklemek için isteğe bağlı bir geri çağırma vardır.</span><span class="sxs-lookup"><span data-stu-id="d5d61-235">There is an optional callback in NetX HTTP Server to insert a date header in its response messages.</span></span> <span data-ttu-id="d5d61-236">HTTP sunucusu bir put veya GET isteğine yanıt vermediğinde bu geri çağırma çağrılır</span><span class="sxs-lookup"><span data-stu-id="d5d61-236">This callback is invoked when the HTTP Server is responding to a put or get request</span></span>

<span data-ttu-id="d5d61-237">HTTP sunucusuna bir GMT Tarih geri çağırması kaydetmek için, NetX HTTP sunucusunda aşağıdaki hizmet tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="d5d61-237">To register a GMT date callback with the HTTP server, the following service is defined in the NetX HTTP Server.</span></span>

```c
UINT _nx_http_server_gmt_callback_set(NX_HTTP_SERVER *server_ptr,
                                     VOID (*gmt_get)(NX_HTTP_SERVER_DATE *date);
```

<span data-ttu-id="d5d61-238">NX_HTTP_SERVER_DATE veri türü aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="d5d61-238">The NX_HTTP_SERVER_DATE data type is defined as follows:</span></span>

```c
typedef struct NX_HTTP_SERVER_DATE_STRUCT
{
    USHORT     nx_http_server_year;         /* Year        */
    UCHAR      nx_http_server_month;        /* Month       */
    UCHAR      nx_http_server_day;          /* Day         */
    UCHAR      nx_http_server_hour;         /* Hour        */
    UCHAR      nx_http_server_minute;       /* Minute      */
    UCHAR      nx_http_server_second;       /* Second      */
    UCHAR      nx_http_server_weekday;      /* Weekday     */
} NX_HTTP_SERVER_DATE;
```

## <a name="http-cache-info-get-callback"></a><span data-ttu-id="d5d61-239">HTTP önbellek bilgileri geri çağırma al</span><span class="sxs-lookup"><span data-stu-id="d5d61-239">HTTP Cache Info Get Callback</span></span>

<span data-ttu-id="d5d61-240">HTTP sunucusu, belirli bir kaynak için HTTP uygulamasından maksimum yaş ve Tarih istemek üzere bir geri çağırma işlemi içerir.</span><span class="sxs-lookup"><span data-stu-id="d5d61-240">The HTTP Server has a callback to request the max age and date from the HTTP application for a specific resource.</span></span> <span data-ttu-id="d5d61-241">Bu bilgiler, HTTP sunucusunun bir Istemci GET isteğine yanıt olarak tüm sayfayı gönderip göndermediğini tespit etmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d5d61-241">This information is used to determine if the HTTP server sends the entire page in response to a Client Get request.</span></span> <span data-ttu-id="d5d61-242">Istemci isteğindeki "değiştirilme sonrasında" veya alma önbelleği geri araması tarafından döndürülen "son değiştirilme" tarihi ile eşleşmiyorsa, sayfanın tamamı gönderilir.</span><span class="sxs-lookup"><span data-stu-id="d5d61-242">If the “if modified since” in the Client request is not found or does not match the “last modified” date returned by the get cache callback, the entire page is sent.</span></span>

<span data-ttu-id="d5d61-243">Geri aramayı HTTP sunucusuna kaydetmek için aşağıdaki hizmet tanımlanmıştır:</span><span class="sxs-lookup"><span data-stu-id="d5d61-243">To register the callback with the HTTP server the following service is defined:</span></span>

```c
UINT _nx_http_server_cache_info_callback_set(NX_HTTP_SERVER *server_ptr,
                                            UINT (*cache_info_get)
                                            (CHAR *, UINT *, NX_HTTP_SERVER_DATE *));
```

## <a name="http-multipart-support"></a><span data-ttu-id="d5d61-244">HTTP çok parçalı desteği</span><span class="sxs-lookup"><span data-stu-id="d5d61-244">HTTP Multipart Support</span></span>

<span data-ttu-id="d5d61-245">Çok amaçlı Internet posta uzantıları (MIME) başlangıçta SMTP protokolüne yöneliktir, ancak kullanımı HTTP 'ye yayılmıştır.</span><span class="sxs-lookup"><span data-stu-id="d5d61-245">Multipurpose Internet Mail Extensions (MIME) was originally intended for the SMTP protocol, but its use has spread to HTTP.</span></span> <span data-ttu-id="d5d61-246">MIME, iletilerin aynı ileti içinde karma ileti türlerini (ör. image/jpg ve metin/düz) içermesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="d5d61-246">MIME allows messages to contain mixed message types (e.g. image/jpg and text/plain) within the same message.</span></span> <span data-ttu-id="d5d61-247">NetX HTTP sunucusu, Istemciden MIME içeren HTTP iletilerindeki içerik türünü belirlemede hizmetler ekledi.</span><span class="sxs-lookup"><span data-stu-id="d5d61-247">NetX HTTP Server has added services to determine content type in HTTP messages containing MIME from the Client.</span></span> <span data-ttu-id="d5d61-248">HTTP çok parçalı desteğini etkinleştirmek ve bu hizmetleri kullanmak için **NX_HTTP_MULTIPART_ENABLE** yapılandırma seçeneğinin tanımlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d5d61-248">To enable HTTP multipart support and use these services, the configuration option **NX_HTTP_MULTIPART_ENABLE** must be defined.</span></span>

```c
UINT nx_http_server_get_entity_header(NX_HTTP_SERVER *server_ptr,
                                     NX_PACKET **packet_pptr,
                                     UCHAR *entity_header_buffer,
                                     ULONG buffer_size);

UINT nx_http_server_get_entity_content(NX_HTTP_SERVER *server_ptr,
                                      NX_PACKET **packet_pptr,
                                      ULONG *available_offset,
                                      ULONG *available_length);
```

<span data-ttu-id="d5d61-249">Bu hizmetlerin kullanımı hakkında daha fazla bilgi için, Bölüm 3 "HTTP hizmetlerinin açıklaması" bölümünde açıklamasına bakın.</span><span class="sxs-lookup"><span data-stu-id="d5d61-249">For more details on the use of these services, see their description in Chapter 3 “Description of HTTP Services”.</span></span>

## <a name="http-multi-thread-support"></a><span data-ttu-id="d5d61-250">HTTP çoklu Iş parçacığı desteği</span><span class="sxs-lookup"><span data-stu-id="d5d61-250">HTTP Multi-Thread Support</span></span>

<span data-ttu-id="d5d61-251">NetX HTTP Istemci Hizmetleri birden çok iş parçacığından aynı anda çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="d5d61-251">The NetX HTTP Client services can be called from multiple threads simultaneously.</span></span> <span data-ttu-id="d5d61-252">Ancak, belirli bir HTTP Istemci örneği için okuma veya yazma istekleri aynı iş parçacığından sırayla yapılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d5d61-252">However, read or write requests for a particular HTTP Client instance should be done in sequence from the same thread.</span></span>

## <a name="http-rfcs"></a><span data-ttu-id="d5d61-253">HTTP RFC 'Leri</span><span class="sxs-lookup"><span data-stu-id="d5d61-253">HTTP RFCs</span></span>

<span data-ttu-id="d5d61-254">NetX HTTP, RFC1945 "Hypertext Transfer Protocol/1.0", RFC 2581 "TCP tıkanıklık denetimi", RFC 1122 "Internet konakları için gereksinimler" ve ilgili RFC 'Ler ile uyumludur.</span><span class="sxs-lookup"><span data-stu-id="d5d61-254">NetX HTTP is compliant with RFC1945 “Hypertext Transfer Protocol/1.0”, RFC 2581 “TCP Congestion Control”, RFC 1122 “Requirements for Internet Hosts”, and related RFCs.</span></span>