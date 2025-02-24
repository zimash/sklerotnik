===============
Cross-compiling
===============

Accompanying Go arguments
-------------------------

More known OS and architectures can be found `here <https://github.com/golang/go/blob/master/src/go/build/syslist.go>`_.

.. list-table:: GOOS:
   :widths: 25 25
   :header-rows: 1

   * - OS
     - $GOOS
   * - Linux
     - linux
   * - MacOS X
     - darwin
   * - Windows
     - windows
   * - FreeBSD
     - freebsd

.. list-table:: GOARCH:
   :widths: 25 25
   :header-rows: 1

   * - Architecture
     - $GOARCH
   * - x386
     - 386
   * - AMD64
     - amd64
   * - ARM
     - arm

.. list-table:: GOARM + GOARCH:
   :widths: 25 25 25 25
   :header-rows: 1

   * - Architecture
     - Status
     - GOARM value
     - GOARCH value
   * - ARMv5
     - supported
     - GOARM=5
     - GOARCH=arm
   * - ARMv6
     - supported
     - GOARM=6
     - GOARCH=arm
   * - ARMv7
     - supported
     - GOARM=7
     - GOARCH=arm
   * - ARMv8
     - supported
     - n/a
     - GOARCH=arm64
