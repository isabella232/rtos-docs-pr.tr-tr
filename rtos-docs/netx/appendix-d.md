---
title: Ek D - Azure RTOS NetX BSD-Compatible Yuva API'si
description: IPv4 için BSD-Compatible Yuva API'si hakkında bilgi edinin.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: bd4a35c19cd794a5135f01abe5595456d39b5306ba25ce2966c3bb1aea14ea17
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116790097"
---
# <a name="appendix-d---azure-rtos-netx-bsd-compatible-socket-api"></a>Ek D - Azure RTOS NetX BSD-Compatible Yuva API'si

## <a name="bsd-compatible-socket-api"></a>BSD-Compatible Yuvası API'si

BSD-Compatible Yuva API'si, temel NetX temellerini kullanarak BSD YuvaLARı API çağrılarının bir alt kümesini (bazı sınırlamalarla) Azure RTOS destekler. IPv4 protokolleri ve ağ adresi desteği vardır. Bu BSD-Compatible Yuva API'si katmanı, iç NetX temel elemanlarını kullanır ve gereksiz NetX hata denetimlerini atlar.

Yapılandırılabilir seçenekler konak uygulamanın en fazla yuva sayısını, TCP maksimum pencere boyutunu ve dinleme kuyruğu derinliğini tanımlamasına olanak sağlar.

Performans ve mimari kısıtlamaları nedeniyle, bu BSD-Compatible Yuva API'si tüm BSD Yuva çağrılarını desteklemez. Ayrıca, BSD hizmetleri için tüm BSD seçenekleri mevcut değildir, özellikle de şunlardır:

- ***select** _ işlevi yalnızca _fd_set readfds* ile çalışır; bu çağrıda writefds gibi diğer bağımsız değişkenler \* *(örneğin,* *writefds*) desteklenmiyor.
- *Int flags* bağımsız değişkeni ***send** _, _*_recv,_*_ _*_sendto_*_ ve _ *_recvfrom_** işlevleri için desteklenmiyor. BSD-Compatible Yuvası API'si yalnızca sınırlı sayıda BSD Yuva çağrısını destekler.

Kaynak kodu basitlik için tasarlanmıştır ve yalnızca iki dosyadan oluşur,***nx_bsd.c** _ _*_ve nx_bsd.h_*_. Yükleme, bu iki dosyanın derleme projesine (NetX kitaplığına değil) eklerini ve BSD Yuva hizmeti çağrılarını kullanan konak uygulamasını oluşturmayı gerektirir. _ *_nx_bsd.h_** dosyasının da uygulama kaynağınıza dahil olması gerekir. Örnek tanıtım dosyaları, NetX ile ücretsiz olarak kullanılabilen dağıtıma dahil edilir. Yuva **API'si 417** BSD-Compatible Ve Beni Oku dosyaları, Yuva API'si paketiyle birlikte BSD-Compatible yardım içinde mevcuttur.

BSD-Compatible Yuvaları API'si aşağıdaki BSD Yuva API çağrılarını destekler:

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
