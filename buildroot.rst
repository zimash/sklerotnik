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
