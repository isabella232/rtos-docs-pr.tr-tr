---
title: Bölüm 3 - Azure RTOS NetX Noktadan Noktaya Protokolü (PPP) hizmetlerinin açıklaması
description: Bu bölümde, tüm NetX PPP Azure RTOS (aşağıda listelenmiştir) alfabetik sırada bir açıklama yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 980348b5c50acfb82b2d8fda8786a1d48bf59c69e7949b6f62b64515b59bf42d
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116798767"
---
# <a name="chapter-3---description-of-azure-rtos-netx-point-to-point-protocol-ppp-services"></a>Bölüm 3 - Azure RTOS NetX Noktadan Noktaya Protokolü (PPP) hizmetlerinin açıklaması

Bu bölümde, tüm NetX PPP Azure RTOS (aşağıda listelenmiştir) alfabetik sırada bir açıklama yer almaktadır.

Aşağıdaki API açıklamalarında yer alan "Dönüş Değerleri" bölümünde, **KALıN**  olmayan değerler tamamen devre dışı bırakılırken, BOLD NX_DISABLE_ERROR_CHECKING API hata denetimlerini devre dışı bırakmak için kullanılan tanımdan etkilenmez.

- **nx_ppp_byte_receive:** *Seri ISR'den bir byte alma*
- **nx_ppp_chap_challenge:** CHAP *challenge oluşturma*
- **nx_ppp_chap_enable:** CHAP *kimlik doğrulamasını etkinleştirme*
- **nx_ppp_create:** *PPP örneği oluşturma*
- **nx_ppp_delete:** *PPP örneğini silme*
- **nx_ppp_dns_address_get:** DNS *IP adresini al*
- **nx_ppp_dns_address_set:***DNS Sunucusu IP adresini ayarlama*
- **nx_ppp_secondary_dns_address_get:** *İkincil DNS Sunucusu IP adresini al*
- **nx_ppp_secondary_dns_address_set:** Secondary_DNS *Sunucusu IP adresini ayarlayın*
- **nx_ppp_interface_index_get:** IP *arabirimi dizinini al*
- **nx_ppp_ip_address_assign:** *IPCP için IP adresleri atama*
- **nx_ppp_link_down_notify:** Bağlantıyı *kapatarak uygulamayı bilgilendirme*
- **nx_ppp_link_up_notify:** *Uygulamayı bağlantı durumuna bildirme*
- **nx_ppp_nak_authentication_notify:** KIMLIK *doğrulaması ALıNDı ise uygulamaya bildirme*
- **nx_ppp_pap_enable:** *PAP kimlik doğrulamasını etkinleştirme*
- **nx_ppp_ping_request:** *LCP yankı isteği gönderme*
- **nx_ppp_raw_string_send:** *PPP olmayan dize gönderme*
- **nx_ppp_restart:** *PPP işlemeyi yeniden başlatın*
- **nx_ppp_start:** *PPP işlemeyi başlatma*
- **nx_ppp_status_get:** *Geçerli PPP durumunu al*
- **nx_ppp_stop:** *PPP işlemeyi durdurma*
- **nx_ppp_packet_receive:** *PPP paketini alma*
- **nx_ppp_packet_send_set:** *PPP paket gönderme işlevini ayarlama*

## <a name="nx_ppp_byte_receive"></a>nx_ppp_byte_receive

Seri ISR'den bir byte alma

### <a name="prototype"></a>Prototype

```c
UINT nx_ppp_byte_receive(NX_PPP *ppp_ptr, UCHAR byte);
```

### <a name="description"></a>Description

Bu hizmet genellikle alınan bir bayta PPP'ye aktarım için uygulamanın seri sürücüsü Kesme Hizmeti Yordamı'dan (ISR) çağrılır. Çağrıldık, bu yordam alınan bayta döngüsel bir byte arabelleğine yer ve işleme için uygun PPP iş parçacığını bilgi sağlar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ppp_ptr:** PPP denetim bloğuna işaretçi.
- **byte:** Seri cihazdan alınan byte

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:**(0x00) Başarılı PPP bayt alma.
- **NX_PPP_BUFFER_FULL:**(0xB1) PPP seri arabelleği zaten dolu.
- NX_PTR_ERROR: (0x07) Geçersiz PPP işaretçisi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları, ISR'ler

### <a name="example"></a>Örnek

```c
/* Notify “my_ppp” of a received byte. */
status =  nx_ppp_byte_receive(&my_ppp, new_byte);

/* If status is NX_SUCCESS the received byte was successfully
   buffered. */
```

## <a name="nx_ppp_chap_challenge"></a>nx_ppp_chap_challenge

CHAP challenge oluşturma

### <a name="prototype"></a>Prototype

```c
UINT nx_ppp_chap_challenge(NX_PPP *ppp_ptr);
```

### <a name="description"></a>Description

Bu hizmet, PPP bağlantısı zaten çalışıyor durumda olduktan sonra bir CHAP zorluk başlatıyor. Bu, uygulamaya bağlantının orijinalliğini düzenli aralıklarla doğrulama olanağı sağlar. Zorluk başarısız olursa PPP bağlantısı kapatılır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ppp_ptr:** PPP denetim bloğuna işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:**(0x00) Başarılı PPP challenge başlatıldı.
- **NX_PPP_FAILURE:**(0xB0) Geçersiz PPP, CHAP yalnızca yanıt için etkinleştirildi.
- **NX_NOT_IMPLEMENTED:**(0x80) CHAP mantığı, NX_PPP_DISABLE_CHAP.
- NX_PTR_ERROR: (0x07) Geçersiz PPP işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Initiate a PPP challenge for instance “my_ppp”. */
status =  nx_ppp_chap_challenge(&my_ppp);

/* If status is NX_SUCCESS a CHAP challenge “my_ppp” was successfully 
initiated. */
```

## <a name="nx_ppp_chap_enable"></a>nx_ppp_chap_enable

CHAP kimlik doğrulamasını etkinleştirme

### <a name="prototype"></a>Prototype

```c
UINT nx_ppp_chap_enable(NX_PPP *ppp_ptr, 
                        UINT (*get_challenge_values)(CHAR *rand_value,CHAR *id,CHAR *name),
                        UINT (*get_responder_values)(CHAR *system,CHAR *name,CHAR *secret),
                        UINT (*get_verification_values)(CHAR *system,CHAR *name,CHAR *secret)); 
```

### <a name="description"></a>Description

Bu hizmet, Challenge-Handshake PPP örneği için Kimlik Doğrulama Protokolü'ne (CHAP) olanak sağlar.

"***get_challenge_values**_" ve "_ get_verification_values **" işlev işaretçileri belirtilirse, bu PPP örneği IÇIN CHAP * gereklidir. Aksi takdirde CHAP yalnızca eşlerin zorluk isteklerine yanıt verir.

Gerekli geri çağırma işlevlerinde aşağıda başvurulan çeşitli veri öğeleri vardır. Gizli dizi *,* ad  ve *sistem* veri öğelerinin, en fazla NX_PPP_NAME_SIZE-1 boyutuna sahip NULL sonlandırıldı dizeleri olması beklenir. Veri *rand_value,* en fazla NX_PPP_VALUE_SIZE-1 boyutuna sahip NULL sonlandırmalı bir dize olması beklenir. Veri öğesi *kimliği,* basit bir imzasız karakter t type'dır.

>[!NOTE]
> Bu işlev, nx_ppp_create *sonra ancak* nx_ip_create veya nx_ip_interface_attach. 

### <a name="input-parameters"></a>Giriş Parametreleri

- **ppp_ptr:** PPP denetim bloğuna işaretçi.
- **get_challenge_values:** Zorluk için kullanılan değerleri almak için uygulama işlevinin işaretçisi. Rand_value *,* *id* ve secret *değerlerinin* sağlanan hedeflere kopyalanmalıdır.
- **get_responder_values:** Bir soruna yanıt vermek için kullanılan değerleri alan uygulama işlevinin işaretçisi. Sistem, *ad* *ve gizli* *değerlerin sağlanan* hedeflere kopyalanmalıdır.
- **get_verification_values:** Test yanıtını doğrulamak için kullanılan değerleri alan uygulama işlevinin işaretçisi. Sistem, *ad**ve gizli* *değerlerin sağlanan* hedeflere kopyalanmalıdır.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:**(0x00) Başarılı PPP CHAP etkinleştirmesi
- **NX_NOT_IMPLEMENTED:**(0x80) CHAP mantığı, NX_PPP_DISABLE_CHAP.
- NX_PTR_ERROR: (0x07) Geçersiz PPP işaretçisi veya geri çağırma işlevi işaretçisi. Bir *get_challenge_values* belirtilirse, get_verification_values *işlevinin* de sağlanmalıdır.
- NX_CALLER_ERROR: (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, iş parçacıkları

### <a name="example"></a>Örnek

```c
CHAR    name_string[] = "username";
CHAR    rand_value_string[] = "123456";
CHAR    system_string[] = "system";
CHAR    secret_string[] = "secret";

/* Enable CHAP in both directions (CHAP challenger and CHAP responder) for 
“my_ppp”. */
status =  nx_ppp_chap_enable(&my_ppp,   get_challenge_values, 
                              get_responder_values,
                              get_verification_values);


/* If status is NX_SUCCESS, “my_ppp” has CHAP enabled. */
/* Define the CHAP enable routines.  */
UINT  get_challenge_values(CHAR *rand_value, CHAR *id, CHAR *name)
{
   UINT    i;
   for (i = 0; i< (NX_PPP_NAME_SIZE-1); i++)
   {
      name[i] = name_string[i];
   }
   name[i] =  0;
   
   *id =  '1';  /* One byte  */
   for (i = 0; i< (NX_PPP_VALUE_SIZE-1); i++)
   {
      rand_value[i] =  rand_value_string[i];
   }
   rand_value[i] =  0;
   
   return(NX_SUCCESS);  
}


UINT  get_responder_values(CHAR *system, CHAR *name, CHAR *secret)
{
   UINT    i;
   
   for (i = 0; i< (NX_PPP_NAME_SIZE-1); i++)
   {
      name[i] = name_string[i];
   }
   name[i] =  0;

   for (i = 0; i< (NX_PPP_NAME_SIZE-1); i++)
   {
      system[i] =  system_string[i];
   }
   system[i] =  0;
   
   for (i = 0; i< (NX_PPP_NAME_SIZE-1); i++)
   {
      secret[i] =  secret_string[i];
   }
   secret[i] =  0;
   
   return(NX_SUCCESS);  
}

UINT  get_verification_values(CHAR *system, CHAR *name, CHAR *secret)
{
   UINT    i;
   
   for (i = 0; i< (NX_PPP_NAME_SIZE-1); i++)
   {
      name[i] = name_string[i];
   }
   name[i] =  0;
   
   for (i = 0; i< (NX_PPP_NAME_SIZE-1); i++)
   {
      system[i] =  system_string[i];
   }
   system[i] =  0;
   
   for (i = 0; i< (NX_PPP_NAME_SIZE-1); i++)
   {
      secret[i] =  secret_string[i];
   }
   secret[i] =  0;
   
   return(NX_SUCCESS);  
}

```
## <a name="nx_ppp_create"></a>nx_ppp_create

PPP örneği oluşturma

### <a name="prototype"></a>Prototype

```c
UINT  nx_ppp_create(NX_PPP *ppp_ptr, CHAR *name, NX_IP *ip_ptr, 
                    VOID *stack_memory_ptr, ULONG stack_size, 
                    UINT thread_priority, NX_PACKET_POOL *pool_ptr,
                    void (*ppp_invalid_packet_handler)(NX_PACKET *packet_ptr),
                    void (*ppp_byte_send)(UCHAR byte));
```

### <a name="description"></a>Description

Bu hizmet, belirtilen NetX IP örneği için bir PPP örneği oluşturur.

>[!NOTE]
> NetX IP iş parçacığını PPP iş parçacığı önceliklerinden daha yüksek bir önceliğe sahip olarak oluşturmak genellikle iyi bir fikirdir. IP iş parçacığı *nx_ip_create* belirtme hakkında daha fazla bilgi için lütfen nx_ip_create hizmetine bakın.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ppp_ptr:** PPP denetim bloğuna işaretçi.
- **name:** Bu PPP örneğinin adı.
- **ip_ptr:** Henüz oluşturulmamış IP örneği için denetim bloğuna işaretçi.
- **stack_memory_ptr:** PPP iş parçacığının yığın alanı başlangıç işaretçisi.
- **stack_size:** İş parçacığı yığınında bayt cinsinden boyut.
- **pool_ptr:** Varsayılan paket havuzunun işaretçisi.
- **thread_priority:** İç PPP iş parçacıklarının önceliği (1-31).
- **ppp_invalid_packet_handler:** PPP olmayan tüm paketler için uygulamanın işleyicisine işlev işaretçisi. NetX PPP genellikle başlatma sırasında bu yordamı arar. Burası, uygulamanın modem komutlarına yanıt verebiliyor veya Windows XP'de NetX PPP uygulaması, Windows XP tarafından gönderilen ilk "CLIENT" istemci sunucusuna yanıt olarak PPP'yi başlatabiliyor.
- **ppp_byte_send:** Uygulamanın seri bayt çıkış yordamına işlev işaretçisi.


### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:**(0x00) Başarılı PPP oluşturma.
- NX_PTR_ERROR: (0x07) Geçersiz PPP, IP veya byte çıkış işlevi işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Create “my_ppp” for IP instance “my_ip”. */
status =  nx_ppp_create(&my_ppp, “my PPP”, &my_ip, stack_start, 1024, 2, 
                        &my_pool, my_invalid_packet_handler, my_out_byte);

/* If status is NX_SUCCESS the PPP instance was successfully
   created. */
```

## <a name="nx_ppp_delete"></a>nx_ppp_delete

PPP örneğini silme

### <a name="prototype"></a>Prototype

```c
UINT nx_ppp_delete(NX_PPP *ppp_ptr);
```

### <a name="description"></a>Description

Bu hizmet, daha önce oluşturulan PPP örneğini siler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ppp_ptr:** PPP denetim bloğuna işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:**(0x00) PpP silme işlemi başarılı.
- NX_PTR_ERROR: (0x07) Geçersiz PPP işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Delete PPP instance “my_ppp”. */
status =  nx_ppp_delete(&my_ppp);

/* If status is NX_SUCCESS the “my_ppp” was successfully deleted. */
```

## <a name="nx_ppp_dns_address_get"></a>nx_ppp_dns_address_get

DNS IP adresi al

### <a name="prototype"></a>Prototype

```c
UINT nx_ppp_dns_address_get(NX_PPP *ppp_ptr, ULONG *dns_address_ptr);
```

### <a name="description"></a>Description

Bu hizmet, eş tarafından sağlanan DNS IP adresini almaktadır. Eş tarafından ip adresi sağlanmadı ise 0 IP adresi döndürülür.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ppp_ptr:** PPP denetim bloğuna işaretçi.
- **dns_address_ptr:** DNS IP adresi hedefi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:**(0x00) Başarılı PPP adresi get.
- **NX_PPP_NOT_ESTABLISHED:**(0xB5) PPP eşle anlaşmayı tamamlanmadı.
- NX_PTR_ERROR: (0x07) Geçersiz PPP işaretçisi.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, iş parçacıkları, süreerler, ISR'ler

### <a name="example"></a>Örnek

```c

ULONG  my_dns_address;

/* Get IP Server address supplied by peer. */
status =  nx_ppp_dns_address_get(&my_ppp, &my_dns_address);

/* If status is NX_SUCCESS the “my_dns_address” contains the DNS IP address – 
   if the peer supplied one. */
```

## <a name="nx_ppp_secondary_dns_address_get"></a>nx_ppp_secondary_dns_address_get

İkincil DNS Sunucusu IP adresini al

### <a name="prototype"></a>Prototype

```c
UINT nx_ppp_secondary_dns_address_get(NX_PPP *ppp_ptr, ULONG *dns_address_ptr);
```

### <a name="description"></a>Description

Bu hizmet, IPCP el sıkışması içinde eş tarafından sağlanan ikincil DNS IP adresini alın. Eş tarafından ip adresi sağlanmadı ise 0 IP adresi döndürülür.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ppp_ptr:** PPP denetim bloğuna işaretçi.
- **dns_address_ptr:** İkincil DNS sunucusu adresi hedefi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:**(0x00) Başarılı DNS adresi get.
- **NX_PPP_NOT_ESTABLISHED:**(0xB5) PPP eşle anlaşmayı tamamlanmadı.
- NX_PTR_ERROR: (0x07) Geçersiz PPP işaretçisi.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, iş parçacıkları, süreerler, ISR'ler

### <a name="example"></a>Örnek

```c
ULONG  my_dns_address;

/* Get secondary DNS Server address supplied by peer. */
status =  nx_ppp_secondary_dns_address_get(&my_ppp, &my_dns_address);

/* If status is NX_SUCCESS the “my_dns_address” contains the secondary DNS Server address – if the peer supplied one. */
```

## <a name="nx_ppp_dns_address_set"></a>nx_ppp_dns_address_set

Birincil DNS Sunucusu IP adresini ayarlama

### <a name="prototype"></a>Prototype

```c
UINT nx_ppp_dns_address_set(NX_PPP *ppp_ptr, ULONG dns_address);
```

### <a name="description"></a>Description

Bu hizmet DNS Sunucusu IP adresini ayarlar. Eş IPCP durumuna bir DNS Sunucusu seçenek isteği gönderirse, bu konak bilgileri sağlar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ppp_ptr:** PPP denetim bloğuna işaretçi.
- **dns_address:** DNS sunucusu adresi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:**(0x00) Başarılı DNS adresi kümesi.
- **NX_PPP_NOT_ESTABLISHED:**(0xB5) PPP eşle anlaşmayı tamamlanmadı.
- NX_PTR_ERROR: (0x07) Geçersiz PPP işaretçisi.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, iş parçacıkları

### <a name="example"></a>Örnek

```c

ULONG  my_dns_address = IP_ADDRESS(1,2,3,1);

/* Set DNS Server address. */
status =  nx_ppp_dns_address_set(&my_ppp, my_dns_address);

/* If status is NX_SUCCESS the “my_dns_address” will be the DNS Server address provided if the peer requests one. */

```

## <a name="nx_ppp_secondary_dns_address_set"></a>nx_ppp_secondary_dns_address_set

İkincil DNS Sunucusu IP adresini ayarlama

### <a name="prototype"></a>Prototype

```c
UINT nx_ppp_secondary_dns_address_set(NX_PPP *ppp_ptr, ULONG dns_address);
```

### <a name="description"></a>Description

Bu hizmet ikincil DNS Sunucusu IP adresini ayarlar. Eş IPCP durumda ikincil bir DNS Sunucusu seçenek isteği gönderirse, bu konak bilgileri sağlar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ppp_ptr:** PPP denetim bloğuna işaretçi.
- **dns_address:** İkincil DNS sunucusu adresi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:**(0x00) Başarılı DNS adresi kümesi. 
- **NX_PPP_NOT_ESTABLISHED:**(0xB5) PPP eşle anlaşmayı tamamlanmadı.
- NX_PTR_ERROR: (0x07) Geçersiz PPP işaretçisi.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, iş parçacıkları

### <a name="example"></a>Örnek

```c
ULONG  my_dns_address = IP_ADDRESS(1,2,3,1);

/* Set DNS Server address. */
status =  nx_ppp_secondary_dns_address_set(&my_ppp, my_dns_address);

/* If status is NX_SUCCESS the “my_dns_address” will be the secondary DNS Server address provided if the peer requests one. */

```
## <a name="nx_ppp_interface_index_get"></a>nx_ppp_interface_index_get

IP arabirimi dizinini al

### <a name="prototype"></a>Prototype

```c
UINT nx_ppp_interface_index_get(NX_PPP *ppp_ptr, UINT *index_ptr);
```

### <a name="description"></a>Description

Bu hizmet, bu PPP örneğiyle ilişkili IP arabirimi dizinini almaktadır. Bu, yalnızca PPP örneği bir IP örneğinin birincil arabirimi olmadığında yararlıdır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ppp_ptr**: PPP denetim bloğu işaretçisi.
- **index_ptr**: arabirim dizini hedefi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı PPP dizini Get.
- **NX_IN_PROGRESS**: (0x37) PPP başlatmayı tamamlamadı.
- NX_PTR_ERROR: (0x07) geçersiz PPP işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar, ISRs

### <a name="example"></a>Örnek

```c
ULONG  my_index;

/* Get the interface index for this PPP instance. */
status =  nx_ppp_interface_index_get(&my_ppp, &my_index);

/* If status is NX_SUCCESS the “my_index” contains the IP interface index for
   this PPP instance. */

```
## <a name="nx_ppp_ip_address_assign"></a>nx_ppp_ip_address_assign

IPCP için IP adresleri atama

### <a name="prototype"></a>Prototype

```c
UINT nx_ppp_ip_address_assign(NX_PPP *ppp_ptr, ULONG local_ip_address, 
            ULONG peer_ip_address);
```

### <a name="description"></a>Description

Bu hizmet, Internet Protokolü Denetim Protokolü 'nde (ıPCP) kullanılmak üzere yerel ve eş IP adreslerini ayarlar. PPP uygulaması bu hizmeti, kendisi ve diğer eşdüzey için geçerli IP adreslerine sahip bir PPP örneğinde çağırmalıdır.  Bir PPP örneğiyle kayıtlı geçerli bir adres yoksa, IP adresini tanımlamak için PPP eşine güvenmelidir.


### <a name="input-parameters"></a>Giriş Parametreleri

- **ppp_ptr**: PPP denetim bloğu işaretçisi.
- **local_ip_address**: yerel IP adresi.
- **peer_ip_address**: eşin IP adresi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı PPP adresi ataması.
- NX_PTR_ERROR: (0x07) geçersiz PPP işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Set IP addresses for “my_ppp”. */
status =  nx_ppp_ip_address_assign(&my_ppp, IP_ADDRESS(256,2,2,187), 
IP_ADDRESS(256,2,2,188));


/* If status is NX_SUCCESS the “my_ppp” has the IP addresses. */
```

## <a name="nx_ppp_link_down_notify"></a>nx_ppp_link_down_notify

Bağlantıyı aşağı bağlantıda bilgilendir

### <a name="prototype"></a>Prototype

```c
UINT nx_ppp_link_down_notify(NX_PPP *ppp_ptr, 
                             VOID (*link_down_callback)(NX_PPP *ppp_ptr));
```

### <a name="description"></a>Description

Bu hizmet, uygulamanın bağlantı azaltma bildirimi geri aramasını belirtilen PPP örneğiyle kaydeder. NULL değilse, bağlantının geri çağırma işlevi, bağlantı her gittiğinde çağrılır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ppp_ptr**: PPP denetim bloğu işaretçisi.
- **link_down_callback**: uygulamanın bağlantı azaltma uyarısı işlev işaretçisi. NULL ise, bağlantı azaltma bildirimi devre dışıdır.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) bildirim geri çağırma kaydı başarıyla açıldı.
- NX_PTR_ERROR: (0x07) geçersiz PPP işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar, ISRs

### <a name="example"></a>Örnek

```c
/* Register “my_link_down_callback” to be called whenever the PPP
   link goes down. */
status =  nx_ppp_link_down_notify(&my_ppp, my_link_down_callback);


/* If status is NX_SUCCESS the function “my_link_down_callback” has been
   registered with this PPP instance. */

VOID my_link_down_callback(NX_PPP *ppp_ptr)
{

/* On link down, simply restart PPP.  */
    nx_ppp_restart(ppp_ptr);
} 
```
## <a name="nx_ppp_link_up_notify"></a>nx_ppp_link_up_notify

Bağlantı üzerinde uygulamayı bilgilendir

### <a name="prototype"></a>Prototype

```c
UINT nx_ppp_link_up_notify(NX_PPP *ppp_ptr, 
                           VOID (*link_up_callback)(NX_PPP *ppp_ptr));
```
### <a name="description"></a>Description

Bu hizmet, uygulamanın bağlantı bildirimi geri aramasını belirtilen PPP örneğiyle kaydeder. NULL olmadığında, bağlantının geri çağırma işlevi bağlantı her geldiğinde çağrılır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ppp_ptr**: PPP denetim bloğu işaretçisi.
- **link_up_callback**: uygulamanın bağlantı bildirim işlevi işaretçisi. NULL ise, bağlantı bildirimi devre dışıdır. * *

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı bağlantı geri çağırma kaydı.
- NX_PTR_ERROR: (0x07) geçersiz PPP işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar, ISRs

### <a name="example"></a>Örnek

```c
/* Register “my_link_up_callback” to be called whenever the PPP
   link comes up. */
status =  nx_ppp_link_up_notify(&my_ppp, my_link_up_callback);


/* If status is NX_SUCCESS the function “my_link_up_callback” has been
   registered with this PPP instance. */

VOID my_link_up_callback(NX_PPP *ppp_ptr)
{
    /* On link up, the application my want to start sending/receiving
       UPD/TCP data.  */
}
```

## <a name="nx_ppp_nak_authentication_notify"></a>nx_ppp_nak_authentication_notify

Kimlik doğrulama NAK 'ı alındı ise uygulamayı bilgilendir

### <a name="prototype"></a>Prototype

```c
UINT    nx_ppp_nak_authentication_notify(NX_PPP *ppp_ptr, 
                                         void (*nak_authentication_notify)(void));
```

### <a name="description"></a>Description

Bu hizmet, uygulamanın kimlik doğrulama nak Notification geri aramasını belirtilen PPP örneğiyle kaydeder. NULL değilse, bu geri çağırma işlevi, bir authentiaction sırasında her bir bir NAK aldığında çağırılır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ppp_ptr**: PPP denetim bloğu işaretçisi.
- **nak_authentication_notify**: PPP örneği bir KIMLIK doğrulama nak 'ı aldığında çağrılan işlev işaretçisi. NULL ise, bildirim devre dışı bırakılır.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı bildirim geri çağırma kaydı.
- NX_PTR_ERROR: (0x07) geçersiz PPP işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar, ISRs

### <a name="example"></a>Örnek

```c
/* Register “my_nak_auth_callback” to be called whenever the PPP
   receives a NAK during authentication. */
status =  nx_ppp_nak_authentication_notify(&my_ppp, my_nak_auth_callback);

/* If status is NX_SUCCESS the function “my_nak_auth_callback” has been
   registered with this PPP instance. */

VOID my_nak_auth_callback(NX_PPP *ppp_ptr)
{
   /* Handle the situation of receiving an authentication NAK */
}

```

## <a name="nx_ppp_pap_enable"></a>nx_ppp_pap_enable

PAP kimlik doğrulamasını etkinleştir

### <a name="prototype"></a>Prototype

```c

UINT  nx_ppp_pap_enable(NX_PPP *ppp_ptr, 
                        UINT (*generate_login)(CHAR *name, CHAR *password),
                        UINT (*verify_login)(CHAR *name, CHAR *password));
```

### <a name="description"></a>Description

Bu hizmet, belirtilen PPP örneği için parola kimlik doğrulama protokolü 'Nü (PAP) sunar. "***Verify_login***" işlev işaretçisi belirtilmişse, bu PPP ÖRNEĞI için PAP gereklidir. Aksi halde, PAP yalnızca LCP anlaşması sırasında belirtildiği gibi eşin PAP gereksinimlerine yanıt verir.

Gerekli geri çağırma işlevlerinde aşağıda başvurulan birkaç veri öğesi vardır. Veri öğesi *adının* , en fazla NX_PPP_NAME_SIZE-1 boyutuna sahip null ile sonlandırılmış dize olması beklenir. Veri öğesi *parolasının* , en fazla NX_PPP_PASSWORD_SIZE-1 boyutuna sahip null ile sonlandırılmış bir dize olması da beklenir.

>[!NOTE]
> Bu işlev, *nx_ppp_create* sonra, *nx_ip_create* veya *nx_ip_interface_attach* önce çağrılmalıdır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ppp_ptr**: PPP denetim bloğu işaretçisi.
- **generate_login**: eş tarafından kimlik doğrulaması için *ad* ve *parola* üreten uygulama işlevi işaretçisi. *Ad* ve *parola* değerlerinin sağlanan hedeflere kopyalanması gerektiğini unutmayın.
- **verify_login**: eş tarafından sağlanan *adı* ve *parolayı* doğrulayan uygulama işlevi işaretçisi. Bu yordam, sağlanan *adı* ve *parolayı* karşılaştırmalıdır. Bu yordam NX_SUCCESS döndürürse, ad ve parola doğru ve PPP sonraki adıma geçebilirler. Aksi takdirde, bu yordam NX_PPP_ERROR döndürür ve PPP yalnızca başka bir ad ve parola bekler.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı PPP PAP etkinleştirmesi.
- **NX_NOT_IMPLEMENTED**: (0x80) PAP mantığı NX_PPP_DISABLE_PAP aracılığıyla devre dışı bırakıldı.
- NX_PTR_ERROR: (0x07) geçersiz PPP işaretçisi veya uygulama işlevi işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="example"></a>Örnek

```c
CHAR    name_string[] = "username";
CHAR    password_string[] =  "password";

/* Enable PAP for PPP instance “my_ppp”. */
status =  nx_ppp_pap_enable(&my_ppp, my_generate_login, my_verify_login);

/* If status is NX_SUCCESS the “my_ppp” now has PAP enabled. */

/* Define callback routines for PAP enable.  */

UINT  generate_login(CHAR *name, CHAR *password)
{

UINT    i;

for (i = 0; i< (NX_PPP_NAME_SIZE-1); i++)
name[i] = name_string[i];
name[i] =  0;

for (i = 0; i< (NX_PPP_PASSWORD_SIZE-1); i++)
password[i] = password_string[i];
password_string[i] =  0;

return(NX_SUCCESS);  
}

UINT  verify_login(CHAR *name, CHAR *password)
{

/* Assume name and password are correct. Normally, 
a comparison would be made here!  */
printf("Name: %s, Password: %s\n", name, password);

return(NX_SUCCESS);  
}
```

## <a name="nx_ppp_ping_request"></a>nx_ppp_ping_request

Bir LCP ping isteği gönder

### <a name="prototype"></a>Prototype

```c
UINT  nx_ppp_ping_request(NX_PPP *ppp_ptr, CHAR *data, 
                          UINT data_size, ULONG wait_opion);
```

### <a name="description"></a>Description

Bu hizmet bir LCP ping isteği gönderir ve PPP cihazının yankı yanıtı beklediğini belirten bir bayrak ayarlar. İstek gönderildikten hemen sonra hizmet döndürülür. Yanıt beklemez. 

Eşleşen bir yankı yanıtı alındığında, PPP iş parçacığı görevi bayrağı temizler. PPP cihazının, PPP anlaşmasının LCP bölümünü tamamlamış olması gerekir.

Bu hizmet, bağlantı durumu için donanımın yoklanamaması mümkün olmayabilir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ppp_ptr**: PPP denetim bloğu işaretçisi.
- **veri**: yankı isteğine gönderilmek üzere veri işaretçisi.
- **data_size**: LCP yankı iletisini göndermek için beklenecek wait_option zaman göndermek için veri boyutu.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) gönderilen yankı Isteği başarılı oldu.
- **NX_PPP_NOT_ESTABLISHED**: (0xb5) PPP bağlantısı kurulmadı.
- NX_PTR_ERROR: (0x07) geçersiz PPP işaretçisi veya uygulama işlevi işaretçisi.
- NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

Uygulama iş parçacıkları

### <a name="example"></a>Örnek

```c

CHAR    buffer[] = "username";
UINT    buffer_length =  strlen("username ");

/* Send an LCP ping request”. */
status =  nx_ppp_ping_request(&my_ppp, &buffer[0], buffer_length, 200);

/* If status is NX_SUCCESS the LCP echo request was successfully sent. Now wait to 
   receive a response. */

while(my_ppp.nx_ppp_lcp_echo_reply_id > 0)
{
    tx_thread_sleep(100);
}

/* Got a valid reply! */
```

## <a name="nx_ppp_raw_string_send"></a>nx_ppp_raw_string_send

Ham ASCII dizesi gönder

### <a name="prototype"></a>Prototype

```c
UINT  nx_ppp_raw_sting_send(NX_PPP *ppp_ptr, CHAR *string_ptr);
```

### <a name="description"></a>Description

Bu hizmet, PPP arabiriminden doğrudan PPP olmayan bir ASCII dizesi gönderir. PPP, modem denetimi bilgilerini içeren PPP olmayan bir paket aldıktan sonra genellikle kullanılır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ppp_ptr**: PPP denetim bloğu işaretçisi.
- **string_ptr**: gönderileceği dize işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı PPP ham dize gönderme.
- NX_PTR_ERROR: (0x07) geçersiz PPP işaretçisi veya dize işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c

/* Send “CLIENTSERVER” to “CLIENT” sent by Windows 98 before PPP is
initiated.  */
status =  nx_ppp_raw_string_send(&my_ppp, “CLIENTSERVER”);

/* If status is NX_SUCCESS the raw string was successfully Sent via PPP. */
```
## <a name="nx_ppp_restart"></a>nx_ppp_restart

PPP işlemesini yeniden Başlat

### <a name="prototype"></a>Prototype

```c
UINT  nx_ppp_restart(NX_PPP *ppp_ptr);
```

### <a name="description"></a>Description

Bu hizmet, PPP işlemini yeniden başlatır. Genellikle bağlantının bir bağlantı geri çağrısından veya iletişimin kaybedilmediğini belirten PPP olmayan bir modem iletisiyle yeniden oluşturulması gerektiğinde çağrılır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ppp_ptr**: PPP denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı PPP yeniden başlatması başlatıldı.
- NX_PTR_ERROR: (0x07) geçersiz PPP işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Restart the PPP instance “my_ppp”.  */
status =  nx_ppp_restart(&my_ppp);

/* If status is NX_SUCCESS the PPP instance has been restarted. */
```

## <a name="nx_ppp_start"></a>nx_ppp_start

PPP işlemesini Başlat

### <a name="prototype"></a>Prototype

```c
UINT  nx_ppp_start(NX_PPP *ppp_ptr);
```

### <a name="description"></a>Description

Bu hizmet, PPP işlemini başlatır. Genellikle nx_ppp_stop () çağrıldıktan sonra çağrılır.

>[!NOTE]
> PPP, bağlantı etkinleştirildiğinde otomatik olarak PPP işlemini başlatır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ppp_ptr**: PPP denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı PPP başlatması başlatıldı. 
- **NX_PPP_ALREADY_STARTED**: (0xB9) PPP zaten başlatılmış.
- NX_PTR_ERROR: (0x07) geçersiz PPP işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Start the PPP instance “my_ppp”.  */
status =  nx_ppp_start(&my_ppp);

/* If status is NX_SUCCESS the PPP instance has been started. */
```

## <a name="nx_ppp_status_get"></a>nx_ppp_status_get

Geçerli PPP durumunu al

### <a name="prototype"></a>Prototype

```c
UINT  nx_ppp_status_get(NX_PPP *ppp_ptr, UINT *status_ptr);
```
### <a name="description"></a>Description

Bu hizmet, belirtilen PPP örneğinin geçerli durumunu alır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ppp_ptr**: PPP denetim bloğu işaretçisi.
- **status_ptr**: PPP durumunun hedefi, aşağıdakiler olası durum değerleridir:
    - **NX_PPP_STATUS_ESTABLISHED**
    - **NX_PPP_STATUS_LCP_IN_PROGRESS**
    - **NX_PPP_STATUS_LCP_FAILED**
    - **NX_PPP_STATUS_PAP_IN_PROGRESS**
    - **NX_PPP_STATUS_PAP_FAILED**
    - **NX_PPP_STATUS_CHAP_IN_PROGRESS**
    - **NX_PPP_STATUS_CHAP_FAILED**
    - **NX_PPP_STATUS_IPCP_IN_PROGRESS**
    - **NX_PPP_STATUS_IPCP_FAILED**

>[!NOTE]
> Durum yalnızca API NX_SUCCESS döndürürse geçerlidir. Ayrıca, * _FAILED durum değerlerinden herhangi biri döndürülürse, PPP işleme, uygulama tarafından yeniden başlatılana kadar etkili bir şekilde durdurulur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı PPP durum isteği.
- NX_PTR_ERROR: (0x07) geçersiz PPP işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar, ISRs

### <a name="example"></a>Örnek

```c
UINT ppp_status;
UINT status;


/* Get the current status of PPP instance “my_ppp”.  */
status =  nx_ppp_status_get(&my_ppp, &ppp_status);

/* If status is NX_SUCCESS the current internal PPP status is contained in
   “ppp_status”. */
```
## <a name="nx_ppp_stop"></a>nx_ppp_stop

PPP işlemeyi başlatma

### <a name="prototype"></a>Prototype

```c
UINT  nx_ppp_stop(NX_PPP *ppp_ptr);
```

### <a name="description"></a>Description

Bu hizmet PPP işlemini durdurur. Kullanıcı gerekirse PPP işlemini başlatmak için nx_ppp_start() çağrısı da kullanabilir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ppp_ptr:** PPP denetim bloğuna işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:**(0x00) Başarılı PPP başlangıcı başlatıldı. 
- **NX_PPP_ALREADY_STOPPED:**(0xb8) PPP zaten durduruldu.
- NX_PTR_ERROR: (0x07) Geçersiz PPP işaretçisi.
- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Stop the PPP instance “my_ppp”.  */
status =  nx_ppp_stop(&my_ppp);

/* If status is NX_SUCCESS the PPP instance has been stopped. */
```
## <a name="nx_ppp_packet_receive"></a>nx_ppp_packet_receive

PPP paketi alma

### <a name="prototype"></a>Prototype

```c
UINT  nx_ppp_packet_receive(NX_PPP *ppp_ptr, NX_PACKET *packet_ptr);

```

### <a name="description"></a>Description

Bu hizmet PPP paketini alır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ppp_ptr:** PPP denetim bloğuna işaretçi.
- **packet_ptr:** PPP paketinin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:**(0x00) Başarılı PPP durum isteği.
- NX_PTR_ERROR: (0x07) Geçersiz PPP işaretçisi.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Receive the PPP packet of PPP instance “my_ppp”.  */
status =  nx_ppp_packet_receive(&my_ppp, packet_ptr);

/* If status is NX_SUCCESS the PPP packet has received. */


```
## <a name="nx_ppp_packet_send_set"></a>nx_ppp_packet_send_set

PPP paket gönderme işlevini ayarlama

### <a name="prototype"></a>Prototype

```c
UINT  nx_ppp_packet_send_set(NX_PPP *ppp_ptr, 
                             VOID (*nx_ppp_packet_send)(NX_PACKET *packet_ptr));

```

### <a name="description"></a>Description

Bu hizmet, PPP paketi gönderme funciton'larını ayarlar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ppp_ptr:** PPP denetim bloğuna işaretçi.
- **nx_ppp_packet_send:** PPP paketi gönderme yordamı.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:**(0x00) Başarılı PPP durum isteği.
- NX_PTR_ERROR: (0x07) Geçersiz PPP işaretçisi.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Set the PPP packet send function of PPP instance “my_ppp”.  */
status =  nx_ppp_packet_send_set(&my_ppp, nx_ppp_packet_send);

/* If status is NX_SUCCESS the PPP packet send function has set. */


```