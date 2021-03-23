---
title: Bölüm 3-Azure RTOS NetX Duo TFTP hizmetlerinin açıklaması
description: Bu bölüm, tüm NetX Duo TFTP hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 56f0d8edb991fff6ae30b6411e375ace58c544f7
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825708"
---
# <a name="chapter-3---description-of-azure-rtos-netx-duo-tftp-services"></a>Bölüm 3-Azure RTOS NetX Duo TFTP hizmetlerinin açıklaması

Bu bölüm, tüm NetX Duo TFTP hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir. Aksi belirtilmediği takdirde, tüm hizmetler IPv6 ve IPv4 iletişimini destekler.

Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_DISABLE_ERROR_CHECKING** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.

- **nxd_tftp_client_file_open**: *Açık TFTP istemci dosyası*

- **nxd_tftp_client_create**: *TFTP istemci örneği oluşturma*

- **nxd_tftp_client_delete**: *TFTP istemci örneğini silme*

- **nxd_tftp_client_error_info_get**: *istemci hata bilgilerini al*

- **nxd_tftp_client_file_close**: *istemci dosyasını kapat*

- **nxd_tftp_client_file_open**: *istemci dosyasını aç*

- **nxd_tftp_client_file_read**: *istemci dosyasından bir blok oku*

- **nxd_tftp_client_file_write**: *istemci dosyasına blok yaz*

- **nxd_tftp_client_packet_allocate**: *istemci dosyası yazma için paket ayır*

- **nxd_tftp_client_set_interface**: *TFTP istekleri için fiziksel arabirimi ayarla*

- **nxd_tftp_server_create**: *TFTP sunucusu oluşturma*

- **nxd_tftp_server_delete**: *TFTP sunucusunu Sil*

- **nxd_tftp_server_start**: *TFTP sunucusunu Başlat*

- **nxd_tftp_server_stop**: *TFTP sunucusunu durdur*

> [!NOTE] 
> Yukarıda listelenen tüm hizmetlerin IPv4 eşdeğerleri NetX Duo TFTP Istemcisinde ve sunucu gibi *nx_tftp_server_create* ve *nx_tftp_client_file_open* kullanılabilir. Aşağıdaki sayfalarda yalnızca ' Duo ' API açıklamaları, örneğin *nxd_* ile başlayan hizmetler verilmiştir. NXD_ADDRESS \* girişi belirtildiğinde, IPv4 EŞDEĞERI API, ulong girişi için çağırır. Aksi takdirde, API 'nin kullanılması fark yoktur.

## <a name="nxd_tftp_client_create"></a>nxd_tftp_client_create

TFTP Istemci örneği oluşturma

### <a name="prototype"></a>Prototype

```C
UINT nxd_tftp_client_create(NX_TFTP_CLIENT *tftp_client_ptr,  
     CHAR *tftp_client_name, NX_IP *ip_ptr, NX_PACKET_POOL *pool_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, daha önce oluşturulan IP örneği için bir TFTP Istemci örneği oluşturur.

> [!IMPORTANT]
> Uygulama, sağlanan IP ve paket havuzunun daha önce oluşturulduğundan emin olmalıdır. Buna ek olarak, bu hizmet çağrılmadan önce IP örneği için UDP 'nin etkinleştirilmesi gerekir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **tftp_client_ptr** TFTP Istemci denetim bloğu işaretçisi.

- **tftp_client_name** Bu TFTP Istemci örneğinin adı

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.

- **pool_ptr** Paket havuzu TFTP Istemci örneği işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**(0x00) başarılı TFTP oluşturma.

- **NX_TFTP_INVALID_IP_VERSION** (0x0C) geçersiz veya desteklenmeyen IP sürümü

- **NX_TFTP_INVALID_SERVER_ADDRESS** (0x08) GEÇERSIZ sunucu IP adresi alındı

- **NX_TFTP_NO_ACK_RECEIVED** (0x09) sunucu onayı alınmadı

- NX_PTR_ERROR (0x16) geçersiz IP, havuz veya TFTP işaretçisi.

- NX_INVALID_PARAMETERS (0x4D) geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

Başlatma ve Iş parçacıkları

### <a name="example"></a>Örnek

```C
/* Create a TFTP Client instance. */
status =  nxd_tftp_client_create(&my_tftp_client, “My TFTP Client”, 
                                                    &my_ip, &pool_ptr);

/* If status is NX_SUCCESS a TFTP Client instance was successfully
   created. */
```

## <a name="nxd_tftp_client_delete"></a>nxd_tftp_client_delete

TFTP Istemci örneğini silme

### <a name="prototype"></a>Prototype

```C
UINT nxd_tftp_client_delete(NX_TFTP_CLIENT *tftp_client_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, daha önce oluşturulmuş bir TFTP Istemci örneğini siler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **tftp_client_ptr** Daha önce oluşturulan TFTP istemci örneğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı TFTP istemcisi silme.

- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi.

- NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

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

### <a name="description"></a>Açıklama

Bu hizmet, alınan son hata kodunu döndürür ve işaretçiyi istemcinin iç hata dizesine ayarlar. Hata koşullarında, Kullanıcı sunucu tarafından gönderilen son hatayı görüntüleyebilir. Null hata dizesi bir hata olduğunu gösterir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **tftp_client_ptr** Daha önce oluşturulan TFTP Istemci örneğine yönelik işaretçi.

- **error_code** Hata kodu için hedef alan işaretçisi

- **error_string** Hata dizesi için hedef işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı TFTP hata bilgileri al.  

- NX_PTR_ERROR (0x16) geçersiz TFTP Istemci işaretçisi.

- NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Get error information for client. */
status =  nxd_tftp_client_error_info_get(&my_tftp_client, &error_code,
                    &error_string_ptr);

/* If status is NX_SUCCESS the error code and error string are available. */
```

## <a name="nxd_tftp_client_file_close"></a>nxd_tftp_client_file_close

İstemci dosyasını kapat

### <a name="prototype"></a>Prototype

```C
UINT nxd_tftp_client_file_close(NX_TFTP_CLIENT *tftp_client_ptr,
                                    UINT ip_type);
```

### <a name="description"></a>Açıklama

Bu hizmet, bu TFTP Istemci örneği tarafından daha önce açılmış dosyayı kapatır. Bir TFTP Istemci örneğinin aynı anda yalnızca bir dosya açmasına izin verilir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **tftp_client_ptr** Daha önce oluşturulan TFTP Istemci örneğine yönelik işaretçi.

- **ip_type** Hangi IP protokolünün kullanılacağını belirtin. Geçerli seçenekler IPv4 (4) veya IPv6 (6).

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı TFTP dosyası kapatma.

- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi.

- NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.

- NX_INVALID_PARAMETERS (0x4D) geçersiz işaretçi girişi.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Close the previously opened file associated with “my_client”. */
status =  nxd_tftp_client_file_close(&my_tftp_client);

/* If status is NX_SUCCESS the TFTP file is closed. */
```

## <a name="nx_tftp_client_file_open"></a>nx_tftp_client_file_open

TFTP istemci dosyasını aç

### <a name="prototype"></a>Prototype

```C
UINT nx_tftp_client_file_open(NX_TFTP_CLIENT *tftp_client_ptr, 
            CHAR *file_name, NXD_ADDRESS *server_ip_address, UINT 
            open_type, ULONG wait_option);
```

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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