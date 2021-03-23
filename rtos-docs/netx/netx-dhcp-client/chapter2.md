---
title: Bölüm 2-Azure RTOS NetX DHCP Istemcisini yükleme ve kullanma
description: Bu bölümde, Azure RTOS NetX DHCP istemci bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların bir açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 9224a4df70b8199032066e30108250a3baeb65f5
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826800"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-dhcp-client"></a>Bölüm 2-Azure RTOS NetX DHCP Istemcisini yükleme ve kullanma

Bu bölümde, Azure RTOS NetX DHCP bileşeninin yüklenmesi, kurulumu ve kullanımı ile ilgili çeşitli sorunların bir açıklaması yer almaktadır.

## <a name="product-distribution"></a>Ürün dağıtımı

NetX için DHCP, adresinde bulunabilir [https://github.com/azure-rtos/netx](https://github.com/azure-rtos/netx) . Paket, aşağıdaki gibi, bu belgeyi içeren iki kaynak dosya ve bir PDF dosyası içerir:

- **nx_dhcp. h** NetX için DHCP üst bilgi dosyası

- **nx_dhcp. c** NetX için DHCP için C kaynak dosyası

- **nx_dhcp.pdf** NetX için DHCP 'nin PDF açıklaması

- **demo_netx_dhcp. c** NetX DHCP gösterimi

- **demo_netx_multihome_dhcp_client. c** NetX DHCP Istemci, birden çok arabirimde DHCP gösterimi

## <a name="dhcp-installation"></a>DHCP yüklemesi

NetX için DHCP kullanmak istiyorsanız, daha önce bahsedilen dağıtımın tamamı NetX 'in yüklü olduğu dizine kopyalanmalıdır. Örneğin, "*\threadx\arm7\green*" dizininde NETX yüklüyse, *nx_dhcp. h* ve *nx_dhcp. c* dosyaları bu dizine kopyalanmalıdır.

## <a name="using-dhcp"></a>DHCP kullanma

NetX için DHCP kullanmak kolaydır. Temel olarak, uygulama kodu sırasıyla ThreadX ve NetX kullanmak için *tx_api. h* ve *nx_api. h* dahil *nx_dhcp.* h içermelidir. *Nx_dhcp. h* dahil olduğunda, uygulama kodu daha sonra bu KıLAVUZDA belirtilen DHCP işlev çağrılarını yapabilir. Uygulama, yapı işlemine *nx_dhcp. c* de içermelidir. Bu dosya, diğer uygulama dosyalarıyla aynı şekilde derlenmelidir ve nesne formu, uygulamanın dosyalarıyla birlikte bağlanmalıdır. Bu, NetX DHCP 'yi kullanmak için gereklidir.

DHCP 'nin NetX UDP hizmetlerini kullandığından önce, DHCP kullanmadan önce *nx_udp_enable* çağrısıyla UDP 'nin etkinleştirilmesi gerektiğini unutmayın.

Daha önce atanmış bir IP adresi almak için DHCP Istemcisi, Istek iletisiyle DHCP işlemini başlatabilir ve "Istenen IP adresi" 50 seçeneğini DHCP sunucusuna alabilir. DHCP sunucusu, Istemcinin IP adresini veya reddederse bir NACK veriyorsa bir onay iletisiyle yanıt verir. İkinci durumda, DHCP Istemcisi başlangıç durumunda DHCP işlemini bulma iletisi ve istenen IP adresi olmadan yeniden başlatır. Ana bilgisayar uygulaması önce DHCP Istemcisini oluşturur, ardından *nx_dhcp_start* ile DHCP işlemini başlatmadan önce istenen IP adresini ayarlamak için *nx_dhcp_request_client_ip* API hizmetini çağırır. Daha fazla ayrıntı için bu belgede başka bir yerde örnek bir DHCP uygulaması sunulmaktadır.

## <a name="in-the-bound-state"></a>Bağlanma durumunda

DHCP istemcisi bağlı durumdayken, DHCP Istemci iş parçacığı, Istemci durumunu Aralık başına bir kez (NX_DHCP_TIME_INTERVAL tarafından belirtildiği gibi) işler ve Istemciye atanan IP kiralamasının kalan süresini azaltır. Yenileme süresi geçtiğinde, DHCP Istemci durumu Istemcinin DHCP sunucusundan yenileme isteyeceğini yenıleme durumuna güncelleştirilir.


## <a name="sending-dhcp-messages-to-the-server"></a>Sunucuya DHCP Iletileri gönderiliyor

DHCP Istemcisinde, ana bilgisayar uygulamasının DHCP sunucusuna ileti göndermesini sağlayan API hizmetleri vardır. Not Bu hizmetler, ana bilgisayar uygulamasının, DHCP Istemci iç durumunu güncelleştirmeden önce iletiyi ilk gönderdiklerinden, DHCP Istemci protokolünü el ile çalıştırmasına yönelik DEĞILDIR.

  - *nx_dhcp_release*: Bu, ana bilgisayar uygulaması ağdan çıkarken sunucuya bir sürüm iletisi gönderir veya bir IP adresini yeniden gerektirir.

  - *nx_dhcp_decline*: Ana bilgisayar UYGULAMASı, IP adresinin zaten KULLANıMDA olduğunu DHCP istemcisinden bağımsız olarak belirlerse sunucuya bir Red iletisi gönderir.

  - *nx_dhcp_forcerenew*: Bu, sunucuya bir FORCERENEW iletisi gönderir

  - *nx_dhcp_send_request*: bu, *nx_dhcp. h*' de belirtildiği gibi bir DHCP ileti türünde bağımsız değişken alır ve iletiyi sunucuya gönderir. Bu, öncelikli olarak DHCP BILDIR iletisini göndermek için tasarlanmıştır.

Bu belgenin başka bir yerinde bu hizmetler hakkında daha fazla bilgi için "*DHCP hizmetlerinin açıklaması*" başlığına bakın.

## <a name="starting-and-stopping-the-dhcp-client"></a>DHCP Istemcisini başlatma ve durdurma

DHCP Istemcisini, bağlantılı bir durum elde etmesinden bağımsız olarak durdurmak için, ana bilgisayar uygulaması *nx_dhcp_stop* çağırır.

Bir DHCP istemcisini yeniden başlatmak için, ana bilgisayar uygulamasının önce yukarıda açıklanan *nx_dhcp_stop* HIZMETINI kullanarak DHCP istemcisini durdurması gerekir. Daha sonra ana bilgisayar, DHCP Istemcisini sürdürmesini sağlamak için *nx_dhcp_start* çağırabilir. Ana bilgisayar uygulaması önceki bir DHCP Istemci profilini temizlemenizi istiyorsa (örneğin, başka bir ağdaki önceki bir DHCP sunucusundan elde edilen), ana bilgisayar uygulaması, nx_dhcp_start çağrılmadan önce bu görevi açmak için *nx_dhcp_reinitialize* çağırmalıdır.

Tipik bir sıra şu olabilir:

```C
nx_dhcp_stop(&my_dhcp);

nx_dhcp_reinitialize(&my_dhcp);

nx_dhcp_start(&my_dhcp);
```

Yalnızca tek bir DHCP arabiriminde çalışan DHCP uygulamaları için, DHCP Istemcisi durdurulduğunda DHCP ISTEMCI süreölçeri de etkinleştirilir. Bu nedenle, artık IP kiralamasının kalan süresini takip tutmayacaktır. Belirli bir arabirimdeki DHCP Istemcisinin durdurulması DHCP Istemci zamanlayıcısını devre dışı vermez, ancak Zamanlayıcı güncelleştirmelerini Bu arabirimdeki IP kirasında kalan süre için durdurur.

Bu nedenle, ana bilgisayar uygulaması yeniden başlatma veya ağ anahtarlama gerektirmediği takdirde DHCP Istemcisinin durdurulması önerilmez.

## <a name="using-the-dhcp-client-with-auto-ip"></a>DHCP Istemcisini otomatik IP ile kullanma

NetX DHCP Istemcisi, DHCP ve otomatik IP 'nin bir DHCP sunucusunun kullanılabilir veya yanıt verme garantisi olmadığı bir adresi garanti ettiği uygulamalarda otomatik IP protokolüyle aynı anda çalışıyor. Ancak, ana bilgisayar bir sunucu algılayamazsa veya atanmış bir IP adresi alamazsanız, yerel bir IP adresi için otomatik IP protokolüne geçiş yapabilir. Ancak bunu yapmadan önce, otomatik IP "araştırma" ve "savunma" aşamaları üzerinden geçtiğinde DHCP Istemcisinin geçici olarak durdurulması önerilir. Bir otomatik IP adresi konağa atandıktan sonra, DHCP Istemcisi yeniden başlatılabilir ve bir DHCP sunucusu kullanılabilir hale gelirse, ana bilgisayar IP adresi, uygulama çalışırken DHCP sunucusu tarafından sunulan IP adresini kabul edebilir.

NetX otomatik IP 'si, bir IP adresi değişikliği olayında etkinliklerini izlemek için ana bilgisayar için bir adres değişikliği bildirimine sahiptir.

## <a name="small-example-system"></a>Küçük örnek sistem

Aşağıdaki şekil 1,1 ' de NetX 'in nasıl kullanıldığını gösteren bir örnek. DHCP Istemcisi, 101 satırındaki "*my_thread_entry*" oluşturulur. Başarılı oluşturulduktan sonra DHCP işlemi, 108 satırındaki *nx_dhcp_start* çağrısında başlatılır. Bu noktada DHCP Istemci girişimleri DHCP sunucusuyla iletişim kurmak için başlatılır. Bu işlem sırasında, uygulama kodu 95 satırından başlayarak *nx_ip_status_check* hizmeti (veya ikincil bir arabirim için *NX_IP_INTERFACE_STATUS_CHECK* ) kullanılarak IP örneğine geçerli bir IP adresinin kaydedilmesini bekler. Bu, daha kısa bir bekleme seçeneğiyle bir döngüde daha yaygın olarak yapılır.

Satır 127 ' den sonra DHCP geçerli bir IP adresi aldıktan sonra, NetX TCP/IP hizmetlerinden yararlanarak istediğiniz gibi uygulama devam edebilir.

```C
#include  "tx_api.h"
#include  "nx_api.h"
#include  "nx_dhcp.h"

#define   DEMO_STACK_SIZE     4096
TX_THREAD        my_thread;
NX_PACKET_POOL     my_pool;
NX_IP          my_ip;
NX_DHCP         my_dhcp;

/* Define function prototypes. */

void  my_thread_entry(ULONG thread_input);
void  my_netx_driver(struct NX_IP_DRIVER_STRUCT *driver_req);

/* Define main entry point. */

intmain()
{

  /* Enter the ThreadX kernel. */
  tx_kernel_enter();
}


/* Define what the initial system looks like. */

void  tx_application_define(void *first_unused_memory)
{

CHAR  *pointer;
UINT  status;

  
  /* Setup the working pointer. */
  pointer = (CHAR *) first_unused_memory;

  /* Create “my_thread”. */
    tx_thread_create(&my_thread, "my thread", my_thread_entry, 0, 
            pointer, DEMO_STACK_SIZE, 
            2, 2, TX_NO_TIME_SLICE, TX_AUTO_START);
  pointer = pointer + DEMO_STACK_SIZE;

  /* Initialize the NetX system. */
  nx_system_initialize();

  /* Create a packet pool. */
  status = nx_packet_pool_create(&my_pool, "NetX Main Packet Pool", 
                     1024, pointer, 64000);
  pointer = pointer + 64000;

  /* Check for pool creation error. */
  if (status)
    error_counter++;

  /* Create an IP instance without an IP address. */
  status = nx_ip_create(&my_ip, "My NetX IP Instance", IP_ADDRESS(0,0,0,0), 
      0xFFFFFF00, &my_pool, my_netx_driver, pointer, 
      DEMO_STACK_SIZE, 1);
  pointer = pointer + DEMO_STACK_SIZE;

  /* Check for IP create errors. */
  if (status)
    error_counter++;

  /* Enable ARP and supply ARP cache memory for my IP Instance. */
  status = nx_arp_enable(&my_ip, (void *) pointer, 1024);
  pointer = pointer + 1024;

  /* Check for ARP enable errors. */
  if (status)
    error_counter++;

  /* Enable UDP. */
  status = nx_udp_enable(&my_ip);
  if (status)
    error_counter++;
}


/* Define my thread. */

void  my_thread_entry(ULONG thread_input)
{

UINT    status;
ULONG    actual_status;
NX_PACKET  *my_packet;

  /* Wait for the link to come up. */
  do
  {

    /* Get the link status. */
    status = nx_ip_status_check(&my_ip, NX_IP_LINK_ENABLED, 
                            &actual_status, 100);

  } while (status != NX_SUCCESS);

  /* Create a DHCP instance. */
  status = nx_dhcp_create(&my_dhcp, &my_ip, "My DHCP");

  /* Check for DHCP create error. */
  if (status)
    error_counter++;

  /* Start DHCP. */
  nx_dhcp_start(&my_dhcp);

  /* Check for DHCP start error. */
  if (status)
    error_counter++;

  /* Wait for IP address to be resolved through DHCP. */
  nx_ip_status_check(&my_ip, NX_IP_ADDRESS_RESOLVED, 
                        (ULONG *) &status, 100000);

  /* Check to see if we have a valid IP address. */
  if (status)
  {
    error_counter++;
    return;
  }
  else
  {

        /* Yes, a valid IP address is now on lease… All NetX
      services are available.
  }
}
```

Şekil 1,1 NetX ile DHCP kullanımı örneği

## <a name="multi-server-environments"></a>Çoklu sunucu ortamları

Birden çok DHCP sunucusunun bulunduğu ağlarda, DHCP Istemcisi, ilk alınan DHCP sunucusu teklif iletisini kabul eder, Istek durumuna ilerler ve diğer alınan teklifleri yoksayar.

## <a name="arp-probes"></a>ARP araştırmaları

DHCP Istemcisi, IP adresinin zaten kullanımda olmadığından emin olmak için DHCP sunucusundan IP adresi atamasından sonra bir veya daha fazla ARP araştırmaları gönderecek şekilde yapılandırılabilir. ARP araştırma adımı, RFC 2131 tarafından önerilir ve özellikle birden fazla DHCP sunucusuna sahip ortamlarda önemlidir. Ana bilgisayar uygulaması NX_DHCP_CLIENT_SEND_ARP_PROBE seçeneğini etkinleştirmesine izin verirseniz (ek ARP araştırma seçenekleri için bölümdeki **yapılandırma seçeneklerine** bakın), DHCP istemcisi ' kendine adreslenen ' bir ARP araştırması gönderir ve yanıt için belirtilen zamanı bekler. Hiçbiri alınmazsa, DHCP Istemcisi, bağlantılı duruma ilerletir. Yanıt alınmışsa, DHCP Istemcisi adresin zaten kullanımda olduğunu varsayar. Otomatik olarak sunucuya bir reddetme iletisi gönderir ve Istemciyi yeniden başlatarak başlangıç durumundan DHCP araştırmalarını yeniden başlatır. Bu, DHCP durum makinesini yeniden başlatır ve Istemci sunucuya başka bir bulma iletisi gönderir.

## <a name="bootp-protocol"></a>BOOTP Protokolü

DHCP Istemcisi Ayrıca, BOOTP protokolünü de destekler. Bu seçeneği etkinleştirmek ve DHCP yerine BOOTP 'yi kullanmak için, ana bilgisayar uygulamasının NX_DHCP_BOOTP_ENABLE yapılandırma seçeneğini ayarlaması gerekir. Ana bilgisayar uygulaması, BOOTP protokolünde belirli IP adresleri talep edebilir. Ancak, DHCP Istemcisi, bazı durumlarda BOOTP olarak kullanılmak üzere ana bilgisayar işletim sisteminin yüklenmesini desteklemez.

## <a name="dhcp-on-a-secondary-interface"></a>Ikincil bir arabirimde DHCP

NetX DHCP Istemcisi, varsayılan birincil arabirim yerine ikincil arabirimlerde çalıştırılabilir.

NetX DHCP Istemcisini ikincil bir ağ arabiriminde çalıştırmak için, konak uygulamanın, *nx_dhcp_set_interface_index* API HIZMETINI kullanarak DHCP istemcisinin arabirim dizinini ikincil arabirime ayarlaması gerekir. Arabirimin, *nx_ip_interface_attach* hizmeti kullanılarak birincil ağ arabirimine zaten eklenmiş olması gerekir. İkincil arabirimler ekleme hakkında daha fazla bilgi için bkz. NetX Kullanıcı Kılavuzu.

Şekil 1,2 ' de aşağıda, ana bilgisayar uygulamasının ikincil arabirimindeki DHCP sunucusuna bağlandığı örnek bir sistem bulunur. Satır 65 ' de, ikincil arabirim IP görevine null bir IP adresi ile iliştirilir. Satır 104 ' de, DHCP Istemci örneği oluşturulduktan sonra, *nx_dhcp_set_interface_index* çağırarak DHCP istemci arabirimi dizini 1 olarak ayarlanır (örneğin, birincil arabirimden kendisi dizin 0 ' dır). Ardından, DHCP Istemcisi, 108. satırda başlamaya hazırlanmaya başlamıştır.

```C
#include  "tx_api.h"
#include  "nx_api.h"
#include  "nx_dhcp.h"

#define   DEMO_STACK_SIZE     4096
TX_THREAD        my_thread;
NX_PACKET_POOL     my_pool;
NX_IP          my_ip;
NX_DHCP         my_dhcp;

/* Define function prototypes. */

void  my_thread_entry(ULONG thread_input);
void  my_netx_driver(struct NX_IP_DRIVER_STRUCT *driver_req);

/* Define main entry point. */

intmain()
{

  /* Enter the ThreadX kernel. */
  tx_kernel_enter();
}


/* Define what the initial system looks like. */

void  tx_application_define(void *first_unused_memory)
{

CHAR  *pointer;
UINT  status;

  
  /* Setup the working pointer. */
  pointer = (CHAR *) first_unused_memory;

  /* Create “my_thread”. */
    tx_thread_create(&my_thread, "my thread", my_thread_entry, 0, 
            pointer, DEMO_STACK_SIZE, 
            2, 2, TX_NO_TIME_SLICE, TX_AUTO_START);
  pointer = pointer + DEMO_STACK_SIZE;

  /* Initialize the NetX system. */
  nx_system_initialize();

  /* Create a packet pool. */
  status = nx_packet_pool_create(&my_pool, "NetX Main Packet Pool", 
                     1024, pointer, 64000);
  pointer = pointer + 64000;

  /* Check for pool creation error. */
  if (status)
    error_counter++;

  /* Create an IP instance without an IP address. */
  status = nx_ip_create(&my_ip, "My NetX IP Instance", IP_ADDRESS(0,0,0,0), 
       0xFFFFFF00, &my_pool, my_netx_driver, pointer, STACK_SIZE, 1);
  pointer = pointer + DEMO_STACK_SIZE;

  /* Check for IP create errors. */
  if (status)
    error_counter++;

  status = _nx_ip_interface_attach(&ip_0, "port_2", IP_ADDRESS(0, 0, 0,0), 
                            0xFFFFFF00UL, my_netx_driver);
                            
  /* Enable ARP and supply ARP cache memory for my IP Instance. */
  status = nx_arp_enable(&my_ip, (void *) pointer, 1024);
  pointer = pointer + 1024;

  /* Check for ARP enable errors. */
  if (status)
    error_counter++;

  /* Enable UDP. */
  status = nx_udp_enable(&my_ip);
  if (status)
    error_counter++;
}


void  my_thread_entry(ULONG thread_input)
{

UINT    status;
ULONG    status;
NX_PACKET  *my_packet;

  /* Wait for the link to come up. */
  do
  {

    /* Get the link status. */
    status = nx_ip_status_check(&my_ip,NX_IP_LINK_ENABLED,& status,100);
  } while (status != NX_SUCCESS);

  /* Create a DHCP instance. */
  status = nx_dhcp_create(&my_dhcp, &my_ip, "My DHCP");

  /* Check for DHCP create error. */
  if (status)
    error_counter++;

  /* Set the DHCP client interface to the secondary interface. 
    status = nx_dhcp_set_interface_index(&my_dhcp, 1);


  /* Start DHCP. */
  nx_dhcp_start(&my_dhcp);

  /* Check for DHCP start error. */
  if (status)
    error_counter++;

  /* Wait for IP address to be resolved through DHCP. */
  nx_ip_status_check(&my_ip, NX_IP_ADDRESS_RESOLVED, 
                        (ULONG *) &status, 100000);

  /* Check to see if we have a valid IP address. */
  if (status)
  {
    error_counter++;
    return;
  }
  else
  {

        /* Yes, a valid IP address is now on lease… All NetX
      services are available.
  }
}
```

Şekil 1,2 multihome desteğiyle NetX için DHCP örneği

## <a name="dhcp-client-on-multiple-interfaces-simultaneously"></a>Aynı anda birden çok arabirimde DHCP Istemcisi

DHCP Istemcisini birden çok arabirimde çalıştırmak için, *nx_api. h* içindeki NX_MAX_PHYSICAL_INTERFACES, cihaza bağlı olan fiziksel arabirimlerin sayısına ayarlanmalıdır. Varsayılan olarak, bu değer 1 ' dir (örn. birincil arabirim). IP örneğine ek bir arabirim kaydetmek için *nx_ip_interface_attach* hizmetini kullanın. İkincil arabirimler ekleme hakkında daha fazla bilgi için bkz. NetX Kullanıcı Kılavuzu.

Sonraki adım, *nx_dhcp. h* IÇINDEKI NX_DHCP_CLIENT_MAX_RECORDS DHCP 'yi aynı anda çalıştırmak için beklenen en fazla arabirim sayısına ayarlamaya yönelik olur. NX_DHCP_CLIENT_MAX_RECORDS NX_MAX_PHYSICAL_INTERFACES eşit olması gerekmediğini unutmayın. Örneğin, NX_MAX_PHYSICAL_INTERFACES 3 ve NX_DHCP_CLIENT_MAX_RECORDS 2 ' ye eşit olabilir. Bu yapılandırmada, yalnızca iki arabirim (ve herhangi bir zamanda üç fiziksel arabirimden herhangi biri olabilir), herhangi bir anda DHCP 'yi çalıştırabilir. DHCP Istemci kayıtları, ağ arabirimlerine bire bir eşleme içermez, örneğin, Istemci kaydı 1 fiziksel arabirim dizini 1 ile otomatik olarak bağıntılı değildir.

NX_DHCP_CLIENT_MAX_RECORDS Ayrıca, NX_MAX_PHYSICAL_INTERFACES daha büyük olarak ayarlanabilir ancak bu, kullanılmayan istemci kayıtları oluşturur ve belleğin verimsiz bir şekilde kullanılmasını sağlar.

Herhangi bir arabirimde DHCP 'yi başlatabilmeniz için, uygulamanın *nx_dhcp_interface_enable* çağırarak bu arabirimleri etkinleştirmesi gerekir. Özel durumun, *nx_dhcp_create* çağrısında otomatik olarak etkinleştirilen (ve aşağıda açıklanan *nx_dhcp_interface_disable* hizmeti kullanılarak devre dışı bırakılabilen) birincil arabirim olduğunu unutmayın.

Herhangi bir zamanda, bir arabirim DHCP için devre dışı bırakılabilir ve bu arabirimde DHCP çalıştıran diğer arabirimlerden bağımsız olarak durulabilirler.

Yukarıda belirtildiği gibi, DHCP için belirli bir arabirimi etkinleştirmek üzere *nx_dhcp_interface_enable* hizmetini kullanın ve giriş bağımsız değişkeninde fiziksel arabirim dizinini belirtin. NX_DHCP_CLIENT_MAX_RECORDS arabirimlerin tümü, arabirim dizini giriş bağımsız değişkeninin NX_MAX_PHYSICAL_INTERFACES daha az olduğu sınırlamasıyla etkinleştirilebilir.

Belirli bir arabirimde DHCP 'yi başlatmak için *nx_dhcp_interface_start* hizmetini kullanın. Tüm etkin arabirimlerde DHCP 'yi başlatmak için *nx_dhcp_start* hizmetini kullanın. (DHCP 'yi zaten Başlatan arabirimler *nx_dhcp_start* bundan etkilenmeyecektir.)

Bir arabirimdeki DHCP 'yi durdurmak için *nx_dhcp_interface_stop* hizmetini kullanın. DHCP, bu arabirim üzerinde zaten başlatılmış olmalıdır veya bir hata durumu döndürülür. Tüm etkinleştirilen arabirimlerde DHCP 'yi durdurmak için *nx_dhcp_stop* hizmetini kullanın. DHCP, diğer arabirimlerden bağımsız olarak herhangi bir zamanda durdurulabilir.

Var olan DHCP Istemci hizmetlerinin çoğu bir ' interface ' eşdeğerine sahiptir. *nx_dhcp_interface_release* , arabirime özgü *nx_dhcp_release eşdeğerdir.* DHCP Istemcisi tek bir arabirim için yapılandırılmışsa, aynı eylemi gerçekleştirir.

Arabirime özgü olmayan DHCP Istemci hizmetlerinin tipik olarak tüm arabirimlere uygulanacağını, ancak tümünün değil olduğunu unutmayın. İkinci durumda, arabirime özgü olmayan hizmet, arabirim kayıtlarının DHCP Istemci listesinde arama sırasında bulunan ilk DHCP etkin arabirimi için geçerlidir. DHCP için birden çok arabirim etkinleştirildiğinde arabirim temelli olmayan bir hizmetin nasıl gerçekleştirildiğinden ilgili üçüncü bölümde bulunan **hizmetlerin açıklamasına** bakın.

Aşağıdaki örnek dizide, IP örneğinin iki ağ arabirimi vardır ve ilk olarak ikincil arabirimde DHCP 'yi çalıştırır. Daha sonra bir süre sonra, birincil arabirimde DHCP başlatılır. Ardından birincil arabirimdeki IP adresini serbest bırakır ve birincil arabirimde DHCP 'yi yeniden başlatır:

```C
nx_dhcp_create(&my_dhcp_client);
/* By default this enables primary interface for DHCP. */

nx_dhcp_interface_enable(&my_dhcp_client, 1); 
/* Secondary interface is enabled. */

nx_dhcp_interface_start(&my_dhcp_client, 1); 
/* DHCP is started on secondary interface. */

/* Some time later… */

nx_dhcp_interface_start(&my_dhcp_client, 0); 
/* DHCP is started on primary interface. */

nx_dhcp_interface_release(&my_dhcp_client, 0); 

/* Some time later… */

nx_dhcp_interface_start(&my_dhcp_client, 0); 
/* DHCP is restarted on primary interface. */
```

Arabirime özgü hizmetlerin tüm listesi için, Bölüm üçünde **hizmetlerin açıklamasına** bakın.

## <a name="configuration-options"></a>Yapılandırma seçenekleri

*Nx_dhcp. h* içindeki kullanıcı yapılandırılabilir DHCP seçenekleri, ana bilgisayar uygulamasının belirli GEREKSINIMLERI Için DHCP istemcisini ince olarak değiştirmesine izin verir. Bu parametrelerin listesi aşağıda verilmiştir:  
  
- **NX_DHCP_ENABLE_BOOTP** Tanımlı, bu seçenek DHCP yerine BOOTP protokolünü sunar. Varsayılan olarak bu seçenek devre dışıdır.

- **NX_DHCP_CLIENT_RESTORE_STATE** Bu, tanımlanmazsa, DHCP Istemcisinin, kira üzerinde kalan süre dahil olmak üzere geçerli DHCP Istemci lisansını kaydetmesine ve bu durumu DHCP Istemci uygulaması yeniden başlatmalar arasında geri yüklemesine olanak sağlar. Varsayılan değer devre dışıdır.

- **NX_DHCP_CLIENT_USER_CREATE_PACKET_POOL** Ayarlanırsa, DHCP Istemcisi kendi paket havuzunu oluşturmaz. Ana bilgisayar uygulamasının, DHCP Istemci paket havuzunu ayarlamak için nx_dhcp_packet_pool_set hizmetini kullanması gerekir. Varsayılan değer devre dışıdır.

- **NX_DHCP_CLIENT_SEND_ARP_PROBE** Bu, DHCP Istemcisinin atanmış DHCP adresinin başka bir konağa ait olmadığından emin olmak için IP adresi atamasından sonra bir ARP araştırması göndermesini sağlar. Varsayılan olarak, bu seçenek devre dışıdır.

- **NX_DHCP_ARP_PROBE_WAIT** Bir ARP araştırması gönderdikten sonra DHCP Istemcisinin yanıt beklediği sürenin uzunluğunu tanımlar. Varsayılan değer bir saniye (1 * NX_IP_PERIODIC_RATE)

- **NX_DHCP_ARP_PROBE_MIN** ARP araştırmaları gönderme arasındaki aralıkta bulunan en küçük çeşitlemesi tanımlar. Değer 1 saniye olarak ayarlanır.

- **NX_DHCP_ARP_PROBE_MAX** ARP araştırmaları gönderme arasındaki aralıktaki en yüksek çeşitleme tanımlar. Değer 2 saniyeye varsayılan olarak ayarlanır.

- **NX_DHCP_ARP_PROBE_NUM** DHCP sunucusu tarafından atanan IP adresinin zaten kullanımda olup olmadığını belirlemek için gönderilen ARP araştırmaları sayısını tanımlar. Değer 3 yoklamalara göre varsayılan olarak ayarlanır.

- **NX_DHCP_RESTART_WAIT** DHCP istemcisine atanan IP adresi zaten kullanımda ise DHCP Istemcisinin DHCP 'yi yeniden başlatması için bekleyeceği süreyi tanımlar. Değer, varsayılan olarak 10 saniyedir.

- **NX_DHCP_CLIENT_MAX_RECORDS** DHCP Istemci örneğine kaydedilecek en fazla arabirim kaydı sayısını belirtir. DHCP Istemci arabirimi kaydı, belirli bir arabirim üzerinde çalışan DHCP Istemcisinin kaydıdır. Varsayılan değer, fiziksel arabirimlerin sayısı (NX_MAX_PHYSICAL_INTERFACES) olarak ayarlanır.

- **NX_DHCP_CLIENT_SEND_MAX_DHCP_MESSAGE_OPTION** Bu, DHCP Istemcisinin en fazla DHCP ileti boyutu seçeneğini göndermesini sağlar. Varsayılan olarak, bu seçenek devre dışıdır.

- **NX_DHCP_CLIENT_ENABLE_HOST_NAME_CHECK** Bu, DHCP Istemcisinin, nx_dhcp_create çağrısındaki giriş ana bilgisayar adını geçersiz karakterler veya uzunlukla denetlemesini sağlar. Varsayılan olarak, bu seçenek devre dışıdır.

- **NX_DHCP_THREAD_PRIORITY** DHCP iş parçacığının önceliği. Varsayılan olarak, bu değer DHCP iş parçacığının öncelik 3 ' te çalıştığını belirtir.

- **NX_DHCP_THREAD_STACK_SIZE** DHCP iş parçacığı yığınının boyutu. Varsayılan olarak, boyut 2048 bayttır.

- **NX_DHCP_TIME_INTERVAL** DHCP Istemci Zamanlayıcı süre sonu işlevinin yürütüldüğü saniye cinsinden Aralık. Bu işlev, DHCP işlemindeki tüm zaman aşımlarını (örneğin, iletilerin yeniden veya DHCP Istemci durumunun değiştirilmesini) güncelleştirir. Varsayılan olarak, bu değer 1 saniyedir.

- **NX_DHCP_OPTIONS_BUFFER_SIZE** DHCP seçenekleri arabelleğinin boyutu. Varsayılan olarak, bu değer 312 ' dir.

- **NX_DHCP_PACKET_PAYLOAD** DHCP Istemci paketi yükünün bayt cinsinden boyutunu belirtir. Varsayılan değer NX_DHCP_MINIMUM_IP_DATAGRAM + fiziksel üstbilgi boyutudur. Kablolu bir ağdaki fiziksel üst bilgi boyutu genellikle Ethernet çerçeve boyutudur.

- **NX_DHCP_PACKET_POOL_SIZE** DHCP Istemci paket havuzunun boyutunu belirtir. Varsayılan değer (5 * NX_DHCP_PACKET_PAYLOAD) olur. Bu, iç paket havuzu ek yükü için dört paket ve yer sağlar.

- **NX_DHCP_MIN_RETRANS_TIMEOUT** İletiyi yeniden göndermeden önce istemci iletisine bir DHCP sunucusu yanıtı almak için en düşük bekleme seçeneğini belirtir. Varsayılan değer, RFC 2131 önerilen 4 saniyedir.

- **NX_DHCP_MAX_RETRANS_TIMEOUT** İletiyi yeniden göndermeden önce istemci iletisine bir DHCP sunucusu yanıtı almak için en fazla bekleme seçeneğini belirtir. Varsayılan değer, RFC 2131 önerilen 64 saniyedir.

- **NX_DHCP_MIN_RENEW_TIMEOUT** DHCP Istemcisi bir IP adresine bağlandıktan sonra bir DHCP sunucusu iletisi almak ve yenileme isteği göndermek için en az bekleme seçeneğini belirtir. Varsayılan değer 60 saniyedir. Ancak, DHCP Istemcisi en düşük yenileme zaman aşımını varsayılan olarak yapmadan önce DHCP sunucusu iletisinden yenileme ve yeniden bağlama süre sonu zamanlarını kullanır.

- **NX_DHCP_TYPE_OF_SERVICE** DHCP UDP istekleri için gereken hizmet türü. Varsayılan olarak, bu değer normal IP paket hizmetini göstermek için NX_IP_NORMAL olarak tanımlanır.

- **NX_DHCP_FRAGMENT_OPTION** DHCP UDP istekleri için parça etkinleştirme. Varsayılan olarak, bu değer DHCP UDP fragmenting 'yi devre dışı bırakmak için NX_DONT_FRAGMENT.

- **NX_DHCP_TIME_TO_LIVE** Bu paketin, atılmadan önce geçebilmesi gereken yönlendirici sayısını belirtir. Varsayılan değer 0x80 olarak ayarlanır.

- **NX_DHCP_QUEUE_DEPTH** Alma kuyruğunun en yüksek derinlik sayısını belirtir. Varsayılan değer 4 ' e ayarlanır.
