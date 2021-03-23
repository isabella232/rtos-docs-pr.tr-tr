---
title: Bölüm 1-Azure RTOS NetX Duo DHCPv6 Istemcisine giriş
description: IPv6 ağlarında, DHCPv6 bir DHCPv6 sunucusundan dinamik genel IP adresi ataması için DHCP 'yi değiştirir ve birçok geliştirmede de aynı özelliklerin çoğunu sağlar.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 3bf3b52c53bb26e2c9c2c736ae35817eb967f609
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826098"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-dhcpv6-client"></a>Bölüm 1-Azure RTOS NetX Duo DHCPv6 Istemcisine giriş

IPv6 ağlarında, DHCPv6 bir DHCPv6 sunucusundan dinamik genel IP adresi ataması için DHCP 'yi değiştirir ve birçok geliştirmede de aynı özelliklerin çoğunu sağlar. Bu belgede, Azure RTOS NetX Duo DHCPv6 Istemci API 'sinin IPv6 adreslerini almak için nasıl kullanıldığı ayrıntılı olarak açıklanacaktır.

## <a name="dhcpv6-communication"></a>DHCPv6 Iletişimi

DHCPv6 Protokolü UDP kullanır. Istemci, 546 bağlantı noktasını ve sunucu, DHCPv6 iletilerini değiş tokuş etmek için 547 numaralı bağlantı noktasını kullanır. Istemci, kullanılabilir DHCPv6 sunucusuna DHCPv6 isteklerini başlatmak üzere bir kaynak adresi için bağlantı yerel adresini kullanır. Istemci ağdaki tüm DHCPv6 sunucularına yönelik iletileri gönderdiğinde, *FF02:: 01:02* çok noktaya yayın adresi *All_DHCP_Relay_Agents_and_Servers* kullanır. Bu, ayrılmış, bağlantı kapsamlı çok noktaya yayın adresidir.

## <a name="dhcpv6-process-of-requesting-an-ipv6-address"></a>IPv6 adresi ısteyen DHCPv6 Işlemi

Genel bir IPv6 adresi ataması isteme işlemini başlatmak için, Istemci önce *nx_dhcpv6_send_solicit* hizmetini kullanarak bir istem iletisi gönderir:

**UINT nx_dhcpv6_request_solicit (NX_DHCPV6 \* dhcpv6_ptr)**

Bu ileti, *All_DHCP_Relay_Agents_and_Servers* adresi kullanılarak tüm sunuculara gönderilir. İstek isteğinde Istemci, belirli IPv6 adreslerinin sunucuya bir ipucu olarak atanmasını isteyebilir. Ayrıca, DNS sunucusu, NTP sunucusu gibi sunucudan diğer ağ yapılandırma bilgilerini ve Istem iletisindeki seçenek Isteğindeki diğer seçenekleri de isteyebilir.

Istemci isteğine hizmet veren bir DHCPv6 sunucusu, istemciye atayabileceği IPv6 adreslerini, IPv6 adresi kiralama süresini ve Istemci tarafından istenen ek bilgileri içeren bir TANıTıM iletisiyle yanıt verir. DHCPv6 Istemci protokolü, Istemcinin ağdaki tüm DHCPv6 sunucularından TANıTıM iletileri alması için bir süre beklemesi gerekir. Her TANıTıM iletisini geçerli bir ileti olacak şekilde önceden işler ve çeşitli DHCPv6 parametreleri için seçenek verilerini tarar. Ayrıca, sunucu tarafından sağlandıysa tercih seçeneğinde tercih değeri de kontrol eder. Birden fazla TANıTıM iletisi alınmışsa NetX DHCPv6 Istemcisi, bekleme döneminin sonuna kadar en yüksek tercih değeri alınan sunucuyu seçer.

Istemci, tercih değeri 255 olan bir TANıTıM iletisi alırsa özel durum olur. Bu iletiyi hemen kabul eder ve sonraki TANıTıM iletilerini atar.

Bekleme süresi, DHCPv6 Istemcisinin herhangi bir sunucudan yanıt almamışsa başka bir Istem iletisi göndermeden önce bekleyeceği yeniden iletim süresi olarak tanımlanır. Istem durumundaki ilk yeniden iletim zaman aşımı tarafından, RFC 3315 ' de açıklanan DHCPv6 protokolüne 1 saniye olarak tanımlanmıştır. Sonraki yeniden iletim aralıkları, DHCPv6 Istemcisi geçerli bir sunucu yanıtı alamıyorsa, en fazla 120 saniyeye kadar katına çıkar.

Sunucu seçildiğinde, Istemci verileri TANıTıM iletisinden ayıklar ve atanan adres bilgilerini ve kira sürelerini kabul etmek için sunucuya bir Istek iletisi gönderir. Sunucu, istemci IPv6 adreslerini doğrulamak için bir yanıt iletisiyle yanıt verir ve istemciye atanan sunucu ile birlikte kaydedilir.

DHCPv6 Istemcisi atanan IPv6 adreslerini IP örneğiyle (örn. NetX Duo) kaydeder. Yinelenen adres algılama (BABACıĞıM) protokolü için yapılandırıldıysa (varsayılan olarak etkindir), NetX Duo, atanan adresleri ağda benzersiz olduğunu doğrulamak için otomatik olarak komşu Istek iletileri gönderir. Bu durumda, atanan her adres belırsız ' den GEÇERLI ' a yükseltildiğinde DHCPv6 Istemcisine bildirir. DHCPv6 Istemcisi, bağlantılı duruma yükseltilir ve cihaz, ileti göndermek ve iletmek için bu IPv6 adresini kullanabilir. BABACıĞıM Protokolü başarısız olursa NetX Duo, DHCPv6 Istemcisine bildirir ve DHCPv6 Istemcisi sunucuya geri atanan IPv6 adresleri için bir reddetme iletisi gönderir ve DHCPv6 Istemci durumunu ıNIT durumuna sıfırlar.

### <a name="notification-of-successful-address-assignment-and-validation"></a>Başarılı adres atama ve doğrulama bildirimi

Uygulama, DHCPv6 Istemcisi *nx_dhcpv6_client_create* hizmetinde durum değişikliği geri çağırması ile yapılandırılmışsa durum değişikliklerinden DHCPv6 istemci adresi bağlantısı 'nın sonucunu belirleyebilir. Sunucudan yanıt alırsa, gözlemlenen durum değişikliği gözlemden ıNIT 'e kadar olur. Sunucudan bir yanıt aldıysa, ancak sunucu adresi atayamadığında, uygulama DHCPv6 Istemci sunucusu hata geri çağırması ile yapılandırılmışsa ( *nx_dhcpv6_client_create de) bildirilir.* Istemci, bağlantılı duruma ulaşıldığı halde, BABACıĞıM denetiminde başarısız olursa, bir durum değişikliğini ıNIT 'e göre görür. BABACıĞıM için etkinleştirilen bir uygulamanın, istek işlemini başlattıktan sonra baba denetimi zamanına izin vermelidir. Genellikle bu yaklaşık 400-500 onay işareti (çoğu durumda 4-5 saniyedir).

### <a name="relinquishing-an-ipv6-address"></a>Bir IPv6 adresini yeniden barındırma

Istemcinin atanan bir IPv6 adresini serbest bırakması gerekiyorsa, *nx_dhcpv6_request_release* hizmetini çağırarak DHCPv6 sunucusuna bildirir:

### <a name="uint-nx_dhcpv6_request_releasenx_dhcpv6-dhcpv6_ptr"></a>UINT nx_dhcpv6_request_release (NX_DHCPV6 \* dhcpv6_ptr)

DHCPv6 Istemcisi, adresi atayan sunucuya atanan adresleri içeren bir tek noktaya yayın yayın iletisi gönderir ve sunucunun iletiyi aldığını onaylayan bir yanıt bekler.

Note: Istemci için başka bir işlem var, ancak yeniden başlatma sırasında atanan IPv6 adreslerini kullanmaya devam etmeyi planlıyor. Power Up üzerinde yeni bir adres istemeyi planlayana kadar, yayın iletisini güçlendirin. Bu durumun açıklaması için "geçici olmayan bellek gereksinimleri" bölümüne bakın.

### <a name="dhcpv6-lease-timeouts"></a>DHCPv6 kira zaman aşımları

Sunucu tarafından atanan IPv6 kirası, her kimlik Ilişkilendirmesi: geçici olmayan adresler (ıANA) bloğunda iki zaman aşımı parametresi, T1 ve T2 içerir. Bir ıANA, bu kullanıcı kılavuzunun başka bir yerinde açıklanmıştır. DHCPv6 Istemcisinin atanan IPv6 adresine eşit olması durumunda geçen süre, bir yenıleme iletisi göndererek, DHCPv6 Istemcisi otomatik olarak IPv6 adresini yenilemeyi başlatır. Geçen süre T2 'ya eşitse, DHCPv6 Istemcisi yenıleme isteklerine yanıt almamışsa otomatik olarak bir yeniden bağlama iletisi gönderir.

IANA bloğunda bulunan her bir kimlik Ilişkilendirmesi (IA) bloğu ile, tercih edilen ve geçerli ömür dışında iki diğer IPv6 kira parametresi atanır. Tercih edilen ve geçerli yaşam süreleri, atanan IPv6 adresinin sırasıyla kullanım dışı veya geçersiz olduğu durumlarda kullanılır. T1, tercih edilen yaşam süresinden daha az olmalıdır. T2, geçerli yaşam süresinden az olmalıdır.

### <a name="ip-thread-task-requirements"></a>IP Iş parçacığı görev gereksinimleri

NetX Duo DHCPv6 Istemcisi, DHCPv6 istemci hizmetlerini kullanmak için DHCPv6 Istemcisini oluşturmadan önce bir NetX Duo IP örneği oluşturulmasını gerektirir.

UDP, IPv6 ve ICMPv6, IP örneğinde, using DHCPv6 Istemcisinden önce etkinleştirilmelidir.

  - *nx_udp_enable*

  - *nxd_ipv6_enable*

  - *nxd_icmp_enable*

### <a name="packet-pool-requirements"></a>Paket havuzu gereksinimleri

NetX Duo DHCPv6 Istemcisi oluşturma, DHCPv6 iletilerini göndermek için önceden oluşturulmuş bir paket havuzu gerektirir. Paket yükü ve kullanılabilir paket sayısı açısından paket havuzunun boyutu Kullanıcı tarafından yapılandırılabilir ve uygulamanın gönderilecek DHCPv6 iletilerinin ve diğer aktarımların hacmine bağlıdır.

Tipik bir DHCPv6 iletisi, Istemci tarafından istenen IA adreslerinin ve DHCPv6 seçeneklerinin sayısına bağlı olarak 200 bayttır.

### <a name="network-requirements"></a>Ağ Gereksinimleri

NetX Duo DHCPv6 Istemcisi, 546 numaralı bağlantı noktasına yönelik UDP yuvası oluşturulmasını gerektirir. Yuva, DHCPv6 Istemci görevi oluşturulduğunda oluşturulur.

### <a name="non-volatile-memory-requirements"></a>Geçici olmayan bellek gereksinimleri

Bir DHCPv6 Istemcisi, kapatılırken DHCPv6 sunucusuyla birlikte IPv6 kiralamasını serbest bırakır ve yeniden başlatma sırasında yeni IPv6 adresleri isterse, geçici olmayan bellek depolaması gerekli değildir. Bir Istemci, atanmış kiralamasını kullanmaya devam etmek isterse, yeniden başlatmalar arasında geçici olmayan bellek için DHCPv6 Istemcisiyle ilgili bazı bilgileri depolaması gerekir.

Geçici olmayan bellek gereksinimleri ve DHCPv6 Istemci API 'SI, Bölüm 2 ' de **NetX Duo DHCPv6 Istemcisini kullanarak** daha ayrıntılı bir şekilde ele alınmıştır.

### <a name="netx-duo-dhcpv6-client-limitations"></a>NetX Duo DHCPv6 Istemci sınırlamaları

NetX Duo DHCPv6 Istemcisinin geçerli sürümü aşağıdaki sınırlamalara sahiptir:

  - NetX Duo DHCPv6 Istemcisi, sunucu buna izin verildiğini belirtse bile DHCPv6 sunucusuna tek noktaya yayın DHCPv6 iletileri göndermek için sunucu tek noktaya yayın seçeneğini desteklemez.

  - NetX Duo DHCPv6 Istemcisi, bir sunucunun ağdaki Istemcilerde IPv6 adres değişikliklerini başlattığı yeniden yapılandırma isteğini desteklemez.

  - NetX Duo DHCPv6 Istemcisi, DHCPv6 benzersiz tanımlayıcı denetim bloğunun kurumsal biçimini desteklemez. Yalnızca bağlantı katmanını ve bağlantı katmanını ve zaman biçimini destekler.

  - NetX Duo DHCPv6 Istemcisi geçici Ilişkilendirme (TA) adres isteklerini desteklemez, ancak geçici olmayan (ıANA) seçenek isteklerini destekler.

## <a name="multihome-and-multiple-address-support"></a>Çoklu giriş ve çoklu adres desteği

DHCPv6 Istemcisi, arabirim başına birden çok arabirimi ve birden çok adresi destekler. DHCPv6 Istemci hizmeti, *Nx_dhcpv6_client_set_interface* istemci uygulamanın, uygulamanın DHCPv6 sunucusuyla iletişim kuramadığı ağ arabirimini ayarlanmasını sağlar. DHCPv6 Istemcisi birincil arabirime (Dizin sıfır) göre varsayılan değer.

Her arabirim için birden çok adres için, DHCPv6 Istemcisi 0 dizininden başlayan bir iç adres listesini tutar. DHCPv6 Istemcisiyle aynı adresin, arabirim adresleri IP tablosundaki aynı dizinde konumlandırılabilir olabileceğini unutmayın.

Istemci IPv6 adresi kirası hakkında bilgi alan DHCPv6 Istemci Hizmetleri için bazıları için bir adres dizininin belirtilmesi gerekir. Tercih edilen ve geçerli yaşam sürelerini elde etmenin bir örneği aşağıda gösterilmiştir:

```C
UINT nx_dhcpv6_get_valid_ip_address_lease_time(NX_DHCPV6 *dhcpv6_ptr, 
                                              UINT address_index, 
                                              NXD_ADDRESS *ip_address,
                                              ULONG preferred_lifetime, 
                                              ULONG *valid_lifetime)
```

Istemci uygulaması, *nx_dhcpv6_get_valid_ip_address_count* hizmetinden atanan geçerli IPv6 adreslerinin sayısını da alabilir:

```C
UINT nx_dhcpv6_get_valid_ip_address_count(NX_DHCPV6 *dhcpv6_ptr, 
                                          UINT *address_count)
```

NetX Duo 'da birden çok adres desteklenmadan önce oluşturulan eski DHCPv6 Istemci Hizmetleri bir adres dizini almaz. Bu nedenle, bu hizmetlerle, Istemciye kaç tane IA adresinin atandığına bakılmaksızın, istenen veriler birincil Global IA adresinden alınır. Aşağıda bir örnek gösterilmiştir:

```C
UINT nx_dhcpv6_get_IP_address(NX_DHCPV6 *dhcpv6_ptr, 
                              NXD_ADDRESS *ip_address)
```

## <a name="netx-duo-dhcpv6-client-callback-functions"></a>NetX Duo DHCPv6 Istemci geri çağırma Işlevleri

*nx_dhcpv6_state_change_callback*

DHCPv6 Istemcisi, DHCPv6 isteğini işlemenin sonucu olarak yeni bir DHCPv6 durumuna değiştirdiğinde, uygulamaya bu geri arama işlevini bildirir.

*nx_dhcpv6_server_error_handler*

DHCPv6 Istemcisi sıfır olmayan (başarılı olmayan *) bir durum seçeneği içeren* bir sunucu yanıtı aldığında, bu geri çağırma Ile, sunucu hata durum kodunu Içeren bir sunucu yanıtı alır.

Not: Bu geri çağırma işlevleri DHCPv6 Istemci iş parçacığı görevinden çağrıldığı için, Istemci uygulaması, *nx_dhcpv6_start, nx_dhcpv6_stop* ve iletileri doğrudan geri aramadan gönderen API 'lerden herhangi biri olan (örn. *Nx_dhcpv6_request_release*) bir NETX Duo DHCPv6 istemci hizmetini çağırmamalıdır.

## <a name="dhcpv6-rfcs"></a>DHCPv6 RFC 'Leri

NetX Duo DHCP, RFC3315, RFC3646 ve ilgili RFC 'lerle uyumludur.