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
# <a name="chapter-3---description-of-azure-rtos-netx-dns-client-services"></a><span data-ttu-id="d0262-103">Bölüm 3-Azure RTOS NetX DNS Istemci hizmetlerinin açıklaması</span><span class="sxs-lookup"><span data-stu-id="d0262-103">Chapter 3 - Description of Azure RTOS NetX DNS Client Services</span></span>

<span data-ttu-id="d0262-104">Bu bölüm, tüm Azure RTOS NetX DNS hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="d0262-104">This chapter contains a description of all Azure RTOS NetX DNS services (listed below) in alphabetic order.</span></span>

<span data-ttu-id="d0262-105">Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_DISABLE_ERROR_CHECKING** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="d0262-105">In the “Return Values” section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

- <span data-ttu-id="d0262-106">**nx_dns_authority_zone_start_get**: *belirtilen ana bilgisayar adıyla ilişkili bir yetkili bölgesinin başlangıcına bakın*</span><span class="sxs-lookup"><span data-stu-id="d0262-106">**nx_dns_authority_zone_start_get**: *Look up the start of a zone of authority associated with the specified host name*</span></span>
- <span data-ttu-id="d0262-107">**nx_dns_cache_initialize**: *DNS önbelleği başlatın.*</span><span class="sxs-lookup"><span data-stu-id="d0262-107">**nx_dns_cache_initialize**: *Initialize a DNS Cache.*</span></span>
- <span data-ttu-id="d0262-108">**nx_dns_cache_notify_clear**: *Cache Full NOTIFY işlevini temizleyin.*</span><span class="sxs-lookup"><span data-stu-id="d0262-108">**nx_dns_cache_notify_clear**: *Clear the cache full notify function.*</span></span>
- <span data-ttu-id="d0262-109">**nx_dns_cache_notify_set**: *önbellek tam bildirim işlevini ayarlayın.*</span><span class="sxs-lookup"><span data-stu-id="d0262-109">**nx_dns_cache_notify_set**: *Set the cache full notify function.*</span></span>
- <span data-ttu-id="d0262-110">**nx_dns_cname_get**: *giriş etki alanı adı diğer adı için kurallı etki alanı adını arayın*</span><span class="sxs-lookup"><span data-stu-id="d0262-110">**nx_dns_cname_get**: *Look up the canonical domain name for the input domain name alias*</span></span>
- <span data-ttu-id="d0262-111">**nx_dns_create**: *DNS istemci örneği oluşturma*</span><span class="sxs-lookup"><span data-stu-id="d0262-111">**nx_dns_create**: *Create a DNS Client instance*</span></span>
- <span data-ttu-id="d0262-112">**nx_dns_delete**: *DNS istemci örneğini silme*</span><span class="sxs-lookup"><span data-stu-id="d0262-112">**nx_dns_delete**: *Delete a DNS Client instance*</span></span>
- <span data-ttu-id="d0262-113">**nx_dns_domain_name_server_get**: *giriş etki alanı bölgesi için yetkili ad sunucularını arayın*</span><span class="sxs-lookup"><span data-stu-id="d0262-113">**nx_dns_domain_name_server_get**: *Look up the authoritative name servers for the input domain zone*</span></span>
- <span data-ttu-id="d0262-114">**nx_dns_domain_mail_exchange_get**: *belirtilen ana bilgisayar adının ilişkilendirildiği posta değişimine bakın.*</span><span class="sxs-lookup"><span data-stu-id="d0262-114">**nx_dns_domain_mail_exchange_get**: *Look up the mail exchange associated the specified host name.*</span></span>
- <span data-ttu-id="d0262-115">**nx_dns_domain_service_get**: *belirtilen konak adıyla ilişkili hizmet (ler) i ara*</span><span class="sxs-lookup"><span data-stu-id="d0262-115">**nx_dns_domain_service_get**: *Look up the service(s) associated with the specified host name*</span></span>
- <span data-ttu-id="d0262-116">**nx_dns_get_serverlist_size**: *DNS istemci sunucusu listesinin boyutunu Döndür*</span><span class="sxs-lookup"><span data-stu-id="d0262-116">**nx_dns_get_serverlist_size**: *Return the size of the DNS Client server list*</span></span>
- <span data-ttu-id="d0262-117">**nx_dns_info_by_name_get**: *dönüş IP adresi, giriş ana bilgisayar adında bağlantı noktası sorgulama*</span><span class="sxs-lookup"><span data-stu-id="d0262-117">**nx_dns_info_by_name_get**: *Return IP address, port querying on input host name*</span></span>
- <span data-ttu-id="d0262-118">**nx_dns_ipv4_address_by_name_get**: *belirtilen ana bilgisayar adından IPv4 adresini ara*</span><span class="sxs-lookup"><span data-stu-id="d0262-118">**nx_dns_ipv4_address_by_name_get**: *Look up the IPv4 address from the specified host name*</span></span>
- <span data-ttu-id="d0262-119">**nx_dns_host_by_address_get**: *belirtilen IP adresinden bir ana bilgisayar adı ara*</span><span class="sxs-lookup"><span data-stu-id="d0262-119">**nx_dns_host_by_address_get**: *Look up a host name from a specified IP address*</span></span>
- <span data-ttu-id="d0262-120">**nx_dns_host_by_name_get**: *belirtilen ana bilgisayar adından IPv4 adresini ara*</span><span class="sxs-lookup"><span data-stu-id="d0262-120">**nx_dns_host_by_name_get**: *Look up the IPv4 address from the specified host name*</span></span>
- <span data-ttu-id="d0262-121">**nx_dns_host_text_get**: *giriş etki alanı adı için metin verilerini ara*</span><span class="sxs-lookup"><span data-stu-id="d0262-121">**nx_dns_host_text_get**: *Look up the text data for the input domain name*</span></span>
- <span data-ttu-id="d0262-122">**nx_dns_packet_pool_set**: *DNS istemcisi paket havuzunu ayarlama*</span><span class="sxs-lookup"><span data-stu-id="d0262-122">**nx_dns_packet_pool_set**: *Set the DNS Client packet pool*</span></span>
- <span data-ttu-id="d0262-123">**nx_dns_server_add**: *istemci listesine BELIRTILEN adreste bir DNS sunucusu ekleyin*</span><span class="sxs-lookup"><span data-stu-id="d0262-123">**nx_dns_server_add**: *Add a DNS Server at the specified address to the Client list*</span></span>
- <span data-ttu-id="d0262-124">**nx_dns_server_get**: *Istemci listesinde DNS sunucusunu döndürün*</span><span class="sxs-lookup"><span data-stu-id="d0262-124">**nx_dns_server_get**: *Return the DNS Server in the Client list*</span></span>
- <span data-ttu-id="d0262-125">**nx_dns_server_remove**: *bir DNS sunucusunu istemci listesinden kaldırma*</span><span class="sxs-lookup"><span data-stu-id="d0262-125">**nx_dns_server_remove**: *Remove a DNS Server from the Client list*</span></span>
- <span data-ttu-id="d0262-126">**nx_dns_server_remove_all**: *tüm DNS sunucularını istemci listesinden kaldır*</span><span class="sxs-lookup"><span data-stu-id="d0262-126">**nx_dns_server_remove_all**: *Remove all DNS Servers from the Client list*</span></span>

## <a name="nx_dns_authority_zone_start_get"></a><span data-ttu-id="d0262-127">nx_dns_authority_zone_start_get</span><span class="sxs-lookup"><span data-stu-id="d0262-127">nx_dns_authority_zone_start_get</span></span>

<span data-ttu-id="d0262-128">Giriş ana bilgisayarı için yetki bölgesinin başlangıcına bakın</span><span class="sxs-lookup"><span data-stu-id="d0262-128">Look up the start of the zone of authority for the input host</span></span>

### <a name="prototype"></a><span data-ttu-id="d0262-129">Prototype</span><span class="sxs-lookup"><span data-stu-id="d0262-129">Prototype</span></span>

```c
UINT nx_dns_authority_zone_start_get (NX_DNS *dns_ptr, UCHAR *host_name, 
                                      VOID *record_buffer,
                                      UINT buffer_size, 
                                      UINT *record_count, 
                                      ULONG wait_option);

```

### <a name="description"></a><span data-ttu-id="d0262-130">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d0262-130">Description</span></span>

<span data-ttu-id="d0262-131">NX_DNS_ENABLE_EXTENDED_RR_TYPES tanımlanmışsa, bu hizmet giriş etki alanı adı için yetki bölgesinin başlangıcını almak üzere belirtilen etki alanı adına sahip SOA türünde bir sorgu gönderir.</span><span class="sxs-lookup"><span data-stu-id="d0262-131">If NX_DNS_ENABLE_EXTENDED_RR_TYPES is defined, this service sends a query of type SOA with the specified domain name to obtain the start of the zone of authority for the input domain name.</span></span> <span data-ttu-id="d0262-132">DNS Istemcisi, DNS sunucusu yanıtında döndürülen SOA kayıtlarını *record_buffer* bellek konumuna kopyalar.</span><span class="sxs-lookup"><span data-stu-id="d0262-132">The DNS Client copies the SOA record(s) returned in the DNS Server response into the *record_buffer* memory location.</span></span> 
>[!NOTE]
> <span data-ttu-id="d0262-133">*Record_buffer* , verileri almak için 4 baytlık hizalı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d0262-133">The *record_buffer* must be 4-byte aligned to receive the data.</span></span>

<span data-ttu-id="d0262-134">NetX DNS Istemcisinde, SOA kayıt türü NX_DNS_SOA_ENTRY, 7 4 baytlık parametreler olarak kaydedilir, toplam 28 bayt:</span><span class="sxs-lookup"><span data-stu-id="d0262-134">In NetX DNS Client, the SOA record type, NX_DNS_SOA_ENTRY, is saved as seven 4 byte parameters, totaling 28 bytes:</span></span>

- <span data-ttu-id="d0262-135">**nx_dns_soa_host_mname_ptr**: Bu bölge için birincil veri kaynağı işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d0262-135">**nx_dns_soa_host_mname_ptr**: Pointer to primary source of data for this zone</span></span>
- <span data-ttu-id="d0262-136">**nx_dns_soa_host_rname_ptr**: Bu bölgeden sorumlu olan posta kutusu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d0262-136">**nx_dns_soa_host_rname_ptr**: Pointer to mailbox responsible for this zone</span></span>
- <span data-ttu-id="d0262-137">**nx_dns_soa_serial**: bölge sürüm numarası</span><span class="sxs-lookup"><span data-stu-id="d0262-137">**nx_dns_soa_serial**: Zone version number</span></span>
- <span data-ttu-id="d0262-138">**nx_dns_soa_refresh**: yenileme aralığı</span><span class="sxs-lookup"><span data-stu-id="d0262-138">**nx_dns_soa_refresh**: Refresh interval</span></span>
- <span data-ttu-id="d0262-139">**nx_dns_soa_retry**: SOA sorgu yeniden denemeleri arasındaki Aralık</span><span class="sxs-lookup"><span data-stu-id="d0262-139">**nx_dns_soa_retry**: Interval between SOA query retries</span></span>
- <span data-ttu-id="d0262-140">**nx_dns_soa_expire**: SOA süresi dolduğu zaman süresi</span><span class="sxs-lookup"><span data-stu-id="d0262-140">**nx_dns_soa_expire**: Time duration when SOA expires</span></span>
- <span data-ttu-id="d0262-141">**nx_dns_soa_minmum**: SOA ana BILGISAYAR adı DNS yanıt iletilerinde en düşük TTL alanı</span><span class="sxs-lookup"><span data-stu-id="d0262-141">**nx_dns_soa_minmum**: Minimum TTL field in SOA hostname DNS reply messages</span></span>

<span data-ttu-id="d0262-142">İki SOA kaydının depolanması aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="d0262-142">The storage of a two SOA records is shown below.</span></span> <span data-ttu-id="d0262-143">Sabit uzunluklu verileri içeren SOA kayıtları, arabelleğin en üstünden başlayarak girilir.</span><span class="sxs-lookup"><span data-stu-id="d0262-143">The SOA records containing fixed length data are entered starting at the top of the buffer.</span></span> <span data-ttu-id="d0262-144">MNAME ve RNAME işaretçileri, arabelleğin altında depolanan değişken uzunluklu verileri (ana bilgisayar adları) işaret edin.</span><span class="sxs-lookup"><span data-stu-id="d0262-144">The pointers MNAME and RNAME point to the variable length data (host names) which are stored at the bottom of the buffer.</span></span> <span data-ttu-id="d0262-145">Ek SOA kayıtları, ilk kayıttan sonra ("ek SOA kayıtları...") ve değişken uzunluklu verilerin en son girişin değişken uzunluk verilerinde ("ek SOA değişken uzunluğu verileri") depolandıktan sonra girilir:</span><span class="sxs-lookup"><span data-stu-id="d0262-145">Additional SOA records are entered after the first record (“additional SOA records…”) and their variable length data is stored above the last entry’s variable length data (“additional SOA variable length data”):</span></span>

![İki S O A kaydının depolanmasını temsil eden diyagram](media/image2.png)

<span data-ttu-id="d0262-147">Giriş *record_buffer* , sunucu YANıTıNDA tüm SOA verilerini tutamazsa, *record_buffer* sığacak kadar çok kayıt tutar ve arabellekteki kayıt sayısını döndürür.</span><span class="sxs-lookup"><span data-stu-id="d0262-147">If the input *record_buffer* cannot hold all the SOA data in the server reply, the the *record_buffer* holds as many records as will fit and returns the number of records in the buffer.</span></span>

<span data-ttu-id="d0262-148">\* Record_count ' de döndürülen SOA kaydı sayısı ile *,* uygulama *record_buffer* verileri ayrıştırarak bölge yetkilisi ana bilgisayar adı dizelerinin başlangıcını ayıklayabilir.</span><span class="sxs-lookup"><span data-stu-id="d0262-148">With the number of SOA records returned in \**record_count,* the application can parse the data from *record_buffer* and extract the start of zone authority host name strings.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d0262-149">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d0262-149">Input Parameters</span></span>

- <span data-ttu-id="d0262-150">**dns_ptr**: DNS istemcisi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0262-150">**dns_ptr**: Pointer to DNS Client.</span></span>  
- <span data-ttu-id="d0262-151">**host_name**: için SOA verileri almak için ana bilgisayar adı işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d0262-151">**host_name**: Pointer to host name to obtain SOA data for</span></span>
- <span data-ttu-id="d0262-152">**record_buffer**: SOA verilerinin ayıklanacağı konum işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d0262-152">**record_buffer**: Pointer to location to extract SOA data into</span></span>
- <span data-ttu-id="d0262-153">**Buffer_size**: SOA verilerini tutacak arabelleğin boyutu</span><span class="sxs-lookup"><span data-stu-id="d0262-153">**buffer_size**: Size of buffer to hold SOA data</span></span>
- <span data-ttu-id="d0262-154">**record_count**: alınan SOA kaydı sayısına yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="d0262-154">**record_count**: Pointer to the number of SOA records retrieved</span></span>
- <span data-ttu-id="d0262-155">**wait_option**: DNS sunucusu yanıtı alma seçeneğini bekle</span><span class="sxs-lookup"><span data-stu-id="d0262-155">**wait_option**: Wait option to receive DNS Server response</span></span>

### <a name="return-values"></a><span data-ttu-id="d0262-156">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d0262-156">Return Values</span></span>

- <span data-ttu-id="d0262-157">**NX_SUCCESS**: (0x00) SOA verileri başarıyla alındı</span><span class="sxs-lookup"><span data-stu-id="d0262-157">**NX_SUCCESS**: (0x00) Successfully obtained SOA data</span></span>
- <span data-ttu-id="d0262-158">**NX_DNS_NO_SERVER**: (0xA1) istemci sunucu listesi boş</span><span class="sxs-lookup"><span data-stu-id="d0262-158">**NX_DNS_NO_SERVER**: (0xA1) Client server list is empty</span></span>
- <span data-ttu-id="d0262-159">**NX_DNS_QUERY_FAILED**: (0xA3) GEÇERLI bir DNS yanıtı alınmadı</span><span class="sxs-lookup"><span data-stu-id="d0262-159">**NX_DNS_QUERY_FAILED**: (0xA3) No valid DNS response received</span></span>
- <span data-ttu-id="d0262-160">NX_PTR_ERROR: (0x07) geçersiz IP veya DNS işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d0262-160">NX_PTR_ERROR: (0x07) Invalid IP or DNS pointer</span></span>
- <span data-ttu-id="d0262-161">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="d0262-161">NX_CALLER_ERROR: (0x11) Invalid caller of this service</span></span>
- <span data-ttu-id="d0262-162">NX_DNS_PARAM_ERROR: (0xA8) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="d0262-162">NX_DNS_PARAM_ERROR: (0xA8) Invalid non pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d0262-163">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d0262-163">Allowed From</span></span>

<span data-ttu-id="d0262-164">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d0262-164">Threads</span></span>

### <a name="example"></a><span data-ttu-id="d0262-165">Örnek</span><span class="sxs-lookup"><span data-stu-id="d0262-165">Example</span></span>
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


## <a name="nx_dns_cache_initialize"></a><span data-ttu-id="d0262-166">nx_dns_cache_initialize</span><span class="sxs-lookup"><span data-stu-id="d0262-166">nx_dns_cache_initialize</span></span>

<span data-ttu-id="d0262-167">DNS önbelleğini başlatma</span><span class="sxs-lookup"><span data-stu-id="d0262-167">Initialize the DNS Cache</span></span>

### <a name="prototype"></a><span data-ttu-id="d0262-168">Prototype</span><span class="sxs-lookup"><span data-stu-id="d0262-168">Prototype</span></span>

```c
UINT nx_dns_cache_initialize(NX_DNS *dns_ptr,
                             VOID *cache_ptr, UINT cache_size);

```
### <a name="description"></a><span data-ttu-id="d0262-169">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d0262-169">Description</span></span>

<span data-ttu-id="d0262-170">Bu hizmet bir DNS önbelleği oluşturur ve başlatır.</span><span class="sxs-lookup"><span data-stu-id="d0262-170">This service creates and initializes a DNS Cache.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d0262-171">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d0262-171">Input Parameters</span></span>

- <span data-ttu-id="d0262-172">**dns_ptr**: DNS Denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0262-172">**dns_ptr**: Pointer to DNS control block.</span></span>
- <span data-ttu-id="d0262-173">**cache_ptr**: DNS önbelleğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0262-173">**cache_ptr**: Pointer to DNS Cache.</span></span>
- <span data-ttu-id="d0262-174">**cache_size**: DNS önbelleğinin boyutu (bayt).</span><span class="sxs-lookup"><span data-stu-id="d0262-174">**cache_size**: Size of DNS Cache, in bytes.</span></span>

### <a name="return-values"></a><span data-ttu-id="d0262-175">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d0262-175">Return Values</span></span>

- <span data-ttu-id="d0262-176">**NX_SUCCESS**: (0x00) DNS önbelleği başarıyla başlatıldı</span><span class="sxs-lookup"><span data-stu-id="d0262-176">**NX_SUCCESS**: (0x00) DNS Cache successfully initialized</span></span>
- <span data-ttu-id="d0262-177">NX_DNS_ERROR: (0xA0) önbelleği 4 bayt hizalı değil.</span><span class="sxs-lookup"><span data-stu-id="d0262-177">NX_DNS_ERROR: (0xA0) Cache is not 4-byte aligned.</span></span>
- <span data-ttu-id="d0262-178">NX_DNS_PARAM_ERROR: (0xA8) geçersiz DNS KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="d0262-178">NX_DNS_PARAM_ERROR: (0xA8) Invalid DNS ID.</span></span>
- <span data-ttu-id="d0262-179">NX_PTR_ERROR: (0x07) geçersiz DNS işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0262-179">NX_PTR_ERROR: (0x07) Invalid DNS pointer.</span></span>
- <span data-ttu-id="d0262-180">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="d0262-180">NX_CALLER_ERROR: (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d0262-181">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d0262-181">Allowed From</span></span>

<span data-ttu-id="d0262-182">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d0262-182">Threads</span></span>

### <a name="example"></a><span data-ttu-id="d0262-183">Örnek</span><span class="sxs-lookup"><span data-stu-id="d0262-183">Example</span></span>
```c
UCHAR          dns_cache [2048]; 

/* Initialize the DNS Cache.  */
status =  nx_dns_cache_initialize(&my_dns, dns_cache, 2048);
/* If status is NX_SUCCESS DNS Cache was successfully initialized.  */
```

## <a name="nx_dns_cache_notify_clear"></a><span data-ttu-id="d0262-184">nx_dns_cache_notify_clear</span><span class="sxs-lookup"><span data-stu-id="d0262-184">nx_dns_cache_notify_clear</span></span>

<span data-ttu-id="d0262-185">DNS önbelleği tam bildirim işlevini temizle</span><span class="sxs-lookup"><span data-stu-id="d0262-185">Clear the DNS Cache full notify function</span></span>

### <a name="prototype"></a><span data-ttu-id="d0262-186">Prototype</span><span class="sxs-lookup"><span data-stu-id="d0262-186">Prototype</span></span>

```c
UINT     nx_dns_cache_notify_clear(NX_DNS *dns_ptr);
```
### <a name="description"></a><span data-ttu-id="d0262-187">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d0262-187">Description</span></span>

<span data-ttu-id="d0262-188">Bu hizmet önbellek tam bildirim işlevini temizler.</span><span class="sxs-lookup"><span data-stu-id="d0262-188">This service clears the cache full notify function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d0262-189">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d0262-189">Input Parameters</span></span>

- <span data-ttu-id="d0262-190">**dns_ptr**: DNS Denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0262-190">**dns_ptr**: Pointer to DNS control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="d0262-191">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d0262-191">Return Values</span></span>

- <span data-ttu-id="d0262-192">**NX_SUCCESS**: (0x00) DNS önbelleği bildirme başarıyla ayarlandı</span><span class="sxs-lookup"><span data-stu-id="d0262-192">**NX_SUCCESS**: (0x00) DNS cache notify successfully set</span></span>
- <span data-ttu-id="d0262-193">NX_DNS_PARAM_ERROR: (0xA8) geçersiz DNS KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="d0262-193">NX_DNS_PARAM_ERROR: (0xA8) Invalid DNS ID.</span></span>
- <span data-ttu-id="d0262-194">NX_PTR_ERROR: (0x07) geçersiz DNS işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0262-194">NX_PTR_ERROR: (0x07) Invalid DNS pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d0262-195">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d0262-195">Allowed From</span></span>

<span data-ttu-id="d0262-196">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d0262-196">Threads</span></span>

### <a name="example"></a><span data-ttu-id="d0262-197">Örnek</span><span class="sxs-lookup"><span data-stu-id="d0262-197">Example</span></span>

```c
/* Clear the DNS Cache full notify function.  */
status =  nx_dns_cache_notify_clear(&my_dns);

/* If status is NX_SUCCESS DNS Cache full notify function was successfully cleared. */
```

## <a name="nx_dns_cache_notify_set"></a><span data-ttu-id="d0262-198">nx_dns_cache_notify_set</span><span class="sxs-lookup"><span data-stu-id="d0262-198">nx_dns_cache_notify_set</span></span>

<span data-ttu-id="d0262-199">DNS önbelleği tam bildirim işlevini ayarla</span><span class="sxs-lookup"><span data-stu-id="d0262-199">Set the DNS Cache full notify function</span></span>

### <a name="prototype"></a><span data-ttu-id="d0262-200">Prototype</span><span class="sxs-lookup"><span data-stu-id="d0262-200">Prototype</span></span>

```c
UINT nx_dns_cache_notify_set(NX_DNS *dns_ptr, VOID (*cache_full_notify_cb)(NX_DNS *dns_ptr));
```

### <a name="description"></a><span data-ttu-id="d0262-201">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d0262-201">Description</span></span>

<span data-ttu-id="d0262-202">Bu hizmet önbellek tam bildirim işlevini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d0262-202">This service sets the cache full notify function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d0262-203">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d0262-203">Input Parameters</span></span>

- <span data-ttu-id="d0262-204">**dns_ptr**: DNS Denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0262-204">**dns_ptr**: Pointer to DNS control block.</span></span>
- <span data-ttu-id="d0262-205">**cache_full_notify_cb**: önbellek dolduğunda çağrılacak geri çağırma işlevi.</span><span class="sxs-lookup"><span data-stu-id="d0262-205">**cache_full_notify_cb**: The callback function to be invoked when cache become full.</span></span>

### <a name="return-values"></a><span data-ttu-id="d0262-206">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d0262-206">Return Values</span></span>

- <span data-ttu-id="d0262-207">**NX_SUCCESS**: (0x00) DNS önbelleği bildirme başarıyla ayarlandı</span><span class="sxs-lookup"><span data-stu-id="d0262-207">**NX_SUCCESS**: (0x00) DNS cache notify successfully set</span></span>
- <span data-ttu-id="d0262-208">NX_DNS_PARAM_ERROR: (0xA8) geçersiz DNS KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="d0262-208">NX_DNS_PARAM_ERROR: (0xA8) Invalid DNS ID.</span></span>
- <span data-ttu-id="d0262-209">NX_PTR_ERROR: (0x07) geçersiz DNS işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0262-209">NX_PTR_ERROR: (0x07) Invalid DNS pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d0262-210">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d0262-210">Allowed From</span></span>

<span data-ttu-id="d0262-211">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d0262-211">Threads</span></span>

### <a name="example"></a><span data-ttu-id="d0262-212">Örnek</span><span class="sxs-lookup"><span data-stu-id="d0262-212">Example</span></span>

```c
/* Set the DNS Cache full notify function.  */
status =  nx_dns_cache_notify_set(&my_dns, cache_full_notify_cb);

/* If status is NX_SUCCESS DNS Cache full notify function was successfully set.  */
 
```

## <a name="nx_dns_cname_get"></a><span data-ttu-id="d0262-213">nx_dns_cname_get</span><span class="sxs-lookup"><span data-stu-id="d0262-213">nx_dns_cname_get</span></span>

<span data-ttu-id="d0262-214">Giriş ana bilgisayar adının kurallı adını arayın</span><span class="sxs-lookup"><span data-stu-id="d0262-214">Look up the canonical name for the input hostname</span></span>

### <a name="prototype"></a><span data-ttu-id="d0262-215">Prototype</span><span class="sxs-lookup"><span data-stu-id="d0262-215">Prototype</span></span>
```c
UINT nx_dns_cname_get(NX_DNS *dns_ptr, UCHAR *host_name, 
                      UCHAR *record_buffer, UINT buffer_size, 
                      ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="d0262-216">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d0262-216">Description</span></span>

<span data-ttu-id="d0262-217">NX_DNS_ENABLE_EXTENDED_RR_TYPES *nx_dns. h* içinde tanımlanmışsa, bu hizmet kurallı etki alanı adını almak için belirtilen etki alanı ADıNA sahip CNAME türünde bir sorgu gönderir.</span><span class="sxs-lookup"><span data-stu-id="d0262-217">If NX_DNS_ENABLE_EXTENDED_RR_TYPES is defined in *nx_dns.h*, this service sends a query of type CNAME with the specified domain name to obtain the canonical domain name.</span></span> <span data-ttu-id="d0262-218">DNS Istemcisi, DNS sunucusu yanıtında döndürülen CNAME dizesini *record_buffer* bellek konumuna kopyalar.</span><span class="sxs-lookup"><span data-stu-id="d0262-218">The DNS Client copies the CNAME string returned in the DNS Server response into the *record_buffer* memory location.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d0262-219">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d0262-219">Input Parameters</span></span>

- <span data-ttu-id="d0262-220">**dns_ptr**: DNS istemcisi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0262-220">**dns_ptr**: Pointer to DNS Client.</span></span>  
- <span data-ttu-id="d0262-221">**host_name**: için CNAME verilerinin alınacağı ana bilgisayar adı işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d0262-221">**host_name**: Pointer to host name to obtain CNAME data for</span></span>
- <span data-ttu-id="d0262-222">**record_buffer**: CNAME verilerinin ayıklanacağı konum işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d0262-222">**record_buffer**: Pointer to location to extract CNAME data into</span></span>
- <span data-ttu-id="d0262-223">**Buffer_size**: CNAME verilerini tutacak arabelleğin boyutu</span><span class="sxs-lookup"><span data-stu-id="d0262-223">**buffer_size**: Size of buffer to hold CNAME data</span></span>
- <span data-ttu-id="d0262-224">**wait_option**: DNS sunucusu yanıtı alma seçeneğini bekle</span><span class="sxs-lookup"><span data-stu-id="d0262-224">**wait_option**: Wait option to receive DNS Server response</span></span>

### <a name="return-values"></a><span data-ttu-id="d0262-225">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d0262-225">Return Values</span></span>

- <span data-ttu-id="d0262-226">**NX_SUCCESS**: (0x00) CNAME verileri başarıyla alındı</span><span class="sxs-lookup"><span data-stu-id="d0262-226">**NX_SUCCESS**: (0x00) Successfully obtained CNAME data</span></span>
- <span data-ttu-id="d0262-227">**NX_DNS_NO_SERVER**: (0xA1) istemci sunucu listesi boş</span><span class="sxs-lookup"><span data-stu-id="d0262-227">**NX_DNS_NO_SERVER**: (0xA1) Client server list is empty</span></span>
- <span data-ttu-id="d0262-228">**NX_DNS_QUERY_FAILED**: (0xA3) GEÇERLI bir DNS yanıtı alınmadı</span><span class="sxs-lookup"><span data-stu-id="d0262-228">**NX_DNS_QUERY_FAILED**: (0xA3) No valid DNS response received</span></span>
- <span data-ttu-id="d0262-229">NX_PTR_ERROR: (0x07) geçersiz IP veya DNS işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d0262-229">NX_PTR_ERROR: (0x07) Invalid IP or DNS pointer</span></span>
- <span data-ttu-id="d0262-230">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="d0262-230">NX_CALLER_ERROR: (0x11) Invalid caller of this service</span></span>
- <span data-ttu-id="d0262-231">NX_DNS_PARAM_ERROR: (0xA8) geçersiz işaretçi olmayan giriş</span><span class="sxs-lookup"><span data-stu-id="d0262-231">NX_DNS_PARAM_ERROR: (0xA8) Invalid non-pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d0262-232">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d0262-232">Allowed From</span></span>

<span data-ttu-id="d0262-233">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d0262-233">Threads</span></span>

### <a name="example"></a><span data-ttu-id="d0262-234">Örnek</span><span class="sxs-lookup"><span data-stu-id="d0262-234">Example</span></span>

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

## <a name="nx_dns_create"></a><span data-ttu-id="d0262-235">nx_dns_create</span><span class="sxs-lookup"><span data-stu-id="d0262-235">nx_dns_create</span></span>

<span data-ttu-id="d0262-236">DNS Istemci örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="d0262-236">Create a DNS Client instance</span></span>

### <a name="prototype"></a><span data-ttu-id="d0262-237">Prototype</span><span class="sxs-lookup"><span data-stu-id="d0262-237">Prototype</span></span>

```c
UINT nx_dns_create(NX_DNS *dns_ptr, NX_IP *ip_ptr, CHAR *domain_name);
```

### <a name="description"></a><span data-ttu-id="d0262-238">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d0262-238">Description</span></span>

<span data-ttu-id="d0262-239">Bu hizmet, önceden oluşturulan IP örneği için bir DNS Istemci örneği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d0262-239">This service creates a DNS Client instance for the previously created IP instance.</span></span>

>[!NOTE]
><span data-ttu-id="d0262-240">Uygulama, DNS Istemcisi tarafından kullanılan paket havuzunun paket yükünün, en fazla 512 baytlık DNS iletisi, artı UDP, IP ve Ethernet üstbilgileri için yeterince büyük olduğundan emin olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d0262-240">The application must ensure that the packet payload of the packet pool used by the DNS Client is large enough for the maximum 512 byte DNS message, plus UDP, IP and Ethernet headers.</span></span> <span data-ttu-id="d0262-241">DNS Istemcisi kendi paket havuzunu oluşturursa, bu NX_DNS_PACKET_POOL_SIZE ve NX_DNS_PACKET_PAYLOAD tarafından tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="d0262-241">If the DNS Client creates its own packet pool, this is defined by NX_DNS_PACKET_POOL_SIZE and NX_DNS_PACKET_PAYLOAD.</span></span> <span data-ttu-id="d0262-242">DNS Istemci uygulaması daha önce oluşturulmuş bir paket havuzu sağlamayı tercih ediyorsa, IPv4 DNS Istemcisinin yükü, IP üstbilgisi için en fazla DNS ve 20 bayt, UDP üst bilgisi için 8 bayt ve Ethernet üst bilgisi için 14 bayt 512 olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d0262-242">If the DNS Client application prefers to supply a previously created packet pool, the payload for IPv4 DNS Client should be 512 bytes for the maximum DNS plus 20 bytes for the IP header, 8 bytes for the UDP header and 14 bytes for the Ethernet header.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d0262-243">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d0262-243">Input Parameters</span></span>

- <span data-ttu-id="d0262-244">**dns_ptr**: DNS istemcisi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0262-244">**dns_ptr**: Pointer to DNS Client.</span></span>  
- <span data-ttu-id="d0262-245">**ip_ptr**: daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0262-245">**ip_ptr**: Pointer to previously created IP instance.</span></span>  
- <span data-ttu-id="d0262-246">**domain_name**: DNS örneği için etki alanı adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0262-246">**domain_name**: Pointer to domain name for DNS instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="d0262-247">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d0262-247">Return Values</span></span>

- <span data-ttu-id="d0262-248">**NX_SUCCESS**: (0x00) başarılı DNS oluşturma</span><span class="sxs-lookup"><span data-stu-id="d0262-248">**NX_SUCCESS**: (0x00) Successful DNS create</span></span>
- <span data-ttu-id="d0262-249">**NX_DNS_ERROR**: (0xa0) DNS oluşturma hatası</span><span class="sxs-lookup"><span data-stu-id="d0262-249">**NX_DNS_ERROR**: (0xA0) DNS create error</span></span>
- <span data-ttu-id="d0262-250">NX_PTR_ERROR: (0x07) geçersiz IP veya DNS işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d0262-250">NX_PTR_ERROR: (0x07) Invalid IP or DNS pointer</span></span>
- <span data-ttu-id="d0262-251">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="d0262-251">NX_CALLER_ERROR: (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d0262-252">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d0262-252">Allowed From</span></span>

<span data-ttu-id="d0262-253">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d0262-253">Threads</span></span>

### <a name="example"></a><span data-ttu-id="d0262-254">Örnek</span><span class="sxs-lookup"><span data-stu-id="d0262-254">Example</span></span>

```c
/* Create a DNS Client instance.  */
status =  nx_dns_create(&my_dns, &my_ip, "My DNS");

/* If status is NX_SUCCESS a DNS Client instance was successfully
   created.  */
```
## <a name="nx_dns_delete"></a><span data-ttu-id="d0262-255">nx_dns_delete</span><span class="sxs-lookup"><span data-stu-id="d0262-255">nx_dns_delete</span></span>

<span data-ttu-id="d0262-256">DNS Istemci örneğini silme</span><span class="sxs-lookup"><span data-stu-id="d0262-256">Delete a DNS Client instance</span></span>

### <a name="prototype"></a><span data-ttu-id="d0262-257">Prototype</span><span class="sxs-lookup"><span data-stu-id="d0262-257">Prototype</span></span>

```c
UINT     nx_dns_delete(NX_DNS *dns_ptr);
```

### <a name="description"></a><span data-ttu-id="d0262-258">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d0262-258">Description</span></span>

<span data-ttu-id="d0262-259">Bu hizmet, önceden oluşturulmuş bir DNS Istemci örneğini siler ve kaynaklarını boşaltır.</span><span class="sxs-lookup"><span data-stu-id="d0262-259">This service deletes a previously created DNS Client instance and frees up its resources.</span></span> 
>[!NOTE]
> <span data-ttu-id="d0262-260">**NX_DNS_CLIENT_USER_CREATE_PACKET_POOL** TANıMLANDıYSA ve DNS istemcisine Kullanıcı tanımlı bir paket havuzu atanmışsa, artık GEREKMIYORSA, DNS istemcisi paket havuzunu silmek uygulamaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="d0262-260">If **NX_DNS_CLIENT_USER_CREATE_PACKET_POOL** is defined and the DNS Client was assigned a user defined packet pool, it is up to the application to delete the DNS Client packet pool if it no longer needs it.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d0262-261">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d0262-261">Input Parameters</span></span>

- <span data-ttu-id="d0262-262">**dns_ptr**: daha önce oluşturulan DNS **istemci** örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0262-262">**dns_ptr**: Pointer to previously created DNS **Client** instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="d0262-263">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d0262-263">Return Values</span></span>

- <span data-ttu-id="d0262-264">**NX_SUCCESS**: (0x00) başarılı DNS istemcisi silme.</span><span class="sxs-lookup"><span data-stu-id="d0262-264">**NX_SUCCESS**: (0x00) Successful DNS Client delete.</span></span>
- <span data-ttu-id="d0262-265">NX_PTR_ERROR: (0x07) geçersiz IP veya DNS Istemcisi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0262-265">NX_PTR_ERROR: (0x07) Invalid IP or DNS Client pointer.</span></span>
- <span data-ttu-id="d0262-266">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="d0262-266">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d0262-267">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d0262-267">Allowed From</span></span>

<span data-ttu-id="d0262-268">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d0262-268">Threads</span></span>

### <a name="example"></a><span data-ttu-id="d0262-269">Örnek</span><span class="sxs-lookup"><span data-stu-id="d0262-269">Example</span></span>

```c
/* Delete a DNS Client instance.  */
status =  nx_dns_delete(&my_dns);

/* If status is NX_SUCCESS the DNS Client instance was successfully
   deleted.  */
```
## <a name="nx_dns_domain_name_server_get"></a><span data-ttu-id="d0262-270">nx_dns_domain_name_server_get</span><span class="sxs-lookup"><span data-stu-id="d0262-270">nx_dns_domain_name_server_get</span></span>

<span data-ttu-id="d0262-271">Giriş etki alanı bölgesi için yetkili ad sunucularını arayın</span><span class="sxs-lookup"><span data-stu-id="d0262-271">Look up the authoritative name servers for the input domain zone</span></span>

### <a name="prototype"></a><span data-ttu-id="d0262-272">Prototype</span><span class="sxs-lookup"><span data-stu-id="d0262-272">Prototype</span></span>

```c
UINT nx_dns_domain_name_server_get(NX_DNS *dns_ptr, UCHAR *host_name, 
                                   VOID *record_buffer, UINT buffer_size, 
                                   UINT *record_count, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="d0262-273">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d0262-273">Description</span></span>

<span data-ttu-id="d0262-274">NX_DNS_ENABLE_EXTENDED_RR_TYPES tanımlanmışsa, bu hizmet giriş etki alanı adının ad sunucularını almak için belirtilen etki alanı adına sahip NS türünde bir sorgu gönderir.</span><span class="sxs-lookup"><span data-stu-id="d0262-274">If NX_DNS_ENABLE_EXTENDED_RR_TYPES is defined, this service sends a query of type NS with the specified domain name to obtain the name servers for the input domain name.</span></span> <span data-ttu-id="d0262-275">DNS Istemcisi, DNS sunucusu yanıtında döndürülen NS kayıtlarını *record_buffer* bellek konumuna kopyalar.</span><span class="sxs-lookup"><span data-stu-id="d0262-275">The DNS Client copies the NS record(s) returned in the DNS Server response into the *record_buffer* memory location.</span></span> 

>[!NOTE]
><span data-ttu-id="d0262-276">*Record_buffer* , verileri almak için 4 baytlık hizalı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d0262-276">The *record_buffer* must be 4-byte aligned to receive the data.</span></span>

<span data-ttu-id="d0262-277">NetX DNS Istemcisinde NS veri türü NX_DNS_NS_ENTRY, 2 4 baytlık parametreler olarak kaydedilir:</span><span class="sxs-lookup"><span data-stu-id="d0262-277">In NetX DNS Client the NS data type, NX_DNS_NS_ENTRY, is saved as two 4-byte parameters:</span></span>

- <span data-ttu-id="d0262-278">**nx_dns_ns_ipv4_address**: sunucunun IPv4 adresini Adlandır</span><span class="sxs-lookup"><span data-stu-id="d0262-278">**nx_dns_ns_ipv4_address**: Name server’s IPv4 address</span></span>
- <span data-ttu-id="d0262-279">**nx_dns_ns_hostname_ptr**: ad sunucusunun ana bilgisayar adı işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d0262-279">**nx_dns_ns_hostname_ptr**: Pointer to the name server’s hostname</span></span>

<span data-ttu-id="d0262-280">Aşağıda gösterilen arabellek dört NX_DNS_NS_ENTRY kaydı içerir.</span><span class="sxs-lookup"><span data-stu-id="d0262-280">The buffer shown below contains four NX_DNS_NS_ENTRY records.</span></span> <span data-ttu-id="d0262-281">Her girişte ana bilgisayar adı dizesinin işaretçisi, arabelleğin alt yarısında karşılık gelen ana bilgisayar adı dizesine işaret eder:</span><span class="sxs-lookup"><span data-stu-id="d0262-281">The pointer to host name string in each entry points to the corresponding host name string in the bottom half of the buffer:</span></span>

![Dört N X D N S N s giriş kaydı içeren arabelleğin diyagramı.](media/image3.png)

<span data-ttu-id="d0262-283">Giriş *record_buffer* , sunucu YANıTıNDA tüm NS verilerini tutamazsa, *record_buffer* sığacak kadar çok kayıt tutar ve arabellekteki kayıt sayısını döndürür.</span><span class="sxs-lookup"><span data-stu-id="d0262-283">If the input *record_buffer* cannot hold all the NS data in the server reply, the the *record_buffer* holds as many records as will fit and returns the number of records in the buffer.</span></span>

<span data-ttu-id="d0262-284">\* Record_count ' de döndürülen NS kayıtlarının sayısı ile *,* uygulama *RECORD_BUFFER* her kaydın IP adresini ve ana bilgisayar adını ayrıştırabilirler.</span><span class="sxs-lookup"><span data-stu-id="d0262-284">With the number of NS records returned in \**record_count,* the application can parse the IP address and host name of each record in the *record_buffer*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d0262-285">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d0262-285">Input Parameters</span></span>

- <span data-ttu-id="d0262-286">**dns_ptr**: DNS istemcisi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0262-286">**dns_ptr**: Pointer to DNS Client.</span></span>  
- <span data-ttu-id="d0262-287">**host_name**: NS verilerini almak için ana bilgisayar adı işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d0262-287">**host_name**: Pointer to host name to obtain NS data for</span></span>
- <span data-ttu-id="d0262-288">**record_buffer**: NS verilerinin ayıklanacağı konum işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d0262-288">**record_buffer**: Pointer to location to extract NS data into</span></span>
- <span data-ttu-id="d0262-289">**Buffer_size**: NS verilerini tutan arabelleğin boyutu</span><span class="sxs-lookup"><span data-stu-id="d0262-289">**buffer_size**: Size of buffer to hold NS data</span></span>
- <span data-ttu-id="d0262-290">**record_count**: alınan NS kaydı sayısının işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d0262-290">**record_count**: Pointer to the number of NS records retrieved</span></span>
- <span data-ttu-id="d0262-291">**wait_option**: DNS sunucusu yanıtı alma seçeneğini bekle</span><span class="sxs-lookup"><span data-stu-id="d0262-291">**wait_option**: Wait option to receive DNS Server response</span></span>

### <a name="return-values"></a><span data-ttu-id="d0262-292">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d0262-292">Return Values</span></span>

- <span data-ttu-id="d0262-293">**NX_SUCCESS**: (0x00) NS verileri başarıyla alındı</span><span class="sxs-lookup"><span data-stu-id="d0262-293">**NX_SUCCESS**: (0x00) Successfully obtained NS data</span></span>
- <span data-ttu-id="d0262-294">**NX_DNS_NO_SERVER**: (0xA1) istemci sunucu listesi boş</span><span class="sxs-lookup"><span data-stu-id="d0262-294">**NX_DNS_NO_SERVER**: (0xA1) Client server list is empty</span></span>
- <span data-ttu-id="d0262-295">**NX_DNS_QUERY_FAILED**: (0xA3) GEÇERLI bir DNS yanıtı alınmadı</span><span class="sxs-lookup"><span data-stu-id="d0262-295">**NX_DNS_QUERY_FAILED**: (0xA3) No valid DNS response received</span></span>
- <span data-ttu-id="d0262-296">NX_DNS_PARAM_ERROR: (0xA8) geçersiz DNS KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="d0262-296">NX_DNS_PARAM_ERROR: (0xA8) Invalid DNS ID.</span></span>
- <span data-ttu-id="d0262-297">NX_PTR_ERROR: (0x07) geçersiz IP veya DNS işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d0262-297">NX_PTR_ERROR: (0x07) Invalid IP or DNS pointer</span></span>
- <span data-ttu-id="d0262-298">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="d0262-298">NX_CALLER_ERROR: (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d0262-299">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d0262-299">Allowed From</span></span>

<span data-ttu-id="d0262-300">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d0262-300">Threads</span></span>

### <a name="example"></a><span data-ttu-id="d0262-301">Örnek</span><span class="sxs-lookup"><span data-stu-id="d0262-301">Example</span></span>
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

## <a name="nx_dns_domain_mail_exchange_get"></a><span data-ttu-id="d0262-302">nx_dns_domain_mail_exchange_get</span><span class="sxs-lookup"><span data-stu-id="d0262-302">nx_dns_domain_mail_exchange_get</span></span>

<span data-ttu-id="d0262-303">Giriş ana bilgisayar adı için posta alışverişinin aranacağı</span><span class="sxs-lookup"><span data-stu-id="d0262-303">Look up the mail exchange(s) for the input host name</span></span>

### <a name="prototype"></a><span data-ttu-id="d0262-304">Prototype</span><span class="sxs-lookup"><span data-stu-id="d0262-304">Prototype</span></span>
```c
UINT     nx_dns_domain_mail_exchange_get(NX_DNS *dns_ptr, UCHAR *host_name, 
                                        VOID *record_buffer,                                        
                                        UINT buffer_size, 
                                        UINT *record_count, 
                                        ULONG wait_option);

```

### <a name="description"></a><span data-ttu-id="d0262-305">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d0262-305">Description</span></span>

<span data-ttu-id="d0262-306">NX_DNS_ENABLE_EXTENDED_RR_TYPES tanımlanmışsa, bu hizmet giriş etki alanı adı için posta değişimini almak üzere belirtilen etki alanı adına sahip MX türünde bir sorgu gönderir.</span><span class="sxs-lookup"><span data-stu-id="d0262-306">If NX_DNS_ENABLE_EXTENDED_RR_TYPES is defined, this service sends a query of type MX with the specified domain name to obtain the mail exchange for the input domain name.</span></span> <span data-ttu-id="d0262-307">DNS Istemcisi, DNS sunucusu yanıtında döndürülen MX kayıtlarını *record_buffer* bellek konumuna kopyalar.</span><span class="sxs-lookup"><span data-stu-id="d0262-307">The DNS Client copies the MX record(s) returned in the DNS Server response into the *record_buffer* memory location.</span></span>

>[!NOTE]
><span data-ttu-id="d0262-308">*Record_buffer* , verileri almak için 4 baytlık hizalı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d0262-308">The *record_buffer* must be 4-byte aligned to receive the data.</span></span>

<span data-ttu-id="d0262-309">NetX DNS Istemcisinde posta değişim kayıt türü NX_DNS_MAIL_EXCHANGE_ENTRY, dört parametre olarak kaydedilir, bu da 12 baytı toplam olarak kaydeder:</span><span class="sxs-lookup"><span data-stu-id="d0262-309">In NetX DNS Client, the mail exchange record type, NX_DNS_MAIL_EXCHANGE_ENTRY, is saved as four parameters, totaling 12 bytes:</span></span>

- <span data-ttu-id="d0262-310">**nx_dns_mx_ipv4_address**: posta değişimi IPv4 adresi 4 bayt</span><span class="sxs-lookup"><span data-stu-id="d0262-310">**nx_dns_mx_ipv4_address**: Mail exchange IPv4 address 4 bytes</span></span>
- <span data-ttu-id="d0262-311">**nx_dns_mx_preference**: tercih 2 bayt</span><span class="sxs-lookup"><span data-stu-id="d0262-311">**nx_dns_mx_preference**: Preference 2 bytes</span></span>
- <span data-ttu-id="d0262-312">**nx_dns_mx_reserved0**: ayrılmış 2 bayt</span><span class="sxs-lookup"><span data-stu-id="d0262-312">**nx_dns_mx_reserved0**: Reserved 2 bytes</span></span>
- <span data-ttu-id="d0262-313">**nx_dns_mx_hostname_ptr**: posta Exchange Server ana bilgisayar adı 4 bayt işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d0262-313">**nx_dns_mx_hostname_ptr**: Pointer to mail exchange server host name 4 bytes</span></span>

<span data-ttu-id="d0262-314">Dört MX kaydı içeren bir arabellek aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="d0262-314">A buffer containing four MX records is shown below.</span></span> <span data-ttu-id="d0262-315">Her kayıt, yukarıdaki listeden sabit uzunluklu verileri içerir.</span><span class="sxs-lookup"><span data-stu-id="d0262-315">Each record contains the fixed length data from the list above.</span></span> <span data-ttu-id="d0262-316">Posta Exchange Server ana bilgisayar adının işaretçisi, arabelleğin alt kısmındaki karşılık gelen ana bilgisayar adına işaret eder.</span><span class="sxs-lookup"><span data-stu-id="d0262-316">The pointer to the mail exchange server host name points to the corresponding host name at the bottom of the buffer.</span></span>

![Dört adet d X kaydı içeren arabelleği gösteren diyagram.](media/image4.png)

<span data-ttu-id="d0262-318">Giriş *record_buffer* , sunucu YANıTıNDA tüm MX verilerini tutamazsa, *record_buffer* sığacak kadar çok kayıt tutar ve arabellekteki kayıt sayısını döndürür.</span><span class="sxs-lookup"><span data-stu-id="d0262-318">If the input *record_buffer* cannot hold all the MX data in the server reply, the the *record_buffer* holds as many records as will fit and returns the number of records in the buffer.</span></span>

<span data-ttu-id="d0262-319">\**Record_count* ' de döndürülen MX kayıtlarının sayısı ile, uygulama, *record_buffer* her kaydın posta ana bilgisayar adı da dahil olmak üzere MX parametrelerini ayrıştırabilirler.</span><span class="sxs-lookup"><span data-stu-id="d0262-319">With the number of MX records returned in \**record_count,* the application can parse the MX parameters, including the mail host name of each record in the *record_buffer*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d0262-320">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d0262-320">Input Parameters</span></span>

- <span data-ttu-id="d0262-321">**dns_ptr**: DNS istemcisi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0262-321">**dns_ptr**: Pointer to DNS Client.</span></span>  
- <span data-ttu-id="d0262-322">**host_name**: MX verilerini almak için ana bilgisayar adı işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d0262-322">**host_name**: Pointer to host name to obtain MX data for</span></span>
- <span data-ttu-id="d0262-323">**record_buffer**: MX verilerinin ayıklanacağı konum işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d0262-323">**record_buffer**: Pointer to location to extract MX data into</span></span>
- <span data-ttu-id="d0262-324">**Buffer_size**: MX verilerini tutan arabelleğin boyutu</span><span class="sxs-lookup"><span data-stu-id="d0262-324">**buffer_size**: Size of buffer to hold MX data</span></span>
- <span data-ttu-id="d0262-325">**record_count**: alınan MX kaydı sayısının işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d0262-325">**record_count**: Pointer to the number of MX records retrieved</span></span>
- <span data-ttu-id="d0262-326">**wait_option**: DNS sunucusu yanıtı alma seçeneğini bekle</span><span class="sxs-lookup"><span data-stu-id="d0262-326">**wait_option**: Wait option to receive DNS Server response</span></span>

### <a name="return-values"></a><span data-ttu-id="d0262-327">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d0262-327">Return Values</span></span>

- <span data-ttu-id="d0262-328">**NX_SUCCESS**: (0x00) MX verileri başarıyla alındı</span><span class="sxs-lookup"><span data-stu-id="d0262-328">**NX_SUCCESS**: (0x00) Successfully obtained MX data</span></span>
- <span data-ttu-id="d0262-329">**NX_DNS_NO_SERVER**: (0xA1) istemci sunucu listesi boş</span><span class="sxs-lookup"><span data-stu-id="d0262-329">**NX_DNS_NO_SERVER**: (0xA1) Client server list is empty</span></span>
- <span data-ttu-id="d0262-330">**NX_DNS_QUERY_FAILED**: (0xA3) GEÇERLI bir DNS yanıtı alınmadı</span><span class="sxs-lookup"><span data-stu-id="d0262-330">**NX_DNS_QUERY_FAILED**: (0xA3) No valid DNS response received</span></span>
- <span data-ttu-id="d0262-331">NX_DNS_PARAM_ERROR: (0xA8) geçersiz DNS KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="d0262-331">NX_DNS_PARAM_ERROR: (0xA8) Invalid DNS ID.</span></span>
- <span data-ttu-id="d0262-332">NX_PTR_ERROR: (0x07) geçersiz IP veya DNS işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d0262-332">NX_PTR_ERROR: (0x07) Invalid IP or DNS pointer</span></span>
- <span data-ttu-id="d0262-333">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="d0262-333">NX_CALLER_ERROR: (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d0262-334">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d0262-334">Allowed From</span></span>

<span data-ttu-id="d0262-335">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d0262-335">Threads</span></span>

### <a name="example"></a><span data-ttu-id="d0262-336">Örnek</span><span class="sxs-lookup"><span data-stu-id="d0262-336">Example</span></span>
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


## <a name="nx_dns_domain_service_get"></a><span data-ttu-id="d0262-337">nx_dns_domain_service_get</span><span class="sxs-lookup"><span data-stu-id="d0262-337">nx_dns_domain_service_get</span></span>

<span data-ttu-id="d0262-338">Giriş ana bilgisayar adı tarafından belirtilen hizmet (ler) i ara</span><span class="sxs-lookup"><span data-stu-id="d0262-338">Look up the service(s) provided by the input host name</span></span>

### <a name="prototype"></a><span data-ttu-id="d0262-339">Prototype</span><span class="sxs-lookup"><span data-stu-id="d0262-339">Prototype</span></span>

```c
UINT nx_dns_domain_service_get (NX_DNS *dns_ptr, UCHAR *host_name, 
                                VOID *record_buffer, UINT buffer_size, 
                                UINT *record_count, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="d0262-340">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d0262-340">Description</span></span>

<span data-ttu-id="d0262-341">NX_DNS_ENABLE_EXTENDED_RR_TYPES tanımlanmışsa, bu hizmet, hizmet (ler) i ve belirtilen etki alanıyla ilişkili bağlantı noktası numaralarını aramak için belirtilen etki alanı adına sahip SRV türünde bir sorgu gönderir.</span><span class="sxs-lookup"><span data-stu-id="d0262-341">If NX_DNS_ENABLE_EXTENDED_RR_TYPES is defined, this service sends a query of type SRV with the specified domain name to look up the service(s) and their port number associated with the specified domain.</span></span> <span data-ttu-id="d0262-342">DNS Istemcisi, DNS sunucusu yanıtında döndürülen SRV kayıtlarını *record_buffer* bellek konumuna kopyalar.</span><span class="sxs-lookup"><span data-stu-id="d0262-342">The DNS Client copies the SRV record(s) returned in the DNS Server response into the *record_buffer* memory location.</span></span> 

>[!NOTE]
><span data-ttu-id="d0262-343">*Record_buffer* , verileri almak için 4 baytlık hizalı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d0262-343">The *record_buffer* must be 4-byte aligned to receive the data.</span></span>

<span data-ttu-id="d0262-344">NetX DNS Istemcisinde hizmet kayıt türü NX_DNS_SRV_ GIRIŞI, altı parametre olarak kaydedilir ve 16 baytlık bir toplam olur.</span><span class="sxs-lookup"><span data-stu-id="d0262-344">In NetX DNS Client, the service record type, NX_DNS_SRV_ ENTRY, is saved as six parameters, totaling 16 bytes.</span></span> <span data-ttu-id="d0262-345">Bu, değişken uzunlukta SRV verilerinin bellek verimli şekilde depolanmasını sağlar:</span><span class="sxs-lookup"><span data-stu-id="d0262-345">This enables variable length SRV data to be stored in a memory efficient manner:</span></span>

- <span data-ttu-id="d0262-346">**Sunucu IPv4 adresi**: nx_dns_srv_ipv4_address 4 bayt</span><span class="sxs-lookup"><span data-stu-id="d0262-346">**Server IPv4 address**: nx_dns_srv_ipv4_address 4 bytes</span></span>
- <span data-ttu-id="d0262-347">**Sunucu önceliği**: nx_dns_srv_priority 2 bayt</span><span class="sxs-lookup"><span data-stu-id="d0262-347">**Server priority**: nx_dns_srv_priority 2 bytes</span></span>
- <span data-ttu-id="d0262-348">**Sunucu ağırlığı**: nx_dns_srv_weight 2 bayt</span><span class="sxs-lookup"><span data-stu-id="d0262-348">**Server weight**: nx_dns_srv_weight 2 bytes</span></span>
- <span data-ttu-id="d0262-349">**Hizmet bağlantı noktası numarası**: nx_dns_srv_port_number 2 bayt</span><span class="sxs-lookup"><span data-stu-id="d0262-349">**Service port number**: nx_dns_srv_port_number 2 bytes</span></span>
- <span data-ttu-id="d0262-350">**4 baytlık hizalama Için ayrılmıştır**: nx_dns_srv_reserved0 2 bayt</span><span class="sxs-lookup"><span data-stu-id="d0262-350">**Reserved for 4-byte alignment**: nx_dns_srv_reserved0 2 bytes</span></span>
- <span data-ttu-id="d0262-351">**Sunucu ana bilgisayar adı işaretçisi**: \* nx_dns_srv_hostname_ptr 4 bayt</span><span class="sxs-lookup"><span data-stu-id="d0262-351">**Pointer to server host name**: \*nx_dns_srv_hostname_ptr 4 bytes</span></span>

<span data-ttu-id="d0262-352">Dört SRV kaydı, sağlanan arabellekte depolanır.</span><span class="sxs-lookup"><span data-stu-id="d0262-352">Four SRV records are stored in the supplied buffer.</span></span> <span data-ttu-id="d0262-353">Her bir NX_DNS_SRV_ENTRY kaydı, kayıt arabelleğinin alt kısmındaki karşılık gelen ana bilgisayar adı dizesine işaret eden *nx_dns_srv_hostname_ptr* bir işaretçi içerir:</span><span class="sxs-lookup"><span data-stu-id="d0262-353">Each NX_DNS_SRV_ENTRY record contains a pointer, *nx_dns_srv_hostname_ptr*, that points to the corresponding host name string in the bottom of the record buffer:</span></span>

![Sağlanan arabellekte depolanan dört S R V kaydı diyagramı.](media/image5.png)

<span data-ttu-id="d0262-355">Giriş *record_buffer* , sunucu YANıTıNDA tüm SRV verilerini tutamazsa, *record_buffer* sığacak kadar çok kayıt tutar ve arabellekteki kayıt sayısını döndürür.</span><span class="sxs-lookup"><span data-stu-id="d0262-355">If the input *record_buffer* cannot hold all the SRV data in the server reply, the the *record_buffer* holds as many records as will fit and returns the number of records in the buffer.</span></span>

<span data-ttu-id="d0262-356">\**Record_count* ' de döndürülen SRV kayıtlarının sayısı ile, uygulama, *record_buffer* her kaydın sunucu ana bilgisayar adı da dahil olmak üzere SRV parametrelerini ayrıştırabilirler.</span><span class="sxs-lookup"><span data-stu-id="d0262-356">With the number of SRV records returned in \**record_count,* the application can parse the SRV parameters, including the server host name of each record in the *record_buffer*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d0262-357">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d0262-357">Input Parameters</span></span>

- <span data-ttu-id="d0262-358">**dns_ptr**: DNS istemcisi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0262-358">**dns_ptr**: Pointer to DNS Client.</span></span>  
- <span data-ttu-id="d0262-359">**host_name**: SRV verilerini almak için ana bilgisayar adı işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d0262-359">**host_name**: Pointer to host name to obtain SRV data for</span></span>
- <span data-ttu-id="d0262-360">**record_buffer**: SRV verilerinin ayıklanacağı konum işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d0262-360">**record_buffer**: Pointer to location to extract SRV data into</span></span>
- <span data-ttu-id="d0262-361">**Buffer_size**: SRV verilerini tutan arabelleğin boyutu</span><span class="sxs-lookup"><span data-stu-id="d0262-361">**buffer_size**: Size of buffer to hold SRV data</span></span>
- <span data-ttu-id="d0262-362">**record_count**: alınan SRV kaydı sayısına yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="d0262-362">**record_count**: Pointer to the number of SRV records retrieved</span></span>
- <span data-ttu-id="d0262-363">**wait_option**: DNS sunucusu yanıtı alma seçeneğini bekle</span><span class="sxs-lookup"><span data-stu-id="d0262-363">**wait_option**: Wait option to receive DNS Server response</span></span>

### <a name="return-values"></a><span data-ttu-id="d0262-364">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d0262-364">Return Values</span></span>

- <span data-ttu-id="d0262-365">**NX_SUCCESS**: (0x00) SRV verileri başarıyla alındı</span><span class="sxs-lookup"><span data-stu-id="d0262-365">**NX_SUCCESS**: (0x00) Successfully obtained SRV data</span></span>
- <span data-ttu-id="d0262-366">**NX_DNS_NO_SERVER**: (0xA1) istemci sunucu listesi boş</span><span class="sxs-lookup"><span data-stu-id="d0262-366">**NX_DNS_NO_SERVER**: (0xA1) Client server list is empty</span></span>
- <span data-ttu-id="d0262-367">**NX_DNS_QUERY_FAILED**: (0xA3) GEÇERLI bir DNS yanıtı alınmadı</span><span class="sxs-lookup"><span data-stu-id="d0262-367">**NX_DNS_QUERY_FAILED**: (0xA3) No valid DNS response received</span></span>
- <span data-ttu-id="d0262-368">NX_DNS_PARAM_ERROR: (0xA8) geçersiz DNS KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="d0262-368">NX_DNS_PARAM_ERROR: (0xA8) Invalid DNS ID.</span></span>
- <span data-ttu-id="d0262-369">NX_PTR_ERROR: (0x07) geçersiz IP veya DNS işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d0262-369">NX_PTR_ERROR: (0x07) Invalid IP or DNS pointer</span></span>
- <span data-ttu-id="d0262-370">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="d0262-370">NX_CALLER_ERROR: (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d0262-371">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d0262-371">Allowed From</span></span>

<span data-ttu-id="d0262-372">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d0262-372">Threads</span></span>

### <a name="example"></a><span data-ttu-id="d0262-373">Örnek</span><span class="sxs-lookup"><span data-stu-id="d0262-373">Example</span></span>

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

## <a name="nx_dns_get_serverlist_size"></a><span data-ttu-id="d0262-374">nx_dns_get_serverlist_size</span><span class="sxs-lookup"><span data-stu-id="d0262-374">nx_dns_get_serverlist_size</span></span>

<span data-ttu-id="d0262-375">DNS Istemcisinin sunucu listesinin boyutunu döndürür</span><span class="sxs-lookup"><span data-stu-id="d0262-375">Return the size of the DNS Client’s Server list</span></span>

### <a name="prototype"></a><span data-ttu-id="d0262-376">Prototype</span><span class="sxs-lookup"><span data-stu-id="d0262-376">Prototype</span></span>

```c
UINT nx_dns_get_serverlist_size (NX_DNS *dns_ptr, UINT *size);
```

### <a name="description"></a><span data-ttu-id="d0262-377">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d0262-377">Description</span></span>

<span data-ttu-id="d0262-378">Bu hizmet, Istemci listesindeki geçerli DNS sunucularının sayısını döndürür.</span><span class="sxs-lookup"><span data-stu-id="d0262-378">This service returns the number of valid DNS Servers in the Client list.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d0262-379">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d0262-379">Input Parameters</span></span>

- <span data-ttu-id="d0262-380">**dns_ptr**: DNS denetim bloğu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d0262-380">**dns_ptr**: Pointer to DNS control block</span></span>  
- <span data-ttu-id="d0262-381">**Boyut**: listedeki sunucu sayısını döndürür</span><span class="sxs-lookup"><span data-stu-id="d0262-381">**size**: Returns the number of servers in the list</span></span>

### <a name="return-values"></a><span data-ttu-id="d0262-382">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d0262-382">Return Values</span></span>

- <span data-ttu-id="d0262-383">**NX_SUCCESS**: (0x00) DNS sunucusu liste boyutu başarıyla döndürüldü</span><span class="sxs-lookup"><span data-stu-id="d0262-383">**NX_SUCCESS**: (0x00) DNS Server list size successfully returned</span></span>
- <span data-ttu-id="d0262-384">NX_PTR_ERROR: (0x07) geçersiz IP veya DNS işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0262-384">NX_PTR_ERROR: (0x07) Invalid IP or DNS pointer.</span></span>
- <span data-ttu-id="d0262-385">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="d0262-385">NX_CALLER_ERROR: (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d0262-386">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d0262-386">Allowed From</span></span>

<span data-ttu-id="d0262-387">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d0262-387">Threads</span></span>

### <a name="example"></a><span data-ttu-id="d0262-388">Örnek</span><span class="sxs-lookup"><span data-stu-id="d0262-388">Example</span></span>

```c
UINT my_listsize;

/* Get the number of non null DNS Servers in the Client list.  */
status =  nx_dns_get_serverlist_size (&my_dns, 5, &my_listsize);

/* If status is NX_SUCCESS the size of the DNS Server list was successfully
   returned.  */
```

## <a name="nx_dns_info_by_name_get"></a><span data-ttu-id="d0262-389">nx_dns_info_by_name_get</span><span class="sxs-lookup"><span data-stu-id="d0262-389">nx_dns_info_by_name_get</span></span>

<span data-ttu-id="d0262-390">IP adresini ve DNS sunucusunun bağlantı noktasını ana bilgisayar adına göre döndür</span><span class="sxs-lookup"><span data-stu-id="d0262-390">Return ip address and port of DNS server by host name</span></span>

### <a name="prototype"></a><span data-ttu-id="d0262-391">Prototype</span><span class="sxs-lookup"><span data-stu-id="d0262-391">Prototype</span></span>

```c
UINT nx_dns_info_by_name_get(NX_DNS *dns_ptr, UCHAR *host_name, 
                             ULONG *host_address_ptr,  
                             USHORT *host_port_ptr, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="d0262-392">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d0262-392">Description</span></span>

<span data-ttu-id="d0262-393">Bu hizmet, DNS sorgusunun giriş ana bilgisayar adına göre sunucu IP 'sini ve bağlantı noktasını (hizmet kaydı) döndürür.</span><span class="sxs-lookup"><span data-stu-id="d0262-393">This service returns the Server IP and port (service record) based on the input host name by DNS query.</span></span> <span data-ttu-id="d0262-394">Bir hizmet kaydı bulunamazsa, bu yordam giriş adresi İşaretçisinde sıfır bir IP adresi döndürür ve bir hatayı bildirmek için sıfır olmayan bir hata durumu döndürür.</span><span class="sxs-lookup"><span data-stu-id="d0262-394">If a service record is not found, this routine returns a zero IP address in the input address pointer and a non-zero error status return to signal an error.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d0262-395">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d0262-395">Input Parameters</span></span>

- <span data-ttu-id="d0262-396">**dns_ptr**: DNS denetim bloğu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d0262-396">**dns_ptr**: Pointer to DNS control block</span></span>  
- <span data-ttu-id="d0262-397">**host_name**: Ana bilgisayar adı arabelleği işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d0262-397">**host_name**: Pointer to host name buffer</span></span>
- <span data-ttu-id="d0262-398">**host_address_ptr**: döndürülecek adrese yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="d0262-398">**host_address_ptr**: Pointer to address to return</span></span>
- <span data-ttu-id="d0262-399">**host_port_ptr**: DNS yanıtı Için wait_option bekle seçeneğini döndürecek bağlantı noktası işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d0262-399">**host_port_ptr**: Pointer to port to return wait_option Wait option for the DNS response</span></span>

### <a name="return-values"></a><span data-ttu-id="d0262-400">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d0262-400">Return Values</span></span>

- <span data-ttu-id="d0262-401">**NX_SUCCESS**: (0x00) DNS sunucusu kaydı başarıyla döndürüldü</span><span class="sxs-lookup"><span data-stu-id="d0262-401">**NX_SUCCESS**: (0x00) DNS Server record successfully returned</span></span>
- <span data-ttu-id="d0262-402">**NX_DNS_NO_SERVER**: (0xA1) ana bilgisayar adına sorgu göndermek için istemciyle bırlıkte kayıtlı DNS sunucusu yok</span><span class="sxs-lookup"><span data-stu-id="d0262-402">**NX_DNS_NO_SERVER**: (0xA1) No DNS Server registered with Client to send query on hostname</span></span>
- <span data-ttu-id="d0262-403">**NX_DNS_QUERY_FAILED**: (0xA3) DNS sorgusu başarısız oldu; giriş ana bilgisayar adı için Istemci listesindeki herhangi bir DNS sunucusundan yanıt yok veya hizmet kaydı yok.</span><span class="sxs-lookup"><span data-stu-id="d0262-403">**NX_DNS_QUERY_FAILED**: (0xA3) DNS query failed; no response from any DNS servers in Client list or no service record is available for the input hostname.</span></span>
- <span data-ttu-id="d0262-404">NX_PTR_ERROR: (0x07) geçersiz IP veya DNS işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d0262-404">NX_PTR_ERROR: (0x07) Invalid IP or DNS pointer</span></span>
- <span data-ttu-id="d0262-405">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="d0262-405">NX_CALLER_ERROR: (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d0262-406">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d0262-406">Allowed From</span></span>

<span data-ttu-id="d0262-407">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d0262-407">Threads</span></span>

### <a name="example"></a><span data-ttu-id="d0262-408">Örnek</span><span class="sxs-lookup"><span data-stu-id="d0262-408">Example</span></span>
```c
ULONG         ip_address;
USHORT         port;

/* Attempt to resolve the IP address and ports for this host name.  */
status =  nx_dns_info_by_name_get(&my_dns, “www.abc1234.com”, &ip_address, &port, 200);

/* If status is NX_SUCCESS the DNS query was successful and the IP address and
   report for the hostname are returned.  */
```

## <a name="nx_dns_ipv4_address_by_name_get"></a><span data-ttu-id="d0262-409">nx_dns_ipv4_address_by_name_get</span><span class="sxs-lookup"><span data-stu-id="d0262-409">nx_dns_ipv4_address_by_name_get</span></span>

<span data-ttu-id="d0262-410">Giriş ana bilgisayar adı için IPv4 adresini arayın</span><span class="sxs-lookup"><span data-stu-id="d0262-410">Look up the IPv4 address for the input host name</span></span>

### <a name="prototype"></a><span data-ttu-id="d0262-411">Prototype</span><span class="sxs-lookup"><span data-stu-id="d0262-411">Prototype</span></span>

```c
UINT nx_dns_ipv4_address_by_name_get (NX_DNS *dns_ptr, 
                                       UCHAR *host_name_ptr, VOID *buffer, 
                                       UINT buffer_size, 
                                       UINT *record_count,
                                       ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="d0262-412">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d0262-412">Description</span></span>

<span data-ttu-id="d0262-413">Bu hizmet, giriş ana bilgisayar adı için IP adreslerini almak üzere belirtilen ana bilgisayar adına sahip A türünde bir sorgu gönderir.</span><span class="sxs-lookup"><span data-stu-id="d0262-413">This service sends a query of Type A with the specified host name to obtain the IP addresses for the input host name.</span></span> <span data-ttu-id="d0262-414">DNS Istemcisi, IPv4 adresini DNS sunucusu yanıtında döndürülen bir kayıt (lar) dan *record_buffer* bellek konumuna kopyalar.</span><span class="sxs-lookup"><span data-stu-id="d0262-414">The DNS Client copies the IPv4 address from the A record(s) returned in the DNS Server response into the *record_buffer* memory location.</span></span> 

>[!NOTE]
><span data-ttu-id="d0262-415">*Record_buffer* , verileri almak için 4 baytlık hizalı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d0262-415">The *record_buffer* must be 4-byte aligned to receive the data.</span></span>

<span data-ttu-id="d0262-416">Aşağıda gösterildiği gibi, 4 baytlık hizalanmış arabellekte birden çok IPv4 adresi depolanır:</span><span class="sxs-lookup"><span data-stu-id="d0262-416">Multiple IPv4 addresses are stored in the 4-byte aligned buffer as shown below:</span></span>

![4 bayt hizalı arabellekte depolanan birden fazla ı P v 4 adresinin diyagramı.](media/image6.png)

<span data-ttu-id="d0262-418">Sağlanan arabellek tüm IP adresi verilerini tutamıyorsa, kalan kayıtlar *record_buffer* depolanmaz.</span><span class="sxs-lookup"><span data-stu-id="d0262-418">If the supplied buffer cannot hold all the IP address data, the remaining A records are not stored in *record_buffer*.</span></span> <span data-ttu-id="d0262-419">Bu, uygulamanın sunucu yanıtında kullanılabilir IP adresi verilerinin bir kısmını veya tamamını almasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="d0262-419">This enables the application to retrieve one, some or all of the available IP address data in the server reply.</span></span>

<span data-ttu-id="d0262-420">\**Record_count* döndürülen kayıt sayısı ile uygulama, IPv4 adresi verilerini *record_buffer* ayrıştırabilirler.</span><span class="sxs-lookup"><span data-stu-id="d0262-420">With the number of A records returned in \**record_count* the application can parse the IPv4 address data from the *record_buffer*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d0262-421">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d0262-421">Input Parameters</span></span>

- <span data-ttu-id="d0262-422">**dns_ptr**: DNS istemcisi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0262-422">**dns_ptr**: Pointer to DNS Client.</span></span>  
- <span data-ttu-id="d0262-423">**host_name_ptr**: IPv4 verilerinin içine ayıklanacağı konuma IPv4 adresi arabellek işaretçisi almak için ana bilgisayar adı işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d0262-423">**host_name_ptr**: Pointer to host name to obtain IPv4 address buffer Pointer to location to extract IPv4 data into</span></span>
- <span data-ttu-id="d0262-424">**Buffer_size**: IPv4 verilerini tutacak arabelleğin boyutu</span><span class="sxs-lookup"><span data-stu-id="d0262-424">**buffer_size**: Size of buffer to hold IPv4 data</span></span>
- <span data-ttu-id="d0262-425">**wait_option**: DNS sunucusu yanıtı alma seçeneğini bekle</span><span class="sxs-lookup"><span data-stu-id="d0262-425">**wait_option**: Wait option to receive DNS Server response</span></span>

### <a name="return-values"></a><span data-ttu-id="d0262-426">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d0262-426">Return Values</span></span>

- <span data-ttu-id="d0262-427">**NX_SUCCESS**: (0x00) IPv4 verileri başarıyla alındı</span><span class="sxs-lookup"><span data-stu-id="d0262-427">**NX_SUCCESS**: (0x00) Successfully obtained IPv4 data</span></span>
- <span data-ttu-id="d0262-428">**NX_DNS_NO_SERVER**: (0xA1) istemci sunucu listesi boş</span><span class="sxs-lookup"><span data-stu-id="d0262-428">**NX_DNS_NO_SERVER**: (0xA1) Client server list is empty</span></span>
- <span data-ttu-id="d0262-429">**NX_DNS_QUERY_FAILED**: (0xA3) GEÇERLI bir DNS yanıtı alınmadı</span><span class="sxs-lookup"><span data-stu-id="d0262-429">**NX_DNS_QUERY_FAILED**: (0xA3) No valid DNS response received</span></span>
- <span data-ttu-id="d0262-430">NX_DNS_PARAM_ERROR: (0xA8) geçersiz giriş parametresi.</span><span class="sxs-lookup"><span data-stu-id="d0262-430">NX_DNS_PARAM_ERROR: (0xA8) Invalid input parameter.</span></span>
- <span data-ttu-id="d0262-431">NX_PTR_ERROR: (0x07) geçersiz IP veya DNS işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d0262-431">NX_PTR_ERROR: (0x07) Invalid IP or DNS pointer</span></span>
- <span data-ttu-id="d0262-432">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="d0262-432">NX_CALLER_ERROR: (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d0262-433">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d0262-433">Allowed From</span></span>

<span data-ttu-id="d0262-434">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d0262-434">Threads</span></span>

### <a name="example"></a><span data-ttu-id="d0262-435">Örnek</span><span class="sxs-lookup"><span data-stu-id="d0262-435">Example</span></span>

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

## <a name="nx_dns_host_by_address_get"></a><span data-ttu-id="d0262-436">nx_dns_host_by_address_get</span><span class="sxs-lookup"><span data-stu-id="d0262-436">nx_dns_host_by_address_get</span></span>

<span data-ttu-id="d0262-437">Bir IP adresinden ana bilgisayar adı ara</span><span class="sxs-lookup"><span data-stu-id="d0262-437">Look up a host name from an IP address</span></span>

### <a name="prototype"></a><span data-ttu-id="d0262-438">Prototype</span><span class="sxs-lookup"><span data-stu-id="d0262-438">Prototype</span></span>

```c
UINT nx_dns_host_by_address_get(NX_DNS *dns_ptr, ULONG ip_address, 
                                ULONG *host_name_ptr, 
                                ULONG max_host_name_size, 
                                ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="d0262-439">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d0262-439">Description</span></span>

<span data-ttu-id="d0262-440">Bu hizmet, uygulama tarafından daha önce belirtilen bir veya daha fazla DNS sunucusundan sağlanan IP adresinin ad çözümlemesini ister.</span><span class="sxs-lookup"><span data-stu-id="d0262-440">This service requests name resolution of the supplied IP address from one or more DNS Servers previously specified by the application.</span></span> <span data-ttu-id="d0262-441">Başarılı olursa, NULL ile sonlandırılmış ana bilgisayar adı *host_name_ptr* tarafından belirtilen dizede döndürülür.</span><span class="sxs-lookup"><span data-stu-id="d0262-441">If successful, the NULL-terminated host name is returned in the string specified by *host_name_ptr*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d0262-442">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d0262-442">Input Parameters</span></span>

- <span data-ttu-id="d0262-443">**dns_ptr**: daha önce oluşturulan DNS örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0262-443">**dns_ptr**: Pointer to previously created DNS instance.</span></span>
- <span data-ttu-id="d0262-444">**ip_address**: bir ada çözülecek IP adresi</span><span class="sxs-lookup"><span data-stu-id="d0262-444">**ip_address**: IP address to resolve into a name</span></span>
- <span data-ttu-id="d0262-445">**host_name_ptr**: konak adı için hedef alan işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d0262-445">**host_name_ptr**: Pointer to destination area for host name</span></span>
- <span data-ttu-id="d0262-446">**max_host_name_size**: konak adı için hedef alanın boyutu</span><span class="sxs-lookup"><span data-stu-id="d0262-446">**max_host_name_size**: Size of destination area for host name</span></span>
- <span data-ttu-id="d0262-447">**wait_option**: hizmetin her bir DNS sorgusu ve sorgu yeniden denendikten sonra bir DNS sunucusu yanıtı için Zamanlayıcı işaretlerini ne kadar bekleyeceğini tanımlar, bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="d0262-447">**wait_option**: Defines how long the service will wait in timer ticks for a DNS server response after each DNS query and query retry The wait options are defined as follows:</span></span>
    - <span data-ttu-id="d0262-448">**zaman aşımı değeri**: (0x00000001-0xfffffffe) sayısal bir değer (1-0XFFFFFFFE) SEÇILIRSE, DNS çözümlemesi beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="d0262-448">**timeout value**: (0x00000001-0xFFFFFFFE) Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the DNS resolution.</span></span>
    - <span data-ttu-id="d0262-449">**TX_WAIT_FOREVER**: (0xffffffff) TX_WAIT_FOREVER seçilmesi çağıran iş PARÇACıĞıNıN bir DNS sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="d0262-449">**TX_WAIT_FOREVER**: (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a DNS server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="d0262-450">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d0262-450">Return Values</span></span>

- <span data-ttu-id="d0262-451">**NX_SUCCESS**: (0x00) başarılı DNS çözümlemesi</span><span class="sxs-lookup"><span data-stu-id="d0262-451">**NX_SUCCESS**: (0x00) Successful DNS resolution</span></span>  
- <span data-ttu-id="d0262-452">**NX_DNS_TIMEOUT**: (0xA2) DNS mutex 'i alma sırasında zaman aşımına uğradı</span><span class="sxs-lookup"><span data-stu-id="d0262-452">**NX_DNS_TIMEOUT**: (0xA2) Timed out on obtaining DNS mutex</span></span>
- <span data-ttu-id="d0262-453">**NX_DNS_NO_SERVER**: (0xA1) DNS sunucusu adresi belirtilmedi</span><span class="sxs-lookup"><span data-stu-id="d0262-453">**NX_DNS_NO_SERVER**: (0xA1) No DNS Server address specified</span></span>
- <span data-ttu-id="d0262-454">**NX_DNS_QUERY_FAILED**: (0xA3) sorguya yanıt almadı</span><span class="sxs-lookup"><span data-stu-id="d0262-454">**NX_DNS_QUERY_FAILED**: (0xA3) Received no response to query</span></span>
- <span data-ttu-id="d0262-455">**NX_DNS_BAD_ADDRESS_ERROR**: (0xa4) null giriş adresi</span><span class="sxs-lookup"><span data-stu-id="d0262-455">**NX_DNS_BAD_ADDRESS_ERROR**: (0xA4) Null input address</span></span>
- <span data-ttu-id="d0262-456">**NX_DNS_INVALID_ADDRESS_TYPE**: (0Xb2) geçersiz adres türüne (örneğin, IPv6) dizin noktaları</span><span class="sxs-lookup"><span data-stu-id="d0262-456">**NX_DNS_INVALID_ADDRESS_TYPE**: (0xB2) Index points to invalid address type (e.g. IPv6)</span></span>
- <span data-ttu-id="d0262-457">**NX_DNS_PARAM_ERROR**: (0Xa8) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="d0262-457">**NX_DNS_PARAM_ERROR**: (0xA8) Invalid non pointer input</span></span>
- <span data-ttu-id="d0262-458">NX_PTR_ERROR: (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="d0262-458">NX_PTR_ERROR: (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="d0262-459">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="d0262-459">NX_CALLER_ERROR: (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d0262-460">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d0262-460">Allowed From</span></span>

<span data-ttu-id="d0262-461">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d0262-461">Threads</span></span>

### <a name="example"></a><span data-ttu-id="d0262-462">Örnek</span><span class="sxs-lookup"><span data-stu-id="d0262-462">Example</span></span>

```c
#define BUFFER_SIZE   200

UCHAR   resolved_name[200];

/* Get the name associated with IP address 192.2.2.10.  */
status =  nx_dns_host_by_address_get(&my_dns, IP_ADDRESS(192.2.2.10),
                                     &resolved_name[0], BUFFER_SIZE, 450);

/* If status is NX_SUCCESS the name associated with the IP address
   can be found in the resolved_name variable.  */

```

## <a name="nx_dns_host_by_name_get"></a><span data-ttu-id="d0262-463">nx_dns_host_by_name_get</span><span class="sxs-lookup"><span data-stu-id="d0262-463">nx_dns_host_by_name_get</span></span>

<span data-ttu-id="d0262-464">Ana bilgisayar adından bir IP adresi ara</span><span class="sxs-lookup"><span data-stu-id="d0262-464">Look up an IP address from the host name</span></span>

### <a name="prototype"></a><span data-ttu-id="d0262-465">Prototype</span><span class="sxs-lookup"><span data-stu-id="d0262-465">Prototype</span></span>

```c
UINT nx_dns_host_by_name_get(NX_DNS *dns_ptr, UCHAR *host_name, 
                             ULONG *host_address_ptr, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="d0262-466">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d0262-466">Description</span></span>

<span data-ttu-id="d0262-467">Bu hizmet, uygulama tarafından daha önce belirtilen bir veya daha fazla DNS sunucusundan *host_name* tarafından işaret edilen ad çözümlemesini ister.</span><span class="sxs-lookup"><span data-stu-id="d0262-467">This service requests name resolution of the supplied name, pointed to by *host_name*, from one or more DNS Servers previously specified by the application.</span></span> <span data-ttu-id="d0262-468">Başarılı olursa, ilişkili IP adresi *host_address_ptr* tarafından işaret edilen hedefte döndürülür.</span><span class="sxs-lookup"><span data-stu-id="d0262-468">If successful, the associated IP address is returned in the destination pointed to by *host_address_ptr*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d0262-469">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d0262-469">Input Parameters</span></span>

- <span data-ttu-id="d0262-470">**dns_ptr**: daha önce oluşturulan DNS örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0262-470">**dns_ptr**: Pointer to previously created DNS instance.</span></span>
- <span data-ttu-id="d0262-471">**host_name**: Ana bilgisayar adı işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d0262-471">**host_name**: Pointer to host name</span></span>
- <span data-ttu-id="d0262-472">**host_address_ptr**: DNS ana bilgisayar IP adresi işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d0262-472">**host_address_ptr**: Pointer to DNS host IP address</span></span>
- <span data-ttu-id="d0262-473">**wait_option**: hizmetin DNS çözümlemesi için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="d0262-473">**wait_option**: Defines how long the service will wait for the DNS resolution.</span></span> <span data-ttu-id="d0262-474">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="d0262-474">The wait options are defined as follows:</span></span>
    - <span data-ttu-id="d0262-475">**zaman aşımı değeri**: (0x00000001-0xfffffffe) sayısal değer (1-0XFFFFFFFE) SEÇILDIĞINDE, DNS çözümlemesi beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="d0262-475">**timeout value**: (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the DNS resolution.</span></span>
    - <span data-ttu-id="d0262-476">**TX_WAIT_FOREVER**: (0xffffffff) TX_WAIT_FOREVER seçilmesi çağıran iş PARÇACıĞıNıN bir DNS sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="d0262-476">**TX_WAIT_FOREVER**: (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a DNS server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="d0262-477">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d0262-477">Return Values</span></span>

- <span data-ttu-id="d0262-478">**NX_SUCCESS**: (0x00) başarılı DNS çözümlemesi.</span><span class="sxs-lookup"><span data-stu-id="d0262-478">**NX_SUCCESS**: (0x00) Successful DNS resolution.</span></span>
- <span data-ttu-id="d0262-479">**NX_DNS_NO_SERVER**: (0xA1) DNS sunucusu adresi belirtilmedi</span><span class="sxs-lookup"><span data-stu-id="d0262-479">**NX_DNS_NO_SERVER**: (0xA1) No DNS Server address specified</span></span>
- <span data-ttu-id="d0262-480">**NX_DNS_QUERY_FAILED**: (0xA3) sorguya yanıt almadı</span><span class="sxs-lookup"><span data-stu-id="d0262-480">**NX_DNS_QUERY_FAILED**: (0xA3) Received no response to query</span></span>
- <span data-ttu-id="d0262-481">NX_DNS_PARAM_ERROR: (0xA8) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="d0262-481">NX_DNS_PARAM_ERROR: (0xA8) Invalid non pointer input</span></span>
- <span data-ttu-id="d0262-482">NX_PTR_ERROR: (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="d0262-482">NX_PTR_ERROR: (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="d0262-483">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="d0262-483">NX_CALLER_ERROR: (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d0262-484">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d0262-484">Allowed From</span></span>

<span data-ttu-id="d0262-485">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d0262-485">Threads</span></span>

### <a name="example"></a><span data-ttu-id="d0262-486">Örnek</span><span class="sxs-lookup"><span data-stu-id="d0262-486">Example</span></span>
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

## <a name="nx_dns_host_text_get"></a><span data-ttu-id="d0262-487">nx_dns_host_text_get</span><span class="sxs-lookup"><span data-stu-id="d0262-487">nx_dns_host_text_get</span></span>

<span data-ttu-id="d0262-488">Giriş etki alanı adı için metin dizesini arayın</span><span class="sxs-lookup"><span data-stu-id="d0262-488">Look up the text string for the input domain name</span></span>

### <a name="prototype"></a><span data-ttu-id="d0262-489">Prototype</span><span class="sxs-lookup"><span data-stu-id="d0262-489">Prototype</span></span>

```c
UINT nx_dns_host_text_get(NX_DNS *dns_ptr, UCHAR *host_name, 
                          UCHAR *record_buffer, 
                          UINT buffer_size, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="d0262-490">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d0262-490">Description</span></span>

<span data-ttu-id="d0262-491">Bu hizmet, rastgele dize verileri elde etmek için belirtilen etki alanı adı ve arabellekle TXT türünde bir sorgu gönderir.</span><span class="sxs-lookup"><span data-stu-id="d0262-491">This service sends a query of type TXT with the specified domain name and buffer to obtain the arbitrary string data.</span></span>

<span data-ttu-id="d0262-492">DNS Istemcisi, DNS sunucusu yanıtındaki TXT kaydındaki metin dizesini *record_buffer* bellek konumuna kopyalar.</span><span class="sxs-lookup"><span data-stu-id="d0262-492">The DNS Client copies the text string in the TXT record in the DNS Server response into the *record_buffer* memory location.</span></span> 

>[!NOTE]
><span data-ttu-id="d0262-493">*Record_buffer* verileri almak için 4 baytlık hizalı olması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="d0262-493">The *record_buffer* does not need to be 4-byte aligned to receive the data.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d0262-494">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d0262-494">Input Parameters</span></span>

- <span data-ttu-id="d0262-495">**dns_ptr**: DNS istemcisi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0262-495">**dns_ptr**: Pointer to DNS Client.</span></span>  
- <span data-ttu-id="d0262-496">**host_name**: arama yapılacak ana bilgisayarın adı işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d0262-496">**host_name**: Pointer to name of host to search on</span></span>
- <span data-ttu-id="d0262-497">**record_buffer**: txt verilerinin ayıklanacağı konum işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d0262-497">**record_buffer**: Pointer to location to extract TXT data into</span></span>
- <span data-ttu-id="d0262-498">**Buffer_size**: txt verilerini tutan arabelleğin boyutu</span><span class="sxs-lookup"><span data-stu-id="d0262-498">**buffer_size**: Size of buffer to hold TXT data</span></span>
- <span data-ttu-id="d0262-499">**wait_option**: DNS sunucusu yanıtı alma seçeneğini bekle</span><span class="sxs-lookup"><span data-stu-id="d0262-499">**wait_option**: Wait option to receive DNS Server response</span></span>

### <a name="return-values"></a><span data-ttu-id="d0262-500">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d0262-500">Return Values</span></span>

- <span data-ttu-id="d0262-501">**NX_SUCCESS**: (0x00) başarılı bir txt dizesi alındı</span><span class="sxs-lookup"><span data-stu-id="d0262-501">**NX_SUCCESS**: (0x00) Successfully TXT string obtained</span></span>
- <span data-ttu-id="d0262-502">**NX_DNS_NO_SERVER**: (0xA1) istemci sunucu listesi boş</span><span class="sxs-lookup"><span data-stu-id="d0262-502">**NX_DNS_NO_SERVER**: (0xA1) Client server list is empty</span></span>
- <span data-ttu-id="d0262-503">**NX_DNS_QUERY_FAILED**: (0xA3) GEÇERLI bir DNS yanıtı alınmadı</span><span class="sxs-lookup"><span data-stu-id="d0262-503">**NX_DNS_QUERY_FAILED**: (0xA3) No valid DNS response received</span></span>
- <span data-ttu-id="d0262-504">NX_PTR_ERROR: (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="d0262-504">NX_PTR_ERROR: (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="d0262-505">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="d0262-505">NX_CALLER_ERROR: (0x11) Invalid caller of this service</span></span>
- <span data-ttu-id="d0262-506">NX_DNS_PARAM_ERROR: (0xA8) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="d0262-506">NX_DNS_PARAM_ERROR: (0xA8) Invalid non pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d0262-507">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d0262-507">Allowed From</span></span>

<span data-ttu-id="d0262-508">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d0262-508">Threads</span></span>

### <a name="example"></a><span data-ttu-id="d0262-509">Örnek</span><span class="sxs-lookup"><span data-stu-id="d0262-509">Example</span></span>

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

## <a name="nx_dns_packet_pool_set"></a><span data-ttu-id="d0262-510">nx_dns_packet_pool_set</span><span class="sxs-lookup"><span data-stu-id="d0262-510">nx_dns_packet_pool_set</span></span>

<span data-ttu-id="d0262-511">DNS Istemcisi paket havuzunu ayarlama</span><span class="sxs-lookup"><span data-stu-id="d0262-511">Set the DNS Client packet pool</span></span>

### <a name="prototype"></a><span data-ttu-id="d0262-512">Prototype</span><span class="sxs-lookup"><span data-stu-id="d0262-512">Prototype</span></span>

```c
UINT nx_dns_packet_pool_set(NX_DNS *dns_ptr, NX_PACKET_POOL *pool_ptr);
```
### <a name="description"></a><span data-ttu-id="d0262-513">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d0262-513">Description</span></span>

<span data-ttu-id="d0262-514">Bu hizmet, daha önce oluşturulmuş bir paket havuzunu DNS **istemcisi** paket havuzu olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d0262-514">This service sets a previously created packet pool as the DNS **Client** packet pool.</span></span> <span data-ttu-id="d0262-515">DNS Istemcisi, DNS sorguları göndermek için bu paket havuzunu kullanır, bu nedenle paket yükü Ethernet çerçevesini, IP ve UDP üst bilgilerini içeren ve *nx_dns. h* içinde tanımlanan NX_DNS_PACKET_PAYLOAD_UNALIGNED daha az olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="d0262-515">The DNS Client will use this packet pool to send DNS queries, so the packet payload should not be less than NX_DNS_PACKET_PAYLOAD_UNALIGNED which includes the Ethernet frame, IP and UDP headers and is defined in *nx_dns.h*.</span></span>
 
>[!NOTE]
><span data-ttu-id="d0262-516">DNS Istemcisi silindiğinde, paket havuzu onunla silinmez ve artık ihtiyaç duyulmuyorsa, paket havuzunu silmek uygulamanın sorumluluğundadır.</span><span class="sxs-lookup"><span data-stu-id="d0262-516">When the DNS Client is deleted, the packet pool is not deleted with it and it is the responsibility of the application to delete the packet pool when it no longer needs it.</span></span>

>[!NOTE]
><span data-ttu-id="d0262-517">Bu hizmet yalnızca yapılandırma seçeneği NX_DNS_CLIENT_USER_CREATE_PACKET_POOL *nx_dns. h* içinde tanımlanmışsa kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="d0262-517">This service is only available if the configuration option NX_DNS_CLIENT_USER_CREATE_PACKET_POOL is defined in *nx_dns.h*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d0262-518">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d0262-518">Input Parameters</span></span>

- <span data-ttu-id="d0262-519">**dns_ptr**: daha önce oluşturulan DNS **istemci** örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0262-519">**dns_ptr**: Pointer to previously created DNS **Client** instance.</span></span>
- <span data-ttu-id="d0262-520">**pool_ptr**: daha önce oluşturulmuş olan paket havuzuna yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="d0262-520">**pool_ptr**: Pointer to previously created packet pool</span></span>

### <a name="return-values"></a><span data-ttu-id="d0262-521">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d0262-521">Return Values</span></span>

- <span data-ttu-id="d0262-522">**NX_SUCCESS**: (0x00) başarılı tamamlama.</span><span class="sxs-lookup"><span data-stu-id="d0262-522">**NX_SUCCESS**: (0x00) Successful completion.</span></span>
- <span data-ttu-id="d0262-523">Bu seçenek için **NX_NOT_ENABLED**: (0x14) istemci yapılandırılmadı</span><span class="sxs-lookup"><span data-stu-id="d0262-523">**NX_NOT_ENABLED**: (0x14) Client not configured for this option</span></span>
- <span data-ttu-id="d0262-524">NX_PTR_ERROR: (0x07) geçersiz IP veya DNS **istemcisi** işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0262-524">NX_PTR_ERROR: (0x07) Invalid IP or DNS **Client** pointer.</span></span>
- <span data-ttu-id="d0262-525">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="d0262-525">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d0262-526">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d0262-526">Allowed From</span></span>

<span data-ttu-id="d0262-527">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d0262-527">Threads</span></span>

### <a name="example"></a><span data-ttu-id="d0262-528">Örnek</span><span class="sxs-lookup"><span data-stu-id="d0262-528">Example</span></span>
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

## <a name="nx_dns_server_add"></a><span data-ttu-id="d0262-529">nx_dns_server_add</span><span class="sxs-lookup"><span data-stu-id="d0262-529">nx_dns_server_add</span></span>

<span data-ttu-id="d0262-530">DNS sunucusu IP adresi ekle</span><span class="sxs-lookup"><span data-stu-id="d0262-530">Add DNS Server IP Address</span></span>

### <a name="prototype"></a><span data-ttu-id="d0262-531">Prototype</span><span class="sxs-lookup"><span data-stu-id="d0262-531">Prototype</span></span>

```c
UINT nx_dns_server_add(NX_DNS *dns_ptr, ULONG server_address);
```

### <a name="description"></a><span data-ttu-id="d0262-532">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d0262-532">Description</span></span>

<span data-ttu-id="d0262-533">Bu hizmet, sunucu listesine bir IPv4 DNS sunucusu ekler.</span><span class="sxs-lookup"><span data-stu-id="d0262-533">This service adds an IPv4 DNS Server to the server list.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d0262-534">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d0262-534">Input Parameters</span></span>

- <span data-ttu-id="d0262-535">**dns_ptr**: DNS Denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0262-535">**dns_ptr**: Pointer to DNS control block.</span></span>  
- <span data-ttu-id="d0262-536">**server_address**: DNS sunucusunun IP adresi</span><span class="sxs-lookup"><span data-stu-id="d0262-536">**server_address**: IP address of DNS Server</span></span>

### <a name="return-values"></a><span data-ttu-id="d0262-537">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d0262-537">Return Values</span></span>

- <span data-ttu-id="d0262-538">**NX_SUCCESS**: (0x00) sunucu başarıyla eklendi</span><span class="sxs-lookup"><span data-stu-id="d0262-538">**NX_SUCCESS**: (0x00) Server successfully added</span></span>
- <span data-ttu-id="d0262-539">**NX_DNS_DUPLICATE_ENTRY** veya **NX_NO_MORE_ENTRIES**: (0x17) daha fazla DNS sunucusu izin verilmiyor (liste dolu)</span><span class="sxs-lookup"><span data-stu-id="d0262-539">**NX_DNS_DUPLICATE_ENTRY** or **NX_NO_MORE_ENTRIES**: (0x17) No more DNS Servers Allowed (list is full)</span></span>
- <span data-ttu-id="d0262-540">**NX_DNS_PARAM_ERROR**: (0Xa8) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="d0262-540">**NX_DNS_PARAM_ERROR**: (0xA8) Invalid non pointer input</span></span>
- <span data-ttu-id="d0262-541">NX_PTR_ERROR: (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="d0262-541">NX_PTR_ERROR: (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="d0262-542">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="d0262-542">NX_CALLER_ERROR: (0x11) Invalid caller of this service</span></span>
- <span data-ttu-id="d0262-543">NX_DNS_BAD_ADDRESS_ERROR: (0xA4) null sunucu adresi girişi</span><span class="sxs-lookup"><span data-stu-id="d0262-543">NX_DNS_BAD_ADDRESS_ERROR: (0xA4) Null server address input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d0262-544">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d0262-544">Allowed From</span></span>

<span data-ttu-id="d0262-545">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d0262-545">Threads</span></span>

### <a name="example"></a><span data-ttu-id="d0262-546">Örnek</span><span class="sxs-lookup"><span data-stu-id="d0262-546">Example</span></span>

```c
/* Add a DNS Server at IP address 202.2.2.13.  */
status =  nx_dns_server_add(&my_dns, IP_ADDRESS(202,2,2,13));

/* If status is NX_SUCCESS a DNS Server was successfully added.  */
```

## <a name="nx_dns_server_get"></a><span data-ttu-id="d0262-547">nx_dns_server_get</span><span class="sxs-lookup"><span data-stu-id="d0262-547">nx_dns_server_get</span></span>

<span data-ttu-id="d0262-548">Istemci listesinden bir IPv4 DNS sunucusu döndürme</span><span class="sxs-lookup"><span data-stu-id="d0262-548">Return an IPv4 DNS Server from the Client list</span></span>

### <a name="prototype"></a><span data-ttu-id="d0262-549">Prototype</span><span class="sxs-lookup"><span data-stu-id="d0262-549">Prototype</span></span>

```c
UINT nx_dns_server_get(NX_DNS *dns_ptr, UINT index, 
                       ULONG *dns_server_address);
```

### <a name="description"></a><span data-ttu-id="d0262-550">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d0262-550">Description</span></span>

<span data-ttu-id="d0262-551">Bu hizmet, belirtilen dizindeki sunucu listesinden IPv4 DNS sunucusu adresini döndürür.</span><span class="sxs-lookup"><span data-stu-id="d0262-551">This service returns the IPv4 DNS Server address from the server list at the specified index.</span></span> <span data-ttu-id="d0262-552">Dizinin sıfır tabanlı olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d0262-552">Note that the index is zero based.</span></span> <span data-ttu-id="d0262-553">Giriş dizini DNS Istemci listesinin boyutunu aşarsa bir hata döndürülür.</span><span class="sxs-lookup"><span data-stu-id="d0262-553">If the input index exceeds the size of the DNS Client list, an error is returned.</span></span> <span data-ttu-id="d0262-554">*Nx_dns_get_serverlist_size* hizmeti Ilk olarak ISTEMCI listesindeki DNS sunucularının sayısını elde edebilir.</span><span class="sxs-lookup"><span data-stu-id="d0262-554">The *nx_dns_get_serverlist_size* service may be called first obtain the number of DNS servers in the Client list.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d0262-555">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d0262-555">Input Parameters</span></span>

- <span data-ttu-id="d0262-556">**dns_ptr**: DNS denetim bloğu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d0262-556">**dns_ptr**: Pointer to DNS control block</span></span>  
- <span data-ttu-id="d0262-557">**Dizin**: DNS istemcisinin sunucu listesini dizine ekleyin</span><span class="sxs-lookup"><span data-stu-id="d0262-557">**index**: Index into DNS Client’s list of servers</span></span>
- <span data-ttu-id="d0262-558">**dns_server_address**: DNS sunucusunun IP adresi işaretçisi</span><span class="sxs-lookup"><span data-stu-id="d0262-558">**dns_server_address**: Pointer to IP address of DNS Server</span></span>

### <a name="return-values"></a><span data-ttu-id="d0262-559">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d0262-559">Return Values</span></span>

- <span data-ttu-id="d0262-560">**NX_SUCCESS**: (0x00) başarılı sunucu döndürüldü</span><span class="sxs-lookup"><span data-stu-id="d0262-560">**NX_SUCCESS**: (0x00) Successful server returned</span></span>
- <span data-ttu-id="d0262-561">**NX_DNS_SERVER_NOT_FOUND**: (0xA9) boş yuvaya yönelik dizin noktaları</span><span class="sxs-lookup"><span data-stu-id="d0262-561">**NX_DNS_SERVER_NOT_FOUND**: (0xA9) Index points to empty slot</span></span>
- <span data-ttu-id="d0262-562">**NX_DNS_BAD_ADDRESS_ERROR**: (0xa4) null adrese yönelik dizin noktaları</span><span class="sxs-lookup"><span data-stu-id="d0262-562">**NX_DNS_BAD_ADDRESS_ERROR**: (0xA4) Index points to Null address</span></span>
- <span data-ttu-id="d0262-563">**NX_DNS_PARAM_ERROR**: (0Xa8) dizin, listenin boyutunu aşıyor</span><span class="sxs-lookup"><span data-stu-id="d0262-563">**NX_DNS_PARAM_ERROR**: (0xA8) Index exceeds size of list</span></span>
- <span data-ttu-id="d0262-564">NX_PTR_ERROR: (0x07) geçersiz IP veya DNS işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0262-564">NX_PTR_ERROR: (0x07) Invalid IP or DNS pointer.</span></span>
- <span data-ttu-id="d0262-565">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="d0262-565">NX_CALLER_ERROR: (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d0262-566">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d0262-566">Allowed From</span></span>

<span data-ttu-id="d0262-567">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d0262-567">Threads</span></span>

### <a name="example"></a><span data-ttu-id="d0262-568">Örnek</span><span class="sxs-lookup"><span data-stu-id="d0262-568">Example</span></span>

```c
ULONG     my_server_address;

/* Get the DNS Server at index 5 (zero based) into the Client list.  */
status =  nx_dns_server_get(&my_dns, 5, &my_server_addres);

/* If status is NX_SUCCESS a DNS Server was successfully
   returned.  */
```

## <a name="nx_dns_server_remove"></a><span data-ttu-id="d0262-569">nx_dns_server_remove</span><span class="sxs-lookup"><span data-stu-id="d0262-569">nx_dns_server_remove</span></span>

<span data-ttu-id="d0262-570">Bir IPv4 DNS sunucusunu Istemci listesinden kaldır</span><span class="sxs-lookup"><span data-stu-id="d0262-570">Remove an IPv4 DNS Server from the Client list</span></span>

### <a name="prototype"></a><span data-ttu-id="d0262-571">Prototype</span><span class="sxs-lookup"><span data-stu-id="d0262-571">Prototype</span></span>

```c
UINT nx_dns_server_remove(NX_DNS *dns_ptr, ULONG server_address);
```

### <a name="description"></a><span data-ttu-id="d0262-572">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d0262-572">Description</span></span>

<span data-ttu-id="d0262-573">Bu hizmet, bir IPv4 DNS sunucusunu Istemci listesinden kaldırır.</span><span class="sxs-lookup"><span data-stu-id="d0262-573">This service removes an IPv4 DNS Server from the Client list.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d0262-574">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d0262-574">Input Parameters</span></span>

- <span data-ttu-id="d0262-575">**dns_ptr**: DNS Denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0262-575">**dns_ptr**: Pointer to DNS control block.</span></span>
- <span data-ttu-id="d0262-576">**server_address**: DNS sunucusunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="d0262-576">**server_address**: IP address of DNS Server.</span></span>

### <a name="return-values"></a><span data-ttu-id="d0262-577">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d0262-577">Return Values</span></span>

- <span data-ttu-id="d0262-578">**NX_SUCCESS**: (0x00) DNS sunucusu başarıyla kaldırıldı</span><span class="sxs-lookup"><span data-stu-id="d0262-578">**NX_SUCCESS**: (0x00) DNS Server successfully removed</span></span>
- <span data-ttu-id="d0262-579">**NX_DNS_SERVER_NOT_FOUND**: (0xA9) sunucu istemci listesinde değil</span><span class="sxs-lookup"><span data-stu-id="d0262-579">**NX_DNS_SERVER_NOT_FOUND**: (0xA9) Server not in Client list</span></span>
- <span data-ttu-id="d0262-580">**NX_DNS_BAD_ADDRESS_ERROR**: (0xa4) null sunucu adresi girişi</span><span class="sxs-lookup"><span data-stu-id="d0262-580">**NX_DNS_BAD_ADDRESS_ERROR**: (0xA4) Null server address input</span></span>
- <span data-ttu-id="d0262-581">NX_PTR_ERROR: (0x07) geçersiz IP veya DNS işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0262-581">NX_PTR_ERROR: (0x07) Invalid IP or DNS pointer.</span></span>
- <span data-ttu-id="d0262-582">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="d0262-582">NX_CALLER_ERROR: (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d0262-583">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d0262-583">Allowed From</span></span>

<span data-ttu-id="d0262-584">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d0262-584">Threads</span></span>

### <a name="example"></a><span data-ttu-id="d0262-585">Örnek</span><span class="sxs-lookup"><span data-stu-id="d0262-585">Example</span></span>

```c
/* Remove the DNS Server at IP address is 202.2.2.13.  */
status =  nx_dns_server_remove(&my_dns, IP_ADDRESS(202,2,2,13));

/* If status is NX_SUCCESS a DNS Server was successfully
   removed.  */
```

## <a name="nx_dns_server_remove_all"></a><span data-ttu-id="d0262-586">nx_dns_server_remove_all</span><span class="sxs-lookup"><span data-stu-id="d0262-586">nx_dns_server_remove_all</span></span>

<span data-ttu-id="d0262-587">Tüm DNS sunucularını Istemci listesinden kaldır</span><span class="sxs-lookup"><span data-stu-id="d0262-587">Remove all DNS Servers from the Client list</span></span>

### <a name="prototype"></a><span data-ttu-id="d0262-588">Prototype</span><span class="sxs-lookup"><span data-stu-id="d0262-588">Prototype</span></span>

```c
UINT nx_dns_server_remove_all(NX_DNS *dns_ptr);
```

### <a name="description"></a><span data-ttu-id="d0262-589">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d0262-589">Description</span></span>

<span data-ttu-id="d0262-590">Bu hizmet, tüm DNS sunucularını Istemci listesinden kaldırır.</span><span class="sxs-lookup"><span data-stu-id="d0262-590">This service removes all DNS Servers from the Client list.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d0262-591">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="d0262-591">Input Parameters</span></span>

- <span data-ttu-id="d0262-592">**dns_ptr**: DNS Denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0262-592">**dns_ptr**: Pointer to DNS control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="d0262-593">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="d0262-593">Return Values</span></span>

- <span data-ttu-id="d0262-594">**NX_SUCCESS**: (0x00) DNS sunucuları başarıyla kaldırıldı</span><span class="sxs-lookup"><span data-stu-id="d0262-594">**NX_SUCCESS**: (0x00) DNS Servers successfully removed</span></span>
- <span data-ttu-id="d0262-595">**NX_DNS_ERROR**: (0xa0) koruma mutex 'i alınamıyor</span><span class="sxs-lookup"><span data-stu-id="d0262-595">**NX_DNS_ERROR**: (0xA0) Unable to obtain protection mutex</span></span>
- <span data-ttu-id="d0262-596">NX_PTR_ERROR: (0x07) geçersiz IP veya DNS işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0262-596">NX_PTR_ERROR: (0x07) Invalid IP or DNS pointer.</span></span>
- <span data-ttu-id="d0262-597">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="d0262-597">NX_CALLER_ERROR: (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d0262-598">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="d0262-598">Allowed From</span></span>

<span data-ttu-id="d0262-599">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="d0262-599">Threads</span></span>

### <a name="example"></a><span data-ttu-id="d0262-600">Örnek</span><span class="sxs-lookup"><span data-stu-id="d0262-600">Example</span></span>

```c

/* Remove all DNS Servers from the Client list.  */
status =  nx_dns_server_remove_all(&my_dns);

/* If status is NX_SUCCESS all DNS Servers were successfully removed.  */
```