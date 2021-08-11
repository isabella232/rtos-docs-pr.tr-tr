---
title: Bölüm 3 - NetX PPPoE Azure RTOS Hizmetlerinin Açıklaması
description: Bu bölümde, Tüm NetX PPPoE Azure RTOS hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 07/13/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 8310006b7c188fa63402c931459ffd84ebb776c207dc520959208449862fe27f
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116790216"
---
# <a name="chapter-3---description-of-azure-rtos-netx-pppoe-client-services"></a>Bölüm 3 - NetX PPPoE Azure RTOS Hizmetlerinin Açıklaması

Bu bölümde, Tüm NetX PPPoE Azure RTOS hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklaması yer almaktadır.

Aşağıdaki API açıklamalarında yer alan "Dönüş Değerleri" bölümünde, **KALıN**  olmayan değerler tamamen devre dışı bırakılırken, BOLD NX_DISABLE_ERROR_CHECKING API hata denetimlerini devre dışı bırakmak için kullanılan tanımdan etkilenmez.

- **nx_pppoe_client_create** *PPPoE İstemci örneği oluşturma*
- **nx_pppoe_client_delete** *PPPoE İstemci örneğini silme*
- **nx_pppoe_client_host_uniq_set** *PPPoE İstemcisi için benzersiz bir konak ayarlayın*
- **nx_pppoe_client_host_uniq_set_extended** *PPPoE İstemcisi için benzersiz bir konak ayarlayın*
- **nx_pppoe_client_service_name_set** *PPPoE İstemcisi için hizmet adını ayarlayın*
- **nx_pppoe_client_service_name_set_extended** *PPPoE İstemcisi için hizmet adını ayarlama*
- **nx_pppoe_client_session_connect** *Bağlan PPPoE Sunucusuna PPPoE İstemcisi oturumu*
- **nx_pppoe_client_session_packet_send** *PPPoE oturum paketini gönderme*
- **nx_pppoe_client_session_terminate** *PPPoE oturumunu sonlandırma*
- **nx_pppoe_client_session_get** *PPPoE oturum inf'lerini al*

## <a name="nx_pppoe_client_create"></a>nx_pppoe_client_create

PPPoE İstemci örneği oluşturma

### <a name="prototype"></a>Prototype

```c
UINT  nx_pppoe_client_create(NX_PPPOE_CLIENT *pppoe_client_ptr,
                            CHAR *name, NX_IP *ip_ptr,
                            UINT interface_index,
                            NX_PACKET_POOL *pool_ptr,
                            VOID *stack_ptr, ULONG stack_size,
                            UINT priority,
                            VOID (*pppoe_link_driver)
                            (struct NX_IP_DRIVER_STRUCT *)
                            VOID (*pppoe_packet_receive)
                            (NX_PACKET *packet_ptr));
```

### <a name="description"></a>Description

Bu hizmet, belirtilen NetX IP örneği için kullanıcı tarafından sağlanan bağlantı sürücüsü ile bir PPPoE İstemci örneği oluşturur. Bağlantı sürücüsü başlatılmamışsa ve etkinse, bağlantı sürücüsünü başlatmak PPPoE İstemci yazılımından sorumludur.

Ayrıca, uygulamanın iç paket ayırma için kullanmak üzere PPPoE İstemci örneği için önceden oluşturulmuş bir paket havuzu sağlamak gerekir.

> [!NOTE]
> Genel olarak, PPPoE İstemcisi iş parçacığı önceliklerinden daha yüksek bir önceliğe sahip NetX IP iş parçacığı oluşturmak iyi bir fikirdir. IP iş parçacığı *nx_ip_create* belirtme hakkında daha fazla bilgi için lütfen nx_ip_create hizmetine bakın.

### <a name="input-parameters"></a>Giriş Parametreleri

 - **pppoe_client_ptr** PPPoE İstemcisi denetim bloğuna işaretçi.
 - **name** Bu PPPoE İstemci örneğinin adı.
 - **ip_ptr** IP örneği için denetim bloğuna işaretçi.
 - **interface_index** Arabirim dizini.
 - **pool_ptr** Paket havuzunun işaretçisi.
 - **stack_ptr** PPPoE İstemcisi iş parçacığının yığın alanı başlangıç işaretçisi.
 - **stack_size** İş parçacığının yığınında bayt cinsinden boyut.
 - **öncelik** İç PPPoE İstemci iş parçacıklarının önceliği (1-31).
 - **pppoe_link_driver** Kullanıcı tarafından sağlanan bağlantı sürücüsü.
 - **pppoe_packet_receive** Kullanıcı tarafından sağlanan paket alma işlevi.

### <a name="return-values"></a>Dönüş Değerleri

 - **NX_PPPOE_CLIENT_SUCCESS** (0x00) PPPoE İstemcisi oluşturma.
 - NX_PPPOE_CLIENT_PTR_ERROR (0xD1) Geçersiz PPPoE İstemcisi, IP, paket havuzu veya yığın işaretçisi.
 - NX_PPPOE_CLIENT_INVALID_INTERFACE (0xD2) Geçersiz arabirim.
 - NX_PPPOE_CLIENT_PACKET_PAYLOAD_ERROR (0xD3) Paket havuzunun yük boyutu geçersiz.
 - NX_PPPOE_CLIENT_MEMORY_SIZE_ERROR (0xD4) Geçersiz bellek boyutu.
 - NX_PPPOE_CLIENT_PRIORITY_ERROR (0xD5) PPPoE İstemci iş parçacığının geçersiz önceliği.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Create “my_pppoe_client” for IP instance “my_ip”. */
status =  nx_pppoe_client_create(&my_pppoe_client, “my PPPoE Client”, &my_ip,
0, &my_pool, stack_start, 1024, 2,
link_driver, packet_receive);

/* If status is NX_PPPOE_CLIENT_SUCCESS, the “my_pppoe_client” was successfully created. */
```

## <a name="nx_pppoe_client_delete"></a>nx_pppoe_client_delete

PPPoE İstemci örneğini silme

### <a name="prototype"></a>Prototype

```c
UINT nx_pppoe_client_delete(NX_PPPOE_CLIENT *pppoe_client_ptr);
```

### <a name="description"></a>Description

Bu hizmet, önceden oluşturulmuş PPPoE İstemci örneğini siler.

### <a name="input-parameters"></a>Giriş Parametreleri

 - **pppoe_client_ptr** PPPoE İstemcisi denetim bloğu işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

 - **NX_PPPOE_CLIENT_SUCCESS** (0x00) PPPoE İstemcisi silme.
 - NX_PPPOE_CLIENT_PTR_ERROR (0xD1) Geçersiz PPPoE İstemcisi işaretçisi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Delete PPPoE Client instance “my_pppoe_client”. */
status =  nx_pppoe_client_delete(&my_pppoe_client);

/* If status is NX_PPPOE_CLIENT_SUCCESS, the “my_pppoe_client” was successfully deleted. */
```

## <a name="nx_pppoe_client_host_uniq_set"></a>nx_pppoe_client_host_uniq_set

PPPoE İstemcisi ana bilgisayarlarını benzersiz olarak ayarlama

### <a name="prototype"></a>Prototype

```c
UINT nx_pppoe_client_host_uniq_set(
                        NX_PPPOE_CLIENT *pppoe_client_ptr,
                        UCHAR *host_uniq);
```

### <a name="description"></a>Description

Bu hizmet PPPoE İstemcisi ana bilgisayarlarını benzersiz olarak ayarlar. Host-Uniq, bir Access Concentrator'ı belirli bir Konak isteğiyle benzersiz olarak ilişkilendirmek için bir konak tarafından kullanılır.
Bu, Ana Bilgisayar'ın tercihi olan herhangi bir değer ve uzunlukta ikili veriler olabilir.

> [!NOTE]
> konak benzersiz, Null sonlandırılan dize olmalıdır.

> [!NOTE]
> Bu hizmet kullanım dışıdır. Geliştiricilerin *nx_pppoe_client_host_uniq_set_extended() 'a geçişleri teşvik edilecektir.*

### <a name="input-parameters"></a>Giriş Parametreleri

 - **pppoe_client_ptr** PPPoE İstemcisi denetim bloğuna işaretçi.
 - **host_uniq** Benzersiz bir ana bilgisayar işaretçisi. Konak benzersiz, Null sonlandırılan dize olmalıdır.

### <a name="return-values"></a>Dönüş Değerleri

 - **NX_PPPOE_CLIENT_SUCCESS** (0x00) Başarılı PPPoE İstemcisi konak benzersiz kümesi.
 - NX_PPPOE_CLIENT_PTR_ERROR (0xD1) Geçersiz PPPoE İstemcisi işaretçisi.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Set service name for PPPoE Client instance “my_pppoe_client”. */
status =  nx_pppoe_client_host_uniq_set(&my_pppoe_client,
“220000000000000041000000”);

/* If status is NX_PPPOE_CLIENT_SUCCESS, the “my_pppoe_client” host unique has set. */
```

## <a name="nx_pppoe_client_host_uniq_set_extended"></a>nx_pppoe_client_host_uniq_set_extended

PPPoE İstemcisi ana bilgisayarlarını benzersiz olarak ayarlama

### <a name="prototype"></a>Prototype

```c
UINT nx_pppoe_client_host_uniq_set_extended(
                        NX_PPPOE_CLIENT *pppoe_client_ptr,
                        UCHAR *host_uniq,UINT host_uniq_length);
```

### <a name="description"></a>Description

Bu hizmet PPPoE İstemcisi ana bilgisayarlarını benzersiz olarak ayarlar. Host-Uniq, bir Access Concentrator'ı belirli bir Konak isteğiyle benzersiz olarak ilişkilendirmek için bir konak tarafından kullanılır.
Bu, Ana Bilgisayar'ın tercihi olan herhangi bir değer ve uzunlukta ikili veriler olabilir.

> [!NOTE]
> konak benzersiz, Null sonlandırılan dize olmalıdır.

> [!NOTE]
> Bu hizmet, *nx_pppoe_client_host_uniq_set() ile değiştirilir.* Bu sürüm hizmete ek uzunluk bilgileri sağlar.

### <a name="input-parameters"></a>Giriş Parametreleri

 - **pppoe_client_ptr** PPPoE İstemcisi denetim bloğuna işaretçi.
 - **host_uniq** Benzersiz bir ana bilgisayar işaretçisi. Konak benzersiz, Null sonlandırılan dize olmalıdır.
 - **host_uniq_length** Host_uniq

### <a name="return-values"></a>Dönüş Değerleri

 - **NX_PPPOE_CLIENT_SUCCESS** (0x00) Başarılı PPPoE İstemcisi konak benzersiz kümesi.
 - **NX_PPPOE_CLIENT_PTR_ERROR** (0xD1) Geçersiz PPPoE İstemcisi işaretçisi.
 - **NX_SIZE_ERROR** (0x09) Denetim host_uniq_length başarısız

### <a name="allowed-from"></a>İzin Verilen

Başlatma, iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Set service name for PPPoE Client instance “my_pppoe_client”. */
status =  nx_pppoe_client_host_uniq_set_extended(&my_pppoe_client,
“220000000000000041000000”,24);

/* If status is NX_PPPOE_CLIENT_SUCCESS, the “my_pppoe_client” host unique has set. */
```

## <a name="nx_pppoe_client_service_name_set"></a>nx_pppoe_client_service_name_set

PPPoE Istemci hizmeti adını ayarla

### <a name="prototype"></a>Prototype

```c
UINT nx_pppoe_client_service_name_set(
                        NX_PPPOE_CLIENT *pppoe_client_ptr,
                        UCHAR *service_name);
```

### <a name="description"></a>Description

Bu hizmet, PPPoE Istemci hizmeti adını ayarlar. Konağın istediği hizmeti belirten Service-Name. Service-Name ayarlanmamışsa konağın herhangi bir sayıda hizmeti kabul edeceğini belirtir.

> [!NOTE]
> hizmet adı null ile sonlandırılmış bir dize olmalıdır

> [!NOTE]
> Bu hizmet kullanımdan kaldırılmıştır. Geliştiricilerin *nx_pppoe_client_service_name_set_extended ()* uygulamasına geçirilmesi önerilir.

### <a name="input-parameters"></a>Giriş Parametreleri

 - **pppoe_client_ptr** PPPoE Istemci denetim bloğu işaretçisi.
 - **service_name** Hizmet adı işaretçisi. Hizmet adı null ile sonlandırılmış bir dize olmalıdır.

### <a name="return-values"></a>Dönüş Değerleri

 - **NX_PPPOE_CLIENT_SUCCESS** (0x00) başarılı PPPoE istemci hizmeti adı kümesi.
 - **NX_PPPOE_CLIENT_PTR_ERROR** (0Xd1) geçersiz PPPoE istemci işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Set service name for PPPoE Client instance “my_pppoe_client”. */
status =  nx_pppoe_client_service_name_set(&my_pppoe_client,
“BRAS”);

/* If status is NX_PPPOE_CLIENT_SUCCESS, the “my_pppoe_client” service name has set. */
```

## <a name="nx_pppoe_client_service_name_set_extended"></a>nx_pppoe_client_service_name_set_extended

PPPoE Istemci hizmeti adını ayarla

### <a name="prototype"></a>Prototype

```c
UINT nx_pppoe_client_service_name_set_extended(
                        NX_PPPOE_CLIENT *pppoe_client_ptr,
                        UCHAR *service_name,UINT service_name_length);
```

### <a name="description"></a>Description

Bu hizmet, PPPoE Istemci hizmeti adını ayarlar. Konağın istediği hizmeti belirten Service-Name. Service-Name ayarlanmamışsa konağın herhangi bir sayıda hizmeti kabul edeceğini belirtir.

> [!NOTE]
> hizmet adı null ile sonlandırılmış bir dize olmalıdır.

> [!NOTE]
> Bu hizmet *nx_pppoe_client_service_name_set ()* yerini alır. Bu sürüm, işleve ek hizmet adı uzunluk bilgilerini sağlar.

### <a name="input-parameters"></a>Giriş Parametreleri

 - **pppoe_client_ptr** PPPoE Istemci denetim bloğu işaretçisi.
 - **service_name** Hizmet adı işaretçisi. Hizmet adı null ile sonlandırılmış bir dize olmalıdır.
 - **service_name_length** Service_name uzunluğu

### <a name="return-values"></a>Dönüş Değerleri

 - **NX_PPPOE_CLIENT_SUCCESS** (0x00) başarılı PPPoE istemci hizmeti adı kümesi.
 - **NX_PPPOE_CLIENT_PTR_ERROR** (0Xd1) geçersiz PPPoE istemci işaretçisi.
 - **NX_SIZE_ERROR** (0x09) denetim service_name_length başarısız oldu

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Set service name for PPPoE Client instance “my_pppoe_client”. */
status =  nx_pppoe_client_service_name_set_extended(&my_pppoe_client,
“BRAS”,4);

/* If status is NX_PPPOE_CLIENT_SUCCESS, the “my_pppoe_client” service name has set. */
```

## <a name="nx_pppoe_client_session_connect"></a>nx_pppoe_client_session_connect

Bağlan PPPoE Istemci oturumu

### <a name="prototype"></a>Prototype

```c
UINT nx_pppoe_client_session_connect(NX_PPPOE_CLIENT *pppoe_client_ptr,
                                    ULONG wait_option);
```

### <a name="description"></a>Description

Bu hizmet, daha önce oluşturulmuş bir PPPoE Istemcisini belirtilen PPPoE sunucusuna kullanarak PPPoE oturum bağlantısı yapar.

> [!NOTE]
> Bu işlev, *nx_pppoe_client_create*, *nx_pppoe_client_host_uniq_set* ve *nx_pppoe_client_service_name_set* sonra çağrılmalıdır.

### <a name="input-parameters"></a>Giriş Parametreleri

 - **pppoe_client_ptr** PPPoE Istemci denetim bloğu işaretçisi.
 - **wait_option** Bağlantı kurulurken bekle seçeneği.

### <a name="return-values"></a>Dönüş Değerleri

 - **NX_PPPOE_CLIENT_SUCCESS** (0x00) başarılı PPPoE istemci oturumu bağlantısı.
 - NX_PPPOE_CLIENT_PTR_ERROR (0xD1) geçersiz PPPoE Istemci işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Enable PPPoE Client instance “my_pppoe_client”. */
status =  nx_pppoe_client_session_connect(&my_pppoe_client);

/* If status is NX_PPPOE_CLIENT_SUCCESS, the “my_pppoe_client” session connection has connected. */
```

## <a name="nx_pppoe_client_session_packet_send"></a>nx_pppoe_client_session_packet_send

PPPoE Istemci paketini belirtilen oturuma gönder

### <a name="prototype"></a>Prototype

```c
UINT nx_pppoe_client_session_packet_send(
                                    NX_PPPOE_CLIENT *pppoe_client_ptr,
                                    NX_PACKET *packet_ptr);
```

### <a name="description"></a>Description

Bu hizmet, belirtilen oturum KIMLIĞINI kullanarak PPPoE paketi gönderir.

### <a name="input-parameters"></a>Giriş Parametreleri

 - **pppoe_client_ptr** PPPoE Istemci denetim bloğu işaretçisi.
 - **packet_ptr** PPPoE paketi işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

 - **NX_PPPOE_CLIENT_SUCCESS** (0x00) başarılı PPPoE istemci paketi gönderme.
 - NX_PPPOE_CLIENT_PTR_ERROR (0xD1) geçersiz PPPoE Istemci işaretçisi.
 - NX_PPPOE_CLIENT_PACKET_PAYLOAD_ERROR (0xD3) geçersiz PPPoE Istemci paketi.
 - NX_PPPOE_CLIENT_SESSION_NOT_ESTABLISHED (0xD8) PPPoE oturumu kurulmadı.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Send PPPoE client packet to specified session, PPPoE Client instance “my_pppoe_client”. */
status =  nx_pppoe_client_session_packet_send(&my_pppoe_client, packet_ptr);

/* If status is NX_PPPOE_CLIENT_SUCCESS, the “my_pppoe_client” packet has sent. */
```

## <a name="nx_pppoe_client_session_terminate"></a>nx_pppoe_client_session_terminate

PPPoE Istemci oturumunu Sonlandır

### <a name="prototype"></a>Prototype

```c
UINT nx_pppoe_client_session_terminate(
                                    NX_PPPOE_CLIENT *pppoe_client_ptr);
```

### <a name="description"></a>Description

Bu hizmet, belirtilen PPPoE oturumunu sonlandırır.

### <a name="input-parameters"></a>Giriş Parametreleri

 - **pppoe_client_ptr** PPPoE Istemci denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

 - **NX_PPPOE_CLIENT_SUCCESS** (0x00) başarılı PPPoE istemci oturumu sonlandırılır.
 - NX_PPPOE_CLIENT_PTR_ERROR (0xD1) geçersiz PPPoE Istemci işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Terminates the specified PPPoE session, PPPoE Client instance “my_pppoe_client”. */
status =  nx_pppoe_client_session_terminate(&my_pppoe_client);

/* If status is NX_PPPOE_CLIENT_SUCCESS, the session has terminated. */
```

## <a name="nx_pppoe_client_session_get"></a>nx_pppoe_client_session_get

Belirtilen PPPoE oturum bilgilerini al

### <a name="prototype"></a>Prototype

```c
UINT nx_pppoe_client_session_get(NX_PPPOE_CLIENT *pppoe_client_ptr,
                                ULONG *server_mac_msw,
                                ULONG *server_mac_lsw,
                                ULONG *session_id);
```

### <a name="description"></a>Description

Bu hizmet, belirtilen PPPoE oturum bilgilerini, sunucu fiziksel adresini ve oturum kimliğini alır.

### <a name="input-parameters"></a>Giriş Parametreleri

 - **pppoe_server_ptr** PPPoE Istemci denetim bloğu işaretçisi.
 - **server_mac_msw** Sunucu fiziksel adresi MSW işaretçisi.
 - **server_mac_lsw** Sunucu fiziksel adresi MSW işaretçisi.
 - **session_id** Oturum KIMLIĞI işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

 - **NX_PPPOE_CLIENT_SUCCESS** (0x00) başarılı PPPoE istemci oturumu al.
 - NX_PPPOE_CLIENT_PTR_ERROR (0xD1) geçersiz PPPoE Istemci işaretçisi.
 - NX_PPPOE_CLIENT_SESSION_NOT_ESTABLISHED (0xD8) PPPoE oturumu kurulmadı.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Gets the specified PPPoE session information, PPPoE Client instance “my_pppoe_client”. */
status =  nx_pppoe_client_session_get (&my_pppoe_client, &server_mac_msw, &server_mac_lsw, &session_id);

/* If status is NX_PPPOE_CLIENT_SUCCESS, the server physical address and session id
   of the session has got. */
```
