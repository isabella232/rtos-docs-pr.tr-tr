---
title: Bölüm 5-Azure RTOS ThreadX için cihaz sürücüleri
description: Bu bölümde, Azure RTOS ThreadX için cihaz sürücülerinin bir açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 05/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: fd31c586a8b582215d2f0e54e3e543cd1127594599162ca93bbba69b07565f12
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116791268"
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

Bu basit cihaz sürücüsü örneği, bir ThreadX cihaz sürücüsünün temel fikrini gösterir. Ancak, basit cihaz sürücüsü veri arabelleğe alma veya ek yük sorunlarını ele almayacağı için gerçek dünya ThreadX sürücülerini tam olarak temsil etmez. Aşağıdaki bölümde, cihaz sürücüleriyle ilişkili daha gelişmiş sorunlardan bazıları açık almaktadır.

## <a name="advanced-driver-issues"></a>Gelişmiş Sürücü Sorunları

Daha önce belirtildiği gibi, cihaz sürücülerinin uygulamaları kadar benzersiz gereksinimleri vardır. Bazı uygulamalar çok büyük miktarda veri arabelleğe alma gerektirirken, başka bir uygulama yüksek sıklıkta cihaz kesintileri nedeniyle iyileştirilmiş sürücü ISR'leri gerektirebilir.

### <a name="io-buffering"></a>I/O Arabelleğe Alma

Gerçek zamanlı ekli uygulamalarda veri arabelleğe alma için önemli planlamalar gerekir. Tasarımın bazıları, temel alınan donanım cihazı tarafından dikte edilen bir tasarımdır. Cihaz temel bir bayt I/O sağlarsa, büyük olasılıkla basit bir döngüsel arabellek sırasına göredir. Ancak, cihaz blok, DMA veya paket I/O sağlarsa, büyük olasılıkla bir arabellek yönetim şeması gerekir.

### <a name="circular-byte-buffers"></a>Döngüsel Byte Arabellekleri

Döngüsel bayt arabellekleri genellikle UART gibi basit bir seri donanım cihazı yöneten sürücülerde kullanılır. İki döngüsel arabellek en çok bu tür durumlarda kullanılır: biri giriş, biri çıkış için.

Her döngüsel bayt arabelleği bir bayt bellek alanı (genellikle **bir UCHAR** dizisi), okuma işaretçisi ve yazma işaretçisi içerir. Okuma işaretçisi ve yazma işaretçileri arabellekte aynı bellek konumuyla ilgili olduğunda arabellek boş olarak kabul edilir. Sürücü başlatma, hem okuma hem de yazma arabellek işaretçilerini arabelleğin başlangıç adresine ayarlar.

### <a name="circular-buffer-input"></a>Döngüsel Arabellek Girişi

Giriş arabelleği, uygulama hazır olmadan önce gelen karakterleri tutmak için kullanılır. Bir giriş karakteri (genellikle bir kesme hizmeti yordamında) alınca, yeni karakter donanım cihazından alınır ve yazma işaretçisi tarafından işaret ettiği konumda giriş arabelleğine yerleştirilir. Yazma işaretçisi daha sonra arabellekte bir sonraki konuma ileri doğru ilerler. Sonraki konum, arabelleğin sonunu geçmişse, yazma işaretçisi arabelleğin başına ayarlanır. Yeni yazma işaretçisi okuma işaretçisi ile aynı ise, kuyruk tam koşulu yazma işaretçisi ilerlemesi iptal edilir.

Sürücüye yapılan uygulama giriş bayt istekleri önce giriş arabelleğinin okuma ve yazma işaretçilerini inceler. Okuma ve yazma işaretçileri aynı ise arabellek boştur. Aksi takdirde, okuma işaretçisi aynı değilse, okuma işaretçisi tarafından işaret eden bayt giriş arabelleğinden kopyalanır ve okuma işaretçisi sonraki arabellek konumu için gelişmiştir. Yeni okuma işaretçisi arabelleğin sonunu geçmişse en baştan sıfırlanır. Şekil 12'de döngüsel giriş arabelleğinin mantığı yer almaktadır.

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
**ŞEKIL 12. Döngüsel Giriş Arabelleği mantığı**

> [!NOTE]
> *Güvenilir işlem için hem giriş hem de çıkış döngüsel arabelleklerinin okuma ve yazma işaretçileri işlenebilirken kesmeleri kilitlemek gerekebilir. *

### <a name="circular-output-buffer"></a>Döngüsel Çıkış Arabelleği

Çıkış arabelleği, donanım cihazı önceki baytı göndermeden önce çıkışa gelen karakterleri tutmak için kullanılır. Çıkış arabelleği işlemesi giriş arabelleği işlemeye benzer, ancak aktarım tam kesme işlemesi çıkış okuma işaretçisini, uygulama çıkış isteği ise çıkış yazma işaretçisini kullanır.
Aksi takdirde, çıkış arabelleği işlemesi aynıdır. Şekil 13'te döngüsel çıkış arabelleğinin mantığı gösterir.

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
**ŞEKIL 13. Döngüsel Çıkış Arabelleği mantığı**

### <a name="buffer-io-management"></a>Arabellek I/O Yönetimi

Ekli mikro işlemcilerin performansını geliştirmek için birçok çevresel cihaz, yazılım tarafından sağlanan arabelleklerle veri iletir ve alır. Bazı uygulamalar, tek tek veri paketlerini iletmek veya almak için birden çok arabellek kullanılabilir.

I/O arabelleklerinin boyutu ve konumu, uygulama ve/veya sürücü yazılımı tarafından belirlenir. Arabellekler genellikle boyut olarak sabittir ve bir ThreadX blok bellek havuzu içinde yönetilir. Şekil 14'te, ayırmalarını yöneten tipik bir I/O arabelleği ve ThreadX blok bellek havuzu açık bulunmaktadır.

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

**ŞEKIL 14. I/O Arabelleği**

### <a name="tx_io_buffer"></a>TX_IO_BUFFER

Typedef TX_IO_BUFFER iki işaretçiden oluşur. Tx_next_packet  işaretçisi, giriş veya çıkış listesinde birden çok paketin bağlantısını yapmak için kullanılır. Tx_next_buffer  işaretçisi, cihazdan tek bir veri paketinin bir araya gelen arabelleklerini bir araya etmek için kullanılır. Arabellek havuzdan ayrılırken bu işaretçilerin her ikisi de NULL olarak ayarlanır. Buna ek olarak, bazı cihazlar arabellek alanın gerçekte ne kadar veri içerdiğini belirtmek için başka bir alan gerektirmektedir.

### <a name="buffered-io-advantage"></a>Arabelleğe Alındı I/O Avantajı

Arabellek I/O şemasının avantajları nelerdir? En büyük avantajı, verilerin cihaz kayıtları ile uygulamanın belleği arasında kopyalanmamalarındandır. Bunun yerine sürücü, cihaza bir dizi arabellek işaretçisi sağlar. Fiziksel cihaz I/O, sağlanan arabellek belleğini doğrudan kullanır.

bilgi giriş veya çıkış paketlerini kopyalamak için işlemcinin kullanımı son derece maliyetlidir ve yüksek aktarım hızı G/Ç durumlarında kaçınılmalıdır.

Arabelleğe alan G/Ç yaklaşımının bir diğer avantajı, giriş ve çıkış listelerinin tam koşulların yer almamış olduğudır. Kullanılabilir tüm arabellekler herhangi bir anda her iki listede de olabilir. Bu, bölümün önceki kısımlarında sunulan basit bayt döngüsel arabellekleriyle karşıttır. Her biri derlemede belirlenen sabit bir boyuta sahipti.

### <a name="buffered-driver-responsibilities"></a>Arabelleğe Alındı Sürücü Sorumlulukları

Arabelleğe alan cihaz sürücüleri yalnızca bağlantılı I/O arabellek listelerini yönetmekle ilgilidir. Uygulama yazılımı hazır olmadan önce alınan paketler için bir giriş arabelleği listesi korunur. Buna karşılık, donanım aygıtının bunları işleyene kadar daha hızlı gönderilen paketler için bir çıkış arabellek listesi korunur. Şekil 15'te veri paketlerinin basit giriş ve çıkış bağlantılı listeleri ve her paketin yer alan arabellekleri yer almaktadır.

**Giriş Listesi**

![Giriş Listesi](./media/user-guide/input-list.png)

**Çıkış Listesi**

![Çıkış Listesi](./media/user-guide/output-list.png)

**ŞEKIL 15. Input-Output Listeleri**

Aynı I/O arabellekleri ile arabelleğe alan sürücülere sahip uygulamalar arabirimi. Aktarımda, uygulama yazılımı sürücüye iletilen bir veya daha fazla arabellek sağlar. Uygulama yazılımı giriş isteğinde olduğunda sürücü G/Ç arabellekleri içinde giriş verilerini döndürür.

> [!NOTE]
> *Bazı uygulamalarda, uygulamanın sürücüden bir giriş arabelleği için boş arabellek değiştirmesini gerektiren bir sürücü giriş arabirimi oluşturmak yararlı olabilir. Bu, sürücünün içindeki bazı arabellek ayırma işlemlerini hafifletmeye neden olabilir.*

### <a name="interrupt-management"></a>Kesinti Yönetimi

Bazı uygulamalarda cihaz kesme sıklığı, ISR'nin C'de yazarak veya her kesmede ThreadX ile etkileşim kurmasını yasaklar. Örneğin, kesintiye neden olan bağlamı kaydetmek ve geri yüklemek 25us sürerse, kesme sıklığı 50us ise tam bağlam kaydetmesi tavsiye edilemez. Bu gibi durumlarda, cihaz kesintilerinin çoğunu işlemek için küçük bir derleme dili ISR kullanılır. Bu düşük ek yüke sahip ISR yalnızca gerektiğinde ThreadX ile etkileşime geçmenizi sağlar.

Benzer bir tartışma, Bölüm 3'in sonundaki kesme yönetimi tartışmalarında bulunabilir.

### <a name="thread-suspension"></a>İş ParçacığıNı Askıya Alma

Bu bölümün başlarında sunulan basit sürücü örneğinde, bir karakter yoksa giriş hizmetini çağıran askıya alır. Bazı uygulamalarda bu kabul edilebilir bir durum değildir.

Örneğin, bir sürücüden gelen girişi işlemeden sorumlu iş parçacığının başka görevleri de varsa, yalnızca sürücü girişinin askıya alınması büyük olasılıkla işe yaramayacaktır. Bunun yerine, diğer işleme isteklerinin iş parçacığına yapılmasına benzer şekilde, sürücünün istek işleme için özelleştirilebilir olması gerekir.

Çoğu durumda, giriş arabelleği bağlantılı bir listeye yerleştirilir ve iş parçacığının giriş kuyruğuna bir giriş olayı iletisi gönderilir.
