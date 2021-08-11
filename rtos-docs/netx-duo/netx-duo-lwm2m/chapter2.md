---
title: Bölüm 2-RTOS NetX Duo LWM2M Istemcisini yükleme ve kullanma
description: Bu bölümde RTOS NetX Duo LWM2M Istemcisinin nasıl yükleneceği ve kullanılacağı açıklanmaktadır.
author: v-condav
ms.author: v-condav
ms.date: 01/22/2021
ms.topic: article
ms.service: rtos
ms.openlocfilehash: f804ae59dd639ca05d1b8f5251cf8b878e78bb9ad2575e08c21d43b14e727a19
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116796523"
---
# <a name="chapter-2--installation-and-use-of-lwm2m-client"></a>Bölüm 2 LWM2M Client yüklemesi ve kullanımı

Bu bölüm, LWM2M Istemci bileşeninin yüklenmesi, kurulumu ve kullanımı ile ilgili çeşitli sorunların açıklamasını içerir.

## <a name="product-distribution"></a>Ürün dağıtımı

Azure RTOS LWM2M Istemcisi, konumundaki ortak kaynak kodu deposundan elde edilebilir [https://github.com/azure-rtos/netxduo/tree/master/addons/lwm2m](https://github.com/azure-rtos/netxduo/tree/master/addons/lwm2m/) . Paket, bir adet ekleme dosyası olan üç kaynak dosyayı içerir.

* LWM2M Istemcisi için **NX \_ lwm2m \_ Client. h** üstbilgi dosyası

* LWM2M Client için **NX \_ lwm2m \_ Client. c** c kaynak dosyaları

* LWM2M Client demo için **demo \_ NETX \_ lwm2m \_ Client. c** c kaynak dosyası

## <a name="lwm2m-client-installation"></a>LWM2M Istemcisi yüklemesi

LWM2M Istemcisi NetX Duo 'in bir parçasıdır. bu nedenle, GitHub deposundan netx Duo klonladıktan sonra, LWM2M istemci kaynağı ***netxduo/addons/LWM2M*** konumunda bulunabilir.

## <a name="using-lwm2m_client"></a>LWM2M \_ istemcisi kullanma

LWM2M Istemcisi kullanımı basittir. Temel olarak, ***\_ \_ Threadx ve NETX kullanmak için uygulama kodu,*_*_TX \_ API. h_*_ ve _*_NX \_ API. h_*_ ' i içerir. _*_NX \_ lwm2m \_ Client. h_ _ eklendikten sonra *, uygulama kodu daha sonra bu kılavuzda belirtilen lwm2m istemci işlev çağrılarını yapabilir. Uygulamanın Ayrıca, _* _Nx \_ lwm2m \_ Client \_ . \**** dosyalarını NETX kitaplığına aktarması gerekir.

## <a name="configuration-options"></a>Yapılandırma seçenekleri

LWM2M Istemci kitaplığı ve uygulamayı LWM2M Istemcisini kullanarak oluştururken birkaç yapılandırma seçeneği vardır. Yapılandırma seçenekleri, aksi belirtilmediği takdirde, komut satırında, uygulama kaynağında tanımlanabilir.

| Yapılandırma &nbsp; seçeneği | Description |
| --- | --- |
| **NX \_ LWM2M \_ istemci \_ MTU 'su** | IP ve UDP üstbilgileri dahil olmak üzere bir CoAP iletisinin en büyük boyutunu belirtir. Varsayılan değer 1280 ' dir. |
| **NX \_ LWM2M \_ istemci \_ yuvası \_ TOS** | LwM2M UDP için gereken hizmet türü. Varsayılan olarak, bu değer \_ \_ normal IP paket hizmetini BELIRTMEK için NX IP normal olarak tanımlanır. |
| **NX \_ LWM2M \_ istemci \_ yuvası \_ TTL 'si** | Bu paketin, atılmadan önce geçebilmesi gereken yönlendirici sayısını belirtir. Varsayılan değer 0x80 olarak ayarlanır. |
| **NX \_ LWM2M \_ istemci \_ yuva \_ kuyruğu \_ en yüksek** | Alma sırasının maksimum derinliğinin sayısını belirtir. Varsayılan değer 4 ' e ayarlanır. |
| **NX \_ LWM2M \_ istemci \_ en fazla \_ coap \_ URI \_ yolu** | CoAP Uri-Path seçeneğinin en büyük uzunluklarının sayısını belirtir. Varsayılan değer 32 olarak ayarlanır. |
| **NX \_ LWM2M \_ istemci \_ en fazla \_ cihaz \_ hataları** | Cihaz nesnesi tarafından depolanan en fazla hata kodu sayısını belirtir. Varsayılan değer 8 ' dir. |
| **NX \_ LWM2M \_ istemci \_ en yüksek \_ Güvenlik \_ örnekleri** | En fazla güvenlik nesnesi örneği sayısını belirtir. Varsayılan değer, bir önyükleme sunucusunu ve standart sunucuyu desteklemek için 2 ' dir. |
| **NX \_ LWM2M \_ istemci \_ en yüksek \_ sunucu \_ örnekleri** | En fazla sunucu nesne örneği sayısını belirtir. Tek bir standart sunucuyu desteklemek için varsayılan değer 1 ' dir. |
| **NX \_ LWM2M \_ istemci \_ en fazla \_ erişim \_ denetimi \_ örnekleri** | En fazla Access Control örneği sayısını belirtir. Varsayılan değer 0 ' dır ve bu, erişim denetimini devre dışı bırakır. Uygulama birden fazla LWM2M sunucusunu destekliyorsa, her bir nesne örneği (güvenlik nesnesi örnekleri hariç) için bir Access Control örneği oluşturulması gerektiği için, en fazla Access Control örnek sayısı, LWM2M Istemcisinin destekleyeceği en fazla nesne örneği sayısına ayarlanmalıdır. |
| **NX \_ LWM2M \_ istemci \_ en fazla \_ erişim \_ denetimi \_ ACL 'leri** | Access Control örnek başına en fazla ACL kaynağı sayısını belirtir. Varsayılan değer 4'tür. |
| **NX \_ LWM2M \_ istemci \_ en fazla \_ bildirimleri** | LWM2M Istemcisinin destekleyeceği en fazla bildirim sayısını belirtir. Bir LWM2M sunucusu nesneler, nesne örnekleri ve kaynaklar üzerinde bildirimler ayarlayabilir. Varsayılan değer 8 ' dir. |
| **NX \_ LWM2M \_ istemci \_ Maks. \_ kaynaklar** | Nesne başına en fazla kaynak sayısını belirtir. Varsayılan değer 32 ' dir. |
| **NX \_ LWM2M \_ istemci \_ en \_ fazla \_ kaynak sayısı** | Birden çok kaynak için en fazla kaynak örneği sayısını belirtir. Varsayılan değer 8 ' dir. |
| **NX \_ LWM2M \_ istemci \_ önyükleme \_ Boşta \_ Zamanlayıcı** | Oturumu iptal etmeden önce önyükleme oturumu başlatıldığında önyükleme sunucusu istekleri için beklenecek en uzun süreyi belirtir. Varsayılan değer 60 saniyedir. |
| **NX \_ LWM2M \_ istemci \_ DTLS \_ Başlangıç \_ zaman aşımı** | DTLS el sıkışma tamamlanması için beklenecek en uzun süreyi belirtir. Varsayılan değer 30 saniyedir. |
| **NX \_ LWM2M \_ istemci \_ DTLS \_ bitiş \_ zaman aşımı** | DTLS kapatması işleminin tamamlanması için beklenecek en uzun süreyi belirtir. Varsayılan değer 5 saniyedir. |
| **NX \_ LWM2M \_ CLIENT \_ SECURITY \_ Max \_ Server \_ URI** | Null karakteri sonlandırma dahil olmak üzere, sunucu URI 'sinin uzunluk üst sınırını belirtir. Varsayılan değer 128 ' dir. |
| **NX \_ LWM2M \_ istemci \_ Güvenliği \_ en büyük \_ ortak \_ anahtar \_ veya \_ kimlik** | DTLS için ortak anahtar veya kimliğin uzunluk üst sınırını belirtir. Varsayılan değer 128 ' dir. |
| **NX \_ LWM2M \_ istemci \_ Güvenliği \_ en yüksek \_ sunucu \_ ortak \_ anahtarı** | DTLS için sunucu ortak anahtarının uzunluk üst sınırını belirtir. Varsayılan değer 128 ' dir. |
| **NX \_ LWM2M \_ istemci \_ Güvenliği \_ en fazla \_ Gizli \_ anahtarı** | DTLS için gizli anahtar uzunluğu üst sınırını belirtir. Varsayılan değer 128 ' dir. |
| **NX \_ LWM2M \_ istemcisi \_ bekletme \_** | Önyüklemeyi başlatmadan önce beklenecek saniye sayısını belirtir. Varsayılan değer 1 saniyedir. |
| **NX \_ LWM2M \_ istemci \_ yaşam \_ süresi** | Kayıt ömrü için saniye sayısını belirtir. Varsayılan değer 600 saniyedir. |
