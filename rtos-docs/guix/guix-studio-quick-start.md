---
title: Azure Real-Time Işletim sistemi (RTOS) GUıDX Studio Hızlı Başlangıç Kılavuzu
description: bu kılavuzda, microsoft 'un azure rtos gux çalışma zamanı kitaplığı için özel olarak tasarlanan microsoft Windows tabanlı hızlı kullanıcı arabirimi geliştirme ortamı olan azure rtos gux Studio uygulamasının kullanımına ilişkin kısa bir giriş sunulmaktadır.
author: philmea
ms.author: philmea
ms.date: 7/20/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 9ab4dfb2edd8990692ee3dc134207f43e4c757538dbc738f6f406bf40864bfb3
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116785433"
---
# <a name="azure-rtos-guix-studio-quick-start-guide"></a>Azure RTOS Gux Studio Hızlı Başlangıç Kılavuzu

Bu kılavuzda, Azure RTOS Gux Studio kullanımı hakkında kısa bir giriş sunulmaktadır. gux Studio, Microsoft 'un Azure rtos gux çalışma zamanı kitaplığıyla kullanılmak üzere tasarlanan Windows tabanlı bir kullanıcı arabirimi tasarım uygulamasıdır. 

Bu, ThreadX Real-Time Işletim sistemi (RTOS) ve Azure RTOS Gux UI çalışma zamanı kitaplığını kullanan Embedded gerçek zamanlı yazılım geliştiricisi için tasarlanmıştır. Geliştirici standart Azure RTOS ThreadX ve Azure RTOS Gux kavramlarını tanımanız gerekir.

## <a name="summary"></a>Özet

Azure RTOS Gux Studio, kendi grafik arabirim tasarımınızı oluşturmak, derlemek ve çalıştırmak için ihtiyacınız olan her şeyi içerir. gux Studio 'yu değerlendiriyorsanız, değerlendirme seti, test ve değerlendirme amaçları için tek başına Windows masaüstü uygulaması olarak gux tasarımınızı oluşturup çalıştırmanıza olanak tanımak üzere tasarlanmıştır. GUX, grafik çıkışı olan neredeyse tüm gömülü hedefler üzerinde kullanılmak üzere tasarlandığından, sizin oluşturduğunuz iş ve masaüstünde oluşturduğunuz tasarımlar her zaman bir uygulama yazılımınızı değiştirmeden gömülü hedefte derlenir ve çalıştırılabilir.
GUX Studio yükleyicisi, geliştirme sisteminize birkaç bileşen koyar:

- GUX Studio uygulaması.
- Birkaç Gux örnek projesi.
- Örnek projelerde kullanılan tüm grafik kaynakları ve yazı tipleri.
- Microsoft Visual Studio ıde 'yi kullanarak Windows masaüstü ortamında oluşturmaya yönelik çözüm dosyaları ve proje dosyaları.
- Win32 için önceden oluşturulmuş Gux ve ThreadX kitaplıkları, bilgisayarınızda kendi uygulamalarınızı oluşturmanıza ve çalıştırmanıza olanak tanır.
- GUıDX ve ThreadX API üst bilgi dosyaları.

## <a name="prerequisites"></a>Önkoşullar

Azure RTOS Gux Studio yükleyicisi birkaç basit örnek proje içerir ve Gux Studio uygulamasını nasıl kullanacağınızı öğrendiği için bu örnekleri değiştirerek, oluşturarak ve çalıştırarak başlayacağınızı umuz. Windows masaüstünde örnekleri derlemek ve çalıştırmak için bir Microsoft Visual Studio derleyicisi gerekir. Bu araçlar aşağıdaki konumdan indirilebilir:

https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs#DownloadFamilies_4

Microsoft Geliştirici Araçları yüklü değilse, yine de alana 'yi başlatabilir ve Gux Studio uygulamasını kullanarak kendi arabirim tasarımınızı oluşturabilir ve üretilen kaynak kodunu inceleyebilirsiniz. Ancak, tasarımınızı tek başına bir uygulama olarak derleyip çalıştırameyeceksiniz.

## <a name="running-the-examples"></a>Örnekleri çalıştırma

GUX Studio yükleyicisi 'ni çalıştırdıktan sonra, yüklenen içeriğe birçok örnek bir proje ve derleme dosyası bulacaksınız. Masaüstü araçlarınızın yüklenip düzgün çalıştığını doğrulamak için, belirtilen örneklerin her birini olduğu gibi oluşturup çalıştırarak başlamanızı öneririz. Yükleme dizininize olarak başvuracağız \<root> , bu durumda dosya tarayıcınızı kullanmanız ve \<root> /GUIX_Studio_6. x/örneklere gözatmalısınız. Bu dizin içinde demo_guix_calculator, demo_guix_car_infotainment, demo_guix__home_automation, demo_guix_widget_types ve diğerleri gibi birkaç basit örnek program görmeniz gerekir.

## <a name="building-an-example"></a>Örnek oluşturma

Her örnek klasör içinde *derleme* adlı bir alt dizin bulmanız gerekir. Bu yönde, desteklenen her araç zinciri için önceden yapılandırılmış projeler bulunur. örneğin, \<root> /GUIX_Studio_6. x/örneklerine/termometre/build/vs_2019 öğesine gidebilir; önceden yapılandırılmış bir Microsoft Visual Studio çözüm dosyası ve proje dosyası, Visual Studio ıde 'de yüklenmeye ve çalıştırmaya hazırlanacaktır. Farklı bir araç zinciri kullanmak istiyorsanız [azure_rtos_support](https://docs.microsoft.com/azure/azure-portal/supportability/how-to-create-azure-support-request#create-a-support-request)başvurun.

Microsoft Visual C++ ıde 'yi başlatıp bu örneklerden en az birini açmanız önerilir. \<F7>Örnek projeyi derlemek için anahtara basın ve \<F5> başarıyla oluşturulduktan sonra programı çalıştırmak için tuşuna basın. Artık bir Microsoft Windows penceresi içinde çalışan bir Gux Kullanıcı arabirimi görmeniz gerekir.

## <a name="designing-and-running-your-own-user-interface"></a>Kendi Kullanıcı arabiriminizi tasarlama ve çalıştırma

Bu hızlı başlangıç kılavuzu, Gux Studio Kullanıcı Kılavuzu veya GUıDX Kullanıcı kılavuzunun yerini almaz, ancak daha ayrıntılı bilgi için, başlamanıza ve Gux Studio Kullanıcı kılavuzuna başvurarak devam etmeniz önerilir.

Kendi Kullanıcı arabiriminizi oluşturmak ve değiştirmek için iki yöntem vardır. GUX kitaplığı programlama el ile yeniden çalışabilir ve tasarımınızı tam olarak uygulamak için Gux API 'sini doğrudan uygulama yazılımınız içinden kullanabilirsiniz. Daha sık, ekran öğelerinizin tasarımını ve yerleşimini oluşturmak için Gux Studio uygulamasını kullanacaksınız ve ardından kullanıcı arabiriminizin gerçek iş gerçekleştirmesini sağlamak için gereken olay işlemesini ve diğer uygulama mantığını tamamlayacak.

Belirtilen örneklerin her biri, GUıDX Studio arabirimi tasarım uygulaması kullanılarak oluşturulmuştur. GUX Studio yükleyicisi 'ni çalıştırdıktan sonra Gux Studio 6. x. x. x için masaüstünüzde bir simgeye sahip olmanız gerekir.  GUX Studio 'Yu şimdi başlatın ve "demo_guix_widget_types \ guix_widget_types. GXP" adlı projeyi açın. *Widget_types* demo, en YAYGıN Gux pencere öğesi türlerinin birçok çeşitlemelerini gösteren örnek bir projem.

artık bir proje açık olduğuna göre, ıde 'nin sol üst köşesindeki Project görünümünde "birincil" adlı ağaç düğümünü açmak için "+" düğmesine tıklayın ve bu klasörde "Menu_Screen" adlı en üst düzey pencereye tıklayın. Projeniz aşağıda gösterildiği gibi görünmemelidir:

![Projenin açık olduğu Studio ekran görüntüsü.](./media/guix-studio/qs_project_open.png)

## <a name="guix-studio-views"></a>GUX Studio görünümleri

GUX Studio IDE çeşitli ***görünümlerden*** oluşur. Her görünüm, tasarımınızda gezinirken ve bu tasarıma değişiklikler yapmaya yardımcı olmak için tasarlanmıştır.

### <a name="project-view"></a>Project Görünümü

sol üst görünüme Project görünümü denir. Bu görünüm, projenize dahil edilen fiziksel ekranların her birini gösterir (çoğu proje yalnızca bir ekrana sahiptir) ve bu ekranda çalışmak üzere tasarlanan ekranlar ve alt pencere öğeleri görüntülenir.

### <a name="properties-view"></a>Özellikler Görünümü

Project görünümünün altında özellikler görünümü bulunur. Ad özellikleri görünümü gösterdiği gibi, bu görünüm kendileriyle ilişkili çeşitli özellikleri değiştirerek pencere öğelerini değiştirmenize olanak sağlar.

### <a name="target-view"></a>Hedef görünüm

Merkezi görüntü alanına hedef görünüm denir. Bu görünüm, Kullanıcı arayüzün WYSıWYG görünümüdür. GUX kitaplığı hedef görünüm içinde çizim yaptığından, bu görünüm, tasarımınızın gömülü hedefte yürütme sırasında nasıl görüneceğine ilişkin piksel doğru bir gösterimidir. Project görünümünde ya da merkezi hedef görünümünde farklı pencere öğeleri ' ne tıklarsanız, seçtiğiniz pencere öğesinin özelliklerini görüntülemek için özellikler görünümü değiştiğinde görüntülenen değerleri görürsünüz.

### <a name="resource-view"></a>Kaynak Görünümü

Son olarak, sağda Kaynak Görünümü olarak adlandırılan öğeleri görürsünüz. Bu görünüm, projenize dahil edilen renkleri, yazı tiplerini, pixelharitaları ve dizeleri seçmenizi, eklemenizi, silmenizi ve değiştirmenizi sağlar.

## <a name="modifying-the-example"></a>Örneği değiştirme

GUX Studio sezgisel olacak şekilde tasarlanmıştır. Yukarıda gösterilen pencere öğelerinin birini taşımak için, hedef görünümde o pencere öğesine tıklayıp yeni bir konuma sürüklemeniz yeterlidir. Pencere öğesi renklerini değiştirmek için, istenen pencere öğesine tıklayıp Özellikler görünümünde görüntülenecek renkleri değiştirirsiniz. Metin görüntüleme pencere öğesi tarafından kullanılan yazı tipini değiştirmek için Kaynak Görünümü içindeki istenen yazı tipine tıklayıp, yazı tipini istediğiniz hedef pencere öğesine sürükleyip bırakabilirsiniz. Her bir düğmenin gerçekleştirdiği işlemle ilgili hızlı yardımı görmek için farenizi araç çubuğu düğmeleri üzerinde kaydırın.

Kendiniz deneyin ve örnekte küçük değişiklikler yapın. Örneğin, bir pencere öğesini yeni bir konuma sürükleyebilir, bir pencere arka plan rengini değiştirebilir veya bir düğmeyi yeniden boyutlandırabilirsiniz. Pencere öğelerinin silinmesi, uygulama kaynak kodunda ilişkili değişikliklere ihtiyaç duyduğu için, bu örnekteki Pencere öğelerinin herhangi bir pencere öğesi tarafından silinmesini önermiyoruz.

## <a name="running-the-application-within-studio"></a>Uygulamayı Studio 'da çalıştırma

Düzenle 'yi kullanabilirsiniz | Uygulamayı yeni bir masaüstü penceresinde hemen çalıştırmak için uygulama menü komutunu çalıştırın (veya düğme çubuğunda uygulama düğmesini çalıştırın). Özel çizim işlevleri ve diğer uygulama kodu bu yöntem kullanılarak çağrılmaz, ancak kullanıcı arabirimi tasarımınızda hızlıca gezinmenize ve bir ekrandan diğerine gezinme de dahil olmak üzere uygulamanın genel bir fikrini almanızı sağlar.

## <a name="generating-source-files"></a>Kaynak dosyaları oluşturma

Değişikliklerinizi yaptıktan sonra, projeniz için yeni kaynak dosyaları oluşturmak üzere Gux Studio menü komutlarını çağırmanız gerekir. Sonra değişikliklerinizi eylemde görmek için örnek programı yeniden oluşturabilirsiniz. Kaynak dosyaları oluşturmak için, Gux Studio menü komutlarını kullanın Project | Kaynak dosyaları ve Project oluştur | belirtim dosyaları oluştur (ayrıca bu komutları yürütmek için Project görünümünde görüntüle ' ye sağ tıklayabilirsiniz).

Bu yeni kaynak dosyaları oluştururken, projenizle ilişkili kaynak dosyalarının güncelleştirildiğini bildiren bir onay iletisi gözlemleyebilirsiniz. Bu onay iletisini gözlemlemeyin, projenin bulunduğu dizine yazma izinleriniz olduğundan emin olun. Artık Gux Studio uygulamasını kapatabilirsiniz. Projede değişiklik yaptıysanız, GUıDX Studio bu değişiklikleri kaydetmek isteyip istemediğinizi sorar. Devam edin ve değişikliklerinizi kaydedin. Bu örnekler, Gux Studio 'Yu kullanmayı öğrenerek ' yi kullanarak ve ile denemeler yapmayı amaçlar.

### <a name="building-and-running-the-application"></a>Uygulamayı derleme ve çalıştırma

Artık Gux Studio proje çıktı dosyalarınızı ürettiğinden, tek başına bir Win32 yürütülebilir dosyası oluşturmak için derleyip bağlayabilirsiniz. Ayrıca, uygulamanızda tanımladığınız herhangi bir özel çizimi veya olay işlemesini eklemek için, Gux Studio tarafından oluşturulan çıkış dosyalarını kendi uygulama yazılımınızla derleyip bağlamanız gerekir. Microsoft Visual C++ araç zincirini bir örnek olarak kullanacağız, ancak hedeflediğiniz hedef için derleme yapıyorsanız ve çalıştırırsanız, tam olarak aynı yordamın kullanılması gerekir.

- MSVC ıde 'yi başlatın ve çözümü \<root> /GUIX_Studio_5. x/örnekleri/demo_guix_widget_types/build/vs_2019/guix_widget_types. sln dosyasını açın.

- \<F7>Çözümü yeniden derlemek için anahtarı kullanın.
- \<F5>Programı çalıştırmak için anahtarı kullanın.
 
Artık çalışan programı, Studio 'da yaptığınız değişikliklerle birlikte görmeniz gerekir!

### <a name="learning-more"></a>Daha Fazla Bilgi

**Gux Studio Kullanıcı Kılavuzu** , [azrtos-Gux-Studio-User-Guide](https://docs.microsoft.com/azure/rtos/guix/about-guix-studio)' da kullanılabilir. GUX Studio Kullanıcı Kılavuzu, Gux Studio kullanımı için çok daha kapsamlı bir kılavuzdur.

Ayrıca, **Guıdx Kullanıcı Kılavuzu** , [azrtos-Gux-User-Guide](https://docs.microsoft.com/azure/rtos/guix/about-guix)' da kullanılabilir.  Bu kılavuz, Gux uygulamanız yürütüldüğünde "temel altında" neler olduğu hakkında daha ayrıntılı bilgi sağlar. GUIX çalışma zamanı kitaplığının ve GUIX Studio'nun özelliklerini tam olarak kullanmak için bu kılavuzlardan her ikisini de başvurabilirsiniz.

## <a name="customer-support-center"></a>Müşteri Destek Merkezi

Buradaki adımları kullanarak sorularınız veya yardım için lütfen Azure Portal üzerinden bir destek bileti gönderin. Destek isteğinizi daha verimli bir şekilde çözüme kavuşturmamızı sağlamak için bize bir e-posta iletisinde aşağıdaki bilgileri girin:

- Oluşma sıklığı ve güvenilir bir şekilde nasıl yeniden üretilil olduğu da dahil olmak üzere sorunun ayrıntılı açıklaması.
- Soruna neden olan izleme dosyasını iliştirin.
- Kullanmakta Azure RTOS GUIX Studio'nun sürümü (ekranın sol üst kısmında gösterilir).
- _gx_version_idstring Azure RTOS değişkenini dahil olmak üzere **kullanmakta _gx_version_idstring** GUIX **_gx_build_options** sürümü.
