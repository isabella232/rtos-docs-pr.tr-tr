---
title: Bölüm 1-Azure RTOS NetX POP3 Istemcisine giriş
description: Azure RTOS NetX POP3 Istemcisi API 'SI, küçük iş istasyonlarının Istemci postasını almak için POP3 sunucularındaki Istemci mailkkkına erişmesi için bir posta aktarım sistemi sağlar.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 135530f11f8f54acd6d093a05332056dbdc32be3
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826669"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-pop3-client"></a><span data-ttu-id="21c2f-103">Bölüm 1-Azure RTOS NetX POP3 Istemcisine giriş</span><span class="sxs-lookup"><span data-stu-id="21c2f-103">Chapter 1 - Introduction to Azure RTOS NetX POP3 Client</span></span>

<span data-ttu-id="21c2f-104">Postane Protokolü sürüm 3 (POP3), küçük iş istasyonlarının Istemci postasını almak için POP3 sunucularındaki Istemci mailtirmelere erişmesi için bir posta aktarım sistemi sağlamak üzere tasarlanmış bir protokoldür.</span><span class="sxs-lookup"><span data-stu-id="21c2f-104">The Post Office Protocol Version 3 (POP3) is a protocol designed to provide a mail transport system for small workstations to access Client maildrops on POP3 Servers for retrieving Client mail.</span></span> <span data-ttu-id="21c2f-105">POP3, posta aktarımı gerçekleştirmek için Iletim Denetim Protokolü (TCP) hizmetlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="21c2f-105">POP3 utilizes Transmission Control Protocol (TCP) services to perform mail transfer.</span></span> <span data-ttu-id="21c2f-106">Bu nedenle, POP3 son derece güvenilir bir içerik aktarım protokolüdür.</span><span class="sxs-lookup"><span data-stu-id="21c2f-106">Because of this, POP3 is a highly reliable content transfer protocol.</span></span>

<span data-ttu-id="21c2f-107">Ancak POP3, posta işleme konusunda kapsamlı işlemler sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="21c2f-107">However, POP3 is does not provide extensive operations on mail handling.</span></span> <span data-ttu-id="21c2f-108">Genellikle, posta Istemci tarafından indirilir ve ardından sunucunun maildrop 'dan silinir.</span><span class="sxs-lookup"><span data-stu-id="21c2f-108">Typically, mail is downloaded by the Client and then deleted from the Server's maildrop.</span></span>

## <a name="netx-pop3-client-requirements"></a><span data-ttu-id="21c2f-109">NetX POP3 Istemci gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="21c2f-109">NetX POP3 Client Requirements</span></span>

### <a name="client-requirements"></a><span data-ttu-id="21c2f-110">İstemci gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="21c2f-110">Client Requirements</span></span>

<span data-ttu-id="21c2f-111">Azure RTOS NetX POP3 Istemcisi API 'SI, *nx_packet_pool_create* kullanarak daha önce oluşturulmuş bir NETX ıp örneği *nx_ip_create* ve daha önce oluşturulmuş bir NETX paket havuzu gerektirir.</span><span class="sxs-lookup"><span data-stu-id="21c2f-111">The Azure RTOS NetX POP3 Client API requires a previously created NetX IP instance using *nx_ip_create* and a previously created NetX packet pool using *nx_packet_pool_create*.</span></span> <span data-ttu-id="21c2f-112">NetX POP3 Istemcisi TCP hizmetlerini kullandığından, aynı IP örneğinde NetX POP3 Istemci hizmetlerini kullanmadan önce *nx_tcp_enable* çağrısıyla TCP 'nin etkinleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="21c2f-112">Because the NetX POP3 Client utilizes TCP services, TCP must be enabled with the *nx_tcp_enable* call prior to using the NetX POP3 Client services on that same IP instance.</span></span> <span data-ttu-id="21c2f-113">POP3 Istemcisi, sunucunun POP3 bağlantı noktasındaki bir POP3 sunucusuna bağlanmak için bir TCP yuvası kullanır.</span><span class="sxs-lookup"><span data-stu-id="21c2f-113">The POP3 Client uses a TCP socket to connect to a POP3 Server on the Server's POP3 port.</span></span> <span data-ttu-id="21c2f-114">Bu, tipik olarak *bilinen 110 numaralı bağlantı noktasında ayarlanır, ancak HIÇBIR POP3 istemcisi veya sunucusu bu bağlantı noktasını kullanmak zorunda değildir.*</span><span class="sxs-lookup"><span data-stu-id="21c2f-114">This is typically set at the *well-known port 110, though neither POP3 Client nor Server is required to use this port.*</span></span>

<span data-ttu-id="21c2f-115">POP3 Istemcisini oluştururken kullanılan paket havuzunun boyutu, paket yükü ve kullanılabilir paket sayısı bakımından Kullanıcı tarafından yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="21c2f-115">The size of the packet pool used in creating the POP3 Client is user configurable in terms of packet payload and number of packets available.</span></span> <span data-ttu-id="21c2f-116">Paket yalnızca POP3 Istemcisi oluştur hizmetinde kullanılıyorsa, paket yükünün Kullanıcı adı ve parola uzunluğuna veya APOP özetine bağlı olarak 100-120 bayttan fazla olmaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="21c2f-116">If the packet is used only in the POP3 Client create service, the packet payload need not be more than 100-120 bytes depending on the length of username and password, or APOP digest.</span></span> <span data-ttu-id="21c2f-117">Yerel konağın Kullanıcı adına sahip kullanıcı komutu, büyük olasılıkla POP3 Istemcisi tarafından gönderilen en büyük iletidir.</span><span class="sxs-lookup"><span data-stu-id="21c2f-117">The USER command with the local host's user name is probably the largest message sent by the POP3 Client.</span></span> <span data-ttu-id="21c2f-118">IP iç işlemleri TCP denetim verileri göndermek ve almak için çok büyük bir paket yükü gerektirmediğinden, nx_ip_create (IP varsayılan paket havuzunda) aynı paket havuzunu paylaşmak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="21c2f-118">It is possible to share the same packet pool in the nx_ip_create (IP default packet pool) since the IP internal operations do not require a very large packet payload for sending and receiving TCP control data.</span></span>

<span data-ttu-id="21c2f-119">Ancak, ağ sürücüsünün POP3 Istemci paket havuzuyla aynı paket havuzunu kullanması avantajlı olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="21c2f-119">However, it may not be advantageous for the network driver to use the same packet pool as the POP3 Client packet pool.</span></span> <span data-ttu-id="21c2f-120">Genellikle, paket havuzu yükünü al yükü, POP3 Istemci iletilerinden çok daha büyük olan ağ arabiriminin IP örneği MTU 'sunu (genellikle 1500 bayt) ayarlar.</span><span class="sxs-lookup"><span data-stu-id="21c2f-120">Generally, the payload of the receive packet pool payload is set the IP instance MTU (typically 1500 bytes) of the network interface which is much larger than POP3 Client messages.</span></span> <span data-ttu-id="21c2f-121">Gelen POP3 iletileri genellikle çok daha büyük veriler ve giden POP3 Istemci iletileri olur</span><span class="sxs-lookup"><span data-stu-id="21c2f-121">Incoming POP3 messages would usually be much larger data then outgoing POP3 Client messages</span></span>

## <a name="netx-pop3-client-creation"></a><span data-ttu-id="21c2f-122">NetX POP3 Istemcisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="21c2f-122">NetX POP3 Client Creation</span></span>

<span data-ttu-id="21c2f-123">POP3 Istemcisi oluşturma hizmeti, TCP yuvasını oluşturmak *nx_pop3_client_create* ve POP3 sunucusuyla bağlantı kurmak.</span><span class="sxs-lookup"><span data-stu-id="21c2f-123">The POP3 Client create service, *nx_pop3_client_create* create the TCP socket and connect with the POP3 server.</span></span>

<span data-ttu-id="21c2f-124">POP3 sunucusu ile bağlandıktan sonra POP3 Istemci uygulaması, maildrop kutusunda oturan posta öğelerinin sayısını almak için *nx_pop3_client _mail_items_get* çağırabilir:</span><span class="sxs-lookup"><span data-stu-id="21c2f-124">After connecting with the POP3 server, the POP3 Client application can call *nx_pop3_client _mail_items_get* to obtain the number of mail items sitting in its maildrop box:</span></span>

```c
UINT nx_pop3_client_mail_items_get(NX_POP3_CLIENT *client_ptr,
                                UINT *number_mail_items,
                                ULONG *maildrop_total_size)
```

<span data-ttu-id="21c2f-125">Istemci posta kutusunda bir veya daha fazla öğe varsa, uygulama belirli bir posta öğesinin boyutunu *nx_pop3_client_get_mail_item* hizmetini kullanarak alabilir:</span><span class="sxs-lookup"><span data-stu-id="21c2f-125">If one or more items are in the Client maildrop, the application can obtain the size of a specific mail item, using the *nx_pop3_client_get_mail_item* service:</span></span>

```c
UINT nx_pop3_client_mail_item_get(NX_POP3_CLIENT *client_ptr,
                                UINT mail_item,
                                ULONG *item_size)
```

<span data-ttu-id="21c2f-126">Maildrop 'daki ilk posta öğesi Dizin 1 ' dir.</span><span class="sxs-lookup"><span data-stu-id="21c2f-126">The first mail item in the maildrop is at index 1.</span></span>

<span data-ttu-id="21c2f-127">Asıl e-posta iletisini almak için, uygulama, hizmet tarafından son paketin final_packet giriş bağımsız değişkeni tarafından alındığını belirten posta iletisi paketlerini almak için *nx_pop3_client_mail_item_get_message_data* hizmetini çağırabilir:</span><span class="sxs-lookup"><span data-stu-id="21c2f-127">To get the actual mail message, the application can call the *nx_pop3_client_mail_item_get_message_data* service to retrieve the mail message packets until the service indicates the last packet is received by the final_packet input argument:</span></span>

```c
UINT nx_pop3_client_mail_item_message_get(
                        NX_POP3_CLIENT *client_ptr,
                        NX_PACKET **recv_packet_ptr,
                        ULONG *bytes_retrieved,
                        UINT *final_packet)
```

<span data-ttu-id="21c2f-128">Belirli bir posta öğesini silmek için uygulama, önceki *nx_pop3_client_get_mail_item* çağrısında kullanılan aynı dizinle *nx_pop3_client_mail_item_delete* çağırır.</span><span class="sxs-lookup"><span data-stu-id="21c2f-128">To delete a specific mail item, the application calls *nx_pop3_client_mail_item_delete* with the same index as used in the preceding *nx_pop3_client_get_mail_item* call.</span></span>

<span data-ttu-id="21c2f-129">Istemci *nx_pop3_client_delete* hizmeti kullanılarak silinebilir.</span><span class="sxs-lookup"><span data-stu-id="21c2f-129">The Client can be deleted using the *nx_pop3_client_delete* service.</span></span> <span data-ttu-id="21c2f-130">Uygulamanın, *nx_packet_pool_delete* HIZMETINI kullanarak POP3 istemci paket havuzunu silme konusunda uygulamaya yönelik olduğunu göz önünde kalmaz.</span><span class="sxs-lookup"><span data-stu-id="21c2f-130">Note it is up to the application to delete the POP3 Client packet pool using the *nx_packet_pool_delete* service there is no longer has any use for it.</span></span>

## <a name="netx-pop3-client-constraints"></a><span data-ttu-id="21c2f-131">NetX POP3 Istemci kısıtlamaları</span><span class="sxs-lookup"><span data-stu-id="21c2f-131">NetX POP3 Client Constraints</span></span>

<span data-ttu-id="21c2f-132">NetX POP3 Istemcisi uygulamasında bazı kısıtlamalar vardır:</span><span class="sxs-lookup"><span data-stu-id="21c2f-132">There are some constraints in the NetX POP3 Client implementation:</span></span>

1. <span data-ttu-id="21c2f-133">NetX POP3 Istemcisi, kimlik doğrulama komutunu desteklemez, ancak Istemci sunucusu kimlik doğrulaması alışverişi için DIGEST-MD5 kullanarak APOP kimlik doğrulaması uygular.</span><span class="sxs-lookup"><span data-stu-id="21c2f-133">The NetX POP3 Client does not support the AUTH command although it does implement APOP authentication using DIGEST-MD5 for the Client Server authentication exchange.</span></span>

1. <span data-ttu-id="21c2f-134">NetX POP3 Istemcisi tüm POP3 komutlarını uygulamaz (örn. TOP veya UıDL komutları).</span><span class="sxs-lookup"><span data-stu-id="21c2f-134">NetX POP3 Client does not implement all POP3 commands (e.g. the TOP or UIDL commands).</span></span> <span data-ttu-id="21c2f-135">Aşağıda, desteklediği komutların bir listesi verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="21c2f-135">Below is a list of commands it does support:</span></span>
   - <span data-ttu-id="21c2f-136">NOOP</span><span class="sxs-lookup"><span data-stu-id="21c2f-136">NOOP</span></span>
   - <span data-ttu-id="21c2f-137">RSET</span><span class="sxs-lookup"><span data-stu-id="21c2f-137">RSET</span></span>

## <a name="netx-pop3-client-login"></a><span data-ttu-id="21c2f-138">NetX POP3 Istemcisi oturum açma</span><span class="sxs-lookup"><span data-stu-id="21c2f-138">NetX POP3 Client Login</span></span>

<span data-ttu-id="21c2f-139">Bir NetX POP3 Istemcisinin, bir maildrop 'a erişmek için bir POP3 sunucusunda kendi kimliğini (oturum açma) doğrulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="21c2f-139">A NetX POP3 Client must authenticate itself (login) to a POP3 Server to access a maildrop.</span></span> <span data-ttu-id="21c2f-140">Bunu, Kullanıcı/GEÇIŞ komutlarını kullanarak ve POP3 sunucusunda bilinen bir Kullanıcı adı ve parola sağlayarak ya da aşağıda açıklanan APOP komutu ve MD5 özetini kullanarak yapabilir.</span><span class="sxs-lookup"><span data-stu-id="21c2f-140">It can do so either by using the USER/PASS commands and providing a username and password known to the POP3 Server, or by using the APOP command and MD5 digest described below.</span></span>

<span data-ttu-id="21c2f-141">Kullanıcı adı genellikle tam etki alanı adıdır (bir ' @ ' karakteriyle ayrılmış bir yerel parça ve bir etki alanı adı içerir).</span><span class="sxs-lookup"><span data-stu-id="21c2f-141">The username is typically a fully qualified domain name (contains a local-part and a domain name, separated by an '@' character).</span></span> <span data-ttu-id="21c2f-142">Kullanıcı ve PASS POP3 komutlarını kullanırken, Istemci kullanıcı adını ve parolasını Internet üzerinden şifrelenmemiş şekilde gönderiyor.</span><span class="sxs-lookup"><span data-stu-id="21c2f-142">When using the POP3 commands USER and PASS, the Client is sending its username and password unencrypted over the Internet.</span></span>

<span data-ttu-id="21c2f-143">Kullanıcı adı ve parola Temizleme güvenlik riskini ortadan kaldırmak için, NetX POP3 Istemcisi *nx_pop3_client_create* hizmetindeki *APOP_authentication* parametresi ayarlanarak APOP kimlik doğrulamasını kullanacak şekilde yapılandırılabilir:</span><span class="sxs-lookup"><span data-stu-id="21c2f-143">To avoid the security risk of clear texting username and password, the NetX POP3 Client can be configured to use APOP authentication by setting the *APOP_authentication* parameter in the *nx_pop3_client_create* service:</span></span>

```c
UINT  nxd_pop3_client_create(NX_POP3_CLIENT *client_ptr,
                            UINT APOP_authentication,
                            NX_IP *ip_ptr,
                            NX_PACKET_POOL *packet_pool_ptr,
                            NXD_ADDRESS *server_ip_address, ULONG server_port,
                            CHAR *client_name,
                            CHAR *client_password)
```

<span data-ttu-id="21c2f-144">Ya da yalnızca IPv4 uygulamaları için *nx_pop3_client_create* hizmeti:</span><span class="sxs-lookup"><span data-stu-id="21c2f-144">Or for IPv4 only applications, the *nx_pop3_client_create* service:</span></span>

```c
UINT  nx_pop3_client_create(NX_POP3_CLIENT *client_ptr,
                            UINT APOP_authentication,
                            NX_IP *ip_ptr,
                            NX_PACKET_POOL *packet_pool_ptr,
                            ULONG server_ip_address,
                            ULONG server_port, CHAR *client_name,
                            CHAR *client_password)
```

<span data-ttu-id="21c2f-145">Istemci APOP komutunu gönderdiğinde, sunucu etki alanını, yerel saati ve sunucu selamından ayıklanan işlem KIMLIĞINI ve Istemci parolasını içeren bir MD5 özeti alır.</span><span class="sxs-lookup"><span data-stu-id="21c2f-145">When the Client sends the APOP command, it takes an MD5 digest containing the server domain, local time and process ID extracted from the Server greeting, plus the Client password.</span></span> <span data-ttu-id="21c2f-146">POP3 sunucusu aynı bilgileri içeren bir MD5 özeti oluşturacak ve bunun MD5 özeti Istemcinin MD5 özeti ile eşleşiyorsa, Istemcinin kimliği doğrulanır.</span><span class="sxs-lookup"><span data-stu-id="21c2f-146">The POP3 Server will create an MD5 digest containing the same information and if its MD5 digest matches the Client's MD5 digest, the Client is authenticated.</span></span>

<span data-ttu-id="21c2f-147">APOP kimlik doğrulaması başarısız olursa, NetX POP3 Istemcisi Kullanıcı/GEÇIŞ kimlik doğrulaması gerçekleştirmeye çalışır.</span><span class="sxs-lookup"><span data-stu-id="21c2f-147">If APOP authentication fails, NetX POP3 Client will attempt USER/PASS authentication.</span></span>

## <a name="the-pop3-client-maildrop"></a><span data-ttu-id="21c2f-148">POP3 Istemcisi posta bırakma</span><span class="sxs-lookup"><span data-stu-id="21c2f-148">The POP3 Client Maildrop</span></span>

<span data-ttu-id="21c2f-149">İstemci posta, bir posta kutusundaki veya "maildrop" bir POP3 sunucusunda depolanır.</span><span class="sxs-lookup"><span data-stu-id="21c2f-149">Client mail is stored on a POP3 Server in a mailbox or "maildrop."</span></span> <span data-ttu-id="21c2f-150">POP3 sunucusundaki bir Istemci maildrop, posta öğelerinin 1 tabanlı bir listesi olarak temsil edilir.</span><span class="sxs-lookup"><span data-stu-id="21c2f-150">A Client maildrop on a POP3 Server is represented as a 1 based list of mail items.</span></span> <span data-ttu-id="21c2f-151">Diğer bir deyişle, her postanın, Dizin 1 ' deki (sıfır değil) ilk posta öğesiyle maildrop listesindeki diziniyle başvurulur.</span><span class="sxs-lookup"><span data-stu-id="21c2f-151">That is, each mail is referred to by its index in the maildrop list with the first mail item at index 1 (not zero).</span></span> <span data-ttu-id="21c2f-152">POP3 komutları, bu listedeki dizinlerinden belirli posta öğelerine başvurur.</span><span class="sxs-lookup"><span data-stu-id="21c2f-152">POP3 commands refer to specific mail items by their index in this list.</span></span>

## <a name="the-pop3-protocol-state-machine"></a><span data-ttu-id="21c2f-153">POP3 protokol durumu makinesi</span><span class="sxs-lookup"><span data-stu-id="21c2f-153">The POP3 Protocol State Machine</span></span>

<span data-ttu-id="21c2f-154">POP3 protokolü, hem Istemci hem de sunucunun POP3 oturumunun durumunu korumasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="21c2f-154">The POP3 protocol requires that both Client and Server maintain the state of the POP3 session.</span></span> <span data-ttu-id="21c2f-155">İlk olarak, Istemci POP3 sunucusuna bağlanmaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="21c2f-155">First, the Client attempts to connect to the POP3 Server.</span></span> <span data-ttu-id="21c2f-156">Başarılı olursa, RFC 1939 tarafından tanımlanan üç farklı durum bulunan POP3 protokolüne girer.</span><span class="sxs-lookup"><span data-stu-id="21c2f-156">If successful it enters into the POP3 protocol which has three distinct states defined by RFC 1939.</span></span> <span data-ttu-id="21c2f-157">İlk durum, kendisini sunucusuna tanıtmak zorunda olduğu yetkilendirme durumudur.</span><span class="sxs-lookup"><span data-stu-id="21c2f-157">The initial state is the Authorization state in which it must identify itself to the Server.</span></span> <span data-ttu-id="21c2f-158">Yetkilendirme durumunda, POP3 Istemcisi yalnızca Kullanıcı ve GEÇIŞ komutlarını, bu sırada veya APOP komutunu verebilir.</span><span class="sxs-lookup"><span data-stu-id="21c2f-158">In the Authorization state, the POP3 Client can only issue the USER and the PASS commands, and in that order, or the APOP command.</span></span>

<span data-ttu-id="21c2f-159">POP3 Istemcisinin kimliği doğrulandıktan sonra, Istemci oturumu Işlem durumunu girer.</span><span class="sxs-lookup"><span data-stu-id="21c2f-159">Once the POP3 Client is authenticated, the Client session enters the Transaction state.</span></span> <span data-ttu-id="21c2f-160">Bu durumda, Istemci posta silme işlemini indirebilir ve talep edebilir.</span><span class="sxs-lookup"><span data-stu-id="21c2f-160">In this state, the Client can download and request mail deletion.</span></span> <span data-ttu-id="21c2f-161">Işlem durumunda izin verilen komutlar LIST, STAT, RETR, SIL, RSET ve QUIT.</span><span class="sxs-lookup"><span data-stu-id="21c2f-161">The commands allowed in the Transaction state are LIST, STAT, RETR, DELE, RSET and QUIT.</span></span> <span data-ttu-id="21c2f-162">Genellikle, POP3 Istemcisi bir dizi RETR komutuyla izlenen bir STAT komutu gönderir.</span><span class="sxs-lookup"><span data-stu-id="21c2f-162">Typically the POP3 Client sends a STAT command followed by a series of RETR commands (one for each mail item in its maildrop).</span></span>

<span data-ttu-id="21c2f-163">Istemci, çıkış komutuna ulaştıktan sonra POP3 oturumu, sunucudan TCP bağlantısını kesmeyi başlattığı güncelleştirme durumuna girer.</span><span class="sxs-lookup"><span data-stu-id="21c2f-163">Once the Client issues the QUIT command, the POP3 session enters the Update state in which it initiates the TCP disconnect from the Server.</span></span> <span data-ttu-id="21c2f-164">Postayı daha sonra indirmek için, POP3 Istemci uygulaması istediğiniz `nx_pop3_client_mail_items_get` zaman arayarak maildrop 'da yeni posta olup olmadığını denetleyebilir.</span><span class="sxs-lookup"><span data-stu-id="21c2f-164">To download mail later, the POP3 Client application may call `nx_pop3_client_mail_items_get` at any time to check for new mail in the maildrop.</span></span>

### <a name="pop3-server-reply-codes"></a><span data-ttu-id="21c2f-165">POP3 sunucusu yanıt kodları</span><span class="sxs-lookup"><span data-stu-id="21c2f-165">POP3 Server Reply Codes</span></span>

- <span data-ttu-id="21c2f-166">**+ Tamam**: sunucu, istemci komutunu kabul etmek için bu yanıtı kullanır.</span><span class="sxs-lookup"><span data-stu-id="21c2f-166">**+OK**: The Server uses this reply to accept a Client command.</span></span> <span data-ttu-id="21c2f-167">Sunucu, ' + Tamam ' öğesinden sonra ek bilgi içerebilir, ancak posta iletisi verilerini veya LISTE ya da SIL komutlarını karşıdan yükleme durumu dışında Istemcinin bu bilgileri işleyeceğini varsaymaz.</span><span class="sxs-lookup"><span data-stu-id="21c2f-167">The Server can include additional information after the '+OK' but cannot assume the Client will process this information, except in the case of downloading mail message data or the LIST or DELE commands.</span></span> <span data-ttu-id="21c2f-168">İkinci durumda, komut sonrasında ' Argument ', Istemci maildrop içindeki posta öğesinin dizinine başvurduktan sonra.</span><span class="sxs-lookup"><span data-stu-id="21c2f-168">In the latter case, the 'argument' after the command references the index of the mail item in the Client maildrop.</span></span>

- <span data-ttu-id="21c2f-169">**-Err**: sunucu, bir istemci komutunu reddetmek için bu yanıtı kullanır.</span><span class="sxs-lookup"><span data-stu-id="21c2f-169">**-ERR**: The Server uses this reply to reject a Client command.</span></span> <span data-ttu-id="21c2f-170">Sunucu, '-ERR ' sonrasında ek bilgi gönderebilir, ancak Istemcinin bu bilgileri işleyeceğini varsayamaz.</span><span class="sxs-lookup"><span data-stu-id="21c2f-170">The Server may send additional information following the '-ERR' but cannot assume the Client will process this information.</span></span>

### <a name="sample-pop3-client---server-session"></a><span data-ttu-id="21c2f-171">Örnek POP3 Istemcisi-sunucu oturumu</span><span class="sxs-lookup"><span data-stu-id="21c2f-171">Sample POP3 Client - Server Session</span></span>

<span data-ttu-id="21c2f-172">**Kullanıcı/GEÇIŞ kullanan temel POP3 örneği:**</span><span class="sxs-lookup"><span data-stu-id="21c2f-172">**Basic POP3 example using USER/PASS:**</span></span>

```c
S: <wait for connection on TCP port 110>
C: <open connection>
S: +OK POP3 server ready <1896.697170952@dbc.mtview.ca.us>
C: USER mrose
S: +OK mrose is valid
C: PASS mvan99
S: +OK mrose is logged in
C: STAT
S: +OK 2 320
C: RETR 1
S: +OK 120 octets
S: <the POP3 server sends message 1>
S: .
C: DELE 1
S: +OK message 1 deleted
C: RETR 2
S: +OK 200 octets
S: <the POP3 server sends message 2>
S: .
C: DELE 2
S: +OK message 2 deleted
C: QUIT
S: +OK POP3 server signing off (maildrop empty)
C: <close connection>
S: <wait for next connection>
```

<span data-ttu-id="21c2f-173">**APOP (ve STAT yerine LIST) kullanan temel POP3 örneği:**</span><span class="sxs-lookup"><span data-stu-id="21c2f-173">**Basic POP3 example using APOP (and LIST instead of STAT):**</span></span>

```c
S: <wait for connection on TCP port 110>
C: <open connection>
S: +OK POP3 server ready <1896.697170952@dbc.mtview.ca.us>
C: APOP mrose c4c9334bac560ecc979e58001b3e22fb
S: +OK mrose's maildrop has 2 messages (320 octets)
C: LIST
S: +OK 2 messages (320 octets)
S: 1 120
S: 2 200
S: .
C: RETR 1
S: +OK 120 octets
S: <the POP3 server sends message 1>
S: .
C: DELE 1
S: +OK message 1 deleted
C: RETR 2
S: +OK 200 octets
S: <the POP3 server sends message 2>
S: .
C: DELE 2
S: +OK message 2 deleted
C: QUIT
S: +OK dewey POP3 server signing off (maildrop empty)
C: <close connection>
S: <wait for next connection>
```

## <a name="rfcs-supported-by-netx-pop3-client"></a><span data-ttu-id="21c2f-174">NetX POP3 Istemcisi tarafından desteklenen RFC 'Ler</span><span class="sxs-lookup"><span data-stu-id="21c2f-174">RFCs Supported by NetX POP3 Client</span></span>

<span data-ttu-id="21c2f-175">NetX Istemci POP3, RFC 1939 ile uyumludur.</span><span class="sxs-lookup"><span data-stu-id="21c2f-175">NetX Client POP3 is compliant with RFC 1939.</span></span>
