---
title: Bölüm 1-Azure RTOS NetX Duo FTP 'ye giriş
description: Dosya Aktarım Protokolü (FTP), dosya aktarımları için tasarlanmış bir protokoldür.
author: philmea
ms.author: philmea
ms.date: 07/14/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 1d56b20b1c7d719d1b7d9c8c5b2fe234d5577da3
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825985"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-ftp"></a>Bölüm 1-Azure RTOS NetX Duo FTP 'ye giriş

Dosya Aktarım Protokolü (FTP), dosya aktarımları için tasarlanmış bir protokoldür. FTP, dosya aktarım işlevini gerçekleştirmek için güvenilir Iletim Denetimi Protokolü (TCP) hizmetlerinden yararlanır. Bu nedenle, FTP son derece güvenilir bir dosya aktarım protokolüdür. FTP de yüksek Performansdır. Gerçek FTP dosya aktarımı, adanmış bir FTP bağlantısında gerçekleştirilir. NetX Duo FTP hem IPv4 hem de IPv6 ağlarını karşılar. Özgün NetX FTP API 'sindeki bazı değişiklikler IPv6 'Yı barındırmak için gerekli olmasına rağmen IPv6, FTP protokolünü doğrudan değiştirmez, ancak bu belgede açıklanacaktır.

## <a name="ftp-requirements"></a>FTP gereksinimleri

Düzgün çalışması için NetX FTP paketi NetX Duo gerektirir. Konak uygulamanın NetX Hizmetleri ve düzenli görevleri çalıştırmak için bir IP örneği oluşturması gerekir. FTP ana bilgisayar uygulamasının bir IPv6 ağı üzerinde çalıştırılması, IP görevinde IPv6 ve ICMPv6 'nin etkinleştirilmesi gerekir. IPv6 veya IPv4 ağları için de TCP 'nin etkinleştirilmesi gerekir. IPv6 ana bilgisayar uygulamasının, IPv6 API ve/veya DHCPv6 kullanarak linklocal ve Global IPv6 adreslerini ayarlaması gerekir. Bölüm **2** ' de "küçük örnek sistem" bölümündeki bir demo programı bunun nasıl yapıldığını gösterir.

FTP sunucusu ve Istemcisi de, FileX Embedded dosya sistemiyle çalışmak üzere tasarlanmıştır. FileX kullanılamıyorsa, konak geliştiricisi, bu dosyada listelenen hizmetlerin her birini tanımlayarak filex_stub. h ' de önerilen yönergeleri izleyerek kendi dosya sistemlerini uygulayabilir veya değiştirebilir. Bu, bu kılavuzun sonraki bölümlerinde ele alınmıştır.

NetX FTP paketinin FTP Istemci bölümünün başka gereksinimi yoktur.

NetX FTP paketinin FTP sunucusu bölümünde birkaç ek gereksinim vardır. İlk olarak, tüm istemci FTP komut isteklerini ve tüm Istemci FTP veri aktarımlarını işlemek için *iyi bilinen bağlantı noktası 20 ' sini* IŞLEMEK üzere TCP 'nin *iyi bilinen bağlantı noktası 21* ' e tam erişim gerektirir.

## <a name="ftp-constraints"></a>FTP kısıtlamaları

FTP standardı, dosya verilerinin gösterimiyle ilgili birçok seçeneğe sahiptir. NetX FTP; ls – al gibi anahtar seçeneklerini uygulamaz. NetX FTP sunucusu, istekleri ve bağımsız değişkenlerini ardışık paketler yerine tek bir pakette almayı bekler.

UNIX uygulamalarına benzer şekilde NetX FTP aşağıdaki dosya biçimi kısıtlamalarını varsayar:

- Dosya türü: **ikili**
- Dosya biçimi: **Yalnızca baskı dışı**
- Dosya yapısı: **yalnızca dosya yapısı**

## <a name="ftp-file-names"></a>FTP dosya adları

FTP dosya adları, hedef dosya sisteminin (genellikle FileX) biçiminde olmalıdır. Gerektiğinde tam yol bilgileriyle, NULL olarak sonlandırılmış ASCII dizeleri olmalıdır. NetX FTP uygulamasındaki FTP dosya adlarının boyutu için belirtilen sınır yoktur. Ancak, paket havuzu yük boyutu, en büyük yolu ve/veya dosya adını barındırabilmelidir.

## <a name="ftp-client-commands"></a>FTP Istemci komutları

FTP 'nin bağlantıları açmak ve dosya ve dizin işlemlerini gerçekleştirmek için basit bir mekanizması vardır. Temel olarak *BILINEN TCP bağlantı noktası 21*' de bir bağlantı başarıyla kurulduktan sonra istemci tarafından VERILEN standart FTP komutları kümesi vardır. Aşağıdakiler, temel FTP komutlarının bazılarını göstermektedir. FTP 'nin IPv6 üzerinden çalıştırıldığı zaman farkının, bağlantı noktası komutunun EPRT komutuyla değiştirildiğini unutmayın:

- CWD yolu *çalışma dizinini değiştirme*
- SIL filename *belirtilen dosya adını Sil*
- EPRT ip_address, bağlantı noktası *IPv6 adresi ve istemci veri bağlantı noktası sağlar*
- IPv6 için EPSV *istek pasif aktarım modu*
- Dizin LISTESINI *Al dizin listeleme*
- MKD dizini *Yeni dizin oluştur*
- NLST dizini *dizin listesini al*
- NOOP *No işlemi, başarı döndürüyor*
- Parola parola *sağla oturum açma adı*
- *IPv4 IÇIN PASV isteği pasif aktarım modu*
- Bağlantı noktası ip_address, bağlantı noktası *IP adresi ve istemci veri bağlantı noktası sağlar*
- PWD yol yolu *alma geçerli dizin yolu*
- *Sonlandırma istemci bağlantısını* çıkar
- RETR dosya adı *belirtilen dosyayı oku*
- RMD dizini *belirtilen dizini Sil*
- RNFR OldFileName *yeniden adlandırılacak dosyayı belirt*
- RNNEWFILENAME *dosyayı sağlanan dosya adına yeniden adlandır*
- STOR dosya adı *belirtilen dosyayı yaz*
- *İkili dosya görüntüsünü SEÇIN* yazın
- Kullanıcı Kullanıcı adı *oturum açma için* Kullanıcı adı sağlar

Bu ASCII komutları, FTP sunucusu ile FTP işlemleri gerçekleştirmek için NetX FTP Istemci yazılımı tarafından dahili olarak kullanılır.

## <a name="ftp-server-responses"></a>FTP sunucusu yanıtları

FTP sunucusu Istemci isteğini işlediğinde, ASCII 'de isteğe bağlı ASCII metin gelen 3 basamaklı kodlanmış bir yanıt döndürür. Sayısal yanıt, işlemin başarılı veya başarısız olup olmadığını anlamak için FTP Istemci yazılımı tarafından kullanılır. Aşağıdaki listede, Istemci isteklerine yönelik çeşitli FTP sunucusu yanıtları gösterilmektedir:

**İlk sayısal alan anlamı**

- 1xx *pozitif ön durum – başka bir yanıt geliyor*.
- 2xx *pozitif tamamlanma durumu*.
- 3xx *pozitif ön durum – başka bir komutun gönderilmesi gerekir*.
- 4xx *geçici hata koşulu*.
- 5xx *hata koşulu.*

**İkinci sayısal alan anlamı**

- *komutta X0x sözdizimi hatası*.
- x1x *bilgi iletisi*.
- X2X *bağlantısı ile ilgili*.
- x3x *kimlik doğrulaması ile ilgili*.
- x4x *belirtilmemiş*.
- x5x *dosya sistemiyle ilgili*.

Örneğin, çıkış komutu ile FTP bağlantısının bağlantısını kesme isteği genellikle sunucudan bir "221" kodu ile yanıt vermeyecektir. bağlantı kesilmesi başarılı olursa.

## <a name="ftp-passive-transfer-mode"></a>FTP pasif aktarım modu

Varsayılan olarak, NetX Duo FTP Istemcisi, veri yuvası üzerinde verileri FTP sunucusu ile değiş tokuş etmek için etkin aktarım modunu kullanır. Bu düzenleme ile ilgili sorun, FTP Istemcisinin bağlanmak için FTP sunucusunun bir TCP sunucu yuvasını açmasını gerektirmesidir. Bu, olası bir güvenlik riskini temsil eder ve Istemci güvenlik duvarı tarafından engelleniyor olabilir. Pasif aktarım modu, FTP sunucusunun veri bağlantısında TCP sunucusu yuvasını oluşturması için etkin aktarım modundan farklıdır. Bu, güvenlik riskini ortadan kaldırır (FTP Istemcisi için).

Pasif veri aktarımını etkinleştirmek için uygulama, ikinci bağımsız değişkeni NX_TRUE olarak ayarlanan daha önce oluşturulmuş bir FTP Istemcisinde *nx_ftp_client_passive_mode_set* çağırır. Bundan sonra, verileri aktarmaya yönelik tüm sonraki NetX Duo FTP Istemci Hizmetleri (NLST, RETR, STOR) pasif Aktarım modunda denenir.

FTP Istemcisi önce pasif komutu (bağımsız değişken yok), IPv4 için PASV komutu veya IPv6 için EPSV komutu gönderir. FTP sunucusu bu isteği destekliyorsa, PASV için 227 "Tamam" yanıtı ve EPSV için 229 "Tamam" yanıtı döndürülür. Daha sonra Istemci isteği gönderir, örneğin. Sunucu Pasif aktarım modunu reddederse NetX Duo FTP Istemci hizmeti bir hata durumu döndürür.

Pasif aktarım modunu devre dışı bırakıp etkin aktarım moduna geri dönmek için, uygulama NX_FALSE olarak ayarlanan ikinci bağımsız değişkenle *nx_ftp_client_passive_mode_set* çağırır.

## <a name="ftp-communication"></a>FTP Iletişimi

FTP sunucusu, Istemci isteklerini alan *iyi BILINEN TCP bağlantı noktası 21* ' i kullanır. FTP Istemcileri, kullanılabilir herhangi bir TCP bağlantı noktasını kullanabilir. FTP olaylarının genel dizisi aşağıdaki gibidir:

**FTP okuma dosyası istekleri**:

1. İstemci, sunucu bağlantı noktası 21 ' e TCP bağlantısı verir.
1. Sunucu, "220" yanıtını sinyal başarısına gönderir.
1. İstemci "username" ile "Kullanıcı" iletisi gönderir.
1. Sunucu, "331" yanıtını sinyal başarısına gönderir.
1. İstemci "parola" ile "PASS" iletisi gönderir.
1. Sunucu, "230" yanıtını sinyal başarısına gönderir.
1. İstemci ikili aktarım için "tür I" iletisi gönderir.
1. Sunucu, "200" yanıtını sinyal başarısına gönderir.
1. *IPv4 uygulamaları*: ISTEMCI, IP adresi ve bağlantı noktası IÇEREN "bağlantı noktası" iletisi gönderir.<br />*IPv6 uygulamaları*: ISTEMCI, IP adresi ve bağlantı noktası içeren "EPRT" iletisi gönderir.
1. Sunucu, "200" yanıtını sinyal başarısına gönderir.
1. İstemci, okunan dosya adına sahip "RETR" iletisi gönderir.
1. Sunucu, "PORT" komutunda belirtilen istemci veri bağlantı noktasıyla veri yuvası oluşturur ve bağlar.
1. Sunucu, okunan sinyal dosyası "125" yanıtını gönderiyor.
1. Sunucu, veri bağlantısı aracılığıyla dosyanın içeriğini gönderir. Bu işlem, dosya tamamen aktarılana kadar devam eder.
1. İşiniz bittiğinde, sunucu veri bağlantısını keser.
1. Sunucu "250" yanıtını "" olarak göndererek okunan sinyal dosyası başarılı olur.
1. İstemci, FTP bağlantısını sonlandırmak için "QUIT" iletisi gönderir.
1. Sunucu "221" sinyal bağlantısını kesme yanıtı başarılı oldu.
1. Sunucu FTP bağlantısının bağlantısını keser.

Daha önce belirtildiği gibi, IPv4 üzerinde çalışan FTP arasındaki tek fark

IPv6, bağlantı noktası komutunun, IPv6 için EPRT komutuyla değiştirilmiştir

FTP Istemcisi pasif Aktarım modunda bir okuma isteği yapıyorsa, komut sırası aşağıdaki gibidir (**kalın** çizgiler, etkin aktarım modundan farklı bir adım gösterir):

1. İstemci, sunucu bağlantı noktası 21 ' e TCP bağlantısı verir.
1. Sunucu, "220" yanıtını sinyal başarısına gönderir.
1. İstemci "username" ile "Kullanıcı" iletisi gönderir.
1. Sunucu, "331" yanıtını sinyal başarısına gönderir.
1. İstemci "parola" ile "PASS" iletisi gönderir.
1. Sunucu, "230" yanıtını sinyal başarısına gönderir.
1. İstemci ikili aktarım için "tür I" iletisi gönderir.
1. Sunucu, "200" yanıtını sinyal başarısına gönderir.
1. ***IPv4 uygulamaları:* İstemci "PASV" iletisi gönderir.**<br />**_IPv6 uygulamaları:_ İstemci "EPSV" iletisi gönderir.**
1. ***IPv4 uygulamaları:* Sunucu, Istemciye Bağlanılacak "227" yanıtını ve IP adresini ve bağlantı noktasını başarılı bir şekilde sinyaline gönderir.**<br />**_IPv6 uygulamaları:_ Sunucu, Istemciye Bağlanılacak "229" yanıtını ve IP adresini ve bağlantı noktasını başarılı bir şekilde sinyaline gönderir.**
1. İstemci, okunan dosya adına sahip "RETR" iletisi gönderir.
1. **Sunucu, veri sunucusu yuvası oluşturur ve 10. adımdaki yanıtta belirtilen bağlantı noktasını kullanarak bu yuvadaki Istemci bağlantı isteğini dinler.**
1. **Sunucu, okunan dosyayı işaret eden denetim soketine "150" yanıtı gönderir.**
1. Sunucu, veri bağlantısı aracılığıyla dosyanın içeriğini gönderir. Bu işlem, dosya tamamen aktarılana kadar devam eder.
1. İşiniz bittiğinde, sunucu veri bağlantısını keser.
1. **Sunucu, okuma sinyali almak için denetim yuvasında "226" yanıtı gönderir.**
1. İstemci, FTP bağlantısını sonlandırmak için "QUIT" iletisi gönderir.
1. Sunucu "221" sinyal bağlantısını kesme yanıtı başarılı oldu.
1. Sunucu FTP bağlantısının bağlantısını keser.

**FTP yazma istekleri**:

1. İstemci, sunucu bağlantı noktası 21 ' e TCP bağlantısı verir.
1. Sunucu, "220" yanıtını sinyal başarısına gönderir.
1. İstemci "username" ile "Kullanıcı" iletisi gönderir.
1. Sunucu, "331" yanıtını sinyal başarısına gönderir.
1. İstemci "parola" ile "PASS" iletisi gönderir.
1. Sunucu, "230" yanıtını sinyal başarısına gönderir.
1. İstemci ikili aktarım için "tür I" iletisi gönderir.
1. Sunucu, "200" yanıtını sinyal başarısına gönderir.
1. *IPv4 uygulamaları*: ISTEMCI, IP adresi ve bağlantı noktası IÇEREN "bağlantı noktası" iletisi gönderir.<br />*IPv6 uygulamaları*: ISTEMCI, IP adresi ve bağlantı noktası içeren "EPRT" iletisi gönderir.
1. Sunucu, "200" yanıtını sinyal başarısına gönderir.
1. İstemci, yazılacak dosya adına sahip "STOR" iletisi gönderir.
1. Sunucu, veri yuvası oluşturur ve önceki "EPRT" veya "PORT" komutunda belirtilen istemci veri bağlantı noktasıyla bağlanır.
1. Sunucu, "125" yanıtını sinyal dosyası yazma işlemi için gönderir.
1. İstemci, veri bağlantısı aracılığıyla dosyanın içeriğini gönderir. Bu işlem, dosya tamamen aktarılana kadar devam eder.
1. İşiniz bittiğinde, Istemci veri bağlantısını keser.
1. Sunucu, "250" sinyal dosyası yazma yanıtı başarılı oldu.
1. İstemci, FTP bağlantısını sonlandırmak için "QUIT" iletisi gönderir.
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
1. ***IPv4 uygulamaları:* İstemci "PASV" iletisi gönderir.**<br />**_IPv6 uygulamaları:_ İstemci "EPSV" iletisi gönderir.**
1. ***IPv4 uygulamaları:* Sunucu, Istemciye Bağlanılacak "227" yanıtını ve IP adresini ve bağlantı noktasını başarılı bir şekilde sinyaline gönderir.**<br />**_IPv6 uygulamaları:_ Sunucu, Istemciye Bağlanılacak "229" yanıtını ve IP adresini ve bağlantı noktasını başarılı bir şekilde sinyaline gönderir.**
1. İstemci, yazılacak dosya adına sahip "STOR" iletisi gönderir.
1. **Sunucu, veri sunucusu yuvası oluşturur ve 10. adımdaki yanıtta belirtilen bağlantı noktasını kullanarak bu yuvadaki Istemci bağlantı isteğini dinler.**
1. **Sunucu, denetim soketine dosya yazmayı işaret eden "150" yanıtı gönderir.**
1. İstemci, veri bağlantısı aracılığıyla dosyanın içeriğini gönderir. Bu işlem, dosya tamamen aktarılana kadar devam eder.
1. İşiniz bittiğinde, Istemci veri bağlantısını keser.
1. **Sunucu, "226" yanıtını denetim soketine dosya yazmayı işaret etmek için gönderir.**
1. İstemci, FTP bağlantısını sonlandırmak için "QUIT" iletisi gönderir.
1. Sunucu "221" sinyal bağlantısını kesme yanıtı başarılı oldu.
1. Sunucu FTP bağlantısının bağlantısını keser.

## <a name="ftp-authentication"></a>FTP Kimlik Doğrulaması

FTP bağlantısı gerçekleştiğinde, Istemcinin sunucuya bir *Kullanıcı adı* ve *parola* sağlaması gerekir. Bazı FTP siteleri, *anonım FTP* olarak adlandırılan, belirli bir Kullanıcı adı ve parola olmadan FTP erişimine izin verir. Bu bağlantı türü için, Kullanıcı adı için "anonim" belirtilmelidir ve parola, tüm e-posta adresi olmalıdır.

Kullanıcı, oturum açma ve oturum kapatma kimlik doğrulama yordamlarına sahip NetX FTP sağlamaktan sorumludur. Bunlar, ***nxd_ftp_server_create** _ ve _*_nx_ftp_server_create_*_ hizmetleri sırasında sağlanır ve parola işlemeden çağırılır. İkisi arasındaki fark, oturum açma ve oturum kapatma için _*_nxd_ftp_server_create_*_ giriş işlevi Işaretçileridir NETX Duo adres türü _*_NXD_ADDRESS_*_ bekler. Bu veri türü hem IPv4 hem de IPv6 adres biçimlerini barındırır ve bu işlevi hem IPv4 hem de IPv6 ağlarını destekleyen "Duo" hizmeti yapar. LOGIN ve Logout kimlik doğrulama işlevlerinin _ *_nx_ftp_server_create_** giriş işlevi IŞARETÇILERI, ulong IP adresi türünü bekler. Bu işlev, IPv4 ağları ile sınırlıdır. Geliştiricinin mümkün olduğunca "Duo" hizmetini kullanması önerilir.

*Oturum açma* işlevi NX_SUCCESS döndürürse bağlantı DOĞRULANıR ve FTP işlemlerine izin verilir. Aksi takdirde, *oturum açma* işlevi NX_SUCCESS dışında bir şey döndürürse bağlantı girişimi reddedilir.

## <a name="ftp-multi-thread-support"></a>FTP çoklu Iş parçacığı desteği

NetX FTP Istemci Hizmetleri birden çok iş parçacığından aynı anda çağrılabilir. Ancak, belirli bir FTP Istemcisi örneği için okuma veya yazma istekleri aynı iş parçacığından sırayla yapılmalıdır.

## <a name="ftp-rfcs"></a>FTP RFC 'Leri

NetX Duo FTP, RFC 959, RFC 2428 ve ilgili RFC 'lerle uyumludur.
