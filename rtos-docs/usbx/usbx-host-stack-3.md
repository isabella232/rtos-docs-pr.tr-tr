---
title: Bölüm 3 - USBX Konak Yığınının İşlevsel Bileşenleri
description: Bu bölümde, işlevsel bir perspektiften yüksek performanslı USBX ekli USB konak yığınının açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: a3cbbb2e26d66d3db26144a47a1b6cbb11387c7b5b2ba5e19d35df026e5e3598
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116790934"
---
# <a name="chapter-3---functional-components-of-usbx-host-stack"></a>Bölüm 3 - USBX Konak Yığınının İşlevsel Bileşenleri

Bu bölümde, işlevsel bir perspektiften yüksek performanslı USBX ekli USB konak yığınının açıklaması yer almaktadır.

## <a name="execution-overview"></a>Yürütmeye Genel Bakış

USBX çeşitli bileşenlerden oluşur:

- Başlatma
- Uygulama arabirimi çağrıları
- Kök Hub
- Hub Sınıfı
- Konak Sınıfları
- USB Konak Yığını
- Konak denetleyicisi

Aşağıdaki diyagramda USBX konak yığınını göstermektedir.

![USBX Konak Yığını](./media/usbx-host-stack/usbx-host-stack.png)

### <a name="initialization"></a>Başlatma

USBX'i etkinleştirmek için işlev ***ux_system_initialize*** çağrılmalı. Bu işlev USBX'in bellek kaynaklarını başlatıyor.

USBX konak olanaklarını etkinleştirmek için ***işlev*** ux_host_stack_initialize çağrılmalı. Bu işlev, ThreadX iş parçacıkları, mutex'ler ve semaforlar gibi USBX konak yığını tarafından kullanılan tüm kaynakları başlatacak.

En az bir USB konak denetleyicisi ve bir veya daha fazla USB sınıflarını etkinleştirmek uygulama başlatmaya bağlı olur. Sınıflar yığına kaydedilenin ve konak denetleyicilerini başlatma işlevi çağrıldığı zaman veri sistemi etkindir ve cihaz bulma başlatabilirsiniz. Konak denetleyicisinin kök hub'ı bağlı bir cihaz algılarsa, USB topolojisi sorumlu USB numaralama iş parçacığı uyandırıp cihaz numaralama işlemine devam eder.

Kök hub'ın ve aşağı akış hub'larının yapısı nedeniyle, konak denetleyicisi başlatma işlevi döndür olduğunda tüm bağlı USB cihazlarının tamamen yapılandırılmamış olması mümkündür. Özellikle kök hub ile USB cihazları arasında bir veya daha fazla hub varsa, tüm USB cihazlarının numaralarını almak birkaç saniye sürebilir.

### <a name="application-interface-calls"></a>Uygulama Arabirimi Çağrıları

USBX'te iki API düzeyi vardır.

- USB Konak Yığını API'leri
- USB Konak Sınıfı API'leri

Normalde, bir USBX uygulamasının USB konak yığını API'si işlevlerden herhangi birini çağıran bir şey olması gerekir. Çoğu uygulama yalnızca USB Sınıfı API işlevlerine erişecek.

### <a name="usb-host-stack-apis"></a>USB Konak Yığını API'leri

Konak yığını API'si işlevleri USBX bileşenlerinin (konak sınıfları ve konak denetleyicileri), cihazların yapılandırmasını ve kullanılabilir cihaz uç noktaları için aktarım isteklerinin kaydından sorumludur.

### <a name="usb-host-class-api"></a>USB Konak Sınıfı API'si

Sınıf API'leri her USB sınıfına çok özeldir. USB sınıfları için yaygın API işlevlerinin çoğu, bir cihazı açma/kapatma ve cihazdan okuma ve yazma gibi hizmetler sağlar.

### <a name="root-hub"></a>Kök Hub

Her konak denetleyicisi örneğinin bir veya daha fazla USB kök hub'ı vardır. Kök hub'ların sayısı denetleyicinin yapısına göre belirlenir veya denetleyiciden belirli yazmaylar okunarak alınabilirsiniz.

### <a name="hub-class"></a>Hub Sınıfı

Hub sınıfı, USB hub'larını kullanmadan sorumlu. USB hub'ı tek başına bir hub veya klavye ya da monitör gibi bileşik bir cihazın parçası olarak olabilir. Merkez kendi kendine veya veriyle güçlendirilmiş olabilir. Veri yoluyla desteklenen hub'lar en fazla dört aşağı akış bağlantı noktası içerir ve yalnızca 100 mA'dan az güç kullanan otomatik olarak çalışan veya veri yoluyla desteklenen cihazların bağlantılarına izin verir. Hub'lar basamaklı olarak kullanılabilir. En fazla beş merkez birbirine bağlanabilir.

### <a name="usb-host-stack"></a>USB Konak Yığını

USB ana bilgisayar yığını, USBX'in orta parçasıdır. Üç ana işlevi vardır.

- USB'nin topolojilerini yönetin.
- USB cihazını bir veya daha fazla sınıfa bağlayın.
- Cihaz tanımlayıcısı tanımlayıcısını ve USB aktarımlarını gerçekleştirmek için sınıflara bir API sağlama.

### <a name="topology-manager"></a>Topoloji Yöneticisi

USB yığın topolojisi iş parçacığı, yeni bir cihaz bağlandığında veya bir cihazın bağlantısı kesildiğinde uyandırıldı. Kök hub veya normal hub cihaz bağlantılarını kabul eder. Bir cihaz USB'ye bağlandıktan sonra topoloji yöneticisi cihaz tanımlayıcısını alır. Bu tanımlayıcı, bu cihaz için kullanılabilen olası yapılandırma sayısını içerir. Çoğu cihaz yalnızca bir yapılandırmaya sahip olur. Bazı cihazlar, bağlı olduğu bağlantı noktası üzerinde bulunan kullanılabilir güçle farklı şekilde çalışabilirsiniz. Bu durumda, cihaz kullanılabilir güç bağlı olarak seçilecek birden çok yapılandırmaya sahip olur. Cihaz topoloji yöneticisi tarafından yapılandırıldığında, yapılandırma tanımlayıcısında belirtilen güç miktarını çizmesine izin verilir.

## <a name="usb-class-binding"></a>USB Sınıfı Bağlama

Cihaz yapılandırıldığında topoloji yöneticisi, cihaz arabirimi tanımlayıcılarına bakarak sınıf yöneticisinin cihaz keşfine devamsına izin verir. Bir cihazda bir veya daha fazla arabirim tanımlayıcısı olabilir.

Arabirim, bir cihaz içinde bir işlevi temsil eder. Örneğin USB konuşmacının biri ses akışı, biri ses denetimi ve biri de çeşitli konuşmacı düğmelerini yönetmek için olmak üzere üç arabirimi vardır.

Sınıf yöneticisi, cihaz arabirimlerini bir veya daha fazla sınıfa katacak iki mekanizmaya sahiptir. Arabirim tanımlayıcısında bulunan piD/VID (ürün kimliği ve satıcı kimliği) birleşimini veya Sınıf/Alt Sınıf/Protokol birleşimini kullanabilir.

PID/VID birleşimi, genel bir sınıf tarafından yönlendirilene arabirimler için geçerlidir. Sınıf/Alt Sınıf/Protokol birleşimi yazıcı, hub, depolama, ses veya GIZLI GIBI USB-IF sertifikalı bir sınıfa ait arabirimler tarafından kullanılır.

Sınıf yöneticisi, USBX'i başlatmadan itibaren kayıtlı sınıfların listesini içerir. Sınıf yöneticisi, bir sınıf o cihazın arabirimini yönetmeyi kabul edene kadar her sınıfı tek tek çağıracak. Bir sınıf yalnızca bir arabirimi yönetebilir. USB ses konuşmacısı örneği için sınıf yöneticisi arabirimlerin her biri için tüm sınıfları çağıracak.

Bir sınıf bir arabirimi kabul etti mi, bu sınıfın yeni bir örneği oluşturulur. Ardından sınıf yöneticisi, arabirim için varsayılan alternatif ayarı aratır. Bir cihazın her arabirim için bir veya daha fazla alternatif ayarı olabilir. Alternatif ayar 0, bir sınıf bunu değiştirmeye karar verinceye kadar varsayılan olarak kullanılan açık ayarıdır.

Varsayılan alternatif ayar için, sınıf yöneticisi alternatif ayarda yer alan tüm uç noktaları bağlar. Her uç noktanın bağlaması başarılı olursa, sınıf yöneticisi arabirimin başlatmasını bitirecek sınıfına dönerek işini tamamlar.

### <a name="usbx-apis"></a>USBX API'leri

USB yığını, belirli uç noktalarda cihaz ve USB aktarımları gerçekleştirmek üzere USB sınıflarının belirli sayıda API'sini dışarı aktarıyor. Bu API işlevleri bu başvuru kılavuzunda ayrıntılı olarak açıklanmıştır.

### <a name="host-controller"></a>Konak Denetleyicisi

Ana bilgisayar denetleyicisi sürücüsü belirli bir USB denetleyicisi türünü sürücüden sorumludur. Bir USB konak denetleyicisinin içinde birden çok denetleyici olabilir. Örneğin, belirli Intel PC yonga kümesi iki TANE TANECI denetleyici içerir. Bazı USB 2.0 denetleyicileri, EHCI denetleyicisinin bir örneğine ek olarak BIR AHCI denetleyicisinin birden çok örneğini içerir.

Konak denetleyicisi yalnızca aynı denetleyicinin birden çok örneğini yönetir. Çoğu USB 2.0 konak denetleyicisini sürücüye bağlamak için, USBX'in başlatılması sırasında hem OCHI denetleyicisinin hem de EHCI denetleyicisinin başlatılması gerekir.

Konak denetleyicisi aşağıdakilerin yönetiminden sorumludur.

- Kök Hub
- Güç Yönetimi
- Uç Noktalar
- Transfer

### <a name="root-hub"></a>Kök Hub

Kök hub yönetimi, her denetleyici bağlantı noktasının gücünden ve eklenen bir cihaz olup olmadığının belirlenmesinden sorumludur. Bu işlev USBX genel kök hub'ı tarafından denetleyici aşağı akış bağlantı noktalarını sorgulamak için kullanılır.

### <a name="power-management"></a>Güç Yönetimi

Güç yönetimi işleme, askıya alma/sürdürme sinyallerinin aynı anda tüm denetleyici aşağı akış bağlantı noktalarını etkilemesi veya denetleyicinin bu işlevi sunduğunda ayrı ayrı işlemesini sağlar.

### <a name="endpoints"></a>Uç Noktalar

Uç nokta yönetimi, denetleyiciye fiziksel uç noktaların oluşturulmasını veya yok edilmesi için sağlar. Fiziksel uç noktalar, denetleyici ana DMA'yı destekliyorsa veya denetleyicide yazılmışsa denetleyici tarafından ayrıştıran bellek varlıklarıdır. Fiziksel uç noktalar, denetleyici tarafından gerçekleştirilecek işlem bilgilerini içerir.

### <a name="transfers"></a>Transfer

Aktarım yönetimi, oluşturulan uç noktaların her biri üzerinde işlem gerçekleştirmek için bir sınıf sağlar. Her mantıksal uç nokta, USB aktarım istekleri için TRANSFER REQUEST adlı bir bileşen içerir. AKTARıM İsteği, işlemi açıklamak için yığın tarafından kullanılır. Bu AKTARıM İsteği daha sonra yığına ve denetleyiciye geçirerek denetleyicinin özelliklerine bağlı olarak birkaç alt işleme bölüştü.

## <a name="usb-device-framework"></a>USB Cihaz Çerçevesi

USB cihazı bir tanımlayıcı ağacıyla temsil edilen bir cihazdır. Altı ana tanımlayıcı türü vardır.

- Cihaz tanımlayıcıları
- Yapılandırma tanımlayıcıları
- Arabirim tanımlayıcıları
- Uç nokta tanımlayıcıları
- Dize tanımlayıcıları
- İşlevsel tanımlayıcılar

USB cihazı çok basit bir açıklamaya sahip olabilir ve aşağıdakine benzer olabilir.
![Basit USB cihazı](./media/usbx-host-stack/usb-device-simple.png)

Yukarıdaki çizimde, cihazın yalnızca bir yapılandırması vardır. Bu yapılandırmaya, cihazın yalnızca bir işlevi olduğunu ve yalnızca bir uç noktası olduğunu gösteren tek bir arabirim ekli. Cihaz tanımlayıcısına bağlı, cihazın görünür bir tanımlamasını sağlayan bir dize tanımlayıcısıdır.

Ancak, bir cihaz daha karmaşık olabilir ve aşağıdaki gibi görünebilir.

![Karmaşık USB cihazı](./media/usbx-host-stack/usb-device-complex.png)

Yukarıdaki çizimde, cihazın cihaz tanımlayıcısına bağlı iki yapılandırma tanımlayıcısı vardır. Bu cihaz iki güç modu olduğunu veya standart sınıflar ya da özel sınıflar tarafından yönlendiriLl olduğunu gösteriyor olabilir.

İlk yapılandırmaya, cihazın iki mantıksal işlevi olduğunu gösteren iki arabirim eklidir. İlk işlevin 3 uç nokta tanımlayıcısı ve işlevsel tanımlayıcısı vardır. İşlevsel tanımlayıcı, normalde genel bir tanımlayıcı tarafından bulunamaz, bu arabirim hakkında daha fazla bilgi almak için arabirimini sürücüsünden sorumlu sınıfı tarafından kullanılabilir.

### <a name="device-descriptors"></a>Cihaz Tanımlayıcıları

Her USB cihazının tek bir cihaz tanımlayıcısı vardır. Bu tanımlayıcı cihaz tanımlamasını, desteklenen yapılandırma sayısını ve cihazı yapılandırmak için kullanılan varsayılan denetim uç noktasının özelliklerini içerir.

| Uzaklık | Alan              | Boyut | Değer    | Açıklama                             |
| ------ | ------------------ | ---- | -------- | --------------------------------------- |
| 0      | BLength            | 1    | Sayı   | Bu tanımlayıcının bayt cinsinden boyutu |
| 1      | bDescriptorType    | 1    | Sabit | DEVICE Tanımlayıcı Türü |
| 2      | bcdUSB             | 2    | Bcd      | BinaryCoded Ara Kodunda USB Belirtimi Sürüm Numarası<br />Örnek: 2.10, 0x210. Bu alan, cihazın ve tanımlayıcılarının uyumlu olduğu USB Belirtimi'nin yayınını tanımlar. |
| 4      | bDeviceClass       | 1    | Sınıf    | Sınıf kodu (USB-IF tarafından atanır).<br />Bu alan 0'a sıfırlanırsa, yapılandırma içindeki her arabirim kendi sınıf bilgilerini belirtir ve çeşitli arabirimler bağımsız olarak çalışır.<br />Bu alan 1 ile 0xFE arasında bir değere ayarlanırsa, cihaz farklı arabirimlerde farklı sınıf belirtimlerini destekler ve arabirimler bağımsız olarak çalışmayabilirsiniz. Bu değer, toplama arabirimleri için kullanılan sınıf tanımını tanımlar.<br />Bu alan varsayılan olarak 0xFF cihaz sınıfı satıcıya özgü olur. |
| 5      | bDeviceSubClass    | 1    | Alt | Alt sınıf kodu (USB-IF tarafından atanır).<br />Bu kodlar bDeviceClass alanı değerine göre niteliklidir. bDeviceClass alanı 0'a sıfırlanırsa, bu alan da 0'a sıfırlanır. bDeviceClass alanı bir 0xFF olarak ayarlanmazsa, tüm değerler USB tarafından atama için ayrılmıştır. |
| 6      | bDeviceProtocol    | 1    | Protokol | Protokol kodu (USB-IF tarafından atanır).<br />Bu kodlar bDeviceClass ve bDeviceSubClass alanlarının değerine göre niteliklidir. Bir cihaz arabirim temelinden farklı olarak sınıfa özgü protokolleri destekliyorsa, bu kod cihazın kullandığı protokolleri cihaz sınıfının belirtimlerine göre tanımlandığı şekilde tanımlar. Bu alan 0'a sıfırlanırsa, cihaz cihaz bazında sınıfa özgü protokolleri kullanmaz.<br />Ancak, arabirim temelinde sınıfa özgü protokoller kullanabilir.<br />Bu alan bir 0xFF olarak ayarlanırsa, cihaz cihaz temelinde satıcıya özgü bir protokol kullanır. |
| 7      | bMaxPacketSize0    | 1    | Sayı   | Uç nokta sıfır için en büyük paket boyutu (yalnızca 8, 16, 32 veya 64 byte boyutları geçerlidir) |
| 8      | idVendor           | 2    | ID       | Satıcı Kimliği (USB-IF tarafından atanır) |
| 10     | idProduct          | 2    | ID       | Ürün Kimliği (Üretici tarafından atanan) |
| 12     | bcdDevice          | 2    | Bcd      | İkili kodlu ondalık kodlu cihaz yayın numarası |
| 14     | iManufacturer      | 1    | Dizin oluşturma    | Üreticiyi açıklayan dize tanımlayıcısı dizini |
| 15     | iProduct           | 1    | Dizin oluşturma    | Ürünü açıklayan dize tanımlayıcısı dizini |
| 16     | iSerialNumbe       | 1    | Dizin oluşturma    | Cihazın seri numarasını açıklayan dize tanımlayıcısı dizini |
| 17     | bNumConfigurations | 1    | Sayı   | Olası yapılandırma sayısı |

USBX, usb cihaz tanımlayıcısını aşağıdaki gibi tanımlar:

```c
typedef struct UX_DEVICE_DESCRIPTOR_STRUCT
{
    UINT      bLength;
    UINT      bDescriptorType;
    USHORT    bcdUSB;
    UINT      bDeviceClass;
    UINT      bDeviceSubClass;
    UINT      bDeviceProtocol;
    UINT      bMaxPacketSize0;
    USHORT    idVendor;
    USHORT    idProduct;
    USHORT    bcdDevice;
    UINT      iManufacturer;
    UINT      iProduct;
    UINT      iSerialNumber;
    UINT      bNumConfigurations;
} UX_DEVICE_DESCRIPTOR;
```

USB cihaz tanımlayıcısı, şu şekilde açıklanan bir cihaz kapsayıcısı kapsamındadır:

```c
typedef struct UX_DEVICE_STRUCT
{
    ULONG ux_device_handle;
    ULONG ux_device_type;
    ULONG ux_device_state;
    ULONG ux_device_address;
    ULONG ux_device_speed;
    ULONG ux_device_port_location;
    ULONG ux_device_max_power;
    ULONG ux_device_power_source;
    UINT ux_device_current_configuration;

    TX_SEMAPHORE ux_device_protection_semaphore;
    struct UX_DEVICE_STRUCT *ux_device_parent; 
    struct UX_HOST_CLASS_STRUCT *ux_device_class; 
    VOID *ux_device_class_instance;
    struct UX_HCD_STRUCT *ux_device_hcd;
    struct UX_CONFIGURATION_STRUCT *ux_device_first_configuration; 
    struct UX_DEVICE_STRUCT *ux_device_next_device;
    struct UX_DEVICE_DESCRIPTOR_STRUCT ux_device_descriptor;
    struct UX_ENDPOINT_STRUCT ux_device_control_endpoint;
    struct UX_HUB_TT_STRUCT ux_device_hub_tt[UX_MAX_TT];
} UX_DEVICE;
```

- **ux_device_handle:** Cihazın tanıtıcısı. Bu genellikle cihaz için bu yapı örneğinin adresidir.
- **ux_device_type:** Eski değer. Kullanılmıyor.
- **ux_device_state:** Cihaz Durumu: Aşağıdaki değerlerden birini kullanabilirsiniz:
    - **UX_DEVICE_RESET**                0
    - **UX_DEVICE_ATTACHED**             1
    - **UX_DEVICE_ADDRESSED**            2
    - **UX_DEVICE_CONFIGURED**           3
    - **UX_DEVICE_SUSPENDED**            4
    - **UX_DEVICE_RESUMED**              5
    - **UX_DEVICE_SELF_POWERED_STATE**   6
    - **UX_DEVICE_SELF_POWERED_STATE**   7
    - **UX_DEVICE_REMOTE_WAKEUP**        8
    - **UX_DEVICE_BUS_RESET_COMPLETED**  9
    - **UX_DEVICE_REMOVED**              10
    - **UX_DEVICE_FORCE_DISCONNECT**     11
- **ux_device_address:** SET_ADDRESS komutu **kabul** edildikten sonra cihazın adresi (1 ile 127 arasında).
- **ux_device_speed:** Cihazın hızı:
    - **UX_LOW_SPEED_DEVICE**      0
    - **UX_FULL_SPEED_DEVICE**     1
    - **UX_HIGH_SPEED_DEVICE**     2
- **ux_device_port_location:** Üst cihazın bağlantı noktasının dizini (kök hub veya hub).
- **ux_device_max_power:** Cihazın seçili yapılandırmada sahip olduğu maksimum mA gücü.
- **ux_device_power_source:** Aşağıdaki iki değerden biri olabilir:
    - **UX_DEVICE_BUS_POWERED**     1
    - **UX_DEVICE_SELF_POWERED**    2
- **ux_device_current_configuration:** Bu cihaz tarafından kullanılan geçerli yapılandırmanın dizini.
- **ux_device_parent:** Bu cihazın üst öğesi cihaz kapsayıcı işaretçisi. İşaretçi null ise, üst denetleyicinin kök hub'ıdır.
- **ux_device_class:** Bu cihaza sahip olan sınıf türünün işaretçisi.
- **ux_device_class_instance:** Bu cihaza sahip olan sınıfın örneğinin işaretçisi.
- **ux_device_hcd:** Cihazın ekli olduğu USB Konak Denetleyicisi Örneği.
- **ux_device_first_configuration:** Bu cihaz için ilk yapılandırma kapsayıcısı işaretçisi.
- **ux_device_next_device:** USBX tarafından algılanan tüm veri yollarında cihaz listesinde bir sonraki cihazın işaretçisi.
- **ux_device_descriptor:** USB cihaz tanımlayıcısı.
- **ux_device_control_endpoint:** Bu cihaz tarafından kullanılan varsayılan denetim uç noktasının tanımlayıcısı.
- **ux_device_hub_tt:** Cihaz için Hub TT dizisi

### <a name="configuration-descriptors"></a>Yapılandırma Tanımlayıcıları

Yapılandırma tanımlayıcısı belirli bir cihaz yapılandırmasıyla ilgili bilgileri açıklar. USB cihazı bir veya daha fazla yapılandırma tanımlayıcısı içerebilir. Cihaz **tanımlayıcısının bNumConfigurations** alanı, yapılandırma tanımlayıcılarının sayısını gösterir. Tanımlayıcı, YapılandırmaYı Ayarla isteği için parametre olarak kullanıldığında cihazın açıklanan yapılandırmayı varsaymalarını neden olan bir değere sahip **bir bConfigurationValue** alanı içerir.

Tanımlayıcı, yapılandırma tarafından sağlanan arabirim sayısını açıklar. Her arabirim, cihaz içindeki bir mantıksal işlevi temsil eder ve bağımsız olarak çalışabilir. Örneğin, bir USB ses konuşmacısı biri ses akışı için, biri ses denetimi için ve biri konuşmacının düğmelerini yönetmek için bir ADET USB arabirimi olmak kaydıyla üç arabirime sahip olabilir.

Konak yapılandırma tanımlayıcısı GET_DESCRIPTOR bir istek oluşturduğunda, tüm ilgili arabirim ve uç nokta tanımlayıcıları döndürülür.

| Uzaklık | Alan               | Boyut | Değer    | Açıklama                       |
| ------ | ------------------- | ---- | -------- | --------------------------------- |
| 0      | bLength             | 1    | Sayı   | Bu tanımlayıcının bayt cinsinden boyutu. |
| 1      | bDescriptorType     | 1    | Sabit | YAPILANDIRMA                     |
| 2      | wTotalLength        | 2    | Sayı   | Bu yapılandırma için döndürülen verilerin toplam uzunluğu. Bu yapılandırma için döndürülen tüm tanımlayıcıların (yapılandırma, arabirim, uç nokta ve sınıfa veya satıcıya özgü) birleşik uzunluğunu içerir. |
| 4      | bNumInterfaces      | 1    | Sayı   | Bu yapılandırma tarafından desteklenen arabirimlerin sayısı. |
| 5      | bConfigurationValue | 1    | Sayı   | Ayarlanacak bir bağımsız değişken olarak kullanılacak değer<br/>Bu yapılandırmayı seçmek için yapılandırma. |
| 6      | Yapılandırma      | 1    | Dizin oluşturma    | Bu yapılandırmayı açıklayan dize tanımlayıcısının dizini. |
| 7      | bMAttributes        | 1    | Biteş   | Yapılandırma özellikleri D7 Bus destekleniyor<br />D6 otomatik olarak destekleniyor<br />D5 uzaktan uyandırma<br />D4.. 0 ayrılmış (0 ' a sıfırlayın)<br />Veri yolundan ve yerel bir kaynaktan güç kullanan bir cihaz yapılandırması hem D7 hem de D6 ayarlar. Çalışma zamanında gerçek güç kaynağı, durumu Al cihaz isteği kullanılarak belirlenebilir.<br />Bir cihaz yapılandırması uzaktan uyandırma 'yi destekliyorsa, D5 1 olarak ayarlanır. |
| 8      | MaxPower            | 1    | Hareketli       | Cihaz tam olarak çalışırken bu belirli yapılandırmadaki veri yolundan USB cihazının maksimum güç tüketimi.<br />2 mA biriminde ifade edilir (örneğin, 50 = 100 mA).<br />Note: bir cihaz yapılandırması, yapılandırmanın veri yolundan veya şirket içinde açık olup olmadığını bildiriyor.<br />Cihaz durumu, cihazın Şu anda kendi kendine açık olup olmadığını bildiriyor. Bir cihazın dış güç kaynağıyla bağlantısı kesilirse, cihazın artık kendi kendine açık olmadığını belirtmek için cihaz durumunu güncelleştirir. |

USBX, bir USB yapılandırma tanımlayıcısını aşağıdaki şekilde tanımlar.

```c
typedef struct UX_CONFIGURATION_DESCRIPTOR_STRUCT
{
    UINT bLength;
    UINT bDescriptorType;
    USHORT wTotalLength;
    UINT bNumInterfaces;
    UINT bConfigurationValue;
    UINT iConfiguration;
    UINT bmAttributes;
    UINT MaxPower;
} UX_CONFIGURATION_DESCRIPTOR;
```

USB yapılandırma tanımlayıcısı aşağıda gösterildiği gibi açıklanan bir yapılandırma kapsayıcısının bir parçasıdır.

```c
typedef struct UX_CONFIGURATION_STRUCT
{
    ULONG ux_configuration_handle;
    ULONG ux_configuration_state;
    struct UX_CONFIGURATION_DESCRIPTOR_STRUCT ux_configuration_descriptor;
    struct UX_INTERFACE_STRUCT *ux_configuration_first_interface;
    struct UX_CONFIGURATION_STRUCT *ux_configuration_next_configuration;
    struct UX_DEVICE_STRUCT *ux_configuration_device;
} UX_CONFIGURATION;
```

- **ux_configuration_handle**: yapılandırmanın tanıtıcısı. Bu, genellikle yapılandırma için bu yapının örneğinin adresidir.
- **ux_configuration_state**: yapılandırmanın durumu.
- **ux_configuration_descriptor**: USB cihaz tanımlayıcısı.
- **ux_configuration_first_interface**: Bu yapılandırma için ilk arabirime yönelik işaretçi.
- **ux_configuration_next_configuration**: aynı cihaz için bir sonraki yapılandırmaya yönelik işaretçi.
- **ux_configuration_device**: Bu yapılandırmanın cihaz sahibine yönelik işaretçi.

### <a name="interface-descriptors"></a>Arabirim tanımlayıcıları

Arabirim tanımlayıcısı, bir yapılandırma içindeki belirli bir arabirimi tanımlar. Arabirim, USB cihazındaki mantıksal bir işlevdir. Yapılandırma, yapılandırma içindeki benzersiz bir uç nokta kümesini açıklayan bir veya daha fazla uç nokta tanımlayıcısı olan bir veya daha fazla arabirim sağlar. Bir yapılandırma birden fazla arabirimi desteklediğinde, belirli bir arabirim için uç nokta tanımlayıcıları, belirtilen yapılandırma için **GET_DESCRIPTOR** isteği tarafından döndürülen verilerdeki arabirim tanımlayıcısını izler.

Bir arabirim tanımlayıcısı her zaman bir yapılandırma tanımlayıcısının parçası olarak döndürülür. Arabirim tanımlayıcısı bir GET_DESCRIPTOR isteği tarafından doğrudan erişilemez.

Bir arabirim, uç noktaların ve/veya özelliklerinin cihaz yapılandırıldıktan sonra bulunmasına izin veren alternatif ayarlar içerebilir. Bir arabirim için varsayılan ayar her zaman sıfır ayarı olarak ayarlanır. Bir sınıf, arabirim davranışını ve ilişkili uç noktaların özelliklerini değiştirmek için geçerli alternatif ayarı değiştirmeyi seçebilir. SET_INTERFACE isteği, alternatif bir ayar seçmek veya varsayılan ayara dönmek için kullanılır.

Alternatif ayarlar, diğer arabirimler işlem sırasında kaldığı sürece cihaz yapılandırmasının bir kısmının değiştirilebilir olmasını sağlar. Bir yapılandırmanın bir veya daha fazla arabirimi için alternatif ayarları varsa, her ayara ayrı bir arabirim tanımlayıcısı ve ilişkili uç noktaları dahildir.

Bir cihaz yapılandırmasında iki alternatif ayar içeren tek bir arabirim varsa, yapılandırma için GET_DESCRIPTOR isteği yapılandırma tanımlayıcısını döndürür, ardından **Bfacenumber** ve **balternatesetting** alanları sıfır olarak ayarlanmış arabirim tanımlayıcısı, bu ayar için uç nokta tanımlayıcılarını ve ardından başka bir arabirim tanımlayıcısı ve ilgili uç nokta tanımlayıcılarını izler. İkinci arabirim tanımlayıcısının **Bınterfacenumber** alanı da sıfır olarak ayarlanır, ancak ikinci arabirim tanımlayıcısının **balternatesetting** alanı, bu alternatif ayarın ilk arabirime ait olduğunu gösteren 1 olarak ayarlanır.

Bir arabirimin kendisiyle ilişkili uç noktası olamaz, bu durumda yalnızca varsayılan denetim uç noktası bu arabirim için geçerlidir.

Diğer ayarlar temel olarak arabirimle ilişkili düzenli uç noktalar için istenen bant genişliğini değiştirmek için kullanılır. Örneğin, bir USB konuşmacı akış arabirimi, zaman aralıklı uç noktasında 0 bant genişliği talebi olan ilk alternatif ayara sahip olmalıdır. Diğer alternatif ayarlar, ses akış sıklığına bağlı olarak farklı bant genişliği gereksinimleri seçebilir.

Arabirimin USB tanımlayıcısı aşağıdaki gibidir:

| Uzaklık | Alan              | Boyut | Değer     | CI                              |
| ------ | ------------------ | ---- | --------- | --------------------------------------- |
| 0      | bLength            | 1    | Sayı    | Bu tanımlayıcının bayt cinsinden boyutu.       |
| 1      | bDescriptorType    | 1    | Sabit  | ARABIRIM tanımlayıcı türü               |
| 2      | Bfacenumber   | 1    | Sayı    | Arabirim sayısı. Bu yapılandırma tarafından desteklenen eşzamanlı arabirimlerin dizisindeki dizini tanımlayan sıfır tabanlı değer. |
| 3      | bAltenateSetting   | 1    | Sayı    | Önceki alanda tanımlanan arabirim için alternatif ayarı seçmek için kullanılan değer. |
| 4      | bNumEndpoints      | 1    | Sayı    | Bu arabirim tarafından kullanılan uç nokta sayısı (uç nokta sıfır hariç). Bu değer 0 ise, bu arabirim yalnızca bir uç nokta sıfır kullanır. |
| 5      | bInterfaceClass    | 1    | Sınıf     | Sınıf kodu (USB tarafından atanan)<br />Bu alan 0 olarak sıfırlandığında arabirim, USB tarafından belirtilen herhangi bir cihaz sınıfına ait değildir.<br />Bu alan 0xFF olarak ayarlanırsa, arabirim sınıfı satıcıya özeldir.<br />Diğer tüm değerler USB tarafından atanmak üzere ayrılmıştır. |
| 6      | Bınterfacesubclass | 1    | Alt  | Alt sınıf kodu (USB tarafından atanır).<br />Bu kodlar bInterfaceClass alanı değerine göre niteliklidir. bInterfaceClass alanı 0'a sıfırlanırsa, bu alan da 0'a sıfırlanır. bInterfaceClass alanı varsayılan olarak 0xFF tüm değerler USB tarafından atama için ayrılmıştır. |
| 7      | bInterfaceProtocol | 1    | Protokol  | Protokol kodu (USB tarafından atanır). Bu kodlar bInterfaceClass ve bInterfaceSubClass alanlarının değerine göre niteliklidir. Arabirim sınıfa özgü istekleri destekliyorsa, bu kod cihazın kullandığı protokolleri cihaz sınıfının belirtimleri tarafından tanımlandığı şekilde tanımlar.<br />Bu alan 0'a sıfırlanırsa, cihaz bu arabirimde sınıfa özgü bir protokol kullanmaz. Bu alan varsayılan olarak 0xFF cihaz, bu arabirim için satıcıya özgü bir protokol kullanır. |
| 8      | ıınterface         | 1    | Dizin oluşturma     | Bu arabirimi açıklayan dize tanımlayıcısı dizini. |

USBX, bir USB arabirimi tanımlayıcısını aşağıdaki gibi tanımlar.

```c
typedef struct UX_INTERFACE_DESCRIPTOR_STRUCT
{
    UINT bLength;
    UINT bDescriptorType;
    UINT bInterfaceNumber;
    UINT bAlternateSetting;
    UINT bNumEndpoints;
    UINT bInterfaceClass
    UINT bInterfaceSubClass;
    UINT bInterfaceProtocol;
    UINT iInterface;
} UX_INTERFACE_DESCRIPTOR;
```

USB arabirim tanımlayıcısı, aşağıdaki şekilde açıklanan bir arabirim kapsayıcısı kapsamındadır.

```c
typedef struct UX_INTERFACE_STRUCT
{
    ULONG ux_interface_handle;
    ULONG ux_interface_state;
    ULONG ux_interface_current_alternate_setting;
    struct UX_INTERFACE_DESCRIPTOR_STRUCT ux_interface_descriptor;
    struct UX_HOST_CLASS_STRUCT    *ux_interface_class;
    VOID    *ux_interface_class_instance;
    struct UX_ENDPOINT_STRUCT    *ux_interface_first_endpoint;
    struct UX_INTERFACE_STRUCT    *ux_interface_next_interface;
    struct UX_CONFIGURATION_STRUCT    *ux_interface_configuration;
} UX_INTERFACE;
```

- **ux_interface_handle:** Arabirimin tanıtıcısı. Bu genellikle arabirim için bu yapı örneğinin adresidir.
- **ux_interface_state:** Arabirimin durumu.
- **ux_interface_descriptor:** USB arabirim tanımlayıcısı.
- **ux_interface_class:** Bu arabirime sahip olan sınıf türünün işaretçisi.
- **ux_interface_class_instance:** Bu arabirime sahip olan sınıfın örneğine işaretçi.
- **ux_interface_first_endpoint:** Bu arabirimle kaydedilen ilk uç noktanın işaretçisi.
- **ux_interface_next_interface:** Yapılandırmayla ilişkili sonraki arabirimin işaretçisi.
- **ux_interface_configuration:** Bu arabirimin yapılandırma sahibine işaretçi.

### <a name="endpoint-descriptors"></a>Uç Nokta Tanımlayıcıları

Bir arabirimle ilişkili her uç noktanın kendi uç nokta tanımlayıcısı vardır. Bu tanımlayıcı, her uç noktanın bant genişliği gereksinimlerini, uç noktayla ilişkili maksimum yükü, periyodikliğini ve yönünü belirlemek için konak yığını için gereken bilgileri içerir. Uç nokta tanımlayıcısı her zaman yapılandırma için bir GET_DESCRIPTOR komutu tarafından döndürülür.

Cihaz tanımlayıcısıyla ilişkili varsayılan denetim uç noktası, arabirimle ilişkili uç noktaların parçası olarak sayılmaz ve bu nedenle bu tanımlayıcıda döndürülz.

Konak yazılımı bir arabirim için alternatif ayarda değişiklik isteğinde olduğunda, ilişkili tüm uç noktalar ve USB kaynakları yeni alternatif ayara göre değiştirilir.

Varsayılan denetim uç noktaları dışında uç noktalar arabirimler arasında paylaşamaz.

| Uzaklık | Alan            | Boyut | Değer    | Açıklama                       |
| ------ | ---------------- | ---- | -------- | --------------------------------- |
| 0      | bLength          | 1    | Sayı   | Bu tanımlayıcının bayt cinsinden boyutu. |
| 1      | bDescriptorType  | 1    | Sabit | ENDPOINT Tanımlayıcı Türü. |
| 2      | bEndpointAddress | 1    | Uç Nokta | Bu tanımlayıcı tarafından açıklanan USB cihazında uç noktanın adresi. Adres aşağıdaki gibi kodlanmıştır:<br />Bit 3...0: Uç nokta numarası<br />Bit 6...4: Ayrılmış, sıfıra sıfırla<br />Bit 7: Denetim uç noktaları için yoksayılan yön<br />0 = OUT uç noktası<br />1 = IN uç noktası |
| 3      | bmAttributes     | 1    | Bitmap   | Bu alan, **bConfigurationValue** alanı kullanılarak yapılandırıldığında uç noktanın özniteliklerini açıklar. Bit 1..0: Aktarım Türü<br />00 = Denetim<br />01 = Isochronous<br />10 = Toplu<br />11 = Kesinti<br />Bir zaman uyumsuz uç nokta yoksa, bit 5..2 ayrılmıştır ve sıfır olarak ayarlanır. isochronous ise, bunlar aşağıdaki gibi tanımlanır:<br />Bit 3..2: Eşitleme Türü<br />00 = Eşitleme Yok<br />01 = Zaman Uyumsuz<br />10 = Uyarlamalı<br />11 = Zaman Uyumlu<br />Bit 5..4: Kullanım Türü<br />00 = Veri uç noktası<br />01 = Geri bildirim uç noktası<br />10 = Örtülü geri bildirim veri uç noktası<br />11 = Ayrılmış |
| 4      | wMaxPacketSize   | 2    | Sayı   | Bu uç noktanın bu yapılandırma seçildiğinde gönderebilecek veya alabilen maksimum paket boyutu.<br />Zaman uyumsuz uç noktalar için bu değer, veri verisi sürelerini zaman çizelgesinde (per-(micro)frame veri yüklerinin gerekli olduğu şekilde, zaman çizelgesinde rezervasyon yapmak için kullanılır. Kanal, sürekli olarak ayrılandan daha az bant genişliği kullanabilir. Cihaz, gerekirse normal, USB olmayan tanımlı mekanizmalar aracılığıyla kullanılan gerçek bant genişliğini raporlar.<br />Tüm uç noktalar için bit 10..0, en büyük paket boyutunu (bayt cinsinden) belirtir.<br />Yüksek hızlı zaman uyumsuz ve kesme uç noktaları için:<br />Bit 12...11 mikro çerçeve başına ek işlem fırsatı sayısını belirtir: 00 = Yok (mikro çerçeve başına 1 işlem)<br />01 = 1 ek (mikro çerçeve başına 2)<br />10 = 2 ek (mikro çerçeve başına 3)<br />11 = Ayrılmış<br />Bit 15..13 ayrılmıştır ve sıfır olarak ayarlanır. |
| 6      | Bınterval        | 1     | Sayı   | Veri aktarımları için yoklama uç noktası için sayı aralığı.<br />Cihaz işletim hızına (yani, 1 milisaniyelik veya 125 μs birimi) bağlı olarak çerçeveler veya mikro çerçeveler olarak ifade edilir.<br />Tam/üst aralıklı zaman aralıklı uç noktalar için bu değer 1 ile 16 arasında olmalıdır. **Bınterval** , 2bınterval-1 değerinin üs değeri olarak kullanılır; Örneğin, bir **Bınterval** 4, 8 (24-1) süresini gösterir.<br />Tam/Low-Speed kesme uç noktaları için bu alanın değeri 1 ile 255 arasında olabilir.<br />Yüksek hızlı kesme uç noktaları için **Bınterval** , bir 2bınterval-1 değeri için üs olarak kullanılır; Örneğin, bir **Bınterval** 4, 8 (24-1) süresini gösterir. Bu değer 1 ile 16 arasında olmalıdır.<br />Yüksek hızda toplu/denetim noktaları için **Bınterval** , uç noktanın en fazla nak oranını belirtir. 0 değeri, uç noktayı hiçbir şekilde gösterir. Diğer değerler, her bir **bin** mikro kare için en fazla bir nak gösterir.<br />Bu değer 0 ile 255 arasında olmalıdır. |

USBX, bir USB uç nokta tanımlayıcısını aşağıdaki şekilde tanımlar:

```c
typedef struct UX_ENDPOINT_DESCRIPTOR_STRUCT
{
    UINT bLength;
    UINT bDescriptorType;
    UINT bEndpointAddress;
    UINT bmAttributes;
    USHORT wMaxPacketSize;
    UINT bInterval;
} UX_ENDPOINT_DESCRIPTOR;
```

USB uç nokta tanımlayıcısı, aşağıdaki gibi açıklanan bir uç nokta kapsayıcısının parçasıdır.

```c
typedef struct UX_ENDPOINT_STRUCT {
    ULONG    ux_endpoint_handle;
    ULONG    ux_endpoint_state;
    VOID    *ux_endpoint_ed;
    struct UX_ENDPOINT_DESCRIPTOR_STRUCT    ux_endpoint_descriptor;
    struct UX_ENDPOINT_STRUCT    *ux_endpoint_next_endpoint;
    struct UX_INTERFACE_STRUCT    *ux_endpoint_interface;
    struct UX_DEVICE_STRUCT    *ux_endpoint_device;
    struct UX_TRANSFER REQUEST_STRUCT    ux_endpoint_transfer request;
} UX_ENDPOINT;

```

- **ux_endpoint_handle**: uç noktanın tanıtıcısı. Bu, genellikle uç nokta için bu yapının örneğinin adresidir.
- **ux_endpoint_state**: uç noktanın durumu.
- **ux_endpoint_ed**: konak denetleyicisi katmanında fiziksel uç noktaya işaretçi.
- **ux_endpoint_descriptor**: USB uç nokta tanımlayıcısı.
- **ux_endpoint_next_endpoint**: aynı arabirime ait olan bir sonraki uç noktaya işaretçi.
- **ux_endpoint_interface**: Bu uç nokta arabirimine sahip olan arabirime yönelik işaretçi.
- **ux_endpoint_device**: ana cihaz kapsayıcısının işaretçisi.
- **ux_endpoint_transfer isteği**: cihazdan/cihazdan veri göndermek/almak için kullanılan USB aktarım isteği.

### <a name="string-descriptors"></a>Dize tanımlayıcıları

Dize tanımlayıcıları isteğe bağlıdır. Bir cihaz dize tanımlayıcılarını desteklemiyorsa, cihaz, yapılandırma ve arabirim tanımlayıcılarının içindeki dize tanımlayıcılarının tüm başvuruları sıfıra sıfırlanmalıdır.

Dize tanımlayıcıları UNICODE kodlaması kullanır ve bu sayede birkaç karakter kümesi desteğine izin verir. Bir USB cihazdaki dizeler birden çok dili destekleyebilir. Bir dize tanımlayıcısı istenirken, istek sahibi istenen dili USB-IF tarafından tanımlanan bir dil KIMLIĞI kullanarak belirtir. Şu anda tanımlı USB LangID listesi, USBX ekinde bulunabilir??.
Tüm diller için dize dizini sıfır, cihaz tarafından desteklenen iki baytlık bir GID kodlarından oluşan bir diziyi içeren bir dize tanımlayıcısı döndürür. UNICODE dizesinin 0 sonlandırılmadığından not edilmelidir. Bunun yerine, dize dizisinin boyutu, tanımlayıcının ilk baytında bulunan dizinin boyutundan iki çıkartılacak şekilde hesaplanır.

USB dize tanımlayıcısı 0, aşağıdaki gibi kodlanır.

| Uzaklık | Alan           | Boyut | Değer    | Açıklama                      |
| ------ | --------------- | ---- | -------- | -------------------------------- |
| 0      | bLength         | 1    | N + 2      | Bu tanımlayıcının bayt cinsinden boyutu |
| 1      | bDescriptorType | 1    | Sabit | DIZE tanımlayıcı türü           |
| 2      | wLANGID [0]      | 2    | Sayı   | LANGıD kodu 0                    |
| ...    | ...]            | ...  | ...      | ...                              |
| N      | wLANGID [n]      | 2    | Sayı   | LANGıD kodu n                    |

Diğer USB dize tanımlayıcıları aşağıdaki şekilde kodlanır.

| Uzaklık | Alan           | Boyut | Değer    | Açıklama                      |
| ------ | --------------- | ---- | -------- | -------------------------------- |
| 0      | bLength         | 1    | Sayı   | Bu tanımlayıcının bayt cinsinden boyutu |
| 1      | bDescriptorType | 1    | Sabit | DIZE tanımlayıcı türü           |
| 2      | bString         | n    | Sayı   | UNICODE kodlamalı dize           |

USBX, sıfır olmayan uzunlukta bir USB dize tanımlayıcısını aşağıdaki şekilde tanımlar:

```c
typedef struct UX_STRING_DESCRIPTOR_STRUCT
{
    UINT bLength;
    UINT bDescriptorType;
    USHORT bString[1];
} UX_STRING_DESCRIPTOR;
```

### <a name="functional-descriptors"></a>İşlevsel tanımlayıcılar

İşlevsel tanımlayıcılar, sınıfa özgü tanımlayıcılar olarak da bilinir. Normalde genel tanımlayıcılarla aynı temel yapıları kullanır ve ek bilgilerin sınıf tarafından kullanılabilmesini sağlar. Örneğin, USB ses hoparlörü söz konusu olduğunda, sınıfa özgü tanımlayıcılar, desteklenen ses frekansı türünün her alternatif ayarı için ses sınıfının almasına izin verir.

### <a name="usbx-device-descriptor-framework-in-memory"></a>Bellek içinde USBX cihaz tanımlayıcısı çerçevesi

USBX, bellek ve işlev tanımlayıcıları hariç tüm tanımlayıcılara sahip olan tüm cihaz tanımlayıcılarını tutar. Aşağıdaki diyagramda bu tanımlayıcılarının nasıl depolandığı ve ilişkili olduğu gösterilmektedir.

![Bellek içinde USBX cihaz tanımlayıcısı çerçevesi](./media/usbx-host-stack/usbx-device-descriptor-framework.png)
