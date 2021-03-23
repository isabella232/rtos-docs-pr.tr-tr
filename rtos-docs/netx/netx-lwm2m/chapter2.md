---
title: Bölüm 2-Azure RTOS NetX LWM2M yükleme ve kullanımı
description: Bu bölümde, Azure RTOS NetX LWM2M bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların bir açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 8c13d3b092d3a5b59bd0369f6ffc162509d02590
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826699"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-lwm2m"></a><span data-ttu-id="ac42a-103">Bölüm 2-Azure RTOS NetX LWM2M yükleme ve kullanımı</span><span class="sxs-lookup"><span data-stu-id="ac42a-103">Chapter 2 - Installation and use of Azure RTOS NetX LWM2M</span></span>

<span data-ttu-id="ac42a-104">Bu bölümde, Azure RTOS NetX LWM2M bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların bir açıklaması yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="ac42a-104">This chapter contains a description of various issues related to installation, setup, and usage of the Azure RTOS NetX LWM2M component.</span></span>

## <a name="product-distribution"></a><span data-ttu-id="ac42a-105">Ürün dağıtımı</span><span class="sxs-lookup"><span data-stu-id="ac42a-105">Product Distribution</span></span>

<span data-ttu-id="ac42a-106">NetX LWM2M, adresinde bulunabilir [https://github.com/azure-rtos/netx](https://github.com/azure-rtos/netx) .</span><span class="sxs-lookup"><span data-stu-id="ac42a-106">NetX LWM2M is available at [https://github.com/azure-rtos/netx](https://github.com/azure-rtos/netx).</span></span> <span data-ttu-id="ac42a-107">Bu paket üç kaynak dosyası, bir içerme dosyası ve bu belgeyi içeren bir PDF dosyası içerir ve aşağıdaki gibi:</span><span class="sxs-lookup"><span data-stu-id="ac42a-107">The package includes three source files, one include files, and a PDF file that contains this document, as follows:</span></span>

- <span data-ttu-id="ac42a-108">**nx_lwm2m_client. h**: NETX lwm2m istemcisi için üst bilgi dosyası</span><span class="sxs-lookup"><span data-stu-id="ac42a-108">**nx_lwm2m_client.h**: Header file for the NetX LWM2M Client</span></span>

- <span data-ttu-id="ac42a-109">\*\*nx_lwm2m_ \*. c/h\*\*: NETX lwm2m için c/h kaynak dosyaları</span><span class="sxs-lookup"><span data-stu-id="ac42a-109">**nx_lwm2m_\*.c/h**: C/H Source files for NetX LWM2M</span></span>

- <span data-ttu-id="ac42a-110">**demo_netx_lwm2m_client. c**: NETX Lwm2m istemci tanıtımı Için c kaynak dosyası</span><span class="sxs-lookup"><span data-stu-id="ac42a-110">**demo_netx_lwm2m_client.c**: C Source file for NetX LWM2M Client Demo</span></span>

- <span data-ttu-id="ac42a-111">**NetX_LWM2M_User_Guide.pdf**: NETX LWM2M ürününün PDF açıklaması</span><span class="sxs-lookup"><span data-stu-id="ac42a-111">**NetX_LWM2M_User_Guide.pdf**: PDF description of NetX LWM2M product</span></span>

## <a name="netx-lwm2m-installation"></a><span data-ttu-id="ac42a-112">NetX LWM2M yüklemesi</span><span class="sxs-lookup"><span data-stu-id="ac42a-112">NetX LWM2M Installation</span></span>

<span data-ttu-id="ac42a-113">NetX LWM2M kullanabilmeniz için, daha önce bahsedilen dağıtımın tamamı NetX 'in yüklü olduğu dizine kopyalanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ac42a-113">In order to use NetX LWM2M, the entire distribution mentioned previously should be copied to the same directory where NetX is installed.</span></span> <span data-ttu-id="ac42a-114">Örneğin, NetX, "*\\ threadx \\ ARM7 \\ green*" dizinine yüklenirse *nx_lwm2m&#42;. &#42;* dosyaları bu dizine kopyalanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ac42a-114">For example, if NetX is installed in the directory "*\\threadx\\arm7\\green*" then the *nx_lwm2m&#42;.&#42;* files should be copied into this directory.</span></span>

## <a name="using-netx-lwm2m"></a><span data-ttu-id="ac42a-115">NetX LWM2M kullanma</span><span class="sxs-lookup"><span data-stu-id="ac42a-115">Using NetX LWM2M</span></span>

<span data-ttu-id="ac42a-116">NetX LWM2M kullanmak kolaydır.</span><span class="sxs-lookup"><span data-stu-id="ac42a-116">Using NetX LWM2M is easy.</span></span> <span data-ttu-id="ac42a-117">Temel olarak uygulama kodu, ThreadX ve NetX kullanmak için *tx_api. h* ve *nx_api. h* dahil *nx_lwm2m_client. h* 'yi içermelidir.</span><span class="sxs-lookup"><span data-stu-id="ac42a-117">Basically, the application code must include *nx_lwm2m_client.h* after it includes *tx_api.h* and *nx_api.h*, in order to use ThreadX and NetX.</span></span> <span data-ttu-id="ac42a-118">*Nx_lwm2m_client. h* dahil olduğunda, uygulama kodu daha sonra bu kılavuzda belirtilen NETX lwm2m işlev çağrılarını yapabilir.</span><span class="sxs-lookup"><span data-stu-id="ac42a-118">Once *nx_lwm2m_client.h* is included, the application code is then able to make the NetX LWM2M function calls specified later in this guide.</span></span> <span data-ttu-id="ac42a-119">Uygulamanın Ayrıca, *nx_lwm2m&#42;. &#42;* dosyalarını NETX kitaplığına aktarması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ac42a-119">The application must also import the *nx_lwm2m&#42;.&#42;* files into the NetX library.</span></span>

## <a name="configuration-options"></a><span data-ttu-id="ac42a-120">Yapılandırma seçenekleri</span><span class="sxs-lookup"><span data-stu-id="ac42a-120">Configuration Options</span></span>

<span data-ttu-id="ac42a-121">LWM2M Istemci kitaplığı ve uygulamayı LWM2M Istemcisini kullanarak oluştururken birkaç yapılandırma seçeneği vardır.</span><span class="sxs-lookup"><span data-stu-id="ac42a-121">There are several configuration options when building the LWM2M Client library and the application using the LWM2M Client.</span></span> <span data-ttu-id="ac42a-122">Yapılandırma seçenekleri, aksi belirtilmediği takdirde, komut satırında, uygulama kaynağında tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="ac42a-122">The configuration options can be defined in the application source, on the command line, unless otherwise specified.</span></span>

### <a name="nx_lwm2m_client_disable_error_checking"></a><span data-ttu-id="ac42a-123">NX_LWM2M_CLIENT_DISABLE_ERROR_CHECKING</span><span class="sxs-lookup"><span data-stu-id="ac42a-123">NX_LWM2M_CLIENT_DISABLE_ERROR_CHECKING</span></span>

<span data-ttu-id="ac42a-124">Tanımlanmıştır, temel LWM2M Istemci hata denetimi API 'sini kaldırır ve performansı geliştirir.</span><span class="sxs-lookup"><span data-stu-id="ac42a-124">Defined, removes the basic LWM2M Client error checking API and improves performance.</span></span> <span data-ttu-id="ac42a-125">Hata denetimini devre dışı bırakarak etkilenmeyen API dönüş kodları, API tanımında kalın yazı tipiyle listelenmiştir.</span><span class="sxs-lookup"><span data-stu-id="ac42a-125">API return codes not affected by disabling error checking are listed in bold typeface in the API definition.</span></span>

### <a name="nx_lwm2m_client_disable_float"></a><span data-ttu-id="ac42a-126">NX_LWM2M_CLIENT_DISABLE_FLOAT</span><span class="sxs-lookup"><span data-stu-id="ac42a-126">NX_LWM2M_CLIENT_DISABLE_FLOAT</span></span>

<span data-ttu-id="ac42a-127">Tanımlanmış, kayan nokta numarası değerlerinin desteğini kaldırır.</span><span class="sxs-lookup"><span data-stu-id="ac42a-127">Defined, removes the support of floating point numbers values.</span></span> <span data-ttu-id="ac42a-128">Devre dışı bırakıldığında LWM2M Istemcisi float veri türüne sahip kaynakları desteklemez.</span><span class="sxs-lookup"><span data-stu-id="ac42a-128">When disabled the LWM2M Client cannot support Resources with Float data type.</span></span>

### <a name="nx_lwm2m_client_disable_float64"></a><span data-ttu-id="ac42a-129">NX_LWM2M_CLIENT_DISABLE_FLOAT64</span><span class="sxs-lookup"><span data-stu-id="ac42a-129">NX_LWM2M_CLIENT_DISABLE_FLOAT64</span></span>

<span data-ttu-id="ac42a-130">Tanımlı, 64 bitlik kayan nokta sayı değerlerinin desteğini kaldırır.</span><span class="sxs-lookup"><span data-stu-id="ac42a-130">Defined, removes the support of 64-bit floating point numbers values.</span></span> <span data-ttu-id="ac42a-131">LWM2M Istemcisi 64 bitlik kayan sayılar içeren TLV iletileri almaya devam edebilir, ancak değerler işlenmek üzere 32 bitlik kayan noktaya dönüştürülür.</span><span class="sxs-lookup"><span data-stu-id="ac42a-131">The LWM2M Client can still receive TLV messages containing 64-bit floating numbers, but the values are converted to 32-bit floating point for processing.</span></span>

### <a name="nx_lwm2m_client_priority"></a><span data-ttu-id="ac42a-132">NX_LWM2M_CLIENT_PRIORITY</span><span class="sxs-lookup"><span data-stu-id="ac42a-132">NX_LWM2M_CLIENT_PRIORITY</span></span>

<span data-ttu-id="ac42a-133">LWM2M Istemci iş parçacığının önceliğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="ac42a-133">Specifies the priority of the LWM2M Client thread.</span></span> <span data-ttu-id="ac42a-134">Varsayılan olarak, 16 önceliğini belirtmek için bu değer 16 olarak tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="ac42a-134">By default, this value is defined as 16 to specify priority 16.</span></span>

### <a name="nx_lwm2m_client_max_device_errors"></a><span data-ttu-id="ac42a-135">NX_LWM2M_CLIENT_MAX_DEVICE_ERRORS</span><span class="sxs-lookup"><span data-stu-id="ac42a-135">NX_LWM2M_CLIENT_MAX_DEVICE_ERRORS</span></span>

<span data-ttu-id="ac42a-136">Cihaz nesnesi tarafından depolanan en fazla hata kodu sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="ac42a-136">Specifies the maximum number of error codes stored by the Device Object.</span></span> <span data-ttu-id="ac42a-137">Varsayılan değer 8 ' dir.</span><span class="sxs-lookup"><span data-stu-id="ac42a-137">The default value is 8.</span></span>

### <a name="nx_lwm2m_client_max_security_instances"></a><span data-ttu-id="ac42a-138">NX_LWM2M_CLIENT_MAX_SECURITY_INSTANCES</span><span class="sxs-lookup"><span data-stu-id="ac42a-138">NX_LWM2M_CLIENT_MAX_SECURITY_INSTANCES</span></span>

<span data-ttu-id="ac42a-139">En fazla güvenlik nesnesi örneği sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="ac42a-139">Specifies the maximum number of Security Object Instances.</span></span> <span data-ttu-id="ac42a-140">Varsayılan değer, bir önyükleme sunucusunu ve standart sunucuyu desteklemek için 2 ' dir.</span><span class="sxs-lookup"><span data-stu-id="ac42a-140">The default value is 2 for supporting a Bootstrap Server and a standard Server.</span></span>

### <a name="nx_lwm2m_client_max_server_instances"></a><span data-ttu-id="ac42a-141">NX_LWM2M_CLIENT_MAX_SERVER_INSTANCES</span><span class="sxs-lookup"><span data-stu-id="ac42a-141">NX_LWM2M_CLIENT_MAX_SERVER_INSTANCES</span></span>

<span data-ttu-id="ac42a-142">En fazla sunucu nesne örneği sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="ac42a-142">Specifies the maximum number of Server Object Instances.</span></span> <span data-ttu-id="ac42a-143">Tek bir standart sunucuyu desteklemek için varsayılan değer 1 ' dir.</span><span class="sxs-lookup"><span data-stu-id="ac42a-143">The default value is 1 for supporting a single standard Server.</span></span>

### <a name="nx_lwm2m_client_max_server_uri"></a><span data-ttu-id="ac42a-144">NX_LWM2M_CLIENT_MAX_SERVER_URI</span><span class="sxs-lookup"><span data-stu-id="ac42a-144">NX_LWM2M_CLIENT_MAX_SERVER_URI</span></span>

<span data-ttu-id="ac42a-145">Bir sunucu URI 'sinin Sonlandırıcı karakteri de dahil olmak üzere maksimum uzunluğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="ac42a-145">Specifies the maximum length of a server URI, including terminating nil character.</span></span> <span data-ttu-id="ac42a-146">Varsayılan değer 128 ' dir.</span><span class="sxs-lookup"><span data-stu-id="ac42a-146">The default value is 128.</span></span>

### <a name="nx_lwm2m_client_max_access_control_instances"></a><span data-ttu-id="ac42a-147">NX_LWM2M_CLIENT_MAX_ACCESS_CONTROL_INSTANCES</span><span class="sxs-lookup"><span data-stu-id="ac42a-147">NX_LWM2M_CLIENT_MAX_ACCESS_CONTROL_INSTANCES</span></span>

<span data-ttu-id="ac42a-148">En fazla Access Control örneği sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="ac42a-148">Specifies the maximum number of Access Control Instances.</span></span> <span data-ttu-id="ac42a-149">Varsayılan değer 0 ' dır ve bu, erişim denetimini devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="ac42a-149">The default value is 0, which disables access control.</span></span> <span data-ttu-id="ac42a-150">Uygulama birden fazla LWM2M sunucusunu destekliyorsa, her bir nesne örneği (güvenlik nesnesi örnekleri hariç) için bir Access Control örneği oluşturulması gerektiği için, en fazla Access Control örnek sayısı, LWM2M Istemcisinin destekleyeceği en fazla nesne örneği sayısına ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ac42a-150">If the application supports more than one LWM2M Server, the maximum number of Access Control Instances must be set to the maximum number of Object Instances that the LWM2M Client will support, as one Access Control Instance must be created for each Object Instance (except for the Security Object Instances).</span></span>

### <a name="nx_lwm2m_client_max_access_control_acls"></a><span data-ttu-id="ac42a-151">NX_LWM2M_CLIENT_MAX_ACCESS_CONTROL_ACLS</span><span class="sxs-lookup"><span data-stu-id="ac42a-151">NX_LWM2M_CLIENT_MAX_ACCESS_CONTROL_ACLS</span></span>

<span data-ttu-id="ac42a-152">Access Control örnek başına en fazla ACL kaynağı sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="ac42a-152">Specifies the maximum number of ACL resources per Access Control Instance.</span></span> <span data-ttu-id="ac42a-153">Varsayılan değer 4'tür.</span><span class="sxs-lookup"><span data-stu-id="ac42a-153">The default value is 4.</span></span>

### <a name="nx_lwm2m_client_max_notifications"></a><span data-ttu-id="ac42a-154">NX_LWM2M_CLIENT_MAX_NOTIFICATIONS</span><span class="sxs-lookup"><span data-stu-id="ac42a-154">NX_LWM2M_CLIENT_MAX_NOTIFICATIONS</span></span>

<span data-ttu-id="ac42a-155">LWM2M Istemcisinin destekleyeceği en fazla bildirim sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="ac42a-155">Specifies the maximum number of notifications that the LWM2M Client will support.</span></span> <span data-ttu-id="ac42a-156">Bir LWM2M sunucusu nesneler, nesne örnekleri ve kaynaklar üzerinde bildirimler ayarlayabilir.</span><span class="sxs-lookup"><span data-stu-id="ac42a-156">A LWM2M Server can set notifications on Objects, Object Instances, and Resources.</span></span> <span data-ttu-id="ac42a-157">Varsayılan değer 8 ' dir.</span><span class="sxs-lookup"><span data-stu-id="ac42a-157">The default value is 8.</span></span>

### <a name="nx_lwm2m_client_max_resources"></a><span data-ttu-id="ac42a-158">NX_LWM2M_CLIENT_MAX_RESOURCES</span><span class="sxs-lookup"><span data-stu-id="ac42a-158">NX_LWM2M_CLIENT_MAX_RESOURCES</span></span>

<span data-ttu-id="ac42a-159">Nesne başına en fazla kaynak sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="ac42a-159">Specifies the maximum number of Resources per Object.</span></span> <span data-ttu-id="ac42a-160">Varsayılan değer 32 ' dir.</span><span class="sxs-lookup"><span data-stu-id="ac42a-160">The default value is 32.</span></span>

### <a name="nx_lwm2m_client_bootstrap_idle_timer"></a><span data-ttu-id="ac42a-161">NX_LWM2M_CLIENT_BOOTSTRAP_IDLE_TIMER</span><span class="sxs-lookup"><span data-stu-id="ac42a-161">NX_LWM2M_CLIENT_BOOTSTRAP_IDLE_TIMER</span></span>

<span data-ttu-id="ac42a-162">Oturumu iptal etmeden önce önyükleme oturumu başlatıldığında önyükleme sunucusu istekleri için beklenecek en uzun süreyi belirtir.</span><span class="sxs-lookup"><span data-stu-id="ac42a-162">Specifies the maximum time to wait for bootstrap server requests when the bootstrap session is initiated before aborting the session.</span></span> <span data-ttu-id="ac42a-163">Varsayılan değer 60 saniyedir.</span><span class="sxs-lookup"><span data-stu-id="ac42a-163">The default value is 60 seconds.</span></span>

### <a name="nx_lwm2m_client_dtls_start_timeout"></a><span data-ttu-id="ac42a-164">NX_LWM2M_CLIENT_DTLS_START_TIMEOUT</span><span class="sxs-lookup"><span data-stu-id="ac42a-164">NX_LWM2M_CLIENT_DTLS_START_TIMEOUT</span></span>

<span data-ttu-id="ac42a-165">DTLS el sıkışma tamamlanması için beklenecek en uzun süreyi belirtir.</span><span class="sxs-lookup"><span data-stu-id="ac42a-165">Specifies the maximum time to wait for DTLS handshake completion.</span></span> <span data-ttu-id="ac42a-166">Varsayılan değer 30 saniyedir.</span><span class="sxs-lookup"><span data-stu-id="ac42a-166">The default value is 30 seconds.</span></span>

### <a name="nx_lwm2m_client_dtls_end_timeout"></a><span data-ttu-id="ac42a-167">NX_LWM2M_CLIENT_DTLS_END_TIMEOUT</span><span class="sxs-lookup"><span data-stu-id="ac42a-167">NX_LWM2M_CLIENT_DTLS_END_TIMEOUT</span></span>

<span data-ttu-id="ac42a-168">DTLS kapatması işleminin tamamlanması için beklenecek en uzun süreyi belirtir.</span><span class="sxs-lookup"><span data-stu-id="ac42a-168">Specifies the maximum time to wait for DTLS shutdown completion.</span></span> <span data-ttu-id="ac42a-169">Varsayılan değer 5 saniyedir.</span><span class="sxs-lookup"><span data-stu-id="ac42a-169">The default value is 5 seconds.</span></span>
