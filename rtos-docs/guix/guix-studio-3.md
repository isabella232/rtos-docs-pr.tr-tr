---
title: GUX Studio açıklaması
description: Bu bölüm, GUıDX Studio Sistem Analizi aracının bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 89bbcd51c22dddef6e420750e8c8805a66344335
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826369"
---
# <a name="chapter-3-description-of-guix-studio"></a>Bölüm 3: Gux Studio 'nun açıklaması

Bu bölüm, GUıDX Studio Sistem Analizi aracının bir açıklamasını içerir. Bu bölümde GUI 'nin Genel işlevselliğinin açıklaması bulunur. 

## <a name="guix-studio-views"></a>GUX Studio görünümleri

"**Toolbar** _, _*_proje görünümü_*_, _*_Özellikler görünümü_*_, _*_hedef görünümü_*_ ve _*_kaynak görünümü_*_ gibi, guıdx Studio Kullanıcı arabiriminin beş ana alanı vardır. _ *_Şekil 2_** temel Gux STUDIO Kullanıcı arabirimini gösterir. Görünümlerin her biri, aşağıdaki alt bölümlerde daha ayrıntılı bir şekilde ele alınmıştır.

![Temel Gux Studio Kullanıcı arabiriminin ekran görüntüsü.](./media/guix-studio/image_10.png)

**Şekil 2**

### <a name="title"></a>Başlık

- GUX Studio 18: ***title** _, şu anda _ *_Şekil 2_** ' nin en üstünde gösterildiği gibi, açık projenin yanı sıra Gux Studio sürümünü de görüntüler.

### <a name="toolbar"></a>Araç Çubuğu

***Toolbar** _, _ *_Şekil 3_* * ' de gösterildiği gibi, Gux Studio geliştiricisi için kullanılabilen düğmeleri gösterir.

![GUX Studio Toolbar 'ın ekran görüntüsü.](./media/guix-studio/image11.jpg)

**Şekil 3**

Araç çubuğu düğmeleri aşağıdaki gibi tanımlanır:

![Yeni düğmesi](./media/guix-studio/new-button.png) Yeni bir Gux Studio projesi oluşturur

![Aç düğmesi](./media/guix-studio/open-button.png) Mevcut bir Gux Studio projesini açar

![Kaydet düğmesi](./media/guix-studio/save-button.png) Projeyi kaydeder

![Kes düğmesi](./media/guix-studio/cut-button.png) Alt öğeleri içeren seçili pencere öğesini kes

![Kopyala düğmesini](./media/guix-studio/copy-button.png) Alt öğeler de dahil olmak üzere seçili pencere öğesini Kopyala

![Yapıştır düğmesi](./media/guix-studio/paste-button.png) Pencere öğesini ve alt öğeleri Yapıştır

![Sola Hizala düğmesi](./media/guix-studio/left-align-button.png) Seçili pencere öğelerini Sola Hizala

![Sağa Hizala düğmesi](./media/guix-studio/right-align-button.png) Seçili pencere öğelerini Sağa Hizala

![Üste Hizala düğmesi](./media/guix-studio/top-align-button.png) Seçili pencere öğelerini Üste Hizala

![Alt hizalama düğmesi](./media/guix-studio/bottom-align-button.png) Seçili pencere öğelerini Alta Hizala

![Dikey boşluk düğmesi](./media/guix-studio/space-vertically-button.png) Seçilen pencere öğelerini dikey olarak eşit alan

![Yatay boşluk düğmesi](./media/guix-studio/space-horizontally-button.png) Seçilen pencere öğelerini yatay olarak eşit alan

![Eşit genişlik düğmesi](./media/guix-studio/equal-width-button.png) Seçili pencere öğelerini eşit genişliğe getir

![Eşit yükseklik düğmesi](./media/guix-studio/equal-height-button.png) Seçili Pencere öğelerinin yüksekliğini eşit yap

![Öne taşı düğmesi](./media/guix-studio/move-front-button.png) Seçili pencere öğelerini öne taşı

![Geri taşı düğmesi](./media/guix-studio/move-back-button.png) Seçili pencere öğelerini arkaya taşı

![Boyut düğmesi](./media/guix-studio/size-button.png) Seçilen pencere öğesini içerik yakınlaştırma hedef ekranına Boyutlandır

![Uzaklaştır düğmesi](./media/guix-studio/zoom-out-button.png) Hedef ekranı uzaklaştır

![Yakınlaştır düğmesi](./media/guix-studio/zoom-in-button.png) Hedef ekranda Yakınlaştır

![Kaydet düğmesi](./media/guix-studio/record-button.png) Makroyu kaydet

![Kayıttan yürütme düğmesi](./media/guix-studio/playback-button.png) Kayıttan yürütme makrosu

![Çalıştır düğmesi](./media/guix-studio/run-button.png) Uygulamayı çalıştır

![Hakkında düğmesi](./media/guix-studio/about-button.png) GUX Studio hakkında

### <a name="project-view"></a>Proje görünümü

***Proje görünümü** _ ekli Kullanıcı arabirimini oluşturan hiyerarşik liste Gux nesnelerini gösterir. Yeni Gux nesneleri, üst nesneye tıklayıp _*_Ekle_*_ menüsünden bir nesne seçilerek (ya da nesneye sağ tıklayıp sağ tıklama menüsünden seçilerek) eklenebilir. Aşağıdaki _*_Şekil 4_*_ ' te Gux Studio _ *_proje görünümü_* * gösterilmektedir.

![GUX Studio proje görünümünün ekran görüntüsü.](./media/guix-studio/image_35.png)

**Şekil 4**

### <a name="properties-view"></a>Özellikler Görünümü

***Özellikler Görünümü** _, şu anda seçili olan Gux nesnesinin ayrıntılı özellik bilgilerini gösterir. Bu, _*_proje görünümü_*_ aracılığıyla veya _*_hedef görünümdeki_*_ nesneye doğrudan tıklanarak seçilebilir. Aşağıdaki _*_Şekil 5_*_ ' te Gux Studio _ *_Özellikler Görünümü_* * gösterilmektedir.

![GUX Studio özellikleri görünümünün ekran görüntüsü.](./media/guix-studio/image36.jpg)

**Şekil 5**

### <a name="target-view"></a>Hedef görünüm

***Target View** _, WYSIWYG ekran tasarımı ve düzen alanıdır. Bu görünüm, hedef donanımınızın fiziksel görüntüsünü veya görüntülenmesini temsil eder. Nesneler, basit fare işlemleri aracılığıyla seçilebilir, taşınabilir, yeniden boyutlandırılabilir, vb. olabilir. Ayrıca, hizalama ve Z düzeni düğme işlemleri hedef görünümdeki seçili nesneler üzerinde kullanılabilir. _*_Hedef görünümde_*_ bir nesnenin seçilmesi, bu nesnenin Özellikler _*_görünümünde_*_ görüntülenmesine neden olur. Aşağıdaki _*_Şekil 6_*_ ' da Gux Studio _ *_hedef görünümü_* * gösterilmektedir.

![GUX Studio hedef görünümünün ekran görüntüsü.](./media/guix-studio/image_37.png)

**Şekil 6**

### <a name="resource-view"></a>Kaynak Görünümü

***Kaynak görünümü** _, her bir ekran için tanımlanan uygulama ekranları için kullanılabilir kaynakları (renkler, yazı tipleri, pixelharitalar ve dizeler) yönetmek için kullanılır. Kaynak görünümü grup üst bilgilerine tıklayarak her bir grubu genişletebilir ve grup içeriğini inceleyebilirsiniz. Aşağıdaki _*_Şekil 7 '_*_ de Gux Studio _ *_kaynak görünümü_* * gösterilmektedir.

![GUX Studio Kaynak Görünümü ekran görüntüsü.](./media/guix-studio/image38.jpg)

**Şekil 7**

Kaynak gruplarının başlığı geçerli tema adını belirtir. Çoklu Temalar varsa, yukarı ve aşağı oka tıklayarak Temalar arasında geçiş yapabilirsiniz.

Yukarıdaki görünümde bulunan her kaynak grubu grup üstbilgisine tıklanarak genişletilebilir veya daraltılabilirler. Bir sonraki bölümde, her bir kaynak grubunun daha ayrıntılı bir açıklaması aşağıda verilmiştir.

## <a name="the-guix-studio-project"></a>GUX Studio projesi

Bir Gux Studio projesi, UI ekran tasarımı ve UI kaynakları hakkındaki bilgileri saklar. Proje verileri, uzantısı "olan bir XML biçimi dosyasına kaydedilir. ***GXP***". Proje dosyası bir XML şema dosyası olduğundan, sürümü oluşturulmuş ve diğer herhangi bir kaynak dosyayla benzer şekilde paylaşılabilir.

GUX Studio 'Yu kullanmaya ilk kez başladığınızda, dağıtımla birlikte sunulan örnek projelerden birini açmanız veya yeni bir proje oluşturmanız gerekecektir. Tüm çalışmanız proje veri dosyasına kaydedilir.

GUX Studio Ayrıca ANSI C kaynak dosyaları da üretir. Bu kaynak dosyalar, tasarlanan ekranları açıklayan uygulama kaynaklarınızı ya da veri yapılarını içerir. GUX Studio Ayrıca, uygulama ekranlarınızı dinamik olarak oluşturmak için oluşturulan veri yapılarını kullanmayı bildiğiniz bu oluşturulmuş kaynak dosyaları API işlevlerine yazar. Uygulama yazılımınız, Gux Studio içinde tasarladığınız ekranları oluşturmak için yalnızca belirtilen API işlevlerini çağırır.

Kullanıcı arabiriminizi tasarlarken ilerlemeniz durumunda, tasarladığınız arabirimi derleyip çalıştırmanıza imkan tanıyan Gux uyumlu çıkış dosyalarını oluşturmak için düzenli aralıklarla Gux Studio 'Yu kullanmak isteyeceksiniz. Hedef donanımınız ya da Windows masaüstünüzde, ThreadX ve GUıDX benzetimi yapan kaynak dosyaları derleyip çalıştırabilirsiniz.

## <a name="guix-studio-project-organization"></a>GUX Studio Proje organizasyonu

GUX Studio 'nun nasıl etkin bir şekilde kullanıldığını ve Gux Studio IDE 'nin Proje görünümünde sunulan bilgileri anlamayı anlamak için, bir Gux Studio projesinin temel organizasyonu hakkında bilgi sahibi olmanız faydalı olur. Proje görünümü, projenizde bulunan tüm bilgilerin Özet görsel gösterimidir.

Projeyi açıklamadan önce, birkaç terim tanımlamanız gerekir. İlk olarak, **görüntü** terimi fiziksel bir görüntüleme cihazının anlamı olacak şekilde kullanıyoruz. Bu çoğunlukla bir LCD görüntü aygıtıdır, ancak diğer teknolojiyi kullanıyor olabilir. Bir sonraki terim, en üst düzey bir Gux nesnesi olan, genellikle bir Gux penceresi ve ilişkili alt öğelerinden oluşan bir **ekrandır**. Ekran, çalışma zamanında tanımlanabilen ve değiştirilebilen bir yazılım yapısıdır. Son olarak, bir **Tema** kaynak koleksiyonudur. Bir tema, birlikte iyi çalışmak ve son kullanıcıyı tutarlı bir görünüm ile sunmak için tasarlanan renk tanımları, yazı tipi tanımları ve pixelmap tanımlarının bir tablosunu içerir.

Bu proje, proje adı, desteklenen ekran sayısı, her bir ekran için çözünürlük ve renk biçimi, desteklenen dillerin sayısı ve desteklenen her dilin adı gibi bir genel bilgiler kümesi içerir. Proje adı, Proje görünümünde görünen ilk düğümdür.

Ardından Proje, 4 fiziksel ekran için gereken tüm bilgileri ve her bir ekran için kullanılabilen ekranları ve kaynakları düzenler. Görünen adlar proje görünüm ağacındaki bir sonraki düzey düğümlerdir.

GUX Studio uygulamasının benzersiz bir özelliği, her biri kendi x, y çözünürlüğü, renk biçimi, ekranları ve kaynakları olan birden çok fiziksel ekran için yerleşik desteğe sahiptir. GUX uygulamalarının büyük çoğunluğu yalnızca bir fiziksel görüntü kullanır, ancak bu özellik, birden çok eş zamanlı fiziksel ekranı desteklemesi gereken bir ürünü oluşturmak için önemlidir.

Her bir görüntüleme tanımının altında, bu ekran için tanımlanan en üst düzey pencereler veya ekranlar bulunur. Ekran tanımları, her ekranda alt pencere öğelerinin sayısına ve iç içe olmasına bağlı olarak herhangi bir düzeye yuvalanmış olabilir.

Bu ekran ve alt pencere öğesi organizasyonu Proje görünümünde grafiksel bir şekilde görüntülenir.

Her bir ekran ile ilişkili Temalar, görüntüleme tarafından desteklenen temalardır ve her temayı oluşturan kaynak içeridir. Projenizde birden çok ekran varsa, bir ekran ve sonra başka bir görüntü seçtiğinizde Kaynak Görünümü içeriğini değiştirdiğine dikkat edin. Bunun nedeni, kaynak içeriğinin her bir görüntüleme ile bağlantılı olmasından kaynaklanır. Yalnızca renk biçimi farklı olabilir, ancak kullanmayı seçtiğiniz pixelmaps, renkler ve yazı tipleri bir fiziksel görüntü ile diğerine farklılık gösterebilir.

Proje tarafından tutulan son bileşen, her bir ekran ile ilişkili dize tablosu verileri olur. Ekranlar çok farklı x ve y çözünürlüklerine sahip olduğundan, dize verileri projede tanımlanan her bir ekran için bağımsız olarak korunur.
