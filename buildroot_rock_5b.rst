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
  $ make -j $(nproc) source # (опционально), если мы хотим однажды скачать исходники и что-то с ними делать и т.д.
  $ make -j $(nproc) # если пропустить предыдущую команду, будут также скачиваться, по мере необходимости, исходники
  $ ls output/images/
  Image                  rk3588_ddr_lp4_2112MHz_lp5_2736MHz_v1.12.bin  rootfs.ext2  rootfs.tar  u-boot.bin
  rk3588_bl31_v1.40.elf  rk3588-rock-5b.dtb                            rootfs.ext4  sdcard.img  u-boot-rockchip.bin

В артефактах находится rootfs.* и sdcard.img, которые мы можем записать на загрузочную флешку.
А также u-boot*, что можно прошить из загруженной системы, при наличии драйвера устройства [2], при этом стоить
заметить, что он уже присутствует в собранном образе. 

Links
-----

[1] `Radxa ROCK 5B <http://radxa.com/products/rock5/5b/>`_

[2] `Build Vendor U-Boot on Rock 5B Flash U-Boot <https://wiki.radxa.com/Rock5/guide/build-u-boot-on-5b/>`_
