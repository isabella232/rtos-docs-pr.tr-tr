---
title: GUX Studio tarafından oluşturulan kod
description: Ekranlarınızı ve kaynaklarınızı düzenledikten sonra, GUıDX Studio, katıştırılmış uygulamanıza eklenebilen bir çıktı dosyaları kümesi oluşturur.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: f8868ec770aa8f7f35d2866b99e3eb8f501281a8
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104827130"
---
# <a name="chapter-6-guix-studio-generated-code"></a>Bölüm 6: Gux Studio tarafından oluşturulan kod

Ekranlarınızı ve kaynaklarınızı düzenledikten sonra, GUıDX Studio, katıştırılmış uygulamanıza eklenebilen bir çıktı dosyaları kümesi oluşturur. Çıktı dosyaları, Proje menü öğesinden ***kaynak dosyaları oluştur** _ ve _ *_Özellikler oluştur_** seçilerek oluşturulur. GUX Studio tarafından oluşturulan ' c ' dil kaynak kodu dosyalarının derlenmesi ve katıştırılmış uygulama kaynak kodu ile bağlanması amaçlanmıştır. İkili biçimli bir kaynak dosyası üretildiyse, bu dosya hedefteki geçici olmayan bir depolama alanına ve Gux API işlevine programlanmış olmalıdır gx_binres_theme_install çalışma zamanında ikili kaynakları yüklemek için kullanılmalıdır.

Kullanıcının katıştırılmış uygulama kodu, GUıDX Studio tarafından oluşturulan koda başvurular yapar. Ayrıca, GUıDX Studio tarafından oluşturulan kod, projede belirtilen tüm özel pencere öğesi çizimini, olay işlemesini ve bellek ayırma işlevlerini kullanıcının katıştırılmış uygulama kodunda tanımlanacak şekilde bekler. Aksi takdirde, uygulama oluşturulurken bağlantı hataları mevcut olacaktır.

> [!NOTE]
> Kullanıcının, GUıDX Studio tarafından oluşturulan kodu değiştirmek zorunda olmaması ve bunu yeniden yapabilmesi gerekir. Tüm UI değişiklikleri ilişkili Gux Studio projesinde yapılmalıdır. Bu, projeyi katıştırılmış uygulamayla eşitlenmiş halde tutar.

## <a name="generating-resource-files"></a>Kaynak dosyaları oluşturuluyor

GUX Studio tarafından oluşturulan kaynak dosyaları, projenin ***kaynak görünümü*** tanımlanan tüm kaynakları etkili bir şekilde belirleyen tüm guıdx Studio kaynaklarını (renkler, yazı tipleri, pixelmaps ve dizeler) tanımlayan önceden ayarlanmış veri yapıları içerir. Bu kaynak dosyaları, kaynak kodu veya ikili formlarda oluşturulabilir.

Varsayılan olarak, bir dosya standart C kaynak kodu dosyasıdır ve diğeri, uygulama kodunun projede tanımlanan Gux kaynaklarına erişmesi için gerekli olan dış başvurular ve sabitler sağlayan bir C üstbilgi dosyasıdır. Dosya adları şu biçimdedir:

**{*Proje-adı*} _Resources. h**

**{*Proje-adı*} _Resources. c**

Örneğin, "***basit***" Gux Studio projesi Için oluşturulan kaynak dosyaları şunlardır:

**simple_resources. h**

**simple_resources. c**

Kaynak dosyalarını oluşturma işlemi, _*_Proje_*_ menü seçeneğinde ***kaynak dosyaları oluştur** _ seçeneği belirlenerek gerçekleştirilir. Kaynak dosyalarının hedefi, _ *_Configure_** menü öğesindeki _*_projeyi Yapılandır/görüntüler_*_ seçeneği aracılığıyla erişilebilen _*_Proje yapılandırma_*_ iletişim kutusunda belirtilir.

Pixelmap ve Font kaynakları için, ilişkili kaynak düzenlemesi iletişim kutularındaki her bir pixelmap ve yazı tipi için özel bir çıktı dosya adı belirtebilirsiniz. Bu özellik, tüm kaynakları tek bir ortak çıkış dosyasına koymak yerine, çok büyük kaynakları ayrı dosyalara eklemenizi sağlar. Bir font veya pixelmap kaynağı için geçersiz kılınan bir dosya adı belirtmezseniz, bu kaynaklar ortak kaynak dosyasına yazılır.

İkili kaynakları kullanmayı tercih ediyorsanız, ham veya Standart s-kayıt çıkış biçimini belirtebilirsiniz. İkili kaynaklar, uygulama koduyla derlenmez veya bağlanamaz, ancak bunun yerine gx_binres_them_load () API 'sini kullanarak çalışma zamanında yüklenir. Bu API hizmeti, geçici olmayan bellekte depolanan kaynaklarınızı işaret eden kaynak tabloları oluşturur. Daha sonra, gx_display_theme_install () kullanarak bu kaynakları belirli bir görüntüleme ile yükleyebilirsiniz.

## <a name="generating-specification-code"></a>Belirtim kodu üretiliyor

GUX Studio tarafından oluşturulan belirtim dosyaları, Gux Studio 'da tasarlanan kullanıcı arabirimini oluşturmak için tüm C kodlarını içerir. Bu kod ayrıca bu proje için oluşturulan kaynak dosyalarına da başvurur. Kullanıcının uygulama kodu, projede tanımlanan UI nesnelerini gerçekten oluşturmak için bu koda çağrı yapar. Ayrıca, kullanıcının uygulama kodu, projede belirtilen tüm özel pencere öğesi çizimini, olay işlemesini ve bellek ayırma işlevlerini içerir. Varsayılan olarak, bir dosya standart C kaynak kodu dosyasıdır ve diğeri, uygulama kodunun Gux Studio belirtimlerine erişmesi için gerekli olan dış başvurular ve sabitler sağlayan bir C üstbilgi dosyasıdır. Dosya adları şu biçimdedir:

**{*Proje-adı*} _specifications. h**

**{*Proje-adı*} _specifications. c**

Örneğin, "***Simple***" Gux Studio projesi Için oluşturulan belirtim dosyaları şunlardır:

**simple_specifications. h**

**simple_specifications. c**

Belirtim dosyalarını oluşturma işlemi, _*_Proje_*_ menü seçeneğinde ***Belirtim dosyaları oluştur** _ seçeneği belirlenerek gerçekleştirilir. Belirtim dosyalarının hedefi, _ *_Configure_** menü öğesindeki _*_projeyi Yapılandır/görüntüler_*_ seçeneği aracılığıyla erişilebilen _*_Proje yapılandırma_*_ iletişim kutusunda belirtilir.

## <a name="integrating-with-user-code"></a>Kullanıcı koduyla tümleştirme

GUX Studio tarafından oluşturulan kaynak ve belirtim dosyalarını tümleştirme özelliği basittir, yalnızca aşağıdaki adımları izlemeniz gerekir:

1. Kaynak ve belirtim dosyalarını, yol ayarları aracılığıyla gömülü derleme ortamına erişilebilir yapın veya kopyalayın.
2. Tüm kaynak ve belirtim dosyalarını katıştırılmış IDE projesine veya derleme görevleri dosyasına ekleyin
3. Uygulama Embedded kodunun, kaynak ve belirtim dosyalarında yer alan Kullanıcı arabirimini başlatmak ve oluşturmak için gerekli işlevleri çağırdığından emin olun
4. Uygulama Embedded kodunun tüm gerekli özel pencere öğesi çizimini, olay işlemesini ve bellek ayırma işlevlerini içerdiğinden emin olun
5. Uygulamayı oluşturma (Derle ve bağla)
6. Uygulamayı yürütün!