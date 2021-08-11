---
title: Bölüm 1 - NetX Duo Azure RTOS DHCPv6 sunucusuna giriş
description: Bu belgede NetX Duo DHCPv6 Sunucusunun DHCPv6 İstemcilerine IPv6 adreslerini nasıl atadığınız ayrıntılı olarak açıklanmaktadır.
author: philmea
ms.author: philmea
ms.date: 06/08/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 14a9d76731d949e3556a019756caf38b4ef440abfa4cfb927c47607e5712d9ac
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116783665"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-dhcpv6-server"></a>Bölüm 1 - NetX Duo Azure RTOS DHCPv6 sunucusuna giriş

IPv6 ağlarında, İstemcilerin IPv6 adreslerini elde etmek için DHCPv6is gerekir. IPv4 adresleri sunmayarak IPv4in ile sınırlı olan DHCP'nin yerini değiştirmez. DHCPv6, DHCP'ye benzer özelliklere ve birçok geliştirmeye sahiptir. IPv6 durum bilgisiz adres otomatik yapılandırması kullanmayan veya kullanamamış bir İstemci, DHCPv6 Sunucusundan benzersiz bir genel IPv6 adresi atanacak DHCPv6 kullanabilir.

NetX Duo, DHCPv6 gibi IPv6 ağ tabanlı uygulamaları ve ağ protokollerini desteklemek için geliştirilmiştir. Bu belgede NetX Duo DHCPv6 Sunucusunun DHCPv6 İstemcilerine IPv6 adreslerini nasıl atadığınız ayrıntılı olarak açıklanmaktadır.

## <a name="dhcpv6-communication"></a>DHCPv6 İletişimi

**DHCPv6 İleti yapısı**

İleti içeriği temelde bir veya daha fazla (genellikle daha fazla) seçenek bloğu tarafından takip edilen bir ileti üst bilgisidir. Her bloğun bir byte temsil ettiği temel yapı aşağıda verilmiştir:

![DHCPv6 ileti ve seçenek bloğu yapısını gösteren diyagram.](media/image2.jpg)

**Şekil 1. DHCPv6 iletisi ve seçenek bloğu yapısı**

1-byte Msg-Type alanı DHCPv6 iletisi türünü gösterir. 3-byte Transaction-ID alanı İstemci tarafından ayarlanır. Herhangi bir karakter dizisiyle olabilir, ancak sunucuya gönderilen her İstemci iletisi için benzersiz olmalıdır (İstemci tarafından gönderilen yinelenen iletiler arasında tutulmalıdır). Sunucu, istemcinin gecikmeli veya ağ üzerinde bırakılan paketler durumunda Sunucu iletileriyle eşleşmesini sağlamak için İstemciye her yanıt için bu İşlem Kimliği'nin kullanır. Transaction-ID alanını takip etmek, İstemcinin ne istediğini belirtmek için kullanılan bir veya daha fazla DHCPv6 seçeneğidir.

DHCPv6 seçenek yapısı bir seçenek kodu, uzunluk veya kod alanlarının yer almaması bir seçenek uzunluğu alanı ve son olarak istemcinin isteği veriler için bir veya daha fazla 2 bayt seçenek kodu alanı olan seçenek verilerinden oluşur.

Bazı seçenek bloklarının iç içe geçmiş seçenekleri vardır. Örneğin, Geçici Olmayan Adresler için Kimlik İlişkisi *(IANA)* seçeneği, IPv6 adresleri isteğinde kullanılan bir veya daha fazla Kimlik İlişkisi *(IA)* seçeneği içerir. Sunucu Yanıtı iletisinde döndürülen *IANA* seçeneği, Sunucu tarafından verilen IPv6 adresi ve kira süreleriyle aynı *IA* seçeneğinin yanı sıra İstemci adresi isteğinde hata olup olmadığını belirten bir Durum seçeneği içerir. 

Tüm seçenek bloklarının listesi ve açıklamaları Ek **A'da sağlanmıştır.**

**DHCPv6 İleti Türleri**

DHCPv6, DHCP işlevselliğini büyük ölçüde geliştirse de, DHCP ile aynı sayıda ileti kullanır ve DHCP ile aynı satıcı seçeneklerini destekler. DHCPv6 iletilerinin listesi aşağıdaki gibidir:

- SOLICT (1) (İstemci tarafından gönderilir)
- ADVERTISE (2) (Sunucu tarafından gönderilir)
- REQUEST (3) (İstemci tarafından gönderilir)
- REPLY (7) (Sunucu tarafından gönderilir)
- CONFIRM (4) (İstemci tarafından gönderilir)
- RENEW (5) (İstemci tarafından gönderilir)
- REBIND (6) (İstemci tarafından gönderilir)
- YAYıN (8) (İstemci tarafından gönderilir)
- REDDİk (9) (İstemci tarafından gönderilir)
- INFORM_REQUEST (11) (İstemci tarafından gönderilir)
- RECONFIGURE* (10) (Sunucu tarafından gönderilir)

*RECONFIGURE, NetX Duo DHCPv6 Sunucusu tarafından desteklenmiyor.

Parantez içinde eşdeğer DHCPv4 ileti türüne sahip temel DHCPv6 istek dizisi aşağıdaki gibidir:

İstemci ***İstek _**(_Discovery )*Sunucu **Tanıtım** (* Teklif *) İstemci **İsteği** (* İstek ) Sunucu ***Yanıtı** (* DHCPAck*)

İstemci **Yenileme**(aynı) Sunucu **Yanıtı** (*DHCPAck*)

## <a name="dhcpv6-message-validation"></a>DHCPv6 İleti Doğrulama

İşlem Kimliği: İstemcinin Sunucuya gönderdiği her ileti için bir işlem kimliği oluşturması gerekir. DHCPv6 Sunucusu İstemciden gelen ve bu işlem kimliğiyle eşleşmeen tüm iletiyi reddeder. Sunucu da istemciye yanıtlarında aynı işlem kimliğini kullan gerekir.

**DHCPv6 benzersiz Tanımlayıcıları (DUID)**

Tüm Sunucu iletileri ayrıca her iletiye bir DHCPv6 benzersiz Tanımlayıcı (DUID) içermeli veya DHCPv6 İstemcisi iletiyi kabul etmeyecektir. Bağlantı Katmanı (LL) DUID istemci MAC adresini, donanım türünü ve DUID türünü içeren bir denetim bloğu. Bağlantı Katmanı Süresi (LLT) DUID ayrıca konak ağın DUID'leri benzersiz olma şansını azaltan bir zaman alanı içerir. Bu nedenle RFC 3315 LL DUID'ler üzerinden LLT DUID'lerini önermektedir. Konak uygulama kendi benzersiz saat değerini oluşturmazsa, NetX Duo DHCPv6 varsayılan bir değer sağlar. ÜÇÜNCÜ TÜR DUID, kayıtlı bir Enterprise kimliği (IANA'ya kayıtlı gibi) ve bellek boyutuna, diğer donanım yapılandırmasının işletim sistemi türüne bağlı olarak tür ve uzunlukta değişken özel verileri içeren Enterprise (Satıcı tarafından atanan) DUID'dir. Sunucu satıcısı tarafından atanan ve özel kimlik değerlerinin ayar için bu belgenin başka bir yerindeki Yapılandırma Seçenekleri listesine bakın.

İstemcinin ayrıca, sunucuya iletilerine DUID'sini içermesi gerekir INFORM_REQUEST yoksa Sunucu bunları reddeder.

**DHCPv6 İstemci Sunucusu Oturumları**

DHCPv6 İstemcileri ve Sunucuları, UDP üzerinden ileti alışverişi yapıyor. İstemci, DHCPv6 iletilerini göndermek ve almak için bağlantı noktası 546'yı, Sunucu ise 547 bağlantı noktasını kullanır. İstemci başlangıçta DHCPv6 iletilerini ileterek almak için bağlantı yerel adresini kullanır. Tüm iletileri, *All_DHCP_Relay_Agents_and_Servers* çok noktaya yayın adresi *(FF02::01:02)* olarak bilinen ayrılmış, bağlantı kapsamlı çok noktaya yayın adresi kullanarak DHCPv6 sunucularına gönderir.

DHCPv6 Sunucusu, ip adresi atama istekleri için, bu adrese gönderilen *Solicit* *iletilerini All_DHCP_Relay_Agents_and_Servers* dinler. İstekte *İstemci,* belirli bir IPv6 adresinin ataması isteğinde bulunarak Sunucu'ya bir adres seçmesine izin ve sonra da izin verir. Ayrıca Sunucu'dan diğer ağ yapılandırma bilgilerini de talep edilebilir.

DHCPv6Server geçerli bir *Solicit* iletisi ayıklar ve İstemciye bir IPv6 adresi  atayasa, İstemciye ve IPv6 adresi kira süresine ve İstemci tarafından istenen ek bilgileri içeren bir IPv6 adresini içeren bir Tanıtma iletisiyle yanıt verir. İstemci Sunucu teklifini kabul ederse, Sunucu'ya IPv6 adresini kabul etmiş olduğunu haber veren bir İstek iletisiyle yanıt verir.  Sunucu, İstemcinin Bir Yanıt iletisiyle IPv6 adresine bağlı *olduğunu onaylar.*

İstemci DHCPv6 iletisi geçersizse, Sunucu iletiyi sessizce atar. Sunucu isteği veremiyorsa IP adresi IANA seçeneğinin durum alanında sorunun göstergesini gösteren bir Yanıt iletisi gönderir.  Yinelenen İstemci istekleri alındı ise, İstemcinin paketi almamıştır varsayılan Sunucu önceki DHCPv6 yanıtını yeniden gönderir.

Yinelenen Adres Algılama gibi çeşitli IPv6 protokollerini kullanarak Sunucudan atanan IPv6 adresinin sistem üzerinde başka bir ana bilgisayarla atanmamış olduğunu doğrulamak İstemciye bağlı olur. Adres benzersiz yoksa İstemci Sunucuya bir Reddetme *iletisi* gönderir. Sunucu, IP kiralama tablolarını bu bilgilerle güncelleştirir ve adresin zaten atanmış olduğunu kaydeder. Bu arada İstemcinin DHCPv6 istek işlemini başka bir İstek iletisiyle yeniden *başlatması* gerekir.

Bir IPv6 adresine ek olarak, bir İstemcinin DNS sunucusunu ve muhtemelen ağ etki alanı adı gibi diğer ağ bilgilerini de biliyor olması gerekir. DHCPv6, İstekte Bulun ve İstek iletisinde Seçenek İstekleri'nin  kullanımını kullanarak veya Bilgi İsteği iletileri'ne ayrı olarak bu bilgileri *talep etmek için bir kaynak* sağlar.  DHCPv6 seçenekleri bu bölümün ilerleyen kısımlarında açıklanmıştır.

**IPv6 Kira Süresi**

Sunucu bir İstemciye bir IPv6 adresi vererek, İstemcinin İletileri Yenile ve Yeniden Bağlama kullanarak IPv6 adresini yenilemeye (T1) veya yeniden bağlamaya (T2) başlamasını önerip IANA seçeneğinde kiralama süresini (yaşam süresi) atar.   İkisi arasındaki fark, İstemcinin Yenile isteğine Sunucu DUID'sini dahil etmek için Sunucuyu Yenile iletiyi *yönlendirmiş olduğudur.*  Ancak, herhangi bir sunucu belirtmez ve bu nedenle *Rebind* iletisinde bir Sunucu DUID'i *All_DHCP_Relay_Agents_and_Servers* içerir. Sunucu'ya verilen gerçek IPv6 adresini içeren IA seçeneği, kiralanan IPv6 adresi kullanım dışı veya kullanımdan kaldırılmış (geçersiz) olduğunda tercih edilen ve geçerli yaşam sürelerini de içerir.

NetX Duo DHCPv6 Sunucusu, her İstemcinin İstemci iletileri arasındaki zamanı izlemesi için bir oturum zaman aşımına sahip olur. Bu, bir İstemci ana bilgisayarının bağlantının kaybedilsi veya ağ kapatıyor durumunda gereklidir. Oturum zaman aşımının süresi dolduğunda İstemcinin artık ilgilenmey olduğu veya Sunucudan DHCPv6 istekleri ala olmadığı varsayılır. Sunucu İstemci kaydını siler ve geçici olarak atanmış tüm IPv6 adreslerini kullanılabilir havuza geri döndürür. Oturum zaman aşımı beklemesi, kullanıcı tarafından yapılandırılabilir bir seçenektir.

İstemci, IPv6 adresini serbest bırakmak isterse veya DHCPv6 Sunucusu tarafından atanmış olan IPv6 adresinin zaten kullanımda  olduğunu  keşfederse, sırasıyla bir Yayın veya Reddetme iletisi gönderir. Bir Yayın iletisi *durumunda,* Sunucu bu IPv6 adresi durumunu kullanılabilir havuza geri döndürür. Reddetme iletisi durumunda, *ip* kirası tablosu, bu IPv6 adresinin kullanılabilir olmadığını (ağ üzerinde başka bir varlığa ait) göstermek için güncelleştirir.

**IPv6 Kira ve İstemci Kayıt Verileri**

DHCPv6 Sunucusu İstemci isteklerini kabul etmeye başladığında, IPv6 adresleri isteyen veya atanmış olan etkin İstemcilerin listesini sürdürür. Sunucu, İstemci kira süresini düzenli aralıklarla güncelleen bir kira süreölçeri ile IP kirası süre sonu denetler. Süre geçerli yaşam süresini aşarsa, Sunucu İstemci kaydını temizler ve IPv6 adresini kullanılabilir havuza geri döndürür. Bu olmadan önce yenileme/yeniden bağlama işleminin başlaması İstemciye kaldı!

NetX Duo DHCPv6 Server istemci kayıt tablosu, İstemcileri tanımlamaya yönelik bilgiler ve DHCPv6 İstemci isteklerini doğrulama ve IPv6 adreslerini atama veya yeniden atamaya yönelik 'durum' bilgilerini içerir. Bu tür bilgiler şunları içerir:

- Bir ağ üzerinde her İstemci ana bilgisayarsını benzersiz olarak tanımlayan İstemci DHCPv6 Benzersiz Tanımlayıcısı (DUID). İstemcinin tüm DHCPv6 iletileri için her zaman aynı DUID'i kullanması gerekir.

- İstemci IPv6 adres atama parametrelerini tanımlayan, toplu olarak Geçici Olmayan Adresler (IANA) ve Kimlik İlişkisi IPv6 adresi (IA) için İstemci Kimliği İlişkisi.

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

Sunucu DUıD, ağda DHCPv6 sunucu konağını benzersiz şekilde tanımlar. Bir sunucu, DUıD 'sini daha önce oluşturmadıysa, *nx_dhcpv6_server_set_duid* oluşturmak için kullanabilir. RFC 3315 ' den itibaren, sunucu yeniden başlatıldıktan sonra alabilmesi için DHCPv6 sunucusunun bu DUıD 'yi kalıcı belleğe kaydetmesi gerekir. DHCPv6 sunucusu bağlantı katmanını, bağlantı katmanı saatini ve Enterprise (satıcının atandığı) duıd türlerini destekler. Istemcinin doğrudan DUıD satıcı türünde gönderilmesi gerektiğini unutmayın. Satıcı türü Duıds (17) seçeneği, NetX Duo DHPv6 sunucusu tarafından doğrudan desteklenmez.

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

DHCPv6 İstemcisi bir Reddetme iletisi gönderdiğinde, NetX Duo DHCPv6 Sunucusu adresi IPv6 adres tablolarında mevcut değil olarak işaretler. Bu iletinin Sunucu işlemesini özelleştirme yeteneğine sahip olmak *için nx_dhcpv6_IP_address_declined_handler* *sağlanır.* Ancak, bu geri çağırma şu anda uygulanmaz.

*nx_dhcpv6_server_option_request_handler*

DHCPv6 İstemcisi iletisi seçenek isteği verileri içerdiğinde, NetX Duo DHCPv6 Sunucusu her seçenek isteği seçenek kodunu tanımlansa bu kullanıcı geri çağırmaya iletir. Bu, NetX Duo Server'a kullanıcı tanımlı geri çağırmanın verileri doldurmasına izin verme yeteneği verir. Ancak bu işlevsellik şu anda uygulanmaz.

## <a name="supported-dhcpv6-rfcs"></a>Desteklenen DHCPv6 RFC'ler

NetX Duo DHCPv6 RFC3315, RFC3646 ve ilgili RFC'ler ile uyumludur.