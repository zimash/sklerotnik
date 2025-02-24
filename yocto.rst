=============
Yocto Project
=============

Components:
----------
* BitBake - the Yocto Project build engine;


Build::

   $ git clone git://git.yoctoproject.org/poky
   $ source <pokypath>/oe-init-build-env [builddir] # directory with build name will be created by default
   $ bitbake core-image-sato 

  
Usage BitBake::

   $ bitbake <build target>
   $ bitbake core-image-sato             # creates a root file system image
   $ bitbake -c fetchall core-image-sato # only download all the sources without buidling
   $ bitbake -k core-image-sato          # continue building even if it encounters an error condition
   $ runqemu qemux86                     # prepare qemu environment and launches the emulator
