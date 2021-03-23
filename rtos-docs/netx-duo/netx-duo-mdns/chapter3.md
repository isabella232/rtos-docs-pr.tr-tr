---
title: Bölüm 3-iç hizmet önbelleğinin açıklaması
description: 'NetX Duo mDNS modülü iki iç hizmet önbelleğini yönetir: yerel hizmet önbelleği ve eş hizmet önbelleği.'
author: philmea
ms.author: philmea
ms.date: 07/09/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 007f1080a076730cfbcdedc9f063ac0c427a414c
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825913"
---
# <a name="chapter-3---description-of-internal-service-cache"></a>Bölüm 3-iç hizmet önbelleğinin açıklaması

NetX Duo mDNS modülü iki iç hizmet önbelleğini yönetir: yerel hizmet önbelleği ve eş hizmet önbelleği. Yerel hizmet önbelleği, düğümde çalışan uygulamalar tarafından sunulan hizmetlerle ilgili kaynak kayıtlarını depolar. Gelen sorgular için, söz konusu hizmet sunulan hizmetle eşleşiyorsa, yerel hizmet önbelleğinde depolanan yanıtları içeren mDNS yanıtları. Uygulamalar, API *nx_mdns_service_add ()* çağırarak Hizmetleri kaydeder. Hizmetleri kaldırmak için uygulamalar, yerel hizmet önbelleğindeki karşılık gelen girdileri kaldırmadan önce "güle" iletileri gönderecek olan API *nx_mdns_service_delete ()* kullanır.

Bir hizmet eklendiğinde, mDNS yerel hizmet önbelleğinde en az 3 kaynak kaydı tutar: SRV, PTR ve TXT. Hizmet türü alt tür içeriyorsa ek PTR kaynak kaydı eklenebilir. Örneğin, bir uygulama bir hizmeti kaydeder:

```
*name*._*subtype*._sub._*type*._tcp.local,
```

için bir tane olmak üzere yerel hizmet önbelleğine iki PTR kaynak kaydı eklenir

```
“*_subtype._*sub*._type._*tcp.local *PTR name.type._*tcp*.*local”
```

ve diğeri

```
*“_type._*tcp*.*local *PTR name.type._*tcp*.*local”.
```

Eş hizmeti önbelleği, komşu düğümlerden alınan mDNS kaynak kayıtlarını içerir. mDNS modülü, ağdaki diğer düğümlerin tanıtıldığı kaynak kayıtlarını toplar ve alınan bilgileri eş hizmeti önbelleğinde depolar. Uygulama, ana bilgisayar IPv4 veya IPv6 adresleri gibi bilgiler için sorguladığında, mDNS yerel olarak önbelleğe alınan yanıtlar için eş hizmeti önbelleğinde arama yapar. Uygulamalar, eşler tarafından sunulan hizmetler için sorguladığında, mDNS ilgili PTR, SRV, TXT ve IPv4/IPv6 adres kayıtları için önbelleği arar. Eş hizmeti önbelleği, düğüme gönderilen sorguları da depolar. Örneğin, bir uygulama nx_mdns_service_one_shot_query çağırarak belirli bir hizmet talep edebilir *.* Hizmet eş hizmeti önbelleğinde bulunamazsa, mDNS, eş hizmeti önbelleğinde sorgu soruları (PTR, SRV ve TXT) oluşturur. Bu sorgu soruları, hizmet çözümlenene veya zaman aşımına uğrayana düzenli olarak ağa gönderilir. Benzer şekilde, uygulama, uzun bir süre boyunca belirli bir hizmeti istemek için API *nx_mdns_service_continous_query ()* kullanabilir (uygulama, API *nx_mdns_service_query_stop ()* ) kullanarak daha önce verilen bir sürekli sorguyu iptal eder. Ağa sorgu göndermeden, eş hizmeti önbelleğinde belirli bir hizmeti aramak için, uygulamalar API *nx_mdns_serivce_lookup () kullanabilir.* Bu API yalnızca eş hizmet önbelleğindeki kaynak kayıtlarını arar.

Her kaynak kaydı, hizmet önbelleklerindeki *NX_MDNS_RR* bir veri yapısında depolanır. Kaynak kayıtlarındaki dizeler değişken uzunluktadır, bu nedenle *NX_MDNS_RR* yapısında depolanmaz. Kaynak kaydı, dizenin depolandığı gerçek bellek konumuna yönelik bir işaretçi içerir. Dize tablosu ve kaynak kayıtları, hizmet önbelleğini paylaşır. Kaynak kayıtları, hizmet önbelleğinin başından itibaren depolanır ve önbelleğin sonuna doğru artar. Dize tablosu, hizmet önbelleğinin sonundan başlar ve önbelleğin başına doğru büyür. Dize tablosundaki her bir dizenin bir uzunluk alanı ve bir sayaç alanı vardır. Dize tablosuna bir dize eklendiğinde, tabloda aynı dize zaten varsa, sayaç değeri artırılır ve dize için bellek ayrılmaz. Hizmet önbelleğine daha fazla kaynak kaydı veya yeni dize eklenebileceği takdirde hizmet önbelleği tam olarak değerlendirilir.

Bir uygulamanın yerel ağda sunulan hizmetleri bulmanın iki yolu vardır. Belirli bir hizmeti tek kararlı bir sorgu aracılığıyla arayabilir ya da ağdaki etkinlikleri "izlemek" üzere sürekli bir sorgu başlatabilir. Tek kısa sorgu senaryosunda, uygulamanın hizmet türünü belirtmesi gerekir. mDNS yerel hizmet önbelleğinde ve eş hizmeti önbelleğinde arama yapar. Bir hizmet örneği bulunursa, tek çizgili sorgu kaynak kayıtlarında bulunan bilgilerle birlikte döndürülür. Yerel hizmet önbelleğinde veya eş hizmeti önbelleğinde bir kayıt yoksa, mDNS sorgu iletilerini gönderir. Örnek adı belirtilmişse, "ad. Type. Local" biçiminde belirli bir örnek adına sahip *herhangi* bir tür (SRV ve txt türü sorgula) yerel ağa gönderilir. Örnek adı belirtilmemişse, yerel ağa bir PTR türü sorgu gönderilir. Alınan ilk tamamlanmış hizmet çağırana döndürülür.

Sürekli sorgu farklı şekilde çalışır. Sürekli bir sorgu için tipik kullanım örneği, belirli bir hizmet için yerel ağı (örneğin, yerel ağdaki yazdırma hizmetlerini sürekli olarak aramak için) izbilmenizdir. Bu durumda, uygulama belirli türde hizmetler için bir arama sorgusu (API *nx_mdns_service_continious_* sorgusu aracılığıyla) yayınlar. Çağıran, genellikle belirli bir yanıt beklemez. Sürekli sorgu olarak gönderilen sorgular için, mDNS modülü sorguları, üstel olarak artan aralıklar ile düzenli aralıklarla iletir. Sorguyu durdurmak için, uygulamanın bu sorgularda iç zamanlayıcıyı durdurmak üzere API *nx_mdns_service_query_stop* kullanması gerekir. Sorgu türü NULL olabilir, bu durumda sorgu türü özel PTR türü "_services. _DNS-SD. _udp. Local" olarak ayarlanır. Bu hizmet türü, mDNS tarafından yerel ağda bulunan tüm hizmetleri keşfetmenin bir yolu olarak tanımlanır. Örnek adı belirtilmişse, yerel ağa "Name. Type. Local" adlı belirli örnek adına sahip HERHANGI bir tür (SRV ve TXT türü sorgula) gönderilir. Örnek adı NULL ise, yerel ağa bir PTR türü sorgu gönderilir.

İstenmeyen sorgulardan gelen yanıtlar da dahil olmak üzere tüm yanıtlar, eşdüzey hizmet önbelleğine kaydedilir. Daha sonra uygulama, eş hizmet önbelleğinden belirli bir hizmeti almak için API *nx_mdns_service_lookup* kullanır.

Parçalanmaya yönelik özel Not: her *NX_MDNS_RR* yapısı boyut olarak sabitlenmiştir ve bu nedenle MDNs RR 'leri ekleyip sildiğinden parçalanmaya tabi değildir. Ancak dizeler değişken uzunluktadır. Bir dize silindikten sonra, alan kullanılabilir hale gelir ve yeni dize sığmayacak kadar yeni bir dize için kullanılabilir. Ancak bu işlem belleğin parçaya neden olur. Hizmetler eklenip kaldırıldıkça, dize tablosu, hizmet önbelleğinde dize için yeterli kullanılmamış bayt içermese de, yeni dizelerin eklenemeyeceği noktaya parçalanabilir. Yerel uygulamalar daha kararlı ve öngörülebilir olmaya eğilimlidir. Bu nedenle, yerel hizmet önbelleği parçalanmayı daha az olabilir. Eş hizmet önbelleği, diğer taraftan, hizmetler kullanılabilir hale geldiğinde sürekli olarak RR 'Ler ekleyin veya hizmetler ağdaki düğümler tarafından siliniyorsa RR 'Leri kaldırın. Ağ üzerindeki hizmetler, dize tablosunda daha sık ayırma/silme işlemlerine neden olur ve gider. Zaman içinde, dize tablosunun parçalanmış hale gelmesi olasıdır. Bu durum gerçekleştiğinde, bir basit çözüm tüm eşdüzey hizmet önbelleğinin temizlenmesi olur. Bu, API *nx_mdns_peer_cache_clear ()* çağırarak yapılabilir. Bu API 'nin bekleyen sürekli sorguları otomatik olarak sonlandırdığına unutmayın.
