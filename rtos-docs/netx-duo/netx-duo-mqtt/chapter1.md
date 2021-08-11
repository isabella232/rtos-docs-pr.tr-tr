---
title: Bölüm 1 - NetX Duo MQTT Azure RTOS ye giriş
description: NetX Duo MQTT istemci paketi için NetX Duo (sürüm 5.10 veya sonrası) yüklü, düzgün yapılandırılmış ve IP örneği oluşturulmuş olmalıdır.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: be650186b233d0f1202beecc22f4bd8bc0af4dbe0f677704d09df057fcbc34fc
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116797747"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-mqtt"></a>Bölüm 1 - NetX Duo MQTT Azure RTOS ye giriş

## <a name="netx-duo-mqtt-requirements"></a>NetX Duo MQTT Gereksinimleri

NetX Duo Azure RTOS MQTT istemci paketi için NetX Duo (sürüm 5.10 veya sonrası) yüklü, düzgün yapılandırılmış ve IP örneği oluşturulmuş olmalıdır. TCP modülü sistemde etkinleştirilmelidir. Ayrıca TLS güvenliği gerekli ise, NetX Secure TLS modülünün aracı tarafından gerekli olan güvenlik parametresine göre yapılandırılması gerekir.

## <a name="netx-duo-mqtt-specification"></a>NetX Duo MQTT Belirtimi

NetX Duo MQTT istemci uygulaması, 29 Ekim 2014'te<sup></sup> 3.1.1 SÜRÜMÜ ILE uyumludur. Belirtim şu şekilde bulunabilir:

- [http://mqtt.org/](http://mqtt.org/)

## <a name="netx-duo-mqtt-basic-operation"></a>NetX Duo MQTT Temel İşlem

MQTT (İleti Sırası Telemetri Aktarımı), yayımcı-abone modelini temel alan bir modeldir. Bir istemci, aracı aracılığıyla diğer istemcilere bilgi yayımlar. Bir konu başlığıyla ilgilenen bir istemci, aracı aracılığıyla konuya abone olabilir. Bir aracı, yayımlanan iletileri konuya abone olan istemcilerine teslim etmekle sorumludur. Bu yayımcı-abone modelinde, birden çok istemci aynı konu başlığına sahip verileri yayımlar. İstemci, aynı konuya abone olursa yayımlayan bir ileti alır.

Kullanım durumuna bağlı olarak, bir istemci bir ileti yayımlarken 3 QoS düzeylerinden birini seçebilir:

- **QoS 0:** İleti en çok bir kez teslim edilir. QoS 0 ile gönderilen iletiler kaybolabilir.
- **QoS 1:** İleti en az bir kez teslim edilir. QoS 1 ile gönderilen iletiler birden çok kez teslim edilir.
- **QoS 2:** İleti tam olarak bir kez teslim edilir. QoS 2 ile gönderilen iletilerin yinelemeden teslim edildiği garanti edilir.

> [!NOTE]
> MQTT istemcisinin bu uygulaması QoS düzey 2 iletilerini desteklemez.

QoS 1 ve QoS 2'nin teslim edildiği garanti edildiği için, aracı her istemciye gönderilen QoS 1 ve QoS 2 iletilerinin durumunu takip ediyor. Bu, QoS1 veya QoS 2 iletileri beklediğiniz istemciler için özellikle önemlidir. İstemcinin aracıyla bağlantısı kesiliyor olabilir (örneğin, istemci yeniden başlatıldığında veya iletişim bağlantısı geçici olarak kesildiğinde). İstemci aracıya yeniden bağlandığınızda iletilerin daha sonra teslimi için aracı QoS 1 ve QoS 2 iletilerini depolamalı. Ancak, istemci yeniden bağlantıdan sonra aracıdan eski ileti almamayı seçebilir. İstemci, bağlantıyı * clean_session _ olarak *ayarlanmış* şekilde başlatarak **NX_TRUE** bunu NX_TRUE. Bu durumda, MQTT CONNECT iletisi aldıktan sonra, aracı teslim edilmeyen veya onaylanmamış QoS 1 ya da QoS 2 iletileri de dahil olmak üzere bu istemciyle ilişkili tüm oturum bilgilerini atılmalıdır. Clean_session* bayrağı * NX_FALSE ise, sunucu QoS 1 ve QoS 2 iletilerini yeniden gönderir. __ MQTT İstemcisi ayrıca* *_clean_session* olarak ayarlanırsa onaylanmamış **tüm iletileri NX_TRUE.** Bu bildirim TCP katmanı ACK'den farklıdır, ancak bu da gerçekleşir. MQTT istemcisi aracıya bir bildirim gönderir.

Uygulama, * nxd_mqtt_client_create() _ çağrısıyla **bir MQTT istemci örneği** oluşturur. İstemci oluşturulduktan sonra uygulama, _*_nxd_mqtt_client_connect() çağrısıyla aracıya bağlanabilirsiniz._*_ Aracıya bağlanarak istemci _*_nxd_mqtt_client_subscribe()_*_ çağrısıyla bir konuya abone olabilir veya _*_nxd_mqtt_client_publish() ** çağrısıyla bir konu yayımlar._

Gelen MQTT iletileri MQTT istemci örneğinde alma kuyruğunda depolanır. Uygulama bu iletiyi ***nxd_mqtt_client_message_get() çağrısıyla alır.*** Alma kuyruğunda iletiler varsa, kuyruktan ilk ileti (ör. en eski) çağırana döndürülür. İletiden konu dizesi de döndürülür.

> [!NOTE]
> MQTT **istemcisi alma kuyruğu boşsa*** nxd_mqtt_client_message_get() _ işlevi engellemez. İşlev , _* ve **dönüş _koduyla NXD_MQTT_NO_MESSAGE_ döndürür. Uygulama bu dönüş değerini, hata değil alma kuyruğunun boş olduğunu gösteren bir gösterge olarak kabul etmektir.

Uygulama, gelen iletiler için alma kuyruğunun yoklamasını önlemek için nxd_mqtt_client_recieve_notify_set() çağrısıyla MQTT istemcisine ***bir geri çağırma işlevi kaydedebilir.*** Geri çağırma işlevi şu şekilde bildirildi:

```c
VOID (*receive_notify_callback)(NXD_MQTT_CLIENT *client_ptr, 
    UINT message_count);
```

MQTT istemcisi aracıdan iletileri aldığından, işlev ayarlanırsa geri çağırma işlevini çağırır. Geri çağırma işlevi, işaretçiyi istemci denetim bloğuna ve ileti sayısı değerine iletir. İleti sayısı değeri, alma kuyruğunda MQTT iletilerinin sayısını gösterir. Bu geri çağırma işlevinin MQTT istemci iş parçacığı bağlamında yürütülmektedir. Bu nedenle, geri çağırma işlevi MQTT istemci iş parçacığını engellenmiş herhangi bir yordam yürütmez. Geri çağırma işlevi, iletileri almak için ***nxd_mqtt_client_message_get()*** çağrısı yapmak için uygulama iş parçacığını tetiklemeli.

MQTT istemci hizmetinin bağlantısını kesmek ve sonlandırmak için uygulama ***nxd_mqtt_client_disconnect()** _ ve _*_nxd_mqtt_client_delete() hizmetini kullandır._*_ nxd_mqtt_client_disconnect() _*_çağrısı_*_ yalnızca aracıyla TCP bağlantısını keser. Daha önce alınan ve alma kuyruğunda depolanan iletileri serbest bırakmıştır. Ancak, aktarım kuyruğunda QoS düzey 1 iletilerini serbest bırakmaz. Clean_session bayrağı _ NX_FALSE olarak ayarlanırsa QoS _*_düzey_*_ 1 *_iletileri bağlantıdan sonra NX_FALSE._**

Aracı, istemciyle bağlantıyı da kes olabilir. İstemci ile aracı arasındaki TCP bağlantısı sonlandırılana kadar, disconnect notify işlevi uygulama hakkında bilgi edinebilir. Uygulama, bildirim mekanizmasını kullanmak için * nxd_mqtt_client_disconnect_notify_set* çağrısıyla disconnect notify **işlevini yüklemektedir.** TCP bağlantısının kesilmesi gözlemlendi ve MQTT oturumu oluşturulduktan sonra bildirim işlevi çağrılır.

nxd_mqtt_client_delete() ***çağrısı,*** aktarım kuyruğu ve alma kuyruğunda tüm ileti bloklarını serbest bıraktır. Doğrulanmamış QoS düzey 1 iletileri de silinir.

## <a name="secure-mqtt-connection"></a>Güvenli MQTT Bağlantısı

MQTT istemcisi, NetX Secure TLS modülünü kullanarak aracıyla güvenli bir bağlantı sağlar. TLS güvenliğine sahip MQTT için varsayılan bağlantı noktası numarası 8883'tir ve NXD_MQTT_TLS_PORT.

Aracıyla güvenli bir MQTT bağlantısı oluşturmak için, MQTT CONNECT iletilerinin aracıya gönderilenemeden önce TCP bağlantısı kurulduktan sonra BIR TLS oturumu üzerinde anlaşma yapılması gerekir. TLS oturumu kurulumu, ***nxd_mqtt_client_secure_connect() çağrılarak*** ve kullanıcı tanımlı TLS kurulumu geri çağırma işlevi ileterek başarılı olur. MQTT bağlantı aşamasında, TCP bağlantısı kurulduktan sonra, istemci uygun bir TLS el sıkışma işlemi başlatmak için TLS kurulum geri çağırma işlevini çağırır. TLS oturumu kurulduktan sonra, istemci güvenli kanal üzerinden MQTT CONNECT iletisine devam eder.

Kullanıcı tanımlı geri çağırma işlevi beş giriş değeri alır ve şu şekilde tanımlanır:

```c
UINT tls_Setup_callback(NXD_MQTT_CLIENT *client_ptr,
    NX_SECURE_TLS_SESSION *session_ptr,
    NX_SECURE_TLS_CERTIFICATE *certificate_ptr,
    NX_SECURE_TLS_CERTIFICATE *trusted_cerfiticate);
```

Giriş parametrelerinin açıklaması aşağıda verilmiştir:

- **client_ptr:** MQTT istemci denetim bloğuna işaretçi.
- **session_ptr:** TLS oturum denetim bloğuna işaretçi.
- **certificate_ptr:** Sertifika denetim bloğuna işaretçi. Kurulum işlevi, aracıya göndermeden önce bu sertifikayı yapılandırıyor.
- **trusted_certificate_ptr:** Güvenilen sertifikanın işaretçisi. TLS kurulum işlevi, sunucunun kimliğini doğrulamak için güvenilen sertifikayı yapılandırıyor.

TLS kurulum işlevinde, uygulama bir TLS oturumu oluşturmak ve oturumu uygun bir sertifikayla yapılandırmakla sorumludur. Aşağıdaki sahte kod tipik bir TLS oturumu başlatma yordamını özetler. Okuyucu, TLS API'lerini kullanma hakkında ayrıntılı bilgi için NetX Secure TLS Kullanıcı Kılavuzu'ne başvurur.

Aşağıda örnek bir TLS kurulum geri çağrısı verilmiştir:

```c
UINT tls_setup_callback(NXD_MQTT_CLIENT *client_pt
    NX_SECURE_TLS_SESSION *session_ptr,
    NX_SECURE_TLS_CERTIFICATE *certrifcate_ptr,
    NX_SECURE_TLS_CERTIFICATE *trusted_certificate_ptr)
{
    /* Initialize TLS module */
    nx_secure_tls_initialize();

    /* Create a TLS session */
    nx_secure_tls_session_create(session_ptr, …);

    /* Need to allocate space for the certificate coming in from the broker. */
    memset(certificate_ptr), 0, sizeof(NX_SECURE_TLS_CERTIFICATE));

    nx_secure_tls_remote_certificate_allocate(session_ptr, certificate_ptr);

    /* Add a CA Certificate to our trusted store for verifying incomingserver certificates. */
    nx_secure_tls_certificate_initialize(
        trusted_certificate_ptr,
        ca_cert_der,
        ca_cert_der_len, NULL, 0);
    nx_secure_tls_trusted_certificate_add(session_ptr,
        trusted_certificate));
}
```

## <a name="known-limitations-of-the-netx-duo-mqtt-client"></a>NetX Duo MQTT İstemcisi'nin Bilinen Sınırlamaları

- NetX Duo MQTT, QoS düzey 2 iletilerinin gönderilmesini veya gönderilmesini desteklemez.
- NetX Duo MQTT zincirli paketleri desteklemez.
