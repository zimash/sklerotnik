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
   $ make show-info            # Generate info about packages, as a JSON blurb
   $ make pkg-stats            # Generate info about packages as JSON and HTML

   $ make linux-menuconfig     # Run Linux kernel menuconfig (Only work when linux is enabled)
   $ make busybox-menuconfig   # Run busybox menuconfig (Only works when busybox is enabled)
   $ make uclibc-menuconfig    # Run uclibc menuconfig (Only available when the uClibc C library is selected in the 
                                 internal toolchain backend)
   $ make barebox-menuconfig   # Run barebox menuconfig (Only work when the barebox bootloader is enabled)
   $ make uboot-menuconfig     # Run uboot menuconfig (Only work when the U-Boot bootloader is enabled and the uboot
                                 build system is set to Kconfig)

   $ make source               # Download all sources needed for offline-build (configuration dependent)
   $ make graph-depends        # Generate graph of the dependency tree

   # Notes. If ccache is enabled, running make clean or distclean does not empty the compiler cache used by Buildroot.
   $ make clean                # To delete all build products (including build directories, host, staging and target 
                                 trees, the images and the toolchain)
   $ make distclean            # Resetting Buildroot for a new target: To delete all build products as well as the 
                                 configuration 

* Directories::

                                    .---------.
                                    |         |
                                    | output/ |
                                    |         |
                                    '+-+-+-+-+'
                                     | | | | |
                .--------------------' | | | '--------------------.
                |            .---------' | '----------.           |
                |            |           |            |           |
           .----v----.   .---v----.  .---v---.  .-----v----. .----v----.
           |         |   |        |  |       |  |          | |         |
           | images/ |   | build/ |  | host/ |  | staging/ | | target/ |
           |         |   |        |  |       |  |          | |         |
           '---------'   '--------'  '---+---'  '-----+----' '---------'
                                         |            |
                                         |            '-----------.
                                         |                        | (symlink)
                      .------------------v------------------.     |
                      | $(ARCH)-buildroot-linux-gnu/sysroot <-----'
                      '-------------------------------------'

   board/                      - board specific files;
   configs/                    - board defconfigs;
   dl/                         - directory with downloaded archive/source files;
   output/images/              - where all the images (kernel image, bootloader and root filesystem images) are stored. 
                                 These are the files you need to put on your target system. 
   output/target/              - which contains almost the complete root filesystem for the target: everything needed 
                                 is present except the device files in /dev/ (Buildroot can’t create them because 
                                 Buildroot doesn’t run as root and doesn’t want to run as root). Also, it doesn’t have
                                 the correct permissions (e.g. setuid for the busybox binary). Therefore, this directory 
                                 should not be used on your target. Instead, you should use one of the images built in 
                                 the images/ directory. If you need an extracted image of the root filesystem for booting 
                                 over NFS, then use the tarball image generated in images/ and extract it as root. 
                                 Compared to staging/, target/ contains only the files and libraries needed to run the 
                                 selected target applications: the development files (headers, etc.) are not present, 
                                 the binaries are stripped. builded file system with OS that is used for final images;
   output/staging/             - is a symlink to the target toolchain sysroot inside host/, which exists for backwards
                                 compatibility. 
   output/host/                - contains both the tools built for the host, and the sysroot of the target toolchain. 
                                 The former is an installation of tools compiled for the host that are needed for the 
                                 proper execution of Buildroot, including the cross-compilation toolchain. The latter 
                                 is a hierarchy similar to a root filesystem hierarchy. It contains the headers and 
                                 libraries of all user-space packages that provide and install libraries used by 
                                 other packages. However, this directory is not intended to be the root filesystem 
                                 for the target: it contains a lot of development files, unstripped binaries and 
                                 libraries that make it far too big for an embedded system. These development files 
                                 are used to compile libraries and applications for the target that depend on other 
                                 libraries.;
   output/build/               - where all the components are built (this includes tools needed by Buildroot on the host 
                                 and packages compiled for the target). This directory contains one subdirectory for each
                                 of these components.

* `The package build targets are (in the order they are executed): <https://nightly.buildroot.org/#pkg-build-steps>`_
  
  Command/Target ::

   source:                     Fetch the source (download the tarball, clone the source repository, etc)
   depends                     Build and install all dependencies required to build the package
   extract                     Put the source in the package build directory (extract the tarball, copy the source, etc)
   patch                       Apply the patches, if any
   configure                   Run the configure commands, if any
   build                       Run the compilation commands
   install-staging             target package: Run the installation of the package in the staging directory, if necessary
   install-target              target package: Run the installation of the package in the target directory, if necessary
   install                     target package: Run the 2 previous installation commands
                               host package: Run the installation of the package in the host directory

* Types of packages (the recipes are stored in package/pkg-*.mk files)::

   autotools-package           $(eval $(autotools-package)) and $(eval $(host-autotools-package))   
   cargo-package               $(eval $(cargo-package)) and $(eval $(host-cargo-package)) 
   cmake-package               $(eval $(cmake-package)) and $(eval $(host-cmake-package))               
   generic-package             $(eval $(generic-package)) and $(eval $(host-generic-package))
   golang-package              $(eval $(golang-package)) and $(eval $(host-golang-package))
   kconfig-package             $(eval $(kconfig-package))
   kernel-module               $(eval $(kernel-module))
   luarocks-package            $(eval $(luarocks-package))
   meson-package               $(eval $(meson-package)) and $(eval $(host-meson-package))
   perl-package                $(eval $(perl-package)) and $(eval $(host-perl-package))
   python-package              $(eval $(python-package)) and $(eval $(host-python-package))
   qmake-package               $(eval $(qmake-package)) 
   rebar-package               $(eval $(rebar-package)) and $(eval $(host-rebar-package))
   virtual-package             $(eval $(virtual-package)) and $(eval $(host-virtual-package))
   waf-package                 $(eval $(waf-package)) and 

* Variables::

   TOPDIR                      - the root directory of buildroot, for example - TOPDIR=~/git/buildroot 
   BASE_DIR                    - $(TOPDIR)/output/host, for example - HOST_DIR=~/git/buildroot/output
   HOST_DIR                    - $(TOPDIR)/output/host, for example - HOST_DIR=~/git/buildroot/output/host
   STAGING_DIR                 - $(TOPDIR)/output/host/<ARCH>/sysroot, for example:
                                 STAGING_DIR=~/git/buildroot/output/host/i686-buildroot-linux-gnu/sysroot
                                 STAGING_DIR=~/git/buildroot/output/host/aarch64-buildroot-linux-gnu/sysroot
   TARGET_DIR                  - $(TOPDIR)/output/target, for example TARGET_DIR=~/git/buildroot/output/target
   BUILD_DIR                   - $(TOPDIR)/output/build, for example BUILD_DIR=~/git/buildroot/output/build

* If we are working on some project, for example on the Linux kernel or something else, we can override the 
  original code of the project (in general it will not be downloaded during the execution of ``make [pkg_]source``).
  We need to add local.mk file with a line::

   LINUX_OVERRIDE_SRCDIR=/path/to/where/you/cloned/linux_kernel
   

* Other::

   Buildroot can be built with -j $(nproc) argument. This option allows you to build multiple packages
   at the same time. But it option is experimental and works well in unpstream
   buildroot. To enable this feature we must set BR2_PER_PACKAGES_DIRECTORY to 'y'.

   

Links
-----

* `General Buildroot usage <https://bootlin.com/~thomas/site/buildroot/common-usage.html>`_
