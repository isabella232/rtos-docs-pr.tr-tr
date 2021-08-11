---
title: Ek C-DOS komut satırı yardımcı programları
description: Azure RTOS TraceX yüklemesinde yardımcı alt dizin altında bulunan üç DOS komut satırı yardımcı programı vardır.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: 1a89f8be7e21e416659b904f0ec5b2a3a8f666cdb9a861786e652a38564db48f
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116791559"
---
# <a name="appendix-c---dos-command-line-utilities"></a>Ek C-DOS komut satırı yardımcı programları

Trackingex yüklemesinde, ***Utilities*** alt dizininde bulunan üç DOS komut satırı yardımcı programı vardır.

Sağlanan yardımcı programlar aşağıda listelenmiştir:

| **Yardımcı Program**                              | **Amaç**                               | **Komut satırı tanımları** |
| -------------------------------- | ----------------------------------------- | ---------------------------- |
| **ea2tracex.exe**                | Original_file Association of ThreadX tarafından oluşturulan izleme dosyasını, GHS araçları converted_file TraceX izleme dosyası biçimine dönüştürür. Gana için ThreadX araçları, Gana olmayan araçlar için ThreadX 'den farklı bir izleme biçimi üretir, bu da bu dönüştürme yardımcı programının bu nedenle gereklidir. | ``` > eatracex original_file converted_file <cr> ``` | 
**hex2tracex.exe** | ThreadX tarafından oluşturulan bir izleme dosyasını, Intel ONALTıLı biçimindeki geliştirme aracından ikili TraceX izleme dosyası biçimine dönüştürür. TraceX v5 ve üzeri, ONALTıLıK dosyaları dönüştürmeden açabilir. | ``` hex2tracex hex_file converted_file <cr> ``` | 
**mot2tracex.exe** | ThreadX tarafından oluşturulan bir izleme dosyasını, Motorola S-kayıt biçimindeki geliştirme aracından ikili TraceX izleme dosyası biçimine dönüştürür. TraceX v5 ve üzeri, dosyaları dönüştürmeden S-kayıt dosyaları açabilir. | ``` > mot2tracex mot_file converted_file <cr> ```|