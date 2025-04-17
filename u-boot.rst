==========
Das U-Boot
==========

useful commands
===============

setenv xtrace yes
-----------------

Command execution tracer. Print all args in common/command.c/cmd_process (Symbol SYS_XTRACE in config). Example: 

.. code-block:: shell

  Hit any key to stop autoboot:  0
  => setenv xtrace yes
  => boot
  + boot
  + bootflow scan -lb
  Scanning for bootflows in all bootdevs
  Seq  Method       State   Uclass    Part  Name                      Filename                                                          
  ---  -----------  ------  --------  ----  ------------------------  ----------------   
  

sandbox/sandbox64
=================

.. code-block:: shell

  $ make sandbox64_defconfig
  $ make menuconfig # optional
  $ make -j $(nproc --all)
  $ ./u-boot

Driver model
============

Uclass

    a group of devices which operate in the same way. A uclass provides a way of accessing individual devices within the group, but always using the same interface. For example a GPIO uclass provides operations for get/set value. An I2C uclass may have 10 I2C ports, 4 with one driver, and 6 with another.

Driver

    some code which talks to a peripheral and presents a higher-level interface to it.
Device

    an instance of a driver, tied to a particular port or peripheral.


Failure to locate a device
==========================

Sometimes we have to check if the device is actually bound. Call dm_dump_all() just before you locate the device to make sure it exists.
NOTE: Replace references to dm_dump_all() with dm_dump_tree() in 913d830cf093c10ca3233038e81c11beb63ec802 merge.

Example output of using dm_dump_all() in sandbox_spl_defconfig:

.. code-block:: C

  $ ./spl/u-boot-spl -d ./spl/u-boot-spl.dtb 
  sandbox: starting...

  U-Boot SPL 2021.04-dirty (Apr 03 2025 - 08:57:14 +0300)
  os_spl_to_uboot
  sandbox: starting...


  U-Boot 2021.04-dirty (Apr 03 2025 - 08:57:14 +0300)

   Class     Index  Probed  Driver                Name
  -----------------------------------------------------------
   root          0  [ + ]   root_driver           root_driver
   rsa_mod_ex    0  [   ]   mod_exp_sw            |-- mod_exp_sw
   timer         0  [ + ]   sandbox_timer         |-- sandbox_timer
   serial        0  [   ]   sandbox_serial        |-- sandbox_serial
   clk           0  [   ]   fixed_clock           |-- clk-fixed
   simple_bus    0  [   ]   simple_bus            |-- test-bus
   serial        1  [ + ]   sandbox_serial        `-- serial
  Model: sandbox
  DRAM:  128 MiB
  MMC:   
  In:    serial
  Out:   serial
...
                                   

common structures
=================

.. code-block:: C

  /**                                                                       
   * struct driver - A driver for a feature or peripheral                   
   *                                                                        
   * This holds methods for setting up a new device, and also removing it.  
   * The device needs information to set itself up - this is provided either
   * by platdata or a device tree node (which we find by looking up         
   * matching compatible strings with of_match).                            
  ...
   */
  struct driver {
  »       char *name;
  »       enum uclass_id id;
  ...
  »       int (*bind)(struct udevice *dev);
  »       int (*probe)(struct udevice *dev);
  »       int (*remove)(struct udevice *dev);
  »       int (*unbind)(struct udevice *dev);
  ...

  /**                                                                   
   * struct udevice - An instance of a driver                           
   *                                                                    
   * This holds information about a device, which is a driver bound to a
   * particular port or peripheral (essentially a driver instance).     
  ...
   */
  struct udevice {
  »       const struct driver *driver;
  »       const char *name;
  »       void *platdata;
  ...
  »       struct udevice *parent;
  »       void *priv;            
  »       struct uclass *uclass; 
  »       void *uclass_priv;     
  »       void *parent_priv;     
  ...

  /**                                                                   
   * struct uclass - a U-Boot drive class, collecting together similar drivers
   *                                                                          
   * A uclass provides an interface to a particular function, which is        
   ...
   */
  struct uclass {                        
  »       void *priv;                    
  »       struct uclass_driver *uc_drv;  
  »       struct list_head dev_head;     
  »       struct list_head sibling_node; 
  };                                     

  /**                                            
   * struct uclass_driver - Driver for the uclass
  ...
   */
  struct uclass_driver {                         
  »       const char *name;                      
  »       enum uclass_id id;                     
  »       int (*post_bind)(struct udevice *dev); 
  »       int (*pre_unbind)(struct udevice *dev);
  »       int (*pre_probe)(struct udevice *dev); 
  »       int (*post_probe)(struct udevice *dev);
  »       int (*pre_remove)(struct udevice *dev);
  ...

uclass_id enums are stored in ./include/dm/uclass-id.h:
-------------------------------------------------------

.. code-block:: C

  /* TODO(sjg@chromium.org): this could be compile-time generated */   
  enum uclass_id {                                                     
  »       /* These are used internally by driver model */              
  »       UCLASS_ROOT = 0,                                             
  »       UCLASS_DEMO,                                                 
  »       UCLASS_TEST,                                                 
  »       UCLASS_TEST_FDT,                                             
  »       UCLASS_TEST_BUS,                                             
  ...

U-Boot configuration parameters
===============================

**CONFIG_SYS_LOAD_ADDR** - address in memory to use by default. For example used by default for "kernel image address (**addr**)" in "booti" or for "address of FIT to boot (**fit_addr / fit_addr2 / fit_addr3**)" in bootm;

**CONFIG_STACK_SIZE** - Define max stack size that can be used by U-Boot;

**CONFIG_TEXT_BASE** - Text Base. The address in memory that U-Boot will be copied and executed from initially;

**CONFIG_SYS_MALLOC_F_LEN** - Size of malloc() pool before relocation;

tftp
====

Links
=====

Excellent question and excellent answer `[U-Boot] Many questions about U-Boot's Driver Model <https://u-boot.denx.narkive.com/EBuc4U2v/many-questions-about-s-driver-model>`_
