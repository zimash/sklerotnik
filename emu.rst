===========================================================================================
Documentation and resources about emulators, implementations, hardware specifications, etc.
===========================================================================================
* `How To Write a Computer Emulator <https://fms.komkon.org/EMUL8/HOWTO.html>`_

===========
ZX Spectrum
===========
* `16K / 48K ZX Spectrum Reference <https://worldofspectrum.org/faq/reference/48kreference.htm>`_

======
Chip-8
======
* `Cowgod's Chip-8 Technical Reference v1.0 <http://devernay.free.fr/hacks/chip8/C8TECH10.HTM>`_

====
QEMU
====
.. code-block:: shell

  # View QOM composition tree and device tree:
  $ qemu-system-x86_64 -M q35 -s -S -monitor stdio # Run qemu as pc-q35 machine (-M q35)
                                                   # with freeze CPU at startup (-S), 
                                                   # with redirected monitor to stdio (-monitor stdio),
                                                   # with  -gdb tcp::1234
  QEMU 9.0.2 monitor - type 'help' for more information
  (qemu) info qom-tree                                                        
  /machine (pc-q35-9.0-machine)     
    /fw_cfg (fw_cfg_io)                                                                                                             
      /\x2from@etc\x2facpi\x2frsdp[0] (memory-region)
      /\x2from@etc\x2facpi\x2ftables[0] (memory-region)                       
      /\x2from@etc\x2ftable-loader[0] (memory-region)
      /fwcfg.dma[0] (memory-region)                                                                                                 
      /fwcfg[0] (memory-region)                 
    /peripheral (container)                                
    ...
  (qemu) info qtree                 
  bus: main-system-bus               
    type System                                                                                                                         
    dev: ps2-mouse, id ""        
      gpio-out "" 1             
    dev: ps2-kbd, id ""         
      gpio-out "" 1           
    dev: hpet, id ""                    
      gpio-in "" 2                         
      gpio-out "" 1                
      gpio-out "sysbus-irq" 32               
      timers = 3 (0x3)                
      msi = false                  
      hpet-intcap = 4 (0x4)               
      hpet-offset-saved = true         
      mmio 00000000fed00000/0000000000000400
    dev: ioapic, id ""                       
...


* `QEMU internals (airbus-seclab) <https://airbus-seclab.github.io/qemu_blog/>`_
* `qemu tag (How to add a new architecture to QEMU - Parts 1, 2, 3, 4) <https://fgoehler.com/blog/category/qemu/>`_
* `Внутреннее устройство эмулятора процессора на архитектуре RISC-V для портирования, разработки и отладки ПО (YADRO) <https://osday.ru/2023/presentations/burlaka.pdf>`_
* `Игра в имитацию: как разрабатывать и отлаживать ПО для процессора, которого нет <https://habr.com/en/companies/yadro/articles/776252/>`_
* `Operating System in 1,000 Lines (EN) <https://operating-system-in-1000-lines.vercel.app/en/>`_
* `Операционная система в 1 000 строках кода (часть 1) (RU) В пяти частях <https://habr.com/ru/companies/ruvds/articles/874154/>`_


Links
-----

* `General Buildroot usage <https://bootlin.com/~thomas/site/buildroot/common-usage.html>`_
