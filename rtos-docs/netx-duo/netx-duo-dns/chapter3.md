---
title: Bölüm 3-Azure RTOS NetX Duo DNS Istemci hizmetlerinin açıklaması
description: Bu bölüm, tüm Azure RTOS NetX Duo DNS hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 9634adab3944c29f64d26dd688b5053dc1bd9bcb
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826015"
---
# <a name="chapter-3---description-of-azure-rtos-netx-duo-dns-client-services"></a><span data-ttu-id="12058-103">Bölüm 3-Azure RTOS NetX Duo DNS Istemci hizmetlerinin açıklaması</span><span class="sxs-lookup"><span data-stu-id="12058-103">Chapter 3 - Description of Azure RTOS NetX Duo DNS Client Services</span></span>

<span data-ttu-id="12058-104">Bu bölüm, tüm Azure RTOS NetX DNS hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="12058-104">This chapter contains a description of all Azure RTOS NetX DNS services (listed below) in alphabetic order.</span></span>

<span data-ttu-id="12058-105">Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_DISABLE_ERROR_CHECKING** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="12058-105">In the “Return Values” section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

- <span data-ttu-id="12058-106">**nx_dns_authority_zone_start_get** *belirtilen ana bilgisayar adıyla ilişkili bir yetkili bölgesinin başlangıcına bakmak*</span><span class="sxs-lookup"><span data-stu-id="12058-106">**nx_dns_authority_zone_start_get** *Look up the start of a zone of authority associated with the specified host name*</span></span>

- <span data-ttu-id="12058-107">**nx_dns_cache_initialize** *bir DNS önbelleği başlatın.*</span><span class="sxs-lookup"><span data-stu-id="12058-107">**nx_dns_cache_initialize** *Initialize a DNS Cache.*</span></span>

- <span data-ttu-id="12058-108"> *önbellek tam bildirim işlevini nx_dns_cache_notify_clear temizleyin.*</span><span class="sxs-lookup"><span data-stu-id="12058-108">**nx_dns_cache_notify_clear** *Clear the cache full notify function.*</span></span>

- <span data-ttu-id="12058-109">**nx_dns_cache_notify_set** *Cache Full NOTIFY işlevini ayarlayın.*</span><span class="sxs-lookup"><span data-stu-id="12058-109">**nx_dns_cache_notify_set** *Set the cache full notify function.*</span></span>

- <span data-ttu-id="12058-110"> *giriş etki alanı adı diğer adı için kurallı etki alanı adını aramak* nx_dns_cname_get</span><span class="sxs-lookup"><span data-stu-id="12058-110">**nx_dns_cname_get** *Look up the canonical domain name for the input domain name alias*</span></span>

- <span data-ttu-id="12058-111">**NX_DNS_CREATE** *DNS istemci örneği oluşturma*</span><span class="sxs-lookup"><span data-stu-id="12058-111">**nx_dns_create** *Create a DNS Client instance*</span></span>

- <span data-ttu-id="12058-112">**nx_dns_delete** *bir DNS istemci örneğini silme*</span><span class="sxs-lookup"><span data-stu-id="12058-112">**nx_dns_delete** *Delete a DNS Client instance*</span></span>

- <span data-ttu-id="12058-113">**nx_dns_domain_name_server_get** *giriş etki alanı bölgesi için yetkili ad sunucularını arama*</span><span class="sxs-lookup"><span data-stu-id="12058-113">**nx_dns_domain_name_server_get** *Look up the authoritative name servers for the input domain zone*</span></span>

- <span data-ttu-id="12058-114">**nx_dns_domain_mail_exchange_get** *belirtilen ana bilgisayar adının ilişkili olduğu posta değişimine bakmak.*</span><span class="sxs-lookup"><span data-stu-id="12058-114">**nx_dns_domain_mail_exchange_get** *Look up the mail exchange associated the specified host name.*</span></span>

- <span data-ttu-id="12058-115">**nx_dns_domain_service_get** *belirtilen ana bilgisayar adıyla ilişkili hizmet (ler) i aramak*</span><span class="sxs-lookup"><span data-stu-id="12058-115">**nx_dns_domain_service_get** *Look up the service(s) associated with the specified host name*</span></span>

- <span data-ttu-id="12058-116">**NX_DNS_GET_SERVERLIST_SIZE** *DNS istemci sunucusu listesinin boyutunu döndürür*</span><span class="sxs-lookup"><span data-stu-id="12058-116">**nx_dns_get_serverlist_size** *Return the size of the DNS Client server list*</span></span>

- <span data-ttu-id="12058-117">**nx_dns_info_by_name_get** *dönüş IP adresi, giriş ana bilgisayar adı sorgulama bağlantı noktası*</span><span class="sxs-lookup"><span data-stu-id="12058-117">**nx_dns_info_by_name_get** *Return IP address, port querying on input host name*</span></span>

- <span data-ttu-id="12058-118">**nx_dns_ipv4_address_by_name_get** *belirtilen ana bilgisayar adından IPv4 adresini aramak için*</span><span class="sxs-lookup"><span data-stu-id="12058-118">**nx_dns_ipv4_address_by_name_get** *Look up the IPv4 address from the specified host name*</span></span>

- <span data-ttu-id="12058-119">**nxd_dns_ipv6_address_by_name_get** *belirtilen ana bilgisayar adından IPv6 adresini aramak için*</span><span class="sxs-lookup"><span data-stu-id="12058-119">**nxd_dns_ipv6_address_by_name_get** *Look up the IPv6 address from the specified host name*</span></span>

- <span data-ttu-id="12058-120"> *NXD_DNS_HOST_BY_ADDRESS_GET, belirtilen IP adresinden bir ana bilgisayar adı aramak için nx_dns_host_by_address_get sarmalayıcı Işlevi (yalnızca IPv4 adreslerini destekler)*</span><span class="sxs-lookup"><span data-stu-id="12058-120">**nx_dns_host_by_address_get** *Wrapper function for nxd_dns_host_by_address_get to look up a host name from a specified IP address (supports only IPv4 addresses)*</span></span>

- <span data-ttu-id="12058-121">**nxd_dns_host_by_address_get** *giriş ana BILGISAYAR adından bir IP adresi arar (hem IPv4 hem de IPv6 adreslerini destekler)*</span><span class="sxs-lookup"><span data-stu-id="12058-121">**nxd_dns_host_by_address_get** *Look up an IP address from the input host name (supports both IPv4 and IPv6 addresses)*</span></span>

- <span data-ttu-id="12058-122"> *nxd_dns_host_by_address_get, belirtilen adresten bir ana bilgisayar adı aramak için nx_dns_host_by_name_get sarmalayıcı Işlevi (yalnızca IPv4 adreslerini destekler)*</span><span class="sxs-lookup"><span data-stu-id="12058-122">**nx_dns_host_by_name_get** *Wrapper function for nxd_dns_host_by_address_get to look up a host name from the specified address (supports only IPv4 addresses)*</span></span>

- <span data-ttu-id="12058-123">**nxd_dns_host_by_name_get** *giriş ana BILGISAYAR adından bir IP adresi arar (hem IPv4 hem de IPv6 adreslerini destekler)*</span><span class="sxs-lookup"><span data-stu-id="12058-123">**nxd_dns_host_by_name_get** *Look up an IP address from the input host name (supports both IPv4 and IPv6 addresses)*</span></span>

- <span data-ttu-id="12058-124"> *giriş etki alanı adı için metin verilerini arama* nx_dns_host_text_get</span><span class="sxs-lookup"><span data-stu-id="12058-124">**nx_dns_host_text_get** *Look up the text data for the input domain name*</span></span>

- <span data-ttu-id="12058-125"> *DNS istemcisi paket havuzunu nx_dns_packet_pool_set ayarlama*</span><span class="sxs-lookup"><span data-stu-id="12058-125">**nx_dns_packet_pool_set** *Set the DNS Client packet pool*</span></span>

- <span data-ttu-id="12058-126">nxd_dns_server_add için **nx_dns_server_add** *sarmalayıcı işlevi* *, belirtilen adresteki bir DNS sunucusunu Istemci listesine ekleme (yalnızca IPv4 'ü destekler)*</span><span class="sxs-lookup"><span data-stu-id="12058-126">**nx_dns_server_add** *Wrapper function for* nxd_dns_server_add *to add a DNS Server at the specified address to the Client list (supports only IPv4)*</span></span>

- <span data-ttu-id="12058-127"> *istemci sunucu listesine belirtilen IP adresinin bir dns sunucusunu eklemek Nxd_dns_server_add (hem IPv4 hem de IPv6 adreslerini destekler)*</span><span class="sxs-lookup"><span data-stu-id="12058-127">**nxd_dns_server_add** *Add a DNS Server of the specified IP address to the Client server list (supports both IPv4 or IPv6 addresses)*</span></span>

- <span data-ttu-id="12058-128">**Nx_dns_server_get** *Istemci listesinde DNS sunucusunu döndürür (yalnızca IPv4 adreslerini destekler)*</span><span class="sxs-lookup"><span data-stu-id="12058-128">**nx_dns_server_get** *Return the DNS Server in the Client list (supports only IPv4 addresses)*</span></span>

- <span data-ttu-id="12058-129">**Nxd_dns_server_get** *Istemci listesinde DNS sunucusunu döndürür (hem IPv4 hem de IPv6 adreslerini destekler)*</span><span class="sxs-lookup"><span data-stu-id="12058-129">**nxd_dns_server_get** *Return the DNS Server in the Client list (supports both IPv4 and IPv6 addresses)*</span></span>

- <span data-ttu-id="12058-130"> *ISTEMCI listesinden bir dns sunucusunu kaldırmak nxd_dns_server_remove için nx_dns_server_remove sarmalayıcı işlevi*</span><span class="sxs-lookup"><span data-stu-id="12058-130">**nx_dns_server_remove** *Wrapper function for nxd_dns_server_remove to remove a DNS Server from the Client list*</span></span>

- <span data-ttu-id="12058-131"> *belirtilen IP adresinin bir DNS sunucusunu istemci listesinden kaldırmak Nxd_dns_server_remove (hem IPv4 hem de IPv6 adreslerini destekler)*</span><span class="sxs-lookup"><span data-stu-id="12058-131">**nxd_dns_server_remove** *Remove a DNS Server of the specified IP address from the Client list (supports both IPv4 and IPv6 addresses)*</span></span>

- <span data-ttu-id="12058-132">**nx_dns_server_remove_all** *tüm DNS sunucularını istemci listesinden kaldır*</span><span class="sxs-lookup"><span data-stu-id="12058-132">**nx_dns_server_remove_all** *Remove all DNS Servers from the Client list*</span></span>

## <a name="nx_dns_authority_zone_start_get"></a><span data-ttu-id="12058-133">nx_dns_authority_zone_start_get</span><span class="sxs-lookup"><span data-stu-id="12058-133">nx_dns_authority_zone_start_get</span></span>

<span data-ttu-id="12058-134">Giriş ana bilgisayarı için yetki bölgesinin başlangıcına bakın</span><span class="sxs-lookup"><span data-stu-id="12058-134">Look up the start of the zone of authority for the input host</span></span>

### <a name="prototype"></a><span data-ttu-id="12058-135">Prototype</span><span class="sxs-lookup"><span data-stu-id="12058-135">Prototype</span></span>
```C
UINT nx_dns_authority_zone_start_get (NX_DNS *dns_ptr, UCHAR *host_name, 
                                      VOID *record_buffer,                                        
                                      UINT buffer_size, 
                                      UINT *record_count, 
                                      ULONG wait_option);
```
### <a name="description"></a><span data-ttu-id="12058-136">Açıklama</span><span class="sxs-lookup"><span data-stu-id="12058-136">Description</span></span>

<span data-ttu-id="12058-137">NX_DNS_ENABLE_EXTENDED_RR_TYPES tanımlanmışsa, bu hizmet giriş etki alanı adı için yetki bölgesinin başlangıcını almak üzere belirtilen etki alanı adına sahip SOA türünde bir sorgu gönderir.</span><span class="sxs-lookup"><span data-stu-id="12058-137">If NX_DNS_ENABLE_EXTENDED_RR_TYPES is defined, this service sends a query of type SOA with the specified domain name to obtain the start of the zone of authority for the input domain name.</span></span> <span data-ttu-id="12058-138">DNS Istemcisi, DNS sunucusu yanıtında döndürülen SOA kayıtlarını *record_buffer* bellek konumuna kopyalar.</span><span class="sxs-lookup"><span data-stu-id="12058-138">The DNS Client copies the SOA record(s) returned in the DNS Server response into the *record_buffer* memory location.</span></span>

> [!NOTE]
> <span data-ttu-id="12058-139">*Record_buffer* , verileri almak için 4 baytlık hizalı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="12058-139">The *record_buffer* must be 4-byte aligned to receive the data.</span></span>

<span data-ttu-id="12058-140">NetX Duo DNS Istemcisinde, SOA kayıt türü NX_DNS_SOA_ENTRY, 7 4 baytlık parametreler olarak kaydedilir, toplam 28 bayt:</span><span class="sxs-lookup"><span data-stu-id="12058-140">In NetX Duo DNS Client, the SOA record type, NX_DNS_SOA_ENTRY, is saved as seven 4 byte parameters, totaling 28 bytes:</span></span>

- <span data-ttu-id="12058-141">**nx_dns_soa_host_mname_ptr** Bu bölge için birincil veri kaynağı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="12058-141">**nx_dns_soa_host_mname_ptr** Pointer to primary source of data for this zone.</span></span>
- <span data-ttu-id="12058-142">**nx_dns_soa_host_rname_ptr** Bu bölgeden sorumlu olan posta kutusu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="12058-142">**nx_dns_soa_host_rname_ptr** Pointer to mailbox responsible for this zone</span></span>
- <span data-ttu-id="12058-143">**nx_dns_soa_serial** Bölge sürüm numarası</span><span class="sxs-lookup"><span data-stu-id="12058-143">**nx_dns_soa_serial** Zone version number</span></span>
- <span data-ttu-id="12058-144">**nx_dns_soa_refresh** Yenileme aralığı</span><span class="sxs-lookup"><span data-stu-id="12058-144">**nx_dns_soa_refresh** Refresh interval</span></span>
- <span data-ttu-id="12058-145">**nx_dns_soa_retry** SOA sorgu yeniden denemeleri arasındaki Aralık</span><span class="sxs-lookup"><span data-stu-id="12058-145">**nx_dns_soa_retry** Interval between SOA query retries</span></span>
- <span data-ttu-id="12058-146">**nx_dns_soa_expire** SOA süresinin dolduğu süre</span><span class="sxs-lookup"><span data-stu-id="12058-146">**nx_dns_soa_expire** Time duration when SOA expires</span></span>
- <span data-ttu-id="12058-147">**nx_dns_soa_minmum** SOA ana bilgisayar adı DNS yanıt iletilerinde en düşük TTL alanı</span><span class="sxs-lookup"><span data-stu-id="12058-147">**nx_dns_soa_minmum** Minimum TTL field in SOA hostname DNS reply messages</span></span>

<span data-ttu-id="12058-148">İki SOA kaydının depolanması aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="12058-148">The storage of a two SOA records is shown below.</span></span> <span data-ttu-id="12058-149">Sabit uzunluklu verileri içeren SOA kayıtları, arabelleğin en üstünden başlayarak girilir.</span><span class="sxs-lookup"><span data-stu-id="12058-149">The SOA records containing fixed length data are entered starting at the top of the buffer.</span></span> <span data-ttu-id="12058-150">MNAME ve RNAME işaretçileri, arabelleğin altında depolanan değişken uzunluklu verileri (ana bilgisayar adları) işaret edin.</span><span class="sxs-lookup"><span data-stu-id="12058-150">The pointers MNAME and RNAME point to the variable length data (host names) which are stored at the bottom of the buffer.</span></span> <span data-ttu-id="12058-151">Ek SOA kayıtları, ilk kayıttan sonra ("ek SOA kayıtları...") ve değişken uzunluklu verilerin en son girişin değişken uzunluk verilerinde ("ek SOA değişken uzunluğu verileri") depolandıktan sonra girilir:</span><span class="sxs-lookup"><span data-stu-id="12058-151">Additional SOA records are entered after the first record (“additional SOA records…”) and their variable length data is stored above the last entry’s variable length data (“additional SOA variable length data”):</span></span>

![İki SOA kaydının depolanması](media/image4.png)

<span data-ttu-id="12058-153">Giriş *record_buffer* , sunucu YANıTıNDA tüm SOA verilerini tutamazsa, *record_buffer* sığacak kadar çok kayıt tutar ve arabellekteki kayıt sayısını döndürür.</span><span class="sxs-lookup"><span data-stu-id="12058-153">If the input *record_buffer* cannot hold all the SOA data in the server reply, the the *record_buffer* holds as many records as will fit and returns the number of records in the buffer.</span></span>

<span data-ttu-id="12058-154">\* Record_count ' de döndürülen SOA kaydı sayısı ile *,* uygulama *record_buffer* verileri ayrıştırarak bölge yetkilisi ana bilgisayar adı dizelerinin başlangıcını ayıklayabilir.</span><span class="sxs-lookup"><span data-stu-id="12058-154">With the number of SOA records returned in \**record_count,* the application can parse the data from *record_buffer* and extract the start of zone authority host name strings.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="12058-155">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="12058-155">Input Parameters</span></span>

- <span data-ttu-id="12058-156">**dns_ptr** DNS Istemcisi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="12058-156">**dns_ptr** Pointer to DNS Client.</span></span>  
- <span data-ttu-id="12058-157">**host_name** İçin SOA verilerinin alınacağı ana bilgisayar adı işaretçisi</span><span class="sxs-lookup"><span data-stu-id="12058-157">**host_name** Pointer to host name to obtain SOA data for</span></span>
- <span data-ttu-id="12058-158">**record_buffer** SOA verilerinin ayıklanacağı konum işaretçisi</span><span class="sxs-lookup"><span data-stu-id="12058-158">**record_buffer** Pointer to location to extract SOA data into</span></span>
- <span data-ttu-id="12058-159">**Buffer_size** SOA verilerini tutan arabelleğin boyutu</span><span class="sxs-lookup"><span data-stu-id="12058-159">**buffer_size** Size of buffer to hold SOA data</span></span>
- <span data-ttu-id="12058-160">**record_count** Alınan SOA kaydı sayısına yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="12058-160">**record_count** Pointer to the number of SOA records retrieved</span></span>
- <span data-ttu-id="12058-161">**wait_option** DNS sunucusu yanıtı alma seçeneğini bekle</span><span class="sxs-lookup"><span data-stu-id="12058-161">**wait_option** Wait option to receive DNS Server response</span></span>

### <a name="return-values"></a><span data-ttu-id="12058-162">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="12058-162">Return Values</span></span>

- <span data-ttu-id="12058-163">**NX_SUCCESS** (0x00) SOA verileri başarıyla alındı</span><span class="sxs-lookup"><span data-stu-id="12058-163">**NX_SUCCESS** (0x00) Successfully obtained SOA data</span></span>
- <span data-ttu-id="12058-164">**NX_DNS_NO_SERVER** (0xA1) istemci sunucu listesi boş</span><span class="sxs-lookup"><span data-stu-id="12058-164">**NX_DNS_NO_SERVER** (0xA1) Client server list is empty</span></span>
- <span data-ttu-id="12058-165">**NX_DNS_QUERY_FAILED** (0xA3) GEÇERLI bir DNS yanıtı alınmadı</span><span class="sxs-lookup"><span data-stu-id="12058-165">**NX_DNS_QUERY_FAILED** (0xA3) No valid DNS response received</span></span>
- <span data-ttu-id="12058-166">NX_PTR_ERROR (0x07) geçersiz IP veya DNS işaretçisi</span><span class="sxs-lookup"><span data-stu-id="12058-166">NX_PTR_ERROR (0x07) Invalid IP or DNS pointer</span></span>
- <span data-ttu-id="12058-167">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="12058-167">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>
- <span data-ttu-id="12058-168">NX_DNS_PARAM_ERROR (0xA8) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="12058-168">NX_DNS_PARAM_ERROR (0xA8) Invalid non pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="12058-169">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="12058-169">Allowed From</span></span>

<span data-ttu-id="12058-170">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="12058-170">Threads</span></span>

### <a name="example"></a><span data-ttu-id="12058-171">Örnek</span><span class="sxs-lookup"><span data-stu-id="12058-171">Example</span></span>
```C
UCHAR  record_buffer[50];
UINT   record_count;   
NX_DNS_SOA_ENTRY *nx_dns_soa_entry_ptr;

/* Request the start of authority zone(s) for the specified host. */
status =  nx_dns_authority_zone_start_get(&client_dns, (UCHAR *)"www.my_example.com",  
                                          record _buffer, sizeof(record_buffer), 
                                          &record_count, 500);

/* Check for DNS query error. */
if (status != NX_SUCCESS)
{
         error_counter++;
}
else 
{
    /* If status is NX_SUCCESS a DNS query was successfully completed and SOA data 
       is returned in soa_buffer. */

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

[Output]
----------------------------------------------------
Test SOA: 
serial = 2012111212
refresh = 7200
retry = 1800
expire = 1209600
minmum = 300
host mname = ns1.www.my_example.com
host rname = dns-admin.www.my_example.com
```

## <a name="nx_dns_cache_initialize"></a><span data-ttu-id="12058-172">nx_dns_cache_initialize</span><span class="sxs-lookup"><span data-stu-id="12058-172">nx_dns_cache_initialize</span></span>

<span data-ttu-id="12058-173">DNS önbelleğini başlatma</span><span class="sxs-lookup"><span data-stu-id="12058-173">Initialize the DNS Cache</span></span>

### <a name="prototype"></a><span data-ttu-id="12058-174">Prototype</span><span class="sxs-lookup"><span data-stu-id="12058-174">Prototype</span></span>
```C
UINT nx_dns_cache_initialize(NX_DNS *dns_ptr,
                            VOID *cache_ptr, UINT cache_size);
```

### <a name="description"></a><span data-ttu-id="12058-175">Açıklama</span><span class="sxs-lookup"><span data-stu-id="12058-175">Description</span></span>

<span data-ttu-id="12058-176">Bu hizmet bir DNS önbelleği oluşturur ve başlatır.</span><span class="sxs-lookup"><span data-stu-id="12058-176">This service creates and initializes a DNS Cache.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="12058-177">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="12058-177">Input Parameters</span></span>

- <span data-ttu-id="12058-178">**dns_ptr** DNS denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="12058-178">**dns_ptr** Pointer to DNS control block.</span></span>
- <span data-ttu-id="12058-179">**cache_ptr** DNS önbelleği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="12058-179">**cache_ptr** Pointer to DNS Cache.</span></span>
- <span data-ttu-id="12058-180">**cache_size** DNS önbelleğinin bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="12058-180">**cache_size** Size of DNS Cache, in bytes.</span></span>

### <a name="return-values"></a><span data-ttu-id="12058-181">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="12058-181">Return Values</span></span>

- <span data-ttu-id="12058-182">**NX_SUCCESS** (0x00) DNS önbelleği başarıyla başlatıldı</span><span class="sxs-lookup"><span data-stu-id="12058-182">**NX_SUCCESS** (0x00) DNS Cache successfully initialized</span></span>
- <span data-ttu-id="12058-183">NX_DNS_PARAM_ERROR (0xA8) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="12058-183">NX_DNS_PARAM_ERROR (0xA8) Invalid non pointer input</span></span>
- <span data-ttu-id="12058-184">NX_DNS_CACHE_ERROR (0xB7) geçersiz önbellek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="12058-184">NX_DNS_CACHE_ERROR (0xB7) Invalid Cache pointer.</span></span>
- <span data-ttu-id="12058-185">NX_PTR_ERROR (0x07) geçersiz DNS işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="12058-185">NX_PTR_ERROR (0x07) Invalid DNS pointer.</span></span> 
- <span data-ttu-id="12058-186">NX_DNS_ERROR (0xA0) önbelleği 4 bayt hizalı değil.</span><span class="sxs-lookup"><span data-stu-id="12058-186">NX_DNS_ERROR (0xA0) Cache is not 4-byte aligned.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="12058-187">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="12058-187">Allowed From</span></span>

<span data-ttu-id="12058-188">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="12058-188">Threads</span></span>

### <a name="example"></a><span data-ttu-id="12058-189">Örnek</span><span class="sxs-lookup"><span data-stu-id="12058-189">Example</span></span>
```C
/* Initialize the DNS Cache.  */
status =  nx_dns_cache_initialize(&my_dns, &dns_cache, 2048);

/* If status is NX_SUCCESS DNS Cache was successfully initialized.  */
```

## <a name="nx_dns_cache_notify_clear"></a><span data-ttu-id="12058-190">nx_dns_cache_notify_clear</span><span class="sxs-lookup"><span data-stu-id="12058-190">nx_dns_cache_notify_clear</span></span>

<span data-ttu-id="12058-191">DNS önbelleği tam bildirim işlevini temizle</span><span class="sxs-lookup"><span data-stu-id="12058-191">Clear the DNS Cache full notify function</span></span>

### <a name="prototype"></a><span data-ttu-id="12058-192">Prototype</span><span class="sxs-lookup"><span data-stu-id="12058-192">Prototype</span></span>
```C
UINT nx_dns_cache_notify_clear(NX_DNS *dns_ptr);
```

### <a name="description"></a><span data-ttu-id="12058-193">Açıklama</span><span class="sxs-lookup"><span data-stu-id="12058-193">Description</span></span>

<span data-ttu-id="12058-194">Bu hizmet önbellek tam bildirim işlevini temizler.</span><span class="sxs-lookup"><span data-stu-id="12058-194">This service clears the cache full notify function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="12058-195">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="12058-195">Input Parameters</span></span>

- <span data-ttu-id="12058-196">**dns_ptr** DNS denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="12058-196">**dns_ptr** Pointer to DNS control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="12058-197">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="12058-197">Return Values</span></span>

- <span data-ttu-id="12058-198">**NX_SUCCESS** (0x00) DNS önbellek bildirimi başarıyla ayarlandı</span><span class="sxs-lookup"><span data-stu-id="12058-198">**NX_SUCCESS** (0x00) DNS cache notify successfully set</span></span>
- <span data-ttu-id="12058-199">NX_DNS_PARAM_ERROR (0xA8) geçersiz işaretçi olmayan giriş</span><span class="sxs-lookup"><span data-stu-id="12058-199">NX_DNS_PARAM_ERROR (0xA8) Invalid non-pointer input</span></span>
- <span data-ttu-id="12058-200">NX_PTR_ERROR (0x07) geçersiz DNS işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="12058-200">NX_PTR_ERROR (0x07) Invalid DNS pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="12058-201">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="12058-201">Allowed From</span></span>

<span data-ttu-id="12058-202">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="12058-202">Threads</span></span>

### <a name="example"></a><span data-ttu-id="12058-203">Örnek</span><span class="sxs-lookup"><span data-stu-id="12058-203">Example</span></span>
```C
/* Clear the DNS Cache full notify function. */
status =  nx_dns_cache_notify_clear(&my_dns);

/* If status is NX_SUCCESS DNS Cache full notify function was successfully cleared. */
```

## <a name="nx_dns_cache_notify_set"></a><span data-ttu-id="12058-204">nx_dns_cache_notify_set</span><span class="sxs-lookup"><span data-stu-id="12058-204">nx_dns_cache_notify_set</span></span>

<span data-ttu-id="12058-205">DNS önbelleği tam bildirim işlevini ayarla</span><span class="sxs-lookup"><span data-stu-id="12058-205">Set the DNS Cache full notify function</span></span>

### <a name="prototype"></a><span data-ttu-id="12058-206">Prototype</span><span class="sxs-lookup"><span data-stu-id="12058-206">Prototype</span></span>
```C
UINT nx_dns_cache_notify_set(NX_DNS *dns_ptr,
                            VOID (*cache_full_notify_cb)(NX_DNS *dns_ptr));
```

### <a name="description"></a><span data-ttu-id="12058-207">Açıklama</span><span class="sxs-lookup"><span data-stu-id="12058-207">Description</span></span>

<span data-ttu-id="12058-208">Bu hizmet önbellek tam bildirim işlevini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="12058-208">This service sets the cache full notify function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="12058-209">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="12058-209">Input Parameters</span></span>

- <span data-ttu-id="12058-210">**dns_ptr** DNS denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="12058-210">**dns_ptr** Pointer to DNS control block.</span></span>
- <span data-ttu-id="12058-211">**cache_full_notify_cb** Önbellek dolduğunda çağrılacak geri çağırma işlevi.</span><span class="sxs-lookup"><span data-stu-id="12058-211">**cache_full_notify_cb** The callback function to be invoked when cache become full.</span></span>

### <a name="return-values"></a><span data-ttu-id="12058-212">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="12058-212">Return Values</span></span>

- <span data-ttu-id="12058-213">**NX_SUCCESS** (0x00) DNS önbellek bildirimi başarıyla ayarlandı</span><span class="sxs-lookup"><span data-stu-id="12058-213">**NX_SUCCESS** (0x00) DNS cache notify successfully set</span></span>
- <span data-ttu-id="12058-214">NX_DNS_PARAM_ERROR (0xA8) geçersiz işaretçi olmayan giriş</span><span class="sxs-lookup"><span data-stu-id="12058-214">NX_DNS_PARAM_ERROR (0xA8) Invalid non-pointer input</span></span>
- <span data-ttu-id="12058-215">NX_PTR_ERROR (0x07) geçersiz DNS işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="12058-215">NX_PTR_ERROR (0x07) Invalid DNS pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="12058-216">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="12058-216">Allowed From</span></span>

<span data-ttu-id="12058-217">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="12058-217">Threads</span></span>

### <a name="example"></a><span data-ttu-id="12058-218">Örnek</span><span class="sxs-lookup"><span data-stu-id="12058-218">Example</span></span>
```C
/* Set the DNS Cache full notify function. */
status =  nx_dns_cache_notify_set(&my_dns, cache_full_notify_cb);

/* If status is NX_SUCCESS DNS Cache full notify function was successfully set. */
```

## <a name="nx_dns_cname_get"></a><span data-ttu-id="12058-219">nx_dns_cname_get</span><span class="sxs-lookup"><span data-stu-id="12058-219">nx_dns_cname_get</span></span>

<span data-ttu-id="12058-220">Giriş ana bilgisayar adının kurallı adını arayın</span><span class="sxs-lookup"><span data-stu-id="12058-220">Look up the canonical name for the input hostname</span></span>

### <a name="prototype"></a><span data-ttu-id="12058-221">Prototype</span><span class="sxs-lookup"><span data-stu-id="12058-221">Prototype</span></span>
```C
UINT nx_dns_cname_get(NX_DNS *dns_ptr, UCHAR *host_name, 
                     UCHAR *record_buffer, UINT buffer_size, 
                     ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="12058-222">Açıklama</span><span class="sxs-lookup"><span data-stu-id="12058-222">Description</span></span>

<span data-ttu-id="12058-223">NX_DNS_ENABLE_EXTENDED_RR_TYPES *nxd_dns. h* içinde tanımlanmışsa, bu hizmet kurallı etki alanı adını almak için belirtilen etki alanı ADıNA sahip CNAME türünde bir sorgu gönderir.</span><span class="sxs-lookup"><span data-stu-id="12058-223">If NX_DNS_ENABLE_EXTENDED_RR_TYPES is defined in *nxd_dns.h*, this service sends a query of type CNAME with the specified domain name to obtain the canonical domain name.</span></span> <span data-ttu-id="12058-224">DNS Istemcisi, DNS sunucusu yanıtında döndürülen CNAME dizesini *record_buffer* bellek konumuna kopyalar.</span><span class="sxs-lookup"><span data-stu-id="12058-224">The DNS Client copies the CNAME string returned in the DNS Server response into the *record_buffer* memory location.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="12058-225">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="12058-225">Input Parameters</span></span>

- <span data-ttu-id="12058-226">**dns_ptr** DNS Istemcisi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="12058-226">**dns_ptr** Pointer to DNS Client.</span></span>  
- <span data-ttu-id="12058-227">**host_name** İçin CNAME verilerinin alınacağı ana bilgisayar adı işaretçisi</span><span class="sxs-lookup"><span data-stu-id="12058-227">**host_name** Pointer to host name to obtain CNAME data for</span></span>
- <span data-ttu-id="12058-228">**record_buffer** CNAME verilerinin ayıklanacağı konum işaretçisi</span><span class="sxs-lookup"><span data-stu-id="12058-228">**record_buffer** Pointer to location to extract CNAME data into</span></span>
- <span data-ttu-id="12058-229">**Buffer_size** CNAME verilerini tutan arabelleğin boyutu</span><span class="sxs-lookup"><span data-stu-id="12058-229">**buffer_size** Size of buffer to hold CNAME data</span></span>
- <span data-ttu-id="12058-230">**wait_option** DNS sunucusu yanıtı alma seçeneğini bekle</span><span class="sxs-lookup"><span data-stu-id="12058-230">**wait_option** Wait option to receive DNS Server response</span></span>

### <a name="return-values"></a><span data-ttu-id="12058-231">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="12058-231">Return Values</span></span>

- <span data-ttu-id="12058-232">**NX_SUCCESS** (0x00) CNAME verileri başarıyla alındı</span><span class="sxs-lookup"><span data-stu-id="12058-232">**NX_SUCCESS** (0x00) Successfully obtained CNAME data</span></span>
- <span data-ttu-id="12058-233">**NX_DNS_NO_SERVER** (0xA1) istemci sunucu listesi boş</span><span class="sxs-lookup"><span data-stu-id="12058-233">**NX_DNS_NO_SERVER** (0xA1) Client server list is empty</span></span>
- <span data-ttu-id="12058-234">**NX_DNS_QUERY_FAILED** (0xA3) GEÇERLI bir DNS yanıtı alınmadı</span><span class="sxs-lookup"><span data-stu-id="12058-234">**NX_DNS_QUERY_FAILED** (0xA3) No valid DNS response received</span></span>
- <span data-ttu-id="12058-235">NX_PTR_ERROR (0x07) geçersiz IP veya DNS işaretçisi</span><span class="sxs-lookup"><span data-stu-id="12058-235">NX_PTR_ERROR (0x07) Invalid IP or DNS pointer</span></span>
- <span data-ttu-id="12058-236">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="12058-236">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>
- <span data-ttu-id="12058-237">NX_DNS_PARAM_ERROR (0xA8) geçersiz işaretçi olmayan giriş</span><span class="sxs-lookup"><span data-stu-id="12058-237">NX_DNS_PARAM_ERROR (0xA8) Invalid non-pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="12058-238">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="12058-238">Allowed From</span></span>

<span data-ttu-id="12058-239">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="12058-239">Threads</span></span>

### <a name="example"></a><span data-ttu-id="12058-240">Örnek</span><span class="sxs-lookup"><span data-stu-id="12058-240">Example</span></span>
```C
CHAR            record _buffer[50];

/* Request the canonical name for the specified host. */
status =  nx_dns_cname_get(&client_dns, (UCHAR *)"www.my_example.com ", 
                                   record_buffer, sizeof(record_buffer), 500);

/* Check for DNS query error. */
if (status != NX_SUCCESS)
{
    error_counter++;
}
else     
{
/* If status is NX_SUCCESS a DNS query was successfully completed and 
   the canonical host name is returned in record_buffer. */

    printf("------------------------------------------------------\n");
    printf("Test CNAME: %s\n", record_buffer);
} 

[Output]
----------------------------------------------------
Test CNAME: my_example.com
```

##  <a name="nx_dns_create"></a><span data-ttu-id="12058-241">nx_dns_create</span><span class="sxs-lookup"><span data-stu-id="12058-241">nx_dns_create</span></span>

<span data-ttu-id="12058-242">DNS Istemci örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="12058-242">Create a DNS Client instance</span></span>

### <a name="prototype"></a><span data-ttu-id="12058-243">Prototype</span><span class="sxs-lookup"><span data-stu-id="12058-243">Prototype</span></span>
```C
UINT nx_dns_create(NX_DNS *dns_ptr, NX_IP *ip_ptr, CHAR *domain_name);
```
### <a name="description"></a><span data-ttu-id="12058-244">Açıklama</span><span class="sxs-lookup"><span data-stu-id="12058-244">Description</span></span>

<span data-ttu-id="12058-245">Bu hizmet, önceden oluşturulan IP örneği için bir DNS Istemci örneği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="12058-245">This service creates a DNS Client instance for the previously created IP instance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="12058-246">Uygulama, DNS Istemcisi tarafından kullanılan paket havuzunun paket yükünün, en fazla 512 baytlık DNS iletisi, artı UDP, IP ve Ethernet üstbilgileri için yeterince büyük olduğundan emin olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="12058-246">The application must ensure that the packet payload of the packet pool used by the DNS Client is large enough for the maximum 512 byte DNS message, plus UDP, IP and Ethernet headers.</span></span> <span data-ttu-id="12058-247">DNS Istemcisi kendi paket havuzunu oluşturursa, bu NX_DNS_PACKET_PAYLOAD ve NX_DNS_PACKET_POOL_SIZE tarafından tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="12058-247">If the DNS Client creates its own packet pool, this is defined by NX_DNS_PACKET_PAYLOAD and NX_DNS_PACKET_POOL_SIZE.</span></span>

<span data-ttu-id="12058-248">DNS Istemci uygulaması daha önce oluşturulmuş bir paket havuzu sağlamayı tercih ediyorsa, IPv4 DNS Istemcisinin yükü, IP üstbilgisi için en fazla DNS ve 20 bayt, UDP üst bilgisi için 8 bayt ve Ethernet üst bilgisi için 14 bayt 512 olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="12058-248">If the DNS Client application prefers to supply a previously created packet pool, the payload for IPv4 DNS Client should be 512 bytes for the maximum DNS plus 20 bytes for the IP header, 8 bytes for the UDP header and 14 bytes for the Ethernet header.</span></span> <span data-ttu-id="12058-249">IPv6 için tek fark IP üst bilgisinin 40 bayttır ve bu nedenle paketin 40 baytlık IPv6 üst bilgisine uyum sağlaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="12058-249">For IPv6 the only difference is the IP header is 40 bytes, therefore the packet needs to accommodate the IPv6 header of 40 bytes.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="12058-250">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="12058-250">Input Parameters</span></span>

- <span data-ttu-id="12058-251">**dns_ptr** DNS Istemcisi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="12058-251">**dns_ptr** Pointer to DNS Client.</span></span>  
- <span data-ttu-id="12058-252">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="12058-252">**ip_ptr** Pointer to previously created IP instance.</span></span>  
- <span data-ttu-id="12058-253">**domain_name** DNS örneği için etki alanı adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="12058-253">**domain_name** Pointer to domain name for DNS instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="12058-254">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="12058-254">Return Values</span></span>

- <span data-ttu-id="12058-255">**NX_SUCCESS** (0x00) başarılı DNS oluşturma</span><span class="sxs-lookup"><span data-stu-id="12058-255">**NX_SUCCESS** (0x00) Successful DNS create</span></span>
- <span data-ttu-id="12058-256">**NX_DNS_ERROR** (0xa0) DNS oluşturma hatası</span><span class="sxs-lookup"><span data-stu-id="12058-256">**NX_DNS_ERROR** (0xA0) DNS create error</span></span>
- <span data-ttu-id="12058-257">NX_PTR_ERROR (0x07) geçersiz IP veya DNS işaretçisi</span><span class="sxs-lookup"><span data-stu-id="12058-257">NX_PTR_ERROR (0x07) Invalid IP or DNS pointer</span></span>
- <span data-ttu-id="12058-258">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="12058-258">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="12058-259">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="12058-259">Allowed From</span></span>

<span data-ttu-id="12058-260">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="12058-260">Threads</span></span>

### <a name="example"></a><span data-ttu-id="12058-261">Örnek</span><span class="sxs-lookup"><span data-stu-id="12058-261">Example</span></span>
```C
/* Create a DNS Client instance. */
status =  nx_dns_create(&my_dns, &my_ip, "My DNS");

/* If status is NX_SUCCESS a DNS Client instance was successfully
   created. */
```

## <a name="nx_dns_delete"></a><span data-ttu-id="12058-262">nx_dns_delete</span><span class="sxs-lookup"><span data-stu-id="12058-262">nx_dns_delete</span></span>

<span data-ttu-id="12058-263">DNS Istemci örneğini silme</span><span class="sxs-lookup"><span data-stu-id="12058-263">Delete a DNS Client instance</span></span>

### <a name="prototype"></a><span data-ttu-id="12058-264">Prototype</span><span class="sxs-lookup"><span data-stu-id="12058-264">Prototype</span></span>
```C
UINT nx_dns_delete(NX_DNS *dns_ptr);
```
### <a name="description"></a><span data-ttu-id="12058-265">Açıklama</span><span class="sxs-lookup"><span data-stu-id="12058-265">Description</span></span>

<span data-ttu-id="12058-266">Bu hizmet, önceden oluşturulmuş bir DNS Istemci örneğini siler ve kaynaklarını boşaltır.</span><span class="sxs-lookup"><span data-stu-id="12058-266">This service deletes a previously created DNS Client instance and frees up its resources.</span></span> 

> [!NOTE]
> <span data-ttu-id="12058-267">NX_DNS_CLIENT_USER_CREATE_PACKET_POOL tanımlandıysa ve DNS Istemcisine Kullanıcı tanımlı bir paket havuzu atanmışsa, artık gerekmiyorsa, DNS Istemcisi paket havuzunu silmek uygulamaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="12058-267">If NX_DNS_CLIENT_USER_CREATE_PACKET_POOL is defined and the DNS Client was assigned a user defined packet pool, it is up to the application to delete the DNS Client packet pool if it no longer needs it.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="12058-268">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="12058-268">Input Parameters</span></span>

- <span data-ttu-id="12058-269">**dns_ptr** Daha önce oluşturulan DNS Istemci örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="12058-269">**dns_ptr** Pointer to previously created DNS Client instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="12058-270">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="12058-270">Return Values</span></span>

- <span data-ttu-id="12058-271">**NX_SUCCESS** (0x00) başarılı DNS istemcisi silme.</span><span class="sxs-lookup"><span data-stu-id="12058-271">**NX_SUCCESS** (0x00) Successful DNS Client delete.</span></span>
- <span data-ttu-id="12058-272">NX_PTR_ERROR (0x07) geçersiz IP veya DNS Istemci işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="12058-272">NX_PTR_ERROR (0x07) Invalid IP or DNS Client pointer.</span></span>
- <span data-ttu-id="12058-273">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="12058-273">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="12058-274">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="12058-274">Allowed From</span></span>

<span data-ttu-id="12058-275">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="12058-275">Threads</span></span>

### <a name="example"></a><span data-ttu-id="12058-276">Örnek</span><span class="sxs-lookup"><span data-stu-id="12058-276">Example</span></span>
```C
/* Delete a DNS Client instance. */
status =  nx_dns_delete(&my_dns);

/* If status is NX_SUCCESS the DNS Client instance was successfully
   deleted. */
```

## <a name="nx_dns_domain_name_server_get"></a><span data-ttu-id="12058-277">nx_dns_domain_name_server_get</span><span class="sxs-lookup"><span data-stu-id="12058-277">nx_dns_domain_name_server_get</span></span>

<span data-ttu-id="12058-278">Giriş etki alanı bölgesi için yetkili ad sunucularını arayın</span><span class="sxs-lookup"><span data-stu-id="12058-278">Look up the authoritative name servers for the input domain zone</span></span>

### <a name="prototype"></a><span data-ttu-id="12058-279">Prototype</span><span class="sxs-lookup"><span data-stu-id="12058-279">Prototype</span></span>
```C
UINT nx_dns_domain_name_server_get(NX_DNS *dns_ptr, UCHAR *host_name, 
                                   VOID *record_buffer, UINT buffer_size, 
                                   UINT *record_count, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="12058-280">Açıklama</span><span class="sxs-lookup"><span data-stu-id="12058-280">Description</span></span>

<span data-ttu-id="12058-281">NX_DNS_ENABLE_EXTENDED_RR_TYPES tanımlanmışsa, bu hizmet giriş etki alanı adının ad sunucularını almak için belirtilen etki alanı adına sahip NS türünde bir sorgu gönderir.</span><span class="sxs-lookup"><span data-stu-id="12058-281">If NX_DNS_ENABLE_EXTENDED_RR_TYPES is defined, this service sends a query of type NS with the specified domain name to obtain the name servers for the input domain name.</span></span> <span data-ttu-id="12058-282">DNS Istemcisi, DNS sunucusu yanıtında döndürülen NS kayıtlarını *record_buffer* bellek konumuna kopyalar.</span><span class="sxs-lookup"><span data-stu-id="12058-282">The DNS Client copies the NS record(s) returned in the DNS Server response into the *record_buffer* memory location.</span></span>

> [!NOTE]
> <span data-ttu-id="12058-283">*Record_buffer* , verileri almak için 4 baytlık hizalı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="12058-283">The *record_buffer* must be 4-byte aligned to receive the data.</span></span>

<span data-ttu-id="12058-284">NetX Duo DNS Istemcisinde NS veri türü NX_DNS_NS_ENTRY, 2 4 baytlık parametreler olarak kaydedilir:</span><span class="sxs-lookup"><span data-stu-id="12058-284">In NetX Duo DNS Client the NS data type, NX_DNS_NS_ENTRY, is saved as two 4-byte parameters:</span></span>

- <span data-ttu-id="12058-285">**nx_dns_ns_ipv4_address** Ad sunucusunun IPv4 adresi</span><span class="sxs-lookup"><span data-stu-id="12058-285">**nx_dns_ns_ipv4_address** Name server’s IPv4 address</span></span>
- <span data-ttu-id="12058-286">**nx_dns_ns_hostname_ptr** Ad sunucusunun ana bilgisayar adı işaretçisi</span><span class="sxs-lookup"><span data-stu-id="12058-286">**nx_dns_ns_hostname_ptr** Pointer to the name server’s hostname</span></span>

<span data-ttu-id="12058-287">Aşağıda gösterilen arabellek dört NX_DNS_NS_ENTRY kaydı içerir.</span><span class="sxs-lookup"><span data-stu-id="12058-287">The buffer shown below contains four NX_DNS_NS_ENTRY records.</span></span> <span data-ttu-id="12058-288">Her girişte ana bilgisayar adı dizesinin işaretçisi, arabelleğin alt yarısında karşılık gelen ana bilgisayar adı dizesine işaret eder:</span><span class="sxs-lookup"><span data-stu-id="12058-288">The pointer to host name string in each entry points to the corresponding host name string in the bottom half of the buffer:</span></span>

![Dört NX_DNS_NS_ENTRY kaydı içerir](media/image5.png)

<span data-ttu-id="12058-290">Giriş *record_buffer* , sunucu YANıTıNDA tüm NS verilerini tutamazsa, *record_buffer* sığacak kadar çok kayıt tutar ve arabellekteki kayıt sayısını döndürür.</span><span class="sxs-lookup"><span data-stu-id="12058-290">If the input *record_buffer* cannot hold all the NS data in the server reply, the the *record_buffer* holds as many records as will fit and returns the number of records in the buffer.</span></span>

<span data-ttu-id="12058-291">\* Record_count ' de döndürülen NS kayıtlarının sayısı ile *,* uygulama *RECORD_BUFFER* her kaydın IP adresini ve ana bilgisayar adını ayrıştırabilirler.</span><span class="sxs-lookup"><span data-stu-id="12058-291">With the number of NS records returned in \**record_count,* the application can parse the IP address and host name of each record in the *record_buffer*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="12058-292">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="12058-292">Input Parameters</span></span>

- <span data-ttu-id="12058-293">**dns_ptr** DNS Istemcisi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="12058-293">**dns_ptr** Pointer to DNS Client.</span></span>  
- <span data-ttu-id="12058-294">**host_name** İçin NS verilerinin alınacağı ana bilgisayar adı işaretçisi</span><span class="sxs-lookup"><span data-stu-id="12058-294">**host_name** Pointer to host name to obtain NS data for</span></span>
- <span data-ttu-id="12058-295">**record_buffer** NS verilerinin ayıklanacağı konum işaretçisi</span><span class="sxs-lookup"><span data-stu-id="12058-295">**record_buffer** Pointer to location to extract NS data into</span></span>
- <span data-ttu-id="12058-296">**Buffer_size** NS verilerini tutan arabelleğin boyutu</span><span class="sxs-lookup"><span data-stu-id="12058-296">**buffer_size** Size of buffer to hold NS data</span></span>
- <span data-ttu-id="12058-297">**record_count** Alınan NS kaydı sayısının işaretçisi</span><span class="sxs-lookup"><span data-stu-id="12058-297">**record_count** Pointer to the number of NS records retrieved</span></span>
- <span data-ttu-id="12058-298">**wait_option** DNS sunucusu yanıtı alma seçeneğini bekle</span><span class="sxs-lookup"><span data-stu-id="12058-298">**wait_option** Wait option to receive DNS Server response</span></span>

### <a name="return-values"></a><span data-ttu-id="12058-299">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="12058-299">Return Values</span></span>

- <span data-ttu-id="12058-300">**NX_SUCCESS** (0x00) NS verileri başarıyla alındı</span><span class="sxs-lookup"><span data-stu-id="12058-300">**NX_SUCCESS** (0x00) Successfully obtained NS data</span></span>
- <span data-ttu-id="12058-301">**NX_DNS_NO_SERVER** (0xA1) istemci sunucu listesi boş</span><span class="sxs-lookup"><span data-stu-id="12058-301">**NX_DNS_NO_SERVER** (0xA1) Client server list is empty</span></span>
- <span data-ttu-id="12058-302">**NX_DNS_QUERY_FAILED** (0xA3) GEÇERLI bir DNS yanıtı alınmadı</span><span class="sxs-lookup"><span data-stu-id="12058-302">**NX_DNS_QUERY_FAILED** (0xA3) No valid DNS response received</span></span>
- <span data-ttu-id="12058-303">NX_DNS_PARAM_ERROR (0xA8) geçersiz işaretçi olmayan giriş</span><span class="sxs-lookup"><span data-stu-id="12058-303">NX_DNS_PARAM_ERROR (0xA8) Invalid non-pointer input</span></span>
- <span data-ttu-id="12058-304">NX_PTR_ERROR (0x07) geçersiz IP veya DNS işaretçisi</span><span class="sxs-lookup"><span data-stu-id="12058-304">NX_PTR_ERROR (0x07) Invalid IP or DNS pointer</span></span>
- <span data-ttu-id="12058-305">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="12058-305">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="12058-306">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="12058-306">Allowed From</span></span>

<span data-ttu-id="12058-307">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="12058-307">Threads</span></span>

### <a name="example"></a><span data-ttu-id="12058-308">Örnek</span><span class="sxs-lookup"><span data-stu-id="12058-308">Example</span></span>
```C
#define RECORD_COUNT    10

ULONG  record_buffer[50];
UINT   record_count;          
NX_DNS_NS_ENTRY  *nx_dns_ns_entry_ptr[RECORD_COUNT];

/* Request the name server(s) for the specified host. */
status =  nx_dns_domain_name_server_get(&client_dns, (UCHAR *)" www.my_example.com ",  
                                        record_buffer, sizeof(record_buffer),  
                                        &record_count, 500);

/* Check for DNS query error. */
if (status != NX_SUCCESS)
{
    error_counter++;
}

else     
{
/* If status is NX_SUCCESS a DNS query was successfully completed and NS data
   is returned in record_buffer. */

    printf("------------------------------------------------------\n");
    printf("Test NS: ");
    printf("record_count = %d \n", record_count);      

    /* Get the name server. */
    for(i =0; i< record_count; i++)
    {
        nx_dns_ns_entry_ptr[i] = (NX_DNS_NS_ENTRY *)
                               (record_buffer + i * sizeof(NX_DNS_NS_ENTRY)); 

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

[Output]
------------------------------------------------------
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

## <a name="nx_dns_domain_mail_exchange_get"></a><span data-ttu-id="12058-309">nx_dns_domain_mail_exchange_get</span><span class="sxs-lookup"><span data-stu-id="12058-309">nx_dns_domain_mail_exchange_get</span></span>

<span data-ttu-id="12058-310">Giriş ana bilgisayar adı için posta alışverişinin aranacağı</span><span class="sxs-lookup"><span data-stu-id="12058-310">Look up the mail exchange(s) for the input host name</span></span>

### <a name="prototype"></a><span data-ttu-id="12058-311">Prototype</span><span class="sxs-lookup"><span data-stu-id="12058-311">Prototype</span></span>
```C
UINT nx_dns_domain_mail_exchange_get(NX_DNS *dns_ptr, UCHAR *host_name, 
                                     VOID *record_buffer,                                        
                                     UINT buffer_size, 
                                     UINT *record_count, 
                                     ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="12058-312">Açıklama</span><span class="sxs-lookup"><span data-stu-id="12058-312">Description</span></span>

<span data-ttu-id="12058-313">NX_DNS_ENABLE_EXTENDED_RR_TYPES tanımlanmışsa, bu hizmet giriş etki alanı adı için posta değişimini almak üzere belirtilen etki alanı adına sahip MX türünde bir sorgu gönderir.</span><span class="sxs-lookup"><span data-stu-id="12058-313">If NX_DNS_ENABLE_EXTENDED_RR_TYPES is defined, this service sends a query of type MX with the specified domain name to obtain the mail exchange for the input domain name.</span></span> <span data-ttu-id="12058-314">DNS Istemcisi, DNS sunucusu yanıtında döndürülen MX kayıtlarını *record_buffer* bellek konumuna kopyalar.</span><span class="sxs-lookup"><span data-stu-id="12058-314">The DNS Client copies the MX record(s) returned in the DNS Server response into the *record_buffer* memory location.</span></span> 

> [!NOTE]
> <span data-ttu-id="12058-315">*Record_buffer* , verileri almak için 4 baytlık hizalı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="12058-315">The *record_buffer* must be 4-byte aligned to receive the data.</span></span>

<span data-ttu-id="12058-316">NetX Duo DNS Istemcisinde, posta değişim kayıt türü NX_DNS_MAIL_EXCHANGE_ENTRY, dört parametre olarak kaydedilir, 12 baytı toplam olarak kaydeder:</span><span class="sxs-lookup"><span data-stu-id="12058-316">In NetX Duo DNS Client, the mail exchange record type, NX_DNS_MAIL_EXCHANGE_ENTRY, is saved as four parameters, totaling 12 bytes:</span></span>

- <span data-ttu-id="12058-317">**nx_dns_mx_ipv4_address** Posta değişimi IPv4 adresi 4 bayt</span><span class="sxs-lookup"><span data-stu-id="12058-317">**nx_dns_mx_ipv4_address** Mail exchange IPv4 address 4 bytes</span></span>
- <span data-ttu-id="12058-318">**nx_dns_mx_preference** Tercih 2 bayt</span><span class="sxs-lookup"><span data-stu-id="12058-318">**nx_dns_mx_preference** Preference 2 bytes</span></span>
- <span data-ttu-id="12058-319">**nx_dns_mx_reserved0** Ayrılan 2 bayt</span><span class="sxs-lookup"><span data-stu-id="12058-319">**nx_dns_mx_reserved0** Reserved 2 bytes</span></span>
- <span data-ttu-id="12058-320">**nx_dns_mx_hostname_ptr** Posta Exchange Server ana bilgisayar adı 4 bayt işaretçisi</span><span class="sxs-lookup"><span data-stu-id="12058-320">**nx_dns_mx_hostname_ptr** Pointer to mail exchange server host name 4 bytes</span></span>

<span data-ttu-id="12058-321">Dört MX kaydı içeren bir arabellek aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="12058-321">A buffer containing four MX records is shown below.</span></span> <span data-ttu-id="12058-322">Her kayıt, yukarıdaki listeden sabit uzunluklu verileri içerir.</span><span class="sxs-lookup"><span data-stu-id="12058-322">Each record contains the fixed length data from the list above.</span></span> <span data-ttu-id="12058-323">Posta Exchange Server ana bilgisayar adının işaretçisi, arabelleğin alt kısmındaki karşılık gelen ana bilgisayar adına işaret eder.</span><span class="sxs-lookup"><span data-stu-id="12058-323">The pointer to the mail exchange server host name points to the corresponding host name at the bottom of the buffer.</span></span>

![Dört MX kaydı içeren bir arabellek](media/image6.png)

<span data-ttu-id="12058-325">Giriş *record_buffer* , sunucu YANıTıNDA tüm MX verilerini tutamazsa, *record_buffer* sığacak kadar çok kayıt tutar ve arabellekteki kayıt sayısını döndürür.</span><span class="sxs-lookup"><span data-stu-id="12058-325">If the input *record_buffer* cannot hold all the MX data in the server reply, the the *record_buffer* holds as many records as will fit and returns the number of records in the buffer.</span></span>

<span data-ttu-id="12058-326">\**Record_count* ' de döndürülen MX kayıtlarının sayısı ile, uygulama, *record_buffer* her kaydın posta ana bilgisayar adı da dahil olmak üzere MX parametrelerini ayrıştırabilirler.</span><span class="sxs-lookup"><span data-stu-id="12058-326">With the number of MX records returned in \**record_count,* the application can parse the MX parameters, including the mail host name of each record in the *record_buffer*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="12058-327">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="12058-327">Input Parameters</span></span>

- <span data-ttu-id="12058-328">**dns_ptr** DNS Istemcisi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="12058-328">**dns_ptr** Pointer to DNS Client.</span></span>  
- <span data-ttu-id="12058-329">**host_name** MX verilerini almak için ana bilgisayar adı işaretçisi</span><span class="sxs-lookup"><span data-stu-id="12058-329">**host_name** Pointer to host name to obtain MX data for</span></span>
- <span data-ttu-id="12058-330">**record_buffer** MX verilerinin ayıklanacağı konum işaretçisi</span><span class="sxs-lookup"><span data-stu-id="12058-330">**record_buffer** Pointer to location to extract MX data into</span></span>
- <span data-ttu-id="12058-331">**Buffer_size** MX verilerini tutan arabelleğin boyutu</span><span class="sxs-lookup"><span data-stu-id="12058-331">**buffer_size** Size of buffer to hold MX data</span></span>
- <span data-ttu-id="12058-332">**record_count** Alınan MX kaydı sayısının işaretçisi</span><span class="sxs-lookup"><span data-stu-id="12058-332">**record_count** Pointer to the number of MX records retrieved</span></span>
- <span data-ttu-id="12058-333">**wait_option** DNS sunucusu yanıtı alma seçeneğini bekle</span><span class="sxs-lookup"><span data-stu-id="12058-333">**wait_option** Wait option to receive DNS Server response</span></span>

### <a name="return-values"></a><span data-ttu-id="12058-334">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="12058-334">Return Values</span></span>

- <span data-ttu-id="12058-335">**NX_SUCCESS** (0x00) MX verileri başarıyla alındı</span><span class="sxs-lookup"><span data-stu-id="12058-335">**NX_SUCCESS** (0x00) Successfully obtained MX data</span></span>
- <span data-ttu-id="12058-336">**NX_DNS_NO_SERVER** (0xA1) istemci sunucu listesi boş</span><span class="sxs-lookup"><span data-stu-id="12058-336">**NX_DNS_NO_SERVER** (0xA1) Client server list is empty</span></span>
- <span data-ttu-id="12058-337">**NX_DNS_QUERY_FAILED** (0xA3) GEÇERLI bir DNS yanıtı alınmadı</span><span class="sxs-lookup"><span data-stu-id="12058-337">**NX_DNS_QUERY_FAILED** (0xA3) No valid DNS response received</span></span>
- <span data-ttu-id="12058-338">NX_DNS_PARAM_ERROR (0xA8) geçersiz işaretçi olmayan giriş</span><span class="sxs-lookup"><span data-stu-id="12058-338">NX_DNS_PARAM_ERROR (0xA8) Invalid non-pointer input</span></span>
- <span data-ttu-id="12058-339">NX_PTR_ERROR (0x07) geçersiz IP veya DNS işaretçisi</span><span class="sxs-lookup"><span data-stu-id="12058-339">NX_PTR_ERROR (0x07) Invalid IP or DNS pointer</span></span>
- <span data-ttu-id="12058-340">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="12058-340">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="12058-341">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="12058-341">Allowed From</span></span>

<span data-ttu-id="12058-342">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="12058-342">Threads</span></span>

### <a name="example"></a><span data-ttu-id="12058-343">Örnek</span><span class="sxs-lookup"><span data-stu-id="12058-343">Example</span></span>
```C
#define MAX_RECORD_COUNT 10

ULONG  record_buffer[50];
UINT   record_count;  
NX_DNS_MX_ENTRY  *nx_dns_mx_entry_ptr[MAX_RECORD_COUNT];        

/* Request the mail exchange data for the specified host. */
status =  nx_dns_domain_mail_exchange_get(&client_dns, (UCHAR *)" www.my_example.com ", 
                                          record_buffer, sizeof(record_buffer),   
                                          &record_count, 500);

/* Check for DNS query error. */
if (status != NX_SUCCESS)
{
    error_counter++;
}
       
else     
{
/* If status is NX_SUCCESS a DNS query was successfully completed and MX
   data is returned in record_buffer. */

    printf("------------------------------------------------------\n");
    printf("Test MX: ");
    printf("record_count = %d \n", record_count);      


    /* Get the mail exchange. */
    for(i =0; i< record_count; i++)
    {
        nx_dns_mx_entry_ptr[i] = (NX_DNS_MX_ENTRY *)
               (record_buffer + i * sizeof(NX_DNS_MX_ENTRY));   

        printf("record %d: IP address: %d.%d.%d.%d\n", i, 
            nx_dns_mx_entry_ptr[i] -> nx_dns_mx_ipv4_address >> 24,
            nx_dns_mx_entry_ptr[i] -> nx_dns_mx_ipv4_address >> 16 & 0xFF,                   
            nx_dns_mx_entry_ptr[i] -> nx_dns_mx_ipv4_address >> 8 & 0xFF,
            nx_dns_mx_entry_ptr[i] -> nx_dns_mx_ipv4_address & 0xFF);

        printf("preference = %d \n ", 
            nx_dns_mx_entry_ptr[i] -> nx_dns_mx_preference);

        if(nx_dns_mx_entry_ptr[i] -> nx_dns_mx_hostname_ptr)
            printf("hostname = %s\n", 
                    nx_dns_mx_entry_ptr[i] -> nx_dns_mx_hostname_ptr);
        else
            printf("hostname is not set\n");
}


[Output]

-----------------------------------------------------
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

## <a name="nx_dns_domain_service_get"></a><span data-ttu-id="12058-344">nx_dns_domain_service_get</span><span class="sxs-lookup"><span data-stu-id="12058-344">nx_dns_domain_service_get</span></span>

<span data-ttu-id="12058-345">Giriş ana bilgisayar adı tarafından belirtilen hizmet (ler) i ara</span><span class="sxs-lookup"><span data-stu-id="12058-345">Look up the service(s) provided by the input host name</span></span>

### <a name="prototype"></a><span data-ttu-id="12058-346">Prototype</span><span class="sxs-lookup"><span data-stu-id="12058-346">Prototype</span></span>
```C
UINT nx_dns_domain_service_get (NX_DNS *dns_ptr, UCHAR *host_name, 
                                VOID *record_buffer, UINT buffer_size, 
                                UINT *record_count, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="12058-347">Açıklama</span><span class="sxs-lookup"><span data-stu-id="12058-347">Description</span></span>

<span data-ttu-id="12058-348">NX_DNS_ENABLE_EXTENDED_RR_TYPES tanımlanmışsa, bu hizmet, hizmet (ler) i ve belirtilen etki alanıyla ilişkili bağlantı noktası numaralarını aramak için belirtilen etki alanı adına sahip SRV türünde bir sorgu gönderir.</span><span class="sxs-lookup"><span data-stu-id="12058-348">If NX_DNS_ENABLE_EXTENDED_RR_TYPES is defined, this service sends a query of type SRV with the specified domain name to look up the service(s) and their port number associated with the specified domain.</span></span> <span data-ttu-id="12058-349">DNS Istemcisi, DNS sunucusu yanıtında döndürülen SRV kayıtlarını *record_buffer* bellek konumuna kopyalar.</span><span class="sxs-lookup"><span data-stu-id="12058-349">The DNS Client copies the SRV record(s) returned in the DNS Server response into the *record_buffer* memory location.</span></span> 

> [!NOTE]
> <span data-ttu-id="12058-350">*Record_buffer* , verileri almak için 4 baytlık hizalı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="12058-350">The *record_buffer* must be 4-byte aligned to receive the data.</span></span>

<span data-ttu-id="12058-351">NetX Duo DNS Istemcisinde, hizmet kayıt türü NX_DNS_SRV_ GIRDISI, altı parametre olarak kaydedilir ve 16 baytlık bir toplam olur.</span><span class="sxs-lookup"><span data-stu-id="12058-351">In NetX Duo DNS Client, the service record type, NX_DNS_SRV_ ENTRY, is saved as six parameters, totaling 16 bytes.</span></span> <span data-ttu-id="12058-352">Bu, değişken uzunlukta SRV verilerinin bellek verimli şekilde depolanmasını sağlar:</span><span class="sxs-lookup"><span data-stu-id="12058-352">This enables variable length SRV data to be stored in a memory efficient manner:</span></span>

- <span data-ttu-id="12058-353">**Sunucu IPv4 adresi** nx_dns_srv_ipv4_address 4 bayt</span><span class="sxs-lookup"><span data-stu-id="12058-353">**Server IPv4 address** nx_dns_srv_ipv4_address 4 bytes</span></span>
- <span data-ttu-id="12058-354">**Sunucu önceliği** nx_dns_srv_priority 2 bayt</span><span class="sxs-lookup"><span data-stu-id="12058-354">**Server priority** nx_dns_srv_priority 2 bytes</span></span>
- <span data-ttu-id="12058-355">**Sunucu ağırlığı** nx_dns_srv_weight 2 bayt</span><span class="sxs-lookup"><span data-stu-id="12058-355">**Server weight** nx_dns_srv_weight 2 bytes</span></span>
- <span data-ttu-id="12058-356">**Hizmet bağlantı noktası numarası** nx_dns_srv_port_number 2 bayt</span><span class="sxs-lookup"><span data-stu-id="12058-356">**Service port number** nx_dns_srv_port_number 2 bytes</span></span>
- <span data-ttu-id="12058-357">**4 baytlık hizalama Için ayrılan** 2 bayt nx_dns_srv_reserved0</span><span class="sxs-lookup"><span data-stu-id="12058-357">**Reserved for 4-byte alignment** nx_dns_srv_reserved0 2 bytes</span></span>
- <span data-ttu-id="12058-358">**Sunucu ana bilgisayar adı** \* nx_dns_srv_hostname_ptr 4 bayt işaretçisi</span><span class="sxs-lookup"><span data-stu-id="12058-358">**Pointer to server host name** \*nx_dns_srv_hostname_ptr 4 bytes</span></span>

<span data-ttu-id="12058-359">Dört SRV kaydı, sağlanan arabellekte depolanır.</span><span class="sxs-lookup"><span data-stu-id="12058-359">Four SRV records are stored in the supplied buffer.</span></span> <span data-ttu-id="12058-360">Her bir NX_DNS_SRV_ENTRY kaydı, kayıt arabelleğinin alt kısmındaki karşılık gelen ana bilgisayar adı dizesine işaret eden *nx_dns_srv_hostname_ptr* bir işaretçi içerir:</span><span class="sxs-lookup"><span data-stu-id="12058-360">Each NX_DNS_SRV_ENTRY record contains a pointer, *nx_dns_srv_hostname_ptr*, that points to the corresponding host name string in the bottom of the record buffer:</span></span>

![Dört SRV kaydı](media/image7.png)

<span data-ttu-id="12058-362">Giriş *record_buffer* , sunucu YANıTıNDA tüm SRV verilerini tutamazsa, *record_buffer* sığacak kadar çok kayıt tutar ve arabellekteki kayıt sayısını döndürür.</span><span class="sxs-lookup"><span data-stu-id="12058-362">If the input *record_buffer* cannot hold all the SRV data in the server reply, the the *record_buffer* holds as many records as will fit and returns the number of records in the buffer.</span></span>

<span data-ttu-id="12058-363">\**Record_count* ' de döndürülen SRV kayıtlarının sayısı ile, uygulama, *record_buffer* her kaydın sunucu ana bilgisayar adı da dahil olmak üzere SRV parametrelerini ayrıştırabilirler.</span><span class="sxs-lookup"><span data-stu-id="12058-363">With the number of SRV records returned in \**record_count,* the application can parse the SRV parameters, including the server host name of each record in the *record_buffer*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="12058-364">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="12058-364">Input Parameters</span></span>

- <span data-ttu-id="12058-365">**dns_ptr** DNS Istemcisi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="12058-365">**dns_ptr** Pointer to DNS Client.</span></span>  
- <span data-ttu-id="12058-366">**host_name** İçin SRV verilerini almak üzere ana bilgisayar adı işaretçisi</span><span class="sxs-lookup"><span data-stu-id="12058-366">**host_name** Pointer to host name to obtain SRV data for</span></span>
- <span data-ttu-id="12058-367">**record_buffer** SRV verilerinin ayıklanacağı konum işaretçisi</span><span class="sxs-lookup"><span data-stu-id="12058-367">**record_buffer** Pointer to location to extract SRV data into</span></span>
- <span data-ttu-id="12058-368">**Buffer_size** SRV verilerini tutan arabelleğin boyutu</span><span class="sxs-lookup"><span data-stu-id="12058-368">**buffer_size** Size of buffer to hold SRV data</span></span>
- <span data-ttu-id="12058-369">**record_count** Alınan SRV kaydı sayısının işaretçisi</span><span class="sxs-lookup"><span data-stu-id="12058-369">**record_count** Pointer to the number of SRV records retrieved</span></span>
- <span data-ttu-id="12058-370">**wait_option** DNS sunucusu yanıtı alma seçeneğini bekle</span><span class="sxs-lookup"><span data-stu-id="12058-370">**wait_option** Wait option to receive DNS Server response</span></span>

### <a name="return-values"></a><span data-ttu-id="12058-371">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="12058-371">Return Values</span></span>

- <span data-ttu-id="12058-372">**NX_SUCCESS** (0x00), SRV verileri başarıyla alındı</span><span class="sxs-lookup"><span data-stu-id="12058-372">**NX_SUCCESS** (0x00) Successfully obtained SRV data</span></span>
- <span data-ttu-id="12058-373">**NX_DNS_NO_SERVER** (0xA1) istemci sunucu listesi boş</span><span class="sxs-lookup"><span data-stu-id="12058-373">**NX_DNS_NO_SERVER** (0xA1) Client server list is empty</span></span>
- <span data-ttu-id="12058-374">**NX_DNS_QUERY_FAILED** (0xA3) GEÇERLI bir DNS yanıtı alınmadı</span><span class="sxs-lookup"><span data-stu-id="12058-374">**NX_DNS_QUERY_FAILED** (0xA3) No valid DNS response received</span></span>
- <span data-ttu-id="12058-375">NX_DNS_PARAM_ERROR (0xA8) geçersiz işaretçi parametresi.</span><span class="sxs-lookup"><span data-stu-id="12058-375">NX_DNS_PARAM_ERROR (0xA8) Invalid non pointer parameter.</span></span>
- <span data-ttu-id="12058-376">NX_PTR_ERROR (0x07) geçersiz IP veya DNS işaretçisi</span><span class="sxs-lookup"><span data-stu-id="12058-376">NX_PTR_ERROR (0x07) Invalid IP or DNS pointer</span></span>
- <span data-ttu-id="12058-377">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="12058-377">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="12058-378">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="12058-378">Allowed From</span></span>

<span data-ttu-id="12058-379">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="12058-379">Threads</span></span>

### <a name="example"></a><span data-ttu-id="12058-380">Örnek</span><span class="sxs-lookup"><span data-stu-id="12058-380">Example</span></span>
```C
#define MAX_RECORD_COUNT  10

UCHAR  record_buffer[50];
UINT   record_count;          
NX_DNS_SRV_ENTRY *nx_dns_srv_entry_ptr[MAX_RECORD_COUNT];

/* Request the service(s) provided by the specified host. */
status =  nx_dns_domain_service_get(&client_dns, (UCHAR *)"www.my_example.com ", 
                                    record_buffer, sizeof(record_buffer), 
                                    &record_count, 500);

/* Check for DNS query error. */
if (status != NX_SUCCESS)
{
    error_counter++;
}

else     
{
    /* If status is NX_SUCCESS a DNS query was successfully completed and SRV data
       is returned in record_buffer. */

        printf("------------------------------------------------------\n");
        printf("Test SRV: ");
        printf("record_count = %d \n", record_count);      

           
        /* Get the location of services. */
        for(i =0; i< record_count; i++)
        {
            nx_dns_srv_entry_ptr[i] = (NX_DNS_SRV_ENTRY *)
                                    (record_buffer + i * sizeof(NX_DNS_SRV_ENTRY)); 

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

[Output]
----------------------------------------------------
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

## <a name="nx_dns_get_serverlist_size"></a><span data-ttu-id="12058-381">nx_dns_get_serverlist_size</span><span class="sxs-lookup"><span data-stu-id="12058-381">nx_dns_get_serverlist_size</span></span>

<span data-ttu-id="12058-382">DNS Istemcisinin sunucu listesinin boyutunu döndürür</span><span class="sxs-lookup"><span data-stu-id="12058-382">Return the size of the DNS Client’s Server list</span></span>

### <a name="prototype"></a><span data-ttu-id="12058-383">Prototype</span><span class="sxs-lookup"><span data-stu-id="12058-383">Prototype</span></span>
```C
UINT nx_dns_get_serverlist_size (NX_DNS *dns_ptr, UINT *size);
```
### <a name="description"></a><span data-ttu-id="12058-384">Açıklama</span><span class="sxs-lookup"><span data-stu-id="12058-384">Description</span></span>

<span data-ttu-id="12058-385">Bu hizmet, Istemci listesinde geçerli DNS sunucularının (hem IPv4 hem de IPv6) sayısını döndürür.</span><span class="sxs-lookup"><span data-stu-id="12058-385">This service returns the number of valid DNS Servers (both IPv4 and IPv6) in the Client list.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="12058-386">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="12058-386">Input Parameters</span></span>

- <span data-ttu-id="12058-387">**dns_ptr** DNS denetim bloğu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="12058-387">**dns_ptr** Pointer to DNS control block</span></span>  
- <span data-ttu-id="12058-388">**Boyut** Listedeki sunucu sayısını döndürür</span><span class="sxs-lookup"><span data-stu-id="12058-388">**size** Returns the number of servers in the list</span></span>

### <a name="return-values"></a><span data-ttu-id="12058-389">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="12058-389">Return Values</span></span>

- <span data-ttu-id="12058-390">**NX_SUCCESS** (0x00) DNS sunucusu liste boyutu başarıyla döndürüldü</span><span class="sxs-lookup"><span data-stu-id="12058-390">**NX_SUCCESS** (0x00) DNS Server list size successfully returned</span></span>
- <span data-ttu-id="12058-391">NX_PTR_ERROR (0x07) geçersiz IP veya DNS işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="12058-391">NX_PTR_ERROR (0x07) Invalid IP or DNS pointer.</span></span>
- <span data-ttu-id="12058-392">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="12058-392">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="12058-393">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="12058-393">Allowed From</span></span>

<span data-ttu-id="12058-394">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="12058-394">Threads</span></span>

### <a name="example"></a><span data-ttu-id="12058-395">Örnek</span><span class="sxs-lookup"><span data-stu-id="12058-395">Example</span></span>
```C
UINT my_listsize;

/* Get the number of non null DNS Servers in the Client list. */
status =  nx_dns_get_serverlist_size (&my_dns, 5, &my_listsize);

/* If status is NX_SUCCESS the size of the DNS Server list was successfully
   returned. */
```

## <a name="nx_dns_info_by_name_get"></a><span data-ttu-id="12058-396">nx_dns_info_by_name_get</span><span class="sxs-lookup"><span data-stu-id="12058-396">nx_dns_info_by_name_get</span></span>

<span data-ttu-id="12058-397">IP adresini ve DNS sunucusunun bağlantı noktasını ana bilgisayar adına göre döndür</span><span class="sxs-lookup"><span data-stu-id="12058-397">Return ip address and port of DNS server by host name</span></span>

### <a name="prototype"></a><span data-ttu-id="12058-398">Prototype</span><span class="sxs-lookup"><span data-stu-id="12058-398">Prototype</span></span>
```C
UINT nx_dns_info_by_name_get(NX_DNS *dns_ptr, UCHAR *host_name, 
                             ULONG *host_address_ptr,  
                             USHORT *host_port_ptr, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="12058-399">Açıklama</span><span class="sxs-lookup"><span data-stu-id="12058-399">Description</span></span>

<span data-ttu-id="12058-400">Bu hizmet, DNS sorgusunun giriş ana bilgisayar adına göre sunucu IP 'sini ve bağlantı noktasını (hizmet kaydı) döndürür.</span><span class="sxs-lookup"><span data-stu-id="12058-400">This service returns the Server IP and port (service record) based on the input host name by DNS query.</span></span> <span data-ttu-id="12058-401">Bir hizmet kaydı bulunamazsa, bu yordam giriş adresi İşaretçisinde sıfır bir IP adresi döndürür ve bir hatayı bildirmek için sıfır olmayan bir hata durumu döndürür.</span><span class="sxs-lookup"><span data-stu-id="12058-401">If a service record is not found, this routine returns a zero IP address in the input address pointer and a non-zero error status return to signal an error.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="12058-402">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="12058-402">Input Parameters</span></span>

- <span data-ttu-id="12058-403">**dns_ptr** DNS denetim bloğu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="12058-403">**dns_ptr** Pointer to DNS control block</span></span>  
- <span data-ttu-id="12058-404">**host_name** Ana bilgisayar adı arabelleği işaretçisi</span><span class="sxs-lookup"><span data-stu-id="12058-404">**host_name** Pointer to host name buffer</span></span>
- <span data-ttu-id="12058-405">**host_address_ptr** Döndürülecek adres işaretçisi</span><span class="sxs-lookup"><span data-stu-id="12058-405">**host_address_ptr** Pointer to address to return</span></span>
- <span data-ttu-id="12058-406">**host_port_ptr** Döndürülecek bağlantı noktası işaretçisi</span><span class="sxs-lookup"><span data-stu-id="12058-406">**host_port_ptr** Pointer to port to return</span></span>
- <span data-ttu-id="12058-407">**wait_option** DNS yanıtı için bekleme seçeneği</span><span class="sxs-lookup"><span data-stu-id="12058-407">**wait_option** Wait option for the DNS response</span></span>

### <a name="return-values"></a><span data-ttu-id="12058-408">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="12058-408">Return Values</span></span>

- <span data-ttu-id="12058-409">**NX_SUCCESS** (0x00) DNS sunucusu kaydı başarıyla döndürüldü</span><span class="sxs-lookup"><span data-stu-id="12058-409">**NX_SUCCESS** (0x00) DNS Server record successfully returned</span></span>
- <span data-ttu-id="12058-410">**NX_DNS_NO_SERVER** (0xA1) ana bilgisayar adına sorgu göndermek için istemciyle bırlıkte kayıtlı DNS sunucusu yok</span><span class="sxs-lookup"><span data-stu-id="12058-410">**NX_DNS_NO_SERVER** (0xA1) No DNS Server registered with Client to send query on hostname</span></span>
- <span data-ttu-id="12058-411">**NX_DNS_QUERY_FAILED** (0xA3) DNS sorgusu başarısız oldu; giriş ana bilgisayar adı için Istemci listesindeki herhangi bir DNS sunucusundan yanıt yok veya hizmet kaydı yok.</span><span class="sxs-lookup"><span data-stu-id="12058-411">**NX_DNS_QUERY_FAILED** (0xA3) DNS query failed; no response from any DNS servers in Client list or no service record is available for the input hostname.</span></span>
- <span data-ttu-id="12058-412">NX_PTR_ERROR (0x07) geçersiz IP veya DNS işaretçisi</span><span class="sxs-lookup"><span data-stu-id="12058-412">NX_PTR_ERROR (0x07) Invalid IP or DNS pointer</span></span>
- <span data-ttu-id="12058-413">NX_CALLER_ERROR (0x11) geçersiz çağıran</span><span class="sxs-lookup"><span data-stu-id="12058-413">NX_CALLER_ERROR (0x11) Invalid caller</span></span>

### <a name="allowed-from"></a><span data-ttu-id="12058-414">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="12058-414">Allowed From</span></span>

<span data-ttu-id="12058-415">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="12058-415">Threads</span></span>

### <a name="example"></a><span data-ttu-id="12058-416">Örnek</span><span class="sxs-lookup"><span data-stu-id="12058-416">Example</span></span>
```C
ULONG ip_address
USHORT port;

/* Attempt to resolve the IP address and ports for this host name. */
status =  nx_dns_info_by_name_get(&my_dns, “www.abc1234.com”, &ip_address, &port, 200);

/* If status is NX_SUCCESS the DNS query was successful and the IP address and
   report for the hostname are returned. */
```

## <a name="nx_dns_ipv4_address_by_name_get"></a><span data-ttu-id="12058-417">nx_dns_ipv4_address_by_name_get</span><span class="sxs-lookup"><span data-stu-id="12058-417">nx_dns_ipv4_address_by_name_get</span></span>

<span data-ttu-id="12058-418">Giriş ana bilgisayar adı için IPv4 adresini arayın</span><span class="sxs-lookup"><span data-stu-id="12058-418">Look up the IPv4 address for the input host name</span></span>

### <a name="prototype"></a><span data-ttu-id="12058-419">Prototype</span><span class="sxs-lookup"><span data-stu-id="12058-419">Prototype</span></span>
```C
UINT nx_ dns_ipv4_address_by_name_get (NX_DNS *dns_ptr, 
                                      UCHAR *host_name_ptr, VOID *buffer, 
                                      UINT buffer_size, 
                                      UINT *record_count, 
                                      ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="12058-420">Açıklama</span><span class="sxs-lookup"><span data-stu-id="12058-420">Description</span></span>

<span data-ttu-id="12058-421">Bu hizmet, giriş ana bilgisayar adı için IP adreslerini almak üzere belirtilen ana bilgisayar adına sahip A türünde bir sorgu gönderir.</span><span class="sxs-lookup"><span data-stu-id="12058-421">This service sends a query of Type A with the specified host name to obtain the IP addresses for the input host name.</span></span> <span data-ttu-id="12058-422">DNS Istemcisi, IPv4 adresini DNS sunucusu yanıtında döndürülen bir kayıt (lar) dan *record_buffer* bellek konumuna kopyalar.</span><span class="sxs-lookup"><span data-stu-id="12058-422">The DNS Client copies the IPv4 address from the A record(s) returned in the DNS Server response into the *record_buffer* memory location.</span></span>

> [!NOTE]
> <span data-ttu-id="12058-423">*Record_buffer* , verileri almak için 4 baytlık hizalı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="12058-423">The *record_buffer* must be 4-byte aligned to receive the data.</span></span>

<span data-ttu-id="12058-424">Aşağıda gösterildiği gibi, 4 baytlık hizalanmış arabellekte birden çok IPv4 adresi depolanır:</span><span class="sxs-lookup"><span data-stu-id="12058-424">Multiple IPv4 addresses are stored in the 4-byte aligned buffer as shown below:</span></span>

![birden çok adres 4-bayt hizalı arabellek](media/image8.png)

<span data-ttu-id="12058-426">Sağlanan arabellek tüm IP adresi verilerini tutamıyorsa, kalan kayıtlar *record_buffer* depolanmaz.</span><span class="sxs-lookup"><span data-stu-id="12058-426">If the supplied buffer cannot hold all the IP address data, the remaining A records are not stored in *record_buffer*.</span></span> <span data-ttu-id="12058-427">Bu, uygulamanın sunucu yanıtında kullanılabilir IP adresi verilerinin bir kısmını veya tamamını almasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="12058-427">This enables the application to retrieve one, some or all of the available IP address data in the server reply.</span></span>

<span data-ttu-id="12058-428">\**Record_count* döndürülen kayıt sayısı ile uygulama, IPv4 adresi verilerini *record_buffer* ayrıştırabilirler.</span><span class="sxs-lookup"><span data-stu-id="12058-428">With the number of A records returned in \**record_count* the application can parse the IPv4 address data from the *record_buffer*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="12058-429">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="12058-429">Input Parameters</span></span>

- <span data-ttu-id="12058-430">**dns_ptr** DNS Istemcisi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="12058-430">**dns_ptr** Pointer to DNS Client.</span></span>  
- <span data-ttu-id="12058-431">**host_name_ptr** IPv4 adresini almak için ana bilgisayar adı işaretçisi</span><span class="sxs-lookup"><span data-stu-id="12058-431">**host_name_ptr** Pointer to host name to obtain IPv4 address</span></span>
- <span data-ttu-id="12058-432">**arabellek** IPv4 verilerinin ayıklanacağı konum işaretçisi</span><span class="sxs-lookup"><span data-stu-id="12058-432">**buffer** Pointer to location to extract IPv4 data into</span></span>
- <span data-ttu-id="12058-433">**Buffer_size** IPv4 verilerini tutan arabelleğin boyutu</span><span class="sxs-lookup"><span data-stu-id="12058-433">**buffer_size** Size of buffer to hold IPv4 data</span></span>
- <span data-ttu-id="12058-434">**wait_option** DNS sunucusu yanıtı alma seçeneğini bekle</span><span class="sxs-lookup"><span data-stu-id="12058-434">**wait_option** Wait option to receive DNS Server response</span></span>

### <a name="return-values"></a><span data-ttu-id="12058-435">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="12058-435">Return Values</span></span>

- <span data-ttu-id="12058-436">**NX_SUCCESS** (0x00) IPv4 verileri başarıyla alındı</span><span class="sxs-lookup"><span data-stu-id="12058-436">**NX_SUCCESS** (0x00) Successfully obtained IPv4 data</span></span>
- <span data-ttu-id="12058-437">**NX_DNS_NO_SERVER** (0xA1) istemci sunucu listesi boş</span><span class="sxs-lookup"><span data-stu-id="12058-437">**NX_DNS_NO_SERVER** (0xA1) Client server list is empty</span></span>
- <span data-ttu-id="12058-438">**NX_DNS_QUERY_FAILED** (0xA3) GEÇERLI bir DNS yanıtı alınmadı</span><span class="sxs-lookup"><span data-stu-id="12058-438">**NX_DNS_QUERY_FAILED** (0xA3) No valid DNS response received</span></span>
- <span data-ttu-id="12058-439">NX_PTR_ERROR (0x07) geçersiz IP veya DNS işaretçisi</span><span class="sxs-lookup"><span data-stu-id="12058-439">NX_PTR_ERROR (0x07) Invalid IP or DNS pointer</span></span>
- <span data-ttu-id="12058-440">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="12058-440">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>
- <span data-ttu-id="12058-441">NX_DNS_PARAM_ERROR (0xA8) geçersiz işaretçi parametresi.</span><span class="sxs-lookup"><span data-stu-id="12058-441">NX_DNS_PARAM_ERROR (0xA8) Invalid non pointer parameter.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="12058-442">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="12058-442">Allowed From</span></span>

<span data-ttu-id="12058-443">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="12058-443">Threads</span></span>

### <a name="example"></a><span data-ttu-id="12058-444">Örnek</span><span class="sxs-lookup"><span data-stu-id="12058-444">Example</span></span>
```C
#define MAX_RECORD_COUNT  20

ULONG           record_buffer[50];
UINT            record_count;
ULONG           *ipv4_address_ptr[MAX_RECORD_COUNT];

/* Request the IPv4 address for the specified host. */
status =  nx_dns_ipv4_address_by_name_get(&client_dns, 
                                          (UCHAR *)"www.my_example.com",  
                                           record_buffer,                  
                                           sizeof(record_buffer),&record_count,                
                                           500);

/* Check for DNS query error. */
if (status != NX_SUCCESS)
{
        error_counter++;
}    
        else     
{
    /* If status is NX_SUCCESS a DNS query was successfully completed the IPv4
       address(es) is returned in record_buffer. */

          
            printf("------------------------------------------------------\n");
            printf("Test A: ");
            printf("record_count = %d \n", record_count);      


           /* Get the IPv4 addresses of host. */
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

[Output]

------------------------------------------------------
Test A: record_count = 5 
record 0: IP address: 192.2.2.10
record 1: IP address: 192.2.2.11
record 2: IP address: 192.2.2.12
record 3: IP address: 192.2.2.13
record 4: IP address: 192.2.2.14
```

## <a name="nxd_dns_ipv6_address_by_name_get"></a><span data-ttu-id="12058-445">nxd_dns_ipv6_address_by_name_get</span><span class="sxs-lookup"><span data-stu-id="12058-445">nxd_dns_ipv6_address_by_name_get</span></span>

<span data-ttu-id="12058-446">Giriş ana bilgisayar adı için IPv6 adresini arayın</span><span class="sxs-lookup"><span data-stu-id="12058-446">Look up the IPv6 address for the input host name</span></span>

### <a name="prototype"></a><span data-ttu-id="12058-447">Prototype</span><span class="sxs-lookup"><span data-stu-id="12058-447">Prototype</span></span>
```C
UINT nxd_ dns_ipv6_address_by_name_get(NX_DNS *dns_ptr, 
                                      UCHAR *host_name_ptr, VOID *buffer, 
                                      UINT buffer_size, 
                                      UINT *record_count, 
                                      ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="12058-448">Açıklama</span><span class="sxs-lookup"><span data-stu-id="12058-448">Description</span></span>

<span data-ttu-id="12058-449">Bu hizmet, giriş etki alanı adının IP adreslerini almak için belirtilen etki alanı adına sahip AAAA türünde bir sorgu gönderir.</span><span class="sxs-lookup"><span data-stu-id="12058-449">This service sends a query of type AAAA with the specified domain name to obtain the IP addresses for the input domain name.</span></span> <span data-ttu-id="12058-450">DNS Istemcisi, IPv6 adresini DNS sunucusu yanıtında döndürülen AAAA kaydından *record_buffer* bellek konumuna kopyalar.</span><span class="sxs-lookup"><span data-stu-id="12058-450">The DNS Client copies the IPv6 address from the AAAA record(s) returned in the DNS Server response into the *record_buffer* memory location.</span></span> 

> [!NOTE]
> <span data-ttu-id="12058-451">*Record_buffer* , verileri almak için 4 baytlık hizalı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="12058-451">The *record_buffer* must be 4-byte aligned to receive the data.</span></span>

<span data-ttu-id="12058-452">4 baytlık hizalanmış arabellekte depolanan IPv6 adreslerinin biçimi aşağıda gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="12058-452">The format of IPv6 addresses stored in the 4-byte aligned buffer is shown below:</span></span>

![IPv6 biçimi 4-bayt hizalanmış arabellek](media/image9.png)

<span data-ttu-id="12058-454">Giriş *record_buffer* , sunucu YANıTıNDA tüm aaaa verilerini tutamazsa, *record_buffer* sığacak kadar çok kayıt tutar ve arabellekteki kayıt sayısını döndürür.</span><span class="sxs-lookup"><span data-stu-id="12058-454">If the input *record_buffer* cannot hold all the AAAA data in the server reply, the the *record_buffer* holds as many records as will fit and returns the number of records in the buffer.</span></span>

<span data-ttu-id="12058-455">\* Record_count ' de döndürülen AAAA kaydı sayısı ile *,* uygulama *record_buffer* her bir kayıttaki IPv6 adreslerini ayrıştırabilirler.</span><span class="sxs-lookup"><span data-stu-id="12058-455">With the number of AAAA records returned in \**record_count,* the application can parse the IPv6 addresses from each record in the *record_buffer*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="12058-456">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="12058-456">Input Parameters</span></span>

- <span data-ttu-id="12058-457">**dns_ptr** DNS Istemcisi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="12058-457">**dns_ptr** Pointer to DNS Client.</span></span>  
- <span data-ttu-id="12058-458">**host_name_ptr** IPv6 adresini almak için ana bilgisayar adı işaretçisi</span><span class="sxs-lookup"><span data-stu-id="12058-458">**host_name_ptr** Pointer to host name to obtain IPv6 address</span></span>
- <span data-ttu-id="12058-459">**arabellek** IPv6 verilerinin ayıklanacağı konum işaretçisi</span><span class="sxs-lookup"><span data-stu-id="12058-459">**buffer** Pointer to location to extract IPv6 data into</span></span>
- <span data-ttu-id="12058-460">**Buffer_size** IPv6 verilerini tutan arabelleğin boyutu</span><span class="sxs-lookup"><span data-stu-id="12058-460">**buffer_size** Size of buffer to hold IPv6 data</span></span>
- <span data-ttu-id="12058-461">**wait_option** DNS sunucusu yanıtı alma seçeneğini bekle</span><span class="sxs-lookup"><span data-stu-id="12058-461">**wait_option** Wait option to receive DNS Server response</span></span>

### <a name="return-values"></a><span data-ttu-id="12058-462">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="12058-462">Return Values</span></span>

- <span data-ttu-id="12058-463">**NX_SUCCESS** (0x00) IPv6 verileri başarıyla alındı</span><span class="sxs-lookup"><span data-stu-id="12058-463">**NX_SUCCESS** (0x00) Successfully obtained IPv6 data</span></span>
- <span data-ttu-id="12058-464">**NX_DNS_NO_SERVER** (0xA1) istemci sunucu listesi boş</span><span class="sxs-lookup"><span data-stu-id="12058-464">**NX_DNS_NO_SERVER** (0xA1) Client server list is empty</span></span>
- <span data-ttu-id="12058-465">**NX_DNS_QUERY_FAILED** (0xA3) GEÇERLI bir DNS yanıtı alınmadı</span><span class="sxs-lookup"><span data-stu-id="12058-465">**NX_DNS_QUERY_FAILED** (0xA3) No valid DNS response received</span></span>
- <span data-ttu-id="12058-466">NX_PTR_ERROR (0x07) geçersiz IP veya DNS işaretçisi</span><span class="sxs-lookup"><span data-stu-id="12058-466">NX_PTR_ERROR (0x07) Invalid IP or DNS pointer</span></span>
- <span data-ttu-id="12058-467">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="12058-467">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>
- <span data-ttu-id="12058-468">NX_DNS_PARAM_ERROR (0xA8) geçersiz işaretçi parametresi.</span><span class="sxs-lookup"><span data-stu-id="12058-468">NX_DNS_PARAM_ERROR (0xA8) Invalid non pointer parameter.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="12058-469">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="12058-469">Allowed From</span></span>

<span data-ttu-id="12058-470">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="12058-470">Threads</span></span>

### <a name="example"></a><span data-ttu-id="12058-471">Örnek</span><span class="sxs-lookup"><span data-stu-id="12058-471">Example</span></span>
```C
#define      MAX_RECORD_COUNT  20

ULONG           record_buffer[50];
UINT            record_count;
NXD_ADDRESS    *ipv6_address_ptr[MAX_RECORD_COUNT];

/* Request the IPv4 address for the specified host. */
status =  nxd_dns_ipv6_address_by_name_get(&client_dns, 
                                           (UCHAR *)"www.my_example.com", 
                                           record__buffer,                  
                                           sizeof(record_buffer), 
                                           &record_count, 500);

/* Check for DNS query error. */
if (status != NX_SUCCESS)
{
        error_counter++;
}    
        else     
{
/* If status is NX_SUCCESS a DNS query was successfully completed the IPv6 
    address(es) is (are) returned in record_buffer. */
      
    printf("------------------------------------------------------\n");
    printf("Test AAAA: ");
    printf("record_count = %d \n", record_count);      

    /* Get the IPv6 addresses of host. */
    for(i =0; i< record_count; i++)
    {

        ipv6_address_ptr[i] = 
            (NX_DNS_IPV6_ADDRESS *)(record_buffer + i * sizeof(NX_DNS_IPV6_ADDRESS)); 
             
        printf("record %d: IP address: %x:%x:%x:%x:%x:%x:%x:%x\n", i, 
                ipv6_address_ptr[i] -> ipv6_address[0]  >>16 & 0xFFFF,
                ipv6_address_ptr[i] -> ipv6_address[0]  & 0xFFFF,
                ipv6_address_ptr[i] -> ipv6_address[1]  >>16 & 0xFFFF,
                ipv6_address_ptr[i] -> ipv6_address[1]  & 0xFFFF,
                ipv6_address_ptr[i] -> ipv6_address[2]  >>16 & 0xFFFF,
                ipv6_address_ptr[i] -> ipv6_address[2]  & 0xFFFF,
                ipv6_address_ptr[i] -> ipv6_address[3]  >>16 & 0xFFFF,
                ipv6_address_ptr[i] -> ipv6_address[3]  & 0xFFFF);
            }
}


[Output]
------------------------------------------------------
Test AAAA: record_count = 1 
record 0: IP address: 2001:0db8:0000:f101: 0000: 0000: 0000:01003
```

## <a name="nx_dns_host_by_address_get"></a><span data-ttu-id="12058-472">nx_dns_host_by_address_get</span><span class="sxs-lookup"><span data-stu-id="12058-472">nx_dns_host_by_address_get</span></span>

<span data-ttu-id="12058-473">Bir IP adresinden ana bilgisayar adı ara</span><span class="sxs-lookup"><span data-stu-id="12058-473">Look up a host name from an IP address</span></span>

### <a name="prototype"></a><span data-ttu-id="12058-474">Prototype</span><span class="sxs-lookup"><span data-stu-id="12058-474">Prototype</span></span>
```C
UINT nx_dns_host_by_address_get(NX_DNS *dns_ptr, ULONG ip_address, 
                                ULONG *host_name_ptr, 
                                ULONG max_host_name_size, 
                                ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="12058-475">Açıklama</span><span class="sxs-lookup"><span data-stu-id="12058-475">Description</span></span>

<span data-ttu-id="12058-476">Bu hizmet, uygulama tarafından daha önce belirtilen bir veya daha fazla DNS sunucusundan sağlanan IP adresinin ad çözümlemesini ister.</span><span class="sxs-lookup"><span data-stu-id="12058-476">This service requests name resolution of the supplied IP address from one or more DNS Servers previously specified by the application.</span></span> <span data-ttu-id="12058-477">Başarılı olursa, NULL ile sonlandırılmış ana bilgisayar adı *host_name_ptr* tarafından belirtilen dizede döndürülür.</span><span class="sxs-lookup"><span data-stu-id="12058-477">If successful, the NULL-terminated host name is returned in the string specified by *host_name_ptr*.</span></span> <span data-ttu-id="12058-478">Bu, *nxd_dns_host_by_address_get* hizmeti için bir sarmalayıcı Işlevidir ve IPv6 adreslerini kabul etmez.</span><span class="sxs-lookup"><span data-stu-id="12058-478">This is a wrapper function for *nxd_dns_host_by_address_get* service and does not accept IPv6 addresses.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="12058-479">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="12058-479">Input Parameters</span></span>

- <span data-ttu-id="12058-480">**dns_ptr** Daha önce oluşturulan DNS örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="12058-480">**dns_ptr** Pointer to previously created DNS instance.</span></span>
- <span data-ttu-id="12058-481">**ip_address** Bir ada çözülecek IP adresi</span><span class="sxs-lookup"><span data-stu-id="12058-481">**ip_address** IP address to resolve into a name</span></span>
- <span data-ttu-id="12058-482">**host_name_ptr** Ana bilgisayar adı için hedef alan işaretçisi</span><span class="sxs-lookup"><span data-stu-id="12058-482">**host_name_ptr** Pointer to destination area for host name</span></span>
- <span data-ttu-id="12058-483">**max_host_name_size** Ana bilgisayar adı için hedef alanın boyutu</span><span class="sxs-lookup"><span data-stu-id="12058-483">**max_host_name_size** Size of destination area for host name</span></span>
- <span data-ttu-id="12058-484">**wait_option** Her DNS sorgusunun ve sorgusunun yeniden denendikten sonra, hizmetin bir DNS sunucusu yanıtı için Zamanlayıcı işaretlerini ne kadar bekleyeceğini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="12058-484">**wait_option** Defines how long the service will wait in timer ticks for a DNS server response after each DNS query and query retry.</span></span> <span data-ttu-id="12058-485">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="12058-485">The wait options are defined as follows:</span></span>

  <span data-ttu-id="12058-486">zaman aşımı değeri (0x00000001-0xFFFFFFFE) TX_WAIT_FOREVER (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="12058-486">timeout value (0x00000001-0xFFFFFFFE) TX_WAIT_FOREVER (0xFFFFFFFF)</span></span>

  <span data-ttu-id="12058-487">TX_WAIT_FOREVER seçildiğinde çağıran iş parçacığının bir DNS sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="12058-487">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a DNS server responds to the request.</span></span>

  <span data-ttu-id="12058-488">Sayısal bir değer (1-0xFFFFFFFE) seçilmesi, DNS çözümlemesi beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="12058-488">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the DNS resolution.</span></span>

### <a name="return-values"></a><span data-ttu-id="12058-489">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="12058-489">Return Values</span></span>

- <span data-ttu-id="12058-490">**NX_SUCCESS** (0x00) başarılı DNS çözümlemesi</span><span class="sxs-lookup"><span data-stu-id="12058-490">**NX_SUCCESS** (0x00) Successful DNS resolution</span></span>  
- <span data-ttu-id="12058-491">**NX_DNS_TIMEOUT** (0xA2), DNS mutex 'i alma sırasında zaman aşımına uğradı</span><span class="sxs-lookup"><span data-stu-id="12058-491">**NX_DNS_TIMEOUT** (0xA2) Timed out on obtaining DNS mutex</span></span>
- <span data-ttu-id="12058-492">**NX_DNS_NO_SERVER** (0xA1) DNS sunucusu adresi belirtilmedi</span><span class="sxs-lookup"><span data-stu-id="12058-492">**NX_DNS_NO_SERVER** (0xA1) No DNS Server address specified</span></span>
- <span data-ttu-id="12058-493">**NX_DNS_QUERY_FAILED** (0xA3) sorguya yanıt almadı</span><span class="sxs-lookup"><span data-stu-id="12058-493">**NX_DNS_QUERY_FAILED** (0xA3) Received no response to query</span></span>
- <span data-ttu-id="12058-494">**NX_DNS_BAD_ADDRESS_ERROR** (0xa4) null giriş adresi</span><span class="sxs-lookup"><span data-stu-id="12058-494">**NX_DNS_BAD_ADDRESS_ERROR** (0xA4) Null input address</span></span>
- <span data-ttu-id="12058-495">**NX_DNS_INVALID_ADDRESS_TYPE** (0xB2) dizin noktaları geçersiz adres türüne (örn. IPv6)</span><span class="sxs-lookup"><span data-stu-id="12058-495">**NX_DNS_INVALID_ADDRESS_TYPE** (0xB2) Index points to invalid address type (e.g. IPv6)</span></span>
- <span data-ttu-id="12058-496">**NX_DNS_PARAM_ERROR** (0Xa8) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="12058-496">**NX_DNS_PARAM_ERROR** (0xA8) Invalid non pointer input</span></span>
- <span data-ttu-id="12058-497">**NX_DNS_IPV6_NOT_SUPPORTED** (0xb3) IPv6 devre dışı olarak kayıt işlenemiyor</span><span class="sxs-lookup"><span data-stu-id="12058-497">**NX_DNS_IPV6_NOT_SUPPORTED** (0xB3) Cannot process record with IPv6 disabled</span></span>
- <span data-ttu-id="12058-498">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="12058-498">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="12058-499">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="12058-499">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="12058-500">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="12058-500">Allowed From</span></span>

<span data-ttu-id="12058-501">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="12058-501">Threads</span></span>

<span data-ttu-id="12058-502">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="12058-502">**Example**</span></span>
```C
#define BUFFER_SIZE   200

UCHAR   resolved_name[200];

/* Get the name associated with IP address 192.2.2.10.  */
status =  nx_dns_host_by_address_get(&my_dns, IP_ADDRESS(192.2.2.10),
                                     &resolved_name[0], BUFFER_SIZE, 450);

/* If status is NX_SUCCESS the name associated with the IP address
   can be found in the resolved_name variable.  */
```

## <a name="nxd_dns_host_by_address_get"></a><span data-ttu-id="12058-503">nxd_dns_host_by_address_get</span><span class="sxs-lookup"><span data-stu-id="12058-503">nxd_dns_host_by_address_get</span></span>

<span data-ttu-id="12058-504">IP adresinden bir ana bilgisayar adı ara</span><span class="sxs-lookup"><span data-stu-id="12058-504">Look up a host name from the IP address</span></span>

### <a name="prototype"></a><span data-ttu-id="12058-505">Prototype</span><span class="sxs-lookup"><span data-stu-id="12058-505">Prototype</span></span>
```C
UINT nxd_dns_host_by_address_get(NX_DNS *dns_ptr, 
                                 NXD_ADDRESS ip_address, 
                                 ULONG *host_name_ptr, 
                                 ULONG max_host_name_size, 
                                 ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="12058-506">Açıklama</span><span class="sxs-lookup"><span data-stu-id="12058-506">Description</span></span>

<span data-ttu-id="12058-507">Bu hizmet, uygulama tarafından daha önce belirtilen bir veya daha fazla DNS sunucusundan *ip_address* giriş bağımsız değişkeninde IPv6 veya IPv4 adresinin ad çözümlemesini ister.</span><span class="sxs-lookup"><span data-stu-id="12058-507">This service requests name resolution of the IPv6 or IPv4 address in the *ip_address* input argument from one or more DNS Servers previously specified by the application.</span></span> <span data-ttu-id="12058-508">Başarılı olursa, NULL ile sonlandırılmış ana bilgisayar adı *host_name_ptr* tarafından belirtilen dizede döndürülür.</span><span class="sxs-lookup"><span data-stu-id="12058-508">If successful, the NULL-terminated host name is returned in the string specified by *host_name_ptr*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="12058-509">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="12058-509">Input Parameters</span></span>

- <span data-ttu-id="12058-510">**dns_ptr** Daha önce oluşturulan DNS örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="12058-510">**dns_ptr** Pointer to previously created DNS instance.</span></span>
- <span data-ttu-id="12058-511">**ip_address** Bir ada çözülecek IP adresi</span><span class="sxs-lookup"><span data-stu-id="12058-511">**ip_address** IP address to resolve into a name</span></span>
- <span data-ttu-id="12058-512">**host_name_ptr** Ana bilgisayar adı için hedef alan işaretçisi</span><span class="sxs-lookup"><span data-stu-id="12058-512">**host_name_ptr** Pointer to destination area for host name</span></span>
- <span data-ttu-id="12058-513">**max_host_name_size** Ana bilgisayar adı için hedef alanın boyutu</span><span class="sxs-lookup"><span data-stu-id="12058-513">**max_host_name_size** Size of destination area for host name</span></span>
- <span data-ttu-id="12058-514">**wait_option** Her DNS sorgusunun ve sorgusunun yeniden denendikten sonra, hizmetin bir DNS sunucusu yanıtı için Zamanlayıcı işaretlerini ne kadar bekleyeceğini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="12058-514">**wait_option** Defines how long the service will wait in timer ticks for a DNS server response after each DNS query and query retry.</span></span> <span data-ttu-id="12058-515">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="12058-515">The wait options are defined as follows:</span></span>

  <span data-ttu-id="12058-516">zaman aşımı değeri (0x00000001-0xFFFFFFFE) TX_WAIT_FOREVER (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="12058-516">timeout value (0x00000001 through 0xFFFFFFFE) TX_WAIT_FOREVER (0xFFFFFFFF)</span></span>  

  <span data-ttu-id="12058-517">TX_WAIT_FOREVER seçildiğinde çağıran iş parçacığının bir DNS sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="12058-517">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a DNS server responds to the request.</span></span>

  <span data-ttu-id="12058-518">Sayısal bir değer (1-0xFFFFFFFE) seçilmesi, DNS çözümlemesi beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="12058-518">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the DNS resolution.</span></span>

### <a name="return-values"></a><span data-ttu-id="12058-519">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="12058-519">Return Values</span></span>

- <span data-ttu-id="12058-520">**NX_SUCCESS** (0x00) başarılı DNS çözümlemesi</span><span class="sxs-lookup"><span data-stu-id="12058-520">**NX_SUCCESS** (0x00) Successful DNS resolution</span></span>  
- <span data-ttu-id="12058-521">**NX_DNS_TIMEOUT** (0xA2), DNS mutex 'i alma sırasında zaman aşımına uğradı</span><span class="sxs-lookup"><span data-stu-id="12058-521">**NX_DNS_TIMEOUT** (0xA2) Timed out on obtaining DNS mutex</span></span>
- <span data-ttu-id="12058-522">**NX_DNS_NO_SERVER** (0xA1) DNS sunucusu adresi belirtilmedi</span><span class="sxs-lookup"><span data-stu-id="12058-522">**NX_DNS_NO_SERVER** (0xA1) No DNS Server address specified</span></span>
- <span data-ttu-id="12058-523">**NX_DNS_QUERY_FAILED** (0xA3) sorguya yanıt almadı</span><span class="sxs-lookup"><span data-stu-id="12058-523">**NX_DNS_QUERY_FAILED** (0xA3) Received no response to query</span></span>
- <span data-ttu-id="12058-524">**NX_DNS_BAD_ADDRESS_ERROR** (0xa4) null giriş adresi</span><span class="sxs-lookup"><span data-stu-id="12058-524">**NX_DNS_BAD_ADDRESS_ERROR** (0xA4) Null input address</span></span>
- <span data-ttu-id="12058-525">**NX_DNS_IPV6_NOT_SUPPORTED** (0xb3) IPv6 devre dışı olarak kayıt işlenemiyor</span><span class="sxs-lookup"><span data-stu-id="12058-525">**NX_DNS_IPV6_NOT_SUPPORTED** (0xB3) Cannot process record with IPv6 disabled</span></span>
- <span data-ttu-id="12058-526">NX_PTR_ERROR (0x07) geçersiz IP veya DNS işaretçisi</span><span class="sxs-lookup"><span data-stu-id="12058-526">NX_PTR_ERROR (0x07) Invalid IP or DNS pointer</span></span>
- <span data-ttu-id="12058-527">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="12058-527">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>
- <span data-ttu-id="12058-528">NX_DNS_PARAM_ERROR (0xA8) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="12058-528">NX_DNS_PARAM_ERROR (0xA8) Invalid non pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="12058-529">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="12058-529">Allowed From</span></span>

<span data-ttu-id="12058-530">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="12058-530">Threads</span></span>

<span data-ttu-id="12058-531">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="12058-531">**Example**</span></span>
```C
UCHAR   resolved_name[200];
NXD_ADDRESS host_address;

host_address.nxd_ip_version = NX_IP_VERISON_V6;
host_address.nxd_ip_address.v6[0] = 0x20010db8;
host_address.nxd_ip_address.v6[1] = 0x0;
host_address.nxd_ip_address.v6[2] = 0xf101;
host_address.nxd_ip-address.v6[3] = 0x108;

/* Get the name associated with theinput host_address. */
status =  nxd_dns_host_by_address_get(&my_dns, &host_address,
                                      resolved_name, sizeof(resolved_name), 4000);

/* Check for DNS query error. */
if (status != NX_SUCCESS)
{
     error_counter++;
}     
else     
{
     printf("------------------------------------------------------\n");
     printf("Test PTR: %s\n", record_buffer);
}

/* If status is NX_SUCCESS the name associated with the IP address
   can be found in the resolved_name variable. */


[Output]

 ------------------------------------------------------
 Test PTR: my_example.net
```

## <a name="nx_dns_host_by_name_get"></a><span data-ttu-id="12058-532">nx_dns_host_by_name_get</span><span class="sxs-lookup"><span data-stu-id="12058-532">nx_dns_host_by_name_get</span></span>

<span data-ttu-id="12058-533">Ana bilgisayar adından bir IP adresi ara</span><span class="sxs-lookup"><span data-stu-id="12058-533">Look up an IP address from the host name</span></span>

### <a name="prototype"></a><span data-ttu-id="12058-534">Prototype</span><span class="sxs-lookup"><span data-stu-id="12058-534">Prototype</span></span>
```C
UINT nx_dns_host_by_name_get(NX_DNS *dns_ptr, UCHAR *host_name, 
                             ULONG *host_address_ptr, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="12058-535">Açıklama</span><span class="sxs-lookup"><span data-stu-id="12058-535">Description</span></span>

<span data-ttu-id="12058-536">Bu hizmet, uygulama tarafından daha önce belirtilen bir veya daha fazla DNS sunucusundan sağlanan adın ad çözümlemesini ister.</span><span class="sxs-lookup"><span data-stu-id="12058-536">This service requests name resolution of the supplied name from one or more DNS Servers previously specified by the application.</span></span> <span data-ttu-id="12058-537">Başarılı olursa, ilişkili IP adresi host_address_ptr tarafından işaret edilen hedefte döndürülür.</span><span class="sxs-lookup"><span data-stu-id="12058-537">If successful, the associated IP address is returned in the destination pointed to by host_address_ptr.</span></span> <span data-ttu-id="12058-538">Bu, *nxd_dns_host_by_name_get* hizmeti için bir sarmalayıcı Işlevidir ve IPv4 adresi girişi ile sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="12058-538">This is a wrapper function for the *nxd_dns_host_by_name_get* service, and is limited to IPv4 address input.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="12058-539">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="12058-539">Input Parameters</span></span>

- <span data-ttu-id="12058-540">**dns_ptr** Daha önce oluşturulan DNS örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="12058-540">**dns_ptr** Pointer to previously created DNS instance.</span></span>
- <span data-ttu-id="12058-541">**host_name** Ana bilgisayar adı işaretçisi</span><span class="sxs-lookup"><span data-stu-id="12058-541">**host_name** Pointer to host name</span></span>
- <span data-ttu-id="12058-542">**host_address_ptr** DNS sunucusu IP adresi döndürüldü</span><span class="sxs-lookup"><span data-stu-id="12058-542">**host_address_ptr** DNS Server IP address returned</span></span>
- <span data-ttu-id="12058-543">**wait_option** Hizmetin DNS çözümlemesi için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="12058-543">**wait_option** Defines how long the service will wait for the DNS resolution.</span></span> <span data-ttu-id="12058-544">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="12058-544">The wait options are defined as follows:</span></span>

  <span data-ttu-id="12058-545">zaman aşımı değeri (0x00000001-0xFFFFFFFE) TX_WAIT_FOREVER (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="12058-545">timeout value (0x00000001 through 0xFFFFFFFE) TX_WAIT_FOREVER (0xFFFFFFFF)</span></span>

  <span data-ttu-id="12058-546">TX_WAIT_FOREVER seçildiğinde çağıran iş parçacığının bir DNS sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="12058-546">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a DNS server responds to the request.</span></span>

  <span data-ttu-id="12058-547">Sayısal bir değer (1-0xFFFFFFFE) seçilmesi, DNS çözümlemesi beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="12058-547">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the DNS resolution.</span></span>

### <a name="return-values"></a><span data-ttu-id="12058-548">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="12058-548">Return Values</span></span>

- <span data-ttu-id="12058-549">**NX_SUCCESS** (0x00) başarılı DNS çözümlemesi.</span><span class="sxs-lookup"><span data-stu-id="12058-549">**NX_SUCCESS** (0x00) Successful DNS resolution.</span></span>
- <span data-ttu-id="12058-550">**NX_DNS_NO_SERVER** (0xA1) DNS sunucusu adresi belirtilmedi</span><span class="sxs-lookup"><span data-stu-id="12058-550">**NX_DNS_NO_SERVER** (0xA1) No DNS Server address specified</span></span>
- <span data-ttu-id="12058-551">**NX_DNS_QUERY_FAILED** (0xA3) sorguya yanıt almadı</span><span class="sxs-lookup"><span data-stu-id="12058-551">**NX_DNS_QUERY_FAILED** (0xA3) Received no response to query</span></span>
- <span data-ttu-id="12058-552">NX_DNS_PARAM_ERROR (0xA8) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="12058-552">NX_DNS_PARAM_ERROR (0xA8) Invalid non pointer input</span></span>
- <span data-ttu-id="12058-553">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="12058-553">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="12058-554">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="12058-554">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="12058-555">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="12058-555">Allowed From</span></span>

<span data-ttu-id="12058-556">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="12058-556">Threads</span></span>

<span data-ttu-id="12058-557">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="12058-557">**Example**</span></span>
```C
ULONG host_address;

/* Get the IP address for the name “www.my_example.com”. */
   status =  nx_dns_host_by_name_get(&my_dns, “www.my_example.com”, &host_address, 4000);

/* Check for DNS query error. */
if (status != NX_SUCCESS)
{
    error_counter++;
}

else     
{

    /* If status is NX_SUCCESS the IP address for “www.my_example.com” can be found 
        in the “ip_address” variable. */
        
    printf("------------------------------------------------------\n");
    printf("Test A: \n");
    printf("IP address: %d.%d.%d.%d\n",
    host_address >> 24,
    host_address >> 16 & 0xFF,                   
    host_address >> 8 & 0xFF,
    host_address & 0xFF);
}

[Output]
 ------------------------------------------------------
Test A: 
IP address: 192.2.2.10
```

## <a name="nxd_dns_host_by_name_get"></a><span data-ttu-id="12058-558">nxd_dns_host_by_name_get</span><span class="sxs-lookup"><span data-stu-id="12058-558">nxd_dns_host_by_name_get</span></span>

<span data-ttu-id="12058-559">Ana bilgisayar adından bir IP adresi ara</span><span class="sxs-lookup"><span data-stu-id="12058-559">Lookup an IP address from the host name</span></span>

### <a name="prototype"></a><span data-ttu-id="12058-560">Prototype</span><span class="sxs-lookup"><span data-stu-id="12058-560">Prototype</span></span>
```C
UINT nxd_dns_host_by_name_get(NX_DNS *dns_ptr, ULONG *host_name, 
                              NXD_ADDRESS *host_address_ptr, 
                              ULONG wait_option, UINT lookup_type);
```

### <a name="description"></a><span data-ttu-id="12058-561">Açıklama</span><span class="sxs-lookup"><span data-stu-id="12058-561">Description</span></span>

<span data-ttu-id="12058-562">Bu hizmet, uygulama tarafından daha önce belirtilen bir veya daha fazla DNS sunucusundan sağlanan IP adresinin ad çözümlemesini ister.</span><span class="sxs-lookup"><span data-stu-id="12058-562">This service requests name resolution of the supplied IP address from one or more DNS Servers previously specified by the application.</span></span> <span data-ttu-id="12058-563">Başarılı olursa, ilişkili IP adresi *host_address_ptr* tarafından işaret edilen bir NXD_ADDRESS döndürülür.</span><span class="sxs-lookup"><span data-stu-id="12058-563">If successful, the associated IP address is returned in an NXD_ADDRESS pointed to by *host_address_ptr*.</span></span> <span data-ttu-id="12058-564">Çağıran lookup_type girişi özel olarak NX_IP_VERSION_V6 olarak ayarladığında, bu hizmet bir ana bilgisayar IPv6 adresi (AAAA kaydı) için sorgu gönderir.</span><span class="sxs-lookup"><span data-stu-id="12058-564">If the caller specifically sets the lookup_type input to NX_IP_VERSION_V6, this service will send out query for a host IPv6 address (AAAA record).</span></span> <span data-ttu-id="12058-565">Çağıran lookup_type girişi özel olarak NX_IP_VERSION_V4 olarak ayarladığında, bu hizmet bir ana bilgisayar IPv4 adresi (bir kayıt) için sorgu gönderir.</span><span class="sxs-lookup"><span data-stu-id="12058-565">If the caller specifically sets the lookup_type input to NX_IP_VERSION_V4, this service will send out query for a host IPv4 address (A record).</span></span>

### <a name="input-parameters"></a><span data-ttu-id="12058-566">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="12058-566">Input Parameters</span></span>

- <span data-ttu-id="12058-567">**dns_ptr** Daha önce oluşturulan DNS Istemci örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="12058-567">**dns_ptr** Pointer to previously created DNS Client instance.</span></span>
- <span data-ttu-id="12058-568">**host_name** IP adresi bulmak için ana bilgisayar adı işaretçisi</span><span class="sxs-lookup"><span data-stu-id="12058-568">**host_name** Pointer to host name to find an IP address of</span></span>
- <span data-ttu-id="12058-569">**host_address_ptr** IP adresini içeren NXD_ADDRESS hedefi işaretçisi</span><span class="sxs-lookup"><span data-stu-id="12058-569">**host_address_ptr** Pointer to destination for NXD_ADDRESS containing the IP address</span></span>
- <span data-ttu-id="12058-570">**wait_option** Hizmetin her sorgu iletimi ve yeniden aktarım için DNS sunucusu yanıtı için Zamanlayıcı işaretlerini ne kadar bekleyeceğini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="12058-570">**wait_option** Defines how long the service will wait in timer ticks for the DNS Server response for each query transmission and retransmission.</span></span> <span data-ttu-id="12058-571">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="12058-571">The wait options are defined as follows:</span></span>

  <span data-ttu-id="12058-572">zaman aşımı değeri (0x00000001-0xFFFFFFFE) TX_WAIT_FOREVER (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="12058-572">timeout value (0x00000001 through 0xFFFFFFFE) TX_WAIT_FOREVER (0xFFFFFFFF)</span></span>  

  <span data-ttu-id="12058-573">TX_WAIT_FOREVER seçildiğinde çağıran iş parçacığının bir DNS sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="12058-573">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a DNS Server responds to the request.</span></span>

  <span data-ttu-id="12058-574">Sayısal bir değer (1-0xFFFFFFFE) seçilmesi, DNS çözümlemesi beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="12058-574">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the DNS resolution.</span></span>

- <span data-ttu-id="12058-575">**lookup_type** Arama türünü belirtin (bir vs AAAA).</span><span class="sxs-lookup"><span data-stu-id="12058-575">**lookup_type** Indicate type of lookup (A vs AAAA).</span></span>

### <a name="return-values"></a><span data-ttu-id="12058-576">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="12058-576">Return Values</span></span>

- <span data-ttu-id="12058-577">**NX_SUCCESS** (0x00) başarılı DNS çözümlemesi.</span><span class="sxs-lookup"><span data-stu-id="12058-577">**NX_SUCCESS** (0x00) Successful DNS resolution.</span></span>
- <span data-ttu-id="12058-578">**NX_DNS_NO_SERVER** (0xA1) DNS sunucusu adresi belirtilmedi</span><span class="sxs-lookup"><span data-stu-id="12058-578">**NX_DNS_NO_SERVER** (0xA1) No DNS Server address specified</span></span>
- <span data-ttu-id="12058-579">**NX_DNS_QUERY_FAILED** (0xA3) sorguya yanıt almadı</span><span class="sxs-lookup"><span data-stu-id="12058-579">**NX_DNS_QUERY_FAILED** (0xA3) Received no response to query</span></span>
- <span data-ttu-id="12058-580">**NX_DNS_BAD_ADDRESS_ERROR** (0xa4) null giriş adresi</span><span class="sxs-lookup"><span data-stu-id="12058-580">**NX_DNS_BAD_ADDRESS_ERROR** (0xA4) Null input address</span></span>
- <span data-ttu-id="12058-581">**NX_DNS_IPV6_NOT_SUPPORTED** (0xb3) IPv6 devre dışı olarak kayıt işlenemiyor</span><span class="sxs-lookup"><span data-stu-id="12058-581">**NX_DNS_IPV6_NOT_SUPPORTED** (0xB3) Cannot process record with IPv6 disabled</span></span>
- <span data-ttu-id="12058-582">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="12058-582">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="12058-583">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="12058-583">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>
- <span data-ttu-id="12058-584">NX_DNS_PARAM_ERROR (0xA8) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="12058-584">NX_DNS_PARAM_ERROR (0xA8) Invalid non pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="12058-585">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="12058-585">Allowed From</span></span>

<span data-ttu-id="12058-586">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="12058-586">Threads</span></span>

<span data-ttu-id="12058-587">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="12058-587">**Example**</span></span>
```C
NXD_ADDRESS host_ipduo_address;

/* Create an AAAA query to obtain the IPv6 address for the host “www.my_example.com”. */
status =  nxd_dns_host_by_name_get(&my_dns, “www.my_example.com”, 
                                   &host_ipduo_address, 4000, 
                                   NX_IP_VERSION_V6);

if (status != NX_SUCCESS)
{
        error_counter++;
}
else
{
/* If status is NX_SUCCESS the IP address for “www.my_example.com” can be 
   found in the “ip_address” variable. */

    printf("------------------------------------------------------\n");
    printf("Test AAAA: \n");

    printf("IP address: %x:%x:%x:%x:%x:%x:%x:%x\n", 
           host_ipduo_address.nxd_ip_address.v6[0]  >>16 & 0xFFFF,
           host_ipduo_address.nxd_ip_address.v6[0]  & 0xFFFF,
           host_ipduo_address.nxd_ip_address.v6[1]  >>16 & 0xFFFF,
           host_ipduo_address.nxd_ip_address.v6[1]  & 0xFFFF,
           host_ipduo_address.nxd_ip_address.v6[2]  >>16 & 0xFFFF,
           host_ipduo_address.nxd_ip_address.v6[2]  & 0xFFFF,
           host_ipduo_address.nxd_ip_address.v6[3]  >>16 & 0xFFFF,
           host_ipduo_address.nxd_ip_address.v6[3]  & 0xFFFF);
}

[Output]

------------------------------------------------------
Test AAAA: 
IP address: 2607:f8b0:4007:800:0:0:0:1008
```

<span data-ttu-id="12058-588">Bu zaman hizmetini kullanmanın başka bir örneği olan bu kez IPv4 adreslerini ve kayıt türlerini kullanarak aşağıda gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="12058-588">Another example of using this time service, this time using IPv4 addresses and A record types, is shown below:</span></span>
```C
/* Create a query to obtain the IPv4 address for the host “www.my_example.com”. */
status =  nxd_dns_host_by_name_get(&my_dns, “www.my_example.com”, &ip_address, 4000, 
                                   NX_IP_VERSION_V4);

/* Check for DNS query error. */
if (status != NX_SUCCESS)
{
    error_counter++;
}
else     
{   
/* If status is NX_SUCCESS the IP address for “www.my_example.com” can be 
   found in the “ip_address” variable. */
  
     printf("------------------------------------------------------\n");
     printf("Test A: \n");
     printf("IP address: %d.%d.%d.%d\n",
            host_ipduo_address.nxd_ip_address.v4 >> 24,
            host_ipduo_address.nxd_ip_address.v4 >> 16 & 0xFF,                   
            host_ipduo_address.nxd_ip_address.v4 >> 8 & 0xFF,
            host_ipduo_address.nxd_ip_address.v4 & 0xFF);
 }

[Output]

------------------------------------------------------
Test A: 
IP address: 192.2.2.10
```

## <a name="nx_dns_host_text_get"></a><span data-ttu-id="12058-589">nx_dns_host_text_get</span><span class="sxs-lookup"><span data-stu-id="12058-589">nx_dns_host_text_get</span></span>

<span data-ttu-id="12058-590">Giriş etki alanı adı için metin dizesini arayın</span><span class="sxs-lookup"><span data-stu-id="12058-590">Look up the text string for the input domain name</span></span>

### <a name="prototype"></a><span data-ttu-id="12058-591">Prototype</span><span class="sxs-lookup"><span data-stu-id="12058-591">Prototype</span></span>
```C
UINT nx_dns_host_text_get(NX_DNS *dns_ptr, UCHAR *host_name, 
                          UCHAR *record_buffer, 
                          UINT buffer_size, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="12058-592">Açıklama</span><span class="sxs-lookup"><span data-stu-id="12058-592">Description</span></span>

<span data-ttu-id="12058-593">Bu hizmet, rastgele dize verileri elde etmek için belirtilen etki alanı adı ve arabellekle TXT türünde bir sorgu gönderir.</span><span class="sxs-lookup"><span data-stu-id="12058-593">This service sends a query of type TXT with the specified domain name and buffer to obtain the arbitrary string data.</span></span>

<span data-ttu-id="12058-594">DNS Istemcisi, DNS sunucusu yanıtındaki TXT kaydındaki metin dizesini *record_buffer* bellek konumuna kopyalar.</span><span class="sxs-lookup"><span data-stu-id="12058-594">The DNS Client copies the text string in the TXT record in the DNS Server response into the *record_buffer* memory location.</span></span> 

> [!NOTE]
> <span data-ttu-id="12058-595">Record_buffer verileri almak için 4 baytlık hizalı olması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="12058-595">The record_buffer does not need to be 4-byte aligned to receive the data.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="12058-596">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="12058-596">Input Parameters</span></span>

- <span data-ttu-id="12058-597">**dns_ptr** DNS Istemcisi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="12058-597">**dns_ptr** Pointer to DNS Client.</span></span>  
- <span data-ttu-id="12058-598">**host_name** Arama yapılacak konağın adı işaretçisi</span><span class="sxs-lookup"><span data-stu-id="12058-598">**host_name** Pointer to name of host to search on</span></span>
- <span data-ttu-id="12058-599">**record_buffer** TXT verilerinin ayıklanacağı konum işaretçisi</span><span class="sxs-lookup"><span data-stu-id="12058-599">**record_buffer** Pointer to location to extract TXT data into</span></span>
- <span data-ttu-id="12058-600">**Buffer_size** TXT verilerini tutan arabelleğin boyutu</span><span class="sxs-lookup"><span data-stu-id="12058-600">**buffer_size** Size of buffer to hold TXT data</span></span>
- <span data-ttu-id="12058-601">**wait_option** DNS sunucusu yanıtı alma seçeneğini bekle</span><span class="sxs-lookup"><span data-stu-id="12058-601">**wait_option** Wait option to receive DNS Server response</span></span>

### <a name="return-values"></a><span data-ttu-id="12058-602">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="12058-602">Return Values</span></span>

- <span data-ttu-id="12058-603">**NX_SUCCESS** (0x00) başarılı bir txt dizesi alındı</span><span class="sxs-lookup"><span data-stu-id="12058-603">**NX_SUCCESS** (0x00) Successfully TXT string obtained</span></span>
- <span data-ttu-id="12058-604">**NX_DNS_NO_SERVER** (0xA1) istemci sunucu listesi boş</span><span class="sxs-lookup"><span data-stu-id="12058-604">**NX_DNS_NO_SERVER** (0xA1) Client server list is empty</span></span>
- <span data-ttu-id="12058-605">**NX_DNS_QUERY_FAILED** (0xA3) GEÇERLI bir DNS yanıtı alınmadı</span><span class="sxs-lookup"><span data-stu-id="12058-605">**NX_DNS_QUERY_FAILED** (0xA3) No valid DNS response received</span></span>
- <span data-ttu-id="12058-606">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="12058-606">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="12058-607">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="12058-607">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>
- <span data-ttu-id="12058-608">NX_DNS_PARAM_ERROR (0xA8) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="12058-608">NX_DNS_PARAM_ERROR (0xA8) Invalid non pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="12058-609">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="12058-609">Allowed From</span></span>

<span data-ttu-id="12058-610">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="12058-610">Threads</span></span>

######   
<span data-ttu-id="12058-611">Örnek</span><span class="sxs-lookup"><span data-stu-id="12058-611">Example</span></span>
```C
CHAR            record_buffer[50];

/* Request the text string for the specified host. */
status =  nx_dns_host_text_get(&client_dns, (UCHAR *)"www.my_example.com", 
                               record_buffer, 
                               sizeof(record_buffer), 500);


/* Check for DNS query error. */
if (status != NX_SUCCESS)
{
     error_counter++;
}
else     
{
    /* If status is NX_SUCCESS a DNS query was successfully completed and the
       text string is returned in record_buffer. */
 
     printf("------------------------------------------------------\n");
     printf("Test TXT:\n %s\n", record_buffer);
} 


[Output]

------------------------------------------------------
Test TXT: 
v=spf1 include:_www.my_example.com ip4:192.2.2.10/31 ip4:192.2.2.11/31 ~all
```

## <a name="nx_dns_packet_pool_set"></a><span data-ttu-id="12058-612">nx_dns_packet_pool_set</span><span class="sxs-lookup"><span data-stu-id="12058-612">nx_dns_packet_pool_set</span></span>

<span data-ttu-id="12058-613">DNS Istemcisi paket havuzunu ayarlama</span><span class="sxs-lookup"><span data-stu-id="12058-613">Set the DNS Client packet pool</span></span>

### <a name="prototype"></a><span data-ttu-id="12058-614">Prototype</span><span class="sxs-lookup"><span data-stu-id="12058-614">Prototype</span></span>
```C
UINT nx_dns_packet_pool_set(NX_DNS *dns_ptr, NX_PACKET_POOL *pool_ptr);
```
### <a name="description"></a><span data-ttu-id="12058-615">Açıklama</span><span class="sxs-lookup"><span data-stu-id="12058-615">Description</span></span>

<span data-ttu-id="12058-616">Bu hizmet, daha önce oluşturulmuş bir paket havuzunu DNS Istemcisi paket havuzu olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="12058-616">This service sets a previously created packet pool as the DNS Client packet pool.</span></span> <span data-ttu-id="12058-617">DNS Istemcisi, DNS sorguları göndermek için bu paket havuzunu kullanır, bu nedenle paket yükü, Ethernet, IP ve UDP üst bilgilerini içeren ve *nxd_dns. h* içinde tanımlanan NX_DNS_PACKET_PAYLOAD daha az olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="12058-617">The DNS Client will use this packet pool to send DNS queries, so the packet payload should not be less than NX_DNS_PACKET_PAYLOAD which includes the Ethernet, IP and UDP headers and is defined in *nxd_dns.h.*</span></span> 

> [!NOTE]
> <span data-ttu-id="12058-618">DNS istemcisi silindiğinde, paket havuzu onunla silinmez ve artık ihtiyaç duyulmuyorsa, paket havuzunu silmek uygulamanın sorumluluğundadır.</span><span class="sxs-lookup"><span data-stu-id="12058-618">*W* hen the DNS Client is deleted, the packet pool is not deleted with it and it is the responsibility of the application to delete the packet pool when it no longer needs it.</span></span>
>
> <span data-ttu-id="12058-619">Bu hizmet yalnızca yapılandırma seçeneği NX_DNS_CLIENT_USER_CREATE_PACKET_POOL *nxd_dns. h* içinde tanımlanmışsa kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="12058-619">This service is only available if the configuration option NX_DNS_CLIENT_USER_CREATE_PACKET_POOL is defined in *nxd_dns.h*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="12058-620">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="12058-620">Input Parameters</span></span>

- <span data-ttu-id="12058-621">**dns_ptr** Daha önce oluşturulan DNS Istemci örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="12058-621">**dns_ptr** Pointer to previously created DNS Client instance.</span></span>
- <span data-ttu-id="12058-622">**pool_ptr** Önceden oluşturulmuş paket havuzuna yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="12058-622">**pool_ptr** Pointer to previously created packet pool</span></span>

### <a name="return-values"></a><span data-ttu-id="12058-623">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="12058-623">Return Values</span></span>

- <span data-ttu-id="12058-624">**NX_SUCCESS** (0x00) başarılı tamamlama.</span><span class="sxs-lookup"><span data-stu-id="12058-624">**NX_SUCCESS** (0x00) Successful completion.</span></span>
- <span data-ttu-id="12058-625">Bu seçenek için **NX_NOT_ENABLED** (0x14) istemci yapılandırılmadı</span><span class="sxs-lookup"><span data-stu-id="12058-625">**NX_NOT_ENABLED** (0x14) Client not configured for this option</span></span>
- <span data-ttu-id="12058-626">NX_PTR_ERROR (0x07) geçersiz IP veya DNS Istemci işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="12058-626">NX_PTR_ERROR (0x07) Invalid IP or DNS Client pointer.</span></span>
- <span data-ttu-id="12058-627">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="12058-627">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="12058-628">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="12058-628">Allowed From</span></span>

<span data-ttu-id="12058-629">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="12058-629">Threads</span></span>

### <a name="example"></a><span data-ttu-id="12058-630">Örnek</span><span class="sxs-lookup"><span data-stu-id="12058-630">Example</span></span>
```C
NXD_DNS my_dns;
NX_PACKET_POOL client_pool;
NX_IP *ip_ptr;


/* Create the DNS Client. */
status =  nx_dns_create(&my_dns, ip_ptr, “My DNS Client”);

/* Create a packet pool for the DNS Client. */
status =  nx_packet_pool_create(&client_pool, "DNS Client Packet Pool", 
                                NX_DNS_PACKET_PAYLOAD, free_mem_pointer, 
                                NX_DNS_PACKET_POOL_SIZE);

/* Set the DNS Client packet pool. */
status =  nx_dns_packet_pool_set(&my_dns, &client_pool);

/* If status is NX_SUCCESS the DNS Client packet pool was successfully set. */
```

## <a name="nx_dns_server_add"></a><span data-ttu-id="12058-631">nx_dns_server_add</span><span class="sxs-lookup"><span data-stu-id="12058-631">nx_dns_server_add</span></span>

<span data-ttu-id="12058-632">DNS sunucusu IP adresi ekle</span><span class="sxs-lookup"><span data-stu-id="12058-632">Add DNS Server IP Address</span></span>

### <a name="prototype"></a><span data-ttu-id="12058-633">Prototype</span><span class="sxs-lookup"><span data-stu-id="12058-633">Prototype</span></span>
```C
UINT nx_dns_server_add(NX_DNS *dns_ptr, ULONG server_address);
```
### <a name="description"></a><span data-ttu-id="12058-634">Açıklama</span><span class="sxs-lookup"><span data-stu-id="12058-634">Description</span></span>

<span data-ttu-id="12058-635">Bu hizmet, sunucu listesine bir IPv4 DNS sunucusu ekler.</span><span class="sxs-lookup"><span data-stu-id="12058-635">This service adds an IPv4 DNS Server to the server list.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="12058-636">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="12058-636">Input Parameters</span></span>

- <span data-ttu-id="12058-637">**dns_ptr** DNS denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="12058-637">**dns_ptr** Pointer to DNS control block.</span></span>  
- <span data-ttu-id="12058-638">**server_address** DNS sunucusunun IP adresi</span><span class="sxs-lookup"><span data-stu-id="12058-638">**server_address** IP address of DNS Server</span></span>

### <a name="return-values"></a><span data-ttu-id="12058-639">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="12058-639">Return Values</span></span>

- <span data-ttu-id="12058-640">**NX_SUCCESS** (0x00) sunucu başarıyla eklendi</span><span class="sxs-lookup"><span data-stu-id="12058-640">**NX_SUCCESS** (0x00) Server successfully added</span></span>
- <span data-ttu-id="12058-641">**NX_DNS_DUPLICATE_ENTRY**</span><span class="sxs-lookup"><span data-stu-id="12058-641">**NX_DNS_DUPLICATE_ENTRY**</span></span>  
<span data-ttu-id="12058-642">**NX_NO_MORE_ENTRIES** (0x17) daha fazla DNS sunucusu izin verilmiyor (liste dolu)</span><span class="sxs-lookup"><span data-stu-id="12058-642">**NX_NO_MORE_ENTRIES** (0x17) No more DNS Servers Allowed (list is full)</span></span>
- <span data-ttu-id="12058-643">**NX_DNS_PARAM_ERROR** (0Xa8) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="12058-643">**NX_DNS_PARAM_ERROR** (0xA8) Invalid non pointer input</span></span>
- <span data-ttu-id="12058-644">**NX_DNS_IPV6_NOT_SUPPORTED** (0xb3) IPv6 devre dışı olarak kayıt işlenemiyor</span><span class="sxs-lookup"><span data-stu-id="12058-644">**NX_DNS_IPV6_NOT_SUPPORTED** (0xB3) Cannot process record with IPv6 disabled</span></span>
- <span data-ttu-id="12058-645">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="12058-645">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="12058-646">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="12058-646">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>
- <span data-ttu-id="12058-647">NX_DNS_BAD_ADDRESS_ERROR (0xA4) null sunucu adresi girişi</span><span class="sxs-lookup"><span data-stu-id="12058-647">NX_DNS_BAD_ADDRESS_ERROR (0xA4) Null server address input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="12058-648">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="12058-648">Allowed From</span></span>

<span data-ttu-id="12058-649">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="12058-649">Threads</span></span>

### <a name="example"></a><span data-ttu-id="12058-650">Örnek</span><span class="sxs-lookup"><span data-stu-id="12058-650">Example</span></span>
```C
/* Add a DNS Server at IP address 202.2.2.13. */
status =  nx_dns_server_add(&my_dns, IP_ADDRESS(202,2,2,13));

/* If status is NX_SUCCESS a DNS Server was successfully added. */
```

## <a name="nxd_dns_server_add"></a><span data-ttu-id="12058-651">nxd_dns_server_add</span><span class="sxs-lookup"><span data-stu-id="12058-651">nxd_dns_server_add</span></span>

<span data-ttu-id="12058-652">Istemci listesine DNS sunucusu Ekle</span><span class="sxs-lookup"><span data-stu-id="12058-652">Add DNS Server to the Client list</span></span>

### <a name="prototype"></a><span data-ttu-id="12058-653">Prototype</span><span class="sxs-lookup"><span data-stu-id="12058-653">Prototype</span></span>
```C
UINT nxd_dns_server_add(NX_DNS *dns_ptr, NXD_ADDRESS *server_address);
```
### <a name="description"></a><span data-ttu-id="12058-654">Açıklama</span><span class="sxs-lookup"><span data-stu-id="12058-654">Description</span></span>

<span data-ttu-id="12058-655">Bu hizmet, DNS sunucusunun IP adresini DNS Istemci sunucusu listesine ekler.</span><span class="sxs-lookup"><span data-stu-id="12058-655">This service adds the IP address of a DNS server to the DNS Client server list.</span></span> <span data-ttu-id="12058-656">Server_address bir IPv4 veya IPv6 adresi olabilir.</span><span class="sxs-lookup"><span data-stu-id="12058-656">The server_address may be either an IPv4 or IPv6 address.</span></span> <span data-ttu-id="12058-657">Istemci, IPv4 adresi veya IPv6 adresiyle aynı sunucuya erişebiliyorsa, sunucu listesine her iki IP adresini de girdi olarak eklemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="12058-657">If the Client wishes to be able to access the same server by either its IPv4 address or IPv6 address it should add both IP addresses as entries to the server list.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="12058-658">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="12058-658">Input Parameters</span></span>

- <span data-ttu-id="12058-659">**dns_ptr** DNS denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="12058-659">**dns_ptr** Pointer to DNS control block.</span></span>
- <span data-ttu-id="12058-660">**server_address** DNS sunucusunun sunucu IP adresini içeren NXD_ADDRESS işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="12058-660">**server_address** Pointer to the NXD_ADDRESS containing the server IP address of DNS Server.</span></span>

### <a name="return-values"></a><span data-ttu-id="12058-661">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="12058-661">Return Values</span></span>

- <span data-ttu-id="12058-662">**NX_SUCCESS** (0x00) sunucu başarıyla eklendi</span><span class="sxs-lookup"><span data-stu-id="12058-662">**NX_SUCCESS** (0x00) Server successfully added</span></span>
- <span data-ttu-id="12058-663">**NX_DNS_DUPLICATE_ENTRY**</span><span class="sxs-lookup"><span data-stu-id="12058-663">**NX_DNS_DUPLICATE_ENTRY**</span></span>  
<span data-ttu-id="12058-664">**NX_NO_MORE_ENTRIES** (0x17) daha fazla DNS sunucusu izin verilmiyor (liste dolu)</span><span class="sxs-lookup"><span data-stu-id="12058-664">**NX_NO_MORE_ENTRIES** (0x17) No more DNS Servers allowed (list is full)</span></span> 
- <span data-ttu-id="12058-665">**NX_DNS_IPV6_NOT_SUPPORTED** (0xb3) IPv6 devre dışı olarak kayıt işlenemiyor</span><span class="sxs-lookup"><span data-stu-id="12058-665">**NX_DNS_IPV6_NOT_SUPPORTED** (0xB3) Cannot process record with IPv6 disabled</span></span>
- <span data-ttu-id="12058-666">**NX_DNS_PARAM_ERROR** (0Xa8) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="12058-666">**NX_DNS_PARAM_ERROR** (0xA8) Invalid non pointer input</span></span>
- <span data-ttu-id="12058-667">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="12058-667">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="12058-668">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="12058-668">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>
- <span data-ttu-id="12058-669">NX_DNS_BAD_ADDRESS_ERROR (0xA4) null sunucu adresi girişi</span><span class="sxs-lookup"><span data-stu-id="12058-669">NX_DNS_BAD_ADDRESS_ERROR (0xA4) Null server address input</span></span>
- <span data-ttu-id="12058-670">NX_DNS_INVALID_ADDRESS_TYPE (0xB2) dizin noktaları geçersiz adres türüne (örn. IPv6)</span><span class="sxs-lookup"><span data-stu-id="12058-670">NX_DNS_INVALID_ADDRESS_TYPE (0xB2) Index points to invalid address type (e.g. IPv6)</span></span>

### <a name="allowed-from"></a><span data-ttu-id="12058-671">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="12058-671">Allowed From</span></span>

<span data-ttu-id="12058-672">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="12058-672">Threads</span></span>

### <a name="example"></a><span data-ttu-id="12058-673">Örnek</span><span class="sxs-lookup"><span data-stu-id="12058-673">Example</span></span>
```C
NXD_ADDRESS server_address;

server_address.nxd_ip_version = NX_IP_VERISON_V6;
server_address.nxd_ip_address.v6[0] = 0x20010db8;
server_address.nxd_ip_address.v6[1] = 0x0;
server_address.nxd_ip_address.v6[2] = 0xf101;
server_address.nxd_ip-address.v6[3] = 0x108;


/* Add a DNS Server with the IP address pointed to by the server_address input. */
status =  nxd_dns_server_add(&my_dns, &server_address);

/* If status is NX_SUCCESS a DNS Server was successfully added. */
```

## <a name="nx_dns_server_get"></a><span data-ttu-id="12058-674">nx_dns_server_get</span><span class="sxs-lookup"><span data-stu-id="12058-674">nx_dns_server_get</span></span>

<span data-ttu-id="12058-675">Istemci listesinden bir IPv4 DNS sunucusu döndürme</span><span class="sxs-lookup"><span data-stu-id="12058-675">Return an IPv4 DNS Server from the Client list</span></span>

### <a name="prototype"></a><span data-ttu-id="12058-676">Prototype</span><span class="sxs-lookup"><span data-stu-id="12058-676">Prototype</span></span>
```C
UINT nx_dns_server_get(NX_DNS *dns_ptr, UINT index, 
                        ULONG *dns_server_address);
```

### <a name="description"></a><span data-ttu-id="12058-677">Açıklama</span><span class="sxs-lookup"><span data-stu-id="12058-677">Description</span></span>

<span data-ttu-id="12058-678">Bu hizmet, belirtilen dizindeki sunucu listesinden IPv4 DNS sunucusu adresini döndürür.</span><span class="sxs-lookup"><span data-stu-id="12058-678">This service returns the IPv4 DNS Server address from the server list at the specified index.</span></span> 

> [!NOTE]
> <span data-ttu-id="12058-679">Dizin sıfır tabanlıdır.</span><span class="sxs-lookup"><span data-stu-id="12058-679">The index is zero based.</span></span> <span data-ttu-id="12058-680">Giriş dizini DNS Istemci listesinin boyutunu aşarsa, o dizinde bir IPv6 adresi bulunur veya belirtilen dizinde null bir adres bulunur, bir hata döndürülür.</span><span class="sxs-lookup"><span data-stu-id="12058-680">If the input index exceeds the size of the DNS Client list, an IPv6 address is found at that index or a null address is found at the specified index, an error is returned.</span></span> <span data-ttu-id="12058-681">*Nx_dns_get_serverlist_size* hizmeti Ilk olarak ISTEMCI listesindeki DNS sunucularının sayısını elde edebilir.</span><span class="sxs-lookup"><span data-stu-id="12058-681">The *nx_dns_get_serverlist_size* service may be called first obtain the number of DNS servers in the Client list.</span></span>

<span data-ttu-id="12058-682">Bu hizmet yalnızca IPv4 adreslerini destekler.</span><span class="sxs-lookup"><span data-stu-id="12058-682">This service does only supports IPv4 addresses.</span></span> <span data-ttu-id="12058-683">Hem IPv4 hem de IPv6 adreslerini destekleyen *nxd_dns_server_get* hizmetini çağırır.</span><span class="sxs-lookup"><span data-stu-id="12058-683">It calls the *nxd_dns_server_get* service which supports both IPv4 and IPv6 addresses.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="12058-684">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="12058-684">Input Parameters</span></span>

- <span data-ttu-id="12058-685">**dns_ptr** DNS denetim bloğu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="12058-685">**dns_ptr** Pointer to DNS control block</span></span>  
- <span data-ttu-id="12058-686">**Dizin** DNS Istemcisinin sunucu listesini dizine ekleyin</span><span class="sxs-lookup"><span data-stu-id="12058-686">**index** Index into DNS Client’s list of servers</span></span>
- <span data-ttu-id="12058-687">**dns_server_address** DNS sunucusunun IP adresi işaretçisi</span><span class="sxs-lookup"><span data-stu-id="12058-687">**dns_server_address** Pointer to IP address of DNS Server</span></span>

### <a name="return-values"></a><span data-ttu-id="12058-688">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="12058-688">Return Values</span></span>

- <span data-ttu-id="12058-689">**NX_SUCCESS** (0x00) başarılı sunucu döndürüldü</span><span class="sxs-lookup"><span data-stu-id="12058-689">**NX_SUCCESS** (0x00) Successful server returned</span></span>
- <span data-ttu-id="12058-690">Boş yuvaya **NX_DNS_SERVER_NOT_FOUND** (0xA9) dizin noktaları</span><span class="sxs-lookup"><span data-stu-id="12058-690">**NX_DNS_SERVER_NOT_FOUND** (0xA9) Index points to empty slot</span></span>
- <span data-ttu-id="12058-691">**NX_DNS_BAD_ADDRESS_ERROR** (0xa4) boş adrese ait dizin noktaları</span><span class="sxs-lookup"><span data-stu-id="12058-691">**NX_DNS_BAD_ADDRESS_ERROR** (0xA4) Index points to Null address</span></span>
- <span data-ttu-id="12058-692">**NX_DNS_INVALID_ADDRESS_TYPE** (0xB2) dizin noktaları geçersiz adres türüne (örn. IPv6)</span><span class="sxs-lookup"><span data-stu-id="12058-692">**NX_DNS_INVALID_ADDRESS_TYPE** (0xB2) Index points to invalid address type (e.g. IPv6)</span></span>
- <span data-ttu-id="12058-693">**NX_DNS_PARAM_ERROR** (0Xa8) geçersiz işaretçi olmayan giriş</span><span class="sxs-lookup"><span data-stu-id="12058-693">**NX_DNS_PARAM_ERROR** (0xA8) Invalid non-pointer input</span></span>
- <span data-ttu-id="12058-694">NX_PTR_ERROR (0x07) geçersiz IP veya DNS işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="12058-694">NX_PTR_ERROR (0x07) Invalid IP or DNS pointer.</span></span>
- <span data-ttu-id="12058-695">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="12058-695">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="12058-696">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="12058-696">Allowed From</span></span>

<span data-ttu-id="12058-697">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="12058-697">Threads</span></span>

### <a name="example"></a><span data-ttu-id="12058-698">Örnek</span><span class="sxs-lookup"><span data-stu-id="12058-698">Example</span></span>
```C
ULONG my_server_address;

/* Get the DNS Server at index 5 (zero based) into the Client list. */
status =  nx_dns_server_get(&my_dns, 5, &my_server_addres);

/* If status is NX_SUCCESS a DNS Server was successfully
   returned. */
```

## <a name="nxd_dns_server_get"></a><span data-ttu-id="12058-699">nxd_dns_server_get</span><span class="sxs-lookup"><span data-stu-id="12058-699">nxd_dns_server_get</span></span>

<span data-ttu-id="12058-700">Istemci listesinden bir DNS sunucusu döndürme</span><span class="sxs-lookup"><span data-stu-id="12058-700">Return a DNS Server from the Client list</span></span>

### <a name="prototype"></a><span data-ttu-id="12058-701">Prototype</span><span class="sxs-lookup"><span data-stu-id="12058-701">Prototype</span></span>
```C
UINT nxd_dns_server_get(NX_DNS *dns_ptr, UINT index, 
                        NXD_ADDRESS *dns_server_address);
```

### <a name="description"></a><span data-ttu-id="12058-702">Açıklama</span><span class="sxs-lookup"><span data-stu-id="12058-702">Description</span></span>

<span data-ttu-id="12058-703">Bu hizmet, belirtilen dizindeki sunucu listesinden DNS sunucusu IP adresini döndürür.</span><span class="sxs-lookup"><span data-stu-id="12058-703">This service returns the DNS Server IP address from the server list at the specified index.</span></span> 

> [!NOTE]
> <span data-ttu-id="12058-704">Dizin sıfır tabanlıdır.</span><span class="sxs-lookup"><span data-stu-id="12058-704">The index is zero based.</span></span> <span data-ttu-id="12058-705">Giriş dizini DNS Istemci listesinin boyutunu aşarsa veya belirtilen dizinde null bir adres bulunursa bir hata döndürülür.</span><span class="sxs-lookup"><span data-stu-id="12058-705">If the input index exceeds the size of the DNS Client list, or a null address is found at the specified index, an error is returned.</span></span> <span data-ttu-id="12058-706">Sunucu listesindeki DNS sunucularının sayısını almak için öncelikle *nx_dns_get_serverlist_size* hizmeti çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="12058-706">The *nx_dns_get_serverlist_size* service may be called first to obtain the number of DNS servers in the server list.</span></span>

<span data-ttu-id="12058-707">Bu hizmet, IPv4 ve IPv6 adreslerini destekler.</span><span class="sxs-lookup"><span data-stu-id="12058-707">This service supports IPv4 and IPv6 addresses.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="12058-708">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="12058-708">Input Parameters</span></span>

- <span data-ttu-id="12058-709">**dns_ptr** DNS denetim bloğu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="12058-709">**dns_ptr** Pointer to DNS control block</span></span>  
- <span data-ttu-id="12058-710">**Dizin** DNS Istemcisinin sunucu listesini dizine ekleyin</span><span class="sxs-lookup"><span data-stu-id="12058-710">**index** Index into DNS Client’s list of servers</span></span>
- <span data-ttu-id="12058-711">**dns_server_address** DNS sunucusunun IP adresi işaretçisi</span><span class="sxs-lookup"><span data-stu-id="12058-711">**dns_server_address** Pointer to IP address of DNS Server</span></span>

### <a name="return-values"></a><span data-ttu-id="12058-712">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="12058-712">Return Values</span></span>

- <span data-ttu-id="12058-713">**NX_SUCCESS** (0x00) sunucu IP adresini başarıyla döndürdü</span><span class="sxs-lookup"><span data-stu-id="12058-713">**NX_SUCCESS** (0x00) Successfully returned server IP address</span></span>
- <span data-ttu-id="12058-714">Boş yuvaya **NX_DNS_SERVER_NOT_FOUND** (0xA9) dizin noktaları</span><span class="sxs-lookup"><span data-stu-id="12058-714">**NX_DNS_SERVER_NOT_FOUND** (0xA9) Index points to empty slot</span></span>
- <span data-ttu-id="12058-715">**NX_DNS_BAD_ADDRESS_ERROR** (0xa4) null sunucu adresine ait dizin noktaları</span><span class="sxs-lookup"><span data-stu-id="12058-715">**NX_DNS_BAD_ADDRESS_ERROR** (0xA4) Index points to null server address</span></span>
- <span data-ttu-id="12058-716">**NX_DNS_INVALID_ADDRESS_TYPE** (0xB2) dizin noktaları geçersiz adres türüne (örn. IPv6)</span><span class="sxs-lookup"><span data-stu-id="12058-716">**NX_DNS_INVALID_ADDRESS_TYPE** (0xB2) Index points to invalid address type (e.g. IPv6)</span></span>
- <span data-ttu-id="12058-717">**NX_DNS_PARAM_ERROR** (0Xa8) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="12058-717">**NX_DNS_PARAM_ERROR** (0xA8) Invalid non pointer input</span></span>
- <span data-ttu-id="12058-718">NX_PTR_ERROR (0x07) geçersiz IP veya DNS işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="12058-718">NX_PTR_ERROR (0x07) Invalid IP or DNS pointer.</span></span>
- <span data-ttu-id="12058-719">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="12058-719">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="12058-720">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="12058-720">Allowed From</span></span>

<span data-ttu-id="12058-721">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="12058-721">Threads</span></span>

### <a name="example"></a><span data-ttu-id="12058-722">Örnek</span><span class="sxs-lookup"><span data-stu-id="12058-722">Example</span></span>
```C
NXD_ADDRESS my_server_address;

/* Get the DNS Server at index 5 (zero based) into the Client list. */
status =  nxd_dns_server_get(&my_dns, 5, &my_server_addres);

/* If status is NX_SUCCESS a DNS Server was successfully
   returned. */
```

## <a name="nx_dns_server_remove"></a><span data-ttu-id="12058-723">nx_dns_server_remove</span><span class="sxs-lookup"><span data-stu-id="12058-723">nx_dns_server_remove</span></span>

<span data-ttu-id="12058-724">Bir IPv4 DNS sunucusunu Istemci listesinden kaldır</span><span class="sxs-lookup"><span data-stu-id="12058-724">Remove an IPv4 DNS Server from the Client list</span></span>

### <a name="prototype"></a><span data-ttu-id="12058-725">Prototype</span><span class="sxs-lookup"><span data-stu-id="12058-725">Prototype</span></span>
```C
UINT nx_dns_server_remove(NX_DNS *dns_ptr, ULONG server_address);
```
### <a name="description"></a><span data-ttu-id="12058-726">Açıklama</span><span class="sxs-lookup"><span data-stu-id="12058-726">Description</span></span>

<span data-ttu-id="12058-727">Bu hizmet, bir IPv4 DNS sunucusunu Istemci listesinden kaldırır.</span><span class="sxs-lookup"><span data-stu-id="12058-727">This service removes an IPv4 DNS Server from the Client list.</span></span> <span data-ttu-id="12058-728">*Nxd_dns_server_remove* için bir sarmalayıcı işlevidir.</span><span class="sxs-lookup"><span data-stu-id="12058-728">It is a wrapper function for *nxd_dns_server_remove*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="12058-729">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="12058-729">Input Parameters</span></span>

- <span data-ttu-id="12058-730">**dns_ptr** DNS denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="12058-730">**dns_ptr** Pointer to DNS control block.</span></span>
- <span data-ttu-id="12058-731">**server_address** DNS sunucusunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="12058-731">**server_address** IP address of DNS Server.</span></span>

### <a name="return-values"></a><span data-ttu-id="12058-732">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="12058-732">Return Values</span></span>

- <span data-ttu-id="12058-733">**NX_SUCCESS** (0x00) DNS sunucusu başarıyla kaldırıldı</span><span class="sxs-lookup"><span data-stu-id="12058-733">**NX_SUCCESS** (0x00) DNS Server successfully removed</span></span>
- <span data-ttu-id="12058-734">**NX_DNS_SERVER_NOT_FOUND** (0xA9) sunucu istemci listesinde değil</span><span class="sxs-lookup"><span data-stu-id="12058-734">**NX_DNS_SERVER_NOT_FOUND** (0xA9) Server not in Client list</span></span>
- <span data-ttu-id="12058-735">**NX_DNS_BAD_ADDRESS_ERROR** (0xa4) null sunucu adresi girişi</span><span class="sxs-lookup"><span data-stu-id="12058-735">**NX_DNS_BAD_ADDRESS_ERROR** (0xA4) Null server address input</span></span>
- <span data-ttu-id="12058-736">**NX_DNS_IPV6_NOT_SUPPORTED** (0xb3) IPv6 devre dışı olarak kayıt işlenemiyor</span><span class="sxs-lookup"><span data-stu-id="12058-736">**NX_DNS_IPV6_NOT_SUPPORTED** (0xB3) Cannot process record with IPv6 disabled</span></span>
- <span data-ttu-id="12058-737">NX_PTR_ERROR (0x07) geçersiz IP veya DNS işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="12058-737">NX_PTR_ERROR (0x07) Invalid IP or DNS pointer.</span></span>
- <span data-ttu-id="12058-738">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="12058-738">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="12058-739">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="12058-739">Allowed From</span></span>

<span data-ttu-id="12058-740">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="12058-740">Threads</span></span>

### <a name="example"></a><span data-ttu-id="12058-741">Örnek</span><span class="sxs-lookup"><span data-stu-id="12058-741">Example</span></span>
```C
/* Remove the DNS Server at IP address is 202.2.2.13.  */
status =  nx_dns_server_remove(&my_dns, IP_ADDRESS(202,2,2,13));

/* If status is NX_SUCCESS a DNS Server was successfully
   removed.  */
```

## <a name="nxd_dns_server_remove"></a><span data-ttu-id="12058-742">nxd_dns_server_remove</span><span class="sxs-lookup"><span data-stu-id="12058-742">nxd_dns_server_remove</span></span>

<span data-ttu-id="12058-743">Istemci listesinden bir DNS sunucusunu kaldırma</span><span class="sxs-lookup"><span data-stu-id="12058-743">Remove a DNS Server from the Client list</span></span>

### <a name="prototype"></a><span data-ttu-id="12058-744">Prototype</span><span class="sxs-lookup"><span data-stu-id="12058-744">Prototype</span></span>
```C
UINT nxd_dns_server_remove(NX_DNS *dns_ptr, NXD_ADDRESS *server_address);
```
### <a name="description"></a><span data-ttu-id="12058-745">Açıklama</span><span class="sxs-lookup"><span data-stu-id="12058-745">Description</span></span>

<span data-ttu-id="12058-746">Bu hizmet, belirtilen IP adresinin bir DNS sunucusunu Istemci listesinden kaldırır.</span><span class="sxs-lookup"><span data-stu-id="12058-746">This service removes a DNS Server of the specified IP address from the Client list.</span></span> <span data-ttu-id="12058-747">Giriş IP adresi hem IPv4 hem de IPv6 adreslerini kabul eder.</span><span class="sxs-lookup"><span data-stu-id="12058-747">The input IP address accepts both IPv4 and IPv6 addresses.</span></span> <span data-ttu-id="12058-748">Sunucu kaldırıldıktan sonra, kalan sunucular aşağı doğru bir dizin taşır ve bu da yuvaları doldurur.</span><span class="sxs-lookup"><span data-stu-id="12058-748">After the server is removed, the remaining servers move down one index in the list to fill the vacated slot.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="12058-749">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="12058-749">Input Parameters</span></span>

- <span data-ttu-id="12058-750">**dns_ptr** DNS denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="12058-750">**dns_ptr** Pointer to DNS control block.</span></span>
- <span data-ttu-id="12058-751">**server_address** DNS sunucusu işaretçisi sunucu IP adresini içeren verileri NXD_ADDRESS.</span><span class="sxs-lookup"><span data-stu-id="12058-751">**server_address** Pointer to DNS Server NXD_ADDRESS data containing server IP address.</span></span>

### <a name="return-values"></a><span data-ttu-id="12058-752">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="12058-752">Return Values</span></span>

- <span data-ttu-id="12058-753">**NX_SUCCESS** (0x00) DNS sunucusu başarıyla kaldırıldı</span><span class="sxs-lookup"><span data-stu-id="12058-753">**NX_SUCCESS** (0x00) DNS Server successfully removed</span></span>
- <span data-ttu-id="12058-754">**NX_DNS_SERVER_NOT_FOUND** (0xA9) sunucu istemci listesinde değil</span><span class="sxs-lookup"><span data-stu-id="12058-754">**NX_DNS_SERVER_NOT_FOUND** (0xA9) Server not in Client list</span></span>
- <span data-ttu-id="12058-755">**NX_DNS_BAD_ADDRESS_ERROR** (0xa4) null sunucu adresi girişi</span><span class="sxs-lookup"><span data-stu-id="12058-755">**NX_DNS_BAD_ADDRESS_ERROR** (0xA4) Null server address input</span></span>
- <span data-ttu-id="12058-756">**NX_DNS_IPV6_NOT_SUPPORTED** (0xb3) IPv6 devre dışı olarak kayıt işlenemiyor</span><span class="sxs-lookup"><span data-stu-id="12058-756">**NX_DNS_IPV6_NOT_SUPPORTED** (0xB3) Cannot process record with IPv6 disabled</span></span>
- <span data-ttu-id="12058-757">NX_PTR_ERROR (0x07) geçersiz IP veya DNS işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="12058-757">NX_PTR_ERROR (0x07) Invalid IP or DNS pointer.</span></span>
- <span data-ttu-id="12058-758">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="12058-758">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>
- <span data-ttu-id="12058-759">NX_DNS_INVALID_ADDRESS_TYPE (0xB2) dizin noktaları geçersiz adres türüne (örn. IPv6)</span><span class="sxs-lookup"><span data-stu-id="12058-759">NX_DNS_INVALID_ADDRESS_TYPE (0xB2) Index points to invalid address type (e.g. IPv6)</span></span>

### <a name="allowed-from"></a><span data-ttu-id="12058-760">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="12058-760">Allowed From</span></span>

<span data-ttu-id="12058-761">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="12058-761">Threads</span></span>

### <a name="example"></a><span data-ttu-id="12058-762">Örnek</span><span class="sxs-lookup"><span data-stu-id="12058-762">Example</span></span>
```C
NXD_ADDRESS server_address;

server_address.nxd_ip_version = NX_IP_VERISON_V6;
server_address.nxd_ip_address.v6[0] = 0x20010db8;
server_address.nxd_ip_address.v6[1] = 0x0;
server_address.nxd_ip_address.v6[2] = 0xf101;
server_address.nxd_ip-address.v6[3] = 0x108;


/* Remove the DNS Server at the specified IP address from the Client list. */
status =  nxd_dns_server_remove(&my_dns,&server_ADDRESS);

/* If status is NX_SUCCESS a DNS Server was successfully removed. */
```

## <a name="nx_dns_server_remove_all"></a><span data-ttu-id="12058-763">nx_dns_server_remove_all</span><span class="sxs-lookup"><span data-stu-id="12058-763">nx_dns_server_remove_all</span></span>

<span data-ttu-id="12058-764">Tüm DNS sunucularını Istemci listesinden kaldır</span><span class="sxs-lookup"><span data-stu-id="12058-764">Remove all DNS Servers from the Client list</span></span>

### <a name="prototype"></a><span data-ttu-id="12058-765">Prototype</span><span class="sxs-lookup"><span data-stu-id="12058-765">Prototype</span></span>
```C
UINT nx_dns_server_remove_all(NX_DNS *dns_ptr);
```
### <a name="description"></a><span data-ttu-id="12058-766">Açıklama</span><span class="sxs-lookup"><span data-stu-id="12058-766">Description</span></span>

<span data-ttu-id="12058-767">Bu hizmet, tüm DNS sunucularını Istemci listesinden kaldırır.</span><span class="sxs-lookup"><span data-stu-id="12058-767">This service removes all DNS Servers from the Client list.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="12058-768">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="12058-768">Input Parameters</span></span>

- <span data-ttu-id="12058-769">**dns_ptr** DNS denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="12058-769">**dns_ptr** Pointer to DNS control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="12058-770">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="12058-770">Return Values</span></span>

- <span data-ttu-id="12058-771">**NX_SUCCESS** (0x00) DNS sunucuları başarıyla kaldırıldı</span><span class="sxs-lookup"><span data-stu-id="12058-771">**NX_SUCCESS** (0x00) DNS Servers successfully removed</span></span>
- <span data-ttu-id="12058-772">**NX_DNS_ERROR** (0xa0) koruma mutex 'i alınamıyor</span><span class="sxs-lookup"><span data-stu-id="12058-772">**NX_DNS_ERROR** (0xA0) Unable to obtain protection mutex</span></span>
- <span data-ttu-id="12058-773">NX_PTR_ERROR (0x07) geçersiz IP veya DNS işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="12058-773">NX_PTR_ERROR (0x07) Invalid IP or DNS pointer.</span></span>
- <span data-ttu-id="12058-774">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="12058-774">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="12058-775">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="12058-775">Allowed From</span></span>

<span data-ttu-id="12058-776">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="12058-776">Threads</span></span>

### <a name="example"></a><span data-ttu-id="12058-777">Örnek</span><span class="sxs-lookup"><span data-stu-id="12058-777">Example</span></span>
```C
/* Remove all DNS Servers from the Client list. */
status =  nx_dns_server_remove_all(&my_dns);

/* If status is NX_SUCCESS all DNS Servers were successfully removed. */
```