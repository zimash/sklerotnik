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

tftp
====
