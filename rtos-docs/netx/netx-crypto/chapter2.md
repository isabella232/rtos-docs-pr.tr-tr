---
title: Bölüm 2-Azure RTOS NetX şifre yüklemesi ve kullanımı
description: Bu bölümde, NetX şifreleme bileşeninin yüklenmesi, kurulumu ve kullanımı ile ilgili çeşitli sorunların bir açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 1616667c5efd73229ed69bcd4e5de5f80e5826f9
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826818"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-crypto"></a><span data-ttu-id="30dbe-103">Bölüm 2-Azure RTOS NetX şifre yüklemesi ve kullanımı</span><span class="sxs-lookup"><span data-stu-id="30dbe-103">Chapter 2 - Installation and use of Azure RTOS NetX Crypto</span></span>

<span data-ttu-id="30dbe-104">Bu bölümde, Azure RTOS NetX şifreleme bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların bir açıklaması yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="30dbe-104">This chapter contains a description of various issues related to installation, setup, and usage of the Azure RTOS NetX Crypto component.</span></span>

## <a name="product-distribution"></a><span data-ttu-id="30dbe-105">Ürün dağıtımı</span><span class="sxs-lookup"><span data-stu-id="30dbe-105">Product Distribution</span></span>

<span data-ttu-id="30dbe-106">Azure RTOS NetX şifrelemesi adresinde bulunabilir [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo) .</span><span class="sxs-lookup"><span data-stu-id="30dbe-106">Azure RTOS NetX Crypto is available at [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo).</span></span> <span data-ttu-id="30dbe-107">Paket, kaynak dosyaları, içerme dosyaları ve bu belgeyi içeren bir PDF dosyasını aşağıdaki gibi içerir:</span><span class="sxs-lookup"><span data-stu-id="30dbe-107">The package includes source files, include files, and a PDF file that contains this document, as follows:</span></span>

- <span data-ttu-id="30dbe-108">**nx_crypto. h**: ortak API üstbilgi dosyası NETX şifreleme modülü</span><span class="sxs-lookup"><span data-stu-id="30dbe-108">**nx_crypto.h**: Public API header file NetX Crypto module</span></span>
- <span data-ttu-id="30dbe-109">\*\*nx_crypto_ \*. c/h\*\*: NETX şifrelemesi için c/h kaynak dosyaları</span><span class="sxs-lookup"><span data-stu-id="30dbe-109">**nx_crypto_\*.c/h**: C/H Source files for NetX Crypto</span></span>
- <span data-ttu-id="30dbe-110">**nx_crypto_port. h**: tüm geliştirme araçlarını ve hedef belirli veri tanımlarını ve yapıları Içeren C üstbilgi dosyası.</span><span class="sxs-lookup"><span data-stu-id="30dbe-110">**nx_crypto_port.h**: C header file containing all development-tool and target specific data definitions and structures.</span></span>
- <span data-ttu-id="30dbe-111">**NetX_Crypto_User_Guide.pdf**: NETX şifre modülünün PDF açıklaması.</span><span class="sxs-lookup"><span data-stu-id="30dbe-111">**NetX_Crypto_User_Guide.pdf**: PDF description of NetX Crypto Module.</span></span>

## <a name="netx-crypto-installation"></a><span data-ttu-id="30dbe-112">NetX şifre yüklemesi</span><span class="sxs-lookup"><span data-stu-id="30dbe-112">NetX Crypto Installation</span></span>

<span data-ttu-id="30dbe-113">Daha önce bahsedilen tüm dağıtım, NetX Duo deposunun kök düzeyinde bulunan **crypto_libraries** dizininde mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="30dbe-113">The entire distribution mentioned previously is available in **crypto_libraries** directory, present at root level of NetX Duo repository.</span></span>

<span data-ttu-id="30dbe-114">NetX şifre kullanabilmesi için, daha önce bahsedilen dağıtımın tamamı, NetX 'in yüklü olduğu aynı dizin düzeyine kopyalanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="30dbe-114">In order to use NetX Crypto, the entire distribution mentioned previously should be copied to the same directory level where NetX is installed.</span></span> <span data-ttu-id="30dbe-115">Örneğin, "\threadx\arm7\NetX" dizininde NetX yüklüyse nx_crypto *.*</span><span class="sxs-lookup"><span data-stu-id="30dbe-115">For example, if NetX is installed in the directory "\threadx\arm7\NetX" then the nx_crypto *.*</span></span> <span data-ttu-id="30dbe-116">dizinler "\Threadx\arm7\netxşifre" dizinine kopyalanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="30dbe-116">directories should be copied into "\threadx\arm7\NetXCrypto".</span></span>

<span data-ttu-id="30dbe-117">Tek başına modda kullanılmak üzere NetX şifrelemesi için, daha önce bahsedilen dağıtımın tamamının uygulama projesine kopyalanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="30dbe-117">For NetX Crypto to be used in standalone mode, the entire distribution mentioned previously should be copied to the application project.</span></span> <span data-ttu-id="30dbe-118">Örneğin **crypto_libraries** dizin uygulama projesine kopyalanmalıdır ya da **crypto_libraries** dizine sahip bir kitaplık projesi oluşturulup uygulama projesine bağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="30dbe-118">For example **crypto_libraries** directory should be copied to the application project or a library project with **crypto_libraries** directory should be created and linked to the application project.</span></span> 

## <a name="using-netx-crypto"></a><span data-ttu-id="30dbe-119">NetX şifre kullanımı</span><span class="sxs-lookup"><span data-stu-id="30dbe-119">Using NetX Crypto</span></span>

<span data-ttu-id="30dbe-120">NetX şifre kullanımı kolaydır.</span><span class="sxs-lookup"><span data-stu-id="30dbe-120">Using NetX Crypto is easy.</span></span> <span data-ttu-id="30dbe-121">Temel olarak, uygulama kodu *nx_crypto. h* öğesini içermelidir.</span><span class="sxs-lookup"><span data-stu-id="30dbe-121">Basically, the application code must include the *nx_crypto.h*.</span></span>  <span data-ttu-id="30dbe-122">*Nx_crypto. h* dahil olduğunda, uygulama kodu daha sonra bu kılavuzda belirtilen NETX şifre işlev çağrılarını yapabilir.</span><span class="sxs-lookup"><span data-stu-id="30dbe-122">Once *nx_crypto.h* is included, the application code is then able to make the NetX Crypto function calls specified later in this guide.</span></span>

## <a name="configuration-options"></a><span data-ttu-id="30dbe-123">Yapılandırma seçenekleri</span><span class="sxs-lookup"><span data-stu-id="30dbe-123">Configuration Options</span></span>

<span data-ttu-id="30dbe-124">NetX şifrelemesi oluşturmak için birkaç yapılandırma seçeneği vardır.</span><span class="sxs-lookup"><span data-stu-id="30dbe-124">There are several configuration options for building NetX Crypto.</span></span> <span data-ttu-id="30dbe-125">Aşağıda, her birinin ayrıntılı olarak açıklandığı tüm seçeneklerin bir listesi verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="30dbe-125">Following is a list of all options, where each is described in detail:</span></span>

- <span data-ttu-id="30dbe-126">**NX_CRYPTO_MAX_RSA_MODULUS_SIZE**: tanımlı, bu seçenek bit cinsinden beklenen maksimum RSA mod sayısını verir.</span><span class="sxs-lookup"><span data-stu-id="30dbe-126">**NX_CRYPTO_MAX_RSA_MODULUS_SIZE**: Defined, this option gives the maximum RSA modulus expected, in bits.</span></span> <span data-ttu-id="30dbe-127">4096 bit mod için varsayılan değer 4096 ' dir.</span><span class="sxs-lookup"><span data-stu-id="30dbe-127">The default value is 4096 for a 4096-bit modulus.</span></span> <span data-ttu-id="30dbe-128">Diğer değerler 3072, 2048 veya 1024 (önerilmez) olabilir.</span><span class="sxs-lookup"><span data-stu-id="30dbe-128">Other values can be 3072, 2048, or 1024 (not recommended).</span></span>
- <span data-ttu-id="30dbe-129">**NX_CRYPTO_FIPS**: tanımlı, bu seçenek FIPS-Compliant kullanımı için gerekli ek güvenlik özelliklerini sunar.</span><span class="sxs-lookup"><span data-stu-id="30dbe-129">**NX_CRYPTO_FIPS**: Defined, this option enables extra security features required for FIPS-Compliant usage.</span></span> <span data-ttu-id="30dbe-130">Bu seçenek FIPS olmayan derleme için etkinleştirilmemiş.</span><span class="sxs-lookup"><span data-stu-id="30dbe-130">This option is not enabled for non-FIPS build.</span></span>
- <span data-ttu-id="30dbe-131">**NX_CRYPTO_STANDALONE_ENABLE**: tanımlı, NETX şifrelemesi 'nin tek başına modda kullanılmasını sağlar (Azure RTOS olmadan).</span><span class="sxs-lookup"><span data-stu-id="30dbe-131">**NX_CRYPTO_STANDALONE_ENABLE**: Defined enables NetX Crypto to be used in standalone mode (without Azure RTOS).</span></span> <span data-ttu-id="30dbe-132">Varsayılan olarak bu simge tanımlı değildir.</span><span class="sxs-lookup"><span data-stu-id="30dbe-132">By default this symbol is not defined.</span></span>
