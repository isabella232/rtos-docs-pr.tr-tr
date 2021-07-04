---
title: Bölüm 2 - NetX Şifrelemesi'Azure RTOS yükleme ve kullanma
description: Bu bölümde NetX Crypto bileşeninin yüklenmesi, kurulumu ve kullanımıyla ilgili çeşitli sorunların açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 3323af5eaf31ac9c167966522df6477c82e99fdc
ms.sourcegitcommit: c98e5360c9cedbe773af5a44f5163f563c85b570
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/24/2021
ms.locfileid: "110337015"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-crypto"></a><span data-ttu-id="e221a-103">Bölüm 2 - NetX Şifrelemesi'Azure RTOS yükleme ve kullanma</span><span class="sxs-lookup"><span data-stu-id="e221a-103">Chapter 2 - Installation and use of Azure RTOS NetX Crypto</span></span>

<span data-ttu-id="e221a-104">Bu bölümde, NetX Crypto bileşeninin yüklenmesi, Azure RTOS ve kullanımı açık almaktadır.</span><span class="sxs-lookup"><span data-stu-id="e221a-104">This chapter describes installation, setup, and usage of the Azure RTOS NetX Crypto component.</span></span>

## <a name="product-distribution"></a><span data-ttu-id="e221a-105">Ürün Dağıtımı</span><span class="sxs-lookup"><span data-stu-id="e221a-105">Product Distribution</span></span>

<span data-ttu-id="e221a-106">Azure RTOS NetX Şifrelemesi şu [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo) şekildedir: .</span><span class="sxs-lookup"><span data-stu-id="e221a-106">Azure RTOS NetX Crypto is available at [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo).</span></span> <span data-ttu-id="e221a-107">Paket kaynak dosyaları, ekleme dosyalarını ve bu belgeyi içeren bir PDF dosyasını aşağıdaki gibi içerir:</span><span class="sxs-lookup"><span data-stu-id="e221a-107">The package includes source files, include files, and a PDF file that contains this document, as follows:</span></span>

- <span data-ttu-id="e221a-108">**nx_crypto.h:** Genel API üst bilgi dosyası NetX Şifreleme modülü</span><span class="sxs-lookup"><span data-stu-id="e221a-108">**nx_crypto.h**: Public API header file NetX Crypto module</span></span>
- <span data-ttu-id="e221a-109">**nx_crypto_\*.c/h:** NetX Crypto için C/H Kaynak dosyaları</span><span class="sxs-lookup"><span data-stu-id="e221a-109">**nx_crypto_\*.c/h**: C/H Source files for NetX Crypto</span></span>
- <span data-ttu-id="e221a-110">**nx_crypto_port.h:** Tüm geliştirme aracını içeren ve belirli veri tanımlarını ve yapılarını hedef alan C üst bilgi dosyası.</span><span class="sxs-lookup"><span data-stu-id="e221a-110">**nx_crypto_port.h**: C header file containing all development-tool and target specific data definitions and structures.</span></span>
- <span data-ttu-id="e221a-111">**NetX_Crypto_User_Guide.pdf:** NetX Şifreleme Modülünün PDF açıklaması.</span><span class="sxs-lookup"><span data-stu-id="e221a-111">**NetX_Crypto_User_Guide.pdf**: PDF description of NetX Crypto Module.</span></span>

## <a name="netx-crypto-installation"></a><span data-ttu-id="e221a-112">NetX Şifreleme Yüklemesi</span><span class="sxs-lookup"><span data-stu-id="e221a-112">NetX Crypto Installation</span></span>

<span data-ttu-id="e221a-113">Daha önce bahsedilen dağıtımın tamamı **NetX** Duo crypto_libraries kök düzeyinde mevcut olan bir dizinde mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="e221a-113">The entire distribution mentioned previously is available in **crypto_libraries** directory, present at root level of NetX Duo repository.</span></span>

<span data-ttu-id="e221a-114">NetX Şifrelemesini kullanmak için, daha önce bahsedilen dağıtımın tamamı NetX'in yüklü olduğu dizin düzeyine kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="e221a-114">In order to use NetX Crypto, the entire distribution mentioned previously should be copied to the same directory level where NetX is installed.</span></span> <span data-ttu-id="e221a-115">Örneğin, "\threadx\arm7\NetX" dizininde NetX yüklüyse,*nx_crypto.*</span><span class="sxs-lookup"><span data-stu-id="e221a-115">For example, if NetX is installed in the directory "\threadx\arm7\NetX" then the nx_crypto *.*</span></span> <span data-ttu-id="e221a-116">dizinleri "\threadx\arm7\NetXCrypto" dizinine kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="e221a-116">directories should be copied into "\threadx\arm7\NetXCrypto".</span></span>

<span data-ttu-id="e221a-117">NetX Şifrelemesi'nin tek başına modda kullanılası için, daha önce bahsedilen dağıtımın tamamı uygulama projesine kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="e221a-117">For NetX Crypto to be used in standalone mode, the entire distribution mentioned previously should be copied to the application project.</span></span> <span data-ttu-id="e221a-118">Örneğin **crypto_libraries** bir dizin uygulama projesine kopyalanmış olmalı veya crypto_libraries dizini olan **bir kitaplık** projesi oluşturularak uygulama projesine bağlan olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e221a-118">For example **crypto_libraries** directory should be copied to the application project or a library project with **crypto_libraries** directory should be created and linked to the application project.</span></span> 

## <a name="using-netx-crypto"></a><span data-ttu-id="e221a-119">NetX Şifrelemesi Kullanma</span><span class="sxs-lookup"><span data-stu-id="e221a-119">Using NetX Crypto</span></span>

<span data-ttu-id="e221a-120">Uygulama kodunun *nx_crypto.h içermesi gerekir.*</span><span class="sxs-lookup"><span data-stu-id="e221a-120">The application code must include the *nx_crypto.h*.</span></span>  <span data-ttu-id="e221a-121">Uygulama *nx_crypto.h* ekli olduktan sonra, uygulama kodu bu kılavuzun devamlarında belirtilen NetX Crypto işlev çağrılarını mümkün hale gelir.</span><span class="sxs-lookup"><span data-stu-id="e221a-121">Once *nx_crypto.h* is included, the application code is then able to make the NetX Crypto function calls specified later in this guide.</span></span>

## <a name="configuration-options"></a><span data-ttu-id="e221a-122">Yapılandırma Seçenekleri</span><span class="sxs-lookup"><span data-stu-id="e221a-122">Configuration Options</span></span>

<span data-ttu-id="e221a-123">NetX Şifrelemesi'nin inşası için çeşitli yapılandırma seçenekleri vardır.</span><span class="sxs-lookup"><span data-stu-id="e221a-123">There are several configuration options for building NetX Crypto.</span></span> <span data-ttu-id="e221a-124">Aşağıda, her biri ayrıntılı olarak açıklanan tüm seçeneklerin listesi velanmıştır:</span><span class="sxs-lookup"><span data-stu-id="e221a-124">Following is a list of all options, where each is described in detail:</span></span>

- <span data-ttu-id="e221a-125">**NX_CRYPTO_MAX_RSA_MODULUS_SIZE:** Tanımlanan, bu seçenek bit olarak beklenen en fazla RSA modu sağlar.</span><span class="sxs-lookup"><span data-stu-id="e221a-125">**NX_CRYPTO_MAX_RSA_MODULUS_SIZE**: Defined, this option gives the maximum RSA modulus expected, in bits.</span></span> <span data-ttu-id="e221a-126">Varsayılan değer 4096 bit mod için 4096'dır.</span><span class="sxs-lookup"><span data-stu-id="e221a-126">The default value is 4096 for a 4096-bit modulus.</span></span> <span data-ttu-id="e221a-127">Diğer değerler 3072, 2048 veya 1024 olabilir (önerilmez).</span><span class="sxs-lookup"><span data-stu-id="e221a-127">Other values can be 3072, 2048, or 1024 (not recommended).</span></span>
- <span data-ttu-id="e221a-128">**NX_CRYPTO_SELF_TEST:** Tanımlandı, NetX Şifreleme modülü için kendi kendine testlere olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="e221a-128">**NX_CRYPTO_SELF_TEST**: Defined, enables self tests for NetX Crypto module.</span></span> <span data-ttu-id="e221a-129">**NX_CRYPTO_FIPS** simgesi artık kullanım dışı bırakıldı ve yeniden **adlandırıldı NX_CRYPTO_SELF_TEST**</span><span class="sxs-lookup"><span data-stu-id="e221a-129">**NX_CRYPTO_FIPS** symbol is now deprecated and renamed to **NX_CRYPTO_SELF_TEST**</span></span>
- <span data-ttu-id="e221a-130">**NX_CRYPTO_STANDALONE_ENABLE:** Tanımlı, NetX Şifrelemesi'nin tek başına modda (tek başına şifreleme olmadan) Azure RTOS.</span><span class="sxs-lookup"><span data-stu-id="e221a-130">**NX_CRYPTO_STANDALONE_ENABLE**: Defined enables NetX Crypto to be used in standalone mode (without Azure RTOS).</span></span> <span data-ttu-id="e221a-131">Varsayılan olarak bu simge tanımlanmamıştır.</span><span class="sxs-lookup"><span data-stu-id="e221a-131">By default this symbol is not defined.</span></span>
