---
title: Bölüm 3-USBX cihaz yığınının Işlevsel bileşenleri
description: Bu bölüm, işlevsel bir perspektiften yüksek performanslı bir USBX Embedded USB cihaz yığınının açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: dc57f3e0f6aa6731f4aaedee8169313ca7276cff
ms.sourcegitcommit: 1aeca2f91960856d8cc24fef65f909639e527599
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/31/2021
ms.locfileid: "106082209"
---
# <a name="chapter-3---functional-components-of-usbx-device-stack"></a><span data-ttu-id="58539-103">Bölüm 3-USBX cihaz yığınının Işlevsel bileşenleri</span><span class="sxs-lookup"><span data-stu-id="58539-103">Chapter 3 - Functional Components of USBX Device Stack</span></span>

<span data-ttu-id="58539-104">Bu bölüm, işlevsel bir perspektiften yüksek performanslı bir USBX Embedded USB cihaz yığınının açıklamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="58539-104">This chapter contains a description of the high performance USBX embedded USB device stack from a functional perspective.</span></span>

## <a name="execution-overview"></a><span data-ttu-id="58539-105">Yürütmeye genel bakış</span><span class="sxs-lookup"><span data-stu-id="58539-105">Execution Overview</span></span>

<span data-ttu-id="58539-106">Cihaz için USBX birkaç bileşenden oluşur.</span><span class="sxs-lookup"><span data-stu-id="58539-106">USBX for the device is composed of several components.</span></span>

- <span data-ttu-id="58539-107">Başlatma</span><span class="sxs-lookup"><span data-stu-id="58539-107">Initialization</span></span>
- <span data-ttu-id="58539-108">Uygulama arabirimi çağrıları</span><span class="sxs-lookup"><span data-stu-id="58539-108">Application interface calls</span></span>
- <span data-ttu-id="58539-109">Cihaz sınıfları</span><span class="sxs-lookup"><span data-stu-id="58539-109">Device Classes</span></span>
- <span data-ttu-id="58539-110">USB cihaz yığını</span><span class="sxs-lookup"><span data-stu-id="58539-110">USB Device Stack</span></span>
- <span data-ttu-id="58539-111">Cihaz denetleyicisi</span><span class="sxs-lookup"><span data-stu-id="58539-111">Device controller</span></span>
- <span data-ttu-id="58539-112">VBUS Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="58539-112">VBUS manager</span></span>

<span data-ttu-id="58539-113">Aşağıdaki diyagramda, USBX cihaz yığını gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="58539-113">The following diagram illustrates the USBX Device stack.</span></span>

![USBX cihaz yığını](media/usbx-device-stack/usbx-device-stack.png)

### <a name="initialization"></a><span data-ttu-id="58539-115">Başlatma</span><span class="sxs-lookup"><span data-stu-id="58539-115">Initialization</span></span>

<span data-ttu-id="58539-116">USBX ' i etkinleştirmek için ***ux_system_initialize*** işlevi çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="58539-116">In order to activate USBX, the function ***ux_system_initialize*** must be called.</span></span> <span data-ttu-id="58539-117">Bu işlev, USBX bellek kaynaklarını başlatır.</span><span class="sxs-lookup"><span data-stu-id="58539-117">This function initializes the memory resources of USBX.</span></span>

<span data-ttu-id="58539-118">USBX cihaz tesislerini etkinleştirmek için ***ux_device_stack_initialize*** işlevi çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="58539-118">In order to activate USBX device facilities, the function ***ux_device_stack_initialize*** must be called.</span></span> <span data-ttu-id="58539-119">Bu işlev, USBX cihaz yığını tarafından kullanılan ve ThreadX iş parçacıkları, zaman uyumu sağlayıcılar ve semaforlar gibi tüm kaynakları başlatacak.</span><span class="sxs-lookup"><span data-stu-id="58539-119">This function will in turn initialize all the resources used by the USBX device stack such as ThreadX threads, mutexes, and semaphores.</span></span>

<span data-ttu-id="58539-120">Bu, USB cihaz denetleyicisini ve bir veya daha fazla USB sınıfını etkinleştirmek için uygulama başlatma 'ya kadar sürer.</span><span class="sxs-lookup"><span data-stu-id="58539-120">It is up to the application initialization to activate the USB device controller and one or more USB classes.</span></span> <span data-ttu-id="58539-121">USB ana bilgisayar tarafının aksine, cihaz tarafında herhangi bir anda yalnızca bir USB denetleyici sürücüsü çalışıyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="58539-121">Contrary to the USB host side, the device side can have only one USB controller driver running at any time.</span></span> <span data-ttu-id="58539-122">Sınıflar yığına kaydedildiğinde ve cihaz denetleyicisi başlatma işlevi çağrıldığında, veri yolu etkin olur ve yığın veri yolu sıfırlama ve konak listeleme komutlarına yanıt gönderir.</span><span class="sxs-lookup"><span data-stu-id="58539-122">When the classes have been registered to the stack and the device controller(s) initialization function has been called, the bus is active and the stack will reply to bus reset and host enumeration commands.</span></span>

### <a name="application-interface-calls"></a><span data-ttu-id="58539-123">Uygulama arabirimi çağrıları</span><span class="sxs-lookup"><span data-stu-id="58539-123">Application Interface Calls</span></span>

<span data-ttu-id="58539-124">USBX içinde iki API düzeyi vardır.</span><span class="sxs-lookup"><span data-stu-id="58539-124">There are two levels of APIs in USBX.</span></span>

- <span data-ttu-id="58539-125">USB cihaz yığını API 'Leri</span><span class="sxs-lookup"><span data-stu-id="58539-125">USB Device Stack APIs</span></span>
- <span data-ttu-id="58539-126">USB cihaz sınıfı API 'Leri</span><span class="sxs-lookup"><span data-stu-id="58539-126">USB Device Class APIs</span></span>

<span data-ttu-id="58539-127">Normalde, bir USBX uygulamasının USB cihaz yığını API 'Lerinden herhangi birini çağırması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="58539-127">Normally, a USBX application should not have to call any of the USB device stack APIs.</span></span> <span data-ttu-id="58539-128">Çoğu uygulama yalnızca USB sınıfı API 'Lerine erişir.</span><span class="sxs-lookup"><span data-stu-id="58539-128">Most applications will only access the USB Class APIs.</span></span>

### <a name="usb-device-stack-apis"></a><span data-ttu-id="58539-129">USB cihaz yığını API 'Leri</span><span class="sxs-lookup"><span data-stu-id="58539-129">USB Device Stack APIs</span></span>

<span data-ttu-id="58539-130">Cihaz yığını API 'Leri, sınıflar ve cihaz çerçevesi gibi USBX cihaz bileşenlerinin kaydı yapmaktan sorumludur.</span><span class="sxs-lookup"><span data-stu-id="58539-130">The device stack APIs are responsible for the registration of USBX device components such as classes and the device framework.</span></span>

### <a name="usb-device-class-apis"></a><span data-ttu-id="58539-131">USB cihaz sınıfı API 'Leri</span><span class="sxs-lookup"><span data-stu-id="58539-131">USB Device Class APIs</span></span>

<span data-ttu-id="58539-132">Sınıf API 'Leri her USB sınıfına çok özeldir.</span><span class="sxs-lookup"><span data-stu-id="58539-132">The Class APIs are very specific to each USB class.</span></span> <span data-ttu-id="58539-133">USB sınıfları için ortak API 'lerin çoğu, bir cihazı açma/kapatma ve bir cihazdan okuma ve bir cihaza yazma gibi hizmetleri sağlamıştır.</span><span class="sxs-lookup"><span data-stu-id="58539-133">Most of the common APIs for USB classes provided services such as opening/closing a device and reading from and writing to a device.</span></span> <span data-ttu-id="58539-134">API 'Ler ana bilgisayar tarafına benzer şekilde benzerdir.</span><span class="sxs-lookup"><span data-stu-id="58539-134">The APIs are similar in nature to the host side.</span></span>

## <a name="device-framework"></a><span data-ttu-id="58539-135">Cihaz çerçevesi</span><span class="sxs-lookup"><span data-stu-id="58539-135">Device Framework</span></span>

<span data-ttu-id="58539-136">USB cihaz tarafı, cihaz çerçevesinin tanımından sorumludur.</span><span class="sxs-lookup"><span data-stu-id="58539-136">The USB device side is responsible for the definition of the device framework.</span></span> <span data-ttu-id="58539-137">Cihaz çerçevesi, aşağıdaki bölümlerde açıklandığı gibi üç kategoriye ayrılmıştır.</span><span class="sxs-lookup"><span data-stu-id="58539-137">The device framework is divided into three categories, as described in the following sections.</span></span>

### <a name="definition-of-the-components-of-the-device-framework"></a><span data-ttu-id="58539-138">Cihaz çerçevesi bileşenlerinin tanımı</span><span class="sxs-lookup"><span data-stu-id="58539-138">Definition of the Components of the Device Framework</span></span>

<span data-ttu-id="58539-139">Cihaz çerçevesinin her bileşeninin tanımı, cihazın doğası ve cihaz tarafından kullanılan kaynaklar ile ilgilidir.</span><span class="sxs-lookup"><span data-stu-id="58539-139">The definition of each component of the device framework is related to the nature of the device and the resources utilized by the device.</span></span> <span data-ttu-id="58539-140">Ana kategoriler aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="58539-140">Following are the main categories.</span></span>

- <span data-ttu-id="58539-141">Cihaz tanımlayıcısı</span><span class="sxs-lookup"><span data-stu-id="58539-141">Device Descriptor</span></span>
- <span data-ttu-id="58539-142">Yapılandırma tanımlayıcısı</span><span class="sxs-lookup"><span data-stu-id="58539-142">Configuration Descriptor</span></span>
- <span data-ttu-id="58539-143">Arabirim tanımlayıcısı</span><span class="sxs-lookup"><span data-stu-id="58539-143">Interface Descriptor</span></span>
- <span data-ttu-id="58539-144">Uç nokta tanımlayıcısı</span><span class="sxs-lookup"><span data-stu-id="58539-144">Endpoint Descriptor</span></span>

<span data-ttu-id="58539-145">USBX hem yüksek hem de tam hızda cihaz bileşeni tanımını destekler (düşük hız tam hızda aynı şekilde kabul edilir).</span><span class="sxs-lookup"><span data-stu-id="58539-145">USBX supports device component definition for both high and full speed (low speed being treated the same way as full speed).</span></span> <span data-ttu-id="58539-146">Bu, cihazın yüksek hızda veya tam hızlı ana bilgisayara bağlıyken farklı şekilde çalışmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="58539-146">This allows the device to operate differently when connected to a high speed or full speed host.</span></span> <span data-ttu-id="58539-147">Tipik farklılıklar, her uç noktanın boyutudur ve cihaz tarafından tüketilen güçlerdir.</span><span class="sxs-lookup"><span data-stu-id="58539-147">The typical differences are the size of each endpoint and the power consumed by the device.</span></span>

<span data-ttu-id="58539-148">Cihaz bileşeninin tanımı, USB belirtimini izleyen bir bayt dizesi biçimini alır.</span><span class="sxs-lookup"><span data-stu-id="58539-148">The definition of the device component takes the form of a byte string that follows the USB specification.</span></span> <span data-ttu-id="58539-149">Tanım bitişik ve çerçevenin bellekte temsil edildiği sıra, numaralandırma sırasında ana bilgisayara döndürülen ile aynı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="58539-149">The definition is contiguous and the order in which the framework is represented in memory will be the same as the one returned to the host during enumeration.</span></span>

<span data-ttu-id="58539-150">Yüksek hızlı USB flash disk için bir cihaz çerçevesi örneği aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="58539-150">Following is an example of a device framework for a high speed USB Flash Disk.</span></span>

```c
#define DEVICE_FRAMEWORK_LENGTH_HIGH_SPEED 60
UCHAR device_framework_high_speed[] = {
    /* Device descriptor */
    0x12, 0x01, 0x00, 0x02, 0x00, 0x00, 0x00, 0x40, 0x0a, 0x07, 0x25, 0x40, 0x01, 0x00, 0x01, 0x02, 0x03, 0x01,

    /* Device qualifier descriptor */
    0x0a, 0x06, 0x00, 0x02, 0x00, 0x00, 0x00, 0x40, 0x01, 0x00,

    /* Configuration descriptor */
    0x09, 0x02, 0x20, 0x00, 0x01, 0x01, 0x00, 0xc0, 0x32,

    /* Interface descriptor */
    0x09, 0x04, 0x00, 0x00, 0x02, 0x08, 0x06, 0x50, 0x00,

    /* Endpoint descriptor (Bulk Out) */
    0x07, 0x05, 0x01, 0x02, 0x00, 0x02, 0x00,

    /* Endpoint descriptor (Bulk In) */
    0x07, 0x05, 0x82, 0x02, 0x00, 0x02, 0x00
};
```

### <a name="definition-of-the-strings-of-the-device-framework"></a><span data-ttu-id="58539-151">Cihaz çerçevesi dizelerinin tanımı</span><span class="sxs-lookup"><span data-stu-id="58539-151">Definition of the Strings of the Device Framework</span></span>

<span data-ttu-id="58539-152">Dizeler bir cihazda isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="58539-152">Strings are optional in a device.</span></span> <span data-ttu-id="58539-153">Bu kişilerin amacı, USB konağının cihaz üreticisi, ürün adı ve Unicode dizeleri aracılığıyla düzeltme numarası hakkında bilgi sahibi sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="58539-153">Their purpose is to let the USB host know about the manufacturer of the device, the product name, and the revision number through Unicode strings.</span></span>

<span data-ttu-id="58539-154">Ana dizeler, cihaz tanımlayıcılarında gömülü olan dizinlerdir.</span><span class="sxs-lookup"><span data-stu-id="58539-154">The main strings are indexes embedded in the device descriptors.</span></span> <span data-ttu-id="58539-155">Ek dizeler dizinleri tek tek arabirimlere katıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="58539-155">Additional strings indexes can be embedded into individual interfaces.</span></span>

<span data-ttu-id="58539-156">Yukarıdaki cihaz çerçevesinin cihaz tanımlayıcısına eklenmiş üç dize dizini olduğunu varsayarsak, dize çerçevesi tanımı bu örnek koda benzeyebilir.</span><span class="sxs-lookup"><span data-stu-id="58539-156">Assuming the device framework above has three string indexes embedded into the device descriptor, the string framework definition could look like this example code.</span></span>

```c
/* String Device Framework:
    Byte 0 and 1: Word containing the language ID: 0x0904 for US
    Byte 2 : Byte containing the index of the descriptor
    Byte 3 : Byte containing the length of the descriptor string
*/

#define STRING_FRAMEWORK_LENGTH 38
UCHAR string_framework[] = {
    /* Manufacturer string descriptor: Index 1 */
    0x09, 0x04, 0x01, 0x0c,
    0x45, 0x78, 0x70, 0x72, 0x65, 0x73, 0x20, 0x4c,
    0x6f, 0x67, 0x69, 0x63,

    /* Product string descriptor: Index 2 */
    0x09, 0x04, 0x02, 0x0c,
    0x4D, 0x4C, 0x36, 0x39, 0x36, 0x35, 0x30, 0x30,
    0x20, 0x53, 0x44, 0x4B,

    /* Serial Number string descriptor: Index 3 */
    0x09, 0x04, 0x03, 0x04,
    0x30, 0x30, 0x30, 0x31
};
```

<span data-ttu-id="58539-157">Her hız için farklı dizelerin kullanılması gerekiyorsa, dizinlerin hız belirsiz olduğu için farklı dizinlerin kullanılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="58539-157">If different strings have to be used for each speed, different indexes must be used as the indexes are speed agnostic.</span></span>

<span data-ttu-id="58539-158">Dizenin kodlaması UNICODE tabanlıdır.</span><span class="sxs-lookup"><span data-stu-id="58539-158">The encoding of the string is UNICODE-based.</span></span> <span data-ttu-id="58539-159">UNICODE kodlama standardı hakkında daha fazla bilgi için aşağıdaki yayına başvurun:</span><span class="sxs-lookup"><span data-stu-id="58539-159">For more information on the UNICODE encoding standard refer to the following publication:</span></span>

<span data-ttu-id="58539-160">*Unicode standart, dünya çapındaki karakter kodlaması, sürüm 1., birimler 1 ve 2, Unicode konsorsiyum, Addison-Wesley yayımlama şirketi, okuma MA.*</span><span class="sxs-lookup"><span data-stu-id="58539-160">*The Unicode Standard, Worldwide Character Encoding, Version 1., Volumes 1 and 2, The Unicode Consortium, Addison-Wesley Publishing Company, Reading MA.*</span></span>

### <a name="definition-of-the-languages-supported-by-the-device-for-each-string"></a><span data-ttu-id="58539-161">Her dize için cihaz tarafından desteklenen dillerin tanımı</span><span class="sxs-lookup"><span data-stu-id="58539-161">Definition of the Languages Supported by the Device for each String</span></span>

<span data-ttu-id="58539-162">USBX 'in varsayılan değer olan Ingilizce olmasına rağmen birden çok dili destekleme yeteneği vardır.</span><span class="sxs-lookup"><span data-stu-id="58539-162">USBX has the ability to support multiple languages although English is the default.</span></span> <span data-ttu-id="58539-163">Dize tanımlayıcıları için her dilin tanımı, aşağıdaki şekilde tanımlanan bir dil tanımı dizisi biçimindedir.</span><span class="sxs-lookup"><span data-stu-id="58539-163">The definition of each language for the string descriptors is in the form of an array of languages definition defined as follows.</span></span>

```c
#define LANGUAGE_ID_FRAMEWORK_LENGTH 2
UCHAR language_id_framework[] = {
    /* English. */
    0x09, 0x04
};
```

<span data-ttu-id="58539-164">Ek dilleri desteklemek için, varsayılan Ingilizce kodundan sonra dil kodu çift baytlı tanımını eklemeniz yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="58539-164">To support additional languages, simply add the language code double-byte definition after the default English code.</span></span> <span data-ttu-id="58539-165">Dil kodu belge içinde Microsoft tarafından tanımlandı.</span><span class="sxs-lookup"><span data-stu-id="58539-165">The language code has been defined by Microsoft in the document.</span></span>

<span data-ttu-id="58539-166">*Windows 95 ve Windows NT, Nadine Kano, Microsoft Press, Redmond WA için uluslararası yazılım geliştirme*</span><span class="sxs-lookup"><span data-stu-id="58539-166">*Developing International Software for Windows 95 and Windows NT, Nadine Kano, Microsoft Press, Redmond WA*</span></span>

## <a name="vbus-manager"></a><span data-ttu-id="58539-167">VBUS Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="58539-167">VBUS Manager</span></span>

<span data-ttu-id="58539-168">Çoğu USB cihaz tasarımlarında, VBUS, USB cihaz çekirdeği 'nin bir parçası değildir, bunun yerine çizgi sinyalini izleyen bir harici GıO 'a bağlanır.</span><span class="sxs-lookup"><span data-stu-id="58539-168">In most USB device designs, VBUS is not part of the USB Device core but rather connected to an external GPIO, which monitors the line signal.</span></span>

<span data-ttu-id="58539-169">Sonuç olarak, VBUS 'ın cihaz denetleyicisi sürücüsünden ayrı olarak yönetilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="58539-169">As a result, VBUS has to be managed separately from the device controller driver.</span></span>

<span data-ttu-id="58539-170">Bu, cihaz denetleyicisine VBUS GÇ adresini sağlamak için uygulamaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="58539-170">It is up to the application to provide the device controller with the address of the VBUS IO.</span></span> <span data-ttu-id="58539-171">Cihaz denetleyicisi başlatılmadan önce VBUS başlatılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="58539-171">VBUS must be initialized prior to the device controller initialization.</span></span>

<span data-ttu-id="58539-172">Sanal veri izleme platformu belirtimine bağlı olarak, VBUS GÇ başlatıldıktan sonra denetleyici sürücüsünün VBUS sinyalleri işlemesini sağlamak mümkündür veya bu mümkün değilse, uygulamanın VBUS işleme kodunu sağlaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="58539-172">Depending on the platform specification for monitoring VBUS, it is possible to let the controller driver handle VBUS signals after the VBUS IO is initialized or if this is not possible, the application has to provide the code for handling VBUS.</span></span>

<span data-ttu-id="58539-173">Uygulama VBUS 'ı kendisine göre işlemesini istiyorsa, tek gereksinimi, bir cihazın ayıklandığını algıladığında işlevi ***ux_device_stack_disconnect*** çağırmalıdır.</span><span class="sxs-lookup"><span data-stu-id="58539-173">If the application wishes to handle VBUS by itself, its only requirement is to call the function ***ux_device_stack_disconnect*** when it detects that a device has been extracted.</span></span> <span data-ttu-id="58539-174">Bir cihaz takıldığında denetleyiciyi bilgilendirmek gerekli değildir çünkü veri yolu SıFıRLAMA onayı/kaldırma sinyali algılandığında denetleyici uyandırır.</span><span class="sxs-lookup"><span data-stu-id="58539-174">It is not necessary to inform the controller when a device is inserted because the controller will wake up when the BUS RESET assert/deassert signal is detected.</span></span>
