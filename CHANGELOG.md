# PCB Revisions Changelog

* v0.1 (no version number printed)
  * Connected HUB75 pins successfully!
  * 4x GPIO, 2x 3V3, 2x GND pins broken out
  * 2x screw terminals to share power
  * 1x Capacitor to smooth input power
  * Power traces wide enough to support 2.3A sustained sourced from Micro-USB port.


* v1.0
  * Added version number silkscreen. And Furret!
  * Add option to output to HUB75 socket using ribbon cable (Mode 1) instead of plugging directly into LED panel (Mode 0).
  * Increased power traces width to the maximum possible width. Ampacity TBD.
  * Simplified assembly instructions added to silkscreen to prevent accidental mistakes!
  * 9 GPIO (all pins used!), 3x 3V3, 3x GND pins broken out
  * Consolidated 5V and GND each to their own screw terminal, so you can securely screw in default HUB75 power connectors.


* v1.1
  * Added SMD capacitor to allow the ESP32-DEVKIT-V1 to automatically load the bootloader. Now you don't need to press the `EN` button to upload new firmware.
  * Consolidated power traces to one layer each.
  