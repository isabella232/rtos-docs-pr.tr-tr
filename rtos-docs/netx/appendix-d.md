---
title: Ek D-Azure RTOS NetX BSD-Compatible yuva API 'SI
description: IPv4 için BSD-Compatible yuva API 'SI hakkında bilgi edinin.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 9062e27d8f447ac8d36e7a09afee5ac14f86f8c3
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826897"
---
# <a name="appendix-d---azure-rtos-netx-bsd-compatible-socket-api"></a>Ek D-Azure RTOS NetX BSD-Compatible yuva API 'SI

## <a name="bsd-compatible-socket-api"></a>BSD-Compatible yuva API 'SI

BSD-Compatible yuva API 'si, aşağıda Azure RTOS NetX temel sürümlerini kullanarak BSD yuvaları API çağrılarının (bazı sınırlamalara sahip) bir alt kümesini destekler. IPv4 protokolleri ve ağ adresleme desteklenir. Bu API iç NetX temel öğelerini kullandığından ve gereksiz NetX hata denetimini atladığı için bu BSD-Compatible yuvaları API katmanı tipik BSD uygulamalarından hızlı veya biraz daha hızlı bir şekilde gerçekleştirilmelidir.

Yapılandırılabilir seçenekler, ana bilgisayar uygulamasının en fazla yuva sayısını, TCP maksimum pencere boyutunu ve dinleme kuyruğunun derinliğini tanımlamasını sağlar.

Performans ve mimari kısıtlamalarından dolayı, bu BSD-Compatible Sockets API 'SI tüm BSD yuvaları çağrılarını desteklemez. Bunlara ek olarak, BSD Hizmetleri için tüm BSD seçenekleri yoktur, özellikle aşağıdakiler aşağıda verilmiştir:

- ***Select** _ işlevi yalnızca _fd_set \* readfds * ile çalışır, bu çağrıdaki diğer bağımsız değişkenler (örneğin, *writefds*, *hariç tutulan tfds* ) desteklenmez.
- *İnt Flags* bağımsız değişkeni ***Send** _*__, alma_*_, _*_SendTo_*_ ve _ *_recvfrom_** işlevleri için desteklenmez. BSD-Compatible Socket API 'SI yalnızca sınırlı sayıda BSD yuvası çağrısı kümesini destekler.

Kaynak kodu basitlik için tasarlanmıştır ve yalnızca iki dosyadan oluşur, ***nx_bsd. c** _ ve _*_nx_bsd. h_*_. Yükleme, bu iki dosyayı derleme projesine (NetX kitaplığı değil) eklemeyi ve BSD yuvası hizmeti çağrılarını kullanacak konak uygulamasını oluşturmayı gerektirir. _ *_Nx_bsd. h_** dosyası da uygulama kaynağınıza dahil olmalıdır. Örnek demo dosyaları, NetX ile ücretsiz olarak kullanılabilen dağıtıma dahildir. Daha fazla ayrıntı, yardım BSD-Compatible yuva API **417** ve benioku dosyalarında BSD-Compatible soket API paketiyle birlikte sağlanır.

BSD-Compatible Sockets API 'si aşağıdaki BSD yuvaları API çağrılarını destekler:

```C
*INT bsd_initialize (NX_IP *default_ip, NX_PACKET_POOL *default_pool,
    CHAR *bsd_memory_not_used);*

*INT getpeername( INT sockID, struct sockaddr *remoteAddress, INT *addressLength);*

*INT getsockname( INT sockID, struct sockaddr *localAddress, INT *addressLength);*

*INT recvfrom(INT sockID, CHAR *buffer, INT buffersize,
    INT flags,struct sockaddr *fromAddr, INT *fromAddrLen);*

*INT recv(INT sockID, VOID *rcvBuffer, INT bufferLength, INT flags);*

*INT sendto(INT sockID, CHAR *msg, INT msgLength, INT flags,
    struct sockaddr *destAddr, INT destAddrLen);*

*INT send(INT sockID, const CHAR *msg, INT msgLength, INT flags);*

 *INT accept(INT sockID, struct sockaddr *ClientAddress, INT *addressLength);*

*INT listen(INT sockID, INT backlog);*

*INT bind (INT sockID, struct sockaddr *localAddress, INT addressLength);*

*INT connect(INT sockID, struct sockaddr *remoteAddress, INT addressLength);*

*INT socket( INT protocolFamily, INT type, INT protocol);*

*INT soc_close ( INT sockID);*

*INT select(INT nfds, fd_set *readfds, fd_set *writefds,
    fd_set *exceptfds, struct timeval *timeout);*

*VOID FD_SET(INT fd, fd_set *fdset);*

*VOID FD_CLR(INT fd, fd_set *fdset);*

*INT FD_ISSET(INT fd, fd_set *fdset);*

*VOID FD_ZERO(fd_set *fdset);*

```
