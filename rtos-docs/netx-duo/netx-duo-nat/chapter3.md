---
title: Bölüm 3-NAT yapılandırma seçenekleri
description: Aşağıdaki listede, tüm seçenekler ve ayrıntılı olarak açıklanan işlevleri yer almaktadır
author: philmea
ms.author: philmea
ms.date: 07/14/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 8c7f2de88b5d70646284d946fdb6fbc743f08b3486430befb4fcda1d7e23e9b9
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116797304"
---
# <a name="chapter-3---nat-configuration-options"></a>Bölüm 3-NAT yapılandırma seçenekleri

NetX Duo NAT API 'SI için yapılandırılabilir seçenekler, *nx_nat. h* ' de ilk diğeri hariç bulunabilir, **NX_DISABLE_ERROR_CHECKING** *nx_nat. c* içinde bulunur. Aşağıdaki liste, ayrıntılı olarak açıklanan tüm seçenekleri ve işlevlerini içerir:

- **NX_NAT_DISABLE_ERROR_CHECKING** Tanımlanmışsa Bu seçenek, temel NAT hata denetimini kaldırır. Genellikle uygulamanın hata ayıklaması yapıldıktan sonra kullanılır. Varsayılan NetX Duo NAT durumu tanımlanmıştır (etkin).
- **NX_NAT_ENABLE_REPLACEMENT** Tanımlandıysa, NAT Önbelleği dolduğunda otomatik değiştirmeyi mümkün olursa bu seçenek.
  > [!NOTE]
  > Yalnızca TCP olmayan en eski oturumu değiştirin.
- **NX_NAT_MIN_ENTRY_COUNT** Bu seçenek, çeviri girişi için en düşük sayıyı ayarlar. Varsayılan sayı 3 ' dir.
- **NX_NAT_TCP_SESSION_TIMEOUT** Bu seçenek, TCP oturumlarının çeviri girişi için zaman aşımını ayarlar. Varsayılan zaman aşımı 24 saattir.
- **NX_NAT_NON_TCP_SESSION_TIMEOUT** Bu seçenek, TCP olmayan oturumlara yönelik çeviri girişi için zaman aşımını ayarlar. Varsayılan zaman aşımı 240 saniyedir.
- **NX_NAT_START_TCP_PORT** Bu seçenek, bir giden TCP paketini atamak üzere kullanılmayan bir TCP bağlantı noktasını bulmak için başlangıç değerini ayarlar. Varsayılan değer 20000 ' dir.
- **NX_NAT_END_TCP_PORT** Bu seçenek, TCP bağlantı noktası üst sınırını giden bir TCP paketini atamak üzere ayarlar. Varsayılan değer 30000 ' dir.
- **NX_NAT_START_UDP_PORT** Bu seçenek, bir giden UDP paketini atamak için kullanılmayan bir UDP bağlantı noktası bulmaya yönelik başlangıç değerini ayarlar. Varsayılan değer 20000 ' dir.
- **NX_NAT_END_UDP_PORT** Bu seçenek, UDP bağlantı noktası üst sınırını giden UDP paketi atanacak şekilde ayarlar. Varsayılan değer 30000 ' dir.
- **NX_NAT_START_ICMP_QUERY_ID** Bu seçenek, bir giden ıCMP sorgu paketi atamak için kullanılmamış bir sorgu KIMLIĞI bulmaya yönelik başlangıç değerini ayarlar. Varsayılan değer 20000 ' dir.
- **NX_NAT_END_ICMP_QUERY_ID** Bu seçenek, giden bir ıCMP sorgu paketi atamak için sorgu kimliklerinin üst sınırını ayarlar. Varsayılan değer 30000 ' dir.
