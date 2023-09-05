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
   $ make linux-menuconfig     # Run Linux kernel menuconfig
   $ make source               # Download all sources needed for offline-build (configuration dependent)
   $ make graph-depends        # Generate graph of the dependency tree

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
