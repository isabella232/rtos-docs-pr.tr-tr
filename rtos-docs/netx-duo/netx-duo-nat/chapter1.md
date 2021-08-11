---
title: Bölüm 1-ağ adresi çevirisine giriş
description: IP ağ adresi çevirisi (NAT), aslında sınırlı sayıda Internet IPv4 adresi sorununu çözmek için geliştirilmiştir.
author: philmea
ms.author: philmea
ms.date: 07/14/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 8639b87decd78f58a34fe6b8033a2427b560c872814abfdbbcb6057166412d0d
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116797474"
---
# <a name="chapter-1---an-introduction-to-network-address-translation"></a>Bölüm 1-ağ adresi çevirisine giriş

## <a name="the-need-for-network-address-translation"></a>Ağ adresi çevirisi gereksinimi

IP ağ adresi çevirisi (NAT), aslında sınırlı sayıda Internet IPv4 adresi sorununu çözmek için geliştirilmiştir. Birden çok cihazın Internet 'e erişmesi gerektiğinde, ancak Internet servis sağlayıcısı (ISS) tarafından yalnızca bir IPv4 Internet adresi atandığında NAT için ihtiyaç vardır.

NAT kullanmanın başka avantajları da vardır. Yerel etki alanı dışındaki ağ topolojisi birçok şekilde değişebilir. Müşteriler sağlayıcıları değiştirebilir, şirket geri kemikleri yeniden düzenlenemeyebilir veya sağlayıcılar birleştirebilir veya bölünebilir. Dış topoloji değiştiğinde, yerel etki alanındaki konaklar için adres atamaları da bu dış değişiklikleri yansıtacak şekilde değişmelidir. Bu türdeki değişiklikler, tek bir adres çevirisi yönlendiricisinde yapılan değişiklikleri merkezileştirerek etki alanı içindeki kullanıcılardan gizlenebilir. NAT, yerel konaklar için genel Internet 'e erişim sağlar ve bunların dışından doğrudan erişime karşı korur. İç kullanım için bir ağ kurulumu ağırlıklı olan kuruluşlar, zaman zaman dış erişime gerek duyulan bu düzen için iyi adaylardır.

## <a name="basic-nat-and-network-address-port-translation"></a>Temel NAT ve ağ adresi bağlantı noktası çevirisi

Ortak ağ ile özel ağ arasında NAT özellikli bir yönlendirici yüklenir. NAT özellikli yönlendiricinin rolü, iç özel IPv4 adresleri ve atanan ortak IPv4 adresi arasında çevrilecek, böylece özel ağdaki tüm cihazlar aynı ortak IPv4 adresini paylaşabilir.

NAT 'ın temel uygulamasında, NAT yönlendiricisinin kendi IP adresinden farklı olarak bir veya daha fazla küresel olarak kayıtlı IP adresi vardır. Bu genel adresler, kendi özel ağındaki ana bilgisayarlara statik veya dinamik olarak atamak için kullanılabilir. NAPT veya ağ adresi bağlantı noktası çevirisi, ağ adresi çevirisi 'nin bir ' Transport ' tanımlayıcısı içerecek şekilde uzatılmasının temel NAT 'nin bir çeşitlemesi. Genellikle bu, TCP ve UDP paketlerinin bağlantı noktası numarasıdır ve ıCMP paketlerinin sorgu KIMLIĞIDIR.

NAT sınırları genelinde bağlantılar genellikle dış bir konağa giden paketleri gönderen özel ağ üzerinde konaklar tarafından başlatılır. Bu konaklar genellikle bu amaçla *dinamik* (GEÇICI) IP adresleri atanır. Ancak, özel ağda ' sunucular ' (örneğin, dış ağdan gelen Istemci isteklerini kabul edecek şekilde HTTP veya FTP sunucuları) varsa, bağlantıların ters yönde başlatılması de mümkündür. NAT genellikle bu yerel Konakları *statik* (kalıcı) bir IP adresi: bağlantı noktası olarak atar.

## <a name="how-network-address-translation-works"></a>Ağ adresi çevirisi nasıl kullanılır

NAT özellikli bir yönlendirici olan tipik bir ağ kurulumu Şekil 1 ' de gösterilmiştir.

![NAT özellikli yönlendirici olan tipik bir ağ kurulumu](media/image2.png)

**Şekil 1-NAT özellikli yönlendirici olan tipik bir ağ kurulumu**

NAT özellikli yönlendirici genellikle iki ağ arabirimine sahiptir. Bir arabirim, genel Internet 'e bağlı; diğeri özel ağa bağlanır. Bu kurulumda tipik bir yönlendirici, özel ağ ile genel ağ arasında hedef IP adresine dayalı IP datagramları yönlendirmesinden sorumludur. NAT özellikli bir yönlendirici, ortak ve özel arabirim arasında bir IPv4 datagramı yönlendirmeden önce adres çevirisini gerçekleştirir. Her TCP veya UDP oturumu için, iç kaynak adresi, kaynak bağlantı noktası numarası ve dış hedef adresi ve hedef bağlantı noktası numarası temelinde bir çeviri oluşturulur. ICMP yankı isteği ve yanıt veri birimi için, bağlantı noktası numarası yerine ıCMP sorgu KIMLIĞI kullanılır.

Ağ adresi çevirisi 'nin tipik bir uygulamasını göstermek için Şekil 2 ' de bir ağ kurulumunu düşünmemize izin verin.

![Ağ adresi çevirisi 'nin tipik bir uygulama](media/image3.png)

**Şekil 2-ağ adresi çevirisi 'nin tipik bir uygulanması**

Bu senaryoda, NAT yönlendiricisi özel ağı sola ve ortak ağı sağa bağlar. Genel ağ tarafında, NAT yönlendirici arabirimi IP adresinin 202.151.25.14 olduğunu varsayalım. özel ağ arabiriminde, NAT yönlendiricisi 192.168.1.254 IP adresini kullanır. Özel ağdaki bir düğüm, Internet üzerindeki bir Web sunucusuyla TCP bağlantısı başlatır.

Şekil 3 ' te, ağ adresi çevirisi işleminin üst düzey bir görünümü gösterilmektedir.

![Ağ adresi çevirisi işleminin üst düzey bir görünümü](media/image4.png)

**Şekil 3-ağ adresi çevirisi işleminin üst düzey bir görünümü**

1. İstemci bir TCP SYN iletisini Web sunucusuna iletir. Gönderen adresi 192.168.1.15, bağlantı noktası numarası 6732; Hedef adres 128.15.54.3, bağlantı noktası numarası 80 ' dir.
1. Istemciden paket, NAT yönlendiricisi tarafından özel ağ arabiriminde alınır. Giden trafik kuralı paket için geçerlidir: gönderenin (Istemci) adresi NAT yönlendiricisinin Genel IP adresine çevrilir 202.15.25.14 ve gönderici (Istemci) kaynak bağlantı noktası numarası, ortak arabirimde 2015 numaralı TCP bağlantı noktasına çevrilir.
1. Paket daha sonra Internet üzerinden iletilir ve sonuç olarak hedef ana bilgisayar 128.15.54.3 ulaşır. Alma tarafında, IP katmanı kaynak adresi ve TCP katmanı bağlantı noktası numarası temelinde, paketin kaynaklandığı 202.151.24.14, bağlantı noktası numarası 2015 olduğunu görürsünüz.
   Şekil 4 ' te, dönüş yolundaki NAT işlemi gösterilmektedir.

   ![Dönüş yolunda NAT işlemi](media/image5.png)

   **Şekil 4-dönüş yolunda NAT işlemi**
1. Bu senaryoda, 128.15.54.3 Internet ana bilgisayarı, hedefi olarak NAT yönlendiricisinin Internet adresine sahip bir yanıt paketi gönderir.
1. Paket, NAT yönlendiricisine ulaşır. Bu bir yerleşik paket olduğundan, bağlantılı çeviri kuralları geçerlidir: hedef adres özgün gönderenin (Istemci) IP adresine geri dönüştürülür: 192.168.1.15, hedef bağlantı noktası numarası 6732.
1. Paket daha sonra iç ağa bağlı arabirim aracılığıyla Istemciye iletilir.

Bu şekilde, gönderenin Internet ağ adresi ve bağlantı noktası numarası, genel Internet 'teki diğer ana bilgisayarlara gösterilmez.

## <a name="netx-duo-nat-features"></a>NetX Duo NAT özellikleri

NAT örneği *nx_nat_create* çağrısı KULLANıLARAK oluşturulduğunda NAT çeviri tablosu oluşturulur.

```C
UINT nx_nat_create(NX_NAT_DEVICE *nat_ptr, NX_IP *ip_ptr,
    UINT global_interface_index,
    VOID *dynamic_cache_memory,
    UINT dynamic_cache_size);
```

Yerel ve dış ağlar arasındaki tüm etkin bağlantılar için ağ adresi çevirilerini izlemek üzere NetX Duo NAT etkin yönlendiricisi, kaynak ve hedef IP adresi ve bağlantı noktası numarası içeren her bir özel ana bilgisayar bağlantısı hakkında bilgi içeren bir çeviri tablosu tutar.

Bu çeviri tablosunun konumu ("cache") dynamic_cache_memory işaretçisiyle ayarlanır. Bu alan 4 bayt hizalı bir arabellek alanı olmalıdır. Tablonun boyutu (veya giriş sayısı), bir NAT tablosu girişi boyutuna göre dynamic_cache_size önbellek boyutu bölünerek belirlenir. Tablo, ***nx_nat. h* içinde tanımlanan NX_NAT_MIN_ENTRY_COUNT tarafından belirtilen en az sayıda giriş için yeterince büyük olmalıdır. Varsayılan değer 3 ' dir.**

NetX Duo NAT çeviri tablosundaki tüm dinamik girişler için zaman aşımı, *nx_nat. h* içinde tanımlanan NX_NAT_ENTRY_RESPONSE_TIMEOUT olarak başlatılır. Varsayılan değer, RFC 2663 tarafından önerildiği şekilde 4 dakikadır (veya 100 mHz işlemci için 240 sistem Ticks). NetX Duo NAT her seferinde, bu girişin NX_NAT_ENTRY_RESPONSE_TIMEOUT zaman aşımını sıfırladığında, bu tablodaki dinamik bir girdiyle eşleşen bir paket alır veya gönderir. NetX Duo NAT, tabloda arama yaparken Ayrıca, bu tabloyu süre dolma girdileri için denetler ve siler.

Yerel ağdaki sunucular için, örneğin, yerel ağdaki sunucular için gelen girdileri statik olarak oluşturmak için, NetX Duo NAT *nx_nat_inbound_entry_create* hizmeti sağlar. Bir tablo girişi yerel ana bilgisayar bağlantısını statik olarak tanımlıyorsa, süresi dolmayacaktır.

```C
UINT nx_nat_inbound_entry_create(NX_NAT_DEVICE *nat_ptr,
    NX_NAT_TRANSLATION_ENTRY *entry_ptr,
    ULONG local_ip_address, USHORT external_port,
    USHORT local_port, UCHAR protocol);
```

Bu hizmet, [Bölüm 4 ' te hizmetlerin açıklaması](chapter4.md) bölümünde daha ayrıntılı olarak açıklanmıştır

Çalışma zamanı sırasında, Çeviri tablosu doluysa ve daha fazla giriş eklenememişse NetX Duo NAT, NAT örneğiyle kayıtlıysa, bir önbellek tam geri çağırması ile NAT uygulamasına bildirim gönderir. Bu, *nx_nat_cache_notify_set* hizmeti kullanılarak yapılır:

```C
UINT nx_nat_cache_notify_set(NX_NAT_DEVICE *nat_ptr,
    VOID (*cache_full_notify_cb)(NX_NAT_DEVICE *nat_ptr));
```

Bu hizmetle ilgili daha fazla ayrıntı için bkz. [Bölüm 4-hizmetlerin açıklaması](chapter4.md) .

## <a name="nat-packet-processing-in-netx-duo"></a>NetX Duo 'da NAT paket Işleme

NetX Duo NAT, bir IPv4 yönlendiricisinde kullanılmak üzere tasarlanmıştır. NAT 'nin çalışması için NetX Duo paketlerin NAT sunucusuna iletilmesi için yapılandırılmış olması gerekir. Bunun nasıl yapılacağını öğrenmek için NetX Duo NAT yüklemesinde Bölüm 2 ' ye bakın. NAT sunucusu daha sonra, ağ üzerindeki bir konağa ' tüketin ' (iletme girişimi) anlamına gelir. Paketi tüketmezse, paket normalde olduğu gibi paket işlemek için NetX Duo 'e ' döndürülür.

NAT sunucusu NetX Duo 'dan iletmek üzere bir paket aldığında, paketin gelen veya giden bir paket olup olmadığını belirler.

Giden paketler için NAT sunucusu, paket IP üstbilgisi kaynak adresini ve bağlantı noktasını denetler. Çeviri tablosu, aynı hedef için daha önce bu konak tarafından gönderilen bir paket için bir girdi içermiyorsa, NAT, benzersiz bir genel kaynak IP adresi (bağlantı için bağlantı noktası) içeren yeni bir giriş oluşturur ve paket üst bilgilerini dış ağa göndermeden önce bu yeni IP adresi: bağlantı noktası ile değiştirir.

Gelen paketler için NAT sunucusu, çeviri tablosunda bir dış IP adresi ile eşleşen önceki bir girişi arar: bağlantı noktası, paket hedefi IP adresiyle eşleşiyor: bağlantı noktası. Eşleşme bulunmazsa, hedef adres: bağlantı noktası yerel ağdaki sunucu için dış adres değilse, paket atılır. Bir eşleşme bulıyorsa, paket üstbilgisinin dış hedef IP adresini (bağlantı noktası) özel IP adresi: bağlantı noktası ile değiştirir ve yerel ağa hedeflenen özel ana bilgisayar üzerinde gönderir.

NetX Duo NAT, benzersiz yerel adres oluşturmak için bir dizi TCP, UDP ve ıCMP çeviri bağlantı noktası kullanır: dış konaklarla bağlanan yerel konaklar için bağlantı noktası bağlantıları. *Nx_nat. h* 'de tanımlanan aşağıdaki kullanıcı yapılandırılabilir seçenekleri, her protokol için aralığı tanımlar:

```C
NX_NAT_START_TCP_PORT

NX_NAT_END_TCP_PORT

NX_NAT_START_UDP_PORT

NX_NAT_END_UDP_PORT

NX_NAT_START_ICMP_QUERY_ID

NX_NAT_END_ICMP_QUERY_ID
```

## <a name="nat-requirements-and-constraints"></a>NAT gereksinimleri ve kısıtlamaları

NetX Duo NAT, NetX Duo 5,8 veya üstünü gerektirir. NAT uygulaması, tek bir IP örneği oluşturulmasını ve iç ve dış fiziksel ağa yönelik bir arabirim gerektirir.

Kısıtlamaları

- NetX Duo NAT, TCP, UDP ve ıCMP 'yi destekler. IGMP desteklenmez.
- NetX Duo NAT, IPv6 adreslemesini desteklemez.
- NETX Duo NAT, bu hizmetleri NAT işlemleriyle tümleştirebilse de DNS veya DHCP hizmetleri içermez.

## <a name="rfcs-supported-by-netx-duo-nat"></a>NetX Duo NAT tarafından desteklenen RFC 'Ler

NetX Duo NAT uygulamasında, aşağıdaki RFC 'lerde sunulan bilgiler temel alınarak verilmiştir:

- RFC 2663: ıp ağ adresi Çeviri (NAT) terimleri ve konuları
- RFC 3022: geleneksel ıp netowrk Çeviri (geleneksel NAT)
- RFC 4787: Tek Noktaya Yayın UDP için Ağ Adresi Çevirisi (NAT) Davranış Gereksinimleri
