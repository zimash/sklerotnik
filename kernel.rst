Configure
=========
.. code-block:: shell

  make config     # text-based
  make menuconfig # ncurses based
  make gconfig    # gtk+ based graphical utility
  make defconfig  # creates configuration based on the defaults for your architectures
  make oldconfig  # validate and update the configuration before

Using utilities such as the excellent distcc and ccache can also dramatically improve 
kernel build time.

Compile
=======
.. code-block:: shell

  zcat /proc/config.gz > ./.config # or make defconfig or cp /boot/config-$(uname -r) ./
  make mrproper #
  make clean # or make distclean 
  make [-j $(nproc)] # After 2.6 kernel, no need to run $ make dep before building kernel
  make -C /lib/modules/$(uname -r)/build M=$PWD [modules] # build modules
  make -C /lib/modules/$(uname -r)/build M=$PWD clean # clean builded files

Installing the new kernel
=========================
.. code-block:: shell

  make modules_install # This install all the compiled modules to their correct home under /lib/modules
  make install         # Install kernel using (your) ~/bin/installkernel or (distribution) /sbin/installkernel
                       # or install to $(INSTALL_PATH) and run lilo

Build external modules (without full compilation of the kernel)
===============================================================
.. code-block:: shell

  make <CONFIG>                    # Prepare the necessary configuration
  make modules_prepare             # Set up for building external modules
  make M=<path_to_module> modules  # Build module

* `Building External Modules <https://docs.kernel.org/kbuild/modules.html>`_

Process state
=============
.. code-block:: shell

  TASK_RUNNING         - The process is runnable;
  TASK_INTERRUPTIBLE   - The process is sleeping (that is, it is blocked), waiting for some condition to exist;
  TASK_UNINTERRUPTIBLE - This state is identical to TASK_INTERRUPTIBLE except that is does not wake up and become runnable if it receives a signal;
  __TASK_TRACED        - The process is being traced by another process, such as a debugger, via ptrace;
  __TASK_STOPPED       - Process execution has stopped; the task is not running nor is it eligible to run;

Manupulating the current process state
======================================
.. code-block:: C
  
  set_task_state(task, state); /* set task `task` to state `state` */
  set_current_state(state);    /* is synonymous to set_task_state(current, state) */

Error Codes
===========
* `errno-base.h <https://elixir.bootlin.com/linux/latest/source/include/uapi/asm-generic/errno-base.h>`_
* `errno.h <https://elixir.bootlin.com/linux/latest/source/include/uapi/asm-generic/errno.h>`_

Firewalls
=========
.. code-block:: C

  NF_DROP 0
  NF_ACCEPT 1
  NF_STOLEN 2
  NF_QUEUE 3
  NF_REPEAT 4

Linux Kernel start
==================
* If we have a NAND flash with UBIFS and we want to boot our system (kernel and initd) from it, in the line of
  booting the kernel, we need to add a line similar to:
.. code-block:: bash

  APPEND console=ttyS0,115200n8 earlycon ubi.mtd=0 root=ubi0:boot rootfstype=ubifs rw rootwait

  # Arguments
  ubi.mtd=0         # mtd device
  rootfstype=ubifs  # type of fs
  root=ubi0:boot    # root partition with label, in this example it is `boot`

Links
=====

* `KUnit - Linux Kernel Unit Testing » Getting Started <https://docs.kernel.org/dev-tools/kunit/start.html>`_
* `Linux Device Driver Tutorial <https://embetronicx.com/linux-device-driver-tutorials/>`_
* `Linux kernel source <https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git>`_
* `Linux Test Project <https://linux-test-project.readthedocs.io/en/latest/>`_
* `Majordomo lists at VGER.KERNEL.ORG <http://vger.kernel.org/vger-lists.html>`_
* `vger.kernel.org <https://subspace.kernel.org/vger.kernel.org.html>`_
