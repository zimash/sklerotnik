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
