---
title: Bölüm 4 - Azure RTOS TraceX performans analizi
description: Bu bölümde, TraceX Azure RTOS analiz aracının nasıl tanımları açık bir şekilde anlatılır.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: 719f27ef54091e2db9eefa982ce0c27561079b5b3a254d3fd09cc46d8f66f252
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116788730"
---
# <a name="chapter-4---azure-rtos-tracex-performance-analysis"></a>Bölüm 4 - Azure RTOS TraceX performans analizi

Bu bölümde, Azure RTOS TraceX performans analizi aracı açıkmektedir:

## <a name="performance-analysis"></a>Performans Analizi

TraceX, izleme dosyalarının yerleşik performans analizini sağlar. Yürütme profili, *popüler hizmetler,* *iş* *parçacığı yığını*  kullanımı ve FileX ve NetX istatistikleri gibi çeşitli performans istatistikleri gibi bilgiler hazır. Bu bilgilere Görünüm menü ***öğesi aracılığıyla*** ulaşabilirsiniz. 


## <a name="execution-profile"></a>Yürütme Profili

* Yürütme Profili Oluştur _ **düğmesini veya** _*_Görüntüle -Yürütme Profili'nin seçimi,_*_ o anda yüklü olan izleme dosyası için TraceX yürütme profilini sunar. Örnek ThreadX tanıtım izlemesi ile ilişkili yürütme profili _*Şekil 19** içinde gösterilir.

![Örnek ThreadX tanıtım izlemesi ile ilişkili yürütme profilinin ekran görüntüsü.](./media/user-guide/execution_profile.png)

**ŞEKIL 19**

Şekil **19'da** gösterilen örnek, işleme zamanlarının neredeyse %45'inin iş parçacığı 2 _ içinde ve işleme zamanlarının neredeyse ***%51'inin _* iş parçacığı _1_** içinde olduğunu gösterir. İzlemenin toplu iş parçacıkları ileti göndererek ve alan bu iş parçacıklarını gösterdiği için mantıksaldır. Bu örnekte kalan yürütme bağlamları yalnızca az miktarda yürütme süresine sahip olur.

## <a name="popular-services"></a>Popüler Hizmetler

* Görünüm **->Popüler Hizmetler** _ seçili durumdaki izleme dosyasında popüler hizmetleri sunar. Varsayılan olarak, bu bilgiler sistemin tamamı için görüntülenir. Ancak, belirli iş parçacıkları için popüler hizmetler de kullanılabilir. Örnek ThreadX tanıtım izlemesinde popüler hizmetler _*Şekil 20** içinde gösterilmiştir.

![Örnek ThreadX tanıtım izlemesinde popüler hizmetlerin ekran görüntüsü.](./media/user-guide/popular_services.png)

**ŞEKIL 20**

Şekil **20'de** gösterilen örnek, tx_queue_send _ ve ***_*_tx_queue_receive_** izlemesinde en popüler iki hizmet olduğunu gösterir. Bu, bu izlemenin yakalandır olduğu standart ThreadX gösteriminin davranışıyla tutarlıdır.

Bu analizin üst kısmında açılan seçim listesi kullanılarak bu analiz için belirli iş parçacıkları seçilebilir. **Şekil 21'de** **_3._** iş parçacığı için bu analizler yer aldı.

![TraceX popüler hizmetlerinin analizinin ekran görüntüsü.](./media/user-guide/popular_services_thread3.png)

**ŞEKIL 21**

## <a name="thread-stack-usage-analysis-for-thread-3"></a>İş Parçacığı Yığını Kullanımı ![İş parçacığı 3 için analiz.](./media/user-guide/screen_shot_17.png)

* İş Parçacığı Yığını **Kullanımı** Oluştur _ düğmesini veya _*_Görünüm -> İş_*_ Parçacığı Yığını Kullanımı'nın seçimi izleme dosyasındaki her iş parçacığı için yığın kullanımını gösterir. Bu, dosyada birçok izleme girdisine geçerli iş parçacığı yığın işaretçisi de dahil olmak üzere ThreadX tarafından lanır. %100 yığın kullanımı, yığının taşmış olduğunu ve uygulamada düzeltilmesi gerektiğini gösterir. Bu izleme dosyası içinde iş parçacığı yürütmesi yoksa, bu iş parçacığı için yığın kullanımı %0'da gösterilir. Örnek ThreadX gösterim izlemesinde iş parçacığı yığını kullanımı _*Şekil 22** içinde gösterilmiştir.

![TraceX İş Parçacığı Yığını Kullanımının Ekran Görüntüsü.](./media/user-guide/thread_stack_usage.png)

**ŞEKIL 22**

Şekil **22'de gösterilen örnek,** bu izlemede çoğu iş parçacığının %9 ile %12 arasında yığın kullanımına sahip olduğunu gösterir.

## <a name="performance-statistics"></a>Performans İstatistikleri

* Performans **İstatistikleri Oluştur** _ düğmesini veya _ *_Görünüm ->_* Performans İstatistikleri * seçeneğinin seçili durumdaki izleme dosyasının performans istatistiklerini sunar. Varsayılan olarak, bu bilgiler sistemin tamamı için görüntülenir. Ancak, performans istatistikleri her bir belirli iş parçacığı için de kullanılabilir.

Örnek ThreadX gösterim izlemesi performans istatistikleri Şekil **23'te gösterilmiştir.**

![TraceX performans istatistiklerinin ekran görüntüsü.](./media/user-guide/performance_statistics.png)

**ŞEKIL 23**

Şekil **23'te** gösterilen örnek, bu izleme dosyasında 18 bağlam anahtarının yanı sıra beş iş parçacığı önsempsi, 16 iş parçacığı askıya alma, 19 iş parçacığı yeniden izlemesi ve üç kesme olduğunu gösterir. Bu izleme dosyasında hiçbir öncelik ters çevirmesi bulunamadı. Belirlenmci ve belirleyici olmayan olmak için  iki öncelik ters çevirme kategorisi *olduğunu fark ettik.* Belirlenmsel öncelik ters çevirmeleri, bir iş parçacığının daha düşük öncelikli bir iş parçacığına ait bir mutex üzerinde engellenmiş olduğu öncelik ters çevirmeleridir. Belirleyici olmayan öncelik ters çevirmesi, belirlenici öncelik ters çevirmesi sırasında farklı bir düşük öncelikli iş parçacığının çalıştırı olduğu nondeteristic priority inversion'tur. Daha sonra, uygulamada öngörülemeyen zamanlama davranışına neden olabilir ve dikkatli bir şekilde araştırmalısınız.

## <a name="filex-statistics"></a>FileX İstatistikleri

* View **-> FileX Statistics** _ öğesini seçerek, o anda yüklenmiş olan izleme dosyasının FileX performans istatistiklerini sunar. Bu bilgiler tüm açık sistem için görüntülenir. /media nesneleri. Örnek FileX gösterim izlemesi performans istatistikleri _*Şekil 24** içinde gösterilmiştir.

![FileX İstatistiklerinin ekran görüntüsü.](./media/user-guide/filex_statistics.png)

**ŞEKIL 24**

Şekil **27'de gösterilen örnek,** 19 olduğunu gösterir. /media açılır, 19 .. /media kapanır, 19 .. /media boşaltıyor, 18 dizin okuması, 19 dizin yazması ve 18 dizin önbelleği isabet isabeti yok. İstatistikler penceresinde aşağı kaydırarak ek bilgiler ılabilir.

## <a name="netx-statistics"></a>NetX İstatistikleri

* Görünüm **-NetX İstatistikleri** _ seçeneği, o anda yüklü olan izleme dosyasının NetX performans istatistiklerini sunar. Bu bilgiler sistemin tamamı için görüntülenir. Örnek NetX gösterim izlemesi performans istatistikleri _*Şekil 25** içinde gösterilmiştir.

![NetX İstatistikleri'nin ekran görüntüsü.](./media/user-guide/netx_statistics.png)

**ŞEKIL 25**

Şekil **25'te** gösterilen örnek ARP, Ping veya UDP olayları olmadığını gösterir, ancak gönderilen 30 IP paketi, gönderilen 1.368 IP baytı, 30 IP paketi alındı ve 1.360 IP baytı alındı.

## <a name="trace-file-information"></a>dosya bilgilerini izleme

* İzleme Dosyası **Bilgilerini görüntüle > _,** açık izleme dosyası hakkında bazı temel bilgileri sunar. Bu bilgiler dosyanın bayt sırası, zaman kaynağının boyutu, her nesne adı için maksimum bayt sayısı ve tüm izleme dosyası işaretçilerinin temel adresini içerir. _ *Şekil 26** standart **_demo_threadx.trx_** izleme dosyasının izleme dosyası bilgilerini gösterir.

![TraceX Dosya Bilgileri'nin ekran görüntüsü.](./media/user-guide/trace_file_info.png)

**ŞEKIL 26**

## <a name="raw-trace-dump"></a>Ham İzleme Dökümü

* View **-> Raw Trace Dump** _ öğesinin seçerek ham izleme dökümlerini içeren dosyaya ad vere bir iletişim kutusu görüntülenir. Dosya adı ve yolu girdikten sonra TraceX, ham izleme dosyasını metin biçiminde derlemek için _*_notepad.exe_*_ dosyasını görüntüler. _ *Şekil 27** standart **_demo_threadx.trx_** izleme dosyasının ham izleme dosyası dökümlerini gösterir.

![Ham izleme dökümü ekran görüntüsü.](./media/user-guide/raw_trace_dump.png)

**ŞEKIL 27**
