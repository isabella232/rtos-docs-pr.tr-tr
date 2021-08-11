---
title: Bölüm 4 - Azure RTOS NetX Duo DHCPv6 sunucu hizmetleri
description: Bu bölümde tüm NetX Duo DHCPv6Server hizmetlerinin açıklaması yer almaktadır
author: philmea
ms.author: philmea
ms.date: 06/08/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: cf6b43f70a7159af6c24496ec2ae2276d5e271af2ad3af99687181df3bf6be6c
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116792035"
---
# <a name="chapter-4---azure-rtos-netx-duo-dhcpv6-server-services"></a>Bölüm 4 - Azure RTOS NetX Duo DHCPv6 sunucu hizmetleri

Bu bölümde tüm NetX Duo DHCPv6Server hizmetlerinin (aşağıda listelenmiştir) açıklaması yer alır.

Aşağıdaki API açıklamalarında yer alan "Dönüş Değerleri" bölümünde, **KALıN**  olmayan değerler tamamen devre dışı bırakılırken, BOLD NX_DISABLE_ERROR_CHECKING API hata denetimlerini devre dışı bırakmak için kullanılan tanımdan etkilenmez.

- nx_dhcpv6_server_create *DHCPv6 sunucusu oluşturma*
- nx_dhcpv6_server_delete *DHCPv6 sunucusunu silme*
- nx_dhcpv6_server_start *DHCPv6 sunucu görevini başlatma*
- nx_dhcpv6_server_suspend *DHCPv6 sunucu görevini askıya alma*
- nx_dhcpv6_server_resume *DHCPv6 istemci işlemesini sürdürme*
- nx_dhcpv6_server_suspend *DHCPv6 istemci işlemesini Askıya Alma*
- nx_dhcpv6_create_dns_address DNS *sunucusunu seçenek istekleri için ayarlama*
- nx_dhcpv6_create_ip_address_range *Kiralanması gereken IP adresleri aralığını oluşturma*
- nx_dhcpv6_reserve_ip_address_range *ip adresi aralığını sunucu listesinden yedekle*
- nx_dhcpv6_set_server_duid *DHCPv6 paketleri için Sunucu DUID'sini ayarlama*
- nx_dhcpv6_add_ip_address_lease *DHCPv6 sunucu tablosuna kiralama kaydı ekleme*
- Nx_dhcpv6_retrieve_ip_address_lease Sunucu *tablosundan IP kira kaydı alma*
- nx_dhcpv6_add_client_record *Tablosuna DHCPv6 İstemci kaydı ekleme*
- nx_dhcpv6_retrieve_client_record Sunucu *tablosundan istemci kaydı alma*
- nx_dhcpv6_server_interface_set Sunucu *DHCPv6 hizmetleri için arabirim dizinini ayarlama*
- nx_dhcpv6_server_option_request_handler_set *isteği işleyicisini ayarlama*

## <a name="nx_dhcpv6_create_dns_address"></a>nx_dhcpv6_create_dns_address

### <a name="set-the-network-dns-server"></a>Ağ DNS sunucusunu ayarlama

**Prototip**

```
UINT nx_dhcpv6_create_dns_address(
     NX_DHCPV6_SERVER *dhcpv6_server_ptr, 
     NXD_ADDRESS *dns_ipv6_address);
```

**Açıklama**

Bu hizmet, Sunucu DHCPv6 ağ arabirimi için DNS sunucusu adresiyle birlikte DHCPv6 Sunucusunu yükler.

**Giriş Parametreleri**

- **dhcpv6_server_ptr** DHCPv6 Sunucusu İşaretçisi
- **dns_ipv6_address** DNS sunucusunun işaretçisi

**Dönüş Değerleri**

- **NX_SUCCESS** (0x00) DNS Sunucuları DHCPv6 Sunucusu örneğine ekli
- **NX_DHCPV6_INVALID_INTERFACE_IP_ADDRESS** (0xE95) Geçersiz bir adres sağlanmalıdır
- NX_PTR_ERROR (0x16) Geçersiz işaretçi girişi

**İzin Verilen**

Uygulama Kodu

**Örnek**

```
/* Set the network DNS server with the input address for the Server DHCPv6interface. */
status = nx_dhcpv6_create__dns_address(&dhcp_server_0, &dns_ipv6_address);
/* If this service returns NX_SUCCESS the DNS server data was accepted. */
```

## <a name="nx_dhcpv6_create_ip_address_range"></a>nx_dhcpv6_create_ip_address_range

### <a name="create-the-server-ip-address-list"></a>Sunucu IP adresi listesini oluşturma

**Prototip**

```
UINT _nx_dhcpv6_create_ip_address_range(
     NX_DHCPV6_SERVER *dhcpv6_server_ptr, 
     NXD_ADDRESS *start_ipv6_address, NXD_ADDRESS *end_ipv6_address, 
     UINT *addresses_added)
```

**Açıklama**

Bu hizmet, Sunucunun atanabilir adres aralığının başlangıç ve bitiş adresleri tarafından belirtilen IP adresi listesini oluşturur. Başlangıç ve bitiş adresleri Sunucu arabirimi adres ön eki ile eşleşmeli (Sunucu DHCPv6 arabirimiyle aynı bağlantıda olmalıdır). Gerçekte eklenen adres sayısı döndürülür.

**Giriş Parametreleri**

- **dhcpv6_server_ptr** DHCPv6 Sunucusu İşaretçisi
- **start_ipv6_address** Eklemek istediğiniz adreslerin başlangıcı
- **end_ipv6_address** Eklemek istediğiniz adreslerin sonu
- ***addresses_added** Eklenen adreslerin çıkışı

**Dönüş Değerleri**

- **NX_SUCCESS** (0x00) IP adresi listesi başarıyla oluşturuldu
- **NX_DHCPV6_INVALID_INTERFACE_IP_ADDRESS** (0xE95) Geçersiz bir adres sağlanmalıdır
- NX_PTR_ERROR (0x16) Geçersiz işaretçi girişi

**İzin Verilen**

Uygulama Kodu

**Örnek**

```
/* Create the Server IP address list for the server DHCPv6 interface. */
status = nx_dhcpv6_create_ip_address_range(&dhcp_server_0,
         &start_ipv6_address, &end_ipv6_address, &addresses_reserved);
/* If status is NX_SUCCESS one or more addresses were successfully added. */
```

## <a name="nx_dhcpv6_reserve_ip_address_range"></a>nx_dhcpv6_reserve_ip_address_range

### <a name="reserve-specified-range-of-ip-addresses"></a>Belirtilen IP adresi aralığını koruma

**Prototip**

```
UINT _nx_dhcpv6_reserve_ip_address_range(
     NX_DHCPV6_SERVER *dhcpv6_server_ptr, 
     NXD_ADDRESS *start_ipv6_address, NXD_ADDRESS *end_ipv6_address, 
     UINT *addresses_reserved)
```

**Açıklama**

Bu hizmet, başlangıç ve bitiş adresleri tarafından belirtilen IP adresi aralığını yedekler. Bu adresler, önceden oluşturulmuş sunucu IP adresi aralığında yer alalıdır. Bu adresler DHCPv6 Sunucusu tarafından hiçbir İstemciye atanmayacak. Başlangıç ve bitiş adresleri Sunucu arabirimi adres ön eki ile eşleşmeli (Sunucu DHCPv6 ağ arabirimiyle aynı bağlantıda olmalıdır). Gerçekten ayrılmış olan adres sayısı döndürülür.

**Giriş Parametreleri**

- **dhcpv6_server_ptr** DHCPv6 Sunucusu İşaretçisi
- **start_ipv6_address** Rezervasyon için adreslerin başlangıcı
- **end_ipv6_address** Yedeklen adres sonu
- ***addresses_reserved** Ayrılan adres sayısı

**Dönüş Değerleri**

- **NX_SUCCESS** (0x00) YAYıN iletisi başarıyla oluşturuldu ve işlendi
- **NX_DHCPV6_INVALID_INTERFACE_IP_ADDRESS** (0xE95) Geçersiz bir adres sağlanmalıdır
- **NX_DHCPV6_INVALID_IP_ADDRESS** (0xED1) Sunucu adresi listesinde başlangıç adresi bulunamadı.
- NX_PTR_ERROR (0x16) Geçersiz işaretçi girişi

**İzin Verilen**

Uygulama Kodu

**Örnek**

```
/* Reserve a range of ip addresses in the Server address table for the server DHCPv6 
network interface. */

status = nx_dhcpv6_reserve_ip_address_range(&dhcp_server_0,
         &start_ipv6_address, &end_ipv6_address, &addresses_reserved);

/* If status is NX_SUCCESS one or more addresses were successfully reserved. */
```

## <a name="nx_dhcpv6_server_create"></a>nx_dhcpv6_server_create

### <a name="create-the-dhcpv6-server-instance"></a>DHCPv6 Sunucusu örneğini oluşturma 

**Prototip**

```
UINT nx_dhcpv6_server_create(NX_DHCPV6_SERVER *dhcpv6_server_ptr, 
        NX_IP *ip_ptr, CHAR *name_ptr, 
        NX_PACKET_POOL *packet_pool_ptr, 
        VOID *stack_ptr,ULONG stack_size,
    VOID (*dhcpv6_address_declined_handler)(struct 
        NX_DHCPV6_SERVER_STRUCT *dhcpv6_server_ptr, 
        NX_DHCPV6_CLIENT *dhcpv6_client_ptr, 
        UINT message),
    VOID (*dhcpv6_option_request_handler)(
        struct NX_DHCPV6_SERVER_STRUCT *dhcpv6_server_ptr, 
        UINT option_request, UCHAR *buffer_ptr, UINT *index));
```

**Açıklama**

Bu hizmet, belirtilen girişle DHCPv6 Sunucusu görevini oluşturur. Geri çağırma işleyicileri isteğe bağlı giriştir. Yığın işaretçisi, IP örneği ve paket havuzu girişi gereklidir. IP örneği ve paket havuzu önceden oluşturulmuş olması gerekir.

Seçenek isteği işleyicisini ayarlamak nx_dhcpv6_server_option_request_handler_set kullanıcıya çağrılmaları teşvik edilmektedir.

**Giriş Parametreleri**

- **dhcpv6_server_ptr** DHCPv6 Sunucusu İşaretçisi
- **ip_ptr** IP örneğinin işaretçisi
- **name_str** Sunucu adı işaretçisi
- **packet_pool_ptr** Sunucu paket havuzu işaretçisi
- **stack_ptr** Sunucu yığın belleği işaretçisi
- **stack_size** Sunucu yığın belleğinin boyutu
- **dhcpv6_address_declined_handler** İstemci Reddetme veya Yayın iletisi işleyicisi işaretçisi
- **dhcpv6_option_request_handler** Seçeneklere işaretçi isteği seçenek işleyicisi

**Dönüş Değerleri**

- **NX_SUCCESS** (0x00) Sunucusu başarıyla sürdürıldı
- NX_PTR_ERROR (0x16) Geçersiz işaretçi girişi
- NX_DHCPV6_PARAM_ERROR İşaretçi olmayan giriş geçersiz

**İzin Verilen**

Uygulama kodu

**Örnek**

```
/* Create the DHCPv6 Server. */
status = nx_dhcpv6_server_create(&dhcp_server_0, &ip_0, "DHCPv6 Server",
         &pool_0, stack_pointer,2048, dhcpv6_decline_handler,
         dhcpv6_get_time_handler);
/* If status is NX_SUCCESS the Server successfully created. */
```

## <a name="nx_dhcpv6_server_delete"></a>nx_dhcpv6_server_delete

### <a name="delete-the-dhcpv6-server"></a>DHCPv6 sunucusunu silme

**Örneğini**

```
UINT _nx_dhcpv6_server_delee(NX_DHCPV6_SERVER *dhcpv6_server_ptr)
```

**Açıklama**

Bu hizmet, DHCPv6 sunucusu görevini ve sunucunun işlediği tüm istekleri siler.

**Giriş parametreleri**

- **dhcpv6_server_ptr** DHCPv6 sunucusu işaretçisi

**Dönüş değerleri**

- **NX_SUCCESS** (0x00) sunucu başarıyla silindi
- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi

**İzin verilen**

İş Parçacıkları

**Örnek**

```
/* Delete the DHCPv6 Serve. */
status = nx_dhcpv6_server_delete(&dhcp_server_0);
/* If status is NX_SUCCESS the Server successfully deleted. */
```

## <a name="nx_dhcpv6_server_resume"></a>nx_dhcpv6_server_resume

### <a name="resume-dhcpv6-server-task"></a>DHCPv6 sunucusu görevini sürdürür 

**Örneğini**

```
UINT _nx_dhcpv6_server_resume(NX_DHCPV6_SERVER *dhcpv6_server_ptr)
```

**Açıklama**

Bu hizmet, DHCPv6 sunucusu görevini ve sunucunun işlediği tüm istekleri sürdürür.

**Giriş parametreleri**

- **dhcpv6_server_ptr** DHCPv6 sunucusu işaretçisi

**Dönüş değerleri**

- **NX_SUCCESS** (0x00) sunucu başarıyla sürdürüldü
- **NX_DHCPV6_ALREADY_STARTED** (0xe91) sunucu zaten çalışıyor
- **durum** (değişken) threadx ve NETX Duo hata durumu
- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi

**İzin verilen**

İş Parçacıkları

**Örnek**

```
/* Resume the DHCPv6 Server task. */
status = nx_dhcpv6_server_resume(&dhcp_server_0);
/* If status is NX_SUCCESS the Server successfully resumed. */
```

## <a name="nx_dhcpv6_server_suspend"></a>nx_dhcpv6_server_suspend

### <a name="suspend-dhcpv6-server-task"></a>DHCPv6 sunucusunu askıya al görevi 

**Örneğini**

```
UINT _nx_dhcpv6_server_suspend(NX_DHCPV6_SERVER *dhcpv6_server_ptr)
```

**Açıklama**

Bu hizmet, DHCPv6 sunucusu görevini ve sunucunun işlediği tüm istekleri askıya alır.

**Giriş parametreleri**

- **dhcpv6_server_ptr** DHCPv6 sunucusu işaretçisi

**Dönüş değerleri**

- **NX_SUCCESS** (0x00) sunucu başarıyla sürdürüldü
- **NX_DHCPV6_NOT_STARTED** (0xe92) sunucusu başlatılmadı 
- **Durum** (değişken) threadx ve NETX Duo hata durumu
- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi

**İzin verilen**

İş Parçacıkları

**Örnek**

```
/* Suspend the DHCPv6 Server task. */
status = nx_dhcpv6_server_suspend(&dhcp_server_0);

/* If status is NX_SUCCESS the Server successfully suspended. */
```

## <a name="nx_dhcpv6_server_start"></a>nx_dhcpv6_server_start

### <a name="start-the-dhcpv6-server-task"></a>DHCPv6 sunucusu görevini başlatın 

**Örneğini**

```
UINT _nx_dhcpv6_server_start(NX_DHCPV6_SERVER *dhcpv6_server_ptr)
```

**Açıklama**

Bu hizmet DHCPv6 sunucusu görevini başlatır ve DHCPv6 Istemci iletilerini almak için uygulama isteklerini işlemek üzere sunucuyu yeniden başlatır. Sunucu örneğinin yeterli bilgilere sahip olduğunu doğrular (sunucu DUıD), DHCPv6 iletilerini göndermek ve almak için UDP yuvasını oluşturup bağlar ve oturum süresini ve IP Kiralama süre sonunu izlemek için zamanlayıcıları etkinleştirir.

>[!NOTE] 
> DHCPv6 sunucusunun çalıştırılabilmesi için, ana bilgisayar uygulaması, sunucunun IP adreslerini atayabileceği IP adresi aralığını oluşturmaktan sorumludur. Ayrıca, sunucu DUıD ve DHCPv6 arabirimini ayarlamaktan de sorumludur (sırasıyla *nx_dhcpv6_server_duid_set* ve *nx_dhcpv6_server_interface_set* .

**Giriş parametreleri**

- **dhcpv6_server_ptr** DHCPv6 sunucusu işaretçisi

**Dönüş değerleri**

- **NX_SUCCESS** (0x00) sunucu başarıyla başlatıldı
- **NX_DHCPV6_ALREADY_STARTED** (0xe91) sunucu zaten çalışıyor
- **NX_DHCPV6_NO_ASSIGNABLE_ADDRESSES** (0xea7) sunucusunda kiralamaya atanabilen bir adres yok
- **NX_DHCPV6_INVALID_GLOBAL_INDEX** (0xe97) genel adres dizini ayarlanmadı
- **NX_DHCPV6_NO_SERVER_DUID** (0xe92) sunucu DUID oluşturulmadı 
- **durum** (değişken) threadx ve NETX Duo hata durumu
- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi

**İzin verilen**

İş Parçacıkları

**Örnek**

```
/* Start the DHCPv6 Server task. */
status = nx_dhcpv6_server_start(&dhcp_server_0);
/* If status is NX_SUCCESS the Server successfully started. */
```

## <a name="nx_dhcpv6_retrieve_ip_address_lease"></a>nx_dhcpv6_retrieve_ip_address_lease

### <a name="get-an-ip-address-lease-from-the-server-table"></a>Sunucu tablosundan bir IP adresi kirası al

**Örneğini**

```
UINT _nx_dhcpv6_retrieve_ip_address_lease(
     NX_DHCPV6_SERVER *dhcpv6_server_ptr, UINT table_index, 
     NXD_ADDRESS *lease_IP_address, ULONG *T1, ULONG *T2, 
     ULONG *valid_lifetime, ULONG *preferred_lifetime)
```

**Açıklama**

Bu hizmet, belirtilen tablo dizini konumundaki sunucu tablosundan bir IP adresi kiralama kaydı alır. Bu işlem, Istemci kaydı verilerinin alınmadan önce veya sonra yapılabilir.

DHCPv6 sunucusu ile geçici olmayan bellek arasında veri depolama ve alma özelliği, DHCPv6 protokolünün bir gereksinimidir. IP Kiralama verilerinin ve Istemci kayıt verilerinin kalıcı olmayan belleğe kaydedildiği sırada farklılık yapmaz.

>[!NOTE] 
> Önce DHCPv6 sunucusunu durdurmadan veya askıya almadan sunucu tablolarına veya sunucudan veri kopyalanması önerilmez.

**Giriş parametreleri**

- **dhcpv6_server_ptr** DHCPv6 sunucusu işaretçisi
- **table_index** Kira depolanacak tablo dizini
- **lease_IP_address** Istemciye kiralanan IP adresi işaretçisi
- **T1** İstemci yenileme süresi istedi
- **T2** İstemci yeniden bağlama süresi istedi
- **valid_lifetime** İstemci kirası kullanım dışı duruma geliyor
- **preferred_lifetime** İstemci kirası geçersiz hale geliyor

**Dönüş değerleri**

- **NX_SUCCESS** (0x00) sunucu başarıyla başlatıldı
- **NX_DHCPV6_PARAMETER_ERROR** (0xe93) geçersiz IP Kiralama verileri girişi
- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi

**İzin verilen**

Uygulama kodu

**Örnek**

```
/* Retrieve the DHCPv6 Server lease data. */
For (I = 0; I < NX_DHCPV6_MAX_LEASES; i++)
{
    /* Get the next lease record. */
    status = nx_dhcpv6_server_startdhcpv6_server_ptr, i, &next_ipv6_address, &T1,
             &T2, &preferred_lifetime, &valid_lifetime);
    /* The host application then saves this record to memory.
}
/* If status is NX_SUCCESS the Server data is successfully downloaded. */
```

## <a name="nx_dhcpv6_add_ip_address_lease"></a>nx_dhcpv6_add_ip_address_lease

### <a name="add-an-ip-address-lease-to-the-server-table"></a>Sunucu tablosuna bir IP adresi kirası ekleyin

**Örneğini**

```
UINT _nx_dhcpv6_add_ip_address_lease(
     NX_DHCPV6_SERVER *dhcpv6_server_ptr, UINT table_index, NXD_ADDRESS *lease_IP_address, ULONG T1, ULONG T2, 
     ULONG valid_lifetime, ULONG preferred_lifetime)
```

**Açıklama**

Bu hizmet, önceki bir DHCPv6 sunucu oturumundan gelen IP Kiralama verilerini geçici olmayan bellekten sunucu kiralama tablosuna yükler. Sunucu ilk kez çalışıyorsa ve önceki kira verisi yoksa, bu gerekli değildir. Bu durum, ana bilgisayar uygulamasının IP adreslerini atamak için *nx_dhcpv6_create_ip_address_range* hizmetini kullanarak bir IP adresi aralığı oluşturması gerekir. Veriler, bir DHCPv6 Kiralama kaydını yeniden oluşturmak için yeterlidir. Tablo dizini belirtilmemelidir. 0xFFFFFFFF (Infinity) olarak ayarlandıysa, DHCPv6 sunucusu, verileri kopyalamak için kullanılabilecek bir sonraki yuvayı bulur.

>[!NOTE] 
> Istemci kayıtları karşıya yüklenmeden önce IP kira verilerinin yüklenmesi yapılmalıdır; yalnızca DHCPv6 sunucusu başlatılmadan önce (yeniden) yapılmalıdır.

DHCPv6 sunucusu ile geçici olmayan bellek arasında veri depolama ve alma özelliği, DHCPv6 protokolünün bir gereksinimidir.

**Giriş parametreleri**

- **dhcpv6_server_ptr** DHCPv6 sunucusu işaretçisi
- **table_index** Kira depolanacak tablo dizini
- **lease_IP_address** Istemciye kiralanan IP adresi işaretçisi
- **T1** İstemci yenileme süresi istedi
- **T2** İstemci yeniden bağlama süresi istedi
- **valid_lifetime** İstemci kirası kullanım dışı duruma geliyor
- **preferred_lifetime** İstemci kirası geçersiz hale geliyor

**Dönüş değerleri**

- **NX_SUCCESS** (0x00) sunucu başarıyla başlatıldı
- **NX_DHCPV6_TABLE_FULL** (0xec4) daha fazla kira verisi Için boşluk yok * *
- **NX_DHCPV6_INVALID_INTERFACE_IP_ADDRESS** (0xe95) kira verisi sunucu DHCPv6 arabirimiyle bağlantılı olarak görünmüyor
- **NX_DHCPV6_PARAM_ERROR** (0xe93) geçersiz IP Kiralama verileri girişi
- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi

**İzin verilen**

Uygulama kodu

**Örnek**

```
/* Copy the IP lease data to the Server address table. Note that the table index
is defaulted to 0xFFFFFFFF meaning the DHCPv6 Server will find an empty slot 
for each lease. */

    For(I = 0; I < NX_DHCPV6_MAX_LEASES; i++)
    {
        status = nx_dhcpv6_add_ip_address_lease(dhcpv6_server_ptr, 0xFFFFFFFF,
                 &next_ipv6_address, &T1, &T2, &preferred_lifetime, &valid_lifetime);
        /* Get the next lease address from memory… */
    }
    
    /* If status is NX_SUCCESS the lease data was successfully uploaded. It is opk
    to add the Client records to the Server table now. */
```

## <a name="nx_dhcpv6_add_client_record"></a>nx_dhcpv6_add_client_record

### <a name="add-a-client-record-to-the-server-table"></a>Sunucu tablosuna bir Istemci kaydı ekleme

**Örneğini**

```
UINT _nx_dhcpv6_add_client_record(NX_DHCPV6_SERVER *dhcpv6_server_ptr, 
     UINT table_index, ULONG message_xid, 
     NXD_ADDRESS *client_address, UINT client_state, 
     ULONG IP_lease_time_accrued, ULONG valid_lifetime, UINT duid_type, UINTduid_hardware, 
     ULONG physical_address_msw, ULONG physical_address_lsw, ULONG duid_time, 
     ULONG duid_vendor_number, UCHAR *duid_vendor_private, UINT duid_private_length)
```

**Açıklama**

Bu hizmet, Istemci verilerini geçici olmayan bellekten sunucu tablosuna tek seferde kopyalar. Bu, yalnızca sunucu yeniden başlatılırsa ve bellekten geri yüklemek için önceki bir oturumdan Istemci verilerinin bulunduğu durumlarda gereklidir. Bir sunucuda önceki veriler yoksa, DHCPv6 sunucusu istemci kayıtları eklemek için Istemci tablosunu başlatır.

Tablo dizinini belirtmek gerekli değildir. 0xFFFFFFFF (Infinity) olarak ayarlandıysa, DHCPv6 sunucusu bir sonraki kullanılabilir yuvayı bulur. DHCPv6 sunucusu, bu verilerden bir Istemci kaydını yeniden oluşturabilir.

>[!NOTE] 
> Ana bilgisayar uygulamasının, Istemci kaydından önce IP Kiralama verilerini yüklemesi gerekır. Bu sayede, her bir Istemci kaydının ilgili tablolarında karşılık gelen IP Kiralama kaydıyla birleştirilebilecek şekilde, DHCPv6 sunucusunun tabloları çapraz bir şekilde bağlantısı sağlanabilir. Bellekten IP Kiralama verilerini karşıya yükleme hakkında ayrıntılı bilgi için bkz. *nx_dhcpv6_add_ip_address_lease* .

>[!NOTE] 
> DUıD türüne bağlı olarak, tüm verilerin sağlanması gerekir. Örneğin, bir Istemcide bir satıcı atanmış DUıD türü varsa, bu, DUıD bağlantı katmanı parametreleri (MAC adresi, donanım türü, DUıD saati) için sıfır olarak gönderebilir.

DHCPv6 sunucusu ile geçici olmayan bellek arasında veri depolama ve alma özelliği, DHCPv6 protokolünün bir gereksinimidir.

**Giriş parametreleri**

- **dhcpv6_server_ptr** DHCPv6 sunucusu işaretçisi

**Dönüş değerleri**

- **NX_SUCCESS** (0x00) sunucu başarıyla başlatıldı
- **NX_ INVALID_PARAMETERS** (0x4D) geçersiz işaretçi girişi * *
- **NX_DHCPV6_TABLE_FULL** (0xec4) başka bir istemci kaydı eklemek için boş yuva kalmadı
- **NX_DHCPV6_ADDRESS_NOT_FOUND** (0xea8) istemci tarafından atanan adres sunucu kira tablosunda bulunamadı.
- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi

**İzin verilen**

Uygulama kodu

**Örnek**

```
/*Add the IP lease data and Client records back to the server before starting
theServer. */
    /* Copy the 'lease data' to the server table FIRST. */
for (i = 0; i< NX_DHCPV6_MAX_LEASES; i++)
    {

        /* Add the next lease record. Let the server find the next
        available slot. */
        status = nx_dhcpv6_add_ip_address_lease(dhcpv6_server_ptr,
                 0xFFFFFFFF,,&next_ipv6_address, NX_DHCPV6_DEFAULT_T1_TIME, 
                 NX_DHCPV6_DEFAULT_T2_TIME, NX_DHCPV6_DEFAULT_PREFERRED_TIME, 
                 NX_DHCPV6_DEFAULT_VALID_TIME);
if (status != NX_SUCCESS)
return status;
        /* Get the next IP lease record from memory. */
        …
    }
    /* Copy the client records to the Server table NEXT.
    for (i = 0; i< NX_DHCPV6_MAX_LEASES; i++)
    {
        /* Add the next client record. Let the server find the next
        available slot. */
        status = nx_dhcpv6_add_client_record(dhcpv6_server_ptr, 0xFFFFFFFF,
                 message_xid, &client_ipv6_address, NX_DHCPV6_STATE_BOUND,
                 IP_lifetime_time_accrued, valid_lifetime, duid_type, 
                 duid_hardware, physical_address_msw, physical_address_lsw, 
                 duid_time, 0, NX_NULL, 0);
if (status != NX_SUCCESS)
return status;
        /* Get the next Client record from memory. */
        …
    }

/* If status is NX_SUCCESS the Server data was successfully restored and 
it is ok to start the DHCPv6 server now. */
```

## <a name="nx_dhcpv6_retrieve_client_record"></a>nx_dhcpv6_retrieve_client_record

### <a name="retrieve-a-client-record-from-the-server-table"></a>Sunucu tablosundan bir Istemci kaydı alma

**Örneğini**

```
UINT _nx_dhcpv6_retrieve_client_record(
     NX_DHCPV6_SERVER *dhcpv6_server_ptr, 
     UINT table_index, ULONG *message_xid, 
     NXD_ADDRESS *client_address, UINT *client_state, 
     ULONG IP_lease_time_accrued, 
     ULONG *valid_lifetime, UINT *duid_type, 
     UINT *duid_hardware, ULONG *physical_address_msw, 
     ULONG *physical_address_lsw, ULONG *duid_time, 
     ULONG *duid_vendor_number, 
     UCHAR *duid_vendor_private, 
     UINT *duid_private_length)
```

**Açıklama**

Bu hizmet, gerekli verileri depolama için sunucunun Istemci kayıt tablosundan geçici olmayan belleğe kopyalar. Sunucu, ters işlemdeki (sunucu tablosuna verileri karşıya yükleme) bu tür verilerden yeterli bir Istemci kaydını yeniden oluşturabilir. DUıD türünden bağımsız olarak işaretçilerin hiçbiri NULL işaretçiler olamaz; veriler tüm parametreler için sıfır olarak başlatılır. Örneğin, Istemci DUıD türü bağlantı katmanı ve zaman ise, satıcı numarası sıfır olarak döndürülür ve özel KIMLIK boş bir dizedir.

DHCPv6 sunucusu ile geçici olmayan bellek arasında veri depolama ve alma özelliği, DHCPv6 protokolünün bir gereksinimidir. IP Kiralama verilerinin ve Istemci kayıt verilerinin kalıcı olmayan belleğe kaydedildiği sırada farklılık yapmaz.

>[!NOTE] 
> Önce DHCPv6 sunucusunu durdurmadan veya askıya almadan sunucu tablolarına veya sunucudan veri kopyalanması önerilmez.

**Giriş parametreleri**

- **dhcpv6_server_ptr** DHCPv6 sunucusu işaretçisi
- **table_index** Sunucunun istemci tablosuna Dizin
- **message_xid** İstemci sunucusu Işlem KIMLIĞI
- **client_address** Istemciye kiralanan IPv6 adresi
- **client_state** İstemci DHCPv6 durumu (örn. bağlantılı)
- **IP_lease_time_accrued** DHCPv6 sunucusuna yönelik işaretçinin zaten **dhcpv6_server_ptr** kira süresi geçildi
- **dhcpv6_server_ptr** DHCPv6 sunucusu işaretçisi

**Dönüş değerleri**

- **NX_SUCCESS** (0x00) sunucu başarıyla başlatıldı
- **NX_DHCPV6_INVALID_DUID** (0xecc) geçersiz veya tutarsız DUID verileri
- **NX_PTR_ERROR** (0x16) geçersiz işaretçi girişi
- NX_INVALID_PARAMETERS (0x4D) geçersiz işaretçi girişi

**İzin verilen**

Uygulama kodu

**Örnek**

```
/* Retrieve the Client records from the DHCPv6 Server table. */
For (i = 0; i< NX_MAX_DHCPV6_CLIENTS; i++)
{
    status = nx_dhcpv6_retrieve_client_recorddhcpv6_server_ptr, i, &message_xid,
             &client_ipv6_address, &client_state, &IP_lifetime_time_accrued, 
             valid_lifetime, &duid_type, &duid_hardware, &physical_address_msw,
             &physical_address_lsw, &duid_time, &duid_vendor_number, &private_id[0], 
             &length);
    /* The host application can save this data to memory now.
}
/* If status is NX_SUCCESS the Server successfully started. */
```

## <a name="nx_dhcpv6_server_interface_set"></a>nx_dhcpv6_server_interface_set

### <a name="setthe-interface-index-for-server-dhcpv6-interface"></a>Sunucu DHCPv6 arabirimi için arabirim dizinini ayarla

**Örneğini**

```
UINT _nx_dhcpv6_server_interface_set(
     NX_DHCPV6_SERVER *dhcpv6_server_ptr, 
     UINT iface_index, UINT ga_address_index)
```

**Açıklama**

Bu hizmet, DHCPv6 sunucusunun DHCPv6 Istemci isteklerini işlediği ağ arabirimini ayarlar. Birden çok giriş desteği olmayan NetX Duo sürümleri için, arabirim değeri varsayılan olarak sıfırdır. Genel Adres dizini, DHCPv6 arabiriminde sunucu genel adresini elde etmek için gereklidir. Bu, kira adreslerinin ve diğer DHCPv6 verilerinin DHCPv6 sunucusuyla bağlantılı olduğundan emin olmak için DHCPv6 mantığı tarafından kullanılır.

Bu, tek bağlantılı cihazlardaki uygulamalar veya çok giriş desteği olmadan, DHCPv6 sunucusu başlatılmadan önce çağrılmalıdır.

**Giriş parametreleri**

- **dhcpv6_server_ptr** DHCPv6 sunucusu işaretçisi
- **iface_index** Sunucu DHCPv6 sunucu arabirimi
- **ga_address_index** Sunucu IP örnek adresi tablosundaki sunucu genel adresinin dizini

**Dönüş değerleri**

- **NX_SUCCESS** (0x00) sunucu başarıyla başlatıldı
- **NX_INVALID_INTERFACE** (0x4C) arabirimi yok
- NX_NO_INTERFACE_ADDRESS (0x50) Genel dizin, IP örneği en fazla IPv6 adresini aşıyor (NX_MAX_IPV6_ADDRESSES)
- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi

**İzin verilen**

Uygulama kodu

**Örnek**

```
/* Set the Server DHCPv6 interface to the primary interface. The global IP 
address is at the index 1 in the IP address table. */
status = nx_dhcpv6_server_interface_set(&dhcp_server_0, 0, 1);

/* If status is NX_SUCCESS the Server interface is successfully set. */
```
## <a name="nx_dhcpv6_set_server_duid"></a>nx_dhcpv6_set_server_duid

### <a name="set-the-server-duid-for-dhcpv6-packets"></a>DHCPv6 paketleri için sunucu DUıD 'sini ayarlama

**Örneğini**

```
UINT _nx_dhcpv6_set_server_duid(NX_DHCPV6_SERVER *dhcpv6_server_ptr,
     UINT duid_type, UINT hardware_type, 
     ULONG mac_address_msw, ULONG mac_address_lsw, 
     ULONG time)
```

**Açıklama**

Bu hizmet, sunucu DUıD 'yi ayarlar ve konak uygulama sunucuyu başlamadan önce çağrılmalıdır. Bağlantı katmanı ve bağlantı katmanı zaman DUıD türleri için, ana bilgisayar uygulamasının donanım türü ve MAC adresi verilerini sağlaması gerekir. Bağlantı katmanı zaman DUID 'Leri için zaman işaretçisi geçerli bir saate işaret etmelidir. 1 Ocak 2000 ' den beri geçen saniye sayısı tipik bir çekirdek değerdir. Sunucu DUıD türü kurumsal, satıcıya atanmış tür ise, DUıD Kullanıcı yapılandırılabilir seçenekleri NX_DHCPV6_SERVER_DUID_VENDOR_PRIVATE_ID ve NX_DHCPV6_SERVER_DUID_VENDOR_ASSIGNED_ID oluşturulur ve zaman ve MAC adresi değerleri NULL olarak ayarlanabilir.

>[!NOTE] 
> Sunucu DUıD parametrelerini, yeniden başlatmalar arasındaki Istemcilere yönelik iletilerde aynı DUıD 'yi kullanacak şekilde kalıcı belleğe kaydetmek, ana bilgisayar uygulamasının sorumluluğundadır. Bu, DHCPv6 protokolünün (RFC 3315) bir gereksinimidir.

**Giriş parametreleri**

- **dhcpv6_server_ptr** DHCPv6 sunucusu işaretçisi
- **duid_type** DHCPv6 sunucusu DUıD türü
- **hardware_type** Donanım türü (örneğin, Ethernet)
- **mac_address_msw** DHCPv6 sunucusu işaretçisi
- **mac_address_lsw** DHCPv6 sunucusu işaretçisi
- **zaman** DUıD için saat değeri

**Dönüş değerleri**

- **NX_SUCCESS** (0x00) sunucu başarıyla askıya alındı
- **NX_DHCPV6_INVALID_SERVER_DUID** (0xe98) bilinmeyen veya desteklenmeyen DUID türü
- **NX_INVALID_PARAMETERS** (0x4D) geçersiz işaretçi girişi
- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi

**İzin verilen**

Uygulama kodu

**Örnek**

```
/* Set the DHCPv6 ServerDUID as Link layer plus time, over Ethernet hardware. */
duid_time = SECONDS_SINCE_JAN_1_2000_MOD_32 + rand();

status = nx_dhcpv6_set_server_duid(&dhcp_server_0,1, 0x6,
         physical_address_msw,physical_address_lsw,duid_time);

/* If status is NX_SUCCESS the ServerDUID is successfully set. */
```

## <a name="nx_dhcpv6_server_option_request_handler_set"></a>nx_dhcpv6_server_option_request_handler_set

### <a name="set-the-option-request-handler-for-dhcpv6-server-instance"></a>DHCPv6 sunucu örneği için seçenek isteği işleyicisini ayarla 

**Örneğini**

```
UINT nx_dhcpv6_server_option_request_handler_set(
     NX_DHCPV6_SERVER *dhcpv6_server_ptr, 
     VOID (*dhcpv6_option_request_handler_extended)(
          struct NX_DHCPV6_SERVER_STRUCT *dhcpv6_server_ptr, 
          UINT option_request, UCHAR *buffer_ptr, 
          UINT *index, UINT available_payload));
```

**Açıklama**

Bu hizmet, DHCPv6 sunucusu genişletilmiş seçenek isteği işleyicisini ayarlar.

**Giriş parametreleri**

- **dhcpv6_server_ptr** DHCPv6 sunucusu işaretçisi
- **dhcpv6_option_request_handler_extended** Genişletilmiş Seçenekler istek işleyicisi işaretçisi

**Dönüş değerleri**

- **NX_SUCCESS** (0x00) sunucu başarıyla sürdürüldü
- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi

**İzin verilen**

Uygulama kodu

**Örnek**

```
/* Set the option request handler for DHCPv6 Server. */
status = nx_dhcpv6_server_option_request_handler_set(&dhcp_server_0,
         dhcpv6_option_request_handler_extended);

/* If status is NX_SUCCESS the extended handler successfully set. */
```