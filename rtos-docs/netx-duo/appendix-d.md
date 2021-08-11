---
title: Ek D - Azure RTOS NetX Duo BSD-Compatible Yuva API'si
description: IPv4 ve IPv6 BSD-Compatible Yuva API'si hakkında bilgi edinin.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: cd43c3efa18dd76f6eb996c84091024f48ad65aa5839958066161080dc02127e
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116789757"
---
# <a name="appendix-d---azure-rtos-netx-duo-bsd-compatible-socket-api"></a>Ek D - Azure RTOS NetX Duo BSD-Compatible Yuva API'si

## <a name="bsd-compatible-socket-api"></a>BSD-Compatible Yuvası API'si 
BSD-Compatible Yuva API'si, altında NetX Duo temellerini kullanarak BSD YuvaLARı API çağrılarının bir alt kümesini (bazı sınırlamalarla birlikte) &reg; destekler. Hem IPv6 hem de IPv4 protokolleri ve ağ adresle desteği vardır. Bu BSD-Compatible Yuva API'si katmanı tipik BSD uygulamalarına göre daha hızlı veya biraz daha hızlı çalışmalı çünkü bu API iç NetX Duo temel elemanları kullanır ve gereksiz NetX hata denetimlerini atlar.  

Yapılandırılabilir seçenekler konak uygulamanın en fazla yuva sayısını, TCP maksimum pencere boyutunu ve dinleme kuyruğu derinliğini tanımlamasına olanak sağlar.

Performans ve mimari kısıtlamaları nedeniyle, bu BSD-Compatible Yuva API'si tüm BSD Yuva çağrılarını desteklemez. Ayrıca, BSD hizmetleri için tüm BSD seçenekleri mevcut değildir, özellikle de şunlardır:

  - ***select** _ call yalnızca readfds fd_set çalışır, bu çağrıda diğer bağımsız değişkenler \_ (writefds gibi) ancakfds desteklenmiyor.
  - ***send** _, _*_recv,_*_ _*_sendto_*_ ve _ *_recvfrom_** çağrıları için "int flags" bağımsız değişkeni desteklenmiyor. 
  - BSD-Compatible Yuvası API'si yalnızca sınırlı sayıda BSD Yuva çağrısını destekler.

Kaynak kodu basitlik için tasarlanmıştır ve yalnızca iki dosyadan oluşur: ***nxd_bsd.c** _ _*_ve nxd_bsd.h_*_. Yükleme, bu iki dosyanın derleme projesine (NetX kitaplığına değil) eklerini ve BSD Yuva hizmeti çağrılarını kullanan konak uygulamasını oluşturmayı gerektirir. _ *_nxd_bsd.h_** dosyasının da uygulama kaynağınıza dahil olması gerekir. NetX Duo ile ücretsiz olarak kullanılabilen dağıtıma hem IPv4 hem de IPv6 tabanlı uygulamalar için örnek tanıtım dosyaları dahildir. BSD Uyumsuz Yuva API'si paketiyle birlikte gelen yardım ve Beni Oku dosyalarında daha fazla ayrıntı mevcuttur.

BSD-Compatible Yuvaları API'si aşağıdaki BSD Yuva API çağrılarını destekler:

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