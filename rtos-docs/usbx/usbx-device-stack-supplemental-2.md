---
title: Bölüm 2-USBX cihaz sınıfı konuları
description: USB cihaz RNDIS sınıfı, USB konak sisteminin cihazla Ethernet cihazı olarak iletişim kurmasına olanak tanır. Bu sınıf, Microsoft özel uygulamasına dayalıdır ve Windows platformları için özeldir.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 035492644a911eba3b1c62a79572bc7d4c55f6dd
ms.sourcegitcommit: 1aeca2f91960856d8cc24fef65f909639e527599
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/31/2021
ms.locfileid: "106082226"
---
# <a name="chapter-2---usbx-device-class-considerations"></a><span data-ttu-id="445f1-104">Bölüm 2-USBX cihaz sınıfı konuları</span><span class="sxs-lookup"><span data-stu-id="445f1-104">Chapter 2 - USBX Device Class Considerations</span></span>

## <a name="usb-device-rndis-class"></a><span data-ttu-id="445f1-105">USB cihazı RNDIS sınıfı</span><span class="sxs-lookup"><span data-stu-id="445f1-105">USB Device RNDIS Class</span></span>

<span data-ttu-id="445f1-106">USB cihaz RNDIS sınıfı, USB konak sisteminin cihazla Ethernet cihazı olarak iletişim kurmasına olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="445f1-106">The USB device RNDIS class allows for a USB host system to communicate with the device as a ethernet device.</span></span> <span data-ttu-id="445f1-107">Bu sınıf, Microsoft özel uygulamasına dayalıdır ve Windows platformları için özeldir.</span><span class="sxs-lookup"><span data-stu-id="445f1-107">This class is based on the Microsoft proprietary implementation and is specific to Windows platforms.</span></span>

<span data-ttu-id="445f1-108">RNDIS uyumlu bir cihaz çerçevesinin cihaz yığını tarafından bildirilmesine ihtiyacı vardır.</span><span class="sxs-lookup"><span data-stu-id="445f1-108">A RNDIS compliant device framework needs to be declared by the device stack.</span></span> <span data-ttu-id="445f1-109">Aşağıda bir örnek bulunur.</span><span class="sxs-lookup"><span data-stu-id="445f1-109">An example is found below.</span></span>

```C
unsigned char device_framework_full_speed[] = {
    /* VID: 0x04b4
    PID: 0x1127
    */

    /* Device Descriptor */
    0x12, /* bLength */
    0x01, /* bDescriptorType */
    0x10, 0x01, /* bcdUSB */
    0x02, /* bDeviceClass - CDC */
    0x00, /* bDeviceSubClass */
    0x00, /* bDeviceProtocol */
    0x40, /* bMaxPacketSize0 */
    0xb4, 0x04, /* idVendor */
    0x27, 0x11, /* idProduct */
    0x00, 0x01, /* bcdDevice */
    0x01, /* iManufacturer */
    0x02, /* iProduct */
    0x03, /* iSerialNumber */
    0x01, /* bNumConfigurations */

    /* Configuration Descriptor */
    0x09, /* bLength */
    0x02, /* bDescriptorType */
    0x38, 0x00, /* wTotalLength */
    0x02, /* bNumInterfaces */
    0x01, /* bConfigurationValue */
    0x00, /* iConfiguration */
    0x40, /* bmAttributes - Self-powered */
    0x00, /* bMaxPower */

    /* Interface Association Descriptor */
    0x08, /* bLength */
    0x0b, /* bDescriptorType */
    0x00, /* bFirstInterface */
    0x02, /* bInterfaceCount */
    0x02, /* bFunctionClass - CDC - Communication */
    0xff, /* bFunctionSubClass - Vendor Defined – In this case, RNDIS */
    0x00, /* bFunctionProtocol - No class specific protocol required */
    0x00, /* iFunction */

    /* Interface Descriptor */
    0x09, /* bLength */
    0x04, /* bDescriptorType */
    0x00, /* bInterfaceNumber */
    0x00, /* bAlternateSetting */
    0x01, /* bNumEndpoints */
    0x02, /* bInterfaceClass - CDC - Communication */
    0xff, /* bInterfaceSubClass - Vendor Defined – In this case, RNDIS */
    0x00, /* bInterfaceProtocol - No class specific protocol required */
    0x00, /* iInterface */

    /* Endpoint Descriptor */
    0x07, /* bLength */
    0x05, /* bDescriptorType */
    0x83, /* bEndpointAddress */
    0x03, /* bmAttributes - Interrupt */
    0x08, 0x00, /* wMaxPacketSize */
    0xff, /* bInterval */

    /* Interface Descriptor */
    0x09, /* bLength */
    0x04, /* bDescriptorType */
    0x01, /* bInterfaceNumber */
    0x00, /* bAlternateSetting */
    0x02, /* bNumEndpoints */
    0x0a, /* bInterfaceClass - CDC - Data */
    0x00, /* bInterfaceSubClass - Should be 0x00 */
    0x00, /* bInterfaceProtocol - No class specific protocol required */
    0x00, /* iInterface */

    /* Endpoint Descriptor */
    0x07, /* bLength */
    0x05, /* bDescriptorType */
    0x02, /* bEndpointAddress */
    0x02, /* bmAttributes - Bulk */
    0x40, 0x00, /* wMaxPacketSize */
    0x00, /* bInterval */

    /* Endpoint Descriptor */
    0x07, /* bLength */
    0x05, /* bDescriptorType */
    0x81, /* bEndpointAddress */
    0x02, /* bmAttributes - Bulk */
    0x40, 0x00, /* wMaxPacketSize */
    0x00, /* bInterval */
};
```

<span data-ttu-id="445f1-110">RNDIS sınıfı, CDC-ACM ve CDC-ECD için çok benzer bir cihaz tanımlayıcısı yaklaşımı kullanır ve ayrıca bir ıAD tanımlayıcısı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="445f1-110">The RNDIS class uses a very similar device descriptor approach to the CDC-ACM and CDC-ECM and also requires a IAD descriptor.</span></span> <span data-ttu-id="445f1-111">Cihaz tanımlayıcısının tanımı ve gereksinimleri için CDC-ACM sınıfına bakın.</span><span class="sxs-lookup"><span data-stu-id="445f1-111">See the CDC-ACM class for definition and requirements for the device descriptor.</span></span>

<span data-ttu-id="445f1-112">RNDIS sınıfının etkinleştirilmesi aşağıdaki gibidir.</span><span class="sxs-lookup"><span data-stu-id="445f1-112">The activation of the RNDIS class is as follows.</span></span>

```C
/* Set the parameters for callback when insertion/extraction of a CDC device. Set to NULL.*/

parameter.ux_slave_class_rndis_instance_activate = UX_NULL;
parameter.ux_slave_class_rndis_instance_deactivate = UX_NULL;

/* Define a local NODE ID. */

parameter.ux_slave_class_rndis_parameter_local_node_id[0] = 0x00;
parameter.ux_slave_class_rndis_parameter_local_node_id[1] = 0x1e;
parameter.ux_slave_class_rndis_parameter_local_node_id[2] = 0x58;
parameter.ux_slave_class_rndis_parameter_local_node_id[3] = 0x41;
parameter.ux_slave_class_rndis_parameter_local_node_id[4] = 0xb8;
parameter.ux_slave_class_rndis_parameter_local_node_id[5] = 0x78;

/* Define a remote NODE ID. */

parameter.ux_slave_class_rndis_parameter_remote_node_id[0] = 0x00;
parameter.ux_slave_class_rndis_parameter_remote_node_id[1] = 0x1e;
parameter.ux_slave_class_rndis_parameter_remote_node_id[2] = 0x58;
parameter.ux_slave_class_rndis_parameter_remote_node_id[3] = 0x41;
parameter.ux_slave_class_rndis_parameter_remote_node_id[4] = 0xb8;
parameter.ux_slave_class_rndis_parameter_remote_node_id[5] = 0x79;

/* Set extra parameters used by the RNDIS query command with certain OIDs. */

parameter.ux_slave_class_rndis_parameter_vendor_id = 0x04b4 ;
parameter.ux_slave_class_rndis_parameter_driver_version = 0x1127;
ux_utility_memory_copy(parameter.ux_slave_class_rndis_parameter_vendor_description,
    "ELOGIC RNDIS", 12);

/* Initialize the device rndis class. This class owns both interfaces. */
status = ux_device_stack_class_register(_ux_system_slave_class_rndis_name,
    ux_device_class_rndis_entry, 1,0, &parameter);
```

<span data-ttu-id="445f1-113">CDC-ECD için, RNDIS sınıfı 2 düğüm, bir yerel ve bir uzak, ancak uzak düğümü tanımlayan bir dize tanımlayıcısına sahip olmak için gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="445f1-113">As for the CDC-ECM, the RNDIS class requires 2 nodes, one local and one remote but there is no requirement to have a string descriptor describing the remote node.</span></span>

<span data-ttu-id="445f1-114">Ancak, Microsoft özel mesajlaşma mekanizmasından dolayı bazı ek parametreler gereklidir.</span><span class="sxs-lookup"><span data-stu-id="445f1-114">However due to Microsoft proprietary messaging mechanism, some extra parameters are required.</span></span> <span data-ttu-id="445f1-115">Önce satıcı KIMLIĞININ geçirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="445f1-115">First the vendor ID has to be passed.</span></span> <span data-ttu-id="445f1-116">Benzer şekilde, RNDIS 'in sürücü sürümü.</span><span class="sxs-lookup"><span data-stu-id="445f1-116">Likewise, the driver version of the RNDIS.</span></span> <span data-ttu-id="445f1-117">Bir satıcı dizesi de verilmelidir.</span><span class="sxs-lookup"><span data-stu-id="445f1-117">A vendor string must also be given.</span></span>

<span data-ttu-id="445f1-118">RNDIS sınıfında, her iki şekilde de verileri aktarmaya yönelik yerleşik API 'Ler vardır ancak kullanıcı uygulaması, USB Ethernet cihazından NetX üzerinden iletişim kurduğu için bu uygulamalar uygulamaya gizlenir.</span><span class="sxs-lookup"><span data-stu-id="445f1-118">The RNDIS class has built-in APIs for transferring data both ways but they are hidden to the application as the user application will communicate with the USB Ethernet device through NetX.</span></span>

<span data-ttu-id="445f1-119">USBX RNDIS sınıfı, Azure RTOS NetX ağ yığınına yakın bir şekilde bağlanır.</span><span class="sxs-lookup"><span data-stu-id="445f1-119">The USBX RNDIS class is closely tied to Azure RTOS NetX Network stack.</span></span> <span data-ttu-id="445f1-120">NetX ve USBX RNDIS sınıfını kullanan bir uygulama, NetX ağ yığınını olağan şekilde etkinleştirir ancak ek olarak, USB ağ yığınını aşağıdaki şekilde etkinleştirmek gerekir.</span><span class="sxs-lookup"><span data-stu-id="445f1-120">An application using both NetX and USBX RNDIS class will activate the NetX network stack in its usual way but in addition needs to activate the USB network stack as follows.</span></span>

```C
/* Initialize the NetX system. */

nx_system_initialize();

/* Perform the initialization of the network driver. This will initialize the USBX network layer.*/
ux_network_driver_init();
```

<span data-ttu-id="445f1-121">USB ağ yığınının yalnızca bir kez etkinleştirilmesi ve RNDIS 'e özgü olmaması, ancak NetX hizmetleri gerektiren herhangi bir USB sınıfı için gerekli olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="445f1-121">The USB network stack needs to be activated only once and is not specific to RNDIS but is required by any USB class that requires NetX services.</span></span>

<span data-ttu-id="445f1-122">RNDIS sınıfı, Microsoft işletim sistemlerine özgü olan MAC OS ve Linux konakları tarafından tanınmaz.</span><span class="sxs-lookup"><span data-stu-id="445f1-122">The RNDIS class will not be recognized by MAC OS and Linux hosts as it is specific to Microsoft operating systems.</span></span> <span data-ttu-id="445f1-123">Windows platformlarında, cihaz tanımlayıcısıyla eşleşen konakta bir. inf dosyası bulunması gerekir.</span><span class="sxs-lookup"><span data-stu-id="445f1-123">On windows platforms a .inf file needs to be present on the host that matches the device descriptor.</span></span> <span data-ttu-id="445f1-124">Microsoft, RNDIS sınıfı için bir şablon sağlar ve usbx_windows_host_files dizininde bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="445f1-124">Microsoft supplies a template for the RNDIS class and it can be found in the usbx_windows_host_files directory.</span></span> <span data-ttu-id="445f1-125">Windows 'un daha yeni sürümü için RNDIS_Template. inf dosyası kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="445f1-125">For more recent version of Windows the file RNDIS_Template.inf should be used.</span></span> <span data-ttu-id="445f1-126">Bu dosyanın, cihaz tarafından kullanılan PID/VıD 'yi yansıtacak şekilde değiştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="445f1-126">This file needs to be modified to reflect the PID/VID used by the device.</span></span> <span data-ttu-id="445f1-127">Şirket ve ürün USB-IF ile kaydettirilirse, PID/VıD son müşteriye özgü olacaktır.</span><span class="sxs-lookup"><span data-stu-id="445f1-127">The PID/VID will be specific to the final customer when the company and the product are registered with the USB-IF.</span></span> <span data-ttu-id="445f1-128">INF dosyasında, değiştirilecek alanlar burada bulunur.</span><span class="sxs-lookup"><span data-stu-id="445f1-128">In the inf file, the fields to modify are located here.</span></span>

```Inf
[DeviceList]
%DeviceName%=DriverInstall, USB\\VID_xxxx&PID_yyyy&MI_00

[DeviceList.NTamd64]
%DeviceName%=DriverInstall, USB\\VID_xxxx&PID_yyyy&MI_00
```

<span data-ttu-id="445f1-129">RNDIS cihazının cihaz çerçevesinde, PID/VıD cihaz tanımlayıcısına depolanır (yukarıda belirtilen cihaz tanımlayıcısına bakın)</span><span class="sxs-lookup"><span data-stu-id="445f1-129">In the device framework of the RNDIS device, the PID/VID are stored in the device descriptor (see the device descriptor declared above)</span></span>

<span data-ttu-id="445f1-130">USB ana bilgisayar sistemleri, USB RNDIS cihazını bulduğunda, bir ağ arabirimi bağlayacaktır ve cihaz ağ protokol yığını ile birlikte kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="445f1-130">When a USB host systems discovers the USB RNDIS device, it will mount a network interface and the device can be used with network protocol stack.</span></span> <span data-ttu-id="445f1-131">Başvuru için konak Işletim sistemine bakın.</span><span class="sxs-lookup"><span data-stu-id="445f1-131">See the host Operating System for reference.</span></span>

## <a name="usb-device-dfu-class"></a><span data-ttu-id="445f1-132">USB cihaz DFU sınıfı</span><span class="sxs-lookup"><span data-stu-id="445f1-132">USB Device DFU Class</span></span>

<span data-ttu-id="445f1-133">USB cihaz DFU sınıfı, bir USB konak sisteminin bir konak uygulamasına bağlı olarak cihaz bellenimini güncelleştirmesine izin verir.</span><span class="sxs-lookup"><span data-stu-id="445f1-133">The USB device DFU class allows for a USB host system to update the device firmware based on a host application.</span></span> <span data-ttu-id="445f1-134">DFU sınıfı, bir USB-IF standart sınıfıdır.</span><span class="sxs-lookup"><span data-stu-id="445f1-134">The DFU class is a USB-IF standard class.</span></span>

<span data-ttu-id="445f1-135">USBX DFU sınıfı nispeten basittir.</span><span class="sxs-lookup"><span data-stu-id="445f1-135">USBX DFU class is relatively simple.</span></span> <span data-ttu-id="445f1-136">BT cihaz tanımlayıcısı, bir denetim uç noktası olmak üzere hiçbir şey gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="445f1-136">It device descriptor does not require anything but a control endpoint.</span></span> <span data-ttu-id="445f1-137">Çoğu zaman, bu sınıf bir USB Bileşik cihazına gömülecektir.</span><span class="sxs-lookup"><span data-stu-id="445f1-137">Most of the time, this class will be embedded into a USB composite device.</span></span> <span data-ttu-id="445f1-138">Cihaz, bir depolama cihazı veya bir iletişim cihazı gibi herhangi bir şey olabilir ve eklenen DFU arabirimi, ana bilgisayara cihazın belleniminin güncelleştirilmesini sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="445f1-138">The device can be anything such as a storage device or a comm device and the added DFU interface can inform the host that the device can have its firmware updated on the fly.</span></span>

<span data-ttu-id="445f1-139">DFU sınıfı 3 adımda çalışmaktadır.</span><span class="sxs-lookup"><span data-stu-id="445f1-139">The DFU class works in 3 steps.</span></span> <span data-ttu-id="445f1-140">İlk olarak, aygıt, dışarıya aktarılmış sınıfı kullanarak normal şekilde takar.</span><span class="sxs-lookup"><span data-stu-id="445f1-140">First the device mounts as normal using the class exported.</span></span> <span data-ttu-id="445f1-141">Konaktaki (Windows veya Linux) bir uygulama DFU sınıfını oluşturacak ve cihazı DFU moduna sıfırlamaya yönelik bir istek gönderecek.</span><span class="sxs-lookup"><span data-stu-id="445f1-141">An application on the host (Windows or Linux) will exercise the DFU class and send a request to reset the device into DFU mode.</span></span> <span data-ttu-id="445f1-142">Cihaz, veri yolundan kısa bir süre (konak ve cihaz için bir SıFıRLAMA sırasını algılamaya yetecek kadar) kaybolur ve yeniden başlatıldığında cihaz, ana bilgisayar uygulamasının bir bellenim yükseltmesi göndermesini beklemek için özel olarak DFU modunda olur.</span><span class="sxs-lookup"><span data-stu-id="445f1-142">The device will disappear from the bus for a short time (enough for the host and the device to detect a RESET sequence) and upon restarting, the device will be exclusively in DFU mode, waiting for the host application to send a firmware upgrade.</span></span> <span data-ttu-id="445f1-143">Üretici yazılımı yükseltmesi tamamlandığında, ana bilgisayar uygulaması cihazı sıfırlar ve yeniden numaralandırdıktan sonra cihaz yeni üretici yazılımıyla normal işlemine döndürülür.</span><span class="sxs-lookup"><span data-stu-id="445f1-143">When the firmware upgrade has been completed, the host application resets the device and upon re-enumeration the device will revert to its normal operation with the new firmware.</span></span>

<span data-ttu-id="445f1-144">DFU cihaz çerçevesi şuna benzeyecektir.</span><span class="sxs-lookup"><span data-stu-id="445f1-144">A DFU device framework will look like this.</span></span>

```C
UCHAR device_framework_full_speed[] = {

    /* Device descriptor */
    0x12, 0x01, 0x10, 0x01, 0x00, 0x00, 0x00, 0x40,
    0x99, 0x99, 0x00, 0x00, 0x00, 0x00, 0x01, 0x02,
    0x03, 0x01,

    /* Configuration descriptor */
    0x09, 0x02, 0x1b, 0x00, 0x01, 0x01, 0x00, 0xc0,
    0x32,

    /* Interface descriptor for DFU. */
    0x09, 0x04, 0x00, 0x00, 0x00, 0xFE, 0x01, 0x01, 0x00,

    /* Functional descriptor for DFU. */
    0x09, 0x21, 0x0f, 0xE8, 0x03, 0x40, 0x00, 0x00,
    0x01,

};
```

<span data-ttu-id="445f1-145">Bu örnekte, DFU tanımlayıcısı diğer sınıflarla ilişkili değildir.</span><span class="sxs-lookup"><span data-stu-id="445f1-145">In this example, the DFU descriptor is not associated with any other classes.</span></span> <span data-ttu-id="445f1-146">Basit bir arabirim tanımlayıcısına sahiptir ve kendisine bağlı başka uç noktalar yoktur.</span><span class="sxs-lookup"><span data-stu-id="445f1-146">It has a simple interface descriptor and no other endpoints attached to it.</span></span> <span data-ttu-id="445f1-147">Cihazın DFU özelliklerinin ayrıntılarını açıklayan bir Işlevsel tanımlayıcı vardır.</span><span class="sxs-lookup"><span data-stu-id="445f1-147">There is a Functional descriptor that describes the specifics of the DFU capabilities of the device.</span></span>

<span data-ttu-id="445f1-148">DFU yeteneklerinin açıklaması aşağıdaki gibidir.</span><span class="sxs-lookup"><span data-stu-id="445f1-148">The description of the DFU capabilities are as follows.</span></span>

| <span data-ttu-id="445f1-149">Name</span><span class="sxs-lookup"><span data-stu-id="445f1-149">Name</span></span>             | <span data-ttu-id="445f1-150">Uzaklık</span><span class="sxs-lookup"><span data-stu-id="445f1-150">Offset</span></span>  | <span data-ttu-id="445f1-151">Boyut</span><span class="sxs-lookup"><span data-stu-id="445f1-151">Size</span></span> | <span data-ttu-id="445f1-152">tür</span><span class="sxs-lookup"><span data-stu-id="445f1-152">type</span></span>      | <span data-ttu-id="445f1-153">Description</span><span class="sxs-lookup"><span data-stu-id="445f1-153">Description</span></span> |
|------------------|----------|------|-----------|------------|
| <span data-ttu-id="445f1-154">bmAttributes</span><span class="sxs-lookup"><span data-stu-id="445f1-154">bmAttributes</span></span>  | <span data-ttu-id="445f1-155">2</span><span class="sxs-lookup"><span data-stu-id="445f1-155">2</span></span>     | <span data-ttu-id="445f1-156">1</span><span class="sxs-lookup"><span data-stu-id="445f1-156">1</span></span>   | <span data-ttu-id="445f1-157">Bit alanı</span><span class="sxs-lookup"><span data-stu-id="445f1-157">Bit field</span></span> | <span data-ttu-id="445f1-158">Bit 3: cihaz, bir DFU_DETACH isteği aldığında bir veri yolu ayırma-iliştirme sırası gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="445f1-158">Bit 3: device will perform a bus detach-attach sequence when it receives a DFU_DETACH request.</span></span> <span data-ttu-id="445f1-159">Konağın USB sıfırlaması yayınlamamalıdır.</span><span class="sxs-lookup"><span data-stu-id="445f1-159">The host must not issue a USB Reset.</span></span> <span data-ttu-id="445f1-160">(bitWillDetach) 0 = Hayır 1 = Evet bit 2: cihaz, bildirim aşamasından sonra USB üzerinden iletişim kurabilir.</span><span class="sxs-lookup"><span data-stu-id="445f1-160">(bitWillDetach) 0 = no 1 = yes Bit 2: device is able to communicate via USB after Manifestation phase.</span></span> <span data-ttu-id="445f1-161">(Bitbildirimli Estationdayanıklı) 0 = Hayır, veri yolu sıfırlaması 1 = Evet bit 1: karşıya yükleme özellikli (bitCanUpload) 0 = Hayır 1 = Evet bit 0: indirme özelliği (bitCanDnload) 0 = Hayır 1 = Evet</span><span class="sxs-lookup"><span data-stu-id="445f1-161">(bitManifestationTolerant) 0 = no, must see bus reset 1 = yes Bit 1: upload capable (bitCanUpload) 0 = no 1 = yes Bit 0: download capable (bitCanDnload) 0 = no 1 = yes</span></span>  |
| <span data-ttu-id="445f1-162">Wçıkarılabilir zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="445f1-162">wDetachTimeOut</span></span>  | <span data-ttu-id="445f1-163">3</span><span class="sxs-lookup"><span data-stu-id="445f1-163">3</span></span>      | <span data-ttu-id="445f1-164">2</span><span class="sxs-lookup"><span data-stu-id="445f1-164">2</span></span>  | <span data-ttu-id="445f1-165">sayı</span><span class="sxs-lookup"><span data-stu-id="445f1-165">number</span></span>    | <span data-ttu-id="445f1-166">Milisaniye cinsinden, cihazın DFU_DETACH isteği alındıktan sonra bekleyeceği süre.</span><span class="sxs-lookup"><span data-stu-id="445f1-166">Time, in milliseconds, that the device will wait after receipt of the DFU_DETACH request.</span></span> <span data-ttu-id="445f1-167">Bu süre USB sıfırlaması olmadan geçtiğinde cihaz, yeniden yapılandırma aşamasını sonlandırır ve normal işleme geri döndürülür.</span><span class="sxs-lookup"><span data-stu-id="445f1-167">If this time elapses without a USB reset, then the device will terminate the Reconfiguration phase and revert back to normal operation.</span></span> <span data-ttu-id="445f1-168">Bu, cihazın bekleneceği maksimum süreyi (zamanlayıcılar, vb.) temsil eder.</span><span class="sxs-lookup"><span data-stu-id="445f1-168">This represents the maximum time that the device can wait (depending on its timers, etc.).</span></span> <span data-ttu-id="445f1-169">USBX bu değeri 1000 ms olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="445f1-169">USBX sets this value to 1000 ms.</span></span>  |
| <span data-ttu-id="445f1-170">wTransferSize</span><span class="sxs-lookup"><span data-stu-id="445f1-170">wTransferSize</span></span>  | <span data-ttu-id="445f1-171">5</span><span class="sxs-lookup"><span data-stu-id="445f1-171">5</span></span>      | <span data-ttu-id="445f1-172">2</span><span class="sxs-lookup"><span data-stu-id="445f1-172">2</span></span>  | <span data-ttu-id="445f1-173">sayı</span><span class="sxs-lookup"><span data-stu-id="445f1-173">number</span></span>    | <span data-ttu-id="445f1-174">Cihazın her denetim yazma işlemi için kabul edebileceği en fazla bayt sayısı \- .</span><span class="sxs-lookup"><span data-stu-id="445f1-174">Maximum number of bytes that the device can accept per control\-write operation.</span></span> <span data-ttu-id="445f1-175">USBX bu değeri 64 bayt olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="445f1-175">USBX sets this value to 64 bytes.</span></span> |

<span data-ttu-id="445f1-176">DFU sınıfının bildirimi aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="445f1-176">The declaration of the DFU class is as follows:</span></span>

```C
/* Store the DFU parameters. */

dfu_parameter.ux_slave_class_dfu_parameter_instance_activate =
    tx_demo_thread_dfu_activate;

dfu_parameter.ux_slave_class_dfu_parameter_instance_deactivate =
    tx_demo_thread_dfu_deactivate;

dfu_parameter.ux_slave_class_dfu_parameter_read =
    tx_demo_thread_dfu_read;

dfu_parameter.ux_slave_class_dfu_parameter_write =
    tx_demo_thread_dfu_write;

dfu_parameter.ux_slave_class_dfu_parameter_get_status =
    tx_demo_thread_dfu_get_status;

dfu_parameter.ux_slave_class_dfu_parameter_notify =
    tx_demo_thread_dfu_notify;

dfu_parameter.ux_slave_class_dfu_parameter_framework =
    device_framework_dfu;

dfu_parameter.ux_slave_class_dfu_parameter_framework_length =
    DEVICE_FRAMEWORK_LENGTH_DFU;

/* Initialize the device dfu class. The class is connected with interface
1 on configuration 1. */
status = ux_device_stack_class_register(_ux_system_slave_class_dfu_name,
    ux_device_class_dfu_entry, 1, 0,
    (VOID *)&dfu_parameter);

if (status!=UX_SUCCESS) return;
```

<span data-ttu-id="445f1-177">DFU sınıfının hedefe özgü bir cihaz üretici yazılımı uygulamasıyla çalışması gerekir.</span><span class="sxs-lookup"><span data-stu-id="445f1-177">The DFU class needs to work with a device firmware application specific to the target.</span></span> <span data-ttu-id="445f1-178">Bu nedenle, üretici yazılımının okuma ve yazma blokları ve bellenim güncelleştirme uygulamasından durum almak için birkaç geri çağrı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="445f1-178">Therefore it defines several call back to read and write blocks of firmware and to get status from the firmware update application.</span></span> <span data-ttu-id="445f1-179">DFU sınıfında Ayrıca, bellenimin bir başlangıç ve bitiş sonu gerçekleştiğinde uygulamayı bilgilendirmek için bir bildirim geri araması işlevi bulunur.</span><span class="sxs-lookup"><span data-stu-id="445f1-179">The DFU class also has a notify callback function to inform the application when a begin and end of transfer of the firmware occur.</span></span>

<span data-ttu-id="445f1-180">Tipik bir DFU uygulama akışının açıklaması aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="445f1-180">Following is the description of a typical DFU application flow.</span></span>

![DFU uygulama akışı](./media/usbx-device-stack-supplemental/dfu-application-flow.png)

<span data-ttu-id="445f1-182">DFU sınıfının önemli zorluğu, bellenime indirme işlemini gerçekleştirmek için konakta doğru uygulamayı almaktır.</span><span class="sxs-lookup"><span data-stu-id="445f1-182">The major challenge of the DFU class is getting the right application on the host to perform the download the firmware.</span></span> <span data-ttu-id="445f1-183">Microsoft veya USB-IF tarafından sağlanan bir uygulama yok.</span><span class="sxs-lookup"><span data-stu-id="445f1-183">There is no application supplied by Microsoft or the USB-IF.</span></span> <span data-ttu-id="445f1-184">Bazı paylaşılan yazılım var ve Linux 'ta ve Windows 'da daha düşük bir ölçüde iyi çalışır.</span><span class="sxs-lookup"><span data-stu-id="445f1-184">Some shareware exist and they work reasonably well on Linux and to a lesser extent on Windows.</span></span>

<span data-ttu-id="445f1-185">Linux 'ta, bir tane DFU-utils kullanarak burada bulunabilir: [https://wiki.openmoko.org/wiki/Dfu-util](https://wiki.openmoko.org/wiki/Dfu-util) Bu bağlantıda DFU yardımcı programları hakkında çok fazla bilgi bulunabilir: [https://www.libusb.org/wiki/windows_backend](https://www.libusb.org/wiki/windows_backend)</span><span class="sxs-lookup"><span data-stu-id="445f1-185">On Linux, one can use dfu-utils to be found here: [https://wiki.openmoko.org/wiki/Dfu-util](https://wiki.openmoko.org/wiki/Dfu-util) A lot of information on dfu utils can also be found on this link: [https://www.libusb.org/wiki/windows_backend](https://www.libusb.org/wiki/windows_backend)</span></span>

<span data-ttu-id="445f1-186">DFU 'nin Linux uygulamasına, ana bilgisayar ile cihaz arasındaki sıfırlama sırası doğru şekilde gerçekleştirilir ve bu nedenle cihazın bunu yapmasına gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="445f1-186">The Linux implementation of DFU performs correctly the reset sequence between the host and the device and therefore the device does not need to do it.</span></span> <span data-ttu-id="445f1-187">Linux, bmAttributes *Bitwilldetach* 0 olması için kabul edebilir.</span><span class="sxs-lookup"><span data-stu-id="445f1-187">Linux can accept for the bmAttributes *bitWillDetach* to be 0.</span></span> <span data-ttu-id="445f1-188">Diğer taraftan Windows, cihazın sıfırlamayı gerçekleştirmesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="445f1-188">Windows on the other side requires the device to perform the reset.</span></span>

<span data-ttu-id="445f1-189">Windows 'da, USB kayıt defteri, USB cihazını PID/VıD ve USB kitaplığı ile ilişkilendirebilmelidir ve bu da DFU uygulaması tarafından kullanılacaktır.</span><span class="sxs-lookup"><span data-stu-id="445f1-189">On Windows, the USB registry must be able to associate the USB device with its PID/VID and the USB library which will in turn be used by the DFU application.</span></span> <span data-ttu-id="445f1-190">Bu, burada bulunabilerek ücretsiz yardımcı program ile kolayca yapılabilir: [https://sourceforge.net/projects/libwdi/files/zadig/](https://sourceforge.net/projects/libwdi/files/zadig/) .</span><span class="sxs-lookup"><span data-stu-id="445f1-190">This can be easily done with the free utility Zadig which can be found here: [https://sourceforge.net/projects/libwdi/files/zadig/](https://sourceforge.net/projects/libwdi/files/zadig/).</span></span>

<span data-ttu-id="445f1-191">Zadig 'yi ilk kez çalıştırmak bu ekranı gösterecektir:</span><span class="sxs-lookup"><span data-stu-id="445f1-191">Running Zadig for the first time will show this screen:</span></span>

![Zadig 'yi ilk kez çalıştırma](./media/usbx-device-stack-supplemental/zadig.png)

<span data-ttu-id="445f1-193">Cihaz listesinden cihazınızı bulun ve lıbusb Windows sürücüsüyle ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="445f1-193">From the device list, find your device and associate it with the libusb windows driver.</span></span> <span data-ttu-id="445f1-194">Bu işlem, cihazın PID/VıD 'sini DFU yardımcı programları tarafından kullanılan Windows USB kitaplığıyla bağlar.</span><span class="sxs-lookup"><span data-stu-id="445f1-194">This will bind the PID/VID of the device with the Windows USB library used by the DFU utilities.</span></span>

<span data-ttu-id="445f1-195">DFU komutunu çalıştırmak için, yalnızca daraltılmış DFU yardımcı programlarının bir dizine paketini açmanız yeterlidir ve bu DLL 'nin aynı dizinde de bulunduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="445f1-195">To operate the DFU command, simply unpack the zipped dfu utilities into a directory, making sure the libusb dll is also present in the same directory.</span></span> <span data-ttu-id="445f1-196">DFU yardımcı programlarının komut satırındaki bir DOS kutusundan çalıştırılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="445f1-196">The DFU utilities must be run from a DOS box at the command line.</span></span>

<span data-ttu-id="445f1-197">İlk olarak, cihazın listelenip listelenmediğini öğrenmek için **DFU-Util – l** komutunu yazın.</span><span class="sxs-lookup"><span data-stu-id="445f1-197">First, type the command **dfu-util –l** to determine whether the device is listed.</span></span> <span data-ttu-id="445f1-198">Aksi takdirde, cihazın listelenmiş ve USB kitaplığıyla ilişkili olduğundan emin olmak için Zadig 'yi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="445f1-198">If not, run Zadig to make sure the device is listed and associated with the USB library.</span></span> <span data-ttu-id="445f1-199">Aşağıdaki gibi bir ekran görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="445f1-199">You should see a screen as follows:</span></span>

```Command-line
C:\usb specs\DFU\dfu-util-0.6&gt;dfu-util -l dfu-util 0.6

Copyright 2005-2008 Weston Schmidt, Harald Welte and OpenMoko Inc.
Copyright 2010-2012 Tormod Volden and Stefan Schmidt
This program is Free Software and has ABSOLUTELY NO WARRANTY
Found Runtime: [0a5c:21bc] devnum=0, cfg=1, intf=3, alt=0, name="UNDEFINED"
```

<span data-ttu-id="445f1-200">Sonraki adım, dosyayı indirilecek şekilde hazırlanacaktır.</span><span class="sxs-lookup"><span data-stu-id="445f1-200">The next step will be to prepare the file to be downloaded.</span></span> <span data-ttu-id="445f1-201">USBX DFU sınıfı, bu dosya üzerinde herhangi bir doğrulama gerçekleştirmez ve iç biçiminin bağımsız olduğunu göstermez.</span><span class="sxs-lookup"><span data-stu-id="445f1-201">The USBX DFU class does not perform any verification on this file and is agnostic of its internal format.</span></span> <span data-ttu-id="445f1-202">Bu üretici yazılımı dosyası hedefe özgü değildir ancak DFU 'ye veya USBX 'e uygulanmaz.</span><span class="sxs-lookup"><span data-stu-id="445f1-202">This firmware file is very specific to the target but not to DFU nor to USBX.</span></span>

<span data-ttu-id="445f1-203">Ardından, aşağıdaki komutu yazarak DFU-Util 'e dosyayı göndermek için talimat uygulanabilir:</span><span class="sxs-lookup"><span data-stu-id="445f1-203">Then the dfu-util can be instructed to send the file by typing the following command:</span></span>

```Command-line
dfu-util –R –t 64 -D file_to_download.hex
```

<span data-ttu-id="445f1-204">Yazılım yazılımı tamamen indirilene kadar DFU-Util dosya indirme işlemini görüntülemelidir.</span><span class="sxs-lookup"><span data-stu-id="445f1-204">The dfu-util should display the file download process until the firmware has been completely downloaded.</span></span>

## <a name="usb-device-pima-class-ptp-responder"></a><span data-ttu-id="445f1-205">USB cihaz PIMA sınıfı (PTP Yanıtlayıcısı)</span><span class="sxs-lookup"><span data-stu-id="445f1-205">USB Device PIMA Class (PTP Responder)</span></span>

<span data-ttu-id="445f1-206">USB cihaz PIMA sınıfı, bir USB ana bilgisayar sisteminin (Başlatıcı) bir cihaza bağlanmasını sağlar</span><span class="sxs-lookup"><span data-stu-id="445f1-206">The USB device PIMA class allows for a USB host system (Initiator) to connect to a</span></span>

<span data-ttu-id="445f1-207">Medya dosyalarını aktarmak için PIMA cihazı (Resonder).</span><span class="sxs-lookup"><span data-stu-id="445f1-207">PIMA device (Resonder) to transfer media files.</span></span> <span data-ttu-id="445f1-208">USBX Pima sınıfı, PTP class (resim aktarma protokolü için) olarak da bilinen USB-IF PIMA 15740 sınıfına yöneliktir.</span><span class="sxs-lookup"><span data-stu-id="445f1-208">USBX Pima Class is conforming to the USB-IF PIMA 15740 class also known as PTP class (for Picture Transfer Protocol).</span></span>

<span data-ttu-id="445f1-209">USBX Device Side PIMA sınıfı aşağıdaki işlemleri destekler.</span><span class="sxs-lookup"><span data-stu-id="445f1-209">USBX device side PIMA class supports the following operations.</span></span>

| <span data-ttu-id="445f1-210">İşlem kodu</span><span class="sxs-lookup"><span data-stu-id="445f1-210">Operation code</span></span>                                    | <span data-ttu-id="445f1-211">Değer</span><span class="sxs-lookup"><span data-stu-id="445f1-211">Value</span></span> | <span data-ttu-id="445f1-212">Açıklama</span><span class="sxs-lookup"><span data-stu-id="445f1-212">Description</span></span>                       |
|---------------------------------------------------|---------|-----------------------------------------------------|
| <span data-ttu-id="445f1-213">UX_DEVICE_CLASS_PIMA_OC_GET_DEVICE_INFO</span><span class="sxs-lookup"><span data-stu-id="445f1-213">UX_DEVICE_CLASS_PIMA_OC_GET_DEVICE_INFO</span></span>    | <span data-ttu-id="445f1-214">0x1001</span><span class="sxs-lookup"><span data-stu-id="445f1-214">0x1001</span></span>  | <span data-ttu-id="445f1-215">Desteklenen cihaz işlemlerini ve olayları edinin</span><span class="sxs-lookup"><span data-stu-id="445f1-215">Obtain the device supported operations and events</span></span>                                                         |
| <span data-ttu-id="445f1-216">UX_DEVICE_CLASS_PIMA_OC_OPEN_SESSION</span><span class="sxs-lookup"><span data-stu-id="445f1-216">UX_DEVICE_CLASS_PIMA_OC_OPEN_SESSION</span></span>        | <span data-ttu-id="445f1-217">0x1002</span><span class="sxs-lookup"><span data-stu-id="445f1-217">0x1002</span></span>  | <span data-ttu-id="445f1-218">Konak ve cihaz arasında bir oturum açın</span><span class="sxs-lookup"><span data-stu-id="445f1-218">Open a session between the host and the device</span></span>                                                            |
| <span data-ttu-id="445f1-219">UX_DEVICE_CLASS_PIMA_OC_CLOSE_SESSION</span><span class="sxs-lookup"><span data-stu-id="445f1-219">UX_DEVICE_CLASS_PIMA_OC_CLOSE_SESSION</span></span>       | <span data-ttu-id="445f1-220">0x1003</span><span class="sxs-lookup"><span data-stu-id="445f1-220">0x1003</span></span>  | <span data-ttu-id="445f1-221">Konak ve cihaz arasında bir oturumu kapatma</span><span class="sxs-lookup"><span data-stu-id="445f1-221">Close a session between the host and the device</span></span>                                                           |
| <span data-ttu-id="445f1-222">UX_DEVICE_CLASS_PIMA_OC_GET_STORAGE_IDS</span><span class="sxs-lookup"><span data-stu-id="445f1-222">UX_DEVICE_CLASS_PIMA_OC_GET_STORAGE_IDS</span></span>    | <span data-ttu-id="445f1-223">0x1004</span><span class="sxs-lookup"><span data-stu-id="445f1-223">0x1004</span></span>  | <span data-ttu-id="445f1-224">Cihazın depolama KIMLIĞINI döndürür.</span><span class="sxs-lookup"><span data-stu-id="445f1-224">Returns the storage ID for the device.</span></span> <span data-ttu-id="445f1-225">USBX PIMA yalnızca bir depolama KIMLIĞI kullanır</span><span class="sxs-lookup"><span data-stu-id="445f1-225">USBX PIMA uses one storage ID only</span></span> |
| <span data-ttu-id="445f1-226">UX_DEVICE_CLASS_PIMA_OC_GET_STORAGE_INFO</span><span class="sxs-lookup"><span data-stu-id="445f1-226">UX_DEVICE_CLASS_PIMA_OC_GET_STORAGE_INFO</span></span>   | <span data-ttu-id="445f1-227">0x1005</span><span class="sxs-lookup"><span data-stu-id="445f1-227">0x1005</span></span>  | <span data-ttu-id="445f1-228">Depolama nesnesi hakkında en fazla kapasite ve boş alan gibi bilgileri döndür</span><span class="sxs-lookup"><span data-stu-id="445f1-228">Return information about the storage object such as max capacity and free space</span></span>                           |
| <span data-ttu-id="445f1-229">UX_DEVICE_CLASS_PIMA_OC_GET_NUM_OBJECTS</span><span class="sxs-lookup"><span data-stu-id="445f1-229">UX_DEVICE_CLASS_PIMA_OC_GET_NUM_OBJECTS</span></span>    | <span data-ttu-id="445f1-230">0x1006</span><span class="sxs-lookup"><span data-stu-id="445f1-230">0x1006</span></span>  | <span data-ttu-id="445f1-231">Depolama cihazında bulunan nesne sayısını döndür</span><span class="sxs-lookup"><span data-stu-id="445f1-231">Return the number of objects contained in the storage device</span></span>                                              |
| <span data-ttu-id="445f1-232">UX_DEVICE_CLASS_PIMA_OC_GET_OBJECT_HANDLES</span><span class="sxs-lookup"><span data-stu-id="445f1-232">UX_DEVICE_CLASS_PIMA_OC_GET_OBJECT_HANDLES</span></span> | <span data-ttu-id="445f1-233">0x1007</span><span class="sxs-lookup"><span data-stu-id="445f1-233">0x1007</span></span>  | <span data-ttu-id="445f1-234">Depolama cihazında nesnelerin bir tanıtıcı dizisini döndürür</span><span class="sxs-lookup"><span data-stu-id="445f1-234">Return an array of handles of the objects on the storage device</span></span>                                           |
| <span data-ttu-id="445f1-235">UX_DEVICE_CLASS_PIMA_OC_GET_OBJECT_INFO</span><span class="sxs-lookup"><span data-stu-id="445f1-235">UX_DEVICE_CLASS_PIMA_OC_GET_OBJECT_INFO</span></span>    | <span data-ttu-id="445f1-236">0x1008</span><span class="sxs-lookup"><span data-stu-id="445f1-236">0x1008</span></span>  | <span data-ttu-id="445f1-237">Nesnenin adı, Oluşturulma tarihi, değiştirilme tarihi gibi bir nesneyle ilgili bilgileri döndürür</span><span class="sxs-lookup"><span data-stu-id="445f1-237">Return information about an object such as the name of the object, its creation date, modification date</span></span> |
| <span data-ttu-id="445f1-238">UX_DEVICE_CLASS_PIMA_OC_GET_OBJECT</span><span class="sxs-lookup"><span data-stu-id="445f1-238">UX_DEVICE_CLASS_PIMA_OC_GET_OBJECT</span></span>          | <span data-ttu-id="445f1-239">0x1009</span><span class="sxs-lookup"><span data-stu-id="445f1-239">0x1009</span></span>  | <span data-ttu-id="445f1-240">Belirli bir nesneyle ilgili verileri döndürür</span><span class="sxs-lookup"><span data-stu-id="445f1-240">Return the data pertaining to a specific object</span></span>                                                         |
| <span data-ttu-id="445f1-241">UX_DEVICE_CLASS_PIMA_OC_GET_THUMB</span><span class="sxs-lookup"><span data-stu-id="445f1-241">UX_DEVICE_CLASS_PIMA_OC_GET_THUMB</span></span>           | <span data-ttu-id="445f1-242">0x100A</span><span class="sxs-lookup"><span data-stu-id="445f1-242">0x100A</span></span>  | <span data-ttu-id="445f1-243">Bir nesne hakkında kullanılabiliyorsa küçük resmi gönder</span><span class="sxs-lookup"><span data-stu-id="445f1-243">Send the thumbnail if available about an object</span></span>                                                           |
| <span data-ttu-id="445f1-244">UX_DEVICE_CLASS_PIMA_OC_DELETE_OBJECT</span><span class="sxs-lookup"><span data-stu-id="445f1-244">UX_DEVICE_CLASS_PIMA_OC_DELETE_OBJECT</span></span>       | <span data-ttu-id="445f1-245">0x100B</span><span class="sxs-lookup"><span data-stu-id="445f1-245">0x100B</span></span>  | <span data-ttu-id="445f1-246">Medyadaki bir nesneyi silme</span><span class="sxs-lookup"><span data-stu-id="445f1-246">Delete an object on the media</span></span>                                                                             |
| <span data-ttu-id="445f1-247">UX_DEVICE_CLASS_PIMA_OC_SEND_OBJECT_INFO</span><span class="sxs-lookup"><span data-stu-id="445f1-247">UX_DEVICE_CLASS_PIMA_OC_SEND_OBJECT_INFO</span></span>   | <span data-ttu-id="445f1-248">0x100C</span><span class="sxs-lookup"><span data-stu-id="445f1-248">0x100C</span></span>  | <span data-ttu-id="445f1-249">Medyada oluşturulması için bir nesneyle ilgili cihaz bilgilerine gönderin</span><span class="sxs-lookup"><span data-stu-id="445f1-249">Send to the device information about an object for its creation on the media</span></span>                              |
| <span data-ttu-id="445f1-250">UX_DEVICE_CLASS_PIMA_OC_SEND_OBJECT</span><span class="sxs-lookup"><span data-stu-id="445f1-250">UX_DEVICE_CLASS_PIMA_OC_SEND_OBJECT</span></span>         | <span data-ttu-id="445f1-251">0x100D</span><span class="sxs-lookup"><span data-stu-id="445f1-251">0x100D</span></span>  | <span data-ttu-id="445f1-252">Bir nesne için verileri cihaza gönderme</span><span class="sxs-lookup"><span data-stu-id="445f1-252">Send data for an object to the device</span></span>                                                                     |
| <span data-ttu-id="445f1-253">UX_DEVICE_CLASS_PIMA_OC_FORMAT_STORE</span><span class="sxs-lookup"><span data-stu-id="445f1-253">UX_DEVICE_CLASS_PIMA_OC_FORMAT_STORE</span></span>        | <span data-ttu-id="445f1-254">0x100F</span><span class="sxs-lookup"><span data-stu-id="445f1-254">0x100F</span></span>  | <span data-ttu-id="445f1-255">Cihaz medyasını Temizleme</span><span class="sxs-lookup"><span data-stu-id="445f1-255">Clean the device media</span></span>                                                                                    |
| <span data-ttu-id="445f1-256">UX_DEVICE_CLASS_PIMA_OC_RESET_DEVICE</span><span class="sxs-lookup"><span data-stu-id="445f1-256">UX_DEVICE_CLASS_PIMA_OC_RESET_DEVICE</span></span>        | <span data-ttu-id="445f1-257">0x0110</span><span class="sxs-lookup"><span data-stu-id="445f1-257">0x0110</span></span>  | <span data-ttu-id="445f1-258">Hedef cihazı sıfırlayın</span><span class="sxs-lookup"><span data-stu-id="445f1-258">Reset the target device</span></span>                                                                                   |

| <span data-ttu-id="445f1-259">İşlem kodu</span><span class="sxs-lookup"><span data-stu-id="445f1-259">Operation Code</span></span>                                         | <span data-ttu-id="445f1-260">Değer</span><span class="sxs-lookup"><span data-stu-id="445f1-260">Value</span></span> | <span data-ttu-id="445f1-261">Açıklama</span><span class="sxs-lookup"><span data-stu-id="445f1-261">Description</span></span> |
|--------------------------------------------------------|-------|-----------------------------------------|
| <span data-ttu-id="445f1-262">UX_DEVICE_CLASS_PIMA_EC_CANCEL_TRANSACTION</span><span class="sxs-lookup"><span data-stu-id="445f1-262">UX_DEVICE_CLASS_PIMA_EC_CANCEL_TRANSACTION</span></span>       | <span data-ttu-id="445f1-263">0x4001</span><span class="sxs-lookup"><span data-stu-id="445f1-263">0x4001</span></span>  | <span data-ttu-id="445f1-264">Geçerli işlemi iptal eder</span><span class="sxs-lookup"><span data-stu-id="445f1-264">Cancels the current transaction</span></span>                                                 |
| <span data-ttu-id="445f1-265">UX_DEVICE_CLASS_PIMA_EC_OBJECT_ADDED</span><span class="sxs-lookup"><span data-stu-id="445f1-265">UX_DEVICE_CLASS_PIMA_EC_OBJECT_ADDED</span></span>             | <span data-ttu-id="445f1-266">0x4002</span><span class="sxs-lookup"><span data-stu-id="445f1-266">0x4002</span></span>  | <span data-ttu-id="445f1-267">Cihaz medyasına bir nesne eklenmiştir ve bu, host\tarafından alınabilir.</span><span class="sxs-lookup"><span data-stu-id="445f1-267">An object has been added to the device media and can be retrieved by the host\.</span></span> |
| <span data-ttu-id="445f1-268">UX_DEVICE_CLASS_PIMA_EC_OBJECT_REMOVED</span><span class="sxs-lookup"><span data-stu-id="445f1-268">UX_DEVICE_CLASS_PIMA_EC_OBJECT_REMOVED</span></span>           | <span data-ttu-id="445f1-269">0x4003</span><span class="sxs-lookup"><span data-stu-id="445f1-269">0x4003</span></span>  | <span data-ttu-id="445f1-270">Cihaz medyasından bir nesne silindi</span><span class="sxs-lookup"><span data-stu-id="445f1-270">An object has been deleted from the device media</span></span>                                |
| <span data-ttu-id="445f1-271">UX_DEVICE_CLASS_PIMA_EC_STORE_ADDED</span><span class="sxs-lookup"><span data-stu-id="445f1-271">UX_DEVICE_CLASS_PIMA_EC_STORE_ADDED</span></span>              | <span data-ttu-id="445f1-272">0x4004</span><span class="sxs-lookup"><span data-stu-id="445f1-272">0x4004</span></span>  | <span data-ttu-id="445f1-273">Cihaza medya eklendi</span><span class="sxs-lookup"><span data-stu-id="445f1-273">A media has been added to the device</span></span>                                            |
| <span data-ttu-id="445f1-274">UX_DEVICE_CLASS_PIMA_EC_STORE_REMOVED</span><span class="sxs-lookup"><span data-stu-id="445f1-274">UX_DEVICE_CLASS_PIMA_EC_STORE_REMOVED</span></span>            | <span data-ttu-id="445f1-275">0x4005</span><span class="sxs-lookup"><span data-stu-id="445f1-275">0x4005</span></span>  | <span data-ttu-id="445f1-276">Cihazdan bir medya silindi</span><span class="sxs-lookup"><span data-stu-id="445f1-276">A media has been deleted from the device</span></span>                                        |
| <span data-ttu-id="445f1-277">UX_DEVICE_CLASS_PIMA_EC_DEVICE_PROP_CHANGED</span><span class="sxs-lookup"><span data-stu-id="445f1-277">UX_DEVICE_CLASS_PIMA_EC_DEVICE_PROP_CHANGED</span></span>     | <span data-ttu-id="445f1-278">0x4006</span><span class="sxs-lookup"><span data-stu-id="445f1-278">0x4006</span></span>  | <span data-ttu-id="445f1-279">Cihaz özellikleri değiştirildi</span><span class="sxs-lookup"><span data-stu-id="445f1-279">Device properties have changed</span></span>                                                  |
| <span data-ttu-id="445f1-280">UX_DEVICE_CLASS_PIMA_EC_OBJECT_INFO_CHANGED</span><span class="sxs-lookup"><span data-stu-id="445f1-280">UX_DEVICE_CLASS_PIMA_EC_OBJECT_INFO_CHANGED</span></span>     | <span data-ttu-id="445f1-281">0x4007</span><span class="sxs-lookup"><span data-stu-id="445f1-281">0x4007</span></span>  | <span data-ttu-id="445f1-282">Bir nesne bilgisi değişti</span><span class="sxs-lookup"><span data-stu-id="445f1-282">An object information has changed</span></span>                                               |
| <span data-ttu-id="445f1-283">UX_DEVICE_CLASS_PIMA_EC_DEVICE_INFO_CHANGE</span><span class="sxs-lookup"><span data-stu-id="445f1-283">UX_DEVICE_CLASS_PIMA_EC_DEVICE_INFO_CHANGE</span></span>      | <span data-ttu-id="445f1-284">0x4008</span><span class="sxs-lookup"><span data-stu-id="445f1-284">0x4008</span></span>  | <span data-ttu-id="445f1-285">Bir cihaz değiştirildi</span><span class="sxs-lookup"><span data-stu-id="445f1-285">A device has changed</span></span>                                                            |
| <span data-ttu-id="445f1-286">UX_DEVICE_CLASS_PIMA_EC_REQUEST_OBJECT_TRANSFER</span><span class="sxs-lookup"><span data-stu-id="445f1-286">UX_DEVICE_CLASS_PIMA_EC_REQUEST_OBJECT_TRANSFER</span></span> | <span data-ttu-id="445f1-287">0x4009</span><span class="sxs-lookup"><span data-stu-id="445f1-287">0x4009</span></span>  | <span data-ttu-id="445f1-288">Cihaz, konaktan bir nesne aktarımını ister</span><span class="sxs-lookup"><span data-stu-id="445f1-288">The device requests the transfer of an object from the host</span></span>                     |
| <span data-ttu-id="445f1-289">UX_DEVICE_CLASS_PIMA_EC_STORE_FULL</span><span class="sxs-lookup"><span data-stu-id="445f1-289">UX_DEVICE_CLASS_PIMA_EC_STORE_FULL</span></span>               | <span data-ttu-id="445f1-290">0x400A</span><span class="sxs-lookup"><span data-stu-id="445f1-290">0x400A</span></span>  | <span data-ttu-id="445f1-291">Ortam dolu cihaz raporları</span><span class="sxs-lookup"><span data-stu-id="445f1-291">Device reports the media is full</span></span>                                                |
| <span data-ttu-id="445f1-292">UX_DEVICE_CLASS_PIMA_EC_DEVICE_RESET</span><span class="sxs-lookup"><span data-stu-id="445f1-292">UX_DEVICE_CLASS_PIMA_EC_DEVICE_RESET</span></span>             | <span data-ttu-id="445f1-293">0x400B</span><span class="sxs-lookup"><span data-stu-id="445f1-293">0x400B</span></span>  | <span data-ttu-id="445f1-294">Sıfırlanan cihaz raporları</span><span class="sxs-lookup"><span data-stu-id="445f1-294">Device reports it was reset</span></span>                                                     |
| <span data-ttu-id="445f1-295">UX_DEVICE_CLASS_PIMA_EC_STORAGE_INFO_CHANGED</span><span class="sxs-lookup"><span data-stu-id="445f1-295">UX_DEVICE_CLASS_PIMA_EC_STORAGE_INFO_CHANGED</span></span>    | <span data-ttu-id="445f1-296">0x400C</span><span class="sxs-lookup"><span data-stu-id="445f1-296">0x400C</span></span>  | <span data-ttu-id="445f1-297">Cihazda depolama bilgileri değişti</span><span class="sxs-lookup"><span data-stu-id="445f1-297">Storage information has changed on the device</span></span>                                   |
| <span data-ttu-id="445f1-298">UX_DEVICE_CLASS_PIMA_EC_CAPTURE_COMPLETE</span><span class="sxs-lookup"><span data-stu-id="445f1-298">UX_DEVICE_CLASS_PIMA_EC_CAPTURE_COMPLETE</span></span>         | <span data-ttu-id="445f1-299">0x400D</span><span class="sxs-lookup"><span data-stu-id="445f1-299">0x400D</span></span>  | <span data-ttu-id="445f1-300">Yakalama tamamlandı</span><span class="sxs-lookup"><span data-stu-id="445f1-300">Capture is completed</span></span>                                                            |

<span data-ttu-id="445f1-301">USBX PIMA cihaz sınıfı, konaktan PIMA komutlarını dinlemek için bir TX Iş parçacığı kullanır.</span><span class="sxs-lookup"><span data-stu-id="445f1-301">The USBX PIMA device class uses a TX Thread to listen to PIMA commands from the host.</span></span>

<span data-ttu-id="445f1-302">Bir PIMA komutu bir komut bloğundan, bir veri bloğundan ve bir durum aşamasından oluşur.</span><span class="sxs-lookup"><span data-stu-id="445f1-302">A PIMA command is composed of a command block, a data block and a status phase.</span></span>

<span data-ttu-id="445f1-303">İşlev ux_device_class_pima_thread, ana bilgisayar tarafında bir PIMA komutu almak için yığına bir istek gönderir.</span><span class="sxs-lookup"><span data-stu-id="445f1-303">The function ux_device_class_pima_thread posts a request to the stack to receive a PIMA command from the host side.</span></span> <span data-ttu-id="445f1-304">PIMA komutunun kodu çözüldü ve içerik için doğrulanır.</span><span class="sxs-lookup"><span data-stu-id="445f1-304">The PIMA command is decoded and verified for content.</span></span> <span data-ttu-id="445f1-305">Komut bloğu geçerliyse, uygun komut işleyicisine dallandırır.</span><span class="sxs-lookup"><span data-stu-id="445f1-305">If the command block is valid, it branches to the appropriate command handler.</span></span>

<span data-ttu-id="445f1-306">Çoğu PIMA komutları yalnızca, ana bilgisayar tarafından bir oturum açıldığında yürütülebilir.</span><span class="sxs-lookup"><span data-stu-id="445f1-306">Most PIMA commands can only be executed when a session has been opened by the host.</span></span> <span data-ttu-id="445f1-307">Tek özel durum, komut **UX_DEVICE_CLASS_PIMA_OC_GET_DEVICE_INFO**.</span><span class="sxs-lookup"><span data-stu-id="445f1-307">The only exception is the command **UX_DEVICE_CLASS_PIMA_OC_GET_DEVICE_INFO**.</span></span> <span data-ttu-id="445f1-308">USBX PIMA uygulamasıyla, her zaman bir başlatıcı ve Yanıtlayıcı arasında yalnızca bir oturum açılabilir.</span><span class="sxs-lookup"><span data-stu-id="445f1-308">With USBX PIMA implementation, only one session can be opened between an Initiator and Responder at any time.</span></span> <span data-ttu-id="445f1-309">Tek oturumdaki tüm işlemler engelleniyor ve önceki işlem tamamlanmadan önce yeni bir işlem başlayabilirler.</span><span class="sxs-lookup"><span data-stu-id="445f1-309">All transactions within the single session are blocking and no new transaction can begin before the previous one completed.</span></span>

<span data-ttu-id="445f1-310">PIMA işlemleri 3 aşamadan, bir komut aşamasına, isteğe bağlı bir veri aşamasına ve bir yanıt aşamasına göre oluşur.</span><span class="sxs-lookup"><span data-stu-id="445f1-310">PIMA transactions are composed of 3 phases, a command phase, an optional data phase and a response phase.</span></span> <span data-ttu-id="445f1-311">Bir veri aşaması varsa, yalnızca bir yönde olabilir.</span><span class="sxs-lookup"><span data-stu-id="445f1-311">If a data phase is present, it can only be in one direction.</span></span>

<span data-ttu-id="445f1-312">Başlatıcı her zaman PIMA işlemlerinin akışını belirler ancak Yanıtlayıcı, bir oturum sırasında gerçekleşen durum değişikliklerini bilgilendirmek için olayları başlatıcıya geri başlatabilir.</span><span class="sxs-lookup"><span data-stu-id="445f1-312">The Initiator always determines the flow of the PIMA operations but the Responder can initiate events back to the Initiator to inform status changes that happened during a session.</span></span>

<span data-ttu-id="445f1-313">Aşağıdaki diyagramda, ana bilgisayar ve PIMA cihaz sınıfı arasında bir veri nesnesinin aktarımı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="445f1-313">The following diagram shows the transfer of a data object between the host and the PIMA device class.</span></span>

![PIMA işlemleri](./media/usbx-device-stack-supplemental/pima-transactions.png)

## <a name="initialization-of-the-pima-device-class"></a><span data-ttu-id="445f1-315">PIMA cihaz sınıfının başlatılması</span><span class="sxs-lookup"><span data-stu-id="445f1-315">Initialization of the PIMA device class</span></span>

<span data-ttu-id="445f1-316">PIMA cihaz sınıfı, başlatma sırasında uygulama tarafından sağlanan bazı parametrelere ihtiyaç duyuyor.</span><span class="sxs-lookup"><span data-stu-id="445f1-316">The PIMA device class needs some parameters supplied by the application during the initialization.</span></span>

<span data-ttu-id="445f1-317">Aşağıdaki parametreler cihaz ve depolama bilgilerini anlatmaktadır.</span><span class="sxs-lookup"><span data-stu-id="445f1-317">The following parameters describe the device and storage information.</span></span>

- `ux_device_class_pima_manufacturer`
- `ux_device_class_pima_model`
- `ux_device_class_pima_device_version`
- `ux_device_class_pima_serial_number`
- `ux_device_class_pima_storage_id`
- `ux_device_class_pima_storage_type`
- `ux_device_class_pima_storage_file_system_type`
- `ux_device_class_pima_storage_access_capability`
- `ux_device_class_pima_storage_max_capacity_low`
- `ux_device_class_pima_storage_max_capacity_high`
- `ux_device_class_pima_storage_free_space_low`
- `ux_device_class_pima_storage_free_space_high`
- `ux_device_class_pima_storage_free_space_image`
- `ux_device_class_pima_storage_description`
- `ux_device_class_pima_storage_volume_label`

<span data-ttu-id="445f1-318">IZMA sınıfı ayrıca belirli olayları bilgilendirmek veya yerel medyadan veri almak/depolamak için uygulamaya geri çağırma kaydı yapılmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="445f1-318">The PIMA class also requires the registration of callback into the application to inform the application of certain events or retrieve/store data from/to the local media.</span></span> <span data-ttu-id="445f1-319">Geri çağrılar aşağıdaki gibidir.</span><span class="sxs-lookup"><span data-stu-id="445f1-319">The callbacks are as follows.</span></span>

- `ux_device_class_pima_object_number_get`
- `ux_device_class_pima_object_handles_get`
- `ux_device_class_pima_object_info_get`
- `ux_device_class_pima_object_data_get`
- `ux_device_class_pima_object_info_send`
- `ux_device_class_pima_object_data_send`
- `ux_device_class_pima_object_delete`

<span data-ttu-id="445f1-320">Aşağıdaki örnekte, PIMA 'nın istemci tarafının nasıl başlatıldığı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="445f1-320">The following example shows how to initialize the client side of PIMA.</span></span> <span data-ttu-id="445f1-321">Bu örnek, PIMA için istemci olarak PictBridge kullanır.</span><span class="sxs-lookup"><span data-stu-id="445f1-321">This example uses Pictbridge as a client for PIMA.</span></span>

```C
/* Initialize the first XML object valid in the pictbridge instance.

Initialize the handle, type and file name.

The storage handle and the object handle have a fixed value of 1 in our implementation. */

object_info = pictbridge -> ux_pictbridge_object_client;

object_info -> ux_device_class_pima_object_format = UX_DEVICE_CLASS_PIMA_OFC_SCRIPT;
object_info -> ux_device_class_pima_object_storage_id = 1;
object_info -> ux_device_class_pima_object_handle_id = 2;

ux_utility_string_to_unicode(_ux_pictbridge_ddiscovery_name,
    object_info -> ux_device_class_pima_object_filename);

/* Initialize the head and tail of the notification round robin buffers.
   At first, the head and tail are pointing to the beginning of the array.
*/

pictbridge -> ux_pictbridge_event_array_head =
    pictbridge -> ux_pictbridge_event_array;

pictbridge -> ux_pictbridge_event_array_tail =
    pictbridge -> ux_pictbridge_event_array;

pictbridge -> ux_pictbridge_event_array_end =
    pictbridge -> ux_pictbridge_event_array +
    UX_PICTBRIDGE_MAX_EVENT_NUMBER;

/* Initialialize the pima device parameter. */
pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_manufacturer =
    pictbridge -> ux_pictbridge_dpslocal.ux_pictbridge_devinfo_vendor_name;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_model =
    pictbridge -> ux_pictbridge_dpslocal.ux_pictbridge_devinfo_product_name;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_serial_number =
    pictbridge -> ux_pictbridge_dpslocal.ux_pictbridge_devinfo_serial_no;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_storage_id = 1;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_storage_type =
    UX_DEVICE_CLASS_PIMA_STC_FIXED_RAM;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_storage_file_system_type =
    UX_DEVICE_CLASS_PIMA_FSTC_GENERIC_FLAT;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_storage_access_capability =
    UX_DEVICE_CLASS_PIMA_AC_READ_WRITE;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_storage_max_capacity_low =
    pictbridge -> ux_pictbridge_dpslocal.ux_pictbridge_devinfo_storage_size;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_storage_max_capacity_high = 0;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_storage_free_space_low =
    pictbridge -> ux_pictbridge_dpslocal.ux_pictbridge_devinfo_storage_size;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_storage_free_space_high = 0;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_storage_free_space_image = 0;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_storage_description =
    _ux_pictbridge_volume_description;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_storage_volume_label =
    _ux_pictbridge_volume_label;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_object_number_get =
    ux_pictbridge_dpsclient_object_number_get;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_object_handles_get =
    ux_pictbridge_dpsclient_object_handles_get;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_object_info_get =
    ux_pictbridge_dpsclient_object_info_get;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_object_data_get =
    ux_pictbridge_dpsclient_object_data_get;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_object_info_send =
    ux_pictbridge_dpsclient_object_info_send;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_object_data_send =
    ux_pictbridge_dpsclient_object_data_send;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_object_delete =
    ux_pictbridge_dpsclient_object_delete;

/* Store the instance owner. */
pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_application =
    (VOID *) pictbridge;

/* Initialize the device pima class. The class is connected with interface 0 */

status = ux_device_stack_class_register(_ux_system_slave_class_pima_name,
    ux_device_class_pima_entry, 1, 0, (VOID *)&pictbridge -> ux_pictbridge_pima_parameter);

/* Check status. */
if (status != UX_SUCCESS)
```

## <a name="ux_device_class_pima_object_add"></a><span data-ttu-id="445f1-322">ux_device_class_pima_object_add</span><span class="sxs-lookup"><span data-stu-id="445f1-322">ux_device_class_pima_object_add</span></span>

<span data-ttu-id="445f1-323">Bir nesne ekleme ve olayı konağa gönderme</span><span class="sxs-lookup"><span data-stu-id="445f1-323">Adding an object and sending the event to the host</span></span>

### <a name="prototype"></a><span data-ttu-id="445f1-324">Prototype</span><span class="sxs-lookup"><span data-stu-id="445f1-324">Prototype</span></span>

```C
UINT ux_device_class_pima_object_add(
    UX_SLAVE_CLASS_PIMA *pima, 
    ULONG object_handle);
```

### <a name="description"></a><span data-ttu-id="445f1-325">Description</span><span class="sxs-lookup"><span data-stu-id="445f1-325">Description</span></span>

<span data-ttu-id="445f1-326">Bu işlev, PIMA sınıfının bir nesne eklemesi ve Konağı bilgilendirilmesi gerektiğinde çağrılır.</span><span class="sxs-lookup"><span data-stu-id="445f1-326">This function is called when the PIMA class needs to add an object and inform the host.</span></span>

### <a name="parameters"></a><span data-ttu-id="445f1-327">Parametreler</span><span class="sxs-lookup"><span data-stu-id="445f1-327">Parameters</span></span>

- <span data-ttu-id="445f1-328">**Pima**: Pima sınıfı örneğine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="445f1-328">**pima**: Pointer to the pima class instance</span></span>
- <span data-ttu-id="445f1-329">**object_handle**: nesnenin tanıtıcısı.</span><span class="sxs-lookup"><span data-stu-id="445f1-329">**object_handle**: Handle of the object.</span></span>

### <a name="example"></a><span data-ttu-id="445f1-330">Örnek</span><span class="sxs-lookup"><span data-stu-id="445f1-330">Example</span></span>

```C
/* Send the notification to the host that an object has been added. */

status = ux_device_class_pima_object_add(pima, UX_PICTBRIDGE_OBJECT_HANDLE_CLIENT_REQUEST);
```

## <a name="ux_device_class_pima_object_number_get"></a><span data-ttu-id="445f1-331">ux_device_class_pima_object_number_get</span><span class="sxs-lookup"><span data-stu-id="445f1-331">ux_device_class_pima_object_number_get</span></span>

<span data-ttu-id="445f1-332">Uygulamadan nesne numarası alma</span><span class="sxs-lookup"><span data-stu-id="445f1-332">Getting the object number from the application</span></span>

### <a name="prototype"></a><span data-ttu-id="445f1-333">Prototype</span><span class="sxs-lookup"><span data-stu-id="445f1-333">Prototype</span></span>

```C
UINT ux_device_class_pima_object_number_get(
    UX_SLAVE_CLASS_PIMA *pima, 
    ULONG *object_number);
```

### <a name="description"></a><span data-ttu-id="445f1-334">Description</span><span class="sxs-lookup"><span data-stu-id="445f1-334">Description</span></span>

<span data-ttu-id="445f1-335">Bu işlev, PIMA sınıfının yerel sistemdeki nesne sayısını alması ve konağa geri göndermek için gerektiğinde çağrılır.</span><span class="sxs-lookup"><span data-stu-id="445f1-335">This function is called when the PIMA class needs to retrieve the number of objects in the local system and send it back to the host.</span></span>

### <a name="parameters"></a><span data-ttu-id="445f1-336">Parametreler</span><span class="sxs-lookup"><span data-stu-id="445f1-336">Parameters</span></span>

- <span data-ttu-id="445f1-337">**Pima**: Pima sınıfı örneğine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="445f1-337">**pima**: Pointer to the pima class instance</span></span>
- <span data-ttu-id="445f1-338">**object_number**: döndürülecek nesne sayısının adresi</span><span class="sxs-lookup"><span data-stu-id="445f1-338">**object_number**: Address of the number of objects to be returned</span></span>

### <a name="example"></a><span data-ttu-id="445f1-339">Örnek</span><span class="sxs-lookup"><span data-stu-id="445f1-339">Example</span></span>

```C
UINT ux_pictbridge_dpsclient_object_number_get(UX_SLAVE_CLASS_PIMA *pima, ULONG *number_objects)
{
    /* We force the number of objects to be 1 only here. This will be the XML scripts. */
    *number_objects = 1;
    return(UX_SUCCESS);
}
```

## <a name="ux_device_class_pima_object_handles_get"></a><span data-ttu-id="445f1-340">ux_device_class_pima_object_handles_get</span><span class="sxs-lookup"><span data-stu-id="445f1-340">ux_device_class_pima_object_handles_get</span></span>

<span data-ttu-id="445f1-341">Nesne tutamacı dizisini döndürün</span><span class="sxs-lookup"><span data-stu-id="445f1-341">Return the object handle array</span></span>

### <a name="prototype"></a><span data-ttu-id="445f1-342">Prototype</span><span class="sxs-lookup"><span data-stu-id="445f1-342">Prototype</span></span>

```C
UINT **ux_device_class_pima_object_handles_get**(
    UX_SLAVE_CLASS_PIMA_STRUCT *pima,
    ULONG object_handles_format_code,
    ULONG object_handles_association,
    ULONG *object_handles_array,
    ULONG object_handles_max_number);
```

### <a name="description"></a><span data-ttu-id="445f1-343">Description</span><span class="sxs-lookup"><span data-stu-id="445f1-343">Description</span></span>

<span data-ttu-id="445f1-344">Bu işlev, PIMA sınıfının, yerel sistemde nesne işleyicileri dizisini alması ve konağa geri gönderebilmesi gerektiğinde çağrılır.</span><span class="sxs-lookup"><span data-stu-id="445f1-344">This function is called when the PIMA class needs to retrieve the object handles array in the local system and send it back to the host.</span></span>

### <a name="parameters"></a><span data-ttu-id="445f1-345">Parametreler</span><span class="sxs-lookup"><span data-stu-id="445f1-345">Parameters</span></span>

- <span data-ttu-id="445f1-346">**Pima**: Pima sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="445f1-346">**pima**: Pointer to the pima class instance.</span></span>
- <span data-ttu-id="445f1-347">**object_handles_format_code**: tutamaçlar için kodu Biçimlendir</span><span class="sxs-lookup"><span data-stu-id="445f1-347">**object_handles_format_code**: Format code for the handles</span></span>
- <span data-ttu-id="445f1-348">**object_handles_association**: nesne ilişkilendirme kodu</span><span class="sxs-lookup"><span data-stu-id="445f1-348">**object_handles_association**: Object association code</span></span>
- <span data-ttu-id="445f1-349">**object_handle_array**: tanıtıcıların depolanacağı adres</span><span class="sxs-lookup"><span data-stu-id="445f1-349">**object_handle_array**: Address where to store the handles</span></span>
- <span data-ttu-id="445f1-350">**object_handles_max_number**: dizideki en fazla tanıtıcı sayısı</span><span class="sxs-lookup"><span data-stu-id="445f1-350">**object_handles_max_number**: Maximum number of handles in the array</span></span>

### <a name="example"></a><span data-ttu-id="445f1-351">Örnek</span><span class="sxs-lookup"><span data-stu-id="445f1-351">Example</span></span>

```C
UINT ux_pictbridge_dpsclient_object_handles_get(UX_SLAVE_CLASS_PIMA *pima,
    ULONG object_handles_format_code,
    ULONG object_handles_association,
    ULONG *object_handles_array,
    ULONG object_handles_max_number)
{

    UX_PICTBRIDGE *pictbridge;
    UX_SLAVE_CLASS_PIMA_OBJECT *object_info;

    /* Get the pointer to the Pictbridge instance. */
    pictbridge = (UX_PICTBRIDGE *) pima -> ux_device_class_pima_application;

    /* Set the pima pointer to the pictbridge instance. */
    pictbridge -> ux_pictbridge_pima = (VOID *) pima;

    /* We say we have one object but the caller might specify different format code and associations. */
    object_info = pictbridge -> ux_pictbridge_object_client;

    /* Insert in the array the number of found handles so far: 0. */
    ux_utility_long_put((UCHAR *)object_handles_array, 0);

    /* Check the type demanded. */

    if (object_handles_format_code == 0 || object_handles_format_code ==
        0xFFFFFFFF || object_info -> ux_device_class_pima_object_format ==
        object_handles_format_code)
    {
        /* Insert in the array the number of found handles. This handle is for the client XML script. */
        ux_utility_long_put((UCHAR *)object_handles_array, 1);

        /* Adjust the array to point after the number of elements. */
        object_handles_array++;

        /* We have a candicate. Store the handle. */
        ux_utility_long_put((UCHAR *)object_handles_array, object_info ->
            ux_device_class_pima_object_handle_id);
    }

    return(UX_SUCCESS);
}
```

## <a name="ux_device_class_pima_object_info_get"></a><span data-ttu-id="445f1-352">ux_device_class_pima_object_info_get</span><span class="sxs-lookup"><span data-stu-id="445f1-352">ux_device_class_pima_object_info_get</span></span>

<span data-ttu-id="445f1-353">Nesne bilgilerini döndürme</span><span class="sxs-lookup"><span data-stu-id="445f1-353">Return the object information</span></span>

### <a name="prototype"></a><span data-ttu-id="445f1-354">Prototype</span><span class="sxs-lookup"><span data-stu-id="445f1-354">Prototype</span></span>

```C
UINT ux_device_class_pima_object_info_get(
    struct UX_SLAVE_CLASS_PIMA_STRUCT *pima,
    ULONG object_handle, 
    UX_SLAVE_CLASS_PIMA_OBJECT **object);
```

### <a name="description"></a><span data-ttu-id="445f1-355">Description</span><span class="sxs-lookup"><span data-stu-id="445f1-355">Description</span></span>

<span data-ttu-id="445f1-356">Bu işlev, PIMA sınıfının, yerel sistemde nesne işleyicileri dizisini alması ve konağa geri gönderebilmesi gerektiğinde çağrılır.</span><span class="sxs-lookup"><span data-stu-id="445f1-356">This function is called when the PIMA class needs to retrieve the object handles array in the local system and send it back to the host.</span></span>

### <a name="parameters"></a><span data-ttu-id="445f1-357">Parametreler</span><span class="sxs-lookup"><span data-stu-id="445f1-357">Parameters</span></span>

- <span data-ttu-id="445f1-358">**Pima**: Pima sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="445f1-358">**pima**: Pointer to the pima class instance.</span></span>
- <span data-ttu-id="445f1-359">**object_handles**: nesnenin tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="445f1-359">**object_handles**: Handle of the object</span></span>
- <span data-ttu-id="445f1-360">**nesne**: nesne işaretçisi adresi</span><span class="sxs-lookup"><span data-stu-id="445f1-360">**object**: Object pointer address</span></span>

### <a name="example"></a><span data-ttu-id="445f1-361">Örnek</span><span class="sxs-lookup"><span data-stu-id="445f1-361">Example</span></span>

```C
UINT ux_pictbridge_dpsclient_object_info_get(UX_SLAVE_CLASS_PIMA *pima,
    ULONG object_handle, UX_SLAVE_CLASS_PIMA_OBJECT **object)
{
    UX_PICTBRIDGE *pictbridge;
    UX_SLAVE_CLASS_PIMA_OBJECT *object_info;
    /* Get the pointer to the Pictbridge instance. */
    pictbridge = (UX_PICTBRIDGE *)pima -> ux_device_class_pima_application;

    /* Check the object handle. If this is handle 1 or 2 , we need to return the XML script object.
       If the handle is not 1 or 2, this is a JPEG picture or other object to be printed. */
    if ((object_handle == UX_PICTBRIDGE_OBJECT_HANDLE_HOST_RESPONSE) ||
        (object_handle == UX_PICTBRIDGE_OBJECT_HANDLE_CLIENT_REQUEST)) {

        /* Check what XML object is requested. It is either a request script or a response. */
        if (object_handle == UX_PICTBRIDGE_OBJECT_HANDLE_HOST_RESPONSE)
            object_info = (UX_SLAVE_CLASS_PIMA_OBJECT *) pictbridge -> ux_pictbridge_object_host;
        else
            object_info = (UX_SLAVE_CLASS_PIMA_OBJECT *) pictbridge ->
                ux_pictbridge_object_client;
    } else
        /* Get the object info from the job info structure. */
        object_info = (UX_SLAVE_CLASS_PIMA_OBJECT *) pictbridge ->
            ux_pictbridge_jobinfo.ux_pictbridge_jobinfo_object;
    /* Return the pointer to this object. */
    *object = object_info;

    /* We are done. */
    return(UX_SUCCESS);
}
```

## <a name="ux_device_class_pima_object_data_get"></a><span data-ttu-id="445f1-362">ux_device_class_pima_object_data_get</span><span class="sxs-lookup"><span data-stu-id="445f1-362">ux_device_class_pima_object_data_get</span></span>

<span data-ttu-id="445f1-363">Nesne verilerini döndürme</span><span class="sxs-lookup"><span data-stu-id="445f1-363">Return the object data</span></span>

### <a name="prototype"></a><span data-ttu-id="445f1-364">Prototype</span><span class="sxs-lookup"><span data-stu-id="445f1-364">Prototype</span></span>

```C
UINT ux_device_class_pima_object_info_get(
    UX_SLAVE_CLASS_PIMA *pima,
    ULONG object_handle,
    UCHAR *object_buffer,
    ULONG object_offset,
    ULONG object_length_requested,
    ULONG *object_actual_length);
```

### <a name="description"></a><span data-ttu-id="445f1-365">Description</span><span class="sxs-lookup"><span data-stu-id="445f1-365">Description</span></span>

<span data-ttu-id="445f1-366">Bu işlev, PIMA sınıfının, yerel sistemdeki nesne verilerini alması ve konağa geri gönderilmesi gerektiğinde çağrılır.</span><span class="sxs-lookup"><span data-stu-id="445f1-366">This function is called when the PIMA class needs to retrieve the object data in the local system and send it back to the host.</span></span>

### <a name="parameters"></a><span data-ttu-id="445f1-367">Parametreler</span><span class="sxs-lookup"><span data-stu-id="445f1-367">Parameters</span></span>

- <span data-ttu-id="445f1-368">**Pima**: Pima sınıfı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="445f1-368">**pima**: Pointer to the pima class instance.</span></span>
- <span data-ttu-id="445f1-369">**object_handle**: nesnenin tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="445f1-369">**object_handle**: Handle of the object</span></span>
- <span data-ttu-id="445f1-370">**object_buffer**: nesne arabellek adresi</span><span class="sxs-lookup"><span data-stu-id="445f1-370">**object_buffer**: Object buffer address</span></span>
- <span data-ttu-id="445f1-371">**object_length_requested**: istemci tarafından uygulamaya istenen nesne veri uzunluğu</span><span class="sxs-lookup"><span data-stu-id="445f1-371">**object_length_requested**: Object data length requested by the client to the application</span></span>
- <span data-ttu-id="445f1-372">**object_actual_length**: uygulama tarafından döndürülen nesne veri uzunluğu</span><span class="sxs-lookup"><span data-stu-id="445f1-372">**object_actual_length**: Object data length returned by the application</span></span>

### <a name="example"></a><span data-ttu-id="445f1-373">Örnek</span><span class="sxs-lookup"><span data-stu-id="445f1-373">Example</span></span>

```C
UINT ux_pictbridge_dpsclient_object_data_get(UX_SLAVE_CLASS_PIMA *pima,
    ULONG object_handle, UCHAR *object_buffer, ULONG object_offset,
    ULONG object_length_requested, ULONG *object_actual_length)
{

    UX_PICTBRIDGE *pictbridge;
    UX_SLAVE_CLASS_PIMA_OBJECT *object_info;
    UCHAR *pima_object_buffer;
    ULONG actual_length;
    UINT status;

    /* Get the pointer to the Pictbridge instance. */
    pictbridge = (UX_PICTBRIDGE *)pima -> ux_device_class_pima_application;

    /* Check the object handle. If this is handle 1 or 2 , we need to return the XML script object.
       If the handle is not 1 or 2, this is a JPEG picture or other object to be printed. */
    if ((object_handle == UX_PICTBRIDGE_OBJECT_HANDLE_HOST_RESPONSE) ||
        (object_handle == UX_PICTBRIDGE_OBJECT_HANDLE_CLIENT_REQUEST))
    {
        /* Check what XML object is requested. It is either a request script or a response. */
        if (object_handle == UX_PICTBRIDGE_OBJECT_HANDLE_HOST_RESPONSE)
            object_info = (UX_SLAVE_CLASS_PIMA_OBJECT *) pictbridge ->
                ux_pictbridge_object_host;
        else
            object_info = (UX_SLAVE_CLASS_PIMA_OBJECT *) pictbridge ->
                ux_pictbridge_object_client;

       /* Is this the corrent handle ? */
       if (object_info -> ux_device_class_pima_object_handle_id == object_handle)
       {
           /* Get the pointer to the object buffer. */
           pima_object_buffer = object_info -> ux_device_class_pima_object_buffer;

           /* Copy the demanded object data portion. */
           ux_utility_memory_copy(object_buffer, pima_object_buffer +
               object_offset, object_length_requested);

           /* Update the length requested. for a demo, we do not do any checking. */
           *object_actual_length = object_length_requested;

           /* What cycle are we in ? */
           if (pictbridge -> ux_pictbridge_host_client_state_machine &
               UX_PICTBRIDGE_STATE_MACHINE_HOST_REQUEST)
            {
                /* Check if we are blocking for a client request. */
                if (pictbridge -> ux_pictbridge_host_client_state_machine &
                    UX_PICTBRIDGE_STATE_MACHINE_CLIENT_REQUEST_PENDING)

                    /* Yes we are pending, send an event to release the pending request. */
                    ux_utility_event_flags_set(&pictbridge ->
                        ux_pictbridge_event_flags_group,
                        UX_PICTBRIDGE_EVENT_FLAG_STATE_MACHINE_READY, TX_OR);

               /* Since we are in host request, this indicates we are done with the cycle. */
               pictbridge -> ux_pictbridge_host_client_state_machine =
                   UX_PICTBRIDGE_STATE_MACHINE_IDLE;

            }

            /* We have copied the requested data. Return OK. */
            return(UX_SUCCESS);

        }
    }
    else
    {

        /* Get the object info from the job info structure. */
        object_info = (UX_SLAVE_CLASS_PIMA_OBJECT *) pictbridge ->
            ux_pictbridge_jobinfo.ux_pictbridge_jobinfo_object;

        /* Obtain the data from the application jobinfo callback. */
        status = pictbridge -> ux_pictbridge_jobinfo.
            ux_pictbridge_jobinfo_object_data_read(pictbridge, object_buffer, object_offset,
            object_length_requested, &actual_length);

        /* Save the length returned. */
        *object_actual_length = actual_length;

        /* Return the application status. */
        return(status);

    }

    /* Could not find the handle. */

    return(UX_DEVICE_CLASS_PIMA_RC_INVALID_OBJECT_HANDLE);
}
```

## <a name="ux_device_class_pima_object_info_send"></a><span data-ttu-id="445f1-374">ux_device_class_pima_object_info_send</span><span class="sxs-lookup"><span data-stu-id="445f1-374">ux_device_class_pima_object_info_send</span></span>

<span data-ttu-id="445f1-375">Ana bilgisayar nesne bilgilerini gönderir</span><span class="sxs-lookup"><span data-stu-id="445f1-375">Host sends the object information</span></span>

### <a name="prototype"></a><span data-ttu-id="445f1-376">Prototype</span><span class="sxs-lookup"><span data-stu-id="445f1-376">Prototype</span></span>

```C
UINT ux_device_class_pima_object_info_send(
    UX_SLAVE_CLASS_PIMA *pima,
    UX_SLAVE_CLASS_PIMA_OBJECT *object, 
    ULONG *object_handle);
```

### <a name="description"></a><span data-ttu-id="445f1-377">Description</span><span class="sxs-lookup"><span data-stu-id="445f1-377">Description</span></span>

<span data-ttu-id="445f1-378">Bu işlev, PIMA sınıfının daha sonra depolama için yerel sistemdeki nesne bilgilerini alması gerektiğinde çağrılır.</span><span class="sxs-lookup"><span data-stu-id="445f1-378">This function is called when the PIMA class needs to receive the object information in the local system for future storage.</span></span>

### <a name="parameters"></a><span data-ttu-id="445f1-379">Parametreler</span><span class="sxs-lookup"><span data-stu-id="445f1-379">Parameters</span></span>

- <span data-ttu-id="445f1-380">**Pima**: Pima sınıfı örneğine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="445f1-380">**pima**: Pointer to the pima class instance</span></span>
- <span data-ttu-id="445f1-381">**nesne**: nesnenin işaretçisi</span><span class="sxs-lookup"><span data-stu-id="445f1-381">**object**:  Pointer to the object</span></span>
- <span data-ttu-id="445f1-382">**object_handle**: nesnenin tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="445f1-382">**object_handle**: Handle of the object</span></span>

### <a name="example"></a><span data-ttu-id="445f1-383">Örnek</span><span class="sxs-lookup"><span data-stu-id="445f1-383">Example</span></span>

```C
UINT ux_pictbridge_dpsclient_object_info_send(UX_SLAVE_CLASS_PIMA *pima,
    UX_SLAVE_CLASS_PIMA_OBJECT *object, ULONG *object_handle)
{
    UX_PICTBRIDGE *pictbridge;
    UX_SLAVE_CLASS_PIMA_OBJECT *object_info; UCHAR
    string_discovery_name[UX_PICTBRIDGE_MAX_FILE_NAME_SIZE];

    /* Get the pointer to the Pictbridge instance. */
    pictbridge = (UX_PICTBRIDGE *)pima -> ux_device_class_pima_application;

    /* We only have one object. */
    object_info = (UX_SLAVE_CLASS_PIMA_OBJECT *) pictbridge ->
        ux_pictbridge_object_host;

    /* Copy the demanded object info set. */
    ux_utility_memory_copy(object_info, object,
        UX_SLAVE_CLASS_PIMA_OBJECT_DATA_LENGTH);

    /* Store the object handle. In Pictbridge we only receive XML scripts so the handle is hardwired to 1. */
    object_info -> ux_device_class_pima_object_handle_id = 1;
    *object_handle = 1;

    /* Check state machine. If we are in discovery pending mode, check file name of this object. */
    if (pictbridge -> ux_pictbridge_discovery_state ==
        UX_PICTBRIDGE_DPSCLIENT_DISCOVERY_PENDING)
    {
        /* We are in the discovery mode. Check for file name. It must match
           HDISCVRY.DPS in Unicode mode. */

        /* Check if this is a script. */
        if (object_info -> ux_device_class_pima_object_format ==
            UX_DEVICE_CLASS_PIMA_OFC_SCRIPT)
        {

            /* Yes this is a script. We need to search for the HDISCVRY.DPS file name. Get the file name in a ascii format. */
            ux_utility_unicode_to_string(object_info ->
                ux_device_class_pima_object_filename,
                string_discovery_name);

            /* Now, compare it to the HDISCVRY.DPS file name. Check length first. */
            if (ux_utility_string_length_get(_ux_pictbridge_hdiscovery_name)
                == ux_utility_string_length_get(string_discovery_name))
            {

                /* So far, the length of name of the files are the same. Compare names now. */
                if(ux_utility_memory_compare(_ux_pictbridge_hdiscovery_name,
                    string_discovery_name,
                    ux_utility_string_length_get(string_discovery_name)) == UX_SUCCESS)
                {
                    /* We are done with discovery of the printer. We can now send notifications when the camera wants to print an object. */
                    pictbridge -> ux_pictbridge_discovery_state =
                        UX_PICTBRIDGE_DPSCLIENT_DISCOVERY_COMPLETE;

                    /* Set an event flag if the application is listening. */
                    ux_utility_event_flags_set(&pictbridge ->
                        ux_pictbridge_event_flags_group,
                        UX_PICTBRIDGE_EVENT_FLAG_DISCOVERY, TX_OR);

                    /* There is no object during th discovery cycle. */
                    return(UX_SUCCESS);
                }
            }
        }
    }
    /* What cycle are we in ? */
    if (pictbridge -> ux_pictbridge_host_client_state_machine ==
        UX_PICTBRIDGE_STATE_MACHINE_IDLE)

        /* Since we are in idle state, we must have received a request from the host. */
        pictbridge -> ux_pictbridge_host_client_state_machine =
            UX_PICTBRIDGE_STATE_MACHINE_HOST_REQUEST;

    /* We have copied the requested data. Return OK. */
    return(UX_SUCCESS);
}
```

## <a name="ux_device_class_pima_object_data_send"></a><span data-ttu-id="445f1-384">ux_device_class_pima_object_data_send</span><span class="sxs-lookup"><span data-stu-id="445f1-384">ux_device_class_pima_object_data_send</span></span>

<span data-ttu-id="445f1-385">Konak nesne verilerini gönderir</span><span class="sxs-lookup"><span data-stu-id="445f1-385">Host sends the object data</span></span>

### <a name="prototype"></a><span data-ttu-id="445f1-386">Prototype</span><span class="sxs-lookup"><span data-stu-id="445f1-386">Prototype</span></span>

```C
UINT ux_device_class_pima_object_data_send(
    UX_SLAVE_CLASS_PIMA *pima,
    ULONG object_handle, 
    ULONG phase, 
    UCHAR *object_buffer,
    ULONG object_offset, 
    ULONG object_length);
```

### <a name="description"></a><span data-ttu-id="445f1-387">Description</span><span class="sxs-lookup"><span data-stu-id="445f1-387">Description</span></span>

<span data-ttu-id="445f1-388">Bu işlev, PIMA sınıfının depolama için yerel sistemdeki nesne verilerini alması gerektiğinde çağrılır.</span><span class="sxs-lookup"><span data-stu-id="445f1-388">This function is called when the PIMA class needs to receive the object data in the local system for storage.</span></span>

### <a name="parameters"></a><span data-ttu-id="445f1-389">Parametreler</span><span class="sxs-lookup"><span data-stu-id="445f1-389">Parameters</span></span>

- <span data-ttu-id="445f1-390">**Pima**: Pima sınıfı örneğine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="445f1-390">**pima**: Pointer to the pima class instance</span></span>
- <span data-ttu-id="445f1-391">**object_handle**: nesnenin tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="445f1-391">**object_handle**: Handle of the object</span></span>
- <span data-ttu-id="445f1-392">**aşama**: aktarımın aşaması (etkin veya tamamlanmış)</span><span class="sxs-lookup"><span data-stu-id="445f1-392">**phase**: phase of the transfer (active or complete)</span></span>
- <span data-ttu-id="445f1-393">**object_buffer**: nesne arabellek adresi</span><span class="sxs-lookup"><span data-stu-id="445f1-393">**object_buffer**: Object buffer address</span></span>
- <span data-ttu-id="445f1-394">**object_offset**: verilerin adresi</span><span class="sxs-lookup"><span data-stu-id="445f1-394">**object_offset**: Address of data</span></span>
- <span data-ttu-id="445f1-395">**object_length**: uygulama tarafından gönderilen nesne veri uzunluğu</span><span class="sxs-lookup"><span data-stu-id="445f1-395">**object_length**: Object data length sent by application</span></span>

### <a name="example"></a><span data-ttu-id="445f1-396">Örnek</span><span class="sxs-lookup"><span data-stu-id="445f1-396">Example</span></span>

```C
UINT ux_pictbridge_dpsclient_object_data_send(UX_SLAVE_CLASS_PIMA *pima,
    ULONG object_handle,
    ULONG phase,
    UCHAR *object_buffer,
    ULONG object_offset,
    ULONG object_length)
{
    UINT status;
    UX_PICTBRIDGE *pictbridge;
    UX_SLAVE_CLASS_PIMA_OBJECT *object_info;
    ULONG event_flag;
    UCHAR *pima_object_buffer;

    /* Get the pointer to the Pictbridge instance. */
    pictbridge = (UX_PICTBRIDGE *)pima -> ux_device_class_pima_application;

    /* Get the pointer to the pima object. */
    object_info = (UX_SLAVE_CLASS_PIMA_OBJECT *) pictbridge ->
        ux_pictbridge_object_host;

    /* Is this the corrent handle ? */
    if (object_info -> ux_device_class_pima_object_handle_id == object_handle)
    {
        /* Get the pointer to the object buffer. */
        pima_object_buffer = object_info ->
            ux_device_class_pima_object_buffer;

        /* Check the phase. We should wait for the object to be completed and the response sent back before parsing the object. */
        if (phase == UX_DEVICE_CLASS_PIMA_OBJECT_TRANSFER_PHASE_ACTIVE)
        {
            /* Copy the demanded object data portion. */
            ux_utility_memory_copy(pima_object_buffer + object_offset,
                object_buffer, object_length);

            /* Save the length of this object. */
            object_info -> ux_device_class_pima_object_length = object_length;

            /* We are not done yet. */
            return(UX_SUCCESS);
        }
        else
        {
            /* Completion of transfer. We are done. */
            return(UX_SUCCESS);
        }
    }
}
```

## <a name="ux_device_class_pima_object_delete"></a><span data-ttu-id="445f1-397">ux_device_class_pima_object_delete</span><span class="sxs-lookup"><span data-stu-id="445f1-397">ux_device_class_pima_object_delete</span></span>

<span data-ttu-id="445f1-398">Yerel bir nesneyi silme</span><span class="sxs-lookup"><span data-stu-id="445f1-398">Delete a local object</span></span>

### <a name="prototype"></a><span data-ttu-id="445f1-399">Prototype</span><span class="sxs-lookup"><span data-stu-id="445f1-399">Prototype</span></span>

```C
UINT ux_device_class_pima_object_delete(
    UX_SLAVE_CLASS_PIMA *pima,
    ULONG object_handle);
```

### <a name="description"></a><span data-ttu-id="445f1-400">Description</span><span class="sxs-lookup"><span data-stu-id="445f1-400">Description</span></span>

<span data-ttu-id="445f1-401">Bu işlev, PIMA sınıfının yerel depolamadaki bir nesneyi silmesi gerektiğinde çağrılır.</span><span class="sxs-lookup"><span data-stu-id="445f1-401">This function is called when the PIMA class needs to delete an object on the local storage.</span></span>

### <a name="parameters"></a><span data-ttu-id="445f1-402">Parametreler</span><span class="sxs-lookup"><span data-stu-id="445f1-402">Parameters</span></span>

- <span data-ttu-id="445f1-403">**Pima**: Pima sınıfı örneğine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="445f1-403">**pima**: Pointer to the pima class instance</span></span>
- <span data-ttu-id="445f1-404">**object_handle**: nesnenin tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="445f1-404">**object_handle**: Handle of the object</span></span>

### <a name="example"></a><span data-ttu-id="445f1-405">Örnek</span><span class="sxs-lookup"><span data-stu-id="445f1-405">Example</span></span>

```C
UINT ux_pictbridge_dpsclient_object_delete(UX_SLAVE_CLASS_PIMA *pima,
    ULONG object_handle)
{
    /* Delete the object pointer by the handle. */

}
```

## <a name="usb-device-audio-class"></a><span data-ttu-id="445f1-406">USB cihaz ses sınıfı</span><span class="sxs-lookup"><span data-stu-id="445f1-406">USB Device Audio Class</span></span>

<span data-ttu-id="445f1-407">USB cihaz ses sınıfı, USB konak sisteminin cihazla bir ses cihazı olarak iletişim kurmasına olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="445f1-407">The USB device Audio class allows for a USB host system to communicate with the device as an audio device.</span></span> <span data-ttu-id="445f1-408">Bu sınıf, USB Standart ve USB ses sınıfı 1,0 veya 2,0 standardını temel alır.</span><span class="sxs-lookup"><span data-stu-id="445f1-408">This class is based on the USB standard and USB Audio Class 1.0 or 2.0 standard.</span></span>

<span data-ttu-id="445f1-409">USB ses uyumlu bir cihaz çerçevesinin cihaz yığını tarafından bildirilmesine ihtiyacı vardır.</span><span class="sxs-lookup"><span data-stu-id="445f1-409">A USB audio compliant device framework needs to be declared by the device stack.</span></span> <span data-ttu-id="445f1-410">Ses 2,0 konuşmacı örneği aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="445f1-410">An example of an Audio 2.0 speaker follows:</span></span>

```C
unsigned char device_framework_high_speed[] = {

    /* --- Device Descriptor 18 bytes
    0x00 bDeviceClass: Refer to interface
    0x00 bDeviceSubclass: Refer to interface
    0x00 bDeviceProtocol: Refer to interface

    idVendor & idProduct - https://www.linux-usb.org/usb.ids
    */

    /* 0 bLength, bDescriptorType */ 18, 0x01,
    /* 2 bcdUSB : 0x200 (2.00) */ 0x00, 0x02,
    /* 4 bDeviceClass : 0x00 (see interface) */ 0x00,
    /* 5 bDeviceSubClass : 0x00 (see interface) */ 0x00,
    /* 6 bDeviceProtocol : 0x00 (see interface) */ 0x00,
    /* 7 bMaxPacketSize0 */ 0x08,
    /* 8 idVendor, idProduct */ 0x84, 0x84, 0x03, 0x00,
    /* 12 bcdDevice */ 0x00, 0x02,
    /* 14 iManufacturer, iProduct, iSerialNumber */ 0, 0, 0,
    /* 17 bNumConfigurations */ 1,
    /* ---------------- Device Qualifier Descriptor */
    /* 0 bLength, bDescriptorType */ 10, 0x06,
    /* 2 bcdUSB : 0x200 (2.00) */ 0x00,0x02,
    /* 4 bDeviceClass : 0x00 (see interface) */ 0x00,
    /* 5 bDeviceSubClass : 0x00 (see interface) */ 0x00,
    /* 6 bDeviceProtocol : 0x00 (see interface) */ 0x00,
    /* 7 bMaxPacketSize0 */ 8,
    /* 8 bNumConfigurations */ 1,
    /* 9 bReserved */ 0,
    /* --- Configuration Descriptor (9+8+73+55=145, 0x91) */
    /* 0 bLength, bDescriptorType */ 9, 0x02,
    /* 2 wTotalLength */ 145, 0,
    /* 4 bNumInterfaces, bConfigurationValue */ 2, 1,
    /* 6 iConfiguration */ 0,
    /* 7 bmAttributes, bMaxPower */ 0x80, 50,
    /* ----------- Interface Association Descriptor */
    /* 0 bLength, bDescriptorType */ 8, 0x0B,
    /* 2 bFirstInterface, bInterfaceCount */ 0, 2,
    /* 4 bFunctionClass : 0x01 (Audio) */ 0x01,
    /* 5 bFunctionSubClass : 0x00 (UNDEFINED) */ 0x00,
    /* 6 bFunctionProtocol : 0x20 (VERSION_02_00) */ 0x20,
    /* 7 iFunction */ 0,
    /* --- Interface Descriptor #0: Control (9+64=73) */
    /* 0 bLength, bDescriptorType */ 9, 0x04,
    /* 2 bInterfaceNumber, bAlternateSetting */ 0, 0,
    /* 4 bNumEndpoints */ 0,
    /* 5 bInterfaceClass : 0x01 (Audio) */ 0x01,
    /* 6 bInterfaceSubClass : 0x01 (AudioControl) */ 0x01,
    /* 7 bInterfaceProtocol : 0x20 (VERSION_02_00) */ 0x20,
    /* 8 iInterface */ 0,
    /* --- Audio 2.0 AC Interface Header Descriptor (9+8+17+18+12=64, 0x40) */
    /* 0 bLength */ 9,
    /* 1 bDescriptorType, bDescriptorSubtype */ 0x24, 0x01,
    /* 3 bcdADC */ 0x00, 0x02,
    /* 5 bCategory : 0x08 (IO Box) */ 0x08,
    /* 6 wTotalLength */ 64, 0,
    /* 8 bmControls */ 0x00,
    /* -------- Audio 2.0 AC Clock Source Descriptor */
    /* 0 bLength */ 8,
    /* 1 bDescriptorType, bDescriptorSubtype */ 0x24, 0x0A,
    /* 3 bClockID */ 0x10,
    /* 4 bmAttributes : 0x05 (Sync|InternalFixedClk) */ 0x05,
    /* 5 bmControls : 0x01 (FreqReadOnly) */ 0x01,
    /* 6 bAssocTerminal, iClockSource */ 0x00, 0,
    /* ------ Audio 2.0 AC Input Terminal Descriptor */
    /* 0 bLength */ 17,
    /* 1 bDescriptorType, bDescriptorSubtype */ 0x24, 0x02, /* 3 bTerminalID */ 0x04,
    /* 4 wTerminalType : 0x0101 (USB Streaming) */ 0x01, 0x01,
    /* 6 bAssocTerminal, bCSourceID */ 0x00, 0x10,
    /* 8 bNrChannels */ 2,
    /* 9 bmChannelConfig */ 0x00, 0x00, 0x00, 0x00,
    /* 13 iChannelNames, bmControls, iTerminal */ 0, 0x00, 0x00, 0,
    /* -------- Audio 2.0 AC Feature Unit Descriptor */
    /* 0 bLength */ 18,
    /* 1 bDescriptorType, bDescriptorSubtype */ 0x24, 0x06,
    /* 3 bUnitID, bSourceID */ 0x05, 0x04,
    /* 5 bmaControls(0) : 0x0F (VolumeRW|MuteRW) */ 0x0F, 0x00, 0x00, 0x00,
    /* 9 bmaControls(1) : 0x00000000 */ 0x00, 0x00, 0x00, 0x00,
    /* 13 bmaControls(1) : 0x00000000 */ 0x00, 0x00, 0x00, 0x00,
    /* . iFeature */ 0,
    /* ----- Audio 2.0 AC Output Terminal Descriptor */
    /* 0 bLength */ 12,
    /* 1 bDescriptorType, bDescriptorSubtype */ 0x24, 0x03, /* 3 bTerminalID */ 0x06,
    /* 4 wTerminalType : 0x0301 (Speaker) */ 0x01, 0x03,
    /* 6 bAssocTerminal, bSourceID, bCSourceID */ 0x00, 0x05, 0x10,
    /* 9 bmControls, iTerminal */ 0x00, 0x00, 0,
    /* --- Interface Descriptor #1: Stream OUT (9+9+16+6+7+8=55) */
    /* 0 bLength, bDescriptorType */ 9, 0x04,
    /* 2 bInterfaceNumber, bAlternateSetting */ 1, 0,
    /* 4 bNumEndpoints */ 0,
    /* 5 bInterfaceClass : 0x01 (Audio) */ 0x01,
    /* 6 bInterfaceSubClass : 0x01 (AudioStream) */ 0x02,
    /* 7 bInterfaceProtocol : 0x20 (VERSION_02_00) */ 0x20,
    /* 8 iInterface */ 0,
    /* ----------------------- Interface Descriptor */
    /* 0 bLength, bDescriptorType */ 9, 0x04,
    /* 2 bInterfaceNumber, bAlternateSetting */ 1, 1,
    /* 4 bNumEndpoints */ 1,
    /* 5 bInterfaceClass : 0x01 (Audio) */ 0x01,
    /* 6 bInterfaceSubClass : 0x01 (AudioStream) */ 0x02,
    /* 7 bInterfaceProtocol : 0x20 (VERSION_02_00) */ 0x20,
    /* 8 iInterface */ 0,
    /* ----------- Audio 2.0 AS Interface Descriptor */
    /* 0 bLength */ 16,
    /* 1 bDescriptorType, bDescriptorSubtype */ 0x24, 0x01,
    /* 3 bTerminalLink, bmControls */ 0x04, 0x00,
    /* 5 bFormatType : 0x01 (FORMAT_TYPE_I) */ 0x01,
    /* 6 bmFormats : 0x000000001 (PCM) */ 0x01, 0x00, 0x00, 0x00, /* 10 bNrChannels */ 2,
    /* 11 bmChannelConfig */ 0x00, 0x00, 0x00, 0x00,
    /* 15 iChannelNames */ 0, /* --------- Audio 2.0 AS Format Type Descriptor */
    /* 0 bLength */ 6,
    /* 1 bDescriptorType, bDescriptorSubtype */ 0x24, 0x02,
    /* 3 bFormatType : 0x01 (FORMAT_TYPE_I) */ 0x01,
    /* 4 bSubslotSize, bBitResolution */ 2, 16,
    /* ------------------------- Endpoint Descriptor */
    /* 0 bLength, bDescriptorType */ 7, 0x05,
    /* 2 bEndpointAddress */ 0x02,
    /* 3 bmAttributes : 0x0D (Sync|ISO) */ 0x0D,
    /* 4 wMaxPacketSize : 0x0100 (256) */ 0x00, 0x01,
    /* 6 bInterval : 0x04 (1ms) */ 4,
    /* - Audio 2.0 AS ISO Audio Data Endpoint Descriptor */
    /* 0 bLength */ 8,
    /* 1 bDescriptorType, bDescriptorSubtype */ 0x25, 0x01,
    /* 3 bmAttributes, bmControls */ 0x00, 0x00,
    /* 5 bLockDelayUnits, wLockDelay */ 0x00, 0x00, 0x00,
};
```

<span data-ttu-id="445f1-411">Ses sınıfı, arabirimleri gruplamak için bir bileşik cihaz çerçevesi kullanır (denetim ve akış).</span><span class="sxs-lookup"><span data-stu-id="445f1-411">The Audio class uses a composite device framework to group interfaces (control and streaming).</span></span> <span data-ttu-id="445f1-412">Bir sonuç olarak, cihaz tanımlayıcısı tanımlanırken alınması gerekir.</span><span class="sxs-lookup"><span data-stu-id="445f1-412">As a result care should be taken when defining the device descriptor.</span></span> <span data-ttu-id="445f1-413">USBX, dahili olarak arabirimlerin nasıl bağlanacağını öğrenmek için ıAD tanımlayıcısını kullanır.</span><span class="sxs-lookup"><span data-stu-id="445f1-413">USBX relies on the IAD descriptor to know internally how to bind interfaces.</span></span> <span data-ttu-id="445f1-414">IAD tanımlayıcısının, arabirimlerden önce (bir veya daha fazla AudioStreaming Interface tarafından izlenen bir veya daha fazla Audiostream arabirimi) önce bildirilmelidir ve ses sınıfının ilk arabirimini (AudioControl arabirimi) ve kaç arabirimin iliştirildiğine sahip olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="445f1-414">The IAD descriptor should be declared before the interfaces (an AudioControl interface followed by one or more AudioStreaming interfaces) and contain the first interface of the Audio class (the AudioControl interface) and how many interfaces are attached.</span></span>

<span data-ttu-id="445f1-415">Ses sınıfının çalışma şekli, cihazın ses gönderip almayacağı, ancak her iki durumda da ses çerçevesi arabelleklerinin depolanması için bir FıFO kullanmasına bağlıdır: cihaz konağa ses gönderiyorsa, uygulama daha sonra USBX tarafından konağa gönderilen, daha sonra FıFO 'ya ses çerçevesi arabellekleri ekler. cihaz konaktan ses alıyorsa, USBX konaktan alınan ses çerçevesi arabelleklerini daha sonra uygulama tarafından okunan FıFO 'ya ekler.</span><span class="sxs-lookup"><span data-stu-id="445f1-415">The way the audio class works depends on whether the device is sending or receiving audio, but both cases use a FIFO for storing audio frame buffers: if the device is sending audio to the host, then the application adds audio frame buffers to the FIFO which are later sent to the host by USBX; if the device is receiving audio from the host, then USBX adds the audio frame buffers received from the host to the FIFO which are later read by the application.</span></span> <span data-ttu-id="445f1-416">Her ses akışının kendi FıFO 'u vardır ve her ses çerçevesi arabelleği birden çok örnek içerir.</span><span class="sxs-lookup"><span data-stu-id="445f1-416">Each audio stream has its own FIFO, and each audio frame buffer consists of multiple samples.</span></span>

<span data-ttu-id="445f1-417">Ses sınıfının başlatılması aşağıdaki parçaları bekler.</span><span class="sxs-lookup"><span data-stu-id="445f1-417">The initialization of the Audio class expects the following parts.</span></span>

1. <span data-ttu-id="445f1-418">Ses sınıfı aşağıdaki akış parametrelerini bekliyor:</span><span class="sxs-lookup"><span data-stu-id="445f1-418">Audio class expects the following streaming parameters:</span></span>

   ```C
   /* Set the parameters for Audio streams. */
   /* Set the application-defined callback that is invoked when the
      host requests a change to the alternate setting. */
   audio_stream_parameter[0].ux_device_class_audio_stream_parameter_callbacks
       .ux_device_class_audio_stream_change = demo_audio_read_change;

   /* Set the application-defined callback that is invoked whenever
      a USB packet (audio frame) is sent to or received from the host. */
   audio_stream_parameter[0].ux_device_class_audio_stream_parameter_callbacks
       .ux_device_class_audio_stream_frame_done = demo_audio_read_done;

   /* Set the number of audio frame buffers in the FIFO. */
   audio_stream_parameter[0].ux_device_class_audio_stream_parameter_max_frame _buffer_nb = UX_DEMO_FRAME_BUFFER_NB;

   /* Set the maximum size of each audio frame buffer in the FIFO. */
   audio_stream_parameter[0].ux_device_class_audio_stream_parameter_max_frame _buffer_size = UX_DEMO_MAX_FRAME_SIZE;

   /* Set the internally-defined audio processing thread entry pointer. If the application wishes to receive audio from the host
      (which is the case in this example), ux_device_class_audio_read_thread_entry should be used;
      if the application wishes to send data to the host, ux_device_class_audio_write_thread_entry should be used. */
   audio_stream_parameter[0].ux_device_class_audio_stream_parameter_thread_entry = ux_device_class_audio_read_thread_entry;
   ```

2. <span data-ttu-id="445f1-419">Ses sınıfı aşağıdaki işlev parametrelerini bekliyor.</span><span class="sxs-lookup"><span data-stu-id="445f1-419">Audio class expects the following function parameters.</span></span>

   ```C
   /* Set the parameters for Audio device. */

   /* Set the number of streams. */
   audio_parameter.ux_device_class_audio_parameter_streams_nb = 1;

   /* Set the pointer to the first audio stream parameter.
      Note that we initialized this parameter in the previous section.
      Also note that for more than one streams, this should be an array. */
   audio_parameter.ux_device_class_audio_parameter_streams = audio_stream_parameter;

   /* Set the application-defined callback that is invoked when the audio class
      is activated i.e. device is connected to host. */
   audio_parameter.ux_device_class_audio_parameter_callbacks
       .ux_slave_class_audio_instance_activate = demo_audio_instance_activate;

   /* Set the application-defined callback that is invoked when the audio class
      is deactivated i.e. device is disconnected from host. */

   audio_parameter.ux_device_class_audio_parameter_callbacks
       .ux_slave_class_audio_instance_deactivate = demo_audio_instance_deactivate;

   /* Set the application-defined callback that is invoked when the stack receives a control request from the host.
      See below for more details.
   */
   audio_parameter.ux_device_class_audio_parameter_callbacks
       .ux_device_class_audio_control_process = demo_audio20_request_process;

   /* Initialize the device Audio class. This class owns interfaces starting with 0. */
   status = ux_device_stack_class_register(_ux_system_slave_class_audio_name,
       ux_device_class_audio_entry, 1, 0, &audio_parameter);
   if(status!=UX_SUCCESS)
       return;
   ```

   <span data-ttu-id="445f1-420">Yığın konaktan bir denetim isteği aldığında uygulama tanımlı denetim isteği geri araması (***ux_device_class_audio_control_process***; önceki örnekte ayarlanan) çağrılır.</span><span class="sxs-lookup"><span data-stu-id="445f1-420">The application-defined control request callback (***ux_device_class_audio_control_process***; set in the previous example) is invoked when the stack receives a control request from the host.</span></span> <span data-ttu-id="445f1-421">İstek kabul edildiğinde ve işlenirse (onaylanan veya durdurulmuş) geri çağırma başarılı döndürmelidir, aksi takdirde hata döndürülmelidir.</span><span class="sxs-lookup"><span data-stu-id="445f1-421">If the request is accepted and handled (acknowledged or stalled) the callback must return success, otherwise error should be returned.</span></span>

   <span data-ttu-id="445f1-422">Sınıfa özgü denetim isteği işlemi, bir uygulama tanımlı geri arama olarak tanımlanır çünkü denetim istekleri USB ses sürümleri arasında çok farklıdır ve istek işleminin büyük bir bölümü cihaz çerçevesiyle ilgilidir.</span><span class="sxs-lookup"><span data-stu-id="445f1-422">The class-specific control request process is defined as an application-defined callback because the control requests are very different between USB Audio versions and a large part of the request process relates to the device framework.</span></span> <span data-ttu-id="445f1-423">Uygulamanın, cihazı çalışır hale getirmek için istekleri doğru işlemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="445f1-423">The application should handle requests correctly to make the device functional.</span></span>

   <span data-ttu-id="445f1-424">Ses cihazı, ses, sessiz ve örnekleme sıklığı yaygın denetim istekleridir, ancak farklı USB ses sürümleri için basit ve dahili olarak tanımlanmış geri çağrılar, uygulamaların kullanması için sonraki bölümlerde sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="445f1-424">Since for an audio device, volume, mute and sampling frequency are common control requests, simple, internally-defined callbacks for different USB audio versions are introduced in later sections for applications to use.</span></span> <span data-ttu-id="445f1-425">Daha fazla ayrıntı için ***ux_device_class_audio10_control_process** _ ve _ *_ux_device_class_audio_control_request_** bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="445f1-425">Refer to ***ux_device_class_audio10_control_process** _ and _ *_ux_device_class_audio_control_request_** for more details.</span></span>

<span data-ttu-id="445f1-426">Ses cihazının cihaz çerçevesinde, PID/VIP cihaz tanımlayıcısına depolanır (yukarıda belirtilen cihaz tanımlayıcısına bakın).</span><span class="sxs-lookup"><span data-stu-id="445f1-426">In the device framework of the Audio device, the PID/VID are stored in the device descriptor (see the device descriptor declared above).</span></span>

<span data-ttu-id="445f1-427">Bir USB ana bilgisayar sistemi, USB ses cihazını bulur ve ses sınıfını takar, cihaz herhangi bir ses yürütücüsü veya Kaydedicisi (çerçeveye bağlı olarak) ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="445f1-427">When a USB host system discovers the USB Audio device and mounts the audio class, the device can be used with any audio player or recorder (depending on the framework).</span></span> <span data-ttu-id="445f1-428">Başvuru için konak Işletim sistemine bakın.</span><span class="sxs-lookup"><span data-stu-id="445f1-428">See the host Operating System for reference.</span></span>

<span data-ttu-id="445f1-429">Ses sınıfı API 'Leri aşağıda tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="445f1-429">The Audio class APIs are defined below.</span></span>

## <a name="ux_device_class_audio_read_thread_entry"></a><span data-ttu-id="445f1-430">ux_device_class_audio_read_thread_entry</span><span class="sxs-lookup"><span data-stu-id="445f1-430">ux_device_class_audio_read_thread_entry</span></span>

<span data-ttu-id="445f1-431">Ses işlevine yönelik verileri okumak için iş parçacığı girişi.</span><span class="sxs-lookup"><span data-stu-id="445f1-431">Thread entry for reading data for the Audio function.</span></span>

### <a name="prototype"></a><span data-ttu-id="445f1-432">Prototype</span><span class="sxs-lookup"><span data-stu-id="445f1-432">Prototype</span></span>

```C
VOID ux_device_class_audio_read_thread_entry(ULONG audio_stream);
```

### <a name="description"></a><span data-ttu-id="445f1-433">Description</span><span class="sxs-lookup"><span data-stu-id="445f1-433">Description</span></span>

<span data-ttu-id="445f1-434">Bu işlev, konaktan ses okuma isteniyorsa ses akışı başlatma parametresine geçirilir.</span><span class="sxs-lookup"><span data-stu-id="445f1-434">This function is passed to the audio stream initialization parameter if reading audio from the host is desired.</span></span> <span data-ttu-id="445f1-435">Dahili olarak, bu işlevle giriş işlevi olarak bir iş parçacığı oluşturulur; iş parçacığı, ses işlevindeki zaman aralıklı çıkış uç noktası aracılığıyla ses verilerini okur.</span><span class="sxs-lookup"><span data-stu-id="445f1-435">Internally, a thread is created with this function as its entry function; the thread itself reads audio data through the isochronous OUT endpoint in the Audio function.</span></span>

### <a name="parameters"></a><span data-ttu-id="445f1-436">Parametreler</span><span class="sxs-lookup"><span data-stu-id="445f1-436">Parameters</span></span>

- <span data-ttu-id="445f1-437">**audio_stream**: ses akışı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="445f1-437">**audio_stream**: Pointer to the audio stream instance.</span></span>

### <a name="example"></a><span data-ttu-id="445f1-438">Örnek</span><span class="sxs-lookup"><span data-stu-id="445f1-438">Example</span></span>

```C
/* Set parameter to initialize a stream for reading. */
audio_stream_parameter[0].ux_device_class_audio_stream_parameter_thread_entry
     = ux_device_class_audio_read_thread_entry;
```

## <a name="ux_device_class_audio_write_thread_entry"></a><span data-ttu-id="445f1-439">ux_device_class_audio_write_thread_entry</span><span class="sxs-lookup"><span data-stu-id="445f1-439">ux_device_class_audio_write_thread_entry</span></span>

<span data-ttu-id="445f1-440">Ses işlevine veri yazmak için iş parçacığı girişi</span><span class="sxs-lookup"><span data-stu-id="445f1-440">Thread entry for writing data for the Audio function</span></span>

### <a name="prototype"></a><span data-ttu-id="445f1-441">Prototype</span><span class="sxs-lookup"><span data-stu-id="445f1-441">Prototype</span></span>

```C
VOID ux_device_class_audio_write_thread_entry(ULONG audio_stream);
```

### <a name="description"></a><span data-ttu-id="445f1-442">Description</span><span class="sxs-lookup"><span data-stu-id="445f1-442">Description</span></span>

<span data-ttu-id="445f1-443">Bu işlev, konağa ses yazılması isteniyorsa ses akışı başlatma parametresine geçirilir.</span><span class="sxs-lookup"><span data-stu-id="445f1-443">This function is passed to the audio stream initialization parameter if writing audio to the host is desired.</span></span> <span data-ttu-id="445f1-444">Dahili olarak, bu işlevle giriş işlevi olarak bir iş parçacığı oluşturulur; iş parçacığı, ses işlevindeki zaman aralıklı olarak ses verileri yazar.</span><span class="sxs-lookup"><span data-stu-id="445f1-444">Internally, a thread is created with this function as its entry function; the thread itself writes audio data through the isochronous IN endpoint in the Audio function.</span></span>

### <a name="parameters"></a><span data-ttu-id="445f1-445">Parametreler</span><span class="sxs-lookup"><span data-stu-id="445f1-445">Parameters</span></span>

- <span data-ttu-id="445f1-446">**audio_stream**: ses akışı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="445f1-446">**audio_stream**: Pointer to the audio stream instance.</span></span>

### <a name="example"></a><span data-ttu-id="445f1-447">Örnek</span><span class="sxs-lookup"><span data-stu-id="445f1-447">Example</span></span>

```C
/* Set parameter to initialize as stream for writing. */
audio_stream_parameter[0].ux_device_class_audio_stream_parameter_thread_en
    try = ux_device_class_audio_write_thread_entry;
```

## <a name="ux_device_class_audio_stream_get"></a><span data-ttu-id="445f1-448">ux_device_class_audio_stream_get</span><span class="sxs-lookup"><span data-stu-id="445f1-448">ux_device_class_audio_stream_get</span></span>

<span data-ttu-id="445f1-449">Ses işlevi için belirli bir akış örneği al</span><span class="sxs-lookup"><span data-stu-id="445f1-449">Get specific stream instance for the Audio function</span></span>

### <a name="prototype"></a><span data-ttu-id="445f1-450">Prototype</span><span class="sxs-lookup"><span data-stu-id="445f1-450">Prototype</span></span>

```C
UINT ux_device_class_audio_stream_get(
    UX_DEVICE_CLASS_AUDIO *audio,
    ULONG stream_index, 
    UX_DEVICE_CLASS_AUDIO_STREAM **stream);
```

### <a name="description"></a><span data-ttu-id="445f1-451">Description</span><span class="sxs-lookup"><span data-stu-id="445f1-451">Description</span></span>

<span data-ttu-id="445f1-452">Bu işlev, ses sınıfının akış örneğini almak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="445f1-452">This function is used to get a stream instance of audio class.</span></span>

### <a name="parameters"></a><span data-ttu-id="445f1-453">Parametreler</span><span class="sxs-lookup"><span data-stu-id="445f1-453">Parameters</span></span>

- <span data-ttu-id="445f1-454">**Ses**: ses örneğine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="445f1-454">**audio**: Pointer to the audio instance</span></span>
- <span data-ttu-id="445f1-455">**stream_index**: akış örneği dizini 0 ' a göre</span><span class="sxs-lookup"><span data-stu-id="445f1-455">**stream_index**: Stream instance index based on 0</span></span>
- <span data-ttu-id="445f1-456">**Stream**: ses akışı örneği işaretçisini depolamak için arabelleğin işaretçisi</span><span class="sxs-lookup"><span data-stu-id="445f1-456">**stream**: Pointer to buffer to store the audio stream instance pointer</span></span>

### <a name="return-value"></a><span data-ttu-id="445f1-457">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="445f1-457">Return Value</span></span>

- <span data-ttu-id="445f1-458">**UX_SUCCESS** (0x00) Bu işlem başarılı oldu</span><span class="sxs-lookup"><span data-stu-id="445f1-458">**UX_SUCCESS** (0x00) This operation was successful</span></span>
- <span data-ttu-id="445f1-459">İşlevden **UX_ERROR** (0xFF) hatası</span><span class="sxs-lookup"><span data-stu-id="445f1-459">**UX_ERROR** (0xFF) Error from function</span></span>

### <a name="example"></a><span data-ttu-id="445f1-460">Örnek</span><span class="sxs-lookup"><span data-stu-id="445f1-460">Example</span></span>

```C
/* Get audio stream instance. */
status = ux_device_class_audio_stream_get(audio, 0, &stream);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio_reception_start"></a><span data-ttu-id="445f1-461">ux_device_class_audio_reception_start</span><span class="sxs-lookup"><span data-stu-id="445f1-461">ux_device_class_audio_reception_start</span></span>

<span data-ttu-id="445f1-462">Ses akışı için ses verilerini almayı Başlat</span><span class="sxs-lookup"><span data-stu-id="445f1-462">Start audio data reception for the Audio stream</span></span>

### <a name="prototype"></a><span data-ttu-id="445f1-463">Prototype</span><span class="sxs-lookup"><span data-stu-id="445f1-463">Prototype</span></span>

```C
UINT ux_device_class_audio_reception_start(UX_DEVICE_CLASS_AUDIO_STREAM *stream);
```

### <a name="description"></a><span data-ttu-id="445f1-464">Description</span><span class="sxs-lookup"><span data-stu-id="445f1-464">Description</span></span>

<span data-ttu-id="445f1-465">Bu işlev, ses akışında okuma ses verilerini başlatmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="445f1-465">This function is used to start audio data reading in audio streams.</span></span>

### <a name="parameters"></a><span data-ttu-id="445f1-466">Parametreler</span><span class="sxs-lookup"><span data-stu-id="445f1-466">Parameters</span></span>

- <span data-ttu-id="445f1-467">**Stream**: ses akışı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="445f1-467">**stream**: Pointer to the audio stream instance.</span></span>

### <a name="return-value"></a><span data-ttu-id="445f1-468">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="445f1-468">Return Value</span></span>

- <span data-ttu-id="445f1-469">**UX_SUCCESS** (0x00) Bu işlem başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="445f1-469">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="445f1-470">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) arabirim çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="445f1-470">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) The interface is down.</span></span>
- <span data-ttu-id="445f1-471">**UX_BUFFER_OVERFLOW** (0x5D) FIFO arabelleği dolu.</span><span class="sxs-lookup"><span data-stu-id="445f1-471">**UX_BUFFER_OVERFLOW** (0x5d) FIFO buffer is full.</span></span>
- <span data-ttu-id="445f1-472">İşlevden **UX_ERROR** (0xFF) hatası</span><span class="sxs-lookup"><span data-stu-id="445f1-472">**UX_ERROR** (0xFF) Error from function</span></span>

### <a name="example"></a><span data-ttu-id="445f1-473">Örnek</span><span class="sxs-lookup"><span data-stu-id="445f1-473">Example</span></span>

```C
/* Start stream data reception. */
status = ux_device_class_audio_reception_start(stream);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio_sample_read8"></a><span data-ttu-id="445f1-474">ux_device_class_audio_sample_read8</span><span class="sxs-lookup"><span data-stu-id="445f1-474">ux_device_class_audio_sample_read8</span></span>

<span data-ttu-id="445f1-475">Ses akışından 8 bit örneği oku</span><span class="sxs-lookup"><span data-stu-id="445f1-475">Read 8-bit sample from the Audio stream</span></span>

### <a name="prototype"></a><span data-ttu-id="445f1-476">Prototype</span><span class="sxs-lookup"><span data-stu-id="445f1-476">Prototype</span></span>

```C
UINT ux_device_class_audio_sample_read8(
    UX_DEVICE_CLASS_AUDIO_STREAM *stream, 
    UCHAR *buffer);
```

### <a name="description"></a><span data-ttu-id="445f1-477">Description</span><span class="sxs-lookup"><span data-stu-id="445f1-477">Description</span></span>

<span data-ttu-id="445f1-478">Bu işlev, belirtilen akıştan 8 bit ses örnek verilerini okur.</span><span class="sxs-lookup"><span data-stu-id="445f1-478">This function reads 8-bit audio sample data from the specified stream.</span></span>

<span data-ttu-id="445f1-479">Özellikle, FıFO 'daki geçerli ses çerçevesi arabelleğindeki örnek verileri okur.</span><span class="sxs-lookup"><span data-stu-id="445f1-479">Specifically, it reads the sample data from the current audio frame buffer in the FIFO.</span></span> <span data-ttu-id="445f1-480">Bir ses çerçevesindeki son örneği okurken, ana bilgisayardan daha fazla veri kabul etmek için kullanılabilmesi için çerçeve otomatik olarak serbest bırakılır.</span><span class="sxs-lookup"><span data-stu-id="445f1-480">Upon reading the last sample in an audio frame, the frame will be automatically freed so that it can be used to accept more data from the host.</span></span>

### <a name="parameters"></a><span data-ttu-id="445f1-481">Parametreler</span><span class="sxs-lookup"><span data-stu-id="445f1-481">Parameters</span></span>

- <span data-ttu-id="445f1-482">**Stream**: ses akışı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="445f1-482">**stream**: Pointer to the audio stream instance.</span></span>
- <span data-ttu-id="445f1-483">**buffer**: örnek baytı kaydetmek için arabelleğin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="445f1-483">**buffer**: Pointer to the buffer to save sample byte.</span></span>

### <a name="return-value"></a><span data-ttu-id="445f1-484">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="445f1-484">Return Value</span></span>

- <span data-ttu-id="445f1-485">**UX_SUCCESS** (0x00) Bu işlem başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="445f1-485">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="445f1-486">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) arabirim çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="445f1-486">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) The interface is down.</span></span>
- <span data-ttu-id="445f1-487">**UX_BUFFER_OVERFLOW** (0x5D) FIFO arabelleği null.</span><span class="sxs-lookup"><span data-stu-id="445f1-487">**UX_BUFFER_OVERFLOW** (0x5d) FIFO buffer is null.</span></span>
- <span data-ttu-id="445f1-488">İşlevden **UX_ERROR** (0xFF) hatası</span><span class="sxs-lookup"><span data-stu-id="445f1-488">**UX_ERROR** (0xFF) Error from function</span></span>

### <a name="example"></a><span data-ttu-id="445f1-489">Örnek</span><span class="sxs-lookup"><span data-stu-id="445f1-489">Example</span></span>

```C
/* Read a byte in audio FIFO. */

status = ux_device_class_audio_sample_read8(stream, &sample_byte);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio_sample_read16"></a><span data-ttu-id="445f1-490">ux_device_class_audio_sample_read16</span><span class="sxs-lookup"><span data-stu-id="445f1-490">ux_device_class_audio_sample_read16</span></span>

<span data-ttu-id="445f1-491">Ses akışından 16 bit örneği oku</span><span class="sxs-lookup"><span data-stu-id="445f1-491">Read 16-bit sample from the Audio stream</span></span>

### <a name="prototype"></a><span data-ttu-id="445f1-492">Prototype</span><span class="sxs-lookup"><span data-stu-id="445f1-492">Prototype</span></span>

```C
UINT ux_device_class_audio_sample_read16(
    UX_DEVICE_CLASS_AUDIO_STREAM *stream, 
    USHORT *buffer);
```

### <a name="description"></a><span data-ttu-id="445f1-493">Description</span><span class="sxs-lookup"><span data-stu-id="445f1-493">Description</span></span>

<span data-ttu-id="445f1-494">Bu işlev, belirtilen akıştan 16 bit ses örnek verilerini okur.</span><span class="sxs-lookup"><span data-stu-id="445f1-494">This function reads 16-bit audio sample data from the specified stream.</span></span>

<span data-ttu-id="445f1-495">Özellikle, FıFO 'daki geçerli ses çerçevesi arabelleğindeki örnek verileri okur.</span><span class="sxs-lookup"><span data-stu-id="445f1-495">Specifically, it reads the sample data from the current audio frame buffer in the FIFO.</span></span> <span data-ttu-id="445f1-496">Bir ses çerçevesindeki son örneği okurken, ana bilgisayardan daha fazla veri kabul etmek için kullanılabilmesi için çerçeve otomatik olarak serbest bırakılır.</span><span class="sxs-lookup"><span data-stu-id="445f1-496">Upon reading the last sample in an audio frame, the frame will be automatically freed so that it can be used to accept more data from the host.</span></span>

### <a name="parameters"></a><span data-ttu-id="445f1-497">Parametreler</span><span class="sxs-lookup"><span data-stu-id="445f1-497">Parameters</span></span>

- <span data-ttu-id="445f1-498">**Stream**: ses akışı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="445f1-498">**stream**: Pointer to the audio stream instance.</span></span>
- <span data-ttu-id="445f1-499">**buffer**: 16 bit örneği kaydetmek için arabelleğin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="445f1-499">**buffer**: Pointer to the buffer to save the 16-bit sample.</span></span>

### <a name="return-value"></a><span data-ttu-id="445f1-500">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="445f1-500">Return Value</span></span>

- <span data-ttu-id="445f1-501">**UX_SUCCESS** (0x00) Bu işlem başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="445f1-501">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="445f1-502">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) arabirim çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="445f1-502">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) The interface is down.</span></span>
- <span data-ttu-id="445f1-503">**UX_BUFFER_OVERFLOW** (0x5D) FIFO arabelleği null.</span><span class="sxs-lookup"><span data-stu-id="445f1-503">**UX_BUFFER_OVERFLOW** (0x5d) FIFO buffer is null.</span></span>
- <span data-ttu-id="445f1-504">İşlevden **UX_ERROR** (0xFF) hatası</span><span class="sxs-lookup"><span data-stu-id="445f1-504">**UX_ERROR** (0xFF) Error from function</span></span>

### <a name="example"></a><span data-ttu-id="445f1-505">Örnek</span><span class="sxs-lookup"><span data-stu-id="445f1-505">Example</span></span>

```C
/* Read a 16-bit sample in audio FIFO. */

status = ux_device_class_audio_sample_read16(stream, &sample_word);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio_sample_read24"></a><span data-ttu-id="445f1-506">ux_device_class_audio_sample_read24</span><span class="sxs-lookup"><span data-stu-id="445f1-506">ux_device_class_audio_sample_read24</span></span>

<span data-ttu-id="445f1-507">Ses akışından 24 bit örnek okuyun</span><span class="sxs-lookup"><span data-stu-id="445f1-507">Read 24-bit sample from the Audio stream</span></span>

### <a name="prototype"></a><span data-ttu-id="445f1-508">Prototype</span><span class="sxs-lookup"><span data-stu-id="445f1-508">Prototype</span></span>

```C
UINT ux_device_class_audio_sample_read24(
    UX_DEVICE_CLASS_AUDIO_STREAM *stream, 
    ULONG *buffer);
```

### <a name="description"></a><span data-ttu-id="445f1-509">Description</span><span class="sxs-lookup"><span data-stu-id="445f1-509">Description</span></span>

<span data-ttu-id="445f1-510">Bu işlev, belirtilen akıştan alınan 24 bit ses örnek verilerini okur.</span><span class="sxs-lookup"><span data-stu-id="445f1-510">This function reads 24-bit audio sample data from the specified stream.</span></span>

<span data-ttu-id="445f1-511">Özellikle, FıFO 'daki geçerli ses çerçevesi arabelleğindeki örnek verileri okur.</span><span class="sxs-lookup"><span data-stu-id="445f1-511">Specifically, it reads the sample data from the current audio frame buffer in the FIFO.</span></span> <span data-ttu-id="445f1-512">Bir ses çerçevesindeki son örneği okurken, ana bilgisayardan daha fazla veri kabul etmek için kullanılabilmesi için çerçeve otomatik olarak serbest bırakılır.</span><span class="sxs-lookup"><span data-stu-id="445f1-512">Upon reading the last sample in an audio frame, the frame will be automatically freed so that it can be used to accept more data from the host.</span></span>

### <a name="parameters"></a><span data-ttu-id="445f1-513">Parametreler</span><span class="sxs-lookup"><span data-stu-id="445f1-513">Parameters</span></span>

- <span data-ttu-id="445f1-514">**Stream**: ses akışı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="445f1-514">**stream**: Pointer to the audio stream instance.</span></span>
- <span data-ttu-id="445f1-515">**buffer**: 3 baytlık örneği kaydetmek için arabelleğin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="445f1-515">**buffer**: Pointer to the buffer to save the 3-byte sample.</span></span>

### <a name="return-value"></a><span data-ttu-id="445f1-516">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="445f1-516">Return Value</span></span>

- <span data-ttu-id="445f1-517">**UX_SUCCESS** (0x00) Bu işlem başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="445f1-517">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="445f1-518">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) arabirim çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="445f1-518">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) The interface is down.</span></span>
- <span data-ttu-id="445f1-519">**UX_BUFFER_OVERFLOW** (0x5D) FIFO arabelleği null.</span><span class="sxs-lookup"><span data-stu-id="445f1-519">**UX_BUFFER_OVERFLOW** (0x5d) FIFO buffer is null.</span></span>
- <span data-ttu-id="445f1-520">İşlevden **UX_ERROR** (0xFF) hatası</span><span class="sxs-lookup"><span data-stu-id="445f1-520">**UX_ERROR** (0xFF) Error from function</span></span>

### <a name="example"></a><span data-ttu-id="445f1-521">Örnek</span><span class="sxs-lookup"><span data-stu-id="445f1-521">Example</span></span>

```C
/* Read 3 bytes to in audio FIFO. */

status = ux_device_class_audio_sample_read24(stream, &sample_bytes);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio_sample_read32"></a><span data-ttu-id="445f1-522">ux_device_class_audio_sample_read32</span><span class="sxs-lookup"><span data-stu-id="445f1-522">ux_device_class_audio_sample_read32</span></span>

<span data-ttu-id="445f1-523">Ses akışından 32 bitlik örnek okuyun</span><span class="sxs-lookup"><span data-stu-id="445f1-523">Read 32-bit sample from the Audio stream</span></span>

### <a name="prototype"></a><span data-ttu-id="445f1-524">Prototype</span><span class="sxs-lookup"><span data-stu-id="445f1-524">Prototype</span></span>

```C
UINT ux_device_class_audio_sample_read32(
    UX_DEVICE_CLASS_AUDIO_STREAM *stream, 
    ULONG *buffer);
```

### <a name="description"></a><span data-ttu-id="445f1-525">Description</span><span class="sxs-lookup"><span data-stu-id="445f1-525">Description</span></span>

<span data-ttu-id="445f1-526">Bu işlev, belirtilen akıştan 32 bitlik ses örnek verilerini okur.</span><span class="sxs-lookup"><span data-stu-id="445f1-526">This function reads 32-bit audio sample data from the specified stream.</span></span>

<span data-ttu-id="445f1-527">Özellikle, FıFO 'daki geçerli ses çerçevesi arabelleğindeki örnek verileri okur.</span><span class="sxs-lookup"><span data-stu-id="445f1-527">Specifically, it reads the sample data from the current audio frame buffer in the FIFO.</span></span> <span data-ttu-id="445f1-528">Bir ses çerçevesindeki son örneği okurken, ana bilgisayardan daha fazla veri kabul etmek için kullanılabilmesi için çerçeve otomatik olarak serbest bırakılır.</span><span class="sxs-lookup"><span data-stu-id="445f1-528">Upon reading the last sample in an audio frame, the frame will be automatically freed so that it can be used to accept more data from the host.</span></span>

### <a name="parameters"></a><span data-ttu-id="445f1-529">Parametreler</span><span class="sxs-lookup"><span data-stu-id="445f1-529">Parameters</span></span>

- <span data-ttu-id="445f1-530">**Stream**: ses akışı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="445f1-530">**stream**: Pointer to the audio stream instance.</span></span>
- <span data-ttu-id="445f1-531">**buffer**: 4 baytlık verileri kaydetmek için arabelleğin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="445f1-531">**buffer**: Pointer to the buffer to save the 4-byte data.</span></span>

### <a name="return-value"></a><span data-ttu-id="445f1-532">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="445f1-532">Return Value</span></span>

- <span data-ttu-id="445f1-533">**UX_SUCCESS** (0x00) Bu işlem başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="445f1-533">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="445f1-534">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) arabirim çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="445f1-534">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) The interface is down.</span></span>
- <span data-ttu-id="445f1-535">**UX_BUFFER_OVERFLOW** (0x5D) FIFO arabelleği null.</span><span class="sxs-lookup"><span data-stu-id="445f1-535">**UX_BUFFER_OVERFLOW** (0x5d) FIFO buffer is null.</span></span>
- <span data-ttu-id="445f1-536">İşlevden **UX_ERROR** (0xFF) hatası</span><span class="sxs-lookup"><span data-stu-id="445f1-536">**UX_ERROR** (0xFF) Error from function</span></span>

### <a name="example"></a><span data-ttu-id="445f1-537">Örnek</span><span class="sxs-lookup"><span data-stu-id="445f1-537">Example</span></span>

```C
/* Read 4 bytes in audio FIFO. */

status = ux_device_class_audio_sample_read32(stream, &sample_bytes);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio_read_frame_get"></a><span data-ttu-id="445f1-538">ux_device_class_audio_read_frame_get</span><span class="sxs-lookup"><span data-stu-id="445f1-538">ux_device_class_audio_read_frame_get</span></span>

<span data-ttu-id="445f1-539">Ses akışındaki ses çerçevesine erişim sağlayın</span><span class="sxs-lookup"><span data-stu-id="445f1-539">Get access to audio frame in the Audio stream</span></span>

### <a name="prototype"></a><span data-ttu-id="445f1-540">Prototype</span><span class="sxs-lookup"><span data-stu-id="445f1-540">Prototype</span></span>

```C
UINT ux_device_class_audio_read_frame_get(
    UX_DEVICE_CLASS_AUDIO_STREAM *stream,
    UCHAR **frame_data, 
    ULONG *frame_length);
```

### <a name="description"></a><span data-ttu-id="445f1-541">Description</span><span class="sxs-lookup"><span data-stu-id="445f1-541">Description</span></span>

<span data-ttu-id="445f1-542">Bu işlev, ilk ses çerçevesi arabelleğini ve belirtilen akışın FıFO uzunluğunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="445f1-542">This function returns the first audio frame buffer and its length in the specified stream's FIFO.</span></span> <span data-ttu-id="445f1-543">Uygulama verileri işlemeyi tamamladıktan sonra FıFO 'daki çerçeve arabelleğini serbest bırakmak için ux_device_class_audio_read_frame_free kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="445f1-543">When the application is done processing the data, ux_device_class_audio_read_frame_free must be used to free the frame buffer in the FIFO.</span></span>

### <a name="parameters"></a><span data-ttu-id="445f1-544">Parametreler</span><span class="sxs-lookup"><span data-stu-id="445f1-544">Parameters</span></span>

- <span data-ttu-id="445f1-545">**Stream**: ses akışı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="445f1-545">**stream**: Pointer to the audio stream instance.</span></span>
- <span data-ttu-id="445f1-546">**frame_data**: veri işaretçisini döndürmek için veri işaretçisine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="445f1-546">**frame_data**: Pointer to data pointer to return the data pointer in.</span></span>
- <span data-ttu-id="445f1-547">**frame_length**: çerçeve uzunluğunu bayt sayısıyla kaydetmek için arabelleğin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="445f1-547">**frame_length**: Pointer to buffer to save the frame length in number of bytes.</span></span>

### <a name="return-value"></a><span data-ttu-id="445f1-548">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="445f1-548">Return Value</span></span>

- <span data-ttu-id="445f1-549">**UX_SUCCESS** (0x00) Bu işlem başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="445f1-549">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="445f1-550">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) arabirim çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="445f1-550">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) The interface is down.</span></span>
- <span data-ttu-id="445f1-551">**UX_BUFFER_OVERFLOW** (0x5D) FIFO arabelleği null.</span><span class="sxs-lookup"><span data-stu-id="445f1-551">**UX_BUFFER_OVERFLOW** (0x5d) FIFO buffer is null.</span></span>
- <span data-ttu-id="445f1-552">İşlevden **UX_ERROR** (0xFF) hatası</span><span class="sxs-lookup"><span data-stu-id="445f1-552">**UX_ERROR** (0xFF) Error from function</span></span>

### <a name="example"></a><span data-ttu-id="445f1-553">Örnek</span><span class="sxs-lookup"><span data-stu-id="445f1-553">Example</span></span>

```C
/* Get frame access. */

status = ux_device_class_audio_read_frame_get(stream, &frame, &frame_length);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio_read_frame_free"></a><span data-ttu-id="445f1-554">ux_device_class_audio_read_frame_free</span><span class="sxs-lookup"><span data-stu-id="445f1-554">ux_device_class_audio_read_frame_free</span></span>

<span data-ttu-id="445f1-555">Ses akışında ses çerçevesi arabelleğini serbest bırakma</span><span class="sxs-lookup"><span data-stu-id="445f1-555">Free an audio frame buffer in Audio stream</span></span>

### <a name="prototype"></a><span data-ttu-id="445f1-556">Prototype</span><span class="sxs-lookup"><span data-stu-id="445f1-556">Prototype</span></span>

```C
UINT ux_device_class_audio_read_frame_free(UX_DEVICE_CLASS_AUDIO_STREAM *stream);
```

### <a name="description"></a><span data-ttu-id="445f1-557">Description</span><span class="sxs-lookup"><span data-stu-id="445f1-557">Description</span></span>

<span data-ttu-id="445f1-558">Bu işlev, ana bilgisayardan veri alabilmesi için belirtilen akışın FıFO önünde ses çerçevesi arabelleğini serbest bırakır.</span><span class="sxs-lookup"><span data-stu-id="445f1-558">This function frees the audio frame buffer at the front of the specified stream's FIFO so that it can receive data from the host.</span></span>

### <a name="parameters"></a><span data-ttu-id="445f1-559">Parametreler</span><span class="sxs-lookup"><span data-stu-id="445f1-559">Parameters</span></span>

- <span data-ttu-id="445f1-560">**Stream**: ses akışı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="445f1-560">**stream**: Pointer to the audio stream instance.</span></span>

### <a name="return-value"></a><span data-ttu-id="445f1-561">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="445f1-561">Return Value</span></span>

- <span data-ttu-id="445f1-562">**UX_SUCCESS** (0x00) Bu işlem başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="445f1-562">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="445f1-563">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) arabirim çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="445f1-563">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) The interface is down.</span></span>
- <span data-ttu-id="445f1-564">**UX_BUFFER_OVERFLOW** (0x5D) FIFO arabelleği null.</span><span class="sxs-lookup"><span data-stu-id="445f1-564">**UX_BUFFER_OVERFLOW** (0x5d) FIFO buffer is null.</span></span>
- <span data-ttu-id="445f1-565">İşlevden **UX_ERROR** (0xFF) hatası</span><span class="sxs-lookup"><span data-stu-id="445f1-565">**UX_ERROR** (0xFF) Error from function</span></span>

### <a name="example"></a><span data-ttu-id="445f1-566">Örnek</span><span class="sxs-lookup"><span data-stu-id="445f1-566">Example</span></span>

```C
/* Refree a frame buffer in FIFO. */

status = ux_device_class_audio_read_frame_free(stream);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio_transmission_start"></a><span data-ttu-id="445f1-567">ux_device_class_audio_transmission_start</span><span class="sxs-lookup"><span data-stu-id="445f1-567">ux_device_class_audio_transmission_start</span></span>

<span data-ttu-id="445f1-568">Ses akışı için ses veri aktarımını Başlat</span><span class="sxs-lookup"><span data-stu-id="445f1-568">Start audio data transmission for the Audio stream</span></span>

### <a name="prototype"></a><span data-ttu-id="445f1-569">Prototype</span><span class="sxs-lookup"><span data-stu-id="445f1-569">Prototype</span></span>

```C
UINT ux_device_class_audio_transmission_start(UX_DEVICE_CLASS_AUDIO_STREAM *stream);
```

### <a name="description"></a><span data-ttu-id="445f1-570">Description</span><span class="sxs-lookup"><span data-stu-id="445f1-570">Description</span></span>

<span data-ttu-id="445f1-571">Bu işlev, ses sınıfında FıFO 'ya yazılmış ses verileri göndermeye başlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="445f1-571">This function is used to start sending audio data written to the FIFO in the audio class.</span></span>

### <a name="parameters"></a><span data-ttu-id="445f1-572">Parametreler</span><span class="sxs-lookup"><span data-stu-id="445f1-572">Parameters</span></span>

- <span data-ttu-id="445f1-573">**Stream**: ses akışı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="445f1-573">**stream**: Pointer to the audio stream instance.</span></span>

### <a name="return-value"></a><span data-ttu-id="445f1-574">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="445f1-574">Return Value</span></span>

- <span data-ttu-id="445f1-575">**UX_SUCCESS** (0x00) Bu işlem başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="445f1-575">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="445f1-576">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) arabirim çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="445f1-576">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) The interface is down.</span></span>
- <span data-ttu-id="445f1-577">**UX_BUFFER_OVERFLOW** (0x5D) FIFO arabelleği null.</span><span class="sxs-lookup"><span data-stu-id="445f1-577">**UX_BUFFER_OVERFLOW** (0x5d) FIFO buffer is null.</span></span>
- <span data-ttu-id="445f1-578">İşlevden **UX_ERROR** (0xFF) hatası</span><span class="sxs-lookup"><span data-stu-id="445f1-578">**UX_ERROR** (0xFF) Error from function</span></span>

### <a name="example"></a><span data-ttu-id="445f1-579">Örnek</span><span class="sxs-lookup"><span data-stu-id="445f1-579">Example</span></span>

```C
/* Start stream data transmission. */

status = ux_device_class_audio_transmission_start(stream);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio_frame_write"></a><span data-ttu-id="445f1-580">ux_device_class_audio_frame_write</span><span class="sxs-lookup"><span data-stu-id="445f1-580">ux_device_class_audio_frame_write</span></span>

<span data-ttu-id="445f1-581">Ses akışına bir ses çerçevesi yazma</span><span class="sxs-lookup"><span data-stu-id="445f1-581">Write an audio frame into the Audio stream</span></span>

### <a name="prototype"></a><span data-ttu-id="445f1-582">Prototype</span><span class="sxs-lookup"><span data-stu-id="445f1-582">Prototype</span></span>

```C
UINT ux_device_class_audio_frame_write(
    UX_DEVICE_CLASS_AUDIO_STREAM *stream,
    UCHAR *frame,
    ULONG frame_length);
```

### <a name="description"></a><span data-ttu-id="445f1-583">Description</span><span class="sxs-lookup"><span data-stu-id="445f1-583">Description</span></span>

<span data-ttu-id="445f1-584">Bu işlev, ses akışının FıFO ' a bir çerçeve yazar.</span><span class="sxs-lookup"><span data-stu-id="445f1-584">This function writes a frame to the audio stream's FIFO.</span></span> <span data-ttu-id="445f1-585">Çerçeve verileri, konağa gönderilebilmesi için FıFO 'daki kullanılabilir arabelleğe kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="445f1-585">The frame data is copied to the available buffer in the FIFO so that it can be sent to the host.</span></span>

### <a name="parameters"></a><span data-ttu-id="445f1-586">Parametreler</span><span class="sxs-lookup"><span data-stu-id="445f1-586">Parameters</span></span>

- <span data-ttu-id="445f1-587">**Stream**: ses akışı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="445f1-587">**stream**: Pointer to the audio stream instance.</span></span>
- <span data-ttu-id="445f1-588">**çerçeve**: çerçeve verileri işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="445f1-588">**frame**: Pointer to frame data.</span></span>
- <span data-ttu-id="445f1-589">**frame_length** Bayt sayısıyla çerçeve uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="445f1-589">**frame_length** Frame length in number of bytes.</span></span>

### <a name="return-value"></a><span data-ttu-id="445f1-590">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="445f1-590">Return Value</span></span>

- <span data-ttu-id="445f1-591">**UX_SUCCESS** (0x00) Bu işlem başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="445f1-591">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="445f1-592">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) arabirim çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="445f1-592">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) The interface is down.</span></span>
- <span data-ttu-id="445f1-593">**UX_BUFFER_OVERFLOW** (0x5D) FIFO arabelleği dolu.</span><span class="sxs-lookup"><span data-stu-id="445f1-593">**UX_BUFFER_OVERFLOW** (0x5d) FIFO buffer is full.</span></span>
- <span data-ttu-id="445f1-594">İşlevden **UX_ERROR** (0xFF) hatası</span><span class="sxs-lookup"><span data-stu-id="445f1-594">**UX_ERROR** (0xFF) Error from function</span></span>

### <a name="example"></a><span data-ttu-id="445f1-595">Örnek</span><span class="sxs-lookup"><span data-stu-id="445f1-595">Example</span></span>

```C
/* Get frame access. */

status = ux_device_class_audio_frame_write(stream, frame, frame_length);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio_write_frame_get"></a><span data-ttu-id="445f1-596">ux_device_class_audio_write_frame_get</span><span class="sxs-lookup"><span data-stu-id="445f1-596">ux_device_class_audio_write_frame_get</span></span>

<span data-ttu-id="445f1-597">Ses akışındaki ses çerçevesine erişim sağlayın</span><span class="sxs-lookup"><span data-stu-id="445f1-597">Get access to audio frame in the Audio stream</span></span>

### <a name="prototype"></a><span data-ttu-id="445f1-598">Prototype</span><span class="sxs-lookup"><span data-stu-id="445f1-598">Prototype</span></span>

```C
UINT ux_device_class_audio_write_frame_get(
    UX_DEVICE_CLASS_AUDIO_STREAM *stream,
    UCHAR **frame_data, 
    ULONG *frame_length);
```

### <a name="description"></a><span data-ttu-id="445f1-599">Description</span><span class="sxs-lookup"><span data-stu-id="445f1-599">Description</span></span>

<span data-ttu-id="445f1-600">Bu işlev, FıFO 'nun son ses çerçevesi arabelleğinin adresini alır; Ayrıca, ses çerçevesi arabelleğinin uzunluğunu da alır.</span><span class="sxs-lookup"><span data-stu-id="445f1-600">This function retrieves the address of the last audio frame buffer of the FIFO; it also retrieves the length of the audio frame buffer.</span></span> <span data-ttu-id="445f1-601">Uygulama, ses çerçevesi arabelleğini istenen verilerle doldurduktan sonra, ***ux_device_class_audio_write_frame_commit*** kare arabelleği eklemek/FIFO 'ya uygulamak için kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="445f1-601">After the application fills the audio frame buffer with its desired data, ***ux_device_class_audio_write_frame_commit*** must be used to add/commit the frame buffer to the FIFO.</span></span>

### <a name="parameters"></a><span data-ttu-id="445f1-602">Parametreler</span><span class="sxs-lookup"><span data-stu-id="445f1-602">Parameters</span></span>

- <span data-ttu-id="445f1-603">**Stream**: ses akışı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="445f1-603">**stream**: Pointer to the audio stream instance.</span></span>
- <span data-ttu-id="445f1-604">**frame_data**: çerçeve verisi işaretçisini döndürmek için çerçeve verisi işaretçisine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="445f1-604">**frame_data**: Pointer to frame data pointer to return the frame data pointer in.</span></span>
- <span data-ttu-id="445f1-605">**frame_length** Çerçeve uzunluğunu bayt sayısıyla kaydetmek için arabelleğin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="445f1-605">**frame_length** Pointer to the buffer to save frame length in number of bytes .</span></span>

### <a name="return-value"></a><span data-ttu-id="445f1-606">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="445f1-606">Return Value</span></span>

- <span data-ttu-id="445f1-607">**UX_SUCCESS** (0x00) Bu işlem başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="445f1-607">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="445f1-608">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) arabirim çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="445f1-608">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) The interface is down.</span></span>
- <span data-ttu-id="445f1-609">**UX_BUFFER_OVERFLOW** (0x5D) FIFO arabelleği dolu.</span><span class="sxs-lookup"><span data-stu-id="445f1-609">**UX_BUFFER_OVERFLOW** (0x5d) FIFO buffer is full.</span></span>
- <span data-ttu-id="445f1-610">İşlevden **UX_ERROR** (0xFF) hatası</span><span class="sxs-lookup"><span data-stu-id="445f1-610">**UX_ERROR** (0xFF) Error from function</span></span>

### <a name="example"></a><span data-ttu-id="445f1-611">Örnek</span><span class="sxs-lookup"><span data-stu-id="445f1-611">Example</span></span>

```C
/* Get frame access. */

status = ux_device_class_audio_write_frame_get(stream, &frame, &frame_length);

if(status != UX_SUCCESS)
     return;
```

## <a name="ux_device_class_audio_write_frame_commit"></a><span data-ttu-id="445f1-612">ux_device_class_audio_write_frame_commit</span><span class="sxs-lookup"><span data-stu-id="445f1-612">ux_device_class_audio_write_frame_commit</span></span>

<span data-ttu-id="445f1-613">Ses akışına ses çerçevesi arabelleği yürütün.</span><span class="sxs-lookup"><span data-stu-id="445f1-613">Commit an audio frame buffer in Audio stream.</span></span>

### <a name="prototype"></a><span data-ttu-id="445f1-614">Prototype</span><span class="sxs-lookup"><span data-stu-id="445f1-614">Prototype</span></span>

```C
UINT ux_device_class_audio_write_frame_commit(
    UX_DEVICE_CLASS_AUDIO_STREAM *stream, 
    ULONG length);
```

### <a name="description"></a><span data-ttu-id="445f1-615">Description</span><span class="sxs-lookup"><span data-stu-id="445f1-615">Description</span></span>

<span data-ttu-id="445f1-616">Bu işlev, arabellek konağa aktarılmaya hazırlandığından, son ses çerçevesi arabelleğini FıFO 'ya ekler/kaydeder; son ses çerçevesi arabelleğinin ux_device_class_write_frame_get ile doldurulmuş olması gerektiğini göz önünde bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="445f1-616">This function adds/commits the last audio frame buffer to the FIFO so the buffer is ready to be transferred to host; note the last audio frame buffer should have been filled out via ux_device_class_write_frame_get.</span></span>

### <a name="parameters"></a><span data-ttu-id="445f1-617">Parametreler</span><span class="sxs-lookup"><span data-stu-id="445f1-617">Parameters</span></span>

- <span data-ttu-id="445f1-618">**Stream**: ses akışı örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="445f1-618">**stream**: Pointer to the audio stream instance.</span></span>
- <span data-ttu-id="445f1-619">**uzunluk**: arabellekte Ready bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="445f1-619">**length**: Number of bytes ready in the buffer.</span></span>

### <a name="return-value"></a><span data-ttu-id="445f1-620">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="445f1-620">Return Value</span></span>

- <span data-ttu-id="445f1-621">**UX_SUCCESS** (0x00) Bu işlem başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="445f1-621">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="445f1-622">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) arabirim çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="445f1-622">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) The interface is down.</span></span>
- <span data-ttu-id="445f1-623">**UX_BUFFER_OVERFLOW** (0x5D) FIFO arabelleği fssull şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="445f1-623">**UX_BUFFER_OVERFLOW** (0x5d) FIFO buffer is fssull.</span></span>
- <span data-ttu-id="445f1-624">İşlevden **UX_ERROR** (0xFF) hatası</span><span class="sxs-lookup"><span data-stu-id="445f1-624">**UX_ERROR** (0xFF) Error from function</span></span>

### <a name="example"></a><span data-ttu-id="445f1-625">Örnek</span><span class="sxs-lookup"><span data-stu-id="445f1-625">Example</span></span>

```C
/* Commit a frame after fill values in buffer. */

status = ux_device_class_audio_write_frame_commit(stream, 192);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio10_control_process"></a><span data-ttu-id="445f1-626">ux_device_class_audio10_control_process</span><span class="sxs-lookup"><span data-stu-id="445f1-626">ux_device_class_audio10_control_process</span></span>

<span data-ttu-id="445f1-627">USB ses 1,0 denetim isteklerini işle</span><span class="sxs-lookup"><span data-stu-id="445f1-627">Process USB Audio 1.0 control requests</span></span>

### <a name="prototype"></a><span data-ttu-id="445f1-628">Prototype</span><span class="sxs-lookup"><span data-stu-id="445f1-628">Prototype</span></span>

```C
UINT ux_device_class_audio10_control_process(
    UX_DEVICE_CLASS_AUDIO *audio,
    UX_SLAVE_TRANSFER *transfer_request,
    UX_DEVICE_CLASS_AUDIO10_CONTROL_GROUP *group);
```

### <a name="description"></a><span data-ttu-id="445f1-629">Description</span><span class="sxs-lookup"><span data-stu-id="445f1-629">Description</span></span>

<span data-ttu-id="445f1-630">Bu işlev, denetim uç noktasındaki ana bilgisayar tarafından gönderilen temel istekleri, USB ses 1,0 'e özgü bir türle yönetir.</span><span class="sxs-lookup"><span data-stu-id="445f1-630">This function manages basic requests sent by the host on the control endpoint with a USB Audio 1.0 specific type.</span></span>

<span data-ttu-id="445f1-631">Birim ve sessiz isteklerin ses 1,0 özellikleri işlevinde işlenir.</span><span class="sxs-lookup"><span data-stu-id="445f1-631">Audio 1.0 features of volume and mute requests are processed in the function.</span></span> <span data-ttu-id="445f1-632">İstekleri işlerken, istekleri yanıtlamak ve denetim değişikliklerini depolamak için son parametre (Grup) tarafından geçirilen önceden tanımlanmış veriler kullanılır.</span><span class="sxs-lookup"><span data-stu-id="445f1-632">When processing the requests, pre-defined data passed by the last parameter (group) is used to answer requests and store control changes.</span></span>

### <a name="parameters"></a><span data-ttu-id="445f1-633">Parametreler</span><span class="sxs-lookup"><span data-stu-id="445f1-633">Parameters</span></span>

- <span data-ttu-id="445f1-634">**Ses**: ses örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="445f1-634">**audio**: Pointer to the audio instance.</span></span>
- <span data-ttu-id="445f1-635">**Transfer**: aktarım isteği örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="445f1-635">**transfer**: Pointer to the transfer request instance.</span></span>
- <span data-ttu-id="445f1-636">**Grup**: istek işlemi için veri grubu.</span><span class="sxs-lookup"><span data-stu-id="445f1-636">**group**: Data group for request process.</span></span>

### <a name="return-value"></a><span data-ttu-id="445f1-637">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="445f1-637">Return Value</span></span>

- <span data-ttu-id="445f1-638">**UX_SUCCESS** (0x00) Bu işlem başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="445f1-638">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="445f1-639">İşlevden **UX_ERROR** (0xFF) hatası</span><span class="sxs-lookup"><span data-stu-id="445f1-639">**UX_ERROR** (0xFF) Error from function</span></span>

### <a name="example"></a><span data-ttu-id="445f1-640">Örnek</span><span class="sxs-lookup"><span data-stu-id="445f1-640">Example</span></span>

```C
/* Initialize audio 1.0 control values. */

audio_control[0].ux_device_class_audio10_control_fu_id = 2;
audio_control[0].ux_device_class_audio10_control_mute[0] = 0;
audio_control[0].ux_device_class_audio10_control_volume[0] = 0;
audio_control[1].ux_device_class_audio10_control_fu_id = 5;
audio_control[1].ux_device_class_audio10_control_mute[0] = 0;
audio_control[1].ux_device_class_audio10_control_volume[0] = 0;

/* Handle request and update control values.
Note here only mute and volume for master channel is supported.
*/

status = ux_device_class_audio10_control_process(audio, transfer, &group);
if (status == UX_SUCCESS)
{
    /* Request handled, check changes */
    switch(audio_control[0].ux_device_class_audio10_control_changed)
    {
        case UX_DEVICE_CLASS_AUDIO10_CONTROL_MUTE_CHANGED:
        case UX_DEVICE_CLASS_AUDIO10_CONTROL_VOLUME_CHANGED:
        default: break;
    }
}
```

## <a name="ux_device_class_audio20_control_process"></a><span data-ttu-id="445f1-641">ux_device_class_audio20_control_process</span><span class="sxs-lookup"><span data-stu-id="445f1-641">ux_device_class_audio20_control_process</span></span>

<span data-ttu-id="445f1-642">USB ses 1,0 denetim isteklerini işle</span><span class="sxs-lookup"><span data-stu-id="445f1-642">Process USB Audio 1.0 control requests</span></span>

### <a name="prototype"></a><span data-ttu-id="445f1-643">Prototype</span><span class="sxs-lookup"><span data-stu-id="445f1-643">Prototype</span></span>
```C
UINT ux_device_class_audio20_control_process(
    UX_DEVICE_CLASS_AUDIO *audio,
    UX_SLAVE_TRANSFER *transfer_request,
    UX_DEVICE_CLASS_AUDIO20_CONTROL_GROUP *group);
```

### <a name="description"></a><span data-ttu-id="445f1-644">Description</span><span class="sxs-lookup"><span data-stu-id="445f1-644">Description</span></span>

<span data-ttu-id="445f1-645">Bu işlev, denetim uç noktasındaki ana bilgisayar tarafından gönderilen temel istekleri, USB ses 2,0 'e özgü bir türle yönetir.</span><span class="sxs-lookup"><span data-stu-id="445f1-645">This function manages basic requests sent by the host on the control endpoint with a USB Audio 2.0 specific type.</span></span>

<span data-ttu-id="445f1-646">Ses 2,0 örnekleme hızı (tek sabit sıklık varsayıldı), birim ve sessiz isteklerin özellikleri işlevinde işlenir.</span><span class="sxs-lookup"><span data-stu-id="445f1-646">Audio 2.0 sampling rate (assumed single fixed frequency), features of volume and mute requests are processed in the function.</span></span> <span data-ttu-id="445f1-647">İstekleri işlerken, istekleri yanıtlamak ve denetim değişikliklerini depolamak için son parametre (Grup) tarafından geçirilen önceden tanımlanmış veriler kullanılır.</span><span class="sxs-lookup"><span data-stu-id="445f1-647">When processing the requests, pre-defined data passed by the last parameter (group) is used to answer requests and store control changes.</span></span>

### <a name="parameters"></a><span data-ttu-id="445f1-648">Parametreler</span><span class="sxs-lookup"><span data-stu-id="445f1-648">Parameters</span></span>

- <span data-ttu-id="445f1-649">**Ses**: ses örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="445f1-649">**audio**: Pointer to the audio instance.</span></span>
- <span data-ttu-id="445f1-650">**Transfer**: aktarım isteği örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="445f1-650">**transfer**: Pointer to the transfer request instance.</span></span>
- <span data-ttu-id="445f1-651">**Grup**: istek işlemi için veri grubu.</span><span class="sxs-lookup"><span data-stu-id="445f1-651">**group**: Data group for request process.</span></span>

### <a name="return-value"></a><span data-ttu-id="445f1-652">Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="445f1-652">Return Value</span></span>

- <span data-ttu-id="445f1-653">**UX_SUCCESS** (0x00) Bu işlem başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="445f1-653">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="445f1-654">İşlevden **UX_ERROR** (0xFF) hatası</span><span class="sxs-lookup"><span data-stu-id="445f1-654">**UX_ERROR** (0xFF) Error from function</span></span>

### <a name="example"></a><span data-ttu-id="445f1-655">Örnek</span><span class="sxs-lookup"><span data-stu-id="445f1-655">Example</span></span>

```C
/* Initialize audio 2.0 control values. */

audio_control[0].ux_device_class_audio20_control_cs_id = 0x10;
audio_control[0].ux_device_class_audio20_control_sampling_frequency = 48000;
audio_control[0].ux_device_class_audio20_control_fu_id = 2;
audio_control[0].ux_device_class_audio20_control_mute[0] = 0;
audio_control[0].ux_device_class_audio20_control_volume_min[0] = 0;
audio_control[0].ux_device_class_audio20_control_volume_max[0] = 100;
audio_control[0].ux_device_class_audio20_control_volume[0] = 50;
audio_control[1].ux_device_class_audio20_control_cs_id = 0x10;
audio_control[1].ux_device_class_audio20_control_sampling_frequency = 48000;
audio_control[1].ux_device_class_audio20_control_fu_id = 5;
audio_control[1].ux_device_class_audio20_control_mute[0] = 0;
audio_control[1].ux_device_class_audio20_control_volume_min[0] = 0;
audio_control[1].ux_device_class_audio20_control_volume_max[0] = 100;
audio_control[1].ux_device_class_audio20_control_volume[0] = 50;

/* Handle request and update control values.
Note here only mute and volume for master channel is supported.
*/

status = ux_device_class_audio20_control_process(audio, transfer, &group);
if (status == UX_SUCCESS)
{
    /* Request handled, check changes */
    switch(audio_control[0].ux_device_class_audio20_control_changed)
    {
        case UX_DEVICE_CLASS_AUDIO20_CONTROL_MUTE_CHANGED:
        case UX_DEVICE_CLASS_AUDIO20_CONTROL_VOLUME_CHANGED:
        default: break;
    }
}
```
