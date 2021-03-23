---
title: Bölüm 2-Azure RTOS NetX LWM2M yükleme ve kullanımı
description: Bu bölümde, Azure RTOS NetX LWM2M bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların bir açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 8c13d3b092d3a5b59bd0369f6ffc162509d02590
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826699"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-lwm2m"></a>Bölüm 2-Azure RTOS NetX LWM2M yükleme ve kullanımı

Bu bölümde, Azure RTOS NetX LWM2M bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların bir açıklaması yer almaktadır.

## <a name="product-distribution"></a>Ürün dağıtımı

NetX LWM2M, adresinde bulunabilir [https://github.com/azure-rtos/netx](https://github.com/azure-rtos/netx) . Bu paket üç kaynak dosyası, bir içerme dosyası ve bu belgeyi içeren bir PDF dosyası içerir ve aşağıdaki gibi:

- **nx_lwm2m_client. h**: NETX lwm2m istemcisi için üst bilgi dosyası

- **nx_lwm2m_ *. c/h**: NETX lwm2m için c/h kaynak dosyaları

- **demo_netx_lwm2m_client. c**: NETX Lwm2m istemci tanıtımı Için c kaynak dosyası

- **NetX_LWM2M_User_Guide.pdf**: NETX LWM2M ürününün PDF açıklaması

## <a name="netx-lwm2m-installation"></a>NetX LWM2M yüklemesi

NetX LWM2M kullanabilmeniz için, daha önce bahsedilen dağıtımın tamamı NetX 'in yüklü olduğu dizine kopyalanmalıdır. Örneğin, NetX, "*\\ threadx \\ ARM7 \\ green*" dizinine yüklenirse *nx_lwm2m&#42;. &#42;* dosyaları bu dizine kopyalanmalıdır.

## <a name="using-netx-lwm2m"></a>NetX LWM2M kullanma

NetX LWM2M kullanmak kolaydır. Temel olarak uygulama kodu, ThreadX ve NetX kullanmak için *tx_api. h* ve *nx_api. h* dahil *nx_lwm2m_client. h* 'yi içermelidir. *Nx_lwm2m_client. h* dahil olduğunda, uygulama kodu daha sonra bu kılavuzda belirtilen NETX lwm2m işlev çağrılarını yapabilir. Uygulamanın Ayrıca, *nx_lwm2m&#42;. &#42;* dosyalarını NETX kitaplığına aktarması gerekir.

## <a name="configuration-options"></a>Yapılandırma seçenekleri

LWM2M Istemci kitaplığı ve uygulamayı LWM2M Istemcisini kullanarak oluştururken birkaç yapılandırma seçeneği vardır. Yapılandırma seçenekleri, aksi belirtilmediği takdirde, komut satırında, uygulama kaynağında tanımlanabilir.

### <a name="nx_lwm2m_client_disable_error_checking"></a>NX_LWM2M_CLIENT_DISABLE_ERROR_CHECKING

Tanımlanmıştır, temel LWM2M Istemci hata denetimi API 'sini kaldırır ve performansı geliştirir. Hata denetimini devre dışı bırakarak etkilenmeyen API dönüş kodları, API tanımında kalın yazı tipiyle listelenmiştir.

### <a name="nx_lwm2m_client_disable_float"></a>NX_LWM2M_CLIENT_DISABLE_FLOAT

Tanımlanmış, kayan nokta numarası değerlerinin desteğini kaldırır. Devre dışı bırakıldığında LWM2M Istemcisi float veri türüne sahip kaynakları desteklemez.

### <a name="nx_lwm2m_client_disable_float64"></a>NX_LWM2M_CLIENT_DISABLE_FLOAT64

Tanımlı, 64 bitlik kayan nokta sayı değerlerinin desteğini kaldırır. LWM2M Istemcisi 64 bitlik kayan sayılar içeren TLV iletileri almaya devam edebilir, ancak değerler işlenmek üzere 32 bitlik kayan noktaya dönüştürülür.

### <a name="nx_lwm2m_client_priority"></a>NX_LWM2M_CLIENT_PRIORITY

LWM2M Istemci iş parçacığının önceliğini belirtir. Varsayılan olarak, 16 önceliğini belirtmek için bu değer 16 olarak tanımlanır.

### <a name="nx_lwm2m_client_max_device_errors"></a>NX_LWM2M_CLIENT_MAX_DEVICE_ERRORS

Cihaz nesnesi tarafından depolanan en fazla hata kodu sayısını belirtir. Varsayılan değer 8 ' dir.

### <a name="nx_lwm2m_client_max_security_instances"></a>NX_LWM2M_CLIENT_MAX_SECURITY_INSTANCES

En fazla güvenlik nesnesi örneği sayısını belirtir. Varsayılan değer, bir önyükleme sunucusunu ve standart sunucuyu desteklemek için 2 ' dir.

### <a name="nx_lwm2m_client_max_server_instances"></a>NX_LWM2M_CLIENT_MAX_SERVER_INSTANCES

En fazla sunucu nesne örneği sayısını belirtir. Tek bir standart sunucuyu desteklemek için varsayılan değer 1 ' dir.

### <a name="nx_lwm2m_client_max_server_uri"></a>NX_LWM2M_CLIENT_MAX_SERVER_URI

Bir sunucu URI 'sinin Sonlandırıcı karakteri de dahil olmak üzere maksimum uzunluğunu belirtir. Varsayılan değer 128 ' dir.

### <a name="nx_lwm2m_client_max_access_control_instances"></a>NX_LWM2M_CLIENT_MAX_ACCESS_CONTROL_INSTANCES

En fazla Access Control örneği sayısını belirtir. Varsayılan değer 0 ' dır ve bu, erişim denetimini devre dışı bırakır. Uygulama birden fazla LWM2M sunucusunu destekliyorsa, her bir nesne örneği (güvenlik nesnesi örnekleri hariç) için bir Access Control örneği oluşturulması gerektiği için, en fazla Access Control örnek sayısı, LWM2M Istemcisinin destekleyeceği en fazla nesne örneği sayısına ayarlanmalıdır.

### <a name="nx_lwm2m_client_max_access_control_acls"></a>NX_LWM2M_CLIENT_MAX_ACCESS_CONTROL_ACLS

Access Control örnek başına en fazla ACL kaynağı sayısını belirtir. Varsayılan değer 4'tür.

### <a name="nx_lwm2m_client_max_notifications"></a>NX_LWM2M_CLIENT_MAX_NOTIFICATIONS

LWM2M Istemcisinin destekleyeceği en fazla bildirim sayısını belirtir. Bir LWM2M sunucusu nesneler, nesne örnekleri ve kaynaklar üzerinde bildirimler ayarlayabilir. Varsayılan değer 8 ' dir.

### <a name="nx_lwm2m_client_max_resources"></a>NX_LWM2M_CLIENT_MAX_RESOURCES

Nesne başına en fazla kaynak sayısını belirtir. Varsayılan değer 32 ' dir.

### <a name="nx_lwm2m_client_bootstrap_idle_timer"></a>NX_LWM2M_CLIENT_BOOTSTRAP_IDLE_TIMER

Oturumu iptal etmeden önce önyükleme oturumu başlatıldığında önyükleme sunucusu istekleri için beklenecek en uzun süreyi belirtir. Varsayılan değer 60 saniyedir.

### <a name="nx_lwm2m_client_dtls_start_timeout"></a>NX_LWM2M_CLIENT_DTLS_START_TIMEOUT

DTLS el sıkışma tamamlanması için beklenecek en uzun süreyi belirtir. Varsayılan değer 30 saniyedir.

### <a name="nx_lwm2m_client_dtls_end_timeout"></a>NX_LWM2M_CLIENT_DTLS_END_TIMEOUT

DTLS kapatması işleminin tamamlanması için beklenecek en uzun süreyi belirtir. Varsayılan değer 5 saniyedir.
