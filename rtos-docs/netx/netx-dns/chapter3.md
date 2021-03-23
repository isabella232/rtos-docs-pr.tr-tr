---
title: Bölüm 3-Azure RTOS NetX DNS Istemci hizmetlerinin açıklaması
description: Bu bölüm, tüm Azure RTOS NetX DNS hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 18e059e79f9742eaaafffbf15b55b4b5063363f8
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826752"
---
# <a name="chapter-3---description-of-azure-rtos-netx-dns-client-services"></a>Bölüm 3-Azure RTOS NetX DNS Istemci hizmetlerinin açıklaması

Bu bölüm, tüm Azure RTOS NetX DNS hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.

Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_DISABLE_ERROR_CHECKING** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.

- **nx_dns_authority_zone_start_get**: *belirtilen ana bilgisayar adıyla ilişkili bir yetkili bölgesinin başlangıcına bakın*
- **nx_dns_cache_initialize**: *DNS önbelleği başlatın.*
- **nx_dns_cache_notify_clear**: *Cache Full NOTIFY işlevini temizleyin.*
- **nx_dns_cache_notify_set**: *önbellek tam bildirim işlevini ayarlayın.*
- **nx_dns_cname_get**: *giriş etki alanı adı diğer adı için kurallı etki alanı adını arayın*
- **nx_dns_create**: *DNS istemci örneği oluşturma*
- **nx_dns_delete**: *DNS istemci örneğini silme*
- **nx_dns_domain_name_server_get**: *giriş etki alanı bölgesi için yetkili ad sunucularını arayın*
- **nx_dns_domain_mail_exchange_get**: *belirtilen ana bilgisayar adının ilişkilendirildiği posta değişimine bakın.*
- **nx_dns_domain_service_get**: *belirtilen konak adıyla ilişkili hizmet (ler) i ara*
- **nx_dns_get_serverlist_size**: *DNS istemci sunucusu listesinin boyutunu Döndür*
- **nx_dns_info_by_name_get**: *dönüş IP adresi, giriş ana bilgisayar adında bağlantı noktası sorgulama*
- **nx_dns_ipv4_address_by_name_get**: *belirtilen ana bilgisayar adından IPv4 adresini ara*
- **nx_dns_host_by_address_get**: *belirtilen IP adresinden bir ana bilgisayar adı ara*
- **nx_dns_host_by_name_get**: *belirtilen ana bilgisayar adından IPv4 adresini ara*
- **nx_dns_host_text_get**: *giriş etki alanı adı için metin verilerini ara*
- **nx_dns_packet_pool_set**: *DNS istemcisi paket havuzunu ayarlama*
- **nx_dns_server_add**: *istemci listesine BELIRTILEN adreste bir DNS sunucusu ekleyin*
- **nx_dns_server_get**: *Istemci listesinde DNS sunucusunu döndürün*
- **nx_dns_server_remove**: *bir DNS sunucusunu istemci listesinden kaldırma*
- **nx_dns_server_remove_all**: *tüm DNS sunucularını istemci listesinden kaldır*

## <a name="nx_dns_authority_zone_start_get"></a>nx_dns_authority_zone_start_get

Giriş ana bilgisayarı için yetki bölgesinin başlangıcına bakın

### <a name="prototype"></a>Prototype

```c
UINT nx_dns_authority_zone_start_get (NX_DNS *dns_ptr, UCHAR *host_name, 
                                      VOID *record_buffer,
                                      UINT buffer_size, 
                                      UINT *record_count, 
                                      ULONG wait_option);

```

### <a name="description"></a>Açıklama

NX_DNS_ENABLE_EXTENDED_RR_TYPES tanımlanmışsa, bu hizmet giriş etki alanı adı için yetki bölgesinin başlangıcını almak üzere belirtilen etki alanı adına sahip SOA türünde bir sorgu gönderir. DNS Istemcisi, DNS sunucusu yanıtında döndürülen SOA kayıtlarını *record_buffer* bellek konumuna kopyalar. 
>[!NOTE]
> *Record_buffer* , verileri almak için 4 baytlık hizalı olmalıdır.

NetX DNS Istemcisinde, SOA kayıt türü NX_DNS_SOA_ENTRY, 7 4 baytlık parametreler olarak kaydedilir, toplam 28 bayt:

- **nx_dns_soa_host_mname_ptr**: Bu bölge için birincil veri kaynağı işaretçisi
- **nx_dns_soa_host_rname_ptr**: Bu bölgeden sorumlu olan posta kutusu işaretçisi
- **nx_dns_soa_serial**: bölge sürüm numarası
- **nx_dns_soa_refresh**: yenileme aralığı
- **nx_dns_soa_retry**: SOA sorgu yeniden denemeleri arasındaki Aralık
- **nx_dns_soa_expire**: SOA süresi dolduğu zaman süresi
- **nx_dns_soa_minmum**: SOA ana BILGISAYAR adı DNS yanıt iletilerinde en düşük TTL alanı

İki SOA kaydının depolanması aşağıda gösterilmiştir. Sabit uzunluklu verileri içeren SOA kayıtları, arabelleğin en üstünden başlayarak girilir. MNAME ve RNAME işaretçileri, arabelleğin altında depolanan değişken uzunluklu verileri (ana bilgisayar adları) işaret edin. Ek SOA kayıtları, ilk kayıttan sonra ("ek SOA kayıtları...") ve değişken uzunluklu verilerin en son girişin değişken uzunluk verilerinde ("ek SOA değişken uzunluğu verileri") depolandıktan sonra girilir:

![İki S O A kaydının depolanmasını temsil eden diyagram](media/image2.png)

Giriş *record_buffer* , sunucu YANıTıNDA tüm SOA verilerini tutamazsa, *record_buffer* sığacak kadar çok kayıt tutar ve arabellekteki kayıt sayısını döndürür.

* Record_count ' de döndürülen SOA kaydı sayısı ile *,* uygulama *record_buffer* verileri ayrıştırarak bölge yetkilisi ana bilgisayar adı dizelerinin başlangıcını ayıklayabilir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dns_ptr**: DNS istemcisi işaretçisi.  
- **host_name**: için SOA verileri almak için ana bilgisayar adı işaretçisi
- **record_buffer**: SOA verilerinin ayıklanacağı konum işaretçisi
- **Buffer_size**: SOA verilerini tutacak arabelleğin boyutu
- **record_count**: alınan SOA kaydı sayısına yönelik işaretçi
- **wait_option**: DNS sunucusu yanıtı alma seçeneğini bekle

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) SOA verileri başarıyla alındı
- **NX_DNS_NO_SERVER**: (0xA1) istemci sunucu listesi boş
- **NX_DNS_QUERY_FAILED**: (0xA3) GEÇERLI bir DNS yanıtı alınmadı
- NX_PTR_ERROR: (0x07) geçersiz IP veya DNS işaretçisi
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı
- NX_DNS_PARAM_ERROR: (0xA8) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek
```c
UCHAR                  record_buffer[50];
UINT                   record_count;   
NX_DNS_SOA_ENTRY       *nx_dns_soa_entry_ptr;

/* Request the start of authority zone(s) for the specified host.  */
status =  nx_dns_authority_zone_start_get(&client_dns, (UCHAR *)"www.my_example.com",
                                          record _buffer, sizeof(record_buffer), 
                                          &record_count, 500);

/* Check for DNS query error.  */
if (status != NX_SUCCESS)
{
    error_counter++;
}
else 
{
/* If status is NX_SUCCESS a DNS query was successfully completed and SOA data is returned in soa_buffer.  */

/* Set a local pointer to the SOA buffer. */
    nx_dns_soa_entry_ptr = (NX_DNS_SOA_ENTRY *) record_buffer;
    
    printf("------------------------------------------------------\n");
    printf("Test SOA: \n");
    printf("serial = %d\n", nx_dns_soa_entry_ptr -> nx_dns_soa_serial );
    printf("refresh = %d\n", nx_dns_soa_entry_ptr -> nx_dns_soa_refresh );
    printf("retry = %d\n", nx_dns_soa_entry_ptr -> nx_dns_soa_retry );
    printf("expire = %d\n", nx_dns_soa_entry_ptr -> nx_dns_soa_expire );
    printf("minmum = %d\n", nx_dns_soa_entry_ptr -> nx_dns_soa_minmum );
    
    if(nx_dns_soa_entry_ptr -> nx_dns_soa_host_mname_ptr)
    {
        printf("host mname = %s\n", 
               nx_dns_soa_entry_ptr -> nx_dns_soa_host_mname_ptr);
    }
    else
    {
        printf("host mame is not set\n");
    }
    
    if(nx_dns_soa_entry_ptr -> nx_dns_soa_host_rname_ptr)
    {
        printf("host rname = %s\n", 
               nx_dns_soa_entry_ptr -> nx_dns_soa_host_rname_ptr);
    }
    else
    {
     
        printf("host rname is not set\n");
    }
}

```

```Output
Test SOA:
serial = 2012111212
refresh = 7200
retry = 1800
expire = 1209600
minmum = 300
host mname = ns1.www.my_example.com
host rname = dns-admin.www.my_example.com
```


## <a name="nx_dns_cache_initialize"></a>nx_dns_cache_initialize

DNS önbelleğini başlatma

### <a name="prototype"></a>Prototype

```c
UINT nx_dns_cache_initialize(NX_DNS *dns_ptr,
                             VOID *cache_ptr, UINT cache_size);

```
### <a name="description"></a>Açıklama

Bu hizmet bir DNS önbelleği oluşturur ve başlatır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dns_ptr**: DNS Denetim bloğuna yönelik işaretçi.
- **cache_ptr**: DNS önbelleğine yönelik işaretçi.
- **cache_size**: DNS önbelleğinin boyutu (bayt).

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) DNS önbelleği başarıyla başlatıldı
- NX_DNS_ERROR: (0xA0) önbelleği 4 bayt hizalı değil.
- NX_DNS_PARAM_ERROR: (0xA8) geçersiz DNS KIMLIĞI.
- NX_PTR_ERROR: (0x07) geçersiz DNS işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek
```c
UCHAR          dns_cache [2048]; 

/* Initialize the DNS Cache.  */
status =  nx_dns_cache_initialize(&my_dns, dns_cache, 2048);
/* If status is NX_SUCCESS DNS Cache was successfully initialized.  */
```

## <a name="nx_dns_cache_notify_clear"></a>nx_dns_cache_notify_clear

DNS önbelleği tam bildirim işlevini temizle

### <a name="prototype"></a>Prototype

```c
UINT     nx_dns_cache_notify_clear(NX_DNS *dns_ptr);
```
### <a name="description"></a>Açıklama

Bu hizmet önbellek tam bildirim işlevini temizler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dns_ptr**: DNS Denetim bloğuna yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) DNS önbelleği bildirme başarıyla ayarlandı
- NX_DNS_PARAM_ERROR: (0xA8) geçersiz DNS KIMLIĞI.
- NX_PTR_ERROR: (0x07) geçersiz DNS işaretçisi.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Clear the DNS Cache full notify function.  */
status =  nx_dns_cache_notify_clear(&my_dns);

/* If status is NX_SUCCESS DNS Cache full notify function was successfully cleared. */
```

## <a name="nx_dns_cache_notify_set"></a>nx_dns_cache_notify_set

DNS önbelleği tam bildirim işlevini ayarla

### <a name="prototype"></a>Prototype

```c
UINT nx_dns_cache_notify_set(NX_DNS *dns_ptr, VOID (*cache_full_notify_cb)(NX_DNS *dns_ptr));
```

### <a name="description"></a>Açıklama

Bu hizmet önbellek tam bildirim işlevini ayarlar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dns_ptr**: DNS Denetim bloğuna yönelik işaretçi.
- **cache_full_notify_cb**: önbellek dolduğunda çağrılacak geri çağırma işlevi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) DNS önbelleği bildirme başarıyla ayarlandı
- NX_DNS_PARAM_ERROR: (0xA8) geçersiz DNS KIMLIĞI.
- NX_PTR_ERROR: (0x07) geçersiz DNS işaretçisi.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Set the DNS Cache full notify function.  */
status =  nx_dns_cache_notify_set(&my_dns, cache_full_notify_cb);

/* If status is NX_SUCCESS DNS Cache full notify function was successfully set.  */
 
```

## <a name="nx_dns_cname_get"></a>nx_dns_cname_get

Giriş ana bilgisayar adının kurallı adını arayın

### <a name="prototype"></a>Prototype
```c
UINT nx_dns_cname_get(NX_DNS *dns_ptr, UCHAR *host_name, 
                      UCHAR *record_buffer, UINT buffer_size, 
                      ULONG wait_option);
```

### <a name="description"></a>Açıklama

NX_DNS_ENABLE_EXTENDED_RR_TYPES *nx_dns. h* içinde tanımlanmışsa, bu hizmet kurallı etki alanı adını almak için belirtilen etki alanı ADıNA sahip CNAME türünde bir sorgu gönderir. DNS Istemcisi, DNS sunucusu yanıtında döndürülen CNAME dizesini *record_buffer* bellek konumuna kopyalar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dns_ptr**: DNS istemcisi işaretçisi.  
- **host_name**: için CNAME verilerinin alınacağı ana bilgisayar adı işaretçisi
- **record_buffer**: CNAME verilerinin ayıklanacağı konum işaretçisi
- **Buffer_size**: CNAME verilerini tutacak arabelleğin boyutu
- **wait_option**: DNS sunucusu yanıtı alma seçeneğini bekle

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) CNAME verileri başarıyla alındı
- **NX_DNS_NO_SERVER**: (0xA1) istemci sunucu listesi boş
- **NX_DNS_QUERY_FAILED**: (0xA3) GEÇERLI bir DNS yanıtı alınmadı
- NX_PTR_ERROR: (0x07) geçersiz IP veya DNS işaretçisi
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı
- NX_DNS_PARAM_ERROR: (0xA8) geçersiz işaretçi olmayan giriş

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
CHAR            record _buffer[50];

/* Request the canonical name for the specified host.  */
status =  nx_dns_cname_get(&client_dns, (UCHAR *)"www.my_example.com ", 
                            record_buffer, sizeof(record_buffer), 500);

/* Check for DNS query error.  */
if (status != NX_SUCCESS)
{
    error_counter++;
}
else     
{
/* If status is NX_SUCCESS a DNS query was successfully completed and the canonical host name is returned in record_buffer.  */

    printf("------------------------------------------------------\n");
    printf("Test CNAME: %s\n", record_buffer);
} 
```

```Output
Test CNAME: **my_example**.com
```

## <a name="nx_dns_create"></a>nx_dns_create

DNS Istemci örneği oluşturma

### <a name="prototype"></a>Prototype

```c
UINT nx_dns_create(NX_DNS *dns_ptr, NX_IP *ip_ptr, CHAR *domain_name);
```

### <a name="description"></a>Açıklama

Bu hizmet, önceden oluşturulan IP örneği için bir DNS Istemci örneği oluşturur.

>[!NOTE]
>Uygulama, DNS Istemcisi tarafından kullanılan paket havuzunun paket yükünün, en fazla 512 baytlık DNS iletisi, artı UDP, IP ve Ethernet üstbilgileri için yeterince büyük olduğundan emin olmalıdır. DNS Istemcisi kendi paket havuzunu oluşturursa, bu NX_DNS_PACKET_POOL_SIZE ve NX_DNS_PACKET_PAYLOAD tarafından tanımlanır. DNS Istemci uygulaması daha önce oluşturulmuş bir paket havuzu sağlamayı tercih ediyorsa, IPv4 DNS Istemcisinin yükü, IP üstbilgisi için en fazla DNS ve 20 bayt, UDP üst bilgisi için 8 bayt ve Ethernet üst bilgisi için 14 bayt 512 olmalıdır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dns_ptr**: DNS istemcisi işaretçisi.  
- **ip_ptr**: daha önce oluşturulan IP örneğine yönelik işaretçi.  
- **domain_name**: DNS örneği için etki alanı adı işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı DNS oluşturma
- **NX_DNS_ERROR**: (0xa0) DNS oluşturma hatası
- NX_PTR_ERROR: (0x07) geçersiz IP veya DNS işaretçisi
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Create a DNS Client instance.  */
status =  nx_dns_create(&my_dns, &my_ip, "My DNS");

/* If status is NX_SUCCESS a DNS Client instance was successfully
   created.  */
```
## <a name="nx_dns_delete"></a>nx_dns_delete

DNS Istemci örneğini silme

### <a name="prototype"></a>Prototype

```c
UINT     nx_dns_delete(NX_DNS *dns_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, önceden oluşturulmuş bir DNS Istemci örneğini siler ve kaynaklarını boşaltır. 
>[!NOTE]
> **NX_DNS_CLIENT_USER_CREATE_PACKET_POOL** TANıMLANDıYSA ve DNS istemcisine Kullanıcı tanımlı bir paket havuzu atanmışsa, artık GEREKMIYORSA, DNS istemcisi paket havuzunu silmek uygulamaya çalışır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dns_ptr**: daha önce oluşturulan DNS **istemci** örneğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı DNS istemcisi silme.
- NX_PTR_ERROR: (0x07) geçersiz IP veya DNS Istemcisi işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Delete a DNS Client instance.  */
status =  nx_dns_delete(&my_dns);

/* If status is NX_SUCCESS the DNS Client instance was successfully
   deleted.  */
```
## <a name="nx_dns_domain_name_server_get"></a>nx_dns_domain_name_server_get

Giriş etki alanı bölgesi için yetkili ad sunucularını arayın

### <a name="prototype"></a>Prototype

```c
UINT nx_dns_domain_name_server_get(NX_DNS *dns_ptr, UCHAR *host_name, 
                                   VOID *record_buffer, UINT buffer_size, 
                                   UINT *record_count, ULONG wait_option);
```

### <a name="description"></a>Açıklama

NX_DNS_ENABLE_EXTENDED_RR_TYPES tanımlanmışsa, bu hizmet giriş etki alanı adının ad sunucularını almak için belirtilen etki alanı adına sahip NS türünde bir sorgu gönderir. DNS Istemcisi, DNS sunucusu yanıtında döndürülen NS kayıtlarını *record_buffer* bellek konumuna kopyalar. 

>[!NOTE]
>*Record_buffer* , verileri almak için 4 baytlık hizalı olmalıdır.

NetX DNS Istemcisinde NS veri türü NX_DNS_NS_ENTRY, 2 4 baytlık parametreler olarak kaydedilir:

- **nx_dns_ns_ipv4_address**: sunucunun IPv4 adresini Adlandır
- **nx_dns_ns_hostname_ptr**: ad sunucusunun ana bilgisayar adı işaretçisi

Aşağıda gösterilen arabellek dört NX_DNS_NS_ENTRY kaydı içerir. Her girişte ana bilgisayar adı dizesinin işaretçisi, arabelleğin alt yarısında karşılık gelen ana bilgisayar adı dizesine işaret eder:

![Dört N X D N S N s giriş kaydı içeren arabelleğin diyagramı.](media/image3.png)

Giriş *record_buffer* , sunucu YANıTıNDA tüm NS verilerini tutamazsa, *record_buffer* sığacak kadar çok kayıt tutar ve arabellekteki kayıt sayısını döndürür.

* Record_count ' de döndürülen NS kayıtlarının sayısı ile *,* uygulama *RECORD_BUFFER* her kaydın IP adresini ve ana bilgisayar adını ayrıştırabilirler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dns_ptr**: DNS istemcisi işaretçisi.  
- **host_name**: NS verilerini almak için ana bilgisayar adı işaretçisi
- **record_buffer**: NS verilerinin ayıklanacağı konum işaretçisi
- **Buffer_size**: NS verilerini tutan arabelleğin boyutu
- **record_count**: alınan NS kaydı sayısının işaretçisi
- **wait_option**: DNS sunucusu yanıtı alma seçeneğini bekle

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) NS verileri başarıyla alındı
- **NX_DNS_NO_SERVER**: (0xA1) istemci sunucu listesi boş
- **NX_DNS_QUERY_FAILED**: (0xA3) GEÇERLI bir DNS yanıtı alınmadı
- NX_DNS_PARAM_ERROR: (0xA8) geçersiz DNS KIMLIĞI.
- NX_PTR_ERROR: (0x07) geçersiz IP veya DNS işaretçisi
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek
```c
#define RECORD_COUNT        10

ULONG                      record_buffer[50];
UINT                       record_count;          
NX_DNS_NS_ENTRY            *nx_dns_ns_entry_ptr[RECORD_COUNT];

/* Request the name server(s) for the specified host.  */
status =  nx_dns_domain_name_server_get(&client_dns, (UCHAR *)" www.my_example.com ",  
                                        record_buffer, sizeof(record_buffer),  
                                        &record_count, 500);

/* Check for DNS query error.  */
if (status != NX_SUCCESS)
{
    error_counter++;
}

else     
{
    /* If status is NX_SUCCESS a DNS query was successfully completed and NS data is returned in record_buffer.  */

    printf("------------------------------------------------------\n");
    printf("Test NS: ");
    printf("record_count = %d \n", record_count);      

    /* Get the name server.  */
    for(i =0; i< record_count; i++)
    {
        nx_dns_ns_entry_ptr[i] = (NX_DNS_NS_ENTRY *)(record_buffer + i * sizeof(NX_DNS_NS_ENTRY)); 

        printf("record %d: IP address: %d.%d.%d.%d\n", i, 
                nx_dns_ns_entry_ptr[i] -> nx_dns_ns_ipv4_address  >> 24,
                nx_dns_ns_entry_ptr[i] -> nx_dns_ns_ipv4_address >> 16 & 0xFF,                   
                nx_dns_ns_entry_ptr[i] -> nx_dns_ns_ipv4_address >> 8 & 0xFF,
                nx_dns_ns_entry_ptr[i] -> nx_dns_ns_ipv4_address & 0xFF);
        if(nx_dns_ns_entry_ptr[i] -> nx_dns_ns_hostname_ptr)
        {
            printf("hostname = %s\n", 
                    nx_dns_ns_entry_ptr[i] -> nx_dns_ns_hostname_ptr);
        }
        else
            printf("hostname is not set\n");
    }
}
```

```Output
Test NS: record_count = 4 
record 0: IP address: 192.2.2.10
hostname = ns2.www.my_example.com
record 1: IP address: 192.2.2.11
hostname = ns1.www.my_example.com
record 2: IP address: 192.2.2.12
hostname = ns3.www.my_example.com
record 3: IP address: 192.2.2.13
hostname = ns4.www.my_example.com
```

## <a name="nx_dns_domain_mail_exchange_get"></a>nx_dns_domain_mail_exchange_get

Giriş ana bilgisayar adı için posta alışverişinin aranacağı

### <a name="prototype"></a>Prototype
```c
UINT     nx_dns_domain_mail_exchange_get(NX_DNS *dns_ptr, UCHAR *host_name, 
                                        VOID *record_buffer,                                        
                                        UINT buffer_size, 
                                        UINT *record_count, 
                                        ULONG wait_option);

```

### <a name="description"></a>Açıklama

NX_DNS_ENABLE_EXTENDED_RR_TYPES tanımlanmışsa, bu hizmet giriş etki alanı adı için posta değişimini almak üzere belirtilen etki alanı adına sahip MX türünde bir sorgu gönderir. DNS Istemcisi, DNS sunucusu yanıtında döndürülen MX kayıtlarını *record_buffer* bellek konumuna kopyalar.

>[!NOTE]
>*Record_buffer* , verileri almak için 4 baytlık hizalı olmalıdır.

NetX DNS Istemcisinde posta değişim kayıt türü NX_DNS_MAIL_EXCHANGE_ENTRY, dört parametre olarak kaydedilir, bu da 12 baytı toplam olarak kaydeder:

- **nx_dns_mx_ipv4_address**: posta değişimi IPv4 adresi 4 bayt
- **nx_dns_mx_preference**: tercih 2 bayt
- **nx_dns_mx_reserved0**: ayrılmış 2 bayt
- **nx_dns_mx_hostname_ptr**: posta Exchange Server ana bilgisayar adı 4 bayt işaretçisi

Dört MX kaydı içeren bir arabellek aşağıda gösterilmiştir. Her kayıt, yukarıdaki listeden sabit uzunluklu verileri içerir. Posta Exchange Server ana bilgisayar adının işaretçisi, arabelleğin alt kısmındaki karşılık gelen ana bilgisayar adına işaret eder.

![Dört adet d X kaydı içeren arabelleği gösteren diyagram.](media/image4.png)

Giriş *record_buffer* , sunucu YANıTıNDA tüm MX verilerini tutamazsa, *record_buffer* sığacak kadar çok kayıt tutar ve arabellekteki kayıt sayısını döndürür.

**Record_count* ' de döndürülen MX kayıtlarının sayısı ile, uygulama, *record_buffer* her kaydın posta ana bilgisayar adı da dahil olmak üzere MX parametrelerini ayrıştırabilirler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dns_ptr**: DNS istemcisi işaretçisi.  
- **host_name**: MX verilerini almak için ana bilgisayar adı işaretçisi
- **record_buffer**: MX verilerinin ayıklanacağı konum işaretçisi
- **Buffer_size**: MX verilerini tutan arabelleğin boyutu
- **record_count**: alınan MX kaydı sayısının işaretçisi
- **wait_option**: DNS sunucusu yanıtı alma seçeneğini bekle

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) MX verileri başarıyla alındı
- **NX_DNS_NO_SERVER**: (0xA1) istemci sunucu listesi boş
- **NX_DNS_QUERY_FAILED**: (0xA3) GEÇERLI bir DNS yanıtı alınmadı
- NX_DNS_PARAM_ERROR: (0xA8) geçersiz DNS KIMLIĞI.
- NX_PTR_ERROR: (0x07) geçersiz IP veya DNS işaretçisi
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek
```c
#define           MAX_RECORD_COUNT 10

ULONG             record_buffer[50];
UINT              record_count;  
NX_DNS_MX_ENTRY  *nx_dns_mx_entry_ptr[MAX_RECORD_COUNT];        

/* Request the mail exchange data for the specified host.  */
status =  nx_dns_domain_mail_exchange_get(&client_dns, (UCHAR *)" www.my_example.com ", 
                                          record_buffer, sizeof(record_buffer),   
                                          &record_count, 500);

/* Check for DNS query error.  */
if (status != NX_SUCCESS)
{
    error_counter++;
}
       
else     
{
    /* If status is NX_SUCCESS a DNS query was successfully completed and MX data is returned in record_buffer.  */

    printf("------------------------------------------------------\n");
    printf("Test MX: ");
    printf("record_count = %d \n", record_count);      


    /* Get the mail exchange.  */
    for(i =0; i< record_count; i++)
    {
        nx_dns_mx_entry_ptr[i] = (NX_DNS_MX_ENTRY *)(record_buffer + i * sizeof(NX_DNS_MX_ENTRY));   

        printf("record %d: IP address: %d.%d.%d.%d\n", i, 
                nx_dns_mx_entry_ptr[i] -> nx_dns_mx_ipv4_address >> 24,
                nx_dns_mx_entry_ptr[i] -> nx_dns_mx_ipv4_address >> 16 & 0xFF,                   
                nx_dns_mx_entry_ptr[i] -> nx_dns_mx_ipv4_address >> 8 & 0xFF,
                nx_dns_mx_entry_ptr[i] -> nx_dns_mx_ipv4_address & 0xFF);

        printf("preference = %d \n ", nx_dns_mx_entry_ptr[i] -> nx_dns_mx_preference);

        if(nx_dns_mx_entry_ptr[i] -> nx_dns_mx_hostname_ptr)
            printf("hostname = %s\n", nx_dns_mx_entry_ptr[i] -> nx_dns_mx_hostname_ptr);
        else
            printf("hostname is not set\n");
    }
}
```

```Output
Test MX: record_count = 5 
record 0: IP address: 192.2.2.10
preference = 40 
hostname = alt3.aspmx.l.www.my_example.com
record 1: IP address: 192.2.2.11
preference = 50 
hostname = alt4.aspmx.l.www.my_example.com
record 2: IP address: 192.2.2.12
preference = 10 
hostname = aspmx.l.www.my_example.com
record 3: IP address: 192.2.2.13
preference = 20 
hostname = alt1.aspmx.l.www.my_example.com
record 4: IP address: 192.2.2.14
preference = 30 
hostname = alt2.aspmx.l.www.my_example.com
```


## <a name="nx_dns_domain_service_get"></a>nx_dns_domain_service_get

Giriş ana bilgisayar adı tarafından belirtilen hizmet (ler) i ara

### <a name="prototype"></a>Prototype

```c
UINT nx_dns_domain_service_get (NX_DNS *dns_ptr, UCHAR *host_name, 
                                VOID *record_buffer, UINT buffer_size, 
                                UINT *record_count, ULONG wait_option);
```

### <a name="description"></a>Açıklama

NX_DNS_ENABLE_EXTENDED_RR_TYPES tanımlanmışsa, bu hizmet, hizmet (ler) i ve belirtilen etki alanıyla ilişkili bağlantı noktası numaralarını aramak için belirtilen etki alanı adına sahip SRV türünde bir sorgu gönderir. DNS Istemcisi, DNS sunucusu yanıtında döndürülen SRV kayıtlarını *record_buffer* bellek konumuna kopyalar. 

>[!NOTE]
>*Record_buffer* , verileri almak için 4 baytlık hizalı olmalıdır.

NetX DNS Istemcisinde hizmet kayıt türü NX_DNS_SRV_ GIRIŞI, altı parametre olarak kaydedilir ve 16 baytlık bir toplam olur. Bu, değişken uzunlukta SRV verilerinin bellek verimli şekilde depolanmasını sağlar:

- **Sunucu IPv4 adresi**: nx_dns_srv_ipv4_address 4 bayt
- **Sunucu önceliği**: nx_dns_srv_priority 2 bayt
- **Sunucu ağırlığı**: nx_dns_srv_weight 2 bayt
- **Hizmet bağlantı noktası numarası**: nx_dns_srv_port_number 2 bayt
- **4 baytlık hizalama Için ayrılmıştır**: nx_dns_srv_reserved0 2 bayt
- **Sunucu ana bilgisayar adı işaretçisi**: * nx_dns_srv_hostname_ptr 4 bayt

Dört SRV kaydı, sağlanan arabellekte depolanır. Her bir NX_DNS_SRV_ENTRY kaydı, kayıt arabelleğinin alt kısmındaki karşılık gelen ana bilgisayar adı dizesine işaret eden *nx_dns_srv_hostname_ptr* bir işaretçi içerir:

![Sağlanan arabellekte depolanan dört S R V kaydı diyagramı.](media/image5.png)

Giriş *record_buffer* , sunucu YANıTıNDA tüm SRV verilerini tutamazsa, *record_buffer* sığacak kadar çok kayıt tutar ve arabellekteki kayıt sayısını döndürür.

**Record_count* ' de döndürülen SRV kayıtlarının sayısı ile, uygulama, *record_buffer* her kaydın sunucu ana bilgisayar adı da dahil olmak üzere SRV parametrelerini ayrıştırabilirler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dns_ptr**: DNS istemcisi işaretçisi.  
- **host_name**: SRV verilerini almak için ana bilgisayar adı işaretçisi
- **record_buffer**: SRV verilerinin ayıklanacağı konum işaretçisi
- **Buffer_size**: SRV verilerini tutan arabelleğin boyutu
- **record_count**: alınan SRV kaydı sayısına yönelik işaretçi
- **wait_option**: DNS sunucusu yanıtı alma seçeneğini bekle

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) SRV verileri başarıyla alındı
- **NX_DNS_NO_SERVER**: (0xA1) istemci sunucu listesi boş
- **NX_DNS_QUERY_FAILED**: (0xA3) GEÇERLI bir DNS yanıtı alınmadı
- NX_DNS_PARAM_ERROR: (0xA8) geçersiz DNS KIMLIĞI.
- NX_PTR_ERROR: (0x07) geçersiz IP veya DNS işaretçisi
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
#define MAX_RECORD_COUNT  10

UCHAR                  record_buffer[50];
UINT                   record_count;
NX_DNS_SRV_ENTRY       *nx_dns_srv_entry_ptr[MAX_RECORD_COUNT];

/* Request the service(s) provided by the specified host.  */
status =  nx_dns_domain_service_get(&client_dns, (UCHAR *)"www.my_example.com", 
                                    record_buffer, sizeof(record_buffer), 
                                    &record_count, 500);

/* Check for DNS query error.  */
if (status != NX_SUCCESS)
{
    error_counter++;
}

else     
{
    /* If status is NX_SUCCESS a DNS query was successfully completed and SRV data is returned in record_buffer.  */

    printf("------------------------------------------------------\n");
    printf("Test SRV: ");
    printf("record_count = %d \n", record_count);      

       
    /* Get the location of services.  */
    for(i =0; i< record_count; i++)
    {
        nx_dns_srv_entry_ptr[i] = (NX_DNS_SRV_ENTRY *)(record_buffer + i * sizeof(NX_DNS_SRV_ENTRY)); 

        printf("record %d: IP address: %d.%d.%d.%d\n", i, 
        nx_dns_srv_entry_ptr[i] -> nx_dns_srv_ipv4_address >> 24,
        nx_dns_srv_entry_ptr[i] -> nx_dns_srv_ipv4_address >> 16 & 0xFF,                   
        nx_dns_srv_entry_ptr[i] -> nx_dns_srv_ipv4_address >> 8 & 0xFF,
        nx_dns_srv_entry_ptr[i] -> nx_dns_srv_ipv4_address & 0xFF);

       printf("port number = %d\n", 
               nx_dns_srv_entry_ptr[i] -> nx_dns_srv_port_number );
               printf("priority = %d\n", nx_dns_srv_entry_ptr[i] -> nx_dns_srv_priority );
       printf("weight = %d\n", nx_dns_srv_entry_ptr[i] -> nx_dns_srv_weight );

       if(nx_dns_srv_entry_ptr[i] -> nx_dns_srv_hostname_ptr)
       {
            printf("hostname = %s\n", 
            nx_dns_srv_entry_ptr[i] -> nx_dns_srv_hostname_ptr);
        }
       else
            printf("hostname is not set\n");
    }
}
```

```Output
Test SRV: record_count = 3 
record 0: IP address: 192.2.2.10
port number = 5222
priority = 20
weight = 0
hostname = alt4.xmpp.l.www.my_example.com
record 1: IP address: 192.2.2.11
port number = 5222
priority = 5
weight = 0
hostname = xmpp.l.www.my_example.com
record 2: IP address: 192.2.2.12
port number = 5222
priority = 20
weight = 0
hostname = alt1.xmpp.l.www.my_example.com
```

## <a name="nx_dns_get_serverlist_size"></a>nx_dns_get_serverlist_size

DNS Istemcisinin sunucu listesinin boyutunu döndürür

### <a name="prototype"></a>Prototype

```c
UINT nx_dns_get_serverlist_size (NX_DNS *dns_ptr, UINT *size);
```

### <a name="description"></a>Açıklama

Bu hizmet, Istemci listesindeki geçerli DNS sunucularının sayısını döndürür.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dns_ptr**: DNS denetim bloğu işaretçisi  
- **Boyut**: listedeki sunucu sayısını döndürür

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) DNS sunucusu liste boyutu başarıyla döndürüldü
- NX_PTR_ERROR: (0x07) geçersiz IP veya DNS işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
UINT my_listsize;

/* Get the number of non null DNS Servers in the Client list.  */
status =  nx_dns_get_serverlist_size (&my_dns, 5, &my_listsize);

/* If status is NX_SUCCESS the size of the DNS Server list was successfully
   returned.  */
```

## <a name="nx_dns_info_by_name_get"></a>nx_dns_info_by_name_get

IP adresini ve DNS sunucusunun bağlantı noktasını ana bilgisayar adına göre döndür

### <a name="prototype"></a>Prototype

```c
UINT nx_dns_info_by_name_get(NX_DNS *dns_ptr, UCHAR *host_name, 
                             ULONG *host_address_ptr,  
                             USHORT *host_port_ptr, ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, DNS sorgusunun giriş ana bilgisayar adına göre sunucu IP 'sini ve bağlantı noktasını (hizmet kaydı) döndürür. Bir hizmet kaydı bulunamazsa, bu yordam giriş adresi İşaretçisinde sıfır bir IP adresi döndürür ve bir hatayı bildirmek için sıfır olmayan bir hata durumu döndürür.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dns_ptr**: DNS denetim bloğu işaretçisi  
- **host_name**: Ana bilgisayar adı arabelleği işaretçisi
- **host_address_ptr**: döndürülecek adrese yönelik işaretçi
- **host_port_ptr**: DNS yanıtı Için wait_option bekle seçeneğini döndürecek bağlantı noktası işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) DNS sunucusu kaydı başarıyla döndürüldü
- **NX_DNS_NO_SERVER**: (0xA1) ana bilgisayar adına sorgu göndermek için istemciyle bırlıkte kayıtlı DNS sunucusu yok
- **NX_DNS_QUERY_FAILED**: (0xA3) DNS sorgusu başarısız oldu; giriş ana bilgisayar adı için Istemci listesindeki herhangi bir DNS sunucusundan yanıt yok veya hizmet kaydı yok.
- NX_PTR_ERROR: (0x07) geçersiz IP veya DNS işaretçisi
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek
```c
ULONG         ip_address;
USHORT         port;

/* Attempt to resolve the IP address and ports for this host name.  */
status =  nx_dns_info_by_name_get(&my_dns, “www.abc1234.com”, &ip_address, &port, 200);

/* If status is NX_SUCCESS the DNS query was successful and the IP address and
   report for the hostname are returned.  */
```

## <a name="nx_dns_ipv4_address_by_name_get"></a>nx_dns_ipv4_address_by_name_get

Giriş ana bilgisayar adı için IPv4 adresini arayın

### <a name="prototype"></a>Prototype

```c
UINT nx_dns_ipv4_address_by_name_get (NX_DNS *dns_ptr, 
                                       UCHAR *host_name_ptr, VOID *buffer, 
                                       UINT buffer_size, 
                                       UINT *record_count,
                                       ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, giriş ana bilgisayar adı için IP adreslerini almak üzere belirtilen ana bilgisayar adına sahip A türünde bir sorgu gönderir. DNS Istemcisi, IPv4 adresini DNS sunucusu yanıtında döndürülen bir kayıt (lar) dan *record_buffer* bellek konumuna kopyalar. 

>[!NOTE]
>*Record_buffer* , verileri almak için 4 baytlık hizalı olmalıdır.

Aşağıda gösterildiği gibi, 4 baytlık hizalanmış arabellekte birden çok IPv4 adresi depolanır:

![4 bayt hizalı arabellekte depolanan birden fazla ı P v 4 adresinin diyagramı.](media/image6.png)

Sağlanan arabellek tüm IP adresi verilerini tutamıyorsa, kalan kayıtlar *record_buffer* depolanmaz. Bu, uygulamanın sunucu yanıtında kullanılabilir IP adresi verilerinin bir kısmını veya tamamını almasını sağlar.

**Record_count* döndürülen kayıt sayısı ile uygulama, IPv4 adresi verilerini *record_buffer* ayrıştırabilirler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dns_ptr**: DNS istemcisi işaretçisi.  
- **host_name_ptr**: IPv4 verilerinin içine ayıklanacağı konuma IPv4 adresi arabellek işaretçisi almak için ana bilgisayar adı işaretçisi
- **Buffer_size**: IPv4 verilerini tutacak arabelleğin boyutu
- **wait_option**: DNS sunucusu yanıtı alma seçeneğini bekle

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) IPv4 verileri başarıyla alındı
- **NX_DNS_NO_SERVER**: (0xA1) istemci sunucu listesi boş
- **NX_DNS_QUERY_FAILED**: (0xA3) GEÇERLI bir DNS yanıtı alınmadı
- NX_DNS_PARAM_ERROR: (0xA8) geçersiz giriş parametresi.
- NX_PTR_ERROR: (0x07) geçersiz IP veya DNS işaretçisi
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
#define MAX_RECORD_COUNT  20

ULONG           record_buffer[50];
UINT            record_count;
ULONG           *ipv4_address_ptr[MAX_RECORD_COUNT];

/* Request the IPv4 address for the specified host.  */
status =  nx_dns_ipv4_address_by_name_get(&client_dns, 
                                          (UCHAR *)"www.my_example.com",  
                                           record_buffer,                  
                                           sizeof(record_buffer),&record_count,                
                                           500);

        /* Check for DNS query error.  */
if (status != NX_SUCCESS)
{
        error_counter++;
}    
else     
{
    /* If status is NX_SUCCESS a DNS query was successfully completed the IPv4 address(es) is returned in record_buffer.  */
    printf("------------------------------------------------------\n");
    printf("Test A: ");
    printf("record_count = %d \n", record_count);      


    /* Get the IPv4 addresses of host.  */
    for(i =0; i< record_count; i++)
    {
        ipv4_address_ptr[i] = (ULONG *)(record_buffer + i * sizeof(ULONG)); 
        printf("record %d: IP address: %d.%d.%d.%d\n", i, 
                *ipv4_address_ptr[i] >> 24,
                *ipv4_address_ptr[i] >> 16 & 0xFF,                   
                *ipv4_address_ptr[i] >> 8 & 0xFF,
                *ipv4_address_ptr[i] & 0xFF);
    }
}
```

```Output
------------------------------------------------------
Test A: record_count = 5 
record 0: IP address: 192.2.2.10
record 1: IP address: 192.2.2.11
record 2: IP address: 192.2.2.12
record 3: IP address: 192.2.2.13
record 4: IP address: 192.2.2.14
```

## <a name="nx_dns_host_by_address_get"></a>nx_dns_host_by_address_get

Bir IP adresinden ana bilgisayar adı ara

### <a name="prototype"></a>Prototype

```c
UINT nx_dns_host_by_address_get(NX_DNS *dns_ptr, ULONG ip_address, 
                                ULONG *host_name_ptr, 
                                ULONG max_host_name_size, 
                                ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, uygulama tarafından daha önce belirtilen bir veya daha fazla DNS sunucusundan sağlanan IP adresinin ad çözümlemesini ister. Başarılı olursa, NULL ile sonlandırılmış ana bilgisayar adı *host_name_ptr* tarafından belirtilen dizede döndürülür.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dns_ptr**: daha önce oluşturulan DNS örneğine yönelik işaretçi.
- **ip_address**: bir ada çözülecek IP adresi
- **host_name_ptr**: konak adı için hedef alan işaretçisi
- **max_host_name_size**: konak adı için hedef alanın boyutu
- **wait_option**: hizmetin her bir DNS sorgusu ve sorgu yeniden denendikten sonra bir DNS sunucusu yanıtı için Zamanlayıcı işaretlerini ne kadar bekleyeceğini tanımlar, bekleme seçenekleri aşağıdaki gibi tanımlanır:
    - **zaman aşımı değeri**: (0x00000001-0xfffffffe) sayısal bir değer (1-0XFFFFFFFE) SEÇILIRSE, DNS çözümlemesi beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.
    - **TX_WAIT_FOREVER**: (0xffffffff) TX_WAIT_FOREVER seçilmesi çağıran iş PARÇACıĞıNıN bir DNS sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı DNS çözümlemesi  
- **NX_DNS_TIMEOUT**: (0xA2) DNS mutex 'i alma sırasında zaman aşımına uğradı
- **NX_DNS_NO_SERVER**: (0xA1) DNS sunucusu adresi belirtilmedi
- **NX_DNS_QUERY_FAILED**: (0xA3) sorguya yanıt almadı
- **NX_DNS_BAD_ADDRESS_ERROR**: (0xa4) null giriş adresi
- **NX_DNS_INVALID_ADDRESS_TYPE**: (0Xb2) geçersiz adres türüne (örneğin, IPv6) dizin noktaları
- **NX_DNS_PARAM_ERROR**: (0Xa8) geçersiz işaretçi girişi
- NX_PTR_ERROR: (0x07) geçersiz işaretçi girişi
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
#define BUFFER_SIZE   200

UCHAR   resolved_name[200];

/* Get the name associated with IP address 192.2.2.10.  */
status =  nx_dns_host_by_address_get(&my_dns, IP_ADDRESS(192.2.2.10),
                                     &resolved_name[0], BUFFER_SIZE, 450);

/* If status is NX_SUCCESS the name associated with the IP address
   can be found in the resolved_name variable.  */

```

## <a name="nx_dns_host_by_name_get"></a>nx_dns_host_by_name_get

Ana bilgisayar adından bir IP adresi ara

### <a name="prototype"></a>Prototype

```c
UINT nx_dns_host_by_name_get(NX_DNS *dns_ptr, UCHAR *host_name, 
                             ULONG *host_address_ptr, ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, uygulama tarafından daha önce belirtilen bir veya daha fazla DNS sunucusundan *host_name* tarafından işaret edilen ad çözümlemesini ister. Başarılı olursa, ilişkili IP adresi *host_address_ptr* tarafından işaret edilen hedefte döndürülür.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dns_ptr**: daha önce oluşturulan DNS örneğine yönelik işaretçi.
- **host_name**: Ana bilgisayar adı işaretçisi
- **host_address_ptr**: DNS ana bilgisayar IP adresi işaretçisi
- **wait_option**: hizmetin DNS çözümlemesi için bekleyeceği süreyi tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
    - **zaman aşımı değeri**: (0x00000001-0xfffffffe) sayısal değer (1-0XFFFFFFFE) SEÇILDIĞINDE, DNS çözümlemesi beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.
    - **TX_WAIT_FOREVER**: (0xffffffff) TX_WAIT_FOREVER seçilmesi çağıran iş PARÇACıĞıNıN bir DNS sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı DNS çözümlemesi.
- **NX_DNS_NO_SERVER**: (0xA1) DNS sunucusu adresi belirtilmedi
- **NX_DNS_QUERY_FAILED**: (0xA3) sorguya yanıt almadı
- NX_DNS_PARAM_ERROR: (0xA8) geçersiz işaretçi girişi
- NX_PTR_ERROR: (0x07) geçersiz işaretçi girişi
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek
```c
ULONG ip_address;

    /* Get the IP address for the name “www.my_example.com”.  */
    status =  nx_dns_host_by_name_get(&my_dns, “www.my_example.com”, &ip_address, 4000);

    /* Check for DNS query error.  */
    if (status != NX_SUCCESS)
    {
        error_counter++;
    }

    else     
    {

    /* If status is NX_SUCCESS the IP address for “www.my_example.com” can be found in the “ip_address” variable.  */
        
        printf("------------------------------------------------------\n");
        printf("Test A: \n");
        printf("IP address: %d.%d.%d.%d\n",
                host_ip_address >> 24,
                host_ip_address >> 16 & 0xFF,                   
                host_ip_address >> 8 & 0xFF,
                host_ip_address & 0xFF);
    }
```

```Output
Test A: 
IP address: 192.2.2.10
```

## <a name="nx_dns_host_text_get"></a>nx_dns_host_text_get

Giriş etki alanı adı için metin dizesini arayın

### <a name="prototype"></a>Prototype

```c
UINT nx_dns_host_text_get(NX_DNS *dns_ptr, UCHAR *host_name, 
                          UCHAR *record_buffer, 
                          UINT buffer_size, ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, rastgele dize verileri elde etmek için belirtilen etki alanı adı ve arabellekle TXT türünde bir sorgu gönderir.

DNS Istemcisi, DNS sunucusu yanıtındaki TXT kaydındaki metin dizesini *record_buffer* bellek konumuna kopyalar. 

>[!NOTE]
>*Record_buffer* verileri almak için 4 baytlık hizalı olması gerekmez.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dns_ptr**: DNS istemcisi işaretçisi.  
- **host_name**: arama yapılacak ana bilgisayarın adı işaretçisi
- **record_buffer**: txt verilerinin ayıklanacağı konum işaretçisi
- **Buffer_size**: txt verilerini tutan arabelleğin boyutu
- **wait_option**: DNS sunucusu yanıtı alma seçeneğini bekle

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı bir txt dizesi alındı
- **NX_DNS_NO_SERVER**: (0xA1) istemci sunucu listesi boş
- **NX_DNS_QUERY_FAILED**: (0xA3) GEÇERLI bir DNS yanıtı alınmadı
- NX_PTR_ERROR: (0x07) geçersiz işaretçi girişi
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı
- NX_DNS_PARAM_ERROR: (0xA8) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
CHAR            record_buffer[50];

/* Request the text string for the specified host.  */
status =  nx_dns_host_text_get(&client_dns, (UCHAR *)"www.my_example.com", 
                                record_buffer, 
                                sizeof(record_buffer), 500);


/* Check for DNS query error.  */
if (status != NX_SUCCESS)
{
     error_counter++;
}
else     
{
/* If status is NX_SUCCESS a DNS query was successfully completed and the text string is returned in record_buffer.  */
 
     printf("------------------------------------------------------\n");
     printf("Test TXT:\n %s\n", record_buffer);
} 
```

```Output
Test TXT: 
v=spf1 include:_www.my_example.com ip4:192.2.2.10/31 ip4:192.2.2.11/31 ~all
```

## <a name="nx_dns_packet_pool_set"></a>nx_dns_packet_pool_set

DNS Istemcisi paket havuzunu ayarlama

### <a name="prototype"></a>Prototype

```c
UINT nx_dns_packet_pool_set(NX_DNS *dns_ptr, NX_PACKET_POOL *pool_ptr);
```
### <a name="description"></a>Açıklama

Bu hizmet, daha önce oluşturulmuş bir paket havuzunu DNS **istemcisi** paket havuzu olarak ayarlar. DNS Istemcisi, DNS sorguları göndermek için bu paket havuzunu kullanır, bu nedenle paket yükü Ethernet çerçevesini, IP ve UDP üst bilgilerini içeren ve *nx_dns. h* içinde tanımlanan NX_DNS_PACKET_PAYLOAD_UNALIGNED daha az olmamalıdır.
 
>[!NOTE]
>DNS Istemcisi silindiğinde, paket havuzu onunla silinmez ve artık ihtiyaç duyulmuyorsa, paket havuzunu silmek uygulamanın sorumluluğundadır.

>[!NOTE]
>Bu hizmet yalnızca yapılandırma seçeneği NX_DNS_CLIENT_USER_CREATE_PACKET_POOL *nx_dns. h* içinde tanımlanmışsa kullanılabilir

### <a name="input-parameters"></a>Giriş Parametreleri

- **dns_ptr**: daha önce oluşturulan DNS **istemci** örneğine yönelik işaretçi.
- **pool_ptr**: daha önce oluşturulmuş olan paket havuzuna yönelik işaretçi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı tamamlama.
- Bu seçenek için **NX_NOT_ENABLED**: (0x14) istemci yapılandırılmadı
- NX_PTR_ERROR: (0x07) geçersiz IP veya DNS **istemcisi** işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek
```c
NX_DNS             my_dns;
NX_PACKET_POOL     client_pool;
NX_IP             *ip_ptr;


/* Create the DNS Client.  */
status =  nx_dns_create(&my_dns, ip_ptr, “My DNS Client”);

/* Create a packet pool for the DNS Client.  */
status =  nx_packet_pool_create(&client_pool, "DNS Client Packet Pool", 
                                 NX_DNS_PACKET_PAYLOAD, free_mem_pointer, 
                                 NX_DNS_PACKET_POOL_SIZE);

/* Set the DNS Client packet pool.  */
status =  nx_dns_packet_pool_set(&my_dns, &client_pool);

/* If status is NX_SUCCESS the DNS Client packet pool was successfully set.  */
```

## <a name="nx_dns_server_add"></a>nx_dns_server_add

DNS sunucusu IP adresi ekle

### <a name="prototype"></a>Prototype

```c
UINT nx_dns_server_add(NX_DNS *dns_ptr, ULONG server_address);
```

### <a name="description"></a>Açıklama

Bu hizmet, sunucu listesine bir IPv4 DNS sunucusu ekler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dns_ptr**: DNS Denetim bloğuna yönelik işaretçi.  
- **server_address**: DNS sunucusunun IP adresi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) sunucu başarıyla eklendi
- **NX_DNS_DUPLICATE_ENTRY** veya **NX_NO_MORE_ENTRIES**: (0x17) daha fazla DNS sunucusu izin verilmiyor (liste dolu)
- **NX_DNS_PARAM_ERROR**: (0Xa8) geçersiz işaretçi girişi
- NX_PTR_ERROR: (0x07) geçersiz işaretçi girişi
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı
- NX_DNS_BAD_ADDRESS_ERROR: (0xA4) null sunucu adresi girişi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Add a DNS Server at IP address 202.2.2.13.  */
status =  nx_dns_server_add(&my_dns, IP_ADDRESS(202,2,2,13));

/* If status is NX_SUCCESS a DNS Server was successfully added.  */
```

## <a name="nx_dns_server_get"></a>nx_dns_server_get

Istemci listesinden bir IPv4 DNS sunucusu döndürme

### <a name="prototype"></a>Prototype

```c
UINT nx_dns_server_get(NX_DNS *dns_ptr, UINT index, 
                       ULONG *dns_server_address);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen dizindeki sunucu listesinden IPv4 DNS sunucusu adresini döndürür. Dizinin sıfır tabanlı olduğunu unutmayın. Giriş dizini DNS Istemci listesinin boyutunu aşarsa bir hata döndürülür. *Nx_dns_get_serverlist_size* hizmeti Ilk olarak ISTEMCI listesindeki DNS sunucularının sayısını elde edebilir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dns_ptr**: DNS denetim bloğu işaretçisi  
- **Dizin**: DNS istemcisinin sunucu listesini dizine ekleyin
- **dns_server_address**: DNS sunucusunun IP adresi işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı sunucu döndürüldü
- **NX_DNS_SERVER_NOT_FOUND**: (0xA9) boş yuvaya yönelik dizin noktaları
- **NX_DNS_BAD_ADDRESS_ERROR**: (0xa4) null adrese yönelik dizin noktaları
- **NX_DNS_PARAM_ERROR**: (0Xa8) dizin, listenin boyutunu aşıyor
- NX_PTR_ERROR: (0x07) geçersiz IP veya DNS işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
ULONG     my_server_address;

/* Get the DNS Server at index 5 (zero based) into the Client list.  */
status =  nx_dns_server_get(&my_dns, 5, &my_server_addres);

/* If status is NX_SUCCESS a DNS Server was successfully
   returned.  */
```

## <a name="nx_dns_server_remove"></a>nx_dns_server_remove

Bir IPv4 DNS sunucusunu Istemci listesinden kaldır

### <a name="prototype"></a>Prototype

```c
UINT nx_dns_server_remove(NX_DNS *dns_ptr, ULONG server_address);
```

### <a name="description"></a>Açıklama

Bu hizmet, bir IPv4 DNS sunucusunu Istemci listesinden kaldırır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dns_ptr**: DNS Denetim bloğuna yönelik işaretçi.
- **server_address**: DNS sunucusunun IP adresi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) DNS sunucusu başarıyla kaldırıldı
- **NX_DNS_SERVER_NOT_FOUND**: (0xA9) sunucu istemci listesinde değil
- **NX_DNS_BAD_ADDRESS_ERROR**: (0xa4) null sunucu adresi girişi
- NX_PTR_ERROR: (0x07) geçersiz IP veya DNS işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Remove the DNS Server at IP address is 202.2.2.13.  */
status =  nx_dns_server_remove(&my_dns, IP_ADDRESS(202,2,2,13));

/* If status is NX_SUCCESS a DNS Server was successfully
   removed.  */
```

## <a name="nx_dns_server_remove_all"></a>nx_dns_server_remove_all

Tüm DNS sunucularını Istemci listesinden kaldır

### <a name="prototype"></a>Prototype

```c
UINT nx_dns_server_remove_all(NX_DNS *dns_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, tüm DNS sunucularını Istemci listesinden kaldırır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dns_ptr**: DNS Denetim bloğuna yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) DNS sunucuları başarıyla kaldırıldı
- **NX_DNS_ERROR**: (0xa0) koruma mutex 'i alınamıyor
- NX_PTR_ERROR: (0x07) geçersiz IP veya DNS işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c

/* Remove all DNS Servers from the Client list.  */
status =  nx_dns_server_remove_all(&my_dns);

/* If status is NX_SUCCESS all DNS Servers were successfully removed.  */
```