---
title: Bölüm 1 - NetX Duo DNS Azure RTOS'ne giriş
description: DNS, etki alanı adları ile fiziksel IP adresleri arasında eşleme içeren dağıtılmış bir veritabanı sağlar.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: e878d32d6bcf514bb75a76b51e66c4d267b1a5b34f6c4b2df6ab231e5814ffc5
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116792067"
---
# <a name="chapter-1---introduction-to-the-azure-rtos-netx-duo-dns-client"></a>Bölüm 1 - NetX Duo DNS Azure RTOS'ne giriş

DNS, etki alanı adları ile fiziksel IP adresleri arasında eşleme içeren dağıtılmış bir veritabanı sağlar. İnternet üzerinde tam eşlemeyi *içeren tek* bir varlık olduğundan veritabanı dağıtılmış olarak adlandırılır. Eşlemenin bir bölümünü bulunduran bir varlığa DNS Sunucusu denir. İnternet, her biri veritabanının bir alt kümesini içeren çok sayıda DNS Sunucusu'lardan oluşur. DNS Sunucuları ayrıca etki alanı adı eşleme bilgileri için DNS İstemcisi isteklerine yalnızca istenen eşlemeye sahipse yanıt verir.

NetX Duo için DNS İstemcisi protokolü, uygulamaya bir veya daha fazla DNS Sunucusundan eşleme bilgileri talep etmek için hizmetler sağlar.

## <a name="dns-client-setup"></a>DNS İstemcisi Kurulumu

DNS İstemcisi paketinin düzgün çalışması için netX Duo IP örneğinin önceden oluşturulmuş olması gerekir.

DNS İstemcisi'ni oluşturduktan sonra, uygulamanın DNS İstemcisi tarafından bakımı yapılan sunucu listesine bir veya daha fazla DNS sunucusu eklemesi gerekir. Uygulama, DNS sunucuları eklemek için nxd_dns_server_add *kullanır.* NetX Duo DNS İstemcisi hizmeti *nx_dns_server_add* eklemek için de kullanılabilir. Ancak yalnızca IPv4 adreslerini kabul eder ve geliştiricilerin bunun yerine IPv4 *nxd_dns_server_add* kullanılması önerilir.

Ip NX_DNS_IP_GATEWAY_SERVER etkinse ve IP örneği ağ geçidi adresi sıfır olmayansa, IP örneği ağ geçidi birincil DNS sunucusu olarak otomatik olarak eklenir. DNS sunucusu bilgileri statik olarak bilinmiyorsa, NetX Duo için Dinamik Ana Bilgisayar Yapılandırma Protokolü (DHCP) aracılığıyla da türetilen olabilir. Daha fazla bilgi için lütfen NetX Duo DHCP Kullanıcı Kılavuzu'ne bakın.

DNS İstemcisi, DNS iletilerinin iletileceğini bir paket havuzu gerektirir. Varsayılan olarak, DNS İstemcisi bu  paket havuzunu nx_dns_create çağrılsa oluşturur. Yapılandırma seçenekleri NX_DNS_PACKET_PAYLOAD_UNALIGNED NX_DNS_PACKET_POOL_SIZE, uygulamanın sırasıyla bu paket havuzunun paket yükünü ve paket havuzu boyutunu (örneğin paket sayısı) belirlemesine olanak sağlar. Bu seçenekler, Bölüm 2'de "Yapılandırma Seçenekleri" bölümünde açıklanmıştır.

Kendi paket havuzunu oluşturmak için DNS İstemcisi'nin bir alternatifi, uygulamanın paket havuzunu oluşturması ve bunu nx_dns_packet_pool_set hizmetini kullanarak DNS İstemcisi'nin *paket havuzu olarak ayarlamasıdır.* Bunu yapmak için NX_DNS_CLIENT_USER_CREATE_PACKET_POOL seçeneği tanımlanmalıdır. Bu seçenek ayrıca önceden oluşturulmuş  bir paket havuzunu nx_packet_pool_create için paket havuzu işaretçisi girişi olarak kullanarak *nx_dns_packet_pool_set.* DNS İstemcisi örneği silindiğinde, uygulama artık gerekli olmadığı durumlarda etkin NX_DNS_CLIENT_USER_CREATE_PACKET_POOL DNS İstemcisi paket havuzunu silmekle sorumludur.

> [!NOTE] 
> NX_DNS_CLIENT_USER_CREATE_PACKET_POOL seçeneğini kullanarak kendi paket havuzunu sağlamayı seçen uygulamalar için, paket boyutunun DNS maksimum en büyük bayt boyutuna (512 bayt) ek olarak UDP üst bilgisi, IPv4 veya IPv6 üst bilgisi ve MAC üst bilgisi için odaları tutabilecek olması gerekir.

## <a name="dns-messages"></a>DNS İletileri

DNS, konak adları ile IP adresleri arasında eşleme elde etmek için çok basit bir mekanizmaya sahiptir. Bir eşleme elde etmek için DNS İstemcisi, çözülmesi gereken adı veya IP adresini içeren bir DNS sorgu iletisi hazırlar. İleti daha sonra sunucu listesinde ilk DNS sunucusuna gönderilir. Sunucuda böyle bir eşleme varsa, istenen eşleme bilgilerini içeren bir DNS yanıt iletisi kullanarak DNS İstemcisine yanıt verir. Sunucu yanıt vermiyorsa, DNS İstemcisi tüm DNS sunucuları sorgulanana kadar listesinde bir sonraki sunucuyu sorgular. Tüm DNS sunucularından yanıt alınamasa, DNS İstemcisi DNS iletiyi yeniden iletim mantığını yeniden deneme mantığına sahip olur. Bir DNS sorgusu yeniden gönderiken, yeniden iletim zaman aşımı iki katına çıkar. Bu işlem en yüksek iletim zaman aşımına *(nxd_dns.h'de* NX_DNS_MAX_RETRANS_TIMEOUT olarak tanımlanır) ulaşıncaya veya sunucudan başarılı bir yanıt alınana kadar devam eder.

NetX Duo DNS İstemcisi, çağrı çağrısında IP adresinin sürümünü belirterek hem IPv6 adres aramaları (AAAA türü) hem de IPv4 adres aramaları (A türü) *nxd_dns_host_by_name_get* gerçekleştirebilirsiniz. DNS İstemcisi, ip adreslerini kullanarak web ana bilgisayar adlarını almak için IP adreslerinin ters aramalarını (PTR sorguları *nxd_dns_host_by_address_get.* NetX Duo DNS İstemcisi, *eşdeğer* nx_dns_host_by_name_get  nx_dns_host_by_address_get ancak IPv4 ağ iletişimi ile sınırlı olan etki alanı ve ağ iletişimini desteklemeye devam ediyor. Ancak, geliştiricilerin mevcut DNS İstemci uygulamalarını nxd_dns_host_by_name_get *ve* *nxd_dns_host_by_address_get* teşvik edilecektir.

DNS mesajlaşması, istekleri ve alan yanıtlarını göndermek için UDP protokolünü kullanır. DNS Sunucusu, istemcilerden gelen sorgular için 53 numaralı bağlantı noktasını dinler. Bu nedenle, DAHA önce oluşturulmuş bir IP örneğinde ***nx_udp_enable** _ hizmeti kullanılarak NetX Duo'da UDP hizmetlerinin etkinleştirilmesi gerekir (_*_nx_ip_create_**).

Bu noktada DNS İstemcisi, uygulamanın isteklerini kabul etmeye ve DNS sorguları göndermeye hazırdır.

## <a name="extended-dns-resource-record-types"></a>Genişletilmiş DNS Kaynak Kaydı Türleri

Bu NX_DNS_ENABLE_EXTENDED_RR_TYPES, NetX Duo DNS İstemcisi aşağıdaki kayıt türü sorgularını da destekler:

- CNAME: Diğer ad için kurallı adı içerir
- TXT: bir metin dizesi içerir
- NS: yetkili bir ad sunucusu içerir
- SOA: Bir yetki bölgesi başlangıcını içerir
- MX: Posta değişimi için kullanılır
- SRV: Etki alanı tarafından sunulan hizmetle ilgili bilgileri içerir

CNAME ve TXT kayıt türleri dışında, uygulamaNıN DNS veri kaydını almak için 4 bayt hizalı bir arabellek sağlamak zorunda olması gerekir.

NetX Duo DNS İstemcisi'ne kayıt verileri, arabellek alanı kullanımını en verimli şekilde yapacak şekilde depolanır.

Aşağıda sabit uzunlukta (AAAA kaydı türü) bir kayıt arabelleği örneği gösterilmiştir:

![Sabit uzunlukta kayıt arabelleği](media/image2.png)

Kayıt türleri değişken veri uzunluğuna (ana bilgisayar adları değişken uzunlukta olan NS kayıtları gibi) sahip sorgular için, NetX Duo DNS İstemcisi verileri aşağıdaki gibi kaydeder. DNS İstemcisi sorgusunda sağlanan arabellek sabit uzunluktaki veriler ve yapılandırılmamış bellek alanı olarak düzenlenmiştir. Bellek arabelleğinin üst kısmında 4 bayt hizalı kayıt girdileri düzenlenmiştir. Her kayıt girdisi, BU IP adresi için IP adresini ve değişken uzunluk verilerini gösteren bir işaretçi içerir. Her IP adresi için değişken uzunluğu verileri, bellek arabelleğinin sonundan başlayarak yapılandırılmamış alan belleğinde depolanır. Artak her kayıt girdisi için değişken uzunluğu verileri, önceki kayıt girişleri değişken verileriyle bitişik olan sonraki alan belleğine kaydedilir. Bu nedenle değişken verileri, başka bir kayıt girdisini ve değişken verilerini depolamak için yetersiz bellek olana kadar kayıt girişlerini içeren yapılandırılmış bellek alanına doğru 'büyür'.

Bu, aşağıdaki şekilde gösterilmiştir:

![Şekil 2](media/image3.png)

DNS etki alanı adı (NS) veri depolama örneği yukarıda gösterilmiştir.

Kayıt depolama biçimini kullanan NetX Duo DNS İstemcisi sorguları, kayıt arabelleğine kaydedilen kayıt sayısını geri verir. Bu bilgiler, uygulamanın kayıt arabelleğinden NS kayıtlarını ayıklamasını sağlar.

Aşağıda, bu kayıt depolama biçimini kullanarak değişken uzunluklu DNS verilerini depolar bir DNS İstemcisi sorgusu örneği gösterilmiştir:

```C
UINT  _nx_dns_domain_name_server_get(NX_DNS *dns_ptr, 
                    UCHAR *host_name, VOID *record_buffer, 
                    UINT buffer_size, UINT *record_count, 
                    ULONG wait_option);
```


"DNS İstemci Hizmetlerinin Açıklaması" bölüm 3'te daha fazla ayrıntı mevcuttur.

## <a name="dns-cache"></a>DNS Önbelleği

Etkin NX_DNS_CACHE_ENABLE NetX Duo DNS İstemcisi, DNS Önbelleği özelliğini destekler. DNS İstemcisi'ni oluşturdukta, uygulama özel DNS *Önbelleğini ayarlamak için nx_dns_cache_initialize()* API'sini çağırabilirsiniz. DNS Önbelleği özelliğini etkinleştirirse, DNS İstemcisi DNS sorgusu göndermeye başlamadan önce DNS Önbelleği'nin kullanılabilir yanıtını bulur, kullanılabilir yanıtı bulursa doğrudan uygulamaya yanıt verir, aksi takdirde DNS İstemcisi dns sunucusuna sorgu iletisi gönderir ve yanıtı bekler. DNS İstemcisi yanıt iletiyi alır ve kullanılabilir boş önbellek olduğunda, DNS İstemcisi yanıtı uygulamaya döndürür ve yanıtı DNS önbelleğine kaynak kaydı olarak ekler.

Her biri önbellekte bir *NX_DNS_RR* (Kaynak Kaydı) veri yapısına yanıt verir. Kayıtlar'daki dizeler (kaynak kaydı adı ve verileri) değişken uzunluktadır, bu nedenle NX_DNS_RR depolanmaz. Kayıt, dizelerin depolandığı gerçek bellek konumunun işaretçilerini içerir. Dize tablosu ve Kayıtlar önbelleği paylaşır. Kayıtlar önbelleğin başından depolanır ve önbelleğin sonuna doğru büyür. Dize tablosu önbelleğin sonundan başlar ve önbelleğin başlangıcına doğru büyür. Dize tablosunda yer alan her dizenin bir uzunluk alanı ve bir sayaç alanı vardır. Dize tablosuna bir dize ekleniyorsa, aynı dize tabloda zaten varsa sayaç değeri artırılır ve dize için bellek ayrılır. Önbelleğe başka kaynak kaydı veya yeni dize eklene ise önbellek tam olarak kabul edilir.

## <a name="dns-client-limitations"></a>DNS İstemci sınırlamaları

DNS İstemcisi aynı anda bir DNS isteğini destekler. Başka bir DNS isteği yapmaya çalışan iş parçacıkları, önceki DNS isteği tamamlandıktan sonra geçici olarak engellenir.

NetX Duo DNS İstemcisi, ek DNS sorgularını diğer DNS sunucularına iletmeye yetkili yanıtlardan gelen verileri kullanmaz.

## <a name="dns-rfcs"></a>DNS RFC'leri

NetX Duo DNS aşağıdaki RFC'lerle uyumludur:

- RFC1034 ETKI ALANı ADLARı - KAVRAMLAR VE TESISLER
- RFC1035 ETKI ALANı ADLARı - UYGULAMA VE BELIRTIM
- RFC1480 ABD Etki Alanı
- RFC 2782 Hizmetlerin konumunu belirtmek için bir DNS RR (DNS SRV)
- IP Sürümünü Desteklemek için RFC 3596 DNS Uzantıları 6