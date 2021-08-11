---
title: Bölüm 1 - netx duo Azure RTOS (PPP) Noktadan Noktaya Protokolü giriş
description: Bu bölümde NetX Duo Azure RTOS (PPP) Noktadan Noktaya Protokolü modülünü tanıtabilirsiniz.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 56343d563833f30ca0d48f594b547f37fa264b8961a7cd75b0786aac4791d065
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116797220"
---
# <a name="chapter-1---introduction-to-the-azure-rtos-netx-duo-point-to-point-protocol-ppp"></a>Bölüm 1 - netx duo Azure RTOS (PPP) Noktadan Noktaya Protokolü giriş

NetX uygulamaları genellikle Ethernet üzerinden gerçek fiziksel ağa bağlanır. Bu, hem hızlı hem de verimli ağ erişimi sağlar. Ancak, uygulamanın Ethernet erişimine sahip olduğu durumlar vardır. Böyle durumlarda uygulama, doğrudan başka bir ağ üyesine bağlı bir seri arabirim üzerinden ağa bağlanmaya devam ediyor olabilir. Bu tür bir bağlantıyı yönetmek için kullanılan en yaygın yazılım protokolü, Noktadan Noktaya Protokolü (PPP) protokolüdür.

Seri iletişim nispeten basit olsa da PPP biraz karmaşıktır. PPP aslında Bağlantı Denetimi Protokolü (LCP), İnternet Protokolü Denetim Protokolü (IPCP), Parola Kimlik Doğrulama Protokolü (PAP) ve Challenge-Handshake Kimlik Doğrulama Protokolü (CHAP) gibi birden çok protokolden oluşur. LCP, PPP için ana protokoldür. Bağlantının temel bileşenleri burada eşler arası bir şekilde dinamik olarak üzerinde anlaşma sağlar. Bağlantının temel özellikleri başarıyla anlaşıldıktan sonra, bağlı eşlerin geçerli olduğundan emin olmak için PAP ve/veya CHAP kullanılır. her iki eş de geçerli ise, IPCP eşler tarafından kullanılan IP adreslerini anlaşmak için kullanılır. IPCP tamamlandıktan sonra PPP, IP paketleri gönderip alır.

NetX PPP'yi öncelikli olarak bir cihaz sürücüsü olarak görüntüler. Nx_ppp_driver  işlevi, NetX IP oluşturma işlevine sağlanır ve *nx_ip_create.* Aksi takdirde, NetX'in PPP hakkında doğrudan bilgisi olmaz.

## <a name="ppp-serial-communication"></a>PPP Seri İletişimi

NetX PPP paketi, uygulamanın bir seri iletişim sürücüsü sağlamayı gerektirir. Sürücü 8 bit karakterleri desteklemeli ve yazılım akışı denetimi de içerebilir. PpP örneği oluşturmadan önce yapılması gereken sürücüyü başlatmak uygulamanın sorumluluğundadır.

PPP paketlerini göndermek için PPP'ye bir seri sürücü çıkış byte yordamı *sağlanmalıdır* (nx_ppp_create belirtilmelidir). Bu seri sürücü bayt çıkış yordamı, PPP paketinin tamamını iletmek için tekrar tekrar çağrılır. Çıktıyı arabelleğe almak seri sürücünün sorumluluğundadır. Alma tarafında, uygulamanın seri sürücüsü her yeni bir bayt geldiğinde PPP *nx_ppp_byte_receive* işlevini çağırdığında gerekir. Bu genellikle bir Kesme Hizmeti Yordamı (ISR) bağlamından yapılır. Bu *nx_ppp_byte_receive* gelen bayta döngüsel bir arabelleğe yer verir ve PPP'nin varlığının iş parçacığını alır.

## <a name="ppp-over-ethernet-communication"></a>Ethernet Üzerinden PPP İletişimi

NetX PPP, PPP iletiyi Ethernet üzerinden de iletebilir. Bu durumda, NetX PPP paketi uygulamanın bir Ethernet iletişim sürücüsü sağlamalarını gerektirir.

PPP paketlerini Ethernet üzerinden göndermek için PPP'ye bir çıkış yordamı *sağlanmalıdır* (nx_ppp_packet_send_set belirtilir). Bu çıkış yordamı, PPP paketinin tamamını iletmek için tekrar tekrar çağrılır. Alma tarafında, uygulamanın alıcısı her yeni paket geldiğinde PPP *nx_ppp_packet_receive* işlevini çağırdığında gerekir.

## <a name="ppp-packet"></a>PPP Paketi

PPP, tüm PPP protokol denetimi ve kullanıcı verilerini kapsülleme için AHDLC çerçevelerini (HDLC'nin bir alt kümesi) kullanır. AHDLC çerçevesi aşağıdakine benzer:

|**Bayrak**|**Adresi**|**Ctrl**|**Bilgi**|**Crc**|**Bayrak**|
|--------|--------|--------|---------------|-------|--------|
|7e |Ff|03|[0-1502 bayt]|2-byte| 7e|

Her PPP çerçevesi ve bu genel görünüme sahiptir. Bilgi alanı ilk iki bayt PPP protokol türünü içerir. Geçerli değerler aşağıdaki gibi tanımlanır:

- C021: LCP
- 8021: IPCP
- C023: PAP
- C223: CHAP
- 0021: IP Veri Paketi

Protokol 0x0021 varsa, IP paketi hemen takip eder. Aksi takdirde, diğer protokollerden biri varsa, aşağıdaki baytlar bu belirli protokole karşılık gelir.

KARE işaretçilerinin başında/0x7E benzersiz değerler olduğundan emin olmak ve yazılım akışı denetimi desteklemek için AHDLC, çeşitli bayt değerlerini temsil etmek için kaçış dizilerini kullanır. 0x7D değeri, aşağıdaki karakterin kodlanmış olduğunu belirtir. Bu, temel olarak ORed'e özel olarak 0x20. Örneğin, üst 0x03 Ctrl alanı için varsayılan değer iki bayt dizisiyle temsil eder: 7D 23. Varsayılan olarak, 0x20 küçük değerler bir kaçış dizisine, bilgi 0x7E ve 0x7D değerlere dönüştürülür. Kaçış dizileri CRC alanına da uygulanır.

## <a name="link-control-protocol-lcp"></a>Bağlantı Denetimi Protokolü (LCP)

LCP birincil PPP protokolüdür ve çalıştıracak ilk protokoldür. LCP, Maksimum Alma Birimi (MRU) ve Kimlik Doğrulama Protokolü (PAP, CHAP veya hiçbiri) dahil olmak üzere çeşitli PPP parametreleri üzerinde anlaşma yapmakla sorumludur. LCP'nin her iki tarafı da PPP parametrelerini kabul etti mi, varsa kimlik doğrulama protokolleri çalışmaya başlar.

## <a name="password-authentication-protocol-pap"></a>Parola Kimlik Doğrulama Protokolü (PAP)

PAP, bağlantının bir tarafı tarafından sağlanan bir ad ve parolayı (LCP sırasında anlaşıldı) bağlı olan görece basit bir protokoldür. Diğer taraf da bu bilgileri doğrular. Doğruysa, gönderene bir kabul iletisi döndürülür ve PPP IPCP durum makinesine geçebilirsiniz. Aksi takdirde, ad veya parola yanlışsa bağlantı reddedilir.

>[!NOTE]
> Arabirimin her iki tarafı da PAP isteğinde kullanılmaktadır ancak PAP genellikle tek bir yönde kullanılır.

## <a name="challenge-handshake-authentication-protocol-chap"></a>Challenge-Handshake Kimlik Doğrulama Protokolü (CHAP)

CHAP, PAP'den daha karmaşık bir kimlik doğrulama protokolüdür. CHAP kimlik doğrulayıcı, eşlerine bir ad ve değer sağlar. Eş daha sonra sağlanan adı iki varlık arasında paylaşılan bir "gizli" bulmak için kullanır. Daha sonra kimlik, değer ve "gizli" üzerinden hesaplama yapılır. Bu hesaplamanın sonucu yanıtta döndürülür. Doğruysa, PPP IPCP durum makinesine devam eder. Aksi takdirde, sonuç yanlışsa bağlantı reddedilir.

CHAP'nin bir diğer ilginç yönü de bağlantı kurulduktan sonra rastgele aralıklarla ortaya çıkabilir. Bu, kimliği doğrulandıktan sonra bir bağlantının ele geçirilene kadar önlenmesi için kullanılır. Bu rastgele zamanlarda bir zorluk başarısız olursa bağlantı hemen sonlandırılır.

>[!NOTE]
> Arabirimin her iki tarafı da CHAP isteğinde olabilir, ancak CHAP genellikle yalnızca bir yönde kullanılır.

## <a name="internet-protocol-control-protocol-ipcp"></a>İnternet Protokolü Denetim Protokolü (IPCP)

IPCP, PPP iletişimi NetX IP veri aktarımı için kullanılabilir olmadan önce yürütülecek son protokoldür. Bu protokolün ana amacı, bir eş tarafından diğerini IP adresi konusunda bilgilendirmektir. IP adresi ayardikten sonra NetX IP veri aktarımı etkinleştirilir.

## <a name="data-transfer"></a>Veri Aktarımı

Daha önce belirtildiği gibi, NetX IP veri paketleri, ip adresine sahip protokol kimliğine sahip PPP 0x0021. Alınan tüm veri paketleri bir veya daha fazla NX_PACKET yapısına yerleştirilir ve NetX alma işlemesine aktarılır. İletim sırasında NetX paketi içerikleri bir AHDLC çerçevesine yerleştirilir ve iletildi.

## <a name="ppp-rfcs"></a>PPP RFC'leri

NetX PPP RFC1332, RFC1334, RFC1661, RFC1994 ve ilgili RFC'ler ile uyumludur.