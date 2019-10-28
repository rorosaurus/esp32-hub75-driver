# Drive HUB75 LED panels using an ESP32-DEVKIT-V1 and SmartMatrix library
[![Demo](images/demo.gif)](https://www.youtube.com/watch?v=UengvMiGzF8)

## Features
* Connects all 16 pins to drive HUB75 panels using `ESP32_FORUM_PINOUT` from [MatrixHardware_ESP32_V0.h](https://github.com/pixelmatix/SmartMatrix/blob/teensylc/src/MatrixHardware_ESP32_V0.h)
  * Mode 0: directly plug into LED panelOne 16 pin IDC output which supports multiple HUB75 panels daisy-chained in series
  * Mode 1: connect to LED panel via 16 pin IDC cable
* Two screw terminals to allow you to share 5V and GND from the Micro-USB input to your panels.
  * Traces are wide enough to support TODO:TBD total Amps
* 3x5 = 15 pins broken out for additional use: 
  * 3x GND
  * 3x 3.3V: The devkit's LDO can probably spare up to ~0.5A.
  * 9x GPIO (8 with ADC!): for buttons, potentiometers, sensors, etc.!
* Optional pads for one through-hole Electrolytic Capacitor (I use a 1000uF) to smooth the 5V power.
* Optional pads for one SMD Ceramic Capacitor (I use 10uF) to enable the automatic bootloader. No more pressing buttons to upload new firmware!

## Assembly Instructions
Full assembly instructions and more detailed information can be found here: [`ASSEMBLY.md`](ASSEMBLY.md)

## Hardware
For a list of required and optional components, please see [`HARDWARE.md`](HARDWARE.md)

## Software
For links to software I recommend using with this board, please see [`SOFTWARE.md`](SOFTWARE.md)

## PCB Design

Latest board revision is v1.1.

See [`CHANGELOG.md`](CHANGELOG.md) for more information about board revisions.

Gerber file download: [`/gerber/esp32-hub75-driver.zip`](https://github.com/rorosaurus/esp32-hub75-driver/blob/master/gerber/esp32-hub75-driver.zip)
