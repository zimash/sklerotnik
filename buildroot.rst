=========
Buildroot
=========

* Some useful commands::

   $ make -s printvars VARS=%  # -s, --silent, --quiet
                               # printvars - dump internal variables selected with VARS=...

   $ make V=0|1 # 0=> quiet build (default), 1 => verbose build
   $ make <pkg>-source         # Only download the source files for <pkg>
   $ make <pkg>-rebuild        # Restart the build from the build step
   $ make <pkg>-dirclean       # Remove <pkg> build directory
   $ make menuconfig           # Interactive curses-based configurator
   $ make list-defconfigs      # Display the list of boards with a defconfig

   $ make linux-menuconfig     # Run Linux kernel menuconfig (Only work when linux is enabled)
   $ make busybox-menuconfig   # Run busybox menuconfig (Only works when busybox is enabled)
   $ make uclibc-menuconfig    # Run uclibc menuconfig (Only available when the uClibc C library is selected in the internal toolchain backend)
   $ make barebox-menuconfig   # Run barebox menuconfig (Only work when the barebox bootloader is enabled)
   $ make uboot-menuconfig     # Run uboot menuconfig (Only work when the U-Boot bootloader is enabled and the uboot build system is set to Kconfig)

   $ make source               # Download all sources needed for offline-build (configuration dependent)
   $ make graph-depends        # Generate graph of the dependency tree

   # Notes. If ccache is enabled, running make clean or distclean does not empty the compiler cache used by Buildroot.
   $ make clean                # To delete all build products (including build directories, host, staging and target trees, the images and the toolchain)
   $ make distclean            # Resetting Buildroot for a new target: To delete all build products as well as the configuration 

* Directories::

   board                       - board specific files;
   configs                     - board defconfigs;
   dl                          - directory with downloaded archive/source files;
   output/target               - builded file system with OS that is used for final images;
   output/host                 - host-tools for buildingl;
   output/build                - created packages.

* Variables::

   TOPDIR                      - the root directory of buildroot, for example - TOPDIR=~/git/buildroot 
   BASEDIR                     - $(TOPDIR)/output/host, for example - HOST_DIR=~/git/buildroot/output/host
   STAGING_DIR                 - $(TOPDIR)/output/host/<ARCH>/sysroot, for example - STAGING_DIR=~/git/buildroot/output/host/i686-buildroot-linux-gnu/sysroot
   TARGET_DIR                  - $(TOPDIR)/output/target, for example TARGET_DIR=~/git/buildroot/output/target
   BUILD_DIR                   - $(TOPDIR)/output/build, for example BUILD_DIR=~/git/buildroot/output/build

Links
-----

* `General Buildroot usage <https://bootlin.com/~thomas/site/buildroot/common-usage.html>`_
