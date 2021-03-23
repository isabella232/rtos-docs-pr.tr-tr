---
title: Bölüm 3-Azure RTOS NetX PPPoE Istemci hizmetlerinin açıklaması
description: Bu bölüm, tüm Azure RTOS NetX PPPoE Istemci hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 07/13/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 246115fc97d7597246f7fd5b4fb88cb615baab33
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825589"
---
# <a name="chapter-3---description-of-azure-rtos-netx-pppoe-client-services"></a>Bölüm 3-Azure RTOS NetX PPPoE Istemci hizmetlerinin açıklaması

Bu bölüm, tüm Azure RTOS NetX PPPoE Istemci hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.

Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_DISABLE_ERROR_CHECKING** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.

- **nx_pppoe_client_create** *bir PPPoE istemci örneği oluşturma*
- **Nx_pppoe_client_delete** *PPPoE istemci örneğini silme*
- **Nx_pppoe_client_host_uniq_set** *PPPoE istemcisi için benzersiz konak kümesi*
- **Nx_pppoe_client_host_uniq_set_extended** *PPPoE istemcisi için benzersiz konak kümesi*
- **Nx_pppoe_client_service_name_set** *PPPoE istemcisinin hizmet adını ayarlama*
- **Nx_pppoe_client_service_name_set_extended** *PPPoE istemcisinin hizmet adını ayarlama*
- **Nx_pppoe_client_session_connect** *PPPoE Istemci oturumunu PPPoE sunucusuna bağlama*
- **Nx_pppoe_client_session_packet_send** *PPPoE oturum paketi gönder*
- **Nx_pppoe_client_session_terminate** *PPPoE oturumunu Sonlandır*
- **nx_pppoe_client_session_get** *belirtilen PPPoE oturum inf dosyasını Al*

## <a name="nx_pppoe_client_create"></a>nx_pppoe_client_create

Bir PPPoE Istemci örneği oluşturma

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

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen NetX IP örneği için Kullanıcı tarafından sağlanan bağlantı sürücüsüyle bir PPPoE Istemci örneği oluşturur. Bağlantı sürücüsü başlatılmamış ve etkin değilse, PPPoE Istemci yazılımı bağlantı sürücüsünü başlatmaktan sorumludur.

Ayrıca, uygulamanın, iç paket ayırma için kullanması için, PPPoE Istemci örneği için önceden oluşturulmuş bir paket havuzu sağlaması gerekir.

> [!NOTE]
> Genellikle NetX IP iş parçacığını, PPPoE Istemci iş parçacığı önceliğinden daha yüksek bir önceliğe göre oluşturmanız iyi bir fikirdir. IP iş parçacığı önceliğini belirtme hakkında daha fazla bilgi için lütfen *nx_ip_create* hizmetine bakın.

### <a name="input-parameters"></a>Giriş Parametreleri

 - **pppoe_client_ptr** PPPoE Istemci denetim bloğu işaretçisi.
 - **ad** Bu PPPoE Istemci örneğinin adı.
 - **ip_ptr** IP örneği için denetim bloğuna yönelik işaretçi.
 - **interface_index** Arabirim dizini.
 - **pool_ptr** Paket havuzu işaretçisi.
 - **stack_ptr** PPPoE Istemci iş parçacığının yığın alanının başlangıcı işaretçisi.
 - **stack_size** İş parçacığının yığınında bayt cinsinden boyut.
 - **Öncelik** İç PPPoE Istemci iş parçacıklarının önceliği (1-31).
 - **pppoe_link_driver** Kullanıcı tarafından sağlanan bağlantı sürücüsü.
 - **pppoe_packet_receive** Kullanıcı tarafından sağlanan paket alma işlevi.

### <a name="return-values"></a>Dönüş Değerleri

 - **NX_PPPOE_CLIENT_SUCCESS** (0x00) başarılı PPPoE istemcisi oluştur.
 - NX_PPPOE_CLIENT_PTR_ERROR (0xD1) geçersiz PPPoE Istemcisi, IP, paket havuzu veya yığın işaretçisi.
 - NX_PPPOE_CLIENT_INVALID_INTERFACE (0xD2) geçersiz arabirim.
 - NX_PPPOE_CLIENT_PACKET_PAYLOAD_ERROR (0xD3) paket havuzunun yük boyutu geçersiz.
 - NX_PPPOE_CLIENT_MEMORY_SIZE_ERROR (0xD4) geçersiz bellek boyutu.
 - NX_PPPOE_CLIENT_PRIORITY_ERROR (0xD5) PPPoE Istemci iş parçacığının geçersiz önceliği.

### <a name="allowed-from"></a>İzin verilen

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

Bir PPPoE Istemci örneğini silme

### <a name="prototype"></a>Prototype

```c
UINT nx_pppoe_client_delete(NX_PPPOE_CLIENT *pppoe_client_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, önceden oluşturulmuş olan PPPoE Istemci örneğini siler.

### <a name="input-parameters"></a>Giriş Parametreleri

 - **pppoe_client_ptr** PPPoE Istemci denetim bloğu işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

 - **NX_PPPOE_CLIENT_SUCCESS** (0x00) başarılı PPPoE istemcisi silme.
 - NX_PPPOE_CLIENT_PTR_ERROR (0xD1) geçersiz PPPoE Istemci işaretçisi.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Delete PPPoE Client instance “my_pppoe_client”. */
status =  nx_pppoe_client_delete(&my_pppoe_client);

/* If status is NX_PPPOE_CLIENT_SUCCESS, the “my_pppoe_client” was successfully deleted. */
```

## <a name="nx_pppoe_client_host_uniq_set"></a>nx_pppoe_client_host_uniq_set

PPPoE Istemci konağını benzersiz ayarla

### <a name="prototype"></a>Prototype

```c
UINT nx_pppoe_client_host_uniq_set(
                        NX_PPPOE_CLIENT *pppoe_client_ptr,
                        UCHAR *host_uniq);
```

### <a name="description"></a>Açıklama

Bu hizmet, PPPoE Istemci konağını benzersiz olarak ayarlar. Host-Uniq, bir ana bilgisayar tarafından bir erişim yoğunlaştırıcıyı belirli bir ana bilgisayar isteğiyle benzersiz bir şekilde ilişkilendirmek için kullanılır.
Bu, konağın seçtiği herhangi bir değerin ve uzunluğun ikili verileri olabilir.

> [!NOTE]
> benzersiz konak, null ile sonlandırılmış bir dize olmalıdır.

> [!NOTE]
> Bu hizmet kullanımdan kaldırılmıştır. Geliştiricilerin *nx_pppoe_client_host_uniq_set_extended ()* uygulamasına geçirilmesi önerilir.

### <a name="input-parameters"></a>Giriş Parametreleri

 - **pppoe_client_ptr** PPPoE Istemci denetim bloğu işaretçisi.
 - **host_uniq** Benzersiz bir ana bilgisayar işaretçisi. Benzersiz konak, null ile sonlandırılmış bir dize olmalıdır.

### <a name="return-values"></a>Dönüş Değerleri

 - **NX_PPPOE_CLIENT_SUCCESS** (0x00) başarılı PPPoE istemci ana bilgisayar benzersiz kümesi.
 - NX_PPPOE_CLIENT_PTR_ERROR (0xD1) geçersiz PPPoE Istemci işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Set service name for PPPoE Client instance “my_pppoe_client”. */
status =  nx_pppoe_client_host_uniq_set(&my_pppoe_client,
“220000000000000041000000”);

/* If status is NX_PPPOE_CLIENT_SUCCESS, the “my_pppoe_client” host unique has set. */
```

## <a name="nx_pppoe_client_host_uniq_set_extended"></a>nx_pppoe_client_host_uniq_set_extended

PPPoE Istemci konağını benzersiz ayarla

### <a name="prototype"></a>Prototype

```c
UINT nx_pppoe_client_host_uniq_set_extended(
                        NX_PPPOE_CLIENT *pppoe_client_ptr,
                        UCHAR *host_uniq,UINT host_uniq_length);
```

### <a name="description"></a>Açıklama

Bu hizmet, PPPoE Istemci konağını benzersiz olarak ayarlar. Host-Uniq, bir ana bilgisayar tarafından bir erişim yoğunlaştırıcıyı belirli bir ana bilgisayar isteğiyle benzersiz bir şekilde ilişkilendirmek için kullanılır.
Bu, konağın seçtiği herhangi bir değerin ve uzunluğun ikili verileri olabilir.

> [!NOTE]
> benzersiz konak, null ile sonlandırılmış bir dize olmalıdır.

> [!NOTE]
> Bu hizmet *nx_pppoe_client_host_uniq_set ()* yerini alır. Bu sürüm, hizmete ek uzunluk bilgileri sağlar.

### <a name="input-parameters"></a>Giriş Parametreleri

 - **pppoe_client_ptr** PPPoE Istemci denetim bloğu işaretçisi.
 - **host_uniq** Benzersiz bir ana bilgisayar işaretçisi. Benzersiz konak, null ile sonlandırılmış bir dize olmalıdır.
 - **host_uniq_length** Host_uniq uzunluğu

### <a name="return-values"></a>Dönüş Değerleri

 - **NX_PPPOE_CLIENT_SUCCESS** (0x00) başarılı PPPoE istemci ana bilgisayar benzersiz kümesi.
 - **NX_PPPOE_CLIENT_PTR_ERROR** (0Xd1) geçersiz PPPoE istemci işaretçisi.
 - **NX_SIZE_ERROR** (0x09) denetim host_uniq_length başarısız oldu

### <a name="allowed-from"></a>İzin verilen

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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

PPPoE Istemci oturumunu bağlama

### <a name="prototype"></a>Prototype

```c
UINT nx_pppoe_client_session_connect(NX_PPPOE_CLIENT *pppoe_client_ptr,
                                    ULONG wait_option);
```

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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
