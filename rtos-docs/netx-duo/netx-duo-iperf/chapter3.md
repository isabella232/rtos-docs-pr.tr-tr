---
title: Bölüm 3-UDP Iletim testini çalıştırma
description: Bu bölümde, Iperf örneğini çalıştırmaya yönelik yönergeler sağlanmaktadır.
author: v-condav
ms.author: v-condav
ms.date: 08/16/2021
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 2a68ba3ddb71adc424002c815fd023f50b552997
ms.sourcegitcommit: 4842f4cfe9e31b3ac59059f43e598eb70faebc8f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2021
ms.locfileid: "122610022"
---
# <a name="chapter-3-running-the-demonstration"></a>Bölüm 3 tanıtım çalıştırma

Konak tarayıcısının, daha önce gösterildiği gibi NetX Duo Iperf demo Web sayfasını görüntülediğine ve konakta daha önce ve Jperf 'nin çalıştığı varsayıldığında, bu bölümde her bir Iperf testinin nasıl yürütüleceği açıklanmaktadır.

## <a name="running-the-udp-transmit-test"></a>UDP Iletme testini çalıştırma

UDP Iletme testi, konağa NetX Duo UDP iletimi performansını belirler. Bu testte NetX Duo hedefi istemcsahiptir ve Jperf ana bilgisayarı sunucusudur. İlk olarak, Jperf IDE 'de **sunucu** ve **UDP** ' yi seçin. Sonra, **Iperf Çalıştır** ' ı seçin. Iperf sunucusunu aşağıda gösterildiği gibi başlatmak için.

![UDP iletim testini çalıştırma.](media/picture3.jpg)

Şimdi NetX Duo Iperf tanıtım Web sayfasından, testi başlatmak için **UDP Iletme testini Başlat** düğmesini seçin. Artık, aşağıda gösterildiği gibi, Jperf IDE ve NetX Duo Web sayfasındaki performans istatistiklerini gözlemleyebilirsiniz.

![UDP iletim test istatistikleri.](media/picture4.jpg)

Testi gerçekleştirmek için NetX Duo Iperf demo Web sayfasında **buraya** tıklayın bağlantısını seçin. Artık testin performans sonuçlarını gözlemleyebilirsiniz. Bu örnekte, NetX Duo hedefinde Iperf ana bilgisayarına yönelik UDP iletim performansı, aşağıda gösterildiği gibi NetX Duo hedefinde 94Mbps idi.

![UDP iletimi test sonuçları.](media/picture5.jpg)

## <a name="running-the-udp-receive-test"></a>UDP alma testini çalıştırma

UDP alma testi, NetX Duo hedefinde NetX Duo UDP alma performansını belirler. Bu testte NetX Duo hedefi sunucu ve Jperf ana bilgisayarı ise istemcdir. İlk olarak, Jperf IDE 'de **istemci** ve **UDP** ' yi seçin. Ardından, aşağıdaki çizimde gösterildiği gibi NetX Duo Iperf demo Web sayfasında **UDP alma testini Başlat** ' ı seçin.

![UDP alma testi çalıştırılıyor.](media/picture6.jpg)

Şimdi **Iperf Çalıştır** ' ı seçin. Jperf IDE 'den ve aşağıda gösterildiği gibi Jperf IDE 'deki istatistikleri gözlemleyin.

![UDP alma test istatistikleri.](media/picture7.jpg)

Testi gerçekleştirmek için NetX Duo Iperf demo Web sayfasında **buraya** bağlantıyı seçin. Artık testin performans sonuçlarını gözlemleyebilirsiniz. Bu örnekte, NetX Duo hedefinde UDP Alım performansı aşağıda gösterildiği gibi 95Mbps idi.

![UDP alma testi sonuçları](media/picture8.jpg)

## <a name="running-the-tcp-transmit-test"></a>TCP Iletme testini çalıştırma

TCP Iletme testi, konağa NetX Duo TCP iletimi performansını belirler. Bu testte NetX Duo hedefi istemcsahiptir ve Jperf ana bilgisayarı sunucusudur. İlk olarak, Jperf IDE 'de **sunucu** ve **TCP** ' yi seçin. Sonra, **Iperf Çalıştır** ' ı seçin. Iperf sunucusunu aşağıda gösterildiği gibi başlatmak için.

![TCP iletme testini çalıştırma.](media/picture9.jpg)

Şimdi NetX Duo Iperf tanıtım Web sayfasından testi başlatmak için **TCP Iletme testini Başlat** düğmesini seçin. Artık, aşağıda gösterildiği gibi, Jperf IDE ve NetX Duo Iperf demo Web sayfasındaki performans istatistiklerini gözlemleyebilirsiniz.

![TCP iletim test istatistikleri.](media/picture10.jpg)

Testi gerçekleştirmek için NetX Duo Iperf demo Web sayfasında ***buraya*** bağlantıyı seçin. Artık testin performans sonuçlarını gözlemleyebilirsiniz. Bu örnekte, NetX Duo hedefi üzerindeki TCP iletim performansı aşağıda gösterildiği gibi 91Mbps idi.

![TCP iletimi test sonuçları.](media/picture11.jpg)

## <a name="running-the-tcp-receive-test"></a>TCP alma testini çalıştırma

TCP alma testi, NETX Duo hedefinde NetX Duo TCP alma performansını belirler. Bu testte NetX Duo hedefi sunucu ve Jperf ana bilgisayarı ise istemcdir. İlk olarak, Jperf IDE 'de **istemci** ve **TCP** ' yi seçin. Ardından, NetX Duo Web sayfasında gösterildiği gibi **TCP alma testini Başlat** ' ı seçin.

![TCP alma testini çalıştırma](media/picture12.jpg)

Şimdi **Iperf Çalıştır** ' ı seçin. Jperf IDE 'den ve aşağıda gösterildiği gibi Jperf IDE 'deki istatistikleri gözlemleyin.

![TCP alma testi istatistikleri.](media/picture13.jpg)

Testi gerçekleştirmek için NetX Duo Iperf demo Web sayfasında ***buraya*** bağlantıyı seçin. Artık testin performans sonuçlarını gözlemleyebilirsiniz. Bu örnekte, NetX Duo hedefinde TCP Alım performansı aşağıda gösterildiği gibi 71Mbps idi.

![TCP alma testi sonuçları.](media/picture14.jpg)
