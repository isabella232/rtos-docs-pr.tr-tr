---
title: Bölüm 1-Azure RTOS NetX Duo DHCPv6 sunucusuna giriş
description: Bu belgede NetX Duo DHCPv6 sunucusunun, DHCPv6 Istemcilerine IPv6 adresleri nasıl atayacağı ayrıntılı olarak açıklanmaktadır.
author: philmea
ms.author: philmea
ms.date: 06/08/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 6cf7baa91b1804876b97b1d75d1872d1120ad028
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826044"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-dhcpv6-server"></a>Bölüm 1-Azure RTOS NetX Duo DHCPv6 sunucusuna giriş

IPv6 ağlarında, DHCPv6is Istemcilerinin IPv6 adreslerini alması gerekir. IPv4 adresi sunmadığından, IPv4in ile sınırlı olan DHCP 'yi değiştirmez. DHCPv6, DHCP ve birçok geliştirmelere benzer özelliklere sahiptir. IPv6 durum bilgisi olmayan adres otomatik yapılandırması olmayan veya kullanmayan bir Istemci, DHCPv6 sunucusundan benzersiz bir genel IPv6 adresi atamak için DHCPv6 kullanabilir.

NetX Duo, IPv6 ağ tabanlı uygulamaları ve DHCPv6 gibi ağ protokollerini destekleyecek şekilde geliştirilmiştir. Bu belgede NetX Duo DHCPv6 sunucusunun, DHCPv6 Istemcilerine IPv6 adresleri nasıl atayacağı ayrıntılı olarak açıklanmaktadır.

## <a name="dhcpv6-communication"></a>DHCPv6 Iletişimi

**DHCPv6 Ileti yapısı**

İleti içeriği temelde bir ileti üst bilgisi ve ardından bir veya daha fazla (genellikle daha fazla) seçenek bloğu gelir. Aşağıda, her bloğun bir baytı temsil ettiği temel yapı yer verilmiştir:

![DHCPv6 iletisini ve seçenek blok yapısını gösteren diyagram.](media/image2.jpg)

**Şekil 1. DHCPv6 iletisi ve seçenek blok yapısı**

1 baytlık Msg-Type alanı, DHCPv6 iletisi türünü gösterir. 3 baytlık Işlem KIMLIĞI alanı Istemci tarafından ayarlanır. Herhangi bir karakter dizisi olabilir, ancak sunucuya her Istemci iletisi için benzersiz olmalıdır (Istemci tarafından gönderilen yinelenen iletiler arasında sunulur). Sunucu, istemcinin geciktirilen veya ağda bırakılan paketlerin durumunda sunucu iletilerini eşleşmesini sağlamak için Istemciye her bir yanıt için bu Işlem KIMLIĞINI kullanır. Işlem KIMLIĞI alanını takip eden bir veya daha fazla DHCPv6 seçeneği, Istemcinin ne istediğini göstermek için kullanılır.

DHCPv6 seçenek yapısı, bir seçenek kodundan oluşur, uzunluk veya kod alanlarını içermeyen bir seçenek uzunluğu alanıdır ve son olarak, Istemcinin istediği veriler için bir veya daha fazla 2 baytlık seçenek kodu alanı olan seçenek verileri.

Bazı seçenek blokları iç içe seçeneklere sahiptir. Örneğin, *geçici olmayan adres (IANA) seçeneği için bir kimlik ilişkilendirmesi* , IPv6 adresleri istemek için bir veya daha fazla *KIMLIK ilişkilendirmesi (IA)* seçeneği içerir. Sunucu yanıt iletisinde döndürülen *IANA* seçeneği, sunucu tarafından verilen IPv6 adresi ve kira süreleriyle aynı *IA* seçeneğini ve istemci adresi isteğinde bir hata olup olmadığını belirten bir *durum* seçeneğini içerir.

Tüm seçenek bloklarının listesi ve açıklamaları **Ek A**' da verilmiştir.

**DHCPv6 Ileti türleri**

DHCPv6, DHCP işlevlerini önemli ölçüde iyileştirse de DHCP ile aynı sayıda ileti kullanır ve DHCP ile aynı satıcı seçeneklerini destekler. DHCPv6 iletilerinin listesi aşağıdaki gibidir:

- ISTEME (1) (Istemci tarafından gönderilen)
- TANıTMA (2) (sunucu tarafından gönderilen)
- Istek (3) (Istemci tarafından gönderilen)
- Yanıt (7) (sunucu tarafından gönderilen)
- Onayla (4) (Istemci tarafından gönderilen)
- YENILE (5) (Istemci tarafından gönderilen)
- Yeniden bağlama (6) (Istemci tarafından gönderilen)
- Yayın (8) (Istemci tarafından gönderilen)
- Reddet (9) (Istemci tarafından gönderilen)
- INFORM_REQUEST (11) (Istemci tarafından gönderilen)
- YENIDEN YAPıLANDıR * (10) (sunucu tarafından gönderilen)

* YENIDEN yapılandırın NetX Duo DHCPv6 sunucusu tarafından desteklenmez.

Parantez içinde eşdeğer DHCPv4 ileti türü ile temel DHCPv6 istek sırası aşağıdaki gibidir:

İstemci ***istem** _ (_Discovery *) sunucu **tanıtımı** (* teklif *) istemci **isteği** (* istek *) sunucu **yanıtı** (* DHCPACK *)

İstemci **yenileme**(aynı) sunucu **yanıtı** (*DHCPACK*)

## <a name="dhcpv6-message-validation"></a>DHCPv6 Ileti doğrulaması

İşlem KIMLIĞI: Istemci, sunucusuna gönderdiği her ileti için bir işlem KIMLIĞI üretmelidir. DHCPv6 sunucusu, bu işlem KIMLIĞIYLE eşleşmeyen Istemciden gelen tüm iletileri reddeder. Sırasıyla sunucu, yanıtlarındaki aynı işlem KIMLIĞINI Istemciye geri kullanmalıdır.

**DHCPv6 benzersiz tanımlayıcıları (Duıds)**

Tüm sunucu iletileri Ayrıca her iletiye DHCPv6 benzersiz tanımlayıcısını (DUıD) içermelidir veya DHCPv6 Istemcisinin iletiyi kabul etmemelidir. Bağlantı Katmanı (LL) DUıD, istemci MAC adresini, donanım türünü ve DUıD türünü içeren bir denetim bloğudur. Bir bağlantı katmanı saati (LLT) DUıD ek olarak, DUıD 'nin konak ağı üzerinde benzersiz olmaması ihtimalini azaltan bir zaman alanı içerir. Bu nedenle, RFC 3315, LL Duıds üzerinden LLT Duıds önerir. Ana bilgisayar uygulaması kendi benzersiz zaman değerini oluşturmadıysanız NetX Duo DHCPv6 varsayılan bir değer sağlar. Üçüncü DUıD türü, kayıtlı bir kurumsal KIMLIĞI (ıANA ile kayıtlı olduğu gibi) ve tür ve uzunluktadır olan özel verileri (örneğin, bellek boyutu, diğer donanım yapılandırması işletim sistemi türü) içeren bir kurumsal (satıcı tarafından atanan) DUıD türüdür. Sunucu satıcısı atanmış ve özel KIMLIK değerlerini ayarlamak için bu belgede başka bir yerde yapılandırma seçenekleri listesine bakın.

Istemci Ayrıca, INFORM_REQUEST hariç olmak üzere, içindeki DUıD 'sini sunucusuna da dahil etmelidir, aksi durumda sunucu bunları reddeder.

**DHCPv6 Istemci sunucusu oturumları**

DHCPv6 Istemcileri ve sunucuları UDP üzerinden iletiler değiş tokuş. Istemci, DHCPv6 iletilerini göndermek ve almak için 546 bağlantı noktasını kullanır ve sunucu 547 bağlantı noktasını kullanır. Istemci başlangıçta, DHCPv6 iletilerini iletmek ve almak için bağlantı yerel adresini kullanır. *All_DHCP_Relay_Agents_and_Servers* çok noktaya yayın adresi *(FF02:: 01:02)* olarak bilinen ayrılmış, bağlantı kapsamlı çok noktaya yayın adresini kullanarak tüm iletileri DHCPv6 sunucusuna gönderir.

ForIPv6 adres atama istekleri, DHCPv6 sunucusu *All_DHCP_Relay_Agents_and_Servers* adresine gönderilen *istem* iletilerini dinler. *İstek Isteğinde istemci* , belirli bir IPv6 adresi atamasını Isteyebilir veya sunucunun bir tane seçmesini sağlayabilir. Ayrıca, sunucudan diğer ağ yapılandırma bilgilerini de isteyebilir.

DHCPv6Server geçerli bir *istem* iletisini ayıklar ve Istemciye bir IPv6 adresi atayabiliyorsanız, Istemciye vereceğiniz IPv6 adresini, IPv6 adresi kiralama süresini ve istemci tarafından istenen ek bilgileri Içeren bir *tanıtım* iletisi ile yanıt verir. Istemci sunucuyu kabul ederse, sunucunun IPv6 adresini kabul edeceğini bildiren bir *istek* iletisiyle yanıt vermesini sağlar. Sunucu, Istemcinin bir *Yanıt* iletisiyle IPv6 adresine bağlandığını onaylar.

Istemci DHCPv6 iletisi geçersizse, sunucu iletiyi sessizce atar. Sunucu isteği vermezse, IP adresi ıANA seçeneğinin durum alanındaki sorunu belirten bir *Yanıt* iletisi gönderir. Yinelenen Istemci istekleri alınmışsa, sunucu önceki DHCPv6 yanıtını yeniden sonlandırır ve Istemcinin yalnızca paketi almadığını kabul etmez.

Yinelenen adres algılama gibi çeşitli IPv6 protokollerini kullanarak, sunucudan atanan IPv6 adresinin, sistemdeki başka bir konağa atanmadığını doğrulamak Istemciye bağlıdır. Adres benzersiz değilse, Istemci sunucuya bir *Red* iletisi gönderir. Sunucu, IP Kiralama tablosunu bu bilgilerle güncelleştirir, bu, adresin zaten atandığı kayda kaydedilir. Istemcinin DHCPv6 istek işlemini başka bir *istem* iletisiyle yeniden başlatması gerekir.

Bir IPv6 adresine ek olarak, bir Istemcinin DNS sunucusunu ve ağ etki alanı adı gibi diğer ağ bilgilerini de bilmeleri gerekir. DHCPv6, bu bilgileri istek ve *istek* *Iletilerinde bulunan seçenek* Isteklerinin kullanımını veya *bilgi isteği* iletilerinde ayrı olarak kullanmayı istemek için bir yol sağlar. DHCPv6 seçenekleri bu bölümün ilerleyen kısımlarında açıklanmıştır.

**IPv6 kira süresi**

Sunucu bir Istemciye bir IPv6 adresi verdiğinde, Istemci, *yenileme* ve yeniden *bağlanma* iletilerini kullanarak (T1) veya yeniden bağlama (T2) ile ilgili IPv6 adresini yenilemeye başlamasını ÖNERDIĞINDEN, için IANA seçeneğine (ömür) kira süresini de atar. İki arasındaki fark, Istemci, *yenileme Isteğine sunucu* DUID ekleyerek *yenileme* iletisini sunucusuna yönlendirir. Ancak, herhangi bir sunucu belirtmez ve bu nedenle, *All_DHCP_Relay_Agents_and_Servers* adresine yeniden *bağlama* iletisinde bir sunucu DUID içermez. Sunucunun verdiği gerçek IPv6 adresini içeren IA seçeneği, Ayrıca, kiralanan IPv6 adresi sırasıyla kullanım dışı veya eski (geçersiz) duruma geldiğinde, Istemcinin tercih edilen ve geçerli yaşam sürelerini de içermesi gerekir.

NetX Duo DHCPv6 sunucusu, Istemci iletileri arasındaki süreyi izlemek için her Istemci için bir oturum zaman aşımı süresi tutar. Bu, bağlantıyı kaybetmekte olan bir Istemci Konağı durumunda gereklidir. Oturum zaman aşımı süresi dolduğunda, Istemcinin artık ilgilenmiyor veya sunucu için DHCPv6 isteklerini yapabilmemesi varsayılır. Sunucu, Istemci kaydını siler ve kullanılabilir havuza herhangi bir kesin olmayan şekilde atanan IPv6 adresini geri döndürür. Oturum zaman aşımı süresi, Kullanıcı tarafından yapılandırılabilir bir seçenektir.

Istemci, IPv6 adresini serbest bırakabilir veya DHCPv6 sunucusu tarafından kendisine atanan IPv6 adresinin zaten kullanımda olduğunu belirlerse, sırasıyla bir *yayın* veya *reddetme* iletisi gönderir. Bir *Sürüm* Iletisinde, sunucu IPv6 adres durumunu kullanılabilir havuza geri döndürür. *Reddetme* iletisinde, bu IPv6 adresinin kullanılabilir olmadığını BELIRTMEK için IP Kiralama tablosunu güncelleştirir (ağ üzerinde başka bir varlık tarafından sahiplenilir).

**IPv6 kiralama ve Istemci kaydı verileri**

DHCPv6 sunucusu Istemci isteklerini kabul etmeye başladığında, IPv6 adresi isteyen veya atanmış etkin Istemcilerin bir listesini tutar. Sunucu, Istemci kira süresini düzenli olarak güncelleştiren bir kira süreölçeri aracılığıyla IP kira süre sonunu denetler. Süre geçerli yaşam süresini aştığında sunucu, Istemci kaydını siler ve IPv6 adresini kullanılabilir havuza geri döndürür. Bu işlem yapılmadan önce yenileme/yeniden bağlama işlemini başlatmak Istemciye kadar olur!

NetX Duo DHCPv6 sunucusu istemci kaydı tablosu, Istemcileri tanımlamak için bilgiler ve DHCPv6 Istemci isteklerini doğrulamak ve IPv6 adreslerini atamak veya yeniden atamak için ' durum ' bilgilerini içerir. Bu tür bilgiler şunları içerir:

- Bir ağ üzerinde her bir Istemci konağını benzersiz bir şekilde tanımlayan Istemci DHCPv6 benzersiz tanımlayıcısı (DUıD). Istemci her zaman aynı DUıD 'yi tüm DHCPv6 iletileri için kullanmalıdır.

- Geçici olmayan adresler (ıANA) ve kimlik Ilişkilendirmesi IPv6 adresi (IA) için Istemci kimliği Ilişkilendirmesi, Istemci IPv6 adresi atama parametrelerini tanımlayan bir üst üste.

- İstemci seçeneği istekleri (DNS sunucusu, etki alanı adı vb.).

- En son DHCPv6 isteğinin Istemci IPv6 kaynak adresi (ayarlandıysa) ve hedef adresi (çok noktaya yayın yoksa).

- Istemcinin en son ileti türü ve DHCPv6 ' State '.

## <a name="netx-duo-dhcpv6-server-requirements-and-constraints"></a>NetX Duo DHCPv6 sunucu gereksinimleri ve kısıtlamaları

NetX Duo DHCPv6 sunucu API 'SI, ThreadX 5,1 veya üzeri ve NetX Duo 5,5 veya üstünü gerektirir.

**Gereksinimler**

***IP Iş parçacığı görev kurulumu***

NetX Duo DHCPv6 sunucusu, ağ bağlantısı üzerinde DHCPv6 'ye ileti göndermek ve almak için bir IP örneği oluşturulmasını gerektirir. Bu, *nx_ip_create* hizmeti kullanılarak yapılır. NetX Duo DHCPv6 sunucusunun oluşturulması gerekir. Bu, *nx_dhcpv6_server_create* hizmeti kullanılarak yapılır.

DHCPv6 NetX Duo, ICMPv6 ve UDP kullanır. Bu nedenle, aşağıdaki NetX Duo hizmetlerini çağırarak önce IPv6 'nın DHCPv6 sunucusu kullanılmadan önce etkinleştirilmesi gerekir:

- *nx_udp_enable*
- *nxd_ipv6_enable*
- *nxd_icmp_enable*

Daha da, DHCPv6 sunucusu başlatılmadan önce gerçekleştirilecek bir dizi ayarlama görevi vardır:

- Bağlantı yerel ve IPv6 genel adreslerini oluşturun ve doğrulayın. Adres doğrulama etkinleştirilirse, NetX Duo tarafından otomatik olarak gerçekleştirilir ve yinelenen adres algılama özelliği kullanılır. Bağlantı yerel ve genel IP adresi doğrulama hakkında ayrıntılı bilgi için bkz. *NETX Duo Kullanıcı el kitabı* .

- Ağ arabirimi dizinini, DHCPv6 arabirimi için ayarlayın.

- Atanabilir IPv6 adresleri için bir IP adresi aralığı oluşturun. Ya da önceki bir sunucu DHCPv6 oturumunda veriler varsa, bu oturumdaki IPv6 Kiralama tablosu ve istemci kayıtları, geçici olmayan bellekten DHCPv6 sunucusuna yüklenmelidir. Bu belgede başka bir yerde küçük örnek sistem, bu gereksinimi karşılamak için DHCPv6 sunucu hizmetlerini gösterir.

- Sunucu DUıD 'sini ayarlayın. Sunucu, bir önceki oturumda DUıD oluşturmışsa, Istemcilerine iletiler için aynı DUıD 'yi oluşturmak üzere aynı verileri kullanması gerekir. Bu belgede başka bir yerde küçük örnek sistem bu gereksinimin nasıl yapıldığını gösterir.

Bu noktada, DHCPv6 sunucusu çalıştırılmaya hazırdır. NetX Duo DHCPv6 sunucusu, 547 numaralı bağlantı noktasına bağlanacak bir UDP yuvası oluşturacak ve Istemci isteklerini dinlemeye başlayacaktır.

***Paket havuzu gereksinimleri***

NetX Duo DHCPv6 sunucusu, DHCPv6 iletilerini göndermek için bir paket havuzu gerektirir. Paket yükü ve kullanılabilir paket sayısı bakımından paket havuzunun boyutu Kullanıcı tarafından yapılandırılabilir ve bu, ana bilgisayar uygulamasının gönderilmesi için beklenen DHCPv6 iletilerinin ve diğer aktarımların hacmine bağlıdır.

Tipik bir DHCPv6 iletisi, Istemci tarafından istenen ek seçenekler sayısına ve sunucudan kullanılabilir bilgilere bağlı olarak 200-300 bayttır.

***DHCPv6 sunucu arabirimini ayarlama***

DHCPv6 sunucusu, üzerinde Istemci isteklerini kabul edeceği arabirim olarak birincil ağ arabirimini varsayılan olarak belirler. Ancak, ana bilgisayar uygulamasının sunucu genel adresini oluşturmak için kullandığı genel adres dizinini hala ayarlaması gerekir. DHCPv6 arabirim dizini ve genel adres dizini *nx_dhcpv6_server_interface_set* hizmeti kullanılarak ayarlanır. Bu belgede "küçük örnek" de gösterilmiştir.

***Sunucu yeniden başlatıldığında DHCPv6 DUıD kaydetme***

DHCPv6 protokolü, sunucunun birden çok yeniden başlatıldığında aynı DUıD kullanmasını gerektirir. Bu nedenle, DUıD 'yi oluşturmak için kullanılan tüm verilerin bu gereksinim için kalıcı bellekten depolanması ve alınması gerekir. Bağlantı katmanını kullanan konaklar için ve gerçek zamanlı saate erişim gerektiren zaman DUıD. NetX Duo DHCPv6 ana bilgisayar uygulaması, ilk sunucu DUıD oluşturma için bir zaman değeri oluşturmak üzere gerçek zamanlı veri erişimi içermelidir ve bu verileri sonraki sunucu oturumlarında yeniden kullanmak üzere depolar. *Nx_dhcpv6_set_server_duid* daha sonra, DUID verilerini bağımsız değişken olarak alır, ayrıca DUID türüne bağlı yapılandırma seçenekleri de kendı DUID oluşturmak için (veya yeniden üretmek üzere).

***Atanabilir IPv6 adres listesi oluşturma***

Daha önce depolanan IP adresi listesi verileri yoksa, DHCPv6 sunucusu oluşturulduktan sonra sunucu ana bilgisayar uygulamasının bir atanabilir IPv6 genel adresi aralığı oluşturması gerekir. Bu, başlangıç ve bitiş IPv6 adresini giriş olarak alan *nx_dhcpv6_create_ip_address_range* hizmeti kullanılarak yapılır.

***DHCPv6 atanabilir adresi ve Istemci verileri kaydediliyor***

DHCPv6 protokolü, DHCPv6 sunucusunun Istemci ve IPv6 adres verilerini, sunucuyu yeniden başlatma durumunda kalıcı depolamada kaydetmesini gerektirir. NetX Duo DHCPv6 sunucusunda, Istemci ve IPv6 adres verilerini, sırasıyla DHCPv6 sunucusuna yüklemek ve indirmek için çeşitli API 'ler vardır:

*nx_dhcpv6_add_client_record*

*nx_dhcpv6_add_ip_address_lease*

*nx_dhcpv6_retrieve_client_record*

*nx_dhcpv6_retrieve_ip_address_lease*

Sunucu yeniden başlatılmadan önce sunucuya verilerin yüklenmesi yapılmalıdır. Verilerin indirilmesi, yalnızca DHCPv6 sunucusu durdurulduktan sonra (veya askıya alındıktan sonra) yapılmalıdır. Bunu yapmaya yönelik hizmetler bu belgenin ilerleyen kısımlarında ayrıntılı olarak açıklanmıştır. Ancak NetX Duo DHCPv6, kalıcı depolamaya bir erişim tanımlamaz. Bu, ana bilgisayar uygulaması tarafından işlenmelidir. Küçük örnek, ana bilgisayar uygulamasının bunu nasıl kullandığını gösterir.

***Sunucu DHCP benzersiz tanımlayıcısı (DUıD)***

Sunucu DUıD, ağda DHCPv6 sunucu konağını benzersiz şekilde tanımlar. Bir sunucu, DUıD 'sini daha önce oluşturmadıysa, *nx_dhcpv6_server_set_duid* oluşturmak için kullanabilir. RFC 3315 ' den itibaren, sunucu yeniden başlatıldıktan sonra alabilmesi için DHCPv6 sunucusunun bu DUıD 'yi kalıcı belleğe kaydetmesi gerekir. DHCPv6 sunucusu bağlantı katmanını, bağlantı katmanı süresini ve kurumsal (satıcı atanmış) DUıD türlerini destekler. Istemcinin doğrudan DUıD satıcı türünde gönderilmesi gerektiğini unutmayın. Satıcı türü Duıds (17) seçeneği, NetX Duo DHPv6 sunucusu tarafından doğrudan desteklenmez.

DHCPv6 sunucusu konak uygulamasının, kira zaman aşımı dahil olmak üzere IPv6 adres ataması için varsayılan değerleri vardır. Bu seçenekleri nasıl ayarlayabilmek için bu belgede daha sonra yapılandırılabilir seçeneklere bakın. :

*IANA* denetim bloğu, T1 ve T2 alanlarını içerir. *IANA* denetim bloğundaki *IA* bloğu tercih edilen ve geçerli ömür alanlarını içerir. Konak uygulama, bu belgenin başka bir yerinde tanımlanmış yapılandırılabilir seçeneklere sahiptir ve bu seçenekleri ayarlar. Bunlar tüm Istemci IPv6 adresi isteklerine atanır.

Bu DHCPv6 IP Kiralama parametreleri aşağıda tanımlanmıştır.

T1 – Istemcinin IPv6 adresini kendisine atayan sunucudan yenilemeyi başlatması gereken saniye cinsinden süre.

T2: yenileme başarısız olursa, Istemcinin bağlantısı üzerindeki herhangi bir sunucuyla IPv6 adresini yeniden bağlamayı başlatması gereken saniye cinsinden süre.

Tercih edilen ömür: Istemci yenilenmez veya yeniden bağlanmazsa Istemci adresinin kullanım dışı hale geldiği saniye cinsinden süre. Istemci bu adresi kullanmaya devam edebilir.

Geçerli ömür: Istemci IP adresinin süresi dolduğunda ve ağ iletimlerinin bu adresi kullanması gereken süre (saniye cinsinden).

RFC, Istemci *IANA* seçeneğinde tercih edilen yaşam süresi sırasıyla 0,5 ve 0,8 olan T1 ve T2 sürelerini önerir. Sunucuda tercih yoksa, bu zamanları sıfıra ayarlaması gerekir. Bir sunucu yanıtı, T1 ve T2 zamanları içeriyorsa, Istemcinin kendi T1 ve T2 sürelerini belirlemesine izin verir.

**Kısıtlamalar**

NetX Duo DHCPv6 sunucusu, aşağıdaki DHCPv6 seçeneklerini desteklemez:

  - Yalnızca Istek ve yanıt iletisi değişimi için DHCPv6 adresi istek işlemini iyileştiren hızlı Işleme seçeneği

  - Sunucunun Istemcinin IP adresi durumunda değişiklik başlatabilmesine izin veren seçeneği yeniden yapılandırın.

  - Tek noktaya yayın seçeneği; Tüm Istemci iletileri doğrudan DHCPv6 sunucusu yerine *All_DHCP_Relay_Agents_and_Servers* çok noktaya yayın adresine gönderilmelidir.

  - Bir Istemciye verilen geçici bir IP adresi olan geçici adresler (IA_TA) seçeneği için kimlik Ilişkilendirmesi.

  - Istemci Isteği başına birden çok IA (IPv6 adresi) seçeneği

  - DHCPv6 Istemcisi ile sunucu gibi geçiş ana bilgisayarı, Istemci ve sunucu aynı ağda olmalıdır.

  - IPSec ve kimlik doğrulaması, DHCPv6 mesajlaşmada desteklenmez. Ancak, IP örneği kullanımda olan NetX Duo sürümüne bağlı olarak IPSec etkin olabilir.

  - NetX Duo DHCPv6 sunucusu, yalnızca DNS sunucusu seçenek isteğini doğrudan destekler. Bu, gelecek sürümlerde değişebilir.

  - Ön ek temsili seçeneği desteklenmez.

  - Temel alınan NetX Duo ortamında IPSec etkinleştiribilse de DHCPv6 iletilerinin kimlik doğrulaması. Her ikisi de NetX Duo DHCPv6 sunucusu Istemcilere geçiş bağlantılarını desteklemez. Tüm Istemci isteklerinin sunucu ağındaki konaklardan kaynaklanan varsayılmaktadır.

## <a name="netx-duo-dhcpv6-server-callback-functions"></a>NetX Duo DHCPv6 sunucusu geri çağırma Işlevleri

*nx_dhcpv6_IP_address_declined_handler*

DHCPv6 Istemcisi bir reddetme iletisi gönderdiğinde, NetX Duo DHCPv6 sunucusu adresi IPv6 adres tablolarında kullanılamıyor olarak işaretler. Bu iletinin sunucu işlemesini özelleştirmek için *nx_dhcpv6_IP_address_declined_handler* sağlanır *.* Ancak, bu geri arama şu anda uygulanmadı.

*nx_dhcpv6_server_option_request_handler*

DHCPv6 Istemci iletisi seçenek isteği verileri içerdiğinde, NetX Duo DHCPv6 sunucusu her bir seçenek isteği seçenek kodunu, tanımlanmışsa bu kullanıcı geri çağırması için iletir. Bu, NetX Duo sunucusuna, Kullanıcı tanımlı geri aramanın verileri doldurmasını sağlar. Ancak bu işlev şu anda uygulanmıyor.

## <a name="supported-dhcpv6-rfcs"></a>Desteklenen DHCPv6 RFC 'Leri

NetX Duo DHCPv6, RFC3315, RFC3646 ve ilgili RFC 'lerle uyumludur.