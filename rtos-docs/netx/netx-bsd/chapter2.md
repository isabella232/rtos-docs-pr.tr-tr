---
title: Bölüm 2-Azure RTOS NetX BSD yüklemesi ve kullanımı
description: Bu bölümde, Azure RTOS NetX BSD bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: c04175ec18dff160faf853d675c9c85c9a0c6fbc5e834c410a7cb97a739c69f8
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116796711"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-bsd"></a>Bölüm 2-Azure RTOS NetX BSD yüklemesi ve kullanımı

Bu bölümde, Azure RTOS NetX BSD bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların açıklaması yer almaktadır.

## <a name="product-distribution"></a>Ürün dağıtımı

Azure RTOS NetX BSD, konumundaki ortak kaynak kodu deposundan elde edilebilir [https://github.com/azure-rtos/netx/](https://github.com/azure-rtos/netx/) . Paket, aşağıdaki gibi, bu belgeyi içeren iki kaynak dosya ve bir PDF dosyası içerir:

- **nx_bsd. h**: NETX BSD için üst bilgi dosyası
- **nx_bsd. c**: NETX BSD Için c kaynak dosyası
- **nx_bsd.pdf**: NETX BSD Için Kullanıcı Kılavuzu

Tanıtım dosyaları:
- **bsd_demo_tcp. c**
- **bsd_demo_udp. c**

## <a name="netx-bsd-installation"></a>NetX BSD yüklemesi

NetX BSD 'yi kullanmak için, daha önce bahsedilen tüm dağıtım, NetX 'in yüklü olduğu dizine kopyalanmalıdır. Örneğin, "*\threadx\arm7\green*" dizininde NETX yüklüyse, *nx_bsd. h* ve *nx_bsd. c* dosyaları bu dizine kopyalanmalıdır.

## <a name="building-the-threadx-and-netx-components-of-a-bsd-application"></a>Bir BSD uygulamasının ThreadX ve NetX bileşenlerini oluşturma

### <a name="threadx"></a>ThreadX

ThreadX kitaplığı, iş parçacığı yerel depolama alanında *bsd_errno* tanımlamalıdır. Aşağıdaki yordamı öneririz:

1. *Tx_port. h*'de TX_THREAD_EXTENSION makrolarından birini aşağıdaki şekilde ayarlayın:

  ```c
  #define TX_THREAD_EXTENSION_3     int bsd_errno
  ```

2. ThreadX kitaplığını yeniden derleyin.

> [!NOTE]
> TX_THREAD_EXTENSION_3 zaten kullanılıyorsa, Kullanıcı diğer TX_THREAD_EXTENSION makrolarından birini kullanücretsizdir.

### <a name="netx"></a>NetX

NetX BSD hizmetlerini kullanmadan önce, NetX kitaplığı tanımlı NX_ENABLE_EXTENDED_NOTIFY_SUPPORT oluşturulmalıdır (örneğin, *nx_user. h*). Varsayılan olarak tanımlı değildir.

## <a name="using-netx-bsd"></a>NetX BSD kullanma

NetX için BSD kullanmak kolaydır. Temel olarak, uygulama kodu sırasıyla ThreadX ve NetX kullanmak için *tx_api. h* ve *nx_api. h* dahil *nx_bsd.* h içermelidir. *Nx_bsd. h* dahil olduğunda, uygulama kodu daha sonra bu KıLAVUZDA belirtilen BSD hizmetlerini kullanabilir. Uygulama, yapı işlemine *nx_bsd. c* de içermelidir. Bu dosya, diğer uygulama dosyalarıyla aynı şekilde derlenmelidir ve nesne formu, uygulamanın dosyalarıyla birlikte bağlanmalıdır. Bu, NetX BSD 'yi kullanmak için gereklidir.

NetX BSD hizmetlerini kullanmak için, uygulamanın bir IP örneği, bir paket havuzu oluşturması ve bsd_initialize çağırarak BSD hizmetlerini başlatması gerekir *.* Bu kılavuzda daha sonra "küçük örnek" bölümünde gösterilmiştir. Prototip aşağıda gösterilmiştir:

```c
INT bsd_initialize(NX_IP *default_ip, NX_PACKET_POOL *default_pool,
                  CHAR *free_memory_ptr, ULONG bsd_thread_stack_size,
                  UINT bsd_thread_priority);
```

Son üç parametre, TCP olaylarını denetleme ve iş parçacığı yığını alanını tanımlama gibi düzenli görevleri gerçekleştirmeye yönelik bir iş parçacığı oluşturmak için kullanılır.

> [!NOTE]
> Ağ bye sırasında çalışan BSD yuvalarının aksine NetX, konak işlemcisinin ana bilgisayar bayt düzeninde çalışır. Kaynak uyumluluğu nedenleriyle, hton (), ntohs (), htonl (), ntohl () makroları tanımlanmış, ancak geçirilen bağımsız değişkeni değiştirmiyor.

## <a name="netx-bsd-limitations"></a>NetX BSD sınırlamaları

NetX BSD, performans ve mimari sorunlarından dolayı tüm BSD 4,3 yuva özelliklerini desteklemez:

*Gönderme, alma, SendTo* ve *RECVFROM* çağrılarında Int bayrakları desteklenmez.

## <a name="netx-bsd-with-dns-support"></a>DNS desteğiyle NetX BSD

NX_BSD_ENABLE_DNS tanımlanmışsa NetX BSD, ana bilgisayar adı veya ana bilgisayar IP bilgilerini almak için DNS sorguları gönderebilir. Bu özellik, *nx_dns_create* hizmeti kullanılarak bir NETX DNS istemcisinin daha önce oluşturulmasını gerektirir. Bir veya daha fazla bilinen DNS sunucusu IP adresinin, sunucu adresleri eklemek için *nx_dns_server_add* kullanılarak DNS örneğine kaydedilmesi gerekir.

DNS hizmetleri ve bellek ayırma, *GetAddrInfo* ve *GetNameInfo* Hizmetleri tarafından kullanılır:

```c
INT getaddrinfo(const CHAR *node, const CHAR *service,
              const struct addrinfo *hints, struct addrinfo **res)

INT getnameinfo(const struct sockaddr *sa, socklen_t salen,
              char *host, size_t hostlen, char *serv, size_t servlen, int flags)
```

BSD uygulaması, bir ana bilgisayar adı ile *GetAddrInfo* çağırdığında NETX BSD, IP adresini almak için aşağıdaki hizmetlerden herhangi birini çağırır:

- nx_dns_ipv4_address_by_name_get
- nx_dns_cname_get

*Nx_dns_ipv4_address_by_name_get* için NETX BSD ipv4_addr_buffer bellek alanını kullanır. Bu arabelleklerin boyutu () tarafından tanımlanır `NX_BSD_IPV4_ADDR_PER_HOST * 4` .

NETX BSD, *GetAddrInfo*'dan adres bilgilerini döndürmek için, bellek alanı başka bir yapılandırılabilir seçenekler kümesi tarafından tanımlanmış olan *nx_bsd_addrinfo_pool_memory* threadx blok bellek tablosunu kullanır *NX_BSD_IPV4_ADDR_MAX_NUM*.

Yukarıdaki yapılandırma seçenekleri hakkında daha fazla bilgi için bkz. **yapılandırma seçenekleri** .

Ayrıca, NX_DNS_ENABLE_EXTENDED_RR_TYPES tanımlanmışsa ve konak girişi kurallı bir addır, NetX BSD daha önce oluşturulmuş bir blok havuzundan dinamik olarak bellek ayırır *_nx_bsd_cname_block_pool*

> [!NOTE]
> *GetAddrInfo* çağrıldıktan sonra, *freeaddrinfo* hizmeti kullanılarak, kaynak bağımsız değişkeni tarafından işaret edilen belleğin blok tabloya geri bırakılması için BSD uygulaması sorumludur.

## <a name="configuration-options"></a>Yapılandırma seçenekleri

*Nx_bsd. h* içindeki kullanıcı yapılandırılabilir seçenekleri, uygulamanın, belirli gereksinimleri Için NETX BSD yuvalarını ince ayarlamaya izin verir. Bu parametrelerin listesi aşağıda verilmiştir:

- **NX_BSD_TCP_WINDOW**: TCP yuvası oluşturma çağrılarında kullanılır. 65535, 100Mb Ethernet için tipik bir pencere boyutudur. Varsayılan değer 65535 ' dir.
- **NX_BSD_SOCKFD_START** Bu, BSD yuvası dosya tanımlayıcısı başlangıç değerinin mantıksal dizinidir. Varsayılan olarak, bu seçenek 32 ' dir.
- **NX_BSD_MAX_SOCKETS** BSD katmanında kullanılabilir olan en fazla toplam yuva sayısını belirtir ve 32 ' nin katı olmalıdır. değer, varsayılan olarak 32 ' dir.
- **NX_BSD_SOCKET_QUEUE_MAX** Alma yuvası sırasında depolanan en fazla UDP paketi sayısını belirtir. Değer, varsayılan olarak 5 ' tir.
- **NX_BSD_MAX_LISTEN_BACKLOG** Bu, BSD TCP yuvaları için dinleme kuyruğunun (' biriktirme listesi ') boyutunu belirtir. Varsayılan değer 5 ' tir.
- **NX_MICROSECOND_PER_CPU_TICK** Zamanlayıcı kesmesi başına mikrosaniye sayısını belirtir
- **NX_BSD_TIMEOUT** BSD için gereken NetX iç çağrılarındaki süreölçer işaretleri cinsinden zaman aşımını belirtir. Varsayılan değer 20 * NX_IP_PERIODIC_RATE.
- **NX_BSD_TCP_SOCKET_DISCONNECT_TIMEOUT**: NETX bağlantı kesme çağrısının süreölçer işaretleri cinsinden zaman aşımını belirtir. Varsayılan değer 1’dir.
- **NX_BSD_PRINT_ERRORS** Ayarlanırsa, bir BSD işlevinin hata durumu dönüşü bir satır numarası ve hata türü döndürür, örneğin Hatanın gerçekleştiği NX_SOC_ERROR. Bu, uygulama geliştiricisinin hata ayıklama çıkışını tanımlamasını gerektirir. Varsayılan ayar devre dışıdır ve *nx_bsd. h* içinde herhangi bir hata ayıklama çıkışı belirtilmez
- **NX_BSD_TIMER_RATE** BSD düzenli zamanlayıcı görevinin çalışma aralığı. Varsayılan değer 1 saniyedir (1 * NX_IP_PERIODIC_RATE).
- **NX_BSD_TIMEOUT_PROCESS_IN_TIMER** Ayarlanırsa, bu seçenek BSD zaman aşımı işleminin sistem Zamanlayıcı bağlamında yürütülmesine izin verir. Varsayılan davranış devre dışıdır. Bu özellik, Bölüm 2 "NetX BSD yüklemesi ve kullanımı" bölümünde daha ayrıntılı olarak açıklanmıştır.
- **NX_BSD_ENABLE_DNS** Etkinleştirilirse NetX BSD, ana bilgisayar adı veya konak IP adresi için bir DNS sorgusu gönderir. Daha önce oluşturulup başlatılmış bir DNS Istemci örneği gerektirir. Varsayılan olarak etkin değildir.
- **NX_BSD_IPV4_ADDR_MAX_NUM** *GetAddrInfo* tarafından döndürülen en fazla IPv4 adresi sayısı. NX_BSD_IPV4_ADDR_MAX_NUM ile birlikte, bu, *GetAddrInfo* içinde bilgi depolamaya yönelik olarak bellek ayırmak Için NETX BSD bloğu havuzunun boyutunu nx_bsd_addrinfo_block_pool tanımlar. Varsayılan değer 5 ' tir.
- **NX_BSD_IPV4_ADDR_PER_HOST**: DNS sorgusu başına depolanan en yüksek IPv4 adreslerini tanımlar. Varsayılan değer 5 ' tir.

## <a name="bsd-socket-options"></a>BSD yuvası seçenekleri

Aşağıdaki NetX BSD yuva seçeneklerinin listesi, *setsockopt* hizmeti kullanılarak her yuva temelinde çalışma zamanında etkinleştirilebilir (veya devre dışı).

```c
INT setsockopt(INT sockID, INT option_level, INT option_name, const
                void *option_value, INT option_length);
```

*Option_level* için iki farklı ayar vardır.

Çalışma zamanı yuva seçeneklerinin ilk türü yuva düzeyi seçenekleri için SOL_SOCKET. Yuva düzeyi seçeneğini etkinleştirmek için, SOL_SOCKET olarak ayarlanan option_level ve option_name belirli bir seçeneğe ayarla ' *yı çağırın.* örneğin, so_broadcast. Bir seçenek ayarı almak için, option_level tekrar SOL_SOCKET olarak ayarlanan option_name için *getsockopt* çağırın.

Çalışma zamanı yuva düzeyi seçeneklerinin listesi aşağıda gösterilmiştir.

- **So_broadcast**: ayarlandıysa, NETX yuvalarından yayın paketlerinin gönderilmesini ve alınmasına izin vermez. Bu, NetX için varsayılan davranıştır. Tüm yuvalarda bu yetenek vardır.
- **SO_ERROR:** *getsockopt* hizmetini kullanarak belirtilen yuvanın önceki yuva işleminde yuva durumunu almak için kullanılır. Tüm yuvalar bu özelliktedir.
- **SO_KEEPALIVE:** Ayarlanırsa, TCP Canlı Tut özelliğini sağlar. Bu, NetX kitaplığının *nx_user.h* içinde tanımlanan NX_TCP_ENABLE_KEEPALIVE ile nx_user gerektirir. Bu özellik varsayılan olarak devre dışıdır.
- **SO_RCVTIMEO:** Bu, NetX BSD yuvalarında paketleri almak için bekleme seçeneğini saniyeler içinde ayarlar. Varsayılan değer, NX_WAIT_FOREVER (0xFFFFFFFF) veya engelleyici olmayan etkinleştirilirse NX_NO_WAIT (0x0).
- **SO_RCVBUF:** Bu, TCP yuvasının pencere boyutunu ayarlar. Varsayılan değer olan NX_BSD_TCP_WINDOW BSD TCP yuvaları için 64k olarak ayarlanır. Boyutu 65535'in üzerine ayarlamak için NetX kitaplığının tanımlandığı NX_TCP_ENABLE_WINDOW_SCALING gerekir.
- **SO_REUSEADDR:** Ayarlanırsa, birden çok yuvanın bir bağlantı noktasına eşlenmiş olması gerekir. Tipik kullanım TCP Sunucusu yuvası için kullanılır. Bu, NetX yuvalarının varsayılan davranışıdır.

İkinci tür çalışma zamanı yuva seçenekleri, IP seçeneği düzeyidir. BIR IP düzeyi seçeneğini etkinleştirmek için, option_level olarak IP_PROTO option_name *setesockopt* çağrısı IP_MULTICAST_TTL. Bir seçenek ayarını almak için, yeniden option_level olarak ayarlanmış şekilde option_name için *getsockopt* IP_PROTO.

Çalışma zamanı IP düzeyi seçeneklerinin listesi aşağıda gösterilmiştir.

- **IP_MULTICAST_TTL:** Udp yuvaları için yaşam süresi ayarlar. Yuva oluşturulduğunda NX_IP_TIME_TO_LIVE (0x80) varsayılan değerdir. Bu değer, bu yuva seçeneğiyle *setsockopt çağrılarak* geçersiz kılınabilir.
- **IP_ADD_MEMBERSHIP:** Ayarlanırsa, bu seçenekler BSD yuvasının (yalnızca UDP yuvaları için geçerlidir) belirtilen IGMP grubunu birleştirmesini sağlar.
- **IP_DROP_MEMBERSHIP:** Ayarlanırsa, bu seçenekler BSD yuvasının (yalnızca UDP yuvaları için geçerlidir) belirtilen IGMP grubundan ayrılmasını sağlar.

## <a name="small-example-system"></a>Küçük Örnek Sistem

Aşağıdaki Şekil 1.0'da NetX BSD'yi kullanma örneği gösterilmiştir. Bu örnekte, *nx_bsd.h* dahil dosyası 7. satıra getiri. Ardından, IP örneği *bsd_ip* ve *paket havuzu bsd_pool* 20. ve 21. satırda genel değişkenler olarak oluşturulur. Bu tanıtımda ram (sanal) ağ sürücüsü (satır 41) kullanılır. İstemci ve sunucu, bu örnekteki tek BIR IP örneğinde aynı IP adresini paylaşır.

İstemci ve sunucu iş parçacıkları, uygulamayı ayaran ve 293-361 *tx_application_define* 303. ve 309. satırlarda oluşturulur. 327. satırda IP örneği başarıyla etkinleştirilmişse 350. satırda TCP hizmetleri için IP örneği etkinleştirilir. BSD hizmetlerinin kullanılamadan önceki son *gereksinimi, BSD* için gereken tüm veri yapılarını ve NetX bsd_initialize ThreadX kaynaklarını ayarlamak için 360. satırda bsd_initialize çağrısı yapmaktır.

381-397. satırlarda tanımlanan thread_1_entry sunucu iş parçacığı giriş işlevinde uygulama, sürücünün ağ parametreleriyle NetX'i başlatması için bekler.  Bu yapıldıktan sonra, TCP sunucu yuvası ayarlama ayrıntılarını işlemek için 146-253. satırlarda tanımlanan *tcpServer'ı* arar.

*tcpServer,* 159.  satırda yuva hizmetini çağırarak ana yuvayı oluşturur  ve 176. satırda bağlama çağrısını kullanarak dinleme yuvasına bağlar. Ardından 191. satırda bağlantı isteklerini dinlemek için yapılandırılır. Ana yuvanın bir bağlantı isteğini kabul etmey olduğunu unutmayın. Bağlantı isteklerini algılamak için her zaman *select* çağrısı yapılan bir sürekli döngüde çalışır. BSD yuva dizilerinden seçilen ikincil bir BSD yuvasına, 218. satırda *kabul* hizmeti çağrıldikten sonra bağlantı isteği atanır.

İstemci tarafında, 366-377 satırlarında tanımlanan thread_0_entry istemci iş parçacığı giriş işlevi de NetX'in sürücü tarafından başlatılmasını beklemektedir.  Burada yalnızca sunucu tarafının bunu yapmalarını bekleriz. Ardından 54-142. satırda tanımlanan *tcpClient'ı* çağırarak TCP istemci yuvanızı ayarlama ve TCP bağlantısı isteğiyle ilgili ayrıntıları işlemesini sağlar.

TCP istemci yuvası 68. satırda oluşturulur. Yuva belirtilen IP adresine bağlı ve 84. satırda *Connect* çağrısıyla TCP sunucusuna bağlanmaya çalışır. Artık paket göndermeye ve almaya başlamaya hazırdır.

```c
1 /*  This is a small demo of BSD Wrapper for the high-performance NetX TCP/IP stack.
2     This demo demonstrate TCP connection, disconnection, sending, and receiving using
3     ARP and a simulated Ethernet driver. */
4
5 #include     "tx_api.h"
6 #include     "nx_api.h"
7 #include     "nx_bsd.h"
8 #include     <string.h>
9 #include     <stdlib.h>
10
11 #define         DEMO_STACK_SIZE         (16*1024)
12
13
14 /* Define the ThreadX and NetX object control blocks... */
15
16 TX_THREAD       thread_0;
17 TX_THREAD       thread_1;
18
19
20 NX_PACKET_POOL  bsd_pool;
21 NX_IP           bsd_ip;
22
23
24 /* Define the counters used in the demo application... */
25
26 ULONG           error_counter;
27
28 /* Define fd_set for select call */
29 fd_set          master_list,read_ready,read_ready1;
30
31
32 /* Define thread prototypes. */
33
34 VOID            thread_0_entry(ULONG thread_input);
35 VOID            thread_1_entry(ULONG thread_input);
36
37 VOID            tcpClient(CHAR *msg0);
38 VOID            tcpServer(VOID);
39 INT             HandleClient(INT sock);
40
41 VOID            _nx_ram_network_driver(struct NX_IP_DRIVER_STRUCT *driver_req);
42
43
44 /* Define main entry point. */
45
46 int main()
47 {
48
49     /* Enter the ThreadX kernel. */
50     tx_kernel_enter();
51 }
52
53
54 VOID tcpClient(CHAR *msg0)
55 {
56
57 INT     status,status1,send_counter;
58 INT     sock_tcp_1,length,length1;
59 struct  sockaddr_in echoServAddr;       /* Echo server address */
60 struct  sockaddr_in localAddr;          /* Local address */
61 struct  sockaddr_in remoteAddr;         /* Remote address */
62
63 UINT    echoServPort; /* Echo Server Port */
64 CHAR    rcvBuffer1[32]
65
66
67     /* Create BSD TCP Socket */
68     sock_tcp_1 = **socket**( PF_INET, SOCK_STREAM, IPPROTO_TCP);
69     if (sock_tcp_1 == -1)
70     {
71         printf("\nError: BSD TCP Client socket create \n");
72         return;
73     }
74
75     printf("\nBSD TCP Client socket created %lu \n", sock_tcp_1);
76     /* Fill destination port and IP address */
77     echoServPort = 12;
78     memset(&echoServAddr, 0, sizeof(echoServAddr));
79     echoServAddr.sin_family = PF_INET;
80     echoServAddr.sin_addr.s_addr = htonl(0x01020304);
81     echoServAddr.sin_port = echoServPort;
82
83     /* Now connect this client the server */
84     status1 = connect(sock_tcp_1, (struct sockaddr *)&echoServAddr, sizeof(echoServAddr));
85     /* Check for error. */
86     if (status1 != OK)
87     {
88         printf("\nError: BSD TCP Client socket Connect, %d \n",sock_tcp_1);
89         status = soc_close(sock_tcp_1);
90         if (status != ERROR)
91             printf("\nConnect ERROR so BSD Client Socket Closed: %d\n",sock_tcp_1);
92         else
93             printf("\nError: BSD Client Socket close %d\n",sock_tcp_1);
94         return;
95     }
96     /* Get and print source and destination information */
97     printf("\nBSD TCP Client socket: %d connected \n", sock_tcp_1);
98
99     status = getsockname(sock_tcp_1, (struct sockaddr *)&localAddr, &length);
100    printf("Client port = %lu , Client = %lu,", 
            localAddr.sin_port, localAddr.sin_addr.s_addr);
101    status = getpeername( sock_tcp_1, (struct sockaddr *) &remoteAddr, &length1);
102    printf("Remote port = %lu, Remote IP = %lu \n", 
            remoteAddr.sin_port remoteAddr.sin_addr.s_addr);
103
104    send_counter = 1;
105
106    /* Now receive the echoed packet from the server */
107    while(1)
108    {
109        tx_thread_sleep(2);
110
111        printf("\nClient sock: %d Sending packet No: %d to
                server\n",sock_tcp_1,send_counter);
112        status = send(sock_tcp_1,msg0, sizeof(msg0), 0);
113        if (status == ERROR)
114            printf("Error: BSD Client Socket send %d\n",sock_tcp_1);
115        else
116        {
117            printf("\nMessage sent: %s\n",msg0);
118            send_counter++;
119        }
120
121        status = recv(sock_tcp_1, (VOID *)rcvBuffer1, 31,0);
122        if (status == 0)
123            break;
124
125        rcvBuffer1[status] = 0;
126
127        if (status != ERROR)
128            printf("\nBSD Client Socket: %d received %lu bytes: %s ", 
                        sock_tcp_1,(ULONG)status,rcvBuffer1);
129        else
130            printf("\nError: BSD Client Socket receive %d \n",sock_tcp_1);
131
132    }
133
134    /* close this client socket */
135    status = soc_close(sock_tcp_1);
136    if (status != ERROR)
137        printf("\nBSD Client Socket Closed %d\n",sock_tcp_1);
138    else
139        printf("\nError: BSD Client Socket close %d \n",sock_tcp_1);
140
141    /* End */
142 }
143
144
145
146 void tcpServer(void)
147 {
148
149 INT         status,status1,sock,sock_tcp_2,i;
150 struct      sockaddr_in echoServAddr; /* Echo server address */
151 struct      sockaddr_in ClientAddr;
152
153 INT         Clientlen;
154 UINT        echoServPort; /* Echo Server Port */
155
156 INT         maxfd;
157
158 /* Create BSD TCP Server Socket */
159     sock_tcp_2 = socket( PF_INET, SOCK_STREAM, IPPROTO_TCP);
160     if (sock_tcp_2 == -1)
161     {
162         printf("Error: BSD TCP Server socket create\n");
163         return;
164     }
165     else
166         printf("BSD TCP Server socket created \n");
167
168     /* Now fill server side information */
169     echoServPort = 12;
170     memset(&echoServAddr, 0, sizeof(echoServAddr));
171     echoServAddr.sin_family = PF_INET;
172     echoServAddr.sin_addr.s_addr = htonl(0x01020304);
173     echoServAddr.sin_port = echoServPort;
174
175     /* Bind this server socket */
176         status = bind(sock_tcp_2, (struct sockaddr *) &echoServAddr, sizeof(echoServAddr));
177     if (status < 0)
178     {
179         printf("Error: BSD TCP Server Socket Bind \n");
180         return;
181     }
182     else
183         printf("BSD TCP Server Socket bound \n");
184
185     FD_ZERO(&master_list);
186     FD_ZERO(&read_ready);
187     FD_SET(sock_tcp_2,&master_list);
188     maxfd = sock_tcp_2;
189
190     /* Now listen for any client connections for this server socket */
191     status = listen(sock_tcp_2,5);
192     if (status < 0)
193     {
194         printf("Error: BSD TCP Server Socket Listen\n");
195         return;
196     }
197     else
198         printf("BSD TCP Server Socket Listen complete, ");
199
200     /* All set to accept client connections */
201     printf("Now accepting client connections\n");
202
203     /* Loop to create and establish server connections. */
204     while(1)
205     {
206
207         read_ready = master_list;
208         tx_thread_sleep(2); /* Allow some time to other threads too */
209         status = select(maxfd+1,&read_ready,0,0,0);
210         if (status == ERROR)
211         {
212             continue;
213         }
214
215         status = FD_ISSET(sock_tcp_2,&read_ready);
216         if(status)
217         {
218             sock = accept(sock_tcp_2,(struct sockaddr*)&ClientAddr, &Clientlen);
219
220             /* Add this new connection to our master list */
221             FD_SET(sock,&master_list);
222             if ( sock \maxfd)
223             {
224                 maxfd = sock;
225             }
226
227             continue;
228         }
229         for (i = 0; i < (maxfd+1); i++)
230         {
231             if (( i != sock_tcp_2) && (FD_ISSET(i,&master_list)) && 
                    (FD_ISSET(i,&read_ready)))
232             {
233                 status1 = HandleClient(i);
234                 if (status1 == 0)
235                 {
236                     status1 = soc_close(i);
237                     if (status1 == OK)
238                     {
239                         FD_CLR(i,&master_list);
240                         printf("\nBSD Server Socket:%d closed\n",i);
241                     }
242                     else
243                         printf("\nError:BSD Server Socket:%d close\n",i);
244                 }
245
246             }
247         }
248
249         /* Loop back to check any next client connection */
250
251     } /* While(1) ends */
252
253 }
254
255 CHAR     rcvBuffer[128];
256
257 INT     HandleClient(INT sock)
258 {
259
260 INT     status;
261
262
263     status = recv(sock, (VOID *)rcvBuffer, 128,0);
264     if (status == ERROR )
265     {
266         printf("\n BSD Server Socket:%d receive \n",sock);
267         return(ERROR);
268     }
269
270     /* a zero return from a recv() call indicates client is terminated! */
271     if (status == 0)
272     {
273         /* Done with this client , close this secondary server socket */
274         return(status);
275     }
276
277     /* print data received from the client */
278     printf("\nBSD Server Socket:%d received %lu bytes: %s \n", sock, (ULONG)status,rcvBuffer);
279
280     /* And echo the same data to the client */
281     status = send(sock,rcvBuffer, status + 1, 0);
282     if (status == ERROR )
283     {
284         printf("\nError: BSD Server Socket:%d send \n",sock);
285         return(ERROR);
286     }
287     return(status);
288 }
289
290
291 /* Define what the initial system looks like. */
292
293 void     tx_application_define(void *first_unused_memory)
294 {
295
296 CHAR     *pointer;
297 UINT     status;
298
299     /* Setup the working pointer. */
300     pointer = (CHAR *) first_unused_memory;
301
302     /* Create a client thread. */
303     tx_thread_create(&thread_0, "Client1", thread_0_entry, 0,
304         pointer, DEMO_STACK_SIZE, 2, 2, TX_NO_TIME_SLICE, TX_AUTO_START);
305
306     pointer = pointer + DEMO_STACK_SIZE;
307
308     /* Create a server thread. */
309     tx_thread_create(&thread_1, "Server", thread_1_entry, 0,
310         pointer, DEMO_STACK_SIZE,1,1, TX_NO_TIME_SLICE, TX_AUTO_START);
311
312     pointer = pointer + DEMO_STACK_SIZE;
313
314     /* Initialize the NetX system. */
315     nx_system_initialize();
316
317     /* Create a BSD packet pool. */
318     status = nx_packet_pool_create(&bsd_pool,"NetX BSD Packet Pool", 128
                                        pointer, 16384);
319     pointer = pointer + 16384;
320     if (status)
321     {
322         error_counter++;
323         printf("Error in creating BSD packet pool\n!");
324     }
325
326     /* Create an IP instance for BSD. */
327     status = nx_ip_create(&bsd_ip, "NetX IP Instance 2", IP_ADDRESS(1, 2, 3, 4),
                              0xFFFFFF00UL, &bsd_pool, _nx_ram_network_driver,
                              pointer, 2048, 1);
328
329     pointer = pointer + 2048;
330
331     if (status)
332     {
333         error_counter++;
334         printf("Error creating BSD IP instance\n!");
335     }
336
337     /* Enable ARP and supply ARP cache memory for BSD IP Instance */
338     status = nx_arp_enable(&bsd_ip, (void *) pointer, 1024);
339     pointer = pointer + 1024;
340
341     /* Check ARP enable status. */
342     if (status)
343     {
344         error_counter++;
345         printf("Error in Enable ARP and supply ARP cache memory to BSD IP instance\n");
346     }
347
348     /* Enable TCP processing for BSD IP instances. */
349
350     status = nx_tcp_enable(&bsd_ip);
351
352     /* Check TCP enable status. */
353     if (status)
354     {
355         error_counter++;
356         printf("Error in Enable TCP \n");
357     }
358
359     /* Now initialize BSD Scoket Wrapper */
360     status = bsd_initialize(&bsd_ip, &bsd_pool,pointer, 2048, 1);
361 }
362
363
364 /* Define the test threads. */
365
366 void     thread_0_entry)ULONG thread_input)
367 {
368
369 CHAR     *msg0 = "Client 1:
                     "ABCDEFGHIJKLMNOPQRSTUVWXYZ<>ABCDEFGHIJKLMNOPQRSTUVWXYZ<> \
                     "ABCDEFGHIJKLMNOPQRSTUVWXYZ<>END";
370
371     /* Wait till Server side is all set */
372     tx_thread_sleep(2);
373     while (1)
374     {
375         tcpClient(msg0);
376         tx_thread_sleep(1);
377     }
378 }
379
380 /* Define the server thread entry function. */
381 void     thread_1_entry(ULONG thread_input)
382 {
383
384 UINT     status;
385 ULONG    actual_status;
386
387 /* Ensure the IP instance has been initialized. */
388 status = nx_ip_status_check(&bsd_ip, NX_IP_INITIALIZE_DONE, &actual_status, 100);
389
390 /* Check status... */
391 if (status != NX_SUCCESS)
392 {
393     error_counter++;
394     return;
395 }
396 /* Start a TCP Server */
397 tcpServer();
398 }
399
```
