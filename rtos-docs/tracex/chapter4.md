---
title: Bölüm 4-Azure RTOS TraceX performans analizi
description: Bu bölümde, Azure RTOS TraceX Performans Analizi Aracı açıklanmaktadır.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: 6cf1b5bd5349efd97c3afc8a9e7f57f477f06f8f
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104827538"
---
# <a name="chapter-4---azure-rtos-tracex-performance-analysis"></a>Bölüm 4-Azure RTOS TraceX performans analizi

Bu bölümde, Azure RTOS TraceX Performans Analizi Aracı açıklanmaktadır:

## <a name="performance-analysis"></a>Performans Analizi

Trackingex, izleme dosyalarının yerleşik performans analizini sağlar. *Yürütme profili*, *popüler hizmetler*, *Iş parçacığı yığını kullanımı* ve FileX ve NETX *İstatistikleri dahil* çeşitli *performans istatistikleri* gibi bilgiler kullanıma hazırdır. Bu bilgiler, ***Görünüm*** menüsü öğesi aracılığıyla kullanılabilir. 


## <a name="execution-profile"></a>Yürütme profili

***Yürütme profili oluştur** _ düğmesini veya _*_Görünüm-yürütme profilini_*_ seçtiğinizde, şu anda yüklü olan Izleme dosyası için trackingex yürütme profili sunulur. Örnek ThreadX tanıtım izlemesi ile ilişkili yürütme profili _ * Şekil 19 * * içinde gösterilmiştir.

![Örnek ThreadX tanıtım izlemesi ile ilişkili yürütme profilinin ekran görüntüsü.](./media/user-guide/execution_profile.png)

**ŞEKIL 19**

**Şekil 19** ' da gösterilen örnek, işlem zamanının yaklaşık %45 ' ının **_iş parçacığı 2_' nin içinde olduğunu *ve işlem zamanının yaklaşık %51 ' ının _*_iş parçacığı 1_ ' in içinde** olduğunu gösterir. Bu, izlemenin toplu iş parçacıklarının ileti gönderip almasını gösterdiği için bu mantıksal bir olaydır. Kalan yürütme bağlamlarının Bu örnekte yalnızca az miktarda yürütme süresi vardır.

## <a name="popular-services"></a>Popüler hizmetler

***View->popüler hizmetler** _ seçeneğinin belirlenmesi, şu anda yüklü olan izleme dosyasındaki popüler hizmetleri gösterir. Bu bilgiler varsayılan olarak tüm sistem için görüntülenir. Ancak, belirli iş parçacıkları için popüler hizmetler de kullanılabilir. Örnek ThreadX tanıtım izlemede popüler hizmetler _ * şekil 20 * * ' de gösterilir.

![Örnek ThreadX tanıtım izlemede popüler hizmetlerin ekran görüntüsü.](./media/user-guide/popular_services.png)

**ŞEKIL 20**

**Şekil 20** ' de gösterilen örnek, bu izlemede **_tx_queue_send_*_ ve _*_tx_queue_receive_** en popüler iki hizmet olduğunu gösterir. Bu, izlemenin yakalandığı standart ThreadX gösterimi davranışıyla tutarlıdır.

Bu pencerenin üst kısmındaki aşağı açılan seçim listesi kullanılarak bu analizler için belirli iş parçacıkları seçilebilir. **Şekil 21** **_iş parçacığı 3_** için bu analizi gösterir.

![Bir TraceX popüler hizmetler için çözümlemenin ekran görüntüsü.](./media/user-guide/popular_services_thread3.png)

**ŞEKIL 21**

## <a name="thread-stack-usage-analysis-for-thread-3"></a>İş parçacığı yığını kullanımı ![3. iş parçacığı için analiz.](./media/user-guide/screen_shot_17.png)

* Iş parçacığı **yığını kullanımını oluştur** _ düğmesini veya _*_Görünüm-> Iş parçacığı yığını kullanımı_*_ , izleme dosyasındaki her iş parçacığının yığın kullanımını gösterir. Bu, geçerli iş parçacığı yığın işaretçisi de dahil olmak üzere, dosyadaki izleme girdilerinin çoğunda bulunan ThreadX tarafından gerçekleştirilir. Yığın kullanımı %100, yığının taşdığını ve uygulamada düzeltilmesi gerektiğini gösterir. Bu izleme dosyasında iş parçacığı yürütmesi yoksa, bu iş parçacığı için yığın kullanımı %0 olarak gösterilir. Örnek ThreadX tanıtım izlemede iş parçacığı yığını kullanımı _ * şekil 22 * * içinde gösteriliyor.

![TraceX Iş parçacığı yığını kullanımının ekran görüntüsü.](./media/user-guide/thread_stack_usage.png)

**ŞEKIL 22**

**Şekil 22** ' de gösterilen örnek, bu izlemede en çok iş parçacığının %9 ve %12 yığın kullanımı arasında olduğunu gösterir.

## <a name="performance-statistics"></a>Performans Istatistikleri

***Performans Istatistikleri oluştur** _ düğmesi veya _ *_View-> performans istatistikleri_** seçeneğinin belirlenmesi, şu anda yüklü olan izleme dosyasının performans istatistiklerini gösterir. Bu bilgiler varsayılan olarak tüm sistem için görüntülenir. Ancak, performans istatistikleri her belirli iş parçacığı için de kullanılabilir.

Örnek ThreadX tanıtım izlemenin performans istatistikleri **Şekil 23**' te gösterilmiştir.

![TraceX performans istatistiklerinin ekran görüntüsü.](./media/user-guide/performance_statistics.png)

**ŞEKIL 23**

**Şekil 23** ' te gösterilen örnek, bu izleme dosyasında 18 bağlam anahtarı olduğunu ve beş iş parçacığı preemptions, 16 iş parçacığı getirilmesi, 19 iş parçacığı bağlantının sürdürülmesi ve üç kesme olduğunu gösterir. Bu izleme dosyasında herhangi bir öncelik sürümü bulunamadı. İki tür öncelik de vardır; Yani, *belirleyici* ve *belirleyici olmayan* iki kategori. Belirleyici öncelik Inversions, daha düşük öncelikli bir iş parçacığına ait olan bir mutex üzerinde bir iş parçacığının engellendiği öncelikli bir sürümdür. Belirleyici olmayan bir öncelik, farklı bir öncelik iş parçacığının belirleyici bir öncelik veya sürüm sırasında çalıştığı yerdir. Daha sonra uygulamada öngörülemeyen zamanlama davranışına neden olabilir ve dikkatli araştırdık olmalıdır.

## <a name="filex-statistics"></a>FileX Istatistikleri

***View-> FileX STATISTICS** _ ' i seçmek, şu anda yüklü olan Izleme dosyasının FileX performans istatistiklerini gösterir. Bu bilgiler tüm sistemde, tüm açıldıklarında görüntülenir. /Media nesneleri. Örnek FileX tanıtım izlemesinin performans istatistikleri _ * Şekil 24 * * içinde gösterilir.

![FileX Istatistiklerinin ekran görüntüsü.](./media/user-guide/filex_statistics.png)

**ŞEKIL 24**

**Şekil 27** ' de gösterilen örnek 19 olduğunu gösterir. /Medya açılır, 19.. /Media kapanıyor, 19.. /Medya Temizleme, 18 dizin okuma, 19 Dizin yazma ve 18 Dizin önbellek isabetsizliği. Ek ton bilgileri, İstatistik penceresinde aşağı kaydırarak görüntülenebilir.

## <a name="netx-statistics"></a>NetX Istatistikleri

***View-NetX STATISTICS** _ öğesinin seçilmesi, yüklü olan Izleme dosyasının NETX performans istatistiklerini gösterir. Bu bilgiler tüm sistem için görüntülenir. Örnek NetX tanıtım izlemesinin performans istatistikleri _ * Şekil 25 * * içinde gösterilir.

![NetX Istatistiklerinin ekran görüntüsü.](./media/user-guide/netx_statistics.png)

**ŞEKIL 25**

**Şekil 25** ' te gösterilen örnek, ARP, PıNG veya UDP olayları olmadığını, ancak gönderilen 30 IP paketi olduğunu, 1.368 IP baytı gönderildiğini, 30 IP paketi alındığını ve 1.360 IP bayt alındığını gösterir.

## <a name="trace-file-information"></a>İzleme dosyası bilgileri

***View-> Izleme dosyası bilgilerini** seçin _, açılan izleme dosyası hakkında bazı temel bilgileri gösterir. Bu bilgiler, dosyanın bayt sırasını, zaman kaynağının boyutunu, her bir nesne adı için en fazla bayt sayısını ve tüm izleme dosyası işaretçilerinin temel adresini içerir. _ *Şekil 26** standart **_demo_threadx. trx_** izleme dosyası için izleme dosyası bilgilerini gösterir.

![TraceX dosya bilgilerinin ekran görüntüsü.](./media/user-guide/trace_file_info.png)

**ŞEKIL 26**

## <a name="raw-trace-dump"></a>Ham Izleme dökümü

***View-> ham Izleme dökümünü al**' ı seçtiğinizde, ham izleme dökümünü içeren dosyayı adlandırmak için bir iletişim kutusu görüntülenir. Dosya adı ve yolu girildikten sonra, TraceX ham izleme dosyasını metin biçiminde oluşturur ve bunu göstermek için _*_notepad.exe_*_ başlatır. _ *Şekil 27** standart **_demo_threadx. trx_** izleme dosyası için ham izleme dosyası dökümünü gösterir.

![Ham izleme dökümünden oluşan ekran görüntüsü.](./media/user-guide/raw_trace_dump.png)

**ŞEKIL 27**
