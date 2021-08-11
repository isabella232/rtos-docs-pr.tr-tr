---
title: Bölüm 1-Azure RTOS NetX Duo Telnet 'e giriş
description: Azure RTOS NetX Duo Telnet, Internet 'teki iki düğüm arasındaki komutları ve yanıtları aktarmak için tasarlanan bir protokoldür.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 50a2c4d8726863f4e609debadd9ddf2455cfd540219a476970756d3d250ec562
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116799039"
---
# <a name="chapter-1---introduction-to-the-azure-rtos-netx-duo-telnet"></a>Bölüm 1-Azure RTOS NetX Duo Telnet 'e giriş

Azure RTOS NetX Duo Telnet, Internet 'teki iki düğüm arasındaki komutları ve yanıtları aktarmak için tasarlanan bir protokoldür. Telnet, aktarım işlevini gerçekleştirmek için güvenilir Iletim Denetimi Protokolü (TCP) hizmetlerinden yararlanan basit bir protokoldür. Bu nedenle, Telnet son derece güvenilir bir aktarım protokolüdür. Telnet, en çok kullanılan uygulama protokollerinden de biridir.

## <a name="telnet-requirements"></a>Telnet gereksinimleri

NetX Duo Telnet paketi düzgün çalışması için bir NetX IP örneğinin zaten oluşturulmuş olmasını gerektirir. Ayrıca, aynı IP örneğinde TCP 'nin etkinleştirilmesi gerekir. NetX Duo Telnet paketinin Telnet Istemci bölümü başka gereksinimlere sahip değildir.

NetX Duo Telnet paketinin Telnet sunucu bölümünde bir ek gereksinim vardır. Tüm Istemci Telnet isteklerini işlemek için, TCP *iyi bilinen bağlantı noktası 23* ' e tam erişim gerektirir.

## <a name="telnet-constraints"></a>Telnet kısıtlamaları 

NetX Duo Telnet protokolü, Telnet standardını uygular. Ancak, 255 değerine sahip bir bayt tarafından gösterilen Telnet komutlarının yorumu ve yanıtı uygulamanın sorumluluğundadır. Çeşitli Telnet komutları ve komut parametreleri *nxd_telnet_client. h ve nxd_telnet_server. h* dosyalarında tanımlanmıştır.

## <a name="telnet-communication"></a>Telnet Iletişimi

Daha önce belirtildiği gibi, Telnet sunucusu *iyi BILINEN TCP bağlantı noktası 23* Ile alan istemci isteklerini kullanır. Telnet Istemcileri, kullanılabilir herhangi bir TCP bağlantı noktasını kullanabilir.

## <a name="telnet-authentication"></a>Telnet kimlik doğrulaması

Telnet kimlik doğrulaması, uygulamanın Telnet sunucusu geri çağırma işlevinin sorumluluğundadır. Uygulamanın Telnet sunucusu "yeni bağlantı" geri çağırması genellikle Istemciye ad ve/veya parola ister. Daha sonra, Istemci bilgileri sağlamaktan sorumludur. Sunucu daha sonra "verileri al" geri aramasında bilgileri işleyebilir. Bu, uygulama sunucusu kodunun bilgilerin kimliğini doğrulamak ve geçerli olup olmadığına karar vermek zorunda olduğu yerdir.

## <a name="telnet-new-connection-callback"></a>Telnet yeni bağlantı geri çağırması

NetX Duo Telnet sunucusu, her yeni Telnet Istemci isteği alındığında uygulama tarafından belirtilen geri çağırma işlevini çağırır. Uygulama, Telnet sunucusu ***nx_telnet_server_create*** işlevi aracılığıyla oluşturulduğunda geri çağırma işlevini belirtir. "Yeni bağlantı" geri çağrısının tipik eylemleri, Istemciye bir başlık veya istem göndermeyi içerir. Bu, oturum açma bilgileri için bir istem de içerebilir.

### <a name="prototype"></a>Prototype

```c
void  telnet_new_connection(NX_TELNET_SERVER *server_ptr, 
                            UINT logical_connection);
```

### <a name="input-parameters"></a>Giriş Parametreleri

- **server_ptr**: çağıran Telnet sunucusuna yönelik işaretçi.
- **logical_connection**: Telnet sunucusu için iç mantıksal bağlantı. Bu, uygulama tarafından, her Istemci bağlantısına özel arabellekler ve/veya veri yapılarına bir dizin olarak kullanılabilir. Değeri 0 ile NX_TELNET_MAX_CLIENTS-1 arasında değişir.

## <a name="telnet-receive-data-callback"></a>Telnet veri geri araması al

NetX Duo Telnet sunucusu, her yeni Telnet Istemci verisi alındığında uygulamanın belirttiği geri arama işlevini çağırır. Uygulama, Telnet sunucusu ***nx_telnet_server_create*** işlevi aracılığıyla oluşturulduğunda geri çağırma işlevini belirtir. "Yeni bağlantı" geri çağrısının tipik eylemleri, verileri geri ve/veya verileri ayrıştırmayı ve istemciden bir komutun yorumlanmasından kaynaklanan verileri sağlamayı içerir.

Bu geri arama yordamının sağlanan paketi de serbest bırakmalıdır.

### <a name="prototype"></a>Prototype

```c
void  telnet_receive_data(NX_TELNET_SERVER *server_ptr, 
                          UINT logical_connection, NX_PACKET *packet_ptr);
```
### <a name="input-parameters"></a>Giriş Parametreleri

- **server_ptr**: çağıran Telnet sunucusuna yönelik işaretçi.
- **logical_connection**: Telnet sunucusu için iç mantıksal bağlantı. Bu, uygulama tarafından, her Istemci bağlantısına özel arabellekler ve/veya veri yapılarına bir dizin olarak kullanılabilir. Değeri 0 ile NX_TELNET_MAX_CLIENTS-1 arasında değişir.
- **packet_ptr**: istemciden verileri içeren paket işaretçisi.

## <a name="telnet-end-connection-callback"></a>Telnet uç bağlantısı geri çağırması

NetX Duo Telnet sunucusu, bir Telnet Istemcisi bağlantıyı sona erdirdiğinde, uygulama tarafından belirtilen geri çağırma işlevini çağırır. Uygulama, Telnet sunucusu ***nx_telnet_server_create*** işlevi aracılığıyla oluşturulduğunda geri çağırma işlevini belirtir. "Bağlantıyı Sonlandır" geri çağrısının tipik eylemleri, mantıksal bağlantıyla ilişkili tüm Istemci özel veri yapılarını temizlemeyi içerir.

### <a name="prototype"></a>Prototype
```c
void  telnet_end_connection(NX_TELNET_SERVER *server_ptr, 
                            UINT logical_connection);
```

### <a name="input-parameters"></a>Giriş Parametreleri

- **server_ptr** Çağıran Telnet sunucusu işaretçisi.
- **logical_connection** Telnet sunucusu için dahili mantıksal bağlantı. Bu, uygulama tarafından, her Istemci bağlantısına özel arabellekler ve/veya veri yapılarına bir dizin olarak kullanılabilir. Değeri 0 ile NX_TELNET_MAX_CLIENTS-1 arasında değişir.

## <a name="telnet-option-negotiation"></a>Telnet seçeneği anlaşması

NetX Duo Telnet sunucusu, sınırlı bir Telnet seçenekleri kümesini destekler, yankı ve gizleme devam edin.

Bu özelliği etkinleştirmek için NX_TELNET_SERVER_OPTION_DISABLE tanımlanmamış olmalıdır. Varsayılan olarak tanımlı değildir. Telnet sunucusu *nx_telnet_server_create* hizmetinde, istemciye Telnet seçenekleri isteklerinin gönderilmesi için paket ayırabileceği bir paket havuzu oluşturur. Bu paket havuzu için paket yükünü (NX_TELNET_SERVER_PACKET_PAYLOAD) ve paket havuzu boyutunu (NX_TELNET_SERVER_PACKET_POOL_SIZE) ayarlamaya yönelik "yapılandırma seçenekleri" bölümüne bakın. *Nx_telnet_server_delete* hizmeti çağrıldığında bu paket havuzunu silecektir.

Telnet Istemcisiyle bağlantı kurulduğunda, Istemciden seçenek istekleri almamışsa, bu Telnet seçenekleri kümesinin Istemciye gönderilmesi gerekir:

- yankı eder
- yankı verme
- SGA olacak

Istemciden Telnet verileri aldığında, Telnet sunucusu ilk baytın "ıAC" kodu olup olmadığını denetler. Bu durumda, Istemci paketindeki tüm seçenekleri işleyecek olur. Yukarıdaki listede bulunmayan seçenekler yok sayılır.

Varsayılan olarak, NX_TELNET_SERVER_OPTION_DISABLE tanımlanmamışsa ve Telnet seçenek komutlarını iletilmesi gerekiyorsa, Telnet sunucusu kendi iç paket havuzunu oluşturur. Telnet sunucusu paket havuzu NX_TELNET_SERVER_PACKET_PAYLOAD ve NX_TELNET_SERVER_PACKET_POOLSIZE tarafından tanımlanır. Ancak, NX_TELNET_SERVER_USER_CREATE_PACKET_POOL tanımlanmışsa, uygulamanın Telnet sunucusu paket havuzunu oluşturması ve *_nx_telnet_server_packet_pool_set* çağırarak Telnet sunucusu paket havuzu olarak ayarlaması gerekir. Bu işlev hakkında daha fazla bilgi için bkz. Bölüm 3 "Telnet Services açıklaması".

NetX Duo Telnet sunucusunun aksine NetX Duo Telnet Istemcisi görev iş parçacığı, Telnet sunucusundan alınan seçenekleri otomatik olarak göndermez ve vermez. Bu, Telnet Istemci uygulaması tarafından yapılmalıdır.

## <a name="telnet-multi-thread-support"></a>Telnet çoklu Iş parçacığı desteği

NetX Duo Telnet Istemci hizmetleri aynı anda birden çok iş parçacığından çağrılabilir. Ancak, belirli bir Telnet Istemci örneği için okuma veya yazma istekleri aynı iş parçacığından sırayla yapılmalıdır.

## <a name="telnet-rfcs"></a>Telnet RFC 'Leri

NetX Duo Telnet, RFC854 ve ilgili RFC 'lerle uyumludur.
