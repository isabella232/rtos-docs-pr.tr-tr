---
title: Ek D - Döküm ve izleme arabelleği
description: Azure RTOS ThreadX tarafından oluşturulan izleme arabelleğinin ana bilgisayar üzerinde bir dosyaya dökümü, kullanılan geliştirme aracı tarafından sağlanan komutlar ve/veya yardımcı programlar aracılığıyla yapılır.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: afbbabbd04ac4c33a747bb0cce4a9f36ca2d197a819cb48d834429e29fe5572c
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116802404"
---
# <a name="appendix-d---dumping-and-trace-buffer"></a>Ek D - Döküm ve izleme arabelleği

Azure RTOS ThreadX tarafından oluşturulan izleme arabelleğinin ana bilgisayar üzerinde bir dosyaya dökümü, kullanılan geliştirme aracı tarafından sağlanan komutlar ve/veya yardımcı programlar aracılığıyla yapılır. Bu ek, ThreadX ile kullanılan popüler geliştirme araçlarından bazılarında bir konak dosyasına izleme arabelleğinin döküm alma örneklerini içerir. 

## <a name="benchx-tools"></a>BenchX Araçları

İzleme arabelleği, aşağıda gösterildiği gibi __*_ Bellek Görünümü**'nin **içindeki*** Belleği Dosyaya Depola _ düğmesi seçerek BenchX araçlarıyla kolayca bir konak dosyasına ayrılabilir:

![BenchX araçlarında Bellek Görünümü'nin ekran görüntüsü.](./media/user-guide/image642.jpg)

Bu noktada izleme arabelleği adresini, boyutunu, hedef dosya adını (yol dahil) belirtin ve ***aşağıda gösterildiği gibi Kaydet*** düğmesini seçin. Bu, TraceX içinde görüntülemek için ikili izleme dosyasını oluşturacak.

![BenchX araçlarını kaydetme iletişim kutusunun ekran görüntüsü.](./media/user-guide/image643.jpg)

## <a name="realview-tools"></a>RealView Araçları

İzleme arabelleği, RealView'daki komut satırı istemine aşağıdaki komutu girerek ARM RealView araçlarıyla kolayca bir konak dosyasına ayrılabilir:

```c 
> WRITEFILE,raw trace_file.trx=0x6860..0xE560
```

Tamamlandıktan ***sonra, trace_file.trx*** dosyası, 0x6860 adresinden başlayarak bulunan izleme arabelleği içerir ve 0xE560. Bu dosya TraceX tarafından görüntülemeye hazırdır.

## <a name="iar-tools"></a>IAR Araçları

İzleme arabelleği, bellek görünümünde sağ tıklar ve Bellek Tasarrufu... öğesini seçerek IAR araçlarıyla kolayca bir konak dosyasına ***ayrılabilir.*** seçeneği aşağıda gösterildiği gibi.

![IAR araçlarında Bellek Kaydetme seçeneğinin ekran görüntüsü.](./media/user-guide/image0_311.jpg)

Bu, * Bellek Kaydetme _ **iletişim** kutusunun görüntülenebilir. Başlangıç ve bitiş adresini ve izleme dosyası adını girin, ardından Kaydet _*_düğmesini_*_ seçin. Aşağıda gösterilen örnekte IAR araçları belirtilen izleme arabelleğini _*_trace_file.hex_** dosyasındaki Intel HEX kayıtlarına kaydetmektedir.

![IAR araçları Bellek Kaydetme iletişim kutusunun ekran görüntüsü.](./media/user-guide/image648.jpg)

Bu noktada, konakta ***trace_file.hex*** dosyasına kaydedilen ve TraceX ile görüntülemeye hazır olan izleme arabelleğimiz vardır.

## <a name="codewarrior-tools"></a>CodeWarrior Araçları

İzleme arabelleği, Komut Penceresi'ne ***save** _ komutu girerek CodeWarrior araçlarıyla bir konak dosyasına kolayca ayrılabilir. Aşağıdaki örnek _ *_save_** komutu, izleme arabelleğinin en az 0x102200 anda 0x109F00:

```c
> save –b p:0x102200..0x109F00 trace_file.trx -a 32bit
```

Bu, izleme arabelleğinin konakta ***trace_file.trx dosyasına*** kaydedilir.

## <a name="mplab-tools"></a>MPLAB Araçları

MPLAB, Tabloyu Dışarı Aktar yardımcı programı aracılığıyla TraceX ile uyumlu bir izleme dosyası oluşturabilir ve bu sayede herhangi bir bellek aralığının bir konak dosyasına dışarı aktarın. TraceX için bir izleme dosyası oluşturmak üzere bu yardımcı programı kullanmak için aşağıdaki gibi devam edin:

**1. Adım** Belleği Görüntüle -> seçerek bir bellek penceresi açın.

![Görünüm menüsünde seçilen Belleğin ekran görüntüsü.](./media/user-guide/image0_316.jpg)

**2. Adım** Seçeneklerin listesini görüntülemek **için Bellek Görünümü'ne** sağ tıklayın. Bayt **görüntüsü seçmek için Görüntü Biçimi -1** Bayt'i belirtin.

![Biçimi Görüntüle seçeneğinin seçili olduğu Bellek Görünümü'nin ekran görüntüsü.](./media/user-guide/image650.png)

![Git iletişim kutusunun ekran görüntüsü.](./media/user-guide/image651.jpg)

**3. Adım** Bellek Görünümü Penceresi içinde yeniden **sağ** tıklayın ve Git'i seçin. Bu, olay arabelleğinin adresini belirtmenize olanak sağlayan bir iletişim kutusu açar.  Bu örnekte, **_event_buffer_** gösterilir.

![Git seçeneğinin seçili olduğu Bellek Görünümü'nin ekran görüntüsü.](./media/user-guide/image0_312.jpg)

![Görüntülenen örnekle ilgili event_buffer ekran görüntüsü.](./media/user-guide/image653.png)

**4. Adım** Bu, her zaman BTXT dizesi olan izleme arabelleğinin ilk konumunun içeriğini vurgular.

![İzleme arabelleğinin ilk konumunun ekran görüntüsü.](./media/user-guide/image0_313.jpg)

**5. Adım** Şimdi seçenekler menüsünü tekrar sağ tıklatın ve Tabloyu Dışarı **Aktar'ı seçin.**

![Tabloyu Dışarı Aktar seçeneğinin seçili olduğu Bellek Görünümü'nin ekran görüntüsü.](./media/user-guide/image0_314.jpg)

**6. Adım** Bu, gösterildiği gibi **Tabloyu Dışarı Aktar** iletişim kutusunu getirir. Dışarı aktarıla adres aralığını belirtin. Bu örnekte olduğu gibi 8K izleme arabelleği için 0xA00006AC 0xA00026AC aralığını belirtin ve oluşturulacak konak dosyası için bir ad girin (bu örnekte demo_threadx.trx).

! [[Olarak Dışarı Aktar iletişim kutusunun ekran görüntüsü.](./media/user-guide/image656.jpg)

**7. Adım** Konakta **demo_threadx.trx** adlı bir dosya oluşturulur ve bu dosya TraceX tarafından açılabilir.

## <a name="ghs-tools"></a>GHS Araçları

İzleme arabelleği, hata ayıklama komut penceresindeki komut satırı istemine aşağıdaki komutu girerek GHS araçlarıyla kolayca bir konak dosyasına ayrılabilir:

```c
memdump raw c:releasethreadxdemo_threadx.trx event_buffer 32768
```

Tamamlandıktan **sonra, demo_threadx.trx** dosyası, 32.768 bayt boyutuna sahip event_buffer'da bulunan ve TraceX tarafından görüntülemeye hazır olan izleme arabelleği içerir.

## <a name="renesas-hew"></a>Renesas HEW

İzleme arabelleği, aşağıdaki üç adım (ve alt adımlar) izlenmiştir ve Renasas HEW araçlarıyla bir konak dosyasına kolayca ayrılabilir:

**1. Adım** Bellek Penceresini açın.

! [[Bellek Penceresinin ekran görüntüsü.](./media/user-guide/image657.jpg)

**2. Adım** İmleci bellek penceresine yerleştirerek sağ tıklayın.

![Kaydet seçeneğinin seçili olduğu Bellek Penceresinin ekran görüntüsü.](./media/user-guide/image0_315.jpg)

**3. Adım** Kaydet'i seçin ve ardından Farklı Bellek Kaydet penceresinde şunları yapın:

- Dosya biçimi: İkili'yi seçin.
- Dosya Adı Belirtin: İstenen
- Başlangıç adresi belirtin: trace_buffer
- Bitiş adresini belirtin: (trace_buffer+boyut)
- Erişim boyutunu belirtin: 1
- Kaydet’e tıklayın.

![Farklı Bellek Kaydet iletişim kutusunun ekran görüntüsü.](./media/user-guide/image659.jpg)