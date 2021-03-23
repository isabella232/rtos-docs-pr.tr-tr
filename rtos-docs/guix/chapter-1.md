---
title: Bölüm 1-Gux 'e giriş
description: GUX, katıştırılmış Azure RTOS ThreadX tabanlı uygulamalar için özel olarak tasarlanan (GUI) yüksek performanslı gerçek zamanlı bir uygulamasıdır.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: b90da988a03d59b1bca3f5584164d641bef96454
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104827203"
---
# <a name="chapter-1---introduction-to-azure-rtos-guix"></a>Bölüm 1-Azure RTOS Gux 'e giriş

Azure RTOS Gux (GUıDX), katıştırılmış ThreadX tabanlı uygulamalar için özel olarak tasarlanmış bir grafik arabirimi çerçevesinin yüksek performanslı gerçek zamanlı uygulamasıdır. Bu bölümde, GUıDX 'e giriş ve uygulamalarının ve avantajlarının açıklaması yer almaktadır.

## <a name="guix-feature-overview"></a>GUX özelliğine genel bakış

Diğer birçok GUI uygulamasının aksine, GUıDX, küçük mikro denetleyicideki uygulamalardan güçlü RıSC ve DSP işlemcileri kullanan uygulamalara kolayca ölçeklendirerek çok yönlü olacak şekilde tasarlanmıştır. Bu, başlangıçta iş istasyonu ortamları için tasarlanan, ancak ekli tasarımlara sıkıştırılan genel etki alanı veya diğer ticari uygulamalar için keskin karşıtlığa sahiptir. GUX özelliklerine genel bakış aşağıda verilmiştir:

- Ana bilgisayar tabanlı tasarım aracı Gux Studio ile kullanımı kolay

- Tam barındırılan prototipleme için Win32 Gux çalışma zamanı ortamı

- , ThreadX tarafından desteklenen işlemcilerin çoğunu destekler

- Yalnızca ANSI C 'de yazılmış

- Endian nötr

- En küçük, Faücretli katıştırılmış GUI

- Çalışma zamanı yapılandırılabilir, nesne sayısı, ekran boyutu vb.

- Kolay yazma ekran sürücüsü arabirimi

- Renk (32-BPP renk derinliğine kadar), tek renkli ve gri tonlamalı destek

- UTF8 dize kodlaması ve dize kaynakları aracılığıyla çok dilli destek

- Varsayılan ücretsiz yazı tipleri ve yeni yazı tipi ekleme kolay

- Çeşitli boyutlarda birden çok çizim desteklenir

- Farklı boyutlarda birden çok ekran ve renk derinlikleri desteklenir

- Ekran geçiş desteği (belirme, soluklaştırma, çekme vb.)

- Dokunmatik ekran, hareket ve sanal klavye desteği

- Bit eşlem sıkıştırması

- Alfa karıştırma desteği

- Titreme desteği

- Kenar yumuşatma desteği

- Kaplama ve Temalar

- Tuval karışımı

- Tüm pencere yönetimi

  - Üst/alt öğe Ilişkisi

  - Dinamik oluşturma, silme, yeniden boyutlandırma, taşıma
  - Ayrı olay işleme ve çizim 
  - Z-düzeni
  - Kırpma ve görünümler

- Kapsamlı pencere öğeleri kümesi

  - Çeşitli düğme türleri, sürgüler ve çevirmeler

  - Açılan liste
  
  - İstem

  - Çok satırlı metin görünümü
  
  - Tek ve çok satırlı metin girişi
  
  - Sayısal ve metin kaydırma tekerlekleri
  
  - Pencereler ve kaydırma çubukları
  
  - Radyal Ilerleme çubuğu
  
  - Öğesini

### <a name="ansi-c-source-code"></a>ANSI C kaynak kodu

GUX, ANSI C 'de tamamen yazılır ve doğrudan bir ANSI C derleyicisi ve ThreadX desteği olan tüm işlemci mimarisine taşınabilir. ANSI C 'de yazılmış olsa da, GUıDX, nesne odaklı bir model ve devralma kullanır.

### <a name="not-a-black-box"></a>Siyah kutu değil

GUX dağıtımların çoğu, tüm C kaynak kodunu içerir. Bu, birçok ticari GUI uygulamalarıyla oluşan "kara kutu" sorunlarını ortadan kaldırır. GUX kullanarak uygulamalar, GUI 'nin neler yaptığını tam olarak görebilir, hiçbir gizleyebilmekte!

Kaynak kodun olması, uygulamaya özgü değişikliklere de izin verir. Önerilmese de, gerekli olduğunda GUI 'yi değiştirme imkanına kesinlikle yarar vardır. Bu özellikler özellikle, şirket içi veya genel etki alanı ürünleriyle çalışmaya alışkın olan geliştiricilere Comforting. Bunlar, kaynak kodu ve değişiklik yapabilme yeteneğinin olmasını bekler. GUX, bu tür geliştiriciler için en üstün GUI yazılımıdır.

## <a name="embedded-gui-applications"></a>Katıştırılmış GUI uygulamaları

Katıştırılmış GUI uygulamaları, bir kullanıcı arabirimi gereksinimi olan ve cep telefonları, iletişim donatımı, oto motor, lazer yazıcılar, tıbbi cihazlar vb. gibi ürünlerin içinde gizlenen mikro işlemcilerde yürütülen uygulamalardır. Bu uygulamalarda neredeyse her zaman bazı bellek ve performans kısıtlamaları vardır. Katıştırılmış GUI 'ye yönelik başka bir ayrım, yazılım ve donanımının özel bir amaca sahip olması olabilir.

### <a name="real-time-gui-software"></a>Gerçek zamanlı GUI yazılımı

Temelde, işlemesini tam bir süre içinde gerçekleştirmesi gereken GUI yazılımına *gerçek ZAMANLı GUI* yazılımı denır ve GUI uygulamalarına zaman kısıtlamaları eklendiğinde bunlar gerçek zamanlı uygulamalar olarak sınıflandırılır. Gömülü GUI uygulamaları, dış dünyada kendi kendine ait etkileşimlerinden dolayı neredeyse her zaman gerçek zamanlı olarak gerçekleştirilir.

## <a name="guix-benefits"></a>GUX avantajları

Ekli uygulamalar için Gux kullanmanın başlıca avantajları yüksek performanslı, özellik açısından zengin ve çok küçük bellek gereksinimleridir. GUX, yüksek performanslı, çok görevli Azure RTOS ThreadX gerçek zamanlı işletim sistemiyle tamamen tümleşiktir.

### <a name="improved-responsiveness"></a>İyileştirilmiş yanıt hızı

Yüksek performanslı Gux ürünü, uygulamaların daha önce hiç olmadığı kadar hızlı yanıt vermesini sağlar. Bu, özellikle önemli miktarda görsel bilgi veya bu tür bilgileri görüntülemek için katı zamanlama gereksinimlerine sahip olan katıştırılmış uygulamalar için önemlidir.

### <a name="software-maintenance"></a>Yazılım Bakımı

GUIX kullanmak, geliştiricilerin katıştırılmış uygulamalarının GUI yönlerini kolayca bölümlememesini sağlar. Bu bölümlendirme, tüm geliştirme sürecini kolaylaştırır ve gelecekteki yazılım bakımını önemli ölçüde geliştirir.

### <a name="increased-throughput"></a>Artan verimlilik

GUX, doğrudan katıştırılmış uygulamaya aktarılan en yüksek performanslı GUI 'yi sağlar. GUX uygulamaları, Kullanıcı arabirimi bilgilerini Gux olmayan uygulamalardan daha hızlı işleyebilir!

### <a name="processor-isolation"></a>İşlemci yalıtımı

GUIX, uygulama ile temel alınan işlemci ve görüntüleme donanımı arasında sağlam, işlemciye sahip bir arabirim sağlar. Bu, geliştiricilerin, ekran donanımı sorunlarıyla ilgili ek süre harcamak yerine, Kullanıcı arabiriminin üst düzey yönlerini yoğunlaşmasını sağlar.

### <a name="ease-of-use"></a>Kullanım kolaylığı

GUX, uygulama geliştiricisi göz önünde bulundurularak tasarlanmıştır. GUX mimarisi ve hizmet çağrısı arabiriminin anlaşılması kolaydır. Sonuç olarak, GUıDX geliştiricileri gelişmiş özelliklerini hızlı bir şekilde kullanabilir.

### <a name="improve-time-to-market"></a>Pazara ulaşma süresini iyileştirme

GUX 'in güçlü özellikleri yazılım geliştirme sürecini hızlandırır. GUX, çoğu işlemciyi soyutlar ve donanım sorunlarını görüntüler, böylece bu konular uygulama kullanıcı arabirimi uygulamasının çoğunluğunda kaldırılır. Bu özellik, kullanımı kolaylaştırma ve gelişmiş özellik kümesiyle birlikte, pazara daha hızlı bir süre içinde sonuçlanır!

### <a name="protecting-the-software-investment"></a>Yazılım yatırımınızı koruma

GUX, ANSI C 'de özel olarak yazılır ve Azure RTOS ThreadX gerçek zamanlı işletim sistemiyle tamamen tümleşiktir. Bu, Gux uygulamalarının tüm ThreadX desteklenen işlemcilere anında taşınabilir olduğunu gösterir. Daha iyi bir şekilde, her hafta için ThreadX ile tamamen yeni bir işlemci mimarisi desteklenebilir. Sonuç olarak, GUıDX kullanılması uygulamanın geçiş yolunu sağlar ve orijinal geliştirme yatırımını korur.
