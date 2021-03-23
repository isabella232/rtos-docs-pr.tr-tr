---
title: Bölüm 1-Azure RTOS NetX FTP 'ye giriş
description: Dosya Aktarım Protokolü (FTP), dosya aktarımları için tasarlanmış bir protokoldür. FTP, dosya aktarım işlevini gerçekleştirmek için güvenilir Iletim Denetimi Protokolü (TCP) hizmetlerinden yararlanır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 86e132daf96f9039631234f10c8e239b61ad5126
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826734"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-ftp"></a>Bölüm 1-Azure RTOS NetX FTP 'ye giriş

Dosya Aktarım Protokolü (FTP), dosya aktarımları için tasarlanmış bir protokoldür. FTP, dosya aktarım işlevini gerçekleştirmek için güvenilir Iletim Denetimi Protokolü (TCP) hizmetlerinden yararlanır. Bu nedenle, FTP son derece güvenilir bir dosya aktarım protokolüdür. FTP de yüksek Performansdır. Gerçek FTP dosya aktarımı, adanmış bir FTP bağlantısında gerçekleştirilir.

## <a name="ftp-requirements"></a>FTP gereksinimleri

Azure RTOS NetX FTP paketi düzgün şekilde çalışması için bir NetX IP örneğinin zaten oluşturulmuş olmasını gerektirir. Ayrıca, aynı IP örneğinde TCP 'nin etkinleştirilmesi gerekir. NetX FTP paketinin FTP Istemci bölümünün başka gereksinimi yoktur.

NetX FTP paketinin FTP sunucusu bölümünde birkaç ek gereksinim vardır. İlk olarak, tüm istemci FTP komut isteklerini ve tüm Istemci FTP veri aktarımlarını işlemek için *iyi bilinen bağlantı noktası 20 ' sini* IŞLEMEK üzere TCP 'nin *iyi bilinen bağlantı noktası 21* ' e tam erişim gerektirir. FTP sunucusu Ayrıca, FileX Embedded dosya sistemiyle kullanılmak üzere tasarlanmıştır. FileX yoksa, Kullanıcı kendi ortamlarında kullanılan FileX bölümlerinin bağlantı noktasını alabilir. Bu, bu kılavuzun sonraki bölümlerinde ele alınmıştır.

## <a name="ftp-constraints"></a>FTP kısıtlamaları

FTP standardı, dosya verilerinin gösterimiyle ilgili birçok seçeneğe sahiptir. UNIX uygulamalarına benzer şekilde NetX FTP aşağıdaki dosya biçimi kısıtlamalarını varsayar:

- Dosya türü: **ikili**
- Dosya biçimi: **Yalnızca baskı dışı**
- Dosya yapısı: **yalnızca dosya yapısı**
- İletim modu: **yalnızca akış modu**

## <a name="ftp-file-names"></a>FTP dosya adları

FTP dosya adları, hedef dosya sisteminin (genellikle FileX) biçiminde olmalıdır. Gerektiğinde tam yol bilgileriyle, NULL olarak sonlandırılmış ASCII dizeleri olmalıdır. NetX FTP uygulamasındaki FTP dosya adlarının boyutu için belirtilen sınır yoktur. Ancak, paket havuzu yük boyutu, en büyük yolu ve/veya dosya adını barındırabilmelidir.

## <a name="ftp-client-commands"></a>FTP Istemci komutları

FTP 'nin bağlantıları açmak ve dosya ve dizin işlemlerini gerçekleştirmek için basit bir mekanizması vardır. Temel olarak *BILINEN TCP bağlantı noktası 21*' de bir bağlantı başarıyla kurulduktan sonra istemci tarafından VERILEN standart FTP komutları kümesi vardır. Aşağıdakiler, temel FTP komutlarının bazılarını göstermektedir:

### <a name="ftp-command-and-meaning"></a>FTP komutu ve anlamı

- **CWD yolu**: *çalışma dizinini değiştirme*
- **Sil filename**: *belirtilen dosya adını Sil*
- **Liste dizini**: *dizin listesini al*
- **MKD dizini**: *Yeni dizin oluştur*
- **NLST dizini**: *dizin listesini al*
- **Noop**: *işlem yok, başarı döndürüyor*
- **Parola**: *oturum açma için parola belirtin*
- **PASV**: *Pasif aktarım modunu iste*
- **PWD yolu**: *geçerli dizin yolunu toplama*
- **Çık**: *istemci bağlantısını Sonlandır*
- **RETR dosya adı**: *belirtilen dosyayı oku*
- **RMD dizini**: *belirtilen dizini Sil*
- **RNFR OldFileName**: *yeniden adlandırılacak dosyayı belirtin*
- **Rnnewfilename**: *dosyayı sağlanan dosya adına yeniden adlandır*
- **Stor dosya adı**: *belirtilen dosyayı yaz*
- **Tür ı**: *ikili dosya görüntüsünü seçin*
- **Kullanıcı Kullanıcı adı**: *oturum açma için Kullanıcı adı belirtin*
- **Bağlantı noktası ip_address, bağlantı noktası**: *IP adresi ve istemci veri bağlantı noktası sağlayın*

Bu ASCII komutları, FTP sunucusu ile FTP işlemleri gerçekleştirmek için NetX FTP Istemci yazılımı tarafından dahili olarak kullanılır.

## <a name="ftp-server-responses"></a>FTP sunucusu yanıtları

FTP sunucusu, Istemci komut isteklerini alan *iyi BILINEN TCP bağlantı noktası 21* ' i kullanır. FTP sunucusu Istemci komutunu işlediğinde, ASCII ve isteğe bağlı bir ASCII dizesi gelen 3 basamaklı bir sayısal yanıt döndürür. Sayısal yanıt, işlemin başarılı veya başarısız olup olmadığını anlamak için FTP Istemci yazılımı tarafından kullanılır. Aşağıda Istemci komutlarına çeşitli FTP sunucusu yanıtları listelenmektedir:

### <a name="first-numeric-field-and-meaning"></a>İlk sayısal alan ve anlamı

- **1xx**: *pozitif ön durum – başka bir yanıt geliyor*.
- **2xx**: *pozitif tamamlanma durumu*.
- **3xx**: *pozitif ön durum – başka bir komutun gönderilmesi gerekir*.
- **4xx**: *geçici hata koşulu*.
- **5xx**: *hata koşulu.*

### <a name="second-numeric-field-and-meaning"></a>İkinci sayısal alan ve anlam

- **x0x**: komutta sözdizimi hatası.
- **x1x**: bilgilendirici ileti.
- **X2X**: bağlantıyla ilişkili.
- **x3x**: kimlik doğrulama ile ilgili.
- **x4x**: belirtilmedi.
- **x5x**: dosya sistemiyle ilgili.

Örneğin, çıkış komutu ile FTP bağlantısının bağlantısını kesme isteği genellikle sunucudan bir "221" kodu ile yanıt vermeyecektir. bağlantı kesilmesi başarılı olursa.

## <a name="ftp-passive-transfer-mode"></a>FTP pasif aktarım modu

Varsayılan olarak, NetX FTP Istemcisi, veri yuvası üzerinde verileri FTP sunucusu ile değiş tokuş etmek için etkin taşıma modunu kullanır. Bu düzenleme ile ilgili sorun, FTP Istemcisinin bağlanmak için FTP sunucusunun bir TCP sunucu yuvasını açmasını gerektirmesidir. Bu, olası bir güvenlik riskini temsil eder ve Istemci güvenlik duvarı tarafından engelleniyor olabilir. Pasif aktarım modu, FTP sunucusunun veri bağlantısında TCP sunucusu yuvasını oluşturması için etkin aktarım modundan farklıdır. Bu, güvenlik riskini ortadan kaldırır (FTP Istemcisi için).

Pasif veri aktarımını etkinleştirmek için uygulama, ikinci bağımsız değişkeni NX_TRUE olarak ayarlanan daha önce oluşturulmuş bir FTP Istemcisinde *nx_ftp_client_passive_mode_set* çağırır. Bundan sonra, verileri aktarmaya yönelik tüm sonraki NetX FTP Istemci Hizmetleri (NLST, RETR, STOR) pasif Aktarım modunda denenir.

FTP Istemcisi önce PASV komutunu (bağımsız değişken yok) gönderir. FTP sunucusu bu isteği destekliyorsa, 227 "Tamam" yanıtını döndürür. Daha sonra Istemci isteği gönderir, örneğin. Sunucu Pasif aktarım modunu reddederse, NetX FTP Istemci hizmeti bir hata durumu döndürür.

Pasif aktarım modunu devre dışı bırakıp etkin aktarım moduna geri dönmek için, uygulama NX_FALSE olarak ayarlanan ikinci bağımsız değişkenle *nx_ftp_client_passive_mode_set* çağırır.

## <a name="ftp-communication"></a>FTP Iletişimi

FTP sunucusu, Istemci isteklerini alan *iyi BILINEN TCP bağlantı noktası 21* ' i kullanır. FTP Istemcileri, kullanılabilir herhangi bir TCP bağlantı noktasını kullanabilir. FTP olaylarının genel dizisi aşağıdaki gibidir:

### <a name="ftp-read-file-requests"></a>FTP okuma dosyası Istekleri

1. İstemci, sunucu bağlantı noktası 21 ' e TCP bağlantısı verir.
1. Sunucu, "220" yanıtını sinyal başarısına gönderir.
1. İstemci "username" ile "Kullanıcı" iletisi gönderir.
1. Sunucu, "331" yanıtını sinyal başarısına gönderir.
1. İstemci "parola" ile "PASS" iletisi gönderir.
1. Sunucu, "230" yanıtını sinyal başarısına gönderir.
1. İstemci ikili aktarım için "tür I" iletisi gönderir.
1. Sunucu, "200" yanıtını sinyal başarısına gönderir.
1. İstemci, IP adresi ve bağlantı noktası içeren "bağlantı noktası" iletisi gönderir.
1. Sunucu, "200" yanıtını sinyal başarısına gönderir.
1. İstemci, okunan dosya adına sahip "RETR" iletisi gönderir.
1. Sunucu, "PORT" komutunda belirtilen istemci veri bağlantı noktasıyla veri yuvası oluşturur ve bağlar.
1. Sunucu, okunan sinyal dosyası "125" yanıtını gönderiyor.
1. Sunucu, veri bağlantısı aracılığıyla dosyanın içeriğini gönderir. Bu işlem, dosya tamamen aktarılana kadar devam eder.
1. İşiniz bittiğinde, sunucu veri bağlantısını keser.
1. Sunucu "250" yanıtını "" olarak göndererek okunan sinyal dosyası başarılı olur.
1. İstemciler FTP bağlantısını sonlandırmak için "QUIT" gönderir.
1. Sunucu "221" sinyal bağlantısını kesme yanıtı başarılı oldu.
1. Sunucu FTP bağlantısının bağlantısını keser.

Daha önce belirtildiği gibi, IPv4 ve IPv6 üzerinden çalışan FTP arasındaki tek fark bağlantı noktası komutunun, IPv6 için EPRT komutuyla değiştirilmiştir

FTP Istemcisi pasif Aktarım modunda bir okuma isteği yapıyorsa, komut sırası aşağıdaki gibidir (**kalın** çizgiler, etkin aktarım modundan farklı bir adım gösterir):

1. İstemci, sunucu bağlantı noktası 21 ' e TCP bağlantısı verir.
1. Sunucu, "220" yanıtını sinyal başarısına gönderir.
1. İstemci "username" ile "Kullanıcı" iletisi gönderir.
1. Sunucu, "331" yanıtını sinyal başarısına gönderir.
1. İstemci "parola" ile "PASS" iletisi gönderir.
1. Sunucu, "230" yanıtını sinyal başarısına gönderir.
1. İstemci ikili aktarım için "tür I" iletisi gönderir.
1. Sunucu, "200" yanıtını sinyal başarısına gönderir.
1. **İstemci "PASV" iletisi gönderir.**
1. **Sunucu, Istemciye Bağlanılacak "227" yanıtını ve IP adresini ve bağlantı noktasını başarılı bir şekilde sinyaline gönderir.**
1. İstemci, okunan dosya adına sahip "RETR" iletisi gönderir.
1. **Sunucu, veri sunucusu yuvası oluşturur ve "227" yanıtında belirtilen bağlantı noktasını kullanarak bu yuvadaki Istemci bağlantı isteğini dinler.**
1. **Sunucu, okunan dosyayı işaret eden denetim soketine "150" yanıtı gönderir.**
1. Sunucu, veri bağlantısı aracılığıyla dosyanın içeriğini gönderir. Bu işlem, dosya tamamen aktarılana kadar devam eder.
1. İşiniz bittiğinde, sunucu veri bağlantısını keser.
1. **Sunucu, okuma sinyali almak için denetim yuvasında "226" yanıtı gönderir.**
1. İstemci, FTP bağlantısını sonlandırmak için "QUIT" iletisi gönderir.
1. Sunucu "221" sinyal bağlantısını kesme yanıtı başarılı oldu.
1. Sunucu FTP bağlantısının bağlantısını keser.

### <a name="ftp-write-requests"></a>FTP yazma Istekleri

1. İstemci, sunucu bağlantı noktası 21 ' e TCP bağlantısı verir.
1. Sunucu, "220" yanıtını sinyal başarısına gönderir.
1. İstemci "username" ile "Kullanıcı" iletisi gönderir.
1. Sunucu, "331" yanıtını sinyal başarısına gönderir.
1. İstemci "parola" ile "PASS" iletisi gönderir.
1. Sunucu, "230" yanıtını sinyal başarısına gönderir.
1. İstemci ikili aktarım için "tür I" iletisi gönderir.
1. Sunucu, "200" yanıtını sinyal başarısına gönderir.
1. İstemci, IP adresi ve bağlantı noktası içeren "bağlantı noktası" iletisi gönderir.
1. Sunucu, "200" yanıtını sinyal başarısına gönderir.
1. İstemci, yazılacak dosya adına sahip "STOR" iletisi gönderir.
1. Sunucu, "PORT" komutunda belirtilen istemci veri bağlantı noktasıyla veri yuvası oluşturur ve bağlar.
1. Sunucu, "125" yanıtını sinyal dosyası yazma işlemi için gönderir.
1. İstemci, veri bağlantısı aracılığıyla dosyanın içeriğini gönderir. Bu işlem, dosya tamamen aktarılana kadar devam eder.
1. İşiniz bittiğinde, Istemci veri bağlantısını keser.
1. Sunucu, "250" sinyal dosyası yazma yanıtı başarılı oldu.
1. İstemciler FTP bağlantısını sonlandırmak için "QUIT" gönderir.
1. Sunucu "221" sinyal bağlantısını kesme yanıtı başarılı oldu.
1. Sunucu FTP bağlantısının bağlantısını keser.

FTP Istemcisi pasif Aktarım modunda bir yazma isteği yapıyorsa, komut sırası aşağıdaki gibidir (**kalın** çizgiler, etkin aktarım modundan farklı bir adım gösterir):

1. İstemci, sunucu bağlantı noktası 21 ' e TCP bağlantısı verir.
1. Sunucu, "220" yanıtını sinyal başarısına gönderir.
1. İstemci "username" ile "Kullanıcı" iletisi gönderir.
1. Sunucu, "331" yanıtını sinyal başarısına gönderir.
1. İstemci "parola" ile "PASS" iletisi gönderir.
1. Sunucu, "230" yanıtını sinyal başarısına gönderir.
1. İstemci ikili aktarım için "tür I" iletisi gönderir.
1. Sunucu, "200" yanıtını sinyal başarısına gönderir.
1. **İstemci "PASV" iletisi gönderir.**
1. **Sunucu, Istemciye Bağlanılacak "227" yanıtını ve IP adresini ve bağlantı noktasını başarılı bir şekilde sinyaline gönderir.**
1. İstemci, yazılacak dosya adına sahip "STOR" iletisi gönderir.
1. **Sunucu, veri sunucusu yuvası oluşturur ve "227" yanıtında belirtilen bağlantı noktasını kullanarak bu yuvadaki Istemci bağlantı isteğini dinler.**
1. **Sunucu, denetim soketine dosya yazmayı işaret eden "150" yanıtı gönderir.**
1. İstemci, veri bağlantısı aracılığıyla dosyanın içeriğini gönderir. Bu işlem, dosya tamamen aktarılana kadar devam eder.
1. İşiniz bittiğinde, Istemci veri bağlantısını keser.
1. **Sunucu, "226" yanıtını denetim soketine dosya yazmayı işaret etmek için gönderir.**
1. İstemci, FTP bağlantısını sonlandırmak için "QUIT" iletisi gönderir.
1. Sunucu "221" sinyal bağlantısını kesme yanıtı başarılı oldu.
1. Sunucu FTP bağlantısının bağlantısını keser.

## <a name="ftp-authentication"></a>FTP Kimlik Doğrulaması

FTP bağlantısı gerçekleştiğinde, Istemcinin sunucuya bir *Kullanıcı adı* ve *parola* sağlaması gerekir. Bazı FTP siteleri, *anonım FTP* olarak adlandırılan, belirli bir Kullanıcı adı ve parola olmadan FTP erişimine izin verir. Bu bağlantı türü için, Kullanıcı adı için "anonim" belirtilmelidir ve parola, tüm e-posta adresi olmalıdır.

Kullanıcı, oturum açma ve oturum kapatma kimlik doğrulama yordamlarına sahip NetX FTP sağlamaktan sorumludur. Bunlar, ***nx_ftp_server_create** _ işlevi sırasında sağlanır ve parola işlemeden çağırılır. _Login * işlevi NX_SUCCESS döndürürse, bağlantı doğrulanır ve FTP işlemlerine izin verilir. Aksi takdirde, *oturum açma* işlevi NX_SUCCESS dışında bir şey döndürürse bağlantı girişimi reddedilir.

## <a name="ftp-multi-thread-support"></a>FTP çoklu Iş parçacığı desteği

NetX FTP Istemci Hizmetleri birden çok iş parçacığından aynı anda çağrılabilir. Ancak, belirli bir FTP Istemcisi örneği için okuma veya yazma istekleri aynı iş parçacığından sırayla yapılmalıdır.

## <a name="ftp-rfcs"></a>FTP RFC 'Leri

NetX FTP, RFC959 ve ilgili RFC 'lerle uyumludur.