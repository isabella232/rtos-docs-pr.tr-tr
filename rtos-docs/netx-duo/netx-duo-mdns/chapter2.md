---
title: Bölüm 2-mDNS yüklemesi ve kullanımı
description: Bu bölümde, NetX Duo mDNS modülünün yüklenmesi, kurulması ve kullanımı ile ilgili çeşitli sorunların bir açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 07/09/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 6f9e3d023f1bdbde4546a94da1bc1ccb48578d0e
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825919"
---
# <a name="chapter-2---installation-and-use-of-mdns"></a>Bölüm 2-mDNS yüklemesi ve kullanımı

Bu bölümde, NetX Duo mDNS modülünün yüklenmesi, kurulması ve kullanımı ile ilgili çeşitli sorunların bir açıklaması yer almaktadır.

## <a name="product-distribution"></a>Ürün dağıtımı

NetX Duo mDNS, adresinde bulunabilir [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo) . Paket, aşağıdaki gibi, bu belgeyi içeren iki kaynak dosya ve bir PDF dosyası içerir:

- **nxd_mdns. h** NetX Duo mDNS modülü için üst bilgi dosyası
- **nxd_mdns. c** NetX Duo mDNS modülü için C kaynak dosyası
- **nxd_mdns.pdf** NetX Duo için mDNS 'nin PDF açıklaması
- **demo_netxduo_mdns. c** MDNS tarafından sunulan hizmetleri gösteren basit bir tanıtım programı.

## <a name="netx-duo-mdns-installation"></a>NetX Duo mDNS yüklemesi

NetX Duo mDNS API 'Lerini kullanmak için, daha önce bahsedilen tüm dağıtımın, NetX Duo 'un yüklü olduğu dizine kopyalanması gerekir. Örneğin, "*c:\netxduo*" dizininde NETX Duo yüklüyse, *nxd_mdns. h* ve *nxd_mdns. c* bu dizine kopyalanmalıdır.

## <a name="using-netx-duo-mdns"></a>NetX Duo mDNS kullanma

NetX Duo mDNS modülünü kullanmak kolaydır. Temel olarak, uygulama kodu *nxd_mdns.* h *ve tx_api. h ve* *nx_api. h* Içermelidir. Bu, sırasıyla threadx ve NETX Duo kullanmak için. Yapı Projesi, mDNS kaynak kodunu ve uygulama dosyasını ve ThreadX ve NetX kitaplık dosyalarını kapsayan kurs içermelidir. Bu, NetX Duo mDNS kullanmak için gereklidir.

## <a name="configuration-options"></a>Yapılandırma seçenekleri

NetX Duo mDNS modülünü oluşturmak için birkaç yapılandırma seçeneği vardır. Varsayılan değerler listelenir, ancak her bir tanımlama, belirtilen NetX Duo mDNS üst bilgi dosyasına dahil etmeden önce uygulama tarafından ayarlanabilir. Aşağıdaki listede her biri ayrıntılı açıklanmıştır:

- **NX_MDNS_DISABLE_SERVER** MDNS/DNS-SD sunucu işlevini devre dışı bırakır. Sunucu işlevselliği olmadan, mDNS/DNS-SD modülü yerel ana bilgisayar tarafından sunulan hizmetleri duyurmaz ve mDNS enquiries 'e yanıt vermez. Bu simge varsayılan olarak tanımlanmamıştır.
- **NX_MDNS_DISABLE_CLIENT** MDNS/DNS-SD istemci işlevini devre dışı bırakır. İstemci işlevselliği olmadan, mDNS/DNS-SD sorgu göndermez veya ağ üzerinden alınan mDNS sorgu yanıtlarını korumaz.
- **NX_MDNS_ENABLE_ADDRESS_CHECK** Tanımlanan mDNS modülü, alınan mDNS iletilerinden adresleri (kaynak adresi, hedef adres ve bağlantı noktası numaraları) doğrular. Bu sembol varsayılan olarak tanımlanmıştır.
- **NX_MDNS_ENABLE_CLIENT_POOF** Tanımlanan mDNS modülü, hataların pasif bir şekilde gözlemleyerek, mDNS/DNS_SD istemcisi (sorgulayıcı) ağdaki diğer ana bilgisayarlar tarafından verilen çok noktaya yayın sorgularını görür. Bu sembol varsayılan olarak tanımlanmıştır.
- **NX_MDNS_ENABLE_SERVER_NEGATIVE_RESPONSES** Tanımlı, mDNS/DNS-SD Server (Yanıtlayıcı), sahiplik sahibi olan sorgulara olumsuz yanıtlar üretir. Bu sembol varsayılan olarak tanımlanmıştır.
- **NX_MDNS_ENABLE_IPV6** Tanımlı, mDNS/DNS-SD IPv6 adresi üzerinden mDNS iletisi gönderme/işleme iletisi. Bu simge varsayılan olarak tanımlanmamıştır.
- **NX_MDNS_IPV6_ADDRESS_COUNT** En fazla IPv6 adresi ana bilgisayar sayısıdır. Varsayılan değer 2 ' dir.
- **NX_MDNS_HOST_NAME_MAX** Ana bilgisayar adı için en büyük dize boyutu. Varsayılan değer 64 ' dir. NULL Sonlandırıcı içermez.
- **NX_MDNS_SERVICE_NAME_MAX** Hizmet adı için en büyük dize boyutu. Varsayılan değer 64 ' dir. NULL Sonlandırıcı içermez.
- **NX_MDNS_DOMAIN_NAME_MAX** Etki alanı adı için en büyük dize boyutu. Varsayılan değer 16'dır. NULL Sonlandırıcı içermez.
- **NX_MDNS_CONFLICT_COUNT** Ana bilgisayar adı veya hizmet adı için en büyük çakışma sayısı. Varsayılan değer 8 ' dir.
- **NX_MDNS_RR_TTL_HOST** Ana bilgisayar adına sahip kaynak kayıtlarına yönelik TTL değeri (saniye). 120s için varsayılan değer 120 ' dir.
- **NX_MDNS_RR_TTL_OTHER** İkinci olarak diğer kaynak kayıtları için TTL değeri. 75 dakika için varsayılan değer 4500 ' dir.
- **NX_MDNS_PROBING_TIMER_COUNT** MDNS yoklama iletileri arasındaki zaman aralığı (ticks cinsinden). Varsayılan değer, 250ms için 25 ticks değeridir.
- **NX_MDNS_ANNOUNCING_TIMER_COUNT** MDNS duyuru iletileri arasındaki zaman aralığı (ticks cinsinden). Varsayılan değer, 250ms için 25 ticks değeridir.
- **NX_MDNS_GOODBYE_TIMER_COUNT** Yinelenen "güle" iletileri arasındaki zaman aralığı (tick). Varsayılan değer, 250ms için 25 ticks değeridir.
- **NX_MDNS_QUERY_MIN_TIMER_COUNT** İki sorgu arasındaki, zaman aralığı cinsinden minimum zaman aralığı. 1 saniye için varsayılan değer 100 ticks değeridir.
- **NX_MDNS_QUERY_MAX_TIMER_COUNT** İki sorgu arasındaki, zaman aralığı cinsinden maksimum zaman aralığı. 60 saniye için varsayılan değer 360000 ' dir.
- **NX_MDNS_QUERY_DELAY_MIN** İlk sorgu göndermek için gereken en düşük gecikme (Ticks). Varsayılan değer 20ms için 2 ticks değeridir.
- **NX_MDNS_QUERY_DELAY_RANGE** Aralık olarak ilk sorguyu göndermek için gecikme aralığı. Varsayılan değer 100ms için 10 ticks değeridir.
- **NX_MDNS_RESPONSE_INTERVAL** Kaydın çok noktaya yayın yaptığından önce en az 1 ' in zaman aralığını sağlamak üzere bir sorguya yanıt veren zaman aralığı. Varsayılan değer 100 ticks değeridir.
- **NX_MDNS_RESPONSE_PROBING_TIMER_OUT** Kaydın çok noktaya yayın yaptığından en az 250ms aralığı olmasını sağlamak üzere bir araştırma sorgusuna yanıt veren zaman aralığı. Varsayılan değer 25 ticks değeridir.
- **NX_MDNS_RESPONSE_UNIQUE_DELAY** Yerel ağ için benzersiz olan bir hizmete yapılan bir sorguya yanıt verme ve sayaç cinsinden gecikme. Varsayılan değer 10 MS için 1 değer değeridir.
- **NX_MDNS_RESPONSE_SHARED_DELAY_MIN** Paylaşılan kaynağa yönelik bir sorguya yanıt veren, ölçü cinsinden minimum gecikme. Varsayılan değer 20ms için 2 ticks değeridir.
- **NX_MDNS_RESPONSE_SHARED_DELAY_RANGE** Paylaşılan kaynağa yönelik bir sorguya yanıt vermek için, saat cinsinden gecikme aralığı. Varsayılan değer 100ms için 10 ticks değeridir.
- **NX_MDNS_RESPONSE_TC_DELAY_MIN** TC bit içeren bir sorguya yanıt vermek için ölçü cinsinden minimum gecikme. Varsayılan değer, 400ms için 40 ticks değeridir.
- **NX_MDNS_RESPONSE_TC_DELAY_RANGE** Bir sorgu için TC bit ile yanıt verme cinsinden gecikme aralığı. Varsayılan değer 100ms için 10 ticks değeridir.
- **NX_MDNS_TIMER_COUNT_RANGE** MDNS yanıtlarını gönderirken paket, bu zamanlayıcı sayaç aralığı içinde başka bir şekilde gönderilecek yanıtları içerir. Süreölçer sayı aralığı, Tick olarak ifade edilir. Varsayılan değer, 120ms için 12 ' dir. Bu değer, her bir değer 10 ms ise sonraki 120ms aralığında gönderilecek iletileri dahil etmek için bir yanıt verir.
- **NX_MDNS_PROBING_RETRANSMIT_COUNT** Yeniden aktarılan yoklama iletilerinin sayısı. Varsayılan değer 3 ' dir.
- **NX_MDNS_GOODBYE_RETRANSMIT_COUNT** Yeniden aktarılan "güle" iletilerinin sayısı. Varsayılan değer 1’dir.
- **NX_MDNS_POOF_MIN_COUNT** Çok noktaya yayın yanıtı olmayan sorguların sayısı, ana bilgisayar bunu kaydın artık geçerli olmadığını belirten bir gösterge olarak alabilir. Varsayılan değer 2 ' dir.
- **NX_MDNS_POOF_TIME_COUNT** Bu sorgulardan iki ya da daha fazla kez ve beklenen yanıtı içeren çok noktaya yayın yanıtı gördükten sonra, zaman aralığı içindeki zaman aralığı. Varsayılan değer 10 saniye için 1000 ticks değeridir.
- **NX_MDNS_RR_DELETE_DELAY_TIMER_COUNT** Kaynak kaydını silme gecikmesi bu kaydın TTL değeri sıfır olduğunda, 1 saniye boyunca varsayılan değer 100 ticks değeridir.
