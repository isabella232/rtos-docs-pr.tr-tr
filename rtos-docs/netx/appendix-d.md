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
# <a name="appendix-d---azure-rtos-netx-bsd-compatible-socket-api"></a><span data-ttu-id="2f751-103">Ek D-Azure RTOS NetX BSD-Compatible yuva API 'SI</span><span class="sxs-lookup"><span data-stu-id="2f751-103">Appendix D - Azure RTOS NetX BSD-Compatible Socket API</span></span>

## <a name="bsd-compatible-socket-api"></a><span data-ttu-id="2f751-104">BSD-Compatible yuva API 'SI</span><span class="sxs-lookup"><span data-stu-id="2f751-104">BSD-Compatible Socket API</span></span>

<span data-ttu-id="2f751-105">BSD-Compatible yuva API 'si, aşağıda Azure RTOS NetX temel sürümlerini kullanarak BSD yuvaları API çağrılarının (bazı sınırlamalara sahip) bir alt kümesini destekler.</span><span class="sxs-lookup"><span data-stu-id="2f751-105">The BSD-Compatible Socket API supports a subset of the BSD Sockets API calls (with some limitations) by utilizing Azure RTOS NetX primitives underneath.</span></span> <span data-ttu-id="2f751-106">IPv4 protokolleri ve ağ adresleme desteklenir.</span><span class="sxs-lookup"><span data-stu-id="2f751-106">IPv4 protocols and network addressing are supported.</span></span> <span data-ttu-id="2f751-107">Bu API iç NetX temel öğelerini kullandığından ve gereksiz NetX hata denetimini atladığı için bu BSD-Compatible yuvaları API katmanı tipik BSD uygulamalarından hızlı veya biraz daha hızlı bir şekilde gerçekleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="2f751-107">This BSD-Compatible Sockets API layer should perform as fast or slightly faster than typical BSD implementations because this API utilizes internal NetX primitives and bypasses unnecessary NetX error checking.</span></span>

<span data-ttu-id="2f751-108">Yapılandırılabilir seçenekler, ana bilgisayar uygulamasının en fazla yuva sayısını, TCP maksimum pencere boyutunu ve dinleme kuyruğunun derinliğini tanımlamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="2f751-108">Configurable options allow the host application to define the maximum number of sockets, TCP maximum window size, and depth of listen queue.</span></span>

<span data-ttu-id="2f751-109">Performans ve mimari kısıtlamalarından dolayı, bu BSD-Compatible Sockets API 'SI tüm BSD yuvaları çağrılarını desteklemez.</span><span class="sxs-lookup"><span data-stu-id="2f751-109">Due to performance and architecture constraints, this BSD-Compatible Sockets API does not support all BSD Sockets calls.</span></span> <span data-ttu-id="2f751-110">Bunlara ek olarak, BSD Hizmetleri için tüm BSD seçenekleri yoktur, özellikle aşağıdakiler aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="2f751-110">In addition, not all BSD options are available for the BSD services, specifically the following:</span></span>

- <span data-ttu-id="2f751-111">\***Select** _ işlevi yalnızca _fd_set \* readfds \* ile çalışır, bu çağrıdaki diğer bağımsız değişkenler (örneğin, *writefds*, *hariç tutulan tfds* ) desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="2f751-111">The ***select** _ function works with only _fd_set \*readfds*, other arguments in this call e.g., *writefds*, *exceptfds* are not supported.</span></span>
- <span data-ttu-id="2f751-112">*İnt Flags* bağımsız değişkeni ***Send** _*__, alma_\*_, _*_SendTo_*_ ve _ *_recvfrom_*\* işlevleri için desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="2f751-112">The *int flags* argument is not supported for the ***send** _, _*_recv_*_, _*_sendto,_*_ and _ *_recvfrom_** functions.</span></span> <span data-ttu-id="2f751-113">BSD-Compatible Socket API 'SI yalnızca sınırlı sayıda BSD yuvası çağrısı kümesini destekler.</span><span class="sxs-lookup"><span data-stu-id="2f751-113">The BSD-Compatible Socket API supports only limited set of BSD Sockets calls.</span></span>

<span data-ttu-id="2f751-114">Kaynak kodu basitlik için tasarlanmıştır ve yalnızca iki dosyadan oluşur, ***nx_bsd. c** _ ve _*_nx_bsd. h_\*_.</span><span class="sxs-lookup"><span data-stu-id="2f751-114">The source code is designed for simplicity and is comprised of only two files,***nx_bsd.c** _ and _*_nx_bsd.h_\*_.</span></span> <span data-ttu-id="2f751-115">Yükleme, bu iki dosyayı derleme projesine (NetX kitaplığı değil) eklemeyi ve BSD yuvası hizmeti çağrılarını kullanacak konak uygulamasını oluşturmayı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="2f751-115">Installation requires adding these two files to the build project (not the NetX library) and creating the host application which will use BSD Socket service calls.</span></span> <span data-ttu-id="2f751-116">_ *_Nx_bsd. h_*\* dosyası da uygulama kaynağınıza dahil olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="2f751-116">The _ *_nx_bsd.h_*\* file must also be included in your application source.</span></span> <span data-ttu-id="2f751-117">Örnek demo dosyaları, NetX ile ücretsiz olarak kullanılabilen dağıtıma dahildir.</span><span class="sxs-lookup"><span data-stu-id="2f751-117">Sample demo files are included with the distribution which is freely available with NetX.</span></span> <span data-ttu-id="2f751-118">Daha fazla ayrıntı, yardım BSD-Compatible yuva API **417** ve benioku dosyalarında BSD-Compatible soket API paketiyle birlikte sağlanır.</span><span class="sxs-lookup"><span data-stu-id="2f751-118">Further details are available in the help BSD-Compatible Socket API **417** and Readme files bundled with the BSD-Compatible Socket API package.</span></span>

<span data-ttu-id="2f751-119">BSD-Compatible Sockets API 'si aşağıdaki BSD yuvaları API çağrılarını destekler:</span><span class="sxs-lookup"><span data-stu-id="2f751-119">The BSD-Compatible Sockets API supports the following BSD Sockets API calls:</span></span>

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
