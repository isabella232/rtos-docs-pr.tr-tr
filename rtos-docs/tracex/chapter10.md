---
title: Bölüm 10-müşteri Kullanıcı Etkinlikleri
description: Bu bölüm, bu tür olaylar için Kullanıcı tanımlı olayların ve özel simgelerin ve bilgi alanlarının nasıl oluşturulacağı hakkında bir açıklama içerir.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: 635c2d79922de9d5649bab841ae946cac862056c
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104827605"
---
# <a name="chapter-10---customer-user-events"></a>Bölüm 10-müşteri Kullanıcı Etkinlikleri

Bu bölüm, bu tür olaylar için Kullanıcı tanımlı olayların ve özel simgelerin ve bilgi alanlarının nasıl oluşturulacağı hakkında bir açıklama içerir. Bu bölüm aşağıdaki bölümleri içerir: 

## <a name="inserting-user-defined-events"></a>User-Defined olayları ekleme

ThreadX, geliştiricilerin kendi Kullanıcı tanımlı olaylarını günlüğe kaydetmelerine olanak sağlar. bu sayede, TraceX tarafından grafiksel olarak görüntülenebilen daha fazla yararlı bilgi sağlanır. Kullanıcı tanımlı olay numaraları aralığı

**TX_TRACE_USER_EVENT_START** (4096) ile **TX_TRACE_USER_EVENT_END** (65535) (dahil). İzleme arabelleğindeki olayların yerleştirilmesi, Bölüm 5 ' te tanımlanan ***tx_trace_user_event_insert*** aracılığıyla yapılır. Aşağıdaki örnek, Kullanıcı tanımlı olay 4096 ve olay 4098 gibi, hedefteki geçerli izleme arabelleğine iki Kullanıcı tanımlı olay eklemeyi çağırır:

```c
tx_trace_user_event_insert(4096, 1, 2, 3, 4);
tx_trace_user_event_insert(4098,0x100,0x200,0x300,0x400);
```

## <a name="default-display-of-user-defined-events"></a>User-Defined olaylarının varsayılan görüntüsü

![Kullanıcı tanımlı olay simgesi](./media/user-guide/tx-events/image0.png)

Varsayılan olarak, TraceX, Bölüm 6 ' da açıklandığı şekilde, varsayılan kullanıcı tanımlı bir olay simgesiyle tüm Kullanıcı olaylarını görüntüler. Şekil 28, önceki ***tx_trace_user_event_insert*** örnekleri aracılığıyla olay arabelleğine yerleştirilmiş olan 452 ve 453 olaylarına yönelik varsayılan kullanıcı tanımlı olay simgesini gösterir.

![Kullanıcı tanımlı olayların varsayılan görüntüsünün ekran görüntüsü. ](./media/user-guide/10.1.png)
 **Şekil 28**

Ayrıntılı bilgiler, Kullanıcı tanımlı olaylar için de kullanılabilir. Şekil 28, olay numarası 4096 olan olay 452 için ayrıntılı olay bilgilerini gösterir ve belirtilen dört bilgi alanını gösterir.

![Kullanıcı tanımlı olayların ayrıntılı görüntüsünün ekran görüntüsü. ](./media/user-guide/10.2.png)
 **Şekil 29**

## <a name="defining-custom-user-defined-event-icons"></a>Özel User-Defined olay simgeleri tanımlama

TraceX, kullanıcıya özel kullanıcı tanımlı olay simgeleri ve özel bilgi alanı etiketleri oluşturma yeteneği de sağlar. Bu yetenek, ***tracex_custom. trxc** _ yapılandırma dosyasına olay simgesi belirtimleri eklenerek elde edilir. Bu dosya, Kullanıcı tanımlı TraceX yükleme dizininizin _ *_CustomEvents_** alt dizininde bulunur ve varsayılan olarak c:\ Azure_RTOS \TraceX. Şekil 30 ' da örnek bir dizin yolu gösterilmektedir.

![Örnek dizin yolunun ekran görüntüsü. ](./media/user-guide/custom_events_folder.png)
 **Şekil 30**

***Tracex_custom. trxc*** özel olay yapılandırma dosyası, sıfır veya daha fazla özel olay tanımı içeren basıt bir ASCII metin dosyasıdır. Dosya biçimi aşağıdaki gibidir:

```c
//Comments
**Start **
[custom event definition(s)] **End **
```

Başlangıç ve bitiş arasındaki her satır, tek bir özel olay tanımlamak için kullanılır. TraceX, özel olay tanımlanmadığında bu dosyanın şablon sürümünü sağlar ("Başlat" ve "End" etiketleri arasında hiçbir şey). Özel bir olay tanımının biçimi aşağıdaki gibidir:

**sayı, ad, kısaltma, top_color, bottom_color, Label1, etiket 2, etiket 2, Label4**

burada:

- Sayı: Kullanıcı tanımlı olay numarasını tanımlar, bu arada 4096 ile 65535 arasında (dahil).</th>
- ad: Kullanıcı tanımlı etkinliğin mantıksal adını tanımlar.</td>
- kısaltma: iki harfli Kullanıcı tanımlı olay kısaltmasını tanımlar.</td>
- top_color: parantez içinde üç basamaklı bir sayı olan simgenin üst yarısı için RGB değerini tanımlar. Bazı tipik RGB tanımları şunlardır
  - SIYAH = (0, 0, 0)       
  - BEYAZ = (255.255.255)
  - KıRMıZı = (255, 0, 0)     
  - YEŞIL = (0255, 0)     
  - MAVI = (0, 0255)     
  - SARı = (255255, 0)   
  - CAMGÖBEĞI = (0255.255)   
  - MACENTA = (255, 0255)   
  RBG belirtiminin kullanılması kullanıcıya Kullanıcı tanımlı her simge için çok çeşitli renkler sağlar. RBG renk tanımı hakkında daha fazla bilgi için bkz.: https://en.wikipedia.org/wiki/RGB#Digital_representations
- botton_color: parantez içinde üç basamaklı bir sayı olan simgenin alt yarısı için RGB değerini tanımlar.
- Label1: _ *_tx_trace_user_event_insert_** çağrısında belirtildiği gibi, ***info_field_1** _ etiketi.
- Etiket 2: _ *_tx_trace_user_event_insert_** çağrısında belirtildiği gibi, ***info_field_2** _ etiketi.
- etiket 3: _ *_tx_trace_user_event_insert_** çağrısında belirtildiği gibi, ***info_field_3** _ etiketi.
- Label4: _ *_tx_trace_user_event_insert_** çağrısında belirtildiği gibi, ***info_field_4** _ etiketi.

Bu bölümde kullanılan iki Kullanıcı tanımlı olayın örnek tanımları Şekil 10,4 ' de gösterilmiştir. İlk tanım, ***tracex_custom. trxc** _ dosyasının 5. satırında olay 4096 ' dir. Bu tanım, _ * First_User_Event * * adlı Kullanıcı tanımlı olay 4096 ' i verir, **Fe**'nin iki harfli bir kısaltmasını belirtir, simgenin üst kısmını kırmızı, simgenin en alt kısmını yeşil hale getirir ve bilgi alanlarını **First_Info1**, **First_Info2**, **First_Info3** ve **First_Info4** olarak adlandırır. Kullanıcı tanımlı olay 4098, **_tracex_custom. trxc_**' nin 6. satırında benzer şekilde tanımlanır.

![Kullanıcı tanımlı olaylar için örnek tanımlarının ekran görüntüsü. ](./media/user-guide/10.4.png)
 **Şekil 31**

***Tracex_custom. trxc** _ dosyası başlatma sırasında tracex tarafından okunduğundan, özel simge tanımlarının etkili olabilmesi Için tracex 'in çıkış ve yeniden başlatılması gerekir. Şekil 32, _ *_tracex_custom. trxc_* * ' de tanımlanan özel olay simgeleri ile 452 ve 453 Kullanıcı tanımlı olayların tracex görüntüsünü gösterir.

![Özel olay simgeleriyle Kullanıcı tanımlı olayların ekran görüntüsü. ](./media/user-guide/10.5.png)
 **Şekil 32**

Özel olay tanımındaki ek bilgiler çift tıklama, fare üzerinden veya geçerli olay düğmesine tıklayarak seçtiğiniz olay olduğunda gösterilir. Şekil 33, olay 452 ' de çift tıklama seçimini gösterir. Olay adı ve bilgi alanları, ***tracex_custom. trxc*** öğesine eklenen örnek tanımıyla eşleşir.

![Bir olayda çift tıklama seçiminin ekran görüntüsü. ](./media/user-guide/10.6.png)
 **Şekil 33**
