---
title: Bölüm 5-Azure RTOS ThreadX için cihaz sürücüleri
description: Bu bölümde, Azure RTOS ThreadX için cihaz sürücülerinin bir açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 05/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 2432b291f2b3fa7d6d798b8b4c187dd20b97db6b
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104827358"
---
# <a name="chapter-5---device-drivers-for-azure-rtos-threadx"></a>Bölüm 5-Azure RTOS ThreadX için cihaz sürücüleri

Bu bölümde, Azure RTOS ThreadX için cihaz sürücülerinin bir açıklaması yer almaktadır. Bu bölümde sunulan bilgiler, geliştiricilerin uygulamaya özgü sürücüleri yazmasına yardımcı olmak için tasarlanmıştır.

## <a name="device-driver-introduction"></a>Cihaz sürücüsü giriş

Dış ortamla iletişim, çoğu katıştırılmış uygulamanın önemli bir bileşenidir. Bu iletişim, katıştırılmış uygulama yazılımının erişebileceği donanım cihazları aracılığıyla gerçekleştirilir. Bu cihazları yönetmeden sorumlu yazılım bileşenleri genellikle *cihaz sürücüleri* olarak adlandırılır.

Katıştırılmış ve gerçek zamanlı sistemlerdeki cihaz sürücüleri, doğal olarak uygulamaya bağımlıdır. Bu iki asıl nedenden dolayı geçerlidir: hedef donanımın büyük ölçüde çeşitliliğe ve gerçek zamanlı uygulamalara uygulanan eşit oranda performans gereksinimleridir. Bu nedenle, her uygulamanın gereksinimlerini karşılayacak ortak bir sürücü kümesi sağlanması neredeyse imkansızdır. Bu nedenlerden dolayı, bu bölümdeki bilgiler, kullanıcıların *raf dışı* threadx cihaz sürücülerini özelleştirmesini ve kendi belirli sürücülerini yazmasını sağlayacak şekilde tasarlanmıştır.

## <a name="driver-functions"></a>Sürücü Işlevleri

ThreadX cihaz sürücüleri, aşağıdaki gibi sekiz temel işlevsel alandan oluşur.

- **Sürücü başlatma**
- **Sürücü denetimi**
- **Sürücü erişimi**
- **Sürücü girişi**
- **Sürücü çıkışı**
- **Sürücü kesintileri**
- **Sürücü durumu**
- **Sürücü sonlandırma**

Başlatma dışında, her sürücü işlevsel alanı isteğe bağlıdır. Ayrıca, her bir alandaki tam işleme cihaz sürücüsüne özeldir.

### <a name="driver-initialization"></a>Sürücü başlatma
Bu işlevsel alan, gerçek donanım cihazının ve sürücünün iç veri yapılarının başlatılmasından sorumludur. Başlatma tamamlanana kadar diğer sürücü hizmetlerini çağırmaya izin verilmez.

> [!NOTE]
> * Sürücünün başlatma işlevi bileşeni genellikle ***tx_application_define** _ işlevinden veya bir başlatma işleminden çağrılır Thread._

### <a name="driver-control"></a>Sürücü denetimi

Sürücü başlatıldıktan ve işleme hazırladıktan sonra, bu işlevsel alan çalışma zamanı denetiminden sorumludur. Genellikle, çalışma zamanı denetimi, temel alınan donanım cihazında değişiklik yapmaktan oluşur. Örnek olarak, bir seri cihazın baud hızını değiştirme veya bir diskte yeni bir kesim arama sayılabilir.

### <a name="driver-access"></a>Sürücü erişimi

Bazı cihaz sürücüleri yalnızca tek bir uygulama iş parçacığından çağırılır. Böyle durumlarda, bu işlevsel alan gerekli değildir. Ancak, birden çok iş parçacığının eşzamanlı sürücü erişimine ihtiyacı olan uygulamalarda, cihaz sürücüsüne atama/sürüm tesislerini ekleyerek etkileşiminin denetlenmesi gerekir. Alternatif olarak, uygulama sürücü erişimini denetlemek ve sürücü içinde ek yüke ve karmaşıkmaya engel olmak için bir semafor kullanabilir.

### <a name="driver-input"></a>Sürücü girişi

Bu işlevsel alan tüm cihaz girişinden sorumludur. Sürücü girişiyle ilişkili asıl sorunlar genellikle girişin nasıl arabelleğe alınacağını ve iş parçacıklarının böyle bir girişi nasıl bekleyeceğini kapsar.

### <a name="driver-output"></a>Sürücü çıkışı

Bu işlevsel alan tüm cihaz çıktıından sorumludur. Sürücü çıkışıyla ilişkili asıl sorunlar genellikle çıktının nasıl arabelleğe alınacağını ve iş parçacıklarının çıktıyı gerçekleştirmeyi nasıl bekleyeceğini kapsar.

### <a name="driver-interrupts"></a>Sürücü kesintileri

Birçok gerçek zamanlı sistem, cihaz girişi, çıkış, denetim ve hata olaylarının sürücüsünü bilgilendirmek için donanım kesmelerini kullanır. Kesmeler, bu tür dış olaylara garantili bir yanıt süresi sağlar. Kesmeler yerine, sürücü yazılımı bu tür olaylar için düzenli olarak dış donanımı denetleyebilir. Bu teknik *yoklama* olarak adlandırılır. Kesmelerden daha az gerçek zamanlı, ancak yoklama bazı daha az gerçek zamanlı uygulamalar açısından anlamlı olabilir.

### <a name="driver-status"></a>Sürücü durumu

Bu işlev alanı, sürücü işlemiyle ilişkili çalışma zamanı durumu ve istatistiklerini sağlamaktan sorumludur. Bu işlev alanı tarafından yönetilen bilgiler genellikle aşağıdakileri içerir.

- Geçerli cihaz durumu
- Giriş baytları
- Çıkış baytları
- Cihaz hata sayıları

### <a name="driver-termination"></a>Sürücü sonlandırma

Bu işlevsel alan isteğe bağlıdır. Yalnızca sürücü ve/veya fiziksel donanım cihazının kapatılması gerekiyorsa gereklidir. Sonlandırıldıktan sonra, sürücünün yeniden başlatılana kadar tekrar çağrılmaması gerekir.

## <a name="simple-driver-example"></a>Basit sürücü örneği

Bir aygıt sürücüsünü tanımlamanın en iyi yolu bir örnektir. Bu örnekte, sürücü bir yapılandırma kaydı, bir giriş kaydı ve bir çıkış kaydı ile basit bir seri donanım cihazı olduğunu varsayar. Bu basit sürücü örneği, başlatma, giriş, çıkış ve kesme işlevsel bölgelerini gösterir.

### <a name="simple-driver-initialization"></a>Basit sürücü başlatma

Basit sürücünün ***tx_sdriver_initialize*** işlevi, sürücünün giriş ve çıkış işlemini yönetmek için kullanılan iki sayım semaforu oluşturur. Giriş semaforu, seri donanım aygıtı tarafından bir karakter alındığında giriş ıSR tarafından ayarlanır. Bu nedenle, giriş semaforu ilk sıfır sayısı ile oluşturulur.

Buna karşılık, çıkış semaforu seri donanım iletme kaydının kullanılabilirliğini gösterir. İlk olarak, iletme kaydının kullanılabilir olduğunu göstermek için bir değeriyle oluşturulur.

Başlatma işlevi, giriş ve çıkış bildirimleri için düşük düzeyli kesme vektör işleyicilerini yüklemeden de sorumludur. Diğer ThreadX kesme hizmeti yordamları gibi, düşük düzey işleyicinin basit sürücü ıSR 'yi çağırmadan önce ***_tx_thread_context_save** _ ' i çağırması gerekir. Sürücü ıSR çağrıldıktan sonra, alt düzey işleyicinin _ * _ _tx_thread_context_restore_* * çağrısı gerekir.

> [!IMPORTANT]
> * Başlatma işlemi, diğer sürücü işlevlerinden herhangi biri çalıştırılmadan önce çağırılır. Genellikle, ***tx_application_define***'tan sürücü başlatma çağrılır.

```c
VOID tx_sdriver_initialize(VOID)
{
    /* Initialize the two counting semaphores used to control
    the simple driver I/O. */
    tx_semaphore_create(&tx_sdriver_input_semaphore,
                        "simple driver input semaphore", 0);
    tx_semaphore_create(&tx_sdriver_output_semaphore,
                        "simple driver output semaphore", 1);

    /* Setup interrupt vectors for input and output ISRs.
    The initial vector handling should call the ISRs
    defined in this file. */

    /* Configure serial device hardware for RX/TX interrupt
    generation, baud rate, stop bits, etc. */
}
```
**ŞEKIL 9. Basit sürücü başlatma**

### <a name="simple-driver-input"></a>Basit sürücü girişi

Giriş semaforu etrafında basit sürücü merkezlerinin girişi. Bir seri cihaz giriş kesmesi alındığında, giriş semaforu ayarlanır. Bir veya daha fazla iş parçacığı sürücüden bir karakter bekliyorsa, en uzun bekleme olan iş parçacığı sürdürülür. Bekleyen bir iş parçacığı yoksa semafor, bir iş parçacığı sürücü giriş işlevini çağırana kadar ayarlanmış olarak kalır.

Basit sürücü girişi işleme için çeşitli sınırlamalar vardır. Giriş karakterlerinin düşürülme olasılığı en önemlidir. Bu, önceki karakter işlenmeden önce gelen giriş karakterlerini arabelleğe alma özelliği olmadığı için mümkündür. Bu, giriş karakter arabelleği eklenerek kolayca işlenir.

> [!NOTE]
> *Yalnızca iş parçacıklarının*  * **tx_sdriver_input** _ _function. *

Şekil 10 ' da basit sürücü girişiyle ilişkili kaynak kodu gösterilmektedir.

```c
UCHAR tx_sdriver_input(VOID)
{
  /* Determine if there is a character waiting. If not,
  suspend. */
  tx_semaphore_get(&tx_sdriver_input_semaphore,
  TX_WAIT_FOREVER;

  /* Return character from serial RX hardware register. */
  return(*serial_hardware_input_ptr);
}
  VOID tx_sdriver_input_ISR(VOID)
{
  /* See if an input character notification is pending. */
  if (!tx_sdriver_input_semaphore.tx_semaphore_count)
  {
    /* If not, notify thread of an input character. */
    tx_semaphore_put(&tx_sdriver_input_semaphore);
  }
}
```
**ŞEKIL 10. Basit sürücü girişi**

### <a name="simple-driver-output"></a>Basit sürücü çıktısı

Çıktı işleme, seri cihazın aktarım kaydı ücretsizdir sinyali almak için çıkış semaforu kullanır. Çıkış karakteri cihaza gerçekten yazılmadan önce, çıkış semaforu alınır. Mevcut değilse, önceki iletim henüz tamamlanmaz.

Çıkış ıSR, iletim tamamlanma kesmesini işlemekten sorumludur. Çıkış semaforu ayarlamak için çıkış ıSR miktarları işleme, böylece başka bir karakterin çıkışına izin veriliyor.

> [!NOTE]
> *Yalnızca iş parçacıklarının*  * **tx_sdriver_output** _ _function. *

Şekil 11 ' de, basit sürücü çıkışıyla ilişkili kaynak kodu gösterilmektedir.

```c
VOID tx_sdriver_output(UCHAR alpha)
{
  /* Determine if the hardware is ready to transmit a
  character. If not, suspend until the previous output
  completes. */
  tx_semaphore_get(&tx_sdriver_output_semaphore,
                                          TX_WAIT_FOREVER);

  /* Send the character through the hardware. */
  *serial_hardware_output_ptr = alpha;
}
  
VOID tx_sdriver_output_ISR(VOID)
{
  /* Notify thread last character transmit is
  complete. */
  tx_semaphore_put(&tx_sdriver_output_semaphore);
}
```
**ŞEKIL 11. Basit sürücü çıktısı**

### <a name="simple-driver-shortcomings"></a>Basit sürücü eksikler

Bu basit cihaz sürücüsü örneği, bir ThreadX cihaz sürücüsünün temel fikrini gösterir. Ancak, basit cihaz sürücüsü veri arabelleğe alma veya herhangi bir ek yük sorununu gidermez, ancak gerçek dünyada ThreadX sürücülerini tam olarak temsil etmez. Aşağıdaki bölümde, cihaz sürücüleriyle ilişkili daha gelişmiş sorunlardan bazıları açıklanmaktadır.

## <a name="advanced-driver-issues"></a>Gelişmiş sürücü sorunları

Daha önce belirtildiği gibi, cihaz sürücüleri, uygulamaları için benzersiz olan gereksinimlere sahiptir. Bazı uygulamalar, yüksek frekanslı cihaz kesintileri nedeniyle, başka bir uygulama en iyi duruma getirilmiş sürücü ISRs gerektirirken, çok büyük miktarda veri arabelleğe alma gerektirebilir.

### <a name="io-buffering"></a>G/ç arabelleğe alma

Gerçek zamanlı gömülü uygulamalarda veri arabelleğe alma, önemli bir planlama gerektirir. Tasarımın bazıları temel alınan donanım aygıtı tarafından dikte edilir. Cihaz temel bayt g/ç sağlıyorsa, büyük olasılıkla basit bir dairesel arabellek olabilir. Ancak, cihaz blok, DMA veya paket g/ç sağlıyorsa, büyük olasılıkla bir arabellek yönetimi düzeni garanti edilir.

### <a name="circular-byte-buffers"></a>Dairesel bayt arabellekleri

Döngüsel bayt arabellekleri genellikle UART gibi basit bir seri donanım cihazını yöneten sürücülerde kullanılır. Genellikle giriş ve çıkış için bir tane olmak üzere iki dairesel arabellek çoğu zaman bu durumlarda kullanılır.

Her döngüsel bayt arabelleği, bir bayt bellek alanından (genellikle bir **dizi yer)**, bir okuma işaretçisine ve bir yazma işaretçisine oluşur. Okuma işaretçisi ve yazma işaretçileri arabellekteki aynı bellek konumuna başvuru yaparken bir arabellek boş kabul edilir. Sürücü başlatma, hem okuma hem de yazma arabelleği işaretçilerini arabelleğin başlangıç adresine ayarlar.

### <a name="circular-buffer-input"></a>Döngüsel arabellek girişi

Giriş arabelleği, uygulamanın kendisine hazırlanmadan önce gelen karakterleri tutmak için kullanılır. Bir giriş karakteri alındığında (genellikle bir kesme hizmeti yordamında), yeni karakter donanım aygıtından alınır ve yazma işaretçisi tarafından işaret edilen konumdaki giriş arabelleğine konur. Yazma işaretçisi daha sonra arabellekte bir sonraki konuma ilerlemiş olur. Sonraki konum arabelleğin sonunu aşıyorsa, yazma işaretçisi arabelleğin başlangıcına ayarlanır. Yeni yazma işaretçisi okuma işaretçiyle aynıysa yazma işaretçisinin ilerleme durumu iptal edildiğinde sıranın tam koşulu işlenir.

Sürücüye yönelik uygulama giriş bayt istekleri, giriş arabelleğinin okuma ve yazma işaretçilerini ilk olarak inceler. Okuma ve yazma işaretçileri aynıysa, arabellek boştur. Aksi takdirde, okuma işaretçisi aynı değilse, okuma işaretçisi tarafından işaret edilen bayt giriş arabelleğinden kopyalanır ve okuma işaretçisi bir sonraki arabellek konumuna göre ilerlemiş olur. Yeni okuma işaretçisi arabelleğin sonunu aşıyorsa, başlangıca sıfırlanır. Şekil 12 ' de dairesel giriş arabelleğinin mantığı gösterilmektedir.

```c
UCHAR   tx_input_buffer[MAX_SIZE];
UCHAR   tx_input_write_ptr;
UCHAR   tx_input_read_ptr;

/* Initialization. */
tx_input_write_ptr =    &tx_input_buffer[0];
tx_input_read_ptr =     &tx_input_buffer[0];

/* Input byte ISR... UCHAR alpha has character from device. */
save_ptr = tx_input_write_ptr;
*tx_input_write_ptr++ = alpha;
if (tx_input_write_ptr > &tx_input_buffer[MAX_SIZE-1])
    tx_input_write_ptr = &tx_input_buffer[0]; /* Wrap */
if (tx_input_write_ptr == tx_input_read_ptr)
    tx_input_write_ptr = save_ptr; /* Buffer full */

/* Retrieve input byte from buffer... */
if (tx_input_read_ptr != tx_input_write_ptr)
{
  alpha = *tx_input_read_ptr++;
  if (tx_input_read_ptr > &tx_input_buffer[MAX_SIZE-1])
      tx_input_read_ptr = &tx_input_buffer[0];
}
```
**ŞEKIL 12. Döngüsel giriş arabelleği mantığı**

> [!NOTE]
> * Güvenilir bir işlem için hem giriş hem de çıkış dairesel arabelleklerinin okuma ve yazma işaretçilerini işleyerek kesintileri kilitlemesini gerektirebilir. *

### <a name="circular-output-buffer"></a>Döngüsel çıkış arabelleği

Çıktı arabelleği, donanım aygıtı önceki baytı göndermeden önce çıkış için ulaşan karakterleri tutmak için kullanılır. Çıkış arabelleği işleme, giriş arabelleği işlemeye benzerdir, ancak iletim çıkış isteği çıkış okuma işaretçisini, uygulama çıktı isteği çıkış yazma işaretçisinden yararlanır.
Aksi takdirde, çıkış arabelleği işleme aynıdır. Şekil 13, döngüsel çıkış arabelleğinin mantığını gösterir.

```c
UCHAR   tx_output_buffer[MAX_SIZE];
UCHAR   tx_output_write_ptr;
UCHAR   tx_output_read_ptr;

/* Initialization. */
tx_output_write_ptr = &tx_output_buffer[0];
tx_output_read_ptr = &tx_output_buffer[0];

/* Transmit complete ISR... Device ready to send. */
if (tx_output_read_ptr != tx_output_write_ptr)
{
  *device_reg = *tx_output_read_ptr++;
  if (tx_output_read_reg > &tx_output_buffer[MAX_SIZE-1])
      tx_output_read_ptr = &tx_output_buffer[0];
}

/* Output byte driver service. If device busy, buffer! */
save_ptr = tx_output_write_ptr;
*tx_output_write_ptr++ = alpha;
if (tx_output_write_ptr > &tx_output_buffer[MAX_SIZE-1])
    tx_output_write_ptr = &tx_output_buffer[0]; /* Wrap */
if (tx_output_write_ptr == tx_output_read_ptr)
    tx_output_write_ptr = save_ptr; /* Buffer full! */
```
**ŞEKIL 13. Döngüsel çıkış arabelleği mantığı**

### <a name="buffer-io-management"></a>Arabellek g/ç yönetimi

Gömülü mikro işlemcilerin performansını artırmak için, birçok çevresel cihaz cihazı yazılım tarafından sağlanan arabelleklerle veri iletir ve alır. Bazı uygulamalarda, tek tek veri paketlerini iletmek veya almak için birden çok arabellek kullanılabilir.

G/ç arabelleklerinin boyutu ve konumu, uygulama ve/veya sürücü yazılımı tarafından belirlenir. Genellikle, arabellekler boyut olarak sabitlenir ve bir ThreadX blok bellek havuzu içinde yönetilir. Şekil 14, tipik bir g/ç arabelleğini ve bunların ayırmasını yöneten bir ThreadX blok bellek havuzunu açıklar.

```c
typedef struct TX_IO_BUFFER_STRUCT
{
      struct TX_IO_BUFFER_STRUCT *tx_next_packet;
      struct TX_IO_BUFFER_STRUCT *tx_next_buffer;
      UCHAR tx_buffer_area[TX_MAX_BUFFER_SIZE];
} TX_IO_BUFFER;

TX_BLOCK_POOL tx_io_block_pool;

/* Create a pool of I/O buffers. Assume that the pointer
"free_memory_ptr"points to an available memory area that
is 64 KBytes in size. */
tx_block_pool_create(&tx_io_block_pool,
                  "Sample IO Driver Buffer Pool",
                  free_memory_ptr, 0x10000,
                  sizeof(TX_IO_BUFFER));
```

**ŞEKIL 14. G/ç arabelleği**

### <a name="tx_io_buffer"></a>TX_IO_BUFFER

TypeDef TX_IO_BUFFER iki işaretçisinden oluşur. **Tx_next_packet** işaretçisi, giriş veya çıkış listesinde birden çok paketi bağlamak için kullanılır. **Tx_next_buffer** işaretçisi, cihazdan tek bir veri paketini oluşturan arabellekleri birbirine bağlamak için kullanılır. Arabellek havuzdan ayrıldığında, bu işaretçilerin her ikisi de NULL olarak ayarlanır. Ayrıca, bazı cihazlar arabellek alanının ne kadarının veri içerdiğini göstermek için başka bir alan gerektirebilir.

### <a name="buffered-io-advantage"></a>Arabelleğe alınan g/ç avantajı

Arabellek g/ç düzeninin avantajları nelerdir? En büyük avantaj, verilerin cihaz kayıtları ve uygulamanın belleği arasında kopyalanamaması. Bunun yerine, sürücü cihaza bir dizi arabellek işaretçisi sağlar. Fiziksel aygıt g/ç, sağlanan arabellek belleğini doğrudan kullanır.

Bilgilerin giriş veya çıkış paketlerini kopyalamak için işlemcinin kullanılması son derece maliyetlidir ve yüksek performanslı iş g/ç durumunda kaçınılmalıdır.

Ara belleğe alınan g/ç yaklaşımının bir diğer avantajı da giriş ve çıkış listelerinin tam koşulları olmaması olabilir. Tüm kullanılabilir arabellekler her iki listede de herhangi bir anda olabilir. Bu, daha önce bölümün başında sunulan basit bayt dairesel arabelleklerle karşıttır. Her birinin derlemede belirlenen sabit bir boyutu vardır.

### <a name="buffered-driver-responsibilities"></a>Arabellekli sürücü sorumlulukları

Arabelleğe alınmış cihaz sürücüleri yalnızca, g/ç arabelleklerinin bağlı listelerini yönetme ile ilgilidir. Uygulama yazılımı hazırlanmadan önce alınan paketlere yönelik bir giriş arabelleği listesi tutulur. Buna karşılık, bir çıkış arabelleği listesi, donanım cihazından daha hızlı gönderilmekte olan paketlerin bakımını sağlar. Şekil 15 ' te, veri paketlerinin basit giriş ve çıkış bağlantılı listeleri ve her bir paketi oluşturan arabellekler gösterilmektedir.

**Giriş listesi**

![Giriş listesi](./media/user-guide/input-list.png)

**Çıkış listesi**

![Çıkış listesi](./media/user-guide/output-list.png)

**ŞEKIL 15. Input-Output listeleri**

Aynı g/ç arabelleklerine sahip arabellekli sürücülerle uygulamalar arabirimi. İletim sırasında, uygulama yazılımı, iletmek için bir veya daha fazla arabelleme sahip olan sürücüyü sağlar. Uygulama yazılımı giriş istediğinde, sürücü g/ç arabelleklerinde giriş verilerini döndürür.

> [!NOTE]
> *Bazı uygulamalarda, uygulamanın sürücüden gelen bir giriş arabelleği için boş bir arabellek alışverişi gerektirdiğini gerektiren bir sürücü giriş arabirimi oluşturmak yararlı olabilir. Bu, sürücünün içindeki bazı arabellek ayırma işlemlerini giderebilirler.*

### <a name="interrupt-management"></a>Kesme yönetimi

Bazı uygulamalarda, cihaz kesme sıklığı C 'de ıSR yazmayı veya her kesintiye karşı ThreadX ile etkileşime geçmesini engelleyebilir. Örneğin, kesintiye uğramayan bağlamı kaydetmek ve geri yüklemek için 25 ABD sürüyorsa, kesme sıklığının 50 ABD olduğu durumlarda tam bağlam kaydetme işlemini gerçekleştirmek önerilmez. Bu gibi durumlarda, birçok cihaz kesmesi işlemek için küçük bir derleme dili ıSR kullanılır. Bu düşük yüktür ıSR yalnızca gerektiğinde ThreadX ile etkileşime geçebilir.

Bölüm 3 ' ün sonundaki kesme yönetimi tartışmasında benzer bir tartışma bulunabilir.

### <a name="thread-suspension"></a>İş parçacığı askıya alma

Bu bölümde daha önce sunulan basit sürücü örneğinde, bir karakter kullanılamıyorsa giriş hizmeti 'nin çağıranı askıya alınır. Bazı uygulamalarda bu, kabul edilebilir olmayabilir.

Örneğin, bir sürücüden gelen girişin işlenmesinden sorumlu iş parçacığının başka bir işi de varsa, yalnızca sürücü girişinin askıya alınması büyük olasılıkla işe gitmemelidir. Bunun yerine, sürücünün iş parçacığına diğer işleme isteklerinin yapılma biçimine benzer şekilde istek işleme için özelleştirilmelidir.

Çoğu durumda, giriş arabelleği bağlı bir listeye yerleştirilir ve iş parçacığının giriş kuyruğuna bir giriş olayı iletisi gönderilir.
