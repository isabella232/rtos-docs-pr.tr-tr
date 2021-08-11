---
title: Ek A-Azure RTOS NetX Duo DHCPv6 Istemcisi için geri yükleme durumu özelliğinin açıklaması
description: Azure RTOS NetX Duo DHDPv6 Istemci yapılandırma seçeneği NX_DHCPV6_CLIENT_RESTORE_STATE, sistemin önceden oluşturulmuş bir DHCP Istemcisini sistem yeniden başlatmalar arasında bir bağlantılı durumda geri yüklemesine olanak tanır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 6840f89e66d713b1839ac84427b73273b3f9601d4b6d9d39cd94908ac77a77ca
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116791338"
---
# <a name="appendix-a---description-of-the-restore-state-feature-for-azure-rtos-netx-duo-dhcpv6-client"></a>Ek A-Azure RTOS NetX Duo DHCPv6 Istemcisi için geri yükleme durumu özelliğinin açıklaması

Azure RTOS NetX Duo DHDPv6 Istemci yapılandırma seçeneği NX_DHCPV6_CLIENT_RESTORE_STATE, sistemin önceden oluşturulmuş bir DHCP Istemcisini sistem yeniden başlatmalar arasında bir bağlantılı durumda geri yüklemesine olanak tanır.

Bu seçenek ayrıca bir uygulamanın DHCPv6 Istemci iş parçacığını askıya almasına ve devam etmesine olanak tanır. Bu işlem, iş parçacığını kapatmadan askıya alma ve sürdürme arasındaki geçen süre ile güncelleştirilir.

## <a name="restoring-the-dhcpv6-client-between-reboots"></a>Yeniden başlatmalar arasında DHCPv6 Istemcisini geri yükleme

Bir DHCPv6 Istemcisini yeniden başlatmalar arasında geri yüklemek için, DHCPv6 uygulaması DHCPv6 Istemcisinin bir örneğini oluşturur ve ardından normal DHCPv6 protokolünü kullanarak bir IP adresi kirası edinir ve *nx_dhcpv6_start* çağırır. Ardından, DHCPv6 uygulaması protokolün tamamlanmasını bekler. Hepsi de varsa, cihaz, DHCPv6 sunucusundan atanan geçerli bir IP adresi ile bağlantılı duruma erişir. DHCPv6 Istemci uygulaması, kapatmadan önce geçerli DHCPv6 Istemci örneğini, daha sonra geçici olmayan bellekte saklanan bir DHCPv6 Istemci kaydına kaydeder. Sistemin başka bir yerindeki bağımsız bir ' Time Man ', bu güç durumundayken geçen sürenin izini tutar. Uygulama, yeni bir DHCPv6 Istemci örneği oluşturur ve daha önce oluşturulan DHCPv6 Istemci kaydıyla günceller. Geçen süre, "zaman Man" kaynağından alınır ve ardından DHCP Clientv6 kirası üzerinde kalan zamana uygulanır. Bu noktada uygulama, DHCPv6 Istemcisini sürdürür.

Güç kapatma sırasında geçen süre DHCPv6 Istemci durumunu yenıleme veya yeniden bağlama durumuna geçirir, DHCPv6 Istemcisi IP adresi kiralamasını yenilemek veya yeniden bağlamak isteyen DHCPv6 iletilerini otomatik olarak başlatır. IP adresinin geçerliliği dolmuşsa, DHCPv6 Istemcisi IP örneğindeki IP adresini otomatik olarak temizler ve yeni bir IP adresi isteyen başlangıç durumundan DHCPv6 işlemini başlatır.

Bu şekilde, DHCPv6 Istemcisi kesintisiz olarak yeniden başlatmalar arasında çalışabilir.

Bu özelliğin bir çizimi aşağıda verilmiştir.

```C
/* On the power up, create an IP instance, DHCPv6 Client, enable ICMPv6 and UDP
   and other resources (not shown) for the DHCPv6 Client/application
   in tx_application_define(). */
 
/* Define the DHCPv6 Client application thread. */     
void    thread_dhcpv6_client_entry(ULONG thread_input)
{

UINT        status;
UINT        time_elapsed = 0;
NX_DHCPV6_CLIENT_RECORD client_my_record;


    /* No previously saved Client record. Start the DHCPv6 Client in the INIT state. */
    status =  nx_dhcpv6_start(&dhcp_0);

    if (status !=NX_SUCCESS)
        return;

    while(1)    
    {
    
        /* Wait for DHCPv6 Client to get the IP address. */
    }

    /* At some point decide we power down the system. */

    /* Save the Client state data which we will subsequently need to restore the DHCPv6    
       Client. */
    status = nx_dhcpv6_client_get_record(&dhcp_0, &client_my_record);               

    /* Copy this memory to non-volatile memory (not shown). */

    /* Delete the IP and DHCPv6 Client instances before powering down. */
    nx_dhcpv6_client_delete(&dhcp_0);

    nx_ip_delete(&ip_0);

    /* Ready to power down, having released other resources as necessary. */

    /* The application has determined there is a previously saved record. We will 
       restore it to the current DHCPv6 Client instance. */

/* Create the IP and DHCPv6 Client instances, enable ICMPv6 and UDP after powering up. */

/* Calculate the time elapsed during power down */

    /* Get the previous Client state data from non-volatile memory. */

    /* Apply the record to the current Client instance. This will also 
       update the IP instance with IP address, mask etc. */
    status = nx_dhcpv6_client_restore_record(&dhcp_0, &client_my_record, time_elapsed);   

     if (status != NX_SUCCESS)
          return;

     /* We are ready to resume the DHCPv6 Client thread and use the assigned IP address. */
     status = nx_dhcpv6_resume(&dhcp_0);

     if (status != NX_SUCCESS)
          return;

}
```

## <a name="nx_dhcpv6_client_get_record"></a>nx_dhcpv6_client_get_record

Geçerli DHCPv6 Istemci durumunun bir kaydını oluştur

### <a name="prototype"></a>Prototype

```C
ULONG nx_dhcpv6_client_get_record(NX_DHCPV6 *dhcpv6_ptr, 
                                  NX_DHCPV6_CLIENT_RECORD *record_ptr);
```

### <a name="description"></a>Description

Bu hizmet, DHCPv6 Istemcisini record_ptr tarafından işaret edilen kayda kaydeder. Bu, DHCPv6 Istemci uygulamasının, bir güç kapatma ve yeniden başlatma gibi DHCPv6 Istemci durumunu geri yüklemesine olanak tanır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 Istemcisi işaretçisi

- **record_ptr** DHCPv6 Istemci kaydına yönelik işaretçi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS (0x0)** Geçerli Istemci kaydı oluşturuldu

- **NX_DHCPV6_NOT_BOUND** (0xe94) istemci bağlantılı durumda değil, bu nedenle geçerli IP adresi atanmadı

- **NX_PTR_ERROR** (0x16) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
NX_DHCPV6_CLIENT_RECORD dhcpv6_record;


/* Obtain a record of the current client state. */
status=  nx_dhcpv6_client_get_record(&dhcpv6_ptr, &dhcpv6_record);

/* If status is NX_SUCCESS dhcpv6_record contains the current DHCPv6 client record. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_dhcpv6_resume
- nx_dhcpv6_suspend
- nx_dhcpv6_client_restore_record

## <a name="nx_dhcpv6_client_restore_record"></a>nx_dhcpv6_client_restore_record

Kaydedilen kayıttaki DHCPv6 Istemci durumunu geri yükle

### <a name="prototype"></a>Prototype

```C
ULONG nx_dhcpv6_client_restore_record(NX_DHCPV6 *dhcpv6_ptr, 
                                      NX_DHCPV6_CLIENT_RECORD       
                                      *record_ptr, ULONG time_elapsed);
```

### <a name="description"></a>Description

Bu hizmet, DHCPv6 istemcisini record_ptr tarafından işaret edilen DHCPv6 istemci kaydıyla güncelleyerek ve DHCPv6 Istemci Kiralama üzerinde kalan süreyi time_elapsed girişi ile güncelleştirerek, bir DHCPv6 uygulamasının DHCPv6 Istemci durumunu önceki bir oturumdan yeniden oluşturmasını sağlar. Bu, DHCPv6 Istemci uygulamasının, DHCPv6 Istemcisini yeniden oluşturmasını sağlar, örneğin, kapatıldıktan sonra. Bu, DHCPv6 Istemci uygulamasının kapatmadan önce DHCPv6 Istemcisinin bir kaydını oluşturulmasını ve bu kaydın geçici olmayan belleğe kaydedilmesini gerektirir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 Istemcisi işaretçisi

- **record_ptr** DHCPv6 Istemci kaydına yönelik işaretçi

- **time_elapsed** Giriş istemci kaydında kalan kira zamanından çıkarma süresi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS (0x0)** İstemci kaydı geri yüklendi

- NX_PTR_ERROR (0x16) geçersiz Işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
NX_DHCPV6_CLIENT_RECORD dhcpv6_record;
ULONG       time_elapsed;

/* Obtain time (timer ticks) elapsed from independent time keeper. */
time_elapsed = /* to be determined by application */ 1000; 

/* Obtain a record of the current client state. */
status=  nx_dhcpv6_client_restore_record(&dhcpv6_ptr, &dhcpv6_record, time_elapsed);

/* If status is NX_SUCCESS the current DHCPv6 Client pointed to by dhcpv6_ptr contains the current client record updated for time elapsed during power down. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_dhcpv6_client_get_record