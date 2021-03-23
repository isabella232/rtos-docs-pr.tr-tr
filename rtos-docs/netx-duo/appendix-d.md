---
title: Ek D-Azure RTOS NetX Duo BSD-Compatible yuva API 'SI
description: IPv4 ve IPv6 için BSD-Compatible yuva API 'SI hakkında bilgi edinin.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 82439184d9facb6ddcc08ce81bc51182d7f34429
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826231"
---
# <a name="appendix-d---azure-rtos-netx-duo-bsd-compatible-socket-api"></a>Ek D-Azure RTOS NetX Duo BSD-Compatible yuva API 'SI

## <a name="bsd-compatible-socket-api"></a>BSD-Compatible yuva API 'SI 
BSD-Compatible yuva API 'si, altında NetX Duo temel sürümlerini kullanarak BSD yuvaları API çağrılarının (bazı sınırlamalara sahip) bir alt kümesini destekler &reg; . Hem IPv6 hem de IPv4 protokolleri ve ağ adresleme desteklenir. Bu API iç NetX Duo temel öğelerini kullandığından ve gereksiz NetX hata denetimini atladığı için bu BSD-Compatible yuvaları API katmanı tipik BSD uygulamalarından hızlı veya biraz daha hızlı bir şekilde gerçekleştirilmelidir.  

Yapılandırılabilir seçenekler, ana bilgisayar uygulamasının en fazla yuva sayısını, TCP maksimum pencere boyutunu ve dinleme kuyruğunun derinliğini tanımlamasını sağlar.

Performans ve mimari kısıtlamalarından dolayı, bu BSD-Compatible Sockets API 'SI tüm BSD yuvaları çağrılarını desteklemez. Bunlara ek olarak, BSD Hizmetleri için tüm BSD seçenekleri yoktur, özellikle aşağıdakiler aşağıda verilmiştir:

  - ***_ Call** komutunu yalnızca fd_set \_ readfds ile birlikte çalışarak bu çağrıdaki diğer bağımsız değişkenler (örneğin, writefds, hariç tutulan tfds) desteklenmez.
  - "İnt Flags" bağımsız değişkeni ***Send** _*__, alma_*_, _*_SendTo_*_ ve _ *_recvfrom_** çağrılarında desteklenmez. 
  - BSD-Compatible Socket API 'SI yalnızca sınırlı sayıda BSD yuvası çağrısı kümesini destekler.

Kaynak kodu basitlik için tasarlanmıştır ve yalnızca iki dosyadan oluşur, ***nxd_bsd. c** _ ve _*_nxd_bsd. h_*_. Yükleme, bu iki dosyayı derleme projesine (NetX kitaplığı değil) eklemeyi ve BSD yuvası hizmeti çağrılarını kullanacak konak uygulamasını oluşturmayı gerektirir. _ *_Nxd_bsd. h_** dosyası da uygulama kaynağınıza dahil olmalıdır. Hem IPv4 hem de IPv6 tabanlı uygulamalar için örnek Tanıtım dosyaları, NetX Duo ile ücretsiz kullanıma sunulan dağıtıma dahildir. Ek ayrıntılar, BSDCompatible yuva API paketiyle birlikte gelen yardım ve Benioku dosyalarında bulunabilir.

BSD-Compatible Sockets API 'si aşağıdaki BSD yuvaları API çağrılarını destekler:

```c
INT     bsd_initialize (NX_IP *default_ip, NX_PACKET_POOL *default_pool, CHAR
        *bsd_memory_not_used);
```
```c
INT     getpeername( INT sockID, struct sockaddr *remoteAddress, INT
        *addressLength);
```
```c
INT     getsockname( INT sockID, struct sockaddr *localAddress, INT *addressLength);
```
```c
INT     recvfrom(INT sockID, CHAR *buffer, INT buffersize, INT flags,struct sockaddr
        *fromAddr, INT *fromAddrLen);
```
```c        
INT     recv(INT sockID, VOID *rcvBuffer, INT bufferLength, INT flags);
```
```c
INT     sendto(INT sockID, CHAR *msg, INT msgLength, INT flags, struct sockaddr
        *destAddr, INT destAddrLen);
```
```c        
INT     send(INT sockID, const CHAR *msg, INT msgLength, INT flags);
```
```c
INT     accept(INT sockID, struct sockaddr *ClientAddress, INT *addressLength);
```
```c
INT     listen(INT sockID, INT backlog);
```
```c
INT     bind (INT sockID, struct sockaddr *localAddress, INT addressLength);
```
```c
INT     connect(INT sockID, struct sockaddr *remoteAddress, INT addressLength);
```
```c
INT     socket( INT protocolFamily, INT type, INT protocol);
```
```c
INT     soc_close ( INT sockID);
```
```c
INT     select(INT nfds, fd_set *readfds, fd_set *writefds, fd_set *exceptfds, struct
        timeval *timeout);
```
```c
VOID    FD_SET(INT fd, fd_set *fdset);
```
```c
VOID    FD_CLR(INT fd, fd_set *fdset);
```
```c
INT     FD_ISSET(INT fd, fd_set *fdset);
```
```c
VOID    FD_ZERO(fd_set *fdset);
```