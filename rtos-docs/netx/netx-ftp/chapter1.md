---
title: Bölüm 1-Azure RTOS NetX FTP 'ye giriş
description: Dosya Aktarım Protokolü (FTP), dosya aktarımları için tasarlanmış bir protokoldür. FTP, dosya aktarım işlevini gerçekleştirmek için güvenilir Iletim Denetimi Protokolü (TCP) hizmetlerinden yararlanır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 35a7487720578ce8da578c490d96aa3c444ee818167b1bbd10833556e34b3dce
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116799481"
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
1. Sunucu başarı sinyaline "200" yanıtı gönderir.
1. İstemci, okumak için dosya adıyla "RETR" iletisi gönderir.
1. Sunucu veri yuvası oluşturur ve "PORT" komutunda belirtilen istemci veri bağlantı noktasına bağlanır.
1. Sunucu, dosya okumanın başlat olduğunu sinyale "125" yanıtını gönderir.
1. Sunucu, dosyanın içeriğini veri bağlantısı üzerinden gönderir. Bu işlem, dosya tamamen aktarılana kadar devam eder.
1. Tamamlandığında, Sunucu veri bağlantısını keser.
1. Sunucu, dosya okumanın başarılı olduğunu sinyale "250" yanıtını gönderir.
1. İstemciler FTP bağlantısını sonlandırmak için "QUIT" gönderir.
1. Sunucu bağlantıyı kesmenin başarılı olduğunu sinyale "221" yanıtını gönderir.
1. Sunucu FTP bağlantısını keser.

Daha önce belirtildiği gibi, IPv4 ve IPv6 üzerinde çalışan FTP arasındaki tek fark PORT komutunun IPv6 için EPRT komutuyla değiştirilmesidir

FTP İstemcisi pasif aktarım modunda okuma isteğinde bulunuyorsa, komut sırası aşağıdaki gibidir **(kalın** çizgiler etkin aktarım modundan farklı bir adım olduğunu gösterir):

1. İstemci, SUNUCU bağlantı noktası 21'e TCP bağlantısı verir.
1. Sunucu başarı sinyaline "220" yanıtı gönderir.
1. İstemci , "username" ile "USER" iletisi gönderir.
1. Sunucu başarı sinyaline "331" yanıtı gönderir.
1. İstemci , "parola" ile "PASS" iletisi gönderir.
1. Sunucu başarı sinyaline "230" yanıtı gönderir.
1. İstemci, ikili aktarım için "TYPE I" iletisi gönderir.
1. Sunucu başarı sinyaline "200" yanıtı gönderir.
1. **İstemci "PASV" iletisi gönderir.**
1. **Sunucu, başarılı olduğunu işaret etmek için İstemcinin bağlanması için "227" yanıtını ve IP adresini ve bağlantı noktasını gönderir.**
1. İstemci, okumak için dosya adıyla "RETR" iletisi gönderir.
1. **Sunucu veri sunucusu yuvası oluşturur ve "227" yanıtta belirtilen bağlantı noktasını kullanarak bu yuvada İstemci bağlantı isteğini dinler.**
1. **Sunucu, dosyanın okundu olarak işaret etmek için denetim yuvasında "150" yanıtı gönderir.**
1. Sunucu, dosyanın içeriğini veri bağlantısı üzerinden gönderir. Bu işlem, dosya tamamen aktarılana kadar devam eder.
1. Tamamlandığında, Sunucu veri bağlantısını keser.
1. **Sunucu, dosya okumanın başarılı olduğunu işaret etmek için denetim yuvasında "226" yanıtı gönderir.**
1. İstemci, FTP bağlantısını sonlandırmak için "QUIT" gönderir.
1. Sunucu bağlantıyı kesmenin başarılı olduğunu sinyale "221" yanıtını gönderir.
1. Sunucu FTP bağlantısını keser.

### <a name="ftp-write-requests"></a>FTP Yazma İstekleri

1. İstemci, SUNUCU bağlantı noktası 21'e TCP bağlantısı verir.
1. Sunucu başarı sinyaline "220" yanıtı gönderir.
1. İstemci , "username" ile "USER" iletisi gönderir.
1. Sunucu başarı sinyaline "331" yanıtı gönderir.
1. İstemci , "parola" ile "PASS" iletisi gönderir.
1. Sunucu başarı sinyaline "230" yanıtı gönderir.
1. İstemci, ikili aktarım için "TYPE I" iletisi gönderir.
1. Sunucu başarı sinyaline "200" yanıtı gönderir.
1. İstemci, IP adresi ve bağlantı noktası ile "PORT" iletisi gönderir.
1. Sunucu başarı sinyaline "200" yanıtı gönderir.
1. İstemci, yazacak dosya adıyla "STOR" iletisi gönderir.
1. Sunucu veri yuvası oluşturur ve "PORT" komutunda belirtilen istemci veri bağlantı noktasına bağlanır.
1. Sunucu, dosya yazmanın başlat sinyaline "125" yanıtını gönderir.
1. İstemci, dosyanın içeriğini veri bağlantısı üzerinden gönderir. Bu işlem, dosya tamamen aktarılana kadar devam eder.
1. Tamamlandığında İstemci, veri bağlantısını keser.
1. Sunucu, dosya yazmanın başarılı olduğunu sinyale "250" yanıtını gönderir.
1. İstemciler FTP bağlantısını sonlandırmak için "QUIT" gönderir.
1. Sunucu bağlantıyı kesmenin başarılı olduğunu sinyale "221" yanıtını gönderir.
1. Sunucu FTP bağlantısını keser.

FTP İstemcisi pasif aktarım modunda bir yazma isteğinde bulunuyorsa, komut sırası aşağıdaki gibidir **(kalın** çizgiler etkin aktarım modundan farklı bir adım olduğunu gösterir):

1. İstemci, SUNUCU bağlantı noktası 21'e TCP bağlantısı verir.
1. Sunucu başarı sinyaline "220" yanıtı gönderir.
1. İstemci , "username" ile "USER" iletisi gönderir.
1. Sunucu başarı sinyaline "331" yanıtı gönderir.
1. İstemci , "parola" ile "PASS" iletisi gönderir.
1. Sunucu başarı sinyaline "230" yanıtı gönderir.
1. İstemci, ikili aktarım için "TYPE I" iletisi gönderir.
1. Sunucu başarı sinyaline "200" yanıtı gönderir.
1. **İstemci "PASV" iletisi gönderir.**
1. **Sunucu, başarılı olduğunu işaret etmek için İstemcinin bağlanması için "227" yanıtını ve IP adresini ve bağlantı noktasını gönderir.**
1. İstemci, yazacak dosya adıyla "STOR" iletisi gönderir.
1. **Sunucu veri sunucusu yuvası oluşturur ve "227" yanıtta belirtilen bağlantı noktasını kullanarak bu yuvada İstemci bağlantı isteğini dinler.**
1. **Sunucu, dosya yazmanın başlat olduğunu işaret etmek için denetim yuvasında "150" yanıtı gönderir.**
1. İstemci, dosyanın içeriğini veri bağlantısı üzerinden gönderir. Bu işlem, dosya tamamen aktarılana kadar devam eder.
1. Tamamlandığında İstemci, veri bağlantısını keser.
1. **Sunucu, dosya yazmanın başarılı olduğunu işaret etmek için denetim yuvasında "226" yanıtı gönderir.**
1. İstemci, FTP bağlantısını sonlandırmak için "QUIT" gönderir.
1. Sunucu bağlantıyı kesmenin başarılı olduğunu sinyale "221" yanıtını gönderir.
1. Sunucu FTP bağlantısını keser.

## <a name="ftp-authentication"></a>FTP Kimlik Doğrulaması

Bir FTP bağlantısı her gerçekleşti mi, İstemci Sunucuya kullanıcı adı ve *parola* *sağlasa gerekir.* Bazı FTP siteleri, belirli bir kullanıcı adı *ve parola olmadan FTP* erişimine izin veren Anonim FTP olarak adlandırılanlara izin verir. Bu tür bir bağlantı için kullanıcı adı için "anonim" sağlanmalıdır ve parola tam bir e-posta adresidir.

Kullanıcı, oturum açma ve oturum açma kimlik doğrulaması yordamları ile NetX FTP sağlamakla sorumludur. Bunlar * nx_ftp_server_create **_** işlevi sırasında sağlanır ve parola işlemeden çağrılır. _login* işlevi NX_SUCCESS, bağlantının kimliği doğrulanır ve FTP işlemlerine izin verilir. Aksi takdirde, *oturum açma* işlevi NX_SUCCESS başka bir şey döndürürse bağlantı girişimi reddedilir.

## <a name="ftp-multi-thread-support"></a>FTP Çoklu İş Parçacığı Desteği

NetX FTP İstemcisi hizmetleri aynı anda birden çok iş parçacığından çağrılabilirsiniz. Ancak, belirli bir FTP İstemcisi örneği için okuma veya yazma istekleri aynı iş parçacığından sırasıyla yapılmalı.

## <a name="ftp-rfcs"></a>FTP RFC'leri

NetX FTP, RFC959 ve ilgili RFC'ler ile uyumludur.