---
title: Ek A - Geri Yükleme Durumu Özelliğinin Açıklaması
description: NetX DHDP Azure RTOS yapılandırma seçeneği olan NX_DHCP_CLIENT_RESTORE_STATE, sistemin sistem yeniden başlatmaları arasında daha önce oluşturulmuş bir DHCP İstemci Kaydını Bağlı durumda geri yüklemesini sağlar.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 4b7286726eb6bfc666ba7a4b9983847da442fe212a45f4b28e184f70cf46e2b4
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116801249"
---
# <a name="appendix-a---description-of-the-restore-state-feature"></a>Ek A - Geri Yükleme Durumu Özelliğinin Açıklaması

NetX DHDP Azure RTOS yapılandırma seçeneği olan NX_DHCP_CLIENT_RESTORE_STATE, sistemin sistem yeniden başlatmaları arasında daha önce oluşturulmuş bir DHCP İstemci Kaydını Bağlı durumda geri yüklemesini sağlar.

Bu seçenek etkinleştirildiğinde, uygulama DHCP İstemcisi iş parçacığını askıya alabilir ve sürdürebilir. Ayrıca, DHCP İstemcisi'nin iş parçacığını askıya alma ve devam etme arasında geçen süreyle güncelleştirilen bir hizmet de vardır.

## <a name="restoring-the-dhcp-client-between-reboots"></a>Dhcp İstemcisini Yeniden Başlatmalar Arasında Geri Yükleme

Yeniden başlatıldıktan sonra BIR DHCP İstemcisini geri yüklemeden önce, Daha önce oluşturulmuş, Bağlı durumuna ulaşacak ve DHCP sunucusundan bir IP adresi atanacak bir DHCP İstemcisi. Çalışmadan önce, DHCP uygulamasının geçerli DHCP İstemcisi kaydını geçici olmayan belleğe kaydetmesi gerekir. Ayrıca, sistemin başka bir yerinde, bu güç kapatıldı durumu sırasında geçen zamanı takip etmek için bağımsız bir 'zaman tutma' da olması gerekir. Uygulama, güç sağlarken yeni bir DHCP İstemcisi örneği oluşturur ve ardından daha önce oluşturulan DHCP İstemcisi kaydıyla bunu günceller. Geçen süre "zaman ayırıcıdan" elde edilir ve ardından DHCP İstemci kirası üzerinde kalan süreye uygulanır. Bu durum DHCP İstemcisi'nin durumlarını (örneğin, BAĞLANTIDAN YenİLEME'ye) değiştirmesini neden olabilir. Bu noktada, uygulama DHCP İstemcisini sürdürebilir.

Güç kesintisi sırasında geçen süre DHCP İstemcisi durumunu YenİLE veya YenİLE durumuna koyarsa, DHCP İstemcisi IP adresi kiralamasını yenilemek veya yeniden başlatmak için istekte bulunduran DHCP iletilerini otomatik olarak başlatacaktır. IP adresinin süresi dolduğunda, DHCP İstemcisi IP örneğinde IP adresini otomatik olarak temizler ve INIT durumdan DHCP işlemini başlatarak yeni bir IP adresi talep eder.

Bu şekilde DHCP İstemcisi, yeniden başlatmalar arasında kesintisiz olarak çalışır.

Bu özelliğin bir çizimi aşağıda verilmiştir. Bu, DHCP İstemcisi'nin yalnızca birincil arabirimde çalıştırılı olduğunu varsayıyor.

```C
/* On the power up, create an IP instance, DHCP Client, enable ICMP and UDP
   and other resources (not shown) for the DHCP Client/application
   in tx_application_define(). */
 
/* Define the DHCP application thread. */     
void    thread_dhcp_client_entry(ULONG thread_input)
{

UINT        status;
UINT        time_elapsed = 0;
NX_DHCP_CLIENT_RECORD client_nv_record;


if (/* The application checks if there is a previously saved DHCP Client record. */)
{


  /* No previously saved Client record. Start the DHCP Client in the INIT state. */
  status =  nx_dhcp_start(&dhcp_0);

  if (status !=NX_SUCCESS)
    return;

  do
  {
  
    /* Wait for DHCP to assign the IP address. */
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
     restore it to the current DHCP Client instance. */

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

## <a name="resuming-the-dhcp-client-thread-after-suspension"></a>Askıya Alındıktan Sonra DHCP İstemci İş Parçacığını Devam Ediyor 

Bir DHCP İstemcisi iş parçacığını kapatmadan  askıya almak için uygulama, NX_DHCP_SUSPEND durumuna ulaşan ve geçerli bir IP adresine sahip olan DHCP İstemcisi'ne çağrır. DHCP İstemcisini sürdürmeye hazır olduğunda, önce DHCP *nx_dhcp_client_update_time_remaining* kiralamada kalan zamanı (bağımsız bir zaman ayırıcıdan geçen süre) güncelleştirmek için nx_dhcp_client_update_time_remaining'yi arar. Ardından DHCP İstemcisi *nx_dhcp_resume* devam etmek için ağ sunucusunu arar.

Geçen süre DHCP İstemcisi durumunu YenİLE veya YenİLE durumuna koyarsa, DHCP İstemcisi IP adresi kiralamasını yenilemek veya yeniden başlatmak için istekte bulundurarak DHCP iletilerini otomatik olarak başlatacaktır. IP adresinin süresi dolduğunda, DHCP İstemcisi IP adresini otomatik olarak temizler ve INIT durumdan DHCP işlemini başlatarak yeni bir IP adresi talep eder.

Bu özelliğin kullanımı aşağıdaki çizimde verilmiştir.

```C
/* Create an IP instance, DHCP Client, enable ICMP and UDP
   and other resources (not shown) typically in tx_application_define(). */
 
/* Define the DHCP application thread. */     
void    thread_dhcp_client_entry(ULONG thread_input)
{

  /* Start the DHCP Client. */
  status =  nx_dhcp_start(&dhcp_0);

  if (status !=NX_SUCCESS)
    return;

  while(1)
  {
   
    /* Wait for DHCP to obtain an IP address. */
  }

  /* Do tasks with the IP address e.g. send pings to another host on the 
     network... */
  status =  nx_icmp_ping(…);

  if (status !=NX_SUCCESS)
          printf("Failed %d byte Ping!\n", length);

  /* At some later time, suspend the DHCP Client e.g. the device is going to low 
   power mode (sleep) so we do not want any threads to wake it up. */

  nx_dhcp_suspend(&dhcp_0);  

  /* During this suspended state, an independent timer is keeping track of the
     elapsed time. */


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

Aşağıda, bir DHCP İstemcisi durumunu bellekten geri yükleme ve DHCP İstemcisini askıya alma ve devam etme için hizmetlerin listesi verilmiştir.

## <a name="nx_dhcp_client_get_record"></a>nx_dhcp_client_get_record

Geçerli DHCP İstemcisi durumunun kaydını oluşturma

### <a name="prototype"></a>Prototype

```C
ULONG nx_dhcp_ client_get_record(NX_DHCP *dhcp_ptr, 
                                 NX_DHCP_CLIENT_RECORD *record_ptr);
```

### <a name="description"></a>Description

Bu hizmet, DHCP İstemcisi örneğinde bulunan DHCP için etkinleştirilen ilk arabirimde çalışan DHCP İstemcisini, dhcp istemcisinin record_ptr. Bu, DHCP İstemcisi uygulamasının, örneğin bir güç kesintisi ve yeniden başlatma sonrasında DHCP İstemcisi durumunu geri yüklemesini sağlar.

DHCP için birden fazla arabirim etkinleştirilmişse belirli bir arabirimde DHCP İstemcisi kaydını kaydetmek için, dhcp *nx_dhcp_interface_client_get_record* kullanın.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr** DHCP İstemcisi İşaretçisi

- **record_ptr** DHCP İstemcisi kaydının işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x0) İstemci kaydı oluşturuldu

- **NX_DHCP_NOT_BOUND** (0x94) İstemci Bağlı durumda değil

- **NX_DHCP_NO_INTERFACES_ENABLED** (0xA5) DHCP için etkinleştirilmiş arabirim yok

- **NX_PTR_ERROR** (0x16) Geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
NX_DHCP_CLIENT_RECORD dhcp_record;


/* Obtain a record of the current client state. */
status=  nx_dhcp_client_get_record(dhcp_ptr, &dhcp_record);

/* If status is NX_SUCCESS dhcp_record contains the current DHCP client record. */
```

## <a name="nx_dhcp_interface_client_get_record"></a>nx_dhcp_interface_client_get_record

Belirtilen arabirimde geçerli DHCP İstemcisi durumunun kaydını oluşturma

### <a name="prototype"></a>Prototype

```C
ULONG nx_dhcp_interface_client_get_record(NX_DHCP *dhcp_ptr, 
                                 UINT interface_index,
                                 NX_DHCP_CLIENT_RECORD *record_ptr);
```
### <a name="description"></a>Description

Bu hizmet, belirtilen arabirimde çalışan DHCP İstemcisini, belirtilen arabirimde çalışan DHCP İstemcisi'nin record_ptr. Bu, DHCP İstemcisi uygulamasının, örneğin bir güç kesintisi ve yeniden başlatma sonrasında DHCP İstemcisi durumunu geri yüklemesini sağlar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr** DHCP İstemcisi İşaretçisi

- **interface_index** Kayıt almak için dizin

- **record_ptr** DHCP İstemcisi kaydının işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x0) İstemci kaydı oluşturuldu

- **NX_DHCP_NOT_BOUND** (0x94) İstemci Bağlı durumda değil

- **NX_DHCP_BAD_INTERFACE_INDEX_ERROR** (0x9A) Geçersiz arabirim dizini

- NX_PTR_ERROR (0x16) Geçersiz DHCP işaretçisi.

- NX_INVALID_INTERFACE (0x4C) Geçersiz ağ arabirimi

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
NX_DHCP_CLIENT_RECORD dhcp_record;


/* Obtain a record of the current client state on interface 1. */
status=  nx_dhcp_interface_client_get_record(dhcp_ptr, 1, &dhcp_record);

/* If status is NX_SUCCESS dhcp_record contains the current DHCP client record. */
```

## <a name="nx_dhcp_-client_restore_record"></a>nx_dhcp_ client_restore_record

Daha önce kaydedilen bir kayıttan DHCP İstemcisini geri yükleme

### <a name="prototype"></a>Prototype

```C
ULONG nx_dhcp_client_restore_record(NX_DHCP *dhcp_ptr, 
                                    NX_DHCP_CLIENT_RECORD       
                                    *record_ptr, ULONG time_elapsed);
```
### <a name="description"></a>Description

Bu hizmet, bir uygulamanın dhcp istemcisi tarafından işaret ettiği DHCP İstemcisi kaydını kullanarak önceki bir oturumdan DHCP İstemcisini geri yüklemesini record_ptr. Bu time_elapsed, DHCP İstemci kiralamada kalan süreye uygulanır.

Bu, DHCP İstemcisi uygulamasının, kapatılana kadar DHCP İstemcisi'nin bir kaydını oluşturmasını ve bu kaydı uzun olmayan belleğe kaydetmesini gerektirir.

DHCP İstemcisi için birden fazla arabirim etkinse, bu hizmet DHCP İstemcisi örneğinde bulunan ilk geçerli arabirime uygulanır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr** DHCP İstemcisi İşaretçisi

- **record_ptr** DHCP İstemcisi kaydının işaretçisi

- **time_elapsed** Giriş istemci kaydında kalan kira süresinden çıkarma süresi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x0) İstemci kaydı geri yüklendi

- **NX_DHCP_NO_INTERFACES_ENABLED** (0xA5) DHCP çalıştıran arabirim yok

- **NX_PTR_ERROR** (0x16) Geçersiz işaretçi Girişi

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek
```C
NX_DHCP_CLIENT_RECORD dhcp_record;
ULONG       time_elapsed;

/* Obtain time (timer ticks) elapsed from independent time keeper. */
Time_elapsed = /* to be determined by application */ 1000; 


/* Obtain a record of the current client state. */
status=  nx_dhcp_client_restore_record(client_ptr, &dhcp_record, time_elapsed);

/* If status is NX_SUCCESS the current DHCP Client pointed to by dhcp_ptr
   contains the current client record updated for time elapsed during power down. */
```

## <a name="nx_dhcp_interace_client_restore_record"></a>nx_dhcp_interace_client_restore_record

Belirtilen arabirimde daha önce kaydedilmiş bir kayıttan DHCP İstemcisini geri yükleme

### <a name="prototype"></a>Prototype

```C
ULONG nx_dhcp_interface_client_restore_record(NX_DHCP *dhcp_ptr, 
                                              NX_DHCP_CLIENT_RECORD       
                                              *record_ptr, ULONG time_elapsed);
```
### <a name="description"></a>Description

Bu hizmet, uygulamanın dhcp istemcisi tarafından işaret ettiği DHCP İstemcisi kaydını kullanarak belirtilen arabirimde DHCP İstemcisini geri yüklemesini record_ptr. Bu time_elapsed, DHCP İstemci kiralamada kalan süreye uygulanır.

Bu, DHCP İstemcisi uygulamasının, kapatılana kadar DHCP İstemcisi'nin bir kaydını oluşturmasını ve bu kaydı uzun olmayan belleğe kaydetmesini gerektirir.

DHCP İstemcisi için birden fazla arabirim etkinse, bu hizmet DHCP İstemcisi örneğinde bulunan ilk geçerli arabirime uygulanır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr** DHCP İstemcisi İşaretçisi

- **record_ptr** DHCP İstemcisi kaydının işaretçisi

- **time_elapsed** Giriş istemci kaydında kalan kira süresinden çıkarma süresi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x0) İstemci kaydı geri yüklendi

- **NX_DHCP_NOT_BOUND** (0x94) İstemciSI IP adresine bağlı değil

- **NX_DHCP_BAD_INTERFACE_INDEX_ERROR** (0x9A) Geçersiz arabirim dizini

- NX_PTR_ERROR (0x16) Geçersiz DHCP işaretçisi.

- NX_INVALID_INTERFACE (0x4C) geçersiz ağ arabirimi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
NX_DHCP_CLIENT_RECORD dhcp_record;
ULONG       time_elapsed;

/* Obtain time (timer ticks) elapsed from independent time keeper. */
Time_elapsed = /* to be determined by application */ 1000; 


/* Obtain a record of the current client state on the primary interface. */
status=  nx_dhcp_interface_client_restore_record(client_ptr, 0, &dhcp_record, time_elapsed);

/* If status is NX_SUCCESS the current DHCP Client pointed to by dhcp_ptr  
   contains the current client record updated for time elapsed during power down. */
```

## <a name="nx_dhcp_-client_update_time_remaining"></a>nx_dhcp_ client_update_time_remaining

DHCP Istemcisi kiralamasında kalan süreyi Güncelleştir

### <a name="prototype"></a>Prototype

```C
ULONG nx_dhcp_client_update_time_remaining(NX_DHCP *dhcp_ptr
                                           ULONG time_elapsed);
```
### <a name="description"></a>Description

Bu hizmet DHCP istemci IP adresi kirası üzerinde kalan süreyi, DHCP Istemci örneğinde bulunan DHCP için etkinleştirilen ilk arabirimdeki time_elapsed girişi ile güncelleştirir. Uygulama, *nx_dhcp_suspend* kullanarak bu hizmeti kullanmadan önce DHCP istemci iş parçacığını askıya almalıdır. Bu hizmet çağrıldıktan sonra uygulama, *nx_dhcp_resume* çağırarak DHCP istemci iş parçacığını sürdürür.

Bu, DHCP Istemci iş parçacığını bir süre için askıya almanız gereken DHCP Istemci uygulamalarına yöneliktir ve kalan IP adresi kiralama süresini güncelleştirir.

> [!NOTE]
> Bu hizmet, daha önce açıklanan *nx_dhcp_client_get_record* ve *nx_dhcp_client_restore_record* birlikte kullanılmak üzere tasarlanmamıştır. Bu hizmetler daha önce bu bölümde açıklanmıştır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr** DHCP Istemcisi işaretçisi

- **time_elapsed** IP adresi kirası üzerinde kalan süreden çıkarma süresi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x0) istemci IP kirası güncelleştirildi

- **NX_DHCP_NO_INTERFACES_ENABLED** (0xa5) DHCP için etkinleştirilen arabirim yok

- **NX_PTR_ERROR** (0x16) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
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

```C
ULONG nx_dhcp_interface_client_update_time_remaining(NX_DHCP *dhcp_ptr,
                                                     UINT interface_index,
                                                     ULONG time_elapsed);
```
### <a name="description"></a>Description

Bu hizmet DHCP Istemci IP adresi kiralamasında kalan süreyi, bu arabirim DHCP için etkinleştirildiğinde belirtilen arabirimdeki time_elapsed girişi ile güncelleştirir. Uygulama, *nx_dhcp_suspend* kullanarak bu hizmeti kullanmadan önce DHCP istemci iş parçacığını askıya almalıdır. Bu hizmet çağrıldıktan sonra uygulama, *nx_dhcp_resume* çağırarak DHCP istemci iş parçacığını sürdürür. Bkz. DHCP Istemci iş parçacığını askıya alma ve sürdürme, DHCP için etkinleştirilen tüm arabirimler için geçerlidir.

Bu, DHCP Istemci iş parçacığını bir süre için askıya almanız gereken DHCP Istemci uygulamalarına yöneliktir ve kalan IP adresi kiralama süresini güncelleştirir.

> [!NOTE] 
> Bu hizmet, daha önce açıklanan *nx_dhcp_client_get_record* ve *nx_dhcp_client_restore_record* birlikte kullanılmak üzere tasarlanmamıştır. Bu hizmetler daha önce bu bölümde açıklanmıştır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr** DHCP Istemcisi işaretçisi

- **interface_index** Geçen süreyi uygulamak için arabirim dizini

- **time_elapsed** IP adresi kirası üzerinde kalan süreden çıkarma süresi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x0) istemci IP kirası güncelleştirildi

- **NX_DHCP_BAD_INTERFACE_INDEX_ERROR** (0x9A) geçersiz arabirim dizini

- NX_PTR_ERROR (0x16) geçersiz DHCP işaretçisi.

- NX_INVALID_INTERFACE (0x4C) geçersiz ağ arabirimi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
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

```C
ULONG nx_dhcp_suspend(NX_DHCP *dhcp_ptr);
```
### <a name="description"></a>Description

Bu hizmet, geçerli DHCP Istemci iş parçacığını askıya alır. *Nx_dhcp_stop* farklı olarak, bu HIZMET çağrıldığında DHCP istemci durumunda hiçbir değişiklik olmadığını unutmayın.

Bu hizmet, DHCP için etkinleştirilen tüm arabirimlerde çalışan DHCP 'yi askıya alır.

DHCP Istemcisi askıya alındığında DHCP Istemci durumunu geçen süre ile güncelleştirmek için, daha önce açıklanan *nx_dhcp_client_update_time_remaining* bakın. Askıya alınmış bir DHCP Istemci iş parçacığını sürdürmesini sağlamak için uygulama *nx_dhcp_resume* çağırmalıdır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr** DHCP Istemcisi işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x0) istemci iş parçacığı askıya alındı

- **NX_PTR_ERROR** (0x16) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Pause the DHCP client thread. */
status=  nx_dhcp_suspend(client_ptr);

/* If status is NX_SUCCESS the current DHCP Client thread is paused. */
```


## <a name="nx_dhcp_resume"></a>nx_dhcp_resume

Askıya alınmış bir DHCP Istemci iş parçacığını sürdürür

### <a name="prototype"></a>Prototype

```C
ULONG nx_dhcp_resume(NX_DHCP *dhcp_ptr);
```
### <a name="description"></a>Description

Bu hizmet, askıya alınmış bir DHCP Istemci iş parçacığını sürdürür. Istemci iş parçacığına devam ettikten sonra gerçek DHCP Istemci durumunda değişiklik olmadığını unutmayın. DHCP Istemci IP adresi kiralamasında kalan süreyi, *nx_dhcp_resume* çağrılmadan önce geçen süre ile güncelleştirmek için, daha önce açıklanan *nx_dhcp_client_update_time_remaining* bakın.

Bu hizmet, DHCP için etkinleştirilen tüm arabirimlerde çalışan DHCP 'yi sürdürür.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr** DHCP Istemcisi işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x0) istemci iş parçacığı sürdürülüyor

- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Resume the DHCP client thread. */
status=  nx_dhcp_resume(client_ptr);

/* If status is NX_SUCCESS the current DHCP Client thread is resumed. */
```