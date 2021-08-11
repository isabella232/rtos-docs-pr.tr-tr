---
title: Bölüm 3 - NetX Duo Azure RTOS hizmetlerinin açıklaması
description: Bu bölümde, tüm NetX Duo TFTP hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: db7b7469bda02597db6428ecbf080b37a095413411eef2abefb1c4804d7bb1d3
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116799073"
---
# <a name="chapter-3---description-of-azure-rtos-netx-duo-tftp-services"></a>Bölüm 3 - NetX Duo Azure RTOS hizmetlerinin açıklaması

Bu bölümde, tüm NetX Duo TFTP hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklaması yer almaktadır. Aksi belirtilmedikçe, tüm hizmetler IPv6 ve IPv4 iletişimlerini destekler.

Aşağıdaki API açıklamalarında yer alan "Dönüş Değerleri" bölümünde, **KALıN**  olmayan değerler tamamen devre dışı bırakılırken, BOLD NX_DISABLE_ERROR_CHECKING API hata denetimlerini devre dışı bırakmak için kullanılan tanımdan etkilenmez.

- **nxd_tftp_client_file_open:** *TFTP istemci dosyasını açın*

- **nxd_tftp_client_create:** *TFTP istemci örneği oluşturma*

- **nxd_tftp_client_delete:** *TFTP istemci örneğini silme*

- **nxd_tftp_client_error_info_get:** *İstemci hata bilgilerini al*

- **nxd_tftp_client_file_close:** İstemci *dosyasını kapatma*

- **nxd_tftp_client_file_open:** İstemci *dosyasını açın*

- **nxd_tftp_client_file_read:** *İstemci dosyasından bir bloğu okuma*

- **nxd_tftp_client_file_write:** *Blokları istemci dosyasına yazma*

- **nxd_tftp_client_packet_allocate:** İstemci *dosya yazma için paket ayırma*

- **nxd_tftp_client_set_interface:** *TFTP istekleri için fiziksel arabirimi ayarlama*

- **nxd_tftp_server_create:** *TFTP sunucusu oluşturma*

- **nxd_tftp_server_delete:** *TFTP sunucusunu silme*

- **nxd_tftp_server_start:** *TFTP sunucusunu başlatma*

- **nxd_tftp_server_stop:** *TFTP sunucusunu durdurun*

> [!NOTE] 
> Yukarıda listelenen tüm hizmetlerin IPv4 eşdeğerleri NetX Duo TFTP İstemcisi ve  Sunucusu'nx_tftp_server_create ve *nx_tftp_client_file_open.* Yalnızca 'Duo' API açıklamaları (nxd_ ile başlayan hizmetler gibi) aşağıdaki sayfalarda verilmektedir. Bir NXD_ADDRESS \* belirtiliyorsa, IPv4 eşdeğer API ULONG girişi için çağrır. Aksi takdirde API'yi kullanmanın hiçbir farkı yoktur.

## <a name="nxd_tftp_client_create"></a>nxd_tftp_client_create

TFTP İstemci örneği oluşturma

### <a name="prototype"></a>Prototype

```C
UINT nxd_tftp_client_create(NX_TFTP_CLIENT *tftp_client_ptr,  
     CHAR *tftp_client_name, NX_IP *ip_ptr, NX_PACKET_POOL *pool_ptr);
```

### <a name="description"></a>Description

Bu hizmet, daha önce oluşturulan IP örneği için bir TFTP İstemci örneği oluşturur.

> [!IMPORTANT]
> Uygulama, sağlanan IP'nin ve paket havuzunun zaten oluşturulmuş olduğunu kesin olarak onaylar. Ayrıca, bu hizmeti çağırmadan önce IP örneği için UDP etkinleştirilmelidir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **tftp_client_ptr** TFTP İstemcisi denetim bloğu işaretçisi.

- **tftp_client_name** Bu TFTP İstemci örneğinin adı

- **ip_ptr** Daha önce oluşturulan IP örneğinin işaretçisi.

- **pool_ptr** Paket havuzu TFTP İstemci örneği işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**(0x00) Başarılı TFTP oluşturma.

- **NX_TFTP_INVALID_IP_VERSION** (0x0C) Geçersiz veya desteklenmeyen IP sürümü

- **NX_TFTP_INVALID_SERVER_ADDRESS** (0x08) Geçersiz Sunucu IP adresi alındı

- **NX_TFTP_NO_ACK_RECEIVED** (0x09) Sunucu ACK alınamadı

- NX_PTR_ERROR (0x16) Geçersiz IP, havuz veya TFTP işaretçisi.

- NX_INVALID_PARAMETERS (0x4D) İşaretçi olmayan giriş geçersiz

- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

Başlatma ve İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Create a TFTP Client instance. */
status =  nxd_tftp_client_create(&my_tftp_client, “My TFTP Client”, 
                                                    &my_ip, &pool_ptr);

/* If status is NX_SUCCESS a TFTP Client instance was successfully
   created. */
```

## <a name="nxd_tftp_client_delete"></a>nxd_tftp_client_delete

TFTP İstemci örneğini silme

### <a name="prototype"></a>Prototype

```C
UINT nxd_tftp_client_delete(NX_TFTP_CLIENT *tftp_client_ptr);
```

### <a name="description"></a>Description

Bu hizmet, önceden oluşturulmuş bir TFTP İstemci örneğini siler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **tftp_client_ptr** Daha önce oluşturulan TFTP istemci örneğinin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı TFTP İstemcisi silme.

- NX_PTR_ERROR (0x16) Geçersiz işaretçi girişi.

- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Delete a TFTP Client instance. */
status =  nxd_tftp_client_delete(&my_tftp_client);

/* If status is NX_SUCCESS the TFTP Client instance was successfully
   deleted. */
```

## <a name="nxd_tftp_client_error_info_get"></a>nxd_tftp_client_error_info_get

İstemci hata bilgilerini al

### <a name="prototype"></a>Prototype

```C
UINT nxd_tftp_client_error_info_get(NX_TFTP_CLIENT *tftp_client_ptr,
                        UINT *error_code, CHAR **error_string);
```

### <a name="description"></a>Description

Bu hizmet alınan son hata kodunu döndürür ve işaretçiyi istemcinin iç hata dizesine ayarlar. Hata koşullarında, kullanıcı sunucu tarafından gönderilen son hatayı görüntülemeye devam ediyor. Null hata dizesi hiçbir hata olmadığını gösterir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **tftp_client_ptr** Daha önce oluşturulan TFTP İstemci örneğinin işaretçisi.

- **error_code** Hata kodu için hedef alana işaretçi

- **error_string** Hata dizesi için hedefin işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı TFTP hata bilgileri alır.  

- NX_PTR_ERROR (0x16) Geçersiz TFTP İstemci işaretçisi.

- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Get error information for client. */
status =  nxd_tftp_client_error_info_get(&my_tftp_client, &error_code,
                    &error_string_ptr);

/* If status is NX_SUCCESS the error code and error string are available. */
```

## <a name="nxd_tftp_client_file_close"></a>nxd_tftp_client_file_close

İstemci dosyasını kapatma

### <a name="prototype"></a>Prototype

```C
UINT nxd_tftp_client_file_close(NX_TFTP_CLIENT *tftp_client_ptr,
                                    UINT ip_type);
```

### <a name="description"></a>Description

Bu hizmet, bu TFTP İstemci örneği tarafından önceden açılmış olan dosyayı kapatır. Bir TFTP İstemci örneğinin aynı anda yalnızca bir dosya açmasına izin verilir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **tftp_client_ptr** Daha önce oluşturulan TFTP İstemci örneğinin işaretçisi.

- **ip_type** Hangi IP protokolünün kullan kullanır olduğunu gösterme. Geçerli seçenekler IPv4 (4) veya IPv6 (6) seçenekleridir.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı TFTP dosyası kapatma.

- NX_PTR_ERROR (0x16) Geçersiz işaretçi girişi.

- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz.

- NX_INVALID_PARAMETERS (0x4D) İşaretçi olmayan giriş geçersiz.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Close the previously opened file associated with “my_client”. */
status =  nxd_tftp_client_file_close(&my_tftp_client);

/* If status is NX_SUCCESS the TFTP file is closed. */
```

## <a name="nx_tftp_client_file_open"></a>nx_tftp_client_file_open

TFTP istemci dosyasını açma

### <a name="prototype"></a>Prototype

```C
UINT nx_tftp_client_file_open(NX_TFTP_CLIENT *tftp_client_ptr, 
            CHAR *file_name, NXD_ADDRESS *server_ip_address, UINT 
            open_type, ULONG wait_option);
```

### <a name="description"></a>Description

Bu hizmet belirtilen IP adresindeki TFTP sunucusunda belirtilen dosyayı açmaya çalışır. Dosya okuma ya da yazma için açılacak. 

> [!NOTE] 
> Bu yalnızca IPv4 paketleriyle sınırlıdır ve NetX TFTP uygulamalarını desteklemeye yöneliktir. Geliştiricilere, eşdeğer "Duo" hizmet nxd_tftp_client_file_open kullanmak için uygulamalarının bağlantı noktası kullanmaları önerilir *.*

### <a name="input-parameters"></a>Giriş Parametreleri

- **tftp_client_ptr** TFTP denetim bloğu işaretçisi.

- **file_name** ASCII dosya adı, NULL ile sonlandırılmış ve uygun yol bilgileri.

- **server_ip_address** Sunucu TFTP adresi.

- **open_type** Açık istek türü, aşağıdakilerden biri:

  **NX_TFTP_OPEN_FOR_READ** (0x01)

  **NX_TFTP_OPEN_FOR_WRITE** (0x02)

- **wait_option** Hizmetin TFTP Istemci dosyasını açma süresini ne kadar bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:

  **zaman aşımı değeri** (0x00000001 üzerinden 0xfffffffe)

  **TX_WAIT_FOREVER** (0xffffffff) 
  
  TX_WAIT_FOREVER seçilmesi çağıran iş parçacığının bir TFTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur. 
  
  Sayısal bir değer (1-0xFFFFFFFE) seçildiğinde, TFTP sunucu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.

- **ip_type** Hangi IP protokolünün kullanılacağını belirtin. Geçerli seçenekler IPv4 (4) veya IPv6 (6).

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Istemci dosyası başarıyla açıldı

- **NX_TFTP_NOT_CLOSED** (0xC3) istemcisinde zaten dosya açık

- **NX_INVALID_TFTP_SERVER_ADDRESS** (0x08) geçersiz sunucu adresi alındı

- **NX_TFTP_NO_ACK_RECEIVED** (0x09) sunucudan ACK alınmadı

- **NX_TFTP_INVALID_SERVER_ADDRESS** (0x08) geçersiz sunucu IP 'si alındı

- **NX_TFTP_CODE_ERROR** (0x05) alınan hata kodu

- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi.

- NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı

- NX_IP_ADDRESS_ERROR (0x21) geçersiz sunucu IP adresi

- NX_OPTION_ERROR (0x0A) geçersiz açık tür

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Define the TFTP server address. */
NXD_ADDRESS server_ip_address;

server_ip_address.nxd_ip_version = NX_IP_VERSION_V6;
server _ip_address.nxd_ip_address.v6[0] = 0x20010db8;
server _ip_address.nxd_ip_address.v6[1] = 0xf101;
server _ip_address.nxd_ip_address.v6[2] = 0;
server _ip_address.nxd_ip_address.v6[3] = 0x101;

/* Open file “test.txt” for reading on the TFTP Server. */
status =  nxd_tftp_client_file_open(&my_tftp_client, “test.txt”,
        & server_ip_address, NX_TFTP_OPEN_FOR_READ, 200);

/* If status is NX_SUCCESS the “test.txt” file is now open for reading. */
```

## <a name="nxd_tftp_client_file_open"></a>nxd_tftp_client_file_open

TFTP istemci dosyasını aç

### <a name="prototype"></a>Prototype

```C
UINT nxd_tftp_client_file_open(NX_TFTP_CLIENT *tftp_client_ptr,
        CHAR *file_name, NXD_ADDRESS *server_ip_address, UINT 
        open_type, ULONG wait_option, UINT ip_type);
```

### <a name="description"></a>Description

Bu hizmet, belirtilen bir IPv6 adresinde belirtilen dosyayı TFTP sunucusunda açmaya çalışır. Dosya okuma ya da yazma için açılacak.

### <a name="input-parameters"></a>Giriş Parametreleri

- **tftp_client_ptr** TFTP denetim bloğu işaretçisi.

- **file_name** ASCII dosya adı, NULL ile sonlandırılmış ve uygun yol bilgileri.

- **server_ip_address** Sunucu TFTP adresi.

- **open_type** Açık istek türü, aşağıdakilerden biri:

  **NX_TFTP_OPEN_FOR_READ** (0x01)

  **NX_TFTP_OPEN_FOR_WRITE** (0x02)

- **wait_option** Hizmetin TFTP Istemci dosyasını açma süresini ne kadar bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:

  **zaman aşımı değeri** (0x00000001 üzerinden 0xfffffffe)

  **TX_WAIT_FOREVER** (0xffffffff)

  TX_WAIT_FOREVER seçilmesi çağıran iş parçacığının bir TFTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.

  Sayısal bir değer (1-0xFFFFFFFE) seçildiğinde, TFTP sunucu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.

- **ip_type** Hangi IP protokolünün kullanılacağını belirtin. Geçerli seçenekler IPv4 (4) veya IPv6 (6).

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Istemci dosyası başarıyla açıldı

- **NX_TFTP_NOT_CLOSED** (0xC3) istemcisinde zaten dosya açık

- **NX_INVALID_TFTP_SERVER_ADDRESS** (0x08) geçersiz sunucu adresi alındı

- **NX_TFTP_NO_ACK_RECEIVED** (0x09) sunucudan ACK alınmadı

- **NX_TFTP_INVALID_IP_VERSION** (0x0C) geçersiz IP sürümü

- **NX_TFTP_INVALID_SERVER_ADDRESS** (0x08) geçersiz sunucu IP 'si alındı

- **NX_TFTP_CODE_ERROR** (0x05) alınan hata kodu

- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi.

- NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı

- NX_IP_ADDRESS_ERROR (0x21) geçersiz sunucu IP adresi

- NX_OPTION_ERROR (0x0A) geçersiz açık tür

- NX_INVALID_PARAMETERS (0x4D) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Define the TFTP server address. */
NXD_ADDRESS server_ip_address;

server_ip_address.nxd_ip_version = NX_IP_VERSION_V6;
server _ip_address.nxd_ip_address.v6[0] = 0x20010db8;
server _ip_address.nxd_ip_address.v6[1] = 0xf101;
server _ip_address.nxd_ip_address.v6[2] = 0;
server _ip_address.nxd_ip_address.v6[3] = 0x101;

/* Open file “test.txt” for reading on the TFTP Server. */
status =  nxd_tftp_client_file_open(&my_tftp_client, “test.txt”,
                & server_ip_address, NX_TFTP_OPEN_FOR_READ, 200);

/* If status is NX_SUCCESS the “test.txt” file is now open for reading. */
```

## <a name="nxd_tftp_client_file_read"></a>nxd_tftp_client_file_read

İstemci dosyasından bir blok oku

### <a name="prototype"></a>Prototype

```C
UINT nxd_tftp_client_file_read(NX_TFTP_CLIENT *tftp_client_ptr,
                        NX_PACKET **packet_ptr, ULONG wait_option,
                        UINT ip_type);
```

### <a name="description"></a>Description

Bu hizmet, daha önce açılan TFTP Istemci dosyasından 512 baytlık bir blok okur. 512 bayttan az bir blok içeren bir blok, dosyanın sonuna işaret eder.

### <a name="input-parameters"></a>Giriş Parametreleri

- **tftp_client_ptr** TFTP Istemci denetim bloğu işaretçisi.

- **packet_ptr** Dosyadan okunan blok içeren paket hedefi.

- **wait_option** Hizmetin okuma işleminin tamamlanmasını bekleyeceği süreyi tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:

  **zaman aşımı değeri** (0x00000001 üzerinden 0xfffffffe)

  **TX_WAIT_FOREVER** (0xffffffff)

  TX_WAIT_FOREVER seçilmesi çağıran iş parçacığının, TFTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.

  Sayısal bir değer (1-0xFFFFFFFE) seçilmesi, TFTP sunucusunun dosya bloğunu göndermesini beklerken askıya alınması için beklenecek en fazla Zamanlayıcı sayısını belirtir.

- **ip_type** Hangi IP protokolünün kullanılacağını belirtin. Geçerli seçenekler IPv4 (4) veya IPv6 (6).

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı istemci bloğu okuma

- **NX_TFTP_NOT_OPEN** (0xC3) belirtilen istemci dosyası okuma için açık değil

- **NX_NO_PACKET** (0x01) sunucudan paket alınmadı.

- **NX_INVALID_TFTP_SERVER_ADDRESS** (0x08) geçersiz sunucu adresi alındı

- **NX_TFTP_NO_ACK_RECEIVED** (0x09) sunucudan ACK alınmadı

- **NX_TFTP_END_OF_FILE** (0xC5) dosya sonu algılandı (hata değil).

- **NX_TFTP_INVALID_IP_VERSION** (0x0C) geçersiz IP sürümü

- **NX_TFTP_CODE_ERROR** (0x05) alınan hata kodu

- **NX_TFTP_FAILED** (0xC2) bilinmeyen TFTP kodu alındı

- **NX_TFTP_INVALID_BLOCK_NUMBER** (0X0a) geçersiz blok numarası alındı

- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi.

- NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı

- NX_INVALID_PARAMETERS (0x4D) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Read a block from a previously opened file of “my_client”. */
status =  nxd_tftp_client_file_read(&my_tftp_client, &return_packet_ptr, 200);

/* If status is NX_SUCCESS a block of the TFTP file is in the payload of
   “return_packet_ptr”. */
```

## <a name="nxd_tftp_client_file_write"></a>nxd_tftp_client_file_write

Istemci dosyasına bir blok yaz

### <a name="prototype"></a>Prototype

```C
UINT nxd_tftp_client_file_write(NX_TFTP_CLIENT *tftp_client_ptr,
            NX_PACKET *packet_ptr, ULONG wait_option, UINT ip_type);
```

### <a name="description"></a>Description

Bu hizmet, daha önce açılmış olan TFTP Istemci dosyasına 512 baytlık bir blok yazar. 512 bayttan daha az bir blok belirtmek dosyanın sonuna işaret eder.

### <a name="input-parameters"></a>Giriş Parametreleri

- **tftp_client_ptr** TFTP Istemci denetim bloğu işaretçisi.

- **packet_ptr** Dosyaya yazılacak bloğu içeren paket.

- **wait_option** Hizmetin yazma işleminin tamamlanmasını bekleyeceği süreyi tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:

  **zaman aşımı değeri** (0x00000001 üzerinden 0xfffffffe)

  **TX_WAIT_FOREVER** (0xffffffff)

  TX_WAIT_FOREVER seçilmesi çağıran iş parçacığının, TFTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.
 
  Sayısal bir değer (1-0xFFFFFFFE) seçilmesi, TFTP sunucusunun yazma isteği için bir ACK göndermesini beklerken askıya alınması için beklenecek en fazla Zamanlayıcı sayısını belirtir.

- **ip_type** Hangi IP protokolünün kullanılacağını belirtin. Geçerli seçenekler IPv4 (4) veya IPv6 (6).

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı istemci blok yazma

- **NX_TFTP_NOT_OPEN** (0xC3) belirtilen istemci dosyası yazma için açık değil

- **NX_TFTP_TIMEOUT** (0xC1) sunucu onayı beklenirken zaman aşımı oluştu

- **NX_INVALID_TFTP_SERVER_ADDRESS** (0x08) geçersiz sunucu adresi alındı

- **NX_TFTP_NO_ACK_RECEIVED** (0x09) sunucudan ACK alınmadı

- **NX_TFTP_INVALID_IP_VERSION** (0x0C) geçersiz IP sürümü

- **NX_INVALID_TFTP_SERVER_ADDRESS** (0x08) geçersiz sunucu adresi alındı

- **NX_TFTP_CODE_ERROR** (0x05) alınan hata kodu

- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi.

- NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı

- NX_INVALID_PARAMETERS (0x4D) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Write a block to the previously opened file of “my_client”. */
status =  nxd_tftp_client_file_write(&my_tftp_client, packet_ptr, 200);

/* If status is NX_SUCCESS the block in the payload of “packet_ptr” was 
   written to the TFTP file opened by “my_client”. */
```

## <a name="nxd_tftp_client_packet_allocate"></a>nxd_tftp_client_packet_allocate

Istemci dosyası yazma için paket ayır

### <a name="prototype"></a>Prototype

```C
UINT nxd_tftp_client_packet_allocate(NX_PACKET_POOL *pool_ptr,
                        NX_PACKET **packet_ptr, ULONG wait_option,
                        UINT ip_type);
```

### <a name="description"></a>Description

Bu hizmet, belirtilen paket havuzundan bir UDP paketi ayırır ve paket çağırana döndürülmeden önce 4 baytlık TFTP üst bilgisine yer açar. Çağıran daha sonra bir istemci dosyasına yazmak için bir arabellek oluşturabilir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **pool_ptr** Paket havuzu işaretçisi.

- **packet_ptr** Ayrılmış pakete işaretçinin hedefi.

- **wait_option** Hizmetin paket ayırma işleminin tamamlanmasını ne kadar bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:

  **zaman aşımı değeri** (0x00000001 üzerinden 0xfffffffe)

  **TX_WAIT_FOREVER** (0xffffffff)

  TX_WAIT_FOREVER seçilmesi çağıran iş parçacığının ayırma tamamlanana kadar süresiz olarak askıda kalmasına neden olur.

  Sayısal bir değer (1-0xFFFFFFFE) seçilmesi, paket ayırmayı beklerken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.

- **ip_type** Hangi IP protokolünün kullanılacağını belirtin. Geçerli seçenekler IPv4 (4) veya IPv6 (6).

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı paket ayırma

- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi.

- NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı

- NX_INVALID_PARAMETERS (0x4D) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Allocate a packet for TFTP file write. */
status =  nxd_tftp_client_packet_allocate(&my_pool, &packet_ptr, 200);

/* If status is NX_SUCCESS “packet_ptr” contains the new packet. */
```

## <a name="nxd_tftp_client_set_interface"></a>nxd_tftp_client_set_interface

TFTP istekleri için fiziksel arabirimi ayarla

### <a name="prototype"></a>Prototype

```C
UINT nxd_tftp_client_set_interface(NX_TFTP_CLIENT *tftp_client_ptr,
                                    UINT if_index);
```

### <a name="description"></a>Description

Bu hizmet, TFTP Istemcisine yönelik fiziksel arabirimi TFTP paketleri gönderecek ve alacak şekilde ayarlamak için giriş arabirimi dizinini kullanır. Birincil arabirim için varsayılan değer sıfırdır.

> [!NOTE]
> NetX Duo bu hizmeti kullanmak için çok ana adresleme 'yi (v 5.6 veya üzeri) desteklemelidir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **tftp_client_ptr** TFTP Istemci örneğine yönelik işaretçi

- **if_index** Kullanılacak fiziksel arabirimin dizini

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) arabirimi başarıyla ayarlandı (0X0b) geçersiz arabirim girişi

- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi.

- NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı

- NX_TFTP_INVALID_INTERFACE (0x0B) geçersiz arabirim girişi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Specify the primary interface for TFTP requests. */
status =  nxd_tftp_client_set_interface(&client, 0);

/* If status is NX_SUCCESS the primary interface will be use for TFTP communications. */
```

## <a name="nxd_tftp_server_create"></a>nxd_tftp_server_create

TFTP sunucusu oluştur

### <a name="prototype"></a>Prototype

```C
UINT nxd_tftp_server_create(NX_TFTP_SERVER *tftp_server_ptr,
            CHAR *tftp_server_name, NX_IP *ip_ptr, FX_MEDIA *media_ptr, 
            VOID *stack_ptr, ULONG stack_size,
            NX_PACKET_POOL *pool_ptr);
```

### <a name="description"></a>Description

Bu hizmet, 69 numaralı bağlantı noktasında TFTP Istemci isteklerine yanıt veren bir TFTP sunucusu oluşturur. Sunucunun *nxd_tftp_server_start* sonraki bir çağrısıyla başlatılması gerekir.

> [!IMPORTANT]
> Uygulama, sağlanan IP örneğinin, paket havuzunun ve FileX Medya örneğinin zaten oluşturulduğundan emin olmalıdır. Buna ek olarak, bu hizmet çağrılmadan önce IP örneği için UDP 'nin etkinleştirilmesi gerekir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **tftp_server_ptr** TFTP sunucu denetim bloğu işaretçisi.

- **tftp_server_name** Bu TFTP sunucu örneğinin adı

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.

- **media_ptr** FileX medya örneğine yönelik işaretçi.

- **stack_ptr** TFTP sunucusu yığın alanı işaretçisi.

- **stack_size** TFTP sunucu yığınındaki bayt sayısı.

- **pool_ptr** TFTP paket havuzu işaretçisi. 

> [!NOTE]
> Sağlanan havuzun paket yükleri en az 580 bayt boyutunda olmalıdır. <sup>1</sup>

<sup>1</sup> bir paketin veri bölümü tam olarak 512 bayttır, ancak paket yükü boyutu en az 572 bayt olmalıdır. Kalan bayt sayısı, UDP, IPv6 ve Ethernet üstbilgileri ve hizalama için sürücü için gereken olası sondaki baytlar için kullanılır.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı sunucu oluşturma

- **NX_TFTP_POOL_ERROR** (0xC6) paket havuzunda 560 bayttan daha az paket boyutu vardır

- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, Iş parçacıkları

### <a name="example"></a>Örnek

```C
/* Create a TFTP Server called “my_server”. */
status =  nxd_tftp_server_create(&my_server, “My TFTP Server”, &server_ip, 
                &ram_disk, stack_ptr, 2048, pool_ptr);

/* If status is NX_SUCCESS the TFTP Server is created. */
```

## <a name="nxd_tftp_server_delete"></a>nxd_tftp_server_delete

TFTP sunucusunu Sil

### <a name="prototype"></a>Prototype

```C
UINT nxd_tftp_server_delete(NX_TFTP_SERVER *tftp_server_ptr);
```

### <a name="description"></a>Description

Bu hizmet, daha önce oluşturulmuş bir TFTP sunucusunu siler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **tftp_server_ptr** TFTP sunucu denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı sunucu silme

- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi.

- NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Delete the TFTP Server called “my_server”. */
status =  nxd_tftp_server_delete(&my_server);

/* If status is NX_SUCCESS the TFTP Server is deleted. */
```

## <a name="nxd_tftp_server_start"></a>nxd_tftp_server_start

TFTP sunucusunu Başlat

### <a name="prototype"></a>Prototype

```C
UINT nxd_tftp_server_start(NX_TFTP_SERVER *tftp_server_ptr);
```

### <a name="description"></a>Description

Bu hizmet, önceden oluşturulan TFTP sunucusunu başlatır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **tftp_server_ptr** TFTP sunucu denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı sunucu başlatması

- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi.
 
### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="example"></a>Örnek

```C
/* Start the TFTP Server called “my_server”. */
status =  nxd_tftp_server_start(&my_server);

/* If status is NX_SUCCESS the TFTP Server is started. */
```

## <a name="nxd_tftp_server_stop"></a>nxd_tftp_server_stop

TFTP sunucusunu durdur

### <a name="prototype"></a>Prototype

```C
UINT nxd_tftp_server_stop(NX_TFTP_SERVER *tftp_server_ptr);
```

### <a name="description"></a>Description

Bu hizmet, daha önce oluşturulan TFTP sunucusunu durduruyor.

### <a name="input-parameters"></a>Giriş Parametreleri

- **tftp_server_ptr** TFTP sunucu denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı sunucu durdu

- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi.

- NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Stop the TFTP Server called “my_server”. */
status =  nxd_tftp_server_stop(&my_server);

/* If status is NX_SUCCESS the TFTP Server is stopped. */
```