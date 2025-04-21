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


elixir
------

Elixir is a source code cross-referencer inspired by `[XLR] <https://en.wikipedia.org/wiki/LXR_Cross_Referencer>`_.
And this is just a great project from Bootlin company.

`Bootlin, https://elixir.bootlin.com/ <https://elixir.bootlin.com>`_
`The Elixir Cross Referencer (source code) <https://github.com/bootlin/elixir>`_
