---
title: Bölüm 9-Azure RTOS USBX izleme olayları
description: Bu bölüm, TraceX tarafından görünen Azure RTOS USBX olaylarının bir açıklamasını içerir.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: 015e5feedd1d5e90c6491e156c2d0d57a9abaa47518868d375a34e618770d4aa
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116795408"
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
| ![cihaz sınıfı pima Depolama t gönder simgesi](./media/user-guide/usbx-events/image31.png)    | **cihaz sınıfı pima Depolama kimliği gönderme** *(ux_device_class_pima_storage_id_send)* |
| ![Device Class pima Depolama ınfo gönder simgesi](./media/user-guide/usbx-events/image32.png)    | **cihaz sınıfı pima Depolama bilgi gönderme** *(ux_device_class_pima_storage_info_send)* |
| ![Cihaz sınıfı R N D ı etkinleştirme simgesi](./media/user-guide/usbx-events/image33.png)    | **Cihaz sınıfı rndis etkinleştir** *(ux_device_class_rndis_activate)* |
| ![Cihaz sınıfı R N D ı devre dışı bırak simgesi](./media/user-guide/usbx-events/image34.png)    | **Cihaz sınıfı rndis devre dışı bırak** *(ux_device_class_rndis_deactivate)* |
| ![Cihaz sınıfı R N D ı Ileti Keep Aliveicon](./media/user-guide/usbx-events/image35.png)    | **Cihaz sınıfı rndis Iletisi canlı tut** *(ux_device_class_rndis_msg_keep_alive)* |
| ![Cihaz sınıfı R N D ı Ileti sorgu simgesi](./media/user-guide/usbx-events/image36.png)    | **Cihaz sınıfı rndis Ileti sorgusu** *(ux_device_class_rndis_msg_query)* |
| ![Cihaz sınıfı R N D ı Ileti sıfırlama simgesi](./media/user-guide/usbx-events/image37.png)    | **Cihaz sınıfı rndis Ileti sıfırlama** *(ux_device_class_rndis_msg_reset)* |
| ![Cihaz sınıfı R N D ı Ileti kümesi simgesi](./media/user-guide/usbx-events/image38.png)    | **Cihaz sınıfı rndis Ileti kümesi** *(ux_device_class_rndis_msg_set)* |
| ![Cihaz sınıfı R N D ı paket alma simgesi](./media/user-guide/usbx-events/image39.png)    | **Cihaz sınıfı rndis paket alma** *(ux_device_class_rndis_packet_receive)* |
| ![Cihaz sınıfı R N D ı paket Iletme simgesi](./media/user-guide/usbx-events/image40.png)    | **Cihaz sınıfı rndis paket iletimi** *(ux_device_class_rndis_packet_transmit)* |
| ![cihaz sınıfı Depolama etkinleştirme simgesi](./media/user-guide/usbx-events/image41.png)    | **cihaz sınıfı Depolama etkinleştir** *(ux_device_class_storage_activate)* |
| ![cihaz sınıfı Depolama devre dışı bırakma simgesi](./media/user-guide/usbx-events/image42.png)    | **cihaz sınıfı Depolama devre dışı bırak** *(ux_device_class_storage_deactivate)* |
| ![cihaz sınıfı Depolama biçim simgesi](./media/user-guide/usbx-events/image43.png)    | **cihaz sınıfı Depolama biçimi** *(ux_device_class_storage_format)* |
| ![cihaz sınıfı Depolama sorgulama simgesi](./media/user-guide/usbx-events/image44.png)    | **cihaz sınıfı Depolama sorgulama** *(ux_device_class_storage_inquiry)* |
| ![cihaz sınıfı Depolama modu seçme simgesi](./media/user-guide/usbx-events/image45.png)    | **cihaz sınıfı Depolama modu seçme** *(ux_device_class_storage_mode_select)* |
| ![cihaz sınıfı Depolama modu algılama simgesi](./media/user-guide/usbx-events/image46.png)    | **cihaz sınıfı Depolama modu algılama** *(ux_device_class_storage_mode_sense)* |
| ![Cihaz Sınıfı Depolama Medya Kaldırmaya İzin Ver simgesini engelle](./media/user-guide/usbx-events/image47.png)    | **Cihaz Sınıfı Depolama Medya Kaldırmaya İzin Ver** *(ux_device_class_storage_prevent_allow_media_removal)* |
| ![Cihaz Sınıfı Depolama Okuma simgesi](./media/user-guide/usbx-events/image48.png)    | **Cihaz Sınıfı Depolama Okuma** *(ux_device_class_storage_read)* |
| ![Cihaz Sınıfı Depolama Okuma Kapasitesi simgesi](./media/user-guide/usbx-events/image49.png)    | **Cihaz Sınıfı Depolama Okuma Kapasitesi** *(ux_device_class_storage_read_capacity)* |
| ![Cihaz Sınıfı Depolama Okuma Biçimi Kapasitesi simgesi](./media/user-guide/usbx-events/image50.png)    | **Cihaz Sınıfı Depolama Okuma Biçimi Kapasitesi** *(ux_device_class_storage_read_format_capacity)* |
| ![Cihaz Sınıfı Depolama Okuma ToC simgesi](./media/user-guide/usbx-events/image51.png)    | **Device Class Depolama Read TOC** *(ux_device_class_storage_read_toc)* |
| ![Device Class Depolama Request Sense simgesi](./media/user-guide/usbx-events/image52.png)    | **Device Class Depolama Request Sense** *(ux_device_class_storage_request_sense)* |
| ![Cihaz Sınıfı Depolama Başlat Durdurma simgesi](./media/user-guide/usbx-events/image53.png)    | **Cihaz Sınıfı Depolama Başlatma Durdurma** *(ux_device_class_storage_start_stop)* |
| ![Cihaz Sınıfı Depolama Teste Hazır simgesi](./media/user-guide/usbx-events/image54.png)    | **Cihaz Sınıfı Depolama Test Hazır** *(ux_device_class_storage_test_ready)* |
| ![Cihaz Sınıfı Depolama Doğrulama simgesi](./media/user-guide/usbx-events/image55.png)    | **Cihaz Sınıfı Depolama Doğrulama** *(ux_device_class_storage_verify)* |
| ![Cihaz Sınıfı Depolama Yazma simgesi](./media/user-guide/usbx-events/image56.png)    | **Cihaz Sınıfı Depolama Yazma** *(ux_device_class_storage_write)* |
| ![Cihaz Yığını Alternatif Ayar Al simgesi](./media/user-guide/usbx-events/image57.png)    | **Cihaz Yığını Alternatif Ayar Al** *(ux_device_stack_alternate_setting_get)* |
| ![Cihaz Yığını Alternatif Ayar Kümesi simgesi](./media/user-guide/usbx-events/image58.png)    | **Cihaz Yığını Alternatif Ayar Kümesi** *(ux_device_stack_alternate_setting_set)* |
| ![Cihaz Yığını Sınıf Kaydı simgesi](./media/user-guide/usbx-events/image59.png)    | **Cihaz Yığını Sınıf Kaydı** *(ux_device_stack_class_register)* |
| ![Cihaz Yığını Temizleme Özelliği simgesi](./media/user-guide/usbx-events/image60.png)    | **Cihaz Yığını Temizleme Özelliği** *(ux_device_stack_clear_feature)* |
| ![Cihaz Yığını Yapılandırması Al simgesi](./media/user-guide/usbx-events/image61.png)    | **Cihaz Yığını Yapılandırma Get** *(ux_device_stack_configuration_get)* |
| ![Cihaz Yığını Yapılandırma Kümesi simgesi](./media/user-guide/usbx-events/image62.png)    | **Cihaz Yığını Yapılandırma Kümesi** *(ux_device_stack_configuration_set)* |
| ![Cihaz Yığını Bağlan simgesi](./media/user-guide/usbx-events/image63.png)    | **Cihaz Yığını Bağlan** *(ux_device_stack_connect)* |
| ![Cihaz Yığını Tanımlayıcısı Gönder simgesi](./media/user-guide/usbx-events/image64.png)    | **Cihaz Yığını Tanımlayıcı Gönderme** *(ux_device_stack_descriptor_send)* |
| ![Cihaz Yığını Bağlantısını Kes simgesi](./media/user-guide/usbx-events/image65.png)    | **Cihaz Yığını Bağlantısını Kesme** *(ux_device_stack_disconnect)* |
| ![Cihaz Yığını Uç Noktası Durak simgesi](./media/user-guide/usbx-events/image66.png)    | **Cihaz Yığını Uç Noktası Durak** *(ux_device_stack_endpoint_stall)* |
| ![Cihaz Yığını Durum Al simgesi](./media/user-guide/usbx-events/image67.png)    | **Cihaz Yığını Durum Al** *(ux_device_stack_get_status)* |
| ![Cihaz Yığını Konak Uyandırma simgesi](./media/user-guide/usbx-events/image68.png)    | **Cihaz Yığını Ana Bilgisayarı Uyandırma** *(ux_device_stack_host_wakeup)* |
| ![Cihaz Yığını Başlat simgesi](./media/user-guide/usbx-events/image69.png)    | **Cihaz Yığını Başlatma** *(ux_device_stack_initialize)* |
| ![Cihaz Yığını Arabirimi Silme simgesi](./media/user-guide/usbx-events/image70.png)    | **Cihaz Yığını Arabirimi Silme** *(ux_device_stack_interface_delete)* |
| ![Cihaz Yığını Arabirimi Al simgesi](./media/user-guide/usbx-events/image71.png)    | **Cihaz Yığını Arabirimi Al** *(ux_device_stack_interface_get)* |
| ![Cihaz Yığını Arabirim Kümesi simgesi](./media/user-guide/usbx-events/image72.png)    | **Cihaz Yığını Arabirim Kümesi** *(ux_device_stack_interface_set)* |
| ![Cihaz Yığın Kümesi Özellik simgesi](./media/user-guide/usbx-events/image73.png)    | **Cihaz Yığın Kümesi Özelliği** *(ux_device_stack_set_feature)* |
| ![Cihaz Yığını Aktarım Durdurma simgesi](./media/user-guide/usbx-events/image74.png)    | **Cihaz Yığını Aktarım Durdurma** *(ux_device_stack_transfer_abort)* |
| ![*Cihaz Yığını Aktarımı Tüm İstek durdurma simgesi](./media/user-guide/usbx-events/image75.png)    | **Cihaz Yığını Aktarımı Tüm İstek Durdurma** *(ux_device_stack_transfer_all_request_abort)* |
| ![Cihaz Yığını Aktarım İsteği simgesi](./media/user-guide/usbx-events/image76.png)    | **Cihaz Yığını Aktarım İsteği** *(ux_device_stack_transfer_request)* |
| ![Konak Sınıfı Asix Etkinleştirme simgesi](./media/user-guide/usbx-events/image77.png)    | **Konak Sınıfı Asix Etkinleştirmesi** *(ux_host_class_asix_activate)* |
| ![Konak Sınıfı Asix Devre Dışı Bırak simgesi](./media/user-guide/usbx-events/image78.png)    | **Konak Sınıfı Asix Devre Dışı Bırakma** *(ux_host_class_asix_deactivate)* |
| ![Konak Sınıfı Ek Kesme Bildirimi simgesi](./media/user-guide/usbx-events/image79.png)    | **Konak Sınıfı Asix Kesme Bildirimi** *(ux_host_class_asix_interrupt_notification)* |
| ![Konak Sınıfı Ek Okuma simgesi](./media/user-guide/usbx-events/image80.png)    | **Konak Sınıfı Asix Okuma** *(ux_host_class_asix_read)* |
| ![Konak Sınıfı Asix Yazma simgesi](./media/user-guide/usbx-events/image81.png)    | **Konak Sınıfı Asix Yazma** *(ux_host_class_asix_write)* |
| ![Konak Sınıfı Ses Etkinleştirme simgesi](./media/user-guide/usbx-events/image82.png)    | **Konak Sınıfı Ses Etkinleştirme** *(ux_host_class_audio_activate)* |
| ![Konak Sınıfı Ses Denetimi Değeri Al simgesi](./media/user-guide/usbx-events/image83.png)    | **Konak Sınıfı Ses Denetimi Değer Al** *(ux_host_class_audio_control_value_get)* |
| ![Konak Sınıfı Ses Denetimi Değer Kümesi simgesi](./media/user-guide/usbx-events/image84.png)    | **Konak Sınıfı Ses Denetimi Değer Kümesi** *(ux_host_class_audio_control_value_set)* |
| ![Konak Sınıfı Ses Devre Dışı Bırak simgesi](./media/user-guide/usbx-events/image85.png)    | **Konak Sınıfı Ses Devre Dışı Bırakma** *(ux_host_class_audio_deactivate)* |
| ![Konak Sınıfı Ses Okuma simgesi](./media/user-guide/usbx-events/image86.png)    | **Konak Sınıfı Ses Okuma** *(ux_host_class_audio_read)* |
| ![Konak Sınıfı Ses Akışı Örnekleme Alma simgesi](./media/user-guide/usbx-events/image87.png)    | **Konak Sınıfı Ses Akışı Örnekleme Alma** *(ux_host_class_audio_streaming_sampling_get)* |
| ![Konak Sınıfı Ses Akışı Örnekleme Kümesi simgesi](./media/user-guide/usbx-events/image88.png)    | **Konak Sınıfı Ses Akışı Örnekleme Kümesi** *(ux_host_class_audio_streaming_sampling_set)* |
| ![Konak Sınıfı Ses Yazma simgesi](./media/user-guide/usbx-events/image89.png)    | **Konak Sınıfı Ses Yazma** *(ux_host_class_audio_write)* |
| ![Konak Sınıfı C D C A C M Etkinleştirme simgesi](./media/user-guide/usbx-events/image90.png)    | **Konak Sınıfı Cdc Acm Etkinleştirme** *(ux_host_class_cdc_acm_activate)* |
| ![Konak Sınıfı C D C A C M Devre Dışı Bırak simgesi](./media/user-guide/usbx-events/image91.png)    | **Konak Sınıfı Cdc Acm Devre Dışı Bırakma** *(ux_host_class_cdc_acm_deactivate)* |
| ![Kanalda Konak Sınıfı C D C A C M O C T L simgesi](./media/user-guide/usbx-events/image92.png)    | **Kanalda Konak Sınıfı Cdc Acm Ioctl Abort** *(ux_host_class_cdc_acm_ioctl_abort_in_pipe)* |
| ![Konak Sınıfı C D C A C M O C T L Kanaldan Çıkma simgesini durdurma](./media/user-guide/usbx-events/image93.png)    | **Konak Sınıfı Cdc Acm Ioctl Kanal Durdurma** *(ux_host_class_cdc_acm_ioctl_abort_out_pipe)* |
| ![Konak Sınıfı C D C A C M O C T L Cihaz Durumunu Al simgesi](./media/user-guide/usbx-events/image94.png)    | **Konak Sınıfı Cdc Acm Ioctl Cihaz Durumunu Al** *(ux_host_class_cdc_acm_ioctl_get_device_status)* |
| ![Konak Sınıfı C D C A C M O C T L Satır Kodlaması Al simgesi](./media/user-guide/usbx-events/image95.png)    | **Konak Sınıfı Cdc Acm Ioctl Satır Kodlaması Al** *(ux_host_class_cdc_acm_ioctl_get_line_coding)* |
| ![Konak Sınıfı C D C A C M O C T L Bildirim Geri Çağırma simgesi](./media/user-guide/usbx-events/image96.png)    | **Konak Sınıfı Cdc Acm Ioctl Bildirim Geri Çağırma** *(ux_host_class_cdc_acm_ioctl_notification_callback)* |
| ![Konak Sınıfı C D C A C M O C T L Kesme Gönder simgesi](./media/user-guide/usbx-events/image97.png)    | **Konak Sınıfı Cdc Acm Ioctl Send Break** *(ux_host_class_cdc_acm_ioctl_send_break)* |
| ![Konak Sınıfı C D C A C M O C T L Set Line Coding simgesi](./media/user-guide/usbx-events/image98.png)    | **Konak Sınıfı Cdc Acm Ioctl Set Line Coding** *(ux_host_class_cdc_acm_ioctl_set_line_coding)* |
| ![Konak Sınıfı C D C A C M O C T L Satır Durumunu Ayarla simgesi](./media/user-guide/usbx-events/image99.png)    | **Konak Sınıfı Cdc Acm Ioctl Set Line State** *(ux_host_class_cdc_acm_ioctl_set_line_state)* |
| ![Konak Sınıfı C D C A C M Okuma simgesi](./media/user-guide/usbx-events/image100.png)    | **Konak Sınıfı Cdc Acm Read** *(ux_host_class_cdc_acm_read)* |
| ![Konak Sınıfı C D C A C M Sinyal Başlatma simgesi](./media/user-guide/usbx-events/image101.png)    | **Konak Sınıfı Cdc Acm Sinyal Başlatma** *(ux_host_class_cdc_acm_reception_start)* |
| ![Konak Sınıfı C D C A C M Sinyal Durdurma simgesi](./media/user-guide/usbx-events/image102.png)    | **Konak Sınıfı Cdc Acm Sinyal Durdurma** *(ux_host_class_cdc_acm_reception_stop)* |
| ![Konak Sınıfı C D C A C M Yazma simgesi](./media/user-guide/usbx-events/image103.png)    | **Konak Sınıfı Cdc Acm Yazma** *(ux_host_class_cdc_acm_write)* |
| ![Konak Sınıfı Dpump Etkinleştirme simgesi](./media/user-guide/usbx-events/image104.png)    | **Konak Sınıfı Dpump Etkinleştirmesi** *(ux_host_class_dpump_activate)* |
| ![Konak Sınıfı Dpump Devre Dışı Bırak simgesi](./media/user-guide/usbx-events/image105.png)    | **Konak Sınıfı Dpump Devre Dışı Bırakma** *(ux_host_class_dpump_deactivate)* |
| ![Konak Sınıfı Dpump Okuma simgesi](./media/user-guide/usbx-events/image106.png)    | **Konak Sınıfı Dpump Okuma** *(ux_host_class_dpump_read)* |
| ![Konak Sınıfı Dpump Yazma simgesi](./media/user-guide/usbx-events/image107.png)    | **Konak Sınıfı Dpump Yazma** *(ux_host_class_dpump_write)* |
| ![Konak Sınıfı Etkinleştir simgesi](./media/user-guide/usbx-events/image108.png)    | **Host Classını Etkinleştirme** *(ux_host_class_hid_activate)* |
| ![Konak SınıfıNız İstemci Kaydı simgesi](./media/user-guide/usbx-events/image109.png)    | **Konak Sınıfı Gizli İstemci Kaydı** *(ux_host_class_hid_client_register)* |
| ![Konak Sınıfı Devre Dışı Bırak simgesi](./media/user-guide/usbx-events/image110.png)    | **Konak Sınıfı Devre Dışı Bırakma** *(ux_host_class_hid_deactivate)* |
| ![Host Class Idle Get simgesi](./media/user-guide/usbx-events/image111.png)    | **Host Class Idle Get** *(ux_host_class_hid_idle_get)* |
| ![Konak Sınıfı Boşta Kalma Kümesi simgesi](./media/user-guide/usbx-events/image112.png)    | **Host Class Idle Set** *(ux_host_class_hid_idle_set)* |
| ![Konak Sınıfı Klavye Etkinleştirme simgesi](./media/user-guide/usbx-events/image113.png)    | **Host ClassNizi Klavye Etkinleştirme** *(ux_host_class_hid_keyboard_activate)* |
| ![Konak Sınıfı Klavyeyi Devre Dışı Bırak simgesi](./media/user-guide/usbx-events/image114.png)    | **Konak Sınıfı Klavyeyi Devre Dışı Bırakma** *(ux_host_class_hid_keyboard_deactivate)* |
| ![Konak Sınıfı Fare Etkinleştirme simgesi](./media/user-guide/usbx-events/image115.png)    | **Host Class Mouse Activate** *(ux_host_class_hid_mouse_activate)* |
| ![Konak Sınıfı Fare Devre Dışı Bırak simgesi](./media/user-guide/usbx-events/image116.png)    | **Konak Sınıfı FareYi Devre Dışı Bırakma** *(ux_host_class_hid_mouse_deactivate)* |
| ![Konak Sınıfı Uzaktan Denetim Etkinleştirme simgesi](./media/user-guide/usbx-events/image117.png)    | **Konak Sınıfı Remote Control Etkinleştirme** *(ux_host_class_hid_remote_control_activate)* |
| ![Konak Sınıfı Remote Control Devre Dışı Bırak simgesi](./media/user-guide/usbx-events/image118.png)    | **Konak Sınıfı Remote Control'u Devre Dışı Bırakma** *(ux_host_class_hid_remote_control_deactivate)* |
| ![Konak Sınıfı Gizli Rapor Al simgesi](./media/user-guide/usbx-events/image119.png)    | **Host Classını Rapor Al** *(ux_host_class_hid_report_get)* |
| ![Konak Sınıfıınır Rapor Kümesi simgesi](./media/user-guide/usbx-events/image120.png)    | **Host Classınıd Rapor Kümesi** *(ux_host_class_hid_report_set)* |
| ![Konak Sınıfı Hub'ı Etkinleştirme simgesi](./media/user-guide/usbx-events/image121.png)    | **Konak Sınıfı Hub'ı Etkinleştirme** *(ux_host_class_hub_activate)* |
| ![Konak Sınıfı Hub'ı Değişiklik Algılama simgesi](./media/user-guide/usbx-events/image122.png)    | **Konak Sınıfı Hub'ı Değişiklik Algılama** *(ux_host_class_hub_change_detect)* |
| ![*Konak Sınıfı Hub'ı Devre Dışı Bırak simgesi](./media/user-guide/usbx-events/image123.png)    | **Konak Sınıfı Hub'ı Devre Dışı** *Bırakma (ux_host_class_hub_deactivate)* |
| ![Konak Sınıfı Hub'ı Bağlantı Noktası Değiştirme Bağlantı Süreci simgesi](./media/user-guide/usbx-events/image124.png)    | **Konak Sınıfı Hub'ı Bağlantı Noktası Değiştirme Bağlantı Ux_host_class_hub_port_change_connection_process)**  |
| ![Konak Sınıfı Hub'ı Bağlantı Noktası Değişikliği işlemi etkinleştir simgesi](./media/user-guide/usbx-events/image125.png)    | **Konak Sınıfı Hub'ı Bağlantı Noktası Değişikliği etkinleştirme işlemi** *(ux_host_class_hub_port_change_enable_process)* |
| ![Konak Sınıfı Hub'ı Geçerli İşlem Üzerinden Bağlantı Noktası Değişikliği simgesi](./media/user-guide/usbx-events/image126.png)    | **Geçerli İşlem Üzerinden Konak Sınıfı Hub'ı** Bağlantı Noktası Değişikliği *(ux_host_class_hub_port_change_over_current_process)* |
| ![Konak Sınıfı Hub'ı Bağlantı Noktası Değiştirme Sıfırlama süreci simgesi](./media/user-guide/usbx-events/image127.png)    | **Konak Sınıfı Hub'ı Bağlantı Noktası Değiştirme Sıfırlama işlemi** *(ux_host_class_hub_port_change_reset_process)* |
| ![Konak Sınıfı Hub'ı Bağlantı Noktası Değişikliği İşlem Askıya Alma simgesi](./media/user-guide/usbx-events/image128.png)    | **Konak Sınıfı Hub'ı Bağlantı Noktası Değişikliği Askıya Alma işlemi** *(ux_host_class_hub_port_change_suspend_process)* |
| ![Konak Sınıfı Pima Etkinleştirme simgesi](./media/user-guide/usbx-events/image129.png)    | **Pima Etkinleştirme Konak Sınıfı** *(ux_host_class_prima_activate)* |
| ![Konak Sınıfı Pima Devre Dışı Bırak simgesi](./media/user-guide/usbx-events/image130.png)    | **Konak Sınıfı Pima Devre Dışı Bırakma** *(ux_host_class_pima_deactivate)* |
| ![Konak Sınıfı Pima Cihaz Bilgileri Al simgesi](./media/user-guide/usbx-events/image131.png)    | **Konak Sınıfı Pima Cihaz Bilgileri Al** *(ux_host_class_pima_device_info_get)* |
| ![Konak Sınıfı Pima Cihaz Sıfırlama simgesi](./media/user-guide/usbx-events/image132.png)    | **Konak Sınıfı Pima Cihaz Sıfırlama** *(ux_host_class_pima_device_reset)* |
| ![Konak Sınıfı Pima Bildirimi simgesi](./media/user-guide/usbx-events/image133.png)    | **Konak Sınıfı Pima Bildirimi** *(ux_host_class_pima_notification)* |
| ![Konak Sınıfı Pima Numarası Nesneleri Al simgesi](./media/user-guide/usbx-events/image134.png)    | **Konak Sınıfı Pima Sayı NesneleriNin Al** *(ux_host_class_pima_num_objects_get)* |
| ![Konak Sınıfı Pima Nesnesi Kapatma simgesi](./media/user-guide/usbx-events/image135.png)    | **Konak Sınıfı Pima Nesnesi Kapatma** *(ux_host_class_pima_object_close)* |
| ![Konak Sınıfı Pima Nesne Kopyalama simgesi](./media/user-guide/usbx-events/image136.png)    | **Konak Sınıfı Pima Nesne Kopyalama** *(ux_host_class_pima_object_copy)* |
| ![Konak Sınıfı Pima Nesne Silme simgesi](./media/user-guide/usbx-events/image137.png)    | **Konak Sınıfı Pima Nesne Silme** *(ux_host_class_pima_object_delete)* |
| ![Konak Sınıfı Pima Nesnesi Al simgesi](./media/user-guide/usbx-events/image138.png)    | **Konak Sınıfı Pima Nesne Al** *(ux_host_class_pima_object_get)* |
| ![Konak Sınıfı Pima Nesne Bilgileri Al simgesi](./media/user-guide/usbx-events/image139.png)    | **Konak Sınıfı Pima Nesne Bilgisi Al** *(ux_host_class_pima_object_info_get)* |
| ![Konak Sınıfı Pima Nesne Bilgisi Gönderme simgesi](./media/user-guide/usbx-events/image140.png)    | **Konak Sınıfı Pima Nesne Bilgisi Gönderme** *(ux_host_class_pima_object_info_send)* |
| ![Konak Sınıfı Pima Nesnesi Taşıma simgesi](./media/user-guide/usbx-events/image141.png)    | **Konak Sınıfı Pima Nesne Taşıma** *(ux_host_class_pima_object_move)* |
| ![Konak Sınıfı Pima Nesne Gönderme simgesi](./media/user-guide/usbx-events/image142.png)    | **Konak Sınıfı Pima Nesne Gönderme** *(ux_host_class_pima_object_send)* |
| ![Konak Sınıfı Pima Nesne Aktarımı Durdurma simgesi](./media/user-guide/usbx-events/image143.png)    | **Konak Sınıfı Pima Nesne Aktarımı Durdurma** *(ux_host_class_object_transfer_abort)* |
| ![Konak Sınıfı Pima Okuma simgesi](./media/user-guide/usbx-events/image144.png)    | **Konak Sınıfı Pima Read** *(ux_host_class_pima_read)* |
| ![Konak Sınıfı Pima İsteği İptal simgesi](./media/user-guide/usbx-events/image145.png)    | **Konak Sınıfı Pima İstek İptali** *(ux_host_class_pima_request_cancel)* |
| ![Konak Sınıfı Pima Oturumu Kapat simgesi](./media/user-guide/usbx-events/image146.png)    | **Konak Sınıfı Pima Oturumu Kapatma** *(ux_host_class_pima_session_close)* |
| ![Konak Sınıfı Pima Oturumu Aç simgesi](./media/user-guide/usbx-events/image147.png)    | **Konak Sınıfı Pima Oturumu Açık** *(ux_host_class_pima_session_open)* |
| ![Konak Sınıfı Pima Depolama Kimlikleri Al simgesi](./media/user-guide/usbx-events/image148.png)    | **Konak Sınıfı Pima Depolama Kimlikleri Al** *(ux_host_class_pima_storage_ids_get)* |
| ![Konak Sınıfı Pima Depolama Bilgi Al simgesi](./media/user-guide/usbx-events/image149.png)    | **Konak Sınıfı Pima Depolama Bilgi Al** *(ux_host_class_pima_storage_info_get)* |
| ![Konak Sınıfı Pima Parmak Al simgesi](./media/user-guide/usbx-events/image150.png)    | **Konak Sınıfı Pima Thumb Get** *(ux_host_class_pima_thumb_get)* |
| ![Konak Sınıfı Pima Yazma simgesi](./media/user-guide/usbx-events/image151.png)    | **Konak Sınıfı Pima Yazma** *(ux_host_class_pima_write)* |
| ![Konak Sınıfı Yazıcı Etkinleştirme simgesi](./media/user-guide/usbx-events/image152.png)    | **Konak Sınıfı Yazıcı Etkinleştirme** *(ux_host_class_printer_activate)* |
| ![Konak Sınıfı Yazıcı devre dışı bırak simgesi](./media/user-guide/usbx-events/image153.png)    | **Konak Sınıfı Yazıcıyı Devre Dışı Bırakma** *(ux_host_class_printer_deactivate)* |
| ![Konak Sınıfı Yazıcı Adı Al simgesi](./media/user-guide/usbx-events/image154.png)    | **Konak Sınıfı Yazıcı Adı Al** *(ux_host_class_printer_name_get)* |
| ![Konak Sınıfı Yazıcı Okuma simgesi](./media/user-guide/usbx-events/image155.png)    |  **Konak Sınıfı Yazıcı Okuma** *(ux_host_class_printer_read)* |
| ![Konak Sınıfı YazıcıSı Yazılım Sıfırlama simgesi](./media/user-guide/usbx-events/image156.png)    | **Konak Sınıfı YazıcıSı Yazılım Sıfırlaması** *(ux_host_class_printer_soft_reset)* |
| ![Konak Sınıfı Yazıcı Durumu Al simgesi](./media/user-guide/usbx-events/image157.png)    | **Konak Sınıfı Yazıcı Durumu Al** *(ux_host_class_printer_status_get)* |
| ![Konak Sınıfı Yazıcı Yazma simgesi](./media/user-guide/usbx-events/image158.png)    | **Konak Sınıfı Yazıcı Yazma** *(ux_host_class_printer_write)* |
| ![Konak Sınıfı Üretken Etkinleştirme simgesi](./media/user-guide/usbx-events/image159.png)    | **Konak Sınıfı Üretken Etkinleştirme** *(ux_host_class_prolific_activate)* |
| ![Konak Sınıfı Prolific Devre Dışı Bırak simgesi](./media/user-guide/usbx-events/image160.png)    | **Konak Sınıfı Prolific Devre Dışı Bırakma** *(ux_host_class_prolific_deactivate)* |
| ![Kanalda Konak Sınıfı Prolific I O C T L Durdurma simgesi](./media/user-guide/usbx-events/image161.png)    | **Kanalda Konak Sınıfı Prolific Ioctl Abort** *(ux_host_class_prolific_ioctl_abort_in_pipe)* |
| ![Host Class Prolific I O C T L Abort Out Pipe simgesi](./media/user-guide/usbx-events/image162.png)    | **Konak Sınıfı Prolific Ioctl Abort Out Pipe** *(ux_host_class_prolific_ioctl_abort_out_pipe)* |
| ![Konak Sınıfı Prolific I O C T L Cihaz Durumunu Al simgesi](./media/user-guide/usbx-events/image163.png)    | **Konak Sınıfı Prolific Ioctl Cihaz Durumunu Al** *(ux_host_class_prolific_ioctl_get_device_status)* |
| ![Konak Sınıfı Prolific I O C T L Satır Kodlaması Al simgesi](./media/user-guide/usbx-events/image164.png)    | **Konak Sınıfı Prolific Ioctl Satır Kodlaması Al** *(ux_host_class_prolific_ioctl_get_line_coding)* |
| ![Konak Sınıfı Prolific I O C T L Temizleme simgesi](./media/user-guide/usbx-events/image165.png)    | **Konak Sınıfı Prolific Ioctl Purge** *(ux_host_class_prolific_ioctl_purge)* |
| ![Konak Sınıfı Prolific I O C T L Rapor Cihaz Durumu Değişikliği simgesi](./media/user-guide/usbx-events/image166.png)    | **Konak Sınıfı Prolific Ioctl Rapor Cihaz Durumu Değişikliği** *(ux_host_class_prolific_ioctl_report_device_status_change)* |
| ![Konak Sınıfı Prolific I O C T L Kesme Gönder simgesi](./media/user-guide/usbx-events/image167.png)    | **Konak Sınıfı Prolific Ioctl Send Break** *(ux_host_class_prolific_ioctl_send_break)* |
| ![Konak Sınıfı Prolific I O C T L Set Line Coding simgesi](./media/user-guide/usbx-events/image168.png)    | **Konak Sınıfı Prolific Ioctl Set Line Coding** *(ux_host_class_prolific_ioctl_set_line_coding)* |
| ![Konak Sınıfı Prolific I O C T L Set Line State simgesi](./media/user-guide/usbx-events/image169.png)    | **Konak Sınıfı Prolific Ioctl Set Line State** *(ux_host_class_prolific_ioctl_set_line_state)* |
| ![Konak Sınıfı Üretken Okuma simgesi](./media/user-guide/usbx-events/image170.png)    | **Konak Sınıfı Prolific Read** *(ux_host_class_prolific_read)* |
| ![Konak Sınıfı Prolific Sinyal Başlatma simgesi](./media/user-guide/usbx-events/image171.png)    | **Konak Sınıfı Prolific Sinyal Başlatma** *(ux_host_class_prolific_reception_start)* |
| ![Konak Sınıfı Üretken Sinyal Durdurma simgesi](./media/user-guide/usbx-events/image172.png)    | **Konak Sınıfı Üretken Sinyal Durdurma (ux_host_class_prolific_reception_stop)**  |
| ![Konak Sınıfı Üretken Yazma simgesi](./media/user-guide/usbx-events/image173.png)    | **Konak Sınıfı Üretken Yazma** *(ux_host_class_prolific_write)* |
| ![Konak Sınıfı Depolama Etkinleştir simgesi](./media/user-guide/usbx-events/image174.png)    | **Konak Sınıfı Depolama Etkinleştirme** *(ux_host_class_storage_activate)* |
| ![Konak Sınıfı Depolama Devre Dışı Bırak simgesi](./media/user-guide/usbx-events/image175.png)    | **Konak Sınıfı Depolama Devre Dışı Bırakma** (*ux_host_class_storage_deactivate)* |
| ![Konak Sınıfı Depolama Medya Kapasitesi Al simgesi](./media/user-guide/usbx-events/image176.png)    | **Konak Sınıfı Depolama Medya Kapasitesi Al** *(ux_host_class_storage_media_capacity_get)* |
| ![Konak Sınıfı Depolama Medya Biçimi Kapasitesi Al simgesi](./media/user-guide/usbx-events/image177.png)    | **Konak Sınıfı Depolama Medya Biçimi Kapasitesi Al** *(ux_host_class_storage_media_format_capacity_get)* |
| ![Konak Sınıfı Depolama Medya Bağlama simgesi](./media/user-guide/usbx-events/image178.png)    | **Konak Sınıfı Depolama Medya Bağlama** (ux_host_class_storage_media_mount)* |
| ![Konak Sınıfı Depolama Medya Aç simgesi](./media/user-guide/usbx-events/image179.png)    | **Host Class Depolama Media Open** *(ux_host_class_storage_media_open)* |
| ![Konak Sınıfı Depolama Medya Okuma simgesi](./media/user-guide/usbx-events/image180.png)    | **Konak Sınıfı Depolama Medya Okuma** *(ux_host_class_storage_media_read)* |
| ![Konak Sınıfı Depolama Medya Yazma simgesi](./media/user-guide/usbx-events/image181.png)    | **Konak Sınıfı Depolama Medya Yazma** *(ux_host_class_storage_media_write)* |
| ![Konak Sınıfı Depolama İstek Algısı simgesi](./media/user-guide/usbx-events/image182.png)    | **İstek Depolama Konak Sınıfı** *(ux_host_class_storage_request_sense)* |
| ![Konak Sınıfı Depolama Başlat Durdurma simgesi](./media/user-guide/usbx-events/image183.png)    | **Konak Sınıfı Depolama Başlatma Durdurma** *(ux_host_class_storage_start_stop)* |
| ![Konak Sınıfı Depolama Birim Hazır Test simgesi](./media/user-guide/usbx-events/image184.png)    | **Konak Sınıfı Depolama Birim Hazır Testi** *(ux_host_class_storage_activate)* |
| ![Konak Yığını Sınıf Örneği Oluştur simgesi](./media/user-guide/usbx-events/image185.png)    | **Konak Yığını Sınıf Örneği Oluşturma** *(ux_host_stack_class_instance_create)* |
| ![Konak Yığını Sınıf Örneği Yok Etme simgesi](./media/user-guide/usbx-events/image186.png)    | **Konak Yığını Sınıf Örneği Yok Etme** *(ux_host_stack_class_instance_destroy)* |
| ![Konak Yığını Yapılandırması Silme simgesi](./media/user-guide/usbx-events/image187.png)    | **Konak Yığını Yapılandırma Silme** *(ux_host_stack_configuration_delete)* |
| ![Konak Yığını Yapılandırması Numarala simgesi](./media/user-guide/usbx-events/image188.png)    | **Konak Yığını Yapılandırma Numarala** *(ux_host_stack_configuration_enumerate)* |
| ![Konak Yığını Yapılandırma Örneği Oluşturma simgesi](./media/user-guide/usbx-events/image189.png)    | **Konak Yığını Yapılandırma Örneği Oluşturma** *(ux_host_stack_configuration_instance_create)* |
| ![Konak Yığını Yapılandırma Örneği Silme simgesi](./media/user-guide/usbx-events/image190.png)    | **Konak Yığını Yapılandırma Örneği Silme** *(ux_host_stack_configuration_instance_delete)* |
| ![Konak Yığını Yapılandırma Kümesi simgesi](./media/user-guide/usbx-events/image191.png)    | **Konak Yığını Yapılandırma Kümesi** *(ux_host_stack_configuration_set)* |
| ![Konak Yığını Cihaz Adres Kümesi simgesi](./media/user-guide/usbx-events/image192.png)    | **Konak Yığını Cihaz Adres Kümesi** *(ux_host_stack_device_set)* |
| ![Konak Yığını Cihaz Yapılandırması Al simgesi](./media/user-guide/usbx-events/image193.png)    | **Konak Yığını Cihaz Yapılandırma Get** *(ux_host_stack_device_configuration_get)* |
| ![Konak Yığını Cihaz Yapılandırması Seç simgesi](./media/user-guide/usbx-events/image194.png)    | **Konak Yığını Cihaz Yapılandırması Seçme** *(ux_host_stack_device_configuration_select)* |
| ![Konak Yığını Cihaz Tanımlayıcısı Okuma simgesi](./media/user-guide/usbx-events/image195.png)    | **Konak Yığını Cihaz Tanımlayıcısı Okuma** *(ux_host_stack_device_descriptor_read)* |
| ![Konak Yığını Cihazı Al simgesi](./media/user-guide/usbx-events/image196.png)    | **Konak Yığını Cihaz Al** (ux_host_stack_device_get) |
| ![Konak Yığını Cihazı Kaldır simgesi](./media/user-guide/usbx-events/image197.png)    | **Konak Yığını Cihazı Kaldırma** (ux_host_stack_device_get) |
| ![Konak Yığını Cihaz Kaynağı Ücretsiz simgesi](./media/user-guide/usbx-events/image198.png)    | **Konak Yığını Cihaz Kaynağı Ücretsiz** (ux_host_stack_device_resource_free) |
| ![Konak Yığını Uç Nokta Örneği Oluştur simgesi](./media/user-guide/usbx-events/image199.png)    | **Konak Yığını Uç Nokta Örneği Oluşturma** (ux_host_stack_endpoint_instance_create) |
| ![Konak Yığını Uç Nokta Örneği Silme simgesi](./media/user-guide/usbx-events/image200.png)    | **Konak Yığını Uç Nokta Örneği Silme** (ux_host_stack_endpoint_instance_delete) |
| ![Konak Yığını Uç Noktası Sıfırlama simgesi](./media/user-guide/usbx-events/image201.png)    | **Konak Yığını Uç Noktası Sıfırlama** (ux_host_stack_endpoint_reset) |
| ![Konak Yığını Uç Nokta Aktarım Durdurma simgesi](./media/user-guide/usbx-events/image202.png)    | **Konak Yığını Uç Nokta Aktarım Durdurma** (ux_host_stack_endpoint_transfer_abort) |
| ![Konak Yığını Konak Denetleyicisi Kayıt simgesi](./media/user-guide/usbx-events/image203.png)    | **Konak Yığını Konak Denetleyicisi Kaydı** *(ux_host_stack_hcd_register)* |
| ![Konak Yığını Başlat simgesi](./media/user-guide/usbx-events/image204.png)    | **Konak Yığını Başlatma** *(ux_host_stack_initialize)* |
| ![Konak Yığını Arabirimi Uç Noktası Al simgesi](./media/user-guide/usbx-events/image205.png)    | **Konak Yığını Arabirimi Uç Noktası Al** *(ux_host_stack_interface_endpoint_get)* |
| ![Konak Yığını Arabirim Örneği Oluşturma simgesi](./media/user-guide/usbx-events/image206.png)    | **Konak Yığını Arabirim Örneği Oluşturma** *(ux_host_stack_interface_instance_create)* |
| ![Konak Yığını Arabirim Örneği Silme simgesi](./media/user-guide/usbx-events/image207.png)    | **Konak Yığını Arabirim Örneği Silme** *(ux_host_stack_interface_instance_delete)* |
| ![Konak Yığını Arabirim Kümesi simgesi](./media/user-guide/usbx-events/image208.png)    | **Konak Yığını Arabirim Kümesi** *(ux_host_stack_interface_set)* |
| ![Konak Yığını Arabirim Ayarı Seç simgesi](./media/user-guide/usbx-events/image209.png)    | **Konak Yığını Arabirim Ayarı Seçme** *(ux_host_stack_interface_setting_select)* |
| ![Konak Yığını Yeni Yapılandırma Oluştur simgesi](./media/user-guide/usbx-events/image210.png)    | **Konak Yığını Yeni Yapılandırma Oluşturma** *(ux_host_stack_new_configuration_create)* |
| ![Konak Yığını Yeni Cihaz Oluştur simgesi](./media/user-guide/usbx-events/image211.png)    | **Konak Yığını Yeni Cihaz Oluşturma** *(ux_host_stack_new_device_create)* |
| ![Konak Yığını Yeni Uç Nokta Oluştur simgesi](./media/user-guide/usbx-events/image212.png)    | **Konak Yığını Yeni Uç Nokta Oluşturma** *(ux_host_stack_new_endpoint_create)* |
| ![Konak Yığını Kök Hub'ı Değiştirme süreci simgesi](./media/user-guide/usbx-events/image213.png)    | **Konak Yığını Kök Hub'ı Değişiklik Süreci** *(ux_host_stack_rh_change_process)* |
| ![Konak Yığını Kök Hub'ı Cihaz Ayıklama simgesi](./media/user-guide/usbx-events/image214.png)    | **Konak Yığını Kök Hub'ı Cihaz Ayıklama** *(ux_host_stack_rh_device_extraction)* |
| ![Konak Yığını Kök Hub Cihazı Ekleme simgesi](./media/user-guide/usbx-events/image215.png)    | **Konak Yığını Kök Hub Cihazı Ekleme** *(ux_host_stack_rh_device_insertion)* |
| ![Konak Yığını Aktarım İsteği simgesi](./media/user-guide/usbx-events/image216.png)    | **Konak Yığını Aktarım İsteği** *(ux_host_stack_transfer_request)* |
| ![Konak Yığını Aktarım İsteği Durdurma simgesi](./media/user-guide/usbx-events/image217.png)    | **Konak Yığın Aktarım İsteği Durdurma** *(ux_host_stack_transfer_request_abort)* |
| ![U S B X Hata simgesi](./media/user-guide/usbx-events/image218.png)    | **USBX Hatası** *(ux_error)* |

## <a name="event-descriptions"></a>Olay Açıklamaları

Aşağıdaki sayfalarda USBX İzleme Olayları açık bir şekilde anlatılır.

### <a name="device-class-cdc-activate"></a>Cihaz Sınıfı Cdc Etkinleştirme 

#### <a name="ux_device_class_cdc_activate"></a>ux_device_class_cdc_activate

**Simge** ![ Cihaz Sınıfı C D C Etkinleştirme simgesi](./media/user-guide/usbx-events/image1.png)

**Açıklama**

Bu olay bir USBX Cihaz Sınıfı Cdc Etkinleştirme Olayı'dır.

**Bilgi Alanları** 

- Bilgi Alanı 1: Sınıf Örneği.
- Bilgi Alanı 2: Kullanılmadı.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="device-class-cdc-deactivate"></a>Cihaz Sınıfı Cdc Devre Dışı Bırakma 

#### <a name="ux_device_class_cdc_deactivate"></a>ux_device_class_cdc_deactivate

**Simge** ![ Cihaz Sınıfı C D C Devre Dışı Bırak simgesi](./media/user-guide/usbx-events/image2.png)

**Açıklama**

Bu olay bir USBX Cihaz Sınıfı Cdc Devre Dışı Bırak'ı temsil eder.

Bilgi Alanları 

- Bilgi Alanı 1: Sınıf Örneği.
- Bilgi Alanı 2: Kullanılmadı.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="device-class-cdc-read"></a>Cihaz Sınıfı Cdc Okuma 

#### <a name="ux_device_class_cdc_read"></a>ux_device_class_cdc_read

**Simge** ![ Cihaz Sınıfı C D C Okuma simgesi](./media/user-guide/usbx-events/image3.png)

**Açıklama**

Bu olay bir USBX Cihaz Sınıfı Cdc Okuma Olayı'dır.

**Bilgi Alanları**

- Bilgi Alanı 1: Sınıf Örneği.
- Bilgi Alanı 2: Veri işaretçisi.
- Bilgi Alanı 3: İstenen uzunluk.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="device-class-cdc-write"></a>Cihaz Sınıfı Cdc Yazma 

#### <a name="ux_device_class_cdc_write"></a>ux_device_class_cdc_write

**Simge** ![ Cihaz Sınıfı C D C Yazma simgesi](./media/user-guide/usbx-events/image4.png)

**Açıklama**

Bu olay bir USBX Cihaz Sınıfı Cdc Yazma Olayı'dır.

**Bilgi Alanları**

- Bilgi Alanı 1: Sınıf Örneği.
- Bilgi Alanı 2: Veri işaretçisi.
- Bilgi Alanı 3: İstenen uzunluk.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="device-class-dpump-activate"></a>Cihaz Sınıfı Dpump Etkinleştirme 

#### <a name="ux_device_class_dpump_activate"></a>ux_device_class_dpump_activate

**Simge** ![ Cihaz Sınıfı Dpump Etkinleştirme simgesi](./media/user-guide/usbx-events/image5.png)

**Açıklama**

Bu olay bir USBX Cihaz Sınıfı Dpump Etkinleştirme Olayı'dır.

**Bilgi Alanları**

- Bilgi Alanı 1: Sınıf Örneği.
- Bilgi Alanı 2: Kullanılmadı.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="device-class-dpump-deactivate"></a>Cihaz Sınıfı Dpump Devre Dışı Bırakma 

#### <a name="ux_device_class_dpump_deactivate"></a>ux_device_class_dpump_deactivate

**Simge** ![ Cihaz Sınıfı Dpump Devre Dışı Bırak simgesi](./media/user-guide/usbx-events/image6.png)

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

Bu olay bir USBX Cihaz Sınıfı Pima Etkinleştirme Olayı'dır.

**Bilgi Alanları**

- Bilgi Alanı 1: Sınıf Örneği.
- Bilgi Alanı 2: Kullanılmadı.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="device-class-pima-deactivate"></a>Cihaz Sınıfı Pima Devre Dışı Bırakma 

#### <a name="ux_device_class_pima_deactivate"></a>ux_device_class_pima_deactivate

**Simge** ![ Cihaz Sınıfı Pima Devre Dışı Bırak simgesi](./media/user-guide/usbx-events/image17.png)

**Açıklama**

Bu olay bir USBX Cihaz Sınıfı Pima Devre Dışı Bırakma Olayı'dır.

**Bilgi Alanları**

- Bilgi Alanı 1: Sınıf Örneği.
- Bilgi Alanı 2: Kullanılmadı.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="device-class-pima-device-info-send"></a>Cihaz Sınıfı Pima Cihaz Bilgisi Gönderme 

#### <a name="ux_device_class_pima_device_info_send"></a>ux_device_class_pima_device_info_send

**Simge** ![ Cihaz Sınıfı Pima Cihaz Bilgileri Gönderme simgesi](./media/user-guide/usbx-events/image18.png)

**Açıklama**

Bu olay bir USBX Cihaz Sınıfı Pima Cihaz Bilgisi Gönderme Olayı'dır.

**Bilgi Alanları**

- Bilgi Alanı 1: Sınıf Örneği.
- Bilgi Alanı 2: Kullanılmadı.
- Bilgi Alanı 3: Kullanılmaz.

### <a name="device-class-pima-event-get"></a>Cihaz Sınıfı Pima Olay Al 

#### <a name="ux_device_class_pima_event_get"></a>ux_device_class_pima_event_get

**Simge** ![ Cihaz Sınıfı Pima Olayı Al simgesi](./media/user-guide/usbx-events/image19.png)

**Açıklama**

Bu olay bir USBX Cihaz Sınıfı Pima Olay Al Olayı'dır.

**Bilgi Alanları**

- Bilgi Alanı 1: Sınıf Örneği.
- Bilgi Alanı 2: Pima olayı.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="device-class-pima-event-set"></a>Cihaz Sınıfı Pima Olay Kümesi 

#### <a name="ux_device_class_pima_event_set"></a>ux_device_class_pima_event_set

**Simge** ![ Cihaz Sınıfı Pima Olay Kümesi simgesi](./media/user-guide/usbx-events/image20.png)

**Açıklama**

Bu olay bir USBX Cihaz Sınıfı Pima Olay Kümesi Olayı'dır.

**Bilgi Alanları**

- Bilgi Alanı 1: Sınıf Örneği.
- Bilgi Alanı 2: Pima olayı.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="device-class-pima-object-add"></a>Cihaz Sınıfı Pima Nesnesi Ekleme 

#### <a name="ux_device_class_pima_object_add"></a>ux_device_class_pima_object_add

**Simge** ![ Device Class Pima Object Add simgesi](./media/user-guide/usbx-events/image21.png)

**Açıklama**

Bu olay bir USBX Cihaz Sınıfı Pima Nesnesi Ekleme Olayı'dır.

**Bilgi Alanları** 

- Bilgi Alanı 1: Sınıf Örneği.
- Bilgi Alanı 2: Nesne tanıtıcısı.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="device-class-pima-object-data-get"></a>Cihaz Sınıfı Pima Nesne Verilerini Al 

#### <a name="ux_device_class_pima_object_data_get"></a>ux_device_class_pima_object_data_get

**Simge** ![ Cihaz Sınıfı Pima Nesne Verileri Al simgesi](./media/user-guide/usbx-events/image22.png)

**Açıklama**

Bu olay bir USBX Cihaz Sınıfı Pima Nesne Verileri Al Olayı'dır.

**Bilgi Alanları** 

- Bilgi Alanı 1: Sınıf Örneği.
- Bilgi Alanı 2: Nesne tanıtıcısı.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="device-class-pima-object-data-send"></a>Cihaz Sınıfı Pima Nesne Veri Gönderme 

#### <a name="ux_device_class_pima_object_data_send"></a>ux_device_class_pima_object_data_send

**Simge** ![ Cihaz Sınıfı Pima Nesne Verileri Gönderme simgesi](./media/user-guide/usbx-events/image23.png)

**Açıklama**

Bu olay bir USBX Cihaz Sınıfı Pima Nesne Veri Gönderme Olayı'dır.

**Bilgi Alanları** 

- Bilgi Alanı 1: Sınıf Örneği.
- Bilgi Alanı 2: Nesne tanıtıcısı.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="device-class-pima-object-delete"></a>Cihaz Sınıfı Pima Nesne Silme 

#### <a name="ux_device_class_pima_object_delete"></a>ux_device_class_pima_object_delete

**Simge** ![ Cihaz Sınıfı Pima Nesne Silme simgesi](./media/user-guide/usbx-events/image24.png)

**Açıklama**

Bu olay bir USBX Cihaz Sınıfı Pima Nesne Silme Olayı'dır.

**Bilgi Alanları** 

- Bilgi Alanı 1: Sınıf Örneği.
- Bilgi Alanı 2: Nesne tanıtıcısı.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="device-class-pima-object-handles-send"></a>Cihaz Sınıfı Pima Nesne Tanıtıcıları Gönderme 

#### <a name="ux_device_class_pima_object_handles_send"></a>ux_device_class_pima_object_handles_send

**Simge** ![ Cihaz Sınıfı Pima Nesne Tanıtıcıları Gönderme simgesi](./media/user-guide/usbx-events/image25.png)

**Açıklama**

Bu olay, Bir USBX Cihaz Sınıfı Pima Nesnesi Gönderme Olayı tanıtıcılarını temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: Sınıf örneği.
- Bilgi Alanı 2: Depolama kimliği.
- Bilgi Alanı 3: Nesne biçimi kodu.
- Bilgi Alanı 4: Nesne ilişkilendirme.

### <a name="device-class-pima-object-info-get"></a>Cihaz Sınıfı Pima Nesne Bilgileri Al 

#### <a name="ux_device_class_pima_object_info_send"></a>ux_device_class_pima_object_info_send

**Simge** ![ Cihaz Sınıfı Pima Nesne Bilgileri Al simgesi](./media/user-guide/usbx-events/image26.png)

**Açıklama**

Bu olay bir USBX Cihaz Sınıfı Pima Nesne Bilgisi Al Olayı'dır.

**Bilgi Alanları**

- Bilgi Alanı 1: Sınıf Örneği.
- Bilgi Alanı 2: Nesne tanıtıcısı.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="device-class-pima-object-info-send"></a>Cihaz Sınıfı Pima Nesne Bilgisi Gönderme 

#### <a name="ux_device_class_pima_object_info_send"></a>ux_device_class_pima_object_info_send

**Simge** ![ Cihaz Sınıfı Pima Nesne Bilgisi Gönderme simgesi](./media/user-guide/usbx-events/image27.png)

**Açıklama**

Bu olay bir USBX Cihaz Sınıfı Pima Nesne Bilgisi Gönderme Olayı'dır.

**Bilgi Alanları**

- Bilgi Alanı 1: Sınıf Örneği.
- Bilgi Alanı 2: Kullanılmadı.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="device-class-pima-objects-number-send"></a>Cihaz Sınıfı Pima Nesne Numarası Gönderme 

#### <a name="ux_device_class_pima_object_number_send"></a>ux_device_class_pima_object_number_send

**Simge** ![ Device Class Pima Objects Number Send simgesi](./media/user-guide/usbx-events/image28.png)

**Açıklama**

Bu olay bir USBX Cihaz Sınıfı Pima Nesne Numarası Gönderme olayıdır.

**Bilgi Alanları**

- Bilgi Alanı 1: Sınıf Örneği.
- Bilgi Alanı 2: Depolama kimliği.
- Bilgi Alanı 3: Nesne biçimi kodu.
- Bilgi Alanı 4: Nesne ilişkilendirmesi.

### <a name="device-class-pima-partial-object-data-get"></a>Cihaz Sınıfı Pima Kısmi Nesne Verileri Al

#### <a name="ux_device_class_pima_partial_object_data_get"></a>ux_device_class_pima_partial_object_data_get

**Simge** ![ Cihaz Sınıfı Pima Kısmi Nesne Verileri Al simgesi](./media/user-guide/usbx-events/image29.png)

**Açıklama**

Bu olay bir USBX Cihaz Sınıfı Pima Kısmi Nesne Verileri Al Olayı'dır.

**Bilgi Alanları**

- Bilgi Alanı 1: Sınıf Örneği.
- Bilgi Alanı 2: Nesne tanıtıcısı.
- Bilgi Alanı 3: Uzaklık isteği.
- Bilgi Alanı 4: Uzunluk istenen.

### <a name="device-class-pima-response-send"></a>Cihaz Sınıfı Pima Yanıt Gönderme 

#### <a name="ux_device_class_pima_response_send"></a>ux_device_class_pima_response_send

**Simge** ![ Cihaz Sınıfı Pima Yanıt Gönderme simgesi](./media/user-guide/usbx-events/image30.png)

**Açıklama**

Bu olay bir USBX Cihaz Sınıfı Pima Yanıt Gönderme Olayı'dır.

**Bilgi Alanları**

- Bilgi Alanı 1: Sınıf örneği.
- Bilgi Alanı 2: Yanıt kodu.
- Bilgi Alanı 3: Sayı parametresi.
- Bilgi Alanı 4: Pima parametresi 1.

### <a name="device-class-pima-storage-id-send"></a>Cihaz Sınıfı Pima Depolama Kimliği Gönderme 

#### <a name="ux_device_class_pima_storage_id_send"></a>ux_device_class_pima_storage_id_send

**Simge** ![ Cihaz Sınıfı Pima Depolama Kimliği Gönder simgesi](./media/user-guide/usbx-events/image31.png)

**Açıklama**

Bu olay, bir USBX Cihaz Sınıfı Pima Depolama Kimliği Gönderme Olayı'Depolama temsil eder.

**Bilgi Alanları** 

- Bilgi Alanı 1: Sınıf Örneği.
- Bilgi Alanı 2: Kullanılmadı.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="device-class-pima-storage-info-send"></a>Cihaz Sınıfı Pima Depolama Bilgi Gönderme 

#### <a name="ux_device_class_pima_storage_info_send"></a>ux_device_class_pima_storage_info_send

**Simge** ![ Cihaz Sınıfı Pima Depolama Bilgi Gönderme simgesi](./media/user-guide/usbx-events/image32.png)

**Açıklama**

Bu olay, Bilgi Gönderme Olayı'Depolama USBX Cihaz Sınıfı Pima'yı temsil eder.

**Bilgi Alanları** 

- Bilgi Alanı 1: Sınıf Örneği.
- Bilgi Alanı 2: Kullanılmadı.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="device-class-rndis-activate"></a>Cihaz Sınıfı Rndis Etkinleştirme 

#### <a name="ux_device_class_rndis_activate"></a>ux_device_class_rndis_activate

**Simge** ![ Cihaz Sınıfı Rndis Etkinleştirme simgesi](./media/user-guide/usbx-events/image33.png)

**Açıklama**

Bu olay bir USBX Cihaz Sınıfı Rndis Etkinleştirme Olayı'dır.

**Bilgi Alanları** 

- Bilgi Alanı 1: Sınıf Örneği.
- Bilgi Alanı 2: Kullanılmadı.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="device-class-rndis-deactivate"></a>Cihaz Sınıfı Rndis Devre Dışı Bırakma 

#### <a name="ux_device_class_rndis_deactivate"></a>ux_device_class_rndis_deactivate

**Simge** ![ Cihaz Sınıfı Rndis Devre Dışı Bırak simgesi](./media/user-guide/usbx-events/image34.png)

**Açıklama**

Bu olay bir USBX Cihaz Sınıfı Rndis Devre Dışı Bırakma Olayı'dır.

**Bilgi Alanları** 

- Bilgi Alanı 1: Sınıf Örneği.
- Bilgi Alanı 2: Kullanılmadı.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="device-class-rndis-message-keep-alive"></a>Cihaz Sınıfı Rndis İletisi Canlı Tut 

#### <a name="ux_device_class_rndis_msg_keep_alive"></a>ux_device_class_rndis_msg_keep_alive

**Simge** ![ Cihaz Sınıfı Rndis İletisi Canlı Tut simgesi](./media/user-guide/usbx-events/image35.png)

**Açıklama**

Bu olay bir USBX Cihaz Sınıfı Rndis İleti etkin tutma olayı temsil eder.

**Bilgi Alanları** 

- Bilgi Alanı 1: Sınıf Örneği.
- Bilgi Alanı 2: Kullanılmadı.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="device-class-rndis-message-query"></a>Cihaz Sınıfı Rndis İleti Sorgusu 

#### <a name="ux_device_class_rndis_msg_keep_query"></a>ux_device_class_rndis_msg_keep_query

**Simge** ![ Cihaz Sınıfı Rndis İleti Sorgusu simgesi](./media/user-guide/usbx-events/image36.png)

**Açıklama**

Bu olay bir USBX Cihaz Sınıfı Rndis İleti Sorgu Olayı'nı temsil eder.

**Bilgi Alanları** 

- Bilgi Alanı 1: Sınıf Örneği.
- Bilgi Alanı 2: Rndis OID.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="device-class-rndis-message-reset"></a>Cihaz Sınıfı Rndis İleti Sıfırlama 

#### <a name="ux_device_class_rndis_msg_reset"></a>ux_device_class_rndis_msg_reset

**Simge** ![ Cihaz Sınıfı Rndis İleti Sıfırlama simgesi](./media/user-guide/usbx-events/image37.png)

**Açıklama**

Bu olay bir USBX Cihaz Sınıfı Rndis İleti Sıfırlama Olayı'dır.

**Bilgi Alanları** 

- Bilgi Alanı 1: Sınıf Örneği.
- Bilgi Alanı 2: Kullanılmadı.
- Bilgi Alanı 3: Kullanılmaz.

### <a name="device-class-rndis-message-set"></a>Cihaz Sınıfı Rndis İleti Kümesi 

#### <a name="ux_device_class_rndis_msg_set"></a>ux_device_class_rndis_msg_set

**Simge** ![ Cihaz Sınıfı Rndis İleti Kümesi simgesi](./media/user-guide/usbx-events/image38.png)

**Açıklama**

Bu olay bir USBX Cihaz Sınıfı Rndis İleti Kümesi Olayı'dır.

**Bilgi Alanları**

- Bilgi Alanı 1: Sınıf Örneği.
- Bilgi Alanı 2: Rndis OID.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="device-class-rndis-packet-receive"></a>Cihaz Sınıfı Rndis Paket Alma 

#### <a name="ux_device_class_rndis_packet_receive"></a>ux_device_class_rndis_packet_receive

**Simge** ![ Cihaz Sınıfı Rndis Paket Alma simgesi](./media/user-guide/usbx-events/image39.png)

**Açıklama**

Bu olay bir USBX Cihaz Sınıfı Rndis Paket Alma Olayı'dır.

**Bilgi Alanları**

- Bilgi Alanı 1: Sınıf Örneği.
- Bilgi Alanı 2: Kullanılmadı.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="device-class-rndis-packet-transmit"></a>Cihaz Sınıfı Rndis Paket İletme 

#### <a name="ux_device_class_rndis_packet_transmit"></a>ux_device_class_rndis_packet_transmit

**Simge** ![ Cihaz Sınıfı Rndis Paket İletme simgesi](./media/user-guide/usbx-events/image40.png)

**Açıklama**

Bu olay bir USBX Cihaz Sınıfı Rndis Paket İletme Olayı'dır.

**Bilgi Alanları** 

- Bilgi Alanı 1: Sınıf Örneği.
- Bilgi Alanı 2: Kullanılmadı.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="device-class-storage-activate"></a>Cihaz Sınıfı Depolama Etkinleştirme 

#### <a name="ux_device_class_storage_activate"></a>ux_device_class_storage_activate

**Simge** ![ Cihaz Sınıfı Depolama Etkinleştir simgesi](./media/user-guide/usbx-events/image41.png)

**Açıklama**

Bu olay, Etkinleştirme Olayı'nın bir USBX Depolama sınıfını temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: Sınıf Örneği.
- Bilgi Alanı 2: Kullanılmadı.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="device-class-storage-deactivate"></a>Cihaz Sınıfı Depolama Devre Dışı Bırakma 

#### <a name="ux_device_class_storage_deactivate"></a>ux_device_class_storage_deactivate

**Simge** ![ Cihaz Sınıfı Depolama Devre Dışı Bırak simgesi](./media/user-guide/usbx-events/image42.png)

**Açıklama**

Bu olay, Devre Dışı Bırakma Olayı'Depolama USBX Cihaz Sınıfını temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: Sınıf Örneği.
- Bilgi Alanı 2: Kullanılmadı.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="device-class-storage-format"></a>Cihaz Sınıfı Depolama Biçimi 

#### <a name="ux_device_class_storage_format"></a>ux_device_class_storage_format

**Simge** ![ Cihaz Sınıfı Depolama Biçimi simgesi](./media/user-guide/usbx-events/image43.png)

**Açıklama**

Bu olay, BIR USBX Cihaz Sınıfı Depolama Olay'ını temsil eder.

**Bilgi Alanları** 

- Bilgi Alanı 1: Sınıf Örneği.
- Bilgi Alanı 2: Lun.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="device-class-storage-inquiry"></a>Cihaz Sınıfı Depolama Sorgulama 

#### <a name="ux_device_class_storage_inquiry"></a>ux_device_class_storage_inquiry

**Simge** ![ Cihaz Sınıfı Depolama Sorgulama simgesi](./media/user-guide/usbx-events/image44.png)

**Açıklama**

Bu olay, Bir USBX Cihaz Sınıfı Depolama Olay'ını temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: Sınıf Örneği.
- Bilgi Alanı 2: Lun.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="device-class-storage-mode-select"></a>Cihaz Sınıfı Depolama Modu Seçme

#### <a name="ux_device_class_storage_mode_select"></a>ux_device_class_storage_mode_select

**Simge** ![ Cihaz Sınıfı Depolama Modu Seç simgesi](./media/user-guide/usbx-events/image45.png)

**Açıklama**

Bu olay, BIR USBX Cihaz Sınıfı Depolama Modu Seçme Olayı'Depolama temsil eder.

**Bilgi Alanları** 

- Bilgi Alanı 1: Sınıf Örneği.
- Bilgi Alanı 2: Lun.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="device-class-storage-mode-sense"></a>Device Class Depolama Mode Sense 

#### <a name="ux_device_class_storage_mode_sense"></a>ux_device_class_storage_mode_sense

**Simge** ![ Device Class Depolama Mode Sense simgesi](./media/user-guide/usbx-events/image46.png)

**Açıklama**

Bu olay, Bir USBX Cihaz Sınıfı Depolama Algı olayı temsil eder.

Bilgi Alanları 

- NFO alanı 1: sınıf örneği.
- Bilgi alanı 2: LUN.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-storage-prevent-allow-media-removal"></a>cihaz sınıfı Depolama medya kaldırılmasına izin vermeyi engelliyor 

#### <a name="ux_device_class_storage_prevent_allow_media_removal"></a>ux_device_class_storage_prevent_allow_media_removal

**Simge** ![ cihaz sınıfı Depolama medya kaldırma simgesine izin vermeyi engelliyor](./media/user-guide/usbx-events/image47.png)

**Açıklama**

bu olay, medya kaldırma olayına izin vermeyi engellemek Depolama bir usbx cihaz sınıfını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: LUN.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-storage-read"></a>Depolama cihaz sınıfı okuma 

#### <a name="ux_device_class_storage_read"></a>ux_device_class_storage_read

**Simge** ![ cihaz sınıfı Depolama okuma simgesi](./media/user-guide/usbx-events/image48.png)

**Açıklama**

bu olay, Read olayı Depolama bir usbx cihaz sınıfını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: LUN.
- Bilgi alanı 3: sektör.
- Bilgi alanı 4: sayı kesimleri.

### <a name="device-class-storage-read-capacity"></a>cihaz sınıfı Depolama okuma kapasitesi 

#### <a name="ux_device_class_storage_read_capacity"></a>ux_device_class_storage_read_capacity

**Simge** ![ cihaz sınıfı Depolama okuma kapasitesi simgesi](./media/user-guide/usbx-events/image49.png)

**Açıklama**

bu olay, okuma kapasitesi olayını Depolama bir usbx cihaz sınıfını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: LUN.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-storage-read-format-capacity"></a>cihaz sınıfı Depolama okuma biçimi kapasitesi 

#### <a name="ux_device_class_storage_read_format_capacity"></a>ux_device_class_storage_read_format_capacity

**Simge** ![ cihaz sınıfı Depolama okuma biçimi kapasitesi simgesi](./media/user-guide/usbx-events/image50.png)

**Açıklama**

bu olay bir usbx cihaz sınıfını Depolama okuma biçimi kapasitesi olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: LUN.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-storage-read-toc"></a>Device Class Depolama TOC 'yi oku 

#### <a name="ux_device_class_storage_read_toc"></a>ux_device_class_storage_read_toc

**Simge** ![ Device Class Depolama içindekileri oku simgesi](./media/user-guide/usbx-events/image51.png)

**Açıklama**

bu olay bir usbx cihaz sınıfını temsil eder Depolama TOC olayını okur.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: LUN.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-storage-request-sense"></a>cihaz sınıfı Depolama istek algılaması 

#### <a name="ux_device_class_storage_request_sense"></a>ux_device_class_storage_request_sense

**Simge** ![ cihaz sınıfı Depolama istek algılama simgesi](./media/user-guide/usbx-events/image52.png)

**Açıklama**

bu olay, istek algılama olayını Depolama bir usbx cihaz sınıfını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: LUN.
- Bilgi alanı 3: Sense anahtarı.
- Bilgi alanı 4: kod.

### <a name="device-class-storage-start-stop"></a>cihaz sınıfı Depolama başlat durdur 

#### <a name="ux_device_class_storage_start_stop"></a>ux_device_class_storage_start_stop

**Simge** ![ cihaz sınıfı Depolama başlangıcı durdur simgesi](./media/user-guide/usbx-events/image53.png)

**Açıklama**

bu olay, başlatma durdurma olayını Depolama bir usbx cihaz sınıfını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: LUN.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-storage-test-ready"></a>cihaz sınıfı Depolama Test hazırlanıyor 

#### <a name="ux_device_class_storage_test_ready"></a>ux_device_class_storage_test_ready

**Simge** ![ cihaz sınıfı Depolama Test Ready simgesi](./media/user-guide/usbx-events/image54.png)

**Açıklama**

bu olay, Test Ready olayı Depolama bir usbx cihaz sınıfını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: LUN.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-storage-verify"></a>cihaz sınıfı Depolama doğrulaması 

#### <a name="ux_device_class_storage_verify"></a>ux_device_class_storage_verify

**Simge** ![ cihaz sınıfı Depolama doğrulama simgesi](./media/user-guide/usbx-events/image55.png)

**Açıklama**

bu olay, Verify olayını Depolama bir usbx cihaz sınıfını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: LUN.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="device-class-storage-write"></a>cihaz sınıfı Depolama yazma 

#### <a name="ux_device_class_storage_write"></a>ux_device_class_storage_write

**Simge** ![ cihaz sınıfı Depolama yazma simgesi](./media/user-guide/usbx-events/image56.png)

**Açıklama**

bu olay, Write olayı Depolama bir usbx cihaz sınıfını temsil eder.

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

### <a name="device-stack-connect"></a>cihaz yığını Bağlan 

#### <a name="ux_device_stack_connect"></a>ux_device_stack_connect

**Simge** ![ cihaz yığını Bağlan simgesi](./media/user-guide/usbx-events/image63.png)

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

- Bilgi Alanı 1: Uç nokta.
- Bilgi Alanı 2: Kullanılmadı.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="device-stack-get-status"></a>Cihaz Yığını Durumu Al 

#### <a name="ux_device_stack_get_status"></a>ux_device_stack_get_status

**Simge** ![ Cihaz Yığını Durum Al simgesi](./media/user-guide/usbx-events/image67.png)

**Açıklama**

Bu olay bir USBX Cihaz Yığını Durum Al Olayı'dır.

**Bilgi Alanları**

- Bilgi Alanı 1: Kullanılmaz.
- Bilgi Alanı 2: Kullanılmadı.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="device-stack-host-wakeup"></a>Cihaz Yığını Ana Bilgisayarı Uyandırma 

#### <a name="ux_device_stack_host_wakeup"></a>ux_device_stack_host_wakeup

**Simge** ![ Cihaz Yığını Konak Uyandırma simgesi](./media/user-guide/usbx-events/image68.png)

**Açıklama**

Bu olay bir USBX Cihaz Yığını Konak Uyandırma Olayı'dır.

**Bilgi Alanları** 

- Bilgi Alanı 1: Kullanılmaz.
- Bilgi Alanı 2: Kullanılmadı.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="device-stack-initialize"></a>Cihaz Yığını Başlatma 

#### <a name="ux_device_stack_initialize"></a>ux_device_stack_initialize

**Simge** ![ Cihaz Yığını Başlat simgesi](./media/user-guide/usbx-events/image69.png)

**Açıklama**

Bu olay bir USBX Cihaz Yığını Başlatma Olayı'dır.

**Bilgi Alanları** 

- Bilgi Alanı 1: Kullanılmaz.
- Bilgi Alanı 2: Kullanılmadı.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="device-stack-interface-delete"></a>Cihaz Yığını Arabirimi Silme 

#### <a name="ux_device_stack_interface_delete"></a>ux_device_stack_interface_delete

**Simge** ![ Cihaz Yığını Arabirimi Silme simgesi](./media/user-guide/usbx-events/image70.png)

**Açıklama**

Bu olay bir USBX Cihaz Yığını Arabirimi Silme Olayı'dır.

**Bilgi Alanları**

- Bilgi Alanı 1: Arabirim.
- Bilgi Alanı 2: Kullanılmadı.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="device-stack-interface-get"></a>Cihaz Yığını Arabirimi Al 

#### <a name="ux_device_stack_interface_get"></a>ux_device_stack_interface_get

**Simge** ![ Cihaz Yığını Arabirimi Al simgesi](./media/user-guide/usbx-events/image71.png)

**Açıklama**

Bu olay bir USBX Cihaz Yığını Arabirimi Olay Al'dır.

**Bilgi Alanları** 

- Bilgi Alanı 1: Arabirim değeri.
- Bilgi Alanı 2: Kullanılmadı.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="device-stack-interface-set"></a>Cihaz Yığını Arabirim Kümesi 

#### <a name="ux_device_stack_interface_set"></a>ux_device_stack_interface_set

**Simge** ![ Cihaz Yığını Arabirim Kümesi simgesi](./media/user-guide/usbx-events/image72.png)

**Açıklama**

Bu olay bir USBX Cihaz Yığını Arabirim Kümesi Olayı'dır.

**Bilgi Alanları** 

- Bilgi Alanı 1: İstek değeri. Bilgi Alanı 2: İstek dizini.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="device-stack-set-feature"></a>Cihaz Yığın Kümesi Özelliği 

#### <a name="ux_device_stack_set_feature"></a>ux_device_stack_set_feature

**Simge** ![ Cihaz Yığın Kümesi Özellik simgesi](./media/user-guide/usbx-events/image73.png)

**Açıklama**

Bu olay bir USBX Cihaz Yığını Kümesi Özellik Olayı'dır.

**Bilgi Alanları** 

- Bilgi Alanı 1: İstek değeri. Bilgi Alanı 2: İstek dizini.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="device-stack-transfer-abort"></a>Cihaz Yığını Aktarım Durdurma 

#### <a name="ux_device_stack_transfer_abort"></a>ux_device_stack_transfer_abort

**Simge** ![ Cihaz Yığını Aktarım Durdurma simgesi](./media/user-guide/usbx-events/image74.png)

**Açıklama**

Bu olay bir USBX Cihaz Yığını Aktarım Durdurma Olayı'dır.

**Bilgi Alanları** 

- Bilgi Alanı 1: Aktarım isteği.
- Bilgi Alanı 2: Tamamlama kodu.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="device-stack-transfer-all-request-abort"></a>Cihaz Yığını Aktarımı Tüm İstek Durdurma 

#### <a name="ux_device_stack_transfer_all_request_abort"></a>ux_device_stack_transfer_all_request_abort

**Simge** ![ Cihaz Yığını Aktarım Tüm İstek Durdurma simgesi](./media/user-guide/usbx-events/image75.png)

**Açıklama**

Bu olay bir USBX Cihaz Yığını Aktarımı Tüm İstek Durdurma Olaylarını temsil eder.

**Bilgi Alanları** 

- Bilgi Alanı 1: Uç nokta.
- Bilgi Alanı 2: Tamamlama kodu.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="device-stack-transfer-request"></a>Cihaz Yığını Aktarım İsteği 

#### <a name="ux_device_stack_transfer_request"></a>ux_device_stack_transfer_request

**Simge** ![ Cihaz Yığını Aktarım İsteği simgesi](./media/user-guide/usbx-events/image76.png)

**Açıklama**

Bu olay bir USBX Cihaz Yığını Aktarım İsteği Olayı'dır.

**Bilgi Alanları**

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
- Bilgi Alanı 1: Sınıf örneği.
- Bilgi Alanı 2: Veri işaretçisi.
- Bilgi Alanı 3: İstenen uzunluk.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="host-class-audio-streaming-sampling-get"></a>Konak Sınıfı Ses Akışı Örnekleme Alma 

#### <a name="ux_host_class_audio_streaming_sampling_get"></a>ux_host_class_audio_streaming_sampling_get

**Simge** ![ Konak Sınıfı Ses Akışı Örnekleme Alma simgesi](./media/user-guide/usbx-events/image87.png)

**Açıklama**

Bu olay bir USBX Konak Sınıfı Ses Akışı Örnekleme Alma Olayı'dır.

**Bilgi Alanları** 

- Bilgi Alanı 1: Sınıf örneği.
- Bilgi Alanı 2: Kullanılmadı.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="host-class-audio-streaming-sampling-set"></a>Konak Sınıfı Ses Akışı Örnekleme Kümesi 

#### <a name="ux_host_class_audio_streaming_sampling_set"></a>ux_host_class_audio_streaming_sampling_set

**Simge** ![ Konak Sınıfı Ses Akışı Örnekleme Kümesi simgesi](./media/user-guide/usbx-events/image88.png)

**Açıklama**

Bu olay bir USBX Konak Sınıfı Ses Akışı Örnekleme Kümesi Olayı'ı temsil eder.

**Bilgi Alanları** 

- Bilgi Alanı 1: Sınıf örneği.
- Bilgi Alanı 2: Ses Örnekleme.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="host-class-audio-write"></a>Konak Sınıfı Ses Yazma 

#### <a name="ux_host_class_audio_write"></a>ux_host_class_audio_write

**Simge** ![ Konak Sınıfı Ses Yazma simgesi](./media/user-guide/usbx-events/image89.png)

**Açıklama**

Bu olay bir USBX Konak Sınıfı Ses Yazma Olayı'dır.

**Bilgi Alanları** 

- Bilgi Alanı 1: Sınıf örneği.
- Bilgi Alanı 2: Veri işaretçisi.
- Bilgi Alanı 3: İstenen uzunluk.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="host-class-cdc-acm-activate"></a>Konak Sınıfı Cdc Acm Etkinleştirme 

#### <a name="ux_host_class_cdc_acm_activate"></a>ux_host_class_cdc_acm_activate

**Simge** ![ Konak Sınıfı C D C A C M Etkinleştirme simgesi](./media/user-guide/usbx-events/image90.png)

**Açıklama**

Bu olay bir USBX Konak Sınıfı Cdc Acm Etkinleştirme Olayı'dır.

**Bilgi Alanları**

- Bilgi Alanı 1: Sınıf örneği.
- Bilgi Alanı 2: Kullanılmadı.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="host-class-cdc-acm-deactivate"></a>Konak Sınıfı Cdc Acm Devre Dışı Bırakma 

#### <a name="ux_host_class_cdc_acm_deactivate"></a>ux_host_class_cdc_acm_deactivate

**Simge** ![ Konak Sınıfı C D C A C M Devre Dışı Bırak simgesi](./media/user-guide/usbx-events/image91.png)

**Açıklama**

Bu olay bir USBX Konak Sınıfı Cdc Acm Devre Dışı Bırakma Olayı'dır.

**Bilgi Alanları** 

- Bilgi Alanı 1: Sınıf örneği.
- Bilgi Alanı 2: Kullanılmadı.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="host-class-cdc-acm-ioctl-abort-in-pipe"></a>Kanalda Ana Bilgisayar Sınıfı Cdc Acm Ioctl Abort 

#### <a name="ux_host_class_cdc_acm_ioctl_abort_in_pipe"></a>ux_host_class_cdc_acm_ioctl_abort_in_pipe

**Simge** ![ Konak Sınıfı C D C A C M O C T L Kanalda Durdurma simgesi](./media/user-guide/usbx-events/image92.png)

**Açıklama**

Bu olay, Bir USBX Ana Bilgisayar Sınıfı Cdc Acm Ioctl KanalDa Durdurma Olayı'nın temsil eder.

Bilgi Alanları 

- Bilgi Alanı 1: Sınıf örneği.
- Bilgi Alanı 2: Uç nokta.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="host-class-cdc-acm-ioctl-abort-out-pipe"></a>Ana Bilgisayar Sınıfı Cdc Acm Ioctl Kanal Durdurma 

#### <a name="ux_host_class_cdc_acm_ioct_abort_out_pipe"></a>ux_host_class_cdc_acm_ioct_abort_out_pipe

**Simge** ! [[Konak Sınıfı C D C A C M O C T L Kanaldan Çıkma simgesini durdurma](./media/user-guide/usbx-events/image93.png)

**Açıklama**

Bu olay bir USBX Konak Sınıfı Cdc Acm Ioctl Abort Out Pipe Event'i temsil eder.

**Bilgi Alanları** 

- Bilgi Alanı 1: Sınıf örneği.
- Bilgi Alanı 2: Uç nokta.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="host-class-cdc-acm-ioctl-get-device-status"></a>Konak Sınıfı Cdc Acm Ioctl Cihaz Durumunu Al 

#### <a name="ux_host_class_cdc_acm_ioctl_get_device_status"></a>ux_host_class_cdc_acm_ioctl_get_device_status

**Simge** ![ Konak Sınıfı C D C A C M O C T L Cihaz Durumunu Al simgesi](./media/user-guide/usbx-events/image94.png)

**Açıklama**

Bu olay bir USBX Konak Sınıfı Cdc Acm Ioctl Get Device Status Event'i temsil eder.

**Bilgi Alanları** 

- Bilgi Alanı 1: Sınıf örneği.
- Bilgi Alanı 2: Cihaz durumu.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="host-class-cdc-acm-ioctl-get-line-coding"></a>Konak Sınıfı Cdc Acm Ioctl Satır Kodlaması Al 

#### <a name="ux_host_class_cdc_acm_ioctl_get_line_coding"></a>ux_host_class_cdc_acm_ioctl_get_line_coding

**Simge** ![ Konak Sınıfı C D C A C M O C T L Satır Kodlaması Al simgesi](./media/user-guide/usbx-events/image95.png)

**Açıklama**

Bu olay bir USBX Ana Bilgisayar Sınıfı Cdc Acm Ioctl Satır KodlamaSı Olayı Al'ı temsil eder.

**Bilgi Alanları** 

- Bilgi Alanı 1: Sınıf örneği.
- Bilgi Alanı 2: Parametre.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="host-class-cdc-acm-ioctl-notification-callback"></a>Konak Sınıfı Cdc Acm Ioctl Bildirim Geri Çağırma

#### <a name="ux_host_class_cdc_acm_ioctl_notification_callback"></a>ux_host_class_cdc_acm_ioctl_notification_callback

**Simge** ![ Konak Sınıfı C D C A C M O C T L Bildirim Geri Çağırma simgesi](./media/user-guide/usbx-events/image96.png)

**Açıklama**

Bu olay bir USBX Ana Bilgisayar Sınıfı Cdc Acm Ioctl Bildirim Geri Çağırma Olayı'dır.

**Bilgi Alanları**

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
- Bilgi Alanı 2: Veri işaretçisi.
- Bilgi Alanı 3: İstenen uzunluk.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="host-class-dpump-write"></a>Konak Sınıfı Dpump Yazma 

#### <a name="ux_host_class_dpump_write"></a>ux_host_class_dpump_write

**Simge** ![ Konak Sınıfı Dpump Yazma simgesi](./media/user-guide/usbx-events/image107.png)

**Açıklama**

Bu olay bir USBX Konak Sınıfı Dpump Yazma Olayı'ı temsil eder.

**Bilgi Alanları** 

- Bilgi Alanı 1: Sınıf örneği.
- Bilgi Alanı 2: Veri işaretçisi.
- Bilgi Alanı 3: İstenen uzunluk.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="host-class-hid-activate"></a>Host Classını Etkinleştirme 

#### <a name="ux_host_class_hid_activate"></a>ux_host_class_hid_activate

**Simge** ![ Konak Sınıfı Etkinleştir simgesi](./media/user-guide/usbx-events/image108.png)

**Açıklama**

Bu olay bir USBX Ana Bilgisayar Sınıfını Etkinleştirme Olayı'ı temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: Sınıf örneği.
- Bilgi Alanı 2: Kullanılmadı.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="host-class-hid-client-register"></a>Konak Sınıfı Gizli İstemci Kaydı 

#### <a name="ux_host_class_hid_client_register"></a>ux_host_class_hid_client_register

**Simge** ![ Konak SınıfıNız İstemci Kaydı simgesi](./media/user-guide/usbx-events/image109.png)

**Açıklama**

Bu olay bir USBX Konak Sınıfı Gizli İstemci Kaydetme Olayı'ı temsil eder.

**Bilgi Alanları** 

- Bilgi Alanı 1: gizli istemci adı.
- Bilgi Alanı 2: Kullanılmadı.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="host-class-hid-deactivate"></a>Konak Sınıfını Devre Dışı Bırakma 

#### <a name="ux_host_class_hid_deactivate"></a>ux_host_class_hid_deactivate

**Simge** ![ Konak Sınıfı Devre Dışı Bırak simgesi](./media/user-guide/usbx-events/image110.png)

**Açıklama**

Bu olay bir USBX Konak Sınıfını Devre Dışı Bırakma Olayı'dır.

**Bilgi Alanları** 

- Bilgi Alanı 1: Sınıf örneği.
- Bilgi Alanı 2: Kullanılmadı.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="host-class-hid-idle-get"></a>Konak Sınıfı Boşta Al 

#### <a name="ux_host_class_hid_idle_get"></a>ux_host_class_hid_idle_get

**Simge** ![ Host Class Idle Get simgesi](./media/user-guide/usbx-events/image111.png)

**Açıklama**

Bu olay bir USBX Konak Sınıfı BoşTakil Al Olayı'dır.

**Bilgi Alanları** 

- Bilgi Alanı 1: Sınıf örneği.
- Bilgi Alanı 2: Kullanılmadı.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="host-class-hid-idle-set"></a>Konak Sınıfı BoşTakil Küme 

#### <a name="ux_host_class_hid_idle_set"></a>ux_host_class_hid_idle_set

**Simge** ![ Konak Sınıfı Boşta Kalma Kümesi simgesi](./media/user-guide/usbx-events/image112.png)

**Açıklama**

Bu olay bir USBX Konak Sınıfı Boşta Kalma Kümesi Olayı'ı temsil eder.

**Bilgi Alanları** 

- Bilgi Alanı 1: Sınıf örneği.
- Bilgi Alanı 2: Kullanılmadı.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="host-class-hid-keyboard-activate"></a>Konak SınıfıNasla Klavye Etkinleştirme 

#### <a name="ux_host_class_hid_keyboard_activate"></a>ux_host_class_hid_keyboard_activate

**Simge** ![ Konak Sınıfı Klavye Etkinleştirme simgesi](./media/user-guide/usbx-events/image113.png)

**Açıklama**

Bu olay bir USBX Konak Sınıfı Klavye Etkinleştirme Olayı'ı temsil eder.

**Bilgi Alanları**
<p>Bilgi Alanı 1: Sınıf örneği.
<p>Bilgi Alanı 2: Gizli istemci örneği.
<p>Bilgi Alanı 3: Kullanılmaz.
<p>Bilgi Alanı 4: Kullanılmadı.

### <a name="host-class-hid-keyboard-deactivate"></a>Konak Sınıfı Klavyeyi Devre Dışı Bırakma 

#### <a name="ux_host_class_hid_keyboard_deactivate"></a>ux_host_class_hid_keyboard_deactivate

**Simge** ![ Konak Sınıfı Klavyeyi Devre Dışı Bırak simgesi](./media/user-guide/usbx-events/image114.png)

**Açıklama**

Bu olay bir USBX Konak Sınıfı KlavyeYi Devre Dışı Bırakma Olayı'dır.

**Bilgi Alanları**

- Bilgi Alanı 1: Sınıf örneği.
- Bilgi Alanı 2: Gizli istemci örneği.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="host-class-hid-mouse-activate"></a>Konak Sınıfı Fare Etkinleştirme 

#### <a name="ux_host_class_hid_mouse_activate"></a>ux_host_class_hid_mouse_activate

**Simge** ![ Konak Sınıfı Fare Etkinleştirme simgesi](./media/user-guide/usbx-events/image115.png)

**Açıklama**

Bu olay bir USBX Konak Sınıfı Fare Etkinleştirme Olayı'ı temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: Sınıf örneği.
- Bilgi Alanı 2: Gizli istemci örneği.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="host-class-hid-mouse-deactivate"></a>Konak Sınıfı FareYi Devre Dışı Bırakma 

#### <a name="ux_host_class_hid_mouse_deactivate"></a>ux_host_class_hid_mouse_deactivate

**Simge** ![ Konak Sınıfı Fare Devre Dışı Bırak simgesi](./media/user-guide/usbx-events/image116.png)

**Açıklama**

- Bu olay bir USBX Konak Sınıfı Fare Devre Dışı Bırakma Olayı'dır.

**Bilgi Alanları**

- Bilgi Alanı 1: Sınıf örneği.
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

### <a name="host-class-pima-storage-ids-get"></a>konak sınıfı pima Depolama kimlikleri al 

#### <a name="ux_host_class_pima_session_ids_get"></a>ux_host_class_pima_session_ids_get

**Simge** ![ konak sınıfı pima Depolama kimlikleri al simgesi](./media/user-guide/usbx-events/image148.png)

**Açıklama**

bu olay bir usbx konak sınıfı pima Depolama ıds Get olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- nfo alan 2: Depolama ıd dizisi.
- bilgi alanı 3: Depolama kimliği uzunluğu.
Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-pima-storage-info-get"></a>konak sınıfı pima Depolama bilgi al 

#### <a name="ux_host_class_pima_storage_info_get"></a>ux_host_class_pima_storage_info_get

**Simge** ![ konak sınıfı pima Depolama bilgileri al simgesi](./media/user-guide/usbx-events/image149.png)

**Açıklama**

bu olay bir usbx konak sınıfı pima Depolama ınfo Get olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- bilgi alanı 2: Depolama kimliği.
- bilgi alanı 3: Depolama.
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

### <a name="host-class-storage-activate"></a>konak sınıfı Depolama etkinleştir 

#### <a name="ux_host_class_storage_activate"></a>ux_host_class_storage_activate

**Simge** ![ konak sınıfı Depolama etkinleştir simgesi](./media/user-guide/usbx-events/image174.png)

**Açıklama**

bu olay, Activate olayını Depolama bir usbx konak sınıfını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-storage-deactivate"></a>konak sınıfı Depolama devre dışı bırak 

#### <a name="ux_host_class_storage_deactivate"></a>ux_host_class_storage_deactivate

**Simge** ![ konak sınıfı Depolama devre dışı bırak simgesi](./media/user-guide/usbx-events/image175.png)

**Açıklama**

bu olay, devre dışı bırakma olayı Depolama bir usbx konak sınıfını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="host-class-storage-media-capacity-get"></a>konak sınıfı Depolama medya kapasitesini al 

#### <a name="ux_host_class_storage_media_capacity_get"></a>ux_host_class_storage_media_capacity_get

**Simge** ![ konak sınıfı Depolama medya kapasitesini al simgesi](./media/user-guide/usbx-events/image176.png)

**Açıklama**

bu olay bir usbx konak sınıfını Depolama medya kapasitesi Get olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: sınıf örneği.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="host-class-storage-media-format-capacity-get"></a>Konak Sınıfı Depolama Medya Biçimi Kapasitesi Al

#### <a name="ux_host_class_storage_media_format_capacity_get"></a>ux_host_class_storage_media_format_capacity_get

**Simge** ![ Konak Sınıfı Depolama Medya Biçimi Kapasitesi Al simgesi](./media/user-guide/usbx-events/image177.png)

**Açıklama**

Bu olay, Medya Biçimi Kapasite Al Olayı'Depolama USBX Konak Sınıfını temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: Sınıf örneği.
- Bilgi Alanı 2: Kullanılmadı.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

#### <a name="host-class-storage-media-mount"></a>Konak Sınıfı Depolama Medya Bağlama 

#### <a name="ux_host_class_storage_media_mount"></a>ux_host_class_storage_media_mount

**Simge** ![ Konak Sınıfı Depolama Medya Bağlama simgesi](./media/user-guide/usbx-events/image178.png)

**Açıklama**

Bu olay, Medya Bağlama Olayı'nda bir USBX Depolama sınıfını temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: Sınıf örneği.
- Bilgi Alanı 2: Kesim.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="host-class-storage-media-open"></a>Host Class Depolama Media Open 

#### <a name="ux_host_class_storage_media_open"></a>ux_host_class_storage_media_open

**Simge** ![ Konak Sınıfı Depolama Medya Aç simgesi](./media/user-guide/usbx-events/image179.png)

**Açıklama**

Bu olay, Media Open Olayı'na Depolama USBX Konak Sınıfını temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: Sınıf örneği.
- Bilgi Alanı 2: Medya.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="host-class-storage-media-read"></a>Konak Sınıfı Depolama Medya Okuma 

#### <a name="ux_host_class_storage_media_read"></a>ux_host_class_storage_media_read

**Simge** ![ Konak Sınıfı Depolama Medya Okuma simgesi](./media/user-guide/usbx-events/image180.png)

**Açıklama**

Bu olay, Medya Okuma Olayı'Depolama USBX Konak Sınıfını temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: Sınıf örneği.
- Bilgi Alanı 2: Sektör başlangıcı.
- Bilgi Alanı 3: Kesim sayısı.
- Bilgi Alanı 4: Veri işaretçisi.

### <a name="host-class-storage-media-write"></a>Konak Sınıfı Depolama Medya Yazma 

#### <a name="ux_host_class_storage_media_write"></a>ux_host_class_storage_media_write

**Simge** ![ Konak Sınıfı Depolama Medya Yazma simgesi](./media/user-guide/usbx-events/image181.png)

**Açıklama**

Bu olay, Medya Yazma Olayı'Depolama USBX Konak Sınıfını temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: Sınıf örneği.
- Bilgi Alanı 2: Sektör başlangıcı.
- Bilgi Alanı 3: Kesim sayısı.
- Bilgi Alanı 4: Veri işaretçisi.

### <a name="host-class-storage-request-sense"></a>Konak Sınıfı Depolama İstek Algısı 

#### <a name="ux_host_class_storage_request_sense"></a>ux_host_class_storage_request_sense

**Simge** ![ Konak Sınıfı Depolama İstek Algısı simgesi](./media/user-guide/usbx-events/image182.png)

**Açıklama**

Bu olay, İstek Algısı Olayı'Depolama USBX Konak Sınıfını temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: Sınıf örneği.
- Bilgi Alanı 2: Kullanılmadı.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="host-class-storage-start-stop"></a>Konak Sınıfı Depolama Başlatma Durdurma 

#### <a name="ux_host_class_storage_start_stop"></a>ux_host_class_storage_start_stop

**Simge** ![ Konak Sınıfı Depolama Başlat Durdurma simgesi](./media/user-guide/usbx-events/image183.png)

**Açıklama**

Bu olay, Başlatma Durdurma Olayı'Depolama USBX Konak Sınıfını temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: Sınıf örneği.
- Bilgi Alanı 2: Başlatma durdurma sinyali.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="host-class-storage-unit-ready-test"></a>Konak Sınıfı Depolama Birim Hazır Testi 

#### <a name="ux_host_class_storage_unit_ready_test"></a>ux_host_class_storage_unit_ready_test

**Simge** ![ Konak Sınıfı Depolama Birim Hazır Test simgesi](./media/user-guide/usbx-events/image184.png)

**Açıklama**

Bu olay, Birim Hazır Test Olayı'Depolama USBX Konak Sınıfını temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: Sınıf örneği.
- Bilgi Alanı 2: Kullanılmadı.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="host-stack-class-instance-create"></a>Konak Yığını Sınıf Örneği Oluşturma 

#### <a name="ux_host_class_instance_create"></a>ux_host_class_instance_create

**Simge** ![ Konak Yığını Sınıf Örneği Oluştur simgesi](./media/user-guide/usbx-events/image185.png)

**Açıklama**

Bu olay bir USBX Konak Yığını Sınıf Örneği Oluşturma Olayı'dır.

**Bilgi Alanları**

- Bilgi Alanı 1: Sınıf.
- Bilgi Alanı 2: Sınıf Örneği.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="host-stack-class-instance-destroy"></a>Konak Stack Sınıf Örneği Yok Etme 

#### <a name="ux_host_class_instance_create"></a>ux_host_class_instance_create

**Simge** ![ Konak Yığını Sınıf Örneği Yok Etme simgesi](./media/user-guide/usbx-events/image186.png)

**Açıklama**

Bu olay bir USBX Konak Yığını Sınıf Örneği Yok Etme Olayı'ı temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: Sınıf.
- Bilgi Alanı 2: Sınıf Örneği.
- Bilgi Alanı 3: Kullanılmaz.
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
- Bilgi Alanı 4: Kullanılmadı.

### <a name="host-stack-device-remove"></a>Konak Yığını Cihazı Kaldırma 

#### <a name="ux_host_stack_device_remove"></a>ux_host_stack_device_remove

**Simge** ![ Konak Yığını Cihazı Kaldır simgesi](./media/user-guide/usbx-events/image197.png)

**Açıklama**

Bu olay bir USBX Konak Yığını Cihazı Kaldırma Olayı'dır.

**Bilgi Alanları**

- Bilgi Alanı 1: Hcd.
- Bilgi Alanı 2: Üst.
- Bilgi Alanı 3: Bağlantı Noktası Dizini.
- Bilgi Alanı 4: Cihaz.

### <a name="host-stack-device-resource-free"></a>Konak Yığını Cihaz Kaynağı Ücretsiz 

#### <a name="ux_host_stack_device_resource_free"></a>ux_host_stack_device_resource_free

**Simge** ![ Konak Yığını Cihaz Kaynağı Ücretsiz simgesi](./media/user-guide/usbx-events/image198.png)

**Açıklama**

Bu olay bir USBX Konak Yığını Cihazı Kaynağı Boş Olayı temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: Cihaz.
- Bilgi Alanı 2: Kullanılmadı.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="host-stack-endpoint-instance-create"></a>Konak Yığını Uç Nokta Örneği Oluşturma 

#### <a name="ux_host_stack_endpoint_instance_create"></a>ux_host_stack_endpoint_instance_create

**Simge** ![ Konak Yığını Uç Nokta Örneği Oluştur simgesi](./media/user-guide/usbx-events/image199.png)

**Açıklama**

Bu olay bir USBX Konak Yığını Uç Nokta Örneği Oluşturma Olayı'dır.

**Bilgi Alanları**

- Bilgi Alanı 1: Cihaz.
- Bilgi Alanı 2: Uç nokta.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="host-stack-endpoint-instance-delete"></a>Konak Yığını Uç Nokta Örneği Silme 

#### <a name="ux_host_stack_endpoint_instance_delete"></a>ux_host_stack_endpoint_instance_delete

**Simge** ![ Konak Yığını Uç Nokta Örneği Silme simgesi](./media/user-guide/usbx-events/image200.png)

**Açıklama**

Bu olay bir USBX Konak Yığını Uç Nokta Örneği Silme Olayı'dır.

**Bilgi Alanları**

- Bilgi Alanı 2: Uç nokta.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="host-stack-endpoint-reset"></a>Konak Yığını Uç Noktası Sıfırlama 

#### <a name="ux_host_stack_endpoint_reset"></a>ux_host_stack_endpoint_reset

**Simge** ![ Konak Yığını Uç Noktası Sıfırlama simgesi](./media/user-guide/usbx-events/image201.png)

**Açıklama**

Bu olay bir USBX Konak Yığını Uç Noktası Sıfırlama Olayı'dır.

**Bilgi Alanları**

- Bilgi Alanı 1: Cihaz.
- Bilgi Alanı 2: Uç nokta.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="host-stack-endpoint-transfer-abort"></a>Konak Yığını Uç Nokta Aktarım Durdurma 

#### <a name="ux_host_stack_endpoint_transfer_abort"></a>ux_host_stack_endpoint_transfer_abort

**Simge** ![ Konak Yığını Uç Nokta Aktarım Durdurma simgesi](./media/user-guide/usbx-events/image202.png)

**Açıklama**

Bu olay bir USBX Konak Yığını Uç Nokta Aktarımı Durdurma Olayı'dır.

**Bilgi Alanları**

- Bilgi Alanı 1: Uç nokta.
- Bilgi Alanı 2: Kullanılmadı.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="host-stack-host-controller-register"></a>Konak Yığını Konak Denetleyicisi Kaydı 

#### <a name="ux_host_stack_hcd_register"></a>ux_host_stack_hcd_register

**Simge** ![ Konak Yığını Konak Denetleyicisi Kayıt simgesi](./media/user-guide/usbx-events/image203.png)

**Açıklama**

Bu olay bir USBX Konak Yığını Konak Denetleyicisi Kaydını temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: Hcd Adı.
- Bilgi Alanı 2: Kullanılmadı.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="host-stack-initialize"></a>Konak Yığını Başlatma 

#### <a name="ux_host_stack_initialize"></a>ux_host_stack_initialize

**Simge** ![ Konak Yığını Başlat simgesi](./media/user-guide/usbx-events/image204.png)

**Açıklama**

Bu olay bir USBX Konak Yığını Başlatma Olayı'dır.

**Bilgi Alanları**

- Bilgi Alanı 1: Kullanılmaz.
- Bilgi Alanı 2: Kullanılmadı.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="host-stack-interface-endpoint-get"></a>Konak Yığını Arabirimi Uç Noktası Al 

#### <a name="interface_-tcp-retry-entry"></a>Interface_ TCP yeniden deneme girdisi

**Simge** ![ Konak Yığını Arabirimi Uç Noktası Al simgesi](./media/user-guide/usbx-events/image205.png)

**Açıklama**

Bu olay bir iç NetX TCP yeniden deneme olayı temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: Arabirim.
- Bilgi Alanı 2: Uç nokta dizini.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="host-stack-interface-instance-create"></a>Konak Yığını Arabirim Örneği Oluşturma 

#### <a name="ux_host_stack_interface_instance_create"></a>ux_host_stack_interface_instance_create

**Simge** ![ Konak Yığını Arabirim Örneği Oluşturma simgesi](./media/user-guide/usbx-events/image206.png)

**Açıklama**

Bu olay bir USBX Konak Yığını Arabirim Örneği Oluşturma Olayı'dır.

**Bilgi Alanları**

- Bilgi Alanı 1: Arabirim.
- Bilgi Alanı 2: Kullanılmadı.
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

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