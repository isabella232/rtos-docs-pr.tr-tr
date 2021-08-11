---
title: Ekran Flow Tanımlama
description: GUIX Studio, ekran geçişi mantığını otomatik oluşturma ve yürütmeyi destekler.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 1df90acd86b4446d96a66ab3ee21545afcd9824e28efb40204c2966cb075c501
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116785618"
---
# <a name="chapter-7-defining-screen-flow"></a>Bölüm 7: Ekran Flow

GUIX Studio, ekran geçişi mantığını otomatik oluşturma ve yürütmeyi destekler. Kullanıcı, grafik ekran akışı diyagramı oluşturarak ve düzenleyerek ekran geçiş mantığını tanımlar. Projeye bir ekran akışı diyagramı eklenmiştir, iki önemli özellik sağlar: 1) Uygulama Studio ortamından yürütülebilir ve 2) Studio, oluşturulan specifications.c dosyasında belirlenen ekran akışını uygulamak için olay işleyicileri ve ekran geçiş mantığını otomatik olarak üretir ve bu yükü uygulama programından çıkarır. 

Uygulamayı Masaüstünüzde Studio ortamından çalıştırmanız, uygulamanızı yürütmek için derleme/bağlantı döngüsünden geçerek zaman kazandırmanızı sağlar. Uygulamayı derlemeden yapılacaklar konusunda elbette sınırlamalar vardır. Özel çizim işlevleri, özel olay işleyicileri ve karmaşık olay işleme, uygulamayı GUIX Studio ortamından çalıştırarak kullanılamaz. Yine de bu özellik, ekran geçiş mantığını otomatik olarak oluşturma ve bir ekrandan diğerine geçiş yapmak için yürütülecek animasyonları programla özelliğine olanak sağlar. Bu etkiler ve animasyonlar doğrudan GUIX Studio ortamından gözlemlenebilir.

Ekran akışını, tetikleyicileri ve eylemleri aşağıdaki paragraflarda anlatacak şekilde tanımladığınız zaman, kullanıcı arabiriminizin yalnızca Studio ortamından yürütülmesini etkinleştirmenin yanı sıra GUIX Studio'nun olayları işleyen ve bu olayları temel alan eylemler gerçekleştirecek belirtim dosyanız içinde mantık oluşturması için de etkinleştirildiğini unutmayın.  örneğin, bir ekrandan diğerine geçiş.

## <a name="configuring-screen-flow"></a>Ekran Ayarlarını Flow

Bir uygulamanın Studio ortamından yürütülmeden önce birkaç şey tanımlanmalıdır. İlk olarak, Program başlangıcında görüntülenecek en üst düzey ekran veya ekranlar, Studio özellikleri görünümünde "Başlangıçta Görünür" özelliği seçerek göster gerekir. Bu bayrak, program başlatıldığında bu ekranın başlangıçta görüntüleniyor olması gerektiğini gösterir. İsterseniz birden fazla ekranda bu ifade kullanılabilir.

Başlangıçta görünen ekranları tanımlayarak kullanıcı arabirimi uygulamasının ekrandan ekrana nasıl akacaklarını tanımlayabilir. GUIX Studio, ekran geçiş mantığını tanımlamak için bir grafik ekran akışı diyagramı sağlar. Ekran akışı düzenleme iletişim kutusunu açmak için ***Yapılandır, Ekran Flow** _ menü seçimini yapmanız gerekir. _* Şekil _30_**'da ekran çekimini görebilirsiniz.

![GUIX Studio Ekran Görüntüsü iletişim kutusunun Flow görüntüsü.](./media/guix-studio/config_screen_flow.png)

**Şekil 30**

Projede tanımlanan her üst düzey ekran, ekran adını gösteren bir kutu olarak gösterilir. Bu kutu, projede tanımlanan her üst düzey ekranı temsil eden bir yer tutucudur. Bu kutular istediğiniz şekilde taşınabiliyor ve yeniden boyutlandırılabilir. Bir üst düzey ekrandan diğerine geçiş tanımlandığı zaman, bir ekrandan diğerine geçişleri göstermek için iki ekran arasında ok ucu olan bir bağlantı çizgisi gösterilir.

Ekran akışı diyagramının sol tarafındaki ağaç görünümü her üst düzey ekranı gösterir ve ekran akışı diyagramında hangi üst düzey ekranların çizileceklerini seçebilirsiniz.

Ekran akışı diyagramı kaydırılabilir. Kaydırılabilir pencereyi büyütmek için tüm ekran bloklarını görünür alanı aşağı ve sağa sürükleyebilirsiniz. Kaydırılabilir pencereniz büyüttükten sonra fare tekerleğini aşağı kaydırarak görünür alana sığacak şekilde uzaklaştırabilirsiniz. Kaydırılabilir pencere uzaklaştırıldı ise fare tekerleğini yukarı kaydırarak tüm blokları tutabilecek kadar büyütebilirsiniz.

Bir ekranın geçişlerini tanımlamak için, bu ekranın yer tutucusna sağ tıklayarak Tetikleyici Listesini Düzenle iletişim kutusunu açın, bkz. ***Şekil 31***.

![GUIX Studio Tetikleyici Listesini Düzenle iletişim kutusunun ekran görüntüsü.](./media/guix-studio/edit_trigger_list.png)

**Şekil 31**

Tetikleyici düzenleme iletişim kutusunda, kullanıcının ekran geçişlerini tetikleyen ve bu olay tetikleyicilerini çağırmamız için tanımlandığı olaylar listelenir. Tetikleyiciler normalde seçili ekranın bir veya daha fazla alt pencere öğesi tarafından oluşturulan sinyallerdir.

Yeni bir tetikleyici tanımlamak için Tetikleyici Listesini Düzenle iletişim kutusundaki ***** Yeni Tetikleyici Ekle _ düğmesini seçerek _* Şekil _32_** içinde gösterilen Tetikleyici Ekle iletişim kutusunu açın.

![GUIX Studio Tetikleyici Ekle iletişim kutusunun ekran görüntüsü.](./media/guix-studio/add_trigger_for.png)

**Şekil 32**

Yeni bir eylem kümesi tetikleyen olay türünü tanımlayabilir ve bu tetikleyici olayı alınca yürütülecek eylemleri tanımlayabilirsiniz.

Yeni bir animasyon ekranı geçişi tetiklemek için kullanmak istediğiniz olay türünü tanımladığınız zaman, bu yeni tetikleyiciyi kaydedin ve Tetikleyici Listesini Düzenle iletişim kutusunda görüntülenir.

Tetikleyici Listesini Düzenle iletişim kutusunda olayı seçerek ve Tetikleyici Olayı Düzenle düğmesini seçerek bu olayı değiştirebilirsiniz (ilgili eylemleri ***değiştirmeden).***

Benzer şekilde, olayı seçerek ve Seçili Tetikleyiciyi Sil düğmesine tıklayarak herhangi bir tetikleyici olayı ***listeden kaldırabilirsiniz.***

Belirli bir tetikleyici olayına göre gerçekleşmesi gereken animasyon veya ekran geçişlerini belirtmek için bu tetikleyici olayı seçin ve Eylem ***Düzenle düğmesine*** tıklayın. Tanımlanan her tetikleyiciyi temel alarak birden fazla eylemi tetikleyyanın.

Eylemleri **Düzenle düğmesi,** Şekil 33'te gösterilen Tetikleyici için Eylemleri Düzenle iletişim kutusunu getirir: 

![GuiX Studio Tetikleyici için Eylemleri Düzenle iletişim kutusunun ekran görüntüsü.](./media/guix-studio/edit_actions_for_trigger.png)

**Şekil 33**

Bu iletişim kutusu, bu tetikleyici olayına göre uygulanacak herhangi bir sayıda eylem tanımlamaya olanak sağlar. Her eylem tanımını bir görsel animasyon veya geçişle ilişkilendirmeye yardımcı olmak için her eyleme anlamlı bir ad veebilirsiniz. Yukarıdaki örnekte "fade_in_text_screen" ve "fade_out_button_screen" adlı iki eylem tanımladı.

Uygulanacak yeni bir eylem tanımla seçeneği, Eylem Seç iletişim kutusunu (Şekil 34) getiren Yeni Eylem Ekle düğmesine tıklayın:

![GUIX Studio Eylem Seç iletişim kutusunun ekran görüntüsü.](./media/guix-studio/select_action.png)

**Şekil 34**

Kullanılabilir eylem türleri şunlardır:

- **Animasyon:** Belirtilen bilgilerle bir animasyon başlat.
- **Ekleme:** Hedef ekranı üst ekrana iliştirin, üst ekran belirtilmezse hedef ekran kök pencereye ekli olur.
- **Ayırma:** Hedef ekranı üst öğesinden ayırma.
- **Gizle:** Hedef ekranı gizle.
- **Ekran Yığını Pop:** İç ekran yığınından bir ekran açılır.
- **Ekran Yığını Anında Itme:** İç ekran yığınına bir ekran işaretçisi itin.
- **Ekran Yığını Sıfırlama:** İç ekran yığınından tüm ekran işaretçilerini kaldırın.
- **Göster:** Hedef ekranı göster.
- **Geçiş:** Hedef ekranı geçerli ekranın üst ekranına iliştirin ve geçerli ekranı üst ekranından ayırabilirsiniz.
- **Pencere Yürütme:** Hedef ekranı mod olarak yürütür.
- **Pencere Yürütme Durdurma:** Geçerli ekranın model olarak yürütülmesini kapatın.

Seçilen tetikleyici olayına göre gerçekleştirilecek bir eylem tanımlandıktan sonra, bu eylem Tetikleyici için Eylemleri Düzenle iletişim kutusunda görüntülenir. Şekil 35'te gösterildiği gibi bu eylemin parametrelerini değiştirmek için bu eylemi seçin.

![GuiX Studio Tetikleyici için Eylemleri Düzenle iletişim kutusunun ekran görüntüsü.](./media/guix-studio/edit_actions_for_trigger.png)

**Şekil 35**

Eylem türü bir animasyon ise, yürütülecek bir slayt ve/veya soldurma türü animasyonu tanımlamanız için sağda bir animasyon parametreleri kümesi görüntülenir. Bir animasyon eylemi tamamlandığında, animasyonun üst öğesinden otomatik olarak ayrılmasını ve/veya iç ekran yığınına itilmiş olup olmadığını da belirlersiniz. Bu durum genellikle çok katmanlı menü sistemlerini tanımlarken yararlıdır.

Slayt ve soldurma animasyonları için, Easing Func Select düğmesini seçerek Easing İşlevi'nin de kullanımını tanımlayabilirsiniz. Kolay kullanım işlevleri, gerçek yaşam hareketi olaylarını daha yakından taklit etmek için tasarlanmış çeşitli eğrilerdir. Bu düğmeyi seçmek, İşlev **Seç iletişim kutusunu getirir,** Şekil 36:

![GUIX Studio İşlev Seç iletişim kutusunun ekran görüntüsü.](./media/guix-studio/easing_function_select.png)

**Şekil 36**

Bir tetikleyici olayıyla ilişkilendirilen birden çok eylem tanımlayarak her eylemi anlamlı bir ad atamak yararlı olabilir. Eylem adları C söz dizimi adlandırma kurallarına uymalı çünkü bu adlar olay ve eylem tablolarını tanımlamak için oluşturulan belirtimler dosyasında kullanılacaktır.

GUIX Studio'da tetikleyici olayları ve eylemleri tanımladığınız zaman, bu olayları işlemek ve belirtilen eylemleri yürütmek için proje belirtimleri dosyanız içinde otomatik olay işleyicileri oluşturulur. Bu, tetikleyici olayları tanımlandığı herhangi bir özel olay işleyiciye geçirilese de, bu olayları uygulama kodunda işlemeniz GEREKMİYİR. Başka bir deyişle Studio tarafından oluşturulan olay işleyicileri, kendi özel olay işleyicilerinizi değiştirmek yerine geliştirin.

## <a name="running-the-application"></a>Uygulamayı Çalıştırma

Başlangıç ekranları ve ekran akışı diyagramı oluşturulduktan sonra,"Uygulamayı Çalıştır"ı seçerek studio'da uygulama çalıştırabilirsiniz

![Uygulamayı Çalıştır düğmesinin ekran görüntüsü.](./media/guix-studio/image68.jpg)

araç çubuğundaki düğmeyi düzenle'yi | Proje menüsünden veya Düzenleme Ekranı Düzenleme iletişim kutusunun altındaki Çalıştır düğmesini seçerek Flow çalıştırın.

Uygulamayı çalıştırarak yeni bir pencerede "Başlangıçta Görünür" olarak belirlenen ekranları görürsünüz. Bu ekranda yer alan alt pencere öğeleri tamamen çalışır durumdadır. Düğmelere tıklar, kaydırıcıları çalıştırabilirsiniz ve tekerlekleri kaydırabilirsiniz. Bu pencere öğelerinin herhangi biri için özel çizim işlevleri veya müşteri olayı işleme tanımladıysanız, uygulamayı bu modda çalıştırabilirsiniz ancak bunu görmeyebilirsiniz. Ancak tetikleyici olaylarını ve eylemlerini içeren bir ekran akışı diyagramı tanımladıysanız, bu tetikleyiciler çalışır durumda olur ve tanımlanmamış tüm animasyonlar da dahil olmak üzere ekranlar tanımlandığı gibi geçiş gösterir.
