---
title: Bölüm 2 - NetX Duo Iperf Azure RTOS yükleme ve kullanma
description: Bu bölümde, Iperf örneğini yükleme ve kullanma yönergeleri ve sağlar.
author: v-condav
ms.author: v-condav
ms.date: 08/16/2021
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 7e80d89a334ceec3467b23574ab5c231a15f68a1
ms.sourcegitcommit: 4842f4cfe9e31b3ac59059f43e598eb70faebc8f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2021
ms.locfileid: "122610019"
---
# <a name="chapter-2-installation-and-use"></a>Bölüm 2 Yükleme ve Kullanma

Bu bölümde NetX Duo Iperf Gösterimi'nin yüklenmesi, kurulumu ve kullanımıyla ilgili çeşitli sorunların açıklaması yer almaktadır.

## <a name="installing-the-demonstration"></a>Tanıtım Yükleme

Dağıtımda sağlanan platforma özgü yükleme yönergelerini izleyin.

## <a name="installing-iperf"></a>Iperf yükleme

Kullanabileceğiniz çeşitli Iperf programları vardır. Ancak, bu belgeye örnek olarak, İnternet'te birden çok kaynak tarafından kullanılabilen Java tabanlı ***Jperf 2.0.2*** temel verilmiştir.

> [Not] *Jperf, konak makinede Java'nın yüklü olması gerekir.*

## <a name="setting-the-ip-address"></a>IP Adresini Ayarlama

Varsayılan olarak NetX Duo Iperf Gösterimi IP adresi **192.2.2.149 olarak ayarlanmıştır.** Bu, _nx_ip_create çağrısına parametre olarak **_demo_netx_duo_iperf.c_*_*_dosyasında nx_ip_create._**

## <a name="network-assumptions"></a>Ağ Varsayımları

Bu tanıtımda, Iperf konak makinesinin ve NetX Duo Iperf Gösterimi çalıştıran hedef panosunun 100 Mb/sn tam çift yönlü Ethernet anahtarına bağlı olduğu varsayıldı. En iyi performansı elde etmek için test ağına başka trafik ulaşmaz.

Iperf ana bilgisayar ve NetX Duo hedef panosuna çapraz Ethernet kablosuyla arkadan bağlanmak da mümkündür.

## <a name="running-the-demonstration"></a>Tanıtım Çalıştırma

Tanıtım kolayca çalıştırıldı; basit bir şekilde NetX Duo Iperf Tanıtım projesini (genellikle ***demo_netx_duo_iperf.***

## <a name="browse-to-the-demonstration"></a>Tanıtıma göz atma

Iperf konak platformunda bir tarayıcı aracılığıyla hedef panosuna göz atma. Hedef panosu IP **adresinin 192.2.2.149** olduğu varsaysak, aşağıdaki örnek netX Duo Iperf Gösterimi ilk web sayfasıdır.

![Iperf ilk web sayfası örneği](media/Picture1.jpg)

## <a name="running-jperf"></a>Jperf çalıştırma

Jperf'i çalıştırmak kolaydır, tek yapmanız gereken toplu iş Windows ***** jperf.bat_. Bu, aşağıda gösterildiği gibi Jperf IDE'yi başlatıyor. Jperf IDE görüntülendiğinde_ *Sunucu* Adresi * alanı NetX Duo Iperf Tanıtım hedef panosunun IP adresine ayarlandırın. Bu örnekte NetX Duo hedef panosu IP adresi **192.2.2.149'dır.** Ayrıca UDP Bant Genişliği ve **UDP Paket Boyutu** alanları da **vardır.** Bunların aşağıda gösterildiği gibi en iyi UDP alma performansı için kurulumu olması gerekir.

![UDP performansını iyileştirme.](media/Picture2.jpg)
