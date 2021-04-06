---
title: Bölüm 1-yürütme profili kiti 'ne giriş
description: Bu bölümde, Azure RTOS ThreadX Execution profile Kit 'e (EPK) giriş yer almaktadır.
author: v-condav
ms.author: v-condav
ms.date: 01/22/2021
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 7d30676437535229ad5bdbca10dcc9ca009d6e74
ms.sourcegitcommit: d8edbb3207fe99f8afb431597dac063e73383e68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/05/2021
ms.locfileid: "106377652"
---
# <a name="chapter-1--introduction-to-the-execution-profile-kit"></a>Bölüm 1 yürütme profili setini giriş

ThreadX Execution profile Kit (EPK), uygulamaların iş parçacıkları, kesme hizmeti yordamları (ISRS) ve boşta sistem koşulları için yürütme zamanını dinamik olarak izlemelerine yönelik bir altyapı sağlar. Bu, özellikle iyileştirme ve en yüksek performans için uygulamayı ayarlama açısından kullanışlıdır. Ancak, aynı zamanda önemli bir hata ayıklama yardımıdır.

EPK, \" \" iş parçacığı girişi, iş parçacığı ÇıKıŞı, ISR GIRIŞI ve ISR çıkış üzerinde çağrılan derleme kodundaki threadx zamanlama mantığıyla yerleşik kancaları kullanır. EPK yordamları, bu tür olaylar arasındaki süreyi hesaplar ve değişim süresini genel değişkenlerde ve **TX_THREAD** denetim bloğunun üyelerini de depolar.

> [!NOTE]
> *Geliştirici, çalışan bir ThreadX uygulamasına donanım görünürlüğü sağlamak için g/ç PIN 'lerini değiştirmek için bu kanca işlevlerini kendi mantığıyla değiştirebilir ve hatta* değiştirebilir.

## 

## <a name="epk-requirements"></a>EPK gereksinimleri

EPK, çalışması için ThreadX 6,0 (veya üzeri) gerektirir. EPK Ayrıca \" \" , donanım saat kaynağını arttırmadan makul bir çözüm gerektirir. En makul çözüm, genellikle mikro ikinci ölçekte bir şey olur. Çözüm çok harika olursa EPK sayaçları çok hızlı bir şekilde en fazla olur. Buna karşılık, çözüm çok küçükse doğru zamanlama mümkün değildir. Uygulama zaman kaynağı, ***tx_execution_profile. h** _ ' de _ * TX_EXECUTION_TIME_SOURCE * * makrosu tarafından tanımlanır.

C derleyicisi, \" \" imzasız 64 bitlik toplam sayaç için imzasız uzun uzun bir tür içermelidir. Ayrıca, EPK genel değişkenlerin derleyicinin çalışma zamanı başlangıç kodu tarafından başlatıldığını varsayar. Böyle bir durum yoksa, ***tx_execution_profile. c*** ' de tanımlanan genel değişkenlerin uygulama tarafından 0 olarak başlatılması gerekir.

## <a name="epk-installation"></a>EPK yüklemesi

ThreadX EPK 'yi yüklemek için aşağıdaki adımları izleyin ve tüm ThreadX kitaplığını ve uygulamasını yeniden derleyin.

1. ThreadX kitaplığı derleme projenize EPK kaynak dosyalarını (***tx_execution_profile. h** _ ve _*_tx_execution_profile. c_*_) dahil edin. Bu dosyalar, _ *_yardımcı programı/Execution_Profile_** klasörü altındaki [Azure RTOS threadx deposu](<https://github.com/azure-rtos/threadx>) içinde bulunabilir.

1. ***Tx_port. h** _ ' de _ *TX_THREAD_EXTENSION_3** makrosunu aşağıdaki gibi tanımlayın.
```
    #define TX_THREAD_EXTENSION_3 unsigned long long tx_thread_execution_time_total; \
    unsigned long tx_thread_execution_time_last_start;
```

3. Donanım zaman kaynağınıza eşlemek için **_tx_execution_profile. h_** içinde **TX_EXECUTION_TIME_SOURCE** makrosunu tanımlayın.

1. Zamanlama kancalarının ThreadX derleme kodundan çağrılması için derleme ortamının **TX_ENABLE_EXECUTION_CHANGE_NOTIFY** tanımladığından emin olun.

1. 64 bit zaman kaynağını kullanmak istiyorsanız, bunun nasıl yapılacağını gösteren yönergeler için lütfen ***tx_execution_profile. h*** dosyasını gözden geçirin.

1. Tüm bu seçeneklerin düzgün derlenmesi için tüm kitaplık ve uygulamayı yeniden derleyin.

Artık, uygulamanızla EPK kullanmaya hazırsınız.

##  <a name="epk-example"></a>EPK örneği 

Aşağıda, mikro saniye başına 7,2 kez artan 32 bitlik bir Zamanlayıcı kaynağıyla yapılandırılmış standart bir ThreadX tanıtımı üzerinde kullanılan EPK örneği verilmiştir. 

**TX_EXECUTION_TIME_SOURCE** makro, 0xE0001004 ' te bellek eşlemeli Zamanlayıcı kaydını aşağıda gösterildiği gibi almak için tanımlanmıştır.
```
(EXECUTION_TIME_SOURCE_TYPE) \*((ULONG \*) 0xE0001004)
```

Tanıtım çalıştırmasının beş saniye boyunca çalışmasına izin vermek aşağıdaki sonuçları verir.

![Tanıtım çalışmasına izin veren sonuçlar.](media/demo_results.png)

Standart ThreadX tanıtımda boşta kalma süresi olmadığından (iş parçacıkları 1 ve 2 sürekli olarak çalıştırılır), EPK boşta kalma süresi için sıfır değerini doğru şekilde bildirir. Her yürütme kategorisinin mikrosaniye değerini türetmek için ıSR toplam süre ve iş parçacığı değerleri 7,2 ile ayrılabilir. EPK Ayrıca bu bilgilere erişmek için API 'Ler sağlar (lütfen bkz. [Bölüm 2](chapter2.md)).