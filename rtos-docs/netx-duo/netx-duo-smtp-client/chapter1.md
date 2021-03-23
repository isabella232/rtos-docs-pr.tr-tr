---
title: Bölüm 1-Azure RTOS NetX Duo SMTP istemcisine giriş
description: Basit Posta Aktarım Protokolü (SMTP), ağları ve Internet arasında posta aktarmaya yönelik bir protokoldür.
author: philmea
ms.author: philmea
ms.date: 07/09/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: f58a0c235f5c2cd108ba97afe676ffa9b66e715c
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825793"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-smtp-client"></a>Bölüm 1-Azure RTOS NetX Duo SMTP istemcisine giriş

Basit Posta Aktarım Protokolü (SMTP), ağları ve Internet arasında posta aktarmaya yönelik bir protokoldür. Güvenli Iletim Denetim Protokolü (TCP) hizmetlerinden yararlanır ve bu, içerik aktarım işlevini gerçekleştirir.

## <a name="netx-duo-smtp-client-requirements"></a>NetX Duo SMTP Istemci gereksinimleri

NetX Duo SMTP Istemcisi, bir NetX Duo IP örneği ve NetX Duo paket havuzu oluşturulmasını gerektirir. SMTP Istemcisi, bir SMTP sunucusuna, *iyi bilinen 25 numaralı bağlantı noktasında bağlanmak için BIR TCP yuvası kullanır. Bu nedenle*, önce daha önce oluşturulmuş BIR IP örneğinde *nx_tcp_enable* hizmeti çağırarak TCP 'nin etkinleştirilmesi gerekir.

SMTP Istemcisi oluşturma çağrısı (nxd_smtp_client_create), SMTP komutlarının sunucuya iletilmesi ve gerçek posta iletisinin gönderilmesi için önceden oluşturulmuş bir paket havuzu gerektirir. Paket yükü, posta içeriğinin beklenen boyutuna bağlıdır ve TCP, IP üstbilgisi ve MAC üst bilgisine izin vermelidir. (IPv4 üst bilgisi 20 bayt olduğunda IPv6 üstbilgisinin 40 bayt olduğunu unutmayın.)

Tüm posta iletisi bir pakete sığamayacak olursa, SMTP Istemcisi iletiyi geri kalanı içerecek şekilde ek paketler ayırır.

## <a name="netx-duo-smtp-client-constraints"></a>NetX Duo SMTP Istemci kısıtlamaları

NetX Duo SMTP protokolü, RFC 2821 ve 2554 standartları uyguladığı sırada bazı kısıtlamalar vardır:

1. NetX Duo SMTP Istemcisi yalnızca oturum açma ve düz kimlik doğrulamasını destekler, ancak Crae-MD5 Özet kimlik doğrulamasını desteklememektedir.
2. NetX Duo SMTP Istemci iletileri, posta öğesi başına bir alıcı ile sınırlıdır ve SMTP sunucusu ile TCP bağlantısı başına yalnızca bir posta iletisi kullanılır.
3. VRMY, SEND, SOML, EXPN, SAML, ETRN, aç ve BOYUTLANDıR SMTP seçenekleri desteklenmez.
4. SMTP Istemcisi, genellikle posta iletisini oluşturmak için kullanılan posta tarayıcısı ("posta Kullanıcı Aracısı") değil. Yalnızca bir "posta aktarım aracısıdır". Bu işlem, RFC 2821 ' de belirtildiği gibi SMTP taşıması için posta iletisi gövdesinin gerekli şekilde işlenmesini sağlar. Örneğin, alıcı ve ters patika gibi doğru sözdiziminin içeriğini denetlemez. Posta arabelleğindeki bir kısıtlama yoktur, örneğin MIME verileri veya şifresiz metin iletileri. Üst bilgiler ve ileti gövdesi dahil olmak üzere RFC 2822 ' de belirtilen posta iletisi biçimi SMTP Istemcisi API 'sinin kapsamı dışındadır.

## <a name="commands-supported-by-netx-duo-smtp-client"></a>NetX Duo SMTP Istemcisi tarafından desteklenen komutlar

NetX Duo SMTP Istemcisi, bir SMTP sunucusu ile posta oturumu sırasında aşağıdaki komutları kullanır.

- **EHLO** Istemci, SMTP sunucusundan erişilebilen bir veya daha fazla uzantı Protokolü SMTP hizmeti içeren bir oturum başlatmak ister. Bu varsayılan seçenektir.
- **Helo** Istemci, temel SMTP hizmetleriyle sınırlı bir oturum başlatmak istiyor.
- **Posta** Istemci, sunucunun Istemci postasını almasını ister.
- **Kimlik doğrulaması** Istemci, sunucu tarafından kimlik doğrulaması başlatmak istiyor.
- **Alış** Istemci, e-postanın teslim edilmesini istediğiniz başka bir konağın posta kutusunu göndermek istiyor.
- **Veri** Istemci, sunucuya posta iletisi verisi göndermeyi başlatmak istiyor.
- **Çık** Istemci oturumu sonlandırmak istiyor.

## <a name="getting-started"></a>Kullanmaya Başlama

SMTP Istemci uygulaması bir IP örneği oluşturur ve bu IP örneği üzerinde TCP 'yi etkinleştirmesine izin vermez. Daha sonra aşağıdaki hizmeti kullanarak SMTP Istemcisini oluşturur:

```C
UINT nxd_smtp_client_create(NX_SMTP_CLIENT *client_ptr,
    NX_IP *ip_ptr, NX_PACKET_POOL
    *client_packet_pool_ptr,
    CHAR *username, CHAR *password,
    CHAR *from_address,
    CHAR *client_domain,
    UINT authentication_type,
    NXD_ADDRESS *server_address, UINT port);
```

*Client_packet_pool_ptr* , SMTP Istemcisinin SMTP sunucusuna ileti göndermek için kullanacağı önceden oluşturulmuş bir paket havuzuna yönelik bir işaretçidir.

Bir uygulamanın yerel cihaz için bir *from_address* ve sunucu IP adresi sağlaması gerektiğini unutmayın. Tüm adresler tam etki alanı adları olmalıdır. Tam etki alanı adı, bir ' @ ' karakteriyle ayrılmış bir yerel parça ve bir etki alanı adı içerir. SMTP Istemcisinin, aşağıdaki nx_smtp_mail_send hizmetindeki *from_address* veya *recipient_address* söz dizimini denetmediğini unutmayın.

SMTP istemcisi oluşturulduktan sonra, SMTP Istemci uygulaması düzgün şekilde biçimlendirilen bir SMTP posta iletisi içeren bir posta öğesi oluşturur ve aşağıdaki API 'yi kullanarak posta öğesinin isteği SMTP Istemcisine göndermesini sağlar:

```C
UINT nx_smtp_mail_send(NX_SMTP_CLIENT *client_ptr,
    CHAR *recipient_address, UINT priority,
    CHAR *subject, CHAR *mail_body,
    UINT mail_body_length);
```

Kullanıcı perspektifinden IPv4 veya IPv6 üzerinden SMTP Istemcisi çalıştırmanın bir farkı yoktur. İki IP protokolü arasındaki farklılıklar, temel alınan NetX Duo katmanında işlenir.

E-posta göndermek isteyen bir uygulamanın *nx_smtp_client_mail* çağrısında bir alıcı adresi sağlaması gerektiğini unutmayın.

Kimlik doğrulaması için, Kullanıcı adları tam etki alanı adları olabilir veya Kullanıcı adlarını görüntüleyebilir. Bu, sunucunun kimlik doğrulamasını nasıl gerçekleştirdiğine bağlıdır.

Küçük örnek bölümündeki tanıtım bu kullanıcı kılavuzunda daha sonra iletinin nasıl biçimlendirilmesi gerektiğini gösterir. Posta öğesi başarıyla gönderildiyse durum NX_SUCCESS olur. Bir hata oluşursa, bir iç hata, bozuk bir TCP bağlantısı veya sunucu yanıtı hata kodu alma, *nx_smtp_mail_send* sıfır olmayan bir hata durumu döndürür.

Bir posta öğesi gönderilirken NetX Duo SMTP Istemcisi, SMTP sunucusuyla yeni bir TCP bağlantısı oluşturur ve bir SMTP oturumu başlatır. Bu oturumda, Istemci SMTP protokolünün bir parçası olarak SMTP sunucusuna bir dizi komut gönderir ve gerçek posta iletisini göndermekten çıkar. Bu durumda, SMTP oturumunun sonucuna bakılmaksızın TCP bağlantısı sonlandırılır.

Posta iletimi sonrasında, başarı veya hatadan bağımsız olarak, SMTP Istemcisi ' Başlangıç ' durumuna döndürülür ve başka bir posta aktarım oturumu için kullanılabilir.

## <a name="netx-duo-smtp-authentication"></a>NetX Duo SMTP kimlik doğrulaması

Kimlik doğrulaması, SMTP Istemcilerinin kimliklerini SMTP sunucusuna kanıtlamaları ve e-postalarını Güvenilen Kullanıcı olarak teslim etmek için bir yoldur. Çoğu ticari SMTP sunucusu, Istemcilerin kimlik doğrulamasını gerektirir.

Genellikle, kimlik doğrulama verileri Gönderenin Kullanıcı adı ve parolasıyla oluşur. Kimlik doğrulama sınaması sırasında, sunucu bu bilgileri ister ve Istemci, istenen verileri kodlanmış biçimde göndererek yanıt verir. Sunucu, verilerin kodunu çözer ve Kullanıcı veritabanında bir eşleşme bulmaya çalışır. Bulunursa sunucu, kimlik doğrulamasının başarılı olduğunu gösterir. SMTP kimlik doğrulaması, [RFC 2554](http://www.ietf.org/rfc/rfc2554.txt)' de tanımlanmıştır.

*Temel* ve *Özet* gibi iki kimlik doğrulama özelliği vardır. Özet, geçerli NetX Duo SMTP Istemcisinde desteklenmez ve burada açıklanmayacak. Temel kimlik doğrulaması yukarıda açıklanan *ad* ve *parola* kimlik doğrulamasına eşdeğerdir. SMTP temel kimlik doğrulamasında ad ve parolalar Base64 olarak kodlanır. Temel kimlik doğrulamasının avantajı, uygulama ve yaygın kullanım kolaylığıdır. Temel kimlik doğrulamasının ana dezavantajı, istekte openly olarak iletilir.

### <a name="plain-authentication"></a>Düz kimlik doğrulama

NetX Duo SMTP Istemcisi, düz parametreli bir AUTH komutu gönderir. NetX Duo SMTP sunucusu bu tür bir kimlik doğrulamasını destekliyorsa, 334 yanıt koduyla yanıt gönderir. Istemci, sunucuya tek bir Base64 kodlamalı Kullanıcı adı ve parola iletisi ile yanıt verir. Sunucu Istemci kimlik doğrulamasının başarılı olduğunu belirlerse, 235 başarı koduyla yanıt verir.

### <a name="login-authentication"></a>Oturum açma kimlik doğrulaması

NetX Duo SMTP Istemcisi, oturum açma parametresiyle bir AUTH komutu gönderir. NetX Duo SMTP sunucusu bu tür bir kimlik doğrulamasını destekliyorsa, kimlik doğrulamasının ' Challenge ' başlangıcı olarak 334 yanıt kodu ile yanıt gönderir. Genellikle "Kullanıcı adı" olan Istemciye Base64 kodlamalı bir istem gönderir. Istemci, istem kodunu çözer ve Base64 kodlamalı bir kullanıcı adıyla yanıtlar. Sunucu Istemci kullanıcı adını kabul ederse, Istemci parolası için Base64 kodlamalı bir istem gönderir. Istemci Base64 kodlamalı bir parolayla yanıt verir. Sunucu Istemci kimlik doğrulamasının başarılı olduğunu belirlerse, 235 başarı koduyla yanıt verir.

### <a name="no-authentication"></a>Kimlik Doğrulaması Yok

Bazı SMTP sunucuları kimlik doğrulaması olmadan yapılandırılır. Bu durumda, Istemci EHLO iletisi için 250 yanıtı herhangi bir kimlik doğrulama türünü listeetmez. Ancak, hiçbir kimlik doğrulama türü, sunucunun kimlik doğrulaması gerektirmediğinden veya desteklemediği anlamına gelmez. Istemci bu durumda düz veya oturum açma kimlik doğrulaması için yapılandırılmışsa, NetX Duo Istemci iş parçacığı görevi varsayılan olarak düz olur. Istemci HIÇBIRI için yapılandırılmışsa, kimlik doğrulama adımı atlanır ve SMTP durumu posta durumuna ilerler.

Istemci kimlik doğrulaması için yapılandırılmışsa ve SMTP sunucusu kimlik doğrulamasını destekliyorsa, Istemci kimlik doğrulama türü düz olarak çağrılır.

## <a name="rfcs-supported-by-netx-duo-smtp-client"></a>NetX Duo SMTP Istemcisi tarafından desteklenen RFC 'Ler

NetX Duo SMTP Istemcisi API 'SI, kimlik doğrulaması için RFC2821 "Basit Posta Aktarım Protokolü" ve RFC 2554 "SMTP hizmeti uzantısı ile uyumludur. “
