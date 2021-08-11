---
title: Bölüm 1-genel bakış
author: philmea
description: Bu makale, Azure RTOS ThreadX modüllerine genel bakış
ms.author: philmea
ms.date: 07/15/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 9018c10e6fe92b2237ec94b633f2f0030ad1cef4bcbcb7afa5ace20548f012ed
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116799446"
---
# <a name="chapter-1-overview"></a>Bölüm 1: genel bakış

ThreadX modülü bileşeni, uygulamaların, uygulamanın yerleşik bölümünden ayrı olarak oluşturulan modülleri dinamik olarak yüklemesi için bir altyapı sağlar. Bu, özellikle uygulama kodu boyutunun kullanılabilir belleği aşması durumunda faydalıdır. Ayrıca, çekirdek görüntü dağıtıldıktan sonra yeni özelliklerin eklenmesi gerektiği zaman da yardımcı olabilir. Bunlara ek olarak, kısmi bellenim güncelleştirmeleri gerektiğinde dinamik yükleme modülleri de kullanılabilir.

Yüklü modül için bellek koruması, modül girişi içinde belirtilen özelliklere göre isteğe bağlıdır. Bellek koruması belirtildiğinde, işlemcinin bellek yönetimi donanımı, modülün tüm iş parçacıklarının yalnızca modülün koduna ve veri belleğine erişimine izin verilen şekilde yapılandırılır. Herhangi bir gereksiz bellek erişimi veya yürütme, bellek hatasına neden olur ve sorunlu modül iş parçacığı sonlandırılır. Uygulama bir bellek hatası bildirimi geri çağırması kaydederse, bu da bellek hatasının uygulamasını uyarmak için de çağırılır.

ThreadX modülü bileşeni, modüllerin yüklenebildiği bir bellek alanı sağlamak için uygulamayı kullanır. Her modülün yönerge alanı yerinde çalıştırılabilir veya yürütme için RAM modülü bellek alanına kopyalanabilir. Her durumda, modül veri belleği gereksinimleri modül bellek alanından ayrılır.

Yerleşik modül yöneticisi kodunun yalnızca bir kopyası varken, aynı anda yüklenebilen modül sayısıyla ilgili hiçbir sınır yoktur (kullanılabilir bellek miktarı üzerinden). Şekil 1 ' de Modül Yöneticisi ve modüllerle ilişkili ilişki gösterilmektedir.

![Modüller ve Modül Yöneticisi Ilişkisi](media/image2.png)

**Şekil 1** Modüller ve Modül Yöneticisi

Her modülün, uygulamanın tanımlanması sorumluluğu olan kendi bellek alanı olması gerekir. Modül ve Modül Yöneticisi, modül tarafından istenen ThreadX hizmetlerine karşılık gelen önceden tanımlanmış istek kimlikleri aracılığıyla bir yazılım gönderme işlevi aracılığıyla etkileşim kurar. Ayrıca modül, tek bir iş parçacığı giriş noktası ve gerekli yığın boyutu, öncelik, modül KIMLIĞI, geri çağırma iş parçacığı yığın boyutu/öncelik vb. sağlamak için gereklidir. Bu bilgiler, her modülün girişi içinde tanımlanmıştır.

Modül Yöneticisi, ilk modül iş parçacığını oluşturmaktan ve yürütmesini başlatmaktan sorumludur. Modülün ilk iş parçacığı yürütüldükten sonra Modül Yöneticisi, modül tarafından yapılan tüm ThreadX API isteklerinin zincirinden sorumlu olur. Modül içinde ek iş parçacıkları oluşturma özelliği de dahil olmak üzere, bir modülün ThreadX API 'sine tam erişimi vardır.  
  
Modül kaynak kodu adlandırma kuralları basittir: tüm Modül Yöneticisi kaynak dosyaları ***txm_module_manager_ \**** olarak adlandırılır ve modülün tamamen ilişkili tüm dosyaları adın "**_Manager_*_" kısmını atlayın. Ana içerme dosyası _*_txm_module. h_** , yönetici ve modül kaynak kodu tarafından paylaşılır.
