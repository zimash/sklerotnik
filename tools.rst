=====
Tools
=====

gdb
---

Build gdb for multi-target usage::

   $ git clone https://sourceware.org/git/binutils-gdb.git
   $ cd binutils-gdb
   $ ./configure --enable-targets=all
   $ make -j $(nproc)
