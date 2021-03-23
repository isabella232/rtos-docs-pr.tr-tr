---
title: Bölüm 2-Azure RTOS NetX PPPoE sunucusunu yükleme ve kullanma
description: Bu bölümde, Azure RTOS NetX PPPoE sunucu bileşeninin yüklenmesi, kurulumu ve kullanımı ile ilgili çeşitli sorunların bir açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 5b52164911676b68c67da01d698e41c02730e45a
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825588"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-pppoe-server"></a>Bölüm 2-Azure RTOS NetX PPPoE sunucusunu yükleme ve kullanma

Bu bölümde, Azure RTOS NetX PPPoE sunucu bileşeninin yüklenmesi, kurulumu ve kullanımı ile ilgili çeşitli sorunların bir açıklaması yer almaktadır.

## <a name="product-distribution"></a>Ürün dağıtımı

NetX için PPPoE sunucusu, adresinde bulunabilir [https://github.com/azure-rtos/netx](https://github.com/azure-rtos/netx) . Paket, aşağıdaki gibi, bu belgeyi içeren iki kaynak dosya ve bir PDF dosyası içerir:

- **nx_pppoe_server. h**: NETX Için PPPoE sunucusu için üst bilgi dosyası
- **nx_pppoe_server. c**: NETX Için PPPoE sunucusu Için c kaynak dosyası
- **nx_pppoe_server.pdf**: NETX Için PPPoE sunucusunun PDF açıklaması
- **demo_netx_pppoe_server. c**: NETX PPPoE sunucu tanıtımı

## <a name="pppoe-server-installation"></a>PPPoE sunucu yüklemesi

NetX için PPPoE sunucusunu kullanabilmeniz için, daha önce bahsedilen dağıtımın tamamı, NetX 'in yüklü olduğu dizine kopyalanmalıdır. Örneğin, "*\threadx\arm7\green*" dizininde NETX yüklüyse, *nx_pppoe_server. h* ve *nx_pppoe_server. c* dosyaları bu dizine kopyalanmalıdır.

## <a name="using-pppoe-server"></a>PPPoE sunucusunu kullanma

NetX için PPPoE sunucusu kullanmak kolaydır. Temel olarak, uygulama kodu sırasıyla ThreadX ve NetX kullanmak için *tx_api. h* ve *nx_api. h* dahil *nx_pppoe_server.* h içermelidir. *Nx_pppoe_server. h* eklendikten sonra, uygulama kodu bu kılavuzda daha sonra belirtilen PPPoE sunucu işlev çağrılarını yapabilir. Uygulama, yapı işlemine *nx_pppoe_server. c* de içermelidir. Bu dosya, diğer uygulama dosyalarıyla aynı şekilde derlenmelidir ve nesne formu, uygulamanın dosyalarıyla birlikte bağlanmalıdır. Bu, NetX PPPoE sunucusunu kullanmak için gereklidir.

## <a name="small-example-system"></a>Küçük örnek sistem

Aşağıda, The NetX PPPoE sunucusunun nasıl kullanıldığını gösteren bir örnek verilmiştir. Şekil 1,1. Bu örnekte, PPPoE sunucusu içerme dosyası *nx_pppoe_server. h* , 50. satırda getirilir. Ardından, PPPoE sunucusu 248 satırındaki *"thread_0_entry*" içinde oluşturulur. IP örneği oluşturulduktan sonra PPPoE sunucusunun oluşturulması gerektiğini unutmayın. IP örneği oluşturulur ve line165 başlatılır. "*Pppoe_server*" PPPoE sunucu denetim bloğu, daha önce satır 79 ' de genel bir değişken olarak tanımlandı. Bildirim işlevleri, satır 257 ' de ayarlanır. Pppoe_session_data_receive bildirme işlevinin ayarlanmış olması gerektiğini unutmayın. IP ve PPPoE sunucusu başarıyla oluşturulduktan sonra, PPPoE sunucusu, 272 satırındaki nx_pppoe_server_enable çağrısında bir PPPoE oturumu oluşturma işlemidir.

Genel olarak, PPPoE modülünün PPP modülüyle birlikte kullanılması gerekir. Bu örnekte, PPP sunucusu içerme dosyası *nx_ppp. h* , 49. satırda getirilir. Daha sonra, 174 satırındaki PPP sunucusu oluşturulur. Satır 182 PPP paketini göndermek için işlevi ayarlayın. Satır 188-200 IP adreslerini ayarlayın ve PAP protokolünü tanımlayın. Satır 115-139 PAP protokolü için Kullanıcı adı ve parola ayarlayın.

PPPoE oturumu kurulduktan sonra. Uygulama, 281 satırındaki oturum bilgilerini (istemci MAC adresi ve oturum kimliği) almak için nx_pppoe_server_session_get çağırabilir.

Uygulama artık PPP trafiğini işlememesi durumunda, uygulama PppCloseInd veya nx_pppoe_server_session_terminate ve PPPoE oturumunu sonlandırır.

> [!NOTE]
> Bu örnekte, PPPoE sunucusu normal IP Stack ile aynı anda çalışır ve bir Ethernet sürücüsünü paylaşır. Normal IP örneği için aynı Ethernet sürücüsünü, 165. satırda ve PPPoE sunucu 248 örneğine geçirin.

> [!NOTE]
> İşlevler, tanımlanan NX_PPPoE_SERVER_SESSION_CONTROL_ENABELE altında yazılım tarafından çağrılması için PPPoE uygulamasıyla sağlanır.

Tanımlanmışsa, PPPoE oturumunu denetleyen özelliği sunar.

Uygulama belirli API 'yi çağırana kadar, PPPoE sunucusu isteğe otomatik olarak yanıt vermez, PPPoE sunucusu isteğe otomatik olarak yanıt vermez. Nx_pppoe_server. h içinde varsayılan olarak etkinleştirilir.

Fiziksel üstbilgiyi doldurmak için yeterli alan olduğundan emin olmak için **NX_PHYSICAL_HEADER** 24 ' e yeniden tanımlayın. Fiziksel üst bilgi: 14 (Ethernet üstbilgisi) + 6 (PPPoE üstbilgisi) + 2 (PPP üstbilgisi) + 2 (dört baytlık bir Aligment).

```c
/**************************************************************************/
/**************************************************************************/
/**                                                                       */
/** NetX PPPoE Server stack Component                                     */
/**                                                                       */
/** This is a small demo of the high-performance NetX PPPoE Server        */
/** stack. This demo includes IP instance, PPPoE Server and PPP Server    */
/** stack. Create one IP instance includes two interfaces to support      */
/** for normal IP stack and PPPoE Server, PPPoE Server can use the        */
/** mutex of IP instance to send PPPoE message when share one Ethernet    */
/** driver. PPPoE Server work with normal IP instance at the same time.   */
/**                                                                       */
/** Note1: Substitute your Ethernet driver instead of                     */
/** _nx_ram_network_driver before run this demo                           */
/**                                                                       */
/** Note2: Prerequisite for using PPPoE.                                  */
/** Redefine NX_PHYSICAL_HEADER to 24 to ensure enough space for filling  */
/** in physical header. Physical header:14(Ethernet header)               */
/** + 6(PPPoE header) + 2(PPP header) + 2(four-byte aligment)             */
/**                                                                       */
/**************************************************************************/
/**************************************************************************/


/*****************************************************************/
/*                            NetX Stack                         */
/*****************************************************************/

                                      /***************************/
                                      /* PPP Server              */
                                      /***************************/

                                      /***************************/
                                      /* PPPoE Server            */
                                      /***************************/
/***************************/         /***************************/
/* Normal Ethernet Type    */         /* PPPoE Ethernet Type     */
/***************************/         /***************************/
/***************************/         /***************************/
/* Interface 0             */         /* Interface 1             */
/***************************/         /***************************/

/*****************************************************************/
/*                     Ethernet Dirver                           */
/*****************************************************************/

#include     "tx_api.h"
#include     "nx_api.h"
#include     "nx_ppp.h"
#include     "nx_pppoe_server.h"

/* Defined NX_PPP_PPPOE_ENABLE if use Express Logic's PPP, since PPP module has been modified to match PPPoE moduler under this definition. */
#ifdef NX_PPP_PPPOE_ENABLE

/*   If the driver is not initialized in other module, define */
/*   NX_PPPOE_SERVER_INITIALIZE_DRIVER_ENABLE to initialize the driver in PPPoE module. */
/*   In this demo, the driver has been initialized in IP module. */

#ifdef NX_PPPOE_SERVER_INITIALIZE_DRIVER_ENABLE

/*   NX_PPPOE_SERVER_SESSION_CONTROL_ENABLE: If defined, enables the feature that */
/*   controls the PPPoE session. PPPoE server does not automatically response to the */
/*   request until application call specific API. */

/* Define the block size. */
#define     NX_PACKET_POOL_SIZE     ((1536 + sizeof(NX_PACKET)) * 30)
#define     DEMO_STACK_SIZE         2048
#define     PPPOE_THREAD_SIZE       2048

/* Define the ThreadX and NetX object control blocks... */
TX_THREAD           thread_0;

/* Define the packet pool and IP instance for normal IP instnace. */
NX_PACKET_POOL      pool_0;
NX_IP               ip_0;

/* Define the PPP Server instance. */
NX_PPP              ppp_server;

/* Define the PPPoE Server instance. */
NX_PPPOE_SERVER     pppoe_server;

/* Define the counters. */
CHAR                *pointer;
ULONG               error_counter;

/* Define thread prototypes. */
void     thread_0_entry(ULONG thread_input);

/***** Substitute your PPP driver entry function here *********/
extern void     _nx_ppp_driver(NX_IP_DRIVER *driver_req_ptr);

/***** Substitute your Ethernet driver entry function here *********/
extern void     _nx_ram_network_driver(NX_IP_DRIVER *driver_req_ptr);

/* Define the callback functions. */
void     PppDiscoverReq(UINT interfaceHandle);
void     PppOpenReq(UINT interfaceHandle, ULONG length, UCHAR *data);
void     PppCloseRsp(UINT interfaceHandle);
void     PppCloseReq(UINT interfaceHandle);
void     PppTransmitDataReq(UINT interfaceHandle, ULONG length, UCHAR *data, UINT packet_id);
void     PppReceiveDataRsp(UINT interfaceHandle, UCHAR *data);

/* Define the porting layer function for Express Logic's PPP to simulate TTP's PPP. */
/* Functions to be provided by PPP for calling by the PPPoE Stack. */
void     ppp_server_packet_send(NX_PACKET *packet_ptr);

/* Define main entry point. */

int main()
{

    /* Enter the ThreadX kernel. */
    tx_kernel_enter();
}

UINT verify_login(CHAR *name, CHAR *password)
{

    if ((name[0] == 'm') &&
        (name[1] == 'y') &&
        (name[2] == 'n') &&
        (name[3] == 'a') &&
        (name[4] == 'm') &&
        (name[5] == 'e') &&
        (name[6] == (CHAR) 0) &&
        (password[0] == 'm') &&
        (password[1] == 'y') &&
        (password[2] == 'p') &&
        (password[3] == 'a') &&
        (password[4] == 's') &&
        (password[5] == 's') &&
        (password[6] == 'w') &&
        (password[7] == 'o') &&
        (password[8] == 'r') &&
        (password[9] == 'd') &&
        (password[10] == (CHAR) 0))
            return(NX_SUCCESS);
    else
        return(NX_PPP_ERROR);
}

/* Define what the initial system looks like. */

void tx_application_define(void *first_unused_memory)
{

    UINT status;

    /* Setup the working pointer. */
    pointer = (CHAR *) first_unused_memory;

    /* Initialize the NetX system. */
    nx_system_initialize();

    /* Create a packet pool for normal IP instance. */
    status = nx_packet_pool_create(&pool_0, "NetX Main Packet Pool",
                                    (1536 + sizeof(NX_PACKET)),
                                    pointer, NX_PACKET_POOL_SIZE);
                                    pointer = pointer + NX_PACKET_POOL_SIZE;

    /* Check for error. */
    if (status)
        error_counter++;

    /* Create an normal IP instance. */
    status = nx_ip_create(&ip_0, "NetX IP Instance", IP_ADDRESS(192, 168, 100, 43),
                        0xFFFFFF00UL, &pool_0, _nx_ram_network_driver,
                        pointer, 2048, 1);
                        pointer = pointer + 2048;

    /* Check for error. */
    if (status)
        error_counter++;

    /* Create the PPP instance. */
    status = nx_ppp_create(&ppp_server, "PPP Instance", &ip_0, pointer, 2048, 1,
                            &pool_0, NX_NULL, NX_NULL);
    pointer = pointer + 2048;

    /* Check for PPP create error. */
    if (status)
        error_counter++;

    /* Set the PPP packet send function. */
    status = nx_ppp_packet_send_set(&ppp_server, ppp_server_packet_send);

    /* Check for PPP packet send function set error. */
    if (status)
        error_counter++;

    /* Define IP address. This PPP instance is effectively the server since it has both IP addresses. */
    status = nx_ppp_ip_address_assign(&ppp_server, IP_ADDRESS(192, 168, 10, 43),                                         IP_ADDRESS(192, 168, 10, 44));

    /* Check for PPP IP address assign error. */
    if (status)
        error_counter++;

    /* Setup PAP, this PPP instance is effectively the server since it will verify the name and password. */
    status = nx_ppp_pap_enable(&ppp_server, NX_NULL, verify_login);

    /* Check for PPP PAP enable error. */
    if (status)
        error_counter++;

    /* Attach an interface for PPP. */
    status = nx_ip_interface_attach(&ip_0, "Second Interface For PPP", 
                            IP_ADDRESS(0, 0, 0, 0), 0, nx_ppp_driver);

    /* Check for error. */
    if (status)
        error_counter++;

    /* Enable ARP and supply ARP cache memory for Normal IP Instance. */
    status = nx_arp_enable(&ip_0, (void *) pointer, 1024);
    pointer = pointer + 1024;

    /* Check for ARP enable errors. */
    if (status)
        error_counter++;

    /* Enable ICMP */
    status = nx_icmp_enable(&ip_0);
    if(status)
        error_counter++;

    /* Enable UDP traffic. */
    status = nx_udp_enable(&ip_0);
    if (status)
        error_counter++;

    /* Enable TCP traffic. */
    status = nx_tcp_enable(&ip_0);
    if (status)
        error_counter++;

    /* Create the main thread. */
    tx_thread_create(&thread_0, "thread 0", thread_0_entry, 0,
                    pointer, DEMO_STACK_SIZE,
                    4, 4, TX_NO_TIME_SLICE, TX_AUTO_START);
                    pointer = pointer + DEMO_STACK_SIZE;
}

/* Define the test threads. */

void     thread_0_entry(ULONG thread_input)
{
UINT     status;
ULONG    ip_status;

    /* Create the PPPoE instance. */
    status = nx_pppoe_server_create(&pppoe_server, (UCHAR *)"PPPoE Server", &ip_0, 0,
                    _nx_ram_network_driver, &pool_0, pointer, PPPOE_THREAD_SIZE, 4);
    pointer = pointer + PPPOE_THREAD_SIZE;
    if (status)
    {
        error_counter++;
        return;
    }

    /* Set the callback notify function. */
    status = nx_pppoe_server_callback_notify_set(&pppoe_server, PppDiscoverReq,
        PppOpenReq, PppCloseRsp, PppCloseReq, PppTransmitDataReq, PppReceiveDataRsp);

    if (status)
    {
        error_counter++;
        return;
    }

    #ifdef NX_PPPOE_SERVER_SESSION_CONTROL_ENABLE
        /* Call function function to set the default service Name. */
        /* PppInitInd(length, aData); */
    #endif /* NX_PPPOE_SERVER_SESSION_CONTROL_ENABLE */

    /* Enable PPPoE Server. */
    status = nx_pppoe_server_enable(&pppoe_server);
    if (status)
    {
        error_counter++;
        return;
    }

    /* Get the PPPoE Client physical address and Session ID after establish PPPoE Session. */
    /*
        status = nx_pppoe_server_session_get(&pppoe_server, interfaceHandle, &client_mac_msw, &client_mac_lsw, &session_id);
        if (status)
            error_counter++;
    */

    /* Wait for the link to come up. */
    status = nx_ip_interface_status_check(&ip_0, 1, NX_IP_ADDRESS_RESOLVED,
                                            &ip_status, NX_WAIT_FOREVER);
    if (status)
    {
        error_counter++;
        return;
    }

    #ifdef NX_PPPOE_SERVER_SESSION_CONTROL_ENABLE
        /* Call PPPoE function to terminate the PPPoE Session. */
        /* PppCloseInd(interfaceHandle, causeCode); */
    #endif /* NX_PPPOE_SERVER_SESSION_CONTROL_ENABLE */

}

void     PppDiscoverReq(UINT interfaceHandle)
{

    /* Receive the PPPoE Discovery Initiation Message. */
    
    #ifdef NX_PPPOE_SERVER_SESSION_CONTROL_ENABLE
        /* Call PPPoE function to allow TTP's software to define the Service Name field of the PADO packet. */
        PppDiscoverCnf(0, NX_NULL, interfaceHandle);
    #endif /* NX_PPPOE_SERVER_SESSION_CONTROL_ENABLE */
}

void     PppOpenReq(UINT interfaceHandle, ULONG length, UCHAR *data)
{

    /* Get the notify that receive the PPPoE Discovery Request Message. */

    #ifdef NX_PPPOE_SERVER_SESSION_CONTROL_ENABLE
        /* Call PPPoE function to allow TTP's software to accept the PPPoE session. */
        PppOpenCnf(NX_TRUE, interfaceHandle);
    #endif /* NX_PPPOE_SERVER_SESSION_CONTROL_ENABLE */
}

void     PppCloseRsp(UINT interfaceHandle)
{

    /* Get the notify that receive the PPPoE Discovery Terminate Message. */

    #ifdef NX_PPPOE_SERVER_SESSION_CONTROL_ENABLE
        /* Call PPPoE function to allow TTP's software to confirm that the handle has been freed. */
        PppCloseCnf(interfaceHandle);
    #endif /* NX_PPPOE_SERVER_SESSION_CONTROL_ENABLE */
}

void     PppCloseReq(UINT interfaceHandle)
{

    /* Get the notify that PPPoE Discovery Terminate Message has been sent. */

}

void     PppTransmitDataReq(UINT interfaceHandle, ULONG length, UCHAR *data, UINT packet_id)
{

    NX_PACKET *packet_ptr;

    /* Get the notify that receive the PPPoE Session data. */

    /* Call PPP Server to receive the PPP data fame. */
    packet_ptr = (NX_PACKET *)(packet_id);
    nx_ppp_packet_receive(&ppp_server, packet_ptr);

    #ifdef NX_PPPOE_SERVER_SESSION_CONTROL_ENABLE
        /* Call PPPoE function to confirm that the data has been processed. */
        PppTransmitDataCnf(interfaceHandle, data, packet_id);
    #endif /* NX_PPPOE_SERVER_SESSION_CONTROL_ENABLE */
}

void     PppReceiveDataRsp(UINT interfaceHandle, UCHAR *data)
{

    /* Get the notify that the PPPoE Session data has been sent. */

}

/* PPP Server send function. */
void     ppp_server_packet_send(NX_PACKET *packet_ptr)
{

    /* For Express Logic's PPP test, the session should be the first session, so set interfaceHandle as 0. */
    UINT interfaceHandle = 0;

    #ifdef NX_PPPOE_SERVER_SESSION_CONTROL_ENABLE
        while(packet_ptr)
        {

            /* Call functions to be provided by PPPoE for TTP. */
            PppReceiveDataInd(interfaceHandle, (packet_ptr -> nx_packet_append_ptr -
            packet_ptr -> nx_packet_prepend_ptr), packet_ptr -> nx_packet_prepend_ptr);

            /* Move to the next packet structure. */
            packet_ptr = packet_ptr -> nx_packet_next;
        }
    #else
        /* Directly Call PPPoE send function to send out the data through PPPoE module. */
        nx_pppoe_server_session_packet_send(&pppoe_server, interfaceHandle, packet_ptr);
    #endif /* NX_PPPOE_SERVER_SESSION_CONTROL_ENABLE */
}
#endif /* NX_PPPOE_SERVER_INITIALIZE_DRIVER_ENABLE */

#endif /* NX_PPP_PPPOE_ENABLE */
```

Şekil 1,1 NetX ile PPPoE sunucu kullanımı örneği

## <a name="configuration-options"></a>Yapılandırma seçenekleri

NetX için PPPoE sunucusu oluşturmaya yönelik birkaç yapılandırma seçeneği vardır. Aşağıdaki listede her biri ayrıntılı açıklanmıştır:

- **NX_DISABLE_ERROR_CHECKING**: tanımlı, bu seçenek temel PPPoE sunucusu hata denetimini kaldırır. Genellikle uygulamanın hata ayıklaması yapıldıktan sonra kullanılır.

- **NX_PPPOE_SERVER_SESSION_CONTROL_ENABLE**: tanımlanmışsa, PPPoE oturumunu denetleyen özelliği sunar. PPPoE sunucusu, uygulama belirli bir API 'YI çağırana kadar isteğe otomatik olarak yanıt vermez.

- **NX_PPPOE_SERVER_INITIALIZE_DRIVER_ENABLE**: tanımlanmışsa, özelliğin PPPoE modülünde Ethernet sürücüsünü başlatmasını sağlar. Varsayılan olarak devre dışı bırakılır.

- **NX_PPPOE_SERVER_THREAD_TIME_SLICE**: PPPoE sunucu iş parçacığı için zaman dilimi seçeneği. Varsayılan olarak, bu değer TX_NO_TIME_SLICE.

- **NX_PPPOE_SERVER_MAX_CLIENT_SESSION_NUMBER**: Bu, eşzamanlı istemci oturumlarının maksimum sayısını tanımlar. Varsayılan olarak, bu değer 10 ' dur.

- **NX_PPPOE_SERVER_MAX_HOST_UNIQ_SIZE**: bu konak-Uniq 'ın maksimum boyutunu tanımlar. Varsayılan olarak, bu değer 32 ' dir.

- **NX_PPPOE_SERVER_MAX_RELAY_SESSION_ID_SIZE**: Bu, maksimum geçiş-oturum kimliği boyutunu tanımlar. Varsayılan olarak, bu değer 12 ' dir.

- **NX_PPPOE_SERVER_MIN_PACKET_PAYLOAD_SIZE**: PPPoE sunucusu Için en düşük paket yükü boyutunu belirtir. Paket yükü boyutu bu değerden büyükse, paket zincirinden kaçınabilirsiniz. Varsayılan olarak, bu değer 1520 (en fazla Ethernet 1500, Ethernet üstbilgisi 14, CRC 2 ve dört baytlık hizalama 4).

- **NX_PPPOE_SERVER_PACKET_TIMEOUT**: Bu, paket ayırmak veya paketlere veri eklemek için beklemeyi (Zamanlayıcı işaretleri) belirler. Varsayılan olarak, bu değer **NX_IP_PERIODIC_RATE** (100 Ticks).

- **NX_PPPOE_SERVER_START_SESSION_ID**: Bu, PPPoE oturumuna atamaya yönelik başlangıç oturumu kimliğini tanımlar. Varsayılan olarak, bu değer 0X4944 ' dir (KIMLIK için ASCII değeri).