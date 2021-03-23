---
title: Ek D-döküm ve izleme arabelleği
description: Azure RTOS ThreadX tarafından oluşturulan izleme arabelleğinin ana bilgisayardaki bir dosyaya dökümünü almak, kullanılan özel geliştirme aracı tarafından belirtilen komutlar ve/veya yardımcı programlar aracılığıyla yapılır.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: 30f6b5e329feeb2dca37dda391fd738aba587c9a
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104827724"
---
# <a name="appendix-d---dumping-and-trace-buffer"></a>Ek D-döküm ve izleme arabelleği

Azure RTOS ThreadX tarafından oluşturulan izleme arabelleğinin ana bilgisayardaki bir dosyaya dökümünü almak, kullanılan özel geliştirme aracı tarafından belirtilen komutlar ve/veya yardımcı programlar aracılığıyla yapılır. Bu ek, ThreadX ile kullanılan daha popüler geliştirme araçlarından bazılarının bir izleme arabelleğinin bir konak dosyasına dökümünü alma örnekleri içerir. 

## <a name="benchx-tools"></a>BenchX araçları

İzleme arabelleği, aşağıda gösterildiği gibi _ *_bellek görünümü_* * Içindeki ***dosya depolama** _ düğmesine tıklayarak benchx araçlarıyla kolayca bir ana bilgisayar dosyasına dökülebilir:

![BenchX araçlarındaki bellek görünümünün ekran görüntüsü.](./media/user-guide/image642.jpg)

Bu noktada, izleme arabelleği adresini, boyutunu, hedef dosya adını (yol dahil) belirtin ve aşağıda gösterildiği gibi ***Kaydet*** düğmesini seçin. Bu işlem, TraceX içinde görüntülenmek üzere ikili izleme dosyası oluşturur.

![BenchX araçları Kaydet iletişim kutusunun ekran görüntüsü.](./media/user-guide/image643.jpg)

## <a name="realview-tools"></a>RealView araçları

Aşağıdaki komutu, RealView içinde komut satırı istemine girerek, izleme arabelleği ARM RealView araçlarıyla kolayca bir ana bilgisayar dosyasına dökülebilir:

```c 
> WRITEFILE,raw trace_file.trx=0x6860..0xE560
```

Tamamlandıktan sonra, ***trace_file. trx*** dosyası, 0x6860 adresinden başlayarak bulunan izleme arabelleğini Içerir ve 0xE560 adresine gider. Bu dosya TraceX tarafından görüntülenmek için hazırlanıyor.

## <a name="iar-tools"></a>IAR araçları

İzleme arabelleği ıAR araçlarıyla kolayca bir ana bilgisayar dosyasına dökülebilir, bu da bellek görünümüne sağ tıklayıp ***bellek kaydet*** ' i seçerek... seçeneğini aşağıda gösterildiği gibi yapın.

![IAR araçlarında bellek kaydetme seçeneğinin ekran görüntüsü.](./media/user-guide/image0_311.jpg)

Bu, ***bellek kaydetme** _ iletişim kutusunun görüntülenmesine neden olur. Başlangıç ve bitiş adresini ve izleme dosyası adını girin, sonra _*_Kaydet_*_ düğmesini seçin. Aşağıda gösterilen örnekte, ıAR araçları, belirtilen izleme arabelleğini _ *_trace_file. hex_* * DOSYASıNDAKI Intel onaltılı kayıtlarına kaydeder.

![IAR araçları bellek kaydetme iletişim kutusunun ekran görüntüsü.](./media/user-guide/image648.jpg)

Bu noktada, izleme arabelleği konaktaki ***trace_file. hex*** dosyasında kaydedilir ve tracex ile görüntülenmek üzere hazırlandık.

## <a name="codewarrior-tools"></a>CodeWarrior araçları

İzleme arabelleği, komut penceresine ***Save** _ komutunu girerek, CodeWarrior araçlarıyla kolayca bir ana bilgisayar dosyasına dökülebilir. Aşağıdaki örnek _ *_Save_** komutu, izleme arabelleğinin 0x102200 ' da başlayacağını ve 0x109f00 ' da bittiğini varsayar:

```c
> save –b p:0x102200..0x109F00 trace_file.trx -a 32bit
```

Bu, izleme arabelleğinin konaktaki ***trace_file. trx*** dosyasına kaydedilmesine neden olur.

## <a name="mplab-tools"></a>MPLAB araçları

MPLAB, dışa aktarma tablosu aracılığıyla, bir konak dosyasına herhangi bir bellek aralığının dışarı aktarılmasını sağlayan bir TraceX uyumlu izleme dosyası oluşturabilir. Bu yardımcı programı, TraceX için bir izleme dosyası oluşturmak üzere kullanmak için aşağıdaki gibi ilerleyin:

**1. adım** Görüntüle-> belleği ' nı seçerek bir bellek penceresi açın.

![Görünüm menüsünde seçilen belleğin ekran görüntüsü.](./media/user-guide/image0_316.jpg)

**2. adım** Seçeneklerin bir listesini görüntülemek için **bellek görünümü** ' ne sağ tıklayın. Bayt görüntüleme seçeneğini belirlemek için **görüntü biçimini belirtin-1 bayt** .

![Görüntüleme biçimi seçeneği belirlenmiş bellek görünümünün ekran görüntüsü.](./media/user-guide/image650.png)

![Git iletişim kutusunun ekran görüntüsü.](./media/user-guide/image651.jpg)

**3. adım** **Bellek görünümü** penceresinde tekrar sağ tıklayın ve olay arabelleğinin adresini belirtmenizi sağlayan bir iletişim kutusu açan **Git**' i seçin. Bu örnekte görüntülenmekte olan **_event_buffer_** gösterilmektedir.

![Bellek görünümünün git seçeneği seçili olan ekran görüntüsü.](./media/user-guide/image0_312.jpg)

![Görüntülenmekte olan event_buffer gösteren bir örnek ekran görüntüsü.](./media/user-guide/image653.png)

**4. adım** Bu, her zaman BTXT... dizesi olan izleme arabelleğinin ilk konumunun içeriğini vurgular.

![İzleme arabelleğinin ilk konumunun ekran görüntüsü.](./media/user-guide/image0_313.jpg)

**5. adım** Şimdi, Seçenekler menüsünü açmak için tekrar sağ tıklayın ve **tabloyu dışarı aktar**' ı seçin.

![Tablo ver seçeneğinin seçili olduğu bellek görünümünün ekran görüntüsü.](./media/user-guide/image0_314.jpg)

**6. adım** Bu, gösterilen şekilde **dışa aktarma tablosunu** getirir. Dışarı aktarılacak adres aralığını belirtin. 8K izleme arabelleği için, bu örnekte olduğu gibi, 0xA00006AC ' nin 0xA00026AC aralığını belirtin ve oluşturulacak ana bilgisayar dosyası için bir ad girin (Bu örnekte demo_threadx. trx).

! [[Farklı ver iletişim kutusunun ekran görüntüsü.](./media/user-guide/image656.jpg)

**Adım 7** Konakta **demo_threadx. trx** adlı bir dosya oluşturulacaktır ve bu dosya tracex tarafından açılabilir.

## <a name="ghs-tools"></a>GHS araçları

İzleme arabelleği, hata ayıklama komut penceresinde komut satırı isteminde aşağıdaki komutu girerek, GHS araçlarıyla kolayca bir ana bilgisayar dosyasına dökülebilir:

```c
memdump raw c:releasethreadxdemo_threadx.trx event_buffer 32768
```

Tamamlandıktan sonra, **demo_threadx. trx** dosyası, 32.768 bayt boyutunda event_buffer bulunan ve tracex tarafından görüntülenmek üzere hazırlanmakta olan izleme arabelleğini içerecektir.

## <a name="renesas-hew"></a>Renesas HEW

İzleme arabelleği, aşağıdaki üç adımı (ve alt adımları) izleyerek Renasas HEW araçlarıyla kolayca bir ana bilgisayar dosyasına dökülebilir:

**1. adım** Bellek penceresini açın.

! [[Bellek penceresinin ekran görüntüsü.](./media/user-guide/image657.jpg)

**2. adım** İmleci bellek penceresinde yerleştirin ve sağ tıklayın.

![Kaydet seçeneği belirlenmiş olan bellek penceresinin ekran görüntüsü.](./media/user-guide/image0_315.jpg)

**3. adım** Kaydet ' i seçin, ardından belleği farklı Kaydet penceresinde aşağıdakileri yapın:

- Dosya biçimi seçin: Ikili.
- Dosya adını belirtin: Istendiği gibi
- Başlangıç adresini belirtin: trace_buffer
- Bitiş adresini belirtin: (trace_buffer + boyut)
- Erişim boyutunu belirtin: 1
- Kaydet’e tıklayın.

![Belleği Kaydet iletişim kutusunun ekran görüntüsü.](./media/user-guide/image659.jpg)