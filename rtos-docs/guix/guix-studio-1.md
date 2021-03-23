---
title: GUX Studio Kullanıcı Kılavuzu
description: Bu kılavuz, Microsoft 'un Gux çalışma zamanı kitaplığı için özel olarak tasarlanan Microsoft Windows tabanlı Hızlı Kullanıcı arabirimi geliştirme ortamı olan Gux Studio hakkında kapsamlı bilgiler sağlar.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 6a5d628581d4c6b44ff093bac45790d6e2755349
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104827172"
---
# <a name="chapter-1-introduction-to-azure-rtos-guix-studio"></a><span data-ttu-id="32a74-103">Bölüm 1: Azure RTOS Gux Studio 'ya giriş</span><span class="sxs-lookup"><span data-stu-id="32a74-103">Chapter 1: Introduction to Azure RTOS GUIX Studio</span></span>

<span data-ttu-id="32a74-104">Azure RTOS Gux Studio, Microsoft 'un Gux çalışma zamanı kitaplığı için özel olarak tasarlanan Microsoft Windows tabanlı bir hızlı UI geliştirme ortamıdır.</span><span class="sxs-lookup"><span data-stu-id="32a74-104">Azure RTOS GUIX Studio is a Microsoft Windows-based rapid UI development environment specifically designed for the GUIX runtime library from Microsoft.</span></span>

<span data-ttu-id="32a74-105">Ekli UI geliştiricileri, Gux çalışma zamanı ortamını kullanarak kendi yerleşik kullanıcı arabirimini hızlıca oluşturmak ve güncelleştirmek için Gux Studio WYSıWYG ekran Tasarımcısı ' nı kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="32a74-105">Embedded UI Developers can utilize the GUIX Studio WYSIWYG screen designer to quickly create and update their embedded UI using the GUIX run-time environment.</span></span> <span data-ttu-id="32a74-106">GUX Studio tasarımları,. GXP uzantısına sahip bir Gux Studio proje dosyasında kaydedilir ve saklanır.</span><span class="sxs-lookup"><span data-stu-id="32a74-106">GUIX Studio designs are saved and maintained in a GUIX Studio project file, which has the extension .gxp.</span></span> <span data-ttu-id="32a74-107">Tasarımınız hedefte yürütmeye hazırsa, GUıDX Studio tüm gerekli Kullanıcı arabirimi bilgilerini ve kodu içeren C kodu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="32a74-107">When your design is ready for execution on the target, GUIX Studio generates C code that contains all the necessary UI information and code.</span></span>

## <a name="guix-studio-requirements"></a><span data-ttu-id="32a74-108">GUX Studio gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="32a74-108">GUIX Studio Requirements</span></span>

<span data-ttu-id="32a74-109">Microsoft 'un Gux Studio 'nun düzgün çalışması için *WINDOWS XP* (veya üzeri) gerekir.</span><span class="sxs-lookup"><span data-stu-id="32a74-109">In order to function properly, Microsoft's GUIX Studio requires *Windows XP* (or above).</span></span> <span data-ttu-id="32a74-110">Sistemde en az 200 MB RAM, 2 GB kullanılabilir sabit disk alanı ve en az 256 renk içeren 1024x768 ekran görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="32a74-110">The system should have a minimum of 200MB of RAM, 2GB of available hard-disk space, and a minimum display of 1024x768 with 256 colors.</span></span> <span data-ttu-id="32a74-111">Ayrıca, ekli uygulamanın *threadx/Gux v 6.0* veya sonraki sürümlerinde çalışıyor olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="32a74-111">In addition, the embedded application must be running on *ThreadX/GUIX V6.0* or later.</span></span>

<span data-ttu-id="32a74-112">Katıştırılmış UI uygulamasını bağımsız bir Microsoft Windows yürütülebilir dosyası olarak derleyip çalıştırmak istiyorsanız, bir Microsoft Windows yürütülebilir dosyası üretmek için C kaynak kodu derlenebilecek bir derleyici veya yapı ortamı da gerekir.</span><span class="sxs-lookup"><span data-stu-id="32a74-112">If you would like to be able to build and run the embedded UI application as a stand-alone Microsoft Windows executable, you will also need a compiler or build environment capable of compiling C source code to produce a Microsoft Windows executable.</span></span> <span data-ttu-id="32a74-113">GUX Studio 'Ya dahil edilen değerlendirme paketi ayrıca, Visual Studio 2019 uyumlu proje dosyalarını ve sağlanan her bir örnek uygulama için çözümleri içerir.</span><span class="sxs-lookup"><span data-stu-id="32a74-113">The evaluation package included with GUIX Studio also includes Visual Studio 2019 compatible project files and solutions for each of the provided example applications.</span></span> <span data-ttu-id="32a74-114">Farklı bir derleyici kullanıyorsanız, kendi proje dosyalarınızı oluşturmanız veya örnek uygulamalarınızı oluşturma amacıyla dosyaları yapmanız veya ' de desteğe başvurmanız gerekir https://aka.ms/azrtos-support .</span><span class="sxs-lookup"><span data-stu-id="32a74-114">If you are using a different compiler, you will need to create your own project files or make files for the purposes of building your example applications, or contact support at https://aka.ms/azrtos-support.</span></span>

## <a name="guix-studio-constraints"></a><span data-ttu-id="32a74-115">GUX Studio kısıtlamaları</span><span class="sxs-lookup"><span data-stu-id="32a74-115">GUIX Studio Constraints</span></span>

<span data-ttu-id="32a74-116">GUX Studio UI tasarım aracında aşağıdaki gibi çeşitli kısıtlamalar vardır:</span><span class="sxs-lookup"><span data-stu-id="32a74-116">The GUIX Studio UI design tool has several constraints, as follows:</span></span>

- <span data-ttu-id="32a74-117">Proje başına en fazla 4 ekran görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="32a74-117">A maximum of 4 displays per project.</span></span>
- <span data-ttu-id="32a74-118">GUX Studio projesi başına en fazla 100.000 pencere öğesi.</span><span class="sxs-lookup"><span data-stu-id="32a74-118">A maximum of 100,000 widgets per GUIX Studio project.</span></span>
- <span data-ttu-id="32a74-119">En fazla 100.000 farklı kaynak, örneğin, renkler, yazı tipleri, pixelmaps, dizeler vb.</span><span class="sxs-lookup"><span data-stu-id="32a74-119">A maximum of 100,000 distinct resources, e.g., colors, fonts, pixelmaps, strings, etc.</span></span>