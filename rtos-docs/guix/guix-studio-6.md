---
title: GUIX Studio Tarafından Oluşturulan Kod
description: Ekranlarınızı ve kaynaklarınızı düzenlemeyi tamamlarken GUIX Studio, eklenmiş uygulamanıza ekli bir dizi çıkış dosyası oluşturur.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 78b1ec1eea3ec2fcae48c64ad15931f44f34538c876dc8a267c2b1a84234320a
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116785711"
---
# <a name="chapter-6-guix-studio-generated-code"></a>Bölüm 6: GUIX Studio Tarafından Oluşturulan Kod

Ekranlarınızı ve kaynaklarınızı düzenlemeyi tamamlarken GUIX Studio, eklenmiş uygulamanıza ekli bir dizi çıkış dosyası oluşturur. Çıkış dosyaları, kaynak menü öğesinden ***** Kaynak Dosyaları Oluştur _ ve *___* Belirtimleri Oluştur * Project oluşturulur. GUIX Studio tarafından oluşturulan 'c' dil kaynak kodu dosyalarının derlenmiş ve eklenmiş uygulama kaynak koduyla bağlantılı olması amaçlandı. bir ikili biçim kaynak dosyası üretirse, bu dosya hedefte geçici olmayan bir depolama alanına programlanmış olmalı ve GUIX API işlevi gx_binres_theme_install çalışma zamanında ikili kaynakları yüklemek için kullanılmalıdır.

Kullanıcının ekli uygulama kodu GUIX Studio tarafından oluşturulan koda başvuru yapar. Ayrıca GUIX Studio tarafından oluşturulan kod, projede belirtilen tüm özel pencere öğesi çizimi, olay işleme ve bellek ayırma işlevlerinin kullanıcının ekli uygulama kodunda tanımlanmalıdır. Yoksa, uygulamanın yapılsa bağlantı hataları olur.

> [!NOTE]
> Kullanıcının HIÇBIR zaman GUIX Studio tarafından oluşturulan kodu değiştirmesi ve bunu yapmaya karşı koyması gerekir. Tüm kullanıcı arabirimi değişiklikleri ilişkili GUIX Studio projesinde yapılması gerekir. Bu, projenin eklenmiş uygulamayla eşitlenmiş durumda tutması sağlar.

## <a name="generating-resource-files"></a>Kaynak Dosyaları Oluşturma

GUIX Studio tarafından oluşturulan kaynak dosyaları, tüm GUIX Studio kaynaklarını (renkler, yazı tipleri, piksel haritaları ve dizeler) tanımlayan önceden ayarlanmış veri yapıları içerir ve bu da projenin Kaynak Görünümü kaynakları etkili bir ***şekilde*** sunar. Bu kaynak dosyaları kaynak kodunda veya ikili formlarda oluşturulabilir.

Varsayılan olarak, oluşturulan iki dosya vardır, biri standart bir C kaynak kodu dosyası, diğeri ise uygulama kodunun projede tanımlanan GUIX kaynaklarına erişmesi için gereken dış başvuruları ve sabitleri sağlayan bir C üst bilgi dosyasıdır. Dosya adları şu şekildedir:

**{*proje-adı*}_resources.h**

**{*proje-adı*}_resources.c**

Örneğin, " basit " GUIX Studio projesi ***için*** oluşturulan Kaynak dosyaları:

**simple_resources.h**

**simple_resources.c**

Kaynak dosyaları oluşturma, kaynak menüsü seçeneğinde ***** Kaynak Dosyaları Oluştur _ seçeneği _*_Project_*_ ekleyebilirsiniz. Kaynak dosyalarının hedefi,*_Yapılandırma_* Project _**_ iletişim kutusunda belirtilir ve bu iletişim kutusuna _ Yapılandır * menü _*_öğesinde Project/Görüntüler_*_ seçeneği aracılığıyla erişilebilir.

Pixelmap ve Yazı tipi kaynakları için, ilişkili kaynak düzenleme iletişim kutularında her piksel haritası ve yazı tipi için özel bir çıkış dosya adı belirtebilirsiniz. Bu özellik, tüm kaynakları tek bir ortak çıkış dosyasına koymak yerine çok büyük kaynakları ayrı dosyalara koymaya olanak sağlar. Bir yazı tipi veya piksel haritası kaynağı için geçersiz kılınan bir dosya adı belirtmezseniz, bu kaynaklar ortak kaynak dosyasına yazılır.

İkili kaynakları kullanmayı tercih ederseniz, ham veya standart s-record çıkış biçimi belirtebilirsiniz. İkili kaynaklar derlanmaz veya uygulama koduyla bağlantılı değildir, ancak bunun yerine gx_binres_them_load() API'si kullanılarak çalışma zamanında yüklenir. Bu API hizmeti geçici olmayan bellekte depolanan kaynaklarınızı işaret alan kaynak tabloları oluşturur. Daha sonra bu kaynakları belirli bir görüntüyle yüklemek için gx_display_theme_install() kullanabilirsiniz;

## <a name="generating-specification-code"></a>Belirtim Kodu Oluşturma

GUIX Studio tarafından oluşturulan Belirtim dosyaları, GUIX Studio'da tasarlanmış kullanıcı arabirimini oluşturmak için gereken tüm C kodunu içerir. Bu kod ayrıca bu proje için oluşturulan Kaynak dosyalarına da başvurur. Kullanıcının uygulama kodu, projede tanımlanan UI nesnelerini gerçekten oluşturmak için bu koda çağrılar yapacaktır. Ayrıca, kullanıcının uygulama kodu projede belirtilen tüm özel pencere öğesi çizimi, olay işleme ve bellek ayırma işlevlerini içerir. Varsayılan olarak, oluşturulan iki dosya vardır; biri standart bir C kaynak kodu dosyası, diğeri ise uygulama kodunun GUIX Studio Belirtimlerine erişmesi için gereken dış başvuruları ve sabitleri sağlayan bir C üst bilgi dosyasıdır. Dosya adları şu şekildedir:

**{*proje-adı*}_specifications.h**

**{*proje-adı*}_specifications.c**

Örneğin, " basit " GUIX Studio projesi ***için*** oluşturulan Belirtim dosyaları:

**simple_specifications.h**

**simple_specifications.c**

Belirtim dosyalarını oluşturmak için, Project menü seçeneğinde ***** _*_Belirtim Dosyaları Oluştur_*_ _ seçeneği seçerek ekleyebilirsiniz. Belirtim dosyalarının hedefi,*_Project_* _**_ Yapılandır iletişim kutusunda belirtilir ve bu iletişim kutusuna _ Yapılandır * menü _*_öğesinde Project/Görüntüler_*_ seçeneği aracılığıyla erişilebilir.

## <a name="integrating-with-user-code"></a>Kullanıcı Kodu ile Tümleştirme

GUIX Studio tarafından oluşturulan Kaynak ve Belirtim dosyalarını tümleştirerek şu adımları takip etmek oldukça kolaydır:

1. Kaynak ve Belirtim dosyalarını kopyalayıp ekli derleme ortamına giden yol ayarları aracılığıyla erişilebilir hale
2. Ekli IDE projesine veya makefile'a tüm Kaynak ve Belirtim dosyalarını ekleme
3. Uygulama ekli kodunun Kaynak ve Belirtim dosyalarında bulunan kullanıcı arabirimini başlatmak ve oluşturmak için gerekli işlevleri çağırması
4. Uygulama ekli kodunun tüm gerekli özel pencere öğesi çizimini, olay işlemeyi ve bellek ayırma işlevlerini içerdiğini kontrol edin
5. Uygulamayı derleme (derleme ve bağlama)
6. Uygulamayı yürütün!