---
title: Bölüm 5 - ThreadX SMP Azure RTOS Cihaz Sürücüleri
description: Bu bölümde, ThreadX SMP için cihaz Azure RTOS açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 706ad47b2c3e7b2979da7262a4de8d681f4fbc53cb1af59a798b34094734060b
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116792352"
---
# <a name="chapter-5---device-drivers-for-azure-rtos-threadx-smp"></a>Bölüm 5 - ThreadX SMP Azure RTOS Cihaz Sürücüleri

Bu bölümde, ThreadX SMP için cihaz Azure RTOS açıklaması yer almaktadır. Bu bölümde sunulan bilgiler, geliştiricilerin uygulamaya özgü sürücüler yazmanıza yardımcı olmak için tasarlanmıştır. 

## <a name="device-driver-introduction"></a>Cihaz Sürücüsüne Giriş

Dış ortamla iletişim, çoğu ekli uygulamanın önemli bir bileşenidir. Bu iletişim, katıştırılmış uygulama yazılımı tarafından erişilebilen donanım cihazları aracılığıyla başarılı olur. Bu tür cihazları yönetmekle sorumlu yazılım bileşenleri yaygın olarak Cihaz Sürücüleri *olarak da adlandırılan yazılım bileşenleridir.*

Katıştırılmış, gerçek zamanlı sistemlerde cihaz sürücüleri doğal olarak uygulamaya bağımlıdır. Bu durum iki temel nedenden dolayı doğrudur: çok çeşitli hedef donanımlar ve gerçek zamanlı uygulamalara yönelik eşit derecede büyük performans gereksinimleri. Bu nedenle, her uygulamanın gereksinimlerini karşılayacak ortak bir sürücü kümesi sağlamak neredeyse imkansızdır. Bu nedenle, bu bölümdeki bilgiler kullanıcıların hazır *olmayan* ThreadX SMP cihaz sürücülerini özelleştirmelerine ve kendi özel sürücülerini yazmalarına yardımcı olmak için tasarlanmıştır.

## <a name="driver-functions"></a>Sürücü İşlevleri

ThreadX SMP cihaz sürücüleri aşağıdaki gibi sekiz temel işlevsel alandan oluşur:

- **Sürücü Başlatma**
- **Sürücü Denetimi**
- **Sürücü Erişimi**
- **Sürücü Girişi**
- **Sürücü Çıkışı**
- **Sürücü Kesintileri**
- **Sürücü Durumu**
- **Sürücü Sonlandırma**

Başlatma dışında her sürücü işlev alanı isteğe bağlıdır. Ayrıca, her alanda tam işlem cihaz sürücüsüne özeldir.

### <a name="driver-initialization"></a>Sürücü Başlatma 
Bu işlevsel alan, gerçek donanım aygıtının ve sürücünün iç veri yapılarının başlatılama sorumluluğundadır. Başlatma işlemi tamamlanana kadar diğer sürücü hizmetlerini çağırmaya izin verilmez.

> [!IMPORTANT]
> Sürücünün başlatma işlevi bileşeni genellikle tx_application_define **işlevinden veya bir** başlatma iş parçacığından çağrılır.

### <a name="driver-control"></a>Sürücü Denetimi 
Sürücü başlatıldıktan ve işlem için hazır olduktan sonra, bu işlevsel alan çalışma zamanı denetiminden sorumludur. Genellikle, çalışma zamanı denetimi temel donanım cihazında değişiklik yapmakla oluşur. Örnek olarak seri bir cihazın sabit oranını değiştirme veya diskte yeni bir kesim arama örnek olarak verilmiştir.

### <a name="driver-access"></a>Sürücü Erişimi 
Bazı cihaz sürücüleri yalnızca tek bir uygulama iş parçacığından çağrılır. Böyle durumlarda bu işlevsel alan gerekli değildir. Ancak, birden çok iş parçacığının eşzamanlı sürücü erişimine ihtiyacı olan uygulamalarda, etkileşimleri cihaz sürücüsüne atama/sürüm özellikleri ek olarak denetlenmektedir. Alternatif olarak, uygulama sürücü erişimini kontrol etmek ve sürücü içinde ek yük ve sorunlardan kaçınmak için bir semafor kullanabilir. 

### <a name="driver-input"></a>Sürücü Girişi 
Bu işlev alanı tüm cihaz girişlerini sorumludur. Sürücü girişiyle ilişkili asıl sorunlar genellikle girişin arabelleğe nasıl dahil olduğunu ve iş parçacıklarının bu girişi beklemesini içerir. 

### <a name="driver-output"></a>Sürücü Çıkışı 
Bu işlev alanı tüm cihaz çıkışından sorumludur. Sürücü çıkışıyla ilişkili asıl sorunlar genellikle çıkışın nasıl arabelleğe alma ve iş parçacıklarının çıkışı gerçekleştirmeyi beklemesi konularını içerir. 

### <a name="driver-interrupts"></a>Sürücü Kesintileri 
Gerçek zamanlı sistemlerin çoğu cihaz girişi, çıkışı, denetimi ve hata olaylarını sürücüye bildirmek için donanım kesintilerine güvenmektedir. Kesintiler, bu tür dış olaylara garantili bir yanıt süresi sağlar. Kesintiler yerine, sürücü yazılımı bu tür olaylar için dış donanımı düzenli aralıklarla kontrol ediyor olabilir. Bu teknik yoklama *olarak adlandırılan bir tekniktir.* Bu, kesintilere göre daha az gerçek zamanlıdır, ancak yoklama bazı daha az gerçek zamanlı uygulamalar için anlamlı olabilir. 

### <a name="driver-status"></a>Sürücü Durumu 
Bu işlev alanı, sürücü işlemiyle ilişkili çalışma zamanı durumunu ve istatistikleri sağlamakla sorumludur. Bu işlev alanı tarafından yönetilen bilgiler genellikle şunları içerir: 
- Geçerli cihaz durumu
- Giriş baytları
- Çıkış baytları
- Cihaz hata sayıları

### <a name="driver-termination"></a>Sürücü Sonlandırma 
Bu işlev alanı isteğe bağlıdır. Yalnızca sürücünün ve/veya fiziksel donanım aygıtının kapanması gerektiğinde gereklidir. Sonlandırıldıktan sonra, sürücü yeniden başlatılana kadar yeniden çağrılmama gerekir. 

## <a name="simple-driver-example"></a>Basit Sürücü Örneği

Bir cihaz sürücüsünü açıklamanın en iyi yolu bir örnektir. Bu örnekte sürücü, yapılandırma yazmaci, giriş yazmaci ve çıkış yazmaci ile basit bir seri donanım cihazı varsayıyor. Bu basit sürücü örneği başlatma, giriş, çıkış ve kesme işlevsel alanlarını göstermektedir.

### <a name="simple-driver-initialization"></a>Basit Sürücü Başlatma 
Basit ***tx_sdriver_initialize*** işlevi, sürücünün giriş ve çıkış işlemi yönetmek için kullanılan iki sayma semaforu oluşturur. Giriş semaforu, seri donanım cihazı tarafından bir karakter alınca giriş ISR tarafından ayarlanır. Bu nedenle, giriş semaforu ilk sıfır sayısıyla oluşturulur.

Buna karşılık, çıkış semaforu seri donanım iletme yazmaca kullanılabilirliğini gösterir. İletme kaydının başlangıçta kullanılabilir olduğunu belirtmek için bir değeriyle oluşturulur.

Başlatma işlevi ayrıca giriş ve çıkış bildirimleri için alt düzey kesme vektörü işleyicilerini yüklemekle de sorumludur. Diğer ThreadX SMP kesme hizmeti yordamları gibi, alt düzey işleyici basit sürücü **ISR'sini çağırmadan** önce * _tx_thread_context_save _ çağrısı yapmak gerekir. Sürücü ISR döndürdikten sonra, alt düzey işleyicinin _*_ tx_thread_context_restore **_çağrısında tx_thread_context_restore_ gerekir.

> [!IMPORTANT]
> Başlatmanın diğer sürücü işlevlerinden önce çağrılsı önemlidir. Genellikle, sürücü başlatma, 'den **tx_application_define.**

Basit sürücünün başlatma kaynak kodu için sayfa 306'da Şekil 9'a bakın.

```C
VOID     tx_sdriver_initialize(VOID)
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
**ŞEKIL 9. Basit Sürücü Başlatma**

### <a name="simple-driver-input"></a>Basit Sürücü Girişi 
Giriş semafor çevresinde basit sürücü merkezleri. Seri cihaz giriş kesintisi geldiğinde, giriş semaforu ayarlanır. Bir veya daha fazla iş parçacığı sürücüden bir karakter bekliyorsa, en uzun bekleyen iş parçacığı devam eder. Bekleyen iş parçacığı yoksa, bir iş parçacığı sürücü giriş işlevini çağırana kadar semafor yalnızca ayarlanmış olarak kalır.

Basit sürücü girişi işlemeyle ilgili birkaç sınırlama vardır. En önemli olan giriş karakterlerini bırakma potansiyelidir. Bunun nedeni, önceki karakter işlenmeden önce gelen giriş karakterlerini arabelleğe alma özelliği yoktur. Bu, bir giriş karakteri arabelleği ekleyerek kolayca iş görür.

> [!IMPORTANT]
> Yalnızca iş parçacıklarının tx_sdriver_input **çağırmalarına izin** verilir.

Şekil 10'da basit sürücü girişiyle ilişkili kaynak kodu gösterir.

```C
UCHAR     tx_sdriver_input(VOID)
{

    /* Determine if there is a character waiting. If not,
        suspend. */
    tx_semaphore_get(&tx_sdriver_input_semaphore,
                                             TX_WAIT_FOREVER;
    /* Return character from serial RX hardware register. */
    return(*serial_hardware_input_ptr);
}

VOID     tx_sdriver_input_ISR(VOID)
{
    /* See if an input character notification is pending. */
    if (!tx_sdriver_input_semaphore.tx_semaphore_count)
    {
        /* If not, notify thread of an input character. */
        tx_semaphore_put(&tx_sdriver_input_semaphore);
    }
}
```
**ŞEKIL 10. Basit Sürücü Girişi**

### <a name="simple-driver-output"></a>Basit Sürücü Çıkışı 
Çıkış işleme, seri cihazın iletim yazmaca serbest bırakılana işaret etmek için çıkış semaforu kullanır. Cihaza aslında bir çıkış karakteri yazmadan önce çıkış semaforu elde edilir. Kullanılamıyorsa, önceki iletme henüz tamamlanmadı.

Aktarım tamamlama kesme işleminin işlenmesinden çıkış ISR sorumludur. Çıkış ISR'sinde işlem, çıkış semaforu ayarlamaya ve böylece başka bir karakterin çıkışına izin verecek şekilde tutar.

> [!IMPORTANT]
> Yalnızca iş parçacıklarının tx_sdriver_output **izin** verilir.

Şekil 11'de basit sürücü çıkışıyla ilişkili kaynak kodu gösterir.

```C
VOID     tx_sdriver_output(UCHAR alpha)
{

    /* Determine if the hardware is ready to transmit a
       character. If not, suspend until the previous output
        completes. */
    tx_semaphore_get(&tx_sdriver_output_semaphore,
                                            TX_WAIT_FOREVER);
    /* Send the character through the hardware. */
    *serial_hardware_output_ptr = alpha;
}

VOID     tx_sdriver_output_ISR(VOID)
{
    /* Notify thread last character transmit is
        complete. */
    tx_semaphore_put(&tx_sdriver_output_semaphore);
}
```
**ŞEKIL 11. Basit Sürücü Çıkışı**

### <a name="simple-driver-shortcomings"></a>Basit Sürücü Eksikleri 
Bu basit cihaz sürücüsü örneği, ThreadX SMP cihaz sürücüsünün temel fikirlerini gösterir. Ancak, basit cihaz sürücüsü veri arabelleğe alma veya ek yük sorunlarını ele almayacağı için gerçek dünya ThreadX SMP sürücülerini tam olarak temsil etmez. Aşağıdaki bölümde, cihaz sürücüleriyle ilişkili daha gelişmiş sorunlardan bazıları açık almaktadır.

## <a name="advanced-driver-issues"></a>Gelişmiş Sürücü Sorunları

Daha önce belirtildiği gibi, cihaz sürücülerinin uygulamaları kadar benzersiz gereksinimleri vardır. Bazı uygulamalar çok büyük miktarda veri arabelleğe alma gerektirirken, başka bir uygulama yüksek sıklıkta cihaz kesintileri nedeniyle iyileştirilmiş sürücü ISR'leri gerektirebilir.

### <a name="io-buffering"></a>I/O Arabelleğe Alma 
Gerçek zamanlı ekli uygulamalarda veri arabelleğe alma için önemli planlamalar gerekir. Tasarımın bazıları, temel alınan donanım cihazı tarafından dikte edilen bir tasarımdır. Cihaz temel bir bayt I/O sağlarsa, büyük olasılıkla basit bir döngüsel arabellek sırasına göredir. Ancak, cihaz blok, DMA veya paket I/O sağlarsa, büyük olasılıkla bir arabellek yönetim şeması gerekir. 

### <a name="circular-byte-buffers"></a>Döngüsel Byte Arabellekleri 
Döngüsel bayt arabellekleri genellikle UART gibi basit bir seri donanım cihazı yöneten sürücülerde kullanılır. İki döngüsel arabellek en çok bu tür durumlarda kullanılır: biri giriş, biri çıkış için.

Her döngüsel bayt arabelleği bir bayt bellek alanı (genellikle bir UCHAR dizisi), okuma işaretçisi ve yazma işaretçisi içerir. Okuma işaretçisi ve yazma işaretçileri arabellekte aynı bellek konumuyla ilgili olduğunda arabellek boş olarak kabul edilir. Sürücü başlatma, hem okuma hem de yazma arabellek işaretçilerini arabelleğin başlangıç adresine ayarlar.

### <a name="circular-buffer-input"></a>Döngüsel Arabellek Girişi 
Giriş arabelleği, uygulama hazır olmadan önce gelen karakterleri tutmak için kullanılır. Bir giriş karakteri (genellikle bir kesme hizmeti yordamında) alınca, yeni karakter donanım cihazından alınır ve yazma işaretçisi tarafından işaret ettiği konumda giriş arabelleğine yerleştirilir. Yazma işaretçisi daha sonra arabellekte bir sonraki konuma ileri doğru ilerler. Sonraki konum, arabelleğin sonunu geçmişse, yazma işaretçisi arabelleğin başına ayarlanır. Yeni yazma işaretçisi okuma işaretçisi ile aynı ise, kuyruk tam koşulu yazma işaretçisi ilerlemesi iptal edilir.

Sürücüye yapılan uygulama giriş bayt istekleri önce giriş arabelleğinin okuma ve yazma işaretçilerini inceler. Okuma ve yazma işaretçileri aynı ise arabellek boştur. Aksi takdirde, okuma işaretçisi aynı değilse, okuma işaretçisi tarafından işaret eden bayt giriş arabelleğinden kopyalanır ve okuma işaretçisi sonraki arabellek konumu için gelişmiştir. Yeni okuma işaretçisi arabelleğin sonunu geçmişse en baştan sıfırlanır. Şekil 12'de döngüsel giriş arabelleğinin mantığı yer almaktadır.

```C
UCHAR     tx_input_buffer[MAX_SIZE];
UCHAR     tx_input_write_ptr;
UCHAR     tx_input_read_ptr;

/* Initialization.  */
tx_input_write_ptr =  &tx_input_buffer[0];
tx_input_read_ptr =    &tx_input_buffer[0];

/* Input byte ISR... UCHAR alpha has character from device. */
save_ptr =  tx_input_write_ptr;
*tx_input_write_ptr++ =  alpha;
if (tx_input_write_ptr > &tx_input_buffer[MAX_SIZE-1])
    tx_input_write_ptr =  &tx_input_buffer[0];  /* Wrap */
if (tx_input_write_ptr == tx_input_read_ptr)
    tx_input_write_ptr =  save_ptr;  /* Buffer full */

/* Retrieve input byte from buffer... */
if (tx_input_read_ptr != tx_input_write_ptr)
{
    alpha =  *tx_input_read_ptr++;
    if (tx_input_read_ptr > &tx_input_buffer[MAX_SIZE-1])
        tx_input_read_ptr =  &tx_input_buffer[0];
}
```
**ŞEKIL 12. Döngüsel Giriş Arabelleği mantığı**

> [!IMPORTANT]
> Güvenilir işlem için, hem giriş hem de çıkış döngüsel arabelleklerinin okuma ve yazma işaretçileri işlenebilirken kesmeleri kilitlemek gerekebilir.

### <a name="circular-output-buffer"></a>Döngüsel Çıkış Arabelleği 
Çıkış arabelleği, donanım cihazı önceki baytı göndermeden önce çıkışa gelen karakterleri tutmak için kullanılır. Çıkış arabelleği işlemesi giriş arabelleği işlemeye benzer, ancak aktarım tam kesme işlemesi çıkış okuma işaretçisini, uygulama çıkış isteği ise çıkış yazma işaretçisini kullanır. Aksi takdirde, çıkış arabelleği işlemesi aynıdır. Şekil 13'te döngüsel çıkış arabelleğinin mantığı gösterildi.

```C
UCHAR     tx_output_buffer[MAX_SIZE];
UCHAR     tx_output_write_ptr;
UCHAR     tx_output_read_ptr;

/* Initialization.  */
tx_output_write_ptr =  &tx_output_buffer[0];
tx_output_read_ptr =   &tx_output_buffer[0];

/* Transmit complete ISR... Device ready to send. */
if (tx_output_read_ptr != tx_output_write_ptr)
{
    *device_reg =  *tx_output_read_ptr++;
    if (tx_output_read_reg > &tx_output_buffer[MAX_SIZE-1])
    tx_output_read_ptr =  &tx_output_buffer[0];
}

/* Output byte driver service. If device busy, buffer! */
save_ptr =  tx_output_write_ptr;
*tx_output_write_ptr++ =  alpha;
if (tx_output_write_ptr > &tx_output_buffer[MAX_SIZE-1])
    tx_output_write_ptr =  &tx_output_buffer[0];  /* Wrap */
if (tx_output_write_ptr == tx_output_read_ptr)
    tx_output_write_ptr =  save_ptr;  /* Buffer full!  */
```
**ŞEKIL 13. Döngüsel Çıkış Arabelleği mantığı**

### <a name="buffer-io-management"></a>Arabellek I/O Yönetimi 
Ekli mikro işlemcilerin performansını geliştirmek için birçok çevresel cihaz, yazılım tarafından sağlanan arabelleklerle veri iletir ve alır. Bazı uygulamalar, tek tek veri paketlerini iletmek veya almak için birden çok arabellek kullanılabilir. 

I/O arabelleklerinin boyutu ve konumu, uygulama ve/veya sürücü yazılımı tarafından belirlenir. Arabellekler genellikle boyut olarak sabittir ve bir ThreadX SMP blok bellek havuzu içinde yönetilir. Şekil 14'te tipik bir I/O arabelleği ve ayırmayı yöneten ThreadX SMP blok bellek havuzu yer alır.

```C
typedef struct TX_IO_BUFFER_STRUCT
{

      struct TX_IO_BUFFER_STRUCT *tx_next_packet;
    struct TX_IO_BUFFER_STRUCT *tx_next_buffer;
      UCHAR  tx_buffer_area[TX_MAX_BUFFER_SIZE];
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
Typedef TX_IO_BUFFER iki işaretçiden oluşur. ***tx_next_packet** _ işaretçisi, giriş veya çıkış listesinde birden çok paketin bağlantısını yapmak için kullanılır. _ *_tx_next_buffer_** işaretçisi, cihazdan tek bir veri paketinin yer alan arabelleklerini bir araya araya getirdi. Arabellek havuzdan ayrılırken bu işaretçilerin her ikisi de NULL olarak ayarlanır. Buna ek olarak, bazı cihazlar arabellek alanın gerçekte ne kadar veri içerdiğini belirtmek için başka bir alan gerektirmektedir.

### <a name="buffered-io-advantage"></a>Arabelleğe Alındı I/O Avantajı 
Arabellek I/O şemasının avantajları nelerdir? En büyük avantajı, verilerin cihaz kayıtları ile uygulamanın belleği arasında kopyalanmamalarındandır. Bunun yerine sürücü, cihaza bir dizi arabellek işaretçisi sağlar. Fiziksel cihaz I/O, sağlanan arabellek belleğini doğrudan kullanır.

bilgi giriş veya çıkış paketlerini kopyalamak için işlemcinin kullanımı son derece maliyetlidir ve yüksek aktarım hızı G/Ç durumlarında kaçınılmalıdır.

Arabelleğe alan G/Ç yaklaşımının bir diğer avantajı, giriş ve çıkış listelerinin tam koşulların yer almamış olduğudır. Kullanılabilir tüm arabellekler herhangi bir anda her iki listede de olabilir. Bu, bölümün önceki kısımlarında sunulan basit bayt döngüsel arabellekleriyle karşıttır. Her biri derlemede belirlenen sabit bir boyuta sahipti.

### <a name="buffered-driver-responsibilities"></a>Arabelleğe Alındı Sürücü Sorumlulukları 
Arabelleğe alan cihaz sürücüleri yalnızca bağlantılı I/O arabellek listelerini yönetmekle ilgilidir. Uygulama yazılımı hazır olmadan önce alınan paketler için bir giriş arabelleği listesi korunur. Buna karşılık, donanım aygıtının bunları işleyene kadar daha hızlı gönderilen paketler için bir çıkış arabellek listesi korunur. Şekil 314'te Şekil 15'te veri paketlerinin basit giriş ve çıkış bağlantılı listeleri ve her bir paketin arabellekleri görüntülenir.

![Arabelleğe Alındı Sürücü Sorumlulukları](media/image11.png)

**ŞEKIL 15. Input-Output Listeleri**

Aynı I/O arabellekleri ile arabelleğe alan sürücülere sahip uygulamalar arabirimi. Aktarımda, uygulama yazılımı sürücüye iletilen bir veya daha fazla arabellek sağlar. Uygulama yazılımı giriş isteğinde olduğunda sürücü G/Ç arabellekleri içinde giriş verilerini döndürür.

> [!IMPORTANT]
> Bazı uygulamalarda, uygulamanın sürücüden bir giriş arabelleği için boş arabellek değiştirmesini gerektiren bir sürücü giriş arabirimi oluşturmak yararlı olabilir. Bu, sürücünün içindeki bazı arabellek ayırma işlemlerini hafifletmeye neden olabilir.

### <a name="interrupt-management"></a>Kesinti Yönetimi 
Bazı uygulamalarda cihaz kesme sıklığı, ISR'nin C'de yazarak veya her kesmede ThreadX SMP ile etkileşim kurmasını yasaklar. Örneğin, kesintiye neden olan bağlamı kaydetmek ve geri yüklemek 25us sürerse, kesme sıklığı 50us ise tam bağlam kaydetmesi tavsiye edilemez. Bu gibi durumlarda, cihaz kesintilerinin çoğunu işlemek için küçük bir derleme dili ISR kullanılır. Bu düşük başlı ISR yalnızca gerektiğinde ThreadX SMP ile etkileşime geçmeli.

Benzer bir tartışma, Bölüm 3'in sonundaki kesme yönetimi tartışmalarında bulunabilir.

> [!NOTE]
> Sürücü kodunun kritik bölümlerini sürücü ISR kodundan korumak için kesme kilitleme kullanılacaksa, iş parçacığı düzeyinde sürücü kodu her zaman ISR'nin işlendiğinde aynı çekirdekte yürütülecektir. Aksi takdirde, çekirdekler arası koruma yerleşik TX_DISABLE TX_RESTORE iç ThreadX SMP temelleri de kullanılmalıdır.

### <a name="thread-suspension"></a>İş ParçacığıNı Askıya Alma 
Bu bölümün başlarında sunulan basit sürücü örneğinde, bir karakter yoksa giriş hizmetini çağıran askıya alır. Bazı uygulamalarda bu kabul edilebilir bir durum değildir.

Örneğin, bir sürücüden gelen girişi işlemeden sorumlu iş parçacığının başka görevleri de varsa, yalnızca sürücü girişinin askıya alınması büyük olasılıkla işe yaramayacaktır. Bunun yerine, diğer işleme isteklerinin iş parçacığına yapılmasına benzer şekilde, sürücünün istek işleme için özelleştirilebilir olması gerekir.

Çoğu durumda, giriş arabelleği bağlantılı bir listeye yerleştirilir ve iş parçacığının giriş kuyruğuna bir giriş olayı iletisi gönderilir.