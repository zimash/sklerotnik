==========================
kernel tinyconfig для qemu
==========================

Переходим в директорию, где находится ядро. Конфигурируем tinyconfig:

.. code-block:: shell

  $ make tinyconfig     # Configure the tiniest possible kernel

Но текущая конфигурация не содержит ряд опций (поддержка ФС, устройств, serial и т.д.), что требуется для полноценной работы в QEmu.

Что может потребоваться:

.. code-block:: shell

  CONFIG_64BIT               # Для сборки 64-битного ядра
  CONFIG_TTY                 # Поддержка TTY
  CONFIG_SERIAL_8250         # Поддержка 8250/16550 и совместимых
  CONFIG_SERIAL_8250_CONSOLE # Возможность использования последовательного порта как системной консолью
  CONFIG_PRINTK              # Включение поддержки printk

Это минимальное количество опций для сборки ядра и загрузки его в qemu.

Запуск:

.. code-block:: shell

  $ qemu-system-x86_64 -kernel arch/x86/boot/bzImage # Или
  $ qemu-system-x86_64 -kernel arch/x86/boot/bzImage -append "console=ttyS0" -nographic
