---
title: GUX Studio komut satırı
description: GUX Studio, Studio tarafından oluşturulan çıkış dosyalarını güncelleştirmek için gereken derleme işlem hatları için yararlı olan komut satırı çağrısı sağlar.
author: jdeere5220
ms.author: kemaxwel
ms.date: 9/30/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 9f9bfc67c524a77b5bf736407bf2ca372ce98308
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826291"
---
# <a name="chapter-9-guix-studio-command-line"></a><span data-ttu-id="d21b8-103">Bölüm 9: Gux Studio komut satırı</span><span class="sxs-lookup"><span data-stu-id="d21b8-103">Chapter 9: GUIX Studio Command Line</span></span>

<span data-ttu-id="d21b8-104">GUX Studio, Studio tarafından oluşturulan çıkış dosyalarının güncelleştirilmesi için gereken derleme işlem hatları için yararlı olan komut satırı çağrısını destekler.</span><span class="sxs-lookup"><span data-stu-id="d21b8-104">GUIX Studio supports command-line invocation,  which is useful for build pipelines that are required to update of the Studio-generated output files.</span></span>

## <a name="command-line-usage"></a><span data-ttu-id="d21b8-105">Command-Line kullanımı</span><span class="sxs-lookup"><span data-stu-id="d21b8-105">Command-Line Usage</span></span>

<span data-ttu-id="d21b8-106">**Kullanım:** guix_studio \[ seçenek \] \[ bağımsız değişkeni\]</span><span class="sxs-lookup"><span data-stu-id="d21b8-106">**Usage:** guix_studio \[OPTION\] \[ARGUMENT\]</span></span>

<span data-ttu-id="d21b8-107">*. GXP* projesini açın.</span><span class="sxs-lookup"><span data-stu-id="d21b8-107">Open the *.gxp* project.</span></span>

<span data-ttu-id="d21b8-108">Studio projesini açın ve istenen çıktı dosyalarını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d21b8-108">Open the Studio project and generate desired output files.</span></span>


<span data-ttu-id="d21b8-109">**Örnekler:**</span><span class="sxs-lookup"><span data-stu-id="d21b8-109">**Examples:**</span></span>

`guix_studio demo.gxp`  
<span data-ttu-id="d21b8-110">"Demo. GXP" projesini aç</span><span class="sxs-lookup"><span data-stu-id="d21b8-110">Open "demo.gxp" project</span></span>


`guix_studio.exe –p demo.gxp`  
<span data-ttu-id="d21b8-111">"Demo. GXP" projesini aç</span><span class="sxs-lookup"><span data-stu-id="d21b8-111">Open "demo.gxp" project</span></span>


`guix_studio.exe –n –p demo.gxp`  
<span data-ttu-id="d21b8-112">Demo. GXP projesinin tüm çıkış dosyalarını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d21b8-112">Generate all output files of demo.gxp project.</span></span>

`guix_studio.exe –n –r –p demo.gxp`  
<span data-ttu-id="d21b8-113">Demo. GXP projesinin kaynak dosyalarını oluşturma</span><span class="sxs-lookup"><span data-stu-id="d21b8-113">Generate resource files of demo.gxp project</span></span>


## <a name="command-line-options"></a><span data-ttu-id="d21b8-114">Command-Line seçenekleri</span><span class="sxs-lookup"><span data-stu-id="d21b8-114">Command-Line Options</span></span>

```C
***-n --nogui***  
```

<span data-ttu-id="d21b8-115">"Noguı" seçeneği.</span><span class="sxs-lookup"><span data-stu-id="d21b8-115">The "nogui" option.</span></span> <span data-ttu-id="d21b8-116">GUX Studio 'Yu Pencereleme Kullanıcı arabirimi arabirimini başlatmadan çalıştırmayı söyleyin.</span><span class="sxs-lookup"><span data-stu-id="d21b8-116">Tell GUIX Studio to run without starting the windowing UI interface.</span></span>

```C
***-o pathname***  
***--log***  
```

<span data-ttu-id="d21b8-117">Günlük seçeneği, bir günlük dosyası belirtin.</span><span class="sxs-lookup"><span data-stu-id="d21b8-117">Log option, specify a log file.</span></span>

```C
***-b***  
***--binary***  
```

<span data-ttu-id="d21b8-118">İkili kaynak seçeneği.</span><span class="sxs-lookup"><span data-stu-id="d21b8-118">Binary resource option.</span></span> <span data-ttu-id="d21b8-119">C dosyası yerine bir ikili kaynak dosyası üretir.</span><span class="sxs-lookup"><span data-stu-id="d21b8-119">Produces a binary resource file rather than a C file.</span></span>

```C
***-d display1, display2***  
***--display***  
```

<span data-ttu-id="d21b8-120">Adları görüntüle seçeneği.</span><span class="sxs-lookup"><span data-stu-id="d21b8-120">Display names option.</span></span> <span data-ttu-id="d21b8-121">Bu seçenek kullanılırsa, oluşturulan herhangi bir kaynak veya belirtim dosyasına yalnızca belirtilen görünen adlar dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="d21b8-121">If this option is used, then only the specified display names are included in any generated resource or specification files.</span></span> <span data-ttu-id="d21b8-122">Bu seçenek kullanılmazsa, tüm ekranlar dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="d21b8-122">If this option is not used,  all displays are included.</span></span>

```C
***-t theme1, theme2***  
***--theme***  
```

<span data-ttu-id="d21b8-123">Tema adı (ler) seçeneği.</span><span class="sxs-lookup"><span data-stu-id="d21b8-123">Theme name(s) option.</span></span> <span data-ttu-id="d21b8-124">Bu seçenek kullanılırsa, oluşturulan herhangi bir kaynak veya belirtim dosyasına yalnızca belirtilen Tema adları eklenir.</span><span class="sxs-lookup"><span data-stu-id="d21b8-124">If this option is used, then only the specified theme names are included in any generated resource or specification files.</span></span> <span data-ttu-id="d21b8-125">Bu seçenek kullanılmazsa, tüm temalar dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="d21b8-125">If this option is not used, all themes are included.</span></span>

```C
***-l langage1, language2***  
***--language***  
```

<span data-ttu-id="d21b8-126">Dil adı (ler) seçeneği.</span><span class="sxs-lookup"><span data-stu-id="d21b8-126">Language name(s) option.</span></span> <span data-ttu-id="d21b8-127">Bu seçenek kullanılırsa, belirtilen dil adları oluşturulan kaynak veya belirtim dosyalarına dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="d21b8-127">If this option is used,  the specified language names are included in the generated resource or specification files.</span></span> <span data-ttu-id="d21b8-128">Aksi takdirde tüm dil adları dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="d21b8-128">Otherwise all language names are included.</span></span>

```C
***-r [filename]***  
***--resource***  
```

<span data-ttu-id="d21b8-129">Kaynak seçeneği, Studio 'Nun önceden belirlenen görüntüler, Temalar ve diller için bir kaynak dosyası üretmesi gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="d21b8-129">The resource option, specifies that Studio should produce a resource file for previously designated display(s), theme(s), and language(s).</span></span>

```C
***-s [filename]***  
***--specification***  
```

<span data-ttu-id="d21b8-130">Belirtim seçeneği, Studio 'nun belirtilen görüntü, tema ve dil için bir belirtim dosyası üretmesi gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="d21b8-130">The specification option, specify that studio should produce a specification file for designated display(s), theme(s), and language(s).</span></span>

```C
***-p project_pathname***  
***--project***  
```

<span data-ttu-id="d21b8-131">Proje yol adı seçeneği, yüklenecek örnek projeyi belirtin.</span><span class="sxs-lookup"><span data-stu-id="d21b8-131">Project pathname option, specify the example project to be loaded.</span></span>

```C
***-i [pathname]***  
***--import***  
```

<span data-ttu-id="d21b8-132">Dizeyi XLIFF veya CSV biçim dosyasından içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="d21b8-132">Import string from xliff or csv format file.</span></span>

<span data-ttu-id="d21b8-133">***--big_endian***</span><span class="sxs-lookup"><span data-stu-id="d21b8-133">***--big_endian***</span></span>  
<span data-ttu-id="d21b8-134">Büyük endian biçiminde kaynak verileri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d21b8-134">Generate resource data in big-endian format.</span></span>
