---
title: Bölüm 3 - FTP hizmetlerinin açıklaması
description: Bu bölümde, tüm NetX FTP hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 07/09/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: d08d3c07f7be016ece68ff2f58b9ac5ba93ded780105bce362674ed36b5b885d
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116792375"
---
# <a name="chapter-3---description-of-ftp-services"></a>Bölüm 3 - FTP hizmetlerinin açıklaması

Bu bölüm, tüm NetX FTP hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada (aynı hizmetin IPv4 ve IPv6 eşdeğerlerinin eşleştirilmiş olduğu durum dışında) bir açıklama içerir.

> [!NOTE]
> Aşağıdaki API açıklamalarında yer alan "Dönüş Değerleri" bölümünde, **KALıN**  olmayan değerler tamamen devre dışı bırakılırken, BOLD NX_DISABLE_ERROR_CHECKING API hata denetimlerini devre dışı bırakmak için kullanılan tanımdan etkilenmez.

## <a name="nx_ftp_client_connect"></a>nx_ftp_client_connect

Bağlan IPv4 üzerinden bir FTP Sunucusuna yükleme

### <a name="prototype"></a>Prototype

```C
UINT nx_ftp_client_connect(NX_FTP_CLIENT *ftp_client_ptr,
    ULONG server_ip, CHAR *username, CHAR *password,
    ULONG wait_option);
```

### <a name="description"></a>Description

Bu hizmet, daha önce oluşturulan NetX FTP İstemcisi örneğini sağlanan IP adresine FTP Sunucusuna bağlar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_client_ptr** FTP İstemcisi denetim bloğuna işaretçi.
- **server_ip** FTP Sunucusunun IP adresi.
- **kullanıcı adı** Kimlik doğrulaması için istemci kullanıcı adı.
- **parola** Kimlik doğrulaması için istemci parolası.
- **wait_option** Hizmetin FTP İstemcisi bağlantısını ne kadar süre bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri** (0x00000001 0xFFFFFFFE) Sayısal bir değer (1-0xFFFFFFFE) seçmek, FTP Sunucusu yanıtı beklerken askıya alınacak zamanlayıcı saat sayısı üst sayısını belirtir.
  - **TX_WAIT_FOREVER** (0xFFFFFFFF) bir FTP sunucusu TX_WAIT_FOREVER yanıt verene kadar çağrı iş parçacığının süresiz olarak askıya alınmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) FTP bağlantısı.
- **NX_TFTP_EXPECTED_22X_CODE** (0xDB) 22X (tamam) yanıtı alam
- **NX_FTP_EXPECTED_23X_CODE** (0xDC) 23X (tamam) yanıtı alam
- **NX_FTP_EXPECTED_33X_CODE** (0xDE) 33X (tamam) yanıtı alam
- **NX_FTP_NOT_DISCONNECTED** (0xD4) İstemcisi zaten bağlı.
- NX_PTR_ERROR (0x07) Geçersiz işaretçi girişi.
- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz.
- NX_IP_ADDRESS_ERROR (0x21) Geçersiz IP adresi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Connect the FTP Client instance “my_client” to the FTP Server at

IP address 1.2.3.4. */

status = nx_ftp_client_connect(&my_client, IP_ADDRESS(1,2,3,4), NULL, NULL, 100);

/* If status is NX_SUCCESS an FTP Client instance was successfully  
    connected to the FTP Server. */
```

### <a name="see-also"></a>Ayrıca Bkz.

nx_ftp_client_create, nx_ftp_client_delete, nx_ftp_client_directory_create, nx_ftp_client_disconnect, nxd_ftp_client_connect

## <a name="nxd_ftp_client_connect"></a>nxd_ftp_client_connect

Bağlan IPv6 desteğine sahip bir FTP Sunucusuna yükleme

### <a name="prototype"></a>Prototype

```C
UINT nxd_ftp_client_connect(NX_FTP_CLIENT *ftp_client_ptr,
    NXD_ADDRESS *server_ipduo, CHAR *username, CHAR *password,
    ULONG wait_option);
```

### <a name="description"></a>Description

Bu hizmet, daha önce oluşturulan NetX Duo FTP İstemcisi örneğini verilen IP adresi üzerinden FTP Sunucusuna bağlar. Hem IPv4 hem de IPv6 ağları de desteklemektedir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_client_ptr** FTP İstemcisi denetim bloğuna işaretçi.
- **server_ipduo** FTP Sunucusunun IP adresi.
- **kullanıcı adı** Kimlik doğrulaması için istemci kullanıcı adı.
- **parola** Kimlik doğrulaması için istemci parolası.
- **wait_option** Hizmetin FTP İstemcisi bağlantısını ne kadar süre bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri** (0x00000001 0xFFFFFFFE) Sayısal bir değer (1-0xFFFFFFFE) seçmek, FTP Sunucusu yanıtı beklerken askıya alınacak zamanlayıcı saat sayısı üst sayısını belirtir.
  - **TX_WAIT_FOREVER** (0xFFFFFFFF) bir FTP sunucusu TX_WAIT_FOREVER yanıt verene kadar çağrı iş parçacığının süresiz olarak askıya alınmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) FTP bağlantısı.
- **NX_TFTP_EXPECTED_22X_CODE** (0xDB) 22X (tamam) yanıtı alam
- **NX_FTP_EXPECTED_23X_CODE** (0xDC) 23X (tamam) yanıtı alam
- **NX_FTP_EXPECTED_33X_CODE** (0xDE) 33X (tamam) yanıtı alam
- **NX_FTP_NOT_DISCONNECTED** (0xD4) İstemcisi zaten bağlı
- NX_PTR_ERROR (0x07) Geçersiz işaretçi inout.
- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz.
- NX_IP_ADDRESS_ERROR (0x21) Geçersiz IP adresi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Connect an FTP Client instance to the FTP Server. */

/* Set up an IPv6 address for the server here.
    Note this could also be an IPv4 address as well*/

server_ip_addr.nxd_ip_address.v6[3] = 0x106;
server_ip_addr.nxd_ip_address.v6[2] = 0x0;
server_ip_addr.nxd_ip_address.v6[1] = 0x0000f101;
server_ip_addr.nxd_ip_address.v6[0] = 0x20010db8;
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V6;

status = nxd_ftp_client_connect(&my_client, server_ip_addr, NULL, NULL, 100);

/* If status is NX_SUCCESS an FTP Client instance was successfully  
    connected to the FTP Server. */
```

### <a name="see-also"></a>Ayrıca Bkz.

nx_ftp_client_create, nx_ftp_client_delete, nx_ftp_client_directory_create, nx_ftp_client_disconnect, nx_ftp_client_connect

## <a name="nx_ftp_client_create"></a>nx_ftp_client_create

FTP İstemcisi örneği oluşturma

### <a name="prototype"></a>Prototype

```C
UINT nx_ftp_client_create(NX_FTP_CLIENT *ftp_client_ptr,
    CHAR *ftp_client_name, NX_IP *ip_ptr, ULONG window_size,
    NX_PACKET_POOL *pool_ptr);
```

### <a name="description"></a>Description

Bu hizmet bir FTP İstemcisi örneği oluşturur.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_client_ptr** FTP İstemcisi denetim bloğuna işaretçi.
- **ftp_client_name** FTP İstemcisi adı.
- **ip_ptr** Daha önce oluşturulan IP örneğinin işaretçisi.
- **window_size** Bu FTP İstemcisi'nin TCP yuvaları için tanıtılan pencere boyutu.
- **pool_ptr** Bu FTP İstemcisi için varsayılan paket havuzunun işaretçisi. Minimum paket yükünün tam yolu ve dosya veya dizin adını tutacak kadar büyük olması gerektiğini unutmayın.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) FTP İstemcisi oluşturma.
- NX_PTR_ERROR (0x07) Geçersiz işaretçi girişi.

### <a name="allowed-from"></a>İzin Verilen

Başlatma ve İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Create the FTP Client instance “my_client.” */
status = nx_ftp_client_create(&my_client, "My Client", &client_ip,
    2000, &client_pool);
/* If status is NX_SUCCESS the FTP Client instance was successfully created. */
```

## <a name="nx_ftp_client_delete"></a>nx_ftp_client_delete

FTP İstemcisi örneğini silme

### <a name="prototype"></a>Prototype

```C
UINT nx_ftp_client_delete(NX_FTP_CLIENT *ftp_client_ptr);
```

### <a name="description"></a>Description

Bu hizmet bir FTP İstemcisi örneğini siler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_client_ptr** FTP İstemcisi denetim bloğuna işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) BAŞARıLı FTP İstemcisi silme.
- **NX_FTP_NOT_DISCONNECTED** (0xD4) FTP istemcisinin bağlantısı kesildi
- NX_PTR_ERROR (0x07) Geçersiz FTP işaretçisi.
- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Delete the FTP Client instance “my_client.” */

status = nx_ftp_client_delete(&my_client);

/* If status is NX_SUCCESS the FTP Client instance was successfully  
    deleted. */
```

## <a name="nx_ftp_client_directory_create"></a>nx_ftp_client_directory_create

FTP Sunucusunda dizin oluşturma

### <a name="prototype"></a>Prototype

```C
UINT nx_ftp_client_directory_create(NX_FTP_CLIENT *ftp_client_ptr,
    CHAR *directory_name, ULONG wait_option);
```

### <a name="description"></a>Description

Bu hizmet, belirtilen FTP İstemcisi'ne bağlı FTP Sunucusunda belirtilen dizini oluşturur.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_client_ptr** FTP İstemcisi denetim bloğuna işaretçi.
- **directory_name** Oluşturul dizinin adı.
- **wait_option** Hizmetin FTP dizininin oluşturması için ne kadar bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri** (0x00000001 0xFFFFFFFE) Sayısal bir değer (1-0xFFFFFFFE) seçmek, FTP Sunucusu yanıtı beklerken askıya alınacak zamanlayıcı saat sayısı üst sayısını belirtir.
  - **TX_WAIT_FOREVER** (0xFFFFFFFF) bir FTP sunucusu TX_WAIT_FOREVER yanıt verene kadar çağrı iş parçacığının süresiz olarak askıya alınmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) FTP dizini oluşturma.
- **NX_FTP_NOT_CONNECTED** (0xD3) FTP İstemcisi bağlı değil.
- **NX_FTP_EXPECTED_2XX_CODE** (0xDA) 2XX (tamam) yanıtı alam
- NX_PTR_ERROR (0x07) Geçersiz FTP işaretçisi.
- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Create the directory “my_dir” on the FTP Server connected to
    the FTP Client instance “my_client.” */

status = nx_ftp_client_directory_create(&my_client, “my_dir”, 200);

/* If status is NX_SUCCESS the directory “my_dir” was successfully created. */
```

## <a name="nx_ftp_client_directory_default_set"></a>nx_ftp_client_directory_default_set

FTP Sunucusunda varsayılan dizini ayarlama

### <a name="prototype"></a>Prototype

```C
UINT nx_ftp_client_directory_default_set(NX_FTP_CLIENT *ftp_client_ptr,
    CHAR *directory_path, ULONG wait_option);
```

### <a name="description"></a>Description

Bu hizmet, belirtilen FTP İstemcisi'ne bağlı FTP Sunucusundaki varsayılan dizini ayarlar. Bu varsayılan dizin yalnızca bu istemcinin bağlantısı için geçerlidir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_client_ptr** FTP İstemcisi denetim bloğuna işaretçi.
- **directory_path** Ayar için dizin yolunun adı.
- **wait_option** Hizmetin FTP varsayılan dizin kümesi için ne kadar bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri** (0x00000001 0xFFFFFFFE) Sayısal bir değer (1-0xFFFFFFFE) seçmek, FTP Sunucusu yanıtı beklerken askıya alınacak zamanlayıcı saat sayısı üst sayısını belirtir.
  - **TX_WAIT_FOREVER** (0xFFFFFFFF) bir FTP sunucusu TX_WAIT_FOREVER yanıt verene kadar çağrı iş parçacığının süresiz olarak askıya alınmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı FTP varsayılan kümesi.
- **NX_FTP_NOT_CONNECTED** (0xD3) FTP İstemcisi bağlı değil.
- **NX_FTP_EXPECTED_2XX_CODE** (0xDA) 2XX (tamam) yanıtı alam
- NX_PTR_ERROR (0x07) Geçersiz FTP işaretçisi.
- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Set the default directory to “my_dir” on the FTP Server connected to
    the FTP Client instance “my_client.” */

status = nx_ftp_client_directory_default_set(&my_client, “my_dir”, 200);

/* If status is NX_SUCCESS the directory “my_dir” is the default directory. */
```

## <a name="nx_ftp_client_directory_delete"></a>nx_ftp_client_directory_delete

FTP Sunucusunda dizini silme

### <a name="prototype"></a>Prototype

```C
UINT nx_ftp_client_directory_delete(NX_FTP_CLIENT *ftp_client_ptr,
    CHAR *directory_name, ULONG wait_option);
```

### <a name="description"></a>Description

Bu hizmet, belirtilen FTP İstemcisi'ne bağlı FTP Sunucusunda belirtilen dizini siler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_client_ptr** FTP İstemcisi denetim bloğuna işaretçi.
- **directory_name** Silinecek dizinin adı.
- **wait_option** Hizmetin FTP dizini silme için ne kadar süre bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri** (0x00000001 0xFFFFFFFE) Sayısal bir değer (1-0xFFFFFFFE) seçmek, FTP Sunucusu yanıtı beklerken askıya alınacak zamanlayıcı saat sayısı üst sayısını belirtir.
  - **TX_WAIT_FOREVER** (0xFFFFFFFF) bir FTP sunucusu TX_WAIT_FOREVER yanıt verene kadar çağrı iş parçacığının süresiz olarak askıya alınmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) BAŞARıLı FTP dizini silme.
- **NX_FTP_NOT_CONNECTED** (0xD3) FTP İstemcisi bağlı değil.
- **NX_FTP_EXPECTED_2XX_CODE** (0xDA) 2XX (tamam) yanıtı alam
- NX_PTR_ERROR (0x07) Geçersiz FTP işaretçisi.
- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Delete directory “my_dir” on the FTP Server connected to
    the FTP Client instance “my_client.” */

status = nx_ftp_client_directory_delete(&my_client, “my_dir”, 200);

/* If status is NX_SUCCESS the directory “my_dir” is deleted. */
```

## <a name="nx_ftp_client_directory_listing_get"></a>nx_ftp_client_directory_listing_get

FTP Sunucusundan dizin listelemesi al

### <a name="prototype"></a>Prototype

```C
UINT nx_ftp_client_directory_listing_get(NX_FTP_CLIENT *ftp_client_ptr,
    CHAR *directory_name, NX_PACKET **packet_ptr,
    ULONG wait_option);
```

### <a name="description"></a>Description

Bu hizmet, belirtilen FTP İstemcisi'ne bağlı FTP Sunucusunda belirtilen dizinin içeriğini alır. Sağlanan paket işaretçisi bir veya daha fazla dizin girdisi içerir. Her giriş bir birleşimle \<cr/lf\> ayrılır. Dizin ***nx_ftp_client_directory_listing_continue*** işlemini tamamlamak için çağrılmaları gerekir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_client_ptr** FTP İstemcisi denetim bloğuna işaretçi.
- **directory_name** İçeriğini almak için dizinin adı.
- **packet_ptr** Hedef paket işaretçisine işaretçi. Başarılı olursa, paket yükü bir veya daha fazla dizin girdisi içerir.
- **wait_option** Hizmetin FTP dizin listesini ne kadar süre bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri** (0x00000001 0xFFFFFFFE) Sayısal bir değer (1-0xFFFFFFFE) seçmek, FTP Sunucusu yanıtı beklerken askıya alınacak zamanlayıcı saat sayısı üst sayısını belirtir.
  - **TX_WAIT_FOREVER** (0xFFFFFFFF) bir FTP sunucusu TX_WAIT_FOREVER yanıt verene kadar çağrı iş parçacığının süresiz olarak askıya alınmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) BAŞARıLı FTP dizin listesi.
- **NX_FTP_NOT_CONNECTED** (0xD3) FTP İstemcisi bağlı değil.
- **NX_NOT_ENABLED** (0x14) Hizmeti (IPv6) etkin değil
- **NX_FTP_EXPECTED_1XX_CODE** (0xD9) 1XX (tamam) yanıtı alam
- **NX_FTP_EXPECTED_2XX_CODE** (0xDA) 2XX (tamam) yanıtı alam
- NX_PTR_ERROR (0x07) Geçersiz FTP işaretçisi.
- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Get the contents of directory “my_dir” on the FTP Server connected to
    the FTP Client instance “my_client.” */

status = nx_ftp_client_directory_listing_get(&my_client, “my_dir”, &my_packet,
    200);

/* If status is NX_SUCCESS, one or more entries of the directory “my_dir”
    can be found in “my_packet”. */
```

## <a name="nx_ftp_client_directory_listing_continue"></a>nx_ftp_client_directory_listing_continue

FTP Sunucusundan dizin listelemeye devam

### <a name="prototype"></a>Prototype

```C
UINT nx_ftp_client_directory_listing_continue(NX_FTP_CLIENT *ftp_client_ptr,
    NX_PACKET **packet_ptr, ULONG wait_option);
```

### <a name="description"></a>Description

Bu hizmet, belirtilen FTP İstemcisi'ne bağlı FTP Sunucusunda belirtilen dizinin içeriğini almaya devam eder. Hemen önüne bir çağrı ***nx_ftp_client_directory_listing_get.*** Başarılı olursa, sağlanan paket işaretçisi bir veya daha fazla dizin girdisi içerir. Bu yordam, durum alınana NX_FTP_END_OF_LISTING çağrılmalı.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_client_ptr** FTP İstemcisi denetim bloğuna işaretçi.
- **packet_ptr** Hedef paket işaretçisine işaretçi. Başarılı olursa paket yükü, cr/lf veya <ile ayrılmış bir veya daha fazla dizin>.
- **wait_option** Hizmetin FTP dizin listesini ne kadar süre bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri** (0x00000001 0xFFFFFFFE) Sayısal bir değer (1-0xFFFFFFFE) seçmek, FTP Sunucusu yanıtı beklerken askıya alınacak zamanlayıcı saat sayısı üst sayısını belirtir.
  - **TX_WAIT_FOREVER** (0xFFFFFFFF) bir FTP sunucusu TX_WAIT_FOREVER yanıt verene kadar çağrı iş parçacığının süresiz olarak askıya alınmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) BAŞARıLı FTP dizin listesi.
- **NX_FTP_END_OF_LISTING** (0xD8) Bu dizinde başka giriş yok.
- **NX_FTP_NOT_CONNECTED** (0xD3) FTP İstemcisi bağlı değil.
- **NX_FTP_EXPECTED_2XX_CODE** (0xDA) 2XX (tamam) yanıtı alam
- NX_PTR_ERROR (0x07) Geçersiz FTP işaretçisi.
- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Continue getting the contents of directory “my_dir” on the FTP Server
    connected to the FTP Client instance “my_client.” */

status = nx_ftp_client_directory_listing_continue(&my_client, &my_packet,
    200);

/* If status is NX_SUCCESS, one or more entries of the directory “my_dir”
    can be found in “my_packet”. */
```

## <a name="nx_ftp_client_disconnect"></a>nx_ftp_client_disconnect

FTP Sunucusu bağlantısını kesme

### <a name="prototype"></a>Prototype

```C
UINT nx_ftp_client_disconnect(NX_FTP_CLIENT *ftp_client_ptr,
    ULONG wait_option);
```

### <a name="description"></a>Description

Bu hizmet, belirtilen FTP İstemcisi ile önceden kurulmuş bir FTP Sunucusu bağlantısını keser.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_client_ptr** FTP İstemcisi denetim bloğuna işaretçi.
- **wait_option** Hizmetin FTP İstemcisi bağlantısının ne kadar süreyle bağlantısının kesilmesini bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri** (0x00000001 0xFFFFFFFE) Sayısal bir değer (1-0xFFFFFFFE) seçmek, FTP Sunucusu yanıtı beklerken askıya alınacak zamanlayıcı saat sayısı üst sayısını belirtir.
  - **TX_WAIT_FOREVER** (0xFFFFFFFF) bir FTP sunucusu TX_WAIT_FOREVER yanıt verene kadar çağrı iş parçacığının süresiz olarak askıya alınmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) FTP bağlantısı başarılı.
- **NX_FTP_NOT_CONNECTED** (0xD3) FTP İstemcisi bağlı değil.
- **NX_FTP_EXPECTED_2XX_CODE** (0xDA) 2XX (tamam) yanıtı alam
- NX_PTR_ERROR (0x07) Geçersiz FTP işaretçisi.
- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Disconnect “my_client” from the FTP Server. */

status = nx_ftp_client_disconnect(&my_client, 200);

/* If status is NX_SUCCESS, “my_client” has been disconnected. */
```

## <a name="nx_ftp_client_file_close"></a>nx_ftp_client_file_close

İstemci dosyasını kapatma

### <a name="prototype"></a>Prototype

```C
UINT nx_ftp_client_file_close(NX_FTP_CLIENT *ftp_client_ptr,
    ULONG wait_option);
```

### <a name="description"></a>Description

Bu hizmet FTP Sunucusunda daha önce açılmış bir dosyayı kapatır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_client_ptr** FTP İstemcisi denetim bloğuna işaretçi.
- **wait_option** Hizmetin FTP İstemcisi dosyasının kapanması için ne kadar bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri** (0x00000001 0xFFFFFFFE) Sayısal bir değer (1-0xFFFFFFFE) seçmek, FTP Sunucusu yanıtı beklerken askıya alınacak zamanlayıcı saat sayısı üst sayısını belirtir.
  - **TX_WAIT_FOREVER** (0xFFFFFFFF) bir FTP sunucusu TX_WAIT_FOREVER yanıt verene kadar çağrı iş parçacığının süresiz olarak askıya alınmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) FTP dosyası kapatma.
- **NX_FTP_NOT_CONNECTED** (0xD3) FTP İstemcisi bağlı değil.
- **NX_FTP_NOT_OPEN (0xD5)** Dosya açık değil; kapatamaz
- **NX_FTP_EXPECTED_2XX_CODE** (0xDA) 2XX (tamam) yanıtı alam
- NX_PTR_ERROR (0x07) Geçersiz FTP işaretçisi.
- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Close previously opened file of client “my_client” on the FTP Server. */

status = nx_ftp_client_file_close(&my_client, 200);

/* If status is NX_SUCCESS, the file opened previously in the “my_client” FTP
    connection has been closed. */
```

## <a name="nx_ftp_client_file_delete"></a>nx_ftp_client_file_delete

FTP Sunucusundaki dosyayı silme

### <a name="prototype"></a>Prototype

```C
UINT nx_ftp_client_file_delete(NX_FTP_CLIENT *ftp_client_ptr,
    CHAR *file_name, ULONG wait_option);
```

### <a name="description"></a>Description

Bu hizmet, FTP Sunucusunda belirtilen dosyayı siler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_client_ptr** FTP İstemcisi denetim bloğuna işaretçi.
- **file_name** Silinecek dosyanın adı.
- **wait_option** Hizmetin FTP İstemcisi dosya silme için ne kadar süre bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri** (0x00000001 0xFFFFFFFE) Sayısal bir değer (1-0xFFFFFFFE) seçmek, FTP Sunucusu yanıtı beklerken askıya alınacak zamanlayıcı saat sayısı üst sayısını belirtir.
  - **TX_WAIT_FOREVER** (0xFFFFFFFF) bir FTP sunucusu TX_WAIT_FOREVER yanıt verene kadar çağrı iş parçacığının süresiz olarak askıya alınmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) BAŞARıLı FTP dosyası silme.
- **NX_FTP_NOT_CONNECTED** (0xD3) FTP İstemcisi bağlı değil.
- **NX_FTP_EXPECTED_2XX_CODE** (0xDA) 2XX (tamam) yanıtı alam
- NX_PTR_ERROR (0x07) Geçersiz FTP işaretçisi.
- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Delete the file “my_file.txt” on the FTP Server using the previously
    connected client “my_client.” */

status = nx_ftp_client_file_delete(&my_client, “my_file.txt”, 200);

/* If status is NX_SUCCESS, the file “my_file.txt” on the FTP Server is
    deleted. */
```

## <a name="nx_ftp_client_file_open"></a>nx_ftp_client_file_open

FTP Sunucusunda dosyasını açar

### <a name="prototype"></a>Prototype

```C
UINT nx_ftp_client_file_open(NX_FTP_CLIENT *ftp_client_ptr,
    CHAR *file_name, UINT open_type, ULONG wait_option);
```

### <a name="description"></a>Description

Bu hizmet, daha önce belirtilen İstemci örneğine bağlı FTP Sunucusunda belirtilen dosyayı (okuma veya yazma için) açar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_client_ptr** FTP İstemcisi denetim bloğuna işaretçi.
- **file_name** Açılacak dosyanın adı.
- **open_type** NX_FTP_OPEN_FOR_READ  veya **NX_FTP_OPEN_FOR_WRITE.**
- **wait_option** Hizmetin FTP İstemcisi dosyasının açılmasını ne kadar bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri** (0x00000001 0xFFFFFFFE) Sayısal bir değer (1-0xFFFFFFFE) seçmek, FTP Sunucusu yanıtı beklerken askıya alınacak zamanlayıcı saat sayısı üst sayısını belirtir.
  - **TX_WAIT_FOREVER** (0xFFFFFFFF) bir FTP sunucusu TX_WAIT_FOREVER yanıt verene kadar çağrı iş parçacığının süresiz olarak askıya alınmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) FTP dosyası açık.
- **NX_OPTION_ERROR** (0x0A) Geçersiz açık tür.
- **NX_FTP_NOT_CONNECTED** (0xD3) FTP İstemcisi bağlı değil.
- **NX_FTP_NOT_CLOSED** (0xD6) FTP İstemcisi zaten açık.
- **NX_NO_FREE_PORTS** (0x45) Atanma için tcp bağlantı noktası yok
- NX_PTR_ERROR (0x07) Geçersiz FTP işaretçisi.
- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Open the file “my_file.txt” for reading on the FTP Server using the previously
    connected client “my_client.” */

status = nx_ftp_client_file_open(&my_client, “my_file.txt”, NX_FTP_OPEN_FOR_READ,
    200);

/* If status is NX_SUCCESS, the file “my_file.txt” on the FTP Server is
    open for reading. */
```

## <a name="nx_ftp_client_file_read"></a>nx_ftp_client_file_read

Dosyadan okuma

### <a name="prototype"></a>Prototype

```C
UINT nx_ftp_client_file_read(NX_FTP_CLIENT *ftp_client_ptr,
    NX_PACKET **packet_ptr, ULONG wait_option);
```

### <a name="description"></a>Description

Bu hizmet, önceden açılmış bir dosyadan bir paket okur. Durum alınana kadar tekrar tekrar çağrıl NX_FTP_END_OF_FILE gerekir.

Çağıranın bu hizmet için bir paket ayırmay olduğunu unutmayın.  Yalnızca bir paket işaretçisine bir işaretçi sağlamak gerekir. Bu hizmet, bu paket işaretçisini yuva alma kuyruğundan alınan bir pakete işaret etmek için güncelleştirecek.  Başarılı bir durum döndürülürse, bu bir paketin kullanılabilir olduğu anlamına gelir ve paket bittiğinde paketi serbest bırakmak çağıranın sorumluluğundadır.

Sıfır olmayan bir durum (hata durumu veya NX_FTP_END_OF_FILE) döndürülürse, çağıranı paketi serbest bırakmaz. Aksi takdirde, paket işaretçisi NULL olduğunda bir hata oluşturulur.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_client_ptr** FTP İstemcisi denetim bloğuna işaretçi.
- **packet_ptr** Depoilecek veri paketi işaretçisi için hedefin işaretçisi. Başarılı olursa, paketin bir veya hepsi dosyanın içerir.
- **wait_option** Hizmetin FTP İstemcisi dosyasının ne kadar süreyle okunacak şekilde bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri** (0x00000001 0xFFFFFFFE) Sayısal bir değer (1-0xFFFFFFFE) seçmek, FTP Sunucusu yanıtı beklerken askıya alınacak zamanlayıcı saat sayısı üst sayısını belirtir.
  - **TX_WAIT_FOREVER** (0xFFFFFFFF) bir FTP sunucusu TX_WAIT_FOREVER yanıt verene kadar çağrı iş parçacığının süresiz olarak askıya alınmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı FTP dosyası okuma.
- **NX_FTP_NOT_OPEN** (0xD5) FTP İstemcisi açık değil.
- **NX_FTP_END_OF_FILE** (0xD7) Dosya sonu koşulu.
- NX_PTR_ERROR (0x07) Geçersiz FTP işaretçisi.
- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
NX_PACKET   *my_packet;

/* Read a packet of data from the file “my_file.txt” that was previously opened
    from the client “my_client.” */

status = nx_ftp_client_file_read(&my_client, &my_packet, 200);

/* Check status.  */
if (status != NX_SUCCESS)
{
    error_counter++;
}
else
{
    /* Release packet when done with it. */
    nx_packet_release(my_packet);
}

/* If status is NX_SUCCESS, the packet pointer, “my_packet” points to the packet
    that contains the next bytes from the file. If the file is completely
    downloaded, an NX_FTP_END_OF_FILE status is returned (no packet retrieved). */
```

## <a name="nx_ftp_client_file_rename"></a>nx_ftp_client_file_rename

FTP Sunucusundaki dosyayı yeniden adlandırma

### <a name="prototype"></a>Prototype

```C
UINT nx_ftp_client_file_rename(NX_FTP_CLIENT *ftp_ptr, CHAR *filename,
    CHAR *new_filename, ULONG wait_option);
```

### <a name="description"></a>Description

Bu hizmet, FTP Sunucusundaki bir dosyayı yeniden adlandırır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_client_ptr** FTP İstemcisi denetim bloğuna işaretçi.
- **dosya adı** Dosyanın geçerli adı.
- **new_filename** Dosya için yeni ad.
- **wait_option** Hizmetin FTP İstemcisi dosya yeniden adlandırması için ne kadar bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri** (0x00000001 0xFFFFFFFE) Sayısal bir değer (1-0xFFFFFFFE) seçmek, FTP Sunucusu yanıtı beklerken askıya alınacak zamanlayıcı saat sayısı üst sayısını belirtir.
  - **TX_WAIT_FOREVER** (0xFFFFFFFF) bir FTP sunucusu TX_WAIT_FOREVER yanıt verene kadar çağrı iş parçacığının süresiz olarak askıya alınmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı FTP dosyası yeniden adlandırması.
- **NX_FTP_NOT_CONNECTED** (0xD3) FTP İstemcisi bağlı değil.
- **NX_FTP_EXPECTED_3XX_CODE** (0XDD) 3XX (tamam) yanıtı alam
- **NX_FTP_EXPECTED_2XX_CODE** (0xDA) 2XX (tamam) yanıtı alam
- NX_PTR_ERROR (0x07) Geçersiz FTP işaretçisi.
- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Rename file “my_file.txt” to “new_file.txt” on the previously connected
    Client instance “my_client.” */

status = nx_ftp_client_file_rename(&my_client, “my_file.txt”, “new_file.txt”,
    200);

/* If status is NX_SUCCESS, the file has been renamed. */
```

## <a name="nx_ftp_client_file_write"></a>nx_ftp_client_file_write

Dosyaya yazma

### <a name="prototype"></a>Prototype

```C
UINT nx_ftp_client_file_write(NX_FTP_CLIENT *ftp_client_ptr,
    NX_PACKET *packet_ptr, ULONG wait_option);
```

### <a name="description"></a>Description

Bu hizmet, FTP Sunucusunda daha önce açılmış olan dosyaya bir veri paketi yazar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_client_ptr** FTP İstemcisi denetim bloğuna işaretçi.
- **packet_ptr** Yazacak verileri içeren paket işaretçisi.
- **wait_option** Hizmetin FTP İstemcisi dosya yazma için ne kadar süre bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri** (0x00000001 0xFFFFFFFE) Sayısal bir değer (1-0xFFFFFFFE) seçmek, FTP Sunucusu yanıtı beklerken askıya alınacak zamanlayıcı saat sayısı üst sayısını belirtir.
  - **TX_WAIT_FOREVER** (0xFFFFFFFF) bir FTP sunucusu TX_WAIT_FOREVER yanıt verene kadar çağrı iş parçacığının süresiz olarak askıya alınmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı FTP dosyası yazma.
- **NX_FTP_NOT_OPEN** (0xD5) FTP İstemcisi açık değil.
- NX_PTR_ERROR (0x07) Geçersiz FTP işaretçisi.
- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Write the data contained in “my_packet” to the previously opened file
    “my_file.txt”. */

status = nx_ftp_client_file_write(&my_client, my_packet, 200);

/* If status is NX_SUCCESS, the file has been written to. */
```

## <a name="nx_ftp_client_passive_mode_set"></a>nx_ftp_client_passive_mode_set

Pasif aktarım modunu etkinleştirme veya devre dışı bırakma

### <a name="prototype"></a>Prototype

```C
UINT nx_ftp_client_passive_mode_set(NX_FTP_CLIENT *ftp_client_ptr,
    UINT passive_mode_enabled);
```

### <a name="description"></a>Description

Bu hizmet, passive_mode_enabled girişi daha önce oluşturulmuş bir FTP İstemcisi örneğinde NX_TRUE olarak ayarlanırsa, sonraki dosya okuma veya yazma çağrıları (RETR, STOR) veya bir dizin listesini indirme (NLST) aktarım modunda yapılırsa pasif aktarım modunu sağlar. Pasif mod aktarımını devre dışı bırakmak ve etkin aktarım modunun varsayılan davranışına dönmek için bu işlevi passive_mode_enabled olarak ayarlanmış şekilde NX_FALSE.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_client_ptr** FTP İstemcisi denetim bloğuna işaretçi.
- **passive_mode_enabled** Varsayılan olarak NX_TRUE pasif mod etkinleştirilir.<br />Varsayılan olarak NX_FALSE pasif mod devre dışı bırakılır.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı pasif mod kümesi.
- NX_PTR_ERROR (0x07) Geçersiz FTP işaretçisi.
- NX_INVALID_PARAMETERS (0x4D) İşaretçi olmayan giriş geçersiz

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Enable the FTP Client to exchange data with the FTP server in passive mode. */

status = nx_ftp_client_passive_mode_set(&my_client, NX_TRUE);

/* If status is NX_SUCCESS, the FTP client is in passive transfer mode. */
```

## <a name="nx_ftp_server_create"></a>nx_ftp_server_create

FTP Sunucusu oluşturma

### <a name="prototype"></a>Prototype

```C
UINT nx_ftp_server_create(NX_FTP_SERVER *ftp_server_ptr,
    CHAR *ftp_server_name, NX_IP *ip_ptr,
    FX_MEDIA *media_ptr, VOID *stack_ptr, ULONG stack_size,
    NX_PACKET_POOL *pool_ptr,
    UINT (*ftp_login)(struct NX_FTP_SERVER_STRUCT *ftp_server_ptr,
        ULONG client_ip_address,
        UINT client_port, CHAR *name, CHAR *password,
        CHAR *extra_info),
    UINT (*ftp_logout)(struct NX_FTP_SERVER_STRUCT *ftp_server_ptr,
        ULONG client_ip_address, UINT client_port,
         CHAR *name, CHAR *password, CHAR *extra_info));
```

### <a name="description"></a>Description

Bu hizmet, belirtilen ve daha önce oluşturulan NetX IP örneğinde bir FTP Sunucusu örneği oluşturur. FTP Sunucusunun çalışmaya başlaması için ftp sunucusunun ***nx_ftp_server_start*** çağrısıyla başlaması gerektiğini unutmayın.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_server_ptr** FTP Sunucusu denetim bloğu işaretçisi.
- **ftp_server_name** FTP Sunucusunun adı.
- **ip_ptr** İlişkili NetX IP örneğinin işaretçisi. Bir IP örneği için yalnızca bir FTP Sunucusu olduğunu unutmayın.
- **media_ptr** İlişkili FileX medya örneğinin işaretçisi.
- **stack_ptr** İç FTP sunucusu iş parçacığının yığın alanı için bellek işaretçisi.
- **stack_size** *Stack_ptr* tarafından belirtilen yığın alanının boyutu.
- **pool_ptr** Varsayılan NetX paket havuzuna yönelik işaretçi. Notdaki paketlerin yük boyutu, en büyük dosya adına/yola uyum sağlayacak kadar büyük olmalıdır.
- **ftp_login** Uygulamanın oturum açma işlevine yönelik işlev işaretçisi. Bu işleve, bir bağlantı isteyen Istemciden Kullanıcı adı ve parola ve ULONG veri türündeki Istemci adresi verilir. Bu geçerliyse, uygulamanın oturum açma işlevi NX_SUCCESS döndürmelidir.
- **ftp_logout** Uygulamanın oturum kapatma işlevine yönelik işlev işaretçisi. Bu işleve, bir bağlantı kesilmesi isteyen Istemciden Kullanıcı adı ve parola ve ULONG veri türündeki Istemci adresi verilir. Bu geçerliyse, uygulamanın oturum açma işlevi NX_SUCCESS döndürmelidir.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı FTP sunucusu oluşturma.
- NX_PTR_ERROR (0x07) geçersiz FTP işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma ve Iş parçacıkları

### <a name="example"></a>Örnek

```C
/* Create the FTP Server “my_server” on the IP instance “ip_0” using the
    “ram_disk” media. */

status = nx_ftp_server_create(&my_server, “My Server Name”, &ip_0, &ram_disk,
    stack_ptr, stack_size, &pool_0,
    my_login, my_logout);

/* If status is NX_SUCCESS, the FTP Server has been created. */
```

## <a name="nxd_ftp_server_create"></a>nxd_ftp_server_create

IPv4 ve IPv6 desteğiyle FTP sunucusu oluşturma

### <a name="prototype"></a>Prototype

```C
UINT nxd_ftp_server_create(NX_FTP_SERVER *ftp_server_ptr,
    CHAR *ftp_server_name, NX_IP *ip_ptr,
    FX_MEDIA *media_ptr, VOID *stack_ptr, ULONG stack_size,
    NX_PACKET_POOL *pool_ptr,
    UINT (*ftp_login_duo)(struct NX_FTP_SERVER_STRUCT *ftp_server_ptr,
        NXD_ADDRESS *client_ip_address, UINT client_port, CHAR *name,
        CHAR *password, CHAR *extra_info),
    UINT (*ftp_logout_duo)(struct NX_FTP_SERVER_STRUCT *ftp_server_ptr,
        NXD_ADDRESS *client_ip_address, UINT client_port, CHAR *name,
        CHAR *password, CHAR *extra_info));
```

### <a name="description"></a>Description

Bu hizmet, belirtilen ve daha önce oluşturulmuş NetX IP örneğinde bir FTP sunucu örneği oluşturur. Sunucu oluşturulduktan sonra işlemin başlaması için FTP sunucusunun hala ***nx_ftp_server_start*** çağrısıyla başlatılması gerekir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_server_ptr** FTP sunucu denetim bloğu işaretçisi.
- **ftp_server_name** FTP sunucusunun adı.
- **ip_ptr** İlişkili NetX IP örneğine yönelik işaretçi. Bir IP örneği için yalnızca bir FTP sunucusu olabileceğini göz önünde bulabilirsiniz.
- **media_ptr** İlişkili FileX medya örneğine yönelik işaretçi.
- **stack_ptr** İç FTP sunucusu iş parçacığının yığın alanı için bellek işaretçisi.
- **stack_size** *Stack_ptr* tarafından belirtilen yığın alanının boyutu.
- **pool_ptr** Varsayılan NetX paket havuzuna yönelik işaretçi. Notdaki paketlerin yük boyutu, en büyük dosya adına/yola uyum sağlayacak kadar büyük olmalıdır.
- **ftp_login_duo** Uygulamanın oturum açma işlevine yönelik işlev işaretçisi. Bu işleve, bir bağlantı isteyen Istemciden Kullanıcı adı ve parola ve NXD_ADDRESS veri türünde Istemci adresine yönelik bir işaretçi verilir. Bu geçerliyse, uygulamanın oturum açma işlevi NX_SUCCESS döndürmelidir.
- **ftp_logout_duo** Uygulamanın oturum kapatma işlevine yönelik işlev işaretçisi. Bu işleve, bir bağlantı kesilmesi isteyen Istemciden Kullanıcı adı ve parola ve NXD_ADDRESS veri türünde Istemci adresine yönelik bir işaretçi sağlanır. Bu geçerliyse, uygulamanın oturum açma işlevi NX_SUCCESS döndürmelidir.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı FTP sunucusu oluşturma.
- NX_PTR_ERROR (0x07) geçersiz FTP işaretçisi.
- NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

Başlatma ve Iş parçacıkları

### <a name="example"></a>Örnek

```C
/* Create the FTP Server “my_server” on the IP instance “ip_0” using the
    “ram_disk” media. */

status = nxd_ftp_server_create(&my_server, “My Server Name”, &ip_0, &ram_disk,
    stack_ptr, stack_size, &pool_0,
    my_duo_login, my_duo_logout);

/* If status is NX_SUCCESS, the FTP Server has been created. */
```

## <a name="nx_ftp_server_delete"></a>nx_ftp_server_delete

FTP sunucusunu Sil

### <a name="prototype"></a>Prototype

```C
UINT nx_ftp_server_delete(NX_FTP_SERVER *ftp_server_ptr);
```

### <a name="description"></a>Description

Bu hizmet, daha önce oluşturulmuş bir FTP sunucusu örneğini siler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_server_ptr** FTP sunucu denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) FTP sunucusu başarıyla silindi.
- NX_PTR_ERROR (0x07) geçersiz FTP işaretçisi.
- NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Delete the FTP Server “my_server”. */

status = nx_ftp_server_delete(&my_server);

/* If status is NX_SUCCESS, the FTP Server has been deleted. */
```

## <a name="nx_ftp_server_start"></a>nx_ftp_server_start

FTP sunucusunu Başlat

### <a name="prototype"></a>Prototype

```C
UINT nx_ftp_server_start(NX_FTP_SERVER *ftp_server_ptr);
```

### <a name="description"></a>Description

Bu hizmet daha önce oluşturulmuş bir FTP sunucusu örneğini başlatır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_server_ptr** FTP sunucu denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) FTP sunucusu başarıyla başlatıldı.
- NX_PTR_ERROR (0x07) geçersiz FTP işaretçisi.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Start the FTP Server “my_server”. */

status = nx_ftp_server_start(&my_server);

/* If status is NX_SUCCESS, the FTP Server has been started. */
```

## <a name="nx_ftp_server_stop"></a>nx_ftp_server_stop

FTP sunucusunu durdur

### <a name="prototype"></a>Prototype

```C
UINT nx_ftp_server_stop(NX_FTP_SERVER *ftp_server_ptr);
```

### <a name="description"></a>Description

Bu hizmet daha önce oluşturulmuş ve başlatılmış bir FTP sunucu örneğini durduruyor.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_server_ptr** FTP sunucu denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı FTP sunucusu durdu.
- NX_PTR_ERROR (0x07) geçersiz FTP işaretçisi.
- NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Stop the FTP Server “my_server”. */

status = nx_ftp_server_stop(&my_server);

/* If status is NX_SUCCESS, the FTP Server has been stopped. */
```
