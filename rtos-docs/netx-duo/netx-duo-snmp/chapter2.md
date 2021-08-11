---
title: Bölüm 2-Azure RTOS NetX Duo SNMP aracısını yükleme ve kullanma
description: Bu bölümde, NetX Duo SNMP aracı bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 6e18906b6356bd8ff4efdc1ab0f2809d75493ad027c3d3e27e0536ee4b80f43b
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116798291"
---
# <a name="chapter-2---installation-and-use-of-the-azure-rtos-netx-duo-snmp-agent"></a>Bölüm 2-Azure RTOS NetX Duo SNMP aracısını yükleme ve kullanma

Bu bölümde, Azure RTOS NetX Duo SNMP aracı bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların açıklaması yer almaktadır.

## <a name="product-distribution"></a>Ürün dağıtımı

NetX Duo için SNMP Aracısı adresinde bulunabilir [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo) . Bu paket dört kaynak dosyası, bir içerme dosyası ve bu belgeyi içeren bir PDF dosyası içerir ve aşağıdaki gibi:

- **nxd_snmp. h** NetX Duo için SNMP için üst bilgi dosyası
- **demo_snmp_helper. h** SNMP MıB verileri için üst bilgi dosyası
- **nxd_snmp. c** NetX Duo için SNMP Aracısı için C kaynak dosyası
- **nx_md5. c** MD5 Özet algoritmaları
- **nx_sha. c** SHA Özet algoritmaları
- **nx_des. c** DES şifreleme algoritmaları
- **nxd_snmp.pdf** NetX Duo için SNMP Aracısı Kullanıcı Kılavuzu
- **demo_netxduo_snmp. c** Basit SNMP tanıtımı
- **demo_netxduo_mib2. c** Basit MıB2 tanıtımı (MıB 'nin IPv6 adres öğeleri vardır)
- **demo_snmp_helper. h** MıB öğelerini tanımlayan üstbilgi dosyası

## <a name="netx-duo-snmp-agent-installation"></a>NetX Duo SNMP aracısını yükleme

NetX Duo SNMP 'yi kullanmak için, daha önce bahsedilen dağıtımın tamamı NetX Duo 'un yüklü olduğu dizine kopyalanmalıdır. Örneğin, "*\threadx\arm7\green*" dizininde NETX Duo yüklüyse, *nxd_snmp. h*, *nxd_snmp. c*, *nx_md5. c, nx_sha. c* ve nx_ *des. c* dosyaları bu dizine kopyalanmalıdır.

## <a name="using-the-netx-duo-snmp-agent"></a>NetX Duo SNMP aracısını kullanma

Uygulama, derleme projesinde *nxd_snmp. c*, *nx_md5. c, nx_sha. c* ve *nx_des. c* olmalıdır. Uygulama kodu Ayrıca, SNMP hizmetlerini çağırabilmek *için nx_api. h* öğesini ekledikten sonra *nxd_snmp. h* içermelidir. Bu dosyalar, diğer uygulama dosyalarıyla aynı şekilde derlenmelidir ve nesne formu NetX Duo kitaplığı ile bağlantılı olmalıdır. Bu, NetX Duo SNMP 'yi kullanmak için gereklidir.

> [!NOTE]
> *Yapı işleminde **NX_SNMP_NO_SECURITY** belirtilirse, nx_md5. c, nx_sha. c ve nx_des. c dosyaları gerekli değildir.*

> [!NOTE]
> NetX Duo SNMP 'nin UDP hizmetlerini kullandığından bu yana, SNMP kullanmadan önce *nx_udp_enable* çağrısıyla UDP 'nin etkinleştirilmesi gerekir.

## <a name="small-example-system"></a>Küçük örnek sistem

NetX Duo SNMP aracısının nasıl kullanılacağına ilişkin bir örnek aşağıda gösterilen Şekil 1,0 ' de açıklanmıştır. Bu örnekte, *nxd_snmp. h* SNMP içerme dosyası 6. satırda getirilir. *Demo_snmp_helper. h* MIB veritabanı öğelerini tanımlayan üstbilgi dosyası, 8. satırda getirilir. MıB, 32 satırından başlayarak tanımlanmıştır. Sonra SNMP Aracısı, 129 satırındaki "*tx_application_define*" içinde oluşturulur. SNMP Aracısı denetim bloğunun "*my_agent*", daha önce 16. satırda genel bir değişken olarak tanımlandığını unutmayın. IPv6 etkinse IPv6 adresleri, 166-223. satırda IP örneğiyle kaydedilir. SNMP Aracısı 229. satırda başlatılır. SNMP Yöneticisi GET, GETNEXT ve SET isteklerinin yanı sıra Kullanıcı adı ve MıB güncelleştirme istekleri için SNMP nesne geri çağırma tanımları, 250 satırından başlayarak işlenir. Bu örnekte, kimlik doğrulaması gerçekleştirilmez.

> [!NOTE]
> *Aşağıda gösterilen MıB2 tablosu yalnızca bir örnektir. Uygulama farklı bir MıB kullanabilir ve ayrı dosyalara dahil edebilir ve uygulama gereksinimlerine göre GET, GETNEXT veya SET işlemesini tanımlayabilir.*

```c
/* This is a small demo of the NetX SNMP Agent on the high-performance NetX TCP/IP  
   stack. This demo relies on ThreadX and NetX to show simple SNMP the SNMP
   GET/GETNEXT/SET requests on MIB-2 objects.  */

#include  "tx_api.h"
#include  "nx_api.h"
#include  "nxd_snmp.h"
#include  "demo_snmp_helper.h"

#define     DEMO_STACK_SIZE         4096
#define     AGENT_PRIMARY_ADDRESS   IP_ADDRESS(192, 2, 2, 66)

/* Define the ThreadX and NetX object control blocks...  */

TX_THREAD               thread_0;
NX_PACKET_POOL          pool_0;
NX_IP                   ip_0;
NX_SNMP_AGENT           my_agent;


/* Indicate if using IPv6 to communicate with SNMP servers. Note that
   IPv6 must be enabled in the NetX Duo library first. Further, IPv6
   and ICMPv6 services are enabled before starting the SNMP agent. */
#define USE_IPV6


/* Define authentication and privacy keys.  */

#ifdef AUTHENTICATION_REQUIRED
NX_SNMP_SECURITY_KEY    my_authentication_key;
#endif

#ifdef PRIVACY_REQUIRED
NX_SNMP_SECURITY_KEY    my_privacy_key;
#endif

/* Define an error counter variable. */
UINT error_counter = 0;

/* This binds a secondary interfaces to the primary IP network interface 
   if SNMP is required for required for that interface. */
/* #define  MULTI_HOMED_DEVICE */

/* Define function prototypes.  A generic ram driver is used in this demo.  However
   to properly run an SNMP agent demo, a real driver should be substituted. */

VOID    thread_agent_entry(ULONG thread_input);
VOID    _nx_ram_network_driver(NX_IP_DRIVER *driver_req_ptr);
UINT    mib2_get_processing(NX_SNMP_AGENT *agent_ptr, UCHAR *object_requested, 
                            NX_SNMP_OBJECT_DATA *object_data);
UINT    mib2_getnext_processing(NX_SNMP_AGENT *agent_ptr, UCHAR *object_requested, 
                            NX_SNMP_OBJECT_DATA *object_data);
UINT    mib2_set_processing(NX_SNMP_AGENT *agent_ptr, UCHAR *object_requested, 
                            NX_SNMP_OBJECT_DATA *object_data);
UINT    mib2_username_processing(NX_SNMP_AGENT *agent_ptr, UCHAR *username);
VOID    mib2_variable_update(NX_IP *ip_ptr, NX_SNMP_AGENT *agent_ptr);


UCHAR context_engine_id[] = {0x80, 0x00, 0x0d, 0xfe, 0x03, 0x00, 0x11, 0x23, 0x23, 
                             0x44, 0x55};
UINT  context_engine_size = 11;
UCHAR context_name[] = {0x69, 0x6e, 0x69, 0x74, 0x69, 0x61, 0x6c};
UINT  context_name_size = 7;

/* Define main entry point.  */

int main()
{

   /* Enter the ThreadX kernel.  */
   tx_kernel_enter();
}


/* Define what the initial system looks like.  */
void    tx_application_define(void *first_unused_memory)
{

UCHAR   *pointer;
UINT    status;


   /* Setup the working pointer.  */
   pointer =  (UCHAR *) first_unused_memory;

   status = tx_thread_create(&thread_0, "agent thread", thread_agent_entry, 0,  
            pointer, DEMO_STACK_SIZE, 
            4, 4, TX_NO_TIME_SLICE, TX_AUTO_START);
   if (status != NX_SUCCESS)
   {
      return;
   }

   pointer =  pointer + DEMO_STACK_SIZE;


   /* Initialize the NetX system.  */
   nx_system_initialize();

   /* Create packet pool.  */
   status = nx_packet_pool_create(&pool_0, "NetX Packet Pool 0", 2048, 
                                   pointer, 20000);

   if (status != NX_SUCCESS)
   {
      return;
   }
  
   pointer = pointer + 20000;
  
   /* Create an IP instance.  */
   status = nx_ip_create(&ip_0, "SNMP Agent IP Instance", AGENT_PRIMARY_ADDRESS, 
                        0xFFFFFF00UL, &pool_0, _nx_ram_network_driver,
                        pointer, 4096, 1);

   if (status != NX_SUCCESS)
   {
      return;
   }
  
   pointer =  pointer + 4096;
  
   /* Enable ARP and supply ARP cache memory for IP Instance 0.  */
   nx_arp_enable(&ip_0, (void *) pointer, 1024);
   pointer = pointer + 1024;

   /* Enable UPD processing for IP instance.  */
   nx_udp_enable(&ip_0);
  
   /* Enable ICMP for ping.  */
   nx_icmp_enable(&ip_0);
  
   /* Create an SNMP agent instance.  */
   status = nx_snmp_agent_create(&my_agent, "SNMP Agent", &ip_0, pointer, 4096, 
                                 &pool_0, 
                                 mib2_username_processing, mib2_get_processing, 
                                 mib2_getnext_processing, 
                                 mib2_set_processing);


  
   if (status != NX_SUCCESS)
   {
      return;
   }
  
   pointer =  pointer + 4096;
  
   status = nx_snmp_agent_context_engine_set(&my_agent, context_engine_id, 
                                             context_engine_size);
  
   if (status != NX_SUCCESS)
   {
      error_counter++;
   }
  
   return;
}
  
VOID thread_agent_entry(ULONG thread_input)
{
  
#ifdef USE_IPV6
UINT        iface_index, address_index;
UINT        status;
NXD_ADDRESS agent_ipv6_address;
#endif
  
  
      /* Allow NetX time to get initialized. */
      tx_thread_sleep(100);
  
      /* If using IPv6, enable IPv6 and ICMPv6 services and get IPv6 addresses 
         registered with NetX Dou. */
  
#ifdef USE_IPV6
  
      /* Enable IPv6 on the IP instance. */
      status = nxd_ipv6_enable(&ip_0);
   
      /* Check for enable errors.  */
      if (status)
      {
  
         error_counter++;
         return;
      }
      /* Enable ICMPv6 on the IP instance. */
      status = nxd_icmp_enable(&ip_0);
  
      /* Check for enable errors.  */
      if (status)
      {
  
         error_counter++;
         return;
      }
  
      agent_ipv6_address.nxd_ip_address.v6[3] = 0x101;
      agent_ipv6_address.nxd_ip_address.v6[2] = 0x0;
      agent_ipv6_address.nxd_ip_address.v6[1] = 0x0000f101;
      agent_ipv6_address.nxd_ip_address.v6[0] = 0x20010db8;
      agent_ipv6_address.nxd_ip_version = NX_IP_VERSION_V6;
  
      /* Set the primary interface for our DNS IPv6 addresses. */
      iface_index = 0;
  
      /* This assumes we are using the primary network interface (index 0). */
      status = nxd_ipv6_address_set(&ip_0, iface_index, NX_NULL, 10, &address_index);
  
      /* Check for link local address set error.  */
      if (status) 
      {
  
         error_counter++;
         return;
      }
  
      /* Set the host global IP address. We are assuming a 64 
         bit prefix here but this can be any value (< 128). */
      status = nxd_ipv6_address_set(&ip_0, iface_index, &agent_ipv6_address, 64, 
                                    &address_index);
  
      /* Check for global address set error.  */
      if (status) 
      {
  
         error_counter++;
         return;
      }

      /* Wait while NetX Duo validates the link local and global address. */
      tx_thread_sleep(500);
#endif
  
#ifdef AUTHENTICATION_REQUIRED

      /* Create an authentication key.  */
      nx_snmp_agent_md5_key_create(&my_agent, "authpassword", &my_authentication_key);
  
      /* Use the authentication key.  */
      nx_snmp_agent_authenticate_key_use(&my_agent, &my_authentication_key);
#endif
  
#ifdef PRIVACY_REQUIRED
  
      /* Create a privacy key.  */
      nx_snmp_agent_md5_key_create(&my_agent, "privpassword", &my_privacy_key);
  
      /* Use the privacy key.  */
      nx_snmp_agent_privacy_key_use(&my_agent, &my_privacy_key);
#endif
  
      /* Start the SNMP instance.  */
      nx_snmp_agent_start(&my_agent);
  
}
  
/* Define the application's GET processing routine.  */
  
UINT    mib2_get_processing(NX_SNMP_AGENT *agent_ptr, UCHAR *object_requested, 
                            NX_SNMP_OBJECT_DATA *object_data)
{
  
UINT    i;
UINT    status;
  
  
      printf("SNMP Manager GET Request For:  %s", object_requested);
  
      /* Loop through the sample MIB to see if we have information for the supplied 
         variable.  */
      i =  0;
      status =  NX_SNMP_ERROR;
      while (mib2_mib[i].object_name)
      {
  
         /* See if we have found the matching entry.  */
         status =  nx_snmp_object_compare(object_requested, mib2_mib[i].object_name);
  
         /* Was it found?  */
         if (status == NX_SUCCESS)
         {
  
            /* Yes it was found.  */
            break;
         }
  
         /* Move to the next index.  */
         i++;
      }
  
      /* Determine if a not found condition is present.  */
      if (status != NX_SUCCESS)
      {
  
         printf(" NO SUCH NAME!\n");
  
         /* The object was not found - return an error.  */
         return(NX_SNMP_ERROR_NOSUCHNAME);
      }
  
      /* Determine if the entry has a get function.  */
      if (mib2_mib[i].object_get_callback)
      {
  
         /* Yes, call the get function.  */
         status =  (mib2_mib[i].object_get_callback)(mib2_mib[i].object_value_ptr, 
                                                     object_data);
      }
      else
      {
  
         printf(" NO GET FUNCTION!");
  
         /* No get function, return no access.  */
         status =  NX_SNMP_ERROR_NOACCESS;
      }
  
      printf("\n");

      /* Return the status.  */
      return(status);
}
  
  
/* Define the application's GETNEXT processing routine.  */
  
UINT    mib2_getnext_processing(NX_SNMP_AGENT *agent_ptr, UCHAR *object_requested, 
                                NX_SNMP_OBJECT_DATA *object_data)
{
  
UINT    i;
UINT    status;
  
  
   printf("SNMP Manager GETNEXT Request For:  %s", object_requested);
  
   /* Loop through the sample MIB to see if we have information for the supplied 
      variable.  */
      i =  0;
      status =  NX_SNMP_ERROR;
      while (mib2_mib[i].object_name)
      {
  
         /* See if we have found the next entry.  */
         status =  nx_snmp_object_compare(object_requested, mib2_mib[i].object_name);
  
         /* Is the next entry the mib greater?  */
         if (status == NX_SNMP_NEXT_ENTRY)
         {
  
            /* Yes it was found.  */
            break;
         }
  
         /* Move to the next index.  */
         i++;
      }
  
      /* Determine if a not found condition is present.  */
      if (status != NX_SNMP_NEXT_ENTRY)
      {
  
         printf(" NO SUCH NAME!\n");
  
         /* The object was not found - return an error.  */
         return(NX_SNMP_ERROR_NOSUCHNAME);
      }
  
  
      /* Copy the new name into the object.  */
      nx_snmp_object_copy(mib2_mib[i].object_name, object_requested);
  
      printf(" Next Name is: %s", object_requested);
  
      /* Determine if the entry has a get function.  */
      if (mib2_mib[i].object_get_callback)
      {
  
         /* Yes, call the get function.  */
         status =  (mib2_mib[i].object_get_callback)(mib2_mib[i].object_value_ptr, 
                                                     object_data);
  
         /* Determine if the object data indicates an end-of-mib condition.  */
         if (object_data -> nx_snmp_object_data_type == NX_SNMP_END_OF_MIB_VIEW)
         {
  
            /* Copy the name supplied in the mib table.  */
            nx_snmp_object_copy(mib2_mib[i].object_value_ptr, object_requested);
         }
      }
      else
      {
  
         printf(" NO GET FUNCTION!");
  
         /* No get function, return no access.  */
         status =  NX_SNMP_ERROR_NOACCESS;
      }
  
      printf("\n");

      /* Return the status.  */
      return(status);
}
  
  
/* Define the application's SET processing routine.  */
  
UINT    mib2_set_processing(NX_SNMP_AGENT *agent_ptr, UCHAR *object_requested, 
                            NX_SNMP_OBJECT_DATA *object_data)
{
  
UINT    i;
UINT    status;
  
  
   printf("SNMP Manager SET Request For:  %s", object_requested);
  
   /* Loop through the sample MIB to see if we have information for the supplied variable.  */
      i =  0;
      status =  NX_SNMP_ERROR;
      while (mib2_mib[i].object_name)
      {
  
         /* See if we have found the matching entry.  */
         status =  nx_snmp_object_compare(object_requested, mib2_mib[i].object_name);
  
         /* Was it found?  */
         if (status == NX_SUCCESS)
         {
  
            /* Yes it was found.  */
            break;
         }
  
         /* Move to the next index.  */
         i++;
      }
  
      /* Determine if a not found condition is present.  */
      if (status != NX_SUCCESS)
      {
  
         printf(" NO SUCH NAME!\n");
  
         /* The object was not found - return an error.  */
         return(NX_SNMP_ERROR_NOSUCHNAME);
      }
  
  
      /* Determine if the entry has a set function.  */
      if (mib2_mib[i].object_set_callback)
      {
  
         /* Yes, call the set function.  */
         status =  (mib2_mib[i].object_set_callback)(mib2_mib[i].object_value_ptr, 
                                                     object_data);
      }
      else
      {
  
         printf(" NO SET FUNCTION!");
  
         /* No get function, return no access.  */
         status =  NX_SNMP_ERROR_NOACCESS;
      }
  
      printf("\n");

      /* Return the status.  */
      return(status);
}
  
  
/* Define the application's authentication routine.  */
  
UINT  mib2_username_processing(NX_SNMP_AGENT *agent_ptr, UCHAR *username)
{
  
      printf("Username is:  %s\n", username);
  
      /* Update MIB-2 objects. In this example, it is only the SNMP objects.  */
      mib2_variable_update(&ip_0, &my_agent);
  
      /* No authentication is done, just return success!  */
      return(NX_SUCCESS);
}
  
  
/* Define the application's update routine.  */ 
  
VOID  mib2_variable_update(NX_IP *ip_ptr, NX_SNMP_AGENT *agent_ptr)
{
  
      /* Update the snmp parameters.  */
      snmpInPkts =                agent_ptr -> nx_snmp_agent_packets_received;
      snmpOutPkts =               agent_ptr -> nx_snmp_agent_packets_sent;
      snmpInBadVersions =         agent_ptr -> nx_snmp_agent_invalid_version;
      snmpInBadCommunityNames =   agent_ptr -> nx_snmp_agent_authentication_errors;
      snmpInBadCommunityUsers =   agent_ptr -> nx_snmp_agent_username_errors; 
      snmpInASNParseErrs =        agent_ptr -> nx_snmp_agent_internal_errors;
      snmpInTotalReqVars =        agent_ptr -> nx_snmp_agent_total_get_variables;
      snmpInTotalSetVars =        agent_ptr -> nx_snmp_agent_total_set_variables;
      snmpInGetRequests =         agent_ptr -> nx_snmp_agent_get_requests;
      snmpInGetNexts =            agent_ptr -> nx_snmp_agent_getnext_requests;
      snmpInSetRequests =         agent_ptr -> nx_snmp_agent_set_requests;
      snmpOutTooBigs =            agent_ptr -> nx_snmp_agent_too_big_errors;
      snmpOutNoSuchNames =        agent_ptr -> nx_snmp_agent_no_such_name_errors;
      snmpOutBadValues =          agent_ptr -> nx_snmp_agent_bad_value_errors;
      snmpOutGenErrs =            agent_ptr -> nx_snmp_agent_general_errors;
      snmpOutTraps =              agent_ptr -> nx_snmp_agent_traps_sent;
}   
```
Şekil 1,0 NetX Duo ile SNMP Aracısı kullanımı örneği

## <a name="configuration-options"></a>Yapılandırma seçenekleri

NetX Duo için SNMP oluşturmaya yönelik birkaç yapılandırma seçeneği vardır. Aşağıda, her birinin ayrıntılı olarak açıklandığı tüm seçeneklerin bir listesi verilmiştir:  
  
| Tanımlayın                     | Anlamı                                                                                                                                                                                                                                                                        |
|----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **NX_SNMP_AGENT_PRIORITY**     | SNMP ARACıSı iş parçacığının önceliği. Varsayılan olarak, 16 önceliğini belirtmek için bu değer 16 olarak tanımlanır.                                                                                                                                                                         |
| **NX_SNMP_TYPE_OF_SERVICE**    | SNMP UDP yanıtları için gereken hizmet türü. Varsayılan olarak, bu değer normal IP paket hizmetini göstermek için NX_IP_NORMAL olarak tanımlanır. Bu tanımlama, *nxd_snmp. h* 'ye dahil etmeden önce uygulama tarafından ayarlanabilir.                                                       |
| **NX_SNMP_FRAGMENT_OPTION**    | SNMP UDP istekleri için parça etkinleştirme. Varsayılan olarak, bu değer SNMP UDP fragmenting devre dışı bırakmak için NX_DONT_FRAGMENT. Bu tanımlama, *nxd_snmp. h* 'ye dahil etmeden önce uygulama tarafından ayarlanabilir.                                                                                 |
| **NX_SNMP_TIME_TO_LIVE**       | Süresi dolmadan önce yaşam süresini belirtir. Varsayılan değer 0x80 olarak ayarlanır, ancak *nxd_snmp. h* 'ye dahil etmeden önce yeniden tanımlanabilir.                                                                                                                                         |
| **NX_SNMP_AGENT_TIMEOUT**      | İç hizmetlerin askıya alınacağı ThreadX ticks sayısını belirtir. Varsayılan değer 100 olarak ayarlanır, ancak *nxd_snmp. h* 'ye dahil etmeden önce yeniden tanımlanabilir.                                                                                                         |
| **NX_SNMP_MAX_OCTET_STRING**   | SNMP aracısında bir Sekizli dizesinde izin verilen en fazla bayt sayısını belirtir. Varsayılan değer 255 olarak ayarlanır, ancak *nxd_snmp. h* 'ye dahil etmeden önce yeniden tanımlanabilir.                                                                                                    |
| **NX_SNMP_MAX_CONTEXT_STRING** | SNMP aracısında bir bağlam altyapısı dizesi için en fazla bayt sayısını belirtir. Varsayılan değer 32 olarak ayarlanır, ancak *nxd_snmp. h* 'ye dahil etmeden önce yeniden tanımlanabilir.                                                                                                    |
| **NX_SNMP_MAX_USER_NAME**      | Kullanıcı adında en fazla bayt sayısını belirtir (topluluk dizeleri dahil). Varsayılan değer 64 olarak ayarlanır, ancak *nxd_snmp. h* 'ye dahil etmeden önce yeniden tanımlanabilir.                                                                                                      |
| **NX_SNMP_MAX_SECURITY_KEY**   | Bir güvenlik anahtarı dizesinde izin verilen bayt sayısını belirtir. Varsayılan değer 64 olarak ayarlanır, ancak *nxd_snmp. h* 'nin nclusion öğesinden önce yeniden tanımlanabilir.                                                                                                                          |
| **NX_SNMP_PACKET_SIZE**        | SNMP Aracısı oluşturulurken belirtilen havuzdaki paketlerin en küçük boyutunu belirtir. En küçük boyut, tüm SNMP yükünün tek bir pakette yer aldığından emin olmak için gereklidir. Varsayılan değer 560 olarak ayarlanır, ancak *nxd_snmp. h* 'ye dahil etmeden önce yeniden tanımlanabilir. |
| **NX_SNMP_AGENT_PORT**         | Üzerinde SNMP Yöneticisi isteklerinin alan UDP bağlantı noktasını belirtir. Varsayılan bağlantı noktası UDP bağlantı noktası 161 ' dir, ancak *nxd_snmp. h* 'ye dahil etmeden önce yeniden tanımlanabilir.                                                                                                                             |
| **NX_SNMP_MANAGER_TRAP_PORT**  | SNMP Aracısı tuzak isteklerinin gönderileceği UDP bağlantı noktasını belirtir. Varsayılan bağlantı noktası UDP bağlantı noktası 162 ' dir, ancak *nxd_snmp. h* 'ye dahil etmeden önce yeniden tanımlanabilir.                                                                                                                           |
| **NX_SNMP_MAX_TRAP_NAME**      | Tuzak iletileriyle gönderilen Kullanıcı adının tutulacağı dizinin boyutunu belirtir. Varsayılan değer 64 ' dir.                                                                                                                                                                         |
| **NX_SNMP_MAX_TRAP_KEY**       | Tuzak iletileri için kimlik doğrulama ve gizlilik anahtarlarının boyutunu belirtir. Varsayılan değer 64 ' dir.                                                                                                                                                                          |
| **NX_SNMP_TIME_INTERVAL**      | Bu, alınan SNMP paketlerini işleme arasındaki SNMP iş parçacığı görevi tarafından alınan Zamanlayıcı onay işaretleri içindeki uyku aralığını belirler. Varsayılan değer 100’dür. Bu uyku aralığında, konak uygulamanın SNMP API hizmetlerine erişimi vardır.                                           |
| **NX_SNMP_DISABLE_V1**         | Bu, *nxd_snmp. c* IÇINDEKI tüm SNMP sürüm 1 işlemesini kaldırır. Bu, varsayılan olarak tanımlı değildir.                                                                                                                                                                         |
| **NX_SNMP_DISABLE_V2**         | Bu, *nxd_snmp. c* IÇINDEKI tüm SNMP sürüm 2 işlemesini kaldırır. Bu, varsayılan olarak tanımlı değildir.                                                                                                                                                                         |
| **NX_SNMP_DISABLE_V3**         | Tanımlandı, bu işlem nxd_snmp.c'de SNMPv3 *işlemeyi kaldırır.* Varsayılan olarak bu tanımlanmamıştır.                                                                                                                                                                                 |