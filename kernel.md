* configure
```
make config     # text-based
make menuconfig # ncurses based
make gconfig    # gtk+ based graphical utility
make defconfig  # creates configuration based on the defaults for your architectures
make oldconfig  # validate and update the configuration before
```

Using utilities such as the excellent distcc and ccache can also dramatically improve 
kernel build time.

* compile

```
zcat /proc/config.gz > ./.config # or make defconfig or cp /boot/config-$(uname -r) ./
make mrproper #
make clean # or make distclean 
make [-j $(nproc)] # After 2.6 kernel, no need to run $ make dep before building kernel
make -C /lib/modules/$(uname -r)/build M=$PWD [modules] # build modules
make -C /lib/modules/$(uname -r)/build M=$PWD clean # clean builded files
```

* installing the new kernel
```
make modules_install # This install all the compiled modules to their correct home under /lib/modules
make install         # Install kernel using (your) ~/bin/installkernel or (distribution) /sbin/installkernel
                     # or install to $(INSTALL_PATH) and run lilo
```

* Process state
```
TASK_RUNNING         - The process is runnable;
TASK_INTERRUPTIBLE   - The process is sleeping (that is, it is blocked), waiting for some condition to exist;
TASK_UNINTERRUPTIBLE - This state is identical to TASK_INTERRUPTIBLE except that is does not wake up and become runnable if it receives a signal;
__TASK_TRACED        - The process is being traced by another process, such as a debugger, via ptrace;
__TASK_STOPPED       - Process execution has stopped; the task is not running nor is it eligible to run;
```

* Manupulating the current process state
```
set_task_state(task, state); /* set task `task` to state `state` */
set_current_state(state); /* is synonymous to set_task_state(current, state) */
```

* Firewalls

NF_DROP 0
NF_ACCEPT 1
NF_STOLEN 2
NF_QUEUE 3
NF_REPEAT 4


# LINKS
* [KUnit - Linux Kernel Unit Testing » Getting Started](https://docs.kernel.org/dev-tools/kunit/start.html)
* [Linux kernel source](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git)
* [Linux Device Driver Tutorial](https://embetronicx.com/linux-device-driver-tutorials/)
