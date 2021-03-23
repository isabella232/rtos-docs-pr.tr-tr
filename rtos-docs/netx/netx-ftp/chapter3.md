---
title: Bölüm 3-Azure RTOS NetX FTP hizmetlerinin açıklaması
description: Bu bölüm, tüm Azure RTOS NetX FTP hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: b05d03c45607c45acf32474cf8e40861532c5fae
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826722"
---
# <a name="chapter-3---description-of-azure-rtos-netx-ftp-services"></a>Bölüm 3-Azure RTOS NetX FTP hizmetlerinin açıklaması

Bu bölüm, tüm Azure RTOS NetX FTP hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.

Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_DISABLE_ERROR_CHECKING** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.

- **nx_ftp_client_connect**: *FTP sunucusuna bağlan*
- **nx_ftp_client_create**: *FTP istemci örneği oluşturma*
- **nx_ftp_client_delete**: *FTP istemci örneğini silme*
- **nx_ftp_client_directory_create**: *sunucuda bir dizin oluşturma*
- **nx_ftp_client_directory_default_set**: *sunucuda varsayılan dizini ayarla*
- **nx_ftp_client_directory_delete**: *sunucuda bir dizini silme*
- **nx_ftp_client_directory_listing_get**: *sunucudan dizin listesini al*
- **nx_ftp_client_directory_listing_continue**: *sunucudan dizin listesine devam et*
- **nx_ftp_client_disconnect**: *FTP sunucusu bağlantısını kes*
- **nx_ftp_client_file_close**: *istemci dosyasını kapat*
- **nx_ftp_client_file_delete**: *sunucudaki dosyayı Sil*
- **nx_ftp_client_file_open**: *istemci dosyasını aç*
- **nx_ftp_client_file_read**: dosyadan *Oku*
- **nx_ftp_client_file_rename**: *sunucudaki dosyayı yeniden adlandır*
- **nx_ftp_client_file_write**: *dosyaya yaz*
- **nx_ftp_server_create**: *FTP sunucusu oluştur*
- **nx_ftp_server_delete**: *FTP sunucusunu Sil*
- **nx_ftp_server_start**: *FTP sunucusunu Başlat*
- **nx_ftp_server_stop**: *FTP sunucusunu durdur*

## <a name="nx_ftp_client_connect"></a>nx_ftp_client_connect

FTP sunucusuna bağlanma

### <a name="prototype"></a>Prototype

```c
UINT nx_ftp_client_connect(NX_FTP_CLIENT *ftp_client_ptr,
        ULONG server_ip, CHAR *username, CHAR *password,
        ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, önceden oluşturulan FTP Istemci örneğini sağlanan IP adresindeki FTP sunucusuna bağlar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_client_ptr**: FTP istemci denetim bloğu işaretçisi.
- **server_ip**: FTP sunucusunun IP adresi.
- **Kullanıcı adı**: kimlik doğrulaması için istemci Kullanıcı adı.
- **parola**: kimlik doğrulaması için istemci parolası.
- **wait_option**: hizmetin FTP istemci bağlantısı için bekleyeceği süreyi tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri**: (0x00000001 üzerinden 0xfffffffe)
  - **TX_WAIT_FOREVER**: (0xffffffff) TX_WAIT_FOREVER seçilmesi çağıran iş PARÇACıĞıNıN bir FTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur. Sayısal bir değer (1-0xFFFFFFFE) seçilmesi, FTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) FTP bağlantısı başarılı oldu.
- **NX_TFTP_EXPECTED_22X_CODE**: (0xDB), 22x (Tamam) yanıtını almadı
- **NX_FTP_EXPECTED_23X_CODE**: (0xDC), 23x (Tamam) yanıtını almadı
- **NX_FTP_EXPECTED_33X_CODE**: (0xDE), bir 33x (Tamam) yanıtı almadı
- **NX_FTP_NOT_DISCONNECTED**: (0xd4) istemci zaten bağlı.
- NX_PTR_ERROR: (0x07) geçersiz işaretçi girişi.
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.
- NX_IP_ADDRESS_ERROR: (0x21) geçersiz IP adresi.

### <a name="allowed-from"></a>İzin verilen

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

FTP Istemci örneği oluşturma

### <a name="prototype"></a>Prototype

```c
UINT nx_ftp_client_create(NX_FTP_CLIENT *ftp_client_ptr,
    CHAR *ftp_client_name, NX_IP *ip_ptr, ULONG window_size,
    NX_PACKET_POOL *pool_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet bir FTP Istemci örneği oluşturur.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_client_ptr**: FTP istemci denetim bloğu işaretçisi.
- **ftp_client_name**: FTP istemcisinin adı.
- **ip_ptr**: daha önce oluşturulan IP örneğine yönelik işaretçi.
- **window_size**: Bu FTP istemcisinin TCP yuvası için tanıtılan pencere boyutu.
- **pool_ptr**: Bu FTP istemcisi için varsayılan paket havuzuna yönelik işaretçi. En düşük paket yükünün, tüm yolu ve dosya ya da dizin adını tutabilecek kadar büyük olması gerektiğini unutmayın.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı FTP istemcisi oluştur.
- NX_PTR_ERROR: (0x16) geçersiz FTP, IP işaretçisi veya paket havuzu işaretçisi. parola işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma ve Iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Create the FTP Client instance "my_client." */
status = nx_ftp_client_create(&my_client, "My Client", &client_ip,
                                2000, &client_pool);

/* If status is NX_SUCCESS the FTP Client instance was successfully  
created. */
```

## <a name="nx_ftp_client_delete"></a>nx_ftp_client_delete

FTP Istemci örneğini silme

### <a name="prototype"></a>Prototype

```c
UINT nx_ftp_client_delete(NX_FTP_CLIENT *ftp_client_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet bir FTP Istemci örneğini siler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_client_ptr**: FTP istemci denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı FTP istemcisi silme.
- **NX_FTP_NOT_DISCONNECTED**: (0xd4) FTP istemcisi silme hatası.
- NX_PTR_ERROR: (0x16) geçersiz FTP işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Delete the FTP Client instance "my_client." */
status = nx_ftp_client_delete(&my_client);

/* If status is NX_SUCCESS the FTP Client instance was successfully  
    deleted. */
```

## <a name="nx_ftp_client_directory_create"></a>nx_ftp_client_directory_create

FTP sunucusunda bir dizin oluşturma

### <a name="prototype"></a>Prototype

```c
UINT nx_ftp_client_directory_create(NX_FTP_CLIENT *ftp_client_ptr,
                        CHAR *directory_name, ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen FTP sunucusuna bağlı FTP sunucusunda belirtilen dizini oluşturur.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_client_ptr**: FTP istemci denetim bloğu işaretçisi.
- **directory_name**: Oluşturulacak dizinin adı.
- **wait_option**: hizmetin FTP dizin oluşturma için bekleyeceği süreyi tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri**: (0x00000001 üzerinden 0xfffffffe)
  - **TX_WAIT_FOREVER**: (0xffffffff) TX_WAIT_FOREVER seçilmesi çağıran iş PARÇACıĞıNıN bir FTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur. Sayısal bir değer (1-0xFFFFFFFE) seçilmesi, FTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı FTP dizin oluşturma.
- **NX_FTP_NOT_CONNECTED**: (0xd3) FTP istemcisi bağlı değil.
- **NX_FTP_EXPECTED_2XX_CODE**: (0xDA), 2xx (Tamam) yanıtını almadı 
- NX_PTR_ERROR: (0x07) geçersiz FTP işaretçisi. 
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

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

FTP sunucusunda varsayılan dizini ayarla

### <a name="prototype"></a>Prototype

```c
UINT nx_ftp_client_directory_default_set(NX_FTP_CLIENT *ftp_client_ptr,
                                CHAR *directory_path, ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen FTP Istemcisine bağlı FTP sunucusunda varsayılan dizini ayarlar. Bu varsayılan dizin yalnızca bu istemcinin bağlantısı için geçerlidir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_client_ptr**: FTP istemci denetim bloğu işaretçisi.
- **directory_path**: ayarlanacak dizin yolunun adı.
- **wait_option**: hizmetin FTP varsayılan dizin kümesi için bekleyeceği süreyi tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri**: (0x00000001 üzerinden 0xfffffffe)
  - **TX_WAIT_FOREVER**: (0xffffffff) TX_WAIT_FOREVER seçilmesi çağıran iş PARÇACıĞıNıN bir FTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur. Sayısal bir değer (1-0xFFFFFFFE) seçilmesi, FTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı FTP varsayılan kümesi.
- **NX_FTP_NOT_CONNECTED**: (0xd3) FTP istemcisi bağlı değil.
- **NX_FTP_EXPECTED_2XX_CODE**: (0xDA), 2xx (Tamam) yanıtını almadı 
- NX_PTR_ERROR: (0x07) geçersiz FTP işaretçisi. 
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Set the default directory to "my_dir" on the FTP Server connected to
    the FTP Client instance "my_client." */
status = nx_ftp_client_directory_default_set(&my_client, "my_dir", 200);

/* If status is NX_SUCCESS the directory "my_dir" is the default directory. */
```

## <a name="nx_ftp_client_directory_delete"></a>nx_ftp_client_directory_delete

FTP sunucusundaki dizini Sil

### <a name="prototype"></a>Prototype

```c
UINT nx_ftp_client_directory_delete(NX_FTP_CLIENT *ftp_client_ptr,
                        CHAR *directory_name, ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen FTP Istemcisine bağlı FTP sunucusunda belirtilen dizini siler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_client_ptr**: FTP istemci denetim bloğu işaretçisi.
- **directory_name**: silinecek dizinin adı.
- **wait_option**: hizmetin FTP dizin silme işleminin ne kadar bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri**: (0x00000001 üzerinden 0xfffffffe)
  - **TX_WAIT_FOREVER**: (0xffffffff) TX_WAIT_FOREVER seçilmesi çağıran iş PARÇACıĞıNıN bir FTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur. Sayısal bir değer (1-0xFFFFFFFE) seçilmesi, FTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı FTP dizin silme.
- **NX_FTP_NOT_CONNECTED**: (0xd3) FTP istemcisi bağlı değil.
- **NX_FTP_EXPECTED_2XX_CODE**: (0xDA), 2xx (Tamam) yanıtını almadı 
- NX_PTR_ERROR: (0x07) geçersiz FTP işaretçisi. 
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Delete directory "my_dir" on the FTP Server connected to
    the FTP Client instance "my_client." */
status = nx_ftp_client_directory_delete(&my_client, "my_dir", 200);

/* If status is NX_SUCCESS the directory "my_dir" is deleted. */
```

## <a name="nx_ftp_client_directory_listing_get"></a>nx_ftp_client_directory_listing_get

FTP sunucusundan dizin listesini al

### <a name="prototype"></a>Prototype

```c
UINT nx_ftp_client_directory_listing_get(NX_FTP_CLIENT *ftp_client_ptr,
                            CHAR *directory_name, NX_PACKET **packet_ptr,
                            ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen FTP Istemcisine bağlı FTP sunucusunda belirtilen dizinin içeriğini alır. Sağlanan paket işaretçisi bir veya daha fazla dizin girişi içerecektir. Her giriş bir &lt; CR/LF \ birleşimi ile ayrılır. ***Nx_ftp_client_directory_listing_continue***: Dizin Al işlemini tamamlayacak şekilde çağrılmalıdır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_client_ptr**: FTP istemci denetim bloğu işaretçisi.
- **directory_name**: içeriğinin alınacağı dizinin adı.
- **packet_ptr**: hedef paket işaretçisine yönelik işaretçi. Başarılı olursa, paket yükü bir veya daha fazla dizin girişi içerir.
- **wait_option**: hizmetin FTP dizin listesi için bekleyeceği süreyi tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri**: (0x00000001 üzerinden 0xfffffffe)
  - **TX_WAIT_FOREVER**: (0xffffffff) TX_WAIT_FOREVER seçilmesi çağıran iş PARÇACıĞıNıN bir FTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur. Sayısal bir değer (1-0xFFFFFFFE) seçilmesi, FTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) FTP Dizin listeleme başarılı.
- **NX_FTP_NOT_CONNECTED**: (0xd3) FTP istemcisi bağlı değil.
- **NX_NOT_ENABLED**: (0X14) hizmet (IPv6) etkin değil
- **NX_FTP_EXPECTED_1XX_CODE**: (0xD9), 1xx (Tamam) yanıtını almadı
- **NX_FTP_EXPECTED_2XX_CODE**: (0xDA), 2xx (Tamam) yanıtını almadı
- NX_PTR_ERROR: (0x07) geçersiz FTP işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

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

FTP sunucusundan dizin listesine devam et

### <a name="prototype"></a>Prototype

```c
UINT nx_ftp_client_directory_listing_continue(NX_FTP_CLIENT
                    *ftp_client_ptr, NX_PACKET **packet_ptr,
                    ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen FTP Istemcisine bağlı FTP sunucusunda belirtilen dizinin içeriğini almaya devam eder. ***Nx_ftp_client_directory_listing_get*** çağrısı hemen öncesinde gelmelidir. Başarılı olursa, sağlanan paket işaretçisi bir veya daha fazla dizin girişi içerir. Bu yordam, bir NX_FTP_END_OF_LISTING durumu alınana kadar çağrılmalıdır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_client_ptr**: FTP istemci denetim bloğu işaretçisi.
- **packet_ptr**: hedef paket işaretçisine yönelik işaretçi. İşlem başarılı olursa, paket yükü bir CR/LF ile ayrılmış bir veya daha fazla dizin girişi içerecektir &lt; &gt; .
- **wait_option**: hizmetin FTP dizin listesi için bekleyeceği süreyi tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri**: (0x00000001 üzerinden 0xfffffffe)
  - **TX_WAIT_FOREVER**: (0xffffffff) TX_WAIT_FOREVER seçilmesi çağıran iş PARÇACıĞıNıN bir FTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur. Sayısal bir değer (1-0xFFFFFFFE) seçilmesi, FTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) FTP Dizin listeleme başarılı.
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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

Bu hizmet, daha önce açılmış bir dosyanın paketini okur. NX_FTP_END_OF_FILE bir durum alınana kadar kaldı çağrılmalıdır.

Çağıranın bu hizmet için bir paket ayırmadığını unutmayın.  Yalnızca bir paket işaretçisine işaretçi sağlamak için gereklidir. Bu hizmet, bu paket işaretçisini yuva alma sırasından alınan bir pakete işaret edecek şekilde güncelleştirecek.  Başarılı bir durum döndürülürse, bu, kullanılabilir bir paket olduğu anlamına gelir ve bu, paketin yaptığı sırada paketi serbest bırakma sorumluluğudur.

Sıfır olmayan bir durum (bir hata durumu veya NX_FTP_END_OF_FILE) döndürülürse, çağıran paketi serbest bırakmaz. Aksi takdirde, paket işaretçisi NULL olduğunda bir hata oluşturulur.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_client_ptr**: FTP istemci denetim bloğu işaretçisi.
- **packet_ptr**: kuyruktan alınan veri paketi işaretçisi için hedef işaretçisi. Başarılı olursa, paket verileri dosyanın bir kısmını veya tamamını içerir.
- **wait_option**: hizmetin FTP istemci dosyası okuması için ne kadar süre bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri**: (0x00000001 üzerinden 0xfffffffe)
  - **TX_WAIT_FOREVER**: (0xffffffff) TX_WAIT_FOREVER seçilmesi çağıran iş PARÇACıĞıNıN bir FTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur. Sayısal bir değer (1-0xFFFFFFFE) seçilmesi, FTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) FTP dosyası başarıyla okundu.
- **NX_FTP_NOT_OPEN**: (0xd5) FTP istemcisi açık değil.
- **NX_FTP_END_OF_FILE**: (0xd7) dosya koşulunun sonu.
- NX_PTR_ERROR: (0x07) geçersiz FTP işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

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

FTP sunucusundaki dosyayı yeniden adlandır

### <a name="prototype"></a>Prototype

```c
UINT nx_ftp_client_file_rename(NX_FTP_CLIENT *ftp_ptr, CHAR *filename,
                                CHAR *new_filename, ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, FTP sunucusundaki bir dosyayı yeniden adlandırır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_client_ptr**: FTP istemci denetim bloğu işaretçisi.
- **dosya adı**: dosyanın geçerli adı.
- **new_filename**: dosyanın yeni adı.
- **wait_option**: hizmetin FTP istemci dosyası yeniden adlandırma için bekleyeceği süreyi tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri**: (0x00000001 üzerinden 0xfffffffe)
  - **TX_WAIT_FOREVER**: (0xffffffff) TX_WAIT_FOREVER seçilmesi çağıran iş PARÇACıĞıNıN bir FTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur. Sayısal bir değer (1-0xFFFFFFFE) seçilmesi, FTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı FTP dosyası yeniden adlandırma.
- **NX_FTP_NOT_CONNECTED**: (0xd3) FTP istemcisi bağlı değil.
- **NX_FTP_EXPECTED_3XX_CODE**: (0xDD), 3xx (Tamam) yanıtını almadı
- **NX_FTP_EXPECTED_2XX_CODE**: (0xDA), 2xx (Tamam) yanıtını almadı
- NX_PTR_ERROR: (0x07) geçersiz FTP işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

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

Dosyaya yaz

### <a name="prototype"></a>Prototype

```c
UINT nx_ftp_client_file_write(NX_FTP_CLIENT *ftp_client_ptr,
                    NX_PACKET *packet_ptr, ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, FTP sunucusundaki daha önce açılan dosyaya bir veri paketi yazar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_client_ptr**: FTP istemci denetim bloğu işaretçisi.
- **packet_ptr**: yazılacak verileri içeren paket işaretçisi.
- **wait_option**: hizmetin FTP istemci dosyası yazma süresini ne kadar bekleyecektir tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri**: (0x00000001 üzerinden 0xfffffffe)
  - **TX_WAIT_FOREVER**: (0xffffffff) TX_WAIT_FOREVER seçilmesi çağıran iş PARÇACıĞıNıN bir FTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur. Sayısal bir değer (1-0xFFFFFFFE) seçilmesi, FTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı FTP dosyası yazma.
- **NX_FTP_NOT_OPEN**: (0xd5) FTP istemcisi açık değil.
- NX_PTR_ERROR: (0x07) geçersiz FTP işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

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

### <a name="description"></a>Açıklama

Bu hizmet, passive_mode_enabled girişi daha önceden oluşturulmuş bir FTP Istemci örneğinde NX_TRUE olarak ayarlandıysa (RETR, STOR) veya bir dizin listesini indirme (NLST), Aktarım modunda yapıldıktan sonra, pasif aktarım modunu sağlar. Pasif mod aktarımını devre dışı bırakmak ve etkin aktarım modunun varsayılan davranışına geri dönmek için, bu işlevi passive_mode_enabled girişi NX_FALSE kümesiyle çağırın.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_client_ptr**: FTP istemci denetim bloğu işaretçisi.
- **passive_mode_enabled**:
  - NX_TRUE olarak ayarlanırsa, Pasif mod etkinleştirilir.
  - NX_FALSE olarak ayarlanırsa, Pasif mod devre dışıdır.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı Pasif mod kümesi.
- NX_PTR_ERROR: (0x16) geçersiz FTP işaretçisi.
- NX_INVALID_PARAMETERS: (0x4D) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Enable the FTP Client to exchange data with the FTP server in passive mode. */

status = nx_ftp_client_passive_mode_set(&my_client, NX_TRUE);

/* If status is NX_SUCCESS, the FTP client is in passive transfer mode. */
```

## <a name="nx_ftp_server_create"></a>nx_ftp_server_create

FTP sunucusu oluştur

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

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen ve daha önce oluşturulmuş NetX IP örneğinde bir FTP sunucu örneği oluşturur. FTP sunucusunun, işleme başlaması için bir ***nx_ftp_server_start*** çağrısıyla başlatılması gerekir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ftp_server_ptr**: FTP sunucu denetim bloğu işaretçisi.
- **ftp_server_name**: FTP sunucusunun adı.
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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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
