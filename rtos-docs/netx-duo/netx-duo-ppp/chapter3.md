---
title: Bölüm 3-Azure RTOS NetX Duo Noktadan Noktaya Protokolü (PPP) hizmetlerinin açıklaması
description: Bu bölüm, tüm Azure RTOS NetX Duo PPP hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 90c24cad5e595087ba27178243f9dda0dab11029
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825823"
---
# <a name="chapter-3---description-of-azure-rtos-netx-duo-point-to-point-protocol-ppp-services"></a>Bölüm 3-Azure RTOS NetX Duo Noktadan Noktaya Protokolü (PPP) hizmetlerinin açıklaması

Bu bölüm, tüm Azure RTOS NetX Duo PPP hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.

Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_DISABLE_ERROR_CHECKING** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.

- **nx_ppp_byte_receive**: *seri ISR 'den bayt alma*
- **nx_ppp_chap_challenge**: *CHAP sınaması oluşturma*
- **nx_ppp_chap_enable**: *CHAP kimlik doğrulamasını etkinleştir*
- **nx_ppp_create**: *bir PPP örneği oluşturma*
- **nx_ppp_delete**: *bir PPP örneğini silme*
- **nx_ppp_dns_address_get**: *DNS sunucusu IP adresini al*
- **nx_ppp_dns_address_set**:*DNS sunucusu IP adresini ayarla*
- **nx_ppp_secondary_dns_address_get**: *IKINCIL DNS sunucusu IP adresini al*
- **nx_ppp_secondary_dns_address_set**: *Secondary_DNS sunucusu IP adresini ayarla*
- **nx_ppp_interface_index_get**: *IP arabirimi dizinini al*
- **nx_ppp_ip_address_assign**: *IPCP için IP adresleri atama*
- **nx_ppp_link_down_notify**: *bağlantıyı aşağı bağlantıda bilgilendir*
- **nx_ppp_link_up_notify**: *uygulamayı bağlantıda bilgilendir*
- **nx_ppp_nak_authentication_notify**: *Authentication nak alınmışsa uygulamayı bilgilendir*
- **nx_ppp_pap_enable**: *PAP kimlik doğrulamasını etkinleştir*
- **nx_ppp_ping_request**: *bir LCP yankı isteği gönder*
- **nx_ppp_raw_string_send**: *PPP olmayan dize gönder*
- **nx_ppp_restart**: *PPP işlemeyi yeniden Başlat*
- **nx_ppp_start**: *PPP işlemeyi Başlat*
- **nx_ppp_status_get**: *geçerli PPP durumunu Al*
- **nx_ppp_stop**: *PPP işlemesini durdur*
- **nx_ppp_packet_receive**: *PPP paketi alma*
- **nx_ppp_packet_send_set**: *PPP paketi gönderme işlevini ayarla*

## <a name="nx_ppp_byte_receive"></a>nx_ppp_byte_receive

Seri ıSR 'den bayt al

### <a name="prototype"></a>Prototype

```c
UINT nx_ppp_byte_receive(NX_PPP *ppp_ptr, UCHAR byte);
```

### <a name="description"></a>Açıklama

Bu hizmet genellikle uygulamanın seri sürücü kesme hizmeti yordamından (ıSR), alınan bir baytı PPP 'ye aktarmak için çağrılır. Çağrıldığında, bu yordam alınan baytı bir dairesel bayt arabelleğine koyar ve uygun PPP iş parçacığını işlemeye bildirir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ppp_ptr**: PPP denetim bloğu işaretçisi.
- **byte**: seri cihazdan alınan bayt

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı PPP bayt alma.
- **NX_PPP_BUFFER_FULL**: (0Xb1) PPP seri arabelleği zaten dolu.
- NX_PTR_ERROR: (0x07) geçersiz PPP işaretçisi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, ISRs

### <a name="example"></a>Örnek

```c
/* Notify “my_ppp” of a received byte. */
status =  nx_ppp_byte_receive(&my_ppp, new_byte);

/* If status is NX_SUCCESS the received byte was successfully
   buffered. */
```

## <a name="nx_ppp_chap_challenge"></a>nx_ppp_chap_challenge

CHAP sınaması oluşturma

### <a name="prototype"></a>Prototype

```c
UINT nx_ppp_chap_challenge(NX_PPP *ppp_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, PPP bağlantısı zaten çalışır durumda olduktan sonra bir CHAP sınaması başlatır. Bu, uygulamaya düzenli aralıklarla bağlantının orijinalliğini doğrulama olanağı sağlar. Sınama başarısız olursa, PPP bağlantısı kapatılır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ppp_ptr**: PPP denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı PPP sınaması başlatıldı.
- **NX_PPP_FAILURE**: (0Xb0) geçersiz PPP SıNAMASı, CHAP yalnızca yanıt için etkinleştirildi.
- **NX_NOT_IMPLEMENTED**: (0x80) CHAP mantığı NX_PPP_DISABLE_CHAP ile devre dışı bırakıldı.
- NX_PTR_ERROR: (0x07) geçersiz PPP işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Initiate a PPP challenge for instance “my_ppp”. */
status =  nx_ppp_chap_challenge(&my_ppp);

/* If status is NX_SUCCESS a CHAP challenge “my_ppp” was successfully 
initiated. */
```

## <a name="nx_ppp_chap_enable"></a>nx_ppp_chap_enable

CHAP kimlik doğrulamasını etkinleştir

### <a name="prototype"></a>Prototype

```c
UINT nx_ppp_chap_enable(NX_PPP *ppp_ptr, 
                        UINT (*get_challenge_values)(CHAR *rand_value,CHAR *id,CHAR *name),
                        UINT (*get_responder_values)(CHAR *system,CHAR *name,CHAR *secret),
                        UINT (*get_verification_values)(CHAR *system,CHAR *name,CHAR *secret)); 
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen PPP örneği için Challenge-Handshake kimlik doğrulama protokolü (CHAP) sunar.

"***Get_challenge_values**_" ve "_ * _get_verification_values_* *" işlev işaretçileri belirtilmişse, bu PPP örneği için CHAP gereklidir. Aksi halde, CHAP yalnızca eşin sınama isteklerine yanıt verir.

Gerekli geri çağırma işlevlerinde aşağıda başvurulan birkaç veri öğesi vardır. Veri öğeleri *gizli*, *adı* ve *sisteminin* , en fazla NX_PPP_NAME_SIZE-1 boyutuna sahip null ile sonlandırılmış dizeler olması beklenir. *Rand_value* veri öğesi, en fazla NX_PPP_VALUE_SIZE-1 boyutuna sahip null ile sonlandırılmış bir dize olması beklenir. Veri öğesi *kimliği* , bir basit işaretsiz karakter türüdür.

>[!NOTE]
> Bu işlev, *nx_ppp_create* sonra, nx_ip_create veya *nx_ip_interface_attach* önce çağrılmalıdır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ppp_ptr**: PPP denetim bloğu işaretçisi.
- **get_challenge_values**: zorluk için kullanılan değerleri almak için uygulama işlevine yönelik işaretçi. *Rand_value*, *kimlik* ve *gizli* değerlerinin sağlanan hedeflere kopyalanması gerektiğini unutmayın.
- **get_responder_values**: bir Challenge 'a yanıt vermek için kullanılan değerleri alan uygulama işlevi işaretçisi. *System*, *Name* ve *Secret* değerlerinin sağlanan hedeflere kopyalanması gerektiğini unutmayın.
- **get_verification_values**: sınama yanıtını doğrulamak için kullanılan değerleri alan uygulama işlevi işaretçisi. *System*,*Name* ve *Secret* değerlerinin sağlanan hedeflere kopyalanması gerektiğini unutmayın.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı PPP CHAP etkinleştir
- **NX_NOT_IMPLEMENTED**: (0x80) CHAP mantığı NX_PPP_DISABLE_CHAP ile devre dışı bırakıldı.
- NX_PTR_ERROR: (0x07) geçersiz PPP işaretçisi veya geri çağırma işlevi işaretçisi. *Get_challenge_values* belirtilmişse *get_verification_values* işlevinin da sağlanması gerektiğini unutmayın.
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

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

Bir PPP örneği oluşturma

### <a name="prototype"></a>Prototype

```c
UINT  nx_ppp_create(NX_PPP *ppp_ptr, CHAR *name, NX_IP *ip_ptr, 
                    VOID *stack_memory_ptr, ULONG stack_size, 
                    UINT thread_priority, NX_PACKET_POOL *pool_ptr,
                    void (*ppp_invalid_packet_handler)(NX_PACKET *packet_ptr),
                    void (*ppp_byte_send)(UCHAR byte));
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen NetX IP örneği için bir PPP örneği oluşturur. NetX IP örneği oluşturulmadan önce bu işlevin çağrılması gerekir.

>[!NOTE]
> Genellikle NetX IP iş parçacığını, PPP iş parçacığı önceliğinden daha yüksek bir önceliğe göre oluşturmak iyi bir fikirdir. IP iş parçacığı önceliğini belirtme hakkında daha fazla bilgi için lütfen *nx_ip_create* hizmetine bakın.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ppp_ptr**: PPP denetim bloğu işaretçisi.
- **ad**: bu PPP örneğinin adı.
- **ip_ptr**: henüz oluşturulmamış IP örneği için denetim bloğuna yönelik işaretçi.
- **stack_memory_ptr**: PPP iş parçacığının yığın alanının başlangıcı işaretçisi.
- **stack_size**: iş parçacığının yığınında bayt cinsinden boyut.
- **pool_ptr**: varsayılan paket havuzuna yönelik işaretçi.
- **thread_priority**: iç PPP iş parçacıklarının önceliği (1-31).
- **ppp_invalid_packet_handler**: tüm PPP olmayan paketler için uygulamanın işleyicisine yönelik işlev işaretçisi. NetX PPP, genellikle başlatma sırasında bu yordamı çağırır. Bu, uygulamanın modem komutlarına yanıt verebildiği veya Windows XP söz konusu olduğunda, NetX PPP uygulamasının "ISTEMCI sunucusu" ile Windows XP tarafından gönderilen ilk "ISTEMCI" ile yanıt vererek PPP başlatabilir.
- **ppp_byte_send**: uygulamanın seri baytlık çıkış yordamına yönelik işlev işaretçisi.


### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı PPP oluştur.
- NX_PTR_ERROR: (0x07) geçersiz PPP, IP veya Byte çıkış işlevi işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

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

Bir PPP örneğini silme

### <a name="prototype"></a>Prototype

```c
UINT nx_ppp_delete(NX_PPP *ppp_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, önceden oluşturulmuş PPP örneğini siler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ppp_ptr**: PPP denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı PPP silme.
- NX_PTR_ERROR: (0x07) geçersiz PPP işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Delete PPP instance “my_ppp”. */
status =  nx_ppp_delete(&my_ppp);

/* If status is NX_SUCCESS the “my_ppp” was successfully deleted. */
```

## <a name="nx_ppp_dns_address_get"></a>nx_ppp_dns_address_get

DNS sunucusu IP adresini al

### <a name="prototype"></a>Prototype

```c
UINT nx_ppp_dns_address_get(NX_PPP *ppp_ptr, ULONG *dns_address_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, bir ıPCP el sıkışmasının eşi tarafından sağlanan DNS IP adresini alır. Eş tarafından bir IP adresi sağlanmadığında, 0 IP adresi döndürülür.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ppp_ptr**: PPP denetim bloğu işaretçisi.
- **dns_address_ptr**: DNS sunucusu adresi için hedef

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı DNS adresi Get.
- **NX_PPP_NOT_ESTABLISHED**: (0xb5) PPP, eş ile anlaşmayı tamamlamadı.
- NX_PTR_ERROR: (0x07) geçersiz PPP işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar, ISRs

### <a name="example"></a>Örnek

```c

ULONG  my_dns_address;

/* Get DNS Server address supplied by peer. */
status =  nx_ppp_dns_address_get(&my_ppp, &my_dns_address);

/* If status is NX_SUCCESS the “my_dns_address” contains the DNS IP address – 
   if the peer supplied one. */
```

## <a name="nx_ppp_secondary_dns_address_get"></a>nx_ppp_secondary_dns_address_get

Ikincil DNS sunucusu IP adresini al

### <a name="prototype"></a>Prototype

```c
UINT nx_ppp_secondary_dns_address_get(NX_PPP *ppp_ptr, ULONG *dns_address_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, bir ıPCP el sıkışmasının eşi tarafından sağlanan ikincil DNS IP adresini alır. Eş tarafından bir IP adresi sağlanmadığında, 0 IP adresi döndürülür.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ppp_ptr**: PPP denetim bloğu işaretçisi.
- **dns_address_ptr**: ikincil DNS sunucusu adresi için hedef

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı DNS adresi Get.
- **NX_PPP_NOT_ESTABLISHED**: (0xb5) PPP, eş ile anlaşmayı tamamlamadı.
- NX_PTR_ERROR: (0x07) geçersiz PPP işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar, ISRs

### <a name="example"></a>Örnek

```c
ULONG  my_dns_address;

/* Get secondary DNS Server address supplied by peer. */
status =  nx_ppp_secondary_dns_address_get(&my_ppp, &my_dns_address);

/* If status is NX_SUCCESS the “my_dns_address” contains the secondary DNS Server address – if the peer supplied one. */
```

## <a name="nx_ppp_dns_address_set"></a>nx_ppp_dns_address_set

Birincil DNS sunucusu IP adresini ayarla

### <a name="prototype"></a>Prototype

```c
UINT nx_ppp_dns_address_set(NX_PPP *ppp_ptr, ULONG dns_address);
```

### <a name="description"></a>Açıklama

Bu hizmet, DNS sunucusu IP adresini ayarlar. Eş, ıPCP durumunda bir DNS sunucusu seçenek isteği gönderirse, bu ana bilgisayar bu bilgileri sağlar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ppp_ptr**: PPP denetim bloğu işaretçisi.
- **dns_address**: DNS sunucusu adresi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı DNS adresi kümesi.
- **NX_PPP_NOT_ESTABLISHED**: (0xb5) PPP, eş ile anlaşmayı tamamlamadı.
- NX_PTR_ERROR: (0x07) geçersiz PPP işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="example"></a>Örnek

```c

ULONG  my_dns_address = IP_ADDRESS(1,2,3,1);

/* Set DNS Server address. */
status =  nx_ppp_dns_address_set(&my_ppp, my_dns_address);

/* If status is NX_SUCCESS the “my_dns_address” will be the DNS Server address provided if the peer requests one. */

```

## <a name="nx_ppp_secondary_dns_address_set"></a>nx_ppp_secondary_dns_address_set

İkincil DNS sunucusu IP adresini ayarla

### <a name="prototype"></a>Prototype

```c
UINT nx_ppp_secondary_dns_address_set(NX_PPP *ppp_ptr, ULONG dns_address);
```

### <a name="description"></a>Açıklama

Bu hizmet, ikincil DNS sunucusu IP adresini ayarlar. Eş, ıPCP durumunda ikincil bir DNS sunucusu seçenek isteği gönderirse bu konak bilgileri sağlar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ppp_ptr**: PPP denetim bloğu işaretçisi.
- **dns_address**: ikincil DNS sunucusu adresi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı DNS adresi kümesi. 
- **NX_PPP_NOT_ESTABLISHED**: (0xb5) PPP, eş ile anlaşmayı tamamlamadı.
- NX_PTR_ERROR: (0x07) geçersiz PPP işaretçisi.

### <a name="allowed-from"></a>İzin verilen

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

### <a name="description"></a>Açıklama

Bu hizmet, bu PPP örneğiyle ilişkili IP arabirimi dizinini alır. Bu, yalnızca PPP örneği bir IP örneğinin birincil arabirimi olmadığında yararlıdır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ppp_ptr**: PPP denetim bloğu işaretçisi.
- **index_ptr**: arabirim dizini hedefi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı PPP dizini Get.
- **NX_IN_PROGRESS**: (0x37) PPP başlatmayı tamamlamadı.
- NX_PTR_ERROR: (0x07) geçersiz PPP işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

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

### <a name="description"></a>Açıklama

Bu hizmet, Internet Protokolü denetim protokolünde (ıPCP) kullanılmak üzere yerel ve eş IP adreslerini ayarlar. Kendisi ve diğer eşdüzey için geçerli IP adreslerine sahip olan PPP örneği için çağrılmalıdır.

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

### <a name="description"></a>Açıklama

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
### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

Bu hizmet bir LCP isteği gönderir ve PPP cihazının yankı yanıtı beklediğini belirten bir bayrak ayarlar. Bekleme seçeneği öncelikle *nx_packet_allocate* çağrısı içindir. İstek gönderildikten hemen sonra hizmet döndürülür. Yanıt beklemez. 

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
UINT    buffer_length =  sizeof("username ") - 1;

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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
### <a name="description"></a>Açıklama

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

PPP işlemesini Başlat

### <a name="prototype"></a>Prototype

```c
UINT  nx_ppp_stop(NX_PPP *ppp_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, PPP işlemini durduruyor. Kullanıcı ayrıca, gerekirse PPP işlemini başlatmak için nx_ppp_start () öğesini de çağırır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ppp_ptr**: PPP denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı PPP başlatması başlatıldı. 
- **NX_PPP_ALREADY_STOPPED**: (0xB8) PPP zaten durduruldu.
- NX_PTR_ERROR: (0x07) geçersiz PPP işaretçisi.
- NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Stop the PPP instance “my_ppp”.  */
status =  nx_ppp_stop(&my_ppp);

/* If status is NX_SUCCESS the PPP instance has been stopped. */
```
## <a name="nx_ppp_packet_receive"></a>nx_ppp_packet_receive

PPP paketi al

### <a name="prototype"></a>Prototype

```c
UINT  nx_ppp_packet_receive(NX_PPP *ppp_ptr, NX_PACKET *packet_ptr);

```

### <a name="description"></a>Açıklama

Bu hizmet, PPP paketini alır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ppp_ptr**: PPP denetim bloğu işaretçisi.
- **packet_ptr**: PPP paketine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı PPP durum isteği.
- NX_PTR_ERROR: (0x07) geçersiz PPP işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Receive the PPP packet of PPP instance “my_ppp”.  */
status =  nx_ppp_packet_receive(&my_ppp, packet_ptr);

/* If status is NX_SUCCESS the PPP packet has received. */


```
## <a name="nx_ppp_packet_send_set"></a>nx_ppp_packet_send_set

PPP paketi gönderme işlevini ayarlama

### <a name="prototype"></a>Prototype

```c
UINT  nx_ppp_packet_send_set(NX_PPP *ppp_ptr, 
                             VOID (*nx_ppp_packet_send)(NX_PACKET *packet_ptr));

```

### <a name="description"></a>Açıklama

Bu hizmet, PPP paketi gönderme funcıton 'i ayarlar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ppp_ptr**: PPP denetim bloğu işaretçisi.
- **nx_ppp_packet_send**: PPP paketi gönderme yordamı.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı PPP durum isteği.
- NX_PTR_ERROR: (0x07) geçersiz PPP işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Set the PPP packet send function of PPP instance “my_ppp”.  */
status =  nx_ppp_packet_send_set(&my_ppp, nx_ppp_packet_send);

/* If status is NX_SUCCESS the PPP packet send function has set. */


```