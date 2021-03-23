---
title: Bölüm 2-Azure RTOS NetX Noktadan Noktaya Protokolü (PPP) yükleme ve kullanımı
description: Bu bölümde, Azure RTOS NetX Noktadan Noktaya Protokolü (PPP) bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 40f09da31f5541208c3b2cc0eeb54850b3d71f7c
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826656"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-point-to-point-protocol-ppp"></a><span data-ttu-id="ca139-103">Bölüm 2-Azure RTOS NetX Noktadan Noktaya Protokolü (PPP) yükleme ve kullanımı</span><span class="sxs-lookup"><span data-stu-id="ca139-103">Chapter 2 - Installation and use of Azure RTOS NetX Point-to-Point Protocol (PPP)</span></span>

<span data-ttu-id="ca139-104">Bu bölümde, Azure RTOS NetX Noktadan Noktaya Protokolü (PPP) bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların açıklaması yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="ca139-104">This chapter contains a description of various issues related to installation, setup, and usage of the Azure RTOS NetX Point-to-Point Protocol (PPP) component.</span></span>

## <a name="product-distribution"></a><span data-ttu-id="ca139-105">Ürün dağıtımı</span><span class="sxs-lookup"><span data-stu-id="ca139-105">Product Distribution</span></span>

<span data-ttu-id="ca139-106">Azure RTOS NetX Noktadan Noktaya Protokolü (PPP) paketi adresinde bulunabilir <https://github.com/azure-rtos/netx> .</span><span class="sxs-lookup"><span data-stu-id="ca139-106">The Azure RTOS NetX Point-to-Point Protocol (PPP) package is available at <https://github.com/azure-rtos/netx>.</span></span> <span data-ttu-id="ca139-107">Paket aşağıdaki dosyaları içerir:</span><span class="sxs-lookup"><span data-stu-id="ca139-107">The package includes the following files:</span></span>

- <span data-ttu-id="ca139-108">**nx_ppp. h**: NETX için PPP için üst bilgi dosyası</span><span class="sxs-lookup"><span data-stu-id="ca139-108">**nx_ppp.h**: Header file for PPP for NetX</span></span>
- <span data-ttu-id="ca139-109">**nx_ppp. c**: NETX için PPP Için c kaynak dosyası</span><span class="sxs-lookup"><span data-stu-id="ca139-109">**nx_ppp.c**: C Source file for PPP for NetX</span></span>
- <span data-ttu-id="ca139-110">**nx_ppp.pdf**: NETX için PPP açıklaması</span><span class="sxs-lookup"><span data-stu-id="ca139-110">**nx_ppp.pdf**: PDF description of PPP for NetX</span></span>
- <span data-ttu-id="ca139-111">**demo_netx_ppp. c**: NETX PPP tanıtımı</span><span class="sxs-lookup"><span data-stu-id="ca139-111">**demo_netx_ppp.c**: NetX PPP demonstration</span></span>

## <a name="ppp-installation"></a><span data-ttu-id="ca139-112">PPP yüklemesi</span><span class="sxs-lookup"><span data-stu-id="ca139-112">PPP Installation</span></span>

<span data-ttu-id="ca139-113">NetX için PPP kullanmak istiyorsanız, daha önce bahsedilen dağıtımın tamamı NetX ' in yüklü olduğu dizine kopyalanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ca139-113">In order to use PPP for NetX, the entire distribution mentioned previously should be copied to the same directory where NetX is installed.</span></span> <span data-ttu-id="ca139-114">Örneğin, "*\threadx\arm7\green*" dizininde NETX yüklüyse, *nx_ppp. h* ve *nx_ppp. c* dosyaları bu dizine kopyalanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ca139-114">For example, if NetX is installed in the directory “*\threadx\arm7\green*” then the *nx_ppp.h* and *nx_ppp.c* files should be copied into this directory.</span></span>

## <a name="using-ppp"></a><span data-ttu-id="ca139-115">PPP kullanma</span><span class="sxs-lookup"><span data-stu-id="ca139-115">Using PPP</span></span>

<span data-ttu-id="ca139-116">NetX için PPP kullanmak kolaydır.</span><span class="sxs-lookup"><span data-stu-id="ca139-116">Using PPP for NetX is easy.</span></span> <span data-ttu-id="ca139-117">Temel olarak, uygulama kodu sırasıyla ThreadX ve NetX kullanmak için *tx_api. h* ve *nx_api. h* dahil *nx_ppp.* h içermelidir.</span><span class="sxs-lookup"><span data-stu-id="ca139-117">Basically, the application code must include *nx_ppp.h* after it includes *tx_api.h* and *nx_api.h*, in order to use ThreadX and NetX, respectively.</span></span> <span data-ttu-id="ca139-118">*Nx_ppp. h* dahil olduğunda, uygulama kodu daha sonra bu KıLAVUZDA belirtilen PPP işlev çağrılarını yapabilir.</span><span class="sxs-lookup"><span data-stu-id="ca139-118">Once *nx_ppp.h* is included, the application code is then able to make the PPP function calls specified later in this guide.</span></span> <span data-ttu-id="ca139-119">Uygulama, yapı işlemine *nx_ppp. c* de içermelidir.</span><span class="sxs-lookup"><span data-stu-id="ca139-119">The application must also include *nx_ppp.c* in the build process.</span></span> <span data-ttu-id="ca139-120">Bu dosya, diğer uygulama dosyalarıyla aynı şekilde derlenmelidir ve nesne formu, uygulamanın dosyalarıyla birlikte bağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ca139-120">This file must be compiled in the same manner as other application files and its object form must be linked along with the files of the application.</span></span> <span data-ttu-id="ca139-121">Bu, NetX PPP 'yi kullanmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="ca139-121">This is all that is required to use NetX PPP.</span></span>

## <a name="using-modems"></a><span data-ttu-id="ca139-122">Modem kullanma</span><span class="sxs-lookup"><span data-stu-id="ca139-122">Using Modems</span></span>

<span data-ttu-id="ca139-123">İnternet bağlantısı için bir modem gerekliyse, NetX PPP ürününü kullanabilmeniz için bazı özel noktalar gerekir.</span><span class="sxs-lookup"><span data-stu-id="ca139-123">If a modem is required for connection to the internet, some special considerations are required in order to use the NetX PPP product.</span></span> <span data-ttu-id="ca139-124">Temel olarak, bir modem kullanılması, iletişim kaybı için ek başlatma mantığı ve mantığını tanıtır.</span><span class="sxs-lookup"><span data-stu-id="ca139-124">Basically, using a modem introduces additional initialization logic and logic for loss of communication.</span></span> <span data-ttu-id="ca139-125">Ayrıca, ek modem mantığının çoğu NetX PPP bağlamı dışında gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="ca139-125">In addition, most of the additional modem logic is done outside the context of NetX PPP.</span></span> <span data-ttu-id="ca139-126">NetX PPP 'yi modem ile kullanmanın temel akışı şuna benzer:</span><span class="sxs-lookup"><span data-stu-id="ca139-126">The basic flow of using the NetX PPP with a modem goes something like this:</span></span>

1. <span data-ttu-id="ca139-127">Modemi Başlat</span><span class="sxs-lookup"><span data-stu-id="ca139-127">Initialize Modem</span></span>

1. <span data-ttu-id="ca139-128">Internet servis sağlayıcısı (ISS) ara</span><span class="sxs-lookup"><span data-stu-id="ca139-128">Dial Internet Service Provider (ISP)</span></span>

1. <span data-ttu-id="ca139-129">Bağlantıyı bekle</span><span class="sxs-lookup"><span data-stu-id="ca139-129">Wait for Connection</span></span>

1. <span data-ttu-id="ca139-130">Kullanıcı kimliği Istemi bekle</span><span class="sxs-lookup"><span data-stu-id="ca139-130">Wait for UserID Prompt</span></span>

1. <span data-ttu-id="ca139-131">NetX PPP 'yi Başlat [işlemde PPP]</span><span class="sxs-lookup"><span data-stu-id="ca139-131">Start NetX PPP [PPP in operation]</span></span>

1. <span data-ttu-id="ca139-132">Iletişim kaybı</span><span class="sxs-lookup"><span data-stu-id="ca139-132">Loss of Communication</span></span>

1. <span data-ttu-id="ca139-133">NetX PPP 'yi durdurun (veya nx_ppp_restart aracılığıyla yeniden başlatın)</span><span class="sxs-lookup"><span data-stu-id="ca139-133">Stop NetX PPP (or restart via nx_ppp_restart)</span></span>

### <a name="initialize-modem"></a><span data-ttu-id="ca139-134">Modemi Başlat</span><span class="sxs-lookup"><span data-stu-id="ca139-134">Initialize Modem</span></span>

<span data-ttu-id="ca139-135">Uygulamanın alt düzey seri çıkış yordamını kullanarak, modem bir dizi ASCII karakter komutlarıyla başlatılır (daha fazla ayrıntı için Modemin belgelerine bakın).</span><span class="sxs-lookup"><span data-stu-id="ca139-135">Using the application’s low-level serial output routine, the modem is initialized via a series of ASCII character commands (see modem’s documentation for more details).</span></span>

### <a name="dial-internet-service-provider"></a><span data-ttu-id="ca139-136">Internet hizmet sağlayıcısını ara</span><span class="sxs-lookup"><span data-stu-id="ca139-136">Dial Internet Service Provider</span></span>

<span data-ttu-id="ca139-137">Uygulamanın alt düzey seri çıkış yordamını kullanarak, modemin ISS 'yi çevirebileceği için talimat verilir.</span><span class="sxs-lookup"><span data-stu-id="ca139-137">Using the application’s low-level serial output routine, the modem is instructed to dial the ISP.</span></span> <span data-ttu-id="ca139-138">Örneğin, aşağıdaki 123-4567 numaralı bir ISS 'yi aramak için kullanılan bir ASCII dizesinin tipik bir örneğidir:</span><span class="sxs-lookup"><span data-stu-id="ca139-138">For example, the following is typical of an ASCII string used to dial an ISP at the number 123-4567:</span></span>

<span data-ttu-id="ca139-139">"ATDT123456\r"</span><span class="sxs-lookup"><span data-stu-id="ca139-139">“ATDT123456\r”</span></span>

### <a name="wait-for-connection"></a><span data-ttu-id="ca139-140">Bağlantıyı bekle</span><span class="sxs-lookup"><span data-stu-id="ca139-140">Wait for Connection</span></span>

<span data-ttu-id="ca139-141">Bu noktada, uygulama bir bağlantının kurulduğu modemden bildirim almayı bekler.</span><span class="sxs-lookup"><span data-stu-id="ca139-141">At this point, the application waits to receive indication from the modem that a connection has been established.</span></span> <span data-ttu-id="ca139-142">Bu, uygulamanın alt düzey seri giriş yordamından karakter arayarak yapılır.</span><span class="sxs-lookup"><span data-stu-id="ca139-142">This is accomplished by looking for characters from the application’s low-level serial input routine.</span></span> <span data-ttu-id="ca139-143">Genellikle, modemler bir bağlantı oluşturulduğunda "Bağlan" ASCII dizesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="ca139-143">Typically, modems return an ASCII string “CONNECT” when a connection has been established.</span></span>

### <a name="wait-for-user-id-prompt"></a><span data-ttu-id="ca139-144">Kullanıcı KIMLIĞI Istemi bekle</span><span class="sxs-lookup"><span data-stu-id="ca139-144">Wait for User ID Prompt</span></span>

<span data-ttu-id="ca139-145">Bağlantı kurulduktan sonra, uygulamanın ISS 'den bir ilk oturum açma isteği beklemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="ca139-145">Once the connection has been established, the application must now wait for an initial login request from the ISP.</span></span> <span data-ttu-id="ca139-146">Bu genellikle "oturum aç?" gibi bir ASCII dizesi biçimini alır.</span><span class="sxs-lookup"><span data-stu-id="ca139-146">This typically takes the form of an ASCII string like “Login?”</span></span>

### <a name="start-netx-ppp"></a><span data-ttu-id="ca139-147">NetX PPP 'yi Başlat</span><span class="sxs-lookup"><span data-stu-id="ca139-147">Start NetX PPP</span></span>

<span data-ttu-id="ca139-148">Bu noktada NetX PPP başlatılabilir.</span><span class="sxs-lookup"><span data-stu-id="ca139-148">At this point, the NetX PPP can be started.</span></span> <span data-ttu-id="ca139-149">Bu, *nx_ip_create* hizmeti tarafından izlenen *nx_ppp_create* hizmeti çağırarak gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="ca139-149">This is accomplished by calling the *nx_ppp_create* service followed by the *nx_ip_create* service.</span></span> <span data-ttu-id="ca139-150">PAP 'yi etkinleştirmek ve PPP IP adreslerini ayarlamak için ek hizmetler de gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="ca139-150">Additional services to enable PAP and to setup the PPP IP addresses might also be required.</span></span> <span data-ttu-id="ca139-151">Daha fazla bilgi için lütfen bu kılavuzun aşağıdaki bölümlerini gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="ca139-151">Please review the following sections of this guide for more information.</span></span>

### <a name="loss-of-communication"></a><span data-ttu-id="ca139-152">Iletişim kaybı</span><span class="sxs-lookup"><span data-stu-id="ca139-152">Loss of Communication</span></span>

<span data-ttu-id="ca139-153">PPP başlatıldıktan sonra, PPP olmayan herhangi bir bilgi, *nx_ppp_create* hizmetine belirtilen uygulamayı "geçersiz paket işleme" yordamına geçirilir.</span><span class="sxs-lookup"><span data-stu-id="ca139-153">Once PPP is started, any non-PPP information is passed to the “invalid packet handling” routine the application specified to the *nx_ppp_create* service.</span></span> <span data-ttu-id="ca139-154">Genellikle modemler, ISS ile iletişim kesildiğinde "TAŞıYıCı yok" gibi bir ASCII dizesi gönderir.</span><span class="sxs-lookup"><span data-stu-id="ca139-154">Typically, modems send an ASCII string such as “NO CARRIER” when communication is lost with the ISP.</span></span> <span data-ttu-id="ca139-155">Uygulama bu tür bilgilerle PPP olmayan bir paket aldığında, NetX PPP örneğini durdurmanız veya *nx_ppp_restart* API 'SI aracılığıyla PPP durum makinesini yeniden başlatmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ca139-155">When the application receives a non-PPP packet with such information, it should proceed to either stop the NetX PPP instance or to restart the PPP state machine via the *nx_ppp_restart* API.</span></span>

### <a name="stop-netx-ppp"></a><span data-ttu-id="ca139-156">NetX PPP 'yi durdur</span><span class="sxs-lookup"><span data-stu-id="ca139-156">Stop NetX PPP</span></span>

<span data-ttu-id="ca139-157">NetX PPP 'nin durdurulması oldukça basittir.</span><span class="sxs-lookup"><span data-stu-id="ca139-157">Stopping the NetX PPP is fairly straightforward.</span></span> <span data-ttu-id="ca139-158">Temel olarak, oluşturulan tüm yuvalar ilişkisiz ve silinmiş olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ca139-158">Basically, all created sockets must be unbound and deleted.</span></span> <span data-ttu-id="ca139-159">Sonra, *nx_ip_delete* HIZMETI aracılığıyla IP örneğini silin.</span><span class="sxs-lookup"><span data-stu-id="ca139-159">Next, delete the IP instance via the *nx_ip_delete* service.</span></span> <span data-ttu-id="ca139-160">IP örneği silindikten sonra, PPP 'yi durdurma işlemini tamamlaması için *nx_ppp_delete* hizmeti çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ca139-160">Once the IP instance is deleted, the *nx_ppp_delete* service should be called to finish the process of stopping PPP.</span></span> <span data-ttu-id="ca139-161">Bu noktada, uygulama artık ISS ile iletişimi yeniden kurmayı deneyebilir.</span><span class="sxs-lookup"><span data-stu-id="ca139-161">At this point, the application is now able to attempt to reestablish communication with the ISP.</span></span>

## <a name="small-example-system"></a><span data-ttu-id="ca139-162">Küçük örnek sistem</span><span class="sxs-lookup"><span data-stu-id="ca139-162">Small Example System</span></span>

<span data-ttu-id="ca139-163">NetX PPP kullanmanın ne kadar kolay olduğunu gösteren bir örnek, aşağıda görüntülenen Şekil 1,1 ' de açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="ca139-163">An example that illustrates how easy it is to use NetX PPP is described in Figure 1.1 that appears below.</span></span> <span data-ttu-id="ca139-164">Bu örnekte, *nx_ppp. h* PPP içerme dosyası 3. satırda getirilir.</span><span class="sxs-lookup"><span data-stu-id="ca139-164">In this example, the PPP include file *nx_ppp.h* is brought in at line 3.</span></span> <span data-ttu-id="ca139-165">Sonra, 56 satırındaki *"tx_application_define*" içinde PPP oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ca139-165">Next, PPP is created in *”tx_application_define*” at line 56.</span></span> <span data-ttu-id="ca139-166">"*My_ppp*" PPP denetim bloğu, daha önce satır 9 ' da genel bir değişken olarak tanımlandı.</span><span class="sxs-lookup"><span data-stu-id="ca139-166">The PPP control block “*my_ppp*” was defined as a global variable at line 9 previously.</span></span> 

>[!NOTE]
><span data-ttu-id="ca139-167">IP örneği oluşturulmadan önce PPP oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ca139-167">PPP should be created prior to creating the IP instance.</span></span> <span data-ttu-id="ca139-168">PPP ve IP başarıyla oluşturulduktan sonra, "*my_thread*" Iş parçacığı ppp bağlantısının 98. satırda canlı olmasını bekler.</span><span class="sxs-lookup"><span data-stu-id="ca139-168">After successful creation of PPP and IP, the thread “*my_thread*” waits for the PPP link to come alive at line 98.</span></span> <span data-ttu-id="ca139-169">104. satırda, hem PPP hem de NetX tam olarak çalışır.</span><span class="sxs-lookup"><span data-stu-id="ca139-169">At line 104, both PPP and NetX are fully operational.</span></span>

<span data-ttu-id="ca139-170">Bu örnekte görünmeyen bir öğe, uygulamanın seri bayt Alım ıSR ' dir.</span><span class="sxs-lookup"><span data-stu-id="ca139-170">The one item not shown in this example is the application’s serial byte receive ISR.</span></span> <span data-ttu-id="ca139-171">"*My_ppp*" ile *nx_ppp_byte_receive* ve giriş parametresi olarak alınan bayt çağrısı yapması gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="ca139-171">It will need to call *nx_ppp_byte_receive* with “*my_ppp*” and the byte received as input parameters.</span></span>

```c
#include   "tx_api.h"
#include   "nx_api.h"
#include   "nx_ppp.h"

#define     DEMO_STACK_SIZE         4096
TX_THREAD               my_thread;
NX_PACKET_POOL          my_pool;
NX_IP                   my_ip;
NX_PPP                  my_ppp;

/* Define function prototypes. */

void    my_thread_entry(ULONG thread_input);
void    my_serial_driver_byte_output(UCHAR byte);
void    my_invalid_packet_handler(NX_PACKET *packet_ptr);
 
/* Define main entry point. */
intmain()
{

    /* Enter the ThreadX kernel. */
    tx_kernel_enter();
 }


/* Define what the initial system looks like. */

void    tx_application_define(void *first_unused_memory)
{

CHAR    *pointer;
UINT    status;

/* Setup the working pointer. */
pointer =  (CHAR *) first_unused_memory;

/* Create “my_thread”. */
    tx_thread_create(&my_thread, "my thread", my_thread_entry, 0,  
                  pointer, DEMO_STACK_SIZE, 
                  2, 2, TX_NO_TIME_SLICE, TX_AUTO_START);
    pointer =  pointer + DEMO_STACK_SIZE;

    /* Initialize the NetX system. */
    nx_system_initialize();

    /* Create a packet pool. */
    status =  nx_packet_pool_create(&my_pool, "NetX Main Packet Pool", 
                                    1024, pointer, 64000);
    pointer = pointer + 64000;

    /* Check for pool creation error. */
    if (status)
        error_counter++;

    /* Create a PPP instance. */
    status = nx_ppp_create(&my_ppp, “My PPP”, &my_ip, pointer, 1024, 2, 
                           &my_pool, my_invalid_packet_handler, my_serial_driver_byte_output);
    pointer =  pointer + 1024;
    /* Check for PPP creation pool. */
    if (status)
        error_counter++;

    /* Create an IP instance with the PPP driver. */
    status = nx_ip_create(&my_ip,"My NetX IP Instance", 
                           IP_ADDRESS(216,2,3,1), 0xFFFFFF00, &my_pool, 
                           nx_ppp_driver, pointer, DEMO_STACK_SIZE, 1);
    pointer =  pointer + DEMO_STACK_SIZE;

    /* Check for IP create errors. */
    if (status)
        error_counter++;

    /* Enable ICMP for my IP Instance. */
    status =  nx_icmp_enable(&my_ip);

    /* Check for ICMP enable errors. */
    if (status)
        error_counter++;

    /* Enable UDP. */
    status =  nx_udp_enable(&my_ip);
    if (status)
        error_counter++;
}

/* Define my thread. */
void    my_thread_entry(ULONG thread_input)
{

UINT        status;
ULONG       ip_status;
NX_PACKET   *my_packet;

/* Wait for the PPP link in my_ip to become enabled. */
    status =  nx_ip_status_check(&my_ip,NX_IP_LINK_ENABLED,&ip_status,3000);

    /* Check for IP status error. */
    if (status) 
        return;

    /* Link is fully up and operational. All NetX activities 
    are now available. */

}
```
## <a name="configuration-options"></a><span data-ttu-id="ca139-172">Yapılandırma seçenekleri</span><span class="sxs-lookup"><span data-stu-id="ca139-172">Configuration Options</span></span>

<span data-ttu-id="ca139-173">NetX için PPP oluşturmaya yönelik birkaç yapılandırma seçeneği vardır.</span><span class="sxs-lookup"><span data-stu-id="ca139-173">There are several configuration options for building PPP for NetX.</span></span> <span data-ttu-id="ca139-174">Aşağıdaki listede her biri ayrıntılı açıklanmıştır:</span><span class="sxs-lookup"><span data-stu-id="ca139-174">The following list describes each in detail:</span></span>

- <span data-ttu-id="ca139-175">**NX_DISABLE_ERROR_CHECKING**: tanımlı, bu seçenek temel PPP hata denetimini kaldırır.</span><span class="sxs-lookup"><span data-stu-id="ca139-175">**NX_DISABLE_ERROR_CHECKING**: Defined, this option removes the basic PPP error checking.</span></span> <span data-ttu-id="ca139-176">Genellikle uygulamanın hata ayıklaması yapıldıktan sonra kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ca139-176">It is typically used after the application has been debugged.</span></span>
- <span data-ttu-id="ca139-177">**NX_PPP_PPPOE_ENABLE**: TANıMLANMıŞSA, PPP Ethernet üzerinden paket aktarabilir</span><span class="sxs-lookup"><span data-stu-id="ca139-177">**NX_PPP_PPPOE_ENABLE**: If defined, PPP can transmit packet over Ethernet</span></span>
- <span data-ttu-id="ca139-178">**NX_PPP_BASE_TIMEOUT**: Bu, PPP iş parçacığı GÖREVININ, PPP olaylarını denetlemek için uyandırması gereken dönem oranını (süreölçer işaretleri cinsinden) tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ca139-178">**NX_PPP_BASE_TIMEOUT**: This defines the period rate (in timer ticks) that the PPP thread task is woken to check for PPP events.</span></span> <span data-ttu-id="ca139-179">Varsayılan değer 1 \* NX_IP_PERIODIC_RATE (100 Ticks).</span><span class="sxs-lookup"><span data-stu-id="ca139-179">The default value is 1\*NX_IP_PERIODIC_RATE (100 ticks).</span></span>
- <span data-ttu-id="ca139-180">**NX_PPP_DISABLE_INFO**: tanımlanmışsa, iç PPP bilgi toplama devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="ca139-180">**NX_PPP_DISABLE_INFO**: If defined, internal PPP information gathering is disabled.</span></span>
- <span data-ttu-id="ca139-181">**NX_PPP_DEBUG_LOG_ENABLE**: tanımlanmışsa, iç PPP hata ayıklama günlüğü etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="ca139-181">**NX_PPP_DEBUG_LOG_ENABLE**: If defined, internal PPP debug log is enabled.</span></span>
- <span data-ttu-id="ca139-182">**NX_PPP_DEBUG_LOG_PRINT_ENABLE**: tanımlanmışsa, *STDıO* iç PPP hata *ayıklama günlüğü etkinleştirilir* .</span><span class="sxs-lookup"><span data-stu-id="ca139-182">**NX_PPP_DEBUG_LOG_PRINT_ENABLE**:If defined, internal PPP debug log *printf* to *stdio* is enabled.</span></span> <span data-ttu-id="ca139-183">Bu yalnızca hata ayıklama günlüğü de etkinse geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="ca139-183">This is only valid if the debug log is also enabled.</span></span>
- <span data-ttu-id="ca139-184">**NX_PPP_DEBUG_LOG_SIZE**: hata ayıklama günlüğü boyutu (hata ayıklama günlüğündeki giriş sayısı).</span><span class="sxs-lookup"><span data-stu-id="ca139-184">**NX_PPP_DEBUG_LOG_SIZE**: Size of debug log (number of entries in the debug log).</span></span> <span data-ttu-id="ca139-185">Son girdiye ulaşıldığında, hata ayıklama yakalaması ilk girişe kaydırılır ve daha önce yakalanan tüm verilerin üzerine yazar.</span><span class="sxs-lookup"><span data-stu-id="ca139-185">On reaching the last entry, the debug capture wraps to the first entry and overwrites any data previously captured.</span></span> <span data-ttu-id="ca139-186">Varsayılan değer 50 ' dir.</span><span class="sxs-lookup"><span data-stu-id="ca139-186">The default value is 50.</span></span>
- <span data-ttu-id="ca139-187">**NX_PPP_DEBUG_FRAME_SIZE**: alınan bir paket yükünden yakalanan ve hata ayıklama çıkışına kaydedilen maksimum veri miktarı.</span><span class="sxs-lookup"><span data-stu-id="ca139-187">**NX_PPP_DEBUG_FRAME_SIZE**: Maximum amount of data captured from a received packet payload and saved to debug output.</span></span> <span data-ttu-id="ca139-188">Varsayılan değer 50 ' dir.</span><span class="sxs-lookup"><span data-stu-id="ca139-188">The default value is 50.</span></span>
- <span data-ttu-id="ca139-189">**NX_PPP_DISABLE_CHAP**: TANıMLANMıŞSA, MD5 Özet mantığı dahil olmak üzere Iç PPP CHAP mantığı kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="ca139-189">**NX_PPP_DISABLE_CHAP**: If defined, internal PPP CHAP logic is removed, including the MD5 digest logic.</span></span>
- <span data-ttu-id="ca139-190">**NX_PPP_DISABLE_PAP**: tanımlanmışsa, Iç PPP PAP mantığı kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="ca139-190">**NX_PPP_DISABLE_PAP**: If defined, internal PPP PAP logic is removed.</span></span>
- <span data-ttu-id="ca139-191">**NX_PPP_DNS_OPTION_DISABLE**: TANıMLANMıŞSA, DNS seçeneği IPCP yanıtında devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="ca139-191">**NX_PPP_DNS_OPTION_DISABLE**: If defined, DNS Option is disabled in the IPCP response.</span></span>  <span data-ttu-id="ca139-192">Varsayılan olarak bu seçenek tanımlı değildir (DNS seçeneği ayarlanır).</span><span class="sxs-lookup"><span data-stu-id="ca139-192">By default this option is not defined (DNS option is set).</span></span>
- <span data-ttu-id="ca139-193">**NX_PPP_DNS_ADDRESS_MAX_RETRIES**: Bu, PPP ana bilgisayarının her bir DNS sunucusu adresini IPCP durumundaki eşten ne kadar zaman isteyeceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="ca139-193">**NX_PPP_DNS_ADDRESS_MAX_RETRIES**: This specifies how many times the PPP host will request a DNS Server address from the peer in the IPCP state.</span></span> <span data-ttu-id="ca139-194">NX_PPP_DNS_OPTION_DISABLE tanımlanmışsa bu bir etkiye sahip değildir.</span><span class="sxs-lookup"><span data-stu-id="ca139-194">This has no effect if NX_PPP_DNS_OPTION_DISABLE is defined.</span></span> <span data-ttu-id="ca139-195">Varsayılan değer 2 ' dir.</span><span class="sxs-lookup"><span data-stu-id="ca139-195">The default value is 2.</span></span>
- <span data-ttu-id="ca139-196">**NX_PPP_HASHED_VALUE_SIZE**: CHAP kimlik doğrulamasında kullanılan "karma değer" dizelerinin boyutunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="ca139-196">**NX_PPP_HASHED_VALUE_SIZE**: Specifies the size of “hashed value” strings used in CHAP authentication.</span></span> <span data-ttu-id="ca139-197">Varsayılan değer 16 bayt olarak ayarlanır, ancak *nx_ppp. h* 'ye dahil etmeden önce yeniden tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="ca139-197">The default value is set to 16 bytes, but can be redefined prior to inclusion of *nx_ppp.h.*</span></span>
- <span data-ttu-id="ca139-198">**NX_PPP_MAX_LCP_PROTOCOL_RETRIES**: Bu, PPP zaman aşımına uğrarsa DIĞER bir LCP yapılandırma isteği iletisini gönderdikten en fazla yeniden deneme sayısını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ca139-198">**NX_PPP_MAX_LCP_PROTOCOL_RETRIES**: This defines the max number of retries if the PPP times out before sending another LCP configure request message.</span></span> <span data-ttu-id="ca139-199">Bu sayıya ulaşıldığında, PPP el sıkışması durdurulur ve bağlantı durumu kapanır.</span><span class="sxs-lookup"><span data-stu-id="ca139-199">When this number is reached the PPP handshake is aborted and the link status is down.</span></span> <span data-ttu-id="ca139-200">Varsayılan değer 20 ' dir.</span><span class="sxs-lookup"><span data-stu-id="ca139-200">The default value is 20.</span></span>
- <span data-ttu-id="ca139-201">**NX_PPP_MAX_PAP_PROTOCOL_RETRIES**: Bu, başka bir PAP kimlik doğrulama isteği iletisi göndermeden önce PPP zaman aşımına uğrarsa en fazla yeniden deneme sayısını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ca139-201">**NX_PPP_MAX_PAP_PROTOCOL_RETRIES**: This defines the max number of retries if the PPP times out before sending another PAP authentication request message.</span></span> <span data-ttu-id="ca139-202">Bu sayıya ulaşıldığında, PPP el sıkışması durdurulur ve bağlantı durumu kapanır.</span><span class="sxs-lookup"><span data-stu-id="ca139-202">When this number is reached the PPP handshake is aborted and the link status is down.</span></span> <span data-ttu-id="ca139-203">Varsayılan değer 20 ' dir.</span><span class="sxs-lookup"><span data-stu-id="ca139-203">The default value is 20.</span></span>
- <span data-ttu-id="ca139-204">**NX_PPP_MAX_CHAP_PROTOCOL_RETRIES**: Bu, başka bir CHAP sınama iletisi göndermeden önce PPP zaman aşımına uğrarsa en fazla yeniden deneme sayısını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ca139-204">**NX_PPP_MAX_CHAP_PROTOCOL_RETRIES**: This defines the max number of retries if the PPP times out before sending another CHAP challenge message.</span></span> <span data-ttu-id="ca139-205">Bu sayıya ulaşıldığında, PPP el sıkışması durdurulur ve bağlantı durumu kapanır.</span><span class="sxs-lookup"><span data-stu-id="ca139-205">When this number is reached the PPP handshake is aborted and the link status is down.</span></span> <span data-ttu-id="ca139-206">Varsayılan değer 20 ' dir.</span><span class="sxs-lookup"><span data-stu-id="ca139-206">The default value is 20.</span></span>
- <span data-ttu-id="ca139-207">**NX_PPP_MAX_IPCP_PROTOCOL_RETRIES**: Bu, PPP zaman aşımına uğrarsa başka bir IPCP yapılandırma isteği iletisini gönderdikten en fazla yeniden deneme sayısını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ca139-207">**NX_PPP_MAX_IPCP_PROTOCOL_RETRIES**: This defines the max number of retries if the PPP times out before sending another IPCP configure request message.</span></span> <span data-ttu-id="ca139-208">Bu sayıya ulaşıldığında, PPP el sıkışması durdurulur ve bağlantı durumu kapanır.</span><span class="sxs-lookup"><span data-stu-id="ca139-208">When this number is reached the PPP handshake is aborted and the link status is down.</span></span> <span data-ttu-id="ca139-209">Varsayılan değer 20 ' dir.</span><span class="sxs-lookup"><span data-stu-id="ca139-209">The default value is 20.</span></span>
- <span data-ttu-id="ca139-210">**NX_PPP_MRU**: PPP Için en fazla alma BIRIMI (MRU) sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="ca139-210">**NX_PPP_MRU**: Specifies the Maximum Receive Unit (MRU) for PPP.</span></span> <span data-ttu-id="ca139-211">Varsayılan olarak, bu değer 1.500 bayttır (minimum değer).</span><span class="sxs-lookup"><span data-stu-id="ca139-211">By default, this value is 1,500 bytes (the minimum value).</span></span> <span data-ttu-id="ca139-212">Bu tanımlama, *nx_ppp. h*'ye dahil etmeden önce uygulama tarafından ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="ca139-212">This define can be set by the application prior to inclusion of *nx_ppp.h*.</span></span>
- <span data-ttu-id="ca139-213">**NX_PPP_MINIMUM_MRU**: bir LCP yapılandırma isteği iletisinde alınan en küçük MRU değeri belirtir.</span><span class="sxs-lookup"><span data-stu-id="ca139-213">**NX_PPP_MINIMUM_MRU**: Specifies the minimum MRU received in an LCP configure request message.</span></span> <span data-ttu-id="ca139-214">Varsayılan olarak, bu değer 1.500 bayttır (minimum değer).</span><span class="sxs-lookup"><span data-stu-id="ca139-214">By default, this value is 1,500 bytes (the minimum value).</span></span> <span data-ttu-id="ca139-215">Bu tanımlama, *nx_ppp. h*'ye dahil etmeden önce uygulama tarafından ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="ca139-215">This define can be set by the application prior to inclusion of *nx_ppp.h*.</span></span>
- <span data-ttu-id="ca139-216">**NX_PPP_NAME_SIZE**: kimlik doğrulamasında kullanılan "ad" dizelerinin boyutunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="ca139-216">**NX_PPP_NAME_SIZE**: Specifies the size of “name” strings used in authentication.</span></span> <span data-ttu-id="ca139-217">Varsayılan değer 32bytes olarak ayarlanır, ancak \* nx_ppp. h 'ye dahil etmeden önce yeniden tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="ca139-217">The default value is set to 32bytes, but can be redefined prior to inclusion of \*nx_ppp.h.</span></span>
- <span data-ttu-id="ca139-218">**NX_PPP_PASSWORD_SIZE**: kimlik doğrulamasında kullanılan "parola" dizelerinin boyutunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="ca139-218">**NX_PPP_PASSWORD_SIZE**: Specifies the size of “password” strings used in authentication.</span></span> <span data-ttu-id="ca139-219">Varsayılan değer 32bytes olarak ayarlanır, ancak *nx_ppp. h* 'ye dahil etmeden önce yeniden tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="ca139-219">The default value is set to 32bytes, but can be redefined prior to inclusion of *nx_ppp.h.*</span></span>
- <span data-ttu-id="ca139-220">**NX_PPP_PROTOCOL_TIMEOUT**: Bu, PPP GÖREVININ bir PPP protokol isteği iletisine yanıt alması için bekleme seçeneğini (saniye cinsinden) tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ca139-220">**NX_PPP_PROTOCOL_TIMEOUT**: This defines the wait option (in seconds) for the PPP task to receive a response to a PPP protocol request message.</span></span> <span data-ttu-id="ca139-221">Varsayılan değer 4 saniyedir.</span><span class="sxs-lookup"><span data-stu-id="ca139-221">The default value is 4 seconds.</span></span>
- <span data-ttu-id="ca139-222">**NX_PPP_RECEIVE_TIMEOUTS**: Bu, PPP iş parçacığı GÖREVININ bir PPP ileti akışında bir sonraki karakteri almak için bekleyen kaç kez zaman aşımı olduğunu tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ca139-222">**NX_PPP_RECEIVE_TIMEOUTS**: This defines the number of times the PPP thread task times out waiting to receive the next character in a PPP message stream.</span></span> <span data-ttu-id="ca139-223">Bundan sonra PPP paketi yayınlar ve sonraki PPP iletisini almayı beklemeye başlar.</span><span class="sxs-lookup"><span data-stu-id="ca139-223">Thereafter, PPP releases the packet and begins waiting to receive the next PPP message.</span></span> <span data-ttu-id="ca139-224">Varsayılan değer 4'tür.</span><span class="sxs-lookup"><span data-stu-id="ca139-224">The default value is 4.</span></span>
- <span data-ttu-id="ca139-225">**NX_PPP_SERIAL_BUFFER_SIZE**: alma karakteri seri arabelleğinin boyutunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="ca139-225">**NX_PPP_SERIAL_BUFFER_SIZE**: Specifies the size of the receive character serial buffer.</span></span> <span data-ttu-id="ca139-226">Varsayılan olarak, bu değer 3.000 bayttır.</span><span class="sxs-lookup"><span data-stu-id="ca139-226">By default, this value is 3,000 bytes.</span></span> <span data-ttu-id="ca139-227">Bu tanımlama, *nx_ppp. h*'ye dahil etmeden önce uygulama tarafından ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="ca139-227">This define can be set by the application prior to inclusion of *nx_ppp.h*.</span></span>
- <span data-ttu-id="ca139-228">**NX_PPP_TIMEOUT**: Bu, verileri iletmek için paket AYıRMAYA ve IP katmanına gönderilmek üzere paketlere PPP seri verileri arabelleğe almak için bekleme seçeneğini (süreölçer işaretleri) tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ca139-228">**NX_PPP_TIMEOUT**: This defines the wait option (in timer ticks) for allocating packets to transmit data as well as buffer PPP serial data into packets to send to the IP layer.</span></span> <span data-ttu-id="ca139-229">Varsayılan değer 4 \* NX_IP_PERIODIC_RATE (400 Ticks).</span><span class="sxs-lookup"><span data-stu-id="ca139-229">The default value is 4\*NX_IP_PERIODIC_RATE (400 ticks).</span></span>
- <span data-ttu-id="ca139-230">**NX_PPP_THREAD_TIME_SLICE**: PPP iş parçacıkları için zaman dilimi seçeneği.</span><span class="sxs-lookup"><span data-stu-id="ca139-230">**NX_PPP_THREAD_TIME_SLICE**: Time-slice option for PPP threads.</span></span> <span data-ttu-id="ca139-231">Varsayılan olarak, bu değer TX_NO_TIME_SLICE.</span><span class="sxs-lookup"><span data-stu-id="ca139-231">By default, this value is TX_NO_TIME_SLICE.</span></span> <span data-ttu-id="ca139-232">Bu tanımlama, *nx_ppp. h*'ye dahil etmeden önce uygulama tarafından ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="ca139-232">This define can be set by the application prior to inclusion of *nx_ppp.h*.</span></span>
- <span data-ttu-id="ca139-233">**NX_PPP_VALUE_SIZE**: CHAP kimlik doğrulamasında kullanılan "değer" dizelerinin boyutunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="ca139-233">**NX_PPP_VALUE_SIZE**: Specifies the size of “value” strings used in CHAP authentication.</span></span> <span data-ttu-id="ca139-234">Varsayılan değer 32bytes olarak ayarlanır, ancak nx_ppp. h 'ye dahil etmeden önce yeniden tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="ca139-234">The default value is set to 32bytes, but can be redefined prior to inclusion of nx_ppp.h.</span></span>
