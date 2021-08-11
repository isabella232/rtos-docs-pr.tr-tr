---
title: Bölüm 3 - NetX FTP Azure RTOS hizmetlerinin açıklaması
description: Bu bölümde, Tüm NetX FTP Azure RTOS (aşağıda listelenmiştir) alfabetik sırada bir açıklama yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 1aec01088236dcae359c0273a0206c10ea09201eb486478ebd678529413badae
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116799464"
---
# <a name="chapter-3---description-of-azure-rtos-netx-ftp-services"></a>Bölüm 3 - NetX FTP Azure RTOS hizmetlerinin açıklaması

Bu bölümde, Tüm NetX FTP Azure RTOS (aşağıda listelenmiştir) alfabetik sırada bir açıklama yer almaktadır.

Aşağıdaki API açıklamalarında yer alan "Dönüş Değerleri" bölümünde, **KALıN**  olmayan değerler tamamen devre dışı bırakılırken, BOLD NX_DISABLE_ERROR_CHECKING API hata denetimlerini devre dışı bırakmak için kullanılan tanımdan etkilenmez.

- **nx_ftp_client_connect:** *Bağlan FTP Sunucusuna yükleme*
- **nx_ftp_client_create:** FTP *İstemcisi örneği oluşturma*
- **nx_ftp_client_delete:** *FTP İstemcisi örneğini silme*
- **nx_ftp_client_directory_create:** *Sunucu'da dizin oluşturma*
- **nx_ftp_client_directory_default_set:** *Sunucu'da varsayılan dizini ayarlayın*
- **nx_ftp_client_directory_delete:** *Sunucu'da bir dizini silme*
- **nx_ftp_client_directory_listing_get:** *Sunucudan dizin listesini al*
- **nx_ftp_client_directory_listing_continue:** *Sunucudan dizin listelemeye devam*
- **nx_ftp_client_disconnect:** *FTP Sunucusu bağlantısını kesme*
- **nx_ftp_client_file_close:** İstemci *dosyasını kapatma*
- **nx_ftp_client_file_delete:** *Sunucu'da dosya silme*
- **nx_ftp_client_file_open:** *İstemci dosyasını açın*
- **nx_ftp_client_file_read:** *Dosyadan okuma*
- **nx_ftp_client_file_rename:** *Sunucu'da dosyayı yeniden adlandır*
- **nx_ftp_client_file_write:** *Dosyaya yazma*
- **nx_ftp_server_create:** FTP *Sunucusu Oluşturma*
- **nx_ftp_server_delete:** FTP *Sunucusunu Silme*
- **nx_ftp_server_start:** FTP *Sunucusunu Başlat*
- **nx_ftp_server_stop:** FTP *Sunucusunu Durdurma*

## <a name="nx_ftp_client_connect"></a>nx_ftp_client_connect

Bağlan FTP Sunucusuna yükleme

### <a name="prototype"></a>Prototype

```c
UINT nx_ftp_client_connect(NX_FTP_CLIENT *ftp_client_ptr,
        ULONG server_ip, CHAR *username, CHAR *password,
        ULONG wait_option);
```

### <a name="description"></a>Description

Bu hizmet, önceden oluşturulmuş FTP İstemcisi örneğini verilen IP adresi üzerinden FTP Sunucusuna bağlar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_client_ptr:** FTP İstemcisi denetim bloğuna işaretçi.
- **server_ip:** FTP Sunucusunun IP adresi.
- **kullanıcı adı:** Kimlik doğrulaması için istemci kullanıcı adı.
- **parola:** Kimlik doğrulaması için istemci parolası.
- **wait_option:** Hizmetin FTP İstemcisi bağlantısını ne kadar süre bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri:**(0x00000001 aracılığıyla 0xFFFFFFFE)
  - **TX_WAIT_FOREVER:**(0xFFFFFFFF) TX_WAIT_FOREVER bir FTP Sunucusu itene yanıt verene kadar çağrı iş parçacığının süresiz olarak askıya alınmasına neden olur. Sayısal bir değer (1-0xFFFFFFFE) seçmek, FTP Sunucusu yanıtı beklerken askıya alınan süreölçer sayısı üst sayısını belirtir.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:**(0x00) Başarılı FTP bağlantısı.
- **NX_TFTP_EXPECTED_22X_CODE:**(0xDB) 22X (tamam) yanıtı alam
- **NX_FTP_EXPECTED_23X_CODE:**(0xDC) 23X (tamam) yanıtı alam
- **NX_FTP_EXPECTED_33X_CODE:**(0xDE) 33X (tamam) yanıtı alam
- **NX_FTP_NOT_DISCONNECTED:**(0xD4) İstemci zaten bağlı.
- NX_PTR_ERROR: (0x07) Geçersiz işaretçi inout.
- NX_CALLER_ERROR: (0x11) Bu hizmetin çağıranı geçersiz.
- NX_IP_ADDRESS_ERROR: (0x21) Geçersiz IP adresi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Connect the FTP Client instance "my_client" to the FTP Server at
    IP address 1.2.3.4. */
status = nx_ftp_client_connect(&my_client, IP_ADDRESS(1,2,3,4), NULL, NULL, 100);

/* If status is NX_SUCCESS an FTP Client instance was successfully  
connected to the FTP Server. */
```

## <a name="nx_ftp_client_create"></a>nx_ftp_client_create

FTP İstemcisi örneği oluşturma

### <a name="prototype"></a>Prototype

```c
UINT nx_ftp_client_create(NX_FTP_CLIENT *ftp_client_ptr,
    CHAR *ftp_client_name, NX_IP *ip_ptr, ULONG window_size,
    NX_PACKET_POOL *pool_ptr);
```

### <a name="description"></a>Description

Bu hizmet bir FTP İstemcisi örneği oluşturur.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_client_ptr:** FTP İstemcisi denetim bloğuna işaretçi.
- **ftp_client_name:** FTP İstemcisi adı.
- **ip_ptr:** Daha önce oluşturulan IP örneğinin işaretçisi.
- **window_size:** Bu FTP İstemcisi'nin TCP yuvası için tanıtılan pencere boyutu.
- **pool_ptr:** Bu FTP İstemcisi için varsayılan paket havuzunun işaretçisi. Minimum paket yükünün tam yolu ve dosya veya dizin adını tutacak kadar büyük olması gerektiğini unutmayın.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:**(0x00) Başarılı FTP İstemcisi oluşturma.
- NX_PTR_ERROR: (0x16) Geçersiz FTP, IP işaretçisi veya paket havuzu işaretçisi. parola işaretçisi.

### <a name="allowed-from"></a>İzin Verilen

Başlatma ve İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Create the FTP Client instance "my_client." */
status = nx_ftp_client_create(&my_client, "My Client", &client_ip,
                                2000, &client_pool);

/* If status is NX_SUCCESS the FTP Client instance was successfully  
created. */
```

## <a name="nx_ftp_client_delete"></a>nx_ftp_client_delete

FTP İstemcisi örneğini silme

### <a name="prototype"></a>Prototype

```c
UINT nx_ftp_client_delete(NX_FTP_CLIENT *ftp_client_ptr);
```

### <a name="description"></a>Description

Bu hizmet bir FTP İstemcisi örneğini siler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_client_ptr:** FTP İstemcisi denetim bloğuna işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:**(0x00) Başarılı FTP İstemcisi silme.
- **NX_FTP_NOT_DISCONNECTED:**(0xD4) FTP İstemcisi silme hatası.
- NX_PTR_ERROR: (0x16) Geçersiz FTP işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Delete the FTP Client instance "my_client." */
status = nx_ftp_client_delete(&my_client);

/* If status is NX_SUCCESS the FTP Client instance was successfully  
    deleted. */
```

## <a name="nx_ftp_client_directory_create"></a>nx_ftp_client_directory_create

FTP Sunucusunda dizin oluşturma

### <a name="prototype"></a>Prototype

```c
UINT nx_ftp_client_directory_create(NX_FTP_CLIENT *ftp_client_ptr,
                        CHAR *directory_name, ULONG wait_option);
```

### <a name="description"></a>Description

Bu hizmet, belirtilen FTP İstemcisi'ne bağlı FTP Sunucusunda belirtilen dizini oluşturur.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_client_ptr:** FTP İstemcisi denetim bloğuna işaretçi.
- **directory_name:** Oluşturul dizinin adı.
- **wait_option:** Hizmetin FTP dizininin oluşturması için ne kadar bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri:**(0x00000001 aracılığıyla 0xFFFFFFFE)
  - **TX_WAIT_FOREVER:**(0xFFFFFFFF) TX_WAIT_FOREVER bir FTP Sunucusu itene yanıt verene kadar çağrı iş parçacığının süresiz olarak askıya alınmasına neden olur. Sayısal bir değer (1-0xFFFFFFFE) seçmek, FTP Sunucusu yanıtı beklerken askıya alınan süreölçer sayısı üst sayısını belirtir.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:**(0x00) Başarılı FTP dizini oluşturma.
- **NX_FTP_NOT_CONNECTED:**(0xD3) FTP İstemcisi bağlı değil.
- **NX_FTP_EXPECTED_2XX_CODE:**(0xDA) 2XX (tamam) yanıtı alam 
- NX_PTR_ERROR: (0x07) Geçersiz FTP işaretçisi. 
- NX_CALLER_ERROR: (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Create the directory "my_dir" on the FTP Server connected to
    the FTP Client instance "my_client." */
status = nx_ftp_client_directory_create(&my_client, "my_dir", 200);

/* If status is NX_SUCCESS the directory "my_dir" was successfully  
    created. */
```

## <a name="nx_ftp_client_directory_default_set"></a>nx_ftp_client_directory_default_set

FTP Sunucusunda varsayılan dizini ayarlama

### <a name="prototype"></a>Prototype

```c
UINT nx_ftp_client_directory_default_set(NX_FTP_CLIENT *ftp_client_ptr,
                                CHAR *directory_path, ULONG wait_option);
```

### <a name="description"></a>Description

Bu hizmet, belirtilen FTP İstemcisi'ne bağlı FTP Sunucusundaki varsayılan dizini ayarlar. Bu varsayılan dizin yalnızca bu istemcinin bağlantısı için geçerlidir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_client_ptr:** FTP İstemcisi denetim bloğuna işaretçi.
- **directory_path:** Ayar için dizin yolunun adı.
- **wait_option:** Hizmetin FTP varsayılan dizin kümesi için ne kadar bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri:**(0x00000001 aracılığıyla 0xFFFFFFFE)
  - **TX_WAIT_FOREVER:**(0xFFFFFFFF) TX_WAIT_FOREVER bir FTP Sunucusu itene yanıt verene kadar çağrı iş parçacığının süresiz olarak askıya alınmasına neden olur. Sayısal bir değer (1-0xFFFFFFFE) seçmek, FTP Sunucusu yanıtı beklerken askıya alınan süreölçer sayısı üst sayısını belirtir.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:**(0x00) Başarılı FTP varsayılan kümesi.
- **NX_FTP_NOT_CONNECTED:**(0xD3) FTP İstemcisi bağlı değil.
- **NX_FTP_EXPECTED_2XX_CODE:**(0xDA) 2XX (tamam) yanıtı alam 
- NX_PTR_ERROR: (0x07) Geçersiz FTP işaretçisi. 
- NX_CALLER_ERROR: (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Set the default directory to "my_dir" on the FTP Server connected to
    the FTP Client instance "my_client." */
status = nx_ftp_client_directory_default_set(&my_client, "my_dir", 200);

/* If status is NX_SUCCESS the directory "my_dir" is the default directory. */
```

## <a name="nx_ftp_client_directory_delete"></a>nx_ftp_client_directory_delete

FTP Sunucusunda dizini silme

### <a name="prototype"></a>Prototype

```c
UINT nx_ftp_client_directory_delete(NX_FTP_CLIENT *ftp_client_ptr,
                        CHAR *directory_name, ULONG wait_option);
```

### <a name="description"></a>Description

Bu hizmet, belirtilen FTP İstemcisi'ne bağlı FTP Sunucusunda belirtilen dizini siler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_client_ptr:** FTP İstemcisi denetim bloğuna işaretçi.
- **directory_name:** Silinecek dizinin adı.
- **wait_option:** Hizmetin FTP dizini silme için ne kadar süre bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri:**(0x00000001 aracılığıyla 0xFFFFFFFE)
  - **TX_WAIT_FOREVER:**(0xFFFFFFFF) TX_WAIT_FOREVER bir FTP Sunucusu itene yanıt verene kadar çağrı iş parçacığının süresiz olarak askıya alınmasına neden olur. Sayısal bir değer (1-0xFFFFFFFE) seçmek, FTP Sunucusu yanıtı beklerken askıya alınan süreölçer sayısı üst sayısını belirtir.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:**(0x00) Başarılı FTP dizini silme.
- **NX_FTP_NOT_CONNECTED:**(0xD3) FTP İstemcisi bağlı değil.
- **NX_FTP_EXPECTED_2XX_CODE:**(0xDA) 2XX (tamam) yanıtı alam 
- NX_PTR_ERROR: (0x07) Geçersiz FTP işaretçisi. 
- NX_CALLER_ERROR: (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Delete directory "my_dir" on the FTP Server connected to
    the FTP Client instance "my_client." */
status = nx_ftp_client_directory_delete(&my_client, "my_dir", 200);

/* If status is NX_SUCCESS the directory "my_dir" is deleted. */
```

## <a name="nx_ftp_client_directory_listing_get"></a>nx_ftp_client_directory_listing_get

FTP Sunucusundan dizin listelemesi al

### <a name="prototype"></a>Prototype

```c
UINT nx_ftp_client_directory_listing_get(NX_FTP_CLIENT *ftp_client_ptr,
                            CHAR *directory_name, NX_PACKET **packet_ptr,
                            ULONG wait_option);
```

### <a name="description"></a>Description

Bu hizmet, belirtilen FTP İstemcisi'ne bağlı FTP Sunucusunda belirtilen dizinin içeriğini alır. Sağlanan paket işaretçisi bir veya daha fazla dizin girdisi içerir. Her giriş bir &lt; cr/lf\combination ile ayrılır. Dizin ***nx_ftp_client_directory_listing_continue*** tamamlamak için : çağrısı gerekir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_client_ptr:** FTP İstemcisi denetim bloğuna işaretçi.
- **directory_name:** İçeriğini almak için dizin adı.
- **packet_ptr:** Hedef paket işaretçisine işaretçi. Başarılı olursa, paket yükü bir veya daha fazla dizin girdisi içerir.
- **wait_option:** Hizmetin FTP dizin listesini ne kadar süre bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri:**(0x00000001 aracılığıyla 0xFFFFFFFE)
  - **TX_WAIT_FOREVER:**(0xFFFFFFFF) TX_WAIT_FOREVER bir FTP Sunucusu itene yanıt verene kadar çağrı iş parçacığının süresiz olarak askıya alınmasına neden olur. Sayısal bir değer (1-0xFFFFFFFE) seçmek, FTP Sunucusu yanıtı beklerken askıya alınan süreölçer sayısı üst sayısını belirtir.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:**(0x00) Başarılı FTP dizin listesi.
- **NX_FTP_NOT_CONNECTED:**(0xD3) FTP İstemcisi bağlı değil.
- **NX_NOT_ENABLED:**(0x14) Hizmeti (IPv6) etkin değil
- **NX_FTP_EXPECTED_1XX_CODE:**(0xD9) 1XX (tamam) yanıtı alam
- **NX_FTP_EXPECTED_2XX_CODE:**(0xDA) 2XX (tamam) yanıtı alam
- NX_PTR_ERROR: (0x07) Geçersiz FTP işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Get the contents of directory "my_dir" on the FTP Server connected to
    the FTP Client instance "my_client." */
status = nx_ftp_client_directory_listing_get(&my_client, "my_dir", &my_packet,
                                            200);

/* If status is NX_SUCCESS, one or more entries of the directory "my_dir"
    can be found in "my_packet". */
```

## <a name="nx_ftp_client_directory_listing_continue"></a>nx_ftp_client_directory_listing_continue

FTP Sunucusundan dizin listelemeye devam

### <a name="prototype"></a>Prototype

```c
UINT nx_ftp_client_directory_listing_continue(NX_FTP_CLIENT
                    *ftp_client_ptr, NX_PACKET **packet_ptr,
                    ULONG wait_option);
```

### <a name="description"></a>Description

Bu hizmet, belirtilen FTP İstemcisi'ne bağlı FTP Sunucusunda belirtilen dizinin içeriğini almaya devam eder. Hemen önüne bir çağrı ***nx_ftp_client_directory_listing_get.*** Başarılı olursa, sağlanan paket işaretçisi bir veya daha fazla dizin girdisi içerir. Bu yordam, durum alınana NX_FTP_END_OF_LISTING çağrılmalı.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_client_ptr:** FTP İstemcisi denetim bloğuna işaretçi.
- **packet_ptr:** Hedef paket işaretçisine işaretçi. Başarılı olursa, paket yükü cr/lf ile ayrılmış bir veya daha fazla dizin &lt; girdisi &gt; içerir.
- **wait_option:** Hizmetin FTP dizin listesini ne kadar süre bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri:**(0x00000001 aracılığıyla 0xFFFFFFFE)
  - **TX_WAIT_FOREVER:**(0xFFFFFFFF) TX_WAIT_FOREVER bir FTP Sunucusu itene yanıt verene kadar çağrı iş parçacığının süresiz olarak askıya alınmasına neden olur. Sayısal bir değer (1-0xFFFFFFFE) seçmek, FTP Sunucusu yanıtı beklerken askıya alınan süreölçer sayısı üst sayısını belirtir.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:**(0x00) Başarılı FTP dizin listesi.
- **NX_FTP_END_OF_LISTING**: (0xd8) bu dizinde daha fazla girdi yok.
- **NX_FTP_NOT_CONNECTED**: (0xd3) FTP istemcisi bağlı değil.
- **NX_FTP_EXPECTED_2XX_CODE** (0xDA), 2xx (Tamam) yanıtını almadı
- NX_PTR_ERROR: (0x07) geçersiz FTP işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Continue getting the contents of directory "my_dir" on the FTP Server
    connected to the FTP Client instance "my_client." */
status = nx_ftp_client_directory_listing_continue(&my_client, &my_packet,
                                                200);

/* If status is NX_SUCCESS, one or more entries of the directory "my_dir"
    can be found in "my_packet". */
```

## <a name="nx_ftp_client_disconnect"></a>nx_ftp_client_disconnect

FTP sunucusu bağlantısını kes

### <a name="prototype"></a>Prototype

```c
UINT nx_ftp_client_disconnect(NX_FTP_CLIENT *ftp_client_ptr,
                            ULONG wait_option);
```

### <a name="description"></a>Description

Bu hizmet, belirtilen FTP Istemcisiyle önceden oluşturulmuş bir FTP sunucusu bağlantısını keser.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_client_ptr**: FTP istemci denetim bloğu işaretçisi.
- **wait_option**: hizmetin FTP istemcisinin bağlantısını kesmek için bekleyeceği süreyi tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri**: (0x00000001 üzerinden 0xfffffffe)
  - **TX_WAIT_FOREVER**: (0xffffffff) TX_WAIT_FOREVER seçilmesi çağıran iş PARÇACıĞıNıN bir FTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur. Sayısal bir değer (1-0xFFFFFFFE) seçilmesi, FTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) FTP bağlantısı başarıyla açıldı.
- **NX_FTP_NOT_CONNECTED**: (0xd3) FTP istemcisi bağlı değil.
- **NX_FTP_EXPECTED_2XX_CODE**: (0xDA), 2xx (Tamam) yanıtını almadı
- NX_PTR_ERROR: (0x07) geçersiz FTP işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Disconnect "my_client" from the FTP Server. */
status = nx_ftp_client_disconnect(&my_client, 200);

/* If status is NX_SUCCESS, "my_client" has been disconnected. */
```

## <a name="nx_ftp_client_file_close"></a>nx_ftp_client_file_close

Istemci dosyasını kapat

### <a name="prototype"></a>Prototype

```c
UINT nx_ftp_client_file_close(NX_FTP_CLIENT *ftp_client_ptr,
                            ULONG wait_option);
```

### <a name="description"></a>Description

Bu hizmet, FTP sunucusunda daha önce açılmış bir dosyayı kapatır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_client_ptr**: FTP istemci denetim bloğu işaretçisi.
- **wait_option**: hizmetin FTP istemci dosyası kapanması için bekleyeceği süreyi tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri**: (0x00000001 üzerinden 0xfffffffe)
  - **TX_WAIT_FOREVER**: (0xffffffff) TX_WAIT_FOREVER seçilmesi çağıran iş PARÇACıĞıNıN bir FTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur. Sayısal bir değer (1-0xFFFFFFFE) seçilmesi, FTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı FTP dosyası kapatma.
- **NX_FTP_NOT_CONNECTED**: (0xd3) FTP istemcisi bağlı değil.
- **NX_FTP_NOT_OPEN (0xD5)**: dosya açık değil; kapatılamıyor
- **NX_FTP_EXPECTED_2XX_CODE**: (0xDA), 2xx (Tamam) yanıtını almadı
- NX_PTR_ERROR: (0x07) geçersiz FTP işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Close previously opened file of client "my_client" on the FTP Server. */
status = nx_ftp_client_file_close(&my_client, 200);

/* If status is NX_SUCCESS, the file opened previously in the "my_client" FTP
    connection has been closed. */
```

## <a name="nx_ftp_client_file_delete"></a>nx_ftp_client_file_delete

FTP sunucusundaki dosyayı Sil

### <a name="prototype"></a>Prototype

```c
UINT nx_ftp_client_file_delete(NX_FTP_CLIENT *ftp_client_ptr,
                        CHAR *file_name, ULONG wait_option);
```

### <a name="description"></a>Description

Bu hizmet, FTP sunucusunda belirtilen dosyayı siler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_client_ptr**: FTP istemci denetim bloğu işaretçisi.
- **file_name**: Silinecek dosyanın adı.
- **wait_option**: hizmetin FTP istemci dosyası silme işleminin ne kadar bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri**: (0x00000001 üzerinden 0xfffffffe)
  - **TX_WAIT_FOREVER**: (0xffffffff) TX_WAIT_FOREVER seçilmesi çağıran iş PARÇACıĞıNıN bir FTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur. Sayısal bir değer (1-0xFFFFFFFE) seçilmesi, FTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) FTP dosyası başarıyla silindi.
- **NX_FTP_NOT_CONNECTED**: (0xd3) FTP istemcisi bağlı değil.
- **NX_FTP_EXPECTED_2XX_CODE**: (0xDA), 2xx (Tamam) yanıtını almadı
- NX_PTR_ERROR: (0x07) geçersiz FTP işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Delete the file "my_file.txt" on the FTP Server using the previously
    connected client "my_client." */
status = nx_ftp_client_file_delete(&my_client, "my_file.txt", 200);

/* If status is NX_SUCCESS, the file "my_file.txt" on the FTP Server is
    deleted. */
```

## <a name="nx_ftp_client_file_open"></a>nx_ftp_client_file_open

Dosyayı FTP sunucusunda açar

### <a name="prototype"></a>Prototype

```c
UINT nx_ftp_client_file_open(NX_FTP_CLIENT *ftp_client_ptr,
        CHAR *file_name, UINT open_type, ULONG wait_option);
```

### <a name="description"></a>Description

Bu hizmet, belirtilen Istemci örneğine daha önce bağlı FTP sunucusunda belirtilen dosyayı (okuma veya yazma için) açar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_client_ptr**: FTP istemci denetim bloğu işaretçisi.
- **file_name**: açılacak dosyanın adı.
- **open_type**: **NX_FTP_OPEN_FOR_READ** veya **NX_FTP_OPEN_FOR_WRITE**.
- **wait_option**: hizmetin FTP istemci dosyası açılmasını ne kadar süreyle bekleyecektir tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri**: (0x00000001 üzerinden 0xfffffffe)
  - **TX_WAIT_FOREVER**: (0xffffffff) TX_WAIT_FOREVER seçilmesi çağıran iş PARÇACıĞıNıN bir FTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur. Sayısal bir değer (1-0xFFFFFFFE) seçilmesi, FTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) FTP dosyası başarıyla açıldı.
- **NX_OPTION_ERROR**: (0X0a) geçersiz açık tür.
- **NX_FTP_NOT_CONNECTED**: (0xd3) FTP istemcisi bağlı değil.
- **NX_FTP_NOT_CLOSED**: (0xd6) FTP istemcisi zaten açık.
- **NX_NO_FREE_PORTS**: (0x45) atanacak TCP bağlantı noktası yok
- NX_PTR_ERROR: (0x07) geçersiz FTP işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Open the file "my_file.txt" for reading on the FTP Server using the previously
    connected client "my_client." */
status = nx_ftp_client_file_open(&my_client, "my_file.txt", NX_FTP_OPEN_FOR_READ,
                                200);

/* If status is NX_SUCCESS, the file "my_file.txt" on the FTP Server is
    open for reading. */
```

## <a name="nx_ftp_client_file_read"></a>nx_ftp_client_file_read

Dosyadan oku

### <a name="prototype"></a>Prototype

```c
UINT nx_ftp_client_file_read(NX_FTP_CLIENT *ftp_client_ptr,
                NX_PACKET **packet_ptr, ULONG wait_option);
```

### <a name="description"></a>Description

Bu hizmet, önceden açılmış bir dosyadan bir paket okur. Durum alınana kadar tekrar tekrar çağrıl NX_FTP_END_OF_FILE gerekir.

Çağıranın bu hizmet için bir paket ayırmay olduğunu unutmayın.  Yalnızca bir paket işaretçisine bir işaretçi sağlamak gerekir. Bu hizmet, bu paket işaretçisini yuva alma kuyruğundan alınan bir pakete işaret etmek için güncelleştirecek.  Başarılı bir durum döndürülürse, bu bir paketin kullanılabilir olduğu anlamına gelir ve paket bittiğinde paketi serbest bırakmak çağıranın sorumluluğundadır.

Sıfır olmayan bir durum (hata durumu veya NX_FTP_END_OF_FILE) döndürülürse, çağıranı paketi serbest bırakmaz. Aksi takdirde, paket işaretçisi NULL olduğunda bir hata oluşturulur.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_client_ptr:** FTP İstemcisi denetim bloğuna işaretçi.
- **packet_ptr:** Kuyruktan alınan veri paketi işaretçisi için hedefin işaretçisi. Başarılı olursa paket verileri dosyanın bir veya daha hepsini içerir.
- **wait_option:** Hizmetin FTP İstemcisi dosyasının ne kadar süreyle okundu olarak bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri:**(0x00000001 aracılığıyla 0xFFFFFFFE)
  - **TX_WAIT_FOREVER:**(0xFFFFFFFF) TX_WAIT_FOREVER bir FTP Sunucusu itene yanıt verene kadar çağrı iş parçacığının süresiz olarak askıya alınmasına neden olur. Sayısal bir değer (1-0xFFFFFFFE) seçmek, FTP Sunucusu yanıtı beklerken askıya alınan süreölçer sayısı üst sayısını belirtir.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:**(0x00) Başarılı FTP dosyası okuma.
- **NX_FTP_NOT_OPEN:**(0xD5) FTP İstemcisi açık değil.
- **NX_FTP_END_OF_FILE:**(0xD7) Dosya sonu koşulu.
- NX_PTR_ERROR: (0x07) Geçersiz FTP işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
       NX_PACKET   *my_packet;

/* Read a packet of data from the file "my_file.txt" that was previously opened
    from the client "my_client." */

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

/* If status is NX_SUCCESS, the packet pointer, "my_packet" points to the packet
that contains the next bytes from the file. If the file is completely
downloaded, an NX_FTP_END_OF_FILE status is returned (no packet retrieved). */
```

## <a name="nx_ftp_client_file_rename"></a>nx_ftp_client_file_rename

FTP Sunucusundaki dosyayı yeniden adlandırma

### <a name="prototype"></a>Prototype

```c
UINT nx_ftp_client_file_rename(NX_FTP_CLIENT *ftp_ptr, CHAR *filename,
                                CHAR *new_filename, ULONG wait_option);
```

### <a name="description"></a>Description

Bu hizmet, FTP Sunucusundaki bir dosyayı yeniden adlandırır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_client_ptr:** FTP İstemcisi denetim bloğuna işaretçi.
- **filename**: Dosyanın geçerli adı.
- **new_filename:** Dosya için yeni ad.
- **wait_option:** Hizmetin FTP İstemcisi dosya yeniden adlandırması için ne kadar bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri:**(0x00000001 aracılığıyla 0xFFFFFFFE)
  - **TX_WAIT_FOREVER:**(0xFFFFFFFF) TX_WAIT_FOREVER bir FTP Sunucusu itene yanıt verene kadar çağrı iş parçacığının süresiz olarak askıya alınmasına neden olur. Sayısal bir değer (1-0xFFFFFFFE) seçmek, FTP Sunucusu yanıtı beklerken askıya alınan süreölçer sayısı üst sayısını belirtir.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:**(0x00) Başarılı FTP dosyası yeniden adlandırması.
- **NX_FTP_NOT_CONNECTED:**(0xD3) FTP İstemcisi bağlı değil.
- **NX_FTP_EXPECTED_3XX_CODE:**(0XDD) 3XX (tamam) yanıtı alam
- **NX_FTP_EXPECTED_2XX_CODE:**(0xDA) 2XX (tamam) yanıtı alam
- NX_PTR_ERROR: (0x07) Geçersiz FTP işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Rename file "my_file.txt" to "new_file.txt" on the previously connected
    Client instance "my_client." */

status = nx_ftp_client_file_rename(&my_client, "my_file.txt", "new_file.txt",
                                    200);

/* If status is NX_SUCCESS, the file has been renamed. */
```

## <a name="nx_ftp_client_file_write"></a>nx_ftp_client_file_write

Dosyaya yazma

### <a name="prototype"></a>Prototype

```c
UINT nx_ftp_client_file_write(NX_FTP_CLIENT *ftp_client_ptr,
                    NX_PACKET *packet_ptr, ULONG wait_option);
```

### <a name="description"></a>Description

Bu hizmet, FTP Sunucusunda daha önce açılmış olan dosyaya bir veri paketi yazar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_client_ptr:** FTP İstemcisi denetim bloğuna işaretçi.
- **packet_ptr:** Yazacak verileri içeren paket işaretçisi.
- **wait_option:** Hizmetin FTP İstemcisi dosya yazma için ne kadar bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri:**(0x00000001 aracılığıyla 0xFFFFFFFE)
  - **TX_WAIT_FOREVER:**(0xFFFFFFFF) TX_WAIT_FOREVER bir FTP Sunucusu itene yanıt verene kadar çağrı iş parçacığının süresiz olarak askıya alınmasına neden olur. Sayısal bir değer (1-0xFFFFFFFE) seçmek, FTP Sunucusu yanıtı beklerken askıya alınan süreölçer sayısı üst sayısını belirtir.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:**(0x00) Başarılı FTP dosyası yazma.
- **NX_FTP_NOT_OPEN:**(0xD5) FTP İstemcisi açık değil.
- NX_PTR_ERROR: (0x07) Geçersiz FTP işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Write the data contained in "my_packet" to the previously opened file
    "my_file.txt". */

status = nx_ftp_client_file_write(&my_client, my_packet, 200);

/* If status is NX_SUCCESS, the file has been written to. */
```

## <a name="nx_ftp_client_passive_mode_set"></a>nx_ftp_client_passive_mode_set

Pasif aktarım modunu etkinleştirme veya devre dışı bırakma

### <a name="prototype"></a>Prototype

```c
UINT nx_ftp_client_passive_mode_set(NX_FTP_CLIENT *ftp_client_ptr,
                                    UINT passive_mode_enabled);
```

### <a name="description"></a>Description

Bu hizmet, passive_mode_enabled girişi daha önce oluşturulmuş bir FTP İstemcisi örneğinde NX_TRUE olarak ayarlanırsa, sonraki dosya okuma veya yazma çağrıları (RETR, STOR) veya bir dizin listesini indirme (NLST) aktarım modunda yapılırsa pasif aktarım modunu sağlar. Pasif mod aktarımını devre dışı bırakmak ve etkin aktarım modunun varsayılan davranışına dönmek için bu işlevi passive_mode_enabled olarak ayarlanmış şekilde NX_FALSE.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_client_ptr:** FTP İstemcisi denetim bloğuna işaretçi.
- **passive_mode_enabled:**
  - Varsayılan olarak NX_TRUE pasif mod etkinleştirilir.
  - Varsayılan olarak NX_FALSE pasif mod devre dışı bırakılır.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:**(0x00) Başarılı pasif mod kümesi.
- NX_PTR_ERROR: (0x16) Geçersiz FTP işaretçisi.
- NX_INVALID_PARAMETERS: (0x4D) İşaretçi olmayan giriş geçersiz

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Enable the FTP Client to exchange data with the FTP server in passive mode. */

status = nx_ftp_client_passive_mode_set(&my_client, NX_TRUE);

/* If status is NX_SUCCESS, the FTP client is in passive transfer mode. */
```

## <a name="nx_ftp_server_create"></a>nx_ftp_server_create

FTP Sunucusu oluşturma

### <a name="prototype"></a>Prototype

```c
UINT nx_ftp_server_create(NX_FTP_SERVER *ftp_server_ptr,
        CHAR *ftp_server_name, NX_IP *ip_ptr,
        FX_MEDIA *media_ptr, VOID *stack_ptr, ULONG stack_size,
        NX_PACKET_POOL *pool_ptr,
        UINT (*ftp_login)(struct NX_FTP_SERVER_STRUCT
                *ftp_server_ptr, ULONG client_ip_address,
                UINT client_port, CHAR *name, CHAR *password,
                CHAR *extra_info),
        UINT (*ftp_logout)(struct NX_FTP_SERVER_STRUCT
                *ftp_server_ptr, ULONG client_ip_address,
                UINT client_port, CHAR *name, CHAR *password,
                CHAR *extra_info));
```

### <a name="description"></a>Description

Bu hizmet, belirtilen ve daha önce oluşturulan NetX IP örneğinde bir FTP Sunucusu örneği oluşturur. FTP Sunucusunun çalışmaya başlaması için ftp sunucusunun ***nx_ftp_server_start*** çağrısıyla başlaması gerektiğini unutmayın.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_server_ptr:** FTP Sunucusu denetim bloğuna işaretçi.
- **ftp_server_name:** FTP Sunucusunun adı.
- **ip_ptr**: Ilişkili NETX IP örneğine yönelik işaretçi. Bir IP örneği için yalnızca bir FTP sunucusu olabileceğini göz önünde bulabilirsiniz.
- **media_ptr**: Ilişkili FileX medya örneğine yönelik işaretçi.
- **stack_ptr**: Iç FTP sunucusu iş parçacığının yığın alanı için bellek işaretçisi.
- **stack_size**: *stack_ptr* tarafından belirtilen yığın alanının boyutu.
- **pool_ptr**: varsayılan NETX paket havuzuna yönelik işaretçi. Notdaki paketlerin yük boyutu, en büyük dosya adına/yola uyum sağlayacak kadar büyük olmalıdır.
- **ftp_login**: uygulamanın oturum açma işlevine yönelik işlev işaretçisi. Bu işleve bir bağlantı isteyen Istemciden Kullanıcı adı ve parola verilir. Bu geçerliyse, uygulamanın oturum açma işlevi NX_SUCCESS döndürmelidir.
- **ftp_logout**: uygulamanın oturum kapatma işlevine yönelik işlev işaretçisi. Bu işleve, bir bağlantı kesilmesi isteyen Istemciden Kullanıcı adı ve parola verilir. Bu geçerliyse, uygulamanın oturum açma işlevi NX_SUCCESS döndürmelidir.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı FTP sunucusu oluşturma.
- NX_PTR_ERROR: (0x16) geçersiz FTP işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma ve Iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Create the FTP Server "my_server" on the IP instance "ip_0" using the
    "ram_disk" media. */

status = nx_ftp_server_create(&my_server, "My Server Name", &ip_0, &ram_disk,
                                stack_ptr, stack_size, &pool_0,
                                my_login, my_logout);

/* If status is NX_SUCCESS, the FTP Server has been created. */
```

## <a name="nx_ftp_server_delete"></a>nx_ftp_server_delete

FTP sunucusunu Sil

### <a name="prototype"></a>Prototype

```c
UINT nx_ftp_server_delete(NX_FTP_SERVER *ftp_server_ptr);
```

### <a name="description"></a>Description

Bu hizmet, daha önce oluşturulmuş bir FTP sunucusu örneğini siler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_server_ptr**: FTP sunucu denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) FTP sunucusu başarıyla silindi.
- NX_PTR_ERROR: (0x16) geçersiz FTP işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Delete the FTP Server "my_server". */

status = nx_ftp_server_delete(&my_server);

/* If status is NX_SUCCESS, the FTP Server has been deleted. */
```

## <a name="nx_ftp_server_start"></a>nx_ftp_server_start

FTP sunucusunu Başlat

### <a name="prototype"></a>Prototype

```c
UINT nx_ftp_server_start(NX_FTP_SERVER *ftp_server_ptr);
```

### <a name="description"></a>Description

Bu hizmet daha önce oluşturulmuş bir FTP sunucusu örneğini başlatır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_server_ptr**: FTP sunucu denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) FTP sunucusu başarıyla başlatıldı.
- NX_PTR_ERROR: (0x16) geçersiz FTP işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma ve Iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Start the FTP Server "my_server". */

status = nx_ftp_server_start(&my_server);

/* If status is NX_SUCCESS, the FTP Server has been started. */
```

## <a name="nx_ftp_server_stop"></a>nx_ftp_server_stop

FTP sunucusunu durdur

### <a name="prototype"></a>Prototype

```c
UINT nx_ftp_server_stop(NX_FTP_SERVER *ftp_server_ptr);
```

### <a name="description"></a>Description

Bu hizmet daha önce oluşturulmuş ve başlatılmış bir FTP sunucu örneğini durduruyor.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_server_ptr**: FTP sunucu denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) FTP sunucusu başarıyla durdu.
- NX_PTR_ERROR: (0x16) geçersiz FTP işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Stop the FTP Server "my_server". */

status = nx_ftp_server_stop(&my_server);

/* If status is NX_SUCCESS, the FTP Server has been stopped. */
```
