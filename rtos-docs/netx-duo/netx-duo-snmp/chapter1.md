---
title: Bölüm 1-Azure RTOS NetX Duo SNMP 'ye giriş
description: NetX Duo SNMP uygulamasının bir SNMP aracısının olması. Bir aracı SNMP yöneticisinin komutlarına yanıt vermemeye ve olay odaklı tuzakları göndermeye sorumludur.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 5760e35fdbe8d7b27e2ccc82abac37b1f6fb5118
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825781"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-snmp"></a>Bölüm 1-Azure RTOS NetX Duo SNMP 'ye giriş

Basit Ağ Yönetim Protokolü (SNMP), internet 'teki cihazları yönetmek için tasarlanmış bir protokoldür. SNMP, yönetim işlevini gerçekleştirmek için bağlantısız Kullanıcı Datagram Protokolü (UDP) hizmetlerinden yararlanan bir protokoldür. Azure RTOS NetX Duo SNMP uygulamasının bir SNMP aracısının olması vardır. Bir aracı SNMP yöneticisinin komutlarına yanıt vermemeye ve olay odaklı tuzakları göndermeye sorumludur. 

NetX Duo SNMP, SNMP yöneticileriyle hem IPv4 hem de IPv6 iletişimini destekler. NetX SNMP uygulamalarının NetX Duo SNMP 'de derlenmesi ve çalıştırması gerekir. Ancak, geliştiricinin eşdeğer "Duo" hizmetlerini kullanarak mevcut SNMP uygulamalarının bağlantı noktası olması önerilir. Örneğin, SNMP tuzak iletileri gönderirken aşağıdaki ' Duo ' hizmetlerinin NetX eşdeğerini yerine girmesi gerekir:

*nxd_snmp_object_trap_send*

*nxd_snmp_object_trapv2_send*

*nxd_snmp_object_trapv3_send*

Daha fazla ayrıntı için bu kullanıcı kılavuzunun başka bir yerinde **SNMP Aracısı hizmetleri açıklamasına** bakın.

## <a name="netx-duo-snmp-agent-requirements"></a>NetX Duo SNMP Aracısı gereksinimleri

NetX Duo SNMP paketi bir IP örneğinin zaten oluşturulmuş olmasını gerektirir. Buna ek olarak, aynı IP örneğinde UDP 'nin etkinleştirilmesi gerekir.

NetX Duo SNMP aracısının birkaç ek gereksinimi vardır. İlk olarak, tüm SNMP Yöneticisi isteklerini işlemek için 161 numaralı bağlantı noktasına erişim gerektirir. Ayrıca, yöneticiye tuzak iletileri göndermek için 162 numaralı bağlantı noktasına erişim gerektirir.

NetX Duo SNMP aracısını IPv6 üzerinden kullanmak ve IPv6 nesnelerini almak için, IPv6 'yı NetX Duo içinde etkinleştirmeniz gerekir. IPv6 Hizmetleri için IP örneğini etkinleştirme hakkında ayrıntılı bilgi için bkz. ***NETX Duo Kullanıcı Kılavuzu*** .

## <a name="netx-duo-snmp-constraints"></a>NetX Duo SNMP kısıtlamaları

NetX Duo SNMP protokolü SNMP sürüm 1, 2 ve 3 ' ü uygular. SNMPv3 uygulama, MD5 ve SHA kimlik doğrulamasını ve DES şifrelemesini destekler. NetX Duo SNMP aracısının bu sürümü aşağıdaki kısıtlamalara sahiptir:

1. NetX IP örneği başına bir SNMP Aracısı
2. RMON desteği yok
3. SNMP v3 bilgilendirme iletileri desteklenmez
4. DONUK ve NSAP veri türleri desteklenmez
5. IPv6 adresleri sekizli dizeler olarak tanımlanır ve Biçim denetimi uygulamaya bırakılır.

## <a name="snmp-object-names"></a>SNMP nesne adları

SNMP protokolü, internet 'teki cihazları yönetmek için tasarlanmıştır. Bu işlemi gerçekleştirmek için, her SNMP yönetilen cihazının, RFC 1155 tarafından tanımlanan yönetim bilgileri (SMı) yapısı tarafından tanımlanan bir nesne kümesi vardır. Yapı, aşağıdaki gibi görünen bir yapı hiyerarşik ağaç türüdür:

![Yönetim bilgileri yapısının diyagramı.](media/image3.png)

Ağaçtaki her düğüm bir nesnedir. Ağaçtaki "DOD" nesnesi, 1.3.6 gösterimi tarafından tanımlanır, ancak ağaçtaki "Internet" nesnesi 1.3.6.1 gösterimi tarafından tanımlanır. Tüm SNMP nesne adları 1.3.6 gösterimi ile başlar.

Bir SNMP Yöneticisi, cihazdaki hangi nesneyi almak veya ayarlamak istediğinizi belirtmek için bu nesne gösterimini kullanır. NetX Duo SNMP Aracısı, bu tür yönetici isteklerini Yorumlar ve uygulamanın istenen işlemi gerçekleştirmesi için mekanizmalar sağlar.

## <a name="snmp-manager-requests"></a>SNMP Yöneticisi Istekleri

SNMP 'nin cihazları yönetmek için basit bir mekanizması vardır. SNMP Yöneticisi tarafından *161 numaralı bağlantı* noktasında SNMP cihazına VERILEN standart SNMP komutları kümesi vardır. Aşağıdakiler, temel SNMP Yöneticisi komutlarının bazılarını göstermektedir:

| SNMP komutu | Anlamı                                                        |
|--------------|----------------------------------------------------------------|
| GET          | *Belirtilen nesneyi al*                                       |
| GETNEXT      | *Belirtilen nesne KIMLIĞINDEN sonraki mantıksal nesneyi al*      |
| GETBULK      | *Belirtilen nesne KIMLIĞINDEN sonra birden çok mantıksal nesne al* |
| SET          | *Belirtilen nesneyi ayarla*                                       |

Bu komutlar, soyut sözdizimi gösterimi bir (ASN. 1) biçiminde kodlanır ve SNMP Yöneticisi tarafından gönderilen UDP paketinin yükünde bulunur. NetX Duo SNMP Aracısı isteği işler ve sonra ***nx_snmp_agent_create*** çağrısında belirtilen karşılık gelen işleme yordamını çağırır.

## <a name="netx-duo-snmp-agent-traps"></a>NetX Duo SNMP aracı tuzakları

NetX Duo SNMP aracısı ayrıca bir olay SNMP yöneticisini zaman uyumsuz olarak uyarma yeteneği sağlar. Bu, bir SNMP tuzağı komutu aracılığıyla yapılır. SNMP Yöneticisi 'ne tuzak göndermek için her SNMP sürümü için benzersiz bir API vardır. Varsayılan olarak, tuzaklar 162 numaralı bağlantı noktasında SNMP Yöneticisi 'ne gönderilir.

NetX Duo SNMP Aracısı, SNMPv3 tuzak iletileri için ayrı güvenlik anahtarları sağlar. Bunu yapmak için SNMP uygulamasının, yönetici isteklerine yapılan yanıtlara uygulananlardan ayrı bir anahtar kümesi oluşturması gerekir. Tuzak güvenliği, SNMP aracısının kimlik doğrulama ve gizlilik için aynı veya farklı parolaları kullanmasına olanak sağlar. Güvenlik anahtarları oluşturma hakkında daha fazla bilgi için, sonraki bölümde **NETX Duo SNMP kimlik doğrulaması ve şifreleme** bölümüne bakın.

Standart SNMP yakalama değişkenlerinin listesi *nxd_snmp. h* 'nin üstünde numaralandırılır:

| Değişkenler                                 | Değer  |
|-------------------------------------------|---|
| #define NX_SNMP_TRAP_COLDSTART            | 0 |
| #define NX_SNMP_TRAP_WARMSTART            | 1 |
| #define NX_SNMP_TRAP_LINKDOWN             | 2 |
| #define NX_SNMP_TRAP_LINKUP               | 3 |
| #define NX_SNMP_TRAP_AUTHENTICATE_FAILURE | 4 |
| #define NX_SNMP_TRAP_EGPNEIGHBORLOSS      | 5 |
| #define NX_SNMP_TRAP_ENTERPRISESPECIFIC   | 6 |

Bu değişkenleri tuzak iletisine eklemek için, *nx_snmp_agent_trapv2_send* (SNMPv2) veya *nx_snmp_agent_trapv3_send* (SNMPv3) içindeki trap_type giriş bağımsız değişkeni bu değişkenlerin numaralandırılmış değerine ayarlanır. Aşağıdaki bir örnek, bir soğuk başlatma olayının SNMP yöneticisini bilgilendirmek için aşağıda gösterilmiştir:

```c
UINT trap_type = NX_SNMP_TRAP_COLDSTART;

status = nx_snmp_agent_trapv2_send(&my_agent, MIB_IP_ADDRESS,
                                  (UCHAR *)"public", trap_type,
                                  tx_time_get(), NX_NULL);

```

Tuzak iletisine özel değişkenler eklemek için trap_type giriş bağımsız değişkeni NX_SNMP_TRAP_CUSTOM olarak ayarlanır ve tuzak listesi giriş bağımsız değişkeni özel verileri içerir. Tuzak iletisinin sistem zamanı (1.3.6.1.6.3.1.1.4.1.0) olarak içereceği unutulmamalıdır. SNMPv2 için aşağıda bir örnek gösterilmektedir:

```c
NX_SNMP_TRAP_OBJECT trap_list[3];
NX_SNMP_OBJECT_DATA trap_data0;

    /* Load the data into the OBJECT. */
    nx_snmp_object_id_get((void*)"1.3.6.1.4.1.7428.1.3.2.0", &trap_data0);

    /* Update the Trap Object with the object and OID. */
    trap_list[0].nx_snmp_object_string_ptr = (UCHAR *)"1.3.6.1.6.3.1.1.4.0";
    trap_list[0].nx_snmp_object_data  = &trap_data0;

    /* Null terminate the trap list. */
    trap_list[1].nx_snmp_object_string_ptr = NX_NULL;

    status = nx_snmp_agent_trapv2_send(&my_agent, MIB_IP_ADDRESS,
                                      (UCHAR *)"trapduo",
                                      NX_SNMP_TRAP_CUSTOM,
                                      tx_time_get(), trap_list);
```

## <a name="netx-duo-snmp-authentication-and-encryption"></a>NetX Duo SNMP kimlik doğrulaması ve şifreleme

*Temel* ve *Özet* gibi iki kimlik doğrulama özelliği vardır. Temel kimlik doğrulaması, birçok protokolde bulunan basit bir düz metin *Kullanıcı adı* kimlik doğrulamasına eşdeğerdir. SNMP temel kimlik doğrulamasında, Kullanıcı yalnızca sağlanan kullanıcı adının SNMP işlemlerini gerçekleştirmek için geçerli olduğunu doğrular. Temel kimlik doğrulaması, 1 ve 2. SNMP sürümleri için tek seçenektir.

Temel kimlik doğrulamasının ana dezavantajı, Kullanıcı adı düz metin olarak iletilir. SNMPv3 Özet kimlik doğrulaması, Kullanıcı adını hiçbir şekilde düz metin halinde ileterek bu sorunu giderir. Bunun yerine, Kullanıcı adı, bağlam altyapısı ve diğer bilgilerden 96 bitlik bir ' Digest ' türetmek için bir algoritma kullanılır. NetX Duo SNMP Aracısı hem MD5 hem de SHA Özet algoritmalarını destekler.

Kimlik doğrulamasını etkinleştirmek için SNMP aracısının, *nx_snmp_agent_context_engine_set* hizmetini kullanarak kendi bağlam motoru kimliğini ayarlaması gerekir. Bağlam altyapısı KIMLIĞI, kimlik doğrulama anahtarı oluşturulurken kullanılır.

SNMPv3 veri şifrelemesi DES algoritması kullanılarak kullanılabilir. Şifreleme, kimlik doğrulamasının etkinleştirilmesini gerektirir (bir tane, kimlik doğrulama parametreleri ayarlamadan verileri şifreleyemez).

Kimlik doğrulaması ve gizlilik anahtarları oluşturmak için aşağıdaki API kullanılır:

```c
UINT  _nx_snmp_agent_md5_key_create(NX_SNMP_AGENT *agent_ptr,
                                    UCHAR *password, NX_SNMP_SECURITY_KEY
                                   *destination_key)

UINT  _nx_snmp_agent_sha_key_create(NX_SNMP_AGENT *agent_ptr,
                                    UCHAR *password, NX_SNMP_SECURITY_KEY
                                   *destination_key)
```

Daha sonra, SNMP aracısının bu anahtarları kullanacak şekilde yapılandırılması gerekir. SNMP aracısıyla bir anahtar kaydetmek için aşağıdaki API kullanılır:

```c
UINT  _nx_snmp_agent_authenticate_key_use(NX_SNMP_AGENT *agent_ptr,
                                          NX_SNMP_SECURITY_KEY *key)

UINT  _nx_snmp_agent_privacy_key_use(NX_SNMP_AGENT *agent_ptr,
                                    NX_SNMP_SECURITY_KEY *key)
```

Tuzak iletileri için ayrı anahtarlar oluşturulabilir. Tuzak iletileri için anahtar uygulamak için aşağıdaki API kullanılabilir:

```c
UINT  _nx_snmp_agent_auth_trap_key_use(NX_SNMP_AGENT *agent_ptr,
                                       NX_SNMP_SECURITY_KEY *key)

UINT  _nx_snmp_agent_priv_trap_key_use(NX_SNMP_AGENT *agent_ptr,
                                       NX_SNMP_SECURITY_KEY *key)
```

Yanıt iletileri ve tuzak göndermek için kimlik doğrulama veya şifrelemeyi devre dışı bırakmak için bu hizmetleri anahtar işaretçisi girişi NULL olarak ayarlanmış şekilde kullanın.

## <a name="netx-duo-snmp-community-strings"></a>NetX Duo SNMP topluluk dizeleri

NetX Duo SNMP Aracısı hem ortak hem de özel topluluk dizelerini destekler. Ortak dize, *nx_snmp_agent _public_string_set* hizmeti ile ayarlanır. NetX Duo SNMP Aracısı özel dizesi *nx_snmp_agent_private_string_set* hizmeti kullanılarak ayarlanır.

## <a name="netx-duo-snmp-username-callback"></a>NetX Duo SNMP Kullanıcı adı geri araması

NetX Duo SNMP aracı paketi, uygulamanın, her SNMP Istemci isteğinin başlangıcında çağrılan bir Kullanıcı adı geri çağırması belirtmesini ( ***nx_snmp_agent_create*** çağrısı aracılığıyla) sağlar.

Geri arama yordamı, NetX Duo SNMP aracısını Kullanıcı adıyla sağlar. Sağlanan Kullanıcı adı geçerliyse veya isteğe yanıt vermek için Kullanıcı adı denetimi gerekli değilse, Kullanıcı adı geri çağırması **NX_SUCCESS** değerini döndürmelidir. Aksi halde, belirtilen kullanıcı adının geçersiz olduğunu göstermek için yordam **NX_SNMP_ERROR** döndürmelidir.

Uygulama Kullanıcı adı geri çağırma yordamının biçimi aşağıda tanımlanmıştır:

```c
UINT nx_snmp_agent_username_process(NX_SNMP_AGENT *agent_ptr,
                                    UCHAR *username);
```

Giriş parametreleri aşağıdaki gibi tanımlanır:

| Parametre | Anlamı                                              |
|-----------|------------------------------------------------------|
| *agent_ptr* | SNMP Aracısı çağırma işaretçisi                        |
| username  | Gerekli Kullanıcı adına işaretçinin hedefi |

SNMPv1 ve SNMPv2/v2C oturumları için, uygulama, SNMP isteğinin geçerli bir topluluk dizesine sahip olup olmadığını anlamak üzere gelen bir SNMP isteğindeki topluluk dizesini incelemek ister. SNMP uygulamasının bunu yapması için çeşitli hizmetler vardır.

SNMP uygulaması, geçerli SNMP Yöneticisi isteğinin bir GET (örn. GET, GETNEXT veya GETBULK) olduğunu veya bu hizmeti kullanarak istek türünü AYARLAMANıZı sağlayabilir:

```c
UINT nx_snmp_agent_request_get_type_test(NX_SNMP_AGENT *agent_ptr,
                                         UINT *is_get_type);
```

İstek bir GET türüdür, uygulama, giriş topluluğu dizesini SNMP aracısının ortak dizesiyle karşılaştırmak ister:

```c
UINT nx_snmp_agent_public_string_test(NX_SNMP_AGENT *agent_ptr,
                                      UCHAR *username,
                                      UINT *is_public);
```

Benzer şekilde, istek bir küme türü ise, uygulama, giriş topluluğu dizesini SNMP aracısının özel dizesiyle karşılaştırmak ister:

```c
UINT nx_snmp_agent_private_string_test(NX_SNMP_AGENT *agent_ptr,
                                       UCHAR *username,
                                       UINT *is_private);
```

İs_public ve is_private dönüş değerleri, giriş topluluk dizesi geçerli bir genel veya özel topluluk dizesi ise sırasıyla gösterir.

Kullanıcı adı geri çağırma yordamının dönüş değeri, Kullanıcı adının geçerli olup olmadığını gösterir. **NX_SUCCESS** değeri, Kullanıcı adı geçerliyse veya Kullanıcı adı geçersiz ise **NX_SNMP_ERROR** döndürülür.

## <a name="netx-duo-snmp-agent-get-callback"></a>NetX Duo SNMP Aracısı geri arama al

Uygulamanın, SNMP yöneticisinden nesne al isteklerini işlemek için bir geri çağırma yordamı ayarlaması gerekir. Geri çağırma istekte belirtilen nesnenin değerini alır.

Uygulama GET isteği geri arama yordamı aşağıda tanımlanmıştır:

```c
UINT nx_snmp_agent_get_process(NX_SNMP_AGENT *agent_ptr,
                               UCHAR *object_requested,
                               NX_SNMP_OBJECT_DATA *object_data);
```

Giriş parametreleri aşağıdaki gibi tanımlanır:

| Parametre        | Anlamı |
|------------------|----------------------------------|
| *agent_ptr*        | SNMP Aracısı çağırma işaretçisi |
| object_requested | GET işleminin için olduğu nesne KIMLIĞINI temsil eden ASCII dizesi. |
| object_data      | Geri çağırma tarafından alınan değeri tutacak veri yapısı. Bu, aşağıda açıklanan bir dizi NetX Duo SNMP API 'SI ile ayarlanabilir. |

> [!NOTE]
> *Sekizli dizeler için, nesnenin uzunluğu atanmalıdır; böylece iç işlev, geri aramanın bir length bağımsız değişkenine sahip olmadığı için uzunluğu ne kadar süreyle olduğunu bilir:*

```c
object_data -> nx_snmp_object_octet_string_size = mib2_mib[i].length;
```

Veri türü GET geri çağırması tarafından bilinmediğinden, veri türünü denetlemeniz gerekmez. Uzunluk, boş ayrılmış sayısal türler veya dizeler üzerinde herhangi bir etkiye sahip olmayacaktır.

Ardından iç işlevi çağırın:

```c
status = mib2_mib[i].object_get_callback)
                   (mib2_mib[i].object_value_ptr, object_data);
```

Geri çağırma işlevi istenen nesneyi bulamazsa, **NX_SNMP_ERROR_NOSUCHNAME** hata kodu döndürülmelidir. Başka bir hata algılanırsa, **NX_SNMP_ERROR** döndürülmelidir.

## <a name="netx-duo-snmp-agent-getnext-callback"></a>NetX Duo SNMP Aracısı GETNEXT geri çağırma

Uygulamanın, SNMP yöneticisinden GETNEXT nesne istekleri için geri çağırma yordamını da ayarlaması gerekir. GETNEXT geri çağırması, istek tarafından belirtilen sonraki nesnenin değerini alır.

Application GETNEXT istek geri çağırma yordamı aşağıda tanımlanmıştır:

```c
UINT nx_snmp_agent_getnext_process(NX_SNMP_AGENT *agent_ptr,
                                   UCHAR *object_requested,
                                   NX_SNMP_OBJECT_DATA *object_data);
```

Giriş parametreleri aşağıdaki gibi tanımlanır:

| Parametre        | Anlamı |
|------------------|-------------------------------------------|
| *agent_ptr*        | SNMP Aracısı çağırma işaretçisi |
| object_requested | GETNEXT işleminin için olduğu nesne KIMLIĞINI temsil eden ASCII dizesi. |
| object_data      | Geri çağırma tarafından alınan değeri tutacak veri yapısı. Bu, aşağıda açıklanan bir dizi NetX Duo SNMP API 'SI ile ayarlanabilir. |

Geri çağırmalar için aynı ile aynı, iç işlevin uzunluğunun length bir bağımsız değişkeni olmadığından, dizenin ne kadar süreyle olduğunu bilmesi için, sekizli dize verilerine sahip nesneler uzunluğa atanmalıdır.

```c
object_data -> nx_snmp_object_octet_string_size = mib2_mib[i].length;
```

Veri türü GET geri çağırması tarafından bilinmediğinden, veri türünü denetlemeniz gerekmez. Uzunluk, boş ayrılmış sayısal türler veya dizeler üzerinde herhangi bir etkiye sahip olmayacaktır.

Ardından iç işlevi çağırın:

```c
status = mib2_mib[i].object_get_callback)
                   (mib2_mib[i].object_value_ptr, object_data);
```

Geri çağırma işlevi istenen nesneyi bulamazsa, **NX_SNMP_ERROR_NOSUCHNAME** hata kodu döndürülmelidir. Başka bir hata algılanırsa, **NX_SNMP_ERROR** döndürülmelidir.

## <a name="netx-duo-snmp-agent-set-callback"></a>NetX Duo SNMP Aracısı KÜMESI geri araması

Uygulama, SNMP yöneticisinden SET nesne isteklerini işlemek için geri çağırma yordamını ayarlanmalıdır. SET callback, istek tarafından belirtilen nesnenin değerini ayarlar.

Uygulama KÜMESI isteği geri arama yordamı aşağıda tanımlanmıştır:

```c
UINT nx_snmp_agent_set_process(NX_SNMP_AGENT *agent_ptr,
                               UCHAR *object_requested,
                               NX_SNMP_OBJECT_DATA *object_data);
```

Giriş parametreleri aşağıdaki gibi tanımlanır:

| Parametre        | Anlamı |
|------------------|-------- |
| *agent_ptr*      | SNMP Aracısı çağırma işaretçisi |
| object_requested | KÜME işleminin için olduğu nesne KIMLIĞINI temsil eden ASCII dizesi. |
| object_data      | Belirtilen nesne için yeni değeri içeren veri yapısı. Gerçek işlem, aşağıda açıklanan NetX Duo SNMP API 'SI kullanılarak yapılabilir. |

Sekizli dizeler için, küme geri çağrısının, SNMP Aracısı verileri ayrıştırdığından ve türü ve uzunluğu öğrendiğinden, MıB tablosunu verilerin uzunluğuyla güncelleştirmesi gerektiğini unutmayın:

```c
if (object_data -> nx_snmp_object_data_type ==
                           NX_SNMP_ANS1_OCTET_STRING)
{
    mib2_mib[i].length =
        object_data -> nx_snmp_object_octet_string_size;
}

object_data -> nx_snmp_object_octet_string_size =
                                 mib2_mib[i].length;
```

Geri çağırma işlevi istenen nesneyi bulamazsa, **NX_SNMP_ERROR_NOSUCHNAME** hata kodu döndürülmelidir.

NetX Duo SNMP ana bilgisayarı özel topluluk dizeleri oluşturup, küme isteğinin SNMP göndericisi eşleşen özel dizeye sahip değilse, bir **NX_SNMP_ERROR_NOACCESS** hatası döndürebilir. Başka bir hata algılanırsa, **NX_SNMP_ERROR** döndürülmelidir.

> [!NOTE]
> *NetX Duo SNMP Aracısı, dağıtıma sahip bir SNMP MıB veritabanı sağlamasına rağmen öncelikli olarak test ve geliştirme amaçlıdır. Geliştirici, büyük olasılıkla profesyonel SNMP uygulaması için özel bir MıB veritabanı gerektirir.*

## <a name="changing-snmp-version-at-run-time"></a>Çalışma zamanında SNMP sürümünü değiştirme

SNMP Aracısı ana makinesi, *nx_snmp_agent_set_version* hizmetini kullanarak, çalışma zamanında üç sürümün her bırı için SNMP sürümünü değiştirebilir. SNMP Aracısı, *NX_SNMP_AGENT_CREATE* SNMP Aracısı oluşturulduğunda varsayılan olarak üç sürüm için etkinleştirilmiştir. Ancak, uygulama bunu tüm sürümlerin bir alt kümesiyle sınırlayabilir.

> [!NOTE]
> *NX_SNMP_DISABLE_V1, NX_SNMP_DISABLE_V2 ve/veya NX_SNMP_DISABLE_V3 yapılandırma seçenekleri tanımlıysa, bu işlevin etkilenen sürümlerin etkinleştirilmesiyle hiçbir etkisi olmayacaktır.*

SNMP Aracısı, *nx_snmp_agent_get_current_version* hizmeti kullanılarak alınan en son SNMP paketinin SNMP sürümünü alabilir.

## <a name="snmpv3-discovery"></a>SNMPv3 bulma

SNMPv3 için etkinleştirildiyse SNMP Aracısı, SNMP yöneticisinden bulma isteklerine yanıt verir. Bu tür bir istek, yetkili altyapı KIMLIĞI, Kullanıcı adı, önyükleme sayısı ve önyükleme süresi için null değerleri olan güvenlik parametresi verileri içerir. Kimlik doğrulama parametreleri bulma iletisine uygulanmaz. İstekteki değişken bağlama listesi boş (sıfır öğe içeriyor). SNMP Aracısı, sıfır önyükleme süresi ve sayısı ile yanıt verir ve bilinmeyen (null) bir altyapı KIMLIĞIYLE alınan isteklerin sayısı olan 1 item, *Usmstatsunknownengineıds*' ı içeren değişken bağlama listesidir. Tarayıcıdan/yöneticisinden sonraki GETNEXT isteğinde, önyükleme verileri ve güvenlik parametreleri yalnızca güvenlik etkinse doldurulur. Bu durumda, PDU 'da NotInTime veri güncelleştirmesi de gönderilir. Güvenlik parametreleri, örneğin, kimlik doğrulama aracının yöneticinin kimliğini yöneticiye kanıtlamasını sağlar.

SNMPv3 kimlik doğrulaması hakkında daha ayrıntılı bilgi için, RFC 3414 "basit ağ yönetim protokolü 'nün (SNMPv3) 3. sürümü için Kullanıcı tabanlı güvenlik modelinde (USD) kullanılabilir.

## <a name="netx-duo-snmp-rfcs"></a>NetX Duo SNMP RFC 'Leri

NetX Duo SNMP, RFC1155, RFC1157, RFC1215, RFC1901, RFC1905, RFC1906, RFC1907, RFC1908, RFC2571, RFC2572, RFC2574, RFC2575, RFC 3414 ve ilgili RFC 'Ler ile uyumludur.
