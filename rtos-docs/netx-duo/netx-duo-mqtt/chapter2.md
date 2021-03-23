---
title: Bölüm 2-Azure RTOS NetX Duo MQTT istemcisini yükleme ve kullanma
description: Bu bölüm, NetX Duo MQTT Istemci bileşeninin yüklenmesi, kurulumu ve kullanımı ile ilgili çeşitli sorunların açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: cde19a0e84f369f1199ea4027fa09e6bd038e837
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825907"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-duo-mqtt-client"></a>Bölüm 2-Azure RTOS NetX Duo MQTT istemcisini yükleme ve kullanma

Bu bölümde, Azure RTOS NetX Duo MQTT istemci bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların açıklaması yer almaktadır.

## <a name="product-distribution"></a>Ürün dağıtımı

NetX Duo için MQTT Istemcisi, adresinde bulunabilir [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo) . Paket iki kaynak dosyası, bir içerme dosyası ve bu belgeyi içeren bir dosyayı aşağıdaki gibi içerir:

- **nxd_mqtt_client. h** NetX Duo için MQTT Istemcisi üst bilgi dosyası
- **nxd_mqtt_client. c** NetX Duo için MQTT Istemcisi için C kaynak dosyası
- **nxd_mqtt_client.pdf** NetX Duo için MQTT Istemcisinin açıklaması
- **demo_mqtt_client. c** NetX Duo MQTT gösterimi

## <a name="mqtt-client-installation"></a>MQTT Istemci yüklemesi

NetX Duo için MQTT Istemcisini kullanmak istiyorsanız, daha önce bahsedilen dağıtımın tamamı NetX Duo 'un yüklü olduğu dizine kopyalanmalıdır. Örneğin, "*\threadx\arm7\green*" dizininde NETX Duo yüklüyse, NETX Duo MQTT istemcisinin *nxd_mqtt_client. h* ve *nxd_mqtt_client. c* ' nin bu dizine kopyalanması gerekir.

## <a name="using-mqtt-client"></a>MQTT Istemcisini kullanma

NetX Duo için MQTT Istemcisini kullanmak kolaydır. Temel olarak, uygulama kodu *nxd_mqtt_client.* h ve *tx_api* . h ve *nx_api. h* Içermelidir. Bu, sırasıyla threadx ve NETX Duo kullanmak için. MQTT Istemci üst bilgi dosyaları eklendikten sonra, uygulama kodu daha sonra bu kılavuzun ilerleyen kısımlarında açıklanan MQTT hizmetlerini kullanabilir. Uygulama, yapı işlemine *nxd_mqtt_client. c* de içermelidir. Bu dosyalar, diğer uygulama dosyalarıyla aynı şekilde derlenmesi gerekir ve nesne formu, uygulamanın dosyalarıyla birlikte bağlanmalıdır. Bu, NetX Duo MQTT Istemcisini kullanmak için gereklidir.

## <a name="using-mqtt-client-with-netx-secure-tls"></a>NetX güvenli TLS ile MQTT Istemcisini kullanma

MQTT istemcisini NetX güvenli TLS modülü ile birlikte kullanmak için, uygulama NetX güvenli TLS modülünün yüklü olması ve *nx_secure_tls_api. h* ve *nx_crypto. h* içermelidir. MQTT kitaplığı, tanımlı ***NX_SECURE_ENABLE*** simgesiyle oluşturulmalıdır.

## <a name="configuration-options"></a>Yapılandırma seçenekleri

NetX Duo için MQTT istemcisi oluşturmaya yönelik birkaç yapılandırma seçeneği vardır. Aşağıda, her birinin ayrıntılı olarak açıklandığı tüm seçeneklerin bir listesi verilmiştir. Varsayılan değerler listelenir, ancak *nxd_mqtt_client. h* 'ye dahil etmeden önce yeniden tanımlanabilir.

- **NX_DISABLE_ERROR_CHECKING**: tanımlı, bu seçenek temel MQTT istemci hata denetimini kaldırır. Genellikle uygulamanın hata ayıklaması yapıldıktan sonra kullanılır.
- **NX_SECURE_ENABLE**: TANıMLı, MQTT istemcisi TLS desteğiyle oluşturulmuştur.
Bu sembolün tanımlanması için NetX güvenli TLS modülünün yüklenmesi gerekir.
*NX_SECURE_ENABLE* varsayılan olarak etkinleştirilmemiştir. * *
- **NXD_MQTT_REQUIRE_TLS**: tanımlı, uygulamanın MQTT aracısına bağlanmak için TLS kullanması gerekir. Bu özellik için *NX_SECURE_ENABLE* tanımlanmalıdır. Varsayılan olarak, bu simge tanımlı değildir.
- **NXD_MQTT_MAX_TOPIC_NAME_LENGTH**: kullanım dışı.
- **NXD_MQTT_MAX_MESSAGE_LENGTH**: kullanım dışı.
- **NXD_MQTT_KEEPALIVE_TIMER_RATE**: threadx Zamanlayıcı işaretleri içinde MQTT Zamanlayıcı hızını tanımlar. Bu süreölçer, son MQTT denetimi iletisinin gönderilme zamanından sonraki süreyi izlemek için kullanılır ve canlı tutma süresi dolmadan önce bir MQTT PINGREQ iletisi gönderir. Bu süreölçer, istemci, etkin tut zamanlayıcı değeri kümesiyle aracıya bağlanırsa etkinleştirilir. Varsayılan değer, tek saniyelik bir Zamanlayıcı olan TX_TIMER_TICKS_PER_SECOND.
- **NXD_MQTT_PING_TIMEOUT_DELAY**: MQTT istemcisinin, MQTT pingreq gönderildikten sonra ARACıDAN pingyanıt beklediği süreyi tanımlar. Bu zaman aşımı gecikmesinden sonra herhangi bir PINGYANıT alınmadığında, istemci aracıyı yanıt vermeyen olarak değerlendirir ve aracının aracısıyla bağlantısını keser. Varsayılan PING zaman aşımı gecikmesi, bir saniye olan TX_TIMER_TICKS_PER_SECOND.
- **NXD_MQTT_SOCKET_TIMEOUT**: süreölçer onay işaretleri 'nde MQTT sunucusundan bağlantı kesilirken TCP yuvası bağlantı kesme çağrısında zaman aşımını tanımlar. Varsayılan değer NX_WAIT_FOREVER.

## <a name="sample-mqtt-program"></a>Örnek MQTT programı

Aşağıdaki program basit bir MQTT uygulamasını göstermektedir. Kolaylık olması için, dönüş kodlarının başarılı olduğu varsayılır, bu nedenle başka bir hata denetimi yapılmaz.

```c
#define LOCAL_SERVER_ADDRESS (IP_ADDRESS(192, 168, 1, 81))

/*******************************************************/
/* IOT MQTT Client Example                             */
/*******************************************************/
#define DEMO_STACK_SIZE 2048
#define CLIENT_ID_STRING "mytestclient"
#define MQTT_CLIENT_STACK_SIZE 4096
#define STRLEN(p) (sizeof(p) - 1)

/* Declare the MQTT thread stack space. */
static ULONG mqtt_client_stack[MQTT_CLIENT_STACK_SIZE / sizeof(ULONG)];

/* Declare the MQTT client control block. */
static NXD_MQTT_CLIENT mqtt_client;

/* Define the symbol for signaling a received message. */

/* Define the test threads. */

#define TOPIC_NAME "topic"

#define MESSAGE_STRING "This is a message. "

/* Define the priority of the MQTT internal thread. */
#define MQTT_THREAD_PRIORTY 2

/* Define the MQTT keep alive timer for 5 minutes */
#define MQTT_KEEP_ALIVE_TIMER 300
#define QOS0 0
#define QOS1 1

/* Declare event flag, which is used in this demo. */
TX_EVENT_FLAGS_GROUP mqtt_app_flag;
#define DEMO_MESSAGE_EVENT 1
#define DEMO_ALL_EVENTS 3

/* Declare buffers to hold message and topic. */
static UCHAR message_buffer[NXD_MQTT_MAX_MESSAGE_LENGTH];
static UCHAR topic_buffer[NXD_MQTT_MAX_TOPIC_NAME_LENGTH];

/* Declare the disconnect notify function. */
static VOID my_disconnect_func(NXD_MQTT_CLIENT *client_ptr)
{
    printf("client disconnected from server\n");
}

static VOID my_notify_func(NXD_MQTT_CLIENT* client_ptr, UINT number_of_messages)
{
    tx_event_flags_set(&mqtt_app_flag, DEMO_MESSAGE_EVENT, TX_OR);
    return;
}

static ULONG error_counter;
void demo_mqtt_client_local(NX_IP *ip_ptr, NX_PACKET_POOL *pool_ptr)
{
    UINT status;
    NXD_ADDRESS server_ip;
    ULONG events;
    UINT topic_length, message_length;

    /* Create MQTT client instance. */
    nxd_mqtt_client_create(&mqtt_client, "my_client",
        CLIENT_ID_STRING, STRLEN(CLIENT_ID_STRING), ip_ptr, pool_ptr,
        (VOID*)mqtt_client_stack, sizeof(mqtt_client_stack),
        MQTT_THREAD_PRIORTY, NX_NULL, 0);

    /* Register the disconnect notification function. */
    nxd_mqtt_client_disconnect_notify_set(&mqtt_client, my_disconnect_func);

    /* Create an event flag for this demo. */
    status = tx_event_flags_create(&mqtt_app_flag, "my app event");
    server_ip.nxd_ip_version = 4;
    server_ip.nxd_ip_address.v4 = LOCAL_SERVER_ADDRESS;

    /* Start the connection to the server. */
    nxd_mqtt_client_connect(&mqtt_client, &server_ip, NXD_MQTT_PORT, 
        MQTT_KEEP_ALIVE_TIMER, 0, NX_WAIT_FOREVER);

    /* Subscribe to the topic with QoS level 0. */
    nxd_mqtt_client_subscribe(&mqtt_client, TOPIC_NAME, STRLEN(TOPIC_NAME),
        QOS0);

    /* Set the receive notify function. */
    nxd_mqtt_client_receive_notify_set(&mqtt_client, my_notify_func);

    /* Publish a message with QoS Level 1. */
    nxd_mqtt_client_publish(&mqtt_client, TOPIC_NAME,
        STRLEN(TOPIC_NAME), (CHAR*)MESSAGE_STRING, 
        STRLEN(MESSAGE_STRING), 0, QOS1, NX_WAIT_FOREVER);

    /* Now wait for the broker to publish the message. */
    tx_event_flags_get(&mqtt_app_flag, DEMO_ALL_EVENTS,
        TX_OR_CLEAR, &events, TX_WAIT_FOREVER);

    if(events & DEMO_MESSAGE_EVENT)
    {
        nxd_mqtt_client_message_get(&mqtt_client, topic_buffer,
            sizeof(topic_buffer), &topic_length, message_buffer,
            sizeof(message_buffer), &message_length);

        topic_buffer[topic_length] = 0;

        message_buffer[message_length] = 0;

        printf("topic = %s, message = %s\n", topic_buffer, message_buffer);
    }

    /* Now unsubscribe the topic. */
    nxd_mqtt_client_unsubscribe(&mqtt_client, TOPIC_NAME,
        STRLEN(TOPIC_NAME));

    /* Disconnect from the broker. */
    nxd_mqtt_client_disconnect(&mqtt_client);

    /* Delete the client instance, release all the resources. */
    nxd_mqtt_client_delete(&mqtt_client);
    return;
}
```
