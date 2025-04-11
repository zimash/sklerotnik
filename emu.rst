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

  # View QEMU device tree:
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
* `QEMU internals (airbus-seclab) <https://airbus-seclab.github.io/qemu_blog/>`_
* `qemu tag (How to add a new architecture to QEMU - Parts 1, 2, 3, 4) <https://fgoehler.com/blog/category/qemu/>`_


   

Links
-----

* `General Buildroot usage <https://bootlin.com/~thomas/site/buildroot/common-usage.html>`_
