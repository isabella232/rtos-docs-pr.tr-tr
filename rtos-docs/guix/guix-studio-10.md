---
title: Basit Örnek Project
description: Bu bölümde GUIX Studio'da örnek bir proje oluşturma ve örneği GUIX'te yürütme açık bir şekilde anlattır.
author: jdeere5220
ms.author: kemaxwel
ms.date: 9/30/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 8981bed62d2929703e4233d6a3ee31b692226c26d046875a235bf3aca32a7573
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116786660"
---
# <a name="chapter-10-example-project"></a>Bölüm 10: Örnek Project

Bu bölümde GUIX Studio'da örnek bir proje oluşturma ve örneği GUIX'te yürütme açık bir şekilde anlattır.

## <a name="create-new-project"></a>Yeni Proje Oluştur

İlk adım yeni bir proje oluşturmak ve projenin destekleyecek ekranları ve dilleri yapılandırmaktır. GUIX Studio'yu ilk kez başlatacak olurken Son Projeler ***ekranı*** görüntülenir:

![GUIX Studio Son Projeler iletişim kutusunun ekran görüntüsü.](./media/guix-studio/recent_projects.png)

**Şekil 10.1**

* Yeni Oluştur **_... Project** tıklayın düğmesine tıklayarak yeni bir proje başlatabilirsiniz. Burada gösterilen _ Yeni *_GUIX Project_** iletişim kutusu gösterilir:

![GUIX Studio Yeni Uygulama Oluştur iletişim kutusunun Project görüntüsü.](./media/guix-studio/create_new_project.png)

**Şekil 10.2**

Proje adı olarak "***new_example***" yazın. Project adları, özel veya ayrılmış karakter olmayan standart C değişken adlandırma kuralları kullanmalıdır. Projenin kaydedilebilir olduğu konumun yolunu yazın. Yol geçerli bir dosya sistemi dizini olmalıdır, yani guix Studio yoksa dizini oluşturmaz. Projeyi oluşturmak için "Tamam"a tıklayın.

Gösterilen sonraki ekran, Project yapılandırma ekranıdır:

![GUIX Studio Yapılandırma iletişim kutusunun Project görüntüsü.](./media/guix-studio/config_new_project.png)

**Şekil 10.3**

Bu iletişim kutusu, projenizin kaç görüntü destekley desteğine sahip olduğunu belirtmenize ve her görüntüye bir ad vermenizi sağlar. Her ekran tarafından desteklenen renk biçimini belirtmeniz ve isteğe bağlı olarak her görüntü için Studio tarafından oluşturulan çıkış dosyaları için bir yol adı yazmalısiniz. Çıkış dosyalarının varsayılan dizini "***\\ .***" şeklindedir, yani C çıkış dosyaları projenin kendisiyle aynı dizine yazılır.

Bu örnek için ***** Görüntüleme Sayısı _ değerini "1" olarak ayarlayın, görünen ad alanına "_*_main_display_*_" yazın ve " tuval belleği ayır" öğesini _*_kontrol_*_ edin. Çözümleme, renk biçimi ve dizin alanlarını varsayılan değerlerinde bırakın ve _* Tamam _**'a_ tıklayın.

Artık şekil 10.4'te gösterildiği gibi projenizin Studio IDE ile açık olduğunu görüyoruz:

![Studio IDE ile açık bir projenin ekran görüntüsü.](./media/guix-studio/initial_screen.png)

**Şekil 10.4**

Yeni bir proje oluştururken GUIX Studio, projenizin başlangıç noktası olarak otomatik olarak varsayılan bir pencere oluşturur. Bu gri kutu, sizin için oluşturulan varsayılan penceredir ve Hedef Görünüm içinde *ortalar.*

Bu pencere seçili değilse pencereye tıklayın, böylece pencere etrafında kesikli seçim kutusu çizilir. * Özellikler Görünümü **'ne** _, Pencere Öğesi _*_Adı,_*_ _*_Pencere_*_ Öğesi Kimliği , _*_Sol_*_, _*_Üst_*_, _*_Genişlik,_*_ _*_Yükseklik_*_ ve _ *_Kenarlık_** değerini aşağıda gösterilen ayarlarla eş olacak şekilde değiştirin. Bu değişiklikleri yaptığınız sürece, değişikliklerinizin Hedef Görünüm'de hemen etkili olduğunu görüyor olun.

![Özellikler Görünümü iletişim kutusunun ekran görüntüsü.](./media/guix-studio/initial_window_properties.png)

**Şekil 10.5**

Daha sonra * GX_ICON _ pencere öğesi içinde kullanılacak **bir piksel haritası** kaynağı ekleyebilirsiniz. GuiX Studio dağıtımınız ile birlikte bu örnek için uygun olacak çeşitli simgeler sağlanır. Piksel _*_haritalarınızı genişletin Kaynak Görünümü_*_ _ Yeni Piksel Haritası *_Ekle_** düğmesine tıklayın:

![Yeni Piksel Haritası Ekle düğmesinin ekran görüntüsü.](./media/guix-studio/image74.jpg)

GUIX Studio yükleme klasörünüze gidin ve ***./graphics/icons** _ klasöründen _*_i_history_lg.png._*_ Bu _*_kaynağı_*_ projenize eklemek için Aç'a tıklayın. _ *_Pixelmaps_** Kaynak Görünümü şimdi yeni eklenen simge görüntüsünün önizlemesini gösterebilirsiniz:

![Piksel haritalarının ekran Kaynak Görünümü.](./media/guix-studio/example_add_pixelmap.png)

**Şekil 10.6**

Bu yeni görüntü kaynağını daha sonra kullanıcı arabirimi tasarımımızın bir parçası olarak kullanacağız.

Pixelmap kaynağı eklemeye benzer şekilde, bu yazı tipini daha sonra tasarımımızda kullanacağız. ***** Yazı Tipleri _ Kaynak Görünümü ve Yeni Yazı Tipi _*_Ekle düğmesine_*_ tıklayın. Bu eylem Yazı tipi _*_ekle/düzenle iletişim kutusunu_*_ çağırır. Ardından GUIX Studio yükleme klasöründe sağlanan GUIX yazı tiplerini (). _*_ \\ yazı \\ verasans_ _ yazın ve _ _VeraIt.ttf_ adlı *TrueType* yazı tipi dosyasını *_seçin. Yazı tipi adı alanına yazı_* tipi adını "_MEDIUM_ITALIC_" yazın ve yükseklik alanına *_"_*_30_**" yazın. İletişim kutusu şu şekilde görünür:

![Yazı Tipini Düzenle iletişim kutusunun ekran görüntüsü.](./media/guix-studio/example_add_font.png)

**Şekil 10.7**

Bu ***yazı tipini*** projenize eklemek için Tamam'a tıklayın. Artık yazı tipini aşağıdaki gibi Kaynak Görünümü:

![Kaynak Görünümü.](./media/guix-studio/example_font_added.png)

**Şekil 10.8**

Bu yeni yazı tipini daha sonra kullanıcı arabirimi tasarımımızda kullanacağız.

Artık yeni kaynaklara sahip olduğunu göre ekranımıza bu kaynakları kullana bir alt pencere öğesi eklememiz gerekiyor. Hedef Görünüm'de pencereye **sağ tıklayarak**"* hello_world _" adlı önceden oluşturulmuş pencereyi seçin. Şimdi görüntülenen açılır menüde Ekle, Metin, İstem menü komutunu seçerek yeni bir _ *_GX_PROMPT_** pencere öğesi girin ve pencere öğesini arka plan penceresine iliştirin. _**_ Pencereniz şimdi şöyle görünür:

![İstem seçiminin yer alan açılır menüsünün ekran görüntüsü](./media/guix-studio/image78.jpg)

**Şekil 10.9**

_ *_Fonts_** Kaynak Görünümü içinde "***MEDIUM_ITALIC** _" adlı yazı tipine tıklayın ve istemin pencere öğesinde yazı tipini sürükleyip bırakın. Ardından, şekil 10.10'da gösterildiği gibi istemi yeniden boyutlandırmak, istem saydamlığını ayarlamak ve istem metnini ve stilini değiştirmek için istem özelliklerini düzenleyin:

![İstem için Özellikler Görünümü'nin ekran görüntüsü.](./media/guix-studio/image79.jpg)

**Şekil 10.10**

Ekran çözünürlüğüne bağlı olarak bu ayarların her birini görmek için Özellikler Görünümü'ne dikey olarak kaydırmanız gerekebilir. Bu değişiklikleri tamamladikten sonra Hedef Görünüm şu şekilde görüntü gerekir:

![Uygulama seçimiyle birlikte açılan men Merhaba Dünya görüntüsü.](./media/guix-studio/image80.jpg)

**Şekil 10.11**

Daha sonra, ekrana Simge Düğmesi stilinde bir pencere öğesi yer alastırız. Arka plan penceresine tıklayarak arka plan penceresini seçin ve üst düzey menüyü veya sağ tıklama açılan menüsünü kullanarak ***Ekle, Düğme,** Simge Düğmesi _ öğesini seçerek pencereye yeni bir _*_GX_ICON_BUTTON_*_ ekleyin. Daha önce eklemiz _ *_I_HISTORY_LG_** adlı Simgeye tıklayın ve simge düğmesine sürükleyin. Özellikler görünümünü kullanarak simge konumunu ve boyutunu aşağıda olduğu gibi ayarlayın:

![Simge düğmesi stili pencere öğesi için Özellikler Görünümü'nin ekran görüntüsü.](./media/guix-studio/image81.jpg)

**Şekil 10.12**

Ekranınız şimdi şöyle görünür:

![Pano ve pano simgesinin yer Merhaba Dünya menüsünün ekran görüntüsü.](./media/guix-studio/image82.jpg)

**Şekil 10.13**

Basit örnek ekran tasarımı için bu tam olarak çağrılır. Gerçek uygulama ekranlarınızı büyük olasılıkla çok daha karmaşık hale gelecektir, ancak kendi uygulama ekranlarınızı oluşturmak için GUIX Studio'yu nasıl kullanabileceğinizi göstermek için bu yeterlidir.

## <a name="generate-resource-and-application-code"></a>Kaynak ve Uygulama Kodu Oluşturma

Sonraki adım, ekli GUIX çalışma zamanı kullanıcı arabirimini tanımlayan kaynak dosyası ve belirtim dosyasını oluşturmaktır. Çıkış dosyalarınızı oluşturmak için, Project View 'da ***main_display** _ düğümüne sağ tıklar ve *___* Kaynak Dosyaları Oluştur * komutunu seçmeniz gerekir. Şekil 10.14'te gösterildiği gibi kaynak dosyalarınızın oluşturulmuş olduğunu gösteren bir bilgi penceresi gözlemlersiniz:

![Bildirim iletişim kutusunun ekran görüntüsü.](./media/guix-studio/image83.jpg)

**Şekil 10.14**

Bu bildirimi **silmek** için * Tamam _ seçeneğine tıklayın ve _**_ main_display düğümüne sağ tıklar ve *___* Belirtim Dosyaları Oluştur * komutunu seçmek için aynı yordamı kullanın. Benzer bir bildirim penceresi gözlemleyebilirsiniz. Artık basit KULLANıCı arabirimi uygulama dosyalarınızı oluşturabilirsiniz.

## <a name="create-user-supplied-code"></a>Kullanıcı Tarafından Sağlanan Kod Oluşturma

Sonraki adım, GUIX Studio tarafından oluşturulan ekran tasarımını çağıracak kendi uygulama dosyanızı oluşturmaktır. Tercih ettiğiniz düzenleyiciyi kullanarak ***new_example.c*** adlı bir kaynak dosya oluşturun ve bu dosyaya aşağıdaki kaynak kodu girin:

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

Yukarıdaki kaynak kod, yığın boyutu 4K bayt olan adlı tipik bir ThreadX `GUIX New Example Thread` iş parçacığı oluşturur. İlginç iş, new_example_thread_entry ***adlı işlevde başlar.*** Bu işlev, GUIX'e özgü iş parçacığının çalıştırmaya başladığı yerdir.

İlk çağrı, gx_system_initialize ***adlı işleve yapılan çağrıdır.*** Bu çağrı, Gux kitaplığını ilk kullanım için hazırlamak üzere diğer bir GUıDX API 'Leri çağrılmadan önce her zaman gereklidir.

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
