---
title: Ek A-Azure RTOS NetX Duo DHCP Istemci Hizmetleri için geri yükleme durumu özelliğinin açıklaması
description: Bu bölümde, Azure RTOS NetX Duo DHCP Istemci Hizmetleri için geri yükleme durumu özelliğinin bir açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 008ca6fb0052339e188e0240cc38a81d3a6b40e8
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826146"
---
# <a name="appendix-a--description-of-the-restore-state-feature-for-azure-rtos-netx-duo-dhcp-client-services"></a>Ek A: Azure RTOS NetX Duo DHCP Istemci Hizmetleri için geri yükleme durumu özelliğinin açıklaması

NetX Duo DHDP Istemci yapılandırma seçeneği, NX_DHCP_CLIENT_RESTORE_STATE, sistemin önceden oluşturulmuş bir DHCP Istemci kaydını sistem yeniden başlatmalar arasında bağlantılı bir durumda geri yüklemesine olanak tanır.

Bu seçenek etkinleştirildiğinde, uygulama DHCP Istemci iş parçacığını askıya alabilir ve sürdürebilir. DHCP Istemcisini, iş parçacığını askıya alma ve sürdürme arasındaki geçen süre ile güncelleştirmek için de bir hizmet vardır.

## <a name="restoring-the-dhcp-client-between-reboots"></a>Yeniden başlatmalar arasında DHCP Istemcisini geri yükleme

Yeniden başlatmadan sonra bir DHCP Istemcisini geri yüklemeden önce, daha önce oluşturulmuş bir DHCP Istemcisi, bağlantılı duruma ulaşmalıdır ve DHCP sunucusundan bir IP adresi atanır. Kapatmadan önce, DHCP uygulamasının geçerli DHCP Istemci kaydını geçici olmayan belleğe kaydetmesi gerekir. Bu güç durumu sırasında geçen süreyi izlemek için, sistemde başka bir yerde bağımsız bir ' Time Man ' olması gerekir. Uygulama, yeni bir DHCP Istemci örneği oluşturur ve daha önce oluşturulan DHCP Istemci kaydıyla günceller. Geçen süre, "zaman Man" kaynağından alınır ve DHCP Istemcisi kiralamasında kalan zamana uygulanır. Bu, DHCP Istemcisinin, örneğin, yenıleme göre, durumları değiştirmesine neden olabileceğini unutmayın. Bu noktada, uygulama DHCP Istemcisini sürdürür.

Güç kapatma sırasında geçen süre DHCP Istemci durumunu yenıleme ya da yeniden bağlama durumuna geçirir, DHCP Istemcisi IP adresi kiralamasını yenilemek veya yeniden bağlamak isteyen DHCP iletilerini otomatik olarak başlatır. IP adresinin geçerliliği dolmuşsa, DHCP Istemcisi IP örneğindeki IP adresini otomatik olarak temizler ve yeni bir IP adresi isteyen başlangıç durumundan DHCP işlemine başlar.

Bu şekilde, DHCP Istemcisi kesintisiz olarak yeniden başlatmalar arasında çalışabilir.

Bu özelliğin bir çizimi aşağıda verilmiştir. Bu, DHCP Istemcisinin yalnızca birincil arabirimde çalıştığını varsayar.

```c
/* On the power up, create an IP instance, DHCP Client, enable ICMP and UDP
   and other resources (not shown) for the DHCP Client/application
   in tx_application_define().  */
 
/* Define the DHCP application thread. */     
void    thread_dhcp_client_entry(ULONG thread_input)
{

UINT        status;
UINT        time_elapsed = 0;
NX_DHCP_CLIENT_RECORD client_nv_record;


if (/* The application checks if there is a previously saved DHCP Client record. */)
{
    /* No previously saved Client record. Start the DHCP Client in the INIT state.  */
    status =  nx_dhcp_start(&dhcp_0);

    if (status !=NX_SUCCESS)
        return;

    do
    {
        /* Wait for DHCP to assign the IP address.  */
    } while (status != NX_SUCCESS);

    /* We have a valid IP address. */
    /* At some point decide we power down the system. */
    /* Save the Client state data which we will subsequently need to restore the DHCP    
       Client. */
    status = nx_dhcp_client_get_record(&dhcp_0, &client_nv_record);               

    /* Copy this memory to non-volatile memory (not shown). */
    /* Delete the IP and DHCP Client instances before powering down. */
    nx_dhcp_delete(&dhcp_0);

    nx_ip_delete(&ip_0);
    /* Ready to power down, having released other resources as necessary. */

}
else
{

    /* The application has determined there is a previously saved record. We will 
        restore it to the current DHCP Client instance.  */

    /* Get the previous Client state data from non-volatile memory. */

    /* Apply the record to the current Client instance. This will also 
        update the IP instance with IP address, mask etc. */
    status = nx_dhcp_client_restore_record(&dhcp_0, &client_nv_record, time_elapsed);   

    if (status != NX_SUCCESS)
        return;

    /* We are ready to resume the DHCP Client thread and use the assigned IP address. */
    status = nx_dhcp_resume(&dhcp_0);

    if (status != NX_SUCCESS)
        return;

}
```
## <a name="resuming-the-dhcp-client-thread-after-suspension"></a>Askıya alındıktan sonra DHCP Istemci Iş parçacığı sürdürülüyor 

Uygulamayı kapatmadan bir DHCP Istemci iş parçacığını askıya almak için, uygulama, bağlı durumu elde eden ve geçerli bir IP adresine sahip olan bir DHCP Istemcisinde *nx_dhcp_suspend* çağırır. DHCP Istemcisini sürdürmeye hazırlanıyorsa, ilk olarak DHCP adresi kiralamasında kalan süreyi (bağımsız bir saatten geçen süreyi elde) güncelleştirmek için *nx_dhcp_client_update_time_remaining* çağırır. Ardından, DHCP Istemci iş parçacığını sürdürmesini sağlamak için *nx_dhcp_resume* çağırır.

Geçen süre DHCP Istemci durumunu yenıleme veya yeniden bağlama durumuna geçirir, DHCP Istemcisi IP adresi kiralamasını yenilemek veya yeniden bağlamak isteyen DHCP iletilerini otomatik olarak başlatır. IP adresinin geçerliliği dolmuşsa, DHCP Istemcisi IP adresini otomatik olarak temizler ve yeni bir IP adresi isteyen başlangıç durumundan DHCP işlemine başlar.

Bu özelliğin kullanımına ilişkin bir çizim aşağıda verilmiştir.

```c
/* Create an IP instance, DHCP Client, enable ICMP and UDP
   and other resources (not shown) typically in tx_application_define().  */
 
/* Define the DHCP application thread. */     
void    thread_dhcp_client_entry(ULONG thread_input)
{

  /* Start the DHCP Client.  */
  status =  nx_dhcp_start(&dhcp_0);

  if (status !=NX_SUCCESS)
    return;

  while(1)
  {
   /* Wait for DHCP to obtain an IP address.  */
  }

  /* Do tasks with the IP address e.g. send pings to another host on the network...  */
  status =  nx_icmp_ping(…);

  if (status !=NX_SUCCESS)
          printf("Failed %d byte Ping!\n", length);

  /* At some later time, suspend the DHCP Client e.g. the device is going to low 
   power mode (sleep) so we do not want any threads to wake it up. */

  nx_dhcp_suspend(&dhcp_0);  

  /* During this suspended state, an independent timer is keeping track of the elapsed      
     time. */


  /* At some point, we are ready to resume the DHCP Client thread. */

  /* Update the DHCP Client lease time remaining with the time elapsed. */
  status = nx_dhcp_client_update_time_remaining(&dhcp_0, time_elapsed);   

  if (status != NX_SUCCESS)
       return;

  /* We now can resume the DHCP Client thread. */
  status = nx_dhcp_resume(&dhcp_0);

  if (status != NX_SUCCESS)
       return;

  /* Resume tasks e.g. ping another host. */
  status =  nx_icmp_ping(…);

}

```
Aşağıda, bir DHCP Istemci durumunun bellekten geri yüklenmesi ve DHCP Istemcisini askıya almak ve sürdürmek için hizmetlerin bir listesi verilmiştir.

## <a name="nx_dhcp_client_get_record"></a>nx_dhcp_client_get_record

Geçerli DHCP Istemci durumunun bir kaydını oluştur

### <a name="prototype"></a>Prototype

```c
ULONG nx_dhcp_ client_get_record(NX_DHCP *dhcp_ptr, NX_DHCP_CLIENT_RECORD *record_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, DHCP Istemci örneğinde bulunan DHCP için etkinleştirilen ilk arabirimde çalışan DHCP Istemcisini, record_ptr tarafından işaret edilen kayda kaydeder. Bu, DHCP Istemci uygulamasının DHCP Istemci durumunu, örneğin bir güç kapatma ve yeniden başlatma gibi geri yüklemesine olanak tanır.

DHCP için birden fazla arabirim etkinleştirilmişse, belirli bir arabirimdeki DHCP Istemci kaydını kaydetmek için *nx_dhcp_interface_client_get_record* hizmetini kullanın.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr**: DHCP istemcisi işaretçisi
- **record_ptr**: DHCP istemci kaydına yönelik işaretçi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS (0x0)**: istemci kaydı oluşturuldu
- **NX_DHCP_NOT_BOUND**: (0x94) Istemci, bağlantılı durumlarda değil
- **NX_DHCP_NO_INTERFACES_ENABLED**: (0xa5) DHCP için etkinleştirilen arabirim yok
- NX_PTR_ERROR: (0x16) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
NX_DHCP_CLIENT_RECORD dhcp_record;

/* Obtain a record of the current client state. */
status=  nx_dhcp_client_get_record(dhcp_ptr, &dhcp_record);

/* If status is NX_SUCCESS dhcp_record contains the current DHCP client record. */
```

## <a name="nx_dhcp_interface_client_get_record"></a>nx_dhcp_interface_client_get_record

Belirtilen arabirimdeki geçerli DHCP Istemci durumunun bir kaydını oluştur

### <a name="prototype"></a>Prototype

```c
ULONG nx_dhcp_interface_client_get_record(NX_DHCP *dhcp_ptr, UINT interface_index,
                                          NX_DHCP_CLIENT_RECORD *record_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen arabirimde çalışan DHCP Istemcisini record_ptr tarafından işaret edilen kayda kaydeder. Bu, DHCP Istemci uygulamasının DHCP Istemci durumunu, örneğin bir güç kapatma ve yeniden başlatma gibi geri yüklemesine olanak tanır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr**: DHCP istemcisi işaretçisi
- **interface_index**: kaydın alınacağı dizin
- **record_ptr**: DHCP istemci kaydına yönelik işaretçi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS (0x0)**: istemci kaydı oluşturuldu
- **NX_DHCP_NOT_BOUND**: (0x94) **istemci, bağlantılı durumda değil**
- **NX_DHCP_BAD_INTERFACE_INDEX_ERROR**: (0X9a) geçersiz arabirim dizini
- NX_PTR_ERROR: (0x16) geçersiz DHCP işaretçisi.
- NX_INVALID_INTERFACE: (0x4C) geçersiz ağ arabirimi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
NX_DHCP_CLIENT_RECORD dhcp_record;
/* Obtain a record of the current client state on interface 1. */
status=  nx_dhcp_interface_client_get_record(dhcp_ptr, 1, &dhcp_record);

/* If status is NX_SUCCESS dhcp_record contains the current DHCP client record. */
```

## <a name="nx_dhcp_-client_restore_record"></a>nx_dhcp_ client_restore_record

DHCP Istemcisini daha önce kaydedilen bir kayıttan geri yükleme

### <a name="prototype"></a>Prototype

```c
ULONG nx_dhcp_client_restore_record(NX_DHCP *dhcp_ptr, 
                                    NX_DHCP_CLIENT_RECORD *record_ptr, 
                                    ULONG time_elapsed);

```

### <a name="description"></a>Açıklama

Bu hizmet, bir uygulamanın DHCP istemcisini record_ptr tarafından işaret edilen DHCP Istemci kaydını kullanarak önceki bir oturumdan geri yüklemesine olanak sağlar. Time_elapsed girişi, DHCP Istemci kirası üzerinde kalan zamana uygulanır.

Bu, DHCP Istemci uygulamasının kapatmadan önce DHCP Istemcisinin bir kaydını oluşturulmasını ve bu kaydı kalıcı belleğe kaydetmesidir.

DHCP Istemcisi için birden fazla arabirim etkinse, bu hizmet DHCP Istemci örneğinde bulunan ilk geçerli arabirime uygulanır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr**: DHCP istemcisi işaretçisi
- **record_ptr**: DHCP istemci kaydına yönelik işaretçi 
- **time_elapsed**: giriş istemci kaydında kalan kira zamanından çıkartılacak süre

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x0) istemci kaydı geri yüklendi
- **NX_DHCP_NO_INTERFACES_ENABLED**: (0xa5) DHCP çalıştıran arabirim yok
- NX_PTR_ERROR: (0x16) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
NX_DHCP_CLIENT_RECORD dhcp_record;
ULONG       time_elapsed;

/* Obtain time (timer ticks) elapsed from independent time keeper. */
Time_elapsed = /* to be determined by application */ 1000; 

/* Obtain a record of the current client state. */
status=  nx_dhcp_client_restore_record(client_ptr, &dhcp_record, time_elapsed);

/* If status is NX_SUCCESS the current DHCP Client pointed to by dhcp_ptr  contains the current client record updated for time elapsed during power down. */
```

## <a name="nx_dhcp_interace_client_restore_record"></a>nx_dhcp_interace_client_restore_record

DHCP Istemcisini belirtilen arabirimdeki daha önce kaydedilmiş bir kayıttan geri yükle

### <a name="prototype"></a>Prototype

```c
ULONG nx_dhcp_interface_client_restore_record(NX_DHCP *dhcp_ptr, 
                                              NX_DHCP_CLIENT_RECORD *record_ptr, 
                                              ULONG time_elapsed);
```

### <a name="description"></a>Açıklama

Bu hizmet, bir uygulamanın DHCP istemcisini, record_ptr tarafından işaret edilen DHCP Istemci kaydını kullanarak belirtilen arabirime geri yüklemesine olanak sağlar. Time_elapsed girişi, DHCP Istemci kirası üzerinde kalan zamana uygulanır.

Bu, DHCP Istemci uygulamasının kapatmadan önce DHCP Istemcisinin bir kaydını oluşturulmasını ve bu kaydı kalıcı belleğe kaydetmesidir.

DHCP Istemcisi için birden fazla arabirim etkinse, bu hizmet DHCP Istemci örneğinde bulunan ilk geçerli arabirime uygulanır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr**: DHCP istemcisi işaretçisi
- **record_ptr**: DHCP istemci kaydına yönelik işaretçi 
- **time_elapsed**: giriş istemci kaydında kalan kira zamanından çıkartılacak süre

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x0) istemci kaydı geri yüklendi
- **NX_DHCP_NOT_BOUND**: (0x94) istemci IP adresine bağlanmadı
- **NX_DHCP_BAD_INTERFACE_INDEX_ERROR**: (0X9a) geçersiz arabirim dizini
- NX_PTR_ERROR: (0x16) geçersiz DHCP işaretçisi.
- NX_INVALID_INTERFACE: (0x4C) geçersiz ağ arabirimi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
NX_DHCP_CLIENT_RECORD dhcp_record;
ULONG       time_elapsed;

/* Obtain time (timer ticks) elapsed from independent time keeper. */
Time_elapsed = /* to be determined by application */ 1000; 


/* Obtain a record of the current client state on the primary interface. */
status=  nx_dhcp_interface_client_restore_record(client_ptr, 0, &dhcp_record, time_elapsed);

/* If status is NX_SUCCESS the current DHCP Client pointed to by dhcp_ptr  contains the current client record updated for time elapsed during power down. */
```

## <a name="nx_dhcp_-client_update_time_remaining"></a>nx_dhcp_ client_update_time_remaining

DHCP Istemcisi kiralamasında kalan süreyi Güncelleştir

### <a name="prototype"></a>Prototype

```c
ULONG nx_dhcp_client_update_time_remaining(NX_DHCP *dhcp_ptr, ULONG time_elapsed);
```

### <a name="description"></a>Açıklama

Bu hizmet DHCP istemci IP adresi kirası üzerinde kalan süreyi, DHCP Istemci örneğinde bulunan DHCP için etkinleştirilen ilk arabirimdeki time_elapsed girişi ile güncelleştirir. Uygulama, *nx_dhcp_suspend* kullanarak bu hizmeti kullanmadan önce DHCP istemci iş parçacığını askıya almalıdır. Bu hizmet çağrıldıktan sonra uygulama, *nx_dhcp_resume* çağırarak DHCP istemci iş parçacığını sürdürür.

Bu, DHCP Istemci iş parçacığını bir süre için askıya almanız gereken DHCP Istemci uygulamalarına yöneliktir ve kalan IP adresi kiralama süresini güncelleştirir.

Not: Bu hizmet, daha önce açıklanan *nx_dhcp_client_get_record* ve *nx_dhcp_client_restore_record* birlikte kullanılmak üzere tasarlanmamıştır. Bu hizmetler daha önce bu bölümde açıklanmıştır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr**: DHCP istemcisi işaretçisi 
- **time_elapsed**: IP adresi kirası üzerinde kalan süreden çıkartılacak süre

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x0) istemci IP kirası güncelleştirildi
- **NX_DHCP_NO_INTERFACES_ENABLED**: (0xa5) DHCP için etkinleştirilen arabirim yok
- NX_PTR_ERROR: (0x16) geçersiz Işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
ULONG       time_elapsed;

/* Obtain time (timer ticks) elapsed from independent time keeper. */
time_elapsed = /* to be determined by application */ 1000; 


/* Apply the elapsed time to the DHCP Client address lease. */
status=  nx_dhcp_client_update_time_remaining(client_ptr, time_elapsed);

/* If status is NX_SUCCESS the DHCP Client is updated for time elapsed. */
```

## <a name="nx_dhcp_interface_client_update_time_remaining"></a>nx_dhcp_interface_client_update_time_remaining

Belirtilen arabirimdeki DHCP Istemcisi kiralamasında kalan süreyi Güncelleştir

### <a name="prototype"></a>Prototype

```c
ULONG nx_dhcp_interface_client_update_time_remaining(NX_DHCP *dhcp_ptr,
                                                     UINT interface_index,
                                                     ULONG time_elapsed);
```

### <a name="description"></a>Açıklama

Bu hizmet DHCP Istemci IP adresi kiralamasında kalan süreyi, bu arabirim DHCP için etkinleştirildiğinde belirtilen arabirimdeki time_elapsed girişi ile güncelleştirir. Uygulama, *nx_dhcp_suspend* kullanarak bu hizmeti kullanmadan önce DHCP istemci iş parçacığını askıya almalıdır. Bu hizmet çağrıldıktan sonra uygulama, *nx_dhcp_resume* çağırarak DHCP istemci iş parçacığını sürdürür. Bkz. DHCP Istemci iş parçacığını askıya alma ve sürdürme, DHCP için etkinleştirilen tüm arabirimler için geçerlidir.

Bu, DHCP Istemci iş parçacığını bir süre için askıya almanız gereken DHCP Istemci uygulamalarına yöneliktir ve kalan IP adresi kiralama süresini güncelleştirir.

Not: Bu hizmet, daha önce açıklanan *nx_dhcp_client_get_record* ve *nx_dhcp_client_restore_record* birlikte kullanılmak üzere tasarlanmamıştır. Bu hizmetler daha önce bu bölümde açıklanmıştır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr**: DHCP istemcisi işaretçisi
- **interface_index**: geçen sürenin uygulanacağı arabirime olan Dizin
- **time_elapsed**: IP adresi kirası üzerinde kalan süreden çıkartılacak süre

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x0) istemci IP kirası güncelleştirildi
- **NX_DHCP_BAD_INTERFACE_INDEX_ERROR**: (0X9a) geçersiz arabirim dizini
- NX_PTR_ERROR: (0x16) geçersiz DHCP işaretçisi.
- NX_INVALID_INTERFACE: (0x4C) geçersiz ağ arabirimi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
ULONG       time_elapsed;

/* Obtain time (timer ticks) elapsed from independent time keeper. */
time_elapsed = /* to be determined by application */ 1000; 


/* Apply the elapsed time to the DHCP Client address lease on interface 1. */
status=  nx_dhcp_interface_client_update_time_remaining(client_ptr, 1, time_elapsed);

/* If status is NX_SUCCESS the DHCP Client is updated for time elapsed. */

```

## <a name="nx_dhcp_suspend"></a>nx_dhcp_suspend

DHCP Istemci iş parçacığını askıya alma

### <a name="prototype"></a>Prototype

```c
ULONG nx_dhcp_suspend(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, geçerli DHCP Istemci iş parçacığını askıya alır. *Nx_dhcp_stop* farklı olarak, bu HIZMET çağrıldığında DHCP istemci durumunda hiçbir değişiklik olmadığını unutmayın.

Bu hizmet, DHCP için etkinleştirilen tüm arabirimlerde çalışan DHCP 'yi askıya alır.

DHCP Istemcisi askıya alındığında DHCP Istemci durumunu geçen süre ile güncelleştirmek için, daha önce açıklanan *nx_dhcp_client_update_time_remaining* bakın. Askıya alınmış bir DHCP Istemci iş parçacığını sürdürmesini sağlamak için uygulama *nx_dhcp_resume* çağırmalıdır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr**: DHCP istemcisi işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x0) istemci iş parçacığı askıya alındı
- NX_PTR_ERROR: (0x16) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Pause the DHCP client thread. */
status=  nx_dhcp_suspend(client_ptr);

/* If status is NX_SUCCESS the current DHCP Client thread is paused. */
```

## <a name="nx_dhcp_resume"></a>nx_dhcp_resume

Askıya alınmış bir DHCP Istemci iş parçacığını sürdürür

### <a name="prototype"></a>Prototype

```c
ULONG nx_dhcp_resume(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, askıya alınmış bir DHCP Istemci iş parçacığını sürdürür. Istemci iş parçacığına devam ettikten sonra gerçek DHCP Istemci durumunda değişiklik olmadığını unutmayın. DHCP Istemci IP adresi kiralamasında kalan süreyi, *nx_dhcp_resume* çağrılmadan önce geçen süre ile güncelleştirmek için, daha önce açıklanan *nx_dhcp_client_update_time_remaining* bakın.

Bu hizmet, DHCP için etkinleştirilen tüm arabirimlerde çalışan DHCP 'yi sürdürür.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr**: DHCP istemcisi işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x0) istemci iş parçacığı sürdürülüyor
- NX_PTR_ERROR: (0x16) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Resume the DHCP client thread. */
status=  nx_dhcp_resume(client_ptr);

/* If status is NX_SUCCESS the current DHCP Client thread is resumed. */
```