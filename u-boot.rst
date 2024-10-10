==========
Das U-Boot
==========

sandbox/sandbox64
=================

.. code-block:: shell

  $ make sandbox64_defconfig
  $ make menuconfig # optional
  $ make -j $(nproc --all)
  $ ./u-boot


Board Initialisation Flow:
==========================

**lowlevel_init():**

- purpose: essential init to permit execution to reach board_init_f()
- no global_data or BSS
- there is no stack (ARMv7 may have one but it will soon be removed)
- must not set up SDRAM or use console
- must only do the bare minimum to allow execution to continue to
  board_init_f()
- this is almost never needed
- return normally from this function
**board_init_f()**:

- purpose: set up the machine ready for running board_init_r():

  i.e. SDRAM and serial UART
- global_data is available
- stack is in SRAM
- BSS is not available, so you cannot use global/static variables,

  only stack variables and global_data

  Non-SPL-specific notes:

- dram_init() is called to set up DRAM. If already done in SPL this
  can do nothing

  SPL-specific notes:
        
- you can override the entire board_init_f() function with your own
  version as needed.
- preloader_console_init() can be called here in extremis
- should set up SDRAM, and anything needed to make the UART work
- there is no need to clear BSS, it will be done by crt0.S
- for specific scenarios on certain architectures an early BSS *can*
  be made available (via CONFIG_SPL_EARLY_BSS by moving the clearing
  of BSS prior to entering board_init_f()) but doing so is discouraged.
  Instead it is strongly recommended to architect any code changes
  or additions such to not depend on the availability of BSS during
  board_init_f() as indicated in other sections of this README to
  maintain compatibility and consistency across the entire code base.
- must return normally from this function (don't call board_init_r()
  directly)

**board_init_r()**:

- purpose: main execution, common code
- global_data is available
- SDRAM is available
- BSS is available, all static/global variables can be used
- execution eventually continues to main_loop()

Non-SPL-specific notes:

- U-Boot is relocated to the top of memory and is now running from there.

SPL-specific notes:

- stack is optionally in SDRAM, if CONFIG_SPL_STACK_R is defined and CONFIG_SYS_FSL_HAS_CCI400

  Defined For SoC that has cache coherent interconnect CCN-400

  CONFIG_SYS_FSL_HAS_CCN504

  Defined for SoC that has cache coherent interconnect CCN-504


tftp
====

