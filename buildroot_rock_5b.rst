======================================
Сборка Buildroot для Radxa ROCK 5B [1]
======================================

99% описания подходит для остальных преподготовленных `_defconfig-ов`, при отсутствии необходимости в кастомизации.

Выполняем::

  $ git clone https://github.com/buildroot/buildroot 
  $ cd buildroot
  $ git worktree add ../buildroot.2024.8.1 2024.8.1 # создаём worktree для тэга 2024.8.1 или иного, нам необходимого
  $ cd ../buildroot.2024.8.1
  $ make rock5b_defconfig
  $ ./utils/config --enable BR2_PER_PACKAGE_DIRECTORIES
  $ make -j $(nproc)

Links
-----

[1] `Radxa ROCK 5B <http://radxa.com/products/rock5/5b/>`_
