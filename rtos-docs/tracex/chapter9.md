---
title: Bölüm 9-Azure RTOS USBX izleme olayları
description: Bu bölüm, TraceX tarafından görünen Azure RTOS USBX olaylarının bir açıklamasını içerir.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: 98561fe1d131e1d1b0893b7d89eb720881a82ac8
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104828349"
---
# <a name="chapter-9---azure-rtos-usbx-trace-events"></a><span data-ttu-id="c7285-103">Bölüm 9-Azure RTOS USBX izleme olayları</span><span class="sxs-lookup"><span data-stu-id="c7285-103">Chapter 9 - Azure RTOS USBX trace events</span></span>

<span data-ttu-id="c7285-104">Bu bölüm, TraceX tarafından görünen Azure RTOS USBX olaylarının bir açıklamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="c7285-104">This chapter contains a description of the Azure RTOS USBX events displayed by TraceX.</span></span> 

## <a name="list-of-events-and-icons"></a><span data-ttu-id="c7285-105">Olay ve simgelerin listesi</span><span class="sxs-lookup"><span data-stu-id="c7285-105">List of Events and Icons</span></span>

<span data-ttu-id="c7285-106">Aşağıda, TraceX tarafından görünen USBX olaylarının bir listesi verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="c7285-106">The following is a list of USBX events displayed by TraceX.</span></span>

| <span data-ttu-id="c7285-107">Simge</span><span class="sxs-lookup"><span data-stu-id="c7285-107">Icon</span></span>                             | <span data-ttu-id="c7285-108">Anlamı</span><span class="sxs-lookup"><span data-stu-id="c7285-108">Meaning</span></span>                               |
| -------------------------------- | ------------------------------------- |
| ![Cihaz sınıfı C D C etkinleştir simgesi](./media/user-guide/usbx-events/image1.png)    | <span data-ttu-id="c7285-110">**Device Class CDC etkinleştir** *(ux_device_class_cdc_activate)*</span><span class="sxs-lookup"><span data-stu-id="c7285-110">**Device Class Cdc Activate** *(ux_device_class_cdc_activate)*</span></span> |
| ![Cihaz sınıfı C D C devre dışı bırakma simgesi](./media/user-guide/usbx-events/image2.png)    | <span data-ttu-id="c7285-112">**Device Class CDC devre dışı bırak** *(ux_device_class_cdc_deactivate)*</span><span class="sxs-lookup"><span data-stu-id="c7285-112">**Device Class Cdc Deactivate** *(ux_device_class_cdc_deactivate)*</span></span> |
| ![Cihaz sınıfı C D C okuma simgesi](./media/user-guide/usbx-events/image3.png)    | <span data-ttu-id="c7285-114">**Aygıt sınıfı CDC okuma** *(ux_device_class_cdc_read)*</span><span class="sxs-lookup"><span data-stu-id="c7285-114">**Device Class Cdc Read** *(ux_device_class_cdc_read)*</span></span> |
| ![Cihaz sınıfı C D C yazma simgesi](./media/user-guide/usbx-events/image4.png)    | <span data-ttu-id="c7285-116">**Aygıt sınıfı CDC yazma** *(ux_device_class_cdc_write)*</span><span class="sxs-lookup"><span data-stu-id="c7285-116">**Device Class Cdc Write** *(ux_device_class_cdc_write)*</span></span> |
| ![Device Class Dpump etkinleştir simgesi](./media/user-guide/usbx-events/image5.png)    | <span data-ttu-id="c7285-118">**Device Class Dpump etkinleştir** *(ux_device_class_dpump_activate)*</span><span class="sxs-lookup"><span data-stu-id="c7285-118">**Device Class Dpump Activate** *(ux_device_class_dpump_activate)*</span></span> |
| ![Cihaz sınıfı Dpump devre dışı bırakma simgesi](./media/user-guide/usbx-events/image6.png)    | <span data-ttu-id="c7285-120">**Cihaz sınıfı Dpump devre dışı bırakma** *(ux_device_class_dpump_deactivate)*</span><span class="sxs-lookup"><span data-stu-id="c7285-120">**Device Class Dpump Deactivate** *(ux_device_class_dpump_deactivate)*</span></span> |
| ![Cihaz sınıfı Dpump okuma simgesi](./media/user-guide/usbx-events/image7.png)    | <span data-ttu-id="c7285-122">**Cihaz sınıfı Dpump okuma** *(ux_device_class_dpump_read)*</span><span class="sxs-lookup"><span data-stu-id="c7285-122">**Device Class Dpump Read** *(ux_device_class_dpump_read)*</span></span> |
| ![Device Class Dpump yazma simgesi](./media/user-guide/usbx-events/image8.png)    | <span data-ttu-id="c7285-124">**Cihaz sınıfı Dpump yazma** *(ux_device_class_dpump_write)*</span><span class="sxs-lookup"><span data-stu-id="c7285-124">**Device Class Dpump Write** *(ux_device_class_dpump_write)*</span></span> |
| ![Device Class HID etkinleştirme simgesi](./media/user-guide/usbx-events/image9.png)    | <span data-ttu-id="c7285-126">**Device Class HID etkinleştir** *(ux_device_class_hid_activate)*</span><span class="sxs-lookup"><span data-stu-id="c7285-126">**Device Class Hid Activate** *(ux_device_class_hid_activate)*</span></span> |
| ![Cihaz sınıfı HID devre dışı bırakma simgesi](./media/user-guide/usbx-events/image10.png)    | <span data-ttu-id="c7285-128">**Cihaz sınıfı HID devre dışı bırakma** *(ux_device_class_hid_deactivate)*</span><span class="sxs-lookup"><span data-stu-id="c7285-128">**Device Class Hid Deactivate** *(ux_device_class_hid_deactivate)*</span></span> |
| ![Cihaz sınıfı HID tanımlayıcısı gönderme simgesi](./media/user-guide/usbx-events/image11.png)    | <span data-ttu-id="c7285-130">**Cihaz sınıfı HID tanımlayıcısı gönderme** *(ux_device_class_hid_descriptor_send)*</span><span class="sxs-lookup"><span data-stu-id="c7285-130">**Device Class Hid Descriptor Send** *(ux_device_class_hid_descriptor_send)*</span></span> |
| ![Cihaz sınıfı HID olayı al simgesi](./media/user-guide/usbx-events/image12.png)    | <span data-ttu-id="c7285-132">**Cihaz sınıfı HID olayı Get** *(ux_device_class_hid_event_get)*</span><span class="sxs-lookup"><span data-stu-id="c7285-132">**Device Class Hid Event Get** *(ux_device_class_hid_event_get)*</span></span> |
| ![Cihaz sınıfı HID olay kümesi simgesi](./media/user-guide/usbx-events/image13.png)    | <span data-ttu-id="c7285-134">**Cihaz sınıfı HID olay kümesi** *(ux_device_class_hid_event_set)*</span><span class="sxs-lookup"><span data-stu-id="c7285-134">**Device Class Hid Event Set** *(ux_device_class_hid_event_set)*</span></span> |
| ![Cihaz sınıfı HID raporu al simgesi](./media/user-guide/usbx-events/image14.png)    | <span data-ttu-id="c7285-136">**Cihaz sınıfı HID raporu Get** *(ux_device_class_hid_report_get)*</span><span class="sxs-lookup"><span data-stu-id="c7285-136">**Device Class Hid Report Get** *(ux_device_class_hid_report_get)*</span></span> |
| ![Cihaz sınıfı HID rapor kümesi simgesi](./media/user-guide/usbx-events/image15.png)    | <span data-ttu-id="c7285-138">**Cihaz sınıfı HID rapor kümesi** *(ux_device_class_hid_report_set)*</span><span class="sxs-lookup"><span data-stu-id="c7285-138">**Device Class Hid Report Set** *(ux_device_class_hid_report_set)*</span></span> |
| ![Cihaz sınıfı Pima etkinleştirme simgesi](./media/user-guide/usbx-events/image16.png)    | <span data-ttu-id="c7285-140">**Device Class Pima etkinleştir** *(ux_device_class_pima_activate)*</span><span class="sxs-lookup"><span data-stu-id="c7285-140">**Device Class Pima Activate** *(ux_device_class_pima_activate)*</span></span> |
| ![Cihaz sınıfı Pima devre dışı bırakma simgesi](./media/user-guide/usbx-events/image17.png)    | <span data-ttu-id="c7285-142">**Cihaz sınıfı Pima devre dışı bırakma** *(ux_device_class_pima_deactivate)*</span><span class="sxs-lookup"><span data-stu-id="c7285-142">**Device Class Pima Deactivate** *(ux_device_class_pima_deactivate)*</span></span> |
| ![Cihaz sınıfı Pima cihaz bilgileri gönderme simgesi](./media/user-guide/usbx-events/image18.png)    | <span data-ttu-id="c7285-144">**Cihaz sınıfı Pima cihaz bilgileri gönderme** *(ux_device_class_pima_device_info_send)*</span><span class="sxs-lookup"><span data-stu-id="c7285-144">**Device Class Pima Device Info Send** *(ux_device_class_pima_device_info_send)*</span></span> |
| ![Device Class Pima olayı al simgesi](./media/user-guide/usbx-events/image19.png)    | <span data-ttu-id="c7285-146">**Cihaz sınıfı Pima olayı Get** *(ux_device_class_pima_event_get)*</span><span class="sxs-lookup"><span data-stu-id="c7285-146">**Device Class Pima Event Get** *(ux_device_class_pima_event_get)*</span></span> |
| ![Cihaz sınıfı Pima olayı kümesi simgesi](./media/user-guide/usbx-events/image20.png)    | <span data-ttu-id="c7285-148">**Device Class Pima olay kümesi** *(ux_device_class_pima_event_set)*</span><span class="sxs-lookup"><span data-stu-id="c7285-148">**Device Class Pima Event Set** *(ux_device_class_pima_event_set)*</span></span> |
| ![Cihaz sınıfı Pima nesnesi ekleme simgesi](./media/user-guide/usbx-events/image21.png)    | <span data-ttu-id="c7285-150">**Cihaz sınıfı Pima nesnesi ekleme** *(ux_device_class_pima_object_add)*</span><span class="sxs-lookup"><span data-stu-id="c7285-150">**Device Class Pima Object Add** *(ux_device_class_pima_object_add)*</span></span> |
| ![Aygıt sınıfı Pima nesnesi verileri al simgesi](./media/user-guide/usbx-events/image22.png)    | <span data-ttu-id="c7285-152">**Cihaz sınıfı Pima nesnesi verileri al** *(ux_device_class_pima_object_data_get)*</span><span class="sxs-lookup"><span data-stu-id="c7285-152">**Device Class Pima Object Data Get** *(ux_device_class_pima_object_data_get)*</span></span> |
| ![Cihaz sınıfı Pima nesnesi verileri gönderme simgesi](./media/user-guide/usbx-events/image23.png)    | <span data-ttu-id="c7285-154">**Device Class Pima nesne verileri gönderme** *(ux_device_class_pima_object_data_send)*</span><span class="sxs-lookup"><span data-stu-id="c7285-154">**Device Class Pima Object Data Send** *(ux_device_class_pima_object_data_send)*</span></span> |
| ![Device Class Pima nesnesi silme simgesi](./media/user-guide/usbx-events/image24.png)    | <span data-ttu-id="c7285-156">**Device Class Pima nesnesi silme** *(ux_device_class_pima_object_delete)*</span><span class="sxs-lookup"><span data-stu-id="c7285-156">**Device Class Pima Object Delete** *(ux_device_class_pima_object_delete)*</span></span> |
| ![Cihaz sınıfı Pima nesnesi gönderme simgesini Işler](./media/user-guide/usbx-events/image25.png)    | <span data-ttu-id="c7285-158">**Cihaz sınıfı Pima nesnesi gönderme tutamaçları** *(ux_device_class_pima_object_handles_send)*</span><span class="sxs-lookup"><span data-stu-id="c7285-158">**Device Class Pima Object Handles Send** *(ux_device_class_pima_object_handles_send)*</span></span> |
| ![Device Class Pima nesne bilgisi al simgesi](./media/user-guide/usbx-events/image26.png)    | <span data-ttu-id="c7285-160">**Cihaz sınıfı Pima nesnesi bilgileri Get** *(ux_device_class_pima_object_info_get)*</span><span class="sxs-lookup"><span data-stu-id="c7285-160">**Device Class Pima Object Info Get** *(ux_device_class_pima_object_info_get)*</span></span> |
| ![Device Class Pima nesne bilgileri gönderme simgesi](./media/user-guide/usbx-events/image27.png)    | <span data-ttu-id="c7285-162">**Device Class Pima nesne bilgileri gönderme** *(ux_device_class_pima_object_info_send)*</span><span class="sxs-lookup"><span data-stu-id="c7285-162">**Device Class Pima Object Info Send** *(ux_device_class_pima_object_info_send)*</span></span> |
| ![Cihaz sınıfı Pima nesneleri numara Gönder simgesi](./media/user-guide/usbx-events/image28.png)    | <span data-ttu-id="c7285-164">**Cihaz sınıfı Pima nesneleri numara gönderme** *(ux_device_class_pima_objects_number_send)*</span><span class="sxs-lookup"><span data-stu-id="c7285-164">**Device Class Pima Objects Number Send** *(ux_device_class_pima_objects_number_send)*</span></span> |
| ![Device Class Pima kısmi nesne verileri al simgesi](./media/user-guide/usbx-events/image29.png)    | <span data-ttu-id="c7285-166">**Device Class Pima kısmi nesne verileri al** *(ux_device_class_pima_partial_object_data_get)*</span><span class="sxs-lookup"><span data-stu-id="c7285-166">**Device Class Pima Partial Object Data Get** *(ux_device_class_pima_partial_object_data_get)*</span></span> |
| ![Cihaz sınıfı Pima yanıtı gönderme simgesi](./media/user-guide/usbx-events/image30.png)    | <span data-ttu-id="c7285-168">**Cihaz sınıfı Pima yanıtı gönderme** *(ux_device_class_pima_response_send)*</span><span class="sxs-lookup"><span data-stu-id="c7285-168">**Device Class Pima Response Send** *(ux_device_class_pima_response_send)*</span></span>|
| ![Cihaz sınıfı Pima depolama g D Gönder simgesi](./media/user-guide/usbx-events/image31.png)    | <span data-ttu-id="c7285-170">**Cihaz sınıfı Pima depolama kimliği gönderme** *(ux_device_class_pima_storage_id_send)*</span><span class="sxs-lookup"><span data-stu-id="c7285-170">**Device Class Pima Storage Id Send** *(ux_device_class_pima_storage_id_send)*</span></span> |
| ![Cihaz sınıfı Pima depolama bilgileri gönderme simgesi](./media/user-guide/usbx-events/image32.png)    | <span data-ttu-id="c7285-172">**Cihaz sınıfı Pima depolama bilgileri gönderme** *(ux_device_class_pima_storage_info_send)*</span><span class="sxs-lookup"><span data-stu-id="c7285-172">**Device Class Pima Storage Info Send** *(ux_device_class_pima_storage_info_send)*</span></span> |
| ![Cihaz sınıfı R N D ı etkinleştirme simgesi](./media/user-guide/usbx-events/image33.png)    | <span data-ttu-id="c7285-174">**Cihaz sınıfı rndis etkinleştir** *(ux_device_class_rndis_activate)*</span><span class="sxs-lookup"><span data-stu-id="c7285-174">**Device Class Rndis Activate** *(ux_device_class_rndis_activate)*</span></span> |
| ![Cihaz sınıfı R N D ı devre dışı bırak simgesi](./media/user-guide/usbx-events/image34.png)    | <span data-ttu-id="c7285-176">**Cihaz sınıfı rndis devre dışı bırak** *(ux_device_class_rndis_deactivate)*</span><span class="sxs-lookup"><span data-stu-id="c7285-176">**Device Class Rndis Deactivate** *(ux_device_class_rndis_deactivate)*</span></span> |
| ![Cihaz sınıfı R N D ı Ileti Keep Aliveicon](./media/user-guide/usbx-events/image35.png)    | <span data-ttu-id="c7285-178">**Cihaz sınıfı rndis Iletisi canlı tut** *(ux_device_class_rndis_msg_keep_alive)*</span><span class="sxs-lookup"><span data-stu-id="c7285-178">**Device Class Rndis Message Keep Alive** *(ux_device_class_rndis_msg_keep_alive)*</span></span> |
| ![Cihaz sınıfı R N D ı Ileti sorgu simgesi](./media/user-guide/usbx-events/image36.png)    | <span data-ttu-id="c7285-180">**Cihaz sınıfı rndis Ileti sorgusu** *(ux_device_class_rndis_msg_query)*</span><span class="sxs-lookup"><span data-stu-id="c7285-180">**Device Class Rndis Message Query** *(ux_device_class_rndis_msg_query)*</span></span> |
| ![Cihaz sınıfı R N D ı Ileti sıfırlama simgesi](./media/user-guide/usbx-events/image37.png)    | <span data-ttu-id="c7285-182">**Cihaz sınıfı rndis Ileti sıfırlama** *(ux_device_class_rndis_msg_reset)*</span><span class="sxs-lookup"><span data-stu-id="c7285-182">**Device Class Rndis Message Reset** *(ux_device_class_rndis_msg_reset)*</span></span> |
| ![Cihaz sınıfı R N D ı Ileti kümesi simgesi](./media/user-guide/usbx-events/image38.png)    | <span data-ttu-id="c7285-184">**Cihaz sınıfı rndis Ileti kümesi** *(ux_device_class_rndis_msg_set)*</span><span class="sxs-lookup"><span data-stu-id="c7285-184">**Device Class Rndis Message Set** *(ux_device_class_rndis_msg_set)*</span></span> |
| ![Cihaz sınıfı R N D ı paket alma simgesi](./media/user-guide/usbx-events/image39.png)    | <span data-ttu-id="c7285-186">**Cihaz sınıfı rndis paket alma** *(ux_device_class_rndis_packet_receive)*</span><span class="sxs-lookup"><span data-stu-id="c7285-186">**Device Class Rndis Packet Receive** *(ux_device_class_rndis_packet_receive)*</span></span> |
| ![Cihaz sınıfı R N D ı paket Iletme simgesi](./media/user-guide/usbx-events/image40.png)    | <span data-ttu-id="c7285-188">**Cihaz sınıfı rndis paket iletimi** *(ux_device_class_rndis_packet_transmit)*</span><span class="sxs-lookup"><span data-stu-id="c7285-188">**Device Class Rndis Packet Transmit** *(ux_device_class_rndis_packet_transmit)*</span></span> |
| ![Cihaz sınıfı depolama etkinleştirme simgesi](./media/user-guide/usbx-events/image41.png)    | <span data-ttu-id="c7285-190">**Cihaz sınıfı depolama etkinleştir** *(ux_device_class_storage_activate)*</span><span class="sxs-lookup"><span data-stu-id="c7285-190">**Device Class Storage Activate** *(ux_device_class_storage_activate)*</span></span> |
| ![Cihaz sınıfı depolamayı devre dışı bırakma simgesi](./media/user-guide/usbx-events/image42.png)    | <span data-ttu-id="c7285-192">**Cihaz sınıfı depolamayı devre dışı bırakma** *(ux_device_class_storage_deactivate)*</span><span class="sxs-lookup"><span data-stu-id="c7285-192">**Device Class Storage Deactivate** *(ux_device_class_storage_deactivate)*</span></span> |
| ![Cihaz sınıfı depolama biçimi simgesi](./media/user-guide/usbx-events/image43.png)    | <span data-ttu-id="c7285-194">**Cihaz sınıfı depolama biçimi** *(ux_device_class_storage_format)*</span><span class="sxs-lookup"><span data-stu-id="c7285-194">**Device Class Storage Format** *(ux_device_class_storage_format)*</span></span> |
| ![Cihaz sınıfı depolama sorgulama simgesi](./media/user-guide/usbx-events/image44.png)    | <span data-ttu-id="c7285-196">**Cihaz sınıfı depolama sorgusu** *(ux_device_class_storage_inquiry)*</span><span class="sxs-lookup"><span data-stu-id="c7285-196">**Device Class Storage Inquiry** *(ux_device_class_storage_inquiry)*</span></span> |
| ![Cihaz sınıfı depolama modu seçme simgesi](./media/user-guide/usbx-events/image45.png)    | <span data-ttu-id="c7285-198">**Cihaz sınıfı depolama modu seçme** *(ux_device_class_storage_mode_select)*</span><span class="sxs-lookup"><span data-stu-id="c7285-198">**Device Class Storage Mode Select** *(ux_device_class_storage_mode_select)*</span></span> |
| ![Cihaz sınıfı depolama modu algılama simgesi](./media/user-guide/usbx-events/image46.png)    | <span data-ttu-id="c7285-200">**Cihaz sınıfı depolama modu algılama** *(ux_device_class_storage_mode_sense)*</span><span class="sxs-lookup"><span data-stu-id="c7285-200">**Device Class Storage Mode Sense** *(ux_device_class_storage_mode_sense)*</span></span> |
| ![Cihaz sınıfı depolaması medya kaldırma simgesine Izin vermeyi engelliyor](./media/user-guide/usbx-events/image47.png)    | <span data-ttu-id="c7285-202">**Cihaz sınıfı depolaması medya kaldırılmasına Izin vermeyi engelliyor** *(ux_device_class_storage_prevent_allow_media_removal)*</span><span class="sxs-lookup"><span data-stu-id="c7285-202">**Device Class Storage Prevent Allow Media Removal** *(ux_device_class_storage_prevent_allow_media_removal)*</span></span> |
| ![Cihaz sınıfı depolama okuma simgesi](./media/user-guide/usbx-events/image48.png)    | <span data-ttu-id="c7285-204">**Cihaz sınıfı depolama okuma** *(ux_device_class_storage_read)*</span><span class="sxs-lookup"><span data-stu-id="c7285-204">**Device Class Storage Read** *(ux_device_class_storage_read)*</span></span> |
| ![Cihaz sınıfı depolama okuma kapasitesi simgesi](./media/user-guide/usbx-events/image49.png)    | <span data-ttu-id="c7285-206">**Cihaz sınıfı depolama okuma kapasitesi** *(ux_device_class_storage_read_capacity)*</span><span class="sxs-lookup"><span data-stu-id="c7285-206">**Device Class Storage Read Capacity** *(ux_device_class_storage_read_capacity)*</span></span> |
| ![Cihaz sınıfı depolama okuma biçimi kapasitesi simgesi](./media/user-guide/usbx-events/image50.png)    | <span data-ttu-id="c7285-208">**Cihaz sınıfı depolama okuma biçimi kapasitesi** *(ux_device_class_storage_read_format_capacity)*</span><span class="sxs-lookup"><span data-stu-id="c7285-208">**Device Class Storage Read Format Capacity** *(ux_device_class_storage_read_format_capacity)*</span></span> |
| ![Device Class depolama okuma TOC simgesi](./media/user-guide/usbx-events/image51.png)    | <span data-ttu-id="c7285-210">**Device Class DEPOLAMASı TOC okuma** *(ux_device_class_storage_read_toc)*</span><span class="sxs-lookup"><span data-stu-id="c7285-210">**Device Class Storage Read TOC** *(ux_device_class_storage_read_toc)*</span></span> |
| ![Cihaz sınıfı depolama Isteği algılama simgesi](./media/user-guide/usbx-events/image52.png)    | <span data-ttu-id="c7285-212">**Cihaz sınıfı depolama Isteği algılama** *(ux_device_class_storage_request_sense)*</span><span class="sxs-lookup"><span data-stu-id="c7285-212">**Device Class Storage Request Sense** *(ux_device_class_storage_request_sense)*</span></span> |
| ![Cihaz sınıfı depolama başlatma durdurma simgesi](./media/user-guide/usbx-events/image53.png)    | <span data-ttu-id="c7285-214">**Cihaz sınıfı depolama başlatma durdurma** *(ux_device_class_storage_start_stop)*</span><span class="sxs-lookup"><span data-stu-id="c7285-214">**Device Class Storage Start Stop** *(ux_device_class_storage_start_stop)*</span></span> |
| ![Cihaz sınıfı depolama sınaması hazırlanıyor simgesi](./media/user-guide/usbx-events/image54.png)    | <span data-ttu-id="c7285-216">**Cihaz sınıfı depolama sınaması hazırlanıyor** *(ux_device_class_storage_test_ready)*</span><span class="sxs-lookup"><span data-stu-id="c7285-216">**Device Class Storage Test Ready** *(ux_device_class_storage_test_ready)*</span></span> |
| ![Cihaz sınıfı depolama doğrulama simgesi](./media/user-guide/usbx-events/image55.png)    | <span data-ttu-id="c7285-218">**Cihaz sınıfı depolama doğrulaması** *(ux_device_class_storage_verify)*</span><span class="sxs-lookup"><span data-stu-id="c7285-218">**Device Class Storage Verify** *(ux_device_class_storage_verify)*</span></span> |
| ![Cihaz sınıfı depolama yazma simgesi](./media/user-guide/usbx-events/image56.png)    | <span data-ttu-id="c7285-220">**Cihaz sınıfı depolama yazma** *(ux_device_class_storage_write)*</span><span class="sxs-lookup"><span data-stu-id="c7285-220">**Device Class Storage Write** *(ux_device_class_storage_write)*</span></span> |
| ![Cihaz yığını alternatif ayarı al simgesi](./media/user-guide/usbx-events/image57.png)    | <span data-ttu-id="c7285-222">**Cihaz yığını alternatif ayarı al** *(ux_device_stack_alternate_setting_get)*</span><span class="sxs-lookup"><span data-stu-id="c7285-222">**Device Stack Alternate Setting Get** *(ux_device_stack_alternate_setting_get)*</span></span> |
| ![Cihaz yığını alternatif ayarı kümesi simgesi](./media/user-guide/usbx-events/image58.png)    | <span data-ttu-id="c7285-224">**Cihaz yığını alternatif ayar kümesi** *(ux_device_stack_alternate_setting_set)*</span><span class="sxs-lookup"><span data-stu-id="c7285-224">**Device Stack Alternate Setting Set** *(ux_device_stack_alternate_setting_set)*</span></span> |
| ![Cihaz yığını sınıfı kayıt simgesi](./media/user-guide/usbx-events/image59.png)    | <span data-ttu-id="c7285-226">**Cihaz yığını sınıf kaydı** *(ux_device_stack_class_register)*</span><span class="sxs-lookup"><span data-stu-id="c7285-226">**Device Stack Class Register** *(ux_device_stack_class_register)*</span></span> |
| ![Cihaz yığını temiz Özellik simgesi](./media/user-guide/usbx-events/image60.png)    | <span data-ttu-id="c7285-228">**Cihaz yığını temiz Özellik** *(ux_device_stack_clear_feature)*</span><span class="sxs-lookup"><span data-stu-id="c7285-228">**Device Stack Clear Feature** *(ux_device_stack_clear_feature)*</span></span> |
| ![Cihaz yığını yapılandırması Get simgesi](./media/user-guide/usbx-events/image61.png)    | <span data-ttu-id="c7285-230">**Cihaz yığını yapılandırma Get** *(ux_device_stack_configuration_get)*</span><span class="sxs-lookup"><span data-stu-id="c7285-230">**Device Stack Configuration Get** *(ux_device_stack_configuration_get)*</span></span> |
| ![Cihaz yığını yapılandırma kümesi simgesi](./media/user-guide/usbx-events/image62.png)    | <span data-ttu-id="c7285-232">**Cihaz yığını yapılandırma kümesi** *(ux_device_stack_configuration_set)*</span><span class="sxs-lookup"><span data-stu-id="c7285-232">**Device Stack Configuration Set** *(ux_device_stack_configuration_set)*</span></span> |
| ![Cihaz yığını bağlantı simgesi](./media/user-guide/usbx-events/image63.png)    | <span data-ttu-id="c7285-234">**Cihaz yığını bağlantısı** *(ux_device_stack_connect)*</span><span class="sxs-lookup"><span data-stu-id="c7285-234">**Device Stack Connect** *(ux_device_stack_connect)*</span></span> |
| ![Cihaz yığını tanımlayıcısı gönderme simgesi](./media/user-guide/usbx-events/image64.png)    | <span data-ttu-id="c7285-236">**Cihaz yığını tanımlayıcısı gönderme** *(ux_device_stack_descriptor_send)*</span><span class="sxs-lookup"><span data-stu-id="c7285-236">**Device Stack Descriptor Send** *(ux_device_stack_descriptor_send)*</span></span> |
| ![Cihaz yığını bağlantı kesme simgesi](./media/user-guide/usbx-events/image65.png)    | <span data-ttu-id="c7285-238">**Cihaz yığını bağlantısını kesme** *(ux_device_stack_disconnect)*</span><span class="sxs-lookup"><span data-stu-id="c7285-238">**Device Stack Disconnect** *(ux_device_stack_disconnect)*</span></span> |
| ![Cihaz yığını uç noktası kabin simgesi](./media/user-guide/usbx-events/image66.png)    | <span data-ttu-id="c7285-240">**Cihaz yığını uç noktası kabini** *(ux_device_stack_endpoint_stall)*</span><span class="sxs-lookup"><span data-stu-id="c7285-240">**Device Stack Endpoint Stall** *(ux_device_stack_endpoint_stall)*</span></span> |
| ![Cihaz yığını durum Al simgesi](./media/user-guide/usbx-events/image67.png)    | <span data-ttu-id="c7285-242">**Cihaz yığını Get durumu** *(ux_device_stack_get_status)*</span><span class="sxs-lookup"><span data-stu-id="c7285-242">**Device Stack Get Status** *(ux_device_stack_get_status)*</span></span> |
| ![Cihaz yığını ana bilgisayarı uyandırma simgesi](./media/user-guide/usbx-events/image68.png)    | <span data-ttu-id="c7285-244">**Cihaz yığın ana bilgisayarı uyandırma** *(ux_device_stack_host_wakeup)*</span><span class="sxs-lookup"><span data-stu-id="c7285-244">**Device Stack Host Wakeup** *(ux_device_stack_host_wakeup)*</span></span> |
| ![Cihaz yığını başlatma simgesi](./media/user-guide/usbx-events/image69.png)    | <span data-ttu-id="c7285-246">**Cihaz yığını başlatma** *(ux_device_stack_initialize)*</span><span class="sxs-lookup"><span data-stu-id="c7285-246">**Device Stack Initialize** *(ux_device_stack_initialize)*</span></span> |
| ![Cihaz yığını arabirimi silme simgesi](./media/user-guide/usbx-events/image70.png)    | <span data-ttu-id="c7285-248">**Cihaz yığını arabirimini silme** *(ux_device_stack_interface_delete)*</span><span class="sxs-lookup"><span data-stu-id="c7285-248">**Device Stack Interface Delete** *(ux_device_stack_interface_delete)*</span></span> |
| ![Cihaz yığını arabirimi al simgesi](./media/user-guide/usbx-events/image71.png)    | <span data-ttu-id="c7285-250">**Cihaz yığını arabirimi al** *(ux_device_stack_interface_get)*</span><span class="sxs-lookup"><span data-stu-id="c7285-250">**Device Stack Interface Get** *(ux_device_stack_interface_get)*</span></span> |
| ![Cihaz yığını arabirim kümesi simgesi](./media/user-guide/usbx-events/image72.png)    | <span data-ttu-id="c7285-252">**Cihaz yığını arabirim kümesi** *(ux_device_stack_interface_set)*</span><span class="sxs-lookup"><span data-stu-id="c7285-252">**Device Stack Interface Set** *(ux_device_stack_interface_set)*</span></span> |
| ![Cihaz yığını kümesi özellik simgesi](./media/user-guide/usbx-events/image73.png)    | <span data-ttu-id="c7285-254">**Cihaz yığını kümesi özelliği** *(ux_device_stack_set_feature)*</span><span class="sxs-lookup"><span data-stu-id="c7285-254">**Device Stack Set Feature** *(ux_device_stack_set_feature)*</span></span> |
| ![Cihaz yığını aktarım Iptali simgesi](./media/user-guide/usbx-events/image74.png)    | <span data-ttu-id="c7285-256">**Cihaz yığını aktarımı iptali** *(ux_device_stack_transfer_abort)*</span><span class="sxs-lookup"><span data-stu-id="c7285-256">**Device Stack Transfer Abort** *(ux_device_stack_transfer_abort)*</span></span> |
| ![\* Cihaz yığını tüm Isteği Iptal et simgesi](./media/user-guide/usbx-events/image75.png)    | <span data-ttu-id="c7285-258">**Cihaz yığın aktarımı tüm Istek iptali** *(ux_device_stack_transfer_all_request_abort)*</span><span class="sxs-lookup"><span data-stu-id="c7285-258">**Device Stack Transfer All Request Abort** *(ux_device_stack_transfer_all_request_abort)*</span></span> |
| ![Cihaz yığını aktarım Isteği simgesi](./media/user-guide/usbx-events/image76.png)    | <span data-ttu-id="c7285-260">**Cihaz yığını aktarım isteği** *(ux_device_stack_transfer_request)*</span><span class="sxs-lookup"><span data-stu-id="c7285-260">**Device Stack Transfer Request** *(ux_device_stack_transfer_request)*</span></span> |
| ![Ana bilgisayar sınıfı ASIX etkinleştir simgesi](./media/user-guide/usbx-events/image77.png)    | <span data-ttu-id="c7285-262">**Ana bilgisayar sınıfı Aaltıetkinleştir** *(ux_host_class_asix_activate)*</span><span class="sxs-lookup"><span data-stu-id="c7285-262">**Host Class Asix Activate** *(ux_host_class_asix_activate)*</span></span> |
| ![Ana makine sınıfı ASIX devre dışı simgesi](./media/user-guide/usbx-events/image78.png)    | <span data-ttu-id="c7285-264">**Ana bilgisayar sınıfı aaltı devre dışı** *(ux_host_class_asix_deactivate)*</span><span class="sxs-lookup"><span data-stu-id="c7285-264">**Host Class Asix Deactivate** *(ux_host_class_asix_deactivate)*</span></span> |
| ![Ana bilgisayar sınıfı Aaltıkesme bildirimi simgesi](./media/user-guide/usbx-events/image79.png)    | <span data-ttu-id="c7285-266">**Ana bilgisayar sınıfı asix kesme bildirimi** *(ux_host_class_asix_interrupt_notification)*</span><span class="sxs-lookup"><span data-stu-id="c7285-266">**Host Class Asix Interrupt Notification** *(ux_host_class_asix_interrupt_notification)*</span></span> |
| ![Ana bilgisayar sınıfı Aaltıoku simgesi](./media/user-guide/usbx-events/image80.png)    | <span data-ttu-id="c7285-268">**Ana bilgisayar sınıfı Aaltıokuma** *(ux_host_class_asix_read)*</span><span class="sxs-lookup"><span data-stu-id="c7285-268">**Host Class Asix Read** *(ux_host_class_asix_read)*</span></span> |
| ![Ana bilgisayar sınıfı Aaltıyaz simgesi](./media/user-guide/usbx-events/image81.png)    | <span data-ttu-id="c7285-270">**Ana bilgisayar sınıfı Aaltıyaz** *(ux_host_class_asix_write)*</span><span class="sxs-lookup"><span data-stu-id="c7285-270">**Host Class Asix Write** *(ux_host_class_asix_write)*</span></span> |
| ![Konak sınıfı ses etkinleştirme simgesi](./media/user-guide/usbx-events/image82.png)    | <span data-ttu-id="c7285-272">**Konak sınıfı ses etkinleştirme** *(ux_host_class_audio_activate)*</span><span class="sxs-lookup"><span data-stu-id="c7285-272">**Host Class Audio Activate** *(ux_host_class_audio_activate)*</span></span> |
| ![Konak sınıfı ses denetimi değeri Al simgesi](./media/user-guide/usbx-events/image83.png)    | <span data-ttu-id="c7285-274">**Konak sınıfı ses denetimi değeri Get** *(ux_host_class_audio_control_value_get)*</span><span class="sxs-lookup"><span data-stu-id="c7285-274">**Host Class Audio Control Value Get** *(ux_host_class_audio_control_value_get)*</span></span> |
| ![Konak sınıfı ses denetimi değer kümesi simgesi](./media/user-guide/usbx-events/image84.png)    | <span data-ttu-id="c7285-276">**Konak sınıfı ses denetimi değer kümesi** *(ux_host_class_audio_control_value_set)*</span><span class="sxs-lookup"><span data-stu-id="c7285-276">**Host Class Audio Control Value Set** *(ux_host_class_audio_control_value_set)*</span></span> |
| ![Konak sınıfı ses devre dışı bırakma simgesi](./media/user-guide/usbx-events/image85.png)    | <span data-ttu-id="c7285-278">**Konak sınıfı ses devre dışı bırakma** *(ux_host_class_audio_deactivate)*</span><span class="sxs-lookup"><span data-stu-id="c7285-278">**Host Class Audio Deactivate** *(ux_host_class_audio_deactivate)*</span></span> |
| ![Konak sınıfı ses okuma simgesi](./media/user-guide/usbx-events/image86.png)    | <span data-ttu-id="c7285-280">**Ana bilgisayar sınıfı ses okuma** *(ux_host_class_audio_read)*</span><span class="sxs-lookup"><span data-stu-id="c7285-280">**Host Class Audio Read** *(ux_host_class_audio_read)*</span></span> |
| ![Konak sınıfı ses akışı örneklemesi alma simgesi](./media/user-guide/usbx-events/image87.png)    | <span data-ttu-id="c7285-282">**Konak sınıfı ses akışı örneklemesi alma** *(ux_host_class_audio_streaming_sampling_get)*</span><span class="sxs-lookup"><span data-stu-id="c7285-282">**Host Class Audio Streaming Sampling Get** *(ux_host_class_audio_streaming_sampling_get)*</span></span> |
| ![Konak sınıfı ses akışı örnekleme kümesi simgesi](./media/user-guide/usbx-events/image88.png)    | <span data-ttu-id="c7285-284">**Konak sınıfı ses akışı örnekleme kümesi** *(ux_host_class_audio_streaming_sampling_set)*</span><span class="sxs-lookup"><span data-stu-id="c7285-284">**Host Class Audio Streaming Sampling Set** *(ux_host_class_audio_streaming_sampling_set)*</span></span> |
| ![Konak sınıfı ses yazma simgesi](./media/user-guide/usbx-events/image89.png)    | <span data-ttu-id="c7285-286">**Ana bilgisayar sınıfı ses yazma** *(ux_host_class_audio_write)*</span><span class="sxs-lookup"><span data-stu-id="c7285-286">**Host Class Audio Write** *(ux_host_class_audio_write)*</span></span> |
| ![Ana bilgisayar sınıfı C D C A C M etkinleştirme simgesi](./media/user-guide/usbx-events/image90.png)    | <span data-ttu-id="c7285-288">**Ana bilgisayar sınıfı CDC ACM Activate** *(ux_host_class_cdc_acm_activate)*</span><span class="sxs-lookup"><span data-stu-id="c7285-288">**Host Class Cdc Acm Activate** *(ux_host_class_cdc_acm_activate)*</span></span> |
| ![Ana bilgisayar sınıfı C D C A C M devre dışı bırakma simgesi](./media/user-guide/usbx-events/image91.png)    | <span data-ttu-id="c7285-290">**Ana bilgisayar sınıfı CDC ACM Deactivate** *(ux_host_class_cdc_acm_deactivate)*</span><span class="sxs-lookup"><span data-stu-id="c7285-290">**Host Class Cdc Acm Deactivate** *(ux_host_class_cdc_acm_deactivate)*</span></span> |
| ![Ana bilgisayar sınıfı C D C bir C M ı O C T ı kanal simgesi](./media/user-guide/usbx-events/image92.png)    | <span data-ttu-id="c7285-292">**Ana bilgisayar sınıfı CDC ACM IOCTL-kanal** *(ux_host_class_cdc_acm_ioctl_abort_in_pipe)*</span><span class="sxs-lookup"><span data-stu-id="c7285-292">**Host Class Cdc Acm Ioctl Abort In Pipe** *(ux_host_class_cdc_acm_ioctl_abort_in_pipe)*</span></span> |
| ![Ana bilgisayar sınıfı C D C A C M ı u C T L I](./media/user-guide/usbx-events/image93.png)    | <span data-ttu-id="c7285-294">**Ana bilgisayar sınıfı CDC ACM IOCTL Iptal kanalı** *(ux_host_class_cdc_acm_ioctl_abort_out_pipe)*</span><span class="sxs-lookup"><span data-stu-id="c7285-294">**Host Class Cdc Acm Ioctl Abort Out Pipe** *(ux_host_class_cdc_acm_ioctl_abort_out_pipe)*</span></span> |
| ![Ana bilgisayar sınıfı C D C A C M ı O C T I cihaz durum simgesi al](./media/user-guide/usbx-events/image94.png)    | <span data-ttu-id="c7285-296">**Ana bilgisayar sınıfı CDC ACM IOCTL cihaz durumunu Al** *(ux_host_class_cdc_acm_ioctl_get_device_status)*</span><span class="sxs-lookup"><span data-stu-id="c7285-296">**Host Class Cdc Acm Ioctl Get Device Status** *(ux_host_class_cdc_acm_ioctl_get_device_status)*</span></span> |
| ![Ana bilgisayar sınıfı C D C A C M ı O C T m](./media/user-guide/usbx-events/image95.png)    | <span data-ttu-id="c7285-298">**Ana bilgisayar sınıfı CDC ACM IOCTL al satırı kodlama** *(ux_host_class_cdc_acm_ioctl_get_line_coding)*</span><span class="sxs-lookup"><span data-stu-id="c7285-298">**Host Class Cdc Acm Ioctl Get Line Coding** *(ux_host_class_cdc_acm_ioctl_get_line_coding)*</span></span> |
| ![Ana bilgisayar sınıfı C D C A C M ı O C T m](./media/user-guide/usbx-events/image96.png)    | <span data-ttu-id="c7285-300">**Ana bilgisayar sınıfı CDC ACM IOCTL bildirimi geri araması** *(ux_host_class_cdc_acm_ioctl_notification_callback)*</span><span class="sxs-lookup"><span data-stu-id="c7285-300">**Host Class Cdc Acm Ioctl Notification Callback** *(ux_host_class_cdc_acm_ioctl_notification_callback)*</span></span> |
| ![Ana bilgisayar sınıfı C D C c M I m C T ı gönder kesme simgesi](./media/user-guide/usbx-events/image97.png)    | <span data-ttu-id="c7285-302">**Ana bilgisayar sınıfı CDC ACM IOCTL gönderme sonu** *(ux_host_class_cdc_acm_ioctl_send_break)*</span><span class="sxs-lookup"><span data-stu-id="c7285-302">**Host Class Cdc Acm Ioctl Send Break** *(ux_host_class_cdc_acm_ioctl_send_break)*</span></span> |
| ![Ana bilgisayar sınıfı C D C c M ı O C T m](./media/user-guide/usbx-events/image98.png)    | <span data-ttu-id="c7285-304">**Ana bilgisayar sınıfı CDC ACM IOCTL kümesi satırı kodlama** *(ux_host_class_cdc_acm_ioctl_set_line_coding)*</span><span class="sxs-lookup"><span data-stu-id="c7285-304">**Host Class Cdc Acm Ioctl Set Line Coding** *(ux_host_class_cdc_acm_ioctl_set_line_coding)*</span></span> |
| ![Ana bilgisayar sınıfı C D C c M ı O C T ı](./media/user-guide/usbx-events/image99.png)    | <span data-ttu-id="c7285-306">**Ana bilgisayar sınıfı CDC ACM IOCTL kümesi satır durumu** *(ux_host_class_cdc_acm_ioctl_set_line_state)*</span><span class="sxs-lookup"><span data-stu-id="c7285-306">**Host Class Cdc Acm Ioctl Set Line State** *(ux_host_class_cdc_acm_ioctl_set_line_state)*</span></span> |
| ![Ana bilgisayar sınıfı C D C bir C M oku simgesi](./media/user-guide/usbx-events/image100.png)    | <span data-ttu-id="c7285-308">**Ana bilgisayar sınıfı CDC ACM okuma** *(ux_host_class_cdc_acm_read)*</span><span class="sxs-lookup"><span data-stu-id="c7285-308">**Host Class Cdc Acm Read** *(ux_host_class_cdc_acm_read)*</span></span> |
| ![Ana bilgisayar sınıfı C D C A C M alma başlangıç simgesi](./media/user-guide/usbx-events/image101.png)    | <span data-ttu-id="c7285-310">**Ana bilgisayar sınıfı CDC ACM alma başlangıcı** *(ux_host_class_cdc_acm_reception_start)*</span><span class="sxs-lookup"><span data-stu-id="c7285-310">**Host Class Cdc Acm Reception Start** *(ux_host_class_cdc_acm_reception_start)*</span></span> |
| ![Ana bilgisayar sınıfı C D C bir C M alımı durdur simgesi](./media/user-guide/usbx-events/image102.png)    | <span data-ttu-id="c7285-312">**Ana bilgisayar sınıfı CDC ACM alımı durdur** *(ux_host_class_cdc_acm_reception_stop)*</span><span class="sxs-lookup"><span data-stu-id="c7285-312">**Host Class Cdc Acm Reception Stop** *(ux_host_class_cdc_acm_reception_stop)*</span></span> |
| ![Ana bilgisayar sınıfı C D C c M yazma simgesi](./media/user-guide/usbx-events/image103.png)    | <span data-ttu-id="c7285-314">**Ana bilgisayar sınıfı CDC ACM yazma** *(ux_host_class_cdc_acm_write)*</span><span class="sxs-lookup"><span data-stu-id="c7285-314">**Host Class Cdc Acm Write** *(ux_host_class_cdc_acm_write)*</span></span> |
| ![Host Class Dpump etkinleştir simgesi](./media/user-guide/usbx-events/image104.png)    | <span data-ttu-id="c7285-316">**Konak sınıfı Dpump etkinleştir** *(ux_host_class_dpump_activate)*</span><span class="sxs-lookup"><span data-stu-id="c7285-316">**Host Class Dpump Activate** *(ux_host_class_dpump_activate)*</span></span> |
| ![Konak sınıfı Dpump etkinliğini kaldırma simgesi](./media/user-guide/usbx-events/image105.png)    | <span data-ttu-id="c7285-318">**Ana sınıf Dpump devre dışı bırakma** *(ux_host_class_dpump_deactivate)*</span><span class="sxs-lookup"><span data-stu-id="c7285-318">**Host Class Dpump Deactivate** *(ux_host_class_dpump_deactivate)*</span></span> |
| ![Konak sınıfı Dpump oku simgesi](./media/user-guide/usbx-events/image106.png)    | <span data-ttu-id="c7285-320">**Ana bilgisayar sınıfı Dpump okuma** *(ux_host_class_dpump_read)*</span><span class="sxs-lookup"><span data-stu-id="c7285-320">**Host Class Dpump Read** *(ux_host_class_dpump_read)*</span></span> |
| ![Ana sınıf Dpump yazma simgesi](./media/user-guide/usbx-events/image107.png)    | <span data-ttu-id="c7285-322">**Ana bilgisayar sınıfı Dpump yazma** *(ux_host_class_dpump_write)*</span><span class="sxs-lookup"><span data-stu-id="c7285-322">**Host Class Dpump Write** *(ux_host_class_dpump_write)*</span></span> |
| ![Konak sınıfı HID etkinleştirme simgesi](./media/user-guide/usbx-events/image108.png)    | <span data-ttu-id="c7285-324">**Host Class HID etkinleştir** *(ux_host_class_hid_activate)*</span><span class="sxs-lookup"><span data-stu-id="c7285-324">**Host Class Hid Activate** *(ux_host_class_hid_activate)*</span></span> |
| ![Konak sınıfı HID Istemci kaydı simgesi](./media/user-guide/usbx-events/image109.png)    | <span data-ttu-id="c7285-326">**Konak sınıfı HID Istemci kaydı** *(ux_host_class_hid_client_register)*</span><span class="sxs-lookup"><span data-stu-id="c7285-326">**Host Class Hid Client Register** *(ux_host_class_hid_client_register)*</span></span> |
| ![Konak sınıfı HID devre dışı bırakma simgesi](./media/user-guide/usbx-events/image110.png)    | <span data-ttu-id="c7285-328">**Konak sınıfı HID etkinliğini kaldırma** *(ux_host_class_hid_deactivate)*</span><span class="sxs-lookup"><span data-stu-id="c7285-328">**Host Class Hid Deactivate** *(ux_host_class_hid_deactivate)*</span></span> |
| ![Konak sınıfı HID boşta al al simgesi](./media/user-guide/usbx-events/image111.png)    | <span data-ttu-id="c7285-330">**Ana bilgisayar sınıfı HID boşta al** *(ux_host_class_hid_idle_get)*</span><span class="sxs-lookup"><span data-stu-id="c7285-330">**Host Class Hid Idle Get** *(ux_host_class_hid_idle_get)*</span></span> |
| ![Konak sınıfı HID boşta kümesi simgesi](./media/user-guide/usbx-events/image112.png)    | <span data-ttu-id="c7285-332">**Ana bilgisayar sınıfı HID boşta kümesi** *(ux_host_class_hid_idle_set)*</span><span class="sxs-lookup"><span data-stu-id="c7285-332">**Host Class Hid Idle Set** *(ux_host_class_hid_idle_set)*</span></span> |
| ![Host Class HID Klavye etkinleştirme simgesi](./media/user-guide/usbx-events/image113.png)    | <span data-ttu-id="c7285-334">**Host Class HID Klavye etkinleştir** *(ux_host_class_hid_keyboard_activate)*</span><span class="sxs-lookup"><span data-stu-id="c7285-334">**Host Class Hid Keyboard Activate** *(ux_host_class_hid_keyboard_activate)*</span></span> |
| ![Host Class HID Klavye devre dışı simgesi](./media/user-guide/usbx-events/image114.png)    | <span data-ttu-id="c7285-336">**Host Class HID Klavye devre dışı bırakma** *(ux_host_class_hid_keyboard_deactivate)*</span><span class="sxs-lookup"><span data-stu-id="c7285-336">**Host Class Hid Keyboard Deactivate** *(ux_host_class_hid_keyboard_deactivate)*</span></span> |
| ![Host Class HID fare etkinleştirme simgesi](./media/user-guide/usbx-events/image115.png)    | <span data-ttu-id="c7285-338">**Host Class HID fare etkinleştir** *(ux_host_class_hid_mouse_activate)*</span><span class="sxs-lookup"><span data-stu-id="c7285-338">**Host Class Hid Mouse Activate** *(ux_host_class_hid_mouse_activate)*</span></span> |
| ![Konak sınıfı HID fare devre dışı simgesi](./media/user-guide/usbx-events/image116.png)    | <span data-ttu-id="c7285-340">**Host Class HID fare devre dışı bırakma** *(ux_host_class_hid_mouse_deactivate)*</span><span class="sxs-lookup"><span data-stu-id="c7285-340">**Host Class Hid Mouse Deactivate** *(ux_host_class_hid_mouse_deactivate)*</span></span> |
| ![Konak sınıfı HID uzaktan denetim etkinleştirme simgesi](./media/user-guide/usbx-events/image117.png)    | <span data-ttu-id="c7285-342">**Konak sınıfı HID uzaktan denetim etkinleştirme** *(ux_host_class_hid_remote_control_activate)*</span><span class="sxs-lookup"><span data-stu-id="c7285-342">**Host Class Hid Remote Control Activate** *(ux_host_class_hid_remote_control_activate)*</span></span> |
| ![Konak sınıfı HID uzaktan denetim devre dışı simgesi](./media/user-guide/usbx-events/image118.png)    | <span data-ttu-id="c7285-344">**Konak sınıfı HID uzaktan denetim devre dışı** *(ux_host_class_hid_remote_control_deactivate)*</span><span class="sxs-lookup"><span data-stu-id="c7285-344">**Host Class Hid Remote Control Deactivate** *(ux_host_class_hid_remote_control_deactivate)*</span></span> |
| ![Konak sınıfı HID raporu al simgesi](./media/user-guide/usbx-events/image119.png)    | <span data-ttu-id="c7285-346">**Konak sınıfı HID raporu Get** *(ux_host_class_hid_report_get)*</span><span class="sxs-lookup"><span data-stu-id="c7285-346">**Host Class Hid Report Get** *(ux_host_class_hid_report_get)*</span></span> |
| ![Konak sınıfı HID rapor kümesi simgesi](./media/user-guide/usbx-events/image120.png)    | <span data-ttu-id="c7285-348">**Konak sınıfı HID rapor kümesi** *(ux_host_class_hid_report_set)*</span><span class="sxs-lookup"><span data-stu-id="c7285-348">**Host Class Hid Report Set** *(ux_host_class_hid_report_set)*</span></span> |
| ![Konak sınıfı hub etkinleştirme simgesi](./media/user-guide/usbx-events/image121.png)    | <span data-ttu-id="c7285-350">**Konak sınıfı hub 'ı etkinleştir** *(ux_host_class_hub_activate)*</span><span class="sxs-lookup"><span data-stu-id="c7285-350">**Host Class Hub Activate** *(ux_host_class_hub_activate)*</span></span> |
| ![Host Class hub değişikliği algılama simgesi](./media/user-guide/usbx-events/image122.png)    | <span data-ttu-id="c7285-352">**Ana bilgisayar sınıf hub değişikliği algılaması** *(ux_host_class_hub_change_detect)*</span><span class="sxs-lookup"><span data-stu-id="c7285-352">**Host Class Hub Change Detect** *(ux_host_class_hub_change_detect)*</span></span> |
| ![\* Konak sınıfı hub 'ı devre dışı bırakma simgesi](./media/user-guide/usbx-events/image123.png)    | <span data-ttu-id="c7285-354">**Konak sınıfı hub 'ı devre dışı bırakma** *(ux_host_class_hub_deactivate)*</span><span class="sxs-lookup"><span data-stu-id="c7285-354">**Host Class Hub Deactivate** *(ux_host_class_hub_deactivate)*</span></span> |
| ![Konak sınıf hub 'ı bağlantı noktası değişiklik bağlantı Işlemi simgesi](./media/user-guide/usbx-events/image124.png)    | <span data-ttu-id="c7285-356">**Konak sınıf hub 'ı bağlantı noktası değiştirme bağlantı işlemi** *(ux_host_class_hub_port_change_connection_process)*</span><span class="sxs-lookup"><span data-stu-id="c7285-356">**Host Class Hub Port Change Connection Process** *(ux_host_class_hub_port_change_connection_process)*</span></span> |
| ![Konak sınıfı hub bağlantı noktası değişikliği etkinleştirme Işlemi simgesi](./media/user-guide/usbx-events/image125.png)    | <span data-ttu-id="c7285-358">**Host Class hub bağlantı noktası değişikliği etkinleştirme işlemi** *(ux_host_class_hub_port_change_enable_process)*</span><span class="sxs-lookup"><span data-stu-id="c7285-358">**Host Class Hub Port Change Enable Process** *(ux_host_class_hub_port_change_enable_process)*</span></span> |
| ![Ana sınıf hub 'ı bağlantı noktası geçerli Işlem simgesi değişikliği](./media/user-guide/usbx-events/image126.png)    | <span data-ttu-id="c7285-360">Geçerli Işlem *(ux_host_class_hub_port_change_over_current_process)* **üzerinde ana bilgisayar sınıfı hub bağlantı noktası değişikliği**</span><span class="sxs-lookup"><span data-stu-id="c7285-360">**Host Class Hub Port Change Over Current Process** *(ux_host_class_hub_port_change_over_current_process)*</span></span> |
| ![Konak sınıf hub 'ı bağlantı noktası değişiklik sıfırlama Işlemi simgesi](./media/user-guide/usbx-events/image127.png)    | <span data-ttu-id="c7285-362">**Konak sınıf hub 'ı bağlantı noktası değişiklik sıfırlama işlemi** *(ux_host_class_hub_port_change_reset_process)*</span><span class="sxs-lookup"><span data-stu-id="c7285-362">**Host Class Hub Port Change Reset Process** *(ux_host_class_hub_port_change_reset_process)*</span></span> |
| ![Konak sınıf hub 'ı bağlantı noktası değiştirme Işlemi askıya alma simgesi](./media/user-guide/usbx-events/image128.png)    | <span data-ttu-id="c7285-364">**Host Class hub bağlantı noktası değiştirme askıya alma işlemi** *(ux_host_class_hub_port_change_suspend_process)*</span><span class="sxs-lookup"><span data-stu-id="c7285-364">**Host Class Hub Port Change Suspend Process** *(ux_host_class_hub_port_change_suspend_process)*</span></span> |
| ![Konak sınıfı Pima etkinleştirme simgesi](./media/user-guide/usbx-events/image129.png)    | <span data-ttu-id="c7285-366">**Konak sınıfı Pima etkinleştir** *(ux_host_class_prima_activate)*</span><span class="sxs-lookup"><span data-stu-id="c7285-366">**Host Class Pima Activate** *(ux_host_class_prima_activate)*</span></span> |
| ![Konak sınıfı Pima devre dışı bırakma simgesi](./media/user-guide/usbx-events/image130.png)    | <span data-ttu-id="c7285-368">**Konak sınıfı Pima devre dışı bırakma** *(ux_host_class_pima_deactivate)*</span><span class="sxs-lookup"><span data-stu-id="c7285-368">**Host Class Pima Deactivate** *(ux_host_class_pima_deactivate)*</span></span> |
| ![Konak sınıfı Pima cihaz bilgileri al simgesi](./media/user-guide/usbx-events/image131.png)    | <span data-ttu-id="c7285-370">**Konak sınıfı Pima cihaz bilgileri Get** *(ux_host_class_pima_device_info_get)*</span><span class="sxs-lookup"><span data-stu-id="c7285-370">**Host Class Pima Device Info Get** *(ux_host_class_pima_device_info_get)*</span></span> |
| ![Konak sınıfı Pima cihazı sıfırlama simgesi](./media/user-guide/usbx-events/image132.png)    | <span data-ttu-id="c7285-372">**Konak sınıfı Pima cihazı sıfırlama** *(ux_host_class_pima_device_reset)*</span><span class="sxs-lookup"><span data-stu-id="c7285-372">**Host Class Pima Device Reset** *(ux_host_class_pima_device_reset)*</span></span> |
| ![Konak sınıfı Pima bildirimi simgesi](./media/user-guide/usbx-events/image133.png)    | <span data-ttu-id="c7285-374">**Konak sınıfı Pima bildirimi** *(ux_host_class_pima_notification)*</span><span class="sxs-lookup"><span data-stu-id="c7285-374">**Host Class Pima Notification** *(ux_host_class_pima_notification)*</span></span> |
| ![Konak sınıfı Pima sayısı nesneleri Al simgesi](./media/user-guide/usbx-events/image134.png)    | <span data-ttu-id="c7285-376">**Konak sınıfı Pima sayısı nesneleri Al** *(ux_host_class_pima_num_objects_get)*</span><span class="sxs-lookup"><span data-stu-id="c7285-376">**Host Class Pima Number Objects Get** *(ux_host_class_pima_num_objects_get)*</span></span> |
| ![Ana sınıf Pima nesnesi kapatma simgesi](./media/user-guide/usbx-events/image135.png)    | <span data-ttu-id="c7285-378">**Konak sınıfı Pima nesnesi kapat** *(ux_host_class_pima_object_close)*</span><span class="sxs-lookup"><span data-stu-id="c7285-378">**Host Class Pima Object Close** *(ux_host_class_pima_object_close)*</span></span> |
| ![Konak sınıfı Pima nesnesi kopyalama simgesi](./media/user-guide/usbx-events/image136.png)    | <span data-ttu-id="c7285-380">**Konak sınıfı Pima nesne kopyası** *(ux_host_class_pima_object_copy)*</span><span class="sxs-lookup"><span data-stu-id="c7285-380">**Host Class Pima Object Copy** *(ux_host_class_pima_object_copy)*</span></span> |
| ![Konak sınıfı Pima nesnesi silme simgesi](./media/user-guide/usbx-events/image137.png)    | <span data-ttu-id="c7285-382">**Konak sınıfı Pima nesnesi silme** *(ux_host_class_pima_object_delete)*</span><span class="sxs-lookup"><span data-stu-id="c7285-382">**Host Class Pima Object Delete** *(ux_host_class_pima_object_delete)*</span></span> |
| ![Ana sınıf Pima nesnesi Al simgesi](./media/user-guide/usbx-events/image138.png)    | <span data-ttu-id="c7285-384">**Konak sınıfı Pima nesnesi Get** *(ux_host_class_pima_object_get)*</span><span class="sxs-lookup"><span data-stu-id="c7285-384">**Host Class Pima Object Get** *(ux_host_class_pima_object_get)*</span></span> |
| ![Konak sınıfı Pima nesnesi bilgileri al simgesi](./media/user-guide/usbx-events/image139.png)    | <span data-ttu-id="c7285-386">**Konak sınıfı Pima nesnesi bilgileri al** *(ux_host_class_pima_object_info_get)*</span><span class="sxs-lookup"><span data-stu-id="c7285-386">**Host Class Pima Object Info Get** *(ux_host_class_pima_object_info_get)*</span></span> |
| ![Konak sınıfı Pima nesne bilgileri gönderme simgesi](./media/user-guide/usbx-events/image140.png)    | <span data-ttu-id="c7285-388">**Konak sınıfı Pima nesne bilgileri gönderme** *(ux_host_class_pima_object_info_send)*</span><span class="sxs-lookup"><span data-stu-id="c7285-388">**Host Class Pima Object Info Send** *(ux_host_class_pima_object_info_send)*</span></span> |
| ![Konak sınıfı Pima nesnesi taşıma simgesi](./media/user-guide/usbx-events/image141.png)    | <span data-ttu-id="c7285-390">**Konak sınıfı Pima nesnesi taşıma** *(ux_host_class_pima_object_move)*</span><span class="sxs-lookup"><span data-stu-id="c7285-390">**Host Class Pima Object Move** *(ux_host_class_pima_object_move)*</span></span> |
| ![Ana sınıf Pima nesnesi Gönder simgesi](./media/user-guide/usbx-events/image142.png)    | <span data-ttu-id="c7285-392">**Konak sınıfı Pima nesnesi gönderme** *(ux_host_class_pima_object_send)*</span><span class="sxs-lookup"><span data-stu-id="c7285-392">**Host Class Pima Object Send** *(ux_host_class_pima_object_send)*</span></span> |
| ![Konak sınıfı Pima nesne aktarımı Iptali simgesi](./media/user-guide/usbx-events/image143.png)    | <span data-ttu-id="c7285-394">**Konak sınıfı Pima nesnesi aktarımı iptali** *(ux_host_class_object_transfer_abort)*</span><span class="sxs-lookup"><span data-stu-id="c7285-394">**Host Class Pima Object Transfer Abort** *(ux_host_class_object_transfer_abort)*</span></span> |
| ![Konak sınıfı Pima oku simgesi](./media/user-guide/usbx-events/image144.png)    | <span data-ttu-id="c7285-396">**Ana bilgisayar sınıfı Pima okuma** *(ux_host_class_pima_read)*</span><span class="sxs-lookup"><span data-stu-id="c7285-396">**Host Class Pima Read** *(ux_host_class_pima_read)*</span></span> |
| ![Konak sınıfı Pima Isteği Iptal simgesi](./media/user-guide/usbx-events/image145.png)    | <span data-ttu-id="c7285-398">**Konak sınıfı Pima Isteği iptali** *(ux_host_class_pima_request_cancel)*</span><span class="sxs-lookup"><span data-stu-id="c7285-398">**Host Class Pima Request Cancel** *(ux_host_class_pima_request_cancel)*</span></span> |
| ![Ana sınıf Pima oturumu kapatma simgesi](./media/user-guide/usbx-events/image146.png)    | <span data-ttu-id="c7285-400">**Ana bilgisayar sınıfı Pima oturumu kapalı** *(ux_host_class_pima_session_close)*</span><span class="sxs-lookup"><span data-stu-id="c7285-400">**Host Class Pima Session Close** *(ux_host_class_pima_session_close)*</span></span> |
| ![Konak sınıfı Pima oturumu açma simgesi](./media/user-guide/usbx-events/image147.png)    | <span data-ttu-id="c7285-402">**Konak sınıfı Pima oturumu açık** *(ux_host_class_pima_session_open)*</span><span class="sxs-lookup"><span data-stu-id="c7285-402">**Host Class Pima Session Open** *(ux_host_class_pima_session_open)*</span></span> |
| ![Konak sınıfı Pima depolama kimlikleri al simgesi](./media/user-guide/usbx-events/image148.png)    | <span data-ttu-id="c7285-404">**Konak sınıfı Pima depolama kimlikleri al** *(ux_host_class_pima_storage_ids_get)*</span><span class="sxs-lookup"><span data-stu-id="c7285-404">**Host Class Pima Storage Ids Get** *(ux_host_class_pima_storage_ids_get)*</span></span> |
| ![Konak sınıfı Pima depolama bilgileri al simgesi](./media/user-guide/usbx-events/image149.png)    | <span data-ttu-id="c7285-406">**Konak sınıfı Pima depolama bilgileri Get** *(ux_host_class_pima_storage_info_get)*</span><span class="sxs-lookup"><span data-stu-id="c7285-406">**Host Class Pima Storage Info Get** *(ux_host_class_pima_storage_info_get)*</span></span> |
| ![Konak sınıfı Pima Thumb al simgesi](./media/user-guide/usbx-events/image150.png)    | <span data-ttu-id="c7285-408">**Konak sınıfı Pima Parmak Izi al** *(ux_host_class_pima_thumb_get)*</span><span class="sxs-lookup"><span data-stu-id="c7285-408">**Host Class Pima Thumb Get** *(ux_host_class_pima_thumb_get)*</span></span> |
| ![Konak sınıfı Pima yazma simgesi](./media/user-guide/usbx-events/image151.png)    | <span data-ttu-id="c7285-410">**Konak sınıfı Pima yazma** *(ux_host_class_pima_write)*</span><span class="sxs-lookup"><span data-stu-id="c7285-410">**Host Class Pima Write** *(ux_host_class_pima_write)*</span></span> |
| ![Konak sınıfı yazıcı etkinleştirme simgesi](./media/user-guide/usbx-events/image152.png)    | <span data-ttu-id="c7285-412">**Konak sınıfı yazıcısını etkinleştir** *(ux_host_class_printer_activate)*</span><span class="sxs-lookup"><span data-stu-id="c7285-412">**Host Class Printer Activate** *(ux_host_class_printer_activate)*</span></span> |
| ![Konak sınıfı yazıcı devre dışı simgesi](./media/user-guide/usbx-events/image153.png)    | <span data-ttu-id="c7285-414">**Konak sınıfı yazıcısını devre dışı bırak** *(ux_host_class_printer_deactivate)*</span><span class="sxs-lookup"><span data-stu-id="c7285-414">**Host Class Printer Deactivate** *(ux_host_class_printer_deactivate)*</span></span> |
| ![Konak sınıfı yazıcı adı Al simgesi](./media/user-guide/usbx-events/image154.png)    | <span data-ttu-id="c7285-416">**Ana bilgisayar sınıfı yazıcı adı Get** *(ux_host_class_printer_name_get)*</span><span class="sxs-lookup"><span data-stu-id="c7285-416">**Host Class Printer Name Get** *(ux_host_class_printer_name_get)*</span></span> |
| ![Ana bilgisayar sınıfı yazıcı okuma simgesi](./media/user-guide/usbx-events/image155.png)    |  <span data-ttu-id="c7285-418">**Ana bilgisayar sınıfı yazıcı okuma** *(ux_host_class_printer_read)*</span><span class="sxs-lookup"><span data-stu-id="c7285-418">**Host Class Printer Read** *(ux_host_class_printer_read)*</span></span> |
| ![Konak sınıfı yazıcı geçici sıfırlama simgesi](./media/user-guide/usbx-events/image156.png)    | <span data-ttu-id="c7285-420">**Konak sınıfı yazıcı yazılımdan sıfırlama** *(ux_host_class_printer_soft_reset)*</span><span class="sxs-lookup"><span data-stu-id="c7285-420">**Host Class Printer Soft Reset** *(ux_host_class_printer_soft_reset)*</span></span> |
| ![Konak sınıfı yazıcı durumu Al simgesi](./media/user-guide/usbx-events/image157.png)    | <span data-ttu-id="c7285-422">**Konak sınıfı yazıcı durumu Al** *(ux_host_class_printer_status_get)*</span><span class="sxs-lookup"><span data-stu-id="c7285-422">**Host Class Printer Status Get** *(ux_host_class_printer_status_get)*</span></span> |
| ![Konak sınıfı yazıcı yazma simgesi](./media/user-guide/usbx-events/image158.png)    | <span data-ttu-id="c7285-424">**Ana bilgisayar sınıfı yazıcı yazma** *(ux_host_class_printer_write)*</span><span class="sxs-lookup"><span data-stu-id="c7285-424">**Host Class Printer Write** *(ux_host_class_printer_write)*</span></span> |
| ![Konak sınıfı Prolific etkinleştirme simgesi](./media/user-guide/usbx-events/image159.png)    | <span data-ttu-id="c7285-426">**Konak sınıfı Prolific etkinleştir** *(ux_host_class_prolific_activate)*</span><span class="sxs-lookup"><span data-stu-id="c7285-426">**Host Class Prolific Activate** *(ux_host_class_prolific_activate)*</span></span> |
| ![Konak sınıfı Prolific devre dışı bırakma simgesi](./media/user-guide/usbx-events/image160.png)    | <span data-ttu-id="c7285-428">**Konak sınıfı Prolific etkinliğini kaldır** *(ux_host_class_prolific_deactivate)*</span><span class="sxs-lookup"><span data-stu-id="c7285-428">**Host Class Prolific Deactivate** *(ux_host_class_prolific_deactivate)*</span></span> |
| ![Kanal simgesinde ana bilgisayar sınıfı proo C T L durdur](./media/user-guide/usbx-events/image161.png)    | <span data-ttu-id="c7285-430">**Ana bilgisayar sınıfı Işlem kanalında IOCTL iptali** *(ux_host_class_prolific_ioctl_abort_in_pipe)*</span><span class="sxs-lookup"><span data-stu-id="c7285-430">**Host Class Prolific Ioctl Abort In Pipe** *(ux_host_class_prolific_ioctl_abort_in_pipe)*</span></span> |
| ![Ana bilgisayar sınıfı proo C T L m ı Durdur kanal simgesi](./media/user-guide/usbx-events/image162.png)    | <span data-ttu-id="c7285-432">**Ana bilgisayar sınıfı Prolific IOCTL Iptal kanalı** *(ux_host_class_prolific_ioctl_abort_out_pipe)*</span><span class="sxs-lookup"><span data-stu-id="c7285-432">**Host Class Prolific Ioctl Abort Out Pipe** *(ux_host_class_prolific_ioctl_abort_out_pipe)*</span></span> |
| ![Konak sınıfı Prolific g T C T L bir cihaz durumu simgesi al](./media/user-guide/usbx-events/image163.png)    | <span data-ttu-id="c7285-434">**Konak sınıfı Prolific IOCTL cihaz durumunu Al** *(ux_host_class_prolific_ioctl_get_device_status)*</span><span class="sxs-lookup"><span data-stu-id="c7285-434">**Host Class Prolific Ioctl Get Device Status** *(ux_host_class_prolific_ioctl_get_device_status)*</span></span> |
| ![Konak sınıfı Prolific ı T C T L Class for satırı kodlama simgesi](./media/user-guide/usbx-events/image164.png)    | <span data-ttu-id="c7285-436">**Konak sınıfı Prolific IOCTL al satır kodlama** *(ux_host_class_prolific_ioctl_get_line_coding)*</span><span class="sxs-lookup"><span data-stu-id="c7285-436">**Host Class Prolific Ioctl Get Line Coding** *(ux_host_class_prolific_ioctl_get_line_coding)*</span></span> |
| ![Ana bilgisayar sınıfı Prolific T I do u simgesi](./media/user-guide/usbx-events/image165.png)    | <span data-ttu-id="c7285-438">**Ana makine sınıfı, IOCTL Temizleme** *(ux_host_class_prolific_ioctl_purge)*</span><span class="sxs-lookup"><span data-stu-id="c7285-438">**Host Class Prolific Ioctl Purge** *(ux_host_class_prolific_ioctl_purge)*</span></span> |
| ![Konak sınıfı Prolific ı T C T m rapor cihaz durumu değiştirme simgesi](./media/user-guide/usbx-events/image166.png)    | <span data-ttu-id="c7285-440">**Konak sınıfı Prolific IOCTL rapor cihaz durumu değişikliği** *(ux_host_class_prolific_ioctl_report_device_status_change)*</span><span class="sxs-lookup"><span data-stu-id="c7285-440">**Host Class Prolific Ioctl Report Device Status Change** *(ux_host_class_prolific_ioctl_report_device_status_change)*</span></span> |
| ![Konak sınıfı Prolific ı T C T L gönderme sonu simgesi](./media/user-guide/usbx-events/image167.png)    | <span data-ttu-id="c7285-442">**Ana bilgisayar sınıfı, IOCTL gönderme sonu** *(ux_host_class_prolific_ioctl_send_break)*</span><span class="sxs-lookup"><span data-stu-id="c7285-442">**Host Class Prolific Ioctl Send Break** *(ux_host_class_prolific_ioctl_send_break)*</span></span> |
| ![Konak sınıfı Prolific ı T C T L Class for satırı kodlama simgesi](./media/user-guide/usbx-events/image168.png)    | <span data-ttu-id="c7285-444">**Konak sınıfı Prolific IOCTL kümesi satırı kodlama** *(ux_host_class_prolific_ioctl_set_line_coding)*</span><span class="sxs-lookup"><span data-stu-id="c7285-444">**Host Class Prolific Ioctl Set Line Coding** *(ux_host_class_prolific_ioctl_set_line_coding)*</span></span> |
| ![Konak sınıfı Prolific ı T C T L s satır durumu simgesi](./media/user-guide/usbx-events/image169.png)    | <span data-ttu-id="c7285-446">**Konak sınıfı Prolific IOCTL kümesi satır durumu** *(ux_host_class_prolific_ioctl_set_line_state)*</span><span class="sxs-lookup"><span data-stu-id="c7285-446">**Host Class Prolific Ioctl Set Line State** *(ux_host_class_prolific_ioctl_set_line_state)*</span></span> |
| ![Konak sınıfı Prolific okuma simgesi](./media/user-guide/usbx-events/image170.png)    | <span data-ttu-id="c7285-448">**Ana bilgisayar sınıfı, okuma** *(ux_host_class_prolific_read)*</span><span class="sxs-lookup"><span data-stu-id="c7285-448">**Host Class Prolific Read** *(ux_host_class_prolific_read)*</span></span> |
| ![Konak sınıfı Prolific alma başlangıç simgesi](./media/user-guide/usbx-events/image171.png)    | <span data-ttu-id="c7285-450">**Ana bilgisayar sınıfı Prolific alma başlangıcı** *(ux_host_class_prolific_reception_start)*</span><span class="sxs-lookup"><span data-stu-id="c7285-450">**Host Class Prolific Reception Start** *(ux_host_class_prolific_reception_start)*</span></span> |
| ![Konak sınıfı Prolific alımı durdurma simgesi](./media/user-guide/usbx-events/image172.png)    | <span data-ttu-id="c7285-452">**Konak sınıfı Prolific alma durdurma** *(ux_host_class_prolific_reception_stop)*</span><span class="sxs-lookup"><span data-stu-id="c7285-452">**Host Class Prolific Reception Stop** *(ux_host_class_prolific_reception_stop)*</span></span> |
| ![Ana makine sınıfı başlangıç yazma simgesi](./media/user-guide/usbx-events/image173.png)    | <span data-ttu-id="c7285-454">**Ana bilgisayar sınıfı başlangıç yazma** *(ux_host_class_prolific_write)*</span><span class="sxs-lookup"><span data-stu-id="c7285-454">**Host Class Prolific Write** *(ux_host_class_prolific_write)*</span></span> |
| ![Konak sınıfı depolama etkinleştirme simgesi](./media/user-guide/usbx-events/image174.png)    | <span data-ttu-id="c7285-456">**Konak sınıfı depolama etkinleştir** *(ux_host_class_storage_activate)*</span><span class="sxs-lookup"><span data-stu-id="c7285-456">**Host Class Storage Activate** *(ux_host_class_storage_activate)*</span></span> |
| ![Konak sınıfı depolamayı devre dışı bırakma simgesi](./media/user-guide/usbx-events/image175.png)    | <span data-ttu-id="c7285-458">**Konak sınıfı depolamayı devre dışı bırakma** (*ux_host_class_storage_deactivate)*</span><span class="sxs-lookup"><span data-stu-id="c7285-458">**Host Class Storage Deactivate** (*ux_host_class_storage_deactivate)*</span></span> |
| ![Konak sınıfı depolama medyası kapasitesi al simgesi](./media/user-guide/usbx-events/image176.png)    | <span data-ttu-id="c7285-460">**Konak sınıfı depolama medyası kapasitesi al** *(ux_host_class_storage_media_capacity_get)*</span><span class="sxs-lookup"><span data-stu-id="c7285-460">**Host Class Storage Media Capacity Get** *(ux_host_class_storage_media_capacity_get)*</span></span> |
| ![Konak sınıfı depolama medya biçimi kapasitesi al simgesi](./media/user-guide/usbx-events/image177.png)    | <span data-ttu-id="c7285-462">**Konak sınıfı depolama medya biçimi kapasitesi al** *(ux_host_class_storage_media_format_capacity_get)*</span><span class="sxs-lookup"><span data-stu-id="c7285-462">**Host Class Storage Media Format Capacity Get** *(ux_host_class_storage_media_format_capacity_get)*</span></span> |
| ![Konak sınıfı depolama medyası bağlama simgesi](./media/user-guide/usbx-events/image178.png)    | <span data-ttu-id="c7285-464">**Konak sınıfı depolama medyası bağlama** (ux_host_class_storage_media_mount) \*</span><span class="sxs-lookup"><span data-stu-id="c7285-464">**Host Class Storage Media Mount** (ux_host_class_storage_media_mount)\*</span></span> |
| ![Konak sınıfı depolama medyası açık simgesi](./media/user-guide/usbx-events/image179.png)    | <span data-ttu-id="c7285-466">**Konak sınıfı depolama medyası açık** *(ux_host_class_storage_media_open)*</span><span class="sxs-lookup"><span data-stu-id="c7285-466">**Host Class Storage Media Open** *(ux_host_class_storage_media_open)*</span></span> |
| ![Konak sınıfı depolama medyası okuma simgesi](./media/user-guide/usbx-events/image180.png)    | <span data-ttu-id="c7285-468">**Konak sınıfı depolama medyası okuma** *(ux_host_class_storage_media_read)*</span><span class="sxs-lookup"><span data-stu-id="c7285-468">**Host Class Storage Media Read** *(ux_host_class_storage_media_read)*</span></span> |
| ![Konak sınıfı depolama medyası yazma simgesi](./media/user-guide/usbx-events/image181.png)    | <span data-ttu-id="c7285-470">**Konak sınıfı depolama medyası yazma** *(ux_host_class_storage_media_write)*</span><span class="sxs-lookup"><span data-stu-id="c7285-470">**Host Class Storage Media Write** *(ux_host_class_storage_media_write)*</span></span> |
| ![Konak sınıfı depolama Isteği algılama simgesi](./media/user-guide/usbx-events/image182.png)    | <span data-ttu-id="c7285-472">**Konak sınıfı depolama Isteği algılama** *(ux_host_class_storage_request_sense)*</span><span class="sxs-lookup"><span data-stu-id="c7285-472">**Host Class Storage Request Sense** *(ux_host_class_storage_request_sense)*</span></span> |
| ![Konak sınıfı depolama başlatma durdurma simgesi](./media/user-guide/usbx-events/image183.png)    | <span data-ttu-id="c7285-474">**Konak sınıfı depolama başlatma durdurma** *(ux_host_class_storage_start_stop)*</span><span class="sxs-lookup"><span data-stu-id="c7285-474">**Host Class Storage Start Stop** *(ux_host_class_storage_start_stop)*</span></span> |
| ![Konak sınıfı depolama birimi için Ready test simgesi](./media/user-guide/usbx-events/image184.png)    | <span data-ttu-id="c7285-476">**Konak sınıfı depolama birimi Için hazırlanma testi** *(ux_host_class_storage_activate)*</span><span class="sxs-lookup"><span data-stu-id="c7285-476">**Host Class Storage Unit Ready Test** *(ux_host_class_storage_activate)*</span></span> |
| ![Konak yığını sınıf örneği oluşturma simgesi](./media/user-guide/usbx-events/image185.png)    | <span data-ttu-id="c7285-478">**Konak yığını sınıf örneği oluşturma** *(ux_host_stack_class_instance_create)*</span><span class="sxs-lookup"><span data-stu-id="c7285-478">**Host Stack Class Instance Create** *(ux_host_stack_class_instance_create)*</span></span> |
| ![Konak yığını sınıf örneği yok etme simgesi](./media/user-guide/usbx-events/image186.png)    | <span data-ttu-id="c7285-480">**Konak yığını sınıf örneği yok etme** *(ux_host_stack_class_instance_destroy)*</span><span class="sxs-lookup"><span data-stu-id="c7285-480">**Host Stack Class Instance Destroy** *(ux_host_stack_class_instance_destroy)*</span></span> |
| ![Konak yığını yapılandırması silme simgesi](./media/user-guide/usbx-events/image187.png)    | <span data-ttu-id="c7285-482">**Konak yığını yapılandırması silme** *(ux_host_stack_configuration_delete)*</span><span class="sxs-lookup"><span data-stu-id="c7285-482">**Host Stack Configuration Delete** *(ux_host_stack_configuration_delete)*</span></span> |
| ![Konak yığını yapılandırması sıralama simgesi](./media/user-guide/usbx-events/image188.png)    | <span data-ttu-id="c7285-484">**Konak yığını yapılandırması numaralandırması** *(ux_host_stack_configuration_enumerate)*</span><span class="sxs-lookup"><span data-stu-id="c7285-484">**Host Stack Configuration Enumerate** *(ux_host_stack_configuration_enumerate)*</span></span> |
| ![Konak yığını yapılandırma örneği oluşturma simgesi](./media/user-guide/usbx-events/image189.png)    | <span data-ttu-id="c7285-486">**Konak yığını yapılandırma örneği oluşturma** *(ux_host_stack_configuration_instance_create)*</span><span class="sxs-lookup"><span data-stu-id="c7285-486">**Host Stack Configuration Instance Create** *(ux_host_stack_configuration_instance_create)*</span></span> |
| ![Konak yığını yapılandırma örneği silme simgesi](./media/user-guide/usbx-events/image190.png)    | <span data-ttu-id="c7285-488">**Konak yığını yapılandırma örneği silme** *(ux_host_stack_configuration_instance_delete)*</span><span class="sxs-lookup"><span data-stu-id="c7285-488">**Host Stack Configuration Instance Delete** *(ux_host_stack_configuration_instance_delete)*</span></span> |
| ![Konak yığını yapılandırma kümesi simgesi](./media/user-guide/usbx-events/image191.png)    | <span data-ttu-id="c7285-490">**Konak yığını yapılandırma kümesi** *(ux_host_stack_configuration_set)*</span><span class="sxs-lookup"><span data-stu-id="c7285-490">**Host Stack Configuration Set** *(ux_host_stack_configuration_set)*</span></span> |
| ![Konak yığını cihaz adresi kümesi simgesi](./media/user-guide/usbx-events/image192.png)    | <span data-ttu-id="c7285-492">**Konak yığını cihaz adresi kümesi** *(ux_host_stack_device_set)*</span><span class="sxs-lookup"><span data-stu-id="c7285-492">**Host Stack Device Address Set** *(ux_host_stack_device_set)*</span></span> |
| ![Konak yığını cihaz yapılandırması Get simgesi](./media/user-guide/usbx-events/image193.png)    | <span data-ttu-id="c7285-494">**Konak yığını cihaz yapılandırması Get** *(ux_host_stack_device_configuration_get)*</span><span class="sxs-lookup"><span data-stu-id="c7285-494">**Host Stack Device Configuration Get** *(ux_host_stack_device_configuration_get)*</span></span> |
| ![Konak yığını cihaz yapılandırması seçim simgesi](./media/user-guide/usbx-events/image194.png)    | <span data-ttu-id="c7285-496">**Konak yığını cihaz yapılandırması seçme** *(ux_host_stack_device_configuration_select)*</span><span class="sxs-lookup"><span data-stu-id="c7285-496">**Host Stack Device Configuration Select** *(ux_host_stack_device_configuration_select)*</span></span> |
| ![Konak yığını cihaz tanımlayıcısı okuma simgesi](./media/user-guide/usbx-events/image195.png)    | <span data-ttu-id="c7285-498">**Konak yığını cihaz tanımlayıcısı okuma** *(ux_host_stack_device_descriptor_read)*</span><span class="sxs-lookup"><span data-stu-id="c7285-498">**Host Stack Device Descriptor Read** *(ux_host_stack_device_descriptor_read)*</span></span> |
| ![Konak yığını cihazının al simgesi](./media/user-guide/usbx-events/image196.png)    | <span data-ttu-id="c7285-500">**Konak yığını cihazının Get** (ux_host_stack_device_get)</span><span class="sxs-lookup"><span data-stu-id="c7285-500">**Host Stack Device Get** (ux_host_stack_device_get)</span></span> |
| ![Konak yığını cihaz kaldırma simgesi](./media/user-guide/usbx-events/image197.png)    | <span data-ttu-id="c7285-502">**Konak yığını cihazını kaldır** (ux_host_stack_device_get)</span><span class="sxs-lookup"><span data-stu-id="c7285-502">**Host Stack Device Remove** (ux_host_stack_device_get)</span></span> |
| ![Ana bilgisayar yığını cihaz kaynağı boş simgesi](./media/user-guide/usbx-events/image198.png)    | <span data-ttu-id="c7285-504">**Ana bilgisayar yığını cihaz kaynağı boş** (ux_host_stack_device_resource_free)</span><span class="sxs-lookup"><span data-stu-id="c7285-504">**Host Stack Device Resource Free** (ux_host_stack_device_resource_free)</span></span> |
| ![Konak yığını uç noktası örneği oluşturma simgesi](./media/user-guide/usbx-events/image199.png)    | <span data-ttu-id="c7285-506">**Konak yığını uç noktası örneği oluşturma** (ux_host_stack_endpoint_instance_create)</span><span class="sxs-lookup"><span data-stu-id="c7285-506">**Host Stack Endpoint Instance Create** (ux_host_stack_endpoint_instance_create)</span></span> |
| ![Konak yığın uç noktası örneği silme simgesi](./media/user-guide/usbx-events/image200.png)    | <span data-ttu-id="c7285-508">**Konak yığını uç noktası örneği silme** (ux_host_stack_endpoint_instance_delete)</span><span class="sxs-lookup"><span data-stu-id="c7285-508">**Host Stack Endpoint Instance Delete** (ux_host_stack_endpoint_instance_delete)</span></span> |
| ![Konak yığını uç noktası sıfırlama simgesi](./media/user-guide/usbx-events/image201.png)    | <span data-ttu-id="c7285-510">**Konak yığını uç noktası sıfırlama** (ux_host_stack_endpoint_reset)</span><span class="sxs-lookup"><span data-stu-id="c7285-510">**Host Stack Endpoint Reset** (ux_host_stack_endpoint_reset)</span></span> |
| ![Konak yığını uç noktası aktarımı Iptal simgesi](./media/user-guide/usbx-events/image202.png)    | <span data-ttu-id="c7285-512">**Konak yığını uç noktası aktarımı iptal** (ux_host_stack_endpoint_transfer_abort)</span><span class="sxs-lookup"><span data-stu-id="c7285-512">**Host Stack Endpoint Transfer Abort** (ux_host_stack_endpoint_transfer_abort)</span></span> |
| ![Konak yığını konak denetleyicisi kayıt simgesi](./media/user-guide/usbx-events/image203.png)    | <span data-ttu-id="c7285-514">**Konak yığını konak denetleyicisi kaydı** *(ux_host_stack_hcd_register)*</span><span class="sxs-lookup"><span data-stu-id="c7285-514">**Host Stack Host Controller Register** *(ux_host_stack_hcd_register)*</span></span> |
| ![Konak yığını başlatma simgesi](./media/user-guide/usbx-events/image204.png)    | <span data-ttu-id="c7285-516">**Konak yığını başlatma** *(ux_host_stack_initialize)*</span><span class="sxs-lookup"><span data-stu-id="c7285-516">**Host Stack Initialize** *(ux_host_stack_initialize)*</span></span> |
| ![Konak yığını arabirimi uç noktası al simgesi](./media/user-guide/usbx-events/image205.png)    | <span data-ttu-id="c7285-518">**Konak yığını arabirim uç noktası al** *(ux_host_stack_interface_endpoint_get)*</span><span class="sxs-lookup"><span data-stu-id="c7285-518">**Host Stack Interface Endpoint Get** *(ux_host_stack_interface_endpoint_get)*</span></span> |
| ![Konak yığını arabirim örneği oluşturma simgesi](./media/user-guide/usbx-events/image206.png)    | <span data-ttu-id="c7285-520">**Konak yığını arabirim örneği oluşturma** *(ux_host_stack_interface_instance_create)*</span><span class="sxs-lookup"><span data-stu-id="c7285-520">**Host Stack Interface Instance Create** *(ux_host_stack_interface_instance_create)*</span></span> |
| ![Konak yığını arabirim örneği silme simgesi](./media/user-guide/usbx-events/image207.png)    | <span data-ttu-id="c7285-522">**Konak yığını arabirim örneği silme** *(ux_host_stack_interface_instance_delete)*</span><span class="sxs-lookup"><span data-stu-id="c7285-522">**Host Stack Interface Instance Delete** *(ux_host_stack_interface_instance_delete)*</span></span> |
| ![Konak yığını arabirim kümesi simgesi](./media/user-guide/usbx-events/image208.png)    | <span data-ttu-id="c7285-524">**Konak yığını arabirim kümesi** *(ux_host_stack_interface_set)*</span><span class="sxs-lookup"><span data-stu-id="c7285-524">**Host Stack Interface Set** *(ux_host_stack_interface_set)*</span></span> |
| ![Konak yığın arabirimi ayarı seçme simgesi](./media/user-guide/usbx-events/image209.png)    | <span data-ttu-id="c7285-526">**Konak yığını arabirim ayarı seçimi** *(ux_host_stack_interface_setting_select)*</span><span class="sxs-lookup"><span data-stu-id="c7285-526">**Host Stack Interface Setting Select** *(ux_host_stack_interface_setting_select)*</span></span> |
| ![Konak yığını yeni yapılandırma Oluştur simgesi](./media/user-guide/usbx-events/image210.png)    | <span data-ttu-id="c7285-528">**Ana bilgisayar yığını yeni yapılandırma oluşturma** *(ux_host_stack_new_configuration_create)*</span><span class="sxs-lookup"><span data-stu-id="c7285-528">**Host Stack New Configuration Create** *(ux_host_stack_new_configuration_create)*</span></span> |
| ![Konak yığını yeni cihaz Oluştur simgesi](./media/user-guide/usbx-events/image211.png)    | <span data-ttu-id="c7285-530">**Ana bilgisayar yığını yeni cihaz oluşturma** *(ux_host_stack_new_device_create)*</span><span class="sxs-lookup"><span data-stu-id="c7285-530">**Host Stack New Device Create** *(ux_host_stack_new_device_create)*</span></span> |
| ![Ana bilgisayar yığını yeni uç nokta Oluştur simgesi](./media/user-guide/usbx-events/image212.png)    | <span data-ttu-id="c7285-532">**Ana bilgisayar yığını yeni uç nokta oluşturma** *(ux_host_stack_new_endpoint_create)*</span><span class="sxs-lookup"><span data-stu-id="c7285-532">**Host Stack New Endpoint Create** *(ux_host_stack_new_endpoint_create)*</span></span> |
| ![Konak yığını kök hub 'ı değiştirme Işlemi simgesi](./media/user-guide/usbx-events/image213.png)    | <span data-ttu-id="c7285-534">**Konak yığını kök hub 'ı değişiklik işlemi** *(ux_host_stack_rh_change_process)*</span><span class="sxs-lookup"><span data-stu-id="c7285-534">**Host Stack Root Hub Change Process** *(ux_host_stack_rh_change_process)*</span></span> |
| ![Konak yığını kök hub cihazı ayıklama simgesi](./media/user-guide/usbx-events/image214.png)    | <span data-ttu-id="c7285-536">**Konak yığını kök hub cihazı ayıklama** *(ux_host_stack_rh_device_extraction)*</span><span class="sxs-lookup"><span data-stu-id="c7285-536">**Host Stack Root Hub Device Extraction** *(ux_host_stack_rh_device_extraction)*</span></span> |
| ![Konak yığını kök hub cihazı ekleme simgesi](./media/user-guide/usbx-events/image215.png)    | <span data-ttu-id="c7285-538">**Konak yığını kök hub cihazı ekleme** *(ux_host_stack_rh_device_insertion)*</span><span class="sxs-lookup"><span data-stu-id="c7285-538">**Host Stack Root Hub Device Insertion** *(ux_host_stack_rh_device_insertion)*</span></span> |
| ![Konak yığını aktarım Isteği simgesi](./media/user-guide/usbx-events/image216.png)    | <span data-ttu-id="c7285-540">**Ana bilgisayar yığını aktarım isteği** *(ux_host_stack_transfer_request)*</span><span class="sxs-lookup"><span data-stu-id="c7285-540">**Host Stack Transfer Request** *(ux_host_stack_transfer_request)*</span></span> |
| ![Konak yığını aktarım Isteği Iptali simgesi](./media/user-guide/usbx-events/image217.png)    | <span data-ttu-id="c7285-542">**Ana bilgisayar yığını aktarım Isteği iptali** *(ux_host_stack_transfer_request_abort)*</span><span class="sxs-lookup"><span data-stu-id="c7285-542">**Host Stack Transfer Request Abort** *(ux_host_stack_transfer_request_abort)*</span></span> |
| ![U S B X hata simgesi](./media/user-guide/usbx-events/image218.png)    | <span data-ttu-id="c7285-544">**USBX hatası** *(ux_error)*</span><span class="sxs-lookup"><span data-stu-id="c7285-544">**USBX Error** *(ux_error)*</span></span> |

## <a name="event-descriptions"></a><span data-ttu-id="c7285-545">Olay Açıklamaları</span><span class="sxs-lookup"><span data-stu-id="c7285-545">Event Descriptions</span></span>

<span data-ttu-id="c7285-546">Aşağıdaki sayfalar, USBX Izleme olaylarını anlatmaktadır.</span><span class="sxs-lookup"><span data-stu-id="c7285-546">The following pages describe the USBX Trace Events.</span></span>

### <a name="device-class-cdc-activate"></a><span data-ttu-id="c7285-547">Aygıt sınıfı CDC etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="c7285-547">Device Class Cdc Activate</span></span> 

#### <a name="ux_device_class_cdc_activate"></a><span data-ttu-id="c7285-548">ux_device_class_cdc_activate</span><span class="sxs-lookup"><span data-stu-id="c7285-548">ux_device_class_cdc_activate</span></span>

<span data-ttu-id="c7285-549">**Simge** ![ Cihaz sınıfı C D C etkinleştir simgesi](./media/user-guide/usbx-events/image1.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-549">**Icon** ![Device Class C D C Activate icon](./media/user-guide/usbx-events/image1.png)</span></span>

<span data-ttu-id="c7285-550">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-550">**Description**</span></span>

<span data-ttu-id="c7285-551">Bu olay bir USBX cihaz sınıfı CDC Activate olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-551">This event represents a USBX Device Class Cdc Activate Event.</span></span>

<span data-ttu-id="c7285-552">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-552">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-553">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-553">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-554">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-554">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-555">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-555">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-556">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-556">Info Field 4: Not used.</span></span>

### <a name="device-class-cdc-deactivate"></a><span data-ttu-id="c7285-557">Device Class CDC devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="c7285-557">Device Class Cdc Deactivate</span></span> 

#### <a name="ux_device_class_cdc_deactivate"></a><span data-ttu-id="c7285-558">ux_device_class_cdc_deactivate</span><span class="sxs-lookup"><span data-stu-id="c7285-558">ux_device_class_cdc_deactivate</span></span>

<span data-ttu-id="c7285-559">**Simge** ![ Cihaz sınıfı C D C devre dışı bırakma simgesi](./media/user-guide/usbx-events/image2.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-559">**Icon** ![Device Class C D C Deactivate icon](./media/user-guide/usbx-events/image2.png)</span></span>

<span data-ttu-id="c7285-560">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-560">**Description**</span></span>

<span data-ttu-id="c7285-561">Bu olay, bir USBX cihaz sınıfını CDC devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="c7285-561">This event represents a USBX Device Class Cdc Deactivate.</span></span>

<span data-ttu-id="c7285-562">Bilgi alanları</span><span class="sxs-lookup"><span data-stu-id="c7285-562">Information Fields</span></span> 

- <span data-ttu-id="c7285-563">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-563">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-564">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-564">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-565">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-565">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-566">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-566">Info Field 4: Not used.</span></span>

### <a name="device-class-cdc-read"></a><span data-ttu-id="c7285-567">Aygıt sınıfı CDC okuma</span><span class="sxs-lookup"><span data-stu-id="c7285-567">Device Class Cdc Read</span></span> 

#### <a name="ux_device_class_cdc_read"></a><span data-ttu-id="c7285-568">ux_device_class_cdc_read</span><span class="sxs-lookup"><span data-stu-id="c7285-568">ux_device_class_cdc_read</span></span>

<span data-ttu-id="c7285-569">**Simge** ![ Cihaz sınıfı C D C okuma simgesi](./media/user-guide/usbx-events/image3.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-569">**Icon** ![Device Class C D C Read icon](./media/user-guide/usbx-events/image3.png)</span></span>

<span data-ttu-id="c7285-570">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-570">**Description**</span></span>

<span data-ttu-id="c7285-571">Bu olay bir USBX cihaz sınıfı CDC okuma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-571">This event represents a USBX Device Class Cdc Read Event.</span></span>

<span data-ttu-id="c7285-572">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-572">**Information Fields**</span></span>

- <span data-ttu-id="c7285-573">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-573">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-574">Bilgi alanı 2: veri işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c7285-574">Info Field 2: Data pointer.</span></span>
- <span data-ttu-id="c7285-575">Bilgi alanı 3: Istenen uzunluk.</span><span class="sxs-lookup"><span data-stu-id="c7285-575">Info Field 3: Requested length.</span></span>
- <span data-ttu-id="c7285-576">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-576">Info Field 4: Not used.</span></span>

### <a name="device-class-cdc-write"></a><span data-ttu-id="c7285-577">Aygıt sınıfı CDC yazma</span><span class="sxs-lookup"><span data-stu-id="c7285-577">Device Class Cdc Write</span></span> 

#### <a name="ux_device_class_cdc_write"></a><span data-ttu-id="c7285-578">ux_device_class_cdc_write</span><span class="sxs-lookup"><span data-stu-id="c7285-578">ux_device_class_cdc_write</span></span>

<span data-ttu-id="c7285-579">**Simge** ![ Cihaz sınıfı C D C yazma simgesi](./media/user-guide/usbx-events/image4.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-579">**Icon** ![Device Class C D C Write icon](./media/user-guide/usbx-events/image4.png)</span></span>

<span data-ttu-id="c7285-580">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-580">**Description**</span></span>

<span data-ttu-id="c7285-581">Bu olay bir USBX cihaz sınıfı CDC yazma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-581">This event represents a USBX Device Class Cdc Write Event.</span></span>

<span data-ttu-id="c7285-582">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-582">**Information Fields**</span></span>

- <span data-ttu-id="c7285-583">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-583">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-584">Bilgi alanı 2: veri işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c7285-584">Info Field 2: Data pointer.</span></span>
- <span data-ttu-id="c7285-585">Bilgi alanı 3: Istenen uzunluk.</span><span class="sxs-lookup"><span data-stu-id="c7285-585">Info Field 3: Requested length.</span></span>
- <span data-ttu-id="c7285-586">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-586">Info Field 4: Not used.</span></span>

### <a name="device-class-dpump-activate"></a><span data-ttu-id="c7285-587">Cihaz sınıfı Dpump etkinleştir</span><span class="sxs-lookup"><span data-stu-id="c7285-587">Device Class Dpump Activate</span></span> 

#### <a name="ux_device_class_dpump_activate"></a><span data-ttu-id="c7285-588">ux_device_class_dpump_activate</span><span class="sxs-lookup"><span data-stu-id="c7285-588">ux_device_class_dpump_activate</span></span>

<span data-ttu-id="c7285-589">**Simge** ![ Device Class Dpump etkinleştir simgesi](./media/user-guide/usbx-events/image5.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-589">**Icon** ![Device Class Dpump Activate icon](./media/user-guide/usbx-events/image5.png)</span></span>

<span data-ttu-id="c7285-590">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-590">**Description**</span></span>

<span data-ttu-id="c7285-591">Bu olay bir USBX cihaz sınıfı Dpump Activate olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-591">This event represents a USBX Device Class Dpump Activate Event.</span></span>

<span data-ttu-id="c7285-592">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-592">**Information Fields**</span></span>

- <span data-ttu-id="c7285-593">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-593">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-594">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-594">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-595">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-595">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-596">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-596">Info Field 4: Not used.</span></span>

### <a name="device-class-dpump-deactivate"></a><span data-ttu-id="c7285-597">Cihaz sınıfı Dpump devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="c7285-597">Device Class Dpump Deactivate</span></span> 

#### <a name="ux_device_class_dpump_deactivate"></a><span data-ttu-id="c7285-598">ux_device_class_dpump_deactivate</span><span class="sxs-lookup"><span data-stu-id="c7285-598">ux_device_class_dpump_deactivate</span></span>

<span data-ttu-id="c7285-599">**Simge** ![ Cihaz sınıfı Dpump devre dışı bırakma simgesi](./media/user-guide/usbx-events/image6.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-599">**Icon** ![Device Class Dpump Deactivate icon](./media/user-guide/usbx-events/image6.png)</span></span>

<span data-ttu-id="c7285-600">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-600">**Description**</span></span>

<span data-ttu-id="c7285-601">Bu olay bir USBX cihaz sınıfı Dpump Deactivate olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-601">This event represents a USBX Device Class Dpump Deactivate Event.</span></span>

<span data-ttu-id="c7285-602">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-602">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-603">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-603">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-604">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-604">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-605">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-605">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-606">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-606">Info Field 4: Not used.</span></span>

### <a name="device-class-dpump-read"></a><span data-ttu-id="c7285-607">Cihaz sınıfı Dpump okuma</span><span class="sxs-lookup"><span data-stu-id="c7285-607">Device Class Dpump Read</span></span> 

#### <a name="ux_device_class_dpump_read"></a><span data-ttu-id="c7285-608">ux_device_class_dpump_read</span><span class="sxs-lookup"><span data-stu-id="c7285-608">ux_device_class_dpump_read</span></span>

<span data-ttu-id="c7285-609">**Simge** ![ Cihaz sınıfı Dpump okuma simgesi](./media/user-guide/usbx-events/image7.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-609">**Icon** ![Device Class Dpump Read icon](./media/user-guide/usbx-events/image7.png)</span></span>

<span data-ttu-id="c7285-610">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-610">**Description**</span></span>

<span data-ttu-id="c7285-611">Bu olay, bir USBX cihaz sınıfı Dpump okuma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-611">This event represents a USBX Device Class Dpump Read Event.</span></span>

<span data-ttu-id="c7285-612">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-612">**Information Fields**</span></span>

- <span data-ttu-id="c7285-613">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-613">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-614">Bilgi alanı 2: arabellek.</span><span class="sxs-lookup"><span data-stu-id="c7285-614">Info Field 2: Buffer.</span></span>
- <span data-ttu-id="c7285-615">Bilgi alanı 3: Istenen uzunluk.</span><span class="sxs-lookup"><span data-stu-id="c7285-615">Info Field 3: Requested length.</span></span>
- <span data-ttu-id="c7285-616">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-616">Info Field 4: Not used.</span></span>

### <a name="device-class-dpump-write"></a><span data-ttu-id="c7285-617">Cihaz sınıfı Dpump yazma</span><span class="sxs-lookup"><span data-stu-id="c7285-617">Device Class Dpump Write</span></span> 

#### <a name="ux_device_class_dpump_write"></a><span data-ttu-id="c7285-618">ux_device_class_dpump_write</span><span class="sxs-lookup"><span data-stu-id="c7285-618">ux_device_class_dpump_write</span></span>

<span data-ttu-id="c7285-619">**Simge** ![ Device Class Dpump yazma simgesi](./media/user-guide/usbx-events/image8.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-619">**Icon** ![Device Class Dpump Write icon](./media/user-guide/usbx-events/image8.png)</span></span>

<span data-ttu-id="c7285-620">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-620">**Description**</span></span>

<span data-ttu-id="c7285-621">Bu olay, bir USBX cihaz sınıfı Dpump yazma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-621">This event represents a USBX Device Class Dpump Write Event.</span></span>

<span data-ttu-id="c7285-622">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-622">**Information Fields**</span></span>

- <span data-ttu-id="c7285-623">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-623">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-624">Bilgi alanı 2: veri işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c7285-624">Info Field 2: Data pointer.</span></span>
- <span data-ttu-id="c7285-625">Bilgi alanı 3: Istenen uzunluk.</span><span class="sxs-lookup"><span data-stu-id="c7285-625">Info Field 3: Requested length.</span></span>
- <span data-ttu-id="c7285-626">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-626">Info Field 4: Not used.</span></span>

### <a name="device-class-hid-activate"></a><span data-ttu-id="c7285-627">Cihaz sınıfı HID etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="c7285-627">Device Class Hid Activate</span></span> 

#### <a name="ux_device_class_hid_activate"></a><span data-ttu-id="c7285-628">ux_device_class_hid_activate</span><span class="sxs-lookup"><span data-stu-id="c7285-628">ux_device_class_hid_activate</span></span>

<span data-ttu-id="c7285-629">**Simge** ![ Device Class HID etkinleştirme simgesi](./media/user-guide/usbx-events/image9.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-629">**Icon** ![Device Class Hid Activate icon](./media/user-guide/usbx-events/image9.png)</span></span>

<span data-ttu-id="c7285-630">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-630">**Description**</span></span>

<span data-ttu-id="c7285-631">Bu olay bir USBX Device Class HID Activate olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-631">This event represents a USBX Device Class Hid Activate Event.</span></span>

<span data-ttu-id="c7285-632">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-632">**Information Fields**</span></span>

- <span data-ttu-id="c7285-633">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-633">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-634">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-634">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-635">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-635">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-636">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-636">Info Field 4: Not used.</span></span>

### <a name="device-class-hid-deactivate"></a><span data-ttu-id="c7285-637">Cihaz sınıfı HID devre dışı</span><span class="sxs-lookup"><span data-stu-id="c7285-637">Device Class Hid Deactivate</span></span> 

#### <a name="ux_device_class_hid_deactivate"></a><span data-ttu-id="c7285-638">ux_device_class_hid_deactivate</span><span class="sxs-lookup"><span data-stu-id="c7285-638">ux_device_class_hid_deactivate</span></span>

<span data-ttu-id="c7285-639">**Simge** ![ Cihaz sınıfı HID devre dışı bırakma simgesi](./media/user-guide/usbx-events/image10.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-639">**Icon** ![Device Class Hid Deactivate icon](./media/user-guide/usbx-events/image10.png)</span></span>

<span data-ttu-id="c7285-640">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-640">**Description**</span></span>

<span data-ttu-id="c7285-641">Bu olay bir USBX cihaz sınıfı HID devre dışı bırakma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-641">This event represents a USBX Device Class Hid Deactivate Event.</span></span>

<span data-ttu-id="c7285-642">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-642">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-643">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-643">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-644">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-644">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-645">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-645">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-646">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-646">Info Field 4: Not used.</span></span>

### <a name="device-class-hid-descriptor-send"></a><span data-ttu-id="c7285-647">Cihaz sınıfı HID tanımlayıcısı gönderme</span><span class="sxs-lookup"><span data-stu-id="c7285-647">Device Class Hid Descriptor Send</span></span> 

#### <a name="ux_device_class_hid_descritpor_send"></a><span data-ttu-id="c7285-648">ux_device_class_hid_descritpor_send</span><span class="sxs-lookup"><span data-stu-id="c7285-648">ux_device_class_hid_descritpor_send</span></span>

<span data-ttu-id="c7285-649">**Simge** ![ Cihaz sınıfı HID tanımlayıcısı gönderme simgesi](./media/user-guide/usbx-events/image11.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-649">**Icon** ![Device Class Hid Descriptor Send icon](./media/user-guide/usbx-events/image11.png)</span></span>

<span data-ttu-id="c7285-650">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-650">**Description**</span></span>

<span data-ttu-id="c7285-651">Bu olay bir USBX cihaz sınıfı HID tanımlayıcısı gönderme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-651">This event represents a USBX Device Class Hid Descriptor Send Event.</span></span>

<span data-ttu-id="c7285-652">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-652">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-653">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-653">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-654">Bilgi alanı 2: tanımlayıcı türü.</span><span class="sxs-lookup"><span data-stu-id="c7285-654">Info Field 2: Descriptor type.</span></span>
- <span data-ttu-id="c7285-655">Bilgi alanı 3: Istek dizini.</span><span class="sxs-lookup"><span data-stu-id="c7285-655">Info Field 3: Request index.</span></span>
- <span data-ttu-id="c7285-656">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-656">Info Field 4: Not used.</span></span>

### <a name="device-class-hid-event-get"></a><span data-ttu-id="c7285-657">Cihaz sınıfı HID olayı Get</span><span class="sxs-lookup"><span data-stu-id="c7285-657">Device Class Hid Event Get</span></span> 

#### <a name="ux_device_class_hid_event_get"></a><span data-ttu-id="c7285-658">ux_device_class_hid_event_get</span><span class="sxs-lookup"><span data-stu-id="c7285-658">ux_device_class_hid_event_get</span></span>

<span data-ttu-id="c7285-659">**Simge** ![ Cihaz sınıfı HID olayı al simgesi](./media/user-guide/usbx-events/image12.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-659">**Icon** ![Device Class Hid Event Get icon](./media/user-guide/usbx-events/image12.png)</span></span>

<span data-ttu-id="c7285-660">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-660">**Description**</span></span>

<span data-ttu-id="c7285-661">Bu olay bir USBX cihaz sınıfı HID olay Get olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-661">This event represents a USBX Device Class Hid Event Get Event.</span></span>

<span data-ttu-id="c7285-662">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-662">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-663">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-663">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-664">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-664">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-665">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-665">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-666">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-666">Info Field 4: Not used.</span></span>

### <a name="device-class-hid-event-set"></a><span data-ttu-id="c7285-667">Cihaz sınıfı HID olay kümesi</span><span class="sxs-lookup"><span data-stu-id="c7285-667">Device Class Hid Event Set</span></span> 

#### <a name="ux_device_class_hid_event_set"></a><span data-ttu-id="c7285-668">ux_device_class_hid_event_set</span><span class="sxs-lookup"><span data-stu-id="c7285-668">ux_device_class_hid_event_set</span></span>

<span data-ttu-id="c7285-669">**Simge** ![ Cihaz sınıfı HID olay kümesi simgesi](./media/user-guide/usbx-events/image13.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-669">**Icon** ![Device Class Hid Event Set icon](./media/user-guide/usbx-events/image13.png)</span></span>

<span data-ttu-id="c7285-670">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-670">**Description**</span></span>

<span data-ttu-id="c7285-671">Bu olay bir USBX cihaz sınıfı HID olay kümesini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-671">This event represents a USBX Device Class Hid Event Set.</span></span>

<span data-ttu-id="c7285-672">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-672">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-673">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-673">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-674">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-674">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-675">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-675">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-676">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-676">Info Field 4: Not used.</span></span>

### <a name="device-class-hid-report-get"></a><span data-ttu-id="c7285-677">Cihaz sınıfı HID raporu al</span><span class="sxs-lookup"><span data-stu-id="c7285-677">Device Class Hid Report Get</span></span> 

#### <a name="ux_device_class_hid_report_get"></a><span data-ttu-id="c7285-678">ux_device_class_hid_report_get</span><span class="sxs-lookup"><span data-stu-id="c7285-678">ux_device_class_hid_report_get</span></span>

<span data-ttu-id="c7285-679">**Simge** ![ Cihaz sınıfı HID raporu al simgesi](./media/user-guide/usbx-events/image14.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-679">**Icon** ![Device Class Hid Report Get icon](./media/user-guide/usbx-events/image14.png)</span></span>

<span data-ttu-id="c7285-680">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-680">**Description**</span></span>

<span data-ttu-id="c7285-681">Bu olay bir USBX Device Class HID rapor Get olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-681">This event represents a USBX Device Class Hid Report Get Event.</span></span>

<span data-ttu-id="c7285-682">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-682">**Information Fields**</span></span>

- <span data-ttu-id="c7285-683">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-683">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-684">Bilgi alanı 2: tanımlayıcı türü.</span><span class="sxs-lookup"><span data-stu-id="c7285-684">Info Field 2: Descriptor type.</span></span>
- <span data-ttu-id="c7285-685">Bilgi alanı 3: Istek dizini.</span><span class="sxs-lookup"><span data-stu-id="c7285-685">Info Field 3: Request index.</span></span>
- <span data-ttu-id="c7285-686">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-686">Info Field 4: Not used.</span></span>

### <a name="device-class-hid-report-set"></a><span data-ttu-id="c7285-687">Cihaz sınıfı HID rapor kümesi</span><span class="sxs-lookup"><span data-stu-id="c7285-687">Device Class Hid Report Set</span></span> 

#### <a name="ux_device_class_hid_report_set"></a><span data-ttu-id="c7285-688">ux_device_class_hid_report_set</span><span class="sxs-lookup"><span data-stu-id="c7285-688">ux_device_class_hid_report_set</span></span>

<span data-ttu-id="c7285-689">**Simge** ![ Cihaz sınıfı HID rapor kümesi simgesi](./media/user-guide/usbx-events/image15.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-689">**Icon** ![Device Class Hid Report Set icon](./media/user-guide/usbx-events/image15.png)</span></span>

<span data-ttu-id="c7285-690">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-690">**Description**</span></span>

<span data-ttu-id="c7285-691">Bu olay bir USBX cihaz sınıfı HID rapor kümesi olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-691">This event represents a USBX Device Class Hid Report Set Event.</span></span>

<span data-ttu-id="c7285-692">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-692">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-693">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-693">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-694">Bilgi alanı 2: tanımlayıcı türü.</span><span class="sxs-lookup"><span data-stu-id="c7285-694">Info Field 2: Descriptor type.</span></span>
- <span data-ttu-id="c7285-695">Bilgi alanı 3: Istek dizini.</span><span class="sxs-lookup"><span data-stu-id="c7285-695">Info Field 3: Request index.</span></span>
- <span data-ttu-id="c7285-696">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-696">Info Field 4: Not used.</span></span>

### <a name="device-class-pima-activate"></a><span data-ttu-id="c7285-697">Cihaz sınıfı Pima etkinleştir</span><span class="sxs-lookup"><span data-stu-id="c7285-697">Device Class Pima Activate</span></span>

#### <a name="ux_device_class_pima_activate"></a><span data-ttu-id="c7285-698">ux_device_class_pima_activate</span><span class="sxs-lookup"><span data-stu-id="c7285-698">ux_device_class_pima_activate</span></span>

<span data-ttu-id="c7285-699">**Simge** ![ Cihaz sınıfı Pima etkinleştirme simgesi](./media/user-guide/usbx-events/image16.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-699">**Icon** ![Device Class Pima Activate icon](./media/user-guide/usbx-events/image16.png)</span></span>

<span data-ttu-id="c7285-700">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-700">**Description**</span></span>

<span data-ttu-id="c7285-701">Bu olay bir USBX Device Class Pima Activate olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-701">This event represents a USBX Device Class Pima Activate Event.</span></span>

<span data-ttu-id="c7285-702">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-702">**Information Fields**</span></span>

- <span data-ttu-id="c7285-703">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-703">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-704">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-704">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-705">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-705">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-706">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-706">Info Field 4: Not used.</span></span>

### <a name="device-class-pima-deactivate"></a><span data-ttu-id="c7285-707">Cihaz sınıfı Pima devre dışı</span><span class="sxs-lookup"><span data-stu-id="c7285-707">Device Class Pima Deactivate</span></span> 

#### <a name="ux_device_class_pima_deactivate"></a><span data-ttu-id="c7285-708">ux_device_class_pima_deactivate</span><span class="sxs-lookup"><span data-stu-id="c7285-708">ux_device_class_pima_deactivate</span></span>

<span data-ttu-id="c7285-709">**Simge** ![ Cihaz sınıfı Pima devre dışı bırakma simgesi](./media/user-guide/usbx-events/image17.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-709">**Icon** ![Device Class Pima Deactivate icon](./media/user-guide/usbx-events/image17.png)</span></span>

<span data-ttu-id="c7285-710">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-710">**Description**</span></span>

<span data-ttu-id="c7285-711">Bu olay bir USBX Device Class Pima etkinliğini kaldırma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-711">This event represents a USBX Device Class Pima Deactivate Event.</span></span>

<span data-ttu-id="c7285-712">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-712">**Information Fields**</span></span>

- <span data-ttu-id="c7285-713">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-713">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-714">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-714">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-715">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-715">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-716">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-716">Info Field 4: Not used.</span></span>

### <a name="device-class-pima-device-info-send"></a><span data-ttu-id="c7285-717">Cihaz sınıfı Pima cihaz bilgileri gönderme</span><span class="sxs-lookup"><span data-stu-id="c7285-717">Device Class Pima Device Info Send</span></span> 

#### <a name="ux_device_class_pima_device_info_send"></a><span data-ttu-id="c7285-718">ux_device_class_pima_device_info_send</span><span class="sxs-lookup"><span data-stu-id="c7285-718">ux_device_class_pima_device_info_send</span></span>

<span data-ttu-id="c7285-719">**Simge** ![ Cihaz sınıfı Pima cihaz bilgileri gönderme simgesi](./media/user-guide/usbx-events/image18.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-719">**Icon** ![Device Class Pima Device Info Send icon](./media/user-guide/usbx-events/image18.png)</span></span>

<span data-ttu-id="c7285-720">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-720">**Description**</span></span>

<span data-ttu-id="c7285-721">Bu olay bir USBX cihaz sınıfı Pima cihaz bilgileri gönderme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-721">This event represents a USBX Device Class Pima Device Info Send Event.</span></span>

<span data-ttu-id="c7285-722">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-722">**Information Fields**</span></span>

- <span data-ttu-id="c7285-723">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-723">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-724">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-724">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-725">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-725">Info Field 3: Not used.</span></span>

### <a name="device-class-pima-event-get"></a><span data-ttu-id="c7285-726">Cihaz sınıfı Pima olayı Get</span><span class="sxs-lookup"><span data-stu-id="c7285-726">Device Class Pima Event Get</span></span> 

#### <a name="ux_device_class_pima_event_get"></a><span data-ttu-id="c7285-727">ux_device_class_pima_event_get</span><span class="sxs-lookup"><span data-stu-id="c7285-727">ux_device_class_pima_event_get</span></span>

<span data-ttu-id="c7285-728">**Simge** ![ Device Class Pima olayı al simgesi](./media/user-guide/usbx-events/image19.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-728">**Icon** ![Device Class Pima Event Get icon](./media/user-guide/usbx-events/image19.png)</span></span>

<span data-ttu-id="c7285-729">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-729">**Description**</span></span>

<span data-ttu-id="c7285-730">Bu olay bir USBX Device Class Pima olayı Get olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-730">This event represents a USBX Device Class Pima Event Get Event.</span></span>

<span data-ttu-id="c7285-731">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-731">**Information Fields**</span></span>

- <span data-ttu-id="c7285-732">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-732">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-733">Bilgi alanı 2: Pima olayı.</span><span class="sxs-lookup"><span data-stu-id="c7285-733">Info Field 2: Pima event.</span></span>
- <span data-ttu-id="c7285-734">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-734">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-735">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-735">Info Field 4: Not used.</span></span>

### <a name="device-class-pima-event-set"></a><span data-ttu-id="c7285-736">Device Class Pima olay kümesi</span><span class="sxs-lookup"><span data-stu-id="c7285-736">Device Class Pima Event Set</span></span> 

#### <a name="ux_device_class_pima_event_set"></a><span data-ttu-id="c7285-737">ux_device_class_pima_event_set</span><span class="sxs-lookup"><span data-stu-id="c7285-737">ux_device_class_pima_event_set</span></span>

<span data-ttu-id="c7285-738">**Simge** ![ Cihaz sınıfı Pima olayı kümesi simgesi](./media/user-guide/usbx-events/image20.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-738">**Icon** ![Device Class Pima Event Set icon](./media/user-guide/usbx-events/image20.png)</span></span>

<span data-ttu-id="c7285-739">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-739">**Description**</span></span>

<span data-ttu-id="c7285-740">Bu olay bir USBX cihaz sınıfı Pima olay kümesi olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-740">This event represents a USBX Device Class Pima Event Set Event.</span></span>

<span data-ttu-id="c7285-741">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-741">**Information Fields**</span></span>

- <span data-ttu-id="c7285-742">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-742">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-743">Bilgi alanı 2: Pima olayı.</span><span class="sxs-lookup"><span data-stu-id="c7285-743">Info Field 2: Pima event.</span></span>
- <span data-ttu-id="c7285-744">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-744">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-745">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-745">Info Field 4: Not used.</span></span>

### <a name="device-class-pima-object-add"></a><span data-ttu-id="c7285-746">Cihaz sınıfı Pima nesnesi ekleme</span><span class="sxs-lookup"><span data-stu-id="c7285-746">Device Class Pima Object Add</span></span> 

#### <a name="ux_device_class_pima_object_add"></a><span data-ttu-id="c7285-747">ux_device_class_pima_object_add</span><span class="sxs-lookup"><span data-stu-id="c7285-747">ux_device_class_pima_object_add</span></span>

<span data-ttu-id="c7285-748">**Simge** ![ Cihaz sınıfı Pima nesnesi ekleme simgesi](./media/user-guide/usbx-events/image21.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-748">**Icon** ![Device Class Pima Object Add icon](./media/user-guide/usbx-events/image21.png)</span></span>

<span data-ttu-id="c7285-749">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-749">**Description**</span></span>

<span data-ttu-id="c7285-750">Bu olay bir USBX Device Class Pima nesnesi Add olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-750">This event represents a USBX Device Class Pima Object Add Event.</span></span>

<span data-ttu-id="c7285-751">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-751">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-752">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-752">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-753">Bilgi alanı 2: nesne tanıtıcısı.</span><span class="sxs-lookup"><span data-stu-id="c7285-753">Info Field 2: Object handle.</span></span>
- <span data-ttu-id="c7285-754">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-754">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-755">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-755">Info Field 4: Not used.</span></span>

### <a name="device-class-pima-object-data-get"></a><span data-ttu-id="c7285-756">Cihaz sınıfı Pima nesnesi veri al</span><span class="sxs-lookup"><span data-stu-id="c7285-756">Device Class Pima Object Data Get</span></span> 

#### <a name="ux_device_class_pima_object_data_get"></a><span data-ttu-id="c7285-757">ux_device_class_pima_object_data_get</span><span class="sxs-lookup"><span data-stu-id="c7285-757">ux_device_class_pima_object_data_get</span></span>

<span data-ttu-id="c7285-758">**Simge** ![ Aygıt sınıfı Pima nesnesi verileri al simgesi](./media/user-guide/usbx-events/image22.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-758">**Icon** ![Device Class Pima Object Data Get icon](./media/user-guide/usbx-events/image22.png)</span></span>

<span data-ttu-id="c7285-759">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-759">**Description**</span></span>

<span data-ttu-id="c7285-760">Bu olay bir USBX cihaz sınıfı Pima nesne verileri al olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-760">This event represents a USBX Device Class Pima Object Data Get Event.</span></span>

<span data-ttu-id="c7285-761">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-761">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-762">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-762">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-763">Bilgi alanı 2: nesne tanıtıcısı.</span><span class="sxs-lookup"><span data-stu-id="c7285-763">Info Field 2: Object handle.</span></span>
- <span data-ttu-id="c7285-764">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-764">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-765">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-765">Info Field 4: Not used.</span></span>

### <a name="device-class-pima-object-data-send"></a><span data-ttu-id="c7285-766">Cihaz sınıfı Pima nesnesi verileri gönderme</span><span class="sxs-lookup"><span data-stu-id="c7285-766">Device Class Pima Object Data Send</span></span> 

#### <a name="ux_device_class_pima_object_data_send"></a><span data-ttu-id="c7285-767">ux_device_class_pima_object_data_send</span><span class="sxs-lookup"><span data-stu-id="c7285-767">ux_device_class_pima_object_data_send</span></span>

<span data-ttu-id="c7285-768">**Simge** ![ Cihaz sınıfı Pima nesnesi verileri gönderme simgesi](./media/user-guide/usbx-events/image23.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-768">**Icon** ![Device Class Pima Object Data Send icon](./media/user-guide/usbx-events/image23.png)</span></span>

<span data-ttu-id="c7285-769">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-769">**Description**</span></span>

<span data-ttu-id="c7285-770">Bu olay bir USBX cihaz sınıfı Pima nesnesi veri gönderme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-770">This event represents a USBX Device Class Pima Object Data Send Event.</span></span>

<span data-ttu-id="c7285-771">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-771">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-772">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-772">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-773">Bilgi alanı 2: nesne tanıtıcısı.</span><span class="sxs-lookup"><span data-stu-id="c7285-773">Info Field 2: Object handle.</span></span>
- <span data-ttu-id="c7285-774">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-774">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-775">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-775">Info Field 4: Not used.</span></span>

### <a name="device-class-pima-object-delete"></a><span data-ttu-id="c7285-776">Device Class Pima nesnesi silme</span><span class="sxs-lookup"><span data-stu-id="c7285-776">Device Class Pima Object Delete</span></span> 

#### <a name="ux_device_class_pima_object_delete"></a><span data-ttu-id="c7285-777">ux_device_class_pima_object_delete</span><span class="sxs-lookup"><span data-stu-id="c7285-777">ux_device_class_pima_object_delete</span></span>

<span data-ttu-id="c7285-778">**Simge** ![ Device Class Pima nesnesi silme simgesi](./media/user-guide/usbx-events/image24.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-778">**Icon** ![Device Class Pima Object Delete icon](./media/user-guide/usbx-events/image24.png)</span></span>

<span data-ttu-id="c7285-779">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-779">**Description**</span></span>

<span data-ttu-id="c7285-780">Bu olay bir USBX Device Class Pima nesnesi silme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-780">This event represents a USBX Device Class Pima Object Delete Event.</span></span>

<span data-ttu-id="c7285-781">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-781">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-782">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-782">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-783">Bilgi alanı 2: nesne tanıtıcısı.</span><span class="sxs-lookup"><span data-stu-id="c7285-783">Info Field 2: Object handle.</span></span>
- <span data-ttu-id="c7285-784">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-784">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-785">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-785">Info Field 4: Not used.</span></span>

### <a name="device-class-pima-object-handles-send"></a><span data-ttu-id="c7285-786">Cihaz sınıfı Pima nesnesi gönderme tutamaçları</span><span class="sxs-lookup"><span data-stu-id="c7285-786">Device Class Pima Object Handles Send</span></span> 

#### <a name="ux_device_class_pima_object_handles_send"></a><span data-ttu-id="c7285-787">ux_device_class_pima_object_handles_send</span><span class="sxs-lookup"><span data-stu-id="c7285-787">ux_device_class_pima_object_handles_send</span></span>

<span data-ttu-id="c7285-788">**Simge** ![ Cihaz sınıfı Pima nesnesi gönderme simgesini Işler](./media/user-guide/usbx-events/image25.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-788">**Icon** ![Device Class Pima Object Handles Send icon](./media/user-guide/usbx-events/image25.png)</span></span>

<span data-ttu-id="c7285-789">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-789">**Description**</span></span>

<span data-ttu-id="c7285-790">Bu olay, bir USBX cihaz sınıfı Pima nesnesi gönderme olayını Işler.</span><span class="sxs-lookup"><span data-stu-id="c7285-790">This event represents a USBX Device Class Pima Object Handles Send Event.</span></span>

<span data-ttu-id="c7285-791">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-791">**Information Fields**</span></span>

- <span data-ttu-id="c7285-792">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-792">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-793">Bilgi alanı 2: depolama KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="c7285-793">Info Field 2: Storage ID.</span></span>
- <span data-ttu-id="c7285-794">Bilgi alanı 3: nesne biçimi kodu.</span><span class="sxs-lookup"><span data-stu-id="c7285-794">Info Field 3: Object format code.</span></span>
- <span data-ttu-id="c7285-795">Bilgi alanı 4: nesne ilişkilendirmesi.</span><span class="sxs-lookup"><span data-stu-id="c7285-795">Info Field 4: Object association.</span></span>

### <a name="device-class-pima-object-info-get"></a><span data-ttu-id="c7285-796">Device Class Pima nesne bilgisi al</span><span class="sxs-lookup"><span data-stu-id="c7285-796">Device Class Pima Object Info Get</span></span> 

#### <a name="ux_device_class_pima_object_info_send"></a><span data-ttu-id="c7285-797">ux_device_class_pima_object_info_send</span><span class="sxs-lookup"><span data-stu-id="c7285-797">ux_device_class_pima_object_info_send</span></span>

<span data-ttu-id="c7285-798">**Simge** ![ Device Class Pima nesne bilgisi al simgesi](./media/user-guide/usbx-events/image26.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-798">**Icon** ![Device Class Pima Object Info Get icon](./media/user-guide/usbx-events/image26.png)</span></span>

<span data-ttu-id="c7285-799">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-799">**Description**</span></span>

<span data-ttu-id="c7285-800">Bu olay bir USBX Device Class Pima nesne bilgileri al olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-800">This event represents a USBX Device Class Pima Object Info Get Event.</span></span>

<span data-ttu-id="c7285-801">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-801">**Information Fields**</span></span>

- <span data-ttu-id="c7285-802">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-802">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-803">Bilgi alanı 2: nesne tanıtıcısı.</span><span class="sxs-lookup"><span data-stu-id="c7285-803">Info Field 2: Object handle.</span></span>
- <span data-ttu-id="c7285-804">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-804">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-805">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-805">Info Field 4: Not used.</span></span>

### <a name="device-class-pima-object-info-send"></a><span data-ttu-id="c7285-806">Device Class Pima nesne bilgileri gönderme</span><span class="sxs-lookup"><span data-stu-id="c7285-806">Device Class Pima Object Info Send</span></span> 

#### <a name="ux_device_class_pima_object_info_send"></a><span data-ttu-id="c7285-807">ux_device_class_pima_object_info_send</span><span class="sxs-lookup"><span data-stu-id="c7285-807">ux_device_class_pima_object_info_send</span></span>

<span data-ttu-id="c7285-808">**Simge** ![ Device Class Pima nesne bilgileri gönderme simgesi](./media/user-guide/usbx-events/image27.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-808">**Icon** ![Device Class Pima Object Info Send icon](./media/user-guide/usbx-events/image27.png)</span></span>

<span data-ttu-id="c7285-809">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-809">**Description**</span></span>

<span data-ttu-id="c7285-810">Bu olay bir USBX Device Class Pima nesne bilgileri gönderme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-810">This event represents a USBX Device Class Pima Object Info Send Event.</span></span>

<span data-ttu-id="c7285-811">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-811">**Information Fields**</span></span>

- <span data-ttu-id="c7285-812">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-812">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-813">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-813">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-814">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-814">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-815">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-815">Info Field 4: Not used.</span></span>

### <a name="device-class-pima-objects-number-send"></a><span data-ttu-id="c7285-816">Cihaz sınıfı Pima nesneleri sayı gönderme</span><span class="sxs-lookup"><span data-stu-id="c7285-816">Device Class Pima Objects Number Send</span></span> 

#### <a name="ux_device_class_pima_object_number_send"></a><span data-ttu-id="c7285-817">ux_device_class_pima_object_number_send</span><span class="sxs-lookup"><span data-stu-id="c7285-817">ux_device_class_pima_object_number_send</span></span>

<span data-ttu-id="c7285-818">**Simge** ![ Cihaz sınıfı Pima nesneleri numara Gönder simgesi](./media/user-guide/usbx-events/image28.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-818">**Icon** ![Device Class Pima Objects Number Send icon](./media/user-guide/usbx-events/image28.png)</span></span>

<span data-ttu-id="c7285-819">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-819">**Description**</span></span>

<span data-ttu-id="c7285-820">Bu olay bir USBX cihaz sınıfı Pima nesne numarası gönderme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-820">This event represents a USBX Device Class Pima Object Number Send event.</span></span>

<span data-ttu-id="c7285-821">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-821">**Information Fields**</span></span>

- <span data-ttu-id="c7285-822">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-822">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-823">Bilgi alanı 2: depolama KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="c7285-823">Info Field 2: Storage ID.</span></span>
- <span data-ttu-id="c7285-824">Bilgi alanı 3: nesne biçimi kodu.</span><span class="sxs-lookup"><span data-stu-id="c7285-824">Info Field 3: Object format code.</span></span>
- <span data-ttu-id="c7285-825">Bilgi alanı 4: nesne ilişkilendir.</span><span class="sxs-lookup"><span data-stu-id="c7285-825">Info Field 4: Object associate.</span></span>

### <a name="device-class-pima-partial-object-data-get"></a><span data-ttu-id="c7285-826">Device Class Pima kısmi nesne verileri al</span><span class="sxs-lookup"><span data-stu-id="c7285-826">Device Class Pima Partial Object Data Get</span></span>

#### <a name="ux_device_class_pima_partial_object_data_get"></a><span data-ttu-id="c7285-827">ux_device_class_pima_partial_object_data_get</span><span class="sxs-lookup"><span data-stu-id="c7285-827">ux_device_class_pima_partial_object_data_get</span></span>

<span data-ttu-id="c7285-828">**Simge** ![ Device Class Pima kısmi nesne verileri al simgesi](./media/user-guide/usbx-events/image29.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-828">**Icon** ![Device Class Pima Partial Object Data Get icon](./media/user-guide/usbx-events/image29.png)</span></span>

<span data-ttu-id="c7285-829">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-829">**Description**</span></span>

<span data-ttu-id="c7285-830">Bu olay bir USBX cihaz sınıfı Pima kısmi nesne verileri al olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-830">This event represents a USBX Device Class Pima Partial Object Data Get Event.</span></span>

<span data-ttu-id="c7285-831">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-831">**Information Fields**</span></span>

- <span data-ttu-id="c7285-832">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-832">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-833">Bilgi alanı 2: nesne tanıtıcısı.</span><span class="sxs-lookup"><span data-stu-id="c7285-833">Info Field 2: Object handle.</span></span>
- <span data-ttu-id="c7285-834">Bilgi alanı 3: istenen fark.</span><span class="sxs-lookup"><span data-stu-id="c7285-834">Info Field 3: Offset requested.</span></span>
- <span data-ttu-id="c7285-835">Bilgi alanı 4: Uzunluk istendi.</span><span class="sxs-lookup"><span data-stu-id="c7285-835">Info Field 4: Length requested.</span></span>

### <a name="device-class-pima-response-send"></a><span data-ttu-id="c7285-836">Cihaz sınıfı Pima yanıtı gönderme</span><span class="sxs-lookup"><span data-stu-id="c7285-836">Device Class Pima Response Send</span></span> 

#### <a name="ux_device_class_pima_response_send"></a><span data-ttu-id="c7285-837">ux_device_class_pima_response_send</span><span class="sxs-lookup"><span data-stu-id="c7285-837">ux_device_class_pima_response_send</span></span>

<span data-ttu-id="c7285-838">**Simge** ![ Cihaz sınıfı Pima yanıtı gönderme simgesi](./media/user-guide/usbx-events/image30.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-838">**Icon** ![Device Class Pima Response Send icon](./media/user-guide/usbx-events/image30.png)</span></span>

<span data-ttu-id="c7285-839">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-839">**Description**</span></span>

<span data-ttu-id="c7285-840">Bu olay bir USBX Device Class Pima yanıtı gönderme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-840">This event represents a USBX Device Class Pima Response Send Event.</span></span>

<span data-ttu-id="c7285-841">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-841">**Information Fields**</span></span>

- <span data-ttu-id="c7285-842">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-842">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-843">Bilgi alanı 2: yanıt kodu.</span><span class="sxs-lookup"><span data-stu-id="c7285-843">Info Field 2: Response code.</span></span>
- <span data-ttu-id="c7285-844">Bilgi alanı 3: sayı parametresi.</span><span class="sxs-lookup"><span data-stu-id="c7285-844">Info Field 3: Number parameter.</span></span>
- <span data-ttu-id="c7285-845">Bilgi alanı 4: Pima parametresi 1.</span><span class="sxs-lookup"><span data-stu-id="c7285-845">Info Field 4: Pima parameter 1.</span></span>

### <a name="device-class-pima-storage-id-send"></a><span data-ttu-id="c7285-846">Cihaz sınıfı Pima depolama kimliği gönderme</span><span class="sxs-lookup"><span data-stu-id="c7285-846">Device Class Pima Storage Id Send</span></span> 

#### <a name="ux_device_class_pima_storage_id_send"></a><span data-ttu-id="c7285-847">ux_device_class_pima_storage_id_send</span><span class="sxs-lookup"><span data-stu-id="c7285-847">ux_device_class_pima_storage_id_send</span></span>

<span data-ttu-id="c7285-848">**Simge** ![ Cihaz sınıfı Pima depolama kimliği gönderme simgesi](./media/user-guide/usbx-events/image31.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-848">**Icon** ![Device Class Pima Storage Id Send icon](./media/user-guide/usbx-events/image31.png)</span></span>

<span data-ttu-id="c7285-849">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-849">**Description**</span></span>

<span data-ttu-id="c7285-850">Bu olay bir USBX cihaz sınıfı Pima depolama kimliği gönderme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-850">This event represents a USBX Device Class Pima Storage Id Send Event.</span></span>

<span data-ttu-id="c7285-851">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-851">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-852">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-852">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-853">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-853">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-854">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-854">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-855">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-855">Info Field 4: Not used.</span></span>

### <a name="device-class-pima-storage-info-send"></a><span data-ttu-id="c7285-856">Cihaz sınıfı Pima depolama bilgileri gönderme</span><span class="sxs-lookup"><span data-stu-id="c7285-856">Device Class Pima Storage Info Send</span></span> 

#### <a name="ux_device_class_pima_storage_info_send"></a><span data-ttu-id="c7285-857">ux_device_class_pima_storage_info_send</span><span class="sxs-lookup"><span data-stu-id="c7285-857">ux_device_class_pima_storage_info_send</span></span>

<span data-ttu-id="c7285-858">**Simge** ![ Cihaz sınıfı Pima depolama bilgileri gönderme simgesi](./media/user-guide/usbx-events/image32.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-858">**Icon** ![Device Class Pima Storage Info Send icon](./media/user-guide/usbx-events/image32.png)</span></span>

<span data-ttu-id="c7285-859">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-859">**Description**</span></span>

<span data-ttu-id="c7285-860">Bu olay bir USBX cihaz sınıfı Pima depolama bilgileri gönderme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-860">This event represents a USBX Device Class Pima Storage Info Send Event.</span></span>

<span data-ttu-id="c7285-861">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-861">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-862">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-862">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-863">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-863">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-864">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-864">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-865">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-865">Info Field 4: Not used.</span></span>

### <a name="device-class-rndis-activate"></a><span data-ttu-id="c7285-866">Cihaz sınıfı rndis etkinleştir</span><span class="sxs-lookup"><span data-stu-id="c7285-866">Device Class Rndis Activate</span></span> 

#### <a name="ux_device_class_rndis_activate"></a><span data-ttu-id="c7285-867">ux_device_class_rndis_activate</span><span class="sxs-lookup"><span data-stu-id="c7285-867">ux_device_class_rndis_activate</span></span>

<span data-ttu-id="c7285-868">**Simge** ![ Cihaz sınıfı rndis etkinleştir simgesi](./media/user-guide/usbx-events/image33.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-868">**Icon** ![Device Class Rndis Activate icon](./media/user-guide/usbx-events/image33.png)</span></span>

<span data-ttu-id="c7285-869">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-869">**Description**</span></span>

<span data-ttu-id="c7285-870">Bu olay bir USBX cihaz sınıfı rndis Activate olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-870">This event represents a USBX Device Class Rndis Activate Event.</span></span>

<span data-ttu-id="c7285-871">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-871">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-872">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-872">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-873">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-873">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-874">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-874">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-875">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-875">Info Field 4: Not used.</span></span>

### <a name="device-class-rndis-deactivate"></a><span data-ttu-id="c7285-876">Cihaz sınıfı rndis devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="c7285-876">Device Class Rndis Deactivate</span></span> 

#### <a name="ux_device_class_rndis_deactivate"></a><span data-ttu-id="c7285-877">ux_device_class_rndis_deactivate</span><span class="sxs-lookup"><span data-stu-id="c7285-877">ux_device_class_rndis_deactivate</span></span>

<span data-ttu-id="c7285-878">**Simge** ![ Cihaz sınıfı rndis devre dışı bırakma simgesi](./media/user-guide/usbx-events/image34.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-878">**Icon** ![Device Class Rndis Deactivate icon](./media/user-guide/usbx-events/image34.png)</span></span>

<span data-ttu-id="c7285-879">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-879">**Description**</span></span>

<span data-ttu-id="c7285-880">Bu olay bir USBX cihaz sınıfı rndis devre dışı bırakma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-880">This event represents a USBX Device Class Rndis Deactivate Event.</span></span>

<span data-ttu-id="c7285-881">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-881">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-882">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-882">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-883">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-883">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-884">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-884">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-885">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-885">Info Field 4: Not used.</span></span>

### <a name="device-class-rndis-message-keep-alive"></a><span data-ttu-id="c7285-886">Cihaz sınıfı rndis Ileti canlı tut</span><span class="sxs-lookup"><span data-stu-id="c7285-886">Device Class Rndis Message Keep Alive</span></span> 

#### <a name="ux_device_class_rndis_msg_keep_alive"></a><span data-ttu-id="c7285-887">ux_device_class_rndis_msg_keep_alive</span><span class="sxs-lookup"><span data-stu-id="c7285-887">ux_device_class_rndis_msg_keep_alive</span></span>

<span data-ttu-id="c7285-888">**Simge** ![ Cihaz sınıfı rndis Ileti canlı tut simgesi](./media/user-guide/usbx-events/image35.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-888">**Icon** ![Device Class Rndis Message Keep Alive icon](./media/user-guide/usbx-events/image35.png)</span></span>

<span data-ttu-id="c7285-889">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-889">**Description**</span></span>

<span data-ttu-id="c7285-890">Bu olay bir USBX cihaz sınıfını rndis Iletisi etkin tut olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-890">This event represents a USBX Device Class Rndis Message Keep Alive Event.</span></span>

<span data-ttu-id="c7285-891">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-891">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-892">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-892">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-893">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-893">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-894">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-894">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-895">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-895">Info Field 4: Not used.</span></span>

### <a name="device-class-rndis-message-query"></a><span data-ttu-id="c7285-896">Cihaz sınıfı rndis Ileti sorgusu</span><span class="sxs-lookup"><span data-stu-id="c7285-896">Device Class Rndis Message Query</span></span> 

#### <a name="ux_device_class_rndis_msg_keep_query"></a><span data-ttu-id="c7285-897">ux_device_class_rndis_msg_keep_query</span><span class="sxs-lookup"><span data-stu-id="c7285-897">ux_device_class_rndis_msg_keep_query</span></span>

<span data-ttu-id="c7285-898">**Simge** ![ Cihaz sınıfı rndis Iletisi sorgu simgesi](./media/user-guide/usbx-events/image36.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-898">**Icon** ![Device Class Rndis Message Query icon](./media/user-guide/usbx-events/image36.png)</span></span>

<span data-ttu-id="c7285-899">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-899">**Description**</span></span>

<span data-ttu-id="c7285-900">Bu olay bir USBX cihaz sınıfı rndis Iletisi sorgu olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-900">This event represents a USBX Device Class Rndis Message Query Event.</span></span>

<span data-ttu-id="c7285-901">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-901">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-902">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-902">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-903">Bilgi alanı 2: rndis OID.</span><span class="sxs-lookup"><span data-stu-id="c7285-903">Info Field 2: Rndis OID.</span></span>
- <span data-ttu-id="c7285-904">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-904">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-905">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-905">Info Field 4: Not used.</span></span>

### <a name="device-class-rndis-message-reset"></a><span data-ttu-id="c7285-906">Cihaz sınıfı rndis Ileti sıfırlama</span><span class="sxs-lookup"><span data-stu-id="c7285-906">Device Class Rndis Message Reset</span></span> 

#### <a name="ux_device_class_rndis_msg_reset"></a><span data-ttu-id="c7285-907">ux_device_class_rndis_msg_reset</span><span class="sxs-lookup"><span data-stu-id="c7285-907">ux_device_class_rndis_msg_reset</span></span>

<span data-ttu-id="c7285-908">**Simge** ![ Cihaz sınıfı rndis Ileti sıfırlama simgesi](./media/user-guide/usbx-events/image37.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-908">**Icon** ![Device Class Rndis Message Reset icon](./media/user-guide/usbx-events/image37.png)</span></span>

<span data-ttu-id="c7285-909">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-909">**Description**</span></span>

<span data-ttu-id="c7285-910">Bu olay bir USBX cihaz sınıfı rndis Ileti sıfırlama olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-910">This event represents a USBX Device Class Rndis Message Reset Event.</span></span>

<span data-ttu-id="c7285-911">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-911">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-912">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-912">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-913">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-913">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-914">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-914">Info Field 3: Not used.</span></span>

### <a name="device-class-rndis-message-set"></a><span data-ttu-id="c7285-915">Cihaz sınıfı rndis Ileti kümesi</span><span class="sxs-lookup"><span data-stu-id="c7285-915">Device Class Rndis Message Set</span></span> 

#### <a name="ux_device_class_rndis_msg_set"></a><span data-ttu-id="c7285-916">ux_device_class_rndis_msg_set</span><span class="sxs-lookup"><span data-stu-id="c7285-916">ux_device_class_rndis_msg_set</span></span>

<span data-ttu-id="c7285-917">**Simge** ![ Cihaz sınıfı rndis Ileti kümesi simgesi](./media/user-guide/usbx-events/image38.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-917">**Icon** ![Device Class Rndis Message Set icon](./media/user-guide/usbx-events/image38.png)</span></span>

<span data-ttu-id="c7285-918">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-918">**Description**</span></span>

<span data-ttu-id="c7285-919">Bu olay bir USBX cihaz sınıfı rndis Ileti kümesi olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-919">This event represents a USBX Device Class Rndis Message Set Event.</span></span>

<span data-ttu-id="c7285-920">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-920">**Information Fields**</span></span>

- <span data-ttu-id="c7285-921">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-921">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-922">Bilgi alanı 2: rndis OID.</span><span class="sxs-lookup"><span data-stu-id="c7285-922">Info Field 2: Rndis OID.</span></span>
- <span data-ttu-id="c7285-923">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-923">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-924">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-924">Info Field 4: Not used.</span></span>

### <a name="device-class-rndis-packet-receive"></a><span data-ttu-id="c7285-925">Cihaz sınıfı rndis paket alma</span><span class="sxs-lookup"><span data-stu-id="c7285-925">Device Class Rndis Packet Receive</span></span> 

#### <a name="ux_device_class_rndis_packet_receive"></a><span data-ttu-id="c7285-926">ux_device_class_rndis_packet_receive</span><span class="sxs-lookup"><span data-stu-id="c7285-926">ux_device_class_rndis_packet_receive</span></span>

<span data-ttu-id="c7285-927">**Simge** ![ Cihaz sınıfı rndis paket alma simgesi](./media/user-guide/usbx-events/image39.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-927">**Icon** ![Device Class Rndis Packet Receive icon](./media/user-guide/usbx-events/image39.png)</span></span>

<span data-ttu-id="c7285-928">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-928">**Description**</span></span>

<span data-ttu-id="c7285-929">Bu olay bir USBX cihaz sınıfı rndis paket alma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-929">This event represents a USBX Device Class Rndis Packet Receive Event.</span></span>

<span data-ttu-id="c7285-930">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-930">**Information Fields**</span></span>

- <span data-ttu-id="c7285-931">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-931">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-932">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-932">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-933">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-933">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-934">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-934">Info Field 4: Not used.</span></span>

### <a name="device-class-rndis-packet-transmit"></a><span data-ttu-id="c7285-935">Cihaz sınıfı rndis paket Iletimi</span><span class="sxs-lookup"><span data-stu-id="c7285-935">Device Class Rndis Packet Transmit</span></span> 

#### <a name="ux_device_class_rndis_packet_transmit"></a><span data-ttu-id="c7285-936">ux_device_class_rndis_packet_transmit</span><span class="sxs-lookup"><span data-stu-id="c7285-936">ux_device_class_rndis_packet_transmit</span></span>

<span data-ttu-id="c7285-937">**Simge** ![ Cihaz sınıfı rndis paket Iletme simgesi](./media/user-guide/usbx-events/image40.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-937">**Icon** ![Device Class Rndis Packet Transmit icon](./media/user-guide/usbx-events/image40.png)</span></span>

<span data-ttu-id="c7285-938">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-938">**Description**</span></span>

<span data-ttu-id="c7285-939">Bu olay bir USBX cihaz sınıfı rndis paket Iletme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-939">This event represents a USBX Device Class Rndis Packet Transmit Event.</span></span>

<span data-ttu-id="c7285-940">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-940">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-941">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-941">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-942">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-942">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-943">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-943">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-944">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-944">Info Field 4: Not used.</span></span>

### <a name="device-class-storage-activate"></a><span data-ttu-id="c7285-945">Cihaz sınıfı depolamayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="c7285-945">Device Class Storage Activate</span></span> 

#### <a name="ux_device_class_storage_activate"></a><span data-ttu-id="c7285-946">ux_device_class_storage_activate</span><span class="sxs-lookup"><span data-stu-id="c7285-946">ux_device_class_storage_activate</span></span>

<span data-ttu-id="c7285-947">**Simge** ![ Cihaz sınıfı depolama etkinleştirme simgesi](./media/user-guide/usbx-events/image41.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-947">**Icon** ![Device Class Storage Activate icon](./media/user-guide/usbx-events/image41.png)</span></span>

<span data-ttu-id="c7285-948">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-948">**Description**</span></span>

<span data-ttu-id="c7285-949">Bu olay bir USBX cihaz sınıfı depolama etkinleştirme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-949">This event represents a USBX Device Class Storage Activate Event.</span></span>

<span data-ttu-id="c7285-950">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-950">**Information Fields**</span></span>

- <span data-ttu-id="c7285-951">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-951">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-952">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-952">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-953">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-953">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-954">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-954">Info Field 4: Not used.</span></span>

### <a name="device-class-storage-deactivate"></a><span data-ttu-id="c7285-955">Cihaz sınıfı depolamayı devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="c7285-955">Device Class Storage Deactivate</span></span> 

#### <a name="ux_device_class_storage_deactivate"></a><span data-ttu-id="c7285-956">ux_device_class_storage_deactivate</span><span class="sxs-lookup"><span data-stu-id="c7285-956">ux_device_class_storage_deactivate</span></span>

<span data-ttu-id="c7285-957">**Simge** ![ Cihaz sınıfı depolamayı devre dışı bırakma simgesi](./media/user-guide/usbx-events/image42.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-957">**Icon** ![Device Class Storage Deactivate icon](./media/user-guide/usbx-events/image42.png)</span></span>

<span data-ttu-id="c7285-958">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-958">**Description**</span></span>

<span data-ttu-id="c7285-959">Bu olay bir USBX cihaz sınıfı depolaması devre dışı bırakma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-959">This event represents a USBX Device Class Storage Deactivate Event.</span></span>

<span data-ttu-id="c7285-960">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-960">**Information Fields**</span></span>

- <span data-ttu-id="c7285-961">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-961">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-962">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-962">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-963">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-963">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-964">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-964">Info Field 4: Not used.</span></span>

### <a name="device-class-storage-format"></a><span data-ttu-id="c7285-965">Cihaz sınıfı depolama biçimi</span><span class="sxs-lookup"><span data-stu-id="c7285-965">Device Class Storage Format</span></span> 

#### <a name="ux_device_class_storage_format"></a><span data-ttu-id="c7285-966">ux_device_class_storage_format</span><span class="sxs-lookup"><span data-stu-id="c7285-966">ux_device_class_storage_format</span></span>

<span data-ttu-id="c7285-967">**Simge** ![ Cihaz sınıfı depolama biçimi simgesi](./media/user-guide/usbx-events/image43.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-967">**Icon** ![Device Class Storage Format icon](./media/user-guide/usbx-events/image43.png)</span></span>

<span data-ttu-id="c7285-968">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-968">**Description**</span></span>

<span data-ttu-id="c7285-969">Bu olay bir USBX cihaz sınıfı depolama biçimi olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-969">This event represents a USBX Device Class Storage Format Event.</span></span>

<span data-ttu-id="c7285-970">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-970">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-971">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-971">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-972">Bilgi alanı 2: LUN.</span><span class="sxs-lookup"><span data-stu-id="c7285-972">Info Field 2: Lun.</span></span>
- <span data-ttu-id="c7285-973">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-973">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-974">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-974">Info Field 4: Not used.</span></span>

### <a name="device-class-storage-inquiry"></a><span data-ttu-id="c7285-975">Cihaz sınıfı depolama sorgusu</span><span class="sxs-lookup"><span data-stu-id="c7285-975">Device Class Storage Inquiry</span></span> 

#### <a name="ux_device_class_storage_inquiry"></a><span data-ttu-id="c7285-976">ux_device_class_storage_inquiry</span><span class="sxs-lookup"><span data-stu-id="c7285-976">ux_device_class_storage_inquiry</span></span>

<span data-ttu-id="c7285-977">**Simge** ![ Cihaz sınıfı depolama sorgulama simgesi](./media/user-guide/usbx-events/image44.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-977">**Icon** ![Device Class Storage Inquiry icon](./media/user-guide/usbx-events/image44.png)</span></span>

<span data-ttu-id="c7285-978">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-978">**Description**</span></span>

<span data-ttu-id="c7285-979">Bu olay bir USBX cihaz sınıfı depolama sorgulama olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-979">This event represents a USBX Device Class Storage Inquiry Event.</span></span>

<span data-ttu-id="c7285-980">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-980">**Information Fields**</span></span>

- <span data-ttu-id="c7285-981">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-981">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-982">Bilgi alanı 2: LUN.</span><span class="sxs-lookup"><span data-stu-id="c7285-982">Info Field 2: Lun.</span></span>
- <span data-ttu-id="c7285-983">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-983">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-984">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-984">Info Field 4: Not used.</span></span>

### <a name="device-class-storage-mode-select"></a><span data-ttu-id="c7285-985">Cihaz sınıfı depolama modu seçme</span><span class="sxs-lookup"><span data-stu-id="c7285-985">Device Class Storage Mode Select</span></span>

#### <a name="ux_device_class_storage_mode_select"></a><span data-ttu-id="c7285-986">ux_device_class_storage_mode_select</span><span class="sxs-lookup"><span data-stu-id="c7285-986">ux_device_class_storage_mode_select</span></span>

<span data-ttu-id="c7285-987">**Simge** ![ Cihaz sınıfı depolama modu seçme simgesi](./media/user-guide/usbx-events/image45.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-987">**Icon** ![Device Class Storage Mode Select icon](./media/user-guide/usbx-events/image45.png)</span></span>

<span data-ttu-id="c7285-988">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-988">**Description**</span></span>

<span data-ttu-id="c7285-989">Bu olay bir USBX cihaz sınıfı depolama modu seçme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-989">This event represents a USBX Device Class Storage Mode Select Event.</span></span>

<span data-ttu-id="c7285-990">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-990">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-991">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-991">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-992">Bilgi alanı 2: LUN.</span><span class="sxs-lookup"><span data-stu-id="c7285-992">Info Field 2: Lun.</span></span>
- <span data-ttu-id="c7285-993">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-993">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-994">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-994">Info Field 4: Not used.</span></span>

### <a name="device-class-storage-mode-sense"></a><span data-ttu-id="c7285-995">Cihaz sınıfı depolama modu algılama</span><span class="sxs-lookup"><span data-stu-id="c7285-995">Device Class Storage Mode Sense</span></span> 

#### <a name="ux_device_class_storage_mode_sense"></a><span data-ttu-id="c7285-996">ux_device_class_storage_mode_sense</span><span class="sxs-lookup"><span data-stu-id="c7285-996">ux_device_class_storage_mode_sense</span></span>

<span data-ttu-id="c7285-997">**Simge** ![ Cihaz sınıfı depolama modu algılama simgesi](./media/user-guide/usbx-events/image46.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-997">**Icon** ![Device Class Storage Mode Sense icon](./media/user-guide/usbx-events/image46.png)</span></span>

<span data-ttu-id="c7285-998">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-998">**Description**</span></span>

<span data-ttu-id="c7285-999">Bu olay, bir USBX cihaz sınıfı depolama modu Sense olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-999">This event represents a USBX Device Class Storage Mode Sense Event.</span></span>

<span data-ttu-id="c7285-1000">Bilgi alanları</span><span class="sxs-lookup"><span data-stu-id="c7285-1000">Information Fields</span></span> 

- <span data-ttu-id="c7285-1001">NFO alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1001">nfo Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-1002">Bilgi alanı 2: LUN.</span><span class="sxs-lookup"><span data-stu-id="c7285-1002">Info Field 2: Lun.</span></span>
- <span data-ttu-id="c7285-1003">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1003">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1004">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1004">Info Field 4: Not used.</span></span>

### <a name="device-class-storage-prevent-allow-media-removal"></a><span data-ttu-id="c7285-1005">Cihaz sınıfı depolaması medya kaldırılmasına Izin vermeyi engelliyor</span><span class="sxs-lookup"><span data-stu-id="c7285-1005">Device Class Storage Prevent Allow Media Removal</span></span> 

#### <a name="ux_device_class_storage_prevent_allow_media_removal"></a><span data-ttu-id="c7285-1006">ux_device_class_storage_prevent_allow_media_removal</span><span class="sxs-lookup"><span data-stu-id="c7285-1006">ux_device_class_storage_prevent_allow_media_removal</span></span>

<span data-ttu-id="c7285-1007">**Simge** ![ Cihaz sınıfı depolaması medya kaldırma simgesine Izin vermeyi engelliyor](./media/user-guide/usbx-events/image47.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1007">**Icon** ![Device Class Storage Prevent Allow Media Removal icon](./media/user-guide/usbx-events/image47.png)</span></span>

<span data-ttu-id="c7285-1008">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1008">**Description**</span></span>

<span data-ttu-id="c7285-1009">Bu olay bir USBX cihaz sınıfı depolaması, medya kaldırma olayına Izin vermeyi engelliyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1009">This event represents a USBX Device Class Storage Prevent Allow Media Removal Event.</span></span>

<span data-ttu-id="c7285-1010">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1010">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1011">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1011">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-1012">Bilgi alanı 2: LUN.</span><span class="sxs-lookup"><span data-stu-id="c7285-1012">Info Field 2: Lun.</span></span>
- <span data-ttu-id="c7285-1013">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1013">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1014">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1014">Info Field 4: Not used.</span></span>

### <a name="device-class-storage-read"></a><span data-ttu-id="c7285-1015">Cihaz sınıfı depolama okuma</span><span class="sxs-lookup"><span data-stu-id="c7285-1015">Device Class Storage Read</span></span> 

#### <a name="ux_device_class_storage_read"></a><span data-ttu-id="c7285-1016">ux_device_class_storage_read</span><span class="sxs-lookup"><span data-stu-id="c7285-1016">ux_device_class_storage_read</span></span>

<span data-ttu-id="c7285-1017">**Simge** ![ Cihaz sınıfı depolama okuma simgesi](./media/user-guide/usbx-events/image48.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1017">**Icon** ![Device Class Storage Read icon](./media/user-guide/usbx-events/image48.png)</span></span>

<span data-ttu-id="c7285-1018">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1018">**Description**</span></span>

<span data-ttu-id="c7285-1019">Bu olay bir USBX cihaz sınıfı depolama okuma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1019">This event represents a USBX Device Class Storage Read Event.</span></span>

<span data-ttu-id="c7285-1020">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1020">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1021">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1021">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-1022">Bilgi alanı 2: LUN.</span><span class="sxs-lookup"><span data-stu-id="c7285-1022">Info Field 2: Lun.</span></span>
- <span data-ttu-id="c7285-1023">Bilgi alanı 3: sektör.</span><span class="sxs-lookup"><span data-stu-id="c7285-1023">Info Field 3: Sector.</span></span>
- <span data-ttu-id="c7285-1024">Bilgi alanı 4: sayı kesimleri.</span><span class="sxs-lookup"><span data-stu-id="c7285-1024">Info Field 4: Number sectors.</span></span>

### <a name="device-class-storage-read-capacity"></a><span data-ttu-id="c7285-1025">Cihaz sınıfı depolama okuma kapasitesi</span><span class="sxs-lookup"><span data-stu-id="c7285-1025">Device Class Storage Read Capacity</span></span> 

#### <a name="ux_device_class_storage_read_capacity"></a><span data-ttu-id="c7285-1026">ux_device_class_storage_read_capacity</span><span class="sxs-lookup"><span data-stu-id="c7285-1026">ux_device_class_storage_read_capacity</span></span>

<span data-ttu-id="c7285-1027">**Simge** ![ Cihaz sınıfı depolama okuma kapasitesi simgesi](./media/user-guide/usbx-events/image49.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1027">**Icon** ![Device Class Storage Read Capacity icon](./media/user-guide/usbx-events/image49.png)</span></span>

<span data-ttu-id="c7285-1028">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1028">**Description**</span></span>

<span data-ttu-id="c7285-1029">Bu olay bir USBX cihaz sınıfı depolama okuma kapasitesi olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1029">This event represents a USBX Device Class Storage Read Capacity Event.</span></span>

<span data-ttu-id="c7285-1030">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1030">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-1031">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1031">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-1032">Bilgi alanı 2: LUN.</span><span class="sxs-lookup"><span data-stu-id="c7285-1032">Info Field 2: Lun.</span></span>
- <span data-ttu-id="c7285-1033">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1033">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1034">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1034">Info Field 4: Not used.</span></span>

### <a name="device-class-storage-read-format-capacity"></a><span data-ttu-id="c7285-1035">Cihaz sınıfı depolama okuma biçimi kapasitesi</span><span class="sxs-lookup"><span data-stu-id="c7285-1035">Device Class Storage Read Format Capacity</span></span> 

#### <a name="ux_device_class_storage_read_format_capacity"></a><span data-ttu-id="c7285-1036">ux_device_class_storage_read_format_capacity</span><span class="sxs-lookup"><span data-stu-id="c7285-1036">ux_device_class_storage_read_format_capacity</span></span>

<span data-ttu-id="c7285-1037">**Simge** ![ Cihaz sınıfı depolama okuma biçimi kapasitesi simgesi](./media/user-guide/usbx-events/image50.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1037">**Icon** ![Device Class Storage Read Format Capacity icon](./media/user-guide/usbx-events/image50.png)</span></span>

<span data-ttu-id="c7285-1038">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1038">**Description**</span></span>

<span data-ttu-id="c7285-1039">Bu olay bir USBX cihaz sınıfı depolama okuma biçimi kapasitesi olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1039">This event represents a USBX Device Class Storage Read Format Capacity Event.</span></span>

<span data-ttu-id="c7285-1040">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1040">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-1041">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1041">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-1042">Bilgi alanı 2: LUN.</span><span class="sxs-lookup"><span data-stu-id="c7285-1042">Info Field 2: Lun.</span></span>
- <span data-ttu-id="c7285-1043">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1043">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1044">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1044">Info Field 4: Not used.</span></span>

### <a name="device-class-storage-read-toc"></a><span data-ttu-id="c7285-1045">Device Class depolaması TOC okuma</span><span class="sxs-lookup"><span data-stu-id="c7285-1045">Device Class Storage Read TOC</span></span> 

#### <a name="ux_device_class_storage_read_toc"></a><span data-ttu-id="c7285-1046">ux_device_class_storage_read_toc</span><span class="sxs-lookup"><span data-stu-id="c7285-1046">ux_device_class_storage_read_toc</span></span>

<span data-ttu-id="c7285-1047">**Simge** ![ Device Class depolama okuma TOC simgesi](./media/user-guide/usbx-events/image51.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1047">**Icon** ![Device Class Storage Read TOC icon](./media/user-guide/usbx-events/image51.png)</span></span>

<span data-ttu-id="c7285-1048">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1048">**Description**</span></span>

<span data-ttu-id="c7285-1049">Bu olay, bir USBX cihaz sınıfı depolama okuma TOC olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1049">This event represents a USBX Device Class Storage Read TOC Event.</span></span>

<span data-ttu-id="c7285-1050">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1050">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1051">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1051">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-1052">Bilgi alanı 2: LUN.</span><span class="sxs-lookup"><span data-stu-id="c7285-1052">Info Field 2: Lun.</span></span>
- <span data-ttu-id="c7285-1053">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1053">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1054">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1054">Info Field 4: Not used.</span></span>

### <a name="device-class-storage-request-sense"></a><span data-ttu-id="c7285-1055">Cihaz sınıfı depolama Istek algılaması</span><span class="sxs-lookup"><span data-stu-id="c7285-1055">Device Class Storage Request Sense</span></span> 

#### <a name="ux_device_class_storage_request_sense"></a><span data-ttu-id="c7285-1056">ux_device_class_storage_request_sense</span><span class="sxs-lookup"><span data-stu-id="c7285-1056">ux_device_class_storage_request_sense</span></span>

<span data-ttu-id="c7285-1057">**Simge** ![ Cihaz sınıfı depolama Isteği algılama simgesi](./media/user-guide/usbx-events/image52.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1057">**Icon** ![Device Class Storage Request Sense icon](./media/user-guide/usbx-events/image52.png)</span></span>

<span data-ttu-id="c7285-1058">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1058">**Description**</span></span>

<span data-ttu-id="c7285-1059">Bu olay bir USBX cihaz sınıfı depolama Istek algılama olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1059">This event represents a USBX Device Class Storage Request Sense Event.</span></span>

<span data-ttu-id="c7285-1060">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1060">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-1061">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1061">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-1062">Bilgi alanı 2: LUN.</span><span class="sxs-lookup"><span data-stu-id="c7285-1062">Info Field 2: Lun.</span></span>
- <span data-ttu-id="c7285-1063">Bilgi alanı 3: Sense anahtarı.</span><span class="sxs-lookup"><span data-stu-id="c7285-1063">Info Field 3: Sense key.</span></span>
- <span data-ttu-id="c7285-1064">Bilgi alanı 4: kod.</span><span class="sxs-lookup"><span data-stu-id="c7285-1064">Info Field 4: Code.</span></span>

### <a name="device-class-storage-start-stop"></a><span data-ttu-id="c7285-1065">Cihaz sınıfı depolama başlangıç durağı</span><span class="sxs-lookup"><span data-stu-id="c7285-1065">Device Class Storage Start Stop</span></span> 

#### <a name="ux_device_class_storage_start_stop"></a><span data-ttu-id="c7285-1066">ux_device_class_storage_start_stop</span><span class="sxs-lookup"><span data-stu-id="c7285-1066">ux_device_class_storage_start_stop</span></span>

<span data-ttu-id="c7285-1067">**Simge** ![ Cihaz sınıfı depolama başlatma durdurma simgesi](./media/user-guide/usbx-events/image53.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1067">**Icon** ![Device Class Storage Start Stop icon](./media/user-guide/usbx-events/image53.png)</span></span>

<span data-ttu-id="c7285-1068">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1068">**Description**</span></span>

<span data-ttu-id="c7285-1069">Bu olay bir USBX cihaz sınıfı depolama başlatma durdurma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1069">This event represents a USBX Device Class Storage Start Stop Event.</span></span>

<span data-ttu-id="c7285-1070">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1070">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1071">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1071">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-1072">Bilgi alanı 2: LUN.</span><span class="sxs-lookup"><span data-stu-id="c7285-1072">Info Field 2: Lun.</span></span>
- <span data-ttu-id="c7285-1073">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1073">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1074">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1074">Info Field 4: Not used.</span></span>

### <a name="device-class-storage-test-ready"></a><span data-ttu-id="c7285-1075">Cihaz sınıfı depolama sınaması hazırlanıyor</span><span class="sxs-lookup"><span data-stu-id="c7285-1075">Device Class Storage Test Ready</span></span> 

#### <a name="ux_device_class_storage_test_ready"></a><span data-ttu-id="c7285-1076">ux_device_class_storage_test_ready</span><span class="sxs-lookup"><span data-stu-id="c7285-1076">ux_device_class_storage_test_ready</span></span>

<span data-ttu-id="c7285-1077">**Simge** ![ Cihaz sınıfı depolama sınaması hazırlanıyor simgesi](./media/user-guide/usbx-events/image54.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1077">**Icon** ![Device Class Storage Test Ready icon](./media/user-guide/usbx-events/image54.png)</span></span>

<span data-ttu-id="c7285-1078">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1078">**Description**</span></span>

<span data-ttu-id="c7285-1079">Bu olay, bir USBX cihaz sınıfı depolama testinin Ready olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1079">This event represents a USBX Device Class Storage Test Ready Event.</span></span>

<span data-ttu-id="c7285-1080">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1080">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-1081">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1081">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-1082">Bilgi alanı 2: LUN.</span><span class="sxs-lookup"><span data-stu-id="c7285-1082">Info Field 2: Lun.</span></span>
- <span data-ttu-id="c7285-1083">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1083">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1084">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1084">Info Field 4: Not used.</span></span>

### <a name="device-class-storage-verify"></a><span data-ttu-id="c7285-1085">Cihaz sınıfı depolama doğrulaması</span><span class="sxs-lookup"><span data-stu-id="c7285-1085">Device Class Storage Verify</span></span> 

#### <a name="ux_device_class_storage_verify"></a><span data-ttu-id="c7285-1086">ux_device_class_storage_verify</span><span class="sxs-lookup"><span data-stu-id="c7285-1086">ux_device_class_storage_verify</span></span>

<span data-ttu-id="c7285-1087">**Simge** ![ Cihaz sınıfı depolama doğrulama simgesi](./media/user-guide/usbx-events/image55.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1087">**Icon** ![Device Class Storage Verify icon](./media/user-guide/usbx-events/image55.png)</span></span>

<span data-ttu-id="c7285-1088">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1088">**Description**</span></span>

<span data-ttu-id="c7285-1089">Bu olay bir USBX cihaz sınıfı depolama doğrulama olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1089">This event represents a USBX Device Class Storage Verify Event.</span></span>

<span data-ttu-id="c7285-1090">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1090">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-1091">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1091">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-1092">Bilgi alanı 2: LUN.</span><span class="sxs-lookup"><span data-stu-id="c7285-1092">Info Field 2: Lun.</span></span>
- <span data-ttu-id="c7285-1093">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1093">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1094">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1094">Info Field 4: Not used.</span></span>

### <a name="device-class-storage-write"></a><span data-ttu-id="c7285-1095">Cihaz sınıfı depolama yazma</span><span class="sxs-lookup"><span data-stu-id="c7285-1095">Device Class Storage Write</span></span> 

#### <a name="ux_device_class_storage_write"></a><span data-ttu-id="c7285-1096">ux_device_class_storage_write</span><span class="sxs-lookup"><span data-stu-id="c7285-1096">ux_device_class_storage_write</span></span>

<span data-ttu-id="c7285-1097">**Simge** ![ Cihaz sınıfı depolama yazma simgesi](./media/user-guide/usbx-events/image56.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1097">**Icon** ![Device Class Storage Write icon](./media/user-guide/usbx-events/image56.png)</span></span>

<span data-ttu-id="c7285-1098">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1098">**Description**</span></span>

<span data-ttu-id="c7285-1099">Bu olay bir USBX cihaz sınıfı depolama yazma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1099">This event represents a USBX Device Class Storage Write Event.</span></span>

<span data-ttu-id="c7285-1100">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1100">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-1101">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1101">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-1102">Bilgi alanı 2: LUN.</span><span class="sxs-lookup"><span data-stu-id="c7285-1102">Info Field 2: Lun.</span></span>
- <span data-ttu-id="c7285-1103">Bilgi alanı 3: sektör.</span><span class="sxs-lookup"><span data-stu-id="c7285-1103">Info Field 3: Sector.</span></span>
- <span data-ttu-id="c7285-1104">Bilgi alanı 4: sayı kesimleri.</span><span class="sxs-lookup"><span data-stu-id="c7285-1104">Info Field 4: Number sectors.</span></span>

### <a name="device-stack-alternate-setting-get"></a><span data-ttu-id="c7285-1105">Cihaz yığını alternatif ayarı al</span><span class="sxs-lookup"><span data-stu-id="c7285-1105">Device Stack Alternate Setting Get</span></span> 

#### <a name="ux_device_class_alternate_setting_get"></a><span data-ttu-id="c7285-1106">ux_device_class_alternate_setting_get</span><span class="sxs-lookup"><span data-stu-id="c7285-1106">ux_device_class_alternate_setting_get</span></span>

<span data-ttu-id="c7285-1107">**Simge** ![ Cihaz yığını alternatif ayarı al simgesi](./media/user-guide/usbx-events/image57.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1107">**Icon** ![Device Stack Alternate Setting Get icon](./media/user-guide/usbx-events/image57.png)</span></span>

<span data-ttu-id="c7285-1108">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1108">**Description**</span></span>

<span data-ttu-id="c7285-1109">Bu olay bir USBX cihaz yığını alternatif ayarı al olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1109">This event represents a USBX Device Stack Alternate Setting Get Event.</span></span>

<span data-ttu-id="c7285-1110">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1110">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1111">Bilgi alanı 1: arabirim değeri.</span><span class="sxs-lookup"><span data-stu-id="c7285-1111">Info Field 1: Interface value.</span></span>
- <span data-ttu-id="c7285-1112">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1112">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-1113">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1113">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1114">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1114">Info Field 4: Not used.</span></span>

### <a name="device-stack-alternate-setting-set"></a><span data-ttu-id="c7285-1115">Cihaz yığını alternatif ayarı kümesi</span><span class="sxs-lookup"><span data-stu-id="c7285-1115">Device Stack Alternate Setting Set</span></span> 

#### <a name="ux_device_class_alternate_setting_set"></a><span data-ttu-id="c7285-1116">ux_device_class_alternate_setting_set</span><span class="sxs-lookup"><span data-stu-id="c7285-1116">ux_device_class_alternate_setting_set</span></span>

<span data-ttu-id="c7285-1117">**Simge** ![ Cihaz yığını alternatif ayarı kümesi simgesi](./media/user-guide/usbx-events/image58.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1117">**Icon** ![Device Stack Alternate Setting Set icon](./media/user-guide/usbx-events/image58.png)</span></span>

<span data-ttu-id="c7285-1118">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1118">**Description**</span></span>

<span data-ttu-id="c7285-1119">Bu olay bir USBX cihaz yığını alternatif ayar kümesi olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1119">This event represents a USBX Device Stack Alternate Setting Set Event.</span></span>

<span data-ttu-id="c7285-1120">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1120">**Information Fields**</span></span>
- <span data-ttu-id="c7285-1121">Bilgi alanı 1: arabirim değeri.</span><span class="sxs-lookup"><span data-stu-id="c7285-1121">Info Field 1: Interface value.</span></span>
- <span data-ttu-id="c7285-1122">Bilgi alanı 2: alternatif ayar değeri.</span><span class="sxs-lookup"><span data-stu-id="c7285-1122">Info Field 2: Alternate setting value.</span></span>
- <span data-ttu-id="c7285-1123">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1123">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1124">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1124">Info Field 4: Not used.</span></span>

### <a name="device-stack-class-register"></a><span data-ttu-id="c7285-1125">Cihaz yığını sınıf kaydı</span><span class="sxs-lookup"><span data-stu-id="c7285-1125">Device Stack Class Register</span></span> 

#### <a name="ux_device_stack_class_register"></a><span data-ttu-id="c7285-1126">ux_device_stack_class_register</span><span class="sxs-lookup"><span data-stu-id="c7285-1126">ux_device_stack_class_register</span></span>

<span data-ttu-id="c7285-1127">**Simge** ![ Cihaz yığını sınıfı kayıt simgesi](./media/user-guide/usbx-events/image59.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1127">**Icon** ![Device Stack Class Register icon](./media/user-guide/usbx-events/image59.png)</span></span>

<span data-ttu-id="c7285-1128">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1128">**Description**</span></span>

<span data-ttu-id="c7285-1129">Bu olay bir USBX cihaz yığını sınıf kaydı olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1129">This event represents a USBX Device Stack Class Register Event.</span></span>

<span data-ttu-id="c7285-1130">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1130">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1131">Bilgi alanı 1: sınıf adı.</span><span class="sxs-lookup"><span data-stu-id="c7285-1131">Info Field 1: Class name.</span></span>
- <span data-ttu-id="c7285-1132">Bilgi alanı 2: arabirim numarası.</span><span class="sxs-lookup"><span data-stu-id="c7285-1132">Info Field 2: Interface number.</span></span>
- <span data-ttu-id="c7285-1133">Bilgi alanı 3: parametre.</span><span class="sxs-lookup"><span data-stu-id="c7285-1133">Info Field 3: Parameter.</span></span>
- <span data-ttu-id="c7285-1134">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1134">Info Field 4: Not used.</span></span>

### <a name="device-stack-clear-feature"></a><span data-ttu-id="c7285-1135">Cihaz yığını temizleme özelliği</span><span class="sxs-lookup"><span data-stu-id="c7285-1135">Device Stack Clear Feature</span></span> 

#### <a name="ux_device_stack_clear_feature"></a><span data-ttu-id="c7285-1136">ux_device_stack_clear_feature</span><span class="sxs-lookup"><span data-stu-id="c7285-1136">ux_device_stack_clear_feature</span></span>

<span data-ttu-id="c7285-1137">**Simge** ![ Cihaz yığını temiz Özellik simgesi](./media/user-guide/usbx-events/image60.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1137">**Icon** ![Device Stack Clear Feature icon](./media/user-guide/usbx-events/image60.png)</span></span>

<span data-ttu-id="c7285-1138">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1138">**Description**</span></span>

<span data-ttu-id="c7285-1139">Bu olay bir USBX cihaz yığını temiz Özellik olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1139">This event represents a USBX Device Stack Clear Feature Event.</span></span>

<span data-ttu-id="c7285-1140">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1140">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1141">Bilgi alanı 1: Istek türü.</span><span class="sxs-lookup"><span data-stu-id="c7285-1141">Info Field 1: Request type.</span></span>
- <span data-ttu-id="c7285-1142">Bilgi alanı 2: Istek değeri.</span><span class="sxs-lookup"><span data-stu-id="c7285-1142">Info Field 2: Request value.</span></span> <span data-ttu-id="c7285-1143">Bilgi alanı 3: Istek dizini.</span><span class="sxs-lookup"><span data-stu-id="c7285-1143">Info Field 3: Request index.</span></span>
- <span data-ttu-id="c7285-1144">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1144">Info Field 4: Not used.</span></span>

### <a name="device-stack-configuration-get"></a><span data-ttu-id="c7285-1145">Cihaz yığını yapılandırmasını al</span><span class="sxs-lookup"><span data-stu-id="c7285-1145">Device Stack Configuration Get</span></span> 

#### <a name="ux_device_stack_configuration_get-t"></a><span data-ttu-id="c7285-1146">ux_device_stack_configuration_get t</span><span class="sxs-lookup"><span data-stu-id="c7285-1146">ux_device_stack_configuration_get t</span></span>

<span data-ttu-id="c7285-1147">**Simge** ![ Cihaz yığını yapılandırması Get simgesi](./media/user-guide/usbx-events/image61.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1147">**Icon** ![Device Stack Configuration Get icon](./media/user-guide/usbx-events/image61.png)</span></span>

<span data-ttu-id="c7285-1148">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1148">**Description**</span></span>

<span data-ttu-id="c7285-1149">Bu olay bir USBX cihaz yığını yapılandırma Get olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1149">This event represents a USBX Device Stack Configuration Get Event.</span></span>

<span data-ttu-id="c7285-1150">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1150">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-1151">Bilgi alanı 1: yapılandırma değeri.</span><span class="sxs-lookup"><span data-stu-id="c7285-1151">Info Field 1: Configuration value.</span></span>
- <span data-ttu-id="c7285-1152">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1152">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-1153">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1153">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1154">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1154">Info Field 4: Not used.</span></span>

### <a name="device-stack-configuration-set"></a><span data-ttu-id="c7285-1155">Cihaz yığını yapılandırma kümesi</span><span class="sxs-lookup"><span data-stu-id="c7285-1155">Device Stack Configuration Set</span></span> 

#### <a name="ux_device_stack_configuration_set"></a><span data-ttu-id="c7285-1156">ux_device_stack_configuration_set</span><span class="sxs-lookup"><span data-stu-id="c7285-1156">ux_device_stack_configuration_set</span></span>

<span data-ttu-id="c7285-1157">**Simge** ![ Cihaz yığını yapılandırma kümesi simgesi](./media/user-guide/usbx-events/image62.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1157">**Icon** ![Device Stack Configuration Set icon](./media/user-guide/usbx-events/image62.png)</span></span>

<span data-ttu-id="c7285-1158">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1158">**Description**</span></span>

<span data-ttu-id="c7285-1159">Bu olay bir USBX cihaz yığını yapılandırma kümesi olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1159">This event represents a USBX Device Stack Configuration Set Event.</span></span>

<span data-ttu-id="c7285-1160">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1160">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-1161">Bilgi alanı 1: yapılandırma değeri.</span><span class="sxs-lookup"><span data-stu-id="c7285-1161">Info Field 1: Configuration value.</span></span>
- <span data-ttu-id="c7285-1162">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1162">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-1163">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1163">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1164">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1164">Info Field 4: Not used.</span></span>

### <a name="device-stack-connect"></a><span data-ttu-id="c7285-1165">Cihaz yığını bağlantısı</span><span class="sxs-lookup"><span data-stu-id="c7285-1165">Device Stack Connect</span></span> 

#### <a name="ux_device_stack_connect"></a><span data-ttu-id="c7285-1166">ux_device_stack_connect</span><span class="sxs-lookup"><span data-stu-id="c7285-1166">ux_device_stack_connect</span></span>

<span data-ttu-id="c7285-1167">**Simge** ![ Cihaz yığını bağlantı simgesi](./media/user-guide/usbx-events/image63.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1167">**Icon** ![Device Stack Connect icon](./media/user-guide/usbx-events/image63.png)</span></span>

<span data-ttu-id="c7285-1168">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1168">**Description**</span></span>

<span data-ttu-id="c7285-1169">Bu olay bir USBX cihaz yığını tanımlayıcı gönderme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1169">This event represents a USBX Device Stack Descriptor Send Event.</span></span>

<span data-ttu-id="c7285-1170">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1170">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1171">Bilgi alanı 1: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1171">Info Field 1: Not used.</span></span>
- <span data-ttu-id="c7285-1172">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1172">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-1173">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1173">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1174">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1174">Info Field 4: Not used.</span></span>

### <a name="device-stack-descriptor-send"></a><span data-ttu-id="c7285-1175">Cihaz yığını tanımlayıcısı gönderme</span><span class="sxs-lookup"><span data-stu-id="c7285-1175">Device Stack Descriptor Send</span></span> 

#### <a name="ux_device_stack_descriptor_send"></a><span data-ttu-id="c7285-1176">ux_device_stack_descriptor_send</span><span class="sxs-lookup"><span data-stu-id="c7285-1176">ux_device_stack_descriptor_send</span></span>

<span data-ttu-id="c7285-1177">**Simge** ![ Cihaz yığını tanımlayıcısı gönderme simgesi](./media/user-guide/usbx-events/image64.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1177">**Icon** ![Device Stack Descriptor Send icon](./media/user-guide/usbx-events/image64.png)</span></span>

<span data-ttu-id="c7285-1178">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1178">**Description**</span></span>

<span data-ttu-id="c7285-1179">Bu olay bir USBX cihaz yığını tanımlayıcı gönderme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1179">This event represents a USBX Device Stack Descriptor Send Event.</span></span>

<span data-ttu-id="c7285-1180">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1180">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1181">Bilgi alanı 1: tanımlayıcı türü.</span><span class="sxs-lookup"><span data-stu-id="c7285-1181">Info Field 1: Descriptor type.</span></span>
- <span data-ttu-id="c7285-1182">Bilgi alanı 2: Istek dizini.</span><span class="sxs-lookup"><span data-stu-id="c7285-1182">Info Field 2: Request index.</span></span>
- <span data-ttu-id="c7285-1183">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1183">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1184">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1184">Info Field 4: Not used.</span></span>

### <a name="device-stack-disconnect"></a><span data-ttu-id="c7285-1185">Cihaz yığını bağlantısını kes</span><span class="sxs-lookup"><span data-stu-id="c7285-1185">Device Stack Disconnect</span></span> 

#### <a name="ux_device_stack_disconnect"></a><span data-ttu-id="c7285-1186">ux_device_stack_disconnect</span><span class="sxs-lookup"><span data-stu-id="c7285-1186">ux_device_stack_disconnect</span></span>

<span data-ttu-id="c7285-1187">**Simge** ![ Cihaz yığını bağlantı kesme simgesi](./media/user-guide/usbx-events/image65.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1187">**Icon** ![Device Stack Disconnect icon](./media/user-guide/usbx-events/image65.png)</span></span>

<span data-ttu-id="c7285-1188">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1188">**Description**</span></span>

<span data-ttu-id="c7285-1189">Bu olay bir USBX cihaz yığını bağlantı kesme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1189">This event represents a USBX Device Stack Disconnect Event.</span></span>

<span data-ttu-id="c7285-1190">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1190">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1191">Bilgi alanı 1: cihaz.</span><span class="sxs-lookup"><span data-stu-id="c7285-1191">Info Field 1: Device.</span></span>
- <span data-ttu-id="c7285-1192">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1192">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-1193">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1193">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1194">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1194">Info Field 4: Not used.</span></span>

### <a name="device-stack-endpoint-stall"></a><span data-ttu-id="c7285-1195">Cihaz yığını uç noktası kabini</span><span class="sxs-lookup"><span data-stu-id="c7285-1195">Device Stack Endpoint Stall</span></span> 

#### <a name="ux_device_stack_endpoint_stall"></a><span data-ttu-id="c7285-1196">ux_device_stack_endpoint_stall</span><span class="sxs-lookup"><span data-stu-id="c7285-1196">ux_device_stack_endpoint_stall</span></span>

<span data-ttu-id="c7285-1197">**Simge** ![ Cihaz yığını uç noktası kabin simgesi](./media/user-guide/usbx-events/image66.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1197">**Icon** ![Device Stack Endpoint Stall icon](./media/user-guide/usbx-events/image66.png)</span></span>

<span data-ttu-id="c7285-1198">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1198">**Description**</span></span>

<span data-ttu-id="c7285-1199">Bu olay bir USBX cihaz yığını uç nokta kabini olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1199">This event represents a USBX Device Stack Endpoint Stall Event.</span></span>

<span data-ttu-id="c7285-1200">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1200">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-1201">Bilgi alanı 1: uç nokta.</span><span class="sxs-lookup"><span data-stu-id="c7285-1201">Info Field 1: Endpoint.</span></span>
- <span data-ttu-id="c7285-1202">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1202">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-1203">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1203">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1204">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1204">Info Field 4: Not used.</span></span>

### <a name="device-stack-get-status"></a><span data-ttu-id="c7285-1205">Cihaz yığını Get durumu</span><span class="sxs-lookup"><span data-stu-id="c7285-1205">Device Stack Get Status</span></span> 

#### <a name="ux_device_stack_get_status"></a><span data-ttu-id="c7285-1206">ux_device_stack_get_status</span><span class="sxs-lookup"><span data-stu-id="c7285-1206">ux_device_stack_get_status</span></span>

<span data-ttu-id="c7285-1207">**Simge** ![ Cihaz yığını durum Al simgesi](./media/user-guide/usbx-events/image67.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1207">**Icon** ![Device Stack Get Status icon](./media/user-guide/usbx-events/image67.png)</span></span>

<span data-ttu-id="c7285-1208">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1208">**Description**</span></span>

<span data-ttu-id="c7285-1209">Bu olay bir USBX cihaz yığını al durum olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1209">This event represents a USBX Device Stack Get Status Event.</span></span>

<span data-ttu-id="c7285-1210">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1210">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1211">Bilgi alanı 1: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1211">Info Field 1: Not used.</span></span>
- <span data-ttu-id="c7285-1212">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1212">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-1213">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1213">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1214">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1214">Info Field 4: Not used.</span></span>

### <a name="device-stack-host-wakeup"></a><span data-ttu-id="c7285-1215">Cihaz yığını ana bilgisayarı uyandırma</span><span class="sxs-lookup"><span data-stu-id="c7285-1215">Device Stack Host Wakeup</span></span> 

#### <a name="ux_device_stack_host_wakeup"></a><span data-ttu-id="c7285-1216">ux_device_stack_host_wakeup</span><span class="sxs-lookup"><span data-stu-id="c7285-1216">ux_device_stack_host_wakeup</span></span>

<span data-ttu-id="c7285-1217">**Simge** ![ Cihaz yığını ana bilgisayarı uyandırma simgesi](./media/user-guide/usbx-events/image68.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1217">**Icon** ![Device Stack Host Wakeup icon](./media/user-guide/usbx-events/image68.png)</span></span>

<span data-ttu-id="c7285-1218">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1218">**Description**</span></span>

<span data-ttu-id="c7285-1219">Bu olay bir USBX cihaz yığını ana bilgisayarı uyandırma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1219">This event represents a USBX Device Stack Host Wakeup Event.</span></span>

<span data-ttu-id="c7285-1220">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1220">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-1221">Bilgi alanı 1: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1221">Info Field 1: Not used.</span></span>
- <span data-ttu-id="c7285-1222">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1222">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-1223">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1223">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1224">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1224">Info Field 4: Not used.</span></span>

### <a name="device-stack-initialize"></a><span data-ttu-id="c7285-1225">Cihaz yığını başlatma</span><span class="sxs-lookup"><span data-stu-id="c7285-1225">Device Stack Initialize</span></span> 

#### <a name="ux_device_stack_initialize"></a><span data-ttu-id="c7285-1226">ux_device_stack_initialize</span><span class="sxs-lookup"><span data-stu-id="c7285-1226">ux_device_stack_initialize</span></span>

<span data-ttu-id="c7285-1227">**Simge** ![ Cihaz yığını başlatma simgesi](./media/user-guide/usbx-events/image69.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1227">**Icon** ![Device Stack Initialize icon](./media/user-guide/usbx-events/image69.png)</span></span>

<span data-ttu-id="c7285-1228">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1228">**Description**</span></span>

<span data-ttu-id="c7285-1229">Bu olay bir USBX cihaz yığını başlatma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1229">This event represents a USBX Device Stack Initialize Event.</span></span>

<span data-ttu-id="c7285-1230">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1230">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-1231">Bilgi alanı 1: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1231">Info Field 1: Not used.</span></span>
- <span data-ttu-id="c7285-1232">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1232">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-1233">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1233">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1234">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1234">Info Field 4: Not used.</span></span>

### <a name="device-stack-interface-delete"></a><span data-ttu-id="c7285-1235">Cihaz yığını arabirimini silme</span><span class="sxs-lookup"><span data-stu-id="c7285-1235">Device Stack Interface Delete</span></span> 

#### <a name="ux_device_stack_interface_delete"></a><span data-ttu-id="c7285-1236">ux_device_stack_interface_delete</span><span class="sxs-lookup"><span data-stu-id="c7285-1236">ux_device_stack_interface_delete</span></span>

<span data-ttu-id="c7285-1237">**Simge** ![ Cihaz yığını arabirimi silme simgesi](./media/user-guide/usbx-events/image70.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1237">**Icon** ![Device Stack Interface Delete icon](./media/user-guide/usbx-events/image70.png)</span></span>

<span data-ttu-id="c7285-1238">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1238">**Description**</span></span>

<span data-ttu-id="c7285-1239">Bu olay bir USBX cihaz yığını arabirimi silme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1239">This event represents a USBX Device Stack Interface Delete Event.</span></span>

<span data-ttu-id="c7285-1240">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1240">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1241">Bilgi alanı 1: arabirim.</span><span class="sxs-lookup"><span data-stu-id="c7285-1241">Info Field 1: Interface.</span></span>
- <span data-ttu-id="c7285-1242">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1242">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-1243">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1243">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1244">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1244">Info Field 4: Not used.</span></span>

### <a name="device-stack-interface-get"></a><span data-ttu-id="c7285-1245">Cihaz yığını arabirimi al</span><span class="sxs-lookup"><span data-stu-id="c7285-1245">Device Stack Interface Get</span></span> 

#### <a name="ux_device_stack_interface_get"></a><span data-ttu-id="c7285-1246">ux_device_stack_interface_get</span><span class="sxs-lookup"><span data-stu-id="c7285-1246">ux_device_stack_interface_get</span></span>

<span data-ttu-id="c7285-1247">**Simge** ![ Cihaz yığını arabirimi al simgesi](./media/user-guide/usbx-events/image71.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1247">**Icon** ![Device Stack Interface Get icon](./media/user-guide/usbx-events/image71.png)</span></span>

<span data-ttu-id="c7285-1248">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1248">**Description**</span></span>

<span data-ttu-id="c7285-1249">Bu olay bir USBX cihaz yığını arabirimi Get olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1249">This event represents a USBX Device Stack Interface Get Event.</span></span>

<span data-ttu-id="c7285-1250">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1250">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-1251">Bilgi alanı 1: arabirim değeri.</span><span class="sxs-lookup"><span data-stu-id="c7285-1251">Info Field 1: Interface value.</span></span>
- <span data-ttu-id="c7285-1252">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1252">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-1253">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1253">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1254">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1254">Info Field 4: Not used.</span></span>

### <a name="device-stack-interface-set"></a><span data-ttu-id="c7285-1255">Cihaz yığını arabirim kümesi</span><span class="sxs-lookup"><span data-stu-id="c7285-1255">Device Stack Interface Set</span></span> 

#### <a name="ux_device_stack_interface_set"></a><span data-ttu-id="c7285-1256">ux_device_stack_interface_set</span><span class="sxs-lookup"><span data-stu-id="c7285-1256">ux_device_stack_interface_set</span></span>

<span data-ttu-id="c7285-1257">**Simge** ![ Cihaz yığını arabirim kümesi simgesi](./media/user-guide/usbx-events/image72.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1257">**Icon** ![Device Stack Interface Set icon](./media/user-guide/usbx-events/image72.png)</span></span>

<span data-ttu-id="c7285-1258">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1258">**Description**</span></span>

<span data-ttu-id="c7285-1259">Bu olay bir USBX cihaz yığını arabirim kümesi olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1259">This event represents a USBX Device Stack Interface Set Event.</span></span>

<span data-ttu-id="c7285-1260">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1260">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-1261">Bilgi alanı 1: Istek değeri.</span><span class="sxs-lookup"><span data-stu-id="c7285-1261">Info Field 1: Request value.</span></span> <span data-ttu-id="c7285-1262">Bilgi alanı 2: Istek dizini.</span><span class="sxs-lookup"><span data-stu-id="c7285-1262">Info Field 2: Request index.</span></span>
- <span data-ttu-id="c7285-1263">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1263">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1264">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1264">Info Field 4: Not used.</span></span>

### <a name="device-stack-set-feature"></a><span data-ttu-id="c7285-1265">Cihaz yığını kümesi özelliği</span><span class="sxs-lookup"><span data-stu-id="c7285-1265">Device Stack Set Feature</span></span> 

#### <a name="ux_device_stack_set_feature"></a><span data-ttu-id="c7285-1266">ux_device_stack_set_feature</span><span class="sxs-lookup"><span data-stu-id="c7285-1266">ux_device_stack_set_feature</span></span>

<span data-ttu-id="c7285-1267">**Simge** ![ Cihaz yığını kümesi özellik simgesi](./media/user-guide/usbx-events/image73.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1267">**Icon** ![Device Stack Set Feature icon](./media/user-guide/usbx-events/image73.png)</span></span>

<span data-ttu-id="c7285-1268">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1268">**Description**</span></span>

<span data-ttu-id="c7285-1269">Bu olay bir USBX cihaz yığını kümesi özelliği olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1269">This event represents a USBX Device Stack Set Feature Event.</span></span>

<span data-ttu-id="c7285-1270">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1270">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-1271">Bilgi alanı 1: Istek değeri.</span><span class="sxs-lookup"><span data-stu-id="c7285-1271">Info Field 1: Request value.</span></span> <span data-ttu-id="c7285-1272">Bilgi alanı 2: Istek dizini.</span><span class="sxs-lookup"><span data-stu-id="c7285-1272">Info Field 2: Request index.</span></span>
- <span data-ttu-id="c7285-1273">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1273">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1274">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1274">Info Field 4: Not used.</span></span>

### <a name="device-stack-transfer-abort"></a><span data-ttu-id="c7285-1275">Cihaz yığını aktarımı Iptali</span><span class="sxs-lookup"><span data-stu-id="c7285-1275">Device Stack Transfer Abort</span></span> 

#### <a name="ux_device_stack_transfer_abort"></a><span data-ttu-id="c7285-1276">ux_device_stack_transfer_abort</span><span class="sxs-lookup"><span data-stu-id="c7285-1276">ux_device_stack_transfer_abort</span></span>

<span data-ttu-id="c7285-1277">**Simge** ![ Cihaz yığını aktarım Iptali simgesi](./media/user-guide/usbx-events/image74.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1277">**Icon** ![Device Stack Transfer Abort icon](./media/user-guide/usbx-events/image74.png)</span></span>

<span data-ttu-id="c7285-1278">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1278">**Description**</span></span>

<span data-ttu-id="c7285-1279">Bu olay bir USBX cihaz yığını aktarımı Iptali olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1279">This event represents a USBX Device Stack Transfer Abort Event.</span></span>

<span data-ttu-id="c7285-1280">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1280">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-1281">Bilgi alanı 1: aktarım isteği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1281">Info Field 1: Transfer request.</span></span>
- <span data-ttu-id="c7285-1282">Bilgi alanı 2: tamamlanma kodu.</span><span class="sxs-lookup"><span data-stu-id="c7285-1282">Info Field 2: Completion code.</span></span>
- <span data-ttu-id="c7285-1283">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1283">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1284">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1284">Info Field 4: Not used.</span></span>

### <a name="device-stack-transfer-all-request-abort"></a><span data-ttu-id="c7285-1285">Cihaz yığın aktarımı tüm Istek Iptali</span><span class="sxs-lookup"><span data-stu-id="c7285-1285">Device Stack Transfer All Request Abort</span></span> 

#### <a name="ux_device_stack_transfer_all_request_abort"></a><span data-ttu-id="c7285-1286">ux_device_stack_transfer_all_request_abort</span><span class="sxs-lookup"><span data-stu-id="c7285-1286">ux_device_stack_transfer_all_request_abort</span></span>

<span data-ttu-id="c7285-1287">**Simge** ![ Cihaz yığını tüm Isteği Iptal et simgesi](./media/user-guide/usbx-events/image75.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1287">**Icon** ![Device Stack Transfer All Request Abort icon](./media/user-guide/usbx-events/image75.png)</span></span>

<span data-ttu-id="c7285-1288">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1288">**Description**</span></span>

<span data-ttu-id="c7285-1289">Bu olay, tüm Istek Iptali olayını aktar bir USBX cihaz yığınını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1289">This event represents a USBX Device Stack Transfer All Request Abort Event.</span></span>

<span data-ttu-id="c7285-1290">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1290">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-1291">Bilgi alanı 1: uç nokta.</span><span class="sxs-lookup"><span data-stu-id="c7285-1291">Info Field 1: Endpoint.</span></span>
- <span data-ttu-id="c7285-1292">Bilgi alanı 2: tamamlanma kodu.</span><span class="sxs-lookup"><span data-stu-id="c7285-1292">Info Field 2: Completion code.</span></span>
- <span data-ttu-id="c7285-1293">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1293">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1294">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1294">Info Field 4: Not used.</span></span>

### <a name="device-stack-transfer-request"></a><span data-ttu-id="c7285-1295">Cihaz yığını aktarım Isteği</span><span class="sxs-lookup"><span data-stu-id="c7285-1295">Device Stack Transfer Request</span></span> 

#### <a name="ux_device_stack_transfer_request"></a><span data-ttu-id="c7285-1296">ux_device_stack_transfer_request</span><span class="sxs-lookup"><span data-stu-id="c7285-1296">ux_device_stack_transfer_request</span></span>

<span data-ttu-id="c7285-1297">**Simge** ![ Cihaz yığını aktarım Isteği simgesi](./media/user-guide/usbx-events/image76.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1297">**Icon** ![Device Stack Transfer Request icon](./media/user-guide/usbx-events/image76.png)</span></span>

<span data-ttu-id="c7285-1298">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1298">**Description**</span></span>

<span data-ttu-id="c7285-1299">Bu olay bir USBX cihaz yığını aktarım Isteği olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1299">This event represents a USBX Device Stack Transfer Request Event.</span></span>

<span data-ttu-id="c7285-1300">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1300">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1301">Bilgi alanı 1: aktarım isteği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1301">Info Field 1: Transfer request.</span></span>
- <span data-ttu-id="c7285-1302">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1302">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-1303">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1303">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1304">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1304">Info Field 4: Not used.</span></span>

### <a name="host-class-asix-activate"></a><span data-ttu-id="c7285-1305">Ana bilgisayar sınıfı Aaltıetkinleştir</span><span class="sxs-lookup"><span data-stu-id="c7285-1305">Host Class Asix Activate</span></span> 

#### <a name="ux_host_class_asix_activate"></a><span data-ttu-id="c7285-1306">ux_host_class_asix_activate</span><span class="sxs-lookup"><span data-stu-id="c7285-1306">ux_host_class_asix_activate</span></span>

<span data-ttu-id="c7285-1307">**Simge** ![ Ana bilgisayar sınıfı ASIX etkinleştir simgesi](./media/user-guide/usbx-events/image77.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1307">**Icon** ![Host Class Asix Activate icon](./media/user-guide/usbx-events/image77.png)</span></span>

<span data-ttu-id="c7285-1308">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1308">**Description**</span></span>

<span data-ttu-id="c7285-1309">Bu olay, bir USBX konak sınıfının Aaltıyı Etkinleştirünü temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1309">This event represents a USBX Host Class Asix Activate.</span></span>

<span data-ttu-id="c7285-1310">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1310">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1311">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1311">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-1312">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1312">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-1313">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1313">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1314">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1314">Info Field 4: Not used.</span></span>

### <a name="host-class-asix-deactivate"></a><span data-ttu-id="c7285-1315">Ana makine sınıfı ASIX devre dışı</span><span class="sxs-lookup"><span data-stu-id="c7285-1315">Host Class Asix Deactivate</span></span> 

#### <a name="ux_host_class_asix_deactivate"></a><span data-ttu-id="c7285-1316">ux_host_class_asix_deactivate</span><span class="sxs-lookup"><span data-stu-id="c7285-1316">ux_host_class_asix_deactivate</span></span>

<span data-ttu-id="c7285-1317">**Simge** ![ Ana makine sınıfı ASIX devre dışı simgesi](./media/user-guide/usbx-events/image78.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1317">**Icon** ![Host Class Asix Deactivate icon](./media/user-guide/usbx-events/image78.png)</span></span>

<span data-ttu-id="c7285-1318">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1318">**Description**</span></span>

<span data-ttu-id="c7285-1319">Bu olay bir USBX konak sınıfının bir adet devre dışı bırakma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1319">This event represents a USBX Host Class Asix Deactivate Event.</span></span>

<span data-ttu-id="c7285-1320">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1320">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-1321">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1321">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-1322">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1322">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-1323">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1323">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1324">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1324">Info Field 4: Not used.</span></span>

### <a name="host-class-asix-interrupt-notification"></a><span data-ttu-id="c7285-1325">Ana bilgisayar sınıfı asix kesme bildirimi</span><span class="sxs-lookup"><span data-stu-id="c7285-1325">Host Class Asix Interrupt Notification</span></span> 

#### <a name="ux_host_class_asix_interrupt_notification"></a><span data-ttu-id="c7285-1326">ux_host_class_asix_interrupt_notification</span><span class="sxs-lookup"><span data-stu-id="c7285-1326">ux_host_class_asix_interrupt_notification</span></span>

<span data-ttu-id="c7285-1327">**Simge** ![ Ana bilgisayar sınıfı Aaltıkesme bildirimi simgesi](./media/user-guide/usbx-events/image79.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1327">**Icon** ![Host Class Asix Interrupt Notification icon](./media/user-guide/usbx-events/image79.png)</span></span>

<span data-ttu-id="c7285-1328">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1328">**Description**</span></span>

<span data-ttu-id="c7285-1329">Bu olay bir USBX konak sınıfının asix kesme bildirimi olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1329">This event represents a USBX Host Class Asix Interrupt Notification Event.</span></span>

<span data-ttu-id="c7285-1330">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1330">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1331">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1331">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-1332">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1332">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-1333">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1333">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1334">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1334">Info Field 4: Not used.</span></span>

### <a name="host-class-asix-read"></a><span data-ttu-id="c7285-1335">Ana bilgisayar sınıfı Aaltıokuma</span><span class="sxs-lookup"><span data-stu-id="c7285-1335">Host Class Asix Read</span></span> 

#### <a name="ux_host_class_asix_read"></a><span data-ttu-id="c7285-1336">ux_host_class_asix_read</span><span class="sxs-lookup"><span data-stu-id="c7285-1336">ux_host_class_asix_read</span></span>

<span data-ttu-id="c7285-1337">**Simge** ![ Ana bilgisayar sınıfı Aaltıoku simgesi](./media/user-guide/usbx-events/image80.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1337">**Icon** ![Host Class Asix Read icon](./media/user-guide/usbx-events/image80.png)</span></span>

<span data-ttu-id="c7285-1338">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1338">**Description**</span></span>

<span data-ttu-id="c7285-1339">Bu olay bir USBX konak sınıfının Aaltıoku olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1339">This event represents a USBX Host Class Asix Read Event.</span></span>

<span data-ttu-id="c7285-1340">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1340">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-1341">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1341">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1342">Bilgi alanı 2: veri işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c7285-1342">Info Field 2: Data pointer.</span></span>
- <span data-ttu-id="c7285-1343">Bilgi alanı 3: Istenen uzunluk.</span><span class="sxs-lookup"><span data-stu-id="c7285-1343">Info Field 3: Requested length.</span></span>
- <span data-ttu-id="c7285-1344">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1344">Info Field 4: Not used.</span></span>

### <a name="host-class-asix-write"></a><span data-ttu-id="c7285-1345">Ana bilgisayar sınıfı Aaltıyaz</span><span class="sxs-lookup"><span data-stu-id="c7285-1345">Host Class Asix Write</span></span> 

#### <a name="ux_host_class_asix_write"></a><span data-ttu-id="c7285-1346">ux_host_class_asix_write</span><span class="sxs-lookup"><span data-stu-id="c7285-1346">ux_host_class_asix_write</span></span>

<span data-ttu-id="c7285-1347">**Simge** ![ Ana bilgisayar sınıfı Aaltıyaz simgesi](./media/user-guide/usbx-events/image81.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1347">**Icon** ![Host Class Asix Write icon](./media/user-guide/usbx-events/image81.png)</span></span>

<span data-ttu-id="c7285-1348">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1348">**Description**</span></span>

<span data-ttu-id="c7285-1349">Bu olay, bir USBX ana bilgisayar sınıfının altı adet yazma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1349">This event represents a USBX Host Class Asix Write Event.</span></span>

<span data-ttu-id="c7285-1350">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1350">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-1351">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1351">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1352">Bilgi alanı 2: veri işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c7285-1352">Info Field 2: Data pointer.</span></span>
- <span data-ttu-id="c7285-1353">Bilgi alanı 3: Istenen uzunluk.</span><span class="sxs-lookup"><span data-stu-id="c7285-1353">Info Field 3: Requested length.</span></span>
- <span data-ttu-id="c7285-1354">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1354">Info Field 4: Not used.</span></span>

### <a name="host-class-audio-activate"></a><span data-ttu-id="c7285-1355">Konak sınıfı ses etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="c7285-1355">Host Class Audio Activate</span></span> 

#### <a name="ux_host_class_audio_activate"></a><span data-ttu-id="c7285-1356">ux_host_class_audio_activate</span><span class="sxs-lookup"><span data-stu-id="c7285-1356">ux_host_class_audio_activate</span></span>

<span data-ttu-id="c7285-1357">**Simge** ![ Konak sınıfı ses etkinleştirme simgesi](./media/user-guide/usbx-events/image82.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1357">**Icon** ![Host Class Audio Activate icon](./media/user-guide/usbx-events/image82.png)</span></span>

<span data-ttu-id="c7285-1358">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1358">**Description**</span></span>

<span data-ttu-id="c7285-1359">Bu olay bir USBX konak sınıfı ses etkinleştirme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1359">This event represents a USBX Host Class Audio Activate Event.</span></span>

<span data-ttu-id="c7285-1360">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1360">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-1361">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1361">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1362">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1362">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-1363">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1363">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1364">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1364">Info Field 4: Not used.</span></span>

### <a name="host-class-audio-control-value-get"></a><span data-ttu-id="c7285-1365">Konak sınıfı ses denetimi değeri Al</span><span class="sxs-lookup"><span data-stu-id="c7285-1365">Host Class Audio Control Value Get</span></span> 

#### <a name="ux_host_class_audio_control_value_get"></a><span data-ttu-id="c7285-1366">ux_host_class_audio_control_value_get</span><span class="sxs-lookup"><span data-stu-id="c7285-1366">ux_host_class_audio_control_value_get</span></span>

<span data-ttu-id="c7285-1367">**Simge** ![ Konak sınıfı ses denetimi değeri Al simgesi](./media/user-guide/usbx-events/image83.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1367">**Icon** ![Host Class Audio Control Value Get icon](./media/user-guide/usbx-events/image83.png)</span></span>

<span data-ttu-id="c7285-1368">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1368">**Description**</span></span>

<span data-ttu-id="c7285-1369">Bu olay bir USBX konak sınıfı ses denetim değeri Al olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1369">This event represents a USBX Host Class Audio Control Value Get Event.</span></span>

<span data-ttu-id="c7285-1370">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1370">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-1371">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1371">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1372">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1372">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-1373">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1373">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1374">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1374">Info Field 4: Not used.</span></span>

### <a name="host-class-audio-control-value-set"></a><span data-ttu-id="c7285-1375">Konak sınıfı ses denetimi değer kümesi</span><span class="sxs-lookup"><span data-stu-id="c7285-1375">Host Class Audio Control Value Set</span></span> 

#### <a name="ux_host_class_audio_control_value_set"></a><span data-ttu-id="c7285-1376">ux_host_class_audio_control_value_set</span><span class="sxs-lookup"><span data-stu-id="c7285-1376">ux_host_class_audio_control_value_set</span></span>

<span data-ttu-id="c7285-1377">**Simge** ![ Konak sınıfı ses denetimi değer kümesi simgesi](./media/user-guide/usbx-events/image84.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1377">**Icon** ![Host Class Audio Control Value Set icon](./media/user-guide/usbx-events/image84.png)</span></span>

<span data-ttu-id="c7285-1378">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1378">**Description**</span></span>

<span data-ttu-id="c7285-1379">Bu olay, bir iç NetX g/ç sürücüsü ertelenmiş işleme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1379">This event represents an internal NetX I/O driver deferred processing event.</span></span>

<span data-ttu-id="c7285-1380">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1380">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-1381">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1381">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1382">Bilgi alanı 2: ses denetimi.</span><span class="sxs-lookup"><span data-stu-id="c7285-1382">Info Field 2: Audio control.</span></span>
- <span data-ttu-id="c7285-1383">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1383">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1384">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1384">Info Field 4: Not used.</span></span>

### <a name="host-class-audio-deactivate"></a><span data-ttu-id="c7285-1385">Konak sınıfı ses etkinliğini kaldırma</span><span class="sxs-lookup"><span data-stu-id="c7285-1385">Host Class Audio Deactivate</span></span> 

#### <a name="ux_host_class_audio_deactivate"></a><span data-ttu-id="c7285-1386">ux_host_class_audio_deactivate</span><span class="sxs-lookup"><span data-stu-id="c7285-1386">ux_host_class_audio_deactivate</span></span>

<span data-ttu-id="c7285-1387">**Simge** ![ Konak sınıfı ses devre dışı bırakma simgesi](./media/user-guide/usbx-events/image85.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1387">**Icon** ![Host Class Audio Deactivate icon](./media/user-guide/usbx-events/image85.png)</span></span>

<span data-ttu-id="c7285-1388">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1388">**Description**</span></span>

<span data-ttu-id="c7285-1389">Bu olay bir USBX konak sınıfı sesi devre dışı bırakma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1389">This event represents a USBX Host Class Audio Deactivate Event.</span></span>

<span data-ttu-id="c7285-1390">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1390">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-1391">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1391">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1392">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1392">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-1393">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1393">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1394">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1394">Info Field 4: Not used.</span></span>

### <a name="host-class-audio-read"></a><span data-ttu-id="c7285-1395">Konak sınıfı ses okuma</span><span class="sxs-lookup"><span data-stu-id="c7285-1395">Host Class Audio Read</span></span> 

#### <a name="ux_host_class_audio_read"></a><span data-ttu-id="c7285-1396">ux_host_class_audio_read</span><span class="sxs-lookup"><span data-stu-id="c7285-1396">ux_host_class_audio_read</span></span>

<span data-ttu-id="c7285-1397">**Simge** ![ Konak sınıfı ses okuma simgesi](./media/user-guide/usbx-events/image86.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1397">**Icon** ![Host Class Audio Read icon](./media/user-guide/usbx-events/image86.png)</span></span>

<span data-ttu-id="c7285-1398">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1398">**Description**</span></span>

<span data-ttu-id="c7285-1399">Bu olay bir USBX konak sınıfı ses okuma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1399">This event represents a USBX Host Class Audio Read Event.</span></span>

- <span data-ttu-id="c7285-1400">Bilgi alanları</span><span class="sxs-lookup"><span data-stu-id="c7285-1400">Information Fields</span></span> 
- <span data-ttu-id="c7285-1401">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1401">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1402">Bilgi alanı 2: veri işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c7285-1402">Info Field 2: Data pointer.</span></span>
- <span data-ttu-id="c7285-1403">Bilgi alanı 3: Istenen uzunluk.</span><span class="sxs-lookup"><span data-stu-id="c7285-1403">Info Field 3: Requested length.</span></span>
- <span data-ttu-id="c7285-1404">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1404">Info Field 4: Not used.</span></span>

### <a name="host-class-audio-streaming-sampling-get"></a><span data-ttu-id="c7285-1405">Konak sınıfı ses akışı örneklemesi alma</span><span class="sxs-lookup"><span data-stu-id="c7285-1405">Host Class Audio Streaming Sampling Get</span></span> 

#### <a name="ux_host_class_audio_streaming_sampling_get"></a><span data-ttu-id="c7285-1406">ux_host_class_audio_streaming_sampling_get</span><span class="sxs-lookup"><span data-stu-id="c7285-1406">ux_host_class_audio_streaming_sampling_get</span></span>

<span data-ttu-id="c7285-1407">**Simge** ![ Konak sınıfı ses akışı örneklemesi alma simgesi](./media/user-guide/usbx-events/image87.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1407">**Icon** ![Host Class Audio Streaming Sampling Get icon](./media/user-guide/usbx-events/image87.png)</span></span>

<span data-ttu-id="c7285-1408">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1408">**Description**</span></span>

<span data-ttu-id="c7285-1409">Bu olay bir USBX konak sınıfı ses akışı örnekleme Get olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1409">This event represents a USBX Host Class Audio Streaming Sampling Get Event.</span></span>

<span data-ttu-id="c7285-1410">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1410">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-1411">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1411">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1412">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1412">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-1413">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1413">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1414">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1414">Info Field 4: Not used.</span></span>

### <a name="host-class-audio-streaming-sampling-set"></a><span data-ttu-id="c7285-1415">Konak sınıfı ses akışı örnekleme kümesi</span><span class="sxs-lookup"><span data-stu-id="c7285-1415">Host Class Audio Streaming Sampling Set</span></span> 

#### <a name="ux_host_class_audio_streaming_sampling_set"></a><span data-ttu-id="c7285-1416">ux_host_class_audio_streaming_sampling_set</span><span class="sxs-lookup"><span data-stu-id="c7285-1416">ux_host_class_audio_streaming_sampling_set</span></span>

<span data-ttu-id="c7285-1417">**Simge** ![ Konak sınıfı ses akışı örnekleme kümesi simgesi](./media/user-guide/usbx-events/image88.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1417">**Icon** ![Host Class Audio Streaming Sampling Set icon](./media/user-guide/usbx-events/image88.png)</span></span>

<span data-ttu-id="c7285-1418">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1418">**Description**</span></span>

<span data-ttu-id="c7285-1419">Bu olay bir USBX konak sınıfı ses akışı örnekleme kümesi olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1419">This event represents a USBX Host Class Audio Streaming Sampling Set Event.</span></span>

<span data-ttu-id="c7285-1420">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1420">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-1421">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1421">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1422">Bilgi alanı 2: ses örnekleme.</span><span class="sxs-lookup"><span data-stu-id="c7285-1422">Info Field 2: Audio Sampling.</span></span>
- <span data-ttu-id="c7285-1423">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1423">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1424">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1424">Info Field 4: Not used.</span></span>

### <a name="host-class-audio-write"></a><span data-ttu-id="c7285-1425">Konak sınıfı ses yazma</span><span class="sxs-lookup"><span data-stu-id="c7285-1425">Host Class Audio Write</span></span> 

#### <a name="ux_host_class_audio_write"></a><span data-ttu-id="c7285-1426">ux_host_class_audio_write</span><span class="sxs-lookup"><span data-stu-id="c7285-1426">ux_host_class_audio_write</span></span>

<span data-ttu-id="c7285-1427">**Simge** ![ Konak sınıfı ses yazma simgesi](./media/user-guide/usbx-events/image89.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1427">**Icon** ![Host Class Audio Write icon](./media/user-guide/usbx-events/image89.png)</span></span>

<span data-ttu-id="c7285-1428">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1428">**Description**</span></span>

<span data-ttu-id="c7285-1429">Bu olay bir USBX konak sınıfı ses yazma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1429">This event represents a USBX Host Class Audio Write Event.</span></span>

<span data-ttu-id="c7285-1430">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1430">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-1431">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1431">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1432">Bilgi alanı 2: veri işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c7285-1432">Info Field 2: Data pointer.</span></span>
- <span data-ttu-id="c7285-1433">Bilgi alanı 3: Istenen uzunluk.</span><span class="sxs-lookup"><span data-stu-id="c7285-1433">Info Field 3: Requested length.</span></span>
- <span data-ttu-id="c7285-1434">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1434">Info Field 4: Not used.</span></span>

### <a name="host-class-cdc-acm-activate"></a><span data-ttu-id="c7285-1435">Ana bilgisayar sınıfı CDC ACM Activate</span><span class="sxs-lookup"><span data-stu-id="c7285-1435">Host Class Cdc Acm Activate</span></span> 

#### <a name="ux_host_class_cdc_acm_activate"></a><span data-ttu-id="c7285-1436">ux_host_class_cdc_acm_activate</span><span class="sxs-lookup"><span data-stu-id="c7285-1436">ux_host_class_cdc_acm_activate</span></span>

<span data-ttu-id="c7285-1437">**Simge** ![ Ana bilgisayar sınıfı C D C A C M etkinleştirme simgesi](./media/user-guide/usbx-events/image90.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1437">**Icon** ![Host Class C D C A C M Activate icon](./media/user-guide/usbx-events/image90.png)</span></span>

<span data-ttu-id="c7285-1438">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1438">**Description**</span></span>

<span data-ttu-id="c7285-1439">Bu olay bir USBX konak sınıfı CDC ACM Activate olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1439">This event represents a USBX Host Class Cdc Acm Activate Event.</span></span>

<span data-ttu-id="c7285-1440">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1440">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1441">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1441">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1442">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1442">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-1443">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1443">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1444">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1444">Info Field 4: Not used.</span></span>

### <a name="host-class-cdc-acm-deactivate"></a><span data-ttu-id="c7285-1445">Ana bilgisayar sınıfı CDC ACM Deactivate</span><span class="sxs-lookup"><span data-stu-id="c7285-1445">Host Class Cdc Acm Deactivate</span></span> 

#### <a name="ux_host_class_cdc_acm_deactivate"></a><span data-ttu-id="c7285-1446">ux_host_class_cdc_acm_deactivate</span><span class="sxs-lookup"><span data-stu-id="c7285-1446">ux_host_class_cdc_acm_deactivate</span></span>

<span data-ttu-id="c7285-1447">**Simge** ![ Ana bilgisayar sınıfı C D C A C M devre dışı bırakma simgesi](./media/user-guide/usbx-events/image91.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1447">**Icon** ![Host Class C D C A C M Deactivate icon](./media/user-guide/usbx-events/image91.png)</span></span>

<span data-ttu-id="c7285-1448">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1448">**Description**</span></span>

<span data-ttu-id="c7285-1449">Bu olay bir USBX konak sınıfı CDC ACM Deactivate olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1449">This event represents a USBX Host Class Cdc Acm Deactivate Event.</span></span>

<span data-ttu-id="c7285-1450">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1450">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-1451">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1451">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1452">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1452">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-1453">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1453">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1454">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1454">Info Field 4: Not used.</span></span>

### <a name="host-class-cdc-acm-ioctl-abort-in-pipe"></a><span data-ttu-id="c7285-1455">Ana bilgisayar sınıfı CDC ACM IOCTL Iptal kanalı</span><span class="sxs-lookup"><span data-stu-id="c7285-1455">Host Class Cdc Acm Ioctl Abort In Pipe</span></span> 

#### <a name="ux_host_class_cdc_acm_ioctl_abort_in_pipe"></a><span data-ttu-id="c7285-1456">ux_host_class_cdc_acm_ioctl_abort_in_pipe</span><span class="sxs-lookup"><span data-stu-id="c7285-1456">ux_host_class_cdc_acm_ioctl_abort_in_pipe</span></span>

<span data-ttu-id="c7285-1457">**Simge** ![ Ana bilgisayar sınıfı C D C c](./media/user-guide/usbx-events/image92.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1457">**Icon** ![Host Class C D C A C M I O C T L Abort In Pipe icon](./media/user-guide/usbx-events/image92.png)</span></span>

<span data-ttu-id="c7285-1458">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1458">**Description**</span></span>

<span data-ttu-id="c7285-1459">Bu olay, kanal olayında bir USBX konak sınıfını CDC ACM IOCTL Iptali ' ni temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1459">This event represents a USBX Host Class Cdc Acm Ioctl Abort In Pipe Event.</span></span>

<span data-ttu-id="c7285-1460">Bilgi alanları</span><span class="sxs-lookup"><span data-stu-id="c7285-1460">Information Fields</span></span> 

- <span data-ttu-id="c7285-1461">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1461">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1462">Bilgi alanı 2: uç nokta.</span><span class="sxs-lookup"><span data-stu-id="c7285-1462">Info Field 2: Endpoint.</span></span>
- <span data-ttu-id="c7285-1463">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1463">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1464">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1464">Info Field 4: Not used.</span></span>

### <a name="host-class-cdc-acm-ioctl-abort-out-pipe"></a><span data-ttu-id="c7285-1465">Ana bilgisayar sınıfı CDC ACM IOCTL durdurma kanalı</span><span class="sxs-lookup"><span data-stu-id="c7285-1465">Host Class Cdc Acm Ioctl Abort Out Pipe</span></span> 

#### <a name="ux_host_class_cdc_acm_ioct_abort_out_pipe"></a><span data-ttu-id="c7285-1466">ux_host_class_cdc_acm_ioct_abort_out_pipe</span><span class="sxs-lookup"><span data-stu-id="c7285-1466">ux_host_class_cdc_acm_ioct_abort_out_pipe</span></span>

<span data-ttu-id="c7285-1467">**Simge** ! [[Ana bilgisayar sınıfı c D c a c m I ı c T ı Durdur kanal simgesi](./media/user-guide/usbx-events/image93.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1467">**Icon** ![[Host Class C D C A C M I O C T L Abort Out Pipe icon](./media/user-guide/usbx-events/image93.png)</span></span>

<span data-ttu-id="c7285-1468">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1468">**Description**</span></span>

<span data-ttu-id="c7285-1469">Bu olay, bir USBX konak sınıfını CDC ACM IOCTL Abort Out kanal olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1469">This event represents a USBX Host Class Cdc Acm Ioctl Abort Out Pipe Event.</span></span>

<span data-ttu-id="c7285-1470">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1470">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-1471">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1471">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1472">Bilgi alanı 2: uç nokta.</span><span class="sxs-lookup"><span data-stu-id="c7285-1472">Info Field 2: Endpoint.</span></span>
- <span data-ttu-id="c7285-1473">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1473">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1474">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1474">Info Field 4: Not used.</span></span>

### <a name="host-class-cdc-acm-ioctl-get-device-status"></a><span data-ttu-id="c7285-1475">Ana bilgisayar sınıfı CDC ACM IOCTL cihaz durumunu al</span><span class="sxs-lookup"><span data-stu-id="c7285-1475">Host Class Cdc Acm Ioctl Get Device Status</span></span> 

#### <a name="ux_host_class_cdc_acm_ioctl_get_device_status"></a><span data-ttu-id="c7285-1476">ux_host_class_cdc_acm_ioctl_get_device_status</span><span class="sxs-lookup"><span data-stu-id="c7285-1476">ux_host_class_cdc_acm_ioctl_get_device_status</span></span>

<span data-ttu-id="c7285-1477">**Simge** ![ Ana bilgisayar sınıfı C D C A C M ı O C T I cihaz durum simgesi al](./media/user-guide/usbx-events/image94.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1477">**Icon** ![Host Class C D C A C M I O C T L Get Device Status icon](./media/user-guide/usbx-events/image94.png)</span></span>

<span data-ttu-id="c7285-1478">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1478">**Description**</span></span>

<span data-ttu-id="c7285-1479">Bu olay bir USBX konak sınıfı CDC ACM IOCTL Get cihaz durumu olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1479">This event represents a USBX Host Class Cdc Acm Ioctl Get Device Status Event.</span></span>

<span data-ttu-id="c7285-1480">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1480">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-1481">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1481">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1482">Bilgi alanı 2: cihaz durumu.</span><span class="sxs-lookup"><span data-stu-id="c7285-1482">Info Field 2: Device status.</span></span>
- <span data-ttu-id="c7285-1483">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1483">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1484">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1484">Info Field 4: Not used.</span></span>

### <a name="host-class-cdc-acm-ioctl-get-line-coding"></a><span data-ttu-id="c7285-1485">Ana bilgisayar sınıfı CDC ACM IOCTL al satırı kodlama</span><span class="sxs-lookup"><span data-stu-id="c7285-1485">Host Class Cdc Acm Ioctl Get Line Coding</span></span> 

#### <a name="ux_host_class_cdc_acm_ioctl_get_line_coding"></a><span data-ttu-id="c7285-1486">ux_host_class_cdc_acm_ioctl_get_line_coding</span><span class="sxs-lookup"><span data-stu-id="c7285-1486">ux_host_class_cdc_acm_ioctl_get_line_coding</span></span>

<span data-ttu-id="c7285-1487">**Simge** ![ Ana bilgisayar sınıfı C D C A C M ı O C T m](./media/user-guide/usbx-events/image95.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1487">**Icon** ![Host Class C D C A C M I O C T L Get Line Coding icon](./media/user-guide/usbx-events/image95.png)</span></span>

<span data-ttu-id="c7285-1488">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1488">**Description**</span></span>

<span data-ttu-id="c7285-1489">Bu olay, bir USBX konak sınıfını CDC ACM IOCTL Get satırı kodlama olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1489">This event represents a USBX Host Class Cdc Acm Ioctl Get Line Coding Event.</span></span>

<span data-ttu-id="c7285-1490">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1490">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-1491">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1491">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1492">Bilgi alanı 2: parametre.</span><span class="sxs-lookup"><span data-stu-id="c7285-1492">Info Field 2: Parameter.</span></span>
- <span data-ttu-id="c7285-1493">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1493">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1494">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1494">Info Field 4: Not used.</span></span>

### <a name="host-class-cdc-acm-ioctl-notification-callback"></a><span data-ttu-id="c7285-1495">Ana bilgisayar sınıfı CDC ACM IOCTL bildirimi geri araması</span><span class="sxs-lookup"><span data-stu-id="c7285-1495">Host Class Cdc Acm Ioctl Notification Callback</span></span>

#### <a name="ux_host_class_cdc_acm_ioctl_notification_callback"></a><span data-ttu-id="c7285-1496">ux_host_class_cdc_acm_ioctl_notification_callback</span><span class="sxs-lookup"><span data-stu-id="c7285-1496">ux_host_class_cdc_acm_ioctl_notification_callback</span></span>

<span data-ttu-id="c7285-1497">**Simge** ![ Ana bilgisayar sınıfı C D C A C M ı O C T m](./media/user-guide/usbx-events/image96.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1497">**Icon** ![Host Class C D C A C M I O C T L Notification Callback icon](./media/user-guide/usbx-events/image96.png)</span></span>

<span data-ttu-id="c7285-1498">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1498">**Description**</span></span>

<span data-ttu-id="c7285-1499">Bu olay bir USBX konak sınıfı CDC ACM IOCTL Notification geri çağırma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1499">This event represents a USBX Host Class Cdc Acm Ioctl Notification Callback Event.</span></span>

<span data-ttu-id="c7285-1500">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1500">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1501">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1501">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1502">Bilgi alanı 2: parametre.</span><span class="sxs-lookup"><span data-stu-id="c7285-1502">Info Field 2: Parameter.</span></span>
- <span data-ttu-id="c7285-1503">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1503">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1504">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1504">Info Field 4: Not used.</span></span>

### <a name="host-class-cdc-acm-ioctl-send-break"></a><span data-ttu-id="c7285-1505">Ana bilgisayar sınıfı CDC ACM IOCTL gönderme kesmesi</span><span class="sxs-lookup"><span data-stu-id="c7285-1505">Host Class Cdc Acm Ioctl Send Break</span></span> 

#### <a name="ux_host_class_cdc_acm_ioctl_send_break"></a><span data-ttu-id="c7285-1506">ux_host_class_cdc_acm_ioctl_send_break</span><span class="sxs-lookup"><span data-stu-id="c7285-1506">ux_host_class_cdc_acm_ioctl_send_break</span></span>

<span data-ttu-id="c7285-1507">**Simge** ![ Ana bilgisayar sınıfı C D C c M I m C T ı gönder kesme simgesi](./media/user-guide/usbx-events/image97.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1507">**Icon** ![Host Class C D C A C M I O C T L Send Break icon](./media/user-guide/usbx-events/image97.png)</span></span>

<span data-ttu-id="c7285-1508">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1508">**Description**</span></span>

<span data-ttu-id="c7285-1509">Bu olay, bir USBX konak sınıfını CDC ACM IOCTL gönderme kesmesi olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1509">This event represents a USBX Host Class Cdc Acm Ioctl Send Break Event.</span></span>

<span data-ttu-id="c7285-1510">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1510">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-1511">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1511">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1512">Bilgi alanı 2: parametre.</span><span class="sxs-lookup"><span data-stu-id="c7285-1512">Info Field 2: Parameter.</span></span>
- <span data-ttu-id="c7285-1513">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1513">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1514">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1514">Info Field 4: Not used.</span></span>

### <a name="host-class-cdc-acm-ioctl-set-line-coding"></a><span data-ttu-id="c7285-1515">Ana bilgisayar sınıfı CDC ACM IOCTL kümesi satırı kodlama</span><span class="sxs-lookup"><span data-stu-id="c7285-1515">Host Class Cdc Acm Ioctl Set Line Coding</span></span> 

#### <a name="ux_host_class_cdc_acm_ioctl_set_line_coding"></a><span data-ttu-id="c7285-1516">ux_host_class_cdc_acm_ioctl_set_line_coding</span><span class="sxs-lookup"><span data-stu-id="c7285-1516">ux_host_class_cdc_acm_ioctl_set_line_coding</span></span>

<span data-ttu-id="c7285-1517">**Simge** ![ C D C ana bilgisayar sınıfı c M T A c M ı O C T ı satır kodlama simge ](./media/user-guide/usbx-events/image97.png) simgesi ayarla] (./Media/User-Kılavuzu/USBX-Events/image98.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1517">**Icon** ![The Host Class C D C A C M I O C T L Set Line Coding icon](./media/user-guide/usbx-events/image97.png) icon](./media/user-guide/usbx-events/image98.png)</span></span>

<span data-ttu-id="c7285-1518">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1518">**Description**</span></span>

<span data-ttu-id="c7285-1519">Bu olay bir USBX konak sınıfı CDC ACM IOCTL kümesi satırı kodlama olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1519">This event represents a USBX Host Class Cdc Acm Ioctl Set Line Coding Event.</span></span>

<span data-ttu-id="c7285-1520">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1520">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1521">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1521">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1522">Bilgi alanı 2: parametre.</span><span class="sxs-lookup"><span data-stu-id="c7285-1522">Info Field 2: Parameter.</span></span>
- <span data-ttu-id="c7285-1523">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1523">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1524">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1524">Info Field 4: Not used.</span></span>

### <a name="host-class-cdc-acm-ioctl-set-line-state"></a><span data-ttu-id="c7285-1525">Ana bilgisayar sınıfı CDC ACM IOCTL kümesi satır durumu</span><span class="sxs-lookup"><span data-stu-id="c7285-1525">Host Class Cdc Acm Ioctl Set Line State</span></span> 

#### <a name="ux_host_class_cdc_acm_ioctl_set_line_state"></a><span data-ttu-id="c7285-1526">ux_host_class_cdc_acm_ioctl_set_line_state</span><span class="sxs-lookup"><span data-stu-id="c7285-1526">ux_host_class_cdc_acm_ioctl_set_line_state</span></span>

<span data-ttu-id="c7285-1527">**Simge** ![ Ana bilgisayar sınıfı C D C c M ı O C T ı](./media/user-guide/usbx-events/image99.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1527">**Icon** ![Host Class C D C A C M I O C T L Set Line State icon](./media/user-guide/usbx-events/image99.png)</span></span>

<span data-ttu-id="c7285-1528">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1528">**Description**</span></span>

<span data-ttu-id="c7285-1529">Bu olay bir USBX konak sınıfı CDC ACM IOCTL kümesi satır durumu olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1529">This event represents a USBX Host Class Cdc Acm Ioctl Set Line State Event.</span></span>

<span data-ttu-id="c7285-1530">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1530">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-1531">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1531">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1532">Bilgi alanı 2: parametre.</span><span class="sxs-lookup"><span data-stu-id="c7285-1532">Info Field 2: Parameter.</span></span>
- <span data-ttu-id="c7285-1533">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1533">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1534">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1534">Info Field 4: Not used.</span></span>

### <a name="host-class-cdc-acm-read"></a><span data-ttu-id="c7285-1535">Ana bilgisayar sınıfı CDC ACM okuma</span><span class="sxs-lookup"><span data-stu-id="c7285-1535">Host Class Cdc Acm Read</span></span> 

#### <a name="ux_host_class_cdc_acm_read"></a><span data-ttu-id="c7285-1536">ux_host_class_cdc_acm_read</span><span class="sxs-lookup"><span data-stu-id="c7285-1536">ux_host_class_cdc_acm_read</span></span>

<span data-ttu-id="c7285-1537">**Simge** ![ Ana bilgisayar sınıfı C D C bir C M oku simgesi](./media/user-guide/usbx-events/image100.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1537">**Icon** ![Host Class C D C A C M Read icon](./media/user-guide/usbx-events/image100.png)</span></span>

<span data-ttu-id="c7285-1538">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1538">**Description**</span></span>

<span data-ttu-id="c7285-1539">Bu olay bir USBX konak sınıfını CDC ACM Read olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1539">This event represents a USBX Host Class Cdc Acm Read Event.</span></span>

<span data-ttu-id="c7285-1540">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1540">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-1541">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1541">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1542">Bilgi alanı 2: veri işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c7285-1542">Info Field 2: Data pointer.</span></span>
- <span data-ttu-id="c7285-1543">Bilgi alanı 3: Istenen uzunluk.</span><span class="sxs-lookup"><span data-stu-id="c7285-1543">Info Field 3: Requested Length.</span></span>
- <span data-ttu-id="c7285-1544">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1544">Info Field 4: Not used.</span></span>

### <a name="host-class-cdc-acm-reception-start"></a><span data-ttu-id="c7285-1545">Ana bilgisayar sınıfı CDC ACM alma başlangıcı</span><span class="sxs-lookup"><span data-stu-id="c7285-1545">Host Class Cdc Acm Reception Start</span></span> 

#### <a name="ux_host_class_cdc_acm_reception_start"></a><span data-ttu-id="c7285-1546">ux_host_class_cdc_acm_reception_start</span><span class="sxs-lookup"><span data-stu-id="c7285-1546">ux_host_class_cdc_acm_reception_start</span></span>

<span data-ttu-id="c7285-1547">**Simge** ![ Ana bilgisayar sınıfı C D C A C M alma başlangıç simgesi](./media/user-guide/usbx-events/image101.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1547">**Icon** ![Host Class C D C A C M Reception Start icon](./media/user-guide/usbx-events/image101.png)</span></span>

<span data-ttu-id="c7285-1548">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1548">**Description**</span></span>

<span data-ttu-id="c7285-1549">Bu olay, bir USBX konak sınıfını CDC ACM alma başlangıç olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1549">This event represents a USBX Host Class Cdc Acm Reception Start Event.</span></span>

<span data-ttu-id="c7285-1550">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1550">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1551">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1551">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1552">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1552">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-1553">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1553">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1554">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1554">Info Field 4: Not used.</span></span>

### <a name="host-class-cdc-acm-reception-stop"></a><span data-ttu-id="c7285-1555">Ana bilgisayar sınıfı CDC ACM alımı durdur</span><span class="sxs-lookup"><span data-stu-id="c7285-1555">Host Class Cdc Acm Reception Stop</span></span> 

#### <a name="ux_host_class_cdc_acm_reception_stop"></a><span data-ttu-id="c7285-1556">ux_host_class_cdc_acm_reception_stop</span><span class="sxs-lookup"><span data-stu-id="c7285-1556">ux_host_class_cdc_acm_reception_stop</span></span>

<span data-ttu-id="c7285-1557">**Simge** ![ Ana bilgisayar sınıfı C D C bir C M alımı durdur simgesi](./media/user-guide/usbx-events/image102.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1557">**Icon** ![Host Class C D C A C M Reception Stop icon](./media/user-guide/usbx-events/image102.png)</span></span>

<span data-ttu-id="c7285-1558">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1558">**Description**</span></span>

<span data-ttu-id="c7285-1559">Bu olay, bir USBX konak sınıfı CDC ACM alımı durdurma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1559">This event represents a USBX Host Class Cdc Acm Reception Stop Event.</span></span>

<span data-ttu-id="c7285-1560">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1560">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1561">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1561">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-1562">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1562">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1563">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1563">Info Field 4: Not used.</span></span>

### <a name="host-class-cdc-acm-write"></a><span data-ttu-id="c7285-1564">Ana bilgisayar sınıfı CDC ACM yazma</span><span class="sxs-lookup"><span data-stu-id="c7285-1564">Host Class Cdc Acm Write</span></span> 

#### <a name="ux_host_class_acm_write"></a><span data-ttu-id="c7285-1565">ux_host_class_acm_write</span><span class="sxs-lookup"><span data-stu-id="c7285-1565">ux_host_class_acm_write</span></span>

<span data-ttu-id="c7285-1566">**Simge** ![ Ana bilgisayar sınıfı C D C c M yazma simgesi](./media/user-guide/usbx-events/image103.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1566">**Icon** ![Host Class C D C A C M Write icon](./media/user-guide/usbx-events/image103.png)</span></span>

<span data-ttu-id="c7285-1567">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1567">**Description**</span></span>

<span data-ttu-id="c7285-1568">Bu olay bir USBX konak sınıfını CDC ACM yazma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1568">This event represents a USBX Host Class Cdc Acm Write Event.</span></span>

<span data-ttu-id="c7285-1569">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1569">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1570">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1570">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1571">Bilgi alanı 2: veri işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c7285-1571">Info Field 2: Data pointer.</span></span>
- <span data-ttu-id="c7285-1572">Bilgi alanı 3: Istenen uzunluk.</span><span class="sxs-lookup"><span data-stu-id="c7285-1572">Info Field 3: Requested Length.</span></span>
- <span data-ttu-id="c7285-1573">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1573">Info Field 4: Not used.</span></span>

### <a name="host-class-dpump-activate"></a><span data-ttu-id="c7285-1574">Konak sınıfı Dpump etkinleştir</span><span class="sxs-lookup"><span data-stu-id="c7285-1574">Host Class Dpump Activate</span></span> 

#### <a name="ux_host_class_dpump_activate"></a><span data-ttu-id="c7285-1575">ux_host_class_dpump_activate</span><span class="sxs-lookup"><span data-stu-id="c7285-1575">ux_host_class_dpump_activate</span></span>

<span data-ttu-id="c7285-1576">**Simge** ![ Host Class Dpump etkinleştir simgesi](./media/user-guide/usbx-events/image104.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1576">**Icon** ![Host Class Dpump Activate icon](./media/user-guide/usbx-events/image104.png)</span></span>

<span data-ttu-id="c7285-1577">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1577">**Description**</span></span>

<span data-ttu-id="c7285-1578">Bu olay bir USBX konak sınıfı Dpump Activate olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1578">This event represents a USBX Host Class Dpump Activate Event.</span></span>

<span data-ttu-id="c7285-1579">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1579">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-1580">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1580">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1581">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1581">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-1582">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1582">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1583">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1583">Info Field 4: Not used.</span></span>

### <a name="host-class-dpump-deactivate"></a><span data-ttu-id="c7285-1584">Konak sınıfı Dpump devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="c7285-1584">Host Class Dpump Deactivate</span></span> 

#### <a name="ux_host_class_dpump_deactivate"></a><span data-ttu-id="c7285-1585">ux_host_class_dpump_deactivate</span><span class="sxs-lookup"><span data-stu-id="c7285-1585">ux_host_class_dpump_deactivate</span></span>

<span data-ttu-id="c7285-1586">**Simge** ![ Konak sınıfı Dpump etkinliğini kaldırma simgesi](./media/user-guide/usbx-events/image105.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1586">**Icon** ![Host Class Dpump Deactivate icon](./media/user-guide/usbx-events/image105.png)</span></span>

<span data-ttu-id="c7285-1587">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1587">**Description**</span></span>

<span data-ttu-id="c7285-1588">Bu olay bir USBX konak sınıfı Dpump Deactivate olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1588">This event represents a USBX Host Class Dpump Deactivate Event.</span></span>

<span data-ttu-id="c7285-1589">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1589">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-1590">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1590">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1591">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1591">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-1592">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1592">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1593">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1593">Info Field 4: Not used.</span></span>

### <a name="host-class-dpump-read"></a><span data-ttu-id="c7285-1594">Konak sınıfı Dpump okuma</span><span class="sxs-lookup"><span data-stu-id="c7285-1594">Host Class Dpump Read</span></span> 

#### <a name="ux_host_class_dpump_read"></a><span data-ttu-id="c7285-1595">ux_host_class_dpump_read</span><span class="sxs-lookup"><span data-stu-id="c7285-1595">ux_host_class_dpump_read</span></span>

<span data-ttu-id="c7285-1596">**Simge** ![ Konak sınıfı Dpump oku simgesi](./media/user-guide/usbx-events/image106.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1596">**Icon** ![Host Class Dpump Read icon](./media/user-guide/usbx-events/image106.png)</span></span>

<span data-ttu-id="c7285-1597">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1597">**Description**</span></span>

<span data-ttu-id="c7285-1598">Bu olay bir USBX konak sınıfı Dpump okuma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1598">This event represents a USBX Host Class Dpump Read Event.</span></span>

<span data-ttu-id="c7285-1599">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1599">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1600">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1600">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1601">Bilgi alanı 2: veri işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c7285-1601">Info Field 2: Data pointer.</span></span>
- <span data-ttu-id="c7285-1602">Bilgi alanı 3: Istenen uzunluk.</span><span class="sxs-lookup"><span data-stu-id="c7285-1602">Info Field 3: Requested length.</span></span>
- <span data-ttu-id="c7285-1603">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1603">Info Field 4: Not used.</span></span>

### <a name="host-class-dpump-write"></a><span data-ttu-id="c7285-1604">Konak sınıfı Dpump yazma</span><span class="sxs-lookup"><span data-stu-id="c7285-1604">Host Class Dpump Write</span></span> 

#### <a name="ux_host_class_dpump_write"></a><span data-ttu-id="c7285-1605">ux_host_class_dpump_write</span><span class="sxs-lookup"><span data-stu-id="c7285-1605">ux_host_class_dpump_write</span></span>

<span data-ttu-id="c7285-1606">**Simge** ![ Ana sınıf Dpump yazma simgesi](./media/user-guide/usbx-events/image107.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1606">**Icon** ![Host Class Dpump Write icon](./media/user-guide/usbx-events/image107.png)</span></span>

<span data-ttu-id="c7285-1607">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1607">**Description**</span></span>

<span data-ttu-id="c7285-1608">Bu olay bir USBX konak sınıfı Dpump yazma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1608">This event represents a USBX Host Class Dpump Write Event.</span></span>

<span data-ttu-id="c7285-1609">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1609">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-1610">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1610">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1611">Bilgi alanı 2: veri işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c7285-1611">Info Field 2: Data pointer.</span></span>
- <span data-ttu-id="c7285-1612">Bilgi alanı 3: Istenen uzunluk.</span><span class="sxs-lookup"><span data-stu-id="c7285-1612">Info Field 3: Requested length.</span></span>
- <span data-ttu-id="c7285-1613">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1613">Info Field 4: Not used.</span></span>

### <a name="host-class-hid-activate"></a><span data-ttu-id="c7285-1614">Konak sınıfı HID etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="c7285-1614">Host Class Hid Activate</span></span> 

#### <a name="ux_host_class_hid_activate"></a><span data-ttu-id="c7285-1615">ux_host_class_hid_activate</span><span class="sxs-lookup"><span data-stu-id="c7285-1615">ux_host_class_hid_activate</span></span>

<span data-ttu-id="c7285-1616">**Simge** ![ Konak sınıfı HID etkinleştirme simgesi](./media/user-guide/usbx-events/image108.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1616">**Icon** ![Host Class Hid Activate icon](./media/user-guide/usbx-events/image108.png)</span></span>

<span data-ttu-id="c7285-1617">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1617">**Description**</span></span>

<span data-ttu-id="c7285-1618">Bu olay bir USBX konak sınıfı HID etkinleştirme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1618">This event represents a USBX Host Class Hid Activate Event.</span></span>

<span data-ttu-id="c7285-1619">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1619">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1620">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1620">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1621">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1621">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-1622">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1622">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1623">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1623">Info Field 4: Not used.</span></span>

### <a name="host-class-hid-client-register"></a><span data-ttu-id="c7285-1624">Konak sınıfı HID Istemci kaydı</span><span class="sxs-lookup"><span data-stu-id="c7285-1624">Host Class Hid Client Register</span></span> 

#### <a name="ux_host_class_hid_client_register"></a><span data-ttu-id="c7285-1625">ux_host_class_hid_client_register</span><span class="sxs-lookup"><span data-stu-id="c7285-1625">ux_host_class_hid_client_register</span></span>

<span data-ttu-id="c7285-1626">**Simge** ![ Konak sınıfı HID Istemci kaydı simgesi](./media/user-guide/usbx-events/image109.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1626">**Icon** ![Host Class Hid Client Register icon](./media/user-guide/usbx-events/image109.png)</span></span>

<span data-ttu-id="c7285-1627">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1627">**Description**</span></span>

<span data-ttu-id="c7285-1628">Bu olay bir USBX konak sınıfı HID Istemci kaydı olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1628">This event represents a USBX Host Class Hid Client Register Event.</span></span>

<span data-ttu-id="c7285-1629">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1629">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-1630">Bilgi alanı 1: HID istemci adı.</span><span class="sxs-lookup"><span data-stu-id="c7285-1630">Info Field 1: Hid client name.</span></span>
- <span data-ttu-id="c7285-1631">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1631">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-1632">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1632">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1633">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1633">Info Field 4: Not used.</span></span>

### <a name="host-class-hid-deactivate"></a><span data-ttu-id="c7285-1634">Konak sınıfı HID devre dışı</span><span class="sxs-lookup"><span data-stu-id="c7285-1634">Host Class Hid Deactivate</span></span> 

#### <a name="ux_host_class_hid_deactivate"></a><span data-ttu-id="c7285-1635">ux_host_class_hid_deactivate</span><span class="sxs-lookup"><span data-stu-id="c7285-1635">ux_host_class_hid_deactivate</span></span>

<span data-ttu-id="c7285-1636">**Simge** ![ Konak sınıfı HID devre dışı bırakma simgesi](./media/user-guide/usbx-events/image110.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1636">**Icon** ![Host Class Hid Deactivate icon](./media/user-guide/usbx-events/image110.png)</span></span>

<span data-ttu-id="c7285-1637">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1637">**Description**</span></span>

<span data-ttu-id="c7285-1638">Bu olay bir USBX konak sınıfı HID devre dışı bırakma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1638">This event represents a USBX Host Class Hid Deactivate Event.</span></span>

<span data-ttu-id="c7285-1639">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1639">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-1640">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1640">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1641">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1641">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-1642">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1642">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1643">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1643">Info Field 4: Not used.</span></span>

### <a name="host-class-hid-idle-get"></a><span data-ttu-id="c7285-1644">Konak sınıfı HID boşta al</span><span class="sxs-lookup"><span data-stu-id="c7285-1644">Host Class Hid Idle Get</span></span> 

#### <a name="ux_host_class_hid_idle_get"></a><span data-ttu-id="c7285-1645">ux_host_class_hid_idle_get</span><span class="sxs-lookup"><span data-stu-id="c7285-1645">ux_host_class_hid_idle_get</span></span>

<span data-ttu-id="c7285-1646">**Simge** ![ Konak sınıfı HID boşta al al simgesi](./media/user-guide/usbx-events/image111.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1646">**Icon** ![Host Class Hid Idle Get icon](./media/user-guide/usbx-events/image111.png)</span></span>

<span data-ttu-id="c7285-1647">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1647">**Description**</span></span>

<span data-ttu-id="c7285-1648">Bu olay, bir USBX ana bilgisayar sınıfı HID boşta al Get olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1648">This event represents a USBX Host Class Hid Idle Get Event.</span></span>

<span data-ttu-id="c7285-1649">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1649">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-1650">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1650">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1651">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1651">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-1652">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1652">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1653">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1653">Info Field 4: Not used.</span></span>

### <a name="host-class-hid-idle-set"></a><span data-ttu-id="c7285-1654">Konak sınıfı HID boşta kümesi</span><span class="sxs-lookup"><span data-stu-id="c7285-1654">Host Class Hid Idle Set</span></span> 

#### <a name="ux_host_class_hid_idle_set"></a><span data-ttu-id="c7285-1655">ux_host_class_hid_idle_set</span><span class="sxs-lookup"><span data-stu-id="c7285-1655">ux_host_class_hid_idle_set</span></span>

<span data-ttu-id="c7285-1656">**Simge** ![ Konak sınıfı HID boşta kümesi simgesi](./media/user-guide/usbx-events/image112.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1656">**Icon** ![Host Class Hid Idle Set icon](./media/user-guide/usbx-events/image112.png)</span></span>

<span data-ttu-id="c7285-1657">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1657">**Description**</span></span>

<span data-ttu-id="c7285-1658">Bu olay bir USBX konak sınıfı HID boşta ayarlama olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1658">This event represents a USBX Host Class Hid Idle Set Event.</span></span>

<span data-ttu-id="c7285-1659">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1659">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-1660">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1660">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1661">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1661">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-1662">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1662">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1663">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1663">Info Field 4: Not used.</span></span>

### <a name="host-class-hid-keyboard-activate"></a><span data-ttu-id="c7285-1664">Host Class HID Klavye etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="c7285-1664">Host Class Hid Keyboard Activate</span></span> 

#### <a name="ux_host_class_hid_keyboard_activate"></a><span data-ttu-id="c7285-1665">ux_host_class_hid_keyboard_activate</span><span class="sxs-lookup"><span data-stu-id="c7285-1665">ux_host_class_hid_keyboard_activate</span></span>

<span data-ttu-id="c7285-1666">**Simge** ![ Host Class HID Klavye etkinleştirme simgesi](./media/user-guide/usbx-events/image113.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1666">**Icon** ![Host Class Hid Keyboard Activate icon](./media/user-guide/usbx-events/image113.png)</span></span>

<span data-ttu-id="c7285-1667">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1667">**Description**</span></span>

<span data-ttu-id="c7285-1668">Bu olay bir USBX Host Class HID Klavye etkinleştirme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1668">This event represents a USBX Host Class Hid Keyboard Activate Event.</span></span>

<span data-ttu-id="c7285-1669">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1669">**Information Fields**</span></span>
<p><span data-ttu-id="c7285-1670">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1670">Info Field 1: Class instance.</span></span>
<p><span data-ttu-id="c7285-1671">Bilgi alanı 2: HID istemci örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1671">Info Field 2: Hid client instance.</span></span>
<p><span data-ttu-id="c7285-1672">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1672">Info Field 3: Not used.</span></span>
<p><span data-ttu-id="c7285-1673">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1673">Info Field 4: Not used.</span></span>

### <a name="host-class-hid-keyboard-deactivate"></a><span data-ttu-id="c7285-1674">Host Class HID Klavye devre dışı</span><span class="sxs-lookup"><span data-stu-id="c7285-1674">Host Class Hid Keyboard Deactivate</span></span> 

#### <a name="ux_host_class_hid_keyboard_deactivate"></a><span data-ttu-id="c7285-1675">ux_host_class_hid_keyboard_deactivate</span><span class="sxs-lookup"><span data-stu-id="c7285-1675">ux_host_class_hid_keyboard_deactivate</span></span>

<span data-ttu-id="c7285-1676">**Simge** ![ Host Class HID Klavye devre dışı simgesi](./media/user-guide/usbx-events/image114.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1676">**Icon** ![Host Class Hid Keyboard Deactivate icon](./media/user-guide/usbx-events/image114.png)</span></span>

<span data-ttu-id="c7285-1677">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1677">**Description**</span></span>

<span data-ttu-id="c7285-1678">Bu olay bir USBX Host Class HID Klavye devre dışı bırakma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1678">This event represents a USBX Host Class Hid Keyboard Deactivate Event.</span></span>

<span data-ttu-id="c7285-1679">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1679">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1680">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1680">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1681">Bilgi alanı 2: HID istemci örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1681">Info Field 2: Hid client instance.</span></span>
- <span data-ttu-id="c7285-1682">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1682">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1683">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1683">Info Field 4: Not used.</span></span>

### <a name="host-class-hid-mouse-activate"></a><span data-ttu-id="c7285-1684">Konak sınıfı HID fare etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="c7285-1684">Host Class Hid Mouse Activate</span></span> 

#### <a name="ux_host_class_hid_mouse_activate"></a><span data-ttu-id="c7285-1685">ux_host_class_hid_mouse_activate</span><span class="sxs-lookup"><span data-stu-id="c7285-1685">ux_host_class_hid_mouse_activate</span></span>

<span data-ttu-id="c7285-1686">**Simge** ![ Host Class HID fare etkinleştirme simgesi](./media/user-guide/usbx-events/image115.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1686">**Icon** ![Host Class Hid Mouse Activate icon](./media/user-guide/usbx-events/image115.png)</span></span>

<span data-ttu-id="c7285-1687">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1687">**Description**</span></span>

<span data-ttu-id="c7285-1688">Bu olay bir USBX Host Class HID fare etkinleştirme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1688">This event represents a USBX Host Class Hid Mouse Activate Event.</span></span>

<span data-ttu-id="c7285-1689">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1689">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1690">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1690">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1691">Bilgi alanı 2: HID istemci örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1691">Info Field 2: Hid client instance.</span></span>
- <span data-ttu-id="c7285-1692">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1692">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1693">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1693">Info Field 4: Not used.</span></span>

### <a name="host-class-hid-mouse-deactivate"></a><span data-ttu-id="c7285-1694">Konak sınıfı HID fare devre dışı</span><span class="sxs-lookup"><span data-stu-id="c7285-1694">Host Class Hid Mouse Deactivate</span></span> 

#### <a name="ux_host_class_hid_mouse_deactivate"></a><span data-ttu-id="c7285-1695">ux_host_class_hid_mouse_deactivate</span><span class="sxs-lookup"><span data-stu-id="c7285-1695">ux_host_class_hid_mouse_deactivate</span></span>

<span data-ttu-id="c7285-1696">**Simge** ![ Konak sınıfı HID fare devre dışı simgesi](./media/user-guide/usbx-events/image116.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1696">**Icon** ![Host Class Hid Mouse Deactivate icon](./media/user-guide/usbx-events/image116.png)</span></span>

<span data-ttu-id="c7285-1697">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1697">**Description**</span></span>

- <span data-ttu-id="c7285-1698">Bu olay bir USBX Host Class HID fare devre dışı bırakma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1698">This event represents a USBX Host Class Hid Mouse Deactivate Event.</span></span>

<span data-ttu-id="c7285-1699">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1699">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1700">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1700">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1701">Bilgi alanı 2: HID istemci örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1701">Info Field 2: Hid client instance.</span></span>
- <span data-ttu-id="c7285-1702">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1702">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1703">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1703">Info Field 4: Not used.</span></span>

### <a name="host-class-hid-remote-control-activate"></a><span data-ttu-id="c7285-1704">Konak sınıfı HID uzaktan denetim etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="c7285-1704">Host Class Hid Remote Control Activate</span></span> 

#### <a name="ux_host_class_hid_remote_control_activate"></a><span data-ttu-id="c7285-1705">ux_host_class_hid_remote_control_activate</span><span class="sxs-lookup"><span data-stu-id="c7285-1705">ux_host_class_hid_remote_control_activate</span></span>

<span data-ttu-id="c7285-1706">**Simge** ![ Konak sınıfı HID uzaktan denetim etkinleştirme simgesi](./media/user-guide/usbx-events/image117.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1706">**Icon** ![Host Class Hid Remote Control Activate icon](./media/user-guide/usbx-events/image117.png)</span></span>

<span data-ttu-id="c7285-1707">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1707">**Description**</span></span>

<span data-ttu-id="c7285-1708">Bu olay bir USBX konak sınıfı HID uzaktan denetim etkinleştirme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1708">This event represents a USBX Host Class Hid Remote Control Activate Event.</span></span>

<span data-ttu-id="c7285-1709">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1709">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-1710">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1710">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1711">Bilgi alanı 2: HID istemci örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1711">Info Field 2: Hid client instance.</span></span>
- <span data-ttu-id="c7285-1712">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1712">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1713">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1713">Info Field 4: Not used.</span></span>

### <a name="host-class-hid-remote-control-deactivate"></a><span data-ttu-id="c7285-1714">Konak sınıfı HID uzaktan denetim devre dışı</span><span class="sxs-lookup"><span data-stu-id="c7285-1714">Host Class Hid Remote Control Deactivate</span></span> 

#### <a name="ux_host_class_hid_remote_control_deactivate"></a><span data-ttu-id="c7285-1715">ux_host_class_hid_remote_control_deactivate</span><span class="sxs-lookup"><span data-stu-id="c7285-1715">ux_host_class_hid_remote_control_deactivate</span></span>

<span data-ttu-id="c7285-1716">**Simge** ![ Konak sınıfı HID uzaktan denetim devre dışı simgesi](./media/user-guide/usbx-events/image118.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1716">**Icon** ![Host Class Hid Remote Control Deactivate icon](./media/user-guide/usbx-events/image118.png)</span></span>

<span data-ttu-id="c7285-1717">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1717">**Description**</span></span>

<span data-ttu-id="c7285-1718">Bu olay bir USBX konak sınıfı HID uzaktan denetim devre dışı olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1718">This event represents a USBX Host Class Hid Remote Control Deactivate Event.</span></span>

<span data-ttu-id="c7285-1719">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1719">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-1720">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1720">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1721">Bilgi alanı 2: HID istemci örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1721">Info Field 2: Hid client instance.</span></span>
- <span data-ttu-id="c7285-1722">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1722">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1723">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1723">Info Field 4: Not used.</span></span>

### <a name="host-class-hid-report-get"></a><span data-ttu-id="c7285-1724">Konak sınıfı HID raporu al</span><span class="sxs-lookup"><span data-stu-id="c7285-1724">Host Class Hid Report Get</span></span> 

#### <a name="ux_host_class_hid_report_get"></a><span data-ttu-id="c7285-1725">ux_host_class_hid_report_get</span><span class="sxs-lookup"><span data-stu-id="c7285-1725">ux_host_class_hid_report_get</span></span>

<span data-ttu-id="c7285-1726">**Simge** ![ Konak sınıfı HID raporu al simgesi](./media/user-guide/usbx-events/image119.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1726">**Icon** ![Host Class Hid Report Get icon](./media/user-guide/usbx-events/image119.png)</span></span>

<span data-ttu-id="c7285-1727">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1727">**Description**</span></span>

<span data-ttu-id="c7285-1728">Bu olay bir USBX konak sınıfı HID raporu al 'ı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1728">This event represents a USBX Host Class Hid Report Get.</span></span>

<span data-ttu-id="c7285-1729">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1729">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1730">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1730">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1731">Bilgi alanı 2: Istemci raporu.</span><span class="sxs-lookup"><span data-stu-id="c7285-1731">Info Field 2: Client report.</span></span>
- <span data-ttu-id="c7285-1732">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1732">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1733">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1733">Info Field 4: Not used.</span></span>

### <a name="host-class-hid-report-set"></a><span data-ttu-id="c7285-1734">Konak sınıfı HID rapor kümesi</span><span class="sxs-lookup"><span data-stu-id="c7285-1734">Host Class Hid Report Set</span></span> 

#### <a name="ux_host_class_hid_report_set"></a><span data-ttu-id="c7285-1735">ux_host_class_hid_report_set</span><span class="sxs-lookup"><span data-stu-id="c7285-1735">ux_host_class_hid_report_set</span></span>

<span data-ttu-id="c7285-1736">**Simge** ![ Konak sınıfı HID rapor kümesi simgesi](./media/user-guide/usbx-events/image120.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1736">**Icon** ![Host Class Hid Report Set icon](./media/user-guide/usbx-events/image120.png)</span></span>

<span data-ttu-id="c7285-1737">**Açıklama** Bu olay bir USBX konak sınıfı HID rapor kümesini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1737">**Description** This event represents a USBX Host Class Hid Report Set.</span></span>

<span data-ttu-id="c7285-1738">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1738">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1739">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1739">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1740">Bilgi alanı 2: Istemci raporu.</span><span class="sxs-lookup"><span data-stu-id="c7285-1740">Info Field 2: Client report.</span></span>
- <span data-ttu-id="c7285-1741">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1741">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1742">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1742">Info Field 4: Not used.</span></span>

### <a name="host-class-hub-activate"></a><span data-ttu-id="c7285-1743">Konak sınıfı hub 'ı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="c7285-1743">Host Class Hub Activate</span></span> 

#### <a name="ux_host_class_hub_activate"></a><span data-ttu-id="c7285-1744">ux_host_class_hub_activate</span><span class="sxs-lookup"><span data-stu-id="c7285-1744">ux_host_class_hub_activate</span></span>

<span data-ttu-id="c7285-1745">**Simge** ![ Konak sınıfı hub etkinleştirme simgesi](./media/user-guide/usbx-events/image121.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1745">**Icon** ![Host Class Hub Activate icon](./media/user-guide/usbx-events/image121.png)</span></span>

<span data-ttu-id="c7285-1746">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1746">**Description**</span></span>

<span data-ttu-id="c7285-1747">Bu olay bir USBX konak sınıfı hub 'ı etkinleştir olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1747">This event represents a USBX Host Class Hub Activate Event.</span></span>

<span data-ttu-id="c7285-1748">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1748">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-1749">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1749">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1750">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1750">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-1751">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1751">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1752">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1752">Info Field 4: Not used.</span></span>

### <a name="host-class-hub-change-detect"></a><span data-ttu-id="c7285-1753">Konak sınıf hub değişikliği algılaması</span><span class="sxs-lookup"><span data-stu-id="c7285-1753">Host Class Hub Change Detect</span></span> 

#### <a name="ux_host_class_hub_change_detect"></a><span data-ttu-id="c7285-1754">ux_host_class_hub_change_detect</span><span class="sxs-lookup"><span data-stu-id="c7285-1754">ux_host_class_hub_change_detect</span></span>

<span data-ttu-id="c7285-1755">**Simge** ![ Host Class hub değişikliği algılama simgesi](./media/user-guide/usbx-events/image122.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1755">**Icon** ![Host Class Hub Change Detect icon](./media/user-guide/usbx-events/image122.png)</span></span>

<span data-ttu-id="c7285-1756">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1756">**Description**</span></span>

<span data-ttu-id="c7285-1757">Bu olay bir USBX konak sınıfı hub değişiklik algılama olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1757">This event represents a USBX Host Class Hub Change Detect Event.</span></span>

<span data-ttu-id="c7285-1758">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1758">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1759">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1759">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1760">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1760">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-1761">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1761">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1762">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1762">Info Field 4: Not used.</span></span>

### <a name="host-class-hub-deactivate"></a><span data-ttu-id="c7285-1763">Konak sınıfı hub 'ı devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="c7285-1763">Host Class Hub Deactivate</span></span> 

#### <a name="ux_host_class_hub_deactivate"></a><span data-ttu-id="c7285-1764">ux_host_class_hub_deactivate</span><span class="sxs-lookup"><span data-stu-id="c7285-1764">ux_host_class_hub_deactivate</span></span>

<span data-ttu-id="c7285-1765">**Simge** ![ Konak sınıfı hub 'ı devre dışı bırakma simgesi](./media/user-guide/usbx-events/image123.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1765">**Icon** ![Host Class Hub Deactivate icon](./media/user-guide/usbx-events/image123.png)</span></span>

<span data-ttu-id="c7285-1766">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1766">**Description**</span></span>

<span data-ttu-id="c7285-1767">Bu olay bir USBX konak sınıfı hub 'ı devre dışı bırakma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1767">This event represents a USBX Host Class Hub Deactivate Event.</span></span>

<span data-ttu-id="c7285-1768">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1768">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1769">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1769">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1770">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1770">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-1771">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1771">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1772">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1772">Info Field 4: Not used.</span></span>

### <a name="host-class-hub-port-change-connection-process"></a><span data-ttu-id="c7285-1773">Konak sınıf hub 'ı bağlantı noktası değiştirme bağlantı Işlemi</span><span class="sxs-lookup"><span data-stu-id="c7285-1773">Host Class Hub Port Change Connection Process</span></span> 

#### <a name="ux_host_class_hub_change_connection_process"></a><span data-ttu-id="c7285-1774">ux_host_class_hub_change_connection_process</span><span class="sxs-lookup"><span data-stu-id="c7285-1774">ux_host_class_hub_change_connection_process</span></span>

<span data-ttu-id="c7285-1775">**Simge** ![ Konak sınıf hub 'ı bağlantı noktası değişiklik bağlantı Işlemi simgesi](./media/user-guide/usbx-events/image124.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1775">**Icon** ![Host Class Hub Port Change Connection Process icon](./media/user-guide/usbx-events/image124.png)</span></span>

<span data-ttu-id="c7285-1776">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1776">**Description**</span></span>

<span data-ttu-id="c7285-1777">Bu olay bir USBX konak sınıfı hub bağlantı noktası değişim bağlantı Işlemi olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1777">This event represents a USBX Host Class Hub Port Change Connection Process Event.</span></span>

<span data-ttu-id="c7285-1778">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1778">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1779">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1779">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1780">Bilgi alanı 2: bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="c7285-1780">Info Field 2: Port.</span></span>
- <span data-ttu-id="c7285-1781">Bilgi alanı 3: bağlantı noktası durumu.</span><span class="sxs-lookup"><span data-stu-id="c7285-1781">Info Field 3: Port status.</span></span>
- <span data-ttu-id="c7285-1782">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1782">Info Field 4: Not used.</span></span>

### <a name="host-class-hub-port-change-enable-process"></a><span data-ttu-id="c7285-1783">Konak sınıfı hub bağlantı noktası değişikliği etkinleştirme Işlemi</span><span class="sxs-lookup"><span data-stu-id="c7285-1783">Host Class Hub Port Change Enable Process</span></span> 

#### <a name="ux_host_class_hub_port_change_enable_process"></a><span data-ttu-id="c7285-1784">ux_host_class_hub_port_change_enable_process</span><span class="sxs-lookup"><span data-stu-id="c7285-1784">ux_host_class_hub_port_change_enable_process</span></span>

<span data-ttu-id="c7285-1785">**Simge** ![ Konak sınıfı hub bağlantı noktası değişikliği etkinleştirme Işlemi simgesi](./media/user-guide/usbx-events/image125.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1785">**Icon** ![Host Class Hub Port Change Enable Process icon](./media/user-guide/usbx-events/image125.png)</span></span>

<span data-ttu-id="c7285-1786">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1786">**Description**</span></span>

<span data-ttu-id="c7285-1787">Bu olay bir USBX konak sınıfı hub bağlantı noktası değişikliğini Işlemi etkinleştir olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1787">This event represents a USBX Host Class Hub Port Change Enable Process Event.</span></span>

<span data-ttu-id="c7285-1788">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1788">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1789">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1789">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1790">Bilgi alanı 2: bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="c7285-1790">Info Field 2: Port.</span></span>
- <span data-ttu-id="c7285-1791">Bilgi alanı 3: bağlantı noktası durumu.</span><span class="sxs-lookup"><span data-stu-id="c7285-1791">Info Field 3: Port status.</span></span>
- <span data-ttu-id="c7285-1792">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1792">Info Field 4: Not used.</span></span>

### <a name="host-class-hub-port-change-over-current-process"></a><span data-ttu-id="c7285-1793">Geçerli Işlem üzerinde ana bilgisayar sınıfı hub bağlantı noktası değişikliği</span><span class="sxs-lookup"><span data-stu-id="c7285-1793">Host Class Hub Port Change Over Current Process</span></span> 

#### <a name="ux_host_class_hub_port_change_over_current_process"></a><span data-ttu-id="c7285-1794">ux_host_class_hub_port_change_over_current_process</span><span class="sxs-lookup"><span data-stu-id="c7285-1794">ux_host_class_hub_port_change_over_current_process</span></span>

<span data-ttu-id="c7285-1795">**Simge** ![ Ana sınıf hub 'ı bağlantı noktası geçerli Işlem simgesi değişikliği](./media/user-guide/usbx-events/image126.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1795">**Icon** ![Host Class Hub Port Change Over Current Process icon](./media/user-guide/usbx-events/image126.png)</span></span>

<span data-ttu-id="c7285-1796">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1796">**Description**</span></span>

<span data-ttu-id="c7285-1797">Bu olay nx_packet_allocate aracılığıyla bir paket ayırmayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1797">This event represents allocating a packet via nx_packet_allocate.</span></span>

<span data-ttu-id="c7285-1798">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1798">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1799">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1799">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1800">Bilgi alanı 2: bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="c7285-1800">Info Field 2: Port.</span></span>
- <span data-ttu-id="c7285-1801">Bilgi alanı 3: bağlantı noktası durumu.</span><span class="sxs-lookup"><span data-stu-id="c7285-1801">Info Field 3: Port status.</span></span>
- <span data-ttu-id="c7285-1802">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1802">Info Field 4: Not used.</span></span>

### <a name="host-class-hub-port-change-reset-process"></a><span data-ttu-id="c7285-1803">Konak sınıf hub 'ı bağlantı noktası değişiklik sıfırlama Işlemi</span><span class="sxs-lookup"><span data-stu-id="c7285-1803">Host Class Hub Port Change Reset Process</span></span> 

#### <a name="ux_host_class_hub_port_change_reset_process"></a><span data-ttu-id="c7285-1804">ux_host_class_hub_port_change_reset_process</span><span class="sxs-lookup"><span data-stu-id="c7285-1804">ux_host_class_hub_port_change_reset_process</span></span>

<span data-ttu-id="c7285-1805">**Simge** ![ Konak sınıf hub 'ı bağlantı noktası değişiklik sıfırlama Işlemi simgesi](./media/user-guide/usbx-events/image127.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1805">**Icon** ![Host Class Hub Port Change Reset Process icon](./media/user-guide/usbx-events/image127.png)</span></span>

<span data-ttu-id="c7285-1806">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1806">**Description**</span></span>

<span data-ttu-id="c7285-1807">Bu olay bir USBX konak sınıfı hub bağlantı noktası değişiklik sıfırlama Işlemi olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1807">This event represents a USBX Host Class Hub Port Change Reset Process Event.</span></span>

<span data-ttu-id="c7285-1808">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1808">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1809">Bilgi alanı 1: hub.</span><span class="sxs-lookup"><span data-stu-id="c7285-1809">Info Field 1: Hub.</span></span> <span data-ttu-id="c7285-1810">Bilgi alanı 2: bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="c7285-1810">Info Field 2: Port.</span></span>
- <span data-ttu-id="c7285-1811">Bilgi alanı 3: bağlantı noktası durumu.</span><span class="sxs-lookup"><span data-stu-id="c7285-1811">Info Field 3: Port status.</span></span>
- <span data-ttu-id="c7285-1812">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1812">Info Field 4: Not used.</span></span>

### <a name="host-class-hub-port-change-suspend-process"></a><span data-ttu-id="c7285-1813">Konak sınıf hub 'ı bağlantı noktası değiştirme askıya alma Işlemi</span><span class="sxs-lookup"><span data-stu-id="c7285-1813">Host Class Hub Port Change Suspend Process</span></span> 

#### <a name="ux_host_class_hub_port_change_suspend_process"></a><span data-ttu-id="c7285-1814">ux_host_class_hub_port_change_suspend_process</span><span class="sxs-lookup"><span data-stu-id="c7285-1814">ux_host_class_hub_port_change_suspend_process</span></span>

<span data-ttu-id="c7285-1815">**Simge** ![ Konak sınıf hub 'ı bağlantı noktası değiştirme Işlemi askıya alma simgesi](./media/user-guide/usbx-events/image128.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1815">**Icon** ![Host Class Hub Port Change Suspend Process icon](./media/user-guide/usbx-events/image128.png)</span></span>

<span data-ttu-id="c7285-1816">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1816">**Description**</span></span>

<span data-ttu-id="c7285-1817">Bu olay bir USBX konak sınıfı hub 'ı değişiklik askıya alma Işlemi olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1817">This event represents a USBX Host Class Hub Port Change Suspend Process Event.</span></span>

<span data-ttu-id="c7285-1818">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1818">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1819">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1819">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1820">Bilgi alanı 2: bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="c7285-1820">Info Field 2: Port.</span></span>
- <span data-ttu-id="c7285-1821">Bilgi alanı 3: bağlantı noktası durumu.</span><span class="sxs-lookup"><span data-stu-id="c7285-1821">Info Field 3: Port status.</span></span>
- <span data-ttu-id="c7285-1822">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1822">Info Field 4: Not used.</span></span>

### <a name="host-class-pima-activate"></a><span data-ttu-id="c7285-1823">Konak sınıfı Pima etkinleştir</span><span class="sxs-lookup"><span data-stu-id="c7285-1823">Host Class Pima Activate</span></span> 

#### <a name="ux_host_class_pima_activate"></a><span data-ttu-id="c7285-1824">ux_host_class_pima_activate</span><span class="sxs-lookup"><span data-stu-id="c7285-1824">ux_host_class_pima_activate</span></span>

<span data-ttu-id="c7285-1825">**Simge** ![ Konak sınıfı Pima etkinleştirme simgesi](./media/user-guide/usbx-events/image129.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1825">**Icon** ![Host Class Pima Activate icon](./media/user-guide/usbx-events/image129.png)</span></span>

<span data-ttu-id="c7285-1826">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1826">**Description**</span></span>

<span data-ttu-id="c7285-1827">Bu olay bir USBX konak sınıfı Pima Activate olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1827">This event represents a USBX Host Class Pima Activate Event.</span></span>

<span data-ttu-id="c7285-1828">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1828">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1829">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1829">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1830">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1830">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-1831">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1831">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1832">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1832">Info Field 4: Not used.</span></span>

### <a name="host-class-pima-deactivate"></a><span data-ttu-id="c7285-1833">Konak sınıfı Pima devre dışı</span><span class="sxs-lookup"><span data-stu-id="c7285-1833">Host Class Pima Deactivate</span></span> 

#### <a name="ux_host_class_pima_deactivate"></a><span data-ttu-id="c7285-1834">ux_host_class_pima_deactivate</span><span class="sxs-lookup"><span data-stu-id="c7285-1834">ux_host_class_pima_deactivate</span></span>

<span data-ttu-id="c7285-1835">**Simge** ![ Konak sınıfı Pima devre dışı bırakma simgesi](./media/user-guide/usbx-events/image130.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1835">**Icon** ![Host Class Pima Deactivate icon](./media/user-guide/usbx-events/image130.png)</span></span>

<span data-ttu-id="c7285-1836">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1836">**Description**</span></span>

<span data-ttu-id="c7285-1837">Bu olay bir USBX konak sınıfı Pima devre dışı bırakma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1837">This event represents a USBX Host Class Pima Deactivate Event.</span></span>

<span data-ttu-id="c7285-1838">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1838">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1839">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1839">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1840">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1840">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-1841">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1841">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1842">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1842">Info Field 4: Not used.</span></span>

### <a name="host-class-pima-device-info-get"></a><span data-ttu-id="c7285-1843">Konak sınıfı Pima cihaz bilgileri Get</span><span class="sxs-lookup"><span data-stu-id="c7285-1843">Host Class Pima Device Info Get</span></span> 

#### <a name="ux_host_class_pima_device_info_get"></a><span data-ttu-id="c7285-1844">ux_host_class_pima_device_info_get</span><span class="sxs-lookup"><span data-stu-id="c7285-1844">ux_host_class_pima_device_info_get</span></span>

<span data-ttu-id="c7285-1845">**Simge** ![ Konak sınıfı Pima cihaz bilgileri al simgesi](./media/user-guide/usbx-events/image131.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1845">**Icon** ![Host Class Pima Device Info Get icon](./media/user-guide/usbx-events/image131.png)</span></span>

<span data-ttu-id="c7285-1846">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1846">**Description**</span></span>

<span data-ttu-id="c7285-1847">Bu olay bir USBX konak sınıfı Pima cihaz bilgileri Get olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1847">This event represents a USBX Host Class Pima Device Info Get Event.</span></span>

<span data-ttu-id="c7285-1848">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1848">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1849">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1849">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1850">Bilgi alanı 2: Pima cihazı.</span><span class="sxs-lookup"><span data-stu-id="c7285-1850">Info Field 2: Pima device.</span></span>
- <span data-ttu-id="c7285-1851">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1851">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1852">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1852">Info Field 4: Not used.</span></span>

### <a name="host-class-pima-device-reset"></a><span data-ttu-id="c7285-1853">Konak sınıfı Pima cihazı sıfırlama</span><span class="sxs-lookup"><span data-stu-id="c7285-1853">Host Class Pima Device Reset</span></span> 

#### <a name="ux_host_class_pima_device_reset"></a><span data-ttu-id="c7285-1854">ux_host_class_pima_device_reset</span><span class="sxs-lookup"><span data-stu-id="c7285-1854">ux_host_class_pima_device_reset</span></span>

<span data-ttu-id="c7285-1855">**Simge** ![ Konak sınıfı Pima cihazı sıfırlama simgesi](./media/user-guide/usbx-events/image132.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1855">**Icon** ![Host Class Pima Device Reset icon](./media/user-guide/usbx-events/image132.png)</span></span>

<span data-ttu-id="c7285-1856">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1856">**Description**</span></span>

<span data-ttu-id="c7285-1857">Bu olay bir USBX konak sınıfı Pima cihazı sıfırlama olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1857">This event represents a USBX Host Class Pima Device Reset Event.</span></span>

<span data-ttu-id="c7285-1858">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1858">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1859">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1859">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1860">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1860">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-1861">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1861">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1862">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1862">Info Field 4: Not used.</span></span>

### <a name="host-class-pima-notification"></a><span data-ttu-id="c7285-1863">Konak sınıfı Pima bildirimi</span><span class="sxs-lookup"><span data-stu-id="c7285-1863">Host Class Pima Notification</span></span> 

#### <a name="ux_host_class_pima_notification"></a><span data-ttu-id="c7285-1864">ux_host_class_pima_notification</span><span class="sxs-lookup"><span data-stu-id="c7285-1864">ux_host_class_pima_notification</span></span>

<span data-ttu-id="c7285-1865">**Simge** ![ Konak sınıfı Pima bildirimi simgesi](./media/user-guide/usbx-events/image133.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1865">**Icon** ![Host Class Pima Notification icon](./media/user-guide/usbx-events/image133.png)</span></span>

<span data-ttu-id="c7285-1866">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1866">**Description**</span></span>

<span data-ttu-id="c7285-1867">Bu olay bir USBX konak sınıfı Pima bildirimi olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1867">This event represents a USBX Host Class Pima Notification Event.</span></span>

<span data-ttu-id="c7285-1868">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1868">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1869">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1869">Info Field 1: Class instance.</span></span> <span data-ttu-id="c7285-1870">Bilgi alanı 2: olay kodu.</span><span class="sxs-lookup"><span data-stu-id="c7285-1870">Info Field 2: Event code.</span></span>
- <span data-ttu-id="c7285-1871">Bilgi alanı 3: Işlem KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="c7285-1871">Info Field 3: Transaction ID.</span></span>
- <span data-ttu-id="c7285-1872">Bilgi alanı 4: parametre1.</span><span class="sxs-lookup"><span data-stu-id="c7285-1872">Info Field 4: Parameter1.</span></span>

### <a name="host-class-pima-number-objects-get"></a><span data-ttu-id="c7285-1873">Konak sınıfı Pima sayısı nesneleri Al</span><span class="sxs-lookup"><span data-stu-id="c7285-1873">Host Class Pima Number Objects Get</span></span> 

#### <a name="ux_host_class_pima_number_objects_get"></a><span data-ttu-id="c7285-1874">ux_host_class_pima_number_objects_get</span><span class="sxs-lookup"><span data-stu-id="c7285-1874">ux_host_class_pima_number_objects_get</span></span>

<span data-ttu-id="c7285-1875">**Simge** ![ Konak sınıfı Pima sayısı nesneleri Al simgesi](./media/user-guide/usbx-events/image134.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1875">**Icon** ![Host Class Pima Number Objects Get icon](./media/user-guide/usbx-events/image134.png)</span></span>

<span data-ttu-id="c7285-1876">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1876">**Description**</span></span>

<span data-ttu-id="c7285-1877">Bu olay bir USBX konak sınıfı Pima Number nesneleri Al olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1877">This event represents a USBX Host Class Pima Number Objects Get Event.</span></span>

<span data-ttu-id="c7285-1878">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1878">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1879">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1879">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1880">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1880">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-1881">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1881">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1882">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1882">Info Field 4: Not used.</span></span>

### <a name="host-class-pima-object-close"></a><span data-ttu-id="c7285-1883">Konak sınıfı Pima nesnesi kapatma</span><span class="sxs-lookup"><span data-stu-id="c7285-1883">Host Class Pima Object Close</span></span> 

#### <a name="ux_host_class_pima_object_close"></a><span data-ttu-id="c7285-1884">ux_host_class_pima_object_close</span><span class="sxs-lookup"><span data-stu-id="c7285-1884">ux_host_class_pima_object_close</span></span>

<span data-ttu-id="c7285-1885">**Simge** ![ Ana sınıf Pima nesnesi kapatma simgesi](./media/user-guide/usbx-events/image135.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1885">**Icon** ![Host Class Pima Object Close icon](./media/user-guide/usbx-events/image135.png)</span></span>

<span data-ttu-id="c7285-1886">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1886">**Description**</span></span>

<span data-ttu-id="c7285-1887">Bu olay bir USBX Host Class Pima nesnesi Close olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1887">This event represents a USBX Host Class Pima Object Close Event.</span></span>

<span data-ttu-id="c7285-1888">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1888">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1889">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1889">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1890">Bilgi alanı 2: nesne.</span><span class="sxs-lookup"><span data-stu-id="c7285-1890">Info Field 2: Object.</span></span>
- <span data-ttu-id="c7285-1891">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1891">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1892">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1892">Info Field 4: Not used.</span></span>

### <a name="host-class-pima-object-copy"></a><span data-ttu-id="c7285-1893">Konak sınıfı Pima nesne kopyası</span><span class="sxs-lookup"><span data-stu-id="c7285-1893">Host Class Pima Object Copy</span></span> 

#### <a name="ux_host_class_pima_object_copy"></a><span data-ttu-id="c7285-1894">ux_host_class_pima_object_copy</span><span class="sxs-lookup"><span data-stu-id="c7285-1894">ux_host_class_pima_object_copy</span></span>

<span data-ttu-id="c7285-1895">**Simge** ![ Konak sınıfı Pima nesnesi kopyalama simgesi](./media/user-guide/usbx-events/image136.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1895">**Icon** ![Host Class Pima Object Copy icon](./media/user-guide/usbx-events/image136.png)</span></span>

<span data-ttu-id="c7285-1896">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1896">**Description**</span></span>

<span data-ttu-id="c7285-1897">Bu olay bir USBX konak sınıfı Pima nesne kopyalama olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1897">This event represents a USBX Host Class Pima Object Copy Event.</span></span>

<span data-ttu-id="c7285-1898">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1898">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1899">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1899">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1900">Bilgi alanı 2: nesne tanıtıcısı.</span><span class="sxs-lookup"><span data-stu-id="c7285-1900">Info Field 2: Object handle.</span></span>
- <span data-ttu-id="c7285-1901">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1901">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1902">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1902">Info Field 4: Not used.</span></span>

### <a name="host-class-pima-object-delete"></a><span data-ttu-id="c7285-1903">Konak sınıfı Pima nesnesi silme</span><span class="sxs-lookup"><span data-stu-id="c7285-1903">Host Class Pima Object Delete</span></span> 

#### <a name="ux_host_class_pima_object_delete"></a><span data-ttu-id="c7285-1904">ux_host_class_pima_object_delete</span><span class="sxs-lookup"><span data-stu-id="c7285-1904">ux_host_class_pima_object_delete</span></span>

<span data-ttu-id="c7285-1905">**Simge** ![ Konak sınıfı Pima nesnesi silme simgesi](./media/user-guide/usbx-events/image137.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1905">**Icon** ![Host Class Pima Object Delete icon](./media/user-guide/usbx-events/image137.png)</span></span>

<span data-ttu-id="c7285-1906">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1906">**Description**</span></span>

<span data-ttu-id="c7285-1907">Bu olay bir USBX konak sınıfı Pima nesnesi silme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1907">This event represents a USBX Host Class Pima Object Delete Event.</span></span>

<span data-ttu-id="c7285-1908">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1908">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1909">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1909">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1910">Bilgi alanı 2: nesne tanıtıcısı.</span><span class="sxs-lookup"><span data-stu-id="c7285-1910">Info Field 2: Object handle.</span></span>
- <span data-ttu-id="c7285-1911">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1911">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1912">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1912">Info Field 4: Not used.</span></span>

### <a name="host-class-pima-object-get"></a><span data-ttu-id="c7285-1913">Konak sınıfı Pima nesnesi Get</span><span class="sxs-lookup"><span data-stu-id="c7285-1913">Host Class Pima Object Get</span></span> 

#### <a name="ux_host_class_pima_object_get"></a><span data-ttu-id="c7285-1914">ux_host_class_pima_object_get</span><span class="sxs-lookup"><span data-stu-id="c7285-1914">ux_host_class_pima_object_get</span></span>

<span data-ttu-id="c7285-1915">**Simge** ![ Ana sınıf Pima nesnesi Al simgesi](./media/user-guide/usbx-events/image138.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1915">**Icon** ![Host Class Pima Object Get icon](./media/user-guide/usbx-events/image138.png)</span></span>

<span data-ttu-id="c7285-1916">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1916">**Description**</span></span>

<span data-ttu-id="c7285-1917">Bu olay nx_rarp_info_get aracılığıyla RARP bilgilerini almayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1917">This event represents getting RARP information via nx_rarp_info_get.</span></span>

<span data-ttu-id="c7285-1918">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1918">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1919">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1919">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1920">Bilgi alanı 2: nesne tanıtıcısı.</span><span class="sxs-lookup"><span data-stu-id="c7285-1920">Info Field 2: Object handle.</span></span>
- <span data-ttu-id="c7285-1921">Bilgi alanı 3: nesne.</span><span class="sxs-lookup"><span data-stu-id="c7285-1921">Info Field 3: Object.</span></span>
- <span data-ttu-id="c7285-1922">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1922">Info Field 4: Not used.</span></span>

### <a name="host-class-pima-object-info-get"></a><span data-ttu-id="c7285-1923">Konak sınıfı Pima nesnesi bilgi al</span><span class="sxs-lookup"><span data-stu-id="c7285-1923">Host Class Pima Object Info Get</span></span> 

#### <a name="ux_host_class_pima_object_info_get"></a><span data-ttu-id="c7285-1924">ux_host_class_pima_object_info_get</span><span class="sxs-lookup"><span data-stu-id="c7285-1924">ux_host_class_pima_object_info_get</span></span>

<span data-ttu-id="c7285-1925">**Simge** ![ Konak sınıfı Pima nesnesi bilgileri al simgesi](./media/user-guide/usbx-events/image139.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1925">**Icon** ![Host Class Pima Object Info Get icon](./media/user-guide/usbx-events/image139.png)</span></span>

<span data-ttu-id="c7285-1926">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1926">**Description**</span></span>

<span data-ttu-id="c7285-1927">Bu olay bir USBX konak sınıfı Pima nesne bilgileri al olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1927">This event represents a USBX Host Class Pima Object Info Get Event.</span></span>

<span data-ttu-id="c7285-1928">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1928">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1929">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1929">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1930">Bilgi alanı 2: nesne tanıtıcısı.</span><span class="sxs-lookup"><span data-stu-id="c7285-1930">Info Field 2: Object handle.</span></span>
- <span data-ttu-id="c7285-1931">Bilgi alanı 3: nesne.</span><span class="sxs-lookup"><span data-stu-id="c7285-1931">Info Field 3: Object.</span></span>
- <span data-ttu-id="c7285-1932">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1932">Info Field 4: Not used.</span></span>

### <a name="host-class-pima-object-info-send"></a><span data-ttu-id="c7285-1933">Konak sınıfı Pima nesne bilgileri gönderme</span><span class="sxs-lookup"><span data-stu-id="c7285-1933">Host Class Pima Object Info Send</span></span> 

#### <a name="ux_host_class_pima_object_info_send"></a><span data-ttu-id="c7285-1934">ux_host_class_pima_object_info_send</span><span class="sxs-lookup"><span data-stu-id="c7285-1934">ux_host_class_pima_object_info_send</span></span>

<span data-ttu-id="c7285-1935">**Simge** ![ Konak sınıfı Pima nesne bilgileri gönderme simgesi](./media/user-guide/usbx-events/image140.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1935">**Icon** ![Host Class Pima Object Info Send icon](./media/user-guide/usbx-events/image140.png)</span></span>

<span data-ttu-id="c7285-1936">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1936">**Description**</span></span>

<span data-ttu-id="c7285-1937">Bu olay bir USBX konak sınıfı Pima nesne bilgileri gönderme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1937">This event represents a USBX Host Class Pima Object Info Send Event.</span></span>

<span data-ttu-id="c7285-1938">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1938">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1939">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1939">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1940">Bilgi alanı 2: nesne.</span><span class="sxs-lookup"><span data-stu-id="c7285-1940">Info Field 2: Object.</span></span>
- <span data-ttu-id="c7285-1941">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1941">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1942">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1942">Info Field 4: Not used.</span></span>

### <a name="host-class-pima-object-move"></a><span data-ttu-id="c7285-1943">Konak sınıfı Pima nesnesi taşıma</span><span class="sxs-lookup"><span data-stu-id="c7285-1943">Host Class Pima Object Move</span></span> 

#### <a name="ux_host_class_pima_object_move"></a><span data-ttu-id="c7285-1944">ux_host_class_pima_object_move</span><span class="sxs-lookup"><span data-stu-id="c7285-1944">ux_host_class_pima_object_move</span></span>

<span data-ttu-id="c7285-1945">**Simge** ![ Konak sınıfı Pima nesnesi taşıma simgesi](./media/user-guide/usbx-events/image141.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1945">**Icon** ![Host Class Pima Object Move icon](./media/user-guide/usbx-events/image141.png)</span></span>

<span data-ttu-id="c7285-1946">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1946">**Description**</span></span>

<span data-ttu-id="c7285-1947">Bu olay Reprbu olayı, bir USBX konak sınıfı Pima nesne taşıma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1947">This event reprThis event represents a USBX Host Class Pima Object Move Event.</span></span>

<span data-ttu-id="c7285-1948">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1948">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1949">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1949">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1950">Bilgi alanı 2: nesne tanıtıcısı.</span><span class="sxs-lookup"><span data-stu-id="c7285-1950">Info Field 2: Object handle.</span></span>
- <span data-ttu-id="c7285-1951">Bilgi alanı 3: nesne.</span><span class="sxs-lookup"><span data-stu-id="c7285-1951">Info Field 3: Object.</span></span>
- <span data-ttu-id="c7285-1952">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1952">Info Field 4: Not used.</span></span>

### <a name="host-class-pima-object-send"></a><span data-ttu-id="c7285-1953">Konak sınıfı Pima nesnesi gönder</span><span class="sxs-lookup"><span data-stu-id="c7285-1953">Host Class Pima Object Send</span></span> 

#### <a name="ux_host_class_pima_object_move"></a><span data-ttu-id="c7285-1954">ux_host_class_pima_object_move</span><span class="sxs-lookup"><span data-stu-id="c7285-1954">ux_host_class_pima_object_move</span></span>

<span data-ttu-id="c7285-1955">**Simge** ![ Ana sınıf Pima nesnesi Gönder simgesi](./media/user-guide/usbx-events/image142.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1955">**Icon** ![Host Class Pima Object Send icon](./media/user-guide/usbx-events/image142.png)</span></span>

<span data-ttu-id="c7285-1956">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1956">**Description**</span></span>

<span data-ttu-id="c7285-1957">Bu olay bir USBX konak sınıfı Pima nesnesi gönderme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1957">This event represents a USBX Host Class Pima Object Send Event.</span></span>

<span data-ttu-id="c7285-1958">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1958">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1959">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1959">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1960">Bilgi alanı 2: nesne.</span><span class="sxs-lookup"><span data-stu-id="c7285-1960">Info Field 2: Object.</span></span>
- <span data-ttu-id="c7285-1961">Bilgi alanı 3: nesne arabelleği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1961">Info Field 3: Object buffer.</span></span>
- <span data-ttu-id="c7285-1962">Bilgi alanı 4: nesne uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c7285-1962">Info Field 4: Object length.</span></span>

### <a name="host-class-pima-object-transfer-abort"></a><span data-ttu-id="c7285-1963">Konak sınıfı Pima nesnesi aktarımı Iptali</span><span class="sxs-lookup"><span data-stu-id="c7285-1963">Host Class Pima Object Transfer Abort</span></span> 

#### <a name="ux_host_class_pima_object_transfer_abort"></a><span data-ttu-id="c7285-1964">ux_host_class_pima_object_transfer_abort</span><span class="sxs-lookup"><span data-stu-id="c7285-1964">ux_host_class_pima_object_transfer_abort</span></span>

<span data-ttu-id="c7285-1965">**Simge** ![ Konak sınıfı Pima nesne aktarımı Iptali simgesi](./media/user-guide/usbx-events/image143.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1965">**Icon** ![Host Class Pima Object Transfer Abort icon](./media/user-guide/usbx-events/image143.png)</span></span>

<span data-ttu-id="c7285-1966">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1966">**Description**</span></span>

<span data-ttu-id="c7285-1967">Bu olay bir USBX konak sınıfı Pima nesne aktarımı Iptali olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1967">This event represents a USBX Host Class Pima Object Transfer Abort Event.</span></span>

<span data-ttu-id="c7285-1968">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1968">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1969">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1969">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1970">Bilgi alanı 2: nesne tanıtıcısı.</span><span class="sxs-lookup"><span data-stu-id="c7285-1970">Info Field 2: Object handle.</span></span>
- <span data-ttu-id="c7285-1971">Bilgi alanı 3: nesne.</span><span class="sxs-lookup"><span data-stu-id="c7285-1971">Info Field 3: Object.</span></span>
- <span data-ttu-id="c7285-1972">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1972">Info Field 4: Not used.</span></span>

### <a name="host-class-pima-read"></a><span data-ttu-id="c7285-1973">Konak sınıfı Pima oku</span><span class="sxs-lookup"><span data-stu-id="c7285-1973">Host Class Pima Read</span></span> 

#### <a name="ux_host_class_pima_read"></a><span data-ttu-id="c7285-1974">ux_host_class_pima_read</span><span class="sxs-lookup"><span data-stu-id="c7285-1974">ux_host_class_pima_read</span></span>

<span data-ttu-id="c7285-1975">**Simge** ![ Konak sınıfı Pima oku simgesi](./media/user-guide/usbx-events/image144.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1975">**Icon** ![Host Class Pima Read icon](./media/user-guide/usbx-events/image144.png)</span></span>

<span data-ttu-id="c7285-1976">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1976">**Description**</span></span>

<span data-ttu-id="c7285-1977">Bu olay bir USBX konak sınıfı Pima okuma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1977">This event represents a USBX Host Class Pima Read Event.</span></span>

<span data-ttu-id="c7285-1978">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1978">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1979">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1979">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1980">Bilgi alanı 2: veri işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c7285-1980">Info Field 2: Data pointer.</span></span>
- <span data-ttu-id="c7285-1981">Bilgi alanı 3: veri uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c7285-1981">Info Field 3: Data length.</span></span>
- <span data-ttu-id="c7285-1982">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1982">Info Field 4: Not used.</span></span>

### <a name="host-class-pima-request-cancel"></a><span data-ttu-id="c7285-1983">Konak sınıfı Pima Isteği Iptali</span><span class="sxs-lookup"><span data-stu-id="c7285-1983">Host Class Pima Request Cancel</span></span> 

#### <a name="ux_host_class_pima_request_cancel"></a><span data-ttu-id="c7285-1984">ux_host_class_pima_request_cancel</span><span class="sxs-lookup"><span data-stu-id="c7285-1984">ux_host_class_pima_request_cancel</span></span>

<span data-ttu-id="c7285-1985">**Simge** ![ Konak sınıfı Pima Isteği Iptal simgesi](./media/user-guide/usbx-events/image145.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1985">**Icon** ![Host Class Pima Request Cancel icon](./media/user-guide/usbx-events/image145.png)</span></span>

<span data-ttu-id="c7285-1986">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1986">**Description**</span></span>

<span data-ttu-id="c7285-1987">Bu olay bir USBX konak sınıfı Pima Isteği Iptali olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1987">This event represents a USBX Host Class Pima Request Cancel Event.</span></span>

<span data-ttu-id="c7285-1988">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1988">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1989">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1989">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-1990">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1990">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-1991">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1991">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-1992">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-1992">Info Field 4: Not used.</span></span>

### <a name="host-class-pima-session-close"></a><span data-ttu-id="c7285-1993">Konak sınıfı Pima oturumu Kapat</span><span class="sxs-lookup"><span data-stu-id="c7285-1993">Host Class Pima Session Close</span></span> 

#### <a name="ux_host_class_pima_session_close"></a><span data-ttu-id="c7285-1994">ux_host_class_pima_session_close</span><span class="sxs-lookup"><span data-stu-id="c7285-1994">ux_host_class_pima_session_close</span></span>

<span data-ttu-id="c7285-1995">**Simge** ![ Ana sınıf Pima oturumu kapatma simgesi](./media/user-guide/usbx-events/image146.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-1995">**Icon** ![Host Class Pima Session Close icon](./media/user-guide/usbx-events/image146.png)</span></span>

<span data-ttu-id="c7285-1996">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-1996">**Description**</span></span>

<span data-ttu-id="c7285-1997">Bu olay bir USBX konak sınıfı Pima oturumu kapatma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-1997">This event represents a USBX Host Class Pima Session Close Event.</span></span>

<span data-ttu-id="c7285-1998">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-1998">**Information Fields**</span></span>

- <span data-ttu-id="c7285-1999">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-1999">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-2000">Bilgi alanı 2: Pima oturumu.</span><span class="sxs-lookup"><span data-stu-id="c7285-2000">Info Field 2: Pima session.</span></span>
- <span data-ttu-id="c7285-2001">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2001">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2002">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2002">Info Field 4: Not used.</span></span>

### <a name="host-class-pima-session-open"></a><span data-ttu-id="c7285-2003">Konak sınıfı Pima oturumu açık</span><span class="sxs-lookup"><span data-stu-id="c7285-2003">Host Class Pima Session Open</span></span> 

#### <a name="ux_host_class_pima_session_open"></a><span data-ttu-id="c7285-2004">ux_host_class_pima_session_open</span><span class="sxs-lookup"><span data-stu-id="c7285-2004">ux_host_class_pima_session_open</span></span>

<span data-ttu-id="c7285-2005">**Simge** ![ Konak sınıfı Pima oturumu açma simgesi](./media/user-guide/usbx-events/image147.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2005">**Icon** ![Host Class Pima Session Open icon](./media/user-guide/usbx-events/image147.png)</span></span>

<span data-ttu-id="c7285-2006">**Açıklama** Bu olay bir USBX konak sınıfı Pima oturum açma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2006">**Description** This event represents a USBX Host Class Pima Session Open Event.</span></span>

<span data-ttu-id="c7285-2007">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2007">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2008">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-2008">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-2009">Bilgi alanı 2: Pima oturumu.</span><span class="sxs-lookup"><span data-stu-id="c7285-2009">Info Field 2: Pima session.</span></span>
- <span data-ttu-id="c7285-2010">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2010">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2011">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2011">Info Field 4: Not used.</span></span>

### <a name="host-class-pima-storage-ids-get"></a><span data-ttu-id="c7285-2012">Konak sınıfı Pima depolama kimliklerini al</span><span class="sxs-lookup"><span data-stu-id="c7285-2012">Host Class Pima Storage Ids Get</span></span> 

#### <a name="ux_host_class_pima_session_ids_get"></a><span data-ttu-id="c7285-2013">ux_host_class_pima_session_ids_get</span><span class="sxs-lookup"><span data-stu-id="c7285-2013">ux_host_class_pima_session_ids_get</span></span>

<span data-ttu-id="c7285-2014">**Simge** ![ Konak sınıfı Pima depolama kimlikleri al simgesi](./media/user-guide/usbx-events/image148.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2014">**Icon** ![Host Class Pima Storage Ids Get icon](./media/user-guide/usbx-events/image148.png)</span></span>

<span data-ttu-id="c7285-2015">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2015">**Description**</span></span>

<span data-ttu-id="c7285-2016">Bu olay bir USBX konak sınıfı Pima depolama kimlikleri al olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2016">This event represents a USBX Host Class Pima Storage Ids Get Event.</span></span>

<span data-ttu-id="c7285-2017">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2017">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2018">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-2018">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-2019">NFO alanı 2: depolama KIMLIĞI dizisi.</span><span class="sxs-lookup"><span data-stu-id="c7285-2019">nfo Field 2: Storage ID array.</span></span>
- <span data-ttu-id="c7285-2020">Bilgi alanı 3: depolama KIMLIĞI uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c7285-2020">Info Field 3: Storage ID length.</span></span>
<span data-ttu-id="c7285-2021">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2021">Info Field 4: Not used.</span></span>

### <a name="host-class-pima-storage-info-get"></a><span data-ttu-id="c7285-2022">Konak sınıfı Pima depolama bilgileri Get</span><span class="sxs-lookup"><span data-stu-id="c7285-2022">Host Class Pima Storage Info Get</span></span> 

#### <a name="ux_host_class_pima_storage_info_get"></a><span data-ttu-id="c7285-2023">ux_host_class_pima_storage_info_get</span><span class="sxs-lookup"><span data-stu-id="c7285-2023">ux_host_class_pima_storage_info_get</span></span>

<span data-ttu-id="c7285-2024">**Simge** ![ Konak sınıfı Pima depolama bilgileri al simgesi](./media/user-guide/usbx-events/image149.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2024">**Icon** ![Host Class Pima Storage Info Get icon](./media/user-guide/usbx-events/image149.png)</span></span>

<span data-ttu-id="c7285-2025">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2025">**Description**</span></span>

<span data-ttu-id="c7285-2026">Bu olay bir USBX konak sınıfı Pima depolama bilgi al olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2026">This event represents a USBX Host Class Pima Storage Info Get Event.</span></span>

<span data-ttu-id="c7285-2027">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2027">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2028">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-2028">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-2029">Bilgi alanı 2: depolama KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="c7285-2029">Info Field 2: Storage ID.</span></span>
- <span data-ttu-id="c7285-2030">Bilgi alanı 3: depolama.</span><span class="sxs-lookup"><span data-stu-id="c7285-2030">Info Field 3: Storage.</span></span>
- <span data-ttu-id="c7285-2031">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2031">Info Field 4: Not used.</span></span>

### <a name="host-class-pima-thumb-get"></a><span data-ttu-id="c7285-2032">Ana sınıf Pima parmak izi al</span><span class="sxs-lookup"><span data-stu-id="c7285-2032">Host Class Pima Thumb Get</span></span> 

#### <a name="ux_host_class_pima_thumb_get"></a><span data-ttu-id="c7285-2033">ux_host_class_pima_thumb_get</span><span class="sxs-lookup"><span data-stu-id="c7285-2033">ux_host_class_pima_thumb_get</span></span>

<span data-ttu-id="c7285-2034">**Simge** ![ Konak sınıfı Pima Thumb al simgesi](./media/user-guide/usbx-events/image150.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2034">**Icon** ![Host Class Pima Thumb Get icon](./media/user-guide/usbx-events/image150.png)</span></span>

<span data-ttu-id="c7285-2035">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2035">**Description**</span></span>

<span data-ttu-id="c7285-2036">Bu olay, nx_tcp_server_socket_unaccept aracılığıyla bir TCP sunucusu bağlantısının kabul edilmemesine yönelik temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2036">This event represents unaccepting a TCP server connection via nx_tcp_server_socket_unaccept.</span></span>

<span data-ttu-id="c7285-2037">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2037">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-2038">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-2038">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-2039">Bilgi alanı 2: nesne tanıtıcısı.</span><span class="sxs-lookup"><span data-stu-id="c7285-2039">Info Field 2: Object handle.</span></span>
- <span data-ttu-id="c7285-2040">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2040">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2041">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2041">Info Field 4: Not used.</span></span>

### <a name="host-class-pima-write"></a><span data-ttu-id="c7285-2042">Konak sınıfı Pima yazma</span><span class="sxs-lookup"><span data-stu-id="c7285-2042">Host Class Pima Write</span></span> 

#### <a name="ux_host_class_pima_thumb_get"></a><span data-ttu-id="c7285-2043">ux_host_class_pima_thumb_get</span><span class="sxs-lookup"><span data-stu-id="c7285-2043">ux_host_class_pima_thumb_get</span></span>

<span data-ttu-id="c7285-2044">**Simge** ![ Konak sınıfı Pima yazma simgesi](./media/user-guide/usbx-events/image151.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2044">**Icon** ![Host Class Pima Write icon](./media/user-guide/usbx-events/image151.png)</span></span>

<span data-ttu-id="c7285-2045">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2045">**Description**</span></span>

<span data-ttu-id="c7285-2046">Bu olay bir USBX konak sınıfını Pima yazmayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2046">This event represents a USBX Host Class Pima Write.</span></span>

<span data-ttu-id="c7285-2047">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2047">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2048">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-2048">Info Field 1: Class Instance.</span></span>
- <span data-ttu-id="c7285-2049">Bilgi alanı 2: veri işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c7285-2049">Info Field 2: Data pointer.</span></span>
- <span data-ttu-id="c7285-2050">Bilgi alanı 3: veri uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c7285-2050">Info Field 3: Data length.</span></span>
- <span data-ttu-id="c7285-2051">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2051">Info Field 4: Not used.</span></span>

### <a name="host-class-printer-activate"></a><span data-ttu-id="c7285-2052">Konak sınıfı yazıcısını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="c7285-2052">Host Class Printer Activate</span></span> 

#### <a name="ux_host_class_printer_activate"></a><span data-ttu-id="c7285-2053">ux_host_class_printer_activate</span><span class="sxs-lookup"><span data-stu-id="c7285-2053">ux_host_class_printer_activate</span></span>

<span data-ttu-id="c7285-2054">**Simge** ![ Konak sınıfı yazıcı etkinleştirme simgesi](./media/user-guide/usbx-events/image152.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2054">**Icon** ![Host Class Printer Activate icon](./media/user-guide/usbx-events/image152.png)</span></span>

<span data-ttu-id="c7285-2055">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2055">**Description**</span></span>

<span data-ttu-id="c7285-2056">Bu olay bir USBX konak sınıfı yazıcı etkinleştirme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2056">This event represents a USBX Host Class Printer Activate Event.</span></span>

<span data-ttu-id="c7285-2057">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2057">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2058">Bilgi alanı 1: IP örneğine yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c7285-2058">Info Field 1: Pointer to IP instance.</span></span>
- <span data-ttu-id="c7285-2059">Bilgi alanı 2: yuva Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c7285-2059">Info Field 2: Pointer to socket.</span></span>
- <span data-ttu-id="c7285-2060">Bilgi alanı 3: hizmet türü.</span><span class="sxs-lookup"><span data-stu-id="c7285-2060">Info Field 3: Type of service.</span></span>
- <span data-ttu-id="c7285-2061">Bilgi alanı 4: pencere boyutunu al.</span><span class="sxs-lookup"><span data-stu-id="c7285-2061">Info Field 4: Receive window size.</span></span>

### <a name="host-class-printer-deactivate"></a><span data-ttu-id="c7285-2062">Konak sınıfı yazıcısını devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="c7285-2062">Host Class Printer Deactivate</span></span> 

#### <a name="ux_host_class_printer_deactivate"></a><span data-ttu-id="c7285-2063">ux_host_class_printer_deactivate</span><span class="sxs-lookup"><span data-stu-id="c7285-2063">ux_host_class_printer_deactivate</span></span>

<span data-ttu-id="c7285-2064">**Simge** ![ Konak sınıfı yazıcı devre dışı simgesi](./media/user-guide/usbx-events/image153.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2064">**Icon** ![Host Class Printer Deactivate icon](./media/user-guide/usbx-events/image153.png)</span></span>

<span data-ttu-id="c7285-2065">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2065">**Description**</span></span>

<span data-ttu-id="c7285-2066">Bu olay bir USBX konak sınıfı yazıcısı devre dışı bırakma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2066">This event represents a USBX Host Class Printer Deactivate Event.</span></span>

<span data-ttu-id="c7285-2067">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2067">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2068">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-2068">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-2069">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2069">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-2070">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2070">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2071">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2071">Info Field 4: Not used.</span></span>

### <a name="host-class-printer-name-get"></a><span data-ttu-id="c7285-2072">Konak sınıfı yazıcı adı Al</span><span class="sxs-lookup"><span data-stu-id="c7285-2072">Host Class Printer Name Get</span></span> 

#### <a name="ux_host_class_printer_name_get"></a><span data-ttu-id="c7285-2073">ux_host_class_printer_name_get</span><span class="sxs-lookup"><span data-stu-id="c7285-2073">ux_host_class_printer_name_get</span></span>

<span data-ttu-id="c7285-2074">**Simge** ![ Konak sınıfı yazıcı adı Al simgesi](./media/user-guide/usbx-events/image154.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2074">**Icon** ![Host Class Printer Name Get icon](./media/user-guide/usbx-events/image154.png)</span></span>

<span data-ttu-id="c7285-2075">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2075">**Description**</span></span>

<span data-ttu-id="c7285-2076">Bu olay bir USBX konak sınıfı yazıcı adı Al olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2076">This event represents a USBX Host Class Printer Name Get Event.</span></span>

<span data-ttu-id="c7285-2077">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2077">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-2078">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-2078">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-2079">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2079">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-2080">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2080">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2081">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2081">Info Field 4: Not used.</span></span>

### <a name="host-class-printer-read"></a><span data-ttu-id="c7285-2082">Konak sınıfı yazıcısını oku</span><span class="sxs-lookup"><span data-stu-id="c7285-2082">Host Class Printer Read</span></span> 

#### <a name="ux_host_class_printer_read"></a><span data-ttu-id="c7285-2083">ux_host_class_printer_read</span><span class="sxs-lookup"><span data-stu-id="c7285-2083">ux_host_class_printer_read</span></span>

<span data-ttu-id="c7285-2084">**Simge** ![ Ana bilgisayar sınıfı yazıcı okuma simgesi](./media/user-guide/usbx-events/image155.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2084">**Icon** ![Host Class Printer Read icon](./media/user-guide/usbx-events/image155.png)</span></span>

<span data-ttu-id="c7285-2085">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2085">**Description**</span></span>

<span data-ttu-id="c7285-2086">Bu olay bir USBX ana bilgisayar sınıfı yazıcı okuma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2086">This event represents a USBX Host Class Printer Read Event.</span></span>

<span data-ttu-id="c7285-2087">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2087">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2088">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-2088">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-2089">Bilgi alanı 2: veri işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c7285-2089">Info Field 2: Data pointer.</span></span>
- <span data-ttu-id="c7285-2090">Bilgi alanı 3: Istenen uzunluk.</span><span class="sxs-lookup"><span data-stu-id="c7285-2090">Info Field 3: Requested length.</span></span>
- <span data-ttu-id="c7285-2091">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2091">Info Field 4: Not used.</span></span>

### <a name="host-class-printer-soft-reset"></a><span data-ttu-id="c7285-2092">Konak sınıfı yazıcı yazılımdan sıfırlama</span><span class="sxs-lookup"><span data-stu-id="c7285-2092">Host Class Printer Soft Reset</span></span> 

#### <a name="ux_host_class_printer_soft_reset"></a><span data-ttu-id="c7285-2093">ux_host_class_printer_soft_reset</span><span class="sxs-lookup"><span data-stu-id="c7285-2093">ux_host_class_printer_soft_reset</span></span>

<span data-ttu-id="c7285-2094">**Simge** ![ Konak sınıfı yazıcı geçici sıfırlama simgesi](./media/user-guide/usbx-events/image156.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2094">**Icon** ![Host Class Printer Soft Reset icon](./media/user-guide/usbx-events/image156.png)</span></span>

<span data-ttu-id="c7285-2095">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2095">**Description**</span></span>

<span data-ttu-id="c7285-2096">Bu olay bir USBX konak sınıfı yazıcı geçici sıfırlama olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2096">This event represents a USBX Host Class Printer Soft Reset Event.</span></span>

<span data-ttu-id="c7285-2097">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2097">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2098">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-2098">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-2099">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2099">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-2100">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2100">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2101">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2101">Info Field 4: Not used.</span></span>

### <a name="host-class-printer-status-get"></a><span data-ttu-id="c7285-2102">Konak sınıfı yazıcı durumu Al</span><span class="sxs-lookup"><span data-stu-id="c7285-2102">Host Class Printer Status Get</span></span> 

#### <a name="ux_host_class_printer_status_get"></a><span data-ttu-id="c7285-2103">ux_host_class_printer_status_get</span><span class="sxs-lookup"><span data-stu-id="c7285-2103">ux_host_class_printer_status_get</span></span>

<span data-ttu-id="c7285-2104">**Simge** ![ Konak sınıfı yazıcı durumu Al simgesi](./media/user-guide/usbx-events/image157.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2104">**Icon** ![Host Class Printer Status Get icon](./media/user-guide/usbx-events/image157.png)</span></span>

<span data-ttu-id="c7285-2105">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2105">**Description**</span></span>

<span data-ttu-id="c7285-2106">Bu olay bir USBX konak sınıfı yazıcı durumu Al olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2106">This event represents a USBX Host Class Printer Status Get Event.</span></span>

<span data-ttu-id="c7285-2107">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2107">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2108">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-2108">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-2109">Bilgi alanı 2: yazıcı durumu.</span><span class="sxs-lookup"><span data-stu-id="c7285-2109">Info Field 2: Printer status.</span></span>
- <span data-ttu-id="c7285-2110">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2110">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2111">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2111">Info Field 4: Not used.</span></span>

### <a name="host-class-printer-write"></a><span data-ttu-id="c7285-2112">Ana bilgisayar sınıfı yazıcı yazma</span><span class="sxs-lookup"><span data-stu-id="c7285-2112">Host Class Printer Write</span></span> 

#### <a name="ux_host_class_printer_write"></a><span data-ttu-id="c7285-2113">ux_host_class_printer_write</span><span class="sxs-lookup"><span data-stu-id="c7285-2113">ux_host_class_printer_write</span></span>

<span data-ttu-id="c7285-2114">**Simge** ![ Konak sınıfı yazıcı yazma simgesi](./media/user-guide/usbx-events/image158.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2114">**Icon** ![Host Class Printer Write icon](./media/user-guide/usbx-events/image158.png)</span></span>

<span data-ttu-id="c7285-2115">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2115">**Description**</span></span>

<span data-ttu-id="c7285-2116">Bu olay, bir USBX konak sınıfı yazıcısını yazmayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2116">This event represents a USBX Host Class Printer Write.</span></span>

<span data-ttu-id="c7285-2117">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2117">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-2118">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-2118">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-2119">Bilgi alanı 2: veri işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c7285-2119">Info Field 2: Data pointer.</span></span>
- <span data-ttu-id="c7285-2120">Bilgi alanı 3: Istenen uzunluk.</span><span class="sxs-lookup"><span data-stu-id="c7285-2120">Info Field 3: Requested length.</span></span>
- <span data-ttu-id="c7285-2121">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2121">Info Field 4: Not used.</span></span>

### <a name="host-class-prolific-activate"></a><span data-ttu-id="c7285-2122">Konak sınıfı Prolific etkinleştir</span><span class="sxs-lookup"><span data-stu-id="c7285-2122">Host Class Prolific Activate</span></span> 

#### <a name="ux_host_class_prolific_activate"></a><span data-ttu-id="c7285-2123">ux_host_class_prolific_activate</span><span class="sxs-lookup"><span data-stu-id="c7285-2123">ux_host_class_prolific_activate</span></span> 

<span data-ttu-id="c7285-2124">**Simge** ![ Konak sınıfı Prolific etkinleştirme simgesi](./media/user-guide/usbx-events/image159.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2124">**Icon** ![Host Class Prolific Activate icon](./media/user-guide/usbx-events/image159.png)</span></span>

<span data-ttu-id="c7285-2125">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2125">**Description**</span></span>

<span data-ttu-id="c7285-2126">Bu olay bir USBX konak sınıfı Prolific Activate olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2126">This event represents a USBX Host Class Prolific Activate Event.</span></span>

<span data-ttu-id="c7285-2127">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2127">**Information Fields**</span></span> 

- <span data-ttu-id="c7285-2128">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-2128">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-2129">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2129">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-2130">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2130">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2131">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2131">Info Field 4: Not used.</span></span>

### <a name="host-class-prolific-deactivate"></a><span data-ttu-id="c7285-2132">Ana bilgisayar sınıfı Prolifik devre dışı</span><span class="sxs-lookup"><span data-stu-id="c7285-2132">Host Class Prolific Deactivate</span></span> 

#### <a name="ux_host_class_prolific_deactivate"></a><span data-ttu-id="c7285-2133">ux_host_class_prolific_deactivate</span><span class="sxs-lookup"><span data-stu-id="c7285-2133">ux_host_class_prolific_deactivate</span></span> 

<span data-ttu-id="c7285-2134">**Simge** ![ Konak sınıfı Prolific devre dışı bırakma simgesi](./media/user-guide/usbx-events/image160.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2134">**Icon** ![Host Class Prolific Deactivate icon](./media/user-guide/usbx-events/image160.png)</span></span>

<span data-ttu-id="c7285-2135">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2135">**Description**</span></span>

<span data-ttu-id="c7285-2136">Bu olay bir USBX konak sınıfı Prolific Deactivate olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2136">This event represents a USBX Host Class Prolific Deactivate Event.</span></span>

<span data-ttu-id="c7285-2137">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2137">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2138">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-2138">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-2139">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2139">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-2140">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2140">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2141">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2141">Info Field 4: Not used.</span></span>

### <a name="host-class-prolific-ioctl-abort-in-pipe"></a><span data-ttu-id="c7285-2142">Ana bilgisayar sınıfı işlem kanalında IOCTL Iptali</span><span class="sxs-lookup"><span data-stu-id="c7285-2142">Host Class Prolific Ioctl Abort In Pipe</span></span> 

#### <a name="ux_host_class_prolific_ioctl_abort_in_pipe"></a><span data-ttu-id="c7285-2143">ux_host_class_prolific_ioctl_abort_in_pipe</span><span class="sxs-lookup"><span data-stu-id="c7285-2143">ux_host_class_prolific_ioctl_abort_in_pipe</span></span>

<span data-ttu-id="c7285-2144">**Simge** ![ Kanal simgesinde ana bilgisayar sınıfı proo C T L durdur](./media/user-guide/usbx-events/image161.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2144">**Icon** ![Host Class Prolific I O C T L Abort In Pipe icon](./media/user-guide/usbx-events/image161.png)</span></span>

<span data-ttu-id="c7285-2145">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2145">**Description**</span></span>

<span data-ttu-id="c7285-2146">Bu olay, kanal olayında bir USBX ana bilgisayar sınıfını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2146">This event represents a USBX Host Class Prolific Ioctl Abort In Pipe Event.</span></span>

<span data-ttu-id="c7285-2147">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2147">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2148">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-2148">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-2149">Bilgi alanı 2: uç nokta.</span><span class="sxs-lookup"><span data-stu-id="c7285-2149">Info Field 2: Endpoint.</span></span>
- <span data-ttu-id="c7285-2150">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2150">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2151">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2151">Info Field 4: Not used.</span></span>

### <a name="host-class-prolific-ioctl-abort-out-pipe"></a><span data-ttu-id="c7285-2152">Konak sınıfı Prolific IOCTL durdurma kanalı</span><span class="sxs-lookup"><span data-stu-id="c7285-2152">Host Class Prolific Ioctl Abort Out Pipe</span></span> 

#### <a name="ux_host_class_prolific_ioctl_abort_out_pipe"></a><span data-ttu-id="c7285-2153">ux_host_class_prolific_ioctl_abort_out_pipe</span><span class="sxs-lookup"><span data-stu-id="c7285-2153">ux_host_class_prolific_ioctl_abort_out_pipe</span></span>

<span data-ttu-id="c7285-2154">**Simge** ![ Ana bilgisayar sınıfı proo C T L m ı Durdur kanal simgesi](./media/user-guide/usbx-events/image162.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2154">**Icon** ![Host Class Prolific I O C T L Abort Out Pipe icon](./media/user-guide/usbx-events/image162.png)</span></span>

<span data-ttu-id="c7285-2155">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2155">**Description**</span></span>

<span data-ttu-id="c7285-2156">Bu olay, bir USBX konak sınıfı Prolific IOCTL durdurma kanalı olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2156">This event represents a USBX Host Class Prolific Ioctl Abort Out Pipe Event.</span></span>

<span data-ttu-id="c7285-2157">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2157">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2158">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-2158">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-2159">Bilgi alanı 2: uç nokta.</span><span class="sxs-lookup"><span data-stu-id="c7285-2159">Info Field 2: Endpoint.</span></span>
- <span data-ttu-id="c7285-2160">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2160">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2161">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2161">Info Field 4: Not used.</span></span>

### <a name="host-class-prolific-ioctl-get-device-status"></a><span data-ttu-id="c7285-2162">Konak sınıfı Prolific IOCTL cihaz durumunu al</span><span class="sxs-lookup"><span data-stu-id="c7285-2162">Host Class Prolific Ioctl Get Device Status</span></span> 

#### <a name="ux_host_class_prolific_ioctl_get_device_status"></a><span data-ttu-id="c7285-2163">ux_host_class_prolific_ioctl_get_device_status</span><span class="sxs-lookup"><span data-stu-id="c7285-2163">ux_host_class_prolific_ioctl_get_device_status</span></span>

<span data-ttu-id="c7285-2164">**Simge** ![ Konak sınıfı Prolific g T C T L bir cihaz durumu simgesi al](./media/user-guide/usbx-events/image163.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2164">**Icon** ![Host Class Prolific I O C T L Get Device Status icon](./media/user-guide/usbx-events/image163.png)</span></span>

<span data-ttu-id="c7285-2165">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2165">**Description**</span></span>

<span data-ttu-id="c7285-2166">Bu olay bir USBX konak sınıfı Prolific IOCTL Get cihaz durumu olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2166">This event represents a USBX Host Class Prolific Ioctl Get Device Status Event.</span></span>

<span data-ttu-id="c7285-2167">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2167">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2168">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-2168">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-2169">Bilgi alanı 2: cihaz durumu.</span><span class="sxs-lookup"><span data-stu-id="c7285-2169">Info Field 2: Device status.</span></span>
- <span data-ttu-id="c7285-2170">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2170">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2171">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2171">Info Field 4: Not used.</span></span>

### <a name="host-class-prolific-ioctl-get-line-coding"></a><span data-ttu-id="c7285-2172">Konak sınıfı Prolific IOCTL al satırı kodlama</span><span class="sxs-lookup"><span data-stu-id="c7285-2172">Host Class Prolific Ioctl Get Line Coding</span></span> 

#### <a name="ux_host_class_prolific_ioctl_get_line_coding"></a><span data-ttu-id="c7285-2173">ux_host_class_prolific_ioctl_get_line_coding</span><span class="sxs-lookup"><span data-stu-id="c7285-2173">ux_host_class_prolific_ioctl_get_line_coding</span></span>

<span data-ttu-id="c7285-2174">**Simge** ![ Konak sınıfı Prolific ı T C T L Class for satırı kodlama simgesi](./media/user-guide/usbx-events/image164.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2174">**Icon** ![Host Class Prolific I O C T L Get Line Coding icon](./media/user-guide/usbx-events/image164.png)</span></span>

<span data-ttu-id="c7285-2175">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2175">**Description**</span></span>

<span data-ttu-id="c7285-2176">Bu olay, bir USBX konak sınıfı Prolific IOCTL Get satırı kodlama olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2176">This event represents a USBX Host Class Prolific Ioctl Get Line Coding Event.</span></span>

<span data-ttu-id="c7285-2177">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2177">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2178">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-2178">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-2179">Bilgi alanı 2: parametre.</span><span class="sxs-lookup"><span data-stu-id="c7285-2179">Info Field 2: Parameter.</span></span>
- <span data-ttu-id="c7285-2180">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2180">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2181">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2181">Info Field 4: Not used.</span></span>

### <a name="host-class-prolific-ioctl-purge"></a><span data-ttu-id="c7285-2182">Konak sınıfı Prolific IOCTL Temizleme</span><span class="sxs-lookup"><span data-stu-id="c7285-2182">Host Class Prolific Ioctl Purge</span></span> 

#### <a name="ux_host_class_prolific_ioctl_purge"></a><span data-ttu-id="c7285-2183">ux_host_class_prolific_ioctl_purge</span><span class="sxs-lookup"><span data-stu-id="c7285-2183">ux_host_class_prolific_ioctl_purge</span></span>

<span data-ttu-id="c7285-2184">**Simge** ![ Konak sınıfı Prolific IOCTL Temizleme simgesi](./media/user-guide/usbx-events/image165.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2184">**Icon** ![Host Class Prolific Ioctl Purge icon](./media/user-guide/usbx-events/image165.png)</span></span>

<span data-ttu-id="c7285-2185">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2185">**Description**</span></span>

<span data-ttu-id="c7285-2186">Bu olay bir USBX konak sınıfı Prolific IOCTL Temizleme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2186">This event represents a USBX Host Class Prolific Ioctl Purge Event.</span></span>

<span data-ttu-id="c7285-2187">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2187">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2188">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-2188">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-2189">Bilgi alanı 2: parametre.</span><span class="sxs-lookup"><span data-stu-id="c7285-2189">Info Field 2: Parameter.</span></span>
- <span data-ttu-id="c7285-2190">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2190">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2191">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2191">Info Field 4: Not used.</span></span>

### <a name="host-class-prolific-ioctl-report-device"></a><span data-ttu-id="c7285-2192">Konak sınıfı Prolific IOCTL rapor cihazı</span><span class="sxs-lookup"><span data-stu-id="c7285-2192">Host Class Prolific Ioctl Report Device</span></span> 

#### <a name="ux_host_class_prolific_ioctl_report_device"></a><span data-ttu-id="c7285-2193">ux_host_class_prolific_ioctl_report_device</span><span class="sxs-lookup"><span data-stu-id="c7285-2193">ux_host_class_prolific_ioctl_report_device</span></span>

<span data-ttu-id="c7285-2194">**Simge** ![ Konak sınıfı Prolific ı T C T m rapor cihaz simgesi](./media/user-guide/usbx-events/image166.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2194">**Icon** ![Host Class Prolific I O C T L Report Device icon](./media/user-guide/usbx-events/image166.png)</span></span>

<span data-ttu-id="c7285-2195">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2195">**Description**</span></span>

<span data-ttu-id="c7285-2196">Bu olay bir USBX konak sınıfı Prolific IOCTL rapor cihaz durumu değişiklik olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2196">This event represents a USBX Host Class Prolific Ioctl Report Device Status Change Event.</span></span>

<span data-ttu-id="c7285-2197">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2197">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2198">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-2198">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-2199">Bilgi alanı 2: parametre.</span><span class="sxs-lookup"><span data-stu-id="c7285-2199">Info Field 2: Parameter.</span></span>
- <span data-ttu-id="c7285-2200">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2200">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2201">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2201">Info Field 4: Not used.</span></span>

### <a name="host-class-prolific-ioctl-send-break"></a><span data-ttu-id="c7285-2202">Konak sınıfı Prolific IOCTL gönderme kesmesi</span><span class="sxs-lookup"><span data-stu-id="c7285-2202">Host Class Prolific Ioctl Send Break</span></span> 

#### <a name="ux_host_class_prolific_ioctl_send_break"></a><span data-ttu-id="c7285-2203">ux_host_class_prolific_ioctl_send_break</span><span class="sxs-lookup"><span data-stu-id="c7285-2203">ux_host_class_prolific_ioctl_send_break</span></span>

<span data-ttu-id="c7285-2204">**Simge** ![ Konak sınıfı Prolific ı T C T L gönderme sonu simgesi](./media/user-guide/usbx-events/image167.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2204">**Icon** ![Host Class Prolific I O C T L Send Break icon](./media/user-guide/usbx-events/image167.png)</span></span>

<span data-ttu-id="c7285-2205">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2205">**Description**</span></span>

<span data-ttu-id="c7285-2206">Bu olay bir USBX konak sınıfı Prolific IOCTL gönderme kesmesi olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2206">This event represents a USBX Host Class Prolific Ioctl Send Break Event.</span></span>

<span data-ttu-id="c7285-2207">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2207">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2208">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-2208">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-2209">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2209">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-2210">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2210">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2211">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2211">Info Field 4: Not used.</span></span>

### <a name="host-class-prolific-ioctl-set-line-coding"></a><span data-ttu-id="c7285-2212">Konak sınıfı Prolific IOCTL kümesi satırı kodlama</span><span class="sxs-lookup"><span data-stu-id="c7285-2212">Host Class Prolific Ioctl Set Line Coding</span></span> 

#### <a name="ux_host_class_prolific_ioctl_set_line_coding"></a><span data-ttu-id="c7285-2213">ux_host_class_prolific_ioctl_set_line_coding</span><span class="sxs-lookup"><span data-stu-id="c7285-2213">ux_host_class_prolific_ioctl_set_line_coding</span></span>

<span data-ttu-id="c7285-2214">**Simge** ![ Konak sınıfı Prolific ı T C T L Class for satırı kodlama simgesi](./media/user-guide/usbx-events/image168.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2214">**Icon** ![Host Class Prolific I O C T L Set Line Coding icon](./media/user-guide/usbx-events/image168.png)</span></span>

<span data-ttu-id="c7285-2215">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2215">**Description**</span></span>

<span data-ttu-id="c7285-2216">Bu olay, bir USBX konak sınıfı Prolific IOCTL kümesi satırı kodlama olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2216">This event represents a USBX Host Class Prolific Ioctl Set Line Coding Event.</span></span>

<span data-ttu-id="c7285-2217">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2217">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2218">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-2218">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-2219">Bilgi alanı 2: parametre.</span><span class="sxs-lookup"><span data-stu-id="c7285-2219">Info Field 2: Parameter.</span></span>
- <span data-ttu-id="c7285-2220">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2220">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2221">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2221">Info Field 4: Not used.</span></span>

### <a name="host-class-prolific-ioctl-set-line-state"></a><span data-ttu-id="c7285-2222">Konak sınıfı Prolific IOCTL kümesi satır durumu</span><span class="sxs-lookup"><span data-stu-id="c7285-2222">Host Class Prolific Ioctl Set Line State</span></span> 

#### <a name="ux_host_class_prolific_ioctl_set_line_state"></a><span data-ttu-id="c7285-2223">ux_host_class_prolific_ioctl_set_line_state</span><span class="sxs-lookup"><span data-stu-id="c7285-2223">ux_host_class_prolific_ioctl_set_line_state</span></span>

<span data-ttu-id="c7285-2224">**Simge** ![ Konak sınıfı Prolific ı T C T L s satır durumu simgesi](./media/user-guide/usbx-events/image169.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2224">**Icon** ![Host Class Prolific I O C T L Set Line State icon](./media/user-guide/usbx-events/image169.png)</span></span>

<span data-ttu-id="c7285-2225">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2225">**Description**</span></span>

<span data-ttu-id="c7285-2226">Bu olay bir USBX konak sınıfı Prolific IOCTL kümesi satır durumu olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2226">This event represents a USBX Host Class Prolific Ioctl Set Line State Event.</span></span>

<span data-ttu-id="c7285-2227">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2227">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2228">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-2228">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-2229">Bilgi alanı 2: parametre.</span><span class="sxs-lookup"><span data-stu-id="c7285-2229">Info Field 2: Parameter.</span></span>
- <span data-ttu-id="c7285-2230">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2230">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2231">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2231">Info Field 4: Not used.</span></span>

### <a name="host-class-prolific-read"></a><span data-ttu-id="c7285-2232">Ana bilgisayar sınıfı okuma</span><span class="sxs-lookup"><span data-stu-id="c7285-2232">Host Class Prolific Read</span></span> 

#### <a name="ux_host_class_prolific_read"></a><span data-ttu-id="c7285-2233">ux_host_class_prolific_read</span><span class="sxs-lookup"><span data-stu-id="c7285-2233">ux_host_class_prolific_read</span></span>

<span data-ttu-id="c7285-2234">**Simge** ![ Konak sınıfı Prolific okuma simgesi](./media/user-guide/usbx-events/image170.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2234">**Icon** ![Host Class Prolific Read icon](./media/user-guide/usbx-events/image170.png)</span></span>

<span data-ttu-id="c7285-2235">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2235">**Description**</span></span>

<span data-ttu-id="c7285-2236">Bu olay bir USBX konak sınıfı için bir okuma olayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2236">This event represents a USBX Host Class Prolific Read Event.</span></span>

<span data-ttu-id="c7285-2237">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2237">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2238">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-2238">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-2239">Bilgi alanı 2: veri işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c7285-2239">Info Field 2: Data pointer.</span></span>
- <span data-ttu-id="c7285-2240">Bilgi alanı 3: Istenen uzunluk.</span><span class="sxs-lookup"><span data-stu-id="c7285-2240">Info Field 3: Requested length.</span></span>
- <span data-ttu-id="c7285-2241">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2241">Info Field 4: Not used.</span></span>

### <a name="host-class-prolific-reception-start"></a><span data-ttu-id="c7285-2242">Konak sınıfı Prolific alma başlangıcı</span><span class="sxs-lookup"><span data-stu-id="c7285-2242">Host Class Prolific Reception Start</span></span> 

#### <a name="ux_host_class_prolific_reception_start"></a><span data-ttu-id="c7285-2243">ux_host_class_prolific_reception_start</span><span class="sxs-lookup"><span data-stu-id="c7285-2243">ux_host_class_prolific_reception_start</span></span>

<span data-ttu-id="c7285-2244">**Simge** ![ Konak sınıfı Prolific alma başlangıç simgesi](./media/user-guide/usbx-events/image171.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2244">**Icon** ![Host Class Prolific Reception Start icon](./media/user-guide/usbx-events/image171.png)</span></span>

<span data-ttu-id="c7285-2245">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2245">**Description**</span></span>

<span data-ttu-id="c7285-2246">Bu olay bir USBX konak sınıfı Prolific alma başlangıç olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2246">This event represents a USBX Host Class Prolific Reception Start Event.</span></span>

<span data-ttu-id="c7285-2247">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2247">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2248">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-2248">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-2249">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2249">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-2250">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2250">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2251">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2251">Info Field 4: Not used.</span></span>

### <a name="host-class-prolific-reception-stop"></a><span data-ttu-id="c7285-2252">Konak sınıfı Prolific alımı durdur</span><span class="sxs-lookup"><span data-stu-id="c7285-2252">Host Class Prolific Reception Stop</span></span> 

#### <a name="ux_host_class_prolific_reception_stop"></a><span data-ttu-id="c7285-2253">ux_host_class_prolific_reception_stop</span><span class="sxs-lookup"><span data-stu-id="c7285-2253">ux_host_class_prolific_reception_stop</span></span>

<span data-ttu-id="c7285-2254">**Simge** ![ Konak sınıfı Prolific alımı durdurma simgesi](./media/user-guide/usbx-events/image172.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2254">**Icon** ![Host Class Prolific Reception Stop icon](./media/user-guide/usbx-events/image172.png)</span></span>

<span data-ttu-id="c7285-2255">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2255">**Description**</span></span>

<span data-ttu-id="c7285-2256">Bu olay bir USBX konak sınıfı Prolific alma durdurma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2256">This event represents a USBX Host Class Prolific Reception Stop Event.</span></span>

<span data-ttu-id="c7285-2257">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2257">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2258">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-2258">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-2259">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2259">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-2260">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2260">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2261">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2261">Info Field 4: Not used.</span></span>

### <a name="host-class-prolific-write"></a><span data-ttu-id="c7285-2262">Ana bilgisayar sınıfı başlangıç yazma</span><span class="sxs-lookup"><span data-stu-id="c7285-2262">Host Class Prolific Write</span></span> 

#### <a name="ux_host_class_prolific_write"></a><span data-ttu-id="c7285-2263">ux_host_class_prolific_write</span><span class="sxs-lookup"><span data-stu-id="c7285-2263">ux_host_class_prolific_write</span></span>

<span data-ttu-id="c7285-2264">**Simge** ![ Ana makine sınıfı başlangıç yazma simgesi](./media/user-guide/usbx-events/image173.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2264">**Icon** ![Host Class Prolific Write icon](./media/user-guide/usbx-events/image173.png)</span></span>

<span data-ttu-id="c7285-2265">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2265">**Description**</span></span>

<span data-ttu-id="c7285-2266">Bu olay bir USBX konak sınıfı Prolific yazma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2266">This event represents a USBX Host Class Prolific Write Event.</span></span>

<span data-ttu-id="c7285-2267">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2267">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2268">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-2268">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-2269">Bilgi alanı 2: veri işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c7285-2269">Info Field 2: Data pointer.</span></span>
- <span data-ttu-id="c7285-2270">Bilgi alanı 3: Istenen uzunluk.</span><span class="sxs-lookup"><span data-stu-id="c7285-2270">Info Field 3: Requested length.</span></span>
- <span data-ttu-id="c7285-2271">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2271">Info Field 4: Not used.</span></span>

### <a name="host-class-storage-activate"></a><span data-ttu-id="c7285-2272">Konak sınıfı depolamayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="c7285-2272">Host Class Storage Activate</span></span> 

#### <a name="ux_host_class_storage_activate"></a><span data-ttu-id="c7285-2273">ux_host_class_storage_activate</span><span class="sxs-lookup"><span data-stu-id="c7285-2273">ux_host_class_storage_activate</span></span>

<span data-ttu-id="c7285-2274">**Simge** ![ Konak sınıfı depolama etkinleştirme simgesi](./media/user-guide/usbx-events/image174.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2274">**Icon** ![Host Class Storage Activate icon](./media/user-guide/usbx-events/image174.png)</span></span>

<span data-ttu-id="c7285-2275">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2275">**Description**</span></span>

<span data-ttu-id="c7285-2276">Bu olay bir USBX konak sınıfı depolama etkinleştirme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2276">This event represents a USBX Host Class Storage Activate Event.</span></span>

<span data-ttu-id="c7285-2277">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2277">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2278">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-2278">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-2279">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2279">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-2280">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2280">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2281">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2281">Info Field 4: Not used.</span></span>

### <a name="host-class-storage-deactivate"></a><span data-ttu-id="c7285-2282">Konak sınıfı depolamayı devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="c7285-2282">Host Class Storage Deactivate</span></span> 

#### <a name="ux_host_class_storage_deactivate"></a><span data-ttu-id="c7285-2283">ux_host_class_storage_deactivate</span><span class="sxs-lookup"><span data-stu-id="c7285-2283">ux_host_class_storage_deactivate</span></span>

<span data-ttu-id="c7285-2284">**Simge** ![ Konak sınıfı depolamayı devre dışı bırakma simgesi](./media/user-guide/usbx-events/image175.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2284">**Icon** ![Host Class Storage Deactivate icon](./media/user-guide/usbx-events/image175.png)</span></span>

<span data-ttu-id="c7285-2285">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2285">**Description**</span></span>

<span data-ttu-id="c7285-2286">Bu olay bir USBX konak sınıfı depolaması devre dışı bırakma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2286">This event represents a USBX Host Class Storage Deactivate Event.</span></span>

<span data-ttu-id="c7285-2287">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2287">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2288">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-2288">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-2289">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2289">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-2290">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2290">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2291">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2291">Info Field 4: Not used.</span></span>

### <a name="host-class-storage-media-capacity-get"></a><span data-ttu-id="c7285-2292">Konak sınıfı depolama medyası kapasitesi al</span><span class="sxs-lookup"><span data-stu-id="c7285-2292">Host Class Storage Media Capacity Get</span></span> 

#### <a name="ux_host_class_storage_media_capacity_get"></a><span data-ttu-id="c7285-2293">ux_host_class_storage_media_capacity_get</span><span class="sxs-lookup"><span data-stu-id="c7285-2293">ux_host_class_storage_media_capacity_get</span></span>

<span data-ttu-id="c7285-2294">**Simge** ![ Konak sınıfı depolama medyası kapasitesi al simgesi](./media/user-guide/usbx-events/image176.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2294">**Icon** ![Host Class Storage Media Capacity Get icon](./media/user-guide/usbx-events/image176.png)</span></span>

<span data-ttu-id="c7285-2295">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2295">**Description**</span></span>

<span data-ttu-id="c7285-2296">Bu olay bir USBX konak sınıfı depolama medyası kapasitesini al olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2296">This event represents a USBX Host Class Storage Media Capacity Get Event.</span></span>

<span data-ttu-id="c7285-2297">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2297">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2298">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-2298">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-2299">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2299">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-2300">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2300">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2301">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2301">Info Field 4: Not used.</span></span>

### <a name="host-class-storage-media-format-capacity-get"></a><span data-ttu-id="c7285-2302">Konak sınıfı depolama medyası biçim kapasitesini al</span><span class="sxs-lookup"><span data-stu-id="c7285-2302">Host Class Storage Media Format Capacity Get</span></span>

#### <a name="ux_host_class_storage_media_format_capacity_get"></a><span data-ttu-id="c7285-2303">ux_host_class_storage_media_format_capacity_get</span><span class="sxs-lookup"><span data-stu-id="c7285-2303">ux_host_class_storage_media_format_capacity_get</span></span>

<span data-ttu-id="c7285-2304">**Simge** ![ Konak sınıfı depolama medya biçimi kapasitesi al simgesi](./media/user-guide/usbx-events/image177.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2304">**Icon** ![Host Class Storage Media Format Capacity Get icon](./media/user-guide/usbx-events/image177.png)</span></span>

<span data-ttu-id="c7285-2305">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2305">**Description**</span></span>

<span data-ttu-id="c7285-2306">Bu olay bir USBX konak sınıfı depolama medyası biçimlendirme kapasitesini al olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2306">This event represents a USBX Host Class Storage Media Format Capacity Get Event.</span></span>

<span data-ttu-id="c7285-2307">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2307">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2308">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-2308">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-2309">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2309">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-2310">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2310">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2311">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2311">Info Field 4: Not used.</span></span>

#### <a name="host-class-storage-media-mount"></a><span data-ttu-id="c7285-2312">Konak sınıfı depolama medyası bağlama</span><span class="sxs-lookup"><span data-stu-id="c7285-2312">Host Class Storage Media Mount</span></span> 

#### <a name="ux_host_class_storage_media_mount"></a><span data-ttu-id="c7285-2313">ux_host_class_storage_media_mount</span><span class="sxs-lookup"><span data-stu-id="c7285-2313">ux_host_class_storage_media_mount</span></span>

<span data-ttu-id="c7285-2314">**Simge** ![ Konak sınıfı depolama medyası bağlama simgesi](./media/user-guide/usbx-events/image178.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2314">**Icon** ![Host Class Storage Media Mount icon](./media/user-guide/usbx-events/image178.png)</span></span>

<span data-ttu-id="c7285-2315">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2315">**Description**</span></span>

<span data-ttu-id="c7285-2316">Bu olay bir USBX konak sınıfı depolama medyası bağlama olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2316">This event represents a USBX Host Class Storage Media Mount Event.</span></span>

<span data-ttu-id="c7285-2317">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2317">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2318">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-2318">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-2319">Bilgi alanı 2: sektör.</span><span class="sxs-lookup"><span data-stu-id="c7285-2319">Info Field 2: Sector.</span></span>
- <span data-ttu-id="c7285-2320">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2320">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2321">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2321">Info Field 4: Not used.</span></span>

### <a name="host-class-storage-media-open"></a><span data-ttu-id="c7285-2322">Konak sınıfı depolama medyası açık</span><span class="sxs-lookup"><span data-stu-id="c7285-2322">Host Class Storage Media Open</span></span> 

#### <a name="ux_host_class_storage_media_open"></a><span data-ttu-id="c7285-2323">ux_host_class_storage_media_open</span><span class="sxs-lookup"><span data-stu-id="c7285-2323">ux_host_class_storage_media_open</span></span>

<span data-ttu-id="c7285-2324">**Simge** ![ Konak sınıfı depolama medyası açık simgesi](./media/user-guide/usbx-events/image179.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2324">**Icon** ![Host Class Storage Media Open icon](./media/user-guide/usbx-events/image179.png)</span></span>

<span data-ttu-id="c7285-2325">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2325">**Description**</span></span>

<span data-ttu-id="c7285-2326">Bu olay bir USBX konak sınıfı depolama medyası açık olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2326">This event represents a USBX Host Class Storage Media Open Event.</span></span>

<span data-ttu-id="c7285-2327">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2327">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2328">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-2328">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-2329">Bilgi alanı 2: medya.</span><span class="sxs-lookup"><span data-stu-id="c7285-2329">Info Field 2: Media.</span></span>
- <span data-ttu-id="c7285-2330">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2330">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2331">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2331">Info Field 4: Not used.</span></span>

### <a name="host-class-storage-media-read"></a><span data-ttu-id="c7285-2332">Konak sınıfı depolama medyası okuma</span><span class="sxs-lookup"><span data-stu-id="c7285-2332">Host Class Storage Media Read</span></span> 

#### <a name="ux_host_class_storage_media_read"></a><span data-ttu-id="c7285-2333">ux_host_class_storage_media_read</span><span class="sxs-lookup"><span data-stu-id="c7285-2333">ux_host_class_storage_media_read</span></span>

<span data-ttu-id="c7285-2334">**Simge** ![ Konak sınıfı depolama medyası okuma simgesi](./media/user-guide/usbx-events/image180.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2334">**Icon** ![Host Class Storage Media Read icon](./media/user-guide/usbx-events/image180.png)</span></span>

<span data-ttu-id="c7285-2335">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2335">**Description**</span></span>

<span data-ttu-id="c7285-2336">Bu olay bir USBX konak sınıfı depolama medyası okuma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2336">This event represents a USBX Host Class Storage Media Read Event.</span></span>

<span data-ttu-id="c7285-2337">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2337">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2338">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-2338">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-2339">Bilgi alanı 2: kesim başlangıcı.</span><span class="sxs-lookup"><span data-stu-id="c7285-2339">Info Field 2: Sector start.</span></span>
- <span data-ttu-id="c7285-2340">Bilgi alanı 3: sektör sayısı.</span><span class="sxs-lookup"><span data-stu-id="c7285-2340">Info Field 3: Sector count.</span></span>
- <span data-ttu-id="c7285-2341">Bilgi alanı 4: veri işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c7285-2341">Info Field 4: Data pointer.</span></span>

### <a name="host-class-storage-media-write"></a><span data-ttu-id="c7285-2342">Konak sınıfı depolama medyası yazma</span><span class="sxs-lookup"><span data-stu-id="c7285-2342">Host Class Storage Media Write</span></span> 

#### <a name="ux_host_class_storage_media_write"></a><span data-ttu-id="c7285-2343">ux_host_class_storage_media_write</span><span class="sxs-lookup"><span data-stu-id="c7285-2343">ux_host_class_storage_media_write</span></span>

<span data-ttu-id="c7285-2344">**Simge** ![ Konak sınıfı depolama medyası yazma simgesi](./media/user-guide/usbx-events/image181.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2344">**Icon** ![Host Class Storage Media Write icon](./media/user-guide/usbx-events/image181.png)</span></span>

<span data-ttu-id="c7285-2345">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2345">**Description**</span></span>

<span data-ttu-id="c7285-2346">Bu olay bir USBX konak sınıfı depolama medyası yazma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2346">This event represents a USBX Host Class Storage Media Write Event.</span></span>

<span data-ttu-id="c7285-2347">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2347">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2348">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-2348">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-2349">Bilgi alanı 2: kesim başlangıcı.</span><span class="sxs-lookup"><span data-stu-id="c7285-2349">Info Field 2: Sector start.</span></span>
- <span data-ttu-id="c7285-2350">Bilgi alanı 3: sektör sayısı.</span><span class="sxs-lookup"><span data-stu-id="c7285-2350">Info Field 3: Sector count.</span></span>
- <span data-ttu-id="c7285-2351">Bilgi alanı 4: veri işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c7285-2351">Info Field 4: Data pointer.</span></span>

### <a name="host-class-storage-request-sense"></a><span data-ttu-id="c7285-2352">Konak sınıfı depolama Istek algılaması</span><span class="sxs-lookup"><span data-stu-id="c7285-2352">Host Class Storage Request Sense</span></span> 

#### <a name="ux_host_class_storage_request_sense"></a><span data-ttu-id="c7285-2353">ux_host_class_storage_request_sense</span><span class="sxs-lookup"><span data-stu-id="c7285-2353">ux_host_class_storage_request_sense</span></span>

<span data-ttu-id="c7285-2354">**Simge** ![ Konak sınıfı depolama Isteği algılama simgesi](./media/user-guide/usbx-events/image182.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2354">**Icon** ![Host Class Storage Request Sense icon](./media/user-guide/usbx-events/image182.png)</span></span>

<span data-ttu-id="c7285-2355">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2355">**Description**</span></span>

<span data-ttu-id="c7285-2356">Bu olay bir USBX konak sınıfı depolama Istek algılama olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2356">This event represents a USBX Host Class Storage Request Sense Event.</span></span>

<span data-ttu-id="c7285-2357">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2357">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2358">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-2358">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-2359">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2359">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-2360">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2360">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2361">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2361">Info Field 4: Not used.</span></span>

### <a name="host-class-storage-start-stop"></a><span data-ttu-id="c7285-2362">Konak sınıfı depolama başlatma durdurma</span><span class="sxs-lookup"><span data-stu-id="c7285-2362">Host Class Storage Start Stop</span></span> 

#### <a name="ux_host_class_storage_start_stop"></a><span data-ttu-id="c7285-2363">ux_host_class_storage_start_stop</span><span class="sxs-lookup"><span data-stu-id="c7285-2363">ux_host_class_storage_start_stop</span></span>

<span data-ttu-id="c7285-2364">**Simge** ![ Konak sınıfı depolama başlatma durdurma simgesi](./media/user-guide/usbx-events/image183.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2364">**Icon** ![Host Class Storage Start Stop icon](./media/user-guide/usbx-events/image183.png)</span></span>

<span data-ttu-id="c7285-2365">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2365">**Description**</span></span>

<span data-ttu-id="c7285-2366">Bu olay bir USBX konak sınıfı depolama başlangıç durdurma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2366">This event represents a USBX Host Class Storage Start Stop Event.</span></span>

<span data-ttu-id="c7285-2367">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2367">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2368">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-2368">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-2369">Bilgi alanı 2: durdurma sinyalini başlatın.</span><span class="sxs-lookup"><span data-stu-id="c7285-2369">Info Field 2: Start stop signal.</span></span>
- <span data-ttu-id="c7285-2370">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2370">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2371">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2371">Info Field 4: Not used.</span></span>

### <a name="host-class-storage-unit-ready-test"></a><span data-ttu-id="c7285-2372">Konak sınıfı depolama birimi için hazırlanma testi</span><span class="sxs-lookup"><span data-stu-id="c7285-2372">Host Class Storage Unit Ready Test</span></span> 

#### <a name="ux_host_class_storage_unit_ready_test"></a><span data-ttu-id="c7285-2373">ux_host_class_storage_unit_ready_test</span><span class="sxs-lookup"><span data-stu-id="c7285-2373">ux_host_class_storage_unit_ready_test</span></span>

<span data-ttu-id="c7285-2374">**Simge** ![ Konak sınıfı depolama birimi için Ready test simgesi](./media/user-guide/usbx-events/image184.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2374">**Icon** ![Host Class Storage Unit Ready Test icon](./media/user-guide/usbx-events/image184.png)</span></span>

<span data-ttu-id="c7285-2375">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2375">**Description**</span></span>

<span data-ttu-id="c7285-2376">Bu olay, bir USBX konak sınıfı depolama birimi için hazırlanma sınama olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2376">This event represents a USBX Host Class Storage Unit Ready Test Event.</span></span>

<span data-ttu-id="c7285-2377">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2377">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2378">Bilgi alanı 1: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-2378">Info Field 1: Class instance.</span></span>
- <span data-ttu-id="c7285-2379">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2379">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-2380">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2380">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2381">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2381">Info Field 4: Not used.</span></span>

### <a name="host-stack-class-instance-create"></a><span data-ttu-id="c7285-2382">Konak yığını sınıf örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="c7285-2382">Host Stack Class Instance Create</span></span> 

#### <a name="ux_host_class_instance_create"></a><span data-ttu-id="c7285-2383">ux_host_class_instance_create</span><span class="sxs-lookup"><span data-stu-id="c7285-2383">ux_host_class_instance_create</span></span>

<span data-ttu-id="c7285-2384">**Simge** ![ Konak yığını sınıf örneği oluşturma simgesi](./media/user-guide/usbx-events/image185.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2384">**Icon** ![Host Stack Class Instance Create icon](./media/user-guide/usbx-events/image185.png)</span></span>

<span data-ttu-id="c7285-2385">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2385">**Description**</span></span>

<span data-ttu-id="c7285-2386">Bu olay bir USBX konak yığını sınıf örneği oluşturma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2386">This event represents a USBX Host Stack Class Instance Create Event.</span></span>

<span data-ttu-id="c7285-2387">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2387">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2388">Bilgi alanı 1: sınıf.</span><span class="sxs-lookup"><span data-stu-id="c7285-2388">Info Field 1: Class.</span></span>
- <span data-ttu-id="c7285-2389">Bilgi alanı 2: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-2389">Info Field 2: Class Instance.</span></span>
- <span data-ttu-id="c7285-2390">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2390">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2391">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2391">Info Field 4: Not used.</span></span>

### <a name="host-stack-class-instance-destroy"></a><span data-ttu-id="c7285-2392">Konak yığını sınıf örneği yok etme</span><span class="sxs-lookup"><span data-stu-id="c7285-2392">Host Stack Class Instance Destroy</span></span> 

#### <a name="ux_host_class_instance_create"></a><span data-ttu-id="c7285-2393">ux_host_class_instance_create</span><span class="sxs-lookup"><span data-stu-id="c7285-2393">ux_host_class_instance_create</span></span>

<span data-ttu-id="c7285-2394">**Simge** ![ Konak yığını sınıf örneği yok etme simgesi](./media/user-guide/usbx-events/image186.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2394">**Icon** ![Host Stack Class Instance Destroy icon](./media/user-guide/usbx-events/image186.png)</span></span>

<span data-ttu-id="c7285-2395">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2395">**Description**</span></span>

<span data-ttu-id="c7285-2396">Bu olay bir USBX konak yığın sınıfı örneği yok etme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2396">This event represents a USBX Host Stack Class Instance Destroy Event.</span></span>

<span data-ttu-id="c7285-2397">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2397">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2398">Bilgi alanı 1: sınıf.</span><span class="sxs-lookup"><span data-stu-id="c7285-2398">Info Field 1: Class.</span></span>
- <span data-ttu-id="c7285-2399">Bilgi alanı 2: sınıf örneği.</span><span class="sxs-lookup"><span data-stu-id="c7285-2399">Info Field 2: Class Instance.</span></span>
- <span data-ttu-id="c7285-2400">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2400">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2401">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2401">Info Field 4: Not used.</span></span>

### <a name="host-stack-configuration-delete"></a><span data-ttu-id="c7285-2402">Konak yığını yapılandırması silme</span><span class="sxs-lookup"><span data-stu-id="c7285-2402">Host Stack Configuration Delete</span></span> 

#### <a name="ux_host_class_configuration_delete"></a><span data-ttu-id="c7285-2403">ux_host_class_configuration_delete</span><span class="sxs-lookup"><span data-stu-id="c7285-2403">ux_host_class_configuration_delete</span></span>

<span data-ttu-id="c7285-2404">**Simge** ![ Konak yığını yapılandırması silme simgesi](./media/user-guide/usbx-events/image187.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2404">**Icon** ![Host Stack Configuration Delete icon](./media/user-guide/usbx-events/image187.png)</span></span>

<span data-ttu-id="c7285-2405">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2405">**Description**</span></span>

<span data-ttu-id="c7285-2406">Bu olay bir USBX konak yığını yapılandırması silme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2406">This event represents a USBX Host Stack Configuration Delete Event.</span></span>

<span data-ttu-id="c7285-2407">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2407">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2408">Bilgi alanı 1: yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="c7285-2408">Info Field 1: Configuration.</span></span>
- <span data-ttu-id="c7285-2409">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2409">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-2410">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2410">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2411">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2411">Info Field 4: Not used.</span></span>

### <a name="host-stack-configuration-enumerate"></a><span data-ttu-id="c7285-2412">Konak yığını yapılandırması numaralandırması</span><span class="sxs-lookup"><span data-stu-id="c7285-2412">Host Stack Configuration Enumerate</span></span> 

#### <a name="ux_host_stack_configuration_enumerate"></a><span data-ttu-id="c7285-2413">ux_host_stack_configuration_enumerate</span><span class="sxs-lookup"><span data-stu-id="c7285-2413">ux_host_stack_configuration_enumerate</span></span>

<span data-ttu-id="c7285-2414">**Simge** ![ Konak yığını yapılandırması sıralama simgesi](./media/user-guide/usbx-events/image188.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2414">**Icon** ![Host Stack Configuration Enumerate icon](./media/user-guide/usbx-events/image188.png)</span></span>

<span data-ttu-id="c7285-2415">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2415">**Description**</span></span>

<span data-ttu-id="c7285-2416">Bu olay bir USBX konak yığını yapılandırması listeleme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2416">This event represents a USBX Host Stack Configuration Enumerate Event.</span></span>

<span data-ttu-id="c7285-2417">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2417">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2418">Bilgi alanı 1: cihaz.</span><span class="sxs-lookup"><span data-stu-id="c7285-2418">Info Field 1: Device.</span></span>
- <span data-ttu-id="c7285-2419">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2419">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-2420">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2420">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2421">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2421">Info Field 4: Not used.</span></span>

### <a name="stack-configuration-instance-create"></a><span data-ttu-id="c7285-2422">Yığın yapılandırma örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="c7285-2422">Stack Configuration Instance Create</span></span> 

#### <a name="ux_host_stack_configuration_instance_create"></a><span data-ttu-id="c7285-2423">ux_host_stack_configuration_instance_create</span><span class="sxs-lookup"><span data-stu-id="c7285-2423">ux_host_stack_configuration_instance_create</span></span>

<span data-ttu-id="c7285-2424">**Simge** ![ Yığın yapılandırma örneği oluşturma simgesi](./media/user-guide/usbx-events/image189.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2424">**Icon** ![Stack Configuration Instance Create icon](./media/user-guide/usbx-events/image189.png)</span></span>

<span data-ttu-id="c7285-2425">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2425">**Description**</span></span>

<span data-ttu-id="c7285-2426">Bu olay bir USBX konak yığını yapılandırma örneği oluşturma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2426">This event represents a USBX Host Stack Configuration Instance Create Event.</span></span>

<span data-ttu-id="c7285-2427">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2427">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2428">Bilgi alanı 1: yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="c7285-2428">Info Field 1: Configuration.</span></span>
- <span data-ttu-id="c7285-2429">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2429">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-2430">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2430">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2431">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2431">Info Field 4: Not used.</span></span>

### <a name="host-stack-configuration-instance-delete"></a><span data-ttu-id="c7285-2432">Konak yığını yapılandırma örneği silme</span><span class="sxs-lookup"><span data-stu-id="c7285-2432">Host Stack Configuration Instance Delete</span></span> 

#### <a name="ux_host_stack_configuration_instance_delete"></a><span data-ttu-id="c7285-2433">ux_host_stack_configuration_instance_delete</span><span class="sxs-lookup"><span data-stu-id="c7285-2433">ux_host_stack_configuration_instance_delete</span></span>

<span data-ttu-id="c7285-2434">**Simge** ![ Konak yığını yapılandırma örneği silme simgesi](./media/user-guide/usbx-events/image190.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2434">**Icon** ![Host Stack Configuration Instance Delete icon](./media/user-guide/usbx-events/image190.png)</span></span>

<span data-ttu-id="c7285-2435">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2435">**Description**</span></span>

<span data-ttu-id="c7285-2436">Bu olay bir USBX konak yığını yapılandırma örneği silme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2436">This event represents a USBX Host Stack Configuration Instance Delete Event.</span></span>

<span data-ttu-id="c7285-2437">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2437">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2438">Bilgi alanı 1: yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="c7285-2438">Info Field 1: Configuration.</span></span>
- <span data-ttu-id="c7285-2439">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2439">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-2440">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2440">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2441">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2441">Info Field 4: Not used.</span></span>

### <a name="host-stack-configuration-set"></a><span data-ttu-id="c7285-2442">Konak yığını yapılandırma kümesi</span><span class="sxs-lookup"><span data-stu-id="c7285-2442">Host Stack Configuration Set</span></span> 

#### <a name="ux_host_stack_configuration_set"></a><span data-ttu-id="c7285-2443">ux_host_stack_configuration_set</span><span class="sxs-lookup"><span data-stu-id="c7285-2443">ux_host_stack_configuration_set</span></span>

<span data-ttu-id="c7285-2444">**Simge** ![ Konak yığını yapılandırma kümesi simgesi](./media/user-guide/usbx-events/image191.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2444">**Icon** ![Host Stack Configuration Set icon](./media/user-guide/usbx-events/image191.png)</span></span>

<span data-ttu-id="c7285-2445">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2445">**Description**</span></span>

<span data-ttu-id="c7285-2446">Bu olay bir USBX konak yığını yapılandırma kümesi olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2446">This event represents a USBX Host Stack Configuration Set Event.</span></span>

<span data-ttu-id="c7285-2447">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2447">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2448">Bilgi alanı 1: yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="c7285-2448">Info Field 1: Configuration.</span></span>
- <span data-ttu-id="c7285-2449">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2449">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-2450">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2450">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2451">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2451">Info Field 4: Not used.</span></span>

### <a name="host-stack-device-address-set"></a><span data-ttu-id="c7285-2452">Konak yığını cihaz adresi kümesi</span><span class="sxs-lookup"><span data-stu-id="c7285-2452">Host Stack Device Address Set</span></span> 

#### <a name="ux_host_stack_device_address_set"></a><span data-ttu-id="c7285-2453">ux_host_stack_device_address_set</span><span class="sxs-lookup"><span data-stu-id="c7285-2453">ux_host_stack_device_address_set</span></span>

<span data-ttu-id="c7285-2454">**Simge** ![ Konak yığını cihaz adresi kümesi simgesi](./media/user-guide/usbx-events/image192.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2454">**Icon** ![Host Stack Device Address Set icon](./media/user-guide/usbx-events/image192.png)</span></span>

<span data-ttu-id="c7285-2455">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2455">**Description**</span></span>

<span data-ttu-id="c7285-2456">Bu olay bir USBX konak yığını cihaz adresi kümesi olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2456">This event represents a USBX Host Stack Device Address Set Event.</span></span>

<span data-ttu-id="c7285-2457">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2457">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2458">Bilgi alanı 1: cihaz.</span><span class="sxs-lookup"><span data-stu-id="c7285-2458">Info Field 1: Device.</span></span>
- <span data-ttu-id="c7285-2459">Bilgi alanı 2: cihaz adresi.</span><span class="sxs-lookup"><span data-stu-id="c7285-2459">Info Field 2: Device Address.</span></span>
- <span data-ttu-id="c7285-2460">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2460">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2461">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2461">Info Field 4: Not used.</span></span>

### <a name="host-stack-device-configuration-get"></a><span data-ttu-id="c7285-2462">Konak yığını cihaz yapılandırmasını al</span><span class="sxs-lookup"><span data-stu-id="c7285-2462">Host Stack Device Configuration Get</span></span> 

#### <a name="ux_host_stack_device_configuration_get"></a><span data-ttu-id="c7285-2463">ux_host_stack_device_configuration_get</span><span class="sxs-lookup"><span data-stu-id="c7285-2463">ux_host_stack_device_configuration_get</span></span>

<span data-ttu-id="c7285-2464">**Simge** ![ Konak yığını cihaz yapılandırması Get simgesi](./media/user-guide/usbx-events/image193.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2464">**Icon** ![Host Stack Device Configuration Get icon](./media/user-guide/usbx-events/image193.png)</span></span>

<span data-ttu-id="c7285-2465">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2465">**Description**</span></span>

<span data-ttu-id="c7285-2466">Bu olay bir USBX konak yığını cihaz yapılandırması Get olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2466">This event represents a USBX Host Stack Device Configuration Get Event.</span></span>

<span data-ttu-id="c7285-2467">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2467">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2468">Bilgi alanı 1: cihaz.</span><span class="sxs-lookup"><span data-stu-id="c7285-2468">Info Field 1: Device.</span></span>
- <span data-ttu-id="c7285-2469">NFO alanı 2: yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="c7285-2469">nfo Field 2: Configuration.</span></span>
- <span data-ttu-id="c7285-2470">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2470">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2471">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2471">Info Field 4: Not used.</span></span>

### <a name="host-stack-device-configuration-select"></a><span data-ttu-id="c7285-2472">Konak yığını cihaz yapılandırması seçme</span><span class="sxs-lookup"><span data-stu-id="c7285-2472">Host Stack Device Configuration Select</span></span> 

#### <a name="ux_host_stack_device_configuration_select"></a><span data-ttu-id="c7285-2473">ux_host_stack_device_configuration_select</span><span class="sxs-lookup"><span data-stu-id="c7285-2473">ux_host_stack_device_configuration_select</span></span>

<span data-ttu-id="c7285-2474">**Simge** ![ Konak yığını cihaz yapılandırması seçim simgesi](./media/user-guide/usbx-events/image194.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2474">**Icon** ![Host Stack Device Configuration Select icon](./media/user-guide/usbx-events/image194.png)</span></span>

<span data-ttu-id="c7285-2475">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2475">**Description**</span></span>

<span data-ttu-id="c7285-2476">Bu olay bir USBX konak yığını cihaz yapılandırması seçme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2476">This event represents a USBX Host Stack Device Configuration Select Event.</span></span>

<span data-ttu-id="c7285-2477">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2477">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2478">Bilgi alanı 1: cihaz.</span><span class="sxs-lookup"><span data-stu-id="c7285-2478">Info Field 1: Device.</span></span>
- <span data-ttu-id="c7285-2479">Bilgi alanı 2: yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="c7285-2479">Info Field 2: Configuration.</span></span>
- <span data-ttu-id="c7285-2480">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2480">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2481">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2481">Info Field 4: Not used.</span></span>

### <a name="host-stack-device-descriptor-read"></a><span data-ttu-id="c7285-2482">Konak yığını cihaz tanımlayıcısı okuma</span><span class="sxs-lookup"><span data-stu-id="c7285-2482">Host Stack Device Descriptor Read</span></span> 

#### <a name="ux_host_stack_device_descriptor_read"></a><span data-ttu-id="c7285-2483">ux_host_stack_device_descriptor_read</span><span class="sxs-lookup"><span data-stu-id="c7285-2483">ux_host_stack_device_descriptor_read</span></span>

<span data-ttu-id="c7285-2484">**Simge** ![ Konak yığını cihaz tanımlayıcısı okuma simgesi](./media/user-guide/usbx-events/image195.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2484">**Icon** ![Host Stack Device Descriptor Read icon](./media/user-guide/usbx-events/image195.png)</span></span>

<span data-ttu-id="c7285-2485">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2485">**Description**</span></span>

<span data-ttu-id="c7285-2486">Bu olay bir USBX konak yığını cihaz tanımlayıcısı okuma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2486">This event represents a USBX Host Stack Device Descriptor Read Event.</span></span>

<span data-ttu-id="c7285-2487">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2487">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2488">Bilgi alanı 1: cihaz.</span><span class="sxs-lookup"><span data-stu-id="c7285-2488">Info Field 1: Device.</span></span>
- <span data-ttu-id="c7285-2489">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2489">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-2490">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2490">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2491">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2491">Info Field 4: Not used.</span></span>

### <a name="host-stack-device-get"></a><span data-ttu-id="c7285-2492">Konak yığını cihazını al</span><span class="sxs-lookup"><span data-stu-id="c7285-2492">Host Stack Device Get</span></span> 

#### <a name="ux_host_stack_device_get"></a><span data-ttu-id="c7285-2493">ux_host_stack_device_get</span><span class="sxs-lookup"><span data-stu-id="c7285-2493">ux_host_stack_device_get</span></span>

<span data-ttu-id="c7285-2494">**Simge** ![ Konak yığını cihazının al simgesi](./media/user-guide/usbx-events/image196.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2494">**Icon** ![Host Stack Device Get icon](./media/user-guide/usbx-events/image196.png)</span></span>

<span data-ttu-id="c7285-2495">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2495">**Description**</span></span>

<span data-ttu-id="c7285-2496">Bu olay bir USBX konak yığını cihaz Get olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2496">This event represents a USBX Host Stack Device Get Event.</span></span>

<span data-ttu-id="c7285-2497">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2497">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2498">Bilgi alanı 1: cihaz dizini.</span><span class="sxs-lookup"><span data-stu-id="c7285-2498">Info Field 1: Device index.</span></span>
- <span data-ttu-id="c7285-2499">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2499">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-2500">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2500">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2501">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2501">Info Field 4: Not used.</span></span>

### <a name="host-stack-device-remove"></a><span data-ttu-id="c7285-2502">Konak yığını cihazını kaldırma</span><span class="sxs-lookup"><span data-stu-id="c7285-2502">Host Stack Device Remove</span></span> 

#### <a name="ux_host_stack_device_remove"></a><span data-ttu-id="c7285-2503">ux_host_stack_device_remove</span><span class="sxs-lookup"><span data-stu-id="c7285-2503">ux_host_stack_device_remove</span></span>

<span data-ttu-id="c7285-2504">**Simge** ![ Konak yığını cihaz kaldırma simgesi](./media/user-guide/usbx-events/image197.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2504">**Icon** ![Host Stack Device Remove icon](./media/user-guide/usbx-events/image197.png)</span></span>

<span data-ttu-id="c7285-2505">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2505">**Description**</span></span>

<span data-ttu-id="c7285-2506">Bu olay bir USBX konak yığını cihaz kaldırma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2506">This event represents a USBX Host Stack Device Remove Event.</span></span>

<span data-ttu-id="c7285-2507">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2507">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2508">Bilgi alanı 1: HCD.</span><span class="sxs-lookup"><span data-stu-id="c7285-2508">Info Field 1: Hcd.</span></span>
- <span data-ttu-id="c7285-2509">Bilgi alanı 2: üst öğe.</span><span class="sxs-lookup"><span data-stu-id="c7285-2509">Info Field 2: Parent.</span></span>
- <span data-ttu-id="c7285-2510">Bilgi alanı 3: bağlantı noktası dizini.</span><span class="sxs-lookup"><span data-stu-id="c7285-2510">Info Field 3: Port Index.</span></span>
- <span data-ttu-id="c7285-2511">Bilgi alanı 4: cihaz.</span><span class="sxs-lookup"><span data-stu-id="c7285-2511">Info Field 4: Device.</span></span>

### <a name="host-stack-device-resource-free"></a><span data-ttu-id="c7285-2512">Konak yığını cihaz kaynağı boş</span><span class="sxs-lookup"><span data-stu-id="c7285-2512">Host Stack Device Resource Free</span></span> 

#### <a name="ux_host_stack_device_resource_free"></a><span data-ttu-id="c7285-2513">ux_host_stack_device_resource_free</span><span class="sxs-lookup"><span data-stu-id="c7285-2513">ux_host_stack_device_resource_free</span></span>

<span data-ttu-id="c7285-2514">**Simge** ![ Ana bilgisayar yığını cihaz kaynağı boş simgesi](./media/user-guide/usbx-events/image198.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2514">**Icon** ![Host Stack Device Resource Free icon](./media/user-guide/usbx-events/image198.png)</span></span>

<span data-ttu-id="c7285-2515">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2515">**Description**</span></span>

<span data-ttu-id="c7285-2516">Bu olay bir USBX konak yığını cihaz kaynağı ücretsiz olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2516">This event represents a USBX Host Stack Device Resource Free Event.</span></span>

<span data-ttu-id="c7285-2517">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2517">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2518">Bilgi alanı 1: cihaz.</span><span class="sxs-lookup"><span data-stu-id="c7285-2518">Info Field 1: Device.</span></span>
- <span data-ttu-id="c7285-2519">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2519">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-2520">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2520">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2521">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2521">Info Field 4: Not used.</span></span>

### <a name="host-stack-endpoint-instance-create"></a><span data-ttu-id="c7285-2522">Konak yığını uç noktası örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="c7285-2522">Host Stack Endpoint Instance Create</span></span> 

#### <a name="ux_host_stack_endpoint_instance_create"></a><span data-ttu-id="c7285-2523">ux_host_stack_endpoint_instance_create</span><span class="sxs-lookup"><span data-stu-id="c7285-2523">ux_host_stack_endpoint_instance_create</span></span>

<span data-ttu-id="c7285-2524">**Simge** ![ Konak yığını uç noktası örneği oluşturma simgesi](./media/user-guide/usbx-events/image199.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2524">**Icon** ![Host Stack Endpoint Instance Create icon](./media/user-guide/usbx-events/image199.png)</span></span>

<span data-ttu-id="c7285-2525">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2525">**Description**</span></span>

<span data-ttu-id="c7285-2526">Bu olay bir USBX konak yığını uç noktası örneği oluşturma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2526">This event represents a USBX Host Stack Endpoint Instance Create Event.</span></span>

<span data-ttu-id="c7285-2527">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2527">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2528">Bilgi alanı 1: cihaz.</span><span class="sxs-lookup"><span data-stu-id="c7285-2528">Info Field 1: Device.</span></span>
- <span data-ttu-id="c7285-2529">Bilgi alanı 2: uç nokta.</span><span class="sxs-lookup"><span data-stu-id="c7285-2529">Info Field 2: Endpoint.</span></span>
- <span data-ttu-id="c7285-2530">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2530">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2531">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2531">Info Field 4: Not used.</span></span>

### <a name="host-stack-endpoint-instance-delete"></a><span data-ttu-id="c7285-2532">Konak yığın uç noktası örneği silme</span><span class="sxs-lookup"><span data-stu-id="c7285-2532">Host Stack Endpoint Instance Delete</span></span> 

#### <a name="ux_host_stack_endpoint_instance_delete"></a><span data-ttu-id="c7285-2533">ux_host_stack_endpoint_instance_delete</span><span class="sxs-lookup"><span data-stu-id="c7285-2533">ux_host_stack_endpoint_instance_delete</span></span>

<span data-ttu-id="c7285-2534">**Simge** ![ Konak yığın uç noktası örneği silme simgesi](./media/user-guide/usbx-events/image200.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2534">**Icon** ![Host Stack Endpoint Instance Delete icon](./media/user-guide/usbx-events/image200.png)</span></span>

<span data-ttu-id="c7285-2535">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2535">**Description**</span></span>

<span data-ttu-id="c7285-2536">Bu olay bir USBX konak yığını uç noktası örneği silme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2536">This event represents a USBX Host Stack Endpoint Instance Delete Event.</span></span>

<span data-ttu-id="c7285-2537">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2537">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2538">Bilgi alanı 2: uç nokta.</span><span class="sxs-lookup"><span data-stu-id="c7285-2538">Info Field 2: Endpoint.</span></span>
- <span data-ttu-id="c7285-2539">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2539">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2540">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2540">Info Field 4: Not used.</span></span>

### <a name="host-stack-endpoint-reset"></a><span data-ttu-id="c7285-2541">Konak yığını uç noktası sıfırlama</span><span class="sxs-lookup"><span data-stu-id="c7285-2541">Host Stack Endpoint Reset</span></span> 

#### <a name="ux_host_stack_endpoint_reset"></a><span data-ttu-id="c7285-2542">ux_host_stack_endpoint_reset</span><span class="sxs-lookup"><span data-stu-id="c7285-2542">ux_host_stack_endpoint_reset</span></span>

<span data-ttu-id="c7285-2543">**Simge** ![ Konak yığını uç noktası sıfırlama simgesi](./media/user-guide/usbx-events/image201.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2543">**Icon** ![Host Stack Endpoint Reset icon](./media/user-guide/usbx-events/image201.png)</span></span>

<span data-ttu-id="c7285-2544">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2544">**Description**</span></span>

<span data-ttu-id="c7285-2545">Bu olay bir USBX konak yığını uç noktası sıfırlama olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2545">This event represents a USBX Host Stack Endpoint Reset Event.</span></span>

<span data-ttu-id="c7285-2546">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2546">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2547">Bilgi alanı 1: cihaz.</span><span class="sxs-lookup"><span data-stu-id="c7285-2547">Info Field 1: Device.</span></span>
- <span data-ttu-id="c7285-2548">Bilgi alanı 2: uç nokta.</span><span class="sxs-lookup"><span data-stu-id="c7285-2548">Info Field 2: Endpoint.</span></span>
- <span data-ttu-id="c7285-2549">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2549">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2550">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2550">Info Field 4: Not used.</span></span>

### <a name="host-stack-endpoint-transfer-abort"></a><span data-ttu-id="c7285-2551">Konak yığını uç noktası aktarımı Iptali</span><span class="sxs-lookup"><span data-stu-id="c7285-2551">Host Stack Endpoint Transfer Abort</span></span> 

#### <a name="ux_host_stack_endpoint_transfer_abort"></a><span data-ttu-id="c7285-2552">ux_host_stack_endpoint_transfer_abort</span><span class="sxs-lookup"><span data-stu-id="c7285-2552">ux_host_stack_endpoint_transfer_abort</span></span>

<span data-ttu-id="c7285-2553">**Simge** ![ Konak yığını uç noktası aktarımı Iptal simgesi](./media/user-guide/usbx-events/image202.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2553">**Icon** ![Host Stack Endpoint Transfer Abort icon](./media/user-guide/usbx-events/image202.png)</span></span>

<span data-ttu-id="c7285-2554">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2554">**Description**</span></span>

<span data-ttu-id="c7285-2555">Bu olay bir USBX konak yığını uç nokta aktarımı Iptali olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2555">This event represents a USBX Host Stack Endpoint Transfer Abort Event.</span></span>

<span data-ttu-id="c7285-2556">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2556">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2557">Bilgi alanı 1: uç nokta.</span><span class="sxs-lookup"><span data-stu-id="c7285-2557">Info Field 1: Endpoint.</span></span>
- <span data-ttu-id="c7285-2558">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2558">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-2559">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2559">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2560">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2560">Info Field 4: Not used.</span></span>

### <a name="host-stack-host-controller-register"></a><span data-ttu-id="c7285-2561">Konak yığını konak denetleyicisi kaydı</span><span class="sxs-lookup"><span data-stu-id="c7285-2561">Host Stack Host Controller Register</span></span> 

#### <a name="ux_host_stack_hcd_register"></a><span data-ttu-id="c7285-2562">ux_host_stack_hcd_register</span><span class="sxs-lookup"><span data-stu-id="c7285-2562">ux_host_stack_hcd_register</span></span>

<span data-ttu-id="c7285-2563">**Simge** ![ Konak yığını konak denetleyicisi kayıt simgesi](./media/user-guide/usbx-events/image203.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2563">**Icon** ![Host Stack Host Controller Register icon](./media/user-guide/usbx-events/image203.png)</span></span>

<span data-ttu-id="c7285-2564">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2564">**Description**</span></span>

<span data-ttu-id="c7285-2565">Bu olay bir USBX konak yığını konak denetleyicisi kaydını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2565">This event represents a USBX Host Stack Host Controller Register.</span></span>

<span data-ttu-id="c7285-2566">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2566">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2567">Bilgi alanı 1: HCD adı.</span><span class="sxs-lookup"><span data-stu-id="c7285-2567">Info Field 1: Hcd Name.</span></span>
- <span data-ttu-id="c7285-2568">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2568">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-2569">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2569">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2570">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2570">Info Field 4: Not used.</span></span>

### <a name="host-stack-initialize"></a><span data-ttu-id="c7285-2571">Konak yığını başlatma</span><span class="sxs-lookup"><span data-stu-id="c7285-2571">Host Stack Initialize</span></span> 

#### <a name="ux_host_stack_initialize"></a><span data-ttu-id="c7285-2572">ux_host_stack_initialize</span><span class="sxs-lookup"><span data-stu-id="c7285-2572">ux_host_stack_initialize</span></span>

<span data-ttu-id="c7285-2573">**Simge** ![ Konak yığını başlatma simgesi](./media/user-guide/usbx-events/image204.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2573">**Icon** ![Host Stack Initialize icon](./media/user-guide/usbx-events/image204.png)</span></span>

<span data-ttu-id="c7285-2574">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2574">**Description**</span></span>

<span data-ttu-id="c7285-2575">Bu olay bir USBX konak Stack Initialize olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2575">This event represents a USBX Host Stack Initialize Event.</span></span>

<span data-ttu-id="c7285-2576">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2576">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2577">Bilgi alanı 1: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2577">Info Field 1: Not used.</span></span>
- <span data-ttu-id="c7285-2578">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2578">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-2579">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2579">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2580">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2580">Info Field 4: Not used.</span></span>

### <a name="host-stack-interface-endpoint-get"></a><span data-ttu-id="c7285-2581">Konak yığını arabirimi uç noktası al</span><span class="sxs-lookup"><span data-stu-id="c7285-2581">Host Stack Interface Endpoint Get</span></span> 

#### <a name="interface_-tcp-retry-entry"></a><span data-ttu-id="c7285-2582">Interface_ TCP yeniden deneme girdisi</span><span class="sxs-lookup"><span data-stu-id="c7285-2582">Interface_ TCP retry entry</span></span>

<span data-ttu-id="c7285-2583">**Simge** ![ Konak yığını arabirimi uç noktası al simgesi](./media/user-guide/usbx-events/image205.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2583">**Icon** ![Host Stack Interface Endpoint Get icon](./media/user-guide/usbx-events/image205.png)</span></span>

<span data-ttu-id="c7285-2584">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2584">**Description**</span></span>

<span data-ttu-id="c7285-2585">Bu olay bir iç NetX TCP yeniden deneme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2585">This event represents an internal NetX TCP retry event.</span></span>

<span data-ttu-id="c7285-2586">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2586">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2587">Bilgi alanı 1: arabirim.</span><span class="sxs-lookup"><span data-stu-id="c7285-2587">Info Field 1: Interface.</span></span>
- <span data-ttu-id="c7285-2588">Bilgi alanı 2: uç nokta dizini.</span><span class="sxs-lookup"><span data-stu-id="c7285-2588">Info Field 2: Endpoint index.</span></span>
- <span data-ttu-id="c7285-2589">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2589">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2590">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2590">Info Field 4: Not used.</span></span>

### <a name="host-stack-interface-instance-create"></a><span data-ttu-id="c7285-2591">Konak yığını arabirim örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="c7285-2591">Host Stack Interface Instance Create</span></span> 

#### <a name="ux_host_stack_interface_instance_create"></a><span data-ttu-id="c7285-2592">ux_host_stack_interface_instance_create</span><span class="sxs-lookup"><span data-stu-id="c7285-2592">ux_host_stack_interface_instance_create</span></span>

<span data-ttu-id="c7285-2593">**Simge** ![ Konak yığını arabirim örneği oluşturma simgesi](./media/user-guide/usbx-events/image206.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2593">**Icon** ![Host Stack Interface Instance Create icon](./media/user-guide/usbx-events/image206.png)</span></span>

<span data-ttu-id="c7285-2594">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2594">**Description**</span></span>

<span data-ttu-id="c7285-2595">Bu olay bir USBX konak yığını arabirim örneği oluşturma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2595">This event represents a USBX Host Stack Interface Instance Create Event.</span></span>

<span data-ttu-id="c7285-2596">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2596">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2597">Bilgi alanı 1: arabirim.</span><span class="sxs-lookup"><span data-stu-id="c7285-2597">Info Field 1: Interface.</span></span>
- <span data-ttu-id="c7285-2598">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2598">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-2599">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2599">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2600">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2600">Info Field 4: Not used.</span></span>

### <a name="host-stack-interface-instance-delete"></a><span data-ttu-id="c7285-2601">Konak yığını arabirim örneği silme</span><span class="sxs-lookup"><span data-stu-id="c7285-2601">Host Stack Interface Instance Delete</span></span> 

#### <a name="ux_host_stack_interface_instance_delete"></a><span data-ttu-id="c7285-2602">ux_host_stack_interface_instance_delete</span><span class="sxs-lookup"><span data-stu-id="c7285-2602">ux_host_stack_interface_instance_delete</span></span>

<span data-ttu-id="c7285-2603">**Simge** ![ Konak yığını arabirim örneği silme simgesi](./media/user-guide/usbx-events/image207.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2603">**Icon** ![Host Stack Interface Instance Delete icon](./media/user-guide/usbx-events/image207.png)</span></span>

<span data-ttu-id="c7285-2604">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2604">**Description**</span></span>

<span data-ttu-id="c7285-2605">Bu olay bir USBX konak yığını arabirim örneği silme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2605">This event represents a USBX Host Stack Interface Instance Delete Event.</span></span>

<span data-ttu-id="c7285-2606">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2606">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2607">Bilgi alanı 1: arabirim.</span><span class="sxs-lookup"><span data-stu-id="c7285-2607">Info Field 1: Interface.</span></span>
- <span data-ttu-id="c7285-2608">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2608">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-2609">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2609">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2610">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2610">Info Field 4: Not used.</span></span>

### <a name="host-stack-interface-set"></a><span data-ttu-id="c7285-2611">Konak yığını arabirim kümesi</span><span class="sxs-lookup"><span data-stu-id="c7285-2611">Host Stack Interface Set</span></span> 

#### <a name="ux_host_stack_interface_set"></a><span data-ttu-id="c7285-2612">ux_host_stack_interface_set</span><span class="sxs-lookup"><span data-stu-id="c7285-2612">ux_host_stack_interface_set</span></span>

<span data-ttu-id="c7285-2613">**Simge** ![ Konak yığını arabirim kümesi simgesi](./media/user-guide/usbx-events/image208.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2613">**Icon** ![Host Stack Interface Set icon](./media/user-guide/usbx-events/image208.png)</span></span>

<span data-ttu-id="c7285-2614">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2614">**Description**</span></span>

<span data-ttu-id="c7285-2615">Bu olay bir USBX konak yığını arabirim kümesi olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2615">This event represents a USBX Host Stack Interface Set Event.</span></span>

<span data-ttu-id="c7285-2616">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2616">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2617">Bilgi alanı 1: arabirim.</span><span class="sxs-lookup"><span data-stu-id="c7285-2617">Info Field 1: Interface.</span></span>
- <span data-ttu-id="c7285-2618">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2618">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-2619">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2619">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2620">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2620">Info Field 4: Not used.</span></span>

### <a name="host-stack-interface-setting-select"></a><span data-ttu-id="c7285-2621">Konak yığını arabirim ayarı seçimi</span><span class="sxs-lookup"><span data-stu-id="c7285-2621">Host Stack Interface Setting Select</span></span> 

#### <a name="ux_host_stack_interface_setting_select"></a><span data-ttu-id="c7285-2622">ux_host_stack_interface_setting_select</span><span class="sxs-lookup"><span data-stu-id="c7285-2622">ux_host_stack_interface_setting_select</span></span>

<span data-ttu-id="c7285-2623">**Simge** ![ Konak yığın arabirimi ayarı seçme simgesi](./media/user-guide/usbx-events/image209.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2623">**Icon** ![Host Stack Interface Setting Select icon](./media/user-guide/usbx-events/image209.png)</span></span>

<span data-ttu-id="c7285-2624">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2624">**Description**</span></span>

<span data-ttu-id="c7285-2625">Bu olay bir USBX konak yığın arabirimi ayarını seçme olayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2625">This event represents a USBX Host Stack Interface Setting Select Event.</span></span>

<span data-ttu-id="c7285-2626">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2626">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2627">Bilgi alanı 1: arabirim.</span><span class="sxs-lookup"><span data-stu-id="c7285-2627">Info Field 1: Interface.</span></span>
- <span data-ttu-id="c7285-2628">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2628">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-2629">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2629">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2630">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2630">Info Field 4: Not used.</span></span>

### <a name="host-stack-new-configuration-create"></a><span data-ttu-id="c7285-2631">Ana bilgisayar yığını yeni yapılandırma oluşturma</span><span class="sxs-lookup"><span data-stu-id="c7285-2631">Host Stack New Configuration Create</span></span> 

#### <a name="ux_host_stack_new_configuration_create"></a><span data-ttu-id="c7285-2632">ux_host_stack_new_configuration_create</span><span class="sxs-lookup"><span data-stu-id="c7285-2632">ux_host_stack_new_configuration_create</span></span>

<span data-ttu-id="c7285-2633">**Simge** ![ Konak yığını yeni yapılandırma Oluştur simgesi](./media/user-guide/usbx-events/image210.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2633">**Icon** ![Host Stack New Configuration Create icon](./media/user-guide/usbx-events/image210.png)</span></span>

<span data-ttu-id="c7285-2634">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2634">**Description**</span></span>
 
<span data-ttu-id="c7285-2635">Bu olay, bir USBX konak yığınını yeni yapılandırma oluşturma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2635">This event represents a USBX Host Stack New Configuration Create Event.</span></span>

<span data-ttu-id="c7285-2636">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2636">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2637">Bilgi alanı 1: cihaz.</span><span class="sxs-lookup"><span data-stu-id="c7285-2637">Info Field 1: Device.</span></span>
- <span data-ttu-id="c7285-2638">Bilgi alanı 2: yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="c7285-2638">Info Field 2: Configuration.</span></span>
- <span data-ttu-id="c7285-2639">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2639">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2640">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2640">Info Field 4: Not used.</span></span>

### <a name="host-stack-new-device-create"></a><span data-ttu-id="c7285-2641">Ana bilgisayar yığını yeni cihaz oluşturma</span><span class="sxs-lookup"><span data-stu-id="c7285-2641">Host Stack New Device Create</span></span> 

#### <a name="ux_host_stack_new_device_create"></a><span data-ttu-id="c7285-2642">ux_host_stack_new_device_create</span><span class="sxs-lookup"><span data-stu-id="c7285-2642">ux_host_stack_new_device_create</span></span>

<span data-ttu-id="c7285-2643">**Simge** ![ Konak yığını yeni cihaz Oluştur simgesi](./media/user-guide/usbx-events/image211.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2643">**Icon** ![Host Stack New Device Create icon](./media/user-guide/usbx-events/image211.png)</span></span>

<span data-ttu-id="c7285-2644">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2644">**Description**</span></span>
 
 <span data-ttu-id="c7285-2645">Bu olay bir USBX konak yığını yeni cihaz oluşturma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2645">This event represents a USBX Host Stack New Device Create Event.</span></span>

<span data-ttu-id="c7285-2646">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2646">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2647">Bilgi alanı 1: HCD.</span><span class="sxs-lookup"><span data-stu-id="c7285-2647">Info Field 1: Hcd.</span></span>
- <span data-ttu-id="c7285-2648">Bilgi alanı 2: cihaz sahibi.</span><span class="sxs-lookup"><span data-stu-id="c7285-2648">Info Field 2: Device owner.</span></span>
- <span data-ttu-id="c7285-2649">Bilgi alanı 3: bağlantı noktası dizini.</span><span class="sxs-lookup"><span data-stu-id="c7285-2649">Info Field 3: Port index.</span></span>
- <span data-ttu-id="c7285-2650">Bilgi alanı 4: cihaz.</span><span class="sxs-lookup"><span data-stu-id="c7285-2650">Info Field 4: Device.</span></span>

### <a name="host-stack-new-endpoint-create"></a><span data-ttu-id="c7285-2651">Ana bilgisayar yığını yeni uç nokta oluşturma</span><span class="sxs-lookup"><span data-stu-id="c7285-2651">Host Stack New Endpoint Create</span></span> 

#### <a name="ux_host_stack_new_endpoint_create"></a><span data-ttu-id="c7285-2652">ux_host_stack_new_endpoint_create</span><span class="sxs-lookup"><span data-stu-id="c7285-2652">ux_host_stack_new_endpoint_create</span></span>

<span data-ttu-id="c7285-2653">**Simge** ![ Ana bilgisayar yığını yeni uç nokta Oluştur simgesi](./media/user-guide/usbx-events/image212.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2653">**Icon** ![Host Stack New Endpoint Create icon](./media/user-guide/usbx-events/image212.png)</span></span>

<span data-ttu-id="c7285-2654">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2654">**Description**</span></span>
 
<span data-ttu-id="c7285-2655">Bu olay, bir USBX konak yığınını yeni bir uç nokta oluşturma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2655">This event represents a USBX Host Stack New Endpoint Create Event.</span></span>

<span data-ttu-id="c7285-2656">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2656">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2657">Bilgi alanı 1: arabirim.</span><span class="sxs-lookup"><span data-stu-id="c7285-2657">Info Field 1: Interface.</span></span>
- <span data-ttu-id="c7285-2658">Bilgi alanı 2: uç nokta.</span><span class="sxs-lookup"><span data-stu-id="c7285-2658">Info Field 2: Endpoint.</span></span>
- <span data-ttu-id="c7285-2659">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2659">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2660">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2660">Info Field 4: Not used.</span></span>

### <a name="host-stack-root-hub-change-process"></a><span data-ttu-id="c7285-2661">Konak yığını kök hub 'ı değişiklik Işlemi</span><span class="sxs-lookup"><span data-stu-id="c7285-2661">Host Stack Root Hub Change Process</span></span> 

#### <a name="ux_host_stack_rh_change_process"></a><span data-ttu-id="c7285-2662">ux_host_stack_rh_change_process</span><span class="sxs-lookup"><span data-stu-id="c7285-2662">ux_host_stack_rh_change_process</span></span>

<span data-ttu-id="c7285-2663">**Simge** ![ Konak yığını kök hub 'ı değiştirme Işlemi simgesi](./media/user-guide/usbx-events/image213.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2663">**Icon** ![Host Stack Root Hub Change Process icon](./media/user-guide/usbx-events/image213.png)</span></span>

<span data-ttu-id="c7285-2664">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2664">**Description**</span></span>
 
<span data-ttu-id="c7285-2665">Bu olay bir USBX konak yığını kök hub 'ı değişiklik sürecini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2665">This event represents a USBX Host Stack Root Hub Change Process.</span></span>

<span data-ttu-id="c7285-2666">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2666">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2667">Bilgi alanı 1: bağlantı noktası dizini.</span><span class="sxs-lookup"><span data-stu-id="c7285-2667">Info Field 1: Port index.</span></span>
- <span data-ttu-id="c7285-2668">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2668">Info Field 2: Not used.</span></span>
- <span data-ttu-id="c7285-2669">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2669">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2670">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2670">Info Field 4: Not used.</span></span>

### <a name="host-stack-root-hub-device-extraction"></a><span data-ttu-id="c7285-2671">Konak yığını kök hub cihazı ayıklama</span><span class="sxs-lookup"><span data-stu-id="c7285-2671">Host Stack Root Hub Device Extraction</span></span> 

#### <a name="ux_host_stack_rh_device_extraction"></a><span data-ttu-id="c7285-2672">ux_host_stack_rh_device_extraction</span><span class="sxs-lookup"><span data-stu-id="c7285-2672">ux_host_stack_rh_device_extraction</span></span>

<span data-ttu-id="c7285-2673">**Simge** ![ Konak yığını kök hub cihazı ayıklama simgesi](./media/user-guide/usbx-events/image214.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2673">**Icon** ![Host Stack Root Hub Device Extraction icon](./media/user-guide/usbx-events/image214.png)</span></span>

<span data-ttu-id="c7285-2674">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2674">**Description**</span></span>

<span data-ttu-id="c7285-2675">Bu olay bir USBX konak yığını kök hub cihazı ayıklama olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2675">This event represents a USBX Host Stack Root Hub Device Extraction Event.</span></span>

<span data-ttu-id="c7285-2676">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2676">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2677">Bilgi alanı 1: HCD.</span><span class="sxs-lookup"><span data-stu-id="c7285-2677">Info Field 1: Hcd.</span></span>
- <span data-ttu-id="c7285-2678">Bilgi alanı 2: bağlantı noktası dizini.</span><span class="sxs-lookup"><span data-stu-id="c7285-2678">Info Field 2: Port index.</span></span>
- <span data-ttu-id="c7285-2679">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2679">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2680">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2680">Info Field 4: Not used.</span></span>

### <a name="host-stack-root-hub-device-insertion"></a><span data-ttu-id="c7285-2681">Konak yığını kök hub cihazı ekleme</span><span class="sxs-lookup"><span data-stu-id="c7285-2681">Host Stack Root Hub Device Insertion</span></span> 

#### <a name="ux_host_stack_rh_device_insertion"></a><span data-ttu-id="c7285-2682">ux_host_stack_rh_device_insertion</span><span class="sxs-lookup"><span data-stu-id="c7285-2682">ux_host_stack_rh_device_insertion</span></span>

<span data-ttu-id="c7285-2683">**Simge** ![ Konak yığını kök hub cihazı ekleme simgesi](./media/user-guide/usbx-events/image215.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2683">**Icon** ![Host Stack Root Hub Device Insertion icon](./media/user-guide/usbx-events/image215.png)</span></span>

<span data-ttu-id="c7285-2684">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2684">**Description**</span></span>

<span data-ttu-id="c7285-2685">Bu olay bir USBX konak yığını kök hub cihazı ekleme işlemini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2685">This event represents a USBX Host Stack Root Hub Device Insertion.</span></span>

<span data-ttu-id="c7285-2686">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2686">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2687">Bilgi alanı 1: HCD.</span><span class="sxs-lookup"><span data-stu-id="c7285-2687">Info Field 1: Hcd.</span></span>
- <span data-ttu-id="c7285-2688">Bilgi alanı 2: bağlantı noktası dizini.</span><span class="sxs-lookup"><span data-stu-id="c7285-2688">Info Field 2: Port index.</span></span>
- <span data-ttu-id="c7285-2689">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2689">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2690">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2690">Info Field 4: Not used.</span></span>

### <a name="host-stack-transfer-request"></a><span data-ttu-id="c7285-2691">Konak yığını aktarım Isteği</span><span class="sxs-lookup"><span data-stu-id="c7285-2691">Host Stack Transfer Request</span></span> 

#### <a name="ux_host_stack_transfer_request"></a><span data-ttu-id="c7285-2692">ux_host_stack_transfer_request</span><span class="sxs-lookup"><span data-stu-id="c7285-2692">ux_host_stack_transfer_request</span></span>

<span data-ttu-id="c7285-2693">**Simge** ![ Konak yığını aktarım Isteği simgesi](./media/user-guide/usbx-events/image216.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2693">**Icon** ![Host Stack Transfer Request icon](./media/user-guide/usbx-events/image216.png)</span></span>

<span data-ttu-id="c7285-2694">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2694">**Description**</span></span>

<span data-ttu-id="c7285-2695">Bu olay bir USBX konak yığını aktarım Isteğini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2695">This event represents a USBX Host Stack Transfer Request.</span></span>

<span data-ttu-id="c7285-2696">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2696">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2697">Bilgi alanı 1: cihaz.</span><span class="sxs-lookup"><span data-stu-id="c7285-2697">Info Field 1: Device.</span></span>
- <span data-ttu-id="c7285-2698">Bilgi alanı 2: uç nokta.</span><span class="sxs-lookup"><span data-stu-id="c7285-2698">Info Field 2: Endpoint.</span></span>
- <span data-ttu-id="c7285-2699">Bilgi alanı 3: istek aktarma.</span><span class="sxs-lookup"><span data-stu-id="c7285-2699">Info Field 3: Transfer request.</span></span>
- <span data-ttu-id="c7285-2700">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2700">Info Field 4: Not used.</span></span>

### <a name="host-stack-transfer-request-abort"></a><span data-ttu-id="c7285-2701">Konak yığını aktarım Isteği Iptali</span><span class="sxs-lookup"><span data-stu-id="c7285-2701">Host Stack Transfer Request Abort</span></span> 

#### <a name="internal-io-driver-get-status"></a><span data-ttu-id="c7285-2702">İç g/ç sürücüsü Get durumu</span><span class="sxs-lookup"><span data-stu-id="c7285-2702">Internal I/O driver get status</span></span>

<span data-ttu-id="c7285-2703">**Simge** ![ Konak yığını aktarım Isteği Iptali simgesi](./media/user-guide/usbx-events/image217.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2703">**Icon** ![Host Stack Transfer Request Abort icon](./media/user-guide/usbx-events/image217.png)</span></span>

<span data-ttu-id="c7285-2704">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2704">**Description**</span></span>

<span data-ttu-id="c7285-2705">Bu olay bir USBX konak yığını aktarım Isteği Iptali 'ni temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2705">This event represents a USBX Host Stack Transfer Request Abort.</span></span>

<span data-ttu-id="c7285-2706">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2706">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2707">Bilgi alanı 1: cihaz.</span><span class="sxs-lookup"><span data-stu-id="c7285-2707">Info Field 1: Device.</span></span>
- <span data-ttu-id="c7285-2708">Bilgi alanı 2: uç nokta.</span><span class="sxs-lookup"><span data-stu-id="c7285-2708">Info Field 2: Endpoint.</span></span>
- <span data-ttu-id="c7285-2709">Bilgi alanı 3: istek aktarma.</span><span class="sxs-lookup"><span data-stu-id="c7285-2709">Info Field 3: Transfer request.</span></span>
- <span data-ttu-id="c7285-2710">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2710">Info Field 4: Not used.</span></span>

### <a name="usbx-error"></a><span data-ttu-id="c7285-2711">USBX hatası</span><span class="sxs-lookup"><span data-stu-id="c7285-2711">USBX Error</span></span> 

#### <a name="ux_error"></a><span data-ttu-id="c7285-2712">ux_error</span><span class="sxs-lookup"><span data-stu-id="c7285-2712">ux_error</span></span>

<span data-ttu-id="c7285-2713">**Simge** ![ U S B X hata simgesi](./media/user-guide/usbx-events/image218.png)</span><span class="sxs-lookup"><span data-stu-id="c7285-2713">**Icon** ![U S B X Error icon](./media/user-guide/usbx-events/image218.png)</span></span>

<span data-ttu-id="c7285-2714">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c7285-2714">**Description**</span></span>

<span data-ttu-id="c7285-2715">Bu olay bir USBX hata olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c7285-2715">This event represents a USBX Error Event.</span></span>

<span data-ttu-id="c7285-2716">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="c7285-2716">**Information Fields**</span></span>

- <span data-ttu-id="c7285-2717">Bilgi alanı 1: USBX hatası.</span><span class="sxs-lookup"><span data-stu-id="c7285-2717">Info Field 1: USBX error.</span></span>
- <span data-ttu-id="c7285-2718">Bilgi alanı 2: hata adı.</span><span class="sxs-lookup"><span data-stu-id="c7285-2718">Info Field 2: Error Name.</span></span>
- <span data-ttu-id="c7285-2719">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2719">Info Field 3: Not used.</span></span>
- <span data-ttu-id="c7285-2720">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="c7285-2720">Info Field 4: Not used.</span></span>