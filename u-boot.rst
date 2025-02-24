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

      

tftp
====
