---
title: Bölüm 2 - NetX Duo DHCP Sunucusu'Azure RTOS Yükleme ve Kullanma
description: Bu bölümde NetX Duo DHCP bileşeninin yüklenmesi, kurulumu ve kullanımıyla ilgili çeşitli sorunların açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/08/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: aed0b61e595666e834a269911a261b36d10f46069d587ee1be1ec64e143360e9
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116790335"
---
# <a name="chapter-2---installation-and-use-of-the-azure-rtos-netx-duo-dhcp-server"></a>Bölüm 2 - NetX Duo DHCP Azure RTOS yükleme ve kullanma

Bu bölümde NetX Duo DHCP bileşeninin yüklenmesi, kurulumu ve kullanımıyla ilgili çeşitli sorunların açıklaması yer almaktadır.

## <a name="product-distribution"></a>Ürün Dağıtımı

NetX Duo DHCP Sunucusu şu adreste [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo) kullanılabilir: . Paket, aşağıdaki gibi iki kaynak dosya ve bu belgeyi içeren bir PDF dosyası içerir:

- **nxd_dhcp_server.h** NetX Duo DHCP Sunucusu için üst bilgi dosyası
- **nxd_dhcp_server.c** NetX Duo DHCP Sunucusu için C Kaynak dosyası
- **nxd_dhcp_server.pdf** NetX Duo DHCP Sunucusu için Kullanıcı Kılavuzu
- **demo_netxduo_dhcp.c** NetX Duo DHCP Sunucusu gösterimi

## <a name="dhcp-installation"></a>DHCP Yüklemesi

NetX Duo DHCP Sunucusunu kullanmak için daha önce bahsedilen dağıtımın tamamı NetX Duo'nın yüklü olduğu dizine kopyalanır. Örneğin,*"\threadx\arm7\green"* dizininde NetX Duo *yüklüyse, nxd_dhcp_server.h* ve *nxd_dhpc_server.c* dosyalarının bu dizine kopyalanmış olması gerekir.

## <a name="using-netx-duo-dhcp-server"></a>NetX Duo DHCP Sunucusu Kullanma

NetX Duo DHCP Sunucusunu kullanmak kolaydır. Temel olarak, ThreadX ve NetX Duo'nx_dhcp_server kullanmak için uygulama kodu *tx_api.h* ve *nx_api.h*'yi içeren *nx_dhcp_server.h'yi* içermesi gerekir. Uygulama *nxd_dhcp_server.h* ekli olduktan sonra, uygulama kodu bu kılavuzun ilerleyen adımlarında belirtilen DHCP işlev çağrılarını da tamamlar. Uygulamanın derleme sürecinde *nxd_dhcp_server.c'yi* de içermesi gerekir. Bu dosya, diğer uygulama dosyalarıyla aynı şekilde derlenmiş olmalı ve nesne formu uygulamanın dosyalarıyla birlikte bağlanacak. NetX Duo DHCP Sunucusu kullanma hakkında daha fazla bilgi **için, Aşağıdaki Bölümlere Bakın: NetX Duo DHCP**  Sunucusunun Gereksinimleri ve NetX Duo DHCP Sunucusunun **Kısıtlamaları.**

DHCP NetX Duo UDP hizmetlerini kullanıyorsa, DHCP'yi kullanmadan önce *UDP'nin nx_udp_enable* çağrısıyla etkinleştirilmesi gerektiğini unutmayın.

## <a name="requirements-of-the-netx-duo-dhcp-server"></a>NetX Duo DHCP Sunucusunun Gereksinimleri

NetX Duo DHCP Sunucusu, iyi bilinen DHCP bağlantı noktası 67'ye atanmış bir UDP yuva bağlantı noktası gerektirir. DHCP Sunucusunu oluşturmak için uygulamanın en az 548 bayt artı IP, UDP ve Ethernet üst bilgileriyle (4 bayt hizalamalı toplam 44 bayt) paket yüküne sahip bir paket havuzu oluşturması gerekir.

Sunucu ve İstemcinin her ikisinin de Ethernet donanım adresi ayarlarını kullanıyor olduğu varsayılır:

- Donanım türü 1
- Donanım uzunluğu 6
- Atlamalar 0

### <a name="multiple-client-sessions"></a>Birden Çok İstemci Oturumu

NetX Duo DHCP Sunucusu, etkin DHCP istemcilerinin bir tabloyu ve İstemcinin hangi "durum" içinde olduğunu (örneğin, INIT, BOOT, SELECTING, REQUESTING, RENEWING vb.) tutarak birden çok İstemci oturumlarını işebilir. İstemci bir IP kirası bağlı değilse, sonraki İstemci iletisi alınmadan önce oturum zaman aşımı süresi dolsa, Sunucu İstemci oturum verilerini temizler ve atanan IP adresini kullanılabilir havuza geri gönderir. Sunucu aynı İstemciden birden çok DISCOVER iletisi alıyorsa, Sunucu oturum zamanlarını sıfırlar ve İstemcinin sonraki bir REQUEST iletisinde kabul etmek için ayrılmış IP adresini tutar.

NetX Duo DHCP Sunucusu, tek durum istemci DHCP isteğini de kabul eder, örneğin İstemci yalnızca bir REQUEST iletisi gönderir. Bu, İstemciye daha önce DHCP sunucusundan bir IP kirası atandığı varsayılan bir durumdur.

### <a name="setting-interface-specific-network-parameters-server-responses"></a>Arabirime Özgü Ağ Parametrelerini Sunucu Yanıtlarını Ayarlama

Uygulama, dhcp istemcisi isteklerini işlemektedir her arabirim için yönlendirici, alt ağ maskesi ve DNS sunucusu *parametrelerini* nx_dhcp_set_interface_network_parameters oluşturabilir. Aksi takdirde bu parametreler sırasıyla Sunucunun birincil arabiriminde, DHCP ağ alt ağına ve DHCP Sunucusu IP adresine varsayılan olarak IP ağ geçidi olarak kullanılır.

DHCP sunucusu, DHCP istemcilerine gönderdiği DHCP iletilerinin seçenek verilerine bu parametreleri içerir.

### <a name="assigning-ip-addresses-to-the-client"></a>İstemciye IP adresleri atama

İstemci BULMA iletisi istenen bir IP adresini belirtmezseniz, DHCP Sunucusu kendi havuzundan bir IP adresi kullanabilir. Sunucuda kullanılabilir IP adresi yoksa İstemciye bir NACK iletisi gönderir.

Ip adresi kullanılabilir olduğu ve Sunucu IP adresi veritabanında buluna sürece NetX Duo DHCP Sunucusu, istenen IP adresini İstemci İsteği iletisinde verir. Uygulama, nx_dhcp_create_server_ip_address_list hizmetini kullanarak DHCP İstemcilerine atamak için Sunucunun *kullanılabilir IP adresleri nx_dhcp_create_server_ip_address_list* oluşturur. Sunucuda istenen IP adresleri yoksa veya başka bir ana bilgisayar atanmışsa İstemciye bir NACK iletisi gönderir.

DHCP Sunucusu bir İstemci isteği aldığında, İstemcinin DHCP iletisinde İstemci MAC adresi alanında İstemci MAC adresini benzersiz olarak kullanarak olduğunu tanımlar. İstemci, MAC adresini değiştirirse veya başka bir alt ağ üzerine taşınırsa, IP adresini kullanılabilir havuza geri iade etmek ve INIT durumda yeni bir IP adresi isteğinde olmak için Sunucuya bir YAYıN iletisi göndermesi gerekir.

Ayrıntılar için Bkz. Küçük Örnek Sistem **bölümünün Şekil** 1.1. DHCP Sunucusu örneğine kaydedilen IP adresi sayısı, DHCP Sunucusu denetim bloğunda sunucu adresi dizisinin boyutuyla sınırlıdır ve dhcp sunucusu için yapılandırılabilir NX_DHCP_IP_ADDRESS_MAX_LIST_SIZE.

### <a name="ip-address-lease-times"></a>IP Adresi Kiralama Süreleri

Dhcp Sunucusu, bu kiralama süresi, yapılandırılabilir seçenekte tanımlanan Sunucu varsayılan kira süresi'nin altında ise, istek İstemci kira süresini NX_DHCP_DEFAULT_LEASE_TIME. İstemciye atanan yenileme ve yeniden bağlantı süreleri sırasıyla kiralama süresinin %50'si ve %85'idir. Kiralama süresi sonsuz (0xFFFFFFFF) olmadığı sürece, yenileme ve yeniden bağlantı süreleri de sonsuz olarak ayarlanır.

### <a name="dhcp-server-timeouts"></a>DHCP Sunucusu Zaman Aşımı

DHCP Sunucusu, oturum tamamlanmadıkça NX_DHCP_CLIENT_SESSION_TIMEOUT dhcp istemcisinin iletiyi beklemesi için kullanıcı tarafından yapılandırılabilir bir oturum zaman aşımına sahip. Sunucu, daha önce gönderilen iletinin aynı olup olup bakılmaksızın İstemciden bir sonraki iletiyi aldığında zaman out sıfırlanır.

### <a name="internal-error-handling"></a>İç hata işleme

DHCP Sunucusu, dhcp istemci paketlerini nx_dhcp_listen_for_messages alır *ve* işler. Paket geçersizse veya DHCP Sunucusu bir iç hatayla karşılaşırsa bu işlev geçerli DHCP İstemci paketini işlemeyi sonlandıracak. n *x_dhcp_listen_for_messages* hata durumu döndürür. DHCP Sunucusu iş parçacığı, sonraki DHCP İstemcisi iletiyi almak için bu işlevi çağırmadan önce ThreadX zamanlayıcısını kısaca kontrol altına alır. Geçerli sürümde, hata durumu geri dönüşleri için günlük desteği *nx_dhcp_listen_for_messages.*

### <a name="option-55-parameter-request-list"></a>Seçenek 55: Parametre İstek Listesi

NetX Duo DHCP Sunucusu, TEKLIF ve İstemciye geri ilettiği DHCPACK iletileri'nin Parametre İsteği Seçeneği (55) listesine yüklemek için bir dizi seçenekle yapılandırıldı. Bu seçenekler İstemci ağı için ağ kritik yapılandırma verilerini içermeli ve varsayılan olarak yönlendirici IP adresi, alt ağ maskesi ve DNS sunucusu olarak tanımlanır. Seçenek listesi, boşlukla ayrılmış bir listedir ve kullanıcı tarafından yapılandırılabilir NX_DHCP_DEFAULT_SERVER_OPTION_LIST. Bu listede belirtilen seçeneklerin sayısının kullanıcı tanımlı olan NX_DHCP_DEFAULT_OPTION_LIST_SIZE aynı olması gerektiğini unutmayın.

## <a name="constraints-of-the-netx-duo-dhcp-server"></a>NetX Duo DHCP Sunucusunun Kısıtlamaları

### <a name="dhcp-messages"></a>DHCP İletileri

NetX Duo DHCP Sunucusu, İstemciye IP adresi verilmeden önce bir IP adresinin ağ üzerinde başka bir yere atanmamış olduğunu doğrulamaz. Birden çok DHCP sunucusu varsa, bu durum gerçekten de böyle olabilir. *RFC 2131'e* göre IP adresinin kendi ağın benzersiz olduğunu (örn. adrese ping atarak) doğrulamak İstemcinin sorumluluğundadır. Böyle bir ip adresi yoksa Sunucu, veritabanını İstemciden güncelleştirmek için IP adresine sahip bir REDDETME iletisi aldır.

NetX Duo DHCP Sunucusu herhangi bir FORCE_RENEW göndermez. IP adresi kiralamasını yenilemek DHCP İstemcisi'ne göredir. Ancak, DHCP Sunucusu veritabanındaki atanan tüm IP adreslerinde kalan zamanı izler. Bir IP adresi kiralama süresi dolduğunda, bu IP adresi kullanılabilir IP adresleri havuzuna döndürülür. Bu nedenle, IP adresi kiralamasını etkin bir şekilde yenilemek/yeniden bağlantı yapmak İstemci'ye bağlı olur.

İstemciye IP kiralama izni verilir ("bağlı") verilir (veya var olan bir ip kirası yenilendi) hemen oturum verileri temizlenecektir. İstemci paketi sahte olduğunu kanıtlarsa veya İstemci yanıtlarda zaman atlıyorsa, oturum verileri temizlendi.

### <a name="saving-data-between-reboots"></a>Yeniden Başlatmalar Arasında Veri Kaydetme

NetX Duo DHCP Sunucusu, DHCP istek parametreleri de dahil olmak üzere İstemci verilerini bir İstemci kayıt tablosuna kaydeder. Bu tablo geçici olmayan bellekte depolanmaz, bu nedenle DHCP Sunucusu ana bilgisayarının yeniden başlatılması gerekirse bu bilgiler yeniden başlatmalar arasında kaydedilmeyen bilgilerdir.

NetX Duo DHCP Sunucusu, IP adresi kira verilerini bir IP adresi tablosuna kaydeder. Bu tablo geçici olmayan bellekte depolanmaz, bu nedenle DHCP Sunucusu ana bilgisayarının yeniden başlatılması gerekirse bu bilgiler yeniden başlatmalar arasında kaydedilmeyen bilgilerdir.

### <a name="relay-agents"></a>Geçiş Aracıları

NetX Duo DHCP Sunucusu, ağ dışında DHCP isteklerini desteklemez, çünkü 'Geçiş aracısı' alanı için sıfır BIR IP adresi ile yapılandırılır.

## <a name="small-example-system"></a>Küçük Örnek Sistem

Aşağıda görünen Şekil 1.1'de NetX Duo DHCP Sunucusunu kullanmanın ne kadar kolay olduğuna bir örnek verilmiştir. Bu örnekte, DHCP dahil *nxd_dhcp_server.h* dosyası 5. satıra getiri. DHCP Sunucusu iş parçacığı yığını boyutu, IP iş parçacığı yığını boyutu ve test iş parçacığı yığını boyutu 7-13. satırlarda tanımlanır.

İlk olarak, DHCP sunucusunu durdurmak, yeniden başlatmak ve sonunda silmek için isteğe bağlı bir test iş parçacığı görevi, 57. satırda "*test_thread_entry*" işleviyle oluşturulur. DHCP Sunucusu denetim bloğu "*dhcp_server*" 20. satırda genel değişken olarak tanımlanır. Sunucu paket havuzunun, standart DHCP iletisi (548 bayt artı IP ve UDP üst bilgi baytları) kadar büyük bir yüke sahip paketlerle oluşturulmuş olduğunu unutmayın. DHCP Sunucusu için bir IP örneği başarıyla oluşturulduktan sonra, uygulama 96. satırda DHCP Sunucusunu oluşturur. Ardından, uygulama Sunucu IP örneğinin UDP etkinleştirilmiş olarak etkinleştirilmesini sağlar. DHCP Sunucusunu başlatmadan önce, kullanılabilir IP adresi listesi 137. satırda nx_dhcp_create_server_ip_address_list **oluşturulur.** Ağ yapılandırma parametreleri, **nx_dhcp_set_interface_network_parameters** hizmeti kullanılarak aşağıdaki 138. satırda ayarlanır; uygulama 141. satırda nx_dhcp_server_start çağıran DHCP Sunucusu hizmetleri kullanılabilir hale geldi.  Test iş parçacığı görevi, DHCP sunucusunu durdurma ve yeniden başlatma kullanımını gösterir.

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

**Şekil 1.1 Örnek NetX Duo DHCP Sunucusu uygulaması**

## <a name="configuration-options"></a>Yapılandırma Seçenekleri

NetX Duo DHCP Sunucusu'ları için çeşitli yapılandırma seçenekleri vardır. Aşağıdaki listede her biri ayrıntılı olarak açıklanmaktadır:

- **NX_DISABLE_ERROR_CHECKING:** Bu seçenek temel DHCP hata denetimlerini kaldırır. Genellikle uygulama hata ayıklandıktan sonra kullanılır.
- **NX_DHCP_SERVER_THREAD_PRIORITY:** Bu seçenek DHCP Sunucusu iş parçacığının önceliğini belirtir. Varsayılan olarak, bu değer DHCP iş parçacığının öncelik 2'de çalıştır olduğunu belirtir.
- **NX_DHCP_TYPE_OF_SERVICE:** Bu seçenek, DHCP UDP istekleri için gereken hizmet türünü belirtir. Varsayılan olarak, bu değer normal IP NX_IP_NORMAL belirtmek için varsayılan olarak tanımlanmıştır.
- **NX_DHCP_FRAGMENT_OPTION:** DHCP UDP istekleri için parça etkinleştirme. Varsayılan olarak, udp parçalanması devre dışı NX_DONT_FRAGMENT için bu değer bir değer olarak ayarlanır.
- **NX_DHCP_TIME_TO_LIVE:** Paketin atmadan önce geçeceği yönlendirici sayısını belirtir. Varsayılan değer, 0x80.
- **NX_DHCP_QUEUE_DEPTH:** DHCP Sunucusu yuvasının kuyruğu boşaltmadan önce tutar olduğu paket sayısını belirtir. Varsayılan değer 5'tir.
- **NX_DHCP_PACKET_ALLOCATE_TIMEOUT:** NetX DHCP Sunucusunun paket havuzundan bir paket ayırmayı beklemesi için zamanlayıcı değer çizgisi zaman aşımını belirtir. Varsayılan değer, NX_IP_PERIODIC_RATE.
- **NX_DHCP_SUBNET_MASK** Bu, DHCP İstemcisi'nin yapılandırılması gereken alt ağ maskesidir. Varsayılan değer, 0xFFFFFF00.
- **NX_DHCP_FAST_PERIODIC_TIME_INTERVAL:** Bu süre, DHCP Sunucusu hızlı zamanlayıcının kalan oturum sürelerini denetlemesi ve zaman aşımına neden olan oturumları işlemesi için zaman aşımı süresidir.
- **NX_DHCP_SLOW_PERIODIC_TIME_INTERVAL:** DHCP Sunucusu yavaş zamanlayıcının kalan IP adresi kira süresini denetlemesi ve zaman aşımına neden olan kiralamayı işlemesi için zamanlayıcıda zaman aşımı süresidir.
- **NX_DHCP_CLIENT_SESSION_TIMEOUT:** Süreölçerde bu zaman aşımı süresi, DHCP Sunucusunun bir sonraki DHCP İstemcisi iletiyi almak için bekleyeceğini işaretler.
- **NX_DHCP_DEFAULT_LEASE_TIME:** Bu, DHCP İstemcisine atanan saniyeler içinde IP Adresi kira süresidir ve yenileme ve yeniden bağlantı sürelerinin hesaplanması için de temel olarak İstemciye atanır. Varsayılan değer, 0xFFFFFFFF (sonsuz) olarak ayarlanır.
- **NX_DHCP_IP_ADDRESS_MAX_LIST_SIZE:** İstemciye atanma için kullanılabilir IP adreslerini tutmak için DHCP Sunucusu dizisinin boyutudur. Varsayılan değer 20'dir.
- **NX_DHCP_CLIENT_RECORD_TABLE_SIZE:** İstemci kayıtlarını tutmak için DHCP Sunucusu dizisinin boyutudur. Varsayılan değer 50'dir.
- **NX_DHCP_CLIENT_OPTIONS_MAX:** Geçerli oturumda parametre isteği listesinde istenen tüm seçenekleri tutmak için DHCP İstemcisi örneğinde dizisinin boyutudur. Varsayılan değer 12'dir.
- **NX_DHCP_OPTIONAL_SERVER_OPTION_LIST:** Parametre isteği listesinde geçerli DHCP İstemcisi'ne sağlamak için DHCP Sunucusunun varsayılan seçenek listesini tutan arabellektir. Varsayılan değer "1 3 6"dır.
- **NX_DHCP_OPTIONAL_SERVER_OPTION_SIZE:** Bu, DHCP Sunucusunun varsayılan seçenek listesini tutmak için dizinin boyutudur. Varsayılan değer 3'tir.
- **NX_DHCP_SERVER_HOSTNAME_MAX:** Bu, Sunucu ana bilgisayar adını tutmak için arabellek boyutudur. Varsayılan değer 32'dir.
- **NX_DHCP_CLIENT_HOSTNAME_MAX:** Bu, geçerli DHCP Sunucusu İstemci oturumunda İstemci ana bilgisayar adını tutmak için arabellek boyutudur. Varsayılan değer 32'dir.
