---
title: Bölüm 2-NetX Duo SMTP istemcisinin yüklenmesi ve kullanımı
description: Bu bölümde, NetX Duo SMTP Istemci bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 07/09/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 86f324935ba32aab010b81f825be0a6564983a2e
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825786"
---
# <a name="chapter-2---installation-and-use-of-netx-duo-smtp-client"></a>Bölüm 2-NetX Duo SMTP istemcisinin yüklenmesi ve kullanımı

Bu bölümde, NetX Duo SMTP Istemci bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların açıklaması yer almaktadır.

## <a name="netx-duo-smtp-client-installation"></a>NetX Duo SMTP Istemcisi yüklemesi

NetX Duo SMTP Istemcisi adresinde bulunabilir [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo) . Paket aşağıdaki dosyaları içerir:

- **nxd_smtp_client. c** NetX Duo SMTP Istemcisi API 'SI için C kaynak dosyası
- **nxd_smtp_client. h** NetX Duo SMTP Istemcisi API 'SI için C üstbilgi dosyası
- **demo_netxduo_smtp_client. c** NetX Duo SMTP Istemcisi tanıtımı
- **İçinnxd_smtp_client.pdf Kullanıcı Kılavuzu** NetX Duo SMTP Istemcisi API 'SI

NetX Duo SMTP Istemcisi API 'sini kullanmak için, daha önce bahsedilen tüm dağıtım, NetX Duo yüklendiği dizine kopyalanabilir. Örneğin, "c:*\MyProject*" dizininde NETX Duo yüklüyse, *nxd_smtp_client. h ve nxd_smtp_client. c* dosyaları bu dizine kopyalanmalıdır.

## <a name="using-netx-duo-smtp-client"></a>NetX Duo SMTP Istemcisini kullanma

NetX Duo SMTP Istemci uygulamasını oluşturmak için öncelikle ThreadX ve NetX Duo kitaplıklarını oluşturmalı ve bunları Build projesine dahil etmelidir. Uygulamanın, uygulama kaynak kodunda TX *_api. h* ve *nx_api. h*'yi içermesi gerekir. Bu, ThreadX ve NetX Duo hizmetlerini etkinleştirir. Ayrıca, *SMTP istemci hizmetlerini kullanmak için* *tx_api. h* ve nx_api. h sonrasında *nxd_smtp_client. c* ve *nxd_smtp_client. h* içermelidir.

Bu dosyalar, diğer uygulama dosyalarıyla aynı şekilde derlenmesi gerekir ve nesne kodu, uygulamanın dosyalarıyla birlikte bağlanmalıdır. Bu, bir NetX Duo SMTP Istemci uygulaması oluşturmak için gereklidir.

## <a name="small-example-system"></a>Küçük örnek sistem

NetX Duo SMTP Istemcisini kullanmanın bir örneği aşağıda gösterilen Şekil 1 ' de açıklanmıştır. IP örneği için paket havuzu, 68 satırındaki nx_packet_pool_create hizmeti kullanılarak oluşturulur ve çok küçük bir paket yüküne sahiptir. Bunun nedeni, IP örneğinin yalnızca fazla yük gerektirmeyen denetim paketlerini göndermesi içindir. 84. satırda oluşturulan SMTP Istemcisi paket havuzu ve SMTP Istemci iletilerini sunucuya ve ileti verilerine iletmek için kullanılır. Paket yükü çok daha büyük. IP örneği, aynı paket havuzunu kullanan 118. satırda oluşturulur. SMTP protokolü için gereken TCP, 130. satırdaki IP örneğinde etkinleştirilmiştir.

Uygulama iş parçacığında, SMTP Istemcisi *nxd_smtp_client_create* hizmeti kullanılarak oluşturulur, satır 170. *Nxd_smtp_client_create* hizmeti IPv4 ve IPv6 SMTP sunucusu bağlantılarını destekler, ancak bu örnek IPv4 ile sınırlıdır. Ardından posta iletisi, *nx_smtp_mail_send* hizmeti kullanılarak 184. satırda ıletım Için SMTP istemcisine gönderilir. Posta içeriği üst bilgisine sahip konu satırının ileti gövdesinden ayrı olarak oluşturulduğunu unutmayın. Ayrıca, e-posta isteği yalnızca, sözdizimsel olarak doğru olarak kabul edilen tek bir alıcı posta adresini kabul ettiğini unutmayın.

Ardından, uygulama SMTP Istemcisini 200. satırda sonlandırır. *Nx_smtp_client_delete* hizmeti yuva bağlantısının kapalı olduğunu ve bağlantı noktasının ilişkisiz olduğunu denetler. Bu, daha önce kullanımda değilse, paket havuzunu silmek için SMTP Istemci uygulamasına kadar olduğunu unutmayın.

```c
/*
   demo_netxduo_smtp_client.c

   This is a small demo of the NetX Duo SMTP Client on the high-performance NetX
   Duo TCP/IP stack.  This demo relies on Thread, NetX Duo and SMTP Client API to
   perform simple SMTP mail transfers in an SMTP client application to an SMTP mail
   server.   */

#include "nx_api.h"
#include "nx_ip.h"
#include "nxd_smtp_client.h"


/* Define the host user name and mail box parameters */
#define USERNAME               "myusername"
#define PASSWORD               "mypassword"
#define FROM_ADDRESS           "my@mycompany.com"
#define RECIPIENT_ADDRESS      "your@yourcompany.com"
#define LOCAL_DOMAIN           "mycompany.com"

#define SUBJECT_LINE           "NetX Duo SMTP Client Demo"
#define MAIL_BODY              "NetX Duo SMTP client is an SMTP client \r\n" \
                               “implementation for embedded devices to send  \r\n" \
                               "email to SMTP servers. This feature is \r\n" \
                               "intended to allow a device to send simple \r\n " \
                               "status reports using the most universal \r\n " \
                               “Internet application, email.\r\n"

/* See the NetX Duo SMTP Client User Guide for how to set the authentication type.
   The most common authentication type is PLAIN. */
#define CLIENT_AUTHENTICATION_TYPE 3


#define CLIENT_IP_ADDRESS  IP_ADDRESS(1,2,3,5)
#define SERVER_IP_ADDRESS  IP_ADDRESS(1,2,3,4)
#define SERVER_PORT        25


/* Define the NetX Duo and ThreadX structures for the SMTP client appliciation. */
NX_PACKET_POOL                  ip_packet_pool;
NX_PACKET_POOL                  client_packet_pool;
NX_IP                           client_ip;
TX_THREAD                       demo_client_thread;
static NX_SMTP_CLIENT           demo_client;


void    _nx_ram_network_driver(struct NX_IP_DRIVER_STRUCT *driver_req);
void    demo_client_thread_entry(ULONG info);

/* Define main entry point.  */
int main()
{
    /* Enter the ThreadX kernel.  */
    tx_kernel_enter();
}

/* Define what the initial system looks like.  */
void    tx_application_define(void *first_unused_memory)
{

    UINT    status;
    CHAR    *free_memory_pointer;


    /* Setup the pointer to unallocated memory.  */
    free_memory_pointer =  (CHAR *) first_unused_memory;

    /* Create IP default packet pool. */
    status =  nx_packet_pool_create(&ip_packet_pool, "Default IP Packet Pool",
                                    128, free_memory_pointer, 2048);

    /* Update pointer to unallocated (free) memory. */
    free_memory_pointer = free_memory_pointer + 2048;

    /* Create SMTP Client packet pool. This is only for transmitting packets to the
       server. It need not be a separate packet pool than the IP default packet pool
       but for more efficient resource use, we use two different packet pools
       because the CLient SMTP messages generally require more payload than IP
       control packets.

       Packet payload depends on the SMTP Client application requirements.  Size of
       packet payload must include IP and TCP headers. For IPv6 connections, IP and
       TCP header data is 60 bytes. For IPv4 IP and TCP header data is 40 bytes (not
       including TCP options). */
    status |=  nx_packet_pool_create(&client_packet_pool, "SMTP Client Packet Pool",
                                     800, free_memory_pointer, (10*800));

    if (status != NX_SUCCESS)
    {
        return;
    }

    /* Update pointer to unallocated (free) memory. */
    free_memory_pointer = free_memory_pointer + (10*800);

    /* Initialize the NetX system. */
    nx_system_initialize();

    /* Create the client thread */
    status = tx_thread_create(&demo_client_thread, "client_thread",
                              demo_client_thread_entry, 0, free_memory_pointer,
                              2048, 16, 16,
                              TX_NO_TIME_SLICE, TX_DONT_START);

    if (status != NX_SUCCESS)
    {

        printf("Error creating Client thread. Status 0x%x\r\n", status);
        return;
    }

    /* Update pointer to unallocated (free) memory. */
    free_memory_pointer =  free_memory_pointer + 4096;


    /* Create Client IP instance. Remember to replace the generic driver
       with a real ethernet driver to actually run this demo! */

    status = nx_ip_create(&client_ip, "SMTP Client IP Instance", CLIENT_IP_ADDRESS,
                          0xFFFFFF00UL, &ip_packet_pool, _nx_ram_network_driver,
                          free_memory_pointer, 2048, 1);


    free_memory_pointer =  free_memory_pointer + 2048;

    /* Enable ARP and supply ARP cache memory. */
    status =  nx_arp_enable(&client_ip, (void **) free_memory_pointer, 1040);

    /* Update pointer to unallocated (free) memory. */
    free_memory_pointer = free_memory_pointer + 1040;

    /* Enable TCP for client. */
    status =  nx_tcp_enable(&client_ip);

    if (status != NX_SUCCESS)
    {
        return;
    }

    /* Enable ICMP for client. */
    status =  nx_icmp_enable(&client_ip);

    if (status != NX_SUCCESS)
    {
        return;
    }

    /* Start the client thread. */
    tx_thread_resume(&demo_client_thread);

    return;
}


/* Define the smtp application thread task.   */
void    demo_client_thread_entry(ULONG info)
{

    UINT        status;
    UINT        error_counter = 0;
    NXD_ADDRESS server_ip_address;


    tx_thread_sleep(100);

    /* Set up the server IP address. */
    server_ip_address.nxd_ip_version = NX_IP_VERSION_V4;
    server_ip_address.nxd_ip_address.v4 = SERVER_IP_ADDRESS;

    /* The demo client username and password is the authentication
       data used when the server attempts to authentication the client. */

    status =  nxd_smtp_client_create(&demo_client, &client_ip, &client_packet_pool,
                                     USERNAME,
                                     PASSWORD,
                                     FROM_ADDRESS,
                                     LOCAL_DOMAIN, CLIENT_AUTHENTICATION_TYPE,
                                     &server_ip_address, SERVER_PORT);

    if (status != NX_SUCCESS)
    {
        printf("Error creating the client. Status: 0x%x.\n\r", status);
        return;
    }

    /* Create a mail instance with the above text message and recipient info. */
    status =  nx_smtp_mail_send(&demo_client, RECIPIENT_ADDRESS,
                                TP_MAIL_PRIORITY_NORMAL,
                                SUBJECT_LINE, MAIL_BODY, sizeof(MAIL_BODY) - 1);

    /* Check for errors. */
    if (status != NX_SUCCESS)
    {

        /* Mail item was not sent. Note that we need not delete the client. The
           error status may be a failed authentication check or a broken connection.
           We can simply call nx_smtp_mail_send again.  */
        error_counter++;
    }

    /* Release resources used by client. Note that the transmit packet
       pool must be deleted by the application if it no longer has use for it.*/
    status = nx_smtp_client_delete(&demo_client);

    /* Check for errors. */
    if (status != NX_SUCCESS)
    {
        error_counter++;
    }

    return;
}
```

**Şekil 1. NetX Duo ile SMTP Istemcisi kullanımı örneği**

## <a name="client-configuration-options"></a>İstemci yapılandırma seçenekleri

NetX Duo SMTP Istemcisi API 'SI ile birkaç yapılandırma seçeneği vardır. Aşağıda, ayrıntılı olarak açıklanan tüm seçeneklerin bir listesi verilmiştir:

- **NX_SMTP_CLIENT_TCP_WINDOW_SIZE** Bu seçenek, Istemci TCP alma penceresinin boyutunu ayarlar. Bu, temel alınan Ethernet donanımının MTU boyutunun altına ayarlanmalıdır ve IP ve TCP üstbilgileri için odaya izin verir. Varsayılan NetX Duo SMTP Istemcisi TCP pencere boyutu 1460 ' dir.
- **NX_SMTP_CLIENT_PACKET_TIMEOUT** Bu seçenek, NetX paket ayırması sırasında zaman aşımını ayarlar. Varsayılan NetX Duo SMTP Istemcisi paket zaman aşımı 2 saniyedir.
- **NX_SMTP_CLIENT_CONNECTION_TIMEOUT** Bu seçenek Istemci TCP yuvası bağlantı zaman aşımını ayarlar. Varsayılan NetX Duo SMTP Istemcisi bağlantı zaman aşımı 10 saniyedir.
- **NX_SMTP_CLIENT_DISCONNECT_TIMEOUT** Bu seçenek, Istemci TCP yuvası bağlantı kesme zaman aşımını ayarlar. Varsayılan NetX Duo SMTP Istemcisi bağlantı kesme zaman aşımı 5 saniyedir *. SMTP Istemcisi bozuk bağlantı gibi bir iç hatayla karşılaşırsa, bağlantıyı sıfır bekleme zaman aşımıyla sonlandırabileceğini unutmayın.
- **NX_SMTP_GREETING_TIMEOUT** Bu seçenek, Istemcinin, karşılamasına yönelik sunucu yanıtı alması için zaman aşımını ayarlar. Varsayılan NetX Duo SMTP Istemci değeri 10 saniyedir.
- **NX_SMTP_ENVELOPE_TIMEOUT** Bu seçenek, Istemci için sunucu yanıtı almak üzere Istemcinin zaman aşımını ayarlar. Varsayılan NetX Duo SMTP Istemci değeri 10 saniyedir.
- **NX_SMTP_MESSAGE_TIMEOUT** Bu seçenek, e-posta iletisi verilerini almak üzere Istemcinin sunucu yanıtı alması için zaman aşımını ayarlar. Varsayılan NetX Duo SMTP Istemcisi değeri 30 saniyedir.
- **NX_SMTP_CLIENT_SEND_TIMEOUT** Bu seçenek, SMTP kimlik doğrulaması sırasında sunucu ile Kullanıcı parolasını depolamak için arabellek bekleme seçeneğini tanımlar. Varsayılan değer 20 bayttır.
- **NX_SMTP_SERVER_CHALLENGE_MAX_STRING** Bu seçenek, SMTP kimlik doğrulaması sırasında sunucu sınamasını ayıklama için arabellek boyutunu tanımlar. Varsayılan değer 200 bayttır. OTURUM açma ve düz kimlik doğrulama için, SMTP Istemcisi muhtemelen daha küçük bir arabellek kullanabilir.
- **NX_SMTP_CLIENT_MAX_PASSWORD** Bu seçenek, SMTP kimlik doğrulaması sırasında sunucu ile Kullanıcı parolasını depolamak için arabelleğin boyutunu tanımlar. Varsayılan değer 20 bayttır. 
- **NX_SMTP_CLIENT_MAX_USERNAME** Bu seçenek, sunucu ile SMTP kimlik doğrulaması sırasında konak Kullanıcı adını depolamak için arabelleğin boyutunu tanımlar. Varsayılan değer 40 bayttır. 
