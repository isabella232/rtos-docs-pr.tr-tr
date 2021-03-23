---
title: Ek A – Azure RTOS NetX Duo DHCPv6 seçenek kodları
description: Bu bölümde tüm NetX Duo DHCPv6 seçenek kodlarının açıklaması yer almaktadır
author: philmea
ms.author: philmea
ms.date: 06/08/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 36d673c34479ec2d476eeaa094c0dc02714ee010
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826063"
---
# <a name="appendix-a--azure-rtos-netx-duo-dhcpv6-option-codes"></a>Ek A – Azure RTOS NetX Duo DHCPv6 seçenek kodları

| Seçenek              | Kod            | Açıklama |
| ------------------- | ------------------- | --------------- |
| İstemci tanımlayıcısı DUıD | 1 | Ağ üzerinde bir Istemci konağını benzersiz olarak tanımlar |
| Sunucu tanımlayıcısı (DUıD) | 2 | DHCPv6Server konağını ağ üzerinde benzersiz şekilde tanımlar |
| Geçici olmayan adresler için kimlik Ilişkilendirmesi (ıANA) | 3 | Geçici olmayan IP adresi ataması için parametreler |
| Geçici adresler için kimlik Ilişkilendirmesi (ıATA) | 4 | Geçici bir IP adresi ataması için parametreler |
| IA adresi | 5 | Istemciye atanacak gerçek IPv6 adresi ve IPv6 adresi yaşam süreleri |
| Seçenek Isteği | 6 | DNS sunucusu ve diğer ağ yapılandırma parametreleri gibi ağ bilgilerini elde etmek için bilgi isteklerinin listesi. |
| Tercih | 7 | Istemcinin sunucu seçimini etkilemek için sunucu tarafından istemciye tanıtım iletisi dahil edilmiştir. Istemci diğer sunucular üzerinde tercih değeri daha yüksek olan bir sunucu seçmelidir. 255 en büyük değerdir, sıfır iken istemcinin kendisine yanıt veren bir sunucuyu seçebileceğini gösterir |
| Geçen süre | 8 | Istemci, sunucuyla DHCPv6 değişim işlemini başlattığında süreyi (0,01 saniye cinsinden) içerir. Birincil sunucunun Istemci isteğine zamanında yanıt verip vermediğini belirlemek için ikincil sunucu (ler) tarafından kullanılır. |
| Geçiş Iletisi | 9 | Geçiş iletisindeki özgün iletiyi içerir | 
| Kimlik Doğrulaması | 11 | DHCPv6 iletilerinin kimliğini ve içeriğini doğrulamak için bilgiler içerir |
| Sunucu tek noktaya | 12 | Sunucu bu seçeneği, Istemcinin çok noktaya yayın yerine tek noktaya yayın iletilerini doğrudan Istemciden kabul edeceğini bilmesini sağlamak için gönderir. |

Bu NetX Duo DHCPv6 sunucusu sürümünde ıATA, geçiş Iletisi, kimlik doğrulama ve sunucu tek noktaya yayın seçenekleri desteklenmez. Geçerli DHCPv6 protokol seçeneği kodu 10, RFC 3315 ' de tanımsız olarak bırakılır.