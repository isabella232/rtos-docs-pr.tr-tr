---
title: Basit örnek proje
description: Bu bölümde, GUıDX Studio 'da örnek projenin nasıl oluşturulduğu ve Gux üzerinde örnek yürütülmesi açıklanmaktadır.
author: jdeere5220
ms.author: kemaxwel
ms.date: 9/30/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 3661396f097e0ed7bd872fae01a7bec9212001b9
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826428"
---
# <a name="chapter-10-example-project"></a>Bölüm 10: örnek proje

Bu bölümde, GUıDX Studio 'da örnek projenin nasıl oluşturulduğu ve Gux üzerinde örnek yürütülmesi açıklanmaktadır.

## <a name="create-new-project"></a>Yeni Proje Oluştur

İlk adım yeni bir proje oluşturuyor ve projenin destekleyeceği ekranları ve dilleri yapılandırıyor. GUX Studio 'Yu ilk kez başlattığınızda, ***son projeler*** ekranını görürsünüz:

![GUX Studio son projeler iletişim kutusunun ekran görüntüsü.](./media/guix-studio/recent_projects.png)

**Şekil 10,1**

***Yeni proje oluştur** _... öğesine tıklayın. düğmesini başlatın. Burada gösterilen _ *_New GUıDX projesi_** iletişim kutusu görüntülenir:

![GUX Studio yeni proje oluştur iletişim kutusunun ekran görüntüsü.](./media/guix-studio/create_new_project.png)

**Şekil 10,2**

Proje adı olarak "***new_example***" adını yazın. Proje adları, standart C değişken adlandırma kuralları, yani özel veya ayrılmış karakter kullanmalıdır. Projenin kaydedileceği konumun yolunu yazın. Yolun geçerli bir dosya sistemi dizini olması gerekir, diğer bir deyişle, yoksa Gux Studio dizini oluşturmaz. Projeyi oluşturmak için "Tamam" a tıklayın.

Gösterilen sonraki ekran, burada gösterilen proje yapılandırma ekranıdır:

![GUX Studio proje yapılandırma iletişim kutusunun ekran görüntüsü.](./media/guix-studio/config_new_project.png)

**Şekil 10,3**

Bu iletişim kutusu, projenizin kaç tane görüntülediğini belirtmenizi ve her bir görüntü için bir ad vermenizi sağlar. Her bir ekran tarafından desteklenen renk biçimini belirtmeniz gerekir ve isteğe bağlı olarak her bir ekran için Studio tarafından oluşturulan çıkış dosyaları için bir yol adı yazın. Çıkış dosyaları için varsayılan dizin "***. \\***", yani C çıktı dosyaları projenin kendisiyle aynı dizine yazılır.

Bu örnekte, * ekran **sayısı** _ ' i "1" olarak ayarlayın, görünen ad alanına "_*_main_display_*_" adını yazın ve "_*_tuval belleğini ayır_*_" seçeneğini işaretleyin. Çözümleme, renk biçimi ve dizin alanlarını varsayılan değerlerinde bırakın ve _ *_Tamam_* * öğesine tıklayın.

Artık Şekil 10,4 ' de gösterildiği gibi, projenizi Studio IDE ile açık olarak görmeniz gerekir:

![Studio IDE ile açılmış projenin ekran görüntüsü.](./media/guix-studio/initial_screen.png)

**Şekil 10,4**

Yeni bir proje oluşturduğunuzda, GUıDX Studio otomatik olarak projeniz için başlangıç noktası olarak varsayılan bir pencere oluşturur. Bu gri kutu, sizin için oluşturulan varsayılan pencere, *hedef görünüm* içinde ortalandı.

Bu pencere seçili değilse, pencerenin çevresine kesikli seçim kutusu çizilmek üzere pencereye tıklayın. Şimdi ***Özellikler Görünümü** _ ' de, _*_pencere öğesi adı_*_, _*_pencere öğesi kimliği_*_, _*_sol_*_, _*_üst_*_, _*_Genişlik_*_, _*_Yükseklik_*_ ve _ *_Border_** öğesini aşağıda gösterilen ayarlarla eşleşecek şekilde değiştirin. Bu değişiklikleri yaparken, değişikliklerinizin hedef görünümde hemen etkili olduğunu görmeniz gerekir.

![Özellikler Görünümü iletişim kutusunun ekran görüntüsü.](./media/guix-studio/initial_window_properties.png)

**Şekil 10,5**

Bir sonraki adımda, bir ***GX_ICON** _ pencere öğesi içinde kullanılacak bir pixelmap kaynağı ekleyeceğiz. Bu örnekte ince çalışacak şekilde Gux Studio dağıtımlarınız ile çeşitli simgeler sağlanır. _*_Pixelmaps_*_ kaynak görünümü genişletin ve _ *_Yeni pixelmap Ekle_** düğmesine tıklayın:

![Yeni pixelmap Ekle düğmesinin ekran görüntüsü.](./media/guix-studio/image74.jpg)

GUX Studio yükleme klasörünüze gidin ve ***./Graphics/simgeler** _ klasörü içinde _*_i_history_lg.png_*_ adlı dosyayı seçin. Bu kaynağı projenize eklemek için _*_Aç_*_ ' a tıklayın. _ *_Pixelmaps_** kaynak görünümü artık yeni eklenen simge görüntüsünün önizlemesini göstermelidir:

![Pixelmaps Kaynak Görünümü ekran görüntüsü.](./media/guix-studio/example_add_pixelmap.png)

**Şekil 10,6**

Bu yeni görüntü kaynağını daha sonra UI tasarımımızın bir parçası olarak kullanacağız.

Bir pixelmap kaynağı eklemeye benzer şekilde, bu yazı tipini tasarımımızda daha sonra kullanabilmemiz için araç kutusu 'na yeni bir yazı tipi kaynağı ekleyeceğiz. ***Fonts** _ kaynak görünümü genişletin ve _*_Yeni yazı tipi Ekle_*_ düğmesine tıklayın. Bu eylem, yazı tipi _*_Ekle/Düzenle_*_ iletişim kutusunu çağırır. Ardından, Gux Studio yükleme klasöründe sunulan Gux yazı tiplerine gidin _*_ . \\ yazı tipleri \\ _ verasans_ ve _ _veraıt. ttf_*adlı TrueType yazı tipi dosyasını seçin**_._* Yazı tipi adı alanına "_MEDIUM_ITALIC_*_"_* yazı tipini yazın ve yükseklik alanına "_30_* *" yazın. İletişim kutusu artık şöyle görünmelidir:

![Yazı tipi düzenleme iletişim kutusunun ekran görüntüsü.](./media/guix-studio/example_add_font.png)

**Şekil 10,7**

Bu yazı tipini projenize eklemek için ***Tamam*** ' ı tıklatın. Artık Kaynak Görünümü yazı tipini görmeniz gerekir:

![Kaynak Görünümü yazı tiplerinin ekran görüntüsü.](./media/guix-studio/example_font_added.png)

**Şekil 10,8**

Bu yeni yazı tipini, Kullanıcı arabirimi tasarımımızda daha sonra kullanacağız.

Artık yeni kaynakların mevcut olduğuna göre, bu kaynakları kullanan ekranlarımıza bazı alt pencere öğeleri eklememiz gerekiyor. Hedef görünümdeki pencereye sağ tıklayarak "***hello_world** _" adlı önceden oluşturulmuş pencereyi seçin. Artık görüntülenen açılır menüde, yeni bir _ *_GX_PROMPT_** pencere öğesi eklemek ve pencere öğesini arka plan penceresine eklemek için menü komutunu _*_Ekle, metin, komut istemi_*_ ' ni seçin. Pencereniz şu şekilde görünmelidir:

![Istem seçimine sahip bir açılan menünün ekran görüntüsü](./media/guix-studio/image78.jpg)

**Şekil 10,9**

_ *_Fonts_** kaynak görünümü içindeki "***MEDIUM_ITALIC** _" adlı yazı tipine tıklayın ve yazı tipini komut istemi pencere öğesine sürükleyin ve bırakın. Sonra, istemi yeniden boyutlandırmak, istem saydamlığını ayarlamak ve istem metnini ve stilini değiştirmek için Şekil 10,10 ' de gösterilen istem özelliklerini düzenleyin:

![İstem için özellikler görünümünün ekran görüntüsü.](./media/guix-studio/image79.jpg)

**Şekil 10,10**

Bu ayarların her birini ekran çözünürlüğünüzle ilgili olarak görmek için Özellikler görünümünde dikey olarak kaydırma yapmanız gerekebilir. Bu değişiklikleri yaptıktan sonra, hedef görünümlerinizin şu şekilde görünmesi gerekir:

![Merhaba Dünya seçime sahip bir açılır menünün ekran görüntüsü.](./media/guix-studio/image80.jpg)

**Şekil 10,11**

Daha sonra ekrana bir simge düğme stili pencere öğesi yerleştireceğiz. Üzerine tıklayarak arka plan penceresini seçin ve pencereye yeni bir _*_GX_ICON_BUTTON_*_ eklemek için en üst düzey menü veya sağ tıklama açılan menüsünü kullanın. (**Ekle, düğme, simge düğmesi** _) seçeneğini belirleyin. Daha önce eklediğimiz _ *_I_HISTORY_LG_** adlı simgeye tıklayın ve simgeyi simge düğmesine sürükleyin. Özellikler görünümünü kullanarak, simge konumunu ve boyutunu aşağıda göster olarak ayarlayın:

![Simge düğmesi stili pencere öğesi için özellikler görünümünün ekran görüntüsü.](./media/guix-studio/image81.jpg)

**Şekil 10,12**

Ekranınız şu şekilde görünmelidir:

![Merhaba Dünya ve Pano simgesiyle açılan menünün ekran görüntüsü.](./media/guix-studio/image82.jpg)

**Şekil 10,13**

Bu, basit örnek ekran tasarımı için bu tamamlamayı arayacağız. Gerçek uygulama ekranlarınız büyük olasılıkla çok daha karmaşık olacaktır, ancak bu, kendi uygulama ekranlarınızı oluşturmak için Gux Studio 'Yu nasıl kullanacağınızı göstermek için yeterlidir.

## <a name="generate-resource-and-application-code"></a>Kaynak ve uygulama kodu oluştur

Sonraki adım, katıştırılmış Gux çalışma zamanı Kullanıcı arabirimini tanımlayan kaynak dosyası ve belirtim dosyası oluşturmak için kullanılır. Çıkış dosyalarınızı oluşturmak için proje görünümündeki ***main_display** _ düğümüne sağ tıklayıp _ *_kaynak dosyaları oluştur_** komutunu seçmeniz gerekir. Şekil 10,14 ' de gösterildiği gibi, kaynak dosyalarınızın oluşturulduğunu belirten bir bilgi penceresi gözlemleyeceksiniz:

![Bildirim iletişim kutusunun ekran görüntüsü.](./media/guix-studio/image83.jpg)

**Şekil 10,14**

Bu bildirimi kapatmak için ***Tamam** _ ' e tıklayın ve _*_main_display_*_ düğümüne sağ tıklayıp _ *_Belirtim dosyaları oluştur_** komutunu seçerek aynı yordamı kullanın. Benzer bir bildirim penceresi gözlemleyebilirsiniz. Basit UI uygulama dosyalarınızı oluşturdunuz.

## <a name="create-user-supplied-code"></a>Kullanıcı tarafından sağlanan kod oluştur

Sonraki adım, Gux Studio tarafından üretilen ekran tasarımını çağırabilecek kendi uygulama dosyanızı oluşturmaktır. Tercih ettiğiniz düzenleyiciyi kullanarak, ***new_example. c*** adlı bir kaynak dosya oluşturun ve bu dosyaya aşağıdaki kaynak kodu girin:

```C

/* This is an example of the GUIX graphics framework in Win32. */
/* Include system files. */

#include <stdio.h>
#include "tx_api.h"
#include "gx_api.h"

/* Include GUIX resource and specification files for example. */

#include "new_example_resources.h"
#include "new_example_specifications.h"

/* Define the new example thread control block and stack. */

TX_THREAD new_example_thread;
UCHAR new_example_thread_stack[4096];

/* Define the root window pointer. */

GX_WINDOW_ROOT *root_window;

/* Define function prototypes. */

VOID new_example_thread_entry(ULONG thread_input);
UINT win32_graphics_driver_setup_24bpp(GX_DISPLAY *display);

int main()
{
    /* Enter the ThreadX kernel. */
    tx_kernel_enter();
    return(0);
}

VOID tx_application_define(void *first_unused_memory)
{
    /* Create the new example thread. */
    tx_thread_create(&new_example_thread, "GUIX New Example Thread", 
                      new_example_thread_entry, 0, 
                      new_example_thread_stack, sizeof(new_example_thread_stack),
                      1, 1, TX_NO_TIME_SLICE, TX_AUTO_START);
}

VOID new_example_thread_entry(ULONG thread_input)
{

    /* Initialize the GUIX library */
    gx_system_initialize();

    /* Configure the main display. */
    gx_studio_display_configure(MAIN_DISPLAY,                      /* Display to configure*/
                                win32_graphics_driver_setup_24bpp, /* Driver to use */
                                LANGUAGE_ENGLISH,                  /* Language to install */
                                MAIN_DISPLAY_DEFAULT_THEME,        /* Theme to install */
                                &root_window);                     /* Root window pointer */

    /* Create the screen - attached to root window. */

    gx_studio_named_widget_create("hello_world", (GX_WIDGET *) root_window, GX_NULL);

    /* Show the root window to make it visible. */
    gx_widget_show(root_window);

    /* Let GUIX run. */
    gx_system_start();

}
```

Yukarıdaki kaynak kodu, `GUIX New Example Thread` 4k baytlık yığın boyutuyla adlı tipik bir ThreadX iş parçacığı oluşturur. İlginç işler ***new_example_thread_entry*** adlı işlevde başlar. Bu işlev, Gux 'e özgü iş parçacığının çalışmaya başladığı yerdir.

İlk çağrı ***gx_system_initialize*** adlı işleve yapılır. Bu çağrı, Gux kitaplığını ilk kullanım için hazırlamak üzere diğer bir GUıDX API 'Leri çağrılmadan önce her zaman gereklidir.

Sonra, örnek ***gx_studio_display_configure*** işlevini çağırır. Bu işlev, GUıDX görüntüleme örneğini oluşturur, uygulama dizesi tablosunun istenen dilini yüklerse, istenen temayı görüntüleme kaynaklarından yüklerse ve bu görüntü için oluşturulan kök penceresine bir işaretçi döndürüyor. Kök pencere, uygulamamız görüntülenecek olan tüm üst düzey ekranların üst öğesi olarak kullanılır.

Daha sonra örnek, _ *_hello_world_** ekranımız bir örnek oluşturmak için ***gx_studio_named_widget_create** _ ' i çağırır. Bu işlev, tanımladığımız bir ekran örneği oluşturmak için Gux Studio tarafından ürettiği veri yapılarını ve kaynağını kullanır. Bu işlev çağrısına ikinci parametre olarak kök pencere işaretçisini geçirdik, yani ekranın kök pencereye hemen eklenmesini istiyoruz. Son parametre, oluşturulan ekrana bir işaretçi tutmak istiyorsam kullanılabilecek, isteğe bağlı bir dönüş işaretçisidir.

Next ***gx_widget_show** _ çağrılır, bu, kök pencereyi ve tüm alt öğelerini _ *_hello_world_** ekranı gibi görünür hale getirir.

Son olarak, örnek ***gx_system_start*** çağırır. Bu işlev, GUıDX sistem olay işleme döngüsünü yürütmeye başlıyor.

## <a name="build-and-run-the-example"></a>Örneği derleyin ve çalıştırın

Örnek oluşturma ve çalıştırma, derleme araçlarınız ve ortamınıza özeldir. Ancak genel işlemi tanımlayabiliriz:

1. Yeni bir dizin ve uygulama projesi oluşturma
1. Bu dosyaları projeye ekleyin:

    **new_example_resources. c**

    **new_example_specification. c**

    **new_example. c**

1. GUX Studio yükleme yolundan Win32 çalışma zamanı destek dosyalarını ekleyin ***./win32_runtime***. Bu, ThreadX ve GUıDX Win32 üst bilgisini ve çalışma zamanı kitaplık dosyalarını içerir.
1. GUX Win32 kitaplığı 'nı (***GX. lib***) projeye ekleme
1. Projeye ThreadX Win32 kitaplığını (***TX. lib***) ekleme
1. Uygulamayı derleyin, bağlayın ve çalıştırın!
