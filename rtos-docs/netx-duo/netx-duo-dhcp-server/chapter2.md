---
title: Bölüm 2-Azure RTOS NetX Duo DHCP sunucusunu yükleme ve kullanma
description: Bu bölümde, NetX Duo DHCP bileşeninin yüklenmesi, kurulumu ve kullanımı ile ilgili çeşitli sorunların bir açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/08/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 201e8b7e245539c1780ace4c3af4bc063a8485b3
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826111"
---
# <a name="chapter-2---installation-and-use-of-the-azure-rtos-netx-duo-dhcp-server"></a>Bölüm 2-Azure RTOS NetX Duo DHCP sunucusunu yükleme ve kullanma

Bu bölümde, NetX Duo DHCP bileşeninin yüklenmesi, kurulumu ve kullanımı ile ilgili çeşitli sorunların bir açıklaması yer almaktadır.

## <a name="product-distribution"></a>Ürün dağıtımı

NetX Duo DHCP sunucusu, adresinde bulunabilir [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo) . Paket, aşağıdaki gibi, bu belgeyi içeren iki kaynak dosya ve bir PDF dosyası içerir:

- **nxd_dhcp_server. h** NetX Duo DHCP sunucusu için üst bilgi dosyası
- **nxd_dhcp_server. c** NetX Duo DHCP sunucusu için C kaynak dosyası
- **nxd_dhcp_server.pdf** NetX Duo DHCP sunucusu için Kullanıcı Kılavuzu
- **demo_netxduo_dhcp. c** NetX Duo DHCP sunucusu gösterimi

## <a name="dhcp-installation"></a>DHCP yüklemesi

NetX Duo DHCP sunucusunu kullanabilmeniz için, daha önce bahsedilen dağıtımın tamamı NetX Duo 'un yüklü olduğu dizine kopyalanmalıdır. Örneğin, "*\threadx\arm7\green*" dizininde NETX Duo yüklüyse, *nxd_dhcp_server. h* ve *nxd_dhpc_server. c* dosyaları bu dizine kopyalanmalıdır.

## <a name="using-netx-duo-dhcp-server"></a>NetX Duo DHCP sunucusu kullanma

NetX Duo DHCP sunucusu kullanmak kolaydır. Temel olarak, uygulama kodu sırasıyla ThreadX ve NetX Duo kullanmak için *tx_api. h* ve *nx_api. h* dahil *nx_dhcp_server.* h içermelidir. *Nxd_dhcp_server. h* dahil olduğunda, uygulama kodu daha sonra bu KıLAVUZDA belirtilen DHCP işlev çağrılarını yapabilir. Uygulama, yapı işlemine *nxd_dhcp_server. c* de içermelidir. Bu dosya, diğer uygulama dosyalarıyla aynı şekilde derlenmelidir ve nesne formu, uygulamanın dosyalarıyla birlikte bağlanmalıdır. NetX Duo DHCP sunucusu kullanma hakkında daha fazla bilgi için, **NETX Duo** DHCP **sunucusunun** ve **NETX Duo DHCP sunucusunun kısıtlamalarına** yönelik aşağıdaki bölümlerde yer alan gereksinimlere bakın.

DHCP 'nin NetX Duo UDP hizmetlerini kullandığından önce, DHCP kullanmadan önce *nx_udp_enable* çağrısıyla UDP 'nin etkinleştirilmesi gerektiğini unutmayın.

## <a name="requirements-of-the-netx-duo-dhcp-server"></a>NetX Duo DHCP sunucusunun gereksinimleri

NetX Duo DHCP sunucusu, tanınmış DHCP bağlantı noktası 67 ' e atanmış bir UDP yuva bağlantı noktası gerektirir. Uygulama, DHCP sunucusunu oluşturmak için en az 548 bayt artı IP, UDP ve Ethernet üst bilgileri (4 baytlık hizalamayla toplam 44 bayt) ile birlikte paket yüküne sahip bir paket havuzu oluşturması gerekir.

Sunucu ve Istemcinin her ikisi de Ethernet donanım adresi ayarlarını kullandığı varsayılır:

- Donanım türü 1
- Donanım uzunluğu 6
- Atlamalar 0

### <a name="multiple-client-sessions"></a>Birden çok Istemci oturumu

NetX Duo DHCP sunucusu, etkin DHCP istemcilerinin bir tablosunu ve Istemcinin bir ' durum ' durumunu (örneğin, DHCP durumları INIT, önyükleme, seçme, ISTEME, yenıleme vb.) tutarak birden çok Istemci oturumunu idare edebilir. Bir sonraki Istemci iletisini almadan önce oturum zaman aşımı süresi dolarsa, Istemci bir IP kiralamaya bağlanmadığı müddetçe sunucu, Istemci oturumu verilerini temizler ve atanan IP adresini kullanılabilir havuza geri döndürür. Sunucu aynı Istemciden birden çok bulma iletisi alırsa, sunucu oturum zaman aşımını sıfırlar ve Istemcinin sonraki bir Istek iletisinde kabul etmesi için ayrılan IP adresini tutar.

NetX Duo DHCP sunucusu, tek durumlu Istemci DHCP isteğini de kabul eder, örneğin Istemci yalnızca bir Istek iletisi gönderir. Bu, Istemciye daha önce DHCP sunucusundan bir IP kirası atandığını varsayar.

### <a name="setting-interface-specific-network-parameters-server-responses"></a>Arabirime özgü ağ parametreleri sunucu yanıtları ayarlanıyor

Uygulama, *nx_dhcp_set_interface_network_parameters* HIZMETINI kullanarak DHCP istemci isteklerini işleyen her arabirim için yönlendirici, alt ağ MASKESI ve DNS sunucusu parametrelerini ayarlayabilir. Aksi takdirde bu parametreler, sırasıyla sunucunun birincil arabirimindeki IP ağ geçidine, DHCP ağ alt ağına ve DHCP sunucusu IP adresine varsayılan olarak ayarlanır.

DHCP sunucusu, DHCP istemcilerine gönderdiği DHCP iletilerinin seçenek verilerinde bu parametreleri içerir.

### <a name="assigning-ip-addresses-to-the-client"></a>Istemciye IP adresleri atama

Istemci bulma iletisi istenen bir IP adresi belirtmezse, DHCP sunucusu kendi havuzundan birini kullanabilir. Sunucuda kullanılabilir IP adresi yoksa, Istemciye bir NACK iletisi gönderir.

NetX Duo DHCP sunucusu, IP adresi kullanılabildiği ve sunucu IP adresi veritabanında bulunduğu sürece Istemci ISTEğI iletisinde istenen IP adresini verir. Uygulama, *nx_dhcp_create_server_ip_address_list* HIZMETINI kullanarak DHCP istemcilerine atamak için sunucunun kullanılabilir IP adresleri listesini oluşturur. Sunucuda istenen IP adresleri yoksa veya başka bir konağa atanırsa, Istemciye bir NACK iletisi gönderir.

DHCP sunucusu bir Istemci isteği aldığında, istemcinin DHCP iletisindeki Istemci MAC adresi alanındaki istemci MAC adresini benzersiz bir şekilde kullandığını tanımlar. Istemci MAC adresini değiştirirse veya başka bir alt ağa başka bir yere taşınmışsa, IP adresini kullanılabilir havuza geri döndürmek için sunucuya bir sürüm iletisi göndermelidir ve INIT durumunda yeni bir IP adresi istemeniz gerekir.

Ayrıntılar için **küçük örnek sistem** bölümünün Şekil 1,1 bölümüne bakın. DHCP sunucusu örneğine kaydedilen IP adresi sayısı, DHCP sunucusu denetim bloğunda sunucu adresi dizisinin boyutuyla sınırlıdır ve yapılandırılabilir seçenek NX_DHCP_IP_ADDRESS_MAX_LIST_SIZE tarafından tanımlanır.

### <a name="ip-address-lease-times"></a>IP adresi kiralama süreleri

Bu kira süresi, yapılandırılabilir seçenekte NX_DHCP_DEFAULT_LEASE_TIME tanımlanan sunucu varsayılan kira süresinden daha azsa, DHCP sunucusu, istek Istemci kira süresini de kabul eder. Istemciye atanan yenileme ve yeniden bağlama süreleri, kira süresi sonsuzluk (0xFFFFFFFF), bu durumda yenileme ve yeniden bağlama sürelerinin de sonsuz olarak ayarlandığı durumlar dışında %50 ve kira süresinin %85 ' dir.

### <a name="dhcp-server-timeouts"></a>DHCP sunucusu zaman aşımları

DHCP sunucusunda, oturum tamamlanana kadar bir sonraki DHCP Istemci iletisini beklemek için kullanıcı yapılandırılabilir bir oturum zaman aşımı NX_DHCP_CLIENT_SESSION_TIMEOUT vardır. Sunucu Istemciden sonraki iletiyi aldığında, daha önce gönderilen aynı ileti olup olmamasına bakılmaksızın zaman aşımı sıfırlanır.

### <a name="internal-error-handling"></a>İç hata işleme

DHCP sunucusu, *nx_dhcp_listen_for_messages* Işlevindeki DHCP istemci paketlerini alır ve işler. Bu işlev, paket geçersizse geçerli DHCP Istemci paketini işlemeye devam eder veya DHCP sunucusu bir iç hatayla karşılaşır. n *x_dhcp_listen_for_messages* bir hata durumu döndürür. DHCP sunucusu iş parçacığı, sonraki DHCP Istemci iletisini almak için bu işlevi çağırmadan önce ThreadX Scheduler ' ın her bir denetimini yeniden denetler. Geçerli sürümde, nx_dhcp_listen_for_messages hata durumu getirleri için günlük desteği yoktur *.*

### <a name="option-55-parameter-request-list"></a>Seçenek 55: parametre Istek listesi

NetX Duo DHCP sunucusunun, Istemciye geri ilettiği TEKLIF ve DHCPACK iletilerindeki parametre Isteği seçeneği (55) listesine yüklenecek bir seçenek kümesiyle yapılandırılması gerekir. Bu seçenekler, Istemci ağı için ağ açısından kritik yapılandırma verilerini içermeli ve varsayılan olarak yönlendirici IP adresi, alt ağ maskesi ve DNS sunucusu olarak tanımlanmıştır. Seçenek listesi, boşlukla ayrılmış bir liste ve Kullanıcı tarafından yapılandırılabilir NX_DHCP_DEFAULT_SERVER_OPTION_LIST tanımlı bir listesidir. Bu listede belirtilen seçeneklerin sayısı aynı zamanda Kullanıcı tanımlı NX_DHCP_DEFAULT_OPTION_LIST_SIZE eşit olmalıdır.

## <a name="constraints-of-the-netx-duo-dhcp-server"></a>NetX Duo DHCP sunucusunun kısıtlamaları

### <a name="dhcp-messages"></a>DHCP Iletileri

NetX Duo DHCP sunucusu, IP adresini Istemciye vermeden önce ağ üzerinde başka bir yerde bir IP adresi atanmamış olduğunu doğrulamaz. Birden çok DHCP sunucusu varsa, bu durum gerçekten olabilir. *RFC 2131 ' e kadar, IP adresinin ağda benzersiz olduğunu doğrulama* (örneğin, adrese ping) olduğu için istemcinin sorumluluğundadır. Değilse, sunucu, veritabanını Istemciden güncelleştirmek için IP adresine sahip bir reddetme iletisi almalıdır.

NetX Duo DHCP sunucusu FORCE_RENEW iletileri vermiyor. IP adresi kiralamasını yenilemek için DHCP Istemcisine kadar olur. Ancak, DHCP sunucusu, tüm atanan IP adreslerinde kalan süreyi veritabanında izler. Bir IP adresi kirası, IP adresinin kullanılabilir IP adresleri havuzuna döndürüldüğü zaman aşımına uğradığında. Bu nedenle, IP adresi kiralamasını etkin bir şekilde yenilemek/yeniden bağlamak için Istemciye sahip olur.

Istemci, bir IP kirasına (veya mevcut bir tane yenilendiğinde) verildiğinde ("bağlanır"), oturum verileri temizlenir. Istemci paketi sahte bir şekilde kanıtlar veya Istemci yanıtlar arasında zaman aşımına uğrarsa, oturum verileri temizlenir.

### <a name="saving-data-between-reboots"></a>Yeniden başlatmalar arasında veri kaydetme

NetX Duo DHCP sunucusu, DHCP isteği parametreleri de dahil olmak üzere Istemci verilerini bir Istemci kayıt tablosuna kaydeder. Bu tablo geçici olmayan bellekte depolanmaz. bu nedenle, DHCP sunucusu konağının yeniden başlatma işlemleri arasında kaydedilmez.

NetX Duo DHCP sunucusu IP adresi kiralama verilerini bir IP adresi tablosuna kaydeder. Bu tablo geçici olmayan bellekte depolanmaz. bu nedenle, DHCP sunucusu konağının yeniden başlatma işlemleri arasında kaydedilmez.

### <a name="relay-agents"></a>Geçiş aracıları

NetX Duo DHCP sunucusu, ağ DHCP isteklerini desteklemediğinden, ' Relay Agent ' alanı için sıfır bir IP adresi ile yapılandırılmış.

## <a name="small-example-system"></a>Küçük örnek sistem

NetX Duo DHCP sunucusunu kullanmanın ne kadar kolay olduğunu gösteren bir örnek, aşağıda görüntülenen Şekil 1,1 ' de açıklanmıştır. Bu örnekte, *nxd_dhcp_server. h* DHCP içerme dosyası 5. satırda getirilir. DHCP sunucu iş parçacığı yığın boyutu, IP iş parçacığı yığın boyutu ve test iş parçacığı yığın boyutu, 7-13 satırlarında tanımlanmıştır.

İlk olarak, DHCP sunucusunu durdurmak, yeniden başlatmak ve sonunda silmek için isteğe bağlı bir test iş parçacığı görevi 57 satırındaki "*test_thread_entry*" işleviyle oluşturulur. DHCP sunucu denetim bloğu "*dhcp_server*", 20. satırda genel değişken olarak tanımlanır. Sunucu paket havuzunun, en azından standart DHCP iletisi (548 bayt artı IP ve UDP başlık baytı) kadar büyük bir yüke sahip paketlerle oluşturulduğunu unutmayın. DHCP sunucusu için bir IP örneğini başarıyla oluşturduktan sonra, uygulama DHCP sunucusunu 96. satırda oluşturur. Daha sonra uygulama, sunucu IP örneğinin UDP etkin olmasını sağlar. DHCP sunucusunu başlatmadan önce, kullanılabilir IP adresi listesi **nx_dhcp_create_server_ip_address_list** hizmeti kullanılarak 137. satırda oluşturulur. Ağ yapılandırma parametreleri **nx_dhcp_set_interface_network_parameters** hizmeti kullanılarak aşağıdaki 138 satırında ayarlanır. uygulama, 141. satırdaki *Nx_dhcp_server_start* çağırdığında DHCP sunucusu hizmetleri kullanılabilir hale gelir. Test iş parçacığı görevi, DHCP sunucusunu durdurma ve yeniden başlatma kullanımını gösterir.

```C
/* This is a small demo of NetX Duo DHCP Server for the high-performance NetX Duo TCP/IP stack.  */

#include   "tx_api.h"
#include   "nx_api.h"
#include   "nxd_dhcp_server.h"

#define     DEMO_TEST_STACK_SIZE         2048
#define     DEMO_SERVER_STACK_SIZE  2048
#define     SERVER_IP_ADDRESS_LIST  "192.168.2.10 192.168.2.11 192.168.2.12"
#define     PACKET_PAYLOAD          1000
#define     PACKET_POOL_SIZE        (PACKET_PAYLOAD * 10)
#define     SERVER_IP_THREAD_STACK    2048


/* Define the ThreadX and NetX Duo Duo object control blocks...  */

TX_THREAD test_thread;
NX_PACKET_POOL server_pool;
NX_IP server_ip;
NX_DHCP_SERVER dhcp_server;


/* Define the counters used in the demo application...  */

ULONG state_changes;


/* Define thread prototypes.  */

void test_thread_entry(ULONG thread_input);
void nx_etherDriver_mcf5485(struct NX_IP_DRIVER_STRUCT *driver_req);


/* Define main entry point.  */

int main()
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

    /* Create the test thread.  */
    status = tx_thread_create(&test_thread, "test thread", test_thread_entry, 0,
            pointer, TEST_STACK_SIZE,  1, 1, TX_NO_TIME_SLICE, TX_DONT_START);

    if (status)
    {
        printf("Error with DHCP test thread create. Status 0x%x\r\n", status);
        return;
    }

    pointer =  pointer + DEMO_STACK_SIZE;

    /* Initialize the NetX Duosystem.  */
    nx_system_initialize();

    /* Create the DHCP Server packet pool.  */
    status =  nx_packet_pool_create(&server_pool, "NetX Main Packet Pool", PACKET_PAYLOAD,
        pointer, PACKET_POOL_SIZE);
    pointer = pointer + PACKET_POOL_SIZE;

    /* Check for pool creation error.  */
    if (status)
    {
        printf("Error with DHCP server packet pool create. Status 0x%x\r\n", status);
        return;
    }

    /* Create the DHCP Server IP instance.  */
    status = nx_ip_create(&server_ip, "NetX DHCP Server IP", NX_DHCP_SERVER_IP_ADDRESS,
        0xFFFFFF00UL,  &server_pool, nx_etherDriver_mcf5485, pointer,
        R_IP_THREAD_STACK, 1);

    pointer =  pointer + DEMO_IP_THREAD_STACK;

    /* Check for IP create errors.  */
    if (status)
    {
        printf("Error with DHCP server IP task create. Status 0x%x\r\n", status);
        return;
    }

    /* Create the DHCP Server instance.  */
    status =  nx_dhcp_server_create(&dhcp_server, &server_ip, pointer,
                                     DEMO_SERVER_STACK_SIZE,"DHCP Server", &server_pool);

    if (status)
    {
        printf("Error with DHCP server create. Status 0x%x\r\n", status);
        return;
    }

    pointer = pointer + DEMO_SERVER_STACK_SIZE;

    /* Enable ARP and supply ARP cache memory for IP Instance 0.  */
    status =  nx_arp_enable(&server_ip, (void *) pointer, 1024);
    pointer = pointer + 1024;

    /* Check for ARP enable errors.  */
    if (status)
    {
        printf("Error with ARP enable. Status 0x%x\r\n", status);
        return;
    }

    /* Enable UDP traffic.  */
    status =  nx_udp_enable(&server_ip);

    /* Check for UDP enable errors.  */
    if (status)
    {
        printf("Error with ICMP enable. Status 0x%x\r\n", status);
        return;
    }

    /* Enable ICMP to enable the ping utility.  */
    status =  nx_icmp_enable(&server_ip);

    /* Check for errors.  */
    if (status)
    {
        printf("Error with ICMP enable. Status 0x%x\r\n", status);
    }

   status = nx_dhcp_create_server_ip_address_list(&dhcp_server, iface_index,
                                 START_IP_ADDRESS_LIST, END_IP_ADDRESS_LIST, &addresses_added);

   status = nx_dhcp_set_interface_network_parameters(&dhcp_server, iface_index,
                               NX_DHCP_SUBNET_MASK, IP_ADDRESS(10,0,0,1),
                               IP_ADDRESS(10,0,0,1));

    /* Start the DHCP Server.  */
   status =  nx_dhcp_server_start(&dhcp_server);

    tx_thread_resume(&test_thread);
}

/* Define the test thread.  */
void    test_thread_entry(ULONG thread_input)
{
    UINT status;
    UINT keep_spinning;


    /* Just let the test thread be idle till we're ready to shut things down. */
    keep_spinning = 1;
    while(keep_spinning)
    {
        tx_thread_sleep(300);
    }

    printf("Stopping the server...\n");
    status = nx_dhcp_server_stop(&dhcp_server);
    if (status)
    {
        printf("Error with DHCP server stop. Status 0x%x\r\n", status);
        return;
    }

    tx_thread_sleep(500);

    printf("Starting the server...\n");
    status = nx_dhcp_server_start(&dhcp_server);
    if (status)
    {
        printf("Error with DHPC server start. Status 0x%x\r\n", status);
        return;
    }


    tx_thread_sleep(600);

    printf("Stopping the server for good...\n");
    status = nx_dhcp_server_stop(&dhcp_server);
    if (status)
    {
        printf("Error with DHCP server stop. Status 0x%x\r\n", status);
        return;
    }

    tx_thread_sleep(200);


    printf("Deleting the server...\n");
    status = nx_dhcp_server_delete(&dhcp_server);
    if (status)
    {
        printf("Error with DHCP server delete. Status 0x%x\r\n", status);
        return;
    }
}

```

**Şekil 1,1 örnek NetX Duo DHCP sunucusu uygulaması**

## <a name="configuration-options"></a>Yapılandırma seçenekleri

NetX Duo DHCP sunucusu oluşturmaya yönelik birkaç yapılandırma seçeneği vardır. Aşağıdaki listede her biri ayrıntılı açıklanmıştır:

- **NX_DISABLE_ERROR_CHECKING**: Bu seçenek temel DHCP hata denetimini kaldırır. Bu, genellikle uygulamanın hata ayıklaması yapıldıktan sonra kullanılır.
- **NX_DHCP_SERVER_THREAD_PRIORITY**: Bu seçenek, DHCP sunucusu iş parçacığının önceliğini belirtir. Varsayılan olarak, bu değer DHCP iş parçacığının öncelik 2 ' de çalıştığını belirtir.
- **NX_DHCP_TYPE_OF_SERVICE**: Bu seçenek, DHCP UDP istekleri için gereken hizmet türünü belirtir. Varsayılan olarak, bu değer normal IP paket hizmetini göstermek için NX_IP_NORMAL olarak tanımlanır.
- **NX_DHCP_FRAGMENT_OPTION**: DHCP UDP istekleri için parça etkinleştirilir. Varsayılan olarak, bu değer UDP fragmenting devre dışı bırakmak için NX_DONT_FRAGMENT olarak ayarlanır.
- **NX_DHCP_TIME_TO_LIVE**: paketin, atılmadan önce geçebilmesi gereken yönlendirici sayısını belirtir. Varsayılan değer 0x80 ' dır.
- **NX_DHCP_QUEUE_DEPTH**: DHCP sunucusu yuvasının kuyruğu kapatmadan önce sakladığı paketlerin sayısını belirtir. Varsayılan değer 5 ' tir.
- **NX_DHCP_PACKET_ALLOCATE_TIMEOUT**: NETX DHCP sunucusunun paket havuzundan bir paket ayırmasını bekleyeceği süre sonu zaman aşımını belirtir. Varsayılan değer NX_IP_PERIODIC_RATE olarak ayarlanır.
- **NX_DHCP_SUBNET_MASK** Bu, DHCP Istemcisinin ile yapılandırılması gereken alt ağ maskesidir. Varsayılan değer 0xFFFFFF00 olarak ayarlanır.
- **NX_DHCP_FAST_PERIODIC_TIME_INTERVAL**: Bu, DHCP sunucusu hızlı süreölçerinin, kalan oturum süresini denetlemesi ve zaman aşımına uğramış oturumları işlemek için zaman aşımı süresi.
- **NX_DHCP_SLOW_PERIODIC_TIME_INTERVAL**: Bu, DHCP sunucusu yavaş zamanlayıcının, kalan IP adresi kiralama süresini ve zaman aşımına uğradığını denetlemesini sağlayan Zamanlayıcı işaretleri cinsinden zaman aşımı süresi olur.
- **NX_DHCP_CLIENT_SESSION_TIMEOUT**: Bu zaman aşımı SÜRESI, DHCP sunucusunun sonraki DHCP istemci iletisini almak için bekleyeceği süre sonu dönecektir.
- **NX_DHCP_DEFAULT_LEASE_TIME**: Bu, DHCP istemcisine atanan sanıye cinsinden IP adresi kiralama süresi ve aynı zamanda istemciye atanan yenileme ve yeniden bağlama sürelerinin temelini oluşturur. Varsayılan değer 0xFFFFFFFF (Infinity) olarak ayarlanır.
- **NX_DHCP_IP_ADDRESS_MAX_LIST_SIZE**: Bu, istemciye atamaya YÖNELIK kullanılabilir IP adreslerini tutmak Için DHCP sunucusu dizisinin boyutudur. Varsayılan değer 20 ' dir.
- **NX_DHCP_CLIENT_RECORD_TABLE_SIZE**: Bu, istemci kayıtlarının TUTULMASı Için DHCP sunucusu dizisinin boyutudur. Varsayılan değer 50 ' dir.
- **NX_DHCP_CLIENT_OPTIONS_MAX**: Bu, geçerli oturumdaki parametre isteği listesinde istenen tüm seçenekleri tutmak Için DHCP istemci örneğindeki dizinin boyutudur. Varsayılan değer 12 ' dir.
- **NX_DHCP_OPTIONAL_SERVER_OPTION_LIST**: Bu, DHCP sunucusunun varsayılan seçenek listesini tutan, parametre istek LISTESINDEKI geçerli DHCP istemcisine tedarik eden tampondır. Varsayılan değer "1 3 6" dır.
- **NX_DHCP_OPTIONAL_SERVER_OPTION_SIZE**: Bu, DHCP sunucusunun varsayılan seçenek listesini tutan dizinin boyutudur. Varsayılan değer 3 ' dir.
- **NX_DHCP_SERVER_HOSTNAME_MAX**: Bu, sunucu ana bilgisayar adını tutan arabelleğin boyutudur. Varsayılan değer 32 ' dir.
- **NX_DHCP_CLIENT_HOSTNAME_MAX**: Bu, geçerli DHCP sunucusu Istemci oturumunda istemci ana bilgisayar adını tutan arabelleğin boyutudur. Varsayılan değer 32 ' dir.
