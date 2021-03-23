---
title: Bölüm 2-Azure RTOS NetX oto 'nin yüklenmesi ve kullanımı
description: Bu bölümde, Azure RTOS NetX için yükleme, kurulum ve kullanımla ilgili çeşitli sorunların açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 269a3b4e9754fdc19e2cf1482d483fad2b841de9
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825612"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-autoip"></a>Bölüm 2-Azure RTOS NetX oto 'nin yüklenmesi ve kullanımı

Bu bölümde, Azure RTOS NetX için yükleme, kurulum ve kullanımla ilgili çeşitli sorunların açıklaması yer almaktadır.

## <a name="product-distribution"></a>Ürün dağıtımı

NetX için Oto IP adresinden kullanılabilir [https://github.com/azure-rtos/netx](https://github.com/azure-rtos/netx) . Bu paket üç kaynak dosyası, bir içerme dosyası ve bu belgeyi içeren bir PDF dosyası içerir ve aşağıdaki gibi:

- **nx_auto_ip. h**: NETX Oto için üst bilgi dosyası
- **nx_auto_ip. c**: NETX oto Için c kaynak dosyası
- **demo_netx_auto_ip. c**: NETX Oto IP tanıtımı Için c kaynak dosyası
- **nx_auto_ip.pdf**: NETX otomatik IP 'nin PDF açıklaması

## <a name="autoip-installation"></a>Oto IP yüklemesi

NetX oto 'nin kullanılabilmesi için, daha önce bahsedilen tüm dağıtımın, NetX ' in yüklü olduğu dizine kopyalanması gerekir. Örneğin, "*\threadx\arm7\green*" dizininde NETX yüklüyse, *nx_auto_ip. h*, *nx_auto_ip. c* ve *demo_netx_auto_ip. c* dosyaları bu dizine kopyalanmalıdır.

## <a name="using-autoip"></a>Oto IP 'yi kullanma

NetX oto kullanımı kolaydır. Temel olarak uygulama kodu, ThreadX ve NetX kullanmak için *tx_api. h* ve *nx_api. h* dahil *nx_auto_ip. h* 'yi içermelidir. *Nx_auto_ip. h* eklendikten sonra, uygulama kodu daha sonra bu kılavuzun ilerleyen kısımlarında belirtilen Oto IP işlev çağrılarını yapabilir. Uygulama, yapı işlemine *nx_auto_ip. c* de içermelidir. Bu dosyalar, diğer uygulama dosyalarıyla aynı şekilde derlenmesi gerekir ve nesne formu, uygulamanın dosyalarıyla birlikte bağlanmalıdır. Bu, NetX Oto IP 'yi kullanmak için gereklidir.

> [!NOTE]
> CIP, NetX ARP hizmetlerini kullandığından, bu ARP,, Oto IP kullanılmadan önce *nx_arp_enable* çağrısıyla etkinleştirilmelidir.

## <a name="small-example-system"></a>Küçük örnek sistem

NetX oto kullanmanın ne kadar kolay olduğunu gösteren örnek şekil 1,1 ' de aşağıda gösterilen şekilde açıklanmıştır. Bu örnekte, *nx_auto_ip. h* olan Oto IP içerme dosyası, Line 002 ' de getirilir. Ardından, NetX Oto IP örneği, 090 satırındaki "*tx_application_define*" içinde oluşturulur. NetX Oto IP denetim bloğunun "auto_ip_0" daha önce satır 015 adresinde genel bir değişken olarak tanımlandığını unutmayın. Başarılı bir şekilde oluşturulduktan sonra, 098. satırda bir NetX oto başlatılır. IP adresi değiştirme geri çağırma işlevi işlemi, sonraki çakışmaları veya olası DHCP adresi çözümlemesini işlemek için kullanılan 105. satırda başlar.

> [!NOTE]
> Aşağıdaki örnekte konak cihazının tek bilgisayarlı bir cihaz olduğu varsayılır. Birden çok sayfalı bir cihaz için, konak uygulama NetX Oto IP hizmetini kullanarak bir IP adresini yoklamanın ikincil ağ arabirimini belirtmek üzere *nx_auto_ip_interface_*. Birden çok ağ bağlantılı uygulamalar ayarlama hakkında daha fazla bilgi için **NETX Kullanıcı kılavuzuna** bakın. Ana bilgisayar uygulamasının, IP adresi elde ettiğini doğrulamak için NetX API *nx_status_ip_interface_check* kullanması gerektiğini unutmayın.

## <a name="example-of-autoip-use-with-netx"></a>NetX ile Oto IP kullanımı örneği

```c
000 #include "tx_api.h"
001 #include "nx_api.h"
002 #include "nx_auto_ip.h"
003
004 #define         DEMO_STACK_SIZE         4096
005
006 /* Define the ThreadX and NetX object control blocks... */
007
008 TX_THREAD         thread_0;
009 NX_PACKET_POOL    pool_0;
010 NX_IP             ip_0;
011
012
013 /* Define the AUTO IP structures for the IP instance. */
014
015 NX_AUTO_IP         auto_ip_0;
016
017
018 /* Define the counters used in the demo application... */
019
020 ULONG             thread_0_counter;
021 ULONG             address_changes;
022 ULONG             error_counter;
023
024
025 /* Define thread prototypes. */
026
027 void     thread_0_entry(ULONG thread_input);
028 void     ip_address_changed(NX_IP *ip_ptr, VOID *auto_ip_address);
029 void     _nx_ram_network_driver(struct NX_IP_DRIVER_STRUCT *driver_req);
030
031
032 /* Define main entry point. */
033
034 int main()
035 {
036
037     /* Enter the ThreadX kernel. */
038     tx_kernel_enter();
039 }
040
041
042 /* Define what the initial system looks like. */
043
044 void     tx_application_define(void *first_unused_memory)
045 {
046
047 CHAR     *pointer;
048 UINT     status;
049
050
051     /* Setup the working pointer. */
052     pointer = (CHAR *) first_unused_memory;
053
054     /* Create the main thread. */
055     tx_thread_create(&thread_0, "thread 0", thread_0_entry, 0,
056                     pointer, DEMO_STACK_SIZE,
057                     16, 16, 1, TX_AUTO_START);
058
059     pointer = pointer + DEMO_STACK_SIZE;
060
061     /* Initialize the NetX system. */
062     nx_system_initialize();
063
064     /* Create a packet pool. */
065     status = nx_packet_pool_create(&pool_0, "NetX Main Packet Pool", 128,
066                                     pointer, 4096);
067                                     pointer = pointer + 4096;
068
069     if (status)
070         error_counter++;
071
072     /* Create an IP instance. */
073     status = nx_ip_create(&ip_0, "NetX IP Instance 0", IP_ADDRESS(0, 0, 0, 0),
074                             0xFFFFFF00UL, &pool_0, _nx_ram_network_driver,
075                             pointer, 4096, 1);
076                             pointer = pointer + 4096;
077
078     if (status)
079         error_counter++;
080
081     /* Enable ARP and supply ARP cache memory for IP Instance 0. */
082     status = nx_arp_enable(&ip_0, (void *) pointer, 1024);
083     pointer = pointer + 1024;
084
085     /* Check ARP enable status. */
086     if (status)
087         error_counter++;
088
089     /* Create the AutoIP instance for IP Instance 0. */
090     status = nx_auto_ip_create(&auto_ip_0, "AutoIP 0", &ip_0, pointer, 4096, 1);
091     pointer = pointer + 4096;
092
093     /* Check AutoIP create status. */
094     if (status)
095         error_counter++;
096
097     /* Start AutoIP instances. */
098     status = nx_auto_ip_start(&auto_ip_0, 0 /*IP_ADDRESS(169,254,254,255)*/);
099
100     /* Check AutoIP start status. */
101     if (status)
102         error_counter++;
103
104     /* Register an IP address change function for IP Instance 0. */
105     status = nx_ip_address_change_notify(&ip_0, ip_address_changed,
106                                         (void *) &auto_ip_0);
107
108     /* Check IP address change notify status. */
109     if (status)
110         error_counter++;
111     }
112
113
114     /* Define the test thread. */
115
116     void thread_0_entry(ULONG thread_input)
117     {
118
119     UINT      status;
120     ULONG     actual_status;
121
122
123          /* Wait for IP address to be resolved. */
124         do
125         {
126
127             /* Call IP status check routine. */
128             status = nx_ip_status_check(&ip_0, NX_IP_ADDRESS_RESOLVED,
129                                         &actual_status, 10000);
130
131         } while (status != NX_SUCCESS);
132
133         /* Since the IP address is resolved at this point, the application
134         can now fully utilize NetX! */
135
136         while(1)
137         {
138
139
140
141             /* Increment thread 0's counter. */
142             thread_0_counter++;
143
144             /* Sleep... */
145             tx_thread_sleep(10);
146         }
147     }
148
149
150     void ip_address_changed(NX_IP *ip_ptr, VOID *auto_ip_address)
151     {
152
153     ULONG         ip_address;
154     ULONG         network_mask;
155     NX_AUTO_IP    *auto_ip_ptr;
156
157
158     /* Setup pointer to auto IP instance. */
159     auto_ip_ptr = (NX_AUTO_IP *) auto_ip_address;
160
161     /* Pickup the current IP address. */
162     nx_ip_address_get(ip_ptr, &ip_address, &network_mask);
163
164     /* Determine if the IP address has changed back to zero. If so,
165     make sure the AutoIP instance is started. */
166     if (ip_address == 0)
167     {
168
169         /* Get the last AutoIP address for this node. */
170         nx_auto_ip_get_address(auto_ip_ptr, &ip_address);
171
172         /* Start this AutoIP instance. */
173         nx_auto_ip_start(auto_ip_ptr, ip_address);
174     }
175
176     /* Determine if IP address has transitioned to a non local IP address. */
177     else if ((ip_address & 0xFFFF0000UL) != IP_ADDRESS(169, 254, 0, 0))
178     {
179
180         /* Stop the AutoIP processing. */
181         nx_auto_ip_stop(auto_ip_ptr);
182     }
183
184     /* Increment a counter. */
185     address_changes++;
186 }
```

## <a name="configuration-options"></a>Yapılandırma seçenekleri

NetX AutoSize oluşturmak için birkaç yapılandırma seçeneği vardır. Aşağıda, her birinin ayrıntılı olarak açıklandığı tüm seçeneklerin bir listesi verilmiştir:

- **NX_DISABLE_ERROR_CHECKING**: tanımlı, bu seçenek temel Oto IP hata denetimini kaldırır. Genellikle uygulamanın hata ayıklaması yapıldıktan sonra kullanılır.
- **NX_AUTO_IP_PROBE_WAIT**: ilk yoklamayı göndermeden önce beklenecek saniye sayısı. Varsayılan olarak, bu değer 1 olarak tanımlanır.
- **NX_AUTO_IP_PROBE_NUM**: gönderilen ARP araştırmaları sayısı. Varsayılan olarak, bu değer 3 olarak tanımlanır.
- **NX_AUTO_IP_PROBE_MIN**: Gönderen yoklamalar arasında beklenecek saniye sayısı alt sınırı. Varsayılan olarak, bu değer 1 olarak tanımlanır.
- **NX_AUTO_IP_PROBE_MAX**: Gönderen yoklamalar arasında beklenecek en fazla saniye sayısı. Varsayılan olarak, bu değer 2 olarak tanımlanmıştır.
- **NX_AUTO_IP_MAX_CONFLICTS**: işleme gecikmelerini arttırmadan önce, tekrar IP çakışmalarının sayısı. Varsayılan olarak, bu değer 10 olarak tanımlanmıştır.
- **NX_AUTO_IP_RATE_LIMIT_INTERVAL**: Toplam çakışma sayısı aşıldığında bekleme süresinin uzaleceği saniye sayısı. Varsayılan olarak, bu değer 60 olarak tanımlanmıştır.
- **NX_AUTO_IP_ANNOUNCE_WAIT**: duyuru gönderilmeden önce beklenecek saniye sayısı. Varsayılan olarak, bu değer 2 olarak tanımlanmıştır.
- **NX_AUTO_IP_ANNOUNCE_NUM**: gönderileceği ARP duyurusu sayısı. Varsayılan olarak, bu değer 2 olarak tanımlanmıştır.
- **NX_AUTO_IP_ANNOUNCE_INTERVAL**: gönderme duyurusu arasında beklenecek saniye sayısı. Varsayılan olarak, bu değer 2 olarak tanımlanmıştır.
- **NX_AUTO_IP_DEFEND_INTERVAL**: savunma duyurusu arasında beklenecek saniye sayısı. Varsayılan olarak, bu değer 10 olarak tanımlanmıştır.