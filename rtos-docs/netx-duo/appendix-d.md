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
# <a name="appendix-d---azure-rtos-netx-duo-bsd-compatible-socket-api"></a><span data-ttu-id="48c15-103">Ek D-Azure RTOS NetX Duo BSD-Compatible yuva API 'SI</span><span class="sxs-lookup"><span data-stu-id="48c15-103">Appendix D - Azure RTOS NetX Duo BSD-Compatible Socket API</span></span>

## <a name="bsd-compatible-socket-api"></a><span data-ttu-id="48c15-104">BSD-Compatible yuva API 'SI</span><span class="sxs-lookup"><span data-stu-id="48c15-104">BSD-Compatible Socket API</span></span> 
<span data-ttu-id="48c15-105">BSD-Compatible yuva API 'si, altında NetX Duo temel sürümlerini kullanarak BSD yuvaları API çağrılarının (bazı sınırlamalara sahip) bir alt kümesini destekler &reg; .</span><span class="sxs-lookup"><span data-stu-id="48c15-105">The BSD-Compatible Socket API supports a subset of the BSD Sockets API calls (with some limitations) by utilizing NetX Duo&reg; primitives underneath.</span></span> <span data-ttu-id="48c15-106">Hem IPv6 hem de IPv4 protokolleri ve ağ adresleme desteklenir.</span><span class="sxs-lookup"><span data-stu-id="48c15-106">Both IPv6 and IPv4 protocols and network addressing are supported.</span></span> <span data-ttu-id="48c15-107">Bu API iç NetX Duo temel öğelerini kullandığından ve gereksiz NetX hata denetimini atladığı için bu BSD-Compatible yuvaları API katmanı tipik BSD uygulamalarından hızlı veya biraz daha hızlı bir şekilde gerçekleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="48c15-107">This BSD-Compatible Sockets API layer should perform as fast or slightly faster than typical BSD implementations because this API utilizes internal NetX Duo primitives and bypasses unnecessary NetX error checking.</span></span>  

<span data-ttu-id="48c15-108">Yapılandırılabilir seçenekler, ana bilgisayar uygulamasının en fazla yuva sayısını, TCP maksimum pencere boyutunu ve dinleme kuyruğunun derinliğini tanımlamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="48c15-108">Configurable options allow the host application to define the maximum number of sockets, TCP maximum window size, and depth of listen queue.</span></span>

<span data-ttu-id="48c15-109">Performans ve mimari kısıtlamalarından dolayı, bu BSD-Compatible Sockets API 'SI tüm BSD yuvaları çağrılarını desteklemez.</span><span class="sxs-lookup"><span data-stu-id="48c15-109">Due to performance and architecture constraints, this BSD-Compatible Sockets API does not support all BSD Sockets calls.</span></span> <span data-ttu-id="48c15-110">Bunlara ek olarak, BSD Hizmetleri için tüm BSD seçenekleri yoktur, özellikle aşağıdakiler aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="48c15-110">In addition, not all BSD options are available for the BSD services, specifically the following:</span></span>

  - <span data-ttu-id="48c15-111">\***_ Call** komutunu yalnızca fd_set \_ readfds ile birlikte çalışarak bu çağrıdaki diğer bağımsız değişkenler (örneğin, writefds, hariç tutulan tfds) desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="48c15-111">\***select** _ call works with only fd_set \_readfds, other arguments in this call e.g., writefds, exceptfds are not supported.</span></span>
  - <span data-ttu-id="48c15-112">"İnt Flags" bağımsız değişkeni ***Send** _*__, alma_\*_, _*_SendTo_*_ ve _ *_recvfrom_*\* çağrılarında desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="48c15-112">The "int flags" argument is not supported for ***send** _, _*_recv_*_, _*_sendto,_*_ and _ *_recvfrom_** calls.</span></span> 
  - <span data-ttu-id="48c15-113">BSD-Compatible Socket API 'SI yalnızca sınırlı sayıda BSD yuvası çağrısı kümesini destekler.</span><span class="sxs-lookup"><span data-stu-id="48c15-113">The BSD-Compatible Socket API supports only limited set of BSD Sockets calls.</span></span>

<span data-ttu-id="48c15-114">Kaynak kodu basitlik için tasarlanmıştır ve yalnızca iki dosyadan oluşur, ***nxd_bsd. c** _ ve _*_nxd_bsd. h_\*_.</span><span class="sxs-lookup"><span data-stu-id="48c15-114">The source code is designed for simplicity and is comprised of only two files, ***nxd_bsd.c** _ and _*_nxd_bsd.h_\*_.</span></span> <span data-ttu-id="48c15-115">Yükleme, bu iki dosyayı derleme projesine (NetX kitaplığı değil) eklemeyi ve BSD yuvası hizmeti çağrılarını kullanacak konak uygulamasını oluşturmayı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="48c15-115">Installation requires adding these two files to the build project (not the NetX library) and creating the host application which will use BSD Socket service calls.</span></span> <span data-ttu-id="48c15-116">_ *_Nxd_bsd. h_*\* dosyası da uygulama kaynağınıza dahil olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="48c15-116">The _ *_nxd_bsd.h_*\* file must also be included in your application source.</span></span> <span data-ttu-id="48c15-117">Hem IPv4 hem de IPv6 tabanlı uygulamalar için örnek Tanıtım dosyaları, NetX Duo ile ücretsiz kullanıma sunulan dağıtıma dahildir.</span><span class="sxs-lookup"><span data-stu-id="48c15-117">Sample demo files for both IPv4 and IPv6  based applications are included with the distribution which is freely available with NetX Duo.</span></span> <span data-ttu-id="48c15-118">Ek ayrıntılar, BSDCompatible yuva API paketiyle birlikte gelen yardım ve Benioku dosyalarında bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="48c15-118">Further details are available in the help and Readme files bundled with the BSDCompatible Socket API package.</span></span>

<span data-ttu-id="48c15-119">BSD-Compatible Sockets API 'si aşağıdaki BSD yuvaları API çağrılarını destekler:</span><span class="sxs-lookup"><span data-stu-id="48c15-119">The BSD-Compatible Sockets API supports the following BSD Sockets API calls:</span></span>

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