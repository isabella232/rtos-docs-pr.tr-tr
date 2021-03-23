---
title: Bölüm 1-Azure RTOS NetX Duo DNS Istemcisine giriş
description: DNS, etki alanı adlarıyla fiziksel IP adresleri arasında eşleme içeren dağıtılmış bir veritabanı sağlar.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 4c07d6e3183d421c637874dcdeff3767554fca78
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826026"
---
# <a name="chapter-1---introduction-to-the-azure-rtos-netx-duo-dns-client"></a>Bölüm 1-Azure RTOS NetX Duo DNS Istemcisine giriş

DNS, etki alanı adlarıyla fiziksel IP adresleri arasında eşleme içeren dağıtılmış bir veritabanı sağlar. Tüm eşlemeyi içeren Internet 'te tek bir varlık bulunmadığından, veritabanı *dağıtıldı* olarak adlandırılır. Eşlemenin bir kısmını tutan bir varlığa, DNS sunucusu denir. Internet, her biri bir veritabanının alt kümesini içeren çok sayıda DNS sunucusundan oluşur. DNS sunucuları, etki alanı adı eşleme bilgileri için DNS Istemci isteklerini de yalnızca sunucuda istenen eşleme varsa yanıtlar.

NetX Duo için DNS Istemci protokolü, uygulamayı bir veya daha fazla DNS sunucusundan eşleme bilgilerini istemek üzere hizmetlerle birlikte sağlar.

## <a name="dns-client-setup"></a>DNS Istemcisi kurulumu

Düzgün çalışması için, DNS Istemci paketi bir NetX Duo IP örneğinin zaten oluşturulmuş olmasını gerektirir.

DNS Istemcisini oluşturduktan sonra, uygulamanın DNS Istemcisi tarafından tutulan sunucu listesine bir veya daha fazla DNS sunucusu eklemesi gerekir. Uygulama, DNS sunucuları eklemek için *nxd_dns_server_add* hizmetini kullanır. NetX Duo DNS Istemci hizmeti *nx_dns_server_add* sunucu eklemek için de kullanılabilir. Ancak yalnızca IPv4 adreslerini kabul eder ve geliştiricilerin bunun yerine *nxd_dns_server_add* hizmetini kullanması önerilir.

NX_DNS_IP_GATEWAY_SERVER seçeneği etkinse ve IP örneği ağ geçidi adresi sıfır değilse, IP örneği ağ geçidi, birincil DNS sunucusu olarak otomatik olarak eklenir. DNS sunucusu bilgileri statik olarak bilinmiyorsa, NetX Duo için dinamik ana bilgisayar Yapılandırma Protokolü (DHCP) üzerinden de türetilebilir. Daha fazla bilgi için lütfen NetX Duo DHCP Kullanıcı kılavuzuna bakın.

DNS Istemcisi, DNS iletilerini iletmek için bir paket havuzu gerektirir. Varsayılan olarak, *nx_dns_create* HIZMETI çağrıldığında DNS istemcisi bu paket havuzunu oluşturur. Yapılandırma seçenekleri NX_DNS_PACKET_PAYLOAD_UNALIGNED ve NX_DNS_PACKET_POOL_SIZE uygulamanın, bu paket havuzunun paket yükünü ve paket havuzu boyutunu (ör. paket sayısı) belirlemesine izin verir. Bu seçenekler, Bölüm Iki kısmında "yapılandırma seçenekleri" bölümünde açıklanmaktadır.

Kendi paket havuzunu oluşturan DNS Istemcisinin bir alternatifi, uygulamanın paket havuzunu oluşturması ve bu hizmeti *nx_dns_packet_pool_set* HIZMETINI kullanarak DNS istemcisinin paket havuzu olarak ayarlaması içindir. Bunu yapmak için NX_DNS_CLIENT_USER_CREATE_PACKET_POOL seçeneğinin tanımlanması gerekir. Bu seçenek ayrıca, *nx_dns_packet_pool_set* için paket havuzu işaretçisi girişi olarak *nx_packet_pool_create* kullanarak daha önce oluşturulmuş bir paket havuzu gerektirir. DNS Istemcisi örneği silindiğinde, artık gerekmiyorsa, uygulama DNS Istemci paket NX_DNS_CLIENT_USER_CREATE_PACKET_POOL havuzunu silmekten sorumludur.

> [!NOTE] 
> NX_DNS_CLIENT_USER_CREATE_PACKET_POOL seçeneğini kullanarak kendi paket havuzunu sağlamayı tercih eden uygulamalar için, paket boyutunun DNS en yüksek maszu boyutunu (512 bayt) ve UDP üst bilgisi, IPv4 veya IPv6 üst bilgisi ve MAC üst bilgisi için Odalar ' ı tutabilecek olması gerekir.

## <a name="dns-messages"></a>DNS Iletileri

DNS, ana bilgisayar adları ve IP adresleri arasında eşleme almak için çok basit bir mekanizmaya sahiptir. DNS Istemcisi, bir eşleme almak için, ad veya çözümlenmesi gereken IP adresini içeren bir DNS sorgu iletisi hazırlar. İleti daha sonra sunucu listesindeki ilk DNS sunucusuna gönderilir. Sunucuda böyle bir eşleme varsa, istenen eşleme bilgilerini içeren bir DNS yanıt iletisi kullanarak DNS Istemcisine yanıt verir. Sunucu yanıt vermezse, DNS Istemcisi, tüm DNS sunucuları sorgulanana kadar listesinde bir sonraki sunucuyu sorgular. Tüm DNS sunucularından yanıt alınmıyorsa DNS Istemcisinin, DNS iletisini yeniden aktarım mantığı vardır. Bir DNS sorgusunu yeniden gönderme sırasında yeniden iletim zaman aşımı iki katına çıkar. Bu işlem, en fazla iletim zaman aşımı ( *nxd_dns. h* içinde NX_DNS_MAX_RETRANS_TIMEOUT olarak tanımlanır) ulaşılıncaya veya bu sunucudan başarılı bir yanıt alınana kadar devam eder.

NetX Duo DNS Istemcisi, *nxd_dns_host_by_name_get* çağrısında IP adresinin sürümünü belirterek hem IPv6 adres aramalarını (tür aaaa) hem de IPv4 adresi aramalarını (tür A) gerçekleştirebilir. DNS Istemcisi, *nxd_dns_host_by_address_get* kullanarak Web ana bilgisayar adlarını almak için IP ADRESLERININ (PTR sorguları yazın) ters aramalarını gerçekleştirebilir. NetX Duo DNS Istemcisi, eşdeğer hizmetler olan ancak IPv4 ağ iletişimi ile sınırlı olan *nx_dns_host_by_name_get* ve *nx_dns_host_by_address_get* desteklemektedir. Ancak, geliştiriciler mevcut DNS Istemci uygulamalarının *nxd_dns_host_by_name_get* ve *nxd_dns_host_by_address_get* hizmetlerine bağlantı altına alınır.

DNS mesajlaşma istekleri ve alan yanıtlarını göndermek için UDP protokolünü kullanır. DNS sunucusu, istemcilerden gelen sorgular için 53 numaralı bağlantı noktasını dinler. Bu nedenle, daha önce oluşturulmuş bir IP örneğinde (_ *_nx_ip_create_* *) ***nx_udp_enable** _ hizmeti kullanılarak NETX Duo 'da UDP Hizmetleri etkinleştirilmelidir.

Bu noktada, DNS Istemcisi, uygulamadan gelen istekleri kabul etmeye ve DNS sorguları göndermeye hazır hale gelir.

## <a name="extended-dns-resource-record-types"></a>Genişletilmiş DNS kaynak kaydı türleri

NX_DNS_ENABLE_EXTENDED_RR_TYPES etkinleştirilirse NetX Duo DNS Istemcisi aşağıdaki kayıt türü sorgularını de destekler:

- CNAME: bir diğer ad için kurallı adı içerir
- TXT: bir metin dizesi içerir
- NS: bir yetkili ad sunucusu içerir
- SOA: bir yetki bölgesinin başlangıcını içerir
- MX: posta alışverişi için kullanıldı
- SRV: etki alanı tarafından sunulan hizmet hakkındaki bilgileri içerir

CNAME ve TXT kayıt türlerinin dışında, uygulamanın DNS veri kaydını almak için 4 baytlık hizalanmış bir arabellek sağlaması gerekir.

NetX Duo DNS Istemcisinde, kayıt verileri, arabellek alanının en verimli şekilde kullanılmasını sağlamak için bu şekilde depolanır.

Sabit uzunlukta bir kayıt arabelleği örneği (tür AAAA kaydı) aşağıda gösterilmiştir:

![Sabit uzunluktaki kayıt arabelleğini](media/image2.png)

Kayıt türleri değişken veri uzunluğuna sahip olan sorgular için, ana bilgisayar adları değişken uzunlukta olan NS kayıtları gibi, NetX Duo DNS Istemcisi verileri aşağıdaki gibi kaydeder. DNS Istemcisi sorgusunda sağlanan arabellek, sabit uzunluklu verilerin bir alanı ve yapılandırılmamış bellek alanı halinde düzenlenir. Bellek arabelleğinin en üstü 4 baytlık hizalanmış kayıt girişlerine göre düzenlenmiştir. Her kayıt girdisi, IP adresini ve bu IP adresi için değişken uzunluklu verilere yönelik bir işaretçi içerir. Her IP adresi için değişken uzunluklu veri, bellek arabelleğinin sonundan itibaren yapılandırılmamış alan belleğinde depolanır. Art arda her bir kayıt girişinin değişken uzunluğu verileri, önceki kayıt girişleri değişken verilerine bitişik bir sonraki alan belleğine kaydedilir. Bu nedenle, değişken veri, başka bir kayıt girişi ve değişken verileri depolamak için yeterli bellek olmadığından, kayıt girdilerini içeren yapılandırılmış belleğin yapısal alanına doğru bir şekilde ' büyür '.

Bu, aşağıdaki şekilde gösterilmiştir:

![Şekil 2](media/image3.png)

DNS etki alanı adı (NS) veri depolama örneği yukarıda gösterilmektedir.

NetX Duo DNS Istemci sorguları kayıt depolama biçimini kullanarak, kayıt arabelleğine kaydedilen kayıt sayısını döndürür. Bu bilgiler, uygulamanın kayıt arabelleğindeki NS kayıtlarını ayıklamasına olanak sağlar.

Bu kayıt depolama biçimini kullanarak değişken uzunlukta DNS verilerini depolayan DNS Istemci sorgusunun bir örneği aşağıda gösterilmiştir:

```C
UINT  _nx_dns_domain_name_server_get(NX_DNS *dns_ptr, 
                    UCHAR *host_name, VOID *record_buffer, 
                    UINT buffer_size, UINT *record_count, 
                    ULONG wait_option);
```


"DNS Istemci hizmetlerinin açıklaması" başlıklı Bölüm 3 ' te daha fazla ayrıntı bulabilirsiniz.

## <a name="dns-cache"></a>DNS önbelleği

NX_DNS_CACHE_ENABLE etkinleştirilirse NetX Duo DNS Istemcisi DNS önbelleği özelliğini destekler. DNS Istemcisini oluşturduktan sonra uygulama, özel DNS önbelleğini ayarlamak için API *nx_dns_cache_initialize ()* çağırabilir. DNS önbelleği özelliğini etkinleştir özelliği, DNS Istemcisi, DNS sorgusu gönderilmeye başlamadan önce DNS önbelleğinden kullanılabilir yanıtı bulacak, kullanılabilir yanıtı bul, doğrudan uygulamaya yanıt döndürür, aksi takdirde DNS Istemcisi DNS sunucusuna sorgu iletisi gönderir ve yanıtı bekler. DNS Istemcisi yanıt iletisini aldığında ve kullanılabilir boş önbellek varsa, DNS Istemcisi yanıtı uygulamaya döndürür ve aynı zamanda yanıtı kaynak kaydı olarak DNS önbelleğine ekler.

Her biri önbellekte bir veri yapısını *NX_DNS_RR* (kaynak kaydı). Kayıtlardaki dizeler (kaynak kaydı adı ve verileri) değişken uzunluktadır, bu nedenle NX_DNS_RR yapısında depolanmaz. Kayıt, dizelerin depolandığı gerçek bellek konumunun işaretçilerini içerir. Dize tablosu ve kayıtlar önbelleği paylaşır. Kayıtlar önbelleğin başından itibaren saklanır ve önbelleğin sonuna doğru artar. Dize tablosu önbelleğin sonundan başlar ve önbelleğin başına doğru artar. Dize tablosundaki her bir dizenin bir uzunluk alanı ve bir sayaç alanı vardır. Dize tablosuna bir dize eklendiğinde, tabloda aynı dize zaten varsa, sayaç değeri artırılır ve dize için bellek ayrılmaz. Önbellekte daha fazla kaynak kaydı veya yeni dize eklenebileceği takdirde önbellek tam olarak değerlendirilir.

## <a name="dns-client-limitations"></a>DNS Istemci sınırlamaları

DNS Istemcisi tek seferde bir DNS isteğini destekler. Önceki DNS isteği tamamlanana kadar başka bir DNS isteği yapmaya çalışan iş parçacıkları geçici olarak engellenir.

NetX Duo DNS Istemcisi, ek DNS sorgularını diğer DNS sunucularına iletmek için yetkili yanıtlardan veri kullanmaz.

## <a name="dns-rfcs"></a>DNS RFC 'Leri

NetX Duo DNS, aşağıdaki RFC 'lerle uyumludur:

- RFC1034 ETKI ALANı ADLARı-KAVRAMLAR VE TESISLER
- RFC1035 ETKI ALANı ADLARı-UYGULAMA VE BELIRTIM
- RFC1480 ABD etki alanı
- RFC 2782 hizmetlerin konumunu belirtmek için bir DNS RR (DNS SRV)
- RFC 3596 DNS uzantıları IP sürüm 6 ' yı destekler