---
title: Ekran akışını tanımlama
description: GUX Studio, ekran geçiş mantığının otomatik olarak oluşturulmasını ve yürütülmesini destekler.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 1c590725281c785181bcb4c5852346bc973c24d1
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826297"
---
# <a name="chapter-7-defining-screen-flow"></a>Bölüm 7: ekran akışını tanımlama

GUX Studio, ekran geçiş mantığının otomatik olarak oluşturulmasını ve yürütülmesini destekler. Kullanıcı bir grafik ekran akışı diyagramı oluşturup düzenleyerek ekran geçiş mantığını tanımlar. Projeye bir ekran akışı diyagramı eklendiğinde, bu iki önemli özelliği sağlar: 1) uygulama Studio ortamı içinden yürütülebilir ve 2) Studio, üretilen belirtim. c dosyasında belirlenen ekran akışını uygulamak için otomatik olarak olay işleyicileri ve ekran geçiş mantığı oluşturup bu yükü uygulama programından kaldırır. 

Uygulamayı masaüstü ortamınızda çalıştırmak, uygulamanızı yürütmek için bir derleme/bağlantı döngüsünü yapmanız gerekmediği için zaman tasarrufu sağlayan yararlı bir özelliktir. Uygulamanın derlenmesi gerekmeden yapılabilecekleri kurs sınırlamaları vardır. Özel çizim işlevleri, özel olay işleyicileri ve karmaşık olay işleme, uygulamayı Gux Studio ortamı içinden çalıştırırken kullanılamaz. Yine de bu özellik, ekran geçiş mantığını otomatik olarak oluşturmanıza ve bir ekrandan diğerine geçiş yapmak için çalıştırılacak program animasyonlarına olanak tanır. Bu efektler ve animasyonlar, Gux Studio ortamının içinden doğrudan gözlemlenebilir.

Aşağıdaki paragraflarda tanımlayabilmemiz için ekran akışı, Tetikleyiciler ve eylemleri tanımladığınızda, yalnızca Kullanıcı arabiriminin Studio ortamından yürütülmesini etkinleştirirsiniz, ancak aynı zamanda Gux Studio 'yu, olayları işleyecek ve bir ekrandan diğerine geçiş gibi bu olaylara göre eylemler işleyecek bir mantık oluşturacak şekilde etkinleştirirsiniz.

## <a name="configuring-screen-flow"></a>Ekran akışını yapılandırma

Bir uygulamanın Studio ortamı içinden yürütülebilmesi için önce birkaç şeyin tanımlanması gerekir. İlk olarak, program başlangıcında gösterilmesi gereken üst düzey ekranın veya ekranların, Studio özellikleri görünümündeki "Başlangıçta görünür" özelliği seçilerek gösterilmelidir. Bu bayrak, program başlatıldığında bu ekranın başlangıçta görüntülenmesi gerektiğini gösterir. İsterseniz birden fazla ekran bu gösterimi içerebilir.

Başlangıçta görünen ekran (ler) i tanımladıktan sonra Kullanıcı, UI uygulamasının ekrandan ekran 'e nasıl akacağınızı tanımlayabilir. GUX Studio, ekran geçiş mantığını tanımlamak için bir grafik ekran akışı diyagramı sağlar. Ekran akışı düzenleme iletişim kutusunu açmak için menü seçimini ***Yapılandır, ekran akışı** _ ' i seçmeniz yeterlidir.

![GUX Studio ekran akışı iletişim kutusunun ekran görüntüsü.](./media/guix-studio/config_screen_flow.png)

**Şekil 30**

Projede tanımlanan her üst düzey ekran, ekran adını gösteren bir kutu olarak gösterilir. Bu kutu, projede tanımlanan her üst düzey ekranı temsil eden bir yer tutucudur. Bu kutular, istendiği gibi taşınabilir ve yeniden boyutlandırılabilir. Bir üst düzey ekrandan diğerine geçiş tanımlandığında, bir ekrandan diğerine geçişleri göstermek için iki ekran arasında ok düğmeli bir bağlantı çizgisi gösterilir.

Ekran akışı diyagramı 'nın sol tarafındaki ağaç görünümü, her üst düzey ekranı gösterir ve ekran akışı diyagramında hangi üst düzey ekranların çizildiğini seçebileceksiniz.

Ekran akışı diyagramı kaydırılabilir. Kaydırılabilir pencereyi genişletmek için, görünür alanın dışında herhangi bir ekran bloğunu aşağı ve sağa sürükleyebilirsiniz. Kaydırılabilir pencereniz büyütülirse, fare tekerleğini aşağı kaydırarak görünür alana sığacak şekilde yakınlaştırabilirsiniz. Kaydırılabilir pencere yakınlaştırıldığında fare tekerleğini kaydırarak tüm blokları tutmaya yetecek kadar büyük hale getirebilirsiniz.

Bir ekran için geçişleri tanımlamak üzere bu ekran için yer tutucuya sağ tıklayarak tetikleyici listesini Düzenle iletişim kutusunu açın, bkz. ***Şekil 31***.

![GUX Studio düzenleme tetikleyici listesi iletişim kutusunun ekran görüntüsü.](./media/guix-studio/edit_trigger_list.png)

**Şekil 31**

Tetikleyici düzenleme iletişim kutusu, kullanıcının tanımladığı ve bu olay tetikleyicilerini neden çağırdığımız bir ekran geçişi tetikleyecek olayları listeleyecektir. Tetikleyiciler, genellikle seçili ekranın bir veya daha fazla alt pencere öğesi tarafından oluşturulan sinyallerdir.

Yeni bir tetikleyici tanımlamak için, _ *_şekil 32_* * ' de gösterilen tetikleyici Ekle iletişim kutusunu açmak Için tetikleyici listesini Düzenle iletişim kutusunda ***Yeni tetikleyici Ekle** _ düğmesini seçin.

![GUX Studio tetikleyici ekleme iletişim kutusunun ekran görüntüsü.](./media/guix-studio/add_trigger_for.png)

**Şekil 32**

Yeni bir eylem kümesini tetikleyecek olay türünü tanımlayabilir ve bu tetikleyici olay alındığında yürütülecek eylemleri tanımlayabilirsiniz.

Yeni bir animasyon ekran geçişini tetiklemek için kullanmak istediğiniz olay türünü tanımladıktan sonra, bu yeni tetikleyiciyi kaydedin ve tetikleyici listesini Düzenle iletişim kutusunda görüntülenir.

Tetikleyici listesini Düzenle iletişim kutusunda olayı seçip ***tetikleyici olayını Düzenle*** düğmesini seçerek bu olayı değiştirebilirsiniz (ilgili eylemleri değiştirmeden).

Benzer şekilde, olayı seçip ***seçili tetikleyiciyi Sil*** düğmesine tıklayarak herhangi bir tetikleyici olayını listeden kaldırabilirsiniz.

Belirli bir tetikleyici olayına göre gerçekleşmesi gereken animasyon veya ekran geçişini belirtmek için, bu tetikleyici olayını seçin ve ***eylemleri Düzenle*** düğmesine tıklayın. Tanımlı tetikleyiciye göre birden fazla eylem tetikleyebileceğinizi unutmayın.

Eylemleri **Düzenle** düğmesi, Şekil 33 ' de gösterilen tetikleyici Için eylemleri Düzenle iletişim kutusunu getirir: 

![Tetikleyici için Gux Studio düzenleme eylemleri iletişim kutusunun ekran görüntüsü.](./media/guix-studio/edit_actions_for_trigger.png)

**Şekil 33**

Bu iletişim kutusu, bu tetikleyici olayına göre uygulanacak sayıda eylem tanımlamanızı sağlar. Her eyleme, her eylem tanımını bir görsel animasyon veya geçişle ilişkilendirmenize yardımcı olmak için anlamlı bir ad verebilirsiniz. Yukarıdaki örnekte, "fade_in_text_screen" ve "fade_out_button_screen" adlı iki eylem tanımlıyoruz.

Uygulanacak yeni bir eylem tanımlayın, Eylem Seç iletişim kutusunu gösteren yeni eylem Ekle düğmesine tıklayın, Şekil 34:

![GUX Studio eylem seçme iletişim kutusunun ekran görüntüsü.](./media/guix-studio/select_action.png)

**Şekil 34**

Kullanılabilir eylem türleri şunlardır:

- **Animasyon**: belirtilen bilgilerle bir animasyon başlatın.
- **Ekle**: hedef ekranı üst ekrana ekleyin, üst ekran belirtilmemişse, hedef ekran kök pencereye iliştirilir.
- **Ayır**: hedef ekranı üst öğesinden ayırın.
- **Gizle**: hedef ekranını gizleyin.
- **Ekran yığını açılır penceresi**: iç ekran yığınından bir ekran açılır.
- **Ekran yığını gönderme**: iç ekran yığınına bir ekran işaretçisi gönderin.
- **Ekran yığını sıfırlaması**: iç ekran yığınından tüm ekran işaretçilerini kaldırın.
- **Göster**: hedef ekranı göster.
- **Geçiş**: hedef ekranı geçerli ekranın üst öğesine ekleyin ve geçerli ekranı üst öğesinden ayırın.
- **Pencere yürütme**: Modal, hedef ekranı önemli şekilde yürütür.
- **Pencere yürütme durdurma**: geçerli ekranın önemli bir şekilde yürütülmesi çıkış.

Seçilen tetikleyici olayına göre gerçekleştirilecek bir eylem tanımladıktan sonra, bu eylem tetikleyici için eylemleri Düzenle iletişim kutusunda görüntülenir. Bu eylemi, şekil 35 ' de gösterildiği gibi bu eylemin parametrelerini değiştirmek için seçebilirsiniz.

![Tetikleyici için Gux Studio düzenleme eylemleri iletişim kutusunun ekran görüntüsü.](./media/guix-studio/edit_actions_for_trigger.png)

**Şekil 35**

Eylem türü bir animasyon ise, yürütülecek bir slayt ve/veya belirme türü animasyonu tanımlamanızı sağlayan bir animasyon parametreleri kümesi sağ tarafta görüntülenir. Bir animasyon eylemi tamamlandığında, animasyonun kendi üst öğesinden otomatik olarak ayrılmalı ve/veya iç ekran yığınına itilmesi gerektiğini de belirleyebilirsiniz. Bu, çok katmanlı menü sistemlerini tanımlarken yararlı olur.

Slayt ve Soldur animasyonları için, kolaylaştırıcı Işlev Seç düğmesini seçerek kullanılacak kolaylaştırıcı Işlevi de tanımlayabilirsiniz. Kolaylaştırıcı işlevler, gerçek yaşam taşıma olaylarını daha yakından taklit etmek için tasarlanan çeşitli eğrilerle. Bu düğme seçildiğinde, **kolaylaştırıcı Işlev Seç** iletişim kutusu açılır. Şekil 36:

![GUX Studio 'Da kolaylaştırıcı Işlev seçme iletişim kutusunun ekran görüntüsü.](./media/guix-studio/easing_function_select.png)

**Şekil 36**

Tek bir tetikleyici olay ile ilişkilendirmek üzere birden çok eylem tanımlıyorsanız, her eyleme anlamlı bir ad atamak yararlı olabilir. Bu adlar, olay ve eylem tablolarını tanımlamak üzere oluşturulan belirtimlerde kullanılmak üzere, eylem adları C sözdizimi adlandırma kurallarına uymalıdır.

GUX Studio içinde tetikleyici olayları ve eylemleri tanımladığınızda, bu olayları işlemek ve belirtilen eylemleri yürütmek için proje belirtimleri dosyasında otomatik olay işleyicileri oluşturulur. Bu, tetikleyici olayları hala tanımladığınız herhangi bir özel olay işleyicisine geçirilse de, uygulama kodunuzda bu olayları işlemeniz gerekmediği anlamına gelir. Diğer bir deyişle, kendi özel olay işleyicilerinizi değiştirmek yerine Studio tarafından oluşturulan olay işleyicileri.

## <a name="running-the-application"></a>Uygulamayı Çalıştırma

Başlangıç ekranları ve bir ekran akışı diyagramı oluşturulduktan sonra, "uygulamayı çalıştır" seçeneğini belirleyerek uygulamanızı Studio 'da çalıştırabilirsiniz.

![Uygulamayı Çalıştır düğmesinin ekran görüntüsü.](./media/guix-studio/image68.jpg)

araç çubuğundaki düğme Düzenle ' yi seçin | Uygulamayı proje menüsünden çalıştırın veya ekran akışını Düzenle iletişim kutusunun alt kısmındaki Çalıştır düğmesini seçin.

Uygulamayı çalıştırdığınızda, "Başlangıçta görünür" olarak belirlediğiniz ekran (ler) i yeni bir pencere içinde görürsünüz. Bu ekrandaki alt pencere öğeleri tam olarak çalışır. Düğmelere tıklayabilir, sürgüleri işleyebilir ve tekerlekleri, vb.... Bu pencere öğelerinin herhangi biri için özel çizim işlevleri veya müşteri olay işleme tanımladıysanız, uygulamayı bu modda çalıştırırken bunu görmeyecektir. Ancak tetikleyici olayları ve eylemleriyle bir ekran akışı diyagramı tanımladıysanız, bu Tetikleyiciler çalışır durumda olur ve tanımlamış olduğunuz animasyonlar dahil, ekranlarınız sizin tanımladığınız şekilde geçiş yapacaktır.
