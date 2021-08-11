---
title: Bölüm 2 - NetX POP3 İstemcisi'Azure RTOS yükleme ve kullanma
description: NetX POP3 İstemcisi bir kaynak dosya, bir üst bilgi dosyası ve bir tanıtım dosyası içerir. MD5 özet hizmetleri için iki ek dosya vardır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: e8fc4f1194e423efdd179c3b7f33c3935bf683fcdd0321d83a7510dc6bdffb81
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116783399"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-pop3-client"></a>Bölüm 2 - NetX POP3 İstemcisi'Azure RTOS yükleme ve kullanma

NetX POP3 İstemcisi bir kaynak dosya, bir üst bilgi dosyası ve bir tanıtım dosyası içerir. MD5 özet hizmetleri için iki ek dosya vardır. Ayrıca bir Kullanıcı Kılavuzu PDF dosyası da (bu belge) vardır.

- **nx_pop3_client.c:** NetX POP3 İstemci API'si için C Kaynak dosyası
- **nx_pop3_client.h:** NetX POP3 İstemci API'si için C Üst Bilgi dosyası
- **demo_netxduo_pop3_client.c:** POP3 İstemcisi oluşturma ve oturum başlatımı için tanıtım dosyası
- **nx_md5.c:** MD5 özet hizmetlerini tanımlayan C Kaynak dosyası
- **nx_md5.h:** MD5 özet hizmetlerini tanımlayan C Üst Bilgi dosyası
- **nx_pop3_client.pdf:** NetX POP3 İstemci Kullanıcı Kılavuzu

NetX POP3 İstemcisini kullanmak için, daha önce bahsedilen dağıtımın tamamı NetX'in yüklü olduğu dizine kopyalanır. Örneğin, NetX "*\threadx\mcf5272\green"* dizininde *yüklüyse, nx_md5.h*, *nx_md5.c,* *nx_pop3_client.h ve nx_pop3_client.c* dosyalarının bu dizine kopyalanmış olması gerekir.

## <a name="using-netx-pop3-client"></a>NetX POP3 İstemcisini Kullanma

NetX POP3 İstemci hizmetini kullanmak için uygulamanın derleme projesine *nx_pop3_client.c* eklemesi gerekir. ThreadX ve NetX kullanmak için uygulama kodu *nx_md5.h, nx_pop3.h ve nx_pop3_client.h'den* *sonra tx_api.h* ve *nx_api.h'yi* içermeli.

Bu dosyaların diğer uygulama dosyalarıyla aynı şekilde derlenmiş olması ve nesne kodunun uygulamanın dosyalarıyla birlikte bağlantılı olması gerekir. NetX POP3 İstemcisi'nin kullanımı için gerekenler bunlardır.

## <a name="small-example-of-the-netx-pop3-client"></a>NetX POP3 İstemcisi Küçük Örneği

Aşağıda görünen Şekil 1'de NetX POP3 İstemci hizmetlerini kullanma örneği açıklanmıştır. Bu tanıtım, 37. ve 38. satırlarda posta indirme ve oturum tamamlama bildirimi için iki geri çağırmayı ayarlar. POP3 İstemci paket havuzu 76. satırda oluşturulur. IP iş parçacığı görevi 88. satırda oluşturulur. Bu paket havuzunun POP3 İstemci paket havuzu için de kullan olduğunu unutmayın. TCP, 107. satırda IP görevi üzerinde etkinleştirilir.

POP3 İstemcisi, uygulama iş parçacığı giriş işlevinin içinde 133. satırda oluşturulur ve *demo_thread_entry.* Bunun nedeni, *nx_pop3_client_create* hizmetinin POP3 sunucusuyla TCP bağlantısı yapmaya da çalışmasıdır. Başarılı olursa, uygulama, nx_pop3_client_mail_items_get hizmetini kullanarak pop3 sunucusunu 149. satırdaki postadaki *öğe sayısı için sorgular.*

Bir veya daha fazla öğe varsa, uygulama posta iletisini indirmek için her bir posta öğesi için while döngüsünde tekrarlar. RETR isteği, 149. satırda nx_pop3_client_mail_item_get *yapılır.* Başarılı olursa, uygulama 177. *satırda nx_pop3_client_mail_item_message_get* hizmetini kullanarak paketleri indirir ve iletide son paketin 196. satırda alınmıştır. Son olarak uygulama, 199. satırda bir indirmenin başarılı olduğunu varsayarak posta *öğesini* nx_pop3_client_mail_item_delete siler. RFC 1939, POP3 İstemcilerinin, İstemcinin posta dinlemesinde postanın birikerek önlenmesi için Sunucuya indirilen posta öğelerini silmesini talimatı göndermesini önermektedir. Sunucu bunu otomatik olarak da yapar.

Tüm posta öğeleri indirildikten sonra veya bir POP3 İstemcisi hizmet çağrısı başarısız olursa uygulama döngüden çıkar ve nx_pop3_client_delete hizmetini kullanarak 217. satırdaki *POP3 İstemcisini* siler.

```c
/*
    demo_netxduo_pop3.c

    This is a small demo of POP3 Client on the NetX TCP/IP stack.
    This demo relies on Thread, NetX and POP3 Client API to conduct
    a POP3 mail session.
*/

#include "tx_api.h"
#include "nx_api.h"
#include "nx_pop3_client.h"

#define DEMO_STACK_SIZE        4096
#define CLIENT_ADDRESS         IP_ADDRESS(192,2,2,61)
#define SERVER_ADDRESS         IP_ADDRESS(192,2,2,89)
#define SERVER_PORT            110

/* Replace the 'ram' driver with your own Ethernet driver. */
void _nx_ram_network_driver(struct NX_IP_DRIVER_STRUCT *driver_req);

/* Set up the POP3 Client. */

TX_THREAD          demo_client_thread;
NX_POP3_CLIENT     demo_client;
NX_PACKET_POOL     client_packet_pool;
NX_IP              client_ip;

#define PAYLOAD_SIZE 500

/* Set up Client thread entry point. */
void     demo_thread_entry(ULONG info);

/* Shared secret is the same as password. */

#define LOCALHOST              "recipient@domain.com"
#define LOCALHOST_PASSWORD     "testpwd"

/* Define main entry point. */
int main()
{
    /* Enter the ThreadX kernel. */
    tx_kernel_enter();
}

/* Define what the initial system looks like. */
void tx_application_define(void *first_unused_memory)
{

UINT      status;
UCHAR     *free_memory_pointer;

    /* Setup the working pointer. */
    free_memory_pointer = first_unused_memory;

    /* Create a client thread. */
    tx_thread_create(&demo_client_thread, "Client", demo_thread_entry, 0,
                    free_memory_pointer, DEMO_STACK_SIZE, 1, 1,
                    TX_NO_TIME_SLICE, TX_AUTO_START);

    free_memory_pointer = free_memory_pointer + DEMO_STACK_SIZE;

    /* Initialize the NetX system. */
    nx_system_initialize();

    /* The demo client username and password is the authentication
    data used when the server attempts to authentication the client. */

    /* Create Client packet pool. */
    status = nx_packet_pool_create(&client_packet_pool,"POP3 Client Packet Pool",
                        PAYLOAD_SIZE, free_memory_pointer, (PAYLOAD_SIZE * 10));
    if (status != NX_SUCCESS)
    {
        return;
    }

    /* Update pointer to unallocated (free) memory. */
    free_memory_pointer = free_memory_pointer + (PAYLOAD_SIZE * 10);

    /* Create IP instance for demo Client */
    status = nx_ip_create(&client_ip, "POP3 Client IP Instance",
                            CLIENT_ADDRESS, 0xFFFFFF00UL, &client_packet_pool,
                            _nx_ram_network_driver, free_memory_pointer,
                            2048, 1);

    if (status != NX_SUCCESS)
    {
        return;
    }

    /* Update pointer to unallocated (free) memory. */
    free_memory_pointer = free_memory_pointer + 2048;

    /* Enable ARP and supply ARP cache memory. */
    nx_arp_enable(&client_ip, (void **) free_memory_pointer, 1024);

    /* Update pointer to unallocated (free) memory. */
    free_memory_pointer = free_memory_pointer + 1024;

    /* Enable TCP and ICMP for Client IP. */
    nx_tcp_enable(&client_ip);
    nx_icmp_enable(&client_ip);

    return;
}

/* Define the application thread entry function. */

void demo_thread_entry(ULONG info)
{

UINT          status;
UINT          mail_item, number_mail_items;
UINT          bytes_downloaded = 0;
UINT          final_packet = NX_FALSE;
ULONG         total_size, mail_item_size, bytes_retrieved;
NX_PACKET     *packet_ptr;

    /* Let the IP instance get initialized with driver parameters. */
    tx_thread_sleep(40);

    /* Create a NetX POP3 Client instance with no byte or block memory pools.
    Note that it uses its password for its APOP shared secret. */
    status = nx_pop3_client_create(&demo_client,
                        NX_TRUE,
                        &client_ip, &client_packet_pool, SERVER_ADDRESS,
                        SERVER_PORT, LOCALHOST, LOCALHOST_PASSWORD);

    /* Check for error. */
    if (status != NX_SUCCESS)
    {
        status = nx_pop3_client_delete(&demo_client);

        /* Abort. */
        return;
    }

    /* Find out how many items are in our mailbox. */
    status = nx_pop3_client_mail_items_get(&demo_client, &number_mail_items, &total_size);

    printf("Got %d mail items, total size%d \n", number_mail_items, total_size);

    /* If nothing in the mailbox, disconnect. */
    if (number_mail_items == 0)
    {
        nx_pop3_client_delete(&demo_client);

        return;
    }

    /* Download all mail items. */
    mail_item = 1;

    while (mail_item <= number_mail_items)
    {

        /* This submits a RETR request and gets the mail message size. */
        status = nx_pop3_client_mail_item_get(&demo_client, mail_item, &mail_item_size);

        /* Loop to get all mail message packets until the mail item is completely downloaded. */

        while((final_packet == NX_FALSE) && (status == NX_SUCCESS))
        {
            status = nx_pop3_client_mail_item_message_get(&demo_client, &packet_ptr,
                                                        &bytes_retrieved,
                                                        &final_packet);

            if (status != NX_SUCCESS)
            {
                break;
            }

            if (bytes_retrieved != 0)
            {

            printf("Received %d bytes of data for item %d: %s\n",
                    packet_ptr -> nx_packet_length,
                    mail_item, packet_ptr -> nx_packet_prepend_ptr);
            }

            nx_packet_release(packet_ptr);

            /* Determine if this is the last data packet. */
            if (final_packet)
            {
                /* It is. Let the server know it can delete this mail item. */
                status = nx_pop3_client_mail_item_delete(&demo_client, mail_item);
            }

            /* Keep track of how much mail message data is left. */
            bytes_downloaded += bytes_retrieved;
        }

        /* Get the next mail item. */
        mail_item++;

        tx_thread_sleep(100);
    }

    /* Disconnect from the POP3 server. */
    status = nx_pop3_client_quit(&demo_client);

    /* Delete the POP3 Client. This will not delete the Client packet pool. */
    status = nx_pop3_client_delete(&demo_client);

}
```

Şekil 1. NetX POP3 İstemci uygulaması örneği

## <a name="pop3-client-configuration-options"></a>POP3 İstemci Yapılandırma Seçenekleri

NetX POP3 İstemcisi'nin çeşitli yapılandırma seçenekleri vardır. Aşağıda ayrıntılı olarak açıklanan tüm seçeneklerin listesi velanmıştır:

- **NX_POP3_CLIENT_PACKET_TIMEOUT:** Bu, POP3 İstemcisi'nin paket ayırması için saniyeler içinde bekleme seçeneğini tanımlar. Varsayılan değer 1 saniyedir.

- **NX_POP3_CLIENT_CONNECTION_TIMEOUT:** Bu, POP3 İstemcisi'nin POP3 Sunucusuna bağlanması için saniyeler içinde bekleme seçeneğini tanımlar. Varsayılan değer 30 saniyedir.

- **NX_POP3_CLIENT_DISCONNECT_TIMEOUT:** Bu, POP3 İstemcisi'nin POP3 Sunucusu bağlantısının kesilmesi için saniyeler içinde bekleme seçeneğini tanımlar. Varsayılan değer 2 saniyedir.

- **NX_POP3_TCP_SOCKET_SEND_WAIT:** Bu seçenek, hizmet çağrılarında bekleme *nx_tcp_socket_send* ayarlar. Varsayılan değer 2 saniyedir.

- **NX_POP3_SERVER_REPLY_TIMEOUT:** Bu seçenek, bir İstemci *isteğine nx_tcp_socket_receive* sunucu yanıtı için hizmet çağrılarında bekleme seçeneğini ayarlar. Varsayılan değer 10 saniyedir.

- **NX_POP3_CLIENT_TCP_WINDOW_SIZE:** Bu seçenek İstemci TCP alma penceresinin boyutunu ayarlar. Bu, IP örneği MTU boyutu eksi IP ve TCP üst bilgisi olarak ayarlanır. Varsayılan değer 1460'tır.

- **NX_POP3_MAX_USERNAME:** Bu seçenek POP3 İstemci kullanıcı adının arabelleğinin boyutunu ayarlar. Varsayılan değer 40 bayttır.

- **NX_POP3_MAX_PASSWORD:** Bu seçenek POP3 İstemci parolasının arabelleğinin boyutunu ayarlar. Varsayılan değer 20 bayttır.