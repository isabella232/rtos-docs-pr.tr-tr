---
title: Bölüm 1-Azure RTOS NetX Duo TFTP 'ye giriş
description: Önemsiz Dosya Aktarım Protokolü (TFTP), dosya aktarımları için tasarlanan hafif bir protokoldür.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 4431b23e143d05214090547e7f179a6f5def8217
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825709"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-tftp"></a>Bölüm 1-Azure RTOS NetX Duo TFTP 'ye giriş 

Önemsiz Dosya Aktarım Protokolü (TFTP), dosya aktarımları için tasarlanan hafif bir protokoldür. Daha sağlam protokollerin aksine, TFTP kapsamlı hata denetimi gerçekleştirmez ve ayrıca, bir durdurma ve bekleme Protokolü olduğundan sınırlı performansa sahip olabilir. Bir TFTP veri paketi gönderildikten sonra gönderen, alıcı tarafından bir ACK döndürülmesini bekler. Bu basit olsa da, genel TFTP verimini sınırlandırır. TFTP paketi, ana bilgisayarların IP ağları üzerinde TFTP protokolünü kullanmasını sağlar.

## <a name="tftp-requirements"></a>TFTP gereksinimleri

Düzgün çalışması için, NetX Duo TFTP paketinin TFTP Istemcileri bölümü bir IP örneğinin zaten oluşturulmuş olmasını gerektirir. Buna ek olarak, aynı IP örneğinde UDP 'nin etkinleştirilmesi gerekir. NetX Duo TFTP paketinin Istemci bölümünün başka gereksinimi yoktur.

NetX Duo TFTP paketinin TFTP sunucu bölümü bazı ek gereksinimlere sahiptir. İlk olarak, tüm istemci TFTP isteklerini işlemek için UDP 'nin *bilinen ve 69 numaralı bağlantı noktası* için tüm erişimi gerektirir. TFTP sunucusu Ayrıca, FileX Embedded dosya sistemiyle kullanılmak üzere tasarlanmıştır. FileX yoksa, Kullanıcı kendi ortamlarında kullanılan FileX bölümlerinin bağlantı noktasını alabilir. Bu, bu kılavuzun sonraki bölümlerinde ele alınmıştır.

## <a name="tftp-file-names"></a>TFTP dosya adları 

TFTP dosya adları, hedef dosya sisteminin biçiminde olmalıdır. Gerektiğinde tam yol bilgileriyle, NULL olarak sonlandırılmış ASCII dizeleri olmalıdır. NetX Duo TFTP uygulamasında TFTP dosya adlarının boyutunda belirtilen sınır yoktur.

## <a name="tftp-messages"></a>TFTP Iletileri

TFTP, dosyaları açmak, okumak, yazmak ve kapatmak için çok basit bir mekanizmaya sahiptir. UDP üstbilgisinin altında temel olarak 2-4 baytlık TFTP üstbilgisi vardır. TFTP dosyası açık iletilerinin tanımı aşağıdaki biçimdedir:

**oooof... f0OCTET0**

Konum:

- **oooo** 2 baytlık Opcode alanı  
0x0001-okuma için > açın  
0x0002-yazma için > açın

- **f... f** n-bayt dosya adı alanı

- 0 1-byte NULL sonlandırma karakteri

- **Sekizli** İkili aktarım belirtmek için ASCII "SEKIZLI"

- 0 1-byte NULL sonlandırma karakteri

TFTP yazma, ACK ve hata iletilerinin tanımı biraz farklıdır ve aşağıdaki gibi tanımlanır:

**oooobbbbd... TID**

Konum:

- **oooo** 2 baytlık Opcode alanı  
0x0003-> veri paketi  
0x0004-son okuma için > ACK  
0x0005-> hata koşulu  

- **bbbb** 2-Byte blok numarası alanı (1-n)

- **d... d** n-Byte veri alanı


- 0x0001 (okuma) dosya adı 0 SEKIZLI 0

- 0x0002 (yazma) dosya adı 0 SEKIZLI 0

## <a name="tftp-communication"></a>TFTP Iletişimi

TFTP sunucuları Istemci isteklerini dinlemek için iyi bilinen UDP bağlantı noktası 69 ' ü kullanır. TFTP Istemci yuvaları, kullanılabilir herhangi bir UDP bağlantı noktasına bağlanamaz. Karşıya yüklenecek veya İndirilecek dosyayı içeren veri paketi yükü, < 512 bayt içeren son pakete kadar 512 bayt öbeklerine gönderilir. Bu nedenle 512 bayttan az olan bir paket, dosyanın sonuna işaret eder. Genel olay sırası aşağıdaki gibidir:

TFTP okuma dosyası Istekleri:

1.  Istemci, dosya adıyla bir "okuma Için aç" isteği yayınlar ve sunucudan bir yanıt bekler.

2.  Sunucu, dosyanın ilk 512 baytını veya dosya boyutu 512 bayttan az olursa daha az bir değer gönderir.

3.  Istemci verileri alır, bir ACK gönderir ve 512 bayttan fazla dosya içeren dosyalar için sunucudan sonraki paketi bekler.

4.  Istemci 512 bayttan daha az bir paket aldığında sıra sona erer.

TFTP yazma Istekleri:

1.  Istemci, dosya adıyla bir "yazma için aç" isteği yayınlar ve sunucudan blok numarası 0 olan bir ACK 'e bekler.

2.  Sunucu, dosyayı yazmaya hazırsa, blok numarası sıfır olan bir ACK gönderir.

3.  Istemci, dosyanın ilk 512 baytını sunucuya (veya 512 bayttan daha az dosya için daha az) gönderir ve geri BILDIRIM bekler.

4.  Sunucu, baytlar yazıldıktan sonra bir ACK gönderir.

5.  Sıra, Istemci 512 bayttan daha az bir paket yazmayı tamamladığında sona erer.
 

## <a name="tftp-server-session-timer"></a>TFTP sunucusu oturum süreölçeri

TFTP sunucusunda sınırlı sayıda istemci istek yuvası vardır. Bir istemci oturumu bırakılmış görünüyorsa, bu yuva yeniden kullanım için kullanılamaz. Ancak NX_TFTP_SERVER_RETRANSMIT_ENABLE seçeneği etkinleştirilirse NetX Duo TFTP sunucusu, istemci oturumlarının her birinde zaman aşımını izleyen bir oturum süreölçeri oluşturur. Bir oturum zaman aşımı süresi dolduğunda sonlandırılır ve açık dosyalar kapanır. Bu nedenle, ' yuva ' başka bir TFTP Istemci isteği için kullanılabilir hale gelir.

Zaman aşımını ayarlamak için, varsayılan olarak 200 süreölçer işareti olan NX_TFTP_SERVER_RETRANSMIT_TIMEOUT yapılandırma seçeneğini ayarlayın. Oturum zaman aşımlarının denetlenme aralığı, varsayılan olarak 20 süreölçer onay işareti olan NX_TFTP_SERVER_TIMEOUT_PERIOD tarafından ayarlanır.

TFTP Istemcisi TFTP dosyası x medyasına karşıya yüklendiğinde, verilerin TFTP sunucusu RAM diskinden temeldeki medyaya (TFTP Istemci diski belleği) yazılabilmesi için medyanın temizlenmesi gerekir. Bu, uygulama TFTP sunucusunu kapatmak istemiyor fx_media_flush hizmeti kullanılarak yapılabilir.

Ancak, TFTP sunucusunu kapattıktan sonra uygulama, FileX medyası için başka bir kullanımı yoksa fx_media_close hizmetini kullanarak medyayı kapatır. Bu işlem, dosya verilerini TFTP Istemci diskine geri boşaltır, açık dosyaları kapatabilir ve dizin bilgilerini medyaya güncelleştirir.

Bu bölümdeki "küçük örnek" bölümünde bu gösterilmektedir.

FileX medyasını güncelleştirmeye yönelik üçüncü bir seçenek de FileX hizmetlerini açıkça kullanmak yerine FX_FAULT_TOLERANT veya FX_FAULT_TOLERANT_DATA seçenekleriyle derlemeye yöneliktir. Tanımlanmışsa, FileX otomatik olarak yazma isteklerini medya sürücüsüne geçirir. Bu seçenekler, performansı sınırlayabilir ancak kayıp dosya verilerinden veya kayıp kümelerinden daha büyük koruma sağlayabilir. Genel olarak bu ve FileX hakkında daha fazla bilgi için lütfen Express Logic FileX Kullanıcı Kılavuzu 'na bakın.

## <a name="tftp-multi-thread-support"></a>TFTP çoklu Iş parçacığı desteği

NetX Duo TFTP Istemci Hizmetleri birden çok iş parçacığından aynı anda çağrılabilir. Ancak, belirli bir TFTP Istemci örneğine yönelik okuma veya yazma istekleri aynı iş parçacığından sırayla yapılmalıdır.

## <a name="tftp-rfcs"></a>TFTP RFC 'Leri

NetX Duo TFTP, RFC1350 ve ilgili RFC 'lerle uyumludur.

