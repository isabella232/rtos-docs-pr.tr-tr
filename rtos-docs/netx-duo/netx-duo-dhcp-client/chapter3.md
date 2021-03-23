---
title: Bölüm 3-Azure RTOS NetX Duo DHCP Istemci hizmetlerinin açıklaması
description: Bu bölüm, tüm Azure RTOS NetX Duo DHCP Istemci hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: f143a443221ae08848316a458a630a0790108198
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826117"
---
# <a name="chapter-3---description-of-azure-rtos-netx-duo-dhcp-client-services"></a>Bölüm 3-Azure RTOS NetX Duo DHCP Istemci hizmetlerinin açıklaması

Bu bölüm, tüm Azure RTOS NetX Duo DHCP Istemci hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.

Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_DISABLE_ERROR_CHECKING** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.

- **nx_dhcp_create**: *DHCP örneği oluşturma*
- **nx_dhcp_clear_broadcast_flag**: *istemci iletilerinde yayın bayrağını temizle*
- **nx_dhcp_delete**: *bir DHCP örneğini silme*
- **nx_dhcp_force_renew**: *zorla yenileme iletisi gönder*
- **nx_dhcp_packet_pool_set**: *DHCP istemci paket havuzunu ayarlama*
- **nx_dhcp_decline**: *sunucuya reddetme iletisi* gönder
- **nx_dhcp_release**: *sunucuya sürüm iletisi* gönder
- **nx_dhcp_reinitialize**: *DHCP istemci ağı parametrelerini temizle*
- **nx_dhcp_request_client_ip**: *belirli bir IP adresi belirtin*
- **nx_dhcp_send_request**: *sunucuya DHCP iletisi gönder*
- **nx_dhcp_start**: *DHCP istemci işlemesini Başlat*
- **nx_dhcp_stop**: *DHCP istemci işlemesini durdur*
- **nx_dhcp_set_interface_index**: *arabirimi DHCP istemcisini çalıştıracak şekilde ayarlama*
- **nx_dhcp_server_address_get**: *DHCP sunucusu IP adresini al*
- **nx_dhcp_state_change_notify**: *DHCP durumu değiştiğinde geri çağırma işlevini ayarla*
- **nx_dhcp_user_option_retrieve**: *belirtilen DHCP seçeneğini Al*
- **nx_dhcp_user_option_convert**: *dört baytı ulong 'a Dönüştür*

Arabirime özgü DHCP Istemci Hizmetleri:
 
- **nx_dhcp_interface_clear_broadcast_flag**: *belirtilen arabirimdeki istemci iletilerinde yayın bayrağını temizle*
- **nx_dhcp_interface_enable**: *belirtilen arabirimde DHCP çalıştırmak için arabirimi etkinleştir*
- **nx_dhcp_interface_disable**: *belirtilen arabirimde DHCP çalıştırmak için arabirimi devre dışı bırak*
- **nx_dhcp_interface_decline**: *belirtilen arabirimdeki sunucuya reddetme iletisi gönder*
- **nx_dhcp_interface_force_renew**: *belirtilen arabirimde zorla yenileme iletisi gönder*
- **nx_dhcp_interface_reinitialize**: *belirtilen arabirimdeki DHCP istemci ağ parametrelerini temizle*
- **nx_dhcp_interface_release**: *belirtilen arabirimdeki sunucuya sürüm iletisi gönder*
- **nx_dhcp_interface_request_client_ip**: *belirtilen ARABIRIMDE belirli bir IP adresi belirtin*
- **nx_dhcp_interface_send_request**: *belirtilen arabirimdeki DHCP iletisini sunucuya gönderin*
- **nx_dhcp_interface_server_address_get**: *belirtilen ARABIRIMDEKI DHCP sunucusu IP adresini al*
- **nx_dhcp_interface_start**: *belirtilen arabirimde DHCP istemci işlemesini Başlat*
- **nx_dhcp_interface_stop**: *belirtilen arabirimdeki DHCP istemci işlemesini durdur*
- **nx_dhcp_interface_state_change_notify**: *belirtilen arabirimdeki DHCP durumu değiştiğinde geri çağırma işlevini ayarla*
- **nx_dhcp_interface_user_option_retrieve**: belirtilen *arabirimde belirtilen DHCP seçeneğini Al*

NX_DHCP_CLIENT_RESORE_STATE tanımlanmışsa DHCP Istemci Hizmetleri:

- **nx_dhcp_resume**: *önceden oluşturulmuş DHCP istemci durumunu sürdürür*
- **nx_dhcp_suspend**: *DHCP istemci durumunu işlemeyi askıya al*
- **nx_dhcp_client_get_record**: *DHCP istemci durumunun kaydını oluşturma*
- **nx_dhcp_client_restore_record**: *daha önce KAYDEDILMIŞ bir kaydı DHCP istemcisine geri yükleme*
- **nx_dhcp_client_update_time_remaining**: *geçerli DHCP durumunda kalan süreyi Güncelleştir*

NX_DHCP_CLIENT_RESORE_STATE tanımlanmışsa arabirime özgü DHCP Istemci Hizmetleri:

- **nx_dhcp_client_interface_get_record**: *belirtilen arabirimde DHCP istemci durumunun bir kaydını oluşturun*
- **nx_dhcp_client_interface_restore_record**: *önceden kaydedilmiş bir kaydı belirtilen arabirimdeki DHCP istemcisine geri yükleme*
- **nx_dhcp_client_interface_update_time_remaining**: *BELIRTILEN arabirimdeki geçerli DHCP durumunda kalan süreyi Güncelleştir*

## <a name="nx_dhcp_create"></a>nx_dhcp_create

DHCP örneği oluşturma

### <a name="prototype"></a>Prototype

```c
UINT nx_dhcp_create(NX_DHCP *dhcp_ptr, NX_IP *ip_ptr, CHAR *name_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, önceden oluşturulan IP örneği için bir DHCP örneği oluşturur. Varsayılan olarak, birincil arabirim DHCP çalıştırmak için etkinleştirilmiştir. DHCP Istemcisinin NetX Duo uygulamasında kullanılmayan ad girişi, ana bilgisayar adları için RFC 1035 ölçütlerine uymalıdır. Toplam uzunluk 255 karakteri aşmamalıdır, noktalarla ayrılmış etiketlerin bir harfle başlaması ve bir harf ya da sayıyla bitmesi gerekir ve kısa çizgi içeremez, ancak alfasayısal olmayan başka karakterler içermemelidir.

Uygulama, DHCP 'nin IP örneğiyle kaydedilmiş başka bir arabirimi çalıştırmak istiyorsanız ( *nx_ip_interface_attach* kullanarak), uygulama, DHCP 'yi yalnızca o arabirim üzerinde çalıştırmak için *nx_dhcp_set_interface_index* ÇAĞıRABILIR veya bu arabirimde DHCP çalıştırmak için *nx_dhcp_interface_enable* . Daha fazla ayrıntı için bu hizmetlerin açıklamasına bakın.

>[!NOTE]
> Uygulamanın, DHCP Istemci paket havuzu yükünün, RFC 2131 Bölüm 2 tarafından belirtilen en düşük DHCP ileti boyutunu (548 bayt DHCP ileti verilerinin yanı sıra UDP, IP ve fiziksel ağ çerçeve üstbilgileri) destekleyebileceğine emin olması gerekir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr**: DHCP denetim bloğuna yönelik işaretçi. 
- **ip_ptr**: daha önce oluşturulan IP örneğine yönelik işaretçi.  
- **name_ptr**: DHCP örneği için ana bilgisayar adı işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı DHCP oluşturma
- **NX_DHCP_INVALID_NAME**: (0Xa8) geçersiz konak adı
- **NX_DHCP_INVALID_PAYLOAD**: (0x9C) yük DHCP iletisi için çok küçük
- NX_PTR_ERROR: (0x16) geçersiz IP veya DHCP işaretçisi

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Create a DHCP instance.  */
status =  nx_dhcp_create(&my_dhcp, &my_ip, "My-DHCP");

/* If status is NX_SUCCESS a DHCP instance was successfully created.  */
```

## <a name="nx_dhcp_interface_enable"></a>nx_dhcp_interface_enable

Belirtilen arabirimi DHCP çalıştırmak için etkinleştir 

### <a name="prototype"></a>Prototype

```c
UINT nx_dhcp_interface_enable(NX_DHCP *dhcp_ptr, UINT interface_index);
```

### <a name="description"></a>Açıklama

Bu hizmet, DHCP çalıştırmak için belirtilen arabirimi sunar. Varsayılan olarak, birincil arabirim DHCP Istemcisi için etkinleştirilmiştir. Bu noktada, DHCP, *nx_dhcp_interface_start* çağırarak veya tüm ETKINLEŞTIRILMIŞ arabirimlerde DHCP 'yi başlatmak için bu arabirim üzerinde başlatılabilir *nx_dhcp_start*.

>[!NOTE] 
> Uygulamanın, nx_ip_interface_attach kullanarak bu arabirimi IP örneğiyle kaydetmesi gerekir *.*

Ayrıca, bu arabirimi etkin arabirimler listesine eklemek için kullanılabilir bir DHCP Istemci arabirimi ' Record ' olmalıdır. Varsayılan olarak NX_DHCP_CLIENT_MAX_RECORDS 1 olarak tanımlanmıştır. DHCP Istemcisini aynı anda çalıştırmak için beklenen en fazla arabirim sayısına bu seçeneği ayarlayın. Genellikle NX_DHCP_CLIENT_MAX_RECORDS, NX_MAX_PHYSICAL_INTERFACES eşit olur; Ancak, bir cihazda DHCP Istemcisi çalıştırmak beklediğinden daha fazla fiziksel arabirim varsa, bu sayıdan daha az NX_DHCP_CLIENT_MAX_RECORDS ayarlayarak bellek tasarrufu sağlayabilir. DHCP Istemci arabirimi kayıtlarıyla bir fiziksel arabirimlerin eşleştirmesi bir tane değildir.

Bu hizmet ve *nx_dhcp_set_interface_index* arasındaki fark, ikinci olarak yalnızca tek BIR arabirim DHCP 'yi çalıştıracak şekilde ayarlıyor. bu hizmet, BELIRTILEN arabirimi DHCP Için etkinleştirilen istemci arabirimleri listesine ekler.

DHCP arabirimini devre dışı bırakmak için uygulama

*nx_dhcp_interface_disable* hizmet.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr**: DHCP denetim bloğuna yönelik işaretçi.  
- **interface_index**: üzerinde DHCP 'yi etkinleştirmek için arabirim dizini

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı DHCP etkin
- **NX_DHCP_NO_RECORDS_AVAILABLE**: (0xa7) başka BIR arabirimin DHCP için etkinleştirilmesi için kullanılabilir kayıt yok
- **NX_DHCP_INTERFACE_ALREADY_ENABLED**: (0xA3) arabirim DHCP için etkinleştirildi
- NX_PTR_ERROR: (0x16) geçersiz IP veya DHCP işaretçisi
- NX_INVALID_INTERFACE: (0x4C) geçersiz ağ arabirimi

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Enable DHCP on a secondary interface. It is already enabled on the primary 
   interface.  NX_DHCP_CLIENT_MAX_RECORDS is set to 2. */

status =  nx_dhcp_interface_enable(&my_dhcp, 1);
/* If status is NX_SUCCESS the interface was successfully enabled.  */


status = nx_dhcp_start(&my_dhcp);
/* If status is NX_SUCCESS DHCP is running on interface 0 and 1.  */
```

## <a name="nx_dhcp_interface_disable"></a>nx_dhcp_interface_disable

DHCP çalıştırmak için belirtilen arabirimi devre dışı bırak 

### <a name="prototype"></a>Prototype

```c

UINT nx_dhcp_interface_disable(NX_DHCP *dhcp_ptr, 
                               UINT interface_index);
```

### <a name="description"></a>Açıklama

Bu hizmet, DHCP çalıştırmak için belirtilen arabirimi devre dışı bırakır. Bu arabirimdeki DHCP Istemcisini yeniden başlatır.

DHCP Istemcisini yeniden başlatmak için, uygulamanın *nx_dhcp_interface_enable* kullanarak arabirimi yeniden etkinleştirmeleri ve *nx_dhcp_interface_start* çağırarak DHCP 'yi yeniden başlatması gerekir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr**: DHCP denetim bloğuna yönelik işaretçi.  
- **interface_index**: DHCP 'yi devre dışı bırakmak için arabirim dizini

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı DHCP oluşturma
- **NX_DHCP_INTERFACE_NOT_ENABLED**: (0xa4) arabirimi DHCP için etkin değil
- NX_PTR_ERROR: (0x16) geçersiz IP veya DHCP işaretçisi
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı
- NX_INVALID_INTERFACE: (0x4C) geçersiz ağ arabirimi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Disable DHCP on a secondary interface. */

status =  nx_dhcp_interface_disable(&my_dhcp, 1);
/* If status is NX_SUCCESS the interface is successfully disabled.  */
```
## <a name="nx_dhcp_clear_broadcast_flag"></a>nx_dhcp_clear_broadcast_flag

DHCP yayın bayrağını ayarlama

### <a name="prototype"></a>Prototype

```c
UINT nx_dhcp_clear_broadcast_flag(NX_DHCP *dhcp_ptr, UINT clear_flag);
```

### <a name="description"></a>Açıklama

Bu hizmet, DHCP için etkinleştirilen tüm arabirimlerin DHCP ileti üst bilgisini ayarlar veya temizler. Istemci bir IP adresine sahip olmadığından, bazı DHCP iletileri (örneğin, bul) yayın bayrağı Broadcast olarak ayarlanır.

clear_flag değerleri: 

- **NX_TRUE**: yayın bayrağı temizlendi (tek noktaya yayın yanıtı iste)
- **NX_FALSE**: yayın bayrağı ayarlandı (Yayın yanıtı iste)

Bu hizmet, yönlendiricinin, iletme yayını iletilerini reddettiği DHCP sunucusuna ulaşmak için bir yönlendiriciden geçmesi gereken DHCP Istemcilerine yöneliktir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr**: DHCP denetim bloğu işaretçisi  
- **clear_flag**: yayın bayrağını ayarlanacak değer

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) bayrağı başarıyla ayarlandı
- NX_PTR_ERROR: (0x16) geçersiz IP veya DHCP işaretçisi

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Send DHCP Client messages with the broadcast flag cleared (e.g. request a  
    unicast response).  */
status =  nx_dhcp_clear_broadcast_flag(&my_dhcp, NX_TRUE);

/* If status is NX_SUCCESS the DHCP Client broadcast flag is updated.  */
```

## <a name="nx_dhcp_interface_clear_broadcast_flag"></a>nx_dhcp_interface_clear_broadcast_flag

Belirtilen arabirimdeki yayın bayrağını ayarla veya temizle

### <a name="prototype"></a>Prototype

```c
UINT nx_dhcp_interface_clear_broadcast_flag(NX_DHCP *dhcp_ptr, 
                                            UINT interface_index, 
                                            UINT clear_flag);
```

### <a name="description"></a>Açıklama

Bu hizmet, DHCP Istemci ana bilgisayar uygulamasının, DHCP Istemci iletilerindeki yayın bayrağını belirtilen arabirimdeki DHCP sunucusuna ayarlamasını veya temizlemesini sağlar. Daha fazla bilgi için bkz. **nx_dhcp_clear_broadcast_flag**.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr**: DHCP denetim bloğu işaretçisi
- **interface_index**: yayın bayrağını ayarlamak için arabirim dizini
- **clear_flag**: yayın bayrağını ayarlanacak değer

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) bayrağı başarıyla ayarlandı
- **NX_DHCP_INTERFACE_NOT_ENABLED**: (0xa4) arabirimi DHCP için etkin değil
- NX_PTR_ERROR: (0x16) geçersiz IP veya DHCP işaretçisi
- NX_INVALID_INTERFACE: (0x4C) geçersiz ağ arabirimi

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Send DHCP Client messages with the broadcast flag cleared (e.g. request a 
   unicast response) on a previously attached secondary interface.  */

iface_index = 1;

status =  nx_dhcp_interface_clear_broadcast_flag(&my_dhcp, iface_index, NX_TRUE);

/* If status is NX_SUCCESS the DHCP Client broadcast flag is updated.  */
```

## <a name="nx_dhcp_delete"></a>nx_dhcp_delete

DHCP örneğini silme

### <a name="prototype"></a>Prototype

```c
UINT nx_dhcp_delete(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet önceden oluşturulmuş bir DHCP örneğini siler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr**: daha önce oluşturulmuş DHCP örneğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı DHCP silme.
- NX_PTR_ERROR: (0x16) geçersiz DHCP işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Delete a DHCP instance.  */
status =  nx_dhcp_delete(&my_dhcp);

/* If status is NX_SUCCESS the DHCP instance was successfully deleted.  */
```

## <a name="nx_dhcp_-force_renew"></a>nx_dhcp_ force_renew

Zorla yenileme iletisi gönder 

### <a name="prototype"></a>Prototype

```c
UINT nx_dhcp force_renew(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, ana bilgisayar uygulamasının DHCP için etkinleştirilen tüm arabirimlerde zorla yenileme iletisi göndermesini sağlar. DHCP Istemcisi, bir bağlantılı durumda olmalıdır. Bu işlev, DHCP Istemcisinin T1 zaman aşımı dolmadan önce yenilemeyi deneyecek şekilde, durumu yenıleme olarak ayarlar.

Birden çok arabirim DHCP etkinken belirli bir arabirim üzerinde zorla yenileme göndermek için *nx_dhcp_interface_force_renew* kullanın.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr**: daha önce oluşturulmuş DHCP örneğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) zorla yenilemeyi başarıyla gönderdi.
- **NX_DHCP_NOT_BOUND**: (0x94) istemci IP adresi bağlanmadı.  
- NX_PTR_ERROR: (0x16) geçersiz DHCP işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Send a force renew message from the Client.  */
status =  nx_dhcp_force_renew(&my_dhcp);

/* If status is NX_SUCCESS the DHCP client state is the RENEWING state and the    
   DHCP Client thread task will begin renewing before T1 is expired.  */
```

## <a name="nx_dhcp_interface_force_renew"></a>nx_dhcp_interface_force_renew

Belirtilen arabirimde zorla yenileme iletisi gönder

### <a name="prototype"></a>Prototype

```c
UINT nx_dhcp_interface_force_renew(NX_DHCP *dhcp_ptr, 
                                   UINT interface_index);
```

### <a name="description"></a>Açıklama

Bu hizmet, arabirim DHCP için etkinleştirilmiş olduğu sürece, ana bilgisayar uygulamasının giriş arabiriminde zorla yenileme iletisi göndermesini sağlar (bkz. *nx_dhcp_interface_enable*). Belirtilen arabirimdeki DHCP Istemcisinin bağlı durumda olması gerekir. Bu işlev, DHCP Istemcisinin T1 zaman aşımı dolmadan önce yenilemeyi deneyecek şekilde, durumu yenıleme olarak ayarlar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr**: daha önce oluşturulmuş DHCP örneğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) zorla yenilemeyi başarıyla gönderdi.  
- **NX_DHCP_INTERFACE_NOT_ENABLED**: (0xa4) arabirimi DHCP için etkin değil
- NX_PTR_ERROR: (0x16) geçersiz IP veya DHCP işaretçisi
- NX_INVALID_INTERFACE: (0x4C) geçersiz ağ arabirimi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Send a force renew message to the server on interface 1.  */
status =  nx_dhcp_interface_force_renew(&my_dhcp, 1);


/* If status is NX_SUCCESS the DHCP client state is the RENEWING state and the    
   DHCP Client thread task will begin renewing before T1 is expired.  */
```

## <a name="nx_dhcp_packet_pool_set"></a>nx_dhcp_packet_pool_set

DHCP Istemci paket havuzunu ayarlama

### <a name="prototype"></a>Prototype

```c
UINT nx_dhcp_packet_pool_set(NX_DHCP *dhcp_ptr, NX_PACKET_POOL *packet_pool_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, uygulamanın bu hizmet çağrısında daha önce oluşturulmuş bir paket havuzuna bir işaretçi geçirerek DHCP Istemci paket havuzunu oluşturmasına izin verir. Bu özelliği kullanmak için, ana bilgisayar uygulamasının NX_DHCP_CLIENT_USER_CREATE_PACKET_POOL tanımlanmalıdır. Tanımlandığında, *nx_dhcp_create* hizmet istemcinin paket havuzunu oluşturmaz. 

>[!NOTE] 
> Uygulamanın, paket havuzu oluştururken *nxd_dhcp_client. h* içinde NX_DHCP_PACKET_PAYLOAD olarak tanımlanan DHCP istemci paket havuzu yükünün varsayılan değerlerini kullanması önerilir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr**: DHCP denetim bloğuna yönelik işaretçi.  
- **packet_pool_ptr**: daha önce oluşturulmuş olan paket havuzuna yönelik işaretçi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) DHCP istemci paket havuzu ayarlandı
- **NX_NOT_ENABLED**: (0x14) hizmeti etkin değil
- NX_PTR_ERROR: (0x16) geçersiz DHCP işaretçisi
- NX_DHCP_INVALID_PAYLOAD: (0x9C) yük çok küçük

### <a name="allowed-from"></a>İzin verilen

Uygulama kodu

### <a name="example"></a>Örnek

```c
/* Create the packet pool. */
status =  nx_packet_pool_create(&dhcp_pool, "DHCP Client Packet Pool", 
                                 NX_DHCP_PACKET_PAYLOAD, pointer, 
                                 (15 * NX_DHCP_PACKET_PAYLOAD));

/* Create the DHCP Client. */
status =  nx_dhcp_create(&dhcp_0, &ip_0, "janetsdhcp1");

/* Set the DHCP Client packet pool.  */
status =  nx_dhcp_packet_pool_set(&my_dhcp, packet_pool_ptr);
/* If status is NX_SUCCESS packet pool was successfully set.  */

```

## <a name="nx_dhcp_request_client_ip"></a>nx_dhcp_request_client_ip

DHCP örneği için istenen IP adresini ayarlama

### <a name="prototype"></a>Prototype

```c
UINT nx_dhcp_request_client_ip(NX_DHCP *dhcp_ptr, 
                               ULONG client_ip_address, 
                               UINT skip_discover_message);
```

### <a name="description"></a>Açıklama

Bu hizmet, DHCP Istemcisinin DHCP istemci kaydında DHCP için etkinleştirilen ilk arabirimdeki DHCP sunucusundan istemesi için IP adresini ayarlar. *Skip_discover_message* bayrağı AYARLANDıYSA, DHCP istemcisi bulma iletisini atlar ve bir istek iletisi gönderir.

Belirli bir arabirimdeki DHCP iletileri için belirli bir IP isteği ayarlamak üzere *nx_dhcp_interface_request_client_ip* hizmetini kullanın.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr**: DHCP denetim bloğuna yönelik işaretçi.  
- **client_ip_address**: DHCP sunucusundan isteğin IP adresi
- **skip_discover_message**: 
    - Doğru ise, DHCP Istemcisi Istek iletisi gönderir
    - Yanlışsa, bulma iletisini gönderir.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) istenen IP adresi ayarlanmış.
- NX_PTR_ERROR: (0x16) geçersiz DHCP işaretçisi
- NX_DHCP_INVALID_IP_REQUEST: (0x9D) NULL IP adresi istendi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Set the DHCP Client requested IP address and skip the discover message.  */

status =  nx_dhcp_request_client_ip(&my_dhcp, IP(192,168,0,6), NX_TRUE);

/* If status is NX_SUCCESS requested IP address was successfully set.  */

```

## <a name="nx_dhcp_interface_request_client_ip"></a>nx_dhcp_interface_request_client_ip

Belirtilen arabirimdeki DHCP örneği için istenen IP adresini ayarla

### <a name="prototype"></a>Prototype

```c
UINT nx_dhcp_interface_request_client_ip(NX_DHCP *dhcp_ptr, UINT  interface_index, 
                                         ULONG client_ip_address, UINT skip_discover_message);
```

### <a name="description"></a>Açıklama

Bu hizmet, DHCP Istemcisinin, belirtilen arabirimdeki DHCP sunucusundan istemesi için IP adresini ayarlar, bu arabirim DHCP için etkinleştirilmişse (bkz. *nx_dhcp_interface_enable*). *Skip_discover_message* bayrağı AYARLANDıYSA, DHCP istemcisi bulma iletisini atlar ve bir istek iletisi gönderir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr**: DHCP denetim bloğuna yönelik işaretçi.
- **Interface_index**: IP adresi istemek için arabirim dizini
- **client_ip_address**: DHCP sunucusundan isteğin IP adresi
- **skip_discover_message**: true Ise, DHCP istemcisi istek iletisi gönderir; diğer bir deyişle, bulma iletisini gönderir.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) istenen IP adresi ayarlanmış.
- **NX_DHCP_INTERFACE_NOT_ENABLED**: (0xa4) arabirimi DHCP için etkin değil
- NX_PTR_ERROR: (0x16) geçersiz IP veya DHCP işaretçisi
- NX_INVALID_INTERFACE: (0x4C) geçersiz ağ arabirimi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Set the DHCP Client requested IP address and skip the discover message on  
   interface 0.  */
status =  nx_dhcp_interface_request_client_ip(&my_dhcp, 0, IP(192,168,0,6), NX_TRUE);

/* If status is NX_SUCCESS requested IP address was successfully set.  */
```

## <a name="nx_dhcp_reinitialize"></a>nx_dhcp_reinitialize

DHCP istemci ağı parametrelerini Temizleme 

### <a name="prototype"></a>Prototype

```c
UINT nx_dhcp_reinitialize(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, ana bilgisayar uygulama ağ parametrelerini (IP adresi, ağ adresi ve ağ maskesi) temizler ve DHCP için etkinleştirilen tüm arabirimlerde DHCP Istemci durumunu temizler. *Nx_dhcp_stop* ile birlikte KULLANıLıR ve DHCP durum makinesine ' yeniden Başlat ' için *nx_dhcp_start* :

```c
nx_dhcp_stop(&my_dhcp);
nx_dhcp_reinitialize(&my_dhcp);
nx_dhcp_start(&my_dhcp);
```

DHCP için birden fazla arabirim etkinleştirildiğinde belirli bir arabirimdeki DHCP Istemcisini yeniden başlatmak için *nx_dhcp_interface_reinitialize* hizmetini kullanın.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr**: daha önce oluşturulmuş DHCP örneğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) DHCP başarıyla yeniden başlatıldı 
- NX_PTR_ERROR: (0x16) geçersiz DHCP işaretçisi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Reinitialize the previously started DHCP client.  */
status =  nx_dhcp_reinitialize(&my_dhcp);

/* If status is NX_SUCCESS the host application successfully reinitialized its network parameters and DHCP client state. */
```

## <a name="nx_dhcp_interface_reinitialize"></a>nx_dhcp_interface_reinitialize

Belirtilen arabirimdeki DHCP istemci ağ parametrelerini temizle 

### <a name="prototype"></a>Prototype

```c
UINT nx_dhcp_interface_reinitialize(NX_DHCP *dhcp_ptr, 
                                     UINT interface_index);
```

### <a name="description"></a>Açıklama

Bu hizmet, bu arabirim DHCP için etkinleştirilmişse belirtilen arabirimdeki ağ parametrelerini (IP adresi, ağ adresi ve ağ maskesi) temizler (bkz. *nx_dhcp_interface_enable*). Daha fazla bilgi için bkz. *nx_dhcp_reinitialize* .

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr**: daha önce oluşturulmuş DHCP örneğine yönelik işaretçi
- **interface_index**: yeniden başlatmak için arabirim dizini

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) arabirimi başarıyla yeniden başlatıldı
- **NX_DHCP_INTERFACE_NOT_ENABLED**: (0xa4) arabirimi DHCP için etkin değil
- NX_PTR_ERROR: (0x16) geçersiz DHCP işaretçisi
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.
- NX_INVALID_INTERFACE: (0x4C) geçersiz ağ arabirimi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Reinitialize the previously started DHCP client on interface 1.  */
status =  nx_dhcp_interface_reinitialize(&my_dhcp, 1);

/* If status is NX_SUCCESS the host application successfully reinitialized its network parameters and DHCP client state. */
```

## <a name="nx_dhcp_release"></a>nx_dhcp_release

Yayın kiralanan IP adresi

### <a name="prototype"></a>Prototype

```c
UINT nx_dhcp_release(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, bir DHCP sunucusundan alınan IP adresini, yayın iletisini bu sunucuya göndererek yayınlar. Daha sonra DHCP Istemcisini yeniden başlatır. Bu hizmet, DHCP için etkinleştirilen tüm arabirimlere uygulanır.

Uygulama, *nx_dhcp_start* çağırarak DHCP istemcisini yeniden başlatabilir.

Bir adresi belirli bir arabirimdeki DHCP sunucusuna geri yüklemek için *nx_dhcp_interface_release* hizmetini kullanın

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr**: daha önce oluşturulmuş DHCP örneğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı DHCP sürümü.  
- **NX_DHCP_NOT_BOUND**: (0x94) IP adresi kiralamadı, bu nedenle serbest bırakılamaz.
- NX_PTR_ERROR: (0x16) geçersiz DHCP işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Release the previously leased IP address.  */
status =  nx_dhcp_release(&my_dhcp);

/* If status is NX_SUCCESS the previous IP lease was successfully released.  */
```

## <a name="nx_dhcp_interface_release"></a>nx_dhcp_interface_release

Belirtilen arabirimdeki IP adresini serbest bırak

### <a name="prototype"></a>Prototype

```c
UINT nx_dhcp_interface_release(NX_DHCP *dhcp_ptr, UINT interface_index);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen arabirimdeki bir DHCP sunucusundan alınan IP adresini serbest bırakır ve DHCP Istemcisini yeniden başlatır. DHCP Istemcisi, *nx_dhcp_start* çağırarak yeniden başlatılabilir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr**: daha önce oluşturulmuş DHCP örneğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı DHCP sürümü.
- **NX_DHCP_INTERFACE_NOT_ENABLED**: (0xa4) arabirimi DHCP için etkin değil
- **NX_DHCP_NOT_BOUND**: (0x94) IP adresi kiralamadı, bu nedenle serbest bırakılamaz.
- NX_PTR_ERROR: (0x16) geçersiz DHCP işaretçisi
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.
- NX_INVALID_INTERFACE: (0x4C) geçersiz ağ arabirimi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Release the previously leased IP address on interface 1.  */
status =  nx_dhcp_interface_release(&my_dhcp, 1);

/* If status is NX_SUCCESS the previous IP lease was successfully released.  */
```

## <a name="nx_dhcp_decline"></a>nx_dhcp_decline

DHCP sunucusundan IP adresini Reddet

### <a name="prototype"></a>Prototype

```c
UINT nx_dhcp_decline(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, DHCP için etkinleştirilen tüm arabirimlerde DHCP sunucusundan kiralanmış bir IP adresini reddeder. NX_DHCP_CLIENT_ SEND_ ARP_PROBE tanımlanmışsa, DHCP Istemcisi IP adresinin zaten kullanımda olduğunu algılarsa bir reddetme iletisi gönderir. NetX Duo DHCP Istemcisinde ARP araştırma yapılandırması hakkında daha fazla bilgi için bkz. bölüm içinde **ARP araştırmaları** .

Uygulama, adresin başka yollarla kullanımda olduğunu tespit etmezse IP adresini reddetmek için bu hizmeti kullanabilir.

Bu hizmet, DHCP Istemcisini *nx_dhcp_start* çağırarak yeniden başlatılacak şekilde yeniden başlatır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr**: daha önce oluşturulmuş DHCP örneğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) reddetme başarıyla gönderildi  
- **NX_DHCP_NOT_BOUND**: (0x94) DHCP istemcisi bağlanmadı
- NX_PTR_ERROR: (0x16) geçersiz DHCP işaretçisi
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c

/* Decline the IP address offered by the DHCP server.  */
status =  nx_dhcp_decline(&my_dhcp);

/* If status is NX_SUCCESS the previous IP address decline message was successfully trasnmitted.  */
```

## <a name="nx_dhcp_interface_decline"></a>nx_dhcp_interface_decline

Belirtilen arabirimdeki DHCP sunucusundan IP adresini Reddet

### <a name="prototype"></a>Prototype

```c
UINT nx_dhcp_interface_decline(NX_DHCP *dhcp_ptr, 
                               UINT interface_index);
```

### <a name="description"></a>Açıklama

Bu hizmet, DHCP sunucusu tarafından atanan bir IP adresini reddetmek için reddetme iletisini sunucuya gönderir. Ayrıca, DHCP Istemcisini yeniden başlatır. Daha fazla bilgi için bkz. *nx_dhcp_decline* .

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr**: daha önce oluşturulmuş DHCP örneğine yönelik işaretçi.
- **Interface_index**: IP adresini reddetme arabiriminin dizini

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) DHCP reddetme iletisi gönderildi  
- **NX_DHCP_NOT_BOUND**: (0x94) DHCP istemcisi bağlanmadı
- **NX_DHCP_INTERFACE_NOT_ENABLED**: (0xa4) arabirimi DHCP için etkin değil
- NX_PTR_ERROR: (0x16) geçersiz DHCP işaretçisi
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.
- NX_INVALID_INTERFACE: (0x4C) geçersiz ağ arabirimi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Decline the IP address offered by the DHCP server on interface 2.  */
status =  nx_dhcp_interface_decline(&my_dhcp, 2);

/* If status is NX_SUCCESS the previous IP address decline message was successfully trasnmitted.  */
```
## <a name="nx_dhcp_send_request"></a>nx_dhcp_send_request

DHCP iletisini sunucuya gönder

### <a name="prototype"></a>Prototype

```c
UINT nx_dhcp_send_request(NX_DHCP *dhcp_ptr, UINT dhcp_message_type);

```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen DHCP iletisini DHCP Istemci kaydında bulunan DHCP için etkinleştirilen ilk arabirimdeki DHCP sunucusuna gönderir. Bir yayın veya reddetme iletisi göndermek için, uygulamanın sırasıyla *nx_dhcp [_interface] _Release*() veya *nx_dhcp_interface_decline ()* hizmetlerini kullanması gerekir.

Bu hizmeti kullanmak için, DHCP Istemcisinin INFORM_REQUEST ileti türünü gönderme haricinde başlatılmış olması gerekir.

>[!NOTE]
> Bu hizmet, ana bilgisayar uygulamasının DHCP Istemci durumu makinesine ' Drive ' için tasarlanmamıştır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr**: DHCP denetim bloğuna yönelik işaretçi.  
- **dhcp_message_type**: ileti isteği ( *nxd_dhcp_client. h* içinde tanımlı)

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) DHCP iletisi gönderildi  
- **NX_DHCP_NOT_STARTED**: (0x96) geçersiz arabirim dizini
- **NX_DHCP_INVALID_MESSAGE**: (0x9b) göndermek için geçersiz ileti türü
- NX_PTR_ERROR: (0x16) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Send the DHCP INFORM REQUEST message to the server.  */

status =  nx_dhcp_send_request(&my_dhcp, NX_DHCP_TYPE_DHCPINFORM);
/* If status is NX_SUCCESS a DHCP message was successfully sent.  */
```

## <a name="nx_dhcp_interface_send_request"></a>nx_dhcp_interface_send_request

Belirli bir arabirimdeki DHCP iletisini sunucuya gönder

### <a name="prototype"></a>Prototype

```c
UINT nx_dhcp_interface_send_request(NX_DHCP *dhcp_ptr, 
                                    UINT interface_index, 
                                    UINT dhcp_message_type);
```

### <a name="description"></a>Açıklama

Bu hizmet, bu arabirim DHCP için etkinleştirilmişse, belirtilen arabirimdeki DHCP sunucusuna bir ileti gönderir. Bir yayın veya reddetme iletisi göndermek için, uygulamanın sırasıyla *nx_dhcp [_interface] _Release*() veya *nx_dhcp_interface_decline ()* hizmetlerini kullanması gerekir.

DHCP Istemcisi, DHCP BILDIR Istek iletisi türünü göndermek dışında bu hizmeti kullanacak şekilde başlatılmalıdır.

Bu hizmet, ana bilgisayar uygulamasının DHCP Istemci durumu makinesine ' Drive ' için tasarlanmamıştır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr**: DHCP denetim bloğuna yönelik işaretçi.
- **Interface_index**: iletinin gönderileceği arabirimin dizini
- **dhcp_message_type**: ileti isteği (nxd_dhcp_client. h içinde tanımlı)

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) DHCP iletisi gönderildi  
- **NX_DHCP_NOT_STARTED**: (0x96) geçersiz arabirim dizini
- **NX_DHCP_INVALID_MESSAGE**: (0x9b) göndermek için geçersiz ileti türü
- **NX_DHCP_INTERFACE_NOT_ENABLED**: (0xa4) arabirimi DHCP için etkin değil
- NX_PTR_ERROR: (0x16) geçersiz DHCP işaretçisi
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.
- NX_INVALID_INTERFACE: (0x4C) geçersiz ağ arabirimi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Send the INFORM REQUEST message to the server on the primary interface.  */

status =  nx_dhcp_interface_send_request(&my_dhcp, 0, NX_DHCP_TYPE_DHCPINFORM);
/* If status is NX_SUCCESS a DHCP message was successfully sent.  */
```

## <a name="nx_dhcp_server_address_get"></a>nx_dhcp_server_address_get

DHCP Istemcisinin DHCP sunucusu IP adresini al

### <a name="prototype"></a>Prototype

```c
UINT nx_dhcp_server_address_get(NX_DHCP *dhcp_ptr, 
                                ULONG server_address);
```

### <a name="description"></a>Açıklama

Bu hizmet DHCP istemci kaydında bulunan DHCP için etkinleştirilen ilk arabirimdeki DHCP Istemci DHCP sunucusu IP adresini alır. Çağıran bu hizmeti yalnızca DHCP Istemcisi DHCP sunucusu tarafından atanan bir IP adresine bağlandıktan sonra kullanabilir. Konak uygulama, IP adresinin ayarlandığını doğrulamak için *nx_ip_status_check* hizmetini kullanabilir veya NX *_DHCP_STATE_CHANGE_NOTIFY* kullanabilir ve DHCP istemci durumunun NX_DHCP_STATE_BOUND olduğunu sorgulayabilir. Durum değişikliği geri arama işlevini ayarlama hakkında daha fazla ayrıntı için bkz. *nx_dhcp_state_change_notify* .

DHCP Istemcisi için birden çok arabirim etkinleştirildiğinde, belirli bir arabirimdeki DHCP sunucusunu bulmak için *nx_dhcp_interface_server_address_get* hizmetini kullanın

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr**: DHCP denetim bloğuna yönelik işaretçi.
- **server_address**: sunucu IP adresi işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) DHCP sunucusu adresi döndürüldü
- **NX_DHCP_NO_INTERFACES_ENABLED**: (0xa5) DHCP için etkinleştirilen arabirim yok
- NX_PTR_ERROR: (0x16) geçersiz giriş işaretçisi
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Use the state change notify service to determine the Client transition to the bound state and get its DHCP server IP address.*/

void dhcp_state_change(NX_DHCP *dhcp_ptr, UCHAR new_state)
{
ULONG server_address;
UINT  status;

/* Increment state changes counter.  */
state_changes++;

if (dhcp_0.nx_dhcp_state == NX_DHCP_STATE_BOUND)
        {
            status = nx_dhcp_server_address_get(&dhcp_0, &server_address);
        }

}
```

## <a name="nx_dhcp_interface_server_address_get"></a>nx_dhcp_interface_server_address_get

Belirtilen arabirimdeki DHCP Istemcisinin DHCP sunucusu IP adresini al

### <a name="prototype"></a>Prototype

```c
UINT nx_dhcp_interface_server_address_get(NX_DHCP *dhcp_ptr, 
                                          UINT interface_index,
                                          ULONG server_address);
```

### <a name="description"></a>Açıklama

Bu hizmet, bu arabirim DHCP için etkinleştirilmişse, belirtilen arabirimdeki DHCP Istemci DHCP sunucusu IP adresini alır. DHCP Istemcisi, bağlantılı durumda olmalıdır. Bu arabirimdeki DHCP Istemcisini başlattıktan sonra konak uygulama, IP adresinin ayarlandığını doğrulamak için *nx_ip_status_check* hizmetini kullanabilir ya da DHCP istemci durumu değişikliği geri aramasını KULLANABILIR ve DHCP istemci durumunun NX_DHCP_STATE_BOUND. Durum değişikliği geri arama işlevini ayarlama hakkında daha fazla ayrıntı için bkz. *nx_dhcp_state_change_notify* .

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr**: DHCP denetim bloğuna yönelik işaretçi.
- **Interface_index**: IP adresi almak için arabirimin dizini
- **server_address**: sunucu IP adresi işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) DHCP sunucusu adresi döndürüldü
- **NX_DHCP_NO_INTERFACES_ENABLED**: (0xa5) DHCP için etkinleştirilen arabirim yok
- **NX_DHCP_NOT_BOUND**: (0x94) DHCP istemcisi bağlanmadı
- NX_PTR_ERROR: (0x16) geçersiz DHCP işaretçisi
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.
- NX_INVALID_INTERFACE: (0x4C) geçersiz ağ arabirimi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Use the state change notify service to determine the Client transition to the 
bound state and get its DHCP server IP address. */

void dhcp_state_change(NX_DHCP *dhcp_ptr, UCHAR new_state)
{

ULONG server_address;
UINT  status;

/* Increment state changes counter.  */
state_changes++;

/* Get the DHCP server IP address on interface 1 */
if (dhcp_0.nx_dhcp_state == NX_DHCP_STATE_BOUND)
        {
         status = nx_dhcp_interface_server_address_get(&dhcp_0, 1, 
                                                       &server_address);
        }
}
```

## <a name="nx_dhcp_set_interface_index"></a>nx_dhcp_set_interface_index

DHCP örneği için ağ arabirimini ayarla

### <a name="prototype"></a>Prototype

```c
UINT nx_dhcp_set_interface_index(NX_DHCP *dhcp_ptr, UINT index);
```

### <a name="description"></a>Açıklama

Bu hizmet, DHCP örneği için ağ arabirimini, tek bir ağ arabirimi için yapılandırılmış DHCP Istemcisini çalıştırırken üzerinde DHCP sunucusuna bağlanacak şekilde ayarlar.

Varsayılan olarak, DHCP Istemcisi birincil arabirimde çalışır. İkincil bir hizmette DHCP çalıştırmak için bu hizmeti kullanarak ikincil arabirimi DHCP Istemci arabirimi olarak ayarlayın. Uygulamanın, *nx_ip_interface_attach* hizmetini kullanarak BELIRTILEN arabirimi IP örneğine daha önce kaydetmesi gerekir.

>[!NOTE]
> Bu hizmet, DHCP Istemcisini yalnızca bir arabirimde çalıştırmayı hedefleyen uygulamalara yöneliktir. Birden çok arabirimde DHCP çalıştırmak için daha fazla ayrıntı için *nx_dhcp_interface_enable* bakın.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr**: DHCP denetim bloğuna yönelik işaretçi.  
- **Dizin**: cihaz ağ arabiriminin dizini

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) arabirimi başarıyla ayarlandı.
- **NX_INVALID_INTERFACE**: (0x4C) geçersiz ağ arabirimi
- **NX_DHCP_INTERFACE_ALREADY_ENABLED**: (0xA3) arabirim DHCP için etkinleştirildi
- **NX_DHCP_NO_RECORDS_AVAILABLE**: (0xa7) başka bir kayıt yok 
- NX_PTR_ERROR: (0x16) geçersiz DHCP işaretçisi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Set the DHCP Client interface to the secondary interface (index 1).  */
status =  nx_dhcp_set_interface_index(&my_dhcp, 1);
/* If status is NX_SUCCESS a DHCP interface was successfully set.  */
```

## <a name="nx_dhcp_start"></a>nx_dhcp_start

DHCP işlemesini Başlat

### <a name="prototype"></a>Prototype

```c
UINT nx_dhcp_start(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet DHCP için etkinleştirilen tüm arabirimlerde DHCP işlemeyi başlatır. Varsayılan olarak, uygulama nx_dhcp_create çağırdığında, birincil arabirim DHCP için etkinleştirilir *.*

IP örneğinin DHCP Istemci arabirimindeki bir IP adresine bağlı olduğunu doğrulamak için *nx_ip_status_check* kullanarak IP adresinin geçerli olduğunu doğrulayın.

Zaten DHCP çalıştıran başka arabirimler varsa, bu hizmet bu hizmet tarafından etkilenmeyecektir.

Birden çok arabirim etkinleştirildiğinde, belirli bir arabirimde DHCP 'yi başlatmak için *nx_dhcp_interface_start* hizmetini kullanın.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr**: daha önce oluşturulmuş DHCP örneğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı DHCP başlatması.  
- **NX_DHCP_ALREADY_STARTED**: (0x93) DHCP zaten başlatılmış.
- NX_PTR_ERROR: (0x16) geçersiz DHCP işaretçisi.
- NX_CALLER_ERROR: (0x11) geçersiz hizmet çağıranı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Start the DHCP processing for this IP instance.  */
status =  nx_dhcp_start(&my_dhcp);

/* If status is NX_SUCCESS the DHCP was successfully started.  */
```

## <a name="nx_dhcp_interface_start"></a>nx_dhcp_interface_start

Belirtilen arabirimde DHCP işlemeyi Başlat

### <a name="prototype"></a>Prototype

```c
UINT nx_dhcp_interface_start(NX_DHCP *dhcp_ptr, UINT interface_index);
```

### <a name="description"></a>Açıklama

Bu hizmet, bu arabirim DHCP için etkinleştirilmişse, belirtilen arabirim üzerinde DHCP işlemi başlatır. DHCP için bir arabirim etkinleştirme hakkında daha fazla ayrıntı için bkz. *nx_dhcp_interface_enable*(). Varsayılan olarak, uygulama nx_dhcp_create çağırdığında, birincil arabirim DHCP için etkinleştirilir *.*

DHCP Istemcisi çalıştıran başka arabirim yoksa, bu hizmet DHCP istemci iş parçacığını başlatır/sürdürür ve (yeniden) DHCP Istemci zamanlayıcısını etkinleştirir.  
  
Uygulamanın bir IP adresinin elde olup olmadığını doğrulamak için *nx_ip_status_check* kullanması gerekir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr**: daha önce oluşturulmuş DHCP örneğine yönelik işaretçi.
- **Interface_index**: DHCP istemcisinin başlatılacağı Dizin

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı DHCP başlatması. 
- **NX_DHCP_ALREADY_STARTED**: (0x93) DHCP zaten başlatılmış.
- NX_PTR_ERROR: (0x16) geçersiz DHCP işaretçisi.
- NX_CALLER_ERROR: (0x11) geçersiz hizmet çağıranı.
- NX_INVALID_INTERFACE: (0x4C) geçersiz ağ arabirimi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Start the DHCP processing for this IP instance on interface 1.  */
status =  nx_dhcp_interface_start(&my_dhcp, 1);

/* If status is NX_SUCCESS the DHCP was successfully started.  */
```

## <a name="nx_dhcp_state_change_notify"></a>nx_dhcp_state_change_notify

DHCP durum değiştirme geri çağırma işlevini ayarla

### <a name="prototype"></a>Prototype

```c
UINT nx_dhcp_state_change_notify(NX_DHCP *dhcp_ptr, 
                                 VOID (*dhcp_state_change_notify)(NX_DHCP *dhcp_ptr, UCHAR new_state));
```

### <a name="description"></a>Açıklama

Bu hizmet, DHCP durum değişikliklerinin bir uygulamasına bildirimde bulunmak için dhcp_state_change_notify belirtilen geri çağırma işlevini kaydeder. Geri arama işlevi, DHCP Istemcisinin geçiş durumunu sağlar.

Aşağıdakiler, çeşitli DHCP durumlarıyla ilişkili değerlerdir:

- NX_DHCP_STATE_BOOT: 1
- NX_DHCP_STATE_INIT: 2
- NX_DHCP_STATE_SELECTING: 3
- NX_DHCP_STATE_REQUESTING: 4
- NX_DHCP_STATE_BOUND: 5
- NX_DHCP_STATE_RENEWING: 6
- NX_DHCP_STATE_REBINDING: 7
- NX_DHCP_STATE_FORCERENEW: 8
- NX_DHCP_STATE_ADDRESS_PROBING: 9

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr**: daha önce oluşturulmuş DHCP örneğine yönelik işaretçi.
- **dhcp_state_change_notify**: durum değiştirme geri çağırma işlev işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı geri arama kümesi.  
- NX_PTR_ERROR: (0x16) geçersiz DHCP işaretçisi.
- NX_CALLER_ERROR: (0x11) geçersiz hizmet çağıranı.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Register the “my_state_change” function to be called on any DHCP state change, assuming DHCP has alreadybeen created.  */
status =  nx_dhcp_state_change_notify(&my_dhcp, my_state_change);

/* If status is NX_SUCCESS the callback function was successfully
   registered.  */
```

## <a name="nx_dhcp_interface_state_change_notify"></a>nx_dhcp_interface_state_change_notify

Belirtilen arabirimdeki DHCP durum değiştirme geri çağırma işlevini ayarla

### <a name="prototype"></a>Prototype

```c
UINT nx_dhcp_interface_state_change_notify(NX_DHCP *dhcp_ptr, UINT interface_index,
                                           VOID (*dhcp_state_change_notify)(NX_DHCP *dhcp_ptr, 
                                                                            UINT interface_index,
                                                                            UCHAR new_state));
```

### <a name="description"></a>Açıklama

Bu hizmet, DHCP durum değişikliklerinin bir uygulamasına bildirimde bulunmak için belirtilen geri çağırma işlevini kaydeder. Geri çağırma, funcıton giriş bağımsız değişkenleri, arabirim dizinidir ve DHCP Istemcisinin bu arabirimde geçiş olduğu durumdur.

Durum değişikliği işlevleri hakkında daha fazla bilgi için bkz. *nx_dhcp_state_change_notify*().

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr**: daha önce oluşturulmuş DHCP örneğine yönelik işaretçi.
- **dhcp_interface_state_change_notify**: uygulama geri çağırma işlev işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı geri arama kümesi.  
- NX_PTR_ERROR: (0x16) geçersiz DHCP işaretçisi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Register the “my_state_change” function to be called on any DHCP state change,   
   assuming DHCP has alreadybeen created.  */

void dhcp_interstate_state_change(NX_DHCP *dhcp_ptr, UINT iface_index, 
                                  UCHAR new_state);


status =  nx_dhcp_interstate_state_change_notify(&my_dhcp,  
                                                 dhcp_interstate_state_change);

/* If status is NX_SUCCESS the callback function was successfully
   registered.  */
```

## <a name="nx_dhcp_stop"></a>nx_dhcp_stop

DHCP işlemesini durduruyor

### <a name="prototype"></a>Prototype

```c
UINT nx_dhcp_stop(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, DHCP işlemesini Başlatan tüm arabirimlerde DHCP işlemeyi durduruyor. DHCP 'yi işleyen bir arabirim yoksa, bu hizmet DHCP Istemci iş parçacığını askıya alacak ve DHCP Istemci zamanlayıcısını devre dışı kalacak.

DHCP için birden çok arabirim etkinleştirilmişse, belirli bir arabirimdeki DHCP 'yi durdurmak için *nx_dhcp_interface_stop* hizmetini kullanın.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr**: daha önce oluşturulmuş DHCP örneğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı DHCP durağı
- **NX_DHCP_NOT_STARTED**: (0x96) DHCP örneği başlatılmadı.
- NX_PTR_ERROR: (0x16) geçersiz DHCP işaretçisi.
- NX_CALLER_ERROR: (0x11) geçersiz hizmet çağıranı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Stop the DHCP processing for this IP instance.  */
status =  nx_dhcp_stop(&my_dhcp);

/* If status is NX_SUCCESS the DHCP was successfully stopped.  */
```

## <a name="nx_dhcp_interface_stop"></a>nx_dhcp_interface_stop

Belirtilen arabirimdeki DHCP işlemesini durdur

### <a name="prototype"></a>Prototype

```c
UINT nx_dhcp_interface_stop(NX_DHCP *dhcp_ptr, UINT interface_index);
```

### <a name="description"></a>Açıklama

Bu hizmet, DHCP zaten başlatılmışsa belirtilen arabirimdeki DHCP işlemesini durduruyor. DHCP çalıştıran başka arabirimler yoksa, DHCP iş parçacığı ve Zamanlayıcı askıya alınır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr**: daha önce oluşturulmuş DHCP örneğine yönelik işaretçi.
- **Interface_index**: DHCP işleminin durdurulacağı arabirim

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı DHCP durağı
- **NX_DHCP_NOT_STARTED**: (0x96) DHCP başlatılmadı.
- NX_PTR_ERROR: (0x16) geçersiz DHCP işaretçisi.
- NX_CALLER_ERROR: (0x11) geçersiz hizmet çağıranı.
- NX_INVALID_INTERFACE: (0x4C) geçersiz ağ arabirimi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Stop DHCP processing for this IP instance on interface 1.  */
status =  nx_dhcp_interface_stop(&my_dhcp, 1);

/* If status is NX_SUCCESS the DHCP was successfully stopped.  */
```

## <a name="nx_dhcp_user_option_retrieve"></a>nx_dhcp_user_option_retrieve

Son sunucu yanıtından bir DHCP seçeneği alın

### <a name="prototype"></a>Prototype

```c
UINT nx_dhcp_user_option_retrieve(NX_DHCP *dhcp_ptr, UINT request_option, 
                                  UCHAR *destination_ptr, UINT *destination_size);
```

### <a name="description"></a>Açıklama

Bu hizmet, DHCP Istemci kaydında bulunan DHCP için etkinleştirilen ilk arabirimdeki DHCP seçenekleri arabelleğinden belirtilen DHCP seçeneğini alır. Başarılı olursa, seçenek verileri belirtilen arabelleğe kopyalanır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr**: daha önce oluşturulmuş DHCP örneğine yönelik işaretçi.  
- **request_option**: DHCP seçeneği, RFC 'ler tarafından belirtilen şekilde. *Nxd_dhcp_client. h* içindeki NX_DHCP_OPTION seçeneğine bakın.
- **destination_ptr**: Yanıt dizesi için hedefin işaretçisi.  
- **destination_size**: hedefin boyutuna ve dönüşe ilişkin işaretçi, döndürülen bayt sayısını yerleştirmek için hedef.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı seçenek alma.  
- **NX_DHCP_NOT_BOUND**: (0x94) DHCP istemcisi bağlanmadı.
- **NX_DHCP_NO_INTERFACES_ENABLED**: (0xa5) DHCP için etkinleştirilen arabirim yok
- **NX_DHCP_DEST_TO_SMALL**: (0x95) hedef, yanıtı tutmak için çok küçük.
- **NX_DHCP_PARSE_ERROR**: (0x97) seçeneği sunucu yanıtında bulunamadı.
- NX_PTR_ERROR: (0x16) geçersiz giriş işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
UCHAR  dns_ip_string[4];
ULONG  size;

/* Obtain the IP address of the DNS server.  */
size =    sizeof(dnx_ip_string);
status =  nx_dhcp_user_option_retrieve(&my_dhcp, NX_DHCP_OPTION_DNS_SVR,
                                        dns_ip_string, &size);

/* If status is NX_SUCCESS the DNS IP address is in dns_ip_string.  */
```

## <a name="nx_dhcp_interface_user_option_retrieve"></a>nx_dhcp_interface_user_option_retrieve

Belirtilen arabirimdeki son sunucu yanıtından bir DHCP seçeneği alın

### <a name="prototype"></a>Prototype

```c
UINT nx_dhcp_interface_user_option_retrieve(NX_DHCP *dhcp_ptr,
                                            UINT interface_index,
                                            UINT request_option, UCHAR *destination_ptr,
                                            UINT *destination_size);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen arabirim DHCP için etkinleştirilirse belirtilen arabirimdeki DHCP seçenekleri arabelleğinden belirtilen DHCP seçeneğini alır. Başarılı olursa, seçenek verileri belirtilen arabelleğe kopyalanır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr**: daha önce oluşturulmuş DHCP örneğine yönelik işaretçi.
- **Interface_index**: belirtilen seçeneğin alınacağı dizin
- **request_option**: DHCP seçeneği, RFC 'ler tarafından belirtilen şekilde. NX_DHCP_OPTION seçeneğine bakın: *nxd_dhcp_client. h*.  
- **destination_ptr**: Yanıt dizesi için hedefin işaretçisi.  
- **destination_size**: hedefin boyutuna ve dönüşe ilişkin işaretçi, döndürülen bayt sayısını yerleştirmek için hedef.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı seçenek alma.  
- **NX_DHCP_NOT_BOUND**: (0x94) IP adresi atanmadı
- **NX_DHCP_DEST_TO_SMALL**: (0x95) arabellek çok küçük
- **NX_DHCP_PARSE_ERROR**: (0x97) DHCP seçeneği sunucu yanıtında bulunamadı.
- NX_PTR_ERROR: (0x16) geçersiz DHCP işaretçisi.
- NX_CALLER_ERROR: (0x11) geçersiz hizmet çağıranı.
- NX_INVALID_INTERFACE: (0x4C) geçersiz ağ arabirimi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
UCHAR  dns_ip_string[4];
ULONG  size;

/* Obtain the IP address of the DNS server on the prmary interface.  */
size =    sizeof(dnx_ip_string);
status =  nx_dhcp_interface_user_option_retrieve(&my_dhcp, 0, NX_DHCP_OPTION_DNS_SVR,
                                                  dns_ip_string, &size);

/* If status is NX_SUCCESS the DNS IP address is in dns_ip_string.  */
```

## <a name="nx_dhcp_user_option_convert"></a>nx_dhcp_user_option_convert

Dört baytı ULONG 'a Dönüştür

### <a name="prototype"></a>Prototype

```c
ULONG nx_dhcp_user_option_convert(UCHAR *option_string_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, "option_string_ptr" ile işaret edilen dört karakteri işaretsiz bir Long değere dönüştürür. Bu, özellikle IP adresleri olduğunda yararlıdır  
görüntülemeyen.

### <a name="input-parameters"></a>Giriş Parametreleri

- **option_string_ptr**: daha önce alınan seçenek dizesinin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **Değer**: ilk dört baytın değeri.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
UCHAR  dns_ip_string[4];
ULONG  dns_ip;

/* Convert the first four bytes of “dns_ip_string” to an actual IP
address in “dns_ip.”  */
dns_ip=  nx_dhcp_user_option_convert(dns_ip_string);

/* If status is NX_SUCCESS the DNS IP address is in “dns_ip.”  */
```

## <a name="nx_dhcp_user_option_add_callback_set"></a>nx_dhcp_user_option_add_callback_set

Kullanıcı tarafından sağlanan seçenekleri eklemek için geri çağırma işlevini ayarla

### <a name="prototype"></a>Prototype

```c
ULONG nx_dhcp_user_option_add_callbcak_set(NX_DHCP *dhcp_ptr, 
                                           UINT (*dhcp_user_option_add)(NX_DHCP *dhcp_ptr, 
                                                                        UINT iface_index, 
                                                                        UINT message_type, 
                                                                        UCHAR *user_option_ptr, 
                                                                        UINT *user_option_length));
```

### <a name="description"></a>Açıklama

Bu hizmet, Kullanıcı tarafından sağlanan seçenekleri eklemek için belirtilen geri çağırma işlevini kaydeder.

Geri çağırma işlevi belirtilmişse, uygulamalar iface_index ve message_type tarafından pakete Kullanıcı tarafından sağlanan seçenekleri ekleyebilir.

>[!NOTE] 
> Kullanıcı yordamında. Kullanıcı tarafından sağlanan seçenekler eklerken uygulamaların DHCP seçenekleri biçimi gelmelidir. Kullanıcı seçeneklerinin toplam boyutu user_option_length küçük veya eşit olmalı ve user_option_length gerçek seçenek uzunluğu olarak güncellenebilir. Seçenek başarıyla Ekle ' NX_TRUE döndürün, aksi NX_FALSE döndürün.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr**: daha önce oluşturulmuş DHCP örneğine yönelik işaretçi.
- **dhcp_user_option_add**: Kullanıcı seçeneği ekleme işlevi işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı geri arama kümesi.
- NX_PTR_ERROR: (0x16) geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Register the “my_dhcp_user_option_add” function to be called when add DHCP
options, assuming DHCP has already been created.  */

status =  nx_dhcp_user_option_add_callback_set(&my_dhcp, my_dhcp_user_option_add);

/* If status is NX_SUCCESS the callback function was successfully registered.  */

```

