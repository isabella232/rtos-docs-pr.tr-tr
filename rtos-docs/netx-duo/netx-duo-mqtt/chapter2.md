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
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-duo-mqtt-client"></a><span data-ttu-id="95b79-103">Bölüm 2-Azure RTOS NetX Duo MQTT istemcisini yükleme ve kullanma</span><span class="sxs-lookup"><span data-stu-id="95b79-103">Chapter 2 - Installation and use of Azure RTOS NetX Duo MQTT client</span></span>

<span data-ttu-id="95b79-104">Bu bölümde, Azure RTOS NetX Duo MQTT istemci bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların açıklaması yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="95b79-104">This chapter contains a description of various issues related to installation, setup, and usage of the Azure RTOS NetX Duo MQTT client component.</span></span>

## <a name="product-distribution"></a><span data-ttu-id="95b79-105">Ürün dağıtımı</span><span class="sxs-lookup"><span data-stu-id="95b79-105">Product Distribution</span></span>

<span data-ttu-id="95b79-106">NetX Duo için MQTT Istemcisi, adresinde bulunabilir [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo) .</span><span class="sxs-lookup"><span data-stu-id="95b79-106">MQTT Client for NetX Duo is available at [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo).</span></span> <span data-ttu-id="95b79-107">Paket iki kaynak dosyası, bir içerme dosyası ve bu belgeyi içeren bir dosyayı aşağıdaki gibi içerir:</span><span class="sxs-lookup"><span data-stu-id="95b79-107">The package includes two source files, one include file, and a file that contains this document, as follows:</span></span>

- <span data-ttu-id="95b79-108">**nxd_mqtt_client. h** NetX Duo için MQTT Istemcisi üst bilgi dosyası</span><span class="sxs-lookup"><span data-stu-id="95b79-108">**nxd_mqtt_client.h** Header file for MQTT Client for NetX Duo</span></span>
- <span data-ttu-id="95b79-109">**nxd_mqtt_client. c** NetX Duo için MQTT Istemcisi için C kaynak dosyası</span><span class="sxs-lookup"><span data-stu-id="95b79-109">**nxd_mqtt_client.c** C Source file for MQTT Client for NetX Duo</span></span>
- <span data-ttu-id="95b79-110">**nxd_mqtt_client.pdf** NetX Duo için MQTT Istemcisinin açıklaması</span><span class="sxs-lookup"><span data-stu-id="95b79-110">**nxd_mqtt_client.pdf** Description of MQTT Client for NetX Duo</span></span>
- <span data-ttu-id="95b79-111">**demo_mqtt_client. c** NetX Duo MQTT gösterimi</span><span class="sxs-lookup"><span data-stu-id="95b79-111">**demo_mqtt_client.c** NetX Duo MQTT demonstration</span></span>

## <a name="mqtt-client-installation"></a><span data-ttu-id="95b79-112">MQTT Istemci yüklemesi</span><span class="sxs-lookup"><span data-stu-id="95b79-112">MQTT Client Installation</span></span>

<span data-ttu-id="95b79-113">NetX Duo için MQTT Istemcisini kullanmak istiyorsanız, daha önce bahsedilen dağıtımın tamamı NetX Duo 'un yüklü olduğu dizine kopyalanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="95b79-113">In order to use MQTT Client for NetX Duo, the entire distribution mentioned previously should be copied to the same directory where NetX Duo is installed.</span></span> <span data-ttu-id="95b79-114">Örneğin, "*\threadx\arm7\green*" dizininde NETX Duo yüklüyse, NETX Duo MQTT istemcisinin *nxd_mqtt_client. h* ve *nxd_mqtt_client. c* ' nin bu dizine kopyalanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="95b79-114">For example, if NetX Duo is installed in the directory "*\threadx\arm7\green*" then the *nxd_mqtt_client.h* and *nxd_mqtt_client.c* for NetX Duo MQTT Client need to be copied into this directory.</span></span>

## <a name="using-mqtt-client"></a><span data-ttu-id="95b79-115">MQTT Istemcisini kullanma</span><span class="sxs-lookup"><span data-stu-id="95b79-115">Using MQTT Client</span></span>

<span data-ttu-id="95b79-116">NetX Duo için MQTT Istemcisini kullanmak kolaydır.</span><span class="sxs-lookup"><span data-stu-id="95b79-116">Using MQTT Client for NetX Duo is easy.</span></span> <span data-ttu-id="95b79-117">Temel olarak, uygulama kodu *nxd_mqtt_client.* h ve *tx_api* . h ve *nx_api. h* Içermelidir. Bu, sırasıyla threadx ve NETX Duo kullanmak için.</span><span class="sxs-lookup"><span data-stu-id="95b79-117">Basically, the application code must include *nxd_mqtt_client.h* after it includes *tx_api.h* and *nx_api.h*, in order to use ThreadX, and NetX Duo, respectively.</span></span> <span data-ttu-id="95b79-118">MQTT Istemci üst bilgi dosyaları eklendikten sonra, uygulama kodu daha sonra bu kılavuzun ilerleyen kısımlarında açıklanan MQTT hizmetlerini kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="95b79-118">Once the MQTT Client header files are included, the application code is then able to use the MQTT services described later in this guide.</span></span> <span data-ttu-id="95b79-119">Uygulama, yapı işlemine *nxd_mqtt_client. c* de içermelidir.</span><span class="sxs-lookup"><span data-stu-id="95b79-119">The application must also include *nxd_mqtt_client.c* in the build process.</span></span> <span data-ttu-id="95b79-120">Bu dosyalar, diğer uygulama dosyalarıyla aynı şekilde derlenmesi gerekir ve nesne formu, uygulamanın dosyalarıyla birlikte bağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="95b79-120">These files must be compiled in the same manner as other application files and its object form must be linked along with the files of the application.</span></span> <span data-ttu-id="95b79-121">Bu, NetX Duo MQTT Istemcisini kullanmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="95b79-121">This is all that is required to use NetX Duo MQTT Client.</span></span>

## <a name="using-mqtt-client-with-netx-secure-tls"></a><span data-ttu-id="95b79-122">NetX güvenli TLS ile MQTT Istemcisini kullanma</span><span class="sxs-lookup"><span data-stu-id="95b79-122">Using MQTT Client with NetX Secure TLS</span></span>

<span data-ttu-id="95b79-123">MQTT istemcisini NetX güvenli TLS modülü ile birlikte kullanmak için, uygulama NetX güvenli TLS modülünün yüklü olması ve *nx_secure_tls_api. h* ve *nx_crypto. h* içermelidir.</span><span class="sxs-lookup"><span data-stu-id="95b79-123">To use MQTT client with NetX Secure TLS module, application must have NetX Secure TLS module installed, and include *nx_secure_tls_api.h* and *nx_crypto.h*.</span></span> <span data-ttu-id="95b79-124">MQTT kitaplığı, tanımlı ***NX_SECURE_ENABLE*** simgesiyle oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="95b79-124">The MQTT library must be built with the symbol ***NX_SECURE_ENABLE*** defined.</span></span>

## <a name="configuration-options"></a><span data-ttu-id="95b79-125">Yapılandırma seçenekleri</span><span class="sxs-lookup"><span data-stu-id="95b79-125">Configuration Options</span></span>

<span data-ttu-id="95b79-126">NetX Duo için MQTT istemcisi oluşturmaya yönelik birkaç yapılandırma seçeneği vardır.</span><span class="sxs-lookup"><span data-stu-id="95b79-126">There are several configuration options for building MQTT client for NetX Duo.</span></span> <span data-ttu-id="95b79-127">Aşağıda, her birinin ayrıntılı olarak açıklandığı tüm seçeneklerin bir listesi verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="95b79-127">Following is a list of all options, where each is described in detail.</span></span> <span data-ttu-id="95b79-128">Varsayılan değerler listelenir, ancak *nxd_mqtt_client. h* 'ye dahil etmeden önce yeniden tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="95b79-128">The default values are listed, but can be redefined prior to inclusion of *nxd_mqtt_client.h.*</span></span>

- <span data-ttu-id="95b79-129">**NX_DISABLE_ERROR_CHECKING**: tanımlı, bu seçenek temel MQTT istemci hata denetimini kaldırır.</span><span class="sxs-lookup"><span data-stu-id="95b79-129">**NX_DISABLE_ERROR_CHECKING**: Defined, this option removes the basic MQTT client error checking.</span></span> <span data-ttu-id="95b79-130">Genellikle uygulamanın hata ayıklaması yapıldıktan sonra kullanılır.</span><span class="sxs-lookup"><span data-stu-id="95b79-130">It is typically used after the application has been debugged.</span></span>
- <span data-ttu-id="95b79-131">**NX_SECURE_ENABLE**: TANıMLı, MQTT istemcisi TLS desteğiyle oluşturulmuştur.</span><span class="sxs-lookup"><span data-stu-id="95b79-131">**NX_SECURE_ENABLE**: Defined, MQTT Client is built with TLS support.</span></span>
<span data-ttu-id="95b79-132">Bu sembolün tanımlanması için NetX güvenli TLS modülünün yüklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="95b79-132">Defining this symbol requires NetX Secure TLS module to be installed.</span></span>
<span data-ttu-id="95b79-133">*NX_SECURE_ENABLE* varsayılan olarak etkinleştirilmemiştir. \* \*</span><span class="sxs-lookup"><span data-stu-id="95b79-133">*NX_SECURE_ENABLE* is not enabled by default.\*\*</span></span>
- <span data-ttu-id="95b79-134">**NXD_MQTT_REQUIRE_TLS**: tanımlı, uygulamanın MQTT aracısına bağlanmak için TLS kullanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="95b79-134">**NXD_MQTT_REQUIRE_TLS**: Defined, application must use TLS to connect to MQTT broker.</span></span> <span data-ttu-id="95b79-135">Bu özellik için *NX_SECURE_ENABLE* tanımlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="95b79-135">This feature requires *NX_SECURE_ENABLE* defined.</span></span> <span data-ttu-id="95b79-136">Varsayılan olarak, bu simge tanımlı değildir.</span><span class="sxs-lookup"><span data-stu-id="95b79-136">By default, this symbol is not defined.</span></span>
- <span data-ttu-id="95b79-137">**NXD_MQTT_MAX_TOPIC_NAME_LENGTH**: kullanım dışı.</span><span class="sxs-lookup"><span data-stu-id="95b79-137">**NXD_MQTT_MAX_TOPIC_NAME_LENGTH**: Deprecated.</span></span>
- <span data-ttu-id="95b79-138">**NXD_MQTT_MAX_MESSAGE_LENGTH**: kullanım dışı.</span><span class="sxs-lookup"><span data-stu-id="95b79-138">**NXD_MQTT_MAX_MESSAGE_LENGTH**: Deprecated.</span></span>
- <span data-ttu-id="95b79-139">**NXD_MQTT_KEEPALIVE_TIMER_RATE**: threadx Zamanlayıcı işaretleri içinde MQTT Zamanlayıcı hızını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="95b79-139">**NXD_MQTT_KEEPALIVE_TIMER_RATE**: Defines the MQTT timer rate, in ThreadX timer ticks.</span></span> <span data-ttu-id="95b79-140">Bu süreölçer, son MQTT denetimi iletisinin gönderilme zamanından sonraki süreyi izlemek için kullanılır ve canlı tutma süresi dolmadan önce bir MQTT PINGREQ iletisi gönderir.</span><span class="sxs-lookup"><span data-stu-id="95b79-140">This timer is used to keep track of the time since last MQTT control message was sent, and sends out an MQTT PINGREQ message before the keep-alive time expires.</span></span> <span data-ttu-id="95b79-141">Bu süreölçer, istemci, etkin tut zamanlayıcı değeri kümesiyle aracıya bağlanırsa etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="95b79-141">This timer is activated if the client connects to the broker with a keep-alive timer value set.</span></span> <span data-ttu-id="95b79-142">Varsayılan değer, tek saniyelik bir Zamanlayıcı olan TX_TIMER_TICKS_PER_SECOND.</span><span class="sxs-lookup"><span data-stu-id="95b79-142">The default value is TX_TIMER_TICKS_PER_SECOND, which is a one-second timer.</span></span>
- <span data-ttu-id="95b79-143">**NXD_MQTT_PING_TIMEOUT_DELAY**: MQTT istemcisinin, MQTT pingreq gönderildikten sonra ARACıDAN pingyanıt beklediği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="95b79-143">**NXD_MQTT_PING_TIMEOUT_DELAY**: Defines the time the MQTT client waits for PINGRESP from the broker after it sends out MQTT PINGREQ.</span></span> <span data-ttu-id="95b79-144">Bu zaman aşımı gecikmesinden sonra herhangi bir PINGYANıT alınmadığında, istemci aracıyı yanıt vermeyen olarak değerlendirir ve aracının aracısıyla bağlantısını keser.</span><span class="sxs-lookup"><span data-stu-id="95b79-144">If no PINGRESP is received after this timeout delay, the client treats the broker as non-responsive and disconnects itself from the broker.</span></span> <span data-ttu-id="95b79-145">Varsayılan PING zaman aşımı gecikmesi, bir saniye olan TX_TIMER_TICKS_PER_SECOND.</span><span class="sxs-lookup"><span data-stu-id="95b79-145">The default PING timeout delay is TX_TIMER_TICKS_PER_SECOND, which is one second.</span></span>
- <span data-ttu-id="95b79-146">**NXD_MQTT_SOCKET_TIMEOUT**: süreölçer onay işaretleri 'nde MQTT sunucusundan bağlantı kesilirken TCP yuvası bağlantı kesme çağrısında zaman aşımını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="95b79-146">**NXD_MQTT_SOCKET_TIMEOUT**: Defines the time out in the TCP socket disconnect call when disconnecting from the MQTT server in timer ticks.</span></span> <span data-ttu-id="95b79-147">Varsayılan değer NX_WAIT_FOREVER.</span><span class="sxs-lookup"><span data-stu-id="95b79-147">The default value is NX_WAIT_FOREVER.</span></span>

## <a name="sample-mqtt-program"></a><span data-ttu-id="95b79-148">Örnek MQTT programı</span><span class="sxs-lookup"><span data-stu-id="95b79-148">Sample MQTT program</span></span>

<span data-ttu-id="95b79-149">Aşağıdaki program basit bir MQTT uygulamasını göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="95b79-149">The following program illustrates a simple MQTT application.</span></span> <span data-ttu-id="95b79-150">Kolaylık olması için, dönüş kodlarının başarılı olduğu varsayılır, bu nedenle başka bir hata denetimi yapılmaz.</span><span class="sxs-lookup"><span data-stu-id="95b79-150">For simplicity, the return codes are assumed to be successful, therefore no further error checking is done.</span></span>

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
