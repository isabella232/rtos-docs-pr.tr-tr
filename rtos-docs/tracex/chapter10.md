---
title: Bölüm 10 - Müşteri kullanıcı olayları
description: Bu bölümde, bu tür olaylar için kullanıcı tanımlı olayların ve özel simgelerin ve bilgi alanlarının nasıl oluşturulacakları hakkında bir açıklama yer almaktadır.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: b287436fb7f61df846bb0c84d910f5c095bc1f8f6635305e97c9e8b7aab64655
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116790430"
---
# <a name="chapter-10---customer-user-events"></a>Bölüm 10 - Müşteri kullanıcı olayları

Bu bölümde, bu tür olaylar için kullanıcı tanımlı olayların ve özel simgelerin ve bilgi alanlarının nasıl oluşturulacakları hakkında bir açıklama yer almaktadır. Bu bölümde aşağıdaki bölümler yer almaktadır: 

## <a name="inserting-user-defined-events"></a>User-Defined Ekleme

ThreadX, geliştiricilerin kendi kullanıcı tanımlı olaylarını günlük kaydı yapmalarına olanak sağlar ve TraceX tarafından grafiksel olarak görüntülenebilmeleri için daha da kullanışlı bilgiler sağlar. Kullanıcı tanımlı olay numaraları aralığı

**TX_TRACE_USER_EVENT_START** (4096) ile **TX_TRACE_USER_EVENT_END** (65535) arasında). olayların izleme arabelleğine yerleştirilmesi, Bölüm 5'te ***tx_trace_user_event_insert*** aracılığıyla yapılır. Aşağıdaki örnek çağrılar, hedefte geçerli izleme arabelleğine kullanıcı tanımlı iki olay ekler, yani kullanıcı tanımlı olay 4096 ve olay 4098:

```c
tx_trace_user_event_insert(4096, 1, 2, 3, 4);
tx_trace_user_event_insert(4098,0x100,0x200,0x300,0x400);
```

## <a name="default-display-of-user-defined-events"></a>User-Defined Olaylarının Varsayılan Görüntüsü

![Kullanıcı tanımlı olay simgesi](./media/user-guide/tx-events/image0.png)

TraceX varsayılan olarak, 6. Bölümde açıklandığı gibi varsayılan kullanıcı tanımlı Olay simgesine sahip tüm kullanıcı olaylarını görüntüler. Şekil 28'de, önceki örneklerde yer alan olay arabelleğine yerleştirilen 452 ve 453 olayları için varsayılan ***kullanıcı tanımlı olay tx_trace_user_event_insert*** gösterilir.

![Kullanıcı tanımlı olayların varsayılan görüntüsünün ekran görüntüsü. ](./media/user-guide/10.1.png)
 **ŞEKIL 28**

Kullanıcı tanımlı Olaylar için ayrıntılı bilgiler de mevcuttur. Şekil 28'de olay numarası 4096 olan ve belirtilen dört bilgi alanı gösteren olay 452 için ayrıntılı olay bilgileri yer amektedir.

![Kullanıcı tanımlı olayların ayrıntılı görüntüsünün ekran görüntüsü. ](./media/user-guide/10.2.png)
 **ŞEKIL 29**

## <a name="defining-custom-user-defined-event-icons"></a>Özel Olay User-Defined Tanımlama

TraceX ayrıca kullanıcıya özel kullanıcı tanımlı olay simgeleri ve özel bilgi alanı etiketleri oluşturma olanağı da sağlar. Bu özellik, ***tracex_custom.trxc _ yapılandırma dosyasına olay simgesi belirtimleri ekleyerek** elde edilir. Bu dosya, varsayılan olarak c:\Azure_RTOS\TraceX olan kullanıcı tanımlı TraceX yükleme dizininizin _ *_CustomEvents_** alt dizininde bulunur. Şekil 30'da örnek bir dizin yolu gösterilmektedir.

![Örnek bir dizin yolunun ekran görüntüsü. ](./media/user-guide/custom_events_folder.png)
 **ŞEKIL 30**

***tracex_custom.trxc*** özel olay yapılandırma dosyası, sıfır veya daha fazla özel olay tanımı içeren basit bir ASCII metin dosyasıdır. Dosyanın biçimi aşağıdaki gibidir:

```c
//Comments
**Start **
[custom event definition(s)] **End **
```

Başlangıç ve Bitiş arasındaki her satır tek bir özel olay tanımlamak için kullanılır. TraceX, özel olay tanımlanmamış ("Başlat" ve "Bitiş" etiketleri arasında hiçbir şey) bu dosyanın şablon sürümünü sağlar. Özel olay tanımının biçimi aşağıdaki gibidir:

**number, name, abbreviation, top_color, bottom_color, label1, label2, label2, label4**

burada:

- number: 4096 ile 65535 arasındaki kullanıcı tanımlı olay numarasını (dahil) tanımlar.</th>
- name: Kullanıcı tanımlı olayın mantıksal adını tanımlar.</td>
- abbreviation: İki harfli kullanıcı tanımlı olay kısaltmasını tanımlar.</td>
- top_color: Simgenin üst yarısı için RGB değerini tanımlar. Bu değer parantez içinde üç basamaklı bir sayıdır. Bazı tipik RGB tanımları:
  - BLACK = (0,0,0)       
  - WHITE = (255.255.255)
  - RED = (255,0,0)     
  - GREEN = (0,255,0)     
  - BLUE = (0,0,255)     
  - YELLOW = (255.255,0)   
  - CYAN = (0,255,255)   
  - MAGENTA = (255,0,255)   
  RBG belirtimlerinin kullanımı, kullanıcıya kullanıcı tanımlı her simge için geniş bir renk aralığı sağlar. RBG renk tanımı hakkında daha fazla bilgi için bkz: https://en.wikipedia.org/wiki/RGB#Digital_representations
- botton_color: Simgenin alt yarısı için RGB değerini tanımlar. Bu değer parantez içinde üç basamaklı bir sayıdır.
- label1: _ **info_field_1*** çağrısında belirtilen şekilde **_tx_trace_user_event_insert_* _.
- label2: _ **info_field_2*** çağrısında belirtilen şekilde **_tx_trace_user_event_insert_* _.
- label3: _ **info_field_3*** çağrısında belirtilen şekilde **_tx_trace_user_event_insert_* _.
- label4: _ **info_field_4*** çağrısında belirtilen şekilde **_tx_trace_user_event_insert_* _.

Bu bölümde kullanılan iki kullanıcı tanımlı olay için örnek tanımlar Şekil 10.4'te gösterilmiştir. İlk tanım, ***tracex_custom.trxc** _ dosyasının 5. satırda 4096 olayına aittir. Bu tanım kullanıcı tanımlı olay 4096'ya _*First_User_Event** adını verir, **FE'nin** iki harfli kısaltmasını belirtir, simgenin üst kısmını kırmızı yapar, simgenin alt kısmını yeşil yapar ve bilgi alanlarını **First_Info1**, **First_Info2**, First_Info3 ve **First_Info4** olarak tanımlar.  Kullanıcı tanımlı olay 4098, **_tracex_custom.trxc'nin 6. satırına benzer şekilde tanımlanır._**

![Kullanıcı tanımlı olaylar için örnek tanımların ekran görüntüsü. ](./media/user-guide/10.4.png)
 **ŞEKIL 31**

***tracex_custom.trxc** _ dosyası başlatma sırasında TraceX tarafından okunduktan sonra, özel simge tanımları etkili olmadan önce TraceX'ten çıkılıyor ve yeniden başlatılıyor. Şekil 32'de, _*_tracex_custom.trxc_** içinde tanımlanan özel olay simgeleriyle 452 ve 453 kullanıcı tanımlı olayların TraceX görüntüsü gösterilir.

![Özel olay simgeleriyle kullanıcı tanımlı olayların TraceX görüntüsünün ekran görüntüsü. ](./media/user-guide/10.5.png)
 **ŞEKIL 32**

Özel olay tanımındaki ek bilgiler, çift tıklama, fareyle üzerine tıklama veya geçerli olay düğmesine tıklayarak seçim olay olduğunda gösterilir. Şekil 33'te olay 452'de çift tıklama seçimi gösterir. Olay adı ve bilgi alanlarının hepsi ***tracex_custom.trxc'ye eklenen örnek tanımla eştir.***

![Bir olayda çift tıklama seçiminin ekran görüntüsü. ](./media/user-guide/10.6.png)
 **ŞEKIL 33**
