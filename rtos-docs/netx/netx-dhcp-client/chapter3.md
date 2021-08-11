---
title: Bölüm 3 - NetX DHCP Azure RTOS hizmetlerinin açıklaması
description: Bu bölümde, tüm NetX DHCP Azure RTOS (aşağıda listelenmiştir) alfabetik sırada bir açıklama yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 50902d37f823302910b1b219658dcbf1a41406f480c14795ffceea6e733a0848
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116799549"
---
# <a name="chapter-3---description-of-azure-rtos-netx-dhcp-client-services"></a>Bölüm 3 - NetX DHCP Azure RTOS hizmetlerinin açıklaması

Bu bölümde, tüm NetX DHCP Azure RTOS (aşağıda listelenmiştir) alfabetik sırada bir açıklama yer almaktadır.

Aşağıdaki API açıklamalarında yer alan "Dönüş Değerleri" bölümünde, **KALıN**  olmayan değerler tamamen devre dışı bırakılırken, BOLD NX_DISABLE_ERROR_CHECKING API hata denetimlerini devre dışı bırakmak için kullanılan tanımdan etkilenmez.

- **nx_dhcp_create:** *DHCP örneği oluşturma*

- **nx_dhcp_clear_broadcast_flag:** İstemci iletisinde yayın bayrağını temizleme

- **nx_dhcp_delete:** DHCP *örneğini silme*

- **nx_dhcp_decline:** Reddetme *iletisi sunucuya gönder*

- **nx_dhcp_force_renew:** Zorla *yenileme iletisi gönderme*

- **nx_dhcp_packet_pool_set:** *DHCP İstemcisi paket havuzunu ayarlama*

- **nx_dhcp_release:** *Sunucuya Yayın iletisi gönderme*

- **nx_dhcp_reinitialize:** DHCP *istemci ağ parametrelerini temizleme*

- **nx_dhcp_request_client_ip:** Belirli *bir IP adresi belirtin*

- **nx_dhcp_send_request:** DHCP *iletisi sunucuya gönder*

- **nx_dhcp_server_address_get:** DHCP *İstemcisi'nin DHCP sunucu adresini alma*

- **nx_dhcp_set_interface_index:** İstemci *ağ arabirimini belirtin*

- **nx_dhcp_start:** *DHCP işlemeyi başlatma*

- **nx_dhcp_state_change_notify:** DHCP *durum değişikliğini uygulamaya bildirme*

- **nx_dhcp_stop:** DHCP *işlemeyi durdurma*

- **nx_dhcp_user_option_retrieve:** DHCP *alma seçeneği*

- **nx_dhcp_user_option_convert:** Dört *baytı ULONG'a dönüştür*

Arabirime özgü DHCP İstemcisi hizmetleri:

- **nx_dhcp_interface_clear_broadcast_flag:** Belirtilen *arabirimde İstemci iletisinde yayın bayrağını temizleme*

- **nx_dhcp_interface_enable:** Belirtilen *arabirimde DHCP çalıştırmak için arabirimi etkinleştirin*

- **nx_dhcp_interface_disable:** Belirtilen *arabirimde DHCP çalıştırmak için arabirimi devre dışı bırakma*

- **nx_dhcp_interface_decline:** *Belirtilen arabirimde sunucuya Reddetme iletisi gönderme*

- **nx_dhcp_interface_force_renew:** Belirtilen *arabirimde zorla yenileme iletisi gönderme*

- **nx_dhcp_interface_reinitialize:** Belirtilen *arabirimde DHCP istemci ağ parametrelerini temizleme*

- **nx_dhcp_interface_release:** *Belirtilen arabirimde sunucuya Yayın iletisi gönderme*

- **nx_dhcp_interface_request_client_ip:** Belirtilen *arabirimde belirli bir IP adresi belirtin*

- **nx_dhcp_interface_send_request:** *Belirtilen arabirimde sunucuya DHCP iletisi gönderme*

- **nx_dhcp_interface_server_address_get:** Belirtilen *arabirimde DHCP sunucusu IP adresini al*

- **nx_dhcp_interface_start:** Belirtilen *arabirimde DHCP İstemcisi işlemini başlatma*

- **nx_dhcp_interface_stop:** *Belirtilen arabirimde DHCP İstemcisi işlemini durdurun*

- **nx_dhcp_interface_state_change_notify:** *Belirtilen arabirimde DHCP durumu değişirken geri çağırma işlevini ayarlayın*

- **nx_dhcp_interface_user_option_retrieve:** *Belirtilen arabirimde belirtilen DHCP seçeneğini alın*

Dhcp İstemci Hizmetleri NX_DHCP_CLIENT_RESORE_STATE:

- **nx_dhcp_resume:** Daha *önce kurulan DHCP İstemcisi durumunu sürdür*

- **nx_dhcp_suspend:** *DHCP İstemcisi durumunu işlemeyi askıya alma*

- **nx_dhcp_client_get_record:** DHCP *İstemcisi durumunun kaydını oluşturma*

- **nx_dhcp_client_restore_record:** Daha *önce kaydedilmiş bir kaydı DHCP İstemcisi'ne geri yükleme*

- **nx_dhcp_client_update_time_remaining:** *Geçerli DHCP durumda kalan zamanı güncelleştirin*

Arabirim Tanımlı ise Arabirime NX_DHCP_CLIENT_RESORE_STATE DHCP İstemci Hizmetleri:

- **nx_dhcp_client_interface_get_record:** Belirtilen *arabirimde DHCP İstemcisi durumunun kaydını oluşturun*

- **nx_dhcp_client_interface_restore_record:** Belirtilen *arabirimde daha önce kaydedilmiş bir kaydı DHCP İstemcisi'ne geri yükleme*

- **nx_dhcp_client_interface_update_time_remaining:** Belirtilen *arabirimde geçerli DHCP durumda kalan zamanı güncelleştirin*

## <a name="nx_dhcp_create"></a>nx_dhcp_create

DHCP örneği oluşturma

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcp_create(NX_DHCP *dhcp_ptr, NX_IP *ip_ptr, CHAR *name_ptr);
```

### <a name="description"></a>Description

Bu hizmet, daha önce oluşturulan IP örneği için bir DHCP örneği oluşturur. Varsayılan olarak birincil arabirim DHCP'yi çalıştırmaya etkinleştirilir. DHCP İstemcisi'nin NetX uygulamasında kullanılmasa da ad girişi, konak adları için RFC 1035 ölçütlerini izlemeli. Toplam uzunluk 255 karakteri aşmamalıdır, noktalardan ayrı etiketler bir harfle başlamalıdır ve bir harf veya sayı ile bitmeli ve alfasayısal olmayan başka bir karakter yerine kısa çizgi içerebilir.

Uygulama, DHCP'yi IP örneğine kayıtlı başka bir arabirimi *(nx_ip_interface_attach* kullanarak) çalıştırmak isterse, uygulama DHCP'yi yalnızca bu arabirimde çalıştırmak için *nx_dhcp_set_interface_index'yi* veya DHCP'yi bu arabirimde *nx_dhcp_interface_enable* çalıştırmak için nx_dhcp_interface_enable'yi çağırabilirsiniz. Daha fazla ayrıntı için bu hizmetlerin açıklamasına bakın.

> [!NOTE]
> Uygulama, DHCP İstemcisi paket havuzu yükünün RFC 2131 Bölüm 2 (548 bayt DHCP ileti verileri artı UDP, IP ve fiziksel ağ çerçevesi üst bilgileri) tarafından belirtilen en düşük DHCP ileti boyutunu destekleyeneden emin olmalıdır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr** DHCP denetim bloğu işaretçisi.  
- **ip_ptr** Daha önce oluşturulan IP örneğinin işaretçisi.  
- **name_ptr** DHCP örneği için ana bilgisayar adı işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı DHCP oluşturma

- **NX_DHCP_INVALID_NAME** (0xA8) Geçersiz ana bilgisayar adı

- **NX_DHCP_INVALID_PAYLOAD** (0x9C) Yükü DHCP iletisi için çok küçük

- NX_PTR_ERROR (0x16) Geçersiz IP veya DHCP işaretçisi

### <a name="allowed-from"></a>İzin Verilen

**İş parçacıkları,** Başlatma

### <a name="example"></a>Örnek

```C
/* Create a DHCP instance. */
status =  nx_dhcp_create(&my_dhcp, &my_ip, "My-DHCP");

/* If status is NX_SUCCESS a DHCP instance was successfully created. */
```

## <a name="nx_dhcp_interface_enable"></a>nx_dhcp_interface_enable

DHCP'yi çalıştırmak için belirtilen arabirimi etkinleştirme 

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcp_interface_enable(NX_DHCP *dhcp_ptr, UINT interface_index);
```

### <a name="description"></a>Description

Bu hizmet, DHCP'yi çalıştırma için belirtilen arabirimi sağlar. Birincil arabirim varsayılan olarak DHCP İstemcisi için etkindir. Bu noktada, DHCP bu arabirimde nx_dhcp_interface_start *çağrılarak* veya dhcp'yi tüm etkin arabirimlerde başlatarak *nx_dhcp_start.*

Uygulamanın önce bu arabirimi ip örneğine kaydetmesi gerektiğini unutmayın ve *nx_ip_interface_attach.*

Ayrıca, bu arabirimi etkin arabirimler listesine eklemek için kullanılabilir bir DHCP İstemci arabirimi 'kaydı' olmalıdır. Varsayılan olarak NX_DHCP_CLIENT_MAX_RECORDS 1 olarak tanımlanır. Bu seçeneği DHCP İstemcisi'nin aynı anda çalışması beklenen en fazla arabirim sayısına ayarlayın. Genellikle NX_DHCP_CLIENT_MAX_RECORDS eşit NX_MAX_PHYSICAL_INTERFACES; ancak, bir cihaz DHCP İstemcisi'nin çalıştırmasını beklediğinizden daha fazla fiziksel arabirime sahipse, cihaz bu sayıdan NX_DHCP_CLIENT_MAX_RECORDS ayar NX_DHCP_CLIENT_MAX_RECORDS bellek kaydedebilir. DHCP İstemcisi arabirim kayıtlarıyla fiziksel arabirimlerin bire bir eşlemesi yok.

Bu hizmetle nx_dhcp_set_interface_index  arasındaki fark, ikincinin DHCP'yi çalıştırmak için yalnızca tek bir arabirim ayarlarken, bu hizmet yalnızca belirtilen arabirimi DHCP için etkinleştirilmiş İstemci arabirimleri listesine ekler.

Uygulama, DHCP arabirimini devre dışı  bırakmak için nx_dhcp_interface_disable çağırabilirsiniz.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr** DHCP denetim bloğu işaretçisi.  

- **interface_index** DHCP'yi etkinleştirmek için arabirim dizini

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı DHCP etkinleştirmesi

- **NX_DHCP_NO_RECORDS_AVAILABLE** (0xA7) DHCP için başka bir Arabirimin etkinleştirilmesi için kayıt yok

- **NX_DHCP_INTERFACE_ALREADY_ENABLED** (0xA3) Arabirimi DHCP için etkinleştirildi

- NX_PTR_ERROR (0x16) Geçersiz IP veya DHCP işaretçisi

- NX_INVALID_INTERFACE (0x4C) Geçersiz ağ arabirimi

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları, Başlatma

### <a name="example"></a>Örnek

```C
/* Enable DHCP on a secondary interface. It is already enabled on the primary 
   interface. NX_DHCP_CLIENT_MAX_RECORDS is set to 2. */

status =  nx_dhcp_interface_enable(&my_dhcp, 1);
/* If status is NX_SUCCESS the interface was successfully enabled. */


status = nx_dhcp_start(&my_dhcp);
/* If status is NX_SUCCESS DHCP is running on interface 0 and 1. */
```

## <a name="nx_dhcp_interface_disable"></a>nx_dhcp_interface_disable

DHCP çalıştırmak için belirtilen arabirimi devre dışı bırakma 

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcp_interface_disable(NX_DHCP *dhcp_ptr,
                                UINT interface_index);
```

### <a name="description"></a>Description

Bu hizmet, DHCP'yi çalıştırma için belirtilen arabirimi devre dışı bırakıyor. Bu arabirimde DHCP İstemcisi'nin yeniden ilkini sağlar.

DHCP İstemcisini yeniden başlatmak için, uygulamanın nx_dhcp_interface_enable kullanarak arabirimi yeniden etkinleştirmesi *ve* dhcp'yi *nx_dhcp_interface_start.*

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr** DHCP denetim bloğu işaretçisi.  

- **interface_index** DHCP'yi devre dışı bırakmak için arabirim dizini

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı DHCP oluşturma

- **NX_DHCP_INTERFACE_NOT_ENABLED** (0xA4) Arabirimi DHCP için etkinleştirilmedi

- NX_PTR_ERROR (0x16) Geçersiz IP veya DHCP işaretçisi

- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz

- NX_INVALID_INTERFACE (0x4C) Geçersiz ağ arabirimi

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Disable DHCP on a secondary interface.
. */

status = nx_dhcp_interface_disable(&my_dhcp, 1);
/* If status is NX_SUCCESS the interface is successfully disabled. */
```

## <a name="nx_dhcp_clear_broadcast_flag"></a>nx_dhcp_clear_broadcast_flag

DHCP yayın bayrağını ayarlama

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcp_clear_broadcast_flag(NX_DHCP *dhcp_ptr, UINT clear_flag);
```

### <a name="description"></a>Description

Bu hizmet, DHCP için etkinleştirilmiş tüm arabirimler için DHCP ileti üst bilgisi yayın bayrağını ayarlar veya temizler. Bazı DHCP iletileri (örneğin DISCOVER) için, İstemcinin bir IP adresi yoksa yayın bayrağı yayına ayarlanır.

__clear_flag__


- **NX_TRUE** bayrağı temizlenmiştir (tek noktaya yayın yanıtı isteği)

- **NX_FALSE** bayrağı ayarlanmıştır (yayın yanıtı isteği)

Bu hizmet, yönlendiricinin yayın iletilerini iletmeyi reddederek DHCP Sunucusuna gitmek için bir yönlendiriciden geçen DHCP İstemcilerine yöneliktir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr** DHCP denetim bloğu işaretçisi  

- **clear_flag** Yayın bayrağını ayarlanacak değer

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Yayın bayrağı başarıyla güncelleştirildi

- NX_PTR_ERROR (0x16) Geçersiz IP veya DHCP işaretçisi

- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları, Başlatma

### <a name="example"></a>Örnek

```C
/* Send DHCP Client messages with the broadcast flag cleared (e.g. request a  
    unicast response). */
status =  nx_dhcp_clear_broadcast_flag(&my_dhcp, NX_TRUE);

/* If status is NX_SUCCESS the DHCP Client broadcast flag is updated. */
```

## <a name="nx_dhcp_interface_clear_broadcast_flag"></a>nx_dhcp_interface_clear_broadcast_flag

Belirtilen arabirimde yayın bayrağını ayarlama veya temizleme

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcp_interface_clear_broadcast_flag(NX_DHCP *dhcp_ptr,
                                            UINT interface_index,
                                            UINT clear_flag);
```

### <a name="description"></a>Description

Bu hizmet, DHCP İstemcisi konak uygulamasının DHCP İstemcisi iletisinde yayın bayrağını belirtilen arabirimde DHCP Sunucusuna ayarlamasını veya temizlemesini sağlar. Diğer ayrıntılar için **bkz. nx_dhcp_clear_broadcast_flag**

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr** DHCP denetim bloğu işaretçisi

- **interface_index** Yayın bayrağını ayarlamak için arabirim dizini  

- **clear_flag** Yayın bayrağını ayarlanacak değer

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Yayın bayrağı başarıyla güncelleştirildi

- **NX_DHCP_INTERFACE_NOT_ENABLED** (0xA4) Arabirimi DHCP için etkinleştirilmedi

- NX_PTR_ERROR (0x16) Geçersiz IP veya DHCP işaretçisi

- NX_INVALID_INTERFACE (0x4C) Geçersiz ağ arabirimi

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları, Başlatma

### <a name="example"></a>Örnek

```C
/* Send DHCP Client messages with the broadcast flag cleared (e.g. request a 
   unicast response) on a previously attached secondary interface. */

iface_index = 1;

status =  nx_dhcp_interface_clear_broadcast_flag(&my_dhcp, iface_index, NX_TRUE);

/* If status is NX_SUCCESS the DHCP Client broadcast flag is updated. */
```

## <a name="nx_dhcp_delete"></a>nx_dhcp_delete

DHCP örneğini silme

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcp_delete(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a>Description

Bu hizmet, önceden oluşturulmuş bir DHCP örneğini siler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr** Daha önce oluşturulan DHCP örneğinin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) DHCP silme başarılı.

- NX_PTR_ERROR (0x16) Geçersiz DHCP işaretçisi.

- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Delete a DHCP instance. */
status =  nx_dhcp_delete(&my_dhcp);

/* If status is NX_SUCCESS the DHCP instance was successfully deleted. */
```

## <a name="nx_dhcp_-force_renew"></a>nx_dhcp_ force_renew

Zorla yenileme iletisi gönderme 

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcp force_renew(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a>Description

Bu hizmet, konak uygulamanın DHCP için etkinleştirilmiş tüm arabirimlerde zorla yenileme iletisi göndermesini sağlar. DHCP İstemcisi BOUND durumda olması gerekir. Bu işlev, dhcp istemcisinin T1 zaman aşımı süresi dolmadan önce yenilemeyi deneyecek şekilde durumu YenİLEME olarak ayarlar.

Birden çok arabirim DHCP etkin olduğunda belirli bir arabirimde zorla yenileme göndermek için, *nx_dhcp_interface_force_renew.*

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr** Daha önce oluşturulan DHCP örneğinin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Zorla yenileme başarıyla gönderildi.  

- NX_PTR_ERROR (0x16) Geçersiz DHCP işaretçisi.

- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Send a force renew message from the Client. */
status =  nx_dhcp_force_renew(&my_dhcp);

/* If status is NX_SUCCESS the DHCP client state is the RENEWING state and the    
   DHCP Client thread task will begin renewing before T1 is expired. */
```

## <a name="nx_dhcp_interface_force_renew"></a>nx_dhcp_interface_force_renew

Belirtilen arabirimde zorla yenileme iletisi gönderme

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcp_interface_force_renew(NX_DHCP *dhcp_ptr,
                                    UINT interface_index);
```

### <a name="description"></a>Description

Bu hizmet, ana bilgisayar uygulamasının DHCP için etkinleştirilmiş olduğu sürece giriş arabiriminde zorla yenileme iletisi göndermesini sağlar (bkz. *nx_dhcp_interface_enable).* Belirtilen arabirimde DHCP İstemcisi BOUND durumda olması gerekir. Bu işlev, dhcp istemcisinin T1 zaman aşımı süresi dolmadan önce yenilemeyi deneyecek şekilde durumu YenİLEME olarak ayarlar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr** Daha önce oluşturulan DHCP örneğinin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Zorla yenileme başarıyla gönderildi.  

- **NX_DHCP_INTERFACE_NOT_ENABLED**  (0xA4) Arabirimi DHCP için etkinleştirilmedi

- NX_PTR_ERROR (0x16) Geçersiz IP veya DHCP işaretçisi

- NX_INVALID_INTERFACE (0x4C) Geçersiz ağ arabirimi

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Send a force renew message to the server on interface 1. */
status =  nx_dhcp_interface_force_renew(&my_dhcp, 1);

/* If status is NX_SUCCESS the DHCP client state is the RENEWING state and the    
   DHCP Client thread task will begin renewing before T1 is expired. */
```

## <a name="nx_dhcp_packet_pool_set"></a>nx_dhcp_packet_pool_set

DHCP İstemcisi paket havuzunu ayarlama

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcp_packet_pool_set(NX_DHCP *dhcp_ptr,
                            NX_PACKET_POOL *packet_pool_ptr);
```

### <a name="description"></a>Description

Bu hizmet, uygulamanın bu hizmet çağrısında önceden oluşturulmuş bir paket havuzuna bir işaretçi geçerek DHCP İstemcisi paket havuzunu oluşturmasını sağlar. Bu özelliği kullanmak için konak uygulamanın bu özelliği NX_DHCP_CLIENT_USER_CREATE_PACKET_POOL. Tanımlandığı *zaman, nx_dhcp_create* hizmeti İstemcinin paket havuzunu oluşturmaz. Uygulamanın, paket havuzunu oluştururken *nx_dhcp.h'de* NX_DHCP_PACKET_PAYLOAD olarak tanımlanan DHCP istemci paket havuzu yükü için varsayılan değerlerin kullanılması önerilir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr** DHCP denetim bloğu işaretçisi.  

- **packet_pool_ptr** Daha önce oluşturulan paket havuzunun işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) DHCP İstemcisi paket havuzu ayarlanmış

- **NX_NOT_ENABLED** (0x14) Hizmeti etkinleştirilmedi

- NX_PTR_ERROR (0x16) Geçersiz DHCP işaretçisi

- NX_DHCP_INVALID_PAYLOAD (0x9C) Yük çok küçük

### <a name="allowed-from"></a>İzin Verilen

Uygulama kodu

### <a name="example"></a>Örnek

```C
/* Create the packet pool. */
status =  nx_packet_pool_create(&dhcp_pool, "DHCP Client Packet Pool", 
        NX_DHCP_PACKET_PAYLOAD, pointer, (15 * NX_DHCP_PACKET_PAYLOAD));

/* Create the DHCP Client. */
status =  nx_dhcp_create(&dhcp_0, &ip_0, "janetsdhcp1");

/* Set the DHCP Client packet pool. */
status =  nx_dhcp_packet_pool_set(&my_dhcp, packet_pool_ptr);
/* If status is NX_SUCCESS packet pool was successfully set. */
```

## <a name="nx_dhcp_request_client_ip"></a>nx_dhcp_request_client_ip

DHCP örneği için istenen IP adresini ayarlama

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcp_request_client_ip(NX_DHCP *dhcp_ptr,
                                ULONG client_ip_address,
                                UINT skip_discover_message);
```

### <a name="description"></a>Description

Bu hizmet, DHCP İstemcisi kaydında DHCP için etkinleştirilmiş ilk arabirimde DHCP Sunucusundan istekte etmek için DHCP İstemcisi'nin IP adresini ayarlar. İstemci *skip_discover_message* ayarlanırsa, DHCP İstemcisi Bulma iletiyi atlar ve bir İstek iletisi gönderir.

Belirli bir arabirimde DHCP iletilerine yönelik belirli bir IP'ye yönelik isteği ayarlamak için nx_dhcp_interface_request_client_ip *kullanın.*

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr** DHCP denetim bloğu işaretçisi.  

- **client_ip_address** DHCP sunucusundan isteğin IP adresi

- **skip_discover_message** True ise, DHCP İstemcisi İstek iletisi gönderir  
False ise, Bulma iletisi gönderir.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) İstenen IP adresi ayarlanır.

- **NX_DHCP_INTERFACE_NOT_ENABLED** (0xA4) Arabirimi DHCP için etkinleştirilmedi

- NX_PTR_ERROR (0x16) Geçersiz IP veya DHCP işaretçisi

- NX_INVALID_INTERFACE (0x4C) Geçersiz ağ arabirimi
 
### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Set the DHCP Client requested IP address and skip the discover message. */

status =  nx_dhcp_request_client_ip(&my_dhcp, IP(192,168,0,6), NX_TRUE);

/* If status is NX_SUCCESS requested IP address was successfully set. */
```

## <a name="nx_dhcp_interface_request_client_ip"></a>nx_dhcp_interface_request_client_ip

Belirtilen arabirimde DHCP örneği için istenen IP adresini ayarlama

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcp_interface_request_client_ip(NX_DHCP *dhcp_ptr,
                                        UINT interface_index,
                                        ULONG client_ip_address,
                                        UINT skip_discover_message);
```

### <a name="description"></a>Description

Bu hizmet, belirtilen arabirimde DHCP için etkinleştirilmişse DHCP İstemcisi'nin BELIRTILEN arabirimde DHCP Sunucusundan istekte bulunduracak IP adresini ayarlar (bkz. *nx_dhcp_interface_enable).* İstemci *skip_discover_message* ayarlanırsa, DHCP İstemcisi Bulma iletiyi atlar ve bir İstek iletisi gönderir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr** DHCP denetim bloğu işaretçisi.

- **Interface_index** ÜZERINDE IP adresi isteğinde olacak arabirim dizini

- **client_ip_address** DHCP sunucusundan isteğin IP adresi

- **skip_discover_message** True ise, DHCP İstemcisi İstek iletisi gönderir; yoksa Bulma iletisi gönderir.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) İstenen IP adresi ayarlanır.

- **NX_DHCP_INTERFACE_NOT_ENABLED** (0xA4) Arabirimi DHCP için etkinleştirilmedi

- NX_PTR_ERROR (0x16) Geçersiz IP veya DHCP işaretçisi

- NX_INVALID_INTERFACE (0x4C) Geçersiz ağ arabirimi


### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Set the DHCP Client requested IP address and skip the discover message on  
   interface 0. */
status =  nx_dhcp_interface_request_client_ip(&my_dhcp, 0, IP(192,168,0,6), NX_TRUE);

/* If status is NX_SUCCESS requested IP address was successfully set. */
```

## <a name="nx_dhcp_reinitialize"></a>nx_dhcp_reinitialize

DHCP istemci ağ parametrelerini temizleme 

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcp_reinitialize(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a>Description

Bu hizmet, konak uygulama ağ parametrelerini (IP adresi, ağ adresi ve ağ maskesi) temizler ve DHCP için etkinleştirilmiş tüm arabirimlerde DHCP İstemcisi durumunu temizler. DHCP durum makinesini *'nx_dhcp_stop'* *nx_dhcp_start'a* yüklemek için aşağıdakilerle birlikte kullanılır: 

nx_dhcp_stop(&my_dhcp);  
nx_dhcp_reinitialize(&my_dhcp);  
nx_dhcp_start(&my_dhcp);


DHCP için birden çok arabirim etkinleştirildiğinde DHCP İstemcisini belirli bir arabirimde yeniden nx_dhcp_interface_reinitialize *kullanın.*

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr** Daha önce oluşturulan DHCP örneğinin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) DHCP başarıyla yeniden başlatıldı 

- NX_PTR_ERROR (0x16) Geçersiz DHCP işaretçisi

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Reinitialize the previously started DHCP client. */
status =  nx_dhcp_reinitialize(&my_dhcp);

/* If status is NX_SUCCESS the host application successfully reinitialized its 
network parameters and DHCP client state. */
```

## <a name="nx_dhcp_interface_reinitialize"></a>nx_dhcp_interface_reinitialize

Belirtilen arabirimde DHCP istemci ağ parametrelerini temizleme 

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcp_interface_reinitialize(NX_DHCP *dhcp_ptr,
                                    UINT interface_index);
```

### <a name="description"></a>Description

Bu hizmet, bu arabirim DHCP için etkinleştirildiyse belirtilen arabirimde ağ parametrelerini (IP adresi, ağ adresi ve ağ maskesi) temizler (bkz. *nx_dhcp_interface_enable).* Diğer *nx_dhcp_reinitialize* için bkz.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr** Daha önce oluşturulan DHCP örneğinin işaretçisi

- **interface_index** Yeniden oluşturma arabirimi dizini.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Arabirimi başarıyla yeniden başlatıldı

- **NX_DHCP_INTERFACE_NOT_ENABLED** (0xA4) Arabirimi DHCP için etkinleştirilmedi

- NX_PTR_ERROR (0x16) Geçersiz DHCP işaretçisi

- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz.

- NX_INVALID_INTERFACE (0x4C) Geçersiz ağ arabirimi

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Reinitialize the previously started DHCP client on interface 1. */
status =  nx_dhcp_interface_reinitialize(&my_dhcp, 1);

/* If status is NX_SUCCESS the host application successfully reinitialized its 
network parameters and DHCP client state. */
```

## <a name="nx_dhcp_release"></a>nx_dhcp_release

Kiralanan IP adresini serbest bırakma

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcp_release(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a>Description

Bu hizmet, YAYıN iletiyi bu sunucuya göndererek DHCP sunucusundan alınan IP adresini serbest bıraktır. Ardından DHCP İstemcisi'nin yeniden ilkini sağlar. Bu hizmet, DHCP için etkinleştirilmiş tüm arabirimlere uygulanır.

Uygulama, dhcp istemcisini çağırarak DHCP İstemcisini *nx_dhcp_start.*

Bir adresi belirli bir arabirimde DHCP sunucusuna geri serbest bırakmak için nx_dhcp_interface_release *kullanın*

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr** Daha önce oluşturulan DHCP örneğinin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Dhcp sürümü.  

- **NX_DHCP_NOT_BOUND** (0x94) IP adresi serbest bırakılamay için kiralanmaz.

- NX_PTR_ERROR (0x16) Geçersiz DHCP işaretçisi.

- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Release the previously leased IP address. */
status =  nx_dhcp_release(&my_dhcp);

/* If status is NX_SUCCESS the previous IP lease was successfully released. */
```

## <a name="nx_dhcp_interface_release"></a>nx_dhcp_interface_release

Belirtilen arabirimde IP adresini serbest bırakma

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcp_interface_release(NX_DHCP *dhcp_ptr,
                                UINT interface_index);
```

### <a name="description"></a>Description

Bu hizmet, belirtilen arabirimde bir DHCP sunucusundan alınan IP adresini serbest bırakarak DHCP İstemcisini yeniden verir. DHCP İstemcisi, nx_dhcp_start *çağrılarak yeniden nx_dhcp_start.*

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr** Daha önce oluşturulan DHCP örneğinin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Dhcp sürümü.

- **NX_DHCP_INTERFACE_NOT_ENABLED** (0xA4) Arabirimi DHCP için etkinleştirilmedi

- **NX_DHCP_NOT_BOUND** (0x94) IP adresi serbest bırakılamay için kiralanmaz.

- NX_PTR_ERROR (0x16) Geçersiz DHCP işaretçisi

- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz.

- NX_INVALID_INTERFACE (0x4C) Geçersiz ağ arabirimi

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Release the previously leased IP address on interface 1. */
status =  nx_dhcp_interface_release(&my_dhcp, 1);

/* If status is NX_SUCCESS the previous IP lease was successfully released. */
```

## <a name="nx_dhcp_decline"></a>nx_dhcp_decline

DHCP Sunucusundan IP adresini reddetme

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcp_decline(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a>Description

Bu hizmet, DHCP için etkinleştirilmiş tüm arabirimlerde DHCP sunucusundan kiralanan bir IP adresini reddeder. Bu NX_DHCP_CLIENT_ SEND_ ARP_PROBE tanımlanmışsa, IP adresinin zaten kullanımda olduğunu algılarsa DHCP İstemcisi bir REDDETME iletisi gönderir. NetX DHCP **İstemcisi'nin** ARP yoklama yapılandırması hakkında daha fazla bilgi için Birinci Bölümdeki ARP Araştırmaları'ne bakın.

Uygulama, adresin başka bir şekilde kullanımda olduğunu fark ettiyse IP adresini reddetmek için bu hizmeti kullanabilir.

Bu hizmet, DHCP İstemcisi'nin nx_dhcp_start çağrılarak yeniden *başlatıla nx_dhcp_start.*

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr** Daha önce oluşturulan DHCP örneğinin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarıyla gönderilen reddetme  

- **NX_DHCP_NOT_STARTED** (0x96) DHCP örneği başlamadı

- NX_PTR_ERROR (0x16) Geçersiz DHCP işaretçisi

- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Decline the IP address offered by the DHCP server. */
status =  nx_dhcp_decline(&my_dhcp);

/* If status is NX_SUCCESS the previous IP address decline message was 
   successfully trasnmitted. */
```

## <a name="nx_dhcp_interface_decline"></a>nx_dhcp_interface_decline

Belirtilen arabirimde DHCP Sunucusundan IP adresini reddetme

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcp_interface_decline(NX_DHCP *dhcp_ptr,
                                UINT interface_index);
```

### <a name="description"></a>Description

Bu hizmet, DHCP sunucusu tarafından atanan bir IP adresini reddetmek için SUNUCUYA REDDİsİ iletisi gönderir. Ayrıca DHCP İstemcisi'nin de yeniden ilkini sağlar. Diğer *nx_dhcp_decline* için bkz.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr** Daha önce oluşturulan DHCP örneğinin işaretçisi.

- **Interface_index** IP adresini reddetmek için arabirim dizini

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) DHCP reddetme iletisi gönderildi  

- **NX_DHCP_NOT_BOUND** (0x94) DHCP İstemcisi bağlı değil

- **NX_DHCP_INTERFACE_NOT_ENABLED** (0xA4) Arabirimi DHCP için etkinleştirilmedi

- NX_PTR_ERROR (0x16) Geçersiz DHCP işaretçisi

- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz.

- NX_INVALID_INTERFACE (0x4C) Geçersiz ağ arabirimi

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek
```C
/* Decline the IP address offered by the DHCP server on interface 2. */
status =  nx_dhcp_interface_decline(&my_dhcp, 2);

/* If status is NX_SUCCESS the previous IP address decline message was
   successfully trasnmitted. */
```

## <a name="nx_dhcp_send_request"></a>nx_dhcp_send_request

Sunucuya DHCP iletisi gönderme

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcp_send_request(NX_DHCP *dhcp_ptr, UINT dhcp_message_type);
```

### <a name="description"></a>Description

Bu hizmet, belirtilen DHCP iletiyi DHCP İstemci kaydında bulunan DHCP için etkinleştirilmiş ilk arabirimde DHCP sunucusuna gönderir. YAYıN veya REDDIZ iletisi göndermek için uygulamanın *sırasıyla nx_dhcp[_interface]_release*() veya *nx_dhcp_interface_decline() hizmetlerini* kullanması gerekir.

DHCP İstemcisi, bu hizmeti kullanmak için, etki alanı ileti türünü INFORM_REQUEST başlat gerekir.

> [!NOTE] 
> Bu hizmet, konak uygulamanın DHCP İstemcisi durum makinesini "sürücüsüne" yönelik değildir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr** DHCP denetim bloğu işaretçisi.  

- **dhcp_message_type** İleti isteği *(nx_dhcp.h içinde tanımlanır)*

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) DHCP iletisi gönderildi  

- **NX_DHCP_NOT_STARTED** (0x96) Geçersiz arabirim dizini

- **NX_DHCP_INVALID_MESSAGE** (0x9B) Göndermek için geçersiz ileti türü

- NX_PTR_ERROR (0x16) Geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Send the DHCP INFORM REQUEST message to the server. */

status =  nx_dhcp_send_request(&my_dhcp, NX_DHCP_TYPE_DHCPINFORM);
/* If status is NX_SUCCESS a DHCP message was successfully sent. */
```

## <a name="nx_dhcp_interface_send_request"></a>nx_dhcp_interface_send_request

Belirli bir arabirimde Sunucuya DHCP iletisi gönderme

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcp_interface_send_request(NX_DHCP *dhcp_ptr,
                                    UINT interface_index,
                                    UINT dhcp_message_type);
```

### <a name="description"></a>Description

Bu hizmet, bu arabirim DHCP için etkinleştirilmişse belirtilen arabirimde DHCP sunucusuna bir ileti gönderir. YAYıN veya REDDIZ iletisi göndermek için uygulamanın *sırasıyla nx_dhcp[_interface]_release*() veya *nx_dhcp_interface_decline() hizmetlerini* kullanması gerekir.

DHCP INFORM REQUEST ileti türünü göndermek dışında, DHCP İstemcisi bu hizmeti kullanmak üzere başlatıladır.

Bu hizmet, konak uygulamanın DHCP İstemcisi durum makinesini "sürücüsüne" yönelik değildir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr** DHCP denetim bloğu işaretçisi.

- **Interface_index** İleti göndermek için arabirim dizini  

- **dhcp_message_type** İleti isteği *(nx_dhcp.h içinde tanımlanır)*

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) DHCP iletisi gönderildi  

- **NX_DHCP_NOT_STARTED** (0x96) Geçersiz arabirim dizini

- **NX_DHCP_INVALID_MESSAGE** (0x9B) Göndermek için geçersiz ileti türü

- **NX_DHCP_INTERFACE_NOT_ENABLED** (0xA4) Arabirimi DHCP için etkinleştirilmedi

- NX_PTR_ERROR (0x16) Geçersiz DHCP işaretçisi

- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz.

- NX_INVALID_INTERFACE (0x4C) Geçersiz ağ arabirimi

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Send the INFORM REQUEST message to the server on the primary interface. */

status =  nx_dhcp_interface_send_request(&my_dhcp, 0, NX_DHCP_TYPE_DHCPINFORM);
/* If status is NX_SUCCESS a DHCP message was successfully sent. */
```

## <a name="nx_dhcp_server_address_get"></a>nx_dhcp_server_address_get

DHCP İstemcisi'nin DHCP sunucusu IP adresini al

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcp_server_address_get(NX_DHCP *dhcp_ptr,
                                ULONG server_address);
```

### <a name="description"></a>Description

Bu hizmet, DHCP İstemcisi kaydında bulunan DHCP için etkinleştirilmiş ilk arabirimde DHCP İstemcisi DHCP sunucusu IP adresini verir. Çağıran bu hizmeti yalnızca DHCP İstemcisi DHCP Sunucusu tarafından atanan bir IP adresine bağlandikten sonra kullanabilir. Konak uygulama IP *adresinin ayar nx_ip_status_check* için nx_ip_status_check hizmetini kullanabilir veya ip adresini kullanarak DHCP *nx_dhcp_state_change_notify* durumunu sorgu NX_DHCP_STATE_BOUND. Durum *nx_dhcp_state_change_notify* işlevini ayarlama hakkında daha fazla bilgi için bkz. nx_dhcp_state_change_notify.

DHCP İstemcisi için birden çok arabirim etkinleştirildiğinde belirli bir arabirimde DHCP sunucusunu bulmak için, dhcp *nx_dhcp_interface_server_address_get* kullanın

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr** DHCP denetim bloğu işaretçisi.

- **server_address** Sunucu IP adresi işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) DHCP sunucusu adresi döndürüldü

- NX_PTR_ERROR (0x16) Geçersiz giriş işaretçisi

- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Use the state change notify service to determine the Client transition to the 
bound state and get its DHCP server IP address. 
/* void dhcp_state_change(NX_DHCP *dhcp_ptr, UCHAR new_state)
{

ULONG server_address;
UINT  status;

/* Increment state changes counter. */
    state_changes++;

    if (dhcp_0.nx_dhcp_state == NX_DHCP_STATE_BOUND)
    {
            status = nx_dhcp_server_address_get(&dhcp_0, &server_address);
    }
```

## <a name="nx_dhcp_interface_server_address_get"></a>nx_dhcp_interface_server_address_get

Belirtilen arabirimde DHCP İstemcisi'nin DHCP sunucusu IP adresini al

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcp_interface_server_address_get(NX_DHCP *dhcp_ptr,
                                            UINT interface_index,
                                            ULONG server_address);
```

### <a name="description"></a>Description

Bu hizmet, bu arabirim DHCP için etkinleştirilmişse belirtilen arabirimde DHCP İstemcisi DHCP sunucusu IP adresini verir. DHCP İstemcisi Bağlı durumda olması gerekir. Bu arabirimde DHCP İstemcisi'ne başladıktan sonra, konak uygulama IP adresinin ayar olduğunu doğrulamak için *nx_ip_status_check* hizmetini kullanabilir veya DHCP İstemcisi durum değişikliği geri aramasını kullanabilir ve DHCP İstemcisi durumunun NX_DHCP_STATE_BOUND. Durum *nx_dhcp_state_change_notify* işlevini ayarlama hakkında daha fazla bilgi için bkz. nx_dhcp_state_change_notify.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr** DHCP denetim bloğu işaretçisi.

- **Interface_index** IP adresi almak için arabirim dizini  

- **server_address** Sunucu IP adresi işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) DHCP sunucusu adresi döndürüldü

- **NX_DHCP_NO_INTERFACES_ENABLED** (0xA5) DHCP için etkinleştirilmiş arabirim yok

- **NX_DHCP_NOT_BOUND** (0x94) DHCP İstemcisi bağlı değil

- NX_PTR_ERROR (0x16) Geçersiz DHCP işaretçisi

- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz.

- NX_INVALID_INTERFACE (0x4C) Geçersiz ağ arabirimi

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Use the state change notify service to determine the Client transition to the 
bound state and get its DHCP server IP address. 
/* void dhcp_state_change(NX_DHCP *dhcp_ptr, UCHAR new_state)
{

ULONG server_address;
UINT  status;

/* Increment state changes counter. */
    state_changes++;

    /* Get the DHCP server IP address on interface 1 */
    if (dhcp_0.nx_dhcp_state == NX_DHCP_STATE_BOUND)
    {
            status = nx_dhcp_interface_server_address_get(&dhcp_0, 1, 
                                                    &server_address);
    }
```

## <a name="nx_dhcp_set_interface_index"></a>nx_dhcp_set_interface_index

DHCP örneği için ağ arabirimi ayarlama

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcp_set_interface_index(NX_DHCP *dhcp_ptr, UINT index);
```

### <a name="description"></a>Description

Bu hizmet, tek bir ağ arabirimi için yapılandırılmış DHCP İstemcisi'nin çalıştırıldığında DHCP sunucusuna bağlanmak üzere DHCP örneğinin ağ arabirimini ayarlar.

Varsayılan olarak DHCP İstemcisi birincil arabirimde çalışır. DHCP'yi ikincil bir hizmette çalıştırmak için bu hizmeti kullanarak ikincil arabirimi DHCP İstemci arabirimi olarak ayarlayın. Uygulamanın daha önce nx_ip_interface_attach hizmetini kullanarak belirtilen arabirimi IP *örneğine nx_ip_interface_attach* gerekir.

Bu hizmetin DHCP İstemcisini yalnızca bir arabirimde çalıştırmayı amaçlanan uygulamalara yönelik olduğunu unutmayın. DHCP'yi birden çok arabirimde çalıştırmak için *nx_dhcp_interface_enable* için bkz. Dhcp.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr** DHCP denetim bloğu işaretçisi.  

- **dizin** Cihaz ağ arabirimi dizini

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Arabirimi başarıyla ayarlanır.

- **NX_INVALID_INTERFACE** (0x4C) Geçersiz ağ arabirimi

- **NX_DHCP_INTERFACE_ALREADY_ENABLED** (0xA3) Arabirimi DHCP için etkinleştirildi

- **NX_DHCP_NO_RECORDS_AVAILABLE** (0xA7) Başka bir kayıt kullanılamaz

- NX_PTR_ERROR (0x16) Geçersiz DHCP işaretçisi

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Set the DHCP Client interface to the secondary interface (index 1). */
status =  nx_dhcp_set_interface_index(&my_dhcp, 1);
/* If status is NX_SUCCESS a DHCP interface was successfully set. */
```

## <a name="nx_dhcp_start"></a>nx_dhcp_start

DHCP işlemeyi başlatma

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcp_start(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a>Description

Bu hizmet, DHCP için etkinleştirilmiş tüm arabirimlerde DHCP işlemeyi başlatır. Varsayılan olarak, uygulama dhcp'yi çağıran birincil arabirim *nx_dhcp_create.*

IP örneğinin DHCP İstemci arabiriminde bir IP adresine ne zaman bağlı olduğunu doğrulamak için ip *nx_ip_status_check* ip adresinin geçerli olduğunu doğrulamak için ip adresini kullanın.

ZATEN DHCP çalıştıran başka arabirimler varsa, bu hizmet bunları etkilemez.

Birden çok arabirim etkinleştirildiğinde DHCP'yi belirli bir arabirimde başlatmak için nx_dhcp_interface_start *kullanın.*

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr** Daha önce oluşturulan DHCP örneğinin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) DHCP başlangıcı.  

- **NX_DHCP_ALREADY_STARTED** (0x93) DHCP zaten başlatıldı.

- NX_PTR_ERROR (0x16) Geçersiz DHCP işaretçisi.

- NX_CALLER_ERROR (0x11) Geçersiz hizmet çağıranı.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Start the DHCP processing for this IP instance. */
status =  nx_dhcp_start(&my_dhcp);

/* If status is NX_SUCCESS the DHCP was successfully started. */
```

## <a name="nx_dhcp_interface_start"></a>nx_dhcp_interface_start

Belirtilen arabirimde DHCP işlemeyi başlatma

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcp_interface_start(NX_DHCP *dhcp_ptr, UINT interface_index);
```

### <a name="description"></a>Description

Bu hizmet, bu arabirim DHCP için etkinleştirilmişse, belirtilen arabirim üzerinde DHCP işlemi başlatır. DHCP için bir arabirim etkinleştirme hakkında daha fazla ayrıntı için bkz. *nx_dhcp_interface_enable*(). Varsayılan olarak, uygulama nx_dhcp_create çağırdığında, birincil arabirim DHCP için etkinleştirilir *.*

DHCP Istemcisi çalıştıran başka arabirim yoksa, bu hizmet DHCP istemci iş parçacığını başlatır/sürdürür ve (yeniden) DHCP Istemci zamanlayıcısını etkinleştirir.  
  
Uygulamanın bir IP adresinin elde olup olmadığını doğrulamak için *nx_ip_status_check* kullanması gerekir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr** Daha önce oluşturulan DHCP örneğine yönelik işaretçi.

- **Interface_index** DHCP Istemcisinin başlatılacağı Dizin

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı DHCP başlatması.  

- **NX_DHCP_ALREADY_STARTED** (0x93) DHCP örneği zaten başlatılmış.

- NX_PTR_ERROR (0x16) geçersiz DHCP işaretçisi.

- NX_CALLER_ERROR (0x11) geçersiz hizmet çağıranı.

- NX_INVALID_INTERFACE (0x4C) geçersiz ağ arabirimi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Start the DHCP processing for this IP instance on interface 1. */
status =  nx_dhcp_interface_start(&my_dhcp, 1);

/* If status is NX_SUCCESS the DHCP was successfully started. */
```

## <a name="nx_dhcp_state_change_notify"></a>nx_dhcp_state_change_notify

DHCP durum değiştirme geri çağırma işlevini ayarla

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcp_state_change_notify(
          NX_DHCP *dhcp_ptr, 
          VOID (*dhcp_state_change_notify)(NX_DHCP *dhcp_ptr, 
                                           UCHAR new_state));
```

### <a name="description"></a>Description

Bu hizmet, DHCP durum değişikliklerinin bir uygulamasına bildirimde bulunmak için dhcp_state_change_notify belirtilen geri çağırma işlevini kaydeder. Geri arama işlevi, DHCP Istemcisinin geçiş durumunu sağlar.

Aşağıdakiler, çeşitli DHCP durumlarıyla ilişkili değerlerdir:

| Durum                             | Değer |
|-----------------------------------|-------|
| NX \_ DHCP \_ durumu \_ önyüklemesi             | 1     |
| NX \_ DHCP \_ durumu \_ INIT             | 2     |
| NX \_ DHCP \_ durumu \_ seçme        | 3     |
| NX \_ DHCP \_ durumu \_ isteniyor       | 4     |
| NX \_ DHCP \_ durum \_ sınırı            | 5     |
| NX \_ DHCP \_ durumu \_ yenileniyor         | 6     |
| NX \_ DHCP \_ durumu yeniden \_ bağlama        | 7     |
| NX_DHCP_STATE_FORCERENEW          | 8     |
| NX \_ DHCP \_ durum \_ adresi \_ yoklama | 9     |


### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr** Daha önce oluşturulan DHCP örneğine yönelik işaretçi.

- **dhcp_state_change_notify** Durum değişikliği geri çağırma işlev işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı geri çağırma kümesi.  

- NX_PTR_ERROR (0x16) geçersiz DHCP işaretçisi.

- NX_CALLER_ERROR (0x11) geçersiz hizmet çağıranı.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```C
/* Register the “my_state_change” function to be called on any DHCP state change, 
   assuming DHCP has alreadybeen created. */
status =  nx_dhcp_state_change_notify(&my_dhcp, my_state_change);

/* If status is NX_SUCCESS the callback function was successfully
   registered. */
```

## <a name="nx_dhcp_interface_state_change_notify"></a>nx_dhcp_interface_state_change_notify

Belirtilen arabirimdeki DHCP durum değiştirme geri çağırma işlevini ayarla

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcp_interface_state_change_notify(
              NX_DHCP *dhcp_ptr, 
              UINT interface_index,
              VOID (*dhcp_state_change_notify)(NX_DHCP *dhcp_ptr, 
                                               UINT interface_index,
                                               UCHAR new_state));
```

### <a name="description"></a>Description

Bu hizmet, DHCP durum değişikliklerinin bir uygulamasına bildirimde bulunmak için belirtilen geri çağırma işlevini kaydeder. Geri çağırma, funcıton giriş bağımsız değişkenleri, arabirim dizinidir ve DHCP Istemcisinin bu arabirimde geçiş olduğu durumdur.

Durum değişikliği işlevleri hakkında daha fazla bilgi için bkz. *nx_dhcp_state_change_notify*().

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr** Daha önce oluşturulan DHCP örneğine yönelik işaretçi.

- **dhcp_interface_state_change_notify** Uygulama geri çağırma işlev işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı geri çağırma kümesi.  

- NX_PTR_ERROR (0x16) geçersiz DHCP işaretçisi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```C
/* Register the “my_state_change” function to be called on any DHCP state 
   change, assuming DHCP has alreadybeen created. */

void dhcp_interstate_state_change(NX_DHCP *dhcp_ptr, UINT iface_index, 
                                 UCHAR new_state);


status =  nx_dhcp_interstate_state_change_notify(&my_dhcp,  
                                                 dhcp_interstate_state_change);

/* If status is NX_SUCCESS the callback function was successfully
   registered. */
```

## <a name="nx_dhcp_stop"></a>nx_dhcp_stop

DHCP işlemesini durduruyor

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcp_stop(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a>Description

Bu hizmet, DHCP işlemesini Başlatan tüm arabirimlerde DHCP işlemeyi durduruyor. DHCP 'yi işleyen bir arabirim yoksa, bu hizmet DHCP Istemci iş parçacığını askıya alacak ve DHCP Istemci zamanlayıcısını devre dışı kalacak.

DHCP için birden çok arabirim etkinleştirilmişse, belirli bir arabirimdeki DHCP 'yi durdurmak için *nx_dhcp_interface_stop* hizmetini kullanın.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr** Daha önce oluşturulan DHCP örneğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı DHCP durağı

- **NX_DHCP_NOT_STARTED** (0x96) DHCP örneği başlatılmadı.

- NX_PTR_ERROR (0x16) geçersiz DHCP işaretçisi.

- NX_CALLER_ERROR (0x11) geçersiz hizmet çağıranı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Stop the DHCP processing for this IP instance. */
status =  nx_dhcp_stop(&my_dhcp);

/* If status is NX_SUCCESS the DHCP was successfully stopped. */
```

## <a name="nx_dhcp_interface_stop"></a>nx_dhcp_interface_stop

Belirtilen arabirimdeki DHCP işlemesini durdur

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcp_interface_stop(NX_DHCP *dhcp_ptr, UINT interface_index);
```

### <a name="description"></a>Description

Bu hizmet, DHCP zaten başlatılmışsa belirtilen arabirimdeki DHCP işlemesini durduruyor. DHCP çalıştıran başka arabirimler yoksa, DHCP iş parçacığı ve Zamanlayıcı askıya alınır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr** Daha önce oluşturulan DHCP örneğine yönelik işaretçi.

- **Interface_index** DHCP işlemenin durdurulacağı arabirim

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı DHCP durağı

- **NX_DHCP_NOT_STARTED** (0x96) DHCP başlatılmadı.

- NX_PTR_ERROR (0x16) geçersiz DHCP işaretçisi.

- NX_CALLER_ERROR (0x11) geçersiz hizmet çağıranı.

- NX_INVALID_INTERFACE (0x4C) geçersiz ağ arabirimi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Stop DHCP processing for this IP instance on interface 1. */
status =  nx_dhcp_interface_stop(&my_dhcp, 1);

/* If status is NX_SUCCESS the DHCP was successfully stopped. */
```

## <a name="nx_dhcp_user_option_retrieve"></a>nx_dhcp_user_option_retrieve

Son sunucu yanıtından bir DHCP seçeneği alın

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcp_user_option_retrieve(NX_DHCP *dhcp_ptr, 
            UINT request_option, UCHAR *destination_ptr, 
            UINT *destination_size);
```

### <a name="description"></a>Description

Bu hizmet, DHCP Istemci kaydında bulunan DHCP için etkinleştirilen ilk arabirimdeki DHCP seçenekleri arabelleğinden belirtilen DHCP seçeneğini alır. Başarılı olursa, seçenek verileri belirtilen arabelleğe kopyalanır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr** Daha önce oluşturulan DHCP örneğine yönelik işaretçi.  

- **request_option** RFC tarafından belirtilen şekilde DHCP seçeneği. *Nx_dhcp. h* içindeki NX_DHCP_OPTION seçeneğine bakın.

- **destination_ptr** Yanıt dizesi için hedefin işaretçisi.  

- **destination_size** Hedefin boyutuna ve dönüşe ilişkin işaretçi, döndürülen bayt sayısını yerleştirmek için hedef.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı seçenek alma.  

- **NX_DHCP_NOT_BOUND** (0x94) DHCP istemcisi bağlanmadı.

- **NX_DHCP_NO_INTERFACES_ENABLED** (0xa5) DHCP için etkinleştirilen arabirim yok

- **NX_DHCP_DEST_TO_SMALL** (0x95) hedefi, yanıtı tutmak için çok küçük.

- Sunucu yanıtında **NX_DHCP_PARSE_ERROR** (0x97) DHCP seçeneği bulunamadı.

- NX_PTR_ERROR (0x16) geçersiz giriş işaretçisi.

- NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
UCHAR  dns_ip_string[4];
ULONG  size;

/* Obtain the IP address of the DNS server. */
size =    sizeof(dnx_ip_string);
status =  nx_dhcp_user_option_retrieve(&my_dhcp, NX_DHCP_OPTION_DNS_SVR,
        dns_ip_string, &size);

/* If status is NX_SUCCESS the DNS IP address is in dns_ip_string. */
```

## <a name="nx_dhcp_interface_user_option_retrieve"></a>nx_dhcp_interface_user_option_retrieve

Belirtilen arabirimdeki son sunucu yanıtından bir DHCP seçeneği alın

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcp_interface_user_option_retrieve(NX_DHCP *dhcp_ptr,
                  UINT interface_index, 
            UINT request_option, UCHAR *destination_ptr, 
            UINT *destination_size);
```

### <a name="description"></a>Description

Bu hizmet, belirtilen arabirim DHCP için etkinleştirilirse belirtilen arabirimdeki DHCP seçenekleri arabelleğinden belirtilen DHCP seçeneğini alır. Başarılı olursa, seçenek verileri belirtilen arabelleğe kopyalanır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr** Daha önce oluşturulan DHCP örneğine yönelik işaretçi.

- **Interface_index** Belirtilen seçeneğin alınacağı dizin  

- **request_option** RFC tarafından belirtilen şekilde DHCP seçeneği. *Nx_dhcp. h* içindeki NX_DHCP_OPTION seçeneğine bakın.  

- **destination_ptr** Yanıt dizesi için hedefin işaretçisi.  

- **destination_size** Hedefin boyutuna ve dönüşe ilişkin işaretçi, döndürülen bayt sayısını yerleştirmek için hedef.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı seçenek alma.  

- **NX_DHCP_NOT_BOUND** (0x94) IP adresi atanmadı

- **NX_DHCP_DEST_TO_SMALL** (0x95) arabelleği çok küçük

- Sunucu yanıtında **NX_DHCP_PARSE_ERROR** (0x97) DHCP seçeneği bulunamadı.

- NX_PTR_ERROR (0x16) geçersiz DHCP işaretçisi.

- NX_CALLER_ERROR (0x11) geçersiz hizmet çağıranı.

- NX_INVALID_INTERFACE (0x4C) geçersiz ağ arabirimi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
UCHAR  dns_ip_string[4];
ULONG  size;

/* Obtain the IP address of the DNS server on the prmary interface. */
size =    sizeof(dnx_ip_string);
status =  nx_dhcp_interface_user_option_retrieve(&my_dhcp, 0, NX_DHCP_OPTION_DNS_SVR,
        dns_ip_string, &size);

/* If status is NX_SUCCESS the DNS IP address is in dns_ip_string. */
```

## <a name="nx_dhcp_user_option_convert"></a>nx_dhcp_user_option_convert

Dört baytı ULONG 'a Dönüştür

### <a name="prototype"></a>Prototype

```C
ULONG nx_dhcp_user_option_convert(UCHAR *option_string_ptr);
```

### <a name="description"></a>Description

Bu hizmet, "option_string_ptr" ile işaret edilen dört karakteri işaretsiz bir Long değere dönüştürür. Bu, özellikle IP adresleri mevcut olduğunda faydalıdır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **option_string_ptr** Daha önce alınan seçenek dizesinin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **Değer** İlk dört baytın değeri.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
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

```C
ULONG nx_dhcp_user_option_add_callbcak_set(NX_DHCP *dhcp_ptr, 
    UINT (*dhcp_user_option_add)(NX_DHCP *dhcp_ptr, 
                                 UINT iface_index, 
                                 UINT message_type, 
                                 UCHAR *user_option_ptr, 
                                 UINT *user_option_length));
```

### <a name="description"></a>Description

Bu hizmet, Kullanıcı tarafından sağlanan seçenekleri eklemek için belirtilen geri çağırma işlevini kaydeder.

Geri çağırma işlevi belirtilmişse, uygulamalar iface_index ve message_type tarafından pakete Kullanıcı tarafından sağlanan seçenekleri ekleyebilir.

> [!NOTE]
> Kullanıcı yordamında. Kullanıcı tarafından sağlanan seçenekler eklerken uygulamaların DHCP seçenekleri biçimi gelmelidir. Kullanıcı seçeneklerinin toplam boyutu user_option_length küçük veya eşit olmalı ve user_option_length gerçek seçenek uzunluğu olarak güncellenebilir. Seçenek başarıyla Ekle ' NX_TRUE döndürün, aksi NX_FALSE döndürün.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr** Daha önce oluşturulan DHCP örneğine yönelik işaretçi.

- **dhcp_user_option_add** Kullanıcı seçeneği ekleme işlevi işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı geri çağırma kümesi.

- NX_PTR_ERROR (0x16) geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Register the “my_dhcp_user_option_add” function to be called when add DHCP
options, assuming DHCP has already been created. */

status =  nx_dhcp_user_option_add_callback_set(&my_dhcp, my_dhcp_user_option_add);

/* If status is NX_SUCCESS the callback function was successfully registered. */
```
