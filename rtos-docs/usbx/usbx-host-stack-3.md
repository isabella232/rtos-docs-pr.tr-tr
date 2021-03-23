---
title: Bölüm 3-USBX konak yığınının Işlevsel bileşenleri
description: Bu bölümde, işlevsel bir perspektiften yüksek performanslı USBX Embedded USB konak yığınının açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 17b8d884dd2c71d60e91f5fcec40c360060f4fe8
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104828367"
---
# <a name="chapter-3---functional-components-of-usbx-host-stack"></a>Bölüm 3-USBX konak yığınının Işlevsel bileşenleri

Bu bölümde, işlevsel bir perspektiften yüksek performanslı USBX Embedded USB konak yığınının açıklaması yer almaktadır.

## <a name="execution-overview"></a>Yürütmeye genel bakış

USBX çeşitli bileşenlerden oluşur:

- Başlatma
- Uygulama arabirimi çağrıları
- Kök hub
- Hub sınıfı
- Konak sınıfları
- USB ana bilgisayar yığını
- Ana bilgisayar denetleyicisi

Aşağıdaki diyagramda, USBX konak yığını gösterilmektedir.

![USBX konak yığını](./media/usbx-host-stack/usbx-host-stack.png)

### <a name="initialization"></a>Başlatma

USBX ' i etkinleştirmek için ***ux_system_initialize*** işlevi çağrılmalıdır. Bu işlev, USBX bellek kaynaklarını başlatır.

USBX konak tesislerini etkinleştirmek için ***ux_host_stack_initialize*** işlevi çağrılmalıdır. Bu işlev, Işparçacığıx iş parçacıkları, zaman uyumu sağlayıcılar ve semaforlar gibi USBX konak yığını tarafından kullanılan tüm kaynakları başlatacak.

En az bir USB ana bilgisayar denetleyicisi ve bir veya daha fazla USB sınıfı etkinleştirmek için uygulama başlatması en iyisidir. Sınıflar yığına kaydedildiğinde ve konak denetleyicisi (ler) başlatma işlevi veri yolu etkin ve cihaz bulma başlayabilir. Ana bilgisayar denetleyicisinin kök hub 'ı eklenmiş bir cihaz algılarsa, USB topolojisi ücretlendirilmesi halinde USB numaralandırma iş parçacığı uyanma ve cihaz (ler) i numaralandırmaya devam edecektir.

Kök hub ve aşağı akış hub 'larının doğası gereği, ana bilgisayar denetleyicisi başlatma işlevi döndürüldüğünde bağlı olan tüm USB cihazlarının tamamen yapılandırılamamasından kaynaklanabilir. Özellikle kök hub ve USB cihazları arasında bir veya daha fazla hub varsa, tüm USB cihazlarının numaralandırılması birkaç saniye sürebilir.

### <a name="application-interface-calls"></a>Uygulama arabirimi çağrıları

USBX içinde iki API düzeyi vardır.

- USB ana bilgisayar yığını API 'Leri
- USB ana bilgisayar sınıfı API 'Leri

Normalde, bir USBX uygulamasının USB ana bilgisayar yığını API işlevlerinden herhangi birini çağırması gerekmez. Çoğu uygulama yalnızca USB sınıfı API işlevlerine erişir.

### <a name="usb-host-stack-apis"></a>USB ana bilgisayar yığını API 'Leri

Ana bilgisayar yığını API 'SI işlevleri, USBX bileşenlerinin (konak sınıfları ve ana bilgisayar denetleyicileri), cihazların yapılandırmasının ve kullanılabilir cihaz uç noktaları için aktarım isteklerinin işlenmesinden sorumludur.

### <a name="usb-host-class-api"></a>USB ana bilgisayar sınıfı API 'SI

Sınıf API 'Leri her USB sınıfına çok özeldir. USB sınıflarının ortak API işlevlerinin çoğu, bir cihazı açma/kapatma ve bir cihazdan okuma ve bir cihaza yazma gibi hizmetler sağlar.

### <a name="root-hub"></a>Kök hub

Her konak denetleyicisi örneğinde bir veya daha fazla USB kök hub vardır. Kök hub sayısı denetleyicinin doğası gereği belirlenir ya da denetleyiciden belirli Yazmaçları okuyarak alınabilir.

### <a name="hub-class"></a>Hub sınıfı

Hub sınıfı, USB hub 'larını çalıştırırken ücretsizdir. USB hub 'ı tek başına bir hub veya klavye ya da izleyici gibi bileşik bir cihazın parçası olabilir. Hub, kendi gücünü veya veri yolundan güç olabilir. Veri yolu ile desteklenen hub 'lar en fazla dört aşağı akış bağlantı noktasına sahiptir ve yalnızca, 100 ' den az güç kullanan, yalnızca kendi güç destekli veya veri yolundan destekli cihazların bağlanmasına izin verebilir. Hub 'lar basamaklı olabilir. Beş adede kadar hub birbirine bağlanabilir.

### <a name="usb-host-stack"></a>USB ana bilgisayar yığını

USB ana bilgisayar yığını, USBX 'in Merkez parçasıdır. Üç ana işleve sahiptir.

- USB 'nin topolojisini yönetin.
- Bir USB cihazını bir veya daha fazla sınıfa bağlayın.
- Cihaz tanımlayıcısı ve USB aktarımları gerçekleştirmek için sınıflara bir API sağlayın.

### <a name="topology-manager"></a>Topoloji Yöneticisi

USB yığını topolojisi iş parçacığı, yeni bir cihaz bağlandığında veya bir cihazın bağlantısı kesildiğinde başlatılabilmesi uyandırılır. Kök hub veya normal Hub cihaz bağlantılarını kabul edebilir. Bir cihaz USB 'ye bağlandıktan sonra, topoloji Yöneticisi cihaz tanımlayıcısını alır. Bu tanımlayıcı, bu cihaz için kullanılabilir olası yapılandırmaların sayısını içerir. Çoğu cihazda yalnızca bir yapılandırma vardır. Bazı cihazlar, bağlandığı bağlantı noktasında kullanılabilir olan güce göre farklı şekilde çalışabilir. Bu durumda, cihazın kullanılabilir güce göre seçilebilirler birden fazla yapılandırması olacaktır. Cihaz topoloji Yöneticisi tarafından yapılandırıldığında, daha sonra yapılandırma tanımlayıcısında belirtilen güç miktarını çizmeye izin verilir.

## <a name="usb-class-binding"></a>USB sınıfı bağlama

Cihaz yapılandırıldığında, topoloji Yöneticisi sınıf yöneticisinin cihaz bulma işlemini cihaz arabirimi tanımlayıcılarına bakarak devam etmesine izin verir. Bir cihazda bir veya daha fazla arabirim tanımlayıcısı olabilir.

Arabirim bir cihazdaki işlevi temsil eder. Örneğin, bir USB konuşmacının, biri ses akışı, biri ses denetimi için ve diğeri de çeşitli konuşmacı düğmelerini yönetmek için üç arabirimi vardır.

Sınıf Yöneticisi, cihaz arabirimini bir veya daha fazla sınıfa katmak için iki mekanizma içerir. Arabirim tanımlayıcısında bulunan bir PID/VıD (ürün KIMLIĞI ve satıcı KIMLIĞI) bileşimini ya da sınıf/alt sınıf/protokol birleşimini kullanabilir.

PID/VıD birleşimi, genel bir sınıf tarafından yönlendirilmeyen arabirimler için geçerlidir. Sınıf/alt sınıf/protokol birleşimi, bir yazıcı, hub, depolama, ses veya HID gibi bir USB-IF sertifikalı sınıfa ait arabirimler tarafından kullanılır.

Sınıf Yöneticisi, USBX ' in başlatılmasından kayıtlı sınıfların bir listesini içerir. Sınıf Yöneticisi her bir sınıfı, bir sınıf için arabirimi yönetmek için kabul edene kadar her bir sınıfa çağırır. Bir sınıf yalnızca bir arabirimi yönetebilir. USB ses konuşmacının örneği için, sınıf Yöneticisi arabirimlerin her biri için tüm sınıfları çağırır.

Bir sınıf bir arabirimi kabul ettiğinde, bu sınıfın yeni bir örneği oluşturulur. Sınıf Yöneticisi daha sonra arabirim için varsayılan alternatif ayarı arar. Bir cihazın her arabirim için bir veya daha fazla alternatif ayarı olabilir. 0 alternatif ayarı, bir sınıf bunu değiştirmeye karar verdiğinde varsayılan olarak kullanılan ' i olacaktır.

Varsayılan alternatif ayar için, sınıf Yöneticisi alternatif ayarda bulunan tüm uç noktaları bağlayacaktır. Her uç noktanın bağlanması başarılı olursa, sınıf Yöneticisi, arabirimin başlatılmasını tamamlayacaksınız sınıfına dönerek işini tamamlar.

### <a name="usbx-apis"></a>USBX API 'Leri

USB yığını, belirli uç noktalarda cihaz ve USB aktarımları için, USB sınıflarının belirli sayıda API 'sini dışa aktarır. Bu API işlevleri, bu başvuru el kitabında ayrıntılı olarak açıklanmıştır.

### <a name="host-controller"></a>Ana bilgisayar denetleyicisi

Ana bilgisayar denetleyicisi sürücüsü, belirli bir USB denetleyicisi türünü yönlendirmekten sorumludur. Bir USB ana bilgisayar denetleyicisinin içinde birden çok denetleyicisi olabilir. Örneğin, belirli Intel PC yonga seti iki UCı denetleyicisi içerir. Bazı USB 2,0 denetleyicileri, bir EHCı denetleyicisi 'nin bir örneğine ek olarak bir OHCı denetleyicinin birden çok örneğini içerir.

Konak denetleyicisi yalnızca aynı denetleyicinin birden fazla örneğini yönetir. Çoğu USB 2,0 ana bilgisayar denetleyicisini barındırmak için, USBX 'in başlatılması sırasında OÇI denetleyicisini ve EHCı denetleyiciyi başlatmak gerekecektir.

Ana bilgisayar denetleyicisi aşağıdakileri yönetmekten sorumludur.

- Kök hub
- Güç Yönetimi
- Uç Noktalar
- Girişinde

### <a name="root-hub"></a>Kök hub

Kök hub yönetimi, her denetleyici bağlantı noktasının kapatılmasından ve takılı bir cihazın olup olmadığını belirlemekten sorumludur. Bu işlevsellik, denetleyici aşağı akış bağlantı noktalarını sorgulanamıyor için USBX genel kök hub 'ı tarafından kullanılır.

### <a name="power-management"></a>Güç Yönetimi

Güç yönetimi işleme, Gang modunda askıya alma/sürdürme sinyallerinin işlenmesini sağlar, bu nedenle tüm denetleyici aşağı akış bağlantı noktalarını aynı anda veya denetleyici bu işlevselliği sunuyorsa tek tek ayrı ayrı etkiliyor olabilir.

### <a name="endpoints"></a>Uç Noktalar

Uç nokta yönetimi, denetleyiciye fiziksel uç noktaların oluşturulması veya yok edilmesi için sağlar. Fiziksel uç noktalar, denetleyici ana DMA 'Yı destekliyorsa veya denetleyiciye yazılmışsa, denetleyici tarafından Ayrıştırılan bellek varlıklarıdır. Fiziksel uç noktalar, denetleyici tarafından gerçekleştirilecek işlem bilgilerini içerir.

### <a name="transfers"></a>Girişinde

Aktarım yönetimi, oluşturulan her uç nokta üzerinde işlem gerçekleştirmek için bir sınıf sağlar. Her mantıksal uç nokta, USB aktarım istekleri için aktarım ISTEğI adlı bir bileşen içerir. Aktarım ISTEğI, işlemi betimleyen yığın tarafından kullanılır. Bu aktarım ISTEğI daha sonra yığına ve denetleyiciye geçirilir, bu da denetleyicinin özelliklerine bağlı olarak onu birkaç alt işleme bölebilir.

## <a name="usb-device-framework"></a>USB cihaz çerçevesi

Bir USB cihaz, bir tanımlayıcı ağacı tarafından temsil edilir. Altı temel tanımlayıcı türü vardır.

- Cihaz tanımlayıcıları
- Yapılandırma tanımlayıcıları
- Arabirim tanımlayıcıları
- Uç nokta tanımlayıcıları
- Dize tanımlayıcıları
- İşlevsel tanımlayıcılar

USB cihazının çok basit bir açıklaması olabilir ve bu şekilde görünür.
![Basit USB cihaz](./media/usbx-host-stack/usb-device-simple.png)

Yukarıdaki çizimde, cihazın yalnızca bir yapılandırması vardır. Tek bir arabirim bu yapılandırmaya iliştirilir, bu da cihazın yalnızca bir işlevi olduğunu ve yalnızca bir uç nokta olduğunu gösterir. Cihaz tanımlayıcısına eklenmiş, cihazın görünür bir tanımlamasını sağlayan bir dize tanımlayıcısıdır.

Ancak, bir cihaz daha karmaşık olabilir ve aşağıdaki gibi görünebilir.

![Karmaşık USB cihaz](./media/usbx-host-stack/usb-device-complex.png)

Yukarıdaki çizimde, cihazın cihaz tanımlayıcısına bağlı iki yapılandırma tanımlayıcısı vardır. Bu cihaz, iki güç moduna sahip olduğunu veya standart sınıflar ya da özel sınıflar tarafından yönlendirilme gösterebilir.

İlk yapılandırmaya bağlı olarak iki arabirim vardır ve bu, cihazın iki mantıksal işleve sahip olduğunu gösterir. İlk işlevde 3 uç nokta tanımlayıcısı ve bir işlevsel tanımlayıcı bulunur. İşlevsel tanımlayıcı, bu arabirim hakkında normalde genel bir tanımlayıcı tarafından bulunmayan daha fazla bilgi edinmek için arabirimi sürücüden sorumlu sınıf tarafından kullanılabilir.

### <a name="device-descriptors"></a>Cihaz tanımlayıcıları

Her USB cihazının tek bir cihaz tanımlayıcısı vardır. Bu tanımlayıcı cihaz tanımlamasını, Desteklenen yapılandırmaların sayısını ve cihazı yapılandırmak için kullanılan varsayılan denetim uç noktasının özelliklerini içerir.

| Uzaklık | Alan              | Boyut | Değer    | Açıklama                             |
| ------ | ------------------ | ---- | -------- | --------------------------------------- |
| 0      | BLength            | 1    | Sayı   | Bu tanımlayıcının bayt cinsinden boyutu |
| 1      | bDescriptorType    | 1    | Sabit | CIHAZ tanımlayıcı türü |
| 2      | bcdUSB             | 2    | 'De      | BinaryCoded Dec içindeki USB belirtim Yayın numarası<br />Örnek: 2,10, 0x210 ' a eşdeğerdir. Bu alan, cihazın ve tanımlayıcılarının uyumlu olduğu USB belirtiminin sürümünü tanımlar. |
| 4      | bDeviceClass       | 1    | Sınıf    | Sınıf kodu (USB tarafından atanan).<br />Bu alan 0 olarak sıfırlandığında, bir yapılandırma içindeki her arabirim kendi sınıf bilgilerini belirtir ve çeşitli arabirimler bağımsız olarak çalışır.<br />Bu alan 1 ile 0xFE arasında bir değere ayarlanırsa, cihaz farklı arabirimlerde farklı sınıf belirtimlerini destekler ve arabirimler bağımsız olarak çalışmayabilir. Bu değer, toplam arabirimler için kullanılan sınıf tanımını tanımlar.<br />Bu alan 0xFF olarak ayarlandıysa, cihaz sınıfı satıcıya özeldir. |
| 5      | bDeviceSubClass    | 1    | Sınıf | Alt sınıf kodu (USB tarafından atanan).<br />Bu kodlar bDeviceClass alanının değeri ile nitelenir. BDeviceClass alanı 0 olarak sıfırlandığında, bu alan de 0 olarak sıfırlanmalıdır. BDeviceClass alanı 0xFF olarak ayarlanmamışsa, tüm değerler USB tarafından atanmak üzere ayrılmıştır. |
| 6      | bDeviceProtocol    | 1    | Protokol | Protokol kodu (USB tarafından atanan).<br />Bu kodlar bDeviceClass ve bDeviceSubClass alanlarının değeri ile nitelenir. Bir cihaz, bir cihaz temelinde sınıfa özgü protokolleri destekliyorsa, bu kod, cihazın cihaz sınıfının belirtimine göre tanımlandığı şekilde kullandığı protokolleri tanımlar. Bu alan 0 olarak sıfırlandığında, cihaz bir cihaz temelinde sınıfa özel protokoller kullanmaz.<br />Ancak, bir arabirim temelinde sınıfa özel protokoller kullanabilir.<br />Bu alan 0xFF olarak ayarlandıysa, cihaz bir cihaz temelinde satıcıya özgü protokol kullanır. |
| 7      | bMaxPacketSize0    | 1    | Sayı   | Uç nokta sıfırı için maksimum paket boyutu (yalnızca 8, 16, 32 veya 64 bayt boyutları geçerlidir) |
| 8      | ıdvendor           | 2    | ID       | Satıcı KIMLIĞI (USB tarafından atanan) |
| 10     | ıdproduct          | 2    | ID       | Ürün KIMLIĞI (üretici tarafından atanan) |
| 12     | bcdDevice          | 2    | 'De      | İkili kodlu ondalık olarak cihaz Yayın numarası |
| 14     | iManufacturer      | 1    | Dizin oluşturma    | Üreticiyi açıklayan dize tanımlayıcısının dizini |
| 15     | IProduct           | 1    | Dizin oluşturma    | Ürünü açıklayan dize tanımlayıcısının dizini |
| 16     | iSerialNumbe       | 1    | Dizin oluşturma    | Cihazın seri numarasını açıklayan dize tanımlayıcısının dizini |
| 17     | bNumConfigurations | 1    | Sayı   | Olası yapılandırmaların sayısı |

USBX, bir USB cihaz tanımlayıcısını aşağıdaki şekilde tanımlar:

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

USB cihaz tanımlayıcısı şu şekilde açıklanan bir cihaz kapsayıcısının parçasıdır:

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

- **ux_device_handle**: cihazın tanıtıcısı. Bu, genellikle cihaz için bu yapının örneğinin adresidir.
- **ux_device_type**: eski değer. Kullanılmıyor.
- **ux_device_state**: aşağıdaki değerlerden birine sahip olabilecek cihaz durumu:
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
- **ux_device_address**: **SET_ADDRESS** komutu kabul edildikten sonra cihazın adresi (1 ile 127 arasında).
- **ux_device_speed**: cihazın hızı:
    - **UX_LOW_SPEED_DEVICE**      0
    - **UX_FULL_SPEED_DEVICE**     1
    - **UX_HIGH_SPEED_DEVICE**     2
- **ux_device_port_location**: üst cihazın bağlantı noktasının dizini (kök hub veya hub).
- **ux_device_max_power**: en fazla güç, cihazın seçili yapılandırmada işlem gösterebilir.
- **ux_device_power_source**: aşağıdaki iki değerden biri olabilir:
    - **UX_DEVICE_BUS_POWERED**     1
    - **UX_DEVICE_SELF_POWERED**    2
- **ux_device_current_configuration**: Bu cihaz tarafından kullanılan geçerli yapılandırmanın dizini.
- **ux_device_parent**: Bu cihazın üst öğesinin cihaz kapsayıcı işaretçisi. İşaretçi null ise, üst öğe denetleyicinin kök hub 'üdür.
- **ux_device_class**: Bu cihazın sahibi olan sınıf türüne yönelik işaretçi.
- **ux_device_class_instance**: Bu cihaza sahip olan sınıfın örneğine yönelik işaretçi.
- **ux_device_hcd**: Bu cihazın eklendiği USB ana bilgisayar denetleyicisi örneği.
- **ux_device_first_configuration**: Bu cihaz için ilk Yapılandırma kapsayıcısına yönelik işaretçi.
- **ux_device_next_device**: USBX tarafından algılanan tüm veri yollarına cihaz listesinde sonraki cihaza yönelik işaretçi.
- **ux_device_descriptor**: USB cihaz tanımlayıcısı.
- **ux_device_control_endpoint**: Bu cihaz tarafından kullanılan varsayılan denetim uç noktasının tanımlayıcısı.
- **ux_device_hub_tt**: cihaz Için bir hub TTs dizisi

### <a name="configuration-descriptors"></a>Yapılandırma tanımlayıcıları

Yapılandırma tanımlayıcısı, belirli bir cihaz yapılandırmasıyla ilgili bilgileri açıklar. Bir USB cihaz, bir veya daha fazla yapılandırma tanımlayıcısı içerebilir. Cihaz tanımlayıcısındaki **Bnumconfigurations** alanı yapılandırma tanımlayıcılarının sayısını belirtir. Tanımlayıcı, ayarlanan yapılandırma isteğine parametre olarak kullanıldığında bir **Bconfigurationvalue** alanı içerir ve bu değer, küme yapılandırma isteğine parametre olarak kullanılır, cihazın açıklanan yapılandırmayı varsaymasına neden olur.

Tanımlayıcı, yapılandırma tarafından belirtilen arabirimlerin sayısını açıklar. Her arabirim, cihaz içindeki bir mantıksal işlevi temsil eder ve bağımsız olarak çalışmayabilir. Örneğin, bir USB ses konuşmacının, biri ses akışı, biri ses denetimi için bir tane olmak üzere üç arabirimi ve konuşmacı düğmelerini yönetmek için bir HID arabirimi olabilir.

Ana bilgisayar yapılandırma tanımlayıcısı için GET_DESCRIPTOR isteği yayınlar, tüm ilgili arabirim ve uç nokta tanımlayıcıları döndürülür.

| Uzaklık | Alan               | Boyut | Değer    | Açıklama                       |
| ------ | ------------------- | ---- | -------- | --------------------------------- |
| 0      | bLength             | 1    | Sayı   | Bu tanımlayıcının bayt cinsinden boyutu. |
| 1      | bDescriptorType     | 1    | Sabit | YAPILANDIRMA                     |
| 2      | wTotalLength        | 2    | Sayı   | Bu yapılandırma için döndürülen toplam veri uzunluğu. Bu yapılandırma için döndürülen tüm tanımlayıcılar (yapılandırma, arabirim, uç nokta ve sınıf veya satıcıya özgü) Birleşik uzunluğunu içerir. |
| 4      | Bnumınterfaces      | 1    | Sayı   | Bu yapılandırma tarafından desteklenen arabirimlerin sayısı. |
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
| 6      | Bınterfacesubclass | 1    | Sınıf  | Alt sınıf kodu (USB tarafından atanır).<br />Bu kodlar bInterfaceClass alanının değeri ile nitelenir. BInterfaceClass alanı 0 olarak sıfırlandığında, bu alan de 0 olarak sıfırlanmalıdır. BInterfaceClass alanı 0xFF olarak ayarlanmamışsa, tüm değerler USB tarafından atanmak üzere ayrılmıştır. |
| 7      | Bınterfaceprotocol | 1    | Protokol  | Protokol kodu (USB tarafından atanır). Bu kodlar bInterfaceClass ve Bınterfacesubclass alanlarının değeri ile nitelenir. Bir arabirim sınıfa özgü istekleri destekliyorsa, bu kod, cihazın cihaz sınıfının belirtimine göre tanımlandığı şekilde kullandığı protokolleri tanımlar.<br />Bu alan 0 olarak sıfırlandığında, cihaz bu arabirim üzerinde sınıfa özgü bir protokol kullanmaz. Bu alan 0xFF olarak ayarlandıysa, cihaz bu arabirim için satıcıya özgü bir protokol kullanır. |
| 8      | IInterface         | 1    | Dizin oluşturma     | Bu arabirimi açıklayan dize tanımlayıcısının dizini. |

USBX, bir USB arabirim tanımlayıcısını aşağıdaki şekilde tanımlar.

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

USB arabirim tanımlayıcısı, aşağıdaki gibi açıklanan arabirim kapsayıcısının bir parçasıdır.

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

- **ux_interface_handle**: arabirimin tanıtıcısı. Bu, genellikle arabirim için bu yapının örneğinin adresidir.
- **ux_interface_state**: arabirimin durumu.
- **ux_interface_descriptor**: USB arabirim tanımlayıcısı.
- **ux_interface_class**: Bu arabirime sahip olan sınıf türüne yönelik işaretçi.
- **ux_interface_class_instance**: Bu arabirime sahip olan sınıfın örneğine yönelik işaretçi.
- **ux_interface_first_endpoint**: bu arabirimle kaydedilen ilk uç noktaya işaretçi.
- **ux_interface_next_interface**: yapılandırmayla ilişkili bir sonraki arabirime yönelik işaretçi.
- **ux_interface_configuration**: Bu arabirimin yapılandırma sahibine yönelik işaretçi.

### <a name="endpoint-descriptors"></a>Uç nokta tanımlayıcıları

Bir arabirimle ilişkilendirilen her uç noktanın kendi uç nokta tanımlayıcısı vardır. Bu tanımlayıcı, her uç noktanın bant genişliği gereksinimlerini, uç noktayla ilişkili en fazla yükü, dönemsellik ve yönünü belirlemede konak yığınının gerektirdiği bilgileri içerir. Bir uç nokta tanımlayıcısı her zaman yapılandırma için bir GET_DESCRIPTOR komutu tarafından döndürülür.

Cihaz tanımlayıcısıyla ilişkili varsayılan denetim uç noktası, arabirimle ilişkili uç noktalarının parçası olarak sayılmaz ve bu nedenle bu tanımlayıcıda döndürülmedi.

Konak yazılımı bir arabirim için alternatif ayarı istediğinde, tüm ilişkili uç noktalar ve USB kaynakları yeni alternatif ayara göre değiştirilir.

Varsayılan denetim uç noktaları hariç, uç noktalar arabirimler arasında paylaşılamıyor.

| Uzaklık | Alan            | Boyut | Değer    | Açıklama                       |
| ------ | ---------------- | ---- | -------- | --------------------------------- |
| 0      | bLength          | 1    | Sayı   | Bu tanımlayıcının bayt cinsinden boyutu. |
| 1      | bDescriptorType  | 1    | Sabit | UÇ nokta tanımlayıcı türü. |
| 2      | bEndpointAddress | 1    | Uç Nokta | USB cihazında bu tanımlayıcı tarafından tanımlanan bitiş noktasının adresi. Adres şu şekilde kodlanır:<br />Bit 3... 0: uç nokta numarası<br />Bit 6... 4: ayrılmış, sıfıra Sıfırla<br />Bit 7: Yön, denetim uç noktaları için yoksayıldı<br />0 = çıkış uç noktası<br />1 = uç noktada |
| 3      | bmAttributes     | 1    | Biteş   | Bu alan, **Bconfigurationvalue** alanı kullanılarak yapılandırıldığında bitiş noktasının özniteliklerini açıklar. Bit 1.. 0: aktarım türü<br />00 = denetim<br />01 = zaman aralıklı<br />10 = toplu<br />11 = kesme<br />Zaman aralıklı bir uç nokta değilse, bit 5.. 2 ayrılmıştır ve sıfıra ayarlanmalıdır. Zaman aralıklı ise, bunlar aşağıdaki gibi tanımlanır:<br />Bit 3.. 2: eşitleme türü<br />00 = eşitleme yok<br />01 = zaman uyumsuz<br />10 = Uyarlamalı<br />11 = zaman uyumlu<br />Bit 5.. 4: kullanım türü<br />00 = veri uç noktası<br />01 = geri bildirim uç noktası<br />10 = örtük geri bildirim verileri uç noktası<br />11 = ayrılmış |
| 4      | wMaxPacketSize   | 2    | Sayı   | En fazla paket boyutu bu uç nokta, bu yapılandırma seçildiğinde gönderme veya alma özelliğine sahiptir.<br />Zaman aralıklı uç noktalar için bu değer, (mikro) çerçeve veri yükleri için gereken zamanlamaya göre veri yolu ayırmak için kullanılır. Kanal, sürekli olarak, ayrılmış olandan daha az bant genişliği kullanır. Cihaz, gerekirse, normal, USB olmayan tanımlı mekanizmalar aracılığıyla kullanılan gerçek bant genişliğini raporlar.<br />Tüm uç noktalar için bit 10.. 0, en fazla paket boyutunu (bayt olarak) belirtir.<br />Yüksek hızlı zaman aralıklı ve kesme uç noktaları için:<br />BITS 12.. 11 mikro çerçeve başına ek işlem fırsatları sayısını belirtin: 00 = yok (mikro çerçeve başına 1 işlem)<br />01 = 1 ek (mikro çerçeve başına 2)<br />10 = 2 ek (mikro çerçeve başına 3)<br />11 = ayrılmış<br />Bit 15.. 13 ayrılmıştır ve sıfıra ayarlanmalıdır. |
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
