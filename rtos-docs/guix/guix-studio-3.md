---
title: GUIX Studio açıklaması
description: Bu bölümde GUIX Studio sistem analizi aracının açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 843106aa67d2a978c7f271954e028b32ba4dd007fe35a36b7c17ba0f5f80e4a9
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116787216"
---
# <a name="chapter-3-description-of-guix-studio"></a>Bölüm 3: GUIX Studio Açıklaması

Bu bölümde GUIX Studio sistem analizi aracının açıklaması yer almaktadır. Gui'nin genel işlevselliğinin açıklaması bu bölümde bulunabilir. 

## <a name="guix-studio-views"></a>GUIX Studio Görünümleri

GUIX Studio kullanıcı arabiriminin beş temel alanı vardır: ***Araç** Çubuğu _, _*_Project Görünümü,_*_ _*_Özellikler_*_ _*_Görünümü,_*_ Hedef Görünüm ve _*_Kaynak Görünümü._*_ _ *_Şekil 2_** temel GUIX Studio kullanıcı arabirimini gösterir. Görünümlerin her biri aşağıdaki alt bölümlerde daha ayrıntılı olarak ele alınmıştır.

![Temel GUIX Studio kullanıcı arabiriminin ekran görüntüsü.](./media/guix-studio/image_10.png)

**Şekil 2**

### <a name="title"></a>Başlık

- GUIX Studio 18: ***Başlık** _ önceki _ Şekil *_2_** öğesinin en üstünde gösterildiği gibi GUIX Studio sürümünü ve açık olan projeyi görüntüler.

### <a name="toolbar"></a>Araç Çubuğu

***Araç Çubuğu** _* Şekil _3_**'de gösterildiği gibi GUIX Studio geliştiricisi tarafından kullanılabilen düğmeleri gösterir.

![GUIX Studio araç çubuğunun ekran görüntüsü.](./media/guix-studio/image11.jpg)

**Şekil 3**

Araç çubuğu düğmeleri aşağıdaki gibi tanımlanır:

![Yeni düğmesi](./media/guix-studio/new-button.png) Yeni bir GUIX Studio projesi oluşturur

![Aç düğmesi](./media/guix-studio/open-button.png) Var olan bir GUIX Studio projesini açar

![Kaydet düğmesi](./media/guix-studio/save-button.png) Projeyi kaydeder

![Kes düğmesi](./media/guix-studio/cut-button.png) Küçükler de dahil olmak üzere pencere öğesi seçiliyken kes

![Kopyala düğmesini](./media/guix-studio/copy-button.png) Seçili pencere öğelerini, diğer öğeleri de dahil olmak üzere kopyalama

![Yapıştır düğmesi](./media/guix-studio/paste-button.png) Pencere öğesi ve öğeleri yapıştırma

![Sola hizala düğmesi](./media/guix-studio/left-align-button.png) Seçili pencere öğelerini sola hizala

![Sağ hizala düğmesi](./media/guix-studio/right-align-button.png) Seçili pencere öğelerini sağa hizala

![Üst hizala düğmesi](./media/guix-studio/top-align-button.png) Seçili pencere öğelerini üst hizala

![Alta hizala düğmesi](./media/guix-studio/bottom-align-button.png) Seçili pencere öğelerini alt hizala

![Dikey boşluk düğmesi](./media/guix-studio/space-vertically-button.png) Seçilen pencere öğelerini dikey olarak eşit olarak alanla

![Yatay boşluk düğmesi](./media/guix-studio/space-horizontally-button.png) Seçili pencere öğelerini yatay olarak eşit olarak alanla

![Eşit genişlik düğmesi](./media/guix-studio/equal-width-button.png) Seçili pencere öğelerini eşit genişlikte yapma

![Eşit yükseklik düğmesi](./media/guix-studio/equal-height-button.png) Seçilen pencere öğelerinin yüksekliğe eşit hale gelir

![Öne taşı düğmesi](./media/guix-studio/move-front-button.png) Seçili pencere öğelerini öne taşıma

![Geri taşı düğmesi](./media/guix-studio/move-back-button.png) Seçili pencere öğelerini geri taşıma

![Boyut düğmesi](./media/guix-studio/size-button.png) Seçilen pencere öğelerini içeriğe göre boyut hedef ekranı yakınlaştır

![Uzaklaştır düğmesi](./media/guix-studio/zoom-out-button.png) Hedef ekranı uzaklaştırma

![Yakınlaştır düğmesi](./media/guix-studio/zoom-in-button.png) Hedef ekranı yakınlaştırma

![Kayıt düğmesi](./media/guix-studio/record-button.png) Kayıt Makrosu

![Kayıttan yürütme düğmesi](./media/guix-studio/playback-button.png) Kayıttan Yürütme Makrosu

![Çalıştır düğmesi](./media/guix-studio/run-button.png) Uygulamayı Çalıştırma

![Hakkında düğmesi](./media/guix-studio/about-button.png) GUIX Studio hakkında

### <a name="project-view"></a>Project Görünüm

***Project Görünümü** _ ekli kullanıcı arabirimini oluşturan hiyerarşik liste GUIX nesnelerini gösterir. Üst nesneye tıklar ve ardından Ekle menüsünden bir nesne seçerek (veya nesneye sağ tıklar ve sağ tıklama menüsünden seçim ile) yeni GUIX nesneleri eklenebilir. _**_ _*_Aşağıdaki Şekil 4'te_*_ GUIX Studio _*_Project ** gösterilmiştir._

![GUIX Studio Project Görüntüsü.](./media/guix-studio/image_35.png)

**Şekil 4**

### <a name="properties-view"></a>Özellikler Görünümü

* Özellikler **Görünümü** _ seçili olan GUIX nesnesinin ayrıntılı özellik bilgilerini gösterir. Bu bilgiler, _*_Project Görünümü_*_ aracılığıyla veya Doğrudan Hedef Görünüm'de nesnesine _*_tıklayarak seçilebilir._*_ _*_Aşağıdaki Şekil 5'te_*_ GUIX Studio _*_Özellikler Görünümü **_ gösterilmiştir.

![GUIX Studio Özellikler Görünümünün ekran görüntüsü.](./media/guix-studio/image36.jpg)

**Şekil 5**

### <a name="target-view"></a>Hedef Görünüm

***Hedef Görünüm** _ WYSIWYG ekran tasarımı ve düzen alanıdır. Bu görünüm, hedef donanımınız üzerinde kullanılabilen fiziksel ekranı veya ekranları temsil etmek için hazır. Nesneler basit fare işlemleriyle seçilebilir, taşınabilir, yeniden boyutlandırılabilir vb. Buna ek olarak, hizalama ve Z sırası düğme işlemleri Hedef Görünüm'de seçili nesnelerde kullanılabilir. Hedef Görünüm'de bir _*_nesne seçmek,_*_ bu nesnenin özelliklerinin Özellikler Görünümünde de görüntülenebilir. _**_ _*_Aşağıdaki Şekil 6'da_*_ GUIX Studio _*_Hedef Görünümü **gösterilmiştir._

![GUIX Studio Hedef Görünümünün ekran görüntüsü.](./media/guix-studio/image_37.png)

**Şekil 6**

### <a name="resource-view"></a>Kaynak Görünümü

***Kaynak Görünümü** _ her ekran için tanımlanan uygulama ekranlarında kullanılabilen kaynakları (renkler, yazı tipleri, piksel haritaları ve dizeler) yönetmek için kullanılır. Her grubu genişletmek ve grup içeriklerini incelemek için kaynak görünümü grubu üst bilgilerine tıkabilirsiniz. _*_Aşağıdaki Şekil 7'de_*_ ** GUIX Studio _*_Kaynak Görünümü_ gösterilmiştir.

![GUIX Studio Kaynak Görünümü.](./media/guix-studio/image38.jpg)

**Şekil 7**

Kaynak gruplarının başlığı geçerli tema adını gösterir. Birden çok tema varsa yukarı ve aşağı oka tıklayarak temalar arasında geçiş yapabilirsiniz.

Yukarıdaki görünümde yer alan her kaynak grubu, grup üst bilgisinde tıklayarak genişletilebilir veya daraltılmış olabilir. Sonraki bölümde her kaynak gruplarının daha ayrıntılı bir açıklaması verilmiştir.

## <a name="the-guix-studio-project"></a>GUIX Studio Project

GUIX Studio projesi, kullanıcı arabirimi ekran tasarımınız ve kullanıcı arabirimi kaynaklarınız hakkında bilgi sağlar. Proje verileri uzantısı " olan bir XML biçim dosyasına kaydedilir. ***gxp***". Proje dosyası bir XML şema dosyası olduğu için, başka bir kaynak dosyaya benzer şekilde denetlenen ve paylaştırılır.

GUIX Studio'yu kullanmaya ilk kez başlanıyorsa, dağıtımla birlikte sağlanan örnek projelerden birini açmalı veya yeni bir proje oluşturmanız gerekir. Tüm çalışmanız proje veri dosyasına kaydedilir.

GUX Studio Ayrıca ANSI C kaynak dosyaları da üretir. Bu kaynak dosyalar, tasarlanan ekranları açıklayan uygulama kaynaklarınızı ya da veri yapılarını içerir. GUX Studio Ayrıca, uygulama ekranlarınızı dinamik olarak oluşturmak için oluşturulan veri yapılarını kullanmayı bildiğiniz bu oluşturulmuş kaynak dosyaları API işlevlerine yazar. Uygulama yazılımınız, Gux Studio içinde tasarladığınız ekranları oluşturmak için yalnızca belirtilen API işlevlerini çağırır.

Kullanıcı arabiriminizi tasarlarken ilerlemeniz durumunda, tasarladığınız arabirimi derleyip çalıştırmanıza imkan tanıyan Gux uyumlu çıkış dosyalarını oluşturmak için düzenli aralıklarla Gux Studio 'Yu kullanmak isteyeceksiniz. hedef donanımınız veya Windows masaüstünüzde, threadx ve guıdx benzetimi yapan kaynak dosyaları derleyebilir ve çalıştırabilirsiniz.

## <a name="guix-studio-project-organization"></a>gux Studio Project organizasyonu

gux studio 'nun nasıl etkin bir şekilde kullanılacağına ve gux studio ıde 'nin Project görünümünde sunulan bilgileri nasıl anlayabileceğinizi anlamak için, bir gux studio projesinin temel organizasyonu hakkında bilgi sahibi olmanız faydalı olur. Project görünümü, projenizde bulunan tüm bilgilerin özet görsel gösterimidir.

Projeyi açıklamadan önce, birkaç terim tanımlamanız gerekir. İlk olarak, **görüntü** terimi fiziksel bir görüntüleme cihazının anlamı olacak şekilde kullanıyoruz. Bu çoğunlukla bir LCD görüntü aygıtıdır, ancak diğer teknolojiyi kullanıyor olabilir. Bir sonraki terim, en üst düzey bir Gux nesnesi olan, genellikle bir Gux penceresi ve ilişkili alt öğelerinden oluşan bir **ekrandır**. Ekran, çalışma zamanında tanımlanabilen ve değiştirilebilen bir yazılım yapısıdır. Son olarak, bir **Tema** kaynak koleksiyonudur. Bir tema, birlikte iyi çalışmak ve son kullanıcıyı tutarlı bir görünüm ile sunmak için tasarlanan renk tanımları, yazı tipi tanımları ve pixelmap tanımlarının bir tablosunu içerir.

Bu proje, proje adı, desteklenen ekran sayısı, her bir ekran için çözünürlük ve renk biçimi, desteklenen dillerin sayısı ve desteklenen her dilin adı gibi bir genel bilgiler kümesi içerir. proje adı Project görünümünde görünen ilk düğümdür.

Ardından Proje, 4 fiziksel ekran için gereken tüm bilgileri ve her bir ekran için kullanılabilen ekranları ve kaynakları düzenler. görünen adlar Project görünüm ağacındaki bir sonraki düzey düğümlerdir.

GUX Studio uygulamasının benzersiz bir özelliği, her biri kendi x, y çözünürlüğü, renk biçimi, ekranları ve kaynakları olan birden çok fiziksel ekran için yerleşik desteğe sahiptir. GUX uygulamalarının büyük çoğunluğu yalnızca bir fiziksel görüntü kullanır, ancak bu özellik, birden çok eş zamanlı fiziksel ekranı desteklemesi gereken bir ürünü oluşturmak için önemlidir.

Her bir görüntüleme tanımının altında, bu ekran için tanımlanan en üst düzey pencereler veya ekranlar bulunur. Ekran tanımları, her ekranda alt pencere öğelerinin sayısına ve iç içe olmasına bağlı olarak herhangi bir düzeye yuvalanmış olabilir.

bu ekran ve alt pencere öğesi organizasyonu Project görünümünde grafiksel bir şekilde görüntülenir.

Her bir ekran ile ilişkili Temalar, görüntüleme tarafından desteklenen temalardır ve her temayı oluşturan kaynak içeridir. Projenizde birden çok ekran varsa, bir ekran ve sonra başka bir görüntü seçtiğinizde Kaynak Görünümü içeriğini değiştirdiğine dikkat edin. Bunun nedeni, kaynak içeriğinin her bir görüntüleme ile bağlantılı olmasından kaynaklanır. Yalnızca renk biçimi farklı olabilir, ancak kullanmayı seçtiğiniz pixelmaps, renkler ve yazı tipleri bir fiziksel görüntü ile diğerine farklılık gösterebilir.

Proje tarafından tutulan son bileşen, her bir ekran ile ilişkili dize tablosu verileri olur. Ekranlar çok farklı x ve y çözünürlüklerine sahip olduğundan, dize verileri projede tanımlanan her bir ekran için bağımsız olarak korunur.
