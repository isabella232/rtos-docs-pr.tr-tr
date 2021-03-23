---
title: Bölüm 2-Azure RTOS NetX BSD yüklemesi ve kullanımı
description: Bu bölümde, Azure RTOS NetX BSD bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 7539565ccd4956c5354be45000efab8318dc606c
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826843"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-bsd"></a><span data-ttu-id="8ddc1-103">Bölüm 2-Azure RTOS NetX BSD yüklemesi ve kullanımı</span><span class="sxs-lookup"><span data-stu-id="8ddc1-103">Chapter 2 - Installation and Use of Azure RTOS NetX BSD</span></span>

<span data-ttu-id="8ddc1-104">Bu bölümde, Azure RTOS NetX BSD bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların açıklaması yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-104">This chapter contains a description of various issues related to installation, setup, and usage of the Azure RTOS NetX BSD component.</span></span>

## <a name="product-distribution"></a><span data-ttu-id="8ddc1-105">Ürün dağıtımı</span><span class="sxs-lookup"><span data-stu-id="8ddc1-105">Product Distribution</span></span>

<span data-ttu-id="8ddc1-106">Azure RTOS NetX BSD, konumundaki ortak kaynak kodu deposundan elde edilebilir [https://github.com/azure-rtos/netx/](https://github.com/azure-rtos/netx/) .</span><span class="sxs-lookup"><span data-stu-id="8ddc1-106">Azure RTOS NetX BSD can be obtained from our public source code repository at [https://github.com/azure-rtos/netx/](https://github.com/azure-rtos/netx/).</span></span> <span data-ttu-id="8ddc1-107">Paket, aşağıdaki gibi, bu belgeyi içeren iki kaynak dosya ve bir PDF dosyası içerir:</span><span class="sxs-lookup"><span data-stu-id="8ddc1-107">The package includes two source files and a PDF file that contains this document, as follows:</span></span>

- <span data-ttu-id="8ddc1-108">**nx_bsd. h**: NETX BSD için üst bilgi dosyası</span><span class="sxs-lookup"><span data-stu-id="8ddc1-108">**nx_bsd.h**: Header file for NetX BSD</span></span>
- <span data-ttu-id="8ddc1-109">**nx_bsd. c**: NETX BSD Için c kaynak dosyası</span><span class="sxs-lookup"><span data-stu-id="8ddc1-109">**nx_bsd.c**: C Source file for NetX BSD</span></span>
- <span data-ttu-id="8ddc1-110">**nx_bsd.pdf**: NETX BSD Için Kullanıcı Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="8ddc1-110">**nx_bsd.pdf**: User Guide for NetX BSD</span></span>

<span data-ttu-id="8ddc1-111">Tanıtım dosyaları:</span><span class="sxs-lookup"><span data-stu-id="8ddc1-111">Demo files:</span></span>
- <span data-ttu-id="8ddc1-112">**bsd_demo_tcp. c**</span><span class="sxs-lookup"><span data-stu-id="8ddc1-112">**bsd_demo_tcp.c**</span></span>
- <span data-ttu-id="8ddc1-113">**bsd_demo_udp. c**</span><span class="sxs-lookup"><span data-stu-id="8ddc1-113">**bsd_demo_udp.c**</span></span>

## <a name="netx-bsd-installation"></a><span data-ttu-id="8ddc1-114">NetX BSD yüklemesi</span><span class="sxs-lookup"><span data-stu-id="8ddc1-114">NetX BSD Installation</span></span>

<span data-ttu-id="8ddc1-115">NetX BSD 'yi kullanmak için, daha önce bahsedilen tüm dağıtım, NetX 'in yüklü olduğu dizine kopyalanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-115">In order to use NetX BSD the entire distribution mentioned previously should be copied to the same directory where NetX is installed.</span></span> <span data-ttu-id="8ddc1-116">Örneğin, "*\threadx\arm7\green*" dizininde NETX yüklüyse, *nx_bsd. h* ve *nx_bsd. c* dosyaları bu dizine kopyalanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-116">For example, if NetX is installed in the directory "*\threadx\arm7\green*" then the *nx_bsd.h* and *nx_bsd.c* files should be copied into this directory.</span></span>

## <a name="building-the-threadx-and-netx-components-of-a-bsd-application"></a><span data-ttu-id="8ddc1-117">Bir BSD uygulamasının ThreadX ve NetX bileşenlerini oluşturma</span><span class="sxs-lookup"><span data-stu-id="8ddc1-117">Building the ThreadX and NetX components of a BSD Application</span></span>

### <a name="threadx"></a><span data-ttu-id="8ddc1-118">ThreadX</span><span class="sxs-lookup"><span data-stu-id="8ddc1-118">ThreadX</span></span>

<span data-ttu-id="8ddc1-119">ThreadX kitaplığı, iş parçacığı yerel depolama alanında *bsd_errno* tanımlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-119">The ThreadX library must define *bsd_errno* in the thread local storage.</span></span> <span data-ttu-id="8ddc1-120">Aşağıdaki yordamı öneririz:</span><span class="sxs-lookup"><span data-stu-id="8ddc1-120">We recommend the following procedure:</span></span>

1. <span data-ttu-id="8ddc1-121">*Tx_port. h*'de TX_THREAD_EXTENSION makrolarından birini aşağıdaki şekilde ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="8ddc1-121">In *tx_port.h*, set one of the TX_THREAD_EXTENSION macros as follows:</span></span>

  ```c
  #define TX_THREAD_EXTENSION_3     int bsd_errno
  ```

2. <span data-ttu-id="8ddc1-122">ThreadX kitaplığını yeniden derleyin.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-122">Rebuild the ThreadX library.</span></span>

> [!NOTE]
> <span data-ttu-id="8ddc1-123">TX_THREAD_EXTENSION_3 zaten kullanılıyorsa, Kullanıcı diğer TX_THREAD_EXTENSION makrolarından birini kullanücretsizdir.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-123">If TX_THREAD_EXTENSION_3 is already used, the user is free to use one of the other TX_THREAD_EXTENSION macros.</span></span>

### <a name="netx"></a><span data-ttu-id="8ddc1-124">NetX</span><span class="sxs-lookup"><span data-stu-id="8ddc1-124">NetX</span></span>

<span data-ttu-id="8ddc1-125">NetX BSD hizmetlerini kullanmadan önce, NetX kitaplığı tanımlı NX_ENABLE_EXTENDED_NOTIFY_SUPPORT oluşturulmalıdır (örneğin, *nx_user. h*).</span><span class="sxs-lookup"><span data-stu-id="8ddc1-125">Before using NetX BSD Services, the NetX library must be built with NX_ENABLE_EXTENDED_NOTIFY_SUPPORT defined (e.g. in *nx_user.h*).</span></span> <span data-ttu-id="8ddc1-126">Varsayılan olarak tanımlı değildir.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-126">By default it is not defined.</span></span>

## <a name="using-netx-bsd"></a><span data-ttu-id="8ddc1-127">NetX BSD kullanma</span><span class="sxs-lookup"><span data-stu-id="8ddc1-127">Using NetX BSD</span></span>

<span data-ttu-id="8ddc1-128">NetX için BSD kullanmak kolaydır.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-128">Using BSD for NetX is easy.</span></span> <span data-ttu-id="8ddc1-129">Temel olarak, uygulama kodu sırasıyla ThreadX ve NetX kullanmak için *tx_api. h* ve *nx_api. h* dahil *nx_bsd.* h içermelidir.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-129">Basically, the application code must include *nx_bsd.h* after it includes *tx_api.h* and *nx_api.h*, in order to use ThreadX and NetX, respectively.</span></span> <span data-ttu-id="8ddc1-130">*Nx_bsd. h* dahil olduğunda, uygulama kodu daha sonra bu KıLAVUZDA belirtilen BSD hizmetlerini kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-130">Once *nx_bsd.h* is included, the application code is then able to use the BSD services specified later in this guide.</span></span> <span data-ttu-id="8ddc1-131">Uygulama, yapı işlemine *nx_bsd. c* de içermelidir.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-131">The application must also include *nx_bsd.c* in the build process.</span></span> <span data-ttu-id="8ddc1-132">Bu dosya, diğer uygulama dosyalarıyla aynı şekilde derlenmelidir ve nesne formu, uygulamanın dosyalarıyla birlikte bağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-132">This file must be compiled in the same manner as other application files and its object form must be linked along with the files of the application.</span></span> <span data-ttu-id="8ddc1-133">Bu, NetX BSD 'yi kullanmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-133">This is all that is required to use NetX BSD.</span></span>

<span data-ttu-id="8ddc1-134">NetX BSD hizmetlerini kullanmak için, uygulamanın bir IP örneği, bir paket havuzu oluşturması ve bsd_initialize çağırarak BSD hizmetlerini başlatması gerekir *.*</span><span class="sxs-lookup"><span data-stu-id="8ddc1-134">To utilize NetX BSD services, the application must create an IP instance, a packet pool, and initialize BSD services by calling *bsd_initialize.*</span></span> <span data-ttu-id="8ddc1-135">Bu kılavuzda daha sonra "küçük örnek" bölümünde gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-135">This is demonstrated in the "Small Example" section later in this guide.</span></span> <span data-ttu-id="8ddc1-136">Prototip aşağıda gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="8ddc1-136">The prototype is shown below:</span></span>

```c
INT bsd_initialize(NX_IP *default_ip, NX_PACKET_POOL *default_pool,
                  CHAR *free_memory_ptr, ULONG bsd_thread_stack_size,
                  UINT bsd_thread_priority);
```

<span data-ttu-id="8ddc1-137">Son üç parametre, TCP olaylarını denetleme ve iş parçacığı yığını alanını tanımlama gibi düzenli görevleri gerçekleştirmeye yönelik bir iş parçacığı oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-137">The last three parameters are used for creating a thread for performing periodic tasks such as checking for TCP events and define the thread stack space.</span></span>

> [!NOTE]
> <span data-ttu-id="8ddc1-138">Ağ bye sırasında çalışan BSD yuvalarının aksine NetX, konak işlemcisinin ana bilgisayar bayt düzeninde çalışır.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-138">In contrast to BSD sockets, which work in network bye order, NetX works in the host byte order of the host processor.</span></span> <span data-ttu-id="8ddc1-139">Kaynak uyumluluğu nedenleriyle, hton (), ntohs (), htonl (), ntohl () makroları tanımlanmış, ancak geçirilen bağımsız değişkeni değiştirmiyor.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-139">For source compatibility reasons, the macros htons(), ntohs(), htonl(), ntohl() have been defined, but do not modify the argument passed.</span></span>

## <a name="netx-bsd-limitations"></a><span data-ttu-id="8ddc1-140">NetX BSD sınırlamaları</span><span class="sxs-lookup"><span data-stu-id="8ddc1-140">NetX BSD Limitations</span></span>

<span data-ttu-id="8ddc1-141">NetX BSD, performans ve mimari sorunlarından dolayı tüm BSD 4,3 yuva özelliklerini desteklemez:</span><span class="sxs-lookup"><span data-stu-id="8ddc1-141">Due to performance and architecture issues, NetX BSD does not support all the BSD 4.3 socket features:</span></span>

<span data-ttu-id="8ddc1-142">*Gönderme, alma, SendTo* ve *RECVFROM* çağrılarında Int bayrakları desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-142">INT flags are not supported for *send, recv, sendto* and *recvfrom* calls.</span></span>

## <a name="netx-bsd-with-dns-support"></a><span data-ttu-id="8ddc1-143">DNS desteğiyle NetX BSD</span><span class="sxs-lookup"><span data-stu-id="8ddc1-143">NetX BSD with DNS Support</span></span>

<span data-ttu-id="8ddc1-144">NX_BSD_ENABLE_DNS tanımlanmışsa NetX BSD, ana bilgisayar adı veya ana bilgisayar IP bilgilerini almak için DNS sorguları gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-144">If NX_BSD_ENABLE_DNS is defined, NetX BSD can send DNS queries to obtain hostname or host IP information.</span></span> <span data-ttu-id="8ddc1-145">Bu özellik, *nx_dns_create* hizmeti kullanılarak bir NETX DNS istemcisinin daha önce oluşturulmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-145">This feature requires a NetX DNS Client to be previously created using the *nx_dns_create* service.</span></span> <span data-ttu-id="8ddc1-146">Bir veya daha fazla bilinen DNS sunucusu IP adresinin, sunucu adresleri eklemek için *nx_dns_server_add* kullanılarak DNS örneğine kaydedilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-146">One or more known DNS server IP addresses must be registered with the DNS instance using the *nx_dns_server_add* for adding server addresses.</span></span>

<span data-ttu-id="8ddc1-147">DNS hizmetleri ve bellek ayırma, *GetAddrInfo* ve *GetNameInfo* Hizmetleri tarafından kullanılır:</span><span class="sxs-lookup"><span data-stu-id="8ddc1-147">DNS services and memory allocation are used by *getaddrinfo* and *getnameinfo* services:</span></span>

```c
INT getaddrinfo(const CHAR *node, const CHAR *service,
              const struct addrinfo *hints, struct addrinfo **res)

INT getnameinfo(const struct sockaddr *sa, socklen_t salen,
              char *host, size_t hostlen, char *serv, size_t servlen, int flags)
```

<span data-ttu-id="8ddc1-148">BSD uygulaması, bir ana bilgisayar adı ile *GetAddrInfo* çağırdığında NETX BSD, IP adresini almak için aşağıdaki hizmetlerden herhangi birini çağırır:</span><span class="sxs-lookup"><span data-stu-id="8ddc1-148">When the BSD application calls *getaddrinfo* with a hostname, NetX BSD will call any of the below services to obtain the IP address:</span></span>

- <span data-ttu-id="8ddc1-149">nx_dns_ipv4_address_by_name_get</span><span class="sxs-lookup"><span data-stu-id="8ddc1-149">nx_dns_ipv4_address_by_name_get</span></span>
- <span data-ttu-id="8ddc1-150">nx_dns_cname_get</span><span class="sxs-lookup"><span data-stu-id="8ddc1-150">nx_dns_cname_get</span></span>

<span data-ttu-id="8ddc1-151">*Nx_dns_ipv4_address_by_name_get* için NETX BSD ipv4_addr_buffer bellek alanını kullanır.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-151">For *nx_dns_ipv4_address_by_name_get*, NetX BSD uses the ipv4_addr_buffer memory areas.</span></span> <span data-ttu-id="8ddc1-152">Bu arabelleklerin boyutu () tarafından tanımlanır `NX_BSD_IPV4_ADDR_PER_HOST * 4` .</span><span class="sxs-lookup"><span data-stu-id="8ddc1-152">The size of these buffers are defined by (`NX_BSD_IPV4_ADDR_PER_HOST * 4`).</span></span>

<span data-ttu-id="8ddc1-153">NETX BSD, *GetAddrInfo*'dan adres bilgilerini döndürmek için, bellek alanı başka bir yapılandırılabilir seçenekler kümesi tarafından tanımlanmış olan *nx_bsd_addrinfo_pool_memory* threadx blok bellek tablosunu kullanır *NX_BSD_IPV4_ADDR_MAX_NUM*.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-153">For returning address information from *getaddrinfo*, NetX BSD uses the ThreadX block memory table *nx_bsd_addrinfo_pool_memory*, whose memory area is defined by another set of configurable options, *NX_BSD_IPV4_ADDR_MAX_NUM*.</span></span>

<span data-ttu-id="8ddc1-154">Yukarıdaki yapılandırma seçenekleri hakkında daha fazla bilgi için bkz. **yapılandırma seçenekleri** .</span><span class="sxs-lookup"><span data-stu-id="8ddc1-154">See **Configuration Options** for more details on the above configuration options.</span></span>

<span data-ttu-id="8ddc1-155">Ayrıca, NX_DNS_ENABLE_EXTENDED_RR_TYPES tanımlanmışsa ve konak girişi kurallı bir addır, NetX BSD daha önce oluşturulmuş bir blok havuzundan dinamik olarak bellek ayırır *_nx_bsd_cname_block_pool*</span><span class="sxs-lookup"><span data-stu-id="8ddc1-155">Additionally, if NX_DNS_ENABLE_EXTENDED_RR_TYPES is defined, and the host input is a canonical name, NetX BSD will allocate memory dynamically from a previously created block pool *_nx_bsd_cname_block_pool*</span></span>

> [!NOTE]
> <span data-ttu-id="8ddc1-156">*GetAddrInfo* çağrıldıktan sonra, *freeaddrinfo* hizmeti kullanılarak, kaynak bağımsız değişkeni tarafından işaret edilen belleğin blok tabloya geri bırakılması için BSD uygulaması sorumludur.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-156">After calling *getaddrinfo* the BSD application is responsible for releasing the memory pointed to by the res argument back to the block table using the *freeaddrinfo* service.</span></span>

## <a name="configuration-options"></a><span data-ttu-id="8ddc1-157">Yapılandırma seçenekleri</span><span class="sxs-lookup"><span data-stu-id="8ddc1-157">Configuration Options</span></span>

<span data-ttu-id="8ddc1-158">*Nx_bsd. h* içindeki kullanıcı yapılandırılabilir seçenekleri, uygulamanın, belirli gereksinimleri Için NETX BSD yuvalarını ince ayarlamaya izin verir.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-158">User configurable options in *nx_bsd.h* allow the application to fine tune NetX BSD sockets for its particular requirements.</span></span> <span data-ttu-id="8ddc1-159">Bu parametrelerin listesi aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="8ddc1-159">The following is a list of these parameters:</span></span>

- <span data-ttu-id="8ddc1-160">**NX_BSD_TCP_WINDOW**: TCP yuvası oluşturma çağrılarında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-160">**NX_BSD_TCP_WINDOW**: Used in TCP socket create calls.</span></span> <span data-ttu-id="8ddc1-161">65535, 100Mb Ethernet için tipik bir pencere boyutudur.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-161">65535 is a typical window size for 100Mb Ethernet.</span></span> <span data-ttu-id="8ddc1-162">Varsayılan değer 65535 ' dir.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-162">The default value is 65535.</span></span>
- <span data-ttu-id="8ddc1-163">**NX_BSD_SOCKFD_START** Bu, BSD yuvası dosya tanımlayıcısı başlangıç değerinin mantıksal dizinidir.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-163">**NX_BSD_SOCKFD_START** This is the logical index for the BSD socket file descriptor start value.</span></span> <span data-ttu-id="8ddc1-164">Varsayılan olarak, bu seçenek 32 ' dir.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-164">By default this option is 32.</span></span>
- <span data-ttu-id="8ddc1-165">**NX_BSD_MAX_SOCKETS** BSD katmanında kullanılabilir olan en fazla toplam yuva sayısını belirtir ve 32 ' nin katı olmalıdır. değer, varsayılan olarak 32 ' dir.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-165">**NX_BSD_MAX_SOCKETS** Specifies the maximum number of total sockets available in the BSD layer and must be a multiple of 32.The value is defaulted to 32.</span></span>
- <span data-ttu-id="8ddc1-166">**NX_BSD_SOCKET_QUEUE_MAX** Alma yuvası sırasında depolanan en fazla UDP paketi sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-166">**NX_BSD_SOCKET_QUEUE_MAX** Specifies the maximum number of UDP packets stored on the receive socket queue.</span></span> <span data-ttu-id="8ddc1-167">Değer, varsayılan olarak 5 ' tir.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-167">The value is defaulted to 5.</span></span>
- <span data-ttu-id="8ddc1-168">**NX_BSD_MAX_LISTEN_BACKLOG** Bu, BSD TCP yuvaları için dinleme kuyruğunun (' biriktirme listesi ') boyutunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-168">**NX_BSD_MAX_LISTEN_BACKLOG** This specifies the size of the listen queue ('backlog') for BSD TCP sockets.</span></span> <span data-ttu-id="8ddc1-169">Varsayılan değer 5 ' tir.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-169">The default value is 5.</span></span>
- <span data-ttu-id="8ddc1-170">**NX_MICROSECOND_PER_CPU_TICK** Zamanlayıcı kesmesi başına mikrosaniye sayısını belirtir</span><span class="sxs-lookup"><span data-stu-id="8ddc1-170">**NX_MICROSECOND_PER_CPU_TICK** Specifies the number of microseconds per timer interrupt</span></span>
- <span data-ttu-id="8ddc1-171">**NX_BSD_TIMEOUT** BSD için gereken NetX iç çağrılarındaki süreölçer işaretleri cinsinden zaman aşımını belirtir.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-171">**NX_BSD_TIMEOUT** Specifies the timeout in timer ticks on NetX internal calls required by BSD.</span></span> <span data-ttu-id="8ddc1-172">Varsayılan değer 20 \* NX_IP_PERIODIC_RATE.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-172">The default value is 20\*NX_IP_PERIODIC_RATE.</span></span>
- <span data-ttu-id="8ddc1-173">**NX_BSD_TCP_SOCKET_DISCONNECT_TIMEOUT**: NETX bağlantı kesme çağrısının süreölçer işaretleri cinsinden zaman aşımını belirtir.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-173">**NX_BSD_TCP_SOCKET_DISCONNECT_TIMEOUT**: Specifies the timeout in timer ticks on NetX disconnect call.</span></span> <span data-ttu-id="8ddc1-174">Varsayılan değer 1’dir.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-174">The default value is 1.</span></span>
- <span data-ttu-id="8ddc1-175">**NX_BSD_PRINT_ERRORS** Ayarlanırsa, bir BSD işlevinin hata durumu dönüşü bir satır numarası ve hata türü döndürür, örneğin Hatanın gerçekleştiği NX_SOC_ERROR.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-175">**NX_BSD_PRINT_ERRORS** If set, the error status return of a BSD function returns a line number and type of error e.g. NX_SOC_ERROR where the error occurs.</span></span> <span data-ttu-id="8ddc1-176">Bu, uygulama geliştiricisinin hata ayıklama çıkışını tanımlamasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-176">This requires the application developer to define the debug output.</span></span> <span data-ttu-id="8ddc1-177">Varsayılan ayar devre dışıdır ve *nx_bsd. h* içinde herhangi bir hata ayıklama çıkışı belirtilmez</span><span class="sxs-lookup"><span data-stu-id="8ddc1-177">The default setting is disabled and no debug output is specified in *nx_bsd.h*</span></span>
- <span data-ttu-id="8ddc1-178">**NX_BSD_TIMER_RATE** BSD düzenli zamanlayıcı görevinin çalışma aralığı.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-178">**NX_BSD_TIMER_RATE** Interval after which BSD periodic timer task runs.</span></span> <span data-ttu-id="8ddc1-179">Varsayılan değer 1 saniyedir (1 \* NX_IP_PERIODIC_RATE).</span><span class="sxs-lookup"><span data-stu-id="8ddc1-179">The default value is 1 second (1 \* NX_IP_PERIODIC_RATE).</span></span>
- <span data-ttu-id="8ddc1-180">**NX_BSD_TIMEOUT_PROCESS_IN_TIMER** Ayarlanırsa, bu seçenek BSD zaman aşımı işleminin sistem Zamanlayıcı bağlamında yürütülmesine izin verir.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-180">**NX_BSD_TIMEOUT_PROCESS_IN_TIMER** If set, this option allows the BSD timeout process to execute in the system timer context.</span></span> <span data-ttu-id="8ddc1-181">Varsayılan davranış devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-181">The default behavior is disabled.</span></span> <span data-ttu-id="8ddc1-182">Bu özellik, Bölüm 2 "NetX BSD yüklemesi ve kullanımı" bölümünde daha ayrıntılı olarak açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-182">This feature is described in more detail in Chapter 2 "Installation and Use of NetX BSD".</span></span>
- <span data-ttu-id="8ddc1-183">**NX_BSD_ENABLE_DNS** Etkinleştirilirse NetX BSD, ana bilgisayar adı veya konak IP adresi için bir DNS sorgusu gönderir.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-183">**NX_BSD_ENABLE_DNS** If enabled, NetX BSD will send a DNS query for a hostname or host IP address.</span></span> <span data-ttu-id="8ddc1-184">Daha önce oluşturulup başlatılmış bir DNS Istemci örneği gerektirir.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-184">Requires a DNS Client instance to be previously created and started.</span></span> <span data-ttu-id="8ddc1-185">Varsayılan olarak etkin değildir.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-185">By default it is not enabled.</span></span>
- <span data-ttu-id="8ddc1-186">**NX_BSD_IPV4_ADDR_MAX_NUM** *GetAddrInfo* tarafından döndürülen en fazla IPv4 adresi sayısı.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-186">**NX_BSD_IPV4_ADDR_MAX_NUM** Maximum number of IPv4 addresses returned by *getaddrinfo*.</span></span> <span data-ttu-id="8ddc1-187">NX_BSD_IPV4_ADDR_MAX_NUM ile birlikte, bu, *GetAddrInfo* içinde bilgi depolamaya yönelik olarak bellek ayırmak Için NETX BSD bloğu havuzunun boyutunu nx_bsd_addrinfo_block_pool tanımlar.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-187">This along with NX_BSD_IPV4_ADDR_MAX_NUM defines the size of the NetX BSD block pool nx_bsd_addrinfo_block_pool for dynamically allocating memory to address information storage in *getaddrinfo*.</span></span> <span data-ttu-id="8ddc1-188">Varsayılan değer 5 ' tir.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-188">The default value is 5.</span></span>
- <span data-ttu-id="8ddc1-189">**NX_BSD_IPV4_ADDR_PER_HOST**: DNS sorgusu başına depolanan en yüksek IPv4 adreslerini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-189">**NX_BSD_IPV4_ADDR_PER_HOST**: Defines maximum IPv4 addresses stored per DNS query.</span></span> <span data-ttu-id="8ddc1-190">Varsayılan değer 5 ' tir.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-190">The default value is 5.</span></span>

## <a name="bsd-socket-options"></a><span data-ttu-id="8ddc1-191">BSD yuvası seçenekleri</span><span class="sxs-lookup"><span data-stu-id="8ddc1-191">BSD Socket Options</span></span>

<span data-ttu-id="8ddc1-192">Aşağıdaki NetX BSD yuva seçeneklerinin listesi, *setsockopt* hizmeti kullanılarak her yuva temelinde çalışma zamanında etkinleştirilebilir (veya devre dışı).</span><span class="sxs-lookup"><span data-stu-id="8ddc1-192">The following list of NetX BSD socket options can be enabled (or disabled) at run time on a per socket basis using the *setsockopt* service:</span></span>

```c
INT setsockopt(INT sockID, INT option_level, INT option_name, const
                void *option_value, INT option_length);
```

<span data-ttu-id="8ddc1-193">*Option_level* için iki farklı ayar vardır.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-193">There are two different settings for *option_level*.</span></span>

<span data-ttu-id="8ddc1-194">Çalışma zamanı yuva seçeneklerinin ilk türü yuva düzeyi seçenekleri için SOL_SOCKET.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-194">The first type of run time socket options is SOL_SOCKET for socket level options.</span></span> <span data-ttu-id="8ddc1-195">Yuva düzeyi seçeneğini etkinleştirmek için, SOL_SOCKET olarak ayarlanan option_level ve option_name belirli bir seçeneğe ayarla ' *yı çağırın.* örneğin, so_broadcast.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-195">To enable a socket level option, call *setsockopt* with option_level set to SOL_SOCKET and option_name set to the specific option e.g. SO_BROADCAST.</span></span> <span data-ttu-id="8ddc1-196">Bir seçenek ayarı almak için, option_level tekrar SOL_SOCKET olarak ayarlanan option_name için *getsockopt* çağırın.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-196">To retrieve an option setting, call *getsockopt* for the option_name with option_level again set to SOL_SOCKET.</span></span>

<span data-ttu-id="8ddc1-197">Çalışma zamanı yuva düzeyi seçeneklerinin listesi aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-197">The list of run time socket level options is shown below.</span></span>

- <span data-ttu-id="8ddc1-198">**So_broadcast**: ayarlandıysa, NETX yuvalarından yayın paketlerinin gönderilmesini ve alınmasına izin vermez.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-198">**SO_BROADCAST**: If set, this enables sending and receiving broadcast packets from Netx sockets.</span></span> <span data-ttu-id="8ddc1-199">Bu, NetX için varsayılan davranıştır.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-199">This is the default behavior for NetX.</span></span> <span data-ttu-id="8ddc1-200">Tüm yuvalarda bu yetenek vardır.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-200">All sockets have this capability.</span></span>
- <span data-ttu-id="8ddc1-201">**SO_ERROR**: *getsockopt* hizmeti kullanılarak belirtilen yuvanın önceki yuva işleminde yuva durumunu elde etmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-201">**SO_ERROR**: Used to obtain socket status on the previous socket operation of the specified socket, using the *getsockopt* service.</span></span> <span data-ttu-id="8ddc1-202">Tüm yuvalarda bu yetenek vardır.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-202">All sockets have this capability.</span></span>
- <span data-ttu-id="8ddc1-203">**SO_KEEPALIVE**: AYARLANıRSA, TCP canlı tut özelliğini sunar.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-203">**SO_KEEPALIVE**: If set, this enables the TCP Keep Alive feature.</span></span> <span data-ttu-id="8ddc1-204">Bu, NetX kitaplığının *nx_user. h* içinde tanımlanan NX_TCP_ENABLE_KEEPALIVE oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-204">This requires the NetX library to be built with NX_TCP_ENABLE_KEEPALIVE defined in *nx_user.h*.</span></span> <span data-ttu-id="8ddc1-205">Bu özellik varsayılan olarak devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-205">By default this feature is disabled.</span></span>
- <span data-ttu-id="8ddc1-206">**SO_RCVTIMEO**: Bu, NETX BSD yuvalarda paketlerin alınması için saniye cinsinden bekleme seçeneğini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-206">**SO_RCVTIMEO**: This sets the wait option in seconds for receiving packets on NetX BSD sockets.</span></span> <span data-ttu-id="8ddc1-207">Varsayılan değer NX_WAIT_FOREVER (0xFFFFFFFF) veya engelleyici olmayan bir etkin ise, NX_NO_WAIT (0x0).</span><span class="sxs-lookup"><span data-stu-id="8ddc1-207">The default value is the NX_WAIT_FOREVER (0xFFFFFFFF) or, if non-blocking is enabled, NX_NO_WAIT (0x0).</span></span>
- <span data-ttu-id="8ddc1-208">**SO_RCVBUF**: Bu, TCP yuvasının pencere boyutunu ayarlar.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-208">**SO_RCVBUF**: This sets the window size of the TCP socket.</span></span> <span data-ttu-id="8ddc1-209">NX_BSD_TCP_WINDOW varsayılan değeri, BSD TCP yuvaları için 64K olarak ayarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-209">The default value, NX_BSD_TCP_WINDOW, is set to 64k for BSD TCP sockets.</span></span> <span data-ttu-id="8ddc1-210">65535 üzerinden boyutu ayarlamak için NetX kitaplığının NX_TCP_ENABLE_WINDOW_SCALING tanımlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-210">To set the size over 65535 requires the NetX library to be built with the NX_TCP_ENABLE_WINDOW_SCALING be defined.</span></span>
- <span data-ttu-id="8ddc1-211">**SO_REUSEADDR**: ayarlandıysa, bu, birden çok yuvaların bir bağlantı noktasıyla eşleştirilmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-211">**SO_REUSEADDR**: If set, this enables multiple sockets to be mapped to one port.</span></span> <span data-ttu-id="8ddc1-212">Genel kullanım, TCP sunucu soketi içindir.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-212">The typical usage is for the TCP Server socket.</span></span> <span data-ttu-id="8ddc1-213">Bu, NetX yuvalarının varsayılan davranışıdır.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-213">This is the default behavior of NetX sockets.</span></span>

<span data-ttu-id="8ddc1-214">Çalışma zamanı yuva seçeneklerinin ikinci türü, IP seçenek düzeyidir.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-214">The second type of run time socket options is the IP option level.</span></span> <span data-ttu-id="8ddc1-215">Bir IP düzeyi seçeneğini etkinleştirmek için, *setsockopt* ' i çağırın option_level IP_PROTO olarak ayarlayın ve option_name IP_MULTICAST_TTL seçeneğine ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-215">To enable an IP level option, call *setsockopt* with option_level set to IP_PROTO and option_name set to the option e.g. IP_MULTICAST_TTL.</span></span> <span data-ttu-id="8ddc1-216">Bir seçenek ayarı almak için, option_level tekrar IP_PROTO olarak ayarlanan option_name için *getsockopt* çağırın.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-216">To retrieve an option setting, call *getsockopt* for the option_name with option_level again set to IP_PROTO.</span></span>

<span data-ttu-id="8ddc1-217">Çalışma zamanı IP düzeyi seçeneklerinin listesi aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-217">The list of run time IP level options is shown below.</span></span>

- <span data-ttu-id="8ddc1-218">**IP_MULTICAST_TTL**: Bu, UDP yuvaları için yaşam süresini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-218">**IP_MULTICAST_TTL**: This sets the time to live for UDP sockets.</span></span> <span data-ttu-id="8ddc1-219">Yuva oluşturulduğunda varsayılan değer NX_IP_TIME_TO_LIVE (0x80).</span><span class="sxs-lookup"><span data-stu-id="8ddc1-219">The default value is NX_IP_TIME_TO_LIVE (0x80) when the socket is created.</span></span> <span data-ttu-id="8ddc1-220">Bu değer, bu yuva seçeneği ile *setsockopt* çağırarak geçersiz kılınabilir.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-220">This value can be overridden by calling *setsockopt* with this socket option.</span></span>
- <span data-ttu-id="8ddc1-221">**IP_ADD_MEMBERSHIP**: ayarlanırsa, belirtilen IGMP grubuna katılması için bu seçenekler BSD yuvasını (yalnızca UDP yuvaları için geçerlidir) sağlar.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-221">**IP_ADD_MEMBERSHIP**: If set, this options enables the BSD socket (applies only to UDP sockets) to join the specified IGMP group.</span></span>
- <span data-ttu-id="8ddc1-222">**IP_DROP_MEMBERSHIP**: ayarlanırsa, bu seçenekler belirtilen IGMP grubunu BıRAKMAK için BSD yuvasını (yalnızca UDP yuvaları için geçerlidir) sağlar.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-222">**IP_DROP_MEMBERSHIP**: If set, this options enables the BSD socket (applies only to UDP sockets) to leave the specified IGMP group.</span></span>

## <a name="small-example-system"></a><span data-ttu-id="8ddc1-223">Küçük örnek sistem</span><span class="sxs-lookup"><span data-stu-id="8ddc1-223">Small Example System</span></span>

<span data-ttu-id="8ddc1-224">NetX BSD kullanmanın bir örneği aşağıda şekil 1,0 ' de gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-224">An example of how to use NetX BSD is shown in Figure 1.0 below.</span></span> <span data-ttu-id="8ddc1-225">Bu örnekte, içerme dosyası *nx_bsd. h* , 7. satırda getirilir.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-225">In this example, the include file *nx_bsd.h* is brought in at line 7.</span></span> <span data-ttu-id="8ddc1-226">Ardından, IP örneği *bsd_ip* ve paket havuzu *bsd_pool* , 20 ve 21. satırda genel değişkenler olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-226">Next, the IP instance *bsd_ip* and packet pool *bsd_pool* are created as global variables at line 20 and 21.</span></span> <span data-ttu-id="8ddc1-227">Bu tanıtımın bir RAM (sanal) ağ sürücüsü (satır 41) kullandığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-227">Note that this demo uses a ram (virtual) network driver (line 41).</span></span> <span data-ttu-id="8ddc1-228">İstemci ve sunucu, bu örnekteki tek IP örneğinde aynı IP adresini paylaşır.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-228">The client and server will share the same IP address on single IP instance in this example.</span></span>

<span data-ttu-id="8ddc1-229">İstemci ve sunucu iş parçacıkları, uygulamayı ayarlayan ve satırlar 293-361 ' de tanımlanan *tx_application_define* için 303 ve 309. satırda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-229">The client and server threads are created on line 303 and 309 in *tx_application_define* which sets up the application and is defined on lines 293-361.</span></span> <span data-ttu-id="8ddc1-230">Satır 327 ' de IP örneği başarıyla oluşturulduktan sonra, IP örneği 350. satırdaki TCP hizmetleri için etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-230">After IP instance successful creation on line 327, the IP instance is enabled for TCP services on line 350.</span></span> <span data-ttu-id="8ddc1-231">BSD Hizmetleri 'nin kullanılabilmesi için son gereksinim, BSD için gereken tüm veri yapılarını ve NetX ve ThreadX kaynaklarını ayarlamak üzere 360 satırındaki *bsd_initialize* çağırmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-231">The last requirement before BSD services can be used is to call *bsd_initialize* on line 360 to set up all data structures and NetX, and ThreadX resources needed by BSD.</span></span>

<span data-ttu-id="8ddc1-232">Sunucu iş parçacığı girişi işlevinde, 381-397 satırlarında tanımlanan *thread_1_entry* , uygulama sürücünün ağ parametreleriyle NETX başlatmasını bekler.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-232">In the server thread entry function, *thread_1_entry,* which is defined on lines 381-397, the application waits for the driver to initialize NetX with network parameters.</span></span> <span data-ttu-id="8ddc1-233">Bu işlem tamamlandıktan sonra, TCP sunucu yuvasını ayarlama ayrıntılarını işlemek için 146-253 satırlarında tanımlanan *Tcpserver* 'ı çağırır.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-233">Once this is done, it calls *tcpServer,* defined on lines 146-253, to handle the details of setting up the TCP server socket.</span></span>

<span data-ttu-id="8ddc1-234">*Tcpserver* , 159. satırda *yuva* hizmetini çağırarak ana yuvayı oluşturur ve 176. satırdaki *bağlama* çağrısını kullanarak dinleme yuvasına bağlar.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-234">*tcpServer* creates the master socket by calling the *socket* service on line 159 and binds it to the listening socket using the *bind* call on line 176.</span></span> <span data-ttu-id="8ddc1-235">Daha sonra 191 satırındaki bağlantı isteklerini dinlemek üzere yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-235">It is then configured for listening for connection requests on line 191.</span></span> <span data-ttu-id="8ddc1-236">Ana yuvanın bir bağlantı isteğini kabul etmediğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-236">Note that the master socket does not accept a connection request.</span></span> <span data-ttu-id="8ddc1-237">Bağlantı isteklerini algılamak için her seferinde *seçimi* çağıran bir sürekli döngüde çalışır.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-237">It runs in a continuous loop which calls *select* each time to detect connection requests.</span></span> <span data-ttu-id="8ddc1-238">BSD yuvaları dizisinden seçilen bir ikincil BSD yuvasına, 218 satırı üzerinde *Accept* hizmeti çağrıldıktan sonra bağlantı isteği atanır.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-238">A secondary BSD socket chosen from an array of BSD sockets is assigned the connection request after calling the *accept* service on line 218.</span></span>

<span data-ttu-id="8ddc1-239">Istemci tarafında, 366-377 satırlarında tanımlanan *thread_0_entry* istemci iş parçacığı girişi işlevi, ayrıca NETX 'in sürücü tarafından başlatılmasını bekler.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-239">On the Client side, the client thread entry function, *thread_0_entry*, defined on lines 366-377, should also wait for NetX to be initialized by the driver.</span></span> <span data-ttu-id="8ddc1-240">Burada sunucu tarafının bunu yapması Bekleniyorduk.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-240">Here we just wait for the server side to do so.</span></span> <span data-ttu-id="8ddc1-241">Daha sonra, TCP istemci yuvasını ayarlama ve bir TCP bağlantısı isteme ayrıntılarını işlemek için, satır 54-142 ' de tanımlanan *TcpClient* öğesini çağırır.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-241">It then calls *tcpClient* defined on line 54-142, to handle the details of setting up the TCP client socket and requesting a TCP connection.</span></span>

<span data-ttu-id="8ddc1-242">TCP istemci yuvası 68. satırda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-242">The TCP client socket is created on line 68.</span></span> <span data-ttu-id="8ddc1-243">Yuva belirtilen IP adresine bağlıdır ve 84. satırdaki *Connect* 'ı çağırarak TCP sunucusuna bağlanmaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-243">The socket is bound to the specified IP address and attempts to connect to the TCP server by calling *connect* on line 84.</span></span> <span data-ttu-id="8ddc1-244">Artık paket göndermeye ve almaya başlamaya hazırdır.</span><span class="sxs-lookup"><span data-stu-id="8ddc1-244">It is now ready to begin sending and receiving packets.</span></span>

```c
1 /*  This is a small demo of BSD Wrapper for the high-performance NetX TCP/IP stack.
2     This demo demonstrate TCP connection, disconnection, sending, and receiving using
3     ARP and a simulated Ethernet driver. */
4
5 #include     "tx_api.h"
6 #include     "nx_api.h"
7 #include     "nx_bsd.h"
8 #include     <string.h>
9 #include     <stdlib.h>
10
11 #define         DEMO_STACK_SIZE         (16*1024)
12
13
14 /* Define the ThreadX and NetX object control blocks... */
15
16 TX_THREAD       thread_0;
17 TX_THREAD       thread_1;
18
19
20 NX_PACKET_POOL  bsd_pool;
21 NX_IP           bsd_ip;
22
23
24 /* Define the counters used in the demo application... */
25
26 ULONG           error_counter;
27
28 /* Define fd_set for select call */
29 fd_set          master_list,read_ready,read_ready1;
30
31
32 /* Define thread prototypes. */
33
34 VOID            thread_0_entry(ULONG thread_input);
35 VOID            thread_1_entry(ULONG thread_input);
36
37 VOID            tcpClient(CHAR *msg0);
38 VOID            tcpServer(VOID);
39 INT             HandleClient(INT sock);
40
41 VOID            _nx_ram_network_driver(struct NX_IP_DRIVER_STRUCT *driver_req);
42
43
44 /* Define main entry point. */
45
46 int main()
47 {
48
49     /* Enter the ThreadX kernel. */
50     tx_kernel_enter();
51 }
52
53
54 VOID tcpClient(CHAR *msg0)
55 {
56
57 INT     status,status1,send_counter;
58 INT     sock_tcp_1,length,length1;
59 struct  sockaddr_in echoServAddr;       /* Echo server address */
60 struct  sockaddr_in localAddr;          /* Local address */
61 struct  sockaddr_in remoteAddr;         /* Remote address */
62
63 UINT    echoServPort; /* Echo Server Port */
64 CHAR    rcvBuffer1[32]
65
66
67     /* Create BSD TCP Socket */
68     sock_tcp_1 = **socket**( PF_INET, SOCK_STREAM, IPPROTO_TCP);
69     if (sock_tcp_1 == -1)
70     {
71         printf("\nError: BSD TCP Client socket create \n");
72         return;
73     }
74
75     printf("\nBSD TCP Client socket created %lu \n", sock_tcp_1);
76     /* Fill destination port and IP address */
77     echoServPort = 12;
78     memset(&echoServAddr, 0, sizeof(echoServAddr));
79     echoServAddr.sin_family = PF_INET;
80     echoServAddr.sin_addr.s_addr = htonl(0x01020304);
81     echoServAddr.sin_port = echoServPort;
82
83     /* Now connect this client the server */
84     status1 = connect(sock_tcp_1, (struct sockaddr *)&echoServAddr, sizeof(echoServAddr));
85     /* Check for error. */
86     if (status1 != OK)
87     {
88         printf("\nError: BSD TCP Client socket Connect, %d \n",sock_tcp_1);
89         status = soc_close(sock_tcp_1);
90         if (status != ERROR)
91             printf("\nConnect ERROR so BSD Client Socket Closed: %d\n",sock_tcp_1);
92         else
93             printf("\nError: BSD Client Socket close %d\n",sock_tcp_1);
94         return;
95     }
96     /* Get and print source and destination information */
97     printf("\nBSD TCP Client socket: %d connected \n", sock_tcp_1);
98
99     status = getsockname(sock_tcp_1, (struct sockaddr *)&localAddr, &length);
100    printf("Client port = %lu , Client = %lu,", 
            localAddr.sin_port, localAddr.sin_addr.s_addr);
101    status = getpeername( sock_tcp_1, (struct sockaddr *) &remoteAddr, &length1);
102    printf("Remote port = %lu, Remote IP = %lu \n", 
            remoteAddr.sin_port remoteAddr.sin_addr.s_addr);
103
104    send_counter = 1;
105
106    /* Now receive the echoed packet from the server */
107    while(1)
108    {
109        tx_thread_sleep(2);
110
111        printf("\nClient sock: %d Sending packet No: %d to
                server\n",sock_tcp_1,send_counter);
112        status = send(sock_tcp_1,msg0, sizeof(msg0), 0);
113        if (status == ERROR)
114            printf("Error: BSD Client Socket send %d\n",sock_tcp_1);
115        else
116        {
117            printf("\nMessage sent: %s\n",msg0);
118            send_counter++;
119        }
120
121        status = recv(sock_tcp_1, (VOID *)rcvBuffer1, 31,0);
122        if (status == 0)
123            break;
124
125        rcvBuffer1[status] = 0;
126
127        if (status != ERROR)
128            printf("\nBSD Client Socket: %d received %lu bytes: %s ", 
                        sock_tcp_1,(ULONG)status,rcvBuffer1);
129        else
130            printf("\nError: BSD Client Socket receive %d \n",sock_tcp_1);
131
132    }
133
134    /* close this client socket */
135    status = soc_close(sock_tcp_1);
136    if (status != ERROR)
137        printf("\nBSD Client Socket Closed %d\n",sock_tcp_1);
138    else
139        printf("\nError: BSD Client Socket close %d \n",sock_tcp_1);
140
141    /* End */
142 }
143
144
145
146 void tcpServer(void)
147 {
148
149 INT         status,status1,sock,sock_tcp_2,i;
150 struct      sockaddr_in echoServAddr; /* Echo server address */
151 struct      sockaddr_in ClientAddr;
152
153 INT         Clientlen;
154 UINT        echoServPort; /* Echo Server Port */
155
156 INT         maxfd;
157
158 /* Create BSD TCP Server Socket */
159     sock_tcp_2 = socket( PF_INET, SOCK_STREAM, IPPROTO_TCP);
160     if (sock_tcp_2 == -1)
161     {
162         printf("Error: BSD TCP Server socket create\n");
163         return;
164     }
165     else
166         printf("BSD TCP Server socket created \n");
167
168     /* Now fill server side information */
169     echoServPort = 12;
170     memset(&echoServAddr, 0, sizeof(echoServAddr));
171     echoServAddr.sin_family = PF_INET;
172     echoServAddr.sin_addr.s_addr = htonl(0x01020304);
173     echoServAddr.sin_port = echoServPort;
174
175     /* Bind this server socket */
176         status = bind(sock_tcp_2, (struct sockaddr *) &echoServAddr, sizeof(echoServAddr));
177     if (status < 0)
178     {
179         printf("Error: BSD TCP Server Socket Bind \n");
180         return;
181     }
182     else
183         printf("BSD TCP Server Socket bound \n");
184
185     FD_ZERO(&master_list);
186     FD_ZERO(&read_ready);
187     FD_SET(sock_tcp_2,&master_list);
188     maxfd = sock_tcp_2;
189
190     /* Now listen for any client connections for this server socket */
191     status = listen(sock_tcp_2,5);
192     if (status < 0)
193     {
194         printf("Error: BSD TCP Server Socket Listen\n");
195         return;
196     }
197     else
198         printf("BSD TCP Server Socket Listen complete, ");
199
200     /* All set to accept client connections */
201     printf("Now accepting client connections\n");
202
203     /* Loop to create and establish server connections. */
204     while(1)
205     {
206
207         read_ready = master_list;
208         tx_thread_sleep(2); /* Allow some time to other threads too */
209         status = select(maxfd+1,&read_ready,0,0,0);
210         if (status == ERROR)
211         {
212             continue;
213         }
214
215         status = FD_ISSET(sock_tcp_2,&read_ready);
216         if(status)
217         {
218             sock = accept(sock_tcp_2,(struct sockaddr*)&ClientAddr, &Clientlen);
219
220             /* Add this new connection to our master list */
221             FD_SET(sock,&master_list);
222             if ( sock \maxfd)
223             {
224                 maxfd = sock;
225             }
226
227             continue;
228         }
229         for (i = 0; i < (maxfd+1); i++)
230         {
231             if (( i != sock_tcp_2) && (FD_ISSET(i,&master_list)) && 
                    (FD_ISSET(i,&read_ready)))
232             {
233                 status1 = HandleClient(i);
234                 if (status1 == 0)
235                 {
236                     status1 = soc_close(i);
237                     if (status1 == OK)
238                     {
239                         FD_CLR(i,&master_list);
240                         printf("\nBSD Server Socket:%d closed\n",i);
241                     }
242                     else
243                         printf("\nError:BSD Server Socket:%d close\n",i);
244                 }
245
246             }
247         }
248
249         /* Loop back to check any next client connection */
250
251     } /* While(1) ends */
252
253 }
254
255 CHAR     rcvBuffer[128];
256
257 INT     HandleClient(INT sock)
258 {
259
260 INT     status;
261
262
263     status = recv(sock, (VOID *)rcvBuffer, 128,0);
264     if (status == ERROR )
265     {
266         printf("\n BSD Server Socket:%d receive \n",sock);
267         return(ERROR);
268     }
269
270     /* a zero return from a recv() call indicates client is terminated! */
271     if (status == 0)
272     {
273         /* Done with this client , close this secondary server socket */
274         return(status);
275     }
276
277     /* print data received from the client */
278     printf("\nBSD Server Socket:%d received %lu bytes: %s \n", sock, (ULONG)status,rcvBuffer);
279
280     /* And echo the same data to the client */
281     status = send(sock,rcvBuffer, status + 1, 0);
282     if (status == ERROR )
283     {
284         printf("\nError: BSD Server Socket:%d send \n",sock);
285         return(ERROR);
286     }
287     return(status);
288 }
289
290
291 /* Define what the initial system looks like. */
292
293 void     tx_application_define(void *first_unused_memory)
294 {
295
296 CHAR     *pointer;
297 UINT     status;
298
299     /* Setup the working pointer. */
300     pointer = (CHAR *) first_unused_memory;
301
302     /* Create a client thread. */
303     tx_thread_create(&thread_0, "Client1", thread_0_entry, 0,
304         pointer, DEMO_STACK_SIZE, 2, 2, TX_NO_TIME_SLICE, TX_AUTO_START);
305
306     pointer = pointer + DEMO_STACK_SIZE;
307
308     /* Create a server thread. */
309     tx_thread_create(&thread_1, "Server", thread_1_entry, 0,
310         pointer, DEMO_STACK_SIZE,1,1, TX_NO_TIME_SLICE, TX_AUTO_START);
311
312     pointer = pointer + DEMO_STACK_SIZE;
313
314     /* Initialize the NetX system. */
315     nx_system_initialize();
316
317     /* Create a BSD packet pool. */
318     status = nx_packet_pool_create(&bsd_pool,"NetX BSD Packet Pool", 128
                                        pointer, 16384);
319     pointer = pointer + 16384;
320     if (status)
321     {
322         error_counter++;
323         printf("Error in creating BSD packet pool\n!");
324     }
325
326     /* Create an IP instance for BSD. */
327     status = nx_ip_create(&bsd_ip, "NetX IP Instance 2", IP_ADDRESS(1, 2, 3, 4),
                              0xFFFFFF00UL, &bsd_pool, _nx_ram_network_driver,
                              pointer, 2048, 1);
328
329     pointer = pointer + 2048;
330
331     if (status)
332     {
333         error_counter++;
334         printf("Error creating BSD IP instance\n!");
335     }
336
337     /* Enable ARP and supply ARP cache memory for BSD IP Instance */
338     status = nx_arp_enable(&bsd_ip, (void *) pointer, 1024);
339     pointer = pointer + 1024;
340
341     /* Check ARP enable status. */
342     if (status)
343     {
344         error_counter++;
345         printf("Error in Enable ARP and supply ARP cache memory to BSD IP instance\n");
346     }
347
348     /* Enable TCP processing for BSD IP instances. */
349
350     status = nx_tcp_enable(&bsd_ip);
351
352     /* Check TCP enable status. */
353     if (status)
354     {
355         error_counter++;
356         printf("Error in Enable TCP \n");
357     }
358
359     /* Now initialize BSD Scoket Wrapper */
360     status = bsd_initialize(&bsd_ip, &bsd_pool,pointer, 2048, 1);
361 }
362
363
364 /* Define the test threads. */
365
366 void     thread_0_entry)ULONG thread_input)
367 {
368
369 CHAR     *msg0 = "Client 1:
                     "ABCDEFGHIJKLMNOPQRSTUVWXYZ<>ABCDEFGHIJKLMNOPQRSTUVWXYZ<> \
                     "ABCDEFGHIJKLMNOPQRSTUVWXYZ<>END";
370
371     /* Wait till Server side is all set */
372     tx_thread_sleep(2);
373     while (1)
374     {
375         tcpClient(msg0);
376         tx_thread_sleep(1);
377     }
378 }
379
380 /* Define the server thread entry function. */
381 void     thread_1_entry(ULONG thread_input)
382 {
383
384 UINT     status;
385 ULONG    actual_status;
386
387 /* Ensure the IP instance has been initialized. */
388 status = nx_ip_status_check(&bsd_ip, NX_IP_INITIALIZE_DONE, &actual_status, 100);
389
390 /* Check status... */
391 if (status != NX_SUCCESS)
392 {
393     error_counter++;
394     return;
395 }
396 /* Start a TCP Server */
397 tcpServer();
398 }
399
```
