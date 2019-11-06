# Drive HUB75 LED panels using an ESP32-DEVKIT-V1 and SmartMatrix library
[![Demo](https://github.com/rorosaurus/esp32-hub75-driver/raw/master/images/demo.gif)](https://www.youtube.com/watch?v=UengvMiGzF8)

## Features
* Play animated .gifs on your LED panel using [SmartMatrix](https://github.com/pixelmatix/SmartMatrix/tree/teensylc) and [Marc Merlin's AnimatedGIFs sketch](https://github.com/marcmerlin/AnimatedGIFs)!
* Compatible with FastLED as well!
* ESP32 provides 2.4GHz Wifi/Bluetooth capability, and is Arduino compatible!
* The PCB connects all 16 pins needed to drive HUB75 panels using [`ESP32_FORUM_PINOUT`](https://github.com/pixelmatix/SmartMatrix/blob/teensylc/src/MatrixHardware_ESP32_V0.h#L37) from SmartMatrix library.
  * Compatible with 1/8, 1/16, and 1/32 scan type HUB75 panels.
  * Supports multiple HUB75 panels daisy-chained in series!
* Two different ways to connect to your LED panel:
  * Output Mode 0: directly plug this PCB into your LED panel using 2x8 female pin headers.
  * Output Mode 1: connect this PCB to your LED panel via 16 pin IDC ribbon cable.
* Two screw terminals to manage `5V` power flow between ESP32 and your LED panels.
* 3x5 = 15 pins broken out for additional use: 
  * 3x `GND`
  * 3x `3.3V`
  * 9x GPIO pins (8 with ADC!): for buttons, potentiometers, sensors, etc.!
* Optional pads for one through-hole Electrolytic Capacitor (I use 1000uF) to smooth the `5V` power.
* Optional pads for one 1206 SMD Ceramic Capacitor (I use 10uF) to enable the automatic bootloader. No need to press buttons to upload new firmware!

## Assembly Instructions
Full assembly instructions and more detailed information can be found here: [`ASSEMBLY.md`](https://github.com/rorosaurus/esp32-hub75-driver/blob/master/ASSEMBLY.md)

## Hardware
For a list of required and optional components, please see [`HARDWARE.md`](https://github.com/rorosaurus/esp32-hub75-driver/blob/master/HARDWARE.md)

## Software
For links to software I recommend using with this board, please see [`SOFTWARE.md`](https://github.com/rorosaurus/esp32-hub75-driver/blob/master/SOFTWARE.md)

Please note: my shield works with [SmartMatrix](https://github.com/pixelmatix/SmartMatrix/tree/teensylc) library, not [PxMatrix](https://github.com/2dom/PxMatrix).

## PCB Design
Latest board revision is v1.1.

See [`CHANGELOG.md`](https://github.com/rorosaurus/esp32-hub75-driver/blob/master/CHANGELOG.md) for more information about board revisions.

Gerber file download: [`/gerber/esp32-hub75-driver.zip`](https://github.com/rorosaurus/esp32-hub75-driver/blob/master/gerber/esp32-hub75-driver.zip)


## FAQ
I plugged everything in, and I don't see anything on my LED panel!
* Is your code configured correctly? Right pinout? Right panel size, scantype, etc.?
* Is the PCB plugged into the panel correctly?  It's possible to accidently plug in 1 pin too high or too low on the panel input. Check it is properly inserted and each pin aligns properly.