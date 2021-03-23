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
# <a name="chapter-9---azure-rtos-usbx-trace-events"></a>Bölüm 9-Azure RTOS USBX izleme olayları

Bu bölüm, TraceX tarafından görünen Azure RTOS USBX olaylarının bir açıklamasını içerir. 

## <a name="list-of-events-and-icons"></a>Olay ve simgelerin listesi

Aşağıda, TraceX tarafından görünen USBX olaylarının bir listesi verilmiştir.

| Simge                             | Anlamı                               |
| -------------------------------- | ------------------------------------- |
| ![Cihaz sınıfı C D C etkinleştir simgesi](./media/user-guide/usbx-events/image1.png)    | **Device Class CDC etkinleştir** *(ux_device_class_cdc_activate)* |
| ![Cihaz sınıfı C D C devre dışı bırakma simgesi](./media/user-guide/usbx-events/image2.png)    | **Device Class CDC devre dışı bırak** *(ux_device_class_cdc_deactivate)* |
| ![Cihaz sınıfı C D C okuma simgesi](./media/user-guide/usbx-events/image3.png)    | **Aygıt sınıfı CDC okuma** *(ux_device_class_cdc_read)* |
| ![Cihaz sınıfı C D C yazma simgesi](./media/user-guide/usbx-events/image4.png)    | **Aygıt sınıfı CDC yazma** *(ux_device_class_cdc_write)* |
| ![Device Class Dpump etkinleştir simgesi](./media/user-guide/usbx-events/image5.png)    | **Device Class Dpump etkinleştir** *(ux_device_class_dpump_activate)* |
| ![Cihaz sınıfı Dpump devre dışı bırakma simgesi](./media/user-guide/usbx-events/image6.png)    | **Cihaz sınıfı Dpump devre dışı bırakma** *(ux_device_class_dpump_deactivate)* |
| ![Cihaz sınıfı Dpump okuma simgesi](./media/user-guide/usbx-events/image7.png)    | **Cihaz sınıfı Dpump okuma** *(ux_device_class_dpump_read)* |
| ![Device Class Dpump yazma simgesi](./media/user-guide/usbx-events/image8.png)    | **Cihaz sınıfı Dpump yazma** *(ux_device_class_dpump_write)* |
| ![Device Class HID etkinleştirme simgesi](./media/user-guide/usbx-events/image9.png)    | **Device Class HID etkinleştir** *(ux_device_class_hid_activate)* |
| ![Cihaz sınıfı HID devre dışı bırakma simgesi](./media/user-guide/usbx-events/image10.png)    | **Cihaz sınıfı HID devre dışı bırakma** *(ux_device_class_hid_deactivate)* |
| ![Cihaz sınıfı HID tanımlayıcısı gönderme simgesi](./media/user-guide/usbx-events/image11.png)    | **Cihaz sınıfı HID tanımlayıcısı gönderme** *(ux_device_class_hid_descriptor_send)* |
| ![Cihaz sınıfı HID olayı al simgesi](./media/user-guide/usbx-events/image12.png)    | **Cihaz sınıfı HID olayı Get** *(ux_device_class_hid_event_get)* |
| ![Cihaz sınıfı HID olay kümesi simgesi](./media/user-guide/usbx-events/image13.png)    | **Cihaz sınıfı HID olay kümesi** *(ux_device_class_hid_event_set)* |
| ![Cihaz sınıfı HID raporu al simgesi](./media/user-guide/usbx-events/image14.png)    | **Cihaz sınıfı HID raporu Get** *(ux_device_class_hid_report_get)* |
| ![Cihaz sınıfı HID rapor kümesi simgesi](./media/user-guide/usbx-events/image15.png)    | **Cihaz sınıfı HID rapor kümesi** *(ux_device_class_hid_report_set)* |
| ![Cihaz sınıfı Pima etkinleştirme simgesi](./media/user-guide/usbx-events/image16.png)    | **Device Class Pima etkinleştir** *(ux_device_class_pima_activate)* |
| ![Cihaz sınıfı Pima devre dışı bırakma simgesi](./media/user-guide/usbx-events/image17.png)    | **Cihaz sınıfı Pima devre dışı bırakma** *(ux_device_class_pima_deactivate)* |
| ![Cihaz sınıfı Pima cihaz bilgileri gönderme simgesi](./media/user-guide/usbx-events/image18.png)    | **Cihaz sınıfı Pima cihaz bilgileri gönderme** *(ux_device_class_pima_device_info_send)* |
| ![Device Class Pima olayı al simgesi](./media/user-guide/usbx-events/image19.png)    | **Cihaz sınıfı Pima olayı Get** *(ux_device_class_pima_event_get)* |
| ![Cihaz sınıfı Pima olayı kümesi simgesi](./media/user-guide/usbx-events/image20.png)    | **Device Class Pima olay kümesi** *(ux_device_class_pima_event_set)* |
| ![Cihaz sınıfı Pima nesnesi ekleme simgesi](./media/user-guide/usbx-events/image21.png)    | **Cihaz sınıfı Pima nesnesi ekleme** *(ux_device_class_pima_object_add)* |
| ![Aygıt sınıfı Pima nesnesi verileri al simgesi](./media/user-guide/usbx-events/image22.png)    | **Cihaz sınıfı Pima nesnesi verileri al** *(ux_device_class_pima_object_data_get)* |
| ![Cihaz sınıfı Pima nesnesi verileri gönderme simgesi](./media/user-guide/usbx-events/image23.png)    | **Device Class Pima nesne verileri gönderme** *(ux_device_class_pima_object_data_send)* |
| ![Device Class Pima nesnesi silme simgesi](./media/user-guide/usbx-events/image24.png)    | **Device Class Pima nesnesi silme** *(ux_device_class_pima_object_delete)* |
| ![Cihaz sınıfı Pima nesnesi gönderme simgesini Işler](./media/user-guide/usbx-events/image25.png)    | **Cihaz sınıfı Pima nesnesi gönderme tutamaçları** *(ux_device_class_pima_object_handles_send)* |
| ![Device Class Pima nesne bilgisi al simgesi](./media/user-guide/usbx-events/image26.png)    | **Cihaz sınıfı Pima nesnesi bilgileri Get** *(ux_device_class_pima_object_info_get)* |
| ![Device Class Pima nesne bilgileri gönderme simgesi](./media/user-guide/usbx-events/image27.png)    | **Device Class Pima nesne bilgileri gönderme** *(ux_device_class_pima_object_info_send)* |
| ![Cihaz sınıfı Pima nesneleri numara Gönder simgesi](./media/user-guide/usbx-events/image28.png)    | **Cihaz sınıfı Pima nesneleri numara gönderme** *(ux_device_class_pima_objects_number_send)* |
| ![Device Class Pima kısmi nesne verileri al simgesi](./media/user-guide/usbx-events/image29.png)    | **Device Class Pima kısmi nesne verileri al** *(ux_device_class_pima_partial_object_data_get)* |
| ![Cihaz sınıfı Pima yanıtı gönderme simgesi](./media/user-guide/usbx-events/image30.png)    | **Cihaz sınıfı Pima yanıtı gönderme** *(ux_device_class_pima_response_send)*|
| ![Cihaz sınıfı Pima depolama g D Gönder simgesi](./media/user-guide/usbx-events/image31.png)    | **Cihaz sınıfı Pima depolama kimliği gönderme** *(ux_device_class_pima_storage_id_send)* |
| ![Cihaz sınıfı Pima depolama bilgileri gönderme simgesi](./media/user-guide/usbx-events/image32.png)    | **Cihaz sınıfı Pima depolama bilgileri gönderme** *(ux_device_class_pima_storage_info_send)* |
| ![Cihaz sınıfı R N D ı etkinleştirme simgesi](./media/user-guide/usbx-events/image33.png)    | **Cihaz sınıfı rndis etkinleştir** *(ux_device_class_rndis_activate)* |
| ![Cihaz sınıfı R N D ı devre dışı bırak simgesi](./media/user-guide/usbx-events/image34.png)    | **Cihaz sınıfı rndis devre dışı bırak** *(ux_device_class_rndis_deactivate)* |
| ![Cihaz sınıfı R N D ı Ileti Keep Aliveicon](./media/user-guide/usbx-events/image35.png)    | **Cihaz sınıfı rndis Iletisi canlı tut** *(ux_device_class_rndis_msg_keep_alive)* |
| ![Cihaz sınıfı R N D ı Ileti sorgu simgesi](./media/user-guide/usbx-events/image36.png)    | **Cihaz sınıfı rndis Ileti sorgusu** *(ux_device_class_rndis_msg_query)* |
| ![Cihaz sınıfı R N D ı Ileti sıfırlama simgesi](./media/user-guide/usbx-events/image37.png)    | **Cihaz sınıfı rndis Ileti sıfırlama** *(ux_device_class_rndis_msg_reset)* |
| ![Cihaz sınıfı R N D ı Ileti kümesi simgesi](./media/user-guide/usbx-events/image38.png)    | **Cihaz sınıfı rndis Ileti kümesi** *(ux_device_class_rndis_msg_set)* |
| ![Cihaz sınıfı R N D ı paket alma simgesi](./media/user-guide/usbx-events/image39.png)    | **Cihaz sınıfı rndis paket alma** *(ux_device_class_rndis_packet_receive)* |
| ![Cihaz sınıfı R N D ı paket Iletme simgesi](./media/user-guide/usbx-events/image40.png)    | **Cihaz sınıfı rndis paket iletimi** *(ux_device_class_rndis_packet_transmit)* |
| ![Cihaz sınıfı depolama etkinleştirme simgesi](./media/user-guide/usbx-events/image41.png)    | **Cihaz sınıfı depolama etkinleştir** *(ux_device_class_storage_activate)* |
| ![Cihaz sınıfı depolamayı devre dışı bırakma simgesi](./media/user-guide/usbx-events/image42.png)    | **Cihaz sınıfı depolamayı devre dışı bırakma** *(ux_device_class_storage_deactivate)* |
| ![Cihaz sınıfı depolama biçimi simgesi](./media/user-guide/usbx-events/image43.png)    | **Cihaz sınıfı depolama biçimi** *(ux_device_class_storage_format)* |
| ![Cihaz sınıfı depolama sorgulama simgesi](./media/user-guide/usbx-events/image44.png)    | **Cihaz sınıfı depolama sorgusu** *(ux_device_class_storage_inquiry)* |
| ![Cihaz sınıfı depolama modu seçme simgesi](./media/user-guide/usbx-events/image45.png)    | **Cihaz sınıfı depolama modu seçme** *(ux_device_class_storage_mode_select)* |
| ![Cihaz sınıfı depolama modu algılama simgesi](./media/user-guide/usbx-events/image46.png)    | **Cihaz sınıfı depolama modu algılama** *(ux_device_class_storage_mode_sense)* |
| ![Cihaz sınıfı depolaması medya kaldırma simgesine Izin vermeyi engelliyor](./media/user-guide/usbx-events/image47.png)    | **Cihaz sınıfı depolaması medya kaldırılmasına Izin vermeyi engelliyor** *(ux_device_class_storage_prevent_allow_media_removal)* |
| ![Cihaz sınıfı depolama okuma simgesi](./media/user-guide/usbx-events/image48.png)    | **Cihaz sınıfı depolama okuma** *(ux_device_class_storage_read)* |
| ![Cihaz sınıfı depolama okuma kapasitesi simgesi](./media/user-guide/usbx-events/image49.png)    | **Cihaz sınıfı depolama okuma kapasitesi** *(ux_device_class_storage_read_capacity)* |
| ![Cihaz sınıfı depolama okuma biçimi kapasitesi simgesi](./media/user-guide/usbx-events/image50.png)    | **Cihaz sınıfı depolama okuma biçimi kapasitesi** *(ux_device_class_storage_read_format_capacity)* |
| ![Device Class depolama okuma TOC simgesi](./media/user-guide/usbx-events/image51.png)    | **Device Class DEPOLAMASı TOC okuma** *(ux_device_class_storage_read_toc)* |
| ![Cihaz sınıfı depolama Isteği algılama simgesi](./media/user-guide/usbx-events/image52.png)    | **Cihaz sınıfı depolama Isteği algılama** *(ux_device_class_storage_request_sense)* |
| ![Cihaz sınıfı depolama başlatma durdurma simgesi](./media/user-guide/usbx-events/image53.png)    | **Cihaz sınıfı depolama başlatma durdurma** *(ux_device_class_storage_start_stop)* |
| ![Cihaz sınıfı depolama sınaması hazırlanıyor simgesi](./media/user-guide/usbx-events/image54.png)    | **Cihaz sınıfı depolama sınaması hazırlanıyor** *(ux_device_class_storage_test_ready)* |
| ![Cihaz sınıfı depolama doğrulama simgesi](./media/user-guide/usbx-events/image55.png)    | **Cihaz sınıfı depolama doğrulaması** *(ux_device_class_storage_verify)* |
| ![Cihaz sınıfı depolama yazma simgesi](./media/user-guide/usbx-events/image56.png)    | **Cihaz sınıfı depolama yazma** *(ux_device_class_storage_write)* |
| ![Cihaz yığını alternatif ayarı al simgesi](./media/user-guide/usbx-events/image57.png)    | **Cihaz yığını alternatif ayarı al** *(ux_device_stack_alternate_setting_get)* |
| ![Cihaz yığını alternatif ayarı kümesi simgesi](./media/user-guide/usbx-events/image58.png)    | **Cihaz yığını alternatif ayar kümesi** *(ux_device_stack_alternate_setting_set)* |
| ![Cihaz yığını sınıfı kayıt simgesi](./media/user-guide/usbx-events/image59.png)    | **Cihaz yığını sınıf kaydı** *(ux_device_stack_class_register)* |
| ![Cihaz yığını temiz Özellik simgesi](./media/user-guide/usbx-events/image60.png)    | **Cihaz yığını temiz Özellik** *(ux_device_stack_clear_feature)* |
| ![Cihaz yığını yapılandırması Get simgesi](./media/user-guide/usbx-events/image61.png)    | **Cihaz yığını yapılandırma Get** *(ux_device_stack_configuration_get)* |
| ![Cihaz yığını yapılandırma kümesi simgesi](./media/user-guide/usbx-events/image62.png)    | **Cihaz yığını yapılandırma kümesi** *(ux_device_stack_configuration_set)* |
| ![Cihaz yığını bağlantı simgesi](./media/user-guide/usbx-events/image63.png)    | **Cihaz yığını bağlantısı** *(ux_device_stack_connect)* |
| ![Cihaz yığını tanımlayıcısı gönderme simgesi](./media/user-guide/usbx-events/image64.png)    | **Cihaz yığını tanımlayıcısı gönderme** *(ux_device_stack_descriptor_send)* |
| ![Cihaz yığını bağlantı kesme simgesi](./media/user-guide/usbx-events/image65.png)    | **Cihaz yığını bağlantısını kesme** *(ux_device_stack_disconnect)* |
| ![Cihaz yığını uç noktası kabin simgesi](./media/user-guide/usbx-events/image66.png)    | **Cihaz yığını uç noktası kabini** *(ux_device_stack_endpoint_stall)* |
| ![Cihaz yığını durum Al simgesi](./media/user-guide/usbx-events/image67.png)    | **Cihaz yığını Get durumu** *(ux_device_stack_get_status)* |
| ![Cihaz yığını ana bilgisayarı uyandırma simgesi](./media/user-guide/usbx-events/image68.png)    | **Cihaz yığın ana bilgisayarı uyandırma** *(ux_device_stack_host_wakeup)* |
| ![Cihaz yığını başlatma simgesi](./media/user-guide/usbx-events/image69.png)    | **Cihaz yığını başlatma** *(ux_device_stack_initialize)* |
| ![Cihaz yığını arabirimi silme simgesi](./media/user-guide/usbx-events/image70.png)    | **Cihaz yığını arabirimini silme** *(ux_device_stack_interface_delete)* |
| ![Cihaz yığını arabirimi al simgesi](./media/user-guide/usbx-events/image71.png)    | **Cihaz yığını arabirimi al** *(ux_device_stack_interface_get)* |
| ![Cihaz yığını arabirim kümesi simgesi](./media/user-guide/usbx-events/image72.png)    | **Cihaz yığını arabirim kümesi** *(ux_device_stack_interface_set)* |
| ![Cihaz yığını kümesi özellik simgesi](./media/user-guide/usbx-events/image73.png)    | **Cihaz yığını kümesi özelliği** *(ux_device_stack_set_feature)* |
| ![Cihaz yığını aktarım Iptali simgesi](./media/user-guide/usbx-events/image74.png)    | **Cihaz yığını aktarımı iptali** *(ux_device_stack_transfer_abort)* |
| ![* Cihaz yığını tüm Isteği Iptal et simgesi](./media/user-guide/usbx-events/image75.png)    | **Cihaz yığın aktarımı tüm Istek iptali** *(ux_device_stack_transfer_all_request_abort)* |
| ![Cihaz yığını aktarım Isteği simgesi](./media/user-guide/usbx-events/image76.png)    | **Cihaz yığını aktarım isteği** *(ux_device_stack_transfer_request)* |
| ![Ana bilgisayar sınıfı ASIX etkinleştir simgesi](./media/user-guide/usbx-events/image77.png)    | **Ana bilgisayar sınıfı Aaltıetkinleştir** *(ux_host_class_asix_activate)* |
| ![Ana makine sınıfı ASIX devre dışı simgesi](./media/user-guide/usbx-events/image78.png)    | **Ana bilgisayar sınıfı aaltı devre dışı** *(ux_host_class_asix_deactivate)* |
| ![Ana bilgisayar sınıfı Aaltıkesme bildirimi simgesi](./media/user-guide/usbx-events/image79.png)    | **Ana bilgisayar sınıfı asix kesme bildirimi** *(ux_host_class_asix_interrupt_notification)* |
| ![Ana bilgisayar sınıfı Aaltıoku simgesi](./media/user-guide/usbx-events/image80.png)    | **Ana bilgisayar sınıfı Aaltıokuma** *(ux_host_class_asix_read)* |
| ![Ana bilgisayar sınıfı Aaltıyaz simgesi](./media/user-guide/usbx-events/image81.png)    | **Ana bilgisayar sınıfı Aaltıyaz** *(ux_host_class_asix_write)* |
| ![Konak sınıfı ses etkinleştirme simgesi](./media/user-guide/usbx-events/image82.png)    | **Konak sınıfı ses etkinleştirme** *(ux_host_class_audio_activate)* |
| ![Konak sınıfı ses denetimi değeri Al simgesi](./media/user-guide/usbx-events/image83.png)    | **Konak sınıfı ses denetimi değeri Get** *(ux_host_class_audio_control_value_get)* |
| ![Konak sınıfı ses denetimi değer kümesi simgesi](./media/user-guide/usbx-events/image84.png)    | **Konak sınıfı ses denetimi değer kümesi** *(ux_host_class_audio_control_value_set)* |
| ![Konak sınıfı ses devre dışı bırakma simgesi](./media/user-guide/usbx-events/image85.png)    | **Konak sınıfı ses devre dışı bırakma** *(ux_host_class_audio_deactivate)* |
| ![Konak sınıfı ses okuma simgesi](./media/user-guide/usbx-events/image86.png)    | **Ana bilgisayar sınıfı ses okuma** *(ux_host_class_audio_read)* |
| ![Konak sınıfı ses akışı örneklemesi alma simgesi](./media/user-guide/usbx-events/image87.png)    | **Konak sınıfı ses akışı örneklemesi alma** *(ux_host_class_audio_streaming_sampling_get)* |
| ![Konak sınıfı ses akışı örnekleme kümesi simgesi](./media/user-guide/usbx-events/image88.png)    | **Konak sınıfı ses akışı örnekleme kümesi** *(ux_host_class_audio_streaming_sampling_set)* |
| ![Konak sınıfı ses yazma simgesi](./media/user-guide/usbx-events/image89.png)    | **Ana bilgisayar sınıfı ses yazma** *(ux_host_class_audio_write)* |
| ![Ana bilgisayar sınıfı C D C A C M etkinleştirme simgesi](./media/user-guide/usbx-events/image90.png)    | **Ana bilgisayar sınıfı CDC ACM Activate** *(ux_host_class_cdc_acm_activate)* |
| ![Ana bilgisayar sınıfı C D C A C M devre dışı bırakma simgesi](./media/user-guide/usbx-events/image91.png)    | **Ana bilgisayar sınıfı CDC ACM Deactivate** *(ux_host_class_cdc_acm_deactivate)* |
| ![Ana bilgisayar sınıfı C D C bir C M ı O C T ı kanal simgesi](./media/user-guide/usbx-events/image92.png)    | **Ana bilgisayar sınıfı CDC ACM IOCTL-kanal** *(ux_host_class_cdc_acm_ioctl_abort_in_pipe)* |
| ![Ana bilgisayar sınıfı C D C A C M ı u C T L I](./media/user-guide/usbx-events/image93.png)    | **Ana bilgisayar sınıfı CDC ACM IOCTL Iptal kanalı** *(ux_host_class_cdc_acm_ioctl_abort_out_pipe)* |
| ![Ana bilgisayar sınıfı C D C A C M ı O C T I cihaz durum simgesi al](./media/user-guide/usbx-events/image94.png)    | **Ana bilgisayar sınıfı CDC ACM IOCTL cihaz durumunu Al** *(ux_host_class_cdc_acm_ioctl_get_device_status)* |
| ![Ana bilgisayar sınıfı C D C A C M ı O C T m](./media/user-guide/usbx-events/image95.png)    | **Ana bilgisayar sınıfı CDC ACM IOCTL al satırı kodlama** *(ux_host_class_cdc_acm_ioctl_get_line_coding)* |
| ![Ana bilgisayar sınıfı C D C A C M ı O C T m](./media/user-guide/usbx-events/image96.png)    | **Ana bilgisayar sınıfı CDC ACM IOCTL bildirimi geri araması** *(ux_host_class_cdc_acm_ioctl_notification_callback)* |
| ![Ana bilgisayar sınıfı C D C c M I m C T ı gönder kesme simgesi](./media/user-guide/usbx-events/image97.png)    | **Ana bilgisayar sınıfı CDC ACM IOCTL gönderme sonu** *(ux_host_class_cdc_acm_ioctl_send_break)* |
| ![Ana bilgisayar sınıfı C D C c M ı O C T m](./media/user-guide/usbx-events/image98.png)    | **Ana bilgisayar sınıfı CDC ACM IOCTL kümesi satırı kodlama** *(ux_host_class_cdc_acm_ioctl_set_line_coding)* |
| ![Ana bilgisayar sınıfı C D C c M ı O C T ı](./media/user-guide/usbx-events/image99.png)    | **Ana bilgisayar sınıfı CDC ACM IOCTL kümesi satır durumu** *(ux_host_class_cdc_acm_ioctl_set_line_state)* |
| ![Ana bilgisayar sınıfı C D C bir C M oku simgesi](./media/user-guide/usbx-events/image100.png)    | **Ana bilgisayar sınıfı CDC ACM okuma** *(ux_host_class_cdc_acm_read)* |
| ![Ana bilgisayar sınıfı C D C A C M alma başlangıç simgesi](./media/user-guide/usbx-events/image101.png)    | **Ana bilgisayar sınıfı CDC ACM alma başlangıcı** *(ux_host_class_cdc_acm_reception_start)* |
| ![Ana bilgisayar sınıfı C D C bir C M alımı durdur simgesi](./media/user-guide/usbx-events/image102.png)    | **Ana bilgisayar sınıfı CDC ACM alımı durdur** *(ux_host_class_cdc_acm_reception_stop)* |
| ![Ana bilgisayar sınıfı C D C c M yazma simgesi](./media/user-guide/usbx-events/image103.png)    | **Ana bilgisayar sınıfı CDC ACM yazma** *(ux_host_class_cdc_acm_write)* |
| ![Host Class Dpump etkinleştir simgesi](./media/user-guide/usbx-events/image104.png)    | **Konak sınıfı Dpump etkinleştir** *(ux_host_class_dpump_activate)* |
| ![Konak sınıfı Dpump etkinliğini kaldırma simgesi](./media/user-guide/usbx-events/image105.png)    | **Ana sınıf Dpump devre dışı bırakma** *(ux_host_class_dpump_deactivate)* |
| ![Konak sınıfı Dpump oku simgesi](./media/user-guide/usbx-events/image106.png)    | **Ana bilgisayar sınıfı Dpump okuma** *(ux_host_class_dpump_read)* |
| ![Ana sınıf Dpump yazma simgesi](./media/user-guide/usbx-events/image107.png)    | **Ana bilgisayar sınıfı Dpump yazma** *(ux_host_class_dpump_write)* |
| ![Konak sınıfı HID etkinleştirme simgesi](./media/user-guide/usbx-events/image108.png)    | **Host Class HID etkinleştir** *(ux_host_class_hid_activate)* |
| ![Konak sınıfı HID Istemci kaydı simgesi](./media/user-guide/usbx-events/image109.png)    | **Konak sınıfı HID Istemci kaydı** *(ux_host_class_hid_client_register)* |
| ![Konak sınıfı HID devre dışı bırakma simgesi](./media/user-guide/usbx-events/image110.png)    | **Konak sınıfı HID etkinliğini kaldırma** *(ux_host_class_hid_deactivate)* |
| ![Konak sınıfı HID boşta al al simgesi](./media/user-guide/usbx-events/image111.png)    | **Ana bilgisayar sınıfı HID boşta al** *(ux_host_class_hid_idle_get)* |
| ![Konak sınıfı HID boşta kümesi simgesi](./media/user-guide/usbx-events/image112.png)    | **Ana bilgisayar sınıfı HID boşta kümesi** *(ux_host_class_hid_idle_set)* |
| ![Host Class HID Klavye etkinleştirme simgesi](./media/user-guide/usbx-events/image113.png)    | **Host Class HID Klavye etkinleştir** *(ux_host_class_hid_keyboard_activate)* |
| ![Host Class HID Klavye devre dışı simgesi](./media/user-guide/usbx-events/image114.png)    | **Host Class HID Klavye devre dışı bırakma** *(ux_host_class_hid_keyboard_deactivate)* |
| ![Host Class HID fare etkinleştirme simgesi](./media/user-guide/usbx-events/image115.png)    | **Host Class HID fare etkinleştir** *(ux_host_class_hid_mouse_activate)* |
| ![Konak sınıfı HID fare devre dışı simgesi](./media/user-guide/usbx-events/image116.png)    | **Host Class HID fare devre dışı bırakma** *(ux_host_class_hid_mouse_deactivate)* |
| ![Konak sınıfı HID uzaktan denetim etkinleştirme simgesi](./media/user-guide/usbx-events/image117.png)    | **Konak sınıfı HID uzaktan denetim etkinleştirme** *(ux_host_class_hid_remote_control_activate)* |
| ![Konak sınıfı HID uzaktan denetim devre dışı simgesi](./media/user-guide/usbx-events/image118.png)    | **Konak sınıfı HID uzaktan denetim devre dışı** *(ux_host_class_hid_remote_control_deactivate)* |
| ![Konak sınıfı HID raporu al simgesi](./media/user-guide/usbx-events/image119.png)    | **Konak sınıfı HID raporu Get** *(ux_host_class_hid_report_get)* |
| ![Konak sınıfı HID rapor kümesi simgesi](./media/user-guide/usbx-events/image120.png)    | **Konak sınıfı HID rapor kümesi** *(ux_host_class_hid_report_set)* |
| ![Konak sınıfı hub etkinleştirme simgesi](./media/user-guide/usbx-events/image121.png)    | **Konak sınıfı hub 'ı etkinleştir** *(ux_host_class_hub_activate)* |
| ![Host Class hub değişikliği algılama simgesi](./media/user-guide/usbx-events/image122.png)    | **Ana bilgisayar sınıf hub değişikliği algılaması** *(ux_host_class_hub_change_detect)* |
| ![* Konak sınıfı hub 'ı devre dışı bırakma simgesi](./media/user-guide/usbx-events/image123.png)    | **Konak sınıfı hub 'ı devre dışı bırakma** *(ux_host_class_hub_deactivate)* |
| ![Konak sınıf hub 'ı bağlantı noktası değişiklik bağlantı Işlemi simgesi](./media/user-guide/usbx-events/image124.png)    | **Konak sınıf hub 'ı bağlantı noktası değiştirme bağlantı işlemi** *(ux_host_class_hub_port_change_connection_process)* |
| ![Konak sınıfı hub bağlantı noktası değişikliği etkinleştirme Işlemi simgesi](./media/user-guide/usbx-events/image125.png)    | **Host Class hub bağlantı noktası değişikliği etkinleştirme işlemi** *(ux_host_class_hub_port_change_enable_process)* |
| ![Ana sınıf hub 'ı bağlantı noktası geçerli Işlem simgesi değişikliği](./media/user-guide/usbx-events/image126.png)    | Geçerli Işlem *(ux_host_class_hub_port_change_over_current_process)* **üzerinde ana bilgisayar sınıfı hub bağlantı noktası değişikliği** |
| ![Konak sınıf hub 'ı bağlantı noktası değişiklik sıfırlama Işlemi simgesi](./media/user-guide/usbx-events/image127.png)    | **Konak sınıf hub 'ı bağlantı noktası değişiklik sıfırlama işlemi** *(ux_host_class_hub_port_change_reset_process)* |
| ![Konak sınıf hub 'ı bağlantı noktası değiştirme Işlemi askıya alma simgesi](./media/user-guide/usbx-events/image128.png)    | **Host Class hub bağlantı noktası değiştirme askıya alma işlemi** *(ux_host_class_hub_port_change_suspend_process)* |
| ![Konak sınıfı Pima etkinleştirme simgesi](./media/user-guide/usbx-events/image129.png)    | **Konak sınıfı Pima etkinleştir** *(ux_host_class_prima_activate)* |
| ![Konak sınıfı Pima devre dışı bırakma simgesi](./media/user-guide/usbx-events/image130.png)    | **Konak sınıfı Pima devre dışı bırakma** *(ux_host_class_pima_deactivate)* |
| ![Konak sınıfı Pima cihaz bilgileri al simgesi](./media/user-guide/usbx-events/image131.png)    | **Konak sınıfı Pima cihaz bilgileri Get** *(ux_host_class_pima_device_info_get)* |
| ![Konak sınıfı Pima cihazı sıfırlama simgesi](./media/user-guide/usbx-events/image132.png)    | **Konak sınıfı Pima cihazı sıfırlama** *(ux_host_class_pima_device_reset)* |
| ![Konak sınıfı Pima bildirimi simgesi](./media/user-guide/usbx-events/image133.png)    | **Konak sınıfı Pima bildirimi** *(ux_host_class_pima_notification)* |
| ![Konak sınıfı Pima sayısı nesneleri Al simgesi](./media/user-guide/usbx-events/image134.png)    | **Konak sınıfı Pima sayısı nesneleri Al** *(ux_host_class_pima_num_objects_get)* |
| ![Ana sınıf Pima nesnesi kapatma simgesi](./media/user-guide/usbx-events/image135.png)    | **Konak sınıfı Pima nesnesi kapat** *(ux_host_class_pima_object_close)* |
| ![Konak sınıfı Pima nesnesi kopyalama simgesi](./media/user-guide/usbx-events/image136.png)    | **Konak sınıfı Pima nesne kopyası** *(ux_host_class_pima_object_copy)* |
| ![Konak sınıfı Pima nesnesi silme simgesi](./media/user-guide/usbx-events/image137.png)    | **Konak sınıfı Pima nesnesi silme** *(ux_host_class_pima_object_delete)* |
| ![Ana sınıf Pima nesnesi Al simgesi](./media/user-guide/usbx-events/image138.png)    | **Konak sınıfı Pima nesnesi Get** *(ux_host_class_pima_object_get)* |
| ![Konak sınıfı Pima nesnesi bilgileri al simgesi](./media/user-guide/usbx-events/image139.png)    | **Konak sınıfı Pima nesnesi bilgileri al** *(ux_host_class_pima_object_info_get)* |
| ![Konak sınıfı Pima nesne bilgileri gönderme simgesi](./media/user-guide/usbx-events/image140.png)    | **Konak sınıfı Pima nesne bilgileri gönderme** *(ux_host_class_pima_object_info_send)* |
| ![Konak sınıfı Pima nesnesi taşıma simgesi](./media/user-guide/usbx-events/image141.png)    | **Konak sınıfı Pima nesnesi taşıma** *(ux_host_class_pima_object_move)* |
| ![Ana sınıf Pima nesnesi Gönder simgesi](./media/user-guide/usbx-events/image142.png)    | **Konak sınıfı Pima nesnesi gönderme** *(ux_host_class_pima_object_send)* |
| ![Konak sınıfı Pima nesne aktarımı Iptali simgesi](./media/user-guide/usbx-events/image143.png)    | **Konak sınıfı Pima nesnesi aktarımı iptali** *(ux_host_class_object_transfer_abort)* |
| ![Konak sınıfı Pima oku simgesi](./media/user-guide/usbx-events/image144.png)    | **Ana bilgisayar sınıfı Pima okuma** *(ux_host_class_pima_read)* |
| ![Konak sınıfı Pima Isteği Iptal simgesi](./media/user-guide/usbx-events/image145.png)    | **Konak sınıfı Pima Isteği iptali** *(ux_host_class_pima_request_cancel)* |
| ![Ana sınıf Pima oturumu kapatma simgesi](./media/user-guide/usbx-events/image146.png)    | **Ana bilgisayar sınıfı Pima oturumu kapalı** *(ux_host_class_pima_session_close)* |
| ![Konak sınıfı Pima oturumu açma simgesi](./media/user-guide/usbx-events/image147.png)    | **Konak sınıfı Pima oturumu açık** *(ux_host_class_pima_session_open)* |
| ![Konak sınıfı Pima depolama kimlikleri al simgesi](./media/user-guide/usbx-events/image148.png)    | **Konak sınıfı Pima depolama kimlikleri al** *(ux_host_class_pima_storage_ids_get)* |
| ![Konak sınıfı Pima depolama bilgileri al simgesi](./media/user-guide/usbx-events/image149.png)    | **Konak sınıfı Pima depolama bilgileri Get** *(ux_host_class_pima_storage_info_get)* |
| ![Konak sınıfı Pima Thumb al simgesi](./media/user-guide/usbx-events/image150.png)    | **Konak sınıfı Pima Parmak Izi al** *(ux_host_class_pima_thumb_get)* |
| ![Konak sınıfı Pima yazma simgesi](./media/user-guide/usbx-events/image151.png)    | **Konak sınıfı Pima yazma** *(ux_host_class_pima_write)* |
| ![Konak sınıfı yazıcı etkinleştirme simgesi](./media/user-guide/usbx-events/image152.png)    | **Konak sınıfı yazıcısını etkinleştir** *(ux_host_class_printer_activate)* |
| ![Konak sınıfı yazıcı devre dışı simgesi](./media/user-guide/usbx-events/image153.png)    | **Konak sınıfı yazıcısını devre dışı bırak** *(ux_host_class_printer_deactivate)* |
| ![Konak sınıfı yazıcı adı Al simgesi](./media/user-guide/usbx-events/image154.png)    | **Ana bilgisayar sınıfı yazıcı adı Get** *(ux_host_class_printer_name_get)* |
| ![Ana bilgisayar sınıfı yazıcı okuma simgesi](./media/user-guide/usbx-events/image155.png)    |  **Ana bilgisayar sınıfı yazıcı okuma** *(ux_host_class_printer_read)* |
| ![Konak sınıfı yazıcı geçici sıfırlama simgesi](./media/user-guide/usbx-events/image156.png)    | **Konak sınıfı yazıcı yazılımdan sıfırlama** *(ux_host_class_printer_soft_reset)* |
| ![Konak sınıfı yazıcı durumu Al simgesi](./media/user-guide/usbx-events/image157.png)    | **Konak sınıfı yazıcı durumu Al** *(ux_host_class_printer_status_get)* |
| ![Konak sınıfı yazıcı yazma simgesi](./media/user-guide/usbx-events/image158.png)    | **Ana bilgisayar sınıfı yazıcı yazma** *(ux_host_class_printer_write)* |
| ![Konak sınıfı Prolific etkinleştirme simgesi](./media/user-guide/usbx-events/image159.png)    | **Konak sınıfı Prolific etkinleştir** *(ux_host_class_prolific_activate)* |
| ![Konak sınıfı Prolific devre dışı bırakma simgesi](./media/user-guide/usbx-events/image160.png)    | **Konak sınıfı Prolific etkinliğini kaldır** *(ux_host_class_prolific_deactivate)* |
| ![Kanal simgesinde ana bilgisayar sınıfı proo C T L durdur](./media/user-guide/usbx-events/image161.png)    | **Ana bilgisayar sınıfı Işlem kanalında IOCTL iptali** *(ux_host_class_prolific_ioctl_abort_in_pipe)* |
| ![Ana bilgisayar sınıfı proo C T L m ı Durdur kanal simgesi](./media/user-guide/usbx-events/image162.png)    | **Ana bilgisayar sınıfı Prolific IOCTL Iptal kanalı** *(ux_host_class_prolific_ioctl_abort_out_pipe)* |
| ![Konak sınıfı Prolific g T C T L bir cihaz durumu simgesi al](./media/user-guide/usbx-events/image163.png)    | **Konak sınıfı Prolific IOCTL cihaz durumunu Al** *(ux_host_class_prolific_ioctl_get_device_status)* |
| ![Konak sınıfı Prolific ı T C T L Class for satırı kodlama simgesi](./media/user-guide/usbx-events/image164.png)    | **Konak sınıfı Prolific IOCTL al satır kodlama** *(ux_host_class_prolific_ioctl_get_line_coding)* |
| ![Ana bilgisayar sınıfı Prolific T I do u simgesi](./media/user-guide/usbx-events/image165.png)    | **Ana makine sınıfı, IOCTL Temizleme** *(ux_host_class_prolific_ioctl_purge)* |
| ![Konak sınıfı Prolific ı T C T m rapor cihaz durumu değiştirme simgesi](./media/user-guide/usbx-events/image166.png)    | **Konak sınıfı Prolific IOCTL rapor cihaz durumu değişikliği** *(ux_host_class_prolific_ioctl_report_device_status_change)* |
| ![Konak sınıfı Prolific ı T C T L gönderme sonu simgesi](./media/user-guide/usbx-events/image167.png)    | **Ana bilgisayar sınıfı, IOCTL gönderme sonu** *(ux_host_class_prolific_ioctl_send_break)* |
| ![Konak sınıfı Prolific ı T C T L Class for satırı kodlama simgesi](./media/user-guide/usbx-events/image168.png)    | **Konak sınıfı Prolific IOCTL kümesi satırı kodlama** *(ux_host_class_prolific_ioctl_set_line_coding)* |
| ![Konak sınıfı Prolific ı T C T L s satır durumu simgesi](./media/user-guide/usbx-events/image169.png)    | **Konak sınıfı Prolific IOCTL kümesi satır durumu** *(ux_host_class_prolific_ioctl_set_line_state)* |
| ![Konak sınıfı Prolific okuma simgesi](./media/user-guide/usbx-events/image170.png)    | **Ana bilgisayar sınıfı, okuma** *(ux_host_class_prolific_read)* |
| ![Konak sınıfı Prolific alma başlangıç simgesi](./media/user-guide/usbx-events/image171.png)    | **Ana bilgisayar sınıfı Prolific alma başlangıcı** *(ux_host_class_prolific_reception_start)* |
| ![Konak sınıfı Prolific alımı durdurma simgesi](./media/user-guide/usbx-events/image172.png)    | **Konak sınıfı Prolific alma durdurma** *(ux_host_class_prolific_reception_stop)* |
| ![Ana makine sınıfı başlangıç yazma simgesi](./media/user-guide/usbx-events/image173.png)    | **Ana bilgisayar sınıfı başlangıç yazma** *(ux_host_class_prolific_write)* |
| ![Konak sınıfı depolama etkinleştirme simgesi](./media/user-guide/usbx-events/image174.png)    | **Konak sınıfı depolama etkinleştir** *(ux_host_class_storage_activate)* |
| ![Konak sınıfı depolamayı devre dışı bırakma simgesi](./media/user-guide/usbx-events/image175.png)    | **Konak sınıfı depolamayı devre dışı bırakma** (*ux_host_class_storage_deactivate)* |
| ![Konak sınıfı depolama medyası kapasitesi al simgesi](./media/user-guide/usbx-events/image176.png)    | **Konak sınıfı depolama medyası kapasitesi al** *(ux_host_class_storage_media_capacity_get)* |
| ![Konak sınıfı depolama medya biçimi kapasitesi al simgesi](./media/user-guide/usbx-events/image177.png)    | **Konak sınıfı depolama medya biçimi kapasitesi al** *(ux_host_class_storage_media_format_capacity_get)* |
| ![Konak sınıfı depolama medyası bağlama simgesi](./media/user-guide/usbx-events/image178.png)    | **Konak sınıfı depolama medyası bağlama** (ux_host_class_storage_media_mount) * |
| ![Konak sınıfı depolama medyası açık simgesi](./media/user-guide/usbx-events/image179.png)    | **Konak sınıfı depolama medyası açık** *(ux_host_class_storage_media_open)* |
| ![Konak sınıfı depolama medyası okuma simgesi](./media/user-guide/usbx-events/image180.png)    | **Konak sınıfı depolama medyası okuma** *(ux_host_class_storage_media_read)* |
| ![Konak sınıfı depolama medyası yazma simgesi](./media/user-guide/usbx-events/image181.png)    | **Konak sınıfı depolama medyası yazma** *(ux_host_class_storage_media_write)* |
| ![Konak sınıfı depolama Isteği algılama simgesi](./media/user-guide/usbx-events/image182.png)    | **Konak sınıfı depolama Isteği algılama** *(ux_host_class_storage_request_sense)* |
| ![Konak sınıfı depolama başlatma durdurma simgesi](./media/user-guide/usbx-events/image183.png)    | **Konak sınıfı depolama başlatma durdurma** *(ux_host_class_storage_start_stop)* |
| ![Konak sınıfı depolama birimi için Ready test simgesi](./media/user-guide/usbx-events/image184.png)    | **Konak sınıfı depolama birimi Için hazırlanma testi** *(ux_host_class_storage_activate)* |
| ![Konak yığını sınıf örneği oluşturma simgesi](./media/user-guide/usbx-events/image185.png)    | **Konak yığını sınıf örneği oluşturma** *(ux_host_stack_class_instance_create)* |
| ![Konak yığını sınıf örneği yok etme simgesi](./media/user-guide/usbx-events/image186.png)    | **Konak yığını sınıf örneği yok etme** *(ux_host_stack_class_instance_destroy)* |
| ![Konak yığını yapılandırması silme simgesi](./media/user-guide/usbx-events/image187.png)    | **Konak yığını yapılandırması silme** *(ux_host_stack_configuration_delete)* |
| ![Konak yığını yapılandırması sıralama simgesi](./media/user-guide/usbx-events/image188.png)    | **Konak yığını yapılandırması numaralandırması** *(ux_host_stack_configuration_enumerate)* |
| ![Konak yığını yapılandırma örneği oluşturma simgesi](./media/user-guide/usbx-events/image189.png)    | **Konak yığını yapılandırma örneği oluşturma** *(ux_host_stack_configuration_instance_create)* |
| ![Konak yığını yapılandırma örneği silme simgesi](./media/user-guide/usbx-events/image190.png)    | **Konak yığını yapılandırma örneği silme** *(ux_host_stack_configuration_instance_delete)* |
| ![Konak yığını yapılandırma kümesi simgesi](./media/user-guide/usbx-events/image191.png)    | **Konak yığını yapılandırma kümesi** *(ux_host_stack_configuration_set)* |
| ![Konak yığını cihaz adresi kümesi simgesi](./media/user-guide/usbx-events/image192.png)    | **Konak yığını cihaz adresi kümesi** *(ux_host_stack_device_set)* |
| ![Konak yığını cihaz yapılandırması Get simgesi](./media/user-guide/usbx-events/image193.png)    | **Konak yığını cihaz yapılandırması Get** *(ux_host_stack_device_configuration_get)* |
| ![Konak yığını cihaz yapılandırması seçim simgesi](./media/user-guide/usbx-events/image194.png)    | **Konak yığını cihaz yapılandırması seçme** *(ux_host_stack_device_configuration_select)* |
| ![Konak yığını cihaz tanımlayıcısı okuma simgesi](./media/user-guide/usbx-events/image195.png)    | **Konak yığını cihaz tanımlayıcısı okuma** *(ux_host_stack_device_descriptor_read)* |
| ![Konak yığını cihazının al simgesi](./media/user-guide/usbx-events/image196.png)    | **Konak yığını cihazının Get** (ux_host_stack_device_get) |
| ![Konak yığını cihaz kaldırma simgesi](./media/user-guide/usbx-events/image197.png)    | **Konak yığını cihazını kaldır** (ux_host_stack_device_get) |
| ![Ana bilgisayar yığını cihaz kaynağı boş simgesi](./media/user-guide/usbx-events/image198.png)    | **Ana bilgisayar yığını cihaz kaynağı boş** (ux_host_stack_device_resource_free) |
| ![Konak yığını uç noktası örneği oluşturma simgesi](./media/user-guide/usbx-events/image199.png)    | **Konak yığını uç noktası örneği oluşturma** (ux_host_stack_endpoint_instance_create) |
| ![Konak yığın uç noktası örneği silme simgesi](./media/user-guide/usbx-events/image200.png)    | **Konak yığını uç noktası örneği silme** (ux_host_stack_endpoint_instance_delete) |
| ![Konak yığını uç noktası sıfırlama simgesi](./media/user-guide/usbx-events/image201.png)    | **Konak yığını uç noktası sıfırlama** (ux_host_stack_endpoint_reset) |
| ![Konak yığını uç noktası aktarımı Iptal simgesi](./media/user-guide/usbx-events/image202.png)    | **Konak yığını uç noktası aktarımı iptal** (ux_host_stack_endpoint_transfer_abort) |
| ![Konak yığını konak denetleyicisi kayıt simgesi](./media/user-guide/usbx-events/image203.png)    | **Konak yığını konak denetleyicisi kaydı** *(ux_host_stack_hcd_register)* |
| ![Konak yığını başlatma simgesi](./media/user-guide/usbx-events/image204.png)    | **Konak yığını başlatma** *(ux_host_stack_initialize)* |
| ![Konak yığını arabirimi uç noktası al simgesi](./media/user-guide/usbx-events/image205.png)    | **Konak yığını arabirim uç noktası al** *(ux_host_stack_interface_endpoint_get)* |
| ![Konak yığını arabirim örneği oluşturma simgesi](./media/user-guide/usbx-events/image206.png)    | **Konak yığını arabirim örneği oluşturma** *(ux_host_stack_interface_instance_create)* |
| ![Konak yığını arabirim örneği silme simgesi](./media/user-guide/usbx-events/image207.png)    | **Konak yığını arabirim örneği silme** *(ux_host_stack_interface_instance_delete)* |
| ![Konak yığını arabirim kümesi simgesi](./media/user-guide/usbx-events/image208.png)    | **Konak yığını arabirim kümesi** *(ux_host_stack_interface_set)* |
| ![Konak yığın arabirimi ayarı seçme simgesi](./media/user-guide/usbx-events/image209.png)    | **Konak yığını arabirim ayarı seçimi** *(ux_host_stack_interface_setting_select)* |
| ![Konak yığını yeni yapılandırma Oluştur simgesi](./media/user-guide/usbx-events/image210.png)    | **Ana bilgisayar yığını yeni yapılandırma oluşturma** *(ux_host_stack_new_configuration_create)* |
| ![Konak yığını yeni cihaz Oluştur simgesi](./media/user-guide/usbx-events/image211.png)    | **Ana bilgisayar yığını yeni cihaz oluşturma** *(ux_host_stack_new_device_create)* |
| ![Ana bilgisayar yığını yeni uç nokta Oluştur simgesi](./media/user-guide/usbx-events/image212.png)    | **Ana bilgisayar yığını yeni uç nokta oluşturma** *(ux_host_stack_new_endpoint_create)* |
| ![Konak yığını kök hub 'ı değiştirme Işlemi simgesi](./media/user-guide/usbx-events/image213.png)    | **Konak yığını kök hub 'ı değişiklik işlemi** *(ux_host_stack_rh_change_process)* |
| ![Konak yığını kök hub cihazı ayıklama simgesi](./media/user-guide/usbx-events/image214.png)    | **Konak yığını kök hub cihazı ayıklama** *(ux_host_stack_rh_device_extraction)* |
| ![Konak yığını kök hub cihazı ekleme simgesi](./media/user-guide/usbx-events/image215.png)    | **Konak yığını kök hub cihazı ekleme** *(ux_host_stack_rh_device_insertion)* |
| ![Konak yığını aktarım Isteği simgesi](./media/user-guide/usbx-events/image216.png)    | **Ana bilgisayar yığını aktarım isteği** *(ux_host_stack_transfer_request)* |
| ![Konak yığını aktarım Isteği Iptali simgesi](./media/user-guide/usbx-events/image217.png)    | **Ana bilgisayar yığını aktarım Isteği iptali** *(ux_host_stack_transfer_request_abort)* |
| ![U S B X hata simgesi](./media/user-guide/usbx-events/image218.png)    | **USBX hatası** *(ux_error)* |

## <a name="event-descriptions"></a>Olay Açıklamaları

Aşağıdaki sayfalar, USBX Izleme olaylarını anlatmaktadır.

### <a name="device-class-cdc-activate"></a>Aygıt sınıfı CDC etkinleştirme 

#### <a name="ux_device_class_cdc_activate"></a>ux_device_class_cdc_activate

**Simge** ![ Cihaz sınıfı C D C etkinleştir simgesi](./media/user-guide/usbx-events/image1.png)

**Açıklama**

Bu olay bir USBX cihaz sınıfı CDC Activate olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-cdc-deactivate"></a>Device Class CDC devre dışı bırak 

#### <a name="ux_device_class_cdc_deactivate"></a>ux_device_class_cdc_deactivate

**Simge** ![ Cihaz sınıfı C D C devre dışı bırakma simgesi](./media/user-guide/usbx-events/image2.png)

**Açıklama**

Bu olay, bir USBX cihaz sınıfını CDC devre dışı bırakın.

Bilgi alanları 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-cdc-read"></a>Aygıt sınıfı CDC okuma 

#### <a name="ux_device_class_cdc_read"></a>ux_device_class_cdc_read

**Simge** ![ Cihaz sınıfı C D C okuma simgesi](./media/user-guide/usbx-events/image3.png)

**Açıklama**

Bu olay bir USBX cihaz sınıfı CDC okuma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: veri işaretçisi.
- Bilgi alanı 3: Istenen uzunluk.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-cdc-write"></a>Aygıt sınıfı CDC yazma 

#### <a name="ux_device_class_cdc_write"></a>ux_device_class_cdc_write

**Simge** ![ Cihaz sınıfı C D C yazma simgesi](./media/user-guide/usbx-events/image4.png)

**Açıklama**

Bu olay bir USBX cihaz sınıfı CDC yazma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: veri işaretçisi.
- Bilgi alanı 3: Istenen uzunluk.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-dpump-activate"></a>Cihaz sınıfı Dpump etkinleştir 

#### <a name="ux_device_class_dpump_activate"></a>ux_device_class_dpump_activate

**Simge** ![ Device Class Dpump etkinleştir simgesi](./media/user-guide/usbx-events/image5.png)

**Açıklama**

Bu olay bir USBX cihaz sınıfı Dpump Activate olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-dpump-deactivate"></a>Cihaz sınıfı Dpump devre dışı bırakma 

#### <a name="ux_device_class_dpump_deactivate"></a>ux_device_class_dpump_deactivate

**Simge** ![ Cihaz sınıfı Dpump devre dışı bırakma simgesi](./media/user-guide/usbx-events/image6.png)

**Açıklama**

Bu olay bir USBX cihaz sınıfı Dpump Deactivate olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-dpump-read"></a>Cihaz sınıfı Dpump okuma 

#### <a name="ux_device_class_dpump_read"></a>ux_device_class_dpump_read

**Simge** ![ Cihaz sınıfı Dpump okuma simgesi](./media/user-guide/usbx-events/image7.png)

**Açıklama**

Bu olay, bir USBX cihaz sınıfı Dpump okuma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: arabellek.
- Bilgi alanı 3: Istenen uzunluk.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-dpump-write"></a>Cihaz sınıfı Dpump yazma 

#### <a name="ux_device_class_dpump_write"></a>ux_device_class_dpump_write

**Simge** ![ Device Class Dpump yazma simgesi](./media/user-guide/usbx-events/image8.png)

**Açıklama**

Bu olay, bir USBX cihaz sınıfı Dpump yazma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: veri işaretçisi.
- Bilgi alanı 3: Istenen uzunluk.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-hid-activate"></a>Cihaz sınıfı HID etkinleştirme 

#### <a name="ux_device_class_hid_activate"></a>ux_device_class_hid_activate

**Simge** ![ Device Class HID etkinleştirme simgesi](./media/user-guide/usbx-events/image9.png)

**Açıklama**

Bu olay bir USBX Device Class HID Activate olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-hid-deactivate"></a>Cihaz sınıfı HID devre dışı 

#### <a name="ux_device_class_hid_deactivate"></a>ux_device_class_hid_deactivate

**Simge** ![ Cihaz sınıfı HID devre dışı bırakma simgesi](./media/user-guide/usbx-events/image10.png)

**Açıklama**

Bu olay bir USBX cihaz sınıfı HID devre dışı bırakma olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-hid-descriptor-send"></a>Cihaz sınıfı HID tanımlayıcısı gönderme 

#### <a name="ux_device_class_hid_descritpor_send"></a>ux_device_class_hid_descritpor_send

**Simge** ![ Cihaz sınıfı HID tanımlayıcısı gönderme simgesi](./media/user-guide/usbx-events/image11.png)

**Açıklama**

Bu olay bir USBX cihaz sınıfı HID tanımlayıcısı gönderme olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: tanımlayıcı türü.
- Bilgi alanı 3: Istek dizini.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-hid-event-get"></a>Cihaz sınıfı HID olayı Get 

#### <a name="ux_device_class_hid_event_get"></a>ux_device_class_hid_event_get

**Simge** ![ Cihaz sınıfı HID olayı al simgesi](./media/user-guide/usbx-events/image12.png)

**Açıklama**

Bu olay bir USBX cihaz sınıfı HID olay Get olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-hid-event-set"></a>Cihaz sınıfı HID olay kümesi 

#### <a name="ux_device_class_hid_event_set"></a>ux_device_class_hid_event_set

**Simge** ![ Cihaz sınıfı HID olay kümesi simgesi](./media/user-guide/usbx-events/image13.png)

**Açıklama**

Bu olay bir USBX cihaz sınıfı HID olay kümesini temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-hid-report-get"></a>Cihaz sınıfı HID raporu al 

#### <a name="ux_device_class_hid_report_get"></a>ux_device_class_hid_report_get

**Simge** ![ Cihaz sınıfı HID raporu al simgesi](./media/user-guide/usbx-events/image14.png)

**Açıklama**

Bu olay bir USBX Device Class HID rapor Get olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: tanımlayıcı türü.
- Bilgi alanı 3: Istek dizini.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-hid-report-set"></a>Cihaz sınıfı HID rapor kümesi 

#### <a name="ux_device_class_hid_report_set"></a>ux_device_class_hid_report_set

**Simge** ![ Cihaz sınıfı HID rapor kümesi simgesi](./media/user-guide/usbx-events/image15.png)

**Açıklama**

Bu olay bir USBX cihaz sınıfı HID rapor kümesi olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: tanımlayıcı türü.
- Bilgi alanı 3: Istek dizini.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-pima-activate"></a>Cihaz sınıfı Pima etkinleştir

#### <a name="ux_device_class_pima_activate"></a>ux_device_class_pima_activate

**Simge** ![ Cihaz sınıfı Pima etkinleştirme simgesi](./media/user-guide/usbx-events/image16.png)

**Açıklama**

Bu olay bir USBX Device Class Pima Activate olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-pima-deactivate"></a>Cihaz sınıfı Pima devre dışı 

#### <a name="ux_device_class_pima_deactivate"></a>ux_device_class_pima_deactivate

**Simge** ![ Cihaz sınıfı Pima devre dışı bırakma simgesi](./media/user-guide/usbx-events/image17.png)

**Açıklama**

Bu olay bir USBX Device Class Pima etkinliğini kaldırma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-pima-device-info-send"></a>Cihaz sınıfı Pima cihaz bilgileri gönderme 

#### <a name="ux_device_class_pima_device_info_send"></a>ux_device_class_pima_device_info_send

**Simge** ![ Cihaz sınıfı Pima cihaz bilgileri gönderme simgesi](./media/user-guide/usbx-events/image18.png)

**Açıklama**

Bu olay bir USBX cihaz sınıfı Pima cihaz bilgileri gönderme olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.

### <a name="device-class-pima-event-get"></a>Cihaz sınıfı Pima olayı Get 

#### <a name="ux_device_class_pima_event_get"></a>ux_device_class_pima_event_get

**Simge** ![ Device Class Pima olayı al simgesi](./media/user-guide/usbx-events/image19.png)

**Açıklama**

Bu olay bir USBX Device Class Pima olayı Get olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: Pima olayı.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-pima-event-set"></a>Device Class Pima olay kümesi 

#### <a name="ux_device_class_pima_event_set"></a>ux_device_class_pima_event_set

**Simge** ![ Cihaz sınıfı Pima olayı kümesi simgesi](./media/user-guide/usbx-events/image20.png)

**Açıklama**

Bu olay bir USBX cihaz sınıfı Pima olay kümesi olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: Pima olayı.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-pima-object-add"></a>Cihaz sınıfı Pima nesnesi ekleme 

#### <a name="ux_device_class_pima_object_add"></a>ux_device_class_pima_object_add

**Simge** ![ Cihaz sınıfı Pima nesnesi ekleme simgesi](./media/user-guide/usbx-events/image21.png)

**Açıklama**

Bu olay bir USBX Device Class Pima nesnesi Add olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: nesne tanıtıcısı.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-pima-object-data-get"></a>Cihaz sınıfı Pima nesnesi veri al 

#### <a name="ux_device_class_pima_object_data_get"></a>ux_device_class_pima_object_data_get

**Simge** ![ Aygıt sınıfı Pima nesnesi verileri al simgesi](./media/user-guide/usbx-events/image22.png)

**Açıklama**

Bu olay bir USBX cihaz sınıfı Pima nesne verileri al olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: nesne tanıtıcısı.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-pima-object-data-send"></a>Cihaz sınıfı Pima nesnesi verileri gönderme 

#### <a name="ux_device_class_pima_object_data_send"></a>ux_device_class_pima_object_data_send

**Simge** ![ Cihaz sınıfı Pima nesnesi verileri gönderme simgesi](./media/user-guide/usbx-events/image23.png)

**Açıklama**

Bu olay bir USBX cihaz sınıfı Pima nesnesi veri gönderme olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: nesne tanıtıcısı.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-pima-object-delete"></a>Device Class Pima nesnesi silme 

#### <a name="ux_device_class_pima_object_delete"></a>ux_device_class_pima_object_delete

**Simge** ![ Device Class Pima nesnesi silme simgesi](./media/user-guide/usbx-events/image24.png)

**Açıklama**

Bu olay bir USBX Device Class Pima nesnesi silme olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: nesne tanıtıcısı.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-pima-object-handles-send"></a>Cihaz sınıfı Pima nesnesi gönderme tutamaçları 

#### <a name="ux_device_class_pima_object_handles_send"></a>ux_device_class_pima_object_handles_send

**Simge** ![ Cihaz sınıfı Pima nesnesi gönderme simgesini Işler](./media/user-guide/usbx-events/image25.png)

**Açıklama**

Bu olay, bir USBX cihaz sınıfı Pima nesnesi gönderme olayını Işler.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: depolama KIMLIĞI.
- Bilgi alanı 3: nesne biçimi kodu.
- Bilgi alanı 4: nesne ilişkilendirmesi.

### <a name="device-class-pima-object-info-get"></a>Device Class Pima nesne bilgisi al 

#### <a name="ux_device_class_pima_object_info_send"></a>ux_device_class_pima_object_info_send

**Simge** ![ Device Class Pima nesne bilgisi al simgesi](./media/user-guide/usbx-events/image26.png)

**Açıklama**

Bu olay bir USBX Device Class Pima nesne bilgileri al olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: nesne tanıtıcısı.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-pima-object-info-send"></a>Device Class Pima nesne bilgileri gönderme 

#### <a name="ux_device_class_pima_object_info_send"></a>ux_device_class_pima_object_info_send

**Simge** ![ Device Class Pima nesne bilgileri gönderme simgesi](./media/user-guide/usbx-events/image27.png)

**Açıklama**

Bu olay bir USBX Device Class Pima nesne bilgileri gönderme olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-pima-objects-number-send"></a>Cihaz sınıfı Pima nesneleri sayı gönderme 

#### <a name="ux_device_class_pima_object_number_send"></a>ux_device_class_pima_object_number_send

**Simge** ![ Cihaz sınıfı Pima nesneleri numara Gönder simgesi](./media/user-guide/usbx-events/image28.png)

**Açıklama**

Bu olay bir USBX cihaz sınıfı Pima nesne numarası gönderme olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: depolama KIMLIĞI.
- Bilgi alanı 3: nesne biçimi kodu.
- Bilgi alanı 4: nesne ilişkilendir.

### <a name="device-class-pima-partial-object-data-get"></a>Device Class Pima kısmi nesne verileri al

#### <a name="ux_device_class_pima_partial_object_data_get"></a>ux_device_class_pima_partial_object_data_get

**Simge** ![ Device Class Pima kısmi nesne verileri al simgesi](./media/user-guide/usbx-events/image29.png)

**Açıklama**

Bu olay bir USBX cihaz sınıfı Pima kısmi nesne verileri al olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: nesne tanıtıcısı.
- Bilgi alanı 3: istenen fark.
- Bilgi alanı 4: Uzunluk istendi.

### <a name="device-class-pima-response-send"></a>Cihaz sınıfı Pima yanıtı gönderme 

#### <a name="ux_device_class_pima_response_send"></a>ux_device_class_pima_response_send

**Simge** ![ Cihaz sınıfı Pima yanıtı gönderme simgesi](./media/user-guide/usbx-events/image30.png)

**Açıklama**

Bu olay bir USBX Device Class Pima yanıtı gönderme olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: yanıt kodu.
- Bilgi alanı 3: sayı parametresi.
- Bilgi alanı 4: Pima parametresi 1.

### <a name="device-class-pima-storage-id-send"></a>Cihaz sınıfı Pima depolama kimliği gönderme 

#### <a name="ux_device_class_pima_storage_id_send"></a>ux_device_class_pima_storage_id_send

**Simge** ![ Cihaz sınıfı Pima depolama kimliği gönderme simgesi](./media/user-guide/usbx-events/image31.png)

**Açıklama**

Bu olay bir USBX cihaz sınıfı Pima depolama kimliği gönderme olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-pima-storage-info-send"></a>Cihaz sınıfı Pima depolama bilgileri gönderme 

#### <a name="ux_device_class_pima_storage_info_send"></a>ux_device_class_pima_storage_info_send

**Simge** ![ Cihaz sınıfı Pima depolama bilgileri gönderme simgesi](./media/user-guide/usbx-events/image32.png)

**Açıklama**

Bu olay bir USBX cihaz sınıfı Pima depolama bilgileri gönderme olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-rndis-activate"></a>Cihaz sınıfı rndis etkinleştir 

#### <a name="ux_device_class_rndis_activate"></a>ux_device_class_rndis_activate

**Simge** ![ Cihaz sınıfı rndis etkinleştir simgesi](./media/user-guide/usbx-events/image33.png)

**Açıklama**

Bu olay bir USBX cihaz sınıfı rndis Activate olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-rndis-deactivate"></a>Cihaz sınıfı rndis devre dışı bırak 

#### <a name="ux_device_class_rndis_deactivate"></a>ux_device_class_rndis_deactivate

**Simge** ![ Cihaz sınıfı rndis devre dışı bırakma simgesi](./media/user-guide/usbx-events/image34.png)

**Açıklama**

Bu olay bir USBX cihaz sınıfı rndis devre dışı bırakma olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-rndis-message-keep-alive"></a>Cihaz sınıfı rndis Ileti canlı tut 

#### <a name="ux_device_class_rndis_msg_keep_alive"></a>ux_device_class_rndis_msg_keep_alive

**Simge** ![ Cihaz sınıfı rndis Ileti canlı tut simgesi](./media/user-guide/usbx-events/image35.png)

**Açıklama**

Bu olay bir USBX cihaz sınıfını rndis Iletisi etkin tut olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-rndis-message-query"></a>Cihaz sınıfı rndis Ileti sorgusu 

#### <a name="ux_device_class_rndis_msg_keep_query"></a>ux_device_class_rndis_msg_keep_query

**Simge** ![ Cihaz sınıfı rndis Iletisi sorgu simgesi](./media/user-guide/usbx-events/image36.png)

**Açıklama**

Bu olay bir USBX cihaz sınıfı rndis Iletisi sorgu olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: rndis OID.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-rndis-message-reset"></a>Cihaz sınıfı rndis Ileti sıfırlama 

#### <a name="ux_device_class_rndis_msg_reset"></a>ux_device_class_rndis_msg_reset

**Simge** ![ Cihaz sınıfı rndis Ileti sıfırlama simgesi](./media/user-guide/usbx-events/image37.png)

**Açıklama**

Bu olay bir USBX cihaz sınıfı rndis Ileti sıfırlama olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.

### <a name="device-class-rndis-message-set"></a>Cihaz sınıfı rndis Ileti kümesi 

#### <a name="ux_device_class_rndis_msg_set"></a>ux_device_class_rndis_msg_set

**Simge** ![ Cihaz sınıfı rndis Ileti kümesi simgesi](./media/user-guide/usbx-events/image38.png)

**Açıklama**

Bu olay bir USBX cihaz sınıfı rndis Ileti kümesi olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: rndis OID.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-rndis-packet-receive"></a>Cihaz sınıfı rndis paket alma 

#### <a name="ux_device_class_rndis_packet_receive"></a>ux_device_class_rndis_packet_receive

**Simge** ![ Cihaz sınıfı rndis paket alma simgesi](./media/user-guide/usbx-events/image39.png)

**Açıklama**

Bu olay bir USBX cihaz sınıfı rndis paket alma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-rndis-packet-transmit"></a>Cihaz sınıfı rndis paket Iletimi 

#### <a name="ux_device_class_rndis_packet_transmit"></a>ux_device_class_rndis_packet_transmit

**Simge** ![ Cihaz sınıfı rndis paket Iletme simgesi](./media/user-guide/usbx-events/image40.png)

**Açıklama**

Bu olay bir USBX cihaz sınıfı rndis paket Iletme olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-storage-activate"></a>Cihaz sınıfı depolamayı etkinleştirme 

#### <a name="ux_device_class_storage_activate"></a>ux_device_class_storage_activate

**Simge** ![ Cihaz sınıfı depolama etkinleştirme simgesi](./media/user-guide/usbx-events/image41.png)

**Açıklama**

Bu olay bir USBX cihaz sınıfı depolama etkinleştirme olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-storage-deactivate"></a>Cihaz sınıfı depolamayı devre dışı bırakma 

#### <a name="ux_device_class_storage_deactivate"></a>ux_device_class_storage_deactivate

**Simge** ![ Cihaz sınıfı depolamayı devre dışı bırakma simgesi](./media/user-guide/usbx-events/image42.png)

**Açıklama**

Bu olay bir USBX cihaz sınıfı depolaması devre dışı bırakma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-storage-format"></a>Cihaz sınıfı depolama biçimi 

#### <a name="ux_device_class_storage_format"></a>ux_device_class_storage_format

**Simge** ![ Cihaz sınıfı depolama biçimi simgesi](./media/user-guide/usbx-events/image43.png)

**Açıklama**

Bu olay bir USBX cihaz sınıfı depolama biçimi olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: LUN.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-storage-inquiry"></a>Cihaz sınıfı depolama sorgusu 

#### <a name="ux_device_class_storage_inquiry"></a>ux_device_class_storage_inquiry

**Simge** ![ Cihaz sınıfı depolama sorgulama simgesi](./media/user-guide/usbx-events/image44.png)

**Açıklama**

Bu olay bir USBX cihaz sınıfı depolama sorgulama olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: LUN.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-storage-mode-select"></a>Cihaz sınıfı depolama modu seçme

#### <a name="ux_device_class_storage_mode_select"></a>ux_device_class_storage_mode_select

**Simge** ![ Cihaz sınıfı depolama modu seçme simgesi](./media/user-guide/usbx-events/image45.png)

**Açıklama**

Bu olay bir USBX cihaz sınıfı depolama modu seçme olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: LUN.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-storage-mode-sense"></a>Cihaz sınıfı depolama modu algılama 

#### <a name="ux_device_class_storage_mode_sense"></a>ux_device_class_storage_mode_sense

**Simge** ![ Cihaz sınıfı depolama modu algılama simgesi](./media/user-guide/usbx-events/image46.png)

**Açıklama**

Bu olay, bir USBX cihaz sınıfı depolama modu Sense olayını temsil eder.

Bilgi alanları 

- NFO alanı 1: sınıf örneği.
- Bilgi alanı 2: LUN.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-storage-prevent-allow-media-removal"></a>Cihaz sınıfı depolaması medya kaldırılmasına Izin vermeyi engelliyor 

#### <a name="ux_device_class_storage_prevent_allow_media_removal"></a>ux_device_class_storage_prevent_allow_media_removal

**Simge** ![ Cihaz sınıfı depolaması medya kaldırma simgesine Izin vermeyi engelliyor](./media/user-guide/usbx-events/image47.png)

**Açıklama**

Bu olay bir USBX cihaz sınıfı depolaması, medya kaldırma olayına Izin vermeyi engelliyor.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: LUN.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-storage-read"></a>Cihaz sınıfı depolama okuma 

#### <a name="ux_device_class_storage_read"></a>ux_device_class_storage_read

**Simge** ![ Cihaz sınıfı depolama okuma simgesi](./media/user-guide/usbx-events/image48.png)

**Açıklama**

Bu olay bir USBX cihaz sınıfı depolama okuma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: LUN.
- Bilgi alanı 3: sektör.
- Bilgi alanı 4: sayı kesimleri.

### <a name="device-class-storage-read-capacity"></a>Cihaz sınıfı depolama okuma kapasitesi 

#### <a name="ux_device_class_storage_read_capacity"></a>ux_device_class_storage_read_capacity

**Simge** ![ Cihaz sınıfı depolama okuma kapasitesi simgesi](./media/user-guide/usbx-events/image49.png)

**Açıklama**

Bu olay bir USBX cihaz sınıfı depolama okuma kapasitesi olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: LUN.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-storage-read-format-capacity"></a>Cihaz sınıfı depolama okuma biçimi kapasitesi 

#### <a name="ux_device_class_storage_read_format_capacity"></a>ux_device_class_storage_read_format_capacity

**Simge** ![ Cihaz sınıfı depolama okuma biçimi kapasitesi simgesi](./media/user-guide/usbx-events/image50.png)

**Açıklama**

Bu olay bir USBX cihaz sınıfı depolama okuma biçimi kapasitesi olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: LUN.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-storage-read-toc"></a>Device Class depolaması TOC okuma 

#### <a name="ux_device_class_storage_read_toc"></a>ux_device_class_storage_read_toc

**Simge** ![ Device Class depolama okuma TOC simgesi](./media/user-guide/usbx-events/image51.png)

**Açıklama**

Bu olay, bir USBX cihaz sınıfı depolama okuma TOC olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: LUN.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-storage-request-sense"></a>Cihaz sınıfı depolama Istek algılaması 

#### <a name="ux_device_class_storage_request_sense"></a>ux_device_class_storage_request_sense

**Simge** ![ Cihaz sınıfı depolama Isteği algılama simgesi](./media/user-guide/usbx-events/image52.png)

**Açıklama**

Bu olay bir USBX cihaz sınıfı depolama Istek algılama olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: LUN.
- Bilgi alanı 3: Sense anahtarı.
- Bilgi alanı 4: kod.

### <a name="device-class-storage-start-stop"></a>Cihaz sınıfı depolama başlangıç durağı 

#### <a name="ux_device_class_storage_start_stop"></a>ux_device_class_storage_start_stop

**Simge** ![ Cihaz sınıfı depolama başlatma durdurma simgesi](./media/user-guide/usbx-events/image53.png)

**Açıklama**

Bu olay bir USBX cihaz sınıfı depolama başlatma durdurma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: LUN.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-storage-test-ready"></a>Cihaz sınıfı depolama sınaması hazırlanıyor 

#### <a name="ux_device_class_storage_test_ready"></a>ux_device_class_storage_test_ready

**Simge** ![ Cihaz sınıfı depolama sınaması hazırlanıyor simgesi](./media/user-guide/usbx-events/image54.png)

**Açıklama**

Bu olay, bir USBX cihaz sınıfı depolama testinin Ready olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: LUN.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-storage-verify"></a>Cihaz sınıfı depolama doğrulaması 

#### <a name="ux_device_class_storage_verify"></a>ux_device_class_storage_verify

**Simge** ![ Cihaz sınıfı depolama doğrulama simgesi](./media/user-guide/usbx-events/image55.png)

**Açıklama**

Bu olay bir USBX cihaz sınıfı depolama doğrulama olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: LUN.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-storage-write"></a>Cihaz sınıfı depolama yazma 

#### <a name="ux_device_class_storage_write"></a>ux_device_class_storage_write

**Simge** ![ Cihaz sınıfı depolama yazma simgesi](./media/user-guide/usbx-events/image56.png)

**Açıklama**

Bu olay bir USBX cihaz sınıfı depolama yazma olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: LUN.
- Bilgi alanı 3: sektör.
- Bilgi alanı 4: sayı kesimleri.

### <a name="device-stack-alternate-setting-get"></a>Cihaz yığını alternatif ayarı al 

#### <a name="ux_device_class_alternate_setting_get"></a>ux_device_class_alternate_setting_get

**Simge** ![ Cihaz yığını alternatif ayarı al simgesi](./media/user-guide/usbx-events/image57.png)

**Açıklama**

Bu olay bir USBX cihaz yığını alternatif ayarı al olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: arabirim değeri.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-stack-alternate-setting-set"></a>Cihaz yığını alternatif ayarı kümesi 

#### <a name="ux_device_class_alternate_setting_set"></a>ux_device_class_alternate_setting_set

**Simge** ![ Cihaz yığını alternatif ayarı kümesi simgesi](./media/user-guide/usbx-events/image58.png)

**Açıklama**

Bu olay bir USBX cihaz yığını alternatif ayar kümesi olayını temsil eder.

**Bilgi alanları**
- Bilgi alanı 1: arabirim değeri.
- Bilgi alanı 2: alternatif ayar değeri.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-stack-class-register"></a>Cihaz yığını sınıf kaydı 

#### <a name="ux_device_stack_class_register"></a>ux_device_stack_class_register

**Simge** ![ Cihaz yığını sınıfı kayıt simgesi](./media/user-guide/usbx-events/image59.png)

**Açıklama**

Bu olay bir USBX cihaz yığını sınıf kaydı olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf adı.
- Bilgi alanı 2: arabirim numarası.
- Bilgi alanı 3: parametre.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-stack-clear-feature"></a>Cihaz yığını temizleme özelliği 

#### <a name="ux_device_stack_clear_feature"></a>ux_device_stack_clear_feature

**Simge** ![ Cihaz yığını temiz Özellik simgesi](./media/user-guide/usbx-events/image60.png)

**Açıklama**

Bu olay bir USBX cihaz yığını temiz Özellik olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: Istek türü.
- Bilgi alanı 2: Istek değeri. Bilgi alanı 3: Istek dizini.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-stack-configuration-get"></a>Cihaz yığını yapılandırmasını al 

#### <a name="ux_device_stack_configuration_get-t"></a>ux_device_stack_configuration_get t

**Simge** ![ Cihaz yığını yapılandırması Get simgesi](./media/user-guide/usbx-events/image61.png)

**Açıklama**

Bu olay bir USBX cihaz yığını yapılandırma Get olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: yapılandırma değeri.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-stack-configuration-set"></a>Cihaz yığını yapılandırma kümesi 

#### <a name="ux_device_stack_configuration_set"></a>ux_device_stack_configuration_set

**Simge** ![ Cihaz yığını yapılandırma kümesi simgesi](./media/user-guide/usbx-events/image62.png)

**Açıklama**

Bu olay bir USBX cihaz yığını yapılandırma kümesi olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: yapılandırma değeri.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-stack-connect"></a>Cihaz yığını bağlantısı 

#### <a name="ux_device_stack_connect"></a>ux_device_stack_connect

**Simge** ![ Cihaz yığını bağlantı simgesi](./media/user-guide/usbx-events/image63.png)

**Açıklama**

Bu olay bir USBX cihaz yığını tanımlayıcı gönderme olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: kullanılmıyor.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-stack-descriptor-send"></a>Cihaz yığını tanımlayıcısı gönderme 

#### <a name="ux_device_stack_descriptor_send"></a>ux_device_stack_descriptor_send

**Simge** ![ Cihaz yığını tanımlayıcısı gönderme simgesi](./media/user-guide/usbx-events/image64.png)

**Açıklama**

Bu olay bir USBX cihaz yığını tanımlayıcı gönderme olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: tanımlayıcı türü.
- Bilgi alanı 2: Istek dizini.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-stack-disconnect"></a>Cihaz yığını bağlantısını kes 

#### <a name="ux_device_stack_disconnect"></a>ux_device_stack_disconnect

**Simge** ![ Cihaz yığını bağlantı kesme simgesi](./media/user-guide/usbx-events/image65.png)

**Açıklama**

Bu olay bir USBX cihaz yığını bağlantı kesme olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: cihaz.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-stack-endpoint-stall"></a>Cihaz yığını uç noktası kabini 

#### <a name="ux_device_stack_endpoint_stall"></a>ux_device_stack_endpoint_stall

**Simge** ![ Cihaz yığını uç noktası kabin simgesi](./media/user-guide/usbx-events/image66.png)

**Açıklama**

Bu olay bir USBX cihaz yığını uç nokta kabini olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: uç nokta.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-stack-get-status"></a>Cihaz yığını Get durumu 

#### <a name="ux_device_stack_get_status"></a>ux_device_stack_get_status

**Simge** ![ Cihaz yığını durum Al simgesi](./media/user-guide/usbx-events/image67.png)

**Açıklama**

Bu olay bir USBX cihaz yığını al durum olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: kullanılmıyor.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-stack-host-wakeup"></a>Cihaz yığını ana bilgisayarı uyandırma 

#### <a name="ux_device_stack_host_wakeup"></a>ux_device_stack_host_wakeup

**Simge** ![ Cihaz yığını ana bilgisayarı uyandırma simgesi](./media/user-guide/usbx-events/image68.png)

**Açıklama**

Bu olay bir USBX cihaz yığını ana bilgisayarı uyandırma olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: kullanılmıyor.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-stack-initialize"></a>Cihaz yığını başlatma 

#### <a name="ux_device_stack_initialize"></a>ux_device_stack_initialize

**Simge** ![ Cihaz yığını başlatma simgesi](./media/user-guide/usbx-events/image69.png)

**Açıklama**

Bu olay bir USBX cihaz yığını başlatma olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: kullanılmıyor.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-stack-interface-delete"></a>Cihaz yığını arabirimini silme 

#### <a name="ux_device_stack_interface_delete"></a>ux_device_stack_interface_delete

**Simge** ![ Cihaz yığını arabirimi silme simgesi](./media/user-guide/usbx-events/image70.png)

**Açıklama**

Bu olay bir USBX cihaz yığını arabirimi silme olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: arabirim.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-stack-interface-get"></a>Cihaz yığını arabirimi al 

#### <a name="ux_device_stack_interface_get"></a>ux_device_stack_interface_get

**Simge** ![ Cihaz yığını arabirimi al simgesi](./media/user-guide/usbx-events/image71.png)

**Açıklama**

Bu olay bir USBX cihaz yığını arabirimi Get olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: arabirim değeri.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-stack-interface-set"></a>Cihaz yığını arabirim kümesi 

#### <a name="ux_device_stack_interface_set"></a>ux_device_stack_interface_set

**Simge** ![ Cihaz yığını arabirim kümesi simgesi](./media/user-guide/usbx-events/image72.png)

**Açıklama**

Bu olay bir USBX cihaz yığını arabirim kümesi olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: Istek değeri. Bilgi alanı 2: Istek dizini.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-stack-set-feature"></a>Cihaz yığını kümesi özelliği 

#### <a name="ux_device_stack_set_feature"></a>ux_device_stack_set_feature

**Simge** ![ Cihaz yığını kümesi özellik simgesi](./media/user-guide/usbx-events/image73.png)

**Açıklama**

Bu olay bir USBX cihaz yığını kümesi özelliği olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: Istek değeri. Bilgi alanı 2: Istek dizini.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-stack-transfer-abort"></a>Cihaz yığını aktarımı Iptali 

#### <a name="ux_device_stack_transfer_abort"></a>ux_device_stack_transfer_abort

**Simge** ![ Cihaz yığını aktarım Iptali simgesi](./media/user-guide/usbx-events/image74.png)

**Açıklama**

Bu olay bir USBX cihaz yığını aktarımı Iptali olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: aktarım isteği.
- Bilgi alanı 2: tamamlanma kodu.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-stack-transfer-all-request-abort"></a>Cihaz yığın aktarımı tüm Istek Iptali 

#### <a name="ux_device_stack_transfer_all_request_abort"></a>ux_device_stack_transfer_all_request_abort

**Simge** ![ Cihaz yığını tüm Isteği Iptal et simgesi](./media/user-guide/usbx-events/image75.png)

**Açıklama**

Bu olay, tüm Istek Iptali olayını aktar bir USBX cihaz yığınını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: uç nokta.
- Bilgi alanı 2: tamamlanma kodu.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-stack-transfer-request"></a>Cihaz yığını aktarım Isteği 

#### <a name="ux_device_stack_transfer_request"></a>ux_device_stack_transfer_request

**Simge** ![ Cihaz yığını aktarım Isteği simgesi](./media/user-guide/usbx-events/image76.png)

**Açıklama**

Bu olay bir USBX cihaz yığını aktarım Isteği olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: aktarım isteği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-asix-activate"></a>Ana bilgisayar sınıfı Aaltıetkinleştir 

#### <a name="ux_host_class_asix_activate"></a>ux_host_class_asix_activate

**Simge** ![ Ana bilgisayar sınıfı ASIX etkinleştir simgesi](./media/user-guide/usbx-events/image77.png)

**Açıklama**

Bu olay, bir USBX konak sınıfının Aaltıyı Etkinleştirünü temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-asix-deactivate"></a>Ana makine sınıfı ASIX devre dışı 

#### <a name="ux_host_class_asix_deactivate"></a>ux_host_class_asix_deactivate

**Simge** ![ Ana makine sınıfı ASIX devre dışı simgesi](./media/user-guide/usbx-events/image78.png)

**Açıklama**

Bu olay bir USBX konak sınıfının bir adet devre dışı bırakma olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-asix-interrupt-notification"></a>Ana bilgisayar sınıfı asix kesme bildirimi 

#### <a name="ux_host_class_asix_interrupt_notification"></a>ux_host_class_asix_interrupt_notification

**Simge** ![ Ana bilgisayar sınıfı Aaltıkesme bildirimi simgesi](./media/user-guide/usbx-events/image79.png)

**Açıklama**

Bu olay bir USBX konak sınıfının asix kesme bildirimi olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-asix-read"></a>Ana bilgisayar sınıfı Aaltıokuma 

#### <a name="ux_host_class_asix_read"></a>ux_host_class_asix_read

**Simge** ![ Ana bilgisayar sınıfı Aaltıoku simgesi](./media/user-guide/usbx-events/image80.png)

**Açıklama**

Bu olay bir USBX konak sınıfının Aaltıoku olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: veri işaretçisi.
- Bilgi alanı 3: Istenen uzunluk.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-asix-write"></a>Ana bilgisayar sınıfı Aaltıyaz 

#### <a name="ux_host_class_asix_write"></a>ux_host_class_asix_write

**Simge** ![ Ana bilgisayar sınıfı Aaltıyaz simgesi](./media/user-guide/usbx-events/image81.png)

**Açıklama**

Bu olay, bir USBX ana bilgisayar sınıfının altı adet yazma olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: veri işaretçisi.
- Bilgi alanı 3: Istenen uzunluk.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-audio-activate"></a>Konak sınıfı ses etkinleştirme 

#### <a name="ux_host_class_audio_activate"></a>ux_host_class_audio_activate

**Simge** ![ Konak sınıfı ses etkinleştirme simgesi](./media/user-guide/usbx-events/image82.png)

**Açıklama**

Bu olay bir USBX konak sınıfı ses etkinleştirme olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-audio-control-value-get"></a>Konak sınıfı ses denetimi değeri Al 

#### <a name="ux_host_class_audio_control_value_get"></a>ux_host_class_audio_control_value_get

**Simge** ![ Konak sınıfı ses denetimi değeri Al simgesi](./media/user-guide/usbx-events/image83.png)

**Açıklama**

Bu olay bir USBX konak sınıfı ses denetim değeri Al olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-audio-control-value-set"></a>Konak sınıfı ses denetimi değer kümesi 

#### <a name="ux_host_class_audio_control_value_set"></a>ux_host_class_audio_control_value_set

**Simge** ![ Konak sınıfı ses denetimi değer kümesi simgesi](./media/user-guide/usbx-events/image84.png)

**Açıklama**

Bu olay, bir iç NetX g/ç sürücüsü ertelenmiş işleme olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: ses denetimi.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-audio-deactivate"></a>Konak sınıfı ses etkinliğini kaldırma 

#### <a name="ux_host_class_audio_deactivate"></a>ux_host_class_audio_deactivate

**Simge** ![ Konak sınıfı ses devre dışı bırakma simgesi](./media/user-guide/usbx-events/image85.png)

**Açıklama**

Bu olay bir USBX konak sınıfı sesi devre dışı bırakma olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-audio-read"></a>Konak sınıfı ses okuma 

#### <a name="ux_host_class_audio_read"></a>ux_host_class_audio_read

**Simge** ![ Konak sınıfı ses okuma simgesi](./media/user-guide/usbx-events/image86.png)

**Açıklama**

Bu olay bir USBX konak sınıfı ses okuma olayını temsil eder.

- Bilgi alanları 
- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: veri işaretçisi.
- Bilgi alanı 3: Istenen uzunluk.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-audio-streaming-sampling-get"></a>Konak sınıfı ses akışı örneklemesi alma 

#### <a name="ux_host_class_audio_streaming_sampling_get"></a>ux_host_class_audio_streaming_sampling_get

**Simge** ![ Konak sınıfı ses akışı örneklemesi alma simgesi](./media/user-guide/usbx-events/image87.png)

**Açıklama**

Bu olay bir USBX konak sınıfı ses akışı örnekleme Get olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-audio-streaming-sampling-set"></a>Konak sınıfı ses akışı örnekleme kümesi 

#### <a name="ux_host_class_audio_streaming_sampling_set"></a>ux_host_class_audio_streaming_sampling_set

**Simge** ![ Konak sınıfı ses akışı örnekleme kümesi simgesi](./media/user-guide/usbx-events/image88.png)

**Açıklama**

Bu olay bir USBX konak sınıfı ses akışı örnekleme kümesi olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: ses örnekleme.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-audio-write"></a>Konak sınıfı ses yazma 

#### <a name="ux_host_class_audio_write"></a>ux_host_class_audio_write

**Simge** ![ Konak sınıfı ses yazma simgesi](./media/user-guide/usbx-events/image89.png)

**Açıklama**

Bu olay bir USBX konak sınıfı ses yazma olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: veri işaretçisi.
- Bilgi alanı 3: Istenen uzunluk.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-cdc-acm-activate"></a>Ana bilgisayar sınıfı CDC ACM Activate 

#### <a name="ux_host_class_cdc_acm_activate"></a>ux_host_class_cdc_acm_activate

**Simge** ![ Ana bilgisayar sınıfı C D C A C M etkinleştirme simgesi](./media/user-guide/usbx-events/image90.png)

**Açıklama**

Bu olay bir USBX konak sınıfı CDC ACM Activate olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-cdc-acm-deactivate"></a>Ana bilgisayar sınıfı CDC ACM Deactivate 

#### <a name="ux_host_class_cdc_acm_deactivate"></a>ux_host_class_cdc_acm_deactivate

**Simge** ![ Ana bilgisayar sınıfı C D C A C M devre dışı bırakma simgesi](./media/user-guide/usbx-events/image91.png)

**Açıklama**

Bu olay bir USBX konak sınıfı CDC ACM Deactivate olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-cdc-acm-ioctl-abort-in-pipe"></a>Ana bilgisayar sınıfı CDC ACM IOCTL Iptal kanalı 

#### <a name="ux_host_class_cdc_acm_ioctl_abort_in_pipe"></a>ux_host_class_cdc_acm_ioctl_abort_in_pipe

**Simge** ![ Ana bilgisayar sınıfı C D C c](./media/user-guide/usbx-events/image92.png)

**Açıklama**

Bu olay, kanal olayında bir USBX konak sınıfını CDC ACM IOCTL Iptali ' ni temsil eder.

Bilgi alanları 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: uç nokta.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-cdc-acm-ioctl-abort-out-pipe"></a>Ana bilgisayar sınıfı CDC ACM IOCTL durdurma kanalı 

#### <a name="ux_host_class_cdc_acm_ioct_abort_out_pipe"></a>ux_host_class_cdc_acm_ioct_abort_out_pipe

**Simge** ! [[Ana bilgisayar sınıfı c D c a c m I ı c T ı Durdur kanal simgesi](./media/user-guide/usbx-events/image93.png)

**Açıklama**

Bu olay, bir USBX konak sınıfını CDC ACM IOCTL Abort Out kanal olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: uç nokta.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-cdc-acm-ioctl-get-device-status"></a>Ana bilgisayar sınıfı CDC ACM IOCTL cihaz durumunu al 

#### <a name="ux_host_class_cdc_acm_ioctl_get_device_status"></a>ux_host_class_cdc_acm_ioctl_get_device_status

**Simge** ![ Ana bilgisayar sınıfı C D C A C M ı O C T I cihaz durum simgesi al](./media/user-guide/usbx-events/image94.png)

**Açıklama**

Bu olay bir USBX konak sınıfı CDC ACM IOCTL Get cihaz durumu olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: cihaz durumu.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-cdc-acm-ioctl-get-line-coding"></a>Ana bilgisayar sınıfı CDC ACM IOCTL al satırı kodlama 

#### <a name="ux_host_class_cdc_acm_ioctl_get_line_coding"></a>ux_host_class_cdc_acm_ioctl_get_line_coding

**Simge** ![ Ana bilgisayar sınıfı C D C A C M ı O C T m](./media/user-guide/usbx-events/image95.png)

**Açıklama**

Bu olay, bir USBX konak sınıfını CDC ACM IOCTL Get satırı kodlama olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: parametre.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-cdc-acm-ioctl-notification-callback"></a>Ana bilgisayar sınıfı CDC ACM IOCTL bildirimi geri araması

#### <a name="ux_host_class_cdc_acm_ioctl_notification_callback"></a>ux_host_class_cdc_acm_ioctl_notification_callback

**Simge** ![ Ana bilgisayar sınıfı C D C A C M ı O C T m](./media/user-guide/usbx-events/image96.png)

**Açıklama**

Bu olay bir USBX konak sınıfı CDC ACM IOCTL Notification geri çağırma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: parametre.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-cdc-acm-ioctl-send-break"></a>Ana bilgisayar sınıfı CDC ACM IOCTL gönderme kesmesi 

#### <a name="ux_host_class_cdc_acm_ioctl_send_break"></a>ux_host_class_cdc_acm_ioctl_send_break

**Simge** ![ Ana bilgisayar sınıfı C D C c M I m C T ı gönder kesme simgesi](./media/user-guide/usbx-events/image97.png)

**Açıklama**

Bu olay, bir USBX konak sınıfını CDC ACM IOCTL gönderme kesmesi olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: parametre.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-cdc-acm-ioctl-set-line-coding"></a>Ana bilgisayar sınıfı CDC ACM IOCTL kümesi satırı kodlama 

#### <a name="ux_host_class_cdc_acm_ioctl_set_line_coding"></a>ux_host_class_cdc_acm_ioctl_set_line_coding

**Simge** ![ C D C ana bilgisayar sınıfı c M T A c M ı O C T ı satır kodlama simge ](./media/user-guide/usbx-events/image97.png) simgesi ayarla] (./Media/User-Kılavuzu/USBX-Events/image98.png)

**Açıklama**

Bu olay bir USBX konak sınıfı CDC ACM IOCTL kümesi satırı kodlama olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: parametre.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-cdc-acm-ioctl-set-line-state"></a>Ana bilgisayar sınıfı CDC ACM IOCTL kümesi satır durumu 

#### <a name="ux_host_class_cdc_acm_ioctl_set_line_state"></a>ux_host_class_cdc_acm_ioctl_set_line_state

**Simge** ![ Ana bilgisayar sınıfı C D C c M ı O C T ı](./media/user-guide/usbx-events/image99.png)

**Açıklama**

Bu olay bir USBX konak sınıfı CDC ACM IOCTL kümesi satır durumu olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: parametre.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-cdc-acm-read"></a>Ana bilgisayar sınıfı CDC ACM okuma 

#### <a name="ux_host_class_cdc_acm_read"></a>ux_host_class_cdc_acm_read

**Simge** ![ Ana bilgisayar sınıfı C D C bir C M oku simgesi](./media/user-guide/usbx-events/image100.png)

**Açıklama**

Bu olay bir USBX konak sınıfını CDC ACM Read olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: veri işaretçisi.
- Bilgi alanı 3: Istenen uzunluk.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-cdc-acm-reception-start"></a>Ana bilgisayar sınıfı CDC ACM alma başlangıcı 

#### <a name="ux_host_class_cdc_acm_reception_start"></a>ux_host_class_cdc_acm_reception_start

**Simge** ![ Ana bilgisayar sınıfı C D C A C M alma başlangıç simgesi](./media/user-guide/usbx-events/image101.png)

**Açıklama**

Bu olay, bir USBX konak sınıfını CDC ACM alma başlangıç olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-cdc-acm-reception-stop"></a>Ana bilgisayar sınıfı CDC ACM alımı durdur 

#### <a name="ux_host_class_cdc_acm_reception_stop"></a>ux_host_class_cdc_acm_reception_stop

**Simge** ![ Ana bilgisayar sınıfı C D C bir C M alımı durdur simgesi](./media/user-guide/usbx-events/image102.png)

**Açıklama**

Bu olay, bir USBX konak sınıfı CDC ACM alımı durdurma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-cdc-acm-write"></a>Ana bilgisayar sınıfı CDC ACM yazma 

#### <a name="ux_host_class_acm_write"></a>ux_host_class_acm_write

**Simge** ![ Ana bilgisayar sınıfı C D C c M yazma simgesi](./media/user-guide/usbx-events/image103.png)

**Açıklama**

Bu olay bir USBX konak sınıfını CDC ACM yazma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: veri işaretçisi.
- Bilgi alanı 3: Istenen uzunluk.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-dpump-activate"></a>Konak sınıfı Dpump etkinleştir 

#### <a name="ux_host_class_dpump_activate"></a>ux_host_class_dpump_activate

**Simge** ![ Host Class Dpump etkinleştir simgesi](./media/user-guide/usbx-events/image104.png)

**Açıklama**

Bu olay bir USBX konak sınıfı Dpump Activate olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-dpump-deactivate"></a>Konak sınıfı Dpump devre dışı bırakma 

#### <a name="ux_host_class_dpump_deactivate"></a>ux_host_class_dpump_deactivate

**Simge** ![ Konak sınıfı Dpump etkinliğini kaldırma simgesi](./media/user-guide/usbx-events/image105.png)

**Açıklama**

Bu olay bir USBX konak sınıfı Dpump Deactivate olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-dpump-read"></a>Konak sınıfı Dpump okuma 

#### <a name="ux_host_class_dpump_read"></a>ux_host_class_dpump_read

**Simge** ![ Konak sınıfı Dpump oku simgesi](./media/user-guide/usbx-events/image106.png)

**Açıklama**

Bu olay bir USBX konak sınıfı Dpump okuma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: veri işaretçisi.
- Bilgi alanı 3: Istenen uzunluk.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-dpump-write"></a>Konak sınıfı Dpump yazma 

#### <a name="ux_host_class_dpump_write"></a>ux_host_class_dpump_write

**Simge** ![ Ana sınıf Dpump yazma simgesi](./media/user-guide/usbx-events/image107.png)

**Açıklama**

Bu olay bir USBX konak sınıfı Dpump yazma olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: veri işaretçisi.
- Bilgi alanı 3: Istenen uzunluk.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-hid-activate"></a>Konak sınıfı HID etkinleştirme 

#### <a name="ux_host_class_hid_activate"></a>ux_host_class_hid_activate

**Simge** ![ Konak sınıfı HID etkinleştirme simgesi](./media/user-guide/usbx-events/image108.png)

**Açıklama**

Bu olay bir USBX konak sınıfı HID etkinleştirme olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-hid-client-register"></a>Konak sınıfı HID Istemci kaydı 

#### <a name="ux_host_class_hid_client_register"></a>ux_host_class_hid_client_register

**Simge** ![ Konak sınıfı HID Istemci kaydı simgesi](./media/user-guide/usbx-events/image109.png)

**Açıklama**

Bu olay bir USBX konak sınıfı HID Istemci kaydı olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: HID istemci adı.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-hid-deactivate"></a>Konak sınıfı HID devre dışı 

#### <a name="ux_host_class_hid_deactivate"></a>ux_host_class_hid_deactivate

**Simge** ![ Konak sınıfı HID devre dışı bırakma simgesi](./media/user-guide/usbx-events/image110.png)

**Açıklama**

Bu olay bir USBX konak sınıfı HID devre dışı bırakma olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-hid-idle-get"></a>Konak sınıfı HID boşta al 

#### <a name="ux_host_class_hid_idle_get"></a>ux_host_class_hid_idle_get

**Simge** ![ Konak sınıfı HID boşta al al simgesi](./media/user-guide/usbx-events/image111.png)

**Açıklama**

Bu olay, bir USBX ana bilgisayar sınıfı HID boşta al Get olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-hid-idle-set"></a>Konak sınıfı HID boşta kümesi 

#### <a name="ux_host_class_hid_idle_set"></a>ux_host_class_hid_idle_set

**Simge** ![ Konak sınıfı HID boşta kümesi simgesi](./media/user-guide/usbx-events/image112.png)

**Açıklama**

Bu olay bir USBX konak sınıfı HID boşta ayarlama olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-hid-keyboard-activate"></a>Host Class HID Klavye etkinleştirme 

#### <a name="ux_host_class_hid_keyboard_activate"></a>ux_host_class_hid_keyboard_activate

**Simge** ![ Host Class HID Klavye etkinleştirme simgesi](./media/user-guide/usbx-events/image113.png)

**Açıklama**

Bu olay bir USBX Host Class HID Klavye etkinleştirme olayını temsil eder.

**Bilgi alanları**
<p>Bilgi alanı 1: sınıf örneği.
<p>Bilgi alanı 2: HID istemci örneği.
<p>Bilgi alanı 3: kullanılmıyor.
<p>Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-hid-keyboard-deactivate"></a>Host Class HID Klavye devre dışı 

#### <a name="ux_host_class_hid_keyboard_deactivate"></a>ux_host_class_hid_keyboard_deactivate

**Simge** ![ Host Class HID Klavye devre dışı simgesi](./media/user-guide/usbx-events/image114.png)

**Açıklama**

Bu olay bir USBX Host Class HID Klavye devre dışı bırakma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: HID istemci örneği.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-hid-mouse-activate"></a>Konak sınıfı HID fare etkinleştirme 

#### <a name="ux_host_class_hid_mouse_activate"></a>ux_host_class_hid_mouse_activate

**Simge** ![ Host Class HID fare etkinleştirme simgesi](./media/user-guide/usbx-events/image115.png)

**Açıklama**

Bu olay bir USBX Host Class HID fare etkinleştirme olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: HID istemci örneği.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-hid-mouse-deactivate"></a>Konak sınıfı HID fare devre dışı 

#### <a name="ux_host_class_hid_mouse_deactivate"></a>ux_host_class_hid_mouse_deactivate

**Simge** ![ Konak sınıfı HID fare devre dışı simgesi](./media/user-guide/usbx-events/image116.png)

**Açıklama**

- Bu olay bir USBX Host Class HID fare devre dışı bırakma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: HID istemci örneği.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-hid-remote-control-activate"></a>Konak sınıfı HID uzaktan denetim etkinleştirme 

#### <a name="ux_host_class_hid_remote_control_activate"></a>ux_host_class_hid_remote_control_activate

**Simge** ![ Konak sınıfı HID uzaktan denetim etkinleştirme simgesi](./media/user-guide/usbx-events/image117.png)

**Açıklama**

Bu olay bir USBX konak sınıfı HID uzaktan denetim etkinleştirme olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: HID istemci örneği.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-hid-remote-control-deactivate"></a>Konak sınıfı HID uzaktan denetim devre dışı 

#### <a name="ux_host_class_hid_remote_control_deactivate"></a>ux_host_class_hid_remote_control_deactivate

**Simge** ![ Konak sınıfı HID uzaktan denetim devre dışı simgesi](./media/user-guide/usbx-events/image118.png)

**Açıklama**

Bu olay bir USBX konak sınıfı HID uzaktan denetim devre dışı olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: HID istemci örneği.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-hid-report-get"></a>Konak sınıfı HID raporu al 

#### <a name="ux_host_class_hid_report_get"></a>ux_host_class_hid_report_get

**Simge** ![ Konak sınıfı HID raporu al simgesi](./media/user-guide/usbx-events/image119.png)

**Açıklama**

Bu olay bir USBX konak sınıfı HID raporu al 'ı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: Istemci raporu.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-hid-report-set"></a>Konak sınıfı HID rapor kümesi 

#### <a name="ux_host_class_hid_report_set"></a>ux_host_class_hid_report_set

**Simge** ![ Konak sınıfı HID rapor kümesi simgesi](./media/user-guide/usbx-events/image120.png)

**Açıklama** Bu olay bir USBX konak sınıfı HID rapor kümesini temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: Istemci raporu.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-hub-activate"></a>Konak sınıfı hub 'ı etkinleştir 

#### <a name="ux_host_class_hub_activate"></a>ux_host_class_hub_activate

**Simge** ![ Konak sınıfı hub etkinleştirme simgesi](./media/user-guide/usbx-events/image121.png)

**Açıklama**

Bu olay bir USBX konak sınıfı hub 'ı etkinleştir olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-hub-change-detect"></a>Konak sınıf hub değişikliği algılaması 

#### <a name="ux_host_class_hub_change_detect"></a>ux_host_class_hub_change_detect

**Simge** ![ Host Class hub değişikliği algılama simgesi](./media/user-guide/usbx-events/image122.png)

**Açıklama**

Bu olay bir USBX konak sınıfı hub değişiklik algılama olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-hub-deactivate"></a>Konak sınıfı hub 'ı devre dışı bırakma 

#### <a name="ux_host_class_hub_deactivate"></a>ux_host_class_hub_deactivate

**Simge** ![ Konak sınıfı hub 'ı devre dışı bırakma simgesi](./media/user-guide/usbx-events/image123.png)

**Açıklama**

Bu olay bir USBX konak sınıfı hub 'ı devre dışı bırakma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-hub-port-change-connection-process"></a>Konak sınıf hub 'ı bağlantı noktası değiştirme bağlantı Işlemi 

#### <a name="ux_host_class_hub_change_connection_process"></a>ux_host_class_hub_change_connection_process

**Simge** ![ Konak sınıf hub 'ı bağlantı noktası değişiklik bağlantı Işlemi simgesi](./media/user-guide/usbx-events/image124.png)

**Açıklama**

Bu olay bir USBX konak sınıfı hub bağlantı noktası değişim bağlantı Işlemi olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: bağlantı noktası.
- Bilgi alanı 3: bağlantı noktası durumu.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-hub-port-change-enable-process"></a>Konak sınıfı hub bağlantı noktası değişikliği etkinleştirme Işlemi 

#### <a name="ux_host_class_hub_port_change_enable_process"></a>ux_host_class_hub_port_change_enable_process

**Simge** ![ Konak sınıfı hub bağlantı noktası değişikliği etkinleştirme Işlemi simgesi](./media/user-guide/usbx-events/image125.png)

**Açıklama**

Bu olay bir USBX konak sınıfı hub bağlantı noktası değişikliğini Işlemi etkinleştir olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: bağlantı noktası.
- Bilgi alanı 3: bağlantı noktası durumu.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-hub-port-change-over-current-process"></a>Geçerli Işlem üzerinde ana bilgisayar sınıfı hub bağlantı noktası değişikliği 

#### <a name="ux_host_class_hub_port_change_over_current_process"></a>ux_host_class_hub_port_change_over_current_process

**Simge** ![ Ana sınıf hub 'ı bağlantı noktası geçerli Işlem simgesi değişikliği](./media/user-guide/usbx-events/image126.png)

**Açıklama**

Bu olay nx_packet_allocate aracılığıyla bir paket ayırmayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: bağlantı noktası.
- Bilgi alanı 3: bağlantı noktası durumu.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-hub-port-change-reset-process"></a>Konak sınıf hub 'ı bağlantı noktası değişiklik sıfırlama Işlemi 

#### <a name="ux_host_class_hub_port_change_reset_process"></a>ux_host_class_hub_port_change_reset_process

**Simge** ![ Konak sınıf hub 'ı bağlantı noktası değişiklik sıfırlama Işlemi simgesi](./media/user-guide/usbx-events/image127.png)

**Açıklama**

Bu olay bir USBX konak sınıfı hub bağlantı noktası değişiklik sıfırlama Işlemi olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: hub. Bilgi alanı 2: bağlantı noktası.
- Bilgi alanı 3: bağlantı noktası durumu.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-hub-port-change-suspend-process"></a>Konak sınıf hub 'ı bağlantı noktası değiştirme askıya alma Işlemi 

#### <a name="ux_host_class_hub_port_change_suspend_process"></a>ux_host_class_hub_port_change_suspend_process

**Simge** ![ Konak sınıf hub 'ı bağlantı noktası değiştirme Işlemi askıya alma simgesi](./media/user-guide/usbx-events/image128.png)

**Açıklama**

Bu olay bir USBX konak sınıfı hub 'ı değişiklik askıya alma Işlemi olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: bağlantı noktası.
- Bilgi alanı 3: bağlantı noktası durumu.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-pima-activate"></a>Konak sınıfı Pima etkinleştir 

#### <a name="ux_host_class_pima_activate"></a>ux_host_class_pima_activate

**Simge** ![ Konak sınıfı Pima etkinleştirme simgesi](./media/user-guide/usbx-events/image129.png)

**Açıklama**

Bu olay bir USBX konak sınıfı Pima Activate olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-pima-deactivate"></a>Konak sınıfı Pima devre dışı 

#### <a name="ux_host_class_pima_deactivate"></a>ux_host_class_pima_deactivate

**Simge** ![ Konak sınıfı Pima devre dışı bırakma simgesi](./media/user-guide/usbx-events/image130.png)

**Açıklama**

Bu olay bir USBX konak sınıfı Pima devre dışı bırakma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-pima-device-info-get"></a>Konak sınıfı Pima cihaz bilgileri Get 

#### <a name="ux_host_class_pima_device_info_get"></a>ux_host_class_pima_device_info_get

**Simge** ![ Konak sınıfı Pima cihaz bilgileri al simgesi](./media/user-guide/usbx-events/image131.png)

**Açıklama**

Bu olay bir USBX konak sınıfı Pima cihaz bilgileri Get olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: Pima cihazı.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-pima-device-reset"></a>Konak sınıfı Pima cihazı sıfırlama 

#### <a name="ux_host_class_pima_device_reset"></a>ux_host_class_pima_device_reset

**Simge** ![ Konak sınıfı Pima cihazı sıfırlama simgesi](./media/user-guide/usbx-events/image132.png)

**Açıklama**

Bu olay bir USBX konak sınıfı Pima cihazı sıfırlama olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-pima-notification"></a>Konak sınıfı Pima bildirimi 

#### <a name="ux_host_class_pima_notification"></a>ux_host_class_pima_notification

**Simge** ![ Konak sınıfı Pima bildirimi simgesi](./media/user-guide/usbx-events/image133.png)

**Açıklama**

Bu olay bir USBX konak sınıfı Pima bildirimi olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği. Bilgi alanı 2: olay kodu.
- Bilgi alanı 3: Işlem KIMLIĞI.
- Bilgi alanı 4: parametre1.

### <a name="host-class-pima-number-objects-get"></a>Konak sınıfı Pima sayısı nesneleri Al 

#### <a name="ux_host_class_pima_number_objects_get"></a>ux_host_class_pima_number_objects_get

**Simge** ![ Konak sınıfı Pima sayısı nesneleri Al simgesi](./media/user-guide/usbx-events/image134.png)

**Açıklama**

Bu olay bir USBX konak sınıfı Pima Number nesneleri Al olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-pima-object-close"></a>Konak sınıfı Pima nesnesi kapatma 

#### <a name="ux_host_class_pima_object_close"></a>ux_host_class_pima_object_close

**Simge** ![ Ana sınıf Pima nesnesi kapatma simgesi](./media/user-guide/usbx-events/image135.png)

**Açıklama**

Bu olay bir USBX Host Class Pima nesnesi Close olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: nesne.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-pima-object-copy"></a>Konak sınıfı Pima nesne kopyası 

#### <a name="ux_host_class_pima_object_copy"></a>ux_host_class_pima_object_copy

**Simge** ![ Konak sınıfı Pima nesnesi kopyalama simgesi](./media/user-guide/usbx-events/image136.png)

**Açıklama**

Bu olay bir USBX konak sınıfı Pima nesne kopyalama olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: nesne tanıtıcısı.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-pima-object-delete"></a>Konak sınıfı Pima nesnesi silme 

#### <a name="ux_host_class_pima_object_delete"></a>ux_host_class_pima_object_delete

**Simge** ![ Konak sınıfı Pima nesnesi silme simgesi](./media/user-guide/usbx-events/image137.png)

**Açıklama**

Bu olay bir USBX konak sınıfı Pima nesnesi silme olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: nesne tanıtıcısı.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-pima-object-get"></a>Konak sınıfı Pima nesnesi Get 

#### <a name="ux_host_class_pima_object_get"></a>ux_host_class_pima_object_get

**Simge** ![ Ana sınıf Pima nesnesi Al simgesi](./media/user-guide/usbx-events/image138.png)

**Açıklama**

Bu olay nx_rarp_info_get aracılığıyla RARP bilgilerini almayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: nesne tanıtıcısı.
- Bilgi alanı 3: nesne.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-pima-object-info-get"></a>Konak sınıfı Pima nesnesi bilgi al 

#### <a name="ux_host_class_pima_object_info_get"></a>ux_host_class_pima_object_info_get

**Simge** ![ Konak sınıfı Pima nesnesi bilgileri al simgesi](./media/user-guide/usbx-events/image139.png)

**Açıklama**

Bu olay bir USBX konak sınıfı Pima nesne bilgileri al olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: nesne tanıtıcısı.
- Bilgi alanı 3: nesne.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-pima-object-info-send"></a>Konak sınıfı Pima nesne bilgileri gönderme 

#### <a name="ux_host_class_pima_object_info_send"></a>ux_host_class_pima_object_info_send

**Simge** ![ Konak sınıfı Pima nesne bilgileri gönderme simgesi](./media/user-guide/usbx-events/image140.png)

**Açıklama**

Bu olay bir USBX konak sınıfı Pima nesne bilgileri gönderme olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: nesne.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-pima-object-move"></a>Konak sınıfı Pima nesnesi taşıma 

#### <a name="ux_host_class_pima_object_move"></a>ux_host_class_pima_object_move

**Simge** ![ Konak sınıfı Pima nesnesi taşıma simgesi](./media/user-guide/usbx-events/image141.png)

**Açıklama**

Bu olay Reprbu olayı, bir USBX konak sınıfı Pima nesne taşıma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: nesne tanıtıcısı.
- Bilgi alanı 3: nesne.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-pima-object-send"></a>Konak sınıfı Pima nesnesi gönder 

#### <a name="ux_host_class_pima_object_move"></a>ux_host_class_pima_object_move

**Simge** ![ Ana sınıf Pima nesnesi Gönder simgesi](./media/user-guide/usbx-events/image142.png)

**Açıklama**

Bu olay bir USBX konak sınıfı Pima nesnesi gönderme olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: nesne.
- Bilgi alanı 3: nesne arabelleği.
- Bilgi alanı 4: nesne uzunluğu.

### <a name="host-class-pima-object-transfer-abort"></a>Konak sınıfı Pima nesnesi aktarımı Iptali 

#### <a name="ux_host_class_pima_object_transfer_abort"></a>ux_host_class_pima_object_transfer_abort

**Simge** ![ Konak sınıfı Pima nesne aktarımı Iptali simgesi](./media/user-guide/usbx-events/image143.png)

**Açıklama**

Bu olay bir USBX konak sınıfı Pima nesne aktarımı Iptali olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: nesne tanıtıcısı.
- Bilgi alanı 3: nesne.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-pima-read"></a>Konak sınıfı Pima oku 

#### <a name="ux_host_class_pima_read"></a>ux_host_class_pima_read

**Simge** ![ Konak sınıfı Pima oku simgesi](./media/user-guide/usbx-events/image144.png)

**Açıklama**

Bu olay bir USBX konak sınıfı Pima okuma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: veri işaretçisi.
- Bilgi alanı 3: veri uzunluğu.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-pima-request-cancel"></a>Konak sınıfı Pima Isteği Iptali 

#### <a name="ux_host_class_pima_request_cancel"></a>ux_host_class_pima_request_cancel

**Simge** ![ Konak sınıfı Pima Isteği Iptal simgesi](./media/user-guide/usbx-events/image145.png)

**Açıklama**

Bu olay bir USBX konak sınıfı Pima Isteği Iptali olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-pima-session-close"></a>Konak sınıfı Pima oturumu Kapat 

#### <a name="ux_host_class_pima_session_close"></a>ux_host_class_pima_session_close

**Simge** ![ Ana sınıf Pima oturumu kapatma simgesi](./media/user-guide/usbx-events/image146.png)

**Açıklama**

Bu olay bir USBX konak sınıfı Pima oturumu kapatma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: Pima oturumu.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-pima-session-open"></a>Konak sınıfı Pima oturumu açık 

#### <a name="ux_host_class_pima_session_open"></a>ux_host_class_pima_session_open

**Simge** ![ Konak sınıfı Pima oturumu açma simgesi](./media/user-guide/usbx-events/image147.png)

**Açıklama** Bu olay bir USBX konak sınıfı Pima oturum açma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: Pima oturumu.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-pima-storage-ids-get"></a>Konak sınıfı Pima depolama kimliklerini al 

#### <a name="ux_host_class_pima_session_ids_get"></a>ux_host_class_pima_session_ids_get

**Simge** ![ Konak sınıfı Pima depolama kimlikleri al simgesi](./media/user-guide/usbx-events/image148.png)

**Açıklama**

Bu olay bir USBX konak sınıfı Pima depolama kimlikleri al olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- NFO alanı 2: depolama KIMLIĞI dizisi.
- Bilgi alanı 3: depolama KIMLIĞI uzunluğu.
Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-pima-storage-info-get"></a>Konak sınıfı Pima depolama bilgileri Get 

#### <a name="ux_host_class_pima_storage_info_get"></a>ux_host_class_pima_storage_info_get

**Simge** ![ Konak sınıfı Pima depolama bilgileri al simgesi](./media/user-guide/usbx-events/image149.png)

**Açıklama**

Bu olay bir USBX konak sınıfı Pima depolama bilgi al olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: depolama KIMLIĞI.
- Bilgi alanı 3: depolama.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-pima-thumb-get"></a>Ana sınıf Pima parmak izi al 

#### <a name="ux_host_class_pima_thumb_get"></a>ux_host_class_pima_thumb_get

**Simge** ![ Konak sınıfı Pima Thumb al simgesi](./media/user-guide/usbx-events/image150.png)

**Açıklama**

Bu olay, nx_tcp_server_socket_unaccept aracılığıyla bir TCP sunucusu bağlantısının kabul edilmemesine yönelik temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: nesne tanıtıcısı.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-pima-write"></a>Konak sınıfı Pima yazma 

#### <a name="ux_host_class_pima_thumb_get"></a>ux_host_class_pima_thumb_get

**Simge** ![ Konak sınıfı Pima yazma simgesi](./media/user-guide/usbx-events/image151.png)

**Açıklama**

Bu olay bir USBX konak sınıfını Pima yazmayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: veri işaretçisi.
- Bilgi alanı 3: veri uzunluğu.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-printer-activate"></a>Konak sınıfı yazıcısını etkinleştir 

#### <a name="ux_host_class_printer_activate"></a>ux_host_class_printer_activate

**Simge** ![ Konak sınıfı yazıcı etkinleştirme simgesi](./media/user-guide/usbx-events/image152.png)

**Açıklama**

Bu olay bir USBX konak sınıfı yazıcı etkinleştirme olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi.
- Bilgi alanı 2: yuva Işaretçisi.
- Bilgi alanı 3: hizmet türü.
- Bilgi alanı 4: pencere boyutunu al.

### <a name="host-class-printer-deactivate"></a>Konak sınıfı yazıcısını devre dışı bırak 

#### <a name="ux_host_class_printer_deactivate"></a>ux_host_class_printer_deactivate

**Simge** ![ Konak sınıfı yazıcı devre dışı simgesi](./media/user-guide/usbx-events/image153.png)

**Açıklama**

Bu olay bir USBX konak sınıfı yazıcısı devre dışı bırakma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-printer-name-get"></a>Konak sınıfı yazıcı adı Al 

#### <a name="ux_host_class_printer_name_get"></a>ux_host_class_printer_name_get

**Simge** ![ Konak sınıfı yazıcı adı Al simgesi](./media/user-guide/usbx-events/image154.png)

**Açıklama**

Bu olay bir USBX konak sınıfı yazıcı adı Al olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-printer-read"></a>Konak sınıfı yazıcısını oku 

#### <a name="ux_host_class_printer_read"></a>ux_host_class_printer_read

**Simge** ![ Ana bilgisayar sınıfı yazıcı okuma simgesi](./media/user-guide/usbx-events/image155.png)

**Açıklama**

Bu olay bir USBX ana bilgisayar sınıfı yazıcı okuma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: veri işaretçisi.
- Bilgi alanı 3: Istenen uzunluk.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-printer-soft-reset"></a>Konak sınıfı yazıcı yazılımdan sıfırlama 

#### <a name="ux_host_class_printer_soft_reset"></a>ux_host_class_printer_soft_reset

**Simge** ![ Konak sınıfı yazıcı geçici sıfırlama simgesi](./media/user-guide/usbx-events/image156.png)

**Açıklama**

Bu olay bir USBX konak sınıfı yazıcı geçici sıfırlama olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-printer-status-get"></a>Konak sınıfı yazıcı durumu Al 

#### <a name="ux_host_class_printer_status_get"></a>ux_host_class_printer_status_get

**Simge** ![ Konak sınıfı yazıcı durumu Al simgesi](./media/user-guide/usbx-events/image157.png)

**Açıklama**

Bu olay bir USBX konak sınıfı yazıcı durumu Al olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: yazıcı durumu.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-printer-write"></a>Ana bilgisayar sınıfı yazıcı yazma 

#### <a name="ux_host_class_printer_write"></a>ux_host_class_printer_write

**Simge** ![ Konak sınıfı yazıcı yazma simgesi](./media/user-guide/usbx-events/image158.png)

**Açıklama**

Bu olay, bir USBX konak sınıfı yazıcısını yazmayı temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: veri işaretçisi.
- Bilgi alanı 3: Istenen uzunluk.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-prolific-activate"></a>Konak sınıfı Prolific etkinleştir 

#### <a name="ux_host_class_prolific_activate"></a>ux_host_class_prolific_activate 

**Simge** ![ Konak sınıfı Prolific etkinleştirme simgesi](./media/user-guide/usbx-events/image159.png)

**Açıklama**

Bu olay bir USBX konak sınıfı Prolific Activate olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-prolific-deactivate"></a>Ana bilgisayar sınıfı Prolifik devre dışı 

#### <a name="ux_host_class_prolific_deactivate"></a>ux_host_class_prolific_deactivate 

**Simge** ![ Konak sınıfı Prolific devre dışı bırakma simgesi](./media/user-guide/usbx-events/image160.png)

**Açıklama**

Bu olay bir USBX konak sınıfı Prolific Deactivate olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-prolific-ioctl-abort-in-pipe"></a>Ana bilgisayar sınıfı işlem kanalında IOCTL Iptali 

#### <a name="ux_host_class_prolific_ioctl_abort_in_pipe"></a>ux_host_class_prolific_ioctl_abort_in_pipe

**Simge** ![ Kanal simgesinde ana bilgisayar sınıfı proo C T L durdur](./media/user-guide/usbx-events/image161.png)

**Açıklama**

Bu olay, kanal olayında bir USBX ana bilgisayar sınıfını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: uç nokta.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-prolific-ioctl-abort-out-pipe"></a>Konak sınıfı Prolific IOCTL durdurma kanalı 

#### <a name="ux_host_class_prolific_ioctl_abort_out_pipe"></a>ux_host_class_prolific_ioctl_abort_out_pipe

**Simge** ![ Ana bilgisayar sınıfı proo C T L m ı Durdur kanal simgesi](./media/user-guide/usbx-events/image162.png)

**Açıklama**

Bu olay, bir USBX konak sınıfı Prolific IOCTL durdurma kanalı olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: uç nokta.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-prolific-ioctl-get-device-status"></a>Konak sınıfı Prolific IOCTL cihaz durumunu al 

#### <a name="ux_host_class_prolific_ioctl_get_device_status"></a>ux_host_class_prolific_ioctl_get_device_status

**Simge** ![ Konak sınıfı Prolific g T C T L bir cihaz durumu simgesi al](./media/user-guide/usbx-events/image163.png)

**Açıklama**

Bu olay bir USBX konak sınıfı Prolific IOCTL Get cihaz durumu olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: cihaz durumu.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-prolific-ioctl-get-line-coding"></a>Konak sınıfı Prolific IOCTL al satırı kodlama 

#### <a name="ux_host_class_prolific_ioctl_get_line_coding"></a>ux_host_class_prolific_ioctl_get_line_coding

**Simge** ![ Konak sınıfı Prolific ı T C T L Class for satırı kodlama simgesi](./media/user-guide/usbx-events/image164.png)

**Açıklama**

Bu olay, bir USBX konak sınıfı Prolific IOCTL Get satırı kodlama olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: parametre.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-prolific-ioctl-purge"></a>Konak sınıfı Prolific IOCTL Temizleme 

#### <a name="ux_host_class_prolific_ioctl_purge"></a>ux_host_class_prolific_ioctl_purge

**Simge** ![ Konak sınıfı Prolific IOCTL Temizleme simgesi](./media/user-guide/usbx-events/image165.png)

**Açıklama**

Bu olay bir USBX konak sınıfı Prolific IOCTL Temizleme olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: parametre.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-prolific-ioctl-report-device"></a>Konak sınıfı Prolific IOCTL rapor cihazı 

#### <a name="ux_host_class_prolific_ioctl_report_device"></a>ux_host_class_prolific_ioctl_report_device

**Simge** ![ Konak sınıfı Prolific ı T C T m rapor cihaz simgesi](./media/user-guide/usbx-events/image166.png)

**Açıklama**

Bu olay bir USBX konak sınıfı Prolific IOCTL rapor cihaz durumu değişiklik olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: parametre.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-prolific-ioctl-send-break"></a>Konak sınıfı Prolific IOCTL gönderme kesmesi 

#### <a name="ux_host_class_prolific_ioctl_send_break"></a>ux_host_class_prolific_ioctl_send_break

**Simge** ![ Konak sınıfı Prolific ı T C T L gönderme sonu simgesi](./media/user-guide/usbx-events/image167.png)

**Açıklama**

Bu olay bir USBX konak sınıfı Prolific IOCTL gönderme kesmesi olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-prolific-ioctl-set-line-coding"></a>Konak sınıfı Prolific IOCTL kümesi satırı kodlama 

#### <a name="ux_host_class_prolific_ioctl_set_line_coding"></a>ux_host_class_prolific_ioctl_set_line_coding

**Simge** ![ Konak sınıfı Prolific ı T C T L Class for satırı kodlama simgesi](./media/user-guide/usbx-events/image168.png)

**Açıklama**

Bu olay, bir USBX konak sınıfı Prolific IOCTL kümesi satırı kodlama olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: parametre.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-prolific-ioctl-set-line-state"></a>Konak sınıfı Prolific IOCTL kümesi satır durumu 

#### <a name="ux_host_class_prolific_ioctl_set_line_state"></a>ux_host_class_prolific_ioctl_set_line_state

**Simge** ![ Konak sınıfı Prolific ı T C T L s satır durumu simgesi](./media/user-guide/usbx-events/image169.png)

**Açıklama**

Bu olay bir USBX konak sınıfı Prolific IOCTL kümesi satır durumu olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: parametre.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-prolific-read"></a>Ana bilgisayar sınıfı okuma 

#### <a name="ux_host_class_prolific_read"></a>ux_host_class_prolific_read

**Simge** ![ Konak sınıfı Prolific okuma simgesi](./media/user-guide/usbx-events/image170.png)

**Açıklama**

Bu olay bir USBX konak sınıfı için bir okuma olayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: veri işaretçisi.
- Bilgi alanı 3: Istenen uzunluk.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-prolific-reception-start"></a>Konak sınıfı Prolific alma başlangıcı 

#### <a name="ux_host_class_prolific_reception_start"></a>ux_host_class_prolific_reception_start

**Simge** ![ Konak sınıfı Prolific alma başlangıç simgesi](./media/user-guide/usbx-events/image171.png)

**Açıklama**

Bu olay bir USBX konak sınıfı Prolific alma başlangıç olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-prolific-reception-stop"></a>Konak sınıfı Prolific alımı durdur 

#### <a name="ux_host_class_prolific_reception_stop"></a>ux_host_class_prolific_reception_stop

**Simge** ![ Konak sınıfı Prolific alımı durdurma simgesi](./media/user-guide/usbx-events/image172.png)

**Açıklama**

Bu olay bir USBX konak sınıfı Prolific alma durdurma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-prolific-write"></a>Ana bilgisayar sınıfı başlangıç yazma 

#### <a name="ux_host_class_prolific_write"></a>ux_host_class_prolific_write

**Simge** ![ Ana makine sınıfı başlangıç yazma simgesi](./media/user-guide/usbx-events/image173.png)

**Açıklama**

Bu olay bir USBX konak sınıfı Prolific yazma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: veri işaretçisi.
- Bilgi alanı 3: Istenen uzunluk.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-storage-activate"></a>Konak sınıfı depolamayı etkinleştirme 

#### <a name="ux_host_class_storage_activate"></a>ux_host_class_storage_activate

**Simge** ![ Konak sınıfı depolama etkinleştirme simgesi](./media/user-guide/usbx-events/image174.png)

**Açıklama**

Bu olay bir USBX konak sınıfı depolama etkinleştirme olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-storage-deactivate"></a>Konak sınıfı depolamayı devre dışı bırakma 

#### <a name="ux_host_class_storage_deactivate"></a>ux_host_class_storage_deactivate

**Simge** ![ Konak sınıfı depolamayı devre dışı bırakma simgesi](./media/user-guide/usbx-events/image175.png)

**Açıklama**

Bu olay bir USBX konak sınıfı depolaması devre dışı bırakma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-storage-media-capacity-get"></a>Konak sınıfı depolama medyası kapasitesi al 

#### <a name="ux_host_class_storage_media_capacity_get"></a>ux_host_class_storage_media_capacity_get

**Simge** ![ Konak sınıfı depolama medyası kapasitesi al simgesi](./media/user-guide/usbx-events/image176.png)

**Açıklama**

Bu olay bir USBX konak sınıfı depolama medyası kapasitesini al olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-storage-media-format-capacity-get"></a>Konak sınıfı depolama medyası biçim kapasitesini al

#### <a name="ux_host_class_storage_media_format_capacity_get"></a>ux_host_class_storage_media_format_capacity_get

**Simge** ![ Konak sınıfı depolama medya biçimi kapasitesi al simgesi](./media/user-guide/usbx-events/image177.png)

**Açıklama**

Bu olay bir USBX konak sınıfı depolama medyası biçimlendirme kapasitesini al olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

#### <a name="host-class-storage-media-mount"></a>Konak sınıfı depolama medyası bağlama 

#### <a name="ux_host_class_storage_media_mount"></a>ux_host_class_storage_media_mount

**Simge** ![ Konak sınıfı depolama medyası bağlama simgesi](./media/user-guide/usbx-events/image178.png)

**Açıklama**

Bu olay bir USBX konak sınıfı depolama medyası bağlama olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: sektör.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-storage-media-open"></a>Konak sınıfı depolama medyası açık 

#### <a name="ux_host_class_storage_media_open"></a>ux_host_class_storage_media_open

**Simge** ![ Konak sınıfı depolama medyası açık simgesi](./media/user-guide/usbx-events/image179.png)

**Açıklama**

Bu olay bir USBX konak sınıfı depolama medyası açık olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: medya.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-storage-media-read"></a>Konak sınıfı depolama medyası okuma 

#### <a name="ux_host_class_storage_media_read"></a>ux_host_class_storage_media_read

**Simge** ![ Konak sınıfı depolama medyası okuma simgesi](./media/user-guide/usbx-events/image180.png)

**Açıklama**

Bu olay bir USBX konak sınıfı depolama medyası okuma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kesim başlangıcı.
- Bilgi alanı 3: sektör sayısı.
- Bilgi alanı 4: veri işaretçisi.

### <a name="host-class-storage-media-write"></a>Konak sınıfı depolama medyası yazma 

#### <a name="ux_host_class_storage_media_write"></a>ux_host_class_storage_media_write

**Simge** ![ Konak sınıfı depolama medyası yazma simgesi](./media/user-guide/usbx-events/image181.png)

**Açıklama**

Bu olay bir USBX konak sınıfı depolama medyası yazma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kesim başlangıcı.
- Bilgi alanı 3: sektör sayısı.
- Bilgi alanı 4: veri işaretçisi.

### <a name="host-class-storage-request-sense"></a>Konak sınıfı depolama Istek algılaması 

#### <a name="ux_host_class_storage_request_sense"></a>ux_host_class_storage_request_sense

**Simge** ![ Konak sınıfı depolama Isteği algılama simgesi](./media/user-guide/usbx-events/image182.png)

**Açıklama**

Bu olay bir USBX konak sınıfı depolama Istek algılama olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-storage-start-stop"></a>Konak sınıfı depolama başlatma durdurma 

#### <a name="ux_host_class_storage_start_stop"></a>ux_host_class_storage_start_stop

**Simge** ![ Konak sınıfı depolama başlatma durdurma simgesi](./media/user-guide/usbx-events/image183.png)

**Açıklama**

Bu olay bir USBX konak sınıfı depolama başlangıç durdurma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: durdurma sinyalini başlatın.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-storage-unit-ready-test"></a>Konak sınıfı depolama birimi için hazırlanma testi 

#### <a name="ux_host_class_storage_unit_ready_test"></a>ux_host_class_storage_unit_ready_test

**Simge** ![ Konak sınıfı depolama birimi için Ready test simgesi](./media/user-guide/usbx-events/image184.png)

**Açıklama**

Bu olay, bir USBX konak sınıfı depolama birimi için hazırlanma sınama olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-stack-class-instance-create"></a>Konak yığını sınıf örneği oluşturma 

#### <a name="ux_host_class_instance_create"></a>ux_host_class_instance_create

**Simge** ![ Konak yığını sınıf örneği oluşturma simgesi](./media/user-guide/usbx-events/image185.png)

**Açıklama**

Bu olay bir USBX konak yığını sınıf örneği oluşturma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf.
- Bilgi alanı 2: sınıf örneği.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-stack-class-instance-destroy"></a>Konak yığını sınıf örneği yok etme 

#### <a name="ux_host_class_instance_create"></a>ux_host_class_instance_create

**Simge** ![ Konak yığını sınıf örneği yok etme simgesi](./media/user-guide/usbx-events/image186.png)

**Açıklama**

Bu olay bir USBX konak yığın sınıfı örneği yok etme olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf.
- Bilgi alanı 2: sınıf örneği.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-stack-configuration-delete"></a>Konak yığını yapılandırması silme 

#### <a name="ux_host_class_configuration_delete"></a>ux_host_class_configuration_delete

**Simge** ![ Konak yığını yapılandırması silme simgesi](./media/user-guide/usbx-events/image187.png)

**Açıklama**

Bu olay bir USBX konak yığını yapılandırması silme olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: yapılandırma.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-stack-configuration-enumerate"></a>Konak yığını yapılandırması numaralandırması 

#### <a name="ux_host_stack_configuration_enumerate"></a>ux_host_stack_configuration_enumerate

**Simge** ![ Konak yığını yapılandırması sıralama simgesi](./media/user-guide/usbx-events/image188.png)

**Açıklama**

Bu olay bir USBX konak yığını yapılandırması listeleme olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: cihaz.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="stack-configuration-instance-create"></a>Yığın yapılandırma örneği oluşturma 

#### <a name="ux_host_stack_configuration_instance_create"></a>ux_host_stack_configuration_instance_create

**Simge** ![ Yığın yapılandırma örneği oluşturma simgesi](./media/user-guide/usbx-events/image189.png)

**Açıklama**

Bu olay bir USBX konak yığını yapılandırma örneği oluşturma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: yapılandırma.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-stack-configuration-instance-delete"></a>Konak yığını yapılandırma örneği silme 

#### <a name="ux_host_stack_configuration_instance_delete"></a>ux_host_stack_configuration_instance_delete

**Simge** ![ Konak yığını yapılandırma örneği silme simgesi](./media/user-guide/usbx-events/image190.png)

**Açıklama**

Bu olay bir USBX konak yığını yapılandırma örneği silme olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: yapılandırma.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-stack-configuration-set"></a>Konak yığını yapılandırma kümesi 

#### <a name="ux_host_stack_configuration_set"></a>ux_host_stack_configuration_set

**Simge** ![ Konak yığını yapılandırma kümesi simgesi](./media/user-guide/usbx-events/image191.png)

**Açıklama**

Bu olay bir USBX konak yığını yapılandırma kümesi olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: yapılandırma.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-stack-device-address-set"></a>Konak yığını cihaz adresi kümesi 

#### <a name="ux_host_stack_device_address_set"></a>ux_host_stack_device_address_set

**Simge** ![ Konak yığını cihaz adresi kümesi simgesi](./media/user-guide/usbx-events/image192.png)

**Açıklama**

Bu olay bir USBX konak yığını cihaz adresi kümesi olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: cihaz.
- Bilgi alanı 2: cihaz adresi.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-stack-device-configuration-get"></a>Konak yığını cihaz yapılandırmasını al 

#### <a name="ux_host_stack_device_configuration_get"></a>ux_host_stack_device_configuration_get

**Simge** ![ Konak yığını cihaz yapılandırması Get simgesi](./media/user-guide/usbx-events/image193.png)

**Açıklama**

Bu olay bir USBX konak yığını cihaz yapılandırması Get olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: cihaz.
- NFO alanı 2: yapılandırma.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-stack-device-configuration-select"></a>Konak yığını cihaz yapılandırması seçme 

#### <a name="ux_host_stack_device_configuration_select"></a>ux_host_stack_device_configuration_select

**Simge** ![ Konak yığını cihaz yapılandırması seçim simgesi](./media/user-guide/usbx-events/image194.png)

**Açıklama**

Bu olay bir USBX konak yığını cihaz yapılandırması seçme olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: cihaz.
- Bilgi alanı 2: yapılandırma.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-stack-device-descriptor-read"></a>Konak yığını cihaz tanımlayıcısı okuma 

#### <a name="ux_host_stack_device_descriptor_read"></a>ux_host_stack_device_descriptor_read

**Simge** ![ Konak yığını cihaz tanımlayıcısı okuma simgesi](./media/user-guide/usbx-events/image195.png)

**Açıklama**

Bu olay bir USBX konak yığını cihaz tanımlayıcısı okuma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: cihaz.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-stack-device-get"></a>Konak yığını cihazını al 

#### <a name="ux_host_stack_device_get"></a>ux_host_stack_device_get

**Simge** ![ Konak yığını cihazının al simgesi](./media/user-guide/usbx-events/image196.png)

**Açıklama**

Bu olay bir USBX konak yığını cihaz Get olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: cihaz dizini.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-stack-device-remove"></a>Konak yığını cihazını kaldırma 

#### <a name="ux_host_stack_device_remove"></a>ux_host_stack_device_remove

**Simge** ![ Konak yığını cihaz kaldırma simgesi](./media/user-guide/usbx-events/image197.png)

**Açıklama**

Bu olay bir USBX konak yığını cihaz kaldırma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: HCD.
- Bilgi alanı 2: üst öğe.
- Bilgi alanı 3: bağlantı noktası dizini.
- Bilgi alanı 4: cihaz.

### <a name="host-stack-device-resource-free"></a>Konak yığını cihaz kaynağı boş 

#### <a name="ux_host_stack_device_resource_free"></a>ux_host_stack_device_resource_free

**Simge** ![ Ana bilgisayar yığını cihaz kaynağı boş simgesi](./media/user-guide/usbx-events/image198.png)

**Açıklama**

Bu olay bir USBX konak yığını cihaz kaynağı ücretsiz olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: cihaz.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-stack-endpoint-instance-create"></a>Konak yığını uç noktası örneği oluşturma 

#### <a name="ux_host_stack_endpoint_instance_create"></a>ux_host_stack_endpoint_instance_create

**Simge** ![ Konak yığını uç noktası örneği oluşturma simgesi](./media/user-guide/usbx-events/image199.png)

**Açıklama**

Bu olay bir USBX konak yığını uç noktası örneği oluşturma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: cihaz.
- Bilgi alanı 2: uç nokta.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-stack-endpoint-instance-delete"></a>Konak yığın uç noktası örneği silme 

#### <a name="ux_host_stack_endpoint_instance_delete"></a>ux_host_stack_endpoint_instance_delete

**Simge** ![ Konak yığın uç noktası örneği silme simgesi](./media/user-guide/usbx-events/image200.png)

**Açıklama**

Bu olay bir USBX konak yığını uç noktası örneği silme olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 2: uç nokta.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-stack-endpoint-reset"></a>Konak yığını uç noktası sıfırlama 

#### <a name="ux_host_stack_endpoint_reset"></a>ux_host_stack_endpoint_reset

**Simge** ![ Konak yığını uç noktası sıfırlama simgesi](./media/user-guide/usbx-events/image201.png)

**Açıklama**

Bu olay bir USBX konak yığını uç noktası sıfırlama olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: cihaz.
- Bilgi alanı 2: uç nokta.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-stack-endpoint-transfer-abort"></a>Konak yığını uç noktası aktarımı Iptali 

#### <a name="ux_host_stack_endpoint_transfer_abort"></a>ux_host_stack_endpoint_transfer_abort

**Simge** ![ Konak yığını uç noktası aktarımı Iptal simgesi](./media/user-guide/usbx-events/image202.png)

**Açıklama**

Bu olay bir USBX konak yığını uç nokta aktarımı Iptali olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: uç nokta.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-stack-host-controller-register"></a>Konak yığını konak denetleyicisi kaydı 

#### <a name="ux_host_stack_hcd_register"></a>ux_host_stack_hcd_register

**Simge** ![ Konak yığını konak denetleyicisi kayıt simgesi](./media/user-guide/usbx-events/image203.png)

**Açıklama**

Bu olay bir USBX konak yığını konak denetleyicisi kaydını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: HCD adı.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-stack-initialize"></a>Konak yığını başlatma 

#### <a name="ux_host_stack_initialize"></a>ux_host_stack_initialize

**Simge** ![ Konak yığını başlatma simgesi](./media/user-guide/usbx-events/image204.png)

**Açıklama**

Bu olay bir USBX konak Stack Initialize olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: kullanılmıyor.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-stack-interface-endpoint-get"></a>Konak yığını arabirimi uç noktası al 

#### <a name="interface_-tcp-retry-entry"></a>Interface_ TCP yeniden deneme girdisi

**Simge** ![ Konak yığını arabirimi uç noktası al simgesi](./media/user-guide/usbx-events/image205.png)

**Açıklama**

Bu olay bir iç NetX TCP yeniden deneme olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: arabirim.
- Bilgi alanı 2: uç nokta dizini.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-stack-interface-instance-create"></a>Konak yığını arabirim örneği oluşturma 

#### <a name="ux_host_stack_interface_instance_create"></a>ux_host_stack_interface_instance_create

**Simge** ![ Konak yığını arabirim örneği oluşturma simgesi](./media/user-guide/usbx-events/image206.png)

**Açıklama**

Bu olay bir USBX konak yığını arabirim örneği oluşturma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: arabirim.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-stack-interface-instance-delete"></a>Konak yığını arabirim örneği silme 

#### <a name="ux_host_stack_interface_instance_delete"></a>ux_host_stack_interface_instance_delete

**Simge** ![ Konak yığını arabirim örneği silme simgesi](./media/user-guide/usbx-events/image207.png)

**Açıklama**

Bu olay bir USBX konak yığını arabirim örneği silme olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: arabirim.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-stack-interface-set"></a>Konak yığını arabirim kümesi 

#### <a name="ux_host_stack_interface_set"></a>ux_host_stack_interface_set

**Simge** ![ Konak yığını arabirim kümesi simgesi](./media/user-guide/usbx-events/image208.png)

**Açıklama**

Bu olay bir USBX konak yığını arabirim kümesi olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: arabirim.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-stack-interface-setting-select"></a>Konak yığını arabirim ayarı seçimi 

#### <a name="ux_host_stack_interface_setting_select"></a>ux_host_stack_interface_setting_select

**Simge** ![ Konak yığın arabirimi ayarı seçme simgesi](./media/user-guide/usbx-events/image209.png)

**Açıklama**

Bu olay bir USBX konak yığın arabirimi ayarını seçme olayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: arabirim.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-stack-new-configuration-create"></a>Ana bilgisayar yığını yeni yapılandırma oluşturma 

#### <a name="ux_host_stack_new_configuration_create"></a>ux_host_stack_new_configuration_create

**Simge** ![ Konak yığını yeni yapılandırma Oluştur simgesi](./media/user-guide/usbx-events/image210.png)

**Açıklama**
 
Bu olay, bir USBX konak yığınını yeni yapılandırma oluşturma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: cihaz.
- Bilgi alanı 2: yapılandırma.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-stack-new-device-create"></a>Ana bilgisayar yığını yeni cihaz oluşturma 

#### <a name="ux_host_stack_new_device_create"></a>ux_host_stack_new_device_create

**Simge** ![ Konak yığını yeni cihaz Oluştur simgesi](./media/user-guide/usbx-events/image211.png)

**Açıklama**
 
 Bu olay bir USBX konak yığını yeni cihaz oluşturma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: HCD.
- Bilgi alanı 2: cihaz sahibi.
- Bilgi alanı 3: bağlantı noktası dizini.
- Bilgi alanı 4: cihaz.

### <a name="host-stack-new-endpoint-create"></a>Ana bilgisayar yığını yeni uç nokta oluşturma 

#### <a name="ux_host_stack_new_endpoint_create"></a>ux_host_stack_new_endpoint_create

**Simge** ![ Ana bilgisayar yığını yeni uç nokta Oluştur simgesi](./media/user-guide/usbx-events/image212.png)

**Açıklama**
 
Bu olay, bir USBX konak yığınını yeni bir uç nokta oluşturma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: arabirim.
- Bilgi alanı 2: uç nokta.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-stack-root-hub-change-process"></a>Konak yığını kök hub 'ı değişiklik Işlemi 

#### <a name="ux_host_stack_rh_change_process"></a>ux_host_stack_rh_change_process

**Simge** ![ Konak yığını kök hub 'ı değiştirme Işlemi simgesi](./media/user-guide/usbx-events/image213.png)

**Açıklama**
 
Bu olay bir USBX konak yığını kök hub 'ı değişiklik sürecini temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: bağlantı noktası dizini.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-stack-root-hub-device-extraction"></a>Konak yığını kök hub cihazı ayıklama 

#### <a name="ux_host_stack_rh_device_extraction"></a>ux_host_stack_rh_device_extraction

**Simge** ![ Konak yığını kök hub cihazı ayıklama simgesi](./media/user-guide/usbx-events/image214.png)

**Açıklama**

Bu olay bir USBX konak yığını kök hub cihazı ayıklama olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: HCD.
- Bilgi alanı 2: bağlantı noktası dizini.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-stack-root-hub-device-insertion"></a>Konak yığını kök hub cihazı ekleme 

#### <a name="ux_host_stack_rh_device_insertion"></a>ux_host_stack_rh_device_insertion

**Simge** ![ Konak yığını kök hub cihazı ekleme simgesi](./media/user-guide/usbx-events/image215.png)

**Açıklama**

Bu olay bir USBX konak yığını kök hub cihazı ekleme işlemini temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: HCD.
- Bilgi alanı 2: bağlantı noktası dizini.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-stack-transfer-request"></a>Konak yığını aktarım Isteği 

#### <a name="ux_host_stack_transfer_request"></a>ux_host_stack_transfer_request

**Simge** ![ Konak yığını aktarım Isteği simgesi](./media/user-guide/usbx-events/image216.png)

**Açıklama**

Bu olay bir USBX konak yığını aktarım Isteğini temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: cihaz.
- Bilgi alanı 2: uç nokta.
- Bilgi alanı 3: istek aktarma.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-stack-transfer-request-abort"></a>Konak yığını aktarım Isteği Iptali 

#### <a name="internal-io-driver-get-status"></a>İç g/ç sürücüsü Get durumu

**Simge** ![ Konak yığını aktarım Isteği Iptali simgesi](./media/user-guide/usbx-events/image217.png)

**Açıklama**

Bu olay bir USBX konak yığını aktarım Isteği Iptali 'ni temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: cihaz.
- Bilgi alanı 2: uç nokta.
- Bilgi alanı 3: istek aktarma.
- Bilgi alanı 4: kullanılmıyor.

### <a name="usbx-error"></a>USBX hatası 

#### <a name="ux_error"></a>ux_error

**Simge** ![ U S B X hata simgesi](./media/user-guide/usbx-events/image218.png)

**Açıklama**

Bu olay bir USBX hata olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: USBX hatası.
- Bilgi alanı 2: hata adı.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.