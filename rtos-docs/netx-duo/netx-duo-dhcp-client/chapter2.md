---
title: Bölüm 2 - NetX Duo DHCP Azure RTOS yükleme ve kullanma
description: Bu bölümde NetX Duo DHCP İstemcisi bileşeninin yüklenmesi, kurulumu ve kullanımıyla ilgili Azure RTOS bir açıklama yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 08f88f4501a7b44272111cbe5c14ee09474827b72a1239b334fb9d40e8093c51
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116788499"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-duo-dhcp-client"></a>Bölüm 2 - NetX Duo DHCP Azure RTOS yükleme ve kullanma

Bu bölümde NetX Duo DHCP İstemcisi bileşeninin yüklenmesi, kurulumu ve kullanımıyla ilgili Azure RTOS bir açıklama yer almaktadır.

## <a name="product-distribution"></a>Ürün Dağıtımı

Azure RTOS NetX Duo, genel kaynak kod depomuzdan <https://github.com/azure-rtos/netxduo> edinebilirsiniz. Paket aşağıdaki dosyaları içerir:

- **nxd_dhcp_client.h:** NetX Duo DHCP için üst bilgi dosyası
- **nxd_dhcp_client.c:** DHCP NetX Duo için C Kaynak dosyası
- **nxd_dhcp_client.pdf:** NetX Duo DHCP Için Kullanıcı Kılavuzu 
    - **demo_netxduo_dhcp.c**: NetX Duo DHCP İstemcisi gösterimi
    - **demo_netxduo_multihome_dhcp_client.c:** NetX Duo DHCP İstemcisi'nin birden çok arabirimde DHCP gösterimi

## <a name="dhcp-installation"></a>DHCP Yüklemesi

NetX Duo DHCP İstemcisini kullanmak için, daha önce bahsedilen dağıtımın tamamı NetX Duo'nın yüklü olduğu dizine kopyalanır. Örneğin,*"\threadx\arm7\green"* dizininde NetX Duo *yüklüyse, nxd_dhcp_client.h* ve *nxd_dhcp_client.c* dosyalarının bu dizine kopyalanmış olması gerekir.

## <a name="using-dhcp"></a>DHCP kullanma

NetX Duo için DHCP kullanmak kolaydır. Temel olarak, ThreadX ve NetX Duo'nxd_dhcp_client kullanmak için *uygulama kodunun tx_api.h* ve *nx_api.h*' yi içermesi gerekir.  Uygulama *nxd_dhcp_client.h* ekli olduktan sonra, uygulama kodu bu kılavuzun devamlarında belirtilen DHCP işlev çağrılarını mümkün hale gelecektir. Uygulamanın derleme sürecinde *nxd_dhcp_client.c'yi* de içermesi gerekir. Bu dosya, diğer uygulama dosyalarıyla aynı şekilde derlenmiş olmalı ve nesne formu uygulamanın dosyalarıyla birlikte bağlanacak. NetX DHCP kullanmak için gerekenlerin hepsi bu kadardır.

DHCP NetX Duo UDP hizmetlerini kullanıyorsa, DHCP'yi kullanmadan önce *UDP'nin nx_udp_enable* çağrısıyla etkinleştirilmesi gerektiğini unutmayın.

Daha önce atanmış bir IP adresi almak için, DHCP İstemcisi DHCP sunucusuna İstek iletisi ve Seçenek 50 "İstenen IP Adresi" ile DHCP işlemini başlatabilir. DHCP Sunucusu, IP adresini İstemciye verirse bir ACK iletisiyle veya reddederse bir NACK ile yanıt verir. İkinci durumda, DHCP İstemcisi BAŞLATMA durumunda DHCP işlemini bulma iletisiyle ve istenen IP adresiyle yeniden başlatıyor. Konak uygulaması önce DHCP İstemcisi'yi oluşturur, ardından dhcp işlemini *nx_dhcp_request_client_ip* ile başlatmadan önce istenen IP adresini ayarlamak için *nx_dhcp_start.* Daha fazla ayrıntı için bu belgenin başka bir yerinde örnek bir DHCP uygulaması sağlanır.

## <a name="in-the-bound-state"></a>Bağlı Durumda

DHCP İstemcisi bağlı durumdayken, DHCP İstemcisi iş parçacığı İstemci durumunu aralık başına bir kez (NX_DHCP_TIME_INTERVAL tarafından belirtilen şekilde) işler ve İstemciye atanan IP kirası üzerinde kalan süreyi kısar. Yenileme süresi sona erdiğinde DHCP İstemcisi durumu, İstemcinin DHCP Sunucusundan yenileme isteğide bulunduğu YenİLEME durumuna güncelleştirilir.

## <a name="sending-dhcp-messages-to-the-server"></a>Sunucuya DHCP iletileri gönderme

DHCP İstemcisi, konak uygulamanın DHCP Sunucusuna ileti göndermesine olanak sağlayan API hizmetleri içerir. Bu hizmetlerin, konak uygulamanın DHCP İstemci protokolünü el ile çalıştırması amaçlanmaz.

  - *nx_dhcp_release:* Bu, konak uygulama ağdan ayrılırken veya IP adresini geri isterken Sunucuya bir YAYıN iletisi gönderir.
  - *nx_dhcp_decline:* Ana bilgisayar uygulaması, DHCP İstemcisi'nin IP adresinin zaten kullanmakta olduğunu bağımsız olarak belirlerse Sunucuya bir REDDETME iletisi gönderir.
  - *nx_dhcp_forcerenew:* Bu, Sunucuya bir FORCERENEW iletisi gönderir
  - *nx_dhcp_send_request:* Bu, *nxd_dhcp_client.h* içinde belirtilen bir DHCP ileti türü bağımsız değişken olarak alır ve iletiyi Sunucuya gönderir. Bu öncelikle DHCP INFORM iletisi göndermek için tasarlanmıştır.

Bu [hizmetler hakkında daha fazla bilgi](chapter3.md) için bkz. DHCP Hizmetleri Açıklaması 

## <a name="starting-and-stopping-the-dhcp-client"></a>DHCP İstemcisini Başlatma ve Durdurma

Dhcp İstemcisi'nin sınırlayıcı bir durum elde yapılandırmasını durdurması için, konak uygulama *nx_dhcp_stop.*

Bir DHCP İstemcisini yeniden başlatmak için, konak uygulamanın önce yukarıda açıklanan nx_dhcp_stop DHCP *İstemcisini* durdurması gerekir. Ardından konak, DHCP *İstemcisini nx_dhcp_start* için çağrıyı çağırarak. Ana bilgisayar uygulaması önceki bir DHCP İstemci profilini (örneğin, başka bir ağ üzerinde önceki bir DHCP Sunucusundan alınan) temizlemek isterse, konak uygulama, nx_dhcp_reinitialize çağırmadan önce bu görevi dahili olarak gerçekleştirmek için *nx_dhcp_start.* 

Tipik bir sıra şöyle olabilir:

```c
nx_dhcp_stop(&my_dhcp);
nx_dhcp_reinitialize(&my_dhcp);
nx_dhcp_start(&my_dhcp);
```

Yalnızca tek bir DHCP arabiriminde çalışan DHCP uygulamaları için, DHCP İstemcisi'nin durdurulması DHCP İstemcisi zamanlayıcısını da devre dışı bıraktır. Bu nedenle artık IP kirası için kalan sürenin takip uzamaz. Belirli bir arabirimde DHCP İstemcisi'nin durdurulması DHCP İstemcisi zamanlayıcısını devre dışı bırakmaz, ancak bu arabirimde IP kiralamada kalan süreye kadar süreölçer güncelleştirmelerini durdurur

Bu nedenle, konak uygulamanın yeniden başlatılması veya ağ değiştirmesi gerektirdikçe DHCP İstemcisi'nin durdurulması tavsiye değildir.

## <a name="using-the-dhcp-client-with-auto-ip"></a>DHCP İstemcisini Otomatik IP ile Kullanma

NetX Duo DHCP İstemcisi, DHCP ve Otomatik IP'nin DHCP Sunucusunun kullanılabilir veya yanıt verme garantisine sahip olduğu bir adresi garanti eden uygulamalarda Otomatik IP protokolüyle eşzamanlı olarak çalışır. Ancak, ana bilgisayar bir Sunucu algılayamamışsa veya atanmış bir IP adresi alamasa, yerel IP adresi için Otomatik IP protokolüne geçiş olabilir. Ancak bunu yapmadan önce, Otomatik IP "yoklama" ve "savunma" aşamalarından geçirken DHCP İstemcisini geçici olarak durdurmanız tavsiye edilebilir. Ana bilgisayar için bir Otomatik IP adresi atandıktan sonra, DHCP İstemcisi yeniden başlatabilir ve bir DHCP Sunucusu kullanılabilir hale olursa, ana bilgisayar IP adresi uygulama çalışırken DHCP Sunucusu tarafından sunulan IP adresini kabul eder.

NetX Duo Auto IP'sinde, IP adresi değişikliği durumunda ana bilgisayar için etkinliklerini izlemesi için bir adres değişikliği bildirimi vardır.

## <a name="packet-chaining"></a>Paket Zinciri

Paket havuzu ve bellek kaynaklarının daha verimli kullanımı için, DHCP İstemcisi Ethernet sürücüsünden gelen zincirlenmiş paketleri (sürücü MTU'suna aşan veri birimleri) işebilir. Sürücü bu özelliğe sahipse, uygulama paketleri almak için paket havuzunu zorunlu bayt'ın altında NX_DHCP_PACKET_PAYLOAD ayarlayın. NX_DHCP_PACKET_PAYLOAD fiziksel ağ (genellikle Ethernet) çerçevesinin yanı sıra 548 bayt DHCP ileti verisi ve IP ve UDP barındırması gerekir.

Uygulamanın, PAKET İstemcisi'nin bir parçası olan ve DHCP iletilerini göndermek için kullanılan paket havuzu paket yükünü ve paket sayısını en iyi duruma getirmesini sağlar. Boyutu beklenen kullanım ve DHCP İstemcisi iletilerinin boyutuna göre iyileştirici olabilir.

## <a name="small-example-system"></a>Küçük Örnek Sistem

Aşağıdaki Şekil 1.1'de NetX Duo kullanma örneği gösterilmiştir. Uygulama iş parçacığı giriş işlevi "*my_thread_entry*" 101. satırda oluşturulur. Oluşturma başarılı olduktan sonra, DHCP işlemi 108. *nx_dhcp_start* çağrısıyla başlatılır. Bu noktada, DHCP İstemcisi iş parçacığı görevi ayrı olarak bir DHCP sunucusuyla iletişim kurmayı çalışır. Bu işlem sırasında uygulama kodu, 95. satırda *nx_ip_status_check* hizmeti (veya ikincil arabirim için nx_ip_interface_status_check) *kullanılarak GEÇERLI* bir IP adresinin IP örneğine kayıtlı olması için bekler. Bu daha yaygın olarak daha kısa bekleme seçeneği olan bir döngüde yapılır.

127. satırdan sonra DHCP geçerli bir IP adresi aldı ve uygulama, istenen Şekilde NetX Duo TCP/IP hizmetlerini kullanarak devam ediyor olabilir.

```c
#include   "tx_api.h"
#include   "nx_api.h"
#include   "nxd_dhcp_client.h"

#define     DEMO_STACK_SIZE         4096
TX_THREAD               my_thread;
NX_PACKET_POOL          my_pool;
NX_IP                   my_ip;
NX_DHCP                 my_dhcp;

/* Define function prototypes.  */

void    my_thread_entry(ULONG thread_input);
void    my_netx_driver(struct NX_IP_DRIVER_STRUCT *driver_req);

/* Define main entry point.  */
intmain()
{
  /* Enter the ThreadX kernel.  */
  tx_kernel_enter();
}

/* Define what the initial system looks like.  */
void    tx_application_define(void *first_unused_memory)
{

CHAR    *pointer;
UINT    status;
    
    /* Setup the working pointer.  */
    pointer =  (CHAR *) first_unused_memory;

    /* Create “my_thread”.  */
      tx_thread_create(&my_thread, "my thread", my_thread_entry, 0,  
                        pointer, DEMO_STACK_SIZE, 2, 2, 
                        TX_NO_TIME_SLICE, TX_AUTO_START);
    pointer =  pointer + DEMO_STACK_SIZE;

    /* Initialize the NetX Duo system.  */
    nx_system_initialize();

    /* Create a packet pool.  */
    status =  nx_packet_pool_create(&my_pool, "NetX Main Packet Pool", 
                                     1024, pointer, 64000);
    pointer = pointer + 64000;

    /* Check for pool creation error.  */
    if (status)
        error_counter++;

    /* Create an IP instance without an IP address. */
    status = nx_ip_create(&my_ip, "My NetX IP Instance", IP_ADDRESS(0,0,0,0), 
                          0xFFFFFF00, &my_pool, my_netx_driver, pointer, 
                          DEMO_STACK_SIZE, 1);
    pointer =  pointer + DEMO_STACK_SIZE;

    /* Check for IP create errors.  */
    if (status)
        error_counter++;

    /* Enable ARP and supply ARP cache memory for my IP Instance.  */
    status =  nx_arp_enable(&my_ip, (void *) pointer, 1024);
    pointer = pointer + 1024;

    /* Check for ARP enable errors.  */
    if (status)
        error_counter++;

    /* Enable UDP.  */
    status =  nx_udp_enable(&my_ip);
    if (status)
        error_counter++;
 }


 /* Define my thread.  */

 void    my_thread_entry(ULONG thread_input)
 {

 UINT        status;
 ULONG       actual_status;
 NX_PACKET   *my_packet;

    /* Wait for the link to come up.  */
    do
    {
    /* Get the link status.  */
        status =  nx_ip_status_check(&my_ip, NX_IP_LINK_ENABLED, 
                                     &actual_status, 100);
    } while (status != NX_SUCCESS);

    /* Create a DHCP instance.  */
    status =  nx_dhcp_create(&my_dhcp, &my_ip, "My DHCP");

    /* Check for DHCP create error.  */
    if (status)
        error_counter++;

    /* Start DHCP.  */
    nx_dhcp_start(&my_dhcp);

    /* Check for DHCP start error.  */
    if (status)
        error_counter++;

    /* Wait for IP address to be resolved through DHCP.  */
    nx_ip_status_check(&my_ip, NX_IP_ADDRESS_RESOLVED, 
                       (ULONG *) &status, 100000);

    /* Check to see if we have a valid IP address.  */
    if (status)
    {
      error_counter++;
      return;
    }
    else
    {

  /* Yes, a valid IP address is now on lease…  All NetX Duo
        services are available.
    }
 }

```
## <a name="multi-server-environments"></a>Çok Sunuculu Ortamlar

Birden fazla DHCP Sunucusu olan ağlarda, DHCP İstemcisi alınan ilk DHCP Sunucusu Teklifi iletiyi kabul eder, İstek durumuna ilerler ve alınan diğer teklifleri yoksayar.

## <a name="arp-probes"></a>ARP Araştırmaları

DHCP İstemcisi, IP adresinin zaten kullanım dışı olduğunu doğrulamak için DHCP Sunucusundan IP adresi ataması sonrasında bir veya daha fazla ARP araştırması gönderecek şekilde yalıtabilirsiniz. ARP yoklama adımı RFC 2131 tarafından önerilir ve birden fazla DHCP Sunucusuna sahip ortamlarda özellikle önemlidir. Konak uygulama NX_DHCP_CLIENT_SEND_ARP_PROBE seçeneğini sağlarsa (ek  ARP yoklama seçenekleri için Bölüm 2'de Yapılandırma Seçenekleri'ne bakın), DHCP İstemcisi bir 'kendi kendine adreslenen' ARP araştırması gönderir ve yanıt için belirtilen zamanı bekler. Hiçbiri alınmasa, DHCP İstemcisi Sınır durumuna ilerler. Bir yanıt alındı ise, DHCP İstemcisi adresin zaten kullanımda olduğunu varsayıyor. Otomatik olarak Sunucuya bir DECLINE iletisi gönderir ve INIT durumdan DHCP araştırmalarını yeniden başlatmak için İstemciyi yeniden başlatın. Bu, DHCP durum makinesini yeniden başlatılır ve İstemci Sunucuya başka bir DISCOVER iletisi gönderir.

## <a name="bootp-protocol"></a>BOOTP Protokolü

DHCP İstemcisi, BOOTP protokolünü ve DHCP protokolünü de destekler. Bu seçeneği etkinleştirmek ve DHCP yerine BOOTP kullanmak için, konak uygulamanın NX_DHCP_BOOTP_ENABLE ayarlaması gerekir. Konak uygulama, BOOTP protokolünde belirli IP adreslerini yine de talep ediyor olabilir. Ancak, BOOTP bazen bunu yapmak için kullandığı için DHCP İstemcisi ana bilgisayar işletim sisteminin yüklenmesini desteklemez.

## <a name="dhcp-on-a-secondary-interface"></a>İkincil Arabirimde DHCP

NetX Duo DHCP İstemcisi, varsayılan birincil arabirim yerine ikincil arabirimlerde çalıştırabilirsiniz.

NetX Duo DHCP İstemcisini ikincil bir ağ arabiriminde çalıştırmak için, konak uygulamanın DHCP İstemcisi'nin arabirim dizinini, nx_dhcp_set_interface_index API hizmetini *kullanarak ikincil arabirime ayarlaması* gerekir. Arabirim, nx_ip_interface_attach hizmeti kullanılarak birincil ağ *arabirimine nx_ip_interface_attach* gerekir. İkincil arabirimleri ekleme hakkında daha fazla bilgi için bkz. NetX Duo Kullanıcı Kılavuzu.

Aşağıda, konak uygulamanın ikincil arabiriminde DHCP sunucusuna bağlandığı örnek bir sistem (Şekil 1.2) verilmiştir. 65. satırda, ikincil arabirim IP görevine null IP adresiyle ekli olur. 104. satırda, DHCP İstemcisi örneği oluşturulduktan sonra, DHCP İstemcisi arabirim dizini, nx_dhcp_set_interface_index çağrılarak 1 olarak ayarlanır (örneğin, kendisi dizin 0 olan birincil arabirimden *uzaklığı).* Ardından DHCP İstemcisi, 108. satırda başlamaya hazırdır.

```c
#include   "tx_api.h"
#include   "nx_api.h"
#include   "nxd_dhcp_client.h"

#define     DEMO_STACK_SIZE         4096
TX_THREAD               my_thread;
NX_PACKET_POOL          my_pool;
NX_IP                   my_ip;
NX_DHCP                 my_dhcp;

/* Define function prototypes.  */

void    my_thread_entry(ULONG thread_input);
void    my_netx_driver(struct NX_IP_DRIVER_STRUCT *driver_req);

/* Define main entry point.  */

intmain()
{
  /* Enter the ThreadX kernel.  */
  tx_kernel_enter();
}


/* Define what the initial system looks like.  */

void    tx_application_define(void *first_unused_memory)
{

CHAR    *pointer;
UINT    status;

    /* Setup the working pointer.  */
    pointer =  (CHAR *) first_unused_memory;

    /* Create “my_thread”.  */
    tx_thread_create(&my_thread, "my thread", my_thread_entry, 0,  
                      pointer, DEMO_STACK_SIZE, 
                      2, 2, TX_NO_TIME_SLICE, TX_AUTO_START);
    pointer =  pointer + DEMO_STACK_SIZE;

    /* Initialize the NetX Duo system.  */
    nx_system_initialize();

  /* Create a packet pool.  */
    status =  nx_packet_pool_create(&my_pool, "NetX Main Packet Pool", 
                                     1024, pointer, 64000);
    pointer = pointer + 64000;

    /* Check for pool creation error.  */
    if (status)
        error_counter++;

    /* Create an IP instance without an IP address. */
    status = nx_ip_create(&my_ip, "My NetX IP Instance", IP_ADDRESS(0,0,0,0), 
                           0xFFFFFF00, &my_pool, my_netx_driver, pointer, STACK_SIZE, 1);
    pointer =  pointer + DEMO_STACK_SIZE;

    /* Check for IP create errors.  */
    if (status)
        error_counter++;

    status =  _nx_ip_interface_attach(&ip_0, "port_2", IP_ADDRESS(0, 0, 0,0), 
                                       0xFFFFFF00UL, my_netx_driver);

    /* Enable ARP and supply ARP cache memory for my IP Instance.  */
    status =  nx_arp_enable(&my_ip, (void *) pointer, 1024);
    pointer = pointer + 1024;

    /* Check for ARP enable errors.  */
    if (status)
        error_counter++;

    /* Enable UDP.  */
    status =  nx_udp_enable(&my_ip);
    if (status)
        error_counter++;
}


void    my_thread_entry(ULONG thread_input)
{

UINT        status;
ULONG       status;
NX_PACKET   *my_packet;

    /* Wait for the link to come up.  */
    do
    {
      /* Get the link status.  */
        status =  nx_ip_status_check(&my_ip,NX_IP_LINK_ENABLED,& status,100);
    } while (status != NX_SUCCESS);

    /* Create a DHCP instance.  */
    status =  nx_dhcp_create(&my_dhcp, &my_ip, "My DHCP");

    /* Check for DHCP create error.  */
    if (status)
        error_counter++;

    /* Set the DHCP client interface to the secondary interface. */
    status = nx_dhcp_set_interface_index(&my_dhcp, 1);


    /* Start DHCP.  */
    nx_dhcp_start(&my_dhcp);

    /* Check for DHCP start error.  */
    if (status)
        error_counter++;

    /* Wait for IP address to be resolved through DHCP.  */
    nx_ip_status_check(&my_ip, NX_IP_ADDRESS_RESOLVED, 
                       (ULONG *) &status, 100000);

    /* Check to see if we have a valid IP address.  */
    if (status)
    {
        error_counter++;
        return;
    }
    else
    {
    /* Yes, a valid IP address is now on lease…  All NetX Duo
        services are available.*/
    }
}
```

## <a name="dhcp-client-on-multiple-interfaces-simultaneously"></a>Aynı Anda Birden Çok Arabirimde DHCP İstemcisi

DHCP İstemcisini birden çok arabirimde çalıştırmak için *NX_MAX_PHYSICAL_INTERFACES.h'nx_api'daki* sanal ağların cihaza bağlı fiziksel arabirim sayısına ayarlanmış olması gerekir. Varsayılan olarak bu değer 1'tir (örneğin, birincil arabirim). IP örneğine ek bir arabirim kaydetmek için nx_ip_interface_attach *kullanın.* İkincil arabirimleri ekleme hakkında daha fazla bilgi için bkz. NetX Duo Kullanıcı Kılavuzu.

Sonraki adım, *NX_DHCP_CLIENT_MAX_RECORDS.h* nxd_dhcp_client DHCP'nin aynı anda çalışması beklenen en fazla arabirim sayısına ayarlamaktır. Bu NX_DHCP_CLIENT_MAX_RECORDS eşit olması gerek NX_MAX_PHYSICAL_INTERFACES. Örneğin, NX_MAX_PHYSICAL_INTERFACES 3 ve NX_DHCP_CLIENT_MAX_RECORDS 2 ' ye eşit olabilir. Bu yapılandırmada, yalnızca iki arabirim (ve herhangi bir zamanda üç fiziksel arabirimden herhangi biri olabilir), herhangi bir anda DHCP 'yi çalıştırabilir. DHCP Istemci kayıtları, ağ arabirimlerine bire bir eşleme içermez, örneğin, Istemci kaydı 1 fiziksel arabirim dizini 1 ile otomatik olarak bağıntılı değildir.

NX_DHCP_CLIENT_MAX_RECORDS Ayrıca, NX_MAX_PHYSICAL_INTERFACES daha büyük olarak ayarlanabilir ancak bu, kullanılmayan istemci kayıtları oluşturur ve belleğin verimsiz bir şekilde kullanılmasını sağlar.

Herhangi bir arabirimde DHCP 'yi başlatabilmeniz için, uygulamanın *nx_dhcp_interface_enable* çağırarak bu arabirimleri etkinleştirmesi gerekir. Özel durumun, *nx_dhcp_create* çağrısında otomatik olarak etkinleştirilen (ve aşağıda açıklanan *nx_dhcp_interface_disable* hizmeti kullanılarak devre dışı bırakılabilen) birincil arabirim olduğunu unutmayın.

Herhangi bir zamanda, bir arabirim DHCP için devre dışı bırakılabilir ve bu arabirimde DHCP çalıştıran diğer arabirimlerden bağımsız olarak durulabilirler.

Yukarıda belirtildiği gibi, DHCP için belirli bir arabirimi etkinleştirmek üzere *nx_dhcp_interface_enable* hizmetini kullanın ve giriş bağımsız değişkeninde fiziksel arabirim dizinini belirtin. NX_DHCP_CLIENT_MAX_RECORDS arabirimlerin tümü, arabirim dizini giriş bağımsız değişkeninin NX_MAX_PHYSICAL_INTERFACES daha az olduğu sınırlamasıyla etkinleştirilebilir.

Belirli bir arabirimde DHCP 'yi başlatmak için *nx_dhcp_interface_start* hizmetini kullanın. Tüm etkin arabirimlerde DHCP 'yi başlatmak için *nx_dhcp_start* hizmetini kullanın. (DHCP 'yi zaten Başlatan arabirimler *nx_dhcp_start* bundan etkilenmeyecektir.)

Bir arabirimdeki DHCP 'yi durdurmak için *nx_dhcp_interface_stop* hizmetini kullanın. DHCP, bu arabirim üzerinde zaten başlatılmış olmalıdır veya bir hata durumu döndürülür. Tüm etkinleştirilen arabirimlerde DHCP 'yi durdurmak için *nx_dhcp_stop* hizmetini kullanın. DHCP, diğer arabirimlerden bağımsız olarak herhangi bir zamanda durdurulabilir.

Var olan DHCP Istemci hizmetlerinin çoğu bir ' interface ' eşdeğerine sahiptir. *nx_dhcp_interface_release* , arabirime özgü *nx_dhcp_release eşdeğerdir.* DHCP Istemcisi tek bir arabirim için yapılandırılmışsa, aynı eylemi gerçekleştirir.

Arabirime özgü olmayan DHCP Istemci hizmetlerinin tipik olarak tüm arabirimlere uygulanacağını, ancak tümünün değil olduğunu unutmayın. İkinci durumda, arabirime özgü olmayan hizmet, arabirim kayıtlarının DHCP Istemci listesinde arama sırasında bulunan ilk DHCP etkin arabirimi için geçerlidir. DHCP için birden çok arabirim etkinleştirildiğinde arabirim temelli olmayan bir hizmetin nasıl gerçekleştirildiğinden ilgili üçüncü bölümde bulunan **hizmetlerin açıklamasına** bakın.

Aşağıdaki örnek dizide, IP örneğinin iki ağ arabirimi vardır ve ilk olarak ikincil arabirimde DHCP 'yi çalıştırır. Daha sonra bir süre sonra, birincil arabirimde DHCP başlatılır. Ardından birincil arabirimdeki IP adresini serbest bırakır ve birincil arabirimde DHCP 'yi yeniden başlatır:

```c
nx_dhcp_create(&my_dhcp_client); /* By default this enables primary interface for DHCP. */

nx_dhcp_interface_enable(&my_dhcp_client, 1); /* Secondary interface is enabled. */

nx_dhcp_interface_start(&my_dhcp_client, 1); /* DHCP is started on secondary interface. */

/* Some time later… */

nx_dhcp_interface_start(&my_dhcp_client, 0); /* DHCP is started on primary interface. */

nx_dhcp_interface_release(&my_dhcp_client, 0); /* Some time later… */

nx_dhcp_interface_start(&my_dhcp_client, 0); /* DHCP is restarted on primary interface. */
```

Arabirime özgü hizmetlerin tüm listesi için, Bölüm üçünde **hizmetlerin açıklamasına** bakın.

## <a name="configuration-options"></a>Yapılandırma seçenekleri

*Nxd_dhcp_client. h* içindeki kullanıcı yapılandırılabilir DHCP seçenekleri, ana bilgisayar uygulamasının belirli GEREKSINIMLERI Için DHCP istemcisini ince olarak değiştirmesine izin verir. Bu parametrelerin listesi aşağıda verilmiştir:  
  
- **NX_DHCP_ENABLE_BOOTP**: tanımlı, bu seçenek DHCP yerine BOOTP protokolünü etkinleştirmesine izin vermez. Varsayılan olarak bu seçenek devre dışıdır.
- **NX_DHCP_CLIENT_RESTORE_STATE**: tanımlanmışsa bu, DHCP istemcisinin, kira üzerinde kalan süre dahil olmak üzere geçerli DHCP istemci lisansını kaydetmesine ve bu durumu DHCP istemci uygulaması yeniden başlatmalar arasında geri yüklemesine olanak sağlar. Varsayılan değer devre dışıdır.
- **NX_DHCP_CLIENT_USER_CREATE_PACKET_POOL**: AYARLANıRSA, DHCP istemcisi kendi paket havuzunu oluşturmaz. Ana bilgisayar uygulamasının, DHCP Istemci paket havuzunu ayarlamak için *nx_dhcp_packet_pool_set* hizmetini kullanması gerekir. Varsayılan değer devre dışıdır.
- **NX_DHCP_CLIENT_SEND_ARP_PROBE**: tanımlı, bu DHCP istemcisinin, atanan DHCP adresinin başka bir konağa ait olmadığından emin olmak için IP adresi atamasından sonra bir ARP araştırması göndermesini sağlar. Varsayılan olarak, bu seçenek devre dışıdır.
- **NX_DHCP_ARP_PROBE_WAIT**: bir ARP araştırması GÖNDERDIKTEN sonra DHCP istemcisinin yanıt beklediği sürenin uzunluğunu tanımlar. Varsayılan değer bir saniye (1 * NX_IP_PERIODIC_RATE)
- **NX_DHCP_ARP_PROBE_MIN**: ARP araştırmaları gönderme arasındaki aralıkta bulunan minimum çeşitlemesi tanımlar. Değer 1 saniye olarak ayarlanır.
- **NX_DHCP_ARP_PROBE_MAX**: ARP araştırmaları gönderme arasındaki aralıktaki en yüksek çeşitleme tanımlar. Değer 2 saniyeye varsayılan olarak ayarlanır.
- **NX_DHCP_ARP_PROBE_NUM**: DHCP sunucusu tarafından atanan IP adresinin zaten kullanımda olup olmadığını belirlemek IÇIN gönderilen ARP araştırmaları sayısını tanımlar. Değer 3 yoklamalara göre varsayılan olarak ayarlanır.
- **NX_DHCP_RESTART_WAIT**: DHCP ISTEMCISINE atanan IP adresi zaten kullanımda Ise DHCP istemcisinin DHCP 'yi yeniden başlatması için bekleyeceği süreyi tanımlar. Değer, varsayılan olarak 10 saniyedir.
- **NX_DHCP_CLIENT_MAX_RECORDS**: DHCP istemci örneğine kaydedilecek en fazla arabirim kaydı sayısını belirtir. DHCP Istemci arabirimi kaydı, belirli bir arabirim üzerinde çalışan DHCP Istemcisinin kaydıdır. Varsayılan değer, fiziksel arabirimlerin sayısı (NX_MAX_PHYSICAL_INTERFACES) olarak ayarlanır.
- **NX_DHCP_CLIENT_SEND_MAX_DHCP_MESSAGE_OPTION**: TANıMLı, DHCP istemcisinin en fazla DHCP ileti boyutu seçeneğini göndermesini sağlar. Varsayılan olarak, bu seçenek devre dışıdır.
- **NX_DHCP_CLIENT_ENABLE_HOST_NAME_CHECK**: TANıMLı, DHCP istemcisinin, nx_dhcp_create çağrısındaki giriş ana bilgisayar adını geçersiz karakterler veya uzunlukla denetlemesini sağlar. Varsayılan olarak, bu seçenek devre dışıdır.
- **NX_DHCP_THREAD_PRIORITY**: DHCP iş parçacığının önceliği. Varsayılan olarak, bu değer DHCP iş parçacığının öncelik 3 ' te çalıştığını belirtir.
- **NX_DHCP_THREAD_STACK_SIZE**: DHCP iş parçacığı yığınının boyutu. Varsayılan olarak, boyut 2048 bayttır.
- **NX_DHCP_TIME_INTERVAL**: DHCP istemci Zamanlayıcı süre sonu işlevinin yürütüldüğü saniye cinsinden Aralık. Bu işlev, DHCP işlemindeki tüm zaman aşımlarını (örneğin, iletilerin yeniden veya DHCP Istemci durumunun değiştirilmesini) güncelleştirir. Varsayılan olarak, bu değer 1 saniyedir.
- **NX_DHCP_OPTIONS_BUFFER_SIZE**: DHCP seçenekleri arabelleğinin boyutu. Varsayılan olarak, bu değer 312 bayttır.
- **NX_DHCP_PACKET_PAYLOAD**: DHCP istemci paketi yükünün bayt cinsinden boyutunu belirtir. Varsayılan değer NX_DHCP_MINIMUM_IP_DATAGRAM + fiziksel üstbilgi boyutudur. Kablolu bir ağdaki fiziksel üst bilgi boyutu genellikle Ethernet çerçeve boyutudur.
- **NX_DHCP_PACKET_POOL_SIZE**: DHCP istemci paket havuzunun boyutunu belirtir. Varsayılan değer (5 * NX_DHCP_PACKET_PAYLOAD) olur. Bu, iç paket havuzu ek yükü için dört paket ve yer sağlar.
- **NX_DHCP_MIN_RETRANS_TIMEOUT**: iletiyi yeniden göndermeden önce istemci ILETISINE bir DHCP sunucusu yanıtı almak için en düşük bekleme seçeneğini belirtir. Varsayılan değer, RFC 2131 önerilen 4 saniyedir.
- **NX_DHCP_MAX_RETRANS_TIMEOUT**: ileti yeniden gönderilmeden önce istemci ILETISINE bir DHCP sunucusu yanıtı almak için en fazla bekleme seçeneğini belirtir. Varsayılan değer 64 saniyedir.
- **NX_DHCP_MIN_RENEW_TIMEOUT**: DHCP ISTEMCISI bir IP adresine bağlandıktan sonra bir DHCP sunucusu iletisi almak ve yenileme isteği göndermek için en az bekleme seçeneğini belirtir. Varsayılan değer 60 saniyedir. Ancak, DHCP Istemcisi en düşük yenileme zaman aşımını varsayılan olarak yapmadan önce DHCP sunucusu iletisinden yenileme ve yeniden bağlama süre sonu zamanlarını kullanır.
- **NX_DHCP_TYPE_OF_SERVICE**: DHCP UDP istekleri için gereken hizmet türü. Varsayılan olarak, bu değer normal IP paket hizmetini göstermek için NX_IP_NORMAL olarak tanımlanır.
- **NX_DHCP_FRAGMENT_OPTION**: DHCP UDP istekleri için parça etkinleştirilir. Varsayılan olarak, bu değer DHCP UDP fragmenting 'yi devre dışı bırakmak için NX_DONT_FRAGMENT.
- **NX_DHCP_TIME_TO_LIVE**: Bu paketin atılmadan önce geçebilmesi gereken yönlendirici sayısını belirtir. Varsayılan değer 0x80 olarak ayarlanır.
- **NX_DHCP_QUEUE_DEPTH**: en fazla alma kuyruğu derinliği sayısını belirtir. Varsayılan değer 4 ' e ayarlanır.