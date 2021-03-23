---
title: Bölüm 10-müşteri Kullanıcı Etkinlikleri
description: Bu bölüm, bu tür olaylar için Kullanıcı tanımlı olayların ve özel simgelerin ve bilgi alanlarının nasıl oluşturulacağı hakkında bir açıklama içerir.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: 635c2d79922de9d5649bab841ae946cac862056c
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104827605"
---
# <a name="chapter-10---customer-user-events"></a><span data-ttu-id="6541f-103">Bölüm 10-müşteri Kullanıcı Etkinlikleri</span><span class="sxs-lookup"><span data-stu-id="6541f-103">Chapter 10 - Customer user events</span></span>

<span data-ttu-id="6541f-104">Bu bölüm, bu tür olaylar için Kullanıcı tanımlı olayların ve özel simgelerin ve bilgi alanlarının nasıl oluşturulacağı hakkında bir açıklama içerir.</span><span class="sxs-lookup"><span data-stu-id="6541f-104">This chapter contains a description of how to create user-defined events and custom icons and information fields for such events.</span></span> <span data-ttu-id="6541f-105">Bu bölüm aşağıdaki bölümleri içerir:</span><span class="sxs-lookup"><span data-stu-id="6541f-105">This chapter includes the following sections:</span></span> 

## <a name="inserting-user-defined-events"></a><span data-ttu-id="6541f-106">User-Defined olayları ekleme</span><span class="sxs-lookup"><span data-stu-id="6541f-106">Inserting User-Defined Events</span></span>

<span data-ttu-id="6541f-107">ThreadX, geliştiricilerin kendi Kullanıcı tanımlı olaylarını günlüğe kaydetmelerine olanak sağlar. bu sayede, TraceX tarafından grafiksel olarak görüntülenebilen daha fazla yararlı bilgi sağlanır.</span><span class="sxs-lookup"><span data-stu-id="6541f-107">ThreadX provides the ability for developers to log their own user-defined events, providing even more useful information that can be viewed graphically by TraceX.</span></span> <span data-ttu-id="6541f-108">Kullanıcı tanımlı olay numaraları aralığı</span><span class="sxs-lookup"><span data-stu-id="6541f-108">User-defined event numbers range from</span></span>

<span data-ttu-id="6541f-109">**TX_TRACE_USER_EVENT_START** (4096) ile **TX_TRACE_USER_EVENT_END** (65535) (dahil).</span><span class="sxs-lookup"><span data-stu-id="6541f-109">**TX_TRACE_USER_EVENT_START** (4096) through **TX_TRACE_USER_EVENT_END** (65535), inclusive.</span></span> <span data-ttu-id="6541f-110">İzleme arabelleğindeki olayların yerleştirilmesi, Bölüm 5 ' te tanımlanan ***tx_trace_user_event_insert*** aracılığıyla yapılır.</span><span class="sxs-lookup"><span data-stu-id="6541f-110">The placement of the events in the trace buffer is done via the ***tx_trace_user_event_insert***, defined in Chapter 5.</span></span> <span data-ttu-id="6541f-111">Aşağıdaki örnek, Kullanıcı tanımlı olay 4096 ve olay 4098 gibi, hedefteki geçerli izleme arabelleğine iki Kullanıcı tanımlı olay eklemeyi çağırır:</span><span class="sxs-lookup"><span data-stu-id="6541f-111">The following example calls insert two user-defined events into the current trace buffer on the target, namely user-defined event 4096 and event 4098:</span></span>

```c
tx_trace_user_event_insert(4096, 1, 2, 3, 4);
tx_trace_user_event_insert(4098,0x100,0x200,0x300,0x400);
```

## <a name="default-display-of-user-defined-events"></a><span data-ttu-id="6541f-112">User-Defined olaylarının varsayılan görüntüsü</span><span class="sxs-lookup"><span data-stu-id="6541f-112">Default Display of User-Defined Events</span></span>

![Kullanıcı tanımlı olay simgesi](./media/user-guide/tx-events/image0.png)

<span data-ttu-id="6541f-114">Varsayılan olarak, TraceX, Bölüm 6 ' da açıklandığı şekilde, varsayılan kullanıcı tanımlı bir olay simgesiyle tüm Kullanıcı olaylarını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="6541f-114">By default, TraceX displays all user events with a default user-defined Event icon as described in Chapter 6.</span></span> <span data-ttu-id="6541f-115">Şekil 28, önceki ***tx_trace_user_event_insert*** örnekleri aracılığıyla olay arabelleğine yerleştirilmiş olan 452 ve 453 olaylarına yönelik varsayılan kullanıcı tanımlı olay simgesini gösterir.</span><span class="sxs-lookup"><span data-stu-id="6541f-115">Figure 28 shows the default user-defined event icon for events 452 and 453, which were placed in the event buffer via the previous ***tx_trace_user_event_insert*** examples.</span></span>

<span data-ttu-id="6541f-116">![Kullanıcı tanımlı olayların varsayılan görüntüsünün ekran görüntüsü. ](./media/user-guide/10.1.png)
 **Şekil 28**</span><span class="sxs-lookup"><span data-stu-id="6541f-116">![Screenshot of the default display of user-defined events.](./media/user-guide/10.1.png)
**FIGURE 28**</span></span>

<span data-ttu-id="6541f-117">Ayrıntılı bilgiler, Kullanıcı tanımlı olaylar için de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="6541f-117">Detailed information is also available for user-defined Events.</span></span> <span data-ttu-id="6541f-118">Şekil 28, olay numarası 4096 olan olay 452 için ayrıntılı olay bilgilerini gösterir ve belirtilen dört bilgi alanını gösterir.</span><span class="sxs-lookup"><span data-stu-id="6541f-118">Figure 28 shows the detailed event information for event 452, which has event number 4096 and shows the specified four information fields.</span></span>

<span data-ttu-id="6541f-119">![Kullanıcı tanımlı olayların ayrıntılı görüntüsünün ekran görüntüsü. ](./media/user-guide/10.2.png)
 **Şekil 29**</span><span class="sxs-lookup"><span data-stu-id="6541f-119">![Screenshot of the detailed display of user-defined events.](./media/user-guide/10.2.png)
**FIGURE 29**</span></span>

## <a name="defining-custom-user-defined-event-icons"></a><span data-ttu-id="6541f-120">Özel User-Defined olay simgeleri tanımlama</span><span class="sxs-lookup"><span data-stu-id="6541f-120">Defining Custom User-Defined Event Icons</span></span>

<span data-ttu-id="6541f-121">TraceX, kullanıcıya özel kullanıcı tanımlı olay simgeleri ve özel bilgi alanı etiketleri oluşturma yeteneği de sağlar.</span><span class="sxs-lookup"><span data-stu-id="6541f-121">TraceX also provides the user the ability to create custom user-defined event icons and custom information field labels.</span></span> <span data-ttu-id="6541f-122">Bu yetenek, \***tracex_custom. trxc** _ yapılandırma dosyasına olay simgesi belirtimleri eklenerek elde edilir.</span><span class="sxs-lookup"><span data-stu-id="6541f-122">This capability is achieved by adding event icon specifications to the \***tracex_custom.trxc** _ configuration file.</span></span> <span data-ttu-id="6541f-123">Bu dosya, Kullanıcı tanımlı TraceX yükleme dizininizin _ *_CustomEvents_*\* alt dizininde bulunur ve varsayılan olarak c:\ Azure_RTOS \TraceX.</span><span class="sxs-lookup"><span data-stu-id="6541f-123">This file is located in the _ *_CustomEvents_*\* subdirectory of your user-defined TraceX installation directory, which defaults to c:\Azure_RTOS\TraceX.</span></span> <span data-ttu-id="6541f-124">Şekil 30 ' da örnek bir dizin yolu gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="6541f-124">An example directory path is shown in Figure 30.</span></span>

<span data-ttu-id="6541f-125">![Örnek dizin yolunun ekran görüntüsü. ](./media/user-guide/custom_events_folder.png)
 **Şekil 30**</span><span class="sxs-lookup"><span data-stu-id="6541f-125">![Screenshot of an example directory path.](./media/user-guide/custom_events_folder.png)
**FIGURE 30**</span></span>

<span data-ttu-id="6541f-126">***Tracex_custom. trxc*** özel olay yapılandırma dosyası, sıfır veya daha fazla özel olay tanımı içeren basıt bir ASCII metin dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="6541f-126">The ***tracex_custom.trxc*** custom event configuration file is a simple ASCII text file containing zero or more custom event definitions.</span></span> <span data-ttu-id="6541f-127">Dosya biçimi aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="6541f-127">The format of the file is as follows:</span></span>

```c
//Comments
**Start **
[custom event definition(s)] **End **
```

<span data-ttu-id="6541f-128">Başlangıç ve bitiş arasındaki her satır, tek bir özel olay tanımlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6541f-128">Each line between Start and End is used to define a single custom event.</span></span> <span data-ttu-id="6541f-129">TraceX, özel olay tanımlanmadığında bu dosyanın şablon sürümünü sağlar ("Başlat" ve "End" etiketleri arasında hiçbir şey).</span><span class="sxs-lookup"><span data-stu-id="6541f-129">TraceX provides a template version of this file with no custom events defined (nothing between the "Start" and "End" labels).</span></span> <span data-ttu-id="6541f-130">Özel bir olay tanımının biçimi aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="6541f-130">The format of a custom event definition is as follows:</span></span>

<span data-ttu-id="6541f-131">**sayı, ad, kısaltma, top_color, bottom_color, Label1, etiket 2, etiket 2, Label4**</span><span class="sxs-lookup"><span data-stu-id="6541f-131">**number, name, abbreviation, top_color, bottom_color, label1, label2, label2, label4**</span></span>

<span data-ttu-id="6541f-132">burada:</span><span class="sxs-lookup"><span data-stu-id="6541f-132">where:</span></span>

- <span data-ttu-id="6541f-133">Sayı: Kullanıcı tanımlı olay numarasını tanımlar, bu arada 4096 ile 65535 arasında (dahil).</span><span class="sxs-lookup"><span data-stu-id="6541f-133">number: Defines the user-defined event number, between 4096 and 65535, inclusive.</span></span></th>
- <span data-ttu-id="6541f-134">ad: Kullanıcı tanımlı etkinliğin mantıksal adını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="6541f-134">name: Defines the logical name for the user-defined event.</span></span></td>
- <span data-ttu-id="6541f-135">kısaltma: iki harfli Kullanıcı tanımlı olay kısaltmasını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="6541f-135">abbreviation: Defines the two-letter user-defined event abbreviation.</span></span></td>
- <span data-ttu-id="6541f-136">top_color: parantez içinde üç basamaklı bir sayı olan simgenin üst yarısı için RGB değerini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="6541f-136">top_color: Defines the RGB value for the top-half of the icon, which is a three-digit number in parenthesis.</span></span> <span data-ttu-id="6541f-137">Bazı tipik RGB tanımları şunlardır</span><span class="sxs-lookup"><span data-stu-id="6541f-137">Some typical RGB definitions are</span></span>
  - <span data-ttu-id="6541f-138">SIYAH = (0, 0, 0)</span><span class="sxs-lookup"><span data-stu-id="6541f-138">BLACK = (0,0,0)</span></span>       
  - <span data-ttu-id="6541f-139">BEYAZ = (255.255.255)</span><span class="sxs-lookup"><span data-stu-id="6541f-139">WHITE = (255,255,255)</span></span>
  - <span data-ttu-id="6541f-140">KıRMıZı = (255, 0, 0)</span><span class="sxs-lookup"><span data-stu-id="6541f-140">RED = (255,0,0)</span></span>     
  - <span data-ttu-id="6541f-141">YEŞIL = (0255, 0)</span><span class="sxs-lookup"><span data-stu-id="6541f-141">GREEN = (0,255,0)</span></span>     
  - <span data-ttu-id="6541f-142">MAVI = (0, 0255)</span><span class="sxs-lookup"><span data-stu-id="6541f-142">BLUE = (0,0,255)</span></span>     
  - <span data-ttu-id="6541f-143">SARı = (255255, 0)</span><span class="sxs-lookup"><span data-stu-id="6541f-143">YELLOW = (255,255,0)</span></span>   
  - <span data-ttu-id="6541f-144">CAMGÖBEĞI = (0255.255)</span><span class="sxs-lookup"><span data-stu-id="6541f-144">CYAN = (0,255,255)</span></span>   
  - <span data-ttu-id="6541f-145">MACENTA = (255, 0255)</span><span class="sxs-lookup"><span data-stu-id="6541f-145">MAGENTA = (255,0,255)</span></span>   
  <span data-ttu-id="6541f-146">RBG belirtiminin kullanılması kullanıcıya Kullanıcı tanımlı her simge için çok çeşitli renkler sağlar.</span><span class="sxs-lookup"><span data-stu-id="6541f-146">Using the RBG specification gives the user a broad range of colors for each user-defined icon.</span></span> <span data-ttu-id="6541f-147">RBG renk tanımı hakkında daha fazla bilgi için bkz.: https://en.wikipedia.org/wiki/RGB#Digital_representations</span><span class="sxs-lookup"><span data-stu-id="6541f-147">For more information on RBG color definition, see: https://en.wikipedia.org/wiki/RGB#Digital_representations</span></span>
- <span data-ttu-id="6541f-148">botton_color: parantez içinde üç basamaklı bir sayı olan simgenin alt yarısı için RGB değerini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="6541f-148">botton_color: Defines the RGB value for the bottom half of the icon, which is a three-digit number in parenthesis.</span></span>
- <span data-ttu-id="6541f-149">Label1: _ *_tx_trace_user_event_insert_*\* çağrısında belirtildiği gibi, \***info_field_1** _ etiketi.</span><span class="sxs-lookup"><span data-stu-id="6541f-149">label1: Label for ***info_field_1** _, as specified in the _ *_tx_trace_user_event_insert_** call.</span></span>
- <span data-ttu-id="6541f-150">Etiket 2: _ *_tx_trace_user_event_insert_*\* çağrısında belirtildiği gibi, \***info_field_2** _ etiketi.</span><span class="sxs-lookup"><span data-stu-id="6541f-150">label2: Label for ***info_field_2** _, as specified in the _ *_tx_trace_user_event_insert_** call.</span></span>
- <span data-ttu-id="6541f-151">etiket 3: _ *_tx_trace_user_event_insert_*\* çağrısında belirtildiği gibi, \***info_field_3** _ etiketi.</span><span class="sxs-lookup"><span data-stu-id="6541f-151">label3: Label for ***info_field_3** _, as specified in the _ *_tx_trace_user_event_insert_** call.</span></span>
- <span data-ttu-id="6541f-152">Label4: _ *_tx_trace_user_event_insert_*\* çağrısında belirtildiği gibi, \***info_field_4** _ etiketi.</span><span class="sxs-lookup"><span data-stu-id="6541f-152">label4: Label for ***info_field_4** _, as specified in the _ *_tx_trace_user_event_insert_** call.</span></span>

<span data-ttu-id="6541f-153">Bu bölümde kullanılan iki Kullanıcı tanımlı olayın örnek tanımları Şekil 10,4 ' de gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="6541f-153">Example definitions for each of the two user-defined events used in this chapter are shown in Figure 10.4.</span></span> <span data-ttu-id="6541f-154">İlk tanım, \***tracex_custom. trxc** _ dosyasının 5. satırında olay 4096 ' dir.</span><span class="sxs-lookup"><span data-stu-id="6541f-154">The first definition is for event 4096 at line 5 of the \***tracex_custom.trxc** _ file.</span></span> <span data-ttu-id="6541f-155">Bu tanım, _ \* First_User_Event \* \* adlı Kullanıcı tanımlı olay 4096 ' i verir, **Fe**'nin iki harfli bir kısaltmasını belirtir, simgenin üst kısmını kırmızı, simgenin en alt kısmını yeşil hale getirir ve bilgi alanlarını **First_Info1**, **First_Info2**, **First_Info3** ve **First_Info4** olarak adlandırır.</span><span class="sxs-lookup"><span data-stu-id="6541f-155">This definition gives user-defined event 4096 the name _\*First_User_Event\*\*, specifies a two-letter abbreviation of **FE**, makes the top portion of the icon red, the bottom portion of the icon green, and names the information fields as **First_Info1**, **First_Info2**, **First_Info3**, and **First_Info4**.</span></span> <span data-ttu-id="6541f-156">Kullanıcı tanımlı olay 4098, **_tracex_custom. trxc_**' nin 6. satırında benzer şekilde tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="6541f-156">User-defined event 4098 is defined similarly at line 6 of **_tracex_custom.trxc_**.</span></span>

<span data-ttu-id="6541f-157">![Kullanıcı tanımlı olaylar için örnek tanımlarının ekran görüntüsü. ](./media/user-guide/10.4.png)
 **Şekil 31**</span><span class="sxs-lookup"><span data-stu-id="6541f-157">![Screenshot of the example definitions for the user-defined events.](./media/user-guide/10.4.png)
**FIGURE 31**</span></span>

<span data-ttu-id="6541f-158">\***Tracex_custom. trxc** _ dosyası başlatma sırasında tracex tarafından okunduğundan, özel simge tanımlarının etkili olabilmesi Için tracex 'in çıkış ve yeniden başlatılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="6541f-158">Since the \***tracex_custom.trxc** _ file is read by TraceX during initialization, TraceX must be exited and restarted before the custom icon definitions can take effect.</span></span> <span data-ttu-id="6541f-159">Şekil 32, _ *_tracex_custom. trxc_* \* ' de tanımlanan özel olay simgeleri ile 452 ve 453 Kullanıcı tanımlı olayların tracex görüntüsünü gösterir.</span><span class="sxs-lookup"><span data-stu-id="6541f-159">Figure 32 shows the TraceX display of user-defined events 452 and 453 with the custom event icons defined in _\*_tracex_custom.trxc_\*\*.</span></span>

<span data-ttu-id="6541f-160">![Özel olay simgeleriyle Kullanıcı tanımlı olayların ekran görüntüsü. ](./media/user-guide/10.5.png)
 **Şekil 32**</span><span class="sxs-lookup"><span data-stu-id="6541f-160">![Screenshot of the TraceX display of user defined events with the custom event icons.](./media/user-guide/10.5.png)
**FIGURE 32**</span></span>

<span data-ttu-id="6541f-161">Özel olay tanımındaki ek bilgiler çift tıklama, fare üzerinden veya geçerli olay düğmesine tıklayarak seçtiğiniz olay olduğunda gösterilir.</span><span class="sxs-lookup"><span data-stu-id="6541f-161">The additional information in the custom event definition is shown when the event you select using a double-click, mouse-over, or clicking the current event button.</span></span> <span data-ttu-id="6541f-162">Şekil 33, olay 452 ' de çift tıklama seçimini gösterir.</span><span class="sxs-lookup"><span data-stu-id="6541f-162">Figure 33 shows the double-click selection on event 452.</span></span> <span data-ttu-id="6541f-163">Olay adı ve bilgi alanları, ***tracex_custom. trxc*** öğesine eklenen örnek tanımıyla eşleşir.</span><span class="sxs-lookup"><span data-stu-id="6541f-163">The event name and information fields all match the sample definition that was added to ***tracex_custom.trxc***.</span></span>

<span data-ttu-id="6541f-164">![Bir olayda çift tıklama seçiminin ekran görüntüsü. ](./media/user-guide/10.6.png)
 **Şekil 33**</span><span class="sxs-lookup"><span data-stu-id="6541f-164">![Screenshot of the double-click selection on an event.](./media/user-guide/10.6.png)
**FIGURE 33**</span></span>
