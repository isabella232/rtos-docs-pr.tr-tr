---
title: Bölüm 1-Azure RTOS NetX Duo MQTT 'ye giriş
description: NetX Duo MQTT istemci paketi, NetX Duo (sürüm 5,10 veya üzeri) yüklü olmasını, düzgün şekilde yapılandırılmasını ve IP örneğinin oluşturulmasını gerektirir.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 2e13b997f987e2fd82569bcb1904218908313d70
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825912"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-mqtt"></a>Bölüm 1-Azure RTOS NetX Duo MQTT 'ye giriş

## <a name="netx-duo-mqtt-requirements"></a>NetX Duo MQTT gereksinimleri

Azure RTOS NetX Duo MQTT istemci paketi, NetX Duo (sürüm 5,10 veya üzeri) yüklü olmasını, düzgün şekilde yapılandırılmasını ve IP örneğinin oluşturulmasını gerektirir. TCP modülünün sistemde etkinleştirilmiş olması gerekir. Ayrıca, TLS güvenliği gerekliyse, NetX güvenli TLS modülünün, aracı tarafından istenen güvenlik parametresine göre yapılandırılması gerekir.

## <a name="netx-duo-mqtt-specification"></a>NetX Duo MQTT belirtimi

NetX Duo MQTT Client uygulaması, OASSıS MQTT sürümü 3.1.1<sup>on</sup> 29 ' dan fazla 2014 ile uyumludur. Belirtimi şurada bulunabilir:

- [http://mqtt.org/](http://mqtt.org/)

## <a name="netx-duo-mqtt-basic-operation"></a>NetX Duo MQTT temel Işlemi

MQTT (Ileti kuyruğu telemetri aktarımı) Yayımcı-abone modeline dayalıdır. İstemci, bir aracı aracılığıyla diğer istemcilere bilgi yayımlayabilir. Bir konuyla ilgileniyorsa bir istemci, aracı aracılığıyla konuya abone olabilir. Bir aracı, yayınlanmış iletileri konuya abone olan istemcilerine dağıtmaktan sorumludur. Bu Yayımcı-abone modelinde, birden çok istemci aynı konuyla veri yayımlayabilir. İstemci aynı konuya abone olursa istemci yayımladığı bir ileti alır.

Kullanım örneğine bağlı olarak, bir istemci bir ileti yayımlarken 3 QoS düzeyinden birini seçebilir:

- **QoS 0**: ileti en fazla bir kez teslim edilir. QoS 0 ile gönderilen iletiler kaybolmuş olabilir.
- **QoS 1**: ileti en az bir kez teslim edilir. QoS 1 ile gönderilen iletiler birden çok kez teslim edilebilir.
- **QoS 2**: ileti tam olarak bir kez teslim edilir. QoS 2 ile gönderilen iletilerin, çoğaltma olmadan teslim edilmesi garanti edilir.

> [!NOTE]
> MQTT istemcisinin bu uygulama, QoS düzey 2 iletilerini desteklemez.

QoS 1 ve QoS 2 ' nin teslim edileceği garanti edildiğinden, aracı, her istemciye gönderilen QoS 1 ve QoS 2 iletilerinin durumunu izler. Bu, özellikle QoS1 veya QoS 2 iletileri bekleyen istemciler için önemlidir. İstemcinin aracısıyla bağlantısı kesilebilir (örneğin, istemci yeniden başlatıldığında veya iletişim bağlantısı geçici olarak kaybedilmişse). Aracı, istemci aracısına yeniden bağlandığında iletilerin daha sonra teslim edilebilmesi için QoS 1 ve QoS 2 iletilerini depolamalıdır. Bununla birlikte, istemci yeniden bağlandıktan sonra aracıdan eski ileti almamayabilir. İstemci, *clean_session* bayrağı ***NX_TRUE** _ olarak ayarlanmış şekilde bağlantıyı başlatarak bunu yapabilir. Bu durumda, MQTT CONNECT iletisini aldıktan sonra, aracı bu istemciyle ilişkili oturum bilgilerini, teslim edilmemiş ya da onaylanmamış QoS 1 veya QoS 2 iletileri de dahil olmak üzere atar. _Clean_session * bayrağı ***NX_FALSE** Ise_, sunucu QoS 1 ve QoS 2 iletilerini yeniden gönderecektir. MQTT Istemcisi, _clean_session *, ***NX_TRUE *** olarak ayarlandıysa, kabul edilmeyen hiçbir iletiyi de yeniden sonlandırır. Bu onay, TCP katmanı ACK 'ten farklıdır, ancak aynı zamanda olur. MQTT istemcisi, aracıya bir bildirim gönderir.

Uygulama, ***nxd_mqtt_client_create ()** _ öğesini çağırarak MQTT istemci örneği oluşturur. İstemci oluşturulduktan sonra uygulama, _*_nxd_mqtt_client_connect ()_*_ öğesini çağırarak aracıya bağlanabilir. Aracıya bağlandıktan sonra istemci, _*_nxd_mqtt_client_subscribe ()_*_ çağırarak bir konuya abone olabilir veya _ *_nxd_mqtt_client_publish ()_* * çağırarak bir konuyu yayımlayabilir.

Gelen MQTT iletileri, MQTT istemci örneğindeki alma sırasında depolanır. Uygulama, ***nxd_mqtt_client_message_get ()*** çağırarak bu iletiyi alır. Alma kuyruğunda iletiler varsa, sıradaki ilk ileti (örneğin, en eski) çağırana döndürülür. İletideki konu dizesi de döndürülür.

> [!NOTE]
> ***Nxd_mqtt_client_message_get ()** _ IşLEVI MQTT istemcisi alma kuyruğu boş ise engellemez. İşlev, hemen dönüş kodu _ *_NXD_MQTT_NO_MESSAGE_* * ile döndürür. Uygulama, bu dönüş değerini alma sırasının bir hata değil boş olduğunu belirten bir gösterge olarak değerlendirir.

Gelen iletiler için alma sırasının yoklanmaması için, uygulama ***nxd_mqtt_client_recieve_notify_set ()*** çağırarak MQTT istemcisiyle bir geri çağırma işlevi kaydedebilir. Geri çağırma işlevi şöyle bildirilmiştir:

```c
VOID (*receive_notify_callback)(NXD_MQTT_CLIENT *client_ptr, 
    UINT message_count);
```

MQTT istemcisi aracıdan ileti aldığında, işlev ayarlandıysa geri çağırma işlevini çağırır. Geri arama işlevi, işaretçiyi istemci denetim bloğuna ve bir ileti sayısı değerine geçirir. İleti sayısı değeri, alma sırasındaki MQTT iletilerinin sayısını gösterir. Bu geri çağırma işlevinin MQTT istemci iş parçacığı bağlamında yürütüldüğünü unutmayın. Bu nedenle, geri çağırma işlevi MQTT istemci iş parçacığını engelleyebilen herhangi bir yordam yürütmemelidir. Geri çağırma işlevi, iletileri almak için ***nxd_mqtt_client_message_get ()*** çağırmak üzere uygulama iş parçacığını tetiklemelidir.

MQTT istemci hizmetinin bağlantısını kesmek ve sonlandırmak için uygulama, ***nxd_mqtt_client_disconnect ()** _ ve _*_nxd_mqtt_client_delete ()_*_ hizmetini kullanır. _*_Nxd_mqtt_client_disconnect ()_*_ çağırmak, yalnızca ARACıYA TCP bağlantısını keser. Alma kuyruğunda zaten alınmış ve depolanmış iletileri yayınlar. Ancak, iletme sırasında QoS düzey 1 iletileri serbest bırakmaz. _*_Clean_session_*_ bayrağının _ NX_FALSE olarak ayarlandığı varsayıldığında, QoS düzey 1 iletileri bağlantı kurulduğunda yeniden gönderilir *_._**

Aracı da istemciyle bağlantısını kesebilir. İstemci ve aracı arasındaki TCP bağlantısı sonlandırıldığında, uygulamaya bağlantıyı kes bildirim işlevi tarafından bildirim uygulanabilir. Uygulama bildirim mekanizmasını kullanmak için, ***nxd_mqtt_client_disconnect_notify_set *** çağırarak bağlantı kesme bildirme işlevini de yüklüyor. TCP bağlantısı kesildikten ve MQTT oturumu oluşturulduktan sonra, bildirim işlevi çağrılır.

***Nxd_mqtt_client_delete ()*** çağrısı, iletme sırasındaki tüm ileti bloklarını ve alma sırasını yayınlar. Kabul edilmemiş QoS düzey 1 iletileri de silinir.

## <a name="secure-mqtt-connection"></a>Güvenli MQTT bağlantısı

MQTT istemcisi, NetX güvenli TLS modülünü kullanarak aracıya güvenli bir bağlantı oluşturur. TLS 8883 güvenliği ile MQTT için varsayılan bağlantı noktası numarası ***NXD_MQTT_TLS_PORT*** tanımlanmıştır.

Aracıya güvenli bir MQTT bağlantısı oluşturmak için, bir TCP bağlantısı kurulduktan sonra, bir TLS oturumunun, ücret'e gönderilen MQTT CONNECT iletileri gönderilmeden önce anlaşması gerekir. TLS oturum ayarları, ***nxd_mqtt_client_secure_connect ()*** çağırarak ve Kullanıcı TANıMLı bir TLS Kurulumu geri arama işlevinde geçirilerek gerçekleştirilir. MQTT bağlantı aşamasında, TCP bağlantısı kurulduktan sonra istemci, doğru bir TLS el sıkışma işlemini başlatmak için TLS kurulum geri arama işlevini çağırır. TLS oturumu kurulduktan sonra istemci, güvenli kanal üzerinden MQTT CONNECT iletisini devam ettirir.

Kullanıcı tanımlı geri çağırma işlevi beş giriş değeri alır ve şu şekilde bildirilmiştir:

```c
UINT tls_Setup_callback(NXD_MQTT_CLIENT *client_ptr,
    NX_SECURE_TLS_SESSION *session_ptr,
    NX_SECURE_TLS_CERTIFICATE *certificate_ptr,
    NX_SECURE_TLS_CERTIFICATE *trusted_cerfiticate);
```

Giriş parametrelerinin açıklaması aşağıda verilmiştir:

- **client_ptr**: MQTT istemci denetim bloğuna yönelik işaretçi.
- **session_ptr**: TLS oturum denetim bloğuna yönelik işaretçi.
- **certificate_ptr**: sertifika denetim bloğuna yönelik işaretçi. Kurulum işlevi bu sertifikayı aracıya göndermeden önce yapılandırır.
- **trusted_certificate_ptr**: güvenilen sertifikaya yönelik işaretçi. TLS kurulum işlevi, sunucunun kimliğini doğrulamak için güvenilen sertifikayı yapılandırır.

TLS kurulum işlevinde, uygulama bir TLS oturumu oluşturmaktan ve oturumu uygun bir sertifikayla yapılandırmadan sorumludur. Aşağıdaki sözde kod tipik bir TLS oturumu başlatma yordamını özetler. Okuyucu, TLS API 'Leri kullanma hakkında ayrıntılı bilgi için NetX güvenli TLS Kullanıcı Kılavuzu 'na başvurulur.

Aşağıda bir TLS kurulum geri çağırması verilmiştir:

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

## <a name="known-limitations-of-the-netx-duo-mqtt-client"></a>NetX Duo MQTT Istemcisinin bilinen sınırlamaları

- NetX Duo MQTT, QoS düzey 2 iletilerinin gönderilmesini veya alınmasını desteklemez.
- NetX Duo MQTT, zincirleme paketleri desteklemez.
