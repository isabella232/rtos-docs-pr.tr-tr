---
title: Ek-bağlantı noktasına özgü örnekler
description: Bu makalede, ThreadX modülleri için bağlantı noktasına özgü örnekler gösterilmektedir.
author: philmea
ms.author: philmea
ms.date: 07/15/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: c2324a2057bf2ddb2d255b2ff611d34fc664560a
ms.sourcegitcommit: 60ad844b58639d88830f2660ab0c4ff86b92c10f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2021
ms.locfileid: "106549819"
---
# <a name="appendix---port-specific-examples"></a><span data-ttu-id="f8e6b-103">Ek-bağlantı noktasına özgü örnekler</span><span class="sxs-lookup"><span data-stu-id="f8e6b-103">Appendix - Port-specific examples</span></span>

## <a name="arm11-processor"></a><span data-ttu-id="f8e6b-104">ARM11 işlemcisi</span><span class="sxs-lookup"><span data-stu-id="f8e6b-104">ARM11 processor</span></span>

### <a name="arm11-using-gcc"></a><span data-ttu-id="f8e6b-105">GCC kullanarak ARM11</span><span class="sxs-lookup"><span data-stu-id="f8e6b-105">ARM11 using GCC</span></span>

#### <a name="module-preamble-for-arm11-using-gcc"></a><span data-ttu-id="f8e6b-106">GCC kullanarak ARM11 için modül girişi</span><span class="sxs-lookup"><span data-stu-id="f8e6b-106">Module preamble for ARM11 using GCC</span></span>

```armasm
    .arm
    .section .preamble, "ax"

    /* Define the module preamble.  */

    .global _txm_module_preamble
_txm_module_preamble:
    .word       0x4D4F4455                                      @ Module ID
    .word       0x5                                             @ Module Major Version
    .word       0x6                                             @ Module Minor Version
    .word       32                                              @ Module Preamble Size in 32-bit words
    .word       0x12345678                                      @ Module ID (application defined)
    .word       0x02000000                                      @ Module Properties where:
                                                                @   Bits 31-24: Compiler ID
                                                                @           0 -> IAR
                                                                @           1 -> ARM
                                                                @           2 -> GNU
    .word       _txm_module_thread_shell_entry - . - 0          @ Module Shell Entry Point
    .word       demo_module_start - . - 0                       @ Module Start Thread Entry Point
    .word       0                                               @ Module Stop Thread Entry Point
    .word       1                                               @ Module Start/Stop Thread Priority
    .word       1024                                            @ Module Start/Stop Thread Stack Size
    .word       _txm_module_callback_request_thread_entry - . - 0   @ Module Callback Thread Entry
    .word       1                                               @ Module Callback Thread Priority
    .word       1024                                            @ Module Callback Thread Stack Size
    .word       __code_size__                                   @ Module Code Size
    .word       __data_size__                                   @ Module Data Size
    .word       0                                               @ Reserved 0
    .word       0                                               @ Reserved 1
    .word       0                                               @ Reserved 2
    .word       0                                               @ Reserved 3
    .word       0                                               @ Reserved 4
    .word       0                                               @ Reserved 5
    .word       0                                               @ Reserved 6
    .word       0                                               @ Reserved 7  
    .word       0                                               @ Reserved 8  
    .word       0                                               @ Reserved 9
    .word       0                                               @ Reserved 10
    .word       0                                               @ Reserved 11
    .word       0                                               @ Reserved 12
    .word       0                                               @ Reserved 13
    .word       0                                               @ Reserved 14
    .word       0                                               @ Reserved 15
```

#### <a name="module-properties-for-arm11-using-gcc"></a><span data-ttu-id="f8e6b-107">GCC kullanarak ARM11 için modül özellikleri</span><span class="sxs-lookup"><span data-stu-id="f8e6b-107">Module properties for ARM11 using GCC</span></span>

| <span data-ttu-id="f8e6b-108">Sürümleri</span><span class="sxs-lookup"><span data-stu-id="f8e6b-108">Bit</span></span> | <span data-ttu-id="f8e6b-109">Değer</span><span class="sxs-lookup"><span data-stu-id="f8e6b-109">Value</span></span> | <span data-ttu-id="f8e6b-110">Anlamı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-110">Meaning</span></span> |
|---|---|---|
| <span data-ttu-id="f8e6b-111">[23-0]</span><span class="sxs-lookup"><span data-stu-id="f8e6b-111">[23-0]</span></span> | <span data-ttu-id="f8e6b-112">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-112">0</span></span> | <span data-ttu-id="f8e6b-113">Ayrılmıştır</span><span class="sxs-lookup"><span data-stu-id="f8e6b-113">Reserved</span></span>
| <span data-ttu-id="f8e6b-114">[31-24]</span><span class="sxs-lookup"><span data-stu-id="f8e6b-114">[31-24]</span></span> | <br /><span data-ttu-id="f8e6b-115">-</span><span class="sxs-lookup"><span data-stu-id="f8e6b-115">0x00</span></span><br /><span data-ttu-id="f8e6b-116">0x01</span><span class="sxs-lookup"><span data-stu-id="f8e6b-116">0x01</span></span><br /><span data-ttu-id="f8e6b-117">0x02</span><span class="sxs-lookup"><span data-stu-id="f8e6b-117">0x02</span></span> | <span data-ttu-id="f8e6b-118">**Derleyici KIMLIĞI**</span><span class="sxs-lookup"><span data-stu-id="f8e6b-118">**Compiler ID**</span></span><br /><span data-ttu-id="f8e6b-119">IAR dili</span><span class="sxs-lookup"><span data-stu-id="f8e6b-119">IAR</span></span><br /><span data-ttu-id="f8e6b-120">ARM</span><span class="sxs-lookup"><span data-stu-id="f8e6b-120">ARM</span></span><br /><span data-ttu-id="f8e6b-121">GNU</span><span class="sxs-lookup"><span data-stu-id="f8e6b-121">GNU</span></span> |

#### <a name="module-linker-for-arm11-using-gcc"></a><span data-ttu-id="f8e6b-122">GCC kullanarak ARM11 için modül Bağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-122">Module linker for ARM11 using GCC</span></span>

```c
MEMORY
{
  FLASH (rx) : ORIGIN = 0x080F0000, LENGTH = 0x00010000
  RAM   (wx) : ORIGIN = 0x64001800, LENGTH = 0x00100000
}


SECTIONS
{
  __FLASH_segment_start__ = 0x080F0000;
  __FLASH_segment_end__   = 0x080FFFFF;
  __RAM_segment_start__   = 0x64001800;
  __RAM_segment_end__     = 0x64011800;

  __HEAPSIZE__ = 128;

  __preamble_load_start__ = __FLASH_segment_start__;
  .preamble __FLASH_segment_start__ : AT(__FLASH_segment_start__)
  {
    __preamble_start__ = .;
    *(.preamble .preamble.*)
  }
  __preamble_end__ = __preamble_start__ + SIZEOF(.preamble);

  __dynsym_load_start__ =  ALIGN(__preamble_end__ , 4);
  .dynsym ALIGN(__dynsym_load_start__ , 4) : AT(ALIGN(__dynsym_load_start__ , 4))
  {
    . = ALIGN(4);
    KEEP (*(.dynsym))
    KEEP (*(.dynsym*))
    . = ALIGN(4);
  }
  __dynsym_end__ = __dynsym_load_start__ + SIZEOF(.dynsym);

  __dynstr_load_start__ =  ALIGN(__dynsym_end__ , 4);
  .dynstr ALIGN(__dynstr_load_start__ , 4) : AT(ALIGN(__dynstr_load_start__, 4))
  {
    . = ALIGN(4);
    KEEP (*(.dynstr))
    KEEP (*(.dynstr*))
    . = ALIGN(4);
  }
  __dynstr_end__ = __dynstr_load_start__ + SIZEOF(.dynstr);

  __reldyn_load_start__ =  ALIGN(__dynstr_end__ , 4);
  .rel.dyn ALIGN(__reldyn_load_start__ , 4) : AT(ALIGN(__reldyn_load_start__ , 4))
  {
    . = ALIGN(4);
    KEEP (*(.rel.dyn))
    KEEP (*(.rel.dyn*))
    . = ALIGN(4);
  }
  __reldyn_end__ = __reldyn_load_start__ + SIZEOF(.rel.dyn);

  __relplt_load_start__ =  ALIGN(__reldyn_end__ , 4);
  .rel.plt ALIGN(__relplt_load_start__ , 4) : AT(ALIGN(__relplt_load_start__ , 4))
  {
    . = ALIGN(4);
    KEEP (*(.rel.plt))
    KEEP (*(.rel.plt*))
    . = ALIGN(4);
  }
  __relplt_end__ = __relplt_load_start__ + SIZEOF(.rel.plt);

  __plt_load_start__ =  ALIGN(__relplt_end__ , 4);
  .plt ALIGN(__plt_load_start__ , 4) : AT(ALIGN(__plt_load_start__ , 4))
  {
    . = ALIGN(4);
    KEEP (*(.plt))
    KEEP (*(.plt*))
    . = ALIGN(4);
  }
  __plt_end__ = __plt_load_start__ + SIZEOF(.plt);

  __interp_load_start__ =  ALIGN(__plt_end__ , 4);
  .interp ALIGN(__interp_load_start__ , 4) : AT(ALIGN(__interp_load_start__ , 4))
  {
    . = ALIGN(4);
    KEEP (*(.interp))
    KEEP (*(.interp*))
    . = ALIGN(4);
  }
  __interp_end__ = __interp_load_start__ + SIZEOF(.interp);

  __hash_load_start__ =  ALIGN(__interp_end__ , 4);
  .hash ALIGN(__hash_load_start__ , 4) : AT(ALIGN(__hash_load_start__, 4))
  {
    . = ALIGN(4);
    KEEP (*(.hash))
    KEEP (*(.hash*))
    . = ALIGN(4);
  }
  __hash_end__ = __hash_load_start__ + SIZEOF(.hash);

  __text_load_start__ =  ALIGN(__hash_end__ , 4);
  .text ALIGN(__text_load_start__ , 4) : AT(ALIGN(__text_load_start__, 4))
  {
    __text_start__ = .;
    *(.text .text.* .glue_7t .glue_7 .gnu.linkonce.t.* .gcc_except_table  )
  }
  __text_end__ = __text_start__ + SIZEOF(.text);

  __dtors_load_start__ = ALIGN(__text_end__ , 4);
  .dtors ALIGN(__text_end__ , 4) : AT(ALIGN(__text_end__ , 4))
  {
    __dtors_start__ = .;
    KEEP (*(SORT(.dtors.*))) KEEP (*(.dtors))
  }
  __dtors_end__ = __dtors_start__ + SIZEOF(.dtors);

  __ctors_load_start__ = ALIGN(__dtors_end__ , 4);
  .ctors ALIGN(__dtors_end__ , 4) : AT(ALIGN(__dtors_end__ , 4))
  {
    __ctors_start__ = .;
    KEEP (*(SORT(.ctors.*))) KEEP (*(.ctors))
  }
  __ctors_end__ = __ctors_start__ + SIZEOF(.ctors);

  __got_load_start__ = ALIGN(__ctors_end__ , 4);
  .got ALIGN(__ctors_end__ , 4) : AT(ALIGN(__ctors_end__ , 4))
  {
    . = ALIGN(4);
    _sgot = .;
    KEEP (*(.got))
    KEEP (*(.got*))
    . = ALIGN(4);
    _egot = .;
  }
  __got_end__ =  __got_load_start__ + SIZEOF(.got);

  __rodata_load_start__ = ALIGN(__got_end__ , 4);
  .rodata ALIGN(__got_end__ , 4) : AT(ALIGN(__got_end__ , 4))
  {
    __rodata_start__ = .;
    *(.rodata .rodata.* .gnu.linkonce.r.*)
  }
  __rodata_end__ = __rodata_start__ + SIZEOF(.rodata);

  __code_size__ =  __rodata_end__ - __FLASH_segment_start__;

  __fast_load_start__ = ALIGN(__rodata_end__ , 4);

  __fast_load_end__ = __fast_load_start__ + SIZEOF(.fast);

  __new_got_start__ = ALIGN(__RAM_segment_start__ , 4);

  __new_got_end__ =  __new_got_start__ + SIZEOF(.got);

  .fast ALIGN(__new_got_end__ , 4) : AT(ALIGN(__rodata_end__ , 4))
  {
    __fast_start__ = .;
    *(.fast .fast.*)
  }
  __fast_end__ = __fast_start__ + SIZEOF(.fast);

  .fast_run ALIGN(__fast_end__ , 4) (NOLOAD) :
  {
    __fast_run_start__ = .;
    . = MAX(__fast_run_start__ + SIZEOF(.fast), .);
  }
  __fast_run_end__ = __fast_run_start__ + SIZEOF(.fast_run);

  __data_load_start__ = ALIGN(__fast_load_start__ + SIZEOF(.fast) , 4);
  .data ALIGN(__fast_run_end__ , 4) : AT(ALIGN(__fast_load_start__ + SIZEOF(.fast) , 4))
  {
    __data_start__ = .;
    *(.data .data.* .gnu.linkonce.d.*)
  }
  __data_end__ = __data_start__ + SIZEOF(.data);

  __data_load_end__ = __data_load_start__ + SIZEOF(.data);

  __FLASH_segment_used_end__ = ALIGN(__fast_load_start__ + SIZEOF(.fast) , 4) + SIZEOF(.data);

  .data_run ALIGN(__fast_run_end__ , 4) (NOLOAD) :
  {
    __data_run_start__ = .;
    . = MAX(__data_run_start__ + SIZEOF(.data), .);
  }
  __data_run_end__ = __data_run_start__ + SIZEOF(.data_run);

  __bss_load_start__ = ALIGN(__data_run_end__ , 4);
  .bss ALIGN(__data_run_end__ , 4) (NOLOAD) : AT(ALIGN(__data_run_end__ , 4))
  {
    __bss_start__ = .;
    *(.bss .bss.* .gnu.linkonce.b.*) *(COMMON)
  }
  __bss_end__ = __bss_start__ + SIZEOF(.bss);

  __non_init_load_start__ = ALIGN(__bss_end__ , 4);
  .non_init ALIGN(__bss_end__ , 4) (NOLOAD) : AT(ALIGN(__bss_end__ , 4))
  {
    __non_init_start__ = .;
    *(.non_init .non_init.*)
  }
  __non_init_end__ = __non_init_start__ + SIZEOF(.non_init);

  __heap_load_start__ = ALIGN(__non_init_end__ , 4);
  .heap ALIGN(__non_init_end__ , 4) (NOLOAD) : AT(ALIGN(__non_init_end__ , 4))
  {
    __heap_start__ = .;
    *(.heap)
    . = ALIGN(MAX(__heap_start__ + __HEAPSIZE__ , .), 4);
  }
  __heap_end__ = __heap_start__ + SIZEOF(.heap);

  __data_size__ =  __heap_end__ - __RAM_segment_start__;

}
```

#### <a name="building-modules-for-arm11-using-gcc"></a><span data-ttu-id="f8e6b-123">GCC kullanarak ARM11 için modüller oluşturma</span><span class="sxs-lookup"><span data-stu-id="f8e6b-123">Building Modules for ARM11 using GCC</span></span>

<span data-ttu-id="f8e6b-124">GCC kullanarak ARM11 modülü oluşturmaya yönelik basit bir komut satırı örneği:</span><span class="sxs-lookup"><span data-stu-id="f8e6b-124">A simple command-line example for building an ARM11 module using GCC:</span></span>

```dos
arm-none-eabi-gcc -c -g -mcpu=arm1136j-s -msingle-pic-base -fPIC -mpic-register=r9 txm_module_preamble.S
arm-none-eabi-gcc -c -g -mcpu=arm1136j-s -msingle-pic-base -fPIC -mpic-register=r9 gcc_setup.S
arm-none-eabi-gcc -c -g -mcpu=arm1136j-s -msingle-pic-base -fPIC -mpic-register=r9 demo_threadx_module.c
arm-none-eabi-ld -A arm1136j-s -T demo_threadx_module.ld txm_module_preamble.o gcc_setup.o demo_threadx_module.o txm.a txm.a -o demo_threadx_module.out -M > demo_threadx_module.map
```

#### <a name="thread-extension-definition-for-arm11-using-gcc"></a><span data-ttu-id="f8e6b-125">GCC kullanarak ARM11 için iş parçacığı uzantısı tanımı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-125">Thread extension definition for ARM11 using GCC</span></span>

```c
#define TX_THREAD_EXTENSION_2   VOID    *tx_thread_module_instance_ptr;  \
                                VOID    *tx_thread_module_entry_info_ptr;
```

#### <a name="building-module-manager-for-arm11-using-gcc"></a><span data-ttu-id="f8e6b-126">GCC kullanarak ARM11 için Modül Yöneticisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="f8e6b-126">Building Module Manager for ARM11 using GCC</span></span>

<span data-ttu-id="f8e6b-127">Örnek sağlanmaz.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-127">No example is provided.</span></span>

#### <a name="attributes-for-external-memory-enable-api-for-arm11-using-gcc"></a><span data-ttu-id="f8e6b-128">Dış bellek öznitelikleri, GCC kullanarak ARM11 için API 'YI etkinleştirir</span><span class="sxs-lookup"><span data-stu-id="f8e6b-128">Attributes for external memory enable API for ARM11 using GCC</span></span>

<span data-ttu-id="f8e6b-129">Bu özellik bu bağlantı noktasında etkin değil.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-129">This feature not enabled on this port.</span></span>

### <a name="arm11-using-ac5"></a><span data-ttu-id="f8e6b-130">AC5 kullanarak ARM11</span><span class="sxs-lookup"><span data-stu-id="f8e6b-130">ARM11 using AC5</span></span>

#### <a name="module-preamble-for-arm11-using-ac5"></a><span data-ttu-id="f8e6b-131">AC5 kullanarak ARM11 için modül girişi</span><span class="sxs-lookup"><span data-stu-id="f8e6b-131">Module preamble for ARM11 using AC5</span></span>

```armasm
    AREA  Init, CODE, READONLY

;    /* Define public symbols.  */

    EXPORT __txm_module_preamble

;    /* Define application-specific start/stop entry points for the module.  */

    IMPORT demo_module_start

;    /* Define common external references.  */

    IMPORT  _txm_module_thread_shell_entry
    IMPORT  _txm_module_callback_request_thread_entry
    IMPORT  |Image$$ER_RO$$Length|

__txm_module_preamble
        DCD       0x4D4F4455                                        ; Module ID
        DCD       0x5                                               ; Module Major Version
        DCD       0x3                                               ; Module Minor Version
        DCD       32                                                ; Module Preamble Size in 32-bit words
        DCD       0x12345678                                        ; Module ID (application defined)
        DCD       0x01000000                                        ; Module Properties where:
                                                                    ;   Bits 31-24: Compiler ID
                                                                    ;           0 -> IAR
                                                                    ;           1 -> ARM
                                                                    ;           2 -> GNU
                                                                    ;   Bits 23-0:  Reserved
        DCD       _txm_module_thread_shell_entry - . + .            ; Module Shell Entry Point
        DCD       demo_module_start - . + .                         ; Module Start Thread Entry Point
        DCD       0                                                 ; Module Stop Thread Entry Point
        DCD       1                                                 ; Module Start/Stop Thread Priority
        DCD       1024                                              ; Module Start/Stop Thread Stack Size
        DCD       _txm_module_callback_request_thread_entry - . + . ; Module Callback Thread Entry
        DCD       1                                                 ; Module Callback Thread Priority
        DCD       1024                                              ; Module Callback Thread Stack Size
        DCD       |Image$$ER_RO$$Length|                            ; Module Code Size
        DCD       0x4000                                            ; Module Data Size - default to 16K (need to make sure this is large enough for module's data needs!)
        DCD       0                                                 ; Reserved 0
        DCD       0                                                 ; Reserved 1
        DCD       0                                                 ; Reserved 2
        DCD       0                                                 ; Reserved 3
        DCD       0                                                 ; Reserved 4
        DCD       0                                                 ; Reserved 5
        DCD       0                                                 ; Reserved 6
        DCD       0                                                 ; Reserved 7
        DCD       0                                                 ; Reserved 8  
        DCD       0                                                 ; Reserved 9
        DCD       0                                                 ; Reserved 10
        DCD       0                                                 ; Reserved 11
        DCD       0                                                 ; Reserved 12
        DCD       0                                                 ; Reserved 13
        DCD       0                                                 ; Reserved 14
        DCD       0                                                 ; Reserved 15

        END
```

#### <a name="module-properties-for-arm11-using-ac5"></a><span data-ttu-id="f8e6b-132">AC5 kullanarak ARM11 için modül özellikleri</span><span class="sxs-lookup"><span data-stu-id="f8e6b-132">Module properties for ARM11 using AC5</span></span>

| <span data-ttu-id="f8e6b-133">Sürümleri</span><span class="sxs-lookup"><span data-stu-id="f8e6b-133">Bit</span></span> | <span data-ttu-id="f8e6b-134">Değer</span><span class="sxs-lookup"><span data-stu-id="f8e6b-134">Value</span></span> | <span data-ttu-id="f8e6b-135">Anlamı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-135">Meaning</span></span> |
|---|---|---|
| <span data-ttu-id="f8e6b-136">[23-0]</span><span class="sxs-lookup"><span data-stu-id="f8e6b-136">[23-0]</span></span> | <span data-ttu-id="f8e6b-137">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-137">0</span></span> | <span data-ttu-id="f8e6b-138">Ayrılmıştır</span><span class="sxs-lookup"><span data-stu-id="f8e6b-138">Reserved</span></span>
| <span data-ttu-id="f8e6b-139">[31-24]</span><span class="sxs-lookup"><span data-stu-id="f8e6b-139">[31-24]</span></span> | <br /><span data-ttu-id="f8e6b-140">-</span><span class="sxs-lookup"><span data-stu-id="f8e6b-140">0x00</span></span><br /><span data-ttu-id="f8e6b-141">0x01</span><span class="sxs-lookup"><span data-stu-id="f8e6b-141">0x01</span></span><br /><span data-ttu-id="f8e6b-142">0x02</span><span class="sxs-lookup"><span data-stu-id="f8e6b-142">0x02</span></span> | <span data-ttu-id="f8e6b-143">**Derleyici KIMLIĞI**</span><span class="sxs-lookup"><span data-stu-id="f8e6b-143">**Compiler ID**</span></span><br /><span data-ttu-id="f8e6b-144">IAR dili</span><span class="sxs-lookup"><span data-stu-id="f8e6b-144">IAR</span></span><br /><span data-ttu-id="f8e6b-145">ARM</span><span class="sxs-lookup"><span data-stu-id="f8e6b-145">ARM</span></span><br /><span data-ttu-id="f8e6b-146">GNU</span><span class="sxs-lookup"><span data-stu-id="f8e6b-146">GNU</span></span> |

#### <a name="module-linker-for-arm11-using-ac5"></a><span data-ttu-id="f8e6b-147">AC5 kullanarak ARM11 için modül Bağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-147">Module linker for ARM11 using AC5</span></span>

<span data-ttu-id="f8e6b-148">Komut satırı üzerine inşa, bağlayıcı dosyası örneği yok.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-148">Built on command-line, no linker file example.</span></span>

#### <a name="building-modules-for-arm11-using-ac5"></a><span data-ttu-id="f8e6b-149">AC5 kullanarak ARM11 için modüller oluşturma</span><span class="sxs-lookup"><span data-stu-id="f8e6b-149">Building Modules for ARM11 using AC5</span></span>

<span data-ttu-id="f8e6b-150">AC5 kullanarak ARM11 modülü oluşturmaya yönelik basit bir komut satırı örneği:</span><span class="sxs-lookup"><span data-stu-id="f8e6b-150">A simple command-line example for building an ARM11 module using AC5:</span></span>

```dos
armasm -g --cpu ARM1136J-S --apcs /interwork --apcs /ropi --apcs /rwpi txm_module_preamble.s
armcc -g -c -O0 --cpu ARM1136J-S --apcs /interwork --apcs /ropi --apcs /rwpi demo_threadx_module.c
armlink -d -o demo_threadx_module.axf --elf --ro 0 --first txm_module_preamble.o(Init) --entry=_txm_module_thread_shell_entry --ropi --rwpi --remove --map --symbols --list demo_threadx_module.map txm_module_preamble.o demo_threadx_module.o txm.a
```

#### <a name="thread-extension-definition-for-arm11-using-ac5"></a><span data-ttu-id="f8e6b-151">AC5 kullanarak ARM11 için iş parçacığı uzantısı tanımı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-151">Thread extension definition for ARM11 using AC5</span></span>

```c
#define TX_THREAD_EXTENSION_2   VOID    *tx_thread_module_instance_ptr;  \
                                VOID    *tx_thread_module_entry_info_ptr;
```

#### <a name="building-module-manager-for-arm11-using-ac5"></a><span data-ttu-id="f8e6b-152">AC5 kullanarak ARM11 için Modül Yöneticisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="f8e6b-152">Building Module Manager for ARM11 using AC5</span></span>

<span data-ttu-id="f8e6b-153">AC5 kullanarak ARM11 modülü Yöneticisi oluşturmaya yönelik basit bir komut satırı örneği:</span><span class="sxs-lookup"><span data-stu-id="f8e6b-153">A simple command-line example for building an ARM11 module manager using AC5:</span></span>

```dos
armasm -g --cpu ARM1136J-S --apcs /interwork tx_initialize_low_level.s
armcc -g -c -O2 --cpu ARM1136J-S --apcs /interwork demo_threadx_module_manager.c
armcc -g -c -O2 --cpu ARM1136J-S --apcs /interwork module_code.c
armlink -d -o demo_threadx_module_manager.axf --elf --ro 0 --first tx_initialize_low_level.o(Init) --remove --map --symbols --list demo_threadx_module_manager.map tx_initialize_low_level.o demo_threadx_module_manager.o module_code.o tx.a
```

#### <a name="attributes-for-external-memory-enable-api-for-arm11-using-ac5"></a><span data-ttu-id="f8e6b-154">Dış bellek öznitelikleri AC5 kullanarak ARM11 için API 'YI etkinleştirir</span><span class="sxs-lookup"><span data-stu-id="f8e6b-154">Attributes for external memory enable API for ARM11 using AC5</span></span>

<span data-ttu-id="f8e6b-155">Bu özellik bu bağlantı noktasında etkin değil.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-155">This feature not enabled on this port.</span></span>

## <a name="cortex-a7-processor"></a><span data-ttu-id="f8e6b-156">Cortex-A7 işlemcisi</span><span class="sxs-lookup"><span data-stu-id="f8e6b-156">Cortex-A7 processor</span></span>

### <a name="cortex-a7-using-ac5"></a><span data-ttu-id="f8e6b-157">Cortex-AC5 kullanarak A7</span><span class="sxs-lookup"><span data-stu-id="f8e6b-157">Cortex-A7 using AC5</span></span>

#### <a name="module-preamble-for-cortex-a7-using-ac5"></a><span data-ttu-id="f8e6b-158">AC5 kullanarak Cortex için modül girişi-A7</span><span class="sxs-lookup"><span data-stu-id="f8e6b-158">Module preamble for Cortex-A7 using AC5</span></span>

```armasm
    AREA  Init, CODE, READONLY

;    /* Define public symbols.  */

    EXPORT __txm_module_preamble

;    /* Define application-specific start/stop entry points for the module.  */

    IMPORT demo_module_start

;    /* Define common external references.  */

    IMPORT  _txm_module_thread_shell_entry
    IMPORT  _txm_module_callback_request_thread_entry
    IMPORT  |Image$$ER_RO$$Length|
    IMPORT  |Image$$ER_RW$$Length|

__txm_module_preamble
    DCD       0x4D4F4455                                        ; Module ID
    DCD       0x5                                               ; Module Major Version
    DCD       0x3                                               ; Module Minor Version
    DCD       32                                                ; Module Preamble Size in 32-bit words
    DCD       0x12345678                                        ; Module ID (application defined)
    DCD       0x01000001                                        ; Module Properties where:
                                                                ;   Bits 31-24: Compiler ID
                                                                ;           0 -> IAR
                                                                ;           1 -> ARM
                                                                ;           2 -> GNU
                                                                ;   Bits 23-1:  Reserved
                                                                ;   Bit 0:  0 -> Privileged mode execution (no MMU protection)
                                                                ;           1 -> User mode execution (MMU protection)
    DCD       _txm_module_thread_shell_entry - . + .            ; Module Shell Entry Point
    DCD       demo_module_start - . + .                         ; Module Start Thread Entry Point
    DCD       0                                                 ; Module Stop Thread Entry Point
    DCD       1                                                 ; Module Start/Stop Thread Priority
    DCD       1024                                              ; Module Start/Stop Thread Stack Size
    DCD       _txm_module_callback_request_thread_entry - . + . ; Module Callback Thread Entry
    DCD       1                                                 ; Module Callback Thread Priority
    DCD       1024                                              ; Module Callback Thread Stack Size
    DCD       |Image$$ER_RO$$Length| + |Image$$ER_RW$$Length|   ; Module Code Size
    DCD       0x4000                                            ; Module Data Size - default to 16K (need to make sure this is large enough for module's data needs!)
    DCD       0                                                 ; Reserved 0
    DCD       0                                                 ; Reserved 1
    DCD       0                                                 ; Reserved 2
    DCD       0                                                 ; Reserved 3
    DCD       0                                                 ; Reserved 4
    DCD       0                                                 ; Reserved 5
    DCD       0                                                 ; Reserved 6
    DCD       0                                                 ; Reserved 7
    DCD       0                                                 ; Reserved 8
    DCD       0                                                 ; Reserved 9
    DCD       0                                                 ; Reserved 10
    DCD       0                                                 ; Reserved 11
    DCD       0                                                 ; Reserved 12
    DCD       0                                                 ; Reserved 13
    DCD       0                                                 ; Reserved 14
    DCD       0                                                 ; Reserved 15

    END
```

#### <a name="module-properties-for-cortex-a7-using-ac5"></a><span data-ttu-id="f8e6b-159">AC5 kullanarak Cortex-A7 için modül özellikleri</span><span class="sxs-lookup"><span data-stu-id="f8e6b-159">Module properties for Cortex-A7 using AC5</span></span>

| <span data-ttu-id="f8e6b-160">Sürümleri</span><span class="sxs-lookup"><span data-stu-id="f8e6b-160">Bit</span></span> | <span data-ttu-id="f8e6b-161">Değer</span><span class="sxs-lookup"><span data-stu-id="f8e6b-161">Value</span></span> | <span data-ttu-id="f8e6b-162">Anlamı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-162">Meaning</span></span> |
|---|---|---|
| <span data-ttu-id="f8e6b-163">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-163">0</span></span> | <span data-ttu-id="f8e6b-164">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-164">0</span></span><br /><span data-ttu-id="f8e6b-165">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-165">1</span></span> | <span data-ttu-id="f8e6b-166">Ayrıcalıklı mod yürütme</span><span class="sxs-lookup"><span data-stu-id="f8e6b-166">Privileged mode execution</span></span><br /><span data-ttu-id="f8e6b-167">Kullanıcı modu yürütme</span><span class="sxs-lookup"><span data-stu-id="f8e6b-167">User mode execution</span></span> |
| <span data-ttu-id="f8e6b-168">[23-1]</span><span class="sxs-lookup"><span data-stu-id="f8e6b-168">[23-1]</span></span> | <span data-ttu-id="f8e6b-169">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-169">0</span></span> | <span data-ttu-id="f8e6b-170">Ayrılmıştır</span><span class="sxs-lookup"><span data-stu-id="f8e6b-170">Reserved</span></span>
| <span data-ttu-id="f8e6b-171">[31-24]</span><span class="sxs-lookup"><span data-stu-id="f8e6b-171">[31-24]</span></span> | <br /><span data-ttu-id="f8e6b-172">-</span><span class="sxs-lookup"><span data-stu-id="f8e6b-172">0x00</span></span><br /><span data-ttu-id="f8e6b-173">0x01</span><span class="sxs-lookup"><span data-stu-id="f8e6b-173">0x01</span></span><br /><span data-ttu-id="f8e6b-174">0x02</span><span class="sxs-lookup"><span data-stu-id="f8e6b-174">0x02</span></span> | <span data-ttu-id="f8e6b-175">**Derleyici KIMLIĞI**</span><span class="sxs-lookup"><span data-stu-id="f8e6b-175">**Compiler ID**</span></span><br /><span data-ttu-id="f8e6b-176">IAR dili</span><span class="sxs-lookup"><span data-stu-id="f8e6b-176">IAR</span></span><br /><span data-ttu-id="f8e6b-177">ARM</span><span class="sxs-lookup"><span data-stu-id="f8e6b-177">ARM</span></span><br /><span data-ttu-id="f8e6b-178">GNU</span><span class="sxs-lookup"><span data-stu-id="f8e6b-178">GNU</span></span> |

#### <a name="module-linker-for-cortex-a7-using-ac5"></a><span data-ttu-id="f8e6b-179">AC5 kullanarak Cortex için modül Bağlayıcısı-A7</span><span class="sxs-lookup"><span data-stu-id="f8e6b-179">Module linker for Cortex-A7 using AC5</span></span>

<span data-ttu-id="f8e6b-180">Komut satırı üzerine inşa, bağlayıcı dosyası örneği yok.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-180">Built on command-line, no linker file example.</span></span>

#### <a name="building-modules-for-cortex-a7-using-ac5"></a><span data-ttu-id="f8e6b-181">AC5 kullanarak Cortex için modüller oluşturma-A7</span><span class="sxs-lookup"><span data-stu-id="f8e6b-181">Building Modules for Cortex-A7 using AC5</span></span>

<span data-ttu-id="f8e6b-182">AC5 kullanarak Cortex-A7 modülü oluşturmaya yönelik basit bir komut satırı örneği:</span><span class="sxs-lookup"><span data-stu-id="f8e6b-182">A simple command-line example for building a Cortex-A7 module using AC5:</span></span>

```dos
armasm -g --cpu=cortex-a7.no_neon --fpu=softvfp --apcs=/interwork/ropi/rwpi txm_module_preamble.s
armcc  -g --cpu=cortex-a7.no_neon --fpu=softvfp -c --apcs=/interwork/ropi/rwpi --lower_ropi demo_threadx_module.c
armlink -d -o demo_threadx_module.axf --elf --ro 0 --first txm_module_preamble.o(Init) --entry=_txm_module_thread_shell_entry --ropi --rwpi --remove --map --symbols --list demo_threadx_module.map txm_module_preamble.o demo_threadx_module.o txm.a
```

#### <a name="thread-extension-definition-for-cortex-a7-using-ac5"></a><span data-ttu-id="f8e6b-183">AC5 kullanarak Cortex için iş parçacığı uzantısı tanımı A7</span><span class="sxs-lookup"><span data-stu-id="f8e6b-183">Thread extension definition for Cortex-A7 using AC5</span></span>

```c
#define TX_THREAD_EXTENSION_2   ULONG   tx_thread_vfp_enable;                   \
                                VOID    *tx_thread_module_instance_ptr;         \
                                VOID    *tx_thread_module_entry_info_ptr;       \
                                ULONG   tx_thread_module_current_user_mode;     \
                                ULONG   tx_thread_module_user_mode;             \
                                VOID    *tx_thread_module_kernel_stack_start;   \
                                VOID    *tx_thread_module_kernel_stack_end;     \
                                ULONG   tx_thread_module_kernel_stack_size;     \
                                VOID    *tx_thread_module_stack_ptr;            \
                                VOID    *tx_thread_module_stack_start;          \
                                VOID    *tx_thread_module_stack_end;            \
                                ULONG   tx_thread_module_stack_size;            \
                                VOID    *tx_thread_module_reserved;
```

#### <a name="building-module-manager-for-cortex-a7-using-ac5"></a><span data-ttu-id="f8e6b-184">AC5 kullanarak Cortex için Modül Yöneticisi oluşturma-A7</span><span class="sxs-lookup"><span data-stu-id="f8e6b-184">Building Module Manager for Cortex-A7 using AC5</span></span>

<span data-ttu-id="f8e6b-185">AC5 kullanarak Cortex-A7 Module Manager oluşturmaya yönelik basit bir komut satırı örneği:</span><span class="sxs-lookup"><span data-stu-id="f8e6b-185">A simple command-line example for building a Cortex-A7 module manager using AC5:</span></span>

```dos
armasm -g --cpu=cortex-a7.no_neon --fpu=softvfp --apcs=interwork tx_initialize_low_level.s
armcc -g --cpu=cortex-a7.no_neon --fpu=softvfp -c demo_threadx_module_manager.c
armcc -g --cpu=cortex-a7.no_neon --fpu=softvfp -c module_code.c
armlink -d -o demo_threadx_module_manager.axf --elf --ro 0x80000000 --first tx_initialize_low_level.o(VECTORS) --remove --map --symbols --list demo_threadx_module_manager.map tx_initialize_low_level.o demo_threadx_module_manager.o module_code.o tx.a
```

#### <a name="attributes-for-external-memory-enable-api-for-cortex-a7-using-ac5"></a><span data-ttu-id="f8e6b-186">Dış bellek öznitelikleri A7 Cortex için API 'YI etkinleştirir-AC5 kullanarak</span><span class="sxs-lookup"><span data-stu-id="f8e6b-186">Attributes for external memory enable API for Cortex-A7 using AC5</span></span>

<span data-ttu-id="f8e6b-187">Aşağıdaki öznitelikler, paylaşılan bellek ayarlarını ayarlamak için kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="f8e6b-187">The following attributes can be used to set up shared memory settings:</span></span>

| <span data-ttu-id="f8e6b-188">Öznitelik parametresi</span><span class="sxs-lookup"><span data-stu-id="f8e6b-188">Attribute parameter</span></span> | <span data-ttu-id="f8e6b-189">Anlamı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-189">Meaning</span></span> |
|---|---|
| <span data-ttu-id="f8e6b-190">TXM_MMU_ATTRIBUTE_XN</span><span class="sxs-lookup"><span data-stu-id="f8e6b-190">TXM_MMU_ATTRIBUTE_XN</span></span> | <span data-ttu-id="f8e6b-191">Hiçbir şekilde Çalıştır</span><span class="sxs-lookup"><span data-stu-id="f8e6b-191">Execute Never</span></span> |
| <span data-ttu-id="f8e6b-192">TXM_MMU_ATTRIBUTE_B</span><span class="sxs-lookup"><span data-stu-id="f8e6b-192">TXM_MMU_ATTRIBUTE_B</span></span> | <span data-ttu-id="f8e6b-193">B ayarı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-193">B setting</span></span> |
| <span data-ttu-id="f8e6b-194">TXM_MMU_ATTRIBUTE_C</span><span class="sxs-lookup"><span data-stu-id="f8e6b-194">TXM_MMU_ATTRIBUTE_C</span></span> | <span data-ttu-id="f8e6b-195">C ayarı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-195">C setting</span></span> |
| <span data-ttu-id="f8e6b-196">TXM_MMU_ATTRIBUTE_AP</span><span class="sxs-lookup"><span data-stu-id="f8e6b-196">TXM_MMU_ATTRIBUTE_AP</span></span> | <span data-ttu-id="f8e6b-197">AP ayarı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-197">AP setting</span></span> |
| <span data-ttu-id="f8e6b-198">TXM_MMU_ATTRIBUTE_TEX</span><span class="sxs-lookup"><span data-stu-id="f8e6b-198">TXM_MMU_ATTRIBUTE_TEX</span></span> | <span data-ttu-id="f8e6b-199">TEX ayarı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-199">TEX setting</span></span> |

<span data-ttu-id="f8e6b-200">Bu ayarların nasıl yapılandırıldığı hakkında bilgi için bkz. ARM belgeleri.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-200">See ARM documentation for how these settings are configured.</span></span>

## <a name="cortex-m3-processor"></a><span data-ttu-id="f8e6b-201">Cortex-M3 işlemcisi</span><span class="sxs-lookup"><span data-stu-id="f8e6b-201">Cortex-M3 processor</span></span>

### <a name="cortex-m3-using-ac5"></a><span data-ttu-id="f8e6b-202">Cortex-AC5 kullanarak m3</span><span class="sxs-lookup"><span data-stu-id="f8e6b-202">Cortex-M3 using AC5</span></span>

#### <a name="module-preamble-for-cortex-m3-using-ac5"></a><span data-ttu-id="f8e6b-203">AC5 kullanarak Cortex için modül girişi-m3</span><span class="sxs-lookup"><span data-stu-id="f8e6b-203">Module preamble for Cortex-M3 using AC5</span></span>

```armasm
    AREA Init, CODE, READONLY

    PRESERVE8

    ; Define public symbols

    EXPORT __txm_module_preamble

    ; Define application-specific start/stop entry points for the module

    EXTERN demo_module_start

    ; Define common external references

    IMPORT  _txm_module_thread_shell_entry
    IMPORT  _txm_module_callback_request_thread_entry
    IMPORT  |Image$$ER_RO$$Length|
    IMPORT  |Image$$ER_RW$$Length|
    IMPORT  |Image$$ER_RW$$RW$$Length|
    IMPORT  |Image$$ER_RW$$ZI$$Length|
    IMPORT  |Image$$ER_ZI$$ZI$$Length|

__txm_module_preamble
    DCD     0x4D4F4455                                          ; Module ID
    DCD     0x6                                                 ; Module Major Version
    DCD     0x1                                                 ; Module Minor Version
    DCD     32                                                  ; Module Preamble Size in 32-bit words
    DCD     0x12345678                                          ; Module ID (application defined)
    DCD     0x01000007                                          ; Module Properties where:
                                                                ;   Bits 31-24: Compiler ID
                                                                ;           0 -> IAR
                                                                ;           1 -> ARM
                                                                ;           2 -> GNU
                                                                ;   Bit 0:  0 -> Privileged mode execution
                                                                ;           1 -> User mode execution
                                                                ;   Bit 1:  0 -> No MPU protection
                                                                ;           1 -> MPU protection (must have user mode selected)
                                                                ;   Bit 2:  0 -> Disable shared/external memory access
                                                                ;           1 -> Enable shared/external memory access
    DCD     _txm_module_thread_shell_entry - __txm_module_preamble              ; Module Shell Entry Point
    DCD     demo_module_start - __txm_module_preamble           ; Module Start Thread Entry Point
    DCD     0                                                   ; Module Stop Thread Entry Point
    DCD     1                                                   ; Module Start/Stop Thread Priority
    DCD     1024                                                ; Module Start/Stop Thread Stack Size
    DCD     _txm_module_callback_request_thread_entry - __txm_module_preamble   ; Module Callback Thread Entry
    DCD     1                                                   ; Module Callback Thread Priority
    DCD     1024                                                ; Module Callback Thread Stack Size
    DCD     |Image$$ER_RO$$Length| + |Image$$ER_RW$$Length|         ; Module Code Size
    DCD     |Image$$ER_RW$$Length| + |Image$$ER_ZI$$ZI$$Length| ; Module Data Size
    DCD     0                                                   ; Reserved 0
    DCD     0                                                   ; Reserved 1
    DCD     0                                                   ; Reserved 2
    DCD     0                                                   ; Reserved 3
    DCD     0                                                   ; Reserved 4
    DCD     0                                                   ; Reserved 5
    DCD     0                                                   ; Reserved 6
    DCD     0                                                   ; Reserved 7
    DCD     0                                                   ; Reserved 8
    DCD     0                                                   ; Reserved 9
    DCD     0                                                   ; Reserved 10
    DCD     0                                                   ; Reserved 11
    DCD     0                                                   ; Reserved 12
    DCD     0                                                   ; Reserved 13
    DCD     0                                                   ; Reserved 14
    DCD     0                                                   ; Reserved 15

    END

```

#### <a name="module-properties-for-cortex-m3-using-ac5"></a><span data-ttu-id="f8e6b-204">AC5 kullanarak Cortex için modül özellikleri-m3</span><span class="sxs-lookup"><span data-stu-id="f8e6b-204">Module properties for Cortex-M3 using AC5</span></span>

| <span data-ttu-id="f8e6b-205">Sürümleri</span><span class="sxs-lookup"><span data-stu-id="f8e6b-205">Bit</span></span> | <span data-ttu-id="f8e6b-206">Değer</span><span class="sxs-lookup"><span data-stu-id="f8e6b-206">Value</span></span> | <span data-ttu-id="f8e6b-207">Anlamı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-207">Meaning</span></span> |
|---|---|---|
| <span data-ttu-id="f8e6b-208">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-208">0</span></span> | <span data-ttu-id="f8e6b-209">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-209">0</span></span><br /><span data-ttu-id="f8e6b-210">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-210">1</span></span> | <span data-ttu-id="f8e6b-211">Ayrıcalıklı mod yürütme</span><span class="sxs-lookup"><span data-stu-id="f8e6b-211">Privileged mode execution</span></span><br /><span data-ttu-id="f8e6b-212">Kullanıcı modu yürütme</span><span class="sxs-lookup"><span data-stu-id="f8e6b-212">User mode execution</span></span> |
| <span data-ttu-id="f8e6b-213">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-213">1</span></span> | <span data-ttu-id="f8e6b-214">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-214">0</span></span><br /><span data-ttu-id="f8e6b-215">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-215">1</span></span> | <span data-ttu-id="f8e6b-216">MPU koruması yok</span><span class="sxs-lookup"><span data-stu-id="f8e6b-216">No MPU protection</span></span><br /><span data-ttu-id="f8e6b-217">MPU koruması (Kullanıcı modunun seçili olması gerekir)</span><span class="sxs-lookup"><span data-stu-id="f8e6b-217">MPU protection (must have user mode selected)</span></span> |
| <span data-ttu-id="f8e6b-218">2</span><span class="sxs-lookup"><span data-stu-id="f8e6b-218">2</span></span> | <span data-ttu-id="f8e6b-219">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-219">0</span></span><br /><span data-ttu-id="f8e6b-220">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-220">1</span></span> | <span data-ttu-id="f8e6b-221">Paylaşılan/dış bellek erişimini devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="f8e6b-221">Disable shared/external memory access</span></span><br /><span data-ttu-id="f8e6b-222">Paylaşılan/dış bellek erişimini etkinleştir</span><span class="sxs-lookup"><span data-stu-id="f8e6b-222">Enable shared/external memory access</span></span> |
| <span data-ttu-id="f8e6b-223">[23-3]</span><span class="sxs-lookup"><span data-stu-id="f8e6b-223">[23-3]</span></span> | <span data-ttu-id="f8e6b-224">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-224">0</span></span> | <span data-ttu-id="f8e6b-225">Ayrılmıştır</span><span class="sxs-lookup"><span data-stu-id="f8e6b-225">Reserved</span></span>
| <span data-ttu-id="f8e6b-226">[31-24]</span><span class="sxs-lookup"><span data-stu-id="f8e6b-226">[31-24]</span></span> | <br /><span data-ttu-id="f8e6b-227">-</span><span class="sxs-lookup"><span data-stu-id="f8e6b-227">0x00</span></span><br /><span data-ttu-id="f8e6b-228">0x01</span><span class="sxs-lookup"><span data-stu-id="f8e6b-228">0x01</span></span><br /><span data-ttu-id="f8e6b-229">0x02</span><span class="sxs-lookup"><span data-stu-id="f8e6b-229">0x02</span></span> | <span data-ttu-id="f8e6b-230">**Derleyici KIMLIĞI**</span><span class="sxs-lookup"><span data-stu-id="f8e6b-230">**Compiler ID**</span></span><br /><span data-ttu-id="f8e6b-231">IAR dili</span><span class="sxs-lookup"><span data-stu-id="f8e6b-231">IAR</span></span><br /><span data-ttu-id="f8e6b-232">ARM</span><span class="sxs-lookup"><span data-stu-id="f8e6b-232">ARM</span></span><br /><span data-ttu-id="f8e6b-233">GNU</span><span class="sxs-lookup"><span data-stu-id="f8e6b-233">GNU</span></span> |

#### <a name="module-linker-for-cortex-m3-using-ac5"></a><span data-ttu-id="f8e6b-234">AC5 kullanarak Cortex için modül Bağlayıcısı-m3</span><span class="sxs-lookup"><span data-stu-id="f8e6b-234">Module linker for Cortex-M3 using AC5</span></span>

<span data-ttu-id="f8e6b-235">Örnek bağlayıcı dosyası sağlanmaz; bağlantı, komut satırında yapılır.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-235">No example linker file is provided; linking is done on the command line.</span></span> <span data-ttu-id="f8e6b-236">Sonraki bölüme bakın.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-236">See next section.</span></span>

#### <a name="building-modules-for-cortex-m3-using-ac5"></a><span data-ttu-id="f8e6b-237">AC5 kullanarak Cortex için modüller oluşturma-m3</span><span class="sxs-lookup"><span data-stu-id="f8e6b-237">Building Modules for Cortex-M3 using AC5</span></span>

<span data-ttu-id="f8e6b-238">Örnek bir derleme betiği verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="f8e6b-238">An example build script is provided:</span></span>

```dos
armasm -g --cpu=cortex-m3 --apcs=/interwork/ropi/rwpi txm_module_preamble.S
armcc  -g --cpu=cortex-m3 -c --apcs=/interwork/ropi/rwpi --lower_ropi -I../inc -I../../../../common_modules/inc -I../../../../common_modules/module_manager/inc -I../../../../common/inc sample_threadx_module.c
armlink -d -o sample_threadx_module.axf --elf --ro=0x30000 --rw=0x40000 --first txm_module_preamble.o(Init) --entry=_txm_module_thread_shell_entry --ropi --rwpi --remove --map --symbols --list sample_threadx_module.map txm_module_preamble.o sample_threadx_module.o txm.a
```

#### <a name="thread-extension-definition-for-cortex-m3-using-ac5"></a><span data-ttu-id="f8e6b-239">AC5 kullanarak Cortex-M3 için iş parçacığı uzantısı tanımı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-239">Thread extension definition for Cortex-M3 using AC5</span></span>

```c
#define TX_THREAD_EXTENSION_2               VOID    *tx_thread_module_instance_ptr;         \
                                            VOID    *tx_thread_module_entry_info_ptr;       \
                                            ULONG   tx_thread_module_current_user_mode;     \
                                            ULONG   tx_thread_module_user_mode;             \
                                            ULONG   tx_thread_module_saved_lr;              \
                                            VOID    *tx_thread_module_kernel_stack_start;   \
                                            VOID    *tx_thread_module_kernel_stack_end;     \
                                            ULONG   tx_thread_module_kernel_stack_size;     \
                                            VOID    *tx_thread_module_stack_ptr;            \
                                            VOID    *tx_thread_module_stack_start;          \
                                            VOID    *tx_thread_module_stack_end;            \
                                            ULONG   tx_thread_module_stack_size;            \
                                            VOID    *tx_thread_module_reserved;
```

#### <a name="building-module-manager-for-cortex-m3-using-ac5"></a><span data-ttu-id="f8e6b-240">AC5 kullanarak Cortex için Modül Yöneticisi oluşturma-m3</span><span class="sxs-lookup"><span data-stu-id="f8e6b-240">Building Module Manager for Cortex-M3 using AC5</span></span>

<span data-ttu-id="f8e6b-241">Bkz. örnek build_threadx_module_manager_demo.bat:</span><span class="sxs-lookup"><span data-stu-id="f8e6b-241">See example build_threadx_module_manager_demo.bat:</span></span>

```dos
armasm -g --cpu=cortex-m3 --apcs=interwork tx_initialize_low_level.S
armcc -g --cpu=cortex-m3 -c -I../inc -I../../../../common_modules/inc -I../../../../common_modules/module_manager/inc -I../../../../common/inc sample_threadx_module_manager.c
armlink -d -o sample_threadx_module_manager.axf --elf --ro 0x00000000 --first tx_initialize_low_level.o(RESET) --remove --map --symbols --list sample_threadx_module_manager.map tx_initialize_low_level.o sample_threadx_module_manager.o tx.a
```

#### <a name="attributes-for-external-memory-enable-api-for-cortex-m3-using-ac5"></a><span data-ttu-id="f8e6b-242">Dış bellek öznitelikleri AC5 kullanarak Cortex için API 'YI etkinleştirir-m3</span><span class="sxs-lookup"><span data-stu-id="f8e6b-242">Attributes for external memory enable API for Cortex-M3 using AC5</span></span>

<span data-ttu-id="f8e6b-243">Modülün paylaşılan belleğe her zaman okuma erişimi vardır.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-243">Module always has read access to shared memory.</span></span>

| <span data-ttu-id="f8e6b-244">Öznitelik parametresi</span><span class="sxs-lookup"><span data-stu-id="f8e6b-244">Attribute parameter</span></span> | <span data-ttu-id="f8e6b-245">Anlamı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-245">Meaning</span></span> |
|---|---|
| <span data-ttu-id="f8e6b-246">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span><span class="sxs-lookup"><span data-stu-id="f8e6b-246">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span></span> | <span data-ttu-id="f8e6b-247">Yazma erişimi</span><span class="sxs-lookup"><span data-stu-id="f8e6b-247">Write access</span></span> |

### <a name="cortex-m3-using-ac6"></a><span data-ttu-id="f8e6b-248">Cortex-AC6 kullanarak m3</span><span class="sxs-lookup"><span data-stu-id="f8e6b-248">Cortex-M3 using AC6</span></span>

#### <a name="module-preamble-for-cortex-m3-using-ac6"></a><span data-ttu-id="f8e6b-249">AC6 kullanarak Cortex için modül girişi-m3</span><span class="sxs-lookup"><span data-stu-id="f8e6b-249">Module preamble for Cortex-M3 using AC6</span></span>

```armasm
    .text
    .align 4
    .syntax unified
    .section Init
    
    // Define public symbols
    .global __txm_module_preamble

    // Define application-specific start/stop entry points for the module
    .global demo_module_start

    // Define common external references
    .global  _txm_module_thread_shell_entry
    .global  _txm_module_callback_request_thread_entry

    .eabi_attribute Tag_ABI_PCS_RO_data, 1
    .eabi_attribute Tag_ABI_PCS_R9_use,  1
    .eabi_attribute Tag_ABI_PCS_RW_data, 2

__txm_module_preamble:
    .dc.l   0x4D4F4455                                          // Module ID
    .dc.l   0x6                                                 // Module Major Version
    .dc.l   0x1                                                 // Module Minor Version
    .dc.l   32                                                  // Module Preamble Size in 32-bit words
    .dc.l   0x12345678                                          // Module ID (application defined)
    .dc.l   0x01000007                                          // Module Properties where:
                                                                //   Bits 31-24: Compiler ID
                                                                //           0 -> IAR
                                                                //           1 -> ARM
                                                                //           2 -> GNU
                                                                //   Bit 0:  0 -> Privileged mode execution
                                                                //           1 -> User mode execution
                                                                //   Bit 1:  0 -> No MPU protection
                                                                //           1 -> MPU protection (must have user mode selected)
                                                                //   Bit 2:  0 -> Disable shared/external memory access
                                                                //           1 -> Enable shared/external memory access
    .dc.l   _txm_module_thread_shell_entry - __txm_module_preamble // Module Shell Entry Point
    .dc.l   demo_module_start - __txm_module_preamble           // Module Start Thread Entry Point
    .dc.l   0                                                   // Module Stop Thread Entry Point
    .dc.l   1                                                   // Module Start/Stop Thread Priority
    .dc.l   1024                                                // Module Start/Stop Thread Stack Size
    .dc.l   _txm_module_callback_request_thread_entry - __txm_module_preamble // Module Callback Thread Entry
    .dc.l   1                                                   // Module Callback Thread Priority
    .dc.l   1024                                                // Module Callback Thread Stack Size
    .dc.l   0x10000                                             // Module Code Size
    .dc.l   0x10000                                             // Module Data Size
    .dc.l   0                                                   // Reserved 0
    .dc.l   0                                                   // Reserved 1
    .dc.l   0                                                   // Reserved 2
    .dc.l   0                                                   // Reserved 3
    .dc.l   0                                                   // Reserved 4
    .dc.l   0                                                   // Reserved 5
    .dc.l   0                                                   // Reserved 6
    .dc.l   0                                                   // Reserved 7
    .dc.l   0                                                   // Reserved 8
    .dc.l   0                                                   // Reserved 9
    .dc.l   0                                                   // Reserved 10
    .dc.l   0                                                   // Reserved 11
    .dc.l   0                                                   // Reserved 12
    .dc.l   0                                                   // Reserved 13
    .dc.l   0                                                   // Reserved 14
    .dc.l   0                                                   // Reserved 15
```

#### <a name="module-properties-for-cortex-m3-using-ac6"></a><span data-ttu-id="f8e6b-250">AC6 kullanarak Cortex için modül özellikleri-m3</span><span class="sxs-lookup"><span data-stu-id="f8e6b-250">Module properties for Cortex-M3 using AC6</span></span>

| <span data-ttu-id="f8e6b-251">Sürümleri</span><span class="sxs-lookup"><span data-stu-id="f8e6b-251">Bit</span></span> | <span data-ttu-id="f8e6b-252">Değer</span><span class="sxs-lookup"><span data-stu-id="f8e6b-252">Value</span></span> | <span data-ttu-id="f8e6b-253">Anlamı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-253">Meaning</span></span> |
|---|---|---|
| <span data-ttu-id="f8e6b-254">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-254">0</span></span> | <span data-ttu-id="f8e6b-255">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-255">0</span></span><br /><span data-ttu-id="f8e6b-256">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-256">1</span></span> | <span data-ttu-id="f8e6b-257">Ayrıcalıklı mod yürütme</span><span class="sxs-lookup"><span data-stu-id="f8e6b-257">Privileged mode execution</span></span><br /><span data-ttu-id="f8e6b-258">Kullanıcı modu yürütme</span><span class="sxs-lookup"><span data-stu-id="f8e6b-258">User mode execution</span></span> |
| <span data-ttu-id="f8e6b-259">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-259">1</span></span> | <span data-ttu-id="f8e6b-260">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-260">0</span></span><br /><span data-ttu-id="f8e6b-261">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-261">1</span></span> | <span data-ttu-id="f8e6b-262">MPU koruması yok</span><span class="sxs-lookup"><span data-stu-id="f8e6b-262">No MPU protection</span></span><br /><span data-ttu-id="f8e6b-263">MPU koruması (Kullanıcı modunun seçili olması gerekir)</span><span class="sxs-lookup"><span data-stu-id="f8e6b-263">MPU protection (must have user mode selected)</span></span> |
| <span data-ttu-id="f8e6b-264">2</span><span class="sxs-lookup"><span data-stu-id="f8e6b-264">2</span></span> | <span data-ttu-id="f8e6b-265">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-265">0</span></span><br /><span data-ttu-id="f8e6b-266">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-266">1</span></span> | <span data-ttu-id="f8e6b-267">Paylaşılan/dış bellek erişimini devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="f8e6b-267">Disable shared/external memory access</span></span><br /><span data-ttu-id="f8e6b-268">Paylaşılan/dış bellek erişimini etkinleştir</span><span class="sxs-lookup"><span data-stu-id="f8e6b-268">Enable shared/external memory access</span></span> |
| <span data-ttu-id="f8e6b-269">[23-3]</span><span class="sxs-lookup"><span data-stu-id="f8e6b-269">[23-3]</span></span> | <span data-ttu-id="f8e6b-270">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-270">0</span></span> | <span data-ttu-id="f8e6b-271">Ayrılmıştır</span><span class="sxs-lookup"><span data-stu-id="f8e6b-271">Reserved</span></span>
| <span data-ttu-id="f8e6b-272">[31-24]</span><span class="sxs-lookup"><span data-stu-id="f8e6b-272">[31-24]</span></span> | <br /><span data-ttu-id="f8e6b-273">-</span><span class="sxs-lookup"><span data-stu-id="f8e6b-273">0x00</span></span><br /><span data-ttu-id="f8e6b-274">0x01</span><span class="sxs-lookup"><span data-stu-id="f8e6b-274">0x01</span></span><br /><span data-ttu-id="f8e6b-275">0x02</span><span class="sxs-lookup"><span data-stu-id="f8e6b-275">0x02</span></span> | <span data-ttu-id="f8e6b-276">**Derleyici KIMLIĞI**</span><span class="sxs-lookup"><span data-stu-id="f8e6b-276">**Compiler ID**</span></span><br /><span data-ttu-id="f8e6b-277">IAR dili</span><span class="sxs-lookup"><span data-stu-id="f8e6b-277">IAR</span></span><br /><span data-ttu-id="f8e6b-278">ARM</span><span class="sxs-lookup"><span data-stu-id="f8e6b-278">ARM</span></span><br /><span data-ttu-id="f8e6b-279">GNU</span><span class="sxs-lookup"><span data-stu-id="f8e6b-279">GNU</span></span> |

#### <a name="module-linker-for-cortex-m3-using-ac6"></a><span data-ttu-id="f8e6b-280">AC6 kullanarak Cortex için modül Bağlayıcısı-m3</span><span class="sxs-lookup"><span data-stu-id="f8e6b-280">Module linker for Cortex-M3 using AC6</span></span>

<span data-ttu-id="f8e6b-281">Bağlayıcı dosyası kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-281">No linker file is used.</span></span> <span data-ttu-id="f8e6b-282">Bkz. proje ayarları.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-282">See project settings.</span></span>

#### <a name="building-modules-for-cortex-m3-using-ac6"></a><span data-ttu-id="f8e6b-283">AC6 kullanarak Cortex için modüller oluşturma-m3</span><span class="sxs-lookup"><span data-stu-id="f8e6b-283">Building Modules for Cortex-M3 using AC6</span></span>

<span data-ttu-id="f8e6b-284">Örnek çalışma alanı sağlanır.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-284">An example workspace is provided.</span></span> <span data-ttu-id="f8e6b-285">ThreadX kitaplığı, ThreadX modülleri kitaplığı, örnek Modül projesi ve örnek Module Manager projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-285">Build the ThreadX library, ThreadX Modules library, sample module project, and sample module manager project.</span></span>

#### <a name="thread-extension-definition-for-cortex-m3-using-ac6"></a><span data-ttu-id="f8e6b-286">AC6 kullanarak Cortex-M3 için iş parçacığı uzantısı tanımı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-286">Thread extension definition for Cortex-M3 using AC6</span></span>

```c
#define TX_THREAD_EXTENSION_2               VOID    *tx_thread_module_instance_ptr;         \
                                            VOID    *tx_thread_module_entry_info_ptr;       \
                                            ULONG   tx_thread_module_current_user_mode;     \
                                            ULONG   tx_thread_module_user_mode;             \
                                            ULONG   tx_thread_module_saved_lr;              \
                                            VOID    *tx_thread_module_kernel_stack_start;   \
                                            VOID    *tx_thread_module_kernel_stack_end;     \
                                            ULONG   tx_thread_module_kernel_stack_size;     \
                                            VOID    *tx_thread_module_stack_ptr;            \
                                            VOID    *tx_thread_module_stack_start;          \
                                            VOID    *tx_thread_module_stack_end;            \
                                            ULONG   tx_thread_module_stack_size;            \
                                            VOID    *tx_thread_module_reserved;
```

#### <a name="building-module-manager-for-cortex-m3-using-ac6"></a><span data-ttu-id="f8e6b-287">AC6 kullanarak Cortex için Modül Yöneticisi oluşturma-m3</span><span class="sxs-lookup"><span data-stu-id="f8e6b-287">Building Module Manager for Cortex-M3 using AC6</span></span>

<span data-ttu-id="f8e6b-288">Örnek çalışma alanı sağlanır.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-288">An example workspace is provided.</span></span> <span data-ttu-id="f8e6b-289">ThreadX kitaplığı, ThreadX modülleri kitaplığı, örnek Modül projesi ve örnek Module Manager projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-289">Build the ThreadX library, ThreadX Modules library, sample module project, and sample module manager project.</span></span>

#### <a name="attributes-for-external-memory-enable-api-for-cortex-m3-using-ac6"></a><span data-ttu-id="f8e6b-290">Dış bellek öznitelikleri AC6 kullanarak Cortex için API 'YI etkinleştirir-m3</span><span class="sxs-lookup"><span data-stu-id="f8e6b-290">Attributes for external memory enable API for Cortex-M3 using AC6</span></span>

<span data-ttu-id="f8e6b-291">Modülün paylaşılan belleğe her zaman okuma erişimi vardır.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-291">Module always has read access to shared memory.</span></span>

| <span data-ttu-id="f8e6b-292">Öznitelik parametresi</span><span class="sxs-lookup"><span data-stu-id="f8e6b-292">Attribute parameter</span></span> | <span data-ttu-id="f8e6b-293">Anlamı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-293">Meaning</span></span> |
|---|---|
| <span data-ttu-id="f8e6b-294">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span><span class="sxs-lookup"><span data-stu-id="f8e6b-294">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span></span> | <span data-ttu-id="f8e6b-295">Yazma erişimi</span><span class="sxs-lookup"><span data-stu-id="f8e6b-295">Write access</span></span> |

### <a name="cortex-m3-using-gnu"></a><span data-ttu-id="f8e6b-296">Cortex-GNU kullanan m3</span><span class="sxs-lookup"><span data-stu-id="f8e6b-296">Cortex-M3 using GNU</span></span>

#### <a name="module-preamble-for-cortex-m3-using-gnu"></a><span data-ttu-id="f8e6b-297">GNU kullanarak Cortex için modül girişi-m3</span><span class="sxs-lookup"><span data-stu-id="f8e6b-297">Module preamble for Cortex-M3 using GNU</span></span>

```armasm
    .text
    .align 4
    .syntax unified

    /* Define public symbols.  */
    .global __txm_module_preamble

    /* Define application-specific start/stop entry points for the module.  */
    .global demo_module_start

    /* Define common external refrences.  */
    .global _txm_module_thread_shell_entry
    .global _txm_module_callback_request_thread_entry

__txm_module_preamble:
    .dc.l      0x4D4F4455                                       // Module ID
    .dc.l      0x6                                              // Module Major Version
    .dc.l      0x1                                              // Module Minor Version
    .dc.l      32                                               // Module Preamble Size in 32-bit words
    .dc.l      0x12345678                                       // Module ID (application defined)
    .dc.l      0x02000007                                       // Module Properties where:
                                                                //   Bits 31-24: Compiler ID
                                                                //           0 -> IAR
                                                                //           1 -> ARM
                                                                //           2 -> GNU
                                                                //   Bits 23-3: Reserved
                                                                //   Bit 2:  0 -> Disable shared/external memory access
                                                                //           1 -> Enable shared/external memory access
                                                                //   Bit 1:  0 -> No MPU protection
                                                                //           1 -> MPU protection (must have user mode selected - bit 0 set)
                                                                //   Bit 0:  0 -> Privileged mode execution
                                                                //           1 -> User mode execution
    .dc.l      _txm_module_thread_shell_entry - . - 0           // Module Shell Entry Point
    .dc.l      demo_module_start - . - 0                        // Module Start Thread Entry Point
    .dc.l      0                                                // Module Stop Thread Entry Point 
    .dc.l      1                                                // Module Start/Stop Thread Priority
    .dc.l      1024                                             // Module Start/Stop Thread Stack Size
    .dc.l      _txm_module_callback_request_thread_entry - . - 0 // Module Callback Thread Entry
    .dc.l      1                                                // Module Callback Thread Priority
    .dc.l      1024                                             // Module Callback Thread Stack Size
    .dc.l      __code_size__                                    // Module Code Size
    .dc.l      __data_size__                                    // Module Data Size
    .dc.l      0                                                // Reserved 0
    .dc.l      0                                                // Reserved 1
    .dc.l      0                                                // Reserved 2
    .dc.l      0                                                // Reserved 3
    .dc.l      0                                                // Reserved 4
    .dc.l      0                                                // Reserved 5
    .dc.l      0                                                // Reserved 6
    .dc.l      0                                                // Reserved 7
    .dc.l      0                                                // Reserved 8
    .dc.l      0                                                // Reserved 9
    .dc.l      0                                                // Reserved 10
    .dc.l      0                                                // Reserved 11
    .dc.l      0                                                // Reserved 12
    .dc.l      0                                                // Reserved 13
    .dc.l      0                                                // Reserved 14
    .dc.l      0                                                // Reserved 15

```

#### <a name="module-properties-for-cortex-m3-using-gnu"></a><span data-ttu-id="f8e6b-298">GNU kullanarak Cortex için modül özellikleri-m3</span><span class="sxs-lookup"><span data-stu-id="f8e6b-298">Module properties for Cortex-M3 using GNU</span></span>

| <span data-ttu-id="f8e6b-299">Sürümleri</span><span class="sxs-lookup"><span data-stu-id="f8e6b-299">Bit</span></span> | <span data-ttu-id="f8e6b-300">Değer</span><span class="sxs-lookup"><span data-stu-id="f8e6b-300">Value</span></span> | <span data-ttu-id="f8e6b-301">Anlamı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-301">Meaning</span></span> |
|---|---|---|
| <span data-ttu-id="f8e6b-302">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-302">0</span></span> | <span data-ttu-id="f8e6b-303">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-303">0</span></span><br /><span data-ttu-id="f8e6b-304">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-304">1</span></span> | <span data-ttu-id="f8e6b-305">Ayrıcalıklı mod yürütme</span><span class="sxs-lookup"><span data-stu-id="f8e6b-305">Privileged mode execution</span></span><br /><span data-ttu-id="f8e6b-306">Kullanıcı modu yürütme</span><span class="sxs-lookup"><span data-stu-id="f8e6b-306">User mode execution</span></span> |
| <span data-ttu-id="f8e6b-307">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-307">1</span></span> | <span data-ttu-id="f8e6b-308">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-308">0</span></span><br /><span data-ttu-id="f8e6b-309">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-309">1</span></span> | <span data-ttu-id="f8e6b-310">MPU koruması yok</span><span class="sxs-lookup"><span data-stu-id="f8e6b-310">No MPU protection</span></span><br /><span data-ttu-id="f8e6b-311">MPU koruması (Kullanıcı modunun seçili olması gerekir)</span><span class="sxs-lookup"><span data-stu-id="f8e6b-311">MPU protection (must have user mode selected)</span></span> |
| <span data-ttu-id="f8e6b-312">2</span><span class="sxs-lookup"><span data-stu-id="f8e6b-312">2</span></span> | <span data-ttu-id="f8e6b-313">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-313">0</span></span><br /><span data-ttu-id="f8e6b-314">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-314">1</span></span> | <span data-ttu-id="f8e6b-315">Paylaşılan/dış bellek erişimini devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="f8e6b-315">Disable shared/external memory access</span></span><br /><span data-ttu-id="f8e6b-316">Paylaşılan/dış bellek erişimini etkinleştir</span><span class="sxs-lookup"><span data-stu-id="f8e6b-316">Enable shared/external memory access</span></span> |
| <span data-ttu-id="f8e6b-317">[23-3]</span><span class="sxs-lookup"><span data-stu-id="f8e6b-317">[23-3]</span></span> | <span data-ttu-id="f8e6b-318">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-318">0</span></span> | <span data-ttu-id="f8e6b-319">Ayrılmıştır</span><span class="sxs-lookup"><span data-stu-id="f8e6b-319">Reserved</span></span>
| <span data-ttu-id="f8e6b-320">[31-24]</span><span class="sxs-lookup"><span data-stu-id="f8e6b-320">[31-24]</span></span> | <br /><span data-ttu-id="f8e6b-321">-</span><span class="sxs-lookup"><span data-stu-id="f8e6b-321">0x00</span></span><br /><span data-ttu-id="f8e6b-322">0x01</span><span class="sxs-lookup"><span data-stu-id="f8e6b-322">0x01</span></span><br /><span data-ttu-id="f8e6b-323">0x02</span><span class="sxs-lookup"><span data-stu-id="f8e6b-323">0x02</span></span> | <span data-ttu-id="f8e6b-324">**Derleyici KIMLIĞI**</span><span class="sxs-lookup"><span data-stu-id="f8e6b-324">**Compiler ID**</span></span><br /><span data-ttu-id="f8e6b-325">IAR dili</span><span class="sxs-lookup"><span data-stu-id="f8e6b-325">IAR</span></span><br /><span data-ttu-id="f8e6b-326">ARM</span><span class="sxs-lookup"><span data-stu-id="f8e6b-326">ARM</span></span><br /><span data-ttu-id="f8e6b-327">GNU</span><span class="sxs-lookup"><span data-stu-id="f8e6b-327">GNU</span></span> |

#### <a name="module-linker-for-cortex-m3-using-gnu"></a><span data-ttu-id="f8e6b-328">GNU kullanarak Cortex için modül Bağlayıcısı-m3</span><span class="sxs-lookup"><span data-stu-id="f8e6b-328">Module linker for Cortex-M3 using GNU</span></span>

```c
MEMORY
{
  FLASH (rx) : ORIGIN = 0x00030000, LENGTH = 0x00010000
  RAM   (wx) : ORIGIN = 0, LENGTH = 0x00100000
}


SECTIONS
{
  __FLASH_segment_start__ = 0x00030000;
  __FLASH_segment_end__   = 0x00040000;
  __RAM_segment_start__   = 0;
  __RAM_segment_end__     = 0x8000;

  __HEAPSIZE__ = 128;

  __preamble_load_start__ = __FLASH_segment_start__;
  .preamble __FLASH_segment_start__ : AT(__FLASH_segment_start__)
  {
    __preamble_start__ = .;
    *(.preamble .preamble.*)
  }
  __preamble_end__ = __preamble_start__ + SIZEOF(.preamble);

  __dynsym_load_start__ =  ALIGN(__preamble_end__ , 4);
  .dynsym ALIGN(__dynsym_load_start__ , 4) : AT(ALIGN(__dynsym_load_start__ , 4))
  {
    . = ALIGN(4);
    KEEP (*(.dynsym))
    KEEP (*(.dynsym*))
    . = ALIGN(4);
  }
  __dynsym_end__ = __dynsym_load_start__ + SIZEOF(.dynsym);

  __dynstr_load_start__ =  ALIGN(__dynsym_end__ , 4);
  .dynstr ALIGN(__dynstr_load_start__ , 4) : AT(ALIGN(__dynstr_load_start__, 4))
  {
    . = ALIGN(4);
    KEEP (*(.dynstr))
    KEEP (*(.dynstr*))
    . = ALIGN(4);
  }
  __dynstr_end__ = __dynstr_load_start__ + SIZEOF(.dynstr);

  __reldyn_load_start__ =  ALIGN(__dynstr_end__ , 4);
  .rel.dyn ALIGN(__reldyn_load_start__ , 4) : AT(ALIGN(__reldyn_load_start__ , 4))
  {
    . = ALIGN(4);
    KEEP (*(.rel.dyn))
    KEEP (*(.rel.dyn*))
    . = ALIGN(4);
  }
  __reldyn_end__ = __reldyn_load_start__ + SIZEOF(.rel.dyn);

  __relplt_load_start__ =  ALIGN(__reldyn_end__ , 4);
  .rel.plt ALIGN(__relplt_load_start__ , 4) : AT(ALIGN(__relplt_load_start__ , 4))
  {
    . = ALIGN(4);
    KEEP (*(.rel.plt))
    KEEP (*(.rel.plt*))
    . = ALIGN(4);
  }
  __relplt_end__ = __relplt_load_start__ + SIZEOF(.rel.plt);

  __plt_load_start__ =  ALIGN(__relplt_end__ , 4);
  .plt ALIGN(__plt_load_start__ , 4) : AT(ALIGN(__plt_load_start__ , 4))
  {
    . = ALIGN(4);
    KEEP (*(.plt))
    KEEP (*(.plt*))
    . = ALIGN(4);
  }
  __plt_end__ = __plt_load_start__ + SIZEOF(.plt);

  __interp_load_start__ =  ALIGN(__plt_end__ , 4);
  .interp ALIGN(__interp_load_start__ , 4) : AT(ALIGN(__interp_load_start__ , 4))
  {
    . = ALIGN(4);
    KEEP (*(.interp))
    KEEP (*(.interp*))
    . = ALIGN(4);
  }
  __interp_end__ = __interp_load_start__ + SIZEOF(.interp);

  __hash_load_start__ =  ALIGN(__interp_end__ , 4);
  .hash ALIGN(__hash_load_start__ , 4) : AT(ALIGN(__hash_load_start__, 4))
  {
    . = ALIGN(4);
    KEEP (*(.hash))
    KEEP (*(.hash*))
    . = ALIGN(4);
  }
  __hash_end__ = __hash_load_start__ + SIZEOF(.hash);

  __text_load_start__ =  ALIGN(__hash_end__ , 4);
  .text ALIGN(__text_load_start__ , 4) : AT(ALIGN(__text_load_start__, 4))
  {
    __text_start__ = .;
    *(.text .text.* .glue_7t .glue_7 .gnu.linkonce.t.* .gcc_except_table  )
  }
  __text_end__ = __text_start__ + SIZEOF(.text);

  __dtors_load_start__ = ALIGN(__text_end__ , 4);
  .dtors ALIGN(__text_end__ , 4) : AT(ALIGN(__text_end__ , 4))
  {
    __dtors_start__ = .;
    KEEP (*(SORT(.dtors.*))) KEEP (*(.dtors))
  }
  __dtors_end__ = __dtors_start__ + SIZEOF(.dtors);

  __ctors_load_start__ = ALIGN(__dtors_end__ , 4);
  .ctors ALIGN(__dtors_end__ , 4) : AT(ALIGN(__dtors_end__ , 4))
  {
    __ctors_start__ = .;
    KEEP (*(SORT(.ctors.*))) KEEP (*(.ctors))
  }
  __ctors_end__ = __ctors_start__ + SIZEOF(.ctors);

  __got_load_start__ = ALIGN(__ctors_end__ , 4);
  .got ALIGN(__ctors_end__ , 4) : AT(ALIGN(__ctors_end__ , 4))
  {
    . = ALIGN(4);
    _sgot = .;
    KEEP (*(.got))
    KEEP (*(.got*))
    . = ALIGN(4);
    _egot = .;
  } 
  __got_end__ =  __got_load_start__ + SIZEOF(.got);

  __rodata_load_start__ = ALIGN(__got_end__ , 4);
  .rodata ALIGN(__got_end__ , 4) : AT(ALIGN(__got_end__ , 4))
  {
    __rodata_start__ = .;
    *(.rodata .rodata.* .gnu.linkonce.r.*)
  }
  __rodata_end__ = __rodata_start__ + SIZEOF(.rodata);
 
  __code_size__ =  __rodata_end__ - __FLASH_segment_start__;

  __fast_load_start__ = ALIGN(__rodata_end__ , 4);

  __fast_load_end__ = __fast_load_start__ + SIZEOF(.fast);

  __new_got_start__ = ALIGN(__RAM_segment_start__ , 4);

  __new_got_end__ =  __new_got_start__ + SIZEOF(.got);

  .fast ALIGN(__new_got_end__ , 4) : AT(ALIGN(__rodata_end__ , 4))
  {
    __fast_start__ = .;
    *(.fast .fast.*)
  }
  __fast_end__ = __fast_start__ + SIZEOF(.fast);

  .fast_run ALIGN(__fast_end__ , 4) (NOLOAD) :
  {
    __fast_run_start__ = .;
    . = MAX(__fast_run_start__ + SIZEOF(.fast), .);
  }
  __fast_run_end__ = __fast_run_start__ + SIZEOF(.fast_run);

  __data_load_start__ = ALIGN(__fast_load_start__ + SIZEOF(.fast) , 4);
  .data ALIGN(__fast_run_end__ , 4) : AT(ALIGN(__fast_load_start__ + SIZEOF(.fast) , 4))
  {
    __data_start__ = .;
    *(.data .data.* .gnu.linkonce.d.*)
  }
  __data_end__ = __data_start__ + SIZEOF(.data);

  __data_load_end__ = __data_load_start__ + SIZEOF(.data);

  __FLASH_segment_used_end__ = ALIGN(__fast_load_start__ + SIZEOF(.fast) , 4) + SIZEOF(.data);

  .data_run ALIGN(__fast_run_end__ , 4) (NOLOAD) :
  {
    __data_run_start__ = .;
    . = MAX(__data_run_start__ + SIZEOF(.data), .);
  }
  __data_run_end__ = __data_run_start__ + SIZEOF(.data_run);

  __bss_load_start__ = ALIGN(__data_run_end__ , 4);
  .bss ALIGN(__data_run_end__ , 4) (NOLOAD) : AT(ALIGN(__data_run_end__ , 4))
  {
    __bss_start__ = .;
    *(.bss .bss.* .gnu.linkonce.b.*) *(COMMON)
  }
  __bss_end__ = __bss_start__ + SIZEOF(.bss);

  __non_init_load_start__ = ALIGN(__bss_end__ , 4);
  .non_init ALIGN(__bss_end__ , 4) (NOLOAD) : AT(ALIGN(__bss_end__ , 4))
  {
    __non_init_start__ = .;
    *(.non_init .non_init.*)
  }
  __non_init_end__ = __non_init_start__ + SIZEOF(.non_init);

  __heap_load_start__ = ALIGN(__non_init_end__ , 4);
  .heap ALIGN(__non_init_end__ , 4) (NOLOAD) : AT(ALIGN(__non_init_end__ , 4))
  {
    __heap_start__ = .;
    *(.heap)
    . = ALIGN(MAX(__heap_start__ + __HEAPSIZE__ , .), 4);
  }
  __heap_end__ = __heap_start__ + SIZEOF(.heap);

  __data_size__ =  __heap_end__ - __RAM_segment_start__;

}
```

#### <a name="building-modules-for-cortex-m3-using-gnu"></a><span data-ttu-id="f8e6b-329">GNU kullanarak Cortex için modüller oluşturma-m3</span><span class="sxs-lookup"><span data-stu-id="f8e6b-329">Building Modules for Cortex-M3 using GNU</span></span>

<span data-ttu-id="f8e6b-330">build_threadx_module_sample.bat bkz:</span><span class="sxs-lookup"><span data-stu-id="f8e6b-330">See build_threadx_module_sample.bat:</span></span>

```dos
arm-none-eabi-gcc -c -g -mcpu=cortex-m3 -fpie -fno-plt -mpic-data-is-text-relative -msingle-pic-base txm_module_preamble.s
arm-none-eabi-gcc -c -g -mcpu=cortex-m3 -fpie -fno-plt -mpic-data-is-text-relative -msingle-pic-base gcc_setup.S
arm-none-eabi-gcc -c -g -mcpu=cortex-m3 -fpie -fno-plt -mpic-data-is-text-relative -msingle-pic-base -I..\inc -I..\..\..\..\common\inc -I..\..\..\..\common_modules\inc sample_threadx_module.c
arm-none-eabi-ld -A cortex-m3 -T sample_threadx_module.ld txm_module_preamble.o gcc_setup.o sample_threadx_module.o -e _txm_module_thread_shell_entry txm.a -o sample_threadx_module.axf -M > sample_threadx_module.map
```

#### <a name="thread-extension-definition-for-cortex-m3-using-gnu"></a><span data-ttu-id="f8e6b-331">GNU kullanan Cortex için iş parçacığı uzantısı tanımı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-331">Thread extension definition for Cortex-M3 using GNU</span></span>

```c
#define TX_THREAD_EXTENSION_2               VOID    *tx_thread_module_instance_ptr;         \
                                            VOID    *tx_thread_module_entry_info_ptr;       \
                                            ULONG   tx_thread_module_current_user_mode;     \
                                            ULONG   tx_thread_module_user_mode;             \
                                            ULONG   tx_thread_module_saved_lr;              \
                                            VOID    *tx_thread_module_kernel_stack_start;   \
                                            VOID    *tx_thread_module_kernel_stack_end;     \
                                            ULONG   tx_thread_module_kernel_stack_size;     \
                                            VOID    *tx_thread_module_stack_ptr;            \
                                            VOID    *tx_thread_module_stack_start;          \
                                            VOID    *tx_thread_module_stack_end;            \
                                            ULONG   tx_thread_module_stack_size;            \
                                            VOID    *tx_thread_module_reserved;
```

#### <a name="building-module-manager-for-cortex-m3-using-gnu"></a><span data-ttu-id="f8e6b-332">GNU kullanarak Cortex için Modül Yöneticisi oluşturma-m3</span><span class="sxs-lookup"><span data-stu-id="f8e6b-332">Building Module Manager for Cortex-M3 using GNU</span></span>

<span data-ttu-id="f8e6b-333">build_threadx_module_manager_sample.bat bkz:</span><span class="sxs-lookup"><span data-stu-id="f8e6b-333">See build_threadx_module_manager_sample.bat:</span></span>

```dos
arm-none-eabi-gcc -c -g -mcpu=cortex-m3 -mthumb -I..\inc -I..\..\..\..\common\inc -I..\..\..\..\common_modules\inc sample_threadx_module_manager.c
arm-none-eabi-gcc -c -g -mcpu=cortex-m3 -mthumb tx_simulator_startup.S
arm-none-eabi-gcc -c -g -mcpu=cortex-m3 -mthumb cortexm_crt0.S
arm-none-eabi-ld -A cortex-m3 -ereset_handler -T sample_threadx.ld tx_simulator_startup.o cortexm_crt0.o sample_threadx_module_manager.o tx.a  libc.a -o sample_threadx_module_manager.axf -M > sample_threadx_module_manager.map
```

#### <a name="attributes-for-external-memory-enable-api-for-cortex-m3-using-gnu"></a><span data-ttu-id="f8e6b-334">Dış bellek öznitelikleri, GNU kullanarak Cortex için API 'YI etkinleştirir-m3</span><span class="sxs-lookup"><span data-stu-id="f8e6b-334">Attributes for external memory enable API for Cortex-M3 using GNU</span></span>

<span data-ttu-id="f8e6b-335">Modülün paylaşılan belleğe her zaman okuma erişimi vardır.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-335">Module always has read access to shared memory.</span></span>

| <span data-ttu-id="f8e6b-336">Öznitelik parametresi</span><span class="sxs-lookup"><span data-stu-id="f8e6b-336">Attribute parameter</span></span> | <span data-ttu-id="f8e6b-337">Anlamı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-337">Meaning</span></span> |
|---|---|
| <span data-ttu-id="f8e6b-338">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span><span class="sxs-lookup"><span data-stu-id="f8e6b-338">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span></span> | <span data-ttu-id="f8e6b-339">Yazma erişimi</span><span class="sxs-lookup"><span data-stu-id="f8e6b-339">Write access</span></span> |

### <a name="cortex-m3-using-iar"></a><span data-ttu-id="f8e6b-340">Cortex-ıAR kullanan m3</span><span class="sxs-lookup"><span data-stu-id="f8e6b-340">Cortex-M3 using IAR</span></span>

#### <a name="module-preamble-for-cortex-m3-using-iar"></a><span data-ttu-id="f8e6b-341">IAR kullanarak Cortex için modül girişi-m3</span><span class="sxs-lookup"><span data-stu-id="f8e6b-341">Module preamble for Cortex-M3 using IAR</span></span>

```c
    SECTION .text:CODE

    AAPCS INTERWORK, ROPI, RWPI_COMPATIBLE,  VFP_COMPATIBLE
    PRESERVE8

    /* Define public symbols.  */

    PUBLIC __txm_module_preamble


    /* Define application-specific start/stop entry points for the module.  */

    EXTERN demo_module_start


    /* Define common external references.  */

    EXTERN  _txm_module_thread_shell_entry
    EXTERN  _txm_module_callback_request_thread_entry
    EXTERN  ROPI$$Length
    EXTERN  RWPI$$Length

    DATA
__txm_module_preamble:
    DC32      0x4D4F4455                                        ; Module ID
    DC32      0x5                                               ; Module Major Version
    DC32      0x6                                               ; Module Minor Version
    DC32      32                                                ; Module Preamble Size in 32-bit words
    DC32      0x12345678                                        ; Module ID (application defined)
    DC32      0x00000007                                        ; Module Properties where:
                                                                ;   Bits 31-24: Compiler ID
                                                                ;           0 -> IAR
                                                                ;           1 -> ARM
                                                                ;           2 -> GNU
                                                                ;   Bits 23-3: Reserved
                                                                ;   Bit 2:  0 -> Disable shared/external memory access
                                                                ;           1 -> Enable shared/external memory access
                                                                ;   Bit 1:  0 -> No MPU protection
                                                                ;           1 -> MPU protection (must have user mode selected - bit 0 set)
                                                                ;   Bit 0:  0 -> Privileged mode execution
                                                                ;           1 -> User mode execution


    DC32      _txm_module_thread_shell_entry - . - 0            ; Module Shell Entry Point
    DC32      demo_module_start - . - 0                         ; Module Start Thread Entry Point
    DC32      0                                                 ; Module Stop Thread Entry Point
    DC32      1                                                 ; Module Start/Stop Thread Priority
    DC32      1024                                              ; Module Start/Stop Thread Stack Size
    DC32      _txm_module_callback_request_thread_entry - . - 0 ; Module Callback Thread Entry
    DC32      1                                                 ; Module Callback Thread Priority
    DC32      1024                                              ; Module Callback Thread Stack Size
    DC32      ROPI$$Length                                      ; Module Code Size
    DC32      RWPI$$Length                                      ; Module Data Size
    DC32      0                                                 ; Reserved 0
    DC32      0                                                 ; Reserved 1
    DC32      0                                                 ; Reserved 2
    DC32      0                                                 ; Reserved 3
    DC32      0                                                 ; Reserved 4
    DC32      0                                                 ; Reserved 5
    DC32      0                                                 ; Reserved 6
    DC32      0                                                 ; Reserved 7
    DC32      0                                                 ; Reserved 8  
    DC32      0                                                 ; Reserved 9
    DC32      0                                                 ; Reserved 10
    DC32      0                                                 ; Reserved 11
    DC32      0                                                 ; Reserved 12
    DC32      0                                                 ; Reserved 13
    DC32      0                                                 ; Reserved 14
    DC32      0                                                 ; Reserved 15

    END
```

#### <a name="module-properties-for-cortex-m3-using-iar"></a><span data-ttu-id="f8e6b-342">Cortex için modül özellikleri-ıAR kullanılarak m3</span><span class="sxs-lookup"><span data-stu-id="f8e6b-342">Module properties for Cortex-M3 using IAR</span></span>

| <span data-ttu-id="f8e6b-343">Sürümleri</span><span class="sxs-lookup"><span data-stu-id="f8e6b-343">Bit</span></span> | <span data-ttu-id="f8e6b-344">Değer</span><span class="sxs-lookup"><span data-stu-id="f8e6b-344">Value</span></span> | <span data-ttu-id="f8e6b-345">Anlamı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-345">Meaning</span></span> |
|---|---|---|
| <span data-ttu-id="f8e6b-346">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-346">0</span></span> | <span data-ttu-id="f8e6b-347">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-347">0</span></span><br /><span data-ttu-id="f8e6b-348">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-348">1</span></span> | <span data-ttu-id="f8e6b-349">Ayrıcalıklı mod yürütme</span><span class="sxs-lookup"><span data-stu-id="f8e6b-349">Privileged mode execution</span></span><br /><span data-ttu-id="f8e6b-350">Kullanıcı modu yürütme</span><span class="sxs-lookup"><span data-stu-id="f8e6b-350">User mode execution</span></span> |
| <span data-ttu-id="f8e6b-351">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-351">1</span></span> | <span data-ttu-id="f8e6b-352">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-352">0</span></span><br /><span data-ttu-id="f8e6b-353">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-353">1</span></span> | <span data-ttu-id="f8e6b-354">MPU koruması yok</span><span class="sxs-lookup"><span data-stu-id="f8e6b-354">No MPU protection</span></span><br /><span data-ttu-id="f8e6b-355">MPU koruması (Kullanıcı modunun seçili olması gerekir)</span><span class="sxs-lookup"><span data-stu-id="f8e6b-355">MPU protection (must have user mode selected)</span></span> |
| <span data-ttu-id="f8e6b-356">2</span><span class="sxs-lookup"><span data-stu-id="f8e6b-356">2</span></span> | <span data-ttu-id="f8e6b-357">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-357">0</span></span><br /><span data-ttu-id="f8e6b-358">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-358">1</span></span> | <span data-ttu-id="f8e6b-359">Paylaşılan/dış bellek erişimini devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="f8e6b-359">Disable shared/external memory access</span></span><br /><span data-ttu-id="f8e6b-360">Paylaşılan/dış bellek erişimini etkinleştir</span><span class="sxs-lookup"><span data-stu-id="f8e6b-360">Enable shared/external memory access</span></span> |
| <span data-ttu-id="f8e6b-361">[23-3]</span><span class="sxs-lookup"><span data-stu-id="f8e6b-361">[23-3]</span></span> | <span data-ttu-id="f8e6b-362">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-362">0</span></span> | <span data-ttu-id="f8e6b-363">Ayrılmıştır</span><span class="sxs-lookup"><span data-stu-id="f8e6b-363">Reserved</span></span>
| <span data-ttu-id="f8e6b-364">[31-24]</span><span class="sxs-lookup"><span data-stu-id="f8e6b-364">[31-24]</span></span> | <br /><span data-ttu-id="f8e6b-365">-</span><span class="sxs-lookup"><span data-stu-id="f8e6b-365">0x00</span></span><br /><span data-ttu-id="f8e6b-366">0x01</span><span class="sxs-lookup"><span data-stu-id="f8e6b-366">0x01</span></span><br /><span data-ttu-id="f8e6b-367">0x02</span><span class="sxs-lookup"><span data-stu-id="f8e6b-367">0x02</span></span> | <span data-ttu-id="f8e6b-368">**Derleyici KIMLIĞI**</span><span class="sxs-lookup"><span data-stu-id="f8e6b-368">**Compiler ID**</span></span><br /><span data-ttu-id="f8e6b-369">IAR dili</span><span class="sxs-lookup"><span data-stu-id="f8e6b-369">IAR</span></span><br /><span data-ttu-id="f8e6b-370">ARM</span><span class="sxs-lookup"><span data-stu-id="f8e6b-370">ARM</span></span><br /><span data-ttu-id="f8e6b-371">GNU</span><span class="sxs-lookup"><span data-stu-id="f8e6b-371">GNU</span></span> |

#### <a name="module-linker-for-cortex-m3-using-iar"></a><span data-ttu-id="f8e6b-372">IAR kullanarak Cortex için modül Bağlayıcısı-m3</span><span class="sxs-lookup"><span data-stu-id="f8e6b-372">Module linker for Cortex-M3 using IAR</span></span>

```c
/*###ICF### Section handled by ICF editor, don't touch! ****/
/*-Editor annotation file-*/
/* IcfEditorFile="$TOOLKIT_DIR$\config\ide\IcfEditor\a_v1_0.xml" */
/*-Specials-*/
define symbol __ICFEDIT_intvec_start__ = 0x0;
/*-Memory Regions-*/
define symbol __ICFEDIT_region_ROM_start__ = 0x080f0000;
define symbol __ICFEDIT_region_ROM_end__   = 0x080fffff;
define symbol __ICFEDIT_region_RAM_start__ = 0x64002800;
define symbol __ICFEDIT_region_RAM_end__   = 0x64100000;
/*-Sizes-*/
define symbol __ICFEDIT_size_cstack__   = 0;
define symbol __ICFEDIT_size_svcstack__ = 0;
define symbol __ICFEDIT_size_irqstack__ = 0;
define symbol __ICFEDIT_size_fiqstack__ = 0;
define symbol __ICFEDIT_size_undstack__ = 0;
define symbol __ICFEDIT_size_abtstack__ = 0;
define symbol __ICFEDIT_size_heap__     = 0x1000;
/**** End of ICF editor section. ###ICF###*/

define memory mem with size = 4G;
define region ROM_region   = mem:[from __ICFEDIT_region_ROM_start__   to __ICFEDIT_region_ROM_end__];
define region RAM_region   = mem:[from __ICFEDIT_region_RAM_start__   to __ICFEDIT_region_RAM_end__];

//define block CSTACK    with alignment = 8, size = __ICFEDIT_size_cstack__   { };
//define block SVC_STACK with alignment = 8, size = __ICFEDIT_size_svcstack__ { };
//define block IRQ_STACK with alignment = 8, size = __ICFEDIT_size_irqstack__ { };
//define block FIQ_STACK with alignment = 8, size = __ICFEDIT_size_fiqstack__ { };
//define block UND_STACK with alignment = 8, size = __ICFEDIT_size_undstack__ { };
//define block ABT_STACK with alignment = 8, size = __ICFEDIT_size_abtstack__ { };
define block HEAP      with alignment = 8, size = __ICFEDIT_size_heap__     { };

initialize by copy { readwrite };
do not initialize  { section .noinit };

//place at address mem:__ICFEDIT_intvec_start__ { readonly section .intvec };

define movable block ROPI with alignment = 4, fixed order
{
  ro object txm_module_preamble_stm32f2xx.o,
  ro,
  ro data
};

define movable block RWPI with alignment = 8, fixed order, static base
{
  rw,
  block HEAP
};

place in ROM_region   { block ROPI };
place in RAM_region   { block RWPI };
```

#### <a name="building-modules-for-cortex-m3-using-iar"></a><span data-ttu-id="f8e6b-373">IAR kullanarak Cortex için modüller oluşturma-m3</span><span class="sxs-lookup"><span data-stu-id="f8e6b-373">Building Modules for Cortex-M3 using IAR</span></span>

<span data-ttu-id="f8e6b-374">Örnek çalışma alanı sağlanır.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-374">An example workspace is provided.</span></span> <span data-ttu-id="f8e6b-375">ThreadX kitaplığı, ThreadX modülleri kitaplığı, demo modülü projesi ve tanıtım modülü Yöneticisi projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-375">Build the ThreadX library, ThreadX Modules library, demo module project, and demo module manager project.</span></span>

#### <a name="thread-extension-definition-for-cortex-m3-using-iar"></a><span data-ttu-id="f8e6b-376">Cortex için iş parçacığı uzantısı tanımı-ıAR kullanılarak m3</span><span class="sxs-lookup"><span data-stu-id="f8e6b-376">Thread extension definition for Cortex-M3 using IAR</span></span>

```c
#define TX_THREAD_EXTENSION_2   VOID    *tx_thread_module_instance_ptr;         \
                                VOID    *tx_thread_module_entry_info_ptr;       \
                                ULONG   tx_thread_module_current_user_mode;     \
                                ULONG   tx_thread_module_user_mode;             \
                                ULONG   tx_thread_module_saved_lr;              \
                                VOID    *tx_thread_module_kernel_stack_start;   \
                                VOID    *tx_thread_module_kernel_stack_end;     \
                                ULONG   tx_thread_module_kernel_stack_size;     \
                                VOID    *tx_thread_module_stack_ptr;            \
                                VOID    *tx_thread_module_stack_start;          \
                                VOID    *tx_thread_module_stack_end;            \
                                ULONG   tx_thread_module_stack_size;            \
                                VOID    *tx_thread_module_reserved;             \
                                VOID    *tx_thread_iar_tls_pointer;
```

#### <a name="building-module-manager-for-cortex-m3-using-iar"></a><span data-ttu-id="f8e6b-377">IAR kullanarak Cortex için Modül Yöneticisi oluşturma-m3</span><span class="sxs-lookup"><span data-stu-id="f8e6b-377">Building Module Manager for Cortex-M3 using IAR</span></span>

<span data-ttu-id="f8e6b-378">Örnek çalışma alanı sağlanır.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-378">An example workspace is provided.</span></span> <span data-ttu-id="f8e6b-379">ThreadX kitaplığı, ThreadX modülleri kitaplığı, demo modülü projesi ve tanıtım modülü Yöneticisi projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-379">Build the ThreadX library, ThreadX Modules library, demo module project, and demo module manager project.</span></span>

#### <a name="attributes-for-external-memory-enable-api-for-cortex-m3-using-iar"></a><span data-ttu-id="f8e6b-380">Dış bellek öznitelikleri, ıAR kullanarak Cortex için API 'YI etkinleştirir</span><span class="sxs-lookup"><span data-stu-id="f8e6b-380">Attributes for external memory enable API for Cortex-M3 using IAR</span></span>

<span data-ttu-id="f8e6b-381">Modülün paylaşılan belleğe her zaman okuma erişimi vardır.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-381">Module always has read access to shared memory.</span></span>

| <span data-ttu-id="f8e6b-382">Öznitelik parametresi</span><span class="sxs-lookup"><span data-stu-id="f8e6b-382">Attribute parameter</span></span> | <span data-ttu-id="f8e6b-383">Anlamı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-383">Meaning</span></span> |
|---|---|
| <span data-ttu-id="f8e6b-384">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span><span class="sxs-lookup"><span data-stu-id="f8e6b-384">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span></span> | <span data-ttu-id="f8e6b-385">Yazma erişimi</span><span class="sxs-lookup"><span data-stu-id="f8e6b-385">Write access</span></span> |

## <a name="cortex-m33-processor"></a><span data-ttu-id="f8e6b-386">Cortex-M33 işlemcisi</span><span class="sxs-lookup"><span data-stu-id="f8e6b-386">Cortex-M33 processor</span></span>

### <a name="cortex-m33-using-ac6"></a><span data-ttu-id="f8e6b-387">Cortex-AC6 kullanarak M33</span><span class="sxs-lookup"><span data-stu-id="f8e6b-387">Cortex-M33 using AC6</span></span>

#### <a name="module-preamble-for-cortex-m33-using-ac6"></a><span data-ttu-id="f8e6b-388">AC6 kullanarak Cortex için modül girişi-M33</span><span class="sxs-lookup"><span data-stu-id="f8e6b-388">Module preamble for Cortex-M33 using AC6</span></span>

```c
    .text
    .align 4
    .syntax unified
    .section RESET
    
    // Define public symbols
    .global __txm_module_preamble

    // Define application-specific start/stop entry points for the module
    .global demo_module_start

    // Define common external references
    .global  _txm_module_thread_shell_entry
    .global  _txm_module_callback_request_thread_entry

    .eabi_attribute Tag_ABI_PCS_RO_data, 1
    .eabi_attribute Tag_ABI_PCS_R9_use,  1
    .eabi_attribute Tag_ABI_PCS_RW_data, 2

__txm_module_preamble:
    .dc.l   0x4D4F4455                                          // Module ID
    .dc.l   0x6                                                 // Module Major Version
    .dc.l   0x1                                                 // Module Minor Version
    .dc.l   32                                                  // Module Preamble Size in 32-bit words
    .dc.l   0x12345678                                          // Module ID (application defined)
    .dc.l   0x01000007                                          // Module Properties where:
                                                                //   Bits 31-24: Compiler ID
                                                                //           0 -> IAR
                                                                //           1 -> ARM
                                                                //           2 -> GNU
                                                                //   Bit 0:  0 -> Privileged mode execution
                                                                //           1 -> User mode execution
                                                                //   Bit 1:  0 -> No MPU protection
                                                                //           1 -> MPU protection (must have user mode selected)
                                                                //   Bit 2:  0 -> Disable shared/external memory access
                                                                //           1 -> Enable shared/external memory access
    .dc.l   _txm_module_thread_shell_entry - __txm_module_preamble // Module Shell Entry Point
    .dc.l   demo_module_start - __txm_module_preamble           // Module Start Thread Entry Point
    .dc.l   0                                                   // Module Stop Thread Entry Point
    .dc.l   1                                                   // Module Start/Stop Thread Priority
    .dc.l   1024                                                // Module Start/Stop Thread Stack Size
    .dc.l   _txm_module_callback_request_thread_entry - __txm_module_preamble // Module Callback Thread Entry
    .dc.l   1                                                   // Module Callback Thread Priority
    .dc.l   1024                                                // Module Callback Thread Stack Size
    //the tools can't add two symbols together, but it should look like this:
    //.dc.l   Image$$ER_RO$$Length + Image$$ER_RW$$Length         // Module Code Size
    //.dc.l   Image$$ER_RW$$Length + Image$$ER_ZI$$ZI$$Length     // Module Data Size
    //so instead we'll define hard values:
    .dc.l   0x4000                                              // Module Code Size
    .dc.l   0x4000                                              // Module Data Size
    .dc.l   0                                                   // Reserved 0
    .dc.l   0                                                   // Reserved 1
    .dc.l   0                                                   // Reserved 2
    .dc.l   0                                                   // Reserved 3
    .dc.l   0                                                   // Reserved 4
    .dc.l   0                                                   // Reserved 5
    .dc.l   0                                                   // Reserved 6
    .dc.l   0                                                   // Reserved 7
    .dc.l   0                                                   // Reserved 8
    .dc.l   0                                                   // Reserved 9
    .dc.l   0                                                   // Reserved 10
    .dc.l   0                                                   // Reserved 11
    .dc.l   0                                                   // Reserved 12
    .dc.l   0                                                   // Reserved 13
    .dc.l   0                                                   // Reserved 14
    .dc.l   0                                                   // Reserved 15
```

#### <a name="module-properties-for-cortex-m33-using-ac6"></a><span data-ttu-id="f8e6b-389">AC6 kullanarak Cortex-M33 için modül özellikleri</span><span class="sxs-lookup"><span data-stu-id="f8e6b-389">Module properties for Cortex-M33 using AC6</span></span>

| <span data-ttu-id="f8e6b-390">Sürümleri</span><span class="sxs-lookup"><span data-stu-id="f8e6b-390">Bit</span></span> | <span data-ttu-id="f8e6b-391">Değer</span><span class="sxs-lookup"><span data-stu-id="f8e6b-391">Value</span></span> | <span data-ttu-id="f8e6b-392">Anlamı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-392">Meaning</span></span> |
|---|---|---|
| <span data-ttu-id="f8e6b-393">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-393">0</span></span> | <span data-ttu-id="f8e6b-394">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-394">0</span></span><br /><span data-ttu-id="f8e6b-395">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-395">1</span></span> | <span data-ttu-id="f8e6b-396">Ayrıcalıklı mod yürütme</span><span class="sxs-lookup"><span data-stu-id="f8e6b-396">Privileged mode execution</span></span><br /><span data-ttu-id="f8e6b-397">Kullanıcı modu yürütme</span><span class="sxs-lookup"><span data-stu-id="f8e6b-397">User mode execution</span></span> |
| <span data-ttu-id="f8e6b-398">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-398">1</span></span> | <span data-ttu-id="f8e6b-399">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-399">0</span></span><br /><span data-ttu-id="f8e6b-400">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-400">1</span></span> | <span data-ttu-id="f8e6b-401">MPU koruması yok</span><span class="sxs-lookup"><span data-stu-id="f8e6b-401">No MPU protection</span></span><br /><span data-ttu-id="f8e6b-402">MPU koruması (Kullanıcı modunun seçili olması gerekir)</span><span class="sxs-lookup"><span data-stu-id="f8e6b-402">MPU protection (must have user mode selected)</span></span> |
| <span data-ttu-id="f8e6b-403">2</span><span class="sxs-lookup"><span data-stu-id="f8e6b-403">2</span></span> | <span data-ttu-id="f8e6b-404">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-404">0</span></span><br /><span data-ttu-id="f8e6b-405">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-405">1</span></span> | <span data-ttu-id="f8e6b-406">Paylaşılan/dış bellek erişimini devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="f8e6b-406">Disable shared/external memory access</span></span><br /><span data-ttu-id="f8e6b-407">Paylaşılan/dış bellek erişimini etkinleştir</span><span class="sxs-lookup"><span data-stu-id="f8e6b-407">Enable shared/external memory access</span></span> |
| <span data-ttu-id="f8e6b-408">[23-3]</span><span class="sxs-lookup"><span data-stu-id="f8e6b-408">[23-3]</span></span> | <span data-ttu-id="f8e6b-409">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-409">0</span></span> | <span data-ttu-id="f8e6b-410">Ayrılmıştır</span><span class="sxs-lookup"><span data-stu-id="f8e6b-410">Reserved</span></span>
| <span data-ttu-id="f8e6b-411">[31-24]</span><span class="sxs-lookup"><span data-stu-id="f8e6b-411">[31-24]</span></span> | <br /><span data-ttu-id="f8e6b-412">-</span><span class="sxs-lookup"><span data-stu-id="f8e6b-412">0x00</span></span><br /><span data-ttu-id="f8e6b-413">0x01</span><span class="sxs-lookup"><span data-stu-id="f8e6b-413">0x01</span></span><br /><span data-ttu-id="f8e6b-414">0x02</span><span class="sxs-lookup"><span data-stu-id="f8e6b-414">0x02</span></span> | <span data-ttu-id="f8e6b-415">**Derleyici KIMLIĞI**</span><span class="sxs-lookup"><span data-stu-id="f8e6b-415">**Compiler ID**</span></span><br /><span data-ttu-id="f8e6b-416">IAR dili</span><span class="sxs-lookup"><span data-stu-id="f8e6b-416">IAR</span></span><br /><span data-ttu-id="f8e6b-417">ARM</span><span class="sxs-lookup"><span data-stu-id="f8e6b-417">ARM</span></span><br /><span data-ttu-id="f8e6b-418">GNU</span><span class="sxs-lookup"><span data-stu-id="f8e6b-418">GNU</span></span> |

#### <a name="module-linker-for-cortex-m33-using-ac6"></a><span data-ttu-id="f8e6b-419">AC6 kullanarak Cortex için modül Bağlayıcısı-M33</span><span class="sxs-lookup"><span data-stu-id="f8e6b-419">Module linker for Cortex-M33 using AC6</span></span>

<span data-ttu-id="f8e6b-420">KEIL araç zinciri için bağlayıcı dosyası gerekmez.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-420">No linker file needed for Keil toolchain.</span></span> <span data-ttu-id="f8e6b-421">Örnek projede derleme ayarları ' na bakın.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-421">See build settings in example project.</span></span>
<span data-ttu-id="f8e6b-422">Önemli bağlayıcı seçenekleri aşağıda listelenmiştir:</span><span class="sxs-lookup"><span data-stu-id="f8e6b-422">Important linker options are listed below:</span></span>

```c
--entry demo_module_start --first __txm_module_preamble
```

#### <a name="building-modules-for-cortex-m33-using-ac6"></a><span data-ttu-id="f8e6b-423">AC6 kullanarak Cortex için modüller oluşturma-M33</span><span class="sxs-lookup"><span data-stu-id="f8e6b-423">Building Modules for Cortex-M33 using AC6</span></span>

<span data-ttu-id="f8e6b-424">Derleyici ayarları:</span><span class="sxs-lookup"><span data-stu-id="f8e6b-424">Compiler settings:</span></span>

```c
-xc -std=c99 --target=arm-arm-none-eabi -mcpu=cortex-m33 -mfpu=fpv5-sp-d16 -mfloat-abi=hard -c
-fno-rtti -funsigned-char -fshort-enums -fshort-wchar
-mlittle-endian -gdwarf-3 -fropi -frwpi -O1 -ffunction-sections -Wno-packed -Wno-missing-variable-declarations -Wno-missing-prototypes -Wno-missing-noreturn -Wno-sign-conversion -Wno-nonportable-include-path -Wno-reserved-id-macro -Wno-unused-macros -Wno-documentation-unknown-command -Wno-documentation -Wno-license-management -Wno-parentheses-equality -I ../../../../../common_modules/inc -I ../../../../../common/inc -I ../../../../../ports_module/cortex_m33/ac6/inc -I ../demo_secure_zone
-I./RTE/_FVP_Simulation_Model
-IC:/Users/your_path/AppData/Local/Arm/Packs/ARM/CMSIS/5.5.1/CMSIS/Core/Include
-IC:/Users/your_path/AppData/Local/Arm/Packs/ARM/CMSIS/5.5.1/Device/ARM/ARMCM33/Include
-D__UVISION_VERSION="531" -D_RTE_ -DARMCM33_DSP_FP_TZ -D_RTE_
-o ./Objects/*.o -MD
```

#### <a name="thread-extension-definition-for-cortex-m33-using-ac6"></a><span data-ttu-id="f8e6b-425">AC6 kullanarak Cortex için iş parçacığı uzantısı tanımı M33</span><span class="sxs-lookup"><span data-stu-id="f8e6b-425">Thread extension definition for Cortex-M33 using AC6</span></span>

```c
#define TX_THREAD_EXTENSION_2                   VOID    *tx_thread_module_instance_ptr;         \
                                                VOID    *tx_thread_module_entry_info_ptr;       \
                                                ULONG   tx_thread_module_current_user_mode;     \
                                                ULONG   tx_thread_module_user_mode;             \
                                                ULONG   tx_thread_module_saved_lr;              \
                                                VOID    *tx_thread_module_kernel_stack_start;   \
                                                VOID    *tx_thread_module_kernel_stack_end;     \
                                                ULONG   tx_thread_module_kernel_stack_size;     \
                                                VOID    *tx_thread_module_stack_ptr;            \
                                                VOID    *tx_thread_module_stack_start;          \
                                                VOID    *tx_thread_module_stack_end;            \
                                                ULONG   tx_thread_module_stack_size;            \
                                                VOID    *tx_thread_module_reserved;
```

#### <a name="building-module-manager-for-cortex-m33-using-ac6"></a><span data-ttu-id="f8e6b-426">AC6 kullanarak Cortex için Modül Yöneticisi oluşturma-M33</span><span class="sxs-lookup"><span data-stu-id="f8e6b-426">Building Module Manager for Cortex-M33 using AC6</span></span>

<span data-ttu-id="f8e6b-427">Örnek çalışma alanı sağlanır.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-427">An example workspace is provided.</span></span> <span data-ttu-id="f8e6b-428">ThreadX kitaplığı, ThreadX modülleri kitaplığı, sample_threadx_module projesi ve demo_threadx_non secure_zone projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-428">Build the ThreadX library, ThreadX Modules library, sample_threadx_module project, and demo_threadx_non-secure_zone project.</span></span>

#### <a name="attributes-for-external-memory-enable-api-for-cortex-m33-using-ac6"></a><span data-ttu-id="f8e6b-429">Dış bellek öznitelikleri M33 Cortex için API 'YI etkinleştirir-AC6 kullanarak</span><span class="sxs-lookup"><span data-stu-id="f8e6b-429">Attributes for external memory enable API for Cortex-M33 using AC6</span></span>

| <span data-ttu-id="f8e6b-430">Öznitelik parametresi</span><span class="sxs-lookup"><span data-stu-id="f8e6b-430">Attribute parameter</span></span> |
|---|
| <span data-ttu-id="f8e6b-431">TXM_MODULE_ATTRIBUTE_NON_SHAREABLE</span><span class="sxs-lookup"><span data-stu-id="f8e6b-431">TXM_MODULE_ATTRIBUTE_NON_SHAREABLE</span></span> |
| <span data-ttu-id="f8e6b-432">TXM_MODULE_ATTRIBUTE_OUTER_SHAREABLE</span><span class="sxs-lookup"><span data-stu-id="f8e6b-432">TXM_MODULE_ATTRIBUTE_OUTER_SHAREABLE</span></span> |
| <span data-ttu-id="f8e6b-433">TXM_MODULE_ATTRIBUTE_INNER_SHAREABLE</span><span class="sxs-lookup"><span data-stu-id="f8e6b-433">TXM_MODULE_ATTRIBUTE_INNER_SHAREABLE</span></span> |
| <span data-ttu-id="f8e6b-434">TXM_MODULE_ATTRIBUTE_READ_WRITE</span><span class="sxs-lookup"><span data-stu-id="f8e6b-434">TXM_MODULE_ATTRIBUTE_READ_WRITE</span></span> |
| <span data-ttu-id="f8e6b-435">TXM_MODULE_ATTRIBUTE_READ_ONLY</span><span class="sxs-lookup"><span data-stu-id="f8e6b-435">TXM_MODULE_ATTRIBUTE_READ_ONLY</span></span> |

### <a name="cortex-m33-using-gnu"></a><span data-ttu-id="f8e6b-436">Cortex-GNU kullanarak M33</span><span class="sxs-lookup"><span data-stu-id="f8e6b-436">Cortex-M33 using GNU</span></span>

#### <a name="module-preamble-for-cortex-m33-using-gnu"></a><span data-ttu-id="f8e6b-437">GNU kullanarak Cortex için modül girişi-M33</span><span class="sxs-lookup"><span data-stu-id="f8e6b-437">Module preamble for Cortex-M33 using GNU</span></span>

#### <a name="module-properties-for-cortex-m33-using-gnu"></a><span data-ttu-id="f8e6b-438">GNU kullanarak Cortex-M33 için modül özellikleri</span><span class="sxs-lookup"><span data-stu-id="f8e6b-438">Module properties for Cortex-M33 using GNU</span></span>

| <span data-ttu-id="f8e6b-439">Sürümleri</span><span class="sxs-lookup"><span data-stu-id="f8e6b-439">Bit</span></span> | <span data-ttu-id="f8e6b-440">Değer</span><span class="sxs-lookup"><span data-stu-id="f8e6b-440">Value</span></span> | <span data-ttu-id="f8e6b-441">Anlamı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-441">Meaning</span></span> |
|---|---|---|
| <span data-ttu-id="f8e6b-442">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-442">0</span></span> | <span data-ttu-id="f8e6b-443">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-443">0</span></span><br /><span data-ttu-id="f8e6b-444">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-444">1</span></span> | <span data-ttu-id="f8e6b-445">Ayrıcalıklı mod yürütme</span><span class="sxs-lookup"><span data-stu-id="f8e6b-445">Privileged mode execution</span></span><br /><span data-ttu-id="f8e6b-446">Kullanıcı modu yürütme</span><span class="sxs-lookup"><span data-stu-id="f8e6b-446">User mode execution</span></span> |
| <span data-ttu-id="f8e6b-447">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-447">1</span></span> | <span data-ttu-id="f8e6b-448">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-448">0</span></span><br /><span data-ttu-id="f8e6b-449">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-449">1</span></span> | <span data-ttu-id="f8e6b-450">MPU koruması yok</span><span class="sxs-lookup"><span data-stu-id="f8e6b-450">No MPU protection</span></span><br /><span data-ttu-id="f8e6b-451">MPU koruması (Kullanıcı modunun seçili olması gerekir)</span><span class="sxs-lookup"><span data-stu-id="f8e6b-451">MPU protection (must have user mode selected)</span></span> |
| <span data-ttu-id="f8e6b-452">2</span><span class="sxs-lookup"><span data-stu-id="f8e6b-452">2</span></span> | <span data-ttu-id="f8e6b-453">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-453">0</span></span><br /><span data-ttu-id="f8e6b-454">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-454">1</span></span> | <span data-ttu-id="f8e6b-455">Paylaşılan/dış bellek erişimini devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="f8e6b-455">Disable shared/external memory access</span></span><br /><span data-ttu-id="f8e6b-456">Paylaşılan/dış bellek erişimini etkinleştir</span><span class="sxs-lookup"><span data-stu-id="f8e6b-456">Enable shared/external memory access</span></span> |
| <span data-ttu-id="f8e6b-457">[23-3]</span><span class="sxs-lookup"><span data-stu-id="f8e6b-457">[23-3]</span></span> | <span data-ttu-id="f8e6b-458">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-458">0</span></span> | <span data-ttu-id="f8e6b-459">Ayrılmıştır</span><span class="sxs-lookup"><span data-stu-id="f8e6b-459">Reserved</span></span>
| <span data-ttu-id="f8e6b-460">[31-24]</span><span class="sxs-lookup"><span data-stu-id="f8e6b-460">[31-24]</span></span> | <br /><span data-ttu-id="f8e6b-461">-</span><span class="sxs-lookup"><span data-stu-id="f8e6b-461">0x00</span></span><br /><span data-ttu-id="f8e6b-462">0x01</span><span class="sxs-lookup"><span data-stu-id="f8e6b-462">0x01</span></span><br /><span data-ttu-id="f8e6b-463">0x02</span><span class="sxs-lookup"><span data-stu-id="f8e6b-463">0x02</span></span> | <span data-ttu-id="f8e6b-464">**Derleyici KIMLIĞI**</span><span class="sxs-lookup"><span data-stu-id="f8e6b-464">**Compiler ID**</span></span><br /><span data-ttu-id="f8e6b-465">IAR dili</span><span class="sxs-lookup"><span data-stu-id="f8e6b-465">IAR</span></span><br /><span data-ttu-id="f8e6b-466">ARM</span><span class="sxs-lookup"><span data-stu-id="f8e6b-466">ARM</span></span><br /><span data-ttu-id="f8e6b-467">GNU</span><span class="sxs-lookup"><span data-stu-id="f8e6b-467">GNU</span></span> |

#### <a name="module-linker-for-cortex-m33-using-gnu"></a><span data-ttu-id="f8e6b-468">GNU kullanarak Cortex için modül Bağlayıcısı-M33</span><span class="sxs-lookup"><span data-stu-id="f8e6b-468">Module linker for Cortex-M33 using GNU</span></span>

#### <a name="building-modules-for-cortex-m33-using-gnu"></a><span data-ttu-id="f8e6b-469">GNU kullanarak Cortex için modüller oluşturma-M33</span><span class="sxs-lookup"><span data-stu-id="f8e6b-469">Building Modules for Cortex-M33 using GNU</span></span>

#### <a name="thread-extension-definition-for-cortex-m33-using-gnu"></a><span data-ttu-id="f8e6b-470">GNU kullanarak Cortex-M33 için iş parçacığı uzantısı tanımı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-470">Thread extension definition for Cortex-M33 using GNU</span></span>

#### <a name="building-module-manager-for-cortex-m33-using-gnu"></a><span data-ttu-id="f8e6b-471">GNU kullanarak Cortex için Modül Yöneticisi oluşturma-M33</span><span class="sxs-lookup"><span data-stu-id="f8e6b-471">Building Module Manager for Cortex-M33 using GNU</span></span>

#### <a name="attributes-for-external-memory-enable-api-for-cortex-m33-using-gnu"></a><span data-ttu-id="f8e6b-472">Dış bellek öznitelikleri, GNU kullanarak Cortex için API 'YI etkinleştirir-M33</span><span class="sxs-lookup"><span data-stu-id="f8e6b-472">Attributes for external memory enable API for Cortex-M33 using GNU</span></span>

| <span data-ttu-id="f8e6b-473">Öznitelik parametresi</span><span class="sxs-lookup"><span data-stu-id="f8e6b-473">Attribute parameter</span></span> |
|---|
| <span data-ttu-id="f8e6b-474">TXM_MODULE_ATTRIBUTE_NON_SHAREABLE</span><span class="sxs-lookup"><span data-stu-id="f8e6b-474">TXM_MODULE_ATTRIBUTE_NON_SHAREABLE</span></span> |
| <span data-ttu-id="f8e6b-475">TXM_MODULE_ATTRIBUTE_OUTER_SHAREABLE</span><span class="sxs-lookup"><span data-stu-id="f8e6b-475">TXM_MODULE_ATTRIBUTE_OUTER_SHAREABLE</span></span> |
| <span data-ttu-id="f8e6b-476">TXM_MODULE_ATTRIBUTE_INNER_SHAREABLE</span><span class="sxs-lookup"><span data-stu-id="f8e6b-476">TXM_MODULE_ATTRIBUTE_INNER_SHAREABLE</span></span> |
| <span data-ttu-id="f8e6b-477">TXM_MODULE_ATTRIBUTE_READ_WRITE</span><span class="sxs-lookup"><span data-stu-id="f8e6b-477">TXM_MODULE_ATTRIBUTE_READ_WRITE</span></span> |
| <span data-ttu-id="f8e6b-478">TXM_MODULE_ATTRIBUTE_READ_ONLY</span><span class="sxs-lookup"><span data-stu-id="f8e6b-478">TXM_MODULE_ATTRIBUTE_READ_ONLY</span></span> |

### <a name="cortex-m33-using-iar"></a><span data-ttu-id="f8e6b-479">Cortex-ıAR kullanarak M33</span><span class="sxs-lookup"><span data-stu-id="f8e6b-479">Cortex-M33 using IAR</span></span>

#### <a name="module-preamble-for-cortex-m33-using-iar"></a><span data-ttu-id="f8e6b-480">IAR kullanarak Cortex için modül girişi-M33</span><span class="sxs-lookup"><span data-stu-id="f8e6b-480">Module preamble for Cortex-M33 using IAR</span></span>

```c
    SECTION .text:CODE

    AAPCS INTERWORK, ROPI, RWPI_COMPATIBLE,  VFP_COMPATIBLE
    PRESERVE8

    /* Define public symbols.  */

    PUBLIC __txm_module_preamble


    /* Define application-specific start/stop entry points for the module.  */

    EXTERN demo_module_start


    /* Define common external refrences.  */

    EXTERN  _txm_module_thread_shell_entry
    EXTERN  _txm_module_callback_request_thread_entry
    EXTERN  ROPI$$Length
    EXTERN  RWPI$$Length

    DATA
__txm_module_preamble:
    DC32      0x4D4F4455                                        // Module ID
    DC32      0x6                                               // Module Major Version
    DC32      0x1                                               // Module Minor Version
    DC32      32                                                // Module Preamble Size in 32-bit words
    DC32      0x12345678                                        // Module ID (application defined)
    DC32      0x00000007                                        // Module Properties where:
                                                                //   Bits 31-24: Compiler ID
                                                                //           0 -> IAR
                                                                //           1 -> ARM
                                                                //           2 -> GNU
                                                                //   Bits 23-3: Reserved
                                                                //   Bit 2:  0 -> Disable shared/external memory access
                                                                //           1 -> Enable shared/external memory access
                                                                //   Bit 1:  0 -> No MPU protection
                                                                //           1 -> MPU protection (must have user mode selected - bit 0 set)
                                                                //   Bit 0:  0 -> Privileged mode execution
                                                                //           1 -> User mode execution
    DC32      _txm_module_thread_shell_entry - . - 0            // Module Shell Entry Point
    DC32      demo_module_start - . - 0                         // Module Start Thread Entry Point
    DC32      0                                                 // Module Stop Thread Entry Point
    DC32      1                                                 // Module Start/Stop Thread Priority
    DC32      1024                                              // Module Start/Stop Thread Stack Size
    DC32      _txm_module_callback_request_thread_entry - . - 0 // Module Callback Thread Entry
    DC32      1                                                 // Module Callback Thread Priority
    DC32      1024                                              // Module Callback Thread Stack Size
    DC32      ROPI$$Length                                      // Module Code Size
    DC32      RWPI$$Length                                      // Module Data Size
    DC32      0                                                 // Reserved 0
    DC32      0                                                 // Reserved 1
    DC32      0                                                 // Reserved 2
    DC32      0                                                 // Reserved 3
    DC32      0                                                 // Reserved 4
    DC32      0                                                 // Reserved 5
    DC32      0                                                 // Reserved 6
    DC32      0                                                 // Reserved 7
    DC32      0                                                 // Reserved 8
    DC32      0                                                 // Reserved 9
    DC32      0                                                 // Reserved 10
    DC32      0                                                 // Reserved 11
    DC32      0                                                 // Reserved 12
    DC32      0                                                 // Reserved 13
    DC32      0                                                 // Reserved 14
    DC32      0                                                 // Reserved 15

    END

```

#### <a name="module-properties-for-cortex-m33-using-iar"></a><span data-ttu-id="f8e6b-481">IAR kullanarak Cortex-M33 için modül özellikleri</span><span class="sxs-lookup"><span data-stu-id="f8e6b-481">Module properties for Cortex-M33 using IAR</span></span>

| <span data-ttu-id="f8e6b-482">Sürümleri</span><span class="sxs-lookup"><span data-stu-id="f8e6b-482">Bit</span></span> | <span data-ttu-id="f8e6b-483">Değer</span><span class="sxs-lookup"><span data-stu-id="f8e6b-483">Value</span></span> | <span data-ttu-id="f8e6b-484">Anlamı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-484">Meaning</span></span> |
|---|---|---|
| <span data-ttu-id="f8e6b-485">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-485">0</span></span> | <span data-ttu-id="f8e6b-486">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-486">0</span></span><br /><span data-ttu-id="f8e6b-487">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-487">1</span></span> | <span data-ttu-id="f8e6b-488">Ayrıcalıklı mod yürütme</span><span class="sxs-lookup"><span data-stu-id="f8e6b-488">Privileged mode execution</span></span><br /><span data-ttu-id="f8e6b-489">Kullanıcı modu yürütme</span><span class="sxs-lookup"><span data-stu-id="f8e6b-489">User mode execution</span></span> |
| <span data-ttu-id="f8e6b-490">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-490">1</span></span> | <span data-ttu-id="f8e6b-491">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-491">0</span></span><br /><span data-ttu-id="f8e6b-492">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-492">1</span></span> | <span data-ttu-id="f8e6b-493">MPU koruması yok</span><span class="sxs-lookup"><span data-stu-id="f8e6b-493">No MPU protection</span></span><br /><span data-ttu-id="f8e6b-494">MPU koruması (Kullanıcı modunun seçili olması gerekir)</span><span class="sxs-lookup"><span data-stu-id="f8e6b-494">MPU protection (must have user mode selected)</span></span> |
| <span data-ttu-id="f8e6b-495">2</span><span class="sxs-lookup"><span data-stu-id="f8e6b-495">2</span></span> | <span data-ttu-id="f8e6b-496">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-496">0</span></span><br /><span data-ttu-id="f8e6b-497">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-497">1</span></span> | <span data-ttu-id="f8e6b-498">Paylaşılan/dış bellek erişimini devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="f8e6b-498">Disable shared/external memory access</span></span><br /><span data-ttu-id="f8e6b-499">Paylaşılan/dış bellek erişimini etkinleştir</span><span class="sxs-lookup"><span data-stu-id="f8e6b-499">Enable shared/external memory access</span></span> |
| <span data-ttu-id="f8e6b-500">[23-3]</span><span class="sxs-lookup"><span data-stu-id="f8e6b-500">[23-3]</span></span> | <span data-ttu-id="f8e6b-501">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-501">0</span></span> | <span data-ttu-id="f8e6b-502">Ayrılmıştır</span><span class="sxs-lookup"><span data-stu-id="f8e6b-502">Reserved</span></span>
| <span data-ttu-id="f8e6b-503">[31-24]</span><span class="sxs-lookup"><span data-stu-id="f8e6b-503">[31-24]</span></span> | <br /><span data-ttu-id="f8e6b-504">-</span><span class="sxs-lookup"><span data-stu-id="f8e6b-504">0x00</span></span><br /><span data-ttu-id="f8e6b-505">0x01</span><span class="sxs-lookup"><span data-stu-id="f8e6b-505">0x01</span></span><br /><span data-ttu-id="f8e6b-506">0x02</span><span class="sxs-lookup"><span data-stu-id="f8e6b-506">0x02</span></span> | <span data-ttu-id="f8e6b-507">**Derleyici KIMLIĞI**</span><span class="sxs-lookup"><span data-stu-id="f8e6b-507">**Compiler ID**</span></span><br /><span data-ttu-id="f8e6b-508">IAR dili</span><span class="sxs-lookup"><span data-stu-id="f8e6b-508">IAR</span></span><br /><span data-ttu-id="f8e6b-509">ARM</span><span class="sxs-lookup"><span data-stu-id="f8e6b-509">ARM</span></span><br /><span data-ttu-id="f8e6b-510">GNU</span><span class="sxs-lookup"><span data-stu-id="f8e6b-510">GNU</span></span> |

#### <a name="module-linker-for-cortex-m33-using-iar"></a><span data-ttu-id="f8e6b-511">IAR kullanarak Cortex için modül Bağlayıcısı-M33</span><span class="sxs-lookup"><span data-stu-id="f8e6b-511">Module linker for Cortex-M33 using IAR</span></span>

```c
/*###ICF### Section handled by ICF editor, don't touch! ****/
/*-Editor annotation file-*/
/* IcfEditorFile="$TOOLKIT_DIR$\config\ide\IcfEditor\a_v1_0.xml" */
/*-Specials-*/
define symbol __ICFEDIT_intvec_start__ = 0x0;
/*-Memory Regions-*/
define symbol __ICFEDIT_region_ROM_start__ = 0x080f0000;
define symbol __ICFEDIT_region_ROM_end__   = 0x080fffff;
define symbol __ICFEDIT_region_RAM_start__ = 0x64002800;
define symbol __ICFEDIT_region_RAM_end__   = 0x64100000;
/*-Sizes-*/
define symbol __ICFEDIT_size_cstack__   = 0;
define symbol __ICFEDIT_size_svcstack__ = 0;
define symbol __ICFEDIT_size_irqstack__ = 0;
define symbol __ICFEDIT_size_fiqstack__ = 0;
define symbol __ICFEDIT_size_undstack__ = 0;
define symbol __ICFEDIT_size_abtstack__ = 0;
define symbol __ICFEDIT_size_heap__     = 0x1000;
/**** End of ICF editor section. ###ICF###*/

define memory mem with size = 4G;
define region ROM_region   = mem:[from __ICFEDIT_region_ROM_start__   to __ICFEDIT_region_ROM_end__];
define region RAM_region   = mem:[from __ICFEDIT_region_RAM_start__   to __ICFEDIT_region_RAM_end__];

//define block CSTACK    with alignment = 8, size = __ICFEDIT_size_cstack__   { };
//define block SVC_STACK with alignment = 8, size = __ICFEDIT_size_svcstack__ { };
//define block IRQ_STACK with alignment = 8, size = __ICFEDIT_size_irqstack__ { };
//define block FIQ_STACK with alignment = 8, size = __ICFEDIT_size_fiqstack__ { };
//define block UND_STACK with alignment = 8, size = __ICFEDIT_size_undstack__ { };
//define block ABT_STACK with alignment = 8, size = __ICFEDIT_size_abtstack__ { };
define block HEAP      with alignment = 8, size = __ICFEDIT_size_heap__     { };

initialize by copy { readwrite };
do not initialize  { section .noinit };

//place at address mem:__ICFEDIT_intvec_start__ { readonly section .intvec };

define movable block ROPI with alignment = 4, fixed order 
{ 
  ro object txm_module_preamble.o,
  ro, 
  ro data 
};

define movable block RWPI with alignment = 8, fixed order, static base
{
  rw,
  block HEAP
};

place in ROM_region   { block ROPI };
place in RAM_region   { block RWPI };
```

#### <a name="building-modules-for-cortex-m33-using-iar"></a><span data-ttu-id="f8e6b-512">IAR kullanarak Cortex için modüller oluşturma-M33</span><span class="sxs-lookup"><span data-stu-id="f8e6b-512">Building Modules for Cortex-M33 using IAR</span></span>

#### <a name="thread-extension-definition-for-cortex-m33-using-iar"></a><span data-ttu-id="f8e6b-513">IAR kullanarak Cortex-M33 için iş parçacığı uzantısı tanımı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-513">Thread extension definition for Cortex-M33 using IAR</span></span>

```c
#define TX_THREAD_EXTENSION_2                   VOID    *tx_thread_module_instance_ptr;         \
                                                VOID    *tx_thread_module_entry_info_ptr;       \
                                                ULONG   tx_thread_module_current_user_mode;     \
                                                ULONG   tx_thread_module_user_mode;             \
                                                ULONG   tx_thread_module_saved_lr;              \
                                                VOID    *tx_thread_module_kernel_stack_start;   \
                                                VOID    *tx_thread_module_kernel_stack_end;     \
                                                ULONG   tx_thread_module_kernel_stack_size;     \
                                                VOID    *tx_thread_module_stack_ptr;            \
                                                VOID    *tx_thread_module_stack_start;          \
                                                VOID    *tx_thread_module_stack_end;            \
                                                ULONG   tx_thread_module_stack_size;            \
                                                VOID    *tx_thread_module_reserved;             \
                                                VOID    *tx_thread_iar_tls_pointer;
```

#### <a name="building-module-manager-for-cortex-m33-using-iar"></a><span data-ttu-id="f8e6b-514">IAR kullanarak Cortex için Modül Yöneticisi oluşturma-M33</span><span class="sxs-lookup"><span data-stu-id="f8e6b-514">Building Module Manager for Cortex-M33 using IAR</span></span>

<span data-ttu-id="f8e6b-515">Örnek çalışma alanı henüz sağlanmadı.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-515">An example workspace is not yet provided.</span></span> <span data-ttu-id="f8e6b-516">Çok yakında.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-516">Coming soon.</span></span>

#### <a name="attributes-for-external-memory-enable-api-for-cortex-m33-using-iar"></a><span data-ttu-id="f8e6b-517">Dış bellek öznitelikleri ıAR kullanarak Cortex için API 'YI etkinleştirir-M33</span><span class="sxs-lookup"><span data-stu-id="f8e6b-517">Attributes for external memory enable API for Cortex-M33 using IAR</span></span>

| <span data-ttu-id="f8e6b-518">Öznitelik parametresi</span><span class="sxs-lookup"><span data-stu-id="f8e6b-518">Attribute parameter</span></span> |
|---|
| <span data-ttu-id="f8e6b-519">TXM_MODULE_ATTRIBUTE_NON_SHAREABLE</span><span class="sxs-lookup"><span data-stu-id="f8e6b-519">TXM_MODULE_ATTRIBUTE_NON_SHAREABLE</span></span> |
| <span data-ttu-id="f8e6b-520">TXM_MODULE_ATTRIBUTE_OUTER_SHAREABLE</span><span class="sxs-lookup"><span data-stu-id="f8e6b-520">TXM_MODULE_ATTRIBUTE_OUTER_SHAREABLE</span></span> |
| <span data-ttu-id="f8e6b-521">TXM_MODULE_ATTRIBUTE_INNER_SHAREABLE</span><span class="sxs-lookup"><span data-stu-id="f8e6b-521">TXM_MODULE_ATTRIBUTE_INNER_SHAREABLE</span></span> |
| <span data-ttu-id="f8e6b-522">TXM_MODULE_ATTRIBUTE_READ_WRITE</span><span class="sxs-lookup"><span data-stu-id="f8e6b-522">TXM_MODULE_ATTRIBUTE_READ_WRITE</span></span> |
| <span data-ttu-id="f8e6b-523">TXM_MODULE_ATTRIBUTE_READ_ONLY</span><span class="sxs-lookup"><span data-stu-id="f8e6b-523">TXM_MODULE_ATTRIBUTE_READ_ONLY</span></span> |

## <a name="cortex-m4-processor"></a><span data-ttu-id="f8e6b-524">Cortex-M4 işlemcisi</span><span class="sxs-lookup"><span data-stu-id="f8e6b-524">Cortex-M4 processor</span></span>

### <a name="cortex-m4-using-ac5"></a><span data-ttu-id="f8e6b-525">Cortex-AC5 kullanarak M4</span><span class="sxs-lookup"><span data-stu-id="f8e6b-525">Cortex-M4 using AC5</span></span>

#### <a name="module-preamble-for-cortex-m4-using-ac5"></a><span data-ttu-id="f8e6b-526">AC5 kullanarak Cortex için modül girişi-M4</span><span class="sxs-lookup"><span data-stu-id="f8e6b-526">Module preamble for Cortex-M4 using AC5</span></span>

```armasm
    AREA Init, CODE, READONLY

    PRESERVE8

    /* Define public symbols.  */

    EXPORT __txm_module_preamble

    ; Define application-specific start/stop entry points for the module

    EXTERN demo_module_start

    /* Define common external references.  */

    IMPORT  _txm_module_thread_shell_entry
    IMPORT  _txm_module_callback_request_thread_entry
    IMPORT  |Image$$ER_RO$$Length|
    IMPORT  |Image$$ER_RW$$Length|
    IMPORT  |Image$$ER_RW$$RW$$Length|
    IMPORT  |Image$$ER_RW$$ZI$$Length|
    IMPORT  |Image$$ER_ZI$$ZI$$Length|

__txm_module_preamble
    DCD     0x4D4F4455                                          // Module ID
    DCD     0x6                                                 // Module Major Version
    DCD     0x1                                                 // Module Minor Version
    DCD     32                                                  // Module Preamble Size in 32-bit words
    DCD     0x12345678                                          // Module ID (application defined)
    DCD     0x01000007                                          // Module Properties where:
                                                                //   Bits 31-24: Compiler ID
                                                                //           0 -> IAR
                                                                //           1 -> ARM
                                                                //           2 -> GNU
                                                                //   Bits 23-3: Reserved
                                                                //   Bit 2:  0 -> Disable shared/external memory access
                                                                //           1 -> Enable shared/external memory access
                                                                //   Bit 1:  0 -> No MPU protection
                                                                //           1 -> MPU protection (must have user mode selected)
                                                                //   Bit 0:  0 -> Privileged mode execution
                                                                //           1 -> User mode execution
    DCD     _txm_module_thread_shell_entry - __txm_module_preamble              // Module Shell Entry Point
    DCD     demo_module_start - __txm_module_preamble           // Module Start Thread Entry Point
    DCD     0                                                   // Module Stop Thread Entry Point
    DCD     1                                                   // Module Start/Stop Thread Priority
    DCD     1024                                                // Module Start/Stop Thread Stack Size
    DCD     _txm_module_callback_request_thread_entry - __txm_module_preamble   // Module Callback Thread Entry
    DCD     1                                                   // Module Callback Thread Priority
    DCD     1024                                                // Module Callback Thread Stack Size
    DCD     |Image$$ER_RO$$Length| + |Image$$ER_RW$$Length|     // Module Code Size
    DCD     |Image$$ER_RW$$Length| + |Image$$ER_ZI$$ZI$$Length| // Module Data Size
    DCD     0                                                   // Reserved 0
    DCD     0                                                   // Reserved 1
    DCD     0                                                   // Reserved 2
    DCD     0                                                   // Reserved 3
    DCD     0                                                   // Reserved 4
    DCD     0                                                   // Reserved 5
    DCD     0                                                   // Reserved 6
    DCD     0                                                   // Reserved 7
    DCD     0                                                   // Reserved 8
    DCD     0                                                   // Reserved 9
    DCD     0                                                   // Reserved 10
    DCD     0                                                   // Reserved 11
    DCD     0                                                   // Reserved 12
    DCD     0                                                   // Reserved 13
    DCD     0                                                   // Reserved 14
    DCD     0                                                   // Reserved 15

    END
```

#### <a name="module-properties-for-cortex-m4-using-ac5"></a><span data-ttu-id="f8e6b-527">AC5 kullanarak Cortex-M4 için modül özellikleri</span><span class="sxs-lookup"><span data-stu-id="f8e6b-527">Module properties for Cortex-M4 using AC5</span></span>

| <span data-ttu-id="f8e6b-528">Sürümleri</span><span class="sxs-lookup"><span data-stu-id="f8e6b-528">Bit</span></span> | <span data-ttu-id="f8e6b-529">Değer</span><span class="sxs-lookup"><span data-stu-id="f8e6b-529">Value</span></span> | <span data-ttu-id="f8e6b-530">Anlamı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-530">Meaning</span></span> |
|---|---|---|
| <span data-ttu-id="f8e6b-531">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-531">0</span></span> | <span data-ttu-id="f8e6b-532">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-532">0</span></span><br /><span data-ttu-id="f8e6b-533">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-533">1</span></span> | <span data-ttu-id="f8e6b-534">Ayrıcalıklı mod yürütme</span><span class="sxs-lookup"><span data-stu-id="f8e6b-534">Privileged mode execution</span></span><br /><span data-ttu-id="f8e6b-535">Kullanıcı modu yürütme</span><span class="sxs-lookup"><span data-stu-id="f8e6b-535">User mode execution</span></span> |
| <span data-ttu-id="f8e6b-536">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-536">1</span></span> | <span data-ttu-id="f8e6b-537">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-537">0</span></span><br /><span data-ttu-id="f8e6b-538">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-538">1</span></span> | <span data-ttu-id="f8e6b-539">MPU koruması yok</span><span class="sxs-lookup"><span data-stu-id="f8e6b-539">No MPU protection</span></span><br /><span data-ttu-id="f8e6b-540">MPU koruması (Kullanıcı modunun seçili olması gerekir)</span><span class="sxs-lookup"><span data-stu-id="f8e6b-540">MPU protection (must have user mode selected)</span></span> |
| <span data-ttu-id="f8e6b-541">2</span><span class="sxs-lookup"><span data-stu-id="f8e6b-541">2</span></span> | <span data-ttu-id="f8e6b-542">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-542">0</span></span><br /><span data-ttu-id="f8e6b-543">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-543">1</span></span> | <span data-ttu-id="f8e6b-544">Paylaşılan/dış bellek erişimini devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="f8e6b-544">Disable shared/external memory access</span></span><br /><span data-ttu-id="f8e6b-545">Paylaşılan/dış bellek erişimini etkinleştir</span><span class="sxs-lookup"><span data-stu-id="f8e6b-545">Enable shared/external memory access</span></span> |
| <span data-ttu-id="f8e6b-546">[23-3]</span><span class="sxs-lookup"><span data-stu-id="f8e6b-546">[23-3]</span></span> | <span data-ttu-id="f8e6b-547">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-547">0</span></span> | <span data-ttu-id="f8e6b-548">Ayrılmıştır</span><span class="sxs-lookup"><span data-stu-id="f8e6b-548">Reserved</span></span>
| <span data-ttu-id="f8e6b-549">[31-24]</span><span class="sxs-lookup"><span data-stu-id="f8e6b-549">[31-24]</span></span> | <br /><span data-ttu-id="f8e6b-550">-</span><span class="sxs-lookup"><span data-stu-id="f8e6b-550">0x00</span></span><br /><span data-ttu-id="f8e6b-551">0x01</span><span class="sxs-lookup"><span data-stu-id="f8e6b-551">0x01</span></span><br /><span data-ttu-id="f8e6b-552">0x02</span><span class="sxs-lookup"><span data-stu-id="f8e6b-552">0x02</span></span> | <span data-ttu-id="f8e6b-553">**Derleyici KIMLIĞI**</span><span class="sxs-lookup"><span data-stu-id="f8e6b-553">**Compiler ID**</span></span><br /><span data-ttu-id="f8e6b-554">IAR dili</span><span class="sxs-lookup"><span data-stu-id="f8e6b-554">IAR</span></span><br /><span data-ttu-id="f8e6b-555">ARM</span><span class="sxs-lookup"><span data-stu-id="f8e6b-555">ARM</span></span><br /><span data-ttu-id="f8e6b-556">GNU</span><span class="sxs-lookup"><span data-stu-id="f8e6b-556">GNU</span></span> |

#### <a name="module-linker-for-cortex-m4-using-ac5"></a><span data-ttu-id="f8e6b-557">AC5 kullanarak Cortex için modül Bağlayıcısı-M4</span><span class="sxs-lookup"><span data-stu-id="f8e6b-557">Module linker for Cortex-M4 using AC5</span></span>

<span data-ttu-id="f8e6b-558">Örnek bağlayıcı dosyası sağlanmaz; bağlantı, komut satırında yapılır.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-558">No example linker file is provided; linking is done on the command line.</span></span> <span data-ttu-id="f8e6b-559">Sonraki bölüme bakın.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-559">See next section.</span></span>

#### <a name="building-modules-for-cortex-m4-using-ac5"></a><span data-ttu-id="f8e6b-560">AC5 kullanarak Cortex için modüller oluşturma-M4</span><span class="sxs-lookup"><span data-stu-id="f8e6b-560">Building Modules for Cortex-M4 using AC5</span></span>

<span data-ttu-id="f8e6b-561">Bkz. örnek build_threadx_module_demo.bat:</span><span class="sxs-lookup"><span data-stu-id="f8e6b-561">See example build_threadx_module_demo.bat:</span></span>

```dos
armasm -g --cpreproc --cpu=cortex-m4 --fpu=vfpv4 --apcs=/interwork/ropi/rwpi txm_module_preamble.S
armcc  -g --cpu=cortex-m4 --fpu=vfpv4 -c --apcs=/interwork/ropi/rwpi --lower_ropi -I../inc -I../../../../common_modules/inc -I../../../../common_modules/module_manager/inc -I../../../../common/inc sample_threadx_module.c
armlink -d -o sample_threadx_module.axf --elf --ro=0x30000 --rw=0x40000 --first txm_module_preamble.o(Init) --entry=_txm_module_thread_shell_entry --ropi --rwpi --remove --map --symbols --list sample_threadx_module.map txm_module_preamble.o sample_threadx_module.o txm.a
```

#### <a name="thread-extension-definition-for-cortex-m4-using-ac5"></a><span data-ttu-id="f8e6b-562">AC5 kullanarak Cortex için iş parçacığı uzantısı tanımı M4</span><span class="sxs-lookup"><span data-stu-id="f8e6b-562">Thread extension definition for Cortex-M4 using AC5</span></span>

```c
#define TX_THREAD_EXTENSION_2               VOID    *tx_thread_module_instance_ptr;         \
                                            VOID    *tx_thread_module_entry_info_ptr;       \
                                            ULONG   tx_thread_module_current_user_mode;     \
                                            ULONG   tx_thread_module_user_mode;             \
                                            ULONG   tx_thread_module_saved_lr;              \
                                            VOID    *tx_thread_module_kernel_stack_start;   \
                                            VOID    *tx_thread_module_kernel_stack_end;     \
                                            ULONG   tx_thread_module_kernel_stack_size;     \
                                            VOID    *tx_thread_module_stack_ptr;            \
                                            VOID    *tx_thread_module_stack_start;          \
                                            VOID    *tx_thread_module_stack_end;            \
                                            ULONG   tx_thread_module_stack_size;            \
                                            VOID    *tx_thread_module_reserved;
```

#### <a name="building-module-manager-for-cortex-m4-using-ac5"></a><span data-ttu-id="f8e6b-563">AC5 kullanarak Cortex için Modül Yöneticisi oluşturma-M4</span><span class="sxs-lookup"><span data-stu-id="f8e6b-563">Building Module Manager for Cortex-M4 using AC5</span></span>

<span data-ttu-id="f8e6b-564">Bkz. örnek build_threadx_module_manager_demo.bat:</span><span class="sxs-lookup"><span data-stu-id="f8e6b-564">See example build_threadx_module_manager_demo.bat:</span></span>

```dos
armasm -g --cpreproc --cpu=cortex-m4 --fpu=vfpv4 --apcs=/interwork tx_initialize_low_level.S
armcc -g --cpu=cortex-m4 --fpu=vfpv4 -c -I../inc -I../../../../common_modules/inc -I../../../../common_modules/module_manager/inc -I../../../../common/inc sample_threadx_module_manager.c
armlink -d -o sample_threadx_module_manager.axf --elf --ro 0x00000000 --first tx_initialize_low_level.o(RESET) --remove --map --symbols --list sample_threadx_module_manager.map tx_initialize_low_level.o sample_threadx_module_manager.o tx.a
```

#### <a name="attributes-for-external-memory-enable-api-for-cortex-m4-using-ac5"></a><span data-ttu-id="f8e6b-565">Dış bellek öznitelikleri M4 Cortex için API 'YI etkinleştirir-AC5 kullanarak</span><span class="sxs-lookup"><span data-stu-id="f8e6b-565">Attributes for external memory enable API for Cortex-M4 using AC5</span></span>

<span data-ttu-id="f8e6b-566">Modülün paylaşılan belleğe her zaman okuma erişimi vardır.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-566">Module always has read access to shared memory.</span></span>

| <span data-ttu-id="f8e6b-567">Öznitelik parametresi</span><span class="sxs-lookup"><span data-stu-id="f8e6b-567">Attribute parameter</span></span> | <span data-ttu-id="f8e6b-568">Anlamı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-568">Meaning</span></span> |
|---|---|
| <span data-ttu-id="f8e6b-569">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span><span class="sxs-lookup"><span data-stu-id="f8e6b-569">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span></span> | <span data-ttu-id="f8e6b-570">Yazma erişimi</span><span class="sxs-lookup"><span data-stu-id="f8e6b-570">Write access</span></span> |

### <a name="cortex-m4-using-ac6"></a><span data-ttu-id="f8e6b-571">Cortex-AC6 kullanarak M4</span><span class="sxs-lookup"><span data-stu-id="f8e6b-571">Cortex-M4 using AC6</span></span>

#### <a name="module-preamble-for-cortex-m4-using-ac6"></a><span data-ttu-id="f8e6b-572">AC6 kullanarak Cortex için modül girişi-M4</span><span class="sxs-lookup"><span data-stu-id="f8e6b-572">Module preamble for Cortex-M4 using AC6</span></span>

```armasm
    .text
    .align 4
    .syntax unified
    .section Init
    
    // Define public symbols
    .global __txm_module_preamble

    // Define application-specific start/stop entry points for the module
    .global demo_module_start

    // Define common external references
    .global  _txm_module_thread_shell_entry
    .global  _txm_module_callback_request_thread_entry

    .eabi_attribute Tag_ABI_PCS_RO_data, 1
    .eabi_attribute Tag_ABI_PCS_R9_use,  1
    .eabi_attribute Tag_ABI_PCS_RW_data, 2

__txm_module_preamble:
    .dc.l   0x4D4F4455                                          // Module ID
    .dc.l   0x6                                                 // Module Major Version
    .dc.l   0x1                                                 // Module Minor Version
    .dc.l   32                                                  // Module Preamble Size in 32-bit words
    .dc.l   0x12345678                                          // Module ID (application defined)
    .dc.l   0x01000007                                          // Module Properties where:
                                                                //   Bits 31-24: Compiler ID
                                                                //           0 -> IAR
                                                                //           1 -> ARM
                                                                //           2 -> GNU
                                                                //   Bit 0:  0 -> Privileged mode execution
                                                                //           1 -> User mode execution
                                                                //   Bit 1:  0 -> No MPU protection
                                                                //           1 -> MPU protection (must have user mode selected)
                                                                //   Bit 2:  0 -> Disable shared/external memory access
                                                                //           1 -> Enable shared/external memory access
    .dc.l   _txm_module_thread_shell_entry - __txm_module_preamble // Module Shell Entry Point
    .dc.l   demo_module_start - __txm_module_preamble           // Module Start Thread Entry Point
    .dc.l   0                                                   // Module Stop Thread Entry Point
    .dc.l   1                                                   // Module Start/Stop Thread Priority
    .dc.l   1024                                                // Module Start/Stop Thread Stack Size
    .dc.l   _txm_module_callback_request_thread_entry - __txm_module_preamble // Module Callback Thread Entry
    .dc.l   1                                                   // Module Callback Thread Priority
    .dc.l   1024                                                // Module Callback Thread Stack Size
    .dc.l   0x10000                                             // Module Code Size
    .dc.l   0x10000                                             // Module Data Size
    .dc.l   0                                                   // Reserved 0
    .dc.l   0                                                   // Reserved 1
    .dc.l   0                                                   // Reserved 2
    .dc.l   0                                                   // Reserved 3
    .dc.l   0                                                   // Reserved 4
    .dc.l   0                                                   // Reserved 5
    .dc.l   0                                                   // Reserved 6
    .dc.l   0                                                   // Reserved 7
    .dc.l   0                                                   // Reserved 8
    .dc.l   0                                                   // Reserved 9
    .dc.l   0                                                   // Reserved 10
    .dc.l   0                                                   // Reserved 11
    .dc.l   0                                                   // Reserved 12
    .dc.l   0                                                   // Reserved 13
    .dc.l   0                                                   // Reserved 14
    .dc.l   0                                                   // Reserved 15
```

#### <a name="module-properties-for-cortex-m4-using-ac6"></a><span data-ttu-id="f8e6b-573">AC6 kullanarak Cortex-M4 için modül özellikleri</span><span class="sxs-lookup"><span data-stu-id="f8e6b-573">Module properties for Cortex-M4 using AC6</span></span>

| <span data-ttu-id="f8e6b-574">Sürümleri</span><span class="sxs-lookup"><span data-stu-id="f8e6b-574">Bit</span></span> | <span data-ttu-id="f8e6b-575">Değer</span><span class="sxs-lookup"><span data-stu-id="f8e6b-575">Value</span></span> | <span data-ttu-id="f8e6b-576">Anlamı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-576">Meaning</span></span> |
|---|---|---|
| <span data-ttu-id="f8e6b-577">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-577">0</span></span> | <span data-ttu-id="f8e6b-578">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-578">0</span></span><br /><span data-ttu-id="f8e6b-579">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-579">1</span></span> | <span data-ttu-id="f8e6b-580">Ayrıcalıklı mod yürütme</span><span class="sxs-lookup"><span data-stu-id="f8e6b-580">Privileged mode execution</span></span><br /><span data-ttu-id="f8e6b-581">Kullanıcı modu yürütme</span><span class="sxs-lookup"><span data-stu-id="f8e6b-581">User mode execution</span></span> |
| <span data-ttu-id="f8e6b-582">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-582">1</span></span> | <span data-ttu-id="f8e6b-583">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-583">0</span></span><br /><span data-ttu-id="f8e6b-584">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-584">1</span></span> | <span data-ttu-id="f8e6b-585">MPU koruması yok</span><span class="sxs-lookup"><span data-stu-id="f8e6b-585">No MPU protection</span></span><br /><span data-ttu-id="f8e6b-586">MPU koruması (Kullanıcı modunun seçili olması gerekir)</span><span class="sxs-lookup"><span data-stu-id="f8e6b-586">MPU protection (must have user mode selected)</span></span> |
| <span data-ttu-id="f8e6b-587">2</span><span class="sxs-lookup"><span data-stu-id="f8e6b-587">2</span></span> | <span data-ttu-id="f8e6b-588">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-588">0</span></span><br /><span data-ttu-id="f8e6b-589">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-589">1</span></span> | <span data-ttu-id="f8e6b-590">Paylaşılan/dış bellek erişimini devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="f8e6b-590">Disable shared/external memory access</span></span><br /><span data-ttu-id="f8e6b-591">Paylaşılan/dış bellek erişimini etkinleştir</span><span class="sxs-lookup"><span data-stu-id="f8e6b-591">Enable shared/external memory access</span></span> |
| <span data-ttu-id="f8e6b-592">[23-3]</span><span class="sxs-lookup"><span data-stu-id="f8e6b-592">[23-3]</span></span> | <span data-ttu-id="f8e6b-593">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-593">0</span></span> | <span data-ttu-id="f8e6b-594">Ayrılmıştır</span><span class="sxs-lookup"><span data-stu-id="f8e6b-594">Reserved</span></span>
| <span data-ttu-id="f8e6b-595">[31-24]</span><span class="sxs-lookup"><span data-stu-id="f8e6b-595">[31-24]</span></span> | <br /><span data-ttu-id="f8e6b-596">-</span><span class="sxs-lookup"><span data-stu-id="f8e6b-596">0x00</span></span><br /><span data-ttu-id="f8e6b-597">0x01</span><span class="sxs-lookup"><span data-stu-id="f8e6b-597">0x01</span></span><br /><span data-ttu-id="f8e6b-598">0x02</span><span class="sxs-lookup"><span data-stu-id="f8e6b-598">0x02</span></span> | <span data-ttu-id="f8e6b-599">**Derleyici KIMLIĞI**</span><span class="sxs-lookup"><span data-stu-id="f8e6b-599">**Compiler ID**</span></span><br /><span data-ttu-id="f8e6b-600">IAR dili</span><span class="sxs-lookup"><span data-stu-id="f8e6b-600">IAR</span></span><br /><span data-ttu-id="f8e6b-601">ARM</span><span class="sxs-lookup"><span data-stu-id="f8e6b-601">ARM</span></span><br /><span data-ttu-id="f8e6b-602">GNU</span><span class="sxs-lookup"><span data-stu-id="f8e6b-602">GNU</span></span> |

#### <a name="module-linker-for-cortex-m4-using-ac6"></a><span data-ttu-id="f8e6b-603">AC6 kullanarak Cortex için modül Bağlayıcısı-M4</span><span class="sxs-lookup"><span data-stu-id="f8e6b-603">Module linker for Cortex-M4 using AC6</span></span>

<span data-ttu-id="f8e6b-604">Bağlayıcı dosyası kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-604">No linker file is used.</span></span> <span data-ttu-id="f8e6b-605">Bkz. proje ayarları.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-605">See project settings.</span></span>

#### <a name="building-modules-for-cortex-m4-using-ac6"></a><span data-ttu-id="f8e6b-606">AC6 kullanarak Cortex için modüller oluşturma-M4</span><span class="sxs-lookup"><span data-stu-id="f8e6b-606">Building Modules for Cortex-M4 using AC6</span></span>

<span data-ttu-id="f8e6b-607">Örnek çalışma alanı sağlanır.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-607">An example workspace is provided.</span></span> <span data-ttu-id="f8e6b-608">ThreadX kitaplığı, ThreadX modülleri kitaplığı, örnek Modül projesi ve örnek Module Manager projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-608">Build the ThreadX library, ThreadX Modules library, sample module project, and sample module manager project.</span></span>

#### <a name="thread-extension-definition-for-cortex-m4-using-ac6"></a><span data-ttu-id="f8e6b-609">AC6 kullanarak Cortex için iş parçacığı uzantısı tanımı M4</span><span class="sxs-lookup"><span data-stu-id="f8e6b-609">Thread extension definition for Cortex-M4 using AC6</span></span>

```c
#define TX_THREAD_EXTENSION_2               VOID    *tx_thread_module_instance_ptr;         \
                                            VOID    *tx_thread_module_entry_info_ptr;       \
                                            ULONG   tx_thread_module_current_user_mode;     \
                                            ULONG   tx_thread_module_user_mode;             \
                                            ULONG   tx_thread_module_saved_lr;              \
                                            VOID    *tx_thread_module_kernel_stack_start;   \
                                            VOID    *tx_thread_module_kernel_stack_end;     \
                                            ULONG   tx_thread_module_kernel_stack_size;     \
                                            VOID    *tx_thread_module_stack_ptr;            \
                                            VOID    *tx_thread_module_stack_start;          \
                                            VOID    *tx_thread_module_stack_end;            \
                                            ULONG   tx_thread_module_stack_size;            \
                                            VOID    *tx_thread_module_reserved;
```

#### <a name="building-module-manager-for-cortex-m4-using-ac6"></a><span data-ttu-id="f8e6b-610">AC6 kullanarak Cortex için Modül Yöneticisi oluşturma-M4</span><span class="sxs-lookup"><span data-stu-id="f8e6b-610">Building Module Manager for Cortex-M4 using AC6</span></span>

<span data-ttu-id="f8e6b-611">Örnek çalışma alanı sağlanır.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-611">An example workspace is provided.</span></span> <span data-ttu-id="f8e6b-612">ThreadX kitaplığı, ThreadX modülleri kitaplığı, örnek Modül projesi ve örnek Module Manager projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-612">Build the ThreadX library, ThreadX Modules library, sample module project, and sample module manager project.</span></span>

#### <a name="attributes-for-external-memory-enable-api-for-cortex-m4-using-ac6"></a><span data-ttu-id="f8e6b-613">Dış bellek öznitelikleri M4 Cortex için API 'YI etkinleştirir-AC6 kullanarak</span><span class="sxs-lookup"><span data-stu-id="f8e6b-613">Attributes for external memory enable API for Cortex-M4 using AC6</span></span>

<span data-ttu-id="f8e6b-614">Modülün paylaşılan belleğe her zaman okuma erişimi vardır.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-614">Module always has read access to shared memory.</span></span>

| <span data-ttu-id="f8e6b-615">Öznitelik parametresi</span><span class="sxs-lookup"><span data-stu-id="f8e6b-615">Attribute parameter</span></span> | <span data-ttu-id="f8e6b-616">Anlamı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-616">Meaning</span></span> |
|---|---|
| <span data-ttu-id="f8e6b-617">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span><span class="sxs-lookup"><span data-stu-id="f8e6b-617">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span></span> | <span data-ttu-id="f8e6b-618">Yazma erişimi</span><span class="sxs-lookup"><span data-stu-id="f8e6b-618">Write access</span></span> |

### <a name="cortex-m4-using-gnu"></a><span data-ttu-id="f8e6b-619">Cortex-GNU kullanarak M4</span><span class="sxs-lookup"><span data-stu-id="f8e6b-619">Cortex-M4 using GNU</span></span>

#### <a name="module-preamble-for-cortex-m4-using-gnu"></a><span data-ttu-id="f8e6b-620">GNU kullanarak Cortex için modül girişi-M4</span><span class="sxs-lookup"><span data-stu-id="f8e6b-620">Module preamble for Cortex-M4 using GNU</span></span>

```armasm
    .text
    .align 4
    .syntax unified

    /* Define public symbols.  */
    .global __txm_module_preamble

    /* Define application-specific start/stop entry points for the module.  */
    .global demo_module_start

    /* Define common external refrences.  */
    .global _txm_module_thread_shell_entry
    .global _txm_module_callback_request_thread_entry

__txm_module_preamble:
    .dc.l      0x4D4F4455                                       // Module ID
    .dc.l      0x6                                              // Module Major Version
    .dc.l      0x1                                              // Module Minor Version
    .dc.l      32                                               // Module Preamble Size in 32-bit words
    .dc.l      0x12345678                                       // Module ID (application defined)
    .dc.l      0x02000007                                       // Module Properties where:
                                                                //   Bits 31-24: Compiler ID
                                                                //           0 -> IAR
                                                                //           1 -> ARM
                                                                //           2 -> GNU
                                                                //   Bits 23-3: Reserved
                                                                //   Bit 2:  0 -> Disable shared/external memory access
                                                                //           1 -> Enable shared/external memory access
                                                                //   Bit 1:  0 -> No MPU protection
                                                                //           1 -> MPU protection (must have user mode selected - bit 0 set)
                                                                //   Bit 0:  0 -> Privileged mode execution
                                                                //           1 -> User mode execution
    .dc.l      _txm_module_thread_shell_entry - . - 0           // Module Shell Entry Point
    .dc.l      demo_module_start - . - 0                        // Module Start Thread Entry Point
    .dc.l      0                                                // Module Stop Thread Entry Point 
    .dc.l      1                                                // Module Start/Stop Thread Priority
    .dc.l      1024                                             // Module Start/Stop Thread Stack Size
    .dc.l      _txm_module_callback_request_thread_entry - . - 0 // Module Callback Thread Entry
    .dc.l      1                                                // Module Callback Thread Priority
    .dc.l      1024                                             // Module Callback Thread Stack Size
    .dc.l      __code_size__                                    // Module Code Size
    .dc.l      __data_size__                                    // Module Data Size
    .dc.l      0                                                // Reserved 0
    .dc.l      0                                                // Reserved 1
    .dc.l      0                                                // Reserved 2
    .dc.l      0                                                // Reserved 3
    .dc.l      0                                                // Reserved 4
    .dc.l      0                                                // Reserved 5
    .dc.l      0                                                // Reserved 6
    .dc.l      0                                                // Reserved 7
    .dc.l      0                                                // Reserved 8
    .dc.l      0                                                // Reserved 9
    .dc.l      0                                                // Reserved 10
    .dc.l      0                                                // Reserved 11
    .dc.l      0                                                // Reserved 12
    .dc.l      0                                                // Reserved 13
    .dc.l      0                                                // Reserved 14
    .dc.l      0                                                // Reserved 15
```

#### <a name="module-properties-for-cortex-m4-using-gnu"></a><span data-ttu-id="f8e6b-621">GNU kullanarak Cortex-M4 için modül özellikleri</span><span class="sxs-lookup"><span data-stu-id="f8e6b-621">Module properties for Cortex-M4 using GNU</span></span>

| <span data-ttu-id="f8e6b-622">Sürümleri</span><span class="sxs-lookup"><span data-stu-id="f8e6b-622">Bit</span></span> | <span data-ttu-id="f8e6b-623">Değer</span><span class="sxs-lookup"><span data-stu-id="f8e6b-623">Value</span></span> | <span data-ttu-id="f8e6b-624">Anlamı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-624">Meaning</span></span> |
|---|---|---|
| <span data-ttu-id="f8e6b-625">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-625">0</span></span> | <span data-ttu-id="f8e6b-626">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-626">0</span></span><br /><span data-ttu-id="f8e6b-627">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-627">1</span></span> | <span data-ttu-id="f8e6b-628">Ayrıcalıklı mod yürütme</span><span class="sxs-lookup"><span data-stu-id="f8e6b-628">Privileged mode execution</span></span><br /><span data-ttu-id="f8e6b-629">Kullanıcı modu yürütme</span><span class="sxs-lookup"><span data-stu-id="f8e6b-629">User mode execution</span></span> |
| <span data-ttu-id="f8e6b-630">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-630">1</span></span> | <span data-ttu-id="f8e6b-631">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-631">0</span></span><br /><span data-ttu-id="f8e6b-632">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-632">1</span></span> | <span data-ttu-id="f8e6b-633">MPU koruması yok</span><span class="sxs-lookup"><span data-stu-id="f8e6b-633">No MPU protection</span></span><br /><span data-ttu-id="f8e6b-634">MPU koruması (Kullanıcı modunun seçili olması gerekir)</span><span class="sxs-lookup"><span data-stu-id="f8e6b-634">MPU protection (must have user mode selected)</span></span> |
| <span data-ttu-id="f8e6b-635">2</span><span class="sxs-lookup"><span data-stu-id="f8e6b-635">2</span></span> | <span data-ttu-id="f8e6b-636">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-636">0</span></span><br /><span data-ttu-id="f8e6b-637">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-637">1</span></span> | <span data-ttu-id="f8e6b-638">Paylaşılan/dış bellek erişimini devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="f8e6b-638">Disable shared/external memory access</span></span><br /><span data-ttu-id="f8e6b-639">Paylaşılan/dış bellek erişimini etkinleştir</span><span class="sxs-lookup"><span data-stu-id="f8e6b-639">Enable shared/external memory access</span></span> |
| <span data-ttu-id="f8e6b-640">[23-3]</span><span class="sxs-lookup"><span data-stu-id="f8e6b-640">[23-3]</span></span> | <span data-ttu-id="f8e6b-641">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-641">0</span></span> | <span data-ttu-id="f8e6b-642">Ayrılmıştır</span><span class="sxs-lookup"><span data-stu-id="f8e6b-642">Reserved</span></span>
| <span data-ttu-id="f8e6b-643">[31-24]</span><span class="sxs-lookup"><span data-stu-id="f8e6b-643">[31-24]</span></span> | <br /><span data-ttu-id="f8e6b-644">-</span><span class="sxs-lookup"><span data-stu-id="f8e6b-644">0x00</span></span><br /><span data-ttu-id="f8e6b-645">0x01</span><span class="sxs-lookup"><span data-stu-id="f8e6b-645">0x01</span></span><br /><span data-ttu-id="f8e6b-646">0x02</span><span class="sxs-lookup"><span data-stu-id="f8e6b-646">0x02</span></span> | <span data-ttu-id="f8e6b-647">**Derleyici KIMLIĞI**</span><span class="sxs-lookup"><span data-stu-id="f8e6b-647">**Compiler ID**</span></span><br /><span data-ttu-id="f8e6b-648">IAR dili</span><span class="sxs-lookup"><span data-stu-id="f8e6b-648">IAR</span></span><br /><span data-ttu-id="f8e6b-649">ARM</span><span class="sxs-lookup"><span data-stu-id="f8e6b-649">ARM</span></span><br /><span data-ttu-id="f8e6b-650">GNU</span><span class="sxs-lookup"><span data-stu-id="f8e6b-650">GNU</span></span> |

#### <a name="module-linker-for-cortex-m4-using-gnu"></a><span data-ttu-id="f8e6b-651">GNU kullanarak Cortex için modül Bağlayıcısı-M4</span><span class="sxs-lookup"><span data-stu-id="f8e6b-651">Module linker for Cortex-M4 using GNU</span></span>

```c
MEMORY
{
  FLASH (rx) : ORIGIN = 0x00030000, LENGTH = 0x00010000
  RAM   (wx) : ORIGIN = 0, LENGTH = 0x00100000
}


SECTIONS
{
  __FLASH_segment_start__ = 0x00030000;
  __FLASH_segment_end__   = 0x00040000;
  __RAM_segment_start__   = 0;
  __RAM_segment_end__     = 0x8000;

  __HEAPSIZE__ = 128;

  __preamble_load_start__ = __FLASH_segment_start__;
  .preamble __FLASH_segment_start__ : AT(__FLASH_segment_start__)
  {
    __preamble_start__ = .;
    *(.preamble .preamble.*)
  }
  __preamble_end__ = __preamble_start__ + SIZEOF(.preamble);

  __dynsym_load_start__ =  ALIGN(__preamble_end__ , 4);
  .dynsym ALIGN(__dynsym_load_start__ , 4) : AT(ALIGN(__dynsym_load_start__ , 4))
  {
    . = ALIGN(4);
    KEEP (*(.dynsym))
    KEEP (*(.dynsym*))
    . = ALIGN(4);
  }
  __dynsym_end__ = __dynsym_load_start__ + SIZEOF(.dynsym);

  __dynstr_load_start__ =  ALIGN(__dynsym_end__ , 4);
  .dynstr ALIGN(__dynstr_load_start__ , 4) : AT(ALIGN(__dynstr_load_start__, 4))
  {
    . = ALIGN(4);
    KEEP (*(.dynstr))
    KEEP (*(.dynstr*))
    . = ALIGN(4);
  }
  __dynstr_end__ = __dynstr_load_start__ + SIZEOF(.dynstr);

  __reldyn_load_start__ =  ALIGN(__dynstr_end__ , 4);
  .rel.dyn ALIGN(__reldyn_load_start__ , 4) : AT(ALIGN(__reldyn_load_start__ , 4))
  {
    . = ALIGN(4);
    KEEP (*(.rel.dyn))
    KEEP (*(.rel.dyn*))
    . = ALIGN(4);
  }
  __reldyn_end__ = __reldyn_load_start__ + SIZEOF(.rel.dyn);

  __relplt_load_start__ =  ALIGN(__reldyn_end__ , 4);
  .rel.plt ALIGN(__relplt_load_start__ , 4) : AT(ALIGN(__relplt_load_start__ , 4))
  {
    . = ALIGN(4);
    KEEP (*(.rel.plt))
    KEEP (*(.rel.plt*))
    . = ALIGN(4);
  }
  __relplt_end__ = __relplt_load_start__ + SIZEOF(.rel.plt);

  __plt_load_start__ =  ALIGN(__relplt_end__ , 4);
  .plt ALIGN(__plt_load_start__ , 4) : AT(ALIGN(__plt_load_start__ , 4))
  {
    . = ALIGN(4);
    KEEP (*(.plt))
    KEEP (*(.plt*))
    . = ALIGN(4);
  }
  __plt_end__ = __plt_load_start__ + SIZEOF(.plt);

  __interp_load_start__ =  ALIGN(__plt_end__ , 4);
  .interp ALIGN(__interp_load_start__ , 4) : AT(ALIGN(__interp_load_start__ , 4))
  {
    . = ALIGN(4);
    KEEP (*(.interp))
    KEEP (*(.interp*))
    . = ALIGN(4);
  }
  __interp_end__ = __interp_load_start__ + SIZEOF(.interp);

  __hash_load_start__ =  ALIGN(__interp_end__ , 4);
  .hash ALIGN(__hash_load_start__ , 4) : AT(ALIGN(__hash_load_start__, 4))
  {
    . = ALIGN(4);
    KEEP (*(.hash))
    KEEP (*(.hash*))
    . = ALIGN(4);
  }
  __hash_end__ = __hash_load_start__ + SIZEOF(.hash);

  __text_load_start__ =  ALIGN(__hash_end__ , 4);
  .text ALIGN(__text_load_start__ , 4) : AT(ALIGN(__text_load_start__, 4))
  {
    __text_start__ = .;
    *(.text .text.* .glue_7t .glue_7 .gnu.linkonce.t.* .gcc_except_table  )
  }
  __text_end__ = __text_start__ + SIZEOF(.text);

  __dtors_load_start__ = ALIGN(__text_end__ , 4);
  .dtors ALIGN(__text_end__ , 4) : AT(ALIGN(__text_end__ , 4))
  {
    __dtors_start__ = .;
    KEEP (*(SORT(.dtors.*))) KEEP (*(.dtors))
  }
  __dtors_end__ = __dtors_start__ + SIZEOF(.dtors);

  __ctors_load_start__ = ALIGN(__dtors_end__ , 4);
  .ctors ALIGN(__dtors_end__ , 4) : AT(ALIGN(__dtors_end__ , 4))
  {
    __ctors_start__ = .;
    KEEP (*(SORT(.ctors.*))) KEEP (*(.ctors))
  }
  __ctors_end__ = __ctors_start__ + SIZEOF(.ctors);

  __got_load_start__ = ALIGN(__ctors_end__ , 4);
  .got ALIGN(__ctors_end__ , 4) : AT(ALIGN(__ctors_end__ , 4))
  {
    . = ALIGN(4);
    _sgot = .;
    KEEP (*(.got))
    KEEP (*(.got*))
    . = ALIGN(4);
    _egot = .;
  } 
  __got_end__ =  __got_load_start__ + SIZEOF(.got);

  __rodata_load_start__ = ALIGN(__got_end__ , 4);
  .rodata ALIGN(__got_end__ , 4) : AT(ALIGN(__got_end__ , 4))
  {
    __rodata_start__ = .;
    *(.rodata .rodata.* .gnu.linkonce.r.*)
  }
  __rodata_end__ = __rodata_start__ + SIZEOF(.rodata);
 
  __code_size__ =  __rodata_end__ - __FLASH_segment_start__;

  __fast_load_start__ = ALIGN(__rodata_end__ , 4);

  __fast_load_end__ = __fast_load_start__ + SIZEOF(.fast);

  __new_got_start__ = ALIGN(__RAM_segment_start__ , 4);

  __new_got_end__ =  __new_got_start__ + SIZEOF(.got);

  .fast ALIGN(__new_got_end__ , 4) : AT(ALIGN(__rodata_end__ , 4))
  {
    __fast_start__ = .;
    *(.fast .fast.*)
  }
  __fast_end__ = __fast_start__ + SIZEOF(.fast);

  .fast_run ALIGN(__fast_end__ , 4) (NOLOAD) :
  {
    __fast_run_start__ = .;
    . = MAX(__fast_run_start__ + SIZEOF(.fast), .);
  }
  __fast_run_end__ = __fast_run_start__ + SIZEOF(.fast_run);

  __data_load_start__ = ALIGN(__fast_load_start__ + SIZEOF(.fast) , 4);
  .data ALIGN(__fast_run_end__ , 4) : AT(ALIGN(__fast_load_start__ + SIZEOF(.fast) , 4))
  {
    __data_start__ = .;
    *(.data .data.* .gnu.linkonce.d.*)
  }
  __data_end__ = __data_start__ + SIZEOF(.data);

  __data_load_end__ = __data_load_start__ + SIZEOF(.data);

  __FLASH_segment_used_end__ = ALIGN(__fast_load_start__ + SIZEOF(.fast) , 4) + SIZEOF(.data);

  .data_run ALIGN(__fast_run_end__ , 4) (NOLOAD) :
  {
    __data_run_start__ = .;
    . = MAX(__data_run_start__ + SIZEOF(.data), .);
  }
  __data_run_end__ = __data_run_start__ + SIZEOF(.data_run);

  __bss_load_start__ = ALIGN(__data_run_end__ , 4);
  .bss ALIGN(__data_run_end__ , 4) (NOLOAD) : AT(ALIGN(__data_run_end__ , 4))
  {
    __bss_start__ = .;
    *(.bss .bss.* .gnu.linkonce.b.*) *(COMMON)
  }
  __bss_end__ = __bss_start__ + SIZEOF(.bss);

  __non_init_load_start__ = ALIGN(__bss_end__ , 4);
  .non_init ALIGN(__bss_end__ , 4) (NOLOAD) : AT(ALIGN(__bss_end__ , 4))
  {
    __non_init_start__ = .;
    *(.non_init .non_init.*)
  }
  __non_init_end__ = __non_init_start__ + SIZEOF(.non_init);

  __heap_load_start__ = ALIGN(__non_init_end__ , 4);
  .heap ALIGN(__non_init_end__ , 4) (NOLOAD) : AT(ALIGN(__non_init_end__ , 4))
  {
    __heap_start__ = .;
    *(.heap)
    . = ALIGN(MAX(__heap_start__ + __HEAPSIZE__ , .), 4);
  }
  __heap_end__ = __heap_start__ + SIZEOF(.heap);

  __data_size__ =  __heap_end__ - __RAM_segment_start__;

}
```

#### <a name="building-modules-for-cortex-m4-using-gnu"></a><span data-ttu-id="f8e6b-652">GNU kullanarak Cortex için modüller oluşturma-M4</span><span class="sxs-lookup"><span data-stu-id="f8e6b-652">Building Modules for Cortex-M4 using GNU</span></span>

<span data-ttu-id="f8e6b-653">build_threadx_module_sample.bat bkz:</span><span class="sxs-lookup"><span data-stu-id="f8e6b-653">See build_threadx_module_sample.bat:</span></span>

```dos
arm-none-eabi-gcc -c -g -mcpu=cortex-m4 -mfloat-abi=hard -mfpu=vfpv4 -fpie -fno-plt -mpic-data-is-text-relative -msingle-pic-base txm_module_preamble.s
arm-none-eabi-gcc -c -g -mcpu=cortex-m4 -mfloat-abi=hard -mfpu=vfpv4 -fpie -fno-plt -mpic-data-is-text-relative -msingle-pic-base gcc_setup.S
arm-none-eabi-gcc -c -g -mcpu=cortex-m4 -mfloat-abi=hard -mfpu=vfpv4 -fpie -fno-plt -mpic-data-is-text-relative -msingle-pic-base -I..\inc -I..\..\..\..\common\inc -I..\..\..\..\common_modules\inc sample_threadx_module.c
arm-none-eabi-ld -A cortex-m4 -T sample_threadx_module.ld txm_module_preamble.o gcc_setup.o sample_threadx_module.o -e _txm_module_thread_shell_entry txm.a -o sample_threadx_module.axf -M > sample_threadx_module.map
```

#### <a name="thread-extension-definition-for-cortex-m4-using-gnu"></a><span data-ttu-id="f8e6b-654">GNU kullanarak Cortex-M4 için iş parçacığı uzantısı tanımı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-654">Thread extension definition for Cortex-M4 using GNU</span></span>

```c
#define TX_THREAD_EXTENSION_2               VOID    *tx_thread_module_instance_ptr;         \
                                            VOID    *tx_thread_module_entry_info_ptr;       \
                                            ULONG   tx_thread_module_current_user_mode;     \
                                            ULONG   tx_thread_module_user_mode;             \
                                            ULONG   tx_thread_module_saved_lr;              \
                                            VOID    *tx_thread_module_kernel_stack_start;   \
                                            VOID    *tx_thread_module_kernel_stack_end;     \
                                            ULONG   tx_thread_module_kernel_stack_size;     \
                                            VOID    *tx_thread_module_stack_ptr;            \
                                            VOID    *tx_thread_module_stack_start;          \
                                            VOID    *tx_thread_module_stack_end;            \
                                            ULONG   tx_thread_module_stack_size;            \
                                            VOID    *tx_thread_module_reserved;
```

#### <a name="building-module-manager-for-cortex-m4-using-gnu"></a><span data-ttu-id="f8e6b-655">GNU kullanarak Cortex için Modül Yöneticisi oluşturma-M4</span><span class="sxs-lookup"><span data-stu-id="f8e6b-655">Building Module Manager for Cortex-M4 using GNU</span></span>

<span data-ttu-id="f8e6b-656">build_threadx_module_manager_sample.bat bkz:</span><span class="sxs-lookup"><span data-stu-id="f8e6b-656">See build_threadx_module_manager_sample.bat:</span></span>

```dos
arm-none-eabi-gcc -c -g -mcpu=cortex-m4 -mfloat-abi=hard -mfpu=vfpv4 -mthumb cortexm_vectors.S
arm-none-eabi-gcc -c -g -mcpu=cortex-m4 -mfloat-abi=hard -mfpu=vfpv4 -mthumb cortexm_crt0.S
arm-none-eabi-gcc -c -g -mcpu=cortex-m4 -mfloat-abi=hard -mfpu=vfpv4 -mthumb tx_initialize_low_level.S
arm-none-eabi-gcc -c -g -mcpu=cortex-m4 -mfloat-abi=hard -mfpu=vfpv4 -mthumb -I..\inc -I..\..\..\..\common\inc -I..\..\..\..\common_modules\inc sample_threadx_module_manager.c
arm-none-eabi-gcc -g -mcpu=cortex-m4 -mfloat-abi=hard -mfpu=vfpv4 -mthumb -T sample_threadx.ld -ereset_handler -nostartfiles -o sample_threadx_module_manager.out -Wl,-Map=sample_threadx_module_manager.map cortexm_vectors.o cortexm_crt0.o tx_initialize_low_level.o sample_threadx_module_manager.o tx.a
```

#### <a name="attributes-for-external-memory-enable-api-for-cortex-m4-using-gnu"></a><span data-ttu-id="f8e6b-657">Dış bellek öznitelikleri, GNU kullanarak Cortex için API 'YI etkinleştirir-M4</span><span class="sxs-lookup"><span data-stu-id="f8e6b-657">Attributes for external memory enable API for Cortex-M4 using GNU</span></span>

<span data-ttu-id="f8e6b-658">Modülün paylaşılan belleğe her zaman okuma erişimi vardır.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-658">Module always has read access to shared memory.</span></span>

| <span data-ttu-id="f8e6b-659">Öznitelik parametresi</span><span class="sxs-lookup"><span data-stu-id="f8e6b-659">Attribute parameter</span></span> | <span data-ttu-id="f8e6b-660">Anlamı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-660">Meaning</span></span> |
|---|---|
| <span data-ttu-id="f8e6b-661">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span><span class="sxs-lookup"><span data-stu-id="f8e6b-661">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span></span> | <span data-ttu-id="f8e6b-662">Yazma erişimi</span><span class="sxs-lookup"><span data-stu-id="f8e6b-662">Write access</span></span> |

### <a name="cortex-m4-using-iar"></a><span data-ttu-id="f8e6b-663">Cortex-ıAR kullanarak M4</span><span class="sxs-lookup"><span data-stu-id="f8e6b-663">Cortex-M4 using IAR</span></span>

#### <a name="module-preamble-for-cortex-m4-using-iar"></a><span data-ttu-id="f8e6b-664">IAR kullanarak Cortex için modül girişi-M4</span><span class="sxs-lookup"><span data-stu-id="f8e6b-664">Module preamble for Cortex-M4 using IAR</span></span>

```c
    SECTION .text:CODE

    AAPCS INTERWORK, ROPI, RWPI_COMPATIBLE,  VFP_COMPATIBLE
    PRESERVE8

    /* Define public symbols.  */

    PUBLIC __txm_module_preamble


    /* Define application-specific start/stop entry points for the module.  */

    EXTERN demo_module_start


    /* Define common external references.  */

    EXTERN  _txm_module_thread_shell_entry
    EXTERN  _txm_module_callback_request_thread_entry
    EXTERN  ROPI$$Length
    EXTERN  RWPI$$Length

    DATA
__txm_module_preamble:
    DC32      0x4D4F4455                                        ; Module ID
    DC32      0x5                                               ; Module Major Version
    DC32      0x6                                               ; Module Minor Version
    DC32      32                                                ; Module Preamble Size in 32-bit words
    DC32      0x12345678                                        ; Module ID (application defined)
    DC32      0x00000007                                        ; Module Properties where:
                                                                ;   Bits 31-24: Compiler ID
                                                                ;           0 -> IAR
                                                                ;           1 -> ARM
                                                                ;           2 -> GNU
                                                                ;   Bits 23-3: Reserved
                                                                ;   Bit 2:  0 -> Disable shared/external memory access
                                                                ;           1 -> Enable shared/external memory access
                                                                ;   Bit 1:  0 -> No MPU protection
                                                                ;           1 -> MPU protection (must have user mode selected - bit 0 set)
                                                                ;   Bit 0:  0 -> Privileged mode execution
                                                                ;           1 -> User mode execution


    DC32      _txm_module_thread_shell_entry - . - 0            ; Module Shell Entry Point
    DC32      demo_module_start - . - 0                         ; Module Start Thread Entry Point
    DC32      0                                                 ; Module Stop Thread Entry Point
    DC32      1                                                 ; Module Start/Stop Thread Priority
    DC32      1024                                              ; Module Start/Stop Thread Stack Size
    DC32      _txm_module_callback_request_thread_entry - . - 0 ; Module Callback Thread Entry
    DC32      1                                                 ; Module Callback Thread Priority
    DC32      1024                                              ; Module Callback Thread Stack Size
    DC32      ROPI$$Length                                      ; Module Code Size
    DC32      RWPI$$Length                                      ; Module Data Size
    DC32      0                                                 ; Reserved 0
    DC32      0                                                 ; Reserved 1
    DC32      0                                                 ; Reserved 2
    DC32      0                                                 ; Reserved 3
    DC32      0                                                 ; Reserved 4
    DC32      0                                                 ; Reserved 5
    DC32      0                                                 ; Reserved 6
    DC32      0                                                 ; Reserved 7
    DC32      0                                                 ; Reserved 8  
    DC32      0                                                 ; Reserved 9
    DC32      0                                                 ; Reserved 10
    DC32      0                                                 ; Reserved 11
    DC32      0                                                 ; Reserved 12
    DC32      0                                                 ; Reserved 13
    DC32      0                                                 ; Reserved 14
    DC32      0                                                 ; Reserved 15

    END
```

#### <a name="module-properties-for-cortex-m4-using-iar"></a><span data-ttu-id="f8e6b-665">IAR kullanarak Cortex-M4 için modül özellikleri</span><span class="sxs-lookup"><span data-stu-id="f8e6b-665">Module properties for Cortex-M4 using IAR</span></span>

| <span data-ttu-id="f8e6b-666">Sürümleri</span><span class="sxs-lookup"><span data-stu-id="f8e6b-666">Bit</span></span> | <span data-ttu-id="f8e6b-667">Değer</span><span class="sxs-lookup"><span data-stu-id="f8e6b-667">Value</span></span> | <span data-ttu-id="f8e6b-668">Anlamı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-668">Meaning</span></span> |
|---|---|---|
| <span data-ttu-id="f8e6b-669">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-669">0</span></span> | <span data-ttu-id="f8e6b-670">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-670">0</span></span><br /><span data-ttu-id="f8e6b-671">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-671">1</span></span> | <span data-ttu-id="f8e6b-672">Ayrıcalıklı mod yürütme</span><span class="sxs-lookup"><span data-stu-id="f8e6b-672">Privileged mode execution</span></span><br /><span data-ttu-id="f8e6b-673">Kullanıcı modu yürütme</span><span class="sxs-lookup"><span data-stu-id="f8e6b-673">User mode execution</span></span> |
| <span data-ttu-id="f8e6b-674">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-674">1</span></span> | <span data-ttu-id="f8e6b-675">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-675">0</span></span><br /><span data-ttu-id="f8e6b-676">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-676">1</span></span> | <span data-ttu-id="f8e6b-677">MPU koruması yok</span><span class="sxs-lookup"><span data-stu-id="f8e6b-677">No MPU protection</span></span><br /><span data-ttu-id="f8e6b-678">MPU koruması (Kullanıcı modunun seçili olması gerekir)</span><span class="sxs-lookup"><span data-stu-id="f8e6b-678">MPU protection (must have user mode selected)</span></span> |
| <span data-ttu-id="f8e6b-679">2</span><span class="sxs-lookup"><span data-stu-id="f8e6b-679">2</span></span> | <span data-ttu-id="f8e6b-680">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-680">0</span></span><br /><span data-ttu-id="f8e6b-681">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-681">1</span></span> | <span data-ttu-id="f8e6b-682">Paylaşılan/dış bellek erişimini devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="f8e6b-682">Disable shared/external memory access</span></span><br /><span data-ttu-id="f8e6b-683">Paylaşılan/dış bellek erişimini etkinleştir</span><span class="sxs-lookup"><span data-stu-id="f8e6b-683">Enable shared/external memory access</span></span> |
| <span data-ttu-id="f8e6b-684">[23-3]</span><span class="sxs-lookup"><span data-stu-id="f8e6b-684">[23-3]</span></span> | <span data-ttu-id="f8e6b-685">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-685">0</span></span> | <span data-ttu-id="f8e6b-686">Ayrılmıştır</span><span class="sxs-lookup"><span data-stu-id="f8e6b-686">Reserved</span></span>
| <span data-ttu-id="f8e6b-687">[31-24]</span><span class="sxs-lookup"><span data-stu-id="f8e6b-687">[31-24]</span></span> | <br /><span data-ttu-id="f8e6b-688">-</span><span class="sxs-lookup"><span data-stu-id="f8e6b-688">0x00</span></span><br /><span data-ttu-id="f8e6b-689">0x01</span><span class="sxs-lookup"><span data-stu-id="f8e6b-689">0x01</span></span><br /><span data-ttu-id="f8e6b-690">0x02</span><span class="sxs-lookup"><span data-stu-id="f8e6b-690">0x02</span></span> | <span data-ttu-id="f8e6b-691">**Derleyici KIMLIĞI**</span><span class="sxs-lookup"><span data-stu-id="f8e6b-691">**Compiler ID**</span></span><br /><span data-ttu-id="f8e6b-692">IAR dili</span><span class="sxs-lookup"><span data-stu-id="f8e6b-692">IAR</span></span><br /><span data-ttu-id="f8e6b-693">ARM</span><span class="sxs-lookup"><span data-stu-id="f8e6b-693">ARM</span></span><br /><span data-ttu-id="f8e6b-694">GNU</span><span class="sxs-lookup"><span data-stu-id="f8e6b-694">GNU</span></span> |

#### <a name="module-linker-for-cortex-m4-using-iar"></a><span data-ttu-id="f8e6b-695">IAR kullanarak Cortex için modül Bağlayıcısı-M4</span><span class="sxs-lookup"><span data-stu-id="f8e6b-695">Module linker for Cortex-M4 using IAR</span></span>

```c
/*###ICF### Section handled by ICF editor, don't touch! ****/
/*-Editor annotation file-*/
/* IcfEditorFile="$TOOLKIT_DIR$\config\ide\IcfEditor\a_v1_0.xml" */
/*-Specials-*/
define symbol __ICFEDIT_intvec_start__ = 0x0;
/*-Memory Regions-*/
define symbol __ICFEDIT_region_ROM_start__ = 0x080f0000;
define symbol __ICFEDIT_region_ROM_end__   = 0x080fffff;
define symbol __ICFEDIT_region_RAM_start__ = 0x64002800;
define symbol __ICFEDIT_region_RAM_end__   = 0x64100000;
/*-Sizes-*/
define symbol __ICFEDIT_size_cstack__   = 0;
define symbol __ICFEDIT_size_svcstack__ = 0;
define symbol __ICFEDIT_size_irqstack__ = 0;
define symbol __ICFEDIT_size_fiqstack__ = 0;
define symbol __ICFEDIT_size_undstack__ = 0;
define symbol __ICFEDIT_size_abtstack__ = 0;
define symbol __ICFEDIT_size_heap__     = 0x1000;
/**** End of ICF editor section. ###ICF###*/

define memory mem with size = 4G;
define region ROM_region   = mem:[from __ICFEDIT_region_ROM_start__   to __ICFEDIT_region_ROM_end__];
define region RAM_region   = mem:[from __ICFEDIT_region_RAM_start__   to __ICFEDIT_region_RAM_end__];

//define block CSTACK    with alignment = 8, size = __ICFEDIT_size_cstack__   { };
//define block SVC_STACK with alignment = 8, size = __ICFEDIT_size_svcstack__ { };
//define block IRQ_STACK with alignment = 8, size = __ICFEDIT_size_irqstack__ { };
//define block FIQ_STACK with alignment = 8, size = __ICFEDIT_size_fiqstack__ { };
//define block UND_STACK with alignment = 8, size = __ICFEDIT_size_undstack__ { };
//define block ABT_STACK with alignment = 8, size = __ICFEDIT_size_abtstack__ { };
define block HEAP      with alignment = 8, size = __ICFEDIT_size_heap__     { };

initialize by copy { readwrite };
do not initialize  { section .noinit };

//place at address mem:__ICFEDIT_intvec_start__ { readonly section .intvec };

define movable block ROPI with alignment = 4, fixed order
{
  ro object txm_module_preamble_stm32f4xx.o,
  ro,
  ro data
};

define movable block RWPI with alignment = 8, fixed order, static base
{
  rw,
  block HEAP
};

place in ROM_region   { block ROPI };
place in RAM_region   { block RWPI };
```

#### <a name="building-modules-for-cortex-m4-using-iar"></a><span data-ttu-id="f8e6b-696">IAR kullanarak Cortex için modüller oluşturma-M4</span><span class="sxs-lookup"><span data-stu-id="f8e6b-696">Building Modules for Cortex-M4 using IAR</span></span>

<span data-ttu-id="f8e6b-697">Örnek çalışma alanı sağlanır.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-697">An example workspace is provided.</span></span> <span data-ttu-id="f8e6b-698">ThreadX kitaplığı, ThreadX modülleri kitaplığı, demo modülü projesi ve tanıtım modülü Yöneticisi projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-698">Build the ThreadX library, ThreadX Modules library, demo module project, and demo module manager project.</span></span>

#### <a name="thread-extension-definition-for-cortex-m4-using-iar"></a><span data-ttu-id="f8e6b-699">IAR kullanarak Cortex-M4 için iş parçacığı uzantısı tanımı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-699">Thread extension definition for Cortex-M4 using IAR</span></span>

```c
#define TX_THREAD_EXTENSION_2   VOID    *tx_thread_module_instance_ptr;         \
                                VOID    *tx_thread_module_entry_info_ptr;       \
                                ULONG   tx_thread_module_current_user_mode;     \
                                ULONG   tx_thread_module_user_mode;             \
                                ULONG   tx_thread_module_saved_lr;              \
                                VOID    *tx_thread_module_kernel_stack_start;   \
                                VOID    *tx_thread_module_kernel_stack_end;     \
                                ULONG   tx_thread_module_kernel_stack_size;     \
                                VOID    *tx_thread_module_stack_ptr;            \
                                VOID    *tx_thread_module_stack_start;          \
                                VOID    *tx_thread_module_stack_end;            \
                                ULONG   tx_thread_module_stack_size;            \
                                VOID    *tx_thread_module_reserved;             \
                                VOID    *tx_thread_iar_tls_pointer;
```

#### <a name="building-module-manager-for-cortex-m4-using-iar"></a><span data-ttu-id="f8e6b-700">IAR kullanarak Cortex için Modül Yöneticisi oluşturma-M4</span><span class="sxs-lookup"><span data-stu-id="f8e6b-700">Building Module Manager for Cortex-M4 using IAR</span></span>

<span data-ttu-id="f8e6b-701">Örnek çalışma alanı sağlanır.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-701">An example workspace is provided.</span></span> <span data-ttu-id="f8e6b-702">ThreadX kitaplığı, ThreadX modülleri kitaplığı, demo modülü projesi ve tanıtım modülü Yöneticisi projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-702">Build the ThreadX library, ThreadX Modules library, demo module project, and demo module manager project.</span></span>

#### <a name="attributes-for-external-memory-enable-api-for-cortex-m4-using-iar"></a><span data-ttu-id="f8e6b-703">Dış bellek öznitelikleri ıAR kullanarak Cortex için API 'YI etkinleştirir-M4</span><span class="sxs-lookup"><span data-stu-id="f8e6b-703">Attributes for external memory enable API for Cortex-M4 using IAR</span></span>

<span data-ttu-id="f8e6b-704">Modülün paylaşılan belleğe her zaman okuma erişimi vardır.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-704">Module always has read access to shared memory.</span></span>

| <span data-ttu-id="f8e6b-705">Öznitelik parametresi</span><span class="sxs-lookup"><span data-stu-id="f8e6b-705">Attribute parameter</span></span> | <span data-ttu-id="f8e6b-706">Anlamı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-706">Meaning</span></span> |
|---|---|
| <span data-ttu-id="f8e6b-707">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span><span class="sxs-lookup"><span data-stu-id="f8e6b-707">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span></span> | <span data-ttu-id="f8e6b-708">Yazma erişimi</span><span class="sxs-lookup"><span data-stu-id="f8e6b-708">Write access</span></span> |

## <a name="cortex-m7-processor"></a><span data-ttu-id="f8e6b-709">Cortex-M7 işlemcisi</span><span class="sxs-lookup"><span data-stu-id="f8e6b-709">Cortex-M7 processor</span></span>

### <a name="cortex-m7-using-ac5"></a><span data-ttu-id="f8e6b-710">Cortex-AC5 kullanarak M7</span><span class="sxs-lookup"><span data-stu-id="f8e6b-710">Cortex-M7 using AC5</span></span>

#### <a name="module-preamble-for-cortex-m7-using-ac5"></a><span data-ttu-id="f8e6b-711">AC5 kullanarak Cortex için modül girişi-M7</span><span class="sxs-lookup"><span data-stu-id="f8e6b-711">Module preamble for Cortex-M7 using AC5</span></span>

```c
    AREA Init, CODE, READONLY

    PRESERVE8

    ; Define public symbols

    EXPORT __txm_module_preamble


    ; Define application-specific start/stop entry points for the module

    EXTERN demo_module_start


    ; Define common external references

    IMPORT  _txm_module_thread_shell_entry
    IMPORT  _txm_module_callback_request_thread_entry
    IMPORT  |Image$$ER_RO$$Length|
    IMPORT  |Image$$ER_RW$$Length|
    IMPORT  |Image$$ER_RW$$RW$$Length|
    IMPORT  |Image$$ER_RW$$ZI$$Length|
    IMPORT  |Image$$ER_ZI$$ZI$$Length|

__txm_module_preamble
    DCD     0x4D4F4455                                          ; Module ID
    DCD     0x5                                                 ; Module Major Version
    DCD     0x6                                                 ; Module Minor Version
    DCD     32                                                  ; Module Preamble Size in 32-bit words
    DCD     0x12345678                                          ; Module ID (application defined)
    DCD     0x01000007                                          ; Module Properties where:
                                                                ;   Bits 31-24: Compiler ID
                                                                ;           0 -> IAR
                                                                ;           1 -> ARM
                                                                ;           2 -> GNU
                                                                ;   Bit 0:  0 -> Privileged mode execution
                                                                ;           1 -> User mode execution
                                                                ;   Bit 1:  0 -> No MPU protection
                                                                ;           1 -> MPU protection (must have user mode selected)
                                                                ;   Bit 2:  0 -> Disable shared/external memory access
                                                                ;           1 -> Enable shared/external memory access
    DCD     _txm_module_thread_shell_entry - __txm_module_preamble              ; Module Shell Entry Point
    DCD     demo_module_start - __txm_module_preamble           ; Module Start Thread Entry Point
    DCD     0                                                   ; Module Stop Thread Entry Point
    DCD     1                                                   ; Module Start/Stop Thread Priority
    DCD     1024                                                ; Module Start/Stop Thread Stack Size
    DCD     _txm_module_callback_request_thread_entry - __txm_module_preamble   ; Module Callback Thread Entry
    DCD     1                                                   ; Module Callback Thread Priority
    DCD     1024                                                ; Module Callback Thread Stack Size
    DCD     |Image$$ER_RO$$Length| + |Image$$ER_RW$$Length|         ; Module Code Size
    DCD     |Image$$ER_RW$$Length| + |Image$$ER_ZI$$ZI$$Length| ; Module Data Size
    DCD     0                                                   ; Reserved 0
    DCD     0                                                   ; Reserved 1
    DCD     0                                                   ; Reserved 2
    DCD     0                                                   ; Reserved 3
    DCD     0                                                   ; Reserved 4
    DCD     0                                                   ; Reserved 5
    DCD     0                                                   ; Reserved 6
    DCD     0                                                   ; Reserved 7
    DCD     0                                                   ; Reserved 8
    DCD     0                                                   ; Reserved 9
    DCD     0                                                   ; Reserved 10
    DCD     0                                                   ; Reserved 11
    DCD     0                                                   ; Reserved 12
    DCD     0                                                   ; Reserved 13
    DCD     0                                                   ; Reserved 14
    DCD     0                                                   ; Reserved 15

    END
```

#### <a name="module-properties-for-cortex-m7-using-ac5"></a><span data-ttu-id="f8e6b-712">AC5 kullanarak Cortex-M7 için modül özellikleri</span><span class="sxs-lookup"><span data-stu-id="f8e6b-712">Module properties for Cortex-M7 using AC5</span></span>

| <span data-ttu-id="f8e6b-713">Sürümleri</span><span class="sxs-lookup"><span data-stu-id="f8e6b-713">Bit</span></span> | <span data-ttu-id="f8e6b-714">Değer</span><span class="sxs-lookup"><span data-stu-id="f8e6b-714">Value</span></span> | <span data-ttu-id="f8e6b-715">Anlamı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-715">Meaning</span></span> |
|---|---|---|
| <span data-ttu-id="f8e6b-716">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-716">0</span></span> | <span data-ttu-id="f8e6b-717">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-717">0</span></span><br /><span data-ttu-id="f8e6b-718">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-718">1</span></span> | <span data-ttu-id="f8e6b-719">Ayrıcalıklı mod yürütme</span><span class="sxs-lookup"><span data-stu-id="f8e6b-719">Privileged mode execution</span></span><br /><span data-ttu-id="f8e6b-720">Kullanıcı modu yürütme</span><span class="sxs-lookup"><span data-stu-id="f8e6b-720">User mode execution</span></span> |
| <span data-ttu-id="f8e6b-721">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-721">1</span></span> | <span data-ttu-id="f8e6b-722">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-722">0</span></span><br /><span data-ttu-id="f8e6b-723">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-723">1</span></span> | <span data-ttu-id="f8e6b-724">MPU koruması yok</span><span class="sxs-lookup"><span data-stu-id="f8e6b-724">No MPU protection</span></span><br /><span data-ttu-id="f8e6b-725">MPU koruması (Kullanıcı modunun seçili olması gerekir)</span><span class="sxs-lookup"><span data-stu-id="f8e6b-725">MPU protection (must have user mode selected)</span></span> |
| <span data-ttu-id="f8e6b-726">2</span><span class="sxs-lookup"><span data-stu-id="f8e6b-726">2</span></span> | <span data-ttu-id="f8e6b-727">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-727">0</span></span><br /><span data-ttu-id="f8e6b-728">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-728">1</span></span> | <span data-ttu-id="f8e6b-729">Paylaşılan/dış bellek erişimini devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="f8e6b-729">Disable shared/external memory access</span></span><br /><span data-ttu-id="f8e6b-730">Paylaşılan/dış bellek erişimini etkinleştir</span><span class="sxs-lookup"><span data-stu-id="f8e6b-730">Enable shared/external memory access</span></span> |
| <span data-ttu-id="f8e6b-731">[23-3]</span><span class="sxs-lookup"><span data-stu-id="f8e6b-731">[23-3]</span></span> | <span data-ttu-id="f8e6b-732">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-732">0</span></span> | <span data-ttu-id="f8e6b-733">Ayrılmıştır</span><span class="sxs-lookup"><span data-stu-id="f8e6b-733">Reserved</span></span>
| <span data-ttu-id="f8e6b-734">[31-24]</span><span class="sxs-lookup"><span data-stu-id="f8e6b-734">[31-24]</span></span> | <br /><span data-ttu-id="f8e6b-735">-</span><span class="sxs-lookup"><span data-stu-id="f8e6b-735">0x00</span></span><br /><span data-ttu-id="f8e6b-736">0x01</span><span class="sxs-lookup"><span data-stu-id="f8e6b-736">0x01</span></span><br /><span data-ttu-id="f8e6b-737">0x02</span><span class="sxs-lookup"><span data-stu-id="f8e6b-737">0x02</span></span> | <span data-ttu-id="f8e6b-738">**Derleyici KIMLIĞI**</span><span class="sxs-lookup"><span data-stu-id="f8e6b-738">**Compiler ID**</span></span><br /><span data-ttu-id="f8e6b-739">IAR dili</span><span class="sxs-lookup"><span data-stu-id="f8e6b-739">IAR</span></span><br /><span data-ttu-id="f8e6b-740">ARM</span><span class="sxs-lookup"><span data-stu-id="f8e6b-740">ARM</span></span><br /><span data-ttu-id="f8e6b-741">GNU</span><span class="sxs-lookup"><span data-stu-id="f8e6b-741">GNU</span></span> |

#### <a name="module-linker-for-cortex-m7-using-ac5"></a><span data-ttu-id="f8e6b-742">AC5 kullanarak Cortex için modül Bağlayıcısı-M7</span><span class="sxs-lookup"><span data-stu-id="f8e6b-742">Module linker for Cortex-M7 using AC5</span></span>

<span data-ttu-id="f8e6b-743">Komut satırı üzerine inşa, bağlayıcı dosyası örneği yok.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-743">Built on command-line, no linker file example.</span></span>

#### <a name="building-modules-for-cortex-m7-using-ac5"></a><span data-ttu-id="f8e6b-744">AC5 kullanarak Cortex için modüller oluşturma-M7</span><span class="sxs-lookup"><span data-stu-id="f8e6b-744">Building Modules for Cortex-M7 using AC5</span></span>

<span data-ttu-id="f8e6b-745">AC5 kullanarak Cortex-M7 modülü oluşturmaya yönelik basit bir komut satırı örneği:</span><span class="sxs-lookup"><span data-stu-id="f8e6b-745">A simple command-line example for building a Cortex-M7 module using AC5:</span></span>

```dos
armasm -g --cpu=cortex-m7 --fpu=softvfp --apcs=/interwork/ropi/rwpi txm_module_preamble.s
armcc  -g --cpu=cortex-m7 --fpu=softvfp -c --apcs=/interwork/ropi/rwpi --lower_ropi -I../inc -I../../../../common_modules/inc -I../../../../common_modules/module_manager/inc -I../../../../common/inc sample_threadx_module.c
armlink -d -o sample_threadx_module.axf --elf --ro 0 --first txm_module_preamble.o(Init) --entry=_txm_module_thread_shell_entry --ropi --rwpi --remove --map --symbols --list sample_threadx_module.map txm_module_preamble.o sample_threadx_module.o txm.a
```

#### <a name="thread-extension-definition-for-cortex-m7-using-ac5"></a><span data-ttu-id="f8e6b-746">AC5 kullanarak Cortex için iş parçacığı uzantısı tanımı M7</span><span class="sxs-lookup"><span data-stu-id="f8e6b-746">Thread extension definition for Cortex-M7 using AC5</span></span>

```c
#define TX_THREAD_EXTENSION_2   VOID    *tx_thread_module_instance_ptr;         \
                                VOID    *tx_thread_module_entry_info_ptr;       \
                                ULONG   tx_thread_module_current_user_mode;     \
                                ULONG   tx_thread_module_user_mode;             \
                                ULONG   tx_thread_module_saved_lr;              \
                                VOID    *tx_thread_module_kernel_stack_start;   \
                                VOID    *tx_thread_module_kernel_stack_end;     \
                                ULONG   tx_thread_module_kernel_stack_size;     \
                                VOID    *tx_thread_module_stack_ptr;            \
                                VOID    *tx_thread_module_stack_start;          \
                                VOID    *tx_thread_module_stack_end;            \
                                ULONG   tx_thread_module_stack_size;            \
                                VOID    *tx_thread_module_reserved;
```

#### <a name="building-module-manager-for-cortex-m7-using-ac5"></a><span data-ttu-id="f8e6b-747">AC5 kullanarak Cortex için Modül Yöneticisi oluşturma-M7</span><span class="sxs-lookup"><span data-stu-id="f8e6b-747">Building Module Manager for Cortex-M7 using AC5</span></span>

<span data-ttu-id="f8e6b-748">AC5 kullanarak Cortex-M7 Module Manager oluşturmaya yönelik basit bir komut satırı örneği:</span><span class="sxs-lookup"><span data-stu-id="f8e6b-748">A simple command-line example for building a Cortex-M7 module manager using AC5:</span></span>

```dos
armasm -g --cpu=cortex-m7 --fpu=softvfp --apcs=interwork tx_initialize_low_level.s
armcc -g --cpu=cortex-m7 --fpu=softvfp -c demo_threadx_module_manager.c
armcc -g --cpu=cortex-m7 --fpu=softvfp -c module_code.c
armlink -d -o demo_threadx_module_manager.axf --elf --ro 0x00000000 --first tx_initialize_low_level.o(RESET) --remove --map --symbols --list demo_threadx_module_manager.map tx_initialize_low_level.o demo_threadx_module_manager.o module_code.o tx.a
```

#### <a name="attributes-for-external-memory-enable-api-for-cortex-m7-using-ac5"></a><span data-ttu-id="f8e6b-749">Dış bellek öznitelikleri M7 Cortex için API 'YI etkinleştirir-AC5 kullanarak</span><span class="sxs-lookup"><span data-stu-id="f8e6b-749">Attributes for external memory enable API for Cortex-M7 using AC5</span></span>

### <a name="cortex-m7-using-ac6"></a><span data-ttu-id="f8e6b-750">Cortex-AC6 kullanarak M7</span><span class="sxs-lookup"><span data-stu-id="f8e6b-750">Cortex-M7 using AC6</span></span>

#### <a name="module-properties-for-cortex-m7-using-ac6"></a><span data-ttu-id="f8e6b-751">AC6 kullanarak Cortex-M7 için modül özellikleri</span><span class="sxs-lookup"><span data-stu-id="f8e6b-751">Module properties for Cortex-M7 using AC6</span></span>

| <span data-ttu-id="f8e6b-752">Sürümleri</span><span class="sxs-lookup"><span data-stu-id="f8e6b-752">Bit</span></span> | <span data-ttu-id="f8e6b-753">Değer</span><span class="sxs-lookup"><span data-stu-id="f8e6b-753">Value</span></span> | <span data-ttu-id="f8e6b-754">Anlamı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-754">Meaning</span></span> |
|---|---|---|
| <span data-ttu-id="f8e6b-755">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-755">0</span></span> | <span data-ttu-id="f8e6b-756">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-756">0</span></span><br /><span data-ttu-id="f8e6b-757">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-757">1</span></span> | <span data-ttu-id="f8e6b-758">Ayrıcalıklı mod yürütme</span><span class="sxs-lookup"><span data-stu-id="f8e6b-758">Privileged mode execution</span></span><br /><span data-ttu-id="f8e6b-759">Kullanıcı modu yürütme</span><span class="sxs-lookup"><span data-stu-id="f8e6b-759">User mode execution</span></span> |
| <span data-ttu-id="f8e6b-760">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-760">1</span></span> | <span data-ttu-id="f8e6b-761">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-761">0</span></span><br /><span data-ttu-id="f8e6b-762">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-762">1</span></span> | <span data-ttu-id="f8e6b-763">MPU koruması yok</span><span class="sxs-lookup"><span data-stu-id="f8e6b-763">No MPU protection</span></span><br /><span data-ttu-id="f8e6b-764">MPU koruması (Kullanıcı modunun seçili olması gerekir)</span><span class="sxs-lookup"><span data-stu-id="f8e6b-764">MPU protection (must have user mode selected)</span></span> |
| <span data-ttu-id="f8e6b-765">2</span><span class="sxs-lookup"><span data-stu-id="f8e6b-765">2</span></span> | <span data-ttu-id="f8e6b-766">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-766">0</span></span><br /><span data-ttu-id="f8e6b-767">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-767">1</span></span> | <span data-ttu-id="f8e6b-768">Paylaşılan/dış bellek erişimini devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="f8e6b-768">Disable shared/external memory access</span></span><br /><span data-ttu-id="f8e6b-769">Paylaşılan/dış bellek erişimini etkinleştir</span><span class="sxs-lookup"><span data-stu-id="f8e6b-769">Enable shared/external memory access</span></span> |
| <span data-ttu-id="f8e6b-770">[23-3]</span><span class="sxs-lookup"><span data-stu-id="f8e6b-770">[23-3]</span></span> | <span data-ttu-id="f8e6b-771">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-771">0</span></span> | <span data-ttu-id="f8e6b-772">Ayrılmıştır</span><span class="sxs-lookup"><span data-stu-id="f8e6b-772">Reserved</span></span>
| <span data-ttu-id="f8e6b-773">[31-24]</span><span class="sxs-lookup"><span data-stu-id="f8e6b-773">[31-24]</span></span> | <br /><span data-ttu-id="f8e6b-774">-</span><span class="sxs-lookup"><span data-stu-id="f8e6b-774">0x00</span></span><br /><span data-ttu-id="f8e6b-775">0x01</span><span class="sxs-lookup"><span data-stu-id="f8e6b-775">0x01</span></span><br /><span data-ttu-id="f8e6b-776">0x02</span><span class="sxs-lookup"><span data-stu-id="f8e6b-776">0x02</span></span> | <span data-ttu-id="f8e6b-777">**Derleyici KIMLIĞI**</span><span class="sxs-lookup"><span data-stu-id="f8e6b-777">**Compiler ID**</span></span><br /><span data-ttu-id="f8e6b-778">IAR dili</span><span class="sxs-lookup"><span data-stu-id="f8e6b-778">IAR</span></span><br /><span data-ttu-id="f8e6b-779">ARM</span><span class="sxs-lookup"><span data-stu-id="f8e6b-779">ARM</span></span><br /><span data-ttu-id="f8e6b-780">GNU</span><span class="sxs-lookup"><span data-stu-id="f8e6b-780">GNU</span></span> |

#### <a name="module-linker-for-cortex-m7-using-ac6"></a><span data-ttu-id="f8e6b-781">AC6 kullanarak Cortex için modül Bağlayıcısı-M7</span><span class="sxs-lookup"><span data-stu-id="f8e6b-781">Module linker for Cortex-M7 using AC6</span></span>

<span data-ttu-id="f8e6b-782">Bağlayıcı dosyası kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-782">No linker file is used.</span></span> <span data-ttu-id="f8e6b-783">Bkz. proje ayarları.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-783">See project settings.</span></span>

#### <a name="building-modules-for-cortex-m7-using-ac6"></a><span data-ttu-id="f8e6b-784">AC6 kullanarak Cortex için modüller oluşturma-M7</span><span class="sxs-lookup"><span data-stu-id="f8e6b-784">Building Modules for Cortex-M7 using AC6</span></span>

<span data-ttu-id="f8e6b-785">Örnek çalışma alanı sağlanır.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-785">An example workspace is provided.</span></span> <span data-ttu-id="f8e6b-786">ThreadX kitaplığı, ThreadX modülleri kitaplığı, örnek Modül projesi ve örnek Module Manager projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-786">Build the ThreadX library, ThreadX Modules library, sample module project, and sample module manager project.</span></span>

#### <a name="thread-extension-definition-for-cortex-m7-using-ac6"></a><span data-ttu-id="f8e6b-787">AC6 kullanarak Cortex için iş parçacığı uzantısı tanımı M7</span><span class="sxs-lookup"><span data-stu-id="f8e6b-787">Thread extension definition for Cortex-M7 using AC6</span></span>

```c
#define TX_THREAD_EXTENSION_2               VOID    *tx_thread_module_instance_ptr;         \
                                            VOID    *tx_thread_module_entry_info_ptr;       \
                                            ULONG   tx_thread_module_current_user_mode;     \
                                            ULONG   tx_thread_module_user_mode;             \
                                            ULONG   tx_thread_module_saved_lr;              \
                                            VOID    *tx_thread_module_kernel_stack_start;   \
                                            VOID    *tx_thread_module_kernel_stack_end;     \
                                            ULONG   tx_thread_module_kernel_stack_size;     \
                                            VOID    *tx_thread_module_stack_ptr;            \
                                            VOID    *tx_thread_module_stack_start;          \
                                            VOID    *tx_thread_module_stack_end;            \
                                            ULONG   tx_thread_module_stack_size;            \
                                            VOID    *tx_thread_module_reserved;
```

#### <a name="building-module-manager-for-cortex-m7-using-ac6"></a><span data-ttu-id="f8e6b-788">AC6 kullanarak Cortex için Modül Yöneticisi oluşturma-M7</span><span class="sxs-lookup"><span data-stu-id="f8e6b-788">Building Module Manager for Cortex-M7 using AC6</span></span>

<span data-ttu-id="f8e6b-789">Örnek çalışma alanı sağlanır.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-789">An example workspace is provided.</span></span> <span data-ttu-id="f8e6b-790">ThreadX kitaplığı, ThreadX modülleri kitaplığı, örnek Modül projesi ve örnek Module Manager projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-790">Build the ThreadX library, ThreadX Modules library, sample module project, and sample module manager project.</span></span>

#### <a name="attributes-for-external-memory-enable-api-for-cortex-m7-using-ac6"></a><span data-ttu-id="f8e6b-791">Dış bellek öznitelikleri M7 Cortex için API 'YI etkinleştirir-AC6 kullanarak</span><span class="sxs-lookup"><span data-stu-id="f8e6b-791">Attributes for external memory enable API for Cortex-M7 using AC6</span></span>

<span data-ttu-id="f8e6b-792">Modülün paylaşılan belleğe her zaman okuma erişimi vardır.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-792">Module always has read access to shared memory.</span></span>

| <span data-ttu-id="f8e6b-793">Öznitelik parametresi</span><span class="sxs-lookup"><span data-stu-id="f8e6b-793">Attribute parameter</span></span> | <span data-ttu-id="f8e6b-794">Anlamı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-794">Meaning</span></span> |
|---|---|
| <span data-ttu-id="f8e6b-795">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span><span class="sxs-lookup"><span data-stu-id="f8e6b-795">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span></span> | <span data-ttu-id="f8e6b-796">Yazma erişimi</span><span class="sxs-lookup"><span data-stu-id="f8e6b-796">Write access</span></span> |

### <a name="cortex-m7-using-gnu"></a><span data-ttu-id="f8e6b-797">Cortex-GNU kullanarak M7</span><span class="sxs-lookup"><span data-stu-id="f8e6b-797">Cortex-M7 using GNU</span></span>

#### <a name="module-properties-for-cortex-m7-using-gnu"></a><span data-ttu-id="f8e6b-798">GNU kullanarak Cortex-M7 için modül özellikleri</span><span class="sxs-lookup"><span data-stu-id="f8e6b-798">Module properties for Cortex-M7 using GNU</span></span>

| <span data-ttu-id="f8e6b-799">Sürümleri</span><span class="sxs-lookup"><span data-stu-id="f8e6b-799">Bit</span></span> | <span data-ttu-id="f8e6b-800">Değer</span><span class="sxs-lookup"><span data-stu-id="f8e6b-800">Value</span></span> | <span data-ttu-id="f8e6b-801">Anlamı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-801">Meaning</span></span> |
|---|---|---|
| <span data-ttu-id="f8e6b-802">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-802">0</span></span> | <span data-ttu-id="f8e6b-803">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-803">0</span></span><br /><span data-ttu-id="f8e6b-804">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-804">1</span></span> | <span data-ttu-id="f8e6b-805">Ayrıcalıklı mod yürütme</span><span class="sxs-lookup"><span data-stu-id="f8e6b-805">Privileged mode execution</span></span><br /><span data-ttu-id="f8e6b-806">Kullanıcı modu yürütme</span><span class="sxs-lookup"><span data-stu-id="f8e6b-806">User mode execution</span></span> |
| <span data-ttu-id="f8e6b-807">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-807">1</span></span> | <span data-ttu-id="f8e6b-808">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-808">0</span></span><br /><span data-ttu-id="f8e6b-809">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-809">1</span></span> | <span data-ttu-id="f8e6b-810">MPU koruması yok</span><span class="sxs-lookup"><span data-stu-id="f8e6b-810">No MPU protection</span></span><br /><span data-ttu-id="f8e6b-811">MPU koruması (Kullanıcı modunun seçili olması gerekir)</span><span class="sxs-lookup"><span data-stu-id="f8e6b-811">MPU protection (must have user mode selected)</span></span> |
| <span data-ttu-id="f8e6b-812">2</span><span class="sxs-lookup"><span data-stu-id="f8e6b-812">2</span></span> | <span data-ttu-id="f8e6b-813">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-813">0</span></span><br /><span data-ttu-id="f8e6b-814">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-814">1</span></span> | <span data-ttu-id="f8e6b-815">Paylaşılan/dış bellek erişimini devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="f8e6b-815">Disable shared/external memory access</span></span><br /><span data-ttu-id="f8e6b-816">Paylaşılan/dış bellek erişimini etkinleştir</span><span class="sxs-lookup"><span data-stu-id="f8e6b-816">Enable shared/external memory access</span></span> |
| <span data-ttu-id="f8e6b-817">[23-3]</span><span class="sxs-lookup"><span data-stu-id="f8e6b-817">[23-3]</span></span> | <span data-ttu-id="f8e6b-818">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-818">0</span></span> | <span data-ttu-id="f8e6b-819">Ayrılmıştır</span><span class="sxs-lookup"><span data-stu-id="f8e6b-819">Reserved</span></span>
| <span data-ttu-id="f8e6b-820">[31-24]</span><span class="sxs-lookup"><span data-stu-id="f8e6b-820">[31-24]</span></span> | <br /><span data-ttu-id="f8e6b-821">-</span><span class="sxs-lookup"><span data-stu-id="f8e6b-821">0x00</span></span><br /><span data-ttu-id="f8e6b-822">0x01</span><span class="sxs-lookup"><span data-stu-id="f8e6b-822">0x01</span></span><br /><span data-ttu-id="f8e6b-823">0x02</span><span class="sxs-lookup"><span data-stu-id="f8e6b-823">0x02</span></span> | <span data-ttu-id="f8e6b-824">**Derleyici KIMLIĞI**</span><span class="sxs-lookup"><span data-stu-id="f8e6b-824">**Compiler ID**</span></span><br /><span data-ttu-id="f8e6b-825">IAR dili</span><span class="sxs-lookup"><span data-stu-id="f8e6b-825">IAR</span></span><br /><span data-ttu-id="f8e6b-826">ARM</span><span class="sxs-lookup"><span data-stu-id="f8e6b-826">ARM</span></span><br /><span data-ttu-id="f8e6b-827">GNU</span><span class="sxs-lookup"><span data-stu-id="f8e6b-827">GNU</span></span> |

#### <a name="module-linker-for-cortex-m7-using-gnu"></a><span data-ttu-id="f8e6b-828">GNU kullanarak Cortex için modül Bağlayıcısı-M7</span><span class="sxs-lookup"><span data-stu-id="f8e6b-828">Module linker for Cortex-M7 using GNU</span></span>

```c
MEMORY
{
  FLASH (rx) : ORIGIN = 0x00030000, LENGTH = 0x00010000
  RAM   (wx) : ORIGIN = 0, LENGTH = 0x00100000
}


SECTIONS
{
  __FLASH_segment_start__ = 0x00030000;
  __FLASH_segment_end__   = 0x00040000;
  __RAM_segment_start__   = 0;
  __RAM_segment_end__     = 0x8000;

  __HEAPSIZE__ = 128;

  __preamble_load_start__ = __FLASH_segment_start__;
  .preamble __FLASH_segment_start__ : AT(__FLASH_segment_start__)
  {
    __preamble_start__ = .;
    *(.preamble .preamble.*)
  }
  __preamble_end__ = __preamble_start__ + SIZEOF(.preamble);

  __dynsym_load_start__ =  ALIGN(__preamble_end__ , 4);
  .dynsym ALIGN(__dynsym_load_start__ , 4) : AT(ALIGN(__dynsym_load_start__ , 4))
  {
    . = ALIGN(4);
    KEEP (*(.dynsym))
    KEEP (*(.dynsym*))
    . = ALIGN(4);
  }
  __dynsym_end__ = __dynsym_load_start__ + SIZEOF(.dynsym);

  __dynstr_load_start__ =  ALIGN(__dynsym_end__ , 4);
  .dynstr ALIGN(__dynstr_load_start__ , 4) : AT(ALIGN(__dynstr_load_start__, 4))
  {
    . = ALIGN(4);
    KEEP (*(.dynstr))
    KEEP (*(.dynstr*))
    . = ALIGN(4);
  }
  __dynstr_end__ = __dynstr_load_start__ + SIZEOF(.dynstr);

  __reldyn_load_start__ =  ALIGN(__dynstr_end__ , 4);
  .rel.dyn ALIGN(__reldyn_load_start__ , 4) : AT(ALIGN(__reldyn_load_start__ , 4))
  {
    . = ALIGN(4);
    KEEP (*(.rel.dyn))
    KEEP (*(.rel.dyn*))
    . = ALIGN(4);
  }
  __reldyn_end__ = __reldyn_load_start__ + SIZEOF(.rel.dyn);

  __relplt_load_start__ =  ALIGN(__reldyn_end__ , 4);
  .rel.plt ALIGN(__relplt_load_start__ , 4) : AT(ALIGN(__relplt_load_start__ , 4))
  {
    . = ALIGN(4);
    KEEP (*(.rel.plt))
    KEEP (*(.rel.plt*))
    . = ALIGN(4);
  }
  __relplt_end__ = __relplt_load_start__ + SIZEOF(.rel.plt);

  __plt_load_start__ =  ALIGN(__relplt_end__ , 4);
  .plt ALIGN(__plt_load_start__ , 4) : AT(ALIGN(__plt_load_start__ , 4))
  {
    . = ALIGN(4);
    KEEP (*(.plt))
    KEEP (*(.plt*))
    . = ALIGN(4);
  }
  __plt_end__ = __plt_load_start__ + SIZEOF(.plt);

  __interp_load_start__ =  ALIGN(__plt_end__ , 4);
  .interp ALIGN(__interp_load_start__ , 4) : AT(ALIGN(__interp_load_start__ , 4))
  {
    . = ALIGN(4);
    KEEP (*(.interp))
    KEEP (*(.interp*))
    . = ALIGN(4);
  }
  __interp_end__ = __interp_load_start__ + SIZEOF(.interp);

  __hash_load_start__ =  ALIGN(__interp_end__ , 4);
  .hash ALIGN(__hash_load_start__ , 4) : AT(ALIGN(__hash_load_start__, 4))
  {
    . = ALIGN(4);
    KEEP (*(.hash))
    KEEP (*(.hash*))
    . = ALIGN(4);
  }
  __hash_end__ = __hash_load_start__ + SIZEOF(.hash);

  __text_load_start__ =  ALIGN(__hash_end__ , 4);
  .text ALIGN(__text_load_start__ , 4) : AT(ALIGN(__text_load_start__, 4))
  {
    __text_start__ = .;
    *(.text .text.* .glue_7t .glue_7 .gnu.linkonce.t.* .gcc_except_table  )
  }
  __text_end__ = __text_start__ + SIZEOF(.text);

  __dtors_load_start__ = ALIGN(__text_end__ , 4);
  .dtors ALIGN(__text_end__ , 4) : AT(ALIGN(__text_end__ , 4))
  {
    __dtors_start__ = .;
    KEEP (*(SORT(.dtors.*))) KEEP (*(.dtors))
  }
  __dtors_end__ = __dtors_start__ + SIZEOF(.dtors);

  __ctors_load_start__ = ALIGN(__dtors_end__ , 4);
  .ctors ALIGN(__dtors_end__ , 4) : AT(ALIGN(__dtors_end__ , 4))
  {
    __ctors_start__ = .;
    KEEP (*(SORT(.ctors.*))) KEEP (*(.ctors))
  }
  __ctors_end__ = __ctors_start__ + SIZEOF(.ctors);

  __got_load_start__ = ALIGN(__ctors_end__ , 4);
  .got ALIGN(__ctors_end__ , 4) : AT(ALIGN(__ctors_end__ , 4))
  {
    . = ALIGN(4);
    _sgot = .;
    KEEP (*(.got))
    KEEP (*(.got*))
    . = ALIGN(4);
    _egot = .;
  } 
  __got_end__ =  __got_load_start__ + SIZEOF(.got);

  __rodata_load_start__ = ALIGN(__got_end__ , 4);
  .rodata ALIGN(__got_end__ , 4) : AT(ALIGN(__got_end__ , 4))
  {
    __rodata_start__ = .;
    *(.rodata .rodata.* .gnu.linkonce.r.*)
  }
  __rodata_end__ = __rodata_start__ + SIZEOF(.rodata);
 
  __code_size__ =  __rodata_end__ - __FLASH_segment_start__;

  __fast_load_start__ = ALIGN(__rodata_end__ , 4);

  __fast_load_end__ = __fast_load_start__ + SIZEOF(.fast);

  __new_got_start__ = ALIGN(__RAM_segment_start__ , 4);

  __new_got_end__ =  __new_got_start__ + SIZEOF(.got);

  .fast ALIGN(__new_got_end__ , 4) : AT(ALIGN(__rodata_end__ , 4))
  {
    __fast_start__ = .;
    *(.fast .fast.*)
  }
  __fast_end__ = __fast_start__ + SIZEOF(.fast);

  .fast_run ALIGN(__fast_end__ , 4) (NOLOAD) :
  {
    __fast_run_start__ = .;
    . = MAX(__fast_run_start__ + SIZEOF(.fast), .);
  }
  __fast_run_end__ = __fast_run_start__ + SIZEOF(.fast_run);

  __data_load_start__ = ALIGN(__fast_load_start__ + SIZEOF(.fast) , 4);
  .data ALIGN(__fast_run_end__ , 4) : AT(ALIGN(__fast_load_start__ + SIZEOF(.fast) , 4))
  {
    __data_start__ = .;
    *(.data .data.* .gnu.linkonce.d.*)
  }
  __data_end__ = __data_start__ + SIZEOF(.data);

  __data_load_end__ = __data_load_start__ + SIZEOF(.data);

  __FLASH_segment_used_end__ = ALIGN(__fast_load_start__ + SIZEOF(.fast) , 4) + SIZEOF(.data);

  .data_run ALIGN(__fast_run_end__ , 4) (NOLOAD) :
  {
    __data_run_start__ = .;
    . = MAX(__data_run_start__ + SIZEOF(.data), .);
  }
  __data_run_end__ = __data_run_start__ + SIZEOF(.data_run);

  __bss_load_start__ = ALIGN(__data_run_end__ , 4);
  .bss ALIGN(__data_run_end__ , 4) (NOLOAD) : AT(ALIGN(__data_run_end__ , 4))
  {
    __bss_start__ = .;
    *(.bss .bss.* .gnu.linkonce.b.*) *(COMMON)
  }
  __bss_end__ = __bss_start__ + SIZEOF(.bss);

  __non_init_load_start__ = ALIGN(__bss_end__ , 4);
  .non_init ALIGN(__bss_end__ , 4) (NOLOAD) : AT(ALIGN(__bss_end__ , 4))
  {
    __non_init_start__ = .;
    *(.non_init .non_init.*)
  }
  __non_init_end__ = __non_init_start__ + SIZEOF(.non_init);

  __heap_load_start__ = ALIGN(__non_init_end__ , 4);
  .heap ALIGN(__non_init_end__ , 4) (NOLOAD) : AT(ALIGN(__non_init_end__ , 4))
  {
    __heap_start__ = .;
    *(.heap)
    . = ALIGN(MAX(__heap_start__ + __HEAPSIZE__ , .), 4);
  }
  __heap_end__ = __heap_start__ + SIZEOF(.heap);

  __data_size__ =  __heap_end__ - __RAM_segment_start__;

}
```

#### <a name="building-modules-for-cortex-m7-using-gnu"></a><span data-ttu-id="f8e6b-829">GNU kullanarak Cortex için modüller oluşturma-M7</span><span class="sxs-lookup"><span data-stu-id="f8e6b-829">Building Modules for Cortex-M7 using GNU</span></span>

<span data-ttu-id="f8e6b-830">build_threadx_module_sample.bat bkz:</span><span class="sxs-lookup"><span data-stu-id="f8e6b-830">See build_threadx_module_sample.bat:</span></span>

```dos
arm-none-eabi-gcc -c -g -mcpu=cortex-m7 -mfloat-abi=hard -mfpu=fpv5-d16 -fpie -fno-plt -mpic-data-is-text-relative -msingle-pic-base txm_module_preamble.s
arm-none-eabi-gcc -c -g -mcpu=cortex-m7 -mfloat-abi=hard -mfpu=fpv5-d16 -fpie -fno-plt -mpic-data-is-text-relative -msingle-pic-base gcc_setup.S
arm-none-eabi-gcc -c -g -mcpu=cortex-m7 -mfloat-abi=hard -mfpu=fpv5-d16 -fpie -fno-plt -mpic-data-is-text-relative -msingle-pic-base -I..\inc -I..\..\..\..\common\inc -I..\..\..\..\common_modules\inc sample_threadx_module.c
arm-none-eabi-ld -A cortex-m7 -T sample_threadx_module.ld txm_module_preamble.o gcc_setup.o sample_threadx_module.o -e _txm_module_thread_shell_entry txm.a -o sample_threadx_module.axf -M > sample_threadx_module.map
```

#### <a name="thread-extension-definition-for-cortex-m7-using-gnu"></a><span data-ttu-id="f8e6b-831">GNU kullanarak Cortex-M7 için iş parçacığı uzantısı tanımı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-831">Thread extension definition for Cortex-M7 using GNU</span></span>

```c
#define TX_THREAD_EXTENSION_2               VOID    *tx_thread_module_instance_ptr;         \
                                            VOID    *tx_thread_module_entry_info_ptr;       \
                                            ULONG   tx_thread_module_current_user_mode;     \
                                            ULONG   tx_thread_module_user_mode;             \
                                            ULONG   tx_thread_module_saved_lr;              \
                                            VOID    *tx_thread_module_kernel_stack_start;   \
                                            VOID    *tx_thread_module_kernel_stack_end;     \
                                            ULONG   tx_thread_module_kernel_stack_size;     \
                                            VOID    *tx_thread_module_stack_ptr;            \
                                            VOID    *tx_thread_module_stack_start;          \
                                            VOID    *tx_thread_module_stack_end;            \
                                            ULONG   tx_thread_module_stack_size;            \
                                            VOID    *tx_thread_module_reserved;
```

#### <a name="building-module-manager-for-cortex-m7-using-gnu"></a><span data-ttu-id="f8e6b-832">GNU kullanarak Cortex için Modül Yöneticisi oluşturma-M7</span><span class="sxs-lookup"><span data-stu-id="f8e6b-832">Building Module Manager for Cortex-M7 using GNU</span></span>

<span data-ttu-id="f8e6b-833">build_threadx_module_manager_sample.bat bkz:</span><span class="sxs-lookup"><span data-stu-id="f8e6b-833">See build_threadx_module_manager_sample.bat:</span></span>

```dos
arm-none-eabi-gcc -c -g -mcpu=cortex-m7 -mfloat-abi=hard -mfpu=fpv5-d16 -mthumb -I..\inc -I..\..\..\..\common\inc -I..\..\..\..\common_modules\inc sample_threadx_module_manager.c
arm-none-eabi-gcc -c -g -mcpu=cortex-m7 -mfloat-abi=hard -mfpu=fpv5-d16 -mthumb tx_simulator_startup.S
arm-none-eabi-gcc -c -g -mcpu=cortex-m7 -mfloat-abi=hard -mfpu=fpv5-d16 -mthumb cortexm_crt0.S
arm-none-eabi-gcc -g -mcpu=cortex-m7 -mfloat-abi=hard -mfpu=fpv5-d16 -mthumb -nostartfiles -ereset_handler -T sample_threadx.ld tx_simulator_startup.o cortexm_crt0.o sample_threadx_module_manager.o tx.a -o sample_threadx_module_manager.axf -Wl,-Map=sample_threadx_module_manager.map
```

#### <a name="attributes-for-external-memory-enable-api-for-cortex-m7-using-gnu"></a><span data-ttu-id="f8e6b-834">Dış bellek öznitelikleri, GNU kullanarak Cortex için API 'YI etkinleştirir-M7</span><span class="sxs-lookup"><span data-stu-id="f8e6b-834">Attributes for external memory enable API for Cortex-M7 using GNU</span></span>

<span data-ttu-id="f8e6b-835">Modülün paylaşılan belleğe her zaman okuma erişimi vardır.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-835">Module always has read access to shared memory.</span></span>

| <span data-ttu-id="f8e6b-836">Öznitelik parametresi</span><span class="sxs-lookup"><span data-stu-id="f8e6b-836">Attribute parameter</span></span> | <span data-ttu-id="f8e6b-837">Anlamı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-837">Meaning</span></span> |
|---|---|
| <span data-ttu-id="f8e6b-838">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span><span class="sxs-lookup"><span data-stu-id="f8e6b-838">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span></span> | <span data-ttu-id="f8e6b-839">Yazma erişimi</span><span class="sxs-lookup"><span data-stu-id="f8e6b-839">Write access</span></span> |

### <a name="cortex-m7-using-iar"></a><span data-ttu-id="f8e6b-840">Cortex-ıAR kullanarak M7</span><span class="sxs-lookup"><span data-stu-id="f8e6b-840">Cortex-M7 using IAR</span></span>

#### <a name="module-preamble-for-cortex-m7-using-iar"></a><span data-ttu-id="f8e6b-841">IAR kullanarak Cortex için modül girişi-M7</span><span class="sxs-lookup"><span data-stu-id="f8e6b-841">Module preamble for Cortex-M7 using IAR</span></span>

```c
    SECTION .text:CODE

    AAPCS INTERWORK, ROPI, RWPI_COMPATIBLE,  VFP_COMPATIBLE
    PRESERVE8

    /* Define public symbols.  */

    PUBLIC __txm_module_preamble


    /* Define application-specific start/stop entry points for the module.  */

    EXTERN demo_module_start


    /* Define common external references.  */

    EXTERN  _txm_module_thread_shell_entry
    EXTERN  _txm_module_callback_request_thread_entry
    EXTERN  ROPI$$Length
    EXTERN  RWPI$$Length

    DATA
__txm_module_preamble:
    DC32      0x4D4F4455                                        ; Module ID
    DC32      0x5                                               ; Module Major Version
    DC32      0x6                                               ; Module Minor Version
    DC32      32                                                ; Module Preamble Size in 32-bit words
    DC32      0x12345678                                        ; Module ID (application defined)
    DC32      0x00000007                                        ; Module Properties where:
                                                                ;   Bits 31-24: Compiler ID
                                                                ;           0 -> IAR
                                                                ;           1 -> ARM
                                                                ;           2 -> GNU
                                                                ;   Bits 23-3: Reserved
                                                                ;   Bit 2:  0 -> Disable shared/external memory access
                                                                ;           1 -> Enable shared/external memory access
                                                                ;   Bit 1:  0 -> No MPU protection
                                                                ;           1 -> MPU protection (must have user mode selected - bit 0 set)
                                                                ;   Bit 0:  0 -> Privileged mode execution
                                                                ;           1 -> User mode execution


    DC32      _txm_module_thread_shell_entry - . - 0            ; Module Shell Entry Point
    DC32      demo_module_start - . - 0                         ; Module Start Thread Entry Point
    DC32      0                                                 ; Module Stop Thread Entry Point
    DC32      1                                                 ; Module Start/Stop Thread Priority
    DC32      1024                                              ; Module Start/Stop Thread Stack Size
    DC32      _txm_module_callback_request_thread_entry - . - 0 ; Module Callback Thread Entry
    DC32      1                                                 ; Module Callback Thread Priority
    DC32      1024                                              ; Module Callback Thread Stack Size
    DC32      ROPI$$Length                                      ; Module Code Size
    DC32      RWPI$$Length                                      ; Module Data Size
    DC32      0                                                 ; Reserved 0
    DC32      0                                                 ; Reserved 1
    DC32      0                                                 ; Reserved 2
    DC32      0                                                 ; Reserved 3
    DC32      0                                                 ; Reserved 4
    DC32      0                                                 ; Reserved 5
    DC32      0                                                 ; Reserved 6
    DC32      0                                                 ; Reserved 7
    DC32      0                                                 ; Reserved 8  
    DC32      0                                                 ; Reserved 9
    DC32      0                                                 ; Reserved 10
    DC32      0                                                 ; Reserved 11
    DC32      0                                                 ; Reserved 12
    DC32      0                                                 ; Reserved 13
    DC32      0                                                 ; Reserved 14
    DC32      0                                                 ; Reserved 15

    END
```

#### <a name="module-properties-for-cortex-m7-using-iar"></a><span data-ttu-id="f8e6b-842">IAR kullanarak Cortex-M7 için modül özellikleri</span><span class="sxs-lookup"><span data-stu-id="f8e6b-842">Module properties for Cortex-M7 using IAR</span></span>

| <span data-ttu-id="f8e6b-843">Sürümleri</span><span class="sxs-lookup"><span data-stu-id="f8e6b-843">Bit</span></span> | <span data-ttu-id="f8e6b-844">Değer</span><span class="sxs-lookup"><span data-stu-id="f8e6b-844">Value</span></span> | <span data-ttu-id="f8e6b-845">Anlamı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-845">Meaning</span></span> |
|---|---|---|
| <span data-ttu-id="f8e6b-846">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-846">0</span></span> | <span data-ttu-id="f8e6b-847">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-847">0</span></span><br /><span data-ttu-id="f8e6b-848">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-848">1</span></span> | <span data-ttu-id="f8e6b-849">Ayrıcalıklı mod yürütme</span><span class="sxs-lookup"><span data-stu-id="f8e6b-849">Privileged mode execution</span></span><br /><span data-ttu-id="f8e6b-850">Kullanıcı modu yürütme</span><span class="sxs-lookup"><span data-stu-id="f8e6b-850">User mode execution</span></span> |
| <span data-ttu-id="f8e6b-851">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-851">1</span></span> | <span data-ttu-id="f8e6b-852">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-852">0</span></span><br /><span data-ttu-id="f8e6b-853">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-853">1</span></span> | <span data-ttu-id="f8e6b-854">MPU koruması yok</span><span class="sxs-lookup"><span data-stu-id="f8e6b-854">No MPU protection</span></span><br /><span data-ttu-id="f8e6b-855">MPU koruması (Kullanıcı modunun seçili olması gerekir)</span><span class="sxs-lookup"><span data-stu-id="f8e6b-855">MPU protection (must have user mode selected)</span></span> |
| <span data-ttu-id="f8e6b-856">2</span><span class="sxs-lookup"><span data-stu-id="f8e6b-856">2</span></span> | <span data-ttu-id="f8e6b-857">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-857">0</span></span><br /><span data-ttu-id="f8e6b-858">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-858">1</span></span> | <span data-ttu-id="f8e6b-859">Paylaşılan/dış bellek erişimini devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="f8e6b-859">Disable shared/external memory access</span></span><br /><span data-ttu-id="f8e6b-860">Paylaşılan/dış bellek erişimini etkinleştir</span><span class="sxs-lookup"><span data-stu-id="f8e6b-860">Enable shared/external memory access</span></span> |
| <span data-ttu-id="f8e6b-861">[23-3]</span><span class="sxs-lookup"><span data-stu-id="f8e6b-861">[23-3]</span></span> | <span data-ttu-id="f8e6b-862">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-862">0</span></span> | <span data-ttu-id="f8e6b-863">Ayrılmıştır</span><span class="sxs-lookup"><span data-stu-id="f8e6b-863">Reserved</span></span>
| <span data-ttu-id="f8e6b-864">[31-24]</span><span class="sxs-lookup"><span data-stu-id="f8e6b-864">[31-24]</span></span> | <br /><span data-ttu-id="f8e6b-865">-</span><span class="sxs-lookup"><span data-stu-id="f8e6b-865">0x00</span></span><br /><span data-ttu-id="f8e6b-866">0x01</span><span class="sxs-lookup"><span data-stu-id="f8e6b-866">0x01</span></span><br /><span data-ttu-id="f8e6b-867">0x02</span><span class="sxs-lookup"><span data-stu-id="f8e6b-867">0x02</span></span> | <span data-ttu-id="f8e6b-868">**Derleyici KIMLIĞI**</span><span class="sxs-lookup"><span data-stu-id="f8e6b-868">**Compiler ID**</span></span><br /><span data-ttu-id="f8e6b-869">IAR dili</span><span class="sxs-lookup"><span data-stu-id="f8e6b-869">IAR</span></span><br /><span data-ttu-id="f8e6b-870">ARM</span><span class="sxs-lookup"><span data-stu-id="f8e6b-870">ARM</span></span><br /><span data-ttu-id="f8e6b-871">GNU</span><span class="sxs-lookup"><span data-stu-id="f8e6b-871">GNU</span></span> |

#### <a name="module-linker-for-cortex-m7-using-iar"></a><span data-ttu-id="f8e6b-872">IAR kullanarak Cortex için modül Bağlayıcısı-M7</span><span class="sxs-lookup"><span data-stu-id="f8e6b-872">Module linker for Cortex-M7 using IAR</span></span>

```c
/*###ICF### Section handled by ICF editor, don't touch! ****/
/*-Editor annotation file-*/
/* IcfEditorFile="$TOOLKIT_DIR$\config\ide\IcfEditor\cortex_v1_0.xml" */
/*-Specials-*/
define symbol __ICFEDIT_intvec_start__     = 0x00400000;
/*-Memory Regions-*/
define symbol __ICFEDIT_region_RAM_start__ = 0x20450000;
define symbol __ICFEDIT_region_RAM_end__   = 0x2045f000 -1;
define symbol __ICFEDIT_region_RAM_NOCACHE_start__ = 0x2045f000;
define symbol __ICFEDIT_region_RAM_NOCACHE_end__   = 0x20460000 -1;
define symbol __ICFEDIT_region_ROM_start__ = 0x00500000;
define symbol __ICFEDIT_region_ROM_end__   = 0x00600000 -1;
define symbol __ICFEDIT_region_SDRAM_start__ = 0x70000000;
define symbol __ICFEDIT_region_SDRAM_end__   = 0x70200000 -1;

/*-Sizes-*/
define symbol __ICFEDIT_size_cstack__      = 0x2000;
define symbol __ICFEDIT_size_heap__        = 0x1000;
/**** End of ICF editor section. ###ICF###*/

define memory mem with size = 4G;
define region RAM_region    = mem:[from __ICFEDIT_region_RAM_start__ to __ICFEDIT_region_RAM_end__];
define region RAM_NOCACHE_region = mem:[from __ICFEDIT_region_RAM_NOCACHE_start__ to __ICFEDIT_region_RAM_NOCACHE_end__];
define region ROM_region    = mem:[from __ICFEDIT_region_ROM_start__ to __ICFEDIT_region_ROM_end__];
define region SDRAM_region  = mem:[from __ICFEDIT_region_SDRAM_start__ to __ICFEDIT_region_SDRAM_end__];

define block HEAP   with alignment = 8, size = __ICFEDIT_size_heap__   { };

initialize by copy { readwrite };
do not initialize  { section .noinit };

define movable block ROPI with alignment = 4, fixed order
{
  ro object txm_module_preamble.o,
  ro,
  ro data
};

define movable block RWPI with alignment = 8, fixed order, static base
{
  rw,
  block HEAP
};

place in ROM_region   { block ROPI };
place in RAM_region   { block RWPI };
```

#### <a name="building-modules-for-cortex-m7-using-iar"></a><span data-ttu-id="f8e6b-873">IAR kullanarak Cortex için modüller oluşturma-M7</span><span class="sxs-lookup"><span data-stu-id="f8e6b-873">Building Modules for Cortex-M7 using IAR</span></span>

<span data-ttu-id="f8e6b-874">Örnek çalışma alanı sağlanır.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-874">An example workspace is provided.</span></span> <span data-ttu-id="f8e6b-875">ThreadX kitaplığı, ThreadX modülleri kitaplığı, demo modülü projesi ve tanıtım modülü Yöneticisi projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-875">Build the ThreadX library, ThreadX Modules library, demo module project, and demo module manager project.</span></span>

#### <a name="thread-extension-definition-for-cortex-m7-using-iar"></a><span data-ttu-id="f8e6b-876">IAR kullanarak Cortex-M7 için iş parçacığı uzantısı tanımı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-876">Thread extension definition for Cortex-M7 using IAR</span></span>

```c
#define TX_THREAD_EXTENSION_2   VOID    *tx_thread_module_instance_ptr;         \
                                VOID    *tx_thread_module_entry_info_ptr;       \
                                ULONG   tx_thread_module_current_user_mode;     \
                                ULONG   tx_thread_module_user_mode;             \
                                ULONG   tx_thread_module_saved_lr;              \
                                VOID    *tx_thread_module_kernel_stack_start;   \
                                VOID    *tx_thread_module_kernel_stack_end;     \
                                ULONG   tx_thread_module_kernel_stack_size;     \
                                VOID    *tx_thread_module_stack_ptr;            \
                                VOID    *tx_thread_module_stack_start;          \
                                VOID    *tx_thread_module_stack_end;            \
                                ULONG   tx_thread_module_stack_size;            \
                                VOID    *tx_thread_module_reserved;             \
                                VOID    *tx_thread_iar_tls_pointer;
```

#### <a name="building-module-manager-for-cortex-m7-using-iar"></a><span data-ttu-id="f8e6b-877">IAR kullanarak Cortex için Modül Yöneticisi oluşturma-M7</span><span class="sxs-lookup"><span data-stu-id="f8e6b-877">Building Module Manager for Cortex-M7 using IAR</span></span>

<span data-ttu-id="f8e6b-878">Örnek çalışma alanı sağlanır.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-878">An example workspace is provided.</span></span> <span data-ttu-id="f8e6b-879">ThreadX kitaplığı, ThreadX modülleri kitaplığı, demo modülü projesi ve tanıtım modülü Yöneticisi projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-879">Build the ThreadX library, ThreadX Modules library, demo module project, and demo module manager project.</span></span>

#### <a name="attributes-for-external-memory-enable-api-for-cortex-m7-using-iar"></a><span data-ttu-id="f8e6b-880">Dış bellek öznitelikleri ıAR kullanarak Cortex için API 'YI etkinleştirir-M7</span><span class="sxs-lookup"><span data-stu-id="f8e6b-880">Attributes for external memory enable API for Cortex-M7 using IAR</span></span>

<span data-ttu-id="f8e6b-881">Modülün paylaşılan belleğe her zaman okuma erişimi vardır.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-881">Module always has read access to shared memory.</span></span>

| <span data-ttu-id="f8e6b-882">Öznitelik parametresi</span><span class="sxs-lookup"><span data-stu-id="f8e6b-882">Attribute parameter</span></span> | <span data-ttu-id="f8e6b-883">Anlamı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-883">Meaning</span></span> |
|---|---|
| <span data-ttu-id="f8e6b-884">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span><span class="sxs-lookup"><span data-stu-id="f8e6b-884">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span></span> | <span data-ttu-id="f8e6b-885">Yazma erişimi</span><span class="sxs-lookup"><span data-stu-id="f8e6b-885">Write access</span></span> |

## <a name="cortex-r4-processor"></a><span data-ttu-id="f8e6b-886">Cortex-R4 işlemcisi</span><span class="sxs-lookup"><span data-stu-id="f8e6b-886">Cortex-R4 processor</span></span>

### <a name="cortex-r4-using-ac6"></a><span data-ttu-id="f8e6b-887">Cortex-AC6 kullanarak R4</span><span class="sxs-lookup"><span data-stu-id="f8e6b-887">Cortex-R4 using AC6</span></span>

#### <a name="module-preamble-for-cortex-r4-using-ac6"></a><span data-ttu-id="f8e6b-888">AC6 kullanarak Cortex için modül girişi-R4</span><span class="sxs-lookup"><span data-stu-id="f8e6b-888">Module preamble for Cortex-R4 using AC6</span></span>

```c
    .text

/* Define common external references.  */

.global     _txm_module_thread_shell_entry
.global     demo_module_start
.global     _txm_module_callback_request_thread_entry
.global     Image$$ER_RO$$Length
.global     Image$$ER_RW$$Length
.global     Image$$ER_ZI$$ZI$$Length

/* Stack aligned, ROPI and RWPI, R9 used as data offset register.  */
.eabi_attribute Tag_ABI_align_preserved, 1
.eabi_attribute Tag_ABI_PCS_RO_data, 1
.eabi_attribute Tag_ABI_PCS_R9_use,  1
.eabi_attribute Tag_ABI_PCS_RW_data, 2

__txm_module_preamble:
.word   0x4D4F4455                                          /* Module ID  */
.word   0x5                                                 /* Module Major Version  */
.word   0x3                                                 /* Module Minor Version  */
.word   32                                                  /* Module Preamble Size in 32-bit words  */
.word   0x12345678                                          /* Module ID (application defined)  */
.word   0x01000001                                          /* Module Properties where:
                                                               Bits 31-24: Compiler ID
                                                                       0 -> IAR
                                                                       1 -> RVDS/ARM
                                                                       2 -> GNU
                                                               Bits 23-1:  Reserved
                                                               Bit 0:  0 -> Privileged mode execution (no MMU protection)
                                                                       1 -> User mode execution (MMU protection)  */
.word   _txm_module_thread_shell_entry - __txm_module_preamble  /* Module Shell Entry Point  */
.word   demo_module_start - __txm_module_preamble           /* Module Start Thread Entry Point  */
.word   0                                                   /* Module Stop Thread Entry Point   */
.word   1                                                   /* Module Start/Stop Thread Priority  */
.word   1024                                                /* Module Start/Stop Thread Stack Size  */
.word   _txm_module_callback_request_thread_entry - __txm_module_preamble   /* Module Callback Thread Entry  */
.word   1                                                   /* Module Callback Thread Priority  */
.word   1024                                                /* Module Callback Thread Stack Size  */
.word   9000                                                /* Module Code Size */
.word   11000                                               /* Module Data Size */
.word   0                                                   /* Reserved 0  */
.word   0                                                   /* Reserved 1  */
.word   0                                                   /* Reserved 2  */
.word   0                                                   /* Reserved 3  */
.word   0                                                   /* Reserved 4  */
.word   0                                                   /* Reserved 5  */
.word   0                                                   /* Reserved 6  */
.word   0                                                   /* Reserved 7  */
.word   0                                                   /* Reserved 8  */
.word   0                                                   /* Reserved 9  */
.word   0                                                   /* Reserved 10  */
.word   0                                                   /* Reserved 11  */
.word   0                                                   /* Reserved 12  */
.word   0                                                   /* Reserved 13  */
.word   0                                                   /* Reserved 14  */
.word   0                                                   /* Reserved 15  */
```

#### <a name="module-properties-for-cortex-r4-using-ac6"></a><span data-ttu-id="f8e6b-889">AC6 kullanarak Cortex-R4 için modül özellikleri</span><span class="sxs-lookup"><span data-stu-id="f8e6b-889">Module properties for Cortex-R4 using AC6</span></span>

| <span data-ttu-id="f8e6b-890">Sürümleri</span><span class="sxs-lookup"><span data-stu-id="f8e6b-890">Bit</span></span> | <span data-ttu-id="f8e6b-891">Değer</span><span class="sxs-lookup"><span data-stu-id="f8e6b-891">Value</span></span> | <span data-ttu-id="f8e6b-892">Anlamı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-892">Meaning</span></span> |
|---|---|---|
| <span data-ttu-id="f8e6b-893">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-893">0</span></span> | <span data-ttu-id="f8e6b-894">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-894">0</span></span><br /><span data-ttu-id="f8e6b-895">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-895">1</span></span> | <span data-ttu-id="f8e6b-896">Ayrıcalıklı mod yürütme</span><span class="sxs-lookup"><span data-stu-id="f8e6b-896">Privileged mode execution</span></span><br /><span data-ttu-id="f8e6b-897">Kullanıcı modu yürütme</span><span class="sxs-lookup"><span data-stu-id="f8e6b-897">User mode execution</span></span> |
| <span data-ttu-id="f8e6b-898">[23-1]</span><span class="sxs-lookup"><span data-stu-id="f8e6b-898">[23-1]</span></span> | <span data-ttu-id="f8e6b-899">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-899">0</span></span> | <span data-ttu-id="f8e6b-900">Ayrılmıştır</span><span class="sxs-lookup"><span data-stu-id="f8e6b-900">Reserved</span></span>
| <span data-ttu-id="f8e6b-901">[31-24]</span><span class="sxs-lookup"><span data-stu-id="f8e6b-901">[31-24]</span></span> | <br /><span data-ttu-id="f8e6b-902">-</span><span class="sxs-lookup"><span data-stu-id="f8e6b-902">0x00</span></span><br /><span data-ttu-id="f8e6b-903">0x01</span><span class="sxs-lookup"><span data-stu-id="f8e6b-903">0x01</span></span><br /><span data-ttu-id="f8e6b-904">0x02</span><span class="sxs-lookup"><span data-stu-id="f8e6b-904">0x02</span></span> | <span data-ttu-id="f8e6b-905">**Derleyici KIMLIĞI**</span><span class="sxs-lookup"><span data-stu-id="f8e6b-905">**Compiler ID**</span></span><br /><span data-ttu-id="f8e6b-906">IAR dili</span><span class="sxs-lookup"><span data-stu-id="f8e6b-906">IAR</span></span><br /><span data-ttu-id="f8e6b-907">ARM</span><span class="sxs-lookup"><span data-stu-id="f8e6b-907">ARM</span></span><br /><span data-ttu-id="f8e6b-908">GNU</span><span class="sxs-lookup"><span data-stu-id="f8e6b-908">GNU</span></span> |

#### <a name="module-linker-for-cortex-r4-using-ac6"></a><span data-ttu-id="f8e6b-909">AC6 kullanarak Cortex için modül Bağlayıcısı-R4</span><span class="sxs-lookup"><span data-stu-id="f8e6b-909">Module linker for Cortex-R4 using AC6</span></span>

<span data-ttu-id="f8e6b-910">Komut satırı üzerine inşa, bağlayıcı dosyası örneği yok.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-910">Built on command-line, no linker file example.</span></span>

#### <a name="building-modules-for-cortex-r4-using-ac6"></a><span data-ttu-id="f8e6b-911">AC6 kullanarak Cortex için modüller oluşturma-R4</span><span class="sxs-lookup"><span data-stu-id="f8e6b-911">Building Modules for Cortex-R4 using AC6</span></span>

<span data-ttu-id="f8e6b-912">AC6 kullanarak Cortex-R4 modülü oluşturmaya yönelik basit bir komut satırı örneği:</span><span class="sxs-lookup"><span data-stu-id="f8e6b-912">A simple command-line example for building a Cortex-R4 module using AC6:</span></span>

```dos
armclang -c -g -fropi -frwpi --target=arm-arm-none-eabi -mcpu=cortex-r4 demo_threadx_module.c
armclang -c -g -fropi -frwpi --target=arm-arm-none-eabi -mcpu=cortex-r4 txm_module_preamble.S
armclang -c -g -fropi -frwpi --target=arm-arm-none-eabi -mcpu=cortex-r4 semihosting.c
armlink -d -o demo_threadx_module.axf --elf --ro 0x00100000 --first txm_module_preamble.o --entry=_txm_module_thread_shell_entry --ropi --rwpi --remove --map --symbols --datacompressor=off --list demo_threadx_module.map txm_module_preamble.o demo_threadx_module.o semihosting.o txm.a
```

#### <a name="thread-extension-definition-for-cortex-r4-using-ac6"></a><span data-ttu-id="f8e6b-913">AC6 kullanarak Cortex için iş parçacığı uzantısı tanımı R4</span><span class="sxs-lookup"><span data-stu-id="f8e6b-913">Thread extension definition for Cortex-R4 using AC6</span></span>

```c
#define TX_THREAD_EXTENSION_2   ULONG   tx_thread_vfp_enable;                   \
                                VOID    *tx_thread_module_instance_ptr;         \
                                VOID    *tx_thread_module_entry_info_ptr;       \
                                ULONG   tx_thread_module_current_user_mode;     \
                                ULONG   tx_thread_module_user_mode;             \
                                VOID    *tx_thread_module_kernel_stack_start;   \
                                VOID    *tx_thread_module_kernel_stack_end;     \
                                ULONG   tx_thread_module_kernel_stack_size;     \
                                VOID    *tx_thread_module_stack_ptr;            \
                                VOID    *tx_thread_module_stack_start;          \
                                VOID    *tx_thread_module_stack_end;            \
                                ULONG   tx_thread_module_stack_size;            \
                                VOID    *tx_thread_module_reserved;
```

#### <a name="building-module-manager-for-cortex-r4-using-ac6"></a><span data-ttu-id="f8e6b-914">AC6 kullanarak Cortex için Modül Yöneticisi oluşturma-R4</span><span class="sxs-lookup"><span data-stu-id="f8e6b-914">Building Module Manager for Cortex-R4 using AC6</span></span>

<span data-ttu-id="f8e6b-915">AC6 kullanarak Cortex-R4 Module Manager oluşturmaya yönelik basit bir komut satırı örneği:</span><span class="sxs-lookup"><span data-stu-id="f8e6b-915">A simple command-line example for building a Cortex-R4 module manager using AC6:</span></span>

```dos
armclang -c -g --target=arm-arm-none-eabi -mcpu=cortex-r4 demo_threadx_module_manager.c
armclang -c -g --target=arm-arm-none-eabi -mcpu=cortex-r4 timer.c
armclang -c -g --target=arm-arm-none-eabi -mcpu=cortex-r4 gic.c
armclang -c -g --target=arm-arm-none-eabi -mcpu=cortex-r4 tx_initialize_low_level.S
armclang -c -g --target=arm-arm-none-eabi -mcpu=cortex-r4 startup.S
armlink -d -o demo_threadx_module_manager.axf --elf --scatter=demo_threadx.scat --remove --map --symbols --list demo_threadx_module_manager.map startup.o timer.o gic.o demo_threadx_module_manager.o tx_initialize_low_level.o tx.a
```

#### <a name="attributes-for-external-memory-enable-api-for-cortex-r4-using-ac6"></a><span data-ttu-id="f8e6b-916">Dış bellek öznitelikleri R4 Cortex için API 'YI etkinleştirir-AC6 kullanarak</span><span class="sxs-lookup"><span data-stu-id="f8e6b-916">Attributes for external memory enable API for Cortex-R4 using AC6</span></span>

<span data-ttu-id="f8e6b-917">Modülün paylaşılan belleğe her zaman okuma erişimi vardır.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-917">Module always has read access to shared memory.</span></span>

| <span data-ttu-id="f8e6b-918">Öznitelik parametresi</span><span class="sxs-lookup"><span data-stu-id="f8e6b-918">Attribute parameter</span></span> | <span data-ttu-id="f8e6b-919">Anlamı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-919">Meaning</span></span> |
|---|---|
| <span data-ttu-id="f8e6b-920">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span><span class="sxs-lookup"><span data-stu-id="f8e6b-920">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span></span> | <span data-ttu-id="f8e6b-921">Yazma erişimi</span><span class="sxs-lookup"><span data-stu-id="f8e6b-921">Write access</span></span> |

### <a name="cortex-r4-using-iar"></a><span data-ttu-id="f8e6b-922">Cortex-ıAR kullanarak R4</span><span class="sxs-lookup"><span data-stu-id="f8e6b-922">Cortex-R4 using IAR</span></span>

#### <a name="module-preamble-for-cortex-r4-using-iar"></a><span data-ttu-id="f8e6b-923">IAR kullanarak Cortex için modül girişi-R4</span><span class="sxs-lookup"><span data-stu-id="f8e6b-923">Module preamble for Cortex-R4 using IAR</span></span>

```c
    SECTION .text:CODE

    AAPCS INTERWORK, ROPI, RWPI_COMPATIBLE,  VFP_COMPATIBLE
    PRESERVE8

    /* Define public symbols.  */
    PUBLIC __txm_module_preamble

    /* Define application-specific start/stop entry points for the module.  */
    EXTERN demo_module_start

    /* Define common external references.  */
    EXTERN  _txm_module_thread_shell_entry
    EXTERN  _txm_module_callback_request_thread_entry
    EXTERN  ROPI$$Length
    EXTERN  RWPI$$Length

    DATA
__txm_module_preamble:
    DC32      0x4D4F4455                                        ; Module ID
    DC32      0x5                                               ; Module Major Version
    DC32      0x6                                               ; Module Minor Version
    DC32      32                                                ; Module Preamble Size in 32-bit words
    DC32      0x12345678                                        ; Module ID (application defined)
    DC32      0x00000001                                        ; Module Properties where:
                                                                ;   Bits 31-24: Compiler ID
                                                                ;           0 -> IAR
                                                                ;           1 -> ARM
                                                                ;           2 -> GNU
                                                                ;   Bits 23-1: Reserved
                                                                ;   Bit 0:  0 -> Privileged mode execution (no MPU protection)
                                                                ;           1 -> User mode execution (MPU protection)
    DC32      _txm_module_thread_shell_entry - . - 0            ; Module Shell Entry Point
    DC32      demo_module_start - . - 0                         ; Module Start Thread Entry Point
    DC32      0                                                 ; Module Stop Thread Entry Point
    DC32      1                                                 ; Module Start/Stop Thread Priority
    DC32      1024                                              ; Module Start/Stop Thread Stack Size
    DC32      _txm_module_callback_request_thread_entry - . - 0 ; Module Callback Thread Entry
    DC32      1                                                 ; Module Callback Thread Priority
    DC32      1024                                              ; Module Callback Thread Stack Size
    DC32      ROPI$$Length                                      ; Module Code Size
    DC32      RWPI$$Length                                      ; Module Data Size
    DC32      0                                                 ; Reserved 0
    DC32      0                                                 ; Reserved 1
    DC32      0                                                 ; Reserved 2
    DC32      0                                                 ; Reserved 3
    DC32      0                                                 ; Reserved 4
    DC32      0                                                 ; Reserved 5
    DC32      0                                                 ; Reserved 6
    DC32      0                                                 ; Reserved 7
    DC32      0                                                 ; Reserved 8  
    DC32      0                                                 ; Reserved 9
    DC32      0                                                 ; Reserved 10
    DC32      0                                                 ; Reserved 11
    DC32      0                                                 ; Reserved 12
    DC32      0                                                 ; Reserved 13
    DC32      0                                                 ; Reserved 14
    DC32      0                                                 ; Reserved 15

    END
```

#### <a name="module-properties-for-cortex-r4-using-iar"></a><span data-ttu-id="f8e6b-924">IAR kullanarak Cortex-R4 için modül özellikleri</span><span class="sxs-lookup"><span data-stu-id="f8e6b-924">Module properties for Cortex-R4 using IAR</span></span>

| <span data-ttu-id="f8e6b-925">Sürümleri</span><span class="sxs-lookup"><span data-stu-id="f8e6b-925">Bit</span></span> | <span data-ttu-id="f8e6b-926">Değer</span><span class="sxs-lookup"><span data-stu-id="f8e6b-926">Value</span></span> | <span data-ttu-id="f8e6b-927">Anlamı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-927">Meaning</span></span> |
|---|---|---|
| <span data-ttu-id="f8e6b-928">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-928">0</span></span> | <span data-ttu-id="f8e6b-929">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-929">0</span></span><br /><span data-ttu-id="f8e6b-930">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-930">1</span></span> | <span data-ttu-id="f8e6b-931">Ayrıcalıklı mod yürütme</span><span class="sxs-lookup"><span data-stu-id="f8e6b-931">Privileged mode execution</span></span><br /><span data-ttu-id="f8e6b-932">Kullanıcı modu yürütme</span><span class="sxs-lookup"><span data-stu-id="f8e6b-932">User mode execution</span></span> |
| <span data-ttu-id="f8e6b-933">[23-1]</span><span class="sxs-lookup"><span data-stu-id="f8e6b-933">[23-1]</span></span> | <span data-ttu-id="f8e6b-934">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-934">0</span></span> | <span data-ttu-id="f8e6b-935">Ayrılmıştır</span><span class="sxs-lookup"><span data-stu-id="f8e6b-935">Reserved</span></span>
| <span data-ttu-id="f8e6b-936">[31-24]</span><span class="sxs-lookup"><span data-stu-id="f8e6b-936">[31-24]</span></span> | <br /><span data-ttu-id="f8e6b-937">-</span><span class="sxs-lookup"><span data-stu-id="f8e6b-937">0x00</span></span><br /><span data-ttu-id="f8e6b-938">0x01</span><span class="sxs-lookup"><span data-stu-id="f8e6b-938">0x01</span></span><br /><span data-ttu-id="f8e6b-939">0x02</span><span class="sxs-lookup"><span data-stu-id="f8e6b-939">0x02</span></span> | <span data-ttu-id="f8e6b-940">**Derleyici KIMLIĞI**</span><span class="sxs-lookup"><span data-stu-id="f8e6b-940">**Compiler ID**</span></span><br /><span data-ttu-id="f8e6b-941">IAR dili</span><span class="sxs-lookup"><span data-stu-id="f8e6b-941">IAR</span></span><br /><span data-ttu-id="f8e6b-942">ARM</span><span class="sxs-lookup"><span data-stu-id="f8e6b-942">ARM</span></span><br /><span data-ttu-id="f8e6b-943">GNU</span><span class="sxs-lookup"><span data-stu-id="f8e6b-943">GNU</span></span> |

#### <a name="module-linker-for-cortex-r4-using-iar"></a><span data-ttu-id="f8e6b-944">IAR kullanarak Cortex için modül Bağlayıcısı-R4</span><span class="sxs-lookup"><span data-stu-id="f8e6b-944">Module linker for Cortex-R4 using IAR</span></span>

```c
/*###ICF### Section handled by ICF editor, don't touch! ****/
/*-Editor annotation file-*/
/* IcfEditorFile="$TOOLKIT_DIR$\config\ide\IcfEditor\a_v1_0.xml" */
/*-Specials-*/
/*-Memory Regions-*/
define symbol __ICFEDIT_region_ROM_start__ = 0x00100000;
define symbol __ICFEDIT_region_ROM_end__   = 0x0013FFFF;
define symbol __ICFEDIT_region_RAM_start__ = 0x08000000;
define symbol __ICFEDIT_region_RAM_end__   = 0x0800FFFF;
/*-Sizes-*/
define symbol __ICFEDIT_size_cstack__   = 0;
define symbol __ICFEDIT_size_svcstack__ = 0;
define symbol __ICFEDIT_size_irqstack__ = 0;
define symbol __ICFEDIT_size_fiqstack__ = 0;
define symbol __ICFEDIT_size_undstack__ = 0;
define symbol __ICFEDIT_size_abtstack__ = 0;
define symbol __ICFEDIT_size_heap__     = 0x100;
/**** End of ICF editor section. ###ICF###*/

define memory mem with size = 4G;
define region ROM_region   = mem:[from __ICFEDIT_region_ROM_start__   to __ICFEDIT_region_ROM_end__];
define region RAM_region   = mem:[from __ICFEDIT_region_RAM_start__   to __ICFEDIT_region_RAM_end__];

define block HEAP      with alignment = 8, size = __ICFEDIT_size_heap__     { };

initialize by copy { readwrite };
do not initialize  { section .noinit };

define movable block ROPI with alignment = 4, fixed order
{
  ro object txm_module_preamble.o,
  ro,
  ro data
};

define movable block RWPI with alignment = 8, fixed order, static base
{
  rw,
  block HEAP
};

place in ROM_region   { block ROPI };
place in RAM_region   { block RWPI };
```

#### <a name="building-modules-for-cortex-r4-using-iar"></a><span data-ttu-id="f8e6b-945">IAR kullanarak Cortex için modüller oluşturma-R4</span><span class="sxs-lookup"><span data-stu-id="f8e6b-945">Building Modules for Cortex-R4 using IAR</span></span>

<span data-ttu-id="f8e6b-946">Örnek çalışma alanı sağlanır.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-946">An example workspace is provided.</span></span> <span data-ttu-id="f8e6b-947">ThreadX kitaplığı, ThreadX modülleri kitaplığı, demo modülü projesi ve tanıtım modülü Yöneticisi projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-947">Build the ThreadX library, ThreadX Modules library, demo module project, and demo module manager project.</span></span>

#### <a name="thread-extension-definition-for-cortex-r4-using-iar"></a><span data-ttu-id="f8e6b-948">IAR kullanarak Cortex-R4 için iş parçacığı uzantısı tanımı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-948">Thread extension definition for Cortex-R4 using IAR</span></span>

```c
#define TX_THREAD_EXTENSION_2   ULONG   tx_thread_vfp_enable;                   \
                                VOID    *tx_thread_module_instance_ptr;         \
                                VOID    *tx_thread_module_entry_info_ptr;       \
                                ULONG   tx_thread_module_current_user_mode;     \
                                ULONG   tx_thread_module_user_mode;             \
                                VOID    *tx_thread_module_kernel_stack_start;   \
                                VOID    *tx_thread_module_kernel_stack_end;     \
                                ULONG   tx_thread_module_kernel_stack_size;     \
                                VOID    *tx_thread_module_stack_ptr;            \
                                VOID    *tx_thread_module_stack_start;          \
                                VOID    *tx_thread_module_stack_end;            \
                                ULONG   tx_thread_module_stack_size;            \
                                VOID    *tx_thread_module_reserved;             \
                                VOID    *tx_thread_iar_tls_pointer;
```

#### <a name="building-module-manager-for-cortex-r4-using-iar"></a><span data-ttu-id="f8e6b-949">IAR kullanarak Cortex için Modül Yöneticisi oluşturma-R4</span><span class="sxs-lookup"><span data-stu-id="f8e6b-949">Building Module Manager for Cortex-R4 using IAR</span></span>

<span data-ttu-id="f8e6b-950">Örnek çalışma alanı sağlanır.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-950">An example workspace is provided.</span></span> <span data-ttu-id="f8e6b-951">ThreadX kitaplığı, ThreadX modülleri kitaplığı, demo modülü projesi ve tanıtım modülü Yöneticisi projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-951">Build the ThreadX library, ThreadX Modules library, demo module project, and demo module manager project.</span></span>

#### <a name="attributes-for-external-memory-enable-api-for-cortex-r4-using-iar"></a><span data-ttu-id="f8e6b-952">Dış bellek öznitelikleri ıAR kullanarak Cortex için API 'YI etkinleştirir-R4</span><span class="sxs-lookup"><span data-stu-id="f8e6b-952">Attributes for external memory enable API for Cortex-R4 using IAR</span></span>

<span data-ttu-id="f8e6b-953">Modülün paylaşılan belleğe her zaman okuma erişimi vardır.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-953">Module always has read access to shared memory.</span></span>

| <span data-ttu-id="f8e6b-954">Öznitelik parametresi</span><span class="sxs-lookup"><span data-stu-id="f8e6b-954">Attribute parameter</span></span> | <span data-ttu-id="f8e6b-955">Anlamı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-955">Meaning</span></span> |
|---|---|
| <span data-ttu-id="f8e6b-956">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span><span class="sxs-lookup"><span data-stu-id="f8e6b-956">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span></span> | <span data-ttu-id="f8e6b-957">Yazma erişimi</span><span class="sxs-lookup"><span data-stu-id="f8e6b-957">Write access</span></span> |

## <a name="mcf544xx-processor"></a><span data-ttu-id="f8e6b-958">MCF544xx işlemcisi</span><span class="sxs-lookup"><span data-stu-id="f8e6b-958">MCF544xx processor</span></span>

### <a name="mcf544xx-using-ghs"></a><span data-ttu-id="f8e6b-959">GHS kullanarak MCF544xx</span><span class="sxs-lookup"><span data-stu-id="f8e6b-959">MCF544xx using GHS</span></span>

#### <a name="module-preamble-for-mcf544xx-using-ghs"></a><span data-ttu-id="f8e6b-960">GHS kullanarak MCF544xx için modül girişi</span><span class="sxs-lookup"><span data-stu-id="f8e6b-960">Module preamble for MCF544xx using GHS</span></span>

```c
    SECT    .preamble, x

    /* Define public symbols.  */
    XDEF __txm_module_preamble

__txm_module_preamble:
    DC.L    0x4D4F4455                                  /* Module ID                                */
    DC.L    0x5                                         /* Module Major Version                     */
    DC.L    0x3                                         /* Module Minor Version                     */
    DC.L    32                                          /* Module Preamble Size in 32-bit words     */
    DC.L    0x12345678                                  /* Module ID (application defined)          */
    DC.L    0x03000003                                  /* Module Properties where:                 */
                                                        /* Bits 31-24: Compiler ID                  */
                                                        /*           3 -> GHS                       */
                                                        /* Bits 23-2: Reserved                      */
                                                        /* Bit 1:  0 -> No MMU protection           */
                                                        /*         1 -> MMU protection (must have   */
                                                        /*              user mode selected)         */
                                                        /* Bit 0:  0 -> Supervisor mode execution   */
                                                        /*         1 -> User mode execution         */
    DC.L    _txm_module_thread_shell_entry              /* Module Shell Entry Point                 */
    DC.L    demo_module_start                           /* Module Start Thread Entry Point          */
    DC.L    0                                           /* Module Stop Thread Entry Point           */
    DC.L    1                                           /* Module Start/Stop Thread Priority        */
    DC.L    2048                                        /* Module Start/Stop Thread Stack Size      */
    DC.L    _txm_module_callback_request_thread_entry   /* Module Callback Thread Entry             */
    DC.L    1                                           /* Module Callback Thread Priority          */
    DC.L    2048                                        /* Module Callback Thread Stack Size        */
    DC.L    module_code_size                            /* Module Code Size                         */
    DC.L    module_data_size                            /* Module Data Size                         */
    DC.L    0                                           /* Reserved 0                               */
    DC.L    0                                           /* Reserved 1                               */
    DC.L    0                                           /* Reserved 2                               */
    DC.L    0                                           /* Reserved 3                               */
    DC.L    0                                           /* Reserved 4                               */
    DC.L    0                                           /* Reserved 5                               */
    DC.L    0                                           /* Reserved 6                               */
    DC.L    0                                           /* Reserved 7                               */
    DC.L    0                                           /* Reserved 8                               */
    DC.L    0                                           /* Reserved 9                               */
    DC.L    0                                           /* Reserved 10                              */
    DC.L    0                                           /* Reserved 11                              */
    DC.L    0                                           /* Reserved 12                              */
    DC.L    0                                           /* Reserved 13                              */
    DC.L    0                                           /* Reserved 14                              */
    DC.L    0                                           /* Reserved 15                              */

    END
```

#### <a name="module-properties-for-mcf544xx-using-ghs"></a><span data-ttu-id="f8e6b-961">GHS kullanarak MCF544xx için modül özellikleri</span><span class="sxs-lookup"><span data-stu-id="f8e6b-961">Module properties for MCF544xx using GHS</span></span>

| <span data-ttu-id="f8e6b-962">Sürümleri</span><span class="sxs-lookup"><span data-stu-id="f8e6b-962">Bit</span></span> | <span data-ttu-id="f8e6b-963">Değer</span><span class="sxs-lookup"><span data-stu-id="f8e6b-963">Value</span></span> | <span data-ttu-id="f8e6b-964">Anlamı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-964">Meaning</span></span> |
|---|---|---|
| <span data-ttu-id="f8e6b-965">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-965">0</span></span> | <span data-ttu-id="f8e6b-966">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-966">0</span></span><br /><span data-ttu-id="f8e6b-967">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-967">1</span></span> | <span data-ttu-id="f8e6b-968">Ayrıcalıklı mod yürütme</span><span class="sxs-lookup"><span data-stu-id="f8e6b-968">Privileged mode execution</span></span><br /><span data-ttu-id="f8e6b-969">Kullanıcı modu yürütme</span><span class="sxs-lookup"><span data-stu-id="f8e6b-969">User mode execution</span></span> |
| <span data-ttu-id="f8e6b-970">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-970">1</span></span> | <span data-ttu-id="f8e6b-971">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-971">0</span></span><br /><span data-ttu-id="f8e6b-972">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-972">1</span></span> | <span data-ttu-id="f8e6b-973">MMU koruması yok</span><span class="sxs-lookup"><span data-stu-id="f8e6b-973">No MMU protection</span></span><br /><span data-ttu-id="f8e6b-974">MMU koruması (Kullanıcı modunun seçili olması gerekir)</span><span class="sxs-lookup"><span data-stu-id="f8e6b-974">MMU protection (must have user mode selected)</span></span> |
| <span data-ttu-id="f8e6b-975">2</span><span class="sxs-lookup"><span data-stu-id="f8e6b-975">2</span></span> | <span data-ttu-id="f8e6b-976">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-976">0</span></span><br /><span data-ttu-id="f8e6b-977">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-977">1</span></span> | <span data-ttu-id="f8e6b-978">Paylaşılan/dış bellek erişimini devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="f8e6b-978">Disable shared/external memory access</span></span><br /><span data-ttu-id="f8e6b-979">Paylaşılan/dış bellek erişimini etkinleştir</span><span class="sxs-lookup"><span data-stu-id="f8e6b-979">Enable shared/external memory access</span></span> |
| <span data-ttu-id="f8e6b-980">[23-3]</span><span class="sxs-lookup"><span data-stu-id="f8e6b-980">[23-3]</span></span> | <span data-ttu-id="f8e6b-981">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-981">0</span></span> | <span data-ttu-id="f8e6b-982">Ayrılmıştır</span><span class="sxs-lookup"><span data-stu-id="f8e6b-982">Reserved</span></span>
| <span data-ttu-id="f8e6b-983">[31-24]</span><span class="sxs-lookup"><span data-stu-id="f8e6b-983">[31-24]</span></span> | <br /><span data-ttu-id="f8e6b-984">0x03</span><span class="sxs-lookup"><span data-stu-id="f8e6b-984">0x03</span></span> | <span data-ttu-id="f8e6b-985">**Derleyici KIMLIĞI**</span><span class="sxs-lookup"><span data-stu-id="f8e6b-985">**Compiler ID**</span></span><br /><span data-ttu-id="f8e6b-986">GHS</span><span class="sxs-lookup"><span data-stu-id="f8e6b-986">GHS</span></span> |

#### <a name="module-linker-for-mcf544xx-using-ghs"></a><span data-ttu-id="f8e6b-987">GHS kullanarak MCF544xx için modül Bağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-987">Module linker for MCF544xx using GHS</span></span>

```c
DEFAULTS {

    heap_reserve =  256
    stack_reserve = 256
}

//
// Program layout for PIC and PID built programs.
//

-sec
{
//
// The data segment
//
    .pidbase                0x00000000 :
    .sdabase                           :
    .sbss                   NOCLEAR    :
    .sdata                             :
    .data                   NOLOAD     :
    .bss                    NOCLEAR    :
    .heap                   ALIGN(16) PAD( heap_reserve +
        // Add space for call-graph profiling if used:
        (isdefined(__ghs_indgcount)?(2000+(sizeof(.text)/2)):0) +
        // Add estimated space for call-count profiling if used:
        (isdefined(__ghs_indmcount)?10000:0) )
                                             :
    .stack      ALIGN(16) PAD(stack_reserve) :

    module_data_size = sizeof(.pidbase) + sizeof(.sdabase) + sizeof(.sbss) + sizeof(.sdata) + sizeof(.data) + sizeof(.bss) + sizeof(.heap) + sizeof(.stack);

//
// The code segment
//

    .picbase                0x00000000 :
    .preamble                          :
    .text                              :
    .syscall                           :
    .fixaddr                           :
    .fixtype                           :
    .rodata                            :
    .ROM.data               ROM(.data) :
    .secinfo                           :

    module_code_size =  endaddr(.secinfo);
}
```

#### <a name="building-modules-for-mcf544xx-using-ghs"></a><span data-ttu-id="f8e6b-988">GHS kullanarak MCF544xx için modüller oluşturma</span><span class="sxs-lookup"><span data-stu-id="f8e6b-988">Building Modules for MCF544xx using GHS</span></span>

<span data-ttu-id="f8e6b-989">Örnek çalışma alanı sağlanır.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-989">An example workspace is provided.</span></span> <span data-ttu-id="f8e6b-990">ThreadX kitaplığı, ThreadX modülleri kitaplığı, demo modülü projesi ve tanıtım modülü Yöneticisi projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-990">Build the ThreadX library, ThreadX Modules library, demo module project, and demo module manager project.</span></span>

#### <a name="thread-extension-definition-for-mcf544xx-using-ghs"></a><span data-ttu-id="f8e6b-991">GHS kullanarak MCF544xx için iş parçacığı uzantısı tanımı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-991">Thread extension definition for MCF544xx using GHS</span></span>

```c
#define TX_THREAD_EXTENSION_2   int     Errno;                                  \
                                VOID    *tx_thread_module_instance_ptr;         \
                                VOID    *tx_thread_module_entry_info_ptr;       \
                                ULONG   tx_thread_module_current_user_mode;     \
                                ULONG   tx_thread_module_user_mode;             \
                                ULONG   tx_thread_module_mmu_protection;        \
                                VOID *  tx_thread_module_dispatch_return;       \
                                VOID    *tx_thread_module_kernel_stack_start;   \
                                VOID    *tx_thread_module_kernel_stack_end;     \
                                ULONG   tx_thread_module_kernel_stack_size;     \
                                VOID    *tx_thread_module_stack_ptr;            \
                                VOID    *tx_thread_module_stack_start;          \
                                VOID    *tx_thread_module_stack_end;            \
                                ULONG   tx_thread_module_stack_size;            \
                                VOID    *tx_thread_module_reserved;
```

#### <a name="building-module-manager-for-mcf544xx-using-ghs"></a><span data-ttu-id="f8e6b-992">GHS kullanarak MCF544xx için Modül Yöneticisi derleniyor</span><span class="sxs-lookup"><span data-stu-id="f8e6b-992">Building Module Manager for MCF544xx using GHS</span></span>

<span data-ttu-id="f8e6b-993">Örnek çalışma alanı sağlanır.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-993">An example workspace is provided.</span></span> <span data-ttu-id="f8e6b-994">ThreadX kitaplığı, ThreadX modülleri kitaplığı, demo modülü projesi ve tanıtım modülü Yöneticisi projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-994">Build the ThreadX library, ThreadX Modules library, demo module project, and demo module manager project.</span></span>

#### <a name="attributes-for-external-memory-enable-api-for-mcf544xx-using-ghs"></a><span data-ttu-id="f8e6b-995">Dış bellek öznitelikleri, GHS kullanarak MCF544xx için API 'YI etkinleştirir</span><span class="sxs-lookup"><span data-stu-id="f8e6b-995">Attributes for external memory enable API for MCF544xx using GHS</span></span>

<span data-ttu-id="f8e6b-996">Bu özellik MCF544xx üzerinde etkin değil.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-996">This feature not enabled on MCF544xx.</span></span>

## <a name="rx63-processor"></a><span data-ttu-id="f8e6b-997">RX63 işlemcisi</span><span class="sxs-lookup"><span data-stu-id="f8e6b-997">RX63 processor</span></span>

### <a name="rx63-using-iar"></a><span data-ttu-id="f8e6b-998">IAR kullanarak RX63</span><span class="sxs-lookup"><span data-stu-id="f8e6b-998">RX63 using IAR</span></span>

#### <a name="module-preamble-for-rx63-using-iar"></a><span data-ttu-id="f8e6b-999">IAR kullanarak RX63 için modül girişi</span><span class="sxs-lookup"><span data-stu-id="f8e6b-999">Module preamble for RX63 using IAR</span></span>

```c
    /* Alignment of 4 (16-byte) */
    SECTION .text:CODE (4)

    /* Define public symbols.  */
    PUBLIC __txm_module_preamble

    /* Define application-specific start/stop entry points for the module.  */
    EXTERN _demo_module_start

    /* Define common external references.  */
    EXTERN  __txm_module_thread_shell_entry
    EXTERN  __txm_module_callback_request_thread_entry
    EXTERN  ROPI$$Length
    EXTERN  RWPI$$Length

    DATA
__txm_module_preamble:
    DC32      0x4D4F4455                                        // Module ID
    DC32      0x5                                               // Module Major Version
    DC32      0x6                                               // Module Minor Version
    DC32      32                                                // Module Preamble Size in 32-bit words
    DC32      0x12345678                                        // Module ID (application defined)
    DC32      0x00000007                                        // Module Properties where:
                                                                //   Bits 31-24: Compiler ID
                                                                //           0 -> IAR
                                                                //           1 -> ARM
                                                                //           2 -> GNU
                                                                //   Bit 0:  0 -> Privileged mode execution
                                                                //           1 -> User mode execution
                                                                //   Bit 1:  0 -> No MPU protection
                                                                //           1 -> MPU protection (must have user mode selected)
                                                                //   Bit 2:  0 -> Disable shared/external memory access
                                                                //           1 -> Enable shared/external memory access
    DC32      __txm_module_thread_shell_entry - $               // Module Shell Entry Point
    DC32      _demo_module_start - $                            // Module Start Thread Entry Point
    DC32      0                                                 // Module Stop Thread Entry Point
    DC32      1                                                 // Module Start/Stop Thread Priority
    DC32      1024                                              // Module Start/Stop Thread Stack Size
    DC32      __txm_module_callback_request_thread_entry - $    // Module Callback Thread Entry
    DC32      1                                                 // Module Callback Thread Priority
    DC32      1024                                              // Module Callback Thread Stack Size
    DC32      ROPI$$Length                                      // Module Code Size
    DC32      RWPI$$Length                                      // Module Data Size
    DC32      0                                                 // Reserved 0
    DC32      0                                                 // Reserved 1
    DC32      0                                                 // Reserved 2
    DC32      0                                                 // Reserved 3
    DC32      0                                                 // Reserved 4
    DC32      0                                                 // Reserved 5
    DC32      0                                                 // Reserved 6
    DC32      0                                                 // Reserved 7
    DC32      0                                                 // Reserved 8  
    DC32      0                                                 // Reserved 9
    DC32      0                                                 // Reserved 10
    DC32      0                                                 // Reserved 11
    DC32      0                                                 // Reserved 12
    DC32      0                                                 // Reserved 13
    DC32      0                                                 // Reserved 14
    DC32      0                                                 // Reserved 15

    END
```

#### <a name="module-properties-for-rx63-using-iar"></a><span data-ttu-id="f8e6b-1000">IAR kullanarak RX63 için modül özellikleri</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1000">Module properties for RX63 using IAR</span></span>

| <span data-ttu-id="f8e6b-1001">Sürümleri</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1001">Bit</span></span> | <span data-ttu-id="f8e6b-1002">Değer</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1002">Value</span></span> | <span data-ttu-id="f8e6b-1003">Anlamı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1003">Meaning</span></span> |
|---|---|---|
| <span data-ttu-id="f8e6b-1004">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1004">0</span></span> | <span data-ttu-id="f8e6b-1005">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1005">0</span></span><br /><span data-ttu-id="f8e6b-1006">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1006">1</span></span> | <span data-ttu-id="f8e6b-1007">Ayrıcalıklı mod yürütme</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1007">Privileged mode execution</span></span><br /><span data-ttu-id="f8e6b-1008">Kullanıcı modu yürütme</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1008">User mode execution</span></span> |
| <span data-ttu-id="f8e6b-1009">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1009">1</span></span> | <span data-ttu-id="f8e6b-1010">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1010">0</span></span><br /><span data-ttu-id="f8e6b-1011">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1011">1</span></span> | <span data-ttu-id="f8e6b-1012">MPU koruması yok</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1012">No MPU protection</span></span><br /><span data-ttu-id="f8e6b-1013">MPU koruması (Kullanıcı modunun seçili olması gerekir)</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1013">MPU protection (must have user mode selected)</span></span> |
| <span data-ttu-id="f8e6b-1014">2</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1014">2</span></span> | <span data-ttu-id="f8e6b-1015">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1015">0</span></span><br /><span data-ttu-id="f8e6b-1016">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1016">1</span></span> | <span data-ttu-id="f8e6b-1017">Paylaşılan/dış bellek erişimini devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1017">Disable shared/external memory access</span></span><br /><span data-ttu-id="f8e6b-1018">Paylaşılan/dış bellek erişimini etkinleştir</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1018">Enable shared/external memory access</span></span> |
| <span data-ttu-id="f8e6b-1019">[23-3]</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1019">[23-3]</span></span> | <span data-ttu-id="f8e6b-1020">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1020">0</span></span> | <span data-ttu-id="f8e6b-1021">Ayrılmıştır</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1021">Reserved</span></span>
| <span data-ttu-id="f8e6b-1022">[31-24]</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1022">[31-24]</span></span> | <br /><span data-ttu-id="f8e6b-1023">-</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1023">0x00</span></span><br /><span data-ttu-id="f8e6b-1024">0x02</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1024">0x02</span></span> | <span data-ttu-id="f8e6b-1025">**Derleyici KIMLIĞI**</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1025">**Compiler ID**</span></span><br /><span data-ttu-id="f8e6b-1026">IAR dili</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1026">IAR</span></span><br /><span data-ttu-id="f8e6b-1027">GNU</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1027">GNU</span></span> |

#### <a name="module-linker-for-rx63-using-iar"></a><span data-ttu-id="f8e6b-1028">IAR kullanarak RX63 için modül Bağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1028">Module linker for RX63 using IAR</span></span>

```c
//-----------------------------------------------------------------------------
// ILINK command file template for the Renesas RX microcontroller R5F563NB
//-----------------------------------------------------------------------------
define exported symbol __link_file_version_4 = 1;

define memory mem with size = 4G;

// ID Code Protection
define exported symbol __ID_BYTES_1_4   = 0xFFFFFFFF;
define exported symbol __ID_BYTES_5_8   = 0xFFFFFFFF;
define exported symbol __ID_BYTES_9_12  = 0xFFFFFFFF;
define exported symbol __ID_BYTES_13_16 = 0xFFFFFFFF;

// Endian Select Register (MDE)
// Choose between Little endian=0xFFFFFFFF or Big endian=0xFFFFFFF8
define exported symbol __MDES           = 0xFFFFFFFF;

// Option Function Select Register 0 (OFS0)
define exported symbol __OFS0           = 0xFFFFFFFF;

// Option Function Select Register 1 (OFS1)
define exported symbol __OFS1           = 0xFFFFFFFF;

//define region ROM_region16 = mem:[from 0xFFFF8000 to 0xFFFFFFFF];
define region RAM_region16 = mem:[from 0x00010000 to 0x00017FFF];
//define region ROM_region24 = mem:[from 0xFFF00000 to 0xFFFFFFFF];
//define region RAM_region24 = mem:[from 0x00000004 to 0x0001FFFF];
define region ROM_region32 = mem:[from 0xFFF10400 to 0xFFFFFFFF];
//define region RAM_region32 = mem:[from 0x00000004 to 0x0001FFFF];
//define region DATA_FLASH_region = mem:[from 0x00100000 to 0x00107FFF];

initialize by copy { rw, ro section D, ro section D_1, ro section D_2 };
do not initialize  { section .*.noinit };

define block HEAP     with alignment = 4, size = _HEAP_SIZE { };
//define block USTACK   with alignment = 4, size = _USTACK_SIZE { };
//define block ISTACK   with alignment = 4, size = _ISTACK_SIZE { };

//define block STACKS with fixed order { block ISTACK,
//                                       block USTACK };

//place at address mem:0xFFFFFF80 { ro section .nmivec };
//"ROM16":place in ROM_region16        { ro section .code16*,
//                                       ro section .data16* };
//"RAM16":place in RAM_region16        { rw section .data16*,
//                                       rw section __DLIB_PERTHREAD };
//"ROM24":place in ROM_region24        { ro section .code24*,
//                                       ro section .data24* };
//"RAM24":place in RAM_region24        { rw section .data24* };
//"ROM32":place in ROM_region32        { ro };
//"RAM32":place in RAM_region32        { rw,
//                                       ro section D,
//                                       ro section D_1,
//                                       ro section D_2,
//                                       block HEAP,
//                                       block STACKS,
//                                       last section FREEMEM };

//"DATAFLASH":place in DATA_FLASH_region
//                                     { ro section .dataflash* };

define movable block ROPI with alignment = 4, fixed order, static base CB
{
  ro object txm_module_preamble_rx63n.o,
  ro,
  ro data
};

define movable block RWPI with alignment = 8, fixed order, static base SB
{
  rw section .sbdata*,
  rw section .sbrel*,
  rw section __DLIB_PERTHREAD,
  block HEAP
};

place in ROM_region32   { block ROPI };
place in RAM_region16   { block RWPI };
```

#### <a name="building-modules-for-rx63-using-iar"></a><span data-ttu-id="f8e6b-1029">IAR kullanarak RX63 için modüller oluşturma</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1029">Building Modules for RX63 using IAR</span></span>

<span data-ttu-id="f8e6b-1030">Örnek çalışma alanı sağlanır.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1030">An example workspace is provided.</span></span> <span data-ttu-id="f8e6b-1031">ThreadX kitaplığı, ThreadX modülleri kitaplığı, demo modülü projesi ve tanıtım modülü Yöneticisi projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1031">Build the ThreadX library, ThreadX Modules library, demo module project, and demo module manager project.</span></span>

#### <a name="thread-extension-definition-for-rxrx635n-using-iar"></a><span data-ttu-id="f8e6b-1032">IAR kullanarak RXRX635N için iş parçacığı uzantısı tanımı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1032">Thread extension definition for RXRX635N using IAR</span></span>

```c
#define TX_THREAD_EXTENSION_2   VOID    *tx_thread_module_instance_ptr;       \
                                VOID    *tx_thread_module_entry_info_ptr;     \
                                ULONG   tx_thread_module_current_user_mode;   \
                                ULONG   tx_thread_module_user_mode;           \
                                VOID    *tx_thread_module_kernel_stack_start; \
                                VOID    *tx_thread_module_kernel_stack_end;   \
                                ULONG   tx_thread_module_kernel_stack_size;   \
                                VOID    *tx_thread_module_stack_ptr;          \
                                VOID    *tx_thread_module_stack_start;        \
                                VOID    *tx_thread_module_stack_end;          \
                                ULONG   tx_thread_module_stack_size;          \
                                VOID    *tx_thread_module_reserved;           \
                                VOID    *tx_thread_iar_tls_pointer;
```

#### <a name="building-module-manager-for-rx63-using-iar"></a><span data-ttu-id="f8e6b-1033">IAR kullanarak RX63 için Modül Yöneticisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1033">Building Module Manager for RX63 using IAR</span></span>

<span data-ttu-id="f8e6b-1034">Örnek çalışma alanı sağlanır.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1034">An example workspace is provided.</span></span> <span data-ttu-id="f8e6b-1035">ThreadX kitaplığı, ThreadX modülleri kitaplığı, demo modülü projesi ve tanıtım modülü Yöneticisi projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1035">Build the ThreadX library, ThreadX Modules library, demo module project, and demo module manager project.</span></span>

#### <a name="attributes-for-external-memory-enable-api-for-rx63-using-iar"></a><span data-ttu-id="f8e6b-1036">Dış bellek öznitelikleri ıAR kullanarak RX63 için API 'YI etkinleştirir</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1036">Attributes for external memory enable API for RX63 using IAR</span></span>

| <span data-ttu-id="f8e6b-1037">Öznitelik parametresi</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1037">Attribute Parameter</span></span> | <span data-ttu-id="f8e6b-1038">Anlamı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1038">Meaning</span></span> |
|---|---|
| <span data-ttu-id="f8e6b-1039">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_EXECUTE</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1039">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_EXECUTE</span></span> | <span data-ttu-id="f8e6b-1040">Kodu Yürüt</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1040">Execute code</span></span> |
| <span data-ttu-id="f8e6b-1041">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1041">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span></span> | <span data-ttu-id="f8e6b-1042">Yazma erişimi</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1042">Write access</span></span> |
| <span data-ttu-id="f8e6b-1043">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_READ</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1043">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_READ</span></span> | <span data-ttu-id="f8e6b-1044">Okuma erişimi</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1044">Read access</span></span> |

## <a name="rx65n-processor"></a><span data-ttu-id="f8e6b-1045">RX65N işlemcisi</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1045">RX65N processor</span></span>

### <a name="rx65n-using-iar"></a><span data-ttu-id="f8e6b-1046">IAR kullanarak RX65N</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1046">RX65N using IAR</span></span>

#### <a name="module-preamble-for-rx65n-using-iar"></a><span data-ttu-id="f8e6b-1047">IAR kullanarak RX65N için modül girişi</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1047">Module preamble for RX65N using IAR</span></span>

```c
    /* Alignment of 4 (16-byte) */
    SECTION .text:CODE (4)

    /* Define public symbols.  */
    PUBLIC __txm_module_preamble

    /* Define application-specific start/stop entry points for the module.  */
    EXTERN _demo_module_start

    /* Define common external references.  */
    EXTERN  __txm_module_thread_shell_entry
    EXTERN  __txm_module_callback_request_thread_entry
    EXTERN  ROPI$$Length
    EXTERN  RWPI$$Length

    DATA
__txm_module_preamble:
    DC32      0x4D4F4455                                        // Module ID
    DC32      0x5                                               // Module Major Version
    DC32      0x6                                               // Module Minor Version
    DC32      32                                                // Module Preamble Size in 32-bit words
    DC32      0x12345678                                        // Module ID (application defined)
    DC32      0x00000007                                        // Module Properties where:
                                                                //   Bits 31-24: Compiler ID
                                                                //           0 -> IAR
                                                                //           1 -> ARM
                                                                //           2 -> GNU
                                                                //   Bit 0:  0 -> Privileged mode execution
                                                                //           1 -> User mode execution
                                                                //   Bit 1:  0 -> No MPU protection
                                                                //           1 -> MPU protection (must have user mode selected)
                                                                //   Bit 2:  0 -> Disable shared/external memory access
                                                                //           1 -> Enable shared/external memory access
    DC32      __txm_module_thread_shell_entry - $               // Module Shell Entry Point
    DC32      _demo_module_start - $                            // Module Start Thread Entry Point
    DC32      0                                                 // Module Stop Thread Entry Point
    DC32      1                                                 // Module Start/Stop Thread Priority
    DC32      1024                                              // Module Start/Stop Thread Stack Size
    DC32      __txm_module_callback_request_thread_entry - $    // Module Callback Thread Entry
    DC32      1                                                 // Module Callback Thread Priority
    DC32      1024                                              // Module Callback Thread Stack Size
    DC32      ROPI$$Length                                      // Module Code Size
    DC32      RWPI$$Length                                      // Module Data Size
    DC32      0                                                 // Reserved 0
    DC32      0                                                 // Reserved 1
    DC32      0                                                 // Reserved 2
    DC32      0                                                 // Reserved 3
    DC32      0                                                 // Reserved 4
    DC32      0                                                 // Reserved 5
    DC32      0                                                 // Reserved 6
    DC32      0                                                 // Reserved 7
    DC32      0                                                 // Reserved 8  
    DC32      0                                                 // Reserved 9
    DC32      0                                                 // Reserved 10
    DC32      0                                                 // Reserved 11
    DC32      0                                                 // Reserved 12
    DC32      0                                                 // Reserved 13
    DC32      0                                                 // Reserved 14
    DC32      0                                                 // Reserved 15

    END
```

#### <a name="module-properties-for-rx65n-using-iar"></a><span data-ttu-id="f8e6b-1048">IAR kullanarak RX65N için modül özellikleri</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1048">Module properties for RX65N using IAR</span></span>

| <span data-ttu-id="f8e6b-1049">Sürümleri</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1049">Bit</span></span> | <span data-ttu-id="f8e6b-1050">Değer</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1050">Value</span></span> | <span data-ttu-id="f8e6b-1051">Anlamı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1051">Meaning</span></span> |
|---|---|---|
| <span data-ttu-id="f8e6b-1052">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1052">0</span></span> | <span data-ttu-id="f8e6b-1053">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1053">0</span></span><br /><span data-ttu-id="f8e6b-1054">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1054">1</span></span> | <span data-ttu-id="f8e6b-1055">Ayrıcalıklı mod yürütme</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1055">Privileged mode execution</span></span><br /><span data-ttu-id="f8e6b-1056">Kullanıcı modu yürütme</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1056">User mode execution</span></span> |
| <span data-ttu-id="f8e6b-1057">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1057">1</span></span> | <span data-ttu-id="f8e6b-1058">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1058">0</span></span><br /><span data-ttu-id="f8e6b-1059">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1059">1</span></span> | <span data-ttu-id="f8e6b-1060">MPU koruması yok</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1060">No MPU protection</span></span><br /><span data-ttu-id="f8e6b-1061">MPU koruması (Kullanıcı modunun seçili olması gerekir)</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1061">MPU protection (must have user mode selected)</span></span> |
| <span data-ttu-id="f8e6b-1062">2</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1062">2</span></span> | <span data-ttu-id="f8e6b-1063">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1063">0</span></span><br /><span data-ttu-id="f8e6b-1064">1</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1064">1</span></span> | <span data-ttu-id="f8e6b-1065">Paylaşılan/dış bellek erişimini devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1065">Disable shared/external memory access</span></span><br /><span data-ttu-id="f8e6b-1066">Paylaşılan/dış bellek erişimini etkinleştir</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1066">Enable shared/external memory access</span></span> |
| <span data-ttu-id="f8e6b-1067">[23-3]</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1067">[23-3]</span></span> | <span data-ttu-id="f8e6b-1068">0</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1068">0</span></span> | <span data-ttu-id="f8e6b-1069">Ayrılmıştır</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1069">Reserved</span></span>
| <span data-ttu-id="f8e6b-1070">[31-24]</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1070">[31-24]</span></span> | <br /><span data-ttu-id="f8e6b-1071">-</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1071">0x00</span></span><br /><span data-ttu-id="f8e6b-1072">0x02</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1072">0x02</span></span> | <span data-ttu-id="f8e6b-1073">**Derleyici KIMLIĞI**</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1073">**Compiler ID**</span></span><br /><span data-ttu-id="f8e6b-1074">IAR dili</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1074">IAR</span></span><br /><span data-ttu-id="f8e6b-1075">GNU</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1075">GNU</span></span> |

#### <a name="module-linker-for-rx65n-using-iar"></a><span data-ttu-id="f8e6b-1076">IAR kullanarak RX65N için modül Bağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1076">Module linker for RX65N using IAR</span></span>

```c
//-----------------------------------------------------------------------------
// ILINK command file template for the Renesas RX microcontroller R5F565N
//-----------------------------------------------------------------------------
define exported symbol __link_file_version_4 = 1;

define memory mem with size = 4G;

// ID Code Protection
define exported symbol __ID_BYTES_1_4   = 0xFFFFFFFF;
define exported symbol __ID_BYTES_5_8   = 0xFFFFFFFF;
define exported symbol __ID_BYTES_9_12  = 0xFFFFFFFF;
define exported symbol __ID_BYTES_13_16 = 0xFFFFFFFF;

// Endian Select Register (MDE)
// Choose between Little endian=0xFFFFFFFF or Big endian=0xFFFFFFF8
define exported symbol __MDES           = 0xFFFFFFFF;

// Option Function Select Register 0 (OFS0)
define exported symbol __OFS0           = 0xFFFFFFFF;

// Option Function Select Register 1 (OFS1)
define exported symbol __OFS1           = 0xFFFFFFFF;

//define region ROM_region16 = mem:[from 0xFFFF8000 to 0xFFFFFFFF];
define region RAM_region16 = mem:[from 0x00010000 to 0x00017FFF];
//define region ROM_region24 = mem:[from 0xFFF00000 to 0xFFFFFFFF];
//define region RAM_region24 = mem:[from 0x00000004 to 0x0001FFFF];
define region ROM_region32 = mem:[from 0xFFF10400 to 0xFFFFFFFF];
//define region RAM_region32 = mem:[from 0x00000004 to 0x0001FFFF];
//define region DATA_FLASH_region = mem:[from 0x00100000 to 0x00107FFF];

initialize by copy { rw, ro section D, ro section D_1, ro section D_2 };
do not initialize  { section .*.noinit };

define block HEAP     with alignment = 4, size = _HEAP_SIZE { };
//define block USTACK   with alignment = 4, size = _USTACK_SIZE { };
//define block ISTACK   with alignment = 4, size = _ISTACK_SIZE { };

//define block STACKS with fixed order { block ISTACK,
//                                       block USTACK };

//place at address mem:0xFFFFFF80 { ro section .nmivec };
//"ROM16":place in ROM_region16        { ro section .code16*,
//                                       ro section .data16* };
//"RAM16":place in RAM_region16        { rw section .data16*,
//                                       rw section __DLIB_PERTHREAD };
//"ROM24":place in ROM_region24        { ro section .code24*,
//                                       ro section .data24* };
//"RAM24":place in RAM_region24        { rw section .data24* };
//"ROM32":place in ROM_region32        { ro };
//"RAM32":place in RAM_region32        { rw,
//                                       ro section D,
//                                       ro section D_1,
//                                       ro section D_2,
//                                       block HEAP,
//                                       block STACKS,
//                                       last section FREEMEM };

//"DATAFLASH":place in DATA_FLASH_region
//                                     { ro section .dataflash* };

define movable block ROPI with alignment = 4, fixed order, static base CB
{
  ro object txm_module_preamble_rx65n.o,
  ro,
  ro data
};

define movable block RWPI with alignment = 8, fixed order, static base SB
{
  rw section .sbdata*,
  rw section .sbrel*,
  rw section __DLIB_PERTHREAD,
  block HEAP
};

place in ROM_region32   { block ROPI };
place in RAM_region16   { block RWPI };
```

#### <a name="building-modules-for-rx65n-using-iar"></a><span data-ttu-id="f8e6b-1077">IAR kullanarak RX65N için modüller oluşturma</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1077">Building Modules for RX65N using IAR</span></span>

<span data-ttu-id="f8e6b-1078">Örnek çalışma alanı sağlanır.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1078">An example workspace is provided.</span></span> <span data-ttu-id="f8e6b-1079">ThreadX kitaplığı, ThreadX modülleri kitaplığı, demo modülü projesi ve tanıtım modülü Yöneticisi projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1079">Build the ThreadX library, ThreadX Modules library, demo module project, and demo module manager project.</span></span>

#### <a name="thread-extension-definition-for-rx65n-using-iar"></a><span data-ttu-id="f8e6b-1080">IAR kullanarak RX65N için iş parçacığı uzantısı tanımı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1080">Thread extension definition for RX65N using IAR</span></span>

```c
#define TX_THREAD_EXTENSION_2   VOID    *tx_thread_module_instance_ptr;         \
                                VOID    *tx_thread_module_entry_info_ptr;       \
                                ULONG   tx_thread_module_current_user_mode;     \
                                ULONG   tx_thread_module_user_mode;             \
                                VOID    *tx_thread_module_kernel_stack_start;   \
                                VOID    *tx_thread_module_kernel_stack_end;     \
                                ULONG   tx_thread_module_kernel_stack_size;     \
                                VOID    *tx_thread_module_stack_ptr;            \
                                VOID    *tx_thread_module_stack_start;          \
                                VOID    *tx_thread_module_stack_end;            \
                                ULONG   tx_thread_module_stack_size;            \
                                VOID    *tx_thread_module_reserved;             \
                                VOID    *tx_thread_iar_tls_pointer;
```

#### <a name="building-module-manager-for-rx65n-using-iar"></a><span data-ttu-id="f8e6b-1081">IAR kullanarak RX65N için Modül Yöneticisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1081">Building Module Manager for RX65N using IAR</span></span>

<span data-ttu-id="f8e6b-1082">Örnek çalışma alanı sağlanır.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1082">An example workspace is provided.</span></span> <span data-ttu-id="f8e6b-1083">ThreadX kitaplığı, ThreadX modülleri kitaplığı, demo modülü projesi ve tanıtım modülü Yöneticisi projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1083">Build the ThreadX library, ThreadX Modules library, demo module project, and demo module manager project.</span></span>

#### <a name="attributes-for-external-memory-enable-api-for-rx65n-using-iar"></a><span data-ttu-id="f8e6b-1084">Dış bellek öznitelikleri ıAR kullanarak RX65N için API 'YI etkinleştirir</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1084">Attributes for external memory enable API for RX65N using IAR</span></span>

| <span data-ttu-id="f8e6b-1085">Öznitelik parametresi</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1085">Attribute Parameter</span></span> | <span data-ttu-id="f8e6b-1086">Anlamı</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1086">Meaning</span></span> |
|---|---|
| <span data-ttu-id="f8e6b-1087">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_EXECUTE</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1087">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_EXECUTE</span></span> | <span data-ttu-id="f8e6b-1088">Kodu Yürüt</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1088">Execute code</span></span> |
| <span data-ttu-id="f8e6b-1089">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1089">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span></span> | <span data-ttu-id="f8e6b-1090">Yazma erişimi</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1090">Write access</span></span> |
| <span data-ttu-id="f8e6b-1091">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_READ</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1091">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_READ</span></span> | <span data-ttu-id="f8e6b-1092">Okuma erişimi</span><span class="sxs-lookup"><span data-stu-id="f8e6b-1092">Read access</span></span> |
