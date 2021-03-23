---
title: Bölüm 1-Azure RTOS NetX Duo TFTP 'ye giriş
description: Önemsiz Dosya Aktarım Protokolü (TFTP), dosya aktarımları için tasarlanan hafif bir protokoldür.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 4431b23e143d05214090547e7f179a6f5def8217
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825709"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-tftp"></a><span data-ttu-id="5c2b2-103">Bölüm 1-Azure RTOS NetX Duo TFTP 'ye giriş</span><span class="sxs-lookup"><span data-stu-id="5c2b2-103">Chapter 1 - Introduction to Azure RTOS NetX Duo TFTP</span></span> 

<span data-ttu-id="5c2b2-104">Önemsiz Dosya Aktarım Protokolü (TFTP), dosya aktarımları için tasarlanan hafif bir protokoldür.</span><span class="sxs-lookup"><span data-stu-id="5c2b2-104">The Trivial File Transfer Protocol (TFTP) is a lightweight protocol designed for file transfers.</span></span> <span data-ttu-id="5c2b2-105">Daha sağlam protokollerin aksine, TFTP kapsamlı hata denetimi gerçekleştirmez ve ayrıca, bir durdurma ve bekleme Protokolü olduğundan sınırlı performansa sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="5c2b2-105">Unlike more robust protocols, TFTP does not perform extensive error checking and can also have limited performance because it is a stop-and-wait protocol.</span></span> <span data-ttu-id="5c2b2-106">Bir TFTP veri paketi gönderildikten sonra gönderen, alıcı tarafından bir ACK döndürülmesini bekler.</span><span class="sxs-lookup"><span data-stu-id="5c2b2-106">After a TFTP data packet is sent, the sender waits for an ACK to be returned by the recipient.</span></span> <span data-ttu-id="5c2b2-107">Bu basit olsa da, genel TFTP verimini sınırlandırır.</span><span class="sxs-lookup"><span data-stu-id="5c2b2-107">Although this is simple, it does limit the overall TFTP throughput.</span></span> <span data-ttu-id="5c2b2-108">TFTP paketi, ana bilgisayarların IP ağları üzerinde TFTP protokolünü kullanmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="5c2b2-108">The TFTP package enables hosts to use the TFTP protocol over IP networks.</span></span>

## <a name="tftp-requirements"></a><span data-ttu-id="5c2b2-109">TFTP gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="5c2b2-109">TFTP Requirements</span></span>

<span data-ttu-id="5c2b2-110">Düzgün çalışması için, NetX Duo TFTP paketinin TFTP Istemcileri bölümü bir IP örneğinin zaten oluşturulmuş olmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="5c2b2-110">In order to function properly, the TFTP Clients portion of the NetX Duo TFTP package requires that an IP instance has already been created.</span></span> <span data-ttu-id="5c2b2-111">Buna ek olarak, aynı IP örneğinde UDP 'nin etkinleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="5c2b2-111">In addition, UDP must be enabled on that same IP instance.</span></span> <span data-ttu-id="5c2b2-112">NetX Duo TFTP paketinin Istemci bölümünün başka gereksinimi yoktur.</span><span class="sxs-lookup"><span data-stu-id="5c2b2-112">The Client portion of the NetX Duo TFTP package has no further requirements.</span></span>

<span data-ttu-id="5c2b2-113">NetX Duo TFTP paketinin TFTP sunucu bölümü bazı ek gereksinimlere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="5c2b2-113">The TFTP Server portion of the NetX Duo TFTP package has several additional requirements.</span></span> <span data-ttu-id="5c2b2-114">İlk olarak, tüm istemci TFTP isteklerini işlemek için UDP 'nin *bilinen ve 69 numaralı bağlantı noktası* için tüm erişimi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="5c2b2-114">First, it requires complete access to the UDP *well known port 69* for handling all client TFTP requests.</span></span> <span data-ttu-id="5c2b2-115">TFTP sunucusu Ayrıca, FileX Embedded dosya sistemiyle kullanılmak üzere tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="5c2b2-115">The TFTP Server is also designed for use with the FileX embedded file system.</span></span> <span data-ttu-id="5c2b2-116">FileX yoksa, Kullanıcı kendi ortamlarında kullanılan FileX bölümlerinin bağlantı noktasını alabilir.</span><span class="sxs-lookup"><span data-stu-id="5c2b2-116">If FileX is not available, the user may port the portions of FileX used to their own environment.</span></span> <span data-ttu-id="5c2b2-117">Bu, bu kılavuzun sonraki bölümlerinde ele alınmıştır.</span><span class="sxs-lookup"><span data-stu-id="5c2b2-117">This is discussed in later sections of this guide.</span></span>

## <a name="tftp-file-names"></a><span data-ttu-id="5c2b2-118">TFTP dosya adları</span><span class="sxs-lookup"><span data-stu-id="5c2b2-118">TFTP File Names</span></span> 

<span data-ttu-id="5c2b2-119">TFTP dosya adları, hedef dosya sisteminin biçiminde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5c2b2-119">TFTP file names should be in the format of the target file system.</span></span> <span data-ttu-id="5c2b2-120">Gerektiğinde tam yol bilgileriyle, NULL olarak sonlandırılmış ASCII dizeleri olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5c2b2-120">They should be NULL terminated ASCII strings, with full path information if necessary.</span></span> <span data-ttu-id="5c2b2-121">NetX Duo TFTP uygulamasında TFTP dosya adlarının boyutunda belirtilen sınır yoktur.</span><span class="sxs-lookup"><span data-stu-id="5c2b2-121">There is no specified limit in the size of TFTP file names in the NetX Duo TFTP implementation.</span></span>

## <a name="tftp-messages"></a><span data-ttu-id="5c2b2-122">TFTP Iletileri</span><span class="sxs-lookup"><span data-stu-id="5c2b2-122">TFTP Messages</span></span>

<span data-ttu-id="5c2b2-123">TFTP, dosyaları açmak, okumak, yazmak ve kapatmak için çok basit bir mekanizmaya sahiptir.</span><span class="sxs-lookup"><span data-stu-id="5c2b2-123">The TFTP has a very simple mechanism for opening, reading, writing, and closing files.</span></span> <span data-ttu-id="5c2b2-124">UDP üstbilgisinin altında temel olarak 2-4 baytlık TFTP üstbilgisi vardır.</span><span class="sxs-lookup"><span data-stu-id="5c2b2-124">There are basically 2-4 bytes of TFTP header underneath the UDP header.</span></span> <span data-ttu-id="5c2b2-125">TFTP dosyası açık iletilerinin tanımı aşağıdaki biçimdedir:</span><span class="sxs-lookup"><span data-stu-id="5c2b2-125">The definition of the TFTP file open messages has the following format:</span></span>

<span data-ttu-id="5c2b2-126">**oooof... f0OCTET0**</span><span class="sxs-lookup"><span data-stu-id="5c2b2-126">**oooof…f0OCTET0**</span></span>

<span data-ttu-id="5c2b2-127">Konum:</span><span class="sxs-lookup"><span data-stu-id="5c2b2-127">Where:</span></span>

- <span data-ttu-id="5c2b2-128">**oooo** 2 baytlık Opcode alanı</span><span class="sxs-lookup"><span data-stu-id="5c2b2-128">**oooo** 2-byte Opcode field</span></span>  
<span data-ttu-id="5c2b2-129">0x0001-okuma için > açın</span><span class="sxs-lookup"><span data-stu-id="5c2b2-129">0x0001 -> Open for read</span></span>  
<span data-ttu-id="5c2b2-130">0x0002-yazma için > açın</span><span class="sxs-lookup"><span data-stu-id="5c2b2-130">0x0002 -> Open for write</span></span>

- <span data-ttu-id="5c2b2-131">**f... f** n-bayt dosya adı alanı</span><span class="sxs-lookup"><span data-stu-id="5c2b2-131">**f…f** n-byte Filename field</span></span>

- <span data-ttu-id="5c2b2-132">0 1-byte NULL sonlandırma karakteri</span><span class="sxs-lookup"><span data-stu-id="5c2b2-132">0  1-byte NULL termination character</span></span>

- <span data-ttu-id="5c2b2-133">**Sekizli** İkili aktarım belirtmek için ASCII "SEKIZLI"</span><span class="sxs-lookup"><span data-stu-id="5c2b2-133">**OCTET** ASCII “OCTET” to specify binary transfer</span></span>

- <span data-ttu-id="5c2b2-134">0 1-byte NULL sonlandırma karakteri</span><span class="sxs-lookup"><span data-stu-id="5c2b2-134">0  1-byte NULL termination character</span></span>

<span data-ttu-id="5c2b2-135">TFTP yazma, ACK ve hata iletilerinin tanımı biraz farklıdır ve aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="5c2b2-135">The definition of the TFTP write, ACK, and error messages are slightly different and are defined as follows:</span></span>

<span data-ttu-id="5c2b2-136">**oooobbbbd... TID**</span><span class="sxs-lookup"><span data-stu-id="5c2b2-136">**oooobbbbd…d**</span></span>

<span data-ttu-id="5c2b2-137">Konum:</span><span class="sxs-lookup"><span data-stu-id="5c2b2-137">Where:</span></span>

- <span data-ttu-id="5c2b2-138">**oooo** 2 baytlık Opcode alanı</span><span class="sxs-lookup"><span data-stu-id="5c2b2-138">**oooo** 2-byte Opcode field</span></span>  
<span data-ttu-id="5c2b2-139">0x0003-> veri paketi</span><span class="sxs-lookup"><span data-stu-id="5c2b2-139">0x0003 -> Data packet</span></span>  
<span data-ttu-id="5c2b2-140">0x0004-son okuma için > ACK</span><span class="sxs-lookup"><span data-stu-id="5c2b2-140">0x0004 -> ACK for last read</span></span>  
<span data-ttu-id="5c2b2-141">0x0005-> hata koşulu</span><span class="sxs-lookup"><span data-stu-id="5c2b2-141">0x0005 -> Error condition</span></span>  

- <span data-ttu-id="5c2b2-142">**bbbb** 2-Byte blok numarası alanı (1-n)</span><span class="sxs-lookup"><span data-stu-id="5c2b2-142">**bbbb** 2-byte Block Number field (1-n)</span></span>

- <span data-ttu-id="5c2b2-143">**d... d** n-Byte veri alanı</span><span class="sxs-lookup"><span data-stu-id="5c2b2-143">**d…d** n-byte Data field</span></span>


- <span data-ttu-id="5c2b2-144">0x0001 (okuma) dosya adı 0 SEKIZLI 0</span><span class="sxs-lookup"><span data-stu-id="5c2b2-144">0x0001 (read) File Name 0 OCTET 0</span></span>

- <span data-ttu-id="5c2b2-145">0x0002 (yazma) dosya adı 0 SEKIZLI 0</span><span class="sxs-lookup"><span data-stu-id="5c2b2-145">0x0002 (write) File Name 0 OCTET 0</span></span>

## <a name="tftp-communication"></a><span data-ttu-id="5c2b2-146">TFTP Iletişimi</span><span class="sxs-lookup"><span data-stu-id="5c2b2-146">TFTP Communication</span></span>

<span data-ttu-id="5c2b2-147">TFTP sunucuları Istemci isteklerini dinlemek için iyi bilinen UDP bağlantı noktası 69 ' ü kullanır.</span><span class="sxs-lookup"><span data-stu-id="5c2b2-147">TFTP Servers utilize the well-known UDP port 69 to listen for Client requests.</span></span> <span data-ttu-id="5c2b2-148">TFTP Istemci yuvaları, kullanılabilir herhangi bir UDP bağlantı noktasına bağlanamaz.</span><span class="sxs-lookup"><span data-stu-id="5c2b2-148">TFTP Client sockets may bind to any available UDP port.</span></span> <span data-ttu-id="5c2b2-149">Karşıya yüklenecek veya İndirilecek dosyayı içeren veri paketi yükü, < 512 bayt içeren son pakete kadar 512 bayt öbeklerine gönderilir.</span><span class="sxs-lookup"><span data-stu-id="5c2b2-149">Data packet payload containing the file to upload or download is sent in 512 byte chunks, until the last packet containing < 512 bytes.</span></span> <span data-ttu-id="5c2b2-150">Bu nedenle 512 bayttan az olan bir paket, dosyanın sonuna işaret eder.</span><span class="sxs-lookup"><span data-stu-id="5c2b2-150">Therefore a packet containing fewer than 512 bytes signals the end of file.</span></span> <span data-ttu-id="5c2b2-151">Genel olay sırası aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="5c2b2-151">The general sequence of events is as follows:</span></span>

<span data-ttu-id="5c2b2-152">TFTP okuma dosyası Istekleri:</span><span class="sxs-lookup"><span data-stu-id="5c2b2-152">TFTP Read File Requests:</span></span>

1.  <span data-ttu-id="5c2b2-153">Istemci, dosya adıyla bir "okuma Için aç" isteği yayınlar ve sunucudan bir yanıt bekler.</span><span class="sxs-lookup"><span data-stu-id="5c2b2-153">The Client issues an “Open For Read” request with the file name and waits for a reply from the Server.</span></span>

2.  <span data-ttu-id="5c2b2-154">Sunucu, dosyanın ilk 512 baytını veya dosya boyutu 512 bayttan az olursa daha az bir değer gönderir.</span><span class="sxs-lookup"><span data-stu-id="5c2b2-154">The Server sends the first 512 bytes of the file or less if the file size is less than 512 bytes.</span></span>

3.  <span data-ttu-id="5c2b2-155">Istemci verileri alır, bir ACK gönderir ve 512 bayttan fazla dosya içeren dosyalar için sunucudan sonraki paketi bekler.</span><span class="sxs-lookup"><span data-stu-id="5c2b2-155">The Client receives data, sends an ACK, and waits for the next packet from the Server for files containing more than 512 bytes.</span></span>

4.  <span data-ttu-id="5c2b2-156">Istemci 512 bayttan daha az bir paket aldığında sıra sona erer.</span><span class="sxs-lookup"><span data-stu-id="5c2b2-156">The sequence ends when the Client receives a packet containing fewer than 512 bytes.</span></span>

<span data-ttu-id="5c2b2-157">TFTP yazma Istekleri:</span><span class="sxs-lookup"><span data-stu-id="5c2b2-157">TFTP Write Requests:</span></span>

1.  <span data-ttu-id="5c2b2-158">Istemci, dosya adıyla bir "yazma için aç" isteği yayınlar ve sunucudan blok numarası 0 olan bir ACK 'e bekler.</span><span class="sxs-lookup"><span data-stu-id="5c2b2-158">The Client issues an “Open for Write” request with the file name and waits for an ACK with a block number of 0 from the Server.</span></span>

2.  <span data-ttu-id="5c2b2-159">Sunucu, dosyayı yazmaya hazırsa, blok numarası sıfır olan bir ACK gönderir.</span><span class="sxs-lookup"><span data-stu-id="5c2b2-159">When the Server is ready to write the file, it sends an ACK with a block number of zero.</span></span>

3.  <span data-ttu-id="5c2b2-160">Istemci, dosyanın ilk 512 baytını sunucuya (veya 512 bayttan daha az dosya için daha az) gönderir ve geri BILDIRIM bekler.</span><span class="sxs-lookup"><span data-stu-id="5c2b2-160">The Client sends the first 512 bytes of the file (or less for files less than 512 bytes) to the Server and waits for an ACK back.</span></span>

4.  <span data-ttu-id="5c2b2-161">Sunucu, baytlar yazıldıktan sonra bir ACK gönderir.</span><span class="sxs-lookup"><span data-stu-id="5c2b2-161">The Server sends an ACK after the bytes are written.</span></span>

5.  <span data-ttu-id="5c2b2-162">Sıra, Istemci 512 bayttan daha az bir paket yazmayı tamamladığında sona erer.</span><span class="sxs-lookup"><span data-stu-id="5c2b2-162">The sequence ends when the Client completes writing a packet containing fewer than 512 bytes.</span></span>
 

## <a name="tftp-server-session-timer"></a><span data-ttu-id="5c2b2-163">TFTP sunucusu oturum süreölçeri</span><span class="sxs-lookup"><span data-stu-id="5c2b2-163">TFTP Server Session Timer</span></span>

<span data-ttu-id="5c2b2-164">TFTP sunucusunda sınırlı sayıda istemci istek yuvası vardır.</span><span class="sxs-lookup"><span data-stu-id="5c2b2-164">The TFTP Server has a limited number of client request slots.</span></span> <span data-ttu-id="5c2b2-165">Bir istemci oturumu bırakılmış görünüyorsa, bu yuva yeniden kullanım için kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="5c2b2-165">If a client session appears to be dropped, that slot cannot be available for re-use.</span></span> <span data-ttu-id="5c2b2-166">Ancak NX_TFTP_SERVER_RETRANSMIT_ENABLE seçeneği etkinleştirilirse NetX Duo TFTP sunucusu, istemci oturumlarının her birinde zaman aşımını izleyen bir oturum süreölçeri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5c2b2-166">However if the NX_TFTP_SERVER_RETRANSMIT_ENABLE option is enabled, the NetX Duo TFTP Server creates an session timer that monitors the timeout on each of its client sessions.</span></span> <span data-ttu-id="5c2b2-167">Bir oturum zaman aşımı süresi dolduğunda sonlandırılır ve açık dosyalar kapanır.</span><span class="sxs-lookup"><span data-stu-id="5c2b2-167">When a session timeout expires it is terminated and any open files are closed.</span></span> <span data-ttu-id="5c2b2-168">Bu nedenle, ' yuva ' başka bir TFTP Istemci isteği için kullanılabilir hale gelir.</span><span class="sxs-lookup"><span data-stu-id="5c2b2-168">Thus the ‘slot’ becomes available for another TFTP Client request.</span></span>

<span data-ttu-id="5c2b2-169">Zaman aşımını ayarlamak için, varsayılan olarak 200 süreölçer işareti olan NX_TFTP_SERVER_RETRANSMIT_TIMEOUT yapılandırma seçeneğini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="5c2b2-169">To set the timeout, adjust the configuration option NX_TFTP_SERVER_RETRANSMIT_TIMEOUT which by default is 200 timer ticks.</span></span> <span data-ttu-id="5c2b2-170">Oturum zaman aşımlarının denetlenme aralığı, varsayılan olarak 20 süreölçer onay işareti olan NX_TFTP_SERVER_TIMEOUT_PERIOD tarafından ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="5c2b2-170">The interval between which session timeouts are checked is set by the NX_TFTP_SERVER_TIMEOUT_PERIOD which is 20 timer ticks by default.</span></span>

<span data-ttu-id="5c2b2-171">TFTP Istemcisi TFTP dosyası x medyasına karşıya yüklendiğinde, verilerin TFTP sunucusu RAM diskinden temeldeki medyaya (TFTP Istemci diski belleği) yazılabilmesi için medyanın temizlenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="5c2b2-171">When the TFTP Client has uploaded (written) files to the TFTP FileX media, the media needs to be flushed so that data can be written from the TFTP server ram disk to the underlying media (TFTP Client disk memory).</span></span> <span data-ttu-id="5c2b2-172">Bu, uygulama TFTP sunucusunu kapatmak istemiyor fx_media_flush hizmeti kullanılarak yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="5c2b2-172">This can be done using the fx_media_flush service if the application does not wish to close the TFTP Server.</span></span>

<span data-ttu-id="5c2b2-173">Ancak, TFTP sunucusunu kapattıktan sonra uygulama, FileX medyası için başka bir kullanımı yoksa fx_media_close hizmetini kullanarak medyayı kapatır.</span><span class="sxs-lookup"><span data-stu-id="5c2b2-173">However, after closing the TFTP server, the application should, if it has no further use for the FileX media, then close the media using the fx_media_close service.</span></span> <span data-ttu-id="5c2b2-174">Bu işlem, dosya verilerini TFTP Istemci diskine geri boşaltır, açık dosyaları kapatabilir ve dizin bilgilerini medyaya güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="5c2b2-174">This will flush the file data back to the TFTP Client disk, close open files, and update the directory information to the media.</span></span>

<span data-ttu-id="5c2b2-175">Bu bölümdeki "küçük örnek" bölümünde bu gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="5c2b2-175">The “Small Example” section in this chapter demonstrates this.</span></span>

<span data-ttu-id="5c2b2-176">FileX medyasını güncelleştirmeye yönelik üçüncü bir seçenek de FileX hizmetlerini açıkça kullanmak yerine FX_FAULT_TOLERANT veya FX_FAULT_TOLERANT_DATA seçenekleriyle derlemeye yöneliktir.</span><span class="sxs-lookup"><span data-stu-id="5c2b2-176">A third option for updating the FileX media is to compile the FileX library with the FX_FAULT_TOLERANT or the FX_FAULT_TOLERANT_DATA options instead of using FileX services explicitly.</span></span> <span data-ttu-id="5c2b2-177">Tanımlanmışsa, FileX otomatik olarak yazma isteklerini medya sürücüsüne geçirir.</span><span class="sxs-lookup"><span data-stu-id="5c2b2-177">If defined, FileX automatically passes write requests to the media driver.</span></span> <span data-ttu-id="5c2b2-178">Bu seçenekler, performansı sınırlayabilir ancak kayıp dosya verilerinden veya kayıp kümelerinden daha büyük koruma sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="5c2b2-178">These options may limit performance but offer greater protection from lost file data or lost clusters.</span></span> <span data-ttu-id="5c2b2-179">Genel olarak bu ve FileX hakkında daha fazla bilgi için lütfen Express Logic FileX Kullanıcı Kılavuzu 'na bakın.</span><span class="sxs-lookup"><span data-stu-id="5c2b2-179">For more information about this and FileX in general, please see the Express Logic FileX User Guide.</span></span>

## <a name="tftp-multi-thread-support"></a><span data-ttu-id="5c2b2-180">TFTP çoklu Iş parçacığı desteği</span><span class="sxs-lookup"><span data-stu-id="5c2b2-180">TFTP Multi-Thread Support</span></span>

<span data-ttu-id="5c2b2-181">NetX Duo TFTP Istemci Hizmetleri birden çok iş parçacığından aynı anda çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="5c2b2-181">The NetX Duo TFTP Client services can be called from multiple threads simultaneously.</span></span> <span data-ttu-id="5c2b2-182">Ancak, belirli bir TFTP Istemci örneğine yönelik okuma veya yazma istekleri aynı iş parçacığından sırayla yapılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5c2b2-182">However, read or write requests for a particular TFTP Client instance should be done in sequence from the same thread.</span></span>

## <a name="tftp-rfcs"></a><span data-ttu-id="5c2b2-183">TFTP RFC 'Leri</span><span class="sxs-lookup"><span data-stu-id="5c2b2-183">TFTP RFCs</span></span>

<span data-ttu-id="5c2b2-184">NetX Duo TFTP, RFC1350 ve ilgili RFC 'lerle uyumludur.</span><span class="sxs-lookup"><span data-stu-id="5c2b2-184">NetX Duo TFTP is compliant with RFC1350 and related RFCs.</span></span>

