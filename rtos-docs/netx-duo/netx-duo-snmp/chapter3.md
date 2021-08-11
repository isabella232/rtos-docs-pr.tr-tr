---
title: Bölüm 3 - NetX Duo Azure RTOS SNMP aracı hizmetlerinin açıklaması
description: Bu bölümde, tüm NetX Duo SNMP Aracısı hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: b24776c2eb25a53195ea4eb452497b23b933e4ab3f9f0a379ea64d8469c1c971
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116790136"
---
# <a name="chapter-3---description-of-azure-rtos-netx-duo-snmp-agent-services"></a>Bölüm 3 - NetX Duo Azure RTOS SNMP aracı hizmetlerinin açıklaması

Bu bölümde tüm NetX Duo SNMP Azure RTOS hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklaması yer almaktadır.

Aşağıdaki API açıklamalarında yer alan "Dönüş Değerleri" bölümünde, **KALıN**  olmayan değerler tamamen devre dışı bırakılırken, BOLD NX_DISABLE_ERROR_CHECKING API hata denetimlerini devre dışı bırakmak için kullanılan tanımdan etkilenmez.

- [nx_snmp_agent_auth_trap_key_use](#nx_snmp_agent_auth_trap_key_use)
   - *Yakalama iletileri için kimlik doğrulama anahtarını (yalnızca SNMP v3) belirtme*
- [nx_snmp_agent_authenticate_key_use](#nx_snmp_agent_authenticate_key_use)
   - *Yanıt iletileri için kimlik doğrulama anahtarını (yalnızca SNMP v3) belirtme*
- [nx_snmp_agent_community_get](#nx_snmp_agent_community_get)
   - *Topluluk adını alma*
- [nx_snmp_agent_context_engine_set](#nx_snmp_agent_context_engine_set)
   - *Bağlam altyapısını ayarlama (yalnızca SNMP v3)*
- [nx_snmp_agent_context_name_set](#nx_snmp_agent_context_name_set)
   - *Bağlam adını ayarlama (yalnızca SNMP v3)*
- [nx_snmp_agent_create](#nx_snmp_agent_create)
   - *SNMP aracısı oluşturma*
- [nx_snmp_agent_current_version_get](#nx_snmp_agent_current_version_get)
   - *Alınan paketin SNMP sürümünü alın*
- [nx_snmp_agent_request_get_type_test](#nx_snmp_agent_request_get_type_test)
   - *Son SNMP isteğinin GET veya SET türü olduğunu belirt*
- [nx_snmp_agent_private_string_test](#nx_snmp_agent_private_string_test)
   - *Dizenin aracı özel dizesiyle eş olup olmadığını belirleme*
- [nx_snmp_agent_public_string_test](#nx_snmp_agent_public_string_test)
   - *Dizenin aracı ortak dizesiyle eş olup olmadığını belirleme*
- [nx_snmp_agent_set_interface](#nx_snmp_agent_set_interface)
   - *SNMP mesajlaşması için ağ arabirimi ayarlama*
- [nx_snmp_agent_private_string_set](#nx_snmp_agent_private_string_set)
   - *SNMP aracısı özel topluluk dizesini ayarlama*
- [nx_snmp_agent_public_string_set](#nx_snmp_agent_public_string_set)
   - *SNMP aracısı genel topluluk dizesini ayarlama*
- [nx_snmp_agent_version_set](#nx_snmp_agent_version_set)
   - *Tüm SNMP sürümleri için SNMP aracı durumunu ayarlama*
- [nx_snmp_agent_delete](#nx_snmp_agent_delete)
   - *SNMP aracıyı silme*
- [nx_snmp_agent_md5_key_create](#nx_snmp_agent_md5_key_create)
   - *Md5 anahtarı oluşturma (yalnızca SNMP v3)*
- [nx_snmp_agent_md5_key_create_extended](#nx_snmp_agent_md5_key_create_extended)
   - *Md5 anahtarı oluşturma (yalnızca SNMP v3)*
- [nx_snmp_agent_priv_trap_key_use](#nx_snmp_agent_priv_trap_key_use)
   - *Yakalama iletileri için şifreleme anahtarını (yalnızca SNMP v3) belirtme*
- [nx_snmp_agent_privacy_key_use](#nx_snmp_agent_privacy_key_use)
   - *Yanıt iletileri için şifreleme anahtarını (yalnızca SNMP v3) belirtme*
- [nx_snmp_agent_sha_key_create](#nx_snmp_agent_sha_key_create)
   - *Sha anahtarı oluşturma (yalnızca SNMP v3)*
- [nx_snmp_agent_sha_key_create_extended](#nx_snmp_agent_sha_key_create_extended)
   - *Sha anahtarı oluşturma (yalnızca SNMP v3)*
- [nx_snmp_agent_start](#nx_snmp_agent_start)
   - *SNMP aracıyı başlatma*
- [nx_snmp_agent_stop](#nx_snmp_agent_stop)
   - *SNMP aracıyı durdurma*
- [nx_snmp_agent_trap_send](#nx_snmp_agent_trap_send)
   - *SNMP v1 yakalaması gönderme (yalnızca IPv4)*
- [nx_snmp_agent_trapv2_send](#nx_snmp_agent_trapv2_send)
   - *SNMP v2 yakalaması gönderme (yalnızca IPv4)*
- [nx_snmp_agent_trapv2_oid_send](#nx_snmp_agent_trapv2_oid_send)
   - *OID'i belirten SNMP v2 yakalaması gönderme (yalnızca IPv4)*
- [nx_snmp_agent_trapv3_send](#nx_snmp_agent_trapv3_send)
   - *SNMP v3 yakalaması gönderme (yalnızca IPv4)*
- [nx_snmp_agent_trapv3_oid_send](#nx_snmp_agent_trapv3_oid_send)
   - *OID'i belirten SNMP v2 yakalaması gönderme (yalnızca IPv4)*
- [nxd_snmp_agent_trap_send](#nxd_snmp_agent_trap_send)
   - *SNMP v1 yakalaması gönderme (IPv4 ve IPv6)*
- [nxd_snmp_agent_trapv2_send](#nxd_snmp_agent_trapv2_send)
   - *SNMP v2 yakalaması gönderme (IPv4 ve IPv6)*
- [nxd_snmp_agent_trapv2_oid_send](#nxd_snmp_agent_trapv2_oid_send)
   - *OID'i belirten SNMP v2 yakalaması (IPv4/IPv6) gönderme*
- [nxd_snmp_agent_trapv3_send](#nxd_snmp_agent_trapv3_send)
   - *SNMP v3 yakalaması gönderme (IPv4 ve IPv6)*
- [nxd_snmp_agent_trapv3_oid_send](#nxd_snmp_agent_trapv3_oid_send)
   - *OID'i belirten SNMP v2 yakalaması (IPv4/IPv6) gönderme*
- [nx_snmp_agent_v3_context_boots_set](#nx_snmp_agent_v3_context_boots_set)
   - *Yeniden başlatma sayısını ayarlama*
- [nx_snmp_object_compare](#nx_snmp_object_compare)
   - *İki nesne karşılaştırma*
- [nx_snmp_object_compare_extended](#nx_snmp_object_compare_extended)
   - *İki nesne karşılaştırma*
- [nx_snmp_object_copy](#nx_snmp_object_copy)
   - *Bir nesneyi kopyalama*
- [nx_snmp_object_copy_extended](#nx_snmp_object_copy_extended)
   - *Bir nesneyi kopyalama*
- [nx_snmp_object_counter_get](#nx_snmp_object_counter_get)
   - *Sayaç nesnesini al*
- [nx_snmp_object_counter_set](#nx_snmp_object_counter_set)
   - *Sayaç nesnesini ayarlama*
- [nx_snmp_object_counter64_get](#nx_snmp_object_counter64_get)
   - *64 bit sayaç nesnesi al*
- [nx_snmp_object_counter64_set](#nx_snmp_object_counter64_set)
   - *64 bit sayaç nesnesi ayarlama*
- [nx_snmp_object_end_of_mib](#nx_snmp_object_end_of_mib)
   - *Mib sonu değerini ayarlama*
- [nx_snmp_object_gauge_get](#nx_snmp_object_gauge_get)
   - *Ölçer nesnesini al*
- [nx_snmp_object_gauge_set](#nx_snmp_object_gauge_set)
   - *Ölçer nesnesini ayarlama*
- [nx_snmp_object_id_get](#nx_snmp_object_id_get)
   - *Nesne kimliğini al*
- [nx_snmp_object_id_set](#nx_snmp_object_id_set)
   - *Nesne kimliğini ayarlama*
- [nx_snmp_object_integer_get](#nx_snmp_object_integer_get)
   - *Tamsayı nesnesi Al*
- [nx_snmp_object_integer_set](#nx_snmp_object_integer_set)
   - *Tamsayı nesnesini ayarla*
- [nx_snmp_object_ip_address_get](#nx_snmp_object_ip_address_get)
   - *IP adresi nesnesi Al (yalnızca IPv4)*
- [nx_snmp_object_ip_address_set](#nx_snmp_object_ip_address_set)
   - *IP adresi nesnesini ayarla (yalnızca IPv4)*
- [nx_snmp_object_ipv6_address_get](#nx_snmp_object_ipv6_address_get)
   - *IP adresi nesnesi Al (yalnızca IPv6)*
- [nx_snmp_object_ipv6_address_set](#nx_snmp_object_ipv6_address_set)
   - *IP adresi nesnesini ayarla (yalnızca IPv6)*
- [nx_snmp_object_no_instance](#nx_snmp_object_no_instance)
   - *Örnek olmayan değer ayarla*
- [nx_snmp_object_not_found](#nx_snmp_object_not_found)
   - *Not Found değeri ayarla*
- [nx_snmp_object_octet_string_get](#nx_snmp_object_octet_string_get)
   - *Sekizli dize nesnesi Al*
- [nx_snmp_object_octet_string_set](#nx_snmp_object_octet_string_set)
   - *Sekizli dize nesnesi ayarla*
- [nx_snmp_object_string_get](#nx_snmp_object_string_get)
   - *ASCII dize nesnesi Al*
- [nx_snmp_object_string_set](#nx_snmp_object_string_set)
   - *ASCII dize nesnesi ayarla*
- [nx_snmp_object_timetics_get](#nx_snmp_object_timetics_get)
   - *Timetika nesnesini Al*
- [nx_snmp_object_timetics_set](#nx_snmp_object_timetics_set)
   - *Timetika nesnesini ayarla*

## <a name="nx_snmp_agent_auth_trap_key_use"></a>nx_snmp_agent_auth_trap_key_use
Tuzak iletileri için kimlik doğrulama anahtarını belirt

### <a name="prototype"></a>Prototype

```c
UINT nx_snmp_agent_auth_trap_key_use(NX_SNMP_AGENT *agent_ptr, 
                                     NX_SNMP_SECURITY_KEY *key);
```
### <a name="description"></a>Description

Bu hizmet, tuzak iletilerindeki SNMPv3 güvenlik üstbilgisinde kimlik doğrulama parametrelerini ayarlamak için kullanılacak anahtarı belirtir. Anahtar için bir NX_NULL değeri sağlamak, kimlik doğrulamasını devre dışı bırakır.

> [!NOTE]
> Anahtarın önceden oluşturulması gerekir. Bkz. nx_snmp_agent_md5_key_create veya nx_snmp_agent_sha_key_create.

### <a name="input-parameters"></a>Giriş Parametreleri

- **agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.
- **anahtar** Daha önce oluşturulmuş bir MD5 veya SHA anahtarı işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı kimlik doğrulama anahtarı kümesi.
- **NX_NOT_ENABLED** (0x14) SNMP güvenliği devre dışı 
- **NX_PTR_ERROR** (0x07) geçersiz SNMP aracı işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, Iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Use previously created “my_key” for SNMPv3 trap message authentication.  */
status =  nx_snmp_agent_auth_trap_key_use(&my_agent, &my_key);


/* If status is NX_SUCCESS the SNMP Agent will use “my_key” for
   for authentication parameters in trap messages.  */
```

## <a name="nx_snmp_agent_authenticate_key_use"></a>nx_snmp_agent_authenticate_key_use
Yanıt iletileri için kimlik doğrulama anahtarını belirtin

### <a name="prototype"></a>Prototype

```c
UINT nx_snmp_agent_authenticate_key_use(NX_SNMP_AGENT *agent_ptr, 
                                        NX_SNMP_SECURITY_KEY *key);
```
### <a name="description"></a>Description

Bu hizmet, ayarlandıktan sonra yapılan tüm istekler için SNMPv3 güvenlik parametresindeki kimlik doğrulama parametreleri için kullanılacak anahtarı belirtir. Anahtar için bir NX_NULL değeri sağlamak, kimlik doğrulamasını devre dışı bırakır.

> [!NOTE]
> Anahtarın önceden oluşturulması gerekir. Bkz. nx_snmp_agent_md5_key_create veya nx_snmp_agent_sha_key_create.

### <a name="input-parameters"></a>Giriş Parametreleri

- **agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.
- **anahtar** Daha önce oluşturulmuş bir MD5 veya SHA anahtarı işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı SNMP anahtar kümesi.
- **NX_NOT_ENABLED** (0x14) SNMP güvenliği devre dışı
- **NX_PTR_ERROR** (0x07) geçersiz SNMP aracı işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, Iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Use previously created “my_key” for SNMPv3 authentication.  */
status =  nx_snmp_agent_authenticate_key_use(&my_agent, &my_key);


/* If status is NX_SUCCESS the SNMP Agent will use “my_key” for
   for setting the authentication parameters of SNMPv3 requests.  */
```

## <a name="nx_snmp_agent_community_get"></a>nx_snmp_agent_community_get
Topluluk adını al

### <a name="prototype"></a>Prototype

```c
UINT nx_snmp_agent_community_get(NX_SNMP_AGENT *agent_ptr, 
                                 UCHAR **community_string_ptr);
```

### <a name="description"></a>Description

Bu hizmet, topluluk adını SNMP Aracısı tarafından alınan en son SNMP isteğinden alır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.
- **community_string_ptr** SNMP Aracısı topluluk dizesini döndürmek için bir dize işaretçisine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı SNMP topluluğu Get.
- **NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, Iş parçacıkları

### <a name="example"></a>Örnek

```c
UCHAR *string_ptr;

/* Pickup the community string pointer for my_agent.  */
status =  nx_snmp_agent_community_get(&my_agent, &string_ptr);


/* If status is NX_SUCCESS the pointer “string_ptr” points to the
   last community name supplied to the SNMP agent.  */
```

## <a name="nx_snmp_agent_request_get_type_test"></a>nx_snmp_agent_request_get_type_test
Son SNMP isteğinin Al veya ayarla türü olduğunu belirtir

### <a name="prototype"></a>Prototype

```c
UINT nx_snmp_agent_request_get_type_test(NX_SNMP_AGENT *agent_ptr,
                                         UINT *is_get_type);
```

### <a name="description"></a>Description

Bu hizmet, SNMP Yöneticisi 'ndeki en son isteğin bir GET (GET, GETNEXT veya GETBULK) veya SET türünde olup olmadığını gösterir. İstek bir GET türüdür veya istek bir küme türü ise SNMP Aracısı özel dizesinde, SNMPv1 veya SNMPv2 uygulamasının alınan topluluk dizesini SNMP Aracısı ortak dizesiyle karşılaştırmak isteyeceğini, Kullanıcı adı geri çağırması ile kullanılması amaçlanmıştır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.
- **is_get_type** İstek türü durumu işaretçisi:  
Tür al NX_TRUE  
Tür AYARLANDıYSA NX_FALSE

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarıyla döndürülen tür
- **NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, Iş parçacıkları

### <a name="example"></a>Örnek

```c
UINT is_get_type;

/* Determine if the current SNMP request is a GET or SET type.  */
status =  nx_snmp_agent_request_get_type_test(&my_agent, &is_get_type);


/* If status is NX_SUCCESS, is_get_type will indicate the request type.  */
```

## <a name="nx_snmp_agent_context_engine_set"></a>nx_snmp_agent_context_engine_set
Bağlam altyapısını ayarla (yalnızca SNMP v3)

### <a name="prototype"></a>Prototype

```c
UINT nx_snmp_agent_context_engine_set(NX_SNMP_AGENT *agent_ptr, 
                                      UCHAR *context_engine, 
                                      UINT context_engine_size);
```
### <a name="description"></a>Description

Bu hizmet SNMP aracısının bağlam altyapısını ayarlar. Yalnızca SNMPv3 işleme için geçerlidir. Uygulama kimlik doğrulaması ve şifreleme kullanıyorsa, anahtar oluşturma işlemi bağlam altyapısı kimliği kullanılırken güvenlik anahtarları oluşturmadan önce bu çağrıl kullanılmalıdır. Yoksa NetX Duo SNMP, *nxd_snmp.c'nin* üst kısmında varsayılan bir bağlam altyapısı kimliği sağlar:

```c
UCHAR _nx_snmp_default_context_engine[NX_SNMP_MAX_CONTEXT_STRING] =  
                {0x80, 0x00, 0x03, 0x10, 0x01, 0xc0, 0xa8, 0x64, 0xaf};

```

### <a name="input-parameters"></a>Giriş Parametreleri

- **agent_ptr** SNMP Aracısı denetim bloğuna işaretçi.
- **context_engine** Bağlam altyapısı dizesinin işaretçisi.
- **context_engine_size** Bağlam altyapısı dizesinin boyutu. Bir bağlam altyapısında bayt sayısı üst sayısının bir NX_SNMP_MAX_CONTEXT_STRING.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı SNMP bağlam altyapısı kümesi.
- **NX_NOT_ENABLED** (0x14) SNMPv3 etkin değil
- **NX_SNMP_ERROR** (0x100) Bağlam altyapısı boyutu hatası.
- **NX_PTR_ERROR** (0x07) Geçersiz giriş işaretçisi.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, İş Parçacıkları

### <a name="example"></a>Örnek

```c
UCHAR my_engine[] = {0x80, 0x00, 0x01, 0x02, 0x03, 0x04, 0x05, 0x06, 0x07};

/* Set the context engine for my_agent.  */
status =  nx_snmp_agent_context_engine_set(&my_agent, my_engine, 9);


/* If status is NX_SUCCESS the context engine has been set.  */
```
## <a name="nx_snmp_agent_context_name_set"></a>nx_snmp_agent_context_name_set
Bağlam adını ayarlama (yalnızca SNMP v3)

### <a name="prototype"></a>Prototype

```c
UINT nx_snmp_agent_context_name_set(NX_SNMP_AGENT *agent_ptr, 
                                    UCHAR *context_name, 
                                    UINT context_name_size);
```

### <a name="description"></a>Description

Bu hizmet, SNMP Aracısı'nın bağlam adını ayarlar. Yalnızca SNMPv3 işleme için geçerlidir. Çağrılmazsa NetX Duo SNMP Aracısı bağlam adını boş bırakır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **agent_ptr** SNMP Aracısı denetim bloğuna işaretçi.
- **context_name** Bağlam adı dizesinin işaretçisi.
- **context_name_size** Bağlam adı dizesinin boyutu. Bir bağlam adı içinde bayt sayısı üst NX_SNMP_MAX_CONTEXT_STRING.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı SNMP bağlam adı kümesi.
- **NX_SNMP_ERROR** (0x100) Bağlam adı boyutu hatası.
- **NX_PTR_ERROR** (0x07) Geçersiz giriş işaretçisi.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Set the context name for my_agent.  */
status =  nx_snmp_agent_context_name_set(&my_agent, “my_context_name”, 15);


/* If status is NX_SUCCESS the context name has been set.  */
```

## <a name="nx_snmp_agent_create"></a>nx_snmp_agent_create
SNMP aracısı oluşturma

### <a name="prototype"></a>Prototype

```c
UINT nx_snmp_agent_create(NX_SNMP_AGENT *agent_ptr, 
      CHAR *snmp_agent_name, NX_IP *ip_ptr, VOID *stack_ptr, 
      ULONG stack_size, NX_PACKET_POOL *pool_ptr,
      UINT (*snmp_agent_username_process)(struct NX_SNMP_AGENT_STRUCT 
                                    *agent_ptr, UCHAR *username),
      UINT (*snmp_agent_get_process)(struct NX_SNMP_AGENT_STRUCT 
                  *agent_ptr, UCHAR *object_requested, 
                  NX_SNMP_OBJECT_DATA *object_data),
      UINT (*snmp_agent_getnext_process)(struct NX_SNMP_AGENT_STRUCT 
                  *agent_ptr, UCHAR *object_requested, 
                  NX_SNMP_OBJECT_DATA *object_data),
      UINT (*snmp_agent_set_process)(struct NX_SNMP_AGENT_STRUCT 
                  *agent_ptr, UCHAR *object_requested, 
                  NX_SNMP_OBJECT_DATA *object_data));
```
### <a name="description"></a>Description

Bu hizmet, belirtilen IP örneğinde bir SNMP Aracısı oluşturur.

### <a name="input-parameters"></a>Giriş Parametreleri

- **agent_ptr** SNMP Aracısı denetim bloğuna işaretçi.
- **snmp_agent_name** SNMP Aracısı ad dizesinin işaretçisi.
- **ip_ptr** IP örneğine işaretçi.
- **stack_ptr** SNMP Aracısı iş parçacığı yığını işaretçisi işaretçisi.
- **stack_size** Bayt cinsinden yığın boyutu.
- **pool_ptr** Bu SNMP Aracısı için varsayılan paket havuzunu işaretçi.
- **snmp_agent_username_process** Uygulamanın kullanıcı adı işleme yordamına işlev işaretçisi.
- **snmp_agent_get_process** Uygulamanın GET isteği işleme yordamına işlev işaretçisi.
- **snmp_agent_getnext_process** Uygulamanın GETNEXT istek işleme yordamına işlev işaretçisi.
- **snmp_agent_set_process** Uygulamanın SET isteği işleme yordamına işlev işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı SNMP Aracısı oluşturma.
- **NX_SNMP_ERROR** (0x100) SNMP Aracısı oluşturma hatası.
- **NX_PTR_ERROR** (0x07) Geçersiz giriş işaretçisi.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, İş Parçacıkları

### <a name="example"></a>Örnek

```c
NX_SNMP_AGENT my_agent;

/* Create the SNMP Agent “my_agent.”  */
status =  nx_snmp_agent_create(&my_agent, "My SNMP Agent", &ip_0, stack_start_ptr,
                4096, &pool_0, my_username_processing, my_get_processing, 
                my_getnext_processing, my_set_processing);


/* If status is NX_SUCCESS the SNMP Agent “my_agent” has been created.  */
```

## <a name="nx_snmp_agent_current_version_get"></a>nx_snmp_agent_current_version_get
SNMP paket sürümünü alın

### <a name="prototype"></a>Prototype

```c
UINT nx_snmp_agent_current_version_get(NX_SNMP_AGENT *agent_ptr, 
                                       UINT *version);
```

### <a name="description"></a>Description

Bu hizmet alınan en son SNMP paketinden ayrıştıran SNMP sürümünü aldı.

### <a name="input-parameters"></a>Giriş Parametreleri

- **agent_ptr** SNMP Aracısı denetim bloğuna işaretçi.
- **sürüm** Alınan SNMP paketinden ayrıştırilen SNMP sürümünün işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı SNMP sürümü get
- **NX_PTR_ERROR** (0x07) Geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
UINT          snmp_version;
NX_SNMP_AGENT my_agent;

/* Get the version of the last received SNMP packet. */
status =  nx_snmp_agent_current_version_get (&my_agent, &snmp_version);


/* If status is NX_SUCCESS, snmp_version contains 
   the received packet SNMP version.  */
```

## <a name="nx_snmp_agent_private_string_test"></a>nx_snmp_agent_private_string_test
Özel dizenin Aracı özel dizesiyle eş olduğunu doğrulama

### <a name="prototype"></a>Prototype

```c
UINT nx_snmp_agent_private_string_test(NX_SNMP_AGENT *agent_ptr, 
                                       UCHAR *community_string,          
                                       UINT *is_private);
```

### <a name="description"></a>Description

Bu hizmet, null sonlandırılan giriş topluluğu dizesini SNMP aracısı özel dizesiyle karşılaştırıldığında bunların eş olup olamalarını gösterir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **agent_ptr** SNMP Aracısı denetim bloğuna işaretçi.
- **community_string** Karşılaştırmak için dize işaretçisi
- **is_private** Karşılaştırma sonucu işaretçisi  
NX_TRUE - dize eşleşmeleri  
NX_FALSE - dize eşle değil

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı karşılaştırma
- **NX_PTR_ERROR** (0x07) Geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
UINT        is_private;
UCHAR       *community_string_ptr;
NX_SNMP_AGENT   my_agent;

/* Determine if the community string matches the agent private string */
status =  nx_snmp_agent_private_string_test(&my_agent, community_string_ptr,  
                                            &is_private);


/* If status is NX_SUCCESS, is_private will indicate if there is a match. 
   If is_private is NX_TRUE, they match.  */
```

## <a name="nx_snmp_agent_public_string_test"></a>nx_snmp_agent_public_string_test
Alınan ortak dizenin Aracı'nın ortak dizesiyle eş olduğunu doğrulama

### <a name="prototype"></a>Prototype

```c
UINT nx_snmp_agent_public_string_test(NX_SNMP_AGENT *agent_ptr, 
                                      UCHAR *community_string,          
                                      UINT *is_public);
```
### <a name="description"></a>Description

Bu hizmet, null sonlandırılan bir giriş topluluğu dizesini SNMP aracısı genel dizesiyle karşılaştırıldığında bunların eş olup olamaylarını gösterir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **agent_ptr** SNMP Aracısı denetim bloğuna işaretçi.
- **community_string** Karşılaştırmak için dize işaretçisi
- **is_public** Karşılaştırma sonucu işaretçisi  
NX_TRUE - dize eşleşmeleri  
NX_FALSE - dize eşle değil

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı karşılaştırma
- **NX_PTR_ERROR** (0x07) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
UINT        is_public;
UCHAR       *community_string_ptr;
NX_SNMP_AGENT   my_agent;


/* Determine if the community string matches the agent public string */
status =  nx_snmp_agent_public_string_test(&my_agent, community_string_ptr,  
                                           &is_public);


/* If status is NX_SUCCESS, is_public will indicate if there is a match. 
   If is_public is true they match.  */
```

## <a name="nx_snmp_agent_version_set"></a>nx_snmp_agent_version_set
Her SNMP sürümü için SNMP aracı durumunu ayarla

### <a name="prototype"></a>Prototype

```c
UINT nx_snmp_agent_version_set(NX_SNMP_AGENT *agent_ptr, 
                               UINT enabled_v1, UINT enable_v2, 
                               UINT enable_v3);
```

### <a name="description"></a>Description

Bu hizmet SNMP aracısındaki her bir SNMP sürümü, v1, v2 ve v3 için durumu (etkin/devre dışı) ayarlar. Kullanıcı tarafından yapılandırılabilir seçenekler, NX_SNMP_DISABLE_V1, NX_SNMP_DISABLE_V2 ve NX_SNMP_DISABLE_V3, bu çalışma zamanı ayarlarını geçersiz kıldığını unutmayın. Varsayılan olarak, SNMP Aracısı üç sürüm için etkinleştirilmiştir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.
- **enabled_v1** SNMP v1 için etkin durumu açık/kapalı olarak ayarlar.
- **enabled_v2** SNMP v2 için etkin durumu açık/kapalı olarak ayarlar.
- **enabled_v3** SNMP v3 için etkin durumu açık/kapalı olarak ayarlar.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı SNMP sürümü kümesi
- **NX_PTR_ERROR** (0x07) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
UINT          v1_on = NX_TRUE;
UINT          v2_on = NX_TRUE;
UINT          v3_on = NX_FALSE;

NX_SNMP_AGENT my_agent;

/* Enable/Disable each SNMP protocol (version) for the SNMP Agent) */
status =  nx_snmp_agent_version_set(&my_agent, v1_on, v2_on, v3_on);


/* If status is NX_SUCCESS, my_agent is enabled only for V1 and V2 assuming 
   NX_SNMP_DISABLE_V1 and NX_SNMP_DISABLE_V2 are not defined. */
```

## <a name="nx_snmp_agent_private_string_set"></a>nx_snmp_agent_private_string_set
SNMP Aracısı özel dizesini ayarla

### <a name="prototype"></a>Prototype

```c
UINT nx_snmp_agent_private_string_set(NX_SNMP_AGENT *agent_ptr, 
                                      UCHAR *community_string);
```

### <a name="description"></a>Description

Bu hizmet SNMP Aracısı özel topluluk dizesini girdi null sonlandırılmış dizesiyle ayarlar. Varsayılan değer NULL (özel dize kümesi yoktur), "özel" topluluk dizesiyle alınan tüm SNMP paketleri, okuma/yazma erişimi için SNMP Aracısı tarafından kabul edilmez. Giriş dizesi Kullanıcı tarafından yapılandırılabilir NX_SNMP_MAX_USER_NAME-1 ' e eşit veya ondan küçük olmalıdır (null sonlandırma için odaya izin vermek için) boyutu.

### <a name="input-parameters"></a>Giriş Parametreleri

- **agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.
- **community_string** Atanacak özel dizeye yönelik işaretçi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) özel dize başarıyla ayarlandı
- **NX_SNMP_ERROR_TOOBIG** (0x01) dize boyutu çok büyük 
- **NX_PTR_ERROR** (0x07) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
NX_SNMP_AGENT my_agent;

/* Set the SNMP agent’s private community string */
status =  nx_snmp_agent_private_string_set(&my_agent, “private”));


/* If status is NX_SUCCESS, the SNMP agent private string is set.  */
```

## <a name="nx_snmp_agent_public_string_set"></a>nx_snmp_agent_public_string_set
SNMP Aracısı genel dizesini ayarla

### <a name="prototype"></a>Prototype

```c
UINT nx_snmp_agent_public_string_set(NX_SNMP_AGENT *agent_ptr, 
                                     UCHAR *community_string);
```

### <a name="description"></a>Description

Bu hizmet SNMP Aracısı ortak topluluk dizesini girdi null sonlandırılmış dizesiyle ayarlar. Topluluk dizesi, Kullanıcı tarafından yapılandırılabilir NX_SNMP_MAX_USER_NAME-1 ' e eşit veya ondan küçük olmalıdır (null sonlandırma için odaya izin vermek için) boyutu.

### <a name="input-parameters"></a>Giriş Parametreleri

- **agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.
- **community_string** Atanacak ortak dizenin işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) genel dize başarıyla ayarlandı
- **NX_SNMP_ERROR_TOOBIG** (0x01) dize boyutu çok büyük
- **NX_PTR_ERROR** (0x07) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
NX_SNMP_AGENT my_agent;

/* Set the SNMP agent’s public string. */
nx_snmp_agent_public_string_set(&my_agent, “my_public”));


/* If status is NX_SUCCESS, the SNMP agent public string is set.  */
```

## <a name="nx_snmp_agent_delete"></a>nx_snmp_agent_delete
SNMP aracısını Sil

### <a name="prototype"></a>Prototype

```C
UINT nx_snmp_agent_delete(NX_SNMP_AGENT *agent_ptr);
```
### <a name="description"></a>Description

Bu hizmet önceden oluşturulmuş bir SNMP aracısını siler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı SNMP Aracısı silme.
- **NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, Iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Delete the SNMP Agent “my_agent.”  */
status =  nx_snmp_agent_delete(&my_agent);


/* If status is NX_SUCCESS the SNMP Agent “my_agent” has been deleted.  */
```

## <a name="nx_snmp_agent_set_interface"></a>nx_snmp_agent_set_interface
SNMP Aracısı ağ arabirimini ayarlama

### <a name="prototype"></a>Prototype

```c
UINT nx_snmp_agent_set_interface(NX_SNMP_AGENT *agent_ptr,  
                                 UINT if_index);
```

### <a name="description"></a>Description

Bu hizmet, SNMP aracısının SNMP ağ arabirimini giriş arabirimi dizini tarafından belirtilen şekilde ayarlar. Bu, yalnızca NetX Duo 5,6 veya üzeri olan SNMP ana bilgisayar uygulamaları için çok sayıda ağ arabirimini destekledikleri için yararlıdır. Ana bilgisayar tarafından belirtilmemişse, birincil arabirim için varsayılan değer sıfırdır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.
- **If_index** SNMP arabirimini belirten Dizin.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı SNMP arabirimi kümesi.
- **NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, Iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Set the SNMP Agent “my_agent” to the secondary interface.  */
if_index = 1;
status =  nx_snmp_agent_set_interface(&my_agent, if_index);


/* If status is NX_SUCCESS the SNMP agent interface is set.  */
```

## <a name="nx_snmp_agent_md5_key_create"></a>nx_snmp_agent_md5_key_create
MD5 anahtarı oluştur (yalnızca SNMP v3)

### <a name="prototype"></a>Prototype

```c
UINT nx_snmp_agent_md5_key_create(NX_SNMP_AGENT *agent_ptr, 
                                  UCHAR *password, 
                                  NX_SNMP_SECURITY_KEY 
                                       *destination_key);
```
### <a name="description"></a>Description

Bu hizmet, kimlik doğrulama ve şifreleme için kullanılabilen bir MD5 anahtarı oluşturur.

Bu hizmet kullanımdan kaldırılmıştır. Geliştiricilerin *nx_snmp_agent_md5_key_create_extended ()* uygulamasına geçirilmesi önerilir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.
- **parola** Parola dizesi işaretçisi.
- **destination_key** SNMP anahtar veri yapısına yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı anahtar oluştur.
- **NX_NOT_ENABLED** (0x14) güvenlik etkin değil.
- **NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, Iş parçacıkları

### <a name="example"></a>Örnek

```c
NX_SNMP_SECURITY_KEY my_key;

/* Create the MD5 key for “my_agent.”   */
status =  nx_snmp_agent_md5_key_create(&my_agent, “authpw”, &my_key);


/* If status is NX_SUCCESS an MD5 key has been created.  */
```

## <a name="nx_snmp_agent_md5_key_create_extended"></a>nx_snmp_agent_md5_key_create_extended
MD5 anahtarı oluştur (yalnızca SNMP v3)

### <a name="prototype"></a>Prototype

```c
UINT nx_snmp_agent_md5_key_create_extended(NX_SNMP_AGENT *agent_ptr, 
                                           UCHAR *password, 
                                           UINT password_length,
                                           NX_SNMP_SECURITY_KEY 
                                           *destination_key);
```
### <a name="description"></a>Description

Bu hizmet, kimlik doğrulama ve şifreleme için kullanılabilen bir MD5 anahtarı oluşturur.

Bu hizmet *nx_snmp_agent_md5_key_create ()* yerini alır. Bu sürüm için çağıranın parola uzunluğu sağlaması gerekir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.
- **parola** Parola dizesi işaretçisi.
- **password_length** Parola dizesinin uzunluğu.
- **destination_key** SNMP anahtar veri yapısına yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı anahtar oluştur.
- **NX_NOT_ENABLED** (0x14) güvenlik etkin değil.
- **NX_SNMP_FAILED** (0x102) SNMP başarısız oldu.
- **NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, Iş parçacıkları

### <a name="example"></a>Örnek

```c
NX_SNMP_SECURITY_KEY my_key;

/* Create the MD5 key for “my_agent.”   */
status =  nx_snmp_agent_md5_key_create_extended(&my_agent, “authpw”, 6, &my_key);


/* If status is NX_SUCCESS the key for the password “authpw” has been created.  */
```

## <a name="nx_snmp_agent_priv_trap_key_use"></a>nx_snmp_agent_priv_trap_key_use
Tuzak iletileri için şifreleme anahtarı belirtin

### <a name="prototype"></a>Prototype

```c
UINT nx_snmp_agent_priv_trap_key_use(NX_SNMP_AGENT *agent_ptr, 
                                     NX_SNMP_SECURITY_KEY *key);
```

### <a name="description"></a>Description

Bu hizmet, önceden oluşturulmuş bir gizlilik anahtarının, SNMPv3 tuzak iletilerinin şifrelenmesi ve şifresinin çözülmesi için kullanıldığını belirtir.

> [!NOTE]
> *Authentictation anahtarının önceden oluşturulması gerekir. SNMP v3 gizliliği (şifreleme) kimlik doğrulaması gerektirir. Ayrıntılar için nx_snmp_agent_auth_trap_key_use bakın.*

### <a name="input-parameters"></a>Giriş Parametreleri

- **agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.
- **anahtar** Daha önce anahtar oluşturma işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı gizlilik anahtarı kümesi.
- **NX_NOT_ENABLED** (0x14) güvenlik etkin değil.
- **NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, Iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Use the “my_privacy_key” for the SNMP Agent “my_agent” trap messages.   */
status =  nx_snmp_agent_priv_trap_key_use(&my_agent, &my_privacy_key);


/* If status is NX_SUCCESS the privacy key is registered with the SNMP agent.  */
```

## <a name="nx_snmp_agent_privacy_key_use"></a>nx_snmp_agent_privacy_key_use
Yanıt iletileri için şifreleme anahtarı belirtin

### <a name="prototype"></a>Prototype

```c
UINT nx_snmp_agent_privacy_key_use(NX_SNMP_AGENT *agent_ptr, 
                                   NX_SNMP_SECURITY_KEY *key);
```
### <a name="description"></a>Description

Bu hizmet, önceden oluşturulmuş anahtarın, SNMPv3 yanıt iletilerinin şifrelenmesi ve şifresinin çözülmesi için kullanıldığını belirtir.

> [!NOTE]
> *Bir kimlik doğrulama anahtarı daha önce belirtilmiş olmalıdır. SNMP v3 şifrelemesi de bir kimlik doğrulama anahtarı oluşturulmasını gerektirir. Ayrıntılar için nx_snmp_agent_authentiation_key_use bakın.*

### <a name="input-parameters"></a>Giriş Parametreleri

- **agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.
- **anahtar** Daha önce anahtar oluşturma işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı gizlilik anahtarı kümesi.
- **NX_NOT_ENABLED** (0x14) güvenlik etkin değil.
- **NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, Iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Use the “my_privacy_key” for the SNMP Agent “my_agent.”   */
status =  nx_snmp_agent_privacy_key_use(&my_agent, &my_privacy_key);


/* If status is NX_SUCCESS the privacy key is registered with the SNMP agent.  */
```

## <a name="nx_snmp_agent_sha_key_create"></a>nx_snmp_agent_sha_key_create
SHA anahtarı oluştur (yalnızca SNMP v3)

### <a name="prototype"></a>Prototype

```c
UINT nx_snmp_agent_sha_key_create(NX_SNMP_AGENT *agent_ptr, 
                                  UCHAR *password, 
                                  NX_SNMP_SECURITY_KEY  
                                  *destination_key);
```
### <a name="description"></a>Description

Bu hizmet, kimlik doğrulama ve şifreleme için kullanılabilen bir SHA anahtarı oluşturur.

Bu hizmet kullanımdan kaldırılmıştır. Geliştiricilerin *nx_snmp_agent_sha_key_create_extended ()* uygulamasına geçirilmesi önerilir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.
- **parola** Parola dizesi işaretçisi.
- **destination_key** SNMP anahtar veri yapısına yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı anahtar oluştur.
- **NX_SNMP_ERROR** (0x100) anahtar oluşturma hatası.
- **NX_PTR_ERROR** (0x07) geçersiz SNMP Aracısı veya anahtar işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, Iş parçacıkları

### <a name="example"></a>Örnek

```c
NX_SNMP_SECURITY_KEY my_key;

/* Create the SHA key for “my_agent.”   */
status =  nx_snmp_agent_sha_key_create(&my_agent, “authpw”, &my_key);


/* If status is NX_SUCCESS the key for the password “authpw” has been created.  */
```

## <a name="nx_snmp_agent_sha_key_create_extended"></a>nx_snmp_agent_sha_key_create_extended
SHA anahtarı oluştur (yalnızca SNMP v3)

### <a name="prototype"></a>Prototype

```c
UINT nx_snmp_agent_sha_key_create_extended(NX_SNMP_AGENT *agent_ptr, 
                                           UCHAR *password, 
                                           UINT password_length,
                                           NX_SNMP_SECURITY_KEY  
                                           *destination_key);
```
### <a name="description"></a>Description

Bu hizmet, kimlik doğrulama ve şifreleme için kullanılabilen bir SHA anahtarı oluşturur.

Bu hizmet *nx_snmp_agent_sha_key_create ()* yerini alır. Bu sürüm için çağıranın parola uzunluğu sağlaması gerekir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.
- **parola** Parola dizesi işaretçisi.
- **password_length** Parola dizesinin uzunluğu.
- **destination_key** SNMP anahtar veri yapısına yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı anahtar oluştur.
- **NX_SNMP_ERROR** (0x100) anahtar oluşturma hatası.
- **NX_SNMP_FAILED** (0x102) anahtar oluşturulamadı.
- **NX_PTR_ERROR** (0x07) geçersiz SNMP Aracısı veya anahtar işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, Iş parçacıkları

### <a name="example"></a>Örnek

```c
NX_SNMP_SECURITY_KEY my_key;

/* Create the SHA key for “my_agent.”   */
status =  nx_snmp_agent_sha_key_create_extended(&my_agent, “authpw”, 6, &my_key);


/* If status is NX_SUCCESS the key for the password “authpw” has been created.  */
```

## <a name="nx_snmp_agent_start"></a>nx_snmp_agent_start
SNMP aracısını Başlat 

### <a name="prototype"></a>Prototype

```c
UINT nx_snmp_agent_start(NX_SNMP_AGENT *agent_ptr);
```
### <a name="description"></a>Description

Bu hizmet UDP yuvasını SNMP bağlantı noktası 161 ' e bağlar ve SNMP Aracısı iş parçacığı görevini başlatır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) SNMP aracısının başarıyla başlangıcı.
- **NX_SNMP_ERROR** (0x100) SNMP Aracısı başlatma hatası.
- **NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, Iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Start the previously created SNMP Agent “my_agent.”   */
status =  nx_snmp_agent_start(&my_agent);


/* If status is NX_SUCCESS the SNMP Agent “my_agent” has been started.  */
```
## <a name="nx_snmp_agent_stop"></a>nx_snmp_agent_stop
SNMP aracısını durdur 

### <a name="prototype"></a>Prototype

```c
UINT nx_snmp_agent_stop(NX_SNMP_AGENT *agent_ptr);
```
### <a name="description"></a>Description

Bu hizmet SNMP Aracısı iş parçacığı görevini durduruyor ve UDP yuvasının SNMP bağlantı noktasına bağlantısını kaldırır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) SNMP aracısının başarıyla durdurulması.
- **NX_PTR_ERROR** (0x07) geçersiz SNMP aracı işaretçisi.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Stop the previously created and started SNMP Agent “my_agent.”   */
status =  nx_snmp_agent_stop(&my_agent);


/* If status is NX_SUCCESS the SNMP Agent “my_agent” has been stopped.  */
```
## <a name="nx_snmp_agent_trap_send"></a>nx_snmp_agent_trap_send
SNMPv1 tuzağı gönder *(yalnızca IPv4)*

### <a name="prototype"></a>Prototype

```c
UINT nx_snmp_agent_trap_send(NX_SNMP_AGENT *agent_ptr, 
                             ULONG ip_address, UCHAR *enterprise, 
                             UINT trap_type, UINT trap_code, 
                             ULONG elapsed_time, 
                             NX_SNMP_TRAP_OBJECT *object_list_ptr);
```

### <a name="description"></a>Description

Bu hizmet, belirtilen IPv4 adresinde SNMP Yöneticisi 'ne SNMP tuzağı gönderir. NetX Duo 'da SNMP tuzağı göndermek için tercih edilen yöntem *nxd_snmp_agent_trap_send* hizmetini kullanmaktır. *nx_snmp_agent_trap_send* , mevcut NETX SNMP Aracısı uygulamalarını desteklemek üzere NETX Duo 'e dahildir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.
- **ip_address** SNMP yöneticisinin IPv4 adresi.
- **kurumsal** Enterprise nesne kimliği dizesi (sysObectID).
- **trap_type** İstenen tuzak türü, aşağıdaki gibi:  
   - NX_SNMP_TRAP_COLDSTART (0)  
   - NX_SNMP_TRAP_WARMSTART (1)  
   - NX_SNMP_TRAP_LINKDOWN (2)  
   - NX_SNMP_TRAP_LINKUP (3)  
   - NX_SNMP_TRAP_AUTHENTICATE_FAILURE (4)  
   - NX_SNMP_TRAP_EGPNEIGHBORLOSS (5)  

- **trap_code** Belirli tuzak kodu.
- **Elapsed_Time** Zaman sistemi (sysUpTime).
- **object_list_ptr** SNMP tuzağı dahil edilecek nesne dizisi ve bunlarla ilişkili değerler. Listenin sonlandırılması NX_NULL.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı SNMP tuzak gönderme.
- **NX_SNMP_ERROR** (0x100) SNMP tuzağı gönderme hatası.
- **NX_NOT_ENABLED** (0x14) SNMPv1 etkin değil.
- **NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
NX_SNMP_TRAP_OBJECT trap_list[5];

ULONG dest_ip_address = IP_ADDRESS(1,2,3,4);

/* Build list of objects to supply in the trap.  */
trap_list[0].nx_snmp_object_string_ptr =  "1.3.6.1.2.1.2.2.1.1.0";
trap_list[0].nx_snmp_object_data.nx_snmp_object_data_type =  NX_SNMP_INTEGER;
trap_list[0].nx_snmp_object_data.nx_snmp_object_data_msw =   counter;
trap_list[1].nx_snmp_object_string_ptr =  "1.3.6.1.2.1.1.3.0";
trap_list[1].nx_snmp_object_data.nx_snmp_object_data_type =  NX_SNMP_TIME_TICS;
trap_list[1].nx_snmp_object_data.nx_snmp_object_data_msw =   tx_time_get();
trap_list[2].nx_snmp_object_string_ptr =  NX_NULL; /* Terminate list!  */

/* Send trap to SNMP manager at 193.2.2.61.  */
status =  nx_snmp_agent_trap_send(&my_agent,dest_ip_address,
                                   "1.3.6.7.7.7", NX_SNMP_TRAP_LINKUP, counter++, 
                                  tx_time_get(), trap_list);

/* If status is NX_SUCCESS the SNMP trap has been sent.  */
```
## <a name="nxd_snmp_agent_trap_send"></a>nxd_snmp_agent_trap_send
SNMPv1 tuzağı gönderme *(IPv4 ve IPv6)*

### <a name="prototype"></a>Prototype

```c
UINT nxd_snmp_agent_trap_send(NX_SNMP_AGENT *agent_ptr, 
            ULONG ip_address, UCHAR *enterprise, UINT trap_type, 
            UINT trap_code, ULONG elapsed_time, 
            NX_SNMP_TRAP_OBJECT *object_list_ptr);
```
### <a name="description"></a>Description

Bu hizmet, belirtilen IP adresindeki SNMP Yöneticisi 'ne SNMP tuzağı gönderir. NetX 'te SNMP tuzağı göndermek için eşdeğer Yöntem *nxd_snmp_agent_trap_send* hizmetidir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.
- **ip_address** SNMP yöneticisinin IPv4 veya IPv6 adresi.
- **kurumsal** Enterprise nesne kimliği dizesi (sysObectID).
- **trap_type** İstenen tuzak türü, aşağıdaki gibi:  
   - NX_SNMP_TRAP_COLDSTART (0)
   - NX_SNMP_TRAP_WARMSTART (1)
   - NX_SNMP_TRAP_LINKDOWN (2)
   - NX_SNMP_TRAP_LINKUP (3)
   - NX_SNMP_TRAP_AUTHENTICATE_FAILURE (4)
   - NX_SNMP_TRAP_EGPNEIGHBORLOSS (5)

- **trap_code** Belirli tuzak kodu.
- **Elapsed_Time** Zaman sistemi (sysUpTime).
- **object_list_ptr** SNMP tuzağı dahil edilecek nesne dizisi ve bunlarla ilişkili değerler. Listenin sonlandırılması NX_NULL.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı SNMP tuzak gönderme.
- **NX_SNMP_ERROR** (0x100) SNMP tuzağı gönderme hatası.
- **NX_NOT_ENABLED** (0x14) SNMPv1 etkin değil.
- **NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
NX_SNMP_TRAP_OBJECT trap_list[5];

NXD_ADDRESS dest_ip_address;

    dest_ip_address.nxd_ip_version = NX_IP_VERSION_V6 ;
    dest_ip_address.nxd_ip_address.v6[0] = 0x20010db8;
    dest_ip_address.nxd_ip_address.v6[1] = 0xf101;
    dest_ip_address.nxd_ip_address.v6[2] = 0x00000000;
    dest_ip_address.nxd_ip_address.v6[3] = 0x00000101;

/* Build list of objects to supply in the trap.  */
trap_list[0].nx_snmp_object_string_ptr =  "1.3.6.1.2.1.2.2.1.1.0";
trap_list[0].nx_snmp_object_data.nx_snmp_object_data_type =  NX_SNMP_INTEGER;
trap_list[0].nx_snmp_object_data.nx_snmp_object_data_msw =   counter;
trap_list[1].nx_snmp_object_string_ptr =  "1.3.6.1.2.1.1.3.0";
trap_list[1].nx_snmp_object_data.nx_snmp_object_data_type =  NX_SNMP_TIME_TICS;
trap_list[1].nx_snmp_object_data.nx_snmp_object_data_msw =   tx_time_get();
trap_list[2].nx_snmp_object_string_ptr =  NX_NULL; /* Terminate list!  */

/* Send trap to SNMP manager at 193.2.2.61.  */
status =  nxd_snmp_agent_trap_send(&my_agent,&dest_ip_address,
                 "1.3.6.7.7.7", NX_SNMP_TRAP_LINKUP, counter++, tx_time_get(), 
               trap_list);

/* If status is NX_SUCCESS the SNMP trap has been sent.  */
```

## <a name="nx_snmp_agent_trapv2_send"></a>nx_snmp_agent_trapv2_send
SNMPv2 tuzak gönderme (yalnızca IPv4)

### <a name="prototype"></a>Prototype

```c
UINT nx_snmp_agent_trapv2_send(NX_SNMP_AGENT *agent_ptr, 
            NXD_ADDRESS *ip_address, UCHAR *community, UINT trap_type, 
            ULONG elapsed_time, NX_SNMP_TRAP_OBJECT *object_list_ptr);
```
### <a name="description"></a>Description

Bu hizmet, belirtilen IPv4 adresindeki SNMP Yöneticisi 'ne bir SNMPv2 tuzak gönderir. NetX Duo 'da SNMP tuzağı göndermek için tercih edilen yöntem *nxd_snmp_agent_trapv2_send* hizmetini kullanmaktır. *nx_snmp_agent_trapv2_send* , mevcut NETX SNMP Aracısı uygulamalarını desteklemek üzere NETX Duo 'e dahildir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.
- **ip_address** SNMP yöneticisinin IPv4 adresi.
- **topluluk** Community adı (kullanıcı adı).
- **trap_type**  
   İstenen tuzak türü. Standart olaylar şunlardır:  
   - NX_SNMP_TRAP_COLDSTART (0)
   - NX_SNMP_TRAP_WARMSTART (1)
   - NX_SNMP_TRAP_LINKDOWN (2)
   - NX_SNMP_TRAP_LINKUP (3)
   - NX_SNMP_TRAP_AUTHENTICATE_FAILURE (4)
   - NX_SNMP_TRAP_EGPNEIGHBORLOSS (5)

   Özel veriler için:  
   - NX_SNMP_TRAP_CUSTOM (0xFFFFFFFF) ( *nxd_snmp. h* içinde tanımlanmıştır)
   
- **Elapsed_Time** Zaman sistemi (sysUpTime).
- **object_list_ptr** SNMP tuzağı dahil edilecek nesne dizisi ve bunlarla ilişkili değerler. Listenin sonlandırılması NX_NULL.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı SNMP tuzak gönderme.
- **NX_SNMP_ERROR** (0x100) SNMP tuzağı gönderme hatası.
- **NX_NOT_ENABLED** (0x14) SNMPv2 etkin değil.
- **NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
NX_SNMP_TRAP_OBJECT trap_list[5];
ULONG  dest_ip_address = IP_ADDRESS(1,2,3,4);

/* Build an empty object list, since it is not needed for the 
   NX_SNMP_TRAP_COLDSTART trap.  */
trap_list[0].nx_snmp_object_string_ptr =  NX_NULL;

/* Send trap to SNMP manager at 193.2.2.61.  */
Status =  nx_snmp_agent_trapv2_send(&my_agent,dest_ip_address, "public",
               NX_SNMP_TRAP_COLDSTART, tx_time_get(), trap_list);

/* If status is NX_SUCCESS the SNMP trap has been sent.  */
```

## <a name="nx_snmp_agent_trapv2_oid_send"></a>nx_snmp_agent_trapv2_oid_send
Doğrudan OID 'yi belirten SNMPv2 tuzağı gönder 

### <a name="prototype"></a>Prototype

```c
UINT nx_snmp_agent_trapv2_oid_send(NX_SNMP_AGENT *agent_ptr, 
                                   ULONG ip_address, UCHAR *community,        
                                   UCHAR *oid, ULONG elapsed_time,   
                                   NX_SNMP_TRAP_OBJECT 
                                            *object_list_ptr);
```
### <a name="description"></a>Description

Bu hizmet, belirtilen IP adresindeki (yalnızca IPv4) SNMP Yöneticisi 'ne bir SNMPv2 tuzak gönderir ve çağıranın OID 'yi doğrudan belirlemesine izin verir. NetX Duo 'da belirtilen OID ile SNMP tuzağı göndermek için tercih edilen yöntem *nxd_snmp_agent_trapv2_oid_send* hizmetini kullanmaktır. Mevcut NetX SNMP Aracısı uygulamalarını desteklemek için, NetX Duo 'e *nx_snmp_agent_trapv2_oid_ Send* işlemi dahildir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.
- **ip_address** SNMP yöneticisinin IP adresi.
- **topluluk** Community adı (kullanıcı adı).
- **OID** OID içeren arabelleğin işaretçisi.
- **Elapsed_Time** Zaman sistemi (sysUpTime).
- **object_list_ptr** SNMP tuzağı dahil edilecek nesne dizisi ve bunlarla ilişkili değerler. Listenin sonlandırılması NX_NULL.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı SNMP tuzak gönderme.
- **NX_SNMP_ERROR** (0x100) SNMP tuzağı gönderme hatası.
- **NX_PTR_ERROR** (0x16) geçersiz SNMP Aracısı veya parametre işaretçisi.
- **NX_IP_ADDRESS_ERROR** (0x21) GEÇERSIZ hedef IP adresi.
- **NX_OPTION_ERROR** (0X0a) geçersiz parametre.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
NX_SNMP_TRAP_OBJECT trap_list[5];

/* Build an empty object list */
trap_list[0].nx_snmp_object_string_ptr =  NX_NULL;

/* Send trap to SNMP manager at 193.2.2.61.  */
Status =  nx_snmp_agent_trapv2_oid_send(&my_agent, IP_ADDRESS(193,2,2,61), 
                                       "public", (UCHAR *)"0.9.9.9.9.9.9.9.9.9",  
                                       tx_time_get(), trap_list);

/* If status is NX_SUCCESS the SNMP trap has been sent.  */
```

## <a name="nxd_snmp_agent_trapv2_send"></a>nxd_snmp_agent_trapv2_send
SNMPv2 tuzağı gönderme (IPv4 ve IPv6)

### <a name="prototype"></a>Prototype

```c
UINT nxd_snmp_agent_trapv2_send(NX_SNMP_AGENT *agent_ptr, 
                                NXD_ADDRESS *ip_address, 
                                UCHAR *community, UINT trap_type, 
                                ULONG elapsed_time, 
                                NX_SNMP_TRAP_OBJECT *object_list_ptr);
```
### <a name="description"></a>Description

Bu hizmet, belirtilen IP adresindeki SNMP Yöneticisi 'ne bir SNMP v2 tuzağı gönderir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.
- **ip_address** SNMP yöneticisinin IP (IPv4 veya IPv6) adresi.
- **topluluk** Community adı (kullanıcı adı).
- **trap_type**  
   İstenen tuzak türü. Standart olaylar şunlardır:  
   - NX_SNMP_TRAP_COLDSTART (0)
   - NX_SNMP_TRAP_WARMSTART (1)
   - NX_SNMP_TRAP_LINKDOWN (2)
   - NX_SNMP_TRAP_LINKUP (3)
   - NX_SNMP_TRAP_AUTHENTICATE_FAILURE (4)
   - NX_SNMP_TRAP_EGPNEIGHBORLOSS (5)

   Özel veriler için:

   - NX_SNMP_TRAP_CUSTOM (0xFFFFFFFF) ( *nxd_snmp. h* içinde tanımlanmıştır)

- **Elapsed_Time** Zaman sistemi (sysUpTime).
- **object_list_ptr** SNMP tuzağı dahil edilecek nesne dizisi ve bunlarla ilişkili değerler. Listenin sonlandırılması NX_NULL.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı SNMP tuzak gönderme.
- **NX_SNMP_ERROR** (0x100) SNMP tuzağı gönderme hatası.
- **NX_NOT_ENABLED** (0x14) SNMPv2 etkin değil.
- **NX_SNMP_INVALID_IP_PROTOCOL_ERROR** (0x104) desteklenmeyen IP sürümü
- **NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
NX_SNMP_TRAP_OBJECT trap_list[5];
NXD_ADDRESS dest_ip_address;

    dest_ip_address.nxd_ip_version = NX_IP_VERSION_V6 ;
    dest_ip_address.nxd_ip_address.v6[0] = 0x20010db8;
    dest_ip_address.nxd_ip_address.v6[1] = 0xf101;
    dest_ip_address.nxd_ip_address.v6[2] = 0x00000000;
    dest_ip_address.nxd_ip_address.v6[3] = 0x00000101;

/* Build an empty object list, since it is not needed for the 
   NX_SNMP_TRAP_COLDSTART trap.  */
trap_list[0].nx_snmp_object_string_ptr =  NX_NULL;

/* Send a standard event trap to SNMP manager at 193.2.2.61.  */
Status =  nxd_snmp_agent_trapv2_send(&my_agent,&dest_ip_address, "public",
                                    NX_SNMP_TRAP_COLDSTART, tx_time_get(),  
                                    trap_list);

/* If status is NX_SUCCESS the SNMP trap has been sent.  */
```

## <a name="nxd_snmp_agent_trapv2_oid_send"></a>nxd_snmp_agent_trapv2_oid_send
Doğrudan OID 'yi belirten SNMPv2 tuzağı gönder 

### <a name="prototype"></a>Prototype

```c
UINT nxd_snmp_agent_trapv2_oid_send(NX_SNMP_AGENT *agent_ptr, 
                                    NXD_ADDRESS *ip_address, 
                                    UCHAR *community,        
                                    UCHAR *oid, ULONG elapsed_time,   
                                    NX_SNMP_TRAP_OBJECT 
                                    *object_list_ptr);
```
### <a name="description"></a>Description

Bu hizmet, belirtilen IP adresindeki (IPv4/IPv6) SNMP Yöneticisi 'ne SNMP v2 tuzağı gönderir ve çağıranın OID 'yi doğrudan belirlemesine izin verir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.
- **ip_address** SNMP yöneticisinin IP adresi (IPv4/IPv6).
- **topluluk** Community adı (kullanıcı adı).
- **OID** OID içeren arabelleğin işaretçisi.
- **Elapsed_Time** Zaman sistemi (sysUpTime).
- **object_list_ptr** SNMP tuzağı dahil edilecek nesne dizisi ve bunlarla ilişkili değerler. Listenin sonlandırılması NX_NULL.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı SNMP tuzak gönderme.
- **NX_SNMP_ERROR** (0x100) SNMP tuzağı gönderme hatası.
- **NX_PTR_ERROR** (0x16) geçersiz SNMP Aracısı veya parametre işaretçisi.
- **NX_IP_ADDRESS_ERROR** (0x21) GEÇERSIZ hedef IP adresi.
- **NX_OPTION_ERROR** (0X0a) geçersiz parametre.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
NX_SNMP_TRAP_OBJECT trap_list[5];
NXD_ADDRESS         address;


/* Build an empty object list */
trap_list[0].nx_snmp_object_string_ptr =  NX_NULL;

address.nxd_ip_version = NX_IP_VERSION_V4;
address.nxd_ip_address.v4 = IP_ADDRESS(193,2,2,61)

/* Send trap to SNMP manager at 193.2.2.61.  */
Status =  nxd_snmp_agent_trapv2_oid_send(&my_agent, &address, 
                                       "public", (UCHAR *)"0.9.9.9.9.9.9.9.9.9",  
                                       tx_time_get(), trap_list);

/* If status is NX_SUCCESS the SNMP trap has been sent.  */
```
## <a name="nx_snmp_agent_trapv3_send"></a>nx_snmp_agent_trapv3_send
SNMPv3 tuzağı gönder (yalnızca IPv4)

### <a name="prototype"></a>Prototype

```c
UINT nx_snmp_agent_trapv3_send(NX_SNMP_AGENT *agent_ptr, 
            ULONG ip_address, UCHAR *username, UINT trap_type, 
            ULONG elapsed_time, NX_SNMP_TRAP_OBJECT *object_list_ptr);
```

### <a name="description"></a>Description

Bu hizmet, belirtilen IPv4 adresinde SNMP Yöneticisi 'ne bir SNMPv3 tuzağı gönderir. NetX Duo 'da SNMP tuzağı göndermek için tercih edilen yöntem *nxd_snmp_agent_trapv3_send* hizmetini kullanmaktır. *nx_snmp_agent_trapv3_send* , mevcut NETX SNMP Aracısı uygulamalarını desteklemek üzere NETX Duo 'e dahildir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.
- **ip_address** SNMP yöneticisinin IPv4 adresi.
- **kullanıcı** adı Community adı (kullanıcı adı).
- **trap_type**  
   İstenen tuzak türü. Standart olaylar şunlardır:  
   - NX_SNMP_TRAP_COLDSTART (0)
   - NX_SNMP_TRAP_WARMSTART (1)
   - NX_SNMP_TRAP_LINKDOWN (2)
   - NX_SNMP_TRAP_LINKUP (3)
   - NX_SNMP_TRAP_AUTHENTICATE_FAILURE (4)
   - NX_SNMP_TRAP_EGPNEIGHBORLOSS (5)

   Özel veriler için:
   - NX_SNMP_TRAP_CUSTOM (0xFFFFFFFF) ( *nxd_snmp. h* içinde tanımlanmıştır)

- **Elapsed_Time** Zaman sistemi (sysUpTime).
- **object_list_ptr** SNMP tuzağı dahil edilecek nesne dizisi ve bunlarla ilişkili değerler. Listenin sonlandırılması NX_NULL.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı SNMP tuzak gönderme.
- **NX_SNMP_ERROR** (0x100) SNMP tuzağı gönderme hatası.
- **NX_NOT_ENABLED** (0x14) SNMPv3 etkin değil.
- **NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, Iş parçacıkları

### <a name="example"></a>Örnek

```c
NX_SNMP_TRAP_OBJECT trap_list[5];
ULONG dest_ip_address = IP_ADDRESS(1,2,3,4);

/* Build an empty object list, since it is not needed for the 
   NX_SNMP_TRAP_COLDSTART trap.  */
trap_list[0].nx_snmp_object_string_ptr =  NX_NULL;

/* Send trap to SNMP manager at 193.2.2.61.  */
Status =  nx_snmp_agent_trapv3_send(&my_agent, dest_ip_address, "public",
               NX_SNMP_TRAP_COLDSTART, tx_time_get(), trap_list);

/* If status is NX_SUCCESS the SNMP trap has been sent.  */
```

## <a name="nx_snmp_agent_trapv3_oid_send"></a>nx_snmp_agent_trapv3_oid_send
Doğrudan OID 'yi belirten SNMPv3 tuzağı gönder 

### <a name="prototype"></a>Prototype

```c
UINT nx_snmp_agent_trapv3_oid_send(NX_SNMP_AGENT *agent_ptr, 
                                   ULONG ip_address, UCHAR *username,        
                                   UCHAR *oid, ULONG elapsed_time,   
                                   NX_SNMP_TRAP_OBJECT 
                                   *object_list_ptr);
```
### <a name="description"></a>Description

Bu hizmet, belirtilen IP adresindeki (yalnızca IPv4) SNMP yöneticisine bir SNMPv3 tuzağı gönderir ve çağıranın OID 'yi doğrudan belirlemesine izin verir. NetX Duo 'da belirtilen OID ile SNMP tuzağı göndermek için tercih edilen yöntem *nxd_snmp_agent_trapv3_oid_send* hizmetini kullanmaktır. Mevcut NetX SNMP Aracısı uygulamalarını desteklemek için, NetX Duo 'e *nx_snmp_agent_trapv3_oid_ Send* işlemi dahildir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.
- **ip_address** SNMP yöneticisinin IP adresi.
- **kullanıcı** adı Community adı (kullanıcı adı).
- **OID** OID içeren arabelleğin işaretçisi.
- **Elapsed_Time** Zaman sistemi (sysUpTime).
- **object_list_ptr** SNMP tuzağı dahil edilecek nesne dizisi ve bunlarla ilişkili değerler. Listenin sonlandırılması NX_NULL.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı SNMP tuzak gönderme.
- **NX_SNMP_ERROR** (0x100) SNMP tuzağı gönderme hatası.
- **NX_PTR_ERROR** (0x16) geçersiz SNMP Aracısı veya parametre işaretçisi.
- **NX_IP_ADDRESS_ERROR** (0x21) GEÇERSIZ hedef IP adresi.
- **NX_OPTION_ERROR** (0X0a) geçersiz parametre.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
NX_SNMP_TRAP_OBJECT trap_list[5];

/* Build an empty object list */
trap_list[0].nx_snmp_object_string_ptr =  NX_NULL;

/* Send trap to SNMP manager at 193.2.2.61.  */
Status =  nx_snmp_agent_trapv3_oid_send(&my_agent, IP_ADDRESS(193,2,2,61), 
                                       "public", (UCHAR *)"0.9.9.9.9.9.9.9.9.9",  
                                       tx_time_get(), trap_list);

/* If status is NX_SUCCESS the SNMP trap has been sent.  */
```
## <a name="nxd_snmp_agent_trapv3_send"></a>nxd_snmp_agent_trapv3_send
SNMPv3 tuzağı gönderme (IPv4 ve IPv6)

### <a name="prototype"></a>Prototype

```c
UINT nxd_snmp_agent_trapv3_send(NX_SNMP_AGENT *agent_ptr, 
                                NXD_ADDRESS *ip_address, 
                                UCHAR *username, UINT trap_type, 
                                ULONG elapsed_time, 
                                NX_SNMP_TRAP_OBJECT *object_list_ptr);
```
### <a name="description"></a>Description

Bu hizmet, belirtilen IP adresindeki SNMP Yöneticisi 'ne SNMP tuzağı gönderir. Tuzak iletisi biçimi SNMP v3 PDU 'SU içinde içerilmediği sürece bu tuzak, SNMP v2 tuzağı temelde aynıdır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.
- **ip_address** SNMP yöneticisinin IP (IPv4 veya IPv6) adresi.
- **kullanıcı** adı Community adı (kullanıcı adı).
- **trap_type**  
   İstenen tuzak türü. Standart olaylar şunlardır:
   - NX_SNMP_TRAP_COLDSTART (0)
   - NX_SNMP_TRAP_WARMSTART (1)
   - NX_SNMP_TRAP_LINKDOWN (2)
   - NX_SNMP_TRAP_LINKUP (3)
   - NX_SNMP_TRAP_AUTHENTICATE_FAILURE (4)
   - NX_SNMP_TRAP_EGPNEIGHBORLOSS (5)  
   Özel veriler için:
   - NX_SNMP_TRAP_CUSTOM (0xFFFFFFFF) ( *nxd_snmp. h* içinde tanımlanmıştır)

- **Elapsed_Time** Zaman sistemi (sysUpTime).
- **object_list_ptr** SNMP tuzağı dahil edilecek nesne dizisi ve bunlarla ilişkili değerler. Listenin sonlandırılması NX_NULL.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı SNMP tuzak gönderme.
- **NX_SNMP_ERROR** (0x100) SNMP tuzağı gönderme hatası.
- **NX_NOT_ENABLED** (0x14) SNMPv3 etkin değil.
- **NX_SNMP_INVALID_IP_PROTOCOL_ERROR** (0x104) desteklenmeyen IP sürümü
- **NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
NX_SNMP_TRAP_OBJECT trap_list[5];
NXD_ADDRESS dest_ip_address;

    dest_ip_address.nxd_ip_version = NX_IP_VERSION_V6 ;
    dest_ip_address.nxd_ip_address.v6[0] = 0x20010db8;
    dest_ip_address.nxd_ip_address.v6[1] = 0xf101;
    dest_ip_address.nxd_ip_address.v6[2] = 0x00000000;
    dest_ip_address.nxd_ip_address.v6[3] = 0x00000101;

/* Build an empty object list, since it is not needed for the 
   NX_SNMP_TRAP_COLDSTART trap.  */
trap_list[0].nx_snmp_object_string_ptr =  NX_NULL;

/* Send trap to SNMP manager at 193.2.2.61.  */
Status =  nxd_snmp_agent_trapv3_send(&my_agent, &dest_ip_address, "public",
                                    NX_SNMP_TRAP_COLDSTART, tx_time_get(),  
                                    trap_list);

/* If status is NX_SUCCESS the SNMP trap has been sent.  */
```

## <a name="nxd_snmp_agent_trapv3_oid_send"></a>nxd_snmp_agent_trapv3_oid_send
Doğrudan OID 'yi belirten SNMPv3 tuzağı gönder 

### <a name="prototype"></a>Prototype

```c
UINT nxd_snmp_agent_trapv3_oid_send(NX_SNMP_AGENT *agent_ptr, 
                                    NXD_ADDRESS *ip_address, 
                                    UCHAR *username,        
                                    UCHAR *oid, ULONG elapsed_time,   
                                    NX_SNMP_TRAP_OBJECT 
                                            *object_list_ptr);
```
### <a name="description"></a>Description

Bu hizmet, belirtilen IP adresindeki (IPv4/IPv6) SNMP Yöneticisi 'ne bir SNMPv3 tuzağı gönderir ve çağıranın OID 'yi doğrudan belirlemesine izin verir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **agent_ptr** SNMP Aracısı denetim bloğu işaretçisi.
- **ip_address** SNMP yöneticisinin IP adresi işaretçisi.
- **Kullanıcı adı** Kullanıcı adı (topluluk adı).
- **OID** OID içeren arabelleğin işaretçisi.
- **Elapsed_Time** Zaman sistemi (sysUpTime).
- **object_list_ptr** SNMP tuzağı dahil edilecek nesne dizisi ve bunlarla ilişkili değerler. Listenin sonlandırılması NX_NULL.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı SNMP tuzak gönderme.
- **NX_SNMP_ERROR** (0x100) SNMP tuzağı gönderme hatası.
- **NX_PTR_ERROR** (0x16) geçersiz SNMP Aracısı veya parametre işaretçisi.
- **NX_IP_ADDRESS_ERROR** (0x21) GEÇERSIZ hedef IP adresi.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
NXD_ADDRESS         ip_address;
NX_SNMP_TRAP_OBJECT trap_list[5];

/* Build an empty object list */
trap_list[0].nx_snmp_object_string_ptr =  NX_NULL;

ip_address.nxd_ip_version = NX_IP_VERSION_V4;
ip_address.nxd_ip_address.v4 = IP_ADDRESS(193,2,2,61);

/* Send trap to SNMP manager at 193.2.2.61.  */
Status =  nxd_snmp_agent_trapv3_oid_send(&my_agent, &ip_address, 
                                       "public", (UCHAR *)"0.9.9.9.9.9.9.9.9.9",  
                                       tx_time_get(), trap_list);

/* If status is NX_SUCCESS the SNMP trap has been sent.  */
```
## <a name="nx_snmp_agent_v3_context_boots_set"></a>nx_snmp_agent_v3_context_boots_set
Yeniden başlatmalar sayısını ayarla (SNMPv3 etkin ise)

### <a name="prototype"></a>Prototype

```c
UINT nx_snmp_agent_v3_context_boots_set(NX_SNMP_AGENT *agent_ptr, 
                                        UINT boots);
```

### <a name="description"></a>Description

Bu hizmet SNMP Aracısı tarafından kaydedilen yeniden başlatmalar sayısını ayarlar. Bu hizmet yalnızca, önyükleme sayısı SNMPv3 protokolünde kullanıldığı için SNMP Aracısı için SNMPv3 etkin olduğunda kullanılabilir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **agent_ptr** SNMP Aracısı denetim bloğu işaretçisi
- **önyüklemeler** SNMP Aracısı önyükleme sayısı ayarlanacak değer

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) önyükleme sayısı başarıyla ayarlandı
- **NX_SNMP_ERROR** (0x100) önyükleme sayısı ayarlanırken hata oluştu
- **NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi

### <a name="allowed-from"></a>İzin verilen

Başlatma, Iş parçacıkları

### <a name="example"></a>Örnek

```c
UINT my_boots = 4;

if (my_agent.nx_snmp_agent_v3_enabled == NX_TRUE)
{
   status = nx_snmp_agent_v3_context_boots_set(&my_agent, my_boots);
}


/* If status is NX_SUCCESS the SNMP boot count is set.  */
```

## <a name="nx_snmp_object_compare"></a>nx_snmp_object_compare
İki nesneyi karşılaştırın 

### <a name="prototype"></a>Prototype

```c
UINT nx_snmp_object_compare(UCHAR *object, UCHAR *reference_object);
```

### <a name="description"></a>Description

Bu hizmet, sağlanan nesne KIMLIĞINI başvuru nesne KIMLIĞIYLE karşılaştırır. Her iki nesne kimliği de ASCII SMı gösteriminde, ör. her iki nesne da "1.3.6" ASCII dizesiyle başlamalıdır.

Bu hizmet kullanımdan kaldırılmıştır. Geliştiricilerin *nx_snmp_object_compare_extended ()* uygulamasına geçirilmesi önerilir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **nesne** Nesne KIMLIĞI işaretçisi.
- **reference_object** Başvuru nesnesi KIMLIĞINE yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) nesne başvuru nesnesiyle eşleşir.
- **NX_SNMP_NEXT_ENTRY** (0x101) nesne başvuru nesnesinden küçüktür.
- **NX_SNMP_ERROR** (0x100) nesne başvuru nesnesinden daha büyük.
- **NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, Iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Compare “requested_object” with the sysDescr object ID of 
   "1.3.6.1.2.1.1.1.0".  */
Status =  nx_snmp_object_compare(requested_object, "1.3.6.1.2.1.1.1.0");

/* If status is NX_SUCCESS, requested_object is the sysDescr object. 
   Otherwise, if status is NX_SNMP_NEXT_ENTRY, the requested object is
   less than the sysDescr. If status is NX_SNMP_ERROR, the object is 
   greater than sysDescr. */
```

## <a name="nx_snmp_object_compare_extended"></a>nx_snmp_object_compare_extended
İki nesneyi karşılaştırın 

### <a name="prototype"></a>Prototype

```c
UINT nx_snmp_object_compare_extended(UCHAR *request_object, 
                                     UINT requested_object_length,
                                     UCHAR *reference_object
                                     UINT reference_object_length);
```
### <a name="description"></a>Description

Bu hizmet, sağlanan nesne KIMLIĞINI başvuru nesne KIMLIĞIYLE karşılaştırır. Her iki nesne kimliği de ASCII SMı gösteriminde, ör. her iki nesne da "1.3.6" ASCII dizesiyle başlamalıdır.

Bu hizmet *nx_snmp_object_compare ()* yerini alır. Bu sürüm, arayanlara uzunluk bilgilerini sağlaması gerekir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **request_object** İstek nesnesi KIMLIĞI işaretçisi.
- **request_object_length** İstek nesnesi KIMLIĞININ uzunluğu.
- **reference_object** Başvuru nesnesi KIMLIĞINE yönelik işaretçi.
- **reference_object_length** Başvuru nesnesi KIMLIĞININ uzunluğu.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) nesne başvuru nesnesiyle eşleşir.
- **NX_SNMP_NEXT_ENTRY** (0x101) nesne başvuru nesnesinden küçüktür.
- **NX_SNMP_ERROR** (0x100) nesne başvuru nesnesinden daha büyük.
- **NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, Iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Compare “requested_object” with the sysDescr object ID of 
   "1.3.6.1.2.1.1.1.0".  */
Status =  nx_snmp_object_compare_extended(requested_object, 17,
                                          "1.3.6.1.2.1.1.1.0", 17);

/* If status is NX_SUCCESS, requested_object is the sysDescr object. 
   Otherwise, if status is NX_SNMP_NEXT_ENTRY, the requested object is
   less than the sysDescr. If status is NX_SNMP_ERROR, the object is 
   greater than sysDescr. */
```

## <a name="nx_snmp_object_copy"></a>nx_snmp_object_copy
Nesne kopyalama 

### <a name="prototype"></a>Prototype

```c
UINT  nx_snmp_object_copy(UCHAR *source_object_name, 
                          UCHAR *destination_object_name);
```
### <a name="description"></a>Description

Bu hizmet, ASCII SIM gösterimi içindeki kaynak nesneyi hedef nesneye kopyalar.

Bu hizmet kullanımdan kaldırılmıştır. Geliştiricilerin *nx_snmp_object_copy_extended ()* uygulamasına geçirilmesi önerilir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **source_object_name** Kaynak nesne KIMLIĞI işaretçisi.
- **destination_object_name** Hedef nesne KIMLIĞI işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **Boyut** Hedef ada kopyalanmış bayt sayısı. Hata ise, sıfır döndürülür.

### <a name="allowed-from"></a>İzin verilen

Başlatma, Iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Copy “my_object” to “my_new_object”.  */
size =  nx_snmp_object_copy(my_object, my_new_object);

/* Size contains the number of bytes copied. */
```

## <a name="nx_snmp_object_copy_extended"></a>nx_snmp_object_copy_extended
Nesne kopyalama 

### <a name="prototype"></a>Prototype

```c
UINT  nx_snmp_object_copy_extended(UCHAR *source_object_name, 
                             UINT source_object_name_length,
                             UCHAR *destination_object_name_buffer,
                             UINT destination_object_name_buffer_size);
```

### <a name="description"></a>Description

Bu hizmet, ASCII SIM gösterimi içindeki kaynak nesneyi hedef nesneye kopyalar.

Bu hizmet *nx_snmp_object_copy ()* yerini alır. Bu sürüm, arayanlara uzunluk bilgilerini sağlaması gerekir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **source_object_name** Kaynak nesne KIMLIĞI işaretçisi.
- **source_object_name_length** Kaynak nesne KIMLIĞININ uzunluğu.
- **destination_object_name_buffer** Hedef nesne arabelleği işaretçisi.
- **destination_object_name_buffer_size** Hedef nesne arabelleğinin boyutu.

### <a name="return-values"></a>Dönüş Değerleri

- **Boyut** Hedef ada kopyalanmış bayt sayısı. Hata ise, sıfır döndürülür.

### <a name="allowed-from"></a>İzin verilen

Başlatma, Iş parçacıkları

### <a name="example"></a>Örnek

```c
UCHAR   my_object = "1.3.6.1.2.1.1.1.0";
UCHAR   my_new_object[32];


/* Copy “my_object” to “my_new_object”.  */
size =  nx_snmp_object_copy(my_object, 17, my_new_object, sizeof(my_new_object));

/* Size contains the number of bytes copied. */
```

## <a name="nx_snmp_object_counter_get"></a>nx_snmp_object_counter_get
Sayaç nesnesi Al 

### <a name="prototype"></a>Prototype

```c
UINT  nx_snmp_object_counter_get(VOID *source_ptr, 
                                 NX_SNMP_OBJECT_DATA *object_data);
```
### <a name="description"></a>Description

Bu hizmet, kaynak işaretçi tarafından belirtilen adresteki sayaç nesnesini alır ve NetX nesne verileri yapısına koyar. Bu yordam genellikle GET veya GETNEXT uygulama geri çağırma yordamından çağırılır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **source_ptr** Sayaç kaynağı işaretçisi.
- **object_data** Hedef nesne yapısına yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Sayaç nesnesi başarıyla alınmıştır.
- **NX_PTR_ERROR** (0x07) Geçersiz giriş işaretçisi.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Get the ifInOctets (1.3.6.1.2.1.2.2.1.10.0) MIB-2 object.  */
status =  nx_snmp_object_counter_get(&ifInOctets, my_object);

/* If status is NX_SUCCESS, the ifInOctets object has been 
   retrieved and is ready to be returned. */
```

## <a name="nx_snmp_object_counter_set"></a>nx_snmp_object_counter_set
Sayaç nesnesini ayarlama 

### <a name="prototype"></a>Prototype

```c
UINT  nx_snmp_object_counter_set(VOID *destination_ptr, 
                                 NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a>Description

Bu hizmet, sayacı NetX nesne veri yapısında sayaç değeriyle hedef işaretçi tarafından belirtilen adrese ayarlar. Bu yordam genellikle SET uygulaması geri çağırma yordamından çağrılır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **destination_ptr** Sayaç hedefi işaretçisi.
- **object_data** Sayaç kaynağı nesne yapısına işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Sayaç nesnesi başarıyla ayarlanmıştır.
- **NX_SNMP_ERROR_WRONGTYPE** (0x07) Geçersiz nesne türü.
- **NX_PTR_ERROR** (0x07) Geçersiz giriş işaretçisi.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Set the ifInOctets (1.3.6.1.2.1.2.2.1.10.0) MIB-2 object with
   the counter object value contained in my_object.  */
status =  nx_snmp_object_counter_set(&ifInOctets, my_object);

/* If status is NX_SUCCESS, the ifInOctets object has been 
   set. */
```

## <a name="nx_snmp_object_counter64_get"></a>nx_snmp_object_counter64_get
64 bit sayaç nesnesi al 

### <a name="prototype"></a>Prototype

```c
UINT  nx_snmp_object_counter64_get(VOID *source_ptr, 
                                   NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a>Description

Bu hizmet, kaynak işaretçi tarafından belirtilen adreste 64 bit sayaç nesnesini alan ve NetX nesne veri yapısına yer alan. Bu yordam genellikle GET veya GETNEXT uygulama geri çağırma yordamından çağrılır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **source_ptr** Sayaç kaynağı işaretçisi.
- **object_data** Hedef nesne yapısına işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Sayaç nesnesi başarıyla alınmıştır.
- **NX_PTR_ERROR** (0x07) Geçersiz giriş işaretçisi

### <a name="allowed-from"></a>İzin Verilen

Başlatma, İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Get the value of my_64_bit_counter and place it into my_object
   for return.  */
status =  nx_snmp_object_counter64_get(&my_64_bit_counter, my_object);

/* If status is NX_SUCCESS, the my_64_bit_counter object has been 
   retrieved and is ready to be returned. */
```

## <a name="nx_snmp_object_counter64_set"></a>nx_snmp_object_counter64_set
64 bit sayaç nesnesi ayarlama 

### <a name="prototype"></a>Prototype

```c
UINT  nx_snmp_object_counter64_set(VOID *destination_ptr, 
                                   NX_SNMP_OBJECT_DATA *object_data);
```
### <a name="description"></a>Description

Bu hizmet, NetX nesne veri yapısında sayaç değeriyle hedef işaretçi tarafından belirtilen adreste 64 bit sayacı ayarlar. Bu yordam genellikle SET uygulaması geri çağırma yordamından çağrılır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **destination_ptr** Sayaç hedefi işaretçisi.
- **object_data** Sayaç kaynağı nesne yapısına işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Sayaç nesnesi başarıyla ayarlanmıştır.
- **NX_SNMP_ERROR_WRONGTYPE** (0x07) Geçersiz nesne türü.
- **NX_PTR_ERROR** (0x07) Geçersiz giriş işaretçisi.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Set the value of my_64_bit_counter with the value in my_object.  */
status =  nx_snmp_object_counter64_set(&my_64_bit_counter, my_object);

/* If status is NX_SUCCESS, the my_64_bit_counter object has been 
   set. */
```

## <a name="nx_snmp_object_end_of_mib"></a>nx_snmp_object_end_of_mib
Mib sonu değerini ayarlama 

### <a name="prototype"></a>Prototype

```c
UINT  nx_snmp_object_end_of_mib(VOID *not_used_ptr, 
                              NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a>Description

Bu hizmet, MIB'in sonuna işaret eder ve genellikle GET veya GETNEXT uygulama geri çağırma yordamından çağrılır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **not_used_ptr** İşaretçi kullanılmadı – NX_NULL.
- **object_data** Hedef nesne yapısına işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Mib sonu nesnesi başarıyla oluşturuldu.
- **NX_PTR_ERROR** (0x07) Geçersiz giriş işaretçisi

### <a name="allowed-from"></a>İzin Verilen

Başlatma, İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Place an end-of-mib value in my_object.  */
status =  nx_snmp_object_end_of_mib(NX_NULL, my_object);

/* If status is NX_SUCCESS, the my_object is now an end-of-mib object. */
```

## <a name="nx_snmp_object_gauge_get"></a>nx_snmp_object_gauge_get
Ölçer nesnesini al 

### <a name="prototype"></a>Prototype

```c
UINT  nx_snmp_object_gauge_get(VOID *source_ptr, 
                               NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a>Description

Bu hizmet, kaynak işaretçi tarafından belirtilen adreste ölçer nesnesini almak ve NetX nesne veri yapısına yer almaktadır. Bu yordam genellikle GET veya GETNEXT uygulama geri çağırma yordamından çağrılır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **source_ptr** Ölçer kaynağı işaretçisi.
- **object_data** Hedef nesne yapısına işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Ölçer nesnesi başarıyla alınmıştır.
- **NX_PTR_ERROR** (0x07) Geçersiz giriş işaretçisi

### <a name="allowed-from"></a>İzin Verilen

Başlatma, İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Get the value of ifSpeed (1.3.6.1.2.1.2.2.1.5.0) and place it in my_object
   for return.  */
status =  nx_snmp_object_gauge_get(&ifSpeed, my_object);

/* If status is NX_SUCCESS, the my_object now contains the ifSpeed gauge value. */
```

## <a name="nx_snmp_object_gauge_set"></a>nx_snmp_object_gauge_set
Ölçer nesnesini ayarlama 

### <a name="prototype"></a>Prototype

```c
UINT  nx_snmp_object_gauge_set(VOID *destination_ptr,
                                     NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a>Description

Bu hizmet ölçeri, NetX nesne veri yapısında ölçer değeriyle hedef işaretçi tarafından belirtilen adreste ayarlar. Bu yordam genellikle SET uygulaması geri çağırma yordamından çağrılır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **destination_ptr** Ölçer hedefi işaretçisi.
- **object_data** Kaynak nesne yapısını ölçer işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Ölçer nesnesi başarıyla ayarlanmıştır.
- **NX_SNMP_ERROR_WRONGTYPE** (0x07) Geçersiz nesne türü.
- **NX_PTR_ERROR** (0x07) Geçersiz giriş işaretçisi

### <a name="allowed-from"></a>İzin Verilen

Başlatma, İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Set the value of “my_gauge” from the gauge value in my_object.  */
status =  nx_snmp_object_gauge_set(&my_gauge, my_object);

/* If status is NX_SUCCESS, the my_gauge now contains the new gauge value. */
```

## <a name="nx_snmp_object_id_get"></a>nx_snmp_object_id_get
Nesne kimliğini al 

### <a name="prototype"></a>Prototype

```c
UINT  nx_snmp_object_id_get(VOID *source_ptr, 
                            NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a>Description

Bu hizmet, kaynak işaretçi tarafından belirtilen adresteki nesne KIMLIĞINI (ASCII SIM gösteriminde) alır ve NetX nesne verileri yapısına koyar. Bu yordam genellikle GET veya GETNEXT uygulama geri çağırma yordamından çağırılır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **source_ptr** Nesne KIMLIĞI kaynağı işaretçisi.
- **object_data** Hedef nesne yapısına yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) nesne kimliği başarıyla alındı.
- **NX_SNMP_ERROR** (0x100) geçersiz nesne uzunluğu
- **NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi

### <a name="allowed-from"></a>İzin verilen

Başlatma, Iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Get the value of sysObjectID(1.3.6.1.2.1.1.2.0) and place it in my_object
   for return.  */
status =  nx_snmp_object_id_get(&sysObjectID, my_object);

/* If status is NX_SUCCESS, the my_object now contains the sysObjectID value. */
```

## <a name="nx_snmp_object_id_set"></a>nx_snmp_object_id_set
Nesne kimliğini ayarla 

### <a name="prototype"></a>Prototype

```c
UINT  nx_snmp_object_id_set(VOID *destination_ptr, 
                             NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a>Description

Bu hizmet, hedef işaretçi tarafından belirtilen adresteki nesne KIMLIĞINI (ASCII SIM gösteriminde), NetX nesne verileri yapısındaki nesne KIMLIĞIYLE ayarlar. Bu yordam genellikle uygulama geri aramasını ayarla yordamından çağırılır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **destination_ptr** Nesne KIMLIĞI hedefi işaretçisi.
- **object_data** Nesne yapısına yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) nesne kimliği başarıyla ayarlandı.
- **NX_SNMP_ERROR_WRONGTYPE** (0x07) geçersiz nesne türü.
- **NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi

### <a name="allowed-from"></a>İzin verilen

Başlatma, Iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Set the string “my_object_id” with the object ID value contained 
   in my_object.  */
status =  nx_snmp_object_id_set(my_object_id, my_object);

/* If status is NX_SUCCESS, the my_object_id now contains the object ID value. */
```

## <a name="nx_snmp_object_integer_get"></a>nx_snmp_object_integer_get
Tamsayı nesnesi Al 

### <a name="prototype"></a>Prototype

```c
UINT  nx_snmp_object_integer_get(VOID *source_ptr, 
                                  NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a>Description

Bu hizmet, kaynak işaretçi tarafından belirtilen adresteki tamsayı nesnesini alır ve NetX nesne verileri yapısına koyar. Bu yordam genellikle GET veya GETNEXT uygulama geri çağırma yordamından çağırılır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **source_ptr** Tamsayı kaynağı işaretçisi.
- **object_data** Hedef nesne yapısına yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) tamsayı nesnesi başarıyla alındı.
- **NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi

### <a name="allowed-from"></a>İzin verilen

Başlatma, Iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Get the value of sysServices (1.3.6.1.2.1.1.7.0) and place it in my_object
   for return.  */
status =  nx_snmp_object_integer_get(&sysServices, my_object);

/* If status is NX_SUCCESS, the my_object now contains the sysServices value. */
```

## <a name="nx_snmp_object_integer_set"></a>nx_snmp_object_integer_set
Tamsayı nesnesini ayarla 

### <a name="prototype"></a>Prototype

```c
UINT  nx_snmp_object_integer_set(VOID *destination_ptr,
                                      NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a>Description

Bu hizmet, hedef işaretçi tarafından belirtilen adresteki tamsayıyı NetX nesne verileri yapısındaki tamsayı değeriyle ayarlar. Bu yordam genellikle uygulama geri aramasını ayarla yordamından çağırılır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **destination_ptr** Tamsayı hedefi işaretçisi.
- **object_data** Tamsayı kaynak nesne yapısına yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) tamsayı nesnesi başarıyla ayarlandı.
- **NX_SNMP_ERROR_WRONGTYPE** (0x07) geçersiz nesne türü.
- **NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi

### <a name="allowed-from"></a>İzin verilen

Başlatma, Iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Set the value of ifAdminStatus from the integer value in my_object.  */
status =  nx_snmp_object_integer_set(&ifAdminStatus, my_object);

/* If status is NX_SUCCESS, ifAdnminStatus now contains the new integer value. */
```

## <a name="nx_snmp_object_ip_address_get"></a>nx_snmp_object_ip_address_get
IP adresi nesnesi Al (yalnızca IPv4)

### <a name="prototype"></a>Prototype

```c
UINT  nx_snmp_object_ip_address_get(VOID *source_ptr,
                                          NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a>Description

Bu hizmet, kaynak işaretçi tarafından belirtilen adresteki IP adresi nesnesini alır ve NetX nesne verileri yapısına koyar. Bu yordam genellikle GET veya GETNEXT uygulama geri çağırma yordamından çağırılır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **source_ptr** IPv4 adres kaynağı işaretçisi.
- **object_data** Hedef nesne yapısına yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) IP adresi nesnesi başarıyla alındı.
- **NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi

### <a name="allowed-from"></a>İzin verilen

Başlatma, Iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Get the value of ipAdEntAddr (1.3.6.1.2.1.4.20.1.1.0) and place it in my_object
   for return.  */
status =  nx_snmp_object_ip_address_get(&ipAdEntAddr, my_object);

/* If status is NX_SUCCESS, the my_object now contains the ipAdEntAddr value. */
```

## <a name="nx_snmp_object_ipv6_address_get"></a>nx_snmp_object_ipv6_address_get
IP adresi nesnesi Al (yalnızca IPv6)

### <a name="prototype"></a>Prototype

```c
UINT  nx_snmp_object_ipv6_address_get(VOID *source_ptr,
                                          NX_SNMP_OBJECT_DATA 
                                      *object_data);
```

### <a name="description"></a>Description

Bu hizmet, kaynak işaretçi tarafından belirtilen adresteki IPv6 adres nesnesini alır ve NetX nesne verileri yapısına koyar.
Bu yordam genellikle GET veya GETNEXT uygulama geri çağırma yordamından çağırılır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **source_ptr** IPv6 adres kaynağı işaretçisi.
- **object_data** Hedef nesne yapısına yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) IP adresi nesnesi başarıyla alındı.
- **NX_SNMP_ERROR_WRONGTYPE** (0x07) yanlış giriş SNMP nesne kodu
- **NX_NOT_ENABLED** (0x14) IPv6 etkin değil
- **NX_PTR_ERROR** (0x07) geçersiz giriş işaretçisi

### <a name="allowed-from"></a>İzin verilen

Başlatma, Iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Get the value of ipAdEntAddr (1.3.6.1.2.1.4.20.1.1.0) and place it in my_object
   for return.  */
status =  nx_snmp_object_ipv6_address_get(&ipAdEntAddr, my_object);

/* If status is NX_SUCCESS, the my_object now contains the ipAdEntAddr value. */
```

## <a name="nx_snmp_object_ip_address_set"></a>nx_snmp_object_ip_address_set
IPv4 adresi nesnesi ayarla 

### <a name="prototype"></a>Prototype

```c
UINT  nx_snmp_object_ip_address_set(VOID *destination_ptr, 
                                    NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a>Description

Bu hizmet, hedef işaretçi tarafından belirtilen adresteki IPv4 adresini NetX nesne verileri yapısındaki IP adresiyle ayarlar. Bu yordam genellikle uygulama geri aramasını ayarla yordamından çağırılır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **destination_ptr** Ayar için IP adresi işaretçisi.
- **object_data** IP adresi nesne yapısına işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) IP adresi nesnesi başarıyla ayarlanmıştır.
- **NX_SNMP_ERROR_WRONGTYPE** (0x07) Geçersiz nesne türü.
- **NX_PTR_ERROR** (0x07) Geçersiz giriş işaretçisi

### <a name="allowed-from"></a>İzin Verilen

Başlatma, İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Set the value of atNetworkAddress to the IP address in my_object.  */
status =  nx_snmp_object_ip_address_set(&atNetworkAddress, my_object);

/* If status is NX_SUCCESS, atNetWorkAddress now contains the new IP address. */
```

## <a name="nx_snmp_object_ipv6_address_set"></a>nx_snmp_object_ipv6_address_set
IPv6 adres nesnesini ayarlama 

### <a name="prototype"></a>Prototype

```c
UINT  nx_snmp_object_ipv6_address_set(VOID *destination_ptr, 
                                      NX_SNMP_OBJECT_DATA  
                                      *object_data);
```

### <a name="description"></a>Description

Bu hizmet, IPv6 adresini, NetX nesne veri yapısında IP adresiyle hedef işaretçi tarafından belirtilen adreste ayarlar. Bu yordam genellikle SET uygulaması geri çağırma yordamından çağrılır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **destination_ptr** Ayar için IP adresi işaretçisi.
- **object_data** IP adresi nesne yapısına işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) IPv6 adresi başarıyla ayarlanmıştır.
- **NX_SNMP_ERROR_WRONGTYPE** (0x07) Geçersiz nesne türü.
- **NX_NOT_ENABLED** (0x14) IPv6 etkin değil
- **NX_PTR_ERROR** (0x07) Geçersiz giriş işaretçisi

### <a name="allowed-from"></a>İzin Verilen

Başlatma, İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Set the value of atNetworkAddress to the IP address in my_object.  */
status =  nx_snmp_object_ipv6_address_set(&atNetworkAddress, my_object);

/* If status is NX_SUCCESS, atNetWorkAddress now contains the new IP address. */
```

## <a name="nx_snmp_object_no_instance"></a>nx_snmp_object_no_instance
Örnek yok nesnesini ayarlama 

### <a name="prototype"></a>Prototype

```c
UINT  nx_snmp_object_no_instance(VOID *not_used_ptr, 
                                 NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a>Description

Bu hizmet, belirtilen nesnenin bir örneği olmadığını ve genellikle GET veya GETNEXT uygulama geri çağırma yordamından çağrılır sinyal bir nesne oluşturur.

### <a name="input-parameters"></a>Giriş Parametreleri

- **not_used_ptr** İşaretçi kullanılmadı – NX_NULL.
- **object_data** Hedef nesne yapısına işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Örnek yok nesnesi başarıyla oluşturuldu.
- **NX_PTR_ERROR** (0x07) Geçersiz giriş işaretçisi

### <a name="allowed-from"></a>İzin Verilen

Başlatma, İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Place no-instance value in my_object.  */
status =  nx_snmp_object_no_instance(NX_NULL, my_object);

/* If status is NX_SUCCESS, the my_object is now a no-instance object. */
```

## <a name="nx_snmp_object_not_found"></a>nx_snmp_object_not_found
Bulunamadı nesnesini ayarlama 

### <a name="prototype"></a>Prototype

```c
UINT  nx_snmp_object_not_found(VOID *not_used_ptr, 
                               NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a>Description

Bu hizmet nesnenin bulunamadı olduğunu ve genellikle GET veya GETNEXT uygulama geri çağırma yordamından çağrılır bir nesne oluşturur.

### <a name="input-parameters"></a>Giriş Parametreleri

- **not_used_ptr** İşaretçi kullanılmadı – NX_NULL.
- **object_data** Hedef nesne yapısına işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Bulunamadı nesnesi başarıyla oluşturuldu.
- **NX_PTR_ERROR** (0x07) Geçersiz giriş işaretçisi

### <a name="allowed-from"></a>İzin Verilen

Başlatma, İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Place not-found value in my_object.  */
status =  nx_snmp_object_not_found(NX_NULL, my_object);

/* If status is NX_SUCCESS, the my_object is now a not-found object. */
```

## <a name="nx_snmp_object_octet_string_get"></a>nx_snmp_object_octet_string_get
Sekizli dize nesnesini al 

### <a name="prototype"></a>Prototype

```c
UINT  nx_snmp_object_octet_string_get(VOID *source_ptr,
                                            NX_SNMP_OBJECT_DATA *object_data, 
                                      UINT length);
```
### <a name="description"></a>Description

Bu hizmet, kaynak işaretçi tarafından belirtilen adreste sekizli dizeyi alır ve NetX nesne veri yapısına yer alır. Bu yordam genellikle GET veya GETNEXT uygulama geri çağırma yordamından çağrılır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **source_ptr** Sekizli dize kaynağının işaretçisi.
- **object_data** Hedef nesne yapısına işaretçi.
- **uzunluk** Sekizli dizede bayt sayısı.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Sekizli dize nesnesi başarıyla alındı.
- **NX_PTR_ERROR** (0x07) Geçersiz giriş işaretçisi

### <a name="allowed-from"></a>İzin Verilen

Başlatma, İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Get the value of the 6-byte ifPhysAddress (1.3.6.1.2.1.2.2.1.6.0) and place 
   it in my_object for return.  */
status =  nx_snmp_object_octet_string_get(ifPhysAddress, my_object, 6);

/* If status is NX_SUCCESS, the my_object now contains the ifPhysAddress value. */
```

## <a name="nx_snmp_object_octet_string_set"></a>nx_snmp_object_octet_string_set
Sekizli dize nesnesini ayarlama 

### <a name="prototype"></a>Prototype

```c
UINT  nx_snmp_object_octet_string_set(VOID *destination_ptr, 
                                      NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a>Description

Bu hizmet, NetX nesne veri yapısında sekizli dize ile hedef işaretçi tarafından belirtilen adreste sekizli dizeyi ayarlar. Bu yordam genellikle SET uygulaması geri çağırma yordamından çağrılır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **destination_ptr** Sekizli dize hedefinin işaretçisi.
- **object_data** Sekizli dize kaynağı nesne yapısına işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Sekizli dize nesnesi başarıyla ayarlanmıştır.
- **NX_SNMP_ERROR_WRONGTYPE** (0x07) Geçersiz nesne türü.
- **NX_PTR_ERROR** (0x07) Geçersiz giriş işaretçisi

### <a name="allowed-from"></a>İzin Verilen

Başlatma, İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Set the value of sysContact (1.3.6.1.2.1.1.4.0) from the 
   octet string in my_object.  */
status =  nx_snmp_object_octet_string_set(sysContact, my_object);

/* If status is NX_SUCCESS, sysContact now contains the new octet string. */
```

## <a name="nx_snmp_object_string_get"></a>nx_snmp_object_string_get
ASCII dize nesnesini al 

### <a name="prototype"></a>Prototype

```c
UINT  nx_snmp_object_string_get(VOID *source_ptr, 
                                NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a>Description

Bu hizmet, kaynak işaretçi tarafından belirtilen adreste ASCII dizesini alır ve NetX nesne veri yapısına yer alır. Bu yordam genellikle GET veya GETNEXT uygulama geri çağırma yordamından çağrılır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **source_ptr** ASCII dize kaynağının işaretçisi.
- **object_data** Hedef nesne yapısına işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) ASCII dize nesnesi başarıyla alındı.
- **NX_SNMP_ERROR** (0x100) Dizesi çok büyük  
- **NX_PTR_ERROR** (0x07) Geçersiz giriş işaretçisi

### <a name="allowed-from"></a>İzin Verilen

Başlatma, İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Get the value of the sysDescr (1.3.6.1.2.1.1.1.0) and place 
   it in my_object for return.  */
status =  nx_snmp_object_string_get(sysDescr, my_object);

/* If status is NX_SUCCESS, the my_object now contains the sysDescr string. */
```

## <a name="nx_snmp_object_string_set"></a>nx_snmp_object_string_set
ASCII dize nesnesini ayarlama 

### <a name="prototype"></a>Prototype

```c
UINT  nx_snmp_object_string_set(VOID *destination_ptr, 
                                NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a>Description

Bu hizmet, ASCII dizesini, NetX nesne veri yapısında ASCII dizesiyle hedef işaretçi tarafından belirtilen adreste ayarlar. Bu yordam genellikle SET uygulaması geri çağırma yordamından çağrılır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **destination_ptr** ASCII dize hedefi işaretçisi.
- **object_data** ASCII dizesi kaynak nesne yapısına işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) ASCII dize nesnesi başarıyla ayarlanmıştır.
- **NX_SNMP_ERROR** (0x100) Dizesi çok büyük.
- **NX_SNMP_ERROR_BADVALUE** (0x03) Dizedeki geçersiz karakter
- **NX_SNMP_ERROR_WRONGTYPE** (0x07) Geçersiz nesne türü.
- **NX_PTR_ERROR** (0x07) Geçersiz giriş işaretçisi

### <a name="allowed-from"></a>İzin Verilen

Başlatma, İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Set the value of sysContact (1.3.6.1.2.1.1.4.0) from the 
   ASCII string in my_object.  */
status =  nx_snmp_object_string_set(sysContact, my_object);

/* If status is NX_SUCCESS, sysContact now contains the new ASCII string. */
```

## <a name="nx_snmp_object_timetics_get"></a>nx_snmp_object_timetics_get
Timetics nesnesini al 

### <a name="prototype"></a>Prototype

```c
UINT  nx_snmp_object_timetics_get(VOID *source_ptr, 
                                  NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a>Description

Bu hizmet, kaynak işaretçi tarafından belirtilen adreste saat saatlerini almak ve NetX nesne veri yapısına yer almaktadır. Bu yordam genellikle GET veya GETNEXT uygulama geri çağırma yordamından çağrılır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **source_ptr** Timetics kaynağının işaretçisi.
- **object_data** Hedef nesne yapısına işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Timetics nesnesi başarıyla alındı.
- **NX_PTR_ERROR** (0x07) Geçersiz giriş işaretçisi

### <a name="allowed-from"></a>İzin Verilen

Başlatma, İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Get the value of the sysUpTime (1.3.6.1.2.1.1.3.0) and place 
   it in my_object for return.  */
status =  nx_snmp_object_timetics_get(sysUpTime, my_object);

/* If status is NX_SUCCESS, the my_object now contains the sysUpTime value. */
```

## <a name="nx_snmp_object_timetics_set"></a>nx_snmp_object_timetics_set
Timetics nesnesini ayarlama 

### <a name="prototype"></a>Prototype

```c
UINT  nx_snmp_object_timetics_set(VOID *destination_ptr, 
                                  NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a>Description

Bu hizmet, Hedef işaretçi tarafından belirtilen adreste saat saat değişkenlerini NetX nesne veri yapısında zamantiklerle ayarlar.
Bu yordam genellikle SET uygulaması geri çağırma yordamından çağrılır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **destination_ptr** Timetics hedefi işaretçisi.
- **object_data** Zamantics kaynağı nesne yapısına işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Timetics nesnesi başarıyla ayarlanmıştır.
- **NX_SNMP_ERROR_WRONGTYPE** (0x07) Geçersiz nesne türü.
- **NX_PTR_ERROR** (0x07) Geçersiz giriş işaretçisi

### <a name="allowed-from"></a>İzin Verilen

Başlatma, İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Set the value of “my_time” from the timetics value in my_object.  */
status =  nx_snmp_object_timetics_set(&my_time, my_object);

/* If status is NX_SUCCESS, my_time now contains the new timetics. */
```