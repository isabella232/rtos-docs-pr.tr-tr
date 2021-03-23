---
title: Bölüm 2-Azure RTOS NetX Duo Oto IP 'yi yükleme ve kullanma
description: Bu bölümde, Azure RTOS NetX Duo Oto IP bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların bir açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 42c58a4cdec34a03eda9f42315438e5fbe2ea594
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826170"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-duo-autoip"></a>Bölüm 2-Azure RTOS NetX Duo Oto IP 'yi yükleme ve kullanma

Bu bölümde, Azure RTOS NetX Duo Oto IP bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların bir açıklaması yer almaktadır.

## <a name="product-distribution"></a>Ürün dağıtımı

Azure RTOS NetX Oto, konumundaki genel kaynak kodu depomızdan elde edilebilir [https://github.com/azure-rtos/netx/](https://github.com/azure-rtos/netx/) . Bu paket üç kaynak dosyası, bir içerme dosyası ve bu belgeyi içeren bir PDF dosyası içerir ve aşağıdaki gibi:

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
> Aşağıdaki örnekte konak cihazının tek bilgisayarlı bir cihaz olduğu varsayılır. Birden çok sayfalı bir cihaz için, konak uygulama NetX Oto IP hizmetini kullanarak bir IP adresini yoklamanın ikincil ağ arabirimini belirtmek üzere *nx_auto_ip_interface_*. Birden çok ağ bağlantılı uygulamalar ayarlama hakkında daha fazla bilgi için [NETX Kullanıcı kılavuzuna](https://docs.microsoft.com/azure/rtos/netx/about-this-guide) bakın. Ana bilgisayar uygulamasının, IP adresi elde ettiğini doğrulamak için NetX API *nx_status_ip_interface_check* kullanması gerektiğini unutmayın.

```c
#include "tx_api.h"
#include "nx_api.h"
#include "nx_auto_ip.h"

#define     DEMO_STACK_SIZE     4096

/* Define the ThreadX and NetX object control blocks... */

TX_THREAD              thread_0;
NX_PACKET_POOL         pool_0;
NX_IP                  ip_0;

/* Define the AUTO IP structures for the IP instance. */

NX_AUTO_IP             auto_ip_0;

/* Define the counters used in the demo application... */

ULONG                 thread_0_counter;
ULONG                 address_changes;
ULONG                 error_counter;

/* Define thread prototypes. */
void     thread_0_entry(ULONG thread_input);
void     ip_address_changed(NX_IP *ip_ptr, VOID *auto_ip_address);
void     _nx_ram_network_driver(struct NX_IP_DRIVER_STRUCT *driver_req);

/* Define main entry point. */

int main()
{

    /* Enter the ThreadX kernel. */
    tx_kernel_enter();
}

/* Define what the initial system looks like. */

void     tx_application_define(void *first_unused_memory)
{

CHAR     *pointer;
UINT     status;

    /* Setup the working pointer. */
    pointer = (CHAR *) first_unused_memory;

    /* Create the main thread. */
    tx_thread_create(&thread_0, "thread 0", thread_0_entry, 0,
                    pointer, DEMO_STACK_SIZE,
                    16, 16, 1, TX_AUTO_START);

    pointer = pointer + DEMO_STACK_SIZE;

    /* Initialize the NetX system. */
    nx_system_initialize();

    /* Create a packet pool. */
    status = nx_packet_pool_create(&pool_0, "NetX Main Packet Pool", 128,
                                    pointer, 4096);
    pointer = pointer + 4096;

    if (status)
        error_counter++;

    /* Create an IP instance. */
    status = nx_ip_create(&ip_0, "NetX IP Instance 0", IP_ADDRESS(0, 0, 0, 0),
                        0xFFFFFF00UL, &pool_0, _nx_ram_network_driver,
                        pointer, 4096, 1);
    pointer = pointer + 4096;

    if (status)
        error_counter++;

    /* Enable ARP and supply ARP cache memory for IP Instance 0. */
    status = nx_arp_enable(&ip_0, (void *) pointer, 1024);
    pointer = pointer + 1024;

    /* Check ARP enable status. */
    if (status)
        error_counter++;

    /* Create the AutoIP instance for IP Instance 0. */
    status = nx_auto_ip_create(&auto_ip_0, "AutoIP 0", &ip_0, pointer, 4096, 1);
    pointer = pointer + 4096;

    /* Check AutoIP create status. */
    if (status)
        error_counter++;

    /* Start AutoIP instances. */
    status = **nx_auto_ip_start**(&auto_ip_0, 0 /*IP_ADDRESS(169,254,254,255)*/);

    /* Check AutoIP start status. */
    if (status)
        error_counter++;

    /* Register an IP address change function for IP Instance 0. */
    status = nx_ip_address_change_notify(&ip_0, ip_address_changed,
                                        (void *) &auto_ip_0);

    /* Check IP address change notify status. */
    if (status)
        error_counter++;
}

/* Define the test thread. */

void     thread_0_entry(ULONG thread_input)
{

UINT     status;
ULONG    actual_status;

    /* Wait for IP address to be resolved. */
    do
    {

        /* Call IP status check routine. */
        status = nx_ip_status_check(&ip_0, NX_IP_ADDRESS_RESOLVED,
            &actual_status, 10000);

    } while (status != NX_SUCCESS);

    /* Since the IP address is resolved at this point, the application can now fully utilize NetX! */

    while(1)
    {

        /* Increment thread 0's counter. */
        thread_0_counter++;

        /* Sleep... */
        tx_thread_sleep(10);
    }
}

void          ip_address_changed(NX_IP *ip_ptr, VOID *auto_ip_address)
{

ULONG         ip_address;
ULONG         network_mask;
NX_AUTO_IP    *auto_ip_ptr;

    /* Setup pointer to auto IP instance. */
    auto_ip_ptr = (NX_AUTO_IP *) auto_ip_address;

    /* Pickup the current IP address. */
    nx_ip_address_get(ip_ptr, &ip_address, &network_mask);

    /* Determine if the IP address has changed back to zero. If so, make sure the AutoIP instance is started. */
    if (ip_address == 0)
    {

        /* Get the last AutoIP address for this node. */
        nx_auto_ip_get_address(auto_ip_ptr, &ip_address);

        /* Start this AutoIP instance. */
        nx_auto_ip_start(auto_ip_ptr, ip_address);
        }

    /* Determine if IP address has transitioned to a non local IP address. */
    else if ((ip_address & 0xFFFF0000UL) != IP_ADDRESS(169, 254, 0, 0))
    {

        /* Stop the AutoIP processing. */
        nx_auto_ip_stop(auto_ip_ptr);
    }

    /* Increment a counter. */
    address_changes++;
}
```

Şekil 1,1 NetX ile Oto IP kullanımı örneği

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
