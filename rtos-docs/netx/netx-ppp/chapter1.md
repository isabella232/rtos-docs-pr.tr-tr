---
title: Bölüm 1-Azure RTOS NetX Noktadan Noktaya Protokolü 'ye giriş (PPP)
description: Genellikle NetX uygulamaları gerçek fiziksel ağa Ethernet üzerinden bağlanır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 9f8cd9e6e0ab086fcbf76df890c03f8d73aa1a99
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826657"
---
# <a name="chapter-1---introduction-to-the-azure-rtos-netx-point-to-point-protocol-ppp"></a>Bölüm 1-Azure RTOS NetX Noktadan Noktaya Protokolü 'ye giriş (PPP)

Genellikle NetX uygulamaları gerçek fiziksel ağa Ethernet üzerinden bağlanır. Bu, hem hızlı hem de verimli olan ağ erişimi sağlar. Ancak, uygulamanın Ethernet erişimi olmayan durumlar vardır. Bu gibi durumlarda, uygulama ağa doğrudan başka bir ağ üyesine bağlı bir seri arabirim aracılığıyla bağlanabilir. Böyle bir bağlantıyı yönetmek için kullanılan en yaygın yazılım Protokolü Noktadan Noktaya Protokolü (PPP).

Seri iletişimi görece basittir, ancak PPP biraz karmaşıktır. PPP aslında bağlantı denetimi Protokolü (LCP), Internet Protokolü Denetim Protokolü (ıPCP), parola kimlik doğrulama protokolü (PAP) ve Challenge-Handshake kimlik doğrulama protokolü (CHAP) gibi birden çok protokolden oluşur. LCP, PPP için ana protokoldür. Bu, bağlantının temel bileşenlerinin eşler arası bir biçimde dinamik olarak anlaşılabileceği yerdir. Bağlantının temel özelliklerine başarıyla anlaşılırsa, bir bağlı eşin geçerli olduğundan emin olmak için PAP ve/veya CHAP kullanılır. Her iki eş de geçerliyse, bu, daha sonra eşler tarafından kullanılan IP adreslerini anlaşmak için kullanılır. IPCP tamamlandığında, PPP IP paketleri gönderebilip alabilir.

NetX, PPP 'yi öncelikle bir cihaz sürücüsü olarak görüntüler. *Nx_ppp_driver* Işlevi NETX IP oluşturma işlevi, *nx_ip_create* için sağlanır. Aksi halde NetX, PPP 'nin doğrudan bir bilgisine sahip değildir.

## <a name="ppp-serial-communication"></a>PPP seri Iletişimi

NetX PPP paketi, uygulamanın bir seri iletişim sürücüsü sağlamasını gerektirir. Sürücü 8 bitlik karakterleri desteklemelidir ve ayrıca yazılım akış denetimi de kullanabilir. Bu, PPP örneği oluşturulmadan önce gerçekleştirilmesi gereken, uygulamanın, sürücünün başlatılması sorumluluğundadır.

PPP paketleri göndermek için, PPP 'ye bir seri sürücü çıkış baytı sağlanması gerekir ( *nx_ppp_create* işlevinde belirtilen). Bu seri sürücü bayt çıkışı yordamı, tüm PPP paketinin iletilmesi için kaldı olarak adlandırılır. Çıktıyı arabelleğe almak için seri sürücünün sorumluluğundadır. Alma tarafında, her yeni bayt geldiğinde uygulamanın seri sürücüsü PPP *nx_ppp_byte_receive* işlevini çağırmalıdır. Bu genellikle bir kesme hizmeti yordamının (ıSR) bağlamı içinden yapılır. *Nx_ppp_byte_receive* işlevi, gelen baytı döngüsel bir arabelleğe koyar ve BT 'nin PPP alma iş parçacığını uyarır.

## <a name="ppp-over-ethernet-communication"></a>Ethernet üzerinden PPP Iletişimi

NetX PPP Ayrıca, Ethernet üzerinden PPP iletisi aktarabilir, bu durumda NetX PPP paketi uygulamanın bir Ethernet iletişim sürücüsü sağlamasını gerektirir.

Ethernet üzerinden PPP paketleri göndermek için, PPP 'ye bir çıkış yordamının sağlanması gerekir ( *nx_ppp_packet_send_set* işlevinde belirtilen). Bu çıkış yordamı, tüm PPP paketinin iletilmesi için kaldı olarak adlandırılacaktır. Alma tarafında, her yeni paket geldiğinde uygulamanın alıcısının PPP *nx_ppp_packet_receive* işlevini çağırması gerekir.

## <a name="ppp-packet"></a>PPP paketi

PPP, tüm PPP protokol denetimi ve Kullanıcı verilerini kapsüllemek için AHDLC çerçevelemeyi (HDLC 'nin bir alt kümesi) kullanır. AHDLC çerçevesi aşağıdaki gibi görünür:

|**Bayrak**|**Addr**|**T**|**Bilgi**|**CRC**|**Bayrak**|
|--------|--------|--------|---------------|-------|--------|
|7E |BENZERI|03|[0-1502 bayt]|2 bayt| 7E|

Her bir ve her PPP çerçevesinin bu genel görünümü vardır. Bilgi alanının ilk iki baytı PPP protokol türünü içerir. Geçerli değerler aşağıdaki gibi tanımlanır:

- C021: LCP
- 8021: ıPCP
- C023: PAP
- C223: CHAP
- 0021: IP veri paketi

0x0021 protokol türü varsa, IP paketi hemen ardından takip edilir. Aksi takdirde, diğer protokollerden biri varsa, aşağıdaki baytlar ilgili protokole karşılık gelir.

Benzersiz 0x7E başlangıcını/bitiş çerçevesi işaretleyicilerini sağlamak ve yazılım akış denetimini desteklemek için, AHANLAR çeşitli bayt değerlerini temsil etmek için kaçış dizileri kullanır. 0x7D değeri, aşağıdaki karakterin kodlanmış olduğunu belirtir, bu, temel olarak özgün karakterin 0x20 ile özel ORed. Örneğin, üstbilgideki CTRL alanı için 0x03 değeri iki baytlık bir sıra ile temsil edilir: 7D 23. Varsayılan olarak, 0x20 ' den küçük değerler bir kaçış dizisine, ayrıca bilgi alanında de 0x7E ve 0x7D değerlerine dönüştürülür. Kaçış sıralarının de CRC alanı için de uygulanacağını unutmayın.

## <a name="link-control-protocol-lcp"></a>Bağlantı Denetimi Protokolü (LCP)

LCP, birincil PPP protokolüdür ve çalıştırmak için ilk protokoldür. LCP, en fazla alma birimi (MRU) ve kullanılacak kimlik doğrulama protokolü (PAP, CHAP veya None) dahil olmak üzere çeşitli PPP parametrelerinin anlaşmasından sorumludur. LCP 'nin her iki tarafında da PPP parametrelerini kabul ettikten sonra, kimlik doğrulama protokolleri (varsa) çalışmaya başlayın.

## <a name="password-authentication-protocol-pap"></a>Parola kimlik doğrulama protokolü (PAP)

PAP, bağlantının bir tarafında (LCP sırasında anlaşılırken) sağlanan bir ad ve parolaya dayanan görece bir şekilde anlaşılır protokoldür. Diğer taraf bu bilgileri doğrular. Doğru ise, gönderene bir kabul iletisi döndürülür ve PPP daha sonra ıPCP eyalet makinesine devam edebilir. Aksi takdirde, ad veya parola yanlışsa bağlantı reddedilir.

>[!NOTE]
> Arabirimin her iki tarafı PAP isteğinde bulunabilir, ancak PAP genellikle yalnızca bir yönde kullanılır.

## <a name="challenge-handshake-authentication-protocol-chap"></a>Challenge-Handshake kimlik doğrulama protokolü (CHAP)

CHAP, PAP 'dan daha karmaşık bir kimlik doğrulama protokolüdür. CHAP Authenticator, eşi için bir ad ve değer sağlar. Daha sonra eş, iki varlık arasında paylaşılan bir "gizli dizi" bulmak için sağlanan adı kullanır. Daha sonra bir hesaplama ID, Value ve "Secret" üzerinden yapılır. Bu hesaplamanın sonucu yanıtta döndürülür. Doğru ise, PPP ıPCP eyalet makinesine devam edebilir. Aksi takdirde, sonuç yanlışsa bağlantı reddedilir.

CHAP 'nin başka bir ilgi çekici yönü, bir bağlantı kurulduktan sonra rastgele aralıklarda gerçekleşebilirler. Bu, bir bağlantının, kimlik doğrulamasından geçtikten sonra ele geçirilmesini engellemek için kullanılır. Bu rastgele zamanlarda bir zorluk başarısız olursa bağlantı hemen sonlandırılır.

>[!NOTE]
> Arabirimin her iki tarafı de CHAP isteğinde bulunabilir, ancak CHAP genellikle yalnızca bir yönde kullanılır.

## <a name="internet-protocol-control-protocol-ipcp"></a>Internet Protokolü Denetim Protokolü (ıPCP)

IPCP, NetX IP veri aktarımı için PPP iletişimi kullanılabilir olmadan önce yürütülecek son protokoldür. Bu protokolün ana amacı, bir eşin IP adreslerini bilgilendirmek için kullanılır. IP adresi kurulduktan sonra NetX IP veri aktarımı etkinleştirilir.

## <a name="data-transfer"></a>Veri Aktarımı

Daha önce belirtildiği gibi, NetX IP veri paketleri, protokol KIMLIĞI 0x0021 olan PPP çerçevelerinde bulunur. Alınan tüm veri paketleri bir veya daha fazla NX_PACKET yapılarına konur ve NetX alma işlemine aktarılır. İletimde, NetX paket içerikleri AHDLC çerçevesine yerleştirilir ve iletilir.

## <a name="ppp-rfcs"></a>PPP RFC 'Leri

NetX PPP, RFC1332, RFC1334, RFC1661, RFC1994 ve ilgili RFC 'lerle uyumludur.