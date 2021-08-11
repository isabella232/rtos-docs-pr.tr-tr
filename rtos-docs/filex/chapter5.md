---
title: Bölüm 5 - FileX için Azure RTOS Sürücüleri
description: Bu bölümde FileX için I/O sürücülerinin Azure RTOS yer almaktadır ve geliştiricilere uygulamaya özgü sürücüler yazmada yardımcı olmak için tasarlanmıştır.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 163893119837a46479b3f346c2bd47d200de2af75232f91a23bbc3f64e20ea50
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116782923"
---
# <a name="chapter-5---io-drivers-for-azure-rtos-filex"></a>Bölüm 5 - FileX için Azure RTOS Sürücüleri

Bu bölümde FileX için I/O sürücülerinin Azure RTOS yer almaktadır ve geliştiricilere uygulamaya özgü sürücüler yazmada yardımcı olmak için tasarlanmıştır.

## <a name="io-driver-introduction"></a>G/Ç Sürücüsüne Giriş

FileX birden çok medya cihazı destekler. Ortam FX_MEDIA medya cihazı yönetmek için gereken her şeyi tanımlar. Bu yapı, medyaya özgü I/O sürücüsü ve sürücü ile FileX arasında bilgi ve durum geçirmeye yönelik ilişkili parametreler de dahil olmak üzere tüm medya bilgilerini içerir. Çoğu sistemde, her FileX medya örneği için benzersiz bir I/O sürücüsü vardır.

## <a name="io-driver-entry"></a>G/Ç Sürücüsü Girişi

Her FileX G/Ç sürücüsünün tek bir giriş işlevi vardır ve bu işlev, ***fx_media_open*** çağrısı tarafından tanımlanır. Sürücü girişi işlevi aşağıdaki biçime sahiptir:

```c
void my_driver_entry(FX_MEDIA *media_ptr);
```

FileX başlatma ve önyükleme kesimi okuma dahil olmak üzere tüm fiziksel medya erişimini isteği için G/Ç sürücü giriş işlevini çağırır. Sürücüye yapılan istekler sırayla yapılır; Diğer bir ifadeyle FileX, başka bir istek gönderilmeden önce geçerli isteğin tamamlanır.

## <a name="io-driver-requests"></a>I/O Sürücü İstekleri

Her G/Ç sürücüsü tek bir giriş işlevine sahip olduğundan, FileX medya denetim bloğu aracılığıyla belirli istekler yapar. Özellikle,  **fx_media_driver_request** isteği **FX_MEDIA** için dosyanın bir üyesi kullanılır. I/O sürücüsü, isteğin başarılı veya başarısız olduğunu fx_media_driver_status **üyesi** aracılığıyla **FX_MEDIA.** Sürücü isteği başarılı olursa, **FX_SUCCESS** önce bu alana yerleştirilir. Aksi takdirde, bir hata algılanırsa, FX_IO_ERROR bu alana yerleştirilir.

### <a name="driver-initialization"></a>Sürücü Başlatma

Gerçek sürücü başlatma işlemi uygulamaya özgü olsa da, genellikle veri yapısı başlatmadan ve muhtemelen bazı ön donanım başlatmalardan oluşur. Bu istek, FileX tarafından yapılan ilk istektir ve dosya fx_media_open yapılır.

Medya yazma koruması algılanırsa, fx_media_driver_write_protect üyesi FX_MEDIA sürücü olarak FX_TRUE.

Aşağıdaki FX_MEDIA sürücü başlatma isteği için kullanılır:

|FX_MEDIA üye|Anlamı|
|-----------|-----------|
|fx_media_driver_request|FX_DRIVER_INIT|

FileX, kesimlerin artık kullanılmama durumuyla ilgili uygulama sürücüsünü bilgilendirmek için bir mekanizma sağlar. Bu, özellikle FLASH'a eşlenmiş tüm kullanımda mantıksal kesimleri yönetmesi gereken FLASH bellek yöneticileri için yararlıdır.

Ücretsiz kesimler hakkında böyle bir bildirim gerekirse, uygulama sürücüsü ilişkili *fx_media_driver_free_sector_update* yapısında FX_MEDIA **alanını** **FX_TRUE.** Ayardan sonra FileX, **_ardışık FX_DRIVER_RELEASE_SECTORS_** bir veya daha fazla kesimin serbest olduğunu belirten bir I/O sürücü çağrısı yapar.

### <a name="boot-sector-read"></a>Önyükleme Kesimi Okuma

FileX, standart bir okuma isteği kullanmak yerine medyanın önyükleme kesimlerini okumak için belirli bir istekte ır. Aşağıdaki **FX_MEDIA,** I/O sürücü önyükleme kesimi okuma isteği için kullanılır:

|FX_MEDIA üye|Anlamı|
|-----------|-----------|
|fx_media_driver_request| FX_DRIVER_BOOT_READ|
|fx_media_driver_buffer| Önyükleme kesimi için hedefin adresi.|

### <a name="boot-sector-write"></a>Önyükleme Kesimi Yazma

FileX, standart bir yazma isteği kullanmak yerine medyanın önyükleme kesimine yazma isteği yapar. Aşağıdaki **FX_MEDIA,** I/O sürücü önyükleme kesimi yazma isteği için kullanılır:

|FX_MEDIA üye|Anlamı|
|-----------|-----------|
|fx_media_driver_request| FX_DRIVER_BOOT_WRITE|
|fx_media_driver_buffer| Önyükleme kesimi kaynağının adresi.|

### <a name="sector-read"></a>Kesim Okuma

FileX, bir veya daha fazla kesimi belleğe okumak için, bir okuma isteğiniN/O sürücüsüne iletir. Aşağıdaki **FX_MEDIA,** I/O sürücü okuma isteği için kullanılır:

|FX_MEDIA üye|Anlamı|
|-----------|-----------|
|fx_media_driver_request| FX_DRIVER_READ|
|fx_media_driver_logical_sector|Okunacak mantıksal kesim|
|fx_media_driver_sectors|Okunacak kesim sayısı|
|fx_media_driver_buffer|Kesimler için hedef arabellek okuma|
|fx_media_driver_data_sector_read|Dosya FX_TRUE kesimi istense bu ayar olarak ayarlayın. Aksi FX_FALSE bir sistem kesimi (FAT veya dizin kesimi) istensin.|
|fx_media_driver_sector_type|İstenen kesimin açık türünü aşağıdaki gibi tanımlar:<br />FX_FAT_SECTOR (2)<br />FX_DIRECTORY_SECTOR (3)<br />FX_DATA_SECTOR (4)|

### <a name="sector-write"></a>Kesim Yazma

FileX, fiziksel medyaya bir veya daha fazla kesim yazarak, I/O sürücüsüne bir yazma isteği yayınlar. Aşağıdaki FX_MEDIA sürücü yazma isteği için kullanılır:

|FX_MEDIA üye| Anlamı|
|-----------|-----------|
|fx_media_driver_request|FX_DRIVER_WRITE|
|fx_media_driver_logical_sector|Yazacak mantıksal kesim|
|fx_media_driver_sectors|Yazacak kesim sayısı|
|fx_media_driver_buffer|Yazma için kesimler için kaynak arabelleği|
|fx_media_driver_system_write| Bir sistem FX_TRUE (FAT veya dizin kesimi) istense bu ayar olarak ayarlayın. Aksi FX_FALSE bir dosya veri kesimi istensin.|
|fx_media_driver_sector_type|İstenen kesimin açık türünü aşağıdaki gibi tanımlar:<br> <br>FX_FAT_SECTOR (2) <br> FX_DIRECTORY_SECTOR (3) <br>FX_DATA_SECTOR (4).|

### <a name="driver-flush"></a>Sürücü Boşaltma

FileX, O/Ç sürücüsüne bir boşaltma isteği yayınarak sürücünün kesim önbelleğinde bulunan tüm kesimleri fiziksel medyaya boşaltır. Elbette, sürücü kesimleri önbelleğe almasa, bu istek için sürücü işlemesi gerekli değildir. Aşağıdaki FX_MEDIA,O sürücü boşaltma isteği için kullanılır:

|FX_MEDIA üye| Anlamı|
|-----------|-----------|
|fx_media_driver_request|FX_DRIVER_FLUSH|

### <a name="driver-abort"></a>Sürücü Iptali

FileX, g/ç sürücüsüne bir iptal isteği vererek fiziksel medyayla tüm fiziksel g/ç etkinliklerini iptal etmek için sürücüye bildirir. Sürücünün yeniden başlatılması bitinceye kadar bir g/ç işlemi gerçekleştirmemelidir. Aşağıdaki FX_MEDIA üyeleri g/ç sürücü iptali isteği için kullanılır:

|FX_MEDIA üyesi| Anlamı|
|-----------|-----------|
|fx_media_driver_request| FX_DRIVER_ABORT|

### <a name="release-sectors"></a>Yayın kesimleri

Başlatma sırasında sürücü tarafından daha önce seçilirse FileX, bir veya daha fazla ardışık kesim ücretsiz olduğunda sürücüyü bilgilendirir. Sürücü aslında bir FLASH Manager ise bu bilgiler, FLASH Manager 'a bu kesimlerin artık gerekli olmadığını bildirmek için kullanılabilir. Aşağıdaki **FX_MEDIA** üyeleri g/ç sürüm kesimleri isteği için kullanılır:

|FX_MEDIA üyesi| Anlamı|
|-----------|-----------|
|fx_media_driver_request|FX_DRIVER_RELEASE_SECTORS|
|fx_media_driver_logical_sector|Ücretsiz kesim başlangıcı|
|fx_media_driver_sectors|Boş sektör sayısı|

### <a name="driver-suspension"></a>Sürücü askıya alma

Fiziksel medyayla g/ç bir süre sürebileceğinden, çağıran iş parçacığının askıya alınması genellikle tercih edilir. Tabii ki bu, temeldeki g/ç işleminin tamamlandığını kesintiye uğratan bir şekilde üstlenir. Bu durumda, iş parçacığı askıya alma, bir ThreadX semaforu ile kolayca uygulanır. Giriş veya çıkış işlemini başlattıktan sonra, g/ç sürücüsü kendi iç g/ç semaforu üzerinde bekletir (sürücü başlatma sırasında başlangıç sayısı sıfır ile oluşturulur). Sürücü g/ç tamamlama kesme işleminin bir parçası olarak, aynı g/ç semaforu ayarlanır ve bu da askıya alınan iş parçacığını uyandırır.

### <a name="sector-translation"></a>Kesim çevirisi

FileX, medyayı doğrusal mantıksal kesimler olarak görüntülediğinde g/ç sürücüsüne yapılan g/ç istekleri mantıksal kesimlerle yapılır. Mantıksal kesimler ve medyanın fiziksel geometrisi arasında çevrilecek, bu da kafa, iz ve fiziksel kesimleri içerebilen sürücü sorumluluğundadır. FLASH ve RAM disk medyası için, mantıksal kesimler genellikle dizini fiziksel kesimlerde eşler. Her durumda, g/ç sürücüsünde mantıksal to fiziksel kesim eşlemesini gerçekleştirmek için tipik formüller aşağıda verilmiştir:

```c
media_ptr -> fx_media_driver_physical_sector =
    (media_ptr -> fx_media_driver_logical_sector % media_ptr -> fx_media_sectors_per_track) + 1;

media_ptr -> fx_media_driver_physical_head =
    (media_ptr -> fx_media_driver_logical_sector/ media_ptr ->
    fx_media_sectors_per_track) % media_ptr -> fx_media_heads;

media_ptr -> fx_media_driver_physical_track =(media_ptr ->
    fx_media_driver_logical_sector/ (media_ptr -> fx_media_sectors_per_track *
    media_ptr -> fx_media_heads)));
```

Fiziksel kesimlerin tek seferde başlayıp mantıksal kesimlerin sıfırdan başlaması gerektiğini unutmayın.

### <a name="hidden-sectors"></a>Gizli kesimler

Gizli kesimler, medyadaki önyükleme kaydından önce yer alır. Bunlar aslında FAT dosya sistemi düzeninin kapsamı dışında olduğundan, sürücünün her mantıksal kesim işleminde hesaba katılmış olmaları gerekir.

### <a name="media-write-protect"></a>Medya yazma koruması

FileX sürücüsü, medya denetim bloğunda fx_media_driver_write_protect alanını ayarlayarak yazma korumasını açabilir. Bu, medyaya yazma girişiminde herhangi bir FileX çağrısı yapılırsa bir hata döndürülmesine neden olur.

## <a name="sample-ram-driver"></a>Örnek RAM sürücüsü

FileX tanıtım sistemi, fx_ram_driver. c dosyasında tanımlanan küçük bir RAM disk sürücüsüyle birlikte dağıtılır. Sürücü, bir 32K bellek alanını varsayar ve 256 128 baytlık kesimler için bir önyükleme kaydı oluşturur. Bu dosya, uygulamaya özel FileX g/ç sürücülerinin nasıl uygulanacağı hakkında iyi bir örnek sağlar.

```c
/*FUNCTION: _fx_ram_driver
RELEASE: PORTABLE C 5.7
AUTHOR: William E. Lamie, Microsoft, Inc.
DESCRIPTION: This function is the entry point to the generic
    RAM disk driver that is delivered with all versions of FileX.
    The format of the RAM disk is easily modified by calling fx_media_format prior to opening the media.

    This driver also serves as a template for developing FileX drivers
    for actual devices. Simply replace the read/write sector logic
    with calls to read/write from the appropriate physical device.

FileX RAM/FLASH structures look like the following:
Physical Sector             Contents
    0                         Boot record
    1                         FAT Area Start
    +FAT Sectors             Root Directory Start
    +Directory Sectors         Data Sector Start

INPUT: media_ptr Media control block pointer
OUTPUT: None
CALLS:     _fx_utility_memory_copy Copy sector memory
        _fx_utility_16_unsigned_read Read 16-bit unsigned
CALLED BY: FileX System Functions
RELEASE HISTORY:

    DATE         NAME         DESCRIPTION
    12-12-2005     William E.     Lamie Initial Version 5.0
    07-18-2007     William E.     Lamie Modified comment(s),
                                resulting in version 5.1
    03-01-2009     William E.     Lamie Modified comment(s),
                                resulting in version 5.2
    11-01-2015     William E.     Lamie Modified comment(s),
                                resulting in version 5.3
    04-15-2016     William E.     Lamie Modified comment(s),
                                resulting in version 5.4
    04-03-2017     William E.     Lamie Modified comment(s),
                                fixed compiler warnings,
                                resulting in version 5.5
    12-01-2018     William E.     Lamie Modified comment(s),
                                checked buffer overflow,
                                resulting in version 5.6
    08-15-2019     William E.     Lamie Modified comment(s),
                                resulting in version 5.7
*/

VOID _fx_ram_driver(FX_MEDIA *media_ptr) { UCHAR *source_buffer;
                                           UCHAR *destination_buffer;
                                           UINT bytes_per_sector;

    /* There are several useful/important pieces of information contained
        in the media structure, some of which are supplied by FileX and
        others are for the driver to setup. The following
        is a summary of the necessary FX_MEDIA structure members:
    FX_MEDIA Member                     Meaning

    fx_media_driver_request             FileX request type.
        Valid requests from FileX are as follows:
        FX_DRIVER_READ
        FX_DRIVER_WRITE
        FX_DRIVER_FLUSH
        FX_DRIVER_ABORT
        FX_DRIVER_INIT
        FX_DRIVER_BOOT_READ
        FX_DRIVER_RELEASE_SECTORS
        FX_DRIVER_BOOT_WRITE FX_DRIVER_UNINIT

    fx_media_driver_status              This value is RETURNED by the driver.
        If the operation is successful, this field should be set to FX_SUCCESS
        for before returning. Otherwise, if an error occurred, this field should be set to FX_IO_ERROR.

    fx_media_driver_buffer              Pointer to buffer to read or write sector data. This is supplied by FileX.

    fx_media_driver_logical_sector      Logical sector FileX is requesting.
    fx_media_driver_sectors             Number of sectors FileX is requesting.

    The following is a summary of the optional FX_MEDIA structure members: FX_MEDIA Member Meaning

    fx_media_driver_info                Pointer to any additional information or memory.
        This is optional for the driver use and is setup from the fx_media_open call.
        The RAM disk uses this pointer for the RAM disk memory itself.

    fx_media_driver_write_protect       The DRIVER sets this to FX_TRUE when media is write protected.
        This is typically done in initialization, but can be done anytime.

    fx_media_driver_free_sector_update  The DRIVER sets this to FX_TRUE when it needs
        to know when clusters are released. This is important for FLASH wear-leveling drivers.

    fx_media_driver_system_write        FileX sets this flag to FX_TRUE if the sector
        being written is a system sector, e.g., a boot, FAT, or directory sector.
        The driver may choose to use this to initiate error recovery logic for greater fault
        tolerance. fx_media_driver_data_sector_read FileX sets this flag to FX_TRUE
        if the sector(s) being read are file data sectors, i.e., NOT system sectors.

    fx_media_driver_sector_type         FileX sets this variable to the specific type of
        sector being read or written. The following sector types are identified:
            FX_UNKNOWN_SECTOR
            FX_BOOT_SECTOR
            FX_FAT_SECTOR
            FX_DIRECTORY_SECTOR
            FX_DATA_SECTOR */

    /* Process the driver request specified in the media control block. */

    switch (media_ptr -> fx_media_driver_request){

        case FX_DRIVER_READ: {

            /* Calculate the RAM disk sector offset. Note the RAM disk memory
            is pointed to by the fx_media_driver_info pointer, which is supplied
            by the application in the call to fx_media_open. */

            source_buffer = ((UCHAR *)media_ptr -> fx_media_driver_info) +
                ((media_ptr -> fx_media_driver_logical_sector +
                media_ptr -> fx_media_hidden_sectors) * media_ptr -> fx_media_bytes_per_sector);

            /* Copy the RAM sector into the destination. */

             _fx_utility_memory_copy(source_buffer,
                media_ptr -> fx_media_driver_buffer, media_ptr -> fx_media_driver_sectors *
                media_ptr -> fx_media_bytes_per_sector);

            /* Successful driver request. */

            media_ptr -> fx_media_driver_status = FX_SUCCESS; break; }

        case FX_DRIVER_WRITE: {

            /* Calculate the RAM disk sector offset. Note the RAM disk memory
                is pointed to by the fx_media_driver_info pointer, which is supplied
                by the application in the call to fx_media_open. */

            destination_buffer = ((UCHAR *)media_ptr -> fx_media_driver_info) +
                ((media_ptr -> fx_media_driver_logical_sector +
                media_ptr -> fx_media_hidden_sectors) * media_ptr -> fx_media_bytes_per_sector);

            /* Copy the source to the RAM sector. */

            _fx_utility_memory_copy(media_ptr -> fx_media_driver_buffer,
                destination_buffer, media_ptr -> fx_media_driver_sectors *
                media_ptr -> fx_media_bytes_per_sector);

            /* Successful driver request. */

            media_ptr -> fx_media_driver_status = FX_SUCCESS; break; }

        case FX_DRIVER_FLUSH: {
            /* Return driver success. */
            media_ptr -> fx_media_driver_status = FX_SUCCESS; break; }

        case FX_DRIVER_ABORT: {
            /* Return driver success. */
            media_ptr -> fx_media_driver_status = FX_SUCCESS; break; }

        case FX_DRIVER_INIT: {

            /* FLASH drivers are responsible for setting several fields
                in the media structure, as follows:
                media_ptr -> fx_media_driver_free_sector_update media_ptr ->
                fx_media_driver_write_protect
                The fx_media_driver_free_sector_update flag is used to instruct
                FileX to inform the driver whenever sectors are not being used.
                This is especially useful for FLASH managers so they don't have
                maintain mapping for sectors no longer in use.
                The fx_media_driver_write_protect flag can be set anytime by
                the driver to indicate the media is not writable. Write attempts
                made when this flag is set are returned as errors. */
            /* Perform basic initialization here... since the boot record is going
                to be read subsequently and again for volume name requests. */
            /* Successful driver request. */

            media_ptr -> fx_media_driver_status = FX_SUCCESS; break; }

         case FX_DRIVER_UNINIT: {

            /* There is nothing to do in this case for the RAM driver.
                For actual devices some shutdown processing may be necessary. */

            /* Successful driver request. */
            media_ptr -> fx_media_driver_status = FX_SUCCESS; break; }

        case FX_DRIVER_BOOT_READ: {
            /* Read the boot record and return to the caller. */

            /* Calculate the RAM disk boot sector offset, which is at the
                very beginning of the RAM disk. Note the RAM disk memory is pointed
                to by the fx_media_driver_info pointer, which is supplied by the
                application in the call to fx_media_open. */

            source_buffer = (UCHAR *)media_ptr -> fx_media_driver_info;

            /* For RAM driver, determine if the boot record is valid. */

            if ((source_buffer[0] != (UCHAR)0xEB) ||

            ((source_buffer[1] != (UCHAR)0x34) &&

            (source_buffer[1] != (UCHAR)0x76)) || /* exFAT jump code. */

            (source_buffer[2] != (UCHAR)0x90)) {

            /* Invalid boot record, return an error! */
            media_ptr -> fx_media_driver_status = FX_MEDIA_INVALID; return; }

            /* For RAM disk only, pickup the bytes per sector. */

            bytes_per_sector =
                _fx_utility_16_unsigned_read(&source_buffer[FX_BYTES_SECTOR]); #ifdef FX_ENABLE_EXFAT

            /* if byte per sector is zero, then treat it as exFAT volume. */

            if (bytes_per_sector == 0 && (source_buffer[1] == (UCHAR)0x76)) {

            /* Pickup the byte per sector shift, and calculate byte per sector. */ 
            bytes_per_sector = (UINT)(1 << source_buffer[FX_EF_BYTE_PER_SECTOR_SHIFT]);

            }

            #endif /* FX_ENABLE_EXFAT */

            /* Ensure this is less than the media memory size. */
            if (bytes_per_sector \media_ptr -> fx_media_memory_size) {

            media_ptr -> fx_media_driver_status = FX_BUFFER_ERROR; break; }

            /* Copy the RAM boot sector into the destination. */

            _fx_utility_memory_copy(source_buffer, media_ptr -> fx_media_driver_buffer, bytes_per_sector);

            /* Successful driver request. */

            media_ptr -> fx_media_driver_status = FX_SUCCESS; break; }

        case FX_DRIVER_BOOT_WRITE: {

            /* Write the boot record and return to the caller. */

            /* Calculate the RAM disk boot sector offset, which is at the
                very beginning of the RAM disk. Note the RAM disk memory is
                pointed to by the fx_media_driver_info pointer, which is supplied
                by the application in the call to fx_media_open. */ 
            destination_buffer = (UCHAR *)media_ptr -> fx_media_driver_info;

            /* Copy the RAM boot sector into the destination. */

            _fx_utility_memory_copy(media_ptr -> fx_media_driver_buffer,
                destination_buffer, media_ptr -> fx_media_bytes_per_sector);

            /* Successful driver request. */

            media_ptr -> fx_media_driver_status = FX_SUCCESS; break; }

        default: {
            /* Invalid driver request. */
            media_ptr -> fx_media_driver_status = FX_IO_ERROR; break;}
    }
}
```
