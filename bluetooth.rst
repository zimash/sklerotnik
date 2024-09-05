=========
Bluetooth
=========

Слои
====

.. list-table:: Host Part:
   :widths: 25 25
   :header-rows: 1

   * - Layer
     - Required Features
   * - L2CAP
     - L2CAP Signaling Channel (CID 0x0001) and all mandatory features associated with it
   * - SDP
     - All mandatory features
   * - ATT
     - If ATT is supported, all mandatory features
   * - GATT
     - GATT is optional when the ATT is supported. When supported, all mandatory features.
   * - GAP
     - All mandatory features in sections 2 through 8

.. list-table:: Controller Part:
   :widths: 25 25
   :header-rows: 1

   * - Layer
     - Required Features
   * - RF
     - All mandatory features
   * - BB
     - All mandatory features
   * - LMP
     - All mandatory features

Сэр Глоссарик Терминов
======================
* L2CAP - Logical Link Control and Adaptation Protocol
* SDP - Service Discovery Protocol
* ATT - Attribute Protocol
* GATT - Generic Attribute Profile
* GAP - Generic Access Profile
* RF - Radio Specification
* BB - Baseband Specification
* LMP - Link Manager Protocol
